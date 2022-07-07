# Setup genesis validator node

Below are the instructions to generate your genesis transaction.

## Generate genesis transaction (pre-launch only)

1. Download the lastest **Euphoria** pre-release from [aurad repo](https://github.com/aura-nw/aura) and run `make` to build the source.
   Or clone source code from the repo
   ```bash
   git clone https://github.com/aura-nw/aura
   cd aura
   git checkout euphoria
   make
   ```
   
2. Initialize the  directories and create the local genesis file with the correct
   chain-id

   ```bash
   aurad config chain-id euphoria-1
   aurad init <MONIKER-NAME> --chain-id euphoria-1
   ```

3. Create a local key pair for creating validator

   ```bash
   aurad keys add <key-name>
   ```

4. Download the pre-genesis file:

   ```bash
   curl -s https://raw.githubusercontent.com/aura-nw/testnets/main/euphoria-1/pre-genesis.json >~/.aura/config/genesis.json
   ```

5. Create the gentx, replace `<key-name>`:

   The number of bonded tokens must be 3600eaura
   
   ```bash
   aurad add-genesis-account <key-name> 3600000000ueaura
   aurad gentx <key-name> 3600000000ueaura [flags] --chain-id euphoria-1
   ```
   
   Flags:
   ```
   --commission-rate                   The initial commission rate percentage
   --commission-max-rate               The maximum commission rate percentage
   --commission-max-change-rate        The maximum commission change rate percentage (per day)
   --min-self-delegation               The minimum self delegation required on the validator
   --moniker                           The validator's moniker
   --details                           The validator's details
   --website                           The validator's website
   ```
   Example:
   ```bash
   aurad gentx aura-wallet 3600000000ueaura --commission-rate 0.05 --commission-max-rate 0.1 --commission-max-change-rate 0.01 --min-self-delegation 1 --moniker "aura-validator" --details "The aura validator details" --website "https://aura.network"  
   ```

   If all goes well, you will see a message similar to the following:

   ```bash
   Genesis transaction written to "/home/[user]/.aurad/config/gentx/gentx-******.json"
   ```

## Submit gentx and logo

1. Fork this repository 

2. Upload your logo (optional) and gentx with format:
   
   ```
   gentx-<validator-name>.json
   <validator-adress>.png
   ```

   Example:
   ```
   gentx-auranode.json
   auravaloper1u09a7hv2r7jmx8ndtrykm0xt3ywcsmvxgtghgt.png
   ```

3. Create a pull request to our main branch
Sample PR: [Link](https://github.com/aura-nw/testnets/pull/4)

### Download finalized genesis and setup your validator

1. Download genesis:

   ```bash
   curl -s <TBA> >~/.aura/config/genesis.json
   ```
2. Setup your nodes and services

   Docs: [Link](https://docs.aura.network/validator/running-a-fullnode)

3. Start the service and wait until the genesis time
