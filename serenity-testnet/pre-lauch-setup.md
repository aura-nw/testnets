# Setup genesis validator node

Below are the instructions to generate your genesis transaction.

## Generate genesis transaction (pre-launch only)

1. Download the lastest serenity release from [aurad repo](https://github.com/aura-nw/aura) and run `make` to build the source.

2. Initialize the  directories and create the local genesis file with the correct
   chain-id

   ```bash
   aurad config chain-id serenity-testnet-001
   aurad init <MONIKER-NAME> --chain-id serenity-testnet-001
   ```

3. Create a local key pair

   ```bash
   aurad keys add <key-name>
   ```

4. Download the pre-genesis file:

   ```bash
   curl -s  https://raw.githubusercontent.com/aura-nw/testnets/main/serenity-testnet/pre-genesis.json >~/.aurad/config/genesis.json
   ```

5. Create the gentx, replace `<key-name>`:

   ```bash
   aurad gentx <key-name> 10000000000uaura --commission-rate=0.01 --chain-id serenity-testnet-001
   ```

   If all goes well, you will see a message similar to the following:

   ```bash
   Genesis transaction written to "/home/[user]/.aurad/config/gentx/gentx-******.json"
   ```
