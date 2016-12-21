# Linux Server Configuration

## Public IP Address

35.165.244.231

## SSH Port

Port 2200

## URL

http://ec2-35-165-244-231.us-west-2.compute.amazonaws.com/catalog/

## Software Installed

- finger
- lynx
- apache2
- postgresql
- git
- python-pip
- python-psycopg2
- unattended-upgrades
- munin

## Configurations made

1. Create a new user named grader and grant this user sudo permissions.
    - `adduser grader`
    - Add grader to the sudoers list by placing a new file in the */etc/sudoers.d/* directory with the following line `grader ALL=(ALL) ALL`
    - Generate ssh keys for the grader on the local machine and place the public key on the AWS instance by copying it to the grader's *.ssh/authorized_keys* file
    - Disable remote root login via the following item in */etc/ssh/sshd_config*: `PermitRootLogin no`
2. Update all currently installed packages.
    - `sudo apt-get update`: Update the package source lists
    - `sudo apt-get upgrade`: Upgrade the installed packages
    - `sudo apt-get autoremove`: Remove packages no longer needed
    - `sudo apt-get install unattended-upgrades`: Install auto updates
    - `sudo dpkg-reconfigure --priority=low unattended-upgrades`: Configure auto updates
3. Configure the local timezone to UTC. No change required. Machine already on UTC+0:

        $date
        Mon Dec 19 00:36:49 UTC 2016
4. Install and configure Apache to serve a Python mod_wsgi application
    - `sudo apt-get install apache2`
    - `sudo apt-get install libapache2-mod-wsgi`
    - `sudo `
5. Change the SSH port from 22 to 2200
    -  Change the SSH port via the following item in */etc/ssh/sshd_config*:`Port 2200`
6. Configure the Uncomplicated Firewall (UFW) to only allow incoming connections for SSH (port 2200), HTTP (port 80), and NTP (port 123)
    - `ufw default deny incoming`
    - `ufw default allow outgoing`
    - `ufw allow 2200/tcp`
    - `ufw allow http`
    - `ufw allow ntp`
7. Install and configure PostgreSQL:
    a. Do not allow remote connections
    b. Create a new user named catalog that has limited permissions to your catalog application database
        - `sudo -u postgres createuser catalog`
        - `sudo -u postgres createdb catalog`
        - `sudo adduser catalog`
        - `sudo -u postgres psql`
        - `ALTER DATABASE catalog OWNER TO catalog`
        - `sudo -u catalog psql`
        - 
8. Install git, clone and set up your Catalog App project (from your GitHub repository from earlier in the Nanodegree program) so that it functions correctly when visiting your server’s IP address in a browser. Remember to set this up appropriately so that your .git directory is not publicly accessible via a browser!
    - `sudo apt-get install git`
    - `git clone {url of github repository}`
    - `sudo apt-get install python-pip`
    - `sudo apt-get install python-psycopg2`
    - `sudo apt-get install libpq-dev`
    - `pip install flask sqlalchemy oauth2client`
    - To make the .git directory publicly inaccessible put this in an .htaccess file at the root of the web server: `RedirectMatch 404 /\.git`
9. Amazon EC2 Instance's public URL: http://ec2-35-165-244-231.us-west-2.compute.amazonaws.com/
    - Used this url when configuring Google connect authentication.
    - Installed Munin for monitoring. Accessible from http://ec2-35-165-244-231.us-west-2.compute.amazonaws.com/munin

## Third-party resources

### User account management
http://askubuntu.com/questions/345974/what-is-the-difference-between-adduser-and-useradd

### SSH
http://askubuntu.com/questions/449364/what-does-without-password-mean-in-sshd-config-file
https://mediatemple.net/community/products/dv/204643810/how-do-i-disable-ssh-login-for-the-root-user

### sudo
http://www.ducea.com/2006/06/18/linux-tips-password-usage-in-sudo-passwd-nopasswd/

### timezone
http://superuser.com/questions/309034/how-to-check-which-timezone-in-linux
http://www.thegeekstuff.com/2010/09/change-timezone-in-linux/

### Firewall
http://askubuntu.com/questions/30781/see-configured-rules-even-when-inactive

### Package Installation
http://askubuntu.com/questions/423355/how-do-i-check-if-a-package-is-installed-on-my-server

### Postgresql
http://alvinalexander.com/blog/post/postgresql/log-in-postgresql-database
https://www.digitalocean.com/community/tutorials/how-to-secure-postgresql-on-an-ubuntu-vps
http://stackoverflow.com/questions/4313323/how-to-change-owner-of-postgresql-database

### Apache
http://askubuntu.com/questions/14763/where-are-the-apache-and-php-log-files
http://stackoverflow.com/questions/6142437/make-git-directory-web-inaccessible
https://www.digitalocean.com/community/tutorials/how-to-install-munin-on-an-ubuntu-vps#step-one%14install-munin

### Flask Deployment
http://flask.pocoo.org/docs/0.11/deploying/mod_wsgi/
http://stackoverflow.com/questions/28253681/you-need-to-install-postgresql-server-dev-x-y-for-building-a-server-side-extensi

