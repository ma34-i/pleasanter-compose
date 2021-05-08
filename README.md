# pleasanter-compose
pleasanter on Docker(docker-compose)

## how to run
1. `docker-compose up -d`
2. exec command (for the first time only)
```
docker exec pleasanter-app /tmp/init.sh
```
3. Access `http://hostname:80`

## reference
- https://pleasanter.org/manual/install-centos8-postgresql