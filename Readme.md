# Bookstack using kubernetes and docker-compose
## Bookstack using kubernetes

### Config

First step is to set environment variables. You can use secrets if you prefer. I recommend it.

If you have more than one service you can use an ingress.
You have available the configuration in the branch with-ingress.

You can set an external static IP in bookstack service with the next parameter:

```
type: LoadBalancer
loadBalancerIP: xx.xx.xx.xx
```

#### Volumes
Since mysql 5.7 if u mount a persistence volume in /var/lib/mysql, mysql return you an error, you must added to mysql deployment just the next argument:

```
args:
  - "--ignore-db-dir=lost+found"
```

Mysql Volume:
```
volumeMounts:
    - mountPath: /var/lib/mysql
    name: mysql-data
```

Bookstack Volumes:
```
volumeMounts:
    - mountPath: /var/www/bookstack/public/uploads
    name: bookstack-uploads
    - mountPath: /var/www/bookstack/public/storage
    name: bookstack-storage
```

## Bookstack using docker-compose

You can change the routes of volumes, ports and environment variables as you wish.


Execute the next command to start docker-compose:

```
$ docker-compose up -d
```

## Bookstack default user

Default user: admin@admin.com \
Default pass: password

* You should delete default admin user and disabled guest user for security reasons.