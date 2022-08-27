# Guide to upgrade Aurad to version v0.3.0

## Get aurad v0.3.0

- Clone the source code with specific branch

```
git clone --branch euphoria_v0.3.0 https://github.com/aura-nw/aura
```

- Build aurad:
```
cd aura
make build

# Verify the version
./build/aurad version
# returns euphoria_v0.3.0
```
## Upgrade

There are 2 ways to upgrade aurad: manually and automatically

### Manually upgrade after network halts

Euphoria network will halt after reaches block 702290. After that, follow steps bellow to upgrade:
- Stop aurad service
- Replace the current aurad with the new one
- Start the aurad service

### Automatic upgrade with cosmovisor
- Set up cosmovisor: https://docs.aura.network/validator/setting-up-cosmovisor
- Make an upgrade folder:
```
mkdir -p $DAEMON_HOME/cosmovisor/upgrades/v0.3.0/bin
```
- Copy the aurad v0.3.0 to the `bin` folder
```
cp ./build/aurad $DAEMON_HOME/cosmovisor/upgrades/v0.3.0/bin
```

Cosmovisor will automatically replace the `aurad` when the network reaches block 702290.
