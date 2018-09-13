---
title: Create SQL Server Availability Group Listener - Azure Virtual Machines | Microsoft Docs
description: Step-by-step instructions for creating a listener for an Always On availability group for SQL Server in Azure Virtual Machines
services: virtual-machines
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: monicar
ms.assetid: d1f291e9-9af2-41ba-9d29-9541e3adcfcf
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 12/28/2016
ms.author: mikeray
ms.openlocfilehash: fe8fcf915e6a9014aaba006f83f6bf80fb03422f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552366"
---
# <a name="configure-an-internal-load-balancer-for-an-always-on-availability-group-in-azure"></a><span data-ttu-id="42b70-103">Configure an internal load balancer for an Always On availability group in Azure</span><span class="sxs-lookup"><span data-stu-id="42b70-103">Configure an internal load balancer for an Always On availability group in Azure</span></span>
<span data-ttu-id="42b70-104">This topic explains how to create an internal load balancer for a SQL Server Always On availability group in Azure virtual machines running in Resource Manager model.</span><span class="sxs-lookup"><span data-stu-id="42b70-104">This topic explains how to create an internal load balancer for a SQL Server Always On availability group in Azure virtual machines running in Resource Manager model.</span></span> <span data-ttu-id="42b70-105">An availability group requires a load balancer when the SQL Server instances are on Azure virtual machines.</span><span class="sxs-lookup"><span data-stu-id="42b70-105">An availability group requires a load balancer when the SQL Server instances are on Azure virtual machines.</span></span> <span data-ttu-id="42b70-106">The load balancer stores the IP address for the availability group listener.</span><span class="sxs-lookup"><span data-stu-id="42b70-106">The load balancer stores the IP address for the availability group listener.</span></span> <span data-ttu-id="42b70-107">If an availability group spans multiple regions, each region needs a load balancer.</span><span class="sxs-lookup"><span data-stu-id="42b70-107">If an availability group spans multiple regions, each region needs a load balancer.</span></span>

<span data-ttu-id="42b70-108">To complete this task, you need to have a SQL Server availability group deployed on Azure virtual machines in Resource Manager model.</span><span class="sxs-lookup"><span data-stu-id="42b70-108">To complete this task, you need to have a SQL Server availability group deployed on Azure virtual machines in Resource Manager model.</span></span> <span data-ttu-id="42b70-109">Both SQL Server virtual machines must belong to the same availability set.</span><span class="sxs-lookup"><span data-stu-id="42b70-109">Both SQL Server virtual machines must belong to the same availability set.</span></span> <span data-ttu-id="42b70-110">You can use the [Microsoft template](virtual-machines-windows-portal-sql-alwayson-availability-groups.md) to automatically create the availability group in Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="42b70-110">You can use the [Microsoft template](virtual-machines-windows-portal-sql-alwayson-availability-groups.md) to automatically create the availability group in Azure Resource Manager.</span></span> <span data-ttu-id="42b70-111">This template automatically creates the internal load balancer for you.</span><span class="sxs-lookup"><span data-stu-id="42b70-111">This template automatically creates the internal load balancer for you.</span></span> 

<span data-ttu-id="42b70-112">If you prefer, you can [manually configure an availability group](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).</span><span class="sxs-lookup"><span data-stu-id="42b70-112">If you prefer, you can [manually configure an availability group](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).</span></span>

<span data-ttu-id="42b70-113">This topic requires that your availability groups are already configured.</span><span class="sxs-lookup"><span data-stu-id="42b70-113">This topic requires that your availability groups are already configured.</span></span>  

<span data-ttu-id="42b70-114">Related topics include:</span><span class="sxs-lookup"><span data-stu-id="42b70-114">Related topics include:</span></span>

* [<span data-ttu-id="42b70-115">Configure Always On Availability Groups in Azure VM (GUI)</span><span class="sxs-lookup"><span data-stu-id="42b70-115">Configure Always On Availability Groups in Azure VM (GUI)</span></span>](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md)   
* [<span data-ttu-id="42b70-116">Configure a VNet-to-VNet connection by using Azure Resource Manager and PowerShell</span><span class="sxs-lookup"><span data-stu-id="42b70-116">Configure a VNet-to-VNet connection by using Azure Resource Manager and PowerShell</span></span>](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md)

<span data-ttu-id="42b70-117">By walking through this document you create and configure a load balancer in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="42b70-117">By walking through this document you create and configure a load balancer in the Azure portal.</span></span> <span data-ttu-id="42b70-118">After that is complete, you will configure the cluster to use the IP address from the load balancer for the availability group listener.</span><span class="sxs-lookup"><span data-stu-id="42b70-118">After that is complete, you will configure the cluster to use the IP address from the load balancer for the availability group listener.</span></span>

## <a name="create-and-configure-the-load-balancer-in-the-azure-portal"></a><span data-ttu-id="42b70-119">Create and configure the load balancer in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="42b70-119">Create and configure the load balancer in the Azure portal</span></span>
<span data-ttu-id="42b70-120">In this portion of the task, do the following steps in the Azure portal:</span><span class="sxs-lookup"><span data-stu-id="42b70-120">In this portion of the task, do the following steps in the Azure portal:</span></span>

1. <span data-ttu-id="42b70-121">Create the load balancer and configure the IP address</span><span class="sxs-lookup"><span data-stu-id="42b70-121">Create the load balancer and configure the IP address</span></span>
2. <span data-ttu-id="42b70-122">Configure the backend pool</span><span class="sxs-lookup"><span data-stu-id="42b70-122">Configure the backend pool</span></span>
3. <span data-ttu-id="42b70-123">Create the probe</span><span class="sxs-lookup"><span data-stu-id="42b70-123">Create the probe</span></span> 
4. <span data-ttu-id="42b70-124">Set the load balancing rules</span><span class="sxs-lookup"><span data-stu-id="42b70-124">Set the load balancing rules</span></span>

> [!NOTE]
> <span data-ttu-id="42b70-125">If the SQL Servers are in different resource groups and regions, you will do all these steps twice, once in each resource group.</span><span class="sxs-lookup"><span data-stu-id="42b70-125">If the SQL Servers are in different resource groups and regions, you will do all these steps twice, once in each resource group.</span></span>
> 
> 

### <a name="1-create-the-load-balancer-and-configure-the-ip-address"></a><span data-ttu-id="42b70-126">1. Create the load balancer and configure the IP address</span><span class="sxs-lookup"><span data-stu-id="42b70-126">1. Create the load balancer and configure the IP address</span></span>
<span data-ttu-id="42b70-127">The first step is to create the load balancer.</span><span class="sxs-lookup"><span data-stu-id="42b70-127">The first step is to create the load balancer.</span></span> <span data-ttu-id="42b70-128">In the Azure portal, open the resource group that contains the SQL Server virtual machines.</span><span class="sxs-lookup"><span data-stu-id="42b70-128">In the Azure portal, open the resource group that contains the SQL Server virtual machines.</span></span> <span data-ttu-id="42b70-129">In the resource group, click **Add**.</span><span class="sxs-lookup"><span data-stu-id="42b70-129">In the resource group, click **Add**.</span></span>

1. <span data-ttu-id="42b70-130">Search for **load balancer**.</span><span class="sxs-lookup"><span data-stu-id="42b70-130">Search for **load balancer**.</span></span> <span data-ttu-id="42b70-131">From the search results select **Load Balancer**, which is published by **Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="42b70-131">From the search results select **Load Balancer**, which is published by **Microsoft**.</span></span>
1. <span data-ttu-id="42b70-132">On the **Load Balancer** blade, click **Create**.</span><span class="sxs-lookup"><span data-stu-id="42b70-132">On the **Load Balancer** blade, click **Create**.</span></span>
1. <span data-ttu-id="42b70-133">On **Create load balancer**, configure the load balancer as follows:</span><span class="sxs-lookup"><span data-stu-id="42b70-133">On **Create load balancer**, configure the load balancer as follows:</span></span>

   | <span data-ttu-id="42b70-134">Setting</span><span class="sxs-lookup"><span data-stu-id="42b70-134">Setting</span></span> | <span data-ttu-id="42b70-135">Value</span><span class="sxs-lookup"><span data-stu-id="42b70-135">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="42b70-136">**Name**</span><span class="sxs-lookup"><span data-stu-id="42b70-136">**Name**</span></span> |<span data-ttu-id="42b70-137">A text name representing the load balancer.</span><span class="sxs-lookup"><span data-stu-id="42b70-137">A text name representing the load balancer.</span></span> <span data-ttu-id="42b70-138">For example, **sqlLB**.</span><span class="sxs-lookup"><span data-stu-id="42b70-138">For example, **sqlLB**.</span></span> |
   | <span data-ttu-id="42b70-139">**Type**</span><span class="sxs-lookup"><span data-stu-id="42b70-139">**Type**</span></span> |<span data-ttu-id="42b70-140">**Internal**</span><span class="sxs-lookup"><span data-stu-id="42b70-140">**Internal**</span></span> |
   | <span data-ttu-id="42b70-141">**Virtual network**</span><span class="sxs-lookup"><span data-stu-id="42b70-141">**Virtual network**</span></span> |<span data-ttu-id="42b70-142">Choose the virtual network that the SQL Servers are in.</span><span class="sxs-lookup"><span data-stu-id="42b70-142">Choose the virtual network that the SQL Servers are in.</span></span> |
   | <span data-ttu-id="42b70-143">**Subnet**</span><span class="sxs-lookup"><span data-stu-id="42b70-143">**Subnet**</span></span> |<span data-ttu-id="42b70-144">Choose the subnet that the SQL Servers are in.</span><span class="sxs-lookup"><span data-stu-id="42b70-144">Choose the subnet that the SQL Servers are in.</span></span> |
   | <span data-ttu-id="42b70-145">**IP address assignment**</span><span class="sxs-lookup"><span data-stu-id="42b70-145">**IP address assignment**</span></span> |<span data-ttu-id="42b70-146">**Static**</span><span class="sxs-lookup"><span data-stu-id="42b70-146">**Static**</span></span> |
   | <span data-ttu-id="42b70-147">**Private IP address**</span><span class="sxs-lookup"><span data-stu-id="42b70-147">**Private IP address**</span></span> |<span data-ttu-id="42b70-148">Specify an available IP address from the subnet.</span><span class="sxs-lookup"><span data-stu-id="42b70-148">Specify an available IP address from the subnet.</span></span> <span data-ttu-id="42b70-149">Use this IP address when you create a listener on the cluster.</span><span class="sxs-lookup"><span data-stu-id="42b70-149">Use this IP address when you create a listener on the cluster.</span></span> <span data-ttu-id="42b70-150">In a PowerShell script later in this article, use this address for the `$ILBIP` variable.</span><span class="sxs-lookup"><span data-stu-id="42b70-150">In a PowerShell script later in this article, use this address for the `$ILBIP` variable.</span></span> |
   | <span data-ttu-id="42b70-151">**Subscription**</span><span class="sxs-lookup"><span data-stu-id="42b70-151">**Subscription**</span></span> |<span data-ttu-id="42b70-152">If you have multiple subscriptions, this field may appear.</span><span class="sxs-lookup"><span data-stu-id="42b70-152">If you have multiple subscriptions, this field may appear.</span></span> <span data-ttu-id="42b70-153">Select the subscription that you want associated with this resource.</span><span class="sxs-lookup"><span data-stu-id="42b70-153">Select the subscription that you want associated with this resource.</span></span> <span data-ttu-id="42b70-154">It is normally the same subscription as all the resources for the availability group.</span><span class="sxs-lookup"><span data-stu-id="42b70-154">It is normally the same subscription as all the resources for the availability group.</span></span> |
   | <span data-ttu-id="42b70-155">**Resource group**</span><span class="sxs-lookup"><span data-stu-id="42b70-155">**Resource group**</span></span> |<span data-ttu-id="42b70-156">Choose the resource group that the SQL Servers are in.</span><span class="sxs-lookup"><span data-stu-id="42b70-156">Choose the resource group that the SQL Servers are in.</span></span> |
   | <span data-ttu-id="42b70-157">**Location**</span><span class="sxs-lookup"><span data-stu-id="42b70-157">**Location**</span></span> |<span data-ttu-id="42b70-158">Choose the Azure location that the SQL Servers are in.</span><span class="sxs-lookup"><span data-stu-id="42b70-158">Choose the Azure location that the SQL Servers are in.</span></span> |

1. <span data-ttu-id="42b70-159">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="42b70-159">Click **Create**.</span></span> 

<span data-ttu-id="42b70-160">Azure creates the load balancer.</span><span class="sxs-lookup"><span data-stu-id="42b70-160">Azure creates the load balancer.</span></span> <span data-ttu-id="42b70-161">The load balancer belongs to a specific network, subnet, resource group, and location.</span><span class="sxs-lookup"><span data-stu-id="42b70-161">The load balancer belongs to a specific network, subnet, resource group, and location.</span></span> <span data-ttu-id="42b70-162">After Azure completes, verify the load balancer settings in Azure.</span><span class="sxs-lookup"><span data-stu-id="42b70-162">After Azure completes, verify the load balancer settings in Azure.</span></span> 

### <a name="2-configure-the-backend-pool"></a><span data-ttu-id="42b70-163">2. Configure the backend pool</span><span class="sxs-lookup"><span data-stu-id="42b70-163">2. Configure the backend pool</span></span>
<span data-ttu-id="42b70-164">The next step is to create a backend address pool.</span><span class="sxs-lookup"><span data-stu-id="42b70-164">The next step is to create a backend address pool.</span></span> <span data-ttu-id="42b70-165">Azure calls the backend address pool *backend pool*.</span><span class="sxs-lookup"><span data-stu-id="42b70-165">Azure calls the backend address pool *backend pool*.</span></span> <span data-ttu-id="42b70-166">In this case, the backend pool is the addresses of the two SQL Servers in your availability group.</span><span class="sxs-lookup"><span data-stu-id="42b70-166">In this case, the backend pool is the addresses of the two SQL Servers in your availability group.</span></span> 

1. <span data-ttu-id="42b70-167">In your resource group, click the load balancer you created.</span><span class="sxs-lookup"><span data-stu-id="42b70-167">In your resource group, click the load balancer you created.</span></span> 
1. <span data-ttu-id="42b70-168">On **Settings**, click **Backend pools**.</span><span class="sxs-lookup"><span data-stu-id="42b70-168">On **Settings**, click **Backend pools**.</span></span>
1. <span data-ttu-id="42b70-169">On **Backend pools**, click **Add** to create a backend address pool.</span><span class="sxs-lookup"><span data-stu-id="42b70-169">On **Backend pools**, click **Add** to create a backend address pool.</span></span> 
1. <span data-ttu-id="42b70-170">On **Add backend pool** under **Name**, type a name for the backend pool.</span><span class="sxs-lookup"><span data-stu-id="42b70-170">On **Add backend pool** under **Name**, type a name for the backend pool.</span></span>
1. <span data-ttu-id="42b70-171">Under **Virtual machines**, click **+ Add a virtual machine**.</span><span class="sxs-lookup"><span data-stu-id="42b70-171">Under **Virtual machines**, click **+ Add a virtual machine**.</span></span> 
1. <span data-ttu-id="42b70-172">Under **Choose virtual machines**, click **Choose an availability set** and specify the availability set that the SQL Server virtual machines belong to.</span><span class="sxs-lookup"><span data-stu-id="42b70-172">Under **Choose virtual machines**, click **Choose an availability set** and specify the availability set that the SQL Server virtual machines belong to.</span></span>
1. <span data-ttu-id="42b70-173">After you have chosen the availability set, click **Choose the virtual machines**.</span><span class="sxs-lookup"><span data-stu-id="42b70-173">After you have chosen the availability set, click **Choose the virtual machines**.</span></span> <span data-ttu-id="42b70-174">Click the two virtual machines that host the SQL Server instances in the availability group.</span><span class="sxs-lookup"><span data-stu-id="42b70-174">Click the two virtual machines that host the SQL Server instances in the availability group.</span></span> <span data-ttu-id="42b70-175">Click **Select**.</span><span class="sxs-lookup"><span data-stu-id="42b70-175">Click **Select**.</span></span> 
1. <span data-ttu-id="42b70-176">Click **OK** to close the blades for **Choose virtual machines**, and **Add backend pool**.</span><span class="sxs-lookup"><span data-stu-id="42b70-176">Click **OK** to close the blades for **Choose virtual machines**, and **Add backend pool**.</span></span> 

<span data-ttu-id="42b70-177">Azure updates the settings for the backend address pool.</span><span class="sxs-lookup"><span data-stu-id="42b70-177">Azure updates the settings for the backend address pool.</span></span> <span data-ttu-id="42b70-178">Now your availability set has a pool of two SQL Servers.</span><span class="sxs-lookup"><span data-stu-id="42b70-178">Now your availability set has a pool of two SQL Servers.</span></span>

### <a name="3-create-a-probe"></a><span data-ttu-id="42b70-179">3. Create a probe</span><span class="sxs-lookup"><span data-stu-id="42b70-179">3. Create a probe</span></span>
<span data-ttu-id="42b70-180">The next step is to create a probe.</span><span class="sxs-lookup"><span data-stu-id="42b70-180">The next step is to create a probe.</span></span> <span data-ttu-id="42b70-181">The probe defines how Azure verifies which of the SQL Servers currently owns the availability group listener.</span><span class="sxs-lookup"><span data-stu-id="42b70-181">The probe defines how Azure verifies which of the SQL Servers currently owns the availability group listener.</span></span> <span data-ttu-id="42b70-182">Azure probes the service based on IP address on a port that you define when you create the probe.</span><span class="sxs-lookup"><span data-stu-id="42b70-182">Azure probes the service based on IP address on a port that you define when you create the probe.</span></span>

1. <span data-ttu-id="42b70-183">On the load balancer **Settings** blade, click **Health probes**.</span><span class="sxs-lookup"><span data-stu-id="42b70-183">On the load balancer **Settings** blade, click **Health probes**.</span></span> 
1. <span data-ttu-id="42b70-184">On the **Health probes** blade, click **Add**.</span><span class="sxs-lookup"><span data-stu-id="42b70-184">On the **Health probes** blade, click **Add**.</span></span>
1. <span data-ttu-id="42b70-185">Configure the probe on the **Add probe** blade.</span><span class="sxs-lookup"><span data-stu-id="42b70-185">Configure the probe on the **Add probe** blade.</span></span> <span data-ttu-id="42b70-186">Use the following values to configure the probe:</span><span class="sxs-lookup"><span data-stu-id="42b70-186">Use the following values to configure the probe:</span></span>

   | <span data-ttu-id="42b70-187">Setting</span><span class="sxs-lookup"><span data-stu-id="42b70-187">Setting</span></span> | <span data-ttu-id="42b70-188">Value</span><span class="sxs-lookup"><span data-stu-id="42b70-188">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="42b70-189">**Name**</span><span class="sxs-lookup"><span data-stu-id="42b70-189">**Name**</span></span> |<span data-ttu-id="42b70-190">A text name representing the probe.</span><span class="sxs-lookup"><span data-stu-id="42b70-190">A text name representing the probe.</span></span> <span data-ttu-id="42b70-191">For example, **SQLAlwaysOnEndPointProbe**.</span><span class="sxs-lookup"><span data-stu-id="42b70-191">For example, **SQLAlwaysOnEndPointProbe**.</span></span> |
   | <span data-ttu-id="42b70-192">**Protocol**</span><span class="sxs-lookup"><span data-stu-id="42b70-192">**Protocol**</span></span> |<span data-ttu-id="42b70-193">**TCP**</span><span class="sxs-lookup"><span data-stu-id="42b70-193">**TCP**</span></span> |
   | <span data-ttu-id="42b70-194">**Port**</span><span class="sxs-lookup"><span data-stu-id="42b70-194">**Port**</span></span> |<span data-ttu-id="42b70-195">You may use any available port.</span><span class="sxs-lookup"><span data-stu-id="42b70-195">You may use any available port.</span></span> <span data-ttu-id="42b70-196">For example, *59999*.</span><span class="sxs-lookup"><span data-stu-id="42b70-196">For example, *59999*.</span></span> |
   | <span data-ttu-id="42b70-197">**Interval**</span><span class="sxs-lookup"><span data-stu-id="42b70-197">**Interval**</span></span> |<span data-ttu-id="42b70-198">*5*</span><span class="sxs-lookup"><span data-stu-id="42b70-198">*5*</span></span> |
   | <span data-ttu-id="42b70-199">**Unhealthy threshold**</span><span class="sxs-lookup"><span data-stu-id="42b70-199">**Unhealthy threshold**</span></span> |<span data-ttu-id="42b70-200">*2*</span><span class="sxs-lookup"><span data-stu-id="42b70-200">*2*</span></span> |

1.  <span data-ttu-id="42b70-201">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="42b70-201">Click **OK**.</span></span> 

> [!NOTE]
> <span data-ttu-id="42b70-202">Make sure that the port you specify is open on the firewall of both SQL Servers.</span><span class="sxs-lookup"><span data-stu-id="42b70-202">Make sure that the port you specify is open on the firewall of both SQL Servers.</span></span> <span data-ttu-id="42b70-203">Both servers require an inbound rule for the TCP port that you use.</span><span class="sxs-lookup"><span data-stu-id="42b70-203">Both servers require an inbound rule for the TCP port that you use.</span></span> <span data-ttu-id="42b70-204">For more information, see [Add or Edit Firewall Rule](http://technet.microsoft.com/library/cc753558.aspx).</span><span class="sxs-lookup"><span data-stu-id="42b70-204">For more information, see [Add or Edit Firewall Rule](http://technet.microsoft.com/library/cc753558.aspx).</span></span> 
> 
> 

<span data-ttu-id="42b70-205">Azure creates the probe.</span><span class="sxs-lookup"><span data-stu-id="42b70-205">Azure creates the probe.</span></span> <span data-ttu-id="42b70-206">Azure uses the probe to test which SQL Server has the listener for the availability group.</span><span class="sxs-lookup"><span data-stu-id="42b70-206">Azure uses the probe to test which SQL Server has the listener for the availability group.</span></span>

### <a name="4-set-the-load-balancing-rules"></a><span data-ttu-id="42b70-207">4. Set the load balancing rules</span><span class="sxs-lookup"><span data-stu-id="42b70-207">4. Set the load balancing rules</span></span>
<span data-ttu-id="42b70-208">Set the load balancing rules.</span><span class="sxs-lookup"><span data-stu-id="42b70-208">Set the load balancing rules.</span></span> <span data-ttu-id="42b70-209">The load balancing rules configure how the load balancer routes traffic to the SQL Servers.</span><span class="sxs-lookup"><span data-stu-id="42b70-209">The load balancing rules configure how the load balancer routes traffic to the SQL Servers.</span></span> <span data-ttu-id="42b70-210">For this load balancer, enable direct server return because only one of the two SQL Servers owns the availability group listener resource at a time.</span><span class="sxs-lookup"><span data-stu-id="42b70-210">For this load balancer, enable direct server return because only one of the two SQL Servers owns the availability group listener resource at a time.</span></span>

1. <span data-ttu-id="42b70-211">On the load balancer **Settings** blade, click **Load balancing rules**.</span><span class="sxs-lookup"><span data-stu-id="42b70-211">On the load balancer **Settings** blade, click **Load balancing rules**.</span></span> 
1. <span data-ttu-id="42b70-212">On the **Load balancing rules** blade, click **Add**.</span><span class="sxs-lookup"><span data-stu-id="42b70-212">On the **Load balancing rules** blade, click **Add**.</span></span>
1. <span data-ttu-id="42b70-213">Use the **Add load balancing rules** blade to configure the load balancing rule.</span><span class="sxs-lookup"><span data-stu-id="42b70-213">Use the **Add load balancing rules** blade to configure the load balancing rule.</span></span> <span data-ttu-id="42b70-214">Use the following settings:</span><span class="sxs-lookup"><span data-stu-id="42b70-214">Use the following settings:</span></span> 

   | <span data-ttu-id="42b70-215">Setting</span><span class="sxs-lookup"><span data-stu-id="42b70-215">Setting</span></span> | <span data-ttu-id="42b70-216">Value</span><span class="sxs-lookup"><span data-stu-id="42b70-216">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="42b70-217">**Name**</span><span class="sxs-lookup"><span data-stu-id="42b70-217">**Name**</span></span> |<span data-ttu-id="42b70-218">A text name representing the load balancing rules.</span><span class="sxs-lookup"><span data-stu-id="42b70-218">A text name representing the load balancing rules.</span></span> <span data-ttu-id="42b70-219">For example, **SQLAlwaysOnEndPointListener**.</span><span class="sxs-lookup"><span data-stu-id="42b70-219">For example, **SQLAlwaysOnEndPointListener**.</span></span> |
   | <span data-ttu-id="42b70-220">**Protocol**</span><span class="sxs-lookup"><span data-stu-id="42b70-220">**Protocol**</span></span> |<span data-ttu-id="42b70-221">**TCP**</span><span class="sxs-lookup"><span data-stu-id="42b70-221">**TCP**</span></span> |
   | <span data-ttu-id="42b70-222">**Port**</span><span class="sxs-lookup"><span data-stu-id="42b70-222">**Port**</span></span> |<span data-ttu-id="42b70-223">*1433*</span><span class="sxs-lookup"><span data-stu-id="42b70-223">*1433*</span></span> |
   | <span data-ttu-id="42b70-224">**Backend Port**</span><span class="sxs-lookup"><span data-stu-id="42b70-224">**Backend Port**</span></span> |<span data-ttu-id="42b70-225">*1433*. This value will be ignored because this rule uses **Floating IP (direct server return)**.</span><span class="sxs-lookup"><span data-stu-id="42b70-225">*1433*. This value will be ignored because this rule uses **Floating IP (direct server return)**.</span></span> |
   | <span data-ttu-id="42b70-226">**Probe**</span><span class="sxs-lookup"><span data-stu-id="42b70-226">**Probe**</span></span> |<span data-ttu-id="42b70-227">Use the name of the probe that you created for this load balancer.</span><span class="sxs-lookup"><span data-stu-id="42b70-227">Use the name of the probe that you created for this load balancer.</span></span> |
   | <span data-ttu-id="42b70-228">**Session persistence**</span><span class="sxs-lookup"><span data-stu-id="42b70-228">**Session persistence**</span></span> |<span data-ttu-id="42b70-229">**None**</span><span class="sxs-lookup"><span data-stu-id="42b70-229">**None**</span></span> |
   | <span data-ttu-id="42b70-230">**Idle timeout (minutes)**</span><span class="sxs-lookup"><span data-stu-id="42b70-230">**Idle timeout (minutes)**</span></span> |<span data-ttu-id="42b70-231">*4*</span><span class="sxs-lookup"><span data-stu-id="42b70-231">*4*</span></span> |
   | <span data-ttu-id="42b70-232">**Floating IP (direct server return)**</span><span class="sxs-lookup"><span data-stu-id="42b70-232">**Floating IP (direct server return)**</span></span> |<span data-ttu-id="42b70-233">**Enabled**</span><span class="sxs-lookup"><span data-stu-id="42b70-233">**Enabled**</span></span> |

   > [!NOTE]
   > <span data-ttu-id="42b70-234">You might have to scroll down on the blade to see all of the settings.</span><span class="sxs-lookup"><span data-stu-id="42b70-234">You might have to scroll down on the blade to see all of the settings.</span></span>
   > 

1. <span data-ttu-id="42b70-235">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="42b70-235">Click **OK**.</span></span> 
1. <span data-ttu-id="42b70-236">Azure configures the load balancing rule.</span><span class="sxs-lookup"><span data-stu-id="42b70-236">Azure configures the load balancing rule.</span></span> <span data-ttu-id="42b70-237">Now the load balancer is configured to route traffic to the SQL Server that hosts the listener for the availability group.</span><span class="sxs-lookup"><span data-stu-id="42b70-237">Now the load balancer is configured to route traffic to the SQL Server that hosts the listener for the availability group.</span></span> 

<span data-ttu-id="42b70-238">At this point, the resource group has a load balancer, connecting to both SQL Server machines.</span><span class="sxs-lookup"><span data-stu-id="42b70-238">At this point, the resource group has a load balancer, connecting to both SQL Server machines.</span></span> <span data-ttu-id="42b70-239">The load balancer also contains an IP address for the SQL Server AlwaysOn availability group listener so that either machine can respond to requests for the availability groups.</span><span class="sxs-lookup"><span data-stu-id="42b70-239">The load balancer also contains an IP address for the SQL Server AlwaysOn availability group listener so that either machine can respond to requests for the availability groups.</span></span>

> [!NOTE]
> <span data-ttu-id="42b70-240">If your SQL Servers are in two separate regions, repeat the steps in the other region.</span><span class="sxs-lookup"><span data-stu-id="42b70-240">If your SQL Servers are in two separate regions, repeat the steps in the other region.</span></span> <span data-ttu-id="42b70-241">Each region requires a load balancer.</span><span class="sxs-lookup"><span data-stu-id="42b70-241">Each region requires a load balancer.</span></span> 
> 
> 

## <a name="configure-the-cluster-to-use-the-load-balancer-ip-address"></a><span data-ttu-id="42b70-242">Configure the cluster to use the load balancer IP address</span><span class="sxs-lookup"><span data-stu-id="42b70-242">Configure the cluster to use the load balancer IP address</span></span>
<span data-ttu-id="42b70-243">The next step is to configure the listener on the cluster, and bring the listener online.</span><span class="sxs-lookup"><span data-stu-id="42b70-243">The next step is to configure the listener on the cluster, and bring the listener online.</span></span> <span data-ttu-id="42b70-244">Do the following steps:</span><span class="sxs-lookup"><span data-stu-id="42b70-244">Do the following steps:</span></span> 

1. <span data-ttu-id="42b70-245">Create the availability group listener on the failover cluster</span><span class="sxs-lookup"><span data-stu-id="42b70-245">Create the availability group listener on the failover cluster</span></span> 
2. <span data-ttu-id="42b70-246">Bring the listener online</span><span class="sxs-lookup"><span data-stu-id="42b70-246">Bring the listener online</span></span>

### <a name="5-create-the-availability-group-listener-on-the-failover-cluster"></a><span data-ttu-id="42b70-247">5. Create the availability group listener on the failover cluster</span><span class="sxs-lookup"><span data-stu-id="42b70-247">5. Create the availability group listener on the failover cluster</span></span>
<span data-ttu-id="42b70-248">In this step, you manually create the availability group listener in Failover Cluster Manager and SQL Server Management Studio (SSMS).</span><span class="sxs-lookup"><span data-stu-id="42b70-248">In this step, you manually create the availability group listener in Failover Cluster Manager and SQL Server Management Studio (SSMS).</span></span>

[!INCLUDE [ag-listener-configure](../../../../includes/virtual-machines-ag-listener-configure.md)]

<!---------------------------
* Use RDP to connect to the Azure virtual machine that hosts the primary replica. 
* Open Failover Cluster Manager.
* Select the **Networks** node, and note the cluster network name. This name will be used in the `$ClusterNetworkName` variable in the PowerShell script.
* Expand the cluster name, and then click **Roles**.
* In the **Roles** pane, right-click the availability group name and then select **Add Resource** > **Client Access Point**.
* In the **Name** box, create a name for this new listener, then click **Next** twice, and then click **Finish**. Do not bring the listener or resource online at this point.
  
  > [!NOTE]
  > The name for the new listener is the network name that applications will use to connect to databases in the SQL Server availability group.
  > 
  > 
* Click the **Resources** tab, then expand the Client Access Point you just created. Right-click the IP resource and click properties. Note the name of the IP address. You will use this name in the `$IPResourceName` variable in the PowerShell script.
* Under **IP Address** click **Static IP Address** and set the static IP address to the same address that you used when you set the load balancer IP address on the Azure portal. Enable NetBIOS for this address and click **OK**. Repeat this step for each IP resource if your solution spans multiple Azure VNets. 
* On the cluster node that currently hosts the primary replica, open an elevated PowerShell ISE and paste the following commands into a new script.
  
        $ClusterNetworkName = "<MyClusterNetworkName>" # the cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher to find the name)
        $IPResourceName = "<IPResourceName>" # the IP Address resource name
        $ILBIP = “<X.X.X.X>” # the IP Address of the Internal Load Balancer (ILB). This is the static IP address for the load balancer you configured in the Azure portal.
  
        Import-Module FailoverClusters
  
        Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"="59999";"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
* Update the variables and run the PowerShell script to configure the IP address and port for the new listener.
  
  > [!NOTE]
  > If your SQL Servers are in separate regions, you need to run the PowerShell script twice. The first time use the cluster network name, cluster IP resource name, and load balancer IP address from the first resource group. The second time use the cluster network name, cluster IP resource name, and load balancer IP address from the second resource group.
  > 
  > 

Now the cluster has an availability group listener resource.

### 2. Bring the listener online
With the availability group listener resource configured, you can bring the listener online so that applications can connect to databases in the availability group with the listener.

* Navigate back to Failover Cluster Manager. Expand **Roles** and then highlight your Availability Group. On the **Resources** tab, right-click the listener name and click **Properties**.
* Click the **Dependencies** tab. If there are multiple resources listed, verify that the IP addresses have OR, not AND, dependencies. Click **OK**.
* Right-click the listener name and click **Bring Online**.
* Once the listener is online, from the **Resources** tab, right-click the availability group and click **Properties**.
* Create a dependency on the listener name resource (not the IP address resources name). Click **OK**.
* Launch SQL Server Management Studio and connect to the primary replica.
* Navigate to **AlwaysOn High Availability** | **Availability Groups** | **Availability Group Listeners**. 
* You should now see the listener name that you created in Failover Cluster Manager. Right-click the listener name and click **Properties**.
* In the **Port** box, specify the port number for the availability group listener by using the $EndpointPort you used earlier (1433 was the default), then click **OK**.

------------------------------->

### <a name="verify-the-configuration-of-the-listener"></a><span data-ttu-id="42b70-249">Verify the configuration of the listener</span><span class="sxs-lookup"><span data-stu-id="42b70-249">Verify the configuration of the listener</span></span>

<span data-ttu-id="42b70-250">If the cluster resources and dependencies are correctly configured, you should be able to see the listener in SQL Server management studios.</span><span class="sxs-lookup"><span data-stu-id="42b70-250">If the cluster resources and dependencies are correctly configured, you should be able to see the listener in SQL Server management studios.</span></span> <span data-ttu-id="42b70-251">Do the following steps to set the listener port:</span><span class="sxs-lookup"><span data-stu-id="42b70-251">Do the following steps to set the listener port:</span></span>

1. <span data-ttu-id="42b70-252">Launch SQL Server Management Studio and connect to the primary replica.</span><span class="sxs-lookup"><span data-stu-id="42b70-252">Launch SQL Server Management Studio and connect to the primary replica.</span></span>
2. <span data-ttu-id="42b70-253">Navigate to **AlwaysOn High Availability** | **Availability Groups** | **Availability Group Listeners**.</span><span class="sxs-lookup"><span data-stu-id="42b70-253">Navigate to **AlwaysOn High Availability** | **Availability Groups** | **Availability Group Listeners**.</span></span> 
1. <span data-ttu-id="42b70-254">You should now see the listener name that you created in Failover Cluster Manager.</span><span class="sxs-lookup"><span data-stu-id="42b70-254">You should now see the listener name that you created in Failover Cluster Manager.</span></span> <span data-ttu-id="42b70-255">Right-click the listener name and click **Properties**.</span><span class="sxs-lookup"><span data-stu-id="42b70-255">Right-click the listener name and click **Properties**.</span></span>
1. <span data-ttu-id="42b70-256">In the **Port** box, specify the port number for the availability group listener by using the $EndpointPort you used earlier (1433 was the default), then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="42b70-256">In the **Port** box, specify the port number for the availability group listener by using the $EndpointPort you used earlier (1433 was the default), then click **OK**.</span></span>

<span data-ttu-id="42b70-257">You now have a SQL Server AlwaysOn availability group in Azure virtual machines running in Resource Manager mode.</span><span class="sxs-lookup"><span data-stu-id="42b70-257">You now have a SQL Server AlwaysOn availability group in Azure virtual machines running in Resource Manager mode.</span></span> 

## <a name="test-the-connection-to-the-listener"></a><span data-ttu-id="42b70-258">Test the connection to the listener</span><span class="sxs-lookup"><span data-stu-id="42b70-258">Test the connection to the listener</span></span>
<span data-ttu-id="42b70-259">To test the connection:</span><span class="sxs-lookup"><span data-stu-id="42b70-259">To test the connection:</span></span>

1. <span data-ttu-id="42b70-260">RDP to a SQL Server that is in the same virtual network, but does not own the replica.</span><span class="sxs-lookup"><span data-stu-id="42b70-260">RDP to a SQL Server that is in the same virtual network, but does not own the replica.</span></span> <span data-ttu-id="42b70-261">This can be the other SQL Server in the cluster.</span><span class="sxs-lookup"><span data-stu-id="42b70-261">This can be the other SQL Server in the cluster.</span></span>
2. <span data-ttu-id="42b70-262">Use **sqlcmd** utility to test the connection.</span><span class="sxs-lookup"><span data-stu-id="42b70-262">Use **sqlcmd** utility to test the connection.</span></span> <span data-ttu-id="42b70-263">For example, the following script establishes a **sqlcmd** connection to the primary replica through the listener with Windows authentication:</span><span class="sxs-lookup"><span data-stu-id="42b70-263">For example, the following script establishes a **sqlcmd** connection to the primary replica through the listener with Windows authentication:</span></span>
   
        sqlcmd -S <listenerName> -E

<span data-ttu-id="42b70-264">The SQLCMD connection automatically connects to whichever instance of SQL Server hosts the primary replica.</span><span class="sxs-lookup"><span data-stu-id="42b70-264">The SQLCMD connection automatically connects to whichever instance of SQL Server hosts the primary replica.</span></span> 

## <a name="guidelines-and-limitations"></a><span data-ttu-id="42b70-265">Guidelines and limitations</span><span class="sxs-lookup"><span data-stu-id="42b70-265">Guidelines and limitations</span></span>
<span data-ttu-id="42b70-266">Note the following guidelines on availability group listener in Azure using internal load balancer:</span><span class="sxs-lookup"><span data-stu-id="42b70-266">Note the following guidelines on availability group listener in Azure using internal load balancer:</span></span>

* <span data-ttu-id="42b70-267">Only one internal availability group listener is supported per cloud service because the listener is configured to the load balancer, and there is only one internal load balancer.</span><span class="sxs-lookup"><span data-stu-id="42b70-267">Only one internal availability group listener is supported per cloud service because the listener is configured to the load balancer, and there is only one internal load balancer.</span></span> <span data-ttu-id="42b70-268">However it is possible to create multiple external listeners.</span><span class="sxs-lookup"><span data-stu-id="42b70-268">However it is possible to create multiple external listeners.</span></span> 
* <span data-ttu-id="42b70-269">With an internal load balancer, you only access the listener from within the same virtual network.</span><span class="sxs-lookup"><span data-stu-id="42b70-269">With an internal load balancer, you only access the listener from within the same virtual network.</span></span>