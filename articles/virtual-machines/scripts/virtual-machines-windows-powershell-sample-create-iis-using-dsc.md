---
title: Azure PowerShell Script Sample - IIS with DSC | Microsoft Docs
description: Azure PowerShell Script Sample - IIS with DSC
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
ms.openlocfilehash: 7269165da046a688dd27aa9f5b325896ad3f65e7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44828282"
---
# <a name="create-an-iis-vm-with-powershell"></a><span data-ttu-id="5c38d-103">Create an IIS VM with PowerShell</span><span class="sxs-lookup"><span data-stu-id="5c38d-103">Create an IIS VM with PowerShell</span></span>

<span data-ttu-id="5c38d-104">This script creates an Azure Virtual Machine running Windows Server 2016, and then uses the Azure Virtual Machine DSC Extension to install IIS.</span><span class="sxs-lookup"><span data-stu-id="5c38d-104">This script creates an Azure Virtual Machine running Windows Server 2016, and then uses the Azure Virtual Machine DSC Extension to install IIS.</span></span> <span data-ttu-id="5c38d-105">After running the script, you can access the default IIS website on the public IP address of the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="5c38d-105">After running the script, you can access the default IIS website on the public IP address of the virtual machine.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="5c38d-106">Sample script</span><span class="sxs-lookup"><span data-stu-id="5c38d-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-dsc/create-windows-vm-iis-dsc.ps1 "Create VM IIS DSC")]

## <a name="clean-up-deployment"></a><span data-ttu-id="5c38d-107">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="5c38d-107">Clean up deployment</span></span>

<span data-ttu-id="5c38d-108">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="5c38d-108">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="5c38d-109">Script explanation</span><span class="sxs-lookup"><span data-stu-id="5c38d-109">Script explanation</span></span>

<span data-ttu-id="5c38d-110">This script uses the following commands to create the deployment.</span><span class="sxs-lookup"><span data-stu-id="5c38d-110">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="5c38d-111">Each item in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="5c38d-111">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="5c38d-112">Command</span><span class="sxs-lookup"><span data-stu-id="5c38d-112">Command</span></span> | <span data-ttu-id="5c38d-113">Notes</span><span class="sxs-lookup"><span data-stu-id="5c38d-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5c38d-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="5c38d-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="5c38d-115">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="5c38d-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="5c38d-116">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="5c38d-116">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="5c38d-117">Creates the virtual machine and connects it to the network card, virtual network, subnet, and network security group.</span><span class="sxs-lookup"><span data-stu-id="5c38d-117">Creates the virtual machine and connects it to the network card, virtual network, subnet, and network security group.</span></span> <span data-ttu-id="5c38d-118">This command also opens port 80 and sets the administrative credentials.</span><span class="sxs-lookup"><span data-stu-id="5c38d-118">This command also opens port 80 and sets the administrative credentials.</span></span> |
| [<span data-ttu-id="5c38d-119">Set-AzureRmVMExtension</span><span class="sxs-lookup"><span data-stu-id="5c38d-119">Set-AzureRmVMExtension</span></span>](/powershell/module/azurerm.compute/set-azurermvmextension) | <span data-ttu-id="5c38d-120">Add a VM extension to the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="5c38d-120">Add a VM extension to the virtual machine.</span></span> <span data-ttu-id="5c38d-121">In this sample, the DSC extension is used to install IIS.</span><span class="sxs-lookup"><span data-stu-id="5c38d-121">In this sample, the DSC extension is used to install IIS.</span></span> |
|[<span data-ttu-id="5c38d-122">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="5c38d-122">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="5c38d-123">Removes a resource group and all resources contained within.</span><span class="sxs-lookup"><span data-stu-id="5c38d-123">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5c38d-124">Next steps</span><span class="sxs-lookup"><span data-stu-id="5c38d-124">Next steps</span></span>

<span data-ttu-id="5c38d-125">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5c38d-125">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="5c38d-126">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5c38d-126">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
