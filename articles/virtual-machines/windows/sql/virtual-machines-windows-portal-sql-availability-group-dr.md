---
title: SQL Server Availability Groups - Azure Virtual Machines - Disaster Recovery | Microsoft Docs
description: This article explains how to configure a SQL Server availability group on Azure virtual machines with a replica in a different region.
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: craigg
editor: monicar
tags: azure-service-management
ms.assetid: 388c464e-a16e-4c9d-a0d5-bb7cf5974689
ms.service: virtual-machines-sql
ms.devlang: na
ms.custom: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/02/2017
ms.author: mikeray
ms.openlocfilehash: 84fa2e051c46e178e3e72709886babc8c3db7b9d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44809964"
---
# <a name="configure-an-always-on-availability-group-on-azure-virtual-machines-in-different-regions"></a><span data-ttu-id="e8c9a-103">Configure an Always On availability group on Azure virtual machines in different regions</span><span class="sxs-lookup"><span data-stu-id="e8c9a-103">Configure an Always On availability group on Azure virtual machines in different regions</span></span>

<span data-ttu-id="e8c9a-104">This article explains how to configure a SQL Server Always On availability group replica on Azure virtual machines in a remote Azure location.</span><span class="sxs-lookup"><span data-stu-id="e8c9a-104">This article explains how to configure a SQL Server Always On availability group replica on Azure virtual machines in a remote Azure location.</span></span> <span data-ttu-id="e8c9a-105">Use this configuration to support disaster recovery.</span><span class="sxs-lookup"><span data-stu-id="e8c9a-105">Use this configuration to support disaster recovery.</span></span>

<span data-ttu-id="e8c9a-106">This article applies to Azure Virtual Machines in Resource Manager mode.</span><span class="sxs-lookup"><span data-stu-id="e8c9a-106">This article applies to Azure Virtual Machines in Resource Manager mode.</span></span>

<span data-ttu-id="e8c9a-107">The following image shows a common deployment of an availability group on Azure virtual machines:</span><span class="sxs-lookup"><span data-stu-id="e8c9a-107">The following image shows a common deployment of an availability group on Azure virtual machines:</span></span>

   ![Availability Group](./media/virtual-machines-windows-portal-sql-availability-group-dr/00-availability-group-basic.png)

<span data-ttu-id="e8c9a-109">In this deployment, all virtual machines are in one Azure region.</span><span class="sxs-lookup"><span data-stu-id="e8c9a-109">In this deployment, all virtual machines are in one Azure region.</span></span> <span data-ttu-id="e8c9a-110">The availability group replicas can have synchronous commit with automatic failover on SQL-1 and SQL-2.</span><span class="sxs-lookup"><span data-stu-id="e8c9a-110">The availability group replicas can have synchronous commit with automatic failover on SQL-1 and SQL-2.</span></span> <span data-ttu-id="e8c9a-111">To build this architecture, see [Availability Group template or tutorial](virtual-machines-windows-portal-sql-availability-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e8c9a-111">To build this architecture, see [Availability Group template or tutorial](virtual-machines-windows-portal-sql-availability-group-overview.md).</span></span>

<span data-ttu-id="e8c9a-112">This architecture is vulnerable to downtime if the Azure region becomes inaccessible.</span><span class="sxs-lookup"><span data-stu-id="e8c9a-112">This architecture is vulnerable to downtime if the Azure region becomes inaccessible.</span></span> <span data-ttu-id="e8c9a-113">To overcome this vulnerability, add a replica in a different Azure region.</span><span class="sxs-lookup"><span data-stu-id="e8c9a-113">To overcome this vulnerability, add a replica in a different Azure region.</span></span> <span data-ttu-id="e8c9a-114">The following diagram shows how the new architecture would look:</span><span class="sxs-lookup"><span data-stu-id="e8c9a-114">The following diagram shows how the new architecture would look:</span></span>

   ![Availability Group DR](./media/virtual-machines-windows-portal-sql-availability-group-dr/00-availability-group-basic-dr.png)

<span data-ttu-id="e8c9a-116">The preceding diagram shows a new virtual machine called SQL-3.</span><span class="sxs-lookup"><span data-stu-id="e8c9a-116">The preceding diagram shows a new virtual machine called SQL-3.</span></span> <span data-ttu-id="e8c9a-117">SQL-3 is in a different Azure region.</span><span class="sxs-lookup"><span data-stu-id="e8c9a-117">SQL-3 is in a different Azure region.</span></span> <span data-ttu-id="e8c9a-118">SQL-3 is added to the Windows Server Failover Cluster.</span><span class="sxs-lookup"><span data-stu-id="e8c9a-118">SQL-3 is added to the Windows Server Failover Cluster.</span></span> <span data-ttu-id="e8c9a-119">SQL-3 can host an availability group replica.</span><span class="sxs-lookup"><span data-stu-id="e8c9a-119">SQL-3 can host an availability group replica.</span></span> <span data-ttu-id="e8c9a-120">Finally, notice that the Azure region for SQL-3 has a new Azure load balancer.</span><span class="sxs-lookup"><span data-stu-id="e8c9a-120">Finally, notice that the Azure region for SQL-3 has a new Azure load balancer.</span></span>

>[!NOTE]
> <span data-ttu-id="e8c9a-121">An Azure availability set is required when more than one virtual machine is in the same region.</span><span class="sxs-lookup"><span data-stu-id="e8c9a-121">An Azure availability set is required when more than one virtual machine is in the same region.</span></span> <span data-ttu-id="e8c9a-122">If only one virtual machine is in the region, then the availability set is not required.</span><span class="sxs-lookup"><span data-stu-id="e8c9a-122">If only one virtual machine is in the region, then the availability set is not required.</span></span> <span data-ttu-id="e8c9a-123">You can only place a virtual machine in an availability set at creation time.</span><span class="sxs-lookup"><span data-stu-id="e8c9a-123">You can only place a virtual machine in an availability set at creation time.</span></span> <span data-ttu-id="e8c9a-124">If the virtual machine is already in an availability set, you can add a virtual machine for an additional replica later.</span><span class="sxs-lookup"><span data-stu-id="e8c9a-124">If the virtual machine is already in an availability set, you can add a virtual machine for an additional replica later.</span></span>

<span data-ttu-id="e8c9a-125">In this architecture, the replica in the remote region is normally configured with asynchronous commit availability mode and manual failover mode.</span><span class="sxs-lookup"><span data-stu-id="e8c9a-125">In this architecture, the replica in the remote region is normally configured with asynchronous commit availability mode and manual failover mode.</span></span>

<span data-ttu-id="e8c9a-126">When availability group replicas are on Azure virtual machines in different Azure regions, each region requires:</span><span class="sxs-lookup"><span data-stu-id="e8c9a-126">When availability group replicas are on Azure virtual machines in different Azure regions, each region requires:</span></span>

* <span data-ttu-id="e8c9a-127">A virtual network gateway</span><span class="sxs-lookup"><span data-stu-id="e8c9a-127">A virtual network gateway</span></span>
* <span data-ttu-id="e8c9a-128">A virtual network gateway connection</span><span class="sxs-lookup"><span data-stu-id="e8c9a-128">A virtual network gateway connection</span></span>

<span data-ttu-id="e8c9a-129">The following diagram shows how the networks communicate between data centers.</span><span class="sxs-lookup"><span data-stu-id="e8c9a-129">The following diagram shows how the networks communicate between data centers.</span></span>

   ![Availability Group](./media/virtual-machines-windows-portal-sql-availability-group-dr/01-vpngateway-example.png)

>[!IMPORTANT]
><span data-ttu-id="e8c9a-131">This architecture incurs outbound data charges for data replicated between Azure regions.</span><span class="sxs-lookup"><span data-stu-id="e8c9a-131">This architecture incurs outbound data charges for data replicated between Azure regions.</span></span> <span data-ttu-id="e8c9a-132">See [Bandwidth Pricing](http://azure.microsoft.com/pricing/details/bandwidth/).</span><span class="sxs-lookup"><span data-stu-id="e8c9a-132">See [Bandwidth Pricing](http://azure.microsoft.com/pricing/details/bandwidth/).</span></span>  

## <a name="create-remote-replica"></a><span data-ttu-id="e8c9a-133">Create remote replica</span><span class="sxs-lookup"><span data-stu-id="e8c9a-133">Create remote replica</span></span>

<span data-ttu-id="e8c9a-134">To create a replica in a remote data center, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="e8c9a-134">To create a replica in a remote data center, do the following steps:</span></span>

1. <span data-ttu-id="e8c9a-135">[Create a virtual network in the new region](../../../virtual-network/manage-virtual-network.md#create-a-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="e8c9a-135">[Create a virtual network in the new region](../../../virtual-network/manage-virtual-network.md#create-a-virtual-network).</span></span>

1. <span data-ttu-id="e8c9a-136">[Configure a VNet-to-VNet connection using the Azure portal](../../../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e8c9a-136">[Configure a VNet-to-VNet connection using the Azure portal](../../../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md).</span></span>

   >[!NOTE]
   ><span data-ttu-id="e8c9a-137">In some cases, you may have to use PowerShell to create the VNet-to-VNet connection.</span><span class="sxs-lookup"><span data-stu-id="e8c9a-137">In some cases, you may have to use PowerShell to create the VNet-to-VNet connection.</span></span> <span data-ttu-id="e8c9a-138">For example, if you use different Azure accounts you cannot configure the connection in the portal.</span><span class="sxs-lookup"><span data-stu-id="e8c9a-138">For example, if you use different Azure accounts you cannot configure the connection in the portal.</span></span> <span data-ttu-id="e8c9a-139">In this case see, [Configure a VNet-to-VNet connection using the Azure portal](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="e8c9a-139">In this case see, [Configure a VNet-to-VNet connection using the Azure portal](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).</span></span>

1. <span data-ttu-id="e8c9a-140">[Create a domain controller in the new region](../../../active-directory/active-directory-new-forest-virtual-machine.md).</span><span class="sxs-lookup"><span data-stu-id="e8c9a-140">[Create a domain controller in the new region](../../../active-directory/active-directory-new-forest-virtual-machine.md).</span></span>

   <span data-ttu-id="e8c9a-141">This domain controller provides authentication if the domain controller in the primary site is not available.</span><span class="sxs-lookup"><span data-stu-id="e8c9a-141">This domain controller provides authentication if the domain controller in the primary site is not available.</span></span>

1. <span data-ttu-id="e8c9a-142">[Create a SQL Server virtual machine in the new region](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="e8c9a-142">[Create a SQL Server virtual machine in the new region](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

1. <span data-ttu-id="e8c9a-143">[Create an Azure load balancer in the network on the new region](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer).</span><span class="sxs-lookup"><span data-stu-id="e8c9a-143">[Create an Azure load balancer in the network on the new region](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer).</span></span>

   <span data-ttu-id="e8c9a-144">This load balancer must:</span><span class="sxs-lookup"><span data-stu-id="e8c9a-144">This load balancer must:</span></span>

   - <span data-ttu-id="e8c9a-145">Be in the same network and subnet as the new virtual machine.</span><span class="sxs-lookup"><span data-stu-id="e8c9a-145">Be in the same network and subnet as the new virtual machine.</span></span>
   - <span data-ttu-id="e8c9a-146">Have a static IP address for the availability group listener.</span><span class="sxs-lookup"><span data-stu-id="e8c9a-146">Have a static IP address for the availability group listener.</span></span>
   - <span data-ttu-id="e8c9a-147">Include a backend pool consisting of only the virtual machines in the same region as the load balancer.</span><span class="sxs-lookup"><span data-stu-id="e8c9a-147">Include a backend pool consisting of only the virtual machines in the same region as the load balancer.</span></span>
   - <span data-ttu-id="e8c9a-148">Use a TCP port probe specific to the IP address.</span><span class="sxs-lookup"><span data-stu-id="e8c9a-148">Use a TCP port probe specific to the IP address.</span></span>
   - <span data-ttu-id="e8c9a-149">Have a load balancing rule specific to the SQL Server in the same region.</span><span class="sxs-lookup"><span data-stu-id="e8c9a-149">Have a load balancing rule specific to the SQL Server in the same region.</span></span>  

1. <span data-ttu-id="e8c9a-150">[Add Failover Clustering feature to the new SQL Server](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms).</span><span class="sxs-lookup"><span data-stu-id="e8c9a-150">[Add Failover Clustering feature to the new SQL Server](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms).</span></span>

1. <span data-ttu-id="e8c9a-151">[Join the new SQL Server to the domain](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain).</span><span class="sxs-lookup"><span data-stu-id="e8c9a-151">[Join the new SQL Server to the domain](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain).</span></span>

1. <span data-ttu-id="e8c9a-152">[Set the new SQL Server service account to use a domain account](virtual-machines-windows-portal-sql-availability-group-prereq.md#setServiceAccount).</span><span class="sxs-lookup"><span data-stu-id="e8c9a-152">[Set the new SQL Server service account to use a domain account](virtual-machines-windows-portal-sql-availability-group-prereq.md#setServiceAccount).</span></span>

1. <span data-ttu-id="e8c9a-153">[Add the new SQL Server to the Windows Server Failover Cluster](virtual-machines-windows-portal-sql-availability-group-tutorial.md#addNode).</span><span class="sxs-lookup"><span data-stu-id="e8c9a-153">[Add the new SQL Server to the Windows Server Failover Cluster](virtual-machines-windows-portal-sql-availability-group-tutorial.md#addNode).</span></span>

1. <span data-ttu-id="e8c9a-154">Create an IP address resource on the cluster.</span><span class="sxs-lookup"><span data-stu-id="e8c9a-154">Create an IP address resource on the cluster.</span></span>

   <span data-ttu-id="e8c9a-155">You can create the IP address resource in Failover Cluster Manager.</span><span class="sxs-lookup"><span data-stu-id="e8c9a-155">You can create the IP address resource in Failover Cluster Manager.</span></span> <span data-ttu-id="e8c9a-156">Right-click the availability group role, click **Add Resource**, **More Resources**, and click **IP Address**.</span><span class="sxs-lookup"><span data-stu-id="e8c9a-156">Right-click the availability group role, click **Add Resource**, **More Resources**, and click **IP Address**.</span></span>

   ![Create IP Address](./media/virtual-machines-windows-portal-sql-availability-group-dr/20-add-ip-resource.png)

   <span data-ttu-id="e8c9a-158">Configure this IP address as follows:</span><span class="sxs-lookup"><span data-stu-id="e8c9a-158">Configure this IP address as follows:</span></span>

   - <span data-ttu-id="e8c9a-159">Use the network from the remote data center.</span><span class="sxs-lookup"><span data-stu-id="e8c9a-159">Use the network from the remote data center.</span></span>
   - <span data-ttu-id="e8c9a-160">Assign the IP address from the new Azure load balancer.</span><span class="sxs-lookup"><span data-stu-id="e8c9a-160">Assign the IP address from the new Azure load balancer.</span></span> 

1. <span data-ttu-id="e8c9a-161">On the new SQL Server in SQL Server Configuration Manager, [enable Always On Availability Groups](http://msdn.microsoft.com/library/ff878259.aspx).</span><span class="sxs-lookup"><span data-stu-id="e8c9a-161">On the new SQL Server in SQL Server Configuration Manager, [enable Always On Availability Groups](http://msdn.microsoft.com/library/ff878259.aspx).</span></span>

1. <span data-ttu-id="e8c9a-162">[Open firewall ports on the new SQL Server](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall).</span><span class="sxs-lookup"><span data-stu-id="e8c9a-162">[Open firewall ports on the new SQL Server](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall).</span></span>

   <span data-ttu-id="e8c9a-163">The port numbers you need to open depend on your environment.</span><span class="sxs-lookup"><span data-stu-id="e8c9a-163">The port numbers you need to open depend on your environment.</span></span> <span data-ttu-id="e8c9a-164">Open ports for the mirroring endpoint and Azure load balancer health probe.</span><span class="sxs-lookup"><span data-stu-id="e8c9a-164">Open ports for the mirroring endpoint and Azure load balancer health probe.</span></span>

1. <span data-ttu-id="e8c9a-165">[Add a replica to the availability group on the new SQL Server](http://msdn.microsoft.com/library/hh213239.aspx).</span><span class="sxs-lookup"><span data-stu-id="e8c9a-165">[Add a replica to the availability group on the new SQL Server](http://msdn.microsoft.com/library/hh213239.aspx).</span></span>

   <span data-ttu-id="e8c9a-166">For a replica in a remote Azure region, set it for asynchronous replication with manual failover.</span><span class="sxs-lookup"><span data-stu-id="e8c9a-166">For a replica in a remote Azure region, set it for asynchronous replication with manual failover.</span></span>  

1. <span data-ttu-id="e8c9a-167">Add the IP address resource as a dependency for the listener client access point (network name) cluster.</span><span class="sxs-lookup"><span data-stu-id="e8c9a-167">Add the IP address resource as a dependency for the listener client access point (network name) cluster.</span></span>

   <span data-ttu-id="e8c9a-168">The following screenshot shows a properly configured IP address cluster resource:</span><span class="sxs-lookup"><span data-stu-id="e8c9a-168">The following screenshot shows a properly configured IP address cluster resource:</span></span>

   ![Availability Group](./media/virtual-machines-windows-portal-sql-availability-group-dr/50-configure-dependency-multiple-ip.png)

   >[!IMPORTANT]
   ><span data-ttu-id="e8c9a-170">The cluster resource group includes both IP addresses.</span><span class="sxs-lookup"><span data-stu-id="e8c9a-170">The cluster resource group includes both IP addresses.</span></span> <span data-ttu-id="e8c9a-171">Both IP addresses are dependencies for the listener client access point.</span><span class="sxs-lookup"><span data-stu-id="e8c9a-171">Both IP addresses are dependencies for the listener client access point.</span></span> <span data-ttu-id="e8c9a-172">Use the **OR** operator in the cluster dependency configuration.</span><span class="sxs-lookup"><span data-stu-id="e8c9a-172">Use the **OR** operator in the cluster dependency configuration.</span></span>

1. <span data-ttu-id="e8c9a-173">[Set the cluster parameters in PowerShell](virtual-machines-windows-portal-sql-availability-group-tutorial.md#setparam).</span><span class="sxs-lookup"><span data-stu-id="e8c9a-173">[Set the cluster parameters in PowerShell](virtual-machines-windows-portal-sql-availability-group-tutorial.md#setparam).</span></span>

<span data-ttu-id="e8c9a-174">Run the PowerShell script with the cluster network name, IP address, and probe port that you configured on the load balancer in the new region.</span><span class="sxs-lookup"><span data-stu-id="e8c9a-174">Run the PowerShell script with the cluster network name, IP address, and probe port that you configured on the load balancer in the new region.</span></span>

   ```PowerShell
   $ClusterNetworkName = "<MyClusterNetworkName>" # The cluster name for the network in the new region (Use Get-ClusterNetwork on Windows Server 2012 of higher to find the name).
   $IPResourceName = "<IPResourceName>" # The cluster name for the new IP Address resource.
   $ILBIP = “<n.n.n.n>” # The IP Address of the Internal Load Balancer (ILB) in the new region. This is the static IP address for the load balancer you configured in the Azure portal.
   [int]$ProbePort = <nnnnn> # The probe port you set on the ILB.

   Import-Module FailoverClusters

   Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
   ```

## <a name="set-connection-for-multiple-subnets"></a><span data-ttu-id="e8c9a-175">Set connection for multiple subnets</span><span class="sxs-lookup"><span data-stu-id="e8c9a-175">Set connection for multiple subnets</span></span>

<span data-ttu-id="e8c9a-176">The replica in the remote data center is part of the availability group but it is in a different subnet.</span><span class="sxs-lookup"><span data-stu-id="e8c9a-176">The replica in the remote data center is part of the availability group but it is in a different subnet.</span></span> <span data-ttu-id="e8c9a-177">If this replica becomes the primary replica, application connection time-outs may occur.</span><span class="sxs-lookup"><span data-stu-id="e8c9a-177">If this replica becomes the primary replica, application connection time-outs may occur.</span></span> <span data-ttu-id="e8c9a-178">This behavior is the same as an on-premises availability group in a multi-subnet deployment.</span><span class="sxs-lookup"><span data-stu-id="e8c9a-178">This behavior is the same as an on-premises availability group in a multi-subnet deployment.</span></span> <span data-ttu-id="e8c9a-179">To allow connections from client applications, either update the client connection or configure name resolution caching on the cluster network name resource.</span><span class="sxs-lookup"><span data-stu-id="e8c9a-179">To allow connections from client applications, either update the client connection or configure name resolution caching on the cluster network name resource.</span></span>

<span data-ttu-id="e8c9a-180">Preferably, update the client connection strings to set `MultiSubnetFailover=Yes`.</span><span class="sxs-lookup"><span data-stu-id="e8c9a-180">Preferably, update the client connection strings to set `MultiSubnetFailover=Yes`.</span></span> <span data-ttu-id="e8c9a-181">See [Connecting With MultiSubnetFailover](http://msdn.microsoft.com/library/gg471494#Anchor_0).</span><span class="sxs-lookup"><span data-stu-id="e8c9a-181">See [Connecting With MultiSubnetFailover](http://msdn.microsoft.com/library/gg471494#Anchor_0).</span></span>

<span data-ttu-id="e8c9a-182">If you cannot modify the connection strings, you can configure name resolution caching.</span><span class="sxs-lookup"><span data-stu-id="e8c9a-182">If you cannot modify the connection strings, you can configure name resolution caching.</span></span> <span data-ttu-id="e8c9a-183">See [Connection Timeouts in Multi-subnet Availability Group](http://blogs.msdn.microsoft.com/alwaysonpro/2014/06/03/connection-timeouts-in-multi-subnet-availability-group/).</span><span class="sxs-lookup"><span data-stu-id="e8c9a-183">See [Connection Timeouts in Multi-subnet Availability Group](http://blogs.msdn.microsoft.com/alwaysonpro/2014/06/03/connection-timeouts-in-multi-subnet-availability-group/).</span></span>

## <a name="fail-over-to-remote-region"></a><span data-ttu-id="e8c9a-184">Fail over to remote region</span><span class="sxs-lookup"><span data-stu-id="e8c9a-184">Fail over to remote region</span></span>

<span data-ttu-id="e8c9a-185">To test listener connectivity to the remote region, you can fail over the replica to the remote region.</span><span class="sxs-lookup"><span data-stu-id="e8c9a-185">To test listener connectivity to the remote region, you can fail over the replica to the remote region.</span></span> <span data-ttu-id="e8c9a-186">While the replica is asynchronous, failover is vulnerable to potential data loss.</span><span class="sxs-lookup"><span data-stu-id="e8c9a-186">While the replica is asynchronous, failover is vulnerable to potential data loss.</span></span> <span data-ttu-id="e8c9a-187">To fail over without data loss, change the availability mode to synchronous and set the failover mode to automatic.</span><span class="sxs-lookup"><span data-stu-id="e8c9a-187">To fail over without data loss, change the availability mode to synchronous and set the failover mode to automatic.</span></span> <span data-ttu-id="e8c9a-188">Use the following steps:</span><span class="sxs-lookup"><span data-stu-id="e8c9a-188">Use the following steps:</span></span>

1. <span data-ttu-id="e8c9a-189">In **Object Explorer**, connect to the instance of SQL Server that hosts the primary replica.</span><span class="sxs-lookup"><span data-stu-id="e8c9a-189">In **Object Explorer**, connect to the instance of SQL Server that hosts the primary replica.</span></span>
1. <span data-ttu-id="e8c9a-190">Under **AlwaysOn Availability Groups**, **Availability Groups**, right-click your availability group and click **Properties**.</span><span class="sxs-lookup"><span data-stu-id="e8c9a-190">Under **AlwaysOn Availability Groups**, **Availability Groups**, right-click your availability group and click **Properties**.</span></span>
1. <span data-ttu-id="e8c9a-191">On the **General** page, under **Availability Replicas**, set the secondary replica in the DR site to use **Synchronous Commit** availability mode and **Automatic** failover mode.</span><span class="sxs-lookup"><span data-stu-id="e8c9a-191">On the **General** page, under **Availability Replicas**, set the secondary replica in the DR site to use **Synchronous Commit** availability mode and **Automatic** failover mode.</span></span>
1. <span data-ttu-id="e8c9a-192">If you have a secondary replica in same site as your primary replica for high availability, set this replica to **Asynchronous Commit** and **Manual**.</span><span class="sxs-lookup"><span data-stu-id="e8c9a-192">If you have a secondary replica in same site as your primary replica for high availability, set this replica to **Asynchronous Commit** and **Manual**.</span></span>
1. <span data-ttu-id="e8c9a-193">Click OK.</span><span class="sxs-lookup"><span data-stu-id="e8c9a-193">Click OK.</span></span>
1. <span data-ttu-id="e8c9a-194">In **Object Explorer**, right-click the availability group, and click **Show Dashboard**.</span><span class="sxs-lookup"><span data-stu-id="e8c9a-194">In **Object Explorer**, right-click the availability group, and click **Show Dashboard**.</span></span>
1. <span data-ttu-id="e8c9a-195">On the dashboard, verify that the replica on the DR site is synchronized.</span><span class="sxs-lookup"><span data-stu-id="e8c9a-195">On the dashboard, verify that the replica on the DR site is synchronized.</span></span>
1. <span data-ttu-id="e8c9a-196">In **Object Explorer**, right-click the availability group, and click **Failover...**. SQL Server Management Studios opens a wizard to fail over SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e8c9a-196">In **Object Explorer**, right-click the availability group, and click **Failover...**. SQL Server Management Studios opens a wizard to fail over SQL Server.</span></span>  
1. <span data-ttu-id="e8c9a-197">Click **Next**, and select the SQL Server instance in the DR site.</span><span class="sxs-lookup"><span data-stu-id="e8c9a-197">Click **Next**, and select the SQL Server instance in the DR site.</span></span> <span data-ttu-id="e8c9a-198">Click **Next** again.</span><span class="sxs-lookup"><span data-stu-id="e8c9a-198">Click **Next** again.</span></span>
1. <span data-ttu-id="e8c9a-199">Connect to the SQL Server instance in the DR site and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="e8c9a-199">Connect to the SQL Server instance in the DR site and click **Next**.</span></span>
1. <span data-ttu-id="e8c9a-200">On the **Summary** page, verify the settings and click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="e8c9a-200">On the **Summary** page, verify the settings and click **Finish**.</span></span>

<span data-ttu-id="e8c9a-201">After testing connectivity, move the primary replica back to your primary data center and set the availability mode back to their normal operating settings.</span><span class="sxs-lookup"><span data-stu-id="e8c9a-201">After testing connectivity, move the primary replica back to your primary data center and set the availability mode back to their normal operating settings.</span></span> <span data-ttu-id="e8c9a-202">The following table shows the normal operational settings for the architecture described in this document:</span><span class="sxs-lookup"><span data-stu-id="e8c9a-202">The following table shows the normal operational settings for the architecture described in this document:</span></span>

| <span data-ttu-id="e8c9a-203">Location</span><span class="sxs-lookup"><span data-stu-id="e8c9a-203">Location</span></span> | <span data-ttu-id="e8c9a-204">Server Instance</span><span class="sxs-lookup"><span data-stu-id="e8c9a-204">Server Instance</span></span> | <span data-ttu-id="e8c9a-205">Role</span><span class="sxs-lookup"><span data-stu-id="e8c9a-205">Role</span></span> | <span data-ttu-id="e8c9a-206">Availability Mode</span><span class="sxs-lookup"><span data-stu-id="e8c9a-206">Availability Mode</span></span> | <span data-ttu-id="e8c9a-207">Failover Mode</span><span class="sxs-lookup"><span data-stu-id="e8c9a-207">Failover Mode</span></span>
| ----- | ----- | ----- | ----- | -----
| <span data-ttu-id="e8c9a-208">Primary data center</span><span class="sxs-lookup"><span data-stu-id="e8c9a-208">Primary data center</span></span> | <span data-ttu-id="e8c9a-209">SQL-1</span><span class="sxs-lookup"><span data-stu-id="e8c9a-209">SQL-1</span></span> | <span data-ttu-id="e8c9a-210">Primary</span><span class="sxs-lookup"><span data-stu-id="e8c9a-210">Primary</span></span> | <span data-ttu-id="e8c9a-211">Synchronous</span><span class="sxs-lookup"><span data-stu-id="e8c9a-211">Synchronous</span></span> | <span data-ttu-id="e8c9a-212">Automatic</span><span class="sxs-lookup"><span data-stu-id="e8c9a-212">Automatic</span></span>
| <span data-ttu-id="e8c9a-213">Primary data center</span><span class="sxs-lookup"><span data-stu-id="e8c9a-213">Primary data center</span></span> | <span data-ttu-id="e8c9a-214">SQL-2</span><span class="sxs-lookup"><span data-stu-id="e8c9a-214">SQL-2</span></span> | <span data-ttu-id="e8c9a-215">Secondary</span><span class="sxs-lookup"><span data-stu-id="e8c9a-215">Secondary</span></span> | <span data-ttu-id="e8c9a-216">Synchronous</span><span class="sxs-lookup"><span data-stu-id="e8c9a-216">Synchronous</span></span> | <span data-ttu-id="e8c9a-217">Automatic</span><span class="sxs-lookup"><span data-stu-id="e8c9a-217">Automatic</span></span>
| <span data-ttu-id="e8c9a-218">Secondary or remote data center</span><span class="sxs-lookup"><span data-stu-id="e8c9a-218">Secondary or remote data center</span></span> | <span data-ttu-id="e8c9a-219">SQL-3</span><span class="sxs-lookup"><span data-stu-id="e8c9a-219">SQL-3</span></span> | <span data-ttu-id="e8c9a-220">Secondary</span><span class="sxs-lookup"><span data-stu-id="e8c9a-220">Secondary</span></span> | <span data-ttu-id="e8c9a-221">Asynchronous</span><span class="sxs-lookup"><span data-stu-id="e8c9a-221">Asynchronous</span></span> | <span data-ttu-id="e8c9a-222">Manual</span><span class="sxs-lookup"><span data-stu-id="e8c9a-222">Manual</span></span>


### <a name="more-information-about-planned-and-forced-manual-failover"></a><span data-ttu-id="e8c9a-223">More information about planned and forced manual failover</span><span class="sxs-lookup"><span data-stu-id="e8c9a-223">More information about planned and forced manual failover</span></span>

<span data-ttu-id="e8c9a-224">For more information, see the following topics:</span><span class="sxs-lookup"><span data-stu-id="e8c9a-224">For more information, see the following topics:</span></span>

- [<span data-ttu-id="e8c9a-225">Perform a Planned Manual Failover of an Availability Group (SQL Server)</span><span class="sxs-lookup"><span data-stu-id="e8c9a-225">Perform a Planned Manual Failover of an Availability Group (SQL Server)</span></span>](http://msdn.microsoft.com/library/hh231018.aspx)
- [<span data-ttu-id="e8c9a-226">Perform a Forced Manual Failover of an Availability Group (SQL Server)</span><span class="sxs-lookup"><span data-stu-id="e8c9a-226">Perform a Forced Manual Failover of an Availability Group (SQL Server)</span></span>](http://msdn.microsoft.com/library/ff877957.aspx)

## <a name="additional-links"></a><span data-ttu-id="e8c9a-227">Additional Links</span><span class="sxs-lookup"><span data-stu-id="e8c9a-227">Additional Links</span></span>

* [<span data-ttu-id="e8c9a-228">Always On Availability Groups</span><span class="sxs-lookup"><span data-stu-id="e8c9a-228">Always On Availability Groups</span></span>](http://msdn.microsoft.com/library/hh510230.aspx)
* [<span data-ttu-id="e8c9a-229">Azure Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="e8c9a-229">Azure Virtual Machines</span></span>](http://docs.microsoft.com/azure/virtual-machines/windows/)
* [<span data-ttu-id="e8c9a-230">Azure Load Balancers</span><span class="sxs-lookup"><span data-stu-id="e8c9a-230">Azure Load Balancers</span></span>](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer)
* [<span data-ttu-id="e8c9a-231">Azure Availability Sets</span><span class="sxs-lookup"><span data-stu-id="e8c9a-231">Azure Availability Sets</span></span>](../manage-availability.md)
