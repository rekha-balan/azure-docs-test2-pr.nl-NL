---
title: Use Docker Machine to create Linux hosts in Azure | Microsoft Docs
description: Describes use of Docker Machine to create docker hosts in Azure.
services: virtual-machines-linux
documentationcenter: ''
author: squillace
manager: timlt
editor: tysonn
ms.assetid: 164b47de-6b17-4e29-8b7d-4996fa65bea4
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 07/22/2016
ms.author: rasquill
ms.openlocfilehash: f83b1d62b0e8da21e99addc00d6ae17394532e5a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549667"
---
# <a name="use-docker-machine-with-the-azure-driver"></a><span data-ttu-id="23816-103">Use Docker Machine with the Azure driver</span><span class="sxs-lookup"><span data-stu-id="23816-103">Use Docker Machine with the Azure driver</span></span>
<span data-ttu-id="23816-104">[Docker](https://www.docker.com/) provides virtualization using Linux containers rather than VMs to isolate application data and computing on a shared resource.</span><span class="sxs-lookup"><span data-stu-id="23816-104">[Docker](https://www.docker.com/) provides virtualization using Linux containers rather than VMs to isolate application data and computing on a shared resource.</span></span> <span data-ttu-id="23816-105">This topic describes how and when to use [Docker Machine](https://docs.docker.com/machine/) .</span><span class="sxs-lookup"><span data-stu-id="23816-105">This topic describes how and when to use [Docker Machine](https://docs.docker.com/machine/) .</span></span> <span data-ttu-id="23816-106">The `docker-machine` command  creates a new Linux VM in Azure enabled as a docker host for Linux containers.</span><span class="sxs-lookup"><span data-stu-id="23816-106">The `docker-machine` command  creates a new Linux VM in Azure enabled as a docker host for Linux containers.</span></span>

## <a name="create-vms-with-docker-machine"></a><span data-ttu-id="23816-107">Create VMs with Docker Machine</span><span class="sxs-lookup"><span data-stu-id="23816-107">Create VMs with Docker Machine</span></span>
<span data-ttu-id="23816-108">Create docker host VMs in Azure with the `docker-machine create` command using the `azure` driver argument for the driver option (`-d`) and any other arguments.</span><span class="sxs-lookup"><span data-stu-id="23816-108">Create docker host VMs in Azure with the `docker-machine create` command using the `azure` driver argument for the driver option (`-d`) and any other arguments.</span></span> 

<span data-ttu-id="23816-109">The following example relies upon the default values, but it does open port 80 on the VM to the internet to test with an nginx container, makes `ops` the logon user for SSH, and calls the new VM `machine`.</span><span class="sxs-lookup"><span data-stu-id="23816-109">The following example relies upon the default values, but it does open port 80 on the VM to the internet to test with an nginx container, makes `ops` the logon user for SSH, and calls the new VM `machine`.</span></span> 

<span data-ttu-id="23816-110">Type `docker-machine create --driver azure` to see the options and their default values; you can also read the [Docker Azure Driver documentation](https://docs.docker.com/machine/drivers/azure/).</span><span class="sxs-lookup"><span data-stu-id="23816-110">Type `docker-machine create --driver azure` to see the options and their default values; you can also read the [Docker Azure Driver documentation](https://docs.docker.com/machine/drivers/azure/).</span></span> <span data-ttu-id="23816-111">(Note that if you have two-factor authentication enabled, you will be prompted to authenticate using the second factor.)</span><span class="sxs-lookup"><span data-stu-id="23816-111">(Note that if you have two-factor authentication enabled, you will be prompted to authenticate using the second factor.)</span></span>

```bash
docker-machine create -d azure \
  --azure-ssh-user ops \
  --azure-subscription-id <Your AZURE_SUBSCRIPTION_ID> \
  --azure-open-port 80 \
  machine
```

<span data-ttu-id="23816-112">The output should look something like this, depending upon whether you have two-factor authentication configured in your account.</span><span class="sxs-lookup"><span data-stu-id="23816-112">The output should look something like this, depending upon whether you have two-factor authentication configured in your account.</span></span>

```bash
Creating CA: /Users/user/.docker/machine/certs/ca.pem
Creating client certificate: /Users/user/.docker/machine/certs/cert.pem
Running pre-create checks...
(machine) Microsoft Azure: To sign in, use a web browser to open the page https://aka.ms/devicelogin. Enter the code <code> to authenticate.
(machine) Completed machine pre-create checks.
Creating machine...
(machine) Querying existing resource group.  name="machine"
(machine) Creating resource group.  name="machine" location="eastus"
(machine) Configuring availability set.  name="docker-machine"
(machine) Configuring network security group.  name="machine-firewall" location="eastus"
(machine) Querying if virtual network already exists.  name="docker-machine-vnet" location="eastus"
(machine) Configuring subnet.  name="docker-machine" vnet="docker-machine-vnet" cidr="192.168.0.0/16"
(machine) Creating public IP address.  name="machine-ip" static=false
(machine) Creating network interface.  name="machine-nic"
(machine) Creating storage account.  name="vhdsolksdjalkjlmgyg6" location="eastus"
(machine) Creating virtual machine.  name="machine" location="eastus" size="Standard_A2" username="ops" osImage="canonical:UbuntuServer:15.10:latest"
Waiting for machine to be running, this may take a few minutes...
Detecting operating system of created instance...
Waiting for SSH to be available...
Detecting the provisioner...
Provisioning with ubuntu(systemd)...
Installing Docker...
Copying certs to the local machine directory...
Copying certs to the remote machine...
Setting Docker configuration on the remote daemon...
Checking connection to Docker...
Docker is up and running!
To see how to connect your Docker Client to the Docker Engine running on this virtual machine, run: docker-machine env machine
```

## <a name="configure-your-docker-shell"></a><span data-ttu-id="23816-113">Configure your docker shell</span><span class="sxs-lookup"><span data-stu-id="23816-113">Configure your docker shell</span></span>
<span data-ttu-id="23816-114">Now, type `docker-machine env <VM name>` to see what you need to do to configure the shell.</span><span class="sxs-lookup"><span data-stu-id="23816-114">Now, type `docker-machine env <VM name>` to see what you need to do to configure the shell.</span></span> 

```bash
docker-machine env machine
```

<span data-ttu-id="23816-115">That prints the environment information, which looks something like this.</span><span class="sxs-lookup"><span data-stu-id="23816-115">That prints the environment information, which looks something like this.</span></span> <span data-ttu-id="23816-116">Note the IP address has been assigned, which you'll need to test the VM.</span><span class="sxs-lookup"><span data-stu-id="23816-116">Note the IP address has been assigned, which you'll need to test the VM.</span></span>

```bash
export DOCKER_TLS_VERIFY="1"
export DOCKER_HOST="tcp://191.237.46.90:2376"
export DOCKER_CERT_PATH="/Users/rasquill/.docker/machine/machines/machine"
export DOCKER_MACHINE_NAME="machine"
# Run this command to configure your shell:
# eval $(docker-machine env machine)
```

<span data-ttu-id="23816-117">You can either run the suggested configuration command, or you can set the environment variables yourself.</span><span class="sxs-lookup"><span data-stu-id="23816-117">You can either run the suggested configuration command, or you can set the environment variables yourself.</span></span> 

## <a name="run-a-container"></a><span data-ttu-id="23816-118">Run a container</span><span class="sxs-lookup"><span data-stu-id="23816-118">Run a container</span></span>
<span data-ttu-id="23816-119">Now you can run a simple web server to test whether all works correctly.</span><span class="sxs-lookup"><span data-stu-id="23816-119">Now you can run a simple web server to test whether all works correctly.</span></span> <span data-ttu-id="23816-120">Here we use a standard nginx image, specify that it should listen on port 80, and that if the VM restarts the container should restart as well (`--restart=always`).</span><span class="sxs-lookup"><span data-stu-id="23816-120">Here we use a standard nginx image, specify that it should listen on port 80, and that if the VM restarts the container should restart as well (`--restart=always`).</span></span> 

```bash
docker run -d -p 80:80 --restart=always nginx
```

<span data-ttu-id="23816-121">The output should look something like the following:</span><span class="sxs-lookup"><span data-stu-id="23816-121">The output should look something like the following:</span></span>

```bash
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

## <a name="test-the-container"></a><span data-ttu-id="23816-122">Test the container</span><span class="sxs-lookup"><span data-stu-id="23816-122">Test the container</span></span>
<span data-ttu-id="23816-123">Examine running containers using `docker ps`:</span><span class="sxs-lookup"><span data-stu-id="23816-123">Examine running containers using `docker ps`:</span></span>

```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                         NAMES
d5b78f27b335        nginx               "nginx -g 'daemon off"   5 minutes ago       Up 5 minutes        0.0.0.0:80->80/tcp, 443/tcp   goofy_mahavira
```

<span data-ttu-id="23816-124">And check to see the running container, type `docker-machine ip <VM name>` to find the IP address (if you forgot from the `env` command):</span><span class="sxs-lookup"><span data-stu-id="23816-124">And check to see the running container, type `docker-machine ip <VM name>` to find the IP address (if you forgot from the `env` command):</span></span>

![Running ngnix container](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/docker-machine/nginxsuccess.png)

## <a name="next-steps"></a><span data-ttu-id="23816-126">Next steps</span><span class="sxs-lookup"><span data-stu-id="23816-126">Next steps</span></span>
<span data-ttu-id="23816-127">If you're interested, you can try out the Azure [Docker VM Extension](dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) to do the same operation using the Azure CLI or Azure resource manager templates.</span><span class="sxs-lookup"><span data-stu-id="23816-127">If you're interested, you can try out the Azure [Docker VM Extension](dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) to do the same operation using the Azure CLI or Azure resource manager templates.</span></span> 

<span data-ttu-id="23816-128">For more examples of working with Docker, see [Working with Docker](https://github.com/Microsoft/HealthClinic.biz/wiki/Working-with-Docker) from the [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) 2015 Connect [demo](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/).</span><span class="sxs-lookup"><span data-stu-id="23816-128">For more examples of working with Docker, see [Working with Docker](https://github.com/Microsoft/HealthClinic.biz/wiki/Working-with-Docker) from the [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) 2015 Connect [demo](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/).</span></span> <span data-ttu-id="23816-129">For more quickstarts from the HealthClinic.biz demo, see [Azure Developer Tools Quickstarts](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts).</span><span class="sxs-lookup"><span data-stu-id="23816-129">For more quickstarts from the HealthClinic.biz demo, see [Azure Developer Tools Quickstarts](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts).</span></span>


