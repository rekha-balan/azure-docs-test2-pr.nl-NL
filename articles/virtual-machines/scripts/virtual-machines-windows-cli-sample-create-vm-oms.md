---
title: Azure CLI Script Sample - Create a Windows Server 2016 VM with OMS monitoring | Microsoft Docs
description: Azure CLI Script Sample - Create a Windows Server 2016 VM with OMS monitoring
services: virtual-machines-Windows
documentationcenter: virtual-machines
author: rickstercdn
manager: timlt
editor: tysonn
tags: ''
ms.assetid: ''
ms.service: virtual-machines-Windows
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-Windows
ms.workload: infrastructure
ms.date: 02/23/2017
ms.author: rclaus
ms.openlocfilehash: 22b371a6339f4940c40de72fe6aeb54dc3e670c2
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556145"
---
# <a name="monitor-a-vm-with-operations-management-suite"></a>Monitor a VM with Operations Management Suite

This script creates an Azure Virtual Machine, installs the Operations Management Suite (OMS) agent, and enrolls the system with an OMS workspace. Once the script has run, the virtual machine will be visible in the OMS console.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Sample script

[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-vm-monitor-oms/create-windows-vm-monitor-oms.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a>Clean up deployment 

Run the following command to remove the resource group, VM, and all related resources.

```azurecli
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a>Script explanation

This script uses the following commands to create a resource group, virtual machine, and all related resources. Each command in the table links to command specific documentation.

| Command | Notes |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Creates a resource group in which all resources are stored. |
| [az vm create](https://docs.microsoft.com/cli/azure/vm#create) | Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG. This command also specifies the virtual machine image to be used, and administrative credentials.  |
| [azure vm extension set](https://docs.microsoft.com/cli/azure/vm/extension#set) | Runs a VM extension against a virtual machine. In this case, the Operations Management Suite agent extension is used to install the OMS agent and enroll the VM in an OMS workspace. |
| [az group delete](https://docs.microsoft.com/cli/azure/vm/extension#set) | Deletes a resource group including all nested resources. |

## <a name="next-steps"></a>Next steps

For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).

Additional virtual machine CLI script samples can be found in the [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
