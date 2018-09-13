---
title: Enabling storage metrics in the Azure portal | Microsoft Docs
description: How to enable storage metrics for the Blob, Queue, Table, and File services
services: storage
documentationcenter: ''
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 0407adfc-2a41-4126-922d-b76e90b74563
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/14/2017
ms.author: robinsh
ms.openlocfilehash: d544695654ff136ee25856cb4a0309f882057ebb
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549579"
---
# <a name="enabling-azure-storage-metrics-and-viewing-metrics-data"></a><span data-ttu-id="6b038-103">Enabling Azure Storage metrics and viewing metrics data</span><span class="sxs-lookup"><span data-stu-id="6b038-103">Enabling Azure Storage metrics and viewing metrics data</span></span>
[!INCLUDE [storage-selector-portal-enable-and-view-metrics](../../includes/storage-selector-portal-enable-and-view-metrics.md)]

## <a name="overview"></a><span data-ttu-id="6b038-104">Overview</span><span class="sxs-lookup"><span data-stu-id="6b038-104">Overview</span></span>
<span data-ttu-id="6b038-105">Storage Metrics is enabled by default when you create a new storage account.</span><span class="sxs-lookup"><span data-stu-id="6b038-105">Storage Metrics is enabled by default when you create a new storage account.</span></span> <span data-ttu-id="6b038-106">You can configure monitoring via the [Azure portal](https://portal.azure.com) or Windows PowerShell, or programmatically via one of the storage client libraries.</span><span class="sxs-lookup"><span data-stu-id="6b038-106">You can configure monitoring via the [Azure portal](https://portal.azure.com) or Windows PowerShell, or programmatically via one of the storage client libraries.</span></span>

<span data-ttu-id="6b038-107">You can configure a retention period for the metrics data: this period determines for how long the storage service keeps the metrics and charges you for the space required to store them.</span><span class="sxs-lookup"><span data-stu-id="6b038-107">You can configure a retention period for the metrics data: this period determines for how long the storage service keeps the metrics and charges you for the space required to store them.</span></span> <span data-ttu-id="6b038-108">Typically, you should use a shorter retention period for minute metrics than hourly metrics because of the significant extra space required for minute metrics.</span><span class="sxs-lookup"><span data-stu-id="6b038-108">Typically, you should use a shorter retention period for minute metrics than hourly metrics because of the significant extra space required for minute metrics.</span></span> <span data-ttu-id="6b038-109">You should choose a retention period such that you have sufficient time to analyze the data and download any metrics you wish to keep for off-line analysis or reporting purposes.</span><span class="sxs-lookup"><span data-stu-id="6b038-109">You should choose a retention period such that you have sufficient time to analyze the data and download any metrics you wish to keep for off-line analysis or reporting purposes.</span></span> <span data-ttu-id="6b038-110">Remember that you will also be billed for downloading metrics data from your storage account.</span><span class="sxs-lookup"><span data-stu-id="6b038-110">Remember that you will also be billed for downloading metrics data from your storage account.</span></span>

## <a name="how-to-enable-metrics-using-the-azure-portal"></a><span data-ttu-id="6b038-111">How to enable metrics using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="6b038-111">How to enable metrics using the Azure portal</span></span>
<span data-ttu-id="6b038-112">Follow these steps to enable metrics in the [Azure portal](https://portal.azure.com):</span><span class="sxs-lookup"><span data-stu-id="6b038-112">Follow these steps to enable metrics in the [Azure portal](https://portal.azure.com):</span></span>

1. <span data-ttu-id="6b038-113">Navigate to your storage account.</span><span class="sxs-lookup"><span data-stu-id="6b038-113">Navigate to your storage account.</span></span>
1. <span data-ttu-id="6b038-114">Select **Diagnostics** on the **Menu** blade</span><span class="sxs-lookup"><span data-stu-id="6b038-114">Select **Diagnostics** on the **Menu** blade</span></span>
1. <span data-ttu-id="6b038-115">Ensure that **Status** is set to **On**.</span><span class="sxs-lookup"><span data-stu-id="6b038-115">Ensure that **Status** is set to **On**.</span></span>
1. <span data-ttu-id="6b038-116">Select the metrics for the services you wish to monitor.</span><span class="sxs-lookup"><span data-stu-id="6b038-116">Select the metrics for the services you wish to monitor.</span></span>
1. <span data-ttu-id="6b038-117">Specify a retention policy to indicate how long to retain metrics and log data.</span><span class="sxs-lookup"><span data-stu-id="6b038-117">Specify a retention policy to indicate how long to retain metrics and log data.</span></span>
1. <span data-ttu-id="6b038-118">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="6b038-118">Select **Save**.</span></span>

<span data-ttu-id="6b038-119">Note that the [Azure portal](https://portal.azure.com) does not currently enable you to configure minute metrics in your storage account; you must enable minute metrics using PowerShell or programmatically.</span><span class="sxs-lookup"><span data-stu-id="6b038-119">Note that the [Azure portal](https://portal.azure.com) does not currently enable you to configure minute metrics in your storage account; you must enable minute metrics using PowerShell or programmatically.</span></span>

## <a name="how-to-enable-metrics-using-powershell"></a><span data-ttu-id="6b038-120">How to enable metrics using PowerShell</span><span class="sxs-lookup"><span data-stu-id="6b038-120">How to enable metrics using PowerShell</span></span>
<span data-ttu-id="6b038-121">You can use PowerShell on your local machine to configure Storage Metrics in your storage account by using the Azure PowerShell cmdlet Get-AzureStorageServiceMetricsProperty to retrieve the current settings, and the cmdlet Set-AzureStorageServiceMetricsProperty to change the current settings.</span><span class="sxs-lookup"><span data-stu-id="6b038-121">You can use PowerShell on your local machine to configure Storage Metrics in your storage account by using the Azure PowerShell cmdlet Get-AzureStorageServiceMetricsProperty to retrieve the current settings, and the cmdlet Set-AzureStorageServiceMetricsProperty to change the current settings.</span></span>

<span data-ttu-id="6b038-122">The cmdlets that control Storage Metrics use the following parameters:</span><span class="sxs-lookup"><span data-stu-id="6b038-122">The cmdlets that control Storage Metrics use the following parameters:</span></span>

* <span data-ttu-id="6b038-123">MetricsType: possible values are Hour and Minute.</span><span class="sxs-lookup"><span data-stu-id="6b038-123">MetricsType: possible values are Hour and Minute.</span></span>
* <span data-ttu-id="6b038-124">ServiceType: possible values are Blob, Queue, and Table.</span><span class="sxs-lookup"><span data-stu-id="6b038-124">ServiceType: possible values are Blob, Queue, and Table.</span></span>
* <span data-ttu-id="6b038-125">MetricsLevel: possible values are None, Service, and ServiceAndApi.</span><span class="sxs-lookup"><span data-stu-id="6b038-125">MetricsLevel: possible values are None, Service, and ServiceAndApi.</span></span>

<span data-ttu-id="6b038-126">For example, the following command switches on minute metrics for the Blob service in your default storage account with the retention period set to five days:</span><span class="sxs-lookup"><span data-stu-id="6b038-126">For example, the following command switches on minute metrics for the Blob service in your default storage account with the retention period set to five days:</span></span>

```powershell
Set-AzureStorageServiceMetricsProperty -MetricsType Minute -ServiceType Blob -MetricsLevel ServiceAndApi  -RetentionDays 5`
```

<span data-ttu-id="6b038-127">The following command retrieves the current hourly metrics level and retention days for the blob service in your default storage account:</span><span class="sxs-lookup"><span data-stu-id="6b038-127">The following command retrieves the current hourly metrics level and retention days for the blob service in your default storage account:</span></span>

```powershell
Get-AzureStorageServiceMetricsProperty -MetricsType Hour -ServiceType Blob
```

<span data-ttu-id="6b038-128">For information about how to configure the Azure PowerShell cmdlets to work with your Azure subscription and how to select the default storage account to use, see: [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="6b038-128">For information about how to configure the Azure PowerShell cmdlets to work with your Azure subscription and how to select the default storage account to use, see: [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>

## <a name="how-to-enable-storage-metrics-programmatically"></a><span data-ttu-id="6b038-129">How to enable Storage metrics programmatically</span><span class="sxs-lookup"><span data-stu-id="6b038-129">How to enable Storage metrics programmatically</span></span>
<span data-ttu-id="6b038-130">The following C# snippet shows how to enable metrics and logging for the Blob service using the storage client library for .NET:</span><span class="sxs-lookup"><span data-stu-id="6b038-130">The following C# snippet shows how to enable metrics and logging for the Blob service using the storage client library for .NET:</span></span>

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

## <a name="viewing-storage-metrics"></a><span data-ttu-id="6b038-131">Viewing Storage metrics</span><span class="sxs-lookup"><span data-stu-id="6b038-131">Viewing Storage metrics</span></span>
<span data-ttu-id="6b038-132">After you configure Storage Analytics metrics to monitor your storage account, Storage Analytics records the metrics in a set of well-known tables in your storage account.</span><span class="sxs-lookup"><span data-stu-id="6b038-132">After you configure Storage Analytics metrics to monitor your storage account, Storage Analytics records the metrics in a set of well-known tables in your storage account.</span></span> <span data-ttu-id="6b038-133">You can configure charts to view hourly metrics in the [Azure portal](https://portal.azure.com):</span><span class="sxs-lookup"><span data-stu-id="6b038-133">You can configure charts to view hourly metrics in the [Azure portal](https://portal.azure.com):</span></span>

1. <span data-ttu-id="6b038-134">Navigate to your storage account in the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6b038-134">Navigate to your storage account in the [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="6b038-135">Select **Metrics** in the **Menu** blade for the service whose metrics you want to view.</span><span class="sxs-lookup"><span data-stu-id="6b038-135">Select **Metrics** in the **Menu** blade for the service whose metrics you want to view.</span></span>
1. <span data-ttu-id="6b038-136">Select **Edit** on the chart you want to configure.</span><span class="sxs-lookup"><span data-stu-id="6b038-136">Select **Edit** on the chart you want to configure.</span></span>
1. <span data-ttu-id="6b038-137">In the **Edit Chart** blade, select the **Time Range**, **Chart type**, and the metrics you want displayed in the chart.</span><span class="sxs-lookup"><span data-stu-id="6b038-137">In the **Edit Chart** blade, select the **Time Range**, **Chart type**, and the metrics you want displayed in the chart.</span></span>
1. <span data-ttu-id="6b038-138">Select **OK**</span><span class="sxs-lookup"><span data-stu-id="6b038-138">Select **OK**</span></span>

<span data-ttu-id="6b038-139">If you want to download the metrics for long-term storage or to analyze them locally, you will need to:</span><span class="sxs-lookup"><span data-stu-id="6b038-139">If you want to download the metrics for long-term storage or to analyze them locally, you will need to:</span></span>

* <span data-ttu-id="6b038-140">Use a tool that is aware of these tables and will allow you to view and download them.</span><span class="sxs-lookup"><span data-stu-id="6b038-140">Use a tool that is aware of these tables and will allow you to view and download them.</span></span>
* <span data-ttu-id="6b038-141">Write a custom application or script to read and store the tables.</span><span class="sxs-lookup"><span data-stu-id="6b038-141">Write a custom application or script to read and store the tables.</span></span>

<span data-ttu-id="6b038-142">Many third-party storage-browsing tools are aware of these tables and enable you to view them directly.</span><span class="sxs-lookup"><span data-stu-id="6b038-142">Many third-party storage-browsing tools are aware of these tables and enable you to view them directly.</span></span>
<span data-ttu-id="6b038-143">Please see [Azure Storage Client Tools](storage-explorers.md) for a list of available tools.</span><span class="sxs-lookup"><span data-stu-id="6b038-143">Please see [Azure Storage Client Tools](storage-explorers.md) for a list of available tools.</span></span>

> [!NOTE]
> <span data-ttu-id="6b038-144">Starting with version 0.8.0 of the [Microsoft Azure Storage Explorer](http://storageexplorer.com/), you can view and download the analytics metrics tables.</span><span class="sxs-lookup"><span data-stu-id="6b038-144">Starting with version 0.8.0 of the [Microsoft Azure Storage Explorer](http://storageexplorer.com/), you can view and download the analytics metrics tables.</span></span>
> 
> 

<span data-ttu-id="6b038-145">In order to access the analytics tables programmatically, do note that the analytics tables do not appear if you list all the tables in your storage account.</span><span class="sxs-lookup"><span data-stu-id="6b038-145">In order to access the analytics tables programmatically, do note that the analytics tables do not appear if you list all the tables in your storage account.</span></span> <span data-ttu-id="6b038-146">You can either access them directly by name, or use the [CloudAnalyticsClient API](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.analytics.cloudanalyticsclient.aspx) in the .NET client library to query the table names.</span><span class="sxs-lookup"><span data-stu-id="6b038-146">You can either access them directly by name, or use the [CloudAnalyticsClient API](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.analytics.cloudanalyticsclient.aspx) in the .NET client library to query the table names.</span></span>

### <a name="hourly-metrics"></a><span data-ttu-id="6b038-147">Hourly metrics</span><span class="sxs-lookup"><span data-stu-id="6b038-147">Hourly metrics</span></span>
* <span data-ttu-id="6b038-148">$MetricsHourPrimaryTransactionsBlob</span><span class="sxs-lookup"><span data-stu-id="6b038-148">$MetricsHourPrimaryTransactionsBlob</span></span>
* <span data-ttu-id="6b038-149">$MetricsHourPrimaryTransactionsTable</span><span class="sxs-lookup"><span data-stu-id="6b038-149">$MetricsHourPrimaryTransactionsTable</span></span>
* <span data-ttu-id="6b038-150">$MetricsHourPrimaryTransactionsQueue</span><span class="sxs-lookup"><span data-stu-id="6b038-150">$MetricsHourPrimaryTransactionsQueue</span></span>

### <a name="minute-metrics"></a><span data-ttu-id="6b038-151">Minute metrics</span><span class="sxs-lookup"><span data-stu-id="6b038-151">Minute metrics</span></span>
* <span data-ttu-id="6b038-152">$MetricsMinutePrimaryTransactionsBlob</span><span class="sxs-lookup"><span data-stu-id="6b038-152">$MetricsMinutePrimaryTransactionsBlob</span></span>
* <span data-ttu-id="6b038-153">$MetricsMinutePrimaryTransactionsTable</span><span class="sxs-lookup"><span data-stu-id="6b038-153">$MetricsMinutePrimaryTransactionsTable</span></span>
* <span data-ttu-id="6b038-154">$MetricsMinutePrimaryTransactionsQueue</span><span class="sxs-lookup"><span data-stu-id="6b038-154">$MetricsMinutePrimaryTransactionsQueue</span></span>

### <a name="capacity"></a><span data-ttu-id="6b038-155">Capacity</span><span class="sxs-lookup"><span data-stu-id="6b038-155">Capacity</span></span>
* <span data-ttu-id="6b038-156">$MetricsCapacityBlob</span><span class="sxs-lookup"><span data-stu-id="6b038-156">$MetricsCapacityBlob</span></span>

<span data-ttu-id="6b038-157">You can find full details of the schemas for these tables at [Storage Analytics Metrics Table Schema](https://msdn.microsoft.com/library/azure/hh343264.aspx).</span><span class="sxs-lookup"><span data-stu-id="6b038-157">You can find full details of the schemas for these tables at [Storage Analytics Metrics Table Schema](https://msdn.microsoft.com/library/azure/hh343264.aspx).</span></span> <span data-ttu-id="6b038-158">The sample rows below show only a subset of the columns available, but illustrate some important features of the way Storage Metrics saves these metrics:</span><span class="sxs-lookup"><span data-stu-id="6b038-158">The sample rows below show only a subset of the columns available, but illustrate some important features of the way Storage Metrics saves these metrics:</span></span>

| <span data-ttu-id="6b038-159">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="6b038-159">PartitionKey</span></span> | <span data-ttu-id="6b038-160">RowKey</span><span class="sxs-lookup"><span data-stu-id="6b038-160">RowKey</span></span> | <span data-ttu-id="6b038-161">Timestamp</span><span class="sxs-lookup"><span data-stu-id="6b038-161">Timestamp</span></span> | <span data-ttu-id="6b038-162">TotalRequests</span><span class="sxs-lookup"><span data-stu-id="6b038-162">TotalRequests</span></span> | <span data-ttu-id="6b038-163">TotalBillableRequests</span><span class="sxs-lookup"><span data-stu-id="6b038-163">TotalBillableRequests</span></span> | <span data-ttu-id="6b038-164">TotalIngress</span><span class="sxs-lookup"><span data-stu-id="6b038-164">TotalIngress</span></span> | <span data-ttu-id="6b038-165">TotalEgress</span><span class="sxs-lookup"><span data-stu-id="6b038-165">TotalEgress</span></span> | <span data-ttu-id="6b038-166">Availability</span><span class="sxs-lookup"><span data-stu-id="6b038-166">Availability</span></span> | <span data-ttu-id="6b038-167">AverageE2ELatency</span><span class="sxs-lookup"><span data-stu-id="6b038-167">AverageE2ELatency</span></span> | <span data-ttu-id="6b038-168">AverageServerLatency</span><span class="sxs-lookup"><span data-stu-id="6b038-168">AverageServerLatency</span></span> | <span data-ttu-id="6b038-169">PercentSuccess</span><span class="sxs-lookup"><span data-stu-id="6b038-169">PercentSuccess</span></span> |
| --- |:---:| ---:| --- | --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="6b038-170">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="6b038-170">20140522T1100</span></span> |<span data-ttu-id="6b038-171">user;All</span><span class="sxs-lookup"><span data-stu-id="6b038-171">user;All</span></span> |<span data-ttu-id="6b038-172">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="6b038-172">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="6b038-173">7</span><span class="sxs-lookup"><span data-stu-id="6b038-173">7</span></span> |<span data-ttu-id="6b038-174">7</span><span class="sxs-lookup"><span data-stu-id="6b038-174">7</span></span> |<span data-ttu-id="6b038-175">4003</span><span class="sxs-lookup"><span data-stu-id="6b038-175">4003</span></span> |<span data-ttu-id="6b038-176">46801</span><span class="sxs-lookup"><span data-stu-id="6b038-176">46801</span></span> |<span data-ttu-id="6b038-177">100</span><span class="sxs-lookup"><span data-stu-id="6b038-177">100</span></span> |<span data-ttu-id="6b038-178">104.4286</span><span class="sxs-lookup"><span data-stu-id="6b038-178">104.4286</span></span> |<span data-ttu-id="6b038-179">6.857143</span><span class="sxs-lookup"><span data-stu-id="6b038-179">6.857143</span></span> |<span data-ttu-id="6b038-180">100</span><span class="sxs-lookup"><span data-stu-id="6b038-180">100</span></span> |
| <span data-ttu-id="6b038-181">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="6b038-181">20140522T1100</span></span> |<span data-ttu-id="6b038-182">user;QueryEntities</span><span class="sxs-lookup"><span data-stu-id="6b038-182">user;QueryEntities</span></span> |<span data-ttu-id="6b038-183">2014-05-22T11:01:16.7640250Z</span><span class="sxs-lookup"><span data-stu-id="6b038-183">2014-05-22T11:01:16.7640250Z</span></span> |<span data-ttu-id="6b038-184">5</span><span class="sxs-lookup"><span data-stu-id="6b038-184">5</span></span> |<span data-ttu-id="6b038-185">5</span><span class="sxs-lookup"><span data-stu-id="6b038-185">5</span></span> |<span data-ttu-id="6b038-186">2694</span><span class="sxs-lookup"><span data-stu-id="6b038-186">2694</span></span> |<span data-ttu-id="6b038-187">45951</span><span class="sxs-lookup"><span data-stu-id="6b038-187">45951</span></span> |<span data-ttu-id="6b038-188">100</span><span class="sxs-lookup"><span data-stu-id="6b038-188">100</span></span> |<span data-ttu-id="6b038-189">143.8</span><span class="sxs-lookup"><span data-stu-id="6b038-189">143.8</span></span> |<span data-ttu-id="6b038-190">7.8</span><span class="sxs-lookup"><span data-stu-id="6b038-190">7.8</span></span> |<span data-ttu-id="6b038-191">100</span><span class="sxs-lookup"><span data-stu-id="6b038-191">100</span></span> |
| <span data-ttu-id="6b038-192">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="6b038-192">20140522T1100</span></span> |<span data-ttu-id="6b038-193">user;QueryEntity</span><span class="sxs-lookup"><span data-stu-id="6b038-193">user;QueryEntity</span></span> |<span data-ttu-id="6b038-194">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="6b038-194">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="6b038-195">1</span><span class="sxs-lookup"><span data-stu-id="6b038-195">1</span></span> |<span data-ttu-id="6b038-196">1</span><span class="sxs-lookup"><span data-stu-id="6b038-196">1</span></span> |<span data-ttu-id="6b038-197">538</span><span class="sxs-lookup"><span data-stu-id="6b038-197">538</span></span> |<span data-ttu-id="6b038-198">633</span><span class="sxs-lookup"><span data-stu-id="6b038-198">633</span></span> |<span data-ttu-id="6b038-199">100</span><span class="sxs-lookup"><span data-stu-id="6b038-199">100</span></span> |<span data-ttu-id="6b038-200">3</span><span class="sxs-lookup"><span data-stu-id="6b038-200">3</span></span> |<span data-ttu-id="6b038-201">3</span><span class="sxs-lookup"><span data-stu-id="6b038-201">3</span></span> |<span data-ttu-id="6b038-202">100</span><span class="sxs-lookup"><span data-stu-id="6b038-202">100</span></span> |
| <span data-ttu-id="6b038-203">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="6b038-203">20140522T1100</span></span> |<span data-ttu-id="6b038-204">user;UpdateEntity</span><span class="sxs-lookup"><span data-stu-id="6b038-204">user;UpdateEntity</span></span> |<span data-ttu-id="6b038-205">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="6b038-205">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="6b038-206">1</span><span class="sxs-lookup"><span data-stu-id="6b038-206">1</span></span> |<span data-ttu-id="6b038-207">1</span><span class="sxs-lookup"><span data-stu-id="6b038-207">1</span></span> |<span data-ttu-id="6b038-208">771</span><span class="sxs-lookup"><span data-stu-id="6b038-208">771</span></span> |<span data-ttu-id="6b038-209">217</span><span class="sxs-lookup"><span data-stu-id="6b038-209">217</span></span> |<span data-ttu-id="6b038-210">100</span><span class="sxs-lookup"><span data-stu-id="6b038-210">100</span></span> |<span data-ttu-id="6b038-211">9</span><span class="sxs-lookup"><span data-stu-id="6b038-211">9</span></span> |<span data-ttu-id="6b038-212">6</span><span class="sxs-lookup"><span data-stu-id="6b038-212">6</span></span> |<span data-ttu-id="6b038-213">100</span><span class="sxs-lookup"><span data-stu-id="6b038-213">100</span></span> |

<span data-ttu-id="6b038-214">In this example minute metrics data, the partition key uses the time at minute resolution.</span><span class="sxs-lookup"><span data-stu-id="6b038-214">In this example minute metrics data, the partition key uses the time at minute resolution.</span></span> <span data-ttu-id="6b038-215">The row key identifies the type of information that is stored in the row and this is composed of two pieces of information, the access type, and the request type:</span><span class="sxs-lookup"><span data-stu-id="6b038-215">The row key identifies the type of information that is stored in the row and this is composed of two pieces of information, the access type, and the request type:</span></span>

* <span data-ttu-id="6b038-216">The access type is either user or system, where user refers to all user requests to the storage service, and system refers to requests made by Storage Analytics.</span><span class="sxs-lookup"><span data-stu-id="6b038-216">The access type is either user or system, where user refers to all user requests to the storage service, and system refers to requests made by Storage Analytics.</span></span>
* <span data-ttu-id="6b038-217">The request type is either all in which case it is a summary line, or it identifies the specific API such as QueryEntity or UpdateEntity.</span><span class="sxs-lookup"><span data-stu-id="6b038-217">The request type is either all in which case it is a summary line, or it identifies the specific API such as QueryEntity or UpdateEntity.</span></span>

<span data-ttu-id="6b038-218">The sample data above shows all the records for a single minute (starting at 11:00AM), so the number of QueryEntities requests plus the number of QueryEntity requests plus the number of UpdateEntity requests add up to seven, which is the total shown on the user:All row.</span><span class="sxs-lookup"><span data-stu-id="6b038-218">The sample data above shows all the records for a single minute (starting at 11:00AM), so the number of QueryEntities requests plus the number of QueryEntity requests plus the number of UpdateEntity requests add up to seven, which is the total shown on the user:All row.</span></span> <span data-ttu-id="6b038-219">Similarly, you can derive the average end-to-end latency 104.4286 on the user:All row by calculating ((143.8 \* 5) + 3 + 9)/7.</span><span class="sxs-lookup"><span data-stu-id="6b038-219">Similarly, you can derive the average end-to-end latency 104.4286 on the user:All row by calculating ((143.8 \* 5) + 3 + 9)/7.</span></span>

## <a name="metrics-alerts"></a><span data-ttu-id="6b038-220">Metrics alerts</span><span class="sxs-lookup"><span data-stu-id="6b038-220">Metrics alerts</span></span>
<span data-ttu-id="6b038-221">You should consider setting up alerts in the [Azure portal](https://portal.azure.com) so Storage Metrics can automatically notify you of important changes in the behavior of your storage services.</span><span class="sxs-lookup"><span data-stu-id="6b038-221">You should consider setting up alerts in the [Azure portal](https://portal.azure.com) so Storage Metrics can automatically notify you of important changes in the behavior of your storage services.</span></span> <span data-ttu-id="6b038-222">If you use a storage explorer tool to download this metrics data in a delimited format, you can use Microsoft Excel to analyze the data.</span><span class="sxs-lookup"><span data-stu-id="6b038-222">If you use a storage explorer tool to download this metrics data in a delimited format, you can use Microsoft Excel to analyze the data.</span></span> <span data-ttu-id="6b038-223">See [Azure Storage Client Tools](storage-explorers.md) for a list of available storage explorer tools.</span><span class="sxs-lookup"><span data-stu-id="6b038-223">See [Azure Storage Client Tools](storage-explorers.md) for a list of available storage explorer tools.</span></span> <span data-ttu-id="6b038-224">You can configure alerts in the **Alert rules** blade, accessible under **Monitoring** in the Storage account menu blade.</span><span class="sxs-lookup"><span data-stu-id="6b038-224">You can configure alerts in the **Alert rules** blade, accessible under **Monitoring** in the Storage account menu blade.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6b038-225">There may be a delay between a storage event and when the corresponding hourly or minute metrics data is recorded.</span><span class="sxs-lookup"><span data-stu-id="6b038-225">There may be a delay between a storage event and when the corresponding hourly or minute metrics data is recorded.</span></span> <span data-ttu-id="6b038-226">In the case of minute metrics, several minutes of data may be written at once.</span><span class="sxs-lookup"><span data-stu-id="6b038-226">In the case of minute metrics, several minutes of data may be written at once.</span></span> <span data-ttu-id="6b038-227">This can lead to transactions from earlier minutes being aggregated into the transaction for the current minute.</span><span class="sxs-lookup"><span data-stu-id="6b038-227">This can lead to transactions from earlier minutes being aggregated into the transaction for the current minute.</span></span> <span data-ttu-id="6b038-228">When this happens, the alert service may not have all available metrics data for the configured alert interval, which may lead to alerts firing unexpectedly.</span><span class="sxs-lookup"><span data-stu-id="6b038-228">When this happens, the alert service may not have all available metrics data for the configured alert interval, which may lead to alerts firing unexpectedly.</span></span>
>

## <a name="accessing-metrics-data-programmatically"></a><span data-ttu-id="6b038-229">Accessing metrics data programmatically</span><span class="sxs-lookup"><span data-stu-id="6b038-229">Accessing metrics data programmatically</span></span>
<span data-ttu-id="6b038-230">The following listing shows sample C# code that accesses the minute metrics for a range of minutes and displays the results in a console Window.</span><span class="sxs-lookup"><span data-stu-id="6b038-230">The following listing shows sample C# code that accesses the minute metrics for a range of minutes and displays the results in a console Window.</span></span> <span data-ttu-id="6b038-231">It uses the Azure Storage Library version 4 that includes the CloudAnalyticsClient class that simplifies accessing the metrics tables in storage.</span><span class="sxs-lookup"><span data-stu-id="6b038-231">It uses the Azure Storage Library version 4 that includes the CloudAnalyticsClient class that simplifies accessing the metrics tables in storage.</span></span>

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

## <a name="what-charges-do-you-incur-when-you-enable-storage-metrics"></a><span data-ttu-id="6b038-232">What charges do you incur when you enable storage metrics?</span><span class="sxs-lookup"><span data-stu-id="6b038-232">What charges do you incur when you enable storage metrics?</span></span>
<span data-ttu-id="6b038-233">Write requests to create table entities for metrics are charged at the standard rates applicable to all Azure Storage operations.</span><span class="sxs-lookup"><span data-stu-id="6b038-233">Write requests to create table entities for metrics are charged at the standard rates applicable to all Azure Storage operations.</span></span>

<span data-ttu-id="6b038-234">Read and delete requests by a client to metrics data are also billable at standard rates.</span><span class="sxs-lookup"><span data-stu-id="6b038-234">Read and delete requests by a client to metrics data are also billable at standard rates.</span></span> <span data-ttu-id="6b038-235">If you have configured a data retention policy, you are not charged when Azure Storage deletes old metrics data.</span><span class="sxs-lookup"><span data-stu-id="6b038-235">If you have configured a data retention policy, you are not charged when Azure Storage deletes old metrics data.</span></span> <span data-ttu-id="6b038-236">However, if you delete analytics data, your account is charged for the delete operations.</span><span class="sxs-lookup"><span data-stu-id="6b038-236">However, if you delete analytics data, your account is charged for the delete operations.</span></span>

<span data-ttu-id="6b038-237">The capacity used by the metrics tables is also billable: you can use the following to estimate the amount of capacity used for storing metrics data:</span><span class="sxs-lookup"><span data-stu-id="6b038-237">The capacity used by the metrics tables is also billable: you can use the following to estimate the amount of capacity used for storing metrics data:</span></span>

* <span data-ttu-id="6b038-238">If each hour a service utilizes every API in every service, then approximately 148KB of data is stored every hour in the metrics transaction tables if you have enabled both service and API level summary.</span><span class="sxs-lookup"><span data-stu-id="6b038-238">If each hour a service utilizes every API in every service, then approximately 148KB of data is stored every hour in the metrics transaction tables if you have enabled both service and API level summary.</span></span>
* <span data-ttu-id="6b038-239">If each hour a service utilizes every API in every service, then approximately 12KB of data is stored every hour in the metrics transaction tables if you have enabled just service level summary.</span><span class="sxs-lookup"><span data-stu-id="6b038-239">If each hour a service utilizes every API in every service, then approximately 12KB of data is stored every hour in the metrics transaction tables if you have enabled just service level summary.</span></span>
* <span data-ttu-id="6b038-240">The capacity table for blobs has two rows added each day (provided user has opted in for logs): this implies that every day the size of this table increases by up to approximately 300 bytes.</span><span class="sxs-lookup"><span data-stu-id="6b038-240">The capacity table for blobs has two rows added each day (provided user has opted in for logs): this implies that every day the size of this table increases by up to approximately 300 bytes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6b038-241">Next steps</span><span class="sxs-lookup"><span data-stu-id="6b038-241">Next steps</span></span>
[<span data-ttu-id="6b038-242">Enabling Storage Logging and Accessing Log Data</span><span class="sxs-lookup"><span data-stu-id="6b038-242">Enabling Storage Logging and Accessing Log Data</span></span>](/rest/api/storageservices/fileservices/Enabling-Storage-Logging-and-Accessing-Log-Data)