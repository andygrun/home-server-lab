# Jellyfin Media Server

## Overview

Jellyfin is running as a Docker container on the Ubuntu home server.

The server is currently configured for local network access only. Remote access has intentionally not been enabled.

---

## Docker Configuration

Jellyfin was initially started using `docker run` and later migrated to Docker Compose.

The current configuration is managed with:

```text
~/jellyfin/docker-compose.yml
Docker Compose configuration
services:
  jellyfin:
    image: jellyfin/jellyfin:latest
    container_name: jellyfin
    network_mode: host
    volumes:
      - /srv/jellyfin/config:/config
      - /srv/jellyfin/cache:/cache
      - /media:/media
    restart: unless-stopped
Configuration directories
Host path	Container path	Purpose
/srv/jellyfin/config	/config	Jellyfin configuration and database
/srv/jellyfin/cache	/cache	Jellyfin cache
/media	/media	Media files
Media Storage

Media is stored under:

/media

Current directory structure:

/media/
├── movies/
└── bjj/
Movies
/media/movies

This directory is configured as the source for the Jellyfin Movies library.

BJJ
/media/bjj

This directory contains Brazilian Jiu-Jitsu instructional videos and is configured as the Jellyfin BJJ library.

Jellyfin Libraries

Current libraries:

Library	Host directory	Jellyfin path
Movies	/media/movies	/media/movies
BJJ	/media/bjj	/media/bjj

The BJJ library uses the Home Videos & Photos content type because the files are instructional videos rather than conventional movies.

File Transfer

Media files can be transferred from the Mac to the Ubuntu server over the local network using scp.

Example:

scp ~/Downloads/example.mp4 andygrun@192.168.1.100:/media/bjj/

The Ubuntu user needs write permission to the destination directory.

Example:

sudo chown -R andygrun:andygrun /media/bjj
Docker Compose Commands
Start Jellyfin
cd ~/jellyfin
docker compose up -d
Stop Jellyfin
cd ~/jellyfin
docker compose down
Restart Jellyfin
cd ~/jellyfin
docker compose restart
View container status
cd ~/jellyfin
docker compose ps
View logs
cd ~/jellyfin
docker compose logs
Follow logs
cd ~/jellyfin
docker compose logs -f
Container Health

The Jellyfin container should report a healthy status.

Check with:

docker ps

Expected status:

Up (healthy)

Docker Compose can also be used:

cd ~/jellyfin
docker compose ps
Network Configuration

Jellyfin uses Docker host networking:

network_mode: host

This allows Jellyfin to use the Ubuntu server's network interface directly.

Jellyfin's default web interface is available on:

http://SERVER_IP:8096

For example:

http://192.168.1.100:8096

Remote access is currently disabled.

Restart Policy

The Compose configuration uses:

restart: unless-stopped

This allows Docker to automatically restart Jellyfin after a server reboot or container failure, unless the container was explicitly stopped.

The configured restart policy can be checked with:

docker inspect jellyfin --format '{{.HostConfig.RestartPolicy.Name}}'

Expected output:

unless-stopped
Initial Jellyfin Setup

The Jellyfin setup wizard was configured with:

Metadata language: English
Country/region: Portugal
Remote connections: Disabled
Automatic port mapping: Disabled
Migration from Docker Run to Docker Compose

Jellyfin was initially deployed with docker run.

The initial container was created using bind mounts for the configuration, cache, and media directories.

Example:

docker run -d \
  -v /srv/jellyfin/config:/config \
  -v /srv/jellyfin/cache:/cache \
  -v /media:/media \
  --net=host \
  jellyfin/jellyfin:latest

The container was later stopped and replaced with a Docker Compose-managed container.

The important part of the migration was preserving the existing bind mounts:

/srv/jellyfin/config
/srv/jellyfin/cache
/media

This allowed the new Compose-managed container to use the existing Jellyfin configuration and media.

Docker Run vs Docker Compose
Docker Run

docker run is useful for quickly creating and testing a container.

The configuration is provided directly as command-line arguments.

For example:

docker run -d \
  -v /srv/jellyfin/config:/config \
  -v /srv/jellyfin/cache:/cache \
  -v /media:/media \
  --net=host \
  jellyfin/jellyfin:latest

The disadvantage is that the configuration can become difficult to remember and reproduce when a container has many options.

Docker Compose

Docker Compose stores the container configuration in a YAML file.

For example:

services:
  jellyfin:
    image: jellyfin/jellyfin:latest
    container_name: jellyfin
    network_mode: host
    volumes:
      - /srv/jellyfin/config:/config
      - /srv/jellyfin/cache:/cache
      - /media:/media
    restart: unless-stopped

The service can then be managed with:

docker compose up -d

This makes the configuration:

Easier to read
Easier to modify
Easier to reproduce
Easier to version-control with Git
Easier to manage as the server grows

For persistent home-server services, Docker Compose is more maintainable than relying on manually remembered docker run commands.

Lessons Learned
Linux permissions

The /media/movies directory was initially created by root, which prevented the normal Ubuntu user from uploading files using scp.

The directory ownership was changed:

sudo chown -R andygrun:andygrun /media/movies

The same approach was used for the BJJ directory:

sudo chown -R andygrun:andygrun /media/bjj

This allowed files to be transferred directly from the Mac over SSH.

Media organization

Initially, the BJJ instructional videos were placed in /media/movies.

They were later moved to:

/media/bjj

A dedicated Jellyfin BJJ library was then created.

The Movies library was recreated so that the moved files were no longer incorrectly listed as movies.

Docker container verification

The Jellyfin container was verified from both the Ubuntu host and inside the container.

For example:

docker exec -it jellyfin ls -lah /media/movies

This confirmed that the /media/movies directory was correctly mounted into the container.

## Current Status

Jellyfin is operational and running under Docker Compose.

### Completed

- [x] Jellyfin installed
- [x] Jellyfin running in Docker
- [x] Migrated from `docker run` to Docker Compose
- [x] Persistent configuration
- [x] Persistent cache
- [x] Media storage configured
- [x] Movies library created
- [x] BJJ library created
- [x] Media transferred over the local network
- [x] Linux permissions configured
- [x] Container health verified
- [x] Restart policy configured
- [x] Local network access verified
- [x] Remote access intentionally disabled

### Future Tasks

- [ ] Test Jellyfin after an Ubuntu server reboot
- [ ] Add more media
- [ ] Investigate hardware transcoding
- [ ] Learn more about Docker networking
- [ ] Consider remote access in the future
- [ ] Add additional Docker services