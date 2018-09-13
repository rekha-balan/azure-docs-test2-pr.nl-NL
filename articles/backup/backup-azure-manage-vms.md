---
title: Manage Resource Manager-deployed virtual machine backups | Microsoft Docs
description: Learn how to manage and monitor Resource Manager-deployed virtual machine backups
services: backup
documentationcenter: ''
author: trinadhk
manager: shreeshd
editor: ''
ms.assetid: f3050283-d60f-472d-b464-cb844e70d67e
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: trinadhk;markgal
ms.openlocfilehash: 5e7dd3132970b3a865097967d1113ce6fcfa0f17
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556196"
---
# <a name="manage-azure-virtual-machine-backups"></a><span data-ttu-id="5e59e-103">Manage Azure virtual machine backups</span><span class="sxs-lookup"><span data-stu-id="5e59e-103">Manage Azure virtual machine backups</span></span>
> [!div class="op_single_selector"]
> * [Manage Azure VM backups](backup-azure-manage-vms.md)
> * [Manage Classic VM backups](backup-azure-manage-vms-classic.md)
>
>

<span data-ttu-id="5e59e-106">This article provides guidance on managing VM backups, and explains the backup alerts information available in the portal dashboard.</span><span class="sxs-lookup"><span data-stu-id="5e59e-106">This article provides guidance on managing VM backups, and explains the backup alerts information available in the portal dashboard.</span></span> <span data-ttu-id="5e59e-107">The guidance in this article applies to using VMs with Recovery Services vaults.</span><span class="sxs-lookup"><span data-stu-id="5e59e-107">The guidance in this article applies to using VMs with Recovery Services vaults.</span></span> <span data-ttu-id="5e59e-108">This article does not cover the creation of virtual machines, nor does it explain how to protect virtual machines.</span><span class="sxs-lookup"><span data-stu-id="5e59e-108">This article does not cover the creation of virtual machines, nor does it explain how to protect virtual machines.</span></span> <span data-ttu-id="5e59e-109">For a primer on protecting Azure Resource Manager-deployed VMs in Azure with a Recovery Services vault, see [First look: Back up VMs to a Recovery Services vault](backup-azure-vms-first-look-arm.md).</span><span class="sxs-lookup"><span data-stu-id="5e59e-109">For a primer on protecting Azure Resource Manager-deployed VMs in Azure with a Recovery Services vault, see [First look: Back up VMs to a Recovery Services vault](backup-azure-vms-first-look-arm.md).</span></span>

## <a name="manage-vaults-and-protected-virtual-machines"></a><span data-ttu-id="5e59e-110">Manage vaults and protected virtual machines</span><span class="sxs-lookup"><span data-stu-id="5e59e-110">Manage vaults and protected virtual machines</span></span>
<span data-ttu-id="5e59e-111">In the Azure portal, the Recovery Services vault dashboard provides access to information about the vault including:</span><span class="sxs-lookup"><span data-stu-id="5e59e-111">In the Azure portal, the Recovery Services vault dashboard provides access to information about the vault including:</span></span>

* <span data-ttu-id="5e59e-112">the most recent backup snapshot, which is also the latest restore point <br\></span><span class="sxs-lookup"><span data-stu-id="5e59e-112">the most recent backup snapshot, which is also the latest restore point <br\></span></span>
* <span data-ttu-id="5e59e-113">the backup policy <br\></span><span class="sxs-lookup"><span data-stu-id="5e59e-113">the backup policy <br\></span></span>
* <span data-ttu-id="5e59e-114">total size of all backup snapshots <br\></span><span class="sxs-lookup"><span data-stu-id="5e59e-114">total size of all backup snapshots <br\></span></span>
* <span data-ttu-id="5e59e-115">number of virtual machines that are protected with the vault <br\></span><span class="sxs-lookup"><span data-stu-id="5e59e-115">number of virtual machines that are protected with the vault <br\></span></span>

<span data-ttu-id="5e59e-116">Many management tasks with a virtual machine backup begin with opening the vault in the dashboard.</span><span class="sxs-lookup"><span data-stu-id="5e59e-116">Many management tasks with a virtual machine backup begin with opening the vault in the dashboard.</span></span> <span data-ttu-id="5e59e-117">However, because vaults can be used to protect multiple items (or multiple VMs), to view details about a particular VM, open the vault item dashboard.</span><span class="sxs-lookup"><span data-stu-id="5e59e-117">However, because vaults can be used to protect multiple items (or multiple VMs), to view details about a particular VM, open the vault item dashboard.</span></span> <span data-ttu-id="5e59e-118">The following procedure shows you how to open the *vault dashboard* and then continue to the *vault item dashboard*.</span><span class="sxs-lookup"><span data-stu-id="5e59e-118">The following procedure shows you how to open the *vault dashboard* and then continue to the *vault item dashboard*.</span></span> <span data-ttu-id="5e59e-119">There are "tips" in both procedures that point out how to add the vault and vault item to the Azure dashboard by using the Pin to dashboard command.</span><span class="sxs-lookup"><span data-stu-id="5e59e-119">There are "tips" in both procedures that point out how to add the vault and vault item to the Azure dashboard by using the Pin to dashboard command.</span></span> <span data-ttu-id="5e59e-120">Pin to dashboard is a way of creating a shortcut to the vault or item.</span><span class="sxs-lookup"><span data-stu-id="5e59e-120">Pin to dashboard is a way of creating a shortcut to the vault or item.</span></span> <span data-ttu-id="5e59e-121">You can also execute common commands from the shortcut.</span><span class="sxs-lookup"><span data-stu-id="5e59e-121">You can also execute common commands from the shortcut.</span></span>

> [!TIP]
> If you have multiple dashboards and blades open, use the dark-blue slider at the bottom of the window to slide the Azure dashboard back and forth.
>
>

![Full view with slider](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-vms/bottom-slider.png)

### <a name="open-a-recovery-services-vault-in-the-dashboard"></a><span data-ttu-id="5e59e-124">Open a Recovery Services vault in the dashboard:</span><span class="sxs-lookup"><span data-stu-id="5e59e-124">Open a Recovery Services vault in the dashboard:</span></span>
1. <span data-ttu-id="5e59e-125">Sign in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="5e59e-125">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="5e59e-126">On the Hub menu, click **Browse** and in the list of resources, type **Recovery Services**.</span><span class="sxs-lookup"><span data-stu-id="5e59e-126">On the Hub menu, click **Browse** and in the list of resources, type **Recovery Services**.</span></span> <span data-ttu-id="5e59e-127">As you begin typing, the list filters based on your input.</span><span class="sxs-lookup"><span data-stu-id="5e59e-127">As you begin typing, the list filters based on your input.</span></span> <span data-ttu-id="5e59e-128">Click **Recovery Services vault**.</span><span class="sxs-lookup"><span data-stu-id="5e59e-128">Click **Recovery Services vault**.</span></span>

    ![Create Recovery Services Vault step 1](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-vms/browse-to-rs-vaults.png) <br/>

    <span data-ttu-id="5e59e-130">The list of Recovery Services vaults are displayed.</span><span class="sxs-lookup"><span data-stu-id="5e59e-130">The list of Recovery Services vaults are displayed.</span></span>

    ![<span data-ttu-id="5e59e-131">List of Recovery Services vaults</span><span class="sxs-lookup"><span data-stu-id="5e59e-131">List of Recovery Services vaults</span></span> ](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-vms/list-o-vaults.png) <br/>

   > [!TIP]
   > If you pin a vault to the Azure Dashboard, that vault is immediately accessible when you open the Azure portal. To pin a vault to the dashboard, in the vault list, right-click the vault, and select **Pin to dashboard**.
   >
   >
3. <span data-ttu-id="5e59e-134">From the list of vaults, select the vault to open its dashboard.</span><span class="sxs-lookup"><span data-stu-id="5e59e-134">From the list of vaults, select the vault to open its dashboard.</span></span> <span data-ttu-id="5e59e-135">When you select the vault, the vault dashboard and the **Settings** blade open.</span><span class="sxs-lookup"><span data-stu-id="5e59e-135">When you select the vault, the vault dashboard and the **Settings** blade open.</span></span> <span data-ttu-id="5e59e-136">In the following image, the **Contoso-vault** dashboard is highlighted.</span><span class="sxs-lookup"><span data-stu-id="5e59e-136">In the following image, the **Contoso-vault** dashboard is highlighted.</span></span>

    ![Open vault dashboard and Settings blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-vms/full-view-rs-vault.png)

### <a name="open-a-vault-item-dashboard"></a><span data-ttu-id="5e59e-138">Open a vault item dashboard</span><span class="sxs-lookup"><span data-stu-id="5e59e-138">Open a vault item dashboard</span></span>
<span data-ttu-id="5e59e-139">In the previous procedure you opened the vault dashboard.</span><span class="sxs-lookup"><span data-stu-id="5e59e-139">In the previous procedure you opened the vault dashboard.</span></span> <span data-ttu-id="5e59e-140">To open the vault item dashboard:</span><span class="sxs-lookup"><span data-stu-id="5e59e-140">To open the vault item dashboard:</span></span>

1. <span data-ttu-id="5e59e-141">In the vault dashboard, on the **Backup Items** tile, click **Azure Virtual Machines**.</span><span class="sxs-lookup"><span data-stu-id="5e59e-141">In the vault dashboard, on the **Backup Items** tile, click **Azure Virtual Machines**.</span></span>

    ![Open backup items tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-vms/contoso-vault-1606.png)

    <span data-ttu-id="5e59e-143">The **Backup Items** blade lists the last backup job for each item.</span><span class="sxs-lookup"><span data-stu-id="5e59e-143">The **Backup Items** blade lists the last backup job for each item.</span></span> <span data-ttu-id="5e59e-144">In this example, there is one virtual machine, demovm-markgal, protected by this vault.</span><span class="sxs-lookup"><span data-stu-id="5e59e-144">In this example, there is one virtual machine, demovm-markgal, protected by this vault.</span></span>  

    ![Backup items tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-vms/backup-items-blade.png)

   > [!TIP]
   > For ease of access, you can pin a vault item to the Azure Dashboard. To pin a vault item, in the vault item list, right-click the item and select **Pin to dashboard**.
   >
   >
2. <span data-ttu-id="5e59e-148">In the **Backup Items** blade, click the item to open the vault item dashboard.</span><span class="sxs-lookup"><span data-stu-id="5e59e-148">In the **Backup Items** blade, click the item to open the vault item dashboard.</span></span>

    ![Backup items tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-vms/backup-items-blade-select-item.png)

    <span data-ttu-id="5e59e-150">The vault item dashboard and its **Settings** blade open.</span><span class="sxs-lookup"><span data-stu-id="5e59e-150">The vault item dashboard and its **Settings** blade open.</span></span>

    ![Backup items dashboard with Settings blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-vms/item-dashboard-settings.png)

    <span data-ttu-id="5e59e-152">From the vault item dashboard, you can accomplish many key management tasks, such as:</span><span class="sxs-lookup"><span data-stu-id="5e59e-152">From the vault item dashboard, you can accomplish many key management tasks, such as:</span></span>

   * <span data-ttu-id="5e59e-153">change policies or create a new backup policy<br\></span><span class="sxs-lookup"><span data-stu-id="5e59e-153">change policies or create a new backup policy<br\></span></span>
   * <span data-ttu-id="5e59e-154">view restore points, and see their consistency state <br\></span><span class="sxs-lookup"><span data-stu-id="5e59e-154">view restore points, and see their consistency state <br\></span></span>
   * <span data-ttu-id="5e59e-155">on-demand backup of a virtual machine <br\></span><span class="sxs-lookup"><span data-stu-id="5e59e-155">on-demand backup of a virtual machine <br\></span></span>
   * <span data-ttu-id="5e59e-156">stop protecting virtual machines <br\></span><span class="sxs-lookup"><span data-stu-id="5e59e-156">stop protecting virtual machines <br\></span></span>
   * <span data-ttu-id="5e59e-157">resume protection of a virtual machine <br\></span><span class="sxs-lookup"><span data-stu-id="5e59e-157">resume protection of a virtual machine <br\></span></span>
   * <span data-ttu-id="5e59e-158">delete a backup data (or recovery point) <br\></span><span class="sxs-lookup"><span data-stu-id="5e59e-158">delete a backup data (or recovery point) <br\></span></span>
   * <span data-ttu-id="5e59e-159">[restore backup disks](backup-azure-arm-restore-vms.md#restore-backed-up-disks)  <br\></span><span class="sxs-lookup"><span data-stu-id="5e59e-159">[restore backup disks](backup-azure-arm-restore-vms.md#restore-backed-up-disks)  <br\></span></span>

<span data-ttu-id="5e59e-160">For the following procedures, the starting point is the vault item dashboard.</span><span class="sxs-lookup"><span data-stu-id="5e59e-160">For the following procedures, the starting point is the vault item dashboard.</span></span>

## <a name="manage-backup-policies"></a><span data-ttu-id="5e59e-161">Manage backup policies</span><span class="sxs-lookup"><span data-stu-id="5e59e-161">Manage backup policies</span></span>
1. <span data-ttu-id="5e59e-162">On the [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **All Settings** to open the **Settings** blade.</span><span class="sxs-lookup"><span data-stu-id="5e59e-162">On the [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **All Settings** to open the **Settings** blade.</span></span>

    ![Backup policy blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-vms/all-settings-button.png)
2. <span data-ttu-id="5e59e-164">On the **Settings** blade, click **Backup policy** to open that blade.</span><span class="sxs-lookup"><span data-stu-id="5e59e-164">On the **Settings** blade, click **Backup policy** to open that blade.</span></span>

    <span data-ttu-id="5e59e-165">On the blade, the backup frequency and retention range details are shown.</span><span class="sxs-lookup"><span data-stu-id="5e59e-165">On the blade, the backup frequency and retention range details are shown.</span></span>

    ![Backup policy blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-vms/backup-policy-blade.png)
3. <span data-ttu-id="5e59e-167">From the **Choose backup policy** menu:</span><span class="sxs-lookup"><span data-stu-id="5e59e-167">From the **Choose backup policy** menu:</span></span>

   * <span data-ttu-id="5e59e-168">To change policies, select a different policy and click **Save**.</span><span class="sxs-lookup"><span data-stu-id="5e59e-168">To change policies, select a different policy and click **Save**.</span></span> <span data-ttu-id="5e59e-169">The new policy is immediately applied to the vault.</span><span class="sxs-lookup"><span data-stu-id="5e59e-169">The new policy is immediately applied to the vault.</span></span> <span data-ttu-id="5e59e-170"><br\></span><span class="sxs-lookup"><span data-stu-id="5e59e-170"><br\></span></span>
   * <span data-ttu-id="5e59e-171">To create a policy, select **Create New**.</span><span class="sxs-lookup"><span data-stu-id="5e59e-171">To create a policy, select **Create New**.</span></span>

     ![Virtual machine backup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-vms/backup-policy-create-new.png)

     <span data-ttu-id="5e59e-173">For instructions on creating a backup policy, see [Defining a backup policy](backup-azure-manage-vms.md#defining-a-backup-policy).</span><span class="sxs-lookup"><span data-stu-id="5e59e-173">For instructions on creating a backup policy, see [Defining a backup policy](backup-azure-manage-vms.md#defining-a-backup-policy).</span></span>

[!INCLUDE [backup-create-backup-policy-for-vm](../../includes/backup-create-backup-policy-for-vm.md)]

## <a name="on-demand-backup-of-a-virtual-machine"></a><span data-ttu-id="5e59e-174">On-demand backup of a virtual machine</span><span class="sxs-lookup"><span data-stu-id="5e59e-174">On-demand backup of a virtual machine</span></span>
<span data-ttu-id="5e59e-175">You can take an on-demand backup of a virtual machine once it is configured for protection.</span><span class="sxs-lookup"><span data-stu-id="5e59e-175">You can take an on-demand backup of a virtual machine once it is configured for protection.</span></span> <span data-ttu-id="5e59e-176">If the initial backup is pending, on-demand backup creates a full copy of the virtual machine in the Recovery Services vault.</span><span class="sxs-lookup"><span data-stu-id="5e59e-176">If the initial backup is pending, on-demand backup creates a full copy of the virtual machine in the Recovery Services vault.</span></span> <span data-ttu-id="5e59e-177">If the initial backup is completed, an on-demand backup will only send changes from the previous snapshot, to the Recovery Services vault.</span><span class="sxs-lookup"><span data-stu-id="5e59e-177">If the initial backup is completed, an on-demand backup will only send changes from the previous snapshot, to the Recovery Services vault.</span></span> <span data-ttu-id="5e59e-178">That is, subsequent backups are always incremental.</span><span class="sxs-lookup"><span data-stu-id="5e59e-178">That is, subsequent backups are always incremental.</span></span>

> [!NOTE]
> The retention range for an on-demand backup is the retention value specified for the Daily backup point in the policy. If no Daily backup point is selected, then the weekly backup point is used.
>
>

<span data-ttu-id="5e59e-181">To trigger an on-demand backup of a virtual machine:</span><span class="sxs-lookup"><span data-stu-id="5e59e-181">To trigger an on-demand backup of a virtual machine:</span></span>

* <span data-ttu-id="5e59e-182">On the [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **Backup now**.</span><span class="sxs-lookup"><span data-stu-id="5e59e-182">On the [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **Backup now**.</span></span>

    ![Backup now button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-vms/backup-now-button.png)

    <span data-ttu-id="5e59e-184">The portal makes sure that you want to start an on-demand backup job.</span><span class="sxs-lookup"><span data-stu-id="5e59e-184">The portal makes sure that you want to start an on-demand backup job.</span></span> <span data-ttu-id="5e59e-185">Click **Yes** to start the backup job.</span><span class="sxs-lookup"><span data-stu-id="5e59e-185">Click **Yes** to start the backup job.</span></span>

    ![Backup now button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-vms/backup-now-check.png)

    <span data-ttu-id="5e59e-187">The backup job creates a recovery point.</span><span class="sxs-lookup"><span data-stu-id="5e59e-187">The backup job creates a recovery point.</span></span> <span data-ttu-id="5e59e-188">The retention range of the recovery point is the same as retention range specified in the policy associated with the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="5e59e-188">The retention range of the recovery point is the same as retention range specified in the policy associated with the virtual machine.</span></span> <span data-ttu-id="5e59e-189">To track the progress for the job, in the vault dashboard, click the **Backup Jobs** tile.</span><span class="sxs-lookup"><span data-stu-id="5e59e-189">To track the progress for the job, in the vault dashboard, click the **Backup Jobs** tile.</span></span>  

## <a name="stop-protecting-virtual-machines"></a><span data-ttu-id="5e59e-190">Stop protecting virtual machines</span><span class="sxs-lookup"><span data-stu-id="5e59e-190">Stop protecting virtual machines</span></span>
<span data-ttu-id="5e59e-191">If you choose to stop protecting a virtual machine, you are asked if you want to retain the recovery points.</span><span class="sxs-lookup"><span data-stu-id="5e59e-191">If you choose to stop protecting a virtual machine, you are asked if you want to retain the recovery points.</span></span> <span data-ttu-id="5e59e-192">There are two ways to stop protecting virtual machines:</span><span class="sxs-lookup"><span data-stu-id="5e59e-192">There are two ways to stop protecting virtual machines:</span></span>

* <span data-ttu-id="5e59e-193">stop all future backup jobs and delete all recovery points, or</span><span class="sxs-lookup"><span data-stu-id="5e59e-193">stop all future backup jobs and delete all recovery points, or</span></span>
* <span data-ttu-id="5e59e-194">stop all future backup jobs but leave the recovery points</span><span class="sxs-lookup"><span data-stu-id="5e59e-194">stop all future backup jobs but leave the recovery points</span></span> <br/>

<span data-ttu-id="5e59e-195">There is a cost associated with leaving the recovery points in storage.</span><span class="sxs-lookup"><span data-stu-id="5e59e-195">There is a cost associated with leaving the recovery points in storage.</span></span> <span data-ttu-id="5e59e-196">However, the benefit of leaving the recovery points is you can restore the virtual machine later, if desired.</span><span class="sxs-lookup"><span data-stu-id="5e59e-196">However, the benefit of leaving the recovery points is you can restore the virtual machine later, if desired.</span></span> <span data-ttu-id="5e59e-197">For information about the cost of leaving the recovery points, see the  [pricing details](https://azure.microsoft.com/pricing/details/backup/).</span><span class="sxs-lookup"><span data-stu-id="5e59e-197">For information about the cost of leaving the recovery points, see the  [pricing details](https://azure.microsoft.com/pricing/details/backup/).</span></span> <span data-ttu-id="5e59e-198">If you choose to delete all recovery points, you cannot restore the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="5e59e-198">If you choose to delete all recovery points, you cannot restore the virtual machine.</span></span>

<span data-ttu-id="5e59e-199">To stop protection for a virtual machine:</span><span class="sxs-lookup"><span data-stu-id="5e59e-199">To stop protection for a virtual machine:</span></span>

1. <span data-ttu-id="5e59e-200">On the [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **Stop backup**.</span><span class="sxs-lookup"><span data-stu-id="5e59e-200">On the [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **Stop backup**.</span></span>

    ![Stop backup button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-vms/stop-backup-button.png)

    <span data-ttu-id="5e59e-202">The Stop Backup blade opens.</span><span class="sxs-lookup"><span data-stu-id="5e59e-202">The Stop Backup blade opens.</span></span>

    ![Stop backup blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-vms/stop-backup-blade.png)
2. <span data-ttu-id="5e59e-204">On the **Stop Backup** blade, choose whether to retain or delete the backup data.</span><span class="sxs-lookup"><span data-stu-id="5e59e-204">On the **Stop Backup** blade, choose whether to retain or delete the backup data.</span></span> <span data-ttu-id="5e59e-205">The information box provides details about your choice.</span><span class="sxs-lookup"><span data-stu-id="5e59e-205">The information box provides details about your choice.</span></span>

    ![Stop protection](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-vms/retain-or-delete-option.png)
3. <span data-ttu-id="5e59e-207">If you chose to retain the backup data, skip to step 4.</span><span class="sxs-lookup"><span data-stu-id="5e59e-207">If you chose to retain the backup data, skip to step 4.</span></span> <span data-ttu-id="5e59e-208">If you chose to delete backup data, confirm that you want to stop the backup jobs and delete the recovery points - type the name of the item.</span><span class="sxs-lookup"><span data-stu-id="5e59e-208">If you chose to delete backup data, confirm that you want to stop the backup jobs and delete the recovery points - type the name of the item.</span></span>

    ![Stop verification](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-vms/item-verification-box.png)

    <span data-ttu-id="5e59e-210">If you aren't sure of the item name, hover over the exclamation mark to view the name.</span><span class="sxs-lookup"><span data-stu-id="5e59e-210">If you aren't sure of the item name, hover over the exclamation mark to view the name.</span></span> <span data-ttu-id="5e59e-211">Also, the name of the item is under **Stop Backup** at the top of the blade.</span><span class="sxs-lookup"><span data-stu-id="5e59e-211">Also, the name of the item is under **Stop Backup** at the top of the blade.</span></span>
4. <span data-ttu-id="5e59e-212">Optionally provide a **Reason** or **Comment**.</span><span class="sxs-lookup"><span data-stu-id="5e59e-212">Optionally provide a **Reason** or **Comment**.</span></span>
5. <span data-ttu-id="5e59e-213">To stop the backup job for the current item, click  ![Stop backup button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-vms/stop-backup-button-blue.png)</span><span class="sxs-lookup"><span data-stu-id="5e59e-213">To stop the backup job for the current item, click  ![Stop backup button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-vms/stop-backup-button-blue.png)</span></span>

    <span data-ttu-id="5e59e-214">A notification message lets you know the backup jobs have been stopped.</span><span class="sxs-lookup"><span data-stu-id="5e59e-214">A notification message lets you know the backup jobs have been stopped.</span></span>

    ![Confirm stop protection](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-vms/stop-message.png)

## <a name="resume-protection-of-a-virtual-machine"></a><span data-ttu-id="5e59e-216">Resume protection of a virtual machine</span><span class="sxs-lookup"><span data-stu-id="5e59e-216">Resume protection of a virtual machine</span></span>
<span data-ttu-id="5e59e-217">If the **Retain Backup Data** option was chosen when protection for the virtual machine was stopped, then it is possible to resume protection.</span><span class="sxs-lookup"><span data-stu-id="5e59e-217">If the **Retain Backup Data** option was chosen when protection for the virtual machine was stopped, then it is possible to resume protection.</span></span> <span data-ttu-id="5e59e-218">If the **Delete Backup Data** option was chosen, then protection for the virtual machine cannot resume.</span><span class="sxs-lookup"><span data-stu-id="5e59e-218">If the **Delete Backup Data** option was chosen, then protection for the virtual machine cannot resume.</span></span>

<span data-ttu-id="5e59e-219">To resume protection for the virtual machine</span><span class="sxs-lookup"><span data-stu-id="5e59e-219">To resume protection for the virtual machine</span></span>

1. <span data-ttu-id="5e59e-220">On the [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **Resume backup**.</span><span class="sxs-lookup"><span data-stu-id="5e59e-220">On the [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **Resume backup**.</span></span>

    ![Resume protection](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-vms/resume-backup-button.png)

    <span data-ttu-id="5e59e-222">The Backup Policy blade opens.</span><span class="sxs-lookup"><span data-stu-id="5e59e-222">The Backup Policy blade opens.</span></span>

   > [!NOTE]
   > When re-protecting the virtual machine, you can choose a different policy than the policy with which virtual machine was protected initially.
   >
   >
2. <span data-ttu-id="5e59e-224">Follow the steps in [Manage backup policies](backup-azure-manage-vms.md#manage-backup-policies) to assign the policy for the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="5e59e-224">Follow the steps in [Manage backup policies](backup-azure-manage-vms.md#manage-backup-policies) to assign the policy for the virtual machine.</span></span>

    <span data-ttu-id="5e59e-225">Once the backup policy is applied to the virtual machine, you see the following message.</span><span class="sxs-lookup"><span data-stu-id="5e59e-225">Once the backup policy is applied to the virtual machine, you see the following message.</span></span>

    ![Successfully protected VM](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-vms/success-message.png)

## <a name="delete-backup-data"></a><span data-ttu-id="5e59e-227">Delete Backup data</span><span class="sxs-lookup"><span data-stu-id="5e59e-227">Delete Backup data</span></span>
<span data-ttu-id="5e59e-228">You can delete the backup data associated with a virtual machine during the **Stop backup** job, or anytime after the backup job has completed.</span><span class="sxs-lookup"><span data-stu-id="5e59e-228">You can delete the backup data associated with a virtual machine during the **Stop backup** job, or anytime after the backup job has completed.</span></span> <span data-ttu-id="5e59e-229">It may even be beneficial to wait days or weeks before deleting the recovery points.</span><span class="sxs-lookup"><span data-stu-id="5e59e-229">It may even be beneficial to wait days or weeks before deleting the recovery points.</span></span> <span data-ttu-id="5e59e-230">Unlike restoring recovery points, when deleting backup data, you cannot choose specific recovery points to delete.</span><span class="sxs-lookup"><span data-stu-id="5e59e-230">Unlike restoring recovery points, when deleting backup data, you cannot choose specific recovery points to delete.</span></span> <span data-ttu-id="5e59e-231">If you choose to delete your backup data, you delete all recovery points associated with the item.</span><span class="sxs-lookup"><span data-stu-id="5e59e-231">If you choose to delete your backup data, you delete all recovery points associated with the item.</span></span>

<span data-ttu-id="5e59e-232">The following procedure assumes the Backup job for the virtual machine has been stopped or disabled.</span><span class="sxs-lookup"><span data-stu-id="5e59e-232">The following procedure assumes the Backup job for the virtual machine has been stopped or disabled.</span></span> <span data-ttu-id="5e59e-233">Once the Backup job is disabled, the **Resume backup** and **Delete backup** options are available in the vault item dashboard.</span><span class="sxs-lookup"><span data-stu-id="5e59e-233">Once the Backup job is disabled, the **Resume backup** and **Delete backup** options are available in the vault item dashboard.</span></span>

![Resume and delete buttons](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-vms/resume-delete-buttons.png)

<span data-ttu-id="5e59e-235">To delete backup data on a virtual machine with the *Backup disabled*:</span><span class="sxs-lookup"><span data-stu-id="5e59e-235">To delete backup data on a virtual machine with the *Backup disabled*:</span></span>

1. <span data-ttu-id="5e59e-236">On the [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **Delete backup**.</span><span class="sxs-lookup"><span data-stu-id="5e59e-236">On the [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **Delete backup**.</span></span>

    ![VM Type](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-vms/delete-backup-buttom.png)

    <span data-ttu-id="5e59e-238">The **Delete Backup Data** blade opens.</span><span class="sxs-lookup"><span data-stu-id="5e59e-238">The **Delete Backup Data** blade opens.</span></span>

    ![VM Type](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-vms/delete-backup-blade.png)
2. <span data-ttu-id="5e59e-240">Type the name of the item to confirm you want to delete the recovery points.</span><span class="sxs-lookup"><span data-stu-id="5e59e-240">Type the name of the item to confirm you want to delete the recovery points.</span></span>

    ![Stop verification](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-vms/item-verification-box.png)

    <span data-ttu-id="5e59e-242">If you aren't sure of the item name, hover over the exclamation mark to view the name.</span><span class="sxs-lookup"><span data-stu-id="5e59e-242">If you aren't sure of the item name, hover over the exclamation mark to view the name.</span></span> <span data-ttu-id="5e59e-243">Also, the name of the item is under **Delete Backup Data** at the top of the blade.</span><span class="sxs-lookup"><span data-stu-id="5e59e-243">Also, the name of the item is under **Delete Backup Data** at the top of the blade.</span></span>
3. <span data-ttu-id="5e59e-244">Optionally provide a **Reason** or **Comment**.</span><span class="sxs-lookup"><span data-stu-id="5e59e-244">Optionally provide a **Reason** or **Comment**.</span></span>
4. <span data-ttu-id="5e59e-245">To delete the backup data for the current item, click  ![Stop backup button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-vms/delete-button.png)</span><span class="sxs-lookup"><span data-stu-id="5e59e-245">To delete the backup data for the current item, click  ![Stop backup button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-vms/delete-button.png)</span></span>

    <span data-ttu-id="5e59e-246">A notification message lets you know the backup data has been deleted.</span><span class="sxs-lookup"><span data-stu-id="5e59e-246">A notification message lets you know the backup data has been deleted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5e59e-247">Next steps</span><span class="sxs-lookup"><span data-stu-id="5e59e-247">Next steps</span></span>
<span data-ttu-id="5e59e-248">For information on re-creating a virtual machine from a recovery point, check out [Restore Azure VMs](backup-azure-restore-vms.md).</span><span class="sxs-lookup"><span data-stu-id="5e59e-248">For information on re-creating a virtual machine from a recovery point, check out [Restore Azure VMs](backup-azure-restore-vms.md).</span></span> <span data-ttu-id="5e59e-249">If you need information on protecting your virtual machines, see [First look: Back up VMs to a Recovery Services vault](backup-azure-vms-first-look-arm.md).</span><span class="sxs-lookup"><span data-stu-id="5e59e-249">If you need information on protecting your virtual machines, see [First look: Back up VMs to a Recovery Services vault](backup-azure-vms-first-look-arm.md).</span></span> <span data-ttu-id="5e59e-250">For information on monitoring events, see [Monitor alerts for Azure virtual machine backups](backup-azure-monitor-vms.md).</span><span class="sxs-lookup"><span data-stu-id="5e59e-250">For information on monitoring events, see [Monitor alerts for Azure virtual machine backups](backup-azure-monitor-vms.md).</span></span>


























