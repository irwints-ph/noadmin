# ⚙️ Visual Studio Community Edition Installation Script (PowerShell)

```powershell
# Run as Administrator

# Download Visual Studio Community bootstrapper
$vsInstaller = "$env:USERPROFILE\Downloads\vs_community.exe"
Invoke-WebRequest -Uri "https://aka.ms/vs/17/release/vs_community.exe" -OutFile $vsInstaller

# Install with specific workloads
Start-Process -FilePath $vsInstaller -ArgumentList `
"--quiet --wait --norestart --installPath C:\Program Files\Microsoft Visual Studio\2022\Community `
--add Microsoft.VisualStudio.Workload.CoreEditor `
--add Microsoft.VisualStudio.Workload.NetWeb `
--add Microsoft.VisualStudio.Workload.ManagedDesktop `
--includeRecommended" -Wait -Verb RunAs

Write-Output "Visual Studio Community Edition installation complete."
```

---

# 🔄 Visual Studio Community Edition Update Script (PowerShell)

```powershell
# Run as Administrator

# Path to Visual Studio Installer
$vsInstaller = "C:\Program Files (x86)\Microsoft Visual Studio\Installer\vs_installer.exe"

# Update all installed instances silently
Start-Process -FilePath $vsInstaller -ArgumentList "update --quiet --wait --norestart" -Wait -Verb RunAs

Write-Output "Visual Studio Community Edition updated successfully."
```

---

# 📦 Specifying Packages (Workloads & Components)

Visual Studio uses **workload IDs** and **component IDs**. You can mix and match depending on what developers need:

| Workload ID | Description |
|-------------|-------------|
| `Microsoft.VisualStudio.Workload.CoreEditor` | Basic editor only |
| `Microsoft.VisualStudio.Workload.ManagedDesktop` | .NET desktop development |
| `Microsoft.VisualStudio.Workload.NetWeb` | ASP.NET and web development |
| `Microsoft.VisualStudio.Workload.NativeDesktop` | C++ desktop development |
| `Microsoft.VisualStudio.Workload.Azure` | Azure development |
| `Microsoft.VisualStudio.Workload.Data` | Data storage and processing |
| `Microsoft.VisualStudio.Workload.Python` | Python development |
| `Microsoft.VisualStudio.Workload.Node` | Node.js development |

👉 To add workloads, append `--add <workloadID>` to the installer command.  
👉 To add individual components, use `--add <componentID>` (e.g., `--add Microsoft.VisualStudio.Component.Git`).

---

# 🛡 ManageEngine Integration Notes
- Upload these scripts into ManageEngine Endpoint Central as **configuration tasks**.  
- Assign to developer device groups.  
- Use **update script** on a schedule (monthly/quarterly).  
- Redirect logs for auditing:
  ```powershell
  .\vs-install.ps1 | Out-File "C:\Logs\vs-install.log"
  ```

---

This gives you a **repeatable, automated way** to install/update Visual Studio Community with exactly the workloads you want.  

Would you like me to also prepare a **recommended workload bundle for typical web developers** (e.g., VSCode + Git + Node.js + .NET + SQL + VS Community with Web workload) so your ManageEngine deployment scripts form a complete dev environment in one go?