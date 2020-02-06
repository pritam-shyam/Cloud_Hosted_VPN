# Self-Hosted VPN with DNS Ad-Block
A custom server with VPN and ad-block capabilties that works on mobile, desktop, and routers. They server can be expanded for addtional use cases. This is a personal project for educational and learning purposes, use at **own risk**.


## Pre-requisites
* Linux Command Line
* Google Cloud Account
* Secure Shell Knowledge (SSH)
* Basic Understanding about Virtual Private Network (VPN)
* General Knowledge on Domain Name System (DNS), IPTables, and Networking


## Setup
### Google Compute Engine VM
Once you have a Google Cloud account and logged in, follow these steps:
* Click **Compute Engine** -> **VM Instances** -> **Create Project**
  * Project can be any name, then **Enable Billing**
* Click **Compute Engine** -> **VM Instances** -> **Create**
  * **Name**: `pi-hole`
  * **Region** and **Zone**: If not auto, choose closet to your physical location
  * **Machine Type**: `micro`
  * **Boot Disk Image**: `Debian 10`
  * Expand **Management, Security, Disks, Networking, Sole Tenancy**
    * Click **Network** -> **Network Interfaces**
    * Choose **Create IP Address** and **Reserve a New Static IP**
* Click **Create** to make a VM instance with the above configuration

We need a custom Firewall Rule for WireGuard VPN to communicate external to the VM
* Click **VPC Network** -> **Firewall Rules** -> **Create Firewall Rule**
  * Name is `allow-wireguard` and change the **Target** to **All instances in the network**
  * The **Source IP Ranges** is `0.0.0.0/0`
  * Select **UDP** and change to `58210`


### Pi-Hole
* Follow the below steps to install Pi-Hole
  * Login into the VM via SSH through the web portal or on your computer
  * Enable root: `sudo su`
  * Update the VM: `apt-get update && apt-get upgrade -y`
  * Install Pi-Hole: `curl -sSL https://install.pi-hole.net | bash`
    * Select **OK** until upstream DNS provider, choose **CloudFlare**
    * In **Select Protocols**, deselect **IPv6**


### WireGuard VPN
* Follow the guide in the below link, it installs WireGuard with a dashboard which makes it simple to install, manage, and add clients
  * [WG-Dashboard](https://github.com/wg-dashboard/wg-dashboard)
  * After install, Login into WebUI
    * Turn off **Enable DNS over TLS**
    * Set DNS to the IP Address of the Pi-Hole
* WireGuard App can be downloaded for the following systems (needed to connect to VPN Server on Google Cloud):
  * Windows
  * macOS
  * Android
  * iOS


## Resources
* [Google Cloud Free Tier](https://cloud.google.com/free/)
* [Pi-Hole](https://pi-hole.net/)
* [WireGuard](https://www.wireguard.com/)
