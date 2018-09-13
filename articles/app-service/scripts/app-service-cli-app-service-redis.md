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
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 12/11/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 0aa1fd19af8819de54ab468c48516f402c1e2a9d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968492"
---
# <a name="connect-a-web-app-to-a-redis-cache"></a><span data-ttu-id="dab84-103">Connect a web app to a redis cache</span><span class="sxs-lookup"><span data-stu-id="dab84-103">Connect a web app to a redis cache</span></span>

<span data-ttu-id="dab84-104">This sample script creates an Azure redis cache and an Azure web app.</span><span class="sxs-lookup"><span data-stu-id="dab84-104">This sample script creates an Azure redis cache and an Azure web app.</span></span> <span data-ttu-id="dab84-105">It then links the redis cache to the web app using app settings.</span><span class="sxs-lookup"><span data-stu-id="dab84-105">It then links the redis cache to the web app using app settings.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

<span data-ttu-id="dab84-106">If you choose to install and use the CLI locally, you need Azure CLI version 2.0 or later.</span><span class="sxs-lookup"><span data-stu-id="dab84-106">If you choose to install and use the CLI locally, you need Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="dab84-107">To find the version, run `az --version`.</span><span class="sxs-lookup"><span data-stu-id="dab84-107">To find the version, run `az --version`.</span></span> <span data-ttu-id="dab84-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="dab84-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="sample-script"></a><span data-ttu-id="dab84-109">Sample script</span><span class="sxs-lookup"><span data-stu-id="dab84-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-redis/connect-to-redis.sh "Azure Redis Cache")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="dab84-110">Script explanation</span><span class="sxs-lookup"><span data-stu-id="dab84-110">Script explanation</span></span>

<span data-ttu-id="dab84-111">This script uses the following commands to create a resource group, web app, redis cache, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="dab84-111">This script uses the following commands to create a resource group, web app, redis cache, and all related resources.</span></span> <span data-ttu-id="dab84-112">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="dab84-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="dab84-113">Command</span><span class="sxs-lookup"><span data-stu-id="dab84-113">Command</span></span> | <span data-ttu-id="dab84-114">Notes</span><span class="sxs-lookup"><span data-stu-id="dab84-114">Notes</span></span> |
|---|---|
| [`az group create`](/cli/azure/group?view=azure-cli-latest#az-group-create) | <span data-ttu-id="dab84-115">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="dab84-115">Creates a resource group in which all resources are stored.</span></span> |
| [`az appservice plan create`](/cli/azure/appservice/plan?view=azure-cli-latest#az-appservice-plan-create) | <span data-ttu-id="dab84-116">Creates an App Service plan.</span><span class="sxs-lookup"><span data-stu-id="dab84-116">Creates an App Service plan.</span></span> |
| [`az webapp create`](/cli/azure/webapp?view=azure-cli-latest#az-webapp-create) | <span data-ttu-id="dab84-117">Creates an Azure web app.</span><span class="sxs-lookup"><span data-stu-id="dab84-117">Creates an Azure web app.</span></span> |
| [`az redis create`](/cli/azure/redis?view=azure-cli-latest#az-redis-create) | <span data-ttu-id="dab84-118">Create new Redis Cache instance.</span><span class="sxs-lookup"><span data-stu-id="dab84-118">Create new Redis Cache instance.</span></span> |
| [`az redis list-keys`](/cli/azure/redis?view=azure-cli-latest#az-redis-list-keys) | <span data-ttu-id="dab84-119">Lists the access keys for the redis cache instance.</span><span class="sxs-lookup"><span data-stu-id="dab84-119">Lists the access keys for the redis cache instance.</span></span> |
| [`az webapp config appsettings set`](/cli/azure/webapp/config/appsettings?view=azure-cli-latest#az-webapp-config-appsettings-set) | <span data-ttu-id="dab84-120">Creates or updates an app setting for an Azure web app.</span><span class="sxs-lookup"><span data-stu-id="dab84-120">Creates or updates an app setting for an Azure web app.</span></span> <span data-ttu-id="dab84-121">App settings are exposed as environment variables for your app.</span><span class="sxs-lookup"><span data-stu-id="dab84-121">App settings are exposed as environment variables for your app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="dab84-122">Next steps</span><span class="sxs-lookup"><span data-stu-id="dab84-122">Next steps</span></span>

<span data-ttu-id="dab84-123">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span><span class="sxs-lookup"><span data-stu-id="dab84-123">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span></span>

<span data-ttu-id="dab84-124">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="dab84-124">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
