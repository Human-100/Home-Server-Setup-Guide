Sure, here's the same `README.md` with **all emojis removed** and clean formatting, ready for GitHub:

---

````markdown
# Home Server Setup Guide

Turn an old laptop or PC into a powerful home server. This guide will walk you through a basic setup, from installation to secure remote access.

---

## What You'll Get

- Personal cloud with unlimited storage
- Access your server securely from anywhere
- Host self-managed apps like media servers, file browsers, backups
- Extend to control your entire home network

---

## What You’ll Need

- An old laptop or PC (even with a broken screen)
- A USB drive (8GB+)
- Basic command line knowledge
- Internet connection

---

## Step 1: Install a Lightweight Linux Server

### 1.1 Download Ubuntu Server (or similar)

Download ISO: https://ubuntu.com/download/server

You can also use Debian, Arch, or any distro you prefer

### 1.2 Flash to USB

Use [Rufus](https://rufus.ie) (Windows) or `balenaEtcher` (macOS/Linux) to flash the ISO to your USB drive.

### 1.3 Boot and Install

Boot the old laptop from USB, and follow the instructions to install Ubuntu Server (no GUI).

Choose minimal installation. When asked:

- Set a hostname (e.g., `homeserver`)
- Create a user
- Install OpenSSH Server when prompted (for remote terminal access)

---

## Step 2: Install CasaOS

### 2.1 Log in via Terminal or SSH

```bash
ssh youruser@yourserverip
````

### 2.2 Install CasaOS

```bash
curl -fsSL https://get.casaos.io | bash
```

This will install CasaOS and run it on port 80. Access it via:
`http://your-server-ip` in any browser

---

## Step 3: Install and Configure Tailscale

Tailscale gives you secure remote access to your server and network.

### 3.1 Install Tailscale

```bash
curl -fsSL https://tailscale.com/install.sh | sh
```

### 3.2 Authenticate Your Device

```bash
sudo tailscale up
```

This will output a URL. Open it in your browser to log in and link the server to your Tailscale account.

### 3.3 Enable at Startup

```bash
sudo systemctl enable tailscaled
```

---

## Step 4: Access CasaOS Remotely

Once Tailscale is set up, you can access CasaOS from anywhere using the Tailscale-assigned IP:

```
http://100.x.x.x (or your tailnet hostname)
```

Make sure you set a strong login password inside the CasaOS web UI.

---

## Step 5: Enable Access to Entire Home Network

To allow your home server to route traffic to your full network:

### 5.1 Enable IP Forwarding

```bash
sudo nano /etc/sysctl.conf
```

Uncomment or add:

```
net.ipv4.ip_forward=1
```

Then apply:

```bash
sudo sysctl -p
```

### 5.2 Enable Subnet Routing in Tailscale

```bash
sudo tailscale up --advertise-routes=192.168.1.0/24
```

Replace `192.168.1.0/24` with your actual LAN subnet.

In the Tailscale admin panel, approve the route.

Now, any authenticated device can reach your home network securely, including IP cameras, NAS drives, smart devices, and more.

---

## Optional: Useful CasaOS Apps

Inside the CasaOS UI, you can easily install:

* Jellyfin – media server for movies, shows, music
* Filebrowser – drag-and-drop file manager
* Nextcloud – personal cloud storage
* Transmission – torrent client
* Home Assistant – smart home automation

---

## Tips

* Use `htop`, `df -h`, and `uptime` to monitor system performance
* Add more storage by mounting external drives via `/etc/fstab`
* Always keep your system updated:

```bash
sudo apt update && sudo apt upgrade
```

---

## Example: IP Webcams From Old Phones

Repurpose old phones using apps like:

* IP Webcam (Android)
* AlfredCamera

You can now access these streams via Tailscale from anywhere.

---

## You're Done

You now have your own self-hosted home server, accessible securely from anywhere, scalable with unlimited storage, and free of monthly cloud fees.

---
