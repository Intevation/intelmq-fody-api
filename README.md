# Documentation

Each contained module has an additional `README.md` to follow.

# Requirements
 * hug
 * psycopg2 >=2.4.5
 * intelmq-mailgen
 * python-dateutil
 * typing
 * postgresql v>=9.5

# License
This software is Free Software available under the terms of
the AGPL v3 or later versions of this license.
See the file `agpl-3.0.txt` or https://www.gnu.org/licenses/agpl-3.0.en.html
for details.

# Operating manual

Because of https://github.com/Intevation/intelmq-fody-backend/issues/12
make sure to restart the serving process(es) each time you have
restarted postgresql.

## Run with hug
```
hug -f intelmq_fody_backend/serve.py -p 8002
```


## Run with Apache and WSGI
```
#as root
apt-get install libapache2-mod-wsgi-py3
```

You might want to use an Apache-Config similar to the example included as
[config/apache-example/001-fody.conf](config/apache-example/001-fody.conf)

# Track db changes by user
Only the module `contactdb_api` exposes the ability to write changes to the db.

If you want to be able to find out which user did which particular change:
 1. Use basic authentication and maintain one userid and password per user.
    (For apache2 this can be done with the `htpasswd` tool.)
 2. Keep logs of the wsgi application at least at the INFO level.

Log entries will show the requested change
together with the authenticated userid, search for
`remote_user =`. Example for apache2:

```sh
pushd /var/log/apache2/
grep 'remote_user =' *
error.log:[Fri May 05 14:19:26.882299 2017] [:error] [pid 2075] 2017-05-05 14:19:26,882 contactdb_api.contactdb_api.serve INFO - Got commit_object = {'orgs': [{'comment': 'Testing', 'first_handle': '', 'name': 'Intevation', 'sector_id': None, 'contacts': [], 'ti_handle': '', 'ripe_org_hdl': '', 'asns': []}], 'commands': ['create']}; remote_user = 'bernhard.reiter'
error.log:[Fri May 05 14:19:26.882299 2017] [:error] [pid 2075] 2017-05-05 14:19274,179 contactdb_api.contactdb_api.serve INFO - Commit successful, results = [('create', 126)]; remote_user = 'bernhard.reiter'
```


# Development

## Origin
Most of the files within this repository originated from:
https://github.com/Intevation/intelmq-mailgen/tree/master/extras
