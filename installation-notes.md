# Ubuntu Server Installation Notes

Download Ubuntu Server LST here: 
https://ubuntu.com/download/server 

🔦 Flash the ISO to a USB Stick using Balena Etcher (macOS) or a disk imaging program of your choice:

Go to https://etcher.balena.io/ and download Etcher 

Plug in a USB stick with 4gb minimum and make sure to back up any data from your USB, this will be formatted clean

Select the Image (ISO you downloaded from Ubuntu's websire) select the drive (your USB stick) flash it! 

🤖 BIOS Settings 





- Installed Ubuntu Server 22.04 LTS on old laptop.
- Set static IP address during install.
- Enabled OpenSSH server.
- Connected via SSH from Mac.

## SSH Configuration

- Generated SSH key on Mac with `ssh-keygen`.
- Copied public key to server using `ssh-copy-id`.
- Verified key-based login.

