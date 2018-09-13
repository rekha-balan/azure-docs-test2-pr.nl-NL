---
title: Viewing diagnostic logs for Azure Data Lake Analytics | Microsoft Docs
description: 'Understand how to setup and access diagnostic logs for Azure Data Lake analytics '
services: data-lake-analytics
documentationcenter: ''
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: cf5633d4-bc43-444e-90fc-f90fbd0b7935
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 02/10/2017
ms.author: larryfr
ms.openlocfilehash: 3119a156304748c95619a175473c6acdcee67406
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555126"
---
# <a name="accessing-diagnostic-logs-for-azure-data-lake-analytics"></a><span data-ttu-id="e5973-103">Accessing diagnostic logs for Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="e5973-103">Accessing diagnostic logs for Azure Data Lake Analytics</span></span>

<span data-ttu-id="e5973-104">Learn about how to enable diagnostic logging for your Data Lake Analytics account and how to view the logs collected for your account.</span><span class="sxs-lookup"><span data-stu-id="e5973-104">Learn about how to enable diagnostic logging for your Data Lake Analytics account and how to view the logs collected for your account.</span></span>

<span data-ttu-id="e5973-105">Organizations can enable diagnostic logging for their Azure Data Lake Analytics account to collect data access audit trails.</span><span class="sxs-lookup"><span data-stu-id="e5973-105">Organizations can enable diagnostic logging for their Azure Data Lake Analytics account to collect data access audit trails.</span></span> <span data-ttu-id="e5973-106">These logs provide information such as:</span><span class="sxs-lookup"><span data-stu-id="e5973-106">These logs provide information such as:</span></span>

* <span data-ttu-id="e5973-107">A list of users that accessed the data.</span><span class="sxs-lookup"><span data-stu-id="e5973-107">A list of users that accessed the data.</span></span>
* <span data-ttu-id="e5973-108">How frequently the data is accessed.</span><span class="sxs-lookup"><span data-stu-id="e5973-108">How frequently the data is accessed.</span></span>
* <span data-ttu-id="e5973-109">How much data is stored in the account.</span><span class="sxs-lookup"><span data-stu-id="e5973-109">How much data is stored in the account.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e5973-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e5973-110">Prerequisites</span></span>

* <span data-ttu-id="e5973-111">**An Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="e5973-111">**An Azure subscription**.</span></span> <span data-ttu-id="e5973-112">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e5973-112">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="e5973-113">**Enable your Azure subscription** for Data Lake Analytics Public Preview.</span><span class="sxs-lookup"><span data-stu-id="e5973-113">**Enable your Azure subscription** for Data Lake Analytics Public Preview.</span></span> <span data-ttu-id="e5973-114">See [instructions](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e5973-114">See [instructions](data-lake-analytics-get-started-portal.md).</span></span>

* <span data-ttu-id="e5973-115">**Azure Data Lake Analytics account**.</span><span class="sxs-lookup"><span data-stu-id="e5973-115">**Azure Data Lake Analytics account**.</span></span> <span data-ttu-id="e5973-116">Follow the instructions at [Get started with Azure Data Lake Analytics using the Azure portal](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e5973-116">Follow the instructions at [Get started with Azure Data Lake Analytics using the Azure portal](data-lake-analytics-get-started-portal.md).</span></span>

## <a name="enable-logging"></a><span data-ttu-id="e5973-117">Enable logging</span><span class="sxs-lookup"><span data-stu-id="e5973-117">Enable logging</span></span>

1. <span data-ttu-id="e5973-118">Sign on to the new [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e5973-118">Sign on to the new [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="e5973-119">Open your Data Lake Analytics account and select **Diagnostic logs** from the __Monitoring section__.</span><span class="sxs-lookup"><span data-stu-id="e5973-119">Open your Data Lake Analytics account and select **Diagnostic logs** from the __Monitoring section__.</span></span> <span data-ttu-id="e5973-120">Next, select __Turn on diagnostics__.</span><span class="sxs-lookup"><span data-stu-id="e5973-120">Next, select __Turn on diagnostics__.</span></span>

    ![Turn on diagnostics to collect audit and request logs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-diagnostic-logs/turn-on-logging.png)

3. <span data-ttu-id="e5973-122">From __Diagnostics settings__, set the status to __On__ and select logging options.</span><span class="sxs-lookup"><span data-stu-id="e5973-122">From __Diagnostics settings__, set the status to __On__ and select logging options.</span></span>

    <span data-ttu-id="e5973-123">![Turn on diagnostics to collect audit and request logs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-diagnostic-logs/enable-diagnostic-logs.png "Enable diagnostic logs")</span><span class="sxs-lookup"><span data-stu-id="e5973-123">![Turn on diagnostics to collect audit and request logs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-diagnostic-logs/enable-diagnostic-logs.png "Enable diagnostic logs")</span></span>

   * <span data-ttu-id="e5973-124">Set **Status** to **On** to enable diagnostic logging.</span><span class="sxs-lookup"><span data-stu-id="e5973-124">Set **Status** to **On** to enable diagnostic logging.</span></span>

   * <span data-ttu-id="e5973-125">You can choose to store/process the data in two different ways.</span><span class="sxs-lookup"><span data-stu-id="e5973-125">You can choose to store/process the data in two different ways.</span></span>

     * <span data-ttu-id="e5973-126">Select __Archive to a storage account__ to store logs in an Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="e5973-126">Select __Archive to a storage account__ to store logs in an Azure storage account.</span></span> <span data-ttu-id="e5973-127">Use this option if you want to archive the data.</span><span class="sxs-lookup"><span data-stu-id="e5973-127">Use this option if you want to archive the data.</span></span> <span data-ttu-id="e5973-128">If you select this option, you must provide an Azure storage account to save the logs to.</span><span class="sxs-lookup"><span data-stu-id="e5973-128">If you select this option, you must provide an Azure storage account to save the logs to.</span></span>

     * <span data-ttu-id="e5973-129">Select **Stream to an Event Hub** to stream log data to an Azure Event Hub.</span><span class="sxs-lookup"><span data-stu-id="e5973-129">Select **Stream to an Event Hub** to stream log data to an Azure Event Hub.</span></span> <span data-ttu-id="e5973-130">Use this option if you have a downstream processing pipeline to analyze incoming logs in real time.</span><span class="sxs-lookup"><span data-stu-id="e5973-130">Use this option if you have a downstream processing pipeline to analyze incoming logs in real time.</span></span> <span data-ttu-id="e5973-131">If you select this option, you must provide the details for the Azure Event Hub you want to use.</span><span class="sxs-lookup"><span data-stu-id="e5973-131">If you select this option, you must provide the details for the Azure Event Hub you want to use.</span></span>

     * <span data-ttu-id="e5973-132">Select __Send to Log Analytics__ to send the data to the Log Analytics service.</span><span class="sxs-lookup"><span data-stu-id="e5973-132">Select __Send to Log Analytics__ to send the data to the Log Analytics service.</span></span> <span data-ttu-id="e5973-133">Use this if you want to use Log Analytics to gather and analyze logs.</span><span class="sxs-lookup"><span data-stu-id="e5973-133">Use this if you want to use Log Analytics to gather and analyze logs.</span></span>
   * <span data-ttu-id="e5973-134">Specify whether you want to get audit logs or request logs or both.</span><span class="sxs-lookup"><span data-stu-id="e5973-134">Specify whether you want to get audit logs or request logs or both.</span></span>

   * <span data-ttu-id="e5973-135">Specify the number of days for which the data must be retained.</span><span class="sxs-lookup"><span data-stu-id="e5973-135">Specify the number of days for which the data must be retained.</span></span>

   * <span data-ttu-id="e5973-136">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="e5973-136">Click **Save**.</span></span>

        > [!NOTE]
        > <span data-ttu-id="e5973-137">You must select either __Archive to a storage account__, __Stream to an Event Hub__ or __Send to Log Analytics__ before using the __Save__ button.</span><span class="sxs-lookup"><span data-stu-id="e5973-137">You must select either __Archive to a storage account__, __Stream to an Event Hub__ or __Send to Log Analytics__ before using the __Save__ button.</span></span>

<span data-ttu-id="e5973-138">Once you have enabled diagnostic settings, you can return to the __Diagnostics logs__ blade to view logs.</span><span class="sxs-lookup"><span data-stu-id="e5973-138">Once you have enabled diagnostic settings, you can return to the __Diagnostics logs__ blade to view logs.</span></span>

## <a name="view-logs"></a><span data-ttu-id="e5973-139">View logs</span><span class="sxs-lookup"><span data-stu-id="e5973-139">View logs</span></span>

<span data-ttu-id="e5973-140">There are two ways to view the log data for your Data Lake Analytics account.</span><span class="sxs-lookup"><span data-stu-id="e5973-140">There are two ways to view the log data for your Data Lake Analytics account.</span></span>

* <span data-ttu-id="e5973-141">From the Data Lake Analytics account settings</span><span class="sxs-lookup"><span data-stu-id="e5973-141">From the Data Lake Analytics account settings</span></span>
* <span data-ttu-id="e5973-142">From the Azure Storage account where the data is stored</span><span class="sxs-lookup"><span data-stu-id="e5973-142">From the Azure Storage account where the data is stored</span></span>

### <a name="using-the-data-lake-analytics-settings-view"></a><span data-ttu-id="e5973-143">Using the Data Lake Analytics Settings view</span><span class="sxs-lookup"><span data-stu-id="e5973-143">Using the Data Lake Analytics Settings view</span></span>

1. <span data-ttu-id="e5973-144">From your Data Lake Analytics account blade, select **Diagnostic Logs** and then select the entry to display logs for.</span><span class="sxs-lookup"><span data-stu-id="e5973-144">From your Data Lake Analytics account blade, select **Diagnostic Logs** and then select the entry to display logs for.</span></span>

    <span data-ttu-id="e5973-145">![View diagnostic logging](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs.png "View diagnostic logs")</span><span class="sxs-lookup"><span data-stu-id="e5973-145">![View diagnostic logging](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs.png "View diagnostic logs")</span></span>

2. <span data-ttu-id="e5973-146">The logs are categorized by **Audit Logs** and **Request Logs**.</span><span class="sxs-lookup"><span data-stu-id="e5973-146">The logs are categorized by **Audit Logs** and **Request Logs**.</span></span>

    ![log entries](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-diagnostic-logs/diagnostic-log-entries.png)

   * <span data-ttu-id="e5973-148">Request logs capture every API request made on the Data Lake Analytics account.</span><span class="sxs-lookup"><span data-stu-id="e5973-148">Request logs capture every API request made on the Data Lake Analytics account.</span></span>
   * <span data-ttu-id="e5973-149">Audit Logs are similar to request Logs but provide a much more detailed breakdown of the operations being performed on the Data Lake Analytics account.</span><span class="sxs-lookup"><span data-stu-id="e5973-149">Audit Logs are similar to request Logs but provide a much more detailed breakdown of the operations being performed on the Data Lake Analytics account.</span></span> <span data-ttu-id="e5973-150">For example, a single upload API call in request logs might result in multiple "Append" operations in the audit logs.</span><span class="sxs-lookup"><span data-stu-id="e5973-150">For example, a single upload API call in request logs might result in multiple "Append" operations in the audit logs.</span></span>

3. <span data-ttu-id="e5973-151">Click the **Download** link for a log entry to download the logs.</span><span class="sxs-lookup"><span data-stu-id="e5973-151">Click the **Download** link for a log entry to download the logs.</span></span>

### <a name="from-the-azure-storage-account-that-contains-log-data"></a><span data-ttu-id="e5973-152">From the Azure Storage account that contains log data</span><span class="sxs-lookup"><span data-stu-id="e5973-152">From the Azure Storage account that contains log data</span></span>

1. <span data-ttu-id="e5973-153">Open the Azure Storage account blade associated with Data Lake Analytics for logging, and then click Blobs.</span><span class="sxs-lookup"><span data-stu-id="e5973-153">Open the Azure Storage account blade associated with Data Lake Analytics for logging, and then click Blobs.</span></span> <span data-ttu-id="e5973-154">The **Blob service** blade lists two containers.</span><span class="sxs-lookup"><span data-stu-id="e5973-154">The **Blob service** blade lists two containers.</span></span>

    <span data-ttu-id="e5973-155">![View diagnostic logging](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs-storage-account.png "View diagnostic logs")</span><span class="sxs-lookup"><span data-stu-id="e5973-155">![View diagnostic logging](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs-storage-account.png "View diagnostic logs")</span></span>

   * <span data-ttu-id="e5973-156">The container **insights-logs-audit** contains the audit logs.</span><span class="sxs-lookup"><span data-stu-id="e5973-156">The container **insights-logs-audit** contains the audit logs.</span></span>
   * <span data-ttu-id="e5973-157">The container **insights-logs-requests** contains the request logs.</span><span class="sxs-lookup"><span data-stu-id="e5973-157">The container **insights-logs-requests** contains the request logs.</span></span>
2. <span data-ttu-id="e5973-158">Within these containers, the logs are stored under the following structure.</span><span class="sxs-lookup"><span data-stu-id="e5973-158">Within these containers, the logs are stored under the following structure.</span></span>

        resourceId=/
          SUBSCRIPTIONS/
            <<SUBSCRIPTION_ID>>/
              RESOURCEGROUPS/
                <<RESOURCE_GRP_NAME>>/
                  PROVIDERS/
                    MICROSOFT.DATALAKEANALYTICS/
                      ACCOUNTS/
                        <DATA_LAKE_ANALYTICS_NAME>>/
                          y=####/
                            m=##/
                              d=##/
                                h=##/
                                  m=00/
                                    PT1H.json

   > [!NOTE]
   > <span data-ttu-id="e5973-159">The `##` entries in the path contain the year, month, day, and hour in which the log was created.</span><span class="sxs-lookup"><span data-stu-id="e5973-159">The `##` entries in the path contain the year, month, day, and hour in which the log was created.</span></span> <span data-ttu-id="e5973-160">Data Lake Analytics creates one file every hour, so `m=` always contains a value of `00`.</span><span class="sxs-lookup"><span data-stu-id="e5973-160">Data Lake Analytics creates one file every hour, so `m=` always contains a value of `00`.</span></span>

    <span data-ttu-id="e5973-161">As an example, the complete path to an audit log could be:</span><span class="sxs-lookup"><span data-stu-id="e5973-161">As an example, the complete path to an audit log could be:</span></span>

        https://adllogs.blob.core.windows.net/insights-logs-audit/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/mydatalakeanalytics/y=2016/m=07/d=18/h=04/m=00/PT1H.json

    <span data-ttu-id="e5973-162">Similarly, the complete path to a request log could be:</span><span class="sxs-lookup"><span data-stu-id="e5973-162">Similarly, the complete path to a request log could be:</span></span>

        https://adllogs.blob.core.windows.net/insights-logs-requests/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/mydatalakeanalytics/y=2016/m=07/d=18/h=14/m=00/PT1H.json

## <a name="log-structure"></a><span data-ttu-id="e5973-163">Log structure</span><span class="sxs-lookup"><span data-stu-id="e5973-163">Log structure</span></span>

<span data-ttu-id="e5973-164">The audit and request logs are in a JSON format.</span><span class="sxs-lookup"><span data-stu-id="e5973-164">The audit and request logs are in a JSON format.</span></span> <span data-ttu-id="e5973-165">In this section, we look at the structure of JSON for request and audit logs.</span><span class="sxs-lookup"><span data-stu-id="e5973-165">In this section, we look at the structure of JSON for request and audit logs.</span></span>

### <a name="request-logs"></a><span data-ttu-id="e5973-166">Request logs</span><span class="sxs-lookup"><span data-stu-id="e5973-166">Request logs</span></span>

<span data-ttu-id="e5973-167">Here's a sample entry in the JSON-formatted request log.</span><span class="sxs-lookup"><span data-stu-id="e5973-167">Here's a sample entry in the JSON-formatted request log.</span></span> <span data-ttu-id="e5973-168">Each blob has one root object called **records** that contains an array of log objects.</span><span class="sxs-lookup"><span data-stu-id="e5973-168">Each blob has one root object called **records** that contains an array of log objects.</span></span>

    {
    "records":
      [        
        . . . .
        ,
        {
             "time": "2016-07-07T21:02:53.456Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/<data_lake_analytics_account_name>",
             "category": "Requests",
             "operationName": "GetAggregatedJobHistory",
             "resultType": "200",
             "callerIpAddress": "::ffff:1.1.1.1",
             "correlationId": "4a11c709-05f5-417c-a98d-6e81b3e29c58",
             "identity": "1808bd5f-62af-45f4-89d8-03c5e81bac30",
             "properties": {
                 "HttpMethod":"POST",
                 "Path":"/JobAggregatedHistory",
                 "RequestContentLength":122,
                 "ClientRequestId":"3b7adbd9-3519-4f28-a61c-bd89506163b8",
                 "StartTime":"2016-07-07T21:02:52.472Z",
                 "EndTime":"2016-07-07T21:02:53.456Z"
                 }
        }
        ,
        . . . .
      ]
    }

#### <a name="request-log-schema"></a><span data-ttu-id="e5973-169">Request log schema</span><span class="sxs-lookup"><span data-stu-id="e5973-169">Request log schema</span></span>

| <span data-ttu-id="e5973-170">Name</span><span class="sxs-lookup"><span data-stu-id="e5973-170">Name</span></span> | <span data-ttu-id="e5973-171">Type</span><span class="sxs-lookup"><span data-stu-id="e5973-171">Type</span></span> | <span data-ttu-id="e5973-172">Description</span><span class="sxs-lookup"><span data-stu-id="e5973-172">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e5973-173">time</span><span class="sxs-lookup"><span data-stu-id="e5973-173">time</span></span> |<span data-ttu-id="e5973-174">String</span><span class="sxs-lookup"><span data-stu-id="e5973-174">String</span></span> |<span data-ttu-id="e5973-175">The timestamp (in UTC) of the log</span><span class="sxs-lookup"><span data-stu-id="e5973-175">The timestamp (in UTC) of the log</span></span> |
| <span data-ttu-id="e5973-176">resourceId</span><span class="sxs-lookup"><span data-stu-id="e5973-176">resourceId</span></span> |<span data-ttu-id="e5973-177">String</span><span class="sxs-lookup"><span data-stu-id="e5973-177">String</span></span> |<span data-ttu-id="e5973-178">The ID of the resource that operation took place on</span><span class="sxs-lookup"><span data-stu-id="e5973-178">The ID of the resource that operation took place on</span></span> |
| <span data-ttu-id="e5973-179">category</span><span class="sxs-lookup"><span data-stu-id="e5973-179">category</span></span> |<span data-ttu-id="e5973-180">String</span><span class="sxs-lookup"><span data-stu-id="e5973-180">String</span></span> |<span data-ttu-id="e5973-181">The log category.</span><span class="sxs-lookup"><span data-stu-id="e5973-181">The log category.</span></span> <span data-ttu-id="e5973-182">For example, **Requests**.</span><span class="sxs-lookup"><span data-stu-id="e5973-182">For example, **Requests**.</span></span> |
| <span data-ttu-id="e5973-183">operationName</span><span class="sxs-lookup"><span data-stu-id="e5973-183">operationName</span></span> |<span data-ttu-id="e5973-184">String</span><span class="sxs-lookup"><span data-stu-id="e5973-184">String</span></span> |<span data-ttu-id="e5973-185">Name of the operation that is logged.</span><span class="sxs-lookup"><span data-stu-id="e5973-185">Name of the operation that is logged.</span></span> <span data-ttu-id="e5973-186">For example, GetAggregatedJobHistory.</span><span class="sxs-lookup"><span data-stu-id="e5973-186">For example, GetAggregatedJobHistory.</span></span> |
| <span data-ttu-id="e5973-187">resultType</span><span class="sxs-lookup"><span data-stu-id="e5973-187">resultType</span></span> |<span data-ttu-id="e5973-188">String</span><span class="sxs-lookup"><span data-stu-id="e5973-188">String</span></span> |<span data-ttu-id="e5973-189">The status of the operation, For example, 200.</span><span class="sxs-lookup"><span data-stu-id="e5973-189">The status of the operation, For example, 200.</span></span> |
| <span data-ttu-id="e5973-190">callerIpAddress</span><span class="sxs-lookup"><span data-stu-id="e5973-190">callerIpAddress</span></span> |<span data-ttu-id="e5973-191">String</span><span class="sxs-lookup"><span data-stu-id="e5973-191">String</span></span> |<span data-ttu-id="e5973-192">The IP address of the client making the request</span><span class="sxs-lookup"><span data-stu-id="e5973-192">The IP address of the client making the request</span></span> |
| <span data-ttu-id="e5973-193">correlationId</span><span class="sxs-lookup"><span data-stu-id="e5973-193">correlationId</span></span> |<span data-ttu-id="e5973-194">String</span><span class="sxs-lookup"><span data-stu-id="e5973-194">String</span></span> |<span data-ttu-id="e5973-195">The id of the log.</span><span class="sxs-lookup"><span data-stu-id="e5973-195">The id of the log.</span></span> <span data-ttu-id="e5973-196">This value can be used to group a set of related log entries</span><span class="sxs-lookup"><span data-stu-id="e5973-196">This value can be used to group a set of related log entries</span></span> |
| <span data-ttu-id="e5973-197">identity</span><span class="sxs-lookup"><span data-stu-id="e5973-197">identity</span></span> |<span data-ttu-id="e5973-198">Object</span><span class="sxs-lookup"><span data-stu-id="e5973-198">Object</span></span> |<span data-ttu-id="e5973-199">The identity that generated the log</span><span class="sxs-lookup"><span data-stu-id="e5973-199">The identity that generated the log</span></span> |
| <span data-ttu-id="e5973-200">properties</span><span class="sxs-lookup"><span data-stu-id="e5973-200">properties</span></span> |<span data-ttu-id="e5973-201">JSON</span><span class="sxs-lookup"><span data-stu-id="e5973-201">JSON</span></span> |<span data-ttu-id="e5973-202">See the next section (Request log properties schema) for details</span><span class="sxs-lookup"><span data-stu-id="e5973-202">See the next section (Request log properties schema) for details</span></span> |

#### <a name="request-log-properties-schema"></a><span data-ttu-id="e5973-203">Request log properties schema</span><span class="sxs-lookup"><span data-stu-id="e5973-203">Request log properties schema</span></span>

| <span data-ttu-id="e5973-204">Name</span><span class="sxs-lookup"><span data-stu-id="e5973-204">Name</span></span> | <span data-ttu-id="e5973-205">Type</span><span class="sxs-lookup"><span data-stu-id="e5973-205">Type</span></span> | <span data-ttu-id="e5973-206">Description</span><span class="sxs-lookup"><span data-stu-id="e5973-206">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e5973-207">HttpMethod</span><span class="sxs-lookup"><span data-stu-id="e5973-207">HttpMethod</span></span> |<span data-ttu-id="e5973-208">String</span><span class="sxs-lookup"><span data-stu-id="e5973-208">String</span></span> |<span data-ttu-id="e5973-209">The HTTP Method used for the operation.</span><span class="sxs-lookup"><span data-stu-id="e5973-209">The HTTP Method used for the operation.</span></span> <span data-ttu-id="e5973-210">For example, GET.</span><span class="sxs-lookup"><span data-stu-id="e5973-210">For example, GET.</span></span> |
| <span data-ttu-id="e5973-211">Path</span><span class="sxs-lookup"><span data-stu-id="e5973-211">Path</span></span> |<span data-ttu-id="e5973-212">String</span><span class="sxs-lookup"><span data-stu-id="e5973-212">String</span></span> |<span data-ttu-id="e5973-213">The path the operation was performed on</span><span class="sxs-lookup"><span data-stu-id="e5973-213">The path the operation was performed on</span></span> |
| <span data-ttu-id="e5973-214">RequestContentLength</span><span class="sxs-lookup"><span data-stu-id="e5973-214">RequestContentLength</span></span> |<span data-ttu-id="e5973-215">int</span><span class="sxs-lookup"><span data-stu-id="e5973-215">int</span></span> |<span data-ttu-id="e5973-216">The content length of the HTTP request</span><span class="sxs-lookup"><span data-stu-id="e5973-216">The content length of the HTTP request</span></span> |
| <span data-ttu-id="e5973-217">ClientRequestId</span><span class="sxs-lookup"><span data-stu-id="e5973-217">ClientRequestId</span></span> |<span data-ttu-id="e5973-218">String</span><span class="sxs-lookup"><span data-stu-id="e5973-218">String</span></span> |<span data-ttu-id="e5973-219">The Id that uniquely identifies this request</span><span class="sxs-lookup"><span data-stu-id="e5973-219">The Id that uniquely identifies this request</span></span> |
| <span data-ttu-id="e5973-220">StartTime</span><span class="sxs-lookup"><span data-stu-id="e5973-220">StartTime</span></span> |<span data-ttu-id="e5973-221">String</span><span class="sxs-lookup"><span data-stu-id="e5973-221">String</span></span> |<span data-ttu-id="e5973-222">The time at which the server received the request</span><span class="sxs-lookup"><span data-stu-id="e5973-222">The time at which the server received the request</span></span> |
| <span data-ttu-id="e5973-223">EndTime</span><span class="sxs-lookup"><span data-stu-id="e5973-223">EndTime</span></span> |<span data-ttu-id="e5973-224">String</span><span class="sxs-lookup"><span data-stu-id="e5973-224">String</span></span> |<span data-ttu-id="e5973-225">The time at which the server sent a response</span><span class="sxs-lookup"><span data-stu-id="e5973-225">The time at which the server sent a response</span></span> |

### <a name="audit-logs"></a><span data-ttu-id="e5973-226">Audit logs</span><span class="sxs-lookup"><span data-stu-id="e5973-226">Audit logs</span></span>

<span data-ttu-id="e5973-227">Here's a sample entry in the JSON-formatted audit log.</span><span class="sxs-lookup"><span data-stu-id="e5973-227">Here's a sample entry in the JSON-formatted audit log.</span></span> <span data-ttu-id="e5973-228">Each blob has one root object called **records** that contains an array of log objects</span><span class="sxs-lookup"><span data-stu-id="e5973-228">Each blob has one root object called **records** that contains an array of log objects</span></span>

    {
    "records":
      [        
        . . . .
        ,
        {
             "time": "2016-07-28T19:15:16.245Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/<data_lake_ANALYTICS_account_name>",
             "category": "Audit",
             "operationName": "JobSubmitted",
             "identity": "user@somewhere.com",
             "properties": {
                 "JobId":"D74B928F-5194-4E6C-971F-C27026C290E6",
                 "JobName": "New Job",
                 "JobRuntimeName": "default",
                 "SubmitTime": "7/28/2016 7:14:57 PM"
                 }
        }
        ,
        . . . .
      ]
    }

#### <a name="audit-log-schema"></a><span data-ttu-id="e5973-229">Audit log schema</span><span class="sxs-lookup"><span data-stu-id="e5973-229">Audit log schema</span></span>

| <span data-ttu-id="e5973-230">Name</span><span class="sxs-lookup"><span data-stu-id="e5973-230">Name</span></span> | <span data-ttu-id="e5973-231">Type</span><span class="sxs-lookup"><span data-stu-id="e5973-231">Type</span></span> | <span data-ttu-id="e5973-232">Description</span><span class="sxs-lookup"><span data-stu-id="e5973-232">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e5973-233">time</span><span class="sxs-lookup"><span data-stu-id="e5973-233">time</span></span> |<span data-ttu-id="e5973-234">String</span><span class="sxs-lookup"><span data-stu-id="e5973-234">String</span></span> |<span data-ttu-id="e5973-235">The timestamp (in UTC) of the log</span><span class="sxs-lookup"><span data-stu-id="e5973-235">The timestamp (in UTC) of the log</span></span> |
| <span data-ttu-id="e5973-236">resourceId</span><span class="sxs-lookup"><span data-stu-id="e5973-236">resourceId</span></span> |<span data-ttu-id="e5973-237">String</span><span class="sxs-lookup"><span data-stu-id="e5973-237">String</span></span> |<span data-ttu-id="e5973-238">The ID of the resource that operation took place on</span><span class="sxs-lookup"><span data-stu-id="e5973-238">The ID of the resource that operation took place on</span></span> |
| <span data-ttu-id="e5973-239">category</span><span class="sxs-lookup"><span data-stu-id="e5973-239">category</span></span> |<span data-ttu-id="e5973-240">String</span><span class="sxs-lookup"><span data-stu-id="e5973-240">String</span></span> |<span data-ttu-id="e5973-241">The log category.</span><span class="sxs-lookup"><span data-stu-id="e5973-241">The log category.</span></span> <span data-ttu-id="e5973-242">For example, **Audit**.</span><span class="sxs-lookup"><span data-stu-id="e5973-242">For example, **Audit**.</span></span> |
| <span data-ttu-id="e5973-243">operationName</span><span class="sxs-lookup"><span data-stu-id="e5973-243">operationName</span></span> |<span data-ttu-id="e5973-244">String</span><span class="sxs-lookup"><span data-stu-id="e5973-244">String</span></span> |<span data-ttu-id="e5973-245">Name of the operation that is logged.</span><span class="sxs-lookup"><span data-stu-id="e5973-245">Name of the operation that is logged.</span></span> <span data-ttu-id="e5973-246">For example, JobSubmitted.</span><span class="sxs-lookup"><span data-stu-id="e5973-246">For example, JobSubmitted.</span></span> |
| <span data-ttu-id="e5973-247">resultType</span><span class="sxs-lookup"><span data-stu-id="e5973-247">resultType</span></span> |<span data-ttu-id="e5973-248">String</span><span class="sxs-lookup"><span data-stu-id="e5973-248">String</span></span> |<span data-ttu-id="e5973-249">A substatus for the job status (operationName).</span><span class="sxs-lookup"><span data-stu-id="e5973-249">A substatus for the job status (operationName).</span></span> |
| <span data-ttu-id="e5973-250">resultSignature</span><span class="sxs-lookup"><span data-stu-id="e5973-250">resultSignature</span></span> |<span data-ttu-id="e5973-251">String</span><span class="sxs-lookup"><span data-stu-id="e5973-251">String</span></span> |<span data-ttu-id="e5973-252">Additional details on the job status (operationName).</span><span class="sxs-lookup"><span data-stu-id="e5973-252">Additional details on the job status (operationName).</span></span> |
| <span data-ttu-id="e5973-253">identity</span><span class="sxs-lookup"><span data-stu-id="e5973-253">identity</span></span> |<span data-ttu-id="e5973-254">String</span><span class="sxs-lookup"><span data-stu-id="e5973-254">String</span></span> |<span data-ttu-id="e5973-255">The user that requested the operation.</span><span class="sxs-lookup"><span data-stu-id="e5973-255">The user that requested the operation.</span></span> <span data-ttu-id="e5973-256">For example, susan@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="e5973-256">For example, susan@contoso.com.</span></span> |
| <span data-ttu-id="e5973-257">properties</span><span class="sxs-lookup"><span data-stu-id="e5973-257">properties</span></span> |<span data-ttu-id="e5973-258">JSON</span><span class="sxs-lookup"><span data-stu-id="e5973-258">JSON</span></span> |<span data-ttu-id="e5973-259">See the next section (Audit log properties schema) for details</span><span class="sxs-lookup"><span data-stu-id="e5973-259">See the next section (Audit log properties schema) for details</span></span> |

> [!NOTE]
> <span data-ttu-id="e5973-260">**resultType** and **resultSignature** provide information on the result of an operation, and only contain a value if an operation has completed.</span><span class="sxs-lookup"><span data-stu-id="e5973-260">**resultType** and **resultSignature** provide information on the result of an operation, and only contain a value if an operation has completed.</span></span> <span data-ttu-id="e5973-261">For example, they contain a value when **operationName** contains a value of **JobStarted** or **JobEnded**.</span><span class="sxs-lookup"><span data-stu-id="e5973-261">For example, they contain a value when **operationName** contains a value of **JobStarted** or **JobEnded**.</span></span>
>
>

#### <a name="audit-log-properties-schema"></a><span data-ttu-id="e5973-262">Audit log properties schema</span><span class="sxs-lookup"><span data-stu-id="e5973-262">Audit log properties schema</span></span>

| <span data-ttu-id="e5973-263">Name</span><span class="sxs-lookup"><span data-stu-id="e5973-263">Name</span></span> | <span data-ttu-id="e5973-264">Type</span><span class="sxs-lookup"><span data-stu-id="e5973-264">Type</span></span> | <span data-ttu-id="e5973-265">Description</span><span class="sxs-lookup"><span data-stu-id="e5973-265">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e5973-266">JobId</span><span class="sxs-lookup"><span data-stu-id="e5973-266">JobId</span></span> |<span data-ttu-id="e5973-267">String</span><span class="sxs-lookup"><span data-stu-id="e5973-267">String</span></span> |<span data-ttu-id="e5973-268">The ID assigned to the job</span><span class="sxs-lookup"><span data-stu-id="e5973-268">The ID assigned to the job</span></span> |
| <span data-ttu-id="e5973-269">JobName</span><span class="sxs-lookup"><span data-stu-id="e5973-269">JobName</span></span> |<span data-ttu-id="e5973-270">String</span><span class="sxs-lookup"><span data-stu-id="e5973-270">String</span></span> |<span data-ttu-id="e5973-271">The name that was provided for the job</span><span class="sxs-lookup"><span data-stu-id="e5973-271">The name that was provided for the job</span></span> |
| <span data-ttu-id="e5973-272">JobRunTime</span><span class="sxs-lookup"><span data-stu-id="e5973-272">JobRunTime</span></span> |<span data-ttu-id="e5973-273">String</span><span class="sxs-lookup"><span data-stu-id="e5973-273">String</span></span> |<span data-ttu-id="e5973-274">The runtime used to process the job</span><span class="sxs-lookup"><span data-stu-id="e5973-274">The runtime used to process the job</span></span> |
| <span data-ttu-id="e5973-275">SubmitTime</span><span class="sxs-lookup"><span data-stu-id="e5973-275">SubmitTime</span></span> |<span data-ttu-id="e5973-276">String</span><span class="sxs-lookup"><span data-stu-id="e5973-276">String</span></span> |<span data-ttu-id="e5973-277">The time (in UTC) that the job was submitted</span><span class="sxs-lookup"><span data-stu-id="e5973-277">The time (in UTC) that the job was submitted</span></span> |
| <span data-ttu-id="e5973-278">StartTime</span><span class="sxs-lookup"><span data-stu-id="e5973-278">StartTime</span></span> |<span data-ttu-id="e5973-279">String</span><span class="sxs-lookup"><span data-stu-id="e5973-279">String</span></span> |<span data-ttu-id="e5973-280">The time the job started running after submission (in UTC).</span><span class="sxs-lookup"><span data-stu-id="e5973-280">The time the job started running after submission (in UTC).</span></span> |
| <span data-ttu-id="e5973-281">EndTime</span><span class="sxs-lookup"><span data-stu-id="e5973-281">EndTime</span></span> |<span data-ttu-id="e5973-282">String</span><span class="sxs-lookup"><span data-stu-id="e5973-282">String</span></span> |<span data-ttu-id="e5973-283">The time the job ended.</span><span class="sxs-lookup"><span data-stu-id="e5973-283">The time the job ended.</span></span> |
| <span data-ttu-id="e5973-284">Parallelism</span><span class="sxs-lookup"><span data-stu-id="e5973-284">Parallelism</span></span> |<span data-ttu-id="e5973-285">String</span><span class="sxs-lookup"><span data-stu-id="e5973-285">String</span></span> |<span data-ttu-id="e5973-286">The number of Data Lake Analytics units requested for this job during submission.</span><span class="sxs-lookup"><span data-stu-id="e5973-286">The number of Data Lake Analytics units requested for this job during submission.</span></span> |

> [!NOTE]
> <span data-ttu-id="e5973-287">**SubmitTime**, **StartTime**, **EndTime** and **Parallelism** provide information on an operation, and only contain a value if an operation has started or completed.</span><span class="sxs-lookup"><span data-stu-id="e5973-287">**SubmitTime**, **StartTime**, **EndTime** and **Parallelism** provide information on an operation, and only contain a value if an operation has started or completed.</span></span> <span data-ttu-id="e5973-288">For example, **SubmitTime** contains a value after **operationName** indicates **JobSubmitted**.</span><span class="sxs-lookup"><span data-stu-id="e5973-288">For example, **SubmitTime** contains a value after **operationName** indicates **JobSubmitted**.</span></span>

## <a name="process-the-log-data"></a><span data-ttu-id="e5973-289">Process the log data</span><span class="sxs-lookup"><span data-stu-id="e5973-289">Process the log data</span></span>

<span data-ttu-id="e5973-290">Azure Data Lake Analytics provides a sample on how to process and analyze the log data.</span><span class="sxs-lookup"><span data-stu-id="e5973-290">Azure Data Lake Analytics provides a sample on how to process and analyze the log data.</span></span> <span data-ttu-id="e5973-291">You can find the sample at [https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample](https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample).</span><span class="sxs-lookup"><span data-stu-id="e5973-291">You can find the sample at [https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample](https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e5973-292">Next steps</span><span class="sxs-lookup"><span data-stu-id="e5973-292">Next steps</span></span>
* [<span data-ttu-id="e5973-293">Overview of Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="e5973-293">Overview of Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)





