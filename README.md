Peertube
=========

This role intalls Peertube, a video-sharing website, from https://github.com/Chocobozzz/PeerTube.

Requirements
------------

This role requires role yedit, to modify yaml files, from https://github.com/kwoodson/yedit.git.

Role Variables
--------------

Domain name where Peertube will be accessible from.

```
peertube_tld: localhost
```

Version of Peertube to download from official git repository.
```
peertube_version: v1.0.0-beta.3
```

Path where to install Peertube.
```
peertube_user_path: /var/www/peertube
```

Set if https is handled by a reverse proxy instead of this nginx server. It
will be used to remove the certbot configuration phase, and remove https from
nginx configuration.
```
peertube_proxy_handle_https: no
```

List of IPs used by optional reverse proxy. For example, it can be set to `[10.0.0.1, 10.0.0.2]`.
```
peertube_proxy_ips: []
```

Password for database. Default value is automatically calculated, and stored in `credentials/peertube/db-$hostname`
```
peertube_dbuser_password: "{{ lookup('password', 'credentials/peertube/db-' + inventory_hostname) }}"
```

Password for peertube user. Default value is automatically calculated, and stored in `credentials/peertube/user-$hostname`
```
peertube_user_password_hashed: "{{ lookup('password', 'credentials/peertube/user-' + inventory_hostname) |password_hash('sha512') }}"
```

Password for admin access to website. Default value is automatically calculated, and stored in `credentials/peertube/web-admin-$hostname`
```
peertube_web_admin_password: "{{ lookup('password', 'credentials/peertube/web-admin-' + inventory_hostname) }}"
```

Dependencies
------------

None

Example Playbook
----------------

    - name: peertube configuration
      hosts: peertube
      become: yes
      roles:
        - lib_yaml_editor
        - ansible-peertube

License
-------

MIT
