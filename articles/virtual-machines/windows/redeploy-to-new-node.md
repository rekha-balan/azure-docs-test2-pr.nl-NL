---
title: Redeploy Windows virtual machines in Azure | Microsoft Docs
description: How to redeploy Windows virtual machines in Azure to mitigate RDP connection issues.
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
tags: azure-resource-manager,top-support-issue
ms.assetid: 0ee456ee-4595-4a14-8916-72c9110fc8bd
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: support-article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 12/16/2016
ms.author: iainfou
ms.openlocfilehash: f09e91521a015891268467a1b8730a6ec835066e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555708"
---
# <a name="redeploy-windows-virtual-machine-to-new-azure-node"></a><span data-ttu-id="2878f-103">Redeploy Windows virtual machine to new Azure node</span><span class="sxs-lookup"><span data-stu-id="2878f-103">Redeploy Windows virtual machine to new Azure node</span></span>
<span data-ttu-id="2878f-104">If you have been facing difficulties troubleshooting Remote Desktop (RDP) connection or application access to Windows-based Azure virtual machine (VM), redeploying the VM may help.</span><span class="sxs-lookup"><span data-stu-id="2878f-104">If you have been facing difficulties troubleshooting Remote Desktop (RDP) connection or application access to Windows-based Azure virtual machine (VM), redeploying the VM may help.</span></span> <span data-ttu-id="2878f-105">When you redeploy a VM, it moves the VM to a new node within the Azure infrastructure and then powers it back on, retaining all your configuration options and associated resources.</span><span class="sxs-lookup"><span data-stu-id="2878f-105">When you redeploy a VM, it moves the VM to a new node within the Azure infrastructure and then powers it back on, retaining all your configuration options and associated resources.</span></span> <span data-ttu-id="2878f-106">This article shows you how to redeploy a VM using Azure PowerShell or the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="2878f-106">This article shows you how to redeploy a VM using Azure PowerShell or the Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="2878f-107">After you redeploy a VM, the temporary disk is lost and dynamic IP addresses associated with virtual network interface are updated.</span><span class="sxs-lookup"><span data-stu-id="2878f-107">After you redeploy a VM, the temporary disk is lost and dynamic IP addresses associated with virtual network interface are updated.</span></span> 


## <a name="using-azure-powershell"></a><span data-ttu-id="2878f-108">Using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="2878f-108">Using Azure PowerShell</span></span>
<span data-ttu-id="2878f-109">Make sure you have the latest Azure PowerShell 1.x installed on your machine.</span><span class="sxs-lookup"><span data-stu-id="2878f-109">Make sure you have the latest Azure PowerShell 1.x installed on your machine.</span></span> <span data-ttu-id="2878f-110">For more information, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="2878f-110">For more information, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>

<span data-ttu-id="2878f-111">The following example deploys the VM named `myVM` in the resource group named `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="2878f-111">The following example deploys the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

```powershell
Set-AzureRmVM -Redeploy -ResourceGroupName "myResourceGroup" -Name "myVM"
```


[!INCLUDE [virtual-machines-common-redeploy-to-new-node](../../../includes/virtual-machines-common-redeploy-to-new-node.md)]

## <a name="next-steps"></a><span data-ttu-id="2878f-112">Next steps</span><span class="sxs-lookup"><span data-stu-id="2878f-112">Next steps</span></span>
<span data-ttu-id="2878f-113">If you are having issues connecting to your VM, you can find specific help on [troubleshooting RDP connections](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) or [detailed RDP troubleshooting steps](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2878f-113">If you are having issues connecting to your VM, you can find specific help on [troubleshooting RDP connections](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) or [detailed RDP troubleshooting steps](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="2878f-114">If you cannot access an application running on your VM, you can also read [application troubleshooting issues](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2878f-114">If you cannot access an application running on your VM, you can also read [application troubleshooting issues](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

