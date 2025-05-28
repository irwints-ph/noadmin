## Python
`Disable from Microsoft Store App Installer python and pyhton3`
  - Settings > Apps > Advanced app settings > App execution aliases

### Install [pyenv-win](https://github.com/pyenv-win/pyenv-win) from `powershell`

`allow to run powershell script for user`

```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

`download and install pyenv`

```powershell
Invoke-WebRequest -UseBasicParsing -Uri "https://raw.githubusercontent.com/pyenv-win/pyenv-win/master/pyenv-win/install-pyenv-win.ps1" -OutFile "./install-pyenv-win.ps1"

./install-pyenv-win.ps1
```

### Install Python
```bash
pyenv install 3.13.3
pyenv global 3.13.3
pyenv version
```

### Install Virtual Environment
```bash
python -m venv %userprofile%/.venv/fastapi
```

### Activate the virtual environment
```bash
%userprofile%/.venv/fastapi/Scripts/activate
python.exe -m pip install --upgrade pip
```

### Install modules on Virtual Environment
```bash
python -m pip install fastapi uvicorn
```

`.vscode\settings.json`
```json
{
  "python.defaultInterpreterPath":"~/.venv/fastapi/Scripts/python.exe"
}
```
`.vscode\launch.json`
```json
{
  "configurations": [
    {
      "name": "Run Main",
      "type": "debugpy",
      "request": "launch",
      "program": "main.py",
      "console": "integratedTerminal"
    },
    {
      "name": "FastAPI App",
      "type": "debugpy",
      "request": "launch",
      "module": "uvicorn",
      "cwd": "${workspaceFolder}/",
      // args per command separated by space indicated by comma      
      "args": [
        "main:app",
        "--reload"
      ]
    }    
  ]
}
```
