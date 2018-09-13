---
title: Back up an Exchange server to Azure Backup with Azure Backup Server | Microsoft Docs
description: Learn how to back up an Exchange server to Azure Backup using Azure Backup Server
services: backup
documentationcenter: ''
author: pvrk
manager: shivamg
editor: ''
ms.assetid: e46557e8-2eaf-4ee0-99ea-00fbb8687dca
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: pullabhk
ms.openlocfilehash: 51b4f1d5a01740a3c7c50dedff674cdcb94a64f4
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660945"
---
# <a name="back-up-an-exchange-server-to-azure-backup-with-azure-backup-server"></a><span data-ttu-id="cd222-103">Back up an Exchange server to Azure Backup with Azure Backup Server</span><span class="sxs-lookup"><span data-stu-id="cd222-103">Back up an Exchange server to Azure Backup with Azure Backup Server</span></span>
<span data-ttu-id="cd222-104">This article describes how to configure Microsoft Azure Backup Server (MABS) to back up a Microsoft Exchange server to Azure.</span><span class="sxs-lookup"><span data-stu-id="cd222-104">This article describes how to configure Microsoft Azure Backup Server (MABS) to back up a Microsoft Exchange server to Azure.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="cd222-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="cd222-105">Prerequisites</span></span>
<span data-ttu-id="cd222-106">Before you continue, make sure that Azure Backup Server is [installed and prepared](backup-azure-microsoft-azure-backup.md).</span><span class="sxs-lookup"><span data-stu-id="cd222-106">Before you continue, make sure that Azure Backup Server is [installed and prepared](backup-azure-microsoft-azure-backup.md).</span></span>

## <a name="mabs-protection-agent"></a><span data-ttu-id="cd222-107">MABS protection agent</span><span class="sxs-lookup"><span data-stu-id="cd222-107">MABS protection agent</span></span>
<span data-ttu-id="cd222-108">To install the MABS protection agent on the Exchange server, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="cd222-108">To install the MABS protection agent on the Exchange server, follow these steps:</span></span>

1. <span data-ttu-id="cd222-109">Make sure that the firewalls are correctly configured.</span><span class="sxs-lookup"><span data-stu-id="cd222-109">Make sure that the firewalls are correctly configured.</span></span> <span data-ttu-id="cd222-110">See [Configure firewall exceptions for the agent](https://technet.microsoft.com/library/Hh758204.aspx).</span><span class="sxs-lookup"><span data-stu-id="cd222-110">See [Configure firewall exceptions for the agent](https://technet.microsoft.com/library/Hh758204.aspx).</span></span>
2. <span data-ttu-id="cd222-111">Install the agent on the Exchange server by clicking **Management > Agents > Install** in MABS Administrator Console.</span><span class="sxs-lookup"><span data-stu-id="cd222-111">Install the agent on the Exchange server by clicking **Management > Agents > Install** in MABS Administrator Console.</span></span> <span data-ttu-id="cd222-112">See [Install the MABS protection agent](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396) for detailed steps.</span><span class="sxs-lookup"><span data-stu-id="cd222-112">See [Install the MABS protection agent](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396) for detailed steps.</span></span>

## <a name="create-a-protection-group-for-the-exchange-server"></a><span data-ttu-id="cd222-113">Create a protection group for the Exchange server</span><span class="sxs-lookup"><span data-stu-id="cd222-113">Create a protection group for the Exchange server</span></span>
1. <span data-ttu-id="cd222-114">In the MABS Administrator Console, click **Protection**, and then click **New** on the tool ribbon to open the **Create New Protection Group** wizard.</span><span class="sxs-lookup"><span data-stu-id="cd222-114">In the MABS Administrator Console, click **Protection**, and then click **New** on the tool ribbon to open the **Create New Protection Group** wizard.</span></span>
2. <span data-ttu-id="cd222-115">On the **Welcome** screen of the wizard click **Next**.</span><span class="sxs-lookup"><span data-stu-id="cd222-115">On the **Welcome** screen of the wizard click **Next**.</span></span>
3. <span data-ttu-id="cd222-116">On the **Select protection group type** screen, select **Servers** and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="cd222-116">On the **Select protection group type** screen, select **Servers** and click **Next**.</span></span>
4. <span data-ttu-id="cd222-117">Select the Exchange server database that you want to protect and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="cd222-117">Select the Exchange server database that you want to protect and click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="cd222-118">If you are protecting Exchange 2013, check the [Exchange 2013 prerequisites](https://technet.microsoft.com/library/dn751029.aspx).</span><span class="sxs-lookup"><span data-stu-id="cd222-118">If you are protecting Exchange 2013, check the [Exchange 2013 prerequisites](https://technet.microsoft.com/library/dn751029.aspx).</span></span>
   >
   >

    <span data-ttu-id="cd222-119">In the following example, the Exchange 2010 database is selected.</span><span class="sxs-lookup"><span data-stu-id="cd222-119">In the following example, the Exchange 2010 database is selected.</span></span>

    ![Select group members](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-exchange-server/select-group-members.png)
5. <span data-ttu-id="cd222-121">Select the data protection method.</span><span class="sxs-lookup"><span data-stu-id="cd222-121">Select the data protection method.</span></span>

    <span data-ttu-id="cd222-122">Name the protection group, and then select both of the following options:</span><span class="sxs-lookup"><span data-stu-id="cd222-122">Name the protection group, and then select both of the following options:</span></span>

   * <span data-ttu-id="cd222-123">I want short-term protection using Disk.</span><span class="sxs-lookup"><span data-stu-id="cd222-123">I want short-term protection using Disk.</span></span>
   * <span data-ttu-id="cd222-124">I want online protection.</span><span class="sxs-lookup"><span data-stu-id="cd222-124">I want online protection.</span></span>
6. <span data-ttu-id="cd222-125">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="cd222-125">Click **Next**.</span></span>
7. <span data-ttu-id="cd222-126">Select the **Run Eseutil to check data integrity** option if you want to check the integrity of the Exchange Server databases.</span><span class="sxs-lookup"><span data-stu-id="cd222-126">Select the **Run Eseutil to check data integrity** option if you want to check the integrity of the Exchange Server databases.</span></span>

    <span data-ttu-id="cd222-127">After you select this option, backup consistency checking will be run on MABS to avoid the I/O traffic that’s generated by running the **eseutil** command on the Exchange server.</span><span class="sxs-lookup"><span data-stu-id="cd222-127">After you select this option, backup consistency checking will be run on MABS to avoid the I/O traffic that’s generated by running the **eseutil** command on the Exchange server.</span></span>

   > [!NOTE]
   > <span data-ttu-id="cd222-128">To use this option, you must copy the Ese.dll and Eseutil.exe files to the C:\Program Files\Microsoft Azure Backup\DPM\DPM\bin directory on the MAB server.</span><span class="sxs-lookup"><span data-stu-id="cd222-128">To use this option, you must copy the Ese.dll and Eseutil.exe files to the C:\Program Files\Microsoft Azure Backup\DPM\DPM\bin directory on the MAB server.</span></span> <span data-ttu-id="cd222-129">Otherwise, the following error is triggered:</span><span class="sxs-lookup"><span data-stu-id="cd222-129">Otherwise, the following error is triggered:</span></span>  
   > <span data-ttu-id="cd222-130">![eseutil error](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-exchange-server/eseutil-error.png)</span><span class="sxs-lookup"><span data-stu-id="cd222-130">![eseutil error](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-exchange-server/eseutil-error.png)</span></span>
   >
   >
8. <span data-ttu-id="cd222-131">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="cd222-131">Click **Next**.</span></span>
9. <span data-ttu-id="cd222-132">Select the database for **Copy Backup**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="cd222-132">Select the database for **Copy Backup**, and then click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="cd222-133">If you do not select “Full backup” for at least one DAG copy of a database, logs will not be truncated.</span><span class="sxs-lookup"><span data-stu-id="cd222-133">If you do not select “Full backup” for at least one DAG copy of a database, logs will not be truncated.</span></span>
   >
   >
10. <span data-ttu-id="cd222-134">Configure the goals for **Short-Term backup**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="cd222-134">Configure the goals for **Short-Term backup**, and then click **Next**.</span></span>
11. <span data-ttu-id="cd222-135">Review the available disk space, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="cd222-135">Review the available disk space, and then click **Next**.</span></span>
12. <span data-ttu-id="cd222-136">Select the time at which the MAB Server will create the initial replication, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="cd222-136">Select the time at which the MAB Server will create the initial replication, and then click **Next**.</span></span>
13. <span data-ttu-id="cd222-137">Select the consistency check options, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="cd222-137">Select the consistency check options, and then click **Next**.</span></span>
14. <span data-ttu-id="cd222-138">Choose the database that you want to back up to Azure, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="cd222-138">Choose the database that you want to back up to Azure, and then click **Next**.</span></span> <span data-ttu-id="cd222-139">For example:</span><span class="sxs-lookup"><span data-stu-id="cd222-139">For example:</span></span>

    ![Specify online protection data](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-exchange-server/specify-online-protection-data.png)
15. <span data-ttu-id="cd222-141">Define the schedule for **Azure Backup**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="cd222-141">Define the schedule for **Azure Backup**, and then click **Next**.</span></span> <span data-ttu-id="cd222-142">For example:</span><span class="sxs-lookup"><span data-stu-id="cd222-142">For example:</span></span>

    ![Specify online backup schedule](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-exchange-server/specify-online-backup-schedule.png)

    > [!NOTE]
    > <span data-ttu-id="cd222-144">Note Online recovery points are based on express full recovery points.</span><span class="sxs-lookup"><span data-stu-id="cd222-144">Note Online recovery points are based on express full recovery points.</span></span> <span data-ttu-id="cd222-145">Therefore, you must schedule the online recovery point after the time that’s specified for the express full recovery point.</span><span class="sxs-lookup"><span data-stu-id="cd222-145">Therefore, you must schedule the online recovery point after the time that’s specified for the express full recovery point.</span></span>
    >
    >
16. <span data-ttu-id="cd222-146">Configure the retention policy for **Azure Backup**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="cd222-146">Configure the retention policy for **Azure Backup**, and then click **Next**.</span></span>
17. <span data-ttu-id="cd222-147">Choose an online replication option and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="cd222-147">Choose an online replication option and click **Next**.</span></span>

    <span data-ttu-id="cd222-148">If you have a large database, it could take a long time for the initial backup to be created over the network.</span><span class="sxs-lookup"><span data-stu-id="cd222-148">If you have a large database, it could take a long time for the initial backup to be created over the network.</span></span> <span data-ttu-id="cd222-149">To avoid this issue, you can create an offline backup.</span><span class="sxs-lookup"><span data-stu-id="cd222-149">To avoid this issue, you can create an offline backup.</span></span>  

    ![Specify online retention policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-exchange-server/specify-online-retention-policy.png)
18. <span data-ttu-id="cd222-151">Confirm the settings, and then click **Create Group**.</span><span class="sxs-lookup"><span data-stu-id="cd222-151">Confirm the settings, and then click **Create Group**.</span></span>
19. <span data-ttu-id="cd222-152">Click **Close**.</span><span class="sxs-lookup"><span data-stu-id="cd222-152">Click **Close**.</span></span>

## <a name="recover-the-exchange-database"></a><span data-ttu-id="cd222-153">Recover the Exchange database</span><span class="sxs-lookup"><span data-stu-id="cd222-153">Recover the Exchange database</span></span>
1. <span data-ttu-id="cd222-154">To recover an Exchange database, click **Recovery** in the MABS Administrator Console.</span><span class="sxs-lookup"><span data-stu-id="cd222-154">To recover an Exchange database, click **Recovery** in the MABS Administrator Console.</span></span>
2. <span data-ttu-id="cd222-155">Locate the Exchange database that you want to recover.</span><span class="sxs-lookup"><span data-stu-id="cd222-155">Locate the Exchange database that you want to recover.</span></span>
3. <span data-ttu-id="cd222-156">Select an online recovery point from the *recovery time* drop-down list.</span><span class="sxs-lookup"><span data-stu-id="cd222-156">Select an online recovery point from the *recovery time* drop-down list.</span></span>
4. <span data-ttu-id="cd222-157">Click **Recover** to start the **Recovery Wizard**.</span><span class="sxs-lookup"><span data-stu-id="cd222-157">Click **Recover** to start the **Recovery Wizard**.</span></span>

<span data-ttu-id="cd222-158">For online recovery points, there are five recovery types:</span><span class="sxs-lookup"><span data-stu-id="cd222-158">For online recovery points, there are five recovery types:</span></span>

* <span data-ttu-id="cd222-159">**Recover to original Exchange Server location:** The data will be recovered to the original Exchange server.</span><span class="sxs-lookup"><span data-stu-id="cd222-159">**Recover to original Exchange Server location:** The data will be recovered to the original Exchange server.</span></span>
* <span data-ttu-id="cd222-160">**Recover to another database on an Exchange Server:** The data will be recovered to another database on another Exchange server.</span><span class="sxs-lookup"><span data-stu-id="cd222-160">**Recover to another database on an Exchange Server:** The data will be recovered to another database on another Exchange server.</span></span>
* <span data-ttu-id="cd222-161">**Recover to a Recovery Database:** The data will be recovered to an Exchange Recovery Database (RDB).</span><span class="sxs-lookup"><span data-stu-id="cd222-161">**Recover to a Recovery Database:** The data will be recovered to an Exchange Recovery Database (RDB).</span></span>
* <span data-ttu-id="cd222-162">**Copy to a network folder:** The data will be recovered to a network folder.</span><span class="sxs-lookup"><span data-stu-id="cd222-162">**Copy to a network folder:** The data will be recovered to a network folder.</span></span>
* <span data-ttu-id="cd222-163">**Copy to tape:** If you have a tape library or a stand-alone tape drive attached and configured on MABS, the recovery point will be copied to a free tape.</span><span class="sxs-lookup"><span data-stu-id="cd222-163">**Copy to tape:** If you have a tape library or a stand-alone tape drive attached and configured on MABS, the recovery point will be copied to a free tape.</span></span>

    ![Choose online replication](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-exchange-server/choose-online-replication.png)

## <a name="next-steps"></a><span data-ttu-id="cd222-165">Next steps</span><span class="sxs-lookup"><span data-stu-id="cd222-165">Next steps</span></span>
* [<span data-ttu-id="cd222-166">Azure Backup FAQ</span><span class="sxs-lookup"><span data-stu-id="cd222-166">Azure Backup FAQ</span></span>](backup-azure-backup-faq.md)






