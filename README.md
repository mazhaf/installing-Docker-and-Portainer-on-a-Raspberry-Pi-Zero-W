# 🐳 Docker + Portainer on Raspberry Pi Zero W

This repository provides step-by-step instructions to install **Docker** and run **Portainer** on a Raspberry Pi Zero W (ARMv6 architecture).

---

## 📋 Requirements

- Raspberry Pi Zero W
- Raspberry Pi OS (Lite or Full)
- Internet connection
- SSH access or local terminal
- Minimum 8GB SD card

---

## 🚀 Installation Steps

### 1. Update and Upgrade System

```bash
sudo apt update && sudo apt upgrade -y

```

---
### 2. Install Docker (ARMv6 compatible)
```bash

curl -sSL https://get.docker.com | sh
```
After install, add your user to the Docker group:

```bash
sudo usermod -aG docker $USER
```

### 3. Install Portainer

Pull the correct Portainer image 
```bash
sudo docker pull portainer/portainer-ce:latest
```
Then run it:
```bash
sudo docker run -d -p 9000:9000 --name=portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:latest
```
### 4. Access Portainer UI

From your browser on the same network, go to:

```bash
http://raspberrypi.local:9000
```
Or use your Pi's IP address:
```bash
http://<your-raspberrypi-ip>:9000
```
or use username and pi name
```bash
http://<your-raspberrypi-user>@<your-raspberrypi-name>.local:9000
```
