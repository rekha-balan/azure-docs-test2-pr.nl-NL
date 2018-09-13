---
title: Create a Azure Media Services account - Azure CLI| Microsoft Docs
description: Use the Azure CLI script to create a Azure Media Services account.
services: media-services
documentationcenter: ''
author: Juliako
manager: cfowler
editor: ''
ms.assetid: ''
ms.service: media-services
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/11/2018
ms.author: juliako
ms.openlocfilehash: 0d6d2af598a587cf263612780b419a092ce76d75
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866116"
---
# <a name="cli-example-create-an-azure-media-services-account"></a>CLI example: Create an Azure Media Services account

The Azure CLI script in this topic shows how to create an Azure Media Services account.

[!INCLUDE [cloud-shell-try-it.md](../../../../includes/cloud-shell-try-it.md)]

If you choose to install and use the CLI locally, this article requires that you are running the Azure CLI version 2.0.20 or later. Run `az --version` to find the version. If you need to install or upgrade, see [Install Azure CLI](/cli/azure/install-azure-cli). 

## <a name="example-script"></a>Example script

[!code-azurecli-interactive[main](../../../../cli_scripts/media-services/media-services-create-account/Create-Account.sh "Create Account")]

## <a name="clean-up-deployment"></a>Clean up deployment

Run the following command to remove the resource group and all resources associated with it.

```azurecli-interactive
az group delete --name amsResourceGroup
```

## <a name="script-explanation"></a>Script explanation

This script uses the following commands. Each command in the table links to command-specific documentation.

| Command | Notes |
|---|---|
| [az group create](/cli/azure/group#az-group-create) | Creates a resource group in which all resources are stored. |
| [az storage account create](/cli/azure/storage/account#az-storage-account-create) | Creates a storage account. |
| [az ams account create](https://docs.microsoft.com/cli/azure/ams/account?view=azure-cli-latest#az-ams-account-create) | Creates a Media Services account. |
| [az ams account sp create](https://docs.microsoft.com/cli/azure/ams/account/sp?view=azure-cli-latest#az-ams-account-sp-create) | Creates a service principal with password and configures its access to an Azure Media Services account. 
| [az group delete](/cli/azure/group#az-group-delete) | Deletes a resource group including all nested resources. |


## <a name="next-steps"></a>Next steps

For more examples, see [Azure CLI samples](../cli-samples.md).
