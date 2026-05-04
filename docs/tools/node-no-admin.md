# Node.js Installation (No Admin Required)

A guide for installing Node.js on Windows without administrator privileges using the portable ZIP version.

## Table of Contents

1. [Prerequisites](#prerequisites)
2. [Download Node.js](#download-nodejs)
3. [Installation Steps](#installation-steps)
4. [Environment Configuration](#environment-configuration)
5. [Package Management](#package-management)
6. [Verification](#verification)
7. [Troubleshooting](#troubleshooting)

## Prerequisites

- Windows 10 or later
- User account with standard privileges
- Internet connection
- Approximately 50MB of free disk space

## Download Node.js

1. **Visit the Official Download Page**
   - Go to [Node.js Downloads](https://nodejs.org/en/download/)
   - Select the **LTS** (Long Term Support) version for stability

2. **Download ZIP Version**
   - Choose **Windows Binary (.zip)** instead of the installer
   - Select **x64** for 64-bit systems
   
   ![Node.js Download](img/node-download.png)

## Installation Steps

### 1. Create Directory Structure

```cmd
mkdir C:\sw\node
```

### 2. Extract Node.js

1. **Download the ZIP file** (e.g., `node-v24.4.1-win-x64.zip`)

2. **Extract using PowerShell:**
   ```powershell
   Expand-Archive -Path "%userprofile%\downloads\node-v24.4.1-win-x64.zip" -DestinationPath "C:\sw\node"
   ```

3. **Or extract manually:**
   - Right-click the downloaded ZIP file
   - Select "Extract All..."
   - Extract to `C:\sw\node`

### 3. Verify Directory Structure

After extraction, you should have:
```
C:\sw\node\node-v24.4.1-win-x64\
├── node.exe
├── npm
├── npm.cmd
├── npx
├── npx.cmd
└── node_modules\
```

## Environment Configuration

### 1. Set NODE_ROOT Environment Variable

```cmd
setx NODE_ROOT "C:\sw\node\node-v24.4.1-win-x64"
```

### 2. Add to PATH

1. **Open Environment Variables GUI:**
   ```cmd
   rundll32 sysdm.cpl,EditEnvironmentVariables
   ```

2. **Add to User PATH:**
   - Add `%NODE_ROOT%` to your PATH variable
   
   ![Node.js PATH](img/node-path.png)

3. **Apply Changes:**
   - Click OK to save
   - Close and reopen command prompt

### 3. Configure npm Global Directory (Optional)

To avoid permission issues with global packages:

```cmd
# Create global directory
mkdir %userprofile%\.npm-global

# Configure npm to use it
npm config set prefix %userprofile%\.npm-global

# Add to PATH
setx PATH "%PATH%;%userprofile%\.npm-global"
```

## Package Management

### npm Basics

```cmd
# Check npm version
npm --version

# Update npm to latest version
npm install -g npm@latest

# List globally installed packages
npm list -g --depth=0

# Install a global package
npm install -g typescript

# Install project dependencies
npm install

# Install and save to package.json
npm install express --save
npm install nodemon --save-dev
```

### Useful Global Packages

```cmd
# TypeScript compiler
npm install -g typescript

# Node.js development server
npm install -g nodemon

# Package manager alternative
npm install -g yarn

# Code formatter
npm install -g prettier

# Linting tool
npm install -g eslint

# HTTP server for static files
npm install -g http-server
```

## Verification

### 1. Test Node.js Installation

```cmd
# Check Node.js version
node --version
```

Expected output similar to:
```
v24.4.1
```

![Node.js Version](img/node-version.png)

### 2. Test npm

```cmd
# Check npm version
npm --version

# Check npm configuration
npm config list
```

### 3. Create Test Project

```cmd
# Create test directory
mkdir C:\temp\node-test
cd C:\temp\node-test

# Initialize new Node.js project
npm init -y

# Create simple test file
echo console.log('Hello, Node.js!'); > app.js

# Run the application
node app.js
```

Expected output:
```
Hello, Node.js!
```

### 4. Test Package Installation

```cmd
# Install a test package locally
npm install lodash

# Create test script
echo const _ = require('lodash'); console.log(_.capitalize('hello world')); > test.js

# Run test
node test.js
```

Expected output:
```
Hello world
```

## Troubleshooting

### Common Issues

#### 1. Command Not Found
**Problem:** `'node' is not recognized as an internal or external command`

**Solutions:**
- Verify `NODE_ROOT` is set correctly
- Check that `%NODE_ROOT%` is in your PATH
- Close and reopen command prompt
- Verify node.exe exists in the specified directory

#### 2. npm Permission Errors
**Problem:** EACCES errors when installing global packages

**Solutions:**
- Configure npm to use a user directory (see [configuration section](#3-configure-npm-global-directory-optional))
- Or install packages locally instead of globally:
```cmd
# Instead of: npm install -g package-name
npx package-name
```

#### 3. PATH Issues
**Problem:** Commands work in one terminal but not another

**Solutions:**
- Restart all terminal windows
- Check environment variables:
```cmd
echo %NODE_ROOT%
echo %PATH%
```
- Use the GUI method for setting PATH

#### 4. Version Conflicts
**Problem:** Multiple Node.js versions causing conflicts

**Solutions:**
- Use Node Version Manager (nvm-windows) for version management
- Or ensure only one Node.js installation is in PATH

### Node Version Manager (Alternative)

For managing multiple Node.js versions, consider using nvm-windows:

```cmd
# Download from: https://github.com/coreybutler/nvm-windows
# Install and use:
nvm install 18.17.0
nvm install 20.5.0
nvm use 20.5.0
```

### Useful Commands

```cmd
# Check Node.js installation path
where node

# Check npm installation path
where npm

# Clear npm cache
npm cache clean --force

# Check outdated packages
npm outdated

# Update packages
npm update

# Audit for vulnerabilities
npm audit
npm audit fix
```

### File Locations

- **Node.js Installation:** `C:\sw\node\node-v24.4.1-win-x64`
- **Global npm packages:** `%userprofile%\.npm-global` (if configured)
- **npm cache:** `%userprofile%\AppData\Roaming\npm-cache`
- **npm configuration:** `%userprofile%\.npmrc`

## Best Practices

1. **Use LTS Versions:** Stick to Long Term Support versions for stability
2. **Local vs Global:** Install packages locally unless they're CLI tools
3. **Package.json:** Always use package.json for project dependencies
4. **Version Locking:** Use package-lock.json for consistent installs
5. **Security:** Regularly run `npm audit` to check for vulnerabilities

## Related Links

- [Node.js Official Website](https://nodejs.org/)
- [npm Documentation](https://docs.npmjs.com/)
- [nvm-windows](https://github.com/coreybutler/nvm-windows)
- [Back to Main Guide](readme.md)