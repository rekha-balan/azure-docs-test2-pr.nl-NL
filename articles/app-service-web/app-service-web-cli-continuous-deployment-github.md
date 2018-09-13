---
title: Azure CLI Script Sample - Continuously deploy web app from GitHub | Microsoft Docs
description: Azure CLI Script Sample - Continuously deploy web app from GitHub
services: app-service\web
documentationcenter: ''
author: cephalin
manager: erikre
editor: ''
tags: azure-service-management
ms.assetid: ''
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: article
ms.date: 02/01/2017
ms.author: cephalin
ms.openlocfilehash: 649521d6f3740b099ab41c8ef70f7e4430aa5de9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662690"
---
# <a name="continuously-deploy-web-app-from-github"></a><span data-ttu-id="e5c5c-103">Continuously deploy web app from GitHub</span><span class="sxs-lookup"><span data-stu-id="e5c5c-103">Continuously deploy web app from GitHub</span></span>

<span data-ttu-id="e5c5c-104">This sample script does the following using Azure CLI 2.0:</span><span class="sxs-lookup"><span data-stu-id="e5c5c-104">This sample script does the following using Azure CLI 2.0:</span></span> 

* <span data-ttu-id="e5c5c-105">Create a web app in Azure App Service in the West Europe Azure region.</span><span class="sxs-lookup"><span data-stu-id="e5c5c-105">Create a web app in Azure App Service in the West Europe Azure region.</span></span> 
* <span data-ttu-id="e5c5c-106">Deploy your web app code from GitHub.</span><span class="sxs-lookup"><span data-stu-id="e5c5c-106">Deploy your web app code from GitHub.</span></span>
* <span data-ttu-id="e5c5c-107">Display the deployed web app in the browser.</span><span class="sxs-lookup"><span data-stu-id="e5c5c-107">Display the deployed web app in the browser.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e5c5c-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e5c5c-108">Prerequisites</span></span>

* <span data-ttu-id="e5c5c-109">Run `az login` to log in to Azure.</span><span class="sxs-lookup"><span data-stu-id="e5c5c-109">Run `az login` to log in to Azure.</span></span>
* <span data-ttu-id="e5c5c-110">Put your web app code in a GitHub repository you own.</span><span class="sxs-lookup"><span data-stu-id="e5c5c-110">Put your web app code in a GitHub repository you own.</span></span>

> [!NOTE]
> <span data-ttu-id="e5c5c-111">If you use a public GitHub repository you don't own, App Service will deploy code from that GitHub repository, but cannot set up the SSH key and webhooks necessary for continuous deployment.</span><span class="sxs-lookup"><span data-stu-id="e5c5c-111">If you use a public GitHub repository you don't own, App Service will deploy code from that GitHub repository, but cannot set up the SSH key and webhooks necessary for continuous deployment.</span></span>
>
>

## <a name="create-vm-sample"></a><span data-ttu-id="e5c5c-112">Create VM sample</span><span class="sxs-lookup"><span data-stu-id="e5c5c-112">Create VM sample</span></span>

[!code-azurecli[main](../../cli_scripts/app-service/deploy-github/deploy-github.sh "Continuously deploy web app from GitHub")]

## <a name="clean-up-deployment"></a><span data-ttu-id="e5c5c-113">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="e5c5c-113">Clean up deployment</span></span> 

<span data-ttu-id="e5c5c-114">After the script sample has been run, the follow command can be used to remove the Resource Group, web app, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="e5c5c-114">After the script sample has been run, the follow command can be used to remove the Resource Group, web app, and all related resources.</span></span>

```azurecli
az group delete --name $webappname
```

## <a name="script-explanation"></a><span data-ttu-id="e5c5c-115">Script explanation</span><span class="sxs-lookup"><span data-stu-id="e5c5c-115">Script explanation</span></span>

<span data-ttu-id="e5c5c-116">This script uses the following commands.</span><span class="sxs-lookup"><span data-stu-id="e5c5c-116">This script uses the following commands.</span></span> <span data-ttu-id="e5c5c-117">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="e5c5c-117">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="e5c5c-118">Command</span><span class="sxs-lookup"><span data-stu-id="e5c5c-118">Command</span></span> | <span data-ttu-id="e5c5c-119">Notes</span><span class="sxs-lookup"><span data-stu-id="e5c5c-119">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e5c5c-120">az group create</span><span class="sxs-lookup"><span data-stu-id="e5c5c-120">az group create</span></span>](https://docs.microsoft.com/en-us/cli/azure/group#create) | <span data-ttu-id="e5c5c-121">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="e5c5c-121">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="e5c5c-122">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="e5c5c-122">az appservice plan create</span></span>](https://docs.microsoft.com/en-us/cli/azure/appservice/plan#create) | <span data-ttu-id="e5c5c-123">Creates an App Service plan.</span><span class="sxs-lookup"><span data-stu-id="e5c5c-123">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="e5c5c-124">az appservice web create</span><span class="sxs-lookup"><span data-stu-id="e5c5c-124">az appservice web create</span></span>](https://docs.microsoft.com/en-us/cli/azure/appservice/web#delete) | <span data-ttu-id="e5c5c-125">Creates a web app.</span><span class="sxs-lookup"><span data-stu-id="e5c5c-125">Creates a web app.</span></span> |
| [<span data-ttu-id="e5c5c-126">az appservice web source-control config</span><span class="sxs-lookup"><span data-stu-id="e5c5c-126">az appservice web source-control config</span></span>](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config) | <span data-ttu-id="e5c5c-127">Associates a web app with a Git or Mercurial repository.</span><span class="sxs-lookup"><span data-stu-id="e5c5c-127">Associates a web app with a Git or Mercurial repository.</span></span> |
| [<span data-ttu-id="e5c5c-128">az appservice web browse</span><span class="sxs-lookup"><span data-stu-id="e5c5c-128">az appservice web browse</span></span>](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) | <span data-ttu-id="e5c5c-129">Open a web app in a browser.</span><span class="sxs-lookup"><span data-stu-id="e5c5c-129">Open a web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e5c5c-130">Next steps</span><span class="sxs-lookup"><span data-stu-id="e5c5c-130">Next steps</span></span>

<span data-ttu-id="e5c5c-131">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/en-us/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e5c5c-131">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/en-us/cli/azure/overview).</span></span>

<span data-ttu-id="e5c5c-132">Additional CLI script samples for Azure App Service Web Apps can be found in the [Azure CLI samples]().</span><span class="sxs-lookup"><span data-stu-id="e5c5c-132">Additional CLI script samples for Azure App Service Web Apps can be found in the [Azure CLI samples]().</span></span>
