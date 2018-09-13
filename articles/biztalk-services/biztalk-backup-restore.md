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
ms.openlocfilehash: 90cf2d0ddbba47a856bf1299a101c5185873b5d8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44805407"
---
# <a name="biztalk-services-backup-and-restore"></a><span data-ttu-id="14cf4-105">BizTalk Services: Backup and Restore</span><span class="sxs-lookup"><span data-stu-id="14cf4-105">BizTalk Services: Backup and Restore</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="14cf4-106">Azure BizTalk Services includes Backup and Restore capabilities.</span><span class="sxs-lookup"><span data-stu-id="14cf4-106">Azure BizTalk Services includes Backup and Restore capabilities.</span></span> 

> [!INCLUDE [Use APIs to manage MABS](../../includes/biztalk-services-retirement-azure-classic-portal.md)]

> [!NOTE]
> <span data-ttu-id="14cf4-107">Hybrid Connections are NOT backed up, regardless of the Edition.</span><span class="sxs-lookup"><span data-stu-id="14cf4-107">Hybrid Connections are NOT backed up, regardless of the Edition.</span></span> <span data-ttu-id="14cf4-108">You must recreate your hybrid connections.</span><span class="sxs-lookup"><span data-stu-id="14cf4-108">You must recreate your hybrid connections.</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="14cf4-109">Before you Begin</span><span class="sxs-lookup"><span data-stu-id="14cf4-109">Before you Begin</span></span>
* <span data-ttu-id="14cf4-110">Backup and Restore may not be available for all editions.</span><span class="sxs-lookup"><span data-stu-id="14cf4-110">Backup and Restore may not be available for all editions.</span></span> <span data-ttu-id="14cf4-111">See [BizTalk Services: Editions Chart](biztalk-editions-feature-chart.md).</span><span class="sxs-lookup"><span data-stu-id="14cf4-111">See [BizTalk Services: Editions Chart](biztalk-editions-feature-chart.md).</span></span>
* <span data-ttu-id="14cf4-112">Backup content can be restored to the same BizTalk Service or to a new BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="14cf4-112">Backup content can be restored to the same BizTalk Service or to a new BizTalk Service.</span></span> <span data-ttu-id="14cf4-113">To restore the BizTalk Service using the same name, the existing BizTalk Service must be deleted and the name must be available.</span><span class="sxs-lookup"><span data-stu-id="14cf4-113">To restore the BizTalk Service using the same name, the existing BizTalk Service must be deleted and the name must be available.</span></span> <span data-ttu-id="14cf4-114">After you delete a BizTalk Service, it can take longer time than wanted for the same name to be available.</span><span class="sxs-lookup"><span data-stu-id="14cf4-114">After you delete a BizTalk Service, it can take longer time than wanted for the same name to be available.</span></span> <span data-ttu-id="14cf4-115">If you cannot wait for the same name to be available, then restore to a new BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="14cf4-115">If you cannot wait for the same name to be available, then restore to a new BizTalk Service.</span></span>
* <span data-ttu-id="14cf4-116">BizTalk Services can be restored to the same edition or a higher edition.</span><span class="sxs-lookup"><span data-stu-id="14cf4-116">BizTalk Services can be restored to the same edition or a higher edition.</span></span> <span data-ttu-id="14cf4-117">Restoring BizTalk Services to a lower edition, from when the backup was taken, is not supported.</span><span class="sxs-lookup"><span data-stu-id="14cf4-117">Restoring BizTalk Services to a lower edition, from when the backup was taken, is not supported.</span></span>
  
    <span data-ttu-id="14cf4-118">For example, a backup using the Basic Edition can be restored to the Premium Edition.</span><span class="sxs-lookup"><span data-stu-id="14cf4-118">For example, a backup using the Basic Edition can be restored to the Premium Edition.</span></span> <span data-ttu-id="14cf4-119">A backup using the Premium Edition cannot be restored to the Standard Edition.</span><span class="sxs-lookup"><span data-stu-id="14cf4-119">A backup using the Premium Edition cannot be restored to the Standard Edition.</span></span>
* <span data-ttu-id="14cf4-120">The EDI Control numbers are backed up to maintain continuity of the control numbers.</span><span class="sxs-lookup"><span data-stu-id="14cf4-120">The EDI Control numbers are backed up to maintain continuity of the control numbers.</span></span> <span data-ttu-id="14cf4-121">If messages are processed after the last backup, restoring this backup content can cause duplicate control numbers.</span><span class="sxs-lookup"><span data-stu-id="14cf4-121">If messages are processed after the last backup, restoring this backup content can cause duplicate control numbers.</span></span>
* <span data-ttu-id="14cf4-122">If a batch has active messages, process the batch **before** running a backup.</span><span class="sxs-lookup"><span data-stu-id="14cf4-122">If a batch has active messages, process the batch **before** running a backup.</span></span> <span data-ttu-id="14cf4-123">When creating a backup (as needed or scheduled), messages in batches are never stored.</span><span class="sxs-lookup"><span data-stu-id="14cf4-123">When creating a backup (as needed or scheduled), messages in batches are never stored.</span></span> 
  
    <span data-ttu-id="14cf4-124">**If a backup is taken with active messages in a batch, these messages are not backed up and are therefore lost.**</span><span class="sxs-lookup"><span data-stu-id="14cf4-124">**If a backup is taken with active messages in a batch, these messages are not backed up and are therefore lost.**</span></span>
* <span data-ttu-id="14cf4-125">Optional: In the BizTalk Services Portal, stop any management operations.</span><span class="sxs-lookup"><span data-stu-id="14cf4-125">Optional: In the BizTalk Services Portal, stop any management operations.</span></span>

## <a name="create-a-backup"></a><span data-ttu-id="14cf4-126">Create a backup</span><span class="sxs-lookup"><span data-stu-id="14cf4-126">Create a backup</span></span>
<span data-ttu-id="14cf4-127">A backup can be taken at any time and is completely controlled by you.</span><span class="sxs-lookup"><span data-stu-id="14cf4-127">A backup can be taken at any time and is completely controlled by you.</span></span> <span data-ttu-id="14cf4-128">To create a backup, use the [REST API for Managing BizTalk Services on Azure](https://msdn.microsoft.com/library/azure/dn232347.aspx).</span><span class="sxs-lookup"><span data-stu-id="14cf4-128">To create a backup, use the [REST API for Managing BizTalk Services on Azure](https://msdn.microsoft.com/library/azure/dn232347.aspx).</span></span>

## <a name="restore"></a><span data-ttu-id="14cf4-129">Restore</span><span class="sxs-lookup"><span data-stu-id="14cf4-129">Restore</span></span>
<span data-ttu-id="14cf4-130">To restore a backup, use the [REST API for Managing BizTalk Services on Azure](https://msdn.microsoft.com/library/azure/dn232347.aspx).</span><span class="sxs-lookup"><span data-stu-id="14cf4-130">To restore a backup, use the [REST API for Managing BizTalk Services on Azure](https://msdn.microsoft.com/library/azure/dn232347.aspx).</span></span>

### <a name="postrestore"></a><span data-ttu-id="14cf4-131">After restoring a backup</span><span class="sxs-lookup"><span data-stu-id="14cf4-131">After restoring a backup</span></span>
<span data-ttu-id="14cf4-132">The BizTalk Service is always restored in a **Suspended** state.</span><span class="sxs-lookup"><span data-stu-id="14cf4-132">The BizTalk Service is always restored in a **Suspended** state.</span></span> <span data-ttu-id="14cf4-133">In this state, you can make any configuration changes before the new environment is functional, including:</span><span class="sxs-lookup"><span data-stu-id="14cf4-133">In this state, you can make any configuration changes before the new environment is functional, including:</span></span>

* <span data-ttu-id="14cf4-134">If you created BizTalk Service applications using the Azure BizTalk Services SDK, you may need to update the Access Control (ACS) credentials in those applications to work with the restored environment.</span><span class="sxs-lookup"><span data-stu-id="14cf4-134">If you created BizTalk Service applications using the Azure BizTalk Services SDK, you may need to update the Access Control (ACS) credentials in those applications to work with the restored environment.</span></span>
* <span data-ttu-id="14cf4-135">You restore a BizTalk Service to replicate an existing BizTalk Service environment.</span><span class="sxs-lookup"><span data-stu-id="14cf4-135">You restore a BizTalk Service to replicate an existing BizTalk Service environment.</span></span> <span data-ttu-id="14cf4-136">In this situation, if there are agreements configured in the original BizTalk Services portal that use a source FTP folder, you may need to update the agreements in the newly restored environment to use a different source FTP folder.</span><span class="sxs-lookup"><span data-stu-id="14cf4-136">In this situation, if there are agreements configured in the original BizTalk Services portal that use a source FTP folder, you may need to update the agreements in the newly restored environment to use a different source FTP folder.</span></span> <span data-ttu-id="14cf4-137">Otherwise, there may be two different agreements trying to pull the same message.</span><span class="sxs-lookup"><span data-stu-id="14cf4-137">Otherwise, there may be two different agreements trying to pull the same message.</span></span>
* <span data-ttu-id="14cf4-138">If you restored to have multiple BizTalk Service environments, make sure you target the correct environment in the Visual Studio applications, PowerShell cmdlets, REST APIs, or Trading Partner Management OM APIs.</span><span class="sxs-lookup"><span data-stu-id="14cf4-138">If you restored to have multiple BizTalk Service environments, make sure you target the correct environment in the Visual Studio applications, PowerShell cmdlets, REST APIs, or Trading Partner Management OM APIs.</span></span>
* <span data-ttu-id="14cf4-139">It's a good practice to configure automated backups on the newly restored BizTalk Service environment.</span><span class="sxs-lookup"><span data-stu-id="14cf4-139">It's a good practice to configure automated backups on the newly restored BizTalk Service environment.</span></span>

## <a name="what-gets-backed-up"></a><span data-ttu-id="14cf4-140">What gets backed up</span><span class="sxs-lookup"><span data-stu-id="14cf4-140">What gets backed up</span></span>
<span data-ttu-id="14cf4-141">When a backup is created, the following items are backed up:</span><span class="sxs-lookup"><span data-stu-id="14cf4-141">When a backup is created, the following items are backed up:</span></span>

<table border="1"> 
<tr bgcolor="FAF9F9">
<th> </th>
<TH><span data-ttu-id="14cf4-142">Items backed up</span><span class="sxs-lookup"><span data-stu-id="14cf4-142">Items backed up</span></span></TH> 
</tr> 
<tr>
<td colspan="2"><span data-ttu-id="14cf4-143">
 <strong>Azure BizTalk Services Portal</strong></span><span class="sxs-lookup"><span data-stu-id="14cf4-143">
 <strong>Azure BizTalk Services Portal</strong></span></span></td>
</tr> 
<tr>
<td><span data-ttu-id="14cf4-144">Configuration and Runtime</span><span class="sxs-lookup"><span data-stu-id="14cf4-144">Configuration and Runtime</span></span></td> 
<td>
<ul>
<li><span data-ttu-id="14cf4-145">Partner and profile details</span><span class="sxs-lookup"><span data-stu-id="14cf4-145">Partner and profile details</span></span></li>
<li><span data-ttu-id="14cf4-146">Partner Agreements</span><span class="sxs-lookup"><span data-stu-id="14cf4-146">Partner Agreements</span></span></li>
<li><span data-ttu-id="14cf4-147">Custom assemblies deployed</span><span class="sxs-lookup"><span data-stu-id="14cf4-147">Custom assemblies deployed</span></span></li>
<li><span data-ttu-id="14cf4-148">Bridges deployed</span><span class="sxs-lookup"><span data-stu-id="14cf4-148">Bridges deployed</span></span></li>
<li><span data-ttu-id="14cf4-149">Certificates</span><span class="sxs-lookup"><span data-stu-id="14cf4-149">Certificates</span></span></li>
<li><span data-ttu-id="14cf4-150">Transforms deployed</span><span class="sxs-lookup"><span data-stu-id="14cf4-150">Transforms deployed</span></span></li>
<li><span data-ttu-id="14cf4-151">Pipelines</span><span class="sxs-lookup"><span data-stu-id="14cf4-151">Pipelines</span></span></li>
<li><span data-ttu-id="14cf4-152">Templates created and saved in the BizTalk Services Portal</span><span class="sxs-lookup"><span data-stu-id="14cf4-152">Templates created and saved in the BizTalk Services Portal</span></span></li>
<li><span data-ttu-id="14cf4-153">X12 ST01 and GS01 mappings</span><span class="sxs-lookup"><span data-stu-id="14cf4-153">X12 ST01 and GS01 mappings</span></span></li>
<li><span data-ttu-id="14cf4-154">Control numbers (EDI)</span><span class="sxs-lookup"><span data-stu-id="14cf4-154">Control numbers (EDI)</span></span></li>
<li><span data-ttu-id="14cf4-155">AS2 Message MIC values</span><span class="sxs-lookup"><span data-stu-id="14cf4-155">AS2 Message MIC values</span></span></li>
</ul>
</td>
</tr> 

<tr>
<td colspan="2"><span data-ttu-id="14cf4-156">
 <strong>Azure BizTalk Service</strong></span><span class="sxs-lookup"><span data-stu-id="14cf4-156">
 <strong>Azure BizTalk Service</strong></span></span></td>
</tr> 
<tr>
<td><span data-ttu-id="14cf4-157">SSL Certificate</span><span class="sxs-lookup"><span data-stu-id="14cf4-157">SSL Certificate</span></span></td> 
<td>
<ul>
<li><span data-ttu-id="14cf4-158">SSL Certificate Data</span><span class="sxs-lookup"><span data-stu-id="14cf4-158">SSL Certificate Data</span></span></li>
<li><span data-ttu-id="14cf4-159">SSL Certificate Password</span><span class="sxs-lookup"><span data-stu-id="14cf4-159">SSL Certificate Password</span></span></li>
</ul>
</td>
</tr> 
<tr>
<td><span data-ttu-id="14cf4-160">BizTalk Service Settings</span><span class="sxs-lookup"><span data-stu-id="14cf4-160">BizTalk Service Settings</span></span></td> 
<td>
<ul>
<li><span data-ttu-id="14cf4-161">Scale unit count</span><span class="sxs-lookup"><span data-stu-id="14cf4-161">Scale unit count</span></span></li>
<li><span data-ttu-id="14cf4-162">Edition</span><span class="sxs-lookup"><span data-stu-id="14cf4-162">Edition</span></span></li>
<li><span data-ttu-id="14cf4-163">Product Version</span><span class="sxs-lookup"><span data-stu-id="14cf4-163">Product Version</span></span></li>
<li><span data-ttu-id="14cf4-164">Region/Datacenter</span><span class="sxs-lookup"><span data-stu-id="14cf4-164">Region/Datacenter</span></span></li>
<li><span data-ttu-id="14cf4-165">Access Control Service (ACS) namespace and key</span><span class="sxs-lookup"><span data-stu-id="14cf4-165">Access Control Service (ACS) namespace and key</span></span></li>
<li><span data-ttu-id="14cf4-166">Tracking database connection string</span><span class="sxs-lookup"><span data-stu-id="14cf4-166">Tracking database connection string</span></span></li>
<li><span data-ttu-id="14cf4-167">Archiving Storage account connection string</span><span class="sxs-lookup"><span data-stu-id="14cf4-167">Archiving Storage account connection string</span></span></li>
<li><span data-ttu-id="14cf4-168">Monitoring storage account connection string</span><span class="sxs-lookup"><span data-stu-id="14cf4-168">Monitoring storage account connection string</span></span></li>
</ul>
</td>
</tr> 
<tr>
<td colspan="2"><span data-ttu-id="14cf4-169">
 <strong>Additional Items</strong></span><span class="sxs-lookup"><span data-stu-id="14cf4-169">
 <strong>Additional Items</strong></span></span></td>
</tr> 
<tr>
<td><span data-ttu-id="14cf4-170">Tracking Database</span><span class="sxs-lookup"><span data-stu-id="14cf4-170">Tracking Database</span></span></td> 
<td><span data-ttu-id="14cf4-171">When the BizTalk Service is created, the Tracking Database details are entered, including the Azure SQL Database Server and the Tracking Database name.</span><span class="sxs-lookup"><span data-stu-id="14cf4-171">When the BizTalk Service is created, the Tracking Database details are entered, including the Azure SQL Database Server and the Tracking Database name.</span></span> <span data-ttu-id="14cf4-172">The Tracking Database is not automatically backed up.</span><span class="sxs-lookup"><span data-stu-id="14cf4-172">The Tracking Database is not automatically backed up.</span></span>
<br/><br/><span data-ttu-id="14cf4-173">
<strong>Important</strong></span><span class="sxs-lookup"><span data-stu-id="14cf4-173">
<strong>Important</strong></span></span><br/>
<span data-ttu-id="14cf4-174">If the Tracking Database is deleted and the database needs recovered, a previous backup must exist.</span><span class="sxs-lookup"><span data-stu-id="14cf4-174">If the Tracking Database is deleted and the database needs recovered, a previous backup must exist.</span></span> <span data-ttu-id="14cf4-175">If a backup does not exist, the Tracking Database and its data are not recoverable.</span><span class="sxs-lookup"><span data-stu-id="14cf4-175">If a backup does not exist, the Tracking Database and its data are not recoverable.</span></span> <span data-ttu-id="14cf4-176">In this situation, create a new Tracking Database with the same database name.</span><span class="sxs-lookup"><span data-stu-id="14cf4-176">In this situation, create a new Tracking Database with the same database name.</span></span> <span data-ttu-id="14cf4-177">Geo-Replication is recommended.</span><span class="sxs-lookup"><span data-stu-id="14cf4-177">Geo-Replication is recommended.</span></span></td>
</tr> 
</table>

## <a name="next"></a><span data-ttu-id="14cf4-178">Next</span><span class="sxs-lookup"><span data-stu-id="14cf4-178">Next</span></span>
<span data-ttu-id="14cf4-179">To create Azure BizTalk Services, go to [BizTalk Services: Provisioning](http://go.microsoft.com/fwlink/p/?LinkID=302280).</span><span class="sxs-lookup"><span data-stu-id="14cf4-179">To create Azure BizTalk Services, go to [BizTalk Services: Provisioning](http://go.microsoft.com/fwlink/p/?LinkID=302280).</span></span> <span data-ttu-id="14cf4-180">To start creating applications, go to [Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=235197).</span><span class="sxs-lookup"><span data-stu-id="14cf4-180">To start creating applications, go to [Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=235197).</span></span>

## <a name="see-also"></a><span data-ttu-id="14cf4-181">See Also</span><span class="sxs-lookup"><span data-stu-id="14cf4-181">See Also</span></span>
* [<span data-ttu-id="14cf4-182">Backup BizTalk Service</span><span class="sxs-lookup"><span data-stu-id="14cf4-182">Backup BizTalk Service</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=325584)
* [<span data-ttu-id="14cf4-183">Restore BizTalk Service from Backup</span><span class="sxs-lookup"><span data-stu-id="14cf4-183">Restore BizTalk Service from Backup</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=325582)
* [<span data-ttu-id="14cf4-184">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span><span class="sxs-lookup"><span data-stu-id="14cf4-184">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302279)
* [<span data-ttu-id="14cf4-185">BizTalk Services: Provisioning</span><span class="sxs-lookup"><span data-stu-id="14cf4-185">BizTalk Services: Provisioning</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302280)
* [<span data-ttu-id="14cf4-186">BizTalk Services: Provisioning Status Chart</span><span class="sxs-lookup"><span data-stu-id="14cf4-186">BizTalk Services: Provisioning Status Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329870)
* [<span data-ttu-id="14cf4-187">BizTalk Services: Dashboard, Monitor and Scale tabs</span><span class="sxs-lookup"><span data-stu-id="14cf4-187">BizTalk Services: Dashboard, Monitor and Scale tabs</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302281)
* [<span data-ttu-id="14cf4-188">BizTalk Services: Throttling</span><span class="sxs-lookup"><span data-stu-id="14cf4-188">BizTalk Services: Throttling</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302282)
* [<span data-ttu-id="14cf4-189">BizTalk Services: Issuer Name and Issuer Key</span><span class="sxs-lookup"><span data-stu-id="14cf4-189">BizTalk Services: Issuer Name and Issuer Key</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303941)
* [<span data-ttu-id="14cf4-190">How do I Start Using the Azure BizTalk Services SDK</span><span class="sxs-lookup"><span data-stu-id="14cf4-190">How do I Start Using the Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)

[BackupStatus]: ./media/biztalk-backup-restore/status-last-backup.png
[Restore]: ./media/biztalk-backup-restore/restore-ui.png
[AutomaticBU]: ./media/biztalk-backup-restore/AutomaticBU.png
[RestoreBizTalkService]: ./media/biztalk-backup-restore/RestoreBizTalkServiceWindow.png

