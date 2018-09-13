---
title: Azure CLI Script Sample - Create a Linux VM with OMS monitoring | Microsoft Docs
description: Azure CLI Script Sample - Create a Linux VM with OMS monitoring
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
ms.openlocfilehash: f6d17b6a4f9fd2436430a9d90d65c7840970f42d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554814"
---
# <a name="monitor-a-vm-with-operations-management-suite"></a><span data-ttu-id="25fdc-103">Monitor a VM with Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="25fdc-103">Monitor a VM with Operations Management Suite</span></span>

<span data-ttu-id="25fdc-104">This script creates an Azure Virtual Machine, installs the Operations Management Suite (OMS) agent, and enrolls the system with an OMS workspace.</span><span class="sxs-lookup"><span data-stu-id="25fdc-104">This script creates an Azure Virtual Machine, installs the Operations Management Suite (OMS) agent, and enrolls the system with an OMS workspace.</span></span> <span data-ttu-id="25fdc-105">Once the script has run, the virtual machine will be visible in the OMS console.</span><span class="sxs-lookup"><span data-stu-id="25fdc-105">Once the script has run, the virtual machine will be visible in the OMS console.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="25fdc-106">Sample script</span><span class="sxs-lookup"><span data-stu-id="25fdc-106">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-vm-monitor-oms/create-vm-monitor-oms.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="25fdc-107">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="25fdc-107">Clean up deployment</span></span> 

<span data-ttu-id="25fdc-108">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="25fdc-108">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="25fdc-109">Script explanation</span><span class="sxs-lookup"><span data-stu-id="25fdc-109">Script explanation</span></span>

<span data-ttu-id="25fdc-110">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="25fdc-110">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="25fdc-111">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="25fdc-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="25fdc-112">Command</span><span class="sxs-lookup"><span data-stu-id="25fdc-112">Command</span></span> | <span data-ttu-id="25fdc-113">Notes</span><span class="sxs-lookup"><span data-stu-id="25fdc-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="25fdc-114">az group create</span><span class="sxs-lookup"><span data-stu-id="25fdc-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="25fdc-115">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="25fdc-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="25fdc-116">az vm create</span><span class="sxs-lookup"><span data-stu-id="25fdc-116">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="25fdc-117">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span><span class="sxs-lookup"><span data-stu-id="25fdc-117">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="25fdc-118">This command also specifies the virtual machine image to be used, and administrative credentials.</span><span class="sxs-lookup"><span data-stu-id="25fdc-118">This command also specifies the virtual machine image to be used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="25fdc-119">azure vm extension set</span><span class="sxs-lookup"><span data-stu-id="25fdc-119">azure vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="25fdc-120">Runs a VM extension against a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="25fdc-120">Runs a VM extension against a virtual machine.</span></span> <span data-ttu-id="25fdc-121">In this case, the Operations Management Suite agent extension is used to install the OMS agent and enroll the VM in an OMS workspace.</span><span class="sxs-lookup"><span data-stu-id="25fdc-121">In this case, the Operations Management Suite agent extension is used to install the OMS agent and enroll the VM in an OMS workspace.</span></span> |
| [<span data-ttu-id="25fdc-122">az group delete</span><span class="sxs-lookup"><span data-stu-id="25fdc-122">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="25fdc-123">Deletes a resource group including all nested resources.</span><span class="sxs-lookup"><span data-stu-id="25fdc-123">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="25fdc-124">Next steps</span><span class="sxs-lookup"><span data-stu-id="25fdc-124">Next steps</span></span>

<span data-ttu-id="25fdc-125">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="25fdc-125">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="25fdc-126">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="25fdc-126">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
