# Docker Compose With Django

## Dockerfile setup
Create a new file named "Dockerfile".

Grab the python 3 image
```
FROM python:3
```

To output the python result to terminal
```
ENV PYTHONUNBUFFERED=1
```

Set the working directory
```
WORKDIR /usr/src/app
```

Copy the requirements.txt file from current directory to the working directory
```
COPY requirements.txt ./
```

Run the command in the working directory
```
RUN pip install -r requirements.txt
```

## Docker compose setup

Docker compose allows us to run multi container application in a network.

Create a file named "docker-compose.yml"

Give the version of docker compose engine
```
version: "3.8"
```
### Django Service

To create a new service / container to use and give a name as django
```
services:
    django:
```

To build the docker file we we created where we used python image.
```
build: .
```

To name the container
```
container_name: django
```

To run the command on the container
```
command: python manage.py runserver 0.0.0.0:8000
```

To define the volume for the container
```
volumes:
    - .:/usr/src/app
```

To map the port of our machine to conatiner port
```
ports:
    - "8000:8000"
```

Write the dependency for this container
```
depends_on:
    - pgdb
```

### Postgres Service

Create a new service
```
pgdb:
```

Write the image of this service
```
image: postgres
```
This will pull postgres image from dockerhub

Give the container name for this service
```
container_name: pgdb
```

## Running the docker compose

```
docker-compose run django django-admin startproject core .
```
This command runs the django service and after the container is build, it executes "<b>django-admin startproject core .</b>" command. 

You might have got error on running django.

Change Allowed Host in settings.py file
```
ALLOWED_HOSTS = ["*"]
```

Now, delete the container which is created.

After that, run this command to start your container
```
docker compose up
```

To execute some commands in django container, open bash in that container
```
docker exec -it django bash
```
Here, -it means interactive terminal

Now run the migrations
```
python manage.py migrate
```

To execute some commands without logging into django container
```
docker-compose run django python manage.py migrate
```

To connect to the postgres database
```
docker exec -it pgdb psql -U postgres
```
This command will connect to the pgdb container in interactive terminal mode (-it) and then execute psql-U postgres command to login as the postgres user.


Now configure the postgres db into django.

Add DB Configuration
```
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'postgres',
        'USER': 'postgres',
        'PASSWORD': 'postgres',
        'HOST': 'pgdb',
        'PORT': 5432,
    }
}
```
HOST value is pgdb. pgdb is the container name.

Run this command
```
docker-compose down
```
It will stop and remove the container.

Then run the command
```
docker-compose up
```


