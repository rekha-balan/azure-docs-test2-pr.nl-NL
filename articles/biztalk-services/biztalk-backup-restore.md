---
title: Create and restore a backup in BizTalk Services | Microsoft Docs
description: BizTalk Services includes Backup and Restore. Learn how to create and restore a backup and determine what gets backed up. MABS, WABS
services: biztalk-services
documentationcenter: ''
author: MandiOhlinger
manager: anneta
editor: ''
ms.assetid: 59f91173-4683-48df-abd5-41262bfce6df
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: ccef9bb71b43cc0761c79bb85822e1f7a9f95bf6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550768"
---
# <a name="biztalk-services-backup-and-restore"></a><span data-ttu-id="7972e-105">BizTalk Services: Backup and Restore</span><span class="sxs-lookup"><span data-stu-id="7972e-105">BizTalk Services: Backup and Restore</span></span>
<span data-ttu-id="7972e-106">Azure BizTalk Services includes Backup and Restore capabilities.</span><span class="sxs-lookup"><span data-stu-id="7972e-106">Azure BizTalk Services includes Backup and Restore capabilities.</span></span> <span data-ttu-id="7972e-107">This topic describes how to backup and restore BizTalk Services using the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="7972e-107">This topic describes how to backup and restore BizTalk Services using the Azure classic portal.</span></span>

<span data-ttu-id="7972e-108">You can also back up BizTalk Services using the [BizTalk Services REST API](http://go.microsoft.com/fwlink/p/?LinkID=325584).</span><span class="sxs-lookup"><span data-stu-id="7972e-108">You can also back up BizTalk Services using the [BizTalk Services REST API](http://go.microsoft.com/fwlink/p/?LinkID=325584).</span></span> 

> [!NOTE]
> <span data-ttu-id="7972e-109">Hybrid Connections are NOT backed up, regardless of the Edition.</span><span class="sxs-lookup"><span data-stu-id="7972e-109">Hybrid Connections are NOT backed up, regardless of the Edition.</span></span> <span data-ttu-id="7972e-110">You must recreate your hybrid connections.</span><span class="sxs-lookup"><span data-stu-id="7972e-110">You must recreate your hybrid connections.</span></span>
> 
> 

## <a name="before-you-begin"></a><span data-ttu-id="7972e-111">Before you Begin</span><span class="sxs-lookup"><span data-stu-id="7972e-111">Before you Begin</span></span>
* <span data-ttu-id="7972e-112">Backup and Restore may not be available for all editions.</span><span class="sxs-lookup"><span data-stu-id="7972e-112">Backup and Restore may not be available for all editions.</span></span> <span data-ttu-id="7972e-113">See [BizTalk Services: Editions Chart](biztalk-editions-feature-chart.md).</span><span class="sxs-lookup"><span data-stu-id="7972e-113">See [BizTalk Services: Editions Chart](biztalk-editions-feature-chart.md).</span></span>
* <span data-ttu-id="7972e-114">Using the Azure classic portal, you can create an On Demand backup or create a scheduled backup.</span><span class="sxs-lookup"><span data-stu-id="7972e-114">Using the Azure classic portal, you can create an On Demand backup or create a scheduled backup.</span></span> 
* <span data-ttu-id="7972e-115">Backup content can be restored to the same BizTalk Service or to a new BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="7972e-115">Backup content can be restored to the same BizTalk Service or to a new BizTalk Service.</span></span> <span data-ttu-id="7972e-116">To restore the BizTalk Service using the same name, the existing BizTalk Service must be deleted and the name must be available.</span><span class="sxs-lookup"><span data-stu-id="7972e-116">To restore the BizTalk Service using the same name, the existing BizTalk Service must be deleted and the name must be available.</span></span> <span data-ttu-id="7972e-117">After you delete a BizTalk Service, it can take longer time than wanted for the same name to be available.</span><span class="sxs-lookup"><span data-stu-id="7972e-117">After you delete a BizTalk Service, it can take longer time than wanted for the same name to be available.</span></span> <span data-ttu-id="7972e-118">If you cannot wait for the same name to be available, then restore to a new BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="7972e-118">If you cannot wait for the same name to be available, then restore to a new BizTalk Service.</span></span>
* <span data-ttu-id="7972e-119">BizTalk Services can be restored to the same edition or a higher edition.</span><span class="sxs-lookup"><span data-stu-id="7972e-119">BizTalk Services can be restored to the same edition or a higher edition.</span></span> <span data-ttu-id="7972e-120">Restoring BizTalk Services to a lower edition, from when the backup was taken, is not supported.</span><span class="sxs-lookup"><span data-stu-id="7972e-120">Restoring BizTalk Services to a lower edition, from when the backup was taken, is not supported.</span></span>
  
    <span data-ttu-id="7972e-121">For example, a backup using the Basic Edition can be restored to the Premium Edition.</span><span class="sxs-lookup"><span data-stu-id="7972e-121">For example, a backup using the Basic Edition can be restored to the Premium Edition.</span></span> <span data-ttu-id="7972e-122">A backup using the Premium Edition cannot be restored to the Standard Edition.</span><span class="sxs-lookup"><span data-stu-id="7972e-122">A backup using the Premium Edition cannot be restored to the Standard Edition.</span></span>
* <span data-ttu-id="7972e-123">The EDI Control numbers are backed up to maintain continuity of the control numbers.</span><span class="sxs-lookup"><span data-stu-id="7972e-123">The EDI Control numbers are backed up to maintain continuity of the control numbers.</span></span> <span data-ttu-id="7972e-124">If messages are processed after the last backup, restoring this backup content can cause duplicate control numbers.</span><span class="sxs-lookup"><span data-stu-id="7972e-124">If messages are processed after the last backup, restoring this backup content can cause duplicate control numbers.</span></span>
* <span data-ttu-id="7972e-125">If a batch has active messages, process the batch **before** running a backup.</span><span class="sxs-lookup"><span data-stu-id="7972e-125">If a batch has active messages, process the batch **before** running a backup.</span></span> <span data-ttu-id="7972e-126">When creating a backup (as needed or scheduled), messages in batches are never stored.</span><span class="sxs-lookup"><span data-stu-id="7972e-126">When creating a backup (as needed or scheduled), messages in batches are never stored.</span></span> 
  
    <span data-ttu-id="7972e-127">**If a backup is taken with active messages in a batch, these messages are not backed up and are therefore lost.**</span><span class="sxs-lookup"><span data-stu-id="7972e-127">**If a backup is taken with active messages in a batch, these messages are not backed up and are therefore lost.**</span></span>
* <span data-ttu-id="7972e-128">Optional: In the BizTalk Services Portal, stop any management operations.</span><span class="sxs-lookup"><span data-stu-id="7972e-128">Optional: In the BizTalk Services Portal, stop any management operations.</span></span>

## <a name="create-a-backup"></a><span data-ttu-id="7972e-129">Create a backup</span><span class="sxs-lookup"><span data-stu-id="7972e-129">Create a backup</span></span>
<span data-ttu-id="7972e-130">A backup can be taken at any time and is completely controlled by you.</span><span class="sxs-lookup"><span data-stu-id="7972e-130">A backup can be taken at any time and is completely controlled by you.</span></span> <span data-ttu-id="7972e-131">This section lists the steps to create backups using the Azure classic portal, including:</span><span class="sxs-lookup"><span data-stu-id="7972e-131">This section lists the steps to create backups using the Azure classic portal, including:</span></span>

[<span data-ttu-id="7972e-132">On Demand backup</span><span class="sxs-lookup"><span data-stu-id="7972e-132">On Demand backup</span></span>](#backupnow)

[<span data-ttu-id="7972e-133">Schedule a backup</span><span class="sxs-lookup"><span data-stu-id="7972e-133">Schedule a backup</span></span>](#backupschedule)

#### <a name="backupnow"></a><span data-ttu-id="7972e-134">On Demand backup</span><span class="sxs-lookup"><span data-stu-id="7972e-134">On Demand backup</span></span>
1. <span data-ttu-id="7972e-135">In the Azure classic portal, select **BizTalk Services**, and then select the BizTalk Service you want to backup.</span><span class="sxs-lookup"><span data-stu-id="7972e-135">In the Azure classic portal, select **BizTalk Services**, and then select the BizTalk Service you want to backup.</span></span>
2. <span data-ttu-id="7972e-136">In the **Dashboard** tab, select **Back up** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="7972e-136">In the **Dashboard** tab, select **Back up** at the bottom of the page.</span></span>
3. <span data-ttu-id="7972e-137">Enter a backup name.</span><span class="sxs-lookup"><span data-stu-id="7972e-137">Enter a backup name.</span></span> <span data-ttu-id="7972e-138">For example, enter *myBizTalkService*BU*Date*.</span><span class="sxs-lookup"><span data-stu-id="7972e-138">For example, enter *myBizTalkService*BU*Date*.</span></span>
4. <span data-ttu-id="7972e-139">Choose a blob storage account and select the checkmark to start the backup.</span><span class="sxs-lookup"><span data-stu-id="7972e-139">Choose a blob storage account and select the checkmark to start the backup.</span></span>

<span data-ttu-id="7972e-140">Once the backup completes, a container with the backup name you enter is created in the storage account.</span><span class="sxs-lookup"><span data-stu-id="7972e-140">Once the backup completes, a container with the backup name you enter is created in the storage account.</span></span> <span data-ttu-id="7972e-141">This container contains your BizTalk Service backup configuration.</span><span class="sxs-lookup"><span data-stu-id="7972e-141">This container contains your BizTalk Service backup configuration.</span></span>

#### <a name="backupschedule"></a><span data-ttu-id="7972e-142">Schedule a backup</span><span class="sxs-lookup"><span data-stu-id="7972e-142">Schedule a backup</span></span>
1. <span data-ttu-id="7972e-143">In the Azure classic portal, select **BizTalk Services**, select the BizTalk Service name you want to schedule the backup, and then select the **Configure** tab.</span><span class="sxs-lookup"><span data-stu-id="7972e-143">In the Azure classic portal, select **BizTalk Services**, select the BizTalk Service name you want to schedule the backup, and then select the **Configure** tab.</span></span>
2. <span data-ttu-id="7972e-144">Set the **Backup Status** to **Automatic**.</span><span class="sxs-lookup"><span data-stu-id="7972e-144">Set the **Backup Status** to **Automatic**.</span></span> 
3. <span data-ttu-id="7972e-145">Select the **Storage Account** to store the backup, enter the **Frequency** to create the backups, and how long to keep the backups (**Retention Days**):</span><span class="sxs-lookup"><span data-stu-id="7972e-145">Select the **Storage Account** to store the backup, enter the **Frequency** to create the backups, and how long to keep the backups (**Retention Days**):</span></span>
   
    ![][AutomaticBU]
   
    <span data-ttu-id="7972e-146">**Notes**</span><span class="sxs-lookup"><span data-stu-id="7972e-146">**Notes**</span></span>     
   
   * <span data-ttu-id="7972e-147">In **Retention Days**, the retention period must be greater than the backup frequency.</span><span class="sxs-lookup"><span data-stu-id="7972e-147">In **Retention Days**, the retention period must be greater than the backup frequency.</span></span>
   * <span data-ttu-id="7972e-148">Select **Always keep at least one backup**, even if it is past the retention period.</span><span class="sxs-lookup"><span data-stu-id="7972e-148">Select **Always keep at least one backup**, even if it is past the retention period.</span></span>
4. <span data-ttu-id="7972e-149">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="7972e-149">Select **Save**.</span></span>

<span data-ttu-id="7972e-150">When a scheduled backup job runs, it creates a container (to store backup data) in the storage account you entered.</span><span class="sxs-lookup"><span data-stu-id="7972e-150">When a scheduled backup job runs, it creates a container (to store backup data) in the storage account you entered.</span></span> <span data-ttu-id="7972e-151">The name of the container is named *BizTalk Service Name-date-time*.</span><span class="sxs-lookup"><span data-stu-id="7972e-151">The name of the container is named *BizTalk Service Name-date-time*.</span></span> 

<span data-ttu-id="7972e-152">If the BizTalk Service dashboard shows a **Failed** status:</span><span class="sxs-lookup"><span data-stu-id="7972e-152">If the BizTalk Service dashboard shows a **Failed** status:</span></span>

![Last scheduled backup status][BackupStatus] 

<span data-ttu-id="7972e-154">The link opens the Management Services Operation Logs to help troubleshoot.</span><span class="sxs-lookup"><span data-stu-id="7972e-154">The link opens the Management Services Operation Logs to help troubleshoot.</span></span> <span data-ttu-id="7972e-155">See [BizTalk Services: Troubleshoot using operation logs](http://go.microsoft.com/fwlink/p/?LinkId=391211).</span><span class="sxs-lookup"><span data-stu-id="7972e-155">See [BizTalk Services: Troubleshoot using operation logs](http://go.microsoft.com/fwlink/p/?LinkId=391211).</span></span>

## <a name="restore"></a><span data-ttu-id="7972e-156">Restore</span><span class="sxs-lookup"><span data-stu-id="7972e-156">Restore</span></span>
<span data-ttu-id="7972e-157">You can restore backups from the Azure classic portal or from the [Restore BizTalk Service REST API](http://go.microsoft.com/fwlink/p/?LinkID=325582).</span><span class="sxs-lookup"><span data-stu-id="7972e-157">You can restore backups from the Azure classic portal or from the [Restore BizTalk Service REST API](http://go.microsoft.com/fwlink/p/?LinkID=325582).</span></span> <span data-ttu-id="7972e-158">This section lists the steps to restore using the classic portal.</span><span class="sxs-lookup"><span data-stu-id="7972e-158">This section lists the steps to restore using the classic portal.</span></span>

#### <a name="before-restoring-a-backup"></a><span data-ttu-id="7972e-159">Before restoring a backup</span><span class="sxs-lookup"><span data-stu-id="7972e-159">Before restoring a backup</span></span>
* <span data-ttu-id="7972e-160">New tracking, archiving, and monitoring stores can be entered while restoring a BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="7972e-160">New tracking, archiving, and monitoring stores can be entered while restoring a BizTalk Service.</span></span>
* <span data-ttu-id="7972e-161">The same EDI Runtime data is restored.</span><span class="sxs-lookup"><span data-stu-id="7972e-161">The same EDI Runtime data is restored.</span></span> <span data-ttu-id="7972e-162">The EDI Runtime backup stores the control numbers.</span><span class="sxs-lookup"><span data-stu-id="7972e-162">The EDI Runtime backup stores the control numbers.</span></span> <span data-ttu-id="7972e-163">The restored control numbers are in sequence from the time of the backup.</span><span class="sxs-lookup"><span data-stu-id="7972e-163">The restored control numbers are in sequence from the time of the backup.</span></span> <span data-ttu-id="7972e-164">If messages are processed after the last backup, restoring this backup content can cause duplicate control numbers.</span><span class="sxs-lookup"><span data-stu-id="7972e-164">If messages are processed after the last backup, restoring this backup content can cause duplicate control numbers.</span></span>

#### <a name="restore-a-backup"></a><span data-ttu-id="7972e-165">Restore a backup</span><span class="sxs-lookup"><span data-stu-id="7972e-165">Restore a backup</span></span>
1. <span data-ttu-id="7972e-166">In the Azure classic portal, select **New** > **App Services** > **BizTalk Service** > **Restore**:</span><span class="sxs-lookup"><span data-stu-id="7972e-166">In the Azure classic portal, select **New** > **App Services** > **BizTalk Service** > **Restore**:</span></span>
   
    ![Restore a backup][Restore]
2. <span data-ttu-id="7972e-168">In **Backup URL**, select the folder icon and expand the Azure storage account that stores the BizTalk Service configuration backup.</span><span class="sxs-lookup"><span data-stu-id="7972e-168">In **Backup URL**, select the folder icon and expand the Azure storage account that stores the BizTalk Service configuration backup.</span></span> <span data-ttu-id="7972e-169">Expand the container and in the right pane, select the corresponding back up .txt file.</span><span class="sxs-lookup"><span data-stu-id="7972e-169">Expand the container and in the right pane, select the corresponding back up .txt file.</span></span> 
   <br/><br/>
   <span data-ttu-id="7972e-170">Select **Open**.</span><span class="sxs-lookup"><span data-stu-id="7972e-170">Select **Open**.</span></span>
3. <span data-ttu-id="7972e-171">On the **Restore BizTalk Service** page, enter a **BizTalk Service Name** and verify the **Domain URL**, **Edition**, and **Region** for the restored BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="7972e-171">On the **Restore BizTalk Service** page, enter a **BizTalk Service Name** and verify the **Domain URL**, **Edition**, and **Region** for the restored BizTalk Service.</span></span> <span data-ttu-id="7972e-172">**Create a new SQL database instance** for the tracking database:</span><span class="sxs-lookup"><span data-stu-id="7972e-172">**Create a new SQL database instance** for the tracking database:</span></span>
   
    ![][RestoreBizTalkService]
   
    <span data-ttu-id="7972e-173">Select the next arrow.</span><span class="sxs-lookup"><span data-stu-id="7972e-173">Select the next arrow.</span></span>
4. <span data-ttu-id="7972e-174">Verify the name of the SQL database, enter the physical server where the SQL database will be created, and a username/password for that server.</span><span class="sxs-lookup"><span data-stu-id="7972e-174">Verify the name of the SQL database, enter the physical server where the SQL database will be created, and a username/password for that server.</span></span>

    <span data-ttu-id="7972e-175">If you want to configure the SQL database edition, size, and other properties, select  **Configure Advanced Database Settings**.</span><span class="sxs-lookup"><span data-stu-id="7972e-175">If you want to configure the SQL database edition, size, and other properties, select  **Configure Advanced Database Settings**.</span></span> 

    <span data-ttu-id="7972e-176">Select the next arrow.</span><span class="sxs-lookup"><span data-stu-id="7972e-176">Select the next arrow.</span></span>

1. <span data-ttu-id="7972e-177">Create a new storage account or enter an existing storage account for the BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="7972e-177">Create a new storage account or enter an existing storage account for the BizTalk Service.</span></span>
2. <span data-ttu-id="7972e-178">Select the checkmark to start the restore.</span><span class="sxs-lookup"><span data-stu-id="7972e-178">Select the checkmark to start the restore.</span></span>

<span data-ttu-id="7972e-179">Once the restoration successfully completes, a new BizTalk Service is listed in a suspended state on the BizTalk Services page in the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="7972e-179">Once the restoration successfully completes, a new BizTalk Service is listed in a suspended state on the BizTalk Services page in the Azure classic portal.</span></span>

### <a name="postrestore"></a><span data-ttu-id="7972e-180">After restoring a backup</span><span class="sxs-lookup"><span data-stu-id="7972e-180">After restoring a backup</span></span>
<span data-ttu-id="7972e-181">The BizTalk Service is always restored in a **Suspended** state.</span><span class="sxs-lookup"><span data-stu-id="7972e-181">The BizTalk Service is always restored in a **Suspended** state.</span></span> <span data-ttu-id="7972e-182">In this state, you can make any configuration changes before the new environment is functional, including:</span><span class="sxs-lookup"><span data-stu-id="7972e-182">In this state, you can make any configuration changes before the new environment is functional, including:</span></span>

* <span data-ttu-id="7972e-183">If you created BizTalk Service applications using the Azure BizTalk Services SDK, you may need to to update the Access Control (ACS) credentials in those applications to work with the restored environment.</span><span class="sxs-lookup"><span data-stu-id="7972e-183">If you created BizTalk Service applications using the Azure BizTalk Services SDK, you may need to to update the Access Control (ACS) credentials in those applications to work with the restored environment.</span></span>
* <span data-ttu-id="7972e-184">You restore a BizTalk Service to replicate an existing BizTalk Service environment.</span><span class="sxs-lookup"><span data-stu-id="7972e-184">You restore a BizTalk Service to replicate an existing BizTalk Service environment.</span></span> <span data-ttu-id="7972e-185">In this situation, if there are agreements configured in the original BizTalk Services portal that use a source FTP folder, you may need to update the agreements in the newly restored environment to use a different source FTP folder.</span><span class="sxs-lookup"><span data-stu-id="7972e-185">In this situation, if there are agreements configured in the original BizTalk Services portal that use a source FTP folder, you may need to update the agreements in the newly restored environment to use a different source FTP folder.</span></span> <span data-ttu-id="7972e-186">Otherwise, there may be two different agreements trying to pull the same message.</span><span class="sxs-lookup"><span data-stu-id="7972e-186">Otherwise, there may be two different agreements trying to pull the same message.</span></span>
* <span data-ttu-id="7972e-187">If you restored to have multiple BizTalk Service environments, make sure you target the correct environment in the Visual Studio applications, PowerShell cmdlets, REST APIs, or Trading Partner Management OM APIs.</span><span class="sxs-lookup"><span data-stu-id="7972e-187">If you restored to have multiple BizTalk Service environments, make sure you target the correct environment in the Visual Studio applications, PowerShell cmdlets, REST APIs, or Trading Partner Management OM APIs.</span></span>
* <span data-ttu-id="7972e-188">It's a good practice to configure automated backups on the newly restored BizTalk Service environment.</span><span class="sxs-lookup"><span data-stu-id="7972e-188">It's a good practice to configure automated backups on the newly restored BizTalk Service environment.</span></span>

<span data-ttu-id="7972e-189">To start the BizTalk Service in the Azure classic portal, select the restored BizTalk Service and select **Resume** in the task bar.</span><span class="sxs-lookup"><span data-stu-id="7972e-189">To start the BizTalk Service in the Azure classic portal, select the restored BizTalk Service and select **Resume** in the task bar.</span></span> 

## <a name="what-gets-backed-up"></a><span data-ttu-id="7972e-190">What gets backed up</span><span class="sxs-lookup"><span data-stu-id="7972e-190">What gets backed up</span></span>
<span data-ttu-id="7972e-191">When a backup is created, the following items are backed up:</span><span class="sxs-lookup"><span data-stu-id="7972e-191">When a backup is created, the following items are backed up:</span></span>

<table border="1"> 
<tr bgcolor="FAF9F9">
<th> </th>
<TH><span data-ttu-id="7972e-192">Items backed up</span><span class="sxs-lookup"><span data-stu-id="7972e-192">Items backed up</span></span></TH> 
</tr> 
<tr>
<td colspan="2"><span data-ttu-id="7972e-193">
 <strong>Azure BizTalk Services Portal</strong></span><span class="sxs-lookup"><span data-stu-id="7972e-193">
 <strong>Azure BizTalk Services Portal</strong></span></span></td>
</tr> 
<tr>
<td><span data-ttu-id="7972e-194">Configuration and Runtime</span><span class="sxs-lookup"><span data-stu-id="7972e-194">Configuration and Runtime</span></span></td> 
<td>
<ul>
<li><span data-ttu-id="7972e-195">Partner and profile details</span><span class="sxs-lookup"><span data-stu-id="7972e-195">Partner and profile details</span></span></li>
<li><span data-ttu-id="7972e-196">Partner Agreements</span><span class="sxs-lookup"><span data-stu-id="7972e-196">Partner Agreements</span></span></li>
<li><span data-ttu-id="7972e-197">Custom assemblies deployed</span><span class="sxs-lookup"><span data-stu-id="7972e-197">Custom assemblies deployed</span></span></li>
<li><span data-ttu-id="7972e-198">Bridges deployed</span><span class="sxs-lookup"><span data-stu-id="7972e-198">Bridges deployed</span></span></li>
<li><span data-ttu-id="7972e-199">Certificates</span><span class="sxs-lookup"><span data-stu-id="7972e-199">Certificates</span></span></li>
<li><span data-ttu-id="7972e-200">Transforms deployed</span><span class="sxs-lookup"><span data-stu-id="7972e-200">Transforms deployed</span></span></li>
<li><span data-ttu-id="7972e-201">Pipelines</span><span class="sxs-lookup"><span data-stu-id="7972e-201">Pipelines</span></span></li>
<li><span data-ttu-id="7972e-202">Templates created and saved in the BizTalk Services Portal</span><span class="sxs-lookup"><span data-stu-id="7972e-202">Templates created and saved in the BizTalk Services Portal</span></span></li>
<li><span data-ttu-id="7972e-203">X12 ST01 and GS01 mappings</span><span class="sxs-lookup"><span data-stu-id="7972e-203">X12 ST01 and GS01 mappings</span></span></li>
<li><span data-ttu-id="7972e-204">Control numbers (EDI)</span><span class="sxs-lookup"><span data-stu-id="7972e-204">Control numbers (EDI)</span></span></li>
<li><span data-ttu-id="7972e-205">AS2 Message MIC values</span><span class="sxs-lookup"><span data-stu-id="7972e-205">AS2 Message MIC values</span></span></li>
</ul>
</td>
</tr> 

<tr>
<td colspan="2"><span data-ttu-id="7972e-206">
 <strong>Azure BizTalk Service</strong></span><span class="sxs-lookup"><span data-stu-id="7972e-206">
 <strong>Azure BizTalk Service</strong></span></span></td>
</tr> 
<tr>
<td><span data-ttu-id="7972e-207">SSL Certificate</span><span class="sxs-lookup"><span data-stu-id="7972e-207">SSL Certificate</span></span></td> 
<td>
<ul>
<li><span data-ttu-id="7972e-208">SSL Certificate Data</span><span class="sxs-lookup"><span data-stu-id="7972e-208">SSL Certificate Data</span></span></li>
<li><span data-ttu-id="7972e-209">SSL Certificate Password</span><span class="sxs-lookup"><span data-stu-id="7972e-209">SSL Certificate Password</span></span></li>
</ul>
</td>
</tr> 
<tr>
<td><span data-ttu-id="7972e-210">BizTalk Service Settings</span><span class="sxs-lookup"><span data-stu-id="7972e-210">BizTalk Service Settings</span></span></td> 
<td>
<ul>
<li><span data-ttu-id="7972e-211">Scale unit count</span><span class="sxs-lookup"><span data-stu-id="7972e-211">Scale unit count</span></span></li>
<li><span data-ttu-id="7972e-212">Edition</span><span class="sxs-lookup"><span data-stu-id="7972e-212">Edition</span></span></li>
<li><span data-ttu-id="7972e-213">Product Version</span><span class="sxs-lookup"><span data-stu-id="7972e-213">Product Version</span></span></li>
<li><span data-ttu-id="7972e-214">Region/Datacenter</span><span class="sxs-lookup"><span data-stu-id="7972e-214">Region/Datacenter</span></span></li>
<li><span data-ttu-id="7972e-215">Access Control Service (ACS) namespace and key</span><span class="sxs-lookup"><span data-stu-id="7972e-215">Access Control Service (ACS) namespace and key</span></span></li>
<li><span data-ttu-id="7972e-216">Tracking database connection string</span><span class="sxs-lookup"><span data-stu-id="7972e-216">Tracking database connection string</span></span></li>
<li><span data-ttu-id="7972e-217">Archiving Storage account connection string</span><span class="sxs-lookup"><span data-stu-id="7972e-217">Archiving Storage account connection string</span></span></li>
<li><span data-ttu-id="7972e-218">Monitoring storage account connection string</span><span class="sxs-lookup"><span data-stu-id="7972e-218">Monitoring storage account connection string</span></span></li>
</ul>
</td>
</tr> 
<tr>
<td colspan="2"><span data-ttu-id="7972e-219">
 <strong>Additional Items</strong></span><span class="sxs-lookup"><span data-stu-id="7972e-219">
 <strong>Additional Items</strong></span></span></td>
</tr> 
<tr>
<td><span data-ttu-id="7972e-220">Tracking Database</span><span class="sxs-lookup"><span data-stu-id="7972e-220">Tracking Database</span></span></td> 
<td><span data-ttu-id="7972e-221">When the BizTalk Service is created, the Tracking Database details are entered, including the Azure SQL Database Server and the Tracking Database name.</span><span class="sxs-lookup"><span data-stu-id="7972e-221">When the BizTalk Service is created, the Tracking Database details are entered, including the Azure SQL Database Server and the Tracking Database name.</span></span> <span data-ttu-id="7972e-222">The Tracking Database is not automatically backed up.</span><span class="sxs-lookup"><span data-stu-id="7972e-222">The Tracking Database is not automatically backed up.</span></span>
<br/><br/><span data-ttu-id="7972e-223">
<strong>Important</strong></span><span class="sxs-lookup"><span data-stu-id="7972e-223">
<strong>Important</strong></span></span><br/>
<span data-ttu-id="7972e-224">If the Tracking Database is deleted and the database needs recovered, a previous backup must exist.</span><span class="sxs-lookup"><span data-stu-id="7972e-224">If the Tracking Database is deleted and the database needs recovered, a previous backup must exist.</span></span> <span data-ttu-id="7972e-225">If a backup does not exist, the Tracking Database and its data are not recoverable.</span><span class="sxs-lookup"><span data-stu-id="7972e-225">If a backup does not exist, the Tracking Database and its data are not recoverable.</span></span> <span data-ttu-id="7972e-226">In this situation, create a new Tracking Database with the same database name.</span><span class="sxs-lookup"><span data-stu-id="7972e-226">In this situation, create a new Tracking Database with the same database name.</span></span> <span data-ttu-id="7972e-227">Geo-Replication is recommended.</span><span class="sxs-lookup"><span data-stu-id="7972e-227">Geo-Replication is recommended.</span></span></td>
</tr> 
</table>

## <a name="next"></a><span data-ttu-id="7972e-228">Next</span><span class="sxs-lookup"><span data-stu-id="7972e-228">Next</span></span>
<span data-ttu-id="7972e-229">To create Azure BizTalk Services in the Azure classic portal, go to [BizTalk Services: Provisioning Using Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=302280).</span><span class="sxs-lookup"><span data-stu-id="7972e-229">To create Azure BizTalk Services in the Azure classic portal, go to [BizTalk Services: Provisioning Using Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=302280).</span></span> <span data-ttu-id="7972e-230">To start creating applications, go to [Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=235197).</span><span class="sxs-lookup"><span data-stu-id="7972e-230">To start creating applications, go to [Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=235197).</span></span>

## <a name="see-also"></a><span data-ttu-id="7972e-231">See Also</span><span class="sxs-lookup"><span data-stu-id="7972e-231">See Also</span></span>
* [<span data-ttu-id="7972e-232">Backup BizTalk Service</span><span class="sxs-lookup"><span data-stu-id="7972e-232">Backup BizTalk Service</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=325584)
* [<span data-ttu-id="7972e-233">Restore BizTalk Service from Backup</span><span class="sxs-lookup"><span data-stu-id="7972e-233">Restore BizTalk Service from Backup</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=325582)
* [<span data-ttu-id="7972e-234">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span><span class="sxs-lookup"><span data-stu-id="7972e-234">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302279)
* [<span data-ttu-id="7972e-235">BizTalk Services: Provisioning Using Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="7972e-235">BizTalk Services: Provisioning Using Azure classic portal</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302280)
* [<span data-ttu-id="7972e-236">BizTalk Services: Provisioning Status Chart</span><span class="sxs-lookup"><span data-stu-id="7972e-236">BizTalk Services: Provisioning Status Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329870)
* [<span data-ttu-id="7972e-237">BizTalk Services: Dashboard, Monitor and Scale tabs</span><span class="sxs-lookup"><span data-stu-id="7972e-237">BizTalk Services: Dashboard, Monitor and Scale tabs</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302281)
* [<span data-ttu-id="7972e-238">BizTalk Services: Throttling</span><span class="sxs-lookup"><span data-stu-id="7972e-238">BizTalk Services: Throttling</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302282)
* [<span data-ttu-id="7972e-239">BizTalk Services: Issuer Name and Issuer Key</span><span class="sxs-lookup"><span data-stu-id="7972e-239">BizTalk Services: Issuer Name and Issuer Key</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303941)
* [<span data-ttu-id="7972e-240">How do I Start Using the Azure BizTalk Services SDK</span><span class="sxs-lookup"><span data-stu-id="7972e-240">How do I Start Using the Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)

[BackupStatus]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/biztalk-services/media/biztalk-backup-restore/status-last-backup.png
[Restore]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/biztalk-services/media/biztalk-backup-restore/restore-ui.png
[AutomaticBU]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/biztalk-services/media/biztalk-backup-restore/AutomaticBU.png
[RestoreBizTalkService]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/biztalk-services/media/biztalk-backup-restore/RestoreBizTalkServiceWindow.png





