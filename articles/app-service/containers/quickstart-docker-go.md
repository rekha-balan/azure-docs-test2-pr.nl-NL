---
title: Deploy a Docker/Go app in Azure Web App for Containers
description: How to deploy a Docker image running a Go application to Web App for Containers.
keywords: azure app service, web app, go, docker, container
services: app-service
author: msangapu
manager: cfowler
ms.assetid: b97bd4e6-dff0-4976-ac20-d5c109a559a8
ms.service: app-service
ms.devlang: go
ms.topic: quickstart
ms.date: 01/17/2018
ms.author: msangapu
ms.custom: mvc
ms.openlocfilehash: f1d58adcc017367a3de8ee6130a3333f86fb501c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869216"
---
# <a name="deploy-a-dockergo-web-app-in-web-app-for-containers"></a><span data-ttu-id="a911c-104">Deploy a Docker/Go web app in Web App for Containers</span><span class="sxs-lookup"><span data-stu-id="a911c-104">Deploy a Docker/Go web app in Web App for Containers</span></span>

<span data-ttu-id="a911c-105">[App Service Linux](app-service-linux-intro.md) provides pre-defined application stacks on Linux with support for languages such as .NET, PHP, Node.js and others.</span><span class="sxs-lookup"><span data-stu-id="a911c-105">[App Service Linux](app-service-linux-intro.md) provides pre-defined application stacks on Linux with support for languages such as .NET, PHP, Node.js and others.</span></span> <span data-ttu-id="a911c-106">You can also use a custom Docker image to run your web app on an application stack that is not already defined in Azure.</span><span class="sxs-lookup"><span data-stu-id="a911c-106">You can also use a custom Docker image to run your web app on an application stack that is not already defined in Azure.</span></span> <span data-ttu-id="a911c-107">This quickstart shows how to create a web app and deploy a Go image from Docker Hub.</span><span class="sxs-lookup"><span data-stu-id="a911c-107">This quickstart shows how to create a web app and deploy a Go image from Docker Hub.</span></span> <span data-ttu-id="a911c-108">You create the web app using the [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="a911c-108">You create the web app using the [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli).</span></span>

![Sample app running in Azure](media/quickstart-docker-go/hello-world-in-browser.png)

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

[!INCLUDE [Configure deployment user](../../../includes/configure-deployment-user.md)]

[!INCLUDE [Create resource group](../../../includes/app-service-web-create-resource-group-linux.md)]

[!INCLUDE [Create app service plan](../../../includes/app-service-web-create-app-service-plan-linux.md)]

## <a name="create-a-web-app"></a><span data-ttu-id="a911c-110">Create a web app</span><span class="sxs-lookup"><span data-stu-id="a911c-110">Create a web app</span></span>

<span data-ttu-id="a911c-111">Create a [web app](../app-service-web-overview.md) in the `myAppServicePlan` App Service plan with the [az webapp create](/cli/azure/webapp?view=azure-cli-latest#az-webapp-create) command.</span><span class="sxs-lookup"><span data-stu-id="a911c-111">Create a [web app](../app-service-web-overview.md) in the `myAppServicePlan` App Service plan with the [az webapp create](/cli/azure/webapp?view=azure-cli-latest#az-webapp-create) command.</span></span> <span data-ttu-id="a911c-112">Don't forget to replace `<app name>` with a globally unique app name.</span><span class="sxs-lookup"><span data-stu-id="a911c-112">Don't forget to replace `<app name>` with a globally unique app name.</span></span>

```azurecli-interactive
az webapp create --resource-group myResourceGroup --plan myAppServicePlan --name <app name> --deployment-container-image-name microsoft/azure-appservices-go-quickstart
```

<span data-ttu-id="a911c-113">In the preceding command, `--deployment-container-image-name` points to the public Docker Hub image [microsoft/azure-appservices-go-quickstart](https://hub.docker.com/r/microsoft/azure-appservices-go-quickstart/).</span><span class="sxs-lookup"><span data-stu-id="a911c-113">In the preceding command, `--deployment-container-image-name` points to the public Docker Hub image [microsoft/azure-appservices-go-quickstart](https://hub.docker.com/r/microsoft/azure-appservices-go-quickstart/).</span></span>

<span data-ttu-id="a911c-114">When the web app has been created, the Azure CLI shows output similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="a911c-114">When the web app has been created, the Azure CLI shows output similar to the following example:</span></span>

```json
{
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
  "cloningInfo": null,
  "containerSize": 0,
  "dailyMemoryTimeQuota": 0,
  "defaultHostName": "<app name>.azurewebsites.net",
  "deploymentLocalGitUrl": "https://<username>@<app name>.scm.azurewebsites.net/<app name>.git",
  "enabled": true,
  < JSON data removed for brevity. >
}
```

## <a name="browse-to-the-app"></a><span data-ttu-id="a911c-115">Browse to the app</span><span class="sxs-lookup"><span data-stu-id="a911c-115">Browse to the app</span></span>

```bash
http://<app_name>.azurewebsites.net/hello
```

![Sample app running in Azure](media/quickstart-docker-go/hello-world-in-browser.png)

<span data-ttu-id="a911c-117">**Congratulations!**</span><span class="sxs-lookup"><span data-stu-id="a911c-117">**Congratulations!**</span></span> <span data-ttu-id="a911c-118">You've deployed a custom Docker image running a Go application to Web App for Containers.</span><span class="sxs-lookup"><span data-stu-id="a911c-118">You've deployed a custom Docker image running a Go application to Web App for Containers.</span></span>

[!INCLUDE [Clean-up section](../../../includes/cli-script-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="a911c-119">Next steps</span><span class="sxs-lookup"><span data-stu-id="a911c-119">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a911c-120">Use a custom Docker image</span><span class="sxs-lookup"><span data-stu-id="a911c-120">Use a custom Docker image</span></span>](tutorial-custom-docker-image.md)
