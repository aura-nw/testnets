# Guide to upgrade Aurad to version v0.7.1

## Get aurad v0.7.1

You can download prebuilt binary or build it yourself
### Download release binary

- Download aurad
```
wget https://github.com/aura-nw/aura/releases/download/v0.7.1-euphoria/aurad
chmod +x aurad
```
- Verify version checksum
```
aurad verion
# returns v0.7.1-euphoria

sha256sum aurad
# returns 7f26f58b75c4fbabfac8a296c039042f9386793ef451f64cfcf560c0de101264
```

### Build from source
- Clone the source code with specific branch

```
git clone --branch v0.7.1-euphoria https://github.com/aura-nw/aura
```

- Build aurad:
```
cd aura
make build

# Verify the version
./build/aurad version
# returns v0.7.1-euphoria
```
## Upgrade

There are 2 ways to upgrade aurad: manually and automatically

### Manually upgrade after network halts

Euphoria network will halt after reaches block **7,545,433**, estimated at **Nov 15th 2023, 13:00 UTC**.

After that, follow steps bellow to upgrade:
- Stop aurad service
- Replace the current aurad with the new one
- Start the aurad service

### Automatic upgrade with cosmovisor
- Set up cosmovisor: https://docs.aura.network/validator/setting-up-cosmovisor
- Make an upgrade folder:
```
mkdir -p $DAEMON_HOME/cosmovisor/upgrades/v0.7.1/bin
```
- Copy the aurad v0.7.1 to the `bin` folder
```
cp ./build/aurad $DAEMON_HOME/cosmovisor/upgrades/v0.7.1/bin
```

Cosmovisor will automatically replace the `aurad` when the network reaches block **7,545,433**.
