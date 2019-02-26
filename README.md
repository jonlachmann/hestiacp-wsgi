# Vesta CP - WSGI template

This files are meant to enable WSGI support on a Debian or Ubuntu.

 1. Install wsgi apache module
    ```
    ~$ sudo apt-get install libapache2-mod-wsgi-py3
    ~$ a2enmod wsgi
    ```

 2. Download wsgi template
    ```
    ~$ cd /usr/local/vesta/data/templates/web
    /web$ wget https://gitlab.com/neyder/vestacp-wsgi/-/archive/master/vestacp-wsgi-master.tar.gz \
       -O- | sudo tar xzvf - --strip-components=1
    ```

 3. Create new package or set wsgi as apache template in the existing package

 4. Add new user and assing him package with wsgi template

 5. Add new domain and check the result

## Hints

 - This is for Python3.

 - You should create a venv in private dir inside your web domain.

 - Your project should be alogside venv named as domain_name.
   ```
   private
   ├── name.domain.tld
   └── venv
   ```
 - wsgi.py script is inside PROJECTAPP directory
   ```
   private/
   └── name.domain.tld
       ├── manage.py
       └── PROJECTAPP
           └── wsgi.py
   ```

 - you can rename PROJECTAPP with

   ```
   ~$ sudo sed -i 's/PROJECTAPP/{change_this}/' conf/web/name.domain.tld.apache2.conf
   ~$ sudo sed -i 's/PROJECTAPP/{change_this}/' conf/web/name.domain.tld.apache2.ssl.conf
   ```

 - this was tested using a django project.
