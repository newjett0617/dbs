# docker-compose-template

```
cp .env.example .env
```

edit .env

```
docker network create --driver=bridge pgsql
docker volume create --driver=local pgsql_data
```

```
docker-compose up -d
```

## connection
```shell
docker exec -i -t pgsql psql --username=postgres
```

## init user and database
```shell
#!/usr/bin/env sh

username=username
password=password
database=database
docker exec pgsql psql \
  --username=postgres \
  --variable=ON_ERROR_STOP=1 \
  --command="CREATE USER ${username} WITH PASSWORD '${password}';" \
  --command="CREATE DATABASE ${database};" \
  --command="GRANT ALL PRIVILEGES ON DATABASE ${database} TO ${username};";
```
