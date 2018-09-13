---
title: Azure CLI script - Change server configurations
description: This sample CLI script lists all available server configurations and updates the value of innodb_lock_wait_timeout.
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
ms.openlocfilehash: 75b1228df8bc19ced1d8377768c08048e6ef9150
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870352"
---
# <a name="list-and-update-configurations-of-an-azure-database-for-mysql-server-using-azure-cli"></a>List and update configurations of an Azure Database for MySQL server using Azure CLI
This sample CLI script lists all available configuration parameters as well as their allowable values for Azure Database for MySQL server, and sets the *innodb_lock_wait_timeout* to a value that is other than the default one.

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

If you choose to run the CLI locally, this article requires Azure CLI version 2.0 or later. Check the version by running `az --version`. See [Install Azure CLI 2.0]( /cli/azure/install-azure-cli) to install or upgrade your version of Azure CLI. 

## <a name="sample-script"></a>Sample script
In this sample script, edit the highlighted lines to update the admin username and password to your own.
[!code-azurecli-interactive[main](../../../cli_scripts/mysql/change-server-configurations/change-server-configurations.sh?highlight=18-19 "List and update configurations of Azure Database for MySQL.")]

## <a name="clean-up-deployment"></a>Clean up deployment
Use the following command to remove the resource group and all resources associated with it after the script has been run. 
[!code-azurecli-interactive[main](../../../cli_scripts/mysql/change-server-configurations/delete-mysql.sh  "Delete the resource group.")]

## <a name="script-explanation"></a>Script explanation
This script uses the commands outlined in the following table:

| **Command** | **Notes** |
|---|---|
| [az group create](/cli/azure/group#az-group-create) | Creates a resource group in which all resources are stored. |
| [az mysql server create](/cli/azure/mysql/server#az-msql-server-create) | Creates a MySQL server that hosts the databases. |
| [az mysql server configuration list](/cli/azure/mysql/server/configuration#az-msql-server-configuration-list) | List the configurations of an Azure Database for MySQL server. |
| [az mysql server configuration set](/cli/azure/mysql/server/configuration#az-msql-server-configuration-set) | Update the configuration of an Azure Database for MySQL server. |
| [az mysql server configuration show](/cli/azure/mysql/server/configuration#az-msql-server-configuration-show) | Show the configuration of an Azure Database for MySQL server. |
| [az group delete](/cli/azure/group#az-group-delete) | Deletes a resource group including all nested resources. |

## <a name="next-steps"></a>Next steps
- Read more information on the Azure CLI: [Azure CLI documentation](/cli/azure).
- Try additional scripts: [Azure CLI samples for Azure Database for MySQL](../sample-scripts-azure-cli.md)
- For more information on server parameters, see [How To Configure Server Parameters in Azure Database for MySQL](../howto-server-parameters.md).
