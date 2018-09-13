---
title: Use Docker Compose on a Linux VM in Azure | Microsoft Docs
description: How to use Docker and Compose on Linux virtual machines with the Azure CLI
services: virtual-machines-linux
documentationcenter: ''
author: cynthn
manager: jeconnoc
editor: ''
tags: azure-resource-manager
ms.assetid: 02ab8cf9-318d-4a28-9d0c-4a31dccc2a84
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 12/18/2017
ms.author: cynthn
ms.openlocfilehash: 3f67a492b8d9d7e64efc63d6a6dbac843696d829
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44787129"
---
# <a name="get-started-with-docker-and-compose-to-define-and-run-a-multi-container-application-in-azure"></a><span data-ttu-id="76ee5-103">Get started with Docker and Compose to define and run a multi-container application in Azure</span><span class="sxs-lookup"><span data-stu-id="76ee5-103">Get started with Docker and Compose to define and run a multi-container application in Azure</span></span>
<span data-ttu-id="76ee5-104">With [Compose](http://github.com/docker/compose), you use a simple text file to define an application consisting of multiple Docker containers.</span><span class="sxs-lookup"><span data-stu-id="76ee5-104">With [Compose](http://github.com/docker/compose), you use a simple text file to define an application consisting of multiple Docker containers.</span></span> <span data-ttu-id="76ee5-105">You then spin up your application in a single command that does everything to deploy your defined environment.</span><span class="sxs-lookup"><span data-stu-id="76ee5-105">You then spin up your application in a single command that does everything to deploy your defined environment.</span></span> <span data-ttu-id="76ee5-106">As an example, this article shows you how to quickly set up a WordPress blog with a backend MariaDB SQL database on an Ubuntu VM.</span><span class="sxs-lookup"><span data-stu-id="76ee5-106">As an example, this article shows you how to quickly set up a WordPress blog with a backend MariaDB SQL database on an Ubuntu VM.</span></span> <span data-ttu-id="76ee5-107">You can also use Compose to set up more complex applications.</span><span class="sxs-lookup"><span data-stu-id="76ee5-107">You can also use Compose to set up more complex applications.</span></span>


## <a name="set-up-a-linux-vm-as-a-docker-host"></a><span data-ttu-id="76ee5-108">Set up a Linux VM as a Docker host</span><span class="sxs-lookup"><span data-stu-id="76ee5-108">Set up a Linux VM as a Docker host</span></span>
<span data-ttu-id="76ee5-109">You can use various Azure procedures and available images or Resource Manager templates in the Azure Marketplace to create a Linux VM and set it up as a Docker host.</span><span class="sxs-lookup"><span data-stu-id="76ee5-109">You can use various Azure procedures and available images or Resource Manager templates in the Azure Marketplace to create a Linux VM and set it up as a Docker host.</span></span> <span data-ttu-id="76ee5-110">For example, see [Using the Docker VM Extension to deploy your environment](dockerextension.md) to quickly create an Ubuntu VM with the Azure Docker VM extension by using a [quickstart template](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span><span class="sxs-lookup"><span data-stu-id="76ee5-110">For example, see [Using the Docker VM Extension to deploy your environment](dockerextension.md) to quickly create an Ubuntu VM with the Azure Docker VM extension by using a [quickstart template](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> 

<span data-ttu-id="76ee5-111">When you use the Docker VM extension, your VM is automatically set up as a Docker host and Compose is already installed.</span><span class="sxs-lookup"><span data-stu-id="76ee5-111">When you use the Docker VM extension, your VM is automatically set up as a Docker host and Compose is already installed.</span></span>


### <a name="create-docker-host-with-azure-cli-20"></a><span data-ttu-id="76ee5-112">Create Docker host with Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="76ee5-112">Create Docker host with Azure CLI 2.0</span></span>
<span data-ttu-id="76ee5-113">Install the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in to an Azure account using [az login](/cli/azure/reference-index#az_login).</span><span class="sxs-lookup"><span data-stu-id="76ee5-113">Install the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in to an Azure account using [az login](/cli/azure/reference-index#az_login).</span></span>

<span data-ttu-id="76ee5-114">First, create a resource group for your Docker environment with [az group create](/cli/azure/group#az_group_create).</span><span class="sxs-lookup"><span data-stu-id="76ee5-114">First, create a resource group for your Docker environment with [az group create](/cli/azure/group#az_group_create).</span></span> <span data-ttu-id="76ee5-115">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span><span class="sxs-lookup"><span data-stu-id="76ee5-115">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="76ee5-116">Next, deploy a VM with [az group deployment create](/cli/azure/group/deployment#az_group_deployment_create) that includes the Azure Docker VM extension from [this Azure Resource Manager template on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span><span class="sxs-lookup"><span data-stu-id="76ee5-116">Next, deploy a VM with [az group deployment create](/cli/azure/group/deployment#az_group_deployment_create) that includes the Azure Docker VM extension from [this Azure Resource Manager template on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> <span data-ttu-id="76ee5-117">When prompted, provide your own unique values for *newStorageAccountName*, *adminUsername*, *adminPassword*, and *dnsNameForPublicIP*:</span><span class="sxs-lookup"><span data-stu-id="76ee5-117">When prompted, provide your own unique values for *newStorageAccountName*, *adminUsername*, *adminPassword*, and *dnsNameForPublicIP*:</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

<span data-ttu-id="76ee5-118">It takes a few minutes for the deployment to finish.</span><span class="sxs-lookup"><span data-stu-id="76ee5-118">It takes a few minutes for the deployment to finish.</span></span>


## <a name="verify-that-compose-is-installed"></a><span data-ttu-id="76ee5-119">Verify that Compose is installed</span><span class="sxs-lookup"><span data-stu-id="76ee5-119">Verify that Compose is installed</span></span>
<span data-ttu-id="76ee5-120">To view details of your VM, including the DNS name, use [az vm show](/cli/azure/vm#az_vm_show):</span><span class="sxs-lookup"><span data-stu-id="76ee5-120">To view details of your VM, including the DNS name, use [az vm show](/cli/azure/vm#az_vm_show):</span></span>

```azurecli
az vm show \
    --resource-group myResourceGroup \
    --name myDockerVM \
    --show-details \
    --query [fqdns] \
    --output tsv
```

<span data-ttu-id="76ee5-121">SSH to your new Docker host.</span><span class="sxs-lookup"><span data-stu-id="76ee5-121">SSH to your new Docker host.</span></span> <span data-ttu-id="76ee5-122">Provide your own username and DNS name from the preceding steps:</span><span class="sxs-lookup"><span data-stu-id="76ee5-122">Provide your own username and DNS name from the preceding steps:</span></span>

```bash
ssh azureuser@mypublicdns.eastus.cloudapp.azure.com
```

<span data-ttu-id="76ee5-123">To check that Compose is installed on the VM, run the following command:</span><span class="sxs-lookup"><span data-stu-id="76ee5-123">To check that Compose is installed on the VM, run the following command:</span></span>

```bash
docker-compose --version
```

<span data-ttu-id="76ee5-124">You see output similar to *docker-compose 1.6.2, build 4d72027*.</span><span class="sxs-lookup"><span data-stu-id="76ee5-124">You see output similar to *docker-compose 1.6.2, build 4d72027*.</span></span>

> [!TIP]
> <span data-ttu-id="76ee5-125">If you used another method to create a Docker host and need to install Compose yourself, see the [Compose documentation](https://github.com/docker/compose/blob/882dc673ce84b0b29cd59b6815cb93f74a6c4134/docs/install.md).</span><span class="sxs-lookup"><span data-stu-id="76ee5-125">If you used another method to create a Docker host and need to install Compose yourself, see the [Compose documentation](https://github.com/docker/compose/blob/882dc673ce84b0b29cd59b6815cb93f74a6c4134/docs/install.md).</span></span>


## <a name="create-a-docker-composeyml-configuration-file"></a><span data-ttu-id="76ee5-126">Create a docker-compose.yml configuration file</span><span class="sxs-lookup"><span data-stu-id="76ee5-126">Create a docker-compose.yml configuration file</span></span>
<span data-ttu-id="76ee5-127">Next you create a `docker-compose.yml` file, which is just a text configuration file, to define the Docker containers to run on the VM.</span><span class="sxs-lookup"><span data-stu-id="76ee5-127">Next you create a `docker-compose.yml` file, which is just a text configuration file, to define the Docker containers to run on the VM.</span></span> <span data-ttu-id="76ee5-128">The file specifies the image to run on each container (or it could be a build from a Dockerfile), necessary environment variables and dependencies, ports, and the links between containers.</span><span class="sxs-lookup"><span data-stu-id="76ee5-128">The file specifies the image to run on each container (or it could be a build from a Dockerfile), necessary environment variables and dependencies, ports, and the links between containers.</span></span> <span data-ttu-id="76ee5-129">For details on yml file syntax, see [Compose file reference](https://docs.docker.com/compose/compose-file/).</span><span class="sxs-lookup"><span data-stu-id="76ee5-129">For details on yml file syntax, see [Compose file reference](https://docs.docker.com/compose/compose-file/).</span></span>

<span data-ttu-id="76ee5-130">Create a *docker-compose.yml* file.</span><span class="sxs-lookup"><span data-stu-id="76ee5-130">Create a *docker-compose.yml* file.</span></span> <span data-ttu-id="76ee5-131">Use your favorite text editor to add some data to the file.</span><span class="sxs-lookup"><span data-stu-id="76ee5-131">Use your favorite text editor to add some data to the file.</span></span> <span data-ttu-id="76ee5-132">The following example creates the file with a prompt for `sensible-editor` to pick an editor that you wish to use:</span><span class="sxs-lookup"><span data-stu-id="76ee5-132">The following example creates the file with a prompt for `sensible-editor` to pick an editor that you wish to use:</span></span>

```bash
sensible-editor docker-compose.yml
```

<span data-ttu-id="76ee5-133">Paste the following example into your Docker Compose file.</span><span class="sxs-lookup"><span data-stu-id="76ee5-133">Paste the following example into your Docker Compose file.</span></span> <span data-ttu-id="76ee5-134">This configuration uses images from the [DockerHub Registry](https://registry.hub.docker.com/_/wordpress/) to install WordPress (the open source blogging and content management system) and a linked backend MariaDB SQL database.</span><span class="sxs-lookup"><span data-stu-id="76ee5-134">This configuration uses images from the [DockerHub Registry](https://registry.hub.docker.com/_/wordpress/) to install WordPress (the open source blogging and content management system) and a linked backend MariaDB SQL database.</span></span> <span data-ttu-id="76ee5-135">Enter your own *MYSQL_ROOT_PASSWORD* as follows:</span><span class="sxs-lookup"><span data-stu-id="76ee5-135">Enter your own *MYSQL_ROOT_PASSWORD* as follows:</span></span>

```sh
wordpress:
  image: wordpress
  links:
    - db:mysql
  ports:
    - 80:80

db:
  image: mariadb
  environment:
    MYSQL_ROOT_PASSWORD: <your password>
```

## <a name="start-the-containers-with-compose"></a><span data-ttu-id="76ee5-136">Start the containers with Compose</span><span class="sxs-lookup"><span data-stu-id="76ee5-136">Start the containers with Compose</span></span>
<span data-ttu-id="76ee5-137">In the same directory as your *docker-compose.yml* file, run the following command (depending on your environment, you might need to run `docker-compose` using `sudo`):</span><span class="sxs-lookup"><span data-stu-id="76ee5-137">In the same directory as your *docker-compose.yml* file, run the following command (depending on your environment, you might need to run `docker-compose` using `sudo`):</span></span>

```bash
docker-compose up -d
```

<span data-ttu-id="76ee5-138">This command starts the Docker containers specified in *docker-compose.yml*.</span><span class="sxs-lookup"><span data-stu-id="76ee5-138">This command starts the Docker containers specified in *docker-compose.yml*.</span></span> <span data-ttu-id="76ee5-139">It takes a minute or two for this step to complete.</span><span class="sxs-lookup"><span data-stu-id="76ee5-139">It takes a minute or two for this step to complete.</span></span> <span data-ttu-id="76ee5-140">You see output similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="76ee5-140">You see output similar to the following example:</span></span>

```bash
Creating wordpress_db_1...
Creating wordpress_wordpress_1...
...
```

> [!NOTE]
> <span data-ttu-id="76ee5-141">Be sure to use the **-d** option on start-up so that the containers run in the background continuously.</span><span class="sxs-lookup"><span data-stu-id="76ee5-141">Be sure to use the **-d** option on start-up so that the containers run in the background continuously.</span></span>


<span data-ttu-id="76ee5-142">To verify that the containers are up, type `docker-compose ps`.</span><span class="sxs-lookup"><span data-stu-id="76ee5-142">To verify that the containers are up, type `docker-compose ps`.</span></span> <span data-ttu-id="76ee5-143">You should see something like:</span><span class="sxs-lookup"><span data-stu-id="76ee5-143">You should see something like:</span></span>

```bash
        Name                       Command               State         Ports
-----------------------------------------------------------------------------------
azureuser_db_1          docker-entrypoint.sh mysqld      Up      3306/tcp
azureuser_wordpress_1   docker-entrypoint.sh apach ...   Up      0.0.0.0:80->80/tcp
```

<span data-ttu-id="76ee5-144">You can now connect to WordPress directly on the VM on port 80.</span><span class="sxs-lookup"><span data-stu-id="76ee5-144">You can now connect to WordPress directly on the VM on port 80.</span></span> <span data-ttu-id="76ee5-145">Open a web browser and enter the DNS name of your VM (such as `http://mypublicdns.eastus.cloudapp.azure.com`).</span><span class="sxs-lookup"><span data-stu-id="76ee5-145">Open a web browser and enter the DNS name of your VM (such as `http://mypublicdns.eastus.cloudapp.azure.com`).</span></span> <span data-ttu-id="76ee5-146">You should now see the WordPress start screen, where you can complete the installation and get started with the application.</span><span class="sxs-lookup"><span data-stu-id="76ee5-146">You should now see the WordPress start screen, where you can complete the installation and get started with the application.</span></span>

![WordPress start screen][wordpress_start]

## <a name="next-steps"></a><span data-ttu-id="76ee5-148">Next steps</span><span class="sxs-lookup"><span data-stu-id="76ee5-148">Next steps</span></span>
* <span data-ttu-id="76ee5-149">Go to the [Docker VM extension user guide](https://github.com/Azure/azure-docker-extension/blob/master/README.md) for more options to configure Docker and Compose in your Docker VM.</span><span class="sxs-lookup"><span data-stu-id="76ee5-149">Go to the [Docker VM extension user guide](https://github.com/Azure/azure-docker-extension/blob/master/README.md) for more options to configure Docker and Compose in your Docker VM.</span></span> <span data-ttu-id="76ee5-150">For example, one option is to put the Compose yml file (converted to JSON) directly in the configuration of the Docker VM extension.</span><span class="sxs-lookup"><span data-stu-id="76ee5-150">For example, one option is to put the Compose yml file (converted to JSON) directly in the configuration of the Docker VM extension.</span></span>
* <span data-ttu-id="76ee5-151">Check out the [Compose command-line reference](http://docs.docker.com/compose/reference/) and [user guide](http://docs.docker.com/compose/) for more examples of building and deploying multi-container apps.</span><span class="sxs-lookup"><span data-stu-id="76ee5-151">Check out the [Compose command-line reference](http://docs.docker.com/compose/reference/) and [user guide](http://docs.docker.com/compose/) for more examples of building and deploying multi-container apps.</span></span>
* <span data-ttu-id="76ee5-152">Use an Azure Resource Manager template, either your own or one contributed from the [community](https://azure.microsoft.com/documentation/templates/), to deploy an Azure VM with Docker and an application set up with Compose.</span><span class="sxs-lookup"><span data-stu-id="76ee5-152">Use an Azure Resource Manager template, either your own or one contributed from the [community](https://azure.microsoft.com/documentation/templates/), to deploy an Azure VM with Docker and an application set up with Compose.</span></span> <span data-ttu-id="76ee5-153">For example, the [Deploy a WordPress blog with Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-wordpress-mysql) template uses Docker and Compose to quickly deploy WordPress with a MySQL backend on an Ubuntu VM.</span><span class="sxs-lookup"><span data-stu-id="76ee5-153">For example, the [Deploy a WordPress blog with Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-wordpress-mysql) template uses Docker and Compose to quickly deploy WordPress with a MySQL backend on an Ubuntu VM.</span></span>
* <span data-ttu-id="76ee5-154">Try integrating Docker Compose with a Docker Swarm cluster.</span><span class="sxs-lookup"><span data-stu-id="76ee5-154">Try integrating Docker Compose with a Docker Swarm cluster.</span></span> <span data-ttu-id="76ee5-155">See [Using Compose with Swarm](https://docs.docker.com/compose/swarm/) for scenarios.</span><span class="sxs-lookup"><span data-stu-id="76ee5-155">See [Using Compose with Swarm](https://docs.docker.com/compose/swarm/) for scenarios.</span></span>

<!--Image references-->

[wordpress_start]: media/docker-compose-quickstart/WordPress.png
