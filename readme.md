# Spring PetClinic Deployment on Kubernetes

This repository contains the deployment files for the Spring PetClinic application on Kubernetes. The deployment setup follows the guidelines from the [DevOpsCube article](https://devopscube.com/deploy-java-app-kubernetes/).

## Table of Contents

- [Introduction](#introduction)
- [Pre-requisites](#pre-requisites)
- [Kubernetes Deployment](#kubernetes-deployment)
- [Steps](#steps)
- [Application URL](#application-url)
- [Troubleshooting](#troubleshooting)
- [Contributing](#contributing)

## Introduction

This project demonstrates how to deploy a Java application, specifically the Spring PetClinic, on a Kubernetes cluster. The application is deployed using a combination of services, deployments, and persistent storage.

## Pre-requisites

Before proceeding, ensure you have the following:

1. A running Kubernetes cluster (Minikube, GKE, or any other provider).
2. kubectl installed and configured to communicate with your Kubernetes cluster.
3. Docker installed for building and pushing the container images.
4. Access to a container registry (Docker Hub, GCR, etc.).
5. Maven (3.9.6) and Java-17 installed in your system

## Build the Java Application
 ```bash
  mvn clean install
  ```

## Kubernetes Deployment

The Kubernetes manifests provided in this repository cover:

- **MySQL Deployment**: A MySQL database deployed in Kubernetes with a PersistentVolumeClaim.
- **Java Application Deployment**: The Spring PetClinic application deployed as a Kubernetes Deployment with associated services.

## Steps

1. **Clone the repository**:
    ```bash
    git clone https://github.com/NahlaAbdAlghany/spring-petclinic-deployment-k8s.git
    cd spring-petclinic-deployment-k8s
    ```

2. **Deploy MySQL**:
    First, deploy the MySQL database which the Spring PetClinic application will use:
    ```bash
    kubectl apply -f mysql-deployment.yaml
    ```

3. **Build the Spring PetClinic Docker Image**:
    If you haven't already built the Docker image for the application, do so:
    ```bash
    docker build -t nahlathabet/spring-petclinic .
    docker push nahlathabet/spring-petclinic
    ```

4. **Deploy the Application**:
    Deploy the Spring PetClinic application to Kubernetes:
    ```bash
    kubectl apply -f java-app-deployment.yaml
    ```

5. **Expose the Application**:
    To access the application, expose it via a service:
    ```bash
    kubectl apply -f service.yaml
    ```

6. **Access the Application**:
    If you're using Minikube, you can access the application via:
    ```bash
    minikube service spring-petclinic-service
    ```

## Application URL

Once deployed, the Spring PetClinic application will be available at the service URL exposed by Kubernetes. If using a cloud provider like GKE or EKS, the application will be accessible via the external IP provided by the service.

## Troubleshooting

If you encounter issues during deployment, consider the following:

- **Check the Pods**:
    Ensure all pods are running correctly:
    ```bash
    kubectl get pods
    ```

- **Check Logs**:
    View the logs of any failing pod:
    ```bash
    kubectl logs <pod-name>
    ```

- **Verify Services**:
    Make sure services are exposing the correct ports:
    ```bash
    kubectl get svc
    ```



---

For more detailed steps and insights, please refer to the original guide on [DevOpsCube](https://devopscube.com/deploy-java-app-kubernetes/).

