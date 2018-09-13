---
title: Azure CLI Script Sample - Deploy a web app from a local Git repository | Microsoft Docs
description: Azure CLI Script Sample - Deploy a web app from a local Git repository
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
ms.openlocfilehash: 7c970e6d4447fed96d91143a502ec823eb60df62
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552626"
---
# <a name="deploy-a-web-app-from-a-local-git-repository"></a><span data-ttu-id="cb6f4-103">Deploy a web app from a local Git repository</span><span class="sxs-lookup"><span data-stu-id="cb6f4-103">Deploy a web app from a local Git repository</span></span>

<span data-ttu-id="cb6f4-104">This sample script does the following using Azure CLI 2.0:</span><span class="sxs-lookup"><span data-stu-id="cb6f4-104">This sample script does the following using Azure CLI 2.0:</span></span> 

* <span data-ttu-id="cb6f4-105">Create a web app in Azure App Service in the West Europe Azure region.</span><span class="sxs-lookup"><span data-stu-id="cb6f4-105">Create a web app in Azure App Service in the West Europe Azure region.</span></span>
* <span data-ttu-id="cb6f4-106">Deploy web app code from a local Git repository.</span><span class="sxs-lookup"><span data-stu-id="cb6f4-106">Deploy web app code from a local Git repository.</span></span>
* <span data-ttu-id="cb6f4-107">Display the deployed web app in the browser.</span><span class="sxs-lookup"><span data-stu-id="cb6f4-107">Display the deployed web app in the browser.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cb6f4-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="cb6f4-108">Prerequisites</span></span>

* <span data-ttu-id="cb6f4-109">Run `az login` to log in to Azure.</span><span class="sxs-lookup"><span data-stu-id="cb6f4-109">Run `az login` to log in to Azure.</span></span>
* <span data-ttu-id="cb6f4-110">Commit your web app code into a local Git repository.</span><span class="sxs-lookup"><span data-stu-id="cb6f4-110">Commit your web app code into a local Git repository.</span></span>

## <a name="create-vm-sample"></a><span data-ttu-id="cb6f4-111">Create VM sample</span><span class="sxs-lookup"><span data-stu-id="cb6f4-111">Create VM sample</span></span>

[!code-azurecli[main](../../cli_scripts/app-service/deploy-local-git/deploy-local-git.sh "Deploy a web app from a local Git repository")]

## <a name="clean-up-deployment"></a><span data-ttu-id="cb6f4-112">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="cb6f4-112">Clean up deployment</span></span> 

<span data-ttu-id="cb6f4-113">After the script sample has been run, the follow command can be used to remove the Resource Group, web app, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="cb6f4-113">After the script sample has been run, the follow command can be used to remove the Resource Group, web app, and all related resources.</span></span>

```azurecli
az group delete --name $webappname
```

## <a name="script-explanation"></a><span data-ttu-id="cb6f4-114">Script explanation</span><span class="sxs-lookup"><span data-stu-id="cb6f4-114">Script explanation</span></span>

<span data-ttu-id="cb6f4-115">This script uses the following commands.</span><span class="sxs-lookup"><span data-stu-id="cb6f4-115">This script uses the following commands.</span></span> <span data-ttu-id="cb6f4-116">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="cb6f4-116">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="cb6f4-117">Command</span><span class="sxs-lookup"><span data-stu-id="cb6f4-117">Command</span></span> | <span data-ttu-id="cb6f4-118">Notes</span><span class="sxs-lookup"><span data-stu-id="cb6f4-118">Notes</span></span> |
|---|---|
| [<span data-ttu-id="cb6f4-119">az group create</span><span class="sxs-lookup"><span data-stu-id="cb6f4-119">az group create</span></span>](https://docs.microsoft.com/en-us/cli/azure/group#create) | <span data-ttu-id="cb6f4-120">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="cb6f4-120">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="cb6f4-121">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="cb6f4-121">az appservice plan create</span></span>](https://docs.microsoft.com/en-us/cli/azure/appservice/plan#create) | <span data-ttu-id="cb6f4-122">Creates an App Service plan.</span><span class="sxs-lookup"><span data-stu-id="cb6f4-122">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="cb6f4-123">az appservice web create</span><span class="sxs-lookup"><span data-stu-id="cb6f4-123">az appservice web create</span></span>](https://docs.microsoft.com/en-us/cli/azure/appservice/web#delete) | <span data-ttu-id="cb6f4-124">Creates a web app</span><span class="sxs-lookup"><span data-stu-id="cb6f4-124">Creates a web app</span></span> |
| [<span data-ttu-id="cb6f4-125">az appservice web source-control config-local-git</span><span class="sxs-lookup"><span data-stu-id="cb6f4-125">az appservice web source-control config-local-git</span></span>](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) | <span data-ttu-id="cb6f4-126">Creates a source control configuration for a local Git repository.</span><span class="sxs-lookup"><span data-stu-id="cb6f4-126">Creates a source control configuration for a local Git repository.</span></span> |
| [<span data-ttu-id="cb6f4-127">az appservice web browse</span><span class="sxs-lookup"><span data-stu-id="cb6f4-127">az appservice web browse</span></span>](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) | <span data-ttu-id="cb6f4-128">Open a web app in a browser.</span><span class="sxs-lookup"><span data-stu-id="cb6f4-128">Open a web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="cb6f4-129">Next steps</span><span class="sxs-lookup"><span data-stu-id="cb6f4-129">Next steps</span></span>

<span data-ttu-id="cb6f4-130">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/en-us/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="cb6f4-130">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/en-us/cli/azure/overview).</span></span>

<span data-ttu-id="cb6f4-131">Additional CLI script samples for Azure App Service Web Apps can be found in the [Azure CLI samples]().</span><span class="sxs-lookup"><span data-stu-id="cb6f4-131">Additional CLI script samples for Azure App Service Web Apps can be found in the [Azure CLI samples]().</span></span>