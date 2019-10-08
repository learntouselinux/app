# Learn to use Linux v1

Version 1 of learn to use linux represents a simple way to serve a single flat html file. The setup consists of a single host machine (Ubuntu 18.01) running apache.

## Basic Setup
- ssh into the machine using a super user account (likely the ubuntu username)
- update the linux box
    - `sudo apt update`
- install apache
    - `sudo apt install apache2`
- cd into `/etc/apache2/sites-available`
- disable default apache2 sites
    - `sudo a2dissite 000-default.conf`
- remove default apache2 sites
    - `sudo rm 000-default.conf default-ssl.conf`
- create a new conf `learntouselinux.com.conf` file to serve the flat html file from `/var/www/learntouselinux.com`
```
<Virtualhost *:80>
    Servername learntouselinux.com
    DocumentRoot /var/www/learntouselinux.com

    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</Virtualhost>
```
- remove old root folder
    - `sudo rm -rf /var/www/html`
- create the new root folder
    - `sudo mkdir /var/www/learntouselinux.com`
- enable the new conf file
    - `sudo a2ensite learntouselinux.com.conf`
- return to your host machine and execute `scp` to copy `index.html` to the remote server
    - `scp ./index.html ubuntu@<server-ip>:/var/www/learntouselinux.com`
- ssh back onto the remote machine and adjust permissions of the learntouselinux directory
    - `sudo chown -R www-data:www-data /var/www/learntouselinux.com`
- reload apache
    - `sudo systemctl reload apache2`
