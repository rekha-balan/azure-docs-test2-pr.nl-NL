---
title: Use Azure Premium Storage with SQL Server | Microsoft Docs
description: This article uses resources created with the classic deployment model, and gives guidance on using Azure Premium Storage with SQL Server running on Azure Virtual Machines.
services: virtual-machines-windows
documentationcenter: ''
author: danielsollondon
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 7ccf99d7-7cce-4e3d-bbab-21b751ab0e88
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 11/28/2016
ms.author: jroth
ms.openlocfilehash: f31830aea102088de145073f5cbb374c95fe3178
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551206"
---
# <a name="use-azure-premium-storage-with-sql-server-on-virtual-machines"></a><span data-ttu-id="39ee1-103">Use Azure Premium Storage with SQL Server on Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="39ee1-103">Use Azure Premium Storage with SQL Server on Virtual Machines</span></span>
## <a name="overview"></a><span data-ttu-id="39ee1-104">Overview</span><span class="sxs-lookup"><span data-stu-id="39ee1-104">Overview</span></span>
<span data-ttu-id="39ee1-105">[Azure Premium Storage](../../../storage/storage-premium-storage.md) is the next generation of storage that provides low latency and high throughput IO.</span><span class="sxs-lookup"><span data-stu-id="39ee1-105">[Azure Premium Storage](../../../storage/storage-premium-storage.md) is the next generation of storage that provides low latency and high throughput IO.</span></span> <span data-ttu-id="39ee1-106">It works best for key IO intensive workloads, such as SQL Server on IaaS [Virtual Machines](https://azure.microsoft.com/services/virtual-machines/).</span><span class="sxs-lookup"><span data-stu-id="39ee1-106">It works best for key IO intensive workloads, such as SQL Server on IaaS [Virtual Machines](https://azure.microsoft.com/services/virtual-machines/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="39ee1-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="39ee1-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="39ee1-108">This article covers using the Classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="39ee1-108">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="39ee1-109">Microsoft recommends that most new deployments use the Resource Manager model.</span><span class="sxs-lookup"><span data-stu-id="39ee1-109">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="39ee1-110">This article provides planning and guidance for migrating a Virtual Machine running SQL Server to use Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="39ee1-110">This article provides planning and guidance for migrating a Virtual Machine running SQL Server to use Premium Storage.</span></span> <span data-ttu-id="39ee1-111">This includes Azure infrastructure (networking, storage) and guest Windows VM steps.</span><span class="sxs-lookup"><span data-stu-id="39ee1-111">This includes Azure infrastructure (networking, storage) and guest Windows VM steps.</span></span> <span data-ttu-id="39ee1-112">The example in the [Appendix](#appendix-migrating-a-multisite-alwayson-cluster-to-premium-storage) shows a full comprehensive end to end migration of how to move larger VMs to take advantage of improved local SSD storage with PowerShell.</span><span class="sxs-lookup"><span data-stu-id="39ee1-112">The example in the [Appendix](#appendix-migrating-a-multisite-alwayson-cluster-to-premium-storage) shows a full comprehensive end to end migration of how to move larger VMs to take advantage of improved local SSD storage with PowerShell.</span></span>

<span data-ttu-id="39ee1-113">It is important to understand the end-to-end process of utilizing Azure Premium Storage with SQL Server on IAAS VMs.</span><span class="sxs-lookup"><span data-stu-id="39ee1-113">It is important to understand the end-to-end process of utilizing Azure Premium Storage with SQL Server on IAAS VMs.</span></span> <span data-ttu-id="39ee1-114">This includes:</span><span class="sxs-lookup"><span data-stu-id="39ee1-114">This includes:</span></span>

* <span data-ttu-id="39ee1-115">Identification of the prerequisites to use Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="39ee1-115">Identification of the prerequisites to use Premium Storage.</span></span>
* <span data-ttu-id="39ee1-116">Examples of deploying SQL Server on IaaS to Premium Storage for new deployments.</span><span class="sxs-lookup"><span data-stu-id="39ee1-116">Examples of deploying SQL Server on IaaS to Premium Storage for new deployments.</span></span>
* <span data-ttu-id="39ee1-117">Examples of migrating existing deployments, both stand-alone servers and deployments using SQL Always On Availability Groups.</span><span class="sxs-lookup"><span data-stu-id="39ee1-117">Examples of migrating existing deployments, both stand-alone servers and deployments using SQL Always On Availability Groups.</span></span>
* <span data-ttu-id="39ee1-118">Possible migration approaches.</span><span class="sxs-lookup"><span data-stu-id="39ee1-118">Possible migration approaches.</span></span>
* <span data-ttu-id="39ee1-119">Full end-to-end example showing Azure, Windows, and SQL Server steps for the migration of an existing Always On implementation.</span><span class="sxs-lookup"><span data-stu-id="39ee1-119">Full end-to-end example showing Azure, Windows, and SQL Server steps for the migration of an existing Always On implementation.</span></span>

<span data-ttu-id="39ee1-120">For more background information on SQL Server in Azure Virtual Machines, see [SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="39ee1-120">For more background information on SQL Server in Azure Virtual Machines, see [SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

<span data-ttu-id="39ee1-121">**Author:** Daniel Sol **Technical Reviewers:** Luis Carlos Vargas Herring, Sanjay Mishra, Pravin Mital, Juergen Thomas, Gonzalo Ruiz.</span><span class="sxs-lookup"><span data-stu-id="39ee1-121">**Author:** Daniel Sol **Technical Reviewers:** Luis Carlos Vargas Herring, Sanjay Mishra, Pravin Mital, Juergen Thomas, Gonzalo Ruiz.</span></span>

## <a name="prerequisites-for-premium-storage"></a><span data-ttu-id="39ee1-122">Prerequisites for Premium Storage</span><span class="sxs-lookup"><span data-stu-id="39ee1-122">Prerequisites for Premium Storage</span></span>
<span data-ttu-id="39ee1-123">There are several prerequisites for using Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="39ee1-123">There are several prerequisites for using Premium Storage.</span></span>

### <a name="machine-size"></a><span data-ttu-id="39ee1-124">Machine size</span><span class="sxs-lookup"><span data-stu-id="39ee1-124">Machine size</span></span>
<span data-ttu-id="39ee1-125">For using Premium Storage you will need to use DS series Virtual Machines (VM).</span><span class="sxs-lookup"><span data-stu-id="39ee1-125">For using Premium Storage you will need to use DS series Virtual Machines (VM).</span></span> <span data-ttu-id="39ee1-126">If you have not used DS Series machines in your cloud service before, you must delete the existing VM, keep the attached disks, and then create a new cloud service before recreating the VM as DS\* role size.</span><span class="sxs-lookup"><span data-stu-id="39ee1-126">If you have not used DS Series machines in your cloud service before, you must delete the existing VM, keep the attached disks, and then create a new cloud service before recreating the VM as DS\* role size.</span></span> <span data-ttu-id="39ee1-127">For more information on Virtual Machine sizes, see [Virtual Machine and Cloud Service Sizes for Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="39ee1-127">For more information on Virtual Machine sizes, see [Virtual Machine and Cloud Service Sizes for Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

### <a name="cloud-services"></a><span data-ttu-id="39ee1-128">Cloud services</span><span class="sxs-lookup"><span data-stu-id="39ee1-128">Cloud services</span></span>
<span data-ttu-id="39ee1-129">You can only use DS\* VMs with Premium Storage when they are created in a new cloud service.</span><span class="sxs-lookup"><span data-stu-id="39ee1-129">You can only use DS\* VMs with Premium Storage when they are created in a new cloud service.</span></span> <span data-ttu-id="39ee1-130">If you are using SQL Server Always On in Azure, the Always On Listener will refer to the Azure Internal or External Load Balancer IP address that is associated with a cloud service.</span><span class="sxs-lookup"><span data-stu-id="39ee1-130">If you are using SQL Server Always On in Azure, the Always On Listener will refer to the Azure Internal or External Load Balancer IP address that is associated with a cloud service.</span></span> <span data-ttu-id="39ee1-131">This article focuses on how to migrate while maintaining availability in this scenario.</span><span class="sxs-lookup"><span data-stu-id="39ee1-131">This article focuses on how to migrate while maintaining availability in this scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="39ee1-132">A DS\* Series must be the first VM that is deployed to the new Cloud Service.</span><span class="sxs-lookup"><span data-stu-id="39ee1-132">A DS\* Series must be the first VM that is deployed to the new Cloud Service.</span></span>
>
>

### <a name="regional-vnets"></a><span data-ttu-id="39ee1-133">Regional VNETS</span><span class="sxs-lookup"><span data-stu-id="39ee1-133">Regional VNETS</span></span>
<span data-ttu-id="39ee1-134">For DS\* VMs you must configure the Virtual Network (VNET) hosting your VMs to be regional.</span><span class="sxs-lookup"><span data-stu-id="39ee1-134">For DS\* VMs you must configure the Virtual Network (VNET) hosting your VMs to be regional.</span></span> <span data-ttu-id="39ee1-135">This “widens” the VNET is to allow the larger VMs to be provisioned in other clusters and allow communication between them.</span><span class="sxs-lookup"><span data-stu-id="39ee1-135">This “widens” the VNET is to allow the larger VMs to be provisioned in other clusters and allow communication between them.</span></span> <span data-ttu-id="39ee1-136">In the following screenshot, the highlighted Location shows regional VNETs, whereas the first result shows a “narrow” VNET.</span><span class="sxs-lookup"><span data-stu-id="39ee1-136">In the following screenshot, the highlighted Location shows regional VNETs, whereas the first result shows a “narrow” VNET.</span></span>

![RegionalVNET][1]

<span data-ttu-id="39ee1-138">You can raise a Microsoft support ticket to migrate to a regional VNET, Microsoft will make a change, then to complete the migration to regional VNETs, change the property AffinityGroup in the network configuration.</span><span class="sxs-lookup"><span data-stu-id="39ee1-138">You can raise a Microsoft support ticket to migrate to a regional VNET, Microsoft will make a change, then to complete the migration to regional VNETs, change the property AffinityGroup in the network configuration.</span></span> <span data-ttu-id="39ee1-139">First export the Network Configuration in PowerShell, and then replace the **AffinityGroup** property in the **VirtualNetworkSite** element with a **Location** property.</span><span class="sxs-lookup"><span data-stu-id="39ee1-139">First export the Network Configuration in PowerShell, and then replace the **AffinityGroup** property in the **VirtualNetworkSite** element with a **Location** property.</span></span> <span data-ttu-id="39ee1-140">Specify `Location = XXXX` where `XXXX` is an Azure region.</span><span class="sxs-lookup"><span data-stu-id="39ee1-140">Specify `Location = XXXX` where `XXXX` is an Azure region.</span></span> <span data-ttu-id="39ee1-141">Then import the new configuration.</span><span class="sxs-lookup"><span data-stu-id="39ee1-141">Then import the new configuration.</span></span>

<span data-ttu-id="39ee1-142">For example, considering the following VNET configuration:</span><span class="sxs-lookup"><span data-stu-id="39ee1-142">For example, considering the following VNET configuration:</span></span>

    <VirtualNetworkSite name="danAzureSQLnet" AffinityGroup="AzureSQLNetwork">
    <AddressSpace>
      <AddressPrefix>10.0.0.0/8</AddressPrefix>
      <AddressPrefix>172.16.0.0/12</AddressPrefix>
    </AddressSpace>
    <Subnets>
    ...
    </VirtualNetworkSite>

<span data-ttu-id="39ee1-143">To move this to a regional VNET in West Europe, change the configuration to the following:</span><span class="sxs-lookup"><span data-stu-id="39ee1-143">To move this to a regional VNET in West Europe, change the configuration to the following:</span></span>

    <VirtualNetworkSite name="danAzureSQLnet" Location="West Europe">
    <AddressSpace>
      <AddressPrefix>10.0.0.0/8</AddressPrefix>
      <AddressPrefix>172.16.0.0/12</AddressPrefix>
    </AddressSpace>
    <Subnets>
    ...
    </VirtualNetworkSite>

### <a name="storage-accounts"></a><span data-ttu-id="39ee1-144">Storage accounts</span><span class="sxs-lookup"><span data-stu-id="39ee1-144">Storage accounts</span></span>
<span data-ttu-id="39ee1-145">You will need to create a new storage account that is configured for Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="39ee1-145">You will need to create a new storage account that is configured for Premium Storage.</span></span> <span data-ttu-id="39ee1-146">Note that the use of Premium Storage is set at the storage account, not on individual VHDs, however when using a DS\* Series VM you can attach VHD’s from Premium and Standard Storage accounts.</span><span class="sxs-lookup"><span data-stu-id="39ee1-146">Note that the use of Premium Storage is set at the storage account, not on individual VHDs, however when using a DS\* Series VM you can attach VHD’s from Premium and Standard Storage accounts.</span></span> <span data-ttu-id="39ee1-147">You may consider this if you do not want to place the OS VHD on to the Premium Storage account.</span><span class="sxs-lookup"><span data-stu-id="39ee1-147">You may consider this if you do not want to place the OS VHD on to the Premium Storage account.</span></span>

<span data-ttu-id="39ee1-148">The following **New-AzureStorageAccountPowerShell** command with the "Premium_LRS" **Type** creates a Premium Storage Account:</span><span class="sxs-lookup"><span data-stu-id="39ee1-148">The following **New-AzureStorageAccountPowerShell** command with the "Premium_LRS" **Type** creates a Premium Storage Account:</span></span>

    $newstorageaccountname = "danpremstor"
    New-AzureStorageAccount -StorageAccountName $newstorageaccountname -Location "West Europe" -Type "Premium_LRS"   

### <a name="vhds-cache-settings"></a><span data-ttu-id="39ee1-149">VHDs Cache Settings</span><span class="sxs-lookup"><span data-stu-id="39ee1-149">VHDs Cache Settings</span></span>
<span data-ttu-id="39ee1-150">The main difference between creating disks that are part of a Premium Storage account is the disk cache setting.</span><span class="sxs-lookup"><span data-stu-id="39ee1-150">The main difference between creating disks that are part of a Premium Storage account is the disk cache setting.</span></span> <span data-ttu-id="39ee1-151">For SQL Server Data volume disks it is recommended that you use ‘**Read Caching**’.</span><span class="sxs-lookup"><span data-stu-id="39ee1-151">For SQL Server Data volume disks it is recommended that you use ‘**Read Caching**’.</span></span> <span data-ttu-id="39ee1-152">For Transaction log volumes, the disk cache setting should be set to ‘**None**’.</span><span class="sxs-lookup"><span data-stu-id="39ee1-152">For Transaction log volumes, the disk cache setting should be set to ‘**None**’.</span></span> <span data-ttu-id="39ee1-153">This is different from the recommendations for Standard Storage accounts.</span><span class="sxs-lookup"><span data-stu-id="39ee1-153">This is different from the recommendations for Standard Storage accounts.</span></span>

<span data-ttu-id="39ee1-154">Once the VHDs have been attached, the cache setting cannot be altered.</span><span class="sxs-lookup"><span data-stu-id="39ee1-154">Once the VHDs have been attached, the cache setting cannot be altered.</span></span> <span data-ttu-id="39ee1-155">You would need to detach and reattach the VHD with an updated cache setting.</span><span class="sxs-lookup"><span data-stu-id="39ee1-155">You would need to detach and reattach the VHD with an updated cache setting.</span></span>

### <a name="windows-storage-spaces"></a><span data-ttu-id="39ee1-156">Windows storage spaces</span><span class="sxs-lookup"><span data-stu-id="39ee1-156">Windows storage spaces</span></span>
<span data-ttu-id="39ee1-157">You can use [Windows Storage Spaces](https://technet.microsoft.com/library/hh831739.aspx) as you did with previous Standard Storage, this will allow you to migrate a VM that is already utilizing Storage Spaces.</span><span class="sxs-lookup"><span data-stu-id="39ee1-157">You can use [Windows Storage Spaces](https://technet.microsoft.com/library/hh831739.aspx) as you did with previous Standard Storage, this will allow you to migrate a VM that is already utilizing Storage Spaces.</span></span> <span data-ttu-id="39ee1-158">The example in [Appendix](#appendix-migrating-a-multisite-alwayson-cluster-to-premium-storage) (step 9 and forward) demonstrates the Powershell code to extract and import a VM with multiple attached VHDs.</span><span class="sxs-lookup"><span data-stu-id="39ee1-158">The example in [Appendix](#appendix-migrating-a-multisite-alwayson-cluster-to-premium-storage) (step 9 and forward) demonstrates the Powershell code to extract and import a VM with multiple attached VHDs.</span></span>

<span data-ttu-id="39ee1-159">Storage Pools were used with Standard Azure storage account to enhance throughput and reduce latency.</span><span class="sxs-lookup"><span data-stu-id="39ee1-159">Storage Pools were used with Standard Azure storage account to enhance throughput and reduce latency.</span></span> <span data-ttu-id="39ee1-160">You might find value in testing Storage Pools with Premium Storage for new deployments, but they do add additional complexity with storage setup.</span><span class="sxs-lookup"><span data-stu-id="39ee1-160">You might find value in testing Storage Pools with Premium Storage for new deployments, but they do add additional complexity with storage setup.</span></span>

#### <a name="how-to-find-which-azure-virtual-disks-map-to-storage-pools"></a><span data-ttu-id="39ee1-161">How to find which Azure Virtual Disks map to storage pools</span><span class="sxs-lookup"><span data-stu-id="39ee1-161">How to find which Azure Virtual Disks map to storage pools</span></span>
<span data-ttu-id="39ee1-162">As there are different cache setting recommendations for attached VHDs, you might decide to copy the VHDs to a Premium Storage account.</span><span class="sxs-lookup"><span data-stu-id="39ee1-162">As there are different cache setting recommendations for attached VHDs, you might decide to copy the VHDs to a Premium Storage account.</span></span> <span data-ttu-id="39ee1-163">However, when you reattach them to the new DS series VM, you might need to alter the cache settings.</span><span class="sxs-lookup"><span data-stu-id="39ee1-163">However, when you reattach them to the new DS series VM, you might need to alter the cache settings.</span></span> <span data-ttu-id="39ee1-164">It is simpler to apply the Premium Storage recommended cache settings when you have separate VHDs for the SQL Data files and log files (rather than a single VHD that contains both).</span><span class="sxs-lookup"><span data-stu-id="39ee1-164">It is simpler to apply the Premium Storage recommended cache settings when you have separate VHDs for the SQL Data files and log files (rather than a single VHD that contains both).</span></span>

> [!NOTE]
> <span data-ttu-id="39ee1-165">If you have SQL Server data and log files on the same volume, the caching option you choose depends on the IO access patterns for your database workloads.</span><span class="sxs-lookup"><span data-stu-id="39ee1-165">If you have SQL Server data and log files on the same volume, the caching option you choose depends on the IO access patterns for your database workloads.</span></span> <span data-ttu-id="39ee1-166">Only testing can demonstrate which caching option is best for this scenario.</span><span class="sxs-lookup"><span data-stu-id="39ee1-166">Only testing can demonstrate which caching option is best for this scenario.</span></span>
>
>

<span data-ttu-id="39ee1-167">However, if you are using Windows Storage Spaces which are made up of multiple VHDs you will need to look at your original scripts to identify which attached VHDs are in what specific pool, so you can then set the cache settings accordingly for each disk.</span><span class="sxs-lookup"><span data-stu-id="39ee1-167">However, if you are using Windows Storage Spaces which are made up of multiple VHDs you will need to look at your original scripts to identify which attached VHDs are in what specific pool, so you can then set the cache settings accordingly for each disk.</span></span>

<span data-ttu-id="39ee1-168">If you do not have original script available to show you which VHDs map to the storage pool, you can use the following steps to determine the disk/storage pool mapping.</span><span class="sxs-lookup"><span data-stu-id="39ee1-168">If you do not have original script available to show you which VHDs map to the storage pool, you can use the following steps to determine the disk/storage pool mapping.</span></span>

<span data-ttu-id="39ee1-169">For each disk, use the following steps:</span><span class="sxs-lookup"><span data-stu-id="39ee1-169">For each disk, use the following steps:</span></span>

1. <span data-ttu-id="39ee1-170">Get list of disks attached to VM with the **Get-AzureVM** command:</span><span class="sxs-lookup"><span data-stu-id="39ee1-170">Get list of disks attached to VM with the **Get-AzureVM** command:</span></span>

    <span data-ttu-id="39ee1-171">Get-AzureVM -ServiceName <servicename> -Name <vmname> | Get-AzureDataDisk</span><span class="sxs-lookup"><span data-stu-id="39ee1-171">Get-AzureVM -ServiceName <servicename> -Name <vmname> | Get-AzureDataDisk</span></span>
2. <span data-ttu-id="39ee1-172">Note the Diskname and LUN.</span><span class="sxs-lookup"><span data-stu-id="39ee1-172">Note the Diskname and LUN.</span></span>

    ![DisknameAndLUN][2]
3. <span data-ttu-id="39ee1-174">Remote desktop into the VM.</span><span class="sxs-lookup"><span data-stu-id="39ee1-174">Remote desktop into the VM.</span></span> <span data-ttu-id="39ee1-175">Then go to **Computer Management** | **Device Manager** | **Disk Drives**.</span><span class="sxs-lookup"><span data-stu-id="39ee1-175">Then go to **Computer Management** | **Device Manager** | **Disk Drives**.</span></span> <span data-ttu-id="39ee1-176">Look at the properties of each of the ‘Microsoft Virtual Disks’</span><span class="sxs-lookup"><span data-stu-id="39ee1-176">Look at the properties of each of the ‘Microsoft Virtual Disks’</span></span>

    ![VirtualDiskProperties][3]
4. <span data-ttu-id="39ee1-178">The LUN number here is a reference to the LUN number you specify when attaching the VHD to the VM.</span><span class="sxs-lookup"><span data-stu-id="39ee1-178">The LUN number here is a reference to the LUN number you specify when attaching the VHD to the VM.</span></span>
5. <span data-ttu-id="39ee1-179">For the ‘Microsoft Virtual Disk’ go to the **Details** tab, then in the **Property** list, go to **Driver Key**.</span><span class="sxs-lookup"><span data-stu-id="39ee1-179">For the ‘Microsoft Virtual Disk’ go to the **Details** tab, then in the **Property** list, go to **Driver Key**.</span></span> <span data-ttu-id="39ee1-180">In the **Value**, note the **Offset**, which is 0002 in the following screenshot.</span><span class="sxs-lookup"><span data-stu-id="39ee1-180">In the **Value**, note the **Offset**, which is 0002 in the following screenshot.</span></span> <span data-ttu-id="39ee1-181">The 0002 denotes the PhysicalDisk2 that the storage pool references.</span><span class="sxs-lookup"><span data-stu-id="39ee1-181">The 0002 denotes the PhysicalDisk2 that the storage pool references.</span></span>

    ![VirtualDiskPropertyDetails][4]
6. <span data-ttu-id="39ee1-183">For each storage pool, dump out the associated disks:</span><span class="sxs-lookup"><span data-stu-id="39ee1-183">For each storage pool, dump out the associated disks:</span></span>

    <span data-ttu-id="39ee1-184">Get-StoragePool -FriendlyName AMS1pooldata | Get-PhysicalDisk</span><span class="sxs-lookup"><span data-stu-id="39ee1-184">Get-StoragePool -FriendlyName AMS1pooldata | Get-PhysicalDisk</span></span>

    ![GetStoragePool][5]

<span data-ttu-id="39ee1-186">Now you can use this information to associate attached VHDs to Physical Disks in Storage Pools.</span><span class="sxs-lookup"><span data-stu-id="39ee1-186">Now you can use this information to associate attached VHDs to Physical Disks in Storage Pools.</span></span>

<span data-ttu-id="39ee1-187">Once you have mapped VHDs to Physical Disks in Storage Pools you can then detach and copy them over to a Premium Storage account, then attach them with the correct cache setting.</span><span class="sxs-lookup"><span data-stu-id="39ee1-187">Once you have mapped VHDs to Physical Disks in Storage Pools you can then detach and copy them over to a Premium Storage account, then attach them with the correct cache setting.</span></span> <span data-ttu-id="39ee1-188">Please see the example in the [Appendix](#appendix-migrating-a-multisite-alwayson-cluster-to-premium-storage), steps 8 through 12.</span><span class="sxs-lookup"><span data-stu-id="39ee1-188">Please see the example in the [Appendix](#appendix-migrating-a-multisite-alwayson-cluster-to-premium-storage), steps 8 through 12.</span></span> <span data-ttu-id="39ee1-189">These steps show how to extract a VM-attached VHD disk configuration to a CSV file, copy the VHDs, alter the disk configuration cache settings, and finally redeploy the VM as a DS series VM with all the attached disks.</span><span class="sxs-lookup"><span data-stu-id="39ee1-189">These steps show how to extract a VM-attached VHD disk configuration to a CSV file, copy the VHDs, alter the disk configuration cache settings, and finally redeploy the VM as a DS series VM with all the attached disks.</span></span>

### <a name="vm-storage-bandwidth-and-vhd-storage-throughput"></a><span data-ttu-id="39ee1-190">VM storage bandwidth and VHD storage throughput</span><span class="sxs-lookup"><span data-stu-id="39ee1-190">VM storage bandwidth and VHD storage throughput</span></span>
<span data-ttu-id="39ee1-191">The amount of storage performance depends on the DS\* VM size specified and the VHD sizes.</span><span class="sxs-lookup"><span data-stu-id="39ee1-191">The amount of storage performance depends on the DS\* VM size specified and the VHD sizes.</span></span> <span data-ttu-id="39ee1-192">The VMs have different allowances for the number of VHDs that can be attached and the maximum bandwidth they will support (MB/s).</span><span class="sxs-lookup"><span data-stu-id="39ee1-192">The VMs have different allowances for the number of VHDs that can be attached and the maximum bandwidth they will support (MB/s).</span></span> <span data-ttu-id="39ee1-193">For the specific bandwidth numbers, see [Virtual Machine and Cloud Service Sizes for Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="39ee1-193">For the specific bandwidth numbers, see [Virtual Machine and Cloud Service Sizes for Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="39ee1-194">Increased IOPS are achieved with larger disk sizes.</span><span class="sxs-lookup"><span data-stu-id="39ee1-194">Increased IOPS are achieved with larger disk sizes.</span></span> <span data-ttu-id="39ee1-195">You should consider this when you think about your migration path.</span><span class="sxs-lookup"><span data-stu-id="39ee1-195">You should consider this when you think about your migration path.</span></span> <span data-ttu-id="39ee1-196">For details, [see the table for IOPS and Disk Types](../../../storage/storage-premium-storage.md#scalability-and-performance-targets).</span><span class="sxs-lookup"><span data-stu-id="39ee1-196">For details, [see the table for IOPS and Disk Types](../../../storage/storage-premium-storage.md#scalability-and-performance-targets).</span></span>

<span data-ttu-id="39ee1-197">Finally, consider that VMs have different maximum disk bandwidths they will support for all disks attached.</span><span class="sxs-lookup"><span data-stu-id="39ee1-197">Finally, consider that VMs have different maximum disk bandwidths they will support for all disks attached.</span></span> <span data-ttu-id="39ee1-198">Under high load, you could saturate the maximum disk bandwidth available for that VM role size.</span><span class="sxs-lookup"><span data-stu-id="39ee1-198">Under high load, you could saturate the maximum disk bandwidth available for that VM role size.</span></span> <span data-ttu-id="39ee1-199">For example a Standard_DS14 will support up to 512MB/s; therefore, with three P30 disks you could saturate the disk bandwidth of the VM.</span><span class="sxs-lookup"><span data-stu-id="39ee1-199">For example a Standard_DS14 will support up to 512MB/s; therefore, with three P30 disks you could saturate the disk bandwidth of the VM.</span></span> <span data-ttu-id="39ee1-200">But in this example, the throughput limit could be exceeded depending on the mix of read and write IOs.</span><span class="sxs-lookup"><span data-stu-id="39ee1-200">But in this example, the throughput limit could be exceeded depending on the mix of read and write IOs.</span></span>

## <a name="new-deployments"></a><span data-ttu-id="39ee1-201">New deployments</span><span class="sxs-lookup"><span data-stu-id="39ee1-201">New deployments</span></span>
<span data-ttu-id="39ee1-202">The next two sections demonstrate how you can deploy SQL Server VMs to Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="39ee1-202">The next two sections demonstrate how you can deploy SQL Server VMs to Premium Storage.</span></span> <span data-ttu-id="39ee1-203">As mentioned before, you do not necessarily need to place the OS disk onto Premium storage.</span><span class="sxs-lookup"><span data-stu-id="39ee1-203">As mentioned before, you do not necessarily need to place the OS disk onto Premium storage.</span></span> <span data-ttu-id="39ee1-204">You might choose to do this if you are intending to place any intensive IO workloads on the OS VHD.</span><span class="sxs-lookup"><span data-stu-id="39ee1-204">You might choose to do this if you are intending to place any intensive IO workloads on the OS VHD.</span></span>

<span data-ttu-id="39ee1-205">The first example demonstrates utilizing existing Azure Gallery Images.</span><span class="sxs-lookup"><span data-stu-id="39ee1-205">The first example demonstrates utilizing existing Azure Gallery Images.</span></span> <span data-ttu-id="39ee1-206">The second example shows how to use a custom VM image that you have in an existing Standard storage account.</span><span class="sxs-lookup"><span data-stu-id="39ee1-206">The second example shows how to use a custom VM image that you have in an existing Standard storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="39ee1-207">These examples assume that you have already created a Regional VNET.</span><span class="sxs-lookup"><span data-stu-id="39ee1-207">These examples assume that you have already created a Regional VNET.</span></span>
>
>

### <a name="create-a-new-vm-with-premium-storage-with-gallery-image"></a><span data-ttu-id="39ee1-208">Create a new VM with Premium Storage with Gallery Image</span><span class="sxs-lookup"><span data-stu-id="39ee1-208">Create a new VM with Premium Storage with Gallery Image</span></span>
<span data-ttu-id="39ee1-209">The example below shows how to place the OS VHD onto premium storage and attach Premium Storage VHDs.</span><span class="sxs-lookup"><span data-stu-id="39ee1-209">The example below shows how to place the OS VHD onto premium storage and attach Premium Storage VHDs.</span></span> <span data-ttu-id="39ee1-210">However, you can also place the OS disk in a Standard Storage account and then attach VHDs that reside in a Premium Storage account.</span><span class="sxs-lookup"><span data-stu-id="39ee1-210">However, you can also place the OS disk in a Standard Storage account and then attach VHDs that reside in a Premium Storage account.</span></span> <span data-ttu-id="39ee1-211">Both scenarios are demonstrated.</span><span class="sxs-lookup"><span data-stu-id="39ee1-211">Both scenarios are demonstrated.</span></span>

    $mysubscription = "DansSubscription"
    $location = "West Europe"

    #Set up subscription
    Set-AzureSubscription -SubscriptionName $mysubscription
    Select-AzureSubscription -SubscriptionName $mysubscription -Current  

#### <a name="step-1-create-a-premium-storage-account"></a><span data-ttu-id="39ee1-212">Step 1: Create a Premium Storage Account</span><span class="sxs-lookup"><span data-stu-id="39ee1-212">Step 1: Create a Premium Storage Account</span></span>
    #Create Premium Storage account, note Type
    $newxiostorageaccountname = "danspremsams"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountname -Location $location -Type "Premium_LRS"  


#### <a name="step-2-create-a-new-cloud-service"></a><span data-ttu-id="39ee1-213">Step 2: Create a New Cloud Service</span><span class="sxs-lookup"><span data-stu-id="39ee1-213">Step 2: Create a New Cloud Service</span></span>
    $destcloudsvc = "danNewSvcAms"
    New-AzureService $destcloudsvc -Location $location


#### <a name="step-3-reserve-a-cloud-service-vip-optional"></a><span data-ttu-id="39ee1-214">Step 3: Reserve a Cloud Service VIP (Optional)</span><span class="sxs-lookup"><span data-stu-id="39ee1-214">Step 3: Reserve a Cloud Service VIP (Optional)</span></span>
    #check exisitng reserved VIP
    Get-AzureReservedIP

    $reservedVIPName = “sqlcloudVIP”
    New-AzureReservedIP –ReservedIPName $reservedVIPName –Label $reservedVIPName –Location $location

#### <a name="step-4-create-a-vm-container"></a><span data-ttu-id="39ee1-215">Step 4: Create a VM Container</span><span class="sxs-lookup"><span data-stu-id="39ee1-215">Step 4: Create a VM Container</span></span>
    #Generate storage keys for later
    $xiostorage = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountname

    ##Generate storage acc contexts
    $xioContext = New-AzureStorageContext –StorageAccountName $newxiostorageaccountname -StorageAccountKey $xiostorage.Primary   

    #Create container
    $containerName = 'vhds'
    New-AzureStorageContainer -Name $containerName -Context $xioContext

#### <a name="step-5-placing-os-vhd-on-standard-or-premium-storage"></a><span data-ttu-id="39ee1-216">Step 5: Placing OS VHD on Standard or Premium Storage</span><span class="sxs-lookup"><span data-stu-id="39ee1-216">Step 5: Placing OS VHD on Standard or Premium Storage</span></span>
    #NOTE: Set up subscription and default storage account which will be used to place the OS VHD in

    #If you want to place the OS VHD Premium Storage Account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount  $newxiostorageaccountname  

    #If you wanted to place the OS VHD Standard Storage Account but attach Premium Storage VHDs then you would run this instead:
    $standardstorageaccountname = "danstdams"

    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount  $standardstorageaccountname

#### <a name="step-6-create-vm"></a><span data-ttu-id="39ee1-217">Step 6: Create VM</span><span class="sxs-lookup"><span data-stu-id="39ee1-217">Step 6: Create VM</span></span>
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
    #Note the size specified ‘-DiskSizeInGB 1023’, this will attach 2 x P30 Premium Storage Disk Type
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


### <a name="create-a-new-vm-to-use-premium-storage-with-a-custom-image"></a><span data-ttu-id="39ee1-218">Create a new VM to use Premium Storage with a custom image</span><span class="sxs-lookup"><span data-stu-id="39ee1-218">Create a new VM to use Premium Storage with a custom image</span></span>
<span data-ttu-id="39ee1-219">This scenario demonstrates where you have existing customized images that reside in a Standard Storage account.</span><span class="sxs-lookup"><span data-stu-id="39ee1-219">This scenario demonstrates where you have existing customized images that reside in a Standard Storage account.</span></span> <span data-ttu-id="39ee1-220">As mentioned if you want to place the OS VHD on Premium Storage you will need to copy the image that exists in the Standard Storage account and transfer them to a Premium Storage before it can be used.</span><span class="sxs-lookup"><span data-stu-id="39ee1-220">As mentioned if you want to place the OS VHD on Premium Storage you will need to copy the image that exists in the Standard Storage account and transfer them to a Premium Storage before it can be used.</span></span> <span data-ttu-id="39ee1-221">If you have an image on premise, you can also use this method to copy that directly to the Premium Storage account.</span><span class="sxs-lookup"><span data-stu-id="39ee1-221">If you have an image on premise, you can also use this method to copy that directly to the Premium Storage account.</span></span>

#### <a name="step-1-create-storage-account"></a><span data-ttu-id="39ee1-222">Step 1: Create Storage Account</span><span class="sxs-lookup"><span data-stu-id="39ee1-222">Step 1: Create Storage Account</span></span>
    $mysubscription = "DansSubscription"
    $location = "West Europe"

    #Create Premium Storage account
    $newxiostorageaccountname = "danspremsams"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountname -Location $location -Type "Premium_LRS"  

    #Standard Storage account
    $origstorageaccountname = "danstdams"

#### <a name="step-2-create-cloud-service"></a><span data-ttu-id="39ee1-223">Step 2 Create Cloud Service</span><span class="sxs-lookup"><span data-stu-id="39ee1-223">Step 2 Create Cloud Service</span></span>
    $destcloudsvc = "danNewSvcAms"
    New-AzureService $destcloudsvc -Location $location


#### <a name="step-3-use-existing-image"></a><span data-ttu-id="39ee1-224">Step 3: Use existing image</span><span class="sxs-lookup"><span data-stu-id="39ee1-224">Step 3: Use existing image</span></span>
<span data-ttu-id="39ee1-225">You can use an existing image.</span><span class="sxs-lookup"><span data-stu-id="39ee1-225">You can use an existing image.</span></span> <span data-ttu-id="39ee1-226">Or, you can [take an image of an existing machine](../classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="39ee1-226">Or, you can [take an image of an existing machine](../classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span> <span data-ttu-id="39ee1-227">Note the machine you image does not have to be DS\* machine.</span><span class="sxs-lookup"><span data-stu-id="39ee1-227">Note the machine you image does not have to be DS\* machine.</span></span> <span data-ttu-id="39ee1-228">Once you have the image, the following steps show how to copy it to the Premium Storage account with the **Start-AzureStorageBlobCopy** PowerShell commandlet.</span><span class="sxs-lookup"><span data-stu-id="39ee1-228">Once you have the image, the following steps show how to copy it to the Premium Storage account with the **Start-AzureStorageBlobCopy** PowerShell commandlet.</span></span>

    #Get storage account keys:
    #Standard Storage account
    $originalstorage =  Get-AzureStorageKey -StorageAccountName $origstorageaccountname
    #Premium Storage account
    $xiostorage = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountname

    #Set up contexts for the storage accounts:
    $origContext = New-AzureStorageContext  –StorageAccountName $origstorageaccountname -StorageAccountKey $originalstorage.Primary
    $destContext = New-AzureStorageContext  –StorageAccountName $newxiostorageaccountname -StorageAccountKey $xiostorage.Primary  

#### <a name="step-4-copy-blob-between-storage-accounts"></a><span data-ttu-id="39ee1-229">Step 4: Copy Blob between Storage Accounts</span><span class="sxs-lookup"><span data-stu-id="39ee1-229">Step 4: Copy Blob between Storage Accounts</span></span>
    #Get Image VHD
    $myImageVHD = "dansoldonorsql2k14-os-2015-04-15.vhd"
    $containerName = 'vhds'

    #Copy Blob between accounts
    $blob = Start-AzureStorageBlobCopy -SrcBlob $myImageVHD -SrcContainer $containerName `
    -DestContainer vhds -Destblob "prem-$myImageVHD" `
    -Context $origContext -DestContext $destContext  

#### <a name="step-5-regularly-check-copy-status"></a><span data-ttu-id="39ee1-230">Step 5: Regularly check copy status:</span><span class="sxs-lookup"><span data-stu-id="39ee1-230">Step 5: Regularly check copy status:</span></span>
    $blob | Get-AzureStorageBlobCopyState

#### <a name="step-6-add-image-disk-to-azure-disk-repository-in-subscription"></a><span data-ttu-id="39ee1-231">Step 6: Add Image disk to Azure disk Repository in Subscription</span><span class="sxs-lookup"><span data-stu-id="39ee1-231">Step 6: Add Image disk to Azure disk Repository in Subscription</span></span>
    $imageMediaLocation = $destContext.BlobEndPoint+"/"+$myImageVHD
    $newimageName = "prem"+"dansoldonorsql2k14"

    Add-AzureVMImage -ImageName $newimageName -MediaLocation $imageMediaLocation

> [!NOTE]
> <span data-ttu-id="39ee1-232">You may find that even though the status reports as success, you could still get a disk lease error.</span><span class="sxs-lookup"><span data-stu-id="39ee1-232">You may find that even though the status reports as success, you could still get a disk lease error.</span></span> <span data-ttu-id="39ee1-233">In this case, wait about 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="39ee1-233">In this case, wait about 10 minutes.</span></span>
>
>

#### <a name="step-7--build-the-vm"></a><span data-ttu-id="39ee1-234">Step 7:  Build the VM</span><span class="sxs-lookup"><span data-stu-id="39ee1-234">Step 7:  Build the VM</span></span>
<span data-ttu-id="39ee1-235">Here you are building the VM from your image and attaching two Premium Storage VHDs:</span><span class="sxs-lookup"><span data-stu-id="39ee1-235">Here you are building the VM from your image and attaching two Premium Storage VHDs:</span></span>

    $newimageName = "prem"+"dansoldonorsql2k14"
    #Set up Machine Specific Information
    $vmName = "dansolchild"
    $vnet = "westeur"
    $subnet = "Clients"
    $ipaddr = "192.168.0.41"

    #This will need to be a new cloud service
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

## <a name="existing-deployments-that-do-not-use-always-on-availability-groups"></a><span data-ttu-id="39ee1-236">Existing deployments that do not use Always On Availability Groups</span><span class="sxs-lookup"><span data-stu-id="39ee1-236">Existing deployments that do not use Always On Availability Groups</span></span>
> [!NOTE]
> <span data-ttu-id="39ee1-237">For existing deployments, first see the [Prerequisites](#prerequisites-for-premium-storage) section of this topic.</span><span class="sxs-lookup"><span data-stu-id="39ee1-237">For existing deployments, first see the [Prerequisites](#prerequisites-for-premium-storage) section of this topic.</span></span>
>
>

<span data-ttu-id="39ee1-238">There are different considerations for SQL Server deployments that do not use Always On Availability Groups and those that do.</span><span class="sxs-lookup"><span data-stu-id="39ee1-238">There are different considerations for SQL Server deployments that do not use Always On Availability Groups and those that do.</span></span> <span data-ttu-id="39ee1-239">If you are not using Always On and have an existing standalone SQL Server, you can upgrade to Premium Storage by using a new cloud service and storage account.</span><span class="sxs-lookup"><span data-stu-id="39ee1-239">If you are not using Always On and have an existing standalone SQL Server, you can upgrade to Premium Storage by using a new cloud service and storage account.</span></span> <span data-ttu-id="39ee1-240">Consider the following options:</span><span class="sxs-lookup"><span data-stu-id="39ee1-240">Consider the following options:</span></span>

* <span data-ttu-id="39ee1-241">**Create a new SQL Server VM**.</span><span class="sxs-lookup"><span data-stu-id="39ee1-241">**Create a new SQL Server VM**.</span></span> <span data-ttu-id="39ee1-242">You can create a new SQL Server VM that uses a Premium Storage account, as documented in New Deployments.</span><span class="sxs-lookup"><span data-stu-id="39ee1-242">You can create a new SQL Server VM that uses a Premium Storage account, as documented in New Deployments.</span></span> <span data-ttu-id="39ee1-243">Then backup and restore your SQL Server configuration and user databases.</span><span class="sxs-lookup"><span data-stu-id="39ee1-243">Then backup and restore your SQL Server configuration and user databases.</span></span> <span data-ttu-id="39ee1-244">The application will need to be updated to reference the new SQL Server if it is being accessed internally or externally.</span><span class="sxs-lookup"><span data-stu-id="39ee1-244">The application will need to be updated to reference the new SQL Server if it is being accessed internally or externally.</span></span> <span data-ttu-id="39ee1-245">You would need to copy all ‘out of db’ objects as if you were doing a Side by Side (SxS) SQL Server migration.</span><span class="sxs-lookup"><span data-stu-id="39ee1-245">You would need to copy all ‘out of db’ objects as if you were doing a Side by Side (SxS) SQL Server migration.</span></span> <span data-ttu-id="39ee1-246">This includes objects such as logins, certificates, and linked servers.</span><span class="sxs-lookup"><span data-stu-id="39ee1-246">This includes objects such as logins, certificates, and linked servers.</span></span>
* <span data-ttu-id="39ee1-247">**Migrate an existing SQL Server VM**.</span><span class="sxs-lookup"><span data-stu-id="39ee1-247">**Migrate an existing SQL Server VM**.</span></span> <span data-ttu-id="39ee1-248">This will require taking the SQL Server VM offline, then transferring it to a new cloud service, which includes copying all of its attached VHDs to the Premium Storage account.</span><span class="sxs-lookup"><span data-stu-id="39ee1-248">This will require taking the SQL Server VM offline, then transferring it to a new cloud service, which includes copying all of its attached VHDs to the Premium Storage account.</span></span> <span data-ttu-id="39ee1-249">When the VM comes online, the application will reference the server host name as before.</span><span class="sxs-lookup"><span data-stu-id="39ee1-249">When the VM comes online, the application will reference the server host name as before.</span></span> <span data-ttu-id="39ee1-250">Be aware that the size of the existing disk will affect the performance characteristics.</span><span class="sxs-lookup"><span data-stu-id="39ee1-250">Be aware that the size of the existing disk will affect the performance characteristics.</span></span> <span data-ttu-id="39ee1-251">For example, a 400 GB disk gets rounded up to a P20.</span><span class="sxs-lookup"><span data-stu-id="39ee1-251">For example, a 400 GB disk gets rounded up to a P20.</span></span> <span data-ttu-id="39ee1-252">If you know that you do not require that disk performance, then you could recreate the VM as a DS Series VM, and attach Premium Storage VHDs of the size/performance specification you require.</span><span class="sxs-lookup"><span data-stu-id="39ee1-252">If you know that you do not require that disk performance, then you could recreate the VM as a DS Series VM, and attach Premium Storage VHDs of the size/performance specification you require.</span></span> <span data-ttu-id="39ee1-253">Then you could detach and reattach the SQL DB files.</span><span class="sxs-lookup"><span data-stu-id="39ee1-253">Then you could detach and reattach the SQL DB files.</span></span>

> [!NOTE]
> <span data-ttu-id="39ee1-254">When copying the VHD disks you should be aware of the size, depending on the size will mean what Premium Storage Disk type they fall into, this determines disk performance specification.</span><span class="sxs-lookup"><span data-stu-id="39ee1-254">When copying the VHD disks you should be aware of the size, depending on the size will mean what Premium Storage Disk type they fall into, this determines disk performance specification.</span></span> <span data-ttu-id="39ee1-255">Azure will round up to the nearest disk size, so if you have a 400GB disk, this will be rounded up to a P20.</span><span class="sxs-lookup"><span data-stu-id="39ee1-255">Azure will round up to the nearest disk size, so if you have a 400GB disk, this will be rounded up to a P20.</span></span> <span data-ttu-id="39ee1-256">Depending on your existing IO requirements of the OS VHD, you might not need to migrate this to a Premium Storage account.</span><span class="sxs-lookup"><span data-stu-id="39ee1-256">Depending on your existing IO requirements of the OS VHD, you might not need to migrate this to a Premium Storage account.</span></span>
>
>

<span data-ttu-id="39ee1-257">If your SQL Server is accessed externally, then the cloud service VIP will change.</span><span class="sxs-lookup"><span data-stu-id="39ee1-257">If your SQL Server is accessed externally, then the cloud service VIP will change.</span></span> <span data-ttu-id="39ee1-258">You will also have to update end points, ACLs, and DNS settings.</span><span class="sxs-lookup"><span data-stu-id="39ee1-258">You will also have to update end points, ACLs, and DNS settings.</span></span>

## <a name="existing-deployments-that-use-always-on-availability-groups"></a><span data-ttu-id="39ee1-259">Existing deployments that use Always On Availability Groups</span><span class="sxs-lookup"><span data-stu-id="39ee1-259">Existing deployments that use Always On Availability Groups</span></span>
> [!NOTE]
> <span data-ttu-id="39ee1-260">For existing deployments, first see the [Prerequisites](#prerequisites-for-premium-storage) section of this topic.</span><span class="sxs-lookup"><span data-stu-id="39ee1-260">For existing deployments, first see the [Prerequisites](#prerequisites-for-premium-storage) section of this topic.</span></span>
>
>

<span data-ttu-id="39ee1-261">Initially in this section we will look at how Always On interacts with Azure Networking.</span><span class="sxs-lookup"><span data-stu-id="39ee1-261">Initially in this section we will look at how Always On interacts with Azure Networking.</span></span> <span data-ttu-id="39ee1-262">We will then break down migrations in to two scenarios: migrations where some downtime can be tolerated and migrations where you must achieve minimal downtime.</span><span class="sxs-lookup"><span data-stu-id="39ee1-262">We will then break down migrations in to two scenarios: migrations where some downtime can be tolerated and migrations where you must achieve minimal downtime.</span></span>

<span data-ttu-id="39ee1-263">On-premises SQL Server Always On Availability Groups use a Listener on-premises that registers a virtual DNS name along with an IP address that is shared between one or more SQL Servers.</span><span class="sxs-lookup"><span data-stu-id="39ee1-263">On-premises SQL Server Always On Availability Groups use a Listener on-premises that registers a virtual DNS name along with an IP address that is shared between one or more SQL Servers.</span></span> <span data-ttu-id="39ee1-264">When clients connect they are routed through the listener IP to the Primary SQL Server.</span><span class="sxs-lookup"><span data-stu-id="39ee1-264">When clients connect they are routed through the listener IP to the Primary SQL Server.</span></span> <span data-ttu-id="39ee1-265">This is the server that owns the Always On IP resource at that time.</span><span class="sxs-lookup"><span data-stu-id="39ee1-265">This is the server that owns the Always On IP resource at that time.</span></span>

![DeploymentsUseAlways On][6]

<span data-ttu-id="39ee1-267">In Microsoft Azure you can have only one IP address assigned to a NIC on the VM, so in order to achieve the same layer of abstraction as on-premises, Azure utilizes the IP address that is assigned to the Internal/External Load Balancers (ILB/ELB).</span><span class="sxs-lookup"><span data-stu-id="39ee1-267">In Microsoft Azure you can have only one IP address assigned to a NIC on the VM, so in order to achieve the same layer of abstraction as on-premises, Azure utilizes the IP address that is assigned to the Internal/External Load Balancers (ILB/ELB).</span></span> <span data-ttu-id="39ee1-268">The IP resource that is shared between the servers is set to the same IP as the ILB/ELB.</span><span class="sxs-lookup"><span data-stu-id="39ee1-268">The IP resource that is shared between the servers is set to the same IP as the ILB/ELB.</span></span> <span data-ttu-id="39ee1-269">This is published in the DNS, and client traffic is passed through the ILB/ELB to the Primary SQL Server replica.</span><span class="sxs-lookup"><span data-stu-id="39ee1-269">This is published in the DNS, and client traffic is passed through the ILB/ELB to the Primary SQL Server replica.</span></span> <span data-ttu-id="39ee1-270">The ILB/ELB knows which SQL Server is primary since it uses probes to probe the Always On IP resource.</span><span class="sxs-lookup"><span data-stu-id="39ee1-270">The ILB/ELB knows which SQL Server is primary since it uses probes to probe the Always On IP resource.</span></span> <span data-ttu-id="39ee1-271">In the previous example, it probes each node that has an endpoint referenced by the ELB/ILB, whichever responds is the Primary SQL Server.</span><span class="sxs-lookup"><span data-stu-id="39ee1-271">In the previous example, it probes each node that has an endpoint referenced by the ELB/ILB, whichever responds is the Primary SQL Server.</span></span>

> [!NOTE]
> <span data-ttu-id="39ee1-272">The ILB and ELB are both assigned to a particular Azure cloud service, therefore any cloud migration in Azure will most likely mean that the Load Balancer IP will change.</span><span class="sxs-lookup"><span data-stu-id="39ee1-272">The ILB and ELB are both assigned to a particular Azure cloud service, therefore any cloud migration in Azure will most likely mean that the Load Balancer IP will change.</span></span>
>
>

### <a name="migrating-always-on-deployments-that-can-allow-some-downtime"></a><span data-ttu-id="39ee1-273">Migrating Always On deployments that can allow some downtime</span><span class="sxs-lookup"><span data-stu-id="39ee1-273">Migrating Always On deployments that can allow some downtime</span></span>
<span data-ttu-id="39ee1-274">There are two strategies to migrate Always On deployments that allow for some downtime:</span><span class="sxs-lookup"><span data-stu-id="39ee1-274">There are two strategies to migrate Always On deployments that allow for some downtime:</span></span>

1. <span data-ttu-id="39ee1-275">**Add more secondary replicas to an existing Always On Cluster**</span><span class="sxs-lookup"><span data-stu-id="39ee1-275">**Add more secondary replicas to an existing Always On Cluster**</span></span>
2. <span data-ttu-id="39ee1-276">**Migrate to a new Always On Cluster**</span><span class="sxs-lookup"><span data-stu-id="39ee1-276">**Migrate to a new Always On Cluster**</span></span>

#### <a name="1-add-more-secondary-replicas-to-an-existing-always-on-cluster"></a><span data-ttu-id="39ee1-277">1. Add more Secondary Replicas to an Existing Always On Cluster</span><span class="sxs-lookup"><span data-stu-id="39ee1-277">1. Add more Secondary Replicas to an Existing Always On Cluster</span></span>
<span data-ttu-id="39ee1-278">One strategy is to add more secondaries to the Always On Availability Group.</span><span class="sxs-lookup"><span data-stu-id="39ee1-278">One strategy is to add more secondaries to the Always On Availability Group.</span></span> <span data-ttu-id="39ee1-279">You need to add these into a new cloud service and update the listener with the new load balancer IP.</span><span class="sxs-lookup"><span data-stu-id="39ee1-279">You need to add these into a new cloud service and update the listener with the new load balancer IP.</span></span>

##### <a name="points-of-downtime"></a><span data-ttu-id="39ee1-280">Points of downtime:</span><span class="sxs-lookup"><span data-stu-id="39ee1-280">Points of downtime:</span></span>
* <span data-ttu-id="39ee1-281">Cluster Validation.</span><span class="sxs-lookup"><span data-stu-id="39ee1-281">Cluster Validation.</span></span>
* <span data-ttu-id="39ee1-282">Testing Always On failovers for New Secondaries.</span><span class="sxs-lookup"><span data-stu-id="39ee1-282">Testing Always On failovers for New Secondaries.</span></span>

<span data-ttu-id="39ee1-283">If you are using Windows Storage Pools within the VM for higher IO throughput, then these will be taken offline during a Full Cluster Validation.</span><span class="sxs-lookup"><span data-stu-id="39ee1-283">If you are using Windows Storage Pools within the VM for higher IO throughput, then these will be taken offline during a Full Cluster Validation.</span></span> <span data-ttu-id="39ee1-284">The validation test is required when you add nodes to the cluster.</span><span class="sxs-lookup"><span data-stu-id="39ee1-284">The validation test is required when you add nodes to the cluster.</span></span> <span data-ttu-id="39ee1-285">The time it takes to run the test can vary, so you should test this in your representative test environment to get an approximate time of how long this will take.</span><span class="sxs-lookup"><span data-stu-id="39ee1-285">The time it takes to run the test can vary, so you should test this in your representative test environment to get an approximate time of how long this will take.</span></span>

<span data-ttu-id="39ee1-286">You should provision time where you can perform manual failover and chaos testing on the newly added nodes to ensure Always On High Availability functions as expected.</span><span class="sxs-lookup"><span data-stu-id="39ee1-286">You should provision time where you can perform manual failover and chaos testing on the newly added nodes to ensure Always On High Availability functions as expected.</span></span>

![DeploymentUseAlways On2][7]

> [!NOTE]
> <span data-ttu-id="39ee1-288">You should stop all instances of SQL Server where the Storage Pools are used before the Validation runs.</span><span class="sxs-lookup"><span data-stu-id="39ee1-288">You should stop all instances of SQL Server where the Storage Pools are used before the Validation runs.</span></span>
>
> ##### <a name="high-level-steps"></a><span data-ttu-id="39ee1-289">High-level steps</span><span class="sxs-lookup"><span data-stu-id="39ee1-289">High-level steps</span></span>
>

1. <span data-ttu-id="39ee1-290">Create two new SQL Servers in new cloud service with attached Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="39ee1-290">Create two new SQL Servers in new cloud service with attached Premium Storage.</span></span>
2. <span data-ttu-id="39ee1-291">Copy over FULL backups and restore with **NORECOVERY**.</span><span class="sxs-lookup"><span data-stu-id="39ee1-291">Copy over FULL backups and restore with **NORECOVERY**.</span></span>
3. <span data-ttu-id="39ee1-292">Copy over ‘out of user DB’ dependent objects, such as logins etc.</span><span class="sxs-lookup"><span data-stu-id="39ee1-292">Copy over ‘out of user DB’ dependent objects, such as logins etc.</span></span>
4. <span data-ttu-id="39ee1-293">Create new a new Internal Load Balancer (ILB) or use an External Load Balancer (ELB), and then set up Load Balanced Endpoints on both new nodes.</span><span class="sxs-lookup"><span data-stu-id="39ee1-293">Create new a new Internal Load Balancer (ILB) or use an External Load Balancer (ELB), and then set up Load Balanced Endpoints on both new nodes.</span></span>

   > [!NOTE]
   > <span data-ttu-id="39ee1-294">Check all Nodes have the correct Endpoint configuration before you continue</span><span class="sxs-lookup"><span data-stu-id="39ee1-294">Check all Nodes have the correct Endpoint configuration before you continue</span></span>
   >
   >
5. <span data-ttu-id="39ee1-295">Stop User/Application Access to the SQL Server (if using Storage Pools).</span><span class="sxs-lookup"><span data-stu-id="39ee1-295">Stop User/Application Access to the SQL Server (if using Storage Pools).</span></span>
6. <span data-ttu-id="39ee1-296">Stop SQL Server Engine Services on All Nodes (if using Storage Pools).</span><span class="sxs-lookup"><span data-stu-id="39ee1-296">Stop SQL Server Engine Services on All Nodes (if using Storage Pools).</span></span>
7. <span data-ttu-id="39ee1-297">Add new Nodes to cluster and run full validation.</span><span class="sxs-lookup"><span data-stu-id="39ee1-297">Add new Nodes to cluster and run full validation.</span></span>
8. <span data-ttu-id="39ee1-298">Once Validation is successful, start all SQL Server Services.</span><span class="sxs-lookup"><span data-stu-id="39ee1-298">Once Validation is successful, start all SQL Server Services.</span></span>
9. <span data-ttu-id="39ee1-299">Backup Transaction logs, and restore user databases.</span><span class="sxs-lookup"><span data-stu-id="39ee1-299">Backup Transaction logs, and restore user databases.</span></span>
10. <span data-ttu-id="39ee1-300">Add new nodes into the Always On Availability Group and place replication into **Synchronous**.</span><span class="sxs-lookup"><span data-stu-id="39ee1-300">Add new nodes into the Always On Availability Group and place replication into **Synchronous**.</span></span>
11. <span data-ttu-id="39ee1-301">Add the IP address resource of the new Cloud Service ILB/ELB through PowerShell for Always On based on the Multi-site example in the [Appendix](#appendix-migrating-a-multisite-alwayson-cluster-to-premium-storage).</span><span class="sxs-lookup"><span data-stu-id="39ee1-301">Add the IP address resource of the new Cloud Service ILB/ELB through PowerShell for Always On based on the Multi-site example in the [Appendix](#appendix-migrating-a-multisite-alwayson-cluster-to-premium-storage).</span></span> <span data-ttu-id="39ee1-302">In Windows clustering, set the **Possible owners** of the **IP Address** resource to the new nodes old.</span><span class="sxs-lookup"><span data-stu-id="39ee1-302">In Windows clustering, set the **Possible owners** of the **IP Address** resource to the new nodes old.</span></span> <span data-ttu-id="39ee1-303">See the ‘Adding IP Address Resource on Same Subnet’ section of the [Appendix](#appendix-migrating-a-multisite-alwayson-cluster-to-premium-storage).</span><span class="sxs-lookup"><span data-stu-id="39ee1-303">See the ‘Adding IP Address Resource on Same Subnet’ section of the [Appendix](#appendix-migrating-a-multisite-alwayson-cluster-to-premium-storage).</span></span>
12. <span data-ttu-id="39ee1-304">Failover to one of the new nodes.</span><span class="sxs-lookup"><span data-stu-id="39ee1-304">Failover to one of the new nodes.</span></span>
13. <span data-ttu-id="39ee1-305">Make the new nodes Auto Failover Partners and test failovers.</span><span class="sxs-lookup"><span data-stu-id="39ee1-305">Make the new nodes Auto Failover Partners and test failovers.</span></span>
14. <span data-ttu-id="39ee1-306">Remove original nodes from Availability Group.</span><span class="sxs-lookup"><span data-stu-id="39ee1-306">Remove original nodes from Availability Group.</span></span>

##### <a name="advantages"></a><span data-ttu-id="39ee1-307">Advantages</span><span class="sxs-lookup"><span data-stu-id="39ee1-307">Advantages</span></span>
* <span data-ttu-id="39ee1-308">New SQL Servers can be tested (SQL Server and Application) before they are added to Always On.</span><span class="sxs-lookup"><span data-stu-id="39ee1-308">New SQL Servers can be tested (SQL Server and Application) before they are added to Always On.</span></span>
* <span data-ttu-id="39ee1-309">You can change the VM size and customize the storage to your exact requirements.</span><span class="sxs-lookup"><span data-stu-id="39ee1-309">You can change the VM size and customize the storage to your exact requirements.</span></span> <span data-ttu-id="39ee1-310">However, it would be beneficial to keep all the SQL file paths the same.</span><span class="sxs-lookup"><span data-stu-id="39ee1-310">However, it would be beneficial to keep all the SQL file paths the same.</span></span>
* <span data-ttu-id="39ee1-311">You can control when the transfer of the DB backups to the Secondary Replicas are started.</span><span class="sxs-lookup"><span data-stu-id="39ee1-311">You can control when the transfer of the DB backups to the Secondary Replicas are started.</span></span> <span data-ttu-id="39ee1-312">This differs from using Azure **Start-AzureStorageBlobCopy** commandlet to copy VHDs, because that is an asynchronous copy.</span><span class="sxs-lookup"><span data-stu-id="39ee1-312">This differs from using Azure **Start-AzureStorageBlobCopy** commandlet to copy VHDs, because that is an asynchronous copy.</span></span>

##### <a name="disadvantages"></a><span data-ttu-id="39ee1-313">Disadvantages</span><span class="sxs-lookup"><span data-stu-id="39ee1-313">Disadvantages</span></span>
* <span data-ttu-id="39ee1-314">When using Windows Storage Pools, there is Cluster downtime during the Full Cluster Validation for the new additional nodes.</span><span class="sxs-lookup"><span data-stu-id="39ee1-314">When using Windows Storage Pools, there is Cluster downtime during the Full Cluster Validation for the new additional nodes.</span></span>
* <span data-ttu-id="39ee1-315">Depending on the SQL Server Version and the existing number of secondary replicas, you might not be able to add more secondary replicas without removing existing secondaries.</span><span class="sxs-lookup"><span data-stu-id="39ee1-315">Depending on the SQL Server Version and the existing number of secondary replicas, you might not be able to add more secondary replicas without removing existing secondaries.</span></span>
* <span data-ttu-id="39ee1-316">There could be long SQL data transfer time while setting up the secondaries.</span><span class="sxs-lookup"><span data-stu-id="39ee1-316">There could be long SQL data transfer time while setting up the secondaries.</span></span>
* <span data-ttu-id="39ee1-317">There is additional cost during migration while you have new machines running in parallel.</span><span class="sxs-lookup"><span data-stu-id="39ee1-317">There is additional cost during migration while you have new machines running in parallel.</span></span>

#### <a name="2-migrate-to-a-new-always-on-cluster"></a><span data-ttu-id="39ee1-318">2. Migrate to a new Always On Cluster</span><span class="sxs-lookup"><span data-stu-id="39ee1-318">2. Migrate to a new Always On Cluster</span></span>
<span data-ttu-id="39ee1-319">Another strategy is to create a brand new Always On Cluster with brand new nodes in new cloud service and then redirect the clients to use it.</span><span class="sxs-lookup"><span data-stu-id="39ee1-319">Another strategy is to create a brand new Always On Cluster with brand new nodes in new cloud service and then redirect the clients to use it.</span></span>

##### <a name="points-of-downtime"></a><span data-ttu-id="39ee1-320">Points of downtime</span><span class="sxs-lookup"><span data-stu-id="39ee1-320">Points of downtime</span></span>
<span data-ttu-id="39ee1-321">There is downtime when you transfer applications and users to the new Always On listener.</span><span class="sxs-lookup"><span data-stu-id="39ee1-321">There is downtime when you transfer applications and users to the new Always On listener.</span></span> <span data-ttu-id="39ee1-322">The downtime depends on:</span><span class="sxs-lookup"><span data-stu-id="39ee1-322">The downtime depends on:</span></span>

* <span data-ttu-id="39ee1-323">The time taken to restore final transaction log backups to databases on new servers.</span><span class="sxs-lookup"><span data-stu-id="39ee1-323">The time taken to restore final transaction log backups to databases on new servers.</span></span>
* <span data-ttu-id="39ee1-324">The time taken to update client applications to use new Always On listener.</span><span class="sxs-lookup"><span data-stu-id="39ee1-324">The time taken to update client applications to use new Always On listener.</span></span>

##### <a name="advantages"></a><span data-ttu-id="39ee1-325">Advantages</span><span class="sxs-lookup"><span data-stu-id="39ee1-325">Advantages</span></span>
* <span data-ttu-id="39ee1-326">You can test the actual production environment, SQL Server, and OS build changes.</span><span class="sxs-lookup"><span data-stu-id="39ee1-326">You can test the actual production environment, SQL Server, and OS build changes.</span></span>
* <span data-ttu-id="39ee1-327">You have the option to customize the storage and to potentially reduce size of VM.</span><span class="sxs-lookup"><span data-stu-id="39ee1-327">You have the option to customize the storage and to potentially reduce size of VM.</span></span> <span data-ttu-id="39ee1-328">This could result in cost reduction.</span><span class="sxs-lookup"><span data-stu-id="39ee1-328">This could result in cost reduction.</span></span>
* <span data-ttu-id="39ee1-329">You can update your SQL Server build or version during this process.</span><span class="sxs-lookup"><span data-stu-id="39ee1-329">You can update your SQL Server build or version during this process.</span></span> <span data-ttu-id="39ee1-330">You can also upgrade the Operating System.</span><span class="sxs-lookup"><span data-stu-id="39ee1-330">You can also upgrade the Operating System.</span></span>
* <span data-ttu-id="39ee1-331">The previous Always On Cluster can act as a solid rollback target.</span><span class="sxs-lookup"><span data-stu-id="39ee1-331">The previous Always On Cluster can act as a solid rollback target.</span></span>

##### <a name="disadvantages"></a><span data-ttu-id="39ee1-332">Disadvantages</span><span class="sxs-lookup"><span data-stu-id="39ee1-332">Disadvantages</span></span>
* <span data-ttu-id="39ee1-333">You need to change the DNS name of the listener if you want both Always On clusters running simultaneously.</span><span class="sxs-lookup"><span data-stu-id="39ee1-333">You need to change the DNS name of the listener if you want both Always On clusters running simultaneously.</span></span> <span data-ttu-id="39ee1-334">This adds administration overhead during the migration as client application strings must reflect the new Listener name.</span><span class="sxs-lookup"><span data-stu-id="39ee1-334">This adds administration overhead during the migration as client application strings must reflect the new Listener name.</span></span>
* <span data-ttu-id="39ee1-335">You must implement a synchronization mechanism between the two environments to keep them as close as possible to minimize the final synchronization requirements before migration.</span><span class="sxs-lookup"><span data-stu-id="39ee1-335">You must implement a synchronization mechanism between the two environments to keep them as close as possible to minimize the final synchronization requirements before migration.</span></span>
* <span data-ttu-id="39ee1-336">There is added cost during migration while you have the new environment running.</span><span class="sxs-lookup"><span data-stu-id="39ee1-336">There is added cost during migration while you have the new environment running.</span></span>

### <a name="migrating-always-on-deployments-for-minimal-downtime"></a><span data-ttu-id="39ee1-337">Migrating Always On Deployments for minimal downtime</span><span class="sxs-lookup"><span data-stu-id="39ee1-337">Migrating Always On Deployments for minimal downtime</span></span>
<span data-ttu-id="39ee1-338">There are two strategies for migrating Always On deployments for minimal downtime:</span><span class="sxs-lookup"><span data-stu-id="39ee1-338">There are two strategies for migrating Always On deployments for minimal downtime:</span></span>

1. <span data-ttu-id="39ee1-339">**Utilize an Existing Secondary: Single-Site**</span><span class="sxs-lookup"><span data-stu-id="39ee1-339">**Utilize an Existing Secondary: Single-Site**</span></span>
2. <span data-ttu-id="39ee1-340">**Utilize Existing Secondary Replica(s): Multi-Site**</span><span class="sxs-lookup"><span data-stu-id="39ee1-340">**Utilize Existing Secondary Replica(s): Multi-Site**</span></span>

#### <a name="1-utilize-an-existing-secondary-single-site"></a><span data-ttu-id="39ee1-341">1. Utilize an existing secondary: Single-Site</span><span class="sxs-lookup"><span data-stu-id="39ee1-341">1. Utilize an existing secondary: Single-Site</span></span>
<span data-ttu-id="39ee1-342">One strategy for minimal downtime is to take an existing cloud secondary and remove it from the current cloud service.</span><span class="sxs-lookup"><span data-stu-id="39ee1-342">One strategy for minimal downtime is to take an existing cloud secondary and remove it from the current cloud service.</span></span> <span data-ttu-id="39ee1-343">Then copy the VHDs to the new Premium Storage account, and create the VM in the new cloud service.</span><span class="sxs-lookup"><span data-stu-id="39ee1-343">Then copy the VHDs to the new Premium Storage account, and create the VM in the new cloud service.</span></span> <span data-ttu-id="39ee1-344">Then update the listener in clustering and failover.</span><span class="sxs-lookup"><span data-stu-id="39ee1-344">Then update the listener in clustering and failover.</span></span>

##### <a name="points-of-downtime"></a><span data-ttu-id="39ee1-345">Points of downtime</span><span class="sxs-lookup"><span data-stu-id="39ee1-345">Points of downtime</span></span>
* <span data-ttu-id="39ee1-346">There is downtime when you update the final node with the Load Balanced endpoint.</span><span class="sxs-lookup"><span data-stu-id="39ee1-346">There is downtime when you update the final node with the Load Balanced endpoint.</span></span>
* <span data-ttu-id="39ee1-347">Your client reconnection might be delayed depending on your client/DNS configuration.</span><span class="sxs-lookup"><span data-stu-id="39ee1-347">Your client reconnection might be delayed depending on your client/DNS configuration.</span></span>
* <span data-ttu-id="39ee1-348">There is additional downtime if you choose to take the Always On Cluster group offline to swap out the IP addresses.</span><span class="sxs-lookup"><span data-stu-id="39ee1-348">There is additional downtime if you choose to take the Always On Cluster group offline to swap out the IP addresses.</span></span> <span data-ttu-id="39ee1-349">You can avoid this by using an OR dependency and Possible Owners for the added IP Address resource.</span><span class="sxs-lookup"><span data-stu-id="39ee1-349">You can avoid this by using an OR dependency and Possible Owners for the added IP Address resource.</span></span> <span data-ttu-id="39ee1-350">See the ‘Adding IP Address Resource on Same Subnet’ section of the [Appendix](#appendix-migrating-a-multisite-alwayson-cluster-to-premium-storage).</span><span class="sxs-lookup"><span data-stu-id="39ee1-350">See the ‘Adding IP Address Resource on Same Subnet’ section of the [Appendix](#appendix-migrating-a-multisite-alwayson-cluster-to-premium-storage).</span></span>

> [!NOTE]
> <span data-ttu-id="39ee1-351">When you want the added node to partake in as an Always On Failover Partner, you need to add an Azure Endpoint with a reference to the Load Balanced Set.</span><span class="sxs-lookup"><span data-stu-id="39ee1-351">When you want the added node to partake in as an Always On Failover Partner, you need to add an Azure Endpoint with a reference to the Load Balanced Set.</span></span> <span data-ttu-id="39ee1-352">When you run the **Add-AzureEndpoint** command to do this, current connections to remain open, but new connections to the listener will not be able to be established until the load balancer has updated.</span><span class="sxs-lookup"><span data-stu-id="39ee1-352">When you run the **Add-AzureEndpoint** command to do this, current connections to remain open, but new connections to the listener will not be able to be established until the load balancer has updated.</span></span> <span data-ttu-id="39ee1-353">In testing this was seen to last 90-120seconds, this should be tested.</span><span class="sxs-lookup"><span data-stu-id="39ee1-353">In testing this was seen to last 90-120seconds, this should be tested.</span></span>
>
>

##### <a name="advantages"></a><span data-ttu-id="39ee1-354">Advantages</span><span class="sxs-lookup"><span data-stu-id="39ee1-354">Advantages</span></span>
* <span data-ttu-id="39ee1-355">No extra cost incurred during migration.</span><span class="sxs-lookup"><span data-stu-id="39ee1-355">No extra cost incurred during migration.</span></span>
* <span data-ttu-id="39ee1-356">A one-to-one migration.</span><span class="sxs-lookup"><span data-stu-id="39ee1-356">A one-to-one migration.</span></span>
* <span data-ttu-id="39ee1-357">Reduced complexity.</span><span class="sxs-lookup"><span data-stu-id="39ee1-357">Reduced complexity.</span></span>
* <span data-ttu-id="39ee1-358">Allows for increased IOPS from Premium Storage SKUs.</span><span class="sxs-lookup"><span data-stu-id="39ee1-358">Allows for increased IOPS from Premium Storage SKUs.</span></span> <span data-ttu-id="39ee1-359">When the disks are detached from the VM and copied to the new cloud service, a 3rd party tool can be used to increase the VHD size, which provides higher throughputs.</span><span class="sxs-lookup"><span data-stu-id="39ee1-359">When the disks are detached from the VM and copied to the new cloud service, a 3rd party tool can be used to increase the VHD size, which provides higher throughputs.</span></span> <span data-ttu-id="39ee1-360">For increasing VHD sizes, see this [forum discussion](https://social.msdn.microsoft.com/Forums/azure/4a9bcc9e-e5bf-4125-9994-7c154c9b0d52/resizing-azure-data-disk?forum=WAVirtualMachinesforWindows).</span><span class="sxs-lookup"><span data-stu-id="39ee1-360">For increasing VHD sizes, see this [forum discussion](https://social.msdn.microsoft.com/Forums/azure/4a9bcc9e-e5bf-4125-9994-7c154c9b0d52/resizing-azure-data-disk?forum=WAVirtualMachinesforWindows).</span></span>

##### <a name="disadvantages"></a><span data-ttu-id="39ee1-361">Disadvantages</span><span class="sxs-lookup"><span data-stu-id="39ee1-361">Disadvantages</span></span>
* <span data-ttu-id="39ee1-362">There is a temporary loss of HA and DR during migration.</span><span class="sxs-lookup"><span data-stu-id="39ee1-362">There is a temporary loss of HA and DR during migration.</span></span>
* <span data-ttu-id="39ee1-363">As this is a 1:1 migration, you will have to use a minimum VM size that will support your number of VHDs, so you might not be able to downsize your VMs.</span><span class="sxs-lookup"><span data-stu-id="39ee1-363">As this is a 1:1 migration, you will have to use a minimum VM size that will support your number of VHDs, so you might not be able to downsize your VMs.</span></span>
* <span data-ttu-id="39ee1-364">This scenario would use the Azure **Start-AzureStorageBlobCopy** commandlet, which is asynchronous.</span><span class="sxs-lookup"><span data-stu-id="39ee1-364">This scenario would use the Azure **Start-AzureStorageBlobCopy** commandlet, which is asynchronous.</span></span> <span data-ttu-id="39ee1-365">There is no SLA on copy completion.</span><span class="sxs-lookup"><span data-stu-id="39ee1-365">There is no SLA on copy completion.</span></span> <span data-ttu-id="39ee1-366">The time of the copies varies, while this depends on wait in queue it will also depend on the amount of data to transfer.</span><span class="sxs-lookup"><span data-stu-id="39ee1-366">The time of the copies varies, while this depends on wait in queue it will also depend on the amount of data to transfer.</span></span> <span data-ttu-id="39ee1-367">The copy time increases if the transfer is going to another Azure data center that supports Premium Storage in another region.</span><span class="sxs-lookup"><span data-stu-id="39ee1-367">The copy time increases if the transfer is going to another Azure data center that supports Premium Storage in another region.</span></span> <span data-ttu-id="39ee1-368">If you just have 2 nodes, consider a possible mitigation in case the copy takes longer than in testing.</span><span class="sxs-lookup"><span data-stu-id="39ee1-368">If you just have 2 nodes, consider a possible mitigation in case the copy takes longer than in testing.</span></span> <span data-ttu-id="39ee1-369">This could include the following ideas.</span><span class="sxs-lookup"><span data-stu-id="39ee1-369">This could include the following ideas.</span></span>
  * <span data-ttu-id="39ee1-370">Add a temporary 3rd SQL Server node for HA before the migration with agreed downtime.</span><span class="sxs-lookup"><span data-stu-id="39ee1-370">Add a temporary 3rd SQL Server node for HA before the migration with agreed downtime.</span></span>
  * <span data-ttu-id="39ee1-371">Run the migration outside of Azure scheduled maintenance.</span><span class="sxs-lookup"><span data-stu-id="39ee1-371">Run the migration outside of Azure scheduled maintenance.</span></span>
  * <span data-ttu-id="39ee1-372">Ensure you have configured your cluster quorum correctly.</span><span class="sxs-lookup"><span data-stu-id="39ee1-372">Ensure you have configured your cluster quorum correctly.</span></span>  

##### <a name="high-level-steps"></a><span data-ttu-id="39ee1-373">High-level steps</span><span class="sxs-lookup"><span data-stu-id="39ee1-373">High-level steps</span></span>
<span data-ttu-id="39ee1-374">This document does not demonstrate a complete end to end example, however the [Appendix](#appendix-migrating-a-multisite-alwayson-cluster-to-premium-storage) provides details that can be leveraged to perform this.</span><span class="sxs-lookup"><span data-stu-id="39ee1-374">This document does not demonstrate a complete end to end example, however the [Appendix](#appendix-migrating-a-multisite-alwayson-cluster-to-premium-storage) provides details that can be leveraged to perform this.</span></span>

![MinimalDowntime][8]

* <span data-ttu-id="39ee1-376">Gather disk configuration, and remove the node (do not delete attached VHDs).</span><span class="sxs-lookup"><span data-stu-id="39ee1-376">Gather disk configuration, and remove the node (do not delete attached VHDs).</span></span>
* <span data-ttu-id="39ee1-377">Create a Premium Storage account and copy VHDs from the Standard Storage account</span><span class="sxs-lookup"><span data-stu-id="39ee1-377">Create a Premium Storage account and copy VHDs from the Standard Storage account</span></span>
* <span data-ttu-id="39ee1-378">Create new cloud service and redeploy the SQL2 VM in that cloud service.</span><span class="sxs-lookup"><span data-stu-id="39ee1-378">Create new cloud service and redeploy the SQL2 VM in that cloud service.</span></span> <span data-ttu-id="39ee1-379">Create the VM using the copied original OS VHD and attaching the copied VHDs.</span><span class="sxs-lookup"><span data-stu-id="39ee1-379">Create the VM using the copied original OS VHD and attaching the copied VHDs.</span></span>
* <span data-ttu-id="39ee1-380">Configure ILB / ELB and add Endpoints.</span><span class="sxs-lookup"><span data-stu-id="39ee1-380">Configure ILB / ELB and add Endpoints.</span></span>
* <span data-ttu-id="39ee1-381">Update Listener by either:</span><span class="sxs-lookup"><span data-stu-id="39ee1-381">Update Listener by either:</span></span>
  * <span data-ttu-id="39ee1-382">Taking the Always On Group offline and updating the Always On Listener with new ILB / ELB IP address.</span><span class="sxs-lookup"><span data-stu-id="39ee1-382">Taking the Always On Group offline and updating the Always On Listener with new ILB / ELB IP address.</span></span>
  * <span data-ttu-id="39ee1-383">Or adding the IP address resource of new Cloud Service ILB/ELB through PowerShell into Windows clustering.</span><span class="sxs-lookup"><span data-stu-id="39ee1-383">Or adding the IP address resource of new Cloud Service ILB/ELB through PowerShell into Windows clustering.</span></span> <span data-ttu-id="39ee1-384">Then set the Possible owners of the IP Address resource to the migrated node, SQL2, and set this as OR dependency in the Network Name.</span><span class="sxs-lookup"><span data-stu-id="39ee1-384">Then set the Possible owners of the IP Address resource to the migrated node, SQL2, and set this as OR dependency in the Network Name.</span></span> <span data-ttu-id="39ee1-385">See the ‘Adding IP Address Resource on Same Subnet’ section of the [Appendix](#appendix-migrating-a-multisite-alwayson-cluster-to-premium-storage).</span><span class="sxs-lookup"><span data-stu-id="39ee1-385">See the ‘Adding IP Address Resource on Same Subnet’ section of the [Appendix](#appendix-migrating-a-multisite-alwayson-cluster-to-premium-storage).</span></span>
* <span data-ttu-id="39ee1-386">Check DNS configuration/propogation to the clients.</span><span class="sxs-lookup"><span data-stu-id="39ee1-386">Check DNS configuration/propogation to the clients.</span></span>
* <span data-ttu-id="39ee1-387">Migrate SQL1 VM, and go through steps 2 – 4.</span><span class="sxs-lookup"><span data-stu-id="39ee1-387">Migrate SQL1 VM, and go through steps 2 – 4.</span></span>
* <span data-ttu-id="39ee1-388">If using steps 5ii, then add SQL1 as a Possible Owner for the added IP Address Resource</span><span class="sxs-lookup"><span data-stu-id="39ee1-388">If using steps 5ii, then add SQL1 as a Possible Owner for the added IP Address Resource</span></span>
* <span data-ttu-id="39ee1-389">Test failovers.</span><span class="sxs-lookup"><span data-stu-id="39ee1-389">Test failovers.</span></span>

#### <a name="2-utilize-existing-secondary-replicas-multi-site"></a><span data-ttu-id="39ee1-390">2. Utilize existing secondary replica(s): Multi-Site</span><span class="sxs-lookup"><span data-stu-id="39ee1-390">2. Utilize existing secondary replica(s): Multi-Site</span></span>
<span data-ttu-id="39ee1-391">If you have nodes in more than one Azure datacenter (DC) or if you have a hybrid environment, then you can use an Always On configuration in this environment to minimize downtime.</span><span class="sxs-lookup"><span data-stu-id="39ee1-391">If you have nodes in more than one Azure datacenter (DC) or if you have a hybrid environment, then you can use an Always On configuration in this environment to minimize downtime.</span></span>

<span data-ttu-id="39ee1-392">The approach is to change the Always On synchronization to Synchronous for the on-premises or secondary Azure DC, and then failover over to that SQL Server.</span><span class="sxs-lookup"><span data-stu-id="39ee1-392">The approach is to change the Always On synchronization to Synchronous for the on-premises or secondary Azure DC, and then failover over to that SQL Server.</span></span> <span data-ttu-id="39ee1-393">Then copy the VHDs to a Premium Storage account, and redeploy the machine into a new cloud service.</span><span class="sxs-lookup"><span data-stu-id="39ee1-393">Then copy the VHDs to a Premium Storage account, and redeploy the machine into a new cloud service.</span></span> <span data-ttu-id="39ee1-394">Update the listener, and then fail back.</span><span class="sxs-lookup"><span data-stu-id="39ee1-394">Update the listener, and then fail back.</span></span>

##### <a name="points-of-downtime"></a><span data-ttu-id="39ee1-395">Points of downtime</span><span class="sxs-lookup"><span data-stu-id="39ee1-395">Points of downtime</span></span>
<span data-ttu-id="39ee1-396">The downtime consists of the time to failover to the alternative DC and back.</span><span class="sxs-lookup"><span data-stu-id="39ee1-396">The downtime consists of the time to failover to the alternative DC and back.</span></span> <span data-ttu-id="39ee1-397">It also depends on your client/DNS configuration and your client reconnection may be delayed.</span><span class="sxs-lookup"><span data-stu-id="39ee1-397">It also depends on your client/DNS configuration and your client reconnection may be delayed.</span></span>
<span data-ttu-id="39ee1-398">Consider the following example of a hybrid Always On configuration:</span><span class="sxs-lookup"><span data-stu-id="39ee1-398">Consider the following example of a hybrid Always On configuration:</span></span>

![MultiSite1][9]

##### <a name="advantages"></a><span data-ttu-id="39ee1-400">Advantages</span><span class="sxs-lookup"><span data-stu-id="39ee1-400">Advantages</span></span>
* <span data-ttu-id="39ee1-401">You can utilize existing infrastructure.</span><span class="sxs-lookup"><span data-stu-id="39ee1-401">You can utilize existing infrastructure.</span></span>
* <span data-ttu-id="39ee1-402">You have the option to pre-upgrade the Azure storage on the DR Azure DC first.</span><span class="sxs-lookup"><span data-stu-id="39ee1-402">You have the option to pre-upgrade the Azure storage on the DR Azure DC first.</span></span>
* <span data-ttu-id="39ee1-403">The DR Azure DC storage can be reconfigured.</span><span class="sxs-lookup"><span data-stu-id="39ee1-403">The DR Azure DC storage can be reconfigured.</span></span>
* <span data-ttu-id="39ee1-404">There is a minimum of two failovers during migration, excluding test failovers.</span><span class="sxs-lookup"><span data-stu-id="39ee1-404">There is a minimum of two failovers during migration, excluding test failovers.</span></span>
* <span data-ttu-id="39ee1-405">You do not need to move SQL Server data with backup and restore.</span><span class="sxs-lookup"><span data-stu-id="39ee1-405">You do not need to move SQL Server data with backup and restore.</span></span>

##### <a name="disadvantages"></a><span data-ttu-id="39ee1-406">Disadvantages</span><span class="sxs-lookup"><span data-stu-id="39ee1-406">Disadvantages</span></span>
* <span data-ttu-id="39ee1-407">Depending on client access to SQL Server, there might be increased latency when SQL Server is running in an alternative DC to the application.</span><span class="sxs-lookup"><span data-stu-id="39ee1-407">Depending on client access to SQL Server, there might be increased latency when SQL Server is running in an alternative DC to the application.</span></span>
* <span data-ttu-id="39ee1-408">The copy time of VHDs to Premium storage could be long.</span><span class="sxs-lookup"><span data-stu-id="39ee1-408">The copy time of VHDs to Premium storage could be long.</span></span> <span data-ttu-id="39ee1-409">This might affect your decision on whether to keep the node in the Availability Group.</span><span class="sxs-lookup"><span data-stu-id="39ee1-409">This might affect your decision on whether to keep the node in the Availability Group.</span></span> <span data-ttu-id="39ee1-410">Consider this for when log intensive work loads are running during the migration is required, since the Primary node will have to keep the unreplicated transactions in its transaction log.</span><span class="sxs-lookup"><span data-stu-id="39ee1-410">Consider this for when log intensive work loads are running during the migration is required, since the Primary node will have to keep the unreplicated transactions in its transaction log.</span></span> <span data-ttu-id="39ee1-411">Therefore this could grow significantly.</span><span class="sxs-lookup"><span data-stu-id="39ee1-411">Therefore this could grow significantly.</span></span>
* <span data-ttu-id="39ee1-412">This scenario would use the Azure **Start-AzureStorageBlobCopy** commandlet, which is asynchronous.</span><span class="sxs-lookup"><span data-stu-id="39ee1-412">This scenario would use the Azure **Start-AzureStorageBlobCopy** commandlet, which is asynchronous.</span></span> <span data-ttu-id="39ee1-413">There is no SLA on completion.</span><span class="sxs-lookup"><span data-stu-id="39ee1-413">There is no SLA on completion.</span></span> <span data-ttu-id="39ee1-414">The time of the copies varies, while this depends on wait in queue, it will also depend on the amount of data to transfer.</span><span class="sxs-lookup"><span data-stu-id="39ee1-414">The time of the copies varies, while this depends on wait in queue, it will also depend on the amount of data to transfer.</span></span> <span data-ttu-id="39ee1-415">Therefore you just have one node in your 2nd data center, you should take mitigation steps in case the copy takes longer than in testing.</span><span class="sxs-lookup"><span data-stu-id="39ee1-415">Therefore you just have one node in your 2nd data center, you should take mitigation steps in case the copy takes longer than in testing.</span></span> <span data-ttu-id="39ee1-416">This could include the following ideas.</span><span class="sxs-lookup"><span data-stu-id="39ee1-416">This could include the following ideas.</span></span>
  * <span data-ttu-id="39ee1-417">Add a temporary 2nd SQL node for HA before the migration with agreed downtime.</span><span class="sxs-lookup"><span data-stu-id="39ee1-417">Add a temporary 2nd SQL node for HA before the migration with agreed downtime.</span></span>
  * <span data-ttu-id="39ee1-418">Run the migration outside of Azure scheduled maintenance.</span><span class="sxs-lookup"><span data-stu-id="39ee1-418">Run the migration outside of Azure scheduled maintenance.</span></span>
  * <span data-ttu-id="39ee1-419">Ensure you have configured your cluster quorum correctly.</span><span class="sxs-lookup"><span data-stu-id="39ee1-419">Ensure you have configured your cluster quorum correctly.</span></span>

<span data-ttu-id="39ee1-420">This scenario assumes that you have documented your install and know how the storage is mapped in order to make changes for optimal disk cache settings.</span><span class="sxs-lookup"><span data-stu-id="39ee1-420">This scenario assumes that you have documented your install and know how the storage is mapped in order to make changes for optimal disk cache settings.</span></span>

##### <a name="high-level-steps"></a><span data-ttu-id="39ee1-421">High-level steps</span><span class="sxs-lookup"><span data-stu-id="39ee1-421">High-level steps</span></span>
![Multisite2][10]

* <span data-ttu-id="39ee1-423">Make the on-premises / alternate Azure DC the SQL Server Primary, and make it the other Auto Failover Partner (AFP).</span><span class="sxs-lookup"><span data-stu-id="39ee1-423">Make the on-premises / alternate Azure DC the SQL Server Primary, and make it the other Auto Failover Partner (AFP).</span></span>
* <span data-ttu-id="39ee1-424">Gather disk configuration information from SQL2, and remove the node (do not delete attached VHDs).</span><span class="sxs-lookup"><span data-stu-id="39ee1-424">Gather disk configuration information from SQL2, and remove the node (do not delete attached VHDs).</span></span>
* <span data-ttu-id="39ee1-425">Create a Premium Storage account and copy VHDs from the Standard Storage account.</span><span class="sxs-lookup"><span data-stu-id="39ee1-425">Create a Premium Storage account and copy VHDs from the Standard Storage account.</span></span>
* <span data-ttu-id="39ee1-426">Create a new cloud service and create the SQL2 VM with its Premiums Storage disks attached.</span><span class="sxs-lookup"><span data-stu-id="39ee1-426">Create a new cloud service and create the SQL2 VM with its Premiums Storage disks attached.</span></span>
* <span data-ttu-id="39ee1-427">Configure ILB / ELB and add Endpoints.</span><span class="sxs-lookup"><span data-stu-id="39ee1-427">Configure ILB / ELB and add Endpoints.</span></span>
* <span data-ttu-id="39ee1-428">Update the Always On Listener with new ILB / ELB IP address and test failover.</span><span class="sxs-lookup"><span data-stu-id="39ee1-428">Update the Always On Listener with new ILB / ELB IP address and test failover.</span></span>
* <span data-ttu-id="39ee1-429">Check the DNS configuration.</span><span class="sxs-lookup"><span data-stu-id="39ee1-429">Check the DNS configuration.</span></span>
* <span data-ttu-id="39ee1-430">Change the AFP to SQL2, and then migrate SQL1 and go through steps 2 – 5.</span><span class="sxs-lookup"><span data-stu-id="39ee1-430">Change the AFP to SQL2, and then migrate SQL1 and go through steps 2 – 5.</span></span>
* <span data-ttu-id="39ee1-431">Test failovers.</span><span class="sxs-lookup"><span data-stu-id="39ee1-431">Test failovers.</span></span>
* <span data-ttu-id="39ee1-432">Switch the AFP back to SQL1 and SQL2</span><span class="sxs-lookup"><span data-stu-id="39ee1-432">Switch the AFP back to SQL1 and SQL2</span></span>

## <a name="appendix-migrating-a-multisite-always-on-cluster-to-premium-storage"></a><span data-ttu-id="39ee1-433">Appendix: Migrating a Multisite Always On Cluster to Premium Storage</span><span class="sxs-lookup"><span data-stu-id="39ee1-433">Appendix: Migrating a Multisite Always On Cluster to Premium Storage</span></span>
<span data-ttu-id="39ee1-434">The remainder of this topic provides a detailed example of converting a multi-site Always On cluster to Premium storage.</span><span class="sxs-lookup"><span data-stu-id="39ee1-434">The remainder of this topic provides a detailed example of converting a multi-site Always On cluster to Premium storage.</span></span> <span data-ttu-id="39ee1-435">It also converts the Listener from using an external load balancer (ELB) to an internal load balancer (ILB).</span><span class="sxs-lookup"><span data-stu-id="39ee1-435">It also converts the Listener from using an external load balancer (ELB) to an internal load balancer (ILB).</span></span>

### <a name="environment"></a><span data-ttu-id="39ee1-436">Environment</span><span class="sxs-lookup"><span data-stu-id="39ee1-436">Environment</span></span>
* <span data-ttu-id="39ee1-437">Windows 2k12 / SQL 2k12</span><span class="sxs-lookup"><span data-stu-id="39ee1-437">Windows 2k12 / SQL 2k12</span></span>
* <span data-ttu-id="39ee1-438">1 DB Files on SP</span><span class="sxs-lookup"><span data-stu-id="39ee1-438">1 DB Files on SP</span></span>
* <span data-ttu-id="39ee1-439">2 x Storage Pools per Node</span><span class="sxs-lookup"><span data-stu-id="39ee1-439">2 x Storage Pools per Node</span></span>

![Appendix1][11]

### <a name="vm"></a><span data-ttu-id="39ee1-441">VM:</span><span class="sxs-lookup"><span data-stu-id="39ee1-441">VM:</span></span>
<span data-ttu-id="39ee1-442">In this example we are going to demonstrate moving from an ELB to ILB.</span><span class="sxs-lookup"><span data-stu-id="39ee1-442">In this example we are going to demonstrate moving from an ELB to ILB.</span></span> <span data-ttu-id="39ee1-443">ELB was available before ILB, so this shows how to switch to this during the migration.</span><span class="sxs-lookup"><span data-stu-id="39ee1-443">ELB was available before ILB, so this shows how to switch to this during the migration.</span></span>

![Appendix2][12]

### <a name="pre-steps-connect-to-subscription"></a><span data-ttu-id="39ee1-445">Pre Steps: Connect to Subscription</span><span class="sxs-lookup"><span data-stu-id="39ee1-445">Pre Steps: Connect to Subscription</span></span>
    Add-AzureAccount

    #Set up subscription
    Get-AzureSubscription

#### <a name="step-1-create-new-storage-account-and-cloud-service"></a><span data-ttu-id="39ee1-446">Step 1: Create New Storage Account and Cloud Service</span><span class="sxs-lookup"><span data-stu-id="39ee1-446">Step 1: Create New Storage Account and Cloud Service</span></span>
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

#### <a name="step-2-increase-the-permitted-failures-on-resources-optional"></a><span data-ttu-id="39ee1-447">Step 2: Increase the permitted failures on resources <Optional></span><span class="sxs-lookup"><span data-stu-id="39ee1-447">Step 2: Increase the permitted failures on resources <Optional></span></span>
<span data-ttu-id="39ee1-448">On certain resources that belong to your Always On Availability Group there are limits on how many failures that can occur in a period, where the cluster service will attempt to restart the resource group.</span><span class="sxs-lookup"><span data-stu-id="39ee1-448">On certain resources that belong to your Always On Availability Group there are limits on how many failures that can occur in a period, where the cluster service will attempt to restart the resource group.</span></span> <span data-ttu-id="39ee1-449">It is recommended you increase this whilst you are walking through this procedure, since if you don’t manually failover and trigger failovers by shutting down machines you can get close to this limit.</span><span class="sxs-lookup"><span data-stu-id="39ee1-449">It is recommended you increase this whilst you are walking through this procedure, since if you don’t manually failover and trigger failovers by shutting down machines you can get close to this limit.</span></span>

<span data-ttu-id="39ee1-450">It would be prudent to double the failure allowance, to do this in Failover Cluster Manager, go to the Properties of the Always On resource group:</span><span class="sxs-lookup"><span data-stu-id="39ee1-450">It would be prudent to double the failure allowance, to do this in Failover Cluster Manager, go to the Properties of the Always On resource group:</span></span>

![Appendix3][13]

<span data-ttu-id="39ee1-452">Change the Maximum Failures to 6.</span><span class="sxs-lookup"><span data-stu-id="39ee1-452">Change the Maximum Failures to 6.</span></span>

#### <a name="step-3-addition-ip-address-resource-for-cluster-group-optional"></a><span data-ttu-id="39ee1-453">Step 3: Addition IP Address resource for Cluster Group <Optional></span><span class="sxs-lookup"><span data-stu-id="39ee1-453">Step 3: Addition IP Address resource for Cluster Group <Optional></span></span>
<span data-ttu-id="39ee1-454">If you have only one IP address for the Cluster Group and this is aligned to the cloud subnet, beware, if you accidentally take offline all cluster nodes in the cloud on that network then the Cluster IP resource and Cluster Network Name will not be able to come online.</span><span class="sxs-lookup"><span data-stu-id="39ee1-454">If you have only one IP address for the Cluster Group and this is aligned to the cloud subnet, beware, if you accidentally take offline all cluster nodes in the cloud on that network then the Cluster IP resource and Cluster Network Name will not be able to come online.</span></span> <span data-ttu-id="39ee1-455">In the event of this it will prevent updates to other cluster resources.</span><span class="sxs-lookup"><span data-stu-id="39ee1-455">In the event of this it will prevent updates to other cluster resources.</span></span>

#### <a name="step-4-dns-configuration"></a><span data-ttu-id="39ee1-456">Step 4: DNS configuration</span><span class="sxs-lookup"><span data-stu-id="39ee1-456">Step 4: DNS configuration</span></span>
<span data-ttu-id="39ee1-457">To implement a smooth transition depends on how DNS is being utilized and updated.</span><span class="sxs-lookup"><span data-stu-id="39ee1-457">To implement a smooth transition depends on how DNS is being utilized and updated.</span></span>
<span data-ttu-id="39ee1-458">When Always On is installed, it creates a Windows Cluster Resource group, if you open Failover Cluster Manager, you will see that at a minimum it will have three resources, the two that the document refers to are:</span><span class="sxs-lookup"><span data-stu-id="39ee1-458">When Always On is installed, it creates a Windows Cluster Resource group, if you open Failover Cluster Manager, you will see that at a minimum it will have three resources, the two that the document refers to are:</span></span>

* <span data-ttu-id="39ee1-459">Virtual Network Name (VNN) – This is the DNS name that client connect to when wanting to connect to SQL Servers via Always On.</span><span class="sxs-lookup"><span data-stu-id="39ee1-459">Virtual Network Name (VNN) – This is the DNS name that client connect to when wanting to connect to SQL Servers via Always On.</span></span>
* <span data-ttu-id="39ee1-460">IP Address Resource – This is the IP address that associated with the VNN, you can have more than one, and in a multisite configuration you will have an IP address per site/subnet.</span><span class="sxs-lookup"><span data-stu-id="39ee1-460">IP Address Resource – This is the IP address that associated with the VNN, you can have more than one, and in a multisite configuration you will have an IP address per site/subnet.</span></span>

<span data-ttu-id="39ee1-461">When connecting to SQL Server, the SQL Server Client driver will retrieve the DNS records associated with the listener and try to connect to each Always On associated IP address, below we discuss some factors that can influence this.</span><span class="sxs-lookup"><span data-stu-id="39ee1-461">When connecting to SQL Server, the SQL Server Client driver will retrieve the DNS records associated with the listener and try to connect to each Always On associated IP address, below we discuss some factors that can influence this.</span></span>

<span data-ttu-id="39ee1-462">The number of concurrent DNS records that are associated with the listener name depends not only on the number of IP addresses associated, but the ‘RegisterAllIpProviders’setting in Failover Clustering for the Always ON VNN resource.</span><span class="sxs-lookup"><span data-stu-id="39ee1-462">The number of concurrent DNS records that are associated with the listener name depends not only on the number of IP addresses associated, but the ‘RegisterAllIpProviders’setting in Failover Clustering for the Always ON VNN resource.</span></span>

<span data-ttu-id="39ee1-463">When you deploy Always On in Azure there are different steps to create the Listener and IP Addresses, you have to manually configure the ‘RegisterAllIpProviders’ to 1, this is different to an on premise Always On deployment where it is already set to 1.</span><span class="sxs-lookup"><span data-stu-id="39ee1-463">When you deploy Always On in Azure there are different steps to create the Listener and IP Addresses, you have to manually configure the ‘RegisterAllIpProviders’ to 1, this is different to an on premise Always On deployment where it is already set to 1.</span></span>

<span data-ttu-id="39ee1-464">If ‘RegisterAllIpProviders’ is 0, then you will only see one DNS record in DNS associated with the Listener:</span><span class="sxs-lookup"><span data-stu-id="39ee1-464">If ‘RegisterAllIpProviders’ is 0, then you will only see one DNS record in DNS associated with the Listener:</span></span>

![Appendix4][14]

<span data-ttu-id="39ee1-466">If ‘RegisterAllIpProviders’ is 1:</span><span class="sxs-lookup"><span data-stu-id="39ee1-466">If ‘RegisterAllIpProviders’ is 1:</span></span>

![Appendix5][15]

<span data-ttu-id="39ee1-468">The code below will dump out the VNN settings and set it for you, please note, for the change to take effect you will need to take the VNN offline and turn it back online, this taking the Listener offline causing client connectivity disruption.</span><span class="sxs-lookup"><span data-stu-id="39ee1-468">The code below will dump out the VNN settings and set it for you, please note, for the change to take effect you will need to take the VNN offline and turn it back online, this taking the Listener offline causing client connectivity disruption.</span></span>

    ##Always On Listener Name
    $ListenerName = "Mylistener"
    ##Get AlwaysOn Network Name Settings
    Get-ClusterResource $ListenerName| Get-ClusterParameter
    ##Set RegisterAllProvidersIP
    Get-ClusterResource $ListenerName| Set-ClusterParameter RegisterAllProvidersIP  1

<span data-ttu-id="39ee1-469">In a later migration step you will need to update the Always On listener with an updated IP address that will reference a load balancer, this will involve an IP Address resource removal and addition.</span><span class="sxs-lookup"><span data-stu-id="39ee1-469">In a later migration step you will need to update the Always On listener with an updated IP address that will reference a load balancer, this will involve an IP Address resource removal and addition.</span></span> <span data-ttu-id="39ee1-470">After the IP update, you need to ensure the new IP address has been updated in DNS Zone and that the clients are updating their local DNS cache.</span><span class="sxs-lookup"><span data-stu-id="39ee1-470">After the IP update, you need to ensure the new IP address has been updated in DNS Zone and that the clients are updating their local DNS cache.</span></span>

<span data-ttu-id="39ee1-471">If your clients reside in a different network segment and reference a different DNS server, you need to consider what happens about DNS Zone Transfer during the migration, as the application reconnect time will be constrained by at least the Zone Transfer Time of any new IP addresses for the listener.</span><span class="sxs-lookup"><span data-stu-id="39ee1-471">If your clients reside in a different network segment and reference a different DNS server, you need to consider what happens about DNS Zone Transfer during the migration, as the application reconnect time will be constrained by at least the Zone Transfer Time of any new IP addresses for the listener.</span></span> <span data-ttu-id="39ee1-472">If you are under time constraint here, you should discuss and test forcing an incremental zone transfer with your Windows teams, and also put the DNS host record to a lower Time To Live (TTL), so the clients update.</span><span class="sxs-lookup"><span data-stu-id="39ee1-472">If you are under time constraint here, you should discuss and test forcing an incremental zone transfer with your Windows teams, and also put the DNS host record to a lower Time To Live (TTL), so the clients update.</span></span> <span data-ttu-id="39ee1-473">For more information, see [Incremental Zone Transfers](https://technet.microsoft.com/library/cc958973.aspx) and [Start-DnsServerZoneTransfer](https://technet.microsoft.com/library/jj649917.aspx).</span><span class="sxs-lookup"><span data-stu-id="39ee1-473">For more information, see [Incremental Zone Transfers](https://technet.microsoft.com/library/cc958973.aspx) and [Start-DnsServerZoneTransfer](https://technet.microsoft.com/library/jj649917.aspx).</span></span>

<span data-ttu-id="39ee1-474">By default the TTL for DNS Record that is associated with the Listener in Always On in Azure is 1200 seconds.</span><span class="sxs-lookup"><span data-stu-id="39ee1-474">By default the TTL for DNS Record that is associated with the Listener in Always On in Azure is 1200 seconds.</span></span> <span data-ttu-id="39ee1-475">You may wish to reduce this if you are under time constraint during your migration to ensure the clients update their DNS with the updated IP address for the listener.</span><span class="sxs-lookup"><span data-stu-id="39ee1-475">You may wish to reduce this if you are under time constraint during your migration to ensure the clients update their DNS with the updated IP address for the listener.</span></span> <span data-ttu-id="39ee1-476">You can see and modify the configuration by dumping out the configuration of the VNN:</span><span class="sxs-lookup"><span data-stu-id="39ee1-476">You can see and modify the configuration by dumping out the configuration of the VNN:</span></span>

    $AGName = "myProductionAG"
    $ListenerName = "Mylistener"
    #Look at HostRecordTTL
    Get-ClusterResource $ListenerName| Get-ClusterParameter

    #Set HostRecordTTL Examples
    Get-ClusterResource $ListenerName| Set-ClusterParameter -Name "HostRecordTTL" 120

<span data-ttu-id="39ee1-477">Please note, the lower the ‘HostRecordTTL’, a higher amount of DNS traffic will occur.</span><span class="sxs-lookup"><span data-stu-id="39ee1-477">Please note, the lower the ‘HostRecordTTL’, a higher amount of DNS traffic will occur.</span></span>

##### <a name="client-application-settings"></a><span data-ttu-id="39ee1-478">Client application settings</span><span class="sxs-lookup"><span data-stu-id="39ee1-478">Client application settings</span></span>
<span data-ttu-id="39ee1-479">If your SQL client application supports the .Net 4.5 SQLClient, then you can use ‘MULTISUBNETFAILOVER=TRUE’ keyword, this is recommended to be applied as it allows for faster connection to SQL Always On Availability Group during failover.</span><span class="sxs-lookup"><span data-stu-id="39ee1-479">If your SQL client application supports the .Net 4.5 SQLClient, then you can use ‘MULTISUBNETFAILOVER=TRUE’ keyword, this is recommended to be applied as it allows for faster connection to SQL Always On Availability Group during failover.</span></span> <span data-ttu-id="39ee1-480">It enumerates through all IP addresses associated with the Always On listener in parallel, and performs a more aggressive TCP connection retry speed during a failover.</span><span class="sxs-lookup"><span data-stu-id="39ee1-480">It enumerates through all IP addresses associated with the Always On listener in parallel, and performs a more aggressive TCP connection retry speed during a failover.</span></span>

<span data-ttu-id="39ee1-481">For more information regarding the settings above, please see [MultiSubnetFailover Keyword and Associated Features](https://msdn.microsoft.com/library/hh213080.aspx#MultiSubnetFailover).</span><span class="sxs-lookup"><span data-stu-id="39ee1-481">For more information regarding the settings above, please see [MultiSubnetFailover Keyword and Associated Features](https://msdn.microsoft.com/library/hh213080.aspx#MultiSubnetFailover).</span></span> <span data-ttu-id="39ee1-482">Also see [SqlClient Support for High Availability, Disaster Recovery](https://msdn.microsoft.com/library/hh205662\(v=vs.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="39ee1-482">Also see [SqlClient Support for High Availability, Disaster Recovery](https://msdn.microsoft.com/library/hh205662\(v=vs.110\).aspx).</span></span>

#### <a name="step-5-cluster-quorum-settings"></a><span data-ttu-id="39ee1-483">Step 5: Cluster quorum settings</span><span class="sxs-lookup"><span data-stu-id="39ee1-483">Step 5: Cluster quorum settings</span></span>
<span data-ttu-id="39ee1-484">As you are going to be taking out at least one SQL Server down at a time, you should modify the cluster quorum setting, if using File Share Witness (FSW) with 2 nodes, you should set the quorum to allow node majority and utilize dynamic voting, and this is to allow for a single node to remain standing.</span><span class="sxs-lookup"><span data-stu-id="39ee1-484">As you are going to be taking out at least one SQL Server down at a time, you should modify the cluster quorum setting, if using File Share Witness (FSW) with 2 nodes, you should set the quorum to allow node majority and utilize dynamic voting, and this is to allow for a single node to remain standing.</span></span>

    Set-ClusterQuorum -NodeMajority  

<span data-ttu-id="39ee1-485">For more information on managing and configuring the cluster quorum, please see [Configure and Manage the Quorum in a Windows Server 2012 Failover Cluster](https://technet.microsoft.com/library/jj612870.aspx).</span><span class="sxs-lookup"><span data-stu-id="39ee1-485">For more information on managing and configuring the cluster quorum, please see [Configure and Manage the Quorum in a Windows Server 2012 Failover Cluster](https://technet.microsoft.com/library/jj612870.aspx).</span></span>

#### <a name="step-6-extract-existing-endpoints-and-acls"></a><span data-ttu-id="39ee1-486">Step 6: Extract Existing Endpoints and ACLs</span><span class="sxs-lookup"><span data-stu-id="39ee1-486">Step 6: Extract Existing Endpoints and ACLs</span></span>
    #GET Endpoint info
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmNameToMigrate | Get-AzureEndpoint
    #GET ACL Rules for Each EP, this example is for the Always On Endpoint
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmNameToMigrate | Get-AzureAclConfig -EndpointName "myAOEndPoint-LB"  

<span data-ttu-id="39ee1-487">Save these to a text file.</span><span class="sxs-lookup"><span data-stu-id="39ee1-487">Save these to a text file.</span></span>

#### <a name="step-7-change-failover-partners-and-replication-modes"></a><span data-ttu-id="39ee1-488">Step 7: Change Failover Partners and Replication Modes</span><span class="sxs-lookup"><span data-stu-id="39ee1-488">Step 7: Change Failover Partners and Replication Modes</span></span>
<span data-ttu-id="39ee1-489">If you have more than 2 SQL Servers, you should change the failover of another secondary in another DC or on premise to ‘Synchronous’ and make it an Automatic Failover Partner (AFP), this is so you maintain HA whilst you are making changes.</span><span class="sxs-lookup"><span data-stu-id="39ee1-489">If you have more than 2 SQL Servers, you should change the failover of another secondary in another DC or on premise to ‘Synchronous’ and make it an Automatic Failover Partner (AFP), this is so you maintain HA whilst you are making changes.</span></span> <span data-ttu-id="39ee1-490">You can do this through TSQL of modify though SSMS:</span><span class="sxs-lookup"><span data-stu-id="39ee1-490">You can do this through TSQL of modify though SSMS:</span></span>

![Appendix6][16]

#### <a name="step-8-remove-secondary-vm-from-cloud-service"></a><span data-ttu-id="39ee1-492">Step 8: Remove Secondary VM from cloud service</span><span class="sxs-lookup"><span data-stu-id="39ee1-492">Step 8: Remove Secondary VM from cloud service</span></span>
<span data-ttu-id="39ee1-493">You should be planning to migrate a cloud secondary node first, if this is currently primary, you should initiate a manual failover.</span><span class="sxs-lookup"><span data-stu-id="39ee1-493">You should be planning to migrate a cloud secondary node first, if this is currently primary, you should initiate a manual failover.</span></span>

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

#### <a name="step-9-change-disk-caching-settings-in-csv-file-and-save"></a><span data-ttu-id="39ee1-494">Step 9: Change disk caching settings in CSV file and save</span><span class="sxs-lookup"><span data-stu-id="39ee1-494">Step 9: Change disk caching settings in CSV file and save</span></span>
<span data-ttu-id="39ee1-495">For data volumes these should be set to READONLY.</span><span class="sxs-lookup"><span data-stu-id="39ee1-495">For data volumes these should be set to READONLY.</span></span>

<span data-ttu-id="39ee1-496">For TLOG volumes these should be set to NONE.</span><span class="sxs-lookup"><span data-stu-id="39ee1-496">For TLOG volumes these should be set to NONE.</span></span>

![Appendix7][17]

#### <a name="step-10-copy-vhds"></a><span data-ttu-id="39ee1-498">Step 10: Copy VHDS</span><span class="sxs-lookup"><span data-stu-id="39ee1-498">Step 10: Copy VHDS</span></span>
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



<span data-ttu-id="39ee1-499">You can check the copy status of the VHDs to the Premium Storage account:</span><span class="sxs-lookup"><span data-stu-id="39ee1-499">You can check the copy status of the VHDs to the Premium Storage account:</span></span>

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

<span data-ttu-id="39ee1-501">Wait until all these are recorded as success.</span><span class="sxs-lookup"><span data-stu-id="39ee1-501">Wait until all these are recorded as success.</span></span>

<span data-ttu-id="39ee1-502">For information for individual blobs:</span><span class="sxs-lookup"><span data-stu-id="39ee1-502">For information for individual blobs:</span></span>

    Get-AzureStorageBlobCopyState -Blob "blobname.vhd" -Container $containerName -Context $xioContext

#### <a name="step-11-register-os-disk"></a><span data-ttu-id="39ee1-503">Step 11: Register OS disk</span><span class="sxs-lookup"><span data-stu-id="39ee1-503">Step 11: Register OS disk</span></span>
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

#### <a name="step-12-import-secondary-into-new-cloud-service"></a><span data-ttu-id="39ee1-504">Step 12: Import secondary into new cloud service</span><span class="sxs-lookup"><span data-stu-id="39ee1-504">Step 12: Import secondary into new cloud service</span></span>
<span data-ttu-id="39ee1-505">The code below also uses the added option here you can import the machine and use the retainable VIP.</span><span class="sxs-lookup"><span data-stu-id="39ee1-505">The code below also uses the added option here you can import the machine and use the retainable VIP.</span></span>

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

#### <a name="step-13-create-ilb-on-new-cloud-svc-add-load-balanced-endpoints-and-acls"></a><span data-ttu-id="39ee1-506">Step 13: Create ILB on New Cloud Svc, Add Load Balanced Endpoints and ACLs</span><span class="sxs-lookup"><span data-stu-id="39ee1-506">Step 13: Create ILB on New Cloud Svc, Add Load Balanced Endpoints and ACLs</span></span>
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

#### <a name="step-14-update-always-on"></a><span data-ttu-id="39ee1-507">Step 14: Update Always On</span><span class="sxs-lookup"><span data-stu-id="39ee1-507">Step 14: Update Always On</span></span>
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

<span data-ttu-id="39ee1-509">Now remove the old cloud service IP Address.</span><span class="sxs-lookup"><span data-stu-id="39ee1-509">Now remove the old cloud service IP Address.</span></span>

![Appendix10][20]

#### <a name="step-15-dns-update-check"></a><span data-ttu-id="39ee1-511">Step 15: DNS update check</span><span class="sxs-lookup"><span data-stu-id="39ee1-511">Step 15: DNS update check</span></span>
<span data-ttu-id="39ee1-512">You should now check DNS Servers on your SQL Server client networks and make sure that clustering has added the extra host record for the added IP address.</span><span class="sxs-lookup"><span data-stu-id="39ee1-512">You should now check DNS Servers on your SQL Server client networks and make sure that clustering has added the extra host record for the added IP address.</span></span> <span data-ttu-id="39ee1-513">If those DNS servers have not updated, consider forcing a DNS Zone transfer and ensure that the clients in there subnet are able to resolve to both Always On IP Addresses, this is so you do not need to wait for automatic DNS replication.</span><span class="sxs-lookup"><span data-stu-id="39ee1-513">If those DNS servers have not updated, consider forcing a DNS Zone transfer and ensure that the clients in there subnet are able to resolve to both Always On IP Addresses, this is so you do not need to wait for automatic DNS replication.</span></span>

#### <a name="step-16-reconfigure-always-on"></a><span data-ttu-id="39ee1-514">Step 16: Reconfigure Always On</span><span class="sxs-lookup"><span data-stu-id="39ee1-514">Step 16: Reconfigure Always On</span></span>
<span data-ttu-id="39ee1-515">At this point you wait for the secondary that node that was migrated to fully resynchronize with the on-premise node and switch to synchronous replication node and make it the AFP.</span><span class="sxs-lookup"><span data-stu-id="39ee1-515">At this point you wait for the secondary that node that was migrated to fully resynchronize with the on-premise node and switch to synchronous replication node and make it the AFP.</span></span>  

#### <a name="step-17-migrate-second-node"></a><span data-ttu-id="39ee1-516">Step 17: Migrate second node</span><span class="sxs-lookup"><span data-stu-id="39ee1-516">Step 17: Migrate second node</span></span>
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

#### <a name="step-18-change-disk-caching-settings-in-csv-file-and-save"></a><span data-ttu-id="39ee1-517">Step 18: Change disk caching settings in CSV file and save</span><span class="sxs-lookup"><span data-stu-id="39ee1-517">Step 18: Change disk caching settings in CSV file and save</span></span>
<span data-ttu-id="39ee1-518">For data volumes these should be set to READONLY.</span><span class="sxs-lookup"><span data-stu-id="39ee1-518">For data volumes these should be set to READONLY.</span></span>

<span data-ttu-id="39ee1-519">For TLOG volumes these should be set to NONE.</span><span class="sxs-lookup"><span data-stu-id="39ee1-519">For TLOG volumes these should be set to NONE.</span></span>

![Appendix11][21]

#### <a name="step-19-create-new-independent-storage-account-for-secondary-node"></a><span data-ttu-id="39ee1-521">Step 19: Create New Independent Storage Account for Secondary Node</span><span class="sxs-lookup"><span data-stu-id="39ee1-521">Step 19: Create New Independent Storage Account for Secondary Node</span></span>
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

#### <a name="step-20-copy-vhds"></a><span data-ttu-id="39ee1-522">Step 20: Copy VHDS</span><span class="sxs-lookup"><span data-stu-id="39ee1-522">Step 20: Copy VHDS</span></span>
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


<span data-ttu-id="39ee1-523">You can check the VHD copy status for all VHDs: ForEach ($disk in $diskobjects) { $lun = $disk.Lun $vhdname = $disk.vhdname $cacheoption = $disk.HostCaching $disklabel = $disk.DiskLabel $diskName = $disk.DiskName</span><span class="sxs-lookup"><span data-stu-id="39ee1-523">You can check the VHD copy status for all VHDs: ForEach ($disk in $diskobjects) { $lun = $disk.Lun $vhdname = $disk.vhdname $cacheoption = $disk.HostCaching $disklabel = $disk.DiskLabel $diskName = $disk.DiskName</span></span>

       $copystate = Get-AzureStorageBlobCopyState -Blob $vhdname -Container $containerName -Context $xioContextnode2
    Write-Host "Copying Disk Lun $lun, Label : $disklabel, VHD : $vhdname, STATUS = " $copystate.Status
       }

![Appendix12][22]

<span data-ttu-id="39ee1-525">Wait until all these are recorded as success.</span><span class="sxs-lookup"><span data-stu-id="39ee1-525">Wait until all these are recorded as success.</span></span>

<span data-ttu-id="39ee1-526">For information for individual blobs:</span><span class="sxs-lookup"><span data-stu-id="39ee1-526">For information for individual blobs:</span></span>

    #Check induvidual blob status
    Get-AzureStorageBlobCopyState -Blob "danRegSvcAms-dansqlams1-2014-07-03.vhd" -Container $containerName -Context $xioContextnode2

#### <a name="step-21-register-os-disk"></a><span data-ttu-id="39ee1-527">Step 21: Register OS disk</span><span class="sxs-lookup"><span data-stu-id="39ee1-527">Step 21: Register OS disk</span></span>
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

#### <a name="step-22-add-load-balanced-endpoints-and-acls"></a><span data-ttu-id="39ee1-528">Step 22: Add Load Balanced Endpoints and ACLs</span><span class="sxs-lookup"><span data-stu-id="39ee1-528">Step 22: Add Load Balanced Endpoints and ACLs</span></span>
    #Endpoints
    $epname="sqlIntEP"
    $prot="tcp"
    $locport=1433
    $pubport=1433
    Get-AzureVM –ServiceName $destcloudsvc –Name $vmNameToMigrate  | Add-AzureEndpoint -Name $epname -Protocol $prot -LocalPort $locport -PublicPort $pubport -ProbePort 59999 -ProbeIntervalInSeconds 5 -ProbeTimeoutInSeconds 11  -ProbeProtocol "TCP" -InternalLoadBalancerName $ilb -LBSetName $ilb -DirectServerReturn $true | Update-AzureVM


    #STOP!!! CHECK in the Azure classic portal or Machine Endpoints through powershell that these Endpoints are created!

    #SET ACLs or Azure Network Security Groups & Windows FWs

    #http://msdn.microsoft.com/library/azure/dn495192.aspx

#### <a name="step-23-test-failover"></a><span data-ttu-id="39ee1-529">Step 23: Test failover</span><span class="sxs-lookup"><span data-stu-id="39ee1-529">Step 23: Test failover</span></span>
<span data-ttu-id="39ee1-530">You should now let the migrated node synchronize with the on-premise Always On node, place it in to synchronous replication mode and wait until it is synchronized.</span><span class="sxs-lookup"><span data-stu-id="39ee1-530">You should now let the migrated node synchronize with the on-premise Always On node, place it in to synchronous replication mode and wait until it is synchronized.</span></span> <span data-ttu-id="39ee1-531">Then failover from on-prem to the first node migrated, which is the AFP.</span><span class="sxs-lookup"><span data-stu-id="39ee1-531">Then failover from on-prem to the first node migrated, which is the AFP.</span></span> <span data-ttu-id="39ee1-532">Once that has worked, change the last migrated node to the AFP.</span><span class="sxs-lookup"><span data-stu-id="39ee1-532">Once that has worked, change the last migrated node to the AFP.</span></span>

<span data-ttu-id="39ee1-533">You should test failovers between all nodes and run though chaos tests to ensure failovers work as expected and in a timely manor.</span><span class="sxs-lookup"><span data-stu-id="39ee1-533">You should test failovers between all nodes and run though chaos tests to ensure failovers work as expected and in a timely manor.</span></span>

#### <a name="step-24-put-back-cluster-quorum-settings--dns-ttl--failover-pntrs--sync-settings"></a><span data-ttu-id="39ee1-534">Step 24: Put back cluster quorum settings / DNS TTL / Failover Pntrs / Sync Settings</span><span class="sxs-lookup"><span data-stu-id="39ee1-534">Step 24: Put back cluster quorum settings / DNS TTL / Failover Pntrs / Sync Settings</span></span>
##### <a name="adding-ip-address-resource-on-same-subnet"></a><span data-ttu-id="39ee1-535">Adding IP Address Resource on Same Subnet</span><span class="sxs-lookup"><span data-stu-id="39ee1-535">Adding IP Address Resource on Same Subnet</span></span>
<span data-ttu-id="39ee1-536">If you have only 2 SQL Servers and want to migrate them to a new cloud service, but want to keep them on the same subnet, you can avoid taking the listener offline to delete the original Always On IP Address and add the New IP Address.</span><span class="sxs-lookup"><span data-stu-id="39ee1-536">If you have only 2 SQL Servers and want to migrate them to a new cloud service, but want to keep them on the same subnet, you can avoid taking the listener offline to delete the original Always On IP Address and add the New IP Address.</span></span> <span data-ttu-id="39ee1-537">If you are migrating the VMs to another subnet you will not need to do this as there will be an additional cluster network that will reference that subnet.</span><span class="sxs-lookup"><span data-stu-id="39ee1-537">If you are migrating the VMs to another subnet you will not need to do this as there will be an additional cluster network that will reference that subnet.</span></span>

<span data-ttu-id="39ee1-538">Once you have brought up the migrated secondary and added in the new IP Address resource for the new cloud service before failover the existing Primary, you should take these steps within the Cluster Failover Manager:</span><span class="sxs-lookup"><span data-stu-id="39ee1-538">Once you have brought up the migrated secondary and added in the new IP Address resource for the new cloud service before failover the existing Primary, you should take these steps within the Cluster Failover Manager:</span></span>

<span data-ttu-id="39ee1-539">To add in IP Address, see the [Appendix](#appendix-migrating-a-multisite-alwayson-cluster-to-premium-storage), step 14.</span><span class="sxs-lookup"><span data-stu-id="39ee1-539">To add in IP Address, see the [Appendix](#appendix-migrating-a-multisite-alwayson-cluster-to-premium-storage), step 14.</span></span>

1. <span data-ttu-id="39ee1-540">For the current IP Address resource, change the possible owner to ‘Existing Primary SQL Server’, in the example below, ‘dansqlams4’:</span><span class="sxs-lookup"><span data-stu-id="39ee1-540">For the current IP Address resource, change the possible owner to ‘Existing Primary SQL Server’, in the example below, ‘dansqlams4’:</span></span>

    ![Appendix13][23]
2. <span data-ttu-id="39ee1-542">For the new IP Address resource, change the possible owner to ‘Migrated secondary SQL Server’, in the example below, ‘dansqlams5’:</span><span class="sxs-lookup"><span data-stu-id="39ee1-542">For the new IP Address resource, change the possible owner to ‘Migrated secondary SQL Server’, in the example below, ‘dansqlams5’:</span></span>

    ![Appendix14][24]
3. <span data-ttu-id="39ee1-544">Once this is set you can failover, and when the last node is migrated the Possible Owners should be edited so that node is added as a Possible Owner:</span><span class="sxs-lookup"><span data-stu-id="39ee1-544">Once this is set you can failover, and when the last node is migrated the Possible Owners should be edited so that node is added as a Possible Owner:</span></span>

    ![Appendix15][25]

## <a name="additional-resources"></a><span data-ttu-id="39ee1-546">Additional resources</span><span class="sxs-lookup"><span data-stu-id="39ee1-546">Additional resources</span></span>
* [<span data-ttu-id="39ee1-547">Azure Premium Storage</span><span class="sxs-lookup"><span data-stu-id="39ee1-547">Azure Premium Storage</span></span>](../../../storage/storage-premium-storage.md)
* [<span data-ttu-id="39ee1-548">Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="39ee1-548">Virtual Machines</span></span>](https://azure.microsoft.com/services/virtual-machines/)
* [<span data-ttu-id="39ee1-549">SQL Server in Azure Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="39ee1-549">SQL Server in Azure Virtual Machines</span></span>](../sql/virtual-machines-windows-sql-server-iaas-overview.md)

<!-- IMAGES -->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sqlclassic/media/virtual-machines-windows-classic-sql-server-premium-storage/1_VNET_Portal.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sqlclassic/media/virtual-machines-windows-classic-sql-server-premium-storage/2_Diskname_Lun.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sqlclassic/media/virtual-machines-windows-classic-sql-server-premium-storage/3_Virtual_Disk_Properties.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sqlclassic/media/virtual-machines-windows-classic-sql-server-premium-storage/4_Virtual_Disk_Properties_Details.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sqlclassic/media/virtual-machines-windows-classic-sql-server-premium-storage/5_Get_Storage_Pool.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sqlclassic/media/virtual-machines-windows-classic-sql-server-premium-storage/6_Deployments_Always_On.png
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sqlclassic/media/virtual-machines-windows-classic-sql-server-premium-storage/7_Add_More_Secondaries.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sqlclassic/media/virtual-machines-windows-classic-sql-server-premium-storage/8_Use_Existing_Secondary_Single_Site.png
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sqlclassic/media/virtual-machines-windows-classic-sql-server-premium-storage/9_Use_Existing_Secondary_Multi_Site.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sqlclassic/media/virtual-machines-windows-classic-sql-server-premium-storage/9_Use_Existing_Secondary_Multi_Site_b.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sqlclassic/media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_01.png
[12]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sqlclassic/media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_02.png
[13]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sqlclassic/media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_03.png
[14]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sqlclassic/media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_04.png
[15]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sqlclassic/media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_05.png
[16]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sqlclassic/media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_06.png
[17]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sqlclassic/media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_07.png
[18]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sqlclassic/media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_08.png
[19]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sqlclassic/media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_09.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sqlclassic/media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_10.png
[21]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sqlclassic/media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_11.png
[22]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sqlclassic/media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_12.png
[23]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sqlclassic/media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_13.png
[24]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sqlclassic/media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_14.png
[25]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sqlclassic/media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_15.png

























