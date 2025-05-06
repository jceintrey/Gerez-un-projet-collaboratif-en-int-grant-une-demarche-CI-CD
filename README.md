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

## CI/CD pipelines & KPIs

The CI/CD pipeline is managed through GitHub Actions and consists of the steps bellow. Please notice all pipelines are executed on push or pr on main.

### Run tests (frontend and backend)

* Executes unit tests for both Angular and Spring Boot
* Generates code coverage reports
* Code quality analysis with SonarCloud

Test pipeline is defined in .github/workflows/tests.yml with 2 jobs (for front and for back).  Please notice the use of a Custom browser defined in karma.conf.js, running in headless mode.

### Performs static code analysis

* Detects bugs, code smells, and duplications with Sonar Cloud integration.

Quality pipeline is defined in .github/workflows/sonar.yml with 2 jobs (for front and for back). I have used github Action sonar pluggin that provides a nice integration with Github (PR comments, badges...).

### Build & Push Docker Images

* Builds Docker images for frontend and backend
* Tags images with the short Git commit hash
* Pushes images to Docker Hub with two tags: specific :sha and :latest

Deploy pipeline is defined in .github/workflows/deploy.yml with 2 jobs (for front and for back)

### Proposed KPIs

Sonar projects are configured in "Clean as you code" mode. The quality is evaluated on the new code lines.

| KPI  | Threshold          | Details |
| :--------------- |:---------------:| -----:|
| Code coverage  |  ≥ 80%        | /!\ only on new code |
| SonarCloud warnings  | < 10             |  .... |

### Metrics

Global backend and frontend observed metrics

| Metric          | Backend | Frontend |
|-----------------|---------|----------|
| Code Coverage   | 38.8%   | 47.6%    |
| Security Issues | 0       | 0        |
| Reliability     | 1       | 1        |
| Maintainability | 6       | 5        |
| Duplications    | 0%      | 0%       |

### User Feedback

#### Ideas

  > Bouton like : "Ça serait top d'avoir un bouton pour liker une blague" - jceintrey 06/05/2025 from dicsussions

#### Bugs

  No bug yet reported

#### Improvements

 > #8 : "les même blagues reviennent régulièrement" - jceintrey 06/05/2025 from issues
