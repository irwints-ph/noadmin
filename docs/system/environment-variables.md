# Environment Variables Setup (No Admin Required)

Environment variables allow tools like Git, Node.js, Python, and VSCode to be used from any terminal.

This guide explains how to safely configure them on Windows **without administrator privileges**.

---

## ⚠️ Important Concept

Windows has two main scopes:

* **User variables** → safe, no admin required (used in this guide)
* **System variables** → requires admin access (NOT used here)

We only modify **User variables**.

---

## 🚀 Open Environment Variables Editor

### Method 1 (Recommended)

```cmd id="env01"
rundll32 sysdm.cpl,EditEnvironmentVariables
```

### Method 2 (Manual Navigation)

1. Open Start Menu
2. Search:

   ```
   Edit the system environment variables
   ```
3. Click **Environment Variables**

---

## 📁 Key Variables You Will Use

You will mainly work with:

* `PATH` → tells Windows where executables are located
* `PROMPT` → custom CMD prompt (see CMD customization guide)
* Tool-specific variables (optional)

---

## 🛠 Adding a New PATH Entry

### Steps:

1. Open Environment Variables
2. Under **User variables**, select `Path`
3. Click **Edit**
4. Click **New**
5. Add your folder path

---

### Example Paths

```text id="env02"
C:\sw\vscode\bin
C:\sw\git\bin
C:\sw\node
C:\sw\python
C:\sw\sqlite
```

---

## 📦 Recommended Standard Structure

All tools should be installed under:

```text id="env03"
C:\sw\
```

Example:

```text id="env03b"
C:\sw\vscode
C:\sw\git
C:\sw\node
C:\sw\python
```

Then add only required `bin` folders to PATH.

---

## 🔄 Verifying PATH Setup

After adding a path, test it in CMD:

```cmd id="env04"
where git
where node
where python
```

Or check versions:

```cmd id="env04b"
git --version
node --version
python --version
```

---

## ⚠️ Common Mistakes

### ❌ Forgetting to restart terminal

Changes only apply to **new sessions**

✔ Fix:

* Close CMD / PowerShell
* Reopen terminal

---

### ❌ Adding incorrect folder

Wrong:

```text id="envbad1"
C:\sw\git\git.exe
```

Correct:

```text id="envgood1"
C:\sw\git\bin
```

---

### ❌ Using System Variables

You do NOT need admin rights.

✔ Always use:

```
User variables
```

---

## 🔁 PATH vs SETX vs GUI

| Method           | Use Case     | Recommendation   |
| ---------------- | ------------ | ---------------- |
| GUI Editor       | Manual setup | ✅ Best option    |
| SETX             | Scripting    | ⚠️ Use carefully |
| System Variables | Admin setup  | ❌ Not needed     |

---

## ⚙️ Using SETX (Optional)

You can also modify PATH via command line:

```cmd id="env05"
setx PATH "%PATH%;C:\sw\git\bin"
```

> ⚠️ Warning:
>
> * Can truncate long PATH values
> * Only affects new terminal sessions
> * Harder to debug than GUI method

---

## 🧠 Best Practice Workflow

1. Install tool into:

   ```
   C:\sw\<tool>
   ```

2. Add only required `bin` folder to PATH

3. Restart terminal

4. Verify with:

   ```cmd
   tool --version
   ```

---

## 🧩 Useful Commands

### Show current PATH

```cmd id="env06"
echo %PATH%
```

### Locate executable

```cmd id="env07"
where <tool>
```

---

## 🛠 Troubleshooting

---

### ❌ Command not recognized

**Cause**
PATH not updated or terminal not restarted

**Fix**

* Restart CMD / PowerShell
* Verify PATH entry exists
* Use `where <tool>`

---

### ❌ Wrong version running

**Cause**
Multiple installations exist

**Fix**

```cmd id="env08"
where node
where python
```

Remove incorrect PATH entry.

---

### ❌ Broken PATH after SETX

**Cause**
SETX truncated or overwritten PATH

**Fix**

* Restore from GUI editor
* Use backup if available
* Avoid SETX for complex PATH editing

---

## 📌 Related Guides

* [CMD Customization](cmd-customization.md)
* [PowerShell Customization](powershell-customization.md)
* [Registry Tweaks](registry-tweaks.md)

---

## 🚀 Optional Upgrade (Advanced Concepts)

### 🔍 How Windows Resolves Commands

When you type a command like:

```cmd
node
```

Windows searches in this order:

1. Current directory
2. Folders in `PATH` (top to bottom)
3. System directories

👉 This is why PATH order matters.

---

### ⚠️ PATH Order Priority

If multiple versions of a tool exist:

```text
C:\sw\node_old
C:\sw\node_new
```

The **first one in PATH wins**.

✔ Fix:

* Move correct version higher in PATH list

---

### 🧪 Diagnosing PATH Issues

Use:

```cmd id="env09"
where node
where python
```

If multiple paths appear, Windows is detecting duplicates.

---

### 🧹 Clean PATH Strategy (Recommended)

To avoid issues:

* Keep all tools under `C:\sw\`
* Avoid mixing installers and portable versions
* Remove unused entries regularly

---

### 🔐 Safe Editing Rule

✔ Prefer GUI editor over SETX for complex PATH changes
✔ Always restart terminal after changes
✔ Keep a backup before major edits
