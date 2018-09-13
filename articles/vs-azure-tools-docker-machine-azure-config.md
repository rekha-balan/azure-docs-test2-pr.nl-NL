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
# <a name="create-docker-hosts-in-azure-with-docker-machine"></a>Create Docker Hosts in Azure with Docker-Machine
Running [Docker](https://www.docker.com/) containers requires a host VM running the docker daemon.
This topic describes how to use the [docker-machine](https://docs.docker.com/machine/) command to create new Linux VMs, configured with the Docker daemon, running in Azure. 

**Note:** 

* *This article depends on docker-machine version 0.9.0-rc2 or greater*
* *Windows Containers will be supported through docker-machine in the near future*

## <a name="create-vms-with-docker-machine"></a>Create VMs with Docker Machine
Create docker host VMs in Azure with the `docker-machine create` command using the `azure` driver. 

The Azure driver will need your subscription ID. You can use the [Azure CLI](cli-install-nodejs.md) or the [Azure Portal](https://portal.azure.com) to retrieve your Azure Subscription. 

**Using the Azure Portal**

* Select Subscriptions from the left navigation page, and copy to subscription id.

**Using the Azure CLI**

* Type ```azure account list``` and copy the subscription id.

Type `docker-machine create --driver azure` to see the options and their default values.
You can also see the [Docker Azure Driver documentation](https://docs.docker.com/machine/drivers/azure/) for more info. 

The following example relies upon the [default values](https://github.com/docker/machine/blob/master/drivers/azure/azure.go#L22), but it does optionally set these values: 

* azure-dns for the name associated with the public IP and certificates generated.  The VM can then safely stop, release the dynamic IP, and give the ability to reconnect after vm starts again with a new IP.  The name prefix needs to be unique for that region  UNIQUE_DNSNAME_PREFIX.westus.cloudapp.azure.com.
* open port 80 on the VM for outbound internet access
* size of the VM to utilize faster premium storage
* premium storage used for the vm disk

```
docker-machine create -d azure --azure-subscription-id <Your AZURE_SUBSCRIPTION_ID> --azure-dns <Your UNIQUE_DNSNAME_PREFIX> --azure-open-port 80 --azure-size Standard_DS1_v2 --azure-storage-type "Premium_LRS" mydockerhost 
```

## <a name="choose-a-docker-host-with-docker-machine"></a>Choose a docker host with docker-machine
Once you have an entry in docker-machine for your host, you can set the default host when running docker commands.

## <a name="using-powershell"></a>Using PowerShell
```powershell
docker-machine env MyDockerHost | Invoke-Expression 
```

## <a name="using-bash"></a>Using Bash
```bash
eval $(docker-machine env MyDockerHost)
```

You can now run docker commands against the specified host

```
docker ps
docker info
```

## <a name="run-a-container"></a>Run a container
With a host configured, you can now run a simple web server to test whether your host was configured correctly.
Here we use a standard nginx image, specify that it should listen on port 80, and that if the host VM restarts, the container will restart as well (`--restart=always`). 

```bash
docker run -d -p 80:80 --restart=always nginx
```

The output should look something like the following:

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

## <a name="test-the-container"></a>Test the container
Examine running containers using `docker ps`:

```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                         NAMES
d5b78f27b335        nginx               "nginx -g 'daemon off"   5 minutes ago       Up 5 minutes        0.0.0.0:80->80/tcp, 443/tcp   goofy_mahavira
```

And check to see the running container, type `docker-machine ip <VM name>` to find the IP address to enter in the browser:

```
PS C:\> docker-machine ip MyDockerHost
191.237.46.90
```

![Running ngnix container](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-docker-machine-azure-config/nginxsuccess.png)

## <a name="summary"></a>Summary
With docker-machine you can easily provision docker hosts in Azure for your individual docker host validations.
For production hosting of containers, see the [Azure Container Service](http://aka.ms/AzureContainerService)

To develop .NET Core Applications with Visual Studio, see [Docker Tools for Visual Studio](http://aka.ms/DockerToolsForVS)


