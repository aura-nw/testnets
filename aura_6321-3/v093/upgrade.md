# Guide to upgrade Aurad to version v0.9.3-euphoria

## Get aurad v0.9.3-euphoria

You can download prebuilt binary or build it yourself
### Download release binary

- Download aurad
```
wget https://github.com/aura-nw/aura/releases/download/v0.9.3-euphoria/aurad
chmod +x aurad
```
- Verify version checksum
```
aurad verion
# returns v0.9.3-euphoria

sha256sum aurad
# returns e59686a2aa4fe2905357c90996b46c322e1da0220a0533012d1a662c0a174e6c
```

### Build from source
- Clone the source code with specific branch

```
git clone --branch v0.9.3-euphoria https://github.com/aura-nw/aura
```

- Build aurad:
```
cd aura
make build

# Verify the version
./build/aurad version
# returns v0.9.3-euphoria
```
## Upgrade

There are 2 ways to upgrade aurad: manually and automatically

### Manually upgrade after network halts

Euphoria network will halt after reaches block **11,679,500**, estimated at **August 9 2024, 13:00 UTC**.

After that, follow steps bellow to upgrade:
- Stop aurad service
- Replace the current aurad with the new one
- Start the aurad service

### Automatic upgrade with cosmovisor
- Set up cosmovisor: https://docs.aura.network/validator/setting-up-cosmovisor
- Make an upgrade folder:
```
mkdir -p $DAEMON_HOME/cosmovisor/upgrades/v0.9.3/bin
```
- Copy the aurad v0.9.3 to the `bin` folder
```
cp ./build/aurad $DAEMON_HOME/cosmovisor/upgrades/v0.9.3/bin
```

Cosmovisor will automatically replace the `aurad` when the network reaches block **11,679,500**.
