Insurance Management - Docker Setup Guide
This guide will walk you through the steps to set up the project using Docker, build a Docker image, push it to Docker Hub, and run the container.

Prerequisites
Before starting, ensure you have the following tools installed:

Docker: To build, run, and manage Docker containers.

Git: To clone the repository from GitHub.

Steps to Set Up the Project Using Docker

1. Clone the Repository
Clone the repository to your local machine:

RUN: git clone https://github.com/GithubResources1/InsuranceManagement.git

RUN:cd InsuranceManagement

2. Create the Dockerfile
Create a Dockerfile in the root directory of your project:

RUN:touch Dockerfile

Add the following content to your Dockerfile:


FROM maven:3.8.4-openjdk-11-slim AS build
WORKDIR /app
ARG JAR_FILE=target/*.jar
COPY pom.xml .
RUN mvn dependency:go-offline
COPY src ./src
RUN mvn clean package -DskipTests


FROM openjdk:11-jre-slim
WORKDIR /app
COPY --from=build app/target/*.jar app.jar
EXPOSE 8081
ENTRYPOINT ["java", "-jar", "app.jar"]

Note: This Dockerfile uses a multi-stage build to optimize the final image. The first stage builds the application using Maven, and the second stage runs the application using a smaller OpenJDK runtime image.

3. Build the Docker Image
Once the Dockerfile is created, build the Docker image:

RUN:docker build -t insurance .

4. Verify the Image
To check if the image was successfully created, run the following command:

RUN:docker images

5. Push to Docker Hub
Create a public repository on Docker Hub.

Log in to Docker Hub:
RUN: docker login

Tag your Docker image for Docker Hub:

RUN:docker tag insurance:latest username/new-reponame:tagname

Push the Docker image to Docker Hub:

RUN:docker push username/new-reponame:tagname

6. Pull the Image on Another Environment
To pull the image to another environment or machine:

RUN:docker pull username/new-reponame:tagname

7. Run the Docker Container
To run the Docker container locally:

RUN:docker run -dp 8081:8081 username/new-reponame:tagname

8. Verify the App on Localhost
Once the container is running, you can verify the application by navigating to http://IPaddress:8081 in your web browser.

9. Access the Running Container
If you need to access the running container, use the following command:

RUN:docker exec -it containername sh

10. View Logs
To view the logs for the container, run:

RUN:docker logs containername

11. Inspect the Container
To inspect the details of the container:

RUN:docker inspect containername

12. Clean Up Old Docker Images
If you need to remove old or unused Docker images, use the following command:

RUN:docker image rm image-id


Conclusion
By following these steps, you can easily set up, build, push, and run the Insurance Management application using Docker. This setup ensures that the application is containerized and can be deployed across different environments with ease.









