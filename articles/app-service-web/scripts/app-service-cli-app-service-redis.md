---
title: Azure CLI Script Sample - Connect a web app to a redis cache | Microsoft Docs
description: Azure CLI Script Sample - Connect a web app to a redis cache
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: ''
tags: azure-service-management
ms.assetid: bc8345b2-8487-40c6-a91f-77414e8688e6
ms.service: app-service
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.openlocfilehash: a7fbd85b6dd9c083fc71f2b1632d8cec4940c0bc
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551296"
---
# <a name="connect-a-web-app-to-a-redis-cache"></a><span data-ttu-id="a06ee-103">Connect a web app to a redis cache</span><span class="sxs-lookup"><span data-stu-id="a06ee-103">Connect a web app to a redis cache</span></span>

<span data-ttu-id="a06ee-104">In this scenario you will learn how to create an Azure redis cache and an Azure web app.</span><span class="sxs-lookup"><span data-stu-id="a06ee-104">In this scenario you will learn how to create an Azure redis cache and an Azure web app.</span></span> <span data-ttu-id="a06ee-105">Then you will link the redis cache to the web app using app settings.</span><span class="sxs-lookup"><span data-stu-id="a06ee-105">Then you will link the redis cache to the web app using app settings.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="a06ee-106">Sample script</span><span class="sxs-lookup"><span data-stu-id="a06ee-106">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/app-service/connect-to-redis/connect-to-redis.sh "Azure Redis Cache")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="a06ee-107">Script explanation</span><span class="sxs-lookup"><span data-stu-id="a06ee-107">Script explanation</span></span>

<span data-ttu-id="a06ee-108">This script uses the following commands to create a resource group, web app, redis cache and all related resources.</span><span class="sxs-lookup"><span data-stu-id="a06ee-108">This script uses the following commands to create a resource group, web app, redis cache and all related resources.</span></span> <span data-ttu-id="a06ee-109">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="a06ee-109">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="a06ee-110">Command</span><span class="sxs-lookup"><span data-stu-id="a06ee-110">Command</span></span> | <span data-ttu-id="a06ee-111">Notes</span><span class="sxs-lookup"><span data-stu-id="a06ee-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="a06ee-112">az group create</span><span class="sxs-lookup"><span data-stu-id="a06ee-112">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="a06ee-113">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="a06ee-113">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="a06ee-114">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="a06ee-114">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="a06ee-115">Creates an App Service plan.</span><span class="sxs-lookup"><span data-stu-id="a06ee-115">Creates an App Service plan.</span></span> <span data-ttu-id="a06ee-116">This is like a server farm for your Azure web app.</span><span class="sxs-lookup"><span data-stu-id="a06ee-116">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="a06ee-117">az appservice web create</span><span class="sxs-lookup"><span data-stu-id="a06ee-117">az appservice web create</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#create) | <span data-ttu-id="a06ee-118">Creates an Azure web app within the App Service plan.</span><span class="sxs-lookup"><span data-stu-id="a06ee-118">Creates an Azure web app within the App Service plan.</span></span> |
| [<span data-ttu-id="a06ee-119">az redis create</span><span class="sxs-lookup"><span data-stu-id="a06ee-119">az redis create</span></span>](https://docs.microsoft.com/en-us/cli/azure/redis#create) | <span data-ttu-id="a06ee-120">Create new Redis Cache instance.</span><span class="sxs-lookup"><span data-stu-id="a06ee-120">Create new Redis Cache instance.</span></span> <span data-ttu-id="a06ee-121">This is where the data will be stored.</span><span class="sxs-lookup"><span data-stu-id="a06ee-121">This is where the data will be stored.</span></span> |
| [<span data-ttu-id="a06ee-122">az redis list-keys</span><span class="sxs-lookup"><span data-stu-id="a06ee-122">az redis list-keys</span></span>](https://docs.microsoft.com/en-us/cli/azure/redis#list-keys) | <span data-ttu-id="a06ee-123">Lists the access keys for the redis cache instance.</span><span class="sxs-lookup"><span data-stu-id="a06ee-123">Lists the access keys for the redis cache instance.</span></span> |
| [<span data-ttu-id="a06ee-124">az appservice web config appsetings update</span><span class="sxs-lookup"><span data-stu-id="a06ee-124">az appservice web config appsetings update</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) | <span data-ttu-id="a06ee-125">Creates or updates an app setting for an Azure web app.</span><span class="sxs-lookup"><span data-stu-id="a06ee-125">Creates or updates an app setting for an Azure web app.</span></span> <span data-ttu-id="a06ee-126">App settings are exposed as environment variables for your app.</span><span class="sxs-lookup"><span data-stu-id="a06ee-126">App settings are exposed as environment variables for your app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a06ee-127">Next steps</span><span class="sxs-lookup"><span data-stu-id="a06ee-127">Next steps</span></span>

<span data-ttu-id="a06ee-128">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a06ee-128">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="a06ee-129">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="a06ee-129">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>