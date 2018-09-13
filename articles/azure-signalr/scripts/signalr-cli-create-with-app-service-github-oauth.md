---
title: Azure CLI Script Sample - Create a web app that uses SignalR Service and GitHub authentication | Microsoft Docs
description: Azure CLI Script Sample - Create a web app that uses SignalR Service and GitHub authentication
services: signalr
documentationcenter: signalr
author: sffamily
manager: cfowler
editor: ''
tags: azure-service-management
ms.service: signalr
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: signalr
ms.date: 04/22/2018
ms.author: zhshang
ms.custom: mvc
ms.openlocfilehash: 94203153b7f9a2fecb664a12ff90548787a4f158
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869011"
---
# <a name="create-a-web-app-that-uses-signalr-service-and-github-authentication"></a><span data-ttu-id="977fe-103">Create a web app that uses SignalR Service and GitHub authentication</span><span class="sxs-lookup"><span data-stu-id="977fe-103">Create a web app that uses SignalR Service and GitHub authentication</span></span>

<span data-ttu-id="977fe-104">This sample script creates a new Azure SignalR Service resource, which is used to push real-time content updates to clients.</span><span class="sxs-lookup"><span data-stu-id="977fe-104">This sample script creates a new Azure SignalR Service resource, which is used to push real-time content updates to clients.</span></span> <span data-ttu-id="977fe-105">This script also adds a new Web App and App Service plan to host your ASP.NET Core Web App that uses the SignalR Service.</span><span class="sxs-lookup"><span data-stu-id="977fe-105">This script also adds a new Web App and App Service plan to host your ASP.NET Core Web App that uses the SignalR Service.</span></span> <span data-ttu-id="977fe-106">The web app is configured with app settings to connect to the new SignalR service resource, and authenticate with [GitHub authentication](https://developer.github.com/v3/guides/basics-of-authentication/).</span><span class="sxs-lookup"><span data-stu-id="977fe-106">The web app is configured with app settings to connect to the new SignalR service resource, and authenticate with [GitHub authentication](https://developer.github.com/v3/guides/basics-of-authentication/).</span></span> <span data-ttu-id="977fe-107">The web app is also configured to use a local git repository deployment source.</span><span class="sxs-lookup"><span data-stu-id="977fe-107">The web app is also configured to use a local git repository deployment source.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="977fe-108">If you choose to install and use the CLI locally, this article requires that you are running the Azure CLI version 2.0 or later.</span><span class="sxs-lookup"><span data-stu-id="977fe-108">If you choose to install and use the CLI locally, this article requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="977fe-109">Run `az --version` to find the version.</span><span class="sxs-lookup"><span data-stu-id="977fe-109">Run `az --version` to find the version.</span></span> <span data-ttu-id="977fe-110">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="977fe-110">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="977fe-111">Sample script</span><span class="sxs-lookup"><span data-stu-id="977fe-111">Sample script</span></span>

<span data-ttu-id="977fe-112">This script uses the *signalr* extension for the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="977fe-112">This script uses the *signalr* extension for the Azure CLI.</span></span> <span data-ttu-id="977fe-113">Execute the following command to install the *signalr* extension for the Azure CLI before using this sample script:</span><span class="sxs-lookup"><span data-stu-id="977fe-113">Execute the following command to install the *signalr* extension for the Azure CLI before using this sample script:</span></span>

```azurecli-interactive
az extension add -n signalr
```

[!code-azurecli-interactive[main](../../../cli_scripts/azure-signalr/create-signalr-with-app-service-github-oauth/create-signalr-with-app-service-github-oauth.sh "Create a new SignalR Service and Web App configured to use SignalR, GitHub OAuth, and local Git repository deployment source.")]

<span data-ttu-id="977fe-114">Make a note of the actual name generated for the new resource group.</span><span class="sxs-lookup"><span data-stu-id="977fe-114">Make a note of the actual name generated for the new resource group.</span></span> <span data-ttu-id="977fe-115">It will be shown in the output.</span><span class="sxs-lookup"><span data-stu-id="977fe-115">It will be shown in the output.</span></span> <span data-ttu-id="977fe-116">You will use that resource group name when you want to delete all group resources.</span><span class="sxs-lookup"><span data-stu-id="977fe-116">You will use that resource group name when you want to delete all group resources.</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="977fe-117">Script explanation</span><span class="sxs-lookup"><span data-stu-id="977fe-117">Script explanation</span></span>

<span data-ttu-id="977fe-118">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="977fe-118">Each command in the table links to command specific documentation.</span></span> <span data-ttu-id="977fe-119">This script uses the following commands:</span><span class="sxs-lookup"><span data-stu-id="977fe-119">This script uses the following commands:</span></span>

| <span data-ttu-id="977fe-120">Command</span><span class="sxs-lookup"><span data-stu-id="977fe-120">Command</span></span> | <span data-ttu-id="977fe-121">Notes</span><span class="sxs-lookup"><span data-stu-id="977fe-121">Notes</span></span> |
|---|---|
| [<span data-ttu-id="977fe-122">az group create</span><span class="sxs-lookup"><span data-stu-id="977fe-122">az group create</span></span>](/cli/azure/group#az-group-create) | <span data-ttu-id="977fe-123">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="977fe-123">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="977fe-124">az signalr create</span><span class="sxs-lookup"><span data-stu-id="977fe-124">az signalr create</span></span>](/cli/azure/ext/signalr/signalr#ext-signalr-az-signalr-create) | <span data-ttu-id="977fe-125">Creates an Azure SignalR Service resource.</span><span class="sxs-lookup"><span data-stu-id="977fe-125">Creates an Azure SignalR Service resource.</span></span> |
| [<span data-ttu-id="977fe-126">az signalr key list</span><span class="sxs-lookup"><span data-stu-id="977fe-126">az signalr key list</span></span>](/cli/azure/ext/signalr/signalr/key#ext-signalr-az-signalr-key-list) | <span data-ttu-id="977fe-127">List the keys, which will be used by your application when pushing real-time content updates with SignalR.</span><span class="sxs-lookup"><span data-stu-id="977fe-127">List the keys, which will be used by your application when pushing real-time content updates with SignalR.</span></span> |
| [<span data-ttu-id="977fe-128">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="977fe-128">az appservice plan create</span></span>](/cli/azure/appservice/plan#az-appservice-plan-create) | <span data-ttu-id="977fe-129">Creates an Azure App Service Plan for hosting web apps.</span><span class="sxs-lookup"><span data-stu-id="977fe-129">Creates an Azure App Service Plan for hosting web apps.</span></span> |
| [<span data-ttu-id="977fe-130">az webapp create</span><span class="sxs-lookup"><span data-stu-id="977fe-130">az webapp create</span></span>](/cli/azure/webapp#az-webapp-create) | <span data-ttu-id="977fe-131">Creates an Azure Web app using the App Service hosting plan.</span><span class="sxs-lookup"><span data-stu-id="977fe-131">Creates an Azure Web app using the App Service hosting plan.</span></span> |
| [<span data-ttu-id="977fe-132">az webapp config appsettings set</span><span class="sxs-lookup"><span data-stu-id="977fe-132">az webapp config appsettings set</span></span>](/cli/azure/webapp/config/appsettings#az-webapp-config-appsettings-set) | <span data-ttu-id="977fe-133">Adds new app settings for the web app.</span><span class="sxs-lookup"><span data-stu-id="977fe-133">Adds new app settings for the web app.</span></span> <span data-ttu-id="977fe-134">These app settings are used to store the SignalR connection string and GitHub OAuth app secrets.</span><span class="sxs-lookup"><span data-stu-id="977fe-134">These app settings are used to store the SignalR connection string and GitHub OAuth app secrets.</span></span> |
| [<span data-ttu-id="977fe-135">az webapp deployment user set</span><span class="sxs-lookup"><span data-stu-id="977fe-135">az webapp deployment user set</span></span>](/cli/azure/webapp/deployment/user#az-webapp-deployment-user-set) | <span data-ttu-id="977fe-136">Update deployment credentials.</span><span class="sxs-lookup"><span data-stu-id="977fe-136">Update deployment credentials.</span></span> |
| [<span data-ttu-id="977fe-137">az webapp deployment source config-local-git</span><span class="sxs-lookup"><span data-stu-id="977fe-137">az webapp deployment source config-local-git</span></span>](/cli/azure/webapp/deployment/source#az-webapp-deployment-source-config-local-git) | <span data-ttu-id="977fe-138">Get a URL for a git repository endpoint to clone and push to for web app deployment.</span><span class="sxs-lookup"><span data-stu-id="977fe-138">Get a URL for a git repository endpoint to clone and push to for web app deployment.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="977fe-139">Next steps</span><span class="sxs-lookup"><span data-stu-id="977fe-139">Next steps</span></span>

<span data-ttu-id="977fe-140">For more information on the Azure CLI, see [Azure CLI documentation](/cli/azure).</span><span class="sxs-lookup"><span data-stu-id="977fe-140">For more information on the Azure CLI, see [Azure CLI documentation](/cli/azure).</span></span>

<span data-ttu-id="977fe-141">Additional Azure SignalR Service CLI script samples can be found in the [Azure SignalR Service documentation](../signalr-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="977fe-141">Additional Azure SignalR Service CLI script samples can be found in the [Azure SignalR Service documentation](../signalr-cli-samples.md).</span></span>
