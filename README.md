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

Thanks
