---
title: Azure PowerShell Script Sample - OMS | Microsoft Docs
description: Azure PowerShell Script Sample - OMS
services: virtual-machines-windows
documentationcenter: virtual-machines
author: cynthn
manager: jeconnoc
editor: tysonn
tags: azure-service-management
ms.assetid: ''
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 12/12/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 5befcb526f6337c05c33bb9b13aa1354ee046248
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44827229"
---
# <a name="create-an-operations-management-suite-monitored-vm-with-powershell"></a><span data-ttu-id="ad27d-103">Create an Operations Management Suite monitored VM with PowerShell</span><span class="sxs-lookup"><span data-stu-id="ad27d-103">Create an Operations Management Suite monitored VM with PowerShell</span></span>

<span data-ttu-id="ad27d-104">This script creates an Azure Virtual Machine, installs the Operations Management Suite (OMS) agent, and enrolls the system with an OMS workspace.</span><span class="sxs-lookup"><span data-stu-id="ad27d-104">This script creates an Azure Virtual Machine, installs the Operations Management Suite (OMS) agent, and enrolls the system with an OMS workspace.</span></span> <span data-ttu-id="ad27d-105">Once the script has run, the virtual machine will be visible in the OMS console.</span><span class="sxs-lookup"><span data-stu-id="ad27d-105">Once the script has run, the virtual machine will be visible in the OMS console.</span></span> <span data-ttu-id="ad27d-106">Also, you need to update the OMS workspace ID and workspace key.</span><span class="sxs-lookup"><span data-stu-id="ad27d-106">Also, you need to update the OMS workspace ID and workspace key.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="ad27d-107">Sample script</span><span class="sxs-lookup"><span data-stu-id="ad27d-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-monitor-oms/create-windows-vm-detailed-oms.ps1 "Create VM OMS")]

## <a name="clean-up-deployment"></a><span data-ttu-id="ad27d-108">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="ad27d-108">Clean up deployment</span></span>

<span data-ttu-id="ad27d-109">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="ad27d-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="ad27d-110">Script explanation</span><span class="sxs-lookup"><span data-stu-id="ad27d-110">Script explanation</span></span>

<span data-ttu-id="ad27d-111">This script uses the following commands to create the deployment.</span><span class="sxs-lookup"><span data-stu-id="ad27d-111">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="ad27d-112">Each item in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="ad27d-112">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="ad27d-113">Command</span><span class="sxs-lookup"><span data-stu-id="ad27d-113">Command</span></span> | <span data-ttu-id="ad27d-114">Notes</span><span class="sxs-lookup"><span data-stu-id="ad27d-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ad27d-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="ad27d-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="ad27d-116">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="ad27d-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="ad27d-117">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="ad27d-117">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="ad27d-118">Creates the virtual machine and connects it to the network card, virtual network, subnet, and network security group.</span><span class="sxs-lookup"><span data-stu-id="ad27d-118">Creates the virtual machine and connects it to the network card, virtual network, subnet, and network security group.</span></span> <span data-ttu-id="ad27d-119">This command also opens port 80 and sets the administrative credentials.</span><span class="sxs-lookup"><span data-stu-id="ad27d-119">This command also opens port 80 and sets the administrative credentials.</span></span> |
| [<span data-ttu-id="ad27d-120">Set-AzureRmVMExtension</span><span class="sxs-lookup"><span data-stu-id="ad27d-120">Set-AzureRmVMExtension</span></span>](/powershell/module/azurerm.compute/set-azurermvmextension) | <span data-ttu-id="ad27d-121">Add a VM extension to the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="ad27d-121">Add a VM extension to the virtual machine.</span></span> <span data-ttu-id="ad27d-122">In this case, the Operations Management Suite agent extension is used to install the OMS agent and enroll the VM in an OMS workspace.</span><span class="sxs-lookup"><span data-stu-id="ad27d-122">In this case, the Operations Management Suite agent extension is used to install the OMS agent and enroll the VM in an OMS workspace.</span></span> |
|[<span data-ttu-id="ad27d-123">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="ad27d-123">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="ad27d-124">Removes a resource group and all resources contained within.</span><span class="sxs-lookup"><span data-stu-id="ad27d-124">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ad27d-125">Next steps</span><span class="sxs-lookup"><span data-stu-id="ad27d-125">Next steps</span></span>

<span data-ttu-id="ad27d-126">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ad27d-126">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="ad27d-127">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ad27d-127">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
