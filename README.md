# Linux server config
Server runs at http://ec2-52-11-138-112.us-west-2.compute.amazonaws.com/

### Users
- Added `grader` user.
- Gave `grader` root permission by creating a sudoers.d/grader file with appropriate config.
- Configured /etc/ssh/sshd_config to change port to 2200 and disabled root login.
- Added keys and changed permission of the ~/.ssh/ directory.

### Update / Upgrade
- sudo apt-get update && sudo apt-get upgrade
- sudo apt-get install unattended-upgrades

Enable it to automatically update
- sudo dpkg-reconfigure --priority=low unattended-upgrades

### UFW
Allowed incoming for ssh on port 2200, HTTP on port 80, and NTP on port 123
- sudo ufw allow 2200/tcp
- sudo ufw allow www
- sudo ufw allow 123/udp

Enable ufw
- sudo ufw enable

### Time
- Changed timezone to UTC from EST using: `dpkg-reconfigure tzdata`.

### Install git
- sudo apt-get install git

### Install PIP and project dependencies
- sudo apt-get install python-pip

Python libs installed:
- oauth2client
- dicttoxml
- Flask
- Flask-Login
- psycopg2
- requests
- sqlalchemy
- werkzeug

### Git repo
- Cloned playlist-crud-app repo into /var/www/
- Created .htaccess file with appropriate redirect config to make .git/ directory unavailable through browsers

### Install Apache
- sudo apt-get install apache2
- sudo apt-get install python-setuptools
- sudo apt-get install libapache2-mod-wsgi
- sudo apt-get install python-dev
- Created .conf file for the playlist app (see `/etc/apache2/sites-available/playlist.conf`)
- Added .wsgi file (see `/var/www/playlist/flaskapp.wsgi/`)
- Enabled virtual host (`sudo a2ensite playlist`)

### PostgreSQL
- sudo apt-get install postgresql postgresql-contrib
- sudo apt-get install postgresql-server-dev-all
- Set up postgres user.
- Created database owned by created user.
Please check with `\du` when in `psql` for details.
- Added hardcoded paths to google/facebook secrets
- Swapped sqlite3 for postgresql database creation (see __init__.py / databse_setup.py in `/var/www/playlist/playlist`)

Resources:
https://discussions.udacity.com/t/project-5-resources/28343
