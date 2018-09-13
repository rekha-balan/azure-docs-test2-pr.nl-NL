---
title: Move a VM (Classic) or Cloud Services role instance to a different subnet - Azure PowerShell | Microsoft Docs
description: Learn how to move VMs (Classic) and Cloud Services role instances to a different subnet using PowerShell.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
ms.assetid: de4135c7-dc5b-4ffa-84cc-1b8364b7b427
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/22/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b094f8338394ef2e84cad3070936d715411326a4
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563931"
---
# <a name="move-a-vm-classic-or-cloud-services-role-instance-to-a-different-subnet-using-powershell"></a><span data-ttu-id="d1097-103">Move a VM (Classic) or Cloud Services role instance to a different subnet using PowerShell</span><span class="sxs-lookup"><span data-stu-id="d1097-103">Move a VM (Classic) or Cloud Services role instance to a different subnet using PowerShell</span></span>
<span data-ttu-id="d1097-104">You can use PowerShell to move your VMs (Classic) from one subnet to another in the same virtual network (VNet).</span><span class="sxs-lookup"><span data-stu-id="d1097-104">You can use PowerShell to move your VMs (Classic) from one subnet to another in the same virtual network (VNet).</span></span> <span data-ttu-id="d1097-105">Role instances can be moved by editing the CSCFG file, rather than using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d1097-105">Role instances can be moved by editing the CSCFG file, rather than using PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="d1097-106">This article explains how to move VMs deployed through the classic deployment model only.</span><span class="sxs-lookup"><span data-stu-id="d1097-106">This article explains how to move VMs deployed through the classic deployment model only.</span></span>
> 
> 

<span data-ttu-id="d1097-107">Why move VMs to another subnet?</span><span class="sxs-lookup"><span data-stu-id="d1097-107">Why move VMs to another subnet?</span></span> <span data-ttu-id="d1097-108">Subnet migration is useful when the older subnet is too small and cannot be expanded due to existing running VMs in that subnet.</span><span class="sxs-lookup"><span data-stu-id="d1097-108">Subnet migration is useful when the older subnet is too small and cannot be expanded due to existing running VMs in that subnet.</span></span> <span data-ttu-id="d1097-109">In that case, you can create a new, larger subnet and migrate the VMs to the new subnet, then after migration is complete, you can delete the old empty subnet.</span><span class="sxs-lookup"><span data-stu-id="d1097-109">In that case, you can create a new, larger subnet and migrate the VMs to the new subnet, then after migration is complete, you can delete the old empty subnet.</span></span>

## <a name="how-to-move-a-vm-to-another-subnet"></a><span data-ttu-id="d1097-110">How to move a VM to another subnet</span><span class="sxs-lookup"><span data-stu-id="d1097-110">How to move a VM to another subnet</span></span>
<span data-ttu-id="d1097-111">To move a VM, run the Set-AzureSubnet PowerShell cmdlet, using the example below as a template.</span><span class="sxs-lookup"><span data-stu-id="d1097-111">To move a VM, run the Set-AzureSubnet PowerShell cmdlet, using the example below as a template.</span></span> <span data-ttu-id="d1097-112">In the example below, we are moving TestVM from its present subnet, to Subnet-2.</span><span class="sxs-lookup"><span data-stu-id="d1097-112">In the example below, we are moving TestVM from its present subnet, to Subnet-2.</span></span> <span data-ttu-id="d1097-113">Be sure to edit the example to reflect your environment.</span><span class="sxs-lookup"><span data-stu-id="d1097-113">Be sure to edit the example to reflect your environment.</span></span> <span data-ttu-id="d1097-114">Note that whenever you run the Update-AzureVM cmdlet as part of a procedure, it will restart your VM as part of the update process.</span><span class="sxs-lookup"><span data-stu-id="d1097-114">Note that whenever you run the Update-AzureVM cmdlet as part of a procedure, it will restart your VM as part of the update process.</span></span>

    Get-AzureVM –ServiceName TestVMCloud –Name TestVM `
    | Set-AzureSubnet –SubnetNames Subnet-2 `
    | Update-AzureVM

<span data-ttu-id="d1097-115">If you specified a static internal private IP for your VM, you'll have to clear that setting before you can move the VM to a new subnet.</span><span class="sxs-lookup"><span data-stu-id="d1097-115">If you specified a static internal private IP for your VM, you'll have to clear that setting before you can move the VM to a new subnet.</span></span> <span data-ttu-id="d1097-116">In that case, use the following:</span><span class="sxs-lookup"><span data-stu-id="d1097-116">In that case, use the following:</span></span>

    Get-AzureVM -ServiceName TestVMCloud -Name TestVM `
    | Remove-AzureStaticVNetIP `
    | Update-AzureVM
    Get-AzureVM -ServiceName TestVMCloud -Name TestVM `
    | Set-AzureSubnet -SubnetNames Subnet-2 `
    | Update-AzureVM

## <a name="to-move-a-role-instance-to-another-subnet"></a><span data-ttu-id="d1097-117">To move a role instance to another subnet</span><span class="sxs-lookup"><span data-stu-id="d1097-117">To move a role instance to another subnet</span></span>
<span data-ttu-id="d1097-118">To move a role instance, edit the CSCFG file.</span><span class="sxs-lookup"><span data-stu-id="d1097-118">To move a role instance, edit the CSCFG file.</span></span> <span data-ttu-id="d1097-119">In the example below, we are moving "Role0" in virtual network *VNETName* from its present subnet to *Subnet-2*.</span><span class="sxs-lookup"><span data-stu-id="d1097-119">In the example below, we are moving "Role0" in virtual network *VNETName* from its present subnet to *Subnet-2*.</span></span> <span data-ttu-id="d1097-120">Because the role instance was already deployed, you'll just change the Subnet name = Subnet-2.</span><span class="sxs-lookup"><span data-stu-id="d1097-120">Because the role instance was already deployed, you'll just change the Subnet name = Subnet-2.</span></span> <span data-ttu-id="d1097-121">Be sure to edit the example to reflect your environment.</span><span class="sxs-lookup"><span data-stu-id="d1097-121">Be sure to edit the example to reflect your environment.</span></span>

    <NetworkConfiguration>
        <VirtualNetworkSite name="VNETName" />
        <AddressAssignments>
           <InstanceAddress roleName="Role0">
                <Subnets><Subnet name="Subnet-2" /></Subnets>
           </InstanceAddress>
        </AddressAssignments>
    </NetworkConfiguration> 
