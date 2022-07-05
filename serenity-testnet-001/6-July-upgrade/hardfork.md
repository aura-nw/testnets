# Hard fork upgrade

This upgrade is effectively a hard fork with the same chain-id. This means we'll need to delete all previous data and start from a new genesis.

NOTE: This assumes you've already ran through setting up a Aura node here: https://docs.aura.network/validator/running-a-fullnode

## Performing the  Upgrade

### 1. Stop the node
```sh
sudo systemctl stop <aurad_service>
```

### 2. Backup priv_validator_key.json
This is only relevant if you're upgrading your validator. Your priv_validator_key.json is how your validator is identified. If you haven't backed it up already, **DO SO NOW**.

An example method for doing so is as follows, which will copy your validator key to the home dir:
```sh
cd ~
cp ~/.aura/config/priv_validator_key.json .
```

*NOTE*: keeping your copy of the validator key on the same machine is NOT sufficient. At a bare minimum it should be backed up locally so you always have access to it.

### 3. Backup priv_validator_state.json
It's worth backing up your `priv_validator_state.json` in case this upgrade fails and an alternative path must be taken. 
```sh
cd ~
cp ~/.aura/data/priv_validator_state.json .
```

### 4. Purge previous chain state and addrbook.json
Because we'll be starting from a new genesis, the previous data is no longer necessary.
```sh
aurad unsafe-reset-all
```

### 5. Download and install the new binary

#### 5a. Install Aurad
This new binary includes the module upgrade.
```sh
git clone https://github.com/aura-nw/aura
cd aura
git checkout serenity
make 
```


#### 5b. [OPTIONAL] If you use cosmovisor
You will need to re-setup cosmovisor with the new genesis.
```sh
rm $DAEMON_HOME/cosmovisor/genesis/bin/aurad
rm -rf $DAEMON_HOME/cosmovisor/upgrades
mkdir $DAEMON_HOME/cosmovisor/upgrades
cp $HOME/go/bin/aurad $DAEMON_HOME/cosmovisor/genesis/bin
rm $DAEMON_HOME/cosmovisor/current
```

Check aurad has copied to the new location.
```sh
$DAEMON_HOME/cosmovisor/genesis/bin/aurad version
```

### 6. Download the upgrade genesis


```sh
rm ~/.aura/config/genesis.json
wget <genesis_link>
tar -xvf aura-upgrade-genesis.tar.gz -C $HOME/.aura/config

# check chain is serenity-testnet-001, genesis time is correct & initial block is ?
cat $HOME/.aura/config/genesis.json | jq '"Genesis Time: " + .genesis_time + " — Chain ID: " + .chain_id + " - Initial Height: " + .initial_height'
```

### 7. Verify genesis shasum

```sh
jq -S -c -M '' ~/.aura/config/genesis.json | sha256sum
?  -
```

### 8. Restore priv_validator_key.json and priv_validator_state.json

**Important** By resetting the state we also resetted the validator sign state, which may cause double sign. We need to restore our backup to prevent this. 

If you are using a remote signer this step is probably not needed

```sh
cp ~/priv_validator_state.json ~/.aura/data/priv_validator_state.json
cp ~/priv_validator_key.json ~/.aura/config/priv_validator_key.json
```

### 9. Start the node
```sh
sudo systemctl restart <aurad_service>
```

### 10. Confirm the process running
```sh
sudo journalctl -fu <aurad_service>
```
