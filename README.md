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

## Check the Cuda Support for tensorflow and torch
Check the cuda, cudnn and python environment supported by tensorflow.
[https://www.tensorflow.org/install/source#gpu](https://www.tensorflow.org/install/source#gpu)

Check the cuda, cudnn and python environment supported by torch.
[https://pytorch.org/get-started/locally/](https://pytorch.org/get-started/locally/)

**In this i am install for tensorflow.**

## Install some essential Package

This help to execute C and C++ code for testing purpose.
```bash
sudo apt install build-essential
``` 

We are installing miniconda because this help to make a specific python environment.
```bash
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
```
To check if miniconda is installed or not
```bash
bash ./Miniconda3-latest-Linux-x86_64.sh
```
use **Ctrl + C** to exit.

```bash
sudo apt install build-essential
```

## Download Cuda
Check the suitable download version from [link](https://www.tensorflow.org/install/source#gpu)

1. Search Cuda <version> download.
2. Visit Nvidia developer page.
3. Register/Login if needed.
4. Select **Linux -> x86-64 -> WSl-Ubuntu -> 2.0 -> runfile(local)**
4. Execute the given code in nvidia developer page to download the cuda. e.g. [wget https://developer.download.nvidia.com/compute/cuda/12.5.0/local_installers/cuda_12.5.0_555.42.02_linux.run]()
5. Execute the given code in nvidia developer page to install cuda. e.g. [sudo sh cuda_12.5.0_555.42.02_linux.run]()
7. **accect** the policy
8. Go down and mark cuda toolkit, Cuda demo suite, cuda documentation is selected and click on install.

## Add cuda to path in bashrc
```bash
nano ~/.bashrc
```

Change the version which was already downloaded.

Paste the code at the bottom of the **bashrc** file and save it **Ctrl + O -> Enter -> Ctrl + X**.
```
export PATH=/usr/local/cuda-12.5/bin${PATH:+:${PATH}}
export LD_LIBRARY_PATH=/usr/local/cuda-12.5/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}
```
```bash
source ~/.bashrc
```

put this on this file **/usr/local/cuda-12.5/lib64** then **Ctrl + O -> Enter -> Ctrl + X**
```bash
sudo nano /etc/ld.so.conf
```

If no error then good to go
```bash
sudo ldconfig
```

## Verify that Cuda i properly installed or not.

```bash
echo $PATH
echo $LD_LIBRARY_PATH
sudo ldconfig -p | grep cuda
```

Check Cuda version
```bash
nvcc --version


nvcc: NVIDIA (R) Cuda compiler driver
Copyright (c) 2005-2025 NVIDIA Corporation
Built on Tue_Jul_11_00:00:00_PDT_2025
Cuda compilation tools, release 12.5, V12.5.0
Build cuda_12.5.r12.5/compiler.12345678_0
```
