# Introduction

This repository is a continuation from previous repositories exploring docker and containerization.  The focus of this repository is on Kubernetes and the orchestration of docker containers

## Goals

1. Run Kubernetes in a local work station
2. Create a series of apps that are run within local pods
3. Learn Kubernetes commands
4. Learn how to update containers in pods

## References

- [aroeh Docker Quickstart Repo](https://github.com/aroeh/docker-quickstart)
- [aroeh Docker Compose Repo](https://github.com/aroeh/docker-compose)
- [Docker Compose CLI Reference](https://docs.docker.com/compose/reference/)
- [Docker Orchestration Overview](https://docs.docker.com/get-started/orchestration/)
- [Kubernetes](https://kubernetes.io/docs/home/)
- [Kubernetes CLI Reference](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#-strong-getting-started-strong-)
- [An Introduction to Kubernetes](https://andrewlock.net/deploying-asp-net-core-applications-to-kubernetes-part-1-an-introduction-to-kubernetes/)
- [Deploy .NET Minimal APIs To Kubernetes!](https://programmingfire.com/deploy-dotnet-minimal-apis-to-kubernetes)
- [Microsoft - Build ASP.NET Core applications deployed as Linux containers](https://docs.microsoft.com/en-us/dotnet/architecture/containerized-lifecycle/design-develop-containerized-apps/build-aspnet-core-applications-linux-containers-aks-kubernetes)
- [How to deploy a .NET 5 API in a Kubernetes cluster](https://faun.pub/how-to-deploy-a-net-5-api-in-a-kubernetes-cluster-53212af6a0e2)
- [How to deploy angular on kubernetes](https://blog.mayadata.io/openebs/steps-to-deploy-angular-application-on-kubernetes)

# Tools

- Windows 10 Pro **Pro or higher is needed since that enables the hyper-v virtualization on windows hosts
- Visual Studio 2022 v17.0.5
- Visual Studio Code v1.63.2
- Docker
    - Desktop v4.4.4
    - Engine v20.10.12
    - Compose v1.29.2
- .Net6
- Node.js v17.6.0
- npm v8.5.2
- AngularCLI v13.2.4

# Getting Started

Follow the Docker documentation to install Kubernetes - [Docker Orchestration Overview](https://docs.docker.com/get-started/orchestration/)

# Solution Overview

There are 3 different solutions in the repository to account for different apps and technologies.  Each one has it's own Dockerfile for containerization.  Currently there are 2 .net apps and 1 angular app

Folder structure is as follows
```
├── .gitignore
├── docker-compose.yml
├── kubernetes
├── angular_app
│   ├── angular_app
│   │   ├── node_modules
│   │   ├── src
│   │   │   ├── App Code
│   │   ├── angular.json
│   │   ├── package.json
├── blazor_app
│   ├── blazor_app.sln
│   ├── blazor_app
│   │   ├── blazor_app.csproj
│   │   ├── Dockerfile
│   │   ├── .dockerignore
│   │   ├── nginx.conf
│   │   ├── Other app files
├── weather_api
│   ├── weather_api.sln
│   ├── weather_api
│   │   ├── weather_api.csproj
│   │   ├── Dockerfile
│   │   ├── .dockerignore
│   │   ├── nginx.conf
│   │   ├── Other app files
```

Each solution can be run independently via an IDE or images/containers for debugging purposes.  They can be run together at the same time via docker-compose.

The Kubernetes directory contains yaml files for pod and service definitions.  Each one definition will contain at least a deployment definition.

# Build and Run

Each project can be built independently but docker and docker compose are the intended ways build all of the projects.  Use a Command line tool that can run docker commands

1. Make sure Docker is running
2. Change to the solution directory containing the docker-compose.yml file
```
cd <PATH>\docker-kubernetes
```
3. Build the docker images
```
docker-compose build
```
4. Deploy and each of the components in Kubernetes
```
kubectl apply -f cache.yml
kubectl apply -f api.yml
kubectl apply -f blazor.yml
kubectl apply -f angular.yml
```

5. Confirm all pods and services are running in Kubernetes
```
kubectl get all
```

> NOTE: You can also get elements with specific commands reference the CLI documentation for more details
> For example to get only deployments
```
kubectl get deployments
```
6. Remove items as needed or remove them all
```
kubectl delete [OPTIONS]
```
```
kubectl delete -f blazorapp.yml
```
```
kubectl delete pods --all
kubectl delete services --all
kubectl delete deployments --all
```