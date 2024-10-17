
# Detailed Installation Guide

This guide provides detailed instructions to set up and configure the PXE Network Boot with multiple OS options. Follow these steps to ensure everything is correctly configured.

## 1. Set up the PXE Server
You need a server that will act as a PXE server. The server must have DHCP and TFTP services enabled.

### Step 1: Install Required Packages
For most Linux distributions, you can use the following commands to install the necessary packages:

```bash
sudo apt-get update
sudo apt-get install dnsmasq tftp-hpa
```

### Step 2: Configure the DHCP Server
Edit the `/etc/dnsmasq.conf` file to configure DHCP and TFTP settings. Here's an example configuration:

```ini
interface=eth0
dhcp-range=192.168.1.50,192.168.1.150,12h
enable-tftp
tftp-root=/srv/tftp
dhcp-boot=pxelinux.0
```

### Step 3: Configure PXE Boot Menu
Edit the PXE boot menu file (`pxelinux.cfg/default`) to include your operating system options. For example:

```bash
LABEL ubuntu
    MENU LABEL Boot Ubuntu 20.04
    KERNEL /os_images/ubuntu/vmlinuz
    INITRD /os_images/ubuntu/initrd.img
    APPEND boot=live
```

## 2. Add Operating System Images
Once your PXE server is set up, you need to add the images of the operating systems. Download or prepare the OS images (Ubuntu, Debian, Windows, etc.) and place them in the `os_images/` directory.

## 3. Boot the Client
Now, set the client machine to boot from the network. Once booted, you will be presented with the PXE menu to choose the OS.

