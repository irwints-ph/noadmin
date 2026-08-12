# Troubleshooting

## Common Issues

### PATH Not Updated
- **Problem:** Commands not recognized after installation
- **Solution:** 
  1. Close and reopen command prompt
  2. Use the GUI method for setting environment variables
  3. Verify PATH contains the correct directories

### Git Not Working in VSCode
- **Problem:** VSCode can't find Git
- **Solution:** 
  1. Check `git.path` setting in VSCode
  2. Ensure Git is in PATH
  3. Restart VSCode after configuration changes

### Git Authentication Issues
- **Problem:** "Authentication failed" or "remote: Support for password authentication was removed"
- **Solution:** 
  1. **For CLI:** Use Personal Access Token instead of password
  2. **For VSCode:** Choose "Use browser" when prompted
  3. Generate token at [GitHub Settings](https://github.com/settings/tokens)
  4. Use token as password when prompted in CLI

- **Problem:** VSCode keeps asking for credentials
- **Solution:**
  1. **If credential manager appears:** Choose "Use browser" option
  2. **If no dialog appears:** Browser should open automatically
  3. Complete authentication in browser (login to GitHub)
  4. Check if Git Credential Manager Core is installed
  5. Restart VSCode after authentication
  6. **Alternative:** Use Personal Access Token in VSCode terminal if browser auth fails

### Permission Errors
- **Problem:** Access denied when creating directories
- **Solution:** 
  1. Ensure you're using user-writable directories (`C:\sw\`)
  2. Check if your antivirus is blocking operations
  3. Try running the command prompt as your current user (do not "Run as Administrator")

### PowerShell Script Execution Blocked
- **Problem:** "File cannot be loaded because running scripts is disabled on this system."
- **Solution:** PowerShell's default security policy prevents running custom scripts (like profile scripts or installers).
  1. Open PowerShell
  2. Run the following command to allow scripts for your user only (does not require admin):
  ```powershell
  Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
  ```

### NPM Global Installation "Access Denied"
- **Problem:** Running `npm install -g <package>` fails with EPERM (Access Denied) trying to write to `C:\Program Files\nodejs`.
- **Solution:** Configure npm to use a folder in your user profile for global packages.
  1. Create a directory for global packages: `mkdir %USERPROFILE%\.npm-global`
  2. Tell npm to use this path: `npm config set prefix "%USERPROFILE%\.npm-global"`
  3. Add `%USERPROFILE%\.npm-global` to your PATH variable using the GUI.

### Git Clone Fails with "Filename too long"
- **Problem:** Cloning a repository or running `npm install` fails due to path length limitations on Windows.
- **Solution:** Enable long path support in Git configuration.
  1. Open your terminal and run:
  ```bash
  git config --global core.longpaths true
  ```

## Useful File Locations

```cmd
# VSCode extensions
%userprofile%\.vscode\extensions

# VSCode user settings
%userprofile%\AppData\Roaming\Code\User\settings.json

# Open environment variables GUI
rundll32 sysdm.cpl,EditEnvironmentVariables
```
