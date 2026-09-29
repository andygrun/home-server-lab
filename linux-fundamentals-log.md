# Linux Fundamentals Learning Log

A hands-on learning log documenting my progress toward becoming a Linux System Administrator. Each entry covers the concepts learned, practical tasks completed, commands used, and key takeaways.

## Day 1 — Linux Server Fundamentals

**Status:** Completed
**Environment:** Ubuntu Server 26.04.1 LTS
**Server:** lab
**Date:** 2026-09-29

**Objective**

Understand the Linux server environment, identify the operating system and kernel, and explore the Linux filesystem.

**Commands used:**

* `whoami` — identify the current user
* `hostname` — identify the server hostname
* `cat /etc/os-release` — identify the operating system and version
* `uname -r` — identify the running Linux kernel
* `pwd` — identify the current working directory
* `ls /` — inspect the root filesystem
* `ls /var/log` — inspect system log locations

**Results:**

* Current user: `andygrun`
* Hostname: `lab`
* Operating system: Ubuntu 26.04.1 LTS (Resolute Raccoon)
* Kernel: `7.0.0-31-generic`
* Home directory: `/home/andygrun`
* Explored `/srv` within the root filesystem
* Inspected `/var/log` for system and application logs

**Key concepts learned:**

* `/etc` — system-wide configuration files
* `/home` — home directories for regular users
* `/var` — variable data, including logs and application data
* `/usr` — installed programs, libraries, and shared resources
* `/srv` — data served by system services
* `/` — the root of the Linux filesystem

**Key takeaways:**

* `whoami` identifies the current user.
* `hostname` identifies the server.
* `cat /etc/os-release` displays operating system information.
* `uname -r` displays the running kernel version.
* `pwd` displays the current working directory.
* Linux organizes files and directories under a single root directory: `/`.
* Logs are essential for troubleshooting Linux systems.

**Test:** Successfully identified the server environment, operating system, kernel, current user, working directory, and key filesystem directories.

**Assessment:** Passed

---

## Day 2 — Files and Directory Management

**Status:** Completed
**Environment:** Ubuntu Server 26.04.1 LTS
**Working directory:** `/home/andygrun/linux-training`
**Date:** 2026-09-29

**Objective**

Learn how to create, inspect, modify, copy, rename, move, and remove files and directories using Linux command-line tools.

**Commands used:**

* `mkdir linux-training` — create a practice directory
* `cd linux-training` — change the current directory
* `pwd` — verify the current location
* `touch notes.txt` — create an empty file
* `ls -l` — inspect detailed file information
* `echo "..." > notes.txt` — write and overwrite file contents
* `cat notes.txt` — read file contents
* `cp notes.txt backup.txt` — copy a file
* `mv backup.txt notes-backup.txt` — rename a file
* `mkdir archive` — create a subdirectory
* `mv notes-backup.txt archive/` — move a file
* `ls -l archive/` — inspect directory contents
* `ls -R` — recursively inspect directory contents
* `cd ..` — return to the parent directory
* `rm -r linux-training` — remove the practice environment

**Test:** Created a complete practice environment, manipulated files and directories, inspected the results, and removed the environment after completing the exercises.

**Redirection operators:**

* `>` — redirects output and overwrites existing file contents
* `>>` — redirects output and appends to existing file contents

**Example:**

```bash
echo "First line" > example.txt
echo "Second line" >> example.txt
cat example.txt
```

Output:

```text
First line
Second line
```

Overwriting the file:

```bash
echo "New content" > example.txt
```

The existing contents are replaced with `New content`.

**Key concepts learned:**

* `mkdir` creates directories.
* `cd` changes the current directory.
* `pwd` displays the current directory.
* `touch` creates an empty file or updates timestamps.
* `ls -l` displays detailed file information.
* `cat` displays file contents.
* `cp` creates copies.
* `mv` moves or renames files.
* `rm -r` recursively removes directories and their contents.
* `>` overwrites existing file contents.
* `>>` appends to existing file contents.

**Safety note:** `rm -r` permanently removes files and directories without moving them to a trash folder. Always verify the target path before executing it.

**Assessment:** Passed

---

## Day 3 — journalctl

**Status:** Completed
**Environment:** Ubuntu Server 26.04.1 LTS
**Date:** 2026-09-22

**Objective**

Learn how to use `journalctl` to inspect, filter, and follow system logs managed by `systemd`.

**Commands used:**

* `journalctl --since "..." --until "..."` — filter logs by a specific time window
* `journalctl --since today` — display logs from today
* `journalctl --since yesterday` — display logs from yesterday
* `journalctl -f` — follow logs live as new entries are written
* `systemctl list-units --type=service --state=running` — confirm running services before filtering
* `journalctl -u docker.service` — filter the journal for a specific systemd unit

**Test:** Pushed changes to GitHub → CI/CD triggered → container redeployed → watched the deployment activity live using `journalctl -f`. Separately queried `docker.service` directly using `journalctl -u docker.service`.

**Real finding:** `journalctl -u docker.service` surfaced a genuine `dockerd` healthcheck failure (`Unavailable: connection ...`) from September 10. The issue was buried in the full journal but became immediately visible after narrowing the logs to the specific unit.

**Key takeaways:**

* `journalctl` provides access to logs collected by `systemd-journald`.
* Time filtering makes large log sets easier to investigate.
* `journalctl -f` is useful for watching events as they happen.
* Filtering by unit with `-u` makes service-specific troubleshooting much easier.
* Effective Linux troubleshooting often starts by narrowing a large set of logs to the relevant service and time period.

**Assessment:** Passed

---

## Day 4 — systemctl

**Status:** Completed
**Environment:** Ubuntu Server 26.04.1 LTS
**Date:** 2026-09-24

**Objective**

Learn how to use `systemctl` to inspect and manage `systemd` services and understand the runtime state of units.

**Commands used:**

* `systemctl --help` — explore available `systemctl` functionality
* `systemctl list-units` — list currently loaded units
* `systemctl stop docker` — stop the Docker service
* `systemctl restart docker` — restart the Docker service
* `systemctl is-active ssh` — check whether the SSH service is currently active
* `systemctl status ssh` — display detailed runtime information about the SSH service

**Test:** Checked runtime information for systemd units, stopped and restarted a service, and checked the service state again to verify the effect of the changes.

**Key concepts learned:**

* `systemctl` is used to communicate with and manage `systemd`.
* A systemd **unit** can represent services and other system resources.
* `systemctl list-units` displays currently loaded units.
* `systemctl status` provides detailed information about a unit.
* `systemctl is-active` provides a simple active/inactive state check.
* `systemctl stop` stops a running service.
* `systemctl restart` stops and starts a service again.

**Key takeaways:**

* `systemctl status` is useful when investigating why a service is not behaving as expected.
* `systemctl is-active` is useful when only the current service state is needed.
* Services can be controlled directly from the command line.
* Understanding `systemctl` is important for Linux service administration and troubleshooting.

**Assessment:** Passed
