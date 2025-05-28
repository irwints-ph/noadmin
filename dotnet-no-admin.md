## Install Dotnet 
- Download the .NET SDK or Runtime binaries from the [Microsoft website][dn]. 
  - [Windows Version SDK 8][dn8w]
- Unzip the contents of the downloaded archive and move to C:\sw\dotnet
- Setup dotnet environment Variables

### dotnet environment Variables
```bash
setx DOTNET_ROOT C:\sw\dotnet\sdk-8.0.410-win-x64
rundll32 sysdm.cpl,EditEnvironmentVariables
```
`add %DOTNET_ROOT% to path`

### dotnet-ef
```bash
dotnet tool install --global dotnet-ef --version 9.0.5
```
> environment variable DOTNET_ROOT is needed by dotnet-ef to work

[dn]:https://dotnet.microsoft.com/en-us/download/dotnet
[dn8w]:https://dotnet.microsoft.com/en-us/download/dotnet/thank-you/sdk-8.0.410-windows-x64-binaries
