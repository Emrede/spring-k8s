# Spring Boot Hello World on Kubernetes with Jenkins CI/CD

## Overview
This repository contains a simple "Hello World" application built with Spring Boot. The application is containerized using Docker, orchestrated with Kubernetes, and automated using a Jenkins CI/CD pipeline.

## Prerequisites
- JDK 17
- Docker
- Kubernetes
- Jenkins

## Stages
Spring Boot: 
- Created a Spring Boot Hello World application by the use of Spring initializer: https://start.spring.io
- Added a controller class named HelloWorldController.java to the application directory.
- It is a REST controller that defines what happens when someone accesses the root URL (/). It returns a simple "Hello, World!" message. The @RestController and @GetMapping("/") annotations make this a REST endpoint accessible via a GET request to the root URL.
- Added web dependency into the build.gradle file.
- Then applicaiton is Dockerized and pushed to the docker hub with following commands: 
```
docker build -t spring-hello-world .
docker images
docker tag <image_id> emrede/spring-hello-world:latest
docker push emrede/spring-hello-world:latest
```
- Docker image names configured accordingly in k8s config files.
- Nginx ingress controller installed with: 
`kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.0.4/deploy/static/provider/cloud/deploy.yaml`
- To run locally on kubernetes basically run:
`kubectl apply -f k8s/`

- Then you can check if everything works correctly with following commands:
Check Pods: kubectl get pods
Check Services: kubectl get svc
Check Ingress: kubectl describe ingress hello-world-ingress

- Look for the "Address" field in the Ingress description to find out where your service can be accessed. If everything is set up correctly, you should be able to access your Spring Boot application via the ingress address. In this case it should be `localhost`

- Install ngrok for public access: ` brew install ngrok/ngrok/ngrok`
- Start a tunnel with `ngrok http 80`
- I have done this on my local and my app is accessible on: `https://b4e0-82-222-120-241.ngrok-free.app`