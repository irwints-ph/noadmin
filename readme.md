# No Windows Admin Installs
1. [VSCode](#installing-vscode)
2. [Git](#installing-git)
3. [dotnet](dotnet-no-admin.md)
4. [Python](python-no-admin.md#python)
    - [pyenv-win](python-no-admin.md#install-pyenv-win)
5. [PostgreSQL](postgresql-no-admin.md)
6. [MySQL](mysql-no-admin.md)
1. [Warning](#warning)
1. [Others](#others)

### Installing VSCode
1. Download [VSCode][1] windows .zip version

    ![vscode-select](img/vscode-zip.png)
1. Extract to c:\sw\code
1. Add c:\sw\code\bin to [path](#adding-to-path)

### Installing Git
1. Download [git][2] portable

  ![git-select](img/git-portable.png)

2. Extract to C:\sw\PortableGit
1. Add C:\sw\PortableGit and C:\sw\PortableGit\bin to [path](#setup-environment-variables)
1. configure git in VS Code

### Configure git in VSCode
`file->prefernce->setting or ctrl + ,`
> or copy the [VSCode configuration](#vscode-configuration-for-all-projects) below
1. keyin git.path
2. Click Edit in settings.json  
  ![git.path][3] 
  ![settings.json][4]

  `"git.path": "C:\\sw\\PortableGit\\bin\\git.exe"`
  
3. save and re-open git
   
`User manager for login on 1st use`

![git-manager](img/vsc-git-credential.png)

4. Or in CMD
```bash
git config user.name "[your name]"
git config user.email "[your email]"
```
## VSCode configuration for all projects
`%userprofile%\AppData\Roaming\Code\User\settings.json`
```json
{
  "git.path": "C:\\sw\\PortableGit\\bin\\git.exe",                 //Git Executable Path
  "editor.fontSize": 18,                                           //Editor Font Size
  "terminal.integrated.defaultProfile.windows": "Command Prompt",  //Default Terminal - CMD
  "terminal.integrated.fontSize": 18,                              //Terminal Font Size
  "editor.tabSize": 2,                                             //Default Editor space tab size
  "workbench.colorCustomizations": {                               //Color Customization
    "terminal.foreground" : "#1AFF01",                             //Terminal Text Color
    "terminal.background" : "#000000"                              //Terminal Background Color
  },
  "terminal.integrated.cursorBlinking": true,                      //Terminal Corsor
  "editor.minimap.enabled": false,                                 //Hide Minimap
  "hediet.vscode-drawio.resizeImages": null,                       //Drwa IO Extsion resize image
}
```

# Setup environment Variables
```bash
setx PATH "%PATH%;C:\sw\PortableGit;C:\sw\PortableGit\bin;C:\sw\code\bin;"
```
## Warning
> Using SETX with varaible will set the current value not future values

> Recommended to use **rundll32 sysdm.cpl,EditEnvironmentVariables** instead


## Install VSCode extensions
```bash
code --install-extension humao.rest-client
code --install-extension shd101wyy.markdown-preview-enhanced
code --install-extension ms-python.debugpy
code --install-extension ritwickdey.liveserver
code --github.copilot
code --hediet.vscode-drawio
code --yy0931.vscode-sqlite3-editor

code --list-extensions

code --github.copilot-chat

```

## Color and Prompt
```
reg add "HKCU\Software\Microsoft\Command Processor" /v DefaultColor /t REG_DWORD /d 0x0a /f

SETX PROMPT $+$M$_$P$_$$$S
```

## Warning
> Using SETX with varaible will set the current value not future values

> Recommended to use **rundll32 sysdm.cpl,EditEnvironmentVariables** instead

### Open Environment Variable for user
```bash
rundll32 sysdm.cpl,EditEnvironmentVariables
```

### Set Powershell Propmt
```ps
function prompt {
  Write-Host ("PS`n" + $(Get-Location) +"`n$") -NoNewline
  return " "
}
```

```explorer
%userprofile%\.vscode\extensions
%userprofile%\AppData\Roaming\Code\User\settings.json
```

[1]:https://code.visualstudio.com/download
[2]:https://git-scm.com/downloads/win
[3]:img/vsc-git-path.png
[4]:img/vsc-git-path-save.png
