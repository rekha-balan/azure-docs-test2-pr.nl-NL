---
title: Recover files from Azure to a Windows Server
description: This tutorial details recovering items from Azure to a Windows Server.
services: backup
author: saurabhsensharma
manager: shivamg
keywords: windows server back up;restore files windows server; back up and disaster recovery
ms.service: backup
ms.topic: tutorial
ms.date: 2/14/2018
ms.author: saurse
ms.custom: mvc
ms.openlocfilehash: e05c80e52605e051bdd6815608ca8c12e1393727
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864486"
---
# <a name="recover-files-from-azure-to-a-windows-server"></a><span data-ttu-id="14cb1-104">Recover files from Azure to a Windows Server</span><span class="sxs-lookup"><span data-stu-id="14cb1-104">Recover files from Azure to a Windows Server</span></span>

<span data-ttu-id="14cb1-105">Azure Backup enables the recovery of individual items from backups of your Windows Server.</span><span class="sxs-lookup"><span data-stu-id="14cb1-105">Azure Backup enables the recovery of individual items from backups of your Windows Server.</span></span> <span data-ttu-id="14cb1-106">Recovering individual files is helpful if you must quickly restore files that are accidentally deleted.</span><span class="sxs-lookup"><span data-stu-id="14cb1-106">Recovering individual files is helpful if you must quickly restore files that are accidentally deleted.</span></span> <span data-ttu-id="14cb1-107">This tutorial covers how you can use the Microsoft Azure Recovery Services Agent (MARS) agent to recover items from backups you have already performed in Azure.</span><span class="sxs-lookup"><span data-stu-id="14cb1-107">This tutorial covers how you can use the Microsoft Azure Recovery Services Agent (MARS) agent to recover items from backups you have already performed in Azure.</span></span> <span data-ttu-id="14cb1-108">In this tutorial you learn how to:</span><span class="sxs-lookup"><span data-stu-id="14cb1-108">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="14cb1-109">Initiate recovery of individual items</span><span class="sxs-lookup"><span data-stu-id="14cb1-109">Initiate recovery of individual items</span></span> 
> * <span data-ttu-id="14cb1-110">Select a recovery point</span><span class="sxs-lookup"><span data-stu-id="14cb1-110">Select a recovery point</span></span> 
> * <span data-ttu-id="14cb1-111">Restore items from a recovery point</span><span class="sxs-lookup"><span data-stu-id="14cb1-111">Restore items from a recovery point</span></span>

<span data-ttu-id="14cb1-112">This tutorial assumes you have already performed the steps to [Back up a Windows Server to Azure](backup-configure-vault.md) and have at least one backup of your Windows Server files in Azure.</span><span class="sxs-lookup"><span data-stu-id="14cb1-112">This tutorial assumes you have already performed the steps to [Back up a Windows Server to Azure](backup-configure-vault.md) and have at least one backup of your Windows Server files in Azure.</span></span>

## <a name="initiate-recovery-of-individual-items"></a><span data-ttu-id="14cb1-113">Initiate recovery of individual items</span><span class="sxs-lookup"><span data-stu-id="14cb1-113">Initiate recovery of individual items</span></span>

<span data-ttu-id="14cb1-114">A helpful user interface wizard named Microsoft Azure Backup is installed with the Microsoft Azure Recovery Services (MARS) agent.</span><span class="sxs-lookup"><span data-stu-id="14cb1-114">A helpful user interface wizard named Microsoft Azure Backup is installed with the Microsoft Azure Recovery Services (MARS) agent.</span></span> <span data-ttu-id="14cb1-115">The Microsoft Azure Backup wizard works with the Microsoft Azure Recovery Services (MARS) agent to retrieve backup data from recovery points stored in Azure.</span><span class="sxs-lookup"><span data-stu-id="14cb1-115">The Microsoft Azure Backup wizard works with the Microsoft Azure Recovery Services (MARS) agent to retrieve backup data from recovery points stored in Azure.</span></span> <span data-ttu-id="14cb1-116">Use the Microsoft Azure Backup wizard to identify the files or folders you want to restore to Windows Server.</span><span class="sxs-lookup"><span data-stu-id="14cb1-116">Use the Microsoft Azure Backup wizard to identify the files or folders you want to restore to Windows Server.</span></span> 

1. <span data-ttu-id="14cb1-117">Open the **Microsoft Azure Backup** snap-in.</span><span class="sxs-lookup"><span data-stu-id="14cb1-117">Open the **Microsoft Azure Backup** snap-in.</span></span> <span data-ttu-id="14cb1-118">You can find it by searching your machine for **Microsoft Azure Backup**.</span><span class="sxs-lookup"><span data-stu-id="14cb1-118">You can find it by searching your machine for **Microsoft Azure Backup**.</span></span>

    ![Backup pending](./media/tutorial-backup-restore-files-windows-server/mars.png)

2. <span data-ttu-id="14cb1-120">In the wizard, click **Recover Data** in the **Actions Pane** of the agent console to start the **Recover Data** wizard.</span><span class="sxs-lookup"><span data-stu-id="14cb1-120">In the wizard, click **Recover Data** in the **Actions Pane** of the agent console to start the **Recover Data** wizard.</span></span>

    ![Backup pending](./media/tutorial-backup-restore-files-windows-server/mars-recover-data.png)

3. <span data-ttu-id="14cb1-122">On the **Getting Started** page, select **This server (server name)** and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="14cb1-122">On the **Getting Started** page, select **This server (server name)** and click **Next**.</span></span>

4. <span data-ttu-id="14cb1-123">On the **Select Recovery Mode** page, select **Individual files and folders** and then click **Next** to begin the recovery point selection process.</span><span class="sxs-lookup"><span data-stu-id="14cb1-123">On the **Select Recovery Mode** page, select **Individual files and folders** and then click **Next** to begin the recovery point selection process.</span></span>
 
5. <span data-ttu-id="14cb1-124">On the **Select Volume and Date** page, select the volume that contains the files or folders you want to restore, and click **Mount**.</span><span class="sxs-lookup"><span data-stu-id="14cb1-124">On the **Select Volume and Date** page, select the volume that contains the files or folders you want to restore, and click **Mount**.</span></span> <span data-ttu-id="14cb1-125">Select a date, and select a time from the drop-down menu that corresponds to a recovery point.</span><span class="sxs-lookup"><span data-stu-id="14cb1-125">Select a date, and select a time from the drop-down menu that corresponds to a recovery point.</span></span> <span data-ttu-id="14cb1-126">Dates in **bold** indicate the availability of at least one recovery point on that day.</span><span class="sxs-lookup"><span data-stu-id="14cb1-126">Dates in **bold** indicate the availability of at least one recovery point on that day.</span></span>

    ![Backup pending](./media/tutorial-backup-restore-files-windows-server/mars-select-date.png)
 
    <span data-ttu-id="14cb1-128">When you click **Mount**, Azure Backup makes the recovery point available as a disk.</span><span class="sxs-lookup"><span data-stu-id="14cb1-128">When you click **Mount**, Azure Backup makes the recovery point available as a disk.</span></span> <span data-ttu-id="14cb1-129">Browse and recover files from the disk.</span><span class="sxs-lookup"><span data-stu-id="14cb1-129">Browse and recover files from the disk.</span></span>

## <a name="restore-items-from-a-recovery-point"></a><span data-ttu-id="14cb1-130">Restore items from a recovery point</span><span class="sxs-lookup"><span data-stu-id="14cb1-130">Restore items from a recovery point</span></span>

1. <span data-ttu-id="14cb1-131">Once the recovery volume is mounted, click **Browse** to open Windows Explorer and find the files and folders you wish to recover.</span><span class="sxs-lookup"><span data-stu-id="14cb1-131">Once the recovery volume is mounted, click **Browse** to open Windows Explorer and find the files and folders you wish to recover.</span></span> 

    ![Backup pending](./media/tutorial-backup-restore-files-windows-server/mars-browse-recover.png)

    <span data-ttu-id="14cb1-133">You can open the files directly from the recovery volume and verify the files.</span><span class="sxs-lookup"><span data-stu-id="14cb1-133">You can open the files directly from the recovery volume and verify the files.</span></span>

2. <span data-ttu-id="14cb1-134">In Windows Explorer, copy the files and/or folders you want to restore and paste them to any desired location on the server.</span><span class="sxs-lookup"><span data-stu-id="14cb1-134">In Windows Explorer, copy the files and/or folders you want to restore and paste them to any desired location on the server.</span></span>

    ![Backup pending](./media/tutorial-backup-restore-files-windows-server/mars-final.png)

3. <span data-ttu-id="14cb1-136">When you are finished restoring the files and/or folders, on the **Browse and Recovery Files** page of the **Recover Data** wizard, click **Unmount**.</span><span class="sxs-lookup"><span data-stu-id="14cb1-136">When you are finished restoring the files and/or folders, on the **Browse and Recovery Files** page of the **Recover Data** wizard, click **Unmount**.</span></span> 

    ![Backup pending](./media/tutorial-backup-restore-files-windows-server/unmount-and-confirm.png)

4.  <span data-ttu-id="14cb1-138">Click **Yes** to confirm that you want to unmount the volume.</span><span class="sxs-lookup"><span data-stu-id="14cb1-138">Click **Yes** to confirm that you want to unmount the volume.</span></span>

    <span data-ttu-id="14cb1-139">Once the snapshot is unmounted, **Job Completed** appears in the **Jobs** pane in the agent console.</span><span class="sxs-lookup"><span data-stu-id="14cb1-139">Once the snapshot is unmounted, **Job Completed** appears in the **Jobs** pane in the agent console.</span></span>

## <a name="next-steps"></a><span data-ttu-id="14cb1-140">Next steps</span><span class="sxs-lookup"><span data-stu-id="14cb1-140">Next steps</span></span>

<span data-ttu-id="14cb1-141">This completes the tutorials on backing up and restoring Windows Server data to Azure.</span><span class="sxs-lookup"><span data-stu-id="14cb1-141">This completes the tutorials on backing up and restoring Windows Server data to Azure.</span></span> <span data-ttu-id="14cb1-142">To learn more about Azure Backup, see the PowerShell sample for backing up encrypted virtual machines.</span><span class="sxs-lookup"><span data-stu-id="14cb1-142">To learn more about Azure Backup, see the PowerShell sample for backing up encrypted virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="14cb1-143">Back up encrypted VM</span><span class="sxs-lookup"><span data-stu-id="14cb1-143">Back up encrypted VM</span></span>](./scripts/backup-powershell-sample-backup-encrypted-vm.md)
