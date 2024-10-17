
# PXE Network Boot with Multiple OS Options

**Description**  
This project sets up a PXE boot environment where a machine without an OS can boot from the network and choose between multiple operating systems. Once the machine is shut down, the OS disappears, leaving no traces.

## Features
- **Boot via Network (PXE)**
- **Multiple OS Choices** (Linux, Debian, Ubuntu, Kali, Windows 10, Windows 11, Windows Server 2019)
- **Temporary OS**: The OS runs entirely in RAM and is deleted upon shutdown.
- **Easy Configuration**: Customizable OS options via a simple menu.

## Project Structure
```bash
├── README.md           # Documentation
├── docs/               # Additional documentation and images
├── pxelinux.cfg/       # PXE boot configuration files
├── os_images/          # Folder containing bootable OS images
└── LICENSE             # License information
```

## Requirements
To set up and use this project, you will need:
- A server with TFTP and DHCP configured (Linux recommended)
- PXE-capable client machines
- OS images for Linux, Windows, and others

## Installation

### Step 1: Set up the PXE server
1. Install `dnsmasq` or `isc-dhcp-server` for DHCP and TFTP.
2. Configure the PXE boot settings by editing `/etc/dnsmasq.conf` (example for `dnsmasq`):
   ```ini
   # Sample dnsmasq.conf for PXE
   interface=eth0
   dhcp-range=192.168.1.50,192.168.1.150,12h
   enable-tftp
   tftp-root=/srv/tftp
   dhcp-boot=pxelinux.0
   ```

### Step 2: Add the OS images
1. Download or prepare OS images (Ubuntu, Debian, Kali, Windows, etc.).
2. Place them in the `os_images/` folder on your server.
3. Modify the PXE configuration to include the OS options:
   ```bash
   # Sample PXE menu
   LABEL ubuntu
       MENU LABEL Boot Ubuntu 20.04
       KERNEL /os_images/ubuntu/vmlinuz
       INITRD /os_images/ubuntu/initrd.img
       APPEND boot=live

   LABEL debian
       MENU LABEL Boot Debian 10
       KERNEL /os_images/debian/vmlinuz
       INITRD /os_images/debian/initrd.img
       APPEND boot=live

   LABEL kali
       MENU LABEL Boot Kali Linux
       KERNEL /os_images/kali/vmlinuz
       INITRD /os_images/kali/initrd.img
       APPEND boot=live

   LABEL windows10
       MENU LABEL Boot Windows 10 PE
       KERNEL /os_images/winpe/wimboot
       INITRD /os_images/winpe/bootmgr.wim
   ```

### Step 3: Boot the client machine
1. Start a machine without an OS.
2. Ensure it is set to boot from the network (PXE boot).
3. Choose the OS from the network boot menu and start using it!

## Usage
- Once the machine is booted into the selected OS, you can use it normally.
- The OS will run in memory, and all data will be lost when the machine is shut down.

## Contributing
Contributions are welcome! Please submit a pull request or open an issue to discuss potential changes.

## License
This project is licensed under the MIT License - see the `LICENSE` file for details.
