### Manual Installation Steps for Older Versions of WSL

#### Enable the Windows Subsystem for Linux
First, you need to enable the "Windows Subsystem for Linux" optional feature before installing any Linux distributions on Windows.

1. Open PowerShell as Administrator (Start menu > PowerShell > right-click > Run as Administrator).
2. Enter the following command:

    ```powershell
    dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
    ```

#### Enable the Virtual Machine Feature
Before installing WSL 2, you must enable the Virtual Machine Platform optional feature. Your machine will require virtualization capabilities to use this feature.

1. Open PowerShell as Administrator.
2. Run the following command:

    ```powershell
    dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
    ```

#### Download the Linux Kernel Update Package
The Linux kernel update package installs the most recent version of the WSL 2 Linux kernel for running WSL inside the Windows operating system image.

1. Download the package from the following link: [Linux kernel update package](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi).
2. Run the installer to update the kernel.

#### Set WSL 2 as the Default Version
To ensure that WSL 2 is used as the default version for new Linux distributions:

1. Open PowerShell as Administrator.
2. Run the following command:

    ```powershell
    wsl --set-default-version 2
    ```
