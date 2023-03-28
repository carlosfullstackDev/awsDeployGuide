# Deploying Java Spring Boot Microservices using Docker on AWS

This guide has step by step explanations of  deploying Java Spring Boot projects using Docker on AWS.

## Prerequisites


- An AWS account
- Docker Desktop for Windows installed
- AWS CLI installed
- Java 8+ installed
- Maven
- Docker hub account

## Deployment Options

For this guide we will use AWS ECS(Elastic Container Services) to perform the deploy, also the containers can be hosted either on docker hub or amazon ecr(Elastic Container Registry)

 Amazon ECS is a service that lets you run Docker containers on a scalable cluster, and EC2 is  which is a service that provides virtual servers where you can install Docker 

## Deployment Steps

To deploy your Java Spring Boot project using Docker on AWS, follow these steps:
• Before starting use mvn package command to create the jar in spring boot



•	Create a Dockerfile that defines how to build a custom Docker image for your Spring Boot application. You can use the openjdk base image and copy your jar file to the image. You can also specify an entrypoint that runs your jar file with java -jar command. For example:

```
FROM openjdk:11
COPY target/*.jar app.jar
ENTRYPOINT ["java", "-jar", "/app.jar"]
```

• Build the Docker Image using:

```
docker build --tag=TagName dir
```
 
 where:
- -t is to mention a tag to the image
- ImageName is the name of the image you want to create
-	TagName is the name of the tag you want to assign to the image
-	dir is the directory where your dockerfile and other files are located

 
 -	Create a docker-compose.yml file that defines how to run your Spring Boot application as a Docker service. You can use the image name that you created in the previous step and specify any ports or environment variables that you need. For example:

```
version: '3'
services:
  app:
    image: spring-boot-app
    ports:
      - "8080:8080"
    environment:
      - SPRING_PROFILES_ACTIVE=dev
```
      
      
      
	Run your docker compose file using docker-compose up command. This will start your Spring Boot application as a Docker container and expose port 8080 on the host machine.


In docker desktop you will be able to see the container running 

![image](https://user-images.githubusercontent.com/127157564/228364743-25cf773b-977e-4cd2-b434-d45d3d399a9d.png)


## Pushing to dockerhub

Once that you have the container created its time to push to dockerhub, and you need to do the following:

- in the CLI authenticate using your dockerhub credentials
- Based on the first steps of the readme its assumed that the image was built on your local and its ready to push
- push the image with the following command

```
 docker push <username>/<reponame>:<tagname>
```

## Bringing the container to AWS

-	Create a task definition that specifies how to run your container, such as the image name, port mappings, memory and CPU requirements, etc.
- 	Create a cluster that defines the compute resources for running your tasks. You can choose between ECS on EC2 or Fargate as the launch type for your cluster. EC2 allows you to have more control over your instances, while Fargate is serverless and abstracts away the underlying infrastructure, in this guide EC2 was chosen
-	Create a service that defines how many tasks you want to run and how they should be distributed across your cluster. You can also configure load balancing, health checks, scaling policies, etc. for your service.
- SSH into your EC2 created instance
- Run this commands to install the latest updates in your instance(This is only needed for first time)

```
sudo yum update -y
sudo yum install docker -y
sudo service docker start
```

- Run the docker container
```
sudo docker run -d -p 80:801 dockerhubusername/dockerhubrepoimagename:latest

```

- To test that the container works perform a REST request using a tool like postman, swagger or ReadyAPI, alternatively you can run the CURL command in your terminal



For more information about deploying Java Spring Boot projects using Docker on AWS, see the following resources:

- [Amazon ECS documentation](https://docs.aws.amazon.com/ecs/index.html)
- [Amazon EC2 documentation](https://docs.aws.amazon.com/ec2/index.html)
- [Docker documentation](https://docs.docker.com/)
