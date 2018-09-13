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
# <a name="create-a-premium-azure-redis-cache-with-clustering"></a>Create a Premium Azure Redis Cache with clustering

In this scenario, you learn how to create a 6 GB Premium tier Azure Redis Cache with clustering enabled and two shards.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a>Sample script

[!code-azurecli[main](../../../cli_scripts/redis-cache/create-premium-cache-cluster/create-premium-cache-cluster.sh "Azure Redis Cache")]

[!INCLUDE [cli-script-clean-up](../../../includes/redis-cli-script-clean-up.md)]

## <a name="script-explanation"></a>Script explanation

This script uses the following commands to create a resource group and a Premium tier redis cache with clustering enable. Each command in the table links to command specific documentation.

| Command | Notes |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#az_group_create) | Creates a resource group in which all resources are stored. |
| [az redis create](https://docs.microsoft.com/cli/azure/redis#az_redis_create) | Create Redis Cache instance. |


## <a name="next-steps"></a>Next steps

For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).

Additional Azure Redis Cache CLI script samples can be found in the [Azure Redis Cache documentation](../cli-samples.md).