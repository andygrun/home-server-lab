🔑 Linux Users, Groups and Permissions Management 

No matter if you are a SystemAdmin, Cloud Engineer or simply a Linux enthusiastic user, knowing how to properly manage users, groups and permissiosn is essential for everyday tasks and to maintain a secure enviroment. 

🧑‍💻 USERS
A user is an individual account on the system. Each user has:

* A username (e.g., john, admin)
* A unique User ID (UID)
* A home directory (e.g., /home/john)
* A default shell (e.g., /bin/bash)
* An associated primary group

Types of Users:

1. Root – Superuser with UID 0. Has unrestricted access.
2. Regular users – Created by administrators or during installation.
3. System users – Used by services (e.g., www-data for web server).

👥 GROUPS 

Groups are a collection of users which make managing permissions easier and mmore efficient. 
Every file/directory has an owner (ser) and  an associeted group. 

🔧 Use groups [username] to list the groups a user belongs to. 

🔐 PERMISSIONS 

In the linux sytem EVERYTHING is a file or a folder and they have permissions that determine who can do what. 

Three types of permissions:

Symbol	Meaning	    Applies to
r	    Read	    View file content or list directory
w	    Write	    Modify file or directory contents
x	    Execute	    Run file or enter directory

This is how a permission string looks like: 
-rwxr-xr-- 

They are composed of 3 sets of 3 pemissons for the three different categorions 

1-3 Onwer 
4-6 Group 
7-9 Others

🔧 Commands

ls -l – Show file permissions
chmod – Change permissions
chown – Change file owner
chgrp – Change group of file





