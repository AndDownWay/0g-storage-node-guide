# 📦 0G Storage Node Setup Guide

This guide will walk you through the steps to deploy a **0G Storage Node**. The 0G System is composed of multiple components, each with specific functionalities. Follow these steps to set up your Storage Node efficiently.

## 📋 **Prerequisites**

Before you start, ensure you have the following:

- **Storage Node**
- **Storage Node CLI**

The 0G Storage Node interacts with on-chain contracts for blob root confirmation and PoRA mining. For official contract addresses, please visit the designated page.

## 💻 **Hardware Requirements**

Make sure your hardware meets these specifications for optimal performance:

- **Memory**: 16 GB RAM
- **CPU**: 4 cores
- **Disk**: 500GB / 1T NVMe SSD
- **Bandwidth**: 500 MBps (Download / Upload)

## 🛠️ **Deployment Steps**

### 1. **Install Dependencies**

Before you can run the Storage Node, you need to install some dependencies.

#### For Linux 🐧

Run the following commands:

```bash
sudo apt-get update
sudo apt-get install clang cmake build-essential
```

#### For macOS 🍏

Use Homebrew to install the necessary packages:

```bash
brew install llvm cmake
```

### 2. **Install Rust 🦀**

Rust is required to build the Storage Node. Install Rust using this command:

```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

### 3. **Install Go 🐹**

Go is another required component. Install Go by following the steps for your operating system:

#### For Linux 🐧

1. Download the Go installer:

    ```bash
    wget https://go.dev/dl/go1.22.0.linux-amd64.tar.gz
    ```

2. Extract the archive:

    ```bash
    sudo rm -rf /usr/local/go && sudo tar -C /usr/local -xzf go1.22.0.linux-amd64.tar.gz
    ```

3. Add Go to your `PATH` environment variable by adding this line to your `~/.profile`:

    ```bash
    export PATH=$PATH:/usr/local/go/bin
    ```

#### For macOS 🍏

Install Go using Homebrew:

```bash
brew install go
```

Or download the Go installer directly from [the official Go website](https://go.dev/dl/), then open the package file and follow the installation prompts.

### 4. **Download the Source Code 📥**

Clone the Storage Node repository from GitHub:

```bash
git clone -b v0.4.0 https://github.com/0glabs/0g-storage-node.git
```

### 5. **Build the Source Code 🛠️**

Navigate to the project directory and build the Storage Node in release mode:

```bash
cd 0g-storage-node
git submodule update --init
cargo build --release
```

## ⚙️ **Configuration**

Before running the node, you need to configure it. Update the `run/config.toml` file as needed:

- **`network_enr_address`**: Must include your instance's public IP for peer discovery.
- **`network_boot_nodes`**: List of peer nodes for the network. Modify as necessary.
- **`log_contract_address`**: Address of the flow contract.
- **`mine_contract_address`**: Address of the mining contract.
- **`blockchain_rpc_endpoint`**: RPC endpoint of the blockchain network.
- **`log_sync_start_block_number`**: The block number to start syncing from.
- **`miner_key`**: Your private key for participating in PoRA and earning mining rewards.
- **`db_max_num_chunks`**: Maximum number of chunk entries to store in the database. Each entry is 256B.

Example configuration:

```toml
network_enr_address = "your_public_ip"
network_boot_nodes = ["/ip4/54.219.26.22/udp/1234/p2p/16Uiu2HAmTVDGNhkHD98zDnJxQWu3i1FL1aFYeh9wiQTNu4pDCgps", "/ip4/52.52.127.117/udp/1234/p2p/16Uiu2HAkzRjxK2gorngB1Xq84qDrT4hSVznYDHj6BkbaE4SGx9oS", "/ip4/18.167.69.68/udp/1234/p2p/16Uiu2HAm2k6ua2mGgvZ8rTMV8GhpW71aVzkQWy7D37TTDuLCpgmX"]
log_contract_address = "your_flow_contract_address"
mine_contract_address = "your_mine_contract_address"
blockchain_rpc_endpoint = "your_rpc_endpoint"
log_sync_start_block_number = 123456
miner_key = "your_64_character_private_key"
db_max_num_chunks = 1000000
```

## 🚀 **Run the Storage Service**

Once configured, you can start the storage service.

### 1. **Check Command Line Options**

Review the available command line options using:

```bash
zgs_node -h
```

### 2. **Run the Node 🏃‍♂️**

Navigate to the `run` directory and start the node with your configuration file:

```bash
cd run

# Use tmux or screen to run in the background
../target/release/zgs_node --config config-testnet.toml --miner-key <your_private_key> --blockchain-rpc-endpoint <blockchain_rpc> --db-max-num-chunks <max_chunk_num>
```

And that's it! 🎉 You’re all set up.

---

Thank you for deploying your **0G Storage Node**! If you have any issues or need assistance, don't hesitate to reach out to our support team. 😊
