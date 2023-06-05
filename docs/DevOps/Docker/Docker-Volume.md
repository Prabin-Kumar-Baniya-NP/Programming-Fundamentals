# Docker Volume

- Docker Volume is a mechanism to persist the data of the containers.
- It lives outside of the container.

## Types of Volume

1. Host Volume
2. Anonymous Volume
3. Named Volume

### Host Volume

- Lives on the Docker File System
- Access from within the container
- Command: docker run -v /path/on/host:/path/in/container ......

### Anonymous Volume

- Docker handles to storage location, not the user
- Difficult to refer for multiple containers because we don't know the name and path for that volume.
- Command: docker run -v /path/in/container .....

### Named Volume

- It is like an anonymous volume which docker handles not the user.
- Just the difference is that we give name to that volume.
  Commands:
  To create the volume

```
docker volume create volume-name
```

To run that volume

```
docker run -v name:/path/in/container ...
```

### List of Commands for Docker Volume

To list volume

```
docker volume ls
```

To inspect the volume

```
docker volume inspect volume-name
```

To create volume

```
docker volume create volume-name
```

To remove volume

```
docker volume rm volume-name
```

## Adding volumes in the docker compose file

```
version: "3.8"

services:
    django:
        build: .
        container_name: django
        command: python manage.py runserver 0.0.0.0:8000
        volumes:
            - .:/usr/src/app
        ports:
            - "8000:8000"
        depends_on:
            - pgdb
    pgdb:
        image: postgres
        container_name: pgdb
        environment:
            - POSTGRES_DB=postgres
            - POSTGRES_USER=postgres
            - POSTGRES_PASSWORD=postgres
        volumes:
            - pgdata:/var/lib/postgresql/data

volumes:
    pgdata: 
```