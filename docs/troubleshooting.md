
# Troubleshooting Guide

If you're experiencing issues with your PXE Network Boot setup, this guide can help you resolve the most common problems.

## 1. PXE Boot Fails or Times Out
- **Check TFTP and DHCP Server**: Ensure the TFTP and DHCP servers are running.
- **Network Configuration**: Make sure the PXE client and server are on the same network segment.

## 2. Client Does Not Receive an IP Address
- **DHCP Configuration**: Double-check the `dhcp-range` setting in the `dnsmasq.conf` file.
- **Firewall**: Ensure that no firewall is blocking DHCP traffic.

## 3. Operating System Image Fails to Load
- **File Path**: Verify that the file paths in the `pxelinux.cfg/default` file are correct.
- **Permissions**: Make sure the OS image files have the correct read permissions.

## 4. No PXE Boot Menu Appears
- **Check PXE Configuration**: Make sure the `pxelinux.cfg/default` file is correctly configured.
- **TFTP Root Directory**: Verify that the TFTP root directory is set correctly.

If these steps don't resolve your issue, consult the logs for additional details.
