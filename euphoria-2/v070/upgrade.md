# Guide to upgrade Aurad to version v0.7.0

## Get aurad v0.7.0

- Clone the source code with specific branch

```
git clone --branch euphoria_v0.7.0 https://github.com/aura-nw/aura
```

- Build aurad:
```
cd aura
make build

# Verify the version
./build/aurad version
# returns euphoria_v0.7.0
```
## Upgrade

### Important Note
- This is upgrade requires migration steps from cosmos sdk 0.45 to 0.47, it takes about 20 minutes for running migrations
- At least **16GB RAM** is required to perform this upgrade

There are 2 ways to upgrade aurad: manually and automatically

### Manually upgrade after network halts

Euphoria network will halt after reaches block **7,097,820**, estimated at **Oct 18th 2023, 13:00 UTC**.

After that, follow steps bellow to upgrade:
- Stop aurad service
- Replace the current aurad with the new one
- Start the aurad service

### Automatic upgrade with cosmovisor
- Set up cosmovisor: https://docs.aura.network/validator/setting-up-cosmovisor
- Make an upgrade folder:
```
mkdir -p $DAEMON_HOME/cosmovisor/upgrades/v0.7.0/bin
```
- Copy the aurad v0.7.0 to the `bin` folder
```
cp ./build/aurad $DAEMON_HOME/cosmovisor/upgrades/v0.7.0/bin
```

Cosmovisor will automatically replace the `aurad` when the network reaches block **7,097,820**.
