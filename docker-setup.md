# Docker & Docker Compose Setup

## Docker

Install Docker Engine

Bash -

sudo apt update
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

Docker Compose

bash -

sudo apt install docker-compose -y
Docker set to start on boot: sudo systemctl enable docker

Verified Docker with docker run hello-world

✅ Enable non-root usage (optional but recommended)

sudo usermod -aG docker $USER

