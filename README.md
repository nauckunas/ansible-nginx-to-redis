# ansible-nginx-to-redis

Ansible playbook to deploy `Nginx` and `Redis` to `Centos 7` servers

Each request to `Nginx` increases count in `Redis` for each matching `User-Agent` string

## Requirements

- Ansible 2.9
- Python 2.7
- Centos 7
- User has to have sudo privileges on specified hosts

## Deployment

Servers can be configured in inventory file

All inventory hosts:
```sh
#!/bin/bash
TARGET_USER='test'
git clone https://github.com/nauckunas/ansible-nginx-to-redis.git
cd ansible-nginx-to-redis
ansible-playbook -u ${TARGET_USER} -i inventory/default webserver.yml
```


Non-inventory host:
```sh
#!/bin/bash
TARGET_HOST='10.0.0.69'
TARGET_USER='test'
git clone https://github.com/nauckunas/ansible-nginx-to-redis.git
cd ansible-nginx-to-redis
ansible-playbook -u ${TARGET_USER} -i ${TARGET_HOST}, webserver.yml
```

## Testing

```sh
$ curl http://10.0.0.69/
:1
$ curl http://10.0.0.69/any-path
:2
$ curl -H "User-agent: any-other" http://10.0.0.69/
:1
$ curl http://10.0.0.69/
:3
```