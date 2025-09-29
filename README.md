# ec2-apache-webserver-
Hands-on: AWS EC2 — Hosting an Apache Web Server.
# Hands-on: AWS EC2 — Hosting an Apache Web Server

I recently launched an Apache Web Server by creating and configuring an EC2 instance on AWS. This project demonstrates:
- Launching and connecting to an EC2 instance
- Installing & configuring Apache
- Hosting a simple web page accessible over the internet

> This repo contains the scripts, architecture diagram and screenshots used during the lab.

## Architecture
![Architecture diagram](docs/architecture.png)

**High-level flow**: User (browser) → EC2 instance (Apache) → (optionally) External resources.

## Quick demo screenshots
![EC2 Connect / Terminal](docs/screenshot-ec2-connect.png)
*SSH session / user-data output*

![App in Browser](docs/screenshot-app-ui.png)
*Apache default/sample page served from EC2*

## How I launched the EC2 instance (summary)
1. Launch EC2 (Amazon Linux 2) — choose an appropriate instance type (t2.micro for free tier).  
2. Attach a Security Group: allow **HTTP (80)** and **SSH (22)** from your IP (or 0.0.0.0/0 for HTTP only).  
3. Use `scripts/ec2-user-data.sh` as *user-data* during launch (or run it manually after SSH).  
4. SSH to instance:
```bash
ssh -i /path/to/key.pem ec2-user@<EC2_PUBLIC_IP>
# then check Apache
sudo systemctl status httpd
curl http://localhost

