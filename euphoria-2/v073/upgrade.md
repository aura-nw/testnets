# Guide to upgrade Aurad to version v0.7.3

## Get aurad v0.7.3

You can download prebuilt binary or build it yourself
### Download release binary

- Download aurad
```
wget https://github.com/aura-nw/aura/releases/download/v0.7.3-euphoria/aurad
chmod +x aurad
```
- Verify version checksum
```
aurad verion
# returns v0.7.3-euphoria

sha256sum aurad
# returns ff381b119f010736f49430de9d89fa794ea13b8d5dbb940357ab476b8cac6e82
```

### Build from source
- Clone the source code with specific branch

```
git clone --branch v0.7.3-euphoria https://github.com/aura-nw/aura
```

- Build aurad:
```
cd aura
make build

# Verify the version
./build/aurad version
# returns v0.7.3-euphoria
```
## Upgrade

There are 2 ways to upgrade aurad: manually and automatically

### Manually upgrade after network halts

Euphoria network will halt after reaches block **8,831,492**, estimated at **Feb 5 2024, 13:00 UTC**.

After that, follow steps bellow to upgrade:
- Stop aurad service
- Replace the current aurad with the new one
- Start the aurad service

### Automatic upgrade with cosmovisor
- Set up cosmovisor: https://docs.aura.network/validator/setting-up-cosmovisor
- Make an upgrade folder:
```
mkdir -p $DAEMON_HOME/cosmovisor/upgrades/v0.7.3/bin
```
- Copy the aurad v0.7.3 to the `bin` folder
```
cp ./build/aurad $DAEMON_HOME/cosmovisor/upgrades/v0.7.3/bin
```

Cosmovisor will automatically replace the `aurad` when the network reaches block **8,831,492**.
