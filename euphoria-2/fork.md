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

- Copy and replace `priv_validator_key.json` of your validator from Euphoria-1 to Euphoria-2
```
cp .aura/config/priv_validator_key.json $HOME_PATH/config/
```

- Download the Euphoria-2 genesis
```
wget https://github.com/aura-nw/testnets/raw/main/euphoria-2/euphoria-2-genesis.tar.gz
tar -xzvf euphoria-2-genesis.tar.gz
mv euphoria-2-genesis.json $HOME_PATH/config/genesis.json
```

- Vefify genesis information
```
cat $HOME_PATH/config/genesis.json | jq '"Genesis Time: " + .genesis_time + " — Chain ID: " + .chain_id + " - Initial Height: " + .initial_height'
# this should return 
# "Genesis Time: 2022-11-25T03:00:00Z — Chain ID: euphoria-2 - Initial Height: 2000001"
```

- Check sorted shasum
```
jq -S -c -M '' $HOME_PATH/config/genesis.json | sha256sum
# this should return
# 2b5efb277b7d49a290ea86bc2474c958ea12b9d42fd19da3cf259eb76961ed6c  -
```

- Stop Euphoria-1, start Euphoria-2 and wait for launch time
```
aurad start --home $HOME_PATH
```

- You can also add a service launch
```
sudo tee /etc/systemd/system/aurad.service > /dev/null <<EOF
[Unit]
Description=aurad
After=network-online.target

[Service]
User=$USER
ExecStart=$(which aurad) start
Restart=on-failure
RestartSec=3
LimitNOFILE=65535

[Install]
WantedBy=multi-user.target
EOF

sudo systemctl daemon-reload && \
sudo systemctl enable aurad && \
sudo systemctl restart aurad && sudo journalctl -u aurad -f -o cat
```
