---
title: Overview of Azure Event Hubs Capture | Microsoft Docs
description: Capture telemetry data with Event Hubs Capture
services: event-hubs
documentationcenter: ''
author: ShubhaVijayasarathy
manager: timlt
editor: ''
ms.assetid: e53cdeea-8a6a-474e-9f96-59d43c0e8562
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/16/2018
ms.author: shvija
ms.openlocfilehash: 603a5dfcf2137c15ae19ea248f3e0f4f136c22f1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870124"
---
# <a name="azure-event-hubs-capture"></a><span data-ttu-id="f97be-103">Azure Event Hubs Capture</span><span class="sxs-lookup"><span data-stu-id="f97be-103">Azure Event Hubs Capture</span></span>

<span data-ttu-id="f97be-104">Azure Event Hubs Capture enables you to automatically deliver the streaming data in Event Hubs to an [Azure Blob storage](https://azure.microsoft.com/services/storage/blobs/) or [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/) account of your choice, with the added flexibility of specifying a time or size interval.</span><span class="sxs-lookup"><span data-stu-id="f97be-104">Azure Event Hubs Capture enables you to automatically deliver the streaming data in Event Hubs to an [Azure Blob storage](https://azure.microsoft.com/services/storage/blobs/) or [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/) account of your choice, with the added flexibility of specifying a time or size interval.</span></span> <span data-ttu-id="f97be-105">Setting up Capture is fast, there are no administrative costs to run it, and it scales automatically with Event Hubs [throughput units](event-hubs-features.md#capacity).</span><span class="sxs-lookup"><span data-stu-id="f97be-105">Setting up Capture is fast, there are no administrative costs to run it, and it scales automatically with Event Hubs [throughput units](event-hubs-features.md#capacity).</span></span> <span data-ttu-id="f97be-106">Event Hubs Capture is the easiest way to load streaming data into Azure, and enables you to focus on data processing rather than on data capture.</span><span class="sxs-lookup"><span data-stu-id="f97be-106">Event Hubs Capture is the easiest way to load streaming data into Azure, and enables you to focus on data processing rather than on data capture.</span></span>

<span data-ttu-id="f97be-107">Event Hubs Capture enables you to process real-time and batch-based pipelines on the same stream.</span><span class="sxs-lookup"><span data-stu-id="f97be-107">Event Hubs Capture enables you to process real-time and batch-based pipelines on the same stream.</span></span> <span data-ttu-id="f97be-108">This means you can build solutions that grow with your needs over time.</span><span class="sxs-lookup"><span data-stu-id="f97be-108">This means you can build solutions that grow with your needs over time.</span></span> <span data-ttu-id="f97be-109">Whether you're building batch-based systems today with an eye towards future real-time processing, or you want to add an efficient cold path to an existing real-time solution, Event Hubs Capture makes working with streaming data easier.</span><span class="sxs-lookup"><span data-stu-id="f97be-109">Whether you're building batch-based systems today with an eye towards future real-time processing, or you want to add an efficient cold path to an existing real-time solution, Event Hubs Capture makes working with streaming data easier.</span></span>

## <a name="how-event-hubs-capture-works"></a><span data-ttu-id="f97be-110">How Event Hubs Capture works</span><span class="sxs-lookup"><span data-stu-id="f97be-110">How Event Hubs Capture works</span></span>

<span data-ttu-id="f97be-111">Event Hubs is a time-retention durable buffer for telemetry ingress, similar to a distributed log.</span><span class="sxs-lookup"><span data-stu-id="f97be-111">Event Hubs is a time-retention durable buffer for telemetry ingress, similar to a distributed log.</span></span> <span data-ttu-id="f97be-112">The key to scaling in Event Hubs is the [partitioned consumer model](event-hubs-features.md#partitions).</span><span class="sxs-lookup"><span data-stu-id="f97be-112">The key to scaling in Event Hubs is the [partitioned consumer model](event-hubs-features.md#partitions).</span></span> <span data-ttu-id="f97be-113">Each partition is an independent segment of data and is consumed independently.</span><span class="sxs-lookup"><span data-stu-id="f97be-113">Each partition is an independent segment of data and is consumed independently.</span></span> <span data-ttu-id="f97be-114">Over time this data ages off, based on the configurable retention period.</span><span class="sxs-lookup"><span data-stu-id="f97be-114">Over time this data ages off, based on the configurable retention period.</span></span> <span data-ttu-id="f97be-115">As a result, a given event hub never gets "too full."</span><span class="sxs-lookup"><span data-stu-id="f97be-115">As a result, a given event hub never gets "too full."</span></span>

<span data-ttu-id="f97be-116">Event Hubs Capture enables you to specify your own Azure Blob storage account and container, or Azure Data Lake Store account, which are used to store the captured data.</span><span class="sxs-lookup"><span data-stu-id="f97be-116">Event Hubs Capture enables you to specify your own Azure Blob storage account and container, or Azure Data Lake Store account, which are used to store the captured data.</span></span> <span data-ttu-id="f97be-117">These accounts can be in the same region as your event hub or in another region, adding to the flexibility of the Event Hubs Capture feature.</span><span class="sxs-lookup"><span data-stu-id="f97be-117">These accounts can be in the same region as your event hub or in another region, adding to the flexibility of the Event Hubs Capture feature.</span></span>

<span data-ttu-id="f97be-118">Captured data is written in [Apache Avro][Apache Avro] format: a compact, fast, binary format that provides rich data structures with inline schema.</span><span class="sxs-lookup"><span data-stu-id="f97be-118">Captured data is written in [Apache Avro][Apache Avro] format: a compact, fast, binary format that provides rich data structures with inline schema.</span></span> <span data-ttu-id="f97be-119">This format is widely used in the Hadoop ecosystem, Stream Analytics, and Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="f97be-119">This format is widely used in the Hadoop ecosystem, Stream Analytics, and Azure Data Factory.</span></span> <span data-ttu-id="f97be-120">More information about working with Avro is available later in this article.</span><span class="sxs-lookup"><span data-stu-id="f97be-120">More information about working with Avro is available later in this article.</span></span>

### <a name="capture-windowing"></a><span data-ttu-id="f97be-121">Capture windowing</span><span class="sxs-lookup"><span data-stu-id="f97be-121">Capture windowing</span></span>

<span data-ttu-id="f97be-122">Event Hubs Capture enables you to set up a window to control capturing.</span><span class="sxs-lookup"><span data-stu-id="f97be-122">Event Hubs Capture enables you to set up a window to control capturing.</span></span> <span data-ttu-id="f97be-123">This window is a minimum size and time configuration with a "first wins policy," meaning that the first trigger encountered causes a capture operation.</span><span class="sxs-lookup"><span data-stu-id="f97be-123">This window is a minimum size and time configuration with a "first wins policy," meaning that the first trigger encountered causes a capture operation.</span></span> <span data-ttu-id="f97be-124">If you have a fifteen-minute, 100 MB capture window and send 1 MB per second, the size window triggers before the time window.</span><span class="sxs-lookup"><span data-stu-id="f97be-124">If you have a fifteen-minute, 100 MB capture window and send 1 MB per second, the size window triggers before the time window.</span></span> <span data-ttu-id="f97be-125">Each partition captures independently and writes a completed block blob at the time of capture, named for the time at which the capture interval was encountered.</span><span class="sxs-lookup"><span data-stu-id="f97be-125">Each partition captures independently and writes a completed block blob at the time of capture, named for the time at which the capture interval was encountered.</span></span> <span data-ttu-id="f97be-126">The storage naming convention is as follows:</span><span class="sxs-lookup"><span data-stu-id="f97be-126">The storage naming convention is as follows:</span></span>

```
{Namespace}/{EventHub}/{PartitionId}/{Year}/{Month}/{Day}/{Hour}/{Minute}/{Second}
```

<span data-ttu-id="f97be-127">Note that the date values are padded with zeroes; an example filename might be:</span><span class="sxs-lookup"><span data-stu-id="f97be-127">Note that the date values are padded with zeroes; an example filename might be:</span></span>

```
https://mystorageaccount.blob.core.windows.net/mycontainer/mynamespace/myeventhub/0/2017/12/08/03/03/17.avro
```

### <a name="scaling-to-throughput-units"></a><span data-ttu-id="f97be-128">Scaling to throughput units</span><span class="sxs-lookup"><span data-stu-id="f97be-128">Scaling to throughput units</span></span>

<span data-ttu-id="f97be-129">Event Hubs traffic is controlled by [throughput units](event-hubs-features.md#capacity).</span><span class="sxs-lookup"><span data-stu-id="f97be-129">Event Hubs traffic is controlled by [throughput units](event-hubs-features.md#capacity).</span></span> <span data-ttu-id="f97be-130">A single throughput unit allows 1 MB per second or 1000 events per second of ingress and twice that amount of egress.</span><span class="sxs-lookup"><span data-stu-id="f97be-130">A single throughput unit allows 1 MB per second or 1000 events per second of ingress and twice that amount of egress.</span></span> <span data-ttu-id="f97be-131">Standard Event Hubs can be configured with 1-20 throughput units, and you can purchase more with a quota increase [support request][support request].</span><span class="sxs-lookup"><span data-stu-id="f97be-131">Standard Event Hubs can be configured with 1-20 throughput units, and you can purchase more with a quota increase [support request][support request].</span></span> <span data-ttu-id="f97be-132">Usage beyond your purchased throughput units is throttled.</span><span class="sxs-lookup"><span data-stu-id="f97be-132">Usage beyond your purchased throughput units is throttled.</span></span> <span data-ttu-id="f97be-133">Event Hubs Capture copies data directly from the internal Event Hubs storage, bypassing throughput unit egress quotas and saving your egress for other processing readers, such as Stream Analytics or Spark.</span><span class="sxs-lookup"><span data-stu-id="f97be-133">Event Hubs Capture copies data directly from the internal Event Hubs storage, bypassing throughput unit egress quotas and saving your egress for other processing readers, such as Stream Analytics or Spark.</span></span>

<span data-ttu-id="f97be-134">Once configured, Event Hubs Capture runs automatically when you send your first event, and continues running.</span><span class="sxs-lookup"><span data-stu-id="f97be-134">Once configured, Event Hubs Capture runs automatically when you send your first event, and continues running.</span></span> <span data-ttu-id="f97be-135">To make it easier for your downstream processing to know that the process is working, Event Hubs writes empty files when there is no data.</span><span class="sxs-lookup"><span data-stu-id="f97be-135">To make it easier for your downstream processing to know that the process is working, Event Hubs writes empty files when there is no data.</span></span> <span data-ttu-id="f97be-136">This process provides a predictable cadence and marker that can feed your batch processors.</span><span class="sxs-lookup"><span data-stu-id="f97be-136">This process provides a predictable cadence and marker that can feed your batch processors.</span></span>

## <a name="setting-up-event-hubs-capture"></a><span data-ttu-id="f97be-137">Setting up Event Hubs Capture</span><span class="sxs-lookup"><span data-stu-id="f97be-137">Setting up Event Hubs Capture</span></span>

<span data-ttu-id="f97be-138">You can configure Capture at the event hub creation time using the [Azure portal](https://portal.azure.com), or using Azure Resource Manager templates.</span><span class="sxs-lookup"><span data-stu-id="f97be-138">You can configure Capture at the event hub creation time using the [Azure portal](https://portal.azure.com), or using Azure Resource Manager templates.</span></span> <span data-ttu-id="f97be-139">For more information, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="f97be-139">For more information, see the following articles:</span></span>

- [<span data-ttu-id="f97be-140">Enable Event Hubs Capture using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="f97be-140">Enable Event Hubs Capture using the Azure portal</span></span>](event-hubs-capture-enable-through-portal.md)
- [<span data-ttu-id="f97be-141">Create an Event Hubs namespace with an event hub and enable Capture using an Azure Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="f97be-141">Create an Event Hubs namespace with an event hub and enable Capture using an Azure Resource Manager template</span></span>](event-hubs-resource-manager-namespace-event-hub-enable-capture.md)

## <a name="exploring-the-captured-files-and-working-with-avro"></a><span data-ttu-id="f97be-142">Exploring the captured files and working with Avro</span><span class="sxs-lookup"><span data-stu-id="f97be-142">Exploring the captured files and working with Avro</span></span>

<span data-ttu-id="f97be-143">Event Hubs Capture creates files in Avro format, as specified on the configured time window.</span><span class="sxs-lookup"><span data-stu-id="f97be-143">Event Hubs Capture creates files in Avro format, as specified on the configured time window.</span></span> <span data-ttu-id="f97be-144">You can view these files in any tool such as [Azure Storage Explorer][Azure Storage Explorer].</span><span class="sxs-lookup"><span data-stu-id="f97be-144">You can view these files in any tool such as [Azure Storage Explorer][Azure Storage Explorer].</span></span> <span data-ttu-id="f97be-145">You can download the files locally to work on them.</span><span class="sxs-lookup"><span data-stu-id="f97be-145">You can download the files locally to work on them.</span></span>

<span data-ttu-id="f97be-146">The files produced by Event Hubs Capture have the following Avro schema:</span><span class="sxs-lookup"><span data-stu-id="f97be-146">The files produced by Event Hubs Capture have the following Avro schema:</span></span>

![][3]

<span data-ttu-id="f97be-147">An easy way to explore Avro files is by using the [Avro Tools][Avro Tools] jar from Apache.</span><span class="sxs-lookup"><span data-stu-id="f97be-147">An easy way to explore Avro files is by using the [Avro Tools][Avro Tools] jar from Apache.</span></span> <span data-ttu-id="f97be-148">After downloading this jar, you can see the schema of a specific Avro file by running the following command:</span><span class="sxs-lookup"><span data-stu-id="f97be-148">After downloading this jar, you can see the schema of a specific Avro file by running the following command:</span></span>

```shell
java -jar avro-tools-1.8.2.jar getschema <name of capture file>
```

<span data-ttu-id="f97be-149">This command returns</span><span class="sxs-lookup"><span data-stu-id="f97be-149">This command returns</span></span>

```json
{

    "type":"record",
    "name":"EventData",
    "namespace":"Microsoft.ServiceBus.Messaging",
    "fields":[
                 {"name":"SequenceNumber","type":"long"},
                 {"name":"Offset","type":"string"},
                 {"name":"EnqueuedTimeUtc","type":"string"},
                 {"name":"SystemProperties","type":{"type":"map","values":["long","double","string","bytes"]}},
                 {"name":"Properties","type":{"type":"map","values":["long","double","string","bytes"]}},
                 {"name":"Body","type":["null","bytes"]}
             ]
}
```

<span data-ttu-id="f97be-150">You can also use Avro Tools to convert the file to JSON format and perform other processing.</span><span class="sxs-lookup"><span data-stu-id="f97be-150">You can also use Avro Tools to convert the file to JSON format and perform other processing.</span></span>

<span data-ttu-id="f97be-151">To perform more advanced processing, download and install Avro for your choice of platform.</span><span class="sxs-lookup"><span data-stu-id="f97be-151">To perform more advanced processing, download and install Avro for your choice of platform.</span></span> <span data-ttu-id="f97be-152">At the time of this writing, there are implementations available for C, C++, C\#, Java, NodeJS, Perl, PHP, Python, and Ruby.</span><span class="sxs-lookup"><span data-stu-id="f97be-152">At the time of this writing, there are implementations available for C, C++, C\#, Java, NodeJS, Perl, PHP, Python, and Ruby.</span></span>

<span data-ttu-id="f97be-153">Apache Avro has complete Getting Started guides for [Java][Java] and [Python][Python].</span><span class="sxs-lookup"><span data-stu-id="f97be-153">Apache Avro has complete Getting Started guides for [Java][Java] and [Python][Python].</span></span> <span data-ttu-id="f97be-154">You can also read the [Getting started with Event Hubs Capture](event-hubs-capture-python.md) article.</span><span class="sxs-lookup"><span data-stu-id="f97be-154">You can also read the [Getting started with Event Hubs Capture](event-hubs-capture-python.md) article.</span></span>

## <a name="how-event-hubs-capture-is-charged"></a><span data-ttu-id="f97be-155">How Event Hubs Capture is charged</span><span class="sxs-lookup"><span data-stu-id="f97be-155">How Event Hubs Capture is charged</span></span>

<span data-ttu-id="f97be-156">Event Hubs Capture is metered similarly to throughput units: as an hourly charge.</span><span class="sxs-lookup"><span data-stu-id="f97be-156">Event Hubs Capture is metered similarly to throughput units: as an hourly charge.</span></span> <span data-ttu-id="f97be-157">The charge is directly proportional to the number of throughput units purchased for the namespace.</span><span class="sxs-lookup"><span data-stu-id="f97be-157">The charge is directly proportional to the number of throughput units purchased for the namespace.</span></span> <span data-ttu-id="f97be-158">As throughput units are increased and decreased, Event Hubs Capture meters increase and decrease to provide matching performance.</span><span class="sxs-lookup"><span data-stu-id="f97be-158">As throughput units are increased and decreased, Event Hubs Capture meters increase and decrease to provide matching performance.</span></span> <span data-ttu-id="f97be-159">The meters occur in tandem.</span><span class="sxs-lookup"><span data-stu-id="f97be-159">The meters occur in tandem.</span></span> <span data-ttu-id="f97be-160">For pricing details, see [Event Hubs pricing](https://azure.microsoft.com/pricing/details/event-hubs/).</span><span class="sxs-lookup"><span data-stu-id="f97be-160">For pricing details, see [Event Hubs pricing](https://azure.microsoft.com/pricing/details/event-hubs/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="f97be-161">Next steps</span><span class="sxs-lookup"><span data-stu-id="f97be-161">Next steps</span></span>

<span data-ttu-id="f97be-162">Event Hubs Capture is the easiest way to get data into Azure.</span><span class="sxs-lookup"><span data-stu-id="f97be-162">Event Hubs Capture is the easiest way to get data into Azure.</span></span> <span data-ttu-id="f97be-163">Using Azure Data Lake, Azure Data Factory, and Azure HDInsight, you can perform batch processing and other analytics using familiar tools and platforms of your choosing, at any scale you need.</span><span class="sxs-lookup"><span data-stu-id="f97be-163">Using Azure Data Lake, Azure Data Factory, and Azure HDInsight, you can perform batch processing and other analytics using familiar tools and platforms of your choosing, at any scale you need.</span></span>

<span data-ttu-id="f97be-164">You can learn more about Event Hubs by visiting the following links:</span><span class="sxs-lookup"><span data-stu-id="f97be-164">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="f97be-165">Get started sending and receiving events</span><span class="sxs-lookup"><span data-stu-id="f97be-165">Get started sending and receiving events</span></span>](event-hubs-dotnet-framework-getstarted-send.md)
* <span data-ttu-id="f97be-166">[Event Hubs overview][Event Hubs overview]</span><span class="sxs-lookup"><span data-stu-id="f97be-166">[Event Hubs overview][Event Hubs overview]</span></span>

[Apache Avro]: http://avro.apache.org/
[support request]: https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade
[Azure Storage Explorer]: http://azurestorageexplorer.codeplex.com/
[3]: ./media/event-hubs-capture-overview/event-hubs-capture3.png
[Avro Tools]: http://www-us.apache.org/dist/avro/avro-1.8.2/java/avro-tools-1.8.2.jar
[Java]: http://avro.apache.org/docs/current/gettingstartedjava.html
[Python]: http://avro.apache.org/docs/current/gettingstartedpython.html
[Event Hubs overview]: event-hubs-what-is-event-hubs.md
