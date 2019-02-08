All I have done to deploy an app to the web.

I have logged in to my virtualenv 
donlowed flask - Python3 - pip3

No issue so far. 

I have this directory 
/var/www/ includs : catalog and html

        /var/www/catalog includes--> catalog  & flaskapp.wsgi

                  


        
        
        /var/www/html : index.html  myapp.wsgi
                  myapp.wsgi :def application(environ, start_response):
                  status = '200 OK'
                  output = 'Hello Udacity!'

                  response_headers = [('Content-type', 'text/plain'), ('Content-Length', str(len(output)))]
                  start_response(status, response_headers)

                  return [output]


I also have this file: sudo nano /etc/apache2/sites-available/Item_catalog-.conf
        <VirtualHost *:80>
ServerName 54.201.251.44
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




Have to Change SSH port from 22 to 2200
Run sudo nano /etc/ssh/sshd_config
Change the port from 22 to 2200



I have done step by step actiosn from this site: https://www.digitalocean.com/community/tutorials/how-to-deploy-a-flask-application-on-an-ubuntu-vps#step-four-%E2%80%93-configure-and-enable-a-new-virtual-host



At the end I run the code: service apache2 reload in my terminal while I am connected to venv : (venv) vagrant@vagrant-ubuntu-trusty-64:/var/www/catalog/catalog$ service apache2 reload 
And I receive this message * Reloading web server apache2                                                                                       * 

HOWEVER, when I go to the http://52.89.36.246/ instead of seeting my __init_.py I see  Apache2 Ubuntu Default Page

also : sudo a2ensite catalog


Also when I try to connect SSH: ssh -i ~/.ssh/Users/alirezabeig/ root@52.89.36.246 : I receive this error _>Warning: Identity file /Users/alirezabeig/.ssh/Users/alirezabeig.rsa not accessible: No such file or directory.
root@52.89.36.246: Permission denied (publickey).
MY PWD is :/Users/alirezabeig/final project


Add user: 

Sudo adduser grader
password: qwerasdzx

One error I receive after running :  ssh grader@52.89.36.246 -p 2222  --> It times out! 

Create : To create the public and private SSH keys on the command-line:
mkdir ~/.ssh
chmod 700 ~/.ssh
ssh-keygen -t rsa

Where the public key is ---/home/vagrant/.ssh/Final_P.rsa

Where the error happens :
run this command : ssh -i ~/.ssh/Final_P.rsa root@52.89.36.246
Error:Permission denied (publickey).


