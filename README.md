# AltaPay DevOps Technical Test

[![Gradle Package](https://github.com/SomaGallai/shop_order_service/actions/workflows/gradle-publish.yml/badge.svg?branch=main)](https://github.com/SomaGallai/shop_order_service/actions/workflows/gradle-publish.yml)

This project contains a Shop Order service written in Java, that you can Run as specified in the section [Run](.README.md#run)

The objective of the test is build, package, and deploy the service to an AWS account

## Assignment

**Functional Requirements**

- [X] Create a build step that will ensure the code can be built
- [X] Create a package step that will publish the docker image to a registry
- [X] Create a provision step that will create the container environment for the image to run
- [X] Create a deploy step that will run the docker image in the container environment created above

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

## Provisioning and deployment steps to re-produce

Commands for Terraform initialization and environment setup.

```bash
terraform init 
terraform apply
```

Command to retrieve the access credentials for your cluster and automatically configure kubectl.

```bash
aws eks --region $(terraform output -raw region) update-kubeconfig --name $(terraform output -raw cluster_name)
```

Command to see if the credentials are correct

```bash
kubectl get all
```

Command to deploy kubernetes deployment and service.

```bash
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
```

Command to see if the service is running.

```bash
kubectl get all
```

There should be a following output:

```bash
NAME                                    READY   STATUS    RESTARTS   AGE
pod/application-test-58b87566f6-dlnsm   1/1     Running   0          106m

NAME                       TYPE           CLUSTER-IP      EXTERNAL-IP                                                                 PORT(S)        AGE
service/application-test   LoadBalancer   172.20.53.210   ac36cf360d67942b7b884f3a5e3ce0ac-844248188.eu-central-1.elb.amazonaws.com   80:30360/TCP   16s
service/kubernetes         ClusterIP      172.20.0.1      <none>                                                                      443/TCP        111m

NAME                               READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/application-test   1/1     1            1           106m

NAME                                          DESIRED   CURRENT   READY   AGE
replicaset.apps/application-test-58b87566f6   1         1         1       106m
```

Where the external IP as can be seen `ac36cf360d67942b7b884f3a5e3ce0ac-844248188.eu-central-1.elb.amazonaws.com` is the Shop Order Service public IP address

To test is run the following command(watch-out as the name of the address might be different):
```bash
http://ac36cf360d67942b7b884f3a5e3ce0ac-844248188.eu-central-1.elb.amazonaws.com/shopOrders
```