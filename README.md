# FSWD-Project-6-Linux-Server-Configuration

## Public IP Address

35.165.244.231

## SSH Port

Port 2200

## URL

## Software Installed

finger

## Configurations made

1. Create a new user named grader and grant this user sudo permissions.
    - `adduser grader`
    - Add grader to the sudoers list by placing a new file in the */etc/sudoers.d/* directory with the following line `grader ALL=(ALL) ALL`
    - Generate ssh keys for the grader on the local machine and place the public key on the AWS instance by copying it to the grader's *.ssh/authorized_keys* file
    - 
2. Update all currently installed packages.
    - `sudo apt-get update`: Update the package source lists
    - `sudo apt-get upgrade`: Upgrade the installed packages
    - `sudo apt-get autoremove`: Remove packages no longer needed
3. Configure the local timezone to UTC. No change required. Machine already on UTC+0
```
    $date
    Mon Dec 19 00:36:49 UTC 2016
```
4. Install and configure Apache to serve a Python mod_wsgi application
5. Change the SSH port from 22 to 2200
6. Configure the Uncomplicated Firewall (UFW) to only allow incoming connections for SSH (port 2200), HTTP (port 80), and NTP (port 123)
7. Install and configure PostgreSQL:
    a. Do not allow remote connections
    b. Create a new user named catalog that has limited permissions to your catalog application database
8. Install git, clone and set up your Catalog App project (from your GitHub repository from earlier in the Nanodegree program) so that it functions correctly when visiting your server’s IP address in a browser. Remember to set this up appropriately so that your .git directory is not publicly accessible via a browser!
9. Your Amazon EC2 Instance's public URL will look something like this: http://ec2-XX-XX-XXX-XXX.us-west-2.compute.amazonaws.com/ where the X's are replaced with your instance's IP address. You can use this url when configuring third party authentication. Please note the the IP address part of the AWS URL uses dashes, not dots.

## Third-party resources

http://askubuntu.com/questions/345974/what-is-the-difference-between-adduser-and-useradd

http://www.ducea.com/2006/06/18/linux-tips-password-usage-in-sudo-passwd-nopasswd/

http://superuser.com/questions/309034/how-to-check-which-timezone-in-linux
http://www.thegeekstuff.com/2010/09/change-timezone-in-linux/