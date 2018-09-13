---
title: Manage Azure Swarm cluster with Docker API
description: Deploy containers to a Docker Swarm cluster in Azure Container Service
services: container-service
author: rgardler
manager: madhana
ms.service: container-service
ms.topic: article
ms.date: 09/13/2016
ms.author: rogardle
ms.custom: mvc
ms.openlocfilehash: 3f8d18bc053bc303ab124ba38c8621d4ee2e8cb8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867036"
---
# <a name="container-management-with-docker-swarm"></a><span data-ttu-id="7adc0-103">Container management with Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="7adc0-103">Container management with Docker Swarm</span></span>

<span data-ttu-id="7adc0-104">Docker Swarm provides an environment for deploying containerized workloads across a pooled set of Docker hosts.</span><span class="sxs-lookup"><span data-stu-id="7adc0-104">Docker Swarm provides an environment for deploying containerized workloads across a pooled set of Docker hosts.</span></span> <span data-ttu-id="7adc0-105">Docker Swarm uses the native Docker API.</span><span class="sxs-lookup"><span data-stu-id="7adc0-105">Docker Swarm uses the native Docker API.</span></span> <span data-ttu-id="7adc0-106">The workflow for managing containers on a Docker Swarm is almost identical to what it would be on a single container host.</span><span class="sxs-lookup"><span data-stu-id="7adc0-106">The workflow for managing containers on a Docker Swarm is almost identical to what it would be on a single container host.</span></span> <span data-ttu-id="7adc0-107">This document provides simple examples of deploying containerized workloads in an Azure Container Service instance of Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="7adc0-107">This document provides simple examples of deploying containerized workloads in an Azure Container Service instance of Docker Swarm.</span></span> <span data-ttu-id="7adc0-108">For more in-depth documentation on Docker Swarm, see [Docker Swarm on Docker.com](https://docs.docker.com/swarm/).</span><span class="sxs-lookup"><span data-stu-id="7adc0-108">For more in-depth documentation on Docker Swarm, see [Docker Swarm on Docker.com](https://docs.docker.com/swarm/).</span></span>

[!INCLUDE [container-service-swarm-mode-note](../../../includes/container-service-swarm-mode-note.md)]

<span data-ttu-id="7adc0-109">Prerequisites to the exercises in this document:</span><span class="sxs-lookup"><span data-stu-id="7adc0-109">Prerequisites to the exercises in this document:</span></span>

[<span data-ttu-id="7adc0-110">Create a Swarm cluster in Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="7adc0-110">Create a Swarm cluster in Azure Container Service</span></span>](container-service-deployment.md)

[<span data-ttu-id="7adc0-111">Connect with the Swarm cluster in Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="7adc0-111">Connect with the Swarm cluster in Azure Container Service</span></span>](../container-service-connect.md)

## <a name="deploy-a-new-container"></a><span data-ttu-id="7adc0-112">Deploy a new container</span><span class="sxs-lookup"><span data-stu-id="7adc0-112">Deploy a new container</span></span>
<span data-ttu-id="7adc0-113">To create a new container in the Docker Swarm, use the `docker run` command (ensuring that you have opened an SSH tunnel to the masters as per the prerequisites above).</span><span class="sxs-lookup"><span data-stu-id="7adc0-113">To create a new container in the Docker Swarm, use the `docker run` command (ensuring that you have opened an SSH tunnel to the masters as per the prerequisites above).</span></span> <span data-ttu-id="7adc0-114">This example creates a container from the `yeasy/simple-web` image:</span><span class="sxs-lookup"><span data-stu-id="7adc0-114">This example creates a container from the `yeasy/simple-web` image:</span></span>

```bash
user@ubuntu:~$ docker run -d -p 80:80 yeasy/simple-web

4298d397b9ab6f37e2d1978ef3c8c1537c938e98a8bf096ff00def2eab04bf72
```

<span data-ttu-id="7adc0-115">After the container has been created, use `docker ps` to return information about the container.</span><span class="sxs-lookup"><span data-stu-id="7adc0-115">After the container has been created, use `docker ps` to return information about the container.</span></span> <span data-ttu-id="7adc0-116">Notice here that the Swarm agent that is hosting the container is listed:</span><span class="sxs-lookup"><span data-stu-id="7adc0-116">Notice here that the Swarm agent that is hosting the container is listed:</span></span>

```bash
user@ubuntu:~$ docker ps

CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                 NAMES
4298d397b9ab        yeasy/simple-web    "/bin/sh -c 'python i"   31 seconds ago      Up 9 seconds        10.0.0.5:80->80/tcp   swarm-agent-34A73819-1/happy_allen
```  

<span data-ttu-id="7adc0-117">You can now access the application that is running in this container through the public DNS name of the Swarm agent load balancer.</span><span class="sxs-lookup"><span data-stu-id="7adc0-117">You can now access the application that is running in this container through the public DNS name of the Swarm agent load balancer.</span></span> <span data-ttu-id="7adc0-118">You can find this information in the Azure portal:</span><span class="sxs-lookup"><span data-stu-id="7adc0-118">You can find this information in the Azure portal:</span></span>  

![Real visit results](./media/container-service-docker-swarm/real-visit.jpg)  

<span data-ttu-id="7adc0-120">By default the Load Balancer has ports 80, 8080 and 443 open.</span><span class="sxs-lookup"><span data-stu-id="7adc0-120">By default the Load Balancer has ports 80, 8080 and 443 open.</span></span> <span data-ttu-id="7adc0-121">If you want to connect on another port you will need to open that port on the Azure Load Balancer for the Agent Pool.</span><span class="sxs-lookup"><span data-stu-id="7adc0-121">If you want to connect on another port you will need to open that port on the Azure Load Balancer for the Agent Pool.</span></span>

## <a name="deploy-multiple-containers"></a><span data-ttu-id="7adc0-122">Deploy multiple containers</span><span class="sxs-lookup"><span data-stu-id="7adc0-122">Deploy multiple containers</span></span>
<span data-ttu-id="7adc0-123">As multiple containers are started, by executing 'docker run' multiple times, you can use the `docker ps` command to see which hosts the containers are running on.</span><span class="sxs-lookup"><span data-stu-id="7adc0-123">As multiple containers are started, by executing 'docker run' multiple times, you can use the `docker ps` command to see which hosts the containers are running on.</span></span> <span data-ttu-id="7adc0-124">In the example below, three containers are spread evenly across the three Swarm agents:</span><span class="sxs-lookup"><span data-stu-id="7adc0-124">In the example below, three containers are spread evenly across the three Swarm agents:</span></span>  

```bash
user@ubuntu:~$ docker ps

CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                 NAMES
11be062ff602        yeasy/simple-web    "/bin/sh -c 'python i"   11 seconds ago      Up 10 seconds       10.0.0.6:83->80/tcp   swarm-agent-34A73819-2/clever_banach
1ff421554c50        yeasy/simple-web    "/bin/sh -c 'python i"   49 seconds ago      Up 48 seconds       10.0.0.4:82->80/tcp   swarm-agent-34A73819-0/stupefied_ride
4298d397b9ab        yeasy/simple-web    "/bin/sh -c 'python i"   2 minutes ago       Up 2 minutes        10.0.0.5:80->80/tcp   swarm-agent-34A73819-1/happy_allen
```  

## <a name="deploy-containers-by-using-docker-compose"></a><span data-ttu-id="7adc0-125">Deploy containers by using Docker Compose</span><span class="sxs-lookup"><span data-stu-id="7adc0-125">Deploy containers by using Docker Compose</span></span>
<span data-ttu-id="7adc0-126">You can use Docker Compose to automate the deployment and configuration of multiple containers.</span><span class="sxs-lookup"><span data-stu-id="7adc0-126">You can use Docker Compose to automate the deployment and configuration of multiple containers.</span></span> <span data-ttu-id="7adc0-127">To do so, ensure that a Secure Shell (SSH) tunnel has been created and that the DOCKER_HOST variable has been set (see the pre-requisites above).</span><span class="sxs-lookup"><span data-stu-id="7adc0-127">To do so, ensure that a Secure Shell (SSH) tunnel has been created and that the DOCKER_HOST variable has been set (see the pre-requisites above).</span></span>

<span data-ttu-id="7adc0-128">Create a docker-compose.yml file on your local system.</span><span class="sxs-lookup"><span data-stu-id="7adc0-128">Create a docker-compose.yml file on your local system.</span></span> <span data-ttu-id="7adc0-129">To do this, use this [sample](https://raw.githubusercontent.com/rgardler/AzureDevTestDeploy/master/docker-compose.yml).</span><span class="sxs-lookup"><span data-stu-id="7adc0-129">To do this, use this [sample](https://raw.githubusercontent.com/rgardler/AzureDevTestDeploy/master/docker-compose.yml).</span></span>

```bash
web:
  image: adtd/web:0.1
  ports:
    - "80:80"
  links:
    - rest:rest-demo-azure.marathon.mesos
rest:
  image: adtd/rest:0.1
  ports:
    - "8080:8080"

```

<span data-ttu-id="7adc0-130">Run `docker-compose up -d` to start the container deployments:</span><span class="sxs-lookup"><span data-stu-id="7adc0-130">Run `docker-compose up -d` to start the container deployments:</span></span>

```bash
user@ubuntu:~/compose$ docker-compose up -d
Pulling rest (adtd/rest:0.1)...
swarm-agent-3B7093B8-0: Pulling adtd/rest:0.1... : downloaded
swarm-agent-3B7093B8-2: Pulling adtd/rest:0.1... : downloaded
swarm-agent-3B7093B8-3: Pulling adtd/rest:0.1... : downloaded
Creating compose_rest_1
Pulling web (adtd/web:0.1)...
swarm-agent-3B7093B8-3: Pulling adtd/web:0.1... : downloaded
swarm-agent-3B7093B8-0: Pulling adtd/web:0.1... : downloaded
swarm-agent-3B7093B8-2: Pulling adtd/web:0.1... : downloaded
Creating compose_web_1
```

<span data-ttu-id="7adc0-131">Finally, the list of running containers will be returned.</span><span class="sxs-lookup"><span data-stu-id="7adc0-131">Finally, the list of running containers will be returned.</span></span> <span data-ttu-id="7adc0-132">This list reflects the containers that were deployed by using Docker Compose:</span><span class="sxs-lookup"><span data-stu-id="7adc0-132">This list reflects the containers that were deployed by using Docker Compose:</span></span>

```bash
user@ubuntu:~/compose$ docker ps
CONTAINER ID        IMAGE               COMMAND                CREATED             STATUS              PORTS                     NAMES
caf185d221b7        adtd/web:0.1        "apache2-foreground"   2 minutes ago       Up About a minute   10.0.0.4:80->80/tcp       swarm-agent-3B7093B8-0/compose_web_1
040efc0ea937        adtd/rest:0.1       "catalina.sh run"      3 minutes ago       Up 2 minutes        10.0.0.4:8080->8080/tcp   swarm-agent-3B7093B8-0/compose_rest_1
```

<span data-ttu-id="7adc0-133">Naturally, you can use `docker-compose ps` to examine only the containers defined in your `compose.yml` file.</span><span class="sxs-lookup"><span data-stu-id="7adc0-133">Naturally, you can use `docker-compose ps` to examine only the containers defined in your `compose.yml` file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7adc0-134">Next steps</span><span class="sxs-lookup"><span data-stu-id="7adc0-134">Next steps</span></span>
[<span data-ttu-id="7adc0-135">Learn more about Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="7adc0-135">Learn more about Docker Swarm</span></span>](https://docs.docker.com/swarm/)

