---
title: Manage Web App for Containers using Azure CLI 2.0 | Microsoft Docs
description: Manage Web App for Containers using Azure CLI.
keywords: azure app service, web app, cli, linux, oss
services: app-service
documentationCenter: ''
author: ahmedelnably
manager: cfowler
editor: ''
ms.assetid: ''
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: aelnably
ms.openlocfilehash: 54c979313a6ffa43008aa9870332b92d2b2f182a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865429"
---
# <a name="manage-web-app-for-containers-using-azure-cli"></a><span data-ttu-id="1eb9a-104">Manage Web App for Containers using Azure CLI</span><span class="sxs-lookup"><span data-stu-id="1eb9a-104">Manage Web App for Containers using Azure CLI</span></span>

<span data-ttu-id="1eb9a-105">Using the commands in this article you are able to create and manage a Web App for Containers using Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="1eb9a-105">Using the commands in this article you are able to create and manage a Web App for Containers using Azure CLI 2.0.</span></span>
<span data-ttu-id="1eb9a-106">You can start using the new version of the CLI in two ways:</span><span class="sxs-lookup"><span data-stu-id="1eb9a-106">You can start using the new version of the CLI in two ways:</span></span>

* <span data-ttu-id="1eb9a-107">[Installing Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) on your machine.</span><span class="sxs-lookup"><span data-stu-id="1eb9a-107">[Installing Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) on your machine.</span></span>
* <span data-ttu-id="1eb9a-108">Using [Azure Cloud Shell (Preview)](../../cloud-shell/overview.md)</span><span class="sxs-lookup"><span data-stu-id="1eb9a-108">Using [Azure Cloud Shell (Preview)](../../cloud-shell/overview.md)</span></span>

## <a name="create-a-linux-app-service-plan"></a><span data-ttu-id="1eb9a-109">Create a Linux App Service Plan</span><span class="sxs-lookup"><span data-stu-id="1eb9a-109">Create a Linux App Service Plan</span></span>

<span data-ttu-id="1eb9a-110">To create a Linux App Service Plan, you can use the following command:</span><span class="sxs-lookup"><span data-stu-id="1eb9a-110">To create a Linux App Service Plan, you can use the following command:</span></span>

```azurecli-interactive
az appservice plan create -n appname -g rgname --is-linux -l "South Central US" --sku S1 --number-of-workers 1
```

## <a name="create-a-custom-docker-container-web-app"></a><span data-ttu-id="1eb9a-111">Create a custom Docker container Web App</span><span class="sxs-lookup"><span data-stu-id="1eb9a-111">Create a custom Docker container Web App</span></span>

<span data-ttu-id="1eb9a-112">To create a web app and configuring it to run a custom Docker container, you can use the following command:</span><span class="sxs-lookup"><span data-stu-id="1eb9a-112">To create a web app and configuring it to run a custom Docker container, you can use the following command:</span></span>

```azurecli-interactive
az webapp create -n sname -g rgname -p pname -i elnably/dockerimagetest
```

## <a name="activate-the-docker-container-logging"></a><span data-ttu-id="1eb9a-113">Activate the Docker container logging</span><span class="sxs-lookup"><span data-stu-id="1eb9a-113">Activate the Docker container logging</span></span>

<span data-ttu-id="1eb9a-114">To activate the Docker container logging, you can use the following command:</span><span class="sxs-lookup"><span data-stu-id="1eb9a-114">To activate the Docker container logging, you can use the following command:</span></span>

```azurecli-interactive
az webapp log config -n sname -g rgname --web-server-logging filesystem
```

## <a name="change-the-custom-docker-container-for-an-existing-web-app-for-containers-app"></a><span data-ttu-id="1eb9a-115">Change the custom Docker container for an existing Web App for Containers App</span><span class="sxs-lookup"><span data-stu-id="1eb9a-115">Change the custom Docker container for an existing Web App for Containers App</span></span>

<span data-ttu-id="1eb9a-116">To change a previously created app, from the current Docker image to a new image, you can use the following command:</span><span class="sxs-lookup"><span data-stu-id="1eb9a-116">To change a previously created app, from the current Docker image to a new image, you can use the following command:</span></span>

```azurecli-interactive
az webapp config container set -n sname -g rgname -c apurvajo/mariohtml5
```

## <a name="using-docker-images-from-a-private-registry"></a><span data-ttu-id="1eb9a-117">Using Docker images from a private registry</span><span class="sxs-lookup"><span data-stu-id="1eb9a-117">Using Docker images from a private registry</span></span>

<span data-ttu-id="1eb9a-118">You can configure your app to use images from a private registry.</span><span class="sxs-lookup"><span data-stu-id="1eb9a-118">You can configure your app to use images from a private registry.</span></span> <span data-ttu-id="1eb9a-119">You need to provide the url for your registry, user name, and password.</span><span class="sxs-lookup"><span data-stu-id="1eb9a-119">You need to provide the url for your registry, user name, and password.</span></span> <span data-ttu-id="1eb9a-120">This can be achieved using the following command:</span><span class="sxs-lookup"><span data-stu-id="1eb9a-120">This can be achieved using the following command:</span></span>

```azurecli-interactive
az webapp config container set -n sname1 -g rgname -c <container name> -r <server url> -u <username> -p <password>
```

## <a name="enable-continuous-deployments-for-custom-docker-images"></a><span data-ttu-id="1eb9a-121">Enable continuous deployments for custom Docker images</span><span class="sxs-lookup"><span data-stu-id="1eb9a-121">Enable continuous deployments for custom Docker images</span></span>

<span data-ttu-id="1eb9a-122">With the following command you can enable the CD functionality, and get the webhook url.</span><span class="sxs-lookup"><span data-stu-id="1eb9a-122">With the following command you can enable the CD functionality, and get the webhook url.</span></span> <span data-ttu-id="1eb9a-123">This url can be used to configure you DockerHub or Azure Container Registry repos.</span><span class="sxs-lookup"><span data-stu-id="1eb9a-123">This url can be used to configure you DockerHub or Azure Container Registry repos.</span></span>

```azurecli-interactive
az webapp deployment container config -n sname -g rgname -e true
```

## <a name="create-a-web-app-for-containers-app-using-one-of-our-built-in-runtime-frameworks"></a><span data-ttu-id="1eb9a-124">Create a Web App for Containers App using one of our built-in runtime frameworks</span><span class="sxs-lookup"><span data-stu-id="1eb9a-124">Create a Web App for Containers App using one of our built-in runtime frameworks</span></span>

<span data-ttu-id="1eb9a-125">To create a PHP 5.6 Web App for Containers App that, you can use the following command.</span><span class="sxs-lookup"><span data-stu-id="1eb9a-125">To create a PHP 5.6 Web App for Containers App that, you can use the following command.</span></span>

```azurecli-interactive
az webapp create -n sname -g rgname -p pname -r "php|5.6"
```

## <a name="change-framework-version-for-an-existing-web-app-for-containers-app"></a><span data-ttu-id="1eb9a-126">Change framework version for an existing Web App for Containers App</span><span class="sxs-lookup"><span data-stu-id="1eb9a-126">Change framework version for an existing Web App for Containers App</span></span>

<span data-ttu-id="1eb9a-127">To change a previously created app, from the current framework version to Node.js 6.11, you can use the following command:</span><span class="sxs-lookup"><span data-stu-id="1eb9a-127">To change a previously created app, from the current framework version to Node.js 6.11, you can use the following command:</span></span>

```azurecli-interactive
az webapp config set -n sname -g rgname --linux-fx-version "node|6.11"
```

## <a name="set-up-git-deployments-for-your-web-app"></a><span data-ttu-id="1eb9a-128">Set up Git deployments for your Web App</span><span class="sxs-lookup"><span data-stu-id="1eb9a-128">Set up Git deployments for your Web App</span></span>

<span data-ttu-id="1eb9a-129">To set up Git deployments for your app, you can use the following command:</span><span class="sxs-lookup"><span data-stu-id="1eb9a-129">To set up Git deployments for your app, you can use the following command:</span></span>

```azurecli-interactive
az webapp deployment source config -n sname -g rgname --repo-url <gitrepo url> --branch <branch>
```

## <a name="next-steps"></a><span data-ttu-id="1eb9a-130">Next steps</span><span class="sxs-lookup"><span data-stu-id="1eb9a-130">Next steps</span></span>

* [<span data-ttu-id="1eb9a-131">What is Azure App Service on Linux?</span><span class="sxs-lookup"><span data-stu-id="1eb9a-131">What is Azure App Service on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="1eb9a-132">Install Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="1eb9a-132">Install Azure CLI 2.0</span></span>](https://docs.microsoft.com/cli/azure/install-azure-cli)
* [<span data-ttu-id="1eb9a-133">Azure Cloud Shell (Preview)</span><span class="sxs-lookup"><span data-stu-id="1eb9a-133">Azure Cloud Shell (Preview)</span></span>](../../cloud-shell/overview.md)
* [<span data-ttu-id="1eb9a-134">Set up staging environments in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="1eb9a-134">Set up staging environments in Azure App Service</span></span>](../../app-service/web-sites-staged-publishing.md?toc=%2fazure%2fapp-service%2fcontainers%2ftoc.json)
* [<span data-ttu-id="1eb9a-135">Continuous Deployment with Web App for Containers</span><span class="sxs-lookup"><span data-stu-id="1eb9a-135">Continuous Deployment with Web App for Containers</span></span>](app-service-linux-ci-cd.md)
