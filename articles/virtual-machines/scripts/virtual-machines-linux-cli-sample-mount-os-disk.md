---
title: Azure CLI Script Sample - Mount operating system disk | Microsoft Docs
description: Azure CLI Script Sample - Mount operating system disk
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: ''
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/27/2017
ms.author: nepeters
ms.openlocfilehash: 08b561f0c6928945c41473e19dcc08e292d5d41e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550845"
---
# <a name="troubleshoot-a-vms-operating-system-disk"></a>Troubleshoot a VMs operating system disk

This script mounts the operating system disk of a failed or problematic virtual machine as a data disk to a second virtual machine. This can be useful when troubleshooting disk issues or recovering data. 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Sample script

[!code-azurecli[main](../../../cli_scripts/virtual-machine/mount-os-disk/mount-os-disk.sh "Quick Create VM")]

## <a name="script-explanation"></a>Script explanation

This script uses the following commands to create a resource group, virtual machine, and all related resources. Each command in the table links to command specific documentation.

| Command | Notes |
|---|---|
| [az vm show](https://docs.microsoft.com/cli/azure/vm#show) | Return a list of virtual machines. In this case, the query option is used to return the virtual machine operating system disk. This value is then added to a variable name ‘uri’. |
| [az vm delete](https://docs.microsoft.com/cli/azure/vm#delete) | Deletes a virtual machine. |
| [az vm create](https://docs.microsoft.com/cli/azure/vm#create) | Creates a virtual machine.  |
| [az vm disk attach](https://docs.microsoft.com/cli/azure/vm/disk#attach) | Attaches a disk to a virtual machine. |
| [az vm list-ip-addresses](https://docs.microsoft.com/cli/azure/vm#list-ip-addresses) | Returns the IP addresses of a virtual machine. |

## <a name="next-steps"></a>Next steps

For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).

Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
