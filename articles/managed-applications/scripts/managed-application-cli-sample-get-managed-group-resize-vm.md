---
title: Azure CLI script sample - Get a managed resource group and resize VMs | Microsoft Docs
description: Azure CLI script sample - Get a managed resource group and resize VMs
services: managed-applications
documentationcenter: na
author: tfitzmac
manager: timlt
ms.service: managed-applications
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/25/2017
ms.author: tomfitz
ms.openlocfilehash: 85d58538e15881308ee1f645f7ddd12ec27c94de
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857128"
---
# <a name="get-resources-in-a-managed-resource-group-and-resize-vms-with-azure-cli"></a>Get resources in a managed resource group and resize VMs with Azure CLI

This script retrieves resources from a managed resource group, and resizes the VMs in that resource group.


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Sample script

[!code-azurecli[main](../../../cli_scripts/managed-applications/get-application/get-application.sh "Get application")]


## <a name="script-explanation"></a>Script explanation

This script uses the following commands to deploy the managed application. Each command in the table links to command-specific documentation.

| Command | Notes |
|---|---|
| [az managedapp list](https://docs.microsoft.com/cli/azure/managedapp#az-managedapp-list) | List managed applications. Provide query values to focus the results. |
| [az resource list](https://docs.microsoft.com/cli/azure/resource#az-resource-list) | List resources. Provide a resource group and query values to focus the result. |
| [az vm resize](https://docs.microsoft.com/cli/azure/vm#az-vm-resize) | Update a virtual machine's size. |


## <a name="next-steps"></a>Next steps

* For an introduction to managed applications, see [Azure Managed Application overview](../overview.md).
* For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).
