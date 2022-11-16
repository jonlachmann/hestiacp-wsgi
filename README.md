# Hestia CP - WSGI template

This files are meant to enable WSGI support on a Debian or Ubuntu.

 1. Install wsgi apache module
    ```
    ~$ sudo apt-get install libapache2-mod-wsgi-py3
    ~$ a2enmod wsgi
    ```

 2. Download wsgi template
    ```
    ~$ cd /usr/local/hestia/data/templates/web/
    /web$ wget https://github.com/jonlachmann/hestiacp-wsgi/archive/refs/heads/master.zip \
       -O- | sudo tar xzvf - --strip-components=1
    ```

 3. If multiple php versions are enabled, put the files in /usr/local/hestia/data/templates/web/apache2/php-fpm
 
 4. Create a new package or set wsgi as apache template in the existing package

 5. Add a new user and assing it a package with wsgi template

 6. Add a new domain and check the result

## Hints

 - This is for Python3.

 - Upgrade your mod_wsgi to 4.6 + (libapache2-mod-wsgi-py3 provides version 4.3)

 - You should create a venv in private dir inside your web domain.

 - Your project should be alogside venv named as app.
   ```
   private
   ├── app
   └── venv
   ```
 - wsgi.py script is inside the app directory

```
   private/
   └── app
       ├── manage.py
       └── wsgi.py
```

 - this was tested using a django project.
