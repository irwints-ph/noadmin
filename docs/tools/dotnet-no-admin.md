# .NET SDK Installation (No Admin Required)

A guide for installing .NET SDK on Windows without administrator privileges using portable binaries.

## Table of Contents

1. [Prerequisites](#prerequisites)
2. [Download .NET SDK](#download-net-sdk)
3. [Installation Steps](#installation-steps)
4. [Environment Configuration](#environment-configuration)
5. [Install .NET Tools](#install-net-tools)
6. [Verification](#verification)
7. [Troubleshooting](#troubleshooting)

## Prerequisites

- Windows 10 or later
- User account with standard privileges
- Internet connection
- Approximately 500MB of free disk space

## Download .NET SDK

1. **Visit the Official Download Page**
   - Go to [Microsoft .NET Downloads](https://dotnet.microsoft.com/en-us/download/dotnet)
   - Select the latest LTS version (recommended) or current version

2. **Download Binaries**
   - Choose **Binaries** instead of installer
   - Select **Windows x64** for 64-bit systems
   - Direct link for .NET 8: [Windows x64 SDK Binaries](https://dotnet.microsoft.com/en-us/download/dotnet/thank-you/sdk-8.0.410-windows-x64-binaries)

## Installation Steps

### 1. Create Directory Structure

```cmd
mkdir C:\sw\dotnet
```

### 2. Extract SDK

1. Extract the downloaded archive to `C:\sw\dotnet\`
2. The extracted folder should be named something like `sdk-8.0.410-win-x64`
3. Your final path should look like: `C:\sw\dotnet\sdk-8.0.410-win-x64`

### 3. Verify Directory Structure

```cmd
dir C:\sw\dotnet\sdk-8.0.410-win-x64
```

You should see folders like:
- `dotnet.exe`
- `sdk\`
- `shared\`
- `templates\`

## Environment Configuration

### 1. Set DOTNET_ROOT Environment Variable

```cmd
setx DOTNET_ROOT "C:\sw\dotnet\sdk-8.0.410-win-x64"
```

### 2. Add to PATH

1. **Open Environment Variables GUI:**
   ```cmd
   rundll32 sysdm.cpl,EditEnvironmentVariables
   ```

2. **Add to User PATH:**
   - Add `%DOTNET_ROOT%` to your PATH variable
   - Or add the full path: `C:\sw\dotnet\sdk-8.0.410-win-x64`

3. **Apply Changes:**
   - Click OK to save
   - Close and reopen command prompt

## Install .NET Tools

### Entity Framework Core Tools

```cmd
dotnet tool install --global dotnet-ef --version 9.0.5
```

> **Note:** The `DOTNET_ROOT` environment variable is required for `dotnet-ef` to work properly.

### Other Useful Global Tools

```cmd
# ASP.NET Core code generator
dotnet tool install --global dotnet-aspnet-codegenerator

# Development certificates
dotnet dev-certs https --trust
```

## Verification

### 1. Test .NET Installation

```cmd
# Check .NET version
dotnet --version

# List installed SDKs
dotnet --list-sdks

# List installed runtimes
dotnet --list-runtimes

# Display .NET info
dotnet --info
```

### 2. Create Test Project

```cmd
# Create a new directory for testing
mkdir C:\temp\dotnet-test
cd C:\temp\dotnet-test

# Create a new console application
dotnet new console -n HelloWorld
cd HelloWorld

# Run the application
dotnet run
```

Expected output:
```
Hello, World!
```

### 3. Test Entity Framework Tools

```cmd
dotnet ef --version
```

## Troubleshooting

### Common Issues

#### 1. Command Not Found
**Problem:** `'dotnet' is not recognized as an internal or external command`

**Solutions:**
- Verify `DOTNET_ROOT` is set correctly
- Check that `%DOTNET_ROOT%` is in your PATH
- Close and reopen command prompt
- Verify the dotnet.exe file exists in the specified directory

#### 2. DOTNET_ROOT Issues
**Problem:** Tools like `dotnet-ef` don't work

**Solutions:**
- Ensure `DOTNET_ROOT` points to the correct directory
- The directory should contain `dotnet.exe`
- Restart command prompt after setting environment variables

#### 3. SSL Certificate Issues
**Problem:** HTTPS development certificate errors

**Solutions:**
```cmd
# Clear existing certificates
dotnet dev-certs https --clean

# Generate new certificate
dotnet dev-certs https --trust
```

#### 4. Permission Errors
**Problem:** Cannot install global tools

**Solutions:**
- Ensure you have write permissions to the .NET tools directory
- Try installing tools with `--tool-path` to a user directory:
```cmd
dotnet tool install --global dotnet-ef --tool-path %USERPROFILE%\.dotnet\tools
```

### Useful Commands

```cmd
# Check environment variables
echo %DOTNET_ROOT%
echo %PATH%

# List global tools
dotnet tool list --global

# Update global tools
dotnet tool update --global dotnet-ef

# Uninstall global tools
dotnet tool uninstall --global dotnet-ef
```

### File Locations

- **SDK Location:** `C:\sw\dotnet\sdk-8.0.410-win-x64`
- **Global Tools:** `%USERPROFILE%\.dotnet\tools`
- **NuGet Packages:** `%USERPROFILE%\.nuget\packages`

## Related Links

- [.NET Downloads](https://dotnet.microsoft.com/en-us/download/dotnet)
- [.NET CLI Documentation](https://docs.microsoft.com/en-us/dotnet/core/tools/)
- [Entity Framework Core Tools](https://docs.microsoft.com/en-us/ef/core/cli/dotnet)
- [Back to Main Guide](readme.md)