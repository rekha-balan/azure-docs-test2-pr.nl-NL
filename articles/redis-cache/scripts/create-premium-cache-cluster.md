---
title: Azure CLI Script Sample - Create a Premium Azure Redis Cache with clustering | Microsoft Docs
description: Azure CLI Script Sample - Create a Premium tier Azure Redis Cache with clustering
services: redis-cache
documentationcenter: ''
author: wesmc7777
manager: cfowler
editor: ''
tags: azure-service-management
ms.assetid: 07bcceae-2521-4fe3-b88f-ed833104ddd2
ms.service: cache-redis
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 08/30/2017
ms.author: wesmc
ms.openlocfilehash: fb97d19d50ac9845c2495bd167a9cd30805d464b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44800467"
---
# <a name="create-a-premium-azure-redis-cache-with-clustering"></a><span data-ttu-id="b181d-103">Create a Premium Azure Redis Cache with clustering</span><span class="sxs-lookup"><span data-stu-id="b181d-103">Create a Premium Azure Redis Cache with clustering</span></span>

<span data-ttu-id="b181d-104">In this scenario, you learn how to create a 6 GB Premium tier Azure Redis Cache with clustering enabled and two shards.</span><span class="sxs-lookup"><span data-stu-id="b181d-104">In this scenario, you learn how to create a 6 GB Premium tier Azure Redis Cache with clustering enabled and two shards.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="b181d-105">Sample script</span><span class="sxs-lookup"><span data-stu-id="b181d-105">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/redis-cache/create-premium-cache-cluster/create-premium-cache-cluster.sh "Azure Redis Cache")]

[!INCLUDE [cli-script-clean-up](../../../includes/redis-cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="b181d-106">Script explanation</span><span class="sxs-lookup"><span data-stu-id="b181d-106">Script explanation</span></span>

<span data-ttu-id="b181d-107">This script uses the following commands to create a resource group and a Premium tier redis cache with clustering enable.</span><span class="sxs-lookup"><span data-stu-id="b181d-107">This script uses the following commands to create a resource group and a Premium tier redis cache with clustering enable.</span></span> <span data-ttu-id="b181d-108">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="b181d-108">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="b181d-109">Command</span><span class="sxs-lookup"><span data-stu-id="b181d-109">Command</span></span> | <span data-ttu-id="b181d-110">Notes</span><span class="sxs-lookup"><span data-stu-id="b181d-110">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b181d-111">az group create</span><span class="sxs-lookup"><span data-stu-id="b181d-111">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#az_group_create) | <span data-ttu-id="b181d-112">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="b181d-112">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="b181d-113">az redis create</span><span class="sxs-lookup"><span data-stu-id="b181d-113">az redis create</span></span>](https://docs.microsoft.com/cli/azure/redis#az_redis_create) | <span data-ttu-id="b181d-114">Create Redis Cache instance.</span><span class="sxs-lookup"><span data-stu-id="b181d-114">Create Redis Cache instance.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="b181d-115">Next steps</span><span class="sxs-lookup"><span data-stu-id="b181d-115">Next steps</span></span>

<span data-ttu-id="b181d-116">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span><span class="sxs-lookup"><span data-stu-id="b181d-116">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span></span>

<span data-ttu-id="b181d-117">Additional Azure Redis Cache CLI script samples can be found in the [Azure Redis Cache documentation](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="b181d-117">Additional Azure Redis Cache CLI script samples can be found in the [Azure Redis Cache documentation](../cli-samples.md).</span></span>