# Overview

This repository provides a structured guide for setting up a complete development environment on Windows **without administrator privileges**.

It is designed for environments where admin access is restricted, such as:
- corporate laptops
- school or university machines
- shared systems

---

## 🎯 What This Covers

You will learn how to install and configure:

- Code editors (VSCode, Notepad++)
- Version control (Git)
- Programming runtimes (Node.js, Python, .NET)
- Databases (PostgreSQL, MySQL, SQLite)
- Terminal and shell enhancements
- System configuration (PATH, registry, VSCode settings)

All tools are installed using:
- Portable versions, or
- User-space (non-admin) installations

---

## ⚙️ Installation Strategy

Instead of using system-wide installers, this guide follows a consistent approach:

1. Download portable or zip distributions
2. Extract to a user-writable directory (e.g. `C:\sw\`)
3. Manually configure environment variables
4. Verify installation via command line

This avoids:
- admin prompts
- system-level changes
- dependency on IT policies

---

## 📁 Recommended Directory Structure

Use a single root folder (e.g., `C:\sw\`) to keep all tools organized and easy to manage:

```
C:\sw\
 ├── vscode\
 ├── git\
 ├── notepadpp\
 ├── dotnet\
 ├── python\
 ├── node\
 ├── qodo\
 ├── postgresql\
 ├── mysql\
 ├── sqlite\
 └── config\
      ├── env\
      ├── vscode\
      └── registry\
```

- **Tools**: Each tool gets its own folder for binaries and configs.  
- **Databases**: Keep database installs separate for clarity.  
- **Config**: Store reusable scripts, environment variable files, and registry tweaks here.  

---

## ✅ Verification Checklist

After setup, confirm everything works by running:

- `code --version` (VSCode)  
- `git --version` (Git)  
- `python --version` (Python)  
- `node --version` (Node.js)  
- `dotnet --version` (.NET SDK)  
- `psql --version` (PostgreSQL)  

---

## 🔗 Next Steps

- [Prerequisites](docs/getting-started/prerequisites.md) → Ensure your system is ready  
- [VSCode Setup](docs/tools/vscode.md) → Start with your editor  
- [System Configuration](docs/system/environment-variables.md) → Configure PATH and registry  
