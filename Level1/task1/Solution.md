1. Install Docker CE and Docker Compose
sudo yum install -y yum-utils

Add Docker’s official repository:
sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo

Install Docker CE and Docker Compose:
sudo yum install -y docker-ce docker-ce-cli containerd.io docker-compose-plugin

✔️ This installs docker-ce and docker compose (v2 plugin).

2. Start and Enable Docker Service

sudo systemctl start docker
sudo systemctl enable docker

3. Verify Installation

docker --version
docker compose version
systemctl status docker

