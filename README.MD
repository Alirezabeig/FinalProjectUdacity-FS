
For this project we should deploy our app to the web. 

All I have done to deploy my app to the web using ubuntu on Amazon lightsail.

IP address: 54.201.251.44

Project details: 
Prepare a linux configuraiton on a virtual machine to host your web application
Accessible SSH port: 2200


Create a new user:
Sudo adduser grader
Create a new file in the sudoers directory with sudo nano /etc/sudoers.d/grader
Add the following text grader ALL=(ALL:ALL) ALL
Download package lists with sudo apt-get update
Fetch new versions of packages with sudo apt-get upgrade
Change SSH port from 22 to 2200
Run sudo nano /etc/ssh/sshd_config
Change the port from 22 to 2200

Install Apache
sudo apt-get install apache2
Install mod_wsgi

Run sudo apt-get install libapache2-mod-wsgi python-dev
Enable mod_wsgi with sudo a2enmod wsgi
Start the web server with sudo service apache2 start

Install git using: sudo apt-get install git
cd /var/www
sudo mkdir Item_catalog-
cd Item_catalog- 
sudo mkdir Item_catalog- 
Clone the Item Catalog app from my github https://github.com/Alirezabeig/Item_catalog-Github

Create a catalog.wsgi file, then add this inside:
import sys
import logging
logging.basicConfig(stream=sys.stderr)
sys.path.insert(0, "/var/www/Item_catalog-/")

from Item_catalog- import app as application
application.secret_key = 'supersecretkey'

Rename project.py to init.py mv project.py __init__.py
Install virtual environment
Install the virtual environment sudo pip install virtualenv
Create a new virtual environment with sudo virtualenv venv
Activate the virutal environment source venv/bin/activate
Change permissions sudo chmod -R 777 venv
Install Flask and other dependencies
Install pip with sudo apt-get install python-pip
Install Flask pip install Flask
Install other project dependencies sudo pip install httplib2 oauth2client sqlalchemy psycopg2 sqlalchemy_utils
Update path of client_secrets.json file

nano __init__.py
Change client_secrets.json path to /var/www/Item_catalog-/Item_catalog-/client_secrets.json
Configure and enable a new virtual host
Run this: sudo nano /etc/apache2/sites-available/Item_catalog-.conf

   ----------
   
Hee is my Conf file: <VirtualHost *:80>
ServerName mywebsite.com
ServerAdmin almo7383@colorado.edu
WSGIScriptAlias / /var/www/Item_catalog-/Item_catalog-.wsgi
<Directory /var/www/Item_catalog-/Item_catalog-/>
Order allow,deny
Allow from all
</Directory>
Alias /static /var/www/Item_catalog-/Item_catalog-/static
<Directory /var/www/Item_catalog-/Item_catalog-/static/>
Order allow,deny
Allow from all
</Directory>
ErrorLog ${APACHE_LOG_DIR}/error.log
LogLevel warn
CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>


Enable the virtual host sudo a2ensite catalog

Install and configure PostgreSQL
sudo apt-get install libpq-dev python-dev
sudo apt-get install postgresql postgresql-contrib
sudo su - postgres
psql

CREATE USER catalog WITH PASSWORD 'password';
ALTER USER catalog CREATEDB;
CREATE DATABASE Item_catalog- WITH OWNER catalog;
\c Item_catalog-
REVOKE ALL ON SCHEMA public FROM public;
GRANT ALL ON SCHEMA public TO Item_catalog-;
\q
exit
Change create engine line in your __init__.py and Database_set_Finalprject.py to: engine = create_engine('postgresql://Item_catalog-:password@localhost/Item_catalog-')
python /var/www/Item_catalog-/Item_catalog-/Database_set_Finalproject.py

Make sure no remote connections to the database are allowed. Check if the contents of this file sudo nano /etc/postgresql/9.3/main/pg_hba.conf looks like this:
local   all             postgres                                peer
local   all             all                                     peer
host    all             all             127.0.0.1/32            md5
host    all             all             ::1/128                 md5
Restart Apache
sudo service apache2 restart
