---
title: Azure CLI script - Restore an Azure Database for MySQL server
description: This sample Azure CLI script shows how to restore an Azure Database for MySQL server and its databases to a previous point in time.
services: mysql
author: ajlam
ms.author: andrela
manager: kfile
editor: jasonwhowell
ms.service: mysql
ms.devlang: azure-cli
ms.topic: sample
ms.custom: mvc
ms.date: 02/28/2018
ms.openlocfilehash: 5e4eae95eb881ba685f2668073c556373b2e6c10
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855988"
---
# <a name="restore-an-azure-database-for-mysql-server-using-azure-cli"></a>Restore an Azure Database for MySQL server using Azure CLI
This sample CLI script restores a single Azure Database for MySQL server to a previous point in time.

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

If you choose to run the CLI locally, this article requires Azure CLI version 2.0 or later. Check the version by running `az --version`. See [Install Azure CLI 2.0]( /cli/azure/install-azure-cli) to install or upgrade your version of Azure CLI. 

## <a name="sample-script"></a>Sample script
In this sample script, edit the highlighted lines to update the admin username and password to your own. Replace the subscription ID used in the `az monitor` commands with your own subscription ID.
[!code-azurecli-interactive[main](../../../cli_scripts/mysql/backup-restore-pitr/backup-restore.sh?highlight=18-19 "Restore Azure Database for MySQL.")]

## <a name="clean-up-deployment"></a>Clean up deployment
Use the following command to remove the resource group and all resources associated with it after the script has been run. 
[!code-azurecli-interactive[main](../../../cli_scripts/mysql/backup-restore-pitr/delete-mysql.sh  "Delete the resource group.")]

## <a name="script-explanation"></a>Script explanation
This script uses the commands outlined in the following table:

| **Command** | **Notes** |
|---|---|
| [az group create](/cli/azure/group#az-group-create) | Creates a resource group in which all resources are stored. |
| [az mysql server create](/cli/azure/mysql/server#az-mysql-server-create) | Creates a MySQL server that hosts the databases. |
| [az mysql server restore](/cli/azure/mysql/server#az-mysql-server-restore) | Restore a server from backup. |
| [az group delete](/cli/azure/group#az-group-delete) | Deletes a resource group including all nested resources. |

## <a name="next-steps"></a>Next steps
- Read more information on the Azure CLI: [Azure CLI documentation](/cli/azure).
- Try additional scripts: [Azure CLI samples for Azure Database for MySQL](../sample-scripts-azure-cli.md)
