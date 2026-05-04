# Command Prompt (CMD) Customization (No Admin Required)

Customize the Windows Command Prompt to improve readability and usability.

All changes in this guide:

* Apply only to the current user
* Do not require administrator privileges
* Are fully reversible

---

## 🎨 Custom Prompt (Temporary)

You can change the prompt for the current session only.

### Example Prompt

```cmd id="cmd01"
SET PROMPT=$+$M$_%COMPUTERNAME%$_$P$_$$$S
```

### What it does:

* Shows computer name
* Shows current directory
* Adds line breaks for readability

---

## 🔁 Persistent Prompt (Recommended)

You have two safe ways to make the prompt permanent.

---

### Option 1: Using SETX (Command Line)

```cmd id="cmd02"
SETX PROMPT "$+$M$_%COMPUTERNAME%$_$P$_$$$S"
```

> ⚠️ Note: This applies only to **new CMD sessions**.

---

### Option 2: Using GUI Environment Variables (Recommended)

This is the safest and most user-friendly method.

#### Steps:

1. Press `Win + R`

2. Run:

   ```text
   rundll32 sysdm.cpl,EditEnvironmentVariables
   ```

3. Under **User variables**, click **New** (or edit existing variable)

4. Set:

   * **Variable name:**

     ```
     PROMPT
     ```

   * **Variable value:**

     ```
     $+$M$_%COMPUTERNAME%$_$P$_$$$S
     ```

5. Click **OK → OK → Apply**

> 💡 This method is recommended because it avoids issues like PATH truncation that can occur with `SETX`.

---

## ⚖️ SETX vs GUI Comparison

| Method                      | Pros                   | Cons                                      |
| --------------------------- | ---------------------- | ----------------------------------------- |
| SETX                        | Fast, scriptable       | Can truncate long values, harder to debug |
| GUI (Environment Variables) | Safe, visual, reliable | Slightly slower to configure              |

---

## 🎨 Simple Prompt Alternatives

### Basic clean prompt

```cmd id="cmd03"
SET PROMPT=$P$G
```

### Show only current directory

```cmd id="cmd04"
SET PROMPT=$P
```

---

## 🌈 Change CMD Colors

You can set default Command Prompt colors using registry (no admin required).

### Set Green Text

```cmd id="cmd05"
reg add "HKCU\Software\Microsoft\Command Processor" /v DefaultColor /t REG_DWORD /d 0x0a /f
```

### Color Reference

| Value | Color |
| ----- | ----- |
| 0x0a  | Green |
| 0x07  | White |
| 0x0c  | Red   |
| 0x0b  | Cyan  |

---

## 🔄 Apply Changes Immediately

Restart Command Prompt or run:

```cmd id="cmd06"
cmd /k
```

---

## ⚠️ Important Notes

### SET vs SETX

* `SET` → temporary (current session only)
* `SETX` → permanent (new sessions only)

---

### Environment Variable Behavior

* Changes made via SETX or GUI only apply to **new terminal sessions**
* You must restart CMD for changes to appear

---

## 🧩 Useful CMD Tips

### Show all environment variables

```cmd id="cmd07"
set
```

---

### Open CMD in current folder

* Shift + Right Click → **Open in Terminal**
* Or use registry tweaks from:

  ```
  docs/system/registry-tweaks.md
  ```

---

## 🛠 Troubleshooting

---

### ❌ Prompt not updating

**Fix**

* Close and reopen CMD
* Ensure you used SETX or GUI method

---

### ❌ SETX not applying correctly

**Cause**
Environment variables only load on new sessions.

**Fix**

* Restart CMD
* Or log out and log back in

---

### ❌ Weird prompt characters

**Fix**

* Ensure correct syntax (`$P`, `$G`, etc.)
* Do not mix PowerShell prompt syntax with CMD

---

## 📍 Default Prompt Reference

Default CMD prompt is:

```cmd id="cmd08"
$P$G
```

Meaning:

* `$P` = current path
* `$G` = `>` prompt symbol
