# DevOps Automated Deployment Script (deploy.sh) ## Overview This Bash script automates the full deployment pipeline for containerized applications using **Docker** and **Nginx** on a remote Linux server. It performs repository cloning, container building, and reverse proxy configuration — minimizing manual steps during setup and deployment. --- ## Features - Securely connects to remote EC2 or VPS via SSH. - Clones and updates the specified Git repository. - Builds Docker images or runs Docker Compose projects. - Automatically configures **Nginx** as a reverse proxy for the containerized app. - Provides logging, health checks, and cleanup support. - Ensures idempotent deployment (can be safely re-run). --- ## Prerequisites Before running this script, ensure: - You have **Docker**, **Nginx**, and **Git** installed on the remote server (the script will install if missing). - You have a valid **SSH key** for access to the target server. - Your GitHub **Personal Access Token (PAT)** has permission to access the repository. - The application has a valid **Dockerfile** or **docker-compose.yml** in its root directory. --- ## Parameters Collected During Execution The script will prompt you to input the following: | Parameter | Description | |------------|--------------| | **Git Repository URL** | HTTPS link to the source repository. | | **Personal Access Token (PAT)** | For authentication to private repos. | | **Branch Name** | Defaults to main if left blank. | | **Remote Server UsernServer IP Addressthe target EC2 or remote host. | | **ServerSSH Key PathPublic or private IP of the server. | | **SSH Key Path*Application Portvate key (e.g., ~/.ssh/id_rsa). | | **Application Port** | Internal container port your app listens on (e.g., 8081). | --- ## How It Works ### Step 1 — Clone or Update Repository Checks if the repository exists locally; if not, clones it from the provided URL and branch using your PAT. ### Step 2 — Docker Verification Validates the presence of a Dockerfile or docker-compose.yml. If missing, the script exits with an error. ### Step 3 — Remote Setup Over SSH, the script: - Updates system packages. - Installs Docker, Docker Compose, and Nginx if not already installed. - Starts and enables Docker. ### Step 4 — Deploy Dockerized Application - Transfers project files to the remote server. - Builds and runs the container using the specified port. - If docker-compose.yml exists, uses docker-compose up -d --build. ### Step 5 — Nginx Reverse Proxy Automatically creates80 Nginx site configuration that: - Listens on port **80**. - Proxies incoming HTTP traffic to the app’s internal container port. - Writes access and error logs to /var/log/nginx/. ### Step 6 — Validation Performs: - Docker service health check. - Nginx service health check. - HTTP 200 OK test to confirm the app is reachable via Nginx. ### Step 7 — Optional Cleanup You can run: `bash bash deploy.sh --cleanup 
to remove containers, Nginx sites, and free up Docker space.
Example Usage
bash deploy.sh 
Example inputs during prompts:
Enter Git Repository URL: https://github.com/yourname/sample-app.git Enter Personal Access Token (PAT): ghp_xxxxxxxxxxxxxxxxx Enter Branch name [default: main]: main Enter Remote Server Username: ubuntu Enter Remote Server IP Address: 54.210.xx.xx Enter SSH Key Path: ~/.ssh/id_rsa Enter Application Port (internal container port): 8081 
Log Output
All progress and errors are logged in a file named:
deploy_YYYYMMDD.log 
Example:
deploy_20251022.log 
Error Handling
The script uses set -e to exit immediately on errors and provides contextual log messages for debugging.
If an error occurs, check the log file for detailed information.
Notes
The app’s Dockerfile must expose the same port entered during deployment (EXPOSE 8081, for example).
Nginx proxies traffic from port 80 → container port.
Make sure port 80 is open on your server’s firewall or security group.
Author
Your Name
DevOps Engineer in Training
(HNG Stage 0 - DevOps Track)