# Guide to upgrade Aurad to version v0.5.1

## Get aurad v0.5.1

- Clone the source code with specific branch

```
git clone --branch euphoria_v0.5.1 https://github.com/aura-nw/aura
```

- Build aurad:
```
cd aura
make build

# Verify the version
./build/aurad version
# returns euphoria_v0.5.1
```
## Upgrade

**IMPORTANT NOTE**: The security patch for Cosmwasm module requires removing cache after upgrade. Therefore this upgrade should be performed manually.

### Manually upgrade after network halts

Euphoria network will halt after reaches block **4,307,903** ~ Monday 24th, 02:00 AM UTC.

After that, follow steps bellow to upgrade:
- Stop aurad service
- Replace the current aurad with the new one
- Remove wasm cache folder
```
rm -r <aurad node home>/wasm/wasm/cache/
# replace with the location you setup aurad
```
- Start the aurad service
