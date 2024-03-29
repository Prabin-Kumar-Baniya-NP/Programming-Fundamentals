# Docker Compose Example for Django with Redis and Celery

Dockerfile
```
FROM python:3
ENV PYTHONUNBUFFERED=1
WORKDIR /usr/src/app
COPY requirements.txt ./
RUN pip install -r requirements.txt
```

docker-compose.yml
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
        environment:
            - DEBUG=1
            - DJANGO_ALLOWED_HOST=localhost 127.0.0.1
            - CELERY_BROKER=redis://redis:6379/0
            - CELERY_BACKEND=redis://redis:6379/0
        depends_on:
            - pgdb
            - redis
    celery:
        build: .
        command: celery -A core worker -l INFO
        volumes:
            - .:/usr/src/app
        depends_on:
            - django
            - redis
    pgdb:
        image: postgres
        container_name: pgdb
        environment:
            - POSTGRES_DB=postgres
            - POSTGRES_USER=postgres
            - POSTGRES_PASSWORD=postgres
        volumes:
            - pgdata:/var/lib/postgresql/data
    redis:
        image: "redis:alpine"

volumes:
    pgdata: 


```