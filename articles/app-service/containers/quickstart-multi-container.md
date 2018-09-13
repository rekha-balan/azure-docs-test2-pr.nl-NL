---
title: Create a multi-container (preview) app in Azure Web App for Containers using a Docker Compose configuration
description: Deploy your first multi-container app in Azure Web App for Containers in minutes
keywords: azure app service, web app, linux, docker, compose, multicontainer, multi-container, web app for containers, multiple containers, container, kubernetes, wordpress, azure db for mysql, production database with containers
services: app-service\web
documentationcenter: ''
author: msangapu
manager: jeconnoc
editor: ''
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 06/22/2018
ms.author: msangapu
ms.custom: mvc
ms.openlocfilehash: 6fa0bab5d2b402c85ea3ee70e7356f8c8c989ab9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869689"
---
# <a name="create-a-multi-container-preview-app-using-web-app-for-containers"></a><span data-ttu-id="36ba6-104">Create a multi-container (preview) app using Web App for Containers</span><span class="sxs-lookup"><span data-stu-id="36ba6-104">Create a multi-container (preview) app using Web App for Containers</span></span>

<span data-ttu-id="36ba6-105">[Web App for Containers](app-service-linux-intro.md) provides a flexible way to use Docker images.</span><span class="sxs-lookup"><span data-stu-id="36ba6-105">[Web App for Containers](app-service-linux-intro.md) provides a flexible way to use Docker images.</span></span> <span data-ttu-id="36ba6-106">This quickstart shows how to deploy a multi-container app to Web App for Containers in the [Cloud Shell](https://docs.microsoft.com/en-us/azure/cloud-shell/overview) using a Docker Compose configuration.</span><span class="sxs-lookup"><span data-stu-id="36ba6-106">This quickstart shows how to deploy a multi-container app to Web App for Containers in the [Cloud Shell](https://docs.microsoft.com/en-us/azure/cloud-shell/overview) using a Docker Compose configuration.</span></span> <span data-ttu-id="36ba6-107">For Kubernetes and a full end-to-end solution using Azure DB for MySQL, follow the [multi-container tutorial](tutorial-multi-container-app.md).</span><span class="sxs-lookup"><span data-stu-id="36ba6-107">For Kubernetes and a full end-to-end solution using Azure DB for MySQL, follow the [multi-container tutorial](tutorial-multi-container-app.md).</span></span>

<span data-ttu-id="36ba6-108">You'll complete this quickstart in Cloud Shell, but you can also run these commands locally with [Azure CLI](/cli/azure/install-azure-cli) (2.0.32 or later).</span><span class="sxs-lookup"><span data-stu-id="36ba6-108">You'll complete this quickstart in Cloud Shell, but you can also run these commands locally with [Azure CLI](/cli/azure/install-azure-cli) (2.0.32 or later).</span></span> 

![Sample multi-container app on Web App for Containers][1]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="download-the-sample"></a><span data-ttu-id="36ba6-110">Download the sample</span><span class="sxs-lookup"><span data-stu-id="36ba6-110">Download the sample</span></span>

<span data-ttu-id="36ba6-111">For this quickstart, you use the compose file from [Docker](https://docs.docker.com/compose/wordpress/#define-the-project).</span><span class="sxs-lookup"><span data-stu-id="36ba6-111">For this quickstart, you use the compose file from [Docker](https://docs.docker.com/compose/wordpress/#define-the-project).</span></span> <span data-ttu-id="36ba6-112">The configuration file can be found at [Azure Samples](https://github.com/Azure-Samples/multicontainerwordpress).</span><span class="sxs-lookup"><span data-stu-id="36ba6-112">The configuration file can be found at [Azure Samples](https://github.com/Azure-Samples/multicontainerwordpress).</span></span>

[!code-yml[Main](../../../azure-app-service-multi-container/docker-compose-wordpress.yml)]

<span data-ttu-id="36ba6-113">In the Cloud Shell, create a quickstart directory and then change to it.</span><span class="sxs-lookup"><span data-stu-id="36ba6-113">In the Cloud Shell, create a quickstart directory and then change to it.</span></span>

```bash
mkdir quickstart

cd quickstart
```

<span data-ttu-id="36ba6-114">Next, run the following command to clone the sample app repository to your quickstart directory.</span><span class="sxs-lookup"><span data-stu-id="36ba6-114">Next, run the following command to clone the sample app repository to your quickstart directory.</span></span> <span data-ttu-id="36ba6-115">Then change to the `multicontainerwordpress` directory.</span><span class="sxs-lookup"><span data-stu-id="36ba6-115">Then change to the `multicontainerwordpress` directory.</span></span>

```bash
git clone https://github.com/Azure-Samples/multicontainerwordpress

cd multicontainerwordpress
```

## <a name="create-a-resource-group"></a><span data-ttu-id="36ba6-116">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="36ba6-116">Create a resource group</span></span>

[!INCLUDE [resource group intro text](../../../includes/resource-group.md)]

<span data-ttu-id="36ba6-117">In the Cloud Shell, create a resource group with the [`az group create`](/cli/azure/group?view=azure-cli-latest#az-group-create) command.</span><span class="sxs-lookup"><span data-stu-id="36ba6-117">In the Cloud Shell, create a resource group with the [`az group create`](/cli/azure/group?view=azure-cli-latest#az-group-create) command.</span></span> <span data-ttu-id="36ba6-118">The following example creates a resource group named *myResourceGroup* in the *South Central US* location.</span><span class="sxs-lookup"><span data-stu-id="36ba6-118">The following example creates a resource group named *myResourceGroup* in the *South Central US* location.</span></span> <span data-ttu-id="36ba6-119">To see all supported locations for App Service on Linux in **Standard** tier, run the [`az appservice list-locations --sku S1 --linux-workers-enabled`](/cli/azure/appservice?view=azure-cli-latest#az-appservice-list-locations) command.</span><span class="sxs-lookup"><span data-stu-id="36ba6-119">To see all supported locations for App Service on Linux in **Standard** tier, run the [`az appservice list-locations --sku S1 --linux-workers-enabled`](/cli/azure/appservice?view=azure-cli-latest#az-appservice-list-locations) command.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location "South Central US"
```

<span data-ttu-id="36ba6-120">You generally create your resource group and the resources in a region near you.</span><span class="sxs-lookup"><span data-stu-id="36ba6-120">You generally create your resource group and the resources in a region near you.</span></span>

<span data-ttu-id="36ba6-121">When the command finishes, a JSON output shows you the resource group properties.</span><span class="sxs-lookup"><span data-stu-id="36ba6-121">When the command finishes, a JSON output shows you the resource group properties.</span></span>

## <a name="create-an-azure-app-service-plan"></a><span data-ttu-id="36ba6-122">Create an Azure App Service plan</span><span class="sxs-lookup"><span data-stu-id="36ba6-122">Create an Azure App Service plan</span></span>

<span data-ttu-id="36ba6-123">In the Cloud Shell, create an App Service plan in the resource group with the [`az appservice plan create`](/cli/azure/appservice/plan?view=azure-cli-latest#az-appservice-plan-create) command.</span><span class="sxs-lookup"><span data-stu-id="36ba6-123">In the Cloud Shell, create an App Service plan in the resource group with the [`az appservice plan create`](/cli/azure/appservice/plan?view=azure-cli-latest#az-appservice-plan-create) command.</span></span>

<span data-ttu-id="36ba6-124">The following example creates an App Service plan named `myAppServicePlan` in the **Standard** pricing tier (`--sku S1`) and in a Linux container (`--is-linux`).</span><span class="sxs-lookup"><span data-stu-id="36ba6-124">The following example creates an App Service plan named `myAppServicePlan` in the **Standard** pricing tier (`--sku S1`) and in a Linux container (`--is-linux`).</span></span>

```azurecli-interactive
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku S1 --is-linux
```

<span data-ttu-id="36ba6-125">When the App Service plan has been created, the Azure CLI shows information similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="36ba6-125">When the App Service plan has been created, the Azure CLI shows information similar to the following example:</span></span>

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

## <a name="create-a-docker-compose-app"></a><span data-ttu-id="36ba6-126">Create a Docker Compose app</span><span class="sxs-lookup"><span data-stu-id="36ba6-126">Create a Docker Compose app</span></span>

<span data-ttu-id="36ba6-127">In your Cloud Shell terminal, create a multi-container [web app](app-service-linux-intro.md) in the `myAppServicePlan` App Service plan with the [az webapp create](/cli/azure/webapp?view=azure-cli-latest#az-webapp-create) command.</span><span class="sxs-lookup"><span data-stu-id="36ba6-127">In your Cloud Shell terminal, create a multi-container [web app](app-service-linux-intro.md) in the `myAppServicePlan` App Service plan with the [az webapp create](/cli/azure/webapp?view=azure-cli-latest#az-webapp-create) command.</span></span> <span data-ttu-id="36ba6-128">Don't forget to replace _\<app_name>_ with a unique app name.</span><span class="sxs-lookup"><span data-stu-id="36ba6-128">Don't forget to replace _\<app_name>_ with a unique app name.</span></span>

```bash
az webapp create --resource-group myResourceGroup --plan myAppServicePlan --name <app_name> --multicontainer-config-type compose --multicontainer-config-file compose-wordpress.yml
```

<span data-ttu-id="36ba6-129">When the web app has been created, the Azure CLI shows output similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="36ba6-129">When the web app has been created, the Azure CLI shows output similar to the following example:</span></span>

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

### <a name="browse-to-the-app"></a><span data-ttu-id="36ba6-130">Browse to the app</span><span class="sxs-lookup"><span data-stu-id="36ba6-130">Browse to the app</span></span>

<span data-ttu-id="36ba6-131">Browse to the deployed app at (`http://<app_name>.azurewebsites.net`).</span><span class="sxs-lookup"><span data-stu-id="36ba6-131">Browse to the deployed app at (`http://<app_name>.azurewebsites.net`).</span></span> <span data-ttu-id="36ba6-132">The app may take a few minutes to load.</span><span class="sxs-lookup"><span data-stu-id="36ba6-132">The app may take a few minutes to load.</span></span> <span data-ttu-id="36ba6-133">If you receive an error, allow a few more minutes then refresh the browser.</span><span class="sxs-lookup"><span data-stu-id="36ba6-133">If you receive an error, allow a few more minutes then refresh the browser.</span></span>

![Sample multi-container app on Web App for Containers][1]

<span data-ttu-id="36ba6-135">**Congratulations**, you've created a multi-container app in Web App for Containers.</span><span class="sxs-lookup"><span data-stu-id="36ba6-135">**Congratulations**, you've created a multi-container app in Web App for Containers.</span></span>

[!INCLUDE [Clean-up section](../../../includes/cli-script-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="36ba6-136">Next steps</span><span class="sxs-lookup"><span data-stu-id="36ba6-136">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="36ba6-137">Create a multi-container WordPress app in Web App for Containers</span><span class="sxs-lookup"><span data-stu-id="36ba6-137">Create a multi-container WordPress app in Web App for Containers</span></span>](tutorial-multi-container-app.md)

<!--Image references-->
[1]: ./media/tutorial-multi-container-app/azure-multi-container-wordpress-install.png