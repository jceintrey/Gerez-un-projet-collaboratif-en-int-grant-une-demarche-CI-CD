# CI/CD Integration Summary

This project is based on a simple application called BobApp, built with Java Spring Boot for the backend and Angular for the frontend.
The application displays random jokes to the user.

The main objective of the project is to illustrate the use of a CI/CD pipeline in a simple full-stack application. It includes:

* A GitHub Action workflow that runs tests for both frontend and backend, and generates coverage artifacts

* A GitHub Action workflow that checks code quality using SonarCloud

* A GitHub Action workflow that builds and pushes Docker images to Docker Hub

A docker-compose.yml file is also provided for quick and easy deployment.

## Setup

Clone project:

> git clone <git@github.com>:jceintrey/Gerez-un-projet-collaboratif-en-int-grant-une-demarche-CI-CD.git

### Front-end

Go inside folder the front folder:

> cd front

Install dependencies:

> npm install

Launch Front-end:

> npm run start;

#### Build the front with Docker

Build the container:

> docker build -t bobapp-front .  

Start the container:

> docker run -p 8080:8080 --name bobapp-front -d bobapp-front

### Back-end

Go inside folder the back folder:

> cd back

Install dependencies:

> mvn clean install

Launch Back-end:

> mvn spring-boot:run

Launch the tests:

> mvn clean install

#### Build the back with Docker

Build the container:

> docker build -t bobapp-back .

Start the container:

> docker run -p 8080:8080 --name bobapp-back -d bobapp-back

### Run application with compose

In the root directory of the project

 > docker compose up -d

You will be able to access [bobApp](http://localhost:8088)

### images updates

Images are tagged with the commit hash. To use a new version, change tag version in docker-compose.yml and pull images again

```bash
docker compose down
docker compose pull
docker compose up -d
```

You can also use the latest tag to retrieve the latest image

## CICD pipelines

The project defines 3 pipelines with Github Actions:

* test code and generate coverage reports for both front and back - tests.yml
* verify code quality with sonar cloud - sonar.yml
* build and push images on Dockerhub - deploy.yml
