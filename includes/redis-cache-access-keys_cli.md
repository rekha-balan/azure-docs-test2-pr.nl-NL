---
title: include file
description: include file
services: redis-cache
author: wesmc7777
ms.service: cache
ms.topic: include
ms.date: 03/28/2018
ms.author: wesmc
ms.custom: include file
ms.openlocfilehash: 0289604cce7f956406d65743d5b058ec92111724
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856583"
---
### <a name="retrieve-host-name-ports-and-access-keys-using-azure-cli"></a><span data-ttu-id="3459a-103">Retrieve host name, ports, and access keys using Azure CLI</span><span class="sxs-lookup"><span data-stu-id="3459a-103">Retrieve host name, ports, and access keys using Azure CLI</span></span>
<span data-ttu-id="3459a-104">To retrieve the host name and ports using Azure CLI 2.0 you can call [az redis show](https://docs.microsoft.com/cli/azure/redis#az_redis_show), and to retrieve the keys you can call [az redis list-keys](https://docs.microsoft.com/cli/azure/redis#az_redis_list_keys).</span><span class="sxs-lookup"><span data-stu-id="3459a-104">To retrieve the host name and ports using Azure CLI 2.0 you can call [az redis show](https://docs.microsoft.com/cli/azure/redis#az_redis_show), and to retrieve the keys you can call [az redis list-keys](https://docs.microsoft.com/cli/azure/redis#az_redis_list_keys).</span></span> <span data-ttu-id="3459a-105">The following script calls these two commands and echos the hostname, ports, and keys to the console.</span><span class="sxs-lookup"><span data-stu-id="3459a-105">The following script calls these two commands and echos the hostname, ports, and keys to the console.</span></span>

```azurecli
#/bin/bash

# Retrieve the hostname, ports, and keys for contosoCache located in contosoGroup

# Retrieve the hostname and ports for an Azure Redis Cache instance
redis=($(az redis show --name contosoCache --resource-group contosoGroup --query [hostName,enableNonSslPort,port,sslPort] --output tsv))

# Retrieve the keys for an Azure Redis Cache instance
keys=($(az redis list-keys --name contosoCache --resource-group contosoGroup --query [primaryKey,secondaryKey] --output tsv))

# Display the retrieved hostname, keys, and ports
echo "Hostname:" ${redis[0]}
echo "Non SSL Port:" ${redis[2]}
echo "Non SSL Port Enabled:" ${redis[1]}
echo "SSL Port:" ${redis[3]}
echo "Primary Key:" ${keys[0]}
echo "Secondary Key:" ${keys[1]}
```

<span data-ttu-id="3459a-106">For more information about this script, see [Get the hostname, ports, and keys for Azure Redis Cache](../articles/redis-cache/scripts/cache-keys-ports.md).</span><span class="sxs-lookup"><span data-stu-id="3459a-106">For more information about this script, see [Get the hostname, ports, and keys for Azure Redis Cache](../articles/redis-cache/scripts/cache-keys-ports.md).</span></span> <span data-ttu-id="3459a-107">For more information on Azure CLI 2.0, see [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) and [Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="3459a-107">For more information on Azure CLI 2.0, see [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) and [Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli).</span></span>
