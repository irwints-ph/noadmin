# VSCode System Configuration (No Admin Required)

This guide defines a consistent Visual Studio Code setup for a portable, no-admin Windows development environment.

It ensures:

* Consistent editor behavior across machines
* Stable Git integration (portable Git supported)
* Clean terminal experience
* Minimal, reproducible configuration

---

## 📁 Configuration File Location

VSCode stores user settings here:

```text id="vscconfigloc01"
%userprofile%\AppData\Roaming\Code\User\settings.json
```

---

## 🚀 Open Configuration File

### Method 1 (Recommended)

```cmd id="vscconfigopen01"
notepad %userprofile%\AppData\Roaming\Code\User\settings.json
```

### Method 2 (Inside VSCode)

1. Open VSCode
2. Press `Ctrl + ,`
3. Click:

   ```
   Open Settings (JSON)
   ```

---

## ⚙️ Core Configuration Concepts

This setup focuses on:

### 1. Portable Tooling

* Git installed in `C:\sw\PortableGit`
* No dependency on system Git

### 2. Consistent Editor Behavior

* Fixed font size and indentation
* Format-on-save enabled
* Reduced UI clutter

### 3. Predictable Terminal

* Uses Command Prompt as default
* Stable behavior across environments

---

## 🧩 Git Integration (Portable Setup)

If using portable Git:

```text id="vscgitpath01"
C:\sw\PortableGit\bin\git.exe
```

📖 Related:

* [Git Setup Guide](../tools/git.md)

---

## 🖥 Terminal Configuration

* Uses Command Prompt for consistency
* Avoids PowerShell/Git Bash mismatch issues
* Ensures predictable behavior across machines

---

## 🎨 UI & Editor Preferences

* Larger font for readability
* Tabs set to 2 spaces for consistency
* Minimap disabled to reduce noise
* Auto-save enabled for convenience

---

## 📦 Recommended Extensions Note

This file does **not manage extensions**.

Use:

* `docs/tools/vscode.md` for [extension setup](/docs/tools/vscode.md#-install-extensions-optional)

---

## 🧠 Best Practice Principles

* Keep settings minimal
* Avoid per-project overrides unless necessary
* Prefer portability over system integration
* Always assume `C:\sw\` structure

---

## 📌 Full Recommended VSCode Configuration (Golden Setup)

This is the **final recommended configuration** for this environment:

```json id="vscconfigfinal02"
{
  "git.path": "C:\\sw\\PortableGit\\bin\\git.exe",

  "editor.fontSize": 18,
  "editor.tabSize": 2,
  "editor.insertSpaces": true,

  "editor.minimap.enabled": false,
  "editor.wordWrap": "on",
  "editor.formatOnSave": true,

  "terminal.integrated.defaultProfile.windows": "Command Prompt",
  "terminal.integrated.fontSize": 18,
  "terminal.integrated.cursorBlinking": true,

  "workbench.colorTheme": "Default Dark+",
  "workbench.iconTheme": "vs-seti",

  "workbench.colorCustomizations": {
    "terminal.foreground": "#1AFF01",
    "terminal.background": "#000000"
  },

  "files.autoSave": "onFocusChange",

  "explorer.confirmDelete": false,
  "explorer.confirmDragAndDrop": false,

  "hediet.vscode-drawio.resizeImages": null
}
```

---

## 🔄 After Applying Configuration

1. Save `settings.json`
2. Restart VSCode
3. Verify:

   * Git works (`git --version`)
   * Terminal opens as CMD
   * Font size updates
   * Auto-save works

---

## ⚠️ Common Issues

### ❌ Git not detected in VSCode

**Fix**
Ensure:

```text id="vscfixgit01"
C:\sw\PortableGit\bin\git.exe
```

Then verify:

```cmd id="vscfixgit02"
where git
```

---

### ❌ Settings not applying

**Fix**

* Restart VSCode completely
* Ensure JSON syntax is valid

---

### ❌ Terminal not using CMD

**Fix**
Check:

```json id="vscfixterm01"
"terminal.integrated.defaultProfile.windows": "Command Prompt"
```

---

## 📌 Related Guides

---

### 🛠 System Setup

* [Environment Variables](environment-variables.md)
* [CMD Customization](cmd-customization.md)
* [PowerShell Customization](powershell-customization.md)
* [Registry Tweaks](registry-tweaks.md)

---

### 🧰 Development Tools

* [VSCode Setup](../tools/vscode.md)
* [Git Setup](../tools/git.md)
