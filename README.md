README.md
=========

This README provides instructions on how to deploy and run a Docker container on your local machine using an Ansible script. This setup assumes you have Docker installed on your local machine and properly configured.

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
				sudo snap install docker
				docker --version
				
				GITHUB_REPO="https://$USERNAME:$PASSWORD@https://github.com/newstartao/swf-eureka-server.git"
				CONTAINER_NAME="swf-eureka-server"
				IMAGE_NAME="swf-eureka-server-images"
				DOCKERFILE_PATH="path/to/Dockerfile"
				
				git clone $GITHUB_REPO
				cd swf-eureka-server
				docker build -t swf-eureka-server-image .
				docker run -itd --name $CONTAINER_NAME swf-eureka-server-images /bin/bash
				if [ "$(docker ps -q -f name=$CONTAINER_NAME)" ]; then
				  echo "Container $CONTAINER_NAME is running."
				else
				  echo "Failed to start container $CONTAINER_NAME."
				fi
				
				EOT


### Running the shell Script

#### Make it execute permissions and run the shell script using the following command:

chmod +x deploy.sh

USERNAME= **user_name** PASSWORD= **user_token** ./deploy.sh 
	* Edit user_name and user_token


			


