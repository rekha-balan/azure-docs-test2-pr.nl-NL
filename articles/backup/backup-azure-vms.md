---
title: Back up classic-deployed Azure virtual machines to a backup vault| Microsoft Docs
description: Discover, register, and back up your virtual machines with these procedures for Azure virtual machine backup.
services: backup
documentationcenter: ''
author: markgalioto
manager: carmonm
editor: ''
keywords: virtual machine backup; back up virtual machine; backup and disaster recovery; vm backup
ms.assetid: c0ab5469-65fd-4af5-ae9b-f5d183f82ce8
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/15/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: f6f2ebace657f5e02d0c110a4be80d42091b8fde
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563673"
---
# <a name="back-up-azure-virtual-machines-classic-portal"></a><span data-ttu-id="ad1cc-104">Back up Azure virtual machines (classic portal)</span><span class="sxs-lookup"><span data-stu-id="ad1cc-104">Back up Azure virtual machines (classic portal)</span></span>
> [!div class="op_single_selector"]
> * [Back up VMs to Recovery Services vault](backup-azure-arm-vms.md)
> * [Back up VMs to Backup vault](backup-azure-vms.md)
>
>

<span data-ttu-id="ad1cc-107">This article provides the procedures for backing up a Classic-deployed Azure virtual machine (VM) to a Backup vault.</span><span class="sxs-lookup"><span data-stu-id="ad1cc-107">This article provides the procedures for backing up a Classic-deployed Azure virtual machine (VM) to a Backup vault.</span></span> <span data-ttu-id="ad1cc-108">There are a few tasks you need to take care of before you can back up an Azure virtual machine.</span><span class="sxs-lookup"><span data-stu-id="ad1cc-108">There are a few tasks you need to take care of before you can back up an Azure virtual machine.</span></span> <span data-ttu-id="ad1cc-109">If you haven't already done so, complete the [prerequisites](backup-azure-vms-prepare.md) to prepare your environment for backing up your VMs.</span><span class="sxs-lookup"><span data-stu-id="ad1cc-109">If you haven't already done so, complete the [prerequisites](backup-azure-vms-prepare.md) to prepare your environment for backing up your VMs.</span></span>

<span data-ttu-id="ad1cc-110">For additional information, see the articles on [planning your VM backup infrastructure in Azure](backup-azure-vms-introduction.md) and [Azure virtual machines](https://azure.microsoft.com/documentation/services/virtual-machines/).</span><span class="sxs-lookup"><span data-stu-id="ad1cc-110">For additional information, see the articles on [planning your VM backup infrastructure in Azure](backup-azure-vms-introduction.md) and [Azure virtual machines](https://azure.microsoft.com/documentation/services/virtual-machines/).</span></span>

> [!NOTE]
> Azure has two deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md). A Backup vault can only protect Classic-deployed VMs. You cannot protect Resource Manager-deployed VMs with a Backup vault. See [Back up VMs to Recovery Services vault](backup-azure-arm-vms.md) for details on working with Recovery Services vaults.
>
>

<span data-ttu-id="ad1cc-115">Backing up Azure virtual machines involves three key steps:</span><span class="sxs-lookup"><span data-stu-id="ad1cc-115">Backing up Azure virtual machines involves three key steps:</span></span>

![Three steps to back up an Azure IaaS VM](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms/3-steps-for-backup.png)

> [!NOTE]
> Backing up virtual machines is a local process. You cannot back up virtual machines in one region to a backup vault in another region. So, you must create a backup vault in each Azure region, where there are VMs that will be backed up.
>
>

## <a name="step-1---discover-azure-virtual-machines"></a><span data-ttu-id="ad1cc-120">Step 1 - Discover Azure virtual machines</span><span class="sxs-lookup"><span data-stu-id="ad1cc-120">Step 1 - Discover Azure virtual machines</span></span>
<span data-ttu-id="ad1cc-121">To ensure any new virtual machines (VMs) added to the subscription are identified before registering, run the discovery process.</span><span class="sxs-lookup"><span data-stu-id="ad1cc-121">To ensure any new virtual machines (VMs) added to the subscription are identified before registering, run the discovery process.</span></span> <span data-ttu-id="ad1cc-122">The process queries Azure for the list of virtual machines in the subscription, along with additional information like the cloud service name and the region.</span><span class="sxs-lookup"><span data-stu-id="ad1cc-122">The process queries Azure for the list of virtual machines in the subscription, along with additional information like the cloud service name and the region.</span></span>

1. <span data-ttu-id="ad1cc-123">Sign in to the [Classic portal](http://manage.windowsazure.com/)</span><span class="sxs-lookup"><span data-stu-id="ad1cc-123">Sign in to the [Classic portal](http://manage.windowsazure.com/)</span></span>
2. <span data-ttu-id="ad1cc-124">In the list of Azure services, click **Recovery Services** to open the list of Backup and Site Recovery vaults.</span><span class="sxs-lookup"><span data-stu-id="ad1cc-124">In the list of Azure services, click **Recovery Services** to open the list of Backup and Site Recovery vaults.</span></span>
    <span data-ttu-id="ad1cc-125">![Open vault list](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms/choose-vault-list.png)</span><span class="sxs-lookup"><span data-stu-id="ad1cc-125">![Open vault list](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms/choose-vault-list.png)</span></span>
3. <span data-ttu-id="ad1cc-126">In the list of Backup vaults, select the vault to back up a VM.</span><span class="sxs-lookup"><span data-stu-id="ad1cc-126">In the list of Backup vaults, select the vault to back up a VM.</span></span>

    <span data-ttu-id="ad1cc-127">If this is a new vault the portal opens to the **Quick Start** page.</span><span class="sxs-lookup"><span data-stu-id="ad1cc-127">If this is a new vault the portal opens to the **Quick Start** page.</span></span>

    ![Open Registered items menu](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms/vault-quick-start.png)

    <span data-ttu-id="ad1cc-129">If the vault has previously been configured, the portal opens to the most recently used menu.</span><span class="sxs-lookup"><span data-stu-id="ad1cc-129">If the vault has previously been configured, the portal opens to the most recently used menu.</span></span>
4. <span data-ttu-id="ad1cc-130">From the vault menu (at the top of the page), click **Registered Items**.</span><span class="sxs-lookup"><span data-stu-id="ad1cc-130">From the vault menu (at the top of the page), click **Registered Items**.</span></span>

    ![Open Registered items menu](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms/vault-menu.png)
5. <span data-ttu-id="ad1cc-132">From the **Type** menu, select **Azure Virtual Machine**.</span><span class="sxs-lookup"><span data-stu-id="ad1cc-132">From the **Type** menu, select **Azure Virtual Machine**.</span></span>

    ![Select workload](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms/discovery-select-workload.png)
6. <span data-ttu-id="ad1cc-134">Click **DISCOVER** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="ad1cc-134">Click **DISCOVER** at the bottom of the page.</span></span>
    <span data-ttu-id="ad1cc-135">![Discover button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms/discover-button-only.png)</span><span class="sxs-lookup"><span data-stu-id="ad1cc-135">![Discover button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms/discover-button-only.png)</span></span>

    <span data-ttu-id="ad1cc-136">The discovery process may take a few minutes while the virtual machines are being tabulated.</span><span class="sxs-lookup"><span data-stu-id="ad1cc-136">The discovery process may take a few minutes while the virtual machines are being tabulated.</span></span> <span data-ttu-id="ad1cc-137">There is a notification at the bottom of the screen that lets you know that the process is running.</span><span class="sxs-lookup"><span data-stu-id="ad1cc-137">There is a notification at the bottom of the screen that lets you know that the process is running.</span></span>

    ![Discover VMs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms/discovering-vms.png)

    <span data-ttu-id="ad1cc-139">The notification changes when the process is complete.</span><span class="sxs-lookup"><span data-stu-id="ad1cc-139">The notification changes when the process is complete.</span></span> <span data-ttu-id="ad1cc-140">If the discovery process did not find the virtual machines, first ensure the VMs exist.</span><span class="sxs-lookup"><span data-stu-id="ad1cc-140">If the discovery process did not find the virtual machines, first ensure the VMs exist.</span></span> <span data-ttu-id="ad1cc-141">If the VMs exist, ensure the VMs are in the same region as the backup vault.</span><span class="sxs-lookup"><span data-stu-id="ad1cc-141">If the VMs exist, ensure the VMs are in the same region as the backup vault.</span></span> <span data-ttu-id="ad1cc-142">If the VMs exist and are in the same region, ensure the VMs are not already registered to a backup vault.</span><span class="sxs-lookup"><span data-stu-id="ad1cc-142">If the VMs exist and are in the same region, ensure the VMs are not already registered to a backup vault.</span></span> <span data-ttu-id="ad1cc-143">If a VM is assigned to a backup vault it is not available to be assigned to other backup vaults.</span><span class="sxs-lookup"><span data-stu-id="ad1cc-143">If a VM is assigned to a backup vault it is not available to be assigned to other backup vaults.</span></span>

    ![Discovery done](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms/discovery-complete.png)

    <span data-ttu-id="ad1cc-145">Once you have discovered the new items, go to Step 2 and register your VMs.</span><span class="sxs-lookup"><span data-stu-id="ad1cc-145">Once you have discovered the new items, go to Step 2 and register your VMs.</span></span>

## <a name="step-2---register-azure-virtual-machines"></a><span data-ttu-id="ad1cc-146">Step 2 - Register Azure virtual machines</span><span class="sxs-lookup"><span data-stu-id="ad1cc-146">Step 2 - Register Azure virtual machines</span></span>
<span data-ttu-id="ad1cc-147">You register an Azure virtual machine to associate it with the Azure Backup service.</span><span class="sxs-lookup"><span data-stu-id="ad1cc-147">You register an Azure virtual machine to associate it with the Azure Backup service.</span></span> <span data-ttu-id="ad1cc-148">This is typically a one-time activity.</span><span class="sxs-lookup"><span data-stu-id="ad1cc-148">This is typically a one-time activity.</span></span>

1. <span data-ttu-id="ad1cc-149">Navigate to the backup vault under **Recovery Services** in the Azure portal, and then click **Registered Items**.</span><span class="sxs-lookup"><span data-stu-id="ad1cc-149">Navigate to the backup vault under **Recovery Services** in the Azure portal, and then click **Registered Items**.</span></span>
2. <span data-ttu-id="ad1cc-150">Select **Azure Virtual Machine** from the drop-down menu.</span><span class="sxs-lookup"><span data-stu-id="ad1cc-150">Select **Azure Virtual Machine** from the drop-down menu.</span></span>

    ![Select workload](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms/discovery-select-workload.png)
3. <span data-ttu-id="ad1cc-152">Click **REGISTER** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="ad1cc-152">Click **REGISTER** at the bottom of the page.</span></span>
    <span data-ttu-id="ad1cc-153">![Register button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms/register-button-only.png)</span><span class="sxs-lookup"><span data-stu-id="ad1cc-153">![Register button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms/register-button-only.png)</span></span>
4. <span data-ttu-id="ad1cc-154">In the **Register Items** shortcut menu, select the virtual machines that you want to register.</span><span class="sxs-lookup"><span data-stu-id="ad1cc-154">In the **Register Items** shortcut menu, select the virtual machines that you want to register.</span></span> <span data-ttu-id="ad1cc-155">If there are two or more virtual machines with the same name, use the cloud service to distinguish between them.</span><span class="sxs-lookup"><span data-stu-id="ad1cc-155">If there are two or more virtual machines with the same name, use the cloud service to distinguish between them.</span></span>

   > [!TIP]
   > Multiple virtual machines can be registered at one time.
   >
   >

    <span data-ttu-id="ad1cc-157">A job is created for each virtual machine that you've selected.</span><span class="sxs-lookup"><span data-stu-id="ad1cc-157">A job is created for each virtual machine that you've selected.</span></span>
5. <span data-ttu-id="ad1cc-158">Click **View Job** in the notification to go to the **Jobs** page.</span><span class="sxs-lookup"><span data-stu-id="ad1cc-158">Click **View Job** in the notification to go to the **Jobs** page.</span></span>

    ![Register job](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms/register-create-job.png)

    <span data-ttu-id="ad1cc-160">The virtual machine also appears in the list of registered items, along with the status of the registration operation.</span><span class="sxs-lookup"><span data-stu-id="ad1cc-160">The virtual machine also appears in the list of registered items, along with the status of the registration operation.</span></span>

    ![Registering status 1](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms/register-status01.png)

    <span data-ttu-id="ad1cc-162">When the operation completes, the status changes to reflect the *registered* state.</span><span class="sxs-lookup"><span data-stu-id="ad1cc-162">When the operation completes, the status changes to reflect the *registered* state.</span></span>

    ![Registration status 2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms/register-status02.png)

## <a name="step-3---protect-azure-virtual-machines"></a><span data-ttu-id="ad1cc-164">Step 3 - Protect Azure virtual machines</span><span class="sxs-lookup"><span data-stu-id="ad1cc-164">Step 3 - Protect Azure virtual machines</span></span>
<span data-ttu-id="ad1cc-165">Now you can set up a backup and retention policy for the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="ad1cc-165">Now you can set up a backup and retention policy for the virtual machine.</span></span> <span data-ttu-id="ad1cc-166">Multiple virtual machines can be protected by using a single protect action.</span><span class="sxs-lookup"><span data-stu-id="ad1cc-166">Multiple virtual machines can be protected by using a single protect action.</span></span>

<span data-ttu-id="ad1cc-167">Azure Backup vaults created after May 2015 come with a default policy built into the vault.</span><span class="sxs-lookup"><span data-stu-id="ad1cc-167">Azure Backup vaults created after May 2015 come with a default policy built into the vault.</span></span> <span data-ttu-id="ad1cc-168">This default policy comes with a default retention of 30 days and a once-daily backup schedule.</span><span class="sxs-lookup"><span data-stu-id="ad1cc-168">This default policy comes with a default retention of 30 days and a once-daily backup schedule.</span></span>

1. <span data-ttu-id="ad1cc-169">Navigate to the backup vault under **Recovery Services** in the Azure portal, and then click **Registered Items**.</span><span class="sxs-lookup"><span data-stu-id="ad1cc-169">Navigate to the backup vault under **Recovery Services** in the Azure portal, and then click **Registered Items**.</span></span>
2. <span data-ttu-id="ad1cc-170">Select **Azure Virtual Machine** from the drop-down menu.</span><span class="sxs-lookup"><span data-stu-id="ad1cc-170">Select **Azure Virtual Machine** from the drop-down menu.</span></span>

    ![Select workload in portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms/select-workload.png)
3. <span data-ttu-id="ad1cc-172">Click **PROTECT** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="ad1cc-172">Click **PROTECT** at the bottom of the page.</span></span>

    <span data-ttu-id="ad1cc-173">The **Protect Items wizard** appears.</span><span class="sxs-lookup"><span data-stu-id="ad1cc-173">The **Protect Items wizard** appears.</span></span> <span data-ttu-id="ad1cc-174">The wizard only lists virtual machines that are registered and not protected.</span><span class="sxs-lookup"><span data-stu-id="ad1cc-174">The wizard only lists virtual machines that are registered and not protected.</span></span> <span data-ttu-id="ad1cc-175">Select the virtual machines that you want to protect.</span><span class="sxs-lookup"><span data-stu-id="ad1cc-175">Select the virtual machines that you want to protect.</span></span>

    <span data-ttu-id="ad1cc-176">If there are two or more virtual machines with the same name, use the cloud service to distinguish between the virtual machines.</span><span class="sxs-lookup"><span data-stu-id="ad1cc-176">If there are two or more virtual machines with the same name, use the cloud service to distinguish between the virtual machines.</span></span>

   > [!TIP]
   > You can protect multiple virtual machines at one time.
   >
   >

    ![Configure protection at scale](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms/protect-at-scale.png)

4. <span data-ttu-id="ad1cc-179">Choose a **backup schedule** to back up the virtual machines that you've selected.</span><span class="sxs-lookup"><span data-stu-id="ad1cc-179">Choose a **backup schedule** to back up the virtual machines that you've selected.</span></span> <span data-ttu-id="ad1cc-180">You can pick from an existing set of policies or define a new one.</span><span class="sxs-lookup"><span data-stu-id="ad1cc-180">You can pick from an existing set of policies or define a new one.</span></span>

    <span data-ttu-id="ad1cc-181">Each backup policy can have multiple virtual machines associated with it.</span><span class="sxs-lookup"><span data-stu-id="ad1cc-181">Each backup policy can have multiple virtual machines associated with it.</span></span> <span data-ttu-id="ad1cc-182">However, the virtual machine can only be associated with one policy at any given point in time.</span><span class="sxs-lookup"><span data-stu-id="ad1cc-182">However, the virtual machine can only be associated with one policy at any given point in time.</span></span>

    ![Protect with new policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms/policy-schedule.png)

   > [!NOTE]
   > A backup policy includes a retention scheme for the scheduled backups. If you select an existing backup policy, you cannot modify the retention options in the next step.
   >
   >

5. <span data-ttu-id="ad1cc-186">Choose a **retention range** to associate with the backups.</span><span class="sxs-lookup"><span data-stu-id="ad1cc-186">Choose a **retention range** to associate with the backups.</span></span>

    ![Protect with flexible retention](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms/policy-retention.png)

    <span data-ttu-id="ad1cc-188">Retention policy specifies the length of time for storing a backup.</span><span class="sxs-lookup"><span data-stu-id="ad1cc-188">Retention policy specifies the length of time for storing a backup.</span></span> <span data-ttu-id="ad1cc-189">You can specify different retention policies based on when the backup is taken.</span><span class="sxs-lookup"><span data-stu-id="ad1cc-189">You can specify different retention policies based on when the backup is taken.</span></span> <span data-ttu-id="ad1cc-190">For example, a backup point taken daily (which serves as an operational recovery point) might be preserved for 90 days.</span><span class="sxs-lookup"><span data-stu-id="ad1cc-190">For example, a backup point taken daily (which serves as an operational recovery point) might be preserved for 90 days.</span></span> <span data-ttu-id="ad1cc-191">In comparison, a backup point taken at the end of each quarter (for audit purposes) may need to be preserved for many months or years.</span><span class="sxs-lookup"><span data-stu-id="ad1cc-191">In comparison, a backup point taken at the end of each quarter (for audit purposes) may need to be preserved for many months or years.</span></span>

    ![Virtual machine is backed up with recovery point](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms/long-term-retention.png)

    <span data-ttu-id="ad1cc-193">In this example image:</span><span class="sxs-lookup"><span data-stu-id="ad1cc-193">In this example image:</span></span>

   * <span data-ttu-id="ad1cc-194">**Daily retention policy**: Backups taken daily are stored for 30 days.</span><span class="sxs-lookup"><span data-stu-id="ad1cc-194">**Daily retention policy**: Backups taken daily are stored for 30 days.</span></span>
   * <span data-ttu-id="ad1cc-195">**Weekly retention policy**: Backups taken every week on Sunday are preserved for 104 weeks.</span><span class="sxs-lookup"><span data-stu-id="ad1cc-195">**Weekly retention policy**: Backups taken every week on Sunday are preserved for 104 weeks.</span></span>
   * <span data-ttu-id="ad1cc-196">**Monthly retention policy**: Backups taken on the last Sunday of each month are preserved for 120 months.</span><span class="sxs-lookup"><span data-stu-id="ad1cc-196">**Monthly retention policy**: Backups taken on the last Sunday of each month are preserved for 120 months.</span></span>
   * <span data-ttu-id="ad1cc-197">**Yearly retention policy**: Backups taken on the first Sunday of every January are preserved for 99 years.</span><span class="sxs-lookup"><span data-stu-id="ad1cc-197">**Yearly retention policy**: Backups taken on the first Sunday of every January are preserved for 99 years.</span></span>

     <span data-ttu-id="ad1cc-198">A job is created to configure the protection policy and associate the virtual machines to that policy for each virtual machine that you've selected.</span><span class="sxs-lookup"><span data-stu-id="ad1cc-198">A job is created to configure the protection policy and associate the virtual machines to that policy for each virtual machine that you've selected.</span></span>
6. <span data-ttu-id="ad1cc-199">To view the list of **Configure Protection** jobs, from the vaults menu, click **Jobs** and select **Configure Protection** from the **Operation** filter.</span><span class="sxs-lookup"><span data-stu-id="ad1cc-199">To view the list of **Configure Protection** jobs, from the vaults menu, click **Jobs** and select **Configure Protection** from the **Operation** filter.</span></span>

    ![Configure protection job](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms/protect-configureprotection.png)

## <a name="initial-backup"></a><span data-ttu-id="ad1cc-201">Initial backup</span><span class="sxs-lookup"><span data-stu-id="ad1cc-201">Initial backup</span></span>
<span data-ttu-id="ad1cc-202">Once the virtual machine is protected with a policy, it shows up under the **Protected Items** tab with the status of *Protected - (pending initial backup)*.</span><span class="sxs-lookup"><span data-stu-id="ad1cc-202">Once the virtual machine is protected with a policy, it shows up under the **Protected Items** tab with the status of *Protected - (pending initial backup)*.</span></span> <span data-ttu-id="ad1cc-203">By default, the first scheduled backup is the *initial backup*.</span><span class="sxs-lookup"><span data-stu-id="ad1cc-203">By default, the first scheduled backup is the *initial backup*.</span></span>

<span data-ttu-id="ad1cc-204">To trigger the initial backup immediately after configuring protection:</span><span class="sxs-lookup"><span data-stu-id="ad1cc-204">To trigger the initial backup immediately after configuring protection:</span></span>

1. <span data-ttu-id="ad1cc-205">At the bottom of the **Protected Items** page, click **Backup Now**.</span><span class="sxs-lookup"><span data-stu-id="ad1cc-205">At the bottom of the **Protected Items** page, click **Backup Now**.</span></span>

    <span data-ttu-id="ad1cc-206">The Azure Backup service creates a backup job for the initial backup operation.</span><span class="sxs-lookup"><span data-stu-id="ad1cc-206">The Azure Backup service creates a backup job for the initial backup operation.</span></span>
2. <span data-ttu-id="ad1cc-207">Click the **Jobs** tab to view the list of jobs.</span><span class="sxs-lookup"><span data-stu-id="ad1cc-207">Click the **Jobs** tab to view the list of jobs.</span></span>

    ![Backup in progress](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms/protect-inprogress.png)

> [!NOTE]
> During the backup operation, the Azure Backup service issues a command to the backup extension in each virtual machine to flush all write jobs and take a consistent snapshot.
>
>

<span data-ttu-id="ad1cc-210">When the initial backup finishes, the status of the virtual machine in the **Protected Items** tab is *Protected*.</span><span class="sxs-lookup"><span data-stu-id="ad1cc-210">When the initial backup finishes, the status of the virtual machine in the **Protected Items** tab is *Protected*.</span></span>

![Virtual machine is backed up with recovery point](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms/protect-backedupvm.png)

## <a name="viewing-backup-status-and-details"></a><span data-ttu-id="ad1cc-212">Viewing backup status and details</span><span class="sxs-lookup"><span data-stu-id="ad1cc-212">Viewing backup status and details</span></span>
<span data-ttu-id="ad1cc-213">Once protected, the virtual machine count also increases in the **Dashboard** page summary.</span><span class="sxs-lookup"><span data-stu-id="ad1cc-213">Once protected, the virtual machine count also increases in the **Dashboard** page summary.</span></span> <span data-ttu-id="ad1cc-214">The **Dashboard** page also shows the number of jobs from the last 24 hours that were *successful*, have *failed*, and are *in progress*.</span><span class="sxs-lookup"><span data-stu-id="ad1cc-214">The **Dashboard** page also shows the number of jobs from the last 24 hours that were *successful*, have *failed*, and are *in progress*.</span></span> <span data-ttu-id="ad1cc-215">On the **Jobs** page, use the **Status**, **Operation**, or **From** and **To** menus to filter the jobs.</span><span class="sxs-lookup"><span data-stu-id="ad1cc-215">On the **Jobs** page, use the **Status**, **Operation**, or **From** and **To** menus to filter the jobs.</span></span>

![Status of backup in Dashboard page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms/dashboard-protectedvms.png)

<span data-ttu-id="ad1cc-217">Values in the dashboard are refreshed once every 24 hours.</span><span class="sxs-lookup"><span data-stu-id="ad1cc-217">Values in the dashboard are refreshed once every 24 hours.</span></span>

## <a name="troubleshooting-errors"></a><span data-ttu-id="ad1cc-218">Troubleshooting errors</span><span class="sxs-lookup"><span data-stu-id="ad1cc-218">Troubleshooting errors</span></span>
<span data-ttu-id="ad1cc-219">If you run into issues while backing up your virtual machine, look at the [VM     troubleshooting article](backup-azure-vms-troubleshoot.md) for help.</span><span class="sxs-lookup"><span data-stu-id="ad1cc-219">If you run into issues while backing up your virtual machine, look at the [VM     troubleshooting article](backup-azure-vms-troubleshoot.md) for help.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ad1cc-220">Next steps</span><span class="sxs-lookup"><span data-stu-id="ad1cc-220">Next steps</span></span>
* [<span data-ttu-id="ad1cc-221">Manage and monitor your virtual machines</span><span class="sxs-lookup"><span data-stu-id="ad1cc-221">Manage and monitor your virtual machines</span></span>](backup-azure-manage-vms.md)
* [<span data-ttu-id="ad1cc-222">Restore virtual machines</span><span class="sxs-lookup"><span data-stu-id="ad1cc-222">Restore virtual machines</span></span>](backup-azure-restore-vms.md)






















