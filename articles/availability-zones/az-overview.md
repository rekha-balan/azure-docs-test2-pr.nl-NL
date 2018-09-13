---
title: What are Azure Availability Zones? | Microsoft Docs
description: To create highly available and resilient applications in Azure, Availability Zones provide physically separate locations you can use to run your resources.
services: ''
documentationcenter: ''
author: iainfoulds
manager: jeconnoc
editor: ''
tags: ''
ms.assetid: ''
ms.service: azure
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/27/2018
ms.author: iainfou
ms.custom: mvc I am an ITPro and application developer, and I want to protect (use Availability Zones) my applications and data against data center failure (to build Highly Available applications).
ms.openlocfilehash: 6a4dcc2cd3b196221b881783c79ddb0adaa6f38b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865257"
---
# <a name="what-are-availability-zones-in-azure"></a><span data-ttu-id="6f0be-104">What are Availability Zones in Azure?</span><span class="sxs-lookup"><span data-stu-id="6f0be-104">What are Availability Zones in Azure?</span></span>
<span data-ttu-id="6f0be-105">Availability Zones is a high-availability offering that protects your applications and data from datacenter failures.</span><span class="sxs-lookup"><span data-stu-id="6f0be-105">Availability Zones is a high-availability offering that protects your applications and data from datacenter failures.</span></span> <span data-ttu-id="6f0be-106">Availability Zones are unique physical locations within an Azure region.</span><span class="sxs-lookup"><span data-stu-id="6f0be-106">Availability Zones are unique physical locations within an Azure region.</span></span> <span data-ttu-id="6f0be-107">Each zone is made up of one or more datacenters equipped with independent power, cooling, and networking.</span><span class="sxs-lookup"><span data-stu-id="6f0be-107">Each zone is made up of one or more datacenters equipped with independent power, cooling, and networking.</span></span> <span data-ttu-id="6f0be-108">To ensure resiliency, there’s a minimum of three separate zones in all enabled regions.</span><span class="sxs-lookup"><span data-stu-id="6f0be-108">To ensure resiliency, there’s a minimum of three separate zones in all enabled regions.</span></span> <span data-ttu-id="6f0be-109">The physical separation of Availability Zones within a region protects applications and data from datacenter failures.</span><span class="sxs-lookup"><span data-stu-id="6f0be-109">The physical separation of Availability Zones within a region protects applications and data from datacenter failures.</span></span> <span data-ttu-id="6f0be-110">Zone-redundant services replicate your applications and data across Availability Zones to protect from single-points-of-failure.</span><span class="sxs-lookup"><span data-stu-id="6f0be-110">Zone-redundant services replicate your applications and data across Availability Zones to protect from single-points-of-failure.</span></span> <span data-ttu-id="6f0be-111">With Availability Zones, Azure offers industry best 99.99% VM uptime SLA.</span><span class="sxs-lookup"><span data-stu-id="6f0be-111">With Availability Zones, Azure offers industry best 99.99% VM uptime SLA.</span></span> <span data-ttu-id="6f0be-112">The full [Azure SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) explains the guaranteed availability of Azure as a whole.</span><span class="sxs-lookup"><span data-stu-id="6f0be-112">The full [Azure SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) explains the guaranteed availability of Azure as a whole.</span></span>

<span data-ttu-id="6f0be-113">An Availability Zone in an Azure region is a combination of a fault domain and an update domain.</span><span class="sxs-lookup"><span data-stu-id="6f0be-113">An Availability Zone in an Azure region is a combination of a fault domain and an update domain.</span></span> <span data-ttu-id="6f0be-114">For example, if you create three or more VMs across three zones in an Azure region, your VMs are effectively distributed across three fault domains and three update domains.</span><span class="sxs-lookup"><span data-stu-id="6f0be-114">For example, if you create three or more VMs across three zones in an Azure region, your VMs are effectively distributed across three fault domains and three update domains.</span></span> <span data-ttu-id="6f0be-115">The Azure platform recognizes this distribution across update domains to make sure that VMs in different zones are not updated at the same time.</span><span class="sxs-lookup"><span data-stu-id="6f0be-115">The Azure platform recognizes this distribution across update domains to make sure that VMs in different zones are not updated at the same time.</span></span>

<span data-ttu-id="6f0be-116">Build high-availability into your application architecture by co-locating your compute, storage, networking, and data resources within a zone and replicating in other zones.</span><span class="sxs-lookup"><span data-stu-id="6f0be-116">Build high-availability into your application architecture by co-locating your compute, storage, networking, and data resources within a zone and replicating in other zones.</span></span> <span data-ttu-id="6f0be-117">Azure services that support Availability Zones fall into two categories:</span><span class="sxs-lookup"><span data-stu-id="6f0be-117">Azure services that support Availability Zones fall into two categories:</span></span>

- <span data-ttu-id="6f0be-118">**Zonal services** – you pin the resource to a specific zone (for example, virtual machines, managed disks, IP addresses), or</span><span class="sxs-lookup"><span data-stu-id="6f0be-118">**Zonal services** – you pin the resource to a specific zone (for example, virtual machines, managed disks, IP addresses), or</span></span>
- <span data-ttu-id="6f0be-119">**Zone-redundant services** – platform replicates automatically across zones (for example, zone-redundant storage, SQL Database).</span><span class="sxs-lookup"><span data-stu-id="6f0be-119">**Zone-redundant services** – platform replicates automatically across zones (for example, zone-redundant storage, SQL Database).</span></span>

<span data-ttu-id="6f0be-120">To achieve comprehensive business continuity on Azure, build your application architecture using the combination of Availability Zones with Azure region pairs.</span><span class="sxs-lookup"><span data-stu-id="6f0be-120">To achieve comprehensive business continuity on Azure, build your application architecture using the combination of Availability Zones with Azure region pairs.</span></span> <span data-ttu-id="6f0be-121">You can synchronously replicate your applications and data using Availability Zones within an Azure region for high-availability and asynchronously replicate across Azure regions for disaster recovery protection.</span><span class="sxs-lookup"><span data-stu-id="6f0be-121">You can synchronously replicate your applications and data using Availability Zones within an Azure region for high-availability and asynchronously replicate across Azure regions for disaster recovery protection.</span></span>
 
![conceptual view of one zone going down in a region](./media/az-overview/az-graphic-two.png)

## <a name="regions-that-support-availability-zones"></a><span data-ttu-id="6f0be-123">Regions that support Availability Zones</span><span class="sxs-lookup"><span data-stu-id="6f0be-123">Regions that support Availability Zones</span></span>

- <span data-ttu-id="6f0be-124">Central US</span><span class="sxs-lookup"><span data-stu-id="6f0be-124">Central US</span></span>
- <span data-ttu-id="6f0be-125">France Central</span><span class="sxs-lookup"><span data-stu-id="6f0be-125">France Central</span></span>
- <span data-ttu-id="6f0be-126">East US 2 (Preview)</span><span class="sxs-lookup"><span data-stu-id="6f0be-126">East US 2 (Preview)</span></span>
- <span data-ttu-id="6f0be-127">West Europe</span><span class="sxs-lookup"><span data-stu-id="6f0be-127">West Europe</span></span>
- <span data-ttu-id="6f0be-128">Southeast Asia (Preview)</span><span class="sxs-lookup"><span data-stu-id="6f0be-128">Southeast Asia (Preview)</span></span>


## <a name="services-that-support-availability-zones"></a><span data-ttu-id="6f0be-129">Services that support Availability Zones</span><span class="sxs-lookup"><span data-stu-id="6f0be-129">Services that support Availability Zones</span></span>
<span data-ttu-id="6f0be-130">The Azure services that support Availability Zones are:</span><span class="sxs-lookup"><span data-stu-id="6f0be-130">The Azure services that support Availability Zones are:</span></span>

- <span data-ttu-id="6f0be-131">Linux Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="6f0be-131">Linux Virtual Machines</span></span>
- <span data-ttu-id="6f0be-132">Windows Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="6f0be-132">Windows Virtual Machines</span></span>
- <span data-ttu-id="6f0be-133">Virtual Machine Scale Sets</span><span class="sxs-lookup"><span data-stu-id="6f0be-133">Virtual Machine Scale Sets</span></span>
- <span data-ttu-id="6f0be-134">Managed Disks</span><span class="sxs-lookup"><span data-stu-id="6f0be-134">Managed Disks</span></span>
- <span data-ttu-id="6f0be-135">Load Balancer</span><span class="sxs-lookup"><span data-stu-id="6f0be-135">Load Balancer</span></span>
- <span data-ttu-id="6f0be-136">Public IP address</span><span class="sxs-lookup"><span data-stu-id="6f0be-136">Public IP address</span></span>
- <span data-ttu-id="6f0be-137">Zone-redundant storage</span><span class="sxs-lookup"><span data-stu-id="6f0be-137">Zone-redundant storage</span></span>
- <span data-ttu-id="6f0be-138">SQL Database</span><span class="sxs-lookup"><span data-stu-id="6f0be-138">SQL Database</span></span>
- <span data-ttu-id="6f0be-139">Event Hubs</span><span class="sxs-lookup"><span data-stu-id="6f0be-139">Event Hubs</span></span>
- <span data-ttu-id="6f0be-140">Service Bus</span><span class="sxs-lookup"><span data-stu-id="6f0be-140">Service Bus</span></span>
- <span data-ttu-id="6f0be-141">VPN Gateway</span><span class="sxs-lookup"><span data-stu-id="6f0be-141">VPN Gateway</span></span>
- <span data-ttu-id="6f0be-142">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="6f0be-142">ExpressRoute</span></span>


## <a name="pricing"></a><span data-ttu-id="6f0be-143">Pricing</span><span class="sxs-lookup"><span data-stu-id="6f0be-143">Pricing</span></span>
<span data-ttu-id="6f0be-144">There is no additional cost for virtual machines deployed in an Availability Zone.</span><span class="sxs-lookup"><span data-stu-id="6f0be-144">There is no additional cost for virtual machines deployed in an Availability Zone.</span></span> <span data-ttu-id="6f0be-145">99.99% VM uptime SLA is offered when two or more VMs are deployed across two or more Availability Zones within an Azure region.</span><span class="sxs-lookup"><span data-stu-id="6f0be-145">99.99% VM uptime SLA is offered when two or more VMs are deployed across two or more Availability Zones within an Azure region.</span></span> <span data-ttu-id="6f0be-146">There will be additional inter-Availability Zone VM-to-VM data transfer charges.</span><span class="sxs-lookup"><span data-stu-id="6f0be-146">There will be additional inter-Availability Zone VM-to-VM data transfer charges.</span></span> <span data-ttu-id="6f0be-147">For more information, review the [Bandwidth pricing](https://azure.microsoft.com/pricing/details/bandwidth/) page.</span><span class="sxs-lookup"><span data-stu-id="6f0be-147">For more information, review the [Bandwidth pricing](https://azure.microsoft.com/pricing/details/bandwidth/) page.</span></span>


## <a name="get-started-with-availability-zones"></a><span data-ttu-id="6f0be-148">Get started with Availability Zones</span><span class="sxs-lookup"><span data-stu-id="6f0be-148">Get started with Availability Zones</span></span>
- [<span data-ttu-id="6f0be-149">Create a virtual machine</span><span class="sxs-lookup"><span data-stu-id="6f0be-149">Create a virtual machine</span></span>](../virtual-machines/windows/create-portal-availability-zone.md)
- [<span data-ttu-id="6f0be-150">Add a Managed Disk using PowerShell</span><span class="sxs-lookup"><span data-stu-id="6f0be-150">Add a Managed Disk using PowerShell</span></span>](../virtual-machines/windows/attach-disk-ps.md#add-an-empty-data-disk-to-a-virtual-machine)
- [<span data-ttu-id="6f0be-151">Create a zone redundant virtual machine scale set</span><span class="sxs-lookup"><span data-stu-id="6f0be-151">Create a zone redundant virtual machine scale set</span></span>](../virtual-machine-scale-sets/virtual-machine-scale-sets-use-availability-zones.md)
- [<span data-ttu-id="6f0be-152">Load balance VMs across zones using a Standard Load Balancer with a zone-redundant frontend</span><span class="sxs-lookup"><span data-stu-id="6f0be-152">Load balance VMs across zones using a Standard Load Balancer with a zone-redundant frontend</span></span>](../load-balancer/load-balancer-standard-public-zone-redundant-cli.md)
- [<span data-ttu-id="6f0be-153">Load balance VMs within a zone using a Standard Load Balancer with a zonal frontend</span><span class="sxs-lookup"><span data-stu-id="6f0be-153">Load balance VMs within a zone using a Standard Load Balancer with a zonal frontend</span></span>](../load-balancer/load-balancer-standard-public-zonal-cli.md)
- [<span data-ttu-id="6f0be-154">Zone-redundant storage</span><span class="sxs-lookup"><span data-stu-id="6f0be-154">Zone-redundant storage</span></span>](../storage/common/storage-redundancy-zrs.md)
- [<span data-ttu-id="6f0be-155">SQL Database</span><span class="sxs-lookup"><span data-stu-id="6f0be-155">SQL Database</span></span>](../sql-database/sql-database-high-availability.md#zone-redundant-configuration-preview)
- [<span data-ttu-id="6f0be-156">Event Hubs geo-disaster recovery</span><span class="sxs-lookup"><span data-stu-id="6f0be-156">Event Hubs geo-disaster recovery</span></span>](../event-hubs/event-hubs-geo-dr.md#availability-zones-preview)
- [<span data-ttu-id="6f0be-157">Service Bus geo-disaster recovery</span><span class="sxs-lookup"><span data-stu-id="6f0be-157">Service Bus geo-disaster recovery</span></span>](../service-bus-messaging/service-bus-geo-dr.md#availability-zones-preview)
- [<span data-ttu-id="6f0be-158">Create a zone-redundant virtual network gateway</span><span class="sxs-lookup"><span data-stu-id="6f0be-158">Create a zone-redundant virtual network gateway</span></span>](../vpn-gateway/create-zone-redundant-vnet-gateway.md)


## <a name="next-steps"></a><span data-ttu-id="6f0be-159">Next steps</span><span class="sxs-lookup"><span data-stu-id="6f0be-159">Next steps</span></span>
- [<span data-ttu-id="6f0be-160">Quickstart templates</span><span class="sxs-lookup"><span data-stu-id="6f0be-160">Quickstart templates</span></span>](http://aka.ms/azqs)
