---
title: Use reference data and lookup tables in Stream Analytics | Microsoft Docs
description: Use reference data in a Stream Analytics query
keywords: lookup table, reference data
services: stream-analytics
documentationcenter: ''
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 06103be5-553a-4da1-8a8d-3be9ca2aff54
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: b2927931904a2169c3a84737841ee702b10123c1
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563456"
---
# <a name="using-reference-data-or-lookup-tables-in-a-stream-analytics-input-stream"></a>Using reference data or lookup tables in a Stream Analytics input stream
Reference data (also known as a lookup table) is a finite data set that is static or slowing changing in nature, used to perform a lookup or to correlate with your data stream. To make use of reference data in your Azure Stream Analytics job, you will generally use a [Reference Data Join](https://msdn.microsoft.com/library/azure/dn949258.aspx) in your Query. Stream Analytics uses Azure Blob storage as the storage layer for Reference Data, and with Azure Data Factory reference data can be transformed and/or copied to Azure Blob storage, for use as Reference Data, from [any number of cloud-based and on-premises data stores](../data-factory/data-factory-data-movement-activities.md). Reference data is modeled as a sequence of blobs (defined in the input configuration) in ascending order of the date/time specified in the blob name. It **only** supports adding to the end of the sequence by using a date/time **greater** than the one specified by the last blob in the sequence.

Stream Analytics has a **limit of 100 MB per blob** but jobs can process multiple reference blobs by using the **path pattern** property.


## <a name="configuring-reference-data"></a>Configuring reference data
To configure your reference data, you first need to create an input that is of type **Reference Data**. The table below explains each property that you will need to provide while creating the reference data input with its description:


<table>
<tbody>
<tr>
<td>Property Name</td>
<td>Description</td>
</tr>
<tr>
<td>Input Alias</td>
<td>A friendly name that will be used in the job query to reference this input.</td>
</tr>
<tr>
<td>Storage Account</td>
<td>The name of the storage account where your blobs are located. If it’s in the same subscription as your Stream Analytics Job, you can select it from the drop-down.</td>
</tr>
<tr>
<td>Storage Account Key</td>
<td>The secret key associated with the storage account. This gets automatically populated if the storage account is in the same subscription as your Stream Analytics job.</td>
</tr>
<tr>
<td>Storage Container</td>
<td>Containers provide a logical grouping for blobs stored in the Microsoft Azure Blob service. When you upload a blob to the Blob service, you must specify a container for that blob.</td>
</tr>
<tr>
<td>Path Pattern</td>
<td>The path used to locate your blobs within the specified container. Within the path, you may choose to specify one or more instances of the following 2 variables:<BR>{date}, {time}<BR>Example 1: products/{date}/{time}/product-list.csv<BR>Example 2: products/{date}/product-list.csv
</tr>
<tr>
<td>Date Format [optional]</td>
<td>If you have used {date} within the Path Pattern that you specified, then you can select the date format in which your blobs are organized from the drop-down of supported formats.<BR>Example: YYYY/MM/DD, MM/DD/YYYY, etc.</td>
</tr>
<tr>
<td>Time Format [optional]</td>
<td>If you have used {time} within the Path Pattern that you specified, then you can select the time format in which your blobs are organized from the drop-down of supported formats.<BR>Example: HH, HH/mm, or HH-mm</td>
</tr>
<tr>
<td>Event Serialization Format</td>
<td>To make sure your queries work the way you expect, Stream Analytics needs to know which serialization format you're using for incoming data streams. For Reference Data, the supported formats are CSV and JSON.</td>
</tr>
<tr>
<td>Encoding</td>
<td>UTF-8 is the only supported encoding format at this time</td>
</tr>
</tbody>
</table>

## <a name="generating-reference-data-on-a-schedule"></a>Generating reference data on a schedule
If your reference data is a slowly changing data set, then support for refreshing reference data is enabled by specifying a path pattern in the input configuration using the {date} and {time} substitution tokens. Stream Analytics picks up the updated reference data definitions based on this path pattern. For example, a pattern of `sample/{date}/{time}/products.csv` with a date format of **“YYYY-MM-DD”** and a time format of **“HH-mm”** instructs Stream Analytics to pick up the updated blob `sample/2015-04-16/17-30/products.csv` at 5:30 PM on April 16th, 2015 UTC time zone.

> [!NOTE]
> Currently Stream Analytics jobs look for the blob refresh only when the machine time advances to the time encoded in the blob name. For example, the job will look for `sample/2015-04-16/17-30/products.csv` as soon as possible but no earlier than 5:30 PM on April 16th, 2015 UTC time zone. It will *never* look for a blob with an encoded time earlier than the last one that is discovered.
> 
> E.g. once the job finds the blob `sample/2015-04-16/17-30/products.csv` it will ignore any files with an encoded date earlier than 5:30 PM April 16th, 2015 so if a late arriving `sample/2015-04-16/17-25/products.csv` blob gets created in the same container the job will not use it.
> 
> Likewise if `sample/2015-04-16/17-30/products.csv` is only produced at 10:03 PM April 16th, 2015 but no blob with an earlier date is present in the container, the job will use this file starting at 10:03 PM April 16th, 2015 and use the previous reference data until then.
> 
> An exception to this is when the job needs to re-process data back in time or when the job is first started. At start time the job is looking for the most recent blob produced before the job start time specified. This is done to ensure that there is a **non-empty** reference data set when the job starts. If one cannot be found, the job displays the following diagnostic: `Initializing input without a valid reference data blob for UTC time <start time>`.
> 
> 

[Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/) can be used to orchestrate the task of creating the updated blobs required by Stream Analytics to update reference data definitions. Data Factory is a cloud-based data integration service that orchestrates and automates the movement and transformation of data. Data Factory supports [connecting to a large number of cloud based and on-premises data stores](../data-factory/data-factory-data-movement-activities.md) and moving data easily on a regular schedule that you specify. For more information and step by step guidance on how to set up a Data Factory pipeline to generate reference data for Stream Analytics which refreshes on a pre-defined schedule, check out this [GitHub sample](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ReferenceDataRefreshForASAJobs).

## <a name="tips-on-refreshing-your-reference-data"></a>Tips on refreshing your reference data
1. Overwriting reference data blobs will not cause Stream Analytics to reload the blob and in some cases it can cause the job to fail. The recommended way to change reference data is to add a new blob using the same container and path pattern defined in the job input and use a date/time **greater** than the one specified by the last blob in the sequence.
2. Reference data blobs are **not** ordered by the blob’s “Last Modified” time but only by the time and date specified in the blob name using the {date} and {time} substitutions.
3. On a few occasions, a job must go back in time, therefore reference data blobs must not be altered or deleted.

## <a name="get-help"></a>Get help
For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Next steps
You've been introduced to Stream Analytics, a managed service for streaming analytics on data from the Internet of Things. To learn more about this service, see:

* [Get started using Azure Stream Analytics](stream-analytics-get-started.md)
* [Scale Azure Stream Analytics jobs](stream-analytics-scale-jobs.md)
* [Azure Stream Analytics Query Language Reference](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Stream Analytics Management REST API Reference](https://msdn.microsoft.com/library/azure/dn835031.aspx)

<!--Link references-->
[stream.analytics.developer.guide]: ../stream-analytics-developer-guide.md
[stream.analytics.scale.jobs]: stream-analytics-scale-jobs.md
[stream.analytics.introduction]: stream-analytics-introduction.md
[stream.analytics.get.started]: stream-analytics-get-started.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301
