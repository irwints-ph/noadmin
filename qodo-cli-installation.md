# Qodo Command Installation Guide

This guide provides comprehensive instructions for installing Qodo Command on Windows, macOS, and Linux systems.

## 📋 Overview

Qodo Command is a command-line interface for building, running, and managing AI agents. It allows you to automate complex workflows, interact with AI models and external tools, and serve AI agents as HTTP services — all from your terminal.

### Key Features
- 🤖 **Custom Agent Configuration** - Build and manage your own AI agents
- 🔄 **Workflow Automation** - Automate complex engineering workflows
- 🌐 **Interactive Chat Mode** - Talk to agents in natural language
- 💻 **Web UI Mode** - Browser-based interface for agent interaction
- 🔌 **HTTP API Mode** - Serve agents as callable services
- 🔧 **Tool Integration** - Secure integration with external tools and APIs

## 🚀 Quick Installation

### Prerequisites
- **Node.js** (version 14 or higher)
- **npm** (comes with Node.js)

### All Platforms

```bash
# Install Qodo Command globally
npm install -g @qodo/command

# Verify installation
qodo --version

# Login to get started
qodo login
```

### Package Rename Notice
> **📦 Important**: This package was previously named `@qodo/gen`. If you have the old package installed:
>
> ```bash
> npm uninstall -g @qodo/gen
> npm install -g @qodo/command
> ```

## 📦 Detailed Installation Instructions

### Step 1: Install Node.js and npm

Qodo Command requires Node.js and npm. If you don't have them installed:

#### Windows
1. Download Node.js from [nodejs.org](https://nodejs.org/)
2. Run the installer and follow the setup wizard
3. Verify installation:
   ```powershell
   node --version
   npm --version
   ```

#### macOS
```bash
# Using Homebrew (recommended)
brew install node

# Or download from nodejs.org
```

#### Linux
```bash
# Ubuntu/Debian
sudo apt update
sudo apt install nodejs npm

# Fedora/RHEL
sudo dnf install nodejs npm

# Arch Linux
sudo pacman -S nodejs npm
```

### Step 2: Install Qodo Command

Once Node.js and npm are installed, install Qodo Command globally:

```bash
npm install -g @qodo/command
```

### Step 3: Verify Installation

```bash
# Check if Qodo Command is installed correctly
qodo --version

# Should display version information
```

### Step 4: Login and Setup

```bash
# Login to Qodo (required for first use)
qodo login
```

This will:
1. Open your browser for authentication
2. Generate an API key
3. Save the key locally in your `.qodo` folder
4. Set up your account for usage

## ⚙️ Basic Usage

### Interactive Chat Mode

Start an interactive chat session with an AI agent:

```bash
qodo chat
```

Example prompts:
- "Write tests for the files in the auth directory"
- "Add better logging throughout my project"
- "Use Qodo Merge to describe the changes in my working folder"

### Web UI Mode

Launch a browser-based interface:

```bash
qodo --ui
```

### Custom Agents

Run custom agents (requires agent configuration):

```bash
# Run a specific agent command
qodo <command>

# Example: Review a pull request
qodo review --pr=123

# Example: Generate tests
qodo test --path=src/
```

## 🔧 Advanced Features

### Model Selection

Choose which AI model to use:

```bash
# List available models
qodo models

# Use a specific model
qodo chat --model=claude-3-sonnet
qodo chat --model=gpt-4
```

### Webhook Mode

Serve agents as HTTP endpoints:

```bash
# Start agent as webhook
qodo --webhook

# Agent becomes callable via HTTP POST
```

### MCP Mode

Turn agents into Model Context Protocol servers:

```bash
# Run agent as MCP server
qodo --mcp
```

### CI/CD Integration

Run agents in CI environments:

```bash
# CI mode (simplified output)
qodo review --pr=123 --ci
```

## ⚙️ Configuration

### API Key Management

Manage your API keys:

```bash
# List all API keys
qodo key list

# Create a new API key
qodo key create <name>

# Revoke an API key
qodo key revoke <name>
```

### Configuration File

Qodo Command stores configuration in the `.qodo` folder in your home directory:
- **Windows**: `%USERPROFILE%\.qodo\`
- **macOS/Linux**: `~/.qodo/`

### Tool Configuration

Control which tools (MCPs) are available:

```bash
# Use specific tools
qodo chat --tools=git,filesystem,shell

# Available tools:
# - git (version control)
# - filesystem (file operations)
# - shell (command execution)
# - ripgrep (fast text search)
# - web_search (online search)
# - qodo_merge (code review)
```

## 🔧 IDE Integration

### Terminal-Based Integration

Qodo Command works in any IDE through the terminal:

```bash
# Run from any IDE's integrated terminal
qodo chat
qodo --ui
```

### Qodo Gen (IDE Extensions)

For direct IDE integration, use Qodo Gen:
- **VS Code**: [Qodo Extension](https://marketplace.visualstudio.com/items?itemName=Codium.codium)
- **JetBrains**: [Qodo Plugin](https://plugins.jetbrains.com/plugin/21206-codiumai)

### Qodo Merge (Code Review)

For GitHub/GitLab integration:
- **GitHub**: [Qodo Merge](https://github.com/qodo-ai/pr-agent)
- **GitLab**: Available through Qodo Merge setup

## ✅ Verification

### Test Installation

```bash
# Check version
qodo --version

# Test basic functionality
qodo --help

# Start interactive chat (exit with Escape)
qodo chat

# Launch web UI
qodo --ui
```

### Common Commands

```bash
# Interactive chat mode
qodo chat

# Web UI mode
qodo --ui

# List available models
qodo models

# API key management
qodo key list

# Help and documentation
qodo --help
qodo chat --help
```

## 🔧 Troubleshooting

### Common Issues

#### 1. "Command not found" Error

```bash
# Check if npm global packages are in PATH
npm list -g --depth=0

# Check npm global bin directory
npm config get prefix

# Reinstall if needed
npm uninstall -g @qodo/command
npm install -g @qodo/command
```

#### 2. Node.js/npm Issues

```bash
# Check Node.js version (should be 14+)
node --version

# Check npm version
npm --version

# Update npm if needed
npm install -g npm@latest
```

#### 3. Login Issues

```bash
# Try logging in again
qodo login

# Check if API key exists
qodo key list

# Create new API key if needed
qodo key create my-key
```

#### 4. Permission Errors

**Windows:**
```powershell
# Run as Administrator
Start-Process powershell -Verb runAs
```

**macOS/Linux:**
```bash
# Fix npm permissions
sudo chown -R $USER $(npm config get prefix)/{lib/node_modules,bin,share}

# Or use a Node version manager like nvm
```

### Getting Help

```bash
# General help
qodo --help

# Command-specific help
qodo chat --help
qodo key --help

# Version information
qodo --version
```

## 🔄 Updates

### Manual Updates

Update Qodo Command using npm:

```bash
# Update to latest version
npm update -g @qodo/command

# Or reinstall
npm uninstall -g @qodo/command
npm install -g @qodo/command

# Check current version
qodo --version
```

## 🚀 Advanced Usage

### Creating Custom Agents

Create your own agents with configuration files:

```bash
# Create agent.toml in your project
# Define agent instructions, tools, and workflows
# Run custom commands: qodo <your-command>
```

### CI/CD Integration

```yaml
# GitHub Actions example
name: Qodo Command Review
on: [pull_request]
jobs:
  review:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Setup Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '18'
      - name: Install Qodo Command
        run: npm install -g @qodo/command
      - name: Run review
        run: qodo review --pr=${{ github.event.number }} --ci
        env:
          QODO_API_KEY: ${{ secrets.QODO_API_KEY }}
```

## 📚 Additional Resources

- [Official Documentation](https://docs.qodo.ai/qodo-documentation/qodo-command)
- [GitHub Repository](https://github.com/qodo-ai/command)
- [NPM Package](https://www.npmjs.com/package/@qodo/command)
- [Agent Examples](https://github.com/qodo-ai/agents)
- [Release Notes](https://release-notes.command.qodo.ai/)

## 🆘 Support

If you encounter issues:

1. **Check the documentation**: [docs.qodo.ai](https://docs.qodo.ai/qodo-documentation/qodo-command)
2. **Join the community**: [Discord](https://discord.com/invite/kG35uSHDBc)
3. **Visit the website**: [qodo.ai](https://www.qodo.ai/)
4. **Contact support**: [qodo.ai/contact](https://www.qodo.ai/contact)

---

**Note**: Qodo Command is currently in Alpha release. Features and installation methods may change. Always refer to the [official documentation](https://docs.qodo.ai/qodo-documentation/qodo-command) for the most up-to-date information.