---
title: DPM/Azure Backup server protection of a SharePoint farm to Azure | Microsoft Docs
description: This article provides an overview of DPM/Azure Backup server protection of a SharePoint farm to Azure
services: backup
documentationcenter: ''
author: adigan
manager: Nkolli1
editor: ''
ms.assetid: e0c0c252-dc1d-4072-b777-7222c13950b0
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/29/2016
ms.author: adigan;giridham;jimpark;trinadhk;markgal
ms.openlocfilehash: 0bb8caad04aedbdb322df8f98823761787f343d9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556172"
---
# <a name="back-up-a-sharepoint-farm-to-azure"></a><span data-ttu-id="6d132-103">Back up a SharePoint farm to Azure</span><span class="sxs-lookup"><span data-stu-id="6d132-103">Back up a SharePoint farm to Azure</span></span>
<span data-ttu-id="6d132-104">You back up a SharePoint farm to Microsoft Azure by using System Center Data Protection Manager (DPM) in much the same way that you back up other data sources.</span><span class="sxs-lookup"><span data-stu-id="6d132-104">You back up a SharePoint farm to Microsoft Azure by using System Center Data Protection Manager (DPM) in much the same way that you back up other data sources.</span></span> <span data-ttu-id="6d132-105">Azure Backup provides flexibility in the backup schedule to create daily, weekly, monthly, or yearly backup points and gives you retention policy options for various backup points.</span><span class="sxs-lookup"><span data-stu-id="6d132-105">Azure Backup provides flexibility in the backup schedule to create daily, weekly, monthly, or yearly backup points and gives you retention policy options for various backup points.</span></span> <span data-ttu-id="6d132-106">DPM provides the capability to store local disk copies for quick recovery-time objectives (RTO) and to store copies to Azure for economical, long-term retention.</span><span class="sxs-lookup"><span data-stu-id="6d132-106">DPM provides the capability to store local disk copies for quick recovery-time objectives (RTO) and to store copies to Azure for economical, long-term retention.</span></span>

## <a name="sharepoint-supported-versions-and-related-protection-scenarios"></a><span data-ttu-id="6d132-107">SharePoint supported versions and related protection scenarios</span><span class="sxs-lookup"><span data-stu-id="6d132-107">SharePoint supported versions and related protection scenarios</span></span>
<span data-ttu-id="6d132-108">Azure Backup for DPM supports the following scenarios:</span><span class="sxs-lookup"><span data-stu-id="6d132-108">Azure Backup for DPM supports the following scenarios:</span></span>

| <span data-ttu-id="6d132-109">Workload</span><span class="sxs-lookup"><span data-stu-id="6d132-109">Workload</span></span> | <span data-ttu-id="6d132-110">Version</span><span class="sxs-lookup"><span data-stu-id="6d132-110">Version</span></span> | <span data-ttu-id="6d132-111">SharePoint deployment</span><span class="sxs-lookup"><span data-stu-id="6d132-111">SharePoint deployment</span></span> | <span data-ttu-id="6d132-112">DPM deployment type</span><span class="sxs-lookup"><span data-stu-id="6d132-112">DPM deployment type</span></span> | <span data-ttu-id="6d132-113">DPM - System Center 2012 R2</span><span class="sxs-lookup"><span data-stu-id="6d132-113">DPM - System Center 2012 R2</span></span> | <span data-ttu-id="6d132-114">Protection and recovery</span><span class="sxs-lookup"><span data-stu-id="6d132-114">Protection and recovery</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="6d132-115">SharePoint</span><span class="sxs-lookup"><span data-stu-id="6d132-115">SharePoint</span></span> |<span data-ttu-id="6d132-116">SharePoint 2013, SharePoint 2010, SharePoint 2007, SharePoint 3.0</span><span class="sxs-lookup"><span data-stu-id="6d132-116">SharePoint 2013, SharePoint 2010, SharePoint 2007, SharePoint 3.0</span></span> |<span data-ttu-id="6d132-117">SharePoint deployed as a physical server or Hyper-V/VMware virtual machine</span><span class="sxs-lookup"><span data-stu-id="6d132-117">SharePoint deployed as a physical server or Hyper-V/VMware virtual machine</span></span> <br> -------------- <br> <span data-ttu-id="6d132-118">SQL AlwaysOn</span><span class="sxs-lookup"><span data-stu-id="6d132-118">SQL AlwaysOn</span></span> |<span data-ttu-id="6d132-119">Physical server or on-premises Hyper-V virtual machine</span><span class="sxs-lookup"><span data-stu-id="6d132-119">Physical server or on-premises Hyper-V virtual machine</span></span> |<span data-ttu-id="6d132-120">Supports backup to Azure from Update Rollup 5</span><span class="sxs-lookup"><span data-stu-id="6d132-120">Supports backup to Azure from Update Rollup 5</span></span> |<span data-ttu-id="6d132-121">Protect SharePoint Farm recovery options: Recovery farm, database, and file or list item from disk recovery points.</span><span class="sxs-lookup"><span data-stu-id="6d132-121">Protect SharePoint Farm recovery options: Recovery farm, database, and file or list item from disk recovery points.</span></span>  <span data-ttu-id="6d132-122">Farm and database recovery from Azure recovery points.</span><span class="sxs-lookup"><span data-stu-id="6d132-122">Farm and database recovery from Azure recovery points.</span></span> |

## <a name="before-you-start"></a><span data-ttu-id="6d132-123">Before you start</span><span class="sxs-lookup"><span data-stu-id="6d132-123">Before you start</span></span>
<span data-ttu-id="6d132-124">There are a few things you need to confirm before you back up a SharePoint farm to Azure.</span><span class="sxs-lookup"><span data-stu-id="6d132-124">There are a few things you need to confirm before you back up a SharePoint farm to Azure.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="6d132-125">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="6d132-125">Prerequisites</span></span>
<span data-ttu-id="6d132-126">Before you proceed, make sure that you have met all the [prerequisites for using Microsoft Azure Backup](backup-azure-dpm-introduction.md#prerequisites) to protect workloads.</span><span class="sxs-lookup"><span data-stu-id="6d132-126">Before you proceed, make sure that you have met all the [prerequisites for using Microsoft Azure Backup](backup-azure-dpm-introduction.md#prerequisites) to protect workloads.</span></span> <span data-ttu-id="6d132-127">Some tasks for prerequisites include: create a backup vault, download vault credentials, install Azure Backup Agent, and register DPM/Azure Backup Server with the vault.</span><span class="sxs-lookup"><span data-stu-id="6d132-127">Some tasks for prerequisites include: create a backup vault, download vault credentials, install Azure Backup Agent, and register DPM/Azure Backup Server with the vault.</span></span>

### <a name="dpm-agent"></a><span data-ttu-id="6d132-128">DPM agent</span><span class="sxs-lookup"><span data-stu-id="6d132-128">DPM agent</span></span>
<span data-ttu-id="6d132-129">The DPM agent must be installed on the server that's running SharePoint, the servers that are running SQL Server, and all other servers that are part of the SharePoint farm.</span><span class="sxs-lookup"><span data-stu-id="6d132-129">The DPM agent must be installed on the server that's running SharePoint, the servers that are running SQL Server, and all other servers that are part of the SharePoint farm.</span></span> <span data-ttu-id="6d132-130">For more information about how to set up the protection agent, see [Setup Protection Agent](https://technet.microsoft.com/library/hh758034\(v=sc.12\).aspx).</span><span class="sxs-lookup"><span data-stu-id="6d132-130">For more information about how to set up the protection agent, see [Setup Protection Agent](https://technet.microsoft.com/library/hh758034\(v=sc.12\).aspx).</span></span>  <span data-ttu-id="6d132-131">The one exception is that you install the agent only on a single web front end (WFE) server.</span><span class="sxs-lookup"><span data-stu-id="6d132-131">The one exception is that you install the agent only on a single web front end (WFE) server.</span></span> <span data-ttu-id="6d132-132">DPM needs the agent on one WFE server only to serve as the entry point for protection.</span><span class="sxs-lookup"><span data-stu-id="6d132-132">DPM needs the agent on one WFE server only to serve as the entry point for protection.</span></span>

### <a name="sharepoint-farm"></a><span data-ttu-id="6d132-133">SharePoint farm</span><span class="sxs-lookup"><span data-stu-id="6d132-133">SharePoint farm</span></span>
<span data-ttu-id="6d132-134">For every 10 million items in the farm, there must be at least 2 GB of space on the volume where the DPM folder is located.</span><span class="sxs-lookup"><span data-stu-id="6d132-134">For every 10 million items in the farm, there must be at least 2 GB of space on the volume where the DPM folder is located.</span></span> <span data-ttu-id="6d132-135">This space is required for catalog generation.</span><span class="sxs-lookup"><span data-stu-id="6d132-135">This space is required for catalog generation.</span></span> <span data-ttu-id="6d132-136">For DPM to recover specific items (site collections, sites, lists, document libraries, folders, individual documents, and list items), catalog generation creates a list of the URLs that are contained within each content database.</span><span class="sxs-lookup"><span data-stu-id="6d132-136">For DPM to recover specific items (site collections, sites, lists, document libraries, folders, individual documents, and list items), catalog generation creates a list of the URLs that are contained within each content database.</span></span> <span data-ttu-id="6d132-137">You can view the list of URLs in the recoverable item pane in the **Recovery** task area of DPM Administrator Console.</span><span class="sxs-lookup"><span data-stu-id="6d132-137">You can view the list of URLs in the recoverable item pane in the **Recovery** task area of DPM Administrator Console.</span></span>

### <a name="sql-server"></a><span data-ttu-id="6d132-138">SQL Server</span><span class="sxs-lookup"><span data-stu-id="6d132-138">SQL Server</span></span>
<span data-ttu-id="6d132-139">DPM runs as a LocalSystem account.</span><span class="sxs-lookup"><span data-stu-id="6d132-139">DPM runs as a LocalSystem account.</span></span> <span data-ttu-id="6d132-140">To back up SQL Server databases, DPM needs sysadmin privileges on that account for the server that's running SQL Server.</span><span class="sxs-lookup"><span data-stu-id="6d132-140">To back up SQL Server databases, DPM needs sysadmin privileges on that account for the server that's running SQL Server.</span></span> <span data-ttu-id="6d132-141">Set NT AUTHORITY\SYSTEM to *sysadmin* on the server that's running SQL Server before you back it up.</span><span class="sxs-lookup"><span data-stu-id="6d132-141">Set NT AUTHORITY\SYSTEM to *sysadmin* on the server that's running SQL Server before you back it up.</span></span>

<span data-ttu-id="6d132-142">If the SharePoint farm has SQL Server databases that are configured with SQL Server aliases, install the SQL Server client components on the front-end Web server that DPM will protect.</span><span class="sxs-lookup"><span data-stu-id="6d132-142">If the SharePoint farm has SQL Server databases that are configured with SQL Server aliases, install the SQL Server client components on the front-end Web server that DPM will protect.</span></span>

### <a name="sharepoint-server"></a><span data-ttu-id="6d132-143">SharePoint Server</span><span class="sxs-lookup"><span data-stu-id="6d132-143">SharePoint Server</span></span>
<span data-ttu-id="6d132-144">While performance depends on many factors such as size of SharePoint farm, as general guidance one DPM server can protect a 25 TB SharePoint farm.</span><span class="sxs-lookup"><span data-stu-id="6d132-144">While performance depends on many factors such as size of SharePoint farm, as general guidance one DPM server can protect a 25 TB SharePoint farm.</span></span>

### <a name="dpm-update-rollup-5"></a><span data-ttu-id="6d132-145">DPM Update Rollup 5</span><span class="sxs-lookup"><span data-stu-id="6d132-145">DPM Update Rollup 5</span></span>
<span data-ttu-id="6d132-146">To begin protection of a SharePoint farm to Azure, you need to install DPM Update Rollup 5 or later.</span><span class="sxs-lookup"><span data-stu-id="6d132-146">To begin protection of a SharePoint farm to Azure, you need to install DPM Update Rollup 5 or later.</span></span> <span data-ttu-id="6d132-147">Update Rollup 5 provides the ability to protect a SharePoint farm to Azure if the farm is configured by using SQL AlwaysOn.</span><span class="sxs-lookup"><span data-stu-id="6d132-147">Update Rollup 5 provides the ability to protect a SharePoint farm to Azure if the farm is configured by using SQL AlwaysOn.</span></span>
<span data-ttu-id="6d132-148">For more information, see the blog post that introduces [DPM Update Rollup 5](http://blogs.technet.com/b/dpm/archive/2015/02/11/update-rollup-5-for-system-center-2012-r2-data-protection-manager-is-now-available.aspx)</span><span class="sxs-lookup"><span data-stu-id="6d132-148">For more information, see the blog post that introduces [DPM Update Rollup 5](http://blogs.technet.com/b/dpm/archive/2015/02/11/update-rollup-5-for-system-center-2012-r2-data-protection-manager-is-now-available.aspx)</span></span>

### <a name="whats-not-supported"></a><span data-ttu-id="6d132-149">What's not supported</span><span class="sxs-lookup"><span data-stu-id="6d132-149">What's not supported</span></span>
* <span data-ttu-id="6d132-150">DPM that protects a SharePoint farm does not protect search indexes or application service databases.</span><span class="sxs-lookup"><span data-stu-id="6d132-150">DPM that protects a SharePoint farm does not protect search indexes or application service databases.</span></span> <span data-ttu-id="6d132-151">You will need to configure the protection of these databases separately.</span><span class="sxs-lookup"><span data-stu-id="6d132-151">You will need to configure the protection of these databases separately.</span></span>
* <span data-ttu-id="6d132-152">DPM does not provide backup of SharePoint SQL Server databases that are hosted on scale-out file server (SOFS) shares.</span><span class="sxs-lookup"><span data-stu-id="6d132-152">DPM does not provide backup of SharePoint SQL Server databases that are hosted on scale-out file server (SOFS) shares.</span></span>

## <a name="configure-sharepoint-protection"></a><span data-ttu-id="6d132-153">Configure SharePoint protection</span><span class="sxs-lookup"><span data-stu-id="6d132-153">Configure SharePoint protection</span></span>
<span data-ttu-id="6d132-154">Before you can use DPM to protect SharePoint, you must configure the SharePoint VSS Writer service (WSS Writer service) by using **ConfigureSharePoint.exe**.</span><span class="sxs-lookup"><span data-stu-id="6d132-154">Before you can use DPM to protect SharePoint, you must configure the SharePoint VSS Writer service (WSS Writer service) by using **ConfigureSharePoint.exe**.</span></span>

<span data-ttu-id="6d132-155">You can find **ConfigureSharePoint.exe** in the [DPM Installation Path]\bin folder on the front-end web server.</span><span class="sxs-lookup"><span data-stu-id="6d132-155">You can find **ConfigureSharePoint.exe** in the [DPM Installation Path]\bin folder on the front-end web server.</span></span> <span data-ttu-id="6d132-156">This tool provides the protection agent with the credentials for the SharePoint farm.</span><span class="sxs-lookup"><span data-stu-id="6d132-156">This tool provides the protection agent with the credentials for the SharePoint farm.</span></span> <span data-ttu-id="6d132-157">You run it on a single WFE server.</span><span class="sxs-lookup"><span data-stu-id="6d132-157">You run it on a single WFE server.</span></span> <span data-ttu-id="6d132-158">If you have multiple WFE servers, select just one when you configure a protection group.</span><span class="sxs-lookup"><span data-stu-id="6d132-158">If you have multiple WFE servers, select just one when you configure a protection group.</span></span>

### <a name="to-configure-the-sharepoint-vss-writer-service"></a><span data-ttu-id="6d132-159">To configure the SharePoint VSS Writer service</span><span class="sxs-lookup"><span data-stu-id="6d132-159">To configure the SharePoint VSS Writer service</span></span>
1. <span data-ttu-id="6d132-160">On the WFE server, at a command prompt, go to [DPM installation location]\bin\\</span><span class="sxs-lookup"><span data-stu-id="6d132-160">On the WFE server, at a command prompt, go to [DPM installation location]\bin\\</span></span>
2. <span data-ttu-id="6d132-161">Enter ConfigureSharePoint -EnableSharePointProtection.</span><span class="sxs-lookup"><span data-stu-id="6d132-161">Enter ConfigureSharePoint -EnableSharePointProtection.</span></span>
3. <span data-ttu-id="6d132-162">Enter the farm administrator credentials.</span><span class="sxs-lookup"><span data-stu-id="6d132-162">Enter the farm administrator credentials.</span></span> <span data-ttu-id="6d132-163">This account should be a member of the local Administrator group on the WFE server.</span><span class="sxs-lookup"><span data-stu-id="6d132-163">This account should be a member of the local Administrator group on the WFE server.</span></span> <span data-ttu-id="6d132-164">If the farm administrator isn’t a local admin grant the following permissions on the WFE server:</span><span class="sxs-lookup"><span data-stu-id="6d132-164">If the farm administrator isn’t a local admin grant the following permissions on the WFE server:</span></span>
   * <span data-ttu-id="6d132-165">Grant the WSS_Admin_WPG group full control to the DPM folder (%Program Files%\Microsoft Data Protection Manager\DPM).</span><span class="sxs-lookup"><span data-stu-id="6d132-165">Grant the WSS_Admin_WPG group full control to the DPM folder (%Program Files%\Microsoft Data Protection Manager\DPM).</span></span>
   * <span data-ttu-id="6d132-166">Grant the WSS_Admin_WPG group read access to the DPM Registry key (HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager).</span><span class="sxs-lookup"><span data-stu-id="6d132-166">Grant the WSS_Admin_WPG group read access to the DPM Registry key (HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager).</span></span>

> [!NOTE]
> <span data-ttu-id="6d132-167">You’ll need to rerun ConfigureSharePoint.exe whenever there’s a change in the SharePoint farm administrator credentials.</span><span class="sxs-lookup"><span data-stu-id="6d132-167">You’ll need to rerun ConfigureSharePoint.exe whenever there’s a change in the SharePoint farm administrator credentials.</span></span>
> 
> 

## <a name="back-up-a-sharepoint-farm-by-using-dpm"></a><span data-ttu-id="6d132-168">Back up a SharePoint farm by using DPM</span><span class="sxs-lookup"><span data-stu-id="6d132-168">Back up a SharePoint farm by using DPM</span></span>
<span data-ttu-id="6d132-169">After you have configured DPM and the SharePoint farm as explained previously, SharePoint can be protected by DPM.</span><span class="sxs-lookup"><span data-stu-id="6d132-169">After you have configured DPM and the SharePoint farm as explained previously, SharePoint can be protected by DPM.</span></span>

### <a name="to-protect-a-sharepoint-farm"></a><span data-ttu-id="6d132-170">To protect a SharePoint farm</span><span class="sxs-lookup"><span data-stu-id="6d132-170">To protect a SharePoint farm</span></span>
1. <span data-ttu-id="6d132-171">From the **Protection** tab of the DPM Administrator Console, click **New**.</span><span class="sxs-lookup"><span data-stu-id="6d132-171">From the **Protection** tab of the DPM Administrator Console, click **New**.</span></span>
    <span data-ttu-id="6d132-172">![New Protection Tab](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sharepoint/dpm-new-protection-tab.png)</span><span class="sxs-lookup"><span data-stu-id="6d132-172">![New Protection Tab](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sharepoint/dpm-new-protection-tab.png)</span></span>
2. <span data-ttu-id="6d132-173">On the **Select Protection Group Type** page of the **Create New Protection Group** wizard, select **Servers**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="6d132-173">On the **Select Protection Group Type** page of the **Create New Protection Group** wizard, select **Servers**, and then click **Next**.</span></span>
   
    ![Select Protection Group type](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sharepoint/select-protection-group-type.png)
3. <span data-ttu-id="6d132-175">On the **Select Group Members** screen, select the check box for the SharePoint server you want to protect and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="6d132-175">On the **Select Group Members** screen, select the check box for the SharePoint server you want to protect and click **Next**.</span></span>
   
    ![Select group members](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sharepoint/select-group-members2.png)
   
   > [!NOTE]
   > <span data-ttu-id="6d132-177">With the DPM agent installed, you can see the server in the wizard.</span><span class="sxs-lookup"><span data-stu-id="6d132-177">With the DPM agent installed, you can see the server in the wizard.</span></span> <span data-ttu-id="6d132-178">DPM also shows its structure.</span><span class="sxs-lookup"><span data-stu-id="6d132-178">DPM also shows its structure.</span></span> <span data-ttu-id="6d132-179">Because you ran ConfigureSharePoint.exe, DPM communicates with the SharePoint VSS Writer service and its corresponding SQL Server databases and recognizes the SharePoint farm structure, the associated content databases, and any corresponding items.</span><span class="sxs-lookup"><span data-stu-id="6d132-179">Because you ran ConfigureSharePoint.exe, DPM communicates with the SharePoint VSS Writer service and its corresponding SQL Server databases and recognizes the SharePoint farm structure, the associated content databases, and any corresponding items.</span></span>
   > 
   > 
4. <span data-ttu-id="6d132-180">On the **Select Data Protection Method** page, enter the name of the **Protection Group**, and select your preferred *protection methods*.</span><span class="sxs-lookup"><span data-stu-id="6d132-180">On the **Select Data Protection Method** page, enter the name of the **Protection Group**, and select your preferred *protection methods*.</span></span> <span data-ttu-id="6d132-181">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="6d132-181">Click **Next**.</span></span>
   
    ![Select data protection method](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sharepoint/select-data-protection-method1.png)
   
   > [!NOTE]
   > <span data-ttu-id="6d132-183">The disk protection method helps to meet short recovery-time objectives.</span><span class="sxs-lookup"><span data-stu-id="6d132-183">The disk protection method helps to meet short recovery-time objectives.</span></span> <span data-ttu-id="6d132-184">Azure is an economical, long-term protection target compared to tapes.</span><span class="sxs-lookup"><span data-stu-id="6d132-184">Azure is an economical, long-term protection target compared to tapes.</span></span> <span data-ttu-id="6d132-185">For more information, see [Use Azure Backup to replace your tape infrastructure](https://azure.microsoft.com/documentation/articles/backup-azure-backup-cloud-as-tape/)</span><span class="sxs-lookup"><span data-stu-id="6d132-185">For more information, see [Use Azure Backup to replace your tape infrastructure](https://azure.microsoft.com/documentation/articles/backup-azure-backup-cloud-as-tape/)</span></span>
   > 
   > 
5. <span data-ttu-id="6d132-186">On the **Specify Short-Term Goals** page, select your preferred **Retention range** and identify when you want backups to occur.</span><span class="sxs-lookup"><span data-stu-id="6d132-186">On the **Specify Short-Term Goals** page, select your preferred **Retention range** and identify when you want backups to occur.</span></span>
   
    ![Specify short-term goals](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sharepoint/specify-short-term-goals2.png)
   
   > [!NOTE]
   > <span data-ttu-id="6d132-188">Because recovery is most often required for data that's less than five days old, we selected a retention range of five days on disk and ensured that the backup happens during non-production hours, for this example.</span><span class="sxs-lookup"><span data-stu-id="6d132-188">Because recovery is most often required for data that's less than five days old, we selected a retention range of five days on disk and ensured that the backup happens during non-production hours, for this example.</span></span>
   > 
   > 
6. <span data-ttu-id="6d132-189">Review the storage pool disk space allocated for the protection group, and click then **Next**.</span><span class="sxs-lookup"><span data-stu-id="6d132-189">Review the storage pool disk space allocated for the protection group, and click then **Next**.</span></span>
7. <span data-ttu-id="6d132-190">For every protection group, DPM allocates disk space to store and manage replicas.</span><span class="sxs-lookup"><span data-stu-id="6d132-190">For every protection group, DPM allocates disk space to store and manage replicas.</span></span> <span data-ttu-id="6d132-191">At this point, DPM must create a copy of the selected data.</span><span class="sxs-lookup"><span data-stu-id="6d132-191">At this point, DPM must create a copy of the selected data.</span></span> <span data-ttu-id="6d132-192">Select how and when you want the replica created, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="6d132-192">Select how and when you want the replica created, and then click **Next**.</span></span>
   
    ![Choose replica creation method](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sharepoint/choose-replica-creation-method.png)
   
   > [!NOTE]
   > <span data-ttu-id="6d132-194">To make sure that network traffic is not effected, select a time outside production hours.</span><span class="sxs-lookup"><span data-stu-id="6d132-194">To make sure that network traffic is not effected, select a time outside production hours.</span></span>
   > 
   > 
8. <span data-ttu-id="6d132-195">DPM ensures data integrity by performing consistency checks on the replica.</span><span class="sxs-lookup"><span data-stu-id="6d132-195">DPM ensures data integrity by performing consistency checks on the replica.</span></span> <span data-ttu-id="6d132-196">There are two available options.</span><span class="sxs-lookup"><span data-stu-id="6d132-196">There are two available options.</span></span> <span data-ttu-id="6d132-197">You can define a schedule to run consistency checks, or DPM can run consistency checks automatically on the replica whenever it becomes inconsistent.</span><span class="sxs-lookup"><span data-stu-id="6d132-197">You can define a schedule to run consistency checks, or DPM can run consistency checks automatically on the replica whenever it becomes inconsistent.</span></span> <span data-ttu-id="6d132-198">Select your preferred option, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="6d132-198">Select your preferred option, and then click **Next**.</span></span>
   
    ![Consistency Check](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sharepoint/consistency-check.png)
9. <span data-ttu-id="6d132-200">On the **Specify Online Protection Data** page, select the SharePoint farm that you want to protect, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="6d132-200">On the **Specify Online Protection Data** page, select the SharePoint farm that you want to protect, and then click **Next**.</span></span>
   
    ![DPM SharePoint Protection1](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sharepoint/select-online-protection1.png)
10. <span data-ttu-id="6d132-202">On the **Specify Online Backup Schedule** page, select your preferred schedule, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="6d132-202">On the **Specify Online Backup Schedule** page, select your preferred schedule, and then click **Next**.</span></span>
    
    ![Online_backup_schedule](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sharepoint/specify-online-backup-schedule.png)
    
    > [!NOTE]
    > <span data-ttu-id="6d132-204">DPM provides a maximum of two daily backups to Azure at different times.</span><span class="sxs-lookup"><span data-stu-id="6d132-204">DPM provides a maximum of two daily backups to Azure at different times.</span></span> <span data-ttu-id="6d132-205">Azure Backup can also control the amount of WAN bandwidth that can be used for backups in peak and off-peak hours by using [Azure Backup Network Throttling](https://azure.microsoft.com/en-in/documentation/articles/backup-configure-vault/#enable-network-throttling).</span><span class="sxs-lookup"><span data-stu-id="6d132-205">Azure Backup can also control the amount of WAN bandwidth that can be used for backups in peak and off-peak hours by using [Azure Backup Network Throttling](https://azure.microsoft.com/en-in/documentation/articles/backup-configure-vault/#enable-network-throttling).</span></span>
    > 
    > 
11. <span data-ttu-id="6d132-206">Depending on the backup schedule that you selected, on the **Specify Online Retention Policy** page, select the retention policy for daily, weekly, monthly, and yearly backup points.</span><span class="sxs-lookup"><span data-stu-id="6d132-206">Depending on the backup schedule that you selected, on the **Specify Online Retention Policy** page, select the retention policy for daily, weekly, monthly, and yearly backup points.</span></span>
    
    ![Online_retention_policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sharepoint/specify-online-retention.png)
    
    > [!NOTE]
    > <span data-ttu-id="6d132-208">DPM uses a grandfather-father-son retention scheme in which a different retention policy can be chosen for different backup points.</span><span class="sxs-lookup"><span data-stu-id="6d132-208">DPM uses a grandfather-father-son retention scheme in which a different retention policy can be chosen for different backup points.</span></span>
    > 
    > 
12. <span data-ttu-id="6d132-209">Similar to disk, an initial reference point replica needs to be created in Azure.</span><span class="sxs-lookup"><span data-stu-id="6d132-209">Similar to disk, an initial reference point replica needs to be created in Azure.</span></span> <span data-ttu-id="6d132-210">Select your preferred option to create an initial backup copy to Azure, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="6d132-210">Select your preferred option to create an initial backup copy to Azure, and then click **Next**.</span></span>
    
    ![Online_replica](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sharepoint/online-replication.png)
13. <span data-ttu-id="6d132-212">Review your selected settings on the **Summary** page, and then click **Create Group**.</span><span class="sxs-lookup"><span data-stu-id="6d132-212">Review your selected settings on the **Summary** page, and then click **Create Group**.</span></span> <span data-ttu-id="6d132-213">You will see a success message after the protection group has been created.</span><span class="sxs-lookup"><span data-stu-id="6d132-213">You will see a success message after the protection group has been created.</span></span>
    
    ![Summary](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sharepoint/summary.png)

## <a name="restore-a-sharepoint-item-from-disk-by-using-dpm"></a><span data-ttu-id="6d132-215">Restore a SharePoint item from disk by using DPM</span><span class="sxs-lookup"><span data-stu-id="6d132-215">Restore a SharePoint item from disk by using DPM</span></span>
<span data-ttu-id="6d132-216">In the following example, the *Recovering SharePoint item* has been accidentally deleted and needs to be recovered.</span><span class="sxs-lookup"><span data-stu-id="6d132-216">In the following example, the *Recovering SharePoint item* has been accidentally deleted and needs to be recovered.</span></span>
<span data-ttu-id="6d132-217">![DPM SharePoint Protection4](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sharepoint/dpm-sharepoint-protection5.png)</span><span class="sxs-lookup"><span data-stu-id="6d132-217">![DPM SharePoint Protection4](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sharepoint/dpm-sharepoint-protection5.png)</span></span>

1. <span data-ttu-id="6d132-218">Open the **DPM Administrator Console**.</span><span class="sxs-lookup"><span data-stu-id="6d132-218">Open the **DPM Administrator Console**.</span></span> <span data-ttu-id="6d132-219">All SharePoint farms that are protected by DPM are shown in the **Protection** tab.</span><span class="sxs-lookup"><span data-stu-id="6d132-219">All SharePoint farms that are protected by DPM are shown in the **Protection** tab.</span></span>
   
    ![DPM SharePoint Protection3](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sharepoint/dpm-sharepoint-protection4.png)
2. <span data-ttu-id="6d132-221">To begin to recover the item, select the **Recovery** tab.</span><span class="sxs-lookup"><span data-stu-id="6d132-221">To begin to recover the item, select the **Recovery** tab.</span></span>
   
    ![DPM SharePoint Protection5](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sharepoint/dpm-sharepoint-protection6.png)
3. <span data-ttu-id="6d132-223">You can search SharePoint for *Recovering SharePoint item* by using a wildcard-based search within a recovery point range.</span><span class="sxs-lookup"><span data-stu-id="6d132-223">You can search SharePoint for *Recovering SharePoint item* by using a wildcard-based search within a recovery point range.</span></span>
   
    ![DPM SharePoint Protection6](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sharepoint/dpm-sharepoint-protection7.png)
4. <span data-ttu-id="6d132-225">Select the appropriate recovery point from the search results, right-click the item, and then select **Recover**.</span><span class="sxs-lookup"><span data-stu-id="6d132-225">Select the appropriate recovery point from the search results, right-click the item, and then select **Recover**.</span></span>
5. <span data-ttu-id="6d132-226">You can also browse through various recovery points and select a database or item to recover.</span><span class="sxs-lookup"><span data-stu-id="6d132-226">You can also browse through various recovery points and select a database or item to recover.</span></span> <span data-ttu-id="6d132-227">Select **Date > Recovery time**, and then select the correct **Database > SharePoint farm > Recovery point > Item**.</span><span class="sxs-lookup"><span data-stu-id="6d132-227">Select **Date > Recovery time**, and then select the correct **Database > SharePoint farm > Recovery point > Item**.</span></span>
   
    ![DPM SharePoint Protection7](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sharepoint/dpm-sharepoint-protection8.png)
6. <span data-ttu-id="6d132-229">Right-click the item, and then select **Recover** to open the **Recovery Wizard**.</span><span class="sxs-lookup"><span data-stu-id="6d132-229">Right-click the item, and then select **Recover** to open the **Recovery Wizard**.</span></span> <span data-ttu-id="6d132-230">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="6d132-230">Click **Next**.</span></span>
   
    ![Review Recovery Selection](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sharepoint/review-recovery-selection.png)
7. <span data-ttu-id="6d132-232">Select the type of recovery that you want to perform, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="6d132-232">Select the type of recovery that you want to perform, and then click **Next**.</span></span>
   
    ![Recovery Type](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sharepoint/select-recovery-type.png)
   
   > [!NOTE]
   > <span data-ttu-id="6d132-234">The selection of **Recover to original** in the example recovers the item to the original SharePoint site.</span><span class="sxs-lookup"><span data-stu-id="6d132-234">The selection of **Recover to original** in the example recovers the item to the original SharePoint site.</span></span>
   > 
   > 
8. <span data-ttu-id="6d132-235">Select the **Recovery Process** that you want to use.</span><span class="sxs-lookup"><span data-stu-id="6d132-235">Select the **Recovery Process** that you want to use.</span></span>
   
   * <span data-ttu-id="6d132-236">Select **Recover without using a recovery farm** if the SharePoint farm has not changed and is the same as the recovery point that is being restored.</span><span class="sxs-lookup"><span data-stu-id="6d132-236">Select **Recover without using a recovery farm** if the SharePoint farm has not changed and is the same as the recovery point that is being restored.</span></span>
   * <span data-ttu-id="6d132-237">Select **Recover using a recovery farm** if the SharePoint farm has changed since the recovery point was created.</span><span class="sxs-lookup"><span data-stu-id="6d132-237">Select **Recover using a recovery farm** if the SharePoint farm has changed since the recovery point was created.</span></span>
     
     ![Recovery Process](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sharepoint/recovery-process.png)
9. <span data-ttu-id="6d132-239">Provide a staging SQL Server instance location to recover the database temporarily, and provide a staging file share on the DPM server and the server that's running SharePoint to recover the item.</span><span class="sxs-lookup"><span data-stu-id="6d132-239">Provide a staging SQL Server instance location to recover the database temporarily, and provide a staging file share on the DPM server and the server that's running SharePoint to recover the item.</span></span>
   
    ![Staging Location1](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sharepoint/staging-location1.png)
   
    <span data-ttu-id="6d132-241">DPM attaches the content database that is hosting the SharePoint item to the temporary SQL Server instance.</span><span class="sxs-lookup"><span data-stu-id="6d132-241">DPM attaches the content database that is hosting the SharePoint item to the temporary SQL Server instance.</span></span> <span data-ttu-id="6d132-242">From the content database, the DPM server recovers the item and puts it on the staging file location on the DPM server.</span><span class="sxs-lookup"><span data-stu-id="6d132-242">From the content database, the DPM server recovers the item and puts it on the staging file location on the DPM server.</span></span> <span data-ttu-id="6d132-243">The recovered item that's on the staging location of the DPM server now needs to be exported to the staging location on the SharePoint farm.</span><span class="sxs-lookup"><span data-stu-id="6d132-243">The recovered item that's on the staging location of the DPM server now needs to be exported to the staging location on the SharePoint farm.</span></span>
   
    ![Staging Location2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sharepoint/staging-location2.png)
10. <span data-ttu-id="6d132-245">Select **Specify recovery options**, and apply security settings to the SharePoint farm or apply the security settings of the recovery point.</span><span class="sxs-lookup"><span data-stu-id="6d132-245">Select **Specify recovery options**, and apply security settings to the SharePoint farm or apply the security settings of the recovery point.</span></span> <span data-ttu-id="6d132-246">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="6d132-246">Click **Next**.</span></span>
    
    ![Recovery Options](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sharepoint/recovery-options.png)
    
    > [!NOTE]
    > <span data-ttu-id="6d132-248">You can choose to throttle the network bandwidth usage.</span><span class="sxs-lookup"><span data-stu-id="6d132-248">You can choose to throttle the network bandwidth usage.</span></span> <span data-ttu-id="6d132-249">This minimizes impact to the production server during production hours.</span><span class="sxs-lookup"><span data-stu-id="6d132-249">This minimizes impact to the production server during production hours.</span></span>
    > 
    > 
11. <span data-ttu-id="6d132-250">Review the summary information, and then click **Recover** to begin recovery of the file.</span><span class="sxs-lookup"><span data-stu-id="6d132-250">Review the summary information, and then click **Recover** to begin recovery of the file.</span></span>
    
    ![Recovery summary](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sharepoint/recovery-summary.png)
12. <span data-ttu-id="6d132-252">Now select the **Monitoring** tab in the **DPM Administrator Console** to view the **Status** of the recovery.</span><span class="sxs-lookup"><span data-stu-id="6d132-252">Now select the **Monitoring** tab in the **DPM Administrator Console** to view the **Status** of the recovery.</span></span>
    
    ![Recovery Status](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sharepoint/recovery-monitoring.png)
    
    > [!NOTE]
    > <span data-ttu-id="6d132-254">The file is now restored.</span><span class="sxs-lookup"><span data-stu-id="6d132-254">The file is now restored.</span></span> <span data-ttu-id="6d132-255">You can refresh the SharePoint site to check the restored file.</span><span class="sxs-lookup"><span data-stu-id="6d132-255">You can refresh the SharePoint site to check the restored file.</span></span>
    > 
    > 

## <a name="restore-a-sharepoint-database-from-azure-by-using-dpm"></a><span data-ttu-id="6d132-256">Restore a SharePoint database from Azure by using DPM</span><span class="sxs-lookup"><span data-stu-id="6d132-256">Restore a SharePoint database from Azure by using DPM</span></span>
1. <span data-ttu-id="6d132-257">To recover a SharePoint content database, browse through various recovery points (as shown previously), and select the recovery point that you want to restore.</span><span class="sxs-lookup"><span data-stu-id="6d132-257">To recover a SharePoint content database, browse through various recovery points (as shown previously), and select the recovery point that you want to restore.</span></span>
   
    ![DPM SharePoint Protection8](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sharepoint/dpm-sharepoint-protection9.png)
2. <span data-ttu-id="6d132-259">Double-click the SharePoint recovery point to show the available SharePoint catalog information.</span><span class="sxs-lookup"><span data-stu-id="6d132-259">Double-click the SharePoint recovery point to show the available SharePoint catalog information.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="6d132-260">Because the SharePoint farm is protected for long-term retention in Azure, no catalog information (metadata) is available on the DPM server.</span><span class="sxs-lookup"><span data-stu-id="6d132-260">Because the SharePoint farm is protected for long-term retention in Azure, no catalog information (metadata) is available on the DPM server.</span></span> <span data-ttu-id="6d132-261">As a result, whenever a point-in-time SharePoint content database needs to be recovered, you need to catalog the SharePoint farm again.</span><span class="sxs-lookup"><span data-stu-id="6d132-261">As a result, whenever a point-in-time SharePoint content database needs to be recovered, you need to catalog the SharePoint farm again.</span></span>
   > 
   > 
3. <span data-ttu-id="6d132-262">Click **Re-catalog**.</span><span class="sxs-lookup"><span data-stu-id="6d132-262">Click **Re-catalog**.</span></span>
   
    ![DPM SharePoint Protection10](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sharepoint/dpm-sharepoint-protection12.png)
   
    <span data-ttu-id="6d132-264">The **Cloud Recatalog** status window opens.</span><span class="sxs-lookup"><span data-stu-id="6d132-264">The **Cloud Recatalog** status window opens.</span></span>
   
    ![DPM SharePoint Protection11](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sharepoint/dpm-sharepoint-protection13.png)
   
    <span data-ttu-id="6d132-266">After cataloging is finished, the status changes to *Success*.</span><span class="sxs-lookup"><span data-stu-id="6d132-266">After cataloging is finished, the status changes to *Success*.</span></span> <span data-ttu-id="6d132-267">Click **Close**.</span><span class="sxs-lookup"><span data-stu-id="6d132-267">Click **Close**.</span></span>
   
    ![DPM SharePoint Protection12](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sharepoint/dpm-sharepoint-protection14.png)
4. <span data-ttu-id="6d132-269">Click the SharePoint object shown in the DPM **Recovery** tab to get the content database structure.</span><span class="sxs-lookup"><span data-stu-id="6d132-269">Click the SharePoint object shown in the DPM **Recovery** tab to get the content database structure.</span></span> <span data-ttu-id="6d132-270">Right-click the item, and then click **Recover**.</span><span class="sxs-lookup"><span data-stu-id="6d132-270">Right-click the item, and then click **Recover**.</span></span>
   
    ![DPM SharePoint Protection13](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sharepoint/dpm-sharepoint-protection15.png)
5. <span data-ttu-id="6d132-272">At this point, follow the [recovery steps earlier in this article](#restore-a-sharepoint-item-from-disk-using-dpm) to recover a SharePoint content database from disk.</span><span class="sxs-lookup"><span data-stu-id="6d132-272">At this point, follow the [recovery steps earlier in this article](#restore-a-sharepoint-item-from-disk-using-dpm) to recover a SharePoint content database from disk.</span></span>

## <a name="faqs"></a><span data-ttu-id="6d132-273">FAQs</span><span class="sxs-lookup"><span data-stu-id="6d132-273">FAQs</span></span>
<span data-ttu-id="6d132-274">Q: Which versions of DPM support SQL Server 2014 and SQL 2012 (SP2)?</span><span class="sxs-lookup"><span data-stu-id="6d132-274">Q: Which versions of DPM support SQL Server 2014 and SQL 2012 (SP2)?</span></span><br>
<span data-ttu-id="6d132-275">A: DPM 2012 R2 with Update Rollup 4 supports both.</span><span class="sxs-lookup"><span data-stu-id="6d132-275">A: DPM 2012 R2 with Update Rollup 4 supports both.</span></span>

<span data-ttu-id="6d132-276">Q: Can I recover a SharePoint item to the original location if SharePoint is configured by using SQL AlwaysOn (with protection on disk)?</span><span class="sxs-lookup"><span data-stu-id="6d132-276">Q: Can I recover a SharePoint item to the original location if SharePoint is configured by using SQL AlwaysOn (with protection on disk)?</span></span><br>
<span data-ttu-id="6d132-277">A: Yes, the item can be recovered to the original SharePoint site.</span><span class="sxs-lookup"><span data-stu-id="6d132-277">A: Yes, the item can be recovered to the original SharePoint site.</span></span>

<span data-ttu-id="6d132-278">Q: Can I recover a SharePoint database to the original location if SharePoint is configured by using SQL AlwaysOn?</span><span class="sxs-lookup"><span data-stu-id="6d132-278">Q: Can I recover a SharePoint database to the original location if SharePoint is configured by using SQL AlwaysOn?</span></span><br>
<span data-ttu-id="6d132-279">A: Because SharePoint databases are configured in SQL AlwaysOn, they cannot be modified unless the availability group is removed.</span><span class="sxs-lookup"><span data-stu-id="6d132-279">A: Because SharePoint databases are configured in SQL AlwaysOn, they cannot be modified unless the availability group is removed.</span></span> <span data-ttu-id="6d132-280">As a result, DPM cannot restore a database to the original location.</span><span class="sxs-lookup"><span data-stu-id="6d132-280">As a result, DPM cannot restore a database to the original location.</span></span> <span data-ttu-id="6d132-281">You can recover a SQL Server database to another SQL Server instance.</span><span class="sxs-lookup"><span data-stu-id="6d132-281">You can recover a SQL Server database to another SQL Server instance.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6d132-282">Next steps</span><span class="sxs-lookup"><span data-stu-id="6d132-282">Next steps</span></span>
* <span data-ttu-id="6d132-283">Learn more about DPM Protection of SharePoint - see [Video Series - DPM Protection of SharePoint](http://channel9.msdn.com/Series/Azure-Backup/Microsoft-SCDPM-Protection-of-SharePoint-1-of-2-How-to-create-a-SharePoint-Protection-Group)</span><span class="sxs-lookup"><span data-stu-id="6d132-283">Learn more about DPM Protection of SharePoint - see [Video Series - DPM Protection of SharePoint](http://channel9.msdn.com/Series/Azure-Backup/Microsoft-SCDPM-Protection-of-SharePoint-1-of-2-How-to-create-a-SharePoint-Protection-Group)</span></span>
* <span data-ttu-id="6d132-284">Review [Release Notes for System Center 2012 - Data Protection Manager](https://technet.microsoft.com/library/jj860415.aspx)</span><span class="sxs-lookup"><span data-stu-id="6d132-284">Review [Release Notes for System Center 2012 - Data Protection Manager](https://technet.microsoft.com/library/jj860415.aspx)</span></span>
* <span data-ttu-id="6d132-285">Review [Release Notes for Data Protection Manager in System Center 2012 SP1](https://technet.microsoft.com/library/jj860394.aspx)</span><span class="sxs-lookup"><span data-stu-id="6d132-285">Review [Release Notes for Data Protection Manager in System Center 2012 SP1](https://technet.microsoft.com/library/jj860394.aspx)</span></span>































