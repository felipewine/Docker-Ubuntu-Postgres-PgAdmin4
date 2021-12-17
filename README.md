# Docker-Postgres-PgAdmin4

# Table of Contents

● [Installing Postgres and PgAdmin4 from yaml file](#installingpostgres)<br/>
<!-- 
● [Installing Docker Ubuntu on Windows](#installingubuntu)<br/>
&emsp;◌ [Pull a Base Image](#pullubuntuimage)<br/>
&emsp;◌ [Create a New Linux Container](#creatinganewlinux)<br/>

## Installing Docker Ubuntu on Windows <a name="installingubuntu"></a>

### Pull a Base Image <a name="pullubuntuimage"></a>

Before creating a Linux container, you need to pull a base image from Docker’s repository. Open a PowerShell or command prompt and use the following command to pull the latest Ubuntu base image from the repository:

**_docker pull ubuntu_**

<img src="https://user-images.githubusercontent.com/69978184/146469360-95744a7c-6795-4005-a1cd-f27981eacbd2.png" width="600" height="400"/>

If you wanna remove the image just check the Image ID with docker images, and then remove it by executing the command "docker rmi <your-image-id>"</a>

**_docker rmi <your-image-id>_**

<img src="https://user-images.githubusercontent.com/69978184/146469898-142e11eb-a0b9-4cd3-810f-9aa4741cf4fa.png" width="600" height="400"/>

<img src="https://user-images.githubusercontent.com/69978184/146470340-02a0dabc-2cdf-434f-b959-57e44d60f9ab.png" width="600" height="400"/>

Using the above command will pull the latest available version of Ubuntu from the repository. If you want to pull a specific version of Ubuntu, use a tag as shown here:

**_docker pull ubuntu:18.04_**
 
<img src="https://user-images.githubusercontent.com/69978184/146472583-763510dd-3a9a-42ce-96a7-b59db6455a90.png" width="600" height="400"/>

If you want to search the repository for Ubuntu images, use search as shown below:

**_docker search ubuntu_**

To list the available images on the local computer, including information about image size, image ID, and tags:

**_docker images_**

### Create a New Linux Container <a name="creatinganewlinux"></a>

To create a new Linux container, we need the ID of the base image and the docker run command. In the command below, I’ve used the image ID for the latest version of Ubuntu in my local repository, and the bash terminal will launch once the container has started:
 
docker run -i -t cd6d8154f1e1 /bin/bash

<img src="https://user-images.githubusercontent.com/69978184/146474096-8962ea54-4629-42c8-aa0c-97edefcac4d0.png" width="600" height="400"/>

The -i and -t parameters allow the bash process to start in the container, attaches the console to the process’s standard input, output, and standard error, and allocates a pseudo-tty text-only console. Once the container has been created, you’ll be presented with a bash prompt. Type hostname and press ENTER to see the container’s Linux hostname. You can stop the container at any time by typing exit and pressing ENTER. Exiting a container stops it from running.
-->

## Installing Postgres and PgAdmin4 from yaml file <a name="installingpostgres"></a>

To set up our environment, we'll use a Docker compose file and .json file as well, we name both as docker-compose.yml and servers.json inside a folder

**docker-compose.yml_**

     version: '3.8'
     services:
       db:
         container_name: pg_container
         image: postgres
         restart: always
         environment:
           POSTGRES_USER: root
           POSTGRES_PASSWORD: root
           POSTGRES_DB: test_db
         ports:
           - "15432:5432"
       pgadmin:
         container_name: pgadmin4_container
         image: dpage/pgadmin4
         restart: always
         environment:
           PGADMIN_DEFAULT_EMAIL: admin@admin.com
           PGADMIN_DEFAULT_PASSWORD: root
         ports:
           - "5050:80"
         volumes:
            - ./servers.json:/pgadmin4/servers.json # preconfigured servers/connections
            - ./pgpass:/pgpass # passwords for the connections in this file

**_servers.json_**
 
      {
        "Servers": {
          "1": {
            "Name": "docker_postgres",
            "Group": "docker_postgres_group",
            "Host": "host.docker.internal",
            "Port": 15432,
            "MaintenanceDB": "postgres",
            "Username": "postgres",
            "PassFile": "/pgpass",
            "SSLMode": "prefer"
       }
     }
   }


 
<!-- https://petri.com/docker-for-windows-create-a-linux-container-on-windows-10
https://stackoverflow.com/questions/69293137/how-do-i-connect-to-host-docker-internal-postgres-instance
-->
