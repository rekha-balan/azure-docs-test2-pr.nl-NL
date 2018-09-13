---
title: Use Azure Premium Storage with SQL Server | Microsoft Docs
description: This article uses resources created with the classic deployment model, and gives guidance on using Azure Premium Storage with SQL Server running on Azure Virtual Machines.
services: virtual-machines-windows
documentationcenter: ''
author: zroiy
manager: craigg
editor: monicar
tags: azure-service-management
ms.assetid: 7ccf99d7-7cce-4e3d-bbab-21b751ab0e88
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 06/01/2017
ms.author: jroth
ms.openlocfilehash: bb9e30489aa8870fe1c71c8c9a8bd557a2dcf2b1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44783112"
---
# <a name="use-azure-premium-storage-with-sql-server-on-virtual-machines"></a><span data-ttu-id="3791b-103">Use Azure Premium Storage with SQL Server on Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="3791b-103">Use Azure Premium Storage with SQL Server on Virtual Machines</span></span>
## <a name="overview"></a><span data-ttu-id="3791b-104">Overview</span><span class="sxs-lookup"><span data-stu-id="3791b-104">Overview</span></span>
<span data-ttu-id="3791b-105">[Azure Premium Storage](../premium-storage.md) is the next generation of storage that provides low latency and high throughput IO.</span><span class="sxs-lookup"><span data-stu-id="3791b-105">[Azure Premium Storage](../premium-storage.md) is the next generation of storage that provides low latency and high throughput IO.</span></span> <span data-ttu-id="3791b-106">It works best for key IO intensive workloads, such as SQL Server on IaaS [Virtual Machines](https://azure.microsoft.com/services/virtual-machines/).</span><span class="sxs-lookup"><span data-stu-id="3791b-106">It works best for key IO intensive workloads, such as SQL Server on IaaS [Virtual Machines](https://azure.microsoft.com/services/virtual-machines/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3791b-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="3791b-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="3791b-108">This article covers using the Classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="3791b-108">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="3791b-109">Microsoft recommends that most new deployments use the Resource Manager model.</span><span class="sxs-lookup"><span data-stu-id="3791b-109">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="3791b-110">This article provides planning and guidance for migrating a Virtual Machine running SQL Server to use Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="3791b-110">This article provides planning and guidance for migrating a Virtual Machine running SQL Server to use Premium Storage.</span></span> <span data-ttu-id="3791b-111">This includes Azure infrastructure (networking, storage) and guest Windows VM steps.</span><span class="sxs-lookup"><span data-stu-id="3791b-111">This includes Azure infrastructure (networking, storage) and guest Windows VM steps.</span></span> <span data-ttu-id="3791b-112">The example in the [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) shows a full comprehensive end to end migration of how to move larger VMs to take advantage of improved local SSD storage with PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3791b-112">The example in the [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) shows a full comprehensive end to end migration of how to move larger VMs to take advantage of improved local SSD storage with PowerShell.</span></span>

<span data-ttu-id="3791b-113">It is important to understand the end-to-end process of utilizing Azure Premium Storage with SQL Server on IAAS VMs.</span><span class="sxs-lookup"><span data-stu-id="3791b-113">It is important to understand the end-to-end process of utilizing Azure Premium Storage with SQL Server on IAAS VMs.</span></span> <span data-ttu-id="3791b-114">This includes:</span><span class="sxs-lookup"><span data-stu-id="3791b-114">This includes:</span></span>

* <span data-ttu-id="3791b-115">Identification of the prerequisites to use Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="3791b-115">Identification of the prerequisites to use Premium Storage.</span></span>
* <span data-ttu-id="3791b-116">Examples of deploying SQL Server on IaaS to Premium Storage for new deployments.</span><span class="sxs-lookup"><span data-stu-id="3791b-116">Examples of deploying SQL Server on IaaS to Premium Storage for new deployments.</span></span>
* <span data-ttu-id="3791b-117">Examples of migrating existing deployments, both stand-alone servers and deployments using SQL Always On Availability Groups.</span><span class="sxs-lookup"><span data-stu-id="3791b-117">Examples of migrating existing deployments, both stand-alone servers and deployments using SQL Always On Availability Groups.</span></span>
* <span data-ttu-id="3791b-118">Possible migration approaches.</span><span class="sxs-lookup"><span data-stu-id="3791b-118">Possible migration approaches.</span></span>
* <span data-ttu-id="3791b-119">Full end-to-end example showing Azure, Windows, and SQL Server steps for the migration of an existing Always On implementation.</span><span class="sxs-lookup"><span data-stu-id="3791b-119">Full end-to-end example showing Azure, Windows, and SQL Server steps for the migration of an existing Always On implementation.</span></span>

<span data-ttu-id="3791b-120">For more background information on SQL Server in Azure Virtual Machines, see [SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3791b-120">For more background information on SQL Server in Azure Virtual Machines, see [SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

<span data-ttu-id="3791b-121">**Author:** Daniel Sol **Technical Reviewers:** Luis Carlos Vargas Herring, Sanjay Mishra, Pravin Mital, Juergen Thomas, Gonzalo Ruiz.</span><span class="sxs-lookup"><span data-stu-id="3791b-121">**Author:** Daniel Sol **Technical Reviewers:** Luis Carlos Vargas Herring, Sanjay Mishra, Pravin Mital, Juergen Thomas, Gonzalo Ruiz.</span></span>

## <a name="prerequisites-for-premium-storage"></a><span data-ttu-id="3791b-122">Prerequisites for Premium Storage</span><span class="sxs-lookup"><span data-stu-id="3791b-122">Prerequisites for Premium Storage</span></span>
<span data-ttu-id="3791b-123">There are several prerequisites for using Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="3791b-123">There are several prerequisites for using Premium Storage.</span></span>

### <a name="machine-size"></a><span data-ttu-id="3791b-124">Machine size</span><span class="sxs-lookup"><span data-stu-id="3791b-124">Machine size</span></span>
<span data-ttu-id="3791b-125">For using Premium Storage you need to use DS series Virtual Machines (VM).</span><span class="sxs-lookup"><span data-stu-id="3791b-125">For using Premium Storage you need to use DS series Virtual Machines (VM).</span></span> <span data-ttu-id="3791b-126">If you have not used DS Series machines in your cloud service before, you must delete the existing VM, keep the attached disks, and then create a new cloud service before recreating the VM as DS\* role size.</span><span class="sxs-lookup"><span data-stu-id="3791b-126">If you have not used DS Series machines in your cloud service before, you must delete the existing VM, keep the attached disks, and then create a new cloud service before recreating the VM as DS\* role size.</span></span> <span data-ttu-id="3791b-127">For more information on Virtual Machine sizes, see [Virtual Machine and Cloud Service Sizes for Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3791b-127">For more information on Virtual Machine sizes, see [Virtual Machine and Cloud Service Sizes for Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

### <a name="cloud-services"></a><span data-ttu-id="3791b-128">Cloud services</span><span class="sxs-lookup"><span data-stu-id="3791b-128">Cloud services</span></span>
<span data-ttu-id="3791b-129">You can only use DS\* VMs with Premium Storage when they are created in a new cloud service.</span><span class="sxs-lookup"><span data-stu-id="3791b-129">You can only use DS\* VMs with Premium Storage when they are created in a new cloud service.</span></span> <span data-ttu-id="3791b-130">If you are using SQL Server Always On in Azure, the Always On Listener refers to the Azure Internal or External Load Balancer IP address that is associated with a cloud service.</span><span class="sxs-lookup"><span data-stu-id="3791b-130">If you are using SQL Server Always On in Azure, the Always On Listener refers to the Azure Internal or External Load Balancer IP address that is associated with a cloud service.</span></span> <span data-ttu-id="3791b-131">This article focuses on how to migrate while maintaining availability in this scenario.</span><span class="sxs-lookup"><span data-stu-id="3791b-131">This article focuses on how to migrate while maintaining availability in this scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="3791b-132">A DS\* Series must be the first VM that is deployed to the new Cloud Service.</span><span class="sxs-lookup"><span data-stu-id="3791b-132">A DS\* Series must be the first VM that is deployed to the new Cloud Service.</span></span>
>
>

### <a name="regional-vnets"></a><span data-ttu-id="3791b-133">Regional VNETS</span><span class="sxs-lookup"><span data-stu-id="3791b-133">Regional VNETS</span></span>
<span data-ttu-id="3791b-134">For DS\* VMs you must configure the Virtual Network (VNET) hosting your VMs to be regional.</span><span class="sxs-lookup"><span data-stu-id="3791b-134">For DS\* VMs you must configure the Virtual Network (VNET) hosting your VMs to be regional.</span></span> <span data-ttu-id="3791b-135">This “widens” the VNET is to allow the larger VMs to be provisioned in other clusters and allow communication between them.</span><span class="sxs-lookup"><span data-stu-id="3791b-135">This “widens” the VNET is to allow the larger VMs to be provisioned in other clusters and allow communication between them.</span></span> <span data-ttu-id="3791b-136">In the following screenshot, the highlighted Location shows regional VNETs, whereas the first result shows a “narrow” VNET.</span><span class="sxs-lookup"><span data-stu-id="3791b-136">In the following screenshot, the highlighted Location shows regional VNETs, whereas the first result shows a “narrow” VNET.</span></span>

![RegionalVNET][1]

<span data-ttu-id="3791b-138">You can raise a Microsoft support ticket to migrate to a regional VNET.</span><span class="sxs-lookup"><span data-stu-id="3791b-138">You can raise a Microsoft support ticket to migrate to a regional VNET.</span></span> <span data-ttu-id="3791b-139">Microsoft then makes a change.</span><span class="sxs-lookup"><span data-stu-id="3791b-139">Microsoft then makes a change.</span></span> <span data-ttu-id="3791b-140">To complete the migration to regional VNETs, change the property AffinityGroup in the network configuration.</span><span class="sxs-lookup"><span data-stu-id="3791b-140">To complete the migration to regional VNETs, change the property AffinityGroup in the network configuration.</span></span> <span data-ttu-id="3791b-141">First export the Network Configuration in PowerShell, and then replace the **AffinityGroup** property in the **VirtualNetworkSite** element with a **Location** property.</span><span class="sxs-lookup"><span data-stu-id="3791b-141">First export the Network Configuration in PowerShell, and then replace the **AffinityGroup** property in the **VirtualNetworkSite** element with a **Location** property.</span></span> <span data-ttu-id="3791b-142">Specify `Location = XXXX` where `XXXX` is an Azure region.</span><span class="sxs-lookup"><span data-stu-id="3791b-142">Specify `Location = XXXX` where `XXXX` is an Azure region.</span></span> <span data-ttu-id="3791b-143">Then import the new configuration.</span><span class="sxs-lookup"><span data-stu-id="3791b-143">Then import the new configuration.</span></span>

<span data-ttu-id="3791b-144">For example, considering the following VNET configuration:</span><span class="sxs-lookup"><span data-stu-id="3791b-144">For example, considering the following VNET configuration:</span></span>

    <VirtualNetworkSite name="danAzureSQLnet" AffinityGroup="AzureSQLNetwork">
    <AddressSpace>
      <AddressPrefix>10.0.0.0/8</AddressPrefix>
      <AddressPrefix>172.16.0.0/12</AddressPrefix>
    </AddressSpace>
    <Subnets>
    ...
    </VirtualNetworkSite>

<span data-ttu-id="3791b-145">To move this to a regional VNET in West Europe, change the configuration to the following:</span><span class="sxs-lookup"><span data-stu-id="3791b-145">To move this to a regional VNET in West Europe, change the configuration to the following:</span></span>

    <VirtualNetworkSite name="danAzureSQLnet" Location="West Europe">
    <AddressSpace>
      <AddressPrefix>10.0.0.0/8</AddressPrefix>
      <AddressPrefix>172.16.0.0/12</AddressPrefix>
    </AddressSpace>
    <Subnets>
    ...
    </VirtualNetworkSite>

### <a name="storage-accounts"></a><span data-ttu-id="3791b-146">Storage accounts</span><span class="sxs-lookup"><span data-stu-id="3791b-146">Storage accounts</span></span>
<span data-ttu-id="3791b-147">You need to create a new storage account that is configured for Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="3791b-147">You need to create a new storage account that is configured for Premium Storage.</span></span> <span data-ttu-id="3791b-148">Note that the use of Premium Storage is set at the storage account, not on individual VHDs, however when using a DS\* Series VM you can attach VHD’s from Premium and Standard Storage accounts.</span><span class="sxs-lookup"><span data-stu-id="3791b-148">Note that the use of Premium Storage is set at the storage account, not on individual VHDs, however when using a DS\* Series VM you can attach VHD’s from Premium and Standard Storage accounts.</span></span> <span data-ttu-id="3791b-149">You may consider this if you do not want to place the OS VHD on to the Premium Storage account.</span><span class="sxs-lookup"><span data-stu-id="3791b-149">You may consider this if you do not want to place the OS VHD on to the Premium Storage account.</span></span>

<span data-ttu-id="3791b-150">The following **New-AzureStorageAccountPowerShell** command with the "Premium_LRS" **Type** creates a Premium Storage Account:</span><span class="sxs-lookup"><span data-stu-id="3791b-150">The following **New-AzureStorageAccountPowerShell** command with the "Premium_LRS" **Type** creates a Premium Storage Account:</span></span>

    $newstorageaccountname = "danpremstor"
    New-AzureStorageAccount -StorageAccountName $newstorageaccountname -Location "West Europe" -Type "Premium_LRS"   

### <a name="vhds-cache-settings"></a><span data-ttu-id="3791b-151">VHDs Cache Settings</span><span class="sxs-lookup"><span data-stu-id="3791b-151">VHDs Cache Settings</span></span>
<span data-ttu-id="3791b-152">The main difference between creating disks that are part of a Premium Storage account is the disk cache setting.</span><span class="sxs-lookup"><span data-stu-id="3791b-152">The main difference between creating disks that are part of a Premium Storage account is the disk cache setting.</span></span> <span data-ttu-id="3791b-153">For SQL Server Data volume disks it is recommended that you use ‘**Read Caching**’.</span><span class="sxs-lookup"><span data-stu-id="3791b-153">For SQL Server Data volume disks it is recommended that you use ‘**Read Caching**’.</span></span> <span data-ttu-id="3791b-154">For Transaction log volumes, the disk cache setting should be set to ‘**None**’.</span><span class="sxs-lookup"><span data-stu-id="3791b-154">For Transaction log volumes, the disk cache setting should be set to ‘**None**’.</span></span> <span data-ttu-id="3791b-155">This is different from the recommendations for Standard Storage accounts.</span><span class="sxs-lookup"><span data-stu-id="3791b-155">This is different from the recommendations for Standard Storage accounts.</span></span>

<span data-ttu-id="3791b-156">Once the VHDs have been attached, the cache setting cannot be altered.</span><span class="sxs-lookup"><span data-stu-id="3791b-156">Once the VHDs have been attached, the cache setting cannot be altered.</span></span> <span data-ttu-id="3791b-157">You would need to detach and reattach the VHD with an updated cache setting.</span><span class="sxs-lookup"><span data-stu-id="3791b-157">You would need to detach and reattach the VHD with an updated cache setting.</span></span>

### <a name="windows-storage-spaces"></a><span data-ttu-id="3791b-158">Windows storage spaces</span><span class="sxs-lookup"><span data-stu-id="3791b-158">Windows storage spaces</span></span>
<span data-ttu-id="3791b-159">You can use [Windows Storage Spaces](https://technet.microsoft.com/library/hh831739.aspx) as you did with previous Standard Storage, this allows you to migrate a VM that is already utilizing Storage Spaces.</span><span class="sxs-lookup"><span data-stu-id="3791b-159">You can use [Windows Storage Spaces](https://technet.microsoft.com/library/hh831739.aspx) as you did with previous Standard Storage, this allows you to migrate a VM that is already utilizing Storage Spaces.</span></span> <span data-ttu-id="3791b-160">The example in [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) (step 9 and forward) demonstrates the Powershell code to extract and import a VM with multiple attached VHDs.</span><span class="sxs-lookup"><span data-stu-id="3791b-160">The example in [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) (step 9 and forward) demonstrates the Powershell code to extract and import a VM with multiple attached VHDs.</span></span>

<span data-ttu-id="3791b-161">Storage Pools were used with Standard Azure storage account to enhance throughput and reduce latency.</span><span class="sxs-lookup"><span data-stu-id="3791b-161">Storage Pools were used with Standard Azure storage account to enhance throughput and reduce latency.</span></span> <span data-ttu-id="3791b-162">You might find value in testing Storage Pools with Premium Storage for new deployments, but they do add additional complexity with storage setup.</span><span class="sxs-lookup"><span data-stu-id="3791b-162">You might find value in testing Storage Pools with Premium Storage for new deployments, but they do add additional complexity with storage setup.</span></span>

#### <a name="how-to-find-which-azure-virtual-disks-map-to-storage-pools"></a><span data-ttu-id="3791b-163">How to find which Azure Virtual Disks map to storage pools</span><span class="sxs-lookup"><span data-stu-id="3791b-163">How to find which Azure Virtual Disks map to storage pools</span></span>
<span data-ttu-id="3791b-164">As there are different cache setting recommendations for attached VHDs, you might decide to copy the VHDs to a Premium Storage account.</span><span class="sxs-lookup"><span data-stu-id="3791b-164">As there are different cache setting recommendations for attached VHDs, you might decide to copy the VHDs to a Premium Storage account.</span></span> <span data-ttu-id="3791b-165">However, when you reattach them to the new DS series VM, you might need to alter the cache settings.</span><span class="sxs-lookup"><span data-stu-id="3791b-165">However, when you reattach them to the new DS series VM, you might need to alter the cache settings.</span></span> <span data-ttu-id="3791b-166">It is simpler to apply the Premium Storage recommended cache settings when you have separate VHDs for the SQL Data files and log files (rather than a single VHD that contains both).</span><span class="sxs-lookup"><span data-stu-id="3791b-166">It is simpler to apply the Premium Storage recommended cache settings when you have separate VHDs for the SQL Data files and log files (rather than a single VHD that contains both).</span></span>

> [!NOTE]
> <span data-ttu-id="3791b-167">If you have SQL Server data and log files on the same volume, the caching option you choose depends on the IO access patterns for your database workloads.</span><span class="sxs-lookup"><span data-stu-id="3791b-167">If you have SQL Server data and log files on the same volume, the caching option you choose depends on the IO access patterns for your database workloads.</span></span> <span data-ttu-id="3791b-168">Only testing can demonstrate which caching option is best for this scenario.</span><span class="sxs-lookup"><span data-stu-id="3791b-168">Only testing can demonstrate which caching option is best for this scenario.</span></span>
>
>

<span data-ttu-id="3791b-169">However, if you are using Windows Storage Spaces which are made up of multiple VHDs you need to look at your original scripts to identify which attached VHDs are in what specific pool, so you can then set the cache settings accordingly for each disk.</span><span class="sxs-lookup"><span data-stu-id="3791b-169">However, if you are using Windows Storage Spaces which are made up of multiple VHDs you need to look at your original scripts to identify which attached VHDs are in what specific pool, so you can then set the cache settings accordingly for each disk.</span></span>

<span data-ttu-id="3791b-170">If you do not have original script available to show you which VHDs map to the storage pool, you can use the following steps to determine the disk/storage pool mapping.</span><span class="sxs-lookup"><span data-stu-id="3791b-170">If you do not have original script available to show you which VHDs map to the storage pool, you can use the following steps to determine the disk/storage pool mapping.</span></span>

<span data-ttu-id="3791b-171">For each disk, use the following steps:</span><span class="sxs-lookup"><span data-stu-id="3791b-171">For each disk, use the following steps:</span></span>

1. <span data-ttu-id="3791b-172">Get list of disks attached to VM with the **Get-AzureVM** command:</span><span class="sxs-lookup"><span data-stu-id="3791b-172">Get list of disks attached to VM with the **Get-AzureVM** command:</span></span>

    <span data-ttu-id="3791b-173">Get-AzureVM -ServiceName <servicename> -Name <vmname> | Get-AzureDataDisk</span><span class="sxs-lookup"><span data-stu-id="3791b-173">Get-AzureVM -ServiceName <servicename> -Name <vmname> | Get-AzureDataDisk</span></span>
2. <span data-ttu-id="3791b-174">Note the Diskname and LUN.</span><span class="sxs-lookup"><span data-stu-id="3791b-174">Note the Diskname and LUN.</span></span>

    ![DisknameAndLUN][2]
3. <span data-ttu-id="3791b-176">Remote desktop into the VM.</span><span class="sxs-lookup"><span data-stu-id="3791b-176">Remote desktop into the VM.</span></span> <span data-ttu-id="3791b-177">Then go to **Computer Management** | **Device Manager** | **Disk Drives**.</span><span class="sxs-lookup"><span data-stu-id="3791b-177">Then go to **Computer Management** | **Device Manager** | **Disk Drives**.</span></span> <span data-ttu-id="3791b-178">Look at the properties of each of the ‘Microsoft Virtual Disks’</span><span class="sxs-lookup"><span data-stu-id="3791b-178">Look at the properties of each of the ‘Microsoft Virtual Disks’</span></span>

    ![VirtualDiskProperties][3]
4. <span data-ttu-id="3791b-180">The LUN number here is a reference to the LUN number you specify when attaching the VHD to the VM.</span><span class="sxs-lookup"><span data-stu-id="3791b-180">The LUN number here is a reference to the LUN number you specify when attaching the VHD to the VM.</span></span>
5. <span data-ttu-id="3791b-181">For the ‘Microsoft Virtual Disk’ go to the **Details** tab, then in the **Property** list, go to **Driver Key**.</span><span class="sxs-lookup"><span data-stu-id="3791b-181">For the ‘Microsoft Virtual Disk’ go to the **Details** tab, then in the **Property** list, go to **Driver Key**.</span></span> <span data-ttu-id="3791b-182">In the **Value**, note the **Offset**, which is 0002 in the following screenshot.</span><span class="sxs-lookup"><span data-stu-id="3791b-182">In the **Value**, note the **Offset**, which is 0002 in the following screenshot.</span></span> <span data-ttu-id="3791b-183">The 0002 denotes the PhysicalDisk2 that the storage pool references.</span><span class="sxs-lookup"><span data-stu-id="3791b-183">The 0002 denotes the PhysicalDisk2 that the storage pool references.</span></span>

    ![VirtualDiskPropertyDetails][4]
6. <span data-ttu-id="3791b-185">For each storage pool, dump out the associated disks:</span><span class="sxs-lookup"><span data-stu-id="3791b-185">For each storage pool, dump out the associated disks:</span></span>

    <span data-ttu-id="3791b-186">Get-StoragePool -FriendlyName AMS1pooldata | Get-PhysicalDisk</span><span class="sxs-lookup"><span data-stu-id="3791b-186">Get-StoragePool -FriendlyName AMS1pooldata | Get-PhysicalDisk</span></span>

    ![GetStoragePool][5]

<span data-ttu-id="3791b-188">Now you can use this information to associate attached VHDs to Physical Disks in Storage Pools.</span><span class="sxs-lookup"><span data-stu-id="3791b-188">Now you can use this information to associate attached VHDs to Physical Disks in Storage Pools.</span></span>

<span data-ttu-id="3791b-189">Once you have mapped VHDs to Physical Disks in Storage Pools you can then detach and copy them over to a Premium Storage account, then attach them with the correct cache setting.</span><span class="sxs-lookup"><span data-stu-id="3791b-189">Once you have mapped VHDs to Physical Disks in Storage Pools you can then detach and copy them over to a Premium Storage account, then attach them with the correct cache setting.</span></span> <span data-ttu-id="3791b-190">See the example in the [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage), steps 8 through 12.</span><span class="sxs-lookup"><span data-stu-id="3791b-190">See the example in the [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage), steps 8 through 12.</span></span> <span data-ttu-id="3791b-191">These steps show how to extract a VM-attached VHD disk configuration to a CSV file, copy the VHDs, alter the disk configuration cache settings, and finally redeploy the VM as a DS series VM with all the attached disks.</span><span class="sxs-lookup"><span data-stu-id="3791b-191">These steps show how to extract a VM-attached VHD disk configuration to a CSV file, copy the VHDs, alter the disk configuration cache settings, and finally redeploy the VM as a DS series VM with all the attached disks.</span></span>

### <a name="vm-storage-bandwidth-and-vhd-storage-throughput"></a><span data-ttu-id="3791b-192">VM storage bandwidth and VHD storage throughput</span><span class="sxs-lookup"><span data-stu-id="3791b-192">VM storage bandwidth and VHD storage throughput</span></span>
<span data-ttu-id="3791b-193">The amount of storage performance depends on the DS\* VM size specified and the VHD sizes.</span><span class="sxs-lookup"><span data-stu-id="3791b-193">The amount of storage performance depends on the DS\* VM size specified and the VHD sizes.</span></span> <span data-ttu-id="3791b-194">The VMs have different allowances for the number of VHDs that can be attached and the maximum bandwidth they support (MB/s).</span><span class="sxs-lookup"><span data-stu-id="3791b-194">The VMs have different allowances for the number of VHDs that can be attached and the maximum bandwidth they support (MB/s).</span></span> <span data-ttu-id="3791b-195">For the specific bandwidth numbers, see [Virtual Machine and Cloud Service Sizes for Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3791b-195">For the specific bandwidth numbers, see [Virtual Machine and Cloud Service Sizes for Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="3791b-196">Increased IOPS are achieved with larger disk sizes.</span><span class="sxs-lookup"><span data-stu-id="3791b-196">Increased IOPS are achieved with larger disk sizes.</span></span> <span data-ttu-id="3791b-197">You should consider this when you think about your migration path.</span><span class="sxs-lookup"><span data-stu-id="3791b-197">You should consider this when you think about your migration path.</span></span> <span data-ttu-id="3791b-198">For details, [see the table for IOPS and Disk Types](../premium-storage.md#scalability-and-performance-targets).</span><span class="sxs-lookup"><span data-stu-id="3791b-198">For details, [see the table for IOPS and Disk Types](../premium-storage.md#scalability-and-performance-targets).</span></span>

<span data-ttu-id="3791b-199">Finally, consider that VMs have different maximum disk bandwidths that they support for all disks attached.</span><span class="sxs-lookup"><span data-stu-id="3791b-199">Finally, consider that VMs have different maximum disk bandwidths that they support for all disks attached.</span></span> <span data-ttu-id="3791b-200">Under high load, you could saturate the maximum disk bandwidth available for that VM role size.</span><span class="sxs-lookup"><span data-stu-id="3791b-200">Under high load, you could saturate the maximum disk bandwidth available for that VM role size.</span></span> <span data-ttu-id="3791b-201">For example a Standard_DS14 supports up to 512MB/s; therefore, with three P30 disks you could saturate the disk bandwidth of the VM.</span><span class="sxs-lookup"><span data-stu-id="3791b-201">For example a Standard_DS14 supports up to 512MB/s; therefore, with three P30 disks you could saturate the disk bandwidth of the VM.</span></span> <span data-ttu-id="3791b-202">But in this example, the throughput limit could be exceeded depending on the mix of read and write IOs.</span><span class="sxs-lookup"><span data-stu-id="3791b-202">But in this example, the throughput limit could be exceeded depending on the mix of read and write IOs.</span></span>

## <a name="new-deployments"></a><span data-ttu-id="3791b-203">New deployments</span><span class="sxs-lookup"><span data-stu-id="3791b-203">New deployments</span></span>
<span data-ttu-id="3791b-204">The next two sections demonstrate how you can deploy SQL Server VMs to Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="3791b-204">The next two sections demonstrate how you can deploy SQL Server VMs to Premium Storage.</span></span> <span data-ttu-id="3791b-205">As mentioned before, you do not necessarily need to place the OS disk onto Premium storage.</span><span class="sxs-lookup"><span data-stu-id="3791b-205">As mentioned before, you do not necessarily need to place the OS disk onto Premium storage.</span></span> <span data-ttu-id="3791b-206">You might choose to do this if you are intending to place any intensive IO workloads on the OS VHD.</span><span class="sxs-lookup"><span data-stu-id="3791b-206">You might choose to do this if you are intending to place any intensive IO workloads on the OS VHD.</span></span>

<span data-ttu-id="3791b-207">The first example demonstrates utilizing existing Azure Gallery Images.</span><span class="sxs-lookup"><span data-stu-id="3791b-207">The first example demonstrates utilizing existing Azure Gallery Images.</span></span> <span data-ttu-id="3791b-208">The second example shows how to use a custom VM image that you have in an existing Standard storage account.</span><span class="sxs-lookup"><span data-stu-id="3791b-208">The second example shows how to use a custom VM image that you have in an existing Standard storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="3791b-209">These examples assume that you have already created a Regional VNET.</span><span class="sxs-lookup"><span data-stu-id="3791b-209">These examples assume that you have already created a Regional VNET.</span></span>
>
>

### <a name="create-a-new-vm-with-premium-storage-with-gallery-image"></a><span data-ttu-id="3791b-210">Create a new VM with Premium Storage with Gallery Image</span><span class="sxs-lookup"><span data-stu-id="3791b-210">Create a new VM with Premium Storage with Gallery Image</span></span>
<span data-ttu-id="3791b-211">The example below shows how to place the OS VHD onto premium storage and attach Premium Storage VHDs.</span><span class="sxs-lookup"><span data-stu-id="3791b-211">The example below shows how to place the OS VHD onto premium storage and attach Premium Storage VHDs.</span></span> <span data-ttu-id="3791b-212">However, you can also place the OS disk in a Standard Storage account and then attach VHDs that reside in a Premium Storage account.</span><span class="sxs-lookup"><span data-stu-id="3791b-212">However, you can also place the OS disk in a Standard Storage account and then attach VHDs that reside in a Premium Storage account.</span></span> <span data-ttu-id="3791b-213">Both scenarios are demonstrated.</span><span class="sxs-lookup"><span data-stu-id="3791b-213">Both scenarios are demonstrated.</span></span>

    $mysubscription = "DansSubscription"
    $location = "West Europe"

    #Set up subscription
    Set-AzureSubscription -SubscriptionName $mysubscription
    Select-AzureSubscription -SubscriptionName $mysubscription -Current  

#### <a name="step-1-create-a-premium-storage-account"></a><span data-ttu-id="3791b-214">Step 1: Create a Premium Storage Account</span><span class="sxs-lookup"><span data-stu-id="3791b-214">Step 1: Create a Premium Storage Account</span></span>
    #Create Premium Storage account, note Type
    $newxiostorageaccountname = "danspremsams"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountname -Location $location -Type "Premium_LRS"  


#### <a name="step-2-create-a-new-cloud-service"></a><span data-ttu-id="3791b-215">Step 2: Create a New Cloud Service</span><span class="sxs-lookup"><span data-stu-id="3791b-215">Step 2: Create a New Cloud Service</span></span>
    $destcloudsvc = "danNewSvcAms"
    New-AzureService $destcloudsvc -Location $location


#### <a name="step-3-reserve-a-cloud-service-vip-optional"></a><span data-ttu-id="3791b-216">Step 3: Reserve a Cloud Service VIP (Optional)</span><span class="sxs-lookup"><span data-stu-id="3791b-216">Step 3: Reserve a Cloud Service VIP (Optional)</span></span>
    #check exisitng reserved VIP
    Get-AzureReservedIP

    $reservedVIPName = “sqlcloudVIP”
    New-AzureReservedIP –ReservedIPName $reservedVIPName –Label $reservedVIPName –Location $location

#### <a name="step-4-create-a-vm-container"></a><span data-ttu-id="3791b-217">Step 4: Create a VM Container</span><span class="sxs-lookup"><span data-stu-id="3791b-217">Step 4: Create a VM Container</span></span>
    #Generate storage keys for later
    $xiostorage = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountname

    ##Generate storage acc contexts
    $xioContext = New-AzureStorageContext –StorageAccountName $newxiostorageaccountname -StorageAccountKey $xiostorage.Primary   

    #Create container
    $containerName = 'vhds'
    New-AzureStorageContainer -Name $containerName -Context $xioContext

#### <a name="step-5-placing-os-vhd-on-standard-or-premium-storage"></a><span data-ttu-id="3791b-218">Step 5: Placing OS VHD on Standard or Premium Storage</span><span class="sxs-lookup"><span data-stu-id="3791b-218">Step 5: Placing OS VHD on Standard or Premium Storage</span></span>
    #NOTE: Set up subscription and default storage account which is used to place the OS VHD in

    #If you want to place the OS VHD Premium Storage Account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount  $newxiostorageaccountname  

    #If you wanted to place the OS VHD Standard Storage Account but attach Premium Storage VHDs then you would run this instead:
    $standardstorageaccountname = "danstdams"

    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount  $standardstorageaccountname

#### <a name="step-6-create-vm"></a><span data-ttu-id="3791b-219">Step 6: Create VM</span><span class="sxs-lookup"><span data-stu-id="3791b-219">Step 6: Create VM</span></span>
    #Get list of available SQL Server Images from the Azure Image Gallery.
    $galleryImage = Get-AzureVMImage | where-object {$_.ImageName -like "*SQL*2014*Enterprise*"}
    $image = $galleryImage.ImageName

    #Set up Machine Specific Information
    $vmName = "dsDan1"
    $vnet = "dansvnetwesteur"
    $subnet = "SQL"
    $ipaddr = "192.168.0.8"

    #Remember to change to DS series VM
    $newInstanceSize = "Standard_DS1"

    #create new Avaiability Set
    $availabilitySet = "cloudmigAVAMS"

    #Machine User Credentials
    $userName = "myadmin"
    $pass = "mycomplexpwd4*"

    #Create VM Config
    $vmConfigsl = New-AzureVMConfig -Name $vmName -InstanceSize $newInstanceSize -ImageName $image  -AvailabilitySetName $availabilitySet  ` | Add-AzureProvisioningConfig -Windows ` -AdminUserName $userName -Password $pass | Set-AzureSubnet -SubnetNames $subnet | Set-AzureStaticVNetIP -IPAddress $ipaddr

    #Add Data and Log Disks to VM Config
    #Note the size specified ‘-DiskSizeInGB 1023’, this attaches 2 x P30 Premium Storage Disk Type
    #Utilising the Premium Storage enabled Storage account

    $vmConfigsl | Add-AzureDataDisk -CreateNew -DiskSizeInGB 1023 -LUN 0 -HostCaching "ReadOnly"  -DiskLabel "DataDisk1" -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vmName-data1.vhd"
    $vmConfigsl | Add-AzureDataDisk -CreateNew -DiskSizeInGB 1023 -LUN 1 -HostCaching "None"  -DiskLabel "logDisk1" -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vmName-log1.vhd"

    #Create VM
    $vmConfigsl  | New-AzureVM –ServiceName $destcloudsvc -VNetName $vnet ## Optional (-ReservedIPName $reservedVIPName)  

    #Add RDP Endpoint
    $EndpointNameRDPInt = "3389"
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmName | Add-AzureEndpoint -Name "EndpointNameRDP" -Protocol "TCP" -PublicPort "53385" -LocalPort $EndpointNameRDPInt  | Update-AzureVM

    #Check VHD storage account, these should be in $newxiostorageaccountname
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmName | Get-AzureDataDisk
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmName |Get-AzureOSDisk


### <a name="create-a-new-vm-to-use-premium-storage-with-a-custom-image"></a><span data-ttu-id="3791b-220">Create a new VM to use Premium Storage with a custom image</span><span class="sxs-lookup"><span data-stu-id="3791b-220">Create a new VM to use Premium Storage with a custom image</span></span>
<span data-ttu-id="3791b-221">This scenario demonstrates where you have existing customized images that reside in a Standard Storage account.</span><span class="sxs-lookup"><span data-stu-id="3791b-221">This scenario demonstrates where you have existing customized images that reside in a Standard Storage account.</span></span> <span data-ttu-id="3791b-222">As mentioned if you want to place the OS VHD on Premium Storage you need to copy the image that exists in the Standard Storage account and transfer them to a Premium Storage before it can be used.</span><span class="sxs-lookup"><span data-stu-id="3791b-222">As mentioned if you want to place the OS VHD on Premium Storage you need to copy the image that exists in the Standard Storage account and transfer them to a Premium Storage before it can be used.</span></span> <span data-ttu-id="3791b-223">If you have an image on-premises, you can also use this method to copy that directly to the Premium Storage account.</span><span class="sxs-lookup"><span data-stu-id="3791b-223">If you have an image on-premises, you can also use this method to copy that directly to the Premium Storage account.</span></span>

#### <a name="step-1-create-storage-account"></a><span data-ttu-id="3791b-224">Step 1: Create Storage Account</span><span class="sxs-lookup"><span data-stu-id="3791b-224">Step 1: Create Storage Account</span></span>
    $mysubscription = "DansSubscription"
    $location = "West Europe"

    #Create Premium Storage account
    $newxiostorageaccountname = "danspremsams"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountname -Location $location -Type "Premium_LRS"  

    #Standard Storage account
    $origstorageaccountname = "danstdams"

#### <a name="step-2-create-cloud-service"></a><span data-ttu-id="3791b-225">Step 2 Create Cloud Service</span><span class="sxs-lookup"><span data-stu-id="3791b-225">Step 2 Create Cloud Service</span></span>
    $destcloudsvc = "danNewSvcAms"
    New-AzureService $destcloudsvc -Location $location


#### <a name="step-3-use-existing-image"></a><span data-ttu-id="3791b-226">Step 3: Use existing image</span><span class="sxs-lookup"><span data-stu-id="3791b-226">Step 3: Use existing image</span></span>
<span data-ttu-id="3791b-227">You can use an existing image.</span><span class="sxs-lookup"><span data-stu-id="3791b-227">You can use an existing image.</span></span> <span data-ttu-id="3791b-228">Or, you can [take an image of an existing machine](../classic/capture-image-classic.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3791b-228">Or, you can [take an image of an existing machine](../classic/capture-image-classic.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span> <span data-ttu-id="3791b-229">Note the machine that you image does not have to be DS\* machine.</span><span class="sxs-lookup"><span data-stu-id="3791b-229">Note the machine that you image does not have to be DS\* machine.</span></span> <span data-ttu-id="3791b-230">Once you have the image, the following steps show how to copy it to the Premium Storage account with the **Start-AzureStorageBlobCopy** PowerShell commandlet.</span><span class="sxs-lookup"><span data-stu-id="3791b-230">Once you have the image, the following steps show how to copy it to the Premium Storage account with the **Start-AzureStorageBlobCopy** PowerShell commandlet.</span></span>

    #Get storage account keys:
    #Standard Storage account
    $originalstorage =  Get-AzureStorageKey -StorageAccountName $origstorageaccountname
    #Premium Storage account
    $xiostorage = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountname

    #Set up contexts for the storage accounts:
    $origContext = New-AzureStorageContext  –StorageAccountName $origstorageaccountname -StorageAccountKey $originalstorage.Primary
    $destContext = New-AzureStorageContext  –StorageAccountName $newxiostorageaccountname -StorageAccountKey $xiostorage.Primary  

#### <a name="step-4-copy-blob-between-storage-accounts"></a><span data-ttu-id="3791b-231">Step 4: Copy Blob between Storage Accounts</span><span class="sxs-lookup"><span data-stu-id="3791b-231">Step 4: Copy Blob between Storage Accounts</span></span>
    #Get Image VHD
    $myImageVHD = "dansoldonorsql2k14-os-2015-04-15.vhd"
    $containerName = 'vhds'

    #Copy Blob between accounts
    $blob = Start-AzureStorageBlobCopy -SrcBlob $myImageVHD -SrcContainer $containerName `
    -DestContainer vhds -Destblob "prem-$myImageVHD" `
    -Context $origContext -DestContext $destContext  

#### <a name="step-5-regularly-check-copy-status"></a><span data-ttu-id="3791b-232">Step 5: Regularly check copy status:</span><span class="sxs-lookup"><span data-stu-id="3791b-232">Step 5: Regularly check copy status:</span></span>
    $blob | Get-AzureStorageBlobCopyState

#### <a name="step-6-add-image-disk-to-azure-disk-repository-in-subscription"></a><span data-ttu-id="3791b-233">Step 6: Add Image disk to Azure disk Repository in Subscription</span><span class="sxs-lookup"><span data-stu-id="3791b-233">Step 6: Add Image disk to Azure disk Repository in Subscription</span></span>
    $imageMediaLocation = $destContext.BlobEndPoint+"/"+$myImageVHD
    $newimageName = "prem"+"dansoldonorsql2k14"

    Add-AzureVMImage -ImageName $newimageName -MediaLocation $imageMediaLocation

> [!NOTE]
> <span data-ttu-id="3791b-234">You may find that even though the status reports as success, you could still get a disk lease error.</span><span class="sxs-lookup"><span data-stu-id="3791b-234">You may find that even though the status reports as success, you could still get a disk lease error.</span></span> <span data-ttu-id="3791b-235">In this case, wait about 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="3791b-235">In this case, wait about 10 minutes.</span></span>
>
>

#### <a name="step-7--build-the-vm"></a><span data-ttu-id="3791b-236">Step 7:  Build the VM</span><span class="sxs-lookup"><span data-stu-id="3791b-236">Step 7:  Build the VM</span></span>
<span data-ttu-id="3791b-237">Here you are building the VM from your image and attaching two Premium Storage VHDs:</span><span class="sxs-lookup"><span data-stu-id="3791b-237">Here you are building the VM from your image and attaching two Premium Storage VHDs:</span></span>

    $newimageName = "prem"+"dansoldonorsql2k14"
    #Set up Machine Specific Information
    $vmName = "dansolchild"
    $vnet = "westeur"
    $subnet = "Clients"
    $ipaddr = "192.168.0.41"

    #This needs to be a new cloud service
    $destcloudsvc = "danregsvcamsxio2"

    #Use to DS Series VM
    $newInstanceSize = "Standard_DS1"

    #create new Avaiability Set
    $availabilitySet = "cloudmigAVAMS3"

    #Machine User Credentials
    $userName = "myadmin"
    $pass = "theM)stC0mplexP@ssw0rd!”


    #Create VM Config
    $vmConfigsl2 = New-AzureVMConfig -Name $vmName -InstanceSize $newInstanceSize -ImageName $newimageName  -AvailabilitySetName $availabilitySet  ` | Add-AzureProvisioningConfig -Windows ` -AdminUserName $userName -Password $pass | Set-AzureSubnet -SubnetNames $subnet | Set-AzureStaticVNetIP -IPAddress $ipaddr

    $vmConfigsl2 | Add-AzureDataDisk -CreateNew -DiskSizeInGB 1023 -LUN 0 -HostCaching "ReadOnly"  -DiskLabel "DataDisk1" -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vmName-Datadisk-1.vhd"
    $vmConfigsl2 | Add-AzureDataDisk -CreateNew -DiskSizeInGB 1023 -LUN 1 -HostCaching "None"  -DiskLabel "LogDisk1" -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vmName-logdisk-1.vhd"



    $vmConfigsl2 | New-AzureVM –ServiceName $destcloudsvc -VNetName $vnet

## <a name="existing-deployments-that-do-not-use-always-on-availability-groups"></a><span data-ttu-id="3791b-238">Existing deployments that do not use Always On Availability Groups</span><span class="sxs-lookup"><span data-stu-id="3791b-238">Existing deployments that do not use Always On Availability Groups</span></span>
> [!NOTE]
> <span data-ttu-id="3791b-239">For existing deployments, first see the [Prerequisites](#prerequisites-for-premium-storage) section of this article.</span><span class="sxs-lookup"><span data-stu-id="3791b-239">For existing deployments, first see the [Prerequisites](#prerequisites-for-premium-storage) section of this article.</span></span>
>
>

<span data-ttu-id="3791b-240">There are different considerations for SQL Server deployments that do not use Always On Availability Groups and those that do.</span><span class="sxs-lookup"><span data-stu-id="3791b-240">There are different considerations for SQL Server deployments that do not use Always On Availability Groups and those that do.</span></span> <span data-ttu-id="3791b-241">If you are not using Always On and have an existing standalone SQL Server, you can upgrade to Premium Storage by using a new cloud service and storage account.</span><span class="sxs-lookup"><span data-stu-id="3791b-241">If you are not using Always On and have an existing standalone SQL Server, you can upgrade to Premium Storage by using a new cloud service and storage account.</span></span> <span data-ttu-id="3791b-242">Consider the following options:</span><span class="sxs-lookup"><span data-stu-id="3791b-242">Consider the following options:</span></span>

* <span data-ttu-id="3791b-243">**Create a new SQL Server VM**.</span><span class="sxs-lookup"><span data-stu-id="3791b-243">**Create a new SQL Server VM**.</span></span> <span data-ttu-id="3791b-244">You can create a new SQL Server VM that uses a Premium Storage account, as documented in New Deployments.</span><span class="sxs-lookup"><span data-stu-id="3791b-244">You can create a new SQL Server VM that uses a Premium Storage account, as documented in New Deployments.</span></span> <span data-ttu-id="3791b-245">Then back up and restore your SQL Server configuration and user databases.</span><span class="sxs-lookup"><span data-stu-id="3791b-245">Then back up and restore your SQL Server configuration and user databases.</span></span> <span data-ttu-id="3791b-246">The application needs to be updated to reference the new SQL Server if it is being accessed internally or externally.</span><span class="sxs-lookup"><span data-stu-id="3791b-246">The application needs to be updated to reference the new SQL Server if it is being accessed internally or externally.</span></span> <span data-ttu-id="3791b-247">You would need to copy all ‘out of db’ objects as if you were doing a Side by Side (SxS) SQL Server migration.</span><span class="sxs-lookup"><span data-stu-id="3791b-247">You would need to copy all ‘out of db’ objects as if you were doing a Side by Side (SxS) SQL Server migration.</span></span> <span data-ttu-id="3791b-248">This includes objects such as logins, certificates, and linked servers.</span><span class="sxs-lookup"><span data-stu-id="3791b-248">This includes objects such as logins, certificates, and linked servers.</span></span>
* <span data-ttu-id="3791b-249">**Migrate an existing SQL Server VM**.</span><span class="sxs-lookup"><span data-stu-id="3791b-249">**Migrate an existing SQL Server VM**.</span></span> <span data-ttu-id="3791b-250">This requires taking the SQL Server VM offline, then transferring it to a new cloud service, which includes copying all of its attached VHDs to the Premium Storage account.</span><span class="sxs-lookup"><span data-stu-id="3791b-250">This requires taking the SQL Server VM offline, then transferring it to a new cloud service, which includes copying all of its attached VHDs to the Premium Storage account.</span></span> <span data-ttu-id="3791b-251">When the VM comes online, the application references the server host name as before.</span><span class="sxs-lookup"><span data-stu-id="3791b-251">When the VM comes online, the application references the server host name as before.</span></span> <span data-ttu-id="3791b-252">Be aware that the size of the existing disk affects the performance characteristics.</span><span class="sxs-lookup"><span data-stu-id="3791b-252">Be aware that the size of the existing disk affects the performance characteristics.</span></span> <span data-ttu-id="3791b-253">For example, a 400 GB disk gets rounded up to a P20.</span><span class="sxs-lookup"><span data-stu-id="3791b-253">For example, a 400 GB disk gets rounded up to a P20.</span></span> <span data-ttu-id="3791b-254">If you know that you do not require that disk performance, then you could recreate the VM as a DS Series VM, and attach Premium Storage VHDs of the size/performance specification you require.</span><span class="sxs-lookup"><span data-stu-id="3791b-254">If you know that you do not require that disk performance, then you could recreate the VM as a DS Series VM, and attach Premium Storage VHDs of the size/performance specification you require.</span></span> <span data-ttu-id="3791b-255">Then you could detach and reattach the SQL DB files.</span><span class="sxs-lookup"><span data-stu-id="3791b-255">Then you could detach and reattach the SQL DB files.</span></span>

> [!NOTE]
> <span data-ttu-id="3791b-256">When copying the VHD disks you should be aware of the size, depending on the size means what Premium Storage Disk type they fall into, this determines disk performance specification.</span><span class="sxs-lookup"><span data-stu-id="3791b-256">When copying the VHD disks you should be aware of the size, depending on the size means what Premium Storage Disk type they fall into, this determines disk performance specification.</span></span> <span data-ttu-id="3791b-257">Azure rounds up to the nearest disk size, so if you have a 400GB disk, this is rounded up to a P20.</span><span class="sxs-lookup"><span data-stu-id="3791b-257">Azure rounds up to the nearest disk size, so if you have a 400GB disk, this is rounded up to a P20.</span></span> <span data-ttu-id="3791b-258">Depending on your existing IO requirements of the OS VHD, you might not need to migrate this to a Premium Storage account.</span><span class="sxs-lookup"><span data-stu-id="3791b-258">Depending on your existing IO requirements of the OS VHD, you might not need to migrate this to a Premium Storage account.</span></span>
>
>

<span data-ttu-id="3791b-259">If your SQL Server is accessed externally, then the cloud service VIP changes.</span><span class="sxs-lookup"><span data-stu-id="3791b-259">If your SQL Server is accessed externally, then the cloud service VIP changes.</span></span> <span data-ttu-id="3791b-260">You also have to update end points, ACLs, and DNS settings.</span><span class="sxs-lookup"><span data-stu-id="3791b-260">You also have to update end points, ACLs, and DNS settings.</span></span>

## <a name="existing-deployments-that-use-always-on-availability-groups"></a><span data-ttu-id="3791b-261">Existing deployments that use Always On Availability Groups</span><span class="sxs-lookup"><span data-stu-id="3791b-261">Existing deployments that use Always On Availability Groups</span></span>
> [!NOTE]
> <span data-ttu-id="3791b-262">For existing deployments, first see the [Prerequisites](#prerequisites-for-premium-storage) section of this article.</span><span class="sxs-lookup"><span data-stu-id="3791b-262">For existing deployments, first see the [Prerequisites](#prerequisites-for-premium-storage) section of this article.</span></span>
>
>

<span data-ttu-id="3791b-263">Initially in this section we look at how Always On interacts with Azure Networking.</span><span class="sxs-lookup"><span data-stu-id="3791b-263">Initially in this section we look at how Always On interacts with Azure Networking.</span></span> <span data-ttu-id="3791b-264">We then break down migrations in to two scenarios: migrations where some downtime can be tolerated and migrations where you must achieve minimal downtime.</span><span class="sxs-lookup"><span data-stu-id="3791b-264">We then break down migrations in to two scenarios: migrations where some downtime can be tolerated and migrations where you must achieve minimal downtime.</span></span>

<span data-ttu-id="3791b-265">On-premises SQL Server Always On Availability Groups use a Listener on-premises that registers a virtual DNS name along with an IP address that is shared between one or more SQL Servers.</span><span class="sxs-lookup"><span data-stu-id="3791b-265">On-premises SQL Server Always On Availability Groups use a Listener on-premises that registers a virtual DNS name along with an IP address that is shared between one or more SQL Servers.</span></span> <span data-ttu-id="3791b-266">When clients connect they are routed through the listener IP to the Primary SQL Server.</span><span class="sxs-lookup"><span data-stu-id="3791b-266">When clients connect they are routed through the listener IP to the Primary SQL Server.</span></span> <span data-ttu-id="3791b-267">This is the server that owns the Always On IP resource at that time.</span><span class="sxs-lookup"><span data-stu-id="3791b-267">This is the server that owns the Always On IP resource at that time.</span></span>

![DeploymentsUseAlways On][6]

<span data-ttu-id="3791b-269">In Microsoft Azure you can have only one IP address assigned to a NIC on the VM, so in order to achieve the same layer of abstraction as on-premises, Azure utilizes the IP address that is assigned to the Internal/External Load Balancers (ILB/ELB).</span><span class="sxs-lookup"><span data-stu-id="3791b-269">In Microsoft Azure you can have only one IP address assigned to a NIC on the VM, so in order to achieve the same layer of abstraction as on-premises, Azure utilizes the IP address that is assigned to the Internal/External Load Balancers (ILB/ELB).</span></span> <span data-ttu-id="3791b-270">The IP resource that is shared between the servers is set to the same IP as the ILB/ELB.</span><span class="sxs-lookup"><span data-stu-id="3791b-270">The IP resource that is shared between the servers is set to the same IP as the ILB/ELB.</span></span> <span data-ttu-id="3791b-271">This is published in the DNS, and client traffic is passed through the ILB/ELB to the Primary SQL Server replica.</span><span class="sxs-lookup"><span data-stu-id="3791b-271">This is published in the DNS, and client traffic is passed through the ILB/ELB to the Primary SQL Server replica.</span></span> <span data-ttu-id="3791b-272">The ILB/ELB knows which SQL Server is primary since it uses probes to probe the Always On IP resource.</span><span class="sxs-lookup"><span data-stu-id="3791b-272">The ILB/ELB knows which SQL Server is primary since it uses probes to probe the Always On IP resource.</span></span> <span data-ttu-id="3791b-273">In the previous example, it probes each node that has an endpoint referenced by the ELB/ILB, whichever responds is the Primary SQL Server.</span><span class="sxs-lookup"><span data-stu-id="3791b-273">In the previous example, it probes each node that has an endpoint referenced by the ELB/ILB, whichever responds is the Primary SQL Server.</span></span>

> [!NOTE]
> <span data-ttu-id="3791b-274">The ILB and ELB are both assigned to a particular Azure cloud service, therefore any cloud migration in Azure most likely means that the Load Balancer IP changes.</span><span class="sxs-lookup"><span data-stu-id="3791b-274">The ILB and ELB are both assigned to a particular Azure cloud service, therefore any cloud migration in Azure most likely means that the Load Balancer IP changes.</span></span>
>
>

### <a name="migrating-always-on-deployments-that-can-allow-some-downtime"></a><span data-ttu-id="3791b-275">Migrating Always On deployments that can allow some downtime</span><span class="sxs-lookup"><span data-stu-id="3791b-275">Migrating Always On deployments that can allow some downtime</span></span>
<span data-ttu-id="3791b-276">There are two strategies to migrate Always On deployments that allow for some downtime:</span><span class="sxs-lookup"><span data-stu-id="3791b-276">There are two strategies to migrate Always On deployments that allow for some downtime:</span></span>

1. <span data-ttu-id="3791b-277">**Add more secondary replicas to an existing Always On Cluster**</span><span class="sxs-lookup"><span data-stu-id="3791b-277">**Add more secondary replicas to an existing Always On Cluster**</span></span>
2. <span data-ttu-id="3791b-278">**Migrate to a new Always On Cluster**</span><span class="sxs-lookup"><span data-stu-id="3791b-278">**Migrate to a new Always On Cluster**</span></span>

#### <a name="1-add-more-secondary-replicas-to-an-existing-always-on-cluster"></a><span data-ttu-id="3791b-279">1. Add more Secondary Replicas to an Existing Always On Cluster</span><span class="sxs-lookup"><span data-stu-id="3791b-279">1. Add more Secondary Replicas to an Existing Always On Cluster</span></span>
<span data-ttu-id="3791b-280">One strategy is to add more secondaries to the Always On Availability Group.</span><span class="sxs-lookup"><span data-stu-id="3791b-280">One strategy is to add more secondaries to the Always On Availability Group.</span></span> <span data-ttu-id="3791b-281">You need to add these into a new cloud service and update the listener with the new load balancer IP.</span><span class="sxs-lookup"><span data-stu-id="3791b-281">You need to add these into a new cloud service and update the listener with the new load balancer IP.</span></span>

##### <a name="points-of-downtime"></a><span data-ttu-id="3791b-282">Points of downtime:</span><span class="sxs-lookup"><span data-stu-id="3791b-282">Points of downtime:</span></span>
* <span data-ttu-id="3791b-283">Cluster Validation.</span><span class="sxs-lookup"><span data-stu-id="3791b-283">Cluster Validation.</span></span>
* <span data-ttu-id="3791b-284">Testing Always On failovers for New Secondaries.</span><span class="sxs-lookup"><span data-stu-id="3791b-284">Testing Always On failovers for New Secondaries.</span></span>

<span data-ttu-id="3791b-285">If you are using Windows Storage Pools within the VM for higher IO throughput, then these are taken offline during a Full Cluster Validation.</span><span class="sxs-lookup"><span data-stu-id="3791b-285">If you are using Windows Storage Pools within the VM for higher IO throughput, then these are taken offline during a Full Cluster Validation.</span></span> <span data-ttu-id="3791b-286">The validation test is required when you add nodes to the cluster.</span><span class="sxs-lookup"><span data-stu-id="3791b-286">The validation test is required when you add nodes to the cluster.</span></span> <span data-ttu-id="3791b-287">The time it takes to run the test can vary, so you should test this in your representative test environment to get an approximate time of how long this takes.</span><span class="sxs-lookup"><span data-stu-id="3791b-287">The time it takes to run the test can vary, so you should test this in your representative test environment to get an approximate time of how long this takes.</span></span>

<span data-ttu-id="3791b-288">You should provision time where you can perform manual failover and chaos testing on the newly added nodes to ensure Always On High Availability functions as expected.</span><span class="sxs-lookup"><span data-stu-id="3791b-288">You should provision time where you can perform manual failover and chaos testing on the newly added nodes to ensure Always On High Availability functions as expected.</span></span>

![DeploymentUseAlways On2][7]

> [!NOTE]
> <span data-ttu-id="3791b-290">You should stop all instances of SQL Server where the Storage Pools are used before the Validation runs.</span><span class="sxs-lookup"><span data-stu-id="3791b-290">You should stop all instances of SQL Server where the Storage Pools are used before the Validation runs.</span></span>
>
> ##### <a name="high-level-steps"></a><span data-ttu-id="3791b-291">High-level steps</span><span class="sxs-lookup"><span data-stu-id="3791b-291">High-level steps</span></span>
>

1. <span data-ttu-id="3791b-292">Create two new SQL Servers in new cloud service with attached Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="3791b-292">Create two new SQL Servers in new cloud service with attached Premium Storage.</span></span>
2. <span data-ttu-id="3791b-293">Copy over FULL backups and restore with **NORECOVERY**.</span><span class="sxs-lookup"><span data-stu-id="3791b-293">Copy over FULL backups and restore with **NORECOVERY**.</span></span>
3. <span data-ttu-id="3791b-294">Copy over ‘out of user DB’ dependent objects, such as logins etc.</span><span class="sxs-lookup"><span data-stu-id="3791b-294">Copy over ‘out of user DB’ dependent objects, such as logins etc.</span></span>
4. <span data-ttu-id="3791b-295">Create new a new Internal Load Balancer (ILB) or use an External Load Balancer (ELB), and then set up Load Balanced Endpoints on both new nodes.</span><span class="sxs-lookup"><span data-stu-id="3791b-295">Create new a new Internal Load Balancer (ILB) or use an External Load Balancer (ELB), and then set up Load Balanced Endpoints on both new nodes.</span></span>

   > [!NOTE]
   > <span data-ttu-id="3791b-296">Check all Nodes have the correct Endpoint configuration before you continue</span><span class="sxs-lookup"><span data-stu-id="3791b-296">Check all Nodes have the correct Endpoint configuration before you continue</span></span>
   >
   >
5. <span data-ttu-id="3791b-297">Stop User/Application Access to the SQL Server (if using Storage Pools).</span><span class="sxs-lookup"><span data-stu-id="3791b-297">Stop User/Application Access to the SQL Server (if using Storage Pools).</span></span>
6. <span data-ttu-id="3791b-298">Stop SQL Server Engine Services on All Nodes (if using Storage Pools).</span><span class="sxs-lookup"><span data-stu-id="3791b-298">Stop SQL Server Engine Services on All Nodes (if using Storage Pools).</span></span>
7. <span data-ttu-id="3791b-299">Add new Nodes to cluster and run full validation.</span><span class="sxs-lookup"><span data-stu-id="3791b-299">Add new Nodes to cluster and run full validation.</span></span>
8. <span data-ttu-id="3791b-300">Once Validation is successful, start all SQL Server Services.</span><span class="sxs-lookup"><span data-stu-id="3791b-300">Once Validation is successful, start all SQL Server Services.</span></span>
9. <span data-ttu-id="3791b-301">Backup Transaction logs, and restore user databases.</span><span class="sxs-lookup"><span data-stu-id="3791b-301">Backup Transaction logs, and restore user databases.</span></span>
10. <span data-ttu-id="3791b-302">Add new nodes into the Always On Availability Group and place replication into **Synchronous**.</span><span class="sxs-lookup"><span data-stu-id="3791b-302">Add new nodes into the Always On Availability Group and place replication into **Synchronous**.</span></span>
11. <span data-ttu-id="3791b-303">Add the IP address resource of the new Cloud Service ILB/ELB through PowerShell for Always On based on the Multi-site example in the [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span><span class="sxs-lookup"><span data-stu-id="3791b-303">Add the IP address resource of the new Cloud Service ILB/ELB through PowerShell for Always On based on the Multi-site example in the [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span></span> <span data-ttu-id="3791b-304">In Windows clustering, set the **Possible owners** of the **IP Address** resource to the new nodes old.</span><span class="sxs-lookup"><span data-stu-id="3791b-304">In Windows clustering, set the **Possible owners** of the **IP Address** resource to the new nodes old.</span></span> <span data-ttu-id="3791b-305">See the ‘Adding IP Address Resource on Same Subnet’ section of the [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span><span class="sxs-lookup"><span data-stu-id="3791b-305">See the ‘Adding IP Address Resource on Same Subnet’ section of the [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span></span>
12. <span data-ttu-id="3791b-306">Failover to one of the new nodes.</span><span class="sxs-lookup"><span data-stu-id="3791b-306">Failover to one of the new nodes.</span></span>
13. <span data-ttu-id="3791b-307">Make the new nodes Auto Failover Partners and test failovers.</span><span class="sxs-lookup"><span data-stu-id="3791b-307">Make the new nodes Auto Failover Partners and test failovers.</span></span>
14. <span data-ttu-id="3791b-308">Remove original nodes from Availability Group.</span><span class="sxs-lookup"><span data-stu-id="3791b-308">Remove original nodes from Availability Group.</span></span>

##### <a name="advantages"></a><span data-ttu-id="3791b-309">Advantages</span><span class="sxs-lookup"><span data-stu-id="3791b-309">Advantages</span></span>
* <span data-ttu-id="3791b-310">New SQL Servers can be tested (SQL Server and Application) before they are added to Always On.</span><span class="sxs-lookup"><span data-stu-id="3791b-310">New SQL Servers can be tested (SQL Server and Application) before they are added to Always On.</span></span>
* <span data-ttu-id="3791b-311">You can change the VM size and customize the storage to your exact requirements.</span><span class="sxs-lookup"><span data-stu-id="3791b-311">You can change the VM size and customize the storage to your exact requirements.</span></span> <span data-ttu-id="3791b-312">However, it would be beneficial to keep all the SQL file paths the same.</span><span class="sxs-lookup"><span data-stu-id="3791b-312">However, it would be beneficial to keep all the SQL file paths the same.</span></span>
* <span data-ttu-id="3791b-313">You can control when the transfer of the DB backups to the Secondary Replicas is started.</span><span class="sxs-lookup"><span data-stu-id="3791b-313">You can control when the transfer of the DB backups to the Secondary Replicas is started.</span></span> <span data-ttu-id="3791b-314">This differs from using Azure **Start-AzureStorageBlobCopy** commandlet to copy VHDs, because that is an asynchronous copy.</span><span class="sxs-lookup"><span data-stu-id="3791b-314">This differs from using Azure **Start-AzureStorageBlobCopy** commandlet to copy VHDs, because that is an asynchronous copy.</span></span>

##### <a name="disadvantages"></a><span data-ttu-id="3791b-315">Disadvantages</span><span class="sxs-lookup"><span data-stu-id="3791b-315">Disadvantages</span></span>
* <span data-ttu-id="3791b-316">When using Windows Storage Pools, there is Cluster downtime during the Full Cluster Validation for the new additional nodes.</span><span class="sxs-lookup"><span data-stu-id="3791b-316">When using Windows Storage Pools, there is Cluster downtime during the Full Cluster Validation for the new additional nodes.</span></span>
* <span data-ttu-id="3791b-317">Depending on the SQL Server Version and the existing number of secondary replicas, you might not be able to add more secondary replicas without removing existing secondaries.</span><span class="sxs-lookup"><span data-stu-id="3791b-317">Depending on the SQL Server Version and the existing number of secondary replicas, you might not be able to add more secondary replicas without removing existing secondaries.</span></span>
* <span data-ttu-id="3791b-318">There could be long SQL data transfer time while setting up the secondaries.</span><span class="sxs-lookup"><span data-stu-id="3791b-318">There could be long SQL data transfer time while setting up the secondaries.</span></span>
* <span data-ttu-id="3791b-319">There is additional cost during migration while you have new machines running in parallel.</span><span class="sxs-lookup"><span data-stu-id="3791b-319">There is additional cost during migration while you have new machines running in parallel.</span></span>

#### <a name="2-migrate-to-a-new-always-on-cluster"></a><span data-ttu-id="3791b-320">2. Migrate to a new Always On Cluster</span><span class="sxs-lookup"><span data-stu-id="3791b-320">2. Migrate to a new Always On Cluster</span></span>
<span data-ttu-id="3791b-321">Another strategy is to create a brand new Always On Cluster with brand new nodes in new cloud service and then redirect the clients to use it.</span><span class="sxs-lookup"><span data-stu-id="3791b-321">Another strategy is to create a brand new Always On Cluster with brand new nodes in new cloud service and then redirect the clients to use it.</span></span>

##### <a name="points-of-downtime"></a><span data-ttu-id="3791b-322">Points of downtime</span><span class="sxs-lookup"><span data-stu-id="3791b-322">Points of downtime</span></span>
<span data-ttu-id="3791b-323">There is downtime when you transfer applications and users to the new Always On listener.</span><span class="sxs-lookup"><span data-stu-id="3791b-323">There is downtime when you transfer applications and users to the new Always On listener.</span></span> <span data-ttu-id="3791b-324">The downtime depends on:</span><span class="sxs-lookup"><span data-stu-id="3791b-324">The downtime depends on:</span></span>

* <span data-ttu-id="3791b-325">The time taken to restore final transaction log backups to databases on new servers.</span><span class="sxs-lookup"><span data-stu-id="3791b-325">The time taken to restore final transaction log backups to databases on new servers.</span></span>
* <span data-ttu-id="3791b-326">The time taken to update client applications to use new Always On listener.</span><span class="sxs-lookup"><span data-stu-id="3791b-326">The time taken to update client applications to use new Always On listener.</span></span>

##### <a name="advantages"></a><span data-ttu-id="3791b-327">Advantages</span><span class="sxs-lookup"><span data-stu-id="3791b-327">Advantages</span></span>
* <span data-ttu-id="3791b-328">You can test the actual production environment, SQL Server, and OS build changes.</span><span class="sxs-lookup"><span data-stu-id="3791b-328">You can test the actual production environment, SQL Server, and OS build changes.</span></span>
* <span data-ttu-id="3791b-329">You have the option to customize the storage and to potentially reduce size of VM.</span><span class="sxs-lookup"><span data-stu-id="3791b-329">You have the option to customize the storage and to potentially reduce size of VM.</span></span> <span data-ttu-id="3791b-330">This could result in cost reduction.</span><span class="sxs-lookup"><span data-stu-id="3791b-330">This could result in cost reduction.</span></span>
* <span data-ttu-id="3791b-331">You can update your SQL Server build or version during this process.</span><span class="sxs-lookup"><span data-stu-id="3791b-331">You can update your SQL Server build or version during this process.</span></span> <span data-ttu-id="3791b-332">You can also upgrade the Operating System.</span><span class="sxs-lookup"><span data-stu-id="3791b-332">You can also upgrade the Operating System.</span></span>
* <span data-ttu-id="3791b-333">The previous Always On Cluster can act as a solid rollback target.</span><span class="sxs-lookup"><span data-stu-id="3791b-333">The previous Always On Cluster can act as a solid rollback target.</span></span>

##### <a name="disadvantages"></a><span data-ttu-id="3791b-334">Disadvantages</span><span class="sxs-lookup"><span data-stu-id="3791b-334">Disadvantages</span></span>
* <span data-ttu-id="3791b-335">You need to change the DNS name of the listener if you want both Always On clusters running simultaneously.</span><span class="sxs-lookup"><span data-stu-id="3791b-335">You need to change the DNS name of the listener if you want both Always On clusters running simultaneously.</span></span> <span data-ttu-id="3791b-336">This adds administration overhead during the migration as client application strings must reflect the new Listener name.</span><span class="sxs-lookup"><span data-stu-id="3791b-336">This adds administration overhead during the migration as client application strings must reflect the new Listener name.</span></span>
* <span data-ttu-id="3791b-337">You must implement a synchronization mechanism between the two environments to keep them as close as possible to minimize the final synchronization requirements before migration.</span><span class="sxs-lookup"><span data-stu-id="3791b-337">You must implement a synchronization mechanism between the two environments to keep them as close as possible to minimize the final synchronization requirements before migration.</span></span>
* <span data-ttu-id="3791b-338">There is added cost during migration while you have the new environment running.</span><span class="sxs-lookup"><span data-stu-id="3791b-338">There is added cost during migration while you have the new environment running.</span></span>

### <a name="migrating-always-on-deployments-for-minimal-downtime"></a><span data-ttu-id="3791b-339">Migrating Always On Deployments for minimal downtime</span><span class="sxs-lookup"><span data-stu-id="3791b-339">Migrating Always On Deployments for minimal downtime</span></span>
<span data-ttu-id="3791b-340">There are two strategies for migrating Always On deployments for minimal downtime:</span><span class="sxs-lookup"><span data-stu-id="3791b-340">There are two strategies for migrating Always On deployments for minimal downtime:</span></span>

1. <span data-ttu-id="3791b-341">**Utilize an Existing Secondary: Single-Site**</span><span class="sxs-lookup"><span data-stu-id="3791b-341">**Utilize an Existing Secondary: Single-Site**</span></span>
2. <span data-ttu-id="3791b-342">**Utilize Existing Secondary Replica(s): Multi-Site**</span><span class="sxs-lookup"><span data-stu-id="3791b-342">**Utilize Existing Secondary Replica(s): Multi-Site**</span></span>

#### <a name="1-utilize-an-existing-secondary-single-site"></a><span data-ttu-id="3791b-343">1. Utilize an existing secondary: Single-Site</span><span class="sxs-lookup"><span data-stu-id="3791b-343">1. Utilize an existing secondary: Single-Site</span></span>
<span data-ttu-id="3791b-344">One strategy for minimal downtime is to take an existing cloud secondary and remove it from the current cloud service.</span><span class="sxs-lookup"><span data-stu-id="3791b-344">One strategy for minimal downtime is to take an existing cloud secondary and remove it from the current cloud service.</span></span> <span data-ttu-id="3791b-345">Then copy the VHDs to the new Premium Storage account, and create the VM in the new cloud service.</span><span class="sxs-lookup"><span data-stu-id="3791b-345">Then copy the VHDs to the new Premium Storage account, and create the VM in the new cloud service.</span></span> <span data-ttu-id="3791b-346">Then update the listener in clustering and failover.</span><span class="sxs-lookup"><span data-stu-id="3791b-346">Then update the listener in clustering and failover.</span></span>

##### <a name="points-of-downtime"></a><span data-ttu-id="3791b-347">Points of downtime</span><span class="sxs-lookup"><span data-stu-id="3791b-347">Points of downtime</span></span>
* <span data-ttu-id="3791b-348">There is downtime when you update the final node with the Load Balanced endpoint.</span><span class="sxs-lookup"><span data-stu-id="3791b-348">There is downtime when you update the final node with the Load Balanced endpoint.</span></span>
* <span data-ttu-id="3791b-349">Your client reconnection might be delayed depending on your client/DNS configuration.</span><span class="sxs-lookup"><span data-stu-id="3791b-349">Your client reconnection might be delayed depending on your client/DNS configuration.</span></span>
* <span data-ttu-id="3791b-350">There is additional downtime if you choose to take the Always On Cluster group offline to swap out the IP addresses.</span><span class="sxs-lookup"><span data-stu-id="3791b-350">There is additional downtime if you choose to take the Always On Cluster group offline to swap out the IP addresses.</span></span> <span data-ttu-id="3791b-351">You can avoid this by using an OR dependency and Possible Owners for the added IP Address resource.</span><span class="sxs-lookup"><span data-stu-id="3791b-351">You can avoid this by using an OR dependency and Possible Owners for the added IP Address resource.</span></span> <span data-ttu-id="3791b-352">See the ‘Adding IP Address Resource on Same Subnet’ section of the [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span><span class="sxs-lookup"><span data-stu-id="3791b-352">See the ‘Adding IP Address Resource on Same Subnet’ section of the [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span></span>

> [!NOTE]
> <span data-ttu-id="3791b-353">When you want the added node to partake in as an Always On Failover Partner, you need to add an Azure Endpoint with a reference to the Load Balanced Set.</span><span class="sxs-lookup"><span data-stu-id="3791b-353">When you want the added node to partake in as an Always On Failover Partner, you need to add an Azure Endpoint with a reference to the Load Balanced Set.</span></span> <span data-ttu-id="3791b-354">When you run the **Add-AzureEndpoint** command to do this, current connections to remain open, but new connections to the listener are not able to be established until the load balancer has updated.</span><span class="sxs-lookup"><span data-stu-id="3791b-354">When you run the **Add-AzureEndpoint** command to do this, current connections to remain open, but new connections to the listener are not able to be established until the load balancer has updated.</span></span> <span data-ttu-id="3791b-355">In testing this was seen to last 90-120seconds, this should be tested.</span><span class="sxs-lookup"><span data-stu-id="3791b-355">In testing this was seen to last 90-120seconds, this should be tested.</span></span>
>
>

##### <a name="advantages"></a><span data-ttu-id="3791b-356">Advantages</span><span class="sxs-lookup"><span data-stu-id="3791b-356">Advantages</span></span>
* <span data-ttu-id="3791b-357">No extra cost incurred during migration.</span><span class="sxs-lookup"><span data-stu-id="3791b-357">No extra cost incurred during migration.</span></span>
* <span data-ttu-id="3791b-358">A one-to-one migration.</span><span class="sxs-lookup"><span data-stu-id="3791b-358">A one-to-one migration.</span></span>
* <span data-ttu-id="3791b-359">Reduced complexity.</span><span class="sxs-lookup"><span data-stu-id="3791b-359">Reduced complexity.</span></span>
* <span data-ttu-id="3791b-360">Allows for increased IOPS from Premium Storage SKUs.</span><span class="sxs-lookup"><span data-stu-id="3791b-360">Allows for increased IOPS from Premium Storage SKUs.</span></span> <span data-ttu-id="3791b-361">When the disks are detached from the VM and copied to the new cloud service, a 3rd party tool can be used to increase the VHD size, which provides higher throughputs.</span><span class="sxs-lookup"><span data-stu-id="3791b-361">When the disks are detached from the VM and copied to the new cloud service, a 3rd party tool can be used to increase the VHD size, which provides higher throughputs.</span></span> <span data-ttu-id="3791b-362">For increasing VHD sizes, see this [forum discussion](https://social.msdn.microsoft.com/Forums/azure/4a9bcc9e-e5bf-4125-9994-7c154c9b0d52/resizing-azure-data-disk?forum=WAVirtualMachinesforWindows).</span><span class="sxs-lookup"><span data-stu-id="3791b-362">For increasing VHD sizes, see this [forum discussion](https://social.msdn.microsoft.com/Forums/azure/4a9bcc9e-e5bf-4125-9994-7c154c9b0d52/resizing-azure-data-disk?forum=WAVirtualMachinesforWindows).</span></span>

##### <a name="disadvantages"></a><span data-ttu-id="3791b-363">Disadvantages</span><span class="sxs-lookup"><span data-stu-id="3791b-363">Disadvantages</span></span>
* <span data-ttu-id="3791b-364">There is a temporary loss of HA and DR during migration.</span><span class="sxs-lookup"><span data-stu-id="3791b-364">There is a temporary loss of HA and DR during migration.</span></span>
* <span data-ttu-id="3791b-365">As this is a 1:1 migration, you have to use a minimum VM size that supports your number of VHDs, so you might not be able to downsize your VMs.</span><span class="sxs-lookup"><span data-stu-id="3791b-365">As this is a 1:1 migration, you have to use a minimum VM size that supports your number of VHDs, so you might not be able to downsize your VMs.</span></span>
* <span data-ttu-id="3791b-366">This scenario would use the Azure **Start-AzureStorageBlobCopy** commandlet, which is asynchronous.</span><span class="sxs-lookup"><span data-stu-id="3791b-366">This scenario would use the Azure **Start-AzureStorageBlobCopy** commandlet, which is asynchronous.</span></span> <span data-ttu-id="3791b-367">There is no SLA on copy completion.</span><span class="sxs-lookup"><span data-stu-id="3791b-367">There is no SLA on copy completion.</span></span> <span data-ttu-id="3791b-368">The time of the copies varies, while this depends on wait in queue it also depends on the amount of data to transfer.</span><span class="sxs-lookup"><span data-stu-id="3791b-368">The time of the copies varies, while this depends on wait in queue it also depends on the amount of data to transfer.</span></span> <span data-ttu-id="3791b-369">The copy time increases if the transfer is going to another Azure data center that supports Premium Storage in another region.</span><span class="sxs-lookup"><span data-stu-id="3791b-369">The copy time increases if the transfer is going to another Azure data center that supports Premium Storage in another region.</span></span> <span data-ttu-id="3791b-370">If you just have 2 nodes, consider a possible mitigation in case the copy takes longer than in testing.</span><span class="sxs-lookup"><span data-stu-id="3791b-370">If you just have 2 nodes, consider a possible mitigation in case the copy takes longer than in testing.</span></span> <span data-ttu-id="3791b-371">This could include the following ideas.</span><span class="sxs-lookup"><span data-stu-id="3791b-371">This could include the following ideas.</span></span>
  * <span data-ttu-id="3791b-372">Add a temporary 3rd SQL Server node for HA before the migration with agreed downtime.</span><span class="sxs-lookup"><span data-stu-id="3791b-372">Add a temporary 3rd SQL Server node for HA before the migration with agreed downtime.</span></span>
  * <span data-ttu-id="3791b-373">Run the migration outside of Azure scheduled maintenance.</span><span class="sxs-lookup"><span data-stu-id="3791b-373">Run the migration outside of Azure scheduled maintenance.</span></span>
  * <span data-ttu-id="3791b-374">Ensure you have configured your cluster quorum correctly.</span><span class="sxs-lookup"><span data-stu-id="3791b-374">Ensure you have configured your cluster quorum correctly.</span></span>  

##### <a name="high-level-steps"></a><span data-ttu-id="3791b-375">High-level steps</span><span class="sxs-lookup"><span data-stu-id="3791b-375">High-level steps</span></span>
<span data-ttu-id="3791b-376">This document does not demonstrate a complete end to end example, however the [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) provides details that can be leveraged to perform this.</span><span class="sxs-lookup"><span data-stu-id="3791b-376">This document does not demonstrate a complete end to end example, however the [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) provides details that can be leveraged to perform this.</span></span>

![MinimalDowntime][8]

* <span data-ttu-id="3791b-378">Gather disk configuration, and remove the node (do not delete attached VHDs).</span><span class="sxs-lookup"><span data-stu-id="3791b-378">Gather disk configuration, and remove the node (do not delete attached VHDs).</span></span>
* <span data-ttu-id="3791b-379">Create a Premium Storage account and copy VHDs from the Standard Storage account</span><span class="sxs-lookup"><span data-stu-id="3791b-379">Create a Premium Storage account and copy VHDs from the Standard Storage account</span></span>
* <span data-ttu-id="3791b-380">Create new cloud service and redeploy the SQL2 VM in that cloud service.</span><span class="sxs-lookup"><span data-stu-id="3791b-380">Create new cloud service and redeploy the SQL2 VM in that cloud service.</span></span> <span data-ttu-id="3791b-381">Create the VM using the copied original OS VHD and attaching the copied VHDs.</span><span class="sxs-lookup"><span data-stu-id="3791b-381">Create the VM using the copied original OS VHD and attaching the copied VHDs.</span></span>
* <span data-ttu-id="3791b-382">Configure ILB / ELB and add Endpoints.</span><span class="sxs-lookup"><span data-stu-id="3791b-382">Configure ILB / ELB and add Endpoints.</span></span>
* <span data-ttu-id="3791b-383">Update Listener by either:</span><span class="sxs-lookup"><span data-stu-id="3791b-383">Update Listener by either:</span></span>
  * <span data-ttu-id="3791b-384">Taking the Always On Group offline and updating the Always On Listener with new ILB / ELB IP address.</span><span class="sxs-lookup"><span data-stu-id="3791b-384">Taking the Always On Group offline and updating the Always On Listener with new ILB / ELB IP address.</span></span>
  * <span data-ttu-id="3791b-385">Or adding the IP address resource of new Cloud Service ILB/ELB through PowerShell into Windows clustering.</span><span class="sxs-lookup"><span data-stu-id="3791b-385">Or adding the IP address resource of new Cloud Service ILB/ELB through PowerShell into Windows clustering.</span></span> <span data-ttu-id="3791b-386">Then set the Possible owners of the IP Address resource to the migrated node, SQL2, and set this as OR dependency in the Network Name.</span><span class="sxs-lookup"><span data-stu-id="3791b-386">Then set the Possible owners of the IP Address resource to the migrated node, SQL2, and set this as OR dependency in the Network Name.</span></span> <span data-ttu-id="3791b-387">See the ‘Adding IP Address Resource on Same Subnet’ section of the [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span><span class="sxs-lookup"><span data-stu-id="3791b-387">See the ‘Adding IP Address Resource on Same Subnet’ section of the [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span></span>
* <span data-ttu-id="3791b-388">Check DNS configuration/propogation to the clients.</span><span class="sxs-lookup"><span data-stu-id="3791b-388">Check DNS configuration/propogation to the clients.</span></span>
* <span data-ttu-id="3791b-389">Migrate SQL1 VM, and go through steps 2 – 4.</span><span class="sxs-lookup"><span data-stu-id="3791b-389">Migrate SQL1 VM, and go through steps 2 – 4.</span></span>
* <span data-ttu-id="3791b-390">If using steps 5ii, then add SQL1 as a Possible Owner for the added IP Address Resource</span><span class="sxs-lookup"><span data-stu-id="3791b-390">If using steps 5ii, then add SQL1 as a Possible Owner for the added IP Address Resource</span></span>
* <span data-ttu-id="3791b-391">Test failovers.</span><span class="sxs-lookup"><span data-stu-id="3791b-391">Test failovers.</span></span>

#### <a name="2-utilize-existing-secondary-replicas-multi-site"></a><span data-ttu-id="3791b-392">2. Utilize existing secondary replica(s): Multi-Site</span><span class="sxs-lookup"><span data-stu-id="3791b-392">2. Utilize existing secondary replica(s): Multi-Site</span></span>
<span data-ttu-id="3791b-393">If you have nodes in more than one Azure datacenter (DC) or if you have a hybrid environment, then you can use an Always On configuration in this environment to minimize downtime.</span><span class="sxs-lookup"><span data-stu-id="3791b-393">If you have nodes in more than one Azure datacenter (DC) or if you have a hybrid environment, then you can use an Always On configuration in this environment to minimize downtime.</span></span>

<span data-ttu-id="3791b-394">The approach is to change the Always On synchronization to Synchronous for the on-premises or secondary Azure DC, and then failover over to that SQL Server.</span><span class="sxs-lookup"><span data-stu-id="3791b-394">The approach is to change the Always On synchronization to Synchronous for the on-premises or secondary Azure DC, and then failover over to that SQL Server.</span></span> <span data-ttu-id="3791b-395">Then copy the VHDs to a Premium Storage account, and redeploy the machine into a new cloud service.</span><span class="sxs-lookup"><span data-stu-id="3791b-395">Then copy the VHDs to a Premium Storage account, and redeploy the machine into a new cloud service.</span></span> <span data-ttu-id="3791b-396">Update the listener, and then fail back.</span><span class="sxs-lookup"><span data-stu-id="3791b-396">Update the listener, and then fail back.</span></span>

##### <a name="points-of-downtime"></a><span data-ttu-id="3791b-397">Points of downtime</span><span class="sxs-lookup"><span data-stu-id="3791b-397">Points of downtime</span></span>
<span data-ttu-id="3791b-398">The downtime consists of the time to failover to the alternative DC and back.</span><span class="sxs-lookup"><span data-stu-id="3791b-398">The downtime consists of the time to failover to the alternative DC and back.</span></span> <span data-ttu-id="3791b-399">It also depends on your client/DNS configuration and your client reconnection may be delayed.</span><span class="sxs-lookup"><span data-stu-id="3791b-399">It also depends on your client/DNS configuration and your client reconnection may be delayed.</span></span>
<span data-ttu-id="3791b-400">Consider the following example of a hybrid Always On configuration:</span><span class="sxs-lookup"><span data-stu-id="3791b-400">Consider the following example of a hybrid Always On configuration:</span></span>

![MultiSite1][9]

##### <a name="advantages"></a><span data-ttu-id="3791b-402">Advantages</span><span class="sxs-lookup"><span data-stu-id="3791b-402">Advantages</span></span>
* <span data-ttu-id="3791b-403">You can utilize existing infrastructure.</span><span class="sxs-lookup"><span data-stu-id="3791b-403">You can utilize existing infrastructure.</span></span>
* <span data-ttu-id="3791b-404">You have the option to pre-upgrade the Azure storage on the DR Azure DC first.</span><span class="sxs-lookup"><span data-stu-id="3791b-404">You have the option to pre-upgrade the Azure storage on the DR Azure DC first.</span></span>
* <span data-ttu-id="3791b-405">The DR Azure DC storage can be reconfigured.</span><span class="sxs-lookup"><span data-stu-id="3791b-405">The DR Azure DC storage can be reconfigured.</span></span>
* <span data-ttu-id="3791b-406">There is a minimum of two failovers during migration, excluding test failovers.</span><span class="sxs-lookup"><span data-stu-id="3791b-406">There is a minimum of two failovers during migration, excluding test failovers.</span></span>
* <span data-ttu-id="3791b-407">You do not need to move SQL Server data with backup and restore.</span><span class="sxs-lookup"><span data-stu-id="3791b-407">You do not need to move SQL Server data with backup and restore.</span></span>

##### <a name="disadvantages"></a><span data-ttu-id="3791b-408">Disadvantages</span><span class="sxs-lookup"><span data-stu-id="3791b-408">Disadvantages</span></span>
* <span data-ttu-id="3791b-409">Depending on client access to SQL Server, there might be increased latency when SQL Server is running in an alternative DC to the application.</span><span class="sxs-lookup"><span data-stu-id="3791b-409">Depending on client access to SQL Server, there might be increased latency when SQL Server is running in an alternative DC to the application.</span></span>
* <span data-ttu-id="3791b-410">The copy time of VHDs to Premium storage could be long.</span><span class="sxs-lookup"><span data-stu-id="3791b-410">The copy time of VHDs to Premium storage could be long.</span></span> <span data-ttu-id="3791b-411">This might affect your decision on whether to keep the node in the Availability Group.</span><span class="sxs-lookup"><span data-stu-id="3791b-411">This might affect your decision on whether to keep the node in the Availability Group.</span></span> <span data-ttu-id="3791b-412">Consider this for when log intensive work loads are running during the migration is required, since the Primary node has to keep the unreplicated transactions in its transaction log.</span><span class="sxs-lookup"><span data-stu-id="3791b-412">Consider this for when log intensive work loads are running during the migration is required, since the Primary node has to keep the unreplicated transactions in its transaction log.</span></span> <span data-ttu-id="3791b-413">Therefore this could grow significantly.</span><span class="sxs-lookup"><span data-stu-id="3791b-413">Therefore this could grow significantly.</span></span>
* <span data-ttu-id="3791b-414">This scenario would use the Azure **Start-AzureStorageBlobCopy** commandlet, which is asynchronous.</span><span class="sxs-lookup"><span data-stu-id="3791b-414">This scenario would use the Azure **Start-AzureStorageBlobCopy** commandlet, which is asynchronous.</span></span> <span data-ttu-id="3791b-415">There is no SLA on completion.</span><span class="sxs-lookup"><span data-stu-id="3791b-415">There is no SLA on completion.</span></span> <span data-ttu-id="3791b-416">The time of the copies varies, while this depends on wait in queue, it also depend on the amount of data to transfer.</span><span class="sxs-lookup"><span data-stu-id="3791b-416">The time of the copies varies, while this depends on wait in queue, it also depend on the amount of data to transfer.</span></span> <span data-ttu-id="3791b-417">Therefore you just have one node in your 2nd data center, you should take mitigation steps in case the copy takes longer than in testing.</span><span class="sxs-lookup"><span data-stu-id="3791b-417">Therefore you just have one node in your 2nd data center, you should take mitigation steps in case the copy takes longer than in testing.</span></span> <span data-ttu-id="3791b-418">These mitigation steps include the following ideas:</span><span class="sxs-lookup"><span data-stu-id="3791b-418">These mitigation steps include the following ideas:</span></span>
  * <span data-ttu-id="3791b-419">Add a temporary 2nd SQL node for HA before the migration with agreed downtime.</span><span class="sxs-lookup"><span data-stu-id="3791b-419">Add a temporary 2nd SQL node for HA before the migration with agreed downtime.</span></span>
  * <span data-ttu-id="3791b-420">Run the migration outside of Azure scheduled maintenance.</span><span class="sxs-lookup"><span data-stu-id="3791b-420">Run the migration outside of Azure scheduled maintenance.</span></span>
  * <span data-ttu-id="3791b-421">Ensure you have configured your cluster quorum correctly.</span><span class="sxs-lookup"><span data-stu-id="3791b-421">Ensure you have configured your cluster quorum correctly.</span></span>

<span data-ttu-id="3791b-422">This scenario assumes that you have documented your install and know how the storage is mapped in order to make changes for optimal disk cache settings.</span><span class="sxs-lookup"><span data-stu-id="3791b-422">This scenario assumes that you have documented your install and know how the storage is mapped in order to make changes for optimal disk cache settings.</span></span>

##### <a name="high-level-steps"></a><span data-ttu-id="3791b-423">High-level steps</span><span class="sxs-lookup"><span data-stu-id="3791b-423">High-level steps</span></span>
![Multisite2][10]

* <span data-ttu-id="3791b-425">Make the on-premises / alternate Azure DC the SQL Server Primary, and make it the other Auto Failover Partner (AFP).</span><span class="sxs-lookup"><span data-stu-id="3791b-425">Make the on-premises / alternate Azure DC the SQL Server Primary, and make it the other Auto Failover Partner (AFP).</span></span>
* <span data-ttu-id="3791b-426">Gather disk configuration information from SQL2, and remove the node (do not delete attached VHDs).</span><span class="sxs-lookup"><span data-stu-id="3791b-426">Gather disk configuration information from SQL2, and remove the node (do not delete attached VHDs).</span></span>
* <span data-ttu-id="3791b-427">Create a Premium Storage account and copy VHDs from the Standard Storage account.</span><span class="sxs-lookup"><span data-stu-id="3791b-427">Create a Premium Storage account and copy VHDs from the Standard Storage account.</span></span>
* <span data-ttu-id="3791b-428">Create a new cloud service and create the SQL2 VM with its Premiums Storage disks attached.</span><span class="sxs-lookup"><span data-stu-id="3791b-428">Create a new cloud service and create the SQL2 VM with its Premiums Storage disks attached.</span></span>
* <span data-ttu-id="3791b-429">Configure ILB / ELB and add Endpoints.</span><span class="sxs-lookup"><span data-stu-id="3791b-429">Configure ILB / ELB and add Endpoints.</span></span>
* <span data-ttu-id="3791b-430">Update the Always On Listener with new ILB / ELB IP address and test failover.</span><span class="sxs-lookup"><span data-stu-id="3791b-430">Update the Always On Listener with new ILB / ELB IP address and test failover.</span></span>
* <span data-ttu-id="3791b-431">Check the DNS configuration.</span><span class="sxs-lookup"><span data-stu-id="3791b-431">Check the DNS configuration.</span></span>
* <span data-ttu-id="3791b-432">Change the AFP to SQL2, and then migrate SQL1 and go through steps 2 – 5.</span><span class="sxs-lookup"><span data-stu-id="3791b-432">Change the AFP to SQL2, and then migrate SQL1 and go through steps 2 – 5.</span></span>
* <span data-ttu-id="3791b-433">Test failovers.</span><span class="sxs-lookup"><span data-stu-id="3791b-433">Test failovers.</span></span>
* <span data-ttu-id="3791b-434">Switch the AFP back to SQL1 and SQL2</span><span class="sxs-lookup"><span data-stu-id="3791b-434">Switch the AFP back to SQL1 and SQL2</span></span>

## <a name="appendix-migrating-a-multisite-always-on-cluster-to-premium-storage"></a><span data-ttu-id="3791b-435">Appendix: Migrating a Multisite Always On Cluster to Premium Storage</span><span class="sxs-lookup"><span data-stu-id="3791b-435">Appendix: Migrating a Multisite Always On Cluster to Premium Storage</span></span>
<span data-ttu-id="3791b-436">The remainder of this article provides a detailed example of converting a multi-site Always On cluster to Premium storage.</span><span class="sxs-lookup"><span data-stu-id="3791b-436">The remainder of this article provides a detailed example of converting a multi-site Always On cluster to Premium storage.</span></span> <span data-ttu-id="3791b-437">It also converts the Listener from using an external load balancer (ELB) to an internal load balancer (ILB).</span><span class="sxs-lookup"><span data-stu-id="3791b-437">It also converts the Listener from using an external load balancer (ELB) to an internal load balancer (ILB).</span></span>

### <a name="environment"></a><span data-ttu-id="3791b-438">Environment</span><span class="sxs-lookup"><span data-stu-id="3791b-438">Environment</span></span>
* <span data-ttu-id="3791b-439">Windows 2k12 / SQL 2k12</span><span class="sxs-lookup"><span data-stu-id="3791b-439">Windows 2k12 / SQL 2k12</span></span>
* <span data-ttu-id="3791b-440">1 DB Files on SP</span><span class="sxs-lookup"><span data-stu-id="3791b-440">1 DB Files on SP</span></span>
* <span data-ttu-id="3791b-441">2 x Storage Pools per Node</span><span class="sxs-lookup"><span data-stu-id="3791b-441">2 x Storage Pools per Node</span></span>

![Appendix1][11]

### <a name="vm"></a><span data-ttu-id="3791b-443">VM:</span><span class="sxs-lookup"><span data-stu-id="3791b-443">VM:</span></span>
<span data-ttu-id="3791b-444">In this example, we are going to demonstrate moving from an ELB to ILB.</span><span class="sxs-lookup"><span data-stu-id="3791b-444">In this example, we are going to demonstrate moving from an ELB to ILB.</span></span> <span data-ttu-id="3791b-445">ELB was available before ILB, so this shows how to switch to ILB during the migration.</span><span class="sxs-lookup"><span data-stu-id="3791b-445">ELB was available before ILB, so this shows how to switch to ILB during the migration.</span></span>

![Appendix2][12]

### <a name="pre-steps-connect-to-subscription"></a><span data-ttu-id="3791b-447">Pre Steps: Connect to Subscription</span><span class="sxs-lookup"><span data-stu-id="3791b-447">Pre Steps: Connect to Subscription</span></span>
    Add-AzureAccount

    #Set up subscription
    Get-AzureSubscription

#### <a name="step-1-create-new-storage-account-and-cloud-service"></a><span data-ttu-id="3791b-448">Step 1: Create New Storage Account and Cloud Service</span><span class="sxs-lookup"><span data-stu-id="3791b-448">Step 1: Create New Storage Account and Cloud Service</span></span>
    $mysubscription = "DansSubscription"
    $location = "West Europe"

    #Storage accounts
    #current storage account where the vm to migrate resides
    $origstorageaccountname = "danstdams"

    #Create Premium Storage account
    $newxiostorageaccountname = "danspremsams"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountname -Location $location -Type "Premium_LRS"  

    #Generate storage keys for later
    $originalstorage =  Get-AzureStorageKey -StorageAccountName $origstorageaccountname
    $xiostorage = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountname

    #Generate storage acc contexts
    $origContext = New-AzureStorageContext  –StorageAccountName $origstorageaccountname -StorageAccountKey $originalstorage.Primary
    $xioContext = New-AzureStorageContext  –StorageAccountName $newxiostorageaccountname -StorageAccountKey $xiostorage.Primary  

    #Set up subscription and default storage account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount $origstorageaccountname
    Select-AzureSubscription -SubscriptionName $mysubscription -Current

    #CREATE NEW CLOUD SVC
    $vnet = "dansvnetwesteur"

    ##Existing cloud service
    $sourceSvc="dansolSrcAms"

    ##Create new cloud service
    $destcloudsvc = "danNewSvcAms"
    New-AzureService $destcloudsvc -Location $location

#### <a name="step-2-increase-the-permitted-failures-on-resources-optional"></a><span data-ttu-id="3791b-449">Step 2: Increase the permitted failures on resources <Optional></span><span class="sxs-lookup"><span data-stu-id="3791b-449">Step 2: Increase the permitted failures on resources <Optional></span></span>
<span data-ttu-id="3791b-450">On certain resources that belong to your Always On Availability Group there are limits on how many failures that can occur in a period, where the cluster service attempts to restart the resource group.</span><span class="sxs-lookup"><span data-stu-id="3791b-450">On certain resources that belong to your Always On Availability Group there are limits on how many failures that can occur in a period, where the cluster service attempts to restart the resource group.</span></span> <span data-ttu-id="3791b-451">It is recommended you increase this whilst you are walking through this procedure, since if you don’t manually failover and trigger failovers by shutting down machines you can get close to this limit.</span><span class="sxs-lookup"><span data-stu-id="3791b-451">It is recommended you increase this whilst you are walking through this procedure, since if you don’t manually failover and trigger failovers by shutting down machines you can get close to this limit.</span></span>

<span data-ttu-id="3791b-452">It would be prudent to double the failure allowance, to do this in Failover Cluster Manager, go to the Properties of the Always On resource group:</span><span class="sxs-lookup"><span data-stu-id="3791b-452">It would be prudent to double the failure allowance, to do this in Failover Cluster Manager, go to the Properties of the Always On resource group:</span></span>

![Appendix3][13]

<span data-ttu-id="3791b-454">Change the Maximum Failures to 6.</span><span class="sxs-lookup"><span data-stu-id="3791b-454">Change the Maximum Failures to 6.</span></span>

#### <a name="step-3-addition-ip-address-resource-for-cluster-group-optional"></a><span data-ttu-id="3791b-455">Step 3: Addition IP Address resource for Cluster Group <Optional></span><span class="sxs-lookup"><span data-stu-id="3791b-455">Step 3: Addition IP Address resource for Cluster Group <Optional></span></span>
<span data-ttu-id="3791b-456">If you have only one IP address for the Cluster Group and this is aligned to the cloud subnet, beware, if you accidentally take offline all cluster nodes in the cloud on that network then the Cluster IP resource and Cluster Network Name are not be able to come online.</span><span class="sxs-lookup"><span data-stu-id="3791b-456">If you have only one IP address for the Cluster Group and this is aligned to the cloud subnet, beware, if you accidentally take offline all cluster nodes in the cloud on that network then the Cluster IP resource and Cluster Network Name are not be able to come online.</span></span> <span data-ttu-id="3791b-457">In this situation, it prevents updates to other cluster resources.</span><span class="sxs-lookup"><span data-stu-id="3791b-457">In this situation, it prevents updates to other cluster resources.</span></span>

#### <a name="step-4-dns-configuration"></a><span data-ttu-id="3791b-458">Step 4: DNS configuration</span><span class="sxs-lookup"><span data-stu-id="3791b-458">Step 4: DNS configuration</span></span>
<span data-ttu-id="3791b-459">Implementing a smooth transition depends on how DNS is being utilized and updated.</span><span class="sxs-lookup"><span data-stu-id="3791b-459">Implementing a smooth transition depends on how DNS is being utilized and updated.</span></span>
<span data-ttu-id="3791b-460">When Always On is installed, it creates a Windows Cluster Resource group, if you open Failover Cluster Manager, you see that at a minimum it has three resources, the two that the document refers to are:</span><span class="sxs-lookup"><span data-stu-id="3791b-460">When Always On is installed, it creates a Windows Cluster Resource group, if you open Failover Cluster Manager, you see that at a minimum it has three resources, the two that the document refers to are:</span></span>

* <span data-ttu-id="3791b-461">Virtual Network Name (VNN) – the DNS name that clients connect to when wanting to connect to SQL Servers via Always On.</span><span class="sxs-lookup"><span data-stu-id="3791b-461">Virtual Network Name (VNN) – the DNS name that clients connect to when wanting to connect to SQL Servers via Always On.</span></span>
* <span data-ttu-id="3791b-462">IP Address Resource – the IP address that associated with the VNN, you can have more than one, and in a multisite configuration you have an IP address per site/subnet.</span><span class="sxs-lookup"><span data-stu-id="3791b-462">IP Address Resource – the IP address that associated with the VNN, you can have more than one, and in a multisite configuration you have an IP address per site/subnet.</span></span>

<span data-ttu-id="3791b-463">When connecting to SQL Server, the SQL Server Client driver retrieves the DNS records associated with the listener and tries to connect to each Always On associated IP address.</span><span class="sxs-lookup"><span data-stu-id="3791b-463">When connecting to SQL Server, the SQL Server Client driver retrieves the DNS records associated with the listener and tries to connect to each Always On associated IP address.</span></span> <span data-ttu-id="3791b-464">Next, we discuss some factors that can influence this.</span><span class="sxs-lookup"><span data-stu-id="3791b-464">Next, we discuss some factors that can influence this.</span></span>

<span data-ttu-id="3791b-465">The number of concurrent DNS records that are associated with the listener name depends not only on the number of IP addresses associated, but the ‘RegisterAllIpProviders’setting in Failover Clustering for the Always ON VNN resource.</span><span class="sxs-lookup"><span data-stu-id="3791b-465">The number of concurrent DNS records that are associated with the listener name depends not only on the number of IP addresses associated, but the ‘RegisterAllIpProviders’setting in Failover Clustering for the Always ON VNN resource.</span></span>

<span data-ttu-id="3791b-466">When you deploy Always On in Azure there are different steps to create the Listener and IP Addresses, you have to manually configure the ‘RegisterAllIpProviders’ to 1, this is different to an on-premises Always On deployment where it is already set to 1.</span><span class="sxs-lookup"><span data-stu-id="3791b-466">When you deploy Always On in Azure there are different steps to create the Listener and IP Addresses, you have to manually configure the ‘RegisterAllIpProviders’ to 1, this is different to an on-premises Always On deployment where it is already set to 1.</span></span>

<span data-ttu-id="3791b-467">If ‘RegisterAllIpProviders’ is 0, then you only see one DNS record in DNS associated with the Listener:</span><span class="sxs-lookup"><span data-stu-id="3791b-467">If ‘RegisterAllIpProviders’ is 0, then you only see one DNS record in DNS associated with the Listener:</span></span>

![Appendix4][14]

<span data-ttu-id="3791b-469">If ‘RegisterAllIpProviders’ is 1:</span><span class="sxs-lookup"><span data-stu-id="3791b-469">If ‘RegisterAllIpProviders’ is 1:</span></span>

![Appendix5][15]

<span data-ttu-id="3791b-471">The code below dumps out the VNN settings and sets it for you.</span><span class="sxs-lookup"><span data-stu-id="3791b-471">The code below dumps out the VNN settings and sets it for you.</span></span> <span data-ttu-id="3791b-472">For the change to take effect, you need to take the VNN offline and turn it back online.</span><span class="sxs-lookup"><span data-stu-id="3791b-472">For the change to take effect, you need to take the VNN offline and turn it back online.</span></span> <span data-ttu-id="3791b-473">This takes the Listener offline causing client connectivity disruption.</span><span class="sxs-lookup"><span data-stu-id="3791b-473">This takes the Listener offline causing client connectivity disruption.</span></span>

    ##Always On Listener Name
    $ListenerName = "Mylistener"
    ##Get AlwaysOn Network Name Settings
    Get-ClusterResource $ListenerName| Get-ClusterParameter
    ##Set RegisterAllProvidersIP
    Get-ClusterResource $ListenerName| Set-ClusterParameter RegisterAllProvidersIP  1

<span data-ttu-id="3791b-474">In a later migration step, you need to update the Always On listener with an updated IP address that references a load balancer, this involves an IP Address resource removal and addition.</span><span class="sxs-lookup"><span data-stu-id="3791b-474">In a later migration step, you need to update the Always On listener with an updated IP address that references a load balancer, this involves an IP Address resource removal and addition.</span></span> <span data-ttu-id="3791b-475">After the IP update, you need to ensure the new IP address has been updated in DNS Zone and that the clients are updating their local DNS cache.</span><span class="sxs-lookup"><span data-stu-id="3791b-475">After the IP update, you need to ensure the new IP address has been updated in DNS Zone and that the clients are updating their local DNS cache.</span></span>

<span data-ttu-id="3791b-476">If your clients reside in a different network segment and reference a different DNS server, you need to consider what happens about DNS Zone Transfer during the migration, as the application reconnect time is constrained by at least the Zone Transfer Time of any new IP addresses for the listener.</span><span class="sxs-lookup"><span data-stu-id="3791b-476">If your clients reside in a different network segment and reference a different DNS server, you need to consider what happens about DNS Zone Transfer during the migration, as the application reconnect time is constrained by at least the Zone Transfer Time of any new IP addresses for the listener.</span></span> <span data-ttu-id="3791b-477">If you are under time constraint here, you should discuss and test forcing an incremental zone transfer with your Windows teams, and also put the DNS host record to a lower Time To Live (TTL), so the clients update.</span><span class="sxs-lookup"><span data-stu-id="3791b-477">If you are under time constraint here, you should discuss and test forcing an incremental zone transfer with your Windows teams, and also put the DNS host record to a lower Time To Live (TTL), so the clients update.</span></span> <span data-ttu-id="3791b-478">For more information, see [Incremental Zone Transfers](https://technet.microsoft.com/library/cc958973.aspx) and [Start-DnsServerZoneTransfer](https://docs.microsoft.com/powershell/module/dnsserver/start-dnsserverzonetransfer).</span><span class="sxs-lookup"><span data-stu-id="3791b-478">For more information, see [Incremental Zone Transfers](https://technet.microsoft.com/library/cc958973.aspx) and [Start-DnsServerZoneTransfer](https://docs.microsoft.com/powershell/module/dnsserver/start-dnsserverzonetransfer).</span></span>

<span data-ttu-id="3791b-479">By default the TTL for DNS Record that is associated with the Listener in Always On in Azure is 1200 seconds.</span><span class="sxs-lookup"><span data-stu-id="3791b-479">By default the TTL for DNS Record that is associated with the Listener in Always On in Azure is 1200 seconds.</span></span> <span data-ttu-id="3791b-480">You may wish to reduce this if you are under time constraint during your migration to ensure the clients update their DNS with the updated IP address for the listener.</span><span class="sxs-lookup"><span data-stu-id="3791b-480">You may wish to reduce this if you are under time constraint during your migration to ensure the clients update their DNS with the updated IP address for the listener.</span></span> <span data-ttu-id="3791b-481">You can see and modify the configuration by dumping out the configuration of the VNN:</span><span class="sxs-lookup"><span data-stu-id="3791b-481">You can see and modify the configuration by dumping out the configuration of the VNN:</span></span>

    $AGName = "myProductionAG"
    $ListenerName = "Mylistener"
    #Look at HostRecordTTL
    Get-ClusterResource $ListenerName| Get-ClusterParameter

    #Set HostRecordTTL Examples
    Get-ClusterResource $ListenerName| Set-ClusterParameter -Name "HostRecordTTL" 120

> [!NOTE]
> <span data-ttu-id="3791b-482">The lower the ‘HostRecordTTL’, a higher amount of DNS traffic occurs.</span><span class="sxs-lookup"><span data-stu-id="3791b-482">The lower the ‘HostRecordTTL’, a higher amount of DNS traffic occurs.</span></span>

##### <a name="client-application-settings"></a><span data-ttu-id="3791b-483">Client application settings</span><span class="sxs-lookup"><span data-stu-id="3791b-483">Client application settings</span></span>
<span data-ttu-id="3791b-484">If your SQL client application supports the .Net 4.5 SQLClient, then you can use ‘MULTISUBNETFAILOVER=TRUE’ keyword.</span><span class="sxs-lookup"><span data-stu-id="3791b-484">If your SQL client application supports the .Net 4.5 SQLClient, then you can use ‘MULTISUBNETFAILOVER=TRUE’ keyword.</span></span> <span data-ttu-id="3791b-485">This keyword should be applied, because it allows for faster connection to SQL Always On Availability Group during failover.</span><span class="sxs-lookup"><span data-stu-id="3791b-485">This keyword should be applied, because it allows for faster connection to SQL Always On Availability Group during failover.</span></span> <span data-ttu-id="3791b-486">It enumerates through all IP addresses associated with the Always On listener in parallel, and performs a more aggressive TCP connection retry speed during a failover.</span><span class="sxs-lookup"><span data-stu-id="3791b-486">It enumerates through all IP addresses associated with the Always On listener in parallel, and performs a more aggressive TCP connection retry speed during a failover.</span></span>

<span data-ttu-id="3791b-487">For more information about the previous settings, see [MultiSubnetFailover Keyword and Associated Features](https://msdn.microsoft.com/library/hh213080.aspx#MultiSubnetFailover).</span><span class="sxs-lookup"><span data-stu-id="3791b-487">For more information about the previous settings, see [MultiSubnetFailover Keyword and Associated Features](https://msdn.microsoft.com/library/hh213080.aspx#MultiSubnetFailover).</span></span> <span data-ttu-id="3791b-488">Also see [SqlClient Support for High Availability, Disaster Recovery](https://msdn.microsoft.com/library/hh205662\(v=vs.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="3791b-488">Also see [SqlClient Support for High Availability, Disaster Recovery](https://msdn.microsoft.com/library/hh205662\(v=vs.110\).aspx).</span></span>

#### <a name="step-5-cluster-quorum-settings"></a><span data-ttu-id="3791b-489">Step 5: Cluster quorum settings</span><span class="sxs-lookup"><span data-stu-id="3791b-489">Step 5: Cluster quorum settings</span></span>
<span data-ttu-id="3791b-490">As you are going to be taking out at least one SQL Server down at a time, you should modify the cluster quorum setting, if using File Share Witness (FSW) with two nodes, you should set the quorum to allow node majority and utilize dynamic voting, allowing for a single node to remain standing.</span><span class="sxs-lookup"><span data-stu-id="3791b-490">As you are going to be taking out at least one SQL Server down at a time, you should modify the cluster quorum setting, if using File Share Witness (FSW) with two nodes, you should set the quorum to allow node majority and utilize dynamic voting, allowing for a single node to remain standing.</span></span>

    Set-ClusterQuorum -NodeMajority  

<span data-ttu-id="3791b-491">For more information on managing and configuring the cluster quorum, see [Configure and Manage the Quorum in a Windows Server 2012 Failover Cluster](https://technet.microsoft.com/library/jj612870.aspx).</span><span class="sxs-lookup"><span data-stu-id="3791b-491">For more information on managing and configuring the cluster quorum, see [Configure and Manage the Quorum in a Windows Server 2012 Failover Cluster](https://technet.microsoft.com/library/jj612870.aspx).</span></span>

#### <a name="step-6-extract-existing-endpoints-and-acls"></a><span data-ttu-id="3791b-492">Step 6: Extract Existing Endpoints and ACLs</span><span class="sxs-lookup"><span data-stu-id="3791b-492">Step 6: Extract Existing Endpoints and ACLs</span></span>
    #GET Endpoint info
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmNameToMigrate | Get-AzureEndpoint
    #GET ACL Rules for Each EP, this example is for the Always On Endpoint
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmNameToMigrate | Get-AzureAclConfig -EndpointName "myAOEndPoint-LB"  

<span data-ttu-id="3791b-493">Save this text to a file.</span><span class="sxs-lookup"><span data-stu-id="3791b-493">Save this text to a file.</span></span>

#### <a name="step-7-change-failover-partners-and-replication-modes"></a><span data-ttu-id="3791b-494">Step 7: Change Failover Partners and Replication Modes</span><span class="sxs-lookup"><span data-stu-id="3791b-494">Step 7: Change Failover Partners and Replication Modes</span></span>
<span data-ttu-id="3791b-495">If you have more than two SQL Servers, you should change the failover of another secondary in another DC or on-premises to ‘Synchronous’ and make it an Automatic Failover Partner (AFP), this is so you maintain HA whilst you are making changes.</span><span class="sxs-lookup"><span data-stu-id="3791b-495">If you have more than two SQL Servers, you should change the failover of another secondary in another DC or on-premises to ‘Synchronous’ and make it an Automatic Failover Partner (AFP), this is so you maintain HA whilst you are making changes.</span></span> <span data-ttu-id="3791b-496">You can do this through TSQL of modify though SSMS:</span><span class="sxs-lookup"><span data-stu-id="3791b-496">You can do this through TSQL of modify though SSMS:</span></span>

![Appendix6][16]

#### <a name="step-8-remove-secondary-vm-from-cloud-service"></a><span data-ttu-id="3791b-498">Step 8: Remove Secondary VM from cloud service</span><span class="sxs-lookup"><span data-stu-id="3791b-498">Step 8: Remove Secondary VM from cloud service</span></span>
<span data-ttu-id="3791b-499">You should be planning to migrate a cloud secondary node first.</span><span class="sxs-lookup"><span data-stu-id="3791b-499">You should be planning to migrate a cloud secondary node first.</span></span> <span data-ttu-id="3791b-500">If this node is currently primary, you should initiate a manual failover.</span><span class="sxs-lookup"><span data-stu-id="3791b-500">If this node is currently primary, you should initiate a manual failover.</span></span>

    $vmNameToMigrate="dansqlams2"

    #Check machine status
    Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate

    #Shutdown secondary VM
    Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | stop-AzureVM


    #Extract disk configuration

    ##Building Existing Data Disk Configuration
    $file = "C:\Azure Storage Testing\mydiskconfig_$vmNameToMigrate.csv"
    $datadisks = @(Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | Get-AzureDataDisk )
    Add-Content $file “lun, vhdname, hostcaching, disklabel, diskName”
    foreach ($disk in $datadisks)
    {
      $vhdname = $disk.MediaLink.AbsolutePath -creplace  "/vhds/"
      $disk.Lun, , $disk.HostCaching, $vhdname, $disk.DiskLabel,$disks.DiskName
    # Write-Host "copying disk $disk"
    $adddisk = "{0},{1},{2},{3},{4}" -f $disk.Lun,$vhdname, $disk.HostCaching, $disk.DiskLabel, $disk.DiskName
    $adddisk | add-content -path $file
    }

    #Get OS Disk
    $osdisks = Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | Get-AzureOSDisk ## | select -ExpandProperty MediaLink
    $osvhdname = $osdisks.MediaLink.AbsolutePath -creplace  "/vhds/"
    $osdisks.OS, $osdisks.HostCaching, $osvhdname, $osdisks.DiskLabel, $osdisks.DiskName
    $addosdisk = "{0},{1},{2},{3},{4}" -f $osdisks.OS,$osvhdname, $osdisks.HostCaching, $osdisks.Disklabel , $osdisks.DiskName
    $addosdisk | add-content -path $file

    #Import disk config
    $diskobjects  = Import-CSV $file

    #Check disk config, make sure below returns the disks associated with the VM
    $diskobjects

    #Identify OS Disk
    $osdiskimport = $diskobjects | where {$_.lun -eq "Windows"}
    $osdiskforbuild = $osdiskimport.diskName

    #Check machibe is off
    Get-AzureVM -ServiceName $sourceSvc -Name  $vmNameToMigrate

    #Drop machine and rebuild to new cls
    Remove-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate

#### <a name="step-9-change-disk-caching-settings-in-csv-file-and-save"></a><span data-ttu-id="3791b-501">Step 9: Change disk caching settings in CSV file and save</span><span class="sxs-lookup"><span data-stu-id="3791b-501">Step 9: Change disk caching settings in CSV file and save</span></span>
<span data-ttu-id="3791b-502">For data volumes, these should be set to READONLY.</span><span class="sxs-lookup"><span data-stu-id="3791b-502">For data volumes, these should be set to READONLY.</span></span>

<span data-ttu-id="3791b-503">For TLOG volumes, these should be set to NONE.</span><span class="sxs-lookup"><span data-stu-id="3791b-503">For TLOG volumes, these should be set to NONE.</span></span>

![Appendix7][17]

#### <a name="step-10-copy-vhds"></a><span data-ttu-id="3791b-505">Step 10: Copy VHDS</span><span class="sxs-lookup"><span data-stu-id="3791b-505">Step 10: Copy VHDS</span></span>
    #Ensure you have created the container for these:
    $containerName = 'vhds'

    #Create container
    New-AzureStorageContainer -Name $containerName -Context $xioContext

    ####DISK COPYING####
    #Get disks from csv, get settings for each VHDs and copy to Premium Storage accoun
    ForEach ($disk in $diskobjects)
       {
       $lun = $disk.Lun
       $vhdname = $disk.vhdname
       $cacheoption = $disk.HostCaching
       $disklabel = $disk.DiskLabel
       $diskName = $disk.DiskName
       Write-Host "Copying Disk Lun $lun, Label : $disklabel, VHD : $vhdname has cache setting : $cacheoption"

       #Start async copy
       Start-AzureStorageBlobCopy -srcUri "https://$origstorageaccountname.blob.core.windows.net/vhds/$vhdname" `
    -SrcContext $origContext `
    -DestContainer $containerName `
    -DestBlob $vhdname `
    -DestContext $xioContext
       }



<span data-ttu-id="3791b-506">You can check the copy status of the VHDs to the Premium Storage account:</span><span class="sxs-lookup"><span data-stu-id="3791b-506">You can check the copy status of the VHDs to the Premium Storage account:</span></span>

    ForEach ($disk in $diskobjects)
       {
       $lun = $disk.Lun
       $vhdname = $disk.vhdname
       $cacheoption = $disk.HostCaching
       $disklabel = $disk.DiskLabel
       $diskName = $disk.DiskName

       $copystate = Get-AzureStorageBlobCopyState -Blob $vhdname -Container $containerName -Context $xioContext
    Write-Host "Copying Disk Lun $lun, Label : $disklabel, VHD : $vhdname, STATUS = " $copystate.Status
       }

![Appendix8][18]

<span data-ttu-id="3791b-508">Wait until all these are recorded as success.</span><span class="sxs-lookup"><span data-stu-id="3791b-508">Wait until all these are recorded as success.</span></span>

<span data-ttu-id="3791b-509">For information for individual blobs:</span><span class="sxs-lookup"><span data-stu-id="3791b-509">For information for individual blobs:</span></span>

    Get-AzureStorageBlobCopyState -Blob "blobname.vhd" -Container $containerName -Context $xioContext

#### <a name="step-11-register-os-disk"></a><span data-ttu-id="3791b-510">Step 11: Register OS disk</span><span class="sxs-lookup"><span data-stu-id="3791b-510">Step 11: Register OS disk</span></span>
    #Change storage account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount $newxiostorageaccountname
    Select-AzureSubscription -SubscriptionName $mysubscription -Current

    #Register OS disk
    $osdiskimport = $diskobjects | where {$_.lun -eq "Windows"}
    $osvhd = $osdiskimport.vhdname
    $osdiskforbuild = $osdiskimport.diskName

    #Registering OS disk, but as XIO disk
    $xioDiskName = $osdiskforbuild + "xio"
    Add-AzureDisk -DiskName $xioDiskName -MediaLocation  "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$osvhd"  -Label "BootDisk" -OS "Windows"

#### <a name="step-12-import-secondary-into-new-cloud-service"></a><span data-ttu-id="3791b-511">Step 12: Import secondary into new cloud service</span><span class="sxs-lookup"><span data-stu-id="3791b-511">Step 12: Import secondary into new cloud service</span></span>
<span data-ttu-id="3791b-512">The code below also uses the added option here you can import the machine and use the retainable VIP.</span><span class="sxs-lookup"><span data-stu-id="3791b-512">The code below also uses the added option here you can import the machine and use the retainable VIP.</span></span>

    #Build VM Config
    $ipaddr = "192.168.0.5"
    #Remember to change to XIO
    $newInstanceSize = "Standard_DS13"
    $subnet = "SQL"

    #Create new Avaiability Set
    $availabilitySet = "cloudmigAVAMS"

    #build machine config into object
    $vmConfig = New-AzureVMConfig -Name $vmNameToMigrate -InstanceSize $newInstanceSize -DiskName $xioDiskName -AvailabilitySetName $availabilitySet  ` | Add-AzureProvisioningConfig -Windows ` | Set-AzureSubnet -SubnetNames $subnet | Set-AzureStaticVNetIP -IPAddress $ipaddr

    #Reload disk config
    $diskobjects  = Import-CSV $file
    $datadiskimport = $diskobjects | where {$_.lun -ne "Windows"}

    ForEach ( $attachdatadisk in $datadiskimport)
       {
    $label = $attachdatadisk.disklabel
    $lunNo = $attachdatadisk.lun
    $hostcach = $attachdatadisk.hostcaching
    $datadiskforbuild = $attachdatadisk.diskName
    $vhdname = $attachdatadisk.vhdname

    ###Attaching disks to a VM during a deploy to a new cloud service and new storage account is different from just attaching VHDs to just a redeploy in a new cloud service
    $vmConfig | Add-AzureDataDisk -ImportFrom -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vhdname" -LUN $lunNo -HostCaching $hostcach -DiskLabel $label

    }

    #Create VM
    $vmConfig  | New-AzureVM –ServiceName $destcloudsvc –Location $location -VNetName $vnet ## Optional (-ReservedIPName $reservedVIPName)

#### <a name="step-13-create-ilb-on-new-cloud-svc-add-load-balanced-endpoints-and-acls"></a><span data-ttu-id="3791b-513">Step 13: Create ILB on New Cloud Svc, Add Load Balanced Endpoints and ACLs</span><span class="sxs-lookup"><span data-stu-id="3791b-513">Step 13: Create ILB on New Cloud Svc, Add Load Balanced Endpoints and ACLs</span></span>
    #Check for existing ILB
    GET-AzureInternalLoadBalancer -ServiceName $destcloudsvc

    $ilb="sqlIntIlbDest"
    $subnet = "SQL"
    $IP="192.168.0.25"
    Add-AzureInternalLoadBalancer -ServiceName $destcloudsvc -InternalLoadBalancerName $ilb –SubnetName $subnet –StaticVNetIPAddress $IP

    #Endpoints
    $epname="sqlIntEP"
    $prot="tcp"
    $locport=1433
    $pubport=1433
    Get-AzureVM –ServiceName $destcloudsvc –Name $vmNameToMigrate  | Add-AzureEndpoint -Name $epname -Protocol $prot -LocalPort $locport -PublicPort $pubport -ProbePort 59999 -ProbeIntervalInSeconds 5 -ProbeTimeoutInSeconds 11  -ProbeProtocol "TCP" -InternalLoadBalancerName $ilb -LBSetName $ilb -DirectServerReturn $true | Update-AzureVM

    #SET Azure ACLs or Network Security Groups & Windows FWs

    #http://msdn.microsoft.com/library/azure/dn495192.aspx

    ####WAIT FOR FULL AlwaysOn RESYNCRONISATION!!!!!!!!!#####

#### <a name="step-14-update-always-on"></a><span data-ttu-id="3791b-514">Step 14: Update Always On</span><span class="sxs-lookup"><span data-stu-id="3791b-514">Step 14: Update Always On</span></span>
    #Code to be executed on a Cluster Node
    $ClusterNetworkNameAmsterdam = "Cluster Network 2" # the azure cluster subnet network name
    $newCloudServiceIPAmsterdam = "192.168.0.25" # IP address of your cloud service

    $AGName = "myProductionAG"
    $ListenerName = "Mylistener"


    Add-ClusterResource "IP Address $newCloudServiceIPAmsterdam" -ResourceType "IP Address" -Group $AGName -ErrorAction Stop |  Set-ClusterParameter -Multiple @{"Address"="$newCloudServiceIPAmsterdam";"ProbePort"="59999";SubnetMask="255.255.255.255";"Network"=$ClusterNetworkNameAmsterdam;"OverrideAddressMatch"=1;"EnableDhcp"=0} -ErrorAction Stop

    #set dependancy and NETBIOS, then remove old IP address

    #set NETBIOS, then remove old IP address
    Get-ClusterGroup $AGName | Get-ClusterResource -Name "IP Address $newCloudServiceIPAmsterdam" | Set-ClusterParameter -Name EnableNetBIOS -Value 0

    #set dependency to Listener (OR Dependency) and delete previous IP Address resource that references:

    #Make sure no static records in DNS

![Appendix9][19]

<span data-ttu-id="3791b-516">Now remove the old cloud service IP Address.</span><span class="sxs-lookup"><span data-stu-id="3791b-516">Now remove the old cloud service IP Address.</span></span>

![Appendix10][20]

#### <a name="step-15-dns-update-check"></a><span data-ttu-id="3791b-518">Step 15: DNS update check</span><span class="sxs-lookup"><span data-stu-id="3791b-518">Step 15: DNS update check</span></span>
<span data-ttu-id="3791b-519">You should now check DNS Servers on your SQL Server client networks and make sure that clustering has added the extra host record for the added IP address.</span><span class="sxs-lookup"><span data-stu-id="3791b-519">You should now check DNS Servers on your SQL Server client networks and make sure that clustering has added the extra host record for the added IP address.</span></span> <span data-ttu-id="3791b-520">If those DNS servers have not updated, consider forcing a DNS Zone transfer and ensure that the clients in there subnet are able to resolve to both Always On IP Addresses, this is so you do not need to wait for automatic DNS replication.</span><span class="sxs-lookup"><span data-stu-id="3791b-520">If those DNS servers have not updated, consider forcing a DNS Zone transfer and ensure that the clients in there subnet are able to resolve to both Always On IP Addresses, this is so you do not need to wait for automatic DNS replication.</span></span>

#### <a name="step-16-reconfigure-always-on"></a><span data-ttu-id="3791b-521">Step 16: Reconfigure Always On</span><span class="sxs-lookup"><span data-stu-id="3791b-521">Step 16: Reconfigure Always On</span></span>
<span data-ttu-id="3791b-522">At this point, you wait for the secondary that node that was migrated to fully resynchronize with the on-premises node and switch to synchronous replication node and make it the AFP.</span><span class="sxs-lookup"><span data-stu-id="3791b-522">At this point, you wait for the secondary that node that was migrated to fully resynchronize with the on-premises node and switch to synchronous replication node and make it the AFP.</span></span>  

#### <a name="step-17-migrate-second-node"></a><span data-ttu-id="3791b-523">Step 17: Migrate second node</span><span class="sxs-lookup"><span data-stu-id="3791b-523">Step 17: Migrate second node</span></span>
    $vmNameToMigrate="dansqlams1"

    Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate

    #Get endpoint information
    $endpoint = Get-AzureVM -ServiceName $sourceSvc  -Name $vmNameToMigrate | Get-AzureEndpoint

    #Shutdown VM
    Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | stop-AzureVM

    #Get disk config

    #Building Existing Data Disk Configuration
    $file = "C:\Azure Storage Testing\mydiskconfig_$vmNameToMigrate.csv"
    $datadisks = @(Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | Get-AzureDataDisk )
    Add-Content $file “lun, vhdname, hostcaching, disklabel, diskName”
    foreach ($disk in $datadisks)
    {
      $vhdname = $disk.MediaLink.AbsolutePath -creplace  "/vhds/"
      $disk.Lun, , $disk.HostCaching, $vhdname, $disk.DiskLabel,$disks.DiskName
    # Write-Host "copying disk $disk"
    $adddisk = "{0},{1},{2},{3},{4}" -f $disk.Lun,$vhdname, $disk.HostCaching, $disk.DiskLabel, $disk.DiskName
    $adddisk | add-content -path $file
    }

    #Get OS Disk
    $osdisks = Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | Get-AzureOSDisk ## | select -ExpandProperty MediaLink
    $osvhdname = $osdisks.MediaLink.AbsolutePath -creplace  "/vhds/"
    $osdisks.OS, $osdisks.HostCaching, $osvhdname, $osdisks.DiskLabel, $osdisks.DiskName
    $addosdisk = "{0},{1},{2},{3},{4}" -f $osdisks.OS,$osvhdname, $osdisks.HostCaching, $osdisks.Disklabel , $osdisks.DiskName
    $addosdisk | add-content -path $file

    #Import disk config
    $diskobjects  = Import-CSV $file

    #Check disk configuration
    $diskobjects

    #Identify OS Disk
    $osdiskimport = $diskobjects | where {$_.lun -eq "Windows"}
    $osdiskforbuild = $osdiskimport.diskName

    #Check machine is off
    Get-AzureVM -ServiceName $sourceSvc -Name  $vmNameToMigrate

    #Drop machine and rebuild to new cls
    Remove-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate

#### <a name="step-18-change-disk-caching-settings-in-csv-file-and-save"></a><span data-ttu-id="3791b-524">Step 18: Change disk caching settings in CSV file and save</span><span class="sxs-lookup"><span data-stu-id="3791b-524">Step 18: Change disk caching settings in CSV file and save</span></span>
<span data-ttu-id="3791b-525">For data volumes, the cache settings should be set to READONLY.</span><span class="sxs-lookup"><span data-stu-id="3791b-525">For data volumes, the cache settings should be set to READONLY.</span></span>

<span data-ttu-id="3791b-526">For TLOG volumes, the cache settings should be set to NONE.</span><span class="sxs-lookup"><span data-stu-id="3791b-526">For TLOG volumes, the cache settings should be set to NONE.</span></span>

![Appendix11][21]

#### <a name="step-19-create-new-independent-storage-account-for-secondary-node"></a><span data-ttu-id="3791b-528">Step 19: Create New Independent Storage Account for Secondary Node</span><span class="sxs-lookup"><span data-stu-id="3791b-528">Step 19: Create New Independent Storage Account for Secondary Node</span></span>
    $newxiostorageaccountnamenode2 = "danspremsams2"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountnamenode2 -Location $location -Type "Premium_LRS"  

    #Reset the storage account src if node 1 in a different storage account
    $origstorageaccountname2nd = "danstdams2"

    #Generate storage keys for later
    $xiostoragenode2 = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountnamenode2

    #Generate storage acc contexts
    $xioContextnode2 = New-AzureStorageContext  –StorageAccountName $newxiostorageaccountnamenode2 -StorageAccountKey $xiostoragenode2.Primary  

    #Set up subscription and default storage account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount $newxiostorageaccountnamenode2
    Select-AzureSubscription -SubscriptionName $mysubscription -Current

#### <a name="step-20-copy-vhds"></a><span data-ttu-id="3791b-529">Step 20: Copy VHDS</span><span class="sxs-lookup"><span data-stu-id="3791b-529">Step 20: Copy VHDS</span></span>
    #Ensure you have created the container for these:
    $containerName = 'vhds'

    #Create container
    New-AzureStorageContainer -Name $containerName -Context $xioContextnode2  

    ####DISK COPYING####
    ##get disks from csv, get settings for each VHDs and copy to Premium Storage accoun
    ForEach ($disk in $diskobjects)
       {
       $lun = $disk.Lun
       $vhdname = $disk.vhdname
       $cacheoption = $disk.HostCaching
       $disklabel = $disk.DiskLabel
       $diskName = $disk.DiskName
       Write-Host "Copying Disk Lun $lun, Label : $disklabel, VHD : $vhdname has cache setting : $cacheoption"

       #Start async copy
       Start-AzureStorageBlobCopy -srcUri "https://$origstorageaccountname2nd.blob.core.windows.net/vhds/$vhdname" `
        -SrcContext $origContext `
        -DestContainer $containerName `
        -DestBlob $vhdname `
        -DestContext $xioContextnode2
       }

    #Check for copy progress

    #check induvidual blob status
    Get-AzureStorageBlobCopyState -Blob "danRegSvcAms-dansqlams1-2014-07-03.vhd" -Container $containerName -Context $xioContext


<span data-ttu-id="3791b-530">You can check the VHD copy status for all VHDs: ForEach ($disk in $diskobjects) { $lun = $disk.Lun $vhdname = $disk.vhdname $cacheoption = $disk.HostCaching $disklabel = $disk.DiskLabel $diskName = $disk.DiskName</span><span class="sxs-lookup"><span data-stu-id="3791b-530">You can check the VHD copy status for all VHDs: ForEach ($disk in $diskobjects) { $lun = $disk.Lun $vhdname = $disk.vhdname $cacheoption = $disk.HostCaching $disklabel = $disk.DiskLabel $diskName = $disk.DiskName</span></span>

       $copystate = Get-AzureStorageBlobCopyState -Blob $vhdname -Container $containerName -Context $xioContextnode2
    Write-Host "Copying Disk Lun $lun, Label : $disklabel, VHD : $vhdname, STATUS = " $copystate.Status
       }

![Appendix12][22]

<span data-ttu-id="3791b-532">Wait until all these are recorded as success.</span><span class="sxs-lookup"><span data-stu-id="3791b-532">Wait until all these are recorded as success.</span></span>

<span data-ttu-id="3791b-533">For information for individual blobs:</span><span class="sxs-lookup"><span data-stu-id="3791b-533">For information for individual blobs:</span></span>

    #Check induvidual blob status
    Get-AzureStorageBlobCopyState -Blob "danRegSvcAms-dansqlams1-2014-07-03.vhd" -Container $containerName -Context $xioContextnode2

#### <a name="step-21-register-os-disk"></a><span data-ttu-id="3791b-534">Step 21: Register OS disk</span><span class="sxs-lookup"><span data-stu-id="3791b-534">Step 21: Register OS disk</span></span>
    #change storage account to the new XIO storage account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount $newxiostorageaccountnamenode2
    Select-AzureSubscription -SubscriptionName $mysubscription -Current

    #Register OS disk
    $osdiskimport = $diskobjects | where {$_.lun -eq "Windows"}
    $osvhd = $osdiskimport.vhdname
    $osdiskforbuild = $osdiskimport.diskName

    #Registering OS disk, but as XIO disk
    $xioDiskName = $osdiskforbuild + "xio"
    Add-AzureDisk -DiskName $xioDiskName -MediaLocation  "https://$newxiostorageaccountnamenode2.blob.core.windows.net/vhds/$osvhd"  -Label "BootDisk" -OS "Windows"

    #Build VM Config
    $ipaddr = "192.168.0.4"
    $newInstanceSize = "Standard_DS13"

    #Join to existing Avaiability Set

    #Build machine config into object
    $vmConfig = New-AzureVMConfig -Name $vmNameToMigrate -InstanceSize $newInstanceSize -DiskName $xioDiskName -AvailabilitySetName $availabilitySet  ` | Add-AzureProvisioningConfig -Windows ` | Set-AzureSubnet -SubnetNames $subnet | Set-AzureStaticVNetIP -IPAddress $ipaddr

    #Reload disk config
    $diskobjects  = Import-CSV $file
    $datadiskimport = $diskobjects | where {$_.lun -ne "Windows"}

    ForEach ( $attachdatadisk in $datadiskimport)
       {
    $label = $attachdatadisk.disklabel
    $lunNo = $attachdatadisk.lun
    $hostcach = $attachdatadisk.hostcaching
    $datadiskforbuild = $attachdatadisk.diskName
    $vhdname = $attachdatadisk.vhdname

    ###This is different to just a straight cloud service change
    #note if you do not have a disk label the command below will fail, populate as required.
    $vmConfig | Add-AzureDataDisk -ImportFrom -MediaLocation "https://$newxiostorageaccountnamenode2.blob.core.windows.net/vhds/$vhdname" -LUN $lunNo -HostCaching $hostcach -DiskLabel $label

    }

    #Create VM
    $vmConfig  | New-AzureVM –ServiceName $destcloudsvc –Location $location -VNetName $vnet -Verbose

#### <a name="step-22-add-load-balanced-endpoints-and-acls"></a><span data-ttu-id="3791b-535">Step 22: Add Load Balanced Endpoints and ACLs</span><span class="sxs-lookup"><span data-stu-id="3791b-535">Step 22: Add Load Balanced Endpoints and ACLs</span></span>
    #Endpoints
    $epname="sqlIntEP"
    $prot="tcp"
    $locport=1433
    $pubport=1433
    Get-AzureVM –ServiceName $destcloudsvc –Name $vmNameToMigrate  | Add-AzureEndpoint -Name $epname -Protocol $prot -LocalPort $locport -PublicPort $pubport -ProbePort 59999 -ProbeIntervalInSeconds 5 -ProbeTimeoutInSeconds 11  -ProbeProtocol "TCP" -InternalLoadBalancerName $ilb -LBSetName $ilb -DirectServerReturn $true | Update-AzureVM


    #STOP!!! CHECK in the Azure portal or Machine Endpoints through PowerShell that these Endpoints are created!

    #SET ACLs or Azure Network Security Groups & Windows FWs

    #http://msdn.microsoft.com/library/azure/dn495192.aspx

#### <a name="step-23-test-failover"></a><span data-ttu-id="3791b-536">Step 23: Test failover</span><span class="sxs-lookup"><span data-stu-id="3791b-536">Step 23: Test failover</span></span>
<span data-ttu-id="3791b-537">Wait for the migrated node to synchronize with the on-premises Always On node.</span><span class="sxs-lookup"><span data-stu-id="3791b-537">Wait for the migrated node to synchronize with the on-premises Always On node.</span></span> <span data-ttu-id="3791b-538">Place it into synchronous replication mode and wait until it is synchronized.</span><span class="sxs-lookup"><span data-stu-id="3791b-538">Place it into synchronous replication mode and wait until it is synchronized.</span></span> <span data-ttu-id="3791b-539">Then failover from on-prem to the first node migrated, which is the AFP.</span><span class="sxs-lookup"><span data-stu-id="3791b-539">Then failover from on-prem to the first node migrated, which is the AFP.</span></span> <span data-ttu-id="3791b-540">Once that has worked, change the last migrated node to the AFP.</span><span class="sxs-lookup"><span data-stu-id="3791b-540">Once that has worked, change the last migrated node to the AFP.</span></span>

<span data-ttu-id="3791b-541">You should test failovers between all nodes and run though chaos tests to ensure failovers work as expected and in a timely manor.</span><span class="sxs-lookup"><span data-stu-id="3791b-541">You should test failovers between all nodes and run though chaos tests to ensure failovers work as expected and in a timely manor.</span></span>

#### <a name="step-24-put-back-cluster-quorum-settings--dns-ttl--failover-pntrs--sync-settings"></a><span data-ttu-id="3791b-542">Step 24: Put back cluster quorum settings / DNS TTL / Failover Pntrs / Sync Settings</span><span class="sxs-lookup"><span data-stu-id="3791b-542">Step 24: Put back cluster quorum settings / DNS TTL / Failover Pntrs / Sync Settings</span></span>
##### <a name="adding-ip-address-resource-on-same-subnet"></a><span data-ttu-id="3791b-543">Adding IP Address Resource on Same Subnet</span><span class="sxs-lookup"><span data-stu-id="3791b-543">Adding IP Address Resource on Same Subnet</span></span>
<span data-ttu-id="3791b-544">If you have only two SQL Servers and want to migrate them to a new cloud service, but want to keep them on the same subnet, you can avoid taking the listener offline to delete the original Always On IP Address and add the New IP Address.</span><span class="sxs-lookup"><span data-stu-id="3791b-544">If you have only two SQL Servers and want to migrate them to a new cloud service, but want to keep them on the same subnet, you can avoid taking the listener offline to delete the original Always On IP Address and add the New IP Address.</span></span> <span data-ttu-id="3791b-545">If you are migrating the VMs to another subnet, you do not need to do this as there is an additional cluster network that references that subnet.</span><span class="sxs-lookup"><span data-stu-id="3791b-545">If you are migrating the VMs to another subnet, you do not need to do this as there is an additional cluster network that references that subnet.</span></span>

<span data-ttu-id="3791b-546">Once you have brought up the migrated secondary and added in the new IP Address resource for the new cloud service before failover the existing Primary, you should take these steps within the Cluster Failover Manager:</span><span class="sxs-lookup"><span data-stu-id="3791b-546">Once you have brought up the migrated secondary and added in the new IP Address resource for the new cloud service before failover the existing Primary, you should take these steps within the Cluster Failover Manager:</span></span>

<span data-ttu-id="3791b-547">To add in IP Address, see the [Appendix](#appendix-migrating-a-multisite-alwayson-cluster-to-premium-storage), step 14.</span><span class="sxs-lookup"><span data-stu-id="3791b-547">To add in IP Address, see the [Appendix](#appendix-migrating-a-multisite-alwayson-cluster-to-premium-storage), step 14.</span></span>

1. <span data-ttu-id="3791b-548">For the current IP Address resource, change the possible owner to ‘Existing Primary SQL Server’, in the example, ‘dansqlams4’:</span><span class="sxs-lookup"><span data-stu-id="3791b-548">For the current IP Address resource, change the possible owner to ‘Existing Primary SQL Server’, in the example, ‘dansqlams4’:</span></span>

    ![Appendix13][23]
2. <span data-ttu-id="3791b-550">For the new IP Address resource, change the possible owner to ‘Migrated secondary SQL Server’, in the example, ‘dansqlams5’:</span><span class="sxs-lookup"><span data-stu-id="3791b-550">For the new IP Address resource, change the possible owner to ‘Migrated secondary SQL Server’, in the example, ‘dansqlams5’:</span></span>

    ![Appendix14][24]
3. <span data-ttu-id="3791b-552">Once this is set you can failover, and when the last node is migrated the Possible Owners should be edited so that node is added as a Possible Owner:</span><span class="sxs-lookup"><span data-stu-id="3791b-552">Once this is set you can failover, and when the last node is migrated the Possible Owners should be edited so that node is added as a Possible Owner:</span></span>

    ![Appendix15][25]

## <a name="additional-resources"></a><span data-ttu-id="3791b-554">Additional resources</span><span class="sxs-lookup"><span data-stu-id="3791b-554">Additional resources</span></span>
* [<span data-ttu-id="3791b-555">Azure Premium Storage</span><span class="sxs-lookup"><span data-stu-id="3791b-555">Azure Premium Storage</span></span>](../premium-storage.md)
* [<span data-ttu-id="3791b-556">Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="3791b-556">Virtual Machines</span></span>](https://azure.microsoft.com/services/virtual-machines/)
* [<span data-ttu-id="3791b-557">SQL Server in Azure Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="3791b-557">SQL Server in Azure Virtual Machines</span></span>](../sql/virtual-machines-windows-sql-server-iaas-overview.md)

<!-- IMAGES -->
[1]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/1_VNET_Portal.png
[2]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/2_Diskname_Lun.png
[3]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/3_Virtual_Disk_Properties.png
[4]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/4_Virtual_Disk_Properties_Details.png
[5]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/5_Get_Storage_Pool.png
[6]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/6_Deployments_Always_On.png
[7]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/7_Add_More_Secondaries.png
[8]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/8_Use_Existing_Secondary_Single_Site.png
[9]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/9_Use_Existing_Secondary_Multi_Site.png
[10]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/9_Use_Existing_Secondary_Multi_Site_b.png
[11]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_01.png
[12]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_02.png
[13]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_03.png
[14]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_04.png
[15]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_05.png
[16]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_06.png
[17]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_07.png
[18]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_08.png
[19]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_09.png
[20]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_10.png
[21]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_11.png
[22]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_12.png
[23]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_13.png
[24]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_14.png
[25]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_15.png
