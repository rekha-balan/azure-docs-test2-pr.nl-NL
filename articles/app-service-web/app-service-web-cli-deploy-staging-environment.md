---
title: Azure CLI Script Sample - Deploy a web app to a staging environment | Microsoft Docs
description: Azure CLI Script Sample - Deploy a web app to a staging environment
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
ms.openlocfilehash: 6e24be1f9525b976864d63dc433e853f399a545d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553410"
---
# <a name="deploy-a-web-app-to-a-staging-environment"></a><span data-ttu-id="132ef-103">Deploy a web app to a staging environment</span><span class="sxs-lookup"><span data-stu-id="132ef-103">Deploy a web app to a staging environment</span></span>

<span data-ttu-id="132ef-104">This sample script does the following using Azure CLI 2.0:</span><span class="sxs-lookup"><span data-stu-id="132ef-104">This sample script does the following using Azure CLI 2.0:</span></span> 

* <span data-ttu-id="132ef-105">Create a web app in Azure App Service in the West Europe Azure region.</span><span class="sxs-lookup"><span data-stu-id="132ef-105">Create a web app in Azure App Service in the West Europe Azure region.</span></span>
* <span data-ttu-id="132ef-106">Upgrade the App Service plan to STANDARD tier (minimum for deployment slots).</span><span class="sxs-lookup"><span data-stu-id="132ef-106">Upgrade the App Service plan to STANDARD tier (minimum for deployment slots).</span></span>
* <span data-ttu-id="132ef-107">Set up a deployment slot named "staging".</span><span class="sxs-lookup"><span data-stu-id="132ef-107">Set up a deployment slot named "staging".</span></span>
* <span data-ttu-id="132ef-108">Deploy your web app code from GitHub to the staging slot.</span><span class="sxs-lookup"><span data-stu-id="132ef-108">Deploy your web app code from GitHub to the staging slot.</span></span>
* <span data-ttu-id="132ef-109">Open the deployed staging slot in the browser for verification.</span><span class="sxs-lookup"><span data-stu-id="132ef-109">Open the deployed staging slot in the browser for verification.</span></span>
* <span data-ttu-id="132ef-110">Swap the staging slot into production.</span><span class="sxs-lookup"><span data-stu-id="132ef-110">Swap the staging slot into production.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="132ef-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="132ef-111">Prerequisites</span></span>

* <span data-ttu-id="132ef-112">Run `az login` to log in to Azure.</span><span class="sxs-lookup"><span data-stu-id="132ef-112">Run `az login` to log in to Azure.</span></span>
* <span data-ttu-id="132ef-113">Put your web app code in a GitHub repository you own.</span><span class="sxs-lookup"><span data-stu-id="132ef-113">Put your web app code in a GitHub repository you own.</span></span>

> [!NOTE]
> <span data-ttu-id="132ef-114">If you use a public GitHub repository you don't own, App Service will deploy code from that GitHub repository, but cannot set up the SSH key and webhooks necessary for continuous deployment.</span><span class="sxs-lookup"><span data-stu-id="132ef-114">If you use a public GitHub repository you don't own, App Service will deploy code from that GitHub repository, but cannot set up the SSH key and webhooks necessary for continuous deployment.</span></span>
>
>

## <a name="create-vm-sample"></a><span data-ttu-id="132ef-115">Create VM sample</span><span class="sxs-lookup"><span data-stu-id="132ef-115">Create VM sample</span></span>

[!code-azurecli[main](../../cli_scripts/app-service/deploy-deployment-slot/deploy-deployment-slot.sh "Deploy a web app to a staging environment")]

## <a name="clean-up-deployment"></a><span data-ttu-id="132ef-116">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="132ef-116">Clean up deployment</span></span> 

<span data-ttu-id="132ef-117">After the script sample has been run, the follow command can be used to remove the Resource Group, web app, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="132ef-117">After the script sample has been run, the follow command can be used to remove the Resource Group, web app, and all related resources.</span></span>

```azurecli
az group delete --name $webappname
```

## <a name="script-explanation"></a><span data-ttu-id="132ef-118">Script explanation</span><span class="sxs-lookup"><span data-stu-id="132ef-118">Script explanation</span></span>

<span data-ttu-id="132ef-119">This script uses the following commands.</span><span class="sxs-lookup"><span data-stu-id="132ef-119">This script uses the following commands.</span></span> <span data-ttu-id="132ef-120">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="132ef-120">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="132ef-121">Command</span><span class="sxs-lookup"><span data-stu-id="132ef-121">Command</span></span> | <span data-ttu-id="132ef-122">Notes</span><span class="sxs-lookup"><span data-stu-id="132ef-122">Notes</span></span> |
|---|---|
| [<span data-ttu-id="132ef-123">az group create</span><span class="sxs-lookup"><span data-stu-id="132ef-123">az group create</span></span>](https://docs.microsoft.com/en-us/cli/azure/group#create) | <span data-ttu-id="132ef-124">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="132ef-124">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="132ef-125">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="132ef-125">az appservice plan create</span></span>](https://docs.microsoft.com/en-us/cli/azure/appservice/plan#create) | <span data-ttu-id="132ef-126">Creates an App Service plan.</span><span class="sxs-lookup"><span data-stu-id="132ef-126">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="132ef-127">az appservice web create</span><span class="sxs-lookup"><span data-stu-id="132ef-127">az appservice web create</span></span>](https://docs.microsoft.com/en-us/cli/azure/appservice/web#delete) | <span data-ttu-id="132ef-128">Creates a web app.</span><span class="sxs-lookup"><span data-stu-id="132ef-128">Creates a web app.</span></span> |
| [<span data-ttu-id="132ef-129">az appservice plan update</span><span class="sxs-lookup"><span data-stu-id="132ef-129">az appservice plan update</span></span>](https://docs.microsoft.com/en-us/cli/azure/appservice/plan#update) | <span data-ttu-id="132ef-130">Update an App Service plan to scale its pricing tier.</span><span class="sxs-lookup"><span data-stu-id="132ef-130">Update an App Service plan to scale its pricing tier.</span></span> |
| [<span data-ttu-id="132ef-131">az appservice web deployment slot create</span><span class="sxs-lookup"><span data-stu-id="132ef-131">az appservice web deployment slot create</span></span>](https://docs.microsoft.com/en-us/cli/azure/appservice/web/deployment/slot#create) | <span data-ttu-id="132ef-132">Create a deployment slot.</span><span class="sxs-lookup"><span data-stu-id="132ef-132">Create a deployment slot.</span></span> |
| [<span data-ttu-id="132ef-133">az appservice web source-control config</span><span class="sxs-lookup"><span data-stu-id="132ef-133">az appservice web source-control config</span></span>](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config) | <span data-ttu-id="132ef-134">Associates a web app with a Git or Mercurial repository.</span><span class="sxs-lookup"><span data-stu-id="132ef-134">Associates a web app with a Git or Mercurial repository.</span></span> |
| [<span data-ttu-id="132ef-135">az appservice web browse</span><span class="sxs-lookup"><span data-stu-id="132ef-135">az appservice web browse</span></span>](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) | <span data-ttu-id="132ef-136">Open a web app in a browser.</span><span class="sxs-lookup"><span data-stu-id="132ef-136">Open a web app in a browser.</span></span> |
| [<span data-ttu-id="132ef-137">az appservice web deployment slot swap</span><span class="sxs-lookup"><span data-stu-id="132ef-137">az appservice web deployment slot swap</span></span>](https://docs.microsoft.com/en-us/cli/azure/appservice/web/deployment/slot#swap) | <span data-ttu-id="132ef-138">Swap a specified deployment slot into production.</span><span class="sxs-lookup"><span data-stu-id="132ef-138">Swap a specified deployment slot into production.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="132ef-139">Next steps</span><span class="sxs-lookup"><span data-stu-id="132ef-139">Next steps</span></span>

<span data-ttu-id="132ef-140">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/en-us/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="132ef-140">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/en-us/cli/azure/overview).</span></span>

<span data-ttu-id="132ef-141">Additional CLI script samples for Azure App Service Web Apps can be found in the [Azure CLI samples]().</span><span class="sxs-lookup"><span data-stu-id="132ef-141">Additional CLI script samples for Azure App Service Web Apps can be found in the [Azure CLI samples]().</span></span>
