# Learning Log

## Git

* GitHub no longer accepts account passwords for Git pushes over HTTPS.
* Configured SSH authentication using an Ed25519 key.
* Learned the difference between local and remote branches.
* Used `git pull --rebase` to reconcile divergent local and remote histories.

## Docker

* Learned how a `Dockerfile` defines how an image is built.
* Learned the difference between a Docker image and a container.
* Learned port mapping, including `8080:80`.
* Rebuilt and replaced containers during deployment.

## Linux

* Configured SSH access to an Ubuntu Server.
* Learned basic Linux filesystem structure.
* Worked with file permissions.
* Learned about `systemd` services and how they can be used to manage long-running processes.

## GitHub Actions

* Learned GitHub Actions workflow YAML syntax.
* Configured and used a self-hosted runner.
* Learned about workflow triggers, jobs, and steps.
* Automated Docker-based deployment to the home server.

## Troubleshooting

* Fixed a workflow that initially failed because of YAML indentation.
* Troubleshot a workflow that remained queued because the self-hosted runner was not running and listening for jobs.
* Converted the GitHub Actions runner into a `systemd` service so it starts automatically.
* Resolved case-sensitive file path issues during the Docker/Nginx deployment.
