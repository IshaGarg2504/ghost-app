# ghost-app
Ghost-application

### Prerequisites :
1. Latest version of docker-compose installed
2. openssl installed

To launch the application, follow below steps:
1. Clone/Download the code in your local
2. run "docker-compose up"

## **Ghost-app Functioning:**
Application involves 3 services:
- **Backend : MySQL**
- **Application : Ghost-app**
- **Webserver : NGINX**

- Firstly, MySQL container starts. Make sure to use the username and password to login to mysql DB as mentioned in compose file.
To make the data persistent we will use a named Docker volume called "mysql-volume". The data from /var/lib/mysql (path inside our MySQL container) will be mounted in the volume.

- Ghost service starts after mysql only. Ghost will use this DB to connect with the MySQL container. 
There is a script file under ghost folder "wait-for-it.sh". Ghost will use this script to check if the MySQL service inside the MySQL container is already running, before it will connect.
ghost  folder contains a Dockerfile and scriptfile "wait-for-it.sh". 
Ghost service use this Dockerfile to build the ghost image.
To make the data persistent we will use a named Docker volume called "ghost-volume". The data from /var/lib/ghost/content (path inside our Ghost container) will be mounted in the volume.

- Lastly, We are using NGINX webserver. We are using cutom NGINX configuration "default.conf" which are stored in nginx folder with a Dockerfile to use the custom configuration while building NGINX image.
Custom NGINX configuration includes foloowing:
  1. Enable HTTPS and redirect HTTP to HTTPS
  2. Creation of self-signed certificates with the help of following command :
     **openssl req -x509 -nodes -days 365 -newkey rsa:4096 -keyout nginx-selfsigned.key -out nginx-selfsigned.crt**

  3. Generate a DH key and enable dhparam with the help of following command :
       **openssl dhparam -out dhparam.pem 2048**

  4. Enable HSTS

All the newly created certificates and keys are stored in "/etc/selfsign" for this project and we are using mount volume from the same path in docker-compose.yml

To access the NGINX container from outside world, Make sure to map host port (80/443) with container port (80/443)

To run the app Use :
          **docker-compose up**
Check if all the 3 containers are running, use **docker ps**

If all the containers are runnig, Browse the application on browser using
        **http://HOSTIP>**
 

