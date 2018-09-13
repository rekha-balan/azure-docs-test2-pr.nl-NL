---
title: First Look- Back up Azure VMs with a backup vault | Microsoft Docs
description: Use the classic portal to back up Azure VMs to a Backup vault. This tutorial explains all phases including creating the Backup vault, registering the VMs, creating backup policy, and running the initial backup job.
services: backup
documentationcenter: ''
author: markgalioto
manager: carmonm
editor: ''
ms.assetid: 722820dc-b65f-425c-a9e5-c1946e896a87
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 3/10/2017
ms.author: markgal;
ms.openlocfilehash: caf2a3a523108457ce7e095c78ee3ae1cb59bffd
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660957"
---
# <a name="first-look-backing-up-azure-virtual-machines"></a><span data-ttu-id="23b41-104">First look: Backing up Azure virtual machines</span><span class="sxs-lookup"><span data-stu-id="23b41-104">First look: Backing up Azure virtual machines</span></span>
> [!div class="op_single_selector"]
> * [Protect VMs with a recovery services vault](backup-azure-vms-first-look-arm.md)
> * [Protect Azure VMs with a backup vault](backup-azure-vms-first-look.md)
>
>

<span data-ttu-id="23b41-107">This tutorial takes you through the steps for backing up an Azure virtual machine (VM) to a backup vault in Azure.</span><span class="sxs-lookup"><span data-stu-id="23b41-107">This tutorial takes you through the steps for backing up an Azure virtual machine (VM) to a backup vault in Azure.</span></span> <span data-ttu-id="23b41-108">This article describes the classic model or Service Manager deployment model, for backing up VMs.</span><span class="sxs-lookup"><span data-stu-id="23b41-108">This article describes the classic model or Service Manager deployment model, for backing up VMs.</span></span> <span data-ttu-id="23b41-109">The following steps apply only to Backup vaults created in the classic portal.</span><span class="sxs-lookup"><span data-stu-id="23b41-109">The following steps apply only to Backup vaults created in the classic portal.</span></span> <span data-ttu-id="23b41-110">Microsoft recommends using the Resource Manager model for new deployments.</span><span class="sxs-lookup"><span data-stu-id="23b41-110">Microsoft recommends using the Resource Manager model for new deployments.</span></span>

<span data-ttu-id="23b41-111">If you are interested in backing up a VM to a Recovery Services vault that belongs to a Resource Group, see [First look: Protect VMs with a recovery services vault](backup-azure-vms-first-look-arm.md).</span><span class="sxs-lookup"><span data-stu-id="23b41-111">If you are interested in backing up a VM to a Recovery Services vault that belongs to a Resource Group, see [First look: Protect VMs with a recovery services vault](backup-azure-vms-first-look-arm.md).</span></span>

<span data-ttu-id="23b41-112">To successfully complete the following tutorial, these prerequisites must exist:</span><span class="sxs-lookup"><span data-stu-id="23b41-112">To successfully complete the following tutorial, these prerequisites must exist:</span></span>

* <span data-ttu-id="23b41-113">You have created a VM in your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="23b41-113">You have created a VM in your Azure subscription.</span></span>
* <span data-ttu-id="23b41-114">The VM has connectivity to Azure public IP addresses.</span><span class="sxs-lookup"><span data-stu-id="23b41-114">The VM has connectivity to Azure public IP addresses.</span></span> <span data-ttu-id="23b41-115">For additional information, see [Network connectivity](backup-azure-vms-prepare.md#network-connectivity).</span><span class="sxs-lookup"><span data-stu-id="23b41-115">For additional information, see [Network connectivity](backup-azure-vms-prepare.md#network-connectivity).</span></span>


> [!NOTE]
> Azure has two deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md). This tutorial is for use with virtual machines created in the classic portal.
>
>

## <a name="create-a-backup-vault"></a><span data-ttu-id="23b41-118">Create a backup vault</span><span class="sxs-lookup"><span data-stu-id="23b41-118">Create a backup vault</span></span>
<span data-ttu-id="23b41-119">A backup vault is an entity that stores all the backups and recovery points that have been created over time.</span><span class="sxs-lookup"><span data-stu-id="23b41-119">A backup vault is an entity that stores all the backups and recovery points that have been created over time.</span></span> <span data-ttu-id="23b41-120">The backup vault also contains the backup policies that are applied to the virtual machines being backed up.</span><span class="sxs-lookup"><span data-stu-id="23b41-120">The backup vault also contains the backup policies that are applied to the virtual machines being backed up.</span></span>

> [!IMPORTANT]
> Starting March 2017, you can no longer use the classic portal to create Backup vaults. Existing Backup vaults are still supported, and it is possible to [use Azure PowerShell to create Backup vaults](./backup-client-automation-classic.md#create-a-backup-vault). However, Microsoft recommends you create Recovery Services vaults for all deployments because future enhancements apply to Recovery Services vaults, only.



## <a name="discover-and-register-azure-virtual-machines"></a><span data-ttu-id="23b41-124">Discover and Register Azure virtual machines</span><span class="sxs-lookup"><span data-stu-id="23b41-124">Discover and Register Azure virtual machines</span></span>
<span data-ttu-id="23b41-125">Before registering the VM with a vault, run the discovery process to identify any new VMs.</span><span class="sxs-lookup"><span data-stu-id="23b41-125">Before registering the VM with a vault, run the discovery process to identify any new VMs.</span></span> <span data-ttu-id="23b41-126">This returns a list of virtual machines in the subscription, along with additional information like the cloud service name and the region.</span><span class="sxs-lookup"><span data-stu-id="23b41-126">This returns a list of virtual machines in the subscription, along with additional information like the cloud service name and the region.</span></span>

1. <span data-ttu-id="23b41-127">Sign in to the [Azure Classic portal](http://manage.windowsazure.com/)</span><span class="sxs-lookup"><span data-stu-id="23b41-127">Sign in to the [Azure Classic portal](http://manage.windowsazure.com/)</span></span>
2. <span data-ttu-id="23b41-128">In the Azure classic portal, click **Recovery Services** to open the list of Recovery Services vaults.</span><span class="sxs-lookup"><span data-stu-id="23b41-128">In the Azure classic portal, click **Recovery Services** to open the list of Recovery Services vaults.</span></span>
    <span data-ttu-id="23b41-129">![Select workload](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms-first-look/recovery-services-icon.png)</span><span class="sxs-lookup"><span data-stu-id="23b41-129">![Select workload](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms-first-look/recovery-services-icon.png)</span></span>
3. <span data-ttu-id="23b41-130">From the list of vaults, select the vault to back up a VM.</span><span class="sxs-lookup"><span data-stu-id="23b41-130">From the list of vaults, select the vault to back up a VM.</span></span>

    <span data-ttu-id="23b41-131">When you select your vault, it opens in the **Quick Start** page</span><span class="sxs-lookup"><span data-stu-id="23b41-131">When you select your vault, it opens in the **Quick Start** page</span></span>
4. <span data-ttu-id="23b41-132">From the vault menu, click **Registered Items**.</span><span class="sxs-lookup"><span data-stu-id="23b41-132">From the vault menu, click **Registered Items**.</span></span>

    ![Select workload](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms-first-look/configure-registered-items.png)
5. <span data-ttu-id="23b41-134">From the **Type** menu, select **Azure Virtual Machine**.</span><span class="sxs-lookup"><span data-stu-id="23b41-134">From the **Type** menu, select **Azure Virtual Machine**.</span></span>

    ![Select workload](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms/discovery-select-workload.png)
6. <span data-ttu-id="23b41-136">Click **DISCOVER** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="23b41-136">Click **DISCOVER** at the bottom of the page.</span></span>
    <span data-ttu-id="23b41-137">![Discover button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms/discover-button-only.png)</span><span class="sxs-lookup"><span data-stu-id="23b41-137">![Discover button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms/discover-button-only.png)</span></span>

    <span data-ttu-id="23b41-138">The discovery process may take a few minutes while the virtual machines are being tabulated.</span><span class="sxs-lookup"><span data-stu-id="23b41-138">The discovery process may take a few minutes while the virtual machines are being tabulated.</span></span> <span data-ttu-id="23b41-139">There is a notification at the bottom of the screen that lets you know that the process is running.</span><span class="sxs-lookup"><span data-stu-id="23b41-139">There is a notification at the bottom of the screen that lets you know that the process is running.</span></span>

    ![Discover VMs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms/discovering-vms.png)

    <span data-ttu-id="23b41-141">The notification changes when the process is complete.</span><span class="sxs-lookup"><span data-stu-id="23b41-141">The notification changes when the process is complete.</span></span>

    ![Discovery done](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms-first-look/discovery-complete.png)
7. <span data-ttu-id="23b41-143">Click **REGISTER** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="23b41-143">Click **REGISTER** at the bottom of the page.</span></span>
    <span data-ttu-id="23b41-144">![Register button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms-first-look/register-icon.png)</span><span class="sxs-lookup"><span data-stu-id="23b41-144">![Register button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms-first-look/register-icon.png)</span></span>
8. <span data-ttu-id="23b41-145">In the **Register Items** shortcut menu, select the virtual machines that you want to register.</span><span class="sxs-lookup"><span data-stu-id="23b41-145">In the **Register Items** shortcut menu, select the virtual machines that you want to register.</span></span>

   > [!TIP]
   > Multiple virtual machines can be registered at one time.
   >
   >

    <span data-ttu-id="23b41-147">A job is created for each virtual machine that you've selected.</span><span class="sxs-lookup"><span data-stu-id="23b41-147">A job is created for each virtual machine that you've selected.</span></span>
9. <span data-ttu-id="23b41-148">Click **View Job** in the notification to go to the **Jobs** page.</span><span class="sxs-lookup"><span data-stu-id="23b41-148">Click **View Job** in the notification to go to the **Jobs** page.</span></span>

    ![Register job](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms/register-create-job.png)

    <span data-ttu-id="23b41-150">The virtual machine also appears in the list of registered items, along with the status of the registration operation.</span><span class="sxs-lookup"><span data-stu-id="23b41-150">The virtual machine also appears in the list of registered items, along with the status of the registration operation.</span></span>

    ![Registering status 1](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms/register-status01.png)

    <span data-ttu-id="23b41-152">When the operation completes, the status changes to reflect the *registered* state.</span><span class="sxs-lookup"><span data-stu-id="23b41-152">When the operation completes, the status changes to reflect the *registered* state.</span></span>

    ![Registration status 2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms/register-status02.png)

## <a name="install-the-vm-agent-on-the-virtual-machine"></a><span data-ttu-id="23b41-154">Install the VM Agent on the virtual machine</span><span class="sxs-lookup"><span data-stu-id="23b41-154">Install the VM Agent on the virtual machine</span></span>
<span data-ttu-id="23b41-155">The Azure VM Agent must be installed on the Azure virtual machine for the Backup extension to work.</span><span class="sxs-lookup"><span data-stu-id="23b41-155">The Azure VM Agent must be installed on the Azure virtual machine for the Backup extension to work.</span></span> <span data-ttu-id="23b41-156">If your VM was created from the Azure gallery, the VM Agent is already present on the VM; you can skip to [protecting your VMs](backup-azure-vms-first-look.md#create-the-backup-policy).</span><span class="sxs-lookup"><span data-stu-id="23b41-156">If your VM was created from the Azure gallery, the VM Agent is already present on the VM; you can skip to [protecting your VMs](backup-azure-vms-first-look.md#create-the-backup-policy).</span></span>

<span data-ttu-id="23b41-157">If your VM migrated from an on-premises datacenter, the VM probably does not have the VM Agent installed.</span><span class="sxs-lookup"><span data-stu-id="23b41-157">If your VM migrated from an on-premises datacenter, the VM probably does not have the VM Agent installed.</span></span> <span data-ttu-id="23b41-158">You must install the VM Agent on the virtual machine before proceeding to protect the VM.</span><span class="sxs-lookup"><span data-stu-id="23b41-158">You must install the VM Agent on the virtual machine before proceeding to protect the VM.</span></span> <span data-ttu-id="23b41-159">For detailed steps on installing the VM Agent, see the [VM Agent section of the Backup VMs article](backup-azure-vms-prepare.md#vm-agent).</span><span class="sxs-lookup"><span data-stu-id="23b41-159">For detailed steps on installing the VM Agent, see the [VM Agent section of the Backup VMs article](backup-azure-vms-prepare.md#vm-agent).</span></span>

## <a name="create-the-backup-policy"></a><span data-ttu-id="23b41-160">Create the backup policy</span><span class="sxs-lookup"><span data-stu-id="23b41-160">Create the backup policy</span></span>
<span data-ttu-id="23b41-161">Before you trigger the initial backup job, set the schedule when backup snapshots are taken.</span><span class="sxs-lookup"><span data-stu-id="23b41-161">Before you trigger the initial backup job, set the schedule when backup snapshots are taken.</span></span> <span data-ttu-id="23b41-162">The schedule when backup snapshots are taken, and the length of time those snapshots are retained, is the backup policy.</span><span class="sxs-lookup"><span data-stu-id="23b41-162">The schedule when backup snapshots are taken, and the length of time those snapshots are retained, is the backup policy.</span></span> <span data-ttu-id="23b41-163">The retention information is based on Grandfather-father-son backup rotation scheme.</span><span class="sxs-lookup"><span data-stu-id="23b41-163">The retention information is based on Grandfather-father-son backup rotation scheme.</span></span>

1. <span data-ttu-id="23b41-164">Navigate to the backup vault under **Recovery Services** in the Azure Classic portal, and  click **Registered Items**.</span><span class="sxs-lookup"><span data-stu-id="23b41-164">Navigate to the backup vault under **Recovery Services** in the Azure Classic portal, and  click **Registered Items**.</span></span>
2. <span data-ttu-id="23b41-165">Select **Azure Virtual Machine** from the drop-down menu.</span><span class="sxs-lookup"><span data-stu-id="23b41-165">Select **Azure Virtual Machine** from the drop-down menu.</span></span>

    ![Select workload in portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms/select-workload.png)
3. <span data-ttu-id="23b41-167">Click **PROTECT** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="23b41-167">Click **PROTECT** at the bottom of the page.</span></span>
    <span data-ttu-id="23b41-168">![Click Protect](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms-first-look/protect-icon.png)</span><span class="sxs-lookup"><span data-stu-id="23b41-168">![Click Protect](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms-first-look/protect-icon.png)</span></span>

    <span data-ttu-id="23b41-169">The **Protect Items wizard** appears and lists *only* virtual machines that are registered and not protected.</span><span class="sxs-lookup"><span data-stu-id="23b41-169">The **Protect Items wizard** appears and lists *only* virtual machines that are registered and not protected.</span></span>

    ![Configure protection at scale](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms/protect-at-scale.png)
4. <span data-ttu-id="23b41-171">Select the virtual machines that you want to protect.</span><span class="sxs-lookup"><span data-stu-id="23b41-171">Select the virtual machines that you want to protect.</span></span>

    <span data-ttu-id="23b41-172">If there are two or more virtual machines with the same name, use the Cloud Service to distinguish between the virtual machines.</span><span class="sxs-lookup"><span data-stu-id="23b41-172">If there are two or more virtual machines with the same name, use the Cloud Service to distinguish between the virtual machines.</span></span>
5. <span data-ttu-id="23b41-173">On the **Configure protection** menu select an existing policy or create a new policy to protect the virtual machines that you identified.</span><span class="sxs-lookup"><span data-stu-id="23b41-173">On the **Configure protection** menu select an existing policy or create a new policy to protect the virtual machines that you identified.</span></span>

    <span data-ttu-id="23b41-174">New Backup vaults have a default policy associated with the vault.</span><span class="sxs-lookup"><span data-stu-id="23b41-174">New Backup vaults have a default policy associated with the vault.</span></span> <span data-ttu-id="23b41-175">This policy takes a daily snapshot each evening, and the daily snapshot is retained for 30 days.</span><span class="sxs-lookup"><span data-stu-id="23b41-175">This policy takes a daily snapshot each evening, and the daily snapshot is retained for 30 days.</span></span> <span data-ttu-id="23b41-176">Each backup policy can have multiple virtual machines associated with it.</span><span class="sxs-lookup"><span data-stu-id="23b41-176">Each backup policy can have multiple virtual machines associated with it.</span></span> <span data-ttu-id="23b41-177">However, the virtual machine can only be associated with one policy at a time.</span><span class="sxs-lookup"><span data-stu-id="23b41-177">However, the virtual machine can only be associated with one policy at a time.</span></span>

    ![Protect with new policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms/policy-schedule.png)

   > [!NOTE]
   > A backup policy includes a retention scheme for the scheduled backups. If you select an existing backup policy, you will be unable to modify the retention options in the next step.
   >
   >
6. <span data-ttu-id="23b41-181">On **Retention Range** define the daily, weekly, monthly, and yearly scope for the specific backup points.</span><span class="sxs-lookup"><span data-stu-id="23b41-181">On **Retention Range** define the daily, weekly, monthly, and yearly scope for the specific backup points.</span></span>

    ![Virtual machine is backed up with recovery point](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms/long-term-retention.png)

    <span data-ttu-id="23b41-183">Retention policy specifies the length of time for storing a backup.</span><span class="sxs-lookup"><span data-stu-id="23b41-183">Retention policy specifies the length of time for storing a backup.</span></span> <span data-ttu-id="23b41-184">You can specify different retention policies based on when the backup is taken.</span><span class="sxs-lookup"><span data-stu-id="23b41-184">You can specify different retention policies based on when the backup is taken.</span></span>
7. <span data-ttu-id="23b41-185">Click **Jobs** to view the list of **Configure Protection** jobs.</span><span class="sxs-lookup"><span data-stu-id="23b41-185">Click **Jobs** to view the list of **Configure Protection** jobs.</span></span>

    ![Configure protection job](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms/protect-configureprotection.png)

    <span data-ttu-id="23b41-187">Now that you've established the policy, go to the next step and run the initial backup.</span><span class="sxs-lookup"><span data-stu-id="23b41-187">Now that you've established the policy, go to the next step and run the initial backup.</span></span>

## <a name="initial-backup"></a><span data-ttu-id="23b41-188">Initial backup</span><span class="sxs-lookup"><span data-stu-id="23b41-188">Initial backup</span></span>
<span data-ttu-id="23b41-189">Once a virtual machine has been protected with a policy, you can view that relationship on the **Protected Items** tab. Until the initial backup occurs, the **Protection Status** shows as **Protected - (pending initial backup)**.</span><span class="sxs-lookup"><span data-stu-id="23b41-189">Once a virtual machine has been protected with a policy, you can view that relationship on the **Protected Items** tab. Until the initial backup occurs, the **Protection Status** shows as **Protected - (pending initial backup)**.</span></span> <span data-ttu-id="23b41-190">By default, the first scheduled backup is the *initial backup*.</span><span class="sxs-lookup"><span data-stu-id="23b41-190">By default, the first scheduled backup is the *initial backup*.</span></span>

![Backup pending](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms-first-look/protection-pending-border.png)

<span data-ttu-id="23b41-192">To start the initial backup now:</span><span class="sxs-lookup"><span data-stu-id="23b41-192">To start the initial backup now:</span></span>

1. <span data-ttu-id="23b41-193">On the **Protected Items** page, click **Backup Now** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="23b41-193">On the **Protected Items** page, click **Backup Now** at the bottom of the page.</span></span>
    <span data-ttu-id="23b41-194">![Backup Now icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms-first-look/backup-now-icon.png)</span><span class="sxs-lookup"><span data-stu-id="23b41-194">![Backup Now icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms-first-look/backup-now-icon.png)</span></span>

    <span data-ttu-id="23b41-195">The Azure Backup service creates a backup job for the initial backup operation.</span><span class="sxs-lookup"><span data-stu-id="23b41-195">The Azure Backup service creates a backup job for the initial backup operation.</span></span>
2. <span data-ttu-id="23b41-196">Click the **Jobs** tab to view the list of jobs.</span><span class="sxs-lookup"><span data-stu-id="23b41-196">Click the **Jobs** tab to view the list of jobs.</span></span>

    ![Backup in progress](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms-first-look/protect-inprogress.png)

    <span data-ttu-id="23b41-198">When initial backup is complete, the status of the virtual machine in the **Protected Items** tab is *Protected*.</span><span class="sxs-lookup"><span data-stu-id="23b41-198">When initial backup is complete, the status of the virtual machine in the **Protected Items** tab is *Protected*.</span></span>

    ![Virtual machine is backed up with recovery point](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms/protect-backedupvm.png)

   > [!NOTE]
   > Backing up virtual machines is a local process. You cannot back up virtual machines from one region to a backup vault in another region. So, for every Azure region that has VMs that need to be backed up, at least one backup vault must be created in that region.
   >
   >

## <a name="next-steps"></a><span data-ttu-id="23b41-203">Next steps</span><span class="sxs-lookup"><span data-stu-id="23b41-203">Next steps</span></span>
<span data-ttu-id="23b41-204">Now that you have successfully backed up a VM, there are several next steps that could be of interest.</span><span class="sxs-lookup"><span data-stu-id="23b41-204">Now that you have successfully backed up a VM, there are several next steps that could be of interest.</span></span> <span data-ttu-id="23b41-205">The most logical step is to familiarize yourself with restoring data to a VM.</span><span class="sxs-lookup"><span data-stu-id="23b41-205">The most logical step is to familiarize yourself with restoring data to a VM.</span></span> <span data-ttu-id="23b41-206">However, there are management tasks that will help you understand how to keep your data safe and minimize costs.</span><span class="sxs-lookup"><span data-stu-id="23b41-206">However, there are management tasks that will help you understand how to keep your data safe and minimize costs.</span></span>

* [<span data-ttu-id="23b41-207">Manage and monitor your virtual machines</span><span class="sxs-lookup"><span data-stu-id="23b41-207">Manage and monitor your virtual machines</span></span>](backup-azure-manage-vms.md)
* [<span data-ttu-id="23b41-208">Restore virtual machines</span><span class="sxs-lookup"><span data-stu-id="23b41-208">Restore virtual machines</span></span>](backup-azure-restore-vms.md)
* [<span data-ttu-id="23b41-209">Troubleshooting guidance</span><span class="sxs-lookup"><span data-stu-id="23b41-209">Troubleshooting guidance</span></span>](backup-azure-vms-troubleshoot.md)

## <a name="questions"></a><span data-ttu-id="23b41-210">Questions?</span><span class="sxs-lookup"><span data-stu-id="23b41-210">Questions?</span></span>
<span data-ttu-id="23b41-211">If you have questions, or if there is any feature that you would like to see included, [send us feedback](http://aka.ms/azurebackup_feedback).</span><span class="sxs-lookup"><span data-stu-id="23b41-211">If you have questions, or if there is any feature that you would like to see included, [send us feedback](http://aka.ms/azurebackup_feedback).</span></span>




















