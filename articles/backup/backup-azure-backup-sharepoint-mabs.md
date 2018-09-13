---
title: Use Azure Backup server to back up a SharePoint farm to Azure | Microsoft Docs
description: Use Azure Backup Server to back up and restore your SharePoint data. This article provides the information to configure your SharePoint farm so that desired data can be stored in Azure. You can restore protected SharePoint data from disk or from Azure.
services: backup
documentationcenter: ''
author: pvrk
manager: shivamg
editor: ''
ms.assetid: 34ba87a4-91f1-4054-a4a1-272af1e15496
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: pullabhk
ms.openlocfilehash: 7e21b2939c71b4b41999cc1eb3110048985e0de5
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660934"
---
# <a name="back-up-a-sharepoint-farm-to-azure"></a><span data-ttu-id="43e38-105">Back up a SharePoint farm to Azure</span><span class="sxs-lookup"><span data-stu-id="43e38-105">Back up a SharePoint farm to Azure</span></span>
<span data-ttu-id="43e38-106">You back up a SharePoint farm to Microsoft Azure by using Microsoft Azure Backup Server (MABS) in much the same way that you back up other data sources.</span><span class="sxs-lookup"><span data-stu-id="43e38-106">You back up a SharePoint farm to Microsoft Azure by using Microsoft Azure Backup Server (MABS) in much the same way that you back up other data sources.</span></span> <span data-ttu-id="43e38-107">Azure Backup provides flexibility in the backup schedule to create daily, weekly, monthly, or yearly backup points and gives you retention policy options for various backup points.</span><span class="sxs-lookup"><span data-stu-id="43e38-107">Azure Backup provides flexibility in the backup schedule to create daily, weekly, monthly, or yearly backup points and gives you retention policy options for various backup points.</span></span> <span data-ttu-id="43e38-108">It also provides the capability to store local disk copies for quick recovery-time objectives (RTO) and to store copies to Azure for economical, long-term retention.</span><span class="sxs-lookup"><span data-stu-id="43e38-108">It also provides the capability to store local disk copies for quick recovery-time objectives (RTO) and to store copies to Azure for economical, long-term retention.</span></span>

## <a name="sharepoint-supported-versions-and-related-protection-scenarios"></a><span data-ttu-id="43e38-109">SharePoint supported versions and related protection scenarios</span><span class="sxs-lookup"><span data-stu-id="43e38-109">SharePoint supported versions and related protection scenarios</span></span>
<span data-ttu-id="43e38-110">Azure Backup for DPM supports the following scenarios:</span><span class="sxs-lookup"><span data-stu-id="43e38-110">Azure Backup for DPM supports the following scenarios:</span></span>

| <span data-ttu-id="43e38-111">Workload</span><span class="sxs-lookup"><span data-stu-id="43e38-111">Workload</span></span> | <span data-ttu-id="43e38-112">Version</span><span class="sxs-lookup"><span data-stu-id="43e38-112">Version</span></span> | <span data-ttu-id="43e38-113">SharePoint deployment</span><span class="sxs-lookup"><span data-stu-id="43e38-113">SharePoint deployment</span></span> | <span data-ttu-id="43e38-114">Protection and recovery</span><span class="sxs-lookup"><span data-stu-id="43e38-114">Protection and recovery</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="43e38-115">SharePoint</span><span class="sxs-lookup"><span data-stu-id="43e38-115">SharePoint</span></span> |<span data-ttu-id="43e38-116">SharePoint 2013, SharePoint 2010, SharePoint 2007, SharePoint 3.0</span><span class="sxs-lookup"><span data-stu-id="43e38-116">SharePoint 2013, SharePoint 2010, SharePoint 2007, SharePoint 3.0</span></span> |<span data-ttu-id="43e38-117">SharePoint deployed as a physical server or Hyper-V/VMware virtual machine</span><span class="sxs-lookup"><span data-stu-id="43e38-117">SharePoint deployed as a physical server or Hyper-V/VMware virtual machine</span></span> <br> -------------- <br> <span data-ttu-id="43e38-118">SQL AlwaysOn</span><span class="sxs-lookup"><span data-stu-id="43e38-118">SQL AlwaysOn</span></span> | <span data-ttu-id="43e38-119">Protect SharePoint Farm recovery options: Recovery farm, database, and file or list item from disk recovery points.</span><span class="sxs-lookup"><span data-stu-id="43e38-119">Protect SharePoint Farm recovery options: Recovery farm, database, and file or list item from disk recovery points.</span></span>  <span data-ttu-id="43e38-120">Farm and database recovery from Azure recovery points.</span><span class="sxs-lookup"><span data-stu-id="43e38-120">Farm and database recovery from Azure recovery points.</span></span> |

## <a name="before-you-start"></a><span data-ttu-id="43e38-121">Before you start</span><span class="sxs-lookup"><span data-stu-id="43e38-121">Before you start</span></span>
<span data-ttu-id="43e38-122">There are a few things you need to confirm before you back up a SharePoint farm to Azure.</span><span class="sxs-lookup"><span data-stu-id="43e38-122">There are a few things you need to confirm before you back up a SharePoint farm to Azure.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="43e38-123">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="43e38-123">Prerequisites</span></span>
<span data-ttu-id="43e38-124">Before you proceed, make sure that you have [installed and prepared the Azure Backup Server](backup-azure-microsoft-azure-backup.md) to protect workloads.</span><span class="sxs-lookup"><span data-stu-id="43e38-124">Before you proceed, make sure that you have [installed and prepared the Azure Backup Server](backup-azure-microsoft-azure-backup.md) to protect workloads.</span></span>

### <a name="protection-agent"></a><span data-ttu-id="43e38-125">Protection agent</span><span class="sxs-lookup"><span data-stu-id="43e38-125">Protection agent</span></span>
<span data-ttu-id="43e38-126">The Protection agent must be installed on the server that's running SharePoint, the servers that are running SQL Server, and all other servers that are part of the SharePoint farm.</span><span class="sxs-lookup"><span data-stu-id="43e38-126">The Protection agent must be installed on the server that's running SharePoint, the servers that are running SQL Server, and all other servers that are part of the SharePoint farm.</span></span> <span data-ttu-id="43e38-127">For more information about how to set up the protection agent, see [Setup Protection Agent](https://technet.microsoft.com/library/hh758034\(v=sc.12\).aspx).</span><span class="sxs-lookup"><span data-stu-id="43e38-127">For more information about how to set up the protection agent, see [Setup Protection Agent](https://technet.microsoft.com/library/hh758034\(v=sc.12\).aspx).</span></span>  <span data-ttu-id="43e38-128">The one exception is that you install the agent only on a single web front end (WFE) server.</span><span class="sxs-lookup"><span data-stu-id="43e38-128">The one exception is that you install the agent only on a single web front end (WFE) server.</span></span> <span data-ttu-id="43e38-129">DPM needs the agent on one WFE server only to serve as the entry point for protection.</span><span class="sxs-lookup"><span data-stu-id="43e38-129">DPM needs the agent on one WFE server only to serve as the entry point for protection.</span></span>

### <a name="sharepoint-farm"></a><span data-ttu-id="43e38-130">SharePoint farm</span><span class="sxs-lookup"><span data-stu-id="43e38-130">SharePoint farm</span></span>
<span data-ttu-id="43e38-131">For every 10 million items in the farm, there must be at least 2 GB of space on the volume where the MABS folder is located.</span><span class="sxs-lookup"><span data-stu-id="43e38-131">For every 10 million items in the farm, there must be at least 2 GB of space on the volume where the MABS folder is located.</span></span> <span data-ttu-id="43e38-132">This space is required for catalog generation.</span><span class="sxs-lookup"><span data-stu-id="43e38-132">This space is required for catalog generation.</span></span> <span data-ttu-id="43e38-133">For MABS to recover specific items (site collections, sites, lists, document libraries, folders, individual documents, and list items), catalog generation creates a list of the URLs that are contained within each content database.</span><span class="sxs-lookup"><span data-stu-id="43e38-133">For MABS to recover specific items (site collections, sites, lists, document libraries, folders, individual documents, and list items), catalog generation creates a list of the URLs that are contained within each content database.</span></span> <span data-ttu-id="43e38-134">You can view the list of URLs in the recoverable item pane in the **Recovery** task area of MABS Administrator Console.</span><span class="sxs-lookup"><span data-stu-id="43e38-134">You can view the list of URLs in the recoverable item pane in the **Recovery** task area of MABS Administrator Console.</span></span>

### <a name="sql-server"></a><span data-ttu-id="43e38-135">SQL Server</span><span class="sxs-lookup"><span data-stu-id="43e38-135">SQL Server</span></span>
<span data-ttu-id="43e38-136">MABS runs as a LocalSystem account.</span><span class="sxs-lookup"><span data-stu-id="43e38-136">MABS runs as a LocalSystem account.</span></span> <span data-ttu-id="43e38-137">To back up SQL Server databases, MABS needs sysadmin privileges on that account for the server that's running SQL Server.</span><span class="sxs-lookup"><span data-stu-id="43e38-137">To back up SQL Server databases, MABS needs sysadmin privileges on that account for the server that's running SQL Server.</span></span> <span data-ttu-id="43e38-138">Set NT AUTHORITY\SYSTEM to *sysadmin* on the server that's running SQL Server before you back it up.</span><span class="sxs-lookup"><span data-stu-id="43e38-138">Set NT AUTHORITY\SYSTEM to *sysadmin* on the server that's running SQL Server before you back it up.</span></span>

<span data-ttu-id="43e38-139">If the SharePoint farm has SQL Server databases that are configured with SQL Server aliases, install the SQL Server client components on the front-end Web server that MABS will protect.</span><span class="sxs-lookup"><span data-stu-id="43e38-139">If the SharePoint farm has SQL Server databases that are configured with SQL Server aliases, install the SQL Server client components on the front-end Web server that MABS will protect.</span></span>

### <a name="sharepoint-server"></a><span data-ttu-id="43e38-140">SharePoint Server</span><span class="sxs-lookup"><span data-stu-id="43e38-140">SharePoint Server</span></span>
<span data-ttu-id="43e38-141">While performance depends on many factors such as size of SharePoint farm, as general guidance one MABS can protect a 25 TB SharePoint farm.</span><span class="sxs-lookup"><span data-stu-id="43e38-141">While performance depends on many factors such as size of SharePoint farm, as general guidance one MABS can protect a 25 TB SharePoint farm.</span></span>

### <a name="whats-not-supported"></a><span data-ttu-id="43e38-142">What's not supported</span><span class="sxs-lookup"><span data-stu-id="43e38-142">What's not supported</span></span>
* <span data-ttu-id="43e38-143">MABS that protects a SharePoint farm does not protect search indexes or application service databases.</span><span class="sxs-lookup"><span data-stu-id="43e38-143">MABS that protects a SharePoint farm does not protect search indexes or application service databases.</span></span> <span data-ttu-id="43e38-144">You will need to configure the protection of these databases separately.</span><span class="sxs-lookup"><span data-stu-id="43e38-144">You will need to configure the protection of these databases separately.</span></span>
* <span data-ttu-id="43e38-145">MABS does not provide backup of SharePoint SQL Server databases that are hosted on scale-out file server (SOFS) shares.</span><span class="sxs-lookup"><span data-stu-id="43e38-145">MABS does not provide backup of SharePoint SQL Server databases that are hosted on scale-out file server (SOFS) shares.</span></span>

## <a name="configure-sharepoint-protection"></a><span data-ttu-id="43e38-146">Configure SharePoint protection</span><span class="sxs-lookup"><span data-stu-id="43e38-146">Configure SharePoint protection</span></span>
<span data-ttu-id="43e38-147">Before you can use MABS to protect SharePoint, you must configure the SharePoint VSS Writer service (WSS Writer service) by using **ConfigureSharePoint.exe**.</span><span class="sxs-lookup"><span data-stu-id="43e38-147">Before you can use MABS to protect SharePoint, you must configure the SharePoint VSS Writer service (WSS Writer service) by using **ConfigureSharePoint.exe**.</span></span>

<span data-ttu-id="43e38-148">You can find **ConfigureSharePoint.exe** in the [MABS Installation Path]\bin folder on the front-end web server.</span><span class="sxs-lookup"><span data-stu-id="43e38-148">You can find **ConfigureSharePoint.exe** in the [MABS Installation Path]\bin folder on the front-end web server.</span></span> <span data-ttu-id="43e38-149">This tool provides the protection agent with the credentials for the SharePoint farm.</span><span class="sxs-lookup"><span data-stu-id="43e38-149">This tool provides the protection agent with the credentials for the SharePoint farm.</span></span> <span data-ttu-id="43e38-150">You run it on a single WFE server.</span><span class="sxs-lookup"><span data-stu-id="43e38-150">You run it on a single WFE server.</span></span> <span data-ttu-id="43e38-151">If you have multiple WFE servers, select just one when you configure a protection group.</span><span class="sxs-lookup"><span data-stu-id="43e38-151">If you have multiple WFE servers, select just one when you configure a protection group.</span></span>

### <a name="to-configure-the-sharepoint-vss-writer-service"></a><span data-ttu-id="43e38-152">To configure the SharePoint VSS Writer service</span><span class="sxs-lookup"><span data-stu-id="43e38-152">To configure the SharePoint VSS Writer service</span></span>
1. <span data-ttu-id="43e38-153">On the WFE server, at a command prompt, go to [MABS installation location]\bin\\</span><span class="sxs-lookup"><span data-stu-id="43e38-153">On the WFE server, at a command prompt, go to [MABS installation location]\bin\\</span></span>
2. <span data-ttu-id="43e38-154">Enter ConfigureSharePoint -EnableSharePointProtection.</span><span class="sxs-lookup"><span data-stu-id="43e38-154">Enter ConfigureSharePoint -EnableSharePointProtection.</span></span>
3. <span data-ttu-id="43e38-155">Enter the farm administrator credentials.</span><span class="sxs-lookup"><span data-stu-id="43e38-155">Enter the farm administrator credentials.</span></span> <span data-ttu-id="43e38-156">This account should be a member of the local Administrator group on the WFE server.</span><span class="sxs-lookup"><span data-stu-id="43e38-156">This account should be a member of the local Administrator group on the WFE server.</span></span> <span data-ttu-id="43e38-157">If the farm administrator isn’t a local admin grant the following permissions on the WFE server:</span><span class="sxs-lookup"><span data-stu-id="43e38-157">If the farm administrator isn’t a local admin grant the following permissions on the WFE server:</span></span>
   * <span data-ttu-id="43e38-158">Grant the WSS_Admin_WPG group full control to the DPM folder (%Program Files%\Microsoft Azure Backup\DPM).</span><span class="sxs-lookup"><span data-stu-id="43e38-158">Grant the WSS_Admin_WPG group full control to the DPM folder (%Program Files%\Microsoft Azure Backup\DPM).</span></span>
   * <span data-ttu-id="43e38-159">Grant the WSS_Admin_WPG group read access to the DPM Registry key (HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager).</span><span class="sxs-lookup"><span data-stu-id="43e38-159">Grant the WSS_Admin_WPG group read access to the DPM Registry key (HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager).</span></span>

> [!NOTE]
> <span data-ttu-id="43e38-160">You’ll need to rerun ConfigureSharePoint.exe whenever there’s a change in the SharePoint farm administrator credentials.</span><span class="sxs-lookup"><span data-stu-id="43e38-160">You’ll need to rerun ConfigureSharePoint.exe whenever there’s a change in the SharePoint farm administrator credentials.</span></span>
>
>

## <a name="back-up-a-sharepoint-farm-by-using-mabs"></a><span data-ttu-id="43e38-161">Back up a SharePoint farm by using MABS</span><span class="sxs-lookup"><span data-stu-id="43e38-161">Back up a SharePoint farm by using MABS</span></span>
<span data-ttu-id="43e38-162">After you have configured MABS and the SharePoint farm as explained previously, SharePoint can be protected by MABS.</span><span class="sxs-lookup"><span data-stu-id="43e38-162">After you have configured MABS and the SharePoint farm as explained previously, SharePoint can be protected by MABS.</span></span>

### <a name="to-protect-a-sharepoint-farm"></a><span data-ttu-id="43e38-163">To protect a SharePoint farm</span><span class="sxs-lookup"><span data-stu-id="43e38-163">To protect a SharePoint farm</span></span>
1. <span data-ttu-id="43e38-164">From the **Protection** tab of the MABS Administrator Console, click **New**.</span><span class="sxs-lookup"><span data-stu-id="43e38-164">From the **Protection** tab of the MABS Administrator Console, click **New**.</span></span>
    <span data-ttu-id="43e38-165">![New Protection Tab](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sharepoint/dpm-new-protection-tab.png)</span><span class="sxs-lookup"><span data-stu-id="43e38-165">![New Protection Tab](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sharepoint/dpm-new-protection-tab.png)</span></span>
2. <span data-ttu-id="43e38-166">On the **Select Protection Group Type** page of the **Create New Protection Group** wizard, select **Servers**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="43e38-166">On the **Select Protection Group Type** page of the **Create New Protection Group** wizard, select **Servers**, and then click **Next**.</span></span>

    ![Select Protection Group type](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sharepoint/select-protection-group-type.png)
3. <span data-ttu-id="43e38-168">On the **Select Group Members** screen, select the check box for the SharePoint server you want to protect and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="43e38-168">On the **Select Group Members** screen, select the check box for the SharePoint server you want to protect and click **Next**.</span></span>

    ![Select group members](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sharepoint/select-group-members2.png)

   > [!NOTE]
   > <span data-ttu-id="43e38-170">With the protection agent installed, you can see the server in the wizard.</span><span class="sxs-lookup"><span data-stu-id="43e38-170">With the protection agent installed, you can see the server in the wizard.</span></span> <span data-ttu-id="43e38-171">MABS also shows its structure.</span><span class="sxs-lookup"><span data-stu-id="43e38-171">MABS also shows its structure.</span></span> <span data-ttu-id="43e38-172">Because you ran ConfigureSharePoint.exe, MABS communicates with the SharePoint VSS Writer service and its corresponding SQL Server databases and recognizes the SharePoint farm structure, the associated content databases, and any corresponding items.</span><span class="sxs-lookup"><span data-stu-id="43e38-172">Because you ran ConfigureSharePoint.exe, MABS communicates with the SharePoint VSS Writer service and its corresponding SQL Server databases and recognizes the SharePoint farm structure, the associated content databases, and any corresponding items.</span></span>
   >
   >
4. <span data-ttu-id="43e38-173">On the **Select Data Protection Method** page, enter the name of the **Protection Group**, and select your preferred *protection methods*.</span><span class="sxs-lookup"><span data-stu-id="43e38-173">On the **Select Data Protection Method** page, enter the name of the **Protection Group**, and select your preferred *protection methods*.</span></span> <span data-ttu-id="43e38-174">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="43e38-174">Click **Next**.</span></span>

    ![Select data protection method](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sharepoint/select-data-protection-method1.png)

   > [!NOTE]
   > <span data-ttu-id="43e38-176">The disk protection method helps to meet short recovery-time objectives.</span><span class="sxs-lookup"><span data-stu-id="43e38-176">The disk protection method helps to meet short recovery-time objectives.</span></span>
   >
   >
5. <span data-ttu-id="43e38-177">On the **Specify Short-Term Goals** page, select your preferred **Retention range** and identify when you want backups to occur.</span><span class="sxs-lookup"><span data-stu-id="43e38-177">On the **Specify Short-Term Goals** page, select your preferred **Retention range** and identify when you want backups to occur.</span></span>

    ![Specify short-term goals](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sharepoint/specify-short-term-goals2.png)

   > [!NOTE]
   > <span data-ttu-id="43e38-179">Because recovery is most often required for data that's less than five days old, we selected a retention range of five days on disk and ensured that the backup happens during non-production hours, for this example.</span><span class="sxs-lookup"><span data-stu-id="43e38-179">Because recovery is most often required for data that's less than five days old, we selected a retention range of five days on disk and ensured that the backup happens during non-production hours, for this example.</span></span>
   >
   >
6. <span data-ttu-id="43e38-180">Review the storage pool disk space allocated for the protection group, and click then **Next**.</span><span class="sxs-lookup"><span data-stu-id="43e38-180">Review the storage pool disk space allocated for the protection group, and click then **Next**.</span></span>
7. <span data-ttu-id="43e38-181">For every protection group, MABS allocates disk space to store and manage replicas.</span><span class="sxs-lookup"><span data-stu-id="43e38-181">For every protection group, MABS allocates disk space to store and manage replicas.</span></span> <span data-ttu-id="43e38-182">At this point, MABS must create a copy of the selected data.</span><span class="sxs-lookup"><span data-stu-id="43e38-182">At this point, MABS must create a copy of the selected data.</span></span> <span data-ttu-id="43e38-183">Select how and when you want the replica created, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="43e38-183">Select how and when you want the replica created, and then click **Next**.</span></span>

    ![Choose replica creation method](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sharepoint/choose-replica-creation-method.png)

   > [!NOTE]
   > <span data-ttu-id="43e38-185">To make sure that network traffic is not effected, select a time outside production hours.</span><span class="sxs-lookup"><span data-stu-id="43e38-185">To make sure that network traffic is not effected, select a time outside production hours.</span></span>
   >
   >
8. <span data-ttu-id="43e38-186">MABS ensures data integrity by performing consistency checks on the replica.</span><span class="sxs-lookup"><span data-stu-id="43e38-186">MABS ensures data integrity by performing consistency checks on the replica.</span></span> <span data-ttu-id="43e38-187">There are two available options.</span><span class="sxs-lookup"><span data-stu-id="43e38-187">There are two available options.</span></span> <span data-ttu-id="43e38-188">You can define a schedule to run consistency checks, or DPM can run consistency checks automatically on the replica whenever it becomes inconsistent.</span><span class="sxs-lookup"><span data-stu-id="43e38-188">You can define a schedule to run consistency checks, or DPM can run consistency checks automatically on the replica whenever it becomes inconsistent.</span></span> <span data-ttu-id="43e38-189">Select your preferred option, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="43e38-189">Select your preferred option, and then click **Next**.</span></span>

    ![Consistency Check](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sharepoint/consistency-check.png)
9. <span data-ttu-id="43e38-191">On the **Specify Online Protection Data** page, select the SharePoint farm that you want to protect, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="43e38-191">On the **Specify Online Protection Data** page, select the SharePoint farm that you want to protect, and then click **Next**.</span></span>

    ![DPM SharePoint Protection1](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sharepoint/select-online-protection1.png)
10. <span data-ttu-id="43e38-193">On the **Specify Online Backup Schedule** page, select your preferred schedule, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="43e38-193">On the **Specify Online Backup Schedule** page, select your preferred schedule, and then click **Next**.</span></span>

    ![Online_backup_schedule](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sharepoint/specify-online-backup-schedule.png)

    > [!NOTE]
    > <span data-ttu-id="43e38-195">MABS provides a maximum of two daily backups to Azure from the then available latest disk backup point.</span><span class="sxs-lookup"><span data-stu-id="43e38-195">MABS provides a maximum of two daily backups to Azure from the then available latest disk backup point.</span></span> <span data-ttu-id="43e38-196">Azure Backup can also control the amount of WAN bandwidth that can be used for backups in peak and off-peak hours by using [Azure Backup Network Throttling](https://azure.microsoft.com/documentation/articles/backup-configure-vault/#enable-network-throttling).</span><span class="sxs-lookup"><span data-stu-id="43e38-196">Azure Backup can also control the amount of WAN bandwidth that can be used for backups in peak and off-peak hours by using [Azure Backup Network Throttling](https://azure.microsoft.com/documentation/articles/backup-configure-vault/#enable-network-throttling).</span></span>
    >
    >
11. <span data-ttu-id="43e38-197">Depending on the backup schedule that you selected, on the **Specify Online Retention Policy** page, select the retention policy for daily, weekly, monthly, and yearly backup points.</span><span class="sxs-lookup"><span data-stu-id="43e38-197">Depending on the backup schedule that you selected, on the **Specify Online Retention Policy** page, select the retention policy for daily, weekly, monthly, and yearly backup points.</span></span>

    ![Online_retention_policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sharepoint/specify-online-retention.png)

    > [!NOTE]
    > <span data-ttu-id="43e38-199">MABS uses a grandfather-father-son retention scheme in which a different retention policy can be chosen for different backup points.</span><span class="sxs-lookup"><span data-stu-id="43e38-199">MABS uses a grandfather-father-son retention scheme in which a different retention policy can be chosen for different backup points.</span></span>
    >
    >
12. <span data-ttu-id="43e38-200">Similar to disk, an initial reference point replica needs to be created in Azure.</span><span class="sxs-lookup"><span data-stu-id="43e38-200">Similar to disk, an initial reference point replica needs to be created in Azure.</span></span> <span data-ttu-id="43e38-201">Select your preferred option to create an initial backup copy to Azure, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="43e38-201">Select your preferred option to create an initial backup copy to Azure, and then click **Next**.</span></span>

    ![Online_replica](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sharepoint/online-replication.png)
13. <span data-ttu-id="43e38-203">Review your selected settings on the **Summary** page, and then click **Create Group**.</span><span class="sxs-lookup"><span data-stu-id="43e38-203">Review your selected settings on the **Summary** page, and then click **Create Group**.</span></span> <span data-ttu-id="43e38-204">You will see a success message after the protection group has been created.</span><span class="sxs-lookup"><span data-stu-id="43e38-204">You will see a success message after the protection group has been created.</span></span>

    ![Summary](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sharepoint/summary.png)

## <a name="restore-a-sharepoint-item-from-disk-by-using-mabs"></a><span data-ttu-id="43e38-206">Restore a SharePoint item from disk by using MABS</span><span class="sxs-lookup"><span data-stu-id="43e38-206">Restore a SharePoint item from disk by using MABS</span></span>
<span data-ttu-id="43e38-207">In the following example, the *Recovering SharePoint item* has been accidentally deleted and needs to be recovered.</span><span class="sxs-lookup"><span data-stu-id="43e38-207">In the following example, the *Recovering SharePoint item* has been accidentally deleted and needs to be recovered.</span></span>
<span data-ttu-id="43e38-208">![MABS SharePoint Protection4](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sharepoint/dpm-sharepoint-protection5.png)</span><span class="sxs-lookup"><span data-stu-id="43e38-208">![MABS SharePoint Protection4](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sharepoint/dpm-sharepoint-protection5.png)</span></span>

1. <span data-ttu-id="43e38-209">Open the **DPM Administrator Console**.</span><span class="sxs-lookup"><span data-stu-id="43e38-209">Open the **DPM Administrator Console**.</span></span> <span data-ttu-id="43e38-210">All SharePoint farms that are protected by DPM are shown in the **Protection** tab.</span><span class="sxs-lookup"><span data-stu-id="43e38-210">All SharePoint farms that are protected by DPM are shown in the **Protection** tab.</span></span>

    ![MABS SharePoint Protection3](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sharepoint/dpm-sharepoint-protection4.png)
2. <span data-ttu-id="43e38-212">To begin to recover the item, select the **Recovery** tab.</span><span class="sxs-lookup"><span data-stu-id="43e38-212">To begin to recover the item, select the **Recovery** tab.</span></span>

    ![MABS SharePoint Protection5](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sharepoint/dpm-sharepoint-protection6.png)
3. <span data-ttu-id="43e38-214">You can search SharePoint for *Recovering SharePoint item* by using a wildcard-based search within a recovery point range.</span><span class="sxs-lookup"><span data-stu-id="43e38-214">You can search SharePoint for *Recovering SharePoint item* by using a wildcard-based search within a recovery point range.</span></span>

    ![MABS SharePoint Protection6](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sharepoint/dpm-sharepoint-protection7.png)
4. <span data-ttu-id="43e38-216">Select the appropriate recovery point from the search results, right-click the item, and then select **Recover**.</span><span class="sxs-lookup"><span data-stu-id="43e38-216">Select the appropriate recovery point from the search results, right-click the item, and then select **Recover**.</span></span>
5. <span data-ttu-id="43e38-217">You can also browse through various recovery points and select a database or item to recover.</span><span class="sxs-lookup"><span data-stu-id="43e38-217">You can also browse through various recovery points and select a database or item to recover.</span></span> <span data-ttu-id="43e38-218">Select **Date > Recovery time**, and then select the correct **Database > SharePoint farm > Recovery point > Item**.</span><span class="sxs-lookup"><span data-stu-id="43e38-218">Select **Date > Recovery time**, and then select the correct **Database > SharePoint farm > Recovery point > Item**.</span></span>

    ![MABS SharePoint Protection7](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sharepoint/dpm-sharepoint-protection8.png)
6. <span data-ttu-id="43e38-220">Right-click the item, and then select **Recover** to open the **Recovery Wizard**.</span><span class="sxs-lookup"><span data-stu-id="43e38-220">Right-click the item, and then select **Recover** to open the **Recovery Wizard**.</span></span> <span data-ttu-id="43e38-221">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="43e38-221">Click **Next**.</span></span>

    ![Review Recovery Selection](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sharepoint/review-recovery-selection.png)
7. <span data-ttu-id="43e38-223">Select the type of recovery that you want to perform, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="43e38-223">Select the type of recovery that you want to perform, and then click **Next**.</span></span>

    ![Recovery Type](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sharepoint/select-recovery-type.png)

   > [!NOTE]
   > <span data-ttu-id="43e38-225">The selection of **Recover to original** in the example recovers the item to the original SharePoint site.</span><span class="sxs-lookup"><span data-stu-id="43e38-225">The selection of **Recover to original** in the example recovers the item to the original SharePoint site.</span></span>
   >
   >
8. <span data-ttu-id="43e38-226">Select the **Recovery Process** that you want to use.</span><span class="sxs-lookup"><span data-stu-id="43e38-226">Select the **Recovery Process** that you want to use.</span></span>

   * <span data-ttu-id="43e38-227">Select **Recover without using a recovery farm** if the SharePoint farm has not changed and is the same as the recovery point that is being restored.</span><span class="sxs-lookup"><span data-stu-id="43e38-227">Select **Recover without using a recovery farm** if the SharePoint farm has not changed and is the same as the recovery point that is being restored.</span></span>
   * <span data-ttu-id="43e38-228">Select **Recover using a recovery farm** if the SharePoint farm has changed since the recovery point was created.</span><span class="sxs-lookup"><span data-stu-id="43e38-228">Select **Recover using a recovery farm** if the SharePoint farm has changed since the recovery point was created.</span></span>

     ![Recovery Process](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sharepoint/recovery-process.png)
9. <span data-ttu-id="43e38-230">Provide a staging SQL Server instance location to recover the database temporarily, and provide a staging file share on MABS and the server that's running SharePoint to recover the item.</span><span class="sxs-lookup"><span data-stu-id="43e38-230">Provide a staging SQL Server instance location to recover the database temporarily, and provide a staging file share on MABS and the server that's running SharePoint to recover the item.</span></span>

    ![Staging Location1](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sharepoint/staging-location1.png)

    <span data-ttu-id="43e38-232">MABS attaches the content database that is hosting the SharePoint item to the temporary SQL Server instance.</span><span class="sxs-lookup"><span data-stu-id="43e38-232">MABS attaches the content database that is hosting the SharePoint item to the temporary SQL Server instance.</span></span> <span data-ttu-id="43e38-233">From the content database, it recovers the item and puts it on the staging file location on MABS.</span><span class="sxs-lookup"><span data-stu-id="43e38-233">From the content database, it recovers the item and puts it on the staging file location on MABS.</span></span> <span data-ttu-id="43e38-234">The recovered item that's on the staging location now needs to be exported to the staging location on the SharePoint farm.</span><span class="sxs-lookup"><span data-stu-id="43e38-234">The recovered item that's on the staging location now needs to be exported to the staging location on the SharePoint farm.</span></span>

    ![Staging Location2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sharepoint/staging-location2.png)
10. <span data-ttu-id="43e38-236">Select **Specify recovery options**, and apply security settings to the SharePoint farm or apply the security settings of the recovery point.</span><span class="sxs-lookup"><span data-stu-id="43e38-236">Select **Specify recovery options**, and apply security settings to the SharePoint farm or apply the security settings of the recovery point.</span></span> <span data-ttu-id="43e38-237">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="43e38-237">Click **Next**.</span></span>

    ![Recovery Options](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sharepoint/recovery-options.png)

    > [!NOTE]
    > <span data-ttu-id="43e38-239">You can choose to throttle the network bandwidth usage.</span><span class="sxs-lookup"><span data-stu-id="43e38-239">You can choose to throttle the network bandwidth usage.</span></span> <span data-ttu-id="43e38-240">This minimizes impact to the production server during production hours.</span><span class="sxs-lookup"><span data-stu-id="43e38-240">This minimizes impact to the production server during production hours.</span></span>
    >
    >
11. <span data-ttu-id="43e38-241">Review the summary information, and then click **Recover** to begin recovery of the file.</span><span class="sxs-lookup"><span data-stu-id="43e38-241">Review the summary information, and then click **Recover** to begin recovery of the file.</span></span>

    ![Recovery summary](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sharepoint/recovery-summary.png)
12. <span data-ttu-id="43e38-243">Now select the **Monitoring** tab in the **MABS Administrator Console** to view the **Status** of the recovery.</span><span class="sxs-lookup"><span data-stu-id="43e38-243">Now select the **Monitoring** tab in the **MABS Administrator Console** to view the **Status** of the recovery.</span></span>

    ![Recovery Status](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sharepoint/recovery-monitoring.png)

    > [!NOTE]
    > <span data-ttu-id="43e38-245">The file is now restored.</span><span class="sxs-lookup"><span data-stu-id="43e38-245">The file is now restored.</span></span> <span data-ttu-id="43e38-246">You can refresh the SharePoint site to check the restored file.</span><span class="sxs-lookup"><span data-stu-id="43e38-246">You can refresh the SharePoint site to check the restored file.</span></span>
    >
    >

## <a name="restore-a-sharepoint-database-from-azure-by-using-dpm"></a><span data-ttu-id="43e38-247">Restore a SharePoint database from Azure by using DPM</span><span class="sxs-lookup"><span data-stu-id="43e38-247">Restore a SharePoint database from Azure by using DPM</span></span>
1. <span data-ttu-id="43e38-248">To recover a SharePoint content database, browse through various recovery points (as shown previously), and select the recovery point that you want to restore.</span><span class="sxs-lookup"><span data-stu-id="43e38-248">To recover a SharePoint content database, browse through various recovery points (as shown previously), and select the recovery point that you want to restore.</span></span>

    ![MABS SharePoint Protection8](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sharepoint/dpm-sharepoint-protection9.png)
2. <span data-ttu-id="43e38-250">Double-click the SharePoint recovery point to show the available SharePoint catalog information.</span><span class="sxs-lookup"><span data-stu-id="43e38-250">Double-click the SharePoint recovery point to show the available SharePoint catalog information.</span></span>

   > [!NOTE]
   > <span data-ttu-id="43e38-251">Because the SharePoint farm is protected for long-term retention in Azure, no catalog information (metadata) is available on MABS.</span><span class="sxs-lookup"><span data-stu-id="43e38-251">Because the SharePoint farm is protected for long-term retention in Azure, no catalog information (metadata) is available on MABS.</span></span> <span data-ttu-id="43e38-252">As a result, whenever a point-in-time SharePoint content database needs to be recovered, you need to catalog the SharePoint farm again.</span><span class="sxs-lookup"><span data-stu-id="43e38-252">As a result, whenever a point-in-time SharePoint content database needs to be recovered, you need to catalog the SharePoint farm again.</span></span>
   >
   >
3. <span data-ttu-id="43e38-253">Click **Re-catalog**.</span><span class="sxs-lookup"><span data-stu-id="43e38-253">Click **Re-catalog**.</span></span>

    ![MABS SharePoint Protection10](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sharepoint/dpm-sharepoint-protection12.png)

    <span data-ttu-id="43e38-255">The **Cloud Recatalog** status window opens.</span><span class="sxs-lookup"><span data-stu-id="43e38-255">The **Cloud Recatalog** status window opens.</span></span>

    ![MABS SharePoint Protection11](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sharepoint/dpm-sharepoint-protection13.png)

    <span data-ttu-id="43e38-257">After cataloging is finished, the status changes to *Success*.</span><span class="sxs-lookup"><span data-stu-id="43e38-257">After cataloging is finished, the status changes to *Success*.</span></span> <span data-ttu-id="43e38-258">Click **Close**.</span><span class="sxs-lookup"><span data-stu-id="43e38-258">Click **Close**.</span></span>

    ![MABS SharePoint Protection12](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sharepoint/dpm-sharepoint-protection14.png)
4. <span data-ttu-id="43e38-260">Click the SharePoint object shown in the MABS **Recovery** tab to get the content database structure.</span><span class="sxs-lookup"><span data-stu-id="43e38-260">Click the SharePoint object shown in the MABS **Recovery** tab to get the content database structure.</span></span> <span data-ttu-id="43e38-261">Right-click the item, and then click **Recover**.</span><span class="sxs-lookup"><span data-stu-id="43e38-261">Right-click the item, and then click **Recover**.</span></span>

    ![MABS SharePoint Protection13](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sharepoint/dpm-sharepoint-protection15.png)
5. <span data-ttu-id="43e38-263">At this point, follow the [recovery steps earlier in this article](#restore-a-sharepoint-item-from-disk-using-dpm) to recover a SharePoint content database from disk.</span><span class="sxs-lookup"><span data-stu-id="43e38-263">At this point, follow the [recovery steps earlier in this article](#restore-a-sharepoint-item-from-disk-using-dpm) to recover a SharePoint content database from disk.</span></span>

## <a name="faqs"></a><span data-ttu-id="43e38-264">FAQs</span><span class="sxs-lookup"><span data-stu-id="43e38-264">FAQs</span></span>
<span data-ttu-id="43e38-265">Q: Can I recover a SharePoint item to the original location if SharePoint is configured by using SQL AlwaysOn (with protection on disk)?</span><span class="sxs-lookup"><span data-stu-id="43e38-265">Q: Can I recover a SharePoint item to the original location if SharePoint is configured by using SQL AlwaysOn (with protection on disk)?</span></span><br>
<span data-ttu-id="43e38-266">A: Yes, the item can be recovered to the original SharePoint site.</span><span class="sxs-lookup"><span data-stu-id="43e38-266">A: Yes, the item can be recovered to the original SharePoint site.</span></span>

<span data-ttu-id="43e38-267">Q: Can I recover a SharePoint database to the original location if SharePoint is configured by using SQL AlwaysOn?</span><span class="sxs-lookup"><span data-stu-id="43e38-267">Q: Can I recover a SharePoint database to the original location if SharePoint is configured by using SQL AlwaysOn?</span></span><br>
<span data-ttu-id="43e38-268">A: Because SharePoint databases are configured in SQL AlwaysOn, they cannot be modified unless the availability group is removed.</span><span class="sxs-lookup"><span data-stu-id="43e38-268">A: Because SharePoint databases are configured in SQL AlwaysOn, they cannot be modified unless the availability group is removed.</span></span> <span data-ttu-id="43e38-269">As a result, MABS cannot restore a database to the original location.</span><span class="sxs-lookup"><span data-stu-id="43e38-269">As a result, MABS cannot restore a database to the original location.</span></span> <span data-ttu-id="43e38-270">You can recover a SQL Server database to another SQL Server instance.</span><span class="sxs-lookup"><span data-stu-id="43e38-270">You can recover a SQL Server database to another SQL Server instance.</span></span>

## <a name="next-steps"></a><span data-ttu-id="43e38-271">Next steps</span><span class="sxs-lookup"><span data-stu-id="43e38-271">Next steps</span></span>
* <span data-ttu-id="43e38-272">Learn more about MABS Protection of SharePoint - see [Video Series - DPM Protection of SharePoint](http://channel9.msdn.com/Series/Azure-Backup/Microsoft-SCDPM-Protection-of-SharePoint-1-of-2-How-to-create-a-SharePoint-Protection-Group)</span><span class="sxs-lookup"><span data-stu-id="43e38-272">Learn more about MABS Protection of SharePoint - see [Video Series - DPM Protection of SharePoint](http://channel9.msdn.com/Series/Azure-Backup/Microsoft-SCDPM-Protection-of-SharePoint-1-of-2-How-to-create-a-SharePoint-Protection-Group)</span></span>






























