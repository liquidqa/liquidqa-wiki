# Description
# Linux VM installation
* Install VirtualBox
Based on your host OS, download the corresponding package
```
https://www.virtualbox.org/wiki/Downloads
```

* Download and install the latest Ubuntu LTS Desktop image (At the moment of writing this - Ubuntu 22.04.3 LTS
```
https://releases.ubuntu.com/jammy/ubuntu-22.04.3-desktop-amd64.iso
```
* Recommended (Minimum) System Configuration
```
 Hard disk: 40 GB 
 Virtual Disk type: Dynamically allocated storage
 CPU (Processors): 2 CPUs
 RAM: 4 GB
```

* Network configuration
```
Adapter 1 -> NAT
Adapter 2 -> Bridged Adapter
```
* Pulse Secure (VPN) may cause problems with some of the installations so you may need to turn it OFF.

# VM Configuration

## Packages
* Install core packages
```
sudo apt install -y git can-utils gcc git make net-tools openssh-server perl
```

* Install .NET SDK via official repository

Install the key
```
sudo wget -O - https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor | sudo tee /etc/apt/keyrings/microsoft.gpg
```
Add the Microsoft repository
```
sudo gedit /etc/apt/sources.list.d/microsoft.sources
```
Enter the following text, save the changes and exit Nano editor
```
Types: deb
URIs: https://packages.microsoft.com/ubuntu/22.04/prod/
Suites: jammy
Components: main
Architectures: amd64
Signed-By: /etc/apt/keyrings/microsoft.gpg
```
Install .NET SDK
```
sudo apt update
sudo apt install dotnet-sdk-8.0
```

Verify the installation
```
dotnet --version
```
**Note**: If the previous step fails with permission denied error, install an older version of the snap package:
```
$ sudo snap remove dotnet-sdk
$ sudo snap install dotnet-sdk --edge --classic
$ sudo snap alias dotnet-sdk.dotnet dotnet
```

* Install nvm
```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash
source ~/.bashrc
```

* Validate nvm is running
```
nvm list-remote
```

* Install node
```
nvm install v16.20.2
```

* Verify node and npm
```
node -v
npm -v
```
Versions should be:
Node: v16.20.2
NPM: 8.19.4


## Enable Virtual CAN
* Load the **vcan** module
```
sudo modprobe vcan
```

* Bring-up a CAN interface
```
sudo ip link add dev vcan0 type vcan
sudo ip link set up vcan0
```

* Verify the interface
```
sudo ifconfig vcan0
vcan0: flags=193<UP,RUNNING,NOARP>  mtu 72
        unspec 00-00-00-00-00-00-00-00-00-00-00-00-00-00-00-00  txqueuelen 1000  (UNSPEC)
        RX packets 129  bytes 651 (651.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 129  bytes 651 (651.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

```

* Enable auto-load
```
echo "vcan" | sudo tee -a /etc/modules-load.d/modules.conf
```
* Start and enable systemd-networkd
```
sudo systemctl start systemd-networkd
sudo systemctl enable systemd-networkd
```
* Create VCAN network interface
```
sudo nano /etc/systemd/network/vcan0.netdev
```

Enter the following text, save the changes and exit Nano editor
```
[NetDev]
Name=vcan0
Kind=vcan
MTUBytes=16
Description=Virtual CAN0 network interface
```
* Configure VCAN network interface
```
sudo nano /etc/systemd/network/80-vcan.network
```

Enter the following text, save the changes and exit Nano editor
```
[Match]
Name=vcan0
```
After reboot the interface should be functional and can be verified with
```
sudo ifconfig vcan0
```


##Install Visual Studio Code
Download [.deb package (64 bit)](https://go.microsoft.com/fwlink/?LinkID=760868) of Visual Studio Code

Install Visual Studio Code
```
sudo apt install ./<file>.deb
```
In Visual Studio Code, installing `C# Dev Kit` extension should enable both code completion for C# and C# debugging.

## Install postman [NOT REQUIRED]
```
sudo snap install postman
```
Find and start Postman from the Activities search.

## Configure shared folders
In the guest OS go to Devices -> Shared Folders -> Shared Folder Settings.
Select a folder path from your host machine.
Check Auto-mount and Make Permanent checkboxes.
Click on the Add new Shared folder and click OK.

* Make sure the current user is in the vboxsf group
```
sudo usermod -a -G vboxsf ${USER}
```
Reboot to apply the changes
```
reboot
```

## Bidirectional Copy/Paste (Host <=> Guest)
First in the VM Manager go to Settings and set the Shared Clipboard and Drag'n'Drop to Bidirectional
![bidirectional.PNG](/.attachments/bidirectional-6c7e4741-6613-4bd2-87d9-72ab568c0bfa.PNG)

Next in the guest OS, start a terminal and run the following commands:
```
sudo wget https://download.virtualbox.org/virtualbox/6.1.2/VBoxGuestAdditions_6.1.2.iso
sudo mkdir /media/iso
sudo mount VBoxGuestAdditions_6.1.2.iso /media/iso -o loop
sudo /media/iso/VBoxLinuxAdditions.run
reboot
```
You should be able to Copy/Paste from Host to Guest and Guest to Host now.

# Linux for beginners
## Helpful commands
* **pwd** - shows the directory you’re currently in
* **ls** - It presents to you the contents of a particular directory – both files and directories. You will use this command alongside pwd to navigate your ways inside the mighty Unix filesystem.
* **cd** - Change Directory, the cd command is behind your movement from one directory to another
* **mkdir** - It lets you create folders anywhere you like in your Linux system – given you have got the necessary permission
* **rmdir** - allows you to delete specific folders from your system 
* **df** - display essential information about the disk space on your filesystem
* **cat** - concatenating multiple files, the cat command is used for numerous other purposes since. This is among other Linux commands you will use to create new files, view file contents in the terminal, and redirect output to another command-line tool or file
* **rm** - remove (delete) files and directories in Linux.
* **cp** - copy a file or directory from one folder to another
* **wget** - download files from the web right from the terminal
* **echo** - output a specific text to the terminal console. 
* **sudo** - lets non-privileged users access and modify files that require low-level permissions
* **man** - stands for manual and is one of the most useful Linux commands you can get your hands on. This command, followed by the name of another command lists the manual or documentation page of that command.
