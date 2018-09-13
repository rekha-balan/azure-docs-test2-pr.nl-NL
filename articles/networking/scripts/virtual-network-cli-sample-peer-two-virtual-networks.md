---
title: Azure CLI Script Sample - Peer two virtual networks | Microsoft Docs
description: Azure CLI Script Sample - Peer two virtual networks
services: virtual-network
documentationcenter: virtual-network
author: KumudD
manager: timlt
editor: tysonn
tags: ''
ms.assetid: ''
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: ''
ms.workload: infrastructure
ms.date: 07/07/2017
ms.author: kumud
ms.openlocfilehash: 8ad1e7de85f851b5db6764175bc1136dd19d418d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864671"
---
# <a name="peer-two-virtual-networks"></a>Peer two virtual networks

This script creates and connects two virtual networks in the same region trhough the Azure network. After running the script, you will create a peering between two virtual networks.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


## <a name="sample-script"></a>Sample script

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/peer-two-virtual-networks/peer-two-virtual-networks.sh "Peer two networks")]

## <a name="clean-up-deployment"></a>Clean up deployment 

Run the following command to remove the resource group, VM, and all related resources.

```azurecli
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a>Script explanation

This script uses the following commands to create a resource group, virtual machine, and all related resources. Each command in the table links to command specific documentation.

| Command | Notes |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#az_group_create) | Creates a resource group in which all resources are stored. |
| [az network vnet create](https://docs.microsoft.com/cli/azure/network/vnet#az_network_vnet_create) | Creates an Azure virtual network and subnet. |
| [az network vnet peering create](https://docs.microsoft.com/cli/azure/network/vnet/peering#az_network_vnet_peering_create) | Creates a peering between two virtual networks.  |
| [az group delete](https://docs.microsoft.com/cli/azure/vm/extension#az_vm_extension_set) | Deletes a resource group including all nested resources. |

## <a name="next-steps"></a>Next steps

For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).

Additional networking CLI script samples can be found in the [Azure Networking Overview documentation](../cli-samples.md).
