---
title: Azure Stream Analytics diagnostic logs | Microsoft Docs
description: Learn how to analyze diagnostic logs from Stream Analytics jobs in Microsoft Azure.
keywords: ''
documentationcenter: ''
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: ''
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 3faf0c4e8b29b0460c0b27dfb90239f62a6d57bf
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556744"
---
# <a name="job-diagnostic-logs"></a><span data-ttu-id="7d263-103">Job diagnostic logs</span><span class="sxs-lookup"><span data-stu-id="7d263-103">Job diagnostic logs</span></span>

## <a name="introduction"></a><span data-ttu-id="7d263-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="7d263-104">Introduction</span></span>
<span data-ttu-id="7d263-105">Stream Analytics exposes two types of logs:</span><span class="sxs-lookup"><span data-stu-id="7d263-105">Stream Analytics exposes two types of logs:</span></span> 
* <span data-ttu-id="7d263-106">[Activity logs](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs) that are always enabled and provide insights into operations performed on jobs;</span><span class="sxs-lookup"><span data-stu-id="7d263-106">[Activity logs](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs) that are always enabled and provide insights into operations performed on jobs;</span></span>
* <span data-ttu-id="7d263-107">[Diagnostic logs](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs) that are configurable and provide richer insights into everything that happens with the job starting when it’s created, updated, while it’s running, and until it’s deleted.</span><span class="sxs-lookup"><span data-stu-id="7d263-107">[Diagnostic logs](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs) that are configurable and provide richer insights into everything that happens with the job starting when it’s created, updated, while it’s running, and until it’s deleted.</span></span>

> [!NOTE]
> <span data-ttu-id="7d263-108">It should be noted that the usage of services such as Azure Storage, Event Hub, and Log Analytics for analyzing non-conforming data will be charged based on the pricing model for those services.</span><span class="sxs-lookup"><span data-stu-id="7d263-108">It should be noted that the usage of services such as Azure Storage, Event Hub, and Log Analytics for analyzing non-conforming data will be charged based on the pricing model for those services.</span></span>

## <a name="how-to-enable-diagnostic-logs"></a><span data-ttu-id="7d263-109">How to enable diagnostic logs</span><span class="sxs-lookup"><span data-stu-id="7d263-109">How to enable diagnostic logs</span></span>
<span data-ttu-id="7d263-110">The diagnostics logs are turned **off** by default.</span><span class="sxs-lookup"><span data-stu-id="7d263-110">The diagnostics logs are turned **off** by default.</span></span> <span data-ttu-id="7d263-111">To enable them, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="7d263-111">To enable them, follow these steps:</span></span>

<span data-ttu-id="7d263-112">Sign on to the Azure portal and navigate to the streaming job blade.</span><span class="sxs-lookup"><span data-stu-id="7d263-112">Sign on to the Azure portal and navigate to the streaming job blade.</span></span> <span data-ttu-id="7d263-113">Then go to the "Diagnostic logs" blade under "Monitoring."</span><span class="sxs-lookup"><span data-stu-id="7d263-113">Then go to the "Diagnostic logs" blade under "Monitoring."</span></span>

![blade navigation to diagnostic logs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-job-diagnostic-logs/image1.png)  

<span data-ttu-id="7d263-115">Then click the "Turn on diagnostics" link</span><span class="sxs-lookup"><span data-stu-id="7d263-115">Then click the "Turn on diagnostics" link</span></span>

![turn on diagnostic logs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-job-diagnostic-logs/image2.png)

<span data-ttu-id="7d263-117">On the opened diagnostics, change the status to "On."</span><span class="sxs-lookup"><span data-stu-id="7d263-117">On the opened diagnostics, change the status to "On."</span></span>

![change status diagnostic logs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-job-diagnostic-logs/image3.png)

<span data-ttu-id="7d263-119">Configure the desired archival target (storage account, event hub, Log Analytics) and select the categories of logs that you want to collect (Execution, Authoring).</span><span class="sxs-lookup"><span data-stu-id="7d263-119">Configure the desired archival target (storage account, event hub, Log Analytics) and select the categories of logs that you want to collect (Execution, Authoring).</span></span> <span data-ttu-id="7d263-120">Then save the new diagnostics configuration.</span><span class="sxs-lookup"><span data-stu-id="7d263-120">Then save the new diagnostics configuration.</span></span>

<span data-ttu-id="7d263-121">Once saved the configuration takes about 10 minutes to take effect.</span><span class="sxs-lookup"><span data-stu-id="7d263-121">Once saved the configuration takes about 10 minutes to take effect.</span></span> <span data-ttu-id="7d263-122">After that, the logs will start appearing in the configured archival target (which you can see on the "Diagnostics logs" blade):</span><span class="sxs-lookup"><span data-stu-id="7d263-122">After that, the logs will start appearing in the configured archival target (which you can see on the "Diagnostics logs" blade):</span></span>

![blade navigation to diagnostic logs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-job-diagnostic-logs/image4.png)

<span data-ttu-id="7d263-124">More information about configuring diagnostics is available on the [diagnostic logs](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs) page.</span><span class="sxs-lookup"><span data-stu-id="7d263-124">More information about configuring diagnostics is available on the [diagnostic logs](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs) page.</span></span>

## <a name="diagnostic-logs-categories"></a><span data-ttu-id="7d263-125">Diagnostic logs categories</span><span class="sxs-lookup"><span data-stu-id="7d263-125">Diagnostic logs categories</span></span>
<span data-ttu-id="7d263-126">There are two categories of diagnostic logs that we currently capture:</span><span class="sxs-lookup"><span data-stu-id="7d263-126">There are two categories of diagnostic logs that we currently capture:</span></span>

* <span data-ttu-id="7d263-127">**Authoring:** capture the logs related to job authoring operations: creation, adding and deleting inputs and outputs, adding and updating the query, starting and stopping the job.</span><span class="sxs-lookup"><span data-stu-id="7d263-127">**Authoring:** capture the logs related to job authoring operations: creation, adding and deleting inputs and outputs, adding and updating the query, starting and stopping the job.</span></span>
* <span data-ttu-id="7d263-128">**Execution:** capture what is happening during job execution.</span><span class="sxs-lookup"><span data-stu-id="7d263-128">**Execution:** capture what is happening during job execution.</span></span>
    * <span data-ttu-id="7d263-129">Connectivity errors;</span><span class="sxs-lookup"><span data-stu-id="7d263-129">Connectivity errors;</span></span>
    * <span data-ttu-id="7d263-130">Data processing errors;</span><span class="sxs-lookup"><span data-stu-id="7d263-130">Data processing errors;</span></span>
        * <span data-ttu-id="7d263-131">Events that don’t conform with the query definition (mismatched field types and values, missing fields etc.);</span><span class="sxs-lookup"><span data-stu-id="7d263-131">Events that don’t conform with the query definition (mismatched field types and values, missing fields etc.);</span></span>
        * <span data-ttu-id="7d263-132">Expression evaluation errors;</span><span class="sxs-lookup"><span data-stu-id="7d263-132">Expression evaluation errors;</span></span>
    * <span data-ttu-id="7d263-133">Etc.</span><span class="sxs-lookup"><span data-stu-id="7d263-133">Etc.</span></span>

## <a name="diagnostic-logs-schema"></a><span data-ttu-id="7d263-134">Diagnostic logs schema</span><span class="sxs-lookup"><span data-stu-id="7d263-134">Diagnostic logs schema</span></span>
<span data-ttu-id="7d263-135">All logs are stored in JSON format and each entry has the following common string fields:</span><span class="sxs-lookup"><span data-stu-id="7d263-135">All logs are stored in JSON format and each entry has the following common string fields:</span></span>

<span data-ttu-id="7d263-136">Name</span><span class="sxs-lookup"><span data-stu-id="7d263-136">Name</span></span> | <span data-ttu-id="7d263-137">Description</span><span class="sxs-lookup"><span data-stu-id="7d263-137">Description</span></span>
------- | -------
<span data-ttu-id="7d263-138">time</span><span class="sxs-lookup"><span data-stu-id="7d263-138">time</span></span> | <span data-ttu-id="7d263-139">The timestamp (in UTC) of the log</span><span class="sxs-lookup"><span data-stu-id="7d263-139">The timestamp (in UTC) of the log</span></span>
<span data-ttu-id="7d263-140">resourceId</span><span class="sxs-lookup"><span data-stu-id="7d263-140">resourceId</span></span> | <span data-ttu-id="7d263-141">The ID of the resource that operation took place on, upper-cased.</span><span class="sxs-lookup"><span data-stu-id="7d263-141">The ID of the resource that operation took place on, upper-cased.</span></span> <span data-ttu-id="7d263-142">It includes the subscription id, resource group, and job name.</span><span class="sxs-lookup"><span data-stu-id="7d263-142">It includes the subscription id, resource group, and job name.</span></span> <span data-ttu-id="7d263-143">For example, **/SUBSCRIPTIONS/6503D296-DAC1-4449-9B03-609A1F4A1C87/RESOURCEGROUPS/MY-RESOURCE-GROUP/PROVIDERS/MICROSOFT.STREAMANALYTICS/STREAMINGJOBS/MYSTREAMINGJOB**.</span><span class="sxs-lookup"><span data-stu-id="7d263-143">For example, **/SUBSCRIPTIONS/6503D296-DAC1-4449-9B03-609A1F4A1C87/RESOURCEGROUPS/MY-RESOURCE-GROUP/PROVIDERS/MICROSOFT.STREAMANALYTICS/STREAMINGJOBS/MYSTREAMINGJOB**.</span></span>
<span data-ttu-id="7d263-144">category</span><span class="sxs-lookup"><span data-stu-id="7d263-144">category</span></span> | <span data-ttu-id="7d263-145">The log category, either **Execution** or **Authoring**.</span><span class="sxs-lookup"><span data-stu-id="7d263-145">The log category, either **Execution** or **Authoring**.</span></span>
<span data-ttu-id="7d263-146">operationName</span><span class="sxs-lookup"><span data-stu-id="7d263-146">operationName</span></span> | <span data-ttu-id="7d263-147">Name of the operation that is logged.</span><span class="sxs-lookup"><span data-stu-id="7d263-147">Name of the operation that is logged.</span></span> <span data-ttu-id="7d263-148">For example, **Send Events: SQL Output write failure to mysqloutput**</span><span class="sxs-lookup"><span data-stu-id="7d263-148">For example, **Send Events: SQL Output write failure to mysqloutput**</span></span>
<span data-ttu-id="7d263-149">status</span><span class="sxs-lookup"><span data-stu-id="7d263-149">status</span></span> | <span data-ttu-id="7d263-150">The status of the operation.</span><span class="sxs-lookup"><span data-stu-id="7d263-150">The status of the operation.</span></span> <span data-ttu-id="7d263-151">For example, **Failed, Succeeded**.</span><span class="sxs-lookup"><span data-stu-id="7d263-151">For example, **Failed, Succeeded**.</span></span>
<span data-ttu-id="7d263-152">level</span><span class="sxs-lookup"><span data-stu-id="7d263-152">level</span></span> | <span data-ttu-id="7d263-153">Log level.</span><span class="sxs-lookup"><span data-stu-id="7d263-153">Log level.</span></span> <span data-ttu-id="7d263-154">For example, **Error, Warning, Informational**.</span><span class="sxs-lookup"><span data-stu-id="7d263-154">For example, **Error, Warning, Informational**.</span></span>
<span data-ttu-id="7d263-155">properties</span><span class="sxs-lookup"><span data-stu-id="7d263-155">properties</span></span> | <span data-ttu-id="7d263-156">log entry-specific detail; serialized as JSON string; see following for more details</span><span class="sxs-lookup"><span data-stu-id="7d263-156">log entry-specific detail; serialized as JSON string; see following for more details</span></span>

### <a name="execution-logs-properties-schema"></a><span data-ttu-id="7d263-157">Execution logs properties schema</span><span class="sxs-lookup"><span data-stu-id="7d263-157">Execution logs properties schema</span></span>
<span data-ttu-id="7d263-158">Execution logs contain information about events that happened during Stream Analytics job execution.</span><span class="sxs-lookup"><span data-stu-id="7d263-158">Execution logs contain information about events that happened during Stream Analytics job execution.</span></span>
<span data-ttu-id="7d263-159">Depending on the type of events, properties will have different schema.</span><span class="sxs-lookup"><span data-stu-id="7d263-159">Depending on the type of events, properties will have different schema.</span></span> <span data-ttu-id="7d263-160">We currently have the following types:</span><span class="sxs-lookup"><span data-stu-id="7d263-160">We currently have the following types:</span></span>

### <a name="data-errors"></a><span data-ttu-id="7d263-161">Data errors</span><span class="sxs-lookup"><span data-stu-id="7d263-161">Data errors</span></span>
<span data-ttu-id="7d263-162">Any error in processing data will fall under this category of logs.</span><span class="sxs-lookup"><span data-stu-id="7d263-162">Any error in processing data will fall under this category of logs.</span></span> <span data-ttu-id="7d263-163">Produced mainly during data read, serialization, and write operation.</span><span class="sxs-lookup"><span data-stu-id="7d263-163">Produced mainly during data read, serialization, and write operation.</span></span> <span data-ttu-id="7d263-164">It does not include connectivity errors which are treated as generic events.</span><span class="sxs-lookup"><span data-stu-id="7d263-164">It does not include connectivity errors which are treated as generic events.</span></span>

<span data-ttu-id="7d263-165">Name</span><span class="sxs-lookup"><span data-stu-id="7d263-165">Name</span></span> | <span data-ttu-id="7d263-166">Description</span><span class="sxs-lookup"><span data-stu-id="7d263-166">Description</span></span>
------- | -------
<span data-ttu-id="7d263-167">Source</span><span class="sxs-lookup"><span data-stu-id="7d263-167">Source</span></span> | <span data-ttu-id="7d263-168">Name of the job input or output where the error happened.</span><span class="sxs-lookup"><span data-stu-id="7d263-168">Name of the job input or output where the error happened.</span></span>
<span data-ttu-id="7d263-169">Message</span><span class="sxs-lookup"><span data-stu-id="7d263-169">Message</span></span> | <span data-ttu-id="7d263-170">Message associated with the error.</span><span class="sxs-lookup"><span data-stu-id="7d263-170">Message associated with the error.</span></span>
<span data-ttu-id="7d263-171">Type</span><span class="sxs-lookup"><span data-stu-id="7d263-171">Type</span></span> | <span data-ttu-id="7d263-172">The type of error.</span><span class="sxs-lookup"><span data-stu-id="7d263-172">The type of error.</span></span> <span data-ttu-id="7d263-173">For example, **DataConversionError, CsvParserError, and ServiceBusPropertyColumnMissingError**.</span><span class="sxs-lookup"><span data-stu-id="7d263-173">For example, **DataConversionError, CsvParserError, and ServiceBusPropertyColumnMissingError**.</span></span>
<span data-ttu-id="7d263-174">Data</span><span class="sxs-lookup"><span data-stu-id="7d263-174">Data</span></span> | <span data-ttu-id="7d263-175">Contains data useful to accurately locate the source of the error.</span><span class="sxs-lookup"><span data-stu-id="7d263-175">Contains data useful to accurately locate the source of the error.</span></span> <span data-ttu-id="7d263-176">Subject to truncation depending on size.</span><span class="sxs-lookup"><span data-stu-id="7d263-176">Subject to truncation depending on size.</span></span>

<span data-ttu-id="7d263-177">Depending on the **operationName** value, data errors will have the following schema:</span><span class="sxs-lookup"><span data-stu-id="7d263-177">Depending on the **operationName** value, data errors will have the following schema:</span></span>
* <span data-ttu-id="7d263-178">**Serialize Events** - happening during event read operations when the data at the input does not satisfy the query schema:</span><span class="sxs-lookup"><span data-stu-id="7d263-178">**Serialize Events** - happening during event read operations when the data at the input does not satisfy the query schema:</span></span>
    * <span data-ttu-id="7d263-179">Type mismatch during event (de)serialize: field causing the error.</span><span class="sxs-lookup"><span data-stu-id="7d263-179">Type mismatch during event (de)serialize: field causing the error.</span></span>
    * <span data-ttu-id="7d263-180">Cannot read an event, invalid serialization: information about the place in the input data where the error happened: blob name for blob input, offset and a sample of the data.</span><span class="sxs-lookup"><span data-stu-id="7d263-180">Cannot read an event, invalid serialization: information about the place in the input data where the error happened: blob name for blob input, offset and a sample of the data.</span></span>
* <span data-ttu-id="7d263-181">**Send Events** - write operations: streaming event that caused the error.</span><span class="sxs-lookup"><span data-stu-id="7d263-181">**Send Events** - write operations: streaming event that caused the error.</span></span>

### <a name="generic-events"></a><span data-ttu-id="7d263-182">Generic events</span><span class="sxs-lookup"><span data-stu-id="7d263-182">Generic events</span></span>
<span data-ttu-id="7d263-183">Everything else</span><span class="sxs-lookup"><span data-stu-id="7d263-183">Everything else</span></span>

<span data-ttu-id="7d263-184">Name</span><span class="sxs-lookup"><span data-stu-id="7d263-184">Name</span></span> | <span data-ttu-id="7d263-185">Description</span><span class="sxs-lookup"><span data-stu-id="7d263-185">Description</span></span>
-------- | --------
<span data-ttu-id="7d263-186">Error</span><span class="sxs-lookup"><span data-stu-id="7d263-186">Error</span></span> | <span data-ttu-id="7d263-187">(optional) Error information, usually exception information if available.</span><span class="sxs-lookup"><span data-stu-id="7d263-187">(optional) Error information, usually exception information if available.</span></span>
<span data-ttu-id="7d263-188">Message</span><span class="sxs-lookup"><span data-stu-id="7d263-188">Message</span></span>| <span data-ttu-id="7d263-189">Log message.</span><span class="sxs-lookup"><span data-stu-id="7d263-189">Log message.</span></span>
<span data-ttu-id="7d263-190">Type</span><span class="sxs-lookup"><span data-stu-id="7d263-190">Type</span></span> | <span data-ttu-id="7d263-191">Type of message, maps to internal categorization of errors: for example **JobValidationError, BlobOutputAdapterInitializationFailure**, etc.</span><span class="sxs-lookup"><span data-stu-id="7d263-191">Type of message, maps to internal categorization of errors: for example **JobValidationError, BlobOutputAdapterInitializationFailure**, etc.</span></span>
<span data-ttu-id="7d263-192">Correlation ID</span><span class="sxs-lookup"><span data-stu-id="7d263-192">Correlation ID</span></span> | <span data-ttu-id="7d263-193">[GUID](https://en.wikipedia.org/wiki/Universally_unique_identifier) that uniquely identifies the job execution.</span><span class="sxs-lookup"><span data-stu-id="7d263-193">[GUID](https://en.wikipedia.org/wiki/Universally_unique_identifier) that uniquely identifies the job execution.</span></span> <span data-ttu-id="7d263-194">All execution log entries produced since the job is started until it stops will have the same "Correlation ID."</span><span class="sxs-lookup"><span data-stu-id="7d263-194">All execution log entries produced since the job is started until it stops will have the same "Correlation ID."</span></span>



## <a name="next-steps"></a><span data-ttu-id="7d263-195">Next steps</span><span class="sxs-lookup"><span data-stu-id="7d263-195">Next steps</span></span>
* [<span data-ttu-id="7d263-196">Introduction to Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="7d263-196">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="7d263-197">Get started using Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="7d263-197">Get started using Azure Stream Analytics</span></span>](stream-analytics-get-started.md)
* [<span data-ttu-id="7d263-198">Scale Azure Stream Analytics jobs</span><span class="sxs-lookup"><span data-stu-id="7d263-198">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="7d263-199">Azure Stream Analytics Query Language Reference</span><span class="sxs-lookup"><span data-stu-id="7d263-199">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="7d263-200">Azure Stream Analytics Management REST API Reference</span><span class="sxs-lookup"><span data-stu-id="7d263-200">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)





