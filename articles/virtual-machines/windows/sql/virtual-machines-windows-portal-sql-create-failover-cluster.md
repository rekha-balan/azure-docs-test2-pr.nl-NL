---
title: SQL Server FCI - Azure Virtual Machines | Microsoft Docs
description: This article explains how to create SQL Server Failover Cluster Instance on Azure Virtual Machines.
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 9fc761b1-21ad-4d79-bebc-a2f094ec214d
ms.service: virtual-machines-sql
ms.devlang: na
ms.custom: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 03/17/2017
ms.author: mikeray
ms.openlocfilehash: feccbbd49228f04b1a98a0dc8ebe143fefcfca7a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661727"
---
# <a name="configure-sql-server-failover-cluster-instance-on-azure-virtual-machines"></a><span data-ttu-id="1ddae-103">Configure SQL Server Failover Cluster Instance on Azure Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="1ddae-103">Configure SQL Server Failover Cluster Instance on Azure Virtual Machines</span></span>

<span data-ttu-id="1ddae-104">This article explains how to create a SQL Server Failover Cluster Instance (FCI) on Azure virtual machines in Resource Manager model.</span><span class="sxs-lookup"><span data-stu-id="1ddae-104">This article explains how to create a SQL Server Failover Cluster Instance (FCI) on Azure virtual machines in Resource Manager model.</span></span> <span data-ttu-id="1ddae-105">This solution uses [Windows Server 2016 Datacenter edition Storage Spaces Direct \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview) as a software-based virtual SAN that synchronizes the storage (data disks) between the nodes (Azure VMs) in a Windows Cluster.</span><span class="sxs-lookup"><span data-stu-id="1ddae-105">This solution uses [Windows Server 2016 Datacenter edition Storage Spaces Direct \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview) as a software-based virtual SAN that synchronizes the storage (data disks) between the nodes (Azure VMs) in a Windows Cluster.</span></span> <span data-ttu-id="1ddae-106">S2D is new in Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="1ddae-106">S2D is new in Windows Server 2016.</span></span>

<span data-ttu-id="1ddae-107">The following diagram shows the complete solution on Azure virtual machines:</span><span class="sxs-lookup"><span data-stu-id="1ddae-107">The following diagram shows the complete solution on Azure virtual machines:</span></span>

![Availability Group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sql/media/virtual-machines-windows-portal-sql-create-failover-cluster/00-sql-fci-s2d-complete-solution.png)

<span data-ttu-id="1ddae-109">The preceding diagram shows:</span><span class="sxs-lookup"><span data-stu-id="1ddae-109">The preceding diagram shows:</span></span>

- <span data-ttu-id="1ddae-110">Two Azure virtual machines in a Windows Failover Cluster.</span><span class="sxs-lookup"><span data-stu-id="1ddae-110">Two Azure virtual machines in a Windows Failover Cluster.</span></span> <span data-ttu-id="1ddae-111">When a virtual machine is in a failover cluster it is also called a *cluster node*, or *nodes*.</span><span class="sxs-lookup"><span data-stu-id="1ddae-111">When a virtual machine is in a failover cluster it is also called a *cluster node*, or *nodes*.</span></span>
- <span data-ttu-id="1ddae-112">Each virtual machine has two or more data disks.</span><span class="sxs-lookup"><span data-stu-id="1ddae-112">Each virtual machine has two or more data disks.</span></span>
- <span data-ttu-id="1ddae-113">S2D synchronizes the data on the data disk and presents the synchronized storage as a storage pool.</span><span class="sxs-lookup"><span data-stu-id="1ddae-113">S2D synchronizes the data on the data disk and presents the synchronized storage as a storage pool.</span></span> 
- <span data-ttu-id="1ddae-114">The storage pool presents a cluster shared volume (CSV) to the failover cluster.</span><span class="sxs-lookup"><span data-stu-id="1ddae-114">The storage pool presents a cluster shared volume (CSV) to the failover cluster.</span></span>
- <span data-ttu-id="1ddae-115">The SQL Server FCI cluster role uses the CSV for the data drives.</span><span class="sxs-lookup"><span data-stu-id="1ddae-115">The SQL Server FCI cluster role uses the CSV for the data drives.</span></span> 
- <span data-ttu-id="1ddae-116">An Azure load balancer to hold the IP address for the SQL Server FCI.</span><span class="sxs-lookup"><span data-stu-id="1ddae-116">An Azure load balancer to hold the IP address for the SQL Server FCI.</span></span>
- <span data-ttu-id="1ddae-117">An Azure availability set holds all the resources.</span><span class="sxs-lookup"><span data-stu-id="1ddae-117">An Azure availability set holds all the resources.</span></span>

   >[!NOTE]
   ><span data-ttu-id="1ddae-118">All Azure resources are in the diagram are in the same resource group.</span><span class="sxs-lookup"><span data-stu-id="1ddae-118">All Azure resources are in the diagram are in the same resource group.</span></span>

<span data-ttu-id="1ddae-119">For details about S2D, see [Windows Server 2016 Datacenter edition Storage Spaces Direct \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview).</span><span class="sxs-lookup"><span data-stu-id="1ddae-119">For details about S2D, see [Windows Server 2016 Datacenter edition Storage Spaces Direct \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview).</span></span> 

<span data-ttu-id="1ddae-120">S2D supports two types of architectures - converged and hyper-converged.</span><span class="sxs-lookup"><span data-stu-id="1ddae-120">S2D supports two types of architectures - converged and hyper-converged.</span></span> <span data-ttu-id="1ddae-121">The architecture in this document is hyper-converged.</span><span class="sxs-lookup"><span data-stu-id="1ddae-121">The architecture in this document is hyper-converged.</span></span> <span data-ttu-id="1ddae-122">A hyper-converged infrastructure places the storage on the same servers that host the clustered application.</span><span class="sxs-lookup"><span data-stu-id="1ddae-122">A hyper-converged infrastructure places the storage on the same servers that host the clustered application.</span></span> <span data-ttu-id="1ddae-123">In this architecture, the storage is on each SQL Server FCI node.</span><span class="sxs-lookup"><span data-stu-id="1ddae-123">In this architecture, the storage is on each SQL Server FCI node.</span></span>

### <a name="example-azure-template"></a><span data-ttu-id="1ddae-124">Example Azure template</span><span class="sxs-lookup"><span data-stu-id="1ddae-124">Example Azure template</span></span>

<span data-ttu-id="1ddae-125">You can create the entire solution in Azure from a template.</span><span class="sxs-lookup"><span data-stu-id="1ddae-125">You can create the entire solution in Azure from a template.</span></span> <span data-ttu-id="1ddae-126">An example of a template is available in the GitHub [Azure Quickstart Templates](https://github.com/MSBrett/azure-quickstart-templates/tree/master/sql-server-2016-fci-existing-vnet-and-ad).</span><span class="sxs-lookup"><span data-stu-id="1ddae-126">An example of a template is available in the GitHub [Azure Quickstart Templates](https://github.com/MSBrett/azure-quickstart-templates/tree/master/sql-server-2016-fci-existing-vnet-and-ad).</span></span> <span data-ttu-id="1ddae-127">This example is not designed or tested for any specific workload.</span><span class="sxs-lookup"><span data-stu-id="1ddae-127">This example is not designed or tested for any specific workload.</span></span> <span data-ttu-id="1ddae-128">You can run the template to create a SQL Server FCI with S2D storage connected to your domain.</span><span class="sxs-lookup"><span data-stu-id="1ddae-128">You can run the template to create a SQL Server FCI with S2D storage connected to your domain.</span></span> <span data-ttu-id="1ddae-129">You can evaluate the template, and modify it for your purposes.</span><span class="sxs-lookup"><span data-stu-id="1ddae-129">You can evaluate the template, and modify it for your purposes.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="1ddae-130">Before you begin</span><span class="sxs-lookup"><span data-stu-id="1ddae-130">Before you begin</span></span>

<span data-ttu-id="1ddae-131">There are a few things you need to know and a couple of things that you need in place before you proceed.</span><span class="sxs-lookup"><span data-stu-id="1ddae-131">There are a few things you need to know and a couple of things that you need in place before you proceed.</span></span>

### <a name="what-to-know"></a><span data-ttu-id="1ddae-132">What to know</span><span class="sxs-lookup"><span data-stu-id="1ddae-132">What to know</span></span>
<span data-ttu-id="1ddae-133">You should have an operational understanding of the following technologies:</span><span class="sxs-lookup"><span data-stu-id="1ddae-133">You should have an operational understanding of the following technologies:</span></span>

- [<span data-ttu-id="1ddae-134">Windows cluster technologies</span><span class="sxs-lookup"><span data-stu-id="1ddae-134">Windows cluster technologies</span></span>](http://technet.microsoft.com/library/hh831579.aspx)
-  <span data-ttu-id="1ddae-135">[SQL Server Failover Cluster Instances](http://msdn.microsoft.com/library/ms189134.aspx).</span><span class="sxs-lookup"><span data-stu-id="1ddae-135">[SQL Server Failover Cluster Instances](http://msdn.microsoft.com/library/ms189134.aspx).</span></span> 

<span data-ttu-id="1ddae-136">Also, you should have a general understanding of the following technologies:</span><span class="sxs-lookup"><span data-stu-id="1ddae-136">Also, you should have a general understanding of the following technologies:</span></span>

- [<span data-ttu-id="1ddae-137">Hyper-converged solution using Storage Spaces Direct in Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="1ddae-137">Hyper-converged solution using Storage Spaces Direct in Windows Server 2016</span></span>](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct)
- [<span data-ttu-id="1ddae-138">Azure resource groups</span><span class="sxs-lookup"><span data-stu-id="1ddae-138">Azure resource groups</span></span>](../../../azure-resource-manager/resource-group-portal.md)

### <a name="what-to-have"></a><span data-ttu-id="1ddae-139">What to have</span><span class="sxs-lookup"><span data-stu-id="1ddae-139">What to have</span></span>

<span data-ttu-id="1ddae-140">Before following the instructions in this article, you should already have:</span><span class="sxs-lookup"><span data-stu-id="1ddae-140">Before following the instructions in this article, you should already have:</span></span>

- <span data-ttu-id="1ddae-141">A Microsoft Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="1ddae-141">A Microsoft Azure subscription.</span></span>
- <span data-ttu-id="1ddae-142">A Windows domain on Azure virtual machines.</span><span class="sxs-lookup"><span data-stu-id="1ddae-142">A Windows domain on Azure virtual machines.</span></span>
- <span data-ttu-id="1ddae-143">An account with permission to create objects in the Azure virtual machine.</span><span class="sxs-lookup"><span data-stu-id="1ddae-143">An account with permission to create objects in the Azure virtual machine.</span></span>
- <span data-ttu-id="1ddae-144">An Azure virtual network and subnet with sufficient IP address space for the following components:</span><span class="sxs-lookup"><span data-stu-id="1ddae-144">An Azure virtual network and subnet with sufficient IP address space for the following components:</span></span>
   - <span data-ttu-id="1ddae-145">Both virtual machines.</span><span class="sxs-lookup"><span data-stu-id="1ddae-145">Both virtual machines.</span></span>
   - <span data-ttu-id="1ddae-146">The failover cluster IP address.</span><span class="sxs-lookup"><span data-stu-id="1ddae-146">The failover cluster IP address.</span></span>
   - <span data-ttu-id="1ddae-147">An IP address for each FCI.</span><span class="sxs-lookup"><span data-stu-id="1ddae-147">An IP address for each FCI.</span></span>
- <span data-ttu-id="1ddae-148">DNS configured on the Azure Network, pointing to the domain controllers.</span><span class="sxs-lookup"><span data-stu-id="1ddae-148">DNS configured on the Azure Network, pointing to the domain controllers.</span></span> 

<span data-ttu-id="1ddae-149">With these prerequisites in place, you can proceed with building your failover cluster.</span><span class="sxs-lookup"><span data-stu-id="1ddae-149">With these prerequisites in place, you can proceed with building your failover cluster.</span></span> <span data-ttu-id="1ddae-150">The first step is to create the virtual machines.</span><span class="sxs-lookup"><span data-stu-id="1ddae-150">The first step is to create the virtual machines.</span></span> 

## <a name="step-1-create-virtual-machines"></a><span data-ttu-id="1ddae-151">Step 1: Create virtual machines</span><span class="sxs-lookup"><span data-stu-id="1ddae-151">Step 1: Create virtual machines</span></span>

1. <span data-ttu-id="1ddae-152">Log in to the [Azure portal](http://portal.azure.com) with your subscription.</span><span class="sxs-lookup"><span data-stu-id="1ddae-152">Log in to the [Azure portal](http://portal.azure.com) with your subscription.</span></span>

1. <span data-ttu-id="1ddae-153">[Create an Azure availability set](../create-availability-set.md).</span><span class="sxs-lookup"><span data-stu-id="1ddae-153">[Create an Azure availability set](../create-availability-set.md).</span></span>

   <span data-ttu-id="1ddae-154">The availability set groups virtual machines across fault domains and update domains.</span><span class="sxs-lookup"><span data-stu-id="1ddae-154">The availability set groups virtual machines across fault domains and update domains.</span></span> <span data-ttu-id="1ddae-155">The availability set makes sure that your application is not affected by single points of failure, like the network switch or the power unit of a rack of servers.</span><span class="sxs-lookup"><span data-stu-id="1ddae-155">The availability set makes sure that your application is not affected by single points of failure, like the network switch or the power unit of a rack of servers.</span></span> 

   <span data-ttu-id="1ddae-156">If you have not created the resource group for your virtual machines, do it when you create an Azure availability set.</span><span class="sxs-lookup"><span data-stu-id="1ddae-156">If you have not created the resource group for your virtual machines, do it when you create an Azure availability set.</span></span> <span data-ttu-id="1ddae-157">If you're using the Azure portal to create the availability set, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="1ddae-157">If you're using the Azure portal to create the availability set, do the following steps:</span></span>

   - <span data-ttu-id="1ddae-158">In the Azure portal, click **+** to open the Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="1ddae-158">In the Azure portal, click **+** to open the Azure Marketplace.</span></span> <span data-ttu-id="1ddae-159">Search for **Availability set**.</span><span class="sxs-lookup"><span data-stu-id="1ddae-159">Search for **Availability set**.</span></span>
   - <span data-ttu-id="1ddae-160">Click **Availability set**.</span><span class="sxs-lookup"><span data-stu-id="1ddae-160">Click **Availability set**.</span></span>
   - <span data-ttu-id="1ddae-161">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="1ddae-161">Click **Create**.</span></span>
   - <span data-ttu-id="1ddae-162">On the **Create availability set** blade, set the following values:</span><span class="sxs-lookup"><span data-stu-id="1ddae-162">On the **Create availability set** blade, set the following values:</span></span>
      - <span data-ttu-id="1ddae-163">**Name**: A name for the availability set.</span><span class="sxs-lookup"><span data-stu-id="1ddae-163">**Name**: A name for the availability set.</span></span> 
      - <span data-ttu-id="1ddae-164">**Subscription**: Your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="1ddae-164">**Subscription**: Your Azure subscription.</span></span>
      - <span data-ttu-id="1ddae-165">**Resource group**: If you want to use an existing group, click **Use existing** and select the group from the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="1ddae-165">**Resource group**: If you want to use an existing group, click **Use existing** and select the group from the drop-down list.</span></span> <span data-ttu-id="1ddae-166">Otherwise choose **Create New** and type a name for the group.</span><span class="sxs-lookup"><span data-stu-id="1ddae-166">Otherwise choose **Create New** and type a name for the group.</span></span>
      - <span data-ttu-id="1ddae-167">**Location**: Set the location where you plan to create your virtual machines.</span><span class="sxs-lookup"><span data-stu-id="1ddae-167">**Location**: Set the location where you plan to create your virtual machines.</span></span> 
      - <span data-ttu-id="1ddae-168">**Fault domains**: Use the default (3).</span><span class="sxs-lookup"><span data-stu-id="1ddae-168">**Fault domains**: Use the default (3).</span></span>
      - <span data-ttu-id="1ddae-169">**Update domains**: Use the default (5).</span><span class="sxs-lookup"><span data-stu-id="1ddae-169">**Update domains**: Use the default (5).</span></span>
   - <span data-ttu-id="1ddae-170">Click **Create** to create the availability set.</span><span class="sxs-lookup"><span data-stu-id="1ddae-170">Click **Create** to create the availability set.</span></span> 

1. <span data-ttu-id="1ddae-171">Create the virtual machines in the availability set.</span><span class="sxs-lookup"><span data-stu-id="1ddae-171">Create the virtual machines in the availability set.</span></span>

   <span data-ttu-id="1ddae-172">Provision two SQL Server virtual machines in the Azure availability set.</span><span class="sxs-lookup"><span data-stu-id="1ddae-172">Provision two SQL Server virtual machines in the Azure availability set.</span></span> <span data-ttu-id="1ddae-173">For instructions, see [Provision a SQL Server virtual machine in the Azure portal](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="1ddae-173">For instructions, see [Provision a SQL Server virtual machine in the Azure portal](virtual-machines-windows-portal-sql-server-provision.md).</span></span> 

   <span data-ttu-id="1ddae-174">Place both virtual machines:</span><span class="sxs-lookup"><span data-stu-id="1ddae-174">Place both virtual machines:</span></span>
   
   - <span data-ttu-id="1ddae-175">In the same Azure resource group that your availability set is in.</span><span class="sxs-lookup"><span data-stu-id="1ddae-175">In the same Azure resource group that your availability set is in.</span></span> 
   - <span data-ttu-id="1ddae-176">On the same network as your domain controller.</span><span class="sxs-lookup"><span data-stu-id="1ddae-176">On the same network as your domain controller.</span></span>
   - <span data-ttu-id="1ddae-177">On a subnet with sufficient IP address space for both virtual machines, and all FCIs that you may eventually use on this cluster.</span><span class="sxs-lookup"><span data-stu-id="1ddae-177">On a subnet with sufficient IP address space for both virtual machines, and all FCIs that you may eventually use on this cluster.</span></span> 
   - <span data-ttu-id="1ddae-178">In the Azure availability set.</span><span class="sxs-lookup"><span data-stu-id="1ddae-178">In the Azure availability set.</span></span>   

      >[!IMPORTANT]
      ><span data-ttu-id="1ddae-179">You cannot set or change availability set after a virtual machine has been created.</span><span class="sxs-lookup"><span data-stu-id="1ddae-179">You cannot set or change availability set after a virtual machine has been created.</span></span>

   <span data-ttu-id="1ddae-180">Choose an image from the Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="1ddae-180">Choose an image from the Azure Marketplace.</span></span> <span data-ttu-id="1ddae-181">You can use a Marketplace image with that includes Windows Server and SQL Server, or just the Windows Server.</span><span class="sxs-lookup"><span data-stu-id="1ddae-181">You can use a Marketplace image with that includes Windows Server and SQL Server, or just the Windows Server.</span></span> <span data-ttu-id="1ddae-182">For details, see [Overview of SQL Server on Azure Virtual Machines](../../virtual-machines-windows-sql-server-iaas-overview.md)</span><span class="sxs-lookup"><span data-stu-id="1ddae-182">For details, see [Overview of SQL Server on Azure Virtual Machines](../../virtual-machines-windows-sql-server-iaas-overview.md)</span></span>
   
   <span data-ttu-id="1ddae-183">The official SQL Server images in the Azure Gallery include an installed SQL Server instance, plus the SQL Server installation software, and the required key.</span><span class="sxs-lookup"><span data-stu-id="1ddae-183">The official SQL Server images in the Azure Gallery include an installed SQL Server instance, plus the SQL Server installation software, and the required key.</span></span> 
   
   <span data-ttu-id="1ddae-184">Choose the right image according to how you want to pay for the SQL Server license:</span><span class="sxs-lookup"><span data-stu-id="1ddae-184">Choose the right image according to how you want to pay for the SQL Server license:</span></span> 

   - <span data-ttu-id="1ddae-185">**Pay per usage licensing**: The per-minute cost of these images includes the SQL Server licensing:</span><span class="sxs-lookup"><span data-stu-id="1ddae-185">**Pay per usage licensing**: The per-minute cost of these images includes the SQL Server licensing:</span></span>
      - <span data-ttu-id="1ddae-186">**SQL Server 2016 Enterprise on Windows Server Datacenter 2016**</span><span class="sxs-lookup"><span data-stu-id="1ddae-186">**SQL Server 2016 Enterprise on Windows Server Datacenter 2016**</span></span>
      - <span data-ttu-id="1ddae-187">**SQL Server 2016 Standard on Windows Server Datacenter 2016**</span><span class="sxs-lookup"><span data-stu-id="1ddae-187">**SQL Server 2016 Standard on Windows Server Datacenter 2016**</span></span>
      - <span data-ttu-id="1ddae-188">**SQL Server 2016 Developer on Windows Server Datacenter 2016**</span><span class="sxs-lookup"><span data-stu-id="1ddae-188">**SQL Server 2016 Developer on Windows Server Datacenter 2016**</span></span>
   
   - <span data-ttu-id="1ddae-189">**Bring-your-own-license (BYOL)**</span><span class="sxs-lookup"><span data-stu-id="1ddae-189">**Bring-your-own-license (BYOL)**</span></span>
   
      - <span data-ttu-id="1ddae-190">**{BYOL} SQL Server 2016 Enterprise on Windows Server Datacenter 2016**</span><span class="sxs-lookup"><span data-stu-id="1ddae-190">**{BYOL} SQL Server 2016 Enterprise on Windows Server Datacenter 2016**</span></span>
      - <span data-ttu-id="1ddae-191">**{BYOL} SQL Server 2016 Standard on Windows Server Datacenter 2016**</span><span class="sxs-lookup"><span data-stu-id="1ddae-191">**{BYOL} SQL Server 2016 Standard on Windows Server Datacenter 2016**</span></span> 
   
   >[!IMPORTANT]
   ><span data-ttu-id="1ddae-192">After you create the virtual machine, remove the pre-installed standalone SQL Server instance.</span><span class="sxs-lookup"><span data-stu-id="1ddae-192">After you create the virtual machine, remove the pre-installed standalone SQL Server instance.</span></span> <span data-ttu-id="1ddae-193">You will use the pre-installed SQL Server media to create the SQL Server FCI after you configure the failover cluster and S2D.</span><span class="sxs-lookup"><span data-stu-id="1ddae-193">You will use the pre-installed SQL Server media to create the SQL Server FCI after you configure the failover cluster and S2D.</span></span> 

   <span data-ttu-id="1ddae-194">Alternatively, you can use Azure Marketplace images with just the operating system.</span><span class="sxs-lookup"><span data-stu-id="1ddae-194">Alternatively, you can use Azure Marketplace images with just the operating system.</span></span> <span data-ttu-id="1ddae-195">Choose a **Windows Server 2016 Datacenter** image and install the SQL Server FCI after you configure the failover cluster and S2D.</span><span class="sxs-lookup"><span data-stu-id="1ddae-195">Choose a **Windows Server 2016 Datacenter** image and install the SQL Server FCI after you configure the failover cluster and S2D.</span></span> <span data-ttu-id="1ddae-196">This image does not contain SQL Server installation media.</span><span class="sxs-lookup"><span data-stu-id="1ddae-196">This image does not contain SQL Server installation media.</span></span> <span data-ttu-id="1ddae-197">Place the installation media in a location where you can run the SQL Server installation for each server.</span><span class="sxs-lookup"><span data-stu-id="1ddae-197">Place the installation media in a location where you can run the SQL Server installation for each server.</span></span>

1. <span data-ttu-id="1ddae-198">After Azure creates your virtual machines, connect to each virtual machine with RDP.</span><span class="sxs-lookup"><span data-stu-id="1ddae-198">After Azure creates your virtual machines, connect to each virtual machine with RDP.</span></span> 

   <span data-ttu-id="1ddae-199">When you first connect to a virtual machine with RDP, the computer asks if you want to allow this PC to be discoverable on the network.</span><span class="sxs-lookup"><span data-stu-id="1ddae-199">When you first connect to a virtual machine with RDP, the computer asks if you want to allow this PC to be discoverable on the network.</span></span> <span data-ttu-id="1ddae-200">Click **Yes**.</span><span class="sxs-lookup"><span data-stu-id="1ddae-200">Click **Yes**.</span></span> 

1. <span data-ttu-id="1ddae-201">If you are using one of the SQL Server-based virtual machine images, remove the SQL Server instance.</span><span class="sxs-lookup"><span data-stu-id="1ddae-201">If you are using one of the SQL Server-based virtual machine images, remove the SQL Server instance.</span></span>

   - <span data-ttu-id="1ddae-202">In **Programs and Features**, right-click **Microsoft SQL Server 2016 (64-bit)** and click **Uninstall/Change**.</span><span class="sxs-lookup"><span data-stu-id="1ddae-202">In **Programs and Features**, right-click **Microsoft SQL Server 2016 (64-bit)** and click **Uninstall/Change**.</span></span> 
   - <span data-ttu-id="1ddae-203">Click **Remove**.</span><span class="sxs-lookup"><span data-stu-id="1ddae-203">Click **Remove**.</span></span> 
   - <span data-ttu-id="1ddae-204">Select the default instance.</span><span class="sxs-lookup"><span data-stu-id="1ddae-204">Select the default instance.</span></span>
   - <span data-ttu-id="1ddae-205">Remove all features under **Database Engine Services**.</span><span class="sxs-lookup"><span data-stu-id="1ddae-205">Remove all features under **Database Engine Services**.</span></span> <span data-ttu-id="1ddae-206">Do not remove **Shared Features**.</span><span class="sxs-lookup"><span data-stu-id="1ddae-206">Do not remove **Shared Features**.</span></span> <span data-ttu-id="1ddae-207">See the following picture:</span><span class="sxs-lookup"><span data-stu-id="1ddae-207">See the following picture:</span></span>

      ![Remove Features](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sql/media/virtual-machines-windows-portal-sql-create-failover-cluster/03-remove-features.png)

   - <span data-ttu-id="1ddae-209">Click **Next**, and then click **Remove**.</span><span class="sxs-lookup"><span data-stu-id="1ddae-209">Click **Next**, and then click **Remove**.</span></span>

1. <a name="ports"></a><span data-ttu-id="1ddae-210">Open the firewall ports.</span><span class="sxs-lookup"><span data-stu-id="1ddae-210">Open the firewall ports.</span></span>
   
   <span data-ttu-id="1ddae-211">On each virtual machine, open the following ports on the Windows Firewall.</span><span class="sxs-lookup"><span data-stu-id="1ddae-211">On each virtual machine, open the following ports on the Windows Firewall.</span></span> 

   | <span data-ttu-id="1ddae-212">Purpose</span><span class="sxs-lookup"><span data-stu-id="1ddae-212">Purpose</span></span> | <span data-ttu-id="1ddae-213">TCP Port</span><span class="sxs-lookup"><span data-stu-id="1ddae-213">TCP Port</span></span> | <span data-ttu-id="1ddae-214">Notes</span><span class="sxs-lookup"><span data-stu-id="1ddae-214">Notes</span></span>
   | ------ | ------ | ------
   | <span data-ttu-id="1ddae-215">SQL Server</span><span class="sxs-lookup"><span data-stu-id="1ddae-215">SQL Server</span></span> | <span data-ttu-id="1ddae-216">1433</span><span class="sxs-lookup"><span data-stu-id="1ddae-216">1433</span></span> | <span data-ttu-id="1ddae-217">Normal port for default instances of SQL Server.</span><span class="sxs-lookup"><span data-stu-id="1ddae-217">Normal port for default instances of SQL Server.</span></span> <span data-ttu-id="1ddae-218">If you used an image from the gallery, this port is automatically opened.</span><span class="sxs-lookup"><span data-stu-id="1ddae-218">If you used an image from the gallery, this port is automatically opened.</span></span> 
   | <span data-ttu-id="1ddae-219">Health probe</span><span class="sxs-lookup"><span data-stu-id="1ddae-219">Health probe</span></span> | <span data-ttu-id="1ddae-220">59999</span><span class="sxs-lookup"><span data-stu-id="1ddae-220">59999</span></span> | <span data-ttu-id="1ddae-221">Any open TCP port.</span><span class="sxs-lookup"><span data-stu-id="1ddae-221">Any open TCP port.</span></span> <span data-ttu-id="1ddae-222">In a later step, configure the load balancer [health probe](#probe) and the cluster to use this port.</span><span class="sxs-lookup"><span data-stu-id="1ddae-222">In a later step, configure the load balancer [health probe](#probe) and the cluster to use this port.</span></span>  

1. <span data-ttu-id="1ddae-223">Add storage to the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="1ddae-223">Add storage to the virtual machine.</span></span> <span data-ttu-id="1ddae-224">For detailed information, see [add storage](../../../storage/storage-premium-storage.md).</span><span class="sxs-lookup"><span data-stu-id="1ddae-224">For detailed information, see [add storage](../../../storage/storage-premium-storage.md).</span></span>

   <span data-ttu-id="1ddae-225">Both virtual machines need at least two data disks.</span><span class="sxs-lookup"><span data-stu-id="1ddae-225">Both virtual machines need at least two data disks.</span></span>

   <span data-ttu-id="1ddae-226">Attach raw disks - not NTFS formatted disks.</span><span class="sxs-lookup"><span data-stu-id="1ddae-226">Attach raw disks - not NTFS formatted disks.</span></span> 
      >[!NOTE]
      ><span data-ttu-id="1ddae-227">If you attach NTFS-formatted disks, you can only enable S2D with no disk eligibility check.</span><span class="sxs-lookup"><span data-stu-id="1ddae-227">If you attach NTFS-formatted disks, you can only enable S2D with no disk eligibility check.</span></span>  
   
   <span data-ttu-id="1ddae-228">Attach a minimum of two Premium Storage (SSD disks) to each VM.</span><span class="sxs-lookup"><span data-stu-id="1ddae-228">Attach a minimum of two Premium Storage (SSD disks) to each VM.</span></span> <span data-ttu-id="1ddae-229">We recommend at least P30 (1 TB) disks.</span><span class="sxs-lookup"><span data-stu-id="1ddae-229">We recommend at least P30 (1 TB) disks.</span></span>

   <span data-ttu-id="1ddae-230">Set host caching to **Read-only**.</span><span class="sxs-lookup"><span data-stu-id="1ddae-230">Set host caching to **Read-only**.</span></span>

   <span data-ttu-id="1ddae-231">The storage capacity you use in production environments depends on your workload.</span><span class="sxs-lookup"><span data-stu-id="1ddae-231">The storage capacity you use in production environments depends on your workload.</span></span> <span data-ttu-id="1ddae-232">The values described in this article are for demonstration and testing.</span><span class="sxs-lookup"><span data-stu-id="1ddae-232">The values described in this article are for demonstration and testing.</span></span> 

1. <span data-ttu-id="1ddae-233">[Add the virtual machines to your pre-existing domain](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain).</span><span class="sxs-lookup"><span data-stu-id="1ddae-233">[Add the virtual machines to your pre-existing domain](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain).</span></span>

<span data-ttu-id="1ddae-234">After the virtual machines are created and configured, you can configure the failover cluster.</span><span class="sxs-lookup"><span data-stu-id="1ddae-234">After the virtual machines are created and configured, you can configure the failover cluster.</span></span>

## <a name="step-2-configure-the-windows-failover-cluster-with-s2d"></a><span data-ttu-id="1ddae-235">Step 2: Configure the Windows Failover Cluster with S2D</span><span class="sxs-lookup"><span data-stu-id="1ddae-235">Step 2: Configure the Windows Failover Cluster with S2D</span></span>

<span data-ttu-id="1ddae-236">The next step is to configure the failover cluster with S2D.</span><span class="sxs-lookup"><span data-stu-id="1ddae-236">The next step is to configure the failover cluster with S2D.</span></span> <span data-ttu-id="1ddae-237">In this step, you will do the following substeps:</span><span class="sxs-lookup"><span data-stu-id="1ddae-237">In this step, you will do the following substeps:</span></span>

1. <span data-ttu-id="1ddae-238">Add Windows Failover Clustering feature</span><span class="sxs-lookup"><span data-stu-id="1ddae-238">Add Windows Failover Clustering feature</span></span>
1. <span data-ttu-id="1ddae-239">Validate the cluster</span><span class="sxs-lookup"><span data-stu-id="1ddae-239">Validate the cluster</span></span>
1. <span data-ttu-id="1ddae-240">Create the failover cluster</span><span class="sxs-lookup"><span data-stu-id="1ddae-240">Create the failover cluster</span></span>
1. <span data-ttu-id="1ddae-241">Create the cloud witness</span><span class="sxs-lookup"><span data-stu-id="1ddae-241">Create the cloud witness</span></span>
1. <span data-ttu-id="1ddae-242">Add storage</span><span class="sxs-lookup"><span data-stu-id="1ddae-242">Add storage</span></span>

### <a name="add-windows-failover-clustering-feature"></a><span data-ttu-id="1ddae-243">Add Windows Failover Clustering feature</span><span class="sxs-lookup"><span data-stu-id="1ddae-243">Add Windows Failover Clustering feature</span></span>

1. <span data-ttu-id="1ddae-244">To begin, connect to the first virtual machine with RDP using a domain account that is a member of local administrators, and has permissions to create objects in Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1ddae-244">To begin, connect to the first virtual machine with RDP using a domain account that is a member of local administrators, and has permissions to create objects in Active Directory.</span></span> <span data-ttu-id="1ddae-245">Use this account for the rest of the configuration.</span><span class="sxs-lookup"><span data-stu-id="1ddae-245">Use this account for the rest of the configuration.</span></span>

1. <span data-ttu-id="1ddae-246">[Add Failover Clustering feature to each virtual machine](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-cluster-features-to-both-sql-servers).</span><span class="sxs-lookup"><span data-stu-id="1ddae-246">[Add Failover Clustering feature to each virtual machine](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-cluster-features-to-both-sql-servers).</span></span>

   <span data-ttu-id="1ddae-247">To install Failover Clustering feature from the UI, do the following steps on both virtual machines.</span><span class="sxs-lookup"><span data-stu-id="1ddae-247">To install Failover Clustering feature from the UI, do the following steps on both virtual machines.</span></span> 
   - <span data-ttu-id="1ddae-248">In **Server Manager**, click **Manage**, and then click **Add Roles and Features**.</span><span class="sxs-lookup"><span data-stu-id="1ddae-248">In **Server Manager**, click **Manage**, and then click **Add Roles and Features**.</span></span> 
   - <span data-ttu-id="1ddae-249">In **Add Roles and Features Wizard**, click **Next** until you get to **Select Features**.</span><span class="sxs-lookup"><span data-stu-id="1ddae-249">In **Add Roles and Features Wizard**, click **Next** until you get to **Select Features**.</span></span>
   - <span data-ttu-id="1ddae-250">In **Select Features**, click **Failover Clustering**.</span><span class="sxs-lookup"><span data-stu-id="1ddae-250">In **Select Features**, click **Failover Clustering**.</span></span> <span data-ttu-id="1ddae-251">Include all required features and the management tools.</span><span class="sxs-lookup"><span data-stu-id="1ddae-251">Include all required features and the management tools.</span></span> <span data-ttu-id="1ddae-252">Click **Add Features**.</span><span class="sxs-lookup"><span data-stu-id="1ddae-252">Click **Add Features**.</span></span>
   - <span data-ttu-id="1ddae-253">Click **Next** and then click **Finish** to install the features.</span><span class="sxs-lookup"><span data-stu-id="1ddae-253">Click **Next** and then click **Finish** to install the features.</span></span> 

   <span data-ttu-id="1ddae-254">To install the Failover Clustering feature with PowerShell, run the following script from an administrator PowerShell session on one of the virtual machines.</span><span class="sxs-lookup"><span data-stu-id="1ddae-254">To install the Failover Clustering feature with PowerShell, run the following script from an administrator PowerShell session on one of the virtual machines.</span></span>

   ```PowerShell
   $nodes = ("<node1>","<node2>")
   Invoke-Command  $nodes {Install-WindowsFeature Failover-Clustering -IncludeAllSubFeature -IncludeManagementTools}
   ```

<span data-ttu-id="1ddae-255">For reference, the next steps follow the instructions under Step 3 of [Hyper-converged solution using Storage Spaces Direct in Windows Server 2016](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-3-configure-storage-spaces-direct).</span><span class="sxs-lookup"><span data-stu-id="1ddae-255">For reference, the next steps follow the instructions under Step 3 of [Hyper-converged solution using Storage Spaces Direct in Windows Server 2016](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-3-configure-storage-spaces-direct).</span></span> 

### <a name="validate-the-cluster"></a><span data-ttu-id="1ddae-256">Validate the cluster</span><span class="sxs-lookup"><span data-stu-id="1ddae-256">Validate the cluster</span></span>

<span data-ttu-id="1ddae-257">This guide refers to instructions under [validate cluster](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-31-run-cluster-validation).</span><span class="sxs-lookup"><span data-stu-id="1ddae-257">This guide refers to instructions under [validate cluster](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-31-run-cluster-validation).</span></span>

<span data-ttu-id="1ddae-258">Validate the cluster in the UI or with PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1ddae-258">Validate the cluster in the UI or with PowerShell.</span></span> 

<span data-ttu-id="1ddae-259">To validate the cluster with the UI, do the following steps from one of the virtual machines.</span><span class="sxs-lookup"><span data-stu-id="1ddae-259">To validate the cluster with the UI, do the following steps from one of the virtual machines.</span></span> 

1. <span data-ttu-id="1ddae-260">In **Server Manager**, click **Tools**, then click **Failover Cluster Manager**.</span><span class="sxs-lookup"><span data-stu-id="1ddae-260">In **Server Manager**, click **Tools**, then click **Failover Cluster Manager**.</span></span> 
1. <span data-ttu-id="1ddae-261">In **Failover Cluster Manager**, click **Action**, then click **Validate Configuration...**.</span><span class="sxs-lookup"><span data-stu-id="1ddae-261">In **Failover Cluster Manager**, click **Action**, then click **Validate Configuration...**.</span></span>
1. <span data-ttu-id="1ddae-262">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="1ddae-262">Click **Next**.</span></span> 
1. <span data-ttu-id="1ddae-263">On **Select Servers or a Cluster**, type the name of both virtual machines.</span><span class="sxs-lookup"><span data-stu-id="1ddae-263">On **Select Servers or a Cluster**, type the name of both virtual machines.</span></span>
1. <span data-ttu-id="1ddae-264">On **Testing options**, choose **Run only tests I select**.</span><span class="sxs-lookup"><span data-stu-id="1ddae-264">On **Testing options**, choose **Run only tests I select**.</span></span> <span data-ttu-id="1ddae-265">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="1ddae-265">Click **Next**.</span></span>
1. <span data-ttu-id="1ddae-266">On **Test selection**, include all tests except **Storage**.</span><span class="sxs-lookup"><span data-stu-id="1ddae-266">On **Test selection**, include all tests except **Storage**.</span></span> <span data-ttu-id="1ddae-267">See the following picture:</span><span class="sxs-lookup"><span data-stu-id="1ddae-267">See the following picture:</span></span>

   ![Validate Tests](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sql/media/virtual-machines-windows-portal-sql-create-failover-cluster/10-validate-cluster-test.png)
   
1. <span data-ttu-id="1ddae-269">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="1ddae-269">Click **Next**.</span></span>
1. <span data-ttu-id="1ddae-270">On **Confirmation**, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="1ddae-270">On **Confirmation**, click **Next**.</span></span> 

<span data-ttu-id="1ddae-271">The **Validate a Configuration Wizard** runs the validation tests.</span><span class="sxs-lookup"><span data-stu-id="1ddae-271">The **Validate a Configuration Wizard** runs the validation tests.</span></span> 

<span data-ttu-id="1ddae-272">To validate the cluster with PowerShell, run the following script from an administrator PowerShell session on one of the virtual machines.</span><span class="sxs-lookup"><span data-stu-id="1ddae-272">To validate the cluster with PowerShell, run the following script from an administrator PowerShell session on one of the virtual machines.</span></span>

   ```PowerShell
   Test-Cluster –Node ("<node1>","<node2>") –Include "Storage Spaces Direct", "Inventory", "Network", "System Configuration"
   ```

<span data-ttu-id="1ddae-273">After you validate the cluster, create the failover cluster.</span><span class="sxs-lookup"><span data-stu-id="1ddae-273">After you validate the cluster, create the failover cluster.</span></span>

### <a name="create-the-failover-cluster"></a><span data-ttu-id="1ddae-274">Create the failover cluster</span><span class="sxs-lookup"><span data-stu-id="1ddae-274">Create the failover cluster</span></span>

<span data-ttu-id="1ddae-275">This guide refers to [Create the failover cluster](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-32-create-a-cluster).</span><span class="sxs-lookup"><span data-stu-id="1ddae-275">This guide refers to [Create the failover cluster](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-32-create-a-cluster).</span></span>

<span data-ttu-id="1ddae-276">To create the failover cluster, you need:</span><span class="sxs-lookup"><span data-stu-id="1ddae-276">To create the failover cluster, you need:</span></span> 
- <span data-ttu-id="1ddae-277">The names of the virtual machines that become the cluster nodes.</span><span class="sxs-lookup"><span data-stu-id="1ddae-277">The names of the virtual machines that become the cluster nodes.</span></span> 
- <span data-ttu-id="1ddae-278">A name for the failover cluster</span><span class="sxs-lookup"><span data-stu-id="1ddae-278">A name for the failover cluster</span></span>
- <span data-ttu-id="1ddae-279">An IP address for the failover cluster.</span><span class="sxs-lookup"><span data-stu-id="1ddae-279">An IP address for the failover cluster.</span></span> <span data-ttu-id="1ddae-280">You can use an IP address that is not used on the same Azure virtual network and subnet as the cluster nodes.</span><span class="sxs-lookup"><span data-stu-id="1ddae-280">You can use an IP address that is not used on the same Azure virtual network and subnet as the cluster nodes.</span></span> 

<span data-ttu-id="1ddae-281">The following PowerShell creates a failover cluster.</span><span class="sxs-lookup"><span data-stu-id="1ddae-281">The following PowerShell creates a failover cluster.</span></span> <span data-ttu-id="1ddae-282">Update the script with the names of the nodes (the virtual machine names) and an available IP address from the Azure VNET:</span><span class="sxs-lookup"><span data-stu-id="1ddae-282">Update the script with the names of the nodes (the virtual machine names) and an available IP address from the Azure VNET:</span></span> 

```PowerShell
New-Cluster -Name <FailoverCluster-Name> -Node ("<node1>","<node2>") –StaticAddress <n.n.n.n> -NoStorage
```   

### <a name="create-a-cloud-witness"></a><span data-ttu-id="1ddae-283">Create a cloud witness</span><span class="sxs-lookup"><span data-stu-id="1ddae-283">Create a cloud witness</span></span>

<span data-ttu-id="1ddae-284">Cloud Witness is a new type of cluster quorum witness stored in an Azure Storage Blob.</span><span class="sxs-lookup"><span data-stu-id="1ddae-284">Cloud Witness is a new type of cluster quorum witness stored in an Azure Storage Blob.</span></span> <span data-ttu-id="1ddae-285">This removes the need of a separate VM hosting a witness share.</span><span class="sxs-lookup"><span data-stu-id="1ddae-285">This removes the need of a separate VM hosting a witness share.</span></span>

1. <span data-ttu-id="1ddae-286">[Create a cloud witness for the failover cluster](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness).</span><span class="sxs-lookup"><span data-stu-id="1ddae-286">[Create a cloud witness for the failover cluster](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness).</span></span> 

1. <span data-ttu-id="1ddae-287">Create a blob container.</span><span class="sxs-lookup"><span data-stu-id="1ddae-287">Create a blob container.</span></span> 

1. <span data-ttu-id="1ddae-288">Save the access keys and the container URL.</span><span class="sxs-lookup"><span data-stu-id="1ddae-288">Save the access keys and the container URL.</span></span>

1. <span data-ttu-id="1ddae-289">Configure the failover cluster cluster quorum witness.</span><span class="sxs-lookup"><span data-stu-id="1ddae-289">Configure the failover cluster cluster quorum witness.</span></span> <span data-ttu-id="1ddae-290">See, [Configure the quorum witness in the user interface].(http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness#to-configure-cloud-witness-as-a-quorum-witness) in the UI.</span><span class="sxs-lookup"><span data-stu-id="1ddae-290">See, [Configure the quorum witness in the user interface].(http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness#to-configure-cloud-witness-as-a-quorum-witness) in the UI.</span></span>

### <a name="add-storage"></a><span data-ttu-id="1ddae-291">Add storage</span><span class="sxs-lookup"><span data-stu-id="1ddae-291">Add storage</span></span>

<span data-ttu-id="1ddae-292">The disks for S2D need to be empty and without partitions or other data.</span><span class="sxs-lookup"><span data-stu-id="1ddae-292">The disks for S2D need to be empty and without partitions or other data.</span></span> <span data-ttu-id="1ddae-293">To clean disks follow [the steps in this guide](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-34-clean-disks).</span><span class="sxs-lookup"><span data-stu-id="1ddae-293">To clean disks follow [the steps in this guide](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-34-clean-disks).</span></span>
   
1. <span data-ttu-id="1ddae-294">[Enable Store Spaces Direct \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-35-enable-storage-spaces-direct).</span><span class="sxs-lookup"><span data-stu-id="1ddae-294">[Enable Store Spaces Direct \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-35-enable-storage-spaces-direct).</span></span>

   <span data-ttu-id="1ddae-295">The following PowerShell enables storage spaces direct.</span><span class="sxs-lookup"><span data-stu-id="1ddae-295">The following PowerShell enables storage spaces direct.</span></span>  

   ```PowerShell
   Enable-ClusterS2D
   ```

   <span data-ttu-id="1ddae-296">In **Failover Cluster Manager**, you can now see the storage pool.</span><span class="sxs-lookup"><span data-stu-id="1ddae-296">In **Failover Cluster Manager**, you can now see the storage pool.</span></span>

1. <span data-ttu-id="1ddae-297">[Create a volume](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-36-create-volumes).</span><span class="sxs-lookup"><span data-stu-id="1ddae-297">[Create a volume](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-36-create-volumes).</span></span>

   <span data-ttu-id="1ddae-298">One of the features of S2D is that it automatically creates a storage pool when you enable it.</span><span class="sxs-lookup"><span data-stu-id="1ddae-298">One of the features of S2D is that it automatically creates a storage pool when you enable it.</span></span> <span data-ttu-id="1ddae-299">You are now ready to create a volume.</span><span class="sxs-lookup"><span data-stu-id="1ddae-299">You are now ready to create a volume.</span></span> <span data-ttu-id="1ddae-300">The PowerShell commandlet `New-Volume` automates the volume creation process, including formatting, adding to the cluster, and creating a cluster shared volume (CSV).</span><span class="sxs-lookup"><span data-stu-id="1ddae-300">The PowerShell commandlet `New-Volume` automates the volume creation process, including formatting, adding to the cluster, and creating a cluster shared volume (CSV).</span></span> <span data-ttu-id="1ddae-301">The following example creates an 800 gigabyte (GB) CSV.</span><span class="sxs-lookup"><span data-stu-id="1ddae-301">The following example creates an 800 gigabyte (GB) CSV.</span></span> 

   ```PowerShell
   New-Volume -StoragePoolFriendlyName S2D* -FriendlyName VDisk01 -FileSystem CSVFS_REFS -Size 800GB
   ```   

   <span data-ttu-id="1ddae-302">After this command completes, an 800 GB volume is mounted as a cluster resource.</span><span class="sxs-lookup"><span data-stu-id="1ddae-302">After this command completes, an 800 GB volume is mounted as a cluster resource.</span></span> <span data-ttu-id="1ddae-303">The volume is at `C:\ClusterStorage\Volume1\`.</span><span class="sxs-lookup"><span data-stu-id="1ddae-303">The volume is at `C:\ClusterStorage\Volume1\`.</span></span>

   <span data-ttu-id="1ddae-304">The following diagram shows a cluster shared volume with S2D:</span><span class="sxs-lookup"><span data-stu-id="1ddae-304">The following diagram shows a cluster shared volume with S2D:</span></span>

   ![ClusterSharedVolume](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sql/media/virtual-machines-windows-portal-sql-create-failover-cluster/15-cluster-shared-volume.png)

## <a name="step-3-test-failover-cluster-failover"></a><span data-ttu-id="1ddae-306">Step 3: Test failover cluster failover</span><span class="sxs-lookup"><span data-stu-id="1ddae-306">Step 3: Test failover cluster failover</span></span>

<span data-ttu-id="1ddae-307">In Failover Cluster Manager, verify that you can move the storage resource to the other cluster node.</span><span class="sxs-lookup"><span data-stu-id="1ddae-307">In Failover Cluster Manager, verify that you can move the storage resource to the other cluster node.</span></span> <span data-ttu-id="1ddae-308">If you can connect to the failover cluster with **Failover Cluster Manager** and move the storage from one node to the other, you are ready to configure the FCI.</span><span class="sxs-lookup"><span data-stu-id="1ddae-308">If you can connect to the failover cluster with **Failover Cluster Manager** and move the storage from one node to the other, you are ready to configure the FCI.</span></span> 

## <a name="step-4-create-sql-server-fci"></a><span data-ttu-id="1ddae-309">Step 4: Create SQL Server FCI</span><span class="sxs-lookup"><span data-stu-id="1ddae-309">Step 4: Create SQL Server FCI</span></span>

<span data-ttu-id="1ddae-310">After you have configured the failover cluster and all cluster components including storage, you can create the SQL Server FCI.</span><span class="sxs-lookup"><span data-stu-id="1ddae-310">After you have configured the failover cluster and all cluster components including storage, you can create the SQL Server FCI.</span></span> 

1. <span data-ttu-id="1ddae-311">Connect to the first virtual machine with RDP.</span><span class="sxs-lookup"><span data-stu-id="1ddae-311">Connect to the first virtual machine with RDP.</span></span> 

1. <span data-ttu-id="1ddae-312">In **Failover Cluster Manager**, make sure all cluster core resources are on the first virtual machine.</span><span class="sxs-lookup"><span data-stu-id="1ddae-312">In **Failover Cluster Manager**, make sure all cluster core resources are on the first virtual machine.</span></span> <span data-ttu-id="1ddae-313">If necessary, move all resources to this virtual machine.</span><span class="sxs-lookup"><span data-stu-id="1ddae-313">If necessary, move all resources to this virtual machine.</span></span> 

1. <span data-ttu-id="1ddae-314">Locate the installation media.</span><span class="sxs-lookup"><span data-stu-id="1ddae-314">Locate the installation media.</span></span> <span data-ttu-id="1ddae-315">If the virtual machine uses one of the Azure Marketplace images, the media is located at `C:\SQLServer_<version number>_Full`.</span><span class="sxs-lookup"><span data-stu-id="1ddae-315">If the virtual machine uses one of the Azure Marketplace images, the media is located at `C:\SQLServer_<version number>_Full`.</span></span> <span data-ttu-id="1ddae-316">Click **Setup**.</span><span class="sxs-lookup"><span data-stu-id="1ddae-316">Click **Setup**.</span></span>

1. <span data-ttu-id="1ddae-317">In the **SQL Server Installation Center**, click **Installation**.</span><span class="sxs-lookup"><span data-stu-id="1ddae-317">In the **SQL Server Installation Center**, click **Installation**.</span></span>

1. <span data-ttu-id="1ddae-318">Click **New SQL Server failover cluster installation**.</span><span class="sxs-lookup"><span data-stu-id="1ddae-318">Click **New SQL Server failover cluster installation**.</span></span> <span data-ttu-id="1ddae-319">Follow the instructions in the wizard to install the SQL Server FCI.</span><span class="sxs-lookup"><span data-stu-id="1ddae-319">Follow the instructions in the wizard to install the SQL Server FCI.</span></span> 

   <span data-ttu-id="1ddae-320">The FCI data directories need to be on clustered storage.</span><span class="sxs-lookup"><span data-stu-id="1ddae-320">The FCI data directories need to be on clustered storage.</span></span> <span data-ttu-id="1ddae-321">With S2D, it's not a shared disk, but a mount point to a volume on each server.</span><span class="sxs-lookup"><span data-stu-id="1ddae-321">With S2D, it's not a shared disk, but a mount point to a volume on each server.</span></span> <span data-ttu-id="1ddae-322">S2D synchronizes the volume between both nodes.</span><span class="sxs-lookup"><span data-stu-id="1ddae-322">S2D synchronizes the volume between both nodes.</span></span> <span data-ttu-id="1ddae-323">The volume is presented to the cluster as a cluster shared volume.</span><span class="sxs-lookup"><span data-stu-id="1ddae-323">The volume is presented to the cluster as a cluster shared volume.</span></span> <span data-ttu-id="1ddae-324">Use the CSV mount point for the data directories.</span><span class="sxs-lookup"><span data-stu-id="1ddae-324">Use the CSV mount point for the data directories.</span></span> 

   ![DataDirectories](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sql/media/virtual-machines-windows-portal-sql-create-failover-cluster/20-data-dicrectories.png)

1. <span data-ttu-id="1ddae-326">After you complete the wizard, Setup will install a SQL Server FCI on the first node.</span><span class="sxs-lookup"><span data-stu-id="1ddae-326">After you complete the wizard, Setup will install a SQL Server FCI on the first node.</span></span> 

1. <span data-ttu-id="1ddae-327">After Setup successfully installs the FCI on the first node, connect to the second node with RDP.</span><span class="sxs-lookup"><span data-stu-id="1ddae-327">After Setup successfully installs the FCI on the first node, connect to the second node with RDP.</span></span>

1. <span data-ttu-id="1ddae-328">Open the **SQL Server Installation Center**.</span><span class="sxs-lookup"><span data-stu-id="1ddae-328">Open the **SQL Server Installation Center**.</span></span> <span data-ttu-id="1ddae-329">Click **Installation**.</span><span class="sxs-lookup"><span data-stu-id="1ddae-329">Click **Installation**.</span></span>

1. <span data-ttu-id="1ddae-330">Click **Add node to a SQL Server failover cluster**.</span><span class="sxs-lookup"><span data-stu-id="1ddae-330">Click **Add node to a SQL Server failover cluster**.</span></span> <span data-ttu-id="1ddae-331">Follow the instructions in the wizard to install SQL server and add this server to the FCI.</span><span class="sxs-lookup"><span data-stu-id="1ddae-331">Follow the instructions in the wizard to install SQL server and add this server to the FCI.</span></span>

   >[!NOTE]
   ><span data-ttu-id="1ddae-332">If you used an Azure Marketplace gallery image with SQL Server, SQL Server tools were included with the image.</span><span class="sxs-lookup"><span data-stu-id="1ddae-332">If you used an Azure Marketplace gallery image with SQL Server, SQL Server tools were included with the image.</span></span> <span data-ttu-id="1ddae-333">If you did not use this image, install the SQL Server tools separately.</span><span class="sxs-lookup"><span data-stu-id="1ddae-333">If you did not use this image, install the SQL Server tools separately.</span></span> <span data-ttu-id="1ddae-334">See [Download SQL Server Management Studio (SSMS)](http://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="1ddae-334">See [Download SQL Server Management Studio (SSMS)](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>

## <a name="step-5-create-azure-load-balancer"></a><span data-ttu-id="1ddae-335">Step 5: Create Azure load balancer</span><span class="sxs-lookup"><span data-stu-id="1ddae-335">Step 5: Create Azure load balancer</span></span>

<span data-ttu-id="1ddae-336">On Azure virtual machines, clusters use a load balancer to hold an IP address that needs to be on one cluster node at a time.</span><span class="sxs-lookup"><span data-stu-id="1ddae-336">On Azure virtual machines, clusters use a load balancer to hold an IP address that needs to be on one cluster node at a time.</span></span> <span data-ttu-id="1ddae-337">In this solution, the load balancer holds the IP address for the SQL Server FCI.</span><span class="sxs-lookup"><span data-stu-id="1ddae-337">In this solution, the load balancer holds the IP address for the SQL Server FCI.</span></span> 

<span data-ttu-id="1ddae-338">[Create and configure an Azure load balancer](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer).</span><span class="sxs-lookup"><span data-stu-id="1ddae-338">[Create and configure an Azure load balancer](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer).</span></span>

### <a name="create-the-load-balancer-in-the-azure-portal"></a><span data-ttu-id="1ddae-339">Create the load balancer in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="1ddae-339">Create the load balancer in the Azure portal</span></span>

<span data-ttu-id="1ddae-340">To create the load balancer:</span><span class="sxs-lookup"><span data-stu-id="1ddae-340">To create the load balancer:</span></span>

1. <span data-ttu-id="1ddae-341">In the Azure portal, go to the Resource Group with the virtual machines.</span><span class="sxs-lookup"><span data-stu-id="1ddae-341">In the Azure portal, go to the Resource Group with the virtual machines.</span></span>

1. <span data-ttu-id="1ddae-342">Click **+ Add**.</span><span class="sxs-lookup"><span data-stu-id="1ddae-342">Click **+ Add**.</span></span> <span data-ttu-id="1ddae-343">Search the Marketplace for **Load Balancer**.</span><span class="sxs-lookup"><span data-stu-id="1ddae-343">Search the Marketplace for **Load Balancer**.</span></span> <span data-ttu-id="1ddae-344">Click **Load Balancer**.</span><span class="sxs-lookup"><span data-stu-id="1ddae-344">Click **Load Balancer**.</span></span>

1. <span data-ttu-id="1ddae-345">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="1ddae-345">Click **Create**.</span></span> 

1. <span data-ttu-id="1ddae-346">Configure the load balancer with:</span><span class="sxs-lookup"><span data-stu-id="1ddae-346">Configure the load balancer with:</span></span>

   - <span data-ttu-id="1ddae-347">**Name**: A name that identifies the load balancer.</span><span class="sxs-lookup"><span data-stu-id="1ddae-347">**Name**: A name that identifies the load balancer.</span></span> 
   - <span data-ttu-id="1ddae-348">**Type**: The load balancer can be either public or private.</span><span class="sxs-lookup"><span data-stu-id="1ddae-348">**Type**: The load balancer can be either public or private.</span></span> <span data-ttu-id="1ddae-349">A private load balancer can be accessed from within the same VNET.</span><span class="sxs-lookup"><span data-stu-id="1ddae-349">A private load balancer can be accessed from within the same VNET.</span></span> <span data-ttu-id="1ddae-350">Most Azure applications can use a private load balancer.</span><span class="sxs-lookup"><span data-stu-id="1ddae-350">Most Azure applications can use a private load balancer.</span></span> <span data-ttu-id="1ddae-351">If your application needs access to SQL Server directly over the Internet, use a public load balancer.</span><span class="sxs-lookup"><span data-stu-id="1ddae-351">If your application needs access to SQL Server directly over the Internet, use a public load balancer.</span></span> 
   - <span data-ttu-id="1ddae-352">**Virtual Network**: The same network as the virtual machines.</span><span class="sxs-lookup"><span data-stu-id="1ddae-352">**Virtual Network**: The same network as the virtual machines.</span></span> 
   - <span data-ttu-id="1ddae-353">**Subnet**: The same subnet as the virtual machines.</span><span class="sxs-lookup"><span data-stu-id="1ddae-353">**Subnet**: The same subnet as the virtual machines.</span></span> 
   - <span data-ttu-id="1ddae-354">**Private IP address**: The same IP address that you assigned to the SQL Server FCI cluster network resource.</span><span class="sxs-lookup"><span data-stu-id="1ddae-354">**Private IP address**: The same IP address that you assigned to the SQL Server FCI cluster network resource.</span></span>
   - <span data-ttu-id="1ddae-355">**subscription**: Your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="1ddae-355">**subscription**: Your Azure subscription.</span></span>
   - <span data-ttu-id="1ddae-356">**Resource Group**: Use the same resource group as your virtual machines.</span><span class="sxs-lookup"><span data-stu-id="1ddae-356">**Resource Group**: Use the same resource group as your virtual machines.</span></span> 
   - <span data-ttu-id="1ddae-357">**Location**: Use the same Azure location as your virtual machines.</span><span class="sxs-lookup"><span data-stu-id="1ddae-357">**Location**: Use the same Azure location as your virtual machines.</span></span> 
   <span data-ttu-id="1ddae-358">See the following picture:</span><span class="sxs-lookup"><span data-stu-id="1ddae-358">See the following picture:</span></span>

   ![CreateLoadBalancer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sql/media/virtual-machines-windows-portal-sql-create-failover-cluster/30-load-balancer-create.png)
  
### <a name="configure-the-load-balancer-backend-pool"></a><span data-ttu-id="1ddae-360">Configure the load balancer backend pool</span><span class="sxs-lookup"><span data-stu-id="1ddae-360">Configure the load balancer backend pool</span></span> 

1. <span data-ttu-id="1ddae-361">Return to the Azure Resource Group with the virtual machines and locate the new load balancer.</span><span class="sxs-lookup"><span data-stu-id="1ddae-361">Return to the Azure Resource Group with the virtual machines and locate the new load balancer.</span></span> <span data-ttu-id="1ddae-362">You may have to refresh the view on the Resource Group.</span><span class="sxs-lookup"><span data-stu-id="1ddae-362">You may have to refresh the view on the Resource Group.</span></span> <span data-ttu-id="1ddae-363">Click the load balancer.</span><span class="sxs-lookup"><span data-stu-id="1ddae-363">Click the load balancer.</span></span> 

1. <span data-ttu-id="1ddae-364">On the load balancer blade, click **Backend pools**.</span><span class="sxs-lookup"><span data-stu-id="1ddae-364">On the load balancer blade, click **Backend pools**.</span></span> 

1. <span data-ttu-id="1ddae-365">Click **+ Add** to add a backend pool.</span><span class="sxs-lookup"><span data-stu-id="1ddae-365">Click **+ Add** to add a backend pool.</span></span>

1. <span data-ttu-id="1ddae-366">Type a name for the backend pool.</span><span class="sxs-lookup"><span data-stu-id="1ddae-366">Type a name for the backend pool.</span></span>

1. <span data-ttu-id="1ddae-367">Click **Add a virtual machine**.</span><span class="sxs-lookup"><span data-stu-id="1ddae-367">Click **Add a virtual machine**.</span></span>

1. <span data-ttu-id="1ddae-368">On the **Choose virtual machines** blade, click **Choose an availability set**.</span><span class="sxs-lookup"><span data-stu-id="1ddae-368">On the **Choose virtual machines** blade, click **Choose an availability set**.</span></span>

1. <span data-ttu-id="1ddae-369">Choose the availability set that you placed the SQL Server virtual machines in.</span><span class="sxs-lookup"><span data-stu-id="1ddae-369">Choose the availability set that you placed the SQL Server virtual machines in.</span></span> 

1. <span data-ttu-id="1ddae-370">On the **Choose virtual machines** blade, click **Choose the virtual machines**.</span><span class="sxs-lookup"><span data-stu-id="1ddae-370">On the **Choose virtual machines** blade, click **Choose the virtual machines**.</span></span> 

   <span data-ttu-id="1ddae-371">Your Azure portal should look like the following picture:</span><span class="sxs-lookup"><span data-stu-id="1ddae-371">Your Azure portal should look like the following picture:</span></span>

   ![CreateLoadBalancerBackEnd](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sql/media/virtual-machines-windows-portal-sql-create-failover-cluster/33-load-balancer-back-end.png)

1. <span data-ttu-id="1ddae-373">Click **Select** on the **Choose virtual machines** blade.</span><span class="sxs-lookup"><span data-stu-id="1ddae-373">Click **Select** on the **Choose virtual machines** blade.</span></span>

1. <span data-ttu-id="1ddae-374">Click **OK** twice.</span><span class="sxs-lookup"><span data-stu-id="1ddae-374">Click **OK** twice.</span></span> 

### <a name="configure-a-load-balancer-health-probe"></a><span data-ttu-id="1ddae-375">Configure a load balancer health probe</span><span class="sxs-lookup"><span data-stu-id="1ddae-375">Configure a load balancer health probe</span></span>

1. <span data-ttu-id="1ddae-376">On the load balancer blade, click **Health probes**.</span><span class="sxs-lookup"><span data-stu-id="1ddae-376">On the load balancer blade, click **Health probes**.</span></span> 

1. <span data-ttu-id="1ddae-377">Click **+ Add**.</span><span class="sxs-lookup"><span data-stu-id="1ddae-377">Click **+ Add**.</span></span> 

1. <span data-ttu-id="1ddae-378">On the **Add health probe** blade, <a name="probe"></a>Set the health probe parameters:</span><span class="sxs-lookup"><span data-stu-id="1ddae-378">On the **Add health probe** blade, <a name="probe"></a>Set the health probe parameters:</span></span>

   - <span data-ttu-id="1ddae-379">**Name**: A name for the health probe.</span><span class="sxs-lookup"><span data-stu-id="1ddae-379">**Name**: A name for the health probe.</span></span>
   - <span data-ttu-id="1ddae-380">**Protocol**: TCP.</span><span class="sxs-lookup"><span data-stu-id="1ddae-380">**Protocol**: TCP.</span></span>
   - <span data-ttu-id="1ddae-381">**Port**: Set to an available TCP port.</span><span class="sxs-lookup"><span data-stu-id="1ddae-381">**Port**: Set to an available TCP port.</span></span> <span data-ttu-id="1ddae-382">This port requires an open firewall port.</span><span class="sxs-lookup"><span data-stu-id="1ddae-382">This port requires an open firewall port.</span></span> <span data-ttu-id="1ddae-383">Use the [same port](#ports) you set for the health probe at the firewall.</span><span class="sxs-lookup"><span data-stu-id="1ddae-383">Use the [same port](#ports) you set for the health probe at the firewall.</span></span> 
   - <span data-ttu-id="1ddae-384">**Interval**: 5 Seconds.</span><span class="sxs-lookup"><span data-stu-id="1ddae-384">**Interval**: 5 Seconds.</span></span>
   - <span data-ttu-id="1ddae-385">**Unhealthy threshold**: 2 consecutive failures.</span><span class="sxs-lookup"><span data-stu-id="1ddae-385">**Unhealthy threshold**: 2 consecutive failures.</span></span>

1. <span data-ttu-id="1ddae-386">Click OK.</span><span class="sxs-lookup"><span data-stu-id="1ddae-386">Click OK.</span></span>

### <a name="set-load-balancing-rules"></a><span data-ttu-id="1ddae-387">Set load balancing rules</span><span class="sxs-lookup"><span data-stu-id="1ddae-387">Set load balancing rules</span></span>

1. <span data-ttu-id="1ddae-388">On the load balancer blade, click **Load balancing rules**.</span><span class="sxs-lookup"><span data-stu-id="1ddae-388">On the load balancer blade, click **Load balancing rules**.</span></span> 

1. <span data-ttu-id="1ddae-389">Click **+ Add**.</span><span class="sxs-lookup"><span data-stu-id="1ddae-389">Click **+ Add**.</span></span>

1. <span data-ttu-id="1ddae-390">Set the load balancing rules parameters:</span><span class="sxs-lookup"><span data-stu-id="1ddae-390">Set the load balancing rules parameters:</span></span>

   - <span data-ttu-id="1ddae-391">**Name**: A name for the load balancing rules.</span><span class="sxs-lookup"><span data-stu-id="1ddae-391">**Name**: A name for the load balancing rules.</span></span>
   - <span data-ttu-id="1ddae-392">**Frontend IP address**: Use the IP address for the SQL Server FCI cluster network resource.</span><span class="sxs-lookup"><span data-stu-id="1ddae-392">**Frontend IP address**: Use the IP address for the SQL Server FCI cluster network resource.</span></span> 
   - <span data-ttu-id="1ddae-393">**Port**: Set for the SQL Server FCI TCP port.</span><span class="sxs-lookup"><span data-stu-id="1ddae-393">**Port**: Set for the SQL Server FCI TCP port.</span></span> <span data-ttu-id="1ddae-394">The default instance port is 1433.</span><span class="sxs-lookup"><span data-stu-id="1ddae-394">The default instance port is 1433.</span></span> 
   - <span data-ttu-id="1ddae-395">**Backend port**: This value uses the same port as the **Port** value when you enable **Floating IP (direct server return)**.</span><span class="sxs-lookup"><span data-stu-id="1ddae-395">**Backend port**: This value uses the same port as the **Port** value when you enable **Floating IP (direct server return)**.</span></span>
   - <span data-ttu-id="1ddae-396">**Backend pool**: Use the backend pool name that you configured earlier.</span><span class="sxs-lookup"><span data-stu-id="1ddae-396">**Backend pool**: Use the backend pool name that you configured earlier.</span></span> 
   - <span data-ttu-id="1ddae-397">**Health probe**: Use the health probe that you configured earlier.</span><span class="sxs-lookup"><span data-stu-id="1ddae-397">**Health probe**: Use the health probe that you configured earlier.</span></span>
   - <span data-ttu-id="1ddae-398">**Session persistence**: None.</span><span class="sxs-lookup"><span data-stu-id="1ddae-398">**Session persistence**: None.</span></span>
   - <span data-ttu-id="1ddae-399">**Idle timeout (minutes)**: 4.</span><span class="sxs-lookup"><span data-stu-id="1ddae-399">**Idle timeout (minutes)**: 4.</span></span>
   - <span data-ttu-id="1ddae-400">**Floating IP (direct server return)**: Enabled</span><span class="sxs-lookup"><span data-stu-id="1ddae-400">**Floating IP (direct server return)**: Enabled</span></span>

1. <span data-ttu-id="1ddae-401">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="1ddae-401">Click **OK**.</span></span> 

## <a name="step-6-configure-cluster-for-probe"></a><span data-ttu-id="1ddae-402">Step 6: Configure cluster for probe</span><span class="sxs-lookup"><span data-stu-id="1ddae-402">Step 6: Configure cluster for probe</span></span>

<span data-ttu-id="1ddae-403">Set the cluster probe port parameter in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1ddae-403">Set the cluster probe port parameter in PowerShell.</span></span>

<span data-ttu-id="1ddae-404">To set the cluster probe port parameter, update variables in the following script from your environment.</span><span class="sxs-lookup"><span data-stu-id="1ddae-404">To set the cluster probe port parameter, update variables in the following script from your environment.</span></span> 

  ```PowerShell
   $ClusterNetworkName = "<Cluster Network Name>" # the cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher to find the name).
   $IPResourceName = "IP Address Resource Name" # the IP Address cluster resource name.
   $ILBIP = "<10.0.0.x>" # the IP Address of the Internal Load Balancer (ILB). This is the static IP address for the load balancer you configured in the Azure portal.
   [int]$ProbePort = <59999>
   
   Import-Module FailoverClusters

   Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
   ```


## <a name="step-7-test-fci-failover"></a><span data-ttu-id="1ddae-405">Step 7: Test FCI failover</span><span class="sxs-lookup"><span data-stu-id="1ddae-405">Step 7: Test FCI failover</span></span>

<span data-ttu-id="1ddae-406">Test failover of the FCI to validate cluster functionality.</span><span class="sxs-lookup"><span data-stu-id="1ddae-406">Test failover of the FCI to validate cluster functionality.</span></span> <span data-ttu-id="1ddae-407">Do the following steps:</span><span class="sxs-lookup"><span data-stu-id="1ddae-407">Do the following steps:</span></span>

1. <span data-ttu-id="1ddae-408">Connect to one of the SQL Server FCI cluster nodes with RDP.</span><span class="sxs-lookup"><span data-stu-id="1ddae-408">Connect to one of the SQL Server FCI cluster nodes with RDP.</span></span>

1. <span data-ttu-id="1ddae-409">Open **Failover Cluster Manager**.</span><span class="sxs-lookup"><span data-stu-id="1ddae-409">Open **Failover Cluster Manager**.</span></span> <span data-ttu-id="1ddae-410">Click **Roles**.</span><span class="sxs-lookup"><span data-stu-id="1ddae-410">Click **Roles**.</span></span> <span data-ttu-id="1ddae-411">Notice which node owns the SQL Server FCI role.</span><span class="sxs-lookup"><span data-stu-id="1ddae-411">Notice which node owns the SQL Server FCI role.</span></span> 

1. <span data-ttu-id="1ddae-412">Right-click the SQL Server FCI role.</span><span class="sxs-lookup"><span data-stu-id="1ddae-412">Right-click the SQL Server FCI role.</span></span> 

1. <span data-ttu-id="1ddae-413">Click **Move** and click **Best Possible Node**.</span><span class="sxs-lookup"><span data-stu-id="1ddae-413">Click **Move** and click **Best Possible Node**.</span></span>

<span data-ttu-id="1ddae-414">**Failover Cluster Manager** shows the role and its resources go offline.</span><span class="sxs-lookup"><span data-stu-id="1ddae-414">**Failover Cluster Manager** shows the role and its resources go offline.</span></span> <span data-ttu-id="1ddae-415">The resources then move and come online on the other node.</span><span class="sxs-lookup"><span data-stu-id="1ddae-415">The resources then move and come online on the other node.</span></span> 

### <a name="test-connectivity"></a><span data-ttu-id="1ddae-416">Test connectivity</span><span class="sxs-lookup"><span data-stu-id="1ddae-416">Test connectivity</span></span>

<span data-ttu-id="1ddae-417">To test connectivity, log in to another virtual machine in the same virtual network.</span><span class="sxs-lookup"><span data-stu-id="1ddae-417">To test connectivity, log in to another virtual machine in the same virtual network.</span></span> <span data-ttu-id="1ddae-418">Open **SQL Server Management Studio** and connect to the SQL Server FCI name.</span><span class="sxs-lookup"><span data-stu-id="1ddae-418">Open **SQL Server Management Studio** and connect to the SQL Server FCI name.</span></span> 

>[!NOTE]
><span data-ttu-id="1ddae-419">If necessary, you can [download SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="1ddae-419">If necessary, you can [download SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>

## <a name="limitations"></a><span data-ttu-id="1ddae-420">Limitations</span><span class="sxs-lookup"><span data-stu-id="1ddae-420">Limitations</span></span>
<span data-ttu-id="1ddae-421">On Azure virtual machines, Microsoft Distributed Transaction Coordinator (DTC) is not supported on FCIs because the RPC port is not supported by the load balancer.</span><span class="sxs-lookup"><span data-stu-id="1ddae-421">On Azure virtual machines, Microsoft Distributed Transaction Coordinator (DTC) is not supported on FCIs because the RPC port is not supported by the load balancer.</span></span>

## <a name="see-also"></a><span data-ttu-id="1ddae-422">See Also</span><span class="sxs-lookup"><span data-stu-id="1ddae-422">See Also</span></span>

[<span data-ttu-id="1ddae-423">Setup S2D with remote desktop (Azure)</span><span class="sxs-lookup"><span data-stu-id="1ddae-423">Setup S2D with remote desktop (Azure)</span></span>](http://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/rds-storage-spaces-direct-deployment) 

<span data-ttu-id="1ddae-424">[Hyper-converged solution with storage spaces direct](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct).</span><span class="sxs-lookup"><span data-stu-id="1ddae-424">[Hyper-converged solution with storage spaces direct](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct).</span></span>

[<span data-ttu-id="1ddae-425">Storage Space Direct Overview</span><span class="sxs-lookup"><span data-stu-id="1ddae-425">Storage Space Direct Overview</span></span>](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview)

[<span data-ttu-id="1ddae-426">SQL Server support for S2D</span><span class="sxs-lookup"><span data-stu-id="1ddae-426">SQL Server support for S2D</span></span>](https://blogs.technet.microsoft.com/dataplatforminsider/2016/09/27/sql-server-2016-now-supports-windows-server-2016-storage-spaces-direct/)








