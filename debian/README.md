# Home Assistant Step By Step Easy Install on Debian Server + Ansible Playbooks

[![License: Apache](https://img.shields.io/badge/License-Apache%202-yellow.svg)](hhttps://opensource.org/licenses/Apache-2.0)

:warning: Using Debian 11 and following a strict set of guidelines available [HERE](https://github.com/home-assistant/architecture/blob/6da4482d171f2ef04de9320d313526653b5818b4/adr/0014-home-assistant-supervised.md) will give you an officially supported installation of Home Assistant Supervised. If you choose at anytime to install additional software to the Debian operating system, your installation may become officially unsupported.

:warning: If you do not understand what this means, or that making almost any changes to the underlying OS may render your install Unsupported/Unhealthy, this installation method is not for you and you should install HA OS. If you do not require the supervisor, then installing [HA Container](https://www.home-assistant.io/installation/generic-x86-64#install-home-assistant-container) may be a better option and will allow you full control over the OS to install additional software and Docker containers.

If you are new to Home Assistant, you can now proceed to Section 1 if you need assistance with installing Debian 11. If you already have Debian 11 installed and wish to move on to installing Home Assistant, move on to Section 2.

This guide will help you to install Home Assistant Supervised, on almost any machine type you choose. This guide has been tested on machines including a MacBookPRO M1 2022, Dell Optiplex 7000, and a BeeLink 12 sei12 i7 thin client.



## Section 1 – Install Debian Server
If you would like a step by step guide on how to install Debian 11 to your machine, click here to expand for instructions.

1.1) Start by downloading `debian-live-11.6.0-amd64-standard.iso` from [HERE](https://cdimage.debian.org/debian-cd/current-live/amd64/iso-hybrid/debian-live-11.6.0-amd64-standard.iso). If you would prefer the full Debain image with all drivers, download `firmware-11.6.0-amd64-DVD-1.iso` [HERE](https://cdimage.debian.org/cdimage/unofficial/non-free/cd-including-firmware/11.6.0+nonfree/amd64/iso-dvd/firmware-11.6.0-amd64-DVD-1.iso)

1.2) While Debian is downloading, you will need some other programs to help with the setup and installation. To burn the Debian ISO image to a USB thumb drive, you will use a program called Disk Utils(MAC).

1.3)
1.3.1) Use diskutil list to list available volumes and choose USB device
![image01](../images/image01.png)
1.3.2) Finding usb location using diskutil list, it was **/dev/disk2**
1.3.3) Erase USB drive for FAT32(MS-DOS FAT) + Master Boot Record Schema
![image01](../images/image02.png)
![image01](../images/image03.png)
1.3.4) Unmounting the usb: `sudo diskutil unmountDisk /dev/disk2`
![image01](../images/image04.png)
1.3.5) dding the image: `sudo dd if=firmware-11.6.0-amd64-DVD-1.iso of=/dev/disk2 bs=1`

Wait several hours, and then you can see the follow message in your terminal:
![image01](../images/image05.png)

1.4) After VM boot and Debian installation, the first screen you should be able to select from is Main Menu, on this screen, select **Installer**
![image01](../images/image06.png)

1.5) Next will be **Language**. Choose your language and click continue(English recommended).
![image01](../images/image07.png)
1.6) Next will be **Select your location**. Choose your country and click continue.
![image01](../images/image08.png)
1.7) Next will be **Configure the keyboard**. Select your keyboard type and click continue. The installer will now perform some automated tasks which will take 1-2 minutes.

1.8) Next will be **Configure the network**. Here you can name your machine, the default name will be debian. Choose a name and click continue. You can skip the next page by clicking continue as you do not need to set a domain name.
![image01](../images/image09.png)
1.9) Next will be **Set up users and passwords**. You will be asked to create a password for the root user. Make a note of the password you choose here, and click continue.
(For now I sigest you leave root user setup. The root account will be disabled and the system initial user  account will be given power to root using **sudo** command)
![image01](../images/image10.png)
1.10) Next will be **Set up users and passwords** again. Enter a username, click continue and on the next screen, enter a password for this user account. Make note of both of these, you will need them later.
![image01](../images/image11.png)
![image01](../images/image12.png)
![image01](../images/image13.png)
1.11) Next will be **Configure the clock**. Select the correct time zone and click continue.
![image01](../images/image14.png)
1.12) Next will be **Partition Disks**. Select **Guided - use entire disk** and then click continue. On the next screen make sure the correct disk is selected and click continue. On the next screen select **All files in one partition** and click continue. On the next screen, make sure **Finish partitioning and write changes to disk** is selected, and click continue. On the next screen, select **Yes** and then click continue. The installer will now perform some automated tasks. This will take 1-2 mins.
![image01](../images/image15.png)
![image01](../images/image16.png)
![image01](../images/image17.png)
![image01](../images/image18.png)
![image01](../images/image19.png)
1.13) Next will be **Configure the package manager**. Select **Yes** and click continue. Select your Country and click continue. You can leave the default selection (deb.debian.org](deb.debian.org) selected, or select another mirror of your choosing, and click continue. Leave the next page(proxy) blank and click continue. The installer will now perform some automated tasks. This will take a few minutes.
![image01](../images/image20.png)
![image01](../images/image21.png)
![image01](../images/image22.png)
![image01](../images/image23.png)
1.14) Select **NO** to Configuring popularity -context and continue.
![image01](../images/image24.png)
1.15) Next will be **Software Selection** . Make clear under  all non SSH options and select only one **SSH Server**. Press **Enter** to continue.
![image01](../images/image25.png)
1.15) Next will be Install the **GRUB bootloader**. Select **Yes** and click continue. Now select the drive you are installing Debian on, and click continue. The installer will now perform some automated tasks. This will take 1-2 mins and then installation will be complete.
![image01](../images/image26.png)
![image01](../images/image27.png)
![image01](../images/image28.png)
1.16) You can use your configured login and password to make a first login screen and you can use **sudo su** to access root user.
![image01](../images/image29.png)
![image01](../images/image30.png)
![image01](../images/image31.png)
1.17) Once this has completed, you will need to find the IP address of the machine. You can do this by checking your router, or by typing this command into the terminal.
```terminal
ip a
```
alternatives:
```terminal
hnostname -I
```
![image01](../images/image32.png)
![image01](../images/image33.png)
You should now see some information on your screen showing network configuration. You are looking for information like inet `192.168.1.150/24`, or `192.168.18.33/24`, or, inet `10.1.1.50/24` depending on your network setup. This is the IP of the machine and you can now use this to connect to the machine from another PC using a program lite **Putty** or **Remote Desktop**. Information on how to do this is at Step 3.3 below.

1.18) To remote connections you can use the follow command(using the previous IP):
```terminal
ssh rafael@192.168.18.33
```
![image01](../images/image34.png)


## Section 2 - Install OS Agent, Docker and Dependencies

You will now install the OS Agent for Home Assistant. It is used for Home Assistant OS and Home Assistant Supervised installation types and it allows the Home Assistant Supervisor to communicate with the host operating system.

2.1) Install dependencies
```terminal
sudo apt-get -y update && sudo apt-get -y install curl wget build-essential libncursesw5-dev libssl-dev libsqlite3-dev tk-dev libgdbm-dev libc6-dev libbz2-dev libffi-dev zlib1g-dev && \
sudo apt-get -yinstall lsb-release && \
wget https://www.python.org/ftp/python/3.11.1/Python-3.11.1.tgz && \
tar -xvf Python-3.11.1.tgz && \
cd Python3.11.1 && \
sudo ./configure --enable-optimizations && \
sudo make -j 2 && \
nproc && \
sudo make altinstall && \
python3.11 --version && \
echo 'alias python=/usr/local/bin/python3.11' >> ~/.bashrc && \
echo 'alias python3=/usr/local/bin/python3.11' >> ~/.bashrc && \
echo 'alias pip="python3.11 -m pip"' >> ~/.bashrc && \
source ~/.bashrc 
```

2.2) In terminal (or connected to your machine via SSH using Putty or Remote Desktop - see Step 3.3 for info), run the following commands to update the Debian OS, install Docker and the required dependencies for the OS Agent and the Supervised installer. Execute the following commands one at a time.

```terminal
sudo -i
apt update && sudo apt upgrade -y && sudo apt autoremove -y
apt --fix-broken install
apt-get install jq wget curl udisks2 libglib2.0-bin network-manager dbus systemd-journal-remote -y
curl -fsSL get.docker.com | sh
```
2.3) Visit the OS Agent page and then replace the version number with the latest available, into the commands below. (i.e. replace all references to 1.3.0 with the latest available)
Execute the following commands one at a time.

```terminal
wget https://github.com/home-assistant/os-agent/releases/download/1.4.1/os-agent_1.4.1_linux_x86_64.deb
dpkg -i os-agent_1.4.1_linux_x86_64.deb
```

## Section 3 – Install Home Assistant Supervised

With the OS Agent and dependencies installed, you can move on to installing **Home Assistant Supervised**.

3.1) Enter each line of the below commands into the terminal and execute them one at a time.
If you have rebooted since section 2, make sure you are running as root before executing the below commands.

```terminal
sudo -i
```
Execute the following commands one at a time. (1.4.1 latest)
```terminal
wget https://github.com/home-assistant/supervised-installer/releases/latest/download/homeassistant-supervised.deb
dpkg -i homeassistant-supervised.deb
```
3.2) You may be prompted to choose a machine type during the installation process, if so, choose **generic-x86-64**.
The installation time is generally under 5 mins, however it can take longer so be patient. You can check the progress of Home Assistant setup by connecting to the IP address of your machine in Chrome/Firefox on port 8123. (e.g. http://192.168.18.33:8123)
![image01](../images/image35.png)
Once you can see the login screen, the setup has been completed and you can set up an account name and password. If you are new to Home Assistant you can now configure any smart devices that Home Assistant has automatically discovered on your network. If you have an existing Home Assistant install and you have a snapshot or YAML files you wish to restore, refer to the document Backing up and Restoring your configuration.
You have completed the installation of Home Assistant Supervised on your Debian machine. It is recommended that you log into your machine at least once a month and use the following command to download security patches and keep the OS up to date. You can do this directly on the machine itself via the terminal.

```terminal
sudo apt update && sudo apt upgrade -y && sudo apt autoremove -y
```
Reboot your Operation System and then you can access your HA again , from your browser(Ex: Chrome)
![image01](../images/image36.png)
![image01](../images/image37.png)

3.3) If you wish to install Open-SSH so you can remotely connect to your Home Assistant machine from another PC.
:warning: If you install Open-SSH you will not be adhering to the guidelines of [ADR-0014](https://github.com/home-assistant/architecture/blob/master/adr/0014-home-assistant-supervised.md) and therefore will not have an officially supported installation, however, installing Open-SSH will not break your machine. Run the following from console.
```terminal
sudo apt install openssh-server -y
```
If you do choose to install and use Open-SSH, you can then use software called **PuTTY**.
Or you can use your terminal to remote (using the previous IP):
```terminal
ssh rafael@192.168.18.33
```
![image01](../images/image34.png)

## Section 4 – Install Home Assistant Integrations

4.1) Go to Settings > Devices & Services >
