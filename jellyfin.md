# Jellyfin + Docker + Samba

Jellyfin is a free and open-source media server and suite of multimedia applications designed to organize, manage, and share digital media files to networked devices. 

I've installed it on a docker container and I will use samba file sharing as media souce for a Netflix like experience in my LAN. 

✅ Prerequisites
Make sure you’ve already:

Installed Docker and Docker Compose.
Opened the necessary ports (e.g., with UFW).
reated a directory for your media and configuration.

 ✅ Why Use Docker + Samba-Shared Files for Jellyfin

🔧 Architecture Summary

Samba lets you easily add, rename, or organize files from your Mac or Windows machine.
Dockerized Jellyfin reads media from a bind-mounted volume (/media) that points to the same shared directory.
Jellyfin streams it locally or remotely — clean and isolated.

🧑‍💻 Pros of This Setup

Benefit	                                    Description
🧹 Clean separation	                        Docker keeps Jellyfin contained — easy to backup                                      or reinstall.
🔁 Easy updates	Update                      Jellyfin by just pulling a new container image.
🛠 Linux practice	                        You learn about Docker volumes, permissions, media types.
🔄 Smooth workflow	                        Drag & drop media into your Samba share — it appears in Jellyfin.
🌍 Remote access ready	                    Add reverse proxy (e.g., Caddy, Nginx) + Tailscale/Cloudflare                                  Tunnel for secure remote streaming.

