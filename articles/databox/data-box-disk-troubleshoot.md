---
title: Azure Data Box Disk troubleshooting | Microsoft Docs
description: Describes how to troubleshoot issues seen in Azure Data Box Disk.
services: databox
documentationcenter: NA
author: alkohli
manager: twooley
editor: ''
ms.assetid: ''
ms.service: databox
ms.devlang: NA
ms.topic: overview
ms.custom: mvc
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/03/2018
ms.author: alkohli
ms.openlocfilehash: e1a5cb33bb473daf5b9e45e7c64bcb297eca7733
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968895"
---
# <a name="troubleshoot-issues-in-azure-data-box-disk-preview"></a><span data-ttu-id="c7470-103">Troubleshoot issues in Azure Data Box Disk (Preview)</span><span class="sxs-lookup"><span data-stu-id="c7470-103">Troubleshoot issues in Azure Data Box Disk (Preview)</span></span>

<span data-ttu-id="c7470-104">This article applies to Microsoft Azure Data Box running Preview release.</span><span class="sxs-lookup"><span data-stu-id="c7470-104">This article applies to Microsoft Azure Data Box running Preview release.</span></span> <span data-ttu-id="c7470-105">This article describes some of the complex workflows and management tasks that can be performed on the Data Box and Data Box Disk.</span><span class="sxs-lookup"><span data-stu-id="c7470-105">This article describes some of the complex workflows and management tasks that can be performed on the Data Box and Data Box Disk.</span></span> 

<span data-ttu-id="c7470-106">You can manage the Data Box Disk via the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="c7470-106">You can manage the Data Box Disk via the Azure portal.</span></span> <span data-ttu-id="c7470-107">This article focuses on the tasks that you can perform using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="c7470-107">This article focuses on the tasks that you can perform using the Azure portal.</span></span> <span data-ttu-id="c7470-108">Use the Azure portal to manage orders, manage devices, and track the status of the order as it proceeds to completion.</span><span class="sxs-lookup"><span data-stu-id="c7470-108">Use the Azure portal to manage orders, manage devices, and track the status of the order as it proceeds to completion.</span></span>

<span data-ttu-id="c7470-109">This article includes the following tutorials:</span><span class="sxs-lookup"><span data-stu-id="c7470-109">This article includes the following tutorials:</span></span>

- <span data-ttu-id="c7470-110">Download diagnostic logs</span><span class="sxs-lookup"><span data-stu-id="c7470-110">Download diagnostic logs</span></span>
- <span data-ttu-id="c7470-111">Query activity logs</span><span class="sxs-lookup"><span data-stu-id="c7470-111">Query activity logs</span></span>


> [!IMPORTANT]
> <span data-ttu-id="c7470-112">Data Box is in preview.</span><span class="sxs-lookup"><span data-stu-id="c7470-112">Data Box is in preview.</span></span> <span data-ttu-id="c7470-113">Review the [Azure terms of service for preview](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) before you deploy this solution.</span><span class="sxs-lookup"><span data-stu-id="c7470-113">Review the [Azure terms of service for preview](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) before you deploy this solution.</span></span>

## <a name="download-diagnostic-logs"></a><span data-ttu-id="c7470-114">Download diagnostic logs</span><span class="sxs-lookup"><span data-stu-id="c7470-114">Download diagnostic logs</span></span>

<span data-ttu-id="c7470-115">If there are any errors during the data copy process, then the portal displays a path to the folder where the diagnostics logs are located.</span><span class="sxs-lookup"><span data-stu-id="c7470-115">If there are any errors during the data copy process, then the portal displays a path to the folder where the diagnostics logs are located.</span></span> 

<span data-ttu-id="c7470-116">The diagnostics logs can be:</span><span class="sxs-lookup"><span data-stu-id="c7470-116">The diagnostics logs can be:</span></span>
- <span data-ttu-id="c7470-117">Error logs</span><span class="sxs-lookup"><span data-stu-id="c7470-117">Error logs</span></span>
- <span data-ttu-id="c7470-118">Verbose logs</span><span class="sxs-lookup"><span data-stu-id="c7470-118">Verbose logs</span></span>  

<span data-ttu-id="c7470-119">To navigate to the path for copy log, go to the storage account associated with your Data Box order.</span><span class="sxs-lookup"><span data-stu-id="c7470-119">To navigate to the path for copy log, go to the storage account associated with your Data Box order.</span></span> 

1.  <span data-ttu-id="c7470-120">Go to **General > Order details** and make a note of the storage account associated with your order.</span><span class="sxs-lookup"><span data-stu-id="c7470-120">Go to **General > Order details** and make a note of the storage account associated with your order.</span></span>
 

2.  <span data-ttu-id="c7470-121">Go to **All resources** and search for the storage account identified in the previous step.</span><span class="sxs-lookup"><span data-stu-id="c7470-121">Go to **All resources** and search for the storage account identified in the previous step.</span></span> <span data-ttu-id="c7470-122">Select and click the storage account.</span><span class="sxs-lookup"><span data-stu-id="c7470-122">Select and click the storage account.</span></span>

    ![Copy logs 1](./media/data-box-disk-troubleshoot/data-box-disk-copy-logs1.png)

3.  <span data-ttu-id="c7470-124">Go to **Blob service > Browse blobs** and look for the blob corresponding to the storage account.</span><span class="sxs-lookup"><span data-stu-id="c7470-124">Go to **Blob service > Browse blobs** and look for the blob corresponding to the storage account.</span></span> <span data-ttu-id="c7470-125">Go to **diagnosticslogcontainer > waies**.</span><span class="sxs-lookup"><span data-stu-id="c7470-125">Go to **diagnosticslogcontainer > waies**.</span></span> 

    ![Copy logs 2](./media/data-box-disk-troubleshoot/data-box-disk-copy-logs2.png)

    <span data-ttu-id="c7470-127">You should see both the error logs and the verbose logs for data copy.</span><span class="sxs-lookup"><span data-stu-id="c7470-127">You should see both the error logs and the verbose logs for data copy.</span></span> <span data-ttu-id="c7470-128">Select and click each file and then download a local copy.</span><span class="sxs-lookup"><span data-stu-id="c7470-128">Select and click each file and then download a local copy.</span></span>

## <a name="query-activity-logs"></a><span data-ttu-id="c7470-129">Query Activity logs</span><span class="sxs-lookup"><span data-stu-id="c7470-129">Query Activity logs</span></span>

<span data-ttu-id="c7470-130">Use the activity logs to find an error when troubleshooting or to monitor how a user in your organization modified a resource.</span><span class="sxs-lookup"><span data-stu-id="c7470-130">Use the activity logs to find an error when troubleshooting or to monitor how a user in your organization modified a resource.</span></span> <span data-ttu-id="c7470-131">Through activity logs, you can determine:</span><span class="sxs-lookup"><span data-stu-id="c7470-131">Through activity logs, you can determine:</span></span>

- <span data-ttu-id="c7470-132">What operations were taken on the resources in your subscription.</span><span class="sxs-lookup"><span data-stu-id="c7470-132">What operations were taken on the resources in your subscription.</span></span>
- <span data-ttu-id="c7470-133">Who initiated the operation.</span><span class="sxs-lookup"><span data-stu-id="c7470-133">Who initiated the operation.</span></span> 
- <span data-ttu-id="c7470-134">When the operation occurred.</span><span class="sxs-lookup"><span data-stu-id="c7470-134">When the operation occurred.</span></span>
- <span data-ttu-id="c7470-135">The status of the operation.</span><span class="sxs-lookup"><span data-stu-id="c7470-135">The status of the operation.</span></span>
- <span data-ttu-id="c7470-136">The values of other properties that might help you research the operation.</span><span class="sxs-lookup"><span data-stu-id="c7470-136">The values of other properties that might help you research the operation.</span></span>

<span data-ttu-id="c7470-137">The activity log contains all write operations (such as PUT, POST, DELETE) performed on your resources but not the read operations (such as GET).</span><span class="sxs-lookup"><span data-stu-id="c7470-137">The activity log contains all write operations (such as PUT, POST, DELETE) performed on your resources but not the read operations (such as GET).</span></span> 

<span data-ttu-id="c7470-138">Activity logs are retained for 90 days.</span><span class="sxs-lookup"><span data-stu-id="c7470-138">Activity logs are retained for 90 days.</span></span> <span data-ttu-id="c7470-139">You can query for any range of dates, as long as the starting date is not more than 90 days in the past.</span><span class="sxs-lookup"><span data-stu-id="c7470-139">You can query for any range of dates, as long as the starting date is not more than 90 days in the past.</span></span> <span data-ttu-id="c7470-140">You can also filter by one of the built-in queries in Insights.</span><span class="sxs-lookup"><span data-stu-id="c7470-140">You can also filter by one of the built-in queries in Insights.</span></span> <span data-ttu-id="c7470-141">For instance, click error and then select and click specific failures to understand the root cause.</span><span class="sxs-lookup"><span data-stu-id="c7470-141">For instance, click error and then select and click specific failures to understand the root cause.</span></span>

## <a name="data-box-disk-unlock-tool-errors"></a><span data-ttu-id="c7470-142">Data Box Disk unlock tool errors</span><span class="sxs-lookup"><span data-stu-id="c7470-142">Data Box Disk unlock tool errors</span></span>


| <span data-ttu-id="c7470-143">Error message/Tool behavior</span><span class="sxs-lookup"><span data-stu-id="c7470-143">Error message/Tool behavior</span></span>      | <span data-ttu-id="c7470-144">Recommendations</span><span class="sxs-lookup"><span data-stu-id="c7470-144">Recommendations</span></span>                                                                                               |
|-------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="c7470-145">None</span><span class="sxs-lookup"><span data-stu-id="c7470-145">None</span></span><br><br><span data-ttu-id="c7470-146">Data Box Disk unlock tool crashes.</span><span class="sxs-lookup"><span data-stu-id="c7470-146">Data Box Disk unlock tool crashes.</span></span>                                                                            | <span data-ttu-id="c7470-147">Bitlocker not installed.</span><span class="sxs-lookup"><span data-stu-id="c7470-147">Bitlocker not installed.</span></span> <span data-ttu-id="c7470-148">Ensure that the host computer that is running the Data Box Disk unlock tool has BitLocker installed.</span><span class="sxs-lookup"><span data-stu-id="c7470-148">Ensure that the host computer that is running the Data Box Disk unlock tool has BitLocker installed.</span></span>                                                                            |
| <span data-ttu-id="c7470-149">The current .NET Framework is not supported.</span><span class="sxs-lookup"><span data-stu-id="c7470-149">The current .NET Framework is not supported.</span></span> <span data-ttu-id="c7470-150">The supported versions are 4.5 and later.</span><span class="sxs-lookup"><span data-stu-id="c7470-150">The supported versions are 4.5 and later.</span></span><br><br><span data-ttu-id="c7470-151">Tool exits with a message.</span><span class="sxs-lookup"><span data-stu-id="c7470-151">Tool exits with a message.</span></span>  | <span data-ttu-id="c7470-152">.NET 4.5 is not installed.</span><span class="sxs-lookup"><span data-stu-id="c7470-152">.NET 4.5 is not installed.</span></span> <span data-ttu-id="c7470-153">Install .NET 4.5 or later on the host computer that runs the Data Box Disk unlock tool.</span><span class="sxs-lookup"><span data-stu-id="c7470-153">Install .NET 4.5 or later on the host computer that runs the Data Box Disk unlock tool.</span></span>                                                                            |
| <span data-ttu-id="c7470-154">Could not unlock or verify any volumes.</span><span class="sxs-lookup"><span data-stu-id="c7470-154">Could not unlock or verify any volumes.</span></span> <span data-ttu-id="c7470-155">Contact Microsoft Support.</span><span class="sxs-lookup"><span data-stu-id="c7470-155">Contact Microsoft Support.</span></span>  <br><br><span data-ttu-id="c7470-156">The tool fails to unlock or verify any locked drive.</span><span class="sxs-lookup"><span data-stu-id="c7470-156">The tool fails to unlock or verify any locked drive.</span></span> | <span data-ttu-id="c7470-157">The tool could not unlock any of the locked drives with the supplied passkey.</span><span class="sxs-lookup"><span data-stu-id="c7470-157">The tool could not unlock any of the locked drives with the supplied passkey.</span></span> <span data-ttu-id="c7470-158">Contact Microsoft Support for next steps.</span><span class="sxs-lookup"><span data-stu-id="c7470-158">Contact Microsoft Support for next steps.</span></span>                                                |
| <span data-ttu-id="c7470-159">Following volumes are unlocked and verified.</span><span class="sxs-lookup"><span data-stu-id="c7470-159">Following volumes are unlocked and verified.</span></span> <br><span data-ttu-id="c7470-160">Volume drive letters: E:</span><span class="sxs-lookup"><span data-stu-id="c7470-160">Volume drive letters: E:</span></span><br><span data-ttu-id="c7470-161">Could not unlock any volumes with the following passkeys: werwerqomnf, qwerwerqwdfda</span><span class="sxs-lookup"><span data-stu-id="c7470-161">Could not unlock any volumes with the following passkeys: werwerqomnf, qwerwerqwdfda</span></span> <br><br><span data-ttu-id="c7470-162">The tool unlocks some drives and lists the successful and failed drive letters.</span><span class="sxs-lookup"><span data-stu-id="c7470-162">The tool unlocks some drives and lists the successful and failed drive letters.</span></span>| <span data-ttu-id="c7470-163">Partially succeeded.</span><span class="sxs-lookup"><span data-stu-id="c7470-163">Partially succeeded.</span></span> <span data-ttu-id="c7470-164">Could not unlock some of the drives with the supplied passkey.</span><span class="sxs-lookup"><span data-stu-id="c7470-164">Could not unlock some of the drives with the supplied passkey.</span></span> <span data-ttu-id="c7470-165">Contact Microsoft Support for next steps.</span><span class="sxs-lookup"><span data-stu-id="c7470-165">Contact Microsoft Support for next steps.</span></span> |
| <span data-ttu-id="c7470-166">Could not find locked volumes.</span><span class="sxs-lookup"><span data-stu-id="c7470-166">Could not find locked volumes.</span></span> <span data-ttu-id="c7470-167">Verify disk received from Microsoft is connected properly and is in locked state.</span><span class="sxs-lookup"><span data-stu-id="c7470-167">Verify disk received from Microsoft is connected properly and is in locked state.</span></span>          | <span data-ttu-id="c7470-168">The tool fails to find any locked drives.</span><span class="sxs-lookup"><span data-stu-id="c7470-168">The tool fails to find any locked drives.</span></span> <span data-ttu-id="c7470-169">Either the drives are already unlocked or not detected.</span><span class="sxs-lookup"><span data-stu-id="c7470-169">Either the drives are already unlocked or not detected.</span></span> <span data-ttu-id="c7470-170">Ensure that the drives are connected and are locked.</span><span class="sxs-lookup"><span data-stu-id="c7470-170">Ensure that the drives are connected and are locked.</span></span>                                                           |
| <span data-ttu-id="c7470-171">Fatal error: Invalid parameter</span><span class="sxs-lookup"><span data-stu-id="c7470-171">Fatal error: Invalid parameter</span></span><br><span data-ttu-id="c7470-172">Parameter name: invalid_arg</span><span class="sxs-lookup"><span data-stu-id="c7470-172">Parameter name: invalid_arg</span></span><br><span data-ttu-id="c7470-173">USAGE:</span><span class="sxs-lookup"><span data-stu-id="c7470-173">USAGE:</span></span><br><span data-ttu-id="c7470-174">DataBoxDiskUnlock /PassKeys:<passkey_list_separated_by_semicolon></span><span class="sxs-lookup"><span data-stu-id="c7470-174">DataBoxDiskUnlock /PassKeys:<passkey_list_separated_by_semicolon></span></span><br><br><span data-ttu-id="c7470-175">Example: DataBoxDiskUnlock /PassKeys:passkey1;passkey2;passkey3</span><span class="sxs-lookup"><span data-stu-id="c7470-175">Example: DataBoxDiskUnlock /PassKeys:passkey1;passkey2;passkey3</span></span><br><span data-ttu-id="c7470-176">Example: DataBoxDiskUnlock /SystemCheck</span><span class="sxs-lookup"><span data-stu-id="c7470-176">Example: DataBoxDiskUnlock /SystemCheck</span></span><br><span data-ttu-id="c7470-177">Example: DataBoxDiskUnlock /Help</span><span class="sxs-lookup"><span data-stu-id="c7470-177">Example: DataBoxDiskUnlock /Help</span></span><br><br><span data-ttu-id="c7470-178">/PassKeys:       Get this passkey from Azure DataBox Disk order.</span><span class="sxs-lookup"><span data-stu-id="c7470-178">/PassKeys:       Get this passkey from Azure DataBox Disk order.</span></span> <span data-ttu-id="c7470-179">The passkey unlocks your disks.</span><span class="sxs-lookup"><span data-stu-id="c7470-179">The passkey unlocks your disks.</span></span><br><span data-ttu-id="c7470-180">/Help:           This option provides help on cmdlet usage and examples.</span><span class="sxs-lookup"><span data-stu-id="c7470-180">/Help:           This option provides help on cmdlet usage and examples.</span></span><br><span data-ttu-id="c7470-181">/SystemCheck:    This option checks if your system meets the requirements to run the tool.</span><span class="sxs-lookup"><span data-stu-id="c7470-181">/SystemCheck:    This option checks if your system meets the requirements to run the tool.</span></span><br><br><span data-ttu-id="c7470-182">Press any key to exit.</span><span class="sxs-lookup"><span data-stu-id="c7470-182">Press any key to exit.</span></span> | <span data-ttu-id="c7470-183">Invalid parameter entered.</span><span class="sxs-lookup"><span data-stu-id="c7470-183">Invalid parameter entered.</span></span> <span data-ttu-id="c7470-184">The only allowed parameteres are /SystemCheck, /PassKey, and /Help.</span><span class="sxs-lookup"><span data-stu-id="c7470-184">The only allowed parameteres are /SystemCheck, /PassKey, and /Help.</span></span>                                                                            |
## <a name="next-steps"></a><span data-ttu-id="c7470-185">Next steps</span><span class="sxs-lookup"><span data-stu-id="c7470-185">Next steps</span></span>

- <span data-ttu-id="c7470-186">Learn how to [Manage Data Box Disk via Azure portal](data-box-portal-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="c7470-186">Learn how to [Manage Data Box Disk via Azure portal](data-box-portal-ui-admin.md).</span></span>