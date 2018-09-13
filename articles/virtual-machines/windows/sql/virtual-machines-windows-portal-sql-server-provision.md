---
title: Provision a SQL Server Virtual Machine | Microsoft Docs
description: Create and connect to a SQL Server virtual machine in Azure using the Portal. This tutorial uses the Resource Manager mode.
services: virtual-machines-windows
documentationcenter: na
author: rothja
editor: ''
manager: jhubbard
tags: azure-resource-manager
ms.assetid: 1aff691f-a40a-4de2-b6a0-def1384e086e
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: infrastructure-services
ms.date: 04/03/2017
ms.author: jroth
ms.openlocfilehash: 8a22f38f910e1e215cbf42143378c5acdd87a1cd
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551670"
---
# <a name="provision-a-sql-server-virtual-machine-in-the-azure-portal"></a><span data-ttu-id="93471-104">Provision a SQL Server virtual machine in the Azure Portal</span><span class="sxs-lookup"><span data-stu-id="93471-104">Provision a SQL Server virtual machine in the Azure Portal</span></span>
> [!div class="op_single_selector"]
> * [Portal](virtual-machines-windows-portal-sql-server-provision.md)
> * [PowerShell](virtual-machines-windows-ps-sql-create.md)
> 
> 

<span data-ttu-id="93471-107">This end-to-end tutorial shows you how to use the Azure Portal to provision a virtual machine running SQL Server.</span><span class="sxs-lookup"><span data-stu-id="93471-107">This end-to-end tutorial shows you how to use the Azure Portal to provision a virtual machine running SQL Server.</span></span>

<span data-ttu-id="93471-108">The Azure virtual machine (VM) gallery includes several images that contain Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="93471-108">The Azure virtual machine (VM) gallery includes several images that contain Microsoft SQL Server.</span></span> <span data-ttu-id="93471-109">With a few clicks, you can select one of the SQL VM images from the gallery and provision it in your Azure environment.</span><span class="sxs-lookup"><span data-stu-id="93471-109">With a few clicks, you can select one of the SQL VM images from the gallery and provision it in your Azure environment.</span></span>

<span data-ttu-id="93471-110">In this tutorial, you will:</span><span class="sxs-lookup"><span data-stu-id="93471-110">In this tutorial, you will:</span></span>

* [<span data-ttu-id="93471-111">Select a SQL VM image from the gallery</span><span class="sxs-lookup"><span data-stu-id="93471-111">Select a SQL VM image from the gallery</span></span>](#select-a-sql-vm-image-from-the-gallery)
* [<span data-ttu-id="93471-112">Configure and create the VM</span><span class="sxs-lookup"><span data-stu-id="93471-112">Configure and create the VM</span></span>](#configure-the-vm)
* [<span data-ttu-id="93471-113">Open the VM with Remote Desktop</span><span class="sxs-lookup"><span data-stu-id="93471-113">Open the VM with Remote Desktop</span></span>](#open-the-vm-with-remote-desktop)
* [<span data-ttu-id="93471-114">Connect to SQL Server remotely</span><span class="sxs-lookup"><span data-stu-id="93471-114">Connect to SQL Server remotely</span></span>](#connect-to-sql-server-remotely)

## <a name="select-a-sql-vm-image-from-the-gallery"></a><span data-ttu-id="93471-115">Select a SQL VM image from the gallery</span><span class="sxs-lookup"><span data-stu-id="93471-115">Select a SQL VM image from the gallery</span></span>
1. <span data-ttu-id="93471-116">Log in to the [Azure portal](https://portal.azure.com) using your account.</span><span class="sxs-lookup"><span data-stu-id="93471-116">Log in to the [Azure portal](https://portal.azure.com) using your account.</span></span>
   
   > [!NOTE]
   > If you do not have an Azure account, visit [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).
   > 
   > 
2. <span data-ttu-id="93471-118">On the Azure portal, click **New**.</span><span class="sxs-lookup"><span data-stu-id="93471-118">On the Azure portal, click **New**.</span></span> <span data-ttu-id="93471-119">The portal opens the **New** blade.</span><span class="sxs-lookup"><span data-stu-id="93471-119">The portal opens the **New** blade.</span></span> <span data-ttu-id="93471-120">The SQL Server VM resources are in the **Compute** group of the Marketplace.</span><span class="sxs-lookup"><span data-stu-id="93471-120">The SQL Server VM resources are in the **Compute** group of the Marketplace.</span></span>
3. <span data-ttu-id="93471-121">In the **New** blade, click **Compute** and then click **See all**.</span><span class="sxs-lookup"><span data-stu-id="93471-121">In the **New** blade, click **Compute** and then click **See all**.</span></span>
4. <span data-ttu-id="93471-122">In the **Filter** text box type SQL Server, and press the ENTER key.</span><span class="sxs-lookup"><span data-stu-id="93471-122">In the **Filter** text box type SQL Server, and press the ENTER key.</span></span>

   ![Azure Virtual Machines Blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sql/media/virtual-machines-windows-portal-sql-server-provision/azure-compute-blade2.png)

5. <span data-ttu-id="93471-124">Review the available SQL Server images.</span><span class="sxs-lookup"><span data-stu-id="93471-124">Review the available SQL Server images.</span></span> <span data-ttu-id="93471-125">Each image identifies a SQL Server version and an operating system.</span><span class="sxs-lookup"><span data-stu-id="93471-125">Each image identifies a SQL Server version and an operating system.</span></span> 
6. <span data-ttu-id="93471-126">Select the image for SQL Server 2016 SP1 Developer on Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="93471-126">Select the image for SQL Server 2016 SP1 Developer on Windows Server 2016.</span></span>

   > [!TIP]
   > The Developer edition is used in this tutorial because it is a full-featured edition of SQL Server that is free for development testing purposes. You pay only for the cost of running the VM.
   
   > [!NOTE]
   > SQL VM images include the licensing costs for SQL Server into the per-minute pricing of the VM you create (except for the Developer and Express editions). SQL Server Developer is free for development/testing (not production) and SQL Express is free for lightweight workloads (less than 1GB memory, less than 10 GB storage). There is another option to bring-your-own-license (BYOL) and pay only for the VM. Those image names are prefixed with {BYOL}. For more information on this option, see  [Get started with SQL Server on Azure Virtual Machines](virtual-machines-windows-sql-server-iaas-overview.md).
   > 
   > 
7. <span data-ttu-id="93471-134">Under **Select a deployment model**, verify that **Resource Manager** is selected.</span><span class="sxs-lookup"><span data-stu-id="93471-134">Under **Select a deployment model**, verify that **Resource Manager** is selected.</span></span> <span data-ttu-id="93471-135">Resource Manager is the recommended deployment model for new virtual machines.</span><span class="sxs-lookup"><span data-stu-id="93471-135">Resource Manager is the recommended deployment model for new virtual machines.</span></span> <span data-ttu-id="93471-136">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="93471-136">Click **Create**.</span></span>
   
    ![Create SQL VM with Resource Manager](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sql/media/virtual-machines-windows-portal-sql-server-provision/azure-compute-sql-deployment-model.png)

## <a name="configure-the-vm"></a><span data-ttu-id="93471-138">Configure the VM</span><span class="sxs-lookup"><span data-stu-id="93471-138">Configure the VM</span></span>
<span data-ttu-id="93471-139">There are five blades for configuring a SQL Server virtual machine.</span><span class="sxs-lookup"><span data-stu-id="93471-139">There are five blades for configuring a SQL Server virtual machine.</span></span>

| <span data-ttu-id="93471-140">Step</span><span class="sxs-lookup"><span data-stu-id="93471-140">Step</span></span> | <span data-ttu-id="93471-141">Description</span><span class="sxs-lookup"><span data-stu-id="93471-141">Description</span></span> |
| --- | --- |
| <span data-ttu-id="93471-142">**Basics**</span><span class="sxs-lookup"><span data-stu-id="93471-142">**Basics**</span></span> |[<span data-ttu-id="93471-143">Configure basic settings</span><span class="sxs-lookup"><span data-stu-id="93471-143">Configure basic settings</span></span>](#1-configure-basic-settings) |
| <span data-ttu-id="93471-144">**Size**</span><span class="sxs-lookup"><span data-stu-id="93471-144">**Size**</span></span> |[<span data-ttu-id="93471-145">Choose virtual machine size</span><span class="sxs-lookup"><span data-stu-id="93471-145">Choose virtual machine size</span></span>](#2-choose-virtual-machine-size) |
| <span data-ttu-id="93471-146">**Settings**</span><span class="sxs-lookup"><span data-stu-id="93471-146">**Settings**</span></span> |[<span data-ttu-id="93471-147">Configure optional features</span><span class="sxs-lookup"><span data-stu-id="93471-147">Configure optional features</span></span>](#3-configure-optional-features) |
| <span data-ttu-id="93471-148">**SQL Server settings**</span><span class="sxs-lookup"><span data-stu-id="93471-148">**SQL Server settings**</span></span> |[<span data-ttu-id="93471-149">Configure SQL server settings</span><span class="sxs-lookup"><span data-stu-id="93471-149">Configure SQL server settings</span></span>](#4-configure-sql-server-settings) |
| <span data-ttu-id="93471-150">**Summary**</span><span class="sxs-lookup"><span data-stu-id="93471-150">**Summary**</span></span> |[<span data-ttu-id="93471-151">Review the summary</span><span class="sxs-lookup"><span data-stu-id="93471-151">Review the summary</span></span>](#5-review-the-summary) |

## <a name="1-configure-basic-settings"></a><span data-ttu-id="93471-152">1. Configure basic settings</span><span class="sxs-lookup"><span data-stu-id="93471-152">1. Configure basic settings</span></span>
<span data-ttu-id="93471-153">On the **Basics** blade, provide the following information:</span><span class="sxs-lookup"><span data-stu-id="93471-153">On the **Basics** blade, provide the following information:</span></span>

* <span data-ttu-id="93471-154">Enter a unique virtual machine **Name**.</span><span class="sxs-lookup"><span data-stu-id="93471-154">Enter a unique virtual machine **Name**.</span></span>
* <span data-ttu-id="93471-155">Specify a **User name** for the local administrator account on the VM.</span><span class="sxs-lookup"><span data-stu-id="93471-155">Specify a **User name** for the local administrator account on the VM.</span></span> <span data-ttu-id="93471-156">This account is also added to the SQL Server **sysadmin** fixed server role.</span><span class="sxs-lookup"><span data-stu-id="93471-156">This account is also added to the SQL Server **sysadmin** fixed server role.</span></span>
* <span data-ttu-id="93471-157">Provide a strong **Password**.</span><span class="sxs-lookup"><span data-stu-id="93471-157">Provide a strong **Password**.</span></span>
* <span data-ttu-id="93471-158">If you have multiple subscriptions, verify that the subscription is correct for the new VM.</span><span class="sxs-lookup"><span data-stu-id="93471-158">If you have multiple subscriptions, verify that the subscription is correct for the new VM.</span></span>
* <span data-ttu-id="93471-159">In the **Resource group** box, type a name for a new resource group.</span><span class="sxs-lookup"><span data-stu-id="93471-159">In the **Resource group** box, type a name for a new resource group.</span></span> <span data-ttu-id="93471-160">Alternatively, to use an existing resource group click **Use existing**.</span><span class="sxs-lookup"><span data-stu-id="93471-160">Alternatively, to use an existing resource group click **Use existing**.</span></span> <span data-ttu-id="93471-161">A resource group is a collection of related resources in Azure (virtual machines, storage accounts, virtual networks, etc.).</span><span class="sxs-lookup"><span data-stu-id="93471-161">A resource group is a collection of related resources in Azure (virtual machines, storage accounts, virtual networks, etc.).</span></span>
  
  > [!NOTE]
  > Using a new resource group is helpful if you are just testing or learning about SQL Server deployments in Azure. After you finish with your test, delete the resource group to automatically delete the VM and all resources associated with that resource group. For more information about resource groups, see [Azure Resource Manager Overview](../../../azure-resource-manager/resource-group-overview.md).
  > 
  > 
* <span data-ttu-id="93471-165">Select a **Location** for this deployment.</span><span class="sxs-lookup"><span data-stu-id="93471-165">Select a **Location** for this deployment.</span></span>
* <span data-ttu-id="93471-166">Click **OK** to save the settings.</span><span class="sxs-lookup"><span data-stu-id="93471-166">Click **OK** to save the settings.</span></span>
  
    ![SQL Basics Blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sql/media/virtual-machines-windows-portal-sql-server-provision/azure-sql-basic.png)

## <a name="2-choose-virtual-machine-size"></a><span data-ttu-id="93471-168">2. Choose virtual machine size</span><span class="sxs-lookup"><span data-stu-id="93471-168">2. Choose virtual machine size</span></span>
<span data-ttu-id="93471-169">On the **Size** step, choose a virtual machine size in the **Choose a size** blade.</span><span class="sxs-lookup"><span data-stu-id="93471-169">On the **Size** step, choose a virtual machine size in the **Choose a size** blade.</span></span> <span data-ttu-id="93471-170">The blade initially displays recommended machine sizes based on the image you selected.</span><span class="sxs-lookup"><span data-stu-id="93471-170">The blade initially displays recommended machine sizes based on the image you selected.</span></span>

> [!IMPORTANT]
> The estimated monthly cost displayed on the **Choose a size** blade does not include SQL Server licensing costs. This is the cost of the VM alone. For the Express and Developer editions of SQL Server, this is the total estimated cost. For other editions, see the [Windows Virtual Machines pricing page](https://azure.microsoft.com/pricing/details/virtual-machines/windows/) and select your target edition of SQL Server. 

![SQL VM Size Options](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sql/media/virtual-machines-windows-portal-sql-server-provision/azure-sql-vm-choose-a-size.png)

<span data-ttu-id="93471-176">For production workloads, we recommend selecting a virtual machine size that supports [Premium Storage](../../../storage/storage-premium-storage.md).</span><span class="sxs-lookup"><span data-stu-id="93471-176">For production workloads, we recommend selecting a virtual machine size that supports [Premium Storage](../../../storage/storage-premium-storage.md).</span></span> <span data-ttu-id="93471-177">If you do not require that level of performance, use the **View all** button, which shows all machine size options.</span><span class="sxs-lookup"><span data-stu-id="93471-177">If you do not require that level of performance, use the **View all** button, which shows all machine size options.</span></span> <span data-ttu-id="93471-178">For example, you might use a smaller machine size for a development or test environment.</span><span class="sxs-lookup"><span data-stu-id="93471-178">For example, you might use a smaller machine size for a development or test environment.</span></span>

> [!NOTE]
> For more information about virtual machine sizes see, [Sizes for virtual machines](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). For considerations about SQL Server VM sizes, see [Performance best practices for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-performance.md).
> 
> 

<span data-ttu-id="93471-181">Choose your machine size, and then click **Select**.</span><span class="sxs-lookup"><span data-stu-id="93471-181">Choose your machine size, and then click **Select**.</span></span>

## <a name="3-configure-optional-features"></a><span data-ttu-id="93471-182">3. Configure optional features</span><span class="sxs-lookup"><span data-stu-id="93471-182">3. Configure optional features</span></span>
<span data-ttu-id="93471-183">On the **Settings** blade, configure Azure storage, networking, and monitoring for the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="93471-183">On the **Settings** blade, configure Azure storage, networking, and monitoring for the virtual machine.</span></span>

* <span data-ttu-id="93471-184">Under **Storage**, specify a **Disk type** of either Standard or Premium (SSD).</span><span class="sxs-lookup"><span data-stu-id="93471-184">Under **Storage**, specify a **Disk type** of either Standard or Premium (SSD).</span></span> <span data-ttu-id="93471-185">Premium storage is recommended for production workloads.</span><span class="sxs-lookup"><span data-stu-id="93471-185">Premium storage is recommended for production workloads.</span></span>

> [!NOTE]
> If you select Premium (SSD) for a machine size that does not support Premium Storage, your machine size changes automatically.  
> 
> 

* <span data-ttu-id="93471-187">Under **Storage account**, you can accept the automatically provisioned storage account name.</span><span class="sxs-lookup"><span data-stu-id="93471-187">Under **Storage account**, you can accept the automatically provisioned storage account name.</span></span> <span data-ttu-id="93471-188">You can also click on **Storage account** to choose an existing account and configure the storage account type.</span><span class="sxs-lookup"><span data-stu-id="93471-188">You can also click on **Storage account** to choose an existing account and configure the storage account type.</span></span> <span data-ttu-id="93471-189">By default, Azure creates a new storage account with locally redundant storage.</span><span class="sxs-lookup"><span data-stu-id="93471-189">By default, Azure creates a new storage account with locally redundant storage.</span></span> <span data-ttu-id="93471-190">For more information about storage options, see [Azure Storage replication](../../../storage/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="93471-190">For more information about storage options, see [Azure Storage replication](../../../storage/storage-redundancy.md).</span></span>
* <span data-ttu-id="93471-191">Under **Network**, you can accept the automatically populated values.</span><span class="sxs-lookup"><span data-stu-id="93471-191">Under **Network**, you can accept the automatically populated values.</span></span> <span data-ttu-id="93471-192">You can also click on each feature to manually configure the **Virtual network**, **Subnet**, **Public IP address**, and **Network Security Group**.</span><span class="sxs-lookup"><span data-stu-id="93471-192">You can also click on each feature to manually configure the **Virtual network**, **Subnet**, **Public IP address**, and **Network Security Group**.</span></span> <span data-ttu-id="93471-193">For the purposes of this tutorial, keep the default values.</span><span class="sxs-lookup"><span data-stu-id="93471-193">For the purposes of this tutorial, keep the default values.</span></span>
* <span data-ttu-id="93471-194">Azure enables **Monitoring** by default with the same storage account designated for the VM.</span><span class="sxs-lookup"><span data-stu-id="93471-194">Azure enables **Monitoring** by default with the same storage account designated for the VM.</span></span> <span data-ttu-id="93471-195">You can change these settings here.</span><span class="sxs-lookup"><span data-stu-id="93471-195">You can change these settings here.</span></span>
* <span data-ttu-id="93471-196">Under **Availability set**, specify an availability set.</span><span class="sxs-lookup"><span data-stu-id="93471-196">Under **Availability set**, specify an availability set.</span></span> <span data-ttu-id="93471-197">For the purposes of this tutorial, you can select **none**.</span><span class="sxs-lookup"><span data-stu-id="93471-197">For the purposes of this tutorial, you can select **none**.</span></span> <span data-ttu-id="93471-198">If you plan to set up SQL AlwaysOn Availability Groups, configure the availability to avoid recreating the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="93471-198">If you plan to set up SQL AlwaysOn Availability Groups, configure the availability to avoid recreating the virtual machine.</span></span>  <span data-ttu-id="93471-199">For more information, see [Manage the Availability of Virtual Machines](../manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="93471-199">For more information, see [Manage the Availability of Virtual Machines](../manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="93471-200">When you are done configuring these settings, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="93471-200">When you are done configuring these settings, click **OK**.</span></span>

## <a name="4-configure-sql-server-settings"></a><span data-ttu-id="93471-201">4. Configure SQL server settings</span><span class="sxs-lookup"><span data-stu-id="93471-201">4. Configure SQL server settings</span></span>
<span data-ttu-id="93471-202">On the **SQL Server settings** blade, configure specific settings and optimizations for SQL Server.</span><span class="sxs-lookup"><span data-stu-id="93471-202">On the **SQL Server settings** blade, configure specific settings and optimizations for SQL Server.</span></span> <span data-ttu-id="93471-203">The settings that you can configure for SQL Server include the following.</span><span class="sxs-lookup"><span data-stu-id="93471-203">The settings that you can configure for SQL Server include the following.</span></span>

| <span data-ttu-id="93471-204">Setting</span><span class="sxs-lookup"><span data-stu-id="93471-204">Setting</span></span> |
| --- |
| [<span data-ttu-id="93471-205">Connectivity</span><span class="sxs-lookup"><span data-stu-id="93471-205">Connectivity</span></span>](#connectivity) |
| [<span data-ttu-id="93471-206">Authentication</span><span class="sxs-lookup"><span data-stu-id="93471-206">Authentication</span></span>](#authentication) |
| [<span data-ttu-id="93471-207">Storage configuration</span><span class="sxs-lookup"><span data-stu-id="93471-207">Storage configuration</span></span>](#storage-configuration) |
| [<span data-ttu-id="93471-208">Automated Patching</span><span class="sxs-lookup"><span data-stu-id="93471-208">Automated Patching</span></span>](#automated-patching) |
| [<span data-ttu-id="93471-209">Automated Backup</span><span class="sxs-lookup"><span data-stu-id="93471-209">Automated Backup</span></span>](#automated-backup) |
| [<span data-ttu-id="93471-210">Azure Key Vault Integration</span><span class="sxs-lookup"><span data-stu-id="93471-210">Azure Key Vault Integration</span></span>](#azure-key-vault-integration) |
| [<span data-ttu-id="93471-211">R Services</span><span class="sxs-lookup"><span data-stu-id="93471-211">R Services</span></span>](#r-services) |

### <a name="connectivity"></a><span data-ttu-id="93471-212">Connectivity</span><span class="sxs-lookup"><span data-stu-id="93471-212">Connectivity</span></span>
<span data-ttu-id="93471-213">Under **SQL connectivity**, specify the type of access you want to the SQL Server instance on this VM.</span><span class="sxs-lookup"><span data-stu-id="93471-213">Under **SQL connectivity**, specify the type of access you want to the SQL Server instance on this VM.</span></span> <span data-ttu-id="93471-214">For the purposes of this tutorial, select **Public (internet)** to allow connections to SQL Server from machines or services on the internet.</span><span class="sxs-lookup"><span data-stu-id="93471-214">For the purposes of this tutorial, select **Public (internet)** to allow connections to SQL Server from machines or services on the internet.</span></span> <span data-ttu-id="93471-215">With this option selected, Azure automatically configures the firewall and the network security group to allow traffic on port 1433.</span><span class="sxs-lookup"><span data-stu-id="93471-215">With this option selected, Azure automatically configures the firewall and the network security group to allow traffic on port 1433.</span></span>  

![SQL Connectivity Options](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sql/media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-connectivity-alt.png)

<span data-ttu-id="93471-217">To connect to SQL Server via the internet, you also must enable SQL Server Authentication, which is described in the next section.</span><span class="sxs-lookup"><span data-stu-id="93471-217">To connect to SQL Server via the internet, you also must enable SQL Server Authentication, which is described in the next section.</span></span>

> [!NOTE]
> It is possible to add more restrictions for the network communications to your SQL Server VM. You can do this by editing the Network Security Group after the VM is created. For more information, see [What is a Network Security Group (NSG)?](../../../virtual-network/virtual-networks-nsg.md)
> 
> 

<span data-ttu-id="93471-221">If you would prefer to not enable connections to the Database Engine via the internet, choose one of the following options:</span><span class="sxs-lookup"><span data-stu-id="93471-221">If you would prefer to not enable connections to the Database Engine via the internet, choose one of the following options:</span></span>

* <span data-ttu-id="93471-222">**Local (inside VM only)** to allow connections to SQL Server only from within the VM.</span><span class="sxs-lookup"><span data-stu-id="93471-222">**Local (inside VM only)** to allow connections to SQL Server only from within the VM.</span></span>
* <span data-ttu-id="93471-223">**Private (within Virtual Network)** to allow connections to SQL Server from machines or services in the same virtual network.</span><span class="sxs-lookup"><span data-stu-id="93471-223">**Private (within Virtual Network)** to allow connections to SQL Server from machines or services in the same virtual network.</span></span>

> [!NOTE]
> The virtual machine image for SQL Server Express edition does not automatically enable the TCP/IP protocol. This is true even for the Public and  Private connectivity options. For Express edition, you must use SQL Server Configuration Manager to [manually enable the TCP/IP protocol](#configure-sql-server-to-listen-on-the-tcp-protocol) after creating the VM.
> 
> 

<span data-ttu-id="93471-227">In general, improve security by choosing the most restrictive connectivity that your scenario allows.</span><span class="sxs-lookup"><span data-stu-id="93471-227">In general, improve security by choosing the most restrictive connectivity that your scenario allows.</span></span> <span data-ttu-id="93471-228">But all the options are securable through Network Security Group rules and SQL/Windows Authentication.</span><span class="sxs-lookup"><span data-stu-id="93471-228">But all the options are securable through Network Security Group rules and SQL/Windows Authentication.</span></span>

<span data-ttu-id="93471-229">**Port** defaults to 1433.</span><span class="sxs-lookup"><span data-stu-id="93471-229">**Port** defaults to 1433.</span></span> <span data-ttu-id="93471-230">You can specify a different port number.</span><span class="sxs-lookup"><span data-stu-id="93471-230">You can specify a different port number.</span></span>
<span data-ttu-id="93471-231">For more information, see [Connect to a SQL Server Virtual Machine (Resource Manager) | Microsoft Azure](virtual-machines-windows-sql-connect.md).</span><span class="sxs-lookup"><span data-stu-id="93471-231">For more information, see [Connect to a SQL Server Virtual Machine (Resource Manager) | Microsoft Azure](virtual-machines-windows-sql-connect.md).</span></span>

### <a name="authentication"></a><span data-ttu-id="93471-232">Authentication</span><span class="sxs-lookup"><span data-stu-id="93471-232">Authentication</span></span>
<span data-ttu-id="93471-233">If you require SQL Server Authentication, click **Enable** under **SQL authentication**.</span><span class="sxs-lookup"><span data-stu-id="93471-233">If you require SQL Server Authentication, click **Enable** under **SQL authentication**.</span></span>

![SQL Server Authentication](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sql/media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-authentication.png)

> [!NOTE]
> If you plan to access SQL Server over the internet (i.e. the Public connectivity option), you must enable SQL authentication here. Public access to the SQL Server requires the use of SQL Authentication.
> 
> 

<span data-ttu-id="93471-237">If you enable SQL Server Authentication, specify a **Login name** and **Password**.</span><span class="sxs-lookup"><span data-stu-id="93471-237">If you enable SQL Server Authentication, specify a **Login name** and **Password**.</span></span> <span data-ttu-id="93471-238">This user name is configured as a SQL Server Authentication login and member of the **sysadmin** fixed server role.</span><span class="sxs-lookup"><span data-stu-id="93471-238">This user name is configured as a SQL Server Authentication login and member of the **sysadmin** fixed server role.</span></span> <span data-ttu-id="93471-239">See [Choose an Authentication Mode](http://msdn.microsoft.com/library/ms144284.aspx) for more information about Authentication Modes.</span><span class="sxs-lookup"><span data-stu-id="93471-239">See [Choose an Authentication Mode](http://msdn.microsoft.com/library/ms144284.aspx) for more information about Authentication Modes.</span></span>

<span data-ttu-id="93471-240">If you do not enable SQL Server Authentication, then you can use the local Administrator account on the VM to connect to the SQL Server instance.</span><span class="sxs-lookup"><span data-stu-id="93471-240">If you do not enable SQL Server Authentication, then you can use the local Administrator account on the VM to connect to the SQL Server instance.</span></span>

### <a name="storage-configuration"></a><span data-ttu-id="93471-241">Storage configuration</span><span class="sxs-lookup"><span data-stu-id="93471-241">Storage configuration</span></span>
<span data-ttu-id="93471-242">Click **Storage configuration** to specify the storage requirements.</span><span class="sxs-lookup"><span data-stu-id="93471-242">Click **Storage configuration** to specify the storage requirements.</span></span>

![SQL Storage Configuration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sql/media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-storage.png)

> [!NOTE]
> If you select Standard storage, this option is not available. Automatic storage optimization is available only for Premium Storage.
> 
> 

<span data-ttu-id="93471-246">You can specify requirements as input/output operations per second (IOPs), throughput in MB/s, and total storage size.</span><span class="sxs-lookup"><span data-stu-id="93471-246">You can specify requirements as input/output operations per second (IOPs), throughput in MB/s, and total storage size.</span></span> <span data-ttu-id="93471-247">Configure these values by using the sliding scales.</span><span class="sxs-lookup"><span data-stu-id="93471-247">Configure these values by using the sliding scales.</span></span> <span data-ttu-id="93471-248">The portal automatically calculates the number of disks based on these requirements.</span><span class="sxs-lookup"><span data-stu-id="93471-248">The portal automatically calculates the number of disks based on these requirements.</span></span>

<span data-ttu-id="93471-249">By default, Azure optimizes the storage for 5000 IOPs, 200 MBs, and 1 TB of storage space.</span><span class="sxs-lookup"><span data-stu-id="93471-249">By default, Azure optimizes the storage for 5000 IOPs, 200 MBs, and 1 TB of storage space.</span></span> <span data-ttu-id="93471-250">You can change these storage settings based on workload.</span><span class="sxs-lookup"><span data-stu-id="93471-250">You can change these storage settings based on workload.</span></span> <span data-ttu-id="93471-251">Under **Storage optimized for**, select one of the following options:</span><span class="sxs-lookup"><span data-stu-id="93471-251">Under **Storage optimized for**, select one of the following options:</span></span>

* <span data-ttu-id="93471-252">**General** is the default setting and supports most workloads.</span><span class="sxs-lookup"><span data-stu-id="93471-252">**General** is the default setting and supports most workloads.</span></span>
* <span data-ttu-id="93471-253">**Transactional** processing optimizes the storage for traditional database OLTP workloads.</span><span class="sxs-lookup"><span data-stu-id="93471-253">**Transactional** processing optimizes the storage for traditional database OLTP workloads.</span></span>
* <span data-ttu-id="93471-254">**Data warehousing** optimizes the storage for analytic and reporting workloads.</span><span class="sxs-lookup"><span data-stu-id="93471-254">**Data warehousing** optimizes the storage for analytic and reporting workloads.</span></span>

> [!NOTE]
> The upper limits on the sliders vary depending on your selected virtual machine size.
> 
> 

### <a name="automated-patching"></a><span data-ttu-id="93471-256">Automated patching</span><span class="sxs-lookup"><span data-stu-id="93471-256">Automated patching</span></span>
<span data-ttu-id="93471-257">**Automated patching** is enabled by default.</span><span class="sxs-lookup"><span data-stu-id="93471-257">**Automated patching** is enabled by default.</span></span> <span data-ttu-id="93471-258">Automated patching allows Azure to automatically patch SQL Server and the operating system.</span><span class="sxs-lookup"><span data-stu-id="93471-258">Automated patching allows Azure to automatically patch SQL Server and the operating system.</span></span> <span data-ttu-id="93471-259">Specify a day of the week, time, and duration for a maintenance window.</span><span class="sxs-lookup"><span data-stu-id="93471-259">Specify a day of the week, time, and duration for a maintenance window.</span></span> <span data-ttu-id="93471-260">Azure performs patching in this maintenance window.</span><span class="sxs-lookup"><span data-stu-id="93471-260">Azure performs patching in this maintenance window.</span></span> <span data-ttu-id="93471-261">The maintenance window schedule uses the VM locale for time.</span><span class="sxs-lookup"><span data-stu-id="93471-261">The maintenance window schedule uses the VM locale for time.</span></span> <span data-ttu-id="93471-262">If you do not want Azure to automatically patch SQL Server and the operating system, click **Disable**.</span><span class="sxs-lookup"><span data-stu-id="93471-262">If you do not want Azure to automatically patch SQL Server and the operating system, click **Disable**.</span></span>  

![SQL Automated Patching](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sql/media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-patching.png)

<span data-ttu-id="93471-264">For more information, see [Automated Patching for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-automated-patching.md).</span><span class="sxs-lookup"><span data-stu-id="93471-264">For more information, see [Automated Patching for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-automated-patching.md).</span></span>

### <a name="automated-backup"></a><span data-ttu-id="93471-265">Automated backup</span><span class="sxs-lookup"><span data-stu-id="93471-265">Automated backup</span></span>
<span data-ttu-id="93471-266">Enable automatic database backups for all databases under **Automated backup**.</span><span class="sxs-lookup"><span data-stu-id="93471-266">Enable automatic database backups for all databases under **Automated backup**.</span></span> <span data-ttu-id="93471-267">Automated backup is disabled by default.</span><span class="sxs-lookup"><span data-stu-id="93471-267">Automated backup is disabled by default.</span></span>

<span data-ttu-id="93471-268">When you enable SQL automated backup, you can configure the following:</span><span class="sxs-lookup"><span data-stu-id="93471-268">When you enable SQL automated backup, you can configure the following:</span></span>

* <span data-ttu-id="93471-269">Retention period (days) for backups</span><span class="sxs-lookup"><span data-stu-id="93471-269">Retention period (days) for backups</span></span>
* <span data-ttu-id="93471-270">Storage account to use for backups</span><span class="sxs-lookup"><span data-stu-id="93471-270">Storage account to use for backups</span></span>
* <span data-ttu-id="93471-271">Encryption option and password for backups</span><span class="sxs-lookup"><span data-stu-id="93471-271">Encryption option and password for backups</span></span>
* <span data-ttu-id="93471-272">Backup system databases</span><span class="sxs-lookup"><span data-stu-id="93471-272">Backup system databases</span></span>
* <span data-ttu-id="93471-273">Configure backup schedule</span><span class="sxs-lookup"><span data-stu-id="93471-273">Configure backup schedule</span></span>

<span data-ttu-id="93471-274">To encrypt the backup, click **Enable**.</span><span class="sxs-lookup"><span data-stu-id="93471-274">To encrypt the backup, click **Enable**.</span></span> <span data-ttu-id="93471-275">Then specify the **Password**.</span><span class="sxs-lookup"><span data-stu-id="93471-275">Then specify the **Password**.</span></span> <span data-ttu-id="93471-276">Azure creates a certificate to encrypt the backups and uses the specified password to protect that certificate.</span><span class="sxs-lookup"><span data-stu-id="93471-276">Azure creates a certificate to encrypt the backups and uses the specified password to protect that certificate.</span></span>

![SQL Automated Backup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sql/media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-autobackup2.png)

 <span data-ttu-id="93471-278">For more information, see [Automated Backup for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-automated-backup.md).</span><span class="sxs-lookup"><span data-stu-id="93471-278">For more information, see [Automated Backup for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-automated-backup.md).</span></span>

### <a name="azure-key-vault-integration"></a><span data-ttu-id="93471-279">Azure Key Vault integration</span><span class="sxs-lookup"><span data-stu-id="93471-279">Azure Key Vault integration</span></span>
<span data-ttu-id="93471-280">To store security secrets in Azure for encryption, click **Azure key vault integration** and click **Enable**.</span><span class="sxs-lookup"><span data-stu-id="93471-280">To store security secrets in Azure for encryption, click **Azure key vault integration** and click **Enable**.</span></span>

![SQL Azure Key Vault Integration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sql/media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-akv.png)

<span data-ttu-id="93471-282">The following table lists the parameters required to configure Azure Key Vault Integration.</span><span class="sxs-lookup"><span data-stu-id="93471-282">The following table lists the parameters required to configure Azure Key Vault Integration.</span></span>

| <span data-ttu-id="93471-283">PARAMETER</span><span class="sxs-lookup"><span data-stu-id="93471-283">PARAMETER</span></span> | <span data-ttu-id="93471-284">DESCRIPTION</span><span class="sxs-lookup"><span data-stu-id="93471-284">DESCRIPTION</span></span> | <span data-ttu-id="93471-285">EXAMPLE</span><span class="sxs-lookup"><span data-stu-id="93471-285">EXAMPLE</span></span> |
| --- | --- | --- |
| <span data-ttu-id="93471-286">**Key Vault URL**</span><span class="sxs-lookup"><span data-stu-id="93471-286">**Key Vault URL**</span></span> |<span data-ttu-id="93471-287">The location of the key vault.</span><span class="sxs-lookup"><span data-stu-id="93471-287">The location of the key vault.</span></span> |https://contosokeyvault.vault.azure.net/ |
| <span data-ttu-id="93471-288">**Principal name**</span><span class="sxs-lookup"><span data-stu-id="93471-288">**Principal name**</span></span> |<span data-ttu-id="93471-289">Azure Active Directory service principal name.</span><span class="sxs-lookup"><span data-stu-id="93471-289">Azure Active Directory service principal name.</span></span> <span data-ttu-id="93471-290">This name is also referred to as the Client ID.</span><span class="sxs-lookup"><span data-stu-id="93471-290">This name is also referred to as the Client ID.</span></span> |<span data-ttu-id="93471-291">fde2b411-33d5-4e11-af04eb07b669ccf2</span><span class="sxs-lookup"><span data-stu-id="93471-291">fde2b411-33d5-4e11-af04eb07b669ccf2</span></span> |
| <span data-ttu-id="93471-292">**Principal secret**</span><span class="sxs-lookup"><span data-stu-id="93471-292">**Principal secret**</span></span> |<span data-ttu-id="93471-293">Azure Active Directory service principal secret.</span><span class="sxs-lookup"><span data-stu-id="93471-293">Azure Active Directory service principal secret.</span></span> <span data-ttu-id="93471-294">This secret is also referred to as the Client Secret.</span><span class="sxs-lookup"><span data-stu-id="93471-294">This secret is also referred to as the Client Secret.</span></span> |<span data-ttu-id="93471-295">9VTJSQwzlFepD8XODnzy8n2V01Jd8dAjwm/azF1XDKM=</span><span class="sxs-lookup"><span data-stu-id="93471-295">9VTJSQwzlFepD8XODnzy8n2V01Jd8dAjwm/azF1XDKM=</span></span> |
| <span data-ttu-id="93471-296">**Credential name**</span><span class="sxs-lookup"><span data-stu-id="93471-296">**Credential name**</span></span> |<span data-ttu-id="93471-297">**Credential name**: AKV Integration creates a credential within SQL Server, allowing the VM to have access to the key vault.</span><span class="sxs-lookup"><span data-stu-id="93471-297">**Credential name**: AKV Integration creates a credential within SQL Server, allowing the VM to have access to the key vault.</span></span> <span data-ttu-id="93471-298">Choose a name for this credential.</span><span class="sxs-lookup"><span data-stu-id="93471-298">Choose a name for this credential.</span></span> |<span data-ttu-id="93471-299">mycred1</span><span class="sxs-lookup"><span data-stu-id="93471-299">mycred1</span></span> |

<span data-ttu-id="93471-300">For more information, see [Configure Azure Key Vault Integration for SQL Server on Azure VMs](virtual-machines-windows-ps-sql-keyvault.md).</span><span class="sxs-lookup"><span data-stu-id="93471-300">For more information, see [Configure Azure Key Vault Integration for SQL Server on Azure VMs](virtual-machines-windows-ps-sql-keyvault.md).</span></span>

<span data-ttu-id="93471-301">When you are finished configuring SQL Server settings, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="93471-301">When you are finished configuring SQL Server settings, click **OK**.</span></span>

### <a name="r-services"></a><span data-ttu-id="93471-302">R services</span><span class="sxs-lookup"><span data-stu-id="93471-302">R services</span></span>
<span data-ttu-id="93471-303">You have the option to enable [SQL Server R Services](https://msdn.microsoft.com/library/mt604845.aspx).</span><span class="sxs-lookup"><span data-stu-id="93471-303">You have the option to enable [SQL Server R Services](https://msdn.microsoft.com/library/mt604845.aspx).</span></span> <span data-ttu-id="93471-304">This enables you to use advanced analytics with SQL Server 2016.</span><span class="sxs-lookup"><span data-stu-id="93471-304">This enables you to use advanced analytics with SQL Server 2016.</span></span> <span data-ttu-id="93471-305">Click **Enable** on the **SQL Server Settings** blade.</span><span class="sxs-lookup"><span data-stu-id="93471-305">Click **Enable** on the **SQL Server Settings** blade.</span></span>

![Enable SQL Server R Services](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sql/media/virtual-machines-windows-portal-sql-server-provision/azure-vm-sql-server-r-services.png)


## <a name="5-review-the-summary"></a><span data-ttu-id="93471-307">5. Review the summary</span><span class="sxs-lookup"><span data-stu-id="93471-307">5. Review the summary</span></span>
<span data-ttu-id="93471-308">On the **Summary** blade, review the summary and click **OK** to create SQL Server, resource group, and resources specified for this VM.</span><span class="sxs-lookup"><span data-stu-id="93471-308">On the **Summary** blade, review the summary and click **OK** to create SQL Server, resource group, and resources specified for this VM.</span></span>

<span data-ttu-id="93471-309">You can monitor the deployment from the azure portal.</span><span class="sxs-lookup"><span data-stu-id="93471-309">You can monitor the deployment from the azure portal.</span></span> <span data-ttu-id="93471-310">The **Notifications** button at the top of the screen shows basic status of the deployment.</span><span class="sxs-lookup"><span data-stu-id="93471-310">The **Notifications** button at the top of the screen shows basic status of the deployment.</span></span>

> [!NOTE]
> To provide you with an idea on deployment times, I deployed a SQL VM to the East US region with default settings. This test deployment took a total of 26 minutes to complete. But you might experience a faster or slower deployment time based on your region and selected settings.
> 
> 

## <a name="open-the-vm-with-remote-desktop"></a><span data-ttu-id="93471-314">Open the VM with Remote Desktop</span><span class="sxs-lookup"><span data-stu-id="93471-314">Open the VM with Remote Desktop</span></span>
<span data-ttu-id="93471-315">Use the following steps to connect to the virtual machine with Remote Desktop:</span><span class="sxs-lookup"><span data-stu-id="93471-315">Use the following steps to connect to the virtual machine with Remote Desktop:</span></span>

1. <span data-ttu-id="93471-316">After the Azure VM is built, the icon for the VM appears on your Azure dashboard.</span><span class="sxs-lookup"><span data-stu-id="93471-316">After the Azure VM is built, the icon for the VM appears on your Azure dashboard.</span></span> <span data-ttu-id="93471-317">You can also find it by browsing your existing virtual machines.</span><span class="sxs-lookup"><span data-stu-id="93471-317">You can also find it by browsing your existing virtual machines.</span></span> <span data-ttu-id="93471-318">Click on your new SQL virtual machine.</span><span class="sxs-lookup"><span data-stu-id="93471-318">Click on your new SQL virtual machine.</span></span> <span data-ttu-id="93471-319">A **Virtual machine** blade displays your virtual machine details.</span><span class="sxs-lookup"><span data-stu-id="93471-319">A **Virtual machine** blade displays your virtual machine details.</span></span>
2. <span data-ttu-id="93471-320">At the top of the **Virtual machine** blade, click **Connect**.</span><span class="sxs-lookup"><span data-stu-id="93471-320">At the top of the **Virtual machine** blade, click **Connect**.</span></span>
3. <span data-ttu-id="93471-321">The browser downloads an RDP file for the VM.</span><span class="sxs-lookup"><span data-stu-id="93471-321">The browser downloads an RDP file for the VM.</span></span> <span data-ttu-id="93471-322">Open the RDP file.</span><span class="sxs-lookup"><span data-stu-id="93471-322">Open the RDP file.</span></span>
    <span data-ttu-id="93471-323">![Remote Desktop to SQL VM](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sql/media/virtual-machines-windows-portal-sql-server-provision/azure-sql-vm-remote-desktop.png)</span><span class="sxs-lookup"><span data-stu-id="93471-323">![Remote Desktop to SQL VM](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sql/media/virtual-machines-windows-portal-sql-server-provision/azure-sql-vm-remote-desktop.png)</span></span>
4. <span data-ttu-id="93471-324">The Remote Desktop Connection notifies you that the publisher of this remote connection cannot be identified.</span><span class="sxs-lookup"><span data-stu-id="93471-324">The Remote Desktop Connection notifies you that the publisher of this remote connection cannot be identified.</span></span> <span data-ttu-id="93471-325">Click **Connect** to continue.</span><span class="sxs-lookup"><span data-stu-id="93471-325">Click **Connect** to continue.</span></span>
5. <span data-ttu-id="93471-326">In the **Windows Security** dialog, click **Use another account**.</span><span class="sxs-lookup"><span data-stu-id="93471-326">In the **Windows Security** dialog, click **Use another account**.</span></span>
6. <span data-ttu-id="93471-327">For **User name** type **\<user name>**, where <user name> is the user name that you specified when you configured the VM.</span><span class="sxs-lookup"><span data-stu-id="93471-327">For **User name** type **\<user name>**, where <user name> is the user name that you specified when you configured the VM.</span></span> <span data-ttu-id="93471-328">You have to add an initial backslash before the name.</span><span class="sxs-lookup"><span data-stu-id="93471-328">You have to add an initial backslash before the name.</span></span>
7. <span data-ttu-id="93471-329">Type the **Password** that you previously configured for this VM, and then click **OK** to connect.</span><span class="sxs-lookup"><span data-stu-id="93471-329">Type the **Password** that you previously configured for this VM, and then click **OK** to connect.</span></span>
8. <span data-ttu-id="93471-330">If another **Remote Desktop Connection** dialog asks you whether to connect, click **Yes**.</span><span class="sxs-lookup"><span data-stu-id="93471-330">If another **Remote Desktop Connection** dialog asks you whether to connect, click **Yes**.</span></span>

<span data-ttu-id="93471-331">After you connect to the SQL Server virtual machine, you can launch SQL Server Management Studio and connect with Windows Authentication using your local administrator credentials.</span><span class="sxs-lookup"><span data-stu-id="93471-331">After you connect to the SQL Server virtual machine, you can launch SQL Server Management Studio and connect with Windows Authentication using your local administrator credentials.</span></span> <span data-ttu-id="93471-332">If you enabled SQL Server Authentication, you can also connect with SQL Authentication using the SQL login and password you configured during provisioning.</span><span class="sxs-lookup"><span data-stu-id="93471-332">If you enabled SQL Server Authentication, you can also connect with SQL Authentication using the SQL login and password you configured during provisioning.</span></span>

<span data-ttu-id="93471-333">Access to the machine enables you to directly change machine and SQL Server settings based on your requirements.</span><span class="sxs-lookup"><span data-stu-id="93471-333">Access to the machine enables you to directly change machine and SQL Server settings based on your requirements.</span></span> <span data-ttu-id="93471-334">For example, you could configure the firewall settings or change SQL Server configuration settings.</span><span class="sxs-lookup"><span data-stu-id="93471-334">For example, you could configure the firewall settings or change SQL Server configuration settings.</span></span>

## <a name="connect-to-sql-server-remotely"></a><span data-ttu-id="93471-335">Connect to SQL Server remotely</span><span class="sxs-lookup"><span data-stu-id="93471-335">Connect to SQL Server remotely</span></span>
<span data-ttu-id="93471-336">In this tutorial, we selected **Public** access for the virtual machine and **SQL Server Authentication**.</span><span class="sxs-lookup"><span data-stu-id="93471-336">In this tutorial, we selected **Public** access for the virtual machine and **SQL Server Authentication**.</span></span> <span data-ttu-id="93471-337">These settings automatically configured the virtual machine to allow SQL Server connections from any client over the internet (assuming they have the correct SQL login).</span><span class="sxs-lookup"><span data-stu-id="93471-337">These settings automatically configured the virtual machine to allow SQL Server connections from any client over the internet (assuming they have the correct SQL login).</span></span>

> [!NOTE]
> If you did not select Public during provisioning, then extra steps are required to access your SQL Server instance over the internet. For more information, see  [Connect to a SQL Server Virtual Machine](virtual-machines-windows-sql-connect.md).
> 
> 

<span data-ttu-id="93471-340">The following sections show how to connect to your SQL Server instance on your VM from a different computer over the internet.</span><span class="sxs-lookup"><span data-stu-id="93471-340">The following sections show how to connect to your SQL Server instance on your VM from a different computer over the internet.</span></span>

> [!INCLUDE [Connect to SQL Server in a VM Resource Manager](../../../../includes/virtual-machines-sql-server-connection-steps-resource-manager.md)]
> 
> 

## <a name="next-steps"></a><span data-ttu-id="93471-341">Next Steps</span><span class="sxs-lookup"><span data-stu-id="93471-341">Next Steps</span></span>
<span data-ttu-id="93471-342">For other information about using SQL Server in Azure, see [SQL Server on Azure Virtual Machines](virtual-machines-windows-sql-server-iaas-overview.md) and the [Frequently Asked Questions](virtual-machines-windows-sql-server-iaas-faq.md).</span><span class="sxs-lookup"><span data-stu-id="93471-342">For other information about using SQL Server in Azure, see [SQL Server on Azure Virtual Machines](virtual-machines-windows-sql-server-iaas-overview.md) and the [Frequently Asked Questions](virtual-machines-windows-sql-server-iaas-faq.md).</span></span>

<span data-ttu-id="93471-343">For a video overview of SQL Server on Azure Virtual Machines, watch [Azure VM is the best platform for SQL Server 2016](https://channel9.msdn.com/Events/DataDriven/SQLServer2016/Azure-VM-is-the-best-platform-for-SQL-Server-2016).</span><span class="sxs-lookup"><span data-stu-id="93471-343">For a video overview of SQL Server on Azure Virtual Machines, watch [Azure VM is the best platform for SQL Server 2016](https://channel9.msdn.com/Events/DataDriven/SQLServer2016/Azure-VM-is-the-best-platform-for-SQL-Server-2016).</span></span>

<span data-ttu-id="93471-344">[Explore the Learning Path](https://azure.microsoft.com/documentation/learning-paths/sql-azure-vm/) for SQL Server on Azure virtual machines.</span><span class="sxs-lookup"><span data-stu-id="93471-344">[Explore the Learning Path](https://azure.microsoft.com/documentation/learning-paths/sql-azure-vm/) for SQL Server on Azure virtual machines.</span></span>













