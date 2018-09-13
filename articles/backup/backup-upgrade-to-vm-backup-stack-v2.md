---
title: Upgrade to the Azure VM Backup Stack V2
description: Upgrade process and FAQs for VM backup stack, Resource Manager deployment model
services: backup
author: trinadhk
manager: vijayts
tags: azure-resource-manager, virtual-machine-backup
ms.service: backup
ms.topic: conceptual
ms.date: 8/1/2018
ms.author: trinadhk
ms.openlocfilehash: 1021900620272cc5476d8972daf9d7e0a161797a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871523"
---
# <a name="upgrade-to-azure-vm-backup-stack-v2"></a><span data-ttu-id="faafb-103">Upgrade to Azure VM Backup stack V2</span><span class="sxs-lookup"><span data-stu-id="faafb-103">Upgrade to Azure VM Backup stack V2</span></span>

<span data-ttu-id="faafb-104">The Resource Manager deployment model for the upgrade to virtual machine (VM) backup stack provides the following feature enhancements:</span><span class="sxs-lookup"><span data-stu-id="faafb-104">The Resource Manager deployment model for the upgrade to virtual machine (VM) backup stack provides the following feature enhancements:</span></span>

* <span data-ttu-id="faafb-105">Ability to see snapshots taken as part of a backup job that's available for recovery without waiting for data transfer to finish.</span><span class="sxs-lookup"><span data-stu-id="faafb-105">Ability to see snapshots taken as part of a backup job that's available for recovery without waiting for data transfer to finish.</span></span> <span data-ttu-id="faafb-106">It reduces the wait time for snapshots to copy to the vault before triggering restore.</span><span class="sxs-lookup"><span data-stu-id="faafb-106">It reduces the wait time for snapshots to copy to the vault before triggering restore.</span></span> <span data-ttu-id="faafb-107">Also, this ability eliminates the additional storage requirement for backing up premium VMs, except for the first backup.</span><span class="sxs-lookup"><span data-stu-id="faafb-107">Also, this ability eliminates the additional storage requirement for backing up premium VMs, except for the first backup.</span></span>  

* <span data-ttu-id="faafb-108">Reduces backup and restore times by retaining snapshots locally, for seven days.</span><span class="sxs-lookup"><span data-stu-id="faafb-108">Reduces backup and restore times by retaining snapshots locally, for seven days.</span></span>

* <span data-ttu-id="faafb-109">Support for disk sizes up to 4 TB.</span><span class="sxs-lookup"><span data-stu-id="faafb-109">Support for disk sizes up to 4 TB.</span></span>

* <span data-ttu-id="faafb-110">Ability to use an unmanaged VM's original storage accounts, when restoring.</span><span class="sxs-lookup"><span data-stu-id="faafb-110">Ability to use an unmanaged VM's original storage accounts, when restoring.</span></span> <span data-ttu-id="faafb-111">This ability exists even when the VM has disks that are distributed across storage accounts.</span><span class="sxs-lookup"><span data-stu-id="faafb-111">This ability exists even when the VM has disks that are distributed across storage accounts.</span></span> <span data-ttu-id="faafb-112">It speeds up restore operations for a wide variety of VM configurations.</span><span class="sxs-lookup"><span data-stu-id="faafb-112">It speeds up restore operations for a wide variety of VM configurations.</span></span>
    > [!NOTE]
    > <span data-ttu-id="faafb-113">This ability is not the same as overriding the original VM.</span><span class="sxs-lookup"><span data-stu-id="faafb-113">This ability is not the same as overriding the original VM.</span></span> 
    >

## <a name="whats-changing-in-the-new-stack"></a><span data-ttu-id="faafb-114">What's changing in the new stack?</span><span class="sxs-lookup"><span data-stu-id="faafb-114">What's changing in the new stack?</span></span>
<span data-ttu-id="faafb-115">Currently, the backup job consists of two phases:</span><span class="sxs-lookup"><span data-stu-id="faafb-115">Currently, the backup job consists of two phases:</span></span>
1.  <span data-ttu-id="faafb-116">Taking a VM snapshot.</span><span class="sxs-lookup"><span data-stu-id="faafb-116">Taking a VM snapshot.</span></span> 
2.  <span data-ttu-id="faafb-117">Transferring a VM snapshot to the Azure Backup vault.</span><span class="sxs-lookup"><span data-stu-id="faafb-117">Transferring a VM snapshot to the Azure Backup vault.</span></span> 

<span data-ttu-id="faafb-118">A recovery point is considered created only after phases 1 and 2 are done.</span><span class="sxs-lookup"><span data-stu-id="faafb-118">A recovery point is considered created only after phases 1 and 2 are done.</span></span> <span data-ttu-id="faafb-119">As part of the new stack, a recovery point is created as soon as the snapshot is finished.</span><span class="sxs-lookup"><span data-stu-id="faafb-119">As part of the new stack, a recovery point is created as soon as the snapshot is finished.</span></span> <span data-ttu-id="faafb-120">You can also restore from this recovery point by using the same restore flow.</span><span class="sxs-lookup"><span data-stu-id="faafb-120">You can also restore from this recovery point by using the same restore flow.</span></span> <span data-ttu-id="faafb-121">You can identify this recovery point in the Azure portal by using “snapshot” as the recovery point type.</span><span class="sxs-lookup"><span data-stu-id="faafb-121">You can identify this recovery point in the Azure portal by using “snapshot” as the recovery point type.</span></span> <span data-ttu-id="faafb-122">After the snapshot is transferred to the vault, the recovery point type changes to “snapshot and vault.”</span><span class="sxs-lookup"><span data-stu-id="faafb-122">After the snapshot is transferred to the vault, the recovery point type changes to “snapshot and vault.”</span></span> 

![Backup job in VM backup stack Resource Manager deployment model--storage and vault](./media/backup-azure-vms/instant-rp-flow.jpg) 

<span data-ttu-id="faafb-124">By default, snapshots are kept for seven days.</span><span class="sxs-lookup"><span data-stu-id="faafb-124">By default, snapshots are kept for seven days.</span></span> <span data-ttu-id="faafb-125">This feature allows the restore to finish faster from these snapshots.</span><span class="sxs-lookup"><span data-stu-id="faafb-125">This feature allows the restore to finish faster from these snapshots.</span></span> <span data-ttu-id="faafb-126">It reduces the time that's required to copy data back from the vault to the customer's storage account.</span><span class="sxs-lookup"><span data-stu-id="faafb-126">It reduces the time that's required to copy data back from the vault to the customer's storage account.</span></span> 

## <a name="considerations-before-upgrade"></a><span data-ttu-id="faafb-127">Considerations before upgrade</span><span class="sxs-lookup"><span data-stu-id="faafb-127">Considerations before upgrade</span></span>

* <span data-ttu-id="faafb-128">The upgrade of the VM backup stack is one directional, all backups go into this flow.</span><span class="sxs-lookup"><span data-stu-id="faafb-128">The upgrade of the VM backup stack is one directional, all backups go into this flow.</span></span> <span data-ttu-id="faafb-129">Because the change occurs at the subscription level, all VMs go into this flow.</span><span class="sxs-lookup"><span data-stu-id="faafb-129">Because the change occurs at the subscription level, all VMs go into this flow.</span></span> <span data-ttu-id="faafb-130">All new feature additions are based on the same stack.</span><span class="sxs-lookup"><span data-stu-id="faafb-130">All new feature additions are based on the same stack.</span></span> <span data-ttu-id="faafb-131">Currently you can't control the stack at policy level.</span><span class="sxs-lookup"><span data-stu-id="faafb-131">Currently you can't control the stack at policy level.</span></span>

* <span data-ttu-id="faafb-132">Snapshots are stored locally to boost recovery point creation and also to speed up restore operations.</span><span class="sxs-lookup"><span data-stu-id="faafb-132">Snapshots are stored locally to boost recovery point creation and also to speed up restore operations.</span></span> <span data-ttu-id="faafb-133">As a result, you'll see storage costs that correspond to snapshots taken during the seven-day period.</span><span class="sxs-lookup"><span data-stu-id="faafb-133">As a result, you'll see storage costs that correspond to snapshots taken during the seven-day period.</span></span>

* <span data-ttu-id="faafb-134">Incremental snapshots are stored as page blobs.</span><span class="sxs-lookup"><span data-stu-id="faafb-134">Incremental snapshots are stored as page blobs.</span></span> <span data-ttu-id="faafb-135">All customers that use unmanaged disks are charged for the seven days the snapshots are stored in the customer's local storage account.</span><span class="sxs-lookup"><span data-stu-id="faafb-135">All customers that use unmanaged disks are charged for the seven days the snapshots are stored in the customer's local storage account.</span></span> <span data-ttu-id="faafb-136">Since the restore point collections used by Managed VM backups use blob snapshots at the underlying storage level, for managed disks you will see costs corresponding to [blob snapshot pricing](https://docs.microsoft.com/rest/api/storageservices/understanding-how-snapshots-accrue-charges) and they are incremental.</span><span class="sxs-lookup"><span data-stu-id="faafb-136">Since the restore point collections used by Managed VM backups use blob snapshots at the underlying storage level, for managed disks you will see costs corresponding to [blob snapshot pricing](https://docs.microsoft.com/rest/api/storageservices/understanding-how-snapshots-accrue-charges) and they are incremental.</span></span> 

* <span data-ttu-id="faafb-137">If you restore a premium VM from a snapshot recovery point, a temporary storage location is used while the VM is created.</span><span class="sxs-lookup"><span data-stu-id="faafb-137">If you restore a premium VM from a snapshot recovery point, a temporary storage location is used while the VM is created.</span></span>

* <span data-ttu-id="faafb-138">For premium storage accounts, the snapshots taken for instant recovery points count towards the 10-TB limit of allocated space.</span><span class="sxs-lookup"><span data-stu-id="faafb-138">For premium storage accounts, the snapshots taken for instant recovery points count towards the 10-TB limit of allocated space.</span></span>

## <a name="upgrade"></a><span data-ttu-id="faafb-139">Upgrade</span><span class="sxs-lookup"><span data-stu-id="faafb-139">Upgrade</span></span>
### <a name="the-azure-portal"></a><span data-ttu-id="faafb-140">The Azure portal</span><span class="sxs-lookup"><span data-stu-id="faafb-140">The Azure portal</span></span>
<span data-ttu-id="faafb-141">If you use the Azure portal, you see a notification on the vault dashboard.</span><span class="sxs-lookup"><span data-stu-id="faafb-141">If you use the Azure portal, you see a notification on the vault dashboard.</span></span> <span data-ttu-id="faafb-142">This notification relates to large-disk support and backup and restore speed improvements.</span><span class="sxs-lookup"><span data-stu-id="faafb-142">This notification relates to large-disk support and backup and restore speed improvements.</span></span> <span data-ttu-id="faafb-143">Alternatively you can go to Properties page of the vault to get the upgrade option.</span><span class="sxs-lookup"><span data-stu-id="faafb-143">Alternatively you can go to Properties page of the vault to get the upgrade option.</span></span>

![Backup job in VM backup stack Resource Manager deployment model--support notification](./media/backup-azure-vms/instant-rp-banner.png) 

<span data-ttu-id="faafb-145">To open a screen for upgrading to the new stack, select the banner.</span><span class="sxs-lookup"><span data-stu-id="faafb-145">To open a screen for upgrading to the new stack, select the banner.</span></span> 

![Backup job in VM backup stack Resource Manager deployment model--upgrade](./media/backup-azure-vms/instant-rp.png) 

### <a name="powershell"></a><span data-ttu-id="faafb-147">PowerShell</span><span class="sxs-lookup"><span data-stu-id="faafb-147">PowerShell</span></span>
<span data-ttu-id="faafb-148">Run the following cmdlets from an elevated PowerShell terminal:</span><span class="sxs-lookup"><span data-stu-id="faafb-148">Run the following cmdlets from an elevated PowerShell terminal:</span></span>
1.  <span data-ttu-id="faafb-149">Sign in to your Azure account:</span><span class="sxs-lookup"><span data-stu-id="faafb-149">Sign in to your Azure account:</span></span> 

    ```
    PS C:> Connect-AzureRmAccount
    ```

2.  <span data-ttu-id="faafb-150">Select the subscription that you want to register:</span><span class="sxs-lookup"><span data-stu-id="faafb-150">Select the subscription that you want to register:</span></span>

    ```
    PS C:>  Get-AzureRmSubscription –SubscriptionName "Subscription Name" | Select-AzureRmSubscription
    ```

3.  <span data-ttu-id="faafb-151">Register this subscription:</span><span class="sxs-lookup"><span data-stu-id="faafb-151">Register this subscription:</span></span>

    ```
    PS C:>  Register-AzureRmProviderFeature -FeatureName "InstantBackupandRecovery" –ProviderNamespace Microsoft.RecoveryServices
    ```

## <a name="verify-that-the-upgrade-is-finished"></a><span data-ttu-id="faafb-152">Verify that the upgrade is finished</span><span class="sxs-lookup"><span data-stu-id="faafb-152">Verify that the upgrade is finished</span></span>
<span data-ttu-id="faafb-153">From an elevated PowerShell terminal, run the following cmdlet:</span><span class="sxs-lookup"><span data-stu-id="faafb-153">From an elevated PowerShell terminal, run the following cmdlet:</span></span>

```
Get-AzureRmProviderFeature -FeatureName "InstantBackupandRecovery" –ProviderNamespace Microsoft.RecoveryServices
```

<span data-ttu-id="faafb-154">If it says "Registered," then your subscription is upgraded to VM backup stack Resource Manager deployment model.</span><span class="sxs-lookup"><span data-stu-id="faafb-154">If it says "Registered," then your subscription is upgraded to VM backup stack Resource Manager deployment model.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="faafb-155">Frequently asked questions</span><span class="sxs-lookup"><span data-stu-id="faafb-155">Frequently asked questions</span></span>

<span data-ttu-id="faafb-156">The following questions and answers have been collected from forums and customer questions.</span><span class="sxs-lookup"><span data-stu-id="faafb-156">The following questions and answers have been collected from forums and customer questions.</span></span>

### <a name="will-upgrading-to-v2-impact-current-backups"></a><span data-ttu-id="faafb-157">Will upgrading to V2 impact current backups?</span><span class="sxs-lookup"><span data-stu-id="faafb-157">Will upgrading to V2 impact current backups?</span></span>

<span data-ttu-id="faafb-158">If you upgrade to V2, there's no impact to your current backups, and no need to reconfigure your environment.</span><span class="sxs-lookup"><span data-stu-id="faafb-158">If you upgrade to V2, there's no impact to your current backups, and no need to reconfigure your environment.</span></span> <span data-ttu-id="faafb-159">Upgrade and your backup environment continues to work as it has.</span><span class="sxs-lookup"><span data-stu-id="faafb-159">Upgrade and your backup environment continues to work as it has.</span></span>

### <a name="what-does-it-cost-to-upgrade-to-azure-vm-backup-stack-v2"></a><span data-ttu-id="faafb-160">What does it cost to upgrade to Azure VM Backup stack v2?</span><span class="sxs-lookup"><span data-stu-id="faafb-160">What does it cost to upgrade to Azure VM Backup stack v2?</span></span>

<span data-ttu-id="faafb-161">There is no cost to upgrade the stack to v2.</span><span class="sxs-lookup"><span data-stu-id="faafb-161">There is no cost to upgrade the stack to v2.</span></span> <span data-ttu-id="faafb-162">Snapshots are stored locally to speed up recovery point creation, and restore operations.</span><span class="sxs-lookup"><span data-stu-id="faafb-162">Snapshots are stored locally to speed up recovery point creation, and restore operations.</span></span> <span data-ttu-id="faafb-163">As a result, you'll see storage costs that correspond to the snapshots taken during the seven-day period.</span><span class="sxs-lookup"><span data-stu-id="faafb-163">As a result, you'll see storage costs that correspond to the snapshots taken during the seven-day period.</span></span>

### <a name="does-upgrading-to-stack-v2-increase-the-premium-storage-account-snapshot-limit-by-10-tb"></a><span data-ttu-id="faafb-164">Does upgrading to stack v2 increase the premium storage account snapshot limit by 10 TB?</span><span class="sxs-lookup"><span data-stu-id="faafb-164">Does upgrading to stack v2 increase the premium storage account snapshot limit by 10 TB?</span></span>

<span data-ttu-id="faafb-165">No, total snapshot limit per storage account still remains at 10TB.</span><span class="sxs-lookup"><span data-stu-id="faafb-165">No, total snapshot limit per storage account still remains at 10TB.</span></span> 

### <a name="in-premium-storage-accounts-do-snapshots-taken-for-instant-recovery-point-occupy-the-10-tb-snapshot-limit"></a><span data-ttu-id="faafb-166">In Premium Storage accounts, do snapshots taken for instant recovery point occupy the 10 TB snapshot limit?</span><span class="sxs-lookup"><span data-stu-id="faafb-166">In Premium Storage accounts, do snapshots taken for instant recovery point occupy the 10 TB snapshot limit?</span></span>

<span data-ttu-id="faafb-167">Yes, for premium storage accounts, the snapshots taken for instant recovery point, occupy the allocated 10 TB of space.</span><span class="sxs-lookup"><span data-stu-id="faafb-167">Yes, for premium storage accounts, the snapshots taken for instant recovery point, occupy the allocated 10 TB of space.</span></span>

### <a name="how-does-the-snapshot-work-during-the-seven-day-period"></a><span data-ttu-id="faafb-168">How does the snapshot work during the seven-day period?</span><span class="sxs-lookup"><span data-stu-id="faafb-168">How does the snapshot work during the seven-day period?</span></span> 

<span data-ttu-id="faafb-169">Each day a new snapshot is taken.</span><span class="sxs-lookup"><span data-stu-id="faafb-169">Each day a new snapshot is taken.</span></span> <span data-ttu-id="faafb-170">There are seven individual snapshots.</span><span class="sxs-lookup"><span data-stu-id="faafb-170">There are seven individual snapshots.</span></span> <span data-ttu-id="faafb-171">The service does **not** take a copy on the first day, and add changes for the next six days.</span><span class="sxs-lookup"><span data-stu-id="faafb-171">The service does **not** take a copy on the first day, and add changes for the next six days.</span></span>

### <a name="is-a-v2-snapshot-an-incremental-snapshot-or-full-snapshot"></a><span data-ttu-id="faafb-172">Is a v2 snapshot an incremental snapshot or full snapshot?</span><span class="sxs-lookup"><span data-stu-id="faafb-172">Is a v2 snapshot an incremental snapshot or full snapshot?</span></span>

<span data-ttu-id="faafb-173">Incremental snapshots are used for unmanaged disks.</span><span class="sxs-lookup"><span data-stu-id="faafb-173">Incremental snapshots are used for unmanaged disks.</span></span> <span data-ttu-id="faafb-174">For managed disks, restore point collection created by Azure Backup uses blob snapshots and hence are incremental.</span><span class="sxs-lookup"><span data-stu-id="faafb-174">For managed disks, restore point collection created by Azure Backup uses blob snapshots and hence are incremental.</span></span> 
