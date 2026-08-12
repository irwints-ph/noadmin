# ⚙️ Docker Desktop + WSL Installation Script (PowerShell)

```powershell
# Run as Administrator

# Enable WSL and Virtual Machine Platform
wsl --install

# Optional: Set default distro to Ubuntu
wsl --set-default-version 2

# Download Docker Desktop installer
$dockerInstaller = "$env:USERPROFILE\Downloads\DockerDesktopInstaller.exe"
Invoke-WebRequest -Uri "https://desktop.docker.com/win/main/amd64/Docker Desktop Installer.exe" -OutFile $dockerInstaller

# Install Docker Desktop silently
Start-Process -FilePath $dockerInstaller -ArgumentList "install --quiet" -Wait -Verb RunAs

# Enable WSL integration (default distro)
& "C:\Program Files\Docker\Docker\DockerCli.exe" -SwitchLinuxEngine

Write-Output "Docker Desktop + WSL installation complete."
```

---

# 🔄 Docker Desktop + WSL Update Script (PowerShell)

```powershell
# Run as Administrator

# Stop Docker Desktop if running
Stop-Process -Name "Docker Desktop" -Force -ErrorAction SilentlyContinue

# Download latest installer
$dockerInstaller = "$env:USERPROFILE\Downloads\DockerDesktopInstaller.exe"
Invoke-WebRequest -Uri "https://desktop.docker.com/win/main/amd64/Docker Desktop Installer.exe" -OutFile $dockerInstaller

# Run update silently
Start-Process -FilePath $dockerInstaller -ArgumentList "install --quiet" -Wait -Verb RunAs

Write-Output "Docker Desktop updated successfully."
```

---

# 🛡 ManageEngine Integration Notes

- **Deployment:** Upload these scripts into ManageEngine Endpoint Central (or Desktop Central) as **configuration tasks**.  
- **Execution:** Assign them to device groups (e.g., developer laptops).  
- **Scheduling:** Use ManageEngine’s scheduler to run the update script monthly or quarterly.  
- **Logging:** Redirect script output to a log file for auditing:
  ```powershell
  .\docker-install.ps1 | Out-File "C:\Logs\docker-install.log"
  ```

---

# ✅ Verification Step (Post-Deployment)

After ManageEngine pushes the script, verify on endpoints:
```powershell
docker --version
wsl --version
docker run hello-world
```