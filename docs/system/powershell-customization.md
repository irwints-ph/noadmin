# PowerShell Customization (No Admin Required)

Customize your PowerShell experience to improve readability, usability, and productivity.

All changes in this guide:

* Apply only to the current user
* Do not require administrator privileges
* Are fully reversible

---

## 🚀 Getting Started

### Open PowerShell

You can open PowerShell in several ways:

* Press `Win + R`, type:

  ```text
  powershell
  ```
* Search for **PowerShell** in the Start Menu
* Open via terminal (if configured)

---

## 📁 PowerShell Profile

PowerShell uses a **profile script** that runs every time it starts.

---

### Check if Profile Exists

```powershell
Test-Path $PROFILE
```

---

### Create Profile (if missing)

```powershell
# Create directory if needed
New-Item -ItemType Directory -Path (Split-Path $PROFILE) -Force

# Create profile file
New-Item -ItemType File -Path $PROFILE -Force
```

---

### Edit Profile

```powershell
notepad $PROFILE
```

---

## ⚠️ Execution Policy (If Needed)

If you see errors when loading your profile:

```powershell
Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned
```

> Only run this if PowerShell blocks your profile script.

---

## 🎨 Basic Prompt Customization

Replace your prompt with a more informative version.

```powershell
function prompt {
    $hostname = $env:COMPUTERNAME
    $currentPath = Get-Location
    $userName = $env:USERNAME

    Write-Host "[$userName@$hostname]" -ForegroundColor Green -NoNewline
    Write-Host "`nPS " -ForegroundColor Yellow -NoNewline
    Write-Host "$currentPath" -ForegroundColor Blue
    Write-Host "$ " -ForegroundColor White -NoNewline

    return " "
}
```

---

### Result

```
[username@computer]
PS C:\Users\username
$
```

---

## ⚡ Compact Prompt (Single Line)

```powershell
function prompt {
    $hostname = $env:COMPUTERNAME
    $currentPath = Get-Location
    $userName = $env:USERNAME

    Write-Host "[$userName@$hostname] " -ForegroundColor Green -NoNewline
    Write-Host "PS $currentPath" -ForegroundColor Cyan -NoNewline
    Write-Host " $ " -ForegroundColor White -NoNewline

    return " "
}
```

---

## 🔀 Advanced Prompt (Git Support)

Displays the current Git branch if inside a repository.

```powershell
function prompt {
    $hostname = $env:COMPUTERNAME
    $currentPath = Get-Location
    $userName = $env:USERNAME

    $gitBranch = ""

    if (Get-Command git -ErrorAction SilentlyContinue) {
        $branch = git branch --show-current 2>$null
        if ($branch) {
            $gitBranch = " (git:$branch)"
        }
    }

    Write-Host "[$userName@$hostname]" -ForegroundColor Green -NoNewline
    Write-Host "$gitBranch" -ForegroundColor Magenta -NoNewline
    Write-Host "`nPS " -ForegroundColor Yellow -NoNewline
    Write-Host "$currentPath" -ForegroundColor Blue
    Write-Host "$ " -ForegroundColor White -NoNewline

    return " "
}
```

---

## 🔄 Apply Changes

After saving your profile:

```powershell
. $PROFILE
```

Or restart PowerShell.

---

## 🛠 Troubleshooting

---

### ❌ `$PROFILE` not working

**Cause**
You are running Command Prompt instead of PowerShell.

**Fix**

* PowerShell prompt looks like:

  ```
  PS C:\Users\YourName>
  ```
* Command Prompt looks like:

  ```
  C:\Users\YourName>
  ```

---

### ❌ Execution policy error

**Fix**

```powershell
Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned
```

---

### ❌ Profile not loading

**Fix**

```powershell
Test-Path $PROFILE
. $PROFILE
```

---

### ❌ Colors not displaying correctly

**Fix**

* Use Windows Terminal (recommended)
* Test colors:

  ```powershell
  Write-Host "Test" -ForegroundColor Red
  ```

---

## 📍 Profile Locations

```powershell
$PROFILE | Get-Member -Type NoteProperty
```

Common paths:

* PowerShell (modern):

  ```
  %USERPROFILE%\Documents\PowerShell\Microsoft.PowerShell_profile.ps1
  ```

* Windows PowerShell (legacy):

  ```
  %USERPROFILE%\Documents\WindowsPowerShell\Microsoft.PowerShell_profile.ps1
  ```
