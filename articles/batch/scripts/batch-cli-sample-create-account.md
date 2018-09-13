---
title: Azure CLI Script Sample - Create a Batch account | Microsoft Docs
description: Azure CLI Script Sample - Create a Batch account
services: batch
documentationcenter: ''
author: annatisch
manager: daryls
editor: tysonn
ms.assetid: ''
ms.service: batch
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/20/2017
ms.author: antisch
ms.openlocfilehash: e4ff70c2e741f0f0de693a2997501a446f84bf0a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555213"
---
# <a name="create-a-batch-account-with-the-azure-cli"></a>Create a Batch account with the Azure CLI

This script creates an Azure Batch account and shows how various properties of the account can be queried and updated.

If needed, install the Azure CLI using the instructions found in the [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), and then run `az login` to log into Azure.

## <a name="batch-account-sample-script"></a>Batch account sample script

When you create a Batch account, by default its compute nodes are assigned internally by the Batch service. Allocated compute nodes will be subject to a separate core quota and the account can be authenticated either via Shared Key credentials or an Azure Active Dirctory token.

[!code-azurecli[main](../../../cli_scripts/batch/create-account/create-account.sh "Create Account")]

## <a name="batch-account-using-user-subscription-sample-script"></a>Batch account using user subscription sample script

You can also opt to have Batch create its compute nodes in your own Azure subscription.
Accounts that allocate compute nodes into your subscription must be authenticated via an Azure Active Directory token and the compute nodes allocated will count towards your subscription quota. To create an account in this mode, one must specify a Key Vault reference when creating the account.

[!code-azurecli[main](../../../cli_scripts/batch/create-account/create-account-user-subscription.sh  "Create Account using User Subscription")]

## <a name="clean-up-deployment"></a>Clean up deployment

After you run either of the above sample scripts, run the following command to remove the resource group and all related resources (including Batch accounts, Azure Storage accounts and Azure key vaults).

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Script explanation

This script uses the following commands to create a resource group, Batch account, and all related resources. Each command in the table links to command-specific documentation.

| Command | Notes |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Creates a resource group in which all resources are stored. |
| [az batch account create](https://docs.microsoft.com/cli/azure/batch/account#create) | Creates the Batch account.  |
| [az batch account set](https://docs.microsoft.com/cli/azure/batch/account#set) | Updates properties of the Batch account.  |
| [az batch account show](https://docs.microsoft.com/cli/azure/batch/account#show) | Retrieves details of the specified Batch account.  |
| [az batch account keys list](https://docs.microsoft.com/cli/azure/batch/account/keys#list) | Retrieves the access keys of the specified Batch account.  |
| [az batch account login](https://docs.microsoft.com/cli/azure/batch/account#login) | Authenticates against the specified Batch account for further CLI interaction.  |
| [az storage account create](https://docs.microsoft.com/cli/azure/storage/account#create) | Creates a storage account. |
| [az keyvault create](https://docs.microsoft.com/cli/azure/keyvault#create) | Creates a key vault. |
| [az keyvault set-policy](https://docs.microsoft.com/cli/azure/keyvault#set-policy) | Update the security policy of the specified key vault. |
| [az group delete](https://docs.microsoft.com/cli/azure/group#delete) | Deletes a resource group including all nested resources. |

## <a name="next-steps"></a>Next steps

For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).

Additional Batch CLI script samples can be found in the [Azure Batch CLI documentation](../batch-cli-samples.md).
