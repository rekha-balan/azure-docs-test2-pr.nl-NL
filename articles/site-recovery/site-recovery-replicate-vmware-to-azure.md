---
title: Replicate applications (VMware to Azure) | Microsoft Docs
description: This article describes how to set up replication of virtual machines running on VMware into Azure.
services: site-recovery
documentationcenter: ''
author: asgang
manager: rochakm
editor: ''
ms.assetid: ''
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 2/17/2017
ms.author: asgang
ms.openlocfilehash: ef30457e0183e8dffce32919ea3c324ca4929cc4
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563340"
---
# <a name="replicate-applications"></a><span data-ttu-id="eca17-103">Replicate applications</span><span class="sxs-lookup"><span data-stu-id="eca17-103">Replicate applications</span></span>


<span data-ttu-id="eca17-104">This article describes how to set up replication of virtual machines running on VMware into Azure.</span><span class="sxs-lookup"><span data-stu-id="eca17-104">This article describes how to set up replication of virtual machines running on VMware into Azure.</span></span>
## <a name="prerequisites"></a><span data-ttu-id="eca17-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="eca17-105">Prerequisites</span></span>

<span data-ttu-id="eca17-106">The article assumes that you have already</span><span class="sxs-lookup"><span data-stu-id="eca17-106">The article assumes that you have already</span></span>

1.  [<span data-ttu-id="eca17-107">Setup on-premise source environment</span><span class="sxs-lookup"><span data-stu-id="eca17-107">Setup on-premise source environment</span></span>](site-recovery-set-up-vmware-to-azure.md)
2.  [<span data-ttu-id="eca17-108">Setup target environment in Azure</span><span class="sxs-lookup"><span data-stu-id="eca17-108">Setup target environment in Azure</span></span>](site-recovery-prepare-target-vmware-to-azure.md)


## <a name="enable-replication"></a><span data-ttu-id="eca17-109">Enable replication</span><span class="sxs-lookup"><span data-stu-id="eca17-109">Enable replication</span></span>
#### <a name="before-you-start"></a><span data-ttu-id="eca17-110">Before you start</span><span class="sxs-lookup"><span data-stu-id="eca17-110">Before you start</span></span>
<span data-ttu-id="eca17-111">If you're replicating VMware virtual machines, note that:</span><span class="sxs-lookup"><span data-stu-id="eca17-111">If you're replicating VMware virtual machines, note that:</span></span>

* <span data-ttu-id="eca17-112">VMware VMs are discovered every 15 minutes.</span><span class="sxs-lookup"><span data-stu-id="eca17-112">VMware VMs are discovered every 15 minutes.</span></span> <span data-ttu-id="eca17-113">It might take 15 minutes or longer for them to appear in the portal after discovery.</span><span class="sxs-lookup"><span data-stu-id="eca17-113">It might take 15 minutes or longer for them to appear in the portal after discovery.</span></span> <span data-ttu-id="eca17-114">Likewise discovery can take 15 minutes or more when you add a new vCenter server or vSphere host.</span><span class="sxs-lookup"><span data-stu-id="eca17-114">Likewise discovery can take 15 minutes or more when you add a new vCenter server or vSphere host.</span></span>
* <span data-ttu-id="eca17-115">Environment changes on the virtual machine (such as VMware tools installation) can take 15 minutes or more to be updated in the portal.</span><span class="sxs-lookup"><span data-stu-id="eca17-115">Environment changes on the virtual machine (such as VMware tools installation) can take 15 minutes or more to be updated in the portal.</span></span>
* <span data-ttu-id="eca17-116">You can check the last discovered time for VMware VMs in the **Last Contact At** field for the vCenter server/vSphere host, on the **Configuration Servers** blade.</span><span class="sxs-lookup"><span data-stu-id="eca17-116">You can check the last discovered time for VMware VMs in the **Last Contact At** field for the vCenter server/vSphere host, on the **Configuration Servers** blade.</span></span>
* <span data-ttu-id="eca17-117">To add machines for replication without waiting for the scheduled discovery, highlight the configuration server (don’t click it), and click the **Refresh** button.</span><span class="sxs-lookup"><span data-stu-id="eca17-117">To add machines for replication without waiting for the scheduled discovery, highlight the configuration server (don’t click it), and click the **Refresh** button.</span></span>
* <span data-ttu-id="eca17-118">When you enable replication, if the machine is prepared, the process server automatically installs the Mobility service on it.</span><span class="sxs-lookup"><span data-stu-id="eca17-118">When you enable replication, if the machine is prepared, the process server automatically installs the Mobility service on it.</span></span>


<span data-ttu-id="eca17-119">**Now enable replication as follows**:</span><span class="sxs-lookup"><span data-stu-id="eca17-119">**Now enable replication as follows**:</span></span>

1. <span data-ttu-id="eca17-120">Click **Step 2: Replicate application** > **Source**.</span><span class="sxs-lookup"><span data-stu-id="eca17-120">Click **Step 2: Replicate application** > **Source**.</span></span> <span data-ttu-id="eca17-121">After you've enabled replication for the first time, click **+Replicate** in the vault to enable replication for additional machines.</span><span class="sxs-lookup"><span data-stu-id="eca17-121">After you've enabled replication for the first time, click **+Replicate** in the vault to enable replication for additional machines.</span></span>
2. <span data-ttu-id="eca17-122">In the **Source** blade > **Source**, select the configuration server.</span><span class="sxs-lookup"><span data-stu-id="eca17-122">In the **Source** blade > **Source**, select the configuration server.</span></span>
3. <span data-ttu-id="eca17-123">In **Machine type**, select **Virtual Machines** or **Physical Machines**.</span><span class="sxs-lookup"><span data-stu-id="eca17-123">In **Machine type**, select **Virtual Machines** or **Physical Machines**.</span></span>
4. <span data-ttu-id="eca17-124">In **vCenter/vSphere Hypervisor**, select the vCenter server that manages the vSphere host, or select the host.</span><span class="sxs-lookup"><span data-stu-id="eca17-124">In **vCenter/vSphere Hypervisor**, select the vCenter server that manages the vSphere host, or select the host.</span></span> <span data-ttu-id="eca17-125">This setting isn't relevant if you're replicating physical machines.</span><span class="sxs-lookup"><span data-stu-id="eca17-125">This setting isn't relevant if you're replicating physical machines.</span></span>
5. <span data-ttu-id="eca17-126">Select the process server.</span><span class="sxs-lookup"><span data-stu-id="eca17-126">Select the process server.</span></span> <span data-ttu-id="eca17-127">If you haven't created any additional process servers this will be the name of the configuration server.</span><span class="sxs-lookup"><span data-stu-id="eca17-127">If you haven't created any additional process servers this will be the name of the configuration server.</span></span> <span data-ttu-id="eca17-128">Then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="eca17-128">Then click **OK**.</span></span>

    ![Enable replication](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-vmware-to-azure/enable-replication2.png)

6. <span data-ttu-id="eca17-130">In **Target** select the subscription and the resource group where you want to create the failed over virtual machines.</span><span class="sxs-lookup"><span data-stu-id="eca17-130">In **Target** select the subscription and the resource group where you want to create the failed over virtual machines.</span></span> <span data-ttu-id="eca17-131">Choose the deployment model that you want to use in Azure (classic or resource management) for the failed over virtual machines.</span><span class="sxs-lookup"><span data-stu-id="eca17-131">Choose the deployment model that you want to use in Azure (classic or resource management) for the failed over virtual machines.</span></span>


7. <span data-ttu-id="eca17-132">Select the Azure storage account you want to use for replicating data.</span><span class="sxs-lookup"><span data-stu-id="eca17-132">Select the Azure storage account you want to use for replicating data.</span></span> <span data-ttu-id="eca17-133">Note that:</span><span class="sxs-lookup"><span data-stu-id="eca17-133">Note that:</span></span>

   * <span data-ttu-id="eca17-134">You can select a premium or standard storage account.</span><span class="sxs-lookup"><span data-stu-id="eca17-134">You can select a premium or standard storage account.</span></span> <span data-ttu-id="eca17-135">If you select a premium account, you'll need to specify an additional standard storage account for ongoing replication logs.</span><span class="sxs-lookup"><span data-stu-id="eca17-135">If you select a premium account, you'll need to specify an additional standard storage account for ongoing replication logs.</span></span> <span data-ttu-id="eca17-136">Accounts must be in the same region as the Recovery Services vault.</span><span class="sxs-lookup"><span data-stu-id="eca17-136">Accounts must be in the same region as the Recovery Services vault.</span></span>
   * <span data-ttu-id="eca17-137">If you want to use a different storage account than those you have, you can create one*PLaceholder LInk for creating storage account using resource manager which will be covered in getting started*.</span><span class="sxs-lookup"><span data-stu-id="eca17-137">If you want to use a different storage account than those you have, you can create one*PLaceholder LInk for creating storage account using resource manager which will be covered in getting started*.</span></span> <span data-ttu-id="eca17-138">To create a storage account using Resource Manager, click **Create new**.</span><span class="sxs-lookup"><span data-stu-id="eca17-138">To create a storage account using Resource Manager, click **Create new**.</span></span> <span data-ttu-id="eca17-139">If you want to create a storage account using the classic model, you do that [in the Azure portal](../storage/storage-create-storage-account-classic-portal.md).</span><span class="sxs-lookup"><span data-stu-id="eca17-139">If you want to create a storage account using the classic model, you do that [in the Azure portal](../storage/storage-create-storage-account-classic-portal.md).</span></span>


8. <span data-ttu-id="eca17-140">Select the Azure network and subnet to which Azure VMs will connect, when they're spun up after failover.</span><span class="sxs-lookup"><span data-stu-id="eca17-140">Select the Azure network and subnet to which Azure VMs will connect, when they're spun up after failover.</span></span> <span data-ttu-id="eca17-141">The network must be in the same region as the Recovery Services vault.</span><span class="sxs-lookup"><span data-stu-id="eca17-141">The network must be in the same region as the Recovery Services vault.</span></span> <span data-ttu-id="eca17-142">Select **Configure now for selected machines**, to apply the network setting to all machines you select for protection.</span><span class="sxs-lookup"><span data-stu-id="eca17-142">Select **Configure now for selected machines**, to apply the network setting to all machines you select for protection.</span></span> <span data-ttu-id="eca17-143">Select **Configure later** to select the Azure network per machine.</span><span class="sxs-lookup"><span data-stu-id="eca17-143">Select **Configure later** to select the Azure network per machine.</span></span> <span data-ttu-id="eca17-144">If you don't have a network, you need to [create one](#set-up-an-azure-network).</span><span class="sxs-lookup"><span data-stu-id="eca17-144">If you don't have a network, you need to [create one](#set-up-an-azure-network).</span></span> <span data-ttu-id="eca17-145">To create a network using Resource Manager, click **Create new**.</span><span class="sxs-lookup"><span data-stu-id="eca17-145">To create a network using Resource Manager, click **Create new**.</span></span> <span data-ttu-id="eca17-146">If you want to create a network using the classic model, do that [in the Azure portal](../virtual-network/virtual-networks-create-vnet-classic-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="eca17-146">If you want to create a network using the classic model, do that [in the Azure portal](../virtual-network/virtual-networks-create-vnet-classic-pportal.md).</span></span> <span data-ttu-id="eca17-147">Select a subnet if applicable.</span><span class="sxs-lookup"><span data-stu-id="eca17-147">Select a subnet if applicable.</span></span> <span data-ttu-id="eca17-148">Then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="eca17-148">Then click **OK**.</span></span>

    ![Enable replication](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-vmware-to-azure/enable-rep3.png)
9. <span data-ttu-id="eca17-150">In **Virtual Machines** > **Select virtual machines**, click and select each machine you want to replicate.</span><span class="sxs-lookup"><span data-stu-id="eca17-150">In **Virtual Machines** > **Select virtual machines**, click and select each machine you want to replicate.</span></span> <span data-ttu-id="eca17-151">You can only select machines for which replication can be enabled.</span><span class="sxs-lookup"><span data-stu-id="eca17-151">You can only select machines for which replication can be enabled.</span></span> <span data-ttu-id="eca17-152">Then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="eca17-152">Then click **OK**.</span></span>

    ![Enable replication](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-vmware-to-azure/enable-replication5.png)
10. <span data-ttu-id="eca17-154">In **Properties** > **Configure properties**, select the account that will be used by the process server to automatically install the Mobility service on the machine.</span><span class="sxs-lookup"><span data-stu-id="eca17-154">In **Properties** > **Configure properties**, select the account that will be used by the process server to automatically install the Mobility service on the machine.</span></span> <span data-ttu-id="eca17-155">By default all disks are replicated.</span><span class="sxs-lookup"><span data-stu-id="eca17-155">By default all disks are replicated.</span></span> <span data-ttu-id="eca17-156">Click **All Disks** and clear any disks you don't want to replicate.</span><span class="sxs-lookup"><span data-stu-id="eca17-156">Click **All Disks** and clear any disks you don't want to replicate.</span></span> <span data-ttu-id="eca17-157">Then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="eca17-157">Then click **OK**.</span></span> <span data-ttu-id="eca17-158">You can set additional properties later.</span><span class="sxs-lookup"><span data-stu-id="eca17-158">You can set additional properties later.</span></span>

    ![Enable replication](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-vmware-to-azure/enable-replication6.png)


> [!NOTE]
> <span data-ttu-id="eca17-160">By default all disks on a machine are replicated.</span><span class="sxs-lookup"><span data-stu-id="eca17-160">By default all disks on a machine are replicated.</span></span> <span data-ttu-id="eca17-161">You can [exclude disks from replication](site-recovery-exclude-disk.md).</span><span class="sxs-lookup"><span data-stu-id="eca17-161">You can [exclude disks from replication](site-recovery-exclude-disk.md).</span></span> <span data-ttu-id="eca17-162">For example you might not want to replicate disks with temporary data, or data that's refreshed each time a machine or application restarts (for example pagefile.sys or SQL Server tempdb).</span><span class="sxs-lookup"><span data-stu-id="eca17-162">For example you might not want to replicate disks with temporary data, or data that's refreshed each time a machine or application restarts (for example pagefile.sys or SQL Server tempdb).</span></span>
>



11. <span data-ttu-id="eca17-163">In **Replication settings** > **Configure replication settings**, verify that the correct replication policy is selected.</span><span class="sxs-lookup"><span data-stu-id="eca17-163">In **Replication settings** > **Configure replication settings**, verify that the correct replication policy is selected.</span></span> <span data-ttu-id="eca17-164">You can modify replication policy settings in **Settings** > **Replication policies** > policy name > **Edit Settings**.</span><span class="sxs-lookup"><span data-stu-id="eca17-164">You can modify replication policy settings in **Settings** > **Replication policies** > policy name > **Edit Settings**.</span></span> <span data-ttu-id="eca17-165">Changes you apply to a policy will be applied to replicating and new machines.</span><span class="sxs-lookup"><span data-stu-id="eca17-165">Changes you apply to a policy will be applied to replicating and new machines.</span></span>
12. <span data-ttu-id="eca17-166">Enable **Multi-VM consistency** if you want to gather machines into a replication group, and specify a name for the group.</span><span class="sxs-lookup"><span data-stu-id="eca17-166">Enable **Multi-VM consistency** if you want to gather machines into a replication group, and specify a name for the group.</span></span> <span data-ttu-id="eca17-167">Then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="eca17-167">Then click **OK**.</span></span> <span data-ttu-id="eca17-168">Note that:</span><span class="sxs-lookup"><span data-stu-id="eca17-168">Note that:</span></span>

    * <span data-ttu-id="eca17-169">Machines in replication group replicate together and have shared crash-consistent and app-consistent recovery points when they fail over.</span><span class="sxs-lookup"><span data-stu-id="eca17-169">Machines in replication group replicate together and have shared crash-consistent and app-consistent recovery points when they fail over.</span></span>
    * <span data-ttu-id="eca17-170">We recommend that you gather VMs and physical servers together so that they mirror your workloads.</span><span class="sxs-lookup"><span data-stu-id="eca17-170">We recommend that you gather VMs and physical servers together so that they mirror your workloads.</span></span> <span data-ttu-id="eca17-171">Enabling multi-VM consistency can impact workload performance and should only be used if machines are running the same workload and you need consistency.</span><span class="sxs-lookup"><span data-stu-id="eca17-171">Enabling multi-VM consistency can impact workload performance and should only be used if machines are running the same workload and you need consistency.</span></span>

    ![Enable replication](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-vmware-to-azure/enable-replication7.png)
13. <span data-ttu-id="eca17-173">Click **Enable Replication**.</span><span class="sxs-lookup"><span data-stu-id="eca17-173">Click **Enable Replication**.</span></span> <span data-ttu-id="eca17-174">You can track progress of the **Enable Protection** job in **Settings** > **Jobs** > **Site Recovery Jobs**.</span><span class="sxs-lookup"><span data-stu-id="eca17-174">You can track progress of the **Enable Protection** job in **Settings** > **Jobs** > **Site Recovery Jobs**.</span></span> <span data-ttu-id="eca17-175">After the **Finalize Protection** job runs the machine is ready for failover.</span><span class="sxs-lookup"><span data-stu-id="eca17-175">After the **Finalize Protection** job runs the machine is ready for failover.</span></span>

> [!NOTE]
> <span data-ttu-id="eca17-176">If the machine is prepared for push installation the Mobility service component will be installed when protection is enabled.</span><span class="sxs-lookup"><span data-stu-id="eca17-176">If the machine is prepared for push installation the Mobility service component will be installed when protection is enabled.</span></span> <span data-ttu-id="eca17-177">After the component is installed on the machine a protection job starts and fails.</span><span class="sxs-lookup"><span data-stu-id="eca17-177">After the component is installed on the machine a protection job starts and fails.</span></span> <span data-ttu-id="eca17-178">After the failure you need to manually restart each machine.</span><span class="sxs-lookup"><span data-stu-id="eca17-178">After the failure you need to manually restart each machine.</span></span> <span data-ttu-id="eca17-179">After the restart the protection job begins again and initial replication occurs.</span><span class="sxs-lookup"><span data-stu-id="eca17-179">After the restart the protection job begins again and initial replication occurs.</span></span>
>
>

## <a name="view-and-manage-vm-properties"></a><span data-ttu-id="eca17-180">View and manage VM properties</span><span class="sxs-lookup"><span data-stu-id="eca17-180">View and manage VM properties</span></span>
<span data-ttu-id="eca17-181">We recommend that you verify the properties of the source machine.</span><span class="sxs-lookup"><span data-stu-id="eca17-181">We recommend that you verify the properties of the source machine.</span></span> <span data-ttu-id="eca17-182">Remember that the Azure VM name should conform with [Azure virtual machine requirements](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="eca17-182">Remember that the Azure VM name should conform with [Azure virtual machine requirements](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>

1. <span data-ttu-id="eca17-183">Click **Settings** > **Replicated items** >, and select the machine.</span><span class="sxs-lookup"><span data-stu-id="eca17-183">Click **Settings** > **Replicated items** >, and select the machine.</span></span> <span data-ttu-id="eca17-184">The **Essentials** blade shows information about machines settings and status.</span><span class="sxs-lookup"><span data-stu-id="eca17-184">The **Essentials** blade shows information about machines settings and status.</span></span>
2. <span data-ttu-id="eca17-185">In **Properties**, you can view replication and failover information for the VM.</span><span class="sxs-lookup"><span data-stu-id="eca17-185">In **Properties**, you can view replication and failover information for the VM.</span></span>
3. <span data-ttu-id="eca17-186">In **Compute and Network** > **Compute properties**, you can specify the Azure VM name and target size.</span><span class="sxs-lookup"><span data-stu-id="eca17-186">In **Compute and Network** > **Compute properties**, you can specify the Azure VM name and target size.</span></span> <span data-ttu-id="eca17-187">Modify the name to comply with Azure requirements if you need to.</span><span class="sxs-lookup"><span data-stu-id="eca17-187">Modify the name to comply with Azure requirements if you need to.</span></span>
<span data-ttu-id="eca17-188">![Enable replication](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-vmware-to-azure/VMProperties_AVSET.PNG)</span><span class="sxs-lookup"><span data-stu-id="eca17-188">![Enable replication](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-vmware-to-azure/VMProperties_AVSET.PNG)</span></span>

<span data-ttu-id="eca17-189">*Resource Group*</span><span class="sxs-lookup"><span data-stu-id="eca17-189">*Resource Group*</span></span>
   
  * <span data-ttu-id="eca17-190">You can select a [resource group](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-resource-groups-guidelines) of which machine will become part of  post fail over.</span><span class="sxs-lookup"><span data-stu-id="eca17-190">You can select a [resource group](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-resource-groups-guidelines) of which machine will become part of  post fail over.</span></span> <span data-ttu-id="eca17-191">You can change this setting any time before fail over.</span><span class="sxs-lookup"><span data-stu-id="eca17-191">You can change this setting any time before fail over.</span></span> 
  
> [!NOTE]
> <span data-ttu-id="eca17-192">Post fail over, if you migrate the machine to a different resource group then protection settings of a machine will break.</span><span class="sxs-lookup"><span data-stu-id="eca17-192">Post fail over, if you migrate the machine to a different resource group then protection settings of a machine will break.</span></span>
 
<span data-ttu-id="eca17-193">*Availability Sets*</span><span class="sxs-lookup"><span data-stu-id="eca17-193">*Availability Sets*</span></span>

<span data-ttu-id="eca17-194">You can select an [availability set](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines) if your machine required to be be a part of one post fail over.</span><span class="sxs-lookup"><span data-stu-id="eca17-194">You can select an [availability set](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines) if your machine required to be be a part of one post fail over.</span></span> <span data-ttu-id="eca17-195">While selecting availability set, please keep in mind that:</span><span class="sxs-lookup"><span data-stu-id="eca17-195">While selecting availability set, please keep in mind that:</span></span>

* <span data-ttu-id="eca17-196">Only availability sets belonging to the specified resource group will be listed</span><span class="sxs-lookup"><span data-stu-id="eca17-196">Only availability sets belonging to the specified resource group will be listed</span></span>  
* <span data-ttu-id="eca17-197">Machines with different virtual networks cannot be a part of same availability set</span><span class="sxs-lookup"><span data-stu-id="eca17-197">Machines with different virtual networks cannot be a part of same availability set</span></span> 
* <span data-ttu-id="eca17-198">Only virtual machines of same size can be a part of same availability set</span><span class="sxs-lookup"><span data-stu-id="eca17-198">Only virtual machines of same size can be a part of same availability set</span></span> 

<span data-ttu-id="eca17-199">*Network Properties*</span><span class="sxs-lookup"><span data-stu-id="eca17-199">*Network Properties*</span></span>

<span data-ttu-id="eca17-200">You can also view and add information about the target network, subnet, and IP address that will be assigned to the Azure VM.</span><span class="sxs-lookup"><span data-stu-id="eca17-200">You can also view and add information about the target network, subnet, and IP address that will be assigned to the Azure VM.</span></span> <span data-ttu-id="eca17-201">Note the following:</span><span class="sxs-lookup"><span data-stu-id="eca17-201">Note the following:</span></span>

   * <span data-ttu-id="eca17-202">You can set the target IP address.</span><span class="sxs-lookup"><span data-stu-id="eca17-202">You can set the target IP address.</span></span> <span data-ttu-id="eca17-203">If you don't provide an address, the failed over machine will use DHCP.</span><span class="sxs-lookup"><span data-stu-id="eca17-203">If you don't provide an address, the failed over machine will use DHCP.</span></span> <span data-ttu-id="eca17-204">If you set an address that isn't available at failover, the failover won't work.</span><span class="sxs-lookup"><span data-stu-id="eca17-204">If you set an address that isn't available at failover, the failover won't work.</span></span> <span data-ttu-id="eca17-205">The same target IP address can be used for test failover if the address is available in the test failover network.</span><span class="sxs-lookup"><span data-stu-id="eca17-205">The same target IP address can be used for test failover if the address is available in the test failover network.</span></span>
   * <span data-ttu-id="eca17-206">The number of network adapters is dictated by the size you specify for the target virtual machine, as follows:</span><span class="sxs-lookup"><span data-stu-id="eca17-206">The number of network adapters is dictated by the size you specify for the target virtual machine, as follows:</span></span>

     * <span data-ttu-id="eca17-207">If the number of network adapters on the source machine is less than or equal to the number of adapters allowed for the target machine size, then the target will have the same number of adapters as the source.</span><span class="sxs-lookup"><span data-stu-id="eca17-207">If the number of network adapters on the source machine is less than or equal to the number of adapters allowed for the target machine size, then the target will have the same number of adapters as the source.</span></span>
     * <span data-ttu-id="eca17-208">If the number of adapters for the source virtual machine exceeds the number allowed for the target size then the target size maximum will be used.</span><span class="sxs-lookup"><span data-stu-id="eca17-208">If the number of adapters for the source virtual machine exceeds the number allowed for the target size then the target size maximum will be used.</span></span>
     * <span data-ttu-id="eca17-209">For example if a source machine has two network adapters and the target machine size supports four, the target machine will have two adapters.</span><span class="sxs-lookup"><span data-stu-id="eca17-209">For example if a source machine has two network adapters and the target machine size supports four, the target machine will have two adapters.</span></span> <span data-ttu-id="eca17-210">If the source machine has two adapters but the supported target size only supports one then the target machine will have only one adapter.</span><span class="sxs-lookup"><span data-stu-id="eca17-210">If the source machine has two adapters but the supported target size only supports one then the target machine will have only one adapter.</span></span>     
   * <span data-ttu-id="eca17-211">If the virtual machine has multiple network adapters they will all connect to the same network.</span><span class="sxs-lookup"><span data-stu-id="eca17-211">If the virtual machine has multiple network adapters they will all connect to the same network.</span></span>
   * <span data-ttu-id="eca17-212">If the virtual machine has multiple network adapters then the first one shown in the list becomes the *Default* network adapter in the Azure virtual machine.</span><span class="sxs-lookup"><span data-stu-id="eca17-212">If the virtual machine has multiple network adapters then the first one shown in the list becomes the *Default* network adapter in the Azure virtual machine.</span></span>

4. <span data-ttu-id="eca17-213">In **Disks**, you can see the operating system and data disks on the VM that will be replicated.</span><span class="sxs-lookup"><span data-stu-id="eca17-213">In **Disks**, you can see the operating system and data disks on the VM that will be replicated.</span></span>


## <a name="common-issues"></a><span data-ttu-id="eca17-214">Common issues</span><span class="sxs-lookup"><span data-stu-id="eca17-214">Common issues</span></span>

* <span data-ttu-id="eca17-215">Each disk should be less than 1TB in size.</span><span class="sxs-lookup"><span data-stu-id="eca17-215">Each disk should be less than 1TB in size.</span></span>
* <span data-ttu-id="eca17-216">The OS disk should be a basic disk and not dynamic disk</span><span class="sxs-lookup"><span data-stu-id="eca17-216">The OS disk should be a basic disk and not dynamic disk</span></span>
* <span data-ttu-id="eca17-217">For generation 2/UEFI enabled virtual machines, the operating system family should be Windows and boot disk should be less than 300GB</span><span class="sxs-lookup"><span data-stu-id="eca17-217">For generation 2/UEFI enabled virtual machines, the operating system family should be Windows and boot disk should be less than 300GB</span></span>

## <a name="next-steps"></a><span data-ttu-id="eca17-218">Next steps</span><span class="sxs-lookup"><span data-stu-id="eca17-218">Next steps</span></span>

<span data-ttu-id="eca17-219">Once the protection is completed, you can try [fail over](site-recovery-failover.md) to check whether your application comes up in Azure or not.</span><span class="sxs-lookup"><span data-stu-id="eca17-219">Once the protection is completed, you can try [fail over](site-recovery-failover.md) to check whether your application comes up in Azure or not.</span></span>

<span data-ttu-id="eca17-220">In case you want to disable protection, check how to [clean registration and protection settings](site-recovery-manage-registration-and-protection.md)</span><span class="sxs-lookup"><span data-stu-id="eca17-220">In case you want to disable protection, check how to [clean registration and protection settings](site-recovery-manage-registration-and-protection.md)</span></span>





