---
title: Back up Azure virtual machines at scale
description: Simultaneously back up multiple virtual machines to Azure
services: backup
keywords: virtual machine backup; virtual machine back up; back up vm; backup vm; backup Azure vm; backup and disaster recovery
author: markgalioto
ms.author: markgal
ms.date: 2/14/2018
ms.topic: tutorial
ms.service: backup
ms.custom: mvc
ms.openlocfilehash: ecbf583a9b64868004b246bb01e7f174a21496b0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966312"
---
# <a name="use-azure-portal-to-back-up-multiple-virtual-machines"></a><span data-ttu-id="d62d4-104">Use Azure portal to back up multiple virtual machines</span><span class="sxs-lookup"><span data-stu-id="d62d4-104">Use Azure portal to back up multiple virtual machines</span></span>

<span data-ttu-id="d62d4-105">When you back up data in Azure, you store that data in an Azure resource called a Recovery Services vault.</span><span class="sxs-lookup"><span data-stu-id="d62d4-105">When you back up data in Azure, you store that data in an Azure resource called a Recovery Services vault.</span></span> <span data-ttu-id="d62d4-106">The Recovery Services vault resource is available from the Settings menu of most Azure services.</span><span class="sxs-lookup"><span data-stu-id="d62d4-106">The Recovery Services vault resource is available from the Settings menu of most Azure services.</span></span> <span data-ttu-id="d62d4-107">The benefit of having the Recovery Services vault integrated into the Settings menu of most Azure services makes it very easy to back up data.</span><span class="sxs-lookup"><span data-stu-id="d62d4-107">The benefit of having the Recovery Services vault integrated into the Settings menu of most Azure services makes it very easy to back up data.</span></span> <span data-ttu-id="d62d4-108">However, individually working with each database or virtual machine in your business is tedious.</span><span class="sxs-lookup"><span data-stu-id="d62d4-108">However, individually working with each database or virtual machine in your business is tedious.</span></span> <span data-ttu-id="d62d4-109">What if you want to back up the data for all virtual machines in one department, or in one location?</span><span class="sxs-lookup"><span data-stu-id="d62d4-109">What if you want to back up the data for all virtual machines in one department, or in one location?</span></span> <span data-ttu-id="d62d4-110">It is easy to back up multiple virtual machines by creating a backup policy and applying that policy to the desired virtual machines.</span><span class="sxs-lookup"><span data-stu-id="d62d4-110">It is easy to back up multiple virtual machines by creating a backup policy and applying that policy to the desired virtual machines.</span></span> <span data-ttu-id="d62d4-111">This tutorial explains how to:</span><span class="sxs-lookup"><span data-stu-id="d62d4-111">This tutorial explains how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d62d4-112">Create a Recovery Services vault</span><span class="sxs-lookup"><span data-stu-id="d62d4-112">Create a Recovery Services vault</span></span>
> * <span data-ttu-id="d62d4-113">Define a backup policy</span><span class="sxs-lookup"><span data-stu-id="d62d4-113">Define a backup policy</span></span>
> * <span data-ttu-id="d62d4-114">Apply the backup policy to protect multiple virtual machines</span><span class="sxs-lookup"><span data-stu-id="d62d4-114">Apply the backup policy to protect multiple virtual machines</span></span>
> * <span data-ttu-id="d62d4-115">Trigger an on-demand backup job for the protected virtual machines</span><span class="sxs-lookup"><span data-stu-id="d62d4-115">Trigger an on-demand backup job for the protected virtual machines</span></span>

## <a name="log-in-to-the-azure-portal"></a><span data-ttu-id="d62d4-116">Log in to the Azure portal</span><span class="sxs-lookup"><span data-stu-id="d62d4-116">Log in to the Azure portal</span></span>

<span data-ttu-id="d62d4-117">Log in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="d62d4-117">Log in to the [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="d62d4-118">Create a Recovery Services vault</span><span class="sxs-lookup"><span data-stu-id="d62d4-118">Create a Recovery Services vault</span></span>

<span data-ttu-id="d62d4-119">The Recovery Services vault contains the backup data, and the backup policy applied to the protected virtual machines.</span><span class="sxs-lookup"><span data-stu-id="d62d4-119">The Recovery Services vault contains the backup data, and the backup policy applied to the protected virtual machines.</span></span> <span data-ttu-id="d62d4-120">Backing up virtual machines is a local process.</span><span class="sxs-lookup"><span data-stu-id="d62d4-120">Backing up virtual machines is a local process.</span></span> <span data-ttu-id="d62d4-121">You cannot back up a virtual machine from one location to a Recovery Services vault in another location.</span><span class="sxs-lookup"><span data-stu-id="d62d4-121">You cannot back up a virtual machine from one location to a Recovery Services vault in another location.</span></span> <span data-ttu-id="d62d4-122">So, for each Azure location that has virtual machines to be backed up, at least one Recovery Services vault must exist in that location.</span><span class="sxs-lookup"><span data-stu-id="d62d4-122">So, for each Azure location that has virtual machines to be backed up, at least one Recovery Services vault must exist in that location.</span></span>

1. <span data-ttu-id="d62d4-123">On the left-hand menu, select **All services** and in the services list, type *Recovery Services*.</span><span class="sxs-lookup"><span data-stu-id="d62d4-123">On the left-hand menu, select **All services** and in the services list, type *Recovery Services*.</span></span> <span data-ttu-id="d62d4-124">As you type, the list of resources filters.</span><span class="sxs-lookup"><span data-stu-id="d62d4-124">As you type, the list of resources filters.</span></span> <span data-ttu-id="d62d4-125">When you see Recovery Services vaults in the list, select it to open the Recovery Services vaults menu.</span><span class="sxs-lookup"><span data-stu-id="d62d4-125">When you see Recovery Services vaults in the list, select it to open the Recovery Services vaults menu.</span></span>

    ![Open Recovery Services Vault menu](./media/tutorial-backup-vm-at-scale/full-browser-open-rs-vault.png) <br/>

2. <span data-ttu-id="d62d4-127">In the **Recovery Services vaults** menu, click **Add** to open the Recovery Services vault menu.</span><span class="sxs-lookup"><span data-stu-id="d62d4-127">In the **Recovery Services vaults** menu, click **Add** to open the Recovery Services vault menu.</span></span>

    ![Open vault menu](./media/tutorial-backup-vm-at-scale/provide-vault-detail-2.png)

3. <span data-ttu-id="d62d4-129">In the Recovery Services vault menu,</span><span class="sxs-lookup"><span data-stu-id="d62d4-129">In the Recovery Services vault menu,</span></span> 

    - <span data-ttu-id="d62d4-130">Type *myRecoveryServicesVault* in **Name**,</span><span class="sxs-lookup"><span data-stu-id="d62d4-130">Type *myRecoveryServicesVault* in **Name**,</span></span>
    - <span data-ttu-id="d62d4-131">The current subscription ID appears in **Subscription**.</span><span class="sxs-lookup"><span data-stu-id="d62d4-131">The current subscription ID appears in **Subscription**.</span></span> <span data-ttu-id="d62d4-132">If you have additional subscriptions, you could choose another subscription for the new vault.</span><span class="sxs-lookup"><span data-stu-id="d62d4-132">If you have additional subscriptions, you could choose another subscription for the new vault.</span></span>
    - <span data-ttu-id="d62d4-133">For **Resource group** select **Use existing** and choose *myResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="d62d4-133">For **Resource group** select **Use existing** and choose *myResourceGroup*.</span></span> <span data-ttu-id="d62d4-134">If *myResourceGroup* doesn't exist, select **Create new** and type *myResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="d62d4-134">If *myResourceGroup* doesn't exist, select **Create new** and type *myResourceGroup*.</span></span>
    - <span data-ttu-id="d62d4-135">From the **Location** drop-down menu, choose *West Europe*.</span><span class="sxs-lookup"><span data-stu-id="d62d4-135">From the **Location** drop-down menu, choose *West Europe*.</span></span>
    - <span data-ttu-id="d62d4-136">Click **Create** to create your Recovery Services vault.</span><span class="sxs-lookup"><span data-stu-id="d62d4-136">Click **Create** to create your Recovery Services vault.</span></span>

<span data-ttu-id="d62d4-137">A Recovery Services vault must be in the same location as the virtual machines being protected.</span><span class="sxs-lookup"><span data-stu-id="d62d4-137">A Recovery Services vault must be in the same location as the virtual machines being protected.</span></span> <span data-ttu-id="d62d4-138">If you have virtual machines in multiple regions,create a Recovery Services vault in each region.</span><span class="sxs-lookup"><span data-stu-id="d62d4-138">If you have virtual machines in multiple regions,create a Recovery Services vault in each region.</span></span> <span data-ttu-id="d62d4-139">This tutorial creates a Recovery Services vault in *West Europe* because that is where *myVM* (the virtual machine created with the quickstart) was created.</span><span class="sxs-lookup"><span data-stu-id="d62d4-139">This tutorial creates a Recovery Services vault in *West Europe* because that is where *myVM* (the virtual machine created with the quickstart) was created.</span></span>

<span data-ttu-id="d62d4-140">It can take several minutes for the Recovery Services vault to be created.</span><span class="sxs-lookup"><span data-stu-id="d62d4-140">It can take several minutes for the Recovery Services vault to be created.</span></span> <span data-ttu-id="d62d4-141">Monitor the status notifications in the upper right-hand area of the portal.</span><span class="sxs-lookup"><span data-stu-id="d62d4-141">Monitor the status notifications in the upper right-hand area of the portal.</span></span> <span data-ttu-id="d62d4-142">Once your vault is created, it appears in the list of Recovery Services vaults.</span><span class="sxs-lookup"><span data-stu-id="d62d4-142">Once your vault is created, it appears in the list of Recovery Services vaults.</span></span>

<span data-ttu-id="d62d4-143">When you create a Recovery Services vault, by default the vault has geo-redundant storage.</span><span class="sxs-lookup"><span data-stu-id="d62d4-143">When you create a Recovery Services vault, by default the vault has geo-redundant storage.</span></span> <span data-ttu-id="d62d4-144">To provide data resiliency, geo-redundant storage replicates the data multiple times across two Azure regions.</span><span class="sxs-lookup"><span data-stu-id="d62d4-144">To provide data resiliency, geo-redundant storage replicates the data multiple times across two Azure regions.</span></span>

## <a name="set-backup-policy-to-protect-vms"></a><span data-ttu-id="d62d4-145">Set backup policy to protect VMs</span><span class="sxs-lookup"><span data-stu-id="d62d4-145">Set backup policy to protect VMs</span></span>

<span data-ttu-id="d62d4-146">After creating the Recovery Services vault, the next step is to configure the vault for the type of data, and to set the backup policy.</span><span class="sxs-lookup"><span data-stu-id="d62d4-146">After creating the Recovery Services vault, the next step is to configure the vault for the type of data, and to set the backup policy.</span></span> <span data-ttu-id="d62d4-147">Backup policy is the schedule for how often and when recovery points are taken.</span><span class="sxs-lookup"><span data-stu-id="d62d4-147">Backup policy is the schedule for how often and when recovery points are taken.</span></span> <span data-ttu-id="d62d4-148">Policy also includes the retention range for the recovery points.</span><span class="sxs-lookup"><span data-stu-id="d62d4-148">Policy also includes the retention range for the recovery points.</span></span> <span data-ttu-id="d62d4-149">For this tutorial let's assume your business is a sports complex with a hotel, stadium, and restaurants and concessions, and you are protecting the data on the virtual machines.</span><span class="sxs-lookup"><span data-stu-id="d62d4-149">For this tutorial let's assume your business is a sports complex with a hotel, stadium, and restaurants and concessions, and you are protecting the data on the virtual machines.</span></span> <span data-ttu-id="d62d4-150">The following steps create a backup policy for the financial data.</span><span class="sxs-lookup"><span data-stu-id="d62d4-150">The following steps create a backup policy for the financial data.</span></span>

1. <span data-ttu-id="d62d4-151">From the list of Recovery Services vaults, select **myRecoveryServicesVault** to open its dashboard.</span><span class="sxs-lookup"><span data-stu-id="d62d4-151">From the list of Recovery Services vaults, select **myRecoveryServicesVault** to open its dashboard.</span></span>

   ![Open Scenario menu](./media/tutorial-backup-vm-at-scale/open-vault-from-list.png)

2. <span data-ttu-id="d62d4-153">On the vault dashboard menu, click **Backup** to open the Backup menu.</span><span class="sxs-lookup"><span data-stu-id="d62d4-153">On the vault dashboard menu, click **Backup** to open the Backup menu.</span></span>

3. <span data-ttu-id="d62d4-154">On the Backup Goal menu, in the **Where is your workload running** drop-down menu, choose *Azure*.</span><span class="sxs-lookup"><span data-stu-id="d62d4-154">On the Backup Goal menu, in the **Where is your workload running** drop-down menu, choose *Azure*.</span></span> <span data-ttu-id="d62d4-155">From the **What do you want to backup** drop-down, choose *Virtual machine*, and click **Backup**.</span><span class="sxs-lookup"><span data-stu-id="d62d4-155">From the **What do you want to backup** drop-down, choose *Virtual machine*, and click **Backup**.</span></span>

    <span data-ttu-id="d62d4-156">These actions prepare the Recovery Services vault for interacting with a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="d62d4-156">These actions prepare the Recovery Services vault for interacting with a virtual machine.</span></span> <span data-ttu-id="d62d4-157">Recovery Services vaults have a default policy that creates a restore point each day, and retains the restore points for 30 days.</span><span class="sxs-lookup"><span data-stu-id="d62d4-157">Recovery Services vaults have a default policy that creates a restore point each day, and retains the restore points for 30 days.</span></span>

    ![Open Scenario menu](./media/tutorial-backup-vm-at-scale/backup-goal.png)

4. <span data-ttu-id="d62d4-159">To create a new policy, on the Backup policy menu, from the **Choose backup policy** drop-down menu, select *Create New*.</span><span class="sxs-lookup"><span data-stu-id="d62d4-159">To create a new policy, on the Backup policy menu, from the **Choose backup policy** drop-down menu, select *Create New*.</span></span>

    ![Select workload](./media/tutorial-backup-vm-at-scale/create-new-policy.png)

5. <span data-ttu-id="d62d4-161">In the **Backup policy** menu, for **Policy Name** type *Finance*.</span><span class="sxs-lookup"><span data-stu-id="d62d4-161">In the **Backup policy** menu, for **Policy Name** type *Finance*.</span></span> <span data-ttu-id="d62d4-162">Enter the following changes for the Backup policy:</span><span class="sxs-lookup"><span data-stu-id="d62d4-162">Enter the following changes for the Backup policy:</span></span> 
    - <span data-ttu-id="d62d4-163">For **Backup frequency** set the timezone for *Central Time*.</span><span class="sxs-lookup"><span data-stu-id="d62d4-163">For **Backup frequency** set the timezone for *Central Time*.</span></span> <span data-ttu-id="d62d4-164">Since the sports complex is in Texas, the owner wants the timing to be local.</span><span class="sxs-lookup"><span data-stu-id="d62d4-164">Since the sports complex is in Texas, the owner wants the timing to be local.</span></span> <span data-ttu-id="d62d4-165">Leave the backup frequency set to Daily at 3:30AM.</span><span class="sxs-lookup"><span data-stu-id="d62d4-165">Leave the backup frequency set to Daily at 3:30AM.</span></span>
    - <span data-ttu-id="d62d4-166">For **Retention of daily backup point**, set the period to 90 days.</span><span class="sxs-lookup"><span data-stu-id="d62d4-166">For **Retention of daily backup point**, set the period to 90 days.</span></span>
    - <span data-ttu-id="d62d4-167">For **Retention of weekly backup point**, use the *Monday* restore point and retain it for 52 weeks.</span><span class="sxs-lookup"><span data-stu-id="d62d4-167">For **Retention of weekly backup point**, use the *Monday* restore point and retain it for 52 weeks.</span></span>
    - <span data-ttu-id="d62d4-168">For **Retention of monthly backup point**, use the restore point from First Sunday of the month, and retain it for 36 months.</span><span class="sxs-lookup"><span data-stu-id="d62d4-168">For **Retention of monthly backup point**, use the restore point from First Sunday of the month, and retain it for 36 months.</span></span>
    - <span data-ttu-id="d62d4-169">Deselect the **Retention of yearly backup point** option.</span><span class="sxs-lookup"><span data-stu-id="d62d4-169">Deselect the **Retention of yearly backup point** option.</span></span> <span data-ttu-id="d62d4-170">The leader of Finance doesn't want to keep data longer than 36 months.</span><span class="sxs-lookup"><span data-stu-id="d62d4-170">The leader of Finance doesn't want to keep data longer than 36 months.</span></span>
    - <span data-ttu-id="d62d4-171">Click **OK** to create the backup policy.</span><span class="sxs-lookup"><span data-stu-id="d62d4-171">Click **OK** to create the backup policy.</span></span>

    ![Select workload](./media/tutorial-backup-vm-at-scale/set-new-policy.png) 

    <span data-ttu-id="d62d4-173">After creating the backup policy, associate the policy with the virtual machines.</span><span class="sxs-lookup"><span data-stu-id="d62d4-173">After creating the backup policy, associate the policy with the virtual machines.</span></span>

6. <span data-ttu-id="d62d4-174">In the **Select virtual machines** dialog select *myVM* and click **OK** to deploy the backup policy to the virtual machines.</span><span class="sxs-lookup"><span data-stu-id="d62d4-174">In the **Select virtual machines** dialog select *myVM* and click **OK** to deploy the backup policy to the virtual machines.</span></span> 

    <span data-ttu-id="d62d4-175">All virtual machines that are in the same location, and are not already associated with a backup policy, appear.</span><span class="sxs-lookup"><span data-stu-id="d62d4-175">All virtual machines that are in the same location, and are not already associated with a backup policy, appear.</span></span> <span data-ttu-id="d62d4-176">*myVMH1* and *myVMR1* are selected to be associated with the *Finance* policy.</span><span class="sxs-lookup"><span data-stu-id="d62d4-176">*myVMH1* and *myVMR1* are selected to be associated with the *Finance* policy.</span></span>

    ![Select workload](./media/tutorial-backup-vm-at-scale/choose-vm-to-protect.png) 

    <span data-ttu-id="d62d4-178">When the deployment completes, you receive a notification that deployment successfully completed.</span><span class="sxs-lookup"><span data-stu-id="d62d4-178">When the deployment completes, you receive a notification that deployment successfully completed.</span></span>

## <a name="initial-backup"></a><span data-ttu-id="d62d4-179">Initial backup</span><span class="sxs-lookup"><span data-stu-id="d62d4-179">Initial backup</span></span>

<span data-ttu-id="d62d4-180">You have enabled backup for the Recovery Services vaults, but an initial backup has not been created.</span><span class="sxs-lookup"><span data-stu-id="d62d4-180">You have enabled backup for the Recovery Services vaults, but an initial backup has not been created.</span></span> <span data-ttu-id="d62d4-181">It is a disaster recovery best practice to trigger the first backup, so that your data is protected.</span><span class="sxs-lookup"><span data-stu-id="d62d4-181">It is a disaster recovery best practice to trigger the first backup, so that your data is protected.</span></span> 

<span data-ttu-id="d62d4-182">To run an on-demand backup job:</span><span class="sxs-lookup"><span data-stu-id="d62d4-182">To run an on-demand backup job:</span></span>

1. <span data-ttu-id="d62d4-183">On the vault dashboard, click **3** under **Backup Items**, to open the Backup Items menu.</span><span class="sxs-lookup"><span data-stu-id="d62d4-183">On the vault dashboard, click **3** under **Backup Items**, to open the Backup Items menu.</span></span>

    ![Settings icon](./media/tutorial-backup-vm-at-scale/tutorial-vm-back-up-now.png)

    <span data-ttu-id="d62d4-185">The **Backup Items** menu opens.</span><span class="sxs-lookup"><span data-stu-id="d62d4-185">The **Backup Items** menu opens.</span></span>

2. <span data-ttu-id="d62d4-186">On the **Backup Items** menu, click **Azure Virtual Machine** to open the list of virtual machines associated with the vault.</span><span class="sxs-lookup"><span data-stu-id="d62d4-186">On the **Backup Items** menu, click **Azure Virtual Machine** to open the list of virtual machines associated with the vault.</span></span>

    ![Settings icon](./media/tutorial-backup-vm-at-scale/three-virtual-machines.png)

    <span data-ttu-id="d62d4-188">The **Backup Items** list opens.</span><span class="sxs-lookup"><span data-stu-id="d62d4-188">The **Backup Items** list opens.</span></span>

    ![Backup job triggered](./media/tutorial-backup-vm-at-scale/initial-backup-context-menu.png)

3. <span data-ttu-id="d62d4-190">On the **Backup Items** list, click the ellipses **...** to open the Context menu.</span><span class="sxs-lookup"><span data-stu-id="d62d4-190">On the **Backup Items** list, click the ellipses **...** to open the Context menu.</span></span>

4. <span data-ttu-id="d62d4-191">On the Context menu, select **Backup now**.</span><span class="sxs-lookup"><span data-stu-id="d62d4-191">On the Context menu, select **Backup now**.</span></span>

    ![Context menu](./media/tutorial-backup-vm-at-scale/context-menu.png)

    <span data-ttu-id="d62d4-193">The Backup Now menu opens.</span><span class="sxs-lookup"><span data-stu-id="d62d4-193">The Backup Now menu opens.</span></span>

5. <span data-ttu-id="d62d4-194">On the Backup Now menu, enter the last day to retain the recovery point, and click **Backup**.</span><span class="sxs-lookup"><span data-stu-id="d62d4-194">On the Backup Now menu, enter the last day to retain the recovery point, and click **Backup**.</span></span>

    ![set the last day the Backup Now recovery point is retained](./media/tutorial-backup-vm-at-scale/backup-now-short.png)

    <span data-ttu-id="d62d4-196">Deployment notifications let you know the backup job has been triggered, and that you can monitor the progress of the job on the Backup jobs page.</span><span class="sxs-lookup"><span data-stu-id="d62d4-196">Deployment notifications let you know the backup job has been triggered, and that you can monitor the progress of the job on the Backup jobs page.</span></span> <span data-ttu-id="d62d4-197">Depending on the size of your virtual machine, creating the initial backup may take a while.</span><span class="sxs-lookup"><span data-stu-id="d62d4-197">Depending on the size of your virtual machine, creating the initial backup may take a while.</span></span>

    <span data-ttu-id="d62d4-198">When the initial backup job completes, you can see its status in the Backup job menu.</span><span class="sxs-lookup"><span data-stu-id="d62d4-198">When the initial backup job completes, you can see its status in the Backup job menu.</span></span> <span data-ttu-id="d62d4-199">The on-demand backup job created the initial restore point for *myVM*.</span><span class="sxs-lookup"><span data-stu-id="d62d4-199">The on-demand backup job created the initial restore point for *myVM*.</span></span> <span data-ttu-id="d62d4-200">If you want to back up other virtual machines, repeat these steps for each virtual machine.</span><span class="sxs-lookup"><span data-stu-id="d62d4-200">If you want to back up other virtual machines, repeat these steps for each virtual machine.</span></span> 

    ![Backup Jobs tile](./media/tutorial-backup-vm-at-scale/initial-backup-complete.png)
  
## <a name="clean-up-resources"></a><span data-ttu-id="d62d4-202">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="d62d4-202">Clean up resources</span></span>

<span data-ttu-id="d62d4-203">If you plan to continue on to work with subsequent tutorials, do not clean up the resources created in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="d62d4-203">If you plan to continue on to work with subsequent tutorials, do not clean up the resources created in this tutorial.</span></span> <span data-ttu-id="d62d4-204">If you do not plan to continue, use the following steps to delete all resources created by this tutorial in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="d62d4-204">If you do not plan to continue, use the following steps to delete all resources created by this tutorial in the Azure portal.</span></span>

1. <span data-ttu-id="d62d4-205">On the **myRecoveryServicesVault** dashboard, click **3** under **Backup Items**, to open the Backup Items menu.</span><span class="sxs-lookup"><span data-stu-id="d62d4-205">On the **myRecoveryServicesVault** dashboard, click **3** under **Backup Items**, to open the Backup Items menu.</span></span>

    ![Settings icon](./media/tutorial-backup-vm-at-scale/tutorial-vm-back-up-now.png)


2. <span data-ttu-id="d62d4-207">On the **Backup Items** menu, click **Azure Virtual Machine** to open the list of virtual machines associated with the vault.</span><span class="sxs-lookup"><span data-stu-id="d62d4-207">On the **Backup Items** menu, click **Azure Virtual Machine** to open the list of virtual machines associated with the vault.</span></span>

    ![Settings icon](./media/tutorial-backup-vm-at-scale/three-virtual-machines.png)

    <span data-ttu-id="d62d4-209">The **Backup Items** list opens.</span><span class="sxs-lookup"><span data-stu-id="d62d4-209">The **Backup Items** list opens.</span></span>

3. <span data-ttu-id="d62d4-210">In the **Backup Items** menu, click the ellipsis to open the Context menu.</span><span class="sxs-lookup"><span data-stu-id="d62d4-210">In the **Backup Items** menu, click the ellipsis to open the Context menu.</span></span>

    ![Settings icon](./media/tutorial-backup-vm-at-scale/context-menu-to-delete-vm.png)

4. <span data-ttu-id="d62d4-212">On the context menu select **Stop backup** to open Stop Backup menu.</span><span class="sxs-lookup"><span data-stu-id="d62d4-212">On the context menu select **Stop backup** to open Stop Backup menu.</span></span> 

    ![Settings icon](./media/tutorial-backup-vm-at-scale/context-menu-for-delete.png)

5. <span data-ttu-id="d62d4-214">In the **Stop Backup** menu, select the upper drop-down menu and choose **Delete Backup Data**.</span><span class="sxs-lookup"><span data-stu-id="d62d4-214">In the **Stop Backup** menu, select the upper drop-down menu and choose **Delete Backup Data**.</span></span>

6. <span data-ttu-id="d62d4-215">In the **Type the name of the Backup item** dialog, type *myVM*.</span><span class="sxs-lookup"><span data-stu-id="d62d4-215">In the **Type the name of the Backup item** dialog, type *myVM*.</span></span>
 
7. <span data-ttu-id="d62d4-216">Once the backup item is verified (a checkmark appears), **Stop backup** button is enabled.</span><span class="sxs-lookup"><span data-stu-id="d62d4-216">Once the backup item is verified (a checkmark appears), **Stop backup** button is enabled.</span></span> <span data-ttu-id="d62d4-217">Click **Stop Backup** to stop the policy and delete the restore points.</span><span class="sxs-lookup"><span data-stu-id="d62d4-217">Click **Stop Backup** to stop the policy and delete the restore points.</span></span> 

    ![click Stop backup to delete vault](./media/tutorial-backup-vm-at-scale/provide-reason-for-delete.png)<span data-ttu-id="d62d4-219">.</span><span class="sxs-lookup"><span data-stu-id="d62d4-219">.</span></span>

8. <span data-ttu-id="d62d4-220">In the **myRecoveryServicesVault** menu, click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="d62d4-220">In the **myRecoveryServicesVault** menu, click **Delete**.</span></span>

    ![click Stop backup to delete vault](./media/tutorial-backup-vm-at-scale/deleting-the-vault.png)

    <span data-ttu-id="d62d4-222">Once the vault is deleted, you return to the list of Recovery Services vaults.</span><span class="sxs-lookup"><span data-stu-id="d62d4-222">Once the vault is deleted, you return to the list of Recovery Services vaults.</span></span>


## <a name="next-steps"></a><span data-ttu-id="d62d4-223">Next steps</span><span class="sxs-lookup"><span data-stu-id="d62d4-223">Next steps</span></span>

<span data-ttu-id="d62d4-224">In this tutorial you used the Azure portal to:</span><span class="sxs-lookup"><span data-stu-id="d62d4-224">In this tutorial you used the Azure portal to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d62d4-225">Create a Recovery Services vault</span><span class="sxs-lookup"><span data-stu-id="d62d4-225">Create a Recovery Services vault</span></span>
> * <span data-ttu-id="d62d4-226">Set the vault to protect virtual machines</span><span class="sxs-lookup"><span data-stu-id="d62d4-226">Set the vault to protect virtual machines</span></span>
> * <span data-ttu-id="d62d4-227">Create a custom backup and retention policy</span><span class="sxs-lookup"><span data-stu-id="d62d4-227">Create a custom backup and retention policy</span></span>
> * <span data-ttu-id="d62d4-228">Assign the policy to protect multiple virtual machines</span><span class="sxs-lookup"><span data-stu-id="d62d4-228">Assign the policy to protect multiple virtual machines</span></span>
> * <span data-ttu-id="d62d4-229">Trigger an on-demand back up for virtual machines</span><span class="sxs-lookup"><span data-stu-id="d62d4-229">Trigger an on-demand back up for virtual machines</span></span>

<span data-ttu-id="d62d4-230">Continue to the next tutorial to restore an Azure virtual machine from disk.</span><span class="sxs-lookup"><span data-stu-id="d62d4-230">Continue to the next tutorial to restore an Azure virtual machine from disk.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="d62d4-231">Restore VMs using CLI</span><span class="sxs-lookup"><span data-stu-id="d62d4-231">Restore VMs using CLI</span></span>](./tutorial-restore-disk.md)
