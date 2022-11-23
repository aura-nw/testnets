# Guide to launch Euphoria-2

We are forking Euphoria-2 from Euphoria-1 at block height **2000000**.

For validators who choose to not run Euphoria-2, please unbond and send back test tokens to our faucet address.

For those who want to support Euphoria-2, please follow steps below:

`Note`: To ensure the down time as little as possible, validators should init Euphoria-2 on the new machine, or on the same machine with Euphoria-1 but different home directory

- Download the latest Aura daemon
```
git clone --branch euphoria_v0.4.1 https://github.com/aura-nw/aura
```

- Init the Euphoria-2 home folder
```
export $HOME_PATH=<Euphoria-2 directory>
aurad init <moniker> --home $HOME_PATH
```

- Copy and replace `config/app.toml` and `config/config.toml` from Euphoria-1 to Euphoria-2
```
cp .aura/config/app.toml $HOME_PATH/config/
cp .aura/config/config.toml $HOME_PATH/config/
```

- Download the Euphoria-2 genesis
```
wget <TBD>
tar -xzvf euphoria-2-genesis.tar.gz
mv euphoria-2-genesis.json $HOME_PATH/config/genesis.json
```

- Vefify genesis information
```
cat $HOME_PATH/config/genesis.json | jq '"Genesis Time: " + .genesis_time + " — Chain ID: " + .chain_id + " - Initial Height: " + .initial_height'
# "Genesis Time: 2022-11-25T03:00:00Z — Chain ID: euphoria-2 - Initial Height: 2000001"
```

- Stop Euphoria-1, start Euphoria-2 and wait for launch time
```
aurad start --home $HOME_PATH
```
