# DevLog
Things and stuff learned along the way

# 2025-10-05

Common conversation I'm having across teams deploying containerized applications: "I want to do some development with Docker containers on WSL2. In Windows 11, what is the difference between Hyper-V, Virtual Machine Platform, and Windows Hypervisor Platform? Should I enable all of these features?"

**BLUF**: Just enable Virtual Machine Platform. This gives you everything needed for WSL2 and Docker Desktop without the extra overhead of the full Hyper-V management tools.

### Virtual Machine Platform

- **What it is**: A type 1 hypervisor built into Windows Server and Windows Pro/Enterprise, allowing you to create and manage virtual machines (VMs). 
- **In layman's terms**: The lightweight virtualization component that powers WSL2
- Provides core hypervisor functionality without the full management stack
- **This is what you actually need for Docker on WSL2**

### Hyper-V

- **What it is**: The full hypervisor platform with management tools and UI
- Lets you create and manage traditional Windows VMs through Hyper-V Manager
- Includes networking and storage virtualization features
- **Automatically enables Virtual Machine Platform when installed**

### Windows Hypervisor Platform

- An API layer that lets third-party virtualization software (like VirtualBox, VMware) work alongside the Windows hypervisor
- Only needed if you're using other virtualization tools that need to interact with Windows' hypervisor

### For Docker on WSL2, you need:

- Virtual Machine Platform - Yes, required
- Hyper-V - Not required (but if enabled, it will work fine)
- Windows Hypervisor Platform - Not required

If you later want to create traditional Windows VMs or need full Hyper-V features, you can enable Hyper-V then. Only enable Windows Hypervisor Platform if you need to run other virtualization software alongside Docker.

To enable Virtual Machine Platform, open PowerShell as Administrator and run:

```powershell
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```
Then restart your computer. [source of info here](https://learn.microsoft.com/en-us/windows/wsl/install-manual#step-3---enable-virtual-machine-feature)

# 2025-09-01

[Go for Azure Key Vault](https://learn.microsoft.com/en-us/azure/key-vault/secrets/quick-create-go)

# 2025-08-30

- [Azure Latency](https://www.azurespeed.com/Azure/Latency)
- [AWS Latency](https://awsspeedtest.com/latency)
- [Swagger VS code extention](https://marketplace.visualstudio.com/items?itemName=42Crunch.vscode-openapi)
- [Online swagger editor](https://editor.swagger.io/)
