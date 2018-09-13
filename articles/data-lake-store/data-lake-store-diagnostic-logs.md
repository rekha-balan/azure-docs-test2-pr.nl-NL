---
title: Viewing diagnostic logs for Azure Data Lake Store | Microsoft Docs
description: 'Understand how to setup and access diagnostic logs for Azure Data Lake Store '
services: data-lake-store
documentationcenter: ''
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: f6e75eb1-d0ae-47cf-bdb8-06684b7c0a94
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 02/06/2017
ms.author: nitinme
ms.openlocfilehash: 23bf7c7a2a62cb1b3847c6c04c4d051236132eaa
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556638"
---
# <a name="accessing-diagnostic-logs-for-azure-data-lake-store"></a><span data-ttu-id="4cdf3-103">Accessing diagnostic logs for Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="4cdf3-103">Accessing diagnostic logs for Azure Data Lake Store</span></span>
<span data-ttu-id="4cdf3-104">Learn about how to enable diagnostic logging for your Data Lake Store account and how to view the logs collected for your account.</span><span class="sxs-lookup"><span data-stu-id="4cdf3-104">Learn about how to enable diagnostic logging for your Data Lake Store account and how to view the logs collected for your account.</span></span>

<span data-ttu-id="4cdf3-105">Organizations can enable diagnostic logging for their Azure Data Lake Store account to collect data access audit trails that provides information such as list of users accessing the data, how frequently the data is accessed, how much data is stored in the account, etc.</span><span class="sxs-lookup"><span data-stu-id="4cdf3-105">Organizations can enable diagnostic logging for their Azure Data Lake Store account to collect data access audit trails that provides information such as list of users accessing the data, how frequently the data is accessed, how much data is stored in the account, etc.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4cdf3-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="4cdf3-106">Prerequisites</span></span>
* <span data-ttu-id="4cdf3-107">**An Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="4cdf3-107">**An Azure subscription**.</span></span> <span data-ttu-id="4cdf3-108">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4cdf3-108">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="4cdf3-109">**Azure Data Lake Store account**.</span><span class="sxs-lookup"><span data-stu-id="4cdf3-109">**Azure Data Lake Store account**.</span></span> <span data-ttu-id="4cdf3-110">Follow the instructions at [Get started with Azure Data Lake Store using the Azure Portal](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4cdf3-110">Follow the instructions at [Get started with Azure Data Lake Store using the Azure Portal](data-lake-store-get-started-portal.md).</span></span>

## <a name="enable-diagnostic-logging-for-your-data-lake-store-account"></a><span data-ttu-id="4cdf3-111">Enable diagnostic logging for your Data Lake Store account</span><span class="sxs-lookup"><span data-stu-id="4cdf3-111">Enable diagnostic logging for your Data Lake Store account</span></span>
1. <span data-ttu-id="4cdf3-112">Sign on to the new [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4cdf3-112">Sign on to the new [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="4cdf3-113">Open your Data Lake Store account, and from your Data Lake Store account blade, click **Settings**, and then click **Diagnostic logs**.</span><span class="sxs-lookup"><span data-stu-id="4cdf3-113">Open your Data Lake Store account, and from your Data Lake Store account blade, click **Settings**, and then click **Diagnostic logs**.</span></span>
3. <span data-ttu-id="4cdf3-114">In the **Diagnostics logs** blade, click **Turn on diagnostics**.</span><span class="sxs-lookup"><span data-stu-id="4cdf3-114">In the **Diagnostics logs** blade, click **Turn on diagnostics**.</span></span>

    <span data-ttu-id="4cdf3-115">![Enable diagnostic logging](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-diagnostic-logs/turn-on-diagnostics.png "Enable diagnostic logs")</span><span class="sxs-lookup"><span data-stu-id="4cdf3-115">![Enable diagnostic logging](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-diagnostic-logs/turn-on-diagnostics.png "Enable diagnostic logs")</span></span>

3. <span data-ttu-id="4cdf3-116">In the **Diagnostic** blade, make the following changes to configure diagnostic logging.</span><span class="sxs-lookup"><span data-stu-id="4cdf3-116">In the **Diagnostic** blade, make the following changes to configure diagnostic logging.</span></span>
   
    <span data-ttu-id="4cdf3-117">![Enable diagnostic logging](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-diagnostic-logs/enable-diagnostic-logs.png "Enable diagnostic logs")</span><span class="sxs-lookup"><span data-stu-id="4cdf3-117">![Enable diagnostic logging](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-diagnostic-logs/enable-diagnostic-logs.png "Enable diagnostic logs")</span></span>
   
   * <span data-ttu-id="4cdf3-118">Set **Status** to **On** to enable diagnostic logging.</span><span class="sxs-lookup"><span data-stu-id="4cdf3-118">Set **Status** to **On** to enable diagnostic logging.</span></span>
   * <span data-ttu-id="4cdf3-119">You can choose to store/process the data in different ways.</span><span class="sxs-lookup"><span data-stu-id="4cdf3-119">You can choose to store/process the data in different ways.</span></span>
     
        * <span data-ttu-id="4cdf3-120">Select the option to **Archive to a storage account** to store logs to an Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="4cdf3-120">Select the option to **Archive to a storage account** to store logs to an Azure Storage account.</span></span> <span data-ttu-id="4cdf3-121">You use this option if you want to archive the data that will be batch-processed at a later date.</span><span class="sxs-lookup"><span data-stu-id="4cdf3-121">You use this option if you want to archive the data that will be batch-processed at a later date.</span></span> <span data-ttu-id="4cdf3-122">If you select this option you must provide an Azure Storage account to save the logs to.</span><span class="sxs-lookup"><span data-stu-id="4cdf3-122">If you select this option you must provide an Azure Storage account to save the logs to.</span></span>
        
        * <span data-ttu-id="4cdf3-123">Select the option to **Stream to an event hub** to stream log data to an Azure Event Hub.</span><span class="sxs-lookup"><span data-stu-id="4cdf3-123">Select the option to **Stream to an event hub** to stream log data to an Azure Event Hub.</span></span> <span data-ttu-id="4cdf3-124">Most likely you will use this option if you have a downstream processing pipeline to analyze incoming logs at real time.</span><span class="sxs-lookup"><span data-stu-id="4cdf3-124">Most likely you will use this option if you have a downstream processing pipeline to analyze incoming logs at real time.</span></span> <span data-ttu-id="4cdf3-125">If you select this option, you must provide the details for the Azure Event Hub you want to use.</span><span class="sxs-lookup"><span data-stu-id="4cdf3-125">If you select this option, you must provide the details for the Azure Event Hub you want to use.</span></span>

        * <span data-ttu-id="4cdf3-126">Select the option to **Send to Log Analytics** to use the Azure Log Analytics service to analyze the generated log data.</span><span class="sxs-lookup"><span data-stu-id="4cdf3-126">Select the option to **Send to Log Analytics** to use the Azure Log Analytics service to analyze the generated log data.</span></span> <span data-ttu-id="4cdf3-127">If you select this option, you must provide the details for the Operations Management Suite workspace that you would use the perform log analysis.</span><span class="sxs-lookup"><span data-stu-id="4cdf3-127">If you select this option, you must provide the details for the Operations Management Suite workspace that you would use the perform log analysis.</span></span>
     
   * <span data-ttu-id="4cdf3-128">Specify whether you want to get audit logs or request logs or both.</span><span class="sxs-lookup"><span data-stu-id="4cdf3-128">Specify whether you want to get audit logs or request logs or both.</span></span>
   * <span data-ttu-id="4cdf3-129">Specify the number of days for which the data must be retained.</span><span class="sxs-lookup"><span data-stu-id="4cdf3-129">Specify the number of days for which the data must be retained.</span></span> <span data-ttu-id="4cdf3-130">Retention is only applicable if you are using Azure storage account to archive log data.</span><span class="sxs-lookup"><span data-stu-id="4cdf3-130">Retention is only applicable if you are using Azure storage account to archive log data.</span></span>
   * <span data-ttu-id="4cdf3-131">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="4cdf3-131">Click **Save**.</span></span>

<span data-ttu-id="4cdf3-132">Once you have enabled diagnostic settings, you can watch the logs in the **Diagnostic Logs** tab.</span><span class="sxs-lookup"><span data-stu-id="4cdf3-132">Once you have enabled diagnostic settings, you can watch the logs in the **Diagnostic Logs** tab.</span></span>

## <a name="view-diagnostic-logs-for-your-data-lake-store-account"></a><span data-ttu-id="4cdf3-133">View diagnostic logs for your Data Lake Store account</span><span class="sxs-lookup"><span data-stu-id="4cdf3-133">View diagnostic logs for your Data Lake Store account</span></span>
<span data-ttu-id="4cdf3-134">There are two ways to view the log data for your Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="4cdf3-134">There are two ways to view the log data for your Data Lake Store account.</span></span>

* <span data-ttu-id="4cdf3-135">From the Data Lake Store account settings view</span><span class="sxs-lookup"><span data-stu-id="4cdf3-135">From the Data Lake Store account settings view</span></span>
* <span data-ttu-id="4cdf3-136">From the Azure Storage account where the data is stored</span><span class="sxs-lookup"><span data-stu-id="4cdf3-136">From the Azure Storage account where the data is stored</span></span>

### <a name="using-the-data-lake-store-settings-view"></a><span data-ttu-id="4cdf3-137">Using the Data Lake Store Settings view</span><span class="sxs-lookup"><span data-stu-id="4cdf3-137">Using the Data Lake Store Settings view</span></span>
1. <span data-ttu-id="4cdf3-138">From your Data Lake Store account **Settings** blade, click **Diagnostic Logs**.</span><span class="sxs-lookup"><span data-stu-id="4cdf3-138">From your Data Lake Store account **Settings** blade, click **Diagnostic Logs**.</span></span>
   
    <span data-ttu-id="4cdf3-139">![View diagnostic logging](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-diagnostic-logs/view-diagnostic-logs.png "View diagnostic logs")</span><span class="sxs-lookup"><span data-stu-id="4cdf3-139">![View diagnostic logging](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-diagnostic-logs/view-diagnostic-logs.png "View diagnostic logs")</span></span> 
2. <span data-ttu-id="4cdf3-140">In the **Diagnostic Logs** blade, you should see the logs categorized by **Audit Logs** and **Request Logs**.</span><span class="sxs-lookup"><span data-stu-id="4cdf3-140">In the **Diagnostic Logs** blade, you should see the logs categorized by **Audit Logs** and **Request Logs**.</span></span>
   
   * <span data-ttu-id="4cdf3-141">Request logs capture every API request made on the Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="4cdf3-141">Request logs capture every API request made on the Data Lake Store account.</span></span>
   * <span data-ttu-id="4cdf3-142">Audit Logs are similar to request Logs but provide a much more detailed breakdown of the operations being performed on the Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="4cdf3-142">Audit Logs are similar to request Logs but provide a much more detailed breakdown of the operations being performed on the Data Lake Store account.</span></span> <span data-ttu-id="4cdf3-143">For example, a single upload API call in request logs might result in multiple "Append" operations in the audit logs.</span><span class="sxs-lookup"><span data-stu-id="4cdf3-143">For example, a single upload API call in request logs might result in multiple "Append" operations in the audit logs.</span></span>
3. <span data-ttu-id="4cdf3-144">Click the **Download** link against each log entry to download the logs.</span><span class="sxs-lookup"><span data-stu-id="4cdf3-144">Click the **Download** link against each log entry to download the logs.</span></span>

### <a name="from-the-azure-storage-account-that-contains-log-data"></a><span data-ttu-id="4cdf3-145">From the Azure Storage account that contains log data</span><span class="sxs-lookup"><span data-stu-id="4cdf3-145">From the Azure Storage account that contains log data</span></span>
1. <span data-ttu-id="4cdf3-146">Open the Azure Storage account blade associated with Data Lake Store for logging, and then click Blobs.</span><span class="sxs-lookup"><span data-stu-id="4cdf3-146">Open the Azure Storage account blade associated with Data Lake Store for logging, and then click Blobs.</span></span> <span data-ttu-id="4cdf3-147">The **Blob service** blade lists two containers.</span><span class="sxs-lookup"><span data-stu-id="4cdf3-147">The **Blob service** blade lists two containers.</span></span>
   
    <span data-ttu-id="4cdf3-148">![View diagnostic logging](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-diagnostic-logs/view-diagnostic-logs-storage-account.png "View diagnostic logs")</span><span class="sxs-lookup"><span data-stu-id="4cdf3-148">![View diagnostic logging](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-diagnostic-logs/view-diagnostic-logs-storage-account.png "View diagnostic logs")</span></span>
   
   * <span data-ttu-id="4cdf3-149">The container **insights-logs-audit** contains the audit logs.</span><span class="sxs-lookup"><span data-stu-id="4cdf3-149">The container **insights-logs-audit** contains the audit logs.</span></span>
   * <span data-ttu-id="4cdf3-150">The container **insights-logs-requests** contains the request logs.</span><span class="sxs-lookup"><span data-stu-id="4cdf3-150">The container **insights-logs-requests** contains the request logs.</span></span>
2. <span data-ttu-id="4cdf3-151">Within these containers, the logs are stored under the following structure.</span><span class="sxs-lookup"><span data-stu-id="4cdf3-151">Within these containers, the logs are stored under the following structure.</span></span>
   
    <span data-ttu-id="4cdf3-152">![View diagnostic logging](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-diagnostic-logs/view-diagnostic-logs-storage-account-structure.png "View diagnostic logs")</span><span class="sxs-lookup"><span data-stu-id="4cdf3-152">![View diagnostic logging](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-diagnostic-logs/view-diagnostic-logs-storage-account-structure.png "View diagnostic logs")</span></span>
   
    <span data-ttu-id="4cdf3-153">As an example, the complete path to an audit log could be `https://adllogs.blob.core.windows.net/insights-logs-audit/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/mydatalakestore/y=2016/m=07/d=18/h=04/m=00/PT1H.json`</span><span class="sxs-lookup"><span data-stu-id="4cdf3-153">As an example, the complete path to an audit log could be `https://adllogs.blob.core.windows.net/insights-logs-audit/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/mydatalakestore/y=2016/m=07/d=18/h=04/m=00/PT1H.json`</span></span>
   
    <span data-ttu-id="4cdf3-154">Similary, the complete path to a request log could be `https://adllogs.blob.core.windows.net/insights-logs-requests/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/mydatalakestore/y=2016/m=07/d=18/h=14/m=00/PT1H.json`</span><span class="sxs-lookup"><span data-stu-id="4cdf3-154">Similary, the complete path to a request log could be `https://adllogs.blob.core.windows.net/insights-logs-requests/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/mydatalakestore/y=2016/m=07/d=18/h=14/m=00/PT1H.json`</span></span>

## <a name="understand-the-structure-of-the-log-data"></a><span data-ttu-id="4cdf3-155">Understand the structure of the log data</span><span class="sxs-lookup"><span data-stu-id="4cdf3-155">Understand the structure of the log data</span></span>
<span data-ttu-id="4cdf3-156">The audit and request logs are in a JSON format.</span><span class="sxs-lookup"><span data-stu-id="4cdf3-156">The audit and request logs are in a JSON format.</span></span> <span data-ttu-id="4cdf3-157">In this section, we look at the structure of JSON for request and audit logs.</span><span class="sxs-lookup"><span data-stu-id="4cdf3-157">In this section, we look at the structure of JSON for request and audit logs.</span></span>

### <a name="request-logs"></a><span data-ttu-id="4cdf3-158">Request logs</span><span class="sxs-lookup"><span data-stu-id="4cdf3-158">Request logs</span></span>
<span data-ttu-id="4cdf3-159">Here's a sample entry in the JSON-formatted request log.</span><span class="sxs-lookup"><span data-stu-id="4cdf3-159">Here's a sample entry in the JSON-formatted request log.</span></span> <span data-ttu-id="4cdf3-160">Each blob has one root object called **records** that contains an array of log objects.</span><span class="sxs-lookup"><span data-stu-id="4cdf3-160">Each blob has one root object called **records** that contains an array of log objects.</span></span>

    {
    "records": 
      [        
        . . . .
        ,
        {
             "time": "2016-07-07T21:02:53.456Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/<data_lake_store_account_name>",
             "category": "Requests",
             "operationName": "GETCustomerIngressEgress",
             "resultType": "200",
             "callerIpAddress": "::ffff:1.1.1.1",
             "correlationId": "4a11c709-05f5-417c-a98d-6e81b3e29c58",
             "identity": "1808bd5f-62af-45f4-89d8-03c5e81bac30",
             "properties": {"HttpMethod":"GET","Path":"/webhdfs/v1/Samples/Outputs/Drivers.csv","RequestContentLength":0,"ClientRequestId":"3b7adbd9-3519-4f28-a61c-bd89506163b8","StartTime":"2016-07-07T21:02:52.472Z","EndTime":"2016-07-07T21:02:53.456Z"}
        }
        ,
        . . . .
      ]
    }

#### <a name="request-log-schema"></a><span data-ttu-id="4cdf3-161">Request log schema</span><span class="sxs-lookup"><span data-stu-id="4cdf3-161">Request log schema</span></span>
| <span data-ttu-id="4cdf3-162">Name</span><span class="sxs-lookup"><span data-stu-id="4cdf3-162">Name</span></span> | <span data-ttu-id="4cdf3-163">Type</span><span class="sxs-lookup"><span data-stu-id="4cdf3-163">Type</span></span> | <span data-ttu-id="4cdf3-164">Description</span><span class="sxs-lookup"><span data-stu-id="4cdf3-164">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4cdf3-165">time</span><span class="sxs-lookup"><span data-stu-id="4cdf3-165">time</span></span> |<span data-ttu-id="4cdf3-166">String</span><span class="sxs-lookup"><span data-stu-id="4cdf3-166">String</span></span> |<span data-ttu-id="4cdf3-167">The timestamp (in UTC) of the log</span><span class="sxs-lookup"><span data-stu-id="4cdf3-167">The timestamp (in UTC) of the log</span></span> |
| <span data-ttu-id="4cdf3-168">resourceId</span><span class="sxs-lookup"><span data-stu-id="4cdf3-168">resourceId</span></span> |<span data-ttu-id="4cdf3-169">String</span><span class="sxs-lookup"><span data-stu-id="4cdf3-169">String</span></span> |<span data-ttu-id="4cdf3-170">The ID of the resource that operation took place on</span><span class="sxs-lookup"><span data-stu-id="4cdf3-170">The ID of the resource that operation took place on</span></span> |
| <span data-ttu-id="4cdf3-171">category</span><span class="sxs-lookup"><span data-stu-id="4cdf3-171">category</span></span> |<span data-ttu-id="4cdf3-172">String</span><span class="sxs-lookup"><span data-stu-id="4cdf3-172">String</span></span> |<span data-ttu-id="4cdf3-173">The log category.</span><span class="sxs-lookup"><span data-stu-id="4cdf3-173">The log category.</span></span> <span data-ttu-id="4cdf3-174">For example, **Requests**.</span><span class="sxs-lookup"><span data-stu-id="4cdf3-174">For example, **Requests**.</span></span> |
| <span data-ttu-id="4cdf3-175">operationName</span><span class="sxs-lookup"><span data-stu-id="4cdf3-175">operationName</span></span> |<span data-ttu-id="4cdf3-176">String</span><span class="sxs-lookup"><span data-stu-id="4cdf3-176">String</span></span> |<span data-ttu-id="4cdf3-177">Name of the operation that is logged.</span><span class="sxs-lookup"><span data-stu-id="4cdf3-177">Name of the operation that is logged.</span></span> <span data-ttu-id="4cdf3-178">For example, getfilestatus.</span><span class="sxs-lookup"><span data-stu-id="4cdf3-178">For example, getfilestatus.</span></span> |
| <span data-ttu-id="4cdf3-179">resultType</span><span class="sxs-lookup"><span data-stu-id="4cdf3-179">resultType</span></span> |<span data-ttu-id="4cdf3-180">String</span><span class="sxs-lookup"><span data-stu-id="4cdf3-180">String</span></span> |<span data-ttu-id="4cdf3-181">The status of the operation, For example, 200.</span><span class="sxs-lookup"><span data-stu-id="4cdf3-181">The status of the operation, For example, 200.</span></span> |
| <span data-ttu-id="4cdf3-182">callerIpAddress</span><span class="sxs-lookup"><span data-stu-id="4cdf3-182">callerIpAddress</span></span> |<span data-ttu-id="4cdf3-183">String</span><span class="sxs-lookup"><span data-stu-id="4cdf3-183">String</span></span> |<span data-ttu-id="4cdf3-184">The IP address of the client making the request</span><span class="sxs-lookup"><span data-stu-id="4cdf3-184">The IP address of the client making the request</span></span> |
| <span data-ttu-id="4cdf3-185">correlationId</span><span class="sxs-lookup"><span data-stu-id="4cdf3-185">correlationId</span></span> |<span data-ttu-id="4cdf3-186">String</span><span class="sxs-lookup"><span data-stu-id="4cdf3-186">String</span></span> |<span data-ttu-id="4cdf3-187">The id of the log that can used to group together a set of related log entries</span><span class="sxs-lookup"><span data-stu-id="4cdf3-187">The id of the log that can used to group together a set of related log entries</span></span> |
| <span data-ttu-id="4cdf3-188">identity</span><span class="sxs-lookup"><span data-stu-id="4cdf3-188">identity</span></span> |<span data-ttu-id="4cdf3-189">Object</span><span class="sxs-lookup"><span data-stu-id="4cdf3-189">Object</span></span> |<span data-ttu-id="4cdf3-190">The identity that generated the log</span><span class="sxs-lookup"><span data-stu-id="4cdf3-190">The identity that generated the log</span></span> |
| <span data-ttu-id="4cdf3-191">properties</span><span class="sxs-lookup"><span data-stu-id="4cdf3-191">properties</span></span> |<span data-ttu-id="4cdf3-192">JSON</span><span class="sxs-lookup"><span data-stu-id="4cdf3-192">JSON</span></span> |<span data-ttu-id="4cdf3-193">See below for details</span><span class="sxs-lookup"><span data-stu-id="4cdf3-193">See below for details</span></span> |

#### <a name="request-log-properties-schema"></a><span data-ttu-id="4cdf3-194">Request log properties schema</span><span class="sxs-lookup"><span data-stu-id="4cdf3-194">Request log properties schema</span></span>
| <span data-ttu-id="4cdf3-195">Name</span><span class="sxs-lookup"><span data-stu-id="4cdf3-195">Name</span></span> | <span data-ttu-id="4cdf3-196">Type</span><span class="sxs-lookup"><span data-stu-id="4cdf3-196">Type</span></span> | <span data-ttu-id="4cdf3-197">Description</span><span class="sxs-lookup"><span data-stu-id="4cdf3-197">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4cdf3-198">HttpMethod</span><span class="sxs-lookup"><span data-stu-id="4cdf3-198">HttpMethod</span></span> |<span data-ttu-id="4cdf3-199">String</span><span class="sxs-lookup"><span data-stu-id="4cdf3-199">String</span></span> |<span data-ttu-id="4cdf3-200">The HTTP Method used for the operation.</span><span class="sxs-lookup"><span data-stu-id="4cdf3-200">The HTTP Method used for the operation.</span></span> <span data-ttu-id="4cdf3-201">For example, GET.</span><span class="sxs-lookup"><span data-stu-id="4cdf3-201">For example, GET.</span></span> |
| <span data-ttu-id="4cdf3-202">Path</span><span class="sxs-lookup"><span data-stu-id="4cdf3-202">Path</span></span> |<span data-ttu-id="4cdf3-203">String</span><span class="sxs-lookup"><span data-stu-id="4cdf3-203">String</span></span> |<span data-ttu-id="4cdf3-204">The path the operation was performed on</span><span class="sxs-lookup"><span data-stu-id="4cdf3-204">The path the operation was performed on</span></span> |
| <span data-ttu-id="4cdf3-205">RequestContentLength</span><span class="sxs-lookup"><span data-stu-id="4cdf3-205">RequestContentLength</span></span> |<span data-ttu-id="4cdf3-206">int</span><span class="sxs-lookup"><span data-stu-id="4cdf3-206">int</span></span> |<span data-ttu-id="4cdf3-207">The content length of the HTTP request</span><span class="sxs-lookup"><span data-stu-id="4cdf3-207">The content length of the HTTP request</span></span> |
| <span data-ttu-id="4cdf3-208">ClientRequestId</span><span class="sxs-lookup"><span data-stu-id="4cdf3-208">ClientRequestId</span></span> |<span data-ttu-id="4cdf3-209">String</span><span class="sxs-lookup"><span data-stu-id="4cdf3-209">String</span></span> |<span data-ttu-id="4cdf3-210">The Id that uniquely identifies this request</span><span class="sxs-lookup"><span data-stu-id="4cdf3-210">The Id that uniquely identifies this request</span></span> |
| <span data-ttu-id="4cdf3-211">StartTime</span><span class="sxs-lookup"><span data-stu-id="4cdf3-211">StartTime</span></span> |<span data-ttu-id="4cdf3-212">String</span><span class="sxs-lookup"><span data-stu-id="4cdf3-212">String</span></span> |<span data-ttu-id="4cdf3-213">The time at which the server received the request</span><span class="sxs-lookup"><span data-stu-id="4cdf3-213">The time at which the server received the request</span></span> |
| <span data-ttu-id="4cdf3-214">EndTime</span><span class="sxs-lookup"><span data-stu-id="4cdf3-214">EndTime</span></span> |<span data-ttu-id="4cdf3-215">String</span><span class="sxs-lookup"><span data-stu-id="4cdf3-215">String</span></span> |<span data-ttu-id="4cdf3-216">The time at which the server sent a response</span><span class="sxs-lookup"><span data-stu-id="4cdf3-216">The time at which the server sent a response</span></span> |

### <a name="audit-logs"></a><span data-ttu-id="4cdf3-217">Audit logs</span><span class="sxs-lookup"><span data-stu-id="4cdf3-217">Audit logs</span></span>
<span data-ttu-id="4cdf3-218">Here's a sample entry in the JSON-formatted audit log.</span><span class="sxs-lookup"><span data-stu-id="4cdf3-218">Here's a sample entry in the JSON-formatted audit log.</span></span> <span data-ttu-id="4cdf3-219">Each blob has one root object called **records** that contains an array of log objects</span><span class="sxs-lookup"><span data-stu-id="4cdf3-219">Each blob has one root object called **records** that contains an array of log objects</span></span>

    {
    "records": 
      [        
        . . . .
        ,
        {
             "time": "2016-07-08T19:08:59.359Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/<data_lake_store_account_name>",
             "category": "Audit",
             "operationName": "SeOpenStream",
             "resultType": "0",
             "correlationId": "381110fc03534e1cb99ec52376ceebdf;Append_BrEKAmg;25.66.9.145",
             "identity": "A9DAFFAF-FFEE-4BB5-A4A0-1B6CBBF24355",
             "properties": {"StreamName":"adl://<data_lake_store_account_name>.azuredatalakestore.net/logs.csv"}
        }
        ,
        . . . .
      ]
    }

#### <a name="audit-log-schema"></a><span data-ttu-id="4cdf3-220">Audit log schema</span><span class="sxs-lookup"><span data-stu-id="4cdf3-220">Audit log schema</span></span>
| <span data-ttu-id="4cdf3-221">Name</span><span class="sxs-lookup"><span data-stu-id="4cdf3-221">Name</span></span> | <span data-ttu-id="4cdf3-222">Type</span><span class="sxs-lookup"><span data-stu-id="4cdf3-222">Type</span></span> | <span data-ttu-id="4cdf3-223">Description</span><span class="sxs-lookup"><span data-stu-id="4cdf3-223">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4cdf3-224">time</span><span class="sxs-lookup"><span data-stu-id="4cdf3-224">time</span></span> |<span data-ttu-id="4cdf3-225">String</span><span class="sxs-lookup"><span data-stu-id="4cdf3-225">String</span></span> |<span data-ttu-id="4cdf3-226">The timestamp (in UTC) of the log</span><span class="sxs-lookup"><span data-stu-id="4cdf3-226">The timestamp (in UTC) of the log</span></span> |
| <span data-ttu-id="4cdf3-227">resourceId</span><span class="sxs-lookup"><span data-stu-id="4cdf3-227">resourceId</span></span> |<span data-ttu-id="4cdf3-228">String</span><span class="sxs-lookup"><span data-stu-id="4cdf3-228">String</span></span> |<span data-ttu-id="4cdf3-229">The ID of the resource that operation took place on</span><span class="sxs-lookup"><span data-stu-id="4cdf3-229">The ID of the resource that operation took place on</span></span> |
| <span data-ttu-id="4cdf3-230">category</span><span class="sxs-lookup"><span data-stu-id="4cdf3-230">category</span></span> |<span data-ttu-id="4cdf3-231">String</span><span class="sxs-lookup"><span data-stu-id="4cdf3-231">String</span></span> |<span data-ttu-id="4cdf3-232">The log category.</span><span class="sxs-lookup"><span data-stu-id="4cdf3-232">The log category.</span></span> <span data-ttu-id="4cdf3-233">For example, **Audit**.</span><span class="sxs-lookup"><span data-stu-id="4cdf3-233">For example, **Audit**.</span></span> |
| <span data-ttu-id="4cdf3-234">operationName</span><span class="sxs-lookup"><span data-stu-id="4cdf3-234">operationName</span></span> |<span data-ttu-id="4cdf3-235">String</span><span class="sxs-lookup"><span data-stu-id="4cdf3-235">String</span></span> |<span data-ttu-id="4cdf3-236">Name of the operation that is logged.</span><span class="sxs-lookup"><span data-stu-id="4cdf3-236">Name of the operation that is logged.</span></span> <span data-ttu-id="4cdf3-237">For example, getfilestatus.</span><span class="sxs-lookup"><span data-stu-id="4cdf3-237">For example, getfilestatus.</span></span> |
| <span data-ttu-id="4cdf3-238">resultType</span><span class="sxs-lookup"><span data-stu-id="4cdf3-238">resultType</span></span> |<span data-ttu-id="4cdf3-239">String</span><span class="sxs-lookup"><span data-stu-id="4cdf3-239">String</span></span> |<span data-ttu-id="4cdf3-240">The status of the operation, For example, 200.</span><span class="sxs-lookup"><span data-stu-id="4cdf3-240">The status of the operation, For example, 200.</span></span> |
| <span data-ttu-id="4cdf3-241">correlationId</span><span class="sxs-lookup"><span data-stu-id="4cdf3-241">correlationId</span></span> |<span data-ttu-id="4cdf3-242">String</span><span class="sxs-lookup"><span data-stu-id="4cdf3-242">String</span></span> |<span data-ttu-id="4cdf3-243">The id of the log that can used to group together a set of related log entries</span><span class="sxs-lookup"><span data-stu-id="4cdf3-243">The id of the log that can used to group together a set of related log entries</span></span> |
| <span data-ttu-id="4cdf3-244">identity</span><span class="sxs-lookup"><span data-stu-id="4cdf3-244">identity</span></span> |<span data-ttu-id="4cdf3-245">Object</span><span class="sxs-lookup"><span data-stu-id="4cdf3-245">Object</span></span> |<span data-ttu-id="4cdf3-246">The identity that generated the log</span><span class="sxs-lookup"><span data-stu-id="4cdf3-246">The identity that generated the log</span></span> |
| <span data-ttu-id="4cdf3-247">properties</span><span class="sxs-lookup"><span data-stu-id="4cdf3-247">properties</span></span> |<span data-ttu-id="4cdf3-248">JSON</span><span class="sxs-lookup"><span data-stu-id="4cdf3-248">JSON</span></span> |<span data-ttu-id="4cdf3-249">See below for details</span><span class="sxs-lookup"><span data-stu-id="4cdf3-249">See below for details</span></span> |

#### <a name="audit-log-properties-schema"></a><span data-ttu-id="4cdf3-250">Audit log properties schema</span><span class="sxs-lookup"><span data-stu-id="4cdf3-250">Audit log properties schema</span></span>
| <span data-ttu-id="4cdf3-251">Name</span><span class="sxs-lookup"><span data-stu-id="4cdf3-251">Name</span></span> | <span data-ttu-id="4cdf3-252">Type</span><span class="sxs-lookup"><span data-stu-id="4cdf3-252">Type</span></span> | <span data-ttu-id="4cdf3-253">Description</span><span class="sxs-lookup"><span data-stu-id="4cdf3-253">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4cdf3-254">StreamName</span><span class="sxs-lookup"><span data-stu-id="4cdf3-254">StreamName</span></span> |<span data-ttu-id="4cdf3-255">String</span><span class="sxs-lookup"><span data-stu-id="4cdf3-255">String</span></span> |<span data-ttu-id="4cdf3-256">The path the operation was performed on</span><span class="sxs-lookup"><span data-stu-id="4cdf3-256">The path the operation was performed on</span></span> |

## <a name="samples-to-process-the-log-data"></a><span data-ttu-id="4cdf3-257">Samples to process the log data</span><span class="sxs-lookup"><span data-stu-id="4cdf3-257">Samples to process the log data</span></span>
<span data-ttu-id="4cdf3-258">Azure Data Lake Store provides a sample on how to process and analyze the log data.</span><span class="sxs-lookup"><span data-stu-id="4cdf3-258">Azure Data Lake Store provides a sample on how to process and analyze the log data.</span></span> <span data-ttu-id="4cdf3-259">You can find the sample at [https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample](https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample).</span><span class="sxs-lookup"><span data-stu-id="4cdf3-259">You can find the sample at [https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample](https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample).</span></span> 

## <a name="see-also"></a><span data-ttu-id="4cdf3-260">See also</span><span class="sxs-lookup"><span data-stu-id="4cdf3-260">See also</span></span>
* [<span data-ttu-id="4cdf3-261">Overview of Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="4cdf3-261">Overview of Azure Data Lake Store</span></span>](data-lake-store-overview.md)
* [<span data-ttu-id="4cdf3-262">Secure data in Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="4cdf3-262">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)






