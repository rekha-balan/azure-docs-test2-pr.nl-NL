---
title: Import your data to Analytics in Azure Application Insights | Microsoft Docs
description: Import static data to join with app telemetry, or import a separate data stream to query with Analytics.
services: application-insights
documentationcenter: ''
author: alancameronwills
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: awills
ms.openlocfilehash: ade1a02efeddbfdbeb70912bb6e98e496c65b84d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551649"
---
# <a name="import-data-into-analytics"></a><span data-ttu-id="65e64-103">Import data into Analytics</span><span class="sxs-lookup"><span data-stu-id="65e64-103">Import data into Analytics</span></span>

<span data-ttu-id="65e64-104">Import any tabular data into [Analytics](app-insights-analytics.md), either to join it with [Application Insights](app-insights-overview.md) telemetry from your app, or so that you can analyze it as a separate stream.</span><span class="sxs-lookup"><span data-stu-id="65e64-104">Import any tabular data into [Analytics](app-insights-analytics.md), either to join it with [Application Insights](app-insights-overview.md) telemetry from your app, or so that you can analyze it as a separate stream.</span></span> <span data-ttu-id="65e64-105">Analytics is a powerful query language well-suited to analyzing high-volume timestamped streams of telemetry.</span><span class="sxs-lookup"><span data-stu-id="65e64-105">Analytics is a powerful query language well-suited to analyzing high-volume timestamped streams of telemetry.</span></span>

<span data-ttu-id="65e64-106">You can import data into Analytics using your own schema.</span><span class="sxs-lookup"><span data-stu-id="65e64-106">You can import data into Analytics using your own schema.</span></span> <span data-ttu-id="65e64-107">It doesn't have to use the standard Application Insights schemas such as request or trace.</span><span class="sxs-lookup"><span data-stu-id="65e64-107">It doesn't have to use the standard Application Insights schemas such as request or trace.</span></span>

<span data-ttu-id="65e64-108">You can import JSON or DSV (delimiter-separated values - comma, semicolon or tab) files.</span><span class="sxs-lookup"><span data-stu-id="65e64-108">You can import JSON or DSV (delimiter-separated values - comma, semicolon or tab) files.</span></span>

<span data-ttu-id="65e64-109">There are three situations where importing to Analytics is useful:</span><span class="sxs-lookup"><span data-stu-id="65e64-109">There are three situations where importing to Analytics is useful:</span></span>

* <span data-ttu-id="65e64-110">**Join with app telemetry.**</span><span class="sxs-lookup"><span data-stu-id="65e64-110">**Join with app telemetry.**</span></span> <span data-ttu-id="65e64-111">For example, you could import a table that maps URLs from your website to more readable page titles.</span><span class="sxs-lookup"><span data-stu-id="65e64-111">For example, you could import a table that maps URLs from your website to more readable page titles.</span></span> <span data-ttu-id="65e64-112">In Analytics, you can create a dashboard chart report that shows the ten most popular pages in your website.</span><span class="sxs-lookup"><span data-stu-id="65e64-112">In Analytics, you can create a dashboard chart report that shows the ten most popular pages in your website.</span></span> <span data-ttu-id="65e64-113">Now it can show the page titles instead of the URLs.</span><span class="sxs-lookup"><span data-stu-id="65e64-113">Now it can show the page titles instead of the URLs.</span></span>
* <span data-ttu-id="65e64-114">**Correlate your application telemetry** with other sources such as network traffic, server data, or CDN log files.</span><span class="sxs-lookup"><span data-stu-id="65e64-114">**Correlate your application telemetry** with other sources such as network traffic, server data, or CDN log files.</span></span>
* <span data-ttu-id="65e64-115">**Apply Analytics to a separate data stream.**</span><span class="sxs-lookup"><span data-stu-id="65e64-115">**Apply Analytics to a separate data stream.**</span></span> <span data-ttu-id="65e64-116">Application Insights Analytics is a powerful tool, that works well with sparse, timestamped streams - much better than SQL in many cases.</span><span class="sxs-lookup"><span data-stu-id="65e64-116">Application Insights Analytics is a powerful tool, that works well with sparse, timestamped streams - much better than SQL in many cases.</span></span> <span data-ttu-id="65e64-117">If you have such a stream from some other source, you can analyze it with Analytics.</span><span class="sxs-lookup"><span data-stu-id="65e64-117">If you have such a stream from some other source, you can analyze it with Analytics.</span></span>

<span data-ttu-id="65e64-118">Sending data to your data source is easy.</span><span class="sxs-lookup"><span data-stu-id="65e64-118">Sending data to your data source is easy.</span></span> 

1. <span data-ttu-id="65e64-119">(One time) Define the schema of your data in a 'data source'.</span><span class="sxs-lookup"><span data-stu-id="65e64-119">(One time) Define the schema of your data in a 'data source'.</span></span>
2. <span data-ttu-id="65e64-120">(Periodically) Upload your data to Azure storage, and call the REST API to notify us that new data is waiting for ingestion.</span><span class="sxs-lookup"><span data-stu-id="65e64-120">(Periodically) Upload your data to Azure storage, and call the REST API to notify us that new data is waiting for ingestion.</span></span> <span data-ttu-id="65e64-121">Within a few minutes, the data is available for query in Analytics.</span><span class="sxs-lookup"><span data-stu-id="65e64-121">Within a few minutes, the data is available for query in Analytics.</span></span>

<span data-ttu-id="65e64-122">The frequency of the upload is defined by you and how fast would you like your data to be available for queries.</span><span class="sxs-lookup"><span data-stu-id="65e64-122">The frequency of the upload is defined by you and how fast would you like your data to be available for queries.</span></span> <span data-ttu-id="65e64-123">It is more efficient to upload data in larger chunks, but not larger than 1GB.</span><span class="sxs-lookup"><span data-stu-id="65e64-123">It is more efficient to upload data in larger chunks, but not larger than 1GB.</span></span>

> [!NOTE]
> <span data-ttu-id="65e64-124">*Got lots of data sources to analyze?*</span><span class="sxs-lookup"><span data-stu-id="65e64-124">*Got lots of data sources to analyze?*</span></span> [<span data-ttu-id="65e64-125">*Consider using* logstash *to ship your data into Application Insights.*</span><span class="sxs-lookup"><span data-stu-id="65e64-125">*Consider using* logstash *to ship your data into Application Insights.*</span></span>](https://github.com/Microsoft/logstash-output-application-insights)
> 

## <a name="before-you-start"></a><span data-ttu-id="65e64-126">Before you start</span><span class="sxs-lookup"><span data-stu-id="65e64-126">Before you start</span></span>

<span data-ttu-id="65e64-127">You need:</span><span class="sxs-lookup"><span data-stu-id="65e64-127">You need:</span></span>

1. <span data-ttu-id="65e64-128">An Application Insights resource in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="65e64-128">An Application Insights resource in Microsoft Azure.</span></span>

 * <span data-ttu-id="65e64-129">If you want to analyze your data separately from any other telemetry, [create a new Application Insights resource](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="65e64-129">If you want to analyze your data separately from any other telemetry, [create a new Application Insights resource](app-insights-create-new-resource.md).</span></span>
 * <span data-ttu-id="65e64-130">If you're joining or comparing your data with telemetry from an app that is already set up with Application Insights, then you can use the resource for that app.</span><span class="sxs-lookup"><span data-stu-id="65e64-130">If you're joining or comparing your data with telemetry from an app that is already set up with Application Insights, then you can use the resource for that app.</span></span>
 * <span data-ttu-id="65e64-131">Contributor or owner access to that resource.</span><span class="sxs-lookup"><span data-stu-id="65e64-131">Contributor or owner access to that resource.</span></span>
 
2. <span data-ttu-id="65e64-132">Azure storage.</span><span class="sxs-lookup"><span data-stu-id="65e64-132">Azure storage.</span></span> <span data-ttu-id="65e64-133">You upload to Azure storage, and Analytics gets your data from there.</span><span class="sxs-lookup"><span data-stu-id="65e64-133">You upload to Azure storage, and Analytics gets your data from there.</span></span> 

 * <span data-ttu-id="65e64-134">We recommend you create a dedicated storage account for your blobs.</span><span class="sxs-lookup"><span data-stu-id="65e64-134">We recommend you create a dedicated storage account for your blobs.</span></span> <span data-ttu-id="65e64-135">If your blobs are shared with other processes, it takes longer for our processes to read your blobs.</span><span class="sxs-lookup"><span data-stu-id="65e64-135">If your blobs are shared with other processes, it takes longer for our processes to read your blobs.</span></span>

2. <span data-ttu-id="65e64-136">While this feature is in preview, you must ask for access.</span><span class="sxs-lookup"><span data-stu-id="65e64-136">While this feature is in preview, you must ask for access.</span></span>

 * <span data-ttu-id="65e64-137">From your Application Insights resource in the [Azure portal](https://portal.azure.com), open Analytics.</span><span class="sxs-lookup"><span data-stu-id="65e64-137">From your Application Insights resource in the [Azure portal](https://portal.azure.com), open Analytics.</span></span> 
 * <span data-ttu-id="65e64-138">At the bottom of the schema pane, click the 'Contact us' link under **Other Data Sources.**</span><span class="sxs-lookup"><span data-stu-id="65e64-138">At the bottom of the schema pane, click the 'Contact us' link under **Other Data Sources.**</span></span> 
 * <span data-ttu-id="65e64-139">If you see 'Add data source', then you already have access.</span><span class="sxs-lookup"><span data-stu-id="65e64-139">If you see 'Add data source', then you already have access.</span></span>


## <a name="define-your-schema"></a><span data-ttu-id="65e64-140">Define your schema</span><span class="sxs-lookup"><span data-stu-id="65e64-140">Define your schema</span></span>

<span data-ttu-id="65e64-141">Before you can import data, you must define a *data source,* which specifies the schema of your data.</span><span class="sxs-lookup"><span data-stu-id="65e64-141">Before you can import data, you must define a *data source,* which specifies the schema of your data.</span></span>
<span data-ttu-id="65e64-142">You can have up to 50 data sources in a single Application Insights resource</span><span class="sxs-lookup"><span data-stu-id="65e64-142">You can have up to 50 data sources in a single Application Insights resource</span></span>

1. <span data-ttu-id="65e64-143">Start the data source wizard.</span><span class="sxs-lookup"><span data-stu-id="65e64-143">Start the data source wizard.</span></span>

    ![Add new data source](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-analytics-import/add-new-data-source.png)

    <span data-ttu-id="65e64-145">Provide a name for your new data source.</span><span class="sxs-lookup"><span data-stu-id="65e64-145">Provide a name for your new data source.</span></span>

2. <span data-ttu-id="65e64-146">Define format of the files that you will upload.</span><span class="sxs-lookup"><span data-stu-id="65e64-146">Define format of the files that you will upload.</span></span>

    <span data-ttu-id="65e64-147">You can either define the format manually, or upload a sample file.</span><span class="sxs-lookup"><span data-stu-id="65e64-147">You can either define the format manually, or upload a sample file.</span></span>

    <span data-ttu-id="65e64-148">If the data is in CSV format, the first row of the sample can be column headers.</span><span class="sxs-lookup"><span data-stu-id="65e64-148">If the data is in CSV format, the first row of the sample can be column headers.</span></span> <span data-ttu-id="65e64-149">You can change the field names in the next step.</span><span class="sxs-lookup"><span data-stu-id="65e64-149">You can change the field names in the next step.</span></span>

    <span data-ttu-id="65e64-150">The sample should include at least 10 rows or records of data.</span><span class="sxs-lookup"><span data-stu-id="65e64-150">The sample should include at least 10 rows or records of data.</span></span>

    <span data-ttu-id="65e64-151">Column or field names should have alphanumeric names (without spaces or punctuation).</span><span class="sxs-lookup"><span data-stu-id="65e64-151">Column or field names should have alphanumeric names (without spaces or punctuation).</span></span>

    ![Upload a sample file](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-analytics-import/sample-data-file.png)


3. <span data-ttu-id="65e64-153">Review the schema that the wizard has got.</span><span class="sxs-lookup"><span data-stu-id="65e64-153">Review the schema that the wizard has got.</span></span> <span data-ttu-id="65e64-154">If it inferred the types from a sample, you might need to adjust the inferred types of the columns.</span><span class="sxs-lookup"><span data-stu-id="65e64-154">If it inferred the types from a sample, you might need to adjust the inferred types of the columns.</span></span>

    ![Review the inferred schema](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-analytics-import/data-source-review-schema.png)

 * <span data-ttu-id="65e64-156">(Optional.) Upload a schema definition.</span><span class="sxs-lookup"><span data-stu-id="65e64-156">(Optional.) Upload a schema definition.</span></span> <span data-ttu-id="65e64-157">See the format below.</span><span class="sxs-lookup"><span data-stu-id="65e64-157">See the format below.</span></span>

 * <span data-ttu-id="65e64-158">Select a Timestamp.</span><span class="sxs-lookup"><span data-stu-id="65e64-158">Select a Timestamp.</span></span> <span data-ttu-id="65e64-159">All data in Analytics must have a timestamp field.</span><span class="sxs-lookup"><span data-stu-id="65e64-159">All data in Analytics must have a timestamp field.</span></span> <span data-ttu-id="65e64-160">It must have type `datetime`, but it doesn't have to be named 'timestamp'.</span><span class="sxs-lookup"><span data-stu-id="65e64-160">It must have type `datetime`, but it doesn't have to be named 'timestamp'.</span></span> <span data-ttu-id="65e64-161">If your data has a column containing a date and time in ISO format, choose this as the timestamp column.</span><span class="sxs-lookup"><span data-stu-id="65e64-161">If your data has a column containing a date and time in ISO format, choose this as the timestamp column.</span></span> <span data-ttu-id="65e64-162">Otherwise, choose "as data arrived", and the import process will add a timestamp field.</span><span class="sxs-lookup"><span data-stu-id="65e64-162">Otherwise, choose "as data arrived", and the import process will add a timestamp field.</span></span>

5. <span data-ttu-id="65e64-163">Create the data source.</span><span class="sxs-lookup"><span data-stu-id="65e64-163">Create the data source.</span></span>

### <a name="schema-definition-file-format"></a><span data-ttu-id="65e64-164">Schema definition file format</span><span class="sxs-lookup"><span data-stu-id="65e64-164">Schema definition file format</span></span>

<span data-ttu-id="65e64-165">Instead of editing the schema in UI, you can load the schema definition from a file.</span><span class="sxs-lookup"><span data-stu-id="65e64-165">Instead of editing the schema in UI, you can load the schema definition from a file.</span></span> <span data-ttu-id="65e64-166">The schema definition format is as follows:</span><span class="sxs-lookup"><span data-stu-id="65e64-166">The schema definition format is as follows:</span></span> 

<span data-ttu-id="65e64-167">Delimited format</span><span class="sxs-lookup"><span data-stu-id="65e64-167">Delimited format</span></span> 
```
[ 
    {"location": "0", "name": "RequestName", "type": "string"}, 
    {"location": "1", "name": "timestamp", "type": "datetime"}, 
    {"location": "2", "name": "IPAddress", "type": "string"} 
] 
```

<span data-ttu-id="65e64-168">JSON format</span><span class="sxs-lookup"><span data-stu-id="65e64-168">JSON format</span></span> 
```
[ 
    {"location": "$.name", "name": "name", "type": "string"}, 
    {"location": "$.alias", "name": "alias", "type": "string"}, 
    {"location": "$.room", "name": "room", "type": "long"} 
]
```
 
<span data-ttu-id="65e64-169">Each column is identified by the location, name and type.</span><span class="sxs-lookup"><span data-stu-id="65e64-169">Each column is identified by the location, name and type.</span></span> 

* <span data-ttu-id="65e64-170">Location – For delimited file format it is the position of the mapped value.</span><span class="sxs-lookup"><span data-stu-id="65e64-170">Location – For delimited file format it is the position of the mapped value.</span></span> <span data-ttu-id="65e64-171">For JSON format, it is the jpath of the mapped key.</span><span class="sxs-lookup"><span data-stu-id="65e64-171">For JSON format, it is the jpath of the mapped key.</span></span>
* <span data-ttu-id="65e64-172">Name – the displayed name of the column.</span><span class="sxs-lookup"><span data-stu-id="65e64-172">Name – the displayed name of the column.</span></span>
* <span data-ttu-id="65e64-173">Type – the data type of that column.</span><span class="sxs-lookup"><span data-stu-id="65e64-173">Type – the data type of that column.</span></span>
 
<span data-ttu-id="65e64-174">In case a sample data was used and file format is delimited, the schema definition must map all columns and add new columns at the end.</span><span class="sxs-lookup"><span data-stu-id="65e64-174">In case a sample data was used and file format is delimited, the schema definition must map all columns and add new columns at the end.</span></span> 

<span data-ttu-id="65e64-175">JSON allows partial mapping of the data, therefore the schema definition of JSON format doesn’t have to map every key which is found in a sample data.</span><span class="sxs-lookup"><span data-stu-id="65e64-175">JSON allows partial mapping of the data, therefore the schema definition of JSON format doesn’t have to map every key which is found in a sample data.</span></span> <span data-ttu-id="65e64-176">It can also map columns which are not part of the sample data.</span><span class="sxs-lookup"><span data-stu-id="65e64-176">It can also map columns which are not part of the sample data.</span></span> 

## <a name="import-data"></a><span data-ttu-id="65e64-177">Import data</span><span class="sxs-lookup"><span data-stu-id="65e64-177">Import data</span></span>

<span data-ttu-id="65e64-178">To import data, you upload it to Azure storage, create an access key for it, and then make a REST API call.</span><span class="sxs-lookup"><span data-stu-id="65e64-178">To import data, you upload it to Azure storage, create an access key for it, and then make a REST API call.</span></span>

![Add new data source](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-analytics-import/analytics-upload-process.png)

<span data-ttu-id="65e64-180">You can perform the following process manually, or set up an automated system to do it at regular intervals.</span><span class="sxs-lookup"><span data-stu-id="65e64-180">You can perform the following process manually, or set up an automated system to do it at regular intervals.</span></span> <span data-ttu-id="65e64-181">You need to follow these steps for each block of data you want to import.</span><span class="sxs-lookup"><span data-stu-id="65e64-181">You need to follow these steps for each block of data you want to import.</span></span>

1. <span data-ttu-id="65e64-182">Upload the data to [Azure blob storage](../storage/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="65e64-182">Upload the data to [Azure blob storage](../storage/storage-dotnet-how-to-use-blobs.md).</span></span> 

 * <span data-ttu-id="65e64-183">Blobs can be any size up to 1GB uncompressed.</span><span class="sxs-lookup"><span data-stu-id="65e64-183">Blobs can be any size up to 1GB uncompressed.</span></span> <span data-ttu-id="65e64-184">Large blobs of hundreds of MB are ideal from a performance perspective.</span><span class="sxs-lookup"><span data-stu-id="65e64-184">Large blobs of hundreds of MB are ideal from a performance perspective.</span></span>
 * <span data-ttu-id="65e64-185">You can compress it with Gzip to improve upload time and latency for the data to be available for query.</span><span class="sxs-lookup"><span data-stu-id="65e64-185">You can compress it with Gzip to improve upload time and latency for the data to be available for query.</span></span> <span data-ttu-id="65e64-186">Use the `.gz` filename extension.</span><span class="sxs-lookup"><span data-stu-id="65e64-186">Use the `.gz` filename extension.</span></span>
 * <span data-ttu-id="65e64-187">It's best to use a separate storage account for this purpose, to avoid calls from different services slowing performance.</span><span class="sxs-lookup"><span data-stu-id="65e64-187">It's best to use a separate storage account for this purpose, to avoid calls from different services slowing performance.</span></span>
 * <span data-ttu-id="65e64-188">When sending data in high frequency, every few seconds, it is recommended to use more than one storage account, for performance reasons.</span><span class="sxs-lookup"><span data-stu-id="65e64-188">When sending data in high frequency, every few seconds, it is recommended to use more than one storage account, for performance reasons.</span></span>

 
2. <span data-ttu-id="65e64-189">[Create a Shared Access Signature key for the blob](../storage/storage-dotnet-shared-access-signature-part-2.md).</span><span class="sxs-lookup"><span data-stu-id="65e64-189">[Create a Shared Access Signature key for the blob](../storage/storage-dotnet-shared-access-signature-part-2.md).</span></span> <span data-ttu-id="65e64-190">The key should have an expiration period of one day and provide read access.</span><span class="sxs-lookup"><span data-stu-id="65e64-190">The key should have an expiration period of one day and provide read access.</span></span>
3. <span data-ttu-id="65e64-191">Make a REST call to notify Application Insights that data is waiting.</span><span class="sxs-lookup"><span data-stu-id="65e64-191">Make a REST call to notify Application Insights that data is waiting.</span></span>

 * <span data-ttu-id="65e64-192">Endpoint: `https://dc.services.visualstudio.com/v2/track`</span><span class="sxs-lookup"><span data-stu-id="65e64-192">Endpoint: `https://dc.services.visualstudio.com/v2/track`</span></span>
 * <span data-ttu-id="65e64-193">HTTP method: POST</span><span class="sxs-lookup"><span data-stu-id="65e64-193">HTTP method: POST</span></span>
 * <span data-ttu-id="65e64-194">Payload:</span><span class="sxs-lookup"><span data-stu-id="65e64-194">Payload:</span></span>

```JSON

    {
       "data": {
            "baseType":"OpenSchemaData",
            "baseData":{
               "ver":"2",
               "blobSasUri":"<Blob URI with Shared Access Key>",
               "sourceName":"<Schema ID>",
               "sourceVersion":"1.0"
             }
       },
       "ver":1,
       "name":"Microsoft.ApplicationInsights.OpenSchema",
       "time":"<DateTime>",
       "iKey":"<instrumentation key>"
    }
```

<span data-ttu-id="65e64-195">The placeholders are:</span><span class="sxs-lookup"><span data-stu-id="65e64-195">The placeholders are:</span></span>

* <span data-ttu-id="65e64-196">`Blob URI with Shared Access Key`: You get this from the procedure for creating a key.</span><span class="sxs-lookup"><span data-stu-id="65e64-196">`Blob URI with Shared Access Key`: You get this from the procedure for creating a key.</span></span> <span data-ttu-id="65e64-197">It is specific to the blob.</span><span class="sxs-lookup"><span data-stu-id="65e64-197">It is specific to the blob.</span></span>
* <span data-ttu-id="65e64-198">`Schema ID`: The schema ID generated for your defined schema.</span><span class="sxs-lookup"><span data-stu-id="65e64-198">`Schema ID`: The schema ID generated for your defined schema.</span></span> <span data-ttu-id="65e64-199">The data in this blob should conform to the schema.</span><span class="sxs-lookup"><span data-stu-id="65e64-199">The data in this blob should conform to the schema.</span></span>
* <span data-ttu-id="65e64-200">`DateTime`: The time at which the request is submitted, UTC.</span><span class="sxs-lookup"><span data-stu-id="65e64-200">`DateTime`: The time at which the request is submitted, UTC.</span></span> <span data-ttu-id="65e64-201">We accept these formats: ISO8601 (like "2016-01-01 13:45:01"); RFC822 ("Wed, 14 Dec 16 14:57:01 +0000"); RFC850 ("Wednesday, 14-Dec-16 14:57:00 UTC"); RFC1123 ("Wed, 14 Dec 2016 14:57:00 +0000").</span><span class="sxs-lookup"><span data-stu-id="65e64-201">We accept these formats: ISO8601 (like "2016-01-01 13:45:01"); RFC822 ("Wed, 14 Dec 16 14:57:01 +0000"); RFC850 ("Wednesday, 14-Dec-16 14:57:00 UTC"); RFC1123 ("Wed, 14 Dec 2016 14:57:00 +0000").</span></span>
* <span data-ttu-id="65e64-202">`Instrumentation key` of your Application Insights resource.</span><span class="sxs-lookup"><span data-stu-id="65e64-202">`Instrumentation key` of your Application Insights resource.</span></span>

<span data-ttu-id="65e64-203">The data is available in Analytics after a few minutes.</span><span class="sxs-lookup"><span data-stu-id="65e64-203">The data is available in Analytics after a few minutes.</span></span>

## <a name="error-responses"></a><span data-ttu-id="65e64-204">Error responses</span><span class="sxs-lookup"><span data-stu-id="65e64-204">Error responses</span></span>

* <span data-ttu-id="65e64-205">**400 bad request**: indicates that the request payload is invalid.</span><span class="sxs-lookup"><span data-stu-id="65e64-205">**400 bad request**: indicates that the request payload is invalid.</span></span> <span data-ttu-id="65e64-206">Check:</span><span class="sxs-lookup"><span data-stu-id="65e64-206">Check:</span></span>
 * <span data-ttu-id="65e64-207">Correct instrumentation key.</span><span class="sxs-lookup"><span data-stu-id="65e64-207">Correct instrumentation key.</span></span>
 * <span data-ttu-id="65e64-208">Valid time value.</span><span class="sxs-lookup"><span data-stu-id="65e64-208">Valid time value.</span></span> <span data-ttu-id="65e64-209">It should be the time now in UTC.</span><span class="sxs-lookup"><span data-stu-id="65e64-209">It should be the time now in UTC.</span></span>
 * <span data-ttu-id="65e64-210">Data conforms to the schema.</span><span class="sxs-lookup"><span data-stu-id="65e64-210">Data conforms to the schema.</span></span>
* <span data-ttu-id="65e64-211">**403 Forbidden**: The blob you've sent is not accessible.</span><span class="sxs-lookup"><span data-stu-id="65e64-211">**403 Forbidden**: The blob you've sent is not accessible.</span></span> <span data-ttu-id="65e64-212">Make sure that the shared access key is valid and has not expired.</span><span class="sxs-lookup"><span data-stu-id="65e64-212">Make sure that the shared access key is valid and has not expired.</span></span>
* <span data-ttu-id="65e64-213">**404 Not Found**:</span><span class="sxs-lookup"><span data-stu-id="65e64-213">**404 Not Found**:</span></span>
 * <span data-ttu-id="65e64-214">The blob doesn't exist.</span><span class="sxs-lookup"><span data-stu-id="65e64-214">The blob doesn't exist.</span></span>
 * <span data-ttu-id="65e64-215">The data source name is wrong.</span><span class="sxs-lookup"><span data-stu-id="65e64-215">The data source name is wrong.</span></span>

<span data-ttu-id="65e64-216">More detailed information is available in the response error message.</span><span class="sxs-lookup"><span data-stu-id="65e64-216">More detailed information is available in the response error message.</span></span>


## <a name="sample-code"></a><span data-ttu-id="65e64-217">Sample code</span><span class="sxs-lookup"><span data-stu-id="65e64-217">Sample code</span></span>

<span data-ttu-id="65e64-218">This code uses the [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) NuGet package.</span><span class="sxs-lookup"><span data-stu-id="65e64-218">This code uses the [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) NuGet package.</span></span>

### <a name="classes"></a><span data-ttu-id="65e64-219">Classes</span><span class="sxs-lookup"><span data-stu-id="65e64-219">Classes</span></span>

```C#


namespace IngestionClient 
{ 
    using System; 
    using Newtonsoft.Json; 

    public class AnalyticsDataSourceIngestionRequest 
    { 
        #region Members 
        private const string BaseDataRequiredVersion = "2"; 
        private const string RequestName = "Microsoft.ApplicationInsights.OpenSchema"; 
        #endregion Members 

        public AnalyticsDataSourceIngestionRequest(string ikey, string schemaId, string blobSasUri, int version = 1) 
        { 
            Ver = version; 
            IKey = ikey; 
            Data = new Data 
            { 
                BaseData = new BaseData 
                { 
                    Ver = BaseDataRequiredVersion, 
                    BlobSasUri = blobSasUri, 
                    SourceName = schemaId, 
                    SourceVersion = version.ToString() 
                } 
            }; 
        } 


        [JsonProperty("data")] 
        public Data Data { get; set; } 

        [JsonProperty("ver")] 
        public int Ver { get; set; } 

        [JsonProperty("name")] 
        public string Name { get { return RequestName; } } 

        [JsonProperty("time")] 
        public DateTime Time { get { return DateTime.UtcNow; } } 

        [JsonProperty("iKey")] 
        public string IKey { get; set; } 
    } 

    #region Internal Classes 

    public class Data 
    { 
        private const string DataBaseType = "OpenSchemaData"; 

        [JsonProperty("baseType")] 
        public string BaseType 
        { 
            get { return DataBaseType; } 
        } 

        [JsonProperty("baseData")] 
        public BaseData BaseData { get; set; } 
    } 


    public class BaseData 
    { 
        [JsonProperty("ver")] 
        public string Ver { get; set; } 

        [JsonProperty("blobSasUri")] 
        public string BlobSasUri { get; set; } 

        [JsonProperty("sourceName")] 
        public string SourceName { get; set; } 

        [JsonProperty("sourceVersion")] 
        public string SourceVersion { get; set; } 
    } 

    #endregion Internal Classes 
} 


namespace IngestionClient 
{ 
    using System; 
    using System.IO; 
    using System.Net; 
    using System.Text; 
    using System.Threading.Tasks; 
    using Newtonsoft.Json; 

    public class AnalyticsDataSourceClient 
    { 
        #region Members 
        private readonly Uri endpoint = new Uri("https://dc.services.visualstudio.com/v2/track"); 
        private const string RequestContentType = "application/json; charset=UTF-8"; 
        private const string RequestAccess = "application/json"; 
        #endregion Members 

        #region Public 

        public async Task<bool> RequestBlobIngestion(AnalyticsDataSourceIngestionRequest ingestionRequest) 
        { 
            HttpWebRequest request = WebRequest.CreateHttp(endpoint); 
            request.Method = WebRequestMethods.Http.Post; 
            request.ContentType = RequestContentType; 
            request.Accept = RequestAccess; 

            string notificationJson = Serialize(ingestionRequest); 
            byte[] notificationBytes = GetContentBytes(notificationJson); 
            request.ContentLength = notificationBytes.Length; 

            Stream requestStream = request.GetRequestStream(); 
            requestStream.Write(notificationBytes, 0, notificationBytes.Length); 
            requestStream.Close(); 

            try 
            { 
                using (var response = (HttpWebResponse)await request.GetResponseAsync())
                {
                    return response.StatusCode == HttpStatusCode.OK;
                }
            } 
            catch (WebException e) 
            { 
                HttpWebResponse httpResponse = e.Response as HttpWebResponse; 
                if (httpResponse != null) 
                { 
                    Console.WriteLine( 
                        "Ingestion request failed with status code: {0}. Error: {1}", 
                        httpResponse.StatusCode, 
                        httpResponse.StatusDescription); 
                    return false; 
                }
                throw; 
            } 
        } 
        #endregion Public 

        #region Private 
        private byte[] GetContentBytes(string content) 
        { 
            return Encoding.UTF8.GetBytes(content);
        } 


        private string Serialize(AnalyticsDataSourceIngestionRequest ingestionRequest) 
        { 
            return JsonConvert.SerializeObject(ingestionRequest); 
        } 
        #endregion Private 
    } 
} 

```

### <a name="ingest-data"></a><span data-ttu-id="65e64-220">Ingest data</span><span class="sxs-lookup"><span data-stu-id="65e64-220">Ingest data</span></span>

<span data-ttu-id="65e64-221">Use this code for each blob.</span><span class="sxs-lookup"><span data-stu-id="65e64-221">Use this code for each blob.</span></span> 

```C#


   AnalyticsDataSourceClient client = new AnalyticsDataSourceClient(); 

   var ingestionRequest = new AnalyticsDataSourceIngestionRequest("iKey", "tableId/sourceId", "blobUrlWithSas"); 

   bool success = await client.RequestBlobIngestion(ingestionRequest);

```

## <a name="next-steps"></a><span data-ttu-id="65e64-222">Next steps</span><span class="sxs-lookup"><span data-stu-id="65e64-222">Next steps</span></span>

* [<span data-ttu-id="65e64-223">Tour of the Analytics query language</span><span class="sxs-lookup"><span data-stu-id="65e64-223">Tour of the Analytics query language</span></span>](app-insights-analytics-tour.md)
* [<span data-ttu-id="65e64-224">Use *Logstash* to send data to Application Insights</span><span class="sxs-lookup"><span data-stu-id="65e64-224">Use *Logstash* to send data to Application Insights</span></span>](https://github.com/Microsoft/logstash-output-application-insights)




