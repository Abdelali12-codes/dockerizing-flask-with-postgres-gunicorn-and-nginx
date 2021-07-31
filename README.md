## Dockerizing Flask with Postgres, Gunicorn, and Nginx

## How to install docker-compose on linux

1. sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

2. sudo chmod +x /usr/local/bin/docker-compose

## to use pgAdmin with postgresql follow the steps below:

1. pull the pgadmin image (docker pull dpage/pgadmin4 )
2. inspect the postgres container where your database is reside (docker inspect postgres -f "{{json .NetworkSettings.Networks }}")
3. take the ipadress of your postgres database container that is appear in the response of the above command
4. run the pgadmin container via this command:
   docker run \
   -p 8080:80 \
    -e PGADMIN_DEFAULT_EMAIL=abdelali@gmail.com \
    -e PGADMIN_DEFAULT_PASSWORD=abdelali \
    --name dev-pgadmin \
   -d dpage/pgadmin4
5. go to the browser and tap http://localhost
6. enter the email and the password you used in the step 4 (abdelali@gmail.com ....)
7. create new server and past the ipaddres of your postgres container in the host/ip adress input
8. for clarification (if you used -p 5423:5423 when you started your postgres database container you can only use localhost for the Host/ip addres)

9. for the port keep it as the default for the user name use the one you used when you created your postgres database container (if you did not set it type postgres) for the password use the one you set when you created your postgres envirnment

10. try to connect to it
