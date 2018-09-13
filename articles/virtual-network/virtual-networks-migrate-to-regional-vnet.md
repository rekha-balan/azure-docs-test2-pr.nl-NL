---
title: Migrate an Azure virtual network from an affinity group to a region | Classic | Microsoft Docs
description: Learn how to migrate a virtual network from an affinity group to a region.
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: 84febcb9-bb8b-4e79-ab91-865ad9de41cb
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.openlocfilehash: c495af3e818758cc5fe99af9b5f07506a16b59ef
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44548868"
---
# <a name="how-to-migrate-a-virtual-network-from-an-affinity-group-to-a-region"></a><span data-ttu-id="ca7a4-103">How to migrate a virtual network from an affinity group to a region</span><span class="sxs-lookup"><span data-stu-id="ca7a4-103">How to migrate a virtual network from an affinity group to a region</span></span>
<span data-ttu-id="ca7a4-104">You can use an affinity group to ensure that resources created within the same affinity group are physically hosted by servers that are close together, enabling these resources to communicate quicker.</span><span class="sxs-lookup"><span data-stu-id="ca7a4-104">You can use an affinity group to ensure that resources created within the same affinity group are physically hosted by servers that are close together, enabling these resources to communicate quicker.</span></span> <span data-ttu-id="ca7a4-105">In the past, affinity groups were a requirement for creating virtual networks (VNets).</span><span class="sxs-lookup"><span data-stu-id="ca7a4-105">In the past, affinity groups were a requirement for creating virtual networks (VNets).</span></span> <span data-ttu-id="ca7a4-106">At that time, the network manager service that managed VNets could only work within a set of physical servers or scale unit.</span><span class="sxs-lookup"><span data-stu-id="ca7a4-106">At that time, the network manager service that managed VNets could only work within a set of physical servers or scale unit.</span></span> <span data-ttu-id="ca7a4-107">Architectural improvements have increased the scope of network management to a region.</span><span class="sxs-lookup"><span data-stu-id="ca7a4-107">Architectural improvements have increased the scope of network management to a region.</span></span>

<span data-ttu-id="ca7a4-108">As a result of these architectural improvements, affinity groups are no longer recommended, or required for virtual networks.</span><span class="sxs-lookup"><span data-stu-id="ca7a4-108">As a result of these architectural improvements, affinity groups are no longer recommended, or required for virtual networks.</span></span> <span data-ttu-id="ca7a4-109">The use of affinity groups for VNets is being replaced by regions.</span><span class="sxs-lookup"><span data-stu-id="ca7a4-109">The use of affinity groups for VNets is being replaced by regions.</span></span> <span data-ttu-id="ca7a4-110">VNets that are associated with regions are called regional VNets.</span><span class="sxs-lookup"><span data-stu-id="ca7a4-110">VNets that are associated with regions are called regional VNets.</span></span>

<span data-ttu-id="ca7a4-111">Additionally, we recommend that you don't use affinity groups in general.</span><span class="sxs-lookup"><span data-stu-id="ca7a4-111">Additionally, we recommend that you don't use affinity groups in general.</span></span> <span data-ttu-id="ca7a4-112">Aside from the VNet requirement, affinity groups were also important to use to ensure resources, such as compute and storage, were placed near each other.</span><span class="sxs-lookup"><span data-stu-id="ca7a4-112">Aside from the VNet requirement, affinity groups were also important to use to ensure resources, such as compute and storage, were placed near each other.</span></span> <span data-ttu-id="ca7a4-113">However, with the current Azure network architecture, these placement requirements are no longer necessary.</span><span class="sxs-lookup"><span data-stu-id="ca7a4-113">However, with the current Azure network architecture, these placement requirements are no longer necessary.</span></span> <span data-ttu-id="ca7a4-114">See [Affinity groups and VMs](#Affinity-groups-and-VMs) for the few remaining specific cases where you may want to use an affinity group.</span><span class="sxs-lookup"><span data-stu-id="ca7a4-114">See [Affinity groups and VMs](#Affinity-groups-and-VMs) for the few remaining specific cases where you may want to use an affinity group.</span></span>

## <a name="creating-and-migrating-to-regional-vnets"></a><span data-ttu-id="ca7a4-115">Creating and migrating to regional VNets</span><span class="sxs-lookup"><span data-stu-id="ca7a4-115">Creating and migrating to regional VNets</span></span>
<span data-ttu-id="ca7a4-116">Going forward, when creating new VNets, use *Region*.</span><span class="sxs-lookup"><span data-stu-id="ca7a4-116">Going forward, when creating new VNets, use *Region*.</span></span> <span data-ttu-id="ca7a4-117">You'll see this as an option in the Management Portal.</span><span class="sxs-lookup"><span data-stu-id="ca7a4-117">You'll see this as an option in the Management Portal.</span></span> <span data-ttu-id="ca7a4-118">Note that in the network configuration file, this shows as *Location*.</span><span class="sxs-lookup"><span data-stu-id="ca7a4-118">Note that in the network configuration file, this shows as *Location*.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ca7a4-119">Although it is still technically possible to create a virtual network that is associated with an affinity group, there is no compelling reason to do so.</span><span class="sxs-lookup"><span data-stu-id="ca7a4-119">Although it is still technically possible to create a virtual network that is associated with an affinity group, there is no compelling reason to do so.</span></span> <span data-ttu-id="ca7a4-120">Many new features, such as Network Security Groups, are only available when using a regional VNet and are not available for virtual networks that are associated with affinity groups.</span><span class="sxs-lookup"><span data-stu-id="ca7a4-120">Many new features, such as Network Security Groups, are only available when using a regional VNet and are not available for virtual networks that are associated with affinity groups.</span></span>
> 
> 

### <a name="about-vnets-currently-associated-with-affinity-groups"></a><span data-ttu-id="ca7a4-121">About VNets currently associated with affinity groups</span><span class="sxs-lookup"><span data-stu-id="ca7a4-121">About VNets currently associated with affinity groups</span></span>
<span data-ttu-id="ca7a4-122">VNets that are currently associated with affinity groups are enabled for migration to regional VNets.</span><span class="sxs-lookup"><span data-stu-id="ca7a4-122">VNets that are currently associated with affinity groups are enabled for migration to regional VNets.</span></span> <span data-ttu-id="ca7a4-123">To migrate to a regional VNet, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="ca7a4-123">To migrate to a regional VNet, follow these steps:</span></span>

1. <span data-ttu-id="ca7a4-124">Export the network configuration file.</span><span class="sxs-lookup"><span data-stu-id="ca7a4-124">Export the network configuration file.</span></span> <span data-ttu-id="ca7a4-125">You can use PowerShell or the Management Portal.</span><span class="sxs-lookup"><span data-stu-id="ca7a4-125">You can use PowerShell or the Management Portal.</span></span> <span data-ttu-id="ca7a4-126">For instructions using the Management Portal, see [Configure your VNet using a Network Configuration File](virtual-networks-using-network-configuration-file.md).</span><span class="sxs-lookup"><span data-stu-id="ca7a4-126">For instructions using the Management Portal, see [Configure your VNet using a Network Configuration File](virtual-networks-using-network-configuration-file.md).</span></span>
2. <span data-ttu-id="ca7a4-127">Edit your network configuration file, replacing the old values with the new values.</span><span class="sxs-lookup"><span data-stu-id="ca7a4-127">Edit your network configuration file, replacing the old values with the new values.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="ca7a4-128">The **Location** is the region that you specified for the affinity group that is associated with your VNet.</span><span class="sxs-lookup"><span data-stu-id="ca7a4-128">The **Location** is the region that you specified for the affinity group that is associated with your VNet.</span></span> <span data-ttu-id="ca7a4-129">For example, if your VNet is associated with an affinity group that is located in West US, when you migrate, your Location must point to West US.</span><span class="sxs-lookup"><span data-stu-id="ca7a4-129">For example, if your VNet is associated with an affinity group that is located in West US, when you migrate, your Location must point to West US.</span></span> 
   > 
   > 
   
    <span data-ttu-id="ca7a4-130">Edit the following lines in your network configuration file, replacing the values with your own:</span><span class="sxs-lookup"><span data-stu-id="ca7a4-130">Edit the following lines in your network configuration file, replacing the values with your own:</span></span> 
   
    <span data-ttu-id="ca7a4-131">**Old value:** \<VirtualNetworkSitename="VNetUSWest" AffinityGroup="VNetDemoAG"\></span><span class="sxs-lookup"><span data-stu-id="ca7a4-131">**Old value:** \<VirtualNetworkSitename="VNetUSWest" AffinityGroup="VNetDemoAG"\></span></span> 
   
    <span data-ttu-id="ca7a4-132">**New value:** \<VirtualNetworkSitename="VNetUSWest" Location="West US"\></span><span class="sxs-lookup"><span data-stu-id="ca7a4-132">**New value:** \<VirtualNetworkSitename="VNetUSWest" Location="West US"\></span></span>
3. <span data-ttu-id="ca7a4-133">Save your changes and [import](virtual-networks-using-network-configuration-file.md) the network configuration to Azure.</span><span class="sxs-lookup"><span data-stu-id="ca7a4-133">Save your changes and [import](virtual-networks-using-network-configuration-file.md) the network configuration to Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="ca7a4-134">This migration does NOT cause any downtime to your services.</span><span class="sxs-lookup"><span data-stu-id="ca7a4-134">This migration does NOT cause any downtime to your services.</span></span>
> 
> 

## <a name="affinity-groups-and-vms"></a><span data-ttu-id="ca7a4-135">Affinity groups and VMs</span><span class="sxs-lookup"><span data-stu-id="ca7a4-135">Affinity groups and VMs</span></span>
<span data-ttu-id="ca7a4-136">As mentioned previously, affinity groups are no longer generally recommended for VMs.</span><span class="sxs-lookup"><span data-stu-id="ca7a4-136">As mentioned previously, affinity groups are no longer generally recommended for VMs.</span></span> <span data-ttu-id="ca7a4-137">You should use an affinity group only when a set of VMs must have the absolute lowest network latency between the VMs.</span><span class="sxs-lookup"><span data-stu-id="ca7a4-137">You should use an affinity group only when a set of VMs must have the absolute lowest network latency between the VMs.</span></span> <span data-ttu-id="ca7a4-138">By placing VMs in an affinity group, the VMs will all be placed in the same compute cluster or scale unit.</span><span class="sxs-lookup"><span data-stu-id="ca7a4-138">By placing VMs in an affinity group, the VMs will all be placed in the same compute cluster or scale unit.</span></span>

<span data-ttu-id="ca7a4-139">It's important to note that using an affinity group can have two, possibly negative, consequences:</span><span class="sxs-lookup"><span data-stu-id="ca7a4-139">It's important to note that using an affinity group can have two, possibly negative, consequences:</span></span>

* <span data-ttu-id="ca7a4-140">The set of VM sizes will be limited to the set of VM sizes offered by the compute scale unit.</span><span class="sxs-lookup"><span data-stu-id="ca7a4-140">The set of VM sizes will be limited to the set of VM sizes offered by the compute scale unit.</span></span>
* <span data-ttu-id="ca7a4-141">There is a higher probability of not being able to allocate a new VM.</span><span class="sxs-lookup"><span data-stu-id="ca7a4-141">There is a higher probability of not being able to allocate a new VM.</span></span> <span data-ttu-id="ca7a4-142">This happens when the specific scale unit for the affinity group is out of capacity.</span><span class="sxs-lookup"><span data-stu-id="ca7a4-142">This happens when the specific scale unit for the affinity group is out of capacity.</span></span>

### <a name="what-to-do-if-you-have-a-vm-in-an-affinity-group"></a><span data-ttu-id="ca7a4-143">What to do if you have a VM in an affinity group</span><span class="sxs-lookup"><span data-stu-id="ca7a4-143">What to do if you have a VM in an affinity group</span></span>
<span data-ttu-id="ca7a4-144">VMs that are currently in an affinity group do not need to be removed from the affinity group.</span><span class="sxs-lookup"><span data-stu-id="ca7a4-144">VMs that are currently in an affinity group do not need to be removed from the affinity group.</span></span>

<span data-ttu-id="ca7a4-145">Once a VM is deployed, it is deployed to a single scale unit.</span><span class="sxs-lookup"><span data-stu-id="ca7a4-145">Once a VM is deployed, it is deployed to a single scale unit.</span></span> <span data-ttu-id="ca7a4-146">Affinity groups can restrict the set of available VM sizes for a new VM deployment, but any existing VM that is deployed is already restricted to the set of VM sizes available in the scale unit in which the VM is deployed.</span><span class="sxs-lookup"><span data-stu-id="ca7a4-146">Affinity groups can restrict the set of available VM sizes for a new VM deployment, but any existing VM that is deployed is already restricted to the set of VM sizes available in the scale unit in which the VM is deployed.</span></span> <span data-ttu-id="ca7a4-147">Because of this, removing a VM from the affinity group will have no effect.</span><span class="sxs-lookup"><span data-stu-id="ca7a4-147">Because of this, removing a VM from the affinity group will have no effect.</span></span>

