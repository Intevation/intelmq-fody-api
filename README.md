
# Requirements
 * hug
 * psycopg2
 * intelmq-mailgen
 * python-dateutil

# License
This software is available under the terms of the AGPL v3 or later versions of this license.
See the file `agpl-3.0.txt` or https://www.gnu.org/licenses/agpl-3.0.en.html
for details.

# Run with hug
```
hug -f intelmq_api/serve.py -p 8002
```


# Run with Apache and WSGI



```
#as root
apt-get install libapache2-mod-wsgi-py3
```

You might want to use an Apache-Config like:

```
<VirtualHost *:8000>
        ServerAdmin webmaster@localhost
        DocumentRoot /opt/src/intelmq-api/intelmq_api

        WSGIDaemonProcess fody threads=1 maximum-requests=10000
        WSGIScriptAlias / /opt/src/intelmq-api/intelmq_api/serve.py
        WSGICallableObject __hug_wsgi__

        <Directory /opt/src/intelmq-api/intelmq_api>
            Options FollowSymLinks
            AuthType Basic
            AuthName IntelMQ
            AuthBasicProvider file
            AuthUserFile "/etc/intelmq-manager.htusers"
            Require valid-user
        </Directory>

        ErrorLog ${APACHE_LOG_DIR}/fody-error.log
        CustomLog ${APACHE_LOG_DIR}/fody-access.log combined
</VirtualHost>

```

## Origin
Most of the files within this repository originated from:
https://github.com/Intevation/intelmq-mailgen/tree/master/extras