---
title: Azure CLI Script-Create an Azure Cosmos DB Gremlin API account, database, and graph | Microsoft Docs
description: Azure CLI Script Sample - Create an Azure Cosmos DB Gremlin API account, database, and graph
services: cosmos-db
documentationcenter: cosmosdb
author: SnehaGunda
manager: kfile
tags: azure-service-management
ms.service: cosmos-db
ms.component: cosmosdb-graph
ms.custom: mvc
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: cosmosdb
ms.workload: database
ms.date: 05/29/2018
ms.author: sngun
ms.openlocfilehash: a1fc66c82456b86a7ecc2c050db06cc743fa7573
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870267"
---
# <a name="azure-cosmos-db-create-a-gremlin-api-account-using-the-azure-cli"></a>Azure Cosmos DB: Create a Gremlin API account using the Azure CLI

This sample CLI script creates an Azure Cosmos DB Gremlin API account, database, and graph. 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later. Run `az --version` to find the version. If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Sample script

[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/create-cosmosdb-gremlin-account/create-cosmosdb-gremlin-account.sh?highlight=15-35 "Create an Azure Cosmos DB Gremlin API account, database, and graph")]

## <a name="clean-up-deployment"></a>Clean up deployment

After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Script explanation

This script uses the following commands. Each command in the table links to command specific documentation.

| Command | Notes |
|---|---|
| [az group create](/cli/azure/group#az-group-create) | Creates a resource group in which all resources are stored. |
| [az cosmosdb create](/cli/azure/cosmosdb#az-cosmosdb-create) | Creates an Azure Cosmos DB account. |
| [az group delete](/cli/azure/resource#az-resource-delete) | Deletes a resource group including all nested resources. |

## <a name="next-steps"></a>Next steps

For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).

Additional Azure Cosmos DB CLI script samples can be found in the [Azure Cosmos DB CLI documentation](../cli-samples.md).
