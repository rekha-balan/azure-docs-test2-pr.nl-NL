---
title: Azure CLI Script Sample - Get the hostname, ports, and keys for Azure Redis Cache | Microsoft Docs
description: Azure CLI Script Sample - Get the hostname, ports, and keys for an Azure Redis Cache instance
services: redis-cache
documentationcenter: ''
author: steved0x
manager: douge
editor: ''
tags: azure-service-management
ms.assetid: 761eb24e-2ba7-418d-8fc3-431153e69a90
ms.service: cache-redis
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 04/14/2017
ms.author: sdanie
ms.openlocfilehash: cd9adc784bceb0fff5e7c2bbee2be0950c51c8f6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661674"
---
# <a name="get-the-hostname-ports-and-keys-for-azure-redis-cache"></a><span data-ttu-id="4ddf5-103">Get the hostname, ports, and keys for Azure Redis Cache</span><span class="sxs-lookup"><span data-stu-id="4ddf5-103">Get the hostname, ports, and keys for Azure Redis Cache</span></span>

<span data-ttu-id="4ddf5-104">In this scenario, you learn how to retrieve the hostname, ports, and keys used to connect to an Azure Redis Cache instance.</span><span class="sxs-lookup"><span data-stu-id="4ddf5-104">In this scenario, you learn how to retrieve the hostname, ports, and keys used to connect to an Azure Redis Cache instance.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="4ddf5-105">Sample script</span><span class="sxs-lookup"><span data-stu-id="4ddf5-105">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/redis-cache/cache-keys-ports/cache-keys-ports.sh "Azure Redis Cache")]


## <a name="script-explanation"></a><span data-ttu-id="4ddf5-106">Script explanation</span><span class="sxs-lookup"><span data-stu-id="4ddf5-106">Script explanation</span></span>

<span data-ttu-id="4ddf5-107">This script uses the following commands to retrieve the hostname, keys, and ports of an Azure Redis Cache instance.</span><span class="sxs-lookup"><span data-stu-id="4ddf5-107">This script uses the following commands to retrieve the hostname, keys, and ports of an Azure Redis Cache instance.</span></span> <span data-ttu-id="4ddf5-108">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="4ddf5-108">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="4ddf5-109">Command</span><span class="sxs-lookup"><span data-stu-id="4ddf5-109">Command</span></span> | <span data-ttu-id="4ddf5-110">Notes</span><span class="sxs-lookup"><span data-stu-id="4ddf5-110">Notes</span></span> |
|---|---|
| [<span data-ttu-id="4ddf5-111">az redis show</span><span class="sxs-lookup"><span data-stu-id="4ddf5-111">az redis show</span></span>](https://docs.microsoft.com/cli/azure/redis#show) | <span data-ttu-id="4ddf5-112">Retrieve details of an Azure Redis Cache instance.</span><span class="sxs-lookup"><span data-stu-id="4ddf5-112">Retrieve details of an Azure Redis Cache instance.</span></span> |
| [<span data-ttu-id="4ddf5-113">az redis list-keys</span><span class="sxs-lookup"><span data-stu-id="4ddf5-113">az redis list-keys</span></span>](https://docs.microsoft.com/cli/azure/redis#list-keys) | <span data-ttu-id="4ddf5-114">Retrieve access keys for an Azure Redis Cache instance.</span><span class="sxs-lookup"><span data-stu-id="4ddf5-114">Retrieve access keys for an Azure Redis Cache instance.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="4ddf5-115">Next steps</span><span class="sxs-lookup"><span data-stu-id="4ddf5-115">Next steps</span></span>

<span data-ttu-id="4ddf5-116">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4ddf5-116">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="4ddf5-117">Additional Azure Redis Cache CLI script samples can be found in the [Azure Redis Cache documentation](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="4ddf5-117">Additional Azure Redis Cache CLI script samples can be found in the [Azure Redis Cache documentation](../cli-samples.md).</span></span>