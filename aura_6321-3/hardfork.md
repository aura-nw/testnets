# Guide to launch aura_6321-3

We are forking `aura_6321-3` from `euphoria-2` at block height **9993422**.

These are processes need to be done for this upgrade.

## Relayer

Since updating chain-id would break IBC client states, we need to perform the upgrade for client on every counterparty chains.

Relayers **MUST RUN** this command before the upgrade block **9993422**

```
hermes upgrade client --host-chain <<chain-id>> --client <<client-id>> --upgrade-height **9993422**
```

Example: Update Nois client 
```
hermes upgrade client --host-chain nois-testnet-005 --client 07-tendermint-46 --upgrade-height **9993422**
```
This command will check consecutively until Aura chain reachs the upgrade block and halts, then submit an upgrade ibc client transsaction to Nois chain.

## Validators and Full nodes

After Aura chain halts, follow below instructions: 

1. Stop aurad service
```
systemctl stop <<aurad service>>
```
2. Build new aurad version
```
git clone --branch v0.8.0-euphoria https://github.com/aura-nw/aura
cd aura
make build
# Verify the version
./build/aurad version
# returns v0.8.0-euphoria
```
3. Remove aurad old version and replace the new one
4. **BACK UP ALL PRIVATE KEYS**
5. Remove previous state
```
aurad tendermint unsafe-reset-all --home=$HOME/.aura
rm -r $HOME/.aura/wasm
```
6. Download new genesis file
```
wget << TBA >>
tar -xzvf aura_6321-3-genesis.tar.gz
mv aura_6321-3-genesis.json $HOME/config/genesis.json

# Verify genesis info
cat $HOME/.aura/config/genesis.json | jq '"Genesis Time: " + .genesis_time + " — Chain ID: " + .chain_id + " - Initial Height: " + .initial_height'
# this should return
# "Genesis Time: 2024-04-23T15:00:00Z — Chain ID: aura_6321-3 - Initial Height: 9993422"

# Verify sorted shasum
jq -S -c -M '' $HOME/.aura/config/genesis.json | sha256sum
# this should return
# TBA  -
```
7. Start aurad service
```
systemctl start <<aurad service>>
```
**IMPORTANT NOTE** 
- Starting from genesis requires load states from genesis file to database, it takes **more than 30 minutes** to start and consumes about **15.3 GB RAM**. 
- Please monitor resources carefully. In case aurad process is killed due to lack of RAM, restart service to try again or increase your RAM server to **larger than 16GB RAM**.

### Cosmovisor users

If you are using Cosmovisor to run your node, you can let Cosmovisor replace aurad bin file automatically
```
mkdir -p $HOME/.aura/cosmovisor/upgrades/hardfork/bin
cp ./build/aurad $HOME/.aura/cosmovisor/upgrades/hardfork/bin
```

Cosmovisor will start **FAILED** since it does not contain upgrade handler.

After that, STOP cosmovisor service and follow above instruction from **step 4**.
