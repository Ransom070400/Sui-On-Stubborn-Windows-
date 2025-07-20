# Sui-On-Stubborn-Windows-

# Installing Sui on Windows via WSL and Homebrew

## Overview
This guide provides a streamlined approach to installing the Sui blockchain platform on Windows using Windows Subsystem for Linux (WSL) with Ubuntu, Homebrew package manager, and the official Sui binaries.

## System Requirements
- **Windows 10/11** (64-bit, version 2004 or higher)
- **Administrator privileges**
- 8GB+ RAM (16GB recommended)
- 50GB+ free disk space
- Internet connection

## Installation Steps

### 1. Install WSL and Ubuntu

1. **Open PowerShell as Administrator** (Right-click Start > Windows PowerShell (Admin))
   
2. Install WSL with Ubuntu:
   ```powershell
   wsl --install -d Ubuntu
   ```
   
3. Restart your computer when prompted

4. **Launch Ubuntu** from Start Menu and complete setup:
   - Create a UNIX username and password
   - These credentials are separate from your Windows login

5. Verify installation:
   ```powershell
   wsl -l -v
   ```
   Should show: `Ubuntu  Running  2`

### 2. Set Up Ubuntu Environment

1. Update packages:
   ```bash
   sudo apt update && sudo apt upgrade -y
   ```

2. Install essential dependencies:
   ```bash
   sudo apt install -y build-essential curl git libssl-dev pkg-config
   ```

### 3. Install Homebrew

1. Install Homebrew package manager:
   ```bash
   /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
   ```

2. Add Homebrew to your PATH:
   ```bash
   echo 'eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"' >> ~/.bashrc
   source ~/.bashrc
   ```

3. Verify installation:
   ```bash
   brew --version
   ```
   Should show: `Homebrew 4.x.x`

### 4. Install Sui via Homebrew

1. Add Mysten Labs Homebrew tap:
   ```bash
   brew tap mystenlabs/tap
   ```

2. Install Sui binaries:
   ```bash
   brew install sui
   ```

3. Verify installation:
   ```bash
   sui --version
   ```
   Should show version: `sui x.x.x`

### 5. Configure Sui Environment

1. Initialize Sui client:
   ```bash
   sui client
   ```
   - Follow prompts to create new wallet and addresses
   - Save recovery phrase securely!

2. Connect to Devnet (recommended for beginners):
   ```bash
   sui client switch --env devnet
   ```

3. Check connection status:
   ```bash
   sui client envs
   ```

### 6. Test Your Installation

1. Request test tokens from Devnet faucet:
   ```bash
   curl --location --request POST 'https://faucet.devnet.sui.io/gas' \
   --header 'Content-Type: application/json' \
   --data-raw '{"FixedAmountRequest":{"recipient":"<YOUR_SUI_ADDRESS>"}}'
   ```

2. Check your balance:
   ```bash
   sui client gas
   ```

3. Run a sample transaction:
   ```bash
   sui client objects
   ```

## Post-Installation Setup

### Configure Visual Studio Code (Recommended)
1. Install [WSL extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-wsl)
2. Open Ubuntu terminal: `code .`
3. Create sample project:
   ```bash
   sui move new my_first_package
   ```

### Update Your Environment
Add to `~/.bashrc`:
```bash
# Homebrew
eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"

# Sui
export SUI_HOME="$HOME/sui"
export PATH="$PATH:$HOME/.cargo/bin"
```

## Troubleshooting

**Common Issues:**
1. *WSL installation fails*:
   - Enable virtualization in BIOS/UEFI
   - Run: `dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart`

2. *Brew command not found*:
   ```bash
   eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"
   ```

3. *Sui version not showing*:
   ```bash
   brew upgrade sui
   source ~/.bashrc
   ```

4. *Connection issues with Devnet*:
   ```bash
   sui client new-env --alias devnet --rpc https://fullnode.devnet.sui.io:443
   sui client switch --env devnet
   ```

## Maintenance

**Update Sui:**
```bash
brew update
brew upgrade sui
```

**Uninstall Sui:**
```bash
brew uninstall sui
brew untap mystenlabs/tap
```

**Clean Up WSL:**
```powershell
wsl --unregister Ubuntu
```

## Next Steps
- Explore Sui Move examples: `cd sui/sui_programmability/examples`
- Join Sui Devnet: https://docs.sui.io/build/devnet
- Build your first NFT: https://docs.sui.io/build/move-examples/nft

> **Note:** All commands should be run in the Ubuntu WSL terminal unless specified as PowerShell. Performance is significantly better in WSL 2 compared to native Windows development for blockchain tools.


