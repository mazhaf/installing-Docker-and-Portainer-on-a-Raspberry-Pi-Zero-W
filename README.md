# 🐳 # Installing Docker, Portainer & n8n on Raspberry Pi Zero W

This repository provides step-by-step instructions and configuration files to install **Docker**, **Portainer**, and **n8n** automation tool on a **Raspberry Pi Zero W**.

---

You will learn how to:
- Update and upgrade the Raspberry Pi OS  
- Install Docker and manage it 
- Install Portainer for container management via a web UI  
- Deploy and run n8n as a Docker stack using Portainer  
- Access and start using n8n for workflow automation  

---

## Prerequisites

- Raspberry Pi Zero W with Raspberry Pi OS (Lite preferred)  
- Network connectivity (Wi-Fi or Ethernet via USB adapter)  
- Basic Linux command line knowledge

---

## Step 1: Update & Upgrade System

Run the following command to ensure your system packages are current:

```bash
sudo apt update && sudo apt upgrade -y

```

---
## Step 2: Install Docker

Install Docker using the official convenience script:

```bash

curl -sSL https://get.docker.com | sh
```
After install, add your current user to the docker group so you can run Docker commands without sudo:

```bash
sudo usermod -aG docker $USER
```
---

## Step 3: Install Portainer

Pull the correct Portainer image 

```bash
sudo docker pull portainer/portainer-ce:latest
```
Then run the Portainer container:

```bash
sudo docker run -d -p 9000:9000 --name=portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:latest
```

Open your browser and access Portainer UI at:

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
---

## Step 4: Deploy n8n with Portainer

1. Log in to Portainer.
2. Go to Environments → select your local Docker.
3. Navigate to Stacks → Add stack.
4. Name the stack n8n.
5. Paste the following YAML into the Web editor:

```bash
version: Latest
services:
  n8n:
    image: docker.n8n.io/n8nio/n8n:latest
    ports:
      - "5678:5678"
    environment:
      - GENERIC_TIMEZONE=Asia/Riyadh
      - TZ=Asia/Riyadh
      - N8N_SECURE_COOKIE=false
```
You can change timezone variables.

6. Click Deploy the stack.

---

## Step 5: Access n8n

Open the following URL in your browser:
```bash
http://<your-pi-hostname>.local:5678
```
Replace <your-pi-hostname> with your Raspberry Pi's hostname.

---

## Additional Notes

- The n8n_data volume ensures your workflow data persists across container restarts.
- Change timezone values in the stack file if you’re outside Asia/Riyadh timezone.
- Raspberry Pi Zero W has limited resources — running multiple containers may affect performance.

---

## Troubleshooting

- If Docker commands fail without sudo, ensure you logged out and back in (or rebooted) after adding your user to the Docker group.
- Use docker logs <container_name> to check container logs if something doesn’t start correctly.
- Ensure ports 9000 (Portainer) and 5678 (n8n) are not blocked by firewalls.

## License
This repository is open-source under the MIT License.

