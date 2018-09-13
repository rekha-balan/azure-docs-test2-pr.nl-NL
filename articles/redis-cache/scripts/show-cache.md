---
title: Azure CLI Script Sample - Get details of an Azure Redis Cache | Microsoft Docs
description: Azure CLI Script Sample - Get details of an Azure Redis Cache
services: redis-cache
documentationcenter: ''
author: steved0x
manager: douge
editor: ''
tags: azure-service-management
ms.assetid: 155924e6-00d5-4a8c-ba99-5189f300464a
ms.service: cache-redis
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 04/14/2017
ms.author: sdanie
ms.openlocfilehash: 9f4eb32227bd8a68837eabd58b9d058bc4995d17
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44548757"
---
# <a name="get-details-of-an-azure-redis-cache"></a>Get details of an Azure Redis Cache

In this scenario, you learn how to retrieve the details of an Azure Redis Cache instance, including its provisioning status.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a>Sample script

[!code-azurecli[main](../../../cli_scripts/redis-cache/show-cache/show-cache.sh "Azure Redis Cache")]

## <a name="script-explanation"></a>Script explanation

This script uses the following commands to retrieve the details of an Azure Redis Cache instance. Each command in the table links to command specific documentation.

| Command | Notes |
|---|---|
| [az redis show](https://docs.microsoft.com/cli/azure/redis#show) | Retrieve details of an Azure Redis Cache instance. |


## <a name="next-steps"></a>Next steps

For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).

Additional Azure Redis Cache CLI script samples can be found in the [Azure Redis Cache documentation](../cli-samples.md).