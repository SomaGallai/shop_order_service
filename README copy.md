# AltaPay DevOps Technical Test

This project contains a Shop Order service written in Java, that you can Run as specified in the section [Run](.README.md#run)

The objective of the test is build, package, and deploy the service to an AWS account

## Assignment

**Functional Requirements**

- [ ] Create a build step that will ensure the code can be built
- [ ] Create a package step that will publish the docker image to a registry
- [ ] Create a provision step that will create the container environment for the image to run
- [ ] Create a deploy step that will run the docker image in the container environment created above

**Technical Requirements:**

- You can use either github or gitlab, as long as the project is publicly available
- The environment needs to be build in AWS, with the AWS account and credentials provided
- You can use any provisioning tool, but terraform will be a plus

## Run

### Locally

Install:
- Java 11

```bash
./gradlew bootRun
```

### Docker

Install:
- Docker

```bash
docker build -t technical-test-frontend .
docker run -p 8080:8080 technical-test-frontend
```

## API Documentation

Open API Specification: http://localhost:8080/v3/api-docs/

Swagger: http://localhost:8080/swagger-ui.html