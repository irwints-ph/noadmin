# Python Installation (No Admin Required)

A comprehensive guide for installing Python on Windows without administrator privileges using pyenv-win for version management.

## Table of Contents

1. [Prerequisites](#prerequisites)
2. [Disable Microsoft Store Python](#disable-microsoft-store-python)
3. [Install pyenv-win](#install-pyenv-win)
4. [Install Python](#install-python)
5. [Virtual Environment Setup](#virtual-environment-setup)
6. [VSCode Configuration](#vscode-configuration)
7. [Ubuntu Installation](#ubuntu-installation)
8. [Troubleshooting](#troubleshooting)

## Prerequisites

- Windows 10 or later
- PowerShell (included with Windows)
- User account with standard privileges
- Internet connection
- Approximately 200MB of free disk space per Python version

## Disable Microsoft Store Python

Before installing Python, disable the Microsoft Store app aliases to prevent conflicts:

1. **Open Settings**
   - Press `Win + I` or go to Settings
   - Navigate to **Apps** → **Advanced app settings** → **App execution aliases**

2. **Disable Python Aliases**
   - Turn OFF `python.exe`
   - Turn OFF `python3.exe`

This prevents Windows from redirecting Python commands to the Microsoft Store.

## Install pyenv-win

pyenv-win allows you to install and manage multiple Python versions without admin rights.

### 1. Enable PowerShell Script Execution

```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

### 2. Download and Install pyenv-win

```powershell
# Download the installer
Invoke-WebRequest -UseBasicParsing -Uri "https://raw.githubusercontent.com/pyenv-win/pyenv-win/master/pyenv-win/install-pyenv-win.ps1" -OutFile "./install-pyenv-win.ps1"

# Run the installer
./install-pyenv-win.ps1
```

### 3. Restart Terminal

Close and reopen your command prompt or PowerShell to load the new environment variables.

### 4. Verify Installation

```cmd
pyenv --version
```

## Install Python

### 1. List Available Python Versions

```cmd
pyenv install --list
```

### 2. Install Latest Python Version

```cmd
# Install Python 3.13.3 (or latest available)
pyenv install 3.13.3

# Set as global default
pyenv global 3.13.3

# Verify installation
pyenv version
python --version
```

### 3. Install Additional Versions (Optional)

```cmd
# Install Python 3.11 for compatibility
pyenv install 3.11.10

# List installed versions
pyenv versions

# Switch between versions
pyenv global 3.11.10  # Set 3.11 as default
pyenv global 3.13.3   # Switch back to 3.13
```

## Virtual Environment Setup

Virtual environments isolate project dependencies and prevent conflicts.

### 1. Create Virtual Environment

```cmd
# Create virtual environment for FastAPI project
python -m venv %userprofile%\.venv\fastapi

# Create virtual environment for Django project
python -m venv %userprofile%\.venv\django

# Create virtual environment for data science
python -m venv %userprofile%\.venv\datascience
```

### 2. Activate Virtual Environment

```cmd
# Activate FastAPI environment
%userprofile%\.venv\fastapi\Scripts\activate

# Upgrade pip
python.exe -m pip install --upgrade pip
```

### 3. Install Packages in Virtual Environment

```cmd
# For FastAPI development
python -m pip install fastapi uvicorn

# For Django development
python -m pip install django

# For data science
python -m pip install pandas numpy matplotlib jupyter
```

### 4. Deactivate Virtual Environment

```cmd
deactivate
```

## VSCode Configuration

### 1. Project-Specific Python Interpreter

Create `.vscode/settings.json` in your project root:

```json
{
  "python.defaultInterpreterPath": "~/.venv/fastapi/Scripts/python.exe"
}
```

### 2. Debug Configuration

Create `.vscode/launch.json` for debugging:

```json
{
  "configurations": [
    {
      "name": "Run Main",
      "type": "debugpy",
      "request": "launch",
      "program": "main.py",
      "console": "integratedTerminal"
    },
    {
      "name": "FastAPI App",
      "type": "debugpy",
      "request": "launch",
      "module": "uvicorn",
      "cwd": "${workspaceFolder}/",
      "args": [
        "main:app",
        "--reload"
      ]
    },
    {
      "name": "Django Server",
      "type": "debugpy",
      "request": "launch",
      "program": "manage.py",
      "args": [
        "runserver"
      ],
      "django": true
    }
  ]
}
```

### 3. Install Python Extension

```cmd
code --install-extension ms-python.python
code --install-extension ms-python.debugpy
```

## Ubuntu Installation

For Ubuntu/Linux systems, use the official pyenv installer:

### 1. Install Dependencies

```bash
sudo apt install -y make build-essential libssl-dev zlib1g-dev \
libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm \
libncurses5-dev libncursesw5-dev xz-utils tk-dev libffi-dev \
liblzma-dev git
```

### 2. Install pyenv

```bash
curl https://pyenv.run | bash
```

### 3. Configure Shell

```bash
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.profile
echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.profile
echo -e 'if command -v pyenv 1>/dev/null 2>&1; then\n eval "$(pyenv init -)"\nfi' >> ~/.profile

# Reload shell
exec "$SHELL"
```

### 4. Install Python

```bash
pyenv install --list
pyenv install 3.13.4
pyenv versions
pyenv global 3.13.4
```

## Troubleshooting

### Common Issues

#### 1. pyenv Command Not Found
**Problem:** `'pyenv' is not recognized as an internal or external command`

**Solutions:**
- Restart command prompt/PowerShell
- Check if `%USERPROFILE%\.pyenv\pyenv-win\bin` is in PATH
- Manually add to PATH if needed:
```cmd
setx PATH "%PATH%;%USERPROFILE%\.pyenv\pyenv-win\bin"
```

#### 2. Python Installation Fails
**Problem:** Error during `pyenv install`

**Solutions:**
- Check internet connection
- Try installing a different Python version
- Clear pyenv cache:
```cmd
pyenv install --list
# Try a stable version like 3.11.10
```

#### 3. Virtual Environment Issues
**Problem:** Cannot activate virtual environment

**Solutions:**
- Verify the virtual environment was created successfully
- Check the path to Scripts/activate
- Try creating a new virtual environment:
```cmd
python -m venv %userprofile%\.venv\test
%userprofile%\.venv\test\Scripts\activate
```

#### 4. VSCode Python Interpreter Issues
**Problem:** VSCode can't find Python interpreter

**Solutions:**
- Open Command Palette (`Ctrl+Shift+P`)
- Type "Python: Select Interpreter"
- Choose the correct virtual environment
- Or manually set in settings.json

### Useful Commands

```cmd
# List pyenv commands
pyenv help

# Show current Python version
pyenv version

# List all installed versions
pyenv versions

# List available versions to install
pyenv install --list

# Uninstall a Python version
pyenv uninstall 3.11.10

# Show pyenv installation directory
pyenv root
```

### File Locations

- **pyenv-win:** `%USERPROFILE%\.pyenv`
- **Python installations:** `%USERPROFILE%\.pyenv\pyenv-win\versions`
- **Virtual environments:** `%USERPROFILE%\.venv\`
- **pip cache:** `%USERPROFILE%\AppData\Local\pip\cache`

## Best Practices

1. **Use Virtual Environments:** Always create isolated environments for projects
2. **Pin Python Versions:** Use `.python-version` file in project root
3. **Requirements Files:** Use `requirements.txt` for dependency management
4. **Regular Updates:** Keep pyenv and Python versions updated
5. **Environment Naming:** Use descriptive names for virtual environments

## Related Links

- [pyenv-win GitHub Repository](https://github.com/pyenv-win/pyenv-win)
- [Python Official Documentation](https://docs.python.org/)
- [Virtual Environments Guide](https://docs.python.org/3/tutorial/venv.html)
- [Back to Main Guide](readme.md)