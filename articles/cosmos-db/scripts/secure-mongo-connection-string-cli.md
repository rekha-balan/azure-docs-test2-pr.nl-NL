---
title: Azure CLI Script-Get Azure Cosmos DB connection string for MongoDB apps| Microsoft Docs
description: Azure CLI Script Sample - Get Azure Cosmos DB connection string for MongoDB apps
services: cosmos-db
documentationcenter: cosmosdb
author: SnehaGunda
manager: kfile
tags: azure-service-management
ms.service: cosmos-db
ms.component: cosmosdb-mongo
ms.custom: mvc
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: cosmosdb
ms.workload: database
ms.date: 06/02/2017
ms.author: sngun
ms.openlocfilehash: 9c643ebf0dfa2fda0f5a9c53962d4b26ba842940
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870824"
---
# <a name="get-an-azure-cosmos-db-connection-string-for-mongodb-apps-using-the-azure-cli"></a>Get an Azure Cosmos DB connection string for MongoDB apps using the Azure CLI

This sample gets an Azure Cosmos DB connection string for MongoDB apps using the Azure CLI. 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later. Run `az --version` to find the version. If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Sample script

[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/secure-cosmosdb-get-mongodb-connection-string/secure-cosmosdb-get-mongodb-connection-string.sh?highlight=36-39 "Get Azure Cosmos DB connection string for MongoDB apps")]

## <a name="clean-up-deployment"></a>Clean up deployment

After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Script explanation

This script uses the following commands. Each command in the table links to command specific documentation.

| Command | Notes |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#az-group-create) | Creates a resource group in which all resources are stored. |
| [az cosmosdb update](https://docs.microsoft.com/cli/azure/cosmosdb#az-cosmosdb-update) | Updates an Azure Cosmos DB account. |
| [az cosmosdb list-connection-strings](https://docs.microsoft.com/cli/azure/cosmosdb#az-cosmosdb-list-connection-strings) | Gets the connection string for the account.|
| [az group delete](https://docs.microsoft.com/cli/azure/group#az-group-delete) | Deletes a resource group including all nested resources. |

## <a name="next-steps"></a>Next steps

For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).

Additional Azure Cosmos DB CLI script samples can be found in the [Azure Cosmos DB CLI documentation](../cli-samples.md).
