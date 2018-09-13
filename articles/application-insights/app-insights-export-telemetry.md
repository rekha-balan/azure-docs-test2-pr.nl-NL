---
title: Continuous export of telemetry from Application Insights | Microsoft Docs
description: Export diagnostic and usage data to storage in Microsoft Azure, and download it from there.
services: application-insights
documentationcenter: ''
author: alancameronwills
manager: douge
ms.assetid: 5b859200-b484-4c98-9d9f-929713f1030c
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 02/23/2017
ms.author: awills
ms.openlocfilehash: 7f1306f2a563c867ed5a6869cce5b65fd2e5945d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564176"
---
# <a name="export-telemetry-from-application-insights"></a><span data-ttu-id="3202c-103">Export telemetry from Application Insights</span><span class="sxs-lookup"><span data-stu-id="3202c-103">Export telemetry from Application Insights</span></span>
<span data-ttu-id="3202c-104">Want to keep your telemetry for longer than the standard retention period?</span><span class="sxs-lookup"><span data-stu-id="3202c-104">Want to keep your telemetry for longer than the standard retention period?</span></span> <span data-ttu-id="3202c-105">Or process it in some specialized way?</span><span class="sxs-lookup"><span data-stu-id="3202c-105">Or process it in some specialized way?</span></span> <span data-ttu-id="3202c-106">Continuous Export is ideal for this.</span><span class="sxs-lookup"><span data-stu-id="3202c-106">Continuous Export is ideal for this.</span></span> <span data-ttu-id="3202c-107">The events you see in the Application Insights portal can be exported to storage in Microsoft Azure in JSON format.</span><span class="sxs-lookup"><span data-stu-id="3202c-107">The events you see in the Application Insights portal can be exported to storage in Microsoft Azure in JSON format.</span></span> <span data-ttu-id="3202c-108">From there you can download your data and write whatever code you need to process it.</span><span class="sxs-lookup"><span data-stu-id="3202c-108">From there you can download your data and write whatever code you need to process it.</span></span>  

<span data-ttu-id="3202c-109">Using Continuous Export may incur an additional charge.</span><span class="sxs-lookup"><span data-stu-id="3202c-109">Using Continuous Export may incur an additional charge.</span></span> <span data-ttu-id="3202c-110">Check your [pricing model](http://azure.microsoft.com/pricing/details/application-insights/).</span><span class="sxs-lookup"><span data-stu-id="3202c-110">Check your [pricing model](http://azure.microsoft.com/pricing/details/application-insights/).</span></span>

<span data-ttu-id="3202c-111">Before you set up continuous export, there are some alternatives you might want to consider:</span><span class="sxs-lookup"><span data-stu-id="3202c-111">Before you set up continuous export, there are some alternatives you might want to consider:</span></span>

* <span data-ttu-id="3202c-112">The Export button at the top of a metrics or search blade lets you transfer tables and charts to an Excel spreadsheet.</span><span class="sxs-lookup"><span data-stu-id="3202c-112">The Export button at the top of a metrics or search blade lets you transfer tables and charts to an Excel spreadsheet.</span></span>

* <span data-ttu-id="3202c-113">[Analytics](app-insights-analytics.md) provides a powerful query language for telemetry.</span><span class="sxs-lookup"><span data-stu-id="3202c-113">[Analytics](app-insights-analytics.md) provides a powerful query language for telemetry.</span></span> <span data-ttu-id="3202c-114">It can also export results.</span><span class="sxs-lookup"><span data-stu-id="3202c-114">It can also export results.</span></span>
* <span data-ttu-id="3202c-115">If you're looking to [explore your data in Power BI](app-insights-export-power-bi.md), you can do that without using Continuous Export.</span><span class="sxs-lookup"><span data-stu-id="3202c-115">If you're looking to [explore your data in Power BI](app-insights-export-power-bi.md), you can do that without using Continuous Export.</span></span>
* <span data-ttu-id="3202c-116">The [Data access REST API](https://dev.applicationinsights.io/) lets you access your telemetry programmatically.</span><span class="sxs-lookup"><span data-stu-id="3202c-116">The [Data access REST API](https://dev.applicationinsights.io/) lets you access your telemetry programmatically.</span></span>

<span data-ttu-id="3202c-117">After Continuous Export copies your data to storage (where it can stay for as long as you like), it's still available in Application Insights for the usual [retention period](app-insights-data-retention-privacy.md).</span><span class="sxs-lookup"><span data-stu-id="3202c-117">After Continuous Export copies your data to storage (where it can stay for as long as you like), it's still available in Application Insights for the usual [retention period](app-insights-data-retention-privacy.md).</span></span>

## <a name="setup"></a> <span data-ttu-id="3202c-118">Create a Continuous Export</span><span class="sxs-lookup"><span data-stu-id="3202c-118">Create a Continuous Export</span></span>
1. <span data-ttu-id="3202c-119">In the Application Insights resource for your app, open Continuous Export and choose **Add**:</span><span class="sxs-lookup"><span data-stu-id="3202c-119">In the Application Insights resource for your app, open Continuous Export and choose **Add**:</span></span>

    ![Scroll down and click Continuous Export](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-export-telemetry/01-export.png)

2. <span data-ttu-id="3202c-121">Choose the telemetry data types you want to export.</span><span class="sxs-lookup"><span data-stu-id="3202c-121">Choose the telemetry data types you want to export.</span></span>

3. <span data-ttu-id="3202c-122">Create or select an [Azure storage account](../storage/storage-introduction.md) where you want to store the data.</span><span class="sxs-lookup"><span data-stu-id="3202c-122">Create or select an [Azure storage account](../storage/storage-introduction.md) where you want to store the data.</span></span>

    > [!Warning]
    > <span data-ttu-id="3202c-123">By default, the storage location will be set to the same geographical region as your Application Insights resource.</span><span class="sxs-lookup"><span data-stu-id="3202c-123">By default, the storage location will be set to the same geographical region as your Application Insights resource.</span></span> <span data-ttu-id="3202c-124">If you store in a different region, you may incur transfer charges.</span><span class="sxs-lookup"><span data-stu-id="3202c-124">If you store in a different region, you may incur transfer charges.</span></span>

    ![Click Add, Export Destination, Storage account, and then either create a new store or choose an existing store](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-export-telemetry/02-add.png)

4. <span data-ttu-id="3202c-126">Create or select a container in the storage:</span><span class="sxs-lookup"><span data-stu-id="3202c-126">Create or select a container in the storage:</span></span>

    ![Click Choose event types](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-export-telemetry/create-container.png)

<span data-ttu-id="3202c-128">Once you've created your export, it starts going.</span><span class="sxs-lookup"><span data-stu-id="3202c-128">Once you've created your export, it starts going.</span></span> <span data-ttu-id="3202c-129">You only get data that arrives after you create the export.</span><span class="sxs-lookup"><span data-stu-id="3202c-129">You only get data that arrives after you create the export.</span></span>

<span data-ttu-id="3202c-130">There can be a delay of about an hour before data appears in the storage.</span><span class="sxs-lookup"><span data-stu-id="3202c-130">There can be a delay of about an hour before data appears in the storage.</span></span>

### <a name="to-edit-continuous-export"></a><span data-ttu-id="3202c-131">To edit continuous export</span><span class="sxs-lookup"><span data-stu-id="3202c-131">To edit continuous export</span></span>

<span data-ttu-id="3202c-132">If you want to change the event types later, just edit the export:</span><span class="sxs-lookup"><span data-stu-id="3202c-132">If you want to change the event types later, just edit the export:</span></span>

![Click Choose event types](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-export-telemetry/05-edit.png)

### <a name="to-stop-continuous-export"></a><span data-ttu-id="3202c-134">To stop continuous export</span><span class="sxs-lookup"><span data-stu-id="3202c-134">To stop continuous export</span></span>

<span data-ttu-id="3202c-135">To stop the export, click Disable.</span><span class="sxs-lookup"><span data-stu-id="3202c-135">To stop the export, click Disable.</span></span> <span data-ttu-id="3202c-136">When you click Enable again, the export will restart with new data.</span><span class="sxs-lookup"><span data-stu-id="3202c-136">When you click Enable again, the export will restart with new data.</span></span> <span data-ttu-id="3202c-137">You won't get the data that arrived in the portal while export was disabled.</span><span class="sxs-lookup"><span data-stu-id="3202c-137">You won't get the data that arrived in the portal while export was disabled.</span></span>

<span data-ttu-id="3202c-138">To stop the export permanently, delete it.</span><span class="sxs-lookup"><span data-stu-id="3202c-138">To stop the export permanently, delete it.</span></span> <span data-ttu-id="3202c-139">Doing so doesn't delete your data from storage.</span><span class="sxs-lookup"><span data-stu-id="3202c-139">Doing so doesn't delete your data from storage.</span></span>

### <a name="cant-add-or-change-an-export"></a><span data-ttu-id="3202c-140">Can't add or change an export?</span><span class="sxs-lookup"><span data-stu-id="3202c-140">Can't add or change an export?</span></span>
* <span data-ttu-id="3202c-141">To add or change exports, you need Owner, Contributor or Application Insights Contributor access rights.</span><span class="sxs-lookup"><span data-stu-id="3202c-141">To add or change exports, you need Owner, Contributor or Application Insights Contributor access rights.</span></span> <span data-ttu-id="3202c-142">[Learn about roles][roles].</span><span class="sxs-lookup"><span data-stu-id="3202c-142">[Learn about roles][roles].</span></span>

## <a name="analyze"></a> <span data-ttu-id="3202c-143">What events do you get?</span><span class="sxs-lookup"><span data-stu-id="3202c-143">What events do you get?</span></span>
<span data-ttu-id="3202c-144">The exported data is the raw telemetry we receive from your application, except that we add location data which we calculate from the client IP address.</span><span class="sxs-lookup"><span data-stu-id="3202c-144">The exported data is the raw telemetry we receive from your application, except that we add location data which we calculate from the client IP address.</span></span>

<span data-ttu-id="3202c-145">Data that has been discarded by [sampling](app-insights-sampling.md) is not included in the exported data.</span><span class="sxs-lookup"><span data-stu-id="3202c-145">Data that has been discarded by [sampling](app-insights-sampling.md) is not included in the exported data.</span></span>

<span data-ttu-id="3202c-146">Other calculated metrics are not included.</span><span class="sxs-lookup"><span data-stu-id="3202c-146">Other calculated metrics are not included.</span></span> <span data-ttu-id="3202c-147">For example, we don't export average CPU utilisation, but we do export the raw telemetry from which the average is computed.</span><span class="sxs-lookup"><span data-stu-id="3202c-147">For example, we don't export average CPU utilisation, but we do export the raw telemetry from which the average is computed.</span></span>

<span data-ttu-id="3202c-148">The data also includes the results of any [availability web tests](app-insights-monitor-web-app-availability.md) that you have set up.</span><span class="sxs-lookup"><span data-stu-id="3202c-148">The data also includes the results of any [availability web tests](app-insights-monitor-web-app-availability.md) that you have set up.</span></span>

> [!NOTE]
> <span data-ttu-id="3202c-149">**Sampling.**</span><span class="sxs-lookup"><span data-stu-id="3202c-149">**Sampling.**</span></span> <span data-ttu-id="3202c-150">If your application sends a lot of data, the sampling feature may operate and send only a fraction of the generated telemetry.</span><span class="sxs-lookup"><span data-stu-id="3202c-150">If your application sends a lot of data, the sampling feature may operate and send only a fraction of the generated telemetry.</span></span> [<span data-ttu-id="3202c-151">Learn more about sampling.</span><span class="sxs-lookup"><span data-stu-id="3202c-151">Learn more about sampling.</span></span>](app-insights-sampling.md)
>
>

## <a name="get"></a> <span data-ttu-id="3202c-152">Inspect the data</span><span class="sxs-lookup"><span data-stu-id="3202c-152">Inspect the data</span></span>
<span data-ttu-id="3202c-153">You can inspect the storage directly in the portal.</span><span class="sxs-lookup"><span data-stu-id="3202c-153">You can inspect the storage directly in the portal.</span></span> <span data-ttu-id="3202c-154">Click **Browse**, select your storage account, and then open **Containers**.</span><span class="sxs-lookup"><span data-stu-id="3202c-154">Click **Browse**, select your storage account, and then open **Containers**.</span></span>

<span data-ttu-id="3202c-155">To inspect Azure storage in Visual Studio, open **View**, **Cloud Explorer**.</span><span class="sxs-lookup"><span data-stu-id="3202c-155">To inspect Azure storage in Visual Studio, open **View**, **Cloud Explorer**.</span></span> <span data-ttu-id="3202c-156">(If you don't have that menu command, you need to install the Azure SDK: Open the **New Project** dialog, expand Visual C#/Cloud and choose **Get Microsoft Azure SDK for .NET**.)</span><span class="sxs-lookup"><span data-stu-id="3202c-156">(If you don't have that menu command, you need to install the Azure SDK: Open the **New Project** dialog, expand Visual C#/Cloud and choose **Get Microsoft Azure SDK for .NET**.)</span></span>

<span data-ttu-id="3202c-157">When you open your blob store, you'll see a container with a set of blob files.</span><span class="sxs-lookup"><span data-stu-id="3202c-157">When you open your blob store, you'll see a container with a set of blob files.</span></span> <span data-ttu-id="3202c-158">The URI of each file derived from your Application Insights resource name, its instrumentation key, telemetry-type/date/time.</span><span class="sxs-lookup"><span data-stu-id="3202c-158">The URI of each file derived from your Application Insights resource name, its instrumentation key, telemetry-type/date/time.</span></span> <span data-ttu-id="3202c-159">(The resource name is all lowercase, and the instrumentation key omits dashes.)</span><span class="sxs-lookup"><span data-stu-id="3202c-159">(The resource name is all lowercase, and the instrumentation key omits dashes.)</span></span>

![Inspect the blob store with a suitable tool](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-export-telemetry/04-data.png)

<span data-ttu-id="3202c-161">The date and time are UTC and are when the telemetry was deposited in the store - not the time it was generated.</span><span class="sxs-lookup"><span data-stu-id="3202c-161">The date and time are UTC and are when the telemetry was deposited in the store - not the time it was generated.</span></span> <span data-ttu-id="3202c-162">So if you write code to download the data, it can move linearly through the data.</span><span class="sxs-lookup"><span data-stu-id="3202c-162">So if you write code to download the data, it can move linearly through the data.</span></span>

<span data-ttu-id="3202c-163">Here's the form of the path:</span><span class="sxs-lookup"><span data-stu-id="3202c-163">Here's the form of the path:</span></span>

    $"{applicationName}_{instrumentationKey}/{type}/{blobDeliveryTimeUtc:yyyy-MM-dd}/{ blobDeliveryTimeUtc:HH}/{blobId}_{blobCreationTimeUtc:yyyyMMdd_HHmmss}.blob"

<span data-ttu-id="3202c-164">Where</span><span class="sxs-lookup"><span data-stu-id="3202c-164">Where</span></span>

* <span data-ttu-id="3202c-165">`blobCreationTimeUtc` is time when blob was created in the internal staging storage</span><span class="sxs-lookup"><span data-stu-id="3202c-165">`blobCreationTimeUtc` is time when blob was created in the internal staging storage</span></span>
* <span data-ttu-id="3202c-166">`blobDeliveryTimeUtc` is the time when blob is copied to the export destination storage</span><span class="sxs-lookup"><span data-stu-id="3202c-166">`blobDeliveryTimeUtc` is the time when blob is copied to the export destination storage</span></span>

## <a name="format"></a> <span data-ttu-id="3202c-167">Data format</span><span class="sxs-lookup"><span data-stu-id="3202c-167">Data format</span></span>
* <span data-ttu-id="3202c-168">Each blob is a text file that contains multiple '\n'-separated rows.</span><span class="sxs-lookup"><span data-stu-id="3202c-168">Each blob is a text file that contains multiple '\n'-separated rows.</span></span> <span data-ttu-id="3202c-169">It contains the telemetry processed over a time period of roughly half a minute.</span><span class="sxs-lookup"><span data-stu-id="3202c-169">It contains the telemetry processed over a time period of roughly half a minute.</span></span>
* <span data-ttu-id="3202c-170">Each row represents a telemetry data point such as a request or page view.</span><span class="sxs-lookup"><span data-stu-id="3202c-170">Each row represents a telemetry data point such as a request or page view.</span></span>
* <span data-ttu-id="3202c-171">Each row is an unformatted JSON document.</span><span class="sxs-lookup"><span data-stu-id="3202c-171">Each row is an unformatted JSON document.</span></span> <span data-ttu-id="3202c-172">If you want to sit and stare at it, open it in Visual Studio and choose Edit, Advanced, Format File:</span><span class="sxs-lookup"><span data-stu-id="3202c-172">If you want to sit and stare at it, open it in Visual Studio and choose Edit, Advanced, Format File:</span></span>

![View the telemetry with a suitable tool](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-export-telemetry/06-json.png)

<span data-ttu-id="3202c-174">Time durations are in ticks, where 10 000 ticks = 1ms.</span><span class="sxs-lookup"><span data-stu-id="3202c-174">Time durations are in ticks, where 10 000 ticks = 1ms.</span></span> <span data-ttu-id="3202c-175">For example, these values show a time of 1ms to send a request from the browser, 3ms to receive it, and 1.8s to process the page in the browser:</span><span class="sxs-lookup"><span data-stu-id="3202c-175">For example, these values show a time of 1ms to send a request from the browser, 3ms to receive it, and 1.8s to process the page in the browser:</span></span>

    "sendRequest": {"value": 10000.0},
    "receiveRequest": {"value": 30000.0},
    "clientProcess": {"value": 17970000.0}

[<span data-ttu-id="3202c-176">Detailed data model reference for the property types and values.</span><span class="sxs-lookup"><span data-stu-id="3202c-176">Detailed data model reference for the property types and values.</span></span>](app-insights-export-data-model.md)

## <a name="processing-the-data"></a><span data-ttu-id="3202c-177">Processing the data</span><span class="sxs-lookup"><span data-stu-id="3202c-177">Processing the data</span></span>
<span data-ttu-id="3202c-178">On a small scale, you can write some code to pull apart your data, read it into a spreadsheet, and so on.</span><span class="sxs-lookup"><span data-stu-id="3202c-178">On a small scale, you can write some code to pull apart your data, read it into a spreadsheet, and so on.</span></span> <span data-ttu-id="3202c-179">For example:</span><span class="sxs-lookup"><span data-stu-id="3202c-179">For example:</span></span>

    private IEnumerable<T> DeserializeMany<T>(string folderName)
    {
      var files = Directory.EnumerateFiles(folderName, "*.blob", SearchOption.AllDirectories);
      foreach (var file in files)
      {
         using (var fileReader = File.OpenText(file))
         {
            string fileContent = fileReader.ReadToEnd();
            IEnumerable<string> entities = fileContent.Split('\n').Where(s => !string.IsNullOrWhiteSpace(s));
            foreach (var entity in entities)
            {
                yield return JsonConvert.DeserializeObject<T>(entity);
            }
         }
      }
    }

<span data-ttu-id="3202c-180">For a larger code sample, see [using a worker role][exportasa].</span><span class="sxs-lookup"><span data-stu-id="3202c-180">For a larger code sample, see [using a worker role][exportasa].</span></span>

## <a name="delete"></a><span data-ttu-id="3202c-181">Delete your old data</span><span class="sxs-lookup"><span data-stu-id="3202c-181">Delete your old data</span></span>
<span data-ttu-id="3202c-182">Please note that you are responsible for managing your storage capacity and deleting the old data if necessary.</span><span class="sxs-lookup"><span data-stu-id="3202c-182">Please note that you are responsible for managing your storage capacity and deleting the old data if necessary.</span></span>

## <a name="if-you-regenerate-your-storage-key"></a><span data-ttu-id="3202c-183">If you regenerate your storage key...</span><span class="sxs-lookup"><span data-stu-id="3202c-183">If you regenerate your storage key...</span></span>
<span data-ttu-id="3202c-184">If you change the key to your storage, continuous export will stop working.</span><span class="sxs-lookup"><span data-stu-id="3202c-184">If you change the key to your storage, continuous export will stop working.</span></span> <span data-ttu-id="3202c-185">You'll see a notification in your Azure account.</span><span class="sxs-lookup"><span data-stu-id="3202c-185">You'll see a notification in your Azure account.</span></span>

<span data-ttu-id="3202c-186">Open the Continuous Export blade and edit your export.</span><span class="sxs-lookup"><span data-stu-id="3202c-186">Open the Continuous Export blade and edit your export.</span></span> <span data-ttu-id="3202c-187">Edit the Export Destination, but just leave the same storage selected.</span><span class="sxs-lookup"><span data-stu-id="3202c-187">Edit the Export Destination, but just leave the same storage selected.</span></span> <span data-ttu-id="3202c-188">Click OK to confirm.</span><span class="sxs-lookup"><span data-stu-id="3202c-188">Click OK to confirm.</span></span>

![Edit the continuous export, open and close thee export destination.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-export-telemetry/07-resetstore.png)

<span data-ttu-id="3202c-190">The continuous export will restart.</span><span class="sxs-lookup"><span data-stu-id="3202c-190">The continuous export will restart.</span></span>

## <a name="export-samples"></a><span data-ttu-id="3202c-191">Export samples</span><span class="sxs-lookup"><span data-stu-id="3202c-191">Export samples</span></span>

* <span data-ttu-id="3202c-192">[Export to SQL using Stream Analytics][exportasa]</span><span class="sxs-lookup"><span data-stu-id="3202c-192">[Export to SQL using Stream Analytics][exportasa]</span></span>
* [<span data-ttu-id="3202c-193">Stream Analytics sample 2</span><span class="sxs-lookup"><span data-stu-id="3202c-193">Stream Analytics sample 2</span></span>](app-insights-export-stream-analytics.md)

<span data-ttu-id="3202c-194">On larger scales, consider [HDInsight](https://azure.microsoft.com/services/hdinsight/) - Hadoop clusters in the cloud.</span><span class="sxs-lookup"><span data-stu-id="3202c-194">On larger scales, consider [HDInsight](https://azure.microsoft.com/services/hdinsight/) - Hadoop clusters in the cloud.</span></span> <span data-ttu-id="3202c-195">HDInsight provides a variety of technologies for managing and analyzing big data, and you could use it to process data that has been exported from Application Insights.</span><span class="sxs-lookup"><span data-stu-id="3202c-195">HDInsight provides a variety of technologies for managing and analyzing big data, and you could use it to process data that has been exported from Application Insights.</span></span>

## <a name="q--a"></a><span data-ttu-id="3202c-196">Q & A</span><span class="sxs-lookup"><span data-stu-id="3202c-196">Q & A</span></span>
* <span data-ttu-id="3202c-197">*But all I want is a one-time download of a chart.*</span><span class="sxs-lookup"><span data-stu-id="3202c-197">*But all I want is a one-time download of a chart.*</span></span>  

    <span data-ttu-id="3202c-198">Yes, you can do that.</span><span class="sxs-lookup"><span data-stu-id="3202c-198">Yes, you can do that.</span></span> <span data-ttu-id="3202c-199">At the top of the blade, click **Export Data**.</span><span class="sxs-lookup"><span data-stu-id="3202c-199">At the top of the blade, click **Export Data**.</span></span>
* <span data-ttu-id="3202c-200">*I set up an export, but there's no data in my store.*</span><span class="sxs-lookup"><span data-stu-id="3202c-200">*I set up an export, but there's no data in my store.*</span></span>

    <span data-ttu-id="3202c-201">Did Application Insights receive any telemetry from your app since you set up the export?</span><span class="sxs-lookup"><span data-stu-id="3202c-201">Did Application Insights receive any telemetry from your app since you set up the export?</span></span> <span data-ttu-id="3202c-202">You'll only receive new data.</span><span class="sxs-lookup"><span data-stu-id="3202c-202">You'll only receive new data.</span></span>
* <span data-ttu-id="3202c-203">*I tried to set up an export, but was denied access*</span><span class="sxs-lookup"><span data-stu-id="3202c-203">*I tried to set up an export, but was denied access*</span></span>

    <span data-ttu-id="3202c-204">If the account is owned by your organization, you have to be a member of the owners or contributors groups.</span><span class="sxs-lookup"><span data-stu-id="3202c-204">If the account is owned by your organization, you have to be a member of the owners or contributors groups.</span></span>
* <span data-ttu-id="3202c-205">*Can I export straight to my own on-premises store?*</span><span class="sxs-lookup"><span data-stu-id="3202c-205">*Can I export straight to my own on-premises store?*</span></span>

    <span data-ttu-id="3202c-206">No, sorry.</span><span class="sxs-lookup"><span data-stu-id="3202c-206">No, sorry.</span></span> <span data-ttu-id="3202c-207">Our export engine currently only works with Azure storage at this time.</span><span class="sxs-lookup"><span data-stu-id="3202c-207">Our export engine currently only works with Azure storage at this time.</span></span>  
* <span data-ttu-id="3202c-208">*Is there any limit to the amount of data you put in my store?*</span><span class="sxs-lookup"><span data-stu-id="3202c-208">*Is there any limit to the amount of data you put in my store?*</span></span>

    <span data-ttu-id="3202c-209">No.</span><span class="sxs-lookup"><span data-stu-id="3202c-209">No.</span></span> <span data-ttu-id="3202c-210">We'll keep pushing data in until you delete the export.</span><span class="sxs-lookup"><span data-stu-id="3202c-210">We'll keep pushing data in until you delete the export.</span></span> <span data-ttu-id="3202c-211">We'll stop if we hit the outer limits for blob storage, but that's pretty huge.</span><span class="sxs-lookup"><span data-stu-id="3202c-211">We'll stop if we hit the outer limits for blob storage, but that's pretty huge.</span></span> <span data-ttu-id="3202c-212">It's up to you to control how much storage you use.</span><span class="sxs-lookup"><span data-stu-id="3202c-212">It's up to you to control how much storage you use.</span></span>  
* <span data-ttu-id="3202c-213">*How many blobs should I see in the storage?*</span><span class="sxs-lookup"><span data-stu-id="3202c-213">*How many blobs should I see in the storage?*</span></span>

  * <span data-ttu-id="3202c-214">For every data type you selected to export, a new blob is created every minute (if data is available).</span><span class="sxs-lookup"><span data-stu-id="3202c-214">For every data type you selected to export, a new blob is created every minute (if data is available).</span></span>
  * <span data-ttu-id="3202c-215">In addition, for applications with high traffic, additional partition units are allocated.</span><span class="sxs-lookup"><span data-stu-id="3202c-215">In addition, for applications with high traffic, additional partition units are allocated.</span></span> <span data-ttu-id="3202c-216">In this case each unit creates a blob every minute.</span><span class="sxs-lookup"><span data-stu-id="3202c-216">In this case each unit creates a blob every minute.</span></span>
* <span data-ttu-id="3202c-217">*I regenerated the key to my storage or changed the name of the container, and now the export doesn't work.*</span><span class="sxs-lookup"><span data-stu-id="3202c-217">*I regenerated the key to my storage or changed the name of the container, and now the export doesn't work.*</span></span>

    <span data-ttu-id="3202c-218">Edit the export and open the export destination blade.</span><span class="sxs-lookup"><span data-stu-id="3202c-218">Edit the export and open the export destination blade.</span></span> <span data-ttu-id="3202c-219">Leave the same storage selected as before, and click OK to confirm.</span><span class="sxs-lookup"><span data-stu-id="3202c-219">Leave the same storage selected as before, and click OK to confirm.</span></span> <span data-ttu-id="3202c-220">Export will restart.</span><span class="sxs-lookup"><span data-stu-id="3202c-220">Export will restart.</span></span> <span data-ttu-id="3202c-221">If the change was within the past few days, you won't lose data.</span><span class="sxs-lookup"><span data-stu-id="3202c-221">If the change was within the past few days, you won't lose data.</span></span>
* <span data-ttu-id="3202c-222">*Can I pause the export?*</span><span class="sxs-lookup"><span data-stu-id="3202c-222">*Can I pause the export?*</span></span>

    <span data-ttu-id="3202c-223">Yes.</span><span class="sxs-lookup"><span data-stu-id="3202c-223">Yes.</span></span> <span data-ttu-id="3202c-224">Click Disable.</span><span class="sxs-lookup"><span data-stu-id="3202c-224">Click Disable.</span></span>

## <a name="code-samples"></a><span data-ttu-id="3202c-225">Code samples</span><span class="sxs-lookup"><span data-stu-id="3202c-225">Code samples</span></span>

* [<span data-ttu-id="3202c-226">Stream Analytics sample</span><span class="sxs-lookup"><span data-stu-id="3202c-226">Stream Analytics sample</span></span>](app-insights-export-stream-analytics.md)
* <span data-ttu-id="3202c-227">[Export to SQL using Stream Analytics][exportasa]</span><span class="sxs-lookup"><span data-stu-id="3202c-227">[Export to SQL using Stream Analytics][exportasa]</span></span>
* [<span data-ttu-id="3202c-228">Detailed data model reference for the property types and values.</span><span class="sxs-lookup"><span data-stu-id="3202c-228">Detailed data model reference for the property types and values.</span></span>](app-insights-export-data-model.md)

<!--Link references-->

[exportasa]: app-insights-code-sample-export-sql-stream-analytics.md
[roles]: app-insights-resources-roles-access-control.md







