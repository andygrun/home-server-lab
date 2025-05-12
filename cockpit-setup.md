# Cockpit Setup

Cockpit provides a web GUI for managing Linux servers.

## Installation Steps

```bash
sudo apt update
sudo apt install cockpit -y
sudo systemctl enable --now cockpit.socket

Accessed via https://<server-ip>:9090

Logged in using Linux user credentials

Verified access to logs, network, storage, and terminal
