README.md
=========

This README provides instructions on how to deploy and run a Docker container on your local machine using an shell script. This setup assumes you have Docker installed on your local machine and properly configured.

## Table of Contents:

* Prerequisites
* Running the shell Script

### Prerequisites

To deploy and create a Docker container on your local machine from a GitHub repository, you can create a shell script that automates the process.

#### Create the shell script using the following command:

	cat << EOT > deploy.sh
	#! /bin/bash
	
	sudo apt-get update
	sudo apt-get install docker.io -y
	docker --version
	
	CONTAINER_NAME="swf-eureka-server"
	IMAGE_NAME="ghcr.io/newstartao/swf-eureka-server-main:latest"
	
	echo "$PASSWORD | docker login ghcr.io -u $USERNAME --password-stdin"
	docker pull $IMAGE_NAME
	docker logout ghcr.io
	docker images
	
	docker run -itd --name $CONTAINER_NAME $IMAGE_NAME /bin/bash
	if [ "(docker ps -f name=$CONTAINER_NAME)" ]; then
	  echo
	  docker ps
	  echo
	  echo "Container  is running."
	  echo
	else
	  echo "Failed to start container ."
	fi		
	EOT

### Running the shell Script

##### Make it execute permissions:

	chmod +x deploy.sh
##### Edit your user_name and user_token and run the shell script using the following command:
	USERNAME=user_name PASSWORD=user_token ./deploy.sh


			


