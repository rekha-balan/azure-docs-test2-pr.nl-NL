---
title: Azure CLI Script Sample - Create a SignalR Service with an App Service | Microsoft Docs
description: Azure CLI Script Sample - Create SignalR Service with an App Service
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
ms.date: 04/20/2018
ms.author: zhshang
ms.custom: mvc
ms.openlocfilehash: 70b81eada9c71594b3c5223b825f0a6db8ed7ef1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856046"
---
# <a name="create-a-signalr-service-with-an-app-service"></a><span data-ttu-id="c350c-103">Create a SignalR Service with an App Service</span><span class="sxs-lookup"><span data-stu-id="c350c-103">Create a SignalR Service with an App Service</span></span>

<span data-ttu-id="c350c-104">This sample script creates a new Azure SignalR Service resource, which is used to push real-time content updates to clients.</span><span class="sxs-lookup"><span data-stu-id="c350c-104">This sample script creates a new Azure SignalR Service resource, which is used to push real-time content updates to clients.</span></span> <span data-ttu-id="c350c-105">This script also adds a new Web App and App Service plan to host your ASP.NET Core Web App that uses the SignalR Service.</span><span class="sxs-lookup"><span data-stu-id="c350c-105">This script also adds a new Web App and App Service plan to host your ASP.NET Core Web App that uses the SignalR Service.</span></span> <span data-ttu-id="c350c-106">The web app is configured with an App Setting named *AzureSignalRConnectionString* to connect to the new SignalR service resource.</span><span class="sxs-lookup"><span data-stu-id="c350c-106">The web app is configured with an App Setting named *AzureSignalRConnectionString* to connect to the new SignalR service resource.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="c350c-107">If you choose to install and use the CLI locally, this article requires that you are running the Azure CLI version 2.0 or later.</span><span class="sxs-lookup"><span data-stu-id="c350c-107">If you choose to install and use the CLI locally, this article requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="c350c-108">Run `az --version` to find the version.</span><span class="sxs-lookup"><span data-stu-id="c350c-108">Run `az --version` to find the version.</span></span> <span data-ttu-id="c350c-109">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="c350c-109">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="c350c-110">Sample script</span><span class="sxs-lookup"><span data-stu-id="c350c-110">Sample script</span></span>

<span data-ttu-id="c350c-111">This script uses the *signalr* extension for the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="c350c-111">This script uses the *signalr* extension for the Azure CLI.</span></span> <span data-ttu-id="c350c-112">Execute the following command to install the *signalr* extension for the Azure CLI before using this sample script:</span><span class="sxs-lookup"><span data-stu-id="c350c-112">Execute the following command to install the *signalr* extension for the Azure CLI before using this sample script:</span></span>

```azurecli-interactive
az extension add -n signalr
```

[!code-azurecli-interactive[main](../../../cli_scripts/azure-signalr/create-signalr-with-app-service/create-signalr-with-app-service.sh "Create a new Azure SignalR Service and Web App")]

<span data-ttu-id="c350c-113">Make a note of the actual name generated for the new resource group.</span><span class="sxs-lookup"><span data-stu-id="c350c-113">Make a note of the actual name generated for the new resource group.</span></span> <span data-ttu-id="c350c-114">It will be shown in the output.</span><span class="sxs-lookup"><span data-stu-id="c350c-114">It will be shown in the output.</span></span> <span data-ttu-id="c350c-115">You will use that resource group name when you want to delete all group resources.</span><span class="sxs-lookup"><span data-stu-id="c350c-115">You will use that resource group name when you want to delete all group resources.</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="c350c-116">Script explanation</span><span class="sxs-lookup"><span data-stu-id="c350c-116">Script explanation</span></span>

<span data-ttu-id="c350c-117">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="c350c-117">Each command in the table links to command specific documentation.</span></span> <span data-ttu-id="c350c-118">This script uses the following commands:</span><span class="sxs-lookup"><span data-stu-id="c350c-118">This script uses the following commands:</span></span>

| <span data-ttu-id="c350c-119">Command</span><span class="sxs-lookup"><span data-stu-id="c350c-119">Command</span></span> | <span data-ttu-id="c350c-120">Notes</span><span class="sxs-lookup"><span data-stu-id="c350c-120">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c350c-121">az group create</span><span class="sxs-lookup"><span data-stu-id="c350c-121">az group create</span></span>](/cli/azure/group#az-group-create) | <span data-ttu-id="c350c-122">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="c350c-122">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="c350c-123">az signalr create</span><span class="sxs-lookup"><span data-stu-id="c350c-123">az signalr create</span></span>](/cli/azure/ext/signalr/signalr#ext-signalr-az-signalr-create) | <span data-ttu-id="c350c-124">Creates an Azure SignalR Service resource.</span><span class="sxs-lookup"><span data-stu-id="c350c-124">Creates an Azure SignalR Service resource.</span></span> |
| [<span data-ttu-id="c350c-125">az signalr key list</span><span class="sxs-lookup"><span data-stu-id="c350c-125">az signalr key list</span></span>](/cli/azure/ext/signalr/signalr/key#ext-signalr-az-signalr-key-list) | <span data-ttu-id="c350c-126">List the keys, which will be used by your application when pushing real-time content updates with SignalR.</span><span class="sxs-lookup"><span data-stu-id="c350c-126">List the keys, which will be used by your application when pushing real-time content updates with SignalR.</span></span> |
| [<span data-ttu-id="c350c-127">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="c350c-127">az appservice plan create</span></span>](/cli/azure/appservice/plan#az-appservice-plan-create) | <span data-ttu-id="c350c-128">Creates an Azure App Service Plan for hosting web apps.</span><span class="sxs-lookup"><span data-stu-id="c350c-128">Creates an Azure App Service Plan for hosting web apps.</span></span> |
| [<span data-ttu-id="c350c-129">az webapp create</span><span class="sxs-lookup"><span data-stu-id="c350c-129">az webapp create</span></span>](/cli/azure/webapp#az-webapp-create) | <span data-ttu-id="c350c-130">Creates an Azure Web app using the App Service hosting plan.</span><span class="sxs-lookup"><span data-stu-id="c350c-130">Creates an Azure Web app using the App Service hosting plan.</span></span> |
| [<span data-ttu-id="c350c-131">az webapp config appsettings set</span><span class="sxs-lookup"><span data-stu-id="c350c-131">az webapp config appsettings set</span></span>](/cli/azure/webapp/config/appsettings#az-webapp-config-appsettings-set) | <span data-ttu-id="c350c-132">Adds a new app setting for the web app.</span><span class="sxs-lookup"><span data-stu-id="c350c-132">Adds a new app setting for the web app.</span></span> <span data-ttu-id="c350c-133">This app setting is used to store the SignalR connection string.</span><span class="sxs-lookup"><span data-stu-id="c350c-133">This app setting is used to store the SignalR connection string.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c350c-134">Next steps</span><span class="sxs-lookup"><span data-stu-id="c350c-134">Next steps</span></span>

<span data-ttu-id="c350c-135">For more information on the Azure CLI, see [Azure CLI documentation](/cli/azure).</span><span class="sxs-lookup"><span data-stu-id="c350c-135">For more information on the Azure CLI, see [Azure CLI documentation](/cli/azure).</span></span>

<span data-ttu-id="c350c-136">Additional Azure SignalR Service CLI script samples can be found in the [Azure SignalR Service documentation](../signalr-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="c350c-136">Additional Azure SignalR Service CLI script samples can be found in the [Azure SignalR Service documentation](../signalr-cli-samples.md).</span></span>
