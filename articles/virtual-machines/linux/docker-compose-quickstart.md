---
title: Use Docker Compose on a Linux VM in Azure | Microsoft Docs
description: How to use Docker and Compose on Linux virtual machines with the Azure CLI
services: virtual-machines-linux
documentationcenter: ''
author: iainfoulds
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: 02ab8cf9-318d-4a28-9d0c-4a31dccc2a84
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/13/2017
ms.author: iainfou
ms.openlocfilehash: d922a7d3402c5ad080c29c25ade61a64abdf0818
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563356"
---
# <a name="get-started-with-docker-and-compose-to-define-and-run-a-multi-container-application-in-azure"></a><span data-ttu-id="4838e-103">Get started with Docker and Compose to define and run a multi-container application in Azure</span><span class="sxs-lookup"><span data-stu-id="4838e-103">Get started with Docker and Compose to define and run a multi-container application in Azure</span></span>
<span data-ttu-id="4838e-104">With [Compose](http://github.com/docker/compose), you use a simple text file to define an application consisting of multiple Docker containers.</span><span class="sxs-lookup"><span data-stu-id="4838e-104">With [Compose](http://github.com/docker/compose), you use a simple text file to define an application consisting of multiple Docker containers.</span></span> <span data-ttu-id="4838e-105">You then spin up your application in a single command that does everything to deploy your defined environment.</span><span class="sxs-lookup"><span data-stu-id="4838e-105">You then spin up your application in a single command that does everything to deploy your defined environment.</span></span> <span data-ttu-id="4838e-106">As an example, this article shows you how to quickly set up a WordPress blog with a backend MariaDB SQL database on an Ubuntu VM.</span><span class="sxs-lookup"><span data-stu-id="4838e-106">As an example, this article shows you how to quickly set up a WordPress blog with a backend MariaDB SQL database on an Ubuntu VM.</span></span> <span data-ttu-id="4838e-107">You can also use Compose to set up more complex applications.</span><span class="sxs-lookup"><span data-stu-id="4838e-107">You can also use Compose to set up more complex applications.</span></span>

## <a name="step-1-set-up-a-linux-vm-as-a-docker-host"></a><span data-ttu-id="4838e-108">Step 1: Set up a Linux VM as a Docker host</span><span class="sxs-lookup"><span data-stu-id="4838e-108">Step 1: Set up a Linux VM as a Docker host</span></span>
<span data-ttu-id="4838e-109">You can use various Azure procedures and available images or Resource Manager templates in the Azure Marketplace to create a Linux VM and set it up as a Docker host.</span><span class="sxs-lookup"><span data-stu-id="4838e-109">You can use various Azure procedures and available images or Resource Manager templates in the Azure Marketplace to create a Linux VM and set it up as a Docker host.</span></span> <span data-ttu-id="4838e-110">For example, see [Using the Docker VM Extension to deploy your environment](dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) to quickly create an Ubuntu VM with the Azure Docker VM extension by using a [quickstart template](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span><span class="sxs-lookup"><span data-stu-id="4838e-110">For example, see [Using the Docker VM Extension to deploy your environment](dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) to quickly create an Ubuntu VM with the Azure Docker VM extension by using a [quickstart template](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> 

<span data-ttu-id="4838e-111">When you use the Docker VM extension, your VM is automatically set up as a Docker host and Compose is already installed.</span><span class="sxs-lookup"><span data-stu-id="4838e-111">When you use the Docker VM extension, your VM is automatically set up as a Docker host and Compose is already installed.</span></span> <span data-ttu-id="4838e-112">You can create a VM and use the Docker VM extension using one of the following CLI versions:</span><span class="sxs-lookup"><span data-stu-id="4838e-112">You can create a VM and use the Docker VM extension using one of the following CLI versions:</span></span>

- <span data-ttu-id="4838e-113">[Azure CLI 2.0](#azure-cli-20) - our next generation CLI for the resource management deployment model</span><span class="sxs-lookup"><span data-stu-id="4838e-113">[Azure CLI 2.0](#azure-cli-20) - our next generation CLI for the resource management deployment model</span></span>
- <span data-ttu-id="4838e-114">[Azure CLI 1.0](#azure-cli-10) – our CLI for the classic and resource management deployment models</span><span class="sxs-lookup"><span data-stu-id="4838e-114">[Azure CLI 1.0](#azure-cli-10) – our CLI for the classic and resource management deployment models</span></span>

### <a name="azure-cli-20"></a><span data-ttu-id="4838e-115">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="4838e-115">Azure CLI 2.0</span></span>
<span data-ttu-id="4838e-116">Install the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in to an Azure account using [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="4838e-116">Install the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="4838e-117">First, create a resource group for your Docker environment with [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="4838e-117">First, create a resource group for your Docker environment with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="4838e-118">The following example creates a resource group named `myResourceGroup` in the `West US` location:</span><span class="sxs-lookup"><span data-stu-id="4838e-118">The following example creates a resource group named `myResourceGroup` in the `West US` location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="4838e-119">Next, deploy a VM with [az group deployment create](/cli/azure/group/deployment#create) that includes the Azure Docker VM extension from [this Azure Resource Manager template on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span><span class="sxs-lookup"><span data-stu-id="4838e-119">Next, deploy a VM with [az group deployment create](/cli/azure/group/deployment#create) that includes the Azure Docker VM extension from [this Azure Resource Manager template on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> <span data-ttu-id="4838e-120">Provide your own values for `newStorageAccountName`, `adminUsername`, `adminPassword`, and `dnsNameForPublicIP`:</span><span class="sxs-lookup"><span data-stu-id="4838e-120">Provide your own values for `newStorageAccountName`, `adminUsername`, `adminPassword`, and `dnsNameForPublicIP`:</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"newStorageAccountName": {"value": "mystorageaccount"},
    "adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "dnsNameForPublicIP": {"value": "mypublicdns"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

<span data-ttu-id="4838e-121">It takes a few minutes for the deployment to finish.</span><span class="sxs-lookup"><span data-stu-id="4838e-121">It takes a few minutes for the deployment to finish.</span></span> <span data-ttu-id="4838e-122">Once the deployment is finished, [move to next step](#step-2-verify-that-compose-is-installed) to SSH to your VM.</span><span class="sxs-lookup"><span data-stu-id="4838e-122">Once the deployment is finished, [move to next step](#step-2-verify-that-compose-is-installed) to SSH to your VM.</span></span> 

<span data-ttu-id="4838e-123">Optionally, to instead return control to the prompt and let the deployment continue in the background, add the `--no-wait` flag to the preceding command.</span><span class="sxs-lookup"><span data-stu-id="4838e-123">Optionally, to instead return control to the prompt and let the deployment continue in the background, add the `--no-wait` flag to the preceding command.</span></span> <span data-ttu-id="4838e-124">This process allows you to perform other work in the CLI while the deployment continues for a few minutes.</span><span class="sxs-lookup"><span data-stu-id="4838e-124">This process allows you to perform other work in the CLI while the deployment continues for a few minutes.</span></span> <span data-ttu-id="4838e-125">You can then view details about the Docker host status with [az vm show](/cli/azure/vm#show).</span><span class="sxs-lookup"><span data-stu-id="4838e-125">You can then view details about the Docker host status with [az vm show](/cli/azure/vm#show).</span></span> <span data-ttu-id="4838e-126">The following example checks the status of the VM named `myDockerVM` (the default name from the template - don't change this name) in the resource group named `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="4838e-126">The following example checks the status of the VM named `myDockerVM` (the default name from the template - don't change this name) in the resource group named `myResourceGroup`:</span></span>

```azurecli
az vm show --resource-group myResourceGroup --name myDockerVM \
  --query [provisioningState] --output tsv
```

<span data-ttu-id="4838e-127">When this command returns `Succeeded`, the deployment has finished and you can SSH to the VM in the following step.</span><span class="sxs-lookup"><span data-stu-id="4838e-127">When this command returns `Succeeded`, the deployment has finished and you can SSH to the VM in the following step.</span></span>

### <a name="azure-cli-10"></a><span data-ttu-id="4838e-128">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="4838e-128">Azure CLI 1.0</span></span>
<span data-ttu-id="4838e-129">Install the latest [Azure CLI 1.0](../../cli-install-nodejs.md) and log in to an Azure account.</span><span class="sxs-lookup"><span data-stu-id="4838e-129">Install the latest [Azure CLI 1.0](../../cli-install-nodejs.md) and log in to an Azure account.</span></span> <span data-ttu-id="4838e-130">Make sure that you are in Resource Manager mode to create the VM (`azure config mode arm`).</span><span class="sxs-lookup"><span data-stu-id="4838e-130">Make sure that you are in Resource Manager mode to create the VM (`azure config mode arm`).</span></span>

<span data-ttu-id="4838e-131">The following example creates a resource group named `myResourceGroup` in the `West US` location and deploys a VM with the Azure Docker VM extension.</span><span class="sxs-lookup"><span data-stu-id="4838e-131">The following example creates a resource group named `myResourceGroup` in the `West US` location and deploys a VM with the Azure Docker VM extension.</span></span> <span data-ttu-id="4838e-132">An [Azure Resource Manager template from GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu) is used to deploy the environment:</span><span class="sxs-lookup"><span data-stu-id="4838e-132">An [Azure Resource Manager template from GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu) is used to deploy the environment:</span></span>

```azurecli
azure group create --name myResourceGroup --location "West US" \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

<span data-ttu-id="4838e-133">The Azure CLI returns you to the prompt after only a few seconds, but your Docker host is still being created and configured.</span><span class="sxs-lookup"><span data-stu-id="4838e-133">The Azure CLI returns you to the prompt after only a few seconds, but your Docker host is still being created and configured.</span></span> <span data-ttu-id="4838e-134">It takes a few minutes for the deployment to finish.</span><span class="sxs-lookup"><span data-stu-id="4838e-134">It takes a few minutes for the deployment to finish.</span></span> <span data-ttu-id="4838e-135">You can view details about the Docker host status using the `azure vm show` command.</span><span class="sxs-lookup"><span data-stu-id="4838e-135">You can view details about the Docker host status using the `azure vm show` command.</span></span> <span data-ttu-id="4838e-136">The following example checks the status of the VM named `myDockerVM` (the default name from the template - don't change this name) in the resource group named `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="4838e-136">The following example checks the status of the VM named `myDockerVM` (the default name from the template - don't change this name) in the resource group named `myResourceGroup`.</span></span> <span data-ttu-id="4838e-137">Enter the name of the resource group you created in the preceding step:</span><span class="sxs-lookup"><span data-stu-id="4838e-137">Enter the name of the resource group you created in the preceding step:</span></span>

```azurecli
azure vm show --resource-group myResourceGroup --name myDockerVM
```

## <a name="step-2-verify-that-compose-is-installed"></a><span data-ttu-id="4838e-138">Step 2: Verify that Compose is installed</span><span class="sxs-lookup"><span data-stu-id="4838e-138">Step 2: Verify that Compose is installed</span></span>
<span data-ttu-id="4838e-139">Once the deployment is finished, SSH to your new Docker host using the DNS name you provided during deployment.</span><span class="sxs-lookup"><span data-stu-id="4838e-139">Once the deployment is finished, SSH to your new Docker host using the DNS name you provided during deployment.</span></span> <span data-ttu-id="4838e-140">You can use `azure vm show -g myResourceGroup -n myDockerVM` (Azure CLI 1.0) or `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv` (Azure CLI 2.0) to view details of your VM, including the DNS name.</span><span class="sxs-lookup"><span data-stu-id="4838e-140">You can use `azure vm show -g myResourceGroup -n myDockerVM` (Azure CLI 1.0) or `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv` (Azure CLI 2.0) to view details of your VM, including the DNS name.</span></span>

<span data-ttu-id="4838e-141">To check that Compose is installed on the VM, run the following command:</span><span class="sxs-lookup"><span data-stu-id="4838e-141">To check that Compose is installed on the VM, run the following command:</span></span>

```bash
docker-compose --version
```

<span data-ttu-id="4838e-142">You see output similar to `docker-compose 1.6.2, build 4d72027`.</span><span class="sxs-lookup"><span data-stu-id="4838e-142">You see output similar to `docker-compose 1.6.2, build 4d72027`.</span></span>

> [!TIP]
> <span data-ttu-id="4838e-143">If you used another method to create a Docker host and need to install Compose yourself, see the [Compose documentation](https://github.com/docker/compose/blob/882dc673ce84b0b29cd59b6815cb93f74a6c4134/docs/install.md).</span><span class="sxs-lookup"><span data-stu-id="4838e-143">If you used another method to create a Docker host and need to install Compose yourself, see the [Compose documentation](https://github.com/docker/compose/blob/882dc673ce84b0b29cd59b6815cb93f74a6c4134/docs/install.md).</span></span>


## <a name="step-3-create-a-docker-composeyml-configuration-file"></a><span data-ttu-id="4838e-144">Step 3: Create a docker-compose.yml configuration file</span><span class="sxs-lookup"><span data-stu-id="4838e-144">Step 3: Create a docker-compose.yml configuration file</span></span>
<span data-ttu-id="4838e-145">Next you create a `docker-compose.yml` file, which is just a text configuration file, to define the Docker containers to run on the VM.</span><span class="sxs-lookup"><span data-stu-id="4838e-145">Next you create a `docker-compose.yml` file, which is just a text configuration file, to define the Docker containers to run on the VM.</span></span> <span data-ttu-id="4838e-146">The file specifies the image to run on each container (or it could be a build from a Dockerfile), necessary environment variables and dependencies, ports, and the links between containers.</span><span class="sxs-lookup"><span data-stu-id="4838e-146">The file specifies the image to run on each container (or it could be a build from a Dockerfile), necessary environment variables and dependencies, ports, and the links between containers.</span></span> <span data-ttu-id="4838e-147">For details on yml file syntax, see [Compose file reference](http://docs.docker.com/compose/yml/).</span><span class="sxs-lookup"><span data-stu-id="4838e-147">For details on yml file syntax, see [Compose file reference](http://docs.docker.com/compose/yml/).</span></span>

<span data-ttu-id="4838e-148">Create the `docker-compose.yml` file as follows:</span><span class="sxs-lookup"><span data-stu-id="4838e-148">Create the `docker-compose.yml` file as follows:</span></span>

```bash
touch docker-compose.yml
```

<span data-ttu-id="4838e-149">Use your favorite text editor to add some data to the file.</span><span class="sxs-lookup"><span data-stu-id="4838e-149">Use your favorite text editor to add some data to the file.</span></span> <span data-ttu-id="4838e-150">The following example uses the `vi` editor:</span><span class="sxs-lookup"><span data-stu-id="4838e-150">The following example uses the `vi` editor:</span></span>

```bash
vi docker-compose.yml
```

<span data-ttu-id="4838e-151">Paste the following example into your text file.</span><span class="sxs-lookup"><span data-stu-id="4838e-151">Paste the following example into your text file.</span></span> <span data-ttu-id="4838e-152">This configuration uses images from the [DockerHub Registry](https://registry.hub.docker.com/_/wordpress/) to install WordPress (the open source blogging and content management system) and a linked backend MariaDB SQL database.</span><span class="sxs-lookup"><span data-stu-id="4838e-152">This configuration uses images from the [DockerHub Registry](https://registry.hub.docker.com/_/wordpress/) to install WordPress (the open source blogging and content management system) and a linked backend MariaDB SQL database.</span></span> <span data-ttu-id="4838e-153">Enter your own `MYSQL_ROOT_PASSWORD` as follows:</span><span class="sxs-lookup"><span data-stu-id="4838e-153">Enter your own `MYSQL_ROOT_PASSWORD` as follows:</span></span>

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

## <a name="step-4-start-the-containers-with-compose"></a><span data-ttu-id="4838e-154">Step 4: Start the containers with Compose</span><span class="sxs-lookup"><span data-stu-id="4838e-154">Step 4: Start the containers with Compose</span></span>
<span data-ttu-id="4838e-155">In the same directory as your `docker-compose.yml` file, run the following command (depending on your environment, you might need to run `docker-compose` using `sudo`.):</span><span class="sxs-lookup"><span data-stu-id="4838e-155">In the same directory as your `docker-compose.yml` file, run the following command (depending on your environment, you might need to run `docker-compose` using `sudo`.):</span></span>

```bash
docker-compose up -d
```

<span data-ttu-id="4838e-156">This command starts the Docker containers specified in `docker-compose.yml`.</span><span class="sxs-lookup"><span data-stu-id="4838e-156">This command starts the Docker containers specified in `docker-compose.yml`.</span></span> <span data-ttu-id="4838e-157">It takes a minute or two for this step to complete.</span><span class="sxs-lookup"><span data-stu-id="4838e-157">It takes a minute or two for this step to complete.</span></span> <span data-ttu-id="4838e-158">You see output similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="4838e-158">You see output similar to the following example:</span></span>

```bash
Creating wordpress_db_1...
Creating wordpress_wordpress_1...
...
```

> [!NOTE]
> <span data-ttu-id="4838e-159">Be sure to use the **-d** option on start-up so that the containers run in the background continuously.</span><span class="sxs-lookup"><span data-stu-id="4838e-159">Be sure to use the **-d** option on start-up so that the containers run in the background continuously.</span></span>


<span data-ttu-id="4838e-160">To verify that the containers are up, type `docker-compose ps`.</span><span class="sxs-lookup"><span data-stu-id="4838e-160">To verify that the containers are up, type `docker-compose ps`.</span></span> <span data-ttu-id="4838e-161">You should see something like:</span><span class="sxs-lookup"><span data-stu-id="4838e-161">You should see something like:</span></span>

```bash
Name             Command             State              Ports
-------------------------------------------------------------------------
wordpress_db_1     /docker-           Up                 3306/tcp
             entrypoint.sh
             mysqld
wordpress_wordpr   /entrypoint.sh     Up                 0.0.0.0:80->80
ess_1              apache2-for ...                       /tcp
```

<span data-ttu-id="4838e-162">You can now connect to WordPress directly on the VM on port 80.</span><span class="sxs-lookup"><span data-stu-id="4838e-162">You can now connect to WordPress directly on the VM on port 80.</span></span> <span data-ttu-id="4838e-163">Open a web browser and enter the DNS name of your VM (such as `http://myresourcegroup.westus.cloudapp.azure.com`).</span><span class="sxs-lookup"><span data-stu-id="4838e-163">Open a web browser and enter the DNS name of your VM (such as `http://myresourcegroup.westus.cloudapp.azure.com`).</span></span> <span data-ttu-id="4838e-164">You should now see the WordPress start screen, where you can complete the installation and get started with the application.</span><span class="sxs-lookup"><span data-stu-id="4838e-164">You should now see the WordPress start screen, where you can complete the installation and get started with the application.</span></span>

![WordPress start screen][wordpress_start]

## <a name="next-steps"></a><span data-ttu-id="4838e-166">Next steps</span><span class="sxs-lookup"><span data-stu-id="4838e-166">Next steps</span></span>
* <span data-ttu-id="4838e-167">Go to the [Docker VM extension user guide](https://github.com/Azure/azure-docker-extension/blob/master/README.md) for more options to configure Docker and Compose in your Docker VM.</span><span class="sxs-lookup"><span data-stu-id="4838e-167">Go to the [Docker VM extension user guide](https://github.com/Azure/azure-docker-extension/blob/master/README.md) for more options to configure Docker and Compose in your Docker VM.</span></span> <span data-ttu-id="4838e-168">For example, one option is to put the Compose yml file (converted to JSON) directly in the configuration of the Docker VM extension.</span><span class="sxs-lookup"><span data-stu-id="4838e-168">For example, one option is to put the Compose yml file (converted to JSON) directly in the configuration of the Docker VM extension.</span></span>
* <span data-ttu-id="4838e-169">Check out the [Compose command-line reference](http://docs.docker.com/compose/reference/) and [user guide](http://docs.docker.com/compose/) for more examples of building and deploying multi-container apps.</span><span class="sxs-lookup"><span data-stu-id="4838e-169">Check out the [Compose command-line reference](http://docs.docker.com/compose/reference/) and [user guide](http://docs.docker.com/compose/) for more examples of building and deploying multi-container apps.</span></span>
* <span data-ttu-id="4838e-170">Use an Azure Resource Manager template, either your own or one contributed from the [community](https://azure.microsoft.com/documentation/templates/), to deploy an Azure VM with Docker and an application set up with Compose.</span><span class="sxs-lookup"><span data-stu-id="4838e-170">Use an Azure Resource Manager template, either your own or one contributed from the [community](https://azure.microsoft.com/documentation/templates/), to deploy an Azure VM with Docker and an application set up with Compose.</span></span> <span data-ttu-id="4838e-171">For example, the [Deploy a WordPress blog with Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-wordpress-mysql) template uses Docker and Compose to quickly deploy WordPress with a MySQL backend on an Ubuntu VM.</span><span class="sxs-lookup"><span data-stu-id="4838e-171">For example, the [Deploy a WordPress blog with Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-wordpress-mysql) template uses Docker and Compose to quickly deploy WordPress with a MySQL backend on an Ubuntu VM.</span></span>
* <span data-ttu-id="4838e-172">Try integrating Docker Compose with a Docker Swarm cluster.</span><span class="sxs-lookup"><span data-stu-id="4838e-172">Try integrating Docker Compose with a Docker Swarm cluster.</span></span> <span data-ttu-id="4838e-173">See [Using Compose with Swarm](https://docs.docker.com/compose/swarm/) for scenarios.</span><span class="sxs-lookup"><span data-stu-id="4838e-173">See [Using Compose with Swarm](https://docs.docker.com/compose/swarm/) for scenarios.</span></span>

<!--Image references-->

[wordpress_start]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/docker-compose-quickstart/WordPress.png

