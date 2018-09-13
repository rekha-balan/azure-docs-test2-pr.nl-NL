---
title: Use the Azure Docker VM extension with the Azure CLI 1.0 | Microsoft Docs
description: Learn how to use the Docker VM extension to quickly and securely deploy a Docker environment in Azure using Resource Manager templates.
services: virtual-machines-linux
documentationcenter: ''
author: iainfoulds
manager: timlt
editor: ''
ms.assetid: ''
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 86a683c6d5402a064c5f6ef2f9970849aacfca4d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540824"
---
# <a name="create-a-docker-environment-in-azure-using-the-docker-vm-extension-with-the-azure-cli-10"></a><span data-ttu-id="05a12-103">Create a Docker environment in Azure using the Docker VM extension with the Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="05a12-103">Create a Docker environment in Azure using the Docker VM extension with the Azure CLI 1.0</span></span>
<span data-ttu-id="05a12-104">Docker is a popular container management and imaging platform that allows you to quickly work with containers on Linux (and Windows as well).</span><span class="sxs-lookup"><span data-stu-id="05a12-104">Docker is a popular container management and imaging platform that allows you to quickly work with containers on Linux (and Windows as well).</span></span> <span data-ttu-id="05a12-105">In Azure, there are various ways you can deploy Docker according to your needs.</span><span class="sxs-lookup"><span data-stu-id="05a12-105">In Azure, there are various ways you can deploy Docker according to your needs.</span></span> <span data-ttu-id="05a12-106">This article focuses on using the Docker VM extension and Azure Resource Manager templates.</span><span class="sxs-lookup"><span data-stu-id="05a12-106">This article focuses on using the Docker VM extension and Azure Resource Manager templates.</span></span> 

<span data-ttu-id="05a12-107">For more information about the different deployment methods, including using Docker Machine and Azure Container Services, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="05a12-107">For more information about the different deployment methods, including using Docker Machine and Azure Container Services, see the following articles:</span></span>

* <span data-ttu-id="05a12-108">To quickly prototype an app, you can create a single Docker host using [Docker Machine](docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="05a12-108">To quickly prototype an app, you can create a single Docker host using [Docker Machine](docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="05a12-109">For larger, more stable environments, you can use the Azure Docker VM extension, which also supports [Docker Compose](https://docs.docker.com/compose/overview/) to generate consistent container deployments.</span><span class="sxs-lookup"><span data-stu-id="05a12-109">For larger, more stable environments, you can use the Azure Docker VM extension, which also supports [Docker Compose](https://docs.docker.com/compose/overview/) to generate consistent container deployments.</span></span> <span data-ttu-id="05a12-110">This article details using the Azure Docker VM extension.</span><span class="sxs-lookup"><span data-stu-id="05a12-110">This article details using the Azure Docker VM extension.</span></span>
* <span data-ttu-id="05a12-111">To build production-ready, scalable environments that provide additional scheduling and management tools, you can deploy a [Docker Swarm cluster on Azure Container Services](../../container-service/container-service-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="05a12-111">To build production-ready, scalable environments that provide additional scheduling and management tools, you can deploy a [Docker Swarm cluster on Azure Container Services](../../container-service/container-service-deployment.md).</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="05a12-112">CLI versions to complete the task</span><span class="sxs-lookup"><span data-stu-id="05a12-112">CLI versions to complete the task</span></span>
<span data-ttu-id="05a12-113">You can complete the task using one of the following CLI versions:</span><span class="sxs-lookup"><span data-stu-id="05a12-113">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="05a12-114">[Azure CLI 1.0](#azure-docker-vm-extension-overview) – our CLI for the classic and resource management deployment models (this article)</span><span class="sxs-lookup"><span data-stu-id="05a12-114">[Azure CLI 1.0](#azure-docker-vm-extension-overview) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="05a12-115">[Azure CLI 2.0](dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span><span class="sxs-lookup"><span data-stu-id="05a12-115">[Azure CLI 2.0](dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span> 

## <a name="azure-docker-vm-extension-overview"></a><span data-ttu-id="05a12-116">Azure Docker VM extension overview</span><span class="sxs-lookup"><span data-stu-id="05a12-116">Azure Docker VM extension overview</span></span>
<span data-ttu-id="05a12-117">The Azure Docker VM extension installs and configures the Docker daemon, Docker client, and Docker Compose in your Linux virtual machine (VM).</span><span class="sxs-lookup"><span data-stu-id="05a12-117">The Azure Docker VM extension installs and configures the Docker daemon, Docker client, and Docker Compose in your Linux virtual machine (VM).</span></span> <span data-ttu-id="05a12-118">By using the Azure Docker VM extension, you have more control and features than simply using Docker Machine or creating the Docker host yourself.</span><span class="sxs-lookup"><span data-stu-id="05a12-118">By using the Azure Docker VM extension, you have more control and features than simply using Docker Machine or creating the Docker host yourself.</span></span> <span data-ttu-id="05a12-119">These additional features, such as [Docker Compose](https://docs.docker.com/compose/overview/), make the Azure Docker VM extension suited for more robust developer or production environments.</span><span class="sxs-lookup"><span data-stu-id="05a12-119">These additional features, such as [Docker Compose](https://docs.docker.com/compose/overview/), make the Azure Docker VM extension suited for more robust developer or production environments.</span></span>

<span data-ttu-id="05a12-120">Azure Resource Manager templates define the entire structure of your environment.</span><span class="sxs-lookup"><span data-stu-id="05a12-120">Azure Resource Manager templates define the entire structure of your environment.</span></span> <span data-ttu-id="05a12-121">Templates allow you to create and configure resources such as the Docker host VMs, storage, Role-Based Access Controls (RBAC), and diagnostics.</span><span class="sxs-lookup"><span data-stu-id="05a12-121">Templates allow you to create and configure resources such as the Docker host VMs, storage, Role-Based Access Controls (RBAC), and diagnostics.</span></span> <span data-ttu-id="05a12-122">You can reuse these templates to create additional deployments in a consistent manner.</span><span class="sxs-lookup"><span data-stu-id="05a12-122">You can reuse these templates to create additional deployments in a consistent manner.</span></span> <span data-ttu-id="05a12-123">For more information about Azure Resource Manager and templates, see [Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="05a12-123">For more information about Azure Resource Manager and templates, see [Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span> 

## <a name="deploy-a-template-with-the-azure-docker-vm-extension"></a><span data-ttu-id="05a12-124">Deploy a template with the Azure Docker VM extension</span><span class="sxs-lookup"><span data-stu-id="05a12-124">Deploy a template with the Azure Docker VM extension</span></span>
<span data-ttu-id="05a12-125">Let's use an existing quickstart template to create an Ubuntu VM that uses the Azure Docker VM extension to install and configure the Docker host.</span><span class="sxs-lookup"><span data-stu-id="05a12-125">Let's use an existing quickstart template to create an Ubuntu VM that uses the Azure Docker VM extension to install and configure the Docker host.</span></span> <span data-ttu-id="05a12-126">You can view the template here: [Simple deployment of an Ubuntu VM with Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span><span class="sxs-lookup"><span data-stu-id="05a12-126">You can view the template here: [Simple deployment of an Ubuntu VM with Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> 

<span data-ttu-id="05a12-127">You need the [latest Azure CLI](../../cli-install-nodejs.md) installed and logged in using the Resource Manager mode as follows:</span><span class="sxs-lookup"><span data-stu-id="05a12-127">You need the [latest Azure CLI](../../cli-install-nodejs.md) installed and logged in using the Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="05a12-128">Deploy the template using the Azure CLI, specifying the template URI.</span><span class="sxs-lookup"><span data-stu-id="05a12-128">Deploy the template using the Azure CLI, specifying the template URI.</span></span> <span data-ttu-id="05a12-129">The following example creates a resource group named `myResourceGroup` in the `WestUS` location.</span><span class="sxs-lookup"><span data-stu-id="05a12-129">The following example creates a resource group named `myResourceGroup` in the `WestUS` location.</span></span> <span data-ttu-id="05a12-130">Use your own resource group name and location as follows:</span><span class="sxs-lookup"><span data-stu-id="05a12-130">Use your own resource group name and location as follows:</span></span>

```azurecli
azure group create --name myResourceGroup --location "West US" \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

<span data-ttu-id="05a12-131">Answer the prompts to name your storage account, provide a username and password, and provide a DNS name.</span><span class="sxs-lookup"><span data-stu-id="05a12-131">Answer the prompts to name your storage account, provide a username and password, and provide a DNS name.</span></span> <span data-ttu-id="05a12-132">The output is similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="05a12-132">The output is similar to the following example:</span></span>

```azurecli
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Updating resource group myResourceGroup
info:    Updated resource group myResourceGroup
info:    Supply values for the following parameters
newStorageAccountName: mystorageaccount
adminUsername: ops
adminPassword: P@ssword!
dnsNameForPublicIP: mypublicip
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "azuredeploy"
data:    Id:                  /subscriptions/guid/resourceGroups/myResourceGroup
data:    Name:                myResourceGroup
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags: null
data:
info:    group create command OK
```

<span data-ttu-id="05a12-133">The Azure CLI returns you to the prompt after only a few seconds, but your Docker host is still being created and configured by the Azure Docker VM extension.</span><span class="sxs-lookup"><span data-stu-id="05a12-133">The Azure CLI returns you to the prompt after only a few seconds, but your Docker host is still being created and configured by the Azure Docker VM extension.</span></span> <span data-ttu-id="05a12-134">It takes a few minutes for the deployment to finish.</span><span class="sxs-lookup"><span data-stu-id="05a12-134">It takes a few minutes for the deployment to finish.</span></span> <span data-ttu-id="05a12-135">You can view details about the Docker host status using the `azure vm show` command.</span><span class="sxs-lookup"><span data-stu-id="05a12-135">You can view details about the Docker host status using the `azure vm show` command.</span></span>

<span data-ttu-id="05a12-136">The following example checks the status of the VM named `myDockerVM` (the default name from the template - don't change this name) in the resource group named `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="05a12-136">The following example checks the status of the VM named `myDockerVM` (the default name from the template - don't change this name) in the resource group named `myResourceGroup`.</span></span> <span data-ttu-id="05a12-137">Enter the name of the resource group you created in the preceding step:</span><span class="sxs-lookup"><span data-stu-id="05a12-137">Enter the name of the resource group you created in the preceding step:</span></span>

```azurecli
azure vm show -g myResourceGroup -n myDockerVM
```

<span data-ttu-id="05a12-138">The output of the `azure vm show` command is similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="05a12-138">The output of the `azure vm show` command is similar to the following example:</span></span>

```azurecli
info:    Executing command vm show
+ Looking up the VM "myDockerVM"
+ Looking up the NIC "myVMNicD"
+ Looking up the public ip "myPublicIPD"
data:    Id                              :/subscriptions/guid/resourceGroups/myresourcegroup/providers/Microsoft.Compute/virtualMachines/MyDockerVM
data:    ProvisioningState               :Succeeded
data:    Name                            :MyDockerVM
data:    Location                        :westus
data:    Type                            :Microsoft.Compute/virtualMachines
[...]
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Primary                   :true
data:          MAC Address               :00-0D-3A-33-D3-95
data:          Provisioning State        :Succeeded
data:          Name                      :myVMNicD
data:          Location                  :westus
data:            Public IP address       :13.91.107.235
data:            FQDN                    :mypublicip.westus.cloudapp.azure.com]
data:
data:    Diagnostics Instance View:
info:    vm show command OK
```

<span data-ttu-id="05a12-139">Near the top of the output, you see the `ProvisioningState` of the VM.</span><span class="sxs-lookup"><span data-stu-id="05a12-139">Near the top of the output, you see the `ProvisioningState` of the VM.</span></span> <span data-ttu-id="05a12-140">When this displays `Succeeded`, the deployment has finished and you can SSH to the VM.</span><span class="sxs-lookup"><span data-stu-id="05a12-140">When this displays `Succeeded`, the deployment has finished and you can SSH to the VM.</span></span>

<span data-ttu-id="05a12-141">Towards the end of the output, `FQDN` displays the fully qualified domain name of your Docker host.</span><span class="sxs-lookup"><span data-stu-id="05a12-141">Towards the end of the output, `FQDN` displays the fully qualified domain name of your Docker host.</span></span> <span data-ttu-id="05a12-142">This FQDN is what you use to SSH to your Docker host in the remaining steps.</span><span class="sxs-lookup"><span data-stu-id="05a12-142">This FQDN is what you use to SSH to your Docker host in the remaining steps.</span></span>

## <a name="deploy-your-first-nginx-container"></a><span data-ttu-id="05a12-143">Deploy your first nginx container</span><span class="sxs-lookup"><span data-stu-id="05a12-143">Deploy your first nginx container</span></span>
<span data-ttu-id="05a12-144">Once the deployment has finished, SSH to your new Docker host from your local computer.</span><span class="sxs-lookup"><span data-stu-id="05a12-144">Once the deployment has finished, SSH to your new Docker host from your local computer.</span></span> <span data-ttu-id="05a12-145">Enter your own username and FQDN as follows:</span><span class="sxs-lookup"><span data-stu-id="05a12-145">Enter your own username and FQDN as follows:</span></span>

```bash
ssh ops@mypublicip.westus.cloudapp.azure.com
```

<span data-ttu-id="05a12-146">Once logged in to the Docker host, let's run an nginx container:</span><span class="sxs-lookup"><span data-stu-id="05a12-146">Once logged in to the Docker host, let's run an nginx container:</span></span>

```bash
sudo docker run -d -p 80:80 nginx
```

<span data-ttu-id="05a12-147">The output is similar to the following example as the nginx image is downloaded and a container started:</span><span class="sxs-lookup"><span data-stu-id="05a12-147">The output is similar to the following example as the nginx image is downloaded and a container started:</span></span>

```bash
Unable to find image 'nginx:latest' locally
latest: Pulling from library/nginx
efd26ecc9548: Pull complete
a3ed95caeb02: Pull complete
a48df1751a97: Pull complete
8ddc2d7beb91: Pull complete
Digest: sha256:2ca2638e55319b7bc0c7d028209ea69b1368e95b01383e66dfe7e4f43780926d
Status: Downloaded newer image for nginx:latest
b6ed109fb743a762ff21a4606dd38d3e5d35aff43fa7f12e8d4ed1d920b0cd74
```

<span data-ttu-id="05a12-148">Check the status of the containers running on your Docker host as follows:</span><span class="sxs-lookup"><span data-stu-id="05a12-148">Check the status of the containers running on your Docker host as follows:</span></span>

```bash
sudo docker ps
```

<span data-ttu-id="05a12-149">The output is similar to the following example, showing that the nginx container is running and TCP ports 80 and 443 and being forwarded:</span><span class="sxs-lookup"><span data-stu-id="05a12-149">The output is similar to the following example, showing that the nginx container is running and TCP ports 80 and 443 and being forwarded:</span></span>

```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED              STATUS              PORTS                         NAMES
b6ed109fb743        nginx               "nginx -g 'daemon off"   About a minute ago   Up About a minute   0.0.0.0:80->80/tcp, 443/tcp   adoring_payne
```

<span data-ttu-id="05a12-150">To see your container in action, open up a web browser and enter the FQDN name of your Docker host:</span><span class="sxs-lookup"><span data-stu-id="05a12-150">To see your container in action, open up a web browser and enter the FQDN name of your Docker host:</span></span>

![Running ngnix container](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/dockerextension/nginxrunning.png)

## <a name="azure-docker-vm-extension-template-reference"></a><span data-ttu-id="05a12-152">Azure Docker VM extension template reference</span><span class="sxs-lookup"><span data-stu-id="05a12-152">Azure Docker VM extension template reference</span></span>
<span data-ttu-id="05a12-153">The previous example uses an existing quickstart template.</span><span class="sxs-lookup"><span data-stu-id="05a12-153">The previous example uses an existing quickstart template.</span></span> <span data-ttu-id="05a12-154">You can also deploy the Azure Docker VM extension with your own Resource Manager templates.</span><span class="sxs-lookup"><span data-stu-id="05a12-154">You can also deploy the Azure Docker VM extension with your own Resource Manager templates.</span></span> <span data-ttu-id="05a12-155">To do so, add the following to your Resource Manager templates, defining the `vmName` of your VM appropriately:</span><span class="sxs-lookup"><span data-stu-id="05a12-155">To do so, add the following to your Resource Manager templates, defining the `vmName` of your VM appropriately:</span></span>

```json
{
  "type": "Microsoft.Compute/virtualMachines/extensions",
  "name": "[concat(variables('vmName'), '/DockerExtension'))]",
  "apiVersion": "2015-05-01-preview",
  "location": "[parameters('location')]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
  ],
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "DockerExtension",
    "typeHandlerVersion": "1.1",
    "autoUpgradeMinorVersion": true,
    "settings": {},
    "protectedSettings": {}
  }
}
```

<span data-ttu-id="05a12-156">You can find more detailed walkthrough on using Resource Manager templates by reading [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="05a12-156">You can find more detailed walkthrough on using Resource Manager templates by reading [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="05a12-157">Next steps</span><span class="sxs-lookup"><span data-stu-id="05a12-157">Next steps</span></span>
<span data-ttu-id="05a12-158">You may wish to [configure the Docker daemon TCP port](https://docs.docker.com/engine/reference/commandline/dockerd/#/bind-docker-to-another-hostport-or-a-unix-socket), understand [Docker security](https://docs.docker.com/engine/security/security/), or deploy containers using [Docker Compose](https://docs.docker.com/compose/overview/).</span><span class="sxs-lookup"><span data-stu-id="05a12-158">You may wish to [configure the Docker daemon TCP port](https://docs.docker.com/engine/reference/commandline/dockerd/#/bind-docker-to-another-hostport-or-a-unix-socket), understand [Docker security](https://docs.docker.com/engine/security/security/), or deploy containers using [Docker Compose](https://docs.docker.com/compose/overview/).</span></span> <span data-ttu-id="05a12-159">For more information on the Azure Docker VM Extension itself, see the [GitHub project](https://github.com/Azure/azure-docker-extension/).</span><span class="sxs-lookup"><span data-stu-id="05a12-159">For more information on the Azure Docker VM Extension itself, see the [GitHub project](https://github.com/Azure/azure-docker-extension/).</span></span>

<span data-ttu-id="05a12-160">Read more information about the additional Docker deployment options in Azure:</span><span class="sxs-lookup"><span data-stu-id="05a12-160">Read more information about the additional Docker deployment options in Azure:</span></span>

* [<span data-ttu-id="05a12-161">Use Docker Machine with the Azure driver</span><span class="sxs-lookup"><span data-stu-id="05a12-161">Use Docker Machine with the Azure driver</span></span>](docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)  
* <span data-ttu-id="05a12-162">[Get Started with Docker and Compose to define and run a multi-container application on an Azure virtual machine](docker-compose-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="05a12-162">[Get Started with Docker and Compose to define and run a multi-container application on an Azure virtual machine](docker-compose-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* [<span data-ttu-id="05a12-163">Deploy an Azure Container Service cluster</span><span class="sxs-lookup"><span data-stu-id="05a12-163">Deploy an Azure Container Service cluster</span></span>](../../container-service/container-service-deployment.md)


