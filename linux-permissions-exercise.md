🔑 Practise exercise to create users, groups and to manage permissions. 

✅ 1. Create a New User and Group for a Specific Service

Scenario: You're setting up a service (e.g., a web app) that should run under its own user and group for security isolation. 

🔹 sudo groupadd webapp 

why? In Linux, groups are used to manage permissions for multiple users. Here, we’re preparing to associate a user (and potentially others later) with this group for managing access to files or services like a web app. 

🔹 sudo useradd -r -d /opt/webapp -s /usr/sbin/nologin -g webapp webuser 

This creates a new system user with custom settings.

Breakdown of options:

Option	Meaning

-r	Create a system account (UID < 1000, typically non-login, for services)
-d /opt/webapp	Sets the home directory to /opt/webapp
-s /usr/sbin/nologin	Sets the login shell to a non-interactive one (blocks shell access)
-g webapp	Sets the primary group to webapp
webuser	The actual username being created

Why: You’re creating a non-login system user that will "own" or run a web application, but cannot SSH or log into the system interactively — a least-privilege security practice. 

🔹 sudo mkdir -p /opt/webapp

What it does: Creates the directory /opt/webapp.
-p: Ensures the full path is created if it doesn’t exist already.

Why: This directory is used as the home or working directory for the webuser. It might contain application code, configs, or runtime data.

🔹 sudo chown webuser:webapp /opt/webapp
What it does: Changes the ownership of /opt/webapp:

User owner: webuser
Group owner: webapp

Why: So only the webuser (and optionally others in the webapp group) can access or modify files inside this directory — another security measure to isolate file access to only what's needed by the application.

✅ Check if group exist

🔹 getent group webapp
If the group was created you will see an output otherwise nothing will come up. 

✅ Check if the user exists

🔹 id webuser
you should see something like:

uid=997(webuser) gid=1001(webapp) groups=1001(webapp)

✅ Check directory ownership 

🔹 ls -ld /opt/webapp 
This will show permissions, user group size date and path 

drwxr-xr-x 2 webuser webapp 4096 May 14 12:34 /opt/webapp

✅ Check login is disable 

🔹 sudo su - webuser
Try to "log in" as webuser using su (substitute user):

Output: This account is currently not available.

✅ Test file access permissions
Try writing a file to /opt/webapp as another user:


🔹 sudo -u nobody touch /opt/webapp/testfile
Expected result: Permission denied (unless the directory has overly loose permissions).

✅ Now try as webuser (just a dry run):

🔹 sudo -u webuser touch /opt/webapp/testfile
Expected result: The file should be created, showing webuser has write access.

💡 Summary: 

1. I have created a dedicated group and sustem user to run a service 
2. Ensured no login access for that user
3. Created a working directory for the service 
4. set ownership and permissions properly to enforce security. 


