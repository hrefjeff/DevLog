# WSL2 on Windows 11

Instructions found [here](https://learn.microsoft.com/en-us/windows/wsl/install-manual)

1. Run powershell as administrator

```powershell
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```

2. 
