---
title: Create a multi-container (preview) app in Web App for Containers
description: Learn how to use multiple containers on Azure with Docker Compose and Kubernetes configuration files, with a WordPress and MySQL app.
keywords: azure app service, web app, linux, docker, compose, multicontainer, multi-container, web app for containers, multiple containers, container, kubernetes, wordpress, azure db for mysql, production database with containers
services: app-service
documentationcenter: ''
author: msangapu
manager: jeconnoc
editor: ''
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 06/25/2018
ms.author: msangapu
ms.custom: mvc
ms.openlocfilehash: ff3659bd0f4001424ce27484f08a645f364c2ef6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864645"
---
# <a name="tutorial-create-a-multi-container-preview-app-in-web-app-for-containers"></a><span data-ttu-id="04c3c-104">Tutorial: Create a multi-container (preview) app in Web App for Containers</span><span class="sxs-lookup"><span data-stu-id="04c3c-104">Tutorial: Create a multi-container (preview) app in Web App for Containers</span></span>

<span data-ttu-id="04c3c-105">[Web App for Containers](app-service-linux-intro.md) provides a flexible way to use Docker images.</span><span class="sxs-lookup"><span data-stu-id="04c3c-105">[Web App for Containers](app-service-linux-intro.md) provides a flexible way to use Docker images.</span></span> <span data-ttu-id="04c3c-106">In this tutorial, you'll learn how to create a multi-container app using WordPress and MySQL.</span><span class="sxs-lookup"><span data-stu-id="04c3c-106">In this tutorial, you'll learn how to create a multi-container app using WordPress and MySQL.</span></span> <span data-ttu-id="04c3c-107">You'll complete this tutorial in Cloud Shell, but you can also run these commands locally with the [Azure CLI](/cli/azure/install-azure-cli) command-line tool (2.0.32 or later).</span><span class="sxs-lookup"><span data-stu-id="04c3c-107">You'll complete this tutorial in Cloud Shell, but you can also run these commands locally with the [Azure CLI](/cli/azure/install-azure-cli) command-line tool (2.0.32 or later).</span></span>

<span data-ttu-id="04c3c-108">In this tutorial, you'll learn how to:</span><span class="sxs-lookup"><span data-stu-id="04c3c-108">In this tutorial, you'll learn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="04c3c-109">Convert a Docker Compose configuration to work with Web App for Containers</span><span class="sxs-lookup"><span data-stu-id="04c3c-109">Convert a Docker Compose configuration to work with Web App for Containers</span></span>
> * <span data-ttu-id="04c3c-110">Convert a Kubernetes configuration to work with Web App for Containers</span><span class="sxs-lookup"><span data-stu-id="04c3c-110">Convert a Kubernetes configuration to work with Web App for Containers</span></span>
> * <span data-ttu-id="04c3c-111">Deploy a multi-container app to Azure</span><span class="sxs-lookup"><span data-stu-id="04c3c-111">Deploy a multi-container app to Azure</span></span>
> * <span data-ttu-id="04c3c-112">Add application settings</span><span class="sxs-lookup"><span data-stu-id="04c3c-112">Add application settings</span></span>
> * <span data-ttu-id="04c3c-113">Use persistent storage for your containers</span><span class="sxs-lookup"><span data-stu-id="04c3c-113">Use persistent storage for your containers</span></span>
> * <span data-ttu-id="04c3c-114">Connect to Azure Database for MySQL</span><span class="sxs-lookup"><span data-stu-id="04c3c-114">Connect to Azure Database for MySQL</span></span>
> * <span data-ttu-id="04c3c-115">Troubleshoot errors</span><span class="sxs-lookup"><span data-stu-id="04c3c-115">Troubleshoot errors</span></span>

[!INCLUDE [Free trial note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="prerequisites"></a><span data-ttu-id="04c3c-116">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="04c3c-116">Prerequisites</span></span>

<span data-ttu-id="04c3c-117">To complete this tutorial, you need experience with [Docker Compose](https://docs.docker.com/compose/) or [Kubernetes](https://kubernetes.io/).</span><span class="sxs-lookup"><span data-stu-id="04c3c-117">To complete this tutorial, you need experience with [Docker Compose](https://docs.docker.com/compose/) or [Kubernetes](https://kubernetes.io/).</span></span>

## <a name="download-the-sample"></a><span data-ttu-id="04c3c-118">Download the sample</span><span class="sxs-lookup"><span data-stu-id="04c3c-118">Download the sample</span></span>

<span data-ttu-id="04c3c-119">For this tutorial, you use the compose file from [Docker](https://docs.docker.com/compose/wordpress/#define-the-project), but you'll modify it include Azure Database for MySQL, persistent storage, and Redis.</span><span class="sxs-lookup"><span data-stu-id="04c3c-119">For this tutorial, you use the compose file from [Docker](https://docs.docker.com/compose/wordpress/#define-the-project), but you'll modify it include Azure Database for MySQL, persistent storage, and Redis.</span></span> <span data-ttu-id="04c3c-120">The configuration file can be found at [Azure Samples](https://github.com/Azure-Samples/multicontainerwordpress).</span><span class="sxs-lookup"><span data-stu-id="04c3c-120">The configuration file can be found at [Azure Samples](https://github.com/Azure-Samples/multicontainerwordpress).</span></span>

[!code-yml[Main](../../../azure-app-service-multi-container/docker-compose-wordpress.yml)]

<span data-ttu-id="04c3c-121">In Cloud Shell, create a tutorial directory and then change to it.</span><span class="sxs-lookup"><span data-stu-id="04c3c-121">In Cloud Shell, create a tutorial directory and then change to it.</span></span>

```bash
mkdir tutorial

cd tutorial
```

<span data-ttu-id="04c3c-122">Next, run the following command to clone the sample app repository to your tutorial directory.</span><span class="sxs-lookup"><span data-stu-id="04c3c-122">Next, run the following command to clone the sample app repository to your tutorial directory.</span></span> <span data-ttu-id="04c3c-123">Then change to the `multicontainerwordpress` directory.</span><span class="sxs-lookup"><span data-stu-id="04c3c-123">Then change to the `multicontainerwordpress` directory.</span></span>

```bash
git clone https://github.com/Azure-Samples/multicontainerwordpress

cd multicontainerwordpress
```

## <a name="create-a-resource-group"></a><span data-ttu-id="04c3c-124">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="04c3c-124">Create a resource group</span></span>

[!INCLUDE [resource group intro text](../../../includes/resource-group.md)]

<span data-ttu-id="04c3c-125">In Cloud Shell, create a resource group with the [`az group create`](/cli/azure/group?view=azure-cli-latest#az-group-create) command.</span><span class="sxs-lookup"><span data-stu-id="04c3c-125">In Cloud Shell, create a resource group with the [`az group create`](/cli/azure/group?view=azure-cli-latest#az-group-create) command.</span></span> <span data-ttu-id="04c3c-126">The following example creates a resource group named *myResourceGroup* in the *South Central US* location.</span><span class="sxs-lookup"><span data-stu-id="04c3c-126">The following example creates a resource group named *myResourceGroup* in the *South Central US* location.</span></span> <span data-ttu-id="04c3c-127">To see all supported locations for App Service on Linux in **Standard** tier, run the [`az appservice list-locations --sku S1 --linux-workers-enabled`](/cli/azure/appservice?view=azure-cli-latest#az-appservice-list-locations) command.</span><span class="sxs-lookup"><span data-stu-id="04c3c-127">To see all supported locations for App Service on Linux in **Standard** tier, run the [`az appservice list-locations --sku S1 --linux-workers-enabled`](/cli/azure/appservice?view=azure-cli-latest#az-appservice-list-locations) command.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location "South Central US"
```

<span data-ttu-id="04c3c-128">You generally create your resource group and the resources in a region near you.</span><span class="sxs-lookup"><span data-stu-id="04c3c-128">You generally create your resource group and the resources in a region near you.</span></span>

<span data-ttu-id="04c3c-129">When the command finishes, a JSON output shows you the resource group properties.</span><span class="sxs-lookup"><span data-stu-id="04c3c-129">When the command finishes, a JSON output shows you the resource group properties.</span></span>

## <a name="create-an-azure-app-service-plan"></a><span data-ttu-id="04c3c-130">Create an Azure App Service plan</span><span class="sxs-lookup"><span data-stu-id="04c3c-130">Create an Azure App Service plan</span></span>

<span data-ttu-id="04c3c-131">In Cloud Shell, create an App Service plan in the resource group with the [`az appservice plan create`](/cli/azure/appservice/plan?view=azure-cli-latest#az-appservice-plan-create) command.</span><span class="sxs-lookup"><span data-stu-id="04c3c-131">In Cloud Shell, create an App Service plan in the resource group with the [`az appservice plan create`](/cli/azure/appservice/plan?view=azure-cli-latest#az-appservice-plan-create) command.</span></span>

<!-- [!INCLUDE [app-service-plan](app-service-plan-linux.md)] -->

<span data-ttu-id="04c3c-132">The following example creates an App Service plan named `myAppServicePlan` in the **Standard** pricing tier (`--sku S1`) and in a Linux container (`--is-linux`).</span><span class="sxs-lookup"><span data-stu-id="04c3c-132">The following example creates an App Service plan named `myAppServicePlan` in the **Standard** pricing tier (`--sku S1`) and in a Linux container (`--is-linux`).</span></span>

```azurecli-interactive
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku S1 --is-linux
```

<span data-ttu-id="04c3c-133">When the App Service plan has been created, Cloud Shell shows information similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="04c3c-133">When the App Service plan has been created, Cloud Shell shows information similar to the following example:</span></span>

```json
{
  "adminSiteName": null,
  "appServicePlanName": "myAppServicePlan",
  "geoRegion": "South Central US",
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/0000-0000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan",
  "kind": "linux",
  "location": "South Central US",
  "maximumNumberOfWorkers": 1,
  "name": "myAppServicePlan",
  < JSON data removed for brevity. >
  "targetWorkerSizeId": 0,
  "type": "Microsoft.Web/serverfarms",
  "workerTierName": null
}
```

## <a name="docker-compose-configuration-options"></a><span data-ttu-id="04c3c-134">Docker Compose configuration options</span><span class="sxs-lookup"><span data-stu-id="04c3c-134">Docker Compose configuration options</span></span>

<span data-ttu-id="04c3c-135">For this tutorial, you use the compose file from [Docker](https://docs.docker.com/compose/wordpress/#define-the-project), but you'll modify it include Azure Database for MySQL, persistent storage, and Redis.</span><span class="sxs-lookup"><span data-stu-id="04c3c-135">For this tutorial, you use the compose file from [Docker](https://docs.docker.com/compose/wordpress/#define-the-project), but you'll modify it include Azure Database for MySQL, persistent storage, and Redis.</span></span> <span data-ttu-id="04c3c-136">Alternatively, you can use a [Kubernetes configuration](#use-a-kubernetes-configuration-optional).</span><span class="sxs-lookup"><span data-stu-id="04c3c-136">Alternatively, you can use a [Kubernetes configuration](#use-a-kubernetes-configuration-optional).</span></span> <span data-ttu-id="04c3c-137">The configuration files can be found at [Azure Samples](https://github.com/Azure-Samples/multicontainerwordpress).</span><span class="sxs-lookup"><span data-stu-id="04c3c-137">The configuration files can be found at [Azure Samples](https://github.com/Azure-Samples/multicontainerwordpress).</span></span>

<span data-ttu-id="04c3c-138">The following lists show supported and unsupported Docker Compose configuration options in Web App for Containers:</span><span class="sxs-lookup"><span data-stu-id="04c3c-138">The following lists show supported and unsupported Docker Compose configuration options in Web App for Containers:</span></span>

### <a name="supported-options"></a><span data-ttu-id="04c3c-139">Supported options</span><span class="sxs-lookup"><span data-stu-id="04c3c-139">Supported options</span></span>

* <span data-ttu-id="04c3c-140">command</span><span class="sxs-lookup"><span data-stu-id="04c3c-140">command</span></span>
* <span data-ttu-id="04c3c-141">entrypoint</span><span class="sxs-lookup"><span data-stu-id="04c3c-141">entrypoint</span></span>
* <span data-ttu-id="04c3c-142">environment</span><span class="sxs-lookup"><span data-stu-id="04c3c-142">environment</span></span>
* <span data-ttu-id="04c3c-143">image</span><span class="sxs-lookup"><span data-stu-id="04c3c-143">image</span></span>
* <span data-ttu-id="04c3c-144">ports</span><span class="sxs-lookup"><span data-stu-id="04c3c-144">ports</span></span>
* <span data-ttu-id="04c3c-145">restart</span><span class="sxs-lookup"><span data-stu-id="04c3c-145">restart</span></span>
* <span data-ttu-id="04c3c-146">services</span><span class="sxs-lookup"><span data-stu-id="04c3c-146">services</span></span>
* <span data-ttu-id="04c3c-147">volumes</span><span class="sxs-lookup"><span data-stu-id="04c3c-147">volumes</span></span>

### <a name="unsupported-options"></a><span data-ttu-id="04c3c-148">Unsupported options</span><span class="sxs-lookup"><span data-stu-id="04c3c-148">Unsupported options</span></span>

* <span data-ttu-id="04c3c-149">build (not allowed)</span><span class="sxs-lookup"><span data-stu-id="04c3c-149">build (not allowed)</span></span>
* <span data-ttu-id="04c3c-150">depends_on (ignored)</span><span class="sxs-lookup"><span data-stu-id="04c3c-150">depends_on (ignored)</span></span>
* <span data-ttu-id="04c3c-151">networks (ignored)</span><span class="sxs-lookup"><span data-stu-id="04c3c-151">networks (ignored)</span></span>
* <span data-ttu-id="04c3c-152">secrets (ignored)</span><span class="sxs-lookup"><span data-stu-id="04c3c-152">secrets (ignored)</span></span>

> [!NOTE]
> <span data-ttu-id="04c3c-153">Any other options not explicitly called out are also ignored in Public Preview.</span><span class="sxs-lookup"><span data-stu-id="04c3c-153">Any other options not explicitly called out are also ignored in Public Preview.</span></span>

### <a name="docker-compose-with-wordpress-and-mysql-containers"></a><span data-ttu-id="04c3c-154">Docker Compose with WordPress and MySQL containers</span><span class="sxs-lookup"><span data-stu-id="04c3c-154">Docker Compose with WordPress and MySQL containers</span></span>

## <a name="create-a-docker-compose-app"></a><span data-ttu-id="04c3c-155">Create a Docker Compose app</span><span class="sxs-lookup"><span data-stu-id="04c3c-155">Create a Docker Compose app</span></span>

<span data-ttu-id="04c3c-156">In your Cloud Shell, create a multi-container [web app](app-service-linux-intro.md) in the `myAppServicePlan` App Service plan with the [az webapp create](/cli/azure/webapp?view=azure-cli-latest#az-webapp-create) command.</span><span class="sxs-lookup"><span data-stu-id="04c3c-156">In your Cloud Shell, create a multi-container [web app](app-service-linux-intro.md) in the `myAppServicePlan` App Service plan with the [az webapp create](/cli/azure/webapp?view=azure-cli-latest#az-webapp-create) command.</span></span> <span data-ttu-id="04c3c-157">Don't forget to replace _\<app_name>_ with a unique app name.</span><span class="sxs-lookup"><span data-stu-id="04c3c-157">Don't forget to replace _\<app_name>_ with a unique app name.</span></span>

```bash
az webapp create --resource-group myResourceGroup --plan myAppServicePlan --name <app_name> --multicontainer-config-type compose --multicontainer-config-file docker-compose-wordpress.yml
```

<span data-ttu-id="04c3c-158">When the web app has been created, Cloud Shell shows output similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="04c3c-158">When the web app has been created, Cloud Shell shows output similar to the following example:</span></span>

```json
{
  "additionalProperties": {},
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
  "cloningInfo": null,
  "containerSize": 0,
  "dailyMemoryTimeQuota": 0,
  "defaultHostName": "<app_name>.azurewebsites.net",
  "enabled": true,
  < JSON data removed for brevity. >
}
```

### <a name="browse-to-the-app"></a><span data-ttu-id="04c3c-159">Browse to the app</span><span class="sxs-lookup"><span data-stu-id="04c3c-159">Browse to the app</span></span>

<span data-ttu-id="04c3c-160">Browse to the deployed app at (`http://<app_name>.azurewebsites.net`).</span><span class="sxs-lookup"><span data-stu-id="04c3c-160">Browse to the deployed app at (`http://<app_name>.azurewebsites.net`).</span></span> <span data-ttu-id="04c3c-161">The app may take a few minutes to load.</span><span class="sxs-lookup"><span data-stu-id="04c3c-161">The app may take a few minutes to load.</span></span> <span data-ttu-id="04c3c-162">If you receive an error, allow a few more minutes then refresh the browser.</span><span class="sxs-lookup"><span data-stu-id="04c3c-162">If you receive an error, allow a few more minutes then refresh the browser.</span></span> <span data-ttu-id="04c3c-163">If you're having trouble and would like to troubleshoot, review [container logs](#find-docker-container-logs).</span><span class="sxs-lookup"><span data-stu-id="04c3c-163">If you're having trouble and would like to troubleshoot, review [container logs](#find-docker-container-logs).</span></span>

![Sample multi-container app on Web App for Containers][1]

<span data-ttu-id="04c3c-165">**Congratulations**, you've created a multi-container app in Web App for Containers.</span><span class="sxs-lookup"><span data-stu-id="04c3c-165">**Congratulations**, you've created a multi-container app in Web App for Containers.</span></span> <span data-ttu-id="04c3c-166">Next you'll configure your app to use Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="04c3c-166">Next you'll configure your app to use Azure Database for MySQL.</span></span> <span data-ttu-id="04c3c-167">Don't install WordPress at this time.</span><span class="sxs-lookup"><span data-stu-id="04c3c-167">Don't install WordPress at this time.</span></span>

## <a name="connect-to-production-database"></a><span data-ttu-id="04c3c-168">Connect to production database</span><span class="sxs-lookup"><span data-stu-id="04c3c-168">Connect to production database</span></span>

<span data-ttu-id="04c3c-169">It's not recommended to use database containers in a production environment.</span><span class="sxs-lookup"><span data-stu-id="04c3c-169">It's not recommended to use database containers in a production environment.</span></span> <span data-ttu-id="04c3c-170">The local containers aren't scalable.</span><span class="sxs-lookup"><span data-stu-id="04c3c-170">The local containers aren't scalable.</span></span> <span data-ttu-id="04c3c-171">Instead, you'll use Azure Database for MySQL which can be scaled.</span><span class="sxs-lookup"><span data-stu-id="04c3c-171">Instead, you'll use Azure Database for MySQL which can be scaled.</span></span>

### <a name="create-an-azure-database-for-mysql-server"></a><span data-ttu-id="04c3c-172">Create an Azure Database for MySQL server</span><span class="sxs-lookup"><span data-stu-id="04c3c-172">Create an Azure Database for MySQL server</span></span>

<span data-ttu-id="04c3c-173">Create an Azure Database for MySQL server with the [`az mysql server create`](/cli/azure/mysql/server?view=azure-cli-latest#az-mysql-server-create) command.</span><span class="sxs-lookup"><span data-stu-id="04c3c-173">Create an Azure Database for MySQL server with the [`az mysql server create`](/cli/azure/mysql/server?view=azure-cli-latest#az-mysql-server-create) command.</span></span>

<span data-ttu-id="04c3c-174">In the following command, substitute your MySQL server name where you see the _&lt;mysql_server_name>_ placeholder (valid characters are `a-z`, `0-9`, and `-`).</span><span class="sxs-lookup"><span data-stu-id="04c3c-174">In the following command, substitute your MySQL server name where you see the _&lt;mysql_server_name>_ placeholder (valid characters are `a-z`, `0-9`, and `-`).</span></span> <span data-ttu-id="04c3c-175">This name is part of the MySQL server's hostname  (`<mysql_server_name>.database.windows.net`), it needs to be globally unique.</span><span class="sxs-lookup"><span data-stu-id="04c3c-175">This name is part of the MySQL server's hostname  (`<mysql_server_name>.database.windows.net`), it needs to be globally unique.</span></span>

```azurecli-interactive
az mysql server create --resource-group myResourceGroup --name <mysql_server_name>  --location "South Central US" --admin-user adminuser --admin-password My5up3rStr0ngPaSw0rd! --sku-name B_Gen4_1 --version 5.7
```

<span data-ttu-id="04c3c-176">Creating the server may take a few minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="04c3c-176">Creating the server may take a few minutes to complete.</span></span> <span data-ttu-id="04c3c-177">When the MySQL server is created, Cloud Shell shows information similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="04c3c-177">When the MySQL server is created, Cloud Shell shows information similar to the following example:</span></span>

```json
{
  "administratorLogin": "adminuser",
  "administratorLoginPassword": null,
  "fullyQualifiedDomainName": "<mysql_server_name>.database.windows.net",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.DBforMySQL/servers/<mysql_server_name>",
  "location": "southcentralus",
  "name": "<mysql_server_name>",
  "resourceGroup": "myResourceGroup",
  ...
}
```

### <a name="configure-server-firewall"></a><span data-ttu-id="04c3c-178">Configure server firewall</span><span class="sxs-lookup"><span data-stu-id="04c3c-178">Configure server firewall</span></span>

<span data-ttu-id="04c3c-179">Create a firewall rule for your MySQL server to allow client connections by using the [`az mysql server firewall-rule create`](/cli/azure/mysql/server/firewall-rule?view=azure-cli-latest#az-mysql-server-firewall-rule-create) command.</span><span class="sxs-lookup"><span data-stu-id="04c3c-179">Create a firewall rule for your MySQL server to allow client connections by using the [`az mysql server firewall-rule create`](/cli/azure/mysql/server/firewall-rule?view=azure-cli-latest#az-mysql-server-firewall-rule-create) command.</span></span> <span data-ttu-id="04c3c-180">When both starting IP and end IP are set to 0.0.0.0, the firewall is only opened for other Azure resources.</span><span class="sxs-lookup"><span data-stu-id="04c3c-180">When both starting IP and end IP are set to 0.0.0.0, the firewall is only opened for other Azure resources.</span></span>

```azurecli-interactive
az mysql server firewall-rule create --name allAzureIPs --server <mysql_server_name> --resource-group myResourceGroup --start-ip-address 0.0.0.0 --end-ip-address 0.0.0.0
```

> [!TIP]
> <span data-ttu-id="04c3c-181">You can be even more restrictive in your firewall rule by [using only the outbound IP addresses your app uses](../app-service-ip-addresses.md?toc=%2fazure%2fapp-service%2fcontainers%2ftoc.json#find-outbound-ips).</span><span class="sxs-lookup"><span data-stu-id="04c3c-181">You can be even more restrictive in your firewall rule by [using only the outbound IP addresses your app uses](../app-service-ip-addresses.md?toc=%2fazure%2fapp-service%2fcontainers%2ftoc.json#find-outbound-ips).</span></span>
>

### <a name="create-the-wordpress-database"></a><span data-ttu-id="04c3c-182">Create the WordPress database</span><span class="sxs-lookup"><span data-stu-id="04c3c-182">Create the WordPress database</span></span>

```bash
az mysql db create --resource-group myResourceGroup --server-name <mysql_server_name> --name wordpress
```

<span data-ttu-id="04c3c-183">When the database has been created, Cloud Shell shows information similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="04c3c-183">When the database has been created, Cloud Shell shows information similar to the following example:</span></span>

```json
{
  "additionalProperties": {},
  "charset": "latin1",
  "collation": "latin1_swedish_ci",
  "id": "/subscriptions/12db1644-4b12-4cab-ba54-8ba2f2822c1f/resourceGroups/myResourceGroup/providers/Microsoft.DBforMySQL/servers/<mysql_server_name>/databases/wordpress",
  "name": "wordpress",
  "resourceGroup": "myResourceGroup",
  "type": "Microsoft.DBforMySQL/servers/databases"
}
```

### <a name="configure-database-variables-in-wordpress"></a><span data-ttu-id="04c3c-184">Configure database variables in WordPress</span><span class="sxs-lookup"><span data-stu-id="04c3c-184">Configure database variables in WordPress</span></span>

<span data-ttu-id="04c3c-185">To connect the WordPress app to this new MySQL server, you'll configure a few WordPress-specific environment variables, including the SSL CA path defined by `MYSQL_SSL_CA`.</span><span class="sxs-lookup"><span data-stu-id="04c3c-185">To connect the WordPress app to this new MySQL server, you'll configure a few WordPress-specific environment variables, including the SSL CA path defined by `MYSQL_SSL_CA`.</span></span> <span data-ttu-id="04c3c-186">The [Baltimore CyberTrust Root](https://www.digicert.com/digicert-root-certificates.htm) from [DigiCert](http://www.digicert.com/) is provided in the [custom image](https://docs.microsoft.com/en-us/azure/app-service/containers/tutorial-multi-container-app#use-a-custom-image-for-mysql-ssl-and-other-configurations) below.</span><span class="sxs-lookup"><span data-stu-id="04c3c-186">The [Baltimore CyberTrust Root](https://www.digicert.com/digicert-root-certificates.htm) from [DigiCert](http://www.digicert.com/) is provided in the [custom image](https://docs.microsoft.com/en-us/azure/app-service/containers/tutorial-multi-container-app#use-a-custom-image-for-mysql-ssl-and-other-configurations) below.</span></span>

<span data-ttu-id="04c3c-187">To make these changes, use the [az webapp config appsettings set](/cli/azure/webapp/config/appsettings?view=azure-cli-latest#az-webapp-config-appsettings-set) command in Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="04c3c-187">To make these changes, use the [az webapp config appsettings set](/cli/azure/webapp/config/appsettings?view=azure-cli-latest#az-webapp-config-appsettings-set) command in Cloud Shell.</span></span> <span data-ttu-id="04c3c-188">App settings are case-sensitive and space-separated.</span><span class="sxs-lookup"><span data-stu-id="04c3c-188">App settings are case-sensitive and space-separated.</span></span>

```bash
az webapp config appsettings set --resource-group myResourceGroup --name <app_name> --settings WORDPRESS_DB_HOST="<mysql_server_name>.mysql.database.azure.com" WORDPRESS_DB_USER="adminuser@<mysql_server_name>" WORDPRESS_DB_PASSWORD="My5up3rStr0ngPaSw0rd!" WORDPRESS_DB_NAME="wordpress" MYSQL_SSL_CA="BaltimoreCyberTrustroot.crt.pem"
```

<span data-ttu-id="04c3c-189">When the app setting has been created, Cloud Shell shows information similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="04c3c-189">When the app setting has been created, Cloud Shell shows information similar to the following example:</span></span>

```json
[
  {
    "name": "WORDPRESS_DB_HOST",
    "slotSetting": false,
    "value": "<mysql_server_name>.mysql.database.azure.com"
  },
  {
    "name": "WORDPRESS_DB_USER",
    "slotSetting": false,
    "value": "adminuser@<mysql_server_name>"
  },
  {
    "name": "WORDPRESS_DB_NAME",
    "slotSetting": false,
    "value": "wordpress"
  },
  {
    "name": "WORDPRESS_DB_PASSWORD",
    "slotSetting": false,
    "value": "My5up3rStr0ngPaSw0rd!"
  },
  {
    "name": "MYSQL_SSL_CA",
    "slotSetting": false,
    "value": "BaltimoreCyberTrustroot.crt.pem"
  }
]
```

### <a name="use-a-custom-image-for-mysql-ssl-and-other-configurations"></a><span data-ttu-id="04c3c-190">Use a custom image for MySQL SSL and other configurations</span><span class="sxs-lookup"><span data-stu-id="04c3c-190">Use a custom image for MySQL SSL and other configurations</span></span>

<span data-ttu-id="04c3c-191">By default, SSL is used by Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="04c3c-191">By default, SSL is used by Azure Database for MySQL.</span></span> <span data-ttu-id="04c3c-192">WordPress requires additional configuration to use SSL with MySQL.</span><span class="sxs-lookup"><span data-stu-id="04c3c-192">WordPress requires additional configuration to use SSL with MySQL.</span></span> <span data-ttu-id="04c3c-193">The WordPress 'official image' doesn't provide the additional configuration, but a [custom image](https://hub.docker.com/r/microsoft/multicontainerwordpress/builds/) has been prepared fo your convenience.</span><span class="sxs-lookup"><span data-stu-id="04c3c-193">The WordPress 'official image' doesn't provide the additional configuration, but a [custom image](https://hub.docker.com/r/microsoft/multicontainerwordpress/builds/) has been prepared fo your convenience.</span></span> <span data-ttu-id="04c3c-194">In practice, you would add desired changes to your own image.</span><span class="sxs-lookup"><span data-stu-id="04c3c-194">In practice, you would add desired changes to your own image.</span></span>

<span data-ttu-id="04c3c-195">The custom image is based on the 'official image' of [WordPress from Docker Hub](https://hub.docker.com/_/wordpress/).</span><span class="sxs-lookup"><span data-stu-id="04c3c-195">The custom image is based on the 'official image' of [WordPress from Docker Hub](https://hub.docker.com/_/wordpress/).</span></span> <span data-ttu-id="04c3c-196">The following changes have been made in this custom image for Azure Database for MySQL:</span><span class="sxs-lookup"><span data-stu-id="04c3c-196">The following changes have been made in this custom image for Azure Database for MySQL:</span></span>

* [<span data-ttu-id="04c3c-197">Adds Baltimore Cyber Trust Root Certificate file for SSL to MySQL.</span><span class="sxs-lookup"><span data-stu-id="04c3c-197">Adds Baltimore Cyber Trust Root Certificate file for SSL to MySQL.</span></span>](https://github.com/Azure-Samples/multicontainerwordpress/blob/5669a89e0ee8599285f0e2e6f7e935c16e539b92/docker-entrypoint.sh#L61)
* [<span data-ttu-id="04c3c-198">Uses App Setting for MySQL SSL Certificate Authority certificate in WordPress wp-config.php.</span><span class="sxs-lookup"><span data-stu-id="04c3c-198">Uses App Setting for MySQL SSL Certificate Authority certificate in WordPress wp-config.php.</span></span>](https://github.com/Azure-Samples/multicontainerwordpress/blob/5669a89e0ee8599285f0e2e6f7e935c16e539b92/docker-entrypoint.sh#L163)
* [<span data-ttu-id="04c3c-199">Adds WordPress define for MYSQL_CLIENT_FLAGS needed for MySQL SSL.</span><span class="sxs-lookup"><span data-stu-id="04c3c-199">Adds WordPress define for MYSQL_CLIENT_FLAGS needed for MySQL SSL.</span></span>](https://github.com/Azure-Samples/multicontainerwordpress/blob/5669a89e0ee8599285f0e2e6f7e935c16e539b92/docker-entrypoint.sh#L164)

<span data-ttu-id="04c3c-200">The following changes have been made for Redis (to be used in a later section):</span><span class="sxs-lookup"><span data-stu-id="04c3c-200">The following changes have been made for Redis (to be used in a later section):</span></span>

* [<span data-ttu-id="04c3c-201">Adds PHP extension for Redis v4.0.2.</span><span class="sxs-lookup"><span data-stu-id="04c3c-201">Adds PHP extension for Redis v4.0.2.</span></span>](https://github.com/Azure-Samples/multicontainerwordpress/blob/5669a89e0ee8599285f0e2e6f7e935c16e539b92/Dockerfile#L35)
* [<span data-ttu-id="04c3c-202">Adds unzip needed for file extraction.</span><span class="sxs-lookup"><span data-stu-id="04c3c-202">Adds unzip needed for file extraction.</span></span>](https://github.com/Azure-Samples/multicontainerwordpress/blob/5669a89e0ee8599285f0e2e6f7e935c16e539b92/docker-entrypoint.sh#L71)
* [<span data-ttu-id="04c3c-203">Adds Redis Object Cache 1.3.8 WordPress plugin.</span><span class="sxs-lookup"><span data-stu-id="04c3c-203">Adds Redis Object Cache 1.3.8 WordPress plugin.</span></span>](https://github.com/Azure-Samples/multicontainerwordpress/blob/5669a89e0ee8599285f0e2e6f7e935c16e539b92/docker-entrypoint.sh#L74)
* [<span data-ttu-id="04c3c-204">Uses App Setting for Redis host name in WordPress wp-config.php.</span><span class="sxs-lookup"><span data-stu-id="04c3c-204">Uses App Setting for Redis host name in WordPress wp-config.php.</span></span>](https://github.com/Azure-Samples/multicontainerwordpress/blob/5669a89e0ee8599285f0e2e6f7e935c16e539b92/docker-entrypoint.sh#L162)

<span data-ttu-id="04c3c-205">To use the custom image, you'll update your docker-compose-wordpress.yml file.</span><span class="sxs-lookup"><span data-stu-id="04c3c-205">To use the custom image, you'll update your docker-compose-wordpress.yml file.</span></span> <span data-ttu-id="04c3c-206">In Cloud Shell, type `nano docker-compose-wordpress.yml` to open the nano text editor.</span><span class="sxs-lookup"><span data-stu-id="04c3c-206">In Cloud Shell, type `nano docker-compose-wordpress.yml` to open the nano text editor.</span></span> <span data-ttu-id="04c3c-207">Change the `image: wordpress` to use `image: microsoft/multicontainerwordpress`.</span><span class="sxs-lookup"><span data-stu-id="04c3c-207">Change the `image: wordpress` to use `image: microsoft/multicontainerwordpress`.</span></span> <span data-ttu-id="04c3c-208">You no longer need the database container.</span><span class="sxs-lookup"><span data-stu-id="04c3c-208">You no longer need the database container.</span></span> <span data-ttu-id="04c3c-209">Remove the  `db`, `environment`, `depends_on`, and `volumes` section from the configuration file.</span><span class="sxs-lookup"><span data-stu-id="04c3c-209">Remove the  `db`, `environment`, `depends_on`, and `volumes` section from the configuration file.</span></span> <span data-ttu-id="04c3c-210">Your file should look like the following code:</span><span class="sxs-lookup"><span data-stu-id="04c3c-210">Your file should look like the following code:</span></span>

```yaml
version: '3.3'

services:
   wordpress:
     image: microsoft/multicontainerwordpress
     ports:
       - "8000:80"
     restart: always
```

<span data-ttu-id="04c3c-211">Save your changes and exit nano.</span><span class="sxs-lookup"><span data-stu-id="04c3c-211">Save your changes and exit nano.</span></span> <span data-ttu-id="04c3c-212">Use the command `^O` to save and `^X` to exit.</span><span class="sxs-lookup"><span data-stu-id="04c3c-212">Use the command `^O` to save and `^X` to exit.</span></span>

### <a name="update-app-with-new-configuration"></a><span data-ttu-id="04c3c-213">Update app with new configuration</span><span class="sxs-lookup"><span data-stu-id="04c3c-213">Update app with new configuration</span></span>

<span data-ttu-id="04c3c-214">In Cloud Shell, reconfigure your multi-container [web app](app-service-linux-intro.md) with the [az webapp config container set](/cli/azure/webapp/config/container?view=azure-cli-latest#az-webapp-config-container-set) command.</span><span class="sxs-lookup"><span data-stu-id="04c3c-214">In Cloud Shell, reconfigure your multi-container [web app](app-service-linux-intro.md) with the [az webapp config container set](/cli/azure/webapp/config/container?view=azure-cli-latest#az-webapp-config-container-set) command.</span></span> <span data-ttu-id="04c3c-215">Don't forget to replace _\<app_name>_ with the name of the web app you created earlier.</span><span class="sxs-lookup"><span data-stu-id="04c3c-215">Don't forget to replace _\<app_name>_ with the name of the web app you created earlier.</span></span>

```bash
az webapp config container set --resource-group myResourceGroup --name <app_name> --multicontainer-config-type compose --multicontainer-config-file docker-compose-wordpress.yml
```

<span data-ttu-id="04c3c-216">When the app has been reconfigured, Cloud Shell shows information similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="04c3c-216">When the app has been reconfigured, Cloud Shell shows information similar to the following example:</span></span>

```json
[
  {
    "name": "DOCKER_CUSTOM_IMAGE_NAME",
    "value": "COMPOSE|dmVyc2lvbjogJzMuMycKCnNlcnZpY2VzOgogICB3b3JkcHJlc3M6CiAgICAgaW1hZ2U6IG1zYW5nYXB1L3dvcmRwcmVzcwogICAgIHBvcnRzOgogICAgICAgLSAiODAwMDo4MCIKICAgICByZXN0YXJ0OiBhbHdheXM="
  }
]
```

### <a name="browse-to-the-app"></a><span data-ttu-id="04c3c-217">Browse to the app</span><span class="sxs-lookup"><span data-stu-id="04c3c-217">Browse to the app</span></span>

<span data-ttu-id="04c3c-218">Browse to the deployed app at (`http://<app_name>.azurewebsites.net`).</span><span class="sxs-lookup"><span data-stu-id="04c3c-218">Browse to the deployed app at (`http://<app_name>.azurewebsites.net`).</span></span> <span data-ttu-id="04c3c-219">The app is now using Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="04c3c-219">The app is now using Azure Database for MySQL.</span></span>

![Sample multicontainer app on Web App for Containers][1]

## <a name="add-persistent-storage"></a><span data-ttu-id="04c3c-221">Add persistent storage</span><span class="sxs-lookup"><span data-stu-id="04c3c-221">Add persistent storage</span></span>

<span data-ttu-id="04c3c-222">Your multi-container is now running in Web App for Containers.</span><span class="sxs-lookup"><span data-stu-id="04c3c-222">Your multi-container is now running in Web App for Containers.</span></span> <span data-ttu-id="04c3c-223">However, if you install WordPress now and restart your app later, you'll find that your WordPress installation is gone.</span><span class="sxs-lookup"><span data-stu-id="04c3c-223">However, if you install WordPress now and restart your app later, you'll find that your WordPress installation is gone.</span></span> <span data-ttu-id="04c3c-224">This happens because your Docker Compose configuration currently points to a storage location inside your container.</span><span class="sxs-lookup"><span data-stu-id="04c3c-224">This happens because your Docker Compose configuration currently points to a storage location inside your container.</span></span> <span data-ttu-id="04c3c-225">The files installed into your container don't persist beyond app restart.</span><span class="sxs-lookup"><span data-stu-id="04c3c-225">The files installed into your container don't persist beyond app restart.</span></span> <span data-ttu-id="04c3c-226">In this section, you'll add persistent storage to your WordPress container.</span><span class="sxs-lookup"><span data-stu-id="04c3c-226">In this section, you'll add persistent storage to your WordPress container.</span></span>

### <a name="configure-environment-variables"></a><span data-ttu-id="04c3c-227">Configure environment variables</span><span class="sxs-lookup"><span data-stu-id="04c3c-227">Configure environment variables</span></span>

<span data-ttu-id="04c3c-228">To use of persistent storage, you'll enable this setting within App Service.</span><span class="sxs-lookup"><span data-stu-id="04c3c-228">To use of persistent storage, you'll enable this setting within App Service.</span></span> <span data-ttu-id="04c3c-229">To make this change, use the [az webapp config appsettings set](/cli/azure/webapp/config/appsettings?view=azure-cli-latest#az-webapp-config-appsettings-set) command in Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="04c3c-229">To make this change, use the [az webapp config appsettings set](/cli/azure/webapp/config/appsettings?view=azure-cli-latest#az-webapp-config-appsettings-set) command in Cloud Shell.</span></span> <span data-ttu-id="04c3c-230">App settings are case-sensitive and space-separated.</span><span class="sxs-lookup"><span data-stu-id="04c3c-230">App settings are case-sensitive and space-separated.</span></span>

```bash
az webapp config appsettings set --resource-group myResourceGroup --name <app_name> --settings WEBSITES_ENABLE_APP_SERVICE_STORAGE=TRUE
```

<span data-ttu-id="04c3c-231">When the app setting has been created, Cloud Shell shows information similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="04c3c-231">When the app setting has been created, Cloud Shell shows information similar to the following example:</span></span>

```json
[
  < JSON data removed for brevity. >
  {
    "name": "WORDPRESS_DB_NAME",
    "slotSetting": false,
    "value": "wordpress"
  },
  {
    "name": "WEBSITES_ENABLE_APP_SERVICE_STORAGE",
    "slotSetting": false,
    "value": "TRUE"
  }
]
```

### <a name="modify-configuration-file"></a><span data-ttu-id="04c3c-232">Modify configuration file</span><span class="sxs-lookup"><span data-stu-id="04c3c-232">Modify configuration file</span></span>

<span data-ttu-id="04c3c-233">In the Cloud Shell, type `nano docker-compose-wordpress.yml` to open the nano text editor.</span><span class="sxs-lookup"><span data-stu-id="04c3c-233">In the Cloud Shell, type `nano docker-compose-wordpress.yml` to open the nano text editor.</span></span>

<span data-ttu-id="04c3c-234">The `volumes` option maps the file system to a directory within the container.</span><span class="sxs-lookup"><span data-stu-id="04c3c-234">The `volumes` option maps the file system to a directory within the container.</span></span> <span data-ttu-id="04c3c-235">`${WEBAPP_STORAGE_HOME}` is an environment variable in App Service that is mapped to persistent storage for your app.</span><span class="sxs-lookup"><span data-stu-id="04c3c-235">`${WEBAPP_STORAGE_HOME}` is an environment variable in App Service that is mapped to persistent storage for your app.</span></span> <span data-ttu-id="04c3c-236">You'll use this environment variable in the volumes option so that the WordPress files are installed into persistent storage instead of the container.</span><span class="sxs-lookup"><span data-stu-id="04c3c-236">You'll use this environment variable in the volumes option so that the WordPress files are installed into persistent storage instead of the container.</span></span> <span data-ttu-id="04c3c-237">Make the following modifications to the file:</span><span class="sxs-lookup"><span data-stu-id="04c3c-237">Make the following modifications to the file:</span></span>

<span data-ttu-id="04c3c-238">In the `wordpress` section, add a `volumes` option so it looks like the following code:</span><span class="sxs-lookup"><span data-stu-id="04c3c-238">In the `wordpress` section, add a `volumes` option so it looks like the following code:</span></span>

```yaml
version: '3.3'

services:
   wordpress:
     image: microsoft/multicontainerwordpress
     volumes:
      - ${WEBAPP_STORAGE_HOME}/site/wwwroot:/var/www/html
     ports:
       - "8000:80"
     restart: always
```

### <a name="update-app-with-new-configuration"></a><span data-ttu-id="04c3c-239">Update app with new configuration</span><span class="sxs-lookup"><span data-stu-id="04c3c-239">Update app with new configuration</span></span>

<span data-ttu-id="04c3c-240">In Cloud Shell, reconfigure your multi-container [web app](app-service-linux-intro.md) with the [az webapp config container set](/cli/azure/webapp/config/container?view=azure-cli-latest#az-webapp-config-container-set) command.</span><span class="sxs-lookup"><span data-stu-id="04c3c-240">In Cloud Shell, reconfigure your multi-container [web app](app-service-linux-intro.md) with the [az webapp config container set](/cli/azure/webapp/config/container?view=azure-cli-latest#az-webapp-config-container-set) command.</span></span> <span data-ttu-id="04c3c-241">Don't forget to replace _\<app_name>_ with a unique app name.</span><span class="sxs-lookup"><span data-stu-id="04c3c-241">Don't forget to replace _\<app_name>_ with a unique app name.</span></span>

```bash
az webapp config container set --resource-group myResourceGroup --name <app_name> --multicontainer-config-type compose --multicontainer-config-file docker-compose-wordpress.yml
```

<span data-ttu-id="04c3c-242">After your command runs, it shows output similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="04c3c-242">After your command runs, it shows output similar to the following example:</span></span>

```json
[
  {
    "name": "WEBSITES_ENABLE_APP_SERVICE_STORAGE",
    "slotSetting": false,
    "value": "TRUE"
  },
  {
    "name": "DOCKER_CUSTOM_IMAGE_NAME",
    "value": "COMPOSE|dmVyc2lvbjogJzMuMycKCnNlcnZpY2VzOgogICBteXNxbDoKICAgICBpbWFnZTogbXlzcWw6NS43CiAgICAgdm9sdW1lczoKICAgICAgIC0gZGJfZGF0YTovdmFyL2xpYi9teXNxbAogICAgIHJlc3RhcnQ6IGFsd2F5cwogICAgIGVudmlyb25tZW50OgogICAgICAgTVlTUUxfUk9PVF9QQVNTV09SRDogZXhhbXBsZXBhc3MKCiAgIHdvcmRwcmVzczoKICAgICBkZXBlbmRzX29uOgogICAgICAgLSBteXNxbAogICAgIGltYWdlOiB3b3JkcHJlc3M6bGF0ZXN0CiAgICAgcG9ydHM6CiAgICAgICAtICI4MDAwOjgwIgogICAgIHJlc3RhcnQ6IGFsd2F5cwogICAgIGVudmlyb25tZW50OgogICAgICAgV09SRFBSRVNTX0RCX1BBU1NXT1JEOiBleGFtcGxlcGFzcwp2b2x1bWVzOgogICAgZGJfZGF0YTo="
  }
]
```

### <a name="browse-to-the-app"></a><span data-ttu-id="04c3c-243">Browse to the app</span><span class="sxs-lookup"><span data-stu-id="04c3c-243">Browse to the app</span></span>

<span data-ttu-id="04c3c-244">Browse to the deployed app at (`http://<app_name>.azurewebsites.net`).</span><span class="sxs-lookup"><span data-stu-id="04c3c-244">Browse to the deployed app at (`http://<app_name>.azurewebsites.net`).</span></span>

<span data-ttu-id="04c3c-245">The WordPress container is now using Azure Database for MySQL and persistent storage.</span><span class="sxs-lookup"><span data-stu-id="04c3c-245">The WordPress container is now using Azure Database for MySQL and persistent storage.</span></span>

## <a name="add-redis-container"></a><span data-ttu-id="04c3c-246">Add Redis container</span><span class="sxs-lookup"><span data-stu-id="04c3c-246">Add Redis container</span></span>

 <span data-ttu-id="04c3c-247">The WordPress 'official image' does not include the dependencies for Redis.</span><span class="sxs-lookup"><span data-stu-id="04c3c-247">The WordPress 'official image' does not include the dependencies for Redis.</span></span> <span data-ttu-id="04c3c-248">These dependencies and additional configuration needed to use Redis with WordPress have been prepared for you in this [custom image](https://github.com/Azure-Samples/multicontainerwordpress).</span><span class="sxs-lookup"><span data-stu-id="04c3c-248">These dependencies and additional configuration needed to use Redis with WordPress have been prepared for you in this [custom image](https://github.com/Azure-Samples/multicontainerwordpress).</span></span> <span data-ttu-id="04c3c-249">In practice, you would add desired changes to your own image.</span><span class="sxs-lookup"><span data-stu-id="04c3c-249">In practice, you would add desired changes to your own image.</span></span>

<span data-ttu-id="04c3c-250">The custom image is based on the 'official image' of [WordPress from Docker Hub](https://hub.docker.com/_/wordpress/).</span><span class="sxs-lookup"><span data-stu-id="04c3c-250">The custom image is based on the 'official image' of [WordPress from Docker Hub](https://hub.docker.com/_/wordpress/).</span></span> <span data-ttu-id="04c3c-251">The following changes have been made in this custom image for Redis:</span><span class="sxs-lookup"><span data-stu-id="04c3c-251">The following changes have been made in this custom image for Redis:</span></span>

* [<span data-ttu-id="04c3c-252">Adds PHP extension for Redis v4.0.2.</span><span class="sxs-lookup"><span data-stu-id="04c3c-252">Adds PHP extension for Redis v4.0.2.</span></span>](https://github.com/Azure-Samples/multicontainerwordpress/blob/5669a89e0ee8599285f0e2e6f7e935c16e539b92/Dockerfile#L35)
* [<span data-ttu-id="04c3c-253">Adds unzip needed for file extraction.</span><span class="sxs-lookup"><span data-stu-id="04c3c-253">Adds unzip needed for file extraction.</span></span>](https://github.com/Azure-Samples/multicontainerwordpress/blob/5669a89e0ee8599285f0e2e6f7e935c16e539b92/docker-entrypoint.sh#L71)
* [<span data-ttu-id="04c3c-254">Adds Redis Object Cache 1.3.8 WordPress plugin.</span><span class="sxs-lookup"><span data-stu-id="04c3c-254">Adds Redis Object Cache 1.3.8 WordPress plugin.</span></span>](https://github.com/Azure-Samples/multicontainerwordpress/blob/5669a89e0ee8599285f0e2e6f7e935c16e539b92/docker-entrypoint.sh#L74)
* [<span data-ttu-id="04c3c-255">Uses App Setting for Redis host name in WordPress wp-config.php.</span><span class="sxs-lookup"><span data-stu-id="04c3c-255">Uses App Setting for Redis host name in WordPress wp-config.php.</span></span>](https://github.com/Azure-Samples/multicontainerwordpress/blob/5669a89e0ee8599285f0e2e6f7e935c16e539b92/docker-entrypoint.sh#L162)

<span data-ttu-id="04c3c-256">Add the redis container to the bottom of the configuration file so it looks like the following example:</span><span class="sxs-lookup"><span data-stu-id="04c3c-256">Add the redis container to the bottom of the configuration file so it looks like the following example:</span></span>

[!code-yml[Main](../../../azure-app-service-multi-container/compose-wordpress.yml)]

### <a name="configure-environment-variables"></a><span data-ttu-id="04c3c-257">Configure environment variables</span><span class="sxs-lookup"><span data-stu-id="04c3c-257">Configure environment variables</span></span>

<span data-ttu-id="04c3c-258">To use Redis, you'll enable this setting, `WP_REDIS_HOST`, within App Service.</span><span class="sxs-lookup"><span data-stu-id="04c3c-258">To use Redis, you'll enable this setting, `WP_REDIS_HOST`, within App Service.</span></span> <span data-ttu-id="04c3c-259">This is a *required setting* for WordPress to communicate with the Redis host.</span><span class="sxs-lookup"><span data-stu-id="04c3c-259">This is a *required setting* for WordPress to communicate with the Redis host.</span></span> <span data-ttu-id="04c3c-260">To make this change, use the [az webapp config appsettings set](/cli/azure/webapp/config/appsettings?view=azure-cli-latest#az-webapp-config-appsettings-set) command in Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="04c3c-260">To make this change, use the [az webapp config appsettings set](/cli/azure/webapp/config/appsettings?view=azure-cli-latest#az-webapp-config-appsettings-set) command in Cloud Shell.</span></span> <span data-ttu-id="04c3c-261">App settings are case-sensitive and space-separated.</span><span class="sxs-lookup"><span data-stu-id="04c3c-261">App settings are case-sensitive and space-separated.</span></span>

```bash
az webapp config appsettings set --resource-group myResourceGroup --name <app_name> --settings WP_REDIS_HOST="redis"
```

<span data-ttu-id="04c3c-262">When the app setting has been created, Cloud Shell shows information similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="04c3c-262">When the app setting has been created, Cloud Shell shows information similar to the following example:</span></span>

```json
[
  < JSON data removed for brevity. >
  {
    "name": "WORDPRESS_DB_USER",
    "slotSetting": false,
    "value": "adminuser@<mysql_server_name>"
  },
  {
    "name": "WP_REDIS_HOST",
    "slotSetting": false,
    "value": "redis"
  }
]
```

### <a name="update-app-with-new-configuration"></a><span data-ttu-id="04c3c-263">Update app with new configuration</span><span class="sxs-lookup"><span data-stu-id="04c3c-263">Update app with new configuration</span></span>

<span data-ttu-id="04c3c-264">In Cloud Shell, reconfigure your multi-container [web app](app-service-linux-intro.md) with the [az webapp config container set](/cli/azure/webapp/config/container?view=azure-cli-latest#az-webapp-config-container-set) command.</span><span class="sxs-lookup"><span data-stu-id="04c3c-264">In Cloud Shell, reconfigure your multi-container [web app](app-service-linux-intro.md) with the [az webapp config container set](/cli/azure/webapp/config/container?view=azure-cli-latest#az-webapp-config-container-set) command.</span></span> <span data-ttu-id="04c3c-265">Don't forget to replace _\<app_name>_ with a unique app name.</span><span class="sxs-lookup"><span data-stu-id="04c3c-265">Don't forget to replace _\<app_name>_ with a unique app name.</span></span>

```bash
az webapp config container set --resource-group myResourceGroup --name <app_name> --multicontainer-config-type compose --multicontainer-config-file compose-wordpress.yml
```

<span data-ttu-id="04c3c-266">After your command runs, it shows output similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="04c3c-266">After your command runs, it shows output similar to the following example:</span></span>

```json
[
  {
    "name": "DOCKER_CUSTOM_IMAGE_NAME",
    "value": "COMPOSE|dmVyc2lvbjogJzMuMycKCnNlcnZpY2VzOgogICBteXNxbDoKICAgICBpbWFnZTogbXlzcWw6NS43CiAgICAgdm9sdW1lczoKICAgICAgIC0gZGJfZGF0YTovdmFyL2xpYi9teXNxbAogICAgIHJlc3RhcnQ6IGFsd2F5cwogICAgIGVudmlyb25tZW50OgogICAgICAgTVlTUUxfUk9PVF9QQVNTV09SRDogZXhhbXBsZXBhc3MKCiAgIHdvcmRwcmVzczoKICAgICBkZXBlbmRzX29uOgogICAgICAgLSBteXNxbAogICAgIGltYWdlOiB3b3JkcHJlc3M6bGF0ZXN0CiAgICAgcG9ydHM6CiAgICAgICAtICI4MDAwOjgwIgogICAgIHJlc3RhcnQ6IGFsd2F5cwogICAgIGVudmlyb25tZW50OgogICAgICAgV09SRFBSRVNTX0RCX1BBU1NXT1JEOiBleGFtcGxlcGFzcwp2b2x1bWVzOgogICAgZGJfZGF0YTo="
  }
]
```

### <a name="browse-to-the-app"></a><span data-ttu-id="04c3c-267">Browse to the app</span><span class="sxs-lookup"><span data-stu-id="04c3c-267">Browse to the app</span></span>

<span data-ttu-id="04c3c-268">Browse to the deployed app at (`http://<app_name>.azurewebsites.net`).</span><span class="sxs-lookup"><span data-stu-id="04c3c-268">Browse to the deployed app at (`http://<app_name>.azurewebsites.net`).</span></span>

<span data-ttu-id="04c3c-269">Complete the steps and install WordPress.</span><span class="sxs-lookup"><span data-stu-id="04c3c-269">Complete the steps and install WordPress.</span></span>

### <a name="connect-wordpress-to-redis"></a><span data-ttu-id="04c3c-270">Connect WordPress to Redis</span><span class="sxs-lookup"><span data-stu-id="04c3c-270">Connect WordPress to Redis</span></span>

<span data-ttu-id="04c3c-271">Log-in to WordPress admin. In the left navigation, select **Plugins**, and then select **Installed Plugins**.</span><span class="sxs-lookup"><span data-stu-id="04c3c-271">Log-in to WordPress admin. In the left navigation, select **Plugins**, and then select **Installed Plugins**.</span></span>

![Select WordPress Plugins][2]

<span data-ttu-id="04c3c-273">Show all plugins here</span><span class="sxs-lookup"><span data-stu-id="04c3c-273">Show all plugins here</span></span>

<span data-ttu-id="04c3c-274">In the plugins page, find **Redis Object Cache** and click **Activate**.</span><span class="sxs-lookup"><span data-stu-id="04c3c-274">In the plugins page, find **Redis Object Cache** and click **Activate**.</span></span>

![Activate Redis][3]

<span data-ttu-id="04c3c-276">Click on **Settings**.</span><span class="sxs-lookup"><span data-stu-id="04c3c-276">Click on **Settings**.</span></span>

![Click on Settings][4]

<span data-ttu-id="04c3c-278">Click the **Enable Object Cache** button.</span><span class="sxs-lookup"><span data-stu-id="04c3c-278">Click the **Enable Object Cache** button.</span></span>

![Click the 'Enable Object Cache' button][5]

<span data-ttu-id="04c3c-280">WordPress connects to the Redis server.</span><span class="sxs-lookup"><span data-stu-id="04c3c-280">WordPress connects to the Redis server.</span></span> <span data-ttu-id="04c3c-281">The connection **status** appears on the same page.</span><span class="sxs-lookup"><span data-stu-id="04c3c-281">The connection **status** appears on the same page.</span></span>

![WordPress connects to the Redis server.][6]

<span data-ttu-id="04c3c-284">**Congratulations**, you've connected WordPress to Redis.</span><span class="sxs-lookup"><span data-stu-id="04c3c-284">**Congratulations**, you've connected WordPress to Redis.</span></span> <span data-ttu-id="04c3c-285">The production-ready app is now using **Azure Database for MySQL, persistent storage, and Redis**.</span><span class="sxs-lookup"><span data-stu-id="04c3c-285">The production-ready app is now using **Azure Database for MySQL, persistent storage, and Redis**.</span></span> <span data-ttu-id="04c3c-286">You can now scale out your App Service Plan to multiple instances.</span><span class="sxs-lookup"><span data-stu-id="04c3c-286">You can now scale out your App Service Plan to multiple instances.</span></span>

## <a name="use-a-kubernetes-configuration-optional"></a><span data-ttu-id="04c3c-287">Use a Kubernetes configuration (optional)</span><span class="sxs-lookup"><span data-stu-id="04c3c-287">Use a Kubernetes configuration (optional)</span></span>

<span data-ttu-id="04c3c-288">In this section, you'll learn how to use a Kubernetes configuration to deploy multiple containers.</span><span class="sxs-lookup"><span data-stu-id="04c3c-288">In this section, you'll learn how to use a Kubernetes configuration to deploy multiple containers.</span></span> <span data-ttu-id="04c3c-289">Make sure you follow earlier steps in to create a [resource group](#create-a-resource-group) and an [App Service plan](#create-an-azure-app-service-plan).</span><span class="sxs-lookup"><span data-stu-id="04c3c-289">Make sure you follow earlier steps in to create a [resource group](#create-a-resource-group) and an [App Service plan](#create-an-azure-app-service-plan).</span></span> <span data-ttu-id="04c3c-290">Since the majority of the steps are similar to that of the compose section, the configuration file has been combined for you.</span><span class="sxs-lookup"><span data-stu-id="04c3c-290">Since the majority of the steps are similar to that of the compose section, the configuration file has been combined for you.</span></span>

### <a name="supported-kubernetes-options-for-multi-container"></a><span data-ttu-id="04c3c-291">Supported Kubernetes options for multi-container</span><span class="sxs-lookup"><span data-stu-id="04c3c-291">Supported Kubernetes options for multi-container</span></span>

* <span data-ttu-id="04c3c-292">args</span><span class="sxs-lookup"><span data-stu-id="04c3c-292">args</span></span>
* <span data-ttu-id="04c3c-293">command</span><span class="sxs-lookup"><span data-stu-id="04c3c-293">command</span></span>
* <span data-ttu-id="04c3c-294">containers</span><span class="sxs-lookup"><span data-stu-id="04c3c-294">containers</span></span>
* <span data-ttu-id="04c3c-295">image</span><span class="sxs-lookup"><span data-stu-id="04c3c-295">image</span></span>
* <span data-ttu-id="04c3c-296">name</span><span class="sxs-lookup"><span data-stu-id="04c3c-296">name</span></span>
* <span data-ttu-id="04c3c-297">ports</span><span class="sxs-lookup"><span data-stu-id="04c3c-297">ports</span></span>
* <span data-ttu-id="04c3c-298">spec</span><span class="sxs-lookup"><span data-stu-id="04c3c-298">spec</span></span>

> [!NOTE]
><span data-ttu-id="04c3c-299">Any other Kubernetes options not explicitly called out aren't supported in Public Preview.</span><span class="sxs-lookup"><span data-stu-id="04c3c-299">Any other Kubernetes options not explicitly called out aren't supported in Public Preview.</span></span>
>

### <a name="kubernetes-configuration-file"></a><span data-ttu-id="04c3c-300">Kubernetes configuration file</span><span class="sxs-lookup"><span data-stu-id="04c3c-300">Kubernetes configuration file</span></span>

<span data-ttu-id="04c3c-301">You'll use *kubernetes-wordpress.yml* for this portion of the tutorial.</span><span class="sxs-lookup"><span data-stu-id="04c3c-301">You'll use *kubernetes-wordpress.yml* for this portion of the tutorial.</span></span> <span data-ttu-id="04c3c-302">It is displayed here for your reference:</span><span class="sxs-lookup"><span data-stu-id="04c3c-302">It is displayed here for your reference:</span></span>

[!code-yml[Main](../../../azure-app-service-multi-container/kubernetes-wordpress.yml)]

### <a name="create-an-azure-database-for-mysql-server"></a><span data-ttu-id="04c3c-303">Create an Azure Database for MySQL server</span><span class="sxs-lookup"><span data-stu-id="04c3c-303">Create an Azure Database for MySQL server</span></span>

<span data-ttu-id="04c3c-304">Create a server in Azure Database for MySQL with the [`az mysql server create`](/cli/azure/mysql/server?view=azure-cli-latest#az-mysql-server-create) command.</span><span class="sxs-lookup"><span data-stu-id="04c3c-304">Create a server in Azure Database for MySQL with the [`az mysql server create`](/cli/azure/mysql/server?view=azure-cli-latest#az-mysql-server-create) command.</span></span>

<span data-ttu-id="04c3c-305">In the following command, substitute your MySQL server name where you see the _&lt;mysql_server_name>_ placeholder (valid characters are `a-z`, `0-9`, and `-`).</span><span class="sxs-lookup"><span data-stu-id="04c3c-305">In the following command, substitute your MySQL server name where you see the _&lt;mysql_server_name>_ placeholder (valid characters are `a-z`, `0-9`, and `-`).</span></span> <span data-ttu-id="04c3c-306">This name is part of the MySQL server's hostname  (`<mysql_server_name>.database.windows.net`), it needs to be globally unique.</span><span class="sxs-lookup"><span data-stu-id="04c3c-306">This name is part of the MySQL server's hostname  (`<mysql_server_name>.database.windows.net`), it needs to be globally unique.</span></span>

```azurecli-interactive
az mysql server create --resource-group myResourceGroup --name <mysql_server_name>  --location "South Central US" --admin-user adminuser --admin-password My5up3rStr0ngPaSw0rd! --sku-name B_Gen4_1 --version 5.7
```

<span data-ttu-id="04c3c-307">When the MySQL server is created, Cloud Shell shows information similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="04c3c-307">When the MySQL server is created, Cloud Shell shows information similar to the following example:</span></span>

```json
{
  "administratorLogin": "adminuser",
  "administratorLoginPassword": null,
  "fullyQualifiedDomainName": "<mysql_server_name>.database.windows.net",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.DBforMySQL/servers/<mysql_server_name>",
  "location": "southcentralus",
  "name": "<mysql_server_name>",
  "resourceGroup": "myResourceGroup",
  ...
}
```

### <a name="configure-server-firewall"></a><span data-ttu-id="04c3c-308">Configure server firewall</span><span class="sxs-lookup"><span data-stu-id="04c3c-308">Configure server firewall</span></span>

<span data-ttu-id="04c3c-309">Create a firewall rule for your MySQL server to allow client connections by using the [`az mysql server firewall-rule create`](/cli/azure/mysql/server/firewall-rule?view=azure-cli-latest#az-mysql-server-firewall-rule-create) command.</span><span class="sxs-lookup"><span data-stu-id="04c3c-309">Create a firewall rule for your MySQL server to allow client connections by using the [`az mysql server firewall-rule create`](/cli/azure/mysql/server/firewall-rule?view=azure-cli-latest#az-mysql-server-firewall-rule-create) command.</span></span> <span data-ttu-id="04c3c-310">When both starting IP and end IP are set to 0.0.0.0, the firewall is only opened for other Azure resources.</span><span class="sxs-lookup"><span data-stu-id="04c3c-310">When both starting IP and end IP are set to 0.0.0.0, the firewall is only opened for other Azure resources.</span></span>

```azurecli-interactive
az mysql server firewall-rule create --name allAzureIPs --server <mysql_server_name> --resource-group myResourceGroup --start-ip-address 0.0.0.0 --end-ip-address 0.0.0.0
```

> [!TIP]
> <span data-ttu-id="04c3c-311">You can be even more restrictive in your firewall rule by [using only the outbound IP addresses your app uses](../app-service-ip-addresses.md?toc=%2fazure%2fapp-service%2fcontainers%2ftoc.json#find-outbound-ips).</span><span class="sxs-lookup"><span data-stu-id="04c3c-311">You can be even more restrictive in your firewall rule by [using only the outbound IP addresses your app uses](../app-service-ip-addresses.md?toc=%2fazure%2fapp-service%2fcontainers%2ftoc.json#find-outbound-ips).</span></span>
>

### <a name="create-the-wordpress-database"></a><span data-ttu-id="04c3c-312">Create the WordPress database</span><span class="sxs-lookup"><span data-stu-id="04c3c-312">Create the WordPress database</span></span>

<span data-ttu-id="04c3c-313">If you haven't already, create an [Azure Database for MySQL server](#create-an-azure-database-for-mysql-server).</span><span class="sxs-lookup"><span data-stu-id="04c3c-313">If you haven't already, create an [Azure Database for MySQL server](#create-an-azure-database-for-mysql-server).</span></span>

```bash
az mysql db create --resource-group myResourceGroup --server-name <mysql_server_name> --name wordpress
```

<span data-ttu-id="04c3c-314">When the database has been created, Cloud Shell shows information similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="04c3c-314">When the database has been created, Cloud Shell shows information similar to the following example:</span></span>

```json
{
  "additionalProperties": {},
  "charset": "latin1",
  "collation": "latin1_swedish_ci",
  "id": "/subscriptions/12db1644-4b12-4cab-ba54-8ba2f2822c1f/resourceGroups/myResourceGroup/providers/Microsoft.DBforMySQL/servers/<mysql_server_name>/databases/wordpress",
  "name": "wordpress",
  "resourceGroup": "myResourceGroup",
  "type": "Microsoft.DBforMySQL/servers/databases"
}
```

### <a name="create-a-multi-container-app-kubernetes"></a><span data-ttu-id="04c3c-315">Create a multi-container app (Kubernetes)</span><span class="sxs-lookup"><span data-stu-id="04c3c-315">Create a multi-container app (Kubernetes)</span></span>

<span data-ttu-id="04c3c-316">In Cloud Shell, create a multi-container [web app](app-service-linux-intro.md) in the `myResourceGroup` resource group and the `myAppServicePlan` App Service plan with the [az webapp create](/cli/azure/webapp?view=azure-cli-latest#az-webapp-create) command.</span><span class="sxs-lookup"><span data-stu-id="04c3c-316">In Cloud Shell, create a multi-container [web app](app-service-linux-intro.md) in the `myResourceGroup` resource group and the `myAppServicePlan` App Service plan with the [az webapp create](/cli/azure/webapp?view=azure-cli-latest#az-webapp-create) command.</span></span> <span data-ttu-id="04c3c-317">Don't forget to replace _\<app_name>_ with a unique app name.</span><span class="sxs-lookup"><span data-stu-id="04c3c-317">Don't forget to replace _\<app_name>_ with a unique app name.</span></span>

```bash
az webapp create --resource-group myResourceGroup --plan myAppServicePlan --name <app_name> --multicontainer-config-type kube --multicontainer-config-file kubernetes-wordpress.yml
```

<span data-ttu-id="04c3c-318">When the web app has been created, Cloud Shell shows output similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="04c3c-318">When the web app has been created, Cloud Shell shows output similar to the following example:</span></span>

```json
{
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
  "cloningInfo": null,
  "containerSize": 0,
  "dailyMemoryTimeQuota": 0,
  "defaultHostName": "<app_name>.azurewebsites.net",
  "enabled": true,
  < JSON data removed for brevity. >
}
```

### <a name="configure-database-variables-in-wordpress"></a><span data-ttu-id="04c3c-319">Configure database variables in WordPress</span><span class="sxs-lookup"><span data-stu-id="04c3c-319">Configure database variables in WordPress</span></span>

<span data-ttu-id="04c3c-320">To connect the WordPress app to this new MySQL server, you'll configure a few WordPress-specific environment variables.</span><span class="sxs-lookup"><span data-stu-id="04c3c-320">To connect the WordPress app to this new MySQL server, you'll configure a few WordPress-specific environment variables.</span></span> <span data-ttu-id="04c3c-321">To make this change, use the [az webapp config appsettings set](/cli/azure/webapp/config/appsettings?view=azure-cli-latest#az-webapp-config-appsettings-set) command in Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="04c3c-321">To make this change, use the [az webapp config appsettings set](/cli/azure/webapp/config/appsettings?view=azure-cli-latest#az-webapp-config-appsettings-set) command in Cloud Shell.</span></span> <span data-ttu-id="04c3c-322">App settings are case-sensitive and space-separated.</span><span class="sxs-lookup"><span data-stu-id="04c3c-322">App settings are case-sensitive and space-separated.</span></span>

```bash
az webapp config appsettings set --resource-group myResourceGroup --name <app_name> --settings WORDPRESS_DB_HOST="<mysql_server_name>.mysql.database.azure.com" WORDPRESS_DB_USER="adminuser@<mysql_server_name>" WORDPRESS_DB_PASSWORD="My5up3rStr0ngPaSw0rd!" WORDPRESS_DB_NAME="wordpress" MYSQL_SSL_CA="BaltimoreCyberTrustroot.crt.pem"
```

<span data-ttu-id="04c3c-323">When the app setting has been created, Cloud Shell shows information similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="04c3c-323">When the app setting has been created, Cloud Shell shows information similar to the following example:</span></span>

```json
[
  {
    "name": "WORDPRESS_DB_HOST",
    "slotSetting": false,
    "value": "<mysql_server_name>.mysql.database.azure.com"
  },
  {
    "name": "WORDPRESS_DB_USER",
    "slotSetting": false,
    "value": "adminuser@<mysql_server_name>"
  },
  {
    "name": "WORDPRESS_DB_NAME",
    "slotSetting": false,
    "value": "wordpress"
  },
  {
    "name": "WORDPRESS_DB_PASSWORD",
    "slotSetting": false,
    "value": "My5up3rStr0ngPaSw0rd!"
  }
]
```

### <a name="add-persistent-storage"></a><span data-ttu-id="04c3c-324">Add persistent storage</span><span class="sxs-lookup"><span data-stu-id="04c3c-324">Add persistent storage</span></span>

<span data-ttu-id="04c3c-325">Your multi-container is now running in Web App for Containers.</span><span class="sxs-lookup"><span data-stu-id="04c3c-325">Your multi-container is now running in Web App for Containers.</span></span> <span data-ttu-id="04c3c-326">The data will be erased on restart because the files aren't persisted.</span><span class="sxs-lookup"><span data-stu-id="04c3c-326">The data will be erased on restart because the files aren't persisted.</span></span> <span data-ttu-id="04c3c-327">In this section, you'll add persistent storage to your WordPress container.</span><span class="sxs-lookup"><span data-stu-id="04c3c-327">In this section, you'll add persistent storage to your WordPress container.</span></span>

### <a name="configure-environment-variables"></a><span data-ttu-id="04c3c-328">Configure environment variables</span><span class="sxs-lookup"><span data-stu-id="04c3c-328">Configure environment variables</span></span>

<span data-ttu-id="04c3c-329">To use of persistent storage, you'll enable this setting within App Service.</span><span class="sxs-lookup"><span data-stu-id="04c3c-329">To use of persistent storage, you'll enable this setting within App Service.</span></span> <span data-ttu-id="04c3c-330">To make this change, use the [az webapp config appsettings set](/cli/azure/webapp/config/appsettings?view=azure-cli-latest#az-webapp-config-appsettings-set) command in Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="04c3c-330">To make this change, use the [az webapp config appsettings set](/cli/azure/webapp/config/appsettings?view=azure-cli-latest#az-webapp-config-appsettings-set) command in Cloud Shell.</span></span> <span data-ttu-id="04c3c-331">App settings are case-sensitive and space-separated.</span><span class="sxs-lookup"><span data-stu-id="04c3c-331">App settings are case-sensitive and space-separated.</span></span>

```bash
az webapp config appsettings set --resource-group myResourceGroup --name <app_name> --settings WEBSITES_ENABLE_APP_SERVICE_STORAGE=TRUE
```

<span data-ttu-id="04c3c-332">When the app setting has been created, Cloud Shell shows information similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="04c3c-332">When the app setting has been created, Cloud Shell shows information similar to the following example:</span></span>

```json
[
  {
    "name": "WEBSITES_ENABLE_APP_SERVICE_STORAGE",
    "slotSetting": false,
    "value": "TRUE"
  }
]
```

### <a name="browse-to-the-app"></a><span data-ttu-id="04c3c-333">Browse to the app</span><span class="sxs-lookup"><span data-stu-id="04c3c-333">Browse to the app</span></span>

<span data-ttu-id="04c3c-334">Browse to the deployed app at (`http://<app_name>.azurewebsites.net`).</span><span class="sxs-lookup"><span data-stu-id="04c3c-334">Browse to the deployed app at (`http://<app_name>.azurewebsites.net`).</span></span>

<span data-ttu-id="04c3c-335">The app is now running multiple containers in Web App for Containers.</span><span class="sxs-lookup"><span data-stu-id="04c3c-335">The app is now running multiple containers in Web App for Containers.</span></span>

![Sample multicontainer app on Web App for Containers][1]

<span data-ttu-id="04c3c-337">**Congratulations**, you've created a multi-container app in Web App for Containers.</span><span class="sxs-lookup"><span data-stu-id="04c3c-337">**Congratulations**, you've created a multi-container app in Web App for Containers.</span></span>

<span data-ttu-id="04c3c-338">To use Redis, follow the steps in [Connect WordPress to Redis](#connect-wordpress-to-redis).</span><span class="sxs-lookup"><span data-stu-id="04c3c-338">To use Redis, follow the steps in [Connect WordPress to Redis](#connect-wordpress-to-redis).</span></span>

## <a name="find-docker-container-logs"></a><span data-ttu-id="04c3c-339">Find Docker Container logs</span><span class="sxs-lookup"><span data-stu-id="04c3c-339">Find Docker Container logs</span></span>

<span data-ttu-id="04c3c-340">If you run into issues using multiple containers, you can access the container logs by browsing to: `https://<app_name>.scm.azurewebsites.net/api/logs/docker`.</span><span class="sxs-lookup"><span data-stu-id="04c3c-340">If you run into issues using multiple containers, you can access the container logs by browsing to: `https://<app_name>.scm.azurewebsites.net/api/logs/docker`.</span></span>

<span data-ttu-id="04c3c-341">You'll see output similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="04c3c-341">You'll see output similar to the following example:</span></span>

```json
[
   {
      "machineName":"RD00XYZYZE567A",
      "lastUpdated":"2018-05-10T04:11:45Z",
      "size":25125,
      "href":"https://<app_name>.scm.azurewebsites.net/api/vfs/LogFiles/2018_05_10_RD00XYZYZE567A_docker.log",
      "path":"/home/LogFiles/2018_05_10_RD00XYZYZE567A_docker.log"
   }
]
```

<span data-ttu-id="04c3c-342">You see a log for each container and an additional log for the parent process.</span><span class="sxs-lookup"><span data-stu-id="04c3c-342">You see a log for each container and an additional log for the parent process.</span></span> <span data-ttu-id="04c3c-343">Copy the respective `href` value into the browser to view the log.</span><span class="sxs-lookup"><span data-stu-id="04c3c-343">Copy the respective `href` value into the browser to view the log.</span></span>

[!INCLUDE [Clean-up section](../../../includes/cli-script-clean-up.md)]

<span data-ttu-id="04c3c-344">In this tutorial, you learned how to:</span><span class="sxs-lookup"><span data-stu-id="04c3c-344">In this tutorial, you learned how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="04c3c-345">Convert a Docker Compose configuration to work with Web App for Containers</span><span class="sxs-lookup"><span data-stu-id="04c3c-345">Convert a Docker Compose configuration to work with Web App for Containers</span></span>
> * <span data-ttu-id="04c3c-346">Convert a Kubernetes configuration to work with Web App for Containers</span><span class="sxs-lookup"><span data-stu-id="04c3c-346">Convert a Kubernetes configuration to work with Web App for Containers</span></span>
> * <span data-ttu-id="04c3c-347">Deploy a multi-container app to Azure</span><span class="sxs-lookup"><span data-stu-id="04c3c-347">Deploy a multi-container app to Azure</span></span>
> * <span data-ttu-id="04c3c-348">Add application settings</span><span class="sxs-lookup"><span data-stu-id="04c3c-348">Add application settings</span></span>
> * <span data-ttu-id="04c3c-349">Use persistent storage for your containers</span><span class="sxs-lookup"><span data-stu-id="04c3c-349">Use persistent storage for your containers</span></span>
> * <span data-ttu-id="04c3c-350">Connect to Azure Database for MySQL</span><span class="sxs-lookup"><span data-stu-id="04c3c-350">Connect to Azure Database for MySQL</span></span>
> * <span data-ttu-id="04c3c-351">Troubleshoot errors</span><span class="sxs-lookup"><span data-stu-id="04c3c-351">Troubleshoot errors</span></span>

## <a name="next-steps"></a><span data-ttu-id="04c3c-352">Next steps</span><span class="sxs-lookup"><span data-stu-id="04c3c-352">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="04c3c-353">Use a custom Docker image for Web App for Containers</span><span class="sxs-lookup"><span data-stu-id="04c3c-353">Use a custom Docker image for Web App for Containers</span></span>](tutorial-custom-docker-image.md)

<!--Image references-->
[1]: ./media/tutorial-multi-container-app/azure-multi-container-wordpress-install.png
[2]: ./media/tutorial-multi-container-app/wordpress-plugins.png
[3]: ./media/tutorial-multi-container-app/activate-redis.png
[4]: ./media/tutorial-multi-container-app/redis-settings.png
[5]: ./media/tutorial-multi-container-app/enable-object-cache.png
[6]: ./media/tutorial-multi-container-app/redis-connected.png
