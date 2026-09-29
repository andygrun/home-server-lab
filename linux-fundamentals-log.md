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

## Day 5 — Users and Permissions

**Status:** Completed
**Environment:** Ubuntu Server 26.04.1 LTS
**Working directory:** `/home/andygrun/permissions-training`
**Date:** 2026-09-29

### Objective

Understand Linux users, groups, file ownership, and permissions, and learn how Linux determines whether a user can access, modify, or execute a filesystem object.

### Tasks Completed

#### 1. Identify the current user and group memberships

```bash
id
groups
```

Purpose: Displays the current user's UID, primary group, supplementary groups, and group memberships.

Key result:

* User: `andygrun`
* UID: `1000`
* `andygrun` is a member of several supplementary groups, including `main-group`.

#### 2. Inspect group information

```bash
getent group main-group
```

Purpose: Retrieves information about the `main-group` group.

#### 3. Create a new group

```bash
sudo groupadd main-group
```

Purpose: Creates a new Linux group.

#### 4. Add the current user to the group

```bash
sudo usermod -aG main-group andygrun
```

Purpose: Adds `andygrun` to `main-group`.

Key concept:

* `-G` specifies supplementary groups.
* `-a` means append, preventing existing supplementary group memberships from being replaced.

#### 5. Create a practice file

```bash
touch test.txt
ls -l test.txt
```

Purpose: Creates an empty file and displays its ownership and permissions.

Initial ownership showed:

```text
andygrun andygrun
```

#### 6. Change the group owner

```bash
sudo chgrp main-group test.txt
ls -l test.txt
```

Purpose: Changes the group owner of the file without changing the user owner.

The file ownership became:

```text
andygrun main-group
```

#### 7. Modify group permissions using symbolic notation

```bash
chmod g-w test.txt
chmod g+w test.txt
```

Purpose: Removes and restores write permission for the file's group.

Permission classes:

* `u` = user/owner
* `g` = group
* `o` = others
* `a` = all

Operators:

* `+` = add permission
* `-` = remove permission
* `=` = set permissions exactly

Permission types:

* `r` = read
* `w` = write
* `x` = execute
* `-` = permission not granted

Important concept:

`chmod g+w` applies to the file's **group owner**, not to a group named in the command.

#### 8. Practice numeric permissions

Numeric permission values:

| Permission | Value |
| ---------- | ----: |
| `r`        |     4 |
| `w`        |     2 |
| `x`        |     1 |

Examples:

| Symbolic | Numeric |
| -------- | ------: |
| `rwx`    |       7 |
| `rw-`    |       6 |
| `r-x`    |       5 |
| `r--`    |       4 |
| `-w-`    |       2 |
| `--x`    |       1 |

Commands tested:

```bash
chmod 640 test.txt
chmod 600 test.txt
chmod 755 test.txt
```

Key concept:

Permissions are always displayed in the fixed order:

```text
r w x
```

A missing permission is represented by `-`.

For example:

```text
r-x
```

means read and execute, but no write permission.

#### 9. Practice directory permissions

```bash
mkdir test-dir
chmod 755 test-dir
ls -ld test-dir
```

Purpose: Creates a directory and sets its permissions.

Directory permissions have different meanings from file permissions:

| Permission | Directory meaning                 |
| ---------- | --------------------------------- |
| `r`        | List directory contents           |
| `w`        | Create, delete, or rename entries |
| `x`        | Enter/traverse the directory      |

**Traverse** means being able to enter or pass through a directory to access objects inside it.

#### 10. Test directory write permissions

Created a file inside the directory:

```bash
touch test-dir/secret.txt
```

Removed the owner's write permission from the directory:

```bash
chmod u-w test-dir
```

Attempting to create a file then resulted in:

```text
Permission denied
```

Restored the permission:

```bash
chmod u+w test-dir
```

Key concept:

The ability to create or delete directory entries depends primarily on the **directory's write permission**, not the file's own write permission.

#### 11. Test file deletion

```bash
rm test-dir/secret.txt
touch test-dir/secret.txt
```

The file could be deleted because the user had write permission on the directory.

#### 12. Change file ownership

```bash
sudo chown root test-dir/secret.txt
ls -l test-dir/secret.txt
```

The file ownership changed from:

```text
andygrun andygrun
```

to:

```text
root andygrun
```

Key concept:

Every file has both:

* A user owner
* A group owner

#### 13. Change the group owner

```bash
sudo chgrp main-group test-dir/secret.txt
ls -l test-dir/secret.txt
```

The ownership became:

```text
root main-group
```

#### 14. Test group permissions with a different file owner

Removed group write permission:

```bash
sudo chmod g-w test-dir/secret.txt
ls -l test-dir/secret.txt
```

Result:

```text
-rw-r--r-- 1 root main-group ... secret.txt
```

Because `andygrun` is a member of `main-group`, the group permissions apply to the user.

Attempting to append to the file:

```bash
echo "permission test" >> test-dir/secret.txt
```

Result:

```text
Permission denied
```

This demonstrated that group membership does not automatically grant write access. The group must actually have the required permission.

Restored group write permission:

```bash
sudo chmod g+w test-dir/secret.txt
```

Then:

```bash
echo "permission test" >> test-dir/secret.txt
cat test-dir/secret.txt
```

The write succeeded.

### Key Concepts Learned

#### Users and Groups

Linux uses users and groups to control access to filesystem objects.

A file has:

```text
user owner
group owner
```

A user can belong to multiple supplementary groups.

#### File Ownership

Example:

```text
-rw-rw-r-- 1 root main-group ... secret.txt
```

The ownership is:

```text
root
main-group
```

The first is the user owner and the second is the group owner.

#### Permission Classes

Linux permissions are divided into:

```text
u = user/owner
g = group
o = others
```

For example:

```text
-rw-r-----
```

means:

* Owner: `rw-`
* Group: `r--`
* Others: `---`

#### Permission Evaluation

If a user is not the file owner but belongs to the file's group, the **group permissions** apply.

For example:

```text
-rw-r----- 1 root developers ...
```

If `andy` belongs to `developers`:

* Read: Yes
* Write: No
* Execute: No

#### Files vs Directories

Permissions behave differently on files and directories.

For a file:

* `r` = read contents
* `w` = modify contents
* `x` = execute

For a directory:

* `r` = list contents
* `w` = create/delete/rename entries
* `x` = enter/traverse

#### Ownership vs Group Membership

Being a member of a group does not give a user permission to change a file's ownership or permissions.

In the practical exercise, `andygrun` could use the permissions granted to `main-group`, but could not run:

```bash
chmod g-w test-dir/secret.txt
```

because `root` was the file owner.

Using:

```bash
sudo chmod g-w test-dir/secret.txt
```

worked because elevated privileges were used.

### Commands Practiced

```bash
id
groups
getent group main-group

sudo groupadd main-group
sudo usermod -aG main-group andygrun

touch test.txt
ls -l test.txt

sudo chgrp main-group test.txt

chmod g-w test.txt
chmod g+w test.txt

chmod 640 test.txt
chmod 600 test.txt
chmod 755 test.txt

mkdir test-dir
ls -ld test-dir

chmod u-w test-dir
chmod u+w test-dir

touch test-dir/secret.txt
rm test-dir/secret.txt

sudo chown root test-dir/secret.txt
sudo chgrp main-group test-dir/secret.txt

sudo chmod g-w test-dir/secret.txt
sudo chmod g+w test-dir/secret.txt

echo "permission test" >> test-dir/secret.txt
cat test-dir/secret.txt
```

### Day 5 Assessment

**Result: Passed**

Successfully demonstrated understanding of:

* Linux users and groups
* Primary and supplementary group membership
* File user and group ownership
* Symbolic permissions
* Numeric permissions
* `chmod`
* `chown`
* `chgrp`
* Directory permissions
* The relationship between group membership and file permissions
* Why permission-denied errors occur
* The difference between modifying a file and deleting a directory entry

The practical exercises confirmed that Linux access control is determined by the combination of **user identity, group membership, ownership, and permissions**.

