---
title: Use the Azure Docker VM extension | Microsoft Docs
description: Learn how to use the Docker VM extension to quickly and securely deploy a Docker environment in Azure using Resource Manager templates and the Azure CLI 2.0
services: virtual-machines-linux
documentationcenter: ''
author: iainfoulds
manager: timlt
editor: ''
ms.assetid: 936d67d7-6921-4275-bf11-1e0115e66b7f
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/23/2017
ms.author: iainfou
ms.openlocfilehash: 6cb38ae2ed1da1cd86dbb84f3f4948ff3c06e297
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550021"
---
# <a name="create-a-docker-environment-in-azure-using-the-docker-vm-extension"></a><span data-ttu-id="f1bbe-103">Create a Docker environment in Azure using the Docker VM extension</span><span class="sxs-lookup"><span data-stu-id="f1bbe-103">Create a Docker environment in Azure using the Docker VM extension</span></span>
<span data-ttu-id="f1bbe-104">Docker is a popular container management and imaging platform that allows you to quickly work with containers on Linux.</span><span class="sxs-lookup"><span data-stu-id="f1bbe-104">Docker is a popular container management and imaging platform that allows you to quickly work with containers on Linux.</span></span> <span data-ttu-id="f1bbe-105">In Azure, there are various ways you can deploy Docker according to your needs.</span><span class="sxs-lookup"><span data-stu-id="f1bbe-105">In Azure, there are various ways you can deploy Docker according to your needs.</span></span> <span data-ttu-id="f1bbe-106">This article focuses on using the Docker VM extension and Azure Resource Manager templates with the Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="f1bbe-106">This article focuses on using the Docker VM extension and Azure Resource Manager templates with the Azure CLI 2.0.</span></span> <span data-ttu-id="f1bbe-107">You can also perform these steps with the [Azure CLI 1.0](dockerextension-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f1bbe-107">You can also perform these steps with the [Azure CLI 1.0](dockerextension-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="azure-docker-vm-extension-overview"></a><span data-ttu-id="f1bbe-108">Azure Docker VM extension overview</span><span class="sxs-lookup"><span data-stu-id="f1bbe-108">Azure Docker VM extension overview</span></span>
<span data-ttu-id="f1bbe-109">The Azure Docker VM extension installs and configures the Docker daemon, Docker client, and Docker Compose in your Linux virtual machine (VM).</span><span class="sxs-lookup"><span data-stu-id="f1bbe-109">The Azure Docker VM extension installs and configures the Docker daemon, Docker client, and Docker Compose in your Linux virtual machine (VM).</span></span> <span data-ttu-id="f1bbe-110">By using the Azure Docker VM extension, you have more control and features than simply using Docker Machine or creating the Docker host yourself.</span><span class="sxs-lookup"><span data-stu-id="f1bbe-110">By using the Azure Docker VM extension, you have more control and features than simply using Docker Machine or creating the Docker host yourself.</span></span> <span data-ttu-id="f1bbe-111">These additional features, such as [Docker Compose](https://docs.docker.com/compose/overview/), make the Azure Docker VM extension suited for more robust developer or production environments.</span><span class="sxs-lookup"><span data-stu-id="f1bbe-111">These additional features, such as [Docker Compose](https://docs.docker.com/compose/overview/), make the Azure Docker VM extension suited for more robust developer or production environments.</span></span>

<span data-ttu-id="f1bbe-112">For more information about the different deployment methods, including using Docker Machine and Azure Container Services, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="f1bbe-112">For more information about the different deployment methods, including using Docker Machine and Azure Container Services, see the following articles:</span></span>

* <span data-ttu-id="f1bbe-113">To quickly prototype an app, you can create a single Docker host using [Docker Machine](docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f1bbe-113">To quickly prototype an app, you can create a single Docker host using [Docker Machine](docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="f1bbe-114">To build production-ready, scalable environments that provide additional scheduling and management tools, you can deploy a [Docker Swarm cluster on Azure Container Services](../../container-service/container-service-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="f1bbe-114">To build production-ready, scalable environments that provide additional scheduling and management tools, you can deploy a [Docker Swarm cluster on Azure Container Services](../../container-service/container-service-deployment.md).</span></span>

## <a name="deploy-a-template-with-the-azure-docker-vm-extension"></a><span data-ttu-id="f1bbe-115">Deploy a template with the Azure Docker VM extension</span><span class="sxs-lookup"><span data-stu-id="f1bbe-115">Deploy a template with the Azure Docker VM extension</span></span>
<span data-ttu-id="f1bbe-116">Let's use an existing quickstart template to create an Ubuntu VM that uses the Azure Docker VM extension to install and configure the Docker host.</span><span class="sxs-lookup"><span data-stu-id="f1bbe-116">Let's use an existing quickstart template to create an Ubuntu VM that uses the Azure Docker VM extension to install and configure the Docker host.</span></span> <span data-ttu-id="f1bbe-117">You can view the template here: [Simple deployment of an Ubuntu VM with Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span><span class="sxs-lookup"><span data-stu-id="f1bbe-117">You can view the template here: [Simple deployment of an Ubuntu VM with Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> <span data-ttu-id="f1bbe-118">You need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="f1bbe-118">You need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="f1bbe-119">First, create a resource group with [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="f1bbe-119">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="f1bbe-120">The following example creates a resource group named `myResourceGroup` in the `West US` location:</span><span class="sxs-lookup"><span data-stu-id="f1bbe-120">The following example creates a resource group named `myResourceGroup` in the `West US` location:</span></span>

```azurecli
 az group create --name myResourceGroup --location westus
```

<span data-ttu-id="f1bbe-121">Next, deploy a VM with [az group deployment create](/cli/azure/group/deployment#create) that includes the Azure Docker VM extension from [this Azure Resource Manager template on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span><span class="sxs-lookup"><span data-stu-id="f1bbe-121">Next, deploy a VM with [az group deployment create](/cli/azure/group/deployment#create) that includes the Azure Docker VM extension from [this Azure Resource Manager template on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> <span data-ttu-id="f1bbe-122">Provide your own values for `newStorageAccountName`, `adminUsername`, `adminPassword`, and `dnsNameForPublicIP` as follows:</span><span class="sxs-lookup"><span data-stu-id="f1bbe-122">Provide your own values for `newStorageAccountName`, `adminUsername`, `adminPassword`, and `dnsNameForPublicIP` as follows:</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"newStorageAccountName": {"value": "mystorageaccount"},
    "adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "dnsNameForPublicIP": {"value": "mypublicdns"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

<span data-ttu-id="f1bbe-123">It takes a few minutes for the deployment to finish.</span><span class="sxs-lookup"><span data-stu-id="f1bbe-123">It takes a few minutes for the deployment to finish.</span></span> <span data-ttu-id="f1bbe-124">Once the deployment is finished, [move to next step](#deploy-your-first-nginx-container) to SSH to your VM.</span><span class="sxs-lookup"><span data-stu-id="f1bbe-124">Once the deployment is finished, [move to next step](#deploy-your-first-nginx-container) to SSH to your VM.</span></span> 

<span data-ttu-id="f1bbe-125">Optionally, to instead return control to the prompt and let the deployment continue in the background, add the `--no-wait` flag to the preceding command.</span><span class="sxs-lookup"><span data-stu-id="f1bbe-125">Optionally, to instead return control to the prompt and let the deployment continue in the background, add the `--no-wait` flag to the preceding command.</span></span> <span data-ttu-id="f1bbe-126">This process allows you to perform other work in the CLI while the deployment continues for a few minutes.</span><span class="sxs-lookup"><span data-stu-id="f1bbe-126">This process allows you to perform other work in the CLI while the deployment continues for a few minutes.</span></span> <span data-ttu-id="f1bbe-127">You can then view details about the Docker host status with [az vm show](/cli/azure/vm#show).</span><span class="sxs-lookup"><span data-stu-id="f1bbe-127">You can then view details about the Docker host status with [az vm show](/cli/azure/vm#show).</span></span> <span data-ttu-id="f1bbe-128">The following example checks the status of the VM named `myDockerVM` (the default name from the template - don't change this name) in the resource group named `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="f1bbe-128">The following example checks the status of the VM named `myDockerVM` (the default name from the template - don't change this name) in the resource group named `myResourceGroup`:</span></span>

```azurecli
az vm show --resource-group myResourceGroup --name myDockerVM \
  --query [provisioningState] --output tsv
```

<span data-ttu-id="f1bbe-129">When this command returns `Succeeded`, the deployment has finished and you can SSH to the VM in the following step.</span><span class="sxs-lookup"><span data-stu-id="f1bbe-129">When this command returns `Succeeded`, the deployment has finished and you can SSH to the VM in the following step.</span></span>

## <a name="deploy-your-first-nginx-container"></a><span data-ttu-id="f1bbe-130">Deploy your first nginx container</span><span class="sxs-lookup"><span data-stu-id="f1bbe-130">Deploy your first nginx container</span></span>
<span data-ttu-id="f1bbe-131">To view details of your VM, including the DNS name, use `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv`.</span><span class="sxs-lookup"><span data-stu-id="f1bbe-131">To view details of your VM, including the DNS name, use `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv`.</span></span> <span data-ttu-id="f1bbe-132">SSH to your new Docker host from your local computer as follows:</span><span class="sxs-lookup"><span data-stu-id="f1bbe-132">SSH to your new Docker host from your local computer as follows:</span></span>

```bash
ssh azureuser@mypublicdns.westus.cloudapp.azure.com
```

<span data-ttu-id="f1bbe-133">Once logged in to the Docker host, let's run an nginx container:</span><span class="sxs-lookup"><span data-stu-id="f1bbe-133">Once logged in to the Docker host, let's run an nginx container:</span></span>

```bash
sudo docker run -d -p 80:80 nginx
```

<span data-ttu-id="f1bbe-134">The output is similar to the following example as the nginx image is downloaded and a container started:</span><span class="sxs-lookup"><span data-stu-id="f1bbe-134">The output is similar to the following example as the nginx image is downloaded and a container started:</span></span>

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

<span data-ttu-id="f1bbe-135">Check the status of the containers running on your Docker host as follows:</span><span class="sxs-lookup"><span data-stu-id="f1bbe-135">Check the status of the containers running on your Docker host as follows:</span></span>

```bash
sudo docker ps
```

<span data-ttu-id="f1bbe-136">The output is similar to the following example, showing that the nginx container is running and TCP ports 80 and 443 and being forwarded:</span><span class="sxs-lookup"><span data-stu-id="f1bbe-136">The output is similar to the following example, showing that the nginx container is running and TCP ports 80 and 443 and being forwarded:</span></span>

```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED              STATUS              PORTS                         NAMES
b6ed109fb743        nginx               "nginx -g 'daemon off"   About a minute ago   Up About a minute   0.0.0.0:80->80/tcp, 443/tcp   adoring_payne
```

<span data-ttu-id="f1bbe-137">To see your container in action, open up a web browser and enter the DNS name of your Docker host:</span><span class="sxs-lookup"><span data-stu-id="f1bbe-137">To see your container in action, open up a web browser and enter the DNS name of your Docker host:</span></span>

![Running ngnix container](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/dockerextension/nginxrunning.png)

## <a name="azure-docker-vm-extension-template-reference"></a><span data-ttu-id="f1bbe-139">Azure Docker VM extension template reference</span><span class="sxs-lookup"><span data-stu-id="f1bbe-139">Azure Docker VM extension template reference</span></span>
<span data-ttu-id="f1bbe-140">The previous example uses an existing quickstart template.</span><span class="sxs-lookup"><span data-stu-id="f1bbe-140">The previous example uses an existing quickstart template.</span></span> <span data-ttu-id="f1bbe-141">You can also deploy the Azure Docker VM extension with your own Resource Manager templates.</span><span class="sxs-lookup"><span data-stu-id="f1bbe-141">You can also deploy the Azure Docker VM extension with your own Resource Manager templates.</span></span> <span data-ttu-id="f1bbe-142">To do so, add the following to your Resource Manager templates, defining the `vmName` of your VM appropriately:</span><span class="sxs-lookup"><span data-stu-id="f1bbe-142">To do so, add the following to your Resource Manager templates, defining the `vmName` of your VM appropriately:</span></span>

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

<span data-ttu-id="f1bbe-143">You can find more detailed walkthrough on using Resource Manager templates by reading [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f1bbe-143">You can find more detailed walkthrough on using Resource Manager templates by reading [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f1bbe-144">Next steps</span><span class="sxs-lookup"><span data-stu-id="f1bbe-144">Next steps</span></span>
<span data-ttu-id="f1bbe-145">You may wish to [configure the Docker daemon TCP port](https://docs.docker.com/engine/reference/commandline/dockerd/#/bind-docker-to-another-hostport-or-a-unix-socket), understand [Docker security](https://docs.docker.com/engine/security/security/), or deploy containers using [Docker Compose](https://docs.docker.com/compose/overview/).</span><span class="sxs-lookup"><span data-stu-id="f1bbe-145">You may wish to [configure the Docker daemon TCP port](https://docs.docker.com/engine/reference/commandline/dockerd/#/bind-docker-to-another-hostport-or-a-unix-socket), understand [Docker security](https://docs.docker.com/engine/security/security/), or deploy containers using [Docker Compose](https://docs.docker.com/compose/overview/).</span></span> <span data-ttu-id="f1bbe-146">For more information on the Azure Docker VM Extension itself, see the [GitHub project](https://github.com/Azure/azure-docker-extension/).</span><span class="sxs-lookup"><span data-stu-id="f1bbe-146">For more information on the Azure Docker VM Extension itself, see the [GitHub project](https://github.com/Azure/azure-docker-extension/).</span></span>

<span data-ttu-id="f1bbe-147">Read more information about the additional Docker deployment options in Azure:</span><span class="sxs-lookup"><span data-stu-id="f1bbe-147">Read more information about the additional Docker deployment options in Azure:</span></span>

* [<span data-ttu-id="f1bbe-148">Use Docker Machine with the Azure driver</span><span class="sxs-lookup"><span data-stu-id="f1bbe-148">Use Docker Machine with the Azure driver</span></span>](docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)  
* <span data-ttu-id="f1bbe-149">[Get Started with Docker and Compose to define and run a multi-container application on an Azure virtual machine](docker-compose-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f1bbe-149">[Get Started with Docker and Compose to define and run a multi-container application on an Azure virtual machine](docker-compose-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* [<span data-ttu-id="f1bbe-150">Deploy an Azure Container Service cluster</span><span class="sxs-lookup"><span data-stu-id="f1bbe-150">Deploy an Azure Container Service cluster</span></span>](../../container-service/container-service-deployment.md)


