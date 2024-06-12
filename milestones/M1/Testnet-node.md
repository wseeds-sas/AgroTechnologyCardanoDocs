# Setting Up a Cardano Node on the Testnet

## Prerequisites
- **Operating System**: Linux, macOS, or Windows (using WSL for Linux environment)
- **Processor**: Intel or AMD x86 with 2+ cores, 1.6GHz+ (2GHz+ for stake pool)
- **Memory**: 24GB RAM
- **Storage**: 150GB free disk space (250GB recommended)

## Environment Variables
Set the following environment variables to streamline the setup process:

```bash
export CARDANO_NODE_VERSION=8.0.0
export CARDANO_SRC_DIR=$HOME/cardano-src
export CARDANO_GHC_VERSION=8.10.7
export CARDANO_CABAL_VERSION=3.6.2.0
export CARDANO_NODE_REPO=https://github.com/IntersectMBO/cardano-node
export CARDANO_LIBSODIUM_REPO=https://github.com/IntersectMBO/libsodium
export CARDANO_SECP256K1_REPO=https://github.com/bitcoin-core/secp256k1
export TESTNET_MAGIC=1097911063
export CONFIG_DIR=$CARDANO_SRC_DIR/config
```

## Step-by-Step Instructions

### 1. Install System Dependencies

#### Ubuntu/Debian:
```bash 
sudo apt-get update -y && sudo apt-get upgrade -y
sudo apt-get install -y automake build-essential pkg-config libffi-dev \
    libgmp-dev libssl-dev libtinfo-dev libsystemd-dev zlib1g-dev \
    make g++ tmux git jq wget libncursesw5 libtool autoconf
```

#### Redhat/CentOS:
```bash
sudo yum update -y
sudo yum install -y git gcc gcc-c++ tmux gmp-devel make tar xz wget \
    zlib-devel libtool autoconf jq systemd-devel ncurses-devel \
    ncurses-compat-libs
```

### 2. Install GHC and Cabal

```bash
curl --proto '=https' --tlsv1.2 -sSf https://get-ghcup.haskell.org | sh
ghcup install ghc $CARDANO_GHC_VERSION
ghcup set ghc $CARDANO_GHC_VERSION
ghcup install cabal $CARDANO_CABAL_VERSION
ghcup set cabal $CARDANO_CABAL_VERSION
```

### 3. Download and Compile Dependencies

```bash
mkdir -p $CARDANO_SRC_DIR
cd $CARDANO_SRC_DIR

# Install libsodium
git clone $CARDANO_LIBSODIUM_REPO
cd libsodium
git checkout dbb48cc
./autogen.sh
./configure
make
sudo make install

# Add environment variables for libsodium
echo 'export LD_LIBRARY_PATH="/usr/local/lib:$LD_LIBRARY_PATH"' >> ~/.bashrc
echo 'export PKG_CONFIG_PATH="/usr/local/lib/pkgconfig:$PKG_CONFIG_PATH"' >> ~/.bashrc
source ~/.bashrc

# Install secp256k1
cd $CARDANO_SRC_DIR
git clone $CARDANO_SECP256K1_REPO
cd secp256k1
git checkout ac83be33
./autogen.sh
./configure --enable-module-schnorrsig --enable-experimental
make
make check
sudo make install
```

### 4. Download, Compile, and Install Cardano Node

```bash
cd $CARDANO_SRC_DIR
git clone $CARDANO_NODE_REPO
cd cardano-node
git fetch --all --recurse-submodules --tags
git checkout $CARDANO_NODE_VERSION

cabal configure --with-compiler=ghc-$CARDANO_GHC_VERSION
cabal update
cabal build all

mkdir -p $HOME/.local/bin
cp -p "$(./scripts/bin-path.sh cardano-node)" $HOME/.local/bin/
cp -p "$(./scripts/bin-path.sh cardano-cli)" $HOME/.local/bin/

echo 'export PATH="$HOME/.local/bin/:$PATH"' >> ~/.bashrc
source ~/.bashrc

# Verify installation
cardano-cli --version
cardano-node --version
```

### 5. Download Testnet Configuration Files

```bash
mkdir -p $CONFIG_DIR
cd $CONFIG_DIR
curl -O -J https://book.world.dev.cardano.org/environments/preview/config.json
curl -O -J https://book.world.dev.cardano.org/environments/preview/topology.json
curl -O -J https://book.world.dev.cardano.org/environments/preview/byron-genesis.json
curl -O -J https://book.world.dev.cardano.org/environments/preview/shelley-genesis.json
curl -O -J https://book.world.dev.cardano.org/environments/preview/alonzo-genesis.json
curl -O -J https://book.world.dev.cardano.org/environments/preview/conway-genesis.json
```

### 6. Run the Cardano Node

```bash
cardano-node run \
  --topology $CONFIG_DIR/topology.json \
  --database-path $CARDANO_SRC_DIR/db \
  --socket-path $CARDANO_SRC_DIR/db/node.socket \
  --host-addr 0.0.0.0 \
  --port 3001 \
  --config $CONFIG_DIR/config.json
```

### 7. Querying the Cardano Blockchain

To check the sync status of your node and interact with the blockchain, follow these steps:

1. **Set the `CARDANO_NODE_SOCKET_PATH` Environment Variable**

   Add this to your `~/.bashrc` or `~/.zshrc` file:

    ```bash
   export CARDANO_NODE_SOCKET_PATH="$CARDANO_SRC_DIR/db/node.socket"
    ```
   Reload your shell profile:
   
    ```bash
   source ~/.bashrc  # or source ~/.zshrc
    ```

2. **Query the Blockchain Tip**

   Run the following command to check the sync status:

    ```bash
   cardano-cli query tip --testnet-magic $TESTNET_MAGIC
    ```

   You should see output similar to this:

    ```json
    {
         "block": 2598870,
         "epoch": 133,
         "era": "Shelley",
         "hash": "7b5633590bf8924d8fce5b6515f34fga0c712f64e9b7d273f915656f88fba872",
         "slot": 27149964,
         "syncProgress": "57.09"
    }
    ```

### Useful Commands

- **Check Node Status**:

```bash
  cardano-cli query tip --testnet-magic $TESTNET_MAGIC
```

- **Generate Keys**:

```bash
  cardano-cli address key-gen \
      --verification-key-file payment.vkey \
      --signing-key-file payment.skey
```

- **Build a Transaction**:

```bash
  cardano-cli transaction build-raw \
      --tx-in <TX-IN> \
      --tx-out <TX-OUT> \
      --fee <FEE> \
      --out-file tx.raw
```

- **Sign a Transaction**:

```bash
  cardano-cli transaction sign \
      --tx-body-file tx.raw \
      --signing-key-file payment.skey \
      --testnet-magic $TESTNET_MAGIC \
      --out-file tx.signed
```


- **Submit a Transaction**:

```bash
  cardano-cli transaction submit \
      --tx-file tx.signed \
      --testnet-magic $TESTNET_MAGIC
```

## Conclusion
Following these steps, you should have a Cardano node running on the testnet, ready for further development and testing. Remember to monitor the sync status and ensure your node is fully synchronized before performing transactions.
