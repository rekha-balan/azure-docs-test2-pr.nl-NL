---
title: Azure CLI Script Sample - Create a Windows Server 2016 VM with OMS monitoring | Microsoft Docs
description: Azure CLI Script Sample - Create a Windows Server 2016 VM with OMS monitoring
services: virtual-machines-Windows
documentationcenter: virtual-machines
author: rickstercdn
manager: jeconnoc
editor: tysonn
tags: ''
ms.assetid: ''
ms.service: virtual-machines-Windows
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-Windows
ms.workload: infrastructure
ms.date: 02/23/2017
ms.author: rclaus
ms.custom: mvc
ms.openlocfilehash: 05ecaa856cf2c513b48f0ba0f170dfb3bbf31e75
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44776327"
---
# <a name="monitor-a-vm-with-operations-management-suite"></a><span data-ttu-id="1b024-103">Monitor a VM with Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="1b024-103">Monitor a VM with Operations Management Suite</span></span>

<span data-ttu-id="1b024-104">This script creates an Azure Virtual Machine, installs the Operations Management Suite (OMS) agent, and enrolls the system with an OMS workspace.</span><span class="sxs-lookup"><span data-stu-id="1b024-104">This script creates an Azure Virtual Machine, installs the Operations Management Suite (OMS) agent, and enrolls the system with an OMS workspace.</span></span> <span data-ttu-id="1b024-105">Once the script has run, the virtual machine will be visible in the OMS console.</span><span class="sxs-lookup"><span data-stu-id="1b024-105">Once the script has run, the virtual machine will be visible in the OMS console.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="1b024-106">Sample script</span><span class="sxs-lookup"><span data-stu-id="1b024-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-monitor-oms/create-windows-vm-monitor-oms.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="1b024-107">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="1b024-107">Clean up deployment</span></span> 

<span data-ttu-id="1b024-108">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="1b024-108">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="1b024-109">Script explanation</span><span class="sxs-lookup"><span data-stu-id="1b024-109">Script explanation</span></span>

<span data-ttu-id="1b024-110">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="1b024-110">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="1b024-111">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="1b024-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="1b024-112">Command</span><span class="sxs-lookup"><span data-stu-id="1b024-112">Command</span></span> | <span data-ttu-id="1b024-113">Notes</span><span class="sxs-lookup"><span data-stu-id="1b024-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="1b024-114">az group create</span><span class="sxs-lookup"><span data-stu-id="1b024-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#az_group_create) | <span data-ttu-id="1b024-115">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="1b024-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="1b024-116">az vm create</span><span class="sxs-lookup"><span data-stu-id="1b024-116">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#az_vm_create) | <span data-ttu-id="1b024-117">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span><span class="sxs-lookup"><span data-stu-id="1b024-117">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="1b024-118">This command also specifies the virtual machine image to be used, and administrative credentials.</span><span class="sxs-lookup"><span data-stu-id="1b024-118">This command also specifies the virtual machine image to be used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="1b024-119">azure vm extension set</span><span class="sxs-lookup"><span data-stu-id="1b024-119">azure vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#az_vm_extension_set) | <span data-ttu-id="1b024-120">Runs a VM extension against a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="1b024-120">Runs a VM extension against a virtual machine.</span></span> <span data-ttu-id="1b024-121">In this case, the Operations Management Suite agent extension is used to install the OMS agent and enroll the VM in an OMS workspace.</span><span class="sxs-lookup"><span data-stu-id="1b024-121">In this case, the Operations Management Suite agent extension is used to install the OMS agent and enroll the VM in an OMS workspace.</span></span> |
| [<span data-ttu-id="1b024-122">az group delete</span><span class="sxs-lookup"><span data-stu-id="1b024-122">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#az_vm_extension_set) | <span data-ttu-id="1b024-123">Deletes a resource group including all nested resources.</span><span class="sxs-lookup"><span data-stu-id="1b024-123">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="1b024-124">Next steps</span><span class="sxs-lookup"><span data-stu-id="1b024-124">Next steps</span></span>

<span data-ttu-id="1b024-125">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span><span class="sxs-lookup"><span data-stu-id="1b024-125">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span></span>

<span data-ttu-id="1b024-126">Additional virtual machine CLI script samples can be found in the [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1b024-126">Additional virtual machine CLI script samples can be found in the [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
