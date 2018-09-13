---
title: Azure CLI Script-Scale an elastic pool | Microsoft Docs
description: Azure CLI Script Sample - Scale an elastic database pool
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: ''
ms.service: sql-database
ms.custom: sample
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 04/04/2017
ms.author: janeng
ms.openlocfilehash: b9f08db649839196dfd6dfe8bd95c313d4633e8e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564154"
---
# <a name="scale-an-elastic-pool-in-azure-sql-database-using-the-azure-cli"></a>Scale an elastic pool in Azure SQL Database using the Azure CLI

This sample CLI script creates elastic pools, moves pooled databases, and changes performance levels. 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a>Sample script

[!code-azurecli[main](../../../cli_scripts/sql-database/scale-pool/scale-pool.sh "Move database between pools")]

## <a name="clean-up-deployment"></a>Clean up deployment

After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Script explanation

This script uses the following commands to create a resource group, logical server, SQL Database, and firewall rules. Each command in the table links to command specific documentation.

| Command | Notes |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Creates a resource group in which all resources are stored. |
| [az sql server create](https://docs.microsoft.com/cli/azure/sql/server#create) | Creates a logical server that hosts the SQL Database. |
| [az sql elastic-pools create](https://docs.microsoft.com/cli/azure/sql/elastic-pools#create) | Creates an elastic database pool within the logical server. |
| [az sql db create](https://docs.microsoft.com/cli/azure/sql/db#create) | Creates the SQL Database in the logical server. |
| [az sql elastic-pools update](https://docs.microsoft.com/cli/azure/sql/elastic-pools#update) | Updates an elastic database pool, in this example changes the assigned eDTU. |
| [az group delete](https://docs.microsoft.com/cli/azure/vm/extension#set) | Deletes a resource group including all nested resources. |

## <a name="next-steps"></a>Next steps

For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).

Additional SQL Database CLI script samples can be found in the [Azure SQL Database documentation](../sql-database-cli-samples.md).
