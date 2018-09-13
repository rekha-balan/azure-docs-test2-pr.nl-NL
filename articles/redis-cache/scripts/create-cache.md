---
title: Azure CLI Script Sample - Create an Azure Redis Cache | Microsoft Docs
description: Azure CLI Script Sample - Create an Azure Redis Cache
services: redis-cache
documentationcenter: ''
author: steved0x
manager: douge
editor: ''
tags: azure-service-management
ms.assetid: afd7f6e0-9297-4c98-a95e-597be939cef7
ms.service: cache-redis
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 04/14/2017
ms.author: sdanie
ms.openlocfilehash: c6b153d80de4cbf2bec1bc70d67be7befa0c5ec3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661415"
---
# <a name="create-an-azure-redis-cache"></a><span data-ttu-id="54227-103">Create an Azure Redis Cache</span><span class="sxs-lookup"><span data-stu-id="54227-103">Create an Azure Redis Cache</span></span>

<span data-ttu-id="54227-104">In this scenario, you learn how to create an Azure Redis Cache.</span><span class="sxs-lookup"><span data-stu-id="54227-104">In this scenario, you learn how to create an Azure Redis Cache.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="54227-105">Sample script</span><span class="sxs-lookup"><span data-stu-id="54227-105">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/redis-cache/create-cache/create-cache.sh "Azure Redis Cache")]

[!INCLUDE [cli-script-clean-up](../../../includes/redis-cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="54227-106">Script explanation</span><span class="sxs-lookup"><span data-stu-id="54227-106">Script explanation</span></span>

<span data-ttu-id="54227-107">This script uses the following commands to create a resource group and a redis cache.</span><span class="sxs-lookup"><span data-stu-id="54227-107">This script uses the following commands to create a resource group and a redis cache.</span></span> <span data-ttu-id="54227-108">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="54227-108">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="54227-109">Command</span><span class="sxs-lookup"><span data-stu-id="54227-109">Command</span></span> | <span data-ttu-id="54227-110">Notes</span><span class="sxs-lookup"><span data-stu-id="54227-110">Notes</span></span> |
|---|---|
| [<span data-ttu-id="54227-111">az group create</span><span class="sxs-lookup"><span data-stu-id="54227-111">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="54227-112">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="54227-112">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="54227-113">az redis create</span><span class="sxs-lookup"><span data-stu-id="54227-113">az redis create</span></span>](https://docs.microsoft.com/cli/azure/redis#create) | <span data-ttu-id="54227-114">Create Redis Cache instance.</span><span class="sxs-lookup"><span data-stu-id="54227-114">Create Redis Cache instance.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="54227-115">Next steps</span><span class="sxs-lookup"><span data-stu-id="54227-115">Next steps</span></span>

<span data-ttu-id="54227-116">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="54227-116">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="54227-117">Additional Azure Redis Cache CLI script samples can be found in the [Azure Redis Cache documentation](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="54227-117">Additional Azure Redis Cache CLI script samples can be found in the [Azure Redis Cache documentation](../cli-samples.md).</span></span>