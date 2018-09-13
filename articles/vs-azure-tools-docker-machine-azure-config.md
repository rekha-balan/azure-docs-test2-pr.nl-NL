---
title: Create Docker hosts in Azure with Docker Machine | Microsoft Docs
description: Describes use of Docker Machine to create docker hosts in Azure.
services: azure-container-service
documentationcenter: na
author: mlearned
manager: douge
editor: ''
ms.assetid: 7a3ff6e1-fa93-4a62-b524-ab182d2fea08
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 06/08/2016
ms.author: mlearned
ms.openlocfilehash: 624af3a5ad41d178254c9b4e07c6665ddaa33b50
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549735"
---
# <a name="create-docker-hosts-in-azure-with-docker-machine"></a><span data-ttu-id="6b1a8-103">Create Docker Hosts in Azure with Docker-Machine</span><span class="sxs-lookup"><span data-stu-id="6b1a8-103">Create Docker Hosts in Azure with Docker-Machine</span></span>
<span data-ttu-id="6b1a8-104">Running [Docker](https://www.docker.com/) containers requires a host VM running the docker daemon.</span><span class="sxs-lookup"><span data-stu-id="6b1a8-104">Running [Docker](https://www.docker.com/) containers requires a host VM running the docker daemon.</span></span>
<span data-ttu-id="6b1a8-105">This topic describes how to use the [docker-machine](https://docs.docker.com/machine/) command to create new Linux VMs, configured with the Docker daemon, running in Azure.</span><span class="sxs-lookup"><span data-stu-id="6b1a8-105">This topic describes how to use the [docker-machine](https://docs.docker.com/machine/) command to create new Linux VMs, configured with the Docker daemon, running in Azure.</span></span> 

<span data-ttu-id="6b1a8-106">**Note:**</span><span class="sxs-lookup"><span data-stu-id="6b1a8-106">**Note:**</span></span> 

* <span data-ttu-id="6b1a8-107">*This article depends on docker-machine version 0.9.0-rc2 or greater*</span><span class="sxs-lookup"><span data-stu-id="6b1a8-107">*This article depends on docker-machine version 0.9.0-rc2 or greater*</span></span>
* <span data-ttu-id="6b1a8-108">*Windows Containers will be supported through docker-machine in the near future*</span><span class="sxs-lookup"><span data-stu-id="6b1a8-108">*Windows Containers will be supported through docker-machine in the near future*</span></span>

## <a name="create-vms-with-docker-machine"></a><span data-ttu-id="6b1a8-109">Create VMs with Docker Machine</span><span class="sxs-lookup"><span data-stu-id="6b1a8-109">Create VMs with Docker Machine</span></span>
<span data-ttu-id="6b1a8-110">Create docker host VMs in Azure with the `docker-machine create` command using the `azure` driver.</span><span class="sxs-lookup"><span data-stu-id="6b1a8-110">Create docker host VMs in Azure with the `docker-machine create` command using the `azure` driver.</span></span> 

<span data-ttu-id="6b1a8-111">The Azure driver will need your subscription ID.</span><span class="sxs-lookup"><span data-stu-id="6b1a8-111">The Azure driver will need your subscription ID.</span></span> <span data-ttu-id="6b1a8-112">You can use the [Azure CLI](cli-install-nodejs.md) or the [Azure Portal](https://portal.azure.com) to retrieve your Azure Subscription.</span><span class="sxs-lookup"><span data-stu-id="6b1a8-112">You can use the [Azure CLI](cli-install-nodejs.md) or the [Azure Portal](https://portal.azure.com) to retrieve your Azure Subscription.</span></span> 

<span data-ttu-id="6b1a8-113">**Using the Azure Portal**</span><span class="sxs-lookup"><span data-stu-id="6b1a8-113">**Using the Azure Portal**</span></span>

* <span data-ttu-id="6b1a8-114">Select Subscriptions from the left navigation page, and copy to subscription id.</span><span class="sxs-lookup"><span data-stu-id="6b1a8-114">Select Subscriptions from the left navigation page, and copy to subscription id.</span></span>

<span data-ttu-id="6b1a8-115">**Using the Azure CLI**</span><span class="sxs-lookup"><span data-stu-id="6b1a8-115">**Using the Azure CLI**</span></span>

* <span data-ttu-id="6b1a8-116">Type ```azure account list``` and copy the subscription id.</span><span class="sxs-lookup"><span data-stu-id="6b1a8-116">Type ```azure account list``` and copy the subscription id.</span></span>

<span data-ttu-id="6b1a8-117">Type `docker-machine create --driver azure` to see the options and their default values.</span><span class="sxs-lookup"><span data-stu-id="6b1a8-117">Type `docker-machine create --driver azure` to see the options and their default values.</span></span>
<span data-ttu-id="6b1a8-118">You can also see the [Docker Azure Driver documentation](https://docs.docker.com/machine/drivers/azure/) for more info.</span><span class="sxs-lookup"><span data-stu-id="6b1a8-118">You can also see the [Docker Azure Driver documentation](https://docs.docker.com/machine/drivers/azure/) for more info.</span></span> 

<span data-ttu-id="6b1a8-119">The following example relies upon the [default values](https://github.com/docker/machine/blob/master/drivers/azure/azure.go#L22), but it does optionally set these values:</span><span class="sxs-lookup"><span data-stu-id="6b1a8-119">The following example relies upon the [default values](https://github.com/docker/machine/blob/master/drivers/azure/azure.go#L22), but it does optionally set these values:</span></span> 

* <span data-ttu-id="6b1a8-120">azure-dns for the name associated with the public IP and certificates generated.</span><span class="sxs-lookup"><span data-stu-id="6b1a8-120">azure-dns for the name associated with the public IP and certificates generated.</span></span>  <span data-ttu-id="6b1a8-121">The VM can then safely stop, release the dynamic IP, and give the ability to reconnect after vm starts again with a new IP.</span><span class="sxs-lookup"><span data-stu-id="6b1a8-121">The VM can then safely stop, release the dynamic IP, and give the ability to reconnect after vm starts again with a new IP.</span></span>  <span data-ttu-id="6b1a8-122">The name prefix needs to be unique for that region  UNIQUE_DNSNAME_PREFIX.westus.cloudapp.azure.com.</span><span class="sxs-lookup"><span data-stu-id="6b1a8-122">The name prefix needs to be unique for that region  UNIQUE_DNSNAME_PREFIX.westus.cloudapp.azure.com.</span></span>
* <span data-ttu-id="6b1a8-123">open port 80 on the VM for outbound internet access</span><span class="sxs-lookup"><span data-stu-id="6b1a8-123">open port 80 on the VM for outbound internet access</span></span>
* <span data-ttu-id="6b1a8-124">size of the VM to utilize faster premium storage</span><span class="sxs-lookup"><span data-stu-id="6b1a8-124">size of the VM to utilize faster premium storage</span></span>
* <span data-ttu-id="6b1a8-125">premium storage used for the vm disk</span><span class="sxs-lookup"><span data-stu-id="6b1a8-125">premium storage used for the vm disk</span></span>

```
docker-machine create -d azure --azure-subscription-id <Your AZURE_SUBSCRIPTION_ID> --azure-dns <Your UNIQUE_DNSNAME_PREFIX> --azure-open-port 80 --azure-size Standard_DS1_v2 --azure-storage-type "Premium_LRS" mydockerhost 
```

## <a name="choose-a-docker-host-with-docker-machine"></a><span data-ttu-id="6b1a8-126">Choose a docker host with docker-machine</span><span class="sxs-lookup"><span data-stu-id="6b1a8-126">Choose a docker host with docker-machine</span></span>
<span data-ttu-id="6b1a8-127">Once you have an entry in docker-machine for your host, you can set the default host when running docker commands.</span><span class="sxs-lookup"><span data-stu-id="6b1a8-127">Once you have an entry in docker-machine for your host, you can set the default host when running docker commands.</span></span>

## <a name="using-powershell"></a><span data-ttu-id="6b1a8-128">Using PowerShell</span><span class="sxs-lookup"><span data-stu-id="6b1a8-128">Using PowerShell</span></span>
```powershell
docker-machine env MyDockerHost | Invoke-Expression 
```

## <a name="using-bash"></a><span data-ttu-id="6b1a8-129">Using Bash</span><span class="sxs-lookup"><span data-stu-id="6b1a8-129">Using Bash</span></span>
```bash
eval $(docker-machine env MyDockerHost)
```

<span data-ttu-id="6b1a8-130">You can now run docker commands against the specified host</span><span class="sxs-lookup"><span data-stu-id="6b1a8-130">You can now run docker commands against the specified host</span></span>

```
docker ps
docker info
```

## <a name="run-a-container"></a><span data-ttu-id="6b1a8-131">Run a container</span><span class="sxs-lookup"><span data-stu-id="6b1a8-131">Run a container</span></span>
<span data-ttu-id="6b1a8-132">With a host configured, you can now run a simple web server to test whether your host was configured correctly.</span><span class="sxs-lookup"><span data-stu-id="6b1a8-132">With a host configured, you can now run a simple web server to test whether your host was configured correctly.</span></span>
<span data-ttu-id="6b1a8-133">Here we use a standard nginx image, specify that it should listen on port 80, and that if the host VM restarts, the container will restart as well (`--restart=always`).</span><span class="sxs-lookup"><span data-stu-id="6b1a8-133">Here we use a standard nginx image, specify that it should listen on port 80, and that if the host VM restarts, the container will restart as well (`--restart=always`).</span></span> 

```bash
docker run -d -p 80:80 --restart=always nginx
```

<span data-ttu-id="6b1a8-134">The output should look something like the following:</span><span class="sxs-lookup"><span data-stu-id="6b1a8-134">The output should look something like the following:</span></span>

```
Unable to find image 'nginx:latest' locally
latest: Pulling from library/nginx
efd26ecc9548: Pull complete
a3ed95caeb02: Pull complete
83f52fbfa5f8: Pull complete
fa664caa1402: Pull complete
Digest: sha256:12127e07a75bda1022fbd4ea231f5527a1899aad4679e3940482db3b57383b1d
Status: Downloaded newer image for nginx:latest
25942c35d86fe43c688d0c03ad478f14cc9c16913b0e1c2971cb32eb4d0ab721
```

## <a name="test-the-container"></a><span data-ttu-id="6b1a8-135">Test the container</span><span class="sxs-lookup"><span data-stu-id="6b1a8-135">Test the container</span></span>
<span data-ttu-id="6b1a8-136">Examine running containers using `docker ps`:</span><span class="sxs-lookup"><span data-stu-id="6b1a8-136">Examine running containers using `docker ps`:</span></span>

```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                         NAMES
d5b78f27b335        nginx               "nginx -g 'daemon off"   5 minutes ago       Up 5 minutes        0.0.0.0:80->80/tcp, 443/tcp   goofy_mahavira
```

<span data-ttu-id="6b1a8-137">And check to see the running container, type `docker-machine ip <VM name>` to find the IP address to enter in the browser:</span><span class="sxs-lookup"><span data-stu-id="6b1a8-137">And check to see the running container, type `docker-machine ip <VM name>` to find the IP address to enter in the browser:</span></span>

```
PS C:\> docker-machine ip MyDockerHost
191.237.46.90
```

![Running ngnix container](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-docker-machine-azure-config/nginxsuccess.png)

## <a name="summary"></a><span data-ttu-id="6b1a8-139">Summary</span><span class="sxs-lookup"><span data-stu-id="6b1a8-139">Summary</span></span>
<span data-ttu-id="6b1a8-140">With docker-machine you can easily provision docker hosts in Azure for your individual docker host validations.</span><span class="sxs-lookup"><span data-stu-id="6b1a8-140">With docker-machine you can easily provision docker hosts in Azure for your individual docker host validations.</span></span>
<span data-ttu-id="6b1a8-141">For production hosting of containers, see the [Azure Container Service](http://aka.ms/AzureContainerService)</span><span class="sxs-lookup"><span data-stu-id="6b1a8-141">For production hosting of containers, see the [Azure Container Service](http://aka.ms/AzureContainerService)</span></span>

<span data-ttu-id="6b1a8-142">To develop .NET Core Applications with Visual Studio, see [Docker Tools for Visual Studio](http://aka.ms/DockerToolsForVS)</span><span class="sxs-lookup"><span data-stu-id="6b1a8-142">To develop .NET Core Applications with Visual Studio, see [Docker Tools for Visual Studio](http://aka.ms/DockerToolsForVS)</span></span>


