---
title: Azure Quickstart - Back up a VM with the Azure portal
description: Learn how to back up your virtual machines with the Azure portal
services: backup
author: saurabhsensharma
manager: shivamg
tags: azure-resource-manager, virtual-machine-backup
ms.service: backup
ms.devlang: azurecli
ms.topic: quickstart
ms.date: 7/17/2018
ms.author: saurse
ms.custom: mvc
ms.openlocfilehash: 9d2578e10916d3770e73ab88e4d0e63aea3fe420
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857472"
---
# <a name="back-up-a-virtual-machine-in-azure"></a><span data-ttu-id="9a36d-103">Back up a virtual machine in Azure</span><span class="sxs-lookup"><span data-stu-id="9a36d-103">Back up a virtual machine in Azure</span></span>
<span data-ttu-id="9a36d-104">Azure backups can be created through the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="9a36d-104">Azure backups can be created through the Azure portal.</span></span> <span data-ttu-id="9a36d-105">This method provides a browser-based user interface to create and configure Azure backups and all related resources.</span><span class="sxs-lookup"><span data-stu-id="9a36d-105">This method provides a browser-based user interface to create and configure Azure backups and all related resources.</span></span> <span data-ttu-id="9a36d-106">You can protect your data by taking backups at regular intervals.</span><span class="sxs-lookup"><span data-stu-id="9a36d-106">You can protect your data by taking backups at regular intervals.</span></span> <span data-ttu-id="9a36d-107">Azure Backup creates recovery points that can be stored in geo-redundant recovery vaults.</span><span class="sxs-lookup"><span data-stu-id="9a36d-107">Azure Backup creates recovery points that can be stored in geo-redundant recovery vaults.</span></span> <span data-ttu-id="9a36d-108">This article details how to back up a virtual machine (VM) with the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="9a36d-108">This article details how to back up a virtual machine (VM) with the Azure portal.</span></span> 

<span data-ttu-id="9a36d-109">This quickstart enables backup on an existing Azure VM.</span><span class="sxs-lookup"><span data-stu-id="9a36d-109">This quickstart enables backup on an existing Azure VM.</span></span> <span data-ttu-id="9a36d-110">If you need to create a VM, you can [create a VM with the Azure portal](../virtual-machines/windows/quick-create-portal.md).</span><span class="sxs-lookup"><span data-stu-id="9a36d-110">If you need to create a VM, you can [create a VM with the Azure portal](../virtual-machines/windows/quick-create-portal.md).</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="9a36d-111">Log in to Azure</span><span class="sxs-lookup"><span data-stu-id="9a36d-111">Log in to Azure</span></span>

<span data-ttu-id="9a36d-112">Log in to the Azure portal at http://portal.azure.com.</span><span class="sxs-lookup"><span data-stu-id="9a36d-112">Log in to the Azure portal at http://portal.azure.com.</span></span>

## <a name="select-a-vm-to-back-up"></a><span data-ttu-id="9a36d-113">Select a VM to back up</span><span class="sxs-lookup"><span data-stu-id="9a36d-113">Select a VM to back up</span></span>
<span data-ttu-id="9a36d-114">Create a simple scheduled daily backup to a Recovery Services Vault.</span><span class="sxs-lookup"><span data-stu-id="9a36d-114">Create a simple scheduled daily backup to a Recovery Services Vault.</span></span> 

1. <span data-ttu-id="9a36d-115">In the menu on the left, select **Virtual machines**.</span><span class="sxs-lookup"><span data-stu-id="9a36d-115">In the menu on the left, select **Virtual machines**.</span></span> 
2. <span data-ttu-id="9a36d-116">From the list, choose a VM to back up.</span><span class="sxs-lookup"><span data-stu-id="9a36d-116">From the list, choose a VM to back up.</span></span> <span data-ttu-id="9a36d-117">If you used the sample VM quickstart commands, the VM is named *myVM* in the *myResourceGroup* resource group.</span><span class="sxs-lookup"><span data-stu-id="9a36d-117">If you used the sample VM quickstart commands, the VM is named *myVM* in the *myResourceGroup* resource group.</span></span>
3. <span data-ttu-id="9a36d-118">In the **Operations** section, choose **Backup**.</span><span class="sxs-lookup"><span data-stu-id="9a36d-118">In the **Operations** section, choose **Backup**.</span></span> <span data-ttu-id="9a36d-119">The **Enable backup** window opens.</span><span class="sxs-lookup"><span data-stu-id="9a36d-119">The **Enable backup** window opens.</span></span>


## <a name="enable-backup-on-a-vm"></a><span data-ttu-id="9a36d-120">Enable backup on a VM</span><span class="sxs-lookup"><span data-stu-id="9a36d-120">Enable backup on a VM</span></span>
<span data-ttu-id="9a36d-121">A Recovery Services vault is a logical container that stores the backup data for each protected resource, such as Azure VMs.</span><span class="sxs-lookup"><span data-stu-id="9a36d-121">A Recovery Services vault is a logical container that stores the backup data for each protected resource, such as Azure VMs.</span></span> <span data-ttu-id="9a36d-122">When the backup job for a protected resource runs, it creates a recovery point inside the Recovery Services vault.</span><span class="sxs-lookup"><span data-stu-id="9a36d-122">When the backup job for a protected resource runs, it creates a recovery point inside the Recovery Services vault.</span></span> <span data-ttu-id="9a36d-123">You can then use one of these recovery points to restore data to a given point in time.</span><span class="sxs-lookup"><span data-stu-id="9a36d-123">You can then use one of these recovery points to restore data to a given point in time.</span></span>

1. <span data-ttu-id="9a36d-124">Select **Create new** and provide a name for the new vault, such as *myRecoveryServicesVault*.</span><span class="sxs-lookup"><span data-stu-id="9a36d-124">Select **Create new** and provide a name for the new vault, such as *myRecoveryServicesVault*.</span></span>
2. <span data-ttu-id="9a36d-125">If not already selected, choose **Use existing**, then select the resource group of your VM from the drop-down menu.</span><span class="sxs-lookup"><span data-stu-id="9a36d-125">If not already selected, choose **Use existing**, then select the resource group of your VM from the drop-down menu.</span></span>

    ![Enable VM backup in the Azure portal](./media/quick-backup-vm-portal/enable-backup.png)

    <span data-ttu-id="9a36d-127">By default, the vault is set for Geo-Redundant storage.</span><span class="sxs-lookup"><span data-stu-id="9a36d-127">By default, the vault is set for Geo-Redundant storage.</span></span> <span data-ttu-id="9a36d-128">To further protect your data, this storage redundancy level ensures that your backup data is replicated to a secondary Azure region that is hundreds of miles away from the primary region.</span><span class="sxs-lookup"><span data-stu-id="9a36d-128">To further protect your data, this storage redundancy level ensures that your backup data is replicated to a secondary Azure region that is hundreds of miles away from the primary region.</span></span>

    <span data-ttu-id="9a36d-129">You create and use policies to define when a backup job runs and how long the recovery points are stored.</span><span class="sxs-lookup"><span data-stu-id="9a36d-129">You create and use policies to define when a backup job runs and how long the recovery points are stored.</span></span> <span data-ttu-id="9a36d-130">The default protection policy runs a backup job each day and retains recovery points for 30 days.</span><span class="sxs-lookup"><span data-stu-id="9a36d-130">The default protection policy runs a backup job each day and retains recovery points for 30 days.</span></span> <span data-ttu-id="9a36d-131">You can use these default policy values to quickly protect your VM.</span><span class="sxs-lookup"><span data-stu-id="9a36d-131">You can use these default policy values to quickly protect your VM.</span></span> 

3. <span data-ttu-id="9a36d-132">To accept the default backup policy values, select **Enable Backup**.</span><span class="sxs-lookup"><span data-stu-id="9a36d-132">To accept the default backup policy values, select **Enable Backup**.</span></span>

<span data-ttu-id="9a36d-133">It takes a few moments to create the Recovery Services vault.</span><span class="sxs-lookup"><span data-stu-id="9a36d-133">It takes a few moments to create the Recovery Services vault.</span></span>


## <a name="start-a-backup-job"></a><span data-ttu-id="9a36d-134">Start a backup job</span><span class="sxs-lookup"><span data-stu-id="9a36d-134">Start a backup job</span></span>
<span data-ttu-id="9a36d-135">You can start a backup now rather than wait for the default policy to run the job at the scheduled time.</span><span class="sxs-lookup"><span data-stu-id="9a36d-135">You can start a backup now rather than wait for the default policy to run the job at the scheduled time.</span></span> <span data-ttu-id="9a36d-136">This first backup job creates a full recovery point.</span><span class="sxs-lookup"><span data-stu-id="9a36d-136">This first backup job creates a full recovery point.</span></span> <span data-ttu-id="9a36d-137">Each backup job after this initial backup creates incremental recovery points.</span><span class="sxs-lookup"><span data-stu-id="9a36d-137">Each backup job after this initial backup creates incremental recovery points.</span></span> <span data-ttu-id="9a36d-138">Incremental recovery points are storage and time-efficient, as they only transfer changes made since the last backup.</span><span class="sxs-lookup"><span data-stu-id="9a36d-138">Incremental recovery points are storage and time-efficient, as they only transfer changes made since the last backup.</span></span>

1. <span data-ttu-id="9a36d-139">On the **Backup** window for your VM, select **Backup now**.</span><span class="sxs-lookup"><span data-stu-id="9a36d-139">On the **Backup** window for your VM, select **Backup now**.</span></span>

    ![Perform immediate VM backup in the Azure portal](./media/quick-backup-vm-portal/backup-now.png)

2. <span data-ttu-id="9a36d-141">To accept the backup retention policy of 30 days, leave the default **Retain Backup Till** date.</span><span class="sxs-lookup"><span data-stu-id="9a36d-141">To accept the backup retention policy of 30 days, leave the default **Retain Backup Till** date.</span></span> <span data-ttu-id="9a36d-142">To start the job, select **Backup**.</span><span class="sxs-lookup"><span data-stu-id="9a36d-142">To start the job, select **Backup**.</span></span>


## <a name="monitor-the-backup-job"></a><span data-ttu-id="9a36d-143">Monitor the backup job</span><span class="sxs-lookup"><span data-stu-id="9a36d-143">Monitor the backup job</span></span>
<span data-ttu-id="9a36d-144">In the **Backup** window for your VM, the status of the backup and number of completed restore points are shown.</span><span class="sxs-lookup"><span data-stu-id="9a36d-144">In the **Backup** window for your VM, the status of the backup and number of completed restore points are shown.</span></span> <span data-ttu-id="9a36d-145">Once the VM backup job is complete, information on the **Last backup time**, **Latest restore point**, and **Oldest restore point** is shown on the right-hand side of the **Overview** window.</span><span class="sxs-lookup"><span data-stu-id="9a36d-145">Once the VM backup job is complete, information on the **Last backup time**, **Latest restore point**, and **Oldest restore point** is shown on the right-hand side of the **Overview** window.</span></span>


## <a name="clean-up-deployment"></a><span data-ttu-id="9a36d-146">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="9a36d-146">Clean up deployment</span></span>
<span data-ttu-id="9a36d-147">When no longer needed, you can disable protection on the VM, remove the restore points and Recovery Services vault, then delete the resource group and associated VM resources</span><span class="sxs-lookup"><span data-stu-id="9a36d-147">When no longer needed, you can disable protection on the VM, remove the restore points and Recovery Services vault, then delete the resource group and associated VM resources</span></span>

<span data-ttu-id="9a36d-148">If you are going to continue on to a Backup tutorial that explains how to restore data for your VM, skip the steps in this section and go to [Next steps](#next-steps).</span><span class="sxs-lookup"><span data-stu-id="9a36d-148">If you are going to continue on to a Backup tutorial that explains how to restore data for your VM, skip the steps in this section and go to [Next steps](#next-steps).</span></span>

1. <span data-ttu-id="9a36d-149">Select the **Backup** option for your VM.</span><span class="sxs-lookup"><span data-stu-id="9a36d-149">Select the **Backup** option for your VM.</span></span>

2. <span data-ttu-id="9a36d-150">Select **...More** to show additional options, then choose **Stop backup**.</span><span class="sxs-lookup"><span data-stu-id="9a36d-150">Select **...More** to show additional options, then choose **Stop backup**.</span></span>

    ![Stop VM backup from the Azure portal](./media/quick-backup-vm-portal/stop-backup.png)

3. <span data-ttu-id="9a36d-152">Select **Delete Backup Data** from the drop-down menu.</span><span class="sxs-lookup"><span data-stu-id="9a36d-152">Select **Delete Backup Data** from the drop-down menu.</span></span>

4. <span data-ttu-id="9a36d-153">In the **Type the name of the Backup item** dialog, enter your VM name, such as *myVM*.</span><span class="sxs-lookup"><span data-stu-id="9a36d-153">In the **Type the name of the Backup item** dialog, enter your VM name, such as *myVM*.</span></span> <span data-ttu-id="9a36d-154">Select **Stop Backup**</span><span class="sxs-lookup"><span data-stu-id="9a36d-154">Select **Stop Backup**</span></span>

    <span data-ttu-id="9a36d-155">Once the VM backup has been stopped and recovery points removed, you can delete the resource group.</span><span class="sxs-lookup"><span data-stu-id="9a36d-155">Once the VM backup has been stopped and recovery points removed, you can delete the resource group.</span></span> <span data-ttu-id="9a36d-156">If you used an existing VM, you may wish to leave the resource group and VM in place.</span><span class="sxs-lookup"><span data-stu-id="9a36d-156">If you used an existing VM, you may wish to leave the resource group and VM in place.</span></span>

5. <span data-ttu-id="9a36d-157">In the menu on the left, select **Resource groups**.</span><span class="sxs-lookup"><span data-stu-id="9a36d-157">In the menu on the left, select **Resource groups**.</span></span> 
6. <span data-ttu-id="9a36d-158">From the list, choose your resource group.</span><span class="sxs-lookup"><span data-stu-id="9a36d-158">From the list, choose your resource group.</span></span> <span data-ttu-id="9a36d-159">If you used the sample VM quickstart commands, the resource group is named *myResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="9a36d-159">If you used the sample VM quickstart commands, the resource group is named *myResourceGroup*.</span></span>
7. <span data-ttu-id="9a36d-160">Select **Delete resource group**.</span><span class="sxs-lookup"><span data-stu-id="9a36d-160">Select **Delete resource group**.</span></span> <span data-ttu-id="9a36d-161">To confirm, enter the resource group name, then select **Delete**.</span><span class="sxs-lookup"><span data-stu-id="9a36d-161">To confirm, enter the resource group name, then select **Delete**.</span></span>

    ![Delete the resource group from the Azure portal](./media/quick-backup-vm-portal/delete-resource-group.png)


## <a name="next-steps"></a><span data-ttu-id="9a36d-163">Next steps</span><span class="sxs-lookup"><span data-stu-id="9a36d-163">Next steps</span></span>
<span data-ttu-id="9a36d-164">In this quickstart, you created a Recovery Services vault, enabled protection on a VM, and created the initial recovery point.</span><span class="sxs-lookup"><span data-stu-id="9a36d-164">In this quickstart, you created a Recovery Services vault, enabled protection on a VM, and created the initial recovery point.</span></span> <span data-ttu-id="9a36d-165">To learn more about Azure Backup and Recovery Services, continue to the tutorials.</span><span class="sxs-lookup"><span data-stu-id="9a36d-165">To learn more about Azure Backup and Recovery Services, continue to the tutorials.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9a36d-166">Back up multiple Azure VMs</span><span class="sxs-lookup"><span data-stu-id="9a36d-166">Back up multiple Azure VMs</span></span>](./tutorial-backup-vm-at-scale.md)
