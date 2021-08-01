## create service

[Unit]
Description=gunicorn demo service
After=network.target
StartLimitIntervalSec=0
Requires=gunicorn.socket

[Service]

- User=abdelali
- Group=abdelali
- WorkingDirectory=/home/abdelali/flask-gunicorn/
- #ExecStart=/home/abdelali/flask-gunicorn/env/bin/gunicorn --workers 3 --bind unix:/home/\* abdelali/flask-gunicorn/flask-gunicorn.sock app:app
- ExecStart=/home/abdelali/flask-gunicorn/env/bin/gunicorn app
  [Install]

WantedBy=multi-user.target

## create unix socket

[Unit]

- Description=gunicorn socket

[Socket]

- ListenStream=/run/gunicorn.sock
- Our service won't need permissions for the socket, since it
- inherits the file descriptor by socket activation
- only the nginx daemon will need access to the socket
- for the linux the default user is nginx for debain is www-data so make sure which distro are using and look for the default user in it
  SocketUser=nginx
- Optionally restrict the socket permissions even more.
- SocketMode=600

[Install]

- WantedBy=sockets.target

## configure nginx

server {
listen 8000;
server_name 127.0.0.1;
location / {
proxy_pass http://unix:/run/gunicorn.sock;
}
}
