# Deploying Java Spring Boot Microservices using Docker on AWS(Guide in progress is not complete yet)

This guide has step by step explanations of  deploying Java Spring Boot projects using Docker on AWS.

## Prerequisites, while this guide is mostly geared at windows uses i also include some commands for unix users


- An AWS account
- Docker Desktop for Windows installed
- AWS CLI installed

## Deployment Options

For this guide we will use AWS ECS(Elastic Container Services) to perform the deploy, also the containers can be hosted either on docker hub or amazon ecr(Elastic Container Registry)

 Amazon ECS is a service that lets you run Docker containers on a scalable cluster, and EC2 is  which is a service that provides virtual servers where you can install Docker 

## Deployment Steps

To deploy your Java Spring Boot project using Docker on AWS, follow these steps:

1. Create a Docker Compose file that defines your application and its dependencies.

2. Run the `docker compose up` command to build and test your application locally.

3. Run the `docker compose convert` command to convert your Compose file into an AWS CloudFormation template.

4. Run the `docker compose up --context ecs` command to deploy your application to ECS on Fargate.

5. Create a Dockerfile that defines how to build a custom Docker image for your Spring Boot application. You can use the openjdk base image and copy your jar file to the image. You can also specify an entrypoint that runs your jar file with `java -jar`.

For more information about deploying Java Spring Boot projects using Docker on AWS, see the following resources:

- [Amazon ECS documentation](https://docs.aws.amazon.com/ecs/index.html)
- [Amazon EC2 documentation](https://docs.aws.amazon.com/ec2/index.html)
- [Docker documentation](https://docs.docker.com/)
