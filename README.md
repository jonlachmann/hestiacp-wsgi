# Hestia CP - WSGI template

This files are meant to enable WSGI support on a Debian or Ubuntu.

 1. Install wsgi apache module
    ```
    ~$ sudo apt-get install libapache2-mod-wsgi-py3
    ~$ a2enmod wsgi
    ```

 2. Download wsgi template
    ```
    
    ~$ wget https://github.com/jonlachmann/hestiacp-wsgi/archive/refs/heads/master.zip
    ~$ unzip master.zip
    ~$ sudo cp hestiacp-wsgi-master/apache2/* /usr/local/hestia/data/templates/web/apache2/
    ```

 3. If multiple php versions are enabled, put the files in /usr/local/hestia/data/templates/web/apache2/php-fpm/ instead.
 
 4. Create a new package or set wsgi as apache template in the existing package.

 5. Add a new user and assing it a package with wsgi template.

 6. Add a new domain and check the result.

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
 - wsgi.py script should be inside the app directory, you can create a symlink if it is stored elsewhere. 

```
   private/
   └── app
       ├── manage.py
       └── wsgi.py
```

 - this was tested using a django project, the wsgi.py file had to be modified as below.

```
"""
WSGI config for appname project.

It exposes the WSGI callable as a module-level variable named ``application``.

For more information on this file, see
https://docs.djangoproject.com/en/3.2/howto/deployment/wsgi/
"""

import os
import sys

path = '/home/USERNAME/web/DOMAIN/private/app'
if path not in sys.path:
    sys.path.insert(0, path)

from django.core.wsgi import get_wsgi_application

os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'appname.settings')

application = get_wsgi_application()
```
