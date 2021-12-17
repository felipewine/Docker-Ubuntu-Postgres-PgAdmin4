# Docker-Ubuntu-Postgres-PgAdmin4

# Table of Contents

● [Installing Ubuntu on Docker](#installingubuntu)<br/>
&emsp;◌ [Pull a Base Image](#pullubuntuimage)<br/>

## Installing Ubuntu on Docker <a name="installingubuntu"></a>

### Pull a Base Image <a name="pullubuntuimage"></a>

Before creating a Linux container, you need to pull a base image from Docker’s repository. Open a PowerShell or command prompt and use the following command to pull the latest Ubuntu base image from the repository:

**_docker pull ubuntu_**

<img src="https://user-images.githubusercontent.com/69978184/146469360-95744a7c-6795-4005-a1cd-f27981eacbd2.png" width="600" height="400"/>

If you wanna remove the image just check the Image ID, and then remove it by executing the command "docker rmi <your-image-id>"

Using the above command will pull the latest available version of Ubuntu from the repository. If you want to pull a specific version of Ubuntu, use a tag as shown here:

**_docker pull ubuntu:18.04_**

If you want to search the repository for Ubuntu images, use search as shown below:

**_docker search ubuntu_**

To list the available images on the local computer, including information about image size, image ID, and tags:

**_docker images_**
