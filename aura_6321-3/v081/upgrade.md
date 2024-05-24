# Guide to upgrade Aurad to version v0.8.1

## Get aurad v0.8.1

You can download prebuilt binary or build it yourself
### Download release binary

- Download aurad
```
wget https://github.com/aura-nw/aura/releases/download/v0.8.1-euphoria/aurad
chmod +x aurad
```
- Verify version checksum
```
aurad verion
# returns v0.8.1-euphoria

sha256sum aurad
# returns d3afe0b73f16e4ab76a080f45add2246b3f4c958421f9b0b4be0945f948565a3
```

### Build from source
- Clone the source code with specific branch

```
git clone --branch v0.8.1-euphoria https://github.com/aura-nw/aura
```

- Build aurad:
```
cd aura
make build

# Verify the version
./build/aurad version
# returns v0.8.1-euphoria
```
## Upgrade

There are 2 ways to upgrade aurad: manually and automatically

### Manually upgrade after network halts

Euphoria network will halt after reaches block **10,519,700**, estimated at **May 27 2024, 13:00 UTC**.

After that, follow steps bellow to upgrade:
- Stop aurad service
- Replace the current aurad with the new one
- Start the aurad service

### Automatic upgrade with cosmovisor
- Set up cosmovisor: https://docs.aura.network/validator/setting-up-cosmovisor
- Make an upgrade folder:
```
mkdir -p $DAEMON_HOME/cosmovisor/upgrades/v0.8.1/bin
```
- Copy the aurad v0.8.1 to the `bin` folder
```
cp ./build/aurad $DAEMON_HOME/cosmovisor/upgrades/v0.8.1/bin
```

Cosmovisor will automatically replace the `aurad` when the network reaches block **10,519,700**.
