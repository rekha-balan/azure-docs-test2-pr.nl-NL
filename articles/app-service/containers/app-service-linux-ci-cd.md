---
title: Continuous deployment from a Docker container registry with Web App for Containers - Azure | Microsoft Docs
description: How to set up continuous deployment from a Docker container registry in Web App for Containers.
keywords: azure app service, linux, docker, acr,oss
services: app-service
documentationcenter: ''
author: msangapu
manager: jeconnoc
editor: ''
ms.assetid: a47fb43a-bbbd-4751-bdc1-cd382eae49f8
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2018
ms.author: msangapu
ms.openlocfilehash: 0f2d4626308eed376b71f1b3df2f9e43f1b2a4f7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968343"
---
# <a name="continuous-deployment-with-web-app-for-containers"></a><span data-ttu-id="baa9b-104">Continuous deployment with Web App for Containers</span><span class="sxs-lookup"><span data-stu-id="baa9b-104">Continuous deployment with Web App for Containers</span></span>

<span data-ttu-id="baa9b-105">In this tutorial, you configure continuous deployment for a custom container image from managed [Azure Container Registry](https://azure.microsoft.com/services/container-registry/) repositories or [Docker Hub](https://hub.docker.com).</span><span class="sxs-lookup"><span data-stu-id="baa9b-105">In this tutorial, you configure continuous deployment for a custom container image from managed [Azure Container Registry](https://azure.microsoft.com/services/container-registry/) repositories or [Docker Hub](https://hub.docker.com).</span></span>

## <a name="sign-in-to-azure"></a><span data-ttu-id="baa9b-106">Sign in to Azure</span><span class="sxs-lookup"><span data-stu-id="baa9b-106">Sign in to Azure</span></span>

<span data-ttu-id="baa9b-107">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="baa9b-107">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

## <a name="enable-the-continuous-deployment-feature"></a><span data-ttu-id="baa9b-108">Enable the continuous deployment feature</span><span class="sxs-lookup"><span data-stu-id="baa9b-108">Enable the continuous deployment feature</span></span>

<span data-ttu-id="baa9b-109">Enable the continuous deployment feature by using [Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli) and executing the following command:</span><span class="sxs-lookup"><span data-stu-id="baa9b-109">Enable the continuous deployment feature by using [Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli) and executing the following command:</span></span>

```azurecli-interactive
az webapp deployment container config --name name --resource-group myResourceGroup --enable-cd true
```

<span data-ttu-id="baa9b-110">In the [Azure portal](https://portal.azure.com/), select the **App Service** option on the left side of the page.</span><span class="sxs-lookup"><span data-stu-id="baa9b-110">In the [Azure portal](https://portal.azure.com/), select the **App Service** option on the left side of the page.</span></span>

<span data-ttu-id="baa9b-111">Select the name of the app for which you want to configure Docker Hub continuous deployment.</span><span class="sxs-lookup"><span data-stu-id="baa9b-111">Select the name of the app for which you want to configure Docker Hub continuous deployment.</span></span>

<span data-ttu-id="baa9b-112">On the **Docker Container** page, select **On**, and then select **Save** to enable continuous deployment.</span><span class="sxs-lookup"><span data-stu-id="baa9b-112">On the **Docker Container** page, select **On**, and then select **Save** to enable continuous deployment.</span></span>

![Screenshot of app setting](./media/app-service-webapp-service-linux-ci-cd/step2.png)

## <a name="prepare-the-webhook-url"></a><span data-ttu-id="baa9b-114">Prepare the webhook URL</span><span class="sxs-lookup"><span data-stu-id="baa9b-114">Prepare the webhook URL</span></span>

<span data-ttu-id="baa9b-115">Obtain the webhook URL by using [Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli) and executing the following command:</span><span class="sxs-lookup"><span data-stu-id="baa9b-115">Obtain the webhook URL by using [Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli) and executing the following command:</span></span>

```azurecli-interactive
az webapp deployment container show-cd-url --name sname1 --resource-group rgname
```

<span data-ttu-id="baa9b-116">Make a note of the webhook URL.</span><span class="sxs-lookup"><span data-stu-id="baa9b-116">Make a note of the webhook URL.</span></span> <span data-ttu-id="baa9b-117">You'll need it in the next section.</span><span class="sxs-lookup"><span data-stu-id="baa9b-117">You'll need it in the next section.</span></span>
<span data-ttu-id="baa9b-118">`https://<publishingusername>:<publishingpwd>@<sitename>.scm.azurewebsites.net/docker/hook`.</span><span class="sxs-lookup"><span data-stu-id="baa9b-118">`https://<publishingusername>:<publishingpwd>@<sitename>.scm.azurewebsites.net/docker/hook`.</span></span>

<span data-ttu-id="baa9b-119">You can obtain your `publishingusername` and `publishingpwd` by downloading the web app publish profile using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="baa9b-119">You can obtain your `publishingusername` and `publishingpwd` by downloading the web app publish profile using the Azure portal.</span></span>

![Screenshot of adding webhook 2](./media/app-service-webapp-service-linux-ci-cd/step3-3.png)

## <a name="add-a-webhook"></a><span data-ttu-id="baa9b-121">Add a webhook</span><span class="sxs-lookup"><span data-stu-id="baa9b-121">Add a webhook</span></span>

<span data-ttu-id="baa9b-122">To add a webhook, follow the steps in these guides:</span><span class="sxs-lookup"><span data-stu-id="baa9b-122">To add a webhook, follow the steps in these guides:</span></span>

- <span data-ttu-id="baa9b-123">[Azure Container Registry](../../container-registry/container-registry-webhook.md) using the webhook URL</span><span class="sxs-lookup"><span data-stu-id="baa9b-123">[Azure Container Registry](../../container-registry/container-registry-webhook.md) using the webhook URL</span></span>
- [<span data-ttu-id="baa9b-124">Webhooks for Docker Hub</span><span class="sxs-lookup"><span data-stu-id="baa9b-124">Webhooks for Docker Hub</span></span>](https://docs.docker.com/docker-hub/webhooks/)

## <a name="next-steps"></a><span data-ttu-id="baa9b-125">Next steps</span><span class="sxs-lookup"><span data-stu-id="baa9b-125">Next steps</span></span>

* [<span data-ttu-id="baa9b-126">Introduction to Azure App Service on Linux</span><span class="sxs-lookup"><span data-stu-id="baa9b-126">Introduction to Azure App Service on Linux</span></span>](./app-service-linux-intro.md)
* [<span data-ttu-id="baa9b-127">Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="baa9b-127">Azure Container Registry</span></span>](https://azure.microsoft.com/services/container-registry/)
* [<span data-ttu-id="baa9b-128">Create a .NET Core web app in App Service on Linux</span><span class="sxs-lookup"><span data-stu-id="baa9b-128">Create a .NET Core web app in App Service on Linux</span></span>](quickstart-dotnetcore.md)
* [<span data-ttu-id="baa9b-129">Create a Ruby web app in App Service on Linux</span><span class="sxs-lookup"><span data-stu-id="baa9b-129">Create a Ruby web app in App Service on Linux</span></span>](quickstart-ruby.md)
* [<span data-ttu-id="baa9b-130">Deploy a Docker/Go web app in Web App for Containers</span><span class="sxs-lookup"><span data-stu-id="baa9b-130">Deploy a Docker/Go web app in Web App for Containers</span></span>](quickstart-docker-go.md)
* [<span data-ttu-id="baa9b-131">Azure App Service on Linux FAQ</span><span class="sxs-lookup"><span data-stu-id="baa9b-131">Azure App Service on Linux FAQ</span></span>](./app-service-linux-faq.md)
* [<span data-ttu-id="baa9b-132">Manage Web App for Containers using Azure CLI</span><span class="sxs-lookup"><span data-stu-id="baa9b-132">Manage Web App for Containers using Azure CLI</span></span>](./app-service-linux-cli.md)
