# Git (Portable Installation – No Admin Required)

This guide explains how to install and configure Git on Windows using a **portable setup**.

It is designed for a fully user-space development environment:

* No administrator privileges required
* Works with VSCode portable setup
* Uses `C:\sw\` structure
* Compatible with Node.js, Python, and other tools

---

## 🚀 Download Git (Portable Version)

Download from:

* https://git-scm.com/downloads/win

Select:

* **Portable Git ("thumbdrive edition")**
![Git Portable](/img/git-portable.png)
---

## 📦 Install Git (No Admin Required)

### Step 1: Create Directory

```cmd id="git01"
mkdir C:\sw\PortableGit
```

---

### Step 2: Extract Files

Extract the downloaded archive into:

```text id="git02"
C:\sw\PortableGit
```

---

## 📁 Expected Folder Structure

```text id="git03"
C:\sw\PortableGit
  ├── bin
  ├── cmd
  ├── mingw64
  ├── usr
  └── git-bash.exe
```

---

## 🔧 Add Git to PATH (Required)

Add the following to **User PATH**:

```text id="git04"
C:\sw\PortableGit
C:\sw\PortableGit\bin
```

📖 Related:

* [Environment Variables Setup](../system/environment-variables.md)

---

## ✅ Verify Installation

```cmd id="git05"
git --version
```

Check location:

```cmd id="git06"
where git
```

Expected output:

```text id="git07"
C:\sw\PortableGit\bin\git.exe
```

---

## ⚙️ Initial Git Configuration

Set your identity:

```bash id="git08"
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

Verify configuration:

```bash id="git09"
git config --list
```

---

## 🔐 Authentication (IMPORTANT)

GitHub no longer supports password authentication for Git over HTTPS.

You must use:

* Personal Access Token (PAT) for CLI usage
* VSCode browser login for GUI workflows

---

## 🔑 Option 1: Personal Access Token (CLI)

Use this when working in Command Prompt or terminal.

---

### Step 1: Go to GitHub Token Settings

* https://github.com/settings/tokens
* Or:

  ```
  GitHub → Settings → Developer settings → Personal access tokens → Tokens (classic)
  ```

---

### Step 2: Generate New Token

* Click **"Generate new token (classic)"**

* Add description:

  ```
  Git CLI on Windows
  ```

* Set expiration:

  * Recommended: **90 days or 1 year**

* Select scopes:

  * ✅ `repo` → repository access
  * ✅ `workflow` → GitHub Actions support
  * ✅ `write:packages` → package registry access

---

### Step 3: Copy and Save Token

* Click **Generate token**
* ⚠️ Copy immediately (you will not see it again)
* Store securely (password manager recommended)

---

### Step 4: Use Token in Git

When prompted:

```text id="git10"
Username for 'https://github.com': yourusername
Password for 'https://yourusername@github.com': <paste token here>
```

---

### 🧪 Test Authentication

```bash id="git11"
# Clone repository
git clone https://github.com/yourusername/your-repo.git

# Check remote
git remote -v

# Push changes
git push origin main
```

---

## 🌐 Option 2: VSCode Browser Authentication (Recommended)

When using VSCode:

* Browser opens automatically
* Login to GitHub
* Authentication is handled automatically

📖 Related:

* [VSCode Setup](vscode.md)
* [VSCode Configuration](../system/vscode-config.md)

---

## 🔗 VSCode Integration

Ensure VSCode uses portable Git:

```json id="git12"
"git.path": "C:\\sw\\PortableGit\\bin\\git.exe"
```

---

## 🔄 Updating Portable Git

To update Git:

1. Download new portable version
2. Replace contents of:

   ```
   C:\sw\PortableGit
   ```
3. No reinstall or admin rights required

---

## ⚠️ Common Issues

---

### ❌ Git not recognized

**Cause**
PATH not set correctly

**Fix**
Ensure:

```text id="gitfix01"
C:\sw\PortableGit\bin
```

Then restart terminal.

---

### ❌ Authentication failed

**Cause**
Using password instead of token

**Fix**

* Use Personal Access Token (PAT)
* Or VSCode browser login

---

### ❌ VSCode cannot find Git

**Fix**

```json id="gitfix02"
"git.path": "C:\\sw\\PortableGit\\bin\\git.exe"
```

Restart VSCode after changes.

---

### ❌ Multiple Git installations detected

Check:

```cmd id="gitfix03"
where git
```

If multiple results appear:

* Remove system Git from PATH
* Keep only `C:\sw\PortableGit`

---

## 🧠 Best Practice Setup

Recommended structure:

```text id="gitbp01"
C:\sw\
  ├── vscode
  ├── git
  ├── node
  ├── python
```

Git-specific paths:

```text id="gitbp02"
C:\sw\PortableGit\bin
```

---

## 📌 Related Guides

---

### 🛠 System Setup

* [Environment Variables](../system/environment-variables.md)
* [VSCode Configuration](../system/vscode-config.md)
* [Registry Tweaks](../system/registry-tweaks.md)

---

### 🧰 Development Tools

* [VSCode Setup](vscode.md)
* [Node.js Setup](node.md)
* [Python Setup](python.md)
