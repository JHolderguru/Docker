# Docker is a microservice architecture

### Docker registries - Contains Docker images (public and Pvt)

### Docker Images - read only images used to create containers(built by Docker users)

### Docker - run time instances of docker Images (a container can have more than one image)

## Getting set up
```ubuntu
sudo - apt update
```
## Install Docker
```ubuntu
sudo apt install docker.io
```
## Start and automate Docker
```ubuntu
sudo systemctl start docker
sudo systemctl enable docker
```
## Pulling an Image from Docker
```ubuntu
sudo docker pull centos
```
## The image is pulled and you can run it
```ubuntu
sudo docker run -it centos
```

# Docker Compose File
### We can multiple images in one container with one single command, I will demonstrate
using wordpress, mysql and PHPmyadmin (used to access mysql database ).

### Prereq python pip
```ubuntu
sudo apt-get install python-pip
```
### Install docker compose
```ubuntu
sudo pip install docker-compose
```
### Next I will make a wordpress directory
```ubuntu
mkdir wordpress

sudo gedit docker-compose.yml
```
#### So far I have defined a container and I have named it as word wordpress it is built from image wordpress
#### which is on the dockerhub but it does not have a database and for that I have defined
#### one more container and defined it as wordpress_db.It is built from the image mariaDB which is on the word wordpress
#### At this point we link the two together then define a password. Lastly I will build one more image PHPmyadmin from the image
#### corbinu/docker-PHPmyadmin. This is linked to wordpress_db:mysql.
```yml
wordpress:
  image: wordpress_db
  links:
    -wordpress_db:mysql
  ports:
    -8080:80
wordpress_db
  image: mariadb
  environment:
    MYSQL_ROOT_PASSWORD: password123
phpmyadmin:
  image: corbinu/docker-PHPmyadminlinks:
  links:
    - wordpress_db:mysql
  ports:
   - 8181:80
  environment:
    MYSQL_USERNAME: root
    MYSQL_ROOT_PASSWORD: password123

```    

#### save it and go back to the terminal and runt eh command to pull all 3 images and build the 3 containers

```ubuntu
sudo docker-compose up -d

```

#### open browser and go to the local port
#### localhost:8080 and it should direct to the wordpress and fill in the form
#### click install wordpress and it should take you to the dashboard
#### open another tab and and the localhost:8181 for my PHPmyadmin and user and password as stated above.
#### PHPmyadmin is installed this is use to access mysql database.
