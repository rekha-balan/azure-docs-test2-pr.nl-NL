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
# <a name="monitor-a-vm-with-operations-management-suite"></a><span data-ttu-id="f1be1-103">Monitor a VM with Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="f1be1-103">Monitor a VM with Operations Management Suite</span></span>

<span data-ttu-id="f1be1-104">This script creates an Azure Virtual Machine, installs the Operations Management Suite (OMS) agent, and enrolls the system with an OMS workspace.</span><span class="sxs-lookup"><span data-stu-id="f1be1-104">This script creates an Azure Virtual Machine, installs the Operations Management Suite (OMS) agent, and enrolls the system with an OMS workspace.</span></span> <span data-ttu-id="f1be1-105">Once the script has run, the virtual machine will be visible in the OMS console.</span><span class="sxs-lookup"><span data-stu-id="f1be1-105">Once the script has run, the virtual machine will be visible in the OMS console.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="f1be1-106">Sample script</span><span class="sxs-lookup"><span data-stu-id="f1be1-106">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-vm-monitor-oms/create-windows-vm-monitor-oms.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="f1be1-107">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="f1be1-107">Clean up deployment</span></span> 

<span data-ttu-id="f1be1-108">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="f1be1-108">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="f1be1-109">Script explanation</span><span class="sxs-lookup"><span data-stu-id="f1be1-109">Script explanation</span></span>

<span data-ttu-id="f1be1-110">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="f1be1-110">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="f1be1-111">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="f1be1-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="f1be1-112">Command</span><span class="sxs-lookup"><span data-stu-id="f1be1-112">Command</span></span> | <span data-ttu-id="f1be1-113">Notes</span><span class="sxs-lookup"><span data-stu-id="f1be1-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f1be1-114">az group create</span><span class="sxs-lookup"><span data-stu-id="f1be1-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="f1be1-115">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="f1be1-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="f1be1-116">az vm create</span><span class="sxs-lookup"><span data-stu-id="f1be1-116">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="f1be1-117">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span><span class="sxs-lookup"><span data-stu-id="f1be1-117">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="f1be1-118">This command also specifies the virtual machine image to be used, and administrative credentials.</span><span class="sxs-lookup"><span data-stu-id="f1be1-118">This command also specifies the virtual machine image to be used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="f1be1-119">azure vm extension set</span><span class="sxs-lookup"><span data-stu-id="f1be1-119">azure vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="f1be1-120">Runs a VM extension against a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="f1be1-120">Runs a VM extension against a virtual machine.</span></span> <span data-ttu-id="f1be1-121">In this case, the Operations Management Suite agent extension is used to install the OMS agent and enroll the VM in an OMS workspace.</span><span class="sxs-lookup"><span data-stu-id="f1be1-121">In this case, the Operations Management Suite agent extension is used to install the OMS agent and enroll the VM in an OMS workspace.</span></span> |
| [<span data-ttu-id="f1be1-122">az group delete</span><span class="sxs-lookup"><span data-stu-id="f1be1-122">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="f1be1-123">Deletes a resource group including all nested resources.</span><span class="sxs-lookup"><span data-stu-id="f1be1-123">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f1be1-124">Next steps</span><span class="sxs-lookup"><span data-stu-id="f1be1-124">Next steps</span></span>

<span data-ttu-id="f1be1-125">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f1be1-125">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="f1be1-126">Additional virtual machine CLI script samples can be found in the [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f1be1-126">Additional virtual machine CLI script samples can be found in the [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
