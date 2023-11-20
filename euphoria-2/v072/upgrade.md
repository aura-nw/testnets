# Guide to upgrade Aurad to version v0.7.2

## Get aurad v0.7.2

You can download prebuilt binary or build it yourself
### Download release binary

- Download aurad
```
wget https://github.com/aura-nw/aura/releases/download/v0.7.2-euphoria/aurad
chmod +x aurad
```
- Verify version checksum
```
aurad verion
# returns v0.7.2-euphoria

sha256sum aurad
# returns 2d472071b50331fc6fe9f2beef8396ccbce1ee112b9b2905d6d554ac062e3601
```

### Build from source
- Clone the source code with specific branch

```
git clone --branch v0.7.2-euphoria https://github.com/aura-nw/aura
```

- Build aurad:
```
cd aura
make build

# Verify the version
./build/aurad version
# returns v0.7.2-euphoria
```
## Upgrade

There are 2 ways to upgrade aurad: manually and automatically

### Manually upgrade after network halts

Euphoria network will halt after reaches block **7,655,365**, estimated at **Nov 22nd 2023, 13:00 UTC**.

After that, follow steps bellow to upgrade:
- Stop aurad service
- Replace the current aurad with the new one
- Start the aurad service

### Automatic upgrade with cosmovisor
- Set up cosmovisor: https://docs.aura.network/validator/setting-up-cosmovisor
- Make an upgrade folder:
```
mkdir -p $DAEMON_HOME/cosmovisor/upgrades/v0.7.2/bin
```
- Copy the aurad v0.7.2 to the `bin` folder
```
cp ./build/aurad $DAEMON_HOME/cosmovisor/upgrades/v0.7.2/bin
```

Cosmovisor will automatically replace the `aurad` when the network reaches block **7,655,365**.
