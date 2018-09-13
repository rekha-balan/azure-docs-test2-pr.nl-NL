---
title: Azure CLI Script Sample - Manage web traffic | Microsoft Docs
description: Azure CLI Script Sample - Manage web traffic with an application gateway and a virtual machine scale set.
services: application-gateway
documentationcenter: networking
author: vhorne
manager: jpconnock
editor: tysonn
tags: azure-resource-manager
ms.service: application-gateway
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 01/29/2018
ms.author: victorh
ms.custom: mvc
ms.openlocfilehash: a2046c6d4bbaf91db6a6c4de2023717eaf13fadb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868733"
---
# <a name="manage-web-traffic-using-the-azure-cli"></a>Manage web traffic using the Azure CLI

This script creates an application gateway that uses a virtual machine scale set for backend servers. The application gateway can then be configured to manage web traffic. After running the script, you can test the application gateway using its public IP address.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Sample script

[!code-azurecli-interactive[main](../../../cli_scripts/application-gateway/create-vmss/create-vmss.sh "Create application gateway")]

## <a name="clean-up-deployment"></a>Clean up deployment 

Run the following command to remove the resource group, application gateway, and all related resources.

```azurecli-interactive 
az group delete --name myResourceGroupAG --yes
```

## <a name="script-explanation"></a>Script explanation

This script uses the following commands to create the deployment. Each item in the table links to command specific documentation.

| Command | Notes |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#az-group-create) | Creates a resource group in which all resources are stored. |
| [az network vnet create](https://docs.microsoft.com/cli/azure/network/vnet#az-net) | Creates a virtual network. |
| [az network vnet subnet create](https://docs.microsoft.com/cli/azure/network/vnet/subnet#az-network_vnet_subnet_create) | Creates a subnet in a virtual network. |
| [az network public-ip create](https://docs.microsoft.com/en-us/cli/azure/network/public-ip?view=azure-cli-latest) | Creates the public IP address for the application gateway. |
| [az network application-gateway create](https://docs.microsoft.com/en-us/cli/azure/network/application-gateway?view=azure-cli-latest) | Create an application gateway. |
| [az vmss create](https://docs.microsoft.com/cli/azure/vmss#az-vmss-create) | Creates a virtual machine scale set. |
| [az network public-ip show](https://docs.microsoft.com/cli/azure/network/public-ip#az-network_public_ip_show) | Gets the public IP address of the application gateway. |

## <a name="next-steps"></a>Next steps

For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).

Additional application gateway CLI script samples can be found in the [Azure Windows VM documentation](../cli-samples.md).
