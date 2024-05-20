# Django EC2 Deployment

## Django Setup

- Create an Server with Ubuntu Image.
- Allow TCP traffic to port 8000 in the security group.

- Check for python version

```
python3 --version
```

- Install pip

```
sudo apt update
sudo apt install python3-pip
```

- Clone the repository (https://github.com/Prabin-Kumar-Baniya-NP/Vaccination-Scheduling-App.git)

- Move to the repository and create a virtual environment
```
sudo apt install python3.10-venv
python3 -m venv env
```

- Then, activate the virtual environment
```
source env/bin/activate
```

- Install the dependencies

```
pip3 install -r requirements.txt
```

- Move to the project root (where manage.py file is located) and Create .env files and set the dubug to True and add a secret key.

- Open settings.py file and write * to the list of allowed host. It will allow all the ip address to host this application.

- Move to the project root directory and migrate the changes to SQlite Database.
```
python3 manage.py migrate
```

- Collect the static files.
```
python3 manage.py collectstatic
```

- Compile the .po files for Hindi language.

```
sudo apt install gettext
python3 manage.py compilemessages
```

- Check whether gunicorn is installed. If not, then install gunicorn.
```
pip3 install gunicorn
```

- Start the gunicorn workers.
```
gunicorn mysite.wsgi --bind 0.0.0.0:8000 --workers=2
```

## Setting up Gunicorn Web Server

- Create a gunicorn socket file
```
sudo nano /etc/systemd/system/gunicorn.socket
```
```
[Unit]
Description=gunicorn socket

[Socket]
ListenStream=/run/gunicorn.sock

[Install]
WantedBy=sockets.target
```

- Create a gunicorn service file

```
sudo nano /etc/systemd/system/gunicorn.service
```

```
[Unit]
Description=gunicorn daemon
Requires=gunicorn.socket
After=network.target

[Service]
User=ubuntu
Group=ubuntu
WorkingDirectory=/home/ubuntu/Vaccination-Scheduling-App/mysite/
ExecStart=/home/ubuntu/Vaccination-Scheduling-App/env/bin/gunicorn mysite.wsgi:application --bind unix:/run/gunicorn.sock --workers 2

[Install]
WantedBy=multi-user.target
```

- Start the socket
```
sudo systemctl start gunicorn.socket
```

- Check the status of socket
```
sudo systemctl status gunicorn.socket
```

- Start the gunicorn service
```
sudo systemctl start gunicorn.service
```

- Check the status of gunicorn service
```
sudo systemctl status gunicorn.service
```
```
You will get to see something like this

Jun 19 03:22:00 ip-172-31-6-82.ap-south-1.compute.internal gunicorn[27584]: [2023-06-19 03:22:00 +0000] [27584] [INFO] Starting gunicorn 20.1.0
Jun 19 03:22:00 ip-172-31-6-82.ap-south-1.compute.internal gunicorn[27584]: [2023-06-19 03:22:00 +0000] [27584] [INFO] Listening at: unix:/run/gunicorn.sock (27584)
Jun 19 03:22:00 ip-172-31-6-82.ap-south-1.compute.internal gunicorn[27584]: [2023-06-19 03:22:00 +0000] [27584] [INFO] Using worker: sync
Jun 19 03:22:00 ip-172-31-6-82.ap-south-1.compute.internal gunicorn[27585]: [2023-06-19 03:22:00 +0000] [27585] [INFO] Booting worker with pid: 27585
Jun 19 03:22:00 ip-172-31-6-82.ap-south-1.compute.internal gunicorn[27586]: [2023-06-19 03:22:00 +0000] [27586] [INFO] Booting worker with pid: 27586
```

## Setting up Nginx

- Install nginx
```
sudo apt install nginx
```
- Check the status of nginx, if its inactive, start it
```
sudo systemctl status nginx
sudo systemctl start nginx
```
- Move to sites available directory
```
sudo cd /etc/nginx/sites-available/
```

- Delete the default file

- Move to sites enabled directory
```
sudo cd /etc/nginx/sites-enabled/
```

- Delete the default file

- Now, move to sites-available folder and Create a file named django
```
sudo nano /etc/nginx/sites-available/django
```

```
server {
    listen 80;

    location / {
        proxy_pass http://unix:/run/gunicorn.sock;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

- Now, activate the configuration
```
sudo ln -s /etc/nginx/sites-available/django /etc/nginx/sites-enabled
```

- Restart nginx
```
sudo systemctl restart nginx
```

## Static files via Nginx

- Generate a secret key

```
python manage.py shell
>>> from django.core.management.utils import get_random_secret_key
>>> get_random_secret_key()
```

- Add the secret key to the .env file
- Set debug to False in .env file

- Restart the gunicorn service

[Test the app in private mode]

- To serve static files by nginx, open /etc/nginx/sites-available/django and add

```
location /static/ {
        alias /home/ubuntu/Vaccination-Scheduling-App/mysite/staticfiles/;
    }
```

[Nginx will throw 403 Forbidden on serving files]

- Open nginx.conf (from /etc/nginx/) and change the user

```
user ubuntu;
```

[Check whether nginx can serve the static files]

Also restart nginx
```
sudo systemctl restart nginx
```

## Media files via Nginx

- To serve media files by nginx, open /etc/nginx/sites-available/django and add

```
location /media/ {
        alias /home/ubuntu/Vaccination-Scheduling-App/mysite/media/;
}
```
Also restart nginx
```
sudo systemctl restart nginx
```

## Configure Email Backend

Add this in settings.py file

```py
EMAIL_BACKEND = "django.core.mail.backends.smtp.EmailBackend"

EMAIL_USE_TLS = True
EMAIL_HOST = ""
EMAIL_PORT = "" 
EMAIL_HOST_USER = ""  
EMAIL_HOST_PASSWORD = "" 
```
in the email.py file, add the from value
```py
email = EmailMessage(subject, message, to=[to_email], from_email=EMAIL_HOST_USER)
```

## Securing the website via HTTPS [Incompleted]

Install certbot
```
sudo apt install certbot python3-certbot-nginx
```

Open /etc/nginx/sites-available/django and then add server name
```
server_name prabinkumarbaniya.tech www.prabinkumarbaniya.tech;
```

```
A Record - For IPv4
AAA Record - For IPv6
CNAME - it point to another host. Example: www.prabinkumarbaniya.tech can have cname record prabinkumarbaniya.tech

```
