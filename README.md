# 🚀 Automated Deployment Bash Script

This project automates the setup and deployment of a Dockerized application on a remote Linux server using a single Bash script.

The goal is to simulate a real-world DevOps workflow — fully automated, repeatable, and production-ready.

---

## 🧠 Overview

The `deploy.sh` script performs a complete deployment from GitHub to a remote host.  
It handles everything from cloning the repository to setting up Docker, Docker Compose, and Nginx, then running the application in a container and verifying it’s live.

---

## ⚙️ Features

- Prompts for all required parameters (repo URL, server IP, SSH key, etc.)
- Authenticates and clones private repos using a Personal Access Token (PAT)
- SSHs into the remote server securely
- Installs **Docker**, **Docker Compose**, and **Nginx**
- Deploys the Docker container automatically
- Configures **Nginx** as a reverse proxy
- Validates deployment with `curl`
- Logs every step with timestamps and exit codes
- Idempotent (safe to re-run)

---

## 🧩 Requirements

- Linux or macOS terminal
- Bash (v4 or higher)
- Docker & Docker Compose
- SSH access to a remote Linux server
- GitHub Personal Access Token (PAT) with repo access

---

## 🧭 Usage Instructions

1. **Clone this repository:**
   ```bash
   git [clone https://github.com/0dow0ri7s3/hng13-stage1-devops.git]
   cd deploy-script

Make the script executable:

chmod +x deploy.sh


Run the script:

./deploy.sh

Provide inputs when prompted:

GitHub Repository URL

Personal Access Token (PAT)

Branch name (optional, defaults to main)

SSH Username, Server IP, and SSH key path

Container port (the internal app port)

Wait for deployment to complete.
The script will:

SSH into your server

Install all dependencies

Build and run your Docker container

Configure Nginx

Validate everything automatically

🧱 File Structure
├── deploy.sh           # Main deployment script
├── README.md           # Documentation
└── deploy_logs/        # (optional) Folder for generated logs

🩺 Logs & Error Handling

Every action is logged into deploy_<date>.log

Errors trigger graceful exits with meaningful messages

Failed commands are trapped and logged automatically

Supports re-runs without breaking existing setups

🛠️ Troubleshooting
Issue	Possible Fix
Permission denied on script	Run chmod +x deploy.sh
Docker not found	Script installs Docker automatically, but check with docker --version
SSH failed	Verify correct IP and private key path
Port not reachable	Ensure your server security group or firewall allows it
👤 Author

Odoworitse Afari
DevOps Engineer | Infrastructure Automation | Cloud & CI/CD

🏁 Notes

Do not use Ansible, Terraform, or other config management tools.

This project focuses on shell scripting, automation logic, and deployment reproducibility.

The script simulates a real-world DevOps deployment pipeline from local to remote.
