---
title: Azure CLI Script Sample - Deploy the LAMP Stack in a Load-Balanced Virutal Machin Scale Set | Microsoft Docs
description: Use a custom script extension to deploy the LAMP Stack in a load=balanced virtual machine scale set on Azure.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: allclark
manager: douge
editor: tysonn
tags: azure-service-management
ms.assetid: ''
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 04/05/2017
ms.author: allclark
ms.openlocfilehash: 81d61eac30752b6d5870102c9a0c551a9159bba7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540917"
---
# <a name="deploy-the-lamp-stack-in-a-load-balanced-virtual-machine-scale-set"></a>Deploy the LAMP stack in a load-balanced virtual machine scale set

This example creates a virtual machine scale set and applies an extension that runs a custom script to deploy the LAMP stack on each virtual machine in the scale set.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a>Sample script

[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-scaleset-php-ansible/build-stack.sh "Create virtual machine scale set with LAMP stack")]

## <a name="connect"></a>Connect

Use this code to see how to connect to your VMs and your scale set.

[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-scaleset-php-ansible/how-to-access.sh "Access the virtual machine scale set")]

## <a name="clean-up-deployment"></a>Clean up deployment 

Run the following command to remove the resource group, the scale set and VMs, and all related resources.

```azurecli
az group delete -n myResourceGroup
```

## <a name="script-explanation"></a>Script explanation

This script uses the following commands to create a resource group, virtual machine, availability set, load balancer, and all related resources. Each command in the table links to command specific documentation.

| Command | Notes |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Creates a resource group in which all resources are stored. |
| [az vmss create](https://docs.microsoft.com/cli/azure/vmss#create) | Creates a virtual machine scale set |
| [az network lb rule create](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | Add a load-balanced endpoint |
| [az vmss extension set](https://docs.microsoft.com/cli/azure/vmss/extension#set) | Create the extension that runs the custom script on deployment of a VM |
| [az vmss update-instances](https://docs.microsoft.com/cli/azure/vmss#update-instances) | Run the custom script on the VM instances that were deployed before the extension was applied to the scale set. |
| [az vmss scale](https://docs.microsoft.com/cli/azure/vmss#scale) | Scale up the scale set by adding more VM instances. The custom script is run on these when they are deployed. |
| [az network public-ip list](https://docs.microsoft.com/cli/azure/network/public-ip#list) | Get the IP addresses of the VMs created by the sample. |
| [az network lb show](https://docs.microsoft.com/cli/azure/network/lb#show) | Get the frontend and backend ports used by the load balancer. |

## <a name="next-steps"></a>Next steps

For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).

Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
