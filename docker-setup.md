# Docker & Docker Compose Setup

## Docker

```bash
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
sudo usermod -aG docker $USER

Docker Compose
'''bash

sudo apt install docker-compose -y
Docker set to start on boot: sudo systemctl enable docker

Verified Docker with docker run hello-world
t

