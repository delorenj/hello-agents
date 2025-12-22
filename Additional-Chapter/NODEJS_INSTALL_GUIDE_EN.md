# Node.js and npx Installation Guide

## 📋 Table of Contents

- [Why Install Node.js?](#why-install-nodejs)
- [Windows Installation Guide](#windows-installation-guide)
- [macOS Installation Guide](#macos-installation-guide)
- [Linux Installation Guide](#linux-installation-guide)
- [Verify Installation](#verify-installation)
- [Common Issues](#common-issues)

---

## Why Install Node.js?

In Chapter 10's MCP protocol learning, we need to use community-provided MCP servers. Most of these servers are written in JavaScript/TypeScript and require a Node.js runtime environment.

**After installing Node.js, you will have**:
- ✅ **node**: JavaScript runtime
- ✅ **npm**: Node Package Manager
- ✅ **npx**: npm package runner (automatically downloads and runs npm packages)

**What npx does**:
```bash
# Traditional way: install first, then run
npm install -g @modelcontextprotocol/server-filesystem
server-filesystem

# Using npx: automatically download and run (recommended)
npx @modelcontextprotocol/server-filesystem
```

---

## Windows Installation Guide

### Method 1: Official Installer (Recommended)

#### Step 1: Download Installer

Visit the Node.js official website: https://nodejs.org/

You will see two versions:
- **LTS (Long Term Support)**: Recommended for most users ✅
- **Current**: Contains the latest features

**Recommended to download LTS version** (e.g., 20.x.x LTS)

#### Step 2: Run the Installer

1. Double-click the downloaded `.msi` file
2. Click "Next" to start installation
3. Accept the license agreement
4. Choose installation path (default is fine)
5. **Important**: Make sure to check the following options:
   - ✅ Node.js runtime
   - ✅ npm package manager
   - ✅ Add to PATH (automatically adds to environment variables)
6. Click "Install" to begin installation
7. Wait for installation to complete, click "Finish"

#### Step 3: Verify Installation

Open **PowerShell** or **Command Prompt** (CMD), and enter:

```powershell
# Check Node.js version
node -v
# Should display: v20.x.x

# Check npm version
npm -v
# Should display: 10.x.x

# Check npx version
npx -v
# Should display: 10.x.x
```

If all commands display version numbers properly, installation was successful! ✅

---

## macOS Installation Guide

### Method 1: Official Installer

#### Step 1: Download Installer

Visit: https://nodejs.org/

Download the **LTS version** `.pkg` file

#### Step 2: Install

1. Double-click the `.pkg` file
2. Follow the installation wizard prompts
3. Enter administrator password
4. Complete installation

#### Step 3: Verify Installation

Open **Terminal**, and enter:

```bash
node -v
npm -v
npx -v
```

---

## Linux Installation Guide

### Ubuntu/Debian

#### Method 1: Using NodeSource Repository (Recommended)

```bash
# Update package list
sudo apt update

# Install curl (if not already installed)
sudo apt install -y curl

# Add NodeSource repository (Node.js 20.x LTS)
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -

# Install Node.js and npm
sudo apt install -y nodejs

# Verify installation
node -v
npm -v
npx -v
```

#### Method 2: Using apt (may be older version)

```bash
sudo apt update
sudo apt install -y nodejs npm
```

---

### CentOS/RHEL/Fedora

```bash
# Add NodeSource repository
curl -fsSL https://rpm.nodesource.com/setup_20.x | sudo bash -

# Install Node.js
sudo yum install -y nodejs

# Verify installation
node -v
npm -v
npx -v
```

---

### Arch Linux

```bash
# Install using pacman
sudo pacman -S nodejs npm

# Verify installation
node -v
npm -v
npx -v
```

---

## Verify Installation

### Complete Verification Steps

After installation, run the following commands for complete verification:

```bash
# 1. Check versions
node -v
npm -v
npx -v

# 2. Test Node.js
node -e "console.log('Node.js is working properly!')"

# 3. Test npm
npm --version

# 4. Test npx (run a simple package)
npx cowsay "Hello MCP!"
```

### Expected Output

```
v20.11.0
10.2.4
10.2.4
Node.js is working properly!
10.2.4
 _____________
< Hello MCP! >
 -------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||
```

---

## Test MCP Server Connection

After installation, test connection to community MCP servers:

### Test Filesystem Server

```bash
# Use npx to run filesystem MCP server
npx -y @modelcontextprotocol/server-filesystem .
```

If you see server startup information, everything is working properly!

### Test in Python

Create test script `test_mcp.py`:

```python
import asyncio
from hello_agents.protocols import MCPClient

async def test():
    client = MCPClient([
        "npx", "-y",
        "@modelcontextprotocol/server-filesystem",
        "."
    ])
    
    async with client:
        tools = await client.list_tools()
        print(f"✅ Successfully connected! Available tools: {[t['name'] for t in tools]}")

asyncio.run(test())
```

Run:

```bash
python test_mcp.py
```

---

## Common Issues

### Q1: Command not found after installation

**Windows**:
```powershell
# Check environment variables
echo $env:PATH

# Manually add Node.js to PATH
# 1. Right-click "This PC" -> "Properties"
# 2. "Advanced system settings" -> "Environment Variables"
# 3. Find "Path" in "System variables"
# 4. Add: C:\Program Files\nodejs\
```

**macOS/Linux**:
```bash
# Check environment variables
echo $PATH

# Add to ~/.bashrc or ~/.zshrc
export PATH="/usr/local/bin:$PATH"
source ~/.bashrc  # or source ~/.zshrc
```

---

### Q2: npm is very slow

Use Chinese mirror source (Taobao mirror):

```bash
# Temporary use
npm install --registry=https://registry.npmmirror.com

# Permanent setting
npm config set registry https://registry.npmmirror.com

# Verify
npm config get registry
```

---

### Q3: npx permission error

**Windows**:
```powershell
# Run PowerShell as administrator
```

**macOS/Linux**:
```bash
# Don't use sudo to run npx
# If you encounter permission issues, fix npm global directory permissions
mkdir ~/.npm-global
npm config set prefix '~/.npm-global'
echo 'export PATH=~/.npm-global/bin:$PATH' >> ~/.bashrc
source ~/.bashrc
```

---

### Q4: Version conflicts

If you need to manage multiple Node.js versions, use a version manager:

**Windows**: [nvm-windows](https://github.com/coreybutler/nvm-windows)

```powershell
# After installing nvm-windows
nvm install 20.11.0
nvm use 20.11.0
```

**macOS/Linux**: [nvm](https://github.com/nvm-sh/nvm)

```bash
# Install nvm
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash

# Install Node.js
nvm install 20
nvm use 20
```

---

### Q5: npx downloads packages very slowly

```bash
# Method 1: Use Chinese mirror
npx --registry=https://registry.npmmirror.com @modelcontextprotocol/server-filesystem

# Method 2: Install globally first, then use
npm install -g @modelcontextprotocol/server-filesystem
server-filesystem
```

---

## Next Steps

After installation, you can:

1. ✅ Run `code/02_Connect2MCP.py` to test MCP client connection
2. ✅ Explore community MCP servers: https://github.com/modelcontextprotocol/servers
3. ✅ Continue learning other content in Chapter 10

---

## Reference Resources

- **Node.js Official Website**: https://nodejs.org/
- **npm Documentation**: https://docs.npmjs.com/
- **npx Documentation**: https://docs.npmjs.com/cli/v10/commands/npx
- **MCP Server List**: https://github.com/modelcontextprotocol/servers
- **Taobao npm Mirror**: https://npmmirror.com/

---

**Happy Learning!** 🎉

If you have questions, please refer to the Common Issues section or consult the official documentation.
