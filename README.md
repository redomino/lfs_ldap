What is it?
===========

If you want to install Django LFS [http://www.getlfs.com/] with ldap support, you can fork this repository.

How to use it?
==============

* git clone https://github.com/filippo91/lfs_ldap.git
* cd lfs_ldap
* python bootstrap.py
* virtualenv --no-site-packages . 
* bin/buildout -v 
* Enter your database settings to lfs_project/settings.py 
* bin/django syncdb
* bin/django lfs_init
* bin/django collectstatic
* bin/django runserver

In lfs_project/settings.py comment or delete the default backend configuration and add the following code:

```
LDAP BACKEND SETTINGS

import ldap
from django_auth_ldap.config import LDAPSearch

INSERT YOUR LDAP SERVER URI 

AUTH_LDAP_SERVER_URI = "ldap://ldap.example.com"
AUTH_LDAP_BIND_DN = ""
AUTH_LDAP_BIND_PASSWORD = ""
AUTH_LDAP_USER_SEARCH = LDAPSearch("dc=example,dc=com",
            ldap.SCOPE_SUBTREE, "(uid=%(user)s)")
AUTHENTICATION_BACKENDS = (
            'django_auth_ldap.backend.LDAPBackend',
            'django.contrib.auth.backends.ModelBackend',
            )
            
ATTRIBUTE MAPPING EXAMPLE

AUTH_LDAP_USER_ATTR_MAP = {"username": "USERNAME", "last_name": "SN", "first_name": "FN", "email": "E-MAIL"}
```

Browse to http://localhost:8000

More Information
================

* http://pythonhosted.org/django-auth-ldap/index.html
* Official page <http://www.getlfs.com/>

Credits
=======

Many thanks to Filippo Projetto
