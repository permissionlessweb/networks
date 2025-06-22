# Go-Bitsong v0.23.0 - Gauss
|                 |                                                              |
|-----------------|--------------------------------------------------------------|
| Chain-id        | `bitsong-2b`                                                  |
| Upgrade Version | `v0.23.0`                                             |
| Upgrade Height  | `22990737`                                                    |


The target block for this upgrade is `22990737`, which is expected to arrive at `Thursday June 26th 2025, 15:00:00 UTC` [Chainroot Countdown](https://explorer.chainroot.io/bitsong/blocks/22990737)

## Building Manually:

### 1. Verify that you are currently running the correct version (v0.22.0) of `bitsongd`:

```sh
bitsongd version --long
# name: go-bitsong
# server_name: bitsongd
# client_name: bitsongcli
# version: 0.22.0
# commit: 
# build_tags: netgo,ledger
```

### 2. Make sure your chain halts at the right block: `22990737`
```sh
perl -i -pe 's/^halt-height =.*/halt-height = 22990737/' ~/.bitsongd/config/app.toml
```
then restart your node `systemctl restart bitsongd`

### 3. After the chain has halted, make a backup of your `.bitsongd` directory
```sh
cp -Rf ~/.bitsongd ./bitsongd_backup
```

**NOTE**: It is recommended for validators and operators to take a full data snapshot at the export height before proceeding in case the upgrade does not go as planned or if not enough voting power comes online in a sufficient and agreed upon amount of time. In such a case, the chain will fallback to continue operating `bitsong-2b`.
~z
 
### Option A: Install Go-Bitsong binary
```sh
git clone https://github.com/permissionlessweb/go-bitsong
cd go-bitsong && git pull && git checkout v0.23.0
make install 
```

### 5. Verify you are currently running the correct version (v0.23.0) of the `go-bitsong`:
```sh
bitsongd version --long | grep "cosmos_sdk_veresion/|commit\|version:"
# commit: TBD
# cosmos_sdk_version: v0.53.0
# version: 0.23.0
```

### Option B: Downloading Verified Build:
```sh
# set target platform
export PLATFORM_TARGET=amd64 #arm64
 # delete if exists
rm -rf bitsongd_linux_$PLATFORM_TARGET.tar.gz
# download 
curl -L -o ~/bitsongd-linux-$PLATFORM_TARGET.tar.gz https://github.com/bitsongofficial/go-bitsong/releases/download/v0.23.0/bitsongd-linux-$PLATFORM_TARGET.tar.gz
# verify sha256sum 
sha256sum bitsongd-linux-$PLATFORM_TARGET.tar.gz
# Output: TBD  bitsongd-linux-amd64.tar.gz
# Output: TBD  bitsongd-linux-arm64.tar.gz

# decompress 
tar -xvzf bitsongd-linux-$PLATFORM_TARGET.tar.gz 

## move binary to go bin path
sudo mv build/bitsongd-linux-$PLATFORM_TARGET $HOME/go/bin/bitsongd

## change file ownership, if nessesary 
sudo chmod +x $HOME/go/bin/bitsongd

## confirm binary executable works 
bitsongd version --long 

# build_tags: netgo,ledger
# commit: TBD
# server_name: bitsongd
# version:0.23.0
```

### Option C: Cosmovisor

