---
title: What is Azure Event Hubs? | Microsoft Docs
description: Learn about Azure Event Hubs, a Big Data streaming service that ingests millions of events per second.
services: event-hubs
documentationcenter: na
author: ShubhaVijayasarathy
manager: timlt
ms.service: event-hubs
ms.topic: overview
ms.custom: mvc
ms.date: 08/01/2018
ms.author: shvija
ms.openlocfilehash: 8437b1c10facc28c5fd71b70dd7acf01b7d39e8e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866678"
---
# <a name="what-is-azure-event-hubs"></a><span data-ttu-id="e65b5-104">What is Azure Event Hubs?</span><span class="sxs-lookup"><span data-stu-id="e65b5-104">What is Azure Event Hubs?</span></span>

<span data-ttu-id="e65b5-105">Azure Event Hubs is a Big Data streaming platform and event ingestion service, capable of receiving and processing millions of events per second.</span><span class="sxs-lookup"><span data-stu-id="e65b5-105">Azure Event Hubs is a Big Data streaming platform and event ingestion service, capable of receiving and processing millions of events per second.</span></span> <span data-ttu-id="e65b5-106">Event Hubs can process and store events, data, or telemetry produced by distributed software and devices.</span><span class="sxs-lookup"><span data-stu-id="e65b5-106">Event Hubs can process and store events, data, or telemetry produced by distributed software and devices.</span></span> <span data-ttu-id="e65b5-107">Data sent to an event hub can be transformed and stored using any real-time analytics provider or batching/storage adapters.</span><span class="sxs-lookup"><span data-stu-id="e65b5-107">Data sent to an event hub can be transformed and stored using any real-time analytics provider or batching/storage adapters.</span></span> 

<span data-ttu-id="e65b5-108">Event Hubs is used in some of the following common scenarios:</span><span class="sxs-lookup"><span data-stu-id="e65b5-108">Event Hubs is used in some of the following common scenarios:</span></span>

- <span data-ttu-id="e65b5-109">Anomaly detection (fraud/outliers)</span><span class="sxs-lookup"><span data-stu-id="e65b5-109">Anomaly detection (fraud/outliers)</span></span>
- <span data-ttu-id="e65b5-110">Application logging</span><span class="sxs-lookup"><span data-stu-id="e65b5-110">Application logging</span></span>
- <span data-ttu-id="e65b5-111">Analytics pipelines, such as clickstreams</span><span class="sxs-lookup"><span data-stu-id="e65b5-111">Analytics pipelines, such as clickstreams</span></span>
- <span data-ttu-id="e65b5-112">Live dashboarding</span><span class="sxs-lookup"><span data-stu-id="e65b5-112">Live dashboarding</span></span>
- <span data-ttu-id="e65b5-113">Archiving data</span><span class="sxs-lookup"><span data-stu-id="e65b5-113">Archiving data</span></span>
- <span data-ttu-id="e65b5-114">Transaction processing</span><span class="sxs-lookup"><span data-stu-id="e65b5-114">Transaction processing</span></span>
- <span data-ttu-id="e65b5-115">User telemetry processing</span><span class="sxs-lookup"><span data-stu-id="e65b5-115">User telemetry processing</span></span>
- <span data-ttu-id="e65b5-116">Device telemetry streaming</span><span class="sxs-lookup"><span data-stu-id="e65b5-116">Device telemetry streaming</span></span> 

## <a name="why-use-event-hubs"></a><span data-ttu-id="e65b5-117">Why use Event Hubs?</span><span class="sxs-lookup"><span data-stu-id="e65b5-117">Why use Event Hubs?</span></span>

<span data-ttu-id="e65b5-118">Data is valuable only when there is an easy way to process and get timely insights from data sources.</span><span class="sxs-lookup"><span data-stu-id="e65b5-118">Data is valuable only when there is an easy way to process and get timely insights from data sources.</span></span> <span data-ttu-id="e65b5-119">Event Hubs provides a distributed stream processing platform with low latency and seamless integration, with data and analytics services inside and outside Azure to build a complete Big Data pipeline.</span><span class="sxs-lookup"><span data-stu-id="e65b5-119">Event Hubs provides a distributed stream processing platform with low latency and seamless integration, with data and analytics services inside and outside Azure to build a complete Big Data pipeline.</span></span>

<span data-ttu-id="e65b5-120">Event Hubs represents the "front door" for an event pipeline, often called an *event ingestor* in solution architectures.</span><span class="sxs-lookup"><span data-stu-id="e65b5-120">Event Hubs represents the "front door" for an event pipeline, often called an *event ingestor* in solution architectures.</span></span> <span data-ttu-id="e65b5-121">An event ingestor is a component or service that sits between event publishers and event consumers to decouple the production of an event stream from the consumption of those events.</span><span class="sxs-lookup"><span data-stu-id="e65b5-121">An event ingestor is a component or service that sits between event publishers and event consumers to decouple the production of an event stream from the consumption of those events.</span></span> <span data-ttu-id="e65b5-122">Event Hubs provides a unified streaming platform with time retention buffer, decoupling the event producers from event consumers.</span><span class="sxs-lookup"><span data-stu-id="e65b5-122">Event Hubs provides a unified streaming platform with time retention buffer, decoupling the event producers from event consumers.</span></span> 

<span data-ttu-id="e65b5-123">The following sections describe key features of the Azure Event Hubs service:</span><span class="sxs-lookup"><span data-stu-id="e65b5-123">The following sections describe key features of the Azure Event Hubs service:</span></span> 

## <a name="fully-managed-paas"></a><span data-ttu-id="e65b5-124">Fully managed PaaS</span><span class="sxs-lookup"><span data-stu-id="e65b5-124">Fully managed PaaS</span></span> 

<span data-ttu-id="e65b5-125">Event Hubs is a managed service with little configuration or management overhead, so you focus on your business solutions.</span><span class="sxs-lookup"><span data-stu-id="e65b5-125">Event Hubs is a managed service with little configuration or management overhead, so you focus on your business solutions.</span></span> <span data-ttu-id="e65b5-126">[Event Hubs for Apache Kafka ecosystems](event-hubs-for-kafka-ecosystem-overview.md) gives you the PaaS Kafka experience without having to manage, configure, or run your clusters.</span><span class="sxs-lookup"><span data-stu-id="e65b5-126">[Event Hubs for Apache Kafka ecosystems](event-hubs-for-kafka-ecosystem-overview.md) gives you the PaaS Kafka experience without having to manage, configure, or run your clusters.</span></span>

## <a name="support-for-real-time-and-batch-processing"></a><span data-ttu-id="e65b5-127">Support for real-time and batch processing</span><span class="sxs-lookup"><span data-stu-id="e65b5-127">Support for real-time and batch processing</span></span>

<span data-ttu-id="e65b5-128">Ingest, buffer, store, and process your stream in real time to get actionable insights.</span><span class="sxs-lookup"><span data-stu-id="e65b5-128">Ingest, buffer, store, and process your stream in real time to get actionable insights.</span></span> <span data-ttu-id="e65b5-129">Event Hubs uses a [partitioned consumer model](event-hubs-features.md#partitions), enabling multiple applications to process the stream concurrently and letting you control the velocity of processing.</span><span class="sxs-lookup"><span data-stu-id="e65b5-129">Event Hubs uses a [partitioned consumer model](event-hubs-features.md#partitions), enabling multiple applications to process the stream concurrently and letting you control the velocity of processing.</span></span>

<span data-ttu-id="e65b5-130">[Capture](event-hubs-capture-overview.md) your data in near-real time in an [Azure Blob storage](https://azure.microsoft.com/services/storage/blobs/) or [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/) for long-term retention or micro-batch processing.</span><span class="sxs-lookup"><span data-stu-id="e65b5-130">[Capture](event-hubs-capture-overview.md) your data in near-real time in an [Azure Blob storage](https://azure.microsoft.com/services/storage/blobs/) or [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/) for long-term retention or micro-batch processing.</span></span> <span data-ttu-id="e65b5-131">You can achieve this on the same stream you use for deriving real-time analytics.</span><span class="sxs-lookup"><span data-stu-id="e65b5-131">You can achieve this on the same stream you use for deriving real-time analytics.</span></span> <span data-ttu-id="e65b5-132">Setting up Capture is fast, there are no administrative costs to run it, and it scales automatically with Event Hubs [throughput units](event-hubs-features.md#throughput-units).</span><span class="sxs-lookup"><span data-stu-id="e65b5-132">Setting up Capture is fast, there are no administrative costs to run it, and it scales automatically with Event Hubs [throughput units](event-hubs-features.md#throughput-units).</span></span> <span data-ttu-id="e65b5-133">Event Hubs Capture enables you to focus on data processing rather than on data capture.</span><span class="sxs-lookup"><span data-stu-id="e65b5-133">Event Hubs Capture enables you to focus on data processing rather than on data capture.</span></span>

<span data-ttu-id="e65b5-134">Azure Event Hubs also integrates with [Azure Functions](/azure/azure-functions/) for a serverless architecture.</span><span class="sxs-lookup"><span data-stu-id="e65b5-134">Azure Event Hubs also integrates with [Azure Functions](/azure/azure-functions/) for a serverless architecture.</span></span>

## <a name="scalable"></a><span data-ttu-id="e65b5-135">Scalable</span><span class="sxs-lookup"><span data-stu-id="e65b5-135">Scalable</span></span> 

<span data-ttu-id="e65b5-136">With Event Hubs, you can start with data streams in megabytes, and grow to gigabytes or terabytes.</span><span class="sxs-lookup"><span data-stu-id="e65b5-136">With Event Hubs, you can start with data streams in megabytes, and grow to gigabytes or terabytes.</span></span> <span data-ttu-id="e65b5-137">The [Auto-inflate](event-hubs-auto-inflate.md) feature is one of the many options available to scale the number of throughput units to meet your usage needs.</span><span class="sxs-lookup"><span data-stu-id="e65b5-137">The [Auto-inflate](event-hubs-auto-inflate.md) feature is one of the many options available to scale the number of throughput units to meet your usage needs.</span></span> 

## <a name="rich-ecosystem"></a><span data-ttu-id="e65b5-138">Rich ecosystem</span><span class="sxs-lookup"><span data-stu-id="e65b5-138">Rich ecosystem</span></span>

<span data-ttu-id="e65b5-139">[Event Hubs for Apache Kafka ecosystems](event-hubs-for-kafka-ecosystem-overview.md) enables [Apache Kafka (1.0 and above)](https://kafka.apache.org/) clients and applications to talk to Event Hubs without having to manage any clusters.</span><span class="sxs-lookup"><span data-stu-id="e65b5-139">[Event Hubs for Apache Kafka ecosystems](event-hubs-for-kafka-ecosystem-overview.md) enables [Apache Kafka (1.0 and above)](https://kafka.apache.org/) clients and applications to talk to Event Hubs without having to manage any clusters.</span></span>
 
<span data-ttu-id="e65b5-140">With a broad ecosystem available in various [languages (.NET, Java, Python, Go, Node.js)](https://github.com/Azure/azure-event-hubs), you can easily start processing your streams from Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="e65b5-140">With a broad ecosystem available in various [languages (.NET, Java, Python, Go, Node.js)](https://github.com/Azure/azure-event-hubs), you can easily start processing your streams from Event Hubs.</span></span> <span data-ttu-id="e65b5-141">All supported client languages provide low-level integration.</span><span class="sxs-lookup"><span data-stu-id="e65b5-141">All supported client languages provide low-level integration.</span></span>

## <a name="key-architecture-components"></a><span data-ttu-id="e65b5-142">Key architecture components</span><span class="sxs-lookup"><span data-stu-id="e65b5-142">Key architecture components</span></span>

<span data-ttu-id="e65b5-143">Event Hubs provides message stream handling capability but has characteristics that are different from traditional enterprise messaging.</span><span class="sxs-lookup"><span data-stu-id="e65b5-143">Event Hubs provides message stream handling capability but has characteristics that are different from traditional enterprise messaging.</span></span> <span data-ttu-id="e65b5-144">Event Hubs capabilities are built around high throughput and event processing scenarios.</span><span class="sxs-lookup"><span data-stu-id="e65b5-144">Event Hubs capabilities are built around high throughput and event processing scenarios.</span></span> <span data-ttu-id="e65b5-145">Event Hubs contains the following [key components](event-hubs-features.md):</span><span class="sxs-lookup"><span data-stu-id="e65b5-145">Event Hubs contains the following [key components](event-hubs-features.md):</span></span>

- <span data-ttu-id="e65b5-146">**Event producers**: Any entity that sends data to an event hub.</span><span class="sxs-lookup"><span data-stu-id="e65b5-146">**Event producers**: Any entity that sends data to an event hub.</span></span> <span data-ttu-id="e65b5-147">Event publishers can publish events using HTTPS or AMQP 1.0 or Apache Kafka (1.0 and above)</span><span class="sxs-lookup"><span data-stu-id="e65b5-147">Event publishers can publish events using HTTPS or AMQP 1.0 or Apache Kafka (1.0 and above)</span></span>
- <span data-ttu-id="e65b5-148">**Partitions**: Each consumer only reads a specific subset, or partition, of the message stream.</span><span class="sxs-lookup"><span data-stu-id="e65b5-148">**Partitions**: Each consumer only reads a specific subset, or partition, of the message stream.</span></span>
- <span data-ttu-id="e65b5-149">**Consumer groups**: A view (state, position, or offset) of an entire event hub.</span><span class="sxs-lookup"><span data-stu-id="e65b5-149">**Consumer groups**: A view (state, position, or offset) of an entire event hub.</span></span> <span data-ttu-id="e65b5-150">Consumer groups enable multiple consuming applications to each have a separate view of the event stream, and to read the stream independently at their own pace and with their own offsets.</span><span class="sxs-lookup"><span data-stu-id="e65b5-150">Consumer groups enable multiple consuming applications to each have a separate view of the event stream, and to read the stream independently at their own pace and with their own offsets.</span></span>
- <span data-ttu-id="e65b5-151">**Throughput units**: Pre-purchased units of capacity that control the throughput capacity of Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="e65b5-151">**Throughput units**: Pre-purchased units of capacity that control the throughput capacity of Event Hubs.</span></span>
- <span data-ttu-id="e65b5-152">**Event receivers**: Any entity that reads event data from an event hub.</span><span class="sxs-lookup"><span data-stu-id="e65b5-152">**Event receivers**: Any entity that reads event data from an event hub.</span></span> <span data-ttu-id="e65b5-153">All Event Hubs consumers connect via the AMQP 1.0 session, and events are delivered through the session as they become available.</span><span class="sxs-lookup"><span data-stu-id="e65b5-153">All Event Hubs consumers connect via the AMQP 1.0 session, and events are delivered through the session as they become available.</span></span>

<span data-ttu-id="e65b5-154">The following figure shows the Event Hubs stream processing architecture:</span><span class="sxs-lookup"><span data-stu-id="e65b5-154">The following figure shows the Event Hubs stream processing architecture:</span></span>

![Event Hubs](./media/event-hubs-about/event_hubs_architecture.png)


## <a name="next-steps"></a><span data-ttu-id="e65b5-156">Next steps</span><span class="sxs-lookup"><span data-stu-id="e65b5-156">Next steps</span></span>

<span data-ttu-id="e65b5-157">To get started using Event Hubs, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="e65b5-157">To get started using Event Hubs, see the following articles:</span></span>

* [<span data-ttu-id="e65b5-158">Ingest into Event Hubs</span><span class="sxs-lookup"><span data-stu-id="e65b5-158">Ingest into Event Hubs</span></span>](event-hubs-quickstart-portal.md)
* [<span data-ttu-id="e65b5-159">Event Hubs features overview</span><span class="sxs-lookup"><span data-stu-id="e65b5-159">Event Hubs features overview</span></span>](event-hubs-features.md)
* [<span data-ttu-id="e65b5-160">Frequently asked questions</span><span class="sxs-lookup"><span data-stu-id="e65b5-160">Frequently asked questions</span></span>](event-hubs-faq.md)


