---
title: Back up Azure VMs | Microsoft Docs
description: Discover, register, and back up Azure virtual machines to a recovery services vault.
services: backup
documentationcenter: ''
author: markgalioto
manager: carmonm
editor: ''
keywords: virtual machine backup; back up virtual machine; backup and disaster recovery; arm vm backup
ms.assetid: 5c68481d-7be3-4e68-b87c-0961c267053e
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 2/15/2017
ms.author: trinadhk;jimpark;markgal;
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 34be93d284c470285d9906236f4c70ac24f45fe8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662474"
---
# <a name="back-up-azure-virtual-machines-to-a-recovery-services-vault"></a><span data-ttu-id="39b9e-104">Back up Azure virtual machines to a Recovery Services vault</span><span class="sxs-lookup"><span data-stu-id="39b9e-104">Back up Azure virtual machines to a Recovery Services vault</span></span>
> [!div class="op_single_selector"]
> * [Back up VMs to Recovery Services vault](backup-azure-arm-vms.md)
> * [Back up VMs to Backup vault](backup-azure-vms.md)
>
>

<span data-ttu-id="39b9e-107">This article details how to back up Azure VMs (both Resource Manager-deployed and Classic-deployed) to a Recovery Services vault.</span><span class="sxs-lookup"><span data-stu-id="39b9e-107">This article details how to back up Azure VMs (both Resource Manager-deployed and Classic-deployed) to a Recovery Services vault.</span></span> <span data-ttu-id="39b9e-108">Most of the work for backing up VMs is the preparation.</span><span class="sxs-lookup"><span data-stu-id="39b9e-108">Most of the work for backing up VMs is the preparation.</span></span> <span data-ttu-id="39b9e-109">Before you can back up or protect a VM, you must complete the [prerequisites](backup-azure-arm-vms-prepare.md) to prepare your environment for protecting your VMs.</span><span class="sxs-lookup"><span data-stu-id="39b9e-109">Before you can back up or protect a VM, you must complete the [prerequisites](backup-azure-arm-vms-prepare.md) to prepare your environment for protecting your VMs.</span></span> <span data-ttu-id="39b9e-110">Once you have completed the prerequisites, then you can initiate the backup operation to take snapshots of your VM.</span><span class="sxs-lookup"><span data-stu-id="39b9e-110">Once you have completed the prerequisites, then you can initiate the backup operation to take snapshots of your VM.</span></span>


[!INCLUDE [learn about backup deployment models](../../includes/backup-deployment-models.md)]

<span data-ttu-id="39b9e-111">For more information, see the articles on [planning your VM backup infrastructure in Azure](backup-azure-vms-introduction.md) and [Azure virtual machines](https://azure.microsoft.com/documentation/services/virtual-machines/).</span><span class="sxs-lookup"><span data-stu-id="39b9e-111">For more information, see the articles on [planning your VM backup infrastructure in Azure](backup-azure-vms-introduction.md) and [Azure virtual machines](https://azure.microsoft.com/documentation/services/virtual-machines/).</span></span>

## <a name="triggering-the-backup-job"></a><span data-ttu-id="39b9e-112">Triggering the backup job</span><span class="sxs-lookup"><span data-stu-id="39b9e-112">Triggering the backup job</span></span>
<span data-ttu-id="39b9e-113">The backup policy associated with the Recovery Services vault defines how often and when the backup operation runs.</span><span class="sxs-lookup"><span data-stu-id="39b9e-113">The backup policy associated with the Recovery Services vault defines how often and when the backup operation runs.</span></span> <span data-ttu-id="39b9e-114">By default, the first scheduled backup is the initial backup.</span><span class="sxs-lookup"><span data-stu-id="39b9e-114">By default, the first scheduled backup is the initial backup.</span></span> <span data-ttu-id="39b9e-115">Until the initial backup occurs, the Last Backup Status on the **Backup Jobs** blade shows as **Warning(initial backup pending)**.</span><span class="sxs-lookup"><span data-stu-id="39b9e-115">Until the initial backup occurs, the Last Backup Status on the **Backup Jobs** blade shows as **Warning(initial backup pending)**.</span></span>

![Backup pending](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms-first-look-arm/initial-backup-not-run.png)

<span data-ttu-id="39b9e-117">Unless your initial backup is due to begin soon, it is recommended that you run **Back up Now**.</span><span class="sxs-lookup"><span data-stu-id="39b9e-117">Unless your initial backup is due to begin soon, it is recommended that you run **Back up Now**.</span></span> <span data-ttu-id="39b9e-118">The following procedure starts from the vault dashboard.</span><span class="sxs-lookup"><span data-stu-id="39b9e-118">The following procedure starts from the vault dashboard.</span></span> <span data-ttu-id="39b9e-119">This procedure serves for running the initial backup job after you have completed all prerequisites.</span><span class="sxs-lookup"><span data-stu-id="39b9e-119">This procedure serves for running the initial backup job after you have completed all prerequisites.</span></span> <span data-ttu-id="39b9e-120">If the initial backup job has already been run, this procedure is not available.</span><span class="sxs-lookup"><span data-stu-id="39b9e-120">If the initial backup job has already been run, this procedure is not available.</span></span> <span data-ttu-id="39b9e-121">The associated backup policy determines the next backup job.</span><span class="sxs-lookup"><span data-stu-id="39b9e-121">The associated backup policy determines the next backup job.</span></span>  

<span data-ttu-id="39b9e-122">To run the initial backup job:</span><span class="sxs-lookup"><span data-stu-id="39b9e-122">To run the initial backup job:</span></span>

1. <span data-ttu-id="39b9e-123">On the vault dashboard, click the number under **Backup Items**, or click the **Backup Items** tile.</span><span class="sxs-lookup"><span data-stu-id="39b9e-123">On the vault dashboard, click the number under **Backup Items**, or click the **Backup Items** tile.</span></span> <br/>
  <span data-ttu-id="39b9e-124">![Settings icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms-first-look-arm/rs-vault-config-vm-back-up-now-1.png)</span><span class="sxs-lookup"><span data-stu-id="39b9e-124">![Settings icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms-first-look-arm/rs-vault-config-vm-back-up-now-1.png)</span></span>

  <span data-ttu-id="39b9e-125">The **Backup Items** blade opens.</span><span class="sxs-lookup"><span data-stu-id="39b9e-125">The **Backup Items** blade opens.</span></span>

  ![Back up items](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms-first-look-arm/back-up-items-list.png)

2. <span data-ttu-id="39b9e-127">On the **Backup Items** blade, select the item.</span><span class="sxs-lookup"><span data-stu-id="39b9e-127">On the **Backup Items** blade, select the item.</span></span>

  ![Settings icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms-first-look-arm/back-up-items-list-selected.png)

  <span data-ttu-id="39b9e-129">The **Backup Items** list opens.</span><span class="sxs-lookup"><span data-stu-id="39b9e-129">The **Backup Items** list opens.</span></span> <br/>

  ![Backup job triggered](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms-first-look-arm/backup-items-not-run.png)

3. <span data-ttu-id="39b9e-131">On the **Backup Items** list, click the ellipses **...** to open the Context menu.</span><span class="sxs-lookup"><span data-stu-id="39b9e-131">On the **Backup Items** list, click the ellipses **...** to open the Context menu.</span></span>

  ![Context menu](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms-first-look-arm/context-menu.png)

  <span data-ttu-id="39b9e-133">The Context menu appears.</span><span class="sxs-lookup"><span data-stu-id="39b9e-133">The Context menu appears.</span></span>

  ![Context menu](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms-first-look-arm/context-menu-small.png)

4. <span data-ttu-id="39b9e-135">On the Context menu, click **Backup now**.</span><span class="sxs-lookup"><span data-stu-id="39b9e-135">On the Context menu, click **Backup now**.</span></span>

  ![Context menu](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms-first-look-arm/context-menu-small-backup-now.png)

  <span data-ttu-id="39b9e-137">The Backup Now blade opens.</span><span class="sxs-lookup"><span data-stu-id="39b9e-137">The Backup Now blade opens.</span></span>

  ![shows the Backup Now blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms-first-look-arm/backup-now-blade-short.png)

5. <span data-ttu-id="39b9e-139">On the Backup Now blade, click the calendar icon, use the calendar control to select the last day this recovery point is retained, and click **Backup**.</span><span class="sxs-lookup"><span data-stu-id="39b9e-139">On the Backup Now blade, click the calendar icon, use the calendar control to select the last day this recovery point is retained, and click **Backup**.</span></span>

  ![set the last day the Backup Now recovery point is retained](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms-first-look-arm/backup-now-blade-calendar.png)

  <span data-ttu-id="39b9e-141">Deployment notifications let you know the backup job has been triggered, and that you can monitor the progress of the job on the Backup jobs page.</span><span class="sxs-lookup"><span data-stu-id="39b9e-141">Deployment notifications let you know the backup job has been triggered, and that you can monitor the progress of the job on the Backup jobs page.</span></span> <span data-ttu-id="39b9e-142">Depending on the size of your VM, creating the initial backup may take a while.</span><span class="sxs-lookup"><span data-stu-id="39b9e-142">Depending on the size of your VM, creating the initial backup may take a while.</span></span>

6. <span data-ttu-id="39b9e-143">To view or track the status of the initial backup, on the vault dashboard, on the **Backup Jobs** tile click **In progress**.</span><span class="sxs-lookup"><span data-stu-id="39b9e-143">To view or track the status of the initial backup, on the vault dashboard, on the **Backup Jobs** tile click **In progress**.</span></span>

  ![Backup Jobs tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms-first-look-arm/open-backup-jobs-1.png)

  <span data-ttu-id="39b9e-145">The Backup Jobs blade opens.</span><span class="sxs-lookup"><span data-stu-id="39b9e-145">The Backup Jobs blade opens.</span></span>

  ![Backup Jobs tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms-first-look-arm/backup-jobs-in-jobs-view-1.png)

  <span data-ttu-id="39b9e-147">In the **Backup jobs** blade, you can see the status of all jobs.</span><span class="sxs-lookup"><span data-stu-id="39b9e-147">In the **Backup jobs** blade, you can see the status of all jobs.</span></span> <span data-ttu-id="39b9e-148">Check if the backup job for your VM is still in progress, or if it has finished.</span><span class="sxs-lookup"><span data-stu-id="39b9e-148">Check if the backup job for your VM is still in progress, or if it has finished.</span></span> <span data-ttu-id="39b9e-149">When a backup job is finished, the status is *Completed*.</span><span class="sxs-lookup"><span data-stu-id="39b9e-149">When a backup job is finished, the status is *Completed*.</span></span>

  > [!NOTE]
  > As a part of the backup operation, the Azure Backup service issues a command to the backup extension in each VM to flush all writes and take a consistent snapshot.
  >
  >

## <a name="troubleshooting-errors"></a><span data-ttu-id="39b9e-151">Troubleshooting errors</span><span class="sxs-lookup"><span data-stu-id="39b9e-151">Troubleshooting errors</span></span>
<span data-ttu-id="39b9e-152">If you run into issues while backing up your virtual machine, see the [VM troubleshooting article](backup-azure-vms-troubleshoot.md) for help.</span><span class="sxs-lookup"><span data-stu-id="39b9e-152">If you run into issues while backing up your virtual machine, see the [VM troubleshooting article](backup-azure-vms-troubleshoot.md) for help.</span></span>

## <a name="next-steps"></a><span data-ttu-id="39b9e-153">Next steps</span><span class="sxs-lookup"><span data-stu-id="39b9e-153">Next steps</span></span>
<span data-ttu-id="39b9e-154">Now that you have protected your VM, see the following articles to learn about VM management tasks, and how to restore VMs.</span><span class="sxs-lookup"><span data-stu-id="39b9e-154">Now that you have protected your VM, see the following articles to learn about VM management tasks, and how to restore VMs.</span></span>

* [<span data-ttu-id="39b9e-155">Manage and monitor your virtual machines</span><span class="sxs-lookup"><span data-stu-id="39b9e-155">Manage and monitor your virtual machines</span></span>](backup-azure-manage-vms.md)
* [<span data-ttu-id="39b9e-156">Restore virtual machines</span><span class="sxs-lookup"><span data-stu-id="39b9e-156">Restore virtual machines</span></span>](backup-azure-arm-restore-vms.md)












