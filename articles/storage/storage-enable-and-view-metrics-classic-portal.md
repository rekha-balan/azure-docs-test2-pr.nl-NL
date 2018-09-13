---
title: Enabling storage metrics in the Azure portal | Microsoft Docs
description: How to enable storage metrics for the Blob, Queue, Table, and File services
services: storage
documentationcenter: ''
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 2fb5b229-f099-4334-92be-4e0e7dd257d7
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/03/2017
ms.author: robinsh
ms.openlocfilehash: 3c3c7924655f5b932be2a3d947a4df786fc0630d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564412"
---
# <a name="enabling-storage-metrics-and-viewing-metrics-data"></a><span data-ttu-id="3c273-103">Enabling Storage metrics and viewing metrics data</span><span class="sxs-lookup"><span data-stu-id="3c273-103">Enabling Storage metrics and viewing metrics data</span></span>
[!INCLUDE [storage-selector-portal-enable-and-view-metrics](../../includes/storage-selector-portal-enable-and-view-metrics.md)]

## <a name="overview"></a><span data-ttu-id="3c273-104">Overview</span><span class="sxs-lookup"><span data-stu-id="3c273-104">Overview</span></span>
<span data-ttu-id="3c273-105">Storage Metrics is enabled by default when you create a new storage account.</span><span class="sxs-lookup"><span data-stu-id="3c273-105">Storage Metrics is enabled by default when you create a new storage account.</span></span> <span data-ttu-id="3c273-106">You can configure monitoring using either the [Azure Classic Portal](https://manage.windowsazure.com), Windows PowerShell, or programmatically through a storage API.</span><span class="sxs-lookup"><span data-stu-id="3c273-106">You can configure monitoring using either the [Azure Classic Portal](https://manage.windowsazure.com), Windows PowerShell, or programmatically through a storage API.</span></span>

<span data-ttu-id="3c273-107">When you enable Storage Metrics, you must choose a retention period for the data: this period determines for how long the storage service keeps the metrics and charges you for the space required to store them.</span><span class="sxs-lookup"><span data-stu-id="3c273-107">When you enable Storage Metrics, you must choose a retention period for the data: this period determines for how long the storage service keeps the metrics and charges you for the space required to store them.</span></span> <span data-ttu-id="3c273-108">Typically, you should use a shorter retention period for minute metrics than hourly metrics because of the significant extra space required for minute metrics.</span><span class="sxs-lookup"><span data-stu-id="3c273-108">Typically, you should use a shorter retention period for minute metrics than hourly metrics because of the significant extra space required for minute metrics.</span></span> <span data-ttu-id="3c273-109">You should choose a retention period such that you have sufficient time to analyze the data and download any metrics you wish to keep for off-line analysis or reporting purposes.</span><span class="sxs-lookup"><span data-stu-id="3c273-109">You should choose a retention period such that you have sufficient time to analyze the data and download any metrics you wish to keep for off-line analysis or reporting purposes.</span></span> <span data-ttu-id="3c273-110">Remember that you will also be billed for downloading metrics data from your storage account.</span><span class="sxs-lookup"><span data-stu-id="3c273-110">Remember that you will also be billed for downloading metrics data from your storage account.</span></span>

## <a name="how-to-enable-storage-metrics-using-the-azure-classic-portal"></a><span data-ttu-id="3c273-111">How to enable Storage metrics using the Azure Classic Portal</span><span class="sxs-lookup"><span data-stu-id="3c273-111">How to enable Storage metrics using the Azure Classic Portal</span></span>
<span data-ttu-id="3c273-112">In the [Azure Classic Portal](https://manage.windowsazure.com), you use the Configure page for a storage account to control Storage Metrics.</span><span class="sxs-lookup"><span data-stu-id="3c273-112">In the [Azure Classic Portal](https://manage.windowsazure.com), you use the Configure page for a storage account to control Storage Metrics.</span></span> <span data-ttu-id="3c273-113">For monitoring, you can set a level and a retention period in days for each of blobs, tables, and queues.</span><span class="sxs-lookup"><span data-stu-id="3c273-113">For monitoring, you can set a level and a retention period in days for each of blobs, tables, and queues.</span></span> <span data-ttu-id="3c273-114">In each case, the level is one of the following:</span><span class="sxs-lookup"><span data-stu-id="3c273-114">In each case, the level is one of the following:</span></span>

* <span data-ttu-id="3c273-115">Off — No metrics are collected.</span><span class="sxs-lookup"><span data-stu-id="3c273-115">Off — No metrics are collected.</span></span>
* <span data-ttu-id="3c273-116">Minimal — Storage Metrics collects a basic set of metrics such as ingress/egress, availability, latency, and success percentages, which are aggregated for the Blob, Table, and Queue services.</span><span class="sxs-lookup"><span data-stu-id="3c273-116">Minimal — Storage Metrics collects a basic set of metrics such as ingress/egress, availability, latency, and success percentages, which are aggregated for the Blob, Table, and Queue services.</span></span>
* <span data-ttu-id="3c273-117">Verbose — Storage Metrics collects a full set of metrics that includes the same metrics for each storage API operation, in addition to the service-level metrics.</span><span class="sxs-lookup"><span data-stu-id="3c273-117">Verbose — Storage Metrics collects a full set of metrics that includes the same metrics for each storage API operation, in addition to the service-level metrics.</span></span> <span data-ttu-id="3c273-118">Verbose metrics enable closer analysis of issues that occur during application operations.</span><span class="sxs-lookup"><span data-stu-id="3c273-118">Verbose metrics enable closer analysis of issues that occur during application operations.</span></span>

<span data-ttu-id="3c273-119">Note that the Azure Classic Portal does not currently enable you to configure minute metrics in your storage account; you must enable minute metrics using PowerShell or programmatically.</span><span class="sxs-lookup"><span data-stu-id="3c273-119">Note that the Azure Classic Portal does not currently enable you to configure minute metrics in your storage account; you must enable minute metrics using PowerShell or programmatically.</span></span>

## <a name="how-to-enable-storage-metrics-using-powershell"></a><span data-ttu-id="3c273-120">How to enable Storage metrics using PowerShell</span><span class="sxs-lookup"><span data-stu-id="3c273-120">How to enable Storage metrics using PowerShell</span></span>
<span data-ttu-id="3c273-121">You can use PowerShell on your local machine to configure Storage Metrics in your storage account by using the Azure PowerShell cmdlet Get-AzureStorageServiceMetricsProperty to retrieve the current settings, and the cmdlet Set-AzureStorageServiceMetricsProperty to change the current settings.</span><span class="sxs-lookup"><span data-stu-id="3c273-121">You can use PowerShell on your local machine to configure Storage Metrics in your storage account by using the Azure PowerShell cmdlet Get-AzureStorageServiceMetricsProperty to retrieve the current settings, and the cmdlet Set-AzureStorageServiceMetricsProperty to change the current settings.</span></span>

<span data-ttu-id="3c273-122">The cmdlets that control Storage Metrics use the following parameters:</span><span class="sxs-lookup"><span data-stu-id="3c273-122">The cmdlets that control Storage Metrics use the following parameters:</span></span>

* <span data-ttu-id="3c273-123">MetricsType possible values are Hour and Minute.</span><span class="sxs-lookup"><span data-stu-id="3c273-123">MetricsType possible values are Hour and Minute.</span></span>
* <span data-ttu-id="3c273-124">ServiceType possible values are Blob, Queue, and Table.</span><span class="sxs-lookup"><span data-stu-id="3c273-124">ServiceType possible values are Blob, Queue, and Table.</span></span>
* <span data-ttu-id="3c273-125">MetricsLevel possible values are None (equivalent to Off in the Azure Classic Portal), Service (equivalent to Minimal in the Azure Classic Portal), and ServiceAndApi (equivalent to Verbose in the Azure Classic Portal).</span><span class="sxs-lookup"><span data-stu-id="3c273-125">MetricsLevel possible values are None (equivalent to Off in the Azure Classic Portal), Service (equivalent to Minimal in the Azure Classic Portal), and ServiceAndApi (equivalent to Verbose in the Azure Classic Portal).</span></span>

<span data-ttu-id="3c273-126">For example, the following command switches on minute metrics for the blob service in your default storage account with the retention period set to five days:</span><span class="sxs-lookup"><span data-stu-id="3c273-126">For example, the following command switches on minute metrics for the blob service in your default storage account with the retention period set to five days:</span></span>

```powershell
Set-AzureStorageServiceMetricsProperty -MetricsType Minute -ServiceType Blob -MetricsLevel ServiceAndApi  -RetentionDays 5
```
<span data-ttu-id="3c273-127">The following command retrieves the current hourly metrics level and retention days for the blob service in your default storage account:</span><span class="sxs-lookup"><span data-stu-id="3c273-127">The following command retrieves the current hourly metrics level and retention days for the blob service in your default storage account:</span></span>

```powershell
Get-AzureStorageServiceMetricsProperty -MetricsType Hour -ServiceType Blob
```
<span data-ttu-id="3c273-128">For information about how to configure the Azure PowerShell cmdlets to work with your Azure subscription and how to select the default storage account to use, see: [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="3c273-128">For information about how to configure the Azure PowerShell cmdlets to work with your Azure subscription and how to select the default storage account to use, see: [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>

## <a name="how-to-enable-storage-metrics-programmatically"></a><span data-ttu-id="3c273-129">How to enable Storage metrics programmatically</span><span class="sxs-lookup"><span data-stu-id="3c273-129">How to enable Storage metrics programmatically</span></span>
<span data-ttu-id="3c273-130">The following C# snippet shows how to enable metrics and logging for the Blob service using the storage client library for .NET:</span><span class="sxs-lookup"><span data-stu-id="3c273-130">The following C# snippet shows how to enable metrics and logging for the Blob service using the storage client library for .NET:</span></span>

```csharp
//Parse the connection string for the storage account.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);

// Create service client for credentialed access to the Blob service.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Enable Storage Analytics logging and set retention policy to 10 days. 
ServiceProperties properties = new ServiceProperties();
properties.Logging.LoggingOperations = LoggingOperations.All;
properties.Logging.RetentionDays = 10;
properties.Logging.Version = "1.0";

// Configure service properties for metrics. Both metrics and logging must be set at the same time.
properties.HourMetrics.MetricsLevel = MetricsLevel.ServiceAndApi;
properties.HourMetrics.RetentionDays = 10;
properties.HourMetrics.Version = "1.0";

properties.MinuteMetrics.MetricsLevel = MetricsLevel.ServiceAndApi;
properties.MinuteMetrics.RetentionDays = 10;
properties.MinuteMetrics.Version = "1.0";

// Set the default service version to be used for anonymous requests.
properties.DefaultServiceVersion = "2015-04-05";

// Set the service properties.
blobClient.SetServiceProperties(properties);
```

## <a name="viewing-storage-metrics"></a><span data-ttu-id="3c273-131">Viewing Storage metrics</span><span class="sxs-lookup"><span data-stu-id="3c273-131">Viewing Storage metrics</span></span>
<span data-ttu-id="3c273-132">When you have configured Storage Metrics to monitor your storage account, it records the metrics in a set of well-known tables in your storage account.</span><span class="sxs-lookup"><span data-stu-id="3c273-132">When you have configured Storage Metrics to monitor your storage account, it records the metrics in a set of well-known tables in your storage account.</span></span> <span data-ttu-id="3c273-133">You can use the Monitor page for your storage account in the Azure Classic Portal to view the hourly metrics as they become available on a chart.</span><span class="sxs-lookup"><span data-stu-id="3c273-133">You can use the Monitor page for your storage account in the Azure Classic Portal to view the hourly metrics as they become available on a chart.</span></span> <span data-ttu-id="3c273-134">On this page in the Azure Classic Portal, you can:</span><span class="sxs-lookup"><span data-stu-id="3c273-134">On this page in the Azure Classic Portal, you can:</span></span>

* <span data-ttu-id="3c273-135">Select which metrics to plot on the chart (the choice of available metrics will depend on whether you chose verbose or minimal monitoring for the service on the Configure page).</span><span class="sxs-lookup"><span data-stu-id="3c273-135">Select which metrics to plot on the chart (the choice of available metrics will depend on whether you chose verbose or minimal monitoring for the service on the Configure page).</span></span>
* <span data-ttu-id="3c273-136">Select the time range for the metrics displayed on the chart.</span><span class="sxs-lookup"><span data-stu-id="3c273-136">Select the time range for the metrics displayed on the chart.</span></span>
* <span data-ttu-id="3c273-137">Choose to use an absolute or relative scale to plot the metrics.</span><span class="sxs-lookup"><span data-stu-id="3c273-137">Choose to use an absolute or relative scale to plot the metrics.</span></span>
* <span data-ttu-id="3c273-138">Configure email alerts to notify you when a specific metric reaches a certain value.</span><span class="sxs-lookup"><span data-stu-id="3c273-138">Configure email alerts to notify you when a specific metric reaches a certain value.</span></span>

<span data-ttu-id="3c273-139">If you want to download the metrics for long-term storage or to analyze them locally, you will need to use a tool or write some code to read the tables.</span><span class="sxs-lookup"><span data-stu-id="3c273-139">If you want to download the metrics for long-term storage or to analyze them locally, you will need to use a tool or write some code to read the tables.</span></span> <span data-ttu-id="3c273-140">You must download the minute metrics for analysis.</span><span class="sxs-lookup"><span data-stu-id="3c273-140">You must download the minute metrics for analysis.</span></span> <span data-ttu-id="3c273-141">The tables do not appear if you list all the tables in your storage account, but you can access them directly by name.</span><span class="sxs-lookup"><span data-stu-id="3c273-141">The tables do not appear if you list all the tables in your storage account, but you can access them directly by name.</span></span> <span data-ttu-id="3c273-142">Many third-party storage-browsing tools are aware of these tables and enable you to view them directly (see the blog post [Microsoft Azure Storage Explorers](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx) for a list of available tools).</span><span class="sxs-lookup"><span data-stu-id="3c273-142">Many third-party storage-browsing tools are aware of these tables and enable you to view them directly (see the blog post [Microsoft Azure Storage Explorers](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx) for a list of available tools).</span></span>

### <a name="hourly-metrics"></a><span data-ttu-id="3c273-143">Hourly metrics</span><span class="sxs-lookup"><span data-stu-id="3c273-143">Hourly metrics</span></span>
* <span data-ttu-id="3c273-144">$MetricsHourPrimaryTransactionsBlob</span><span class="sxs-lookup"><span data-stu-id="3c273-144">$MetricsHourPrimaryTransactionsBlob</span></span>
* <span data-ttu-id="3c273-145">$MetricsHourPrimaryTransactionsTable</span><span class="sxs-lookup"><span data-stu-id="3c273-145">$MetricsHourPrimaryTransactionsTable</span></span>
* <span data-ttu-id="3c273-146">$MetricsHourPrimaryTransactionsQueue</span><span class="sxs-lookup"><span data-stu-id="3c273-146">$MetricsHourPrimaryTransactionsQueue</span></span>

### <a name="minute-metrics"></a><span data-ttu-id="3c273-147">Minute metrics</span><span class="sxs-lookup"><span data-stu-id="3c273-147">Minute metrics</span></span>
* <span data-ttu-id="3c273-148">$MetricsMinutePrimaryTransactionsBlob</span><span class="sxs-lookup"><span data-stu-id="3c273-148">$MetricsMinutePrimaryTransactionsBlob</span></span>
* <span data-ttu-id="3c273-149">$MetricsMinutePrimaryTransactionsTable</span><span class="sxs-lookup"><span data-stu-id="3c273-149">$MetricsMinutePrimaryTransactionsTable</span></span>
* <span data-ttu-id="3c273-150">$MetricsMinutePrimaryTransactionsQueue</span><span class="sxs-lookup"><span data-stu-id="3c273-150">$MetricsMinutePrimaryTransactionsQueue</span></span>

### <a name="capacity"></a><span data-ttu-id="3c273-151">Capacity</span><span class="sxs-lookup"><span data-stu-id="3c273-151">Capacity</span></span>
* <span data-ttu-id="3c273-152">$MetricsCapacityBlob</span><span class="sxs-lookup"><span data-stu-id="3c273-152">$MetricsCapacityBlob</span></span>

<span data-ttu-id="3c273-153">You can find full details of the schemas for these tables at [Storage Analytics Metrics Table Schema](https://msdn.microsoft.com/library/azure/hh343264.aspx).</span><span class="sxs-lookup"><span data-stu-id="3c273-153">You can find full details of the schemas for these tables at [Storage Analytics Metrics Table Schema](https://msdn.microsoft.com/library/azure/hh343264.aspx).</span></span> <span data-ttu-id="3c273-154">The sample rows below show only a subset of the columns available, but illustrate some important features of the way Storage Metrics saves these metrics:</span><span class="sxs-lookup"><span data-stu-id="3c273-154">The sample rows below show only a subset of the columns available, but illustrate some important features of the way Storage Metrics saves these metrics:</span></span>

| <span data-ttu-id="3c273-155">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="3c273-155">PartitionKey</span></span> | <span data-ttu-id="3c273-156">RowKey</span><span class="sxs-lookup"><span data-stu-id="3c273-156">RowKey</span></span> | <span data-ttu-id="3c273-157">Timestamp</span><span class="sxs-lookup"><span data-stu-id="3c273-157">Timestamp</span></span> | <span data-ttu-id="3c273-158">TotalRequests</span><span class="sxs-lookup"><span data-stu-id="3c273-158">TotalRequests</span></span> | <span data-ttu-id="3c273-159">TotalBillableRequests</span><span class="sxs-lookup"><span data-stu-id="3c273-159">TotalBillableRequests</span></span> | <span data-ttu-id="3c273-160">TotalIngress</span><span class="sxs-lookup"><span data-stu-id="3c273-160">TotalIngress</span></span> | <span data-ttu-id="3c273-161">TotalEgress</span><span class="sxs-lookup"><span data-stu-id="3c273-161">TotalEgress</span></span> | <span data-ttu-id="3c273-162">Availability</span><span class="sxs-lookup"><span data-stu-id="3c273-162">Availability</span></span> | <span data-ttu-id="3c273-163">AverageE2ELatency</span><span class="sxs-lookup"><span data-stu-id="3c273-163">AverageE2ELatency</span></span> | <span data-ttu-id="3c273-164">AverageServerLatency</span><span class="sxs-lookup"><span data-stu-id="3c273-164">AverageServerLatency</span></span> | <span data-ttu-id="3c273-165">PercentSuccess</span><span class="sxs-lookup"><span data-stu-id="3c273-165">PercentSuccess</span></span> |
| --- |:---:| ---:| --- | --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="3c273-166">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="3c273-166">20140522T1100</span></span> |<span data-ttu-id="3c273-167">user;All</span><span class="sxs-lookup"><span data-stu-id="3c273-167">user;All</span></span> |<span data-ttu-id="3c273-168">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="3c273-168">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="3c273-169">7</span><span class="sxs-lookup"><span data-stu-id="3c273-169">7</span></span> |<span data-ttu-id="3c273-170">7</span><span class="sxs-lookup"><span data-stu-id="3c273-170">7</span></span> |<span data-ttu-id="3c273-171">4003</span><span class="sxs-lookup"><span data-stu-id="3c273-171">4003</span></span> |<span data-ttu-id="3c273-172">46801</span><span class="sxs-lookup"><span data-stu-id="3c273-172">46801</span></span> |<span data-ttu-id="3c273-173">100</span><span class="sxs-lookup"><span data-stu-id="3c273-173">100</span></span> |<span data-ttu-id="3c273-174">104.4286</span><span class="sxs-lookup"><span data-stu-id="3c273-174">104.4286</span></span> |<span data-ttu-id="3c273-175">6.857143</span><span class="sxs-lookup"><span data-stu-id="3c273-175">6.857143</span></span> |<span data-ttu-id="3c273-176">100</span><span class="sxs-lookup"><span data-stu-id="3c273-176">100</span></span> |
| <span data-ttu-id="3c273-177">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="3c273-177">20140522T1100</span></span> |<span data-ttu-id="3c273-178">user;QueryEntities</span><span class="sxs-lookup"><span data-stu-id="3c273-178">user;QueryEntities</span></span> |<span data-ttu-id="3c273-179">2014-05-22T11:01:16.7640250Z</span><span class="sxs-lookup"><span data-stu-id="3c273-179">2014-05-22T11:01:16.7640250Z</span></span> |<span data-ttu-id="3c273-180">5</span><span class="sxs-lookup"><span data-stu-id="3c273-180">5</span></span> |<span data-ttu-id="3c273-181">5</span><span class="sxs-lookup"><span data-stu-id="3c273-181">5</span></span> |<span data-ttu-id="3c273-182">2694</span><span class="sxs-lookup"><span data-stu-id="3c273-182">2694</span></span> |<span data-ttu-id="3c273-183">45951</span><span class="sxs-lookup"><span data-stu-id="3c273-183">45951</span></span> |<span data-ttu-id="3c273-184">100</span><span class="sxs-lookup"><span data-stu-id="3c273-184">100</span></span> |<span data-ttu-id="3c273-185">143.8</span><span class="sxs-lookup"><span data-stu-id="3c273-185">143.8</span></span> |<span data-ttu-id="3c273-186">7.8</span><span class="sxs-lookup"><span data-stu-id="3c273-186">7.8</span></span> |<span data-ttu-id="3c273-187">100</span><span class="sxs-lookup"><span data-stu-id="3c273-187">100</span></span> |
| <span data-ttu-id="3c273-188">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="3c273-188">20140522T1100</span></span> |<span data-ttu-id="3c273-189">user;QueryEntity</span><span class="sxs-lookup"><span data-stu-id="3c273-189">user;QueryEntity</span></span> |<span data-ttu-id="3c273-190">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="3c273-190">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="3c273-191">1</span><span class="sxs-lookup"><span data-stu-id="3c273-191">1</span></span> |<span data-ttu-id="3c273-192">1</span><span class="sxs-lookup"><span data-stu-id="3c273-192">1</span></span> |<span data-ttu-id="3c273-193">538</span><span class="sxs-lookup"><span data-stu-id="3c273-193">538</span></span> |<span data-ttu-id="3c273-194">633</span><span class="sxs-lookup"><span data-stu-id="3c273-194">633</span></span> |<span data-ttu-id="3c273-195">100</span><span class="sxs-lookup"><span data-stu-id="3c273-195">100</span></span> |<span data-ttu-id="3c273-196">3</span><span class="sxs-lookup"><span data-stu-id="3c273-196">3</span></span> |<span data-ttu-id="3c273-197">3</span><span class="sxs-lookup"><span data-stu-id="3c273-197">3</span></span> |<span data-ttu-id="3c273-198">100</span><span class="sxs-lookup"><span data-stu-id="3c273-198">100</span></span> |
| <span data-ttu-id="3c273-199">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="3c273-199">20140522T1100</span></span> |<span data-ttu-id="3c273-200">user;UpdateEntity</span><span class="sxs-lookup"><span data-stu-id="3c273-200">user;UpdateEntity</span></span> |<span data-ttu-id="3c273-201">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="3c273-201">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="3c273-202">1</span><span class="sxs-lookup"><span data-stu-id="3c273-202">1</span></span> |<span data-ttu-id="3c273-203">1</span><span class="sxs-lookup"><span data-stu-id="3c273-203">1</span></span> |<span data-ttu-id="3c273-204">771</span><span class="sxs-lookup"><span data-stu-id="3c273-204">771</span></span> |<span data-ttu-id="3c273-205">217</span><span class="sxs-lookup"><span data-stu-id="3c273-205">217</span></span> |<span data-ttu-id="3c273-206">100</span><span class="sxs-lookup"><span data-stu-id="3c273-206">100</span></span> |<span data-ttu-id="3c273-207">9</span><span class="sxs-lookup"><span data-stu-id="3c273-207">9</span></span> |<span data-ttu-id="3c273-208">6</span><span class="sxs-lookup"><span data-stu-id="3c273-208">6</span></span> |<span data-ttu-id="3c273-209">100</span><span class="sxs-lookup"><span data-stu-id="3c273-209">100</span></span> |

<span data-ttu-id="3c273-210">In this example minute metrics data, the partition key uses the time at minute resolution.</span><span class="sxs-lookup"><span data-stu-id="3c273-210">In this example minute metrics data, the partition key uses the time at minute resolution.</span></span> <span data-ttu-id="3c273-211">The row key identifies the type of information that is stored in the row and this is composed of two pieces of information, the access type, and the request type:</span><span class="sxs-lookup"><span data-stu-id="3c273-211">The row key identifies the type of information that is stored in the row and this is composed of two pieces of information, the access type, and the request type:</span></span>

* <span data-ttu-id="3c273-212">The access type is either user or system, where user refers to all user requests to the storage service, and system refers to requests made by Storage Analytics.</span><span class="sxs-lookup"><span data-stu-id="3c273-212">The access type is either user or system, where user refers to all user requests to the storage service, and system refers to requests made by Storage Analytics.</span></span>
* <span data-ttu-id="3c273-213">The request type is either all in which case it is a summary line, or it identifies the specific API such as QueryEntity or UpdateEntity.</span><span class="sxs-lookup"><span data-stu-id="3c273-213">The request type is either all in which case it is a summary line, or it identifies the specific API such as QueryEntity or UpdateEntity.</span></span>

<span data-ttu-id="3c273-214">The sample data above shows all the records for a single minute (starting at 11:00AM), so the number of QueryEntities requests plus the number of QueryEntity requests plus the number of UpdateEntity requests add up to seven, which is the total shown on the user:All row.</span><span class="sxs-lookup"><span data-stu-id="3c273-214">The sample data above shows all the records for a single minute (starting at 11:00AM), so the number of QueryEntities requests plus the number of QueryEntity requests plus the number of UpdateEntity requests add up to seven, which is the total shown on the user:All row.</span></span> <span data-ttu-id="3c273-215">Similarly, you can derive the average end-to-end latency 104.4286 on the user:All row by calculating ((143.8 \* 5) + 3 + 9)/7.</span><span class="sxs-lookup"><span data-stu-id="3c273-215">Similarly, you can derive the average end-to-end latency 104.4286 on the user:All row by calculating ((143.8 \* 5) + 3 + 9)/7.</span></span>

<span data-ttu-id="3c273-216">You should consider setting up alerts in the Azure Classic Portal on the Monitor page so that Storage Metrics can automatically notify you of any important changes in the behavior of your storage services.If you use a storage explorer tool to download this metrics data in a delimited format, you can use Microsoft Excel to analyze the data.</span><span class="sxs-lookup"><span data-stu-id="3c273-216">You should consider setting up alerts in the Azure Classic Portal on the Monitor page so that Storage Metrics can automatically notify you of any important changes in the behavior of your storage services.If you use a storage explorer tool to download this metrics data in a delimited format, you can use Microsoft Excel to analyze the data.</span></span> <span data-ttu-id="3c273-217">See the blog post [Microsoft Azure Storage Explorers](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx) for a list of available storage explorer tools.</span><span class="sxs-lookup"><span data-stu-id="3c273-217">See the blog post [Microsoft Azure Storage Explorers](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx) for a list of available storage explorer tools.</span></span>

## <a name="accessing-metrics-data-programmatically"></a><span data-ttu-id="3c273-218">Accessing metrics data programmatically</span><span class="sxs-lookup"><span data-stu-id="3c273-218">Accessing metrics data programmatically</span></span>
<span data-ttu-id="3c273-219">The following listing shows sample C# code that accesses the minute metrics for a range of minutes and displays the results in a console Window.</span><span class="sxs-lookup"><span data-stu-id="3c273-219">The following listing shows sample C# code that accesses the minute metrics for a range of minutes and displays the results in a console Window.</span></span> <span data-ttu-id="3c273-220">It uses the Azure Storage Library version 4 that includes the CloudAnalyticsClient class that simplifies accessing the metrics tables in storage.</span><span class="sxs-lookup"><span data-stu-id="3c273-220">It uses the Azure Storage Library version 4 that includes the CloudAnalyticsClient class that simplifies accessing the metrics tables in storage.</span></span>

```csharp
private static void PrintMinuteMetrics(CloudAnalyticsClient analyticsClient, DateTimeOffset startDateTime, DateTimeOffset endDateTime)
{
    // Convert the dates to the format used in the PartitionKey
    var start = startDateTime.ToUniversalTime().ToString("yyyyMMdd'T'HHmm");
    var end = endDateTime.ToUniversalTime().ToString("yyyyMMdd'T'HHmm");

    var services = Enum.GetValues(typeof(StorageService));
    foreach (StorageService service in services)
    {
        Console.WriteLine("Minute Metrics for Service {0} from {1} to {2} UTC", service, start, end);
        var metricsQuery = analyticsClient.CreateMinuteMetricsQuery(service, StorageLocation.Primary);
        var t = analyticsClient.GetMinuteMetricsTable(service);
        var opContext = new OperationContext();
        var query =
          from entity in metricsQuery
          // Note, you can't filter using the entity properties Time, AccessType, or TransactionType
          // because they are calculated fields in the MetricsEntity class.
          // The PartitionKey identifies the DataTime of the metrics.
          where entity.PartitionKey.CompareTo(start) >= 0 && entity.PartitionKey.CompareTo(end) <= 0 
        select entity;

        // Filter on "user" transactions after fetching the metrics from Table Storage.
        // (StartsWith is not supported using LINQ with Azure table storage)
        var results = query.ToList().Where(m => m.RowKey.StartsWith("user"));
        var resultString = results.Aggregate(new StringBuilder(), (builder, metrics) => builder.AppendLine(MetricsString(metrics, opContext))).ToString();
        Console.WriteLine(resultString);
    }
}

private static string MetricsString(MetricsEntity entity, OperationContext opContext)
{
    var entityProperties = entity.WriteEntity(opContext);
    var entityString =
    string.Format("Time: {0}, ", entity.Time) +
    string.Format("AccessType: {0}, ", entity.AccessType) +
    string.Format("TransactionType: {0}, ", entity.TransactionType) +
    string.Join(",", entityProperties.Select(e => new KeyValuePair<string, string>(e.Key.ToString(), e.Value.PropertyAsObject.ToString())));
    return entityString;
}
```

## <a name="what-charges-do-you-incur-when-you-enable-storage-metrics"></a><span data-ttu-id="3c273-221">What charges do you incur when you enable storage metrics?</span><span class="sxs-lookup"><span data-stu-id="3c273-221">What charges do you incur when you enable storage metrics?</span></span>
<span data-ttu-id="3c273-222">Write requests to create table entities for metrics are charged at the standard rates applicable to all Azure Storage operations.</span><span class="sxs-lookup"><span data-stu-id="3c273-222">Write requests to create table entities for metrics are charged at the standard rates applicable to all Azure Storage operations.</span></span>

<span data-ttu-id="3c273-223">Read and delete requests by a client to metrics data are also billable at standard rates.</span><span class="sxs-lookup"><span data-stu-id="3c273-223">Read and delete requests by a client to metrics data are also billable at standard rates.</span></span> <span data-ttu-id="3c273-224">If you have configured a data retention policy, you are not charged when Azure Storage deletes old metrics data.</span><span class="sxs-lookup"><span data-stu-id="3c273-224">If you have configured a data retention policy, you are not charged when Azure Storage deletes old metrics data.</span></span> <span data-ttu-id="3c273-225">However, if you delete analytics data, your account is charged for the delete operations.</span><span class="sxs-lookup"><span data-stu-id="3c273-225">However, if you delete analytics data, your account is charged for the delete operations.</span></span>

<span data-ttu-id="3c273-226">The capacity used by the metrics tables is also billable: you can use the following to estimate the amount of capacity used for storing metrics data:</span><span class="sxs-lookup"><span data-stu-id="3c273-226">The capacity used by the metrics tables is also billable: you can use the following to estimate the amount of capacity used for storing metrics data:</span></span>

* <span data-ttu-id="3c273-227">If each hour a service utilizes every API in every service, then approximately 148KB of data is stored every hour in the metrics transaction tables if you have enabled both service and API level summary.</span><span class="sxs-lookup"><span data-stu-id="3c273-227">If each hour a service utilizes every API in every service, then approximately 148KB of data is stored every hour in the metrics transaction tables if you have enabled both service and API level summary.</span></span>
* <span data-ttu-id="3c273-228">If each hour a service utilizes every API in every service, then approximately 12KB of data is stored every hour in the metrics transaction tables if you have enabled just service level summary.</span><span class="sxs-lookup"><span data-stu-id="3c273-228">If each hour a service utilizes every API in every service, then approximately 12KB of data is stored every hour in the metrics transaction tables if you have enabled just service level summary.</span></span>
* <span data-ttu-id="3c273-229">The capacity table for blobs has two rows added each day (provided user has opted in for logs): this implies that every day the size of this table increases by up to approximately 300 bytes.</span><span class="sxs-lookup"><span data-stu-id="3c273-229">The capacity table for blobs has two rows added each day (provided user has opted in for logs): this implies that every day the size of this table increases by up to approximately 300 bytes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3c273-230">Next steps:</span><span class="sxs-lookup"><span data-stu-id="3c273-230">Next steps:</span></span>
[<span data-ttu-id="3c273-231">Enabling Storage Analytics Logging and Accessing Log Data</span><span class="sxs-lookup"><span data-stu-id="3c273-231">Enabling Storage Analytics Logging and Accessing Log Data</span></span>](https://msdn.microsoft.com/library/dn782840.aspx)