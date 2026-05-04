# Windows Registry Tweaks (No Admin Required)

Customize your Windows context menu and behavior without administrator privileges.

All tweaks in this guide:

* Apply only to the current user (`HKEY_CURRENT_USER`)
* Do not require admin rights
* Are fully reversible

---

## ⚠️ Safety First

Before applying any registry changes:

### Backup Registry (Recommended)

```cmd
reg export HKEY_CURRENT_USER\Software\Classes backup-classes.reg
```

> 📁 **Note:** This command creates the backup file (`backup-classes.reg`) in the **current working directory** (the folder where the command was executed).
>
> To control the location, specify a full path:
>
> ```cmd
> reg export HKEY_CURRENT_USER\Software\Classes C:\sw\backup-classes.reg
> ```

### Key Notes

* Only modify:

  ```
  HKEY_CURRENT_USER
  ```
* Avoid editing unknown registry keys
* Double-check file paths before applying

---

## 📦 How to Apply Registry Files

1. Create a `.reg` file:

   ```cmd
   notepad your-file.reg
   ```

2. Paste the registry content

3. Save the file (ensure it has `.reg` extension)

4. Double-click the file

5. Confirm all prompts

---

## 🧩 Context Menu Enhancements

---

### ▶️ Open with VSCode

```reg
Windows Registry Editor Version 5.00

[HKEY_CURRENT_USER\Software\Classes\Directory\shell\Open with VSCode]
@="Open with VSCode"
"Icon"="C:\\sw\\vscode\\Code.exe"

[HKEY_CURRENT_USER\Software\Classes\Directory\shell\Open with VSCode\command]
@="\"C:\\sw\\vscode\\code.exe\" \"%V\""

[HKEY_CURRENT_USER\Software\Classes\Directory\Background\shell\Open with VSCode]
@="Open with VSCode"
"Icon"="C:\\sw\\vscode\\Code.exe"

[HKEY_CURRENT_USER\Software\Classes\Directory\Background\shell\Open with VSCode\command]
@="\"C:\\sw\\vscode\\code.exe\" \"%V\""
```

**Expected Result**

* Right-click folder → Open with VSCode
* Opens the selected directory as a workspace

---

### ⚠️ Important Notes

* ✅ **Verify the path exists**

  Make sure VSCode is actually installed at:

  ```
  C:\sw\vscode\Code.exe
  ```

  If your installation is in a different location, update the path in the `.reg` file before applying.

---

* 🧠 **Why are there double backslashes (`\\`)?**

  In `.reg` files, the backslash (`\`) is an **escape character**.

  This means:

  ```
  C:\\sw\\vscode\\Code.exe
  ```

  actually represents:

  ```
  C:\sw\vscode\Code.exe
  ```

  If you use a single backslash, the registry file may not work correctly.

---

* 📝 **Quoted paths**

  Paths are wrapped in quotes like:

  ```
  "\"C:\\sw\\vscode\\code.exe\" \"%V\""
  ```

  This ensures:

  * Paths with spaces work correctly
  * The selected folder (`%V`) is passed properly

---

### ▶️ Open in Command Prompt

```reg
Windows Registry Editor Version 5.00

[HKEY_CURRENT_USER\SOFTWARE\Classes\Directory\Background\shell\Open in Terminal]
@="Open in Terminal"
"Icon"="%SystemRoot%\\System32\\shell32.dll,40"

[HKEY_CURRENT_USER\SOFTWARE\Classes\Directory\Background\shell\Open in Terminal\command]
@="cmd.exe /K cd \"%V\""

[HKEY_CURRENT_USER\SOFTWARE\Classes\Directory\shell\Open in Terminal]
@="Open in Terminal"
"Icon"="%SystemRoot%\\System32\\shell32.dll,40"

[HKEY_CURRENT_USER\SOFTWARE\Classes\Directory\shell\Open in Terminal\command]
@="cmd.exe /K cd \"%V\""
```

**Expected Result**

* Right-click folder → Open in Terminal
* Command Prompt opens in the selected directory

---

### ▶️ Open in PowerShell

```reg
Windows Registry Editor Version 5.00

[HKEY_CURRENT_USER\SOFTWARE\Classes\Directory\Background\shell\Open in PowerShell]
@="Open in PowerShell"
"Icon"="powershell.exe"

[HKEY_CURRENT_USER\SOFTWARE\Classes\Directory\Background\shell\Open in PowerShell\command]
@="powershell.exe -NoExit -Command Set-Location '%V'"

[HKEY_CURRENT_USER\SOFTWARE\Classes\Directory\shell\Open in PowerShell]
@="Open in PowerShell"
"Icon"="powershell.exe"

[HKEY_CURRENT_USER\SOFTWARE\Classes\Directory\shell\Open in PowerShell\command]
@="powershell.exe -NoExit -Command Set-Location '%V'"
```

**Expected Result**

* Right-click folder → Open in PowerShell
* PowerShell opens in the selected directory

---

## 🧹 Removing Context Menu Entries

To undo changes, create and run removal `.reg` files.

---

### Remove VSCode Entry

```reg
Windows Registry Editor Version 5.00

[-HKEY_CURRENT_USER\Software\Classes\Directory\shell\Open with VSCode]
[-HKEY_CURRENT_USER\Software\Classes\Directory\Background\shell\Open with VSCode]
```

---

### Remove Command Prompt Entry

```reg
Windows Registry Editor Version 5.00

[-HKEY_CURRENT_USER\SOFTWARE\Classes\Directory\Background\shell\Open in Terminal]
[-HKEY_CURRENT_USER\SOFTWARE\Classes\Directory\shell\Open in Terminal]
```

---

### Remove PowerShell Entry

```reg
Windows Registry Editor Version 5.00

[-HKEY_CURRENT_USER\SOFTWARE\Classes\Directory\Background\shell\Open in PowerShell]
[-HKEY_CURRENT_USER\SOFTWARE\Classes\Directory\shell\Open in PowerShell]
```

---

## 🛠 Troubleshooting

### ❌ Context menu item not showing

**Fix**

```cmd
taskkill /f /im explorer.exe && start explorer.exe
```

* Or log out and log back in
* Reapply the `.reg` file

---

### ❌ Wrong application opens

**Fix**

* Verify install path (e.g. `C:\sw\vscode\code.exe`)
* Update `.reg` file and reapply

---

### ❌ Access denied when applying

**Fix**

* Ensure keys are under `HKEY_CURRENT_USER`
* Do not use `HKEY_LOCAL_MACHINE`
* Check antivirus restrictions
