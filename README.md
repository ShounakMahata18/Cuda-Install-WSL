# Install CUDA in WSL (Windows Subsystem for Linux)

Steps wise guide to install cuda in wsl ubuntu24 for tenserflow and torch.

## Enable Windows subsystem for linux.

- Search 'Turn windows features on or off'.
- Enable Windows subsystem for linux from the environment.


## Download Windows subsystem for linux from microsoft store.

Use the download link [https://apps.microsoft.com/detail/9P9TQF7MRM4R](https://apps.microsoft.com/detail/9P9TQF7MRM4R).\

## Open Terminal

Open powershell as run as administrator.

Run this code to download wsl ubuntu default latest version.
```bash
wsl --install
```

To download ubuntu specific version like ubuntu-24.04
```bash
wsl --install -d ubuntu-24.04
```

## To Check WSL has any dextro or not use
```bash
wsl -l -v
```

## Go to WSL
```bash
wsl Ubuntu
```

Update the installed file
```bash
sudo apt update && sudo apt upgrade -y
```
Exit from that WSL
```bash
exit
```

## To Ubuntu Version
Use this code inside WSL
```bash
lsb_release -a
```
Output
```bash
No LSB modules are available.
Distributor ID: Ubuntu
Description:    Ubuntu 22.04.3 LTS
Release:        22.04
Codename:       jammy
```
## If you want to change the WSL saved files
Migrate from C:/ drive to D:/ drive use the following code.

First check the installed dextro 
- 🔴**wsl -l**.
- 🔴**wsl --list --verbose**
- 🔴**After checking give <DistroName> as Ubuntu-24.04 or Ubuntu as given**

Create a tar file which contain the ubuntu environment.
```bash
wsl --export <DistroName> D:\ubuntu.tar
```

```bash
wsl --unregister <DistroName>
```

Create <NewDistroName> as **Ubuntu**
```bash
wsl --import <NewDistroName> D:\WSL\Ubuntu D:\ubuntu.tar
```

```bash
wsl --set-default <NewDistroName>
```

Remove the existing tar file(optional)
```bash
rm -v D:\ubuntu.tar
```
