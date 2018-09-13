---
title: Azure CLI Script Example - Add an Application in Batch | Microsoft Docs
description: Azure CLI Script Example - Add an Application in Batch
services: batch
documentationcenter: ''
author: dlepow
manager: jeconnoc
editor: ''
ms.assetid: ''
ms.service: batch
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 01/29/2018
ms.author: danlep
ms.openlocfilehash: 7c38ac560a4fd277e2b19999ab0ac81549a5fa2f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44831012"
---
# <a name="cli-example-add-an-application-to-an-azure-batch-account"></a>CLI example: Add an application to an Azure Batch account

This script demonstrates how to add an application for use with an Azure Batch pool or task. To set up an application to add to your Batch account, package your executable, together with any dependencies, into a zip file. 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

If you choose to install and use the CLI locally, this article requires that you are running the Azure CLI version 2.0.20 or later. Run `az --version` to find the version. If you need to install or upgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli). 

## <a name="example-script"></a>Example script

[!code-azurecli-interactive[main](../../../cli_scripts/batch/add-application/add-application.sh "Add Application")]

## <a name="clean-up-deployment"></a>Clean up deployment

Run the following command to remove the resource group and all resources associated with it.

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Script explanation

This script uses the following commands.
Each command in the table links to command-specific documentation.

| Command | Notes |
|---|---|
| [az group create](/cli/azure/group#az-group-create) | Creates a resource group in which all resources are stored. |
| [az storage account create](/cli/azure/storage/account#az-storage-account-create) | Creates a storage account. |
| [az batch account create](/cli/azure/batch/account#az-batch-account-create) | Creates the Batch account. |
| [az batch account login](/cli/azure/batch/account#az-batch-account-login) | Authenticates against the specified Batch account for further CLI interaction.  |
| [az batch application create](/cli/azure/batch/application#az-batch-application-create) | Creates an application.  |
| [az batch application package create](/cli/azure/batch/application/package#az-batch-application-package-create) | Adds an application package to the specified application.  |
| [az batch application set](/cli/azure/batch/application#az-batch-application-set) | Updates properties of an application.  |
| [az group delete](/cli/azure/group#az-group-delete) | Deletes a resource group including all nested resources. |

## <a name="next-steps"></a>Next steps

For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).
