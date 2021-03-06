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
# <a name="create-a-multi-container-preview-app-using-web-app-for-containers"></a>Create a multi-container (preview) app using Web App for Containers

[Web App for Containers](app-service-linux-intro.md) provides a flexible way to use Docker images. This quickstart shows how to deploy a multi-container app to Web App for Containers in the [Cloud Shell](https://docs.microsoft.com/en-us/azure/cloud-shell/overview) using a Docker Compose configuration. For Kubernetes and a full end-to-end solution using Azure DB for MySQL, follow the [multi-container tutorial](tutorial-multi-container-app.md).

You'll complete this quickstart in Cloud Shell, but you can also run these commands locally with [Azure CLI](/cli/azure/install-azure-cli) (2.0.32 or later). 

![Sample multi-container app on Web App for Containers][1]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="download-the-sample"></a>Download the sample

For this quickstart, you use the compose file from [Docker](https://docs.docker.com/compose/wordpress/#define-the-project). The configuration file can be found at [Azure Samples](https://github.com/Azure-Samples/multicontainerwordpress).

[!code-yml[Main](../../../azure-app-service-multi-container/docker-compose-wordpress.yml)]

In the Cloud Shell, create a quickstart directory and then change to it.

```bash
mkdir quickstart

cd quickstart
```

Next, run the following command to clone the sample app repository to your quickstart directory. Then change to the `multicontainerwordpress` directory.

```bash
git clone https://github.com/Azure-Samples/multicontainerwordpress

cd multicontainerwordpress
```

## <a name="create-a-resource-group"></a>Create a resource group

[!INCLUDE [resource group intro text](../../../includes/resource-group.md)]

In the Cloud Shell, create a resource group with the [`az group create`](/cli/azure/group?view=azure-cli-latest#az-group-create) command. The following example creates a resource group named *myResourceGroup* in the *South Central US* location. To see all supported locations for App Service on Linux in **Standard** tier, run the [`az appservice list-locations --sku S1 --linux-workers-enabled`](/cli/azure/appservice?view=azure-cli-latest#az-appservice-list-locations) command.

```azurecli-interactive
az group create --name myResourceGroup --location "South Central US"
```

You generally create your resource group and the resources in a region near you.

When the command finishes, a JSON output shows you the resource group properties.

## <a name="create-an-azure-app-service-plan"></a>Create an Azure App Service plan

In the Cloud Shell, create an App Service plan in the resource group with the [`az appservice plan create`](/cli/azure/appservice/plan?view=azure-cli-latest#az-appservice-plan-create) command.

The following example creates an App Service plan named `myAppServicePlan` in the **Standard** pricing tier (`--sku S1`) and in a Linux container (`--is-linux`).

```azurecli-interactive
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku S1 --is-linux
```

When the App Service plan has been created, the Azure CLI shows information similar to the following example:

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

## <a name="create-a-docker-compose-app"></a>Create a Docker Compose app

In your Cloud Shell terminal, create a multi-container [web app](app-service-linux-intro.md) in the `myAppServicePlan` App Service plan with the [az webapp create](/cli/azure/webapp?view=azure-cli-latest#az-webapp-create) command. Don't forget to replace _\<app_name>_ with a unique app name.

```bash
az webapp create --resource-group myResourceGroup --plan myAppServicePlan --name <app_name> --multicontainer-config-type compose --multicontainer-config-file compose-wordpress.yml
```

When the web app has been created, the Azure CLI shows output similar to the following example:

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

### <a name="browse-to-the-app"></a>Browse to the app

Browse to the deployed app at (`http://<app_name>.azurewebsites.net`). The app may take a few minutes to load. If you receive an error, allow a few more minutes then refresh the browser.

![Sample multi-container app on Web App for Containers][1]

**Congratulations**, you've created a multi-container app in Web App for Containers.

[!INCLUDE [Clean-up section](../../../includes/cli-script-clean-up.md)]

## <a name="next-steps"></a>Next steps

> [!div class="nextstepaction"]
> [Create a multi-container WordPress app in Web App for Containers](tutorial-multi-container-app.md)

<!--Image references-->
[1]: ./media/tutorial-multi-container-app/azure-multi-container-wordpress-install.png