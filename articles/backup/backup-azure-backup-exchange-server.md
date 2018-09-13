---
title: Back up an Exchange server to Azure Backup with System Center 2012 R2 DPM | Microsoft Docs
description: Learn how to back up an Exchange server to Azure Backup using System Center 2012 R2 DPM
services: backup
documentationcenter: ''
author: MaanasSaran
manager: NKolli1
editor: ''
ms.assetid: 13f32256-888e-416e-a78b-40c2a26a5939
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: masaran;jimpark;delhan;trinadhk;markgal
ms.openlocfilehash: 7f72ab001a6aff3047ad80678f0023b026365665
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662462"
---
# <a name="back-up-an-exchange-server-to-azure-backup-with-system-center-2012-r2-dpm"></a><span data-ttu-id="d3241-103">Back up an Exchange server to Azure Backup with System Center 2012 R2 DPM</span><span class="sxs-lookup"><span data-stu-id="d3241-103">Back up an Exchange server to Azure Backup with System Center 2012 R2 DPM</span></span>
<span data-ttu-id="d3241-104">This article describes how to configure a System Center 2012 R2 Data Protection Manager (DPM) server to back up a Microsoft Exchange server to  Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="d3241-104">This article describes how to configure a System Center 2012 R2 Data Protection Manager (DPM) server to back up a Microsoft Exchange server to  Azure Backup.</span></span>  

## <a name="updates"></a><span data-ttu-id="d3241-105">Updates</span><span class="sxs-lookup"><span data-stu-id="d3241-105">Updates</span></span>
<span data-ttu-id="d3241-106">To successfully register the DPM server with Azure Backup, you must install the latest update rollup for System Center 2012 R2 DPM and the latest version of the Azure Backup Agent.</span><span class="sxs-lookup"><span data-stu-id="d3241-106">To successfully register the DPM server with Azure Backup, you must install the latest update rollup for System Center 2012 R2 DPM and the latest version of the Azure Backup Agent.</span></span> <span data-ttu-id="d3241-107">Get the latest update rollup from the [Microsoft Catalog](http://catalog.update.microsoft.com/v7/site/Search.aspx?q=System%20Center%202012%20R2%20Data%20protection%20manager).</span><span class="sxs-lookup"><span data-stu-id="d3241-107">Get the latest update rollup from the [Microsoft Catalog](http://catalog.update.microsoft.com/v7/site/Search.aspx?q=System%20Center%202012%20R2%20Data%20protection%20manager).</span></span>

> [!NOTE]
> <span data-ttu-id="d3241-108">For the examples in this article, version 2.0.8719.0 of the Azure Backup Agent is installed, and Update Rollup 6 is installed on System Center 2012 R2 DPM.</span><span class="sxs-lookup"><span data-stu-id="d3241-108">For the examples in this article, version 2.0.8719.0 of the Azure Backup Agent is installed, and Update Rollup 6 is installed on System Center 2012 R2 DPM.</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="d3241-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d3241-109">Prerequisites</span></span>
<span data-ttu-id="d3241-110">Before you continue, make sure that all the [prerequisites](backup-azure-dpm-introduction.md#prerequisites) for using Microsoft Azure Backup to protect workloads have been met.</span><span class="sxs-lookup"><span data-stu-id="d3241-110">Before you continue, make sure that all the [prerequisites](backup-azure-dpm-introduction.md#prerequisites) for using Microsoft Azure Backup to protect workloads have been met.</span></span> <span data-ttu-id="d3241-111">These prerequisites include the following:</span><span class="sxs-lookup"><span data-stu-id="d3241-111">These prerequisites include the following:</span></span>

* <span data-ttu-id="d3241-112">A backup vault on the Azure site has been created.</span><span class="sxs-lookup"><span data-stu-id="d3241-112">A backup vault on the Azure site has been created.</span></span>
* <span data-ttu-id="d3241-113">Agent and vault credentials have been downloaded to the DPM server.</span><span class="sxs-lookup"><span data-stu-id="d3241-113">Agent and vault credentials have been downloaded to the DPM server.</span></span>
* <span data-ttu-id="d3241-114">The agent is installed on the DPM server.</span><span class="sxs-lookup"><span data-stu-id="d3241-114">The agent is installed on the DPM server.</span></span>
* <span data-ttu-id="d3241-115">The vault credentials were used to register the DPM server.</span><span class="sxs-lookup"><span data-stu-id="d3241-115">The vault credentials were used to register the DPM server.</span></span>
* <span data-ttu-id="d3241-116">If you are protecting Exchange 2016, please upgrade to DPM 2012 R2 UR9 or later</span><span class="sxs-lookup"><span data-stu-id="d3241-116">If you are protecting Exchange 2016, please upgrade to DPM 2012 R2 UR9 or later</span></span>

## <a name="dpm-protection-agent"></a><span data-ttu-id="d3241-117">DPM protection agent</span><span class="sxs-lookup"><span data-stu-id="d3241-117">DPM protection agent</span></span>
<span data-ttu-id="d3241-118">To install the DPM protection agent on the Exchange server, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="d3241-118">To install the DPM protection agent on the Exchange server, follow these steps:</span></span>

1. <span data-ttu-id="d3241-119">Make sure that the firewalls are correctly configured.</span><span class="sxs-lookup"><span data-stu-id="d3241-119">Make sure that the firewalls are correctly configured.</span></span> <span data-ttu-id="d3241-120">See [Configure firewall exceptions for the agent](https://technet.microsoft.com/library/Hh758204.aspx).</span><span class="sxs-lookup"><span data-stu-id="d3241-120">See [Configure firewall exceptions for the agent](https://technet.microsoft.com/library/Hh758204.aspx).</span></span>
2. <span data-ttu-id="d3241-121">Install the agent on the Exchange server by clicking **Management > Agents > Install** in DPM Administrator Console.</span><span class="sxs-lookup"><span data-stu-id="d3241-121">Install the agent on the Exchange server by clicking **Management > Agents > Install** in DPM Administrator Console.</span></span> <span data-ttu-id="d3241-122">See [Install the DPM protection agent](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396) for detailed steps.</span><span class="sxs-lookup"><span data-stu-id="d3241-122">See [Install the DPM protection agent](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396) for detailed steps.</span></span>

## <a name="create-a-protection-group-for-the-exchange-server"></a><span data-ttu-id="d3241-123">Create a protection group for the Exchange server</span><span class="sxs-lookup"><span data-stu-id="d3241-123">Create a protection group for the Exchange server</span></span>
1. <span data-ttu-id="d3241-124">In the DPM Administrator Console, click **Protection**, and then click **New** on the tool ribbon to open the **Create New Protection Group** wizard.</span><span class="sxs-lookup"><span data-stu-id="d3241-124">In the DPM Administrator Console, click **Protection**, and then click **New** on the tool ribbon to open the **Create New Protection Group** wizard.</span></span>
2. <span data-ttu-id="d3241-125">On the **Welcome** screen of the wizard click **Next**.</span><span class="sxs-lookup"><span data-stu-id="d3241-125">On the **Welcome** screen of the wizard click **Next**.</span></span>
3. <span data-ttu-id="d3241-126">On the **Select protection group type** screen, select **Servers** and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="d3241-126">On the **Select protection group type** screen, select **Servers** and click **Next**.</span></span>
4. <span data-ttu-id="d3241-127">Select the Exchange server database that you want to protect and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="d3241-127">Select the Exchange server database that you want to protect and click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="d3241-128">If you are protecting Exchange 2013, check the [Exchange 2013 prerequisites](https://technet.microsoft.com/library/dn751029.aspx).</span><span class="sxs-lookup"><span data-stu-id="d3241-128">If you are protecting Exchange 2013, check the [Exchange 2013 prerequisites](https://technet.microsoft.com/library/dn751029.aspx).</span></span>
   >
   >

    <span data-ttu-id="d3241-129">In the following example, the Exchange 2010 database is selected.</span><span class="sxs-lookup"><span data-stu-id="d3241-129">In the following example, the Exchange 2010 database is selected.</span></span>

    ![Select group members](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-exchange-server/select-group-members.png)
5. <span data-ttu-id="d3241-131">Select the data protection method.</span><span class="sxs-lookup"><span data-stu-id="d3241-131">Select the data protection method.</span></span>

    <span data-ttu-id="d3241-132">Name the protection group, and then select both of the following options:</span><span class="sxs-lookup"><span data-stu-id="d3241-132">Name the protection group, and then select both of the following options:</span></span>

   * <span data-ttu-id="d3241-133">I want short-term protection using Disk.</span><span class="sxs-lookup"><span data-stu-id="d3241-133">I want short-term protection using Disk.</span></span>
   * <span data-ttu-id="d3241-134">I want online protection.</span><span class="sxs-lookup"><span data-stu-id="d3241-134">I want online protection.</span></span>
6. <span data-ttu-id="d3241-135">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="d3241-135">Click **Next**.</span></span>
7. <span data-ttu-id="d3241-136">Select the **Run Eseutil to check data integrity** option if you want to check the integrity of the Exchange Server databases.</span><span class="sxs-lookup"><span data-stu-id="d3241-136">Select the **Run Eseutil to check data integrity** option if you want to check the integrity of the Exchange Server databases.</span></span>

    <span data-ttu-id="d3241-137">After you select this option, backup consistency checking will be run on the DPM server to avoid the I/O traffic that’s generated by running the **eseutil** command on the Exchange server.</span><span class="sxs-lookup"><span data-stu-id="d3241-137">After you select this option, backup consistency checking will be run on the DPM server to avoid the I/O traffic that’s generated by running the **eseutil** command on the Exchange server.</span></span>

   > [!NOTE]
   > <span data-ttu-id="d3241-138">To use this option, you must copy the Ese.dll and Eseutil.exe files to the C:\Program Files\Microsoft System Center 2012 R2\DPM\DPM\bin directory on the DPM server.</span><span class="sxs-lookup"><span data-stu-id="d3241-138">To use this option, you must copy the Ese.dll and Eseutil.exe files to the C:\Program Files\Microsoft System Center 2012 R2\DPM\DPM\bin directory on the DPM server.</span></span> <span data-ttu-id="d3241-139">Otherwise, the following error is triggered:</span><span class="sxs-lookup"><span data-stu-id="d3241-139">Otherwise, the following error is triggered:</span></span>  
   > <span data-ttu-id="d3241-140">![eseutil error](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-exchange-server/eseutil-error.png)</span><span class="sxs-lookup"><span data-stu-id="d3241-140">![eseutil error](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-exchange-server/eseutil-error.png)</span></span>
   >
   >
8. <span data-ttu-id="d3241-141">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="d3241-141">Click **Next**.</span></span>
9. <span data-ttu-id="d3241-142">Select the database for **Copy Backup**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="d3241-142">Select the database for **Copy Backup**, and then click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="d3241-143">If you do not select “Full backup” for at least one DAG copy of a database, logs will not be truncated.</span><span class="sxs-lookup"><span data-stu-id="d3241-143">If you do not select “Full backup” for at least one DAG copy of a database, logs will not be truncated.</span></span>
   >
   >
10. <span data-ttu-id="d3241-144">Configure the goals for **Short-Term backup**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="d3241-144">Configure the goals for **Short-Term backup**, and then click **Next**.</span></span>
11. <span data-ttu-id="d3241-145">Review the available disk space, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="d3241-145">Review the available disk space, and then click **Next**.</span></span>
12. <span data-ttu-id="d3241-146">Select the time at which the DPM server will create the initial replication, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="d3241-146">Select the time at which the DPM server will create the initial replication, and then click **Next**.</span></span>
13. <span data-ttu-id="d3241-147">Select the consistency check options, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="d3241-147">Select the consistency check options, and then click **Next**.</span></span>
14. <span data-ttu-id="d3241-148">Choose the database that you want to back up to Azure, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="d3241-148">Choose the database that you want to back up to Azure, and then click **Next**.</span></span> <span data-ttu-id="d3241-149">For example:</span><span class="sxs-lookup"><span data-stu-id="d3241-149">For example:</span></span>

    ![Specify online protection data](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-exchange-server/specify-online-protection-data.png)
15. <span data-ttu-id="d3241-151">Define the schedule for **Azure Backup**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="d3241-151">Define the schedule for **Azure Backup**, and then click **Next**.</span></span> <span data-ttu-id="d3241-152">For example:</span><span class="sxs-lookup"><span data-stu-id="d3241-152">For example:</span></span>

    ![Specify online backup schedule](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-exchange-server/specify-online-backup-schedule.png)

    > [!NOTE]
    > <span data-ttu-id="d3241-154">Note Online recovery points are based on express full recovery points.</span><span class="sxs-lookup"><span data-stu-id="d3241-154">Note Online recovery points are based on express full recovery points.</span></span> <span data-ttu-id="d3241-155">Therefore, you must schedule the online recovery point after the time that’s specified for the express full recovery point.</span><span class="sxs-lookup"><span data-stu-id="d3241-155">Therefore, you must schedule the online recovery point after the time that’s specified for the express full recovery point.</span></span>
    >
    >
16. <span data-ttu-id="d3241-156">Configure the retention policy for **Azure Backup**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="d3241-156">Configure the retention policy for **Azure Backup**, and then click **Next**.</span></span>
17. <span data-ttu-id="d3241-157">Choose an online replication option and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="d3241-157">Choose an online replication option and click **Next**.</span></span>

    <span data-ttu-id="d3241-158">If you have a large database, it could take a long time for the initial backup to be created over the network.</span><span class="sxs-lookup"><span data-stu-id="d3241-158">If you have a large database, it could take a long time for the initial backup to be created over the network.</span></span> <span data-ttu-id="d3241-159">To avoid this issue, you can create an offline backup.</span><span class="sxs-lookup"><span data-stu-id="d3241-159">To avoid this issue, you can create an offline backup.</span></span>  

    ![Specify online retention policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-exchange-server/specify-online-retention-policy.png)
18. <span data-ttu-id="d3241-161">Confirm the settings, and then click **Create Group**.</span><span class="sxs-lookup"><span data-stu-id="d3241-161">Confirm the settings, and then click **Create Group**.</span></span>
19. <span data-ttu-id="d3241-162">Click **Close**.</span><span class="sxs-lookup"><span data-stu-id="d3241-162">Click **Close**.</span></span>

## <a name="recover-the-exchange-database"></a><span data-ttu-id="d3241-163">Recover the Exchange database</span><span class="sxs-lookup"><span data-stu-id="d3241-163">Recover the Exchange database</span></span>
1. <span data-ttu-id="d3241-164">To recover an Exchange database, click **Recovery** in the DPM Administrator Console.</span><span class="sxs-lookup"><span data-stu-id="d3241-164">To recover an Exchange database, click **Recovery** in the DPM Administrator Console.</span></span>
2. <span data-ttu-id="d3241-165">Locate the Exchange database that you want to recover.</span><span class="sxs-lookup"><span data-stu-id="d3241-165">Locate the Exchange database that you want to recover.</span></span>
3. <span data-ttu-id="d3241-166">Select an online recovery point from the *recovery time* drop-down list.</span><span class="sxs-lookup"><span data-stu-id="d3241-166">Select an online recovery point from the *recovery time* drop-down list.</span></span>
4. <span data-ttu-id="d3241-167">Click **Recover** to start the **Recovery Wizard**.</span><span class="sxs-lookup"><span data-stu-id="d3241-167">Click **Recover** to start the **Recovery Wizard**.</span></span>

<span data-ttu-id="d3241-168">For online recovery points, there are five recovery types:</span><span class="sxs-lookup"><span data-stu-id="d3241-168">For online recovery points, there are five recovery types:</span></span>

* <span data-ttu-id="d3241-169">**Recover to original Exchange Server location:** The data will be recovered to the original Exchange server.</span><span class="sxs-lookup"><span data-stu-id="d3241-169">**Recover to original Exchange Server location:** The data will be recovered to the original Exchange server.</span></span>
* <span data-ttu-id="d3241-170">**Recover to another database on an Exchange Server:** The data will be recovered to another database on another Exchange server.</span><span class="sxs-lookup"><span data-stu-id="d3241-170">**Recover to another database on an Exchange Server:** The data will be recovered to another database on another Exchange server.</span></span>
* <span data-ttu-id="d3241-171">**Recover to a Recovery Database:** The data will be recovered to an Exchange Recovery Database (RDB).</span><span class="sxs-lookup"><span data-stu-id="d3241-171">**Recover to a Recovery Database:** The data will be recovered to an Exchange Recovery Database (RDB).</span></span>
* <span data-ttu-id="d3241-172">**Copy to a network folder:** The data will be recovered to a network folder.</span><span class="sxs-lookup"><span data-stu-id="d3241-172">**Copy to a network folder:** The data will be recovered to a network folder.</span></span>
* <span data-ttu-id="d3241-173">**Copy to tape:** If you have a tape library or a stand-alone tape drive attached and configured on the DPM server, the recovery point will be copied to a free tape.</span><span class="sxs-lookup"><span data-stu-id="d3241-173">**Copy to tape:** If you have a tape library or a stand-alone tape drive attached and configured on the DPM server, the recovery point will be copied to a free tape.</span></span>

    ![Choose online replication](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-exchange-server/choose-online-replication.png)

## <a name="next-steps"></a><span data-ttu-id="d3241-175">Next steps</span><span class="sxs-lookup"><span data-stu-id="d3241-175">Next steps</span></span>
* [<span data-ttu-id="d3241-176">Azure Backup FAQ</span><span class="sxs-lookup"><span data-stu-id="d3241-176">Azure Backup FAQ</span></span>](backup-azure-backup-faq.md)






