---
title: Back up a SharePoint farm on Azure Stack
description: Use Azure Backup Server to back up and restore your SharePoint data on Azure Stack. This article provides the information to configure your SharePoint farm so that desired data can be stored in Azure. You can restore protected SharePoint data from disk or from Azure.
services: backup
author: pvrk
manager: shivamg
ms.service: backup
ms.topic: conceptual
ms.date: 6/8/2018
ms.author: pullabhk
ms.openlocfilehash: 309e817426fff1eb877ab02ae9aa16ddc8f5cf16
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865157"
---
# <a name="back-up-a-sharepoint-farm-on-azure-stack"></a><span data-ttu-id="e4efb-105">Back up a SharePoint farm on Azure Stack</span><span class="sxs-lookup"><span data-stu-id="e4efb-105">Back up a SharePoint farm on Azure Stack</span></span>
<span data-ttu-id="e4efb-106">You back up a SharePoint farm on Azure Stack to Microsoft Azure by using Microsoft Azure Backup Server (MABS) in much the same way that you back up other data sources.</span><span class="sxs-lookup"><span data-stu-id="e4efb-106">You back up a SharePoint farm on Azure Stack to Microsoft Azure by using Microsoft Azure Backup Server (MABS) in much the same way that you back up other data sources.</span></span> <span data-ttu-id="e4efb-107">Azure Backup provides flexibility in the backup schedule to create daily, weekly, monthly, or yearly backup points and gives you retention policy options for various backup points.</span><span class="sxs-lookup"><span data-stu-id="e4efb-107">Azure Backup provides flexibility in the backup schedule to create daily, weekly, monthly, or yearly backup points and gives you retention policy options for various backup points.</span></span> <span data-ttu-id="e4efb-108">It also provides the capability to store local disk copies for quick recovery-time objectives (RTO) and to store copies to Azure for economical, long-term retention.</span><span class="sxs-lookup"><span data-stu-id="e4efb-108">It also provides the capability to store local disk copies for quick recovery-time objectives (RTO) and to store copies to Azure for economical, long-term retention.</span></span>

## <a name="sharepoint-supported-versions-and-related-protection-scenarios"></a><span data-ttu-id="e4efb-109">SharePoint supported versions and related protection scenarios</span><span class="sxs-lookup"><span data-stu-id="e4efb-109">SharePoint supported versions and related protection scenarios</span></span>
<span data-ttu-id="e4efb-110">Azure Backup for MABS supports the following scenarios:</span><span class="sxs-lookup"><span data-stu-id="e4efb-110">Azure Backup for MABS supports the following scenarios:</span></span>

| <span data-ttu-id="e4efb-111">Workload</span><span class="sxs-lookup"><span data-stu-id="e4efb-111">Workload</span></span> | <span data-ttu-id="e4efb-112">Version</span><span class="sxs-lookup"><span data-stu-id="e4efb-112">Version</span></span> | <span data-ttu-id="e4efb-113">SharePoint deployment</span><span class="sxs-lookup"><span data-stu-id="e4efb-113">SharePoint deployment</span></span> | <span data-ttu-id="e4efb-114">Protection and recovery</span><span class="sxs-lookup"><span data-stu-id="e4efb-114">Protection and recovery</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="e4efb-115">SharePoint</span><span class="sxs-lookup"><span data-stu-id="e4efb-115">SharePoint</span></span> |<span data-ttu-id="e4efb-116">SharePoint 2013, SharePoint 2010, SharePoint 2007, SharePoint 3.0</span><span class="sxs-lookup"><span data-stu-id="e4efb-116">SharePoint 2013, SharePoint 2010, SharePoint 2007, SharePoint 3.0</span></span> |<span data-ttu-id="e4efb-117">SharePoint deployed as a physical server or Hyper-V/VMware virtual machine</span><span class="sxs-lookup"><span data-stu-id="e4efb-117">SharePoint deployed as a physical server or Hyper-V/VMware virtual machine</span></span> <br> -------------- <br> <span data-ttu-id="e4efb-118">SQL AlwaysOn</span><span class="sxs-lookup"><span data-stu-id="e4efb-118">SQL AlwaysOn</span></span> | <span data-ttu-id="e4efb-119">Protect SharePoint Farm recovery options: Recovery farm, database, and file or list item from disk recovery points.</span><span class="sxs-lookup"><span data-stu-id="e4efb-119">Protect SharePoint Farm recovery options: Recovery farm, database, and file or list item from disk recovery points.</span></span>  <span data-ttu-id="e4efb-120">Farm and database recovery from Azure recovery points.</span><span class="sxs-lookup"><span data-stu-id="e4efb-120">Farm and database recovery from Azure recovery points.</span></span> |

## <a name="before-you-start"></a><span data-ttu-id="e4efb-121">Before you start</span><span class="sxs-lookup"><span data-stu-id="e4efb-121">Before you start</span></span>
<span data-ttu-id="e4efb-122">There are a few things you need to confirm before you back up a SharePoint farm to Azure.</span><span class="sxs-lookup"><span data-stu-id="e4efb-122">There are a few things you need to confirm before you back up a SharePoint farm to Azure.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="e4efb-123">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e4efb-123">Prerequisites</span></span>
<span data-ttu-id="e4efb-124">Before you proceed, make sure that you have [installed and prepared the Azure Backup Server](backup-mabs-install-azure-stack.md) to protect workloads.</span><span class="sxs-lookup"><span data-stu-id="e4efb-124">Before you proceed, make sure that you have [installed and prepared the Azure Backup Server](backup-mabs-install-azure-stack.md) to protect workloads.</span></span>

### <a name="protection-agent"></a><span data-ttu-id="e4efb-125">Protection agent</span><span class="sxs-lookup"><span data-stu-id="e4efb-125">Protection agent</span></span>
<span data-ttu-id="e4efb-126">The Azure Backup agent must be installed on the server that's running SharePoint, the servers that are running SQL Server, and all other servers that are part of the SharePoint farm.</span><span class="sxs-lookup"><span data-stu-id="e4efb-126">The Azure Backup agent must be installed on the server that's running SharePoint, the servers that are running SQL Server, and all other servers that are part of the SharePoint farm.</span></span> <span data-ttu-id="e4efb-127">For more information about how to set up the protection agent, see [Setup Protection Agent](https://technet.microsoft.com/library/hh758034\(v=sc.12\).aspx).</span><span class="sxs-lookup"><span data-stu-id="e4efb-127">For more information about how to set up the protection agent, see [Setup Protection Agent](https://technet.microsoft.com/library/hh758034\(v=sc.12\).aspx).</span></span>  <span data-ttu-id="e4efb-128">The one exception is that you install the agent only on a single web front end (WFE) server.</span><span class="sxs-lookup"><span data-stu-id="e4efb-128">The one exception is that you install the agent only on a single web front end (WFE) server.</span></span> <span data-ttu-id="e4efb-129">Azure Backup Server needs the agent on one WFE server only to serve as the entry point for protection.</span><span class="sxs-lookup"><span data-stu-id="e4efb-129">Azure Backup Server needs the agent on one WFE server only to serve as the entry point for protection.</span></span>

### <a name="sharepoint-farm"></a><span data-ttu-id="e4efb-130">SharePoint farm</span><span class="sxs-lookup"><span data-stu-id="e4efb-130">SharePoint farm</span></span>
<span data-ttu-id="e4efb-131">For every 10 million items in the farm, there must be at least 2 GB of space on the volume where the MABS folder is located.</span><span class="sxs-lookup"><span data-stu-id="e4efb-131">For every 10 million items in the farm, there must be at least 2 GB of space on the volume where the MABS folder is located.</span></span> <span data-ttu-id="e4efb-132">This space is required for catalog generation.</span><span class="sxs-lookup"><span data-stu-id="e4efb-132">This space is required for catalog generation.</span></span> <span data-ttu-id="e4efb-133">For MABS to recover specific items (site collections, sites, lists, document libraries, folders, individual documents, and list items), catalog generation creates a list of the URLs that are contained within each content database.</span><span class="sxs-lookup"><span data-stu-id="e4efb-133">For MABS to recover specific items (site collections, sites, lists, document libraries, folders, individual documents, and list items), catalog generation creates a list of the URLs that are contained within each content database.</span></span> <span data-ttu-id="e4efb-134">You can view the list of URLs in the recoverable item pane in the **Recovery** task area of MABS Administrator Console.</span><span class="sxs-lookup"><span data-stu-id="e4efb-134">You can view the list of URLs in the recoverable item pane in the **Recovery** task area of MABS Administrator Console.</span></span>

### <a name="sql-server"></a><span data-ttu-id="e4efb-135">SQL Server</span><span class="sxs-lookup"><span data-stu-id="e4efb-135">SQL Server</span></span>
<span data-ttu-id="e4efb-136">Azure Backup Server runs as a LocalSystem account.</span><span class="sxs-lookup"><span data-stu-id="e4efb-136">Azure Backup Server runs as a LocalSystem account.</span></span> <span data-ttu-id="e4efb-137">To back up SQL Server databases, MABS needs sysadmin privileges on that account for the server that's running SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e4efb-137">To back up SQL Server databases, MABS needs sysadmin privileges on that account for the server that's running SQL Server.</span></span> <span data-ttu-id="e4efb-138">Set NT AUTHORITY\SYSTEM to *sysadmin* on the server that's running SQL Server before you back it up.</span><span class="sxs-lookup"><span data-stu-id="e4efb-138">Set NT AUTHORITY\SYSTEM to *sysadmin* on the server that's running SQL Server before you back it up.</span></span>

<span data-ttu-id="e4efb-139">If the SharePoint farm has SQL Server databases that are configured with SQL Server aliases, install the SQL Server client components on the front-end Web server that MABS will protect.</span><span class="sxs-lookup"><span data-stu-id="e4efb-139">If the SharePoint farm has SQL Server databases that are configured with SQL Server aliases, install the SQL Server client components on the front-end Web server that MABS will protect.</span></span>

### <a name="whats-not-supported"></a><span data-ttu-id="e4efb-140">What's not supported</span><span class="sxs-lookup"><span data-stu-id="e4efb-140">What's not supported</span></span>
* <span data-ttu-id="e4efb-141">MABS that protects a SharePoint farm does not protect search indexes or application service databases.</span><span class="sxs-lookup"><span data-stu-id="e4efb-141">MABS that protects a SharePoint farm does not protect search indexes or application service databases.</span></span> <span data-ttu-id="e4efb-142">You will need to configure the protection of these databases separately.</span><span class="sxs-lookup"><span data-stu-id="e4efb-142">You will need to configure the protection of these databases separately.</span></span>
* <span data-ttu-id="e4efb-143">MABS does not provide backup of SharePoint SQL Server databases that are hosted on scale-out file server (SOFS) shares.</span><span class="sxs-lookup"><span data-stu-id="e4efb-143">MABS does not provide backup of SharePoint SQL Server databases that are hosted on scale-out file server (SOFS) shares.</span></span>

## <a name="configure-sharepoint-protection"></a><span data-ttu-id="e4efb-144">Configure SharePoint protection</span><span class="sxs-lookup"><span data-stu-id="e4efb-144">Configure SharePoint protection</span></span>
<span data-ttu-id="e4efb-145">Before you can use MABS to protect SharePoint, you must configure the SharePoint VSS Writer service (WSS Writer service) by using **ConfigureSharePoint.exe**.</span><span class="sxs-lookup"><span data-stu-id="e4efb-145">Before you can use MABS to protect SharePoint, you must configure the SharePoint VSS Writer service (WSS Writer service) by using **ConfigureSharePoint.exe**.</span></span>

<span data-ttu-id="e4efb-146">You can find **ConfigureSharePoint.exe** in the [MABS Installation Path]\bin folder on the front-end web server.</span><span class="sxs-lookup"><span data-stu-id="e4efb-146">You can find **ConfigureSharePoint.exe** in the [MABS Installation Path]\bin folder on the front-end web server.</span></span> <span data-ttu-id="e4efb-147">This tool provides the protection agent with the credentials for the SharePoint farm.</span><span class="sxs-lookup"><span data-stu-id="e4efb-147">This tool provides the protection agent with the credentials for the SharePoint farm.</span></span> <span data-ttu-id="e4efb-148">You run it on a single WFE server.</span><span class="sxs-lookup"><span data-stu-id="e4efb-148">You run it on a single WFE server.</span></span> <span data-ttu-id="e4efb-149">If you have multiple WFE servers, select just one when you configure a protection group.</span><span class="sxs-lookup"><span data-stu-id="e4efb-149">If you have multiple WFE servers, select just one when you configure a protection group.</span></span>

### <a name="to-configure-the-sharepoint-vss-writer-service"></a><span data-ttu-id="e4efb-150">To configure the SharePoint VSS Writer service</span><span class="sxs-lookup"><span data-stu-id="e4efb-150">To configure the SharePoint VSS Writer service</span></span>
1. <span data-ttu-id="e4efb-151">On the WFE server, at a command prompt, go to [MABS installation location]\bin\\</span><span class="sxs-lookup"><span data-stu-id="e4efb-151">On the WFE server, at a command prompt, go to [MABS installation location]\bin\\</span></span>
2. <span data-ttu-id="e4efb-152">Enter ConfigureSharePoint -EnableSharePointProtection.</span><span class="sxs-lookup"><span data-stu-id="e4efb-152">Enter ConfigureSharePoint -EnableSharePointProtection.</span></span>
3. <span data-ttu-id="e4efb-153">Enter the farm administrator credentials.</span><span class="sxs-lookup"><span data-stu-id="e4efb-153">Enter the farm administrator credentials.</span></span> <span data-ttu-id="e4efb-154">This account should be a member of the local Administrator group on the WFE server.</span><span class="sxs-lookup"><span data-stu-id="e4efb-154">This account should be a member of the local Administrator group on the WFE server.</span></span> <span data-ttu-id="e4efb-155">If the farm administrator isn’t a local admin grant the following permissions on the WFE server:</span><span class="sxs-lookup"><span data-stu-id="e4efb-155">If the farm administrator isn’t a local admin grant the following permissions on the WFE server:</span></span>
   * <span data-ttu-id="e4efb-156">Grant the WSS_Admin_WPG group full control to the DPM folder (%Program Files%\Microsoft Azure Backup\DPM).</span><span class="sxs-lookup"><span data-stu-id="e4efb-156">Grant the WSS_Admin_WPG group full control to the DPM folder (%Program Files%\Microsoft Azure Backup\DPM).</span></span>
   * <span data-ttu-id="e4efb-157">Grant the WSS_Admin_WPG group read access to the DPM Registry key (HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager).</span><span class="sxs-lookup"><span data-stu-id="e4efb-157">Grant the WSS_Admin_WPG group read access to the DPM Registry key (HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager).</span></span>

> [!NOTE]
> <span data-ttu-id="e4efb-158">You’ll need to rerun ConfigureSharePoint.exe whenever there’s a change in the SharePoint farm administrator credentials.</span><span class="sxs-lookup"><span data-stu-id="e4efb-158">You’ll need to rerun ConfigureSharePoint.exe whenever there’s a change in the SharePoint farm administrator credentials.</span></span>
>
>

## <a name="back-up-a-sharepoint-farm-by-using-mabs"></a><span data-ttu-id="e4efb-159">Back up a SharePoint farm by using MABS</span><span class="sxs-lookup"><span data-stu-id="e4efb-159">Back up a SharePoint farm by using MABS</span></span>
<span data-ttu-id="e4efb-160">After you have configured MABS and the SharePoint farm as explained previously, SharePoint can be protected by MABS.</span><span class="sxs-lookup"><span data-stu-id="e4efb-160">After you have configured MABS and the SharePoint farm as explained previously, SharePoint can be protected by MABS.</span></span>

### <a name="to-protect-a-sharepoint-farm"></a><span data-ttu-id="e4efb-161">To protect a SharePoint farm</span><span class="sxs-lookup"><span data-stu-id="e4efb-161">To protect a SharePoint farm</span></span>
1. <span data-ttu-id="e4efb-162">From the **Protection** tab of the MABS Administrator Console, click **New**.</span><span class="sxs-lookup"><span data-stu-id="e4efb-162">From the **Protection** tab of the MABS Administrator Console, click **New**.</span></span>
    <span data-ttu-id="e4efb-163">![New Protection Tab](./media/backup-azure-backup-sharepoint/dpm-new-protection-tab.png)</span><span class="sxs-lookup"><span data-stu-id="e4efb-163">![New Protection Tab](./media/backup-azure-backup-sharepoint/dpm-new-protection-tab.png)</span></span>
2. <span data-ttu-id="e4efb-164">On the **Select Protection Group Type** page of the **Create New Protection Group** wizard, select **Servers**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="e4efb-164">On the **Select Protection Group Type** page of the **Create New Protection Group** wizard, select **Servers**, and then click **Next**.</span></span>

    ![Select Protection Group type](./media/backup-azure-backup-sharepoint/select-protection-group-type.png)
3. <span data-ttu-id="e4efb-166">On the **Select Group Members** screen, select the check box for the SharePoint server you want to protect and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="e4efb-166">On the **Select Group Members** screen, select the check box for the SharePoint server you want to protect and click **Next**.</span></span>

    ![Select group members](./media/backup-azure-backup-sharepoint/select-group-members2.png)

   > [!NOTE]
   > <span data-ttu-id="e4efb-168">With the protection agent installed, you can see the server in the wizard.</span><span class="sxs-lookup"><span data-stu-id="e4efb-168">With the protection agent installed, you can see the server in the wizard.</span></span> <span data-ttu-id="e4efb-169">MABS also shows its structure.</span><span class="sxs-lookup"><span data-stu-id="e4efb-169">MABS also shows its structure.</span></span> <span data-ttu-id="e4efb-170">Because you ran ConfigureSharePoint.exe, MABS communicates with the SharePoint VSS Writer service and its corresponding SQL Server databases and recognizes the SharePoint farm structure, the associated content databases, and any corresponding items.</span><span class="sxs-lookup"><span data-stu-id="e4efb-170">Because you ran ConfigureSharePoint.exe, MABS communicates with the SharePoint VSS Writer service and its corresponding SQL Server databases and recognizes the SharePoint farm structure, the associated content databases, and any corresponding items.</span></span>
   >
   >
4. <span data-ttu-id="e4efb-171">On the **Select Data Protection Method** page, enter the name of the **Protection Group**, and select your preferred *protection methods*.</span><span class="sxs-lookup"><span data-stu-id="e4efb-171">On the **Select Data Protection Method** page, enter the name of the **Protection Group**, and select your preferred *protection methods*.</span></span> <span data-ttu-id="e4efb-172">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="e4efb-172">Click **Next**.</span></span>

    ![Select data protection method](./media/backup-azure-backup-sharepoint/select-data-protection-method1.png)

   > [!NOTE]
   > <span data-ttu-id="e4efb-174">The disk protection method helps to meet short recovery-time objectives.</span><span class="sxs-lookup"><span data-stu-id="e4efb-174">The disk protection method helps to meet short recovery-time objectives.</span></span>
   >
   >
5. <span data-ttu-id="e4efb-175">On the **Specify Short-Term Goals** page, select your preferred **Retention range** and identify when you want backups to occur.</span><span class="sxs-lookup"><span data-stu-id="e4efb-175">On the **Specify Short-Term Goals** page, select your preferred **Retention range** and identify when you want backups to occur.</span></span>

    ![Specify short-term goals](./media/backup-azure-backup-sharepoint/specify-short-term-goals2.png)

   > [!NOTE]
   > <span data-ttu-id="e4efb-177">Because recovery is most often required for data that's less than five days old, we selected a retention range of five days on disk and ensured that the backup happens during non-production hours, for this example.</span><span class="sxs-lookup"><span data-stu-id="e4efb-177">Because recovery is most often required for data that's less than five days old, we selected a retention range of five days on disk and ensured that the backup happens during non-production hours, for this example.</span></span>
   >
   >
6. <span data-ttu-id="e4efb-178">Review the storage pool disk space allocated for the protection group, and click then **Next**.</span><span class="sxs-lookup"><span data-stu-id="e4efb-178">Review the storage pool disk space allocated for the protection group, and click then **Next**.</span></span>
7. <span data-ttu-id="e4efb-179">For every protection group, MABS allocates disk space to store and manage replicas.</span><span class="sxs-lookup"><span data-stu-id="e4efb-179">For every protection group, MABS allocates disk space to store and manage replicas.</span></span> <span data-ttu-id="e4efb-180">At this point, MABS must create a copy of the selected data.</span><span class="sxs-lookup"><span data-stu-id="e4efb-180">At this point, MABS must create a copy of the selected data.</span></span> <span data-ttu-id="e4efb-181">Select how and when you want the replica created, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="e4efb-181">Select how and when you want the replica created, and then click **Next**.</span></span>

    ![Choose replica creation method](./media/backup-azure-backup-sharepoint/choose-replica-creation-method.png)

   > [!NOTE]
   > <span data-ttu-id="e4efb-183">To make sure that network traffic is not effected, select a time outside production hours.</span><span class="sxs-lookup"><span data-stu-id="e4efb-183">To make sure that network traffic is not effected, select a time outside production hours.</span></span>
   >
   >
8. <span data-ttu-id="e4efb-184">MABS ensures data integrity by performing consistency checks on the replica.</span><span class="sxs-lookup"><span data-stu-id="e4efb-184">MABS ensures data integrity by performing consistency checks on the replica.</span></span> <span data-ttu-id="e4efb-185">There are two available options.</span><span class="sxs-lookup"><span data-stu-id="e4efb-185">There are two available options.</span></span> <span data-ttu-id="e4efb-186">You can define a schedule to run consistency checks, or DPM can run consistency checks automatically on the replica whenever it becomes inconsistent.</span><span class="sxs-lookup"><span data-stu-id="e4efb-186">You can define a schedule to run consistency checks, or DPM can run consistency checks automatically on the replica whenever it becomes inconsistent.</span></span> <span data-ttu-id="e4efb-187">Select your preferred option, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="e4efb-187">Select your preferred option, and then click **Next**.</span></span>

    ![Consistency Check](./media/backup-azure-backup-sharepoint/consistency-check.png)
9. <span data-ttu-id="e4efb-189">On the **Specify Online Protection Data** page, select the SharePoint farm that you want to protect, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="e4efb-189">On the **Specify Online Protection Data** page, select the SharePoint farm that you want to protect, and then click **Next**.</span></span>

    ![DPM SharePoint Protection1](./media/backup-azure-backup-sharepoint/select-online-protection1.png)
10. <span data-ttu-id="e4efb-191">On the **Specify Online Backup Schedule** page, select your preferred schedule, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="e4efb-191">On the **Specify Online Backup Schedule** page, select your preferred schedule, and then click **Next**.</span></span>

    ![Online_backup_schedule](./media/backup-azure-backup-sharepoint/specify-online-backup-schedule.png)

    > [!NOTE]
    > <span data-ttu-id="e4efb-193">MABS provides a maximum of two daily backups to Azure from the then available latest disk backup point.</span><span class="sxs-lookup"><span data-stu-id="e4efb-193">MABS provides a maximum of two daily backups to Azure from the then available latest disk backup point.</span></span> <span data-ttu-id="e4efb-194">Azure Backup can also control the amount of WAN bandwidth that can be used for backups in peak and off-peak hours by using [Azure Backup Network Throttling](https://azure.microsoft.com/documentation/articles/backup-configure-vault/#enable-network-throttling).</span><span class="sxs-lookup"><span data-stu-id="e4efb-194">Azure Backup can also control the amount of WAN bandwidth that can be used for backups in peak and off-peak hours by using [Azure Backup Network Throttling](https://azure.microsoft.com/documentation/articles/backup-configure-vault/#enable-network-throttling).</span></span>
    >
    >
11. <span data-ttu-id="e4efb-195">Depending on the backup schedule that you selected, on the **Specify Online Retention Policy** page, select the retention policy for daily, weekly, monthly, and yearly backup points.</span><span class="sxs-lookup"><span data-stu-id="e4efb-195">Depending on the backup schedule that you selected, on the **Specify Online Retention Policy** page, select the retention policy for daily, weekly, monthly, and yearly backup points.</span></span>

    ![Online_retention_policy](./media/backup-azure-backup-sharepoint/specify-online-retention.png)

    > [!NOTE]
    > <span data-ttu-id="e4efb-197">MABS uses a grandfather-father-son retention scheme in which a different retention policy can be chosen for different backup points.</span><span class="sxs-lookup"><span data-stu-id="e4efb-197">MABS uses a grandfather-father-son retention scheme in which a different retention policy can be chosen for different backup points.</span></span>
    >
    >
12. <span data-ttu-id="e4efb-198">Similar to disk, an initial reference point replica needs to be created in Azure.</span><span class="sxs-lookup"><span data-stu-id="e4efb-198">Similar to disk, an initial reference point replica needs to be created in Azure.</span></span> <span data-ttu-id="e4efb-199">Select your preferred option to create an initial backup copy to Azure, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="e4efb-199">Select your preferred option to create an initial backup copy to Azure, and then click **Next**.</span></span>

    ![Online_replica](./media/backup-azure-backup-sharepoint/online-replication.png)
13. <span data-ttu-id="e4efb-201">Review your selected settings on the **Summary** page, and then click **Create Group**.</span><span class="sxs-lookup"><span data-stu-id="e4efb-201">Review your selected settings on the **Summary** page, and then click **Create Group**.</span></span> <span data-ttu-id="e4efb-202">You will see a success message after the protection group has been created.</span><span class="sxs-lookup"><span data-stu-id="e4efb-202">You will see a success message after the protection group has been created.</span></span>

    ![Summary](./media/backup-azure-backup-sharepoint/summary.png)

## <a name="restore-a-sharepoint-item-from-disk-by-using-mabs"></a><span data-ttu-id="e4efb-204">Restore a SharePoint item from disk by using MABS</span><span class="sxs-lookup"><span data-stu-id="e4efb-204">Restore a SharePoint item from disk by using MABS</span></span>
<span data-ttu-id="e4efb-205">In the following example, the *Recovering SharePoint item* has been accidentally deleted and needs to be recovered.</span><span class="sxs-lookup"><span data-stu-id="e4efb-205">In the following example, the *Recovering SharePoint item* has been accidentally deleted and needs to be recovered.</span></span>
<span data-ttu-id="e4efb-206">![MABS SharePoint Protection4](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection5.png)</span><span class="sxs-lookup"><span data-stu-id="e4efb-206">![MABS SharePoint Protection4](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection5.png)</span></span>

1. <span data-ttu-id="e4efb-207">Open the **DPM Administrator Console**.</span><span class="sxs-lookup"><span data-stu-id="e4efb-207">Open the **DPM Administrator Console**.</span></span> <span data-ttu-id="e4efb-208">All SharePoint farms that are protected by DPM are shown in the **Protection** tab.</span><span class="sxs-lookup"><span data-stu-id="e4efb-208">All SharePoint farms that are protected by DPM are shown in the **Protection** tab.</span></span>

    ![MABS SharePoint Protection3](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection4.png)
2. <span data-ttu-id="e4efb-210">To begin to recover the item, select the **Recovery** tab.</span><span class="sxs-lookup"><span data-stu-id="e4efb-210">To begin to recover the item, select the **Recovery** tab.</span></span>

    ![MABS SharePoint Protection5](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection6.png)
3. <span data-ttu-id="e4efb-212">You can search SharePoint for *Recovering SharePoint item* by using a wildcard-based search within a recovery point range.</span><span class="sxs-lookup"><span data-stu-id="e4efb-212">You can search SharePoint for *Recovering SharePoint item* by using a wildcard-based search within a recovery point range.</span></span>

    ![MABS SharePoint Protection6](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection7.png)
4. <span data-ttu-id="e4efb-214">Select the appropriate recovery point from the search results, right-click the item, and then select **Recover**.</span><span class="sxs-lookup"><span data-stu-id="e4efb-214">Select the appropriate recovery point from the search results, right-click the item, and then select **Recover**.</span></span>
5. <span data-ttu-id="e4efb-215">You can also browse through various recovery points and select a database or item to recover.</span><span class="sxs-lookup"><span data-stu-id="e4efb-215">You can also browse through various recovery points and select a database or item to recover.</span></span> <span data-ttu-id="e4efb-216">Select **Date > Recovery time**, and then select the correct **Database > SharePoint farm > Recovery point > Item**.</span><span class="sxs-lookup"><span data-stu-id="e4efb-216">Select **Date > Recovery time**, and then select the correct **Database > SharePoint farm > Recovery point > Item**.</span></span>

    ![MABS SharePoint Protection7](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection8.png)
6. <span data-ttu-id="e4efb-218">Right-click the item, and then select **Recover** to open the **Recovery Wizard**.</span><span class="sxs-lookup"><span data-stu-id="e4efb-218">Right-click the item, and then select **Recover** to open the **Recovery Wizard**.</span></span> <span data-ttu-id="e4efb-219">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="e4efb-219">Click **Next**.</span></span>

    ![Review Recovery Selection](./media/backup-azure-backup-sharepoint/review-recovery-selection.png)
7. <span data-ttu-id="e4efb-221">Select the type of recovery that you want to perform, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="e4efb-221">Select the type of recovery that you want to perform, and then click **Next**.</span></span>

    ![Recovery Type](./media/backup-azure-backup-sharepoint/select-recovery-type.png)

   > [!NOTE]
   > <span data-ttu-id="e4efb-223">The selection of **Recover to original** in the example recovers the item to the original SharePoint site.</span><span class="sxs-lookup"><span data-stu-id="e4efb-223">The selection of **Recover to original** in the example recovers the item to the original SharePoint site.</span></span>
   >
   >
8. <span data-ttu-id="e4efb-224">Select the **Recovery Process** that you want to use.</span><span class="sxs-lookup"><span data-stu-id="e4efb-224">Select the **Recovery Process** that you want to use.</span></span>

   * <span data-ttu-id="e4efb-225">Select **Recover without using a recovery farm** if the SharePoint farm has not changed and is the same as the recovery point that is being restored.</span><span class="sxs-lookup"><span data-stu-id="e4efb-225">Select **Recover without using a recovery farm** if the SharePoint farm has not changed and is the same as the recovery point that is being restored.</span></span>
   * <span data-ttu-id="e4efb-226">Select **Recover using a recovery farm** if the SharePoint farm has changed since the recovery point was created.</span><span class="sxs-lookup"><span data-stu-id="e4efb-226">Select **Recover using a recovery farm** if the SharePoint farm has changed since the recovery point was created.</span></span>

     ![Recovery Process](./media/backup-azure-backup-sharepoint/recovery-process.png)
9. <span data-ttu-id="e4efb-228">Provide a staging SQL Server instance location to recover the database temporarily, and provide a staging file share on MABS and the server that's running SharePoint to recover the item.</span><span class="sxs-lookup"><span data-stu-id="e4efb-228">Provide a staging SQL Server instance location to recover the database temporarily, and provide a staging file share on MABS and the server that's running SharePoint to recover the item.</span></span>

    ![Staging Location1](./media/backup-azure-backup-sharepoint/staging-location1.png)

    <span data-ttu-id="e4efb-230">MABS attaches the content database that is hosting the SharePoint item to the temporary SQL Server instance.</span><span class="sxs-lookup"><span data-stu-id="e4efb-230">MABS attaches the content database that is hosting the SharePoint item to the temporary SQL Server instance.</span></span> <span data-ttu-id="e4efb-231">From the content database, it recovers the item and puts it on the staging file location on MABS.</span><span class="sxs-lookup"><span data-stu-id="e4efb-231">From the content database, it recovers the item and puts it on the staging file location on MABS.</span></span> <span data-ttu-id="e4efb-232">The recovered item that's on the staging location now needs to be exported to the staging location on the SharePoint farm.</span><span class="sxs-lookup"><span data-stu-id="e4efb-232">The recovered item that's on the staging location now needs to be exported to the staging location on the SharePoint farm.</span></span>

    ![Staging Location2](./media/backup-azure-backup-sharepoint/staging-location2.png)
10. <span data-ttu-id="e4efb-234">Select **Specify recovery options**, and apply security settings to the SharePoint farm or apply the security settings of the recovery point.</span><span class="sxs-lookup"><span data-stu-id="e4efb-234">Select **Specify recovery options**, and apply security settings to the SharePoint farm or apply the security settings of the recovery point.</span></span> <span data-ttu-id="e4efb-235">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="e4efb-235">Click **Next**.</span></span>

    ![Recovery Options](./media/backup-azure-backup-sharepoint/recovery-options.png)

    > [!NOTE]
    > <span data-ttu-id="e4efb-237">You can choose to throttle the network bandwidth usage.</span><span class="sxs-lookup"><span data-stu-id="e4efb-237">You can choose to throttle the network bandwidth usage.</span></span> <span data-ttu-id="e4efb-238">This minimizes impact to the production server during production hours.</span><span class="sxs-lookup"><span data-stu-id="e4efb-238">This minimizes impact to the production server during production hours.</span></span>
    >
    >
11. <span data-ttu-id="e4efb-239">Review the summary information, and then click **Recover** to begin recovery of the file.</span><span class="sxs-lookup"><span data-stu-id="e4efb-239">Review the summary information, and then click **Recover** to begin recovery of the file.</span></span>

    ![Recovery summary](./media/backup-azure-backup-sharepoint/recovery-summary.png)
12. <span data-ttu-id="e4efb-241">Now select the **Monitoring** tab in the **MABS Administrator Console** to view the **Status** of the recovery.</span><span class="sxs-lookup"><span data-stu-id="e4efb-241">Now select the **Monitoring** tab in the **MABS Administrator Console** to view the **Status** of the recovery.</span></span>

    ![Recovery Status](./media/backup-azure-backup-sharepoint/recovery-monitoring.png)

    > [!NOTE]
    > <span data-ttu-id="e4efb-243">The file is now restored.</span><span class="sxs-lookup"><span data-stu-id="e4efb-243">The file is now restored.</span></span> <span data-ttu-id="e4efb-244">You can refresh the SharePoint site to check the restored file.</span><span class="sxs-lookup"><span data-stu-id="e4efb-244">You can refresh the SharePoint site to check the restored file.</span></span>
    >
    >

## <a name="restore-a-sharepoint-database-from-azure-by-using-dpm"></a><span data-ttu-id="e4efb-245">Restore a SharePoint database from Azure by using DPM</span><span class="sxs-lookup"><span data-stu-id="e4efb-245">Restore a SharePoint database from Azure by using DPM</span></span>
1. <span data-ttu-id="e4efb-246">To recover a SharePoint content database, browse through various recovery points (as shown previously), and select the recovery point that you want to restore.</span><span class="sxs-lookup"><span data-stu-id="e4efb-246">To recover a SharePoint content database, browse through various recovery points (as shown previously), and select the recovery point that you want to restore.</span></span>

    ![MABS SharePoint Protection8](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection9.png)
2. <span data-ttu-id="e4efb-248">Double-click the SharePoint recovery point to show the available SharePoint catalog information.</span><span class="sxs-lookup"><span data-stu-id="e4efb-248">Double-click the SharePoint recovery point to show the available SharePoint catalog information.</span></span>

   > [!NOTE]
   > <span data-ttu-id="e4efb-249">Because the SharePoint farm is protected for long-term retention in Azure, no catalog information (metadata) is available on MABS.</span><span class="sxs-lookup"><span data-stu-id="e4efb-249">Because the SharePoint farm is protected for long-term retention in Azure, no catalog information (metadata) is available on MABS.</span></span> <span data-ttu-id="e4efb-250">As a result, whenever a point-in-time SharePoint content database needs to be recovered, you need to catalog the SharePoint farm again.</span><span class="sxs-lookup"><span data-stu-id="e4efb-250">As a result, whenever a point-in-time SharePoint content database needs to be recovered, you need to catalog the SharePoint farm again.</span></span>
   >
   >
3. <span data-ttu-id="e4efb-251">Click **Re-catalog**.</span><span class="sxs-lookup"><span data-stu-id="e4efb-251">Click **Re-catalog**.</span></span>

    ![MABS SharePoint Protection10](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection12.png)

    <span data-ttu-id="e4efb-253">The **Cloud Recatalog** status window opens.</span><span class="sxs-lookup"><span data-stu-id="e4efb-253">The **Cloud Recatalog** status window opens.</span></span>

    ![MABS SharePoint Protection11](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection13.png)

    <span data-ttu-id="e4efb-255">After cataloging is finished, the status changes to *Success*.</span><span class="sxs-lookup"><span data-stu-id="e4efb-255">After cataloging is finished, the status changes to *Success*.</span></span> <span data-ttu-id="e4efb-256">Click **Close**.</span><span class="sxs-lookup"><span data-stu-id="e4efb-256">Click **Close**.</span></span>

    ![MABS SharePoint Protection12](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection14.png)
4. <span data-ttu-id="e4efb-258">Click the SharePoint object shown in the MABS **Recovery** tab to get the content database structure.</span><span class="sxs-lookup"><span data-stu-id="e4efb-258">Click the SharePoint object shown in the MABS **Recovery** tab to get the content database structure.</span></span> <span data-ttu-id="e4efb-259">Right-click the item, and then click **Recover**.</span><span class="sxs-lookup"><span data-stu-id="e4efb-259">Right-click the item, and then click **Recover**.</span></span>

    ![MABS SharePoint Protection13](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection15.png)
5. <span data-ttu-id="e4efb-261">At this point, follow the [recovery steps earlier in this article](#restore-a-sharepoint-item-from-disk-using-dpm) to recover a SharePoint content database from disk.</span><span class="sxs-lookup"><span data-stu-id="e4efb-261">At this point, follow the [recovery steps earlier in this article](#restore-a-sharepoint-item-from-disk-using-dpm) to recover a SharePoint content database from disk.</span></span>

## <a name="faqs"></a><span data-ttu-id="e4efb-262">FAQs</span><span class="sxs-lookup"><span data-stu-id="e4efb-262">FAQs</span></span>
<span data-ttu-id="e4efb-263">Q: Can I recover a SharePoint item to the original location if SharePoint is configured by using SQL AlwaysOn (with protection on disk)?</span><span class="sxs-lookup"><span data-stu-id="e4efb-263">Q: Can I recover a SharePoint item to the original location if SharePoint is configured by using SQL AlwaysOn (with protection on disk)?</span></span><br>
<span data-ttu-id="e4efb-264">A: Yes, the item can be recovered to the original SharePoint site.</span><span class="sxs-lookup"><span data-stu-id="e4efb-264">A: Yes, the item can be recovered to the original SharePoint site.</span></span>

<span data-ttu-id="e4efb-265">Q: Can I recover a SharePoint database to the original location if SharePoint is configured by using SQL AlwaysOn?</span><span class="sxs-lookup"><span data-stu-id="e4efb-265">Q: Can I recover a SharePoint database to the original location if SharePoint is configured by using SQL AlwaysOn?</span></span><br>
<span data-ttu-id="e4efb-266">A: Because SharePoint databases are configured in SQL AlwaysOn, they cannot be modified unless the availability group is removed.</span><span class="sxs-lookup"><span data-stu-id="e4efb-266">A: Because SharePoint databases are configured in SQL AlwaysOn, they cannot be modified unless the availability group is removed.</span></span> <span data-ttu-id="e4efb-267">As a result, MABS cannot restore a database to the original location.</span><span class="sxs-lookup"><span data-stu-id="e4efb-267">As a result, MABS cannot restore a database to the original location.</span></span> <span data-ttu-id="e4efb-268">You can recover a SQL Server database to another SQL Server instance.</span><span class="sxs-lookup"><span data-stu-id="e4efb-268">You can recover a SQL Server database to another SQL Server instance.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e4efb-269">Next Steps</span><span class="sxs-lookup"><span data-stu-id="e4efb-269">Next Steps</span></span>

<span data-ttu-id="e4efb-270">See the [Backup files and application](backup-mabs-files-applications-azure-stack.md) article.</span><span class="sxs-lookup"><span data-stu-id="e4efb-270">See the [Backup files and application](backup-mabs-files-applications-azure-stack.md) article.</span></span>
<span data-ttu-id="e4efb-271">See the [Backup SQL Server on Azure Stack](backup-mabs-sql-azure-stack.md) article.</span><span class="sxs-lookup"><span data-stu-id="e4efb-271">See the [Backup SQL Server on Azure Stack](backup-mabs-sql-azure-stack.md) article.</span></span>
