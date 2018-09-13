---
title: Azure Event Hubs for Apache Kafka | Microsoft Docs
description: Overview and introduction to Kafka enabled Azure Event Hubs
services: event-hubs
documentationcenter: .net
author: basilhariri
manager: timlt
ms.service: event-hubs
ms.topic: article
ms.date: 08/16/2018
ms.author: bahariri
ms.openlocfilehash: 16c101068be48ba1435ef230b29c679fcef17d08
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864366"
---
# <a name="azure-event-hubs-for-apache-kafka-preview"></a><span data-ttu-id="0dd2a-103">Azure Event Hubs for Apache Kafka (preview)</span><span class="sxs-lookup"><span data-stu-id="0dd2a-103">Azure Event Hubs for Apache Kafka (preview)</span></span>

<span data-ttu-id="0dd2a-104">Event Hubs provides a Kafka endpoint that can be used by your existing Kafka based applications as an alternative to running your own Kafka cluster.</span><span class="sxs-lookup"><span data-stu-id="0dd2a-104">Event Hubs provides a Kafka endpoint that can be used by your existing Kafka based applications as an alternative to running your own Kafka cluster.</span></span> <span data-ttu-id="0dd2a-105">Event Hubs supports [Apache Kafka 1.0](https://kafka.apache.org/10/documentation.html) and newer client versions, and works with your existing Kafka applications, including MirrorMaker.</span><span class="sxs-lookup"><span data-stu-id="0dd2a-105">Event Hubs supports [Apache Kafka 1.0](https://kafka.apache.org/10/documentation.html) and newer client versions, and works with your existing Kafka applications, including MirrorMaker.</span></span> 

## <a name="what-does-event-hubs-for-kafka-provide"></a><span data-ttu-id="0dd2a-106">What does Event Hubs for Kafka provide?</span><span class="sxs-lookup"><span data-stu-id="0dd2a-106">What does Event Hubs for Kafka provide?</span></span>

<span data-ttu-id="0dd2a-107">The Event Hubs for Kafka feature provides a protocol head on top of Azure Event Hubs that is binary compatible with Kafka versions 1.0 and later for both reading from and writing to Kafka topics.</span><span class="sxs-lookup"><span data-stu-id="0dd2a-107">The Event Hubs for Kafka feature provides a protocol head on top of Azure Event Hubs that is binary compatible with Kafka versions 1.0 and later for both reading from and writing to Kafka topics.</span></span> <span data-ttu-id="0dd2a-108">You may start using the Kafka endpoint from your applications with no code change but a minimal configuration change.</span><span class="sxs-lookup"><span data-stu-id="0dd2a-108">You may start using the Kafka endpoint from your applications with no code change but a minimal configuration change.</span></span> <span data-ttu-id="0dd2a-109">You update the connection string in configurations to point to the Kafka endpoint exposed by your event hub instead of pointing to your Kafka cluster.</span><span class="sxs-lookup"><span data-stu-id="0dd2a-109">You update the connection string in configurations to point to the Kafka endpoint exposed by your event hub instead of pointing to your Kafka cluster.</span></span> <span data-ttu-id="0dd2a-110">Then, you can start streaming events from your applications that use the Kafka protocol into Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="0dd2a-110">Then, you can start streaming events from your applications that use the Kafka protocol into Event Hubs.</span></span> 

<span data-ttu-id="0dd2a-111">Conceptually Kafka and Event Hubs are nearly identical: they are both partitioned logs built for streaming data.</span><span class="sxs-lookup"><span data-stu-id="0dd2a-111">Conceptually Kafka and Event Hubs are nearly identical: they are both partitioned logs built for streaming data.</span></span> <span data-ttu-id="0dd2a-112">The following table maps concepts between Kafka and Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="0dd2a-112">The following table maps concepts between Kafka and Event Hubs.</span></span>

### <a name="kafka-and-event-hub-conceptual-mapping"></a><span data-ttu-id="0dd2a-113">Kafka and Event Hub conceptual mapping</span><span class="sxs-lookup"><span data-stu-id="0dd2a-113">Kafka and Event Hub conceptual mapping</span></span>

| <span data-ttu-id="0dd2a-114">Kafka Concept</span><span class="sxs-lookup"><span data-stu-id="0dd2a-114">Kafka Concept</span></span> | <span data-ttu-id="0dd2a-115">Event Hubs Concept</span><span class="sxs-lookup"><span data-stu-id="0dd2a-115">Event Hubs Concept</span></span>|
| --- | --- |
| <span data-ttu-id="0dd2a-116">Cluster</span><span class="sxs-lookup"><span data-stu-id="0dd2a-116">Cluster</span></span> | <span data-ttu-id="0dd2a-117">Namespace</span><span class="sxs-lookup"><span data-stu-id="0dd2a-117">Namespace</span></span> |
| <span data-ttu-id="0dd2a-118">Topic</span><span class="sxs-lookup"><span data-stu-id="0dd2a-118">Topic</span></span> | <span data-ttu-id="0dd2a-119">Event Hubs</span><span class="sxs-lookup"><span data-stu-id="0dd2a-119">Event Hubs</span></span> |
| <span data-ttu-id="0dd2a-120">Partition</span><span class="sxs-lookup"><span data-stu-id="0dd2a-120">Partition</span></span> | <span data-ttu-id="0dd2a-121">Partition</span><span class="sxs-lookup"><span data-stu-id="0dd2a-121">Partition</span></span>|
| <span data-ttu-id="0dd2a-122">Consumer Group</span><span class="sxs-lookup"><span data-stu-id="0dd2a-122">Consumer Group</span></span> | <span data-ttu-id="0dd2a-123">Consumer Group</span><span class="sxs-lookup"><span data-stu-id="0dd2a-123">Consumer Group</span></span> |
| <span data-ttu-id="0dd2a-124">Offset</span><span class="sxs-lookup"><span data-stu-id="0dd2a-124">Offset</span></span> | <span data-ttu-id="0dd2a-125">Offset</span><span class="sxs-lookup"><span data-stu-id="0dd2a-125">Offset</span></span>|

### <a name="key-differences-between-kafka-and-event-hubs"></a><span data-ttu-id="0dd2a-126">Key differences between Kafka and Event Hubs</span><span class="sxs-lookup"><span data-stu-id="0dd2a-126">Key differences between Kafka and Event Hubs</span></span>

<span data-ttu-id="0dd2a-127">While [Apache Kafka](https://kafka.apache.org/) is software, which you can run wherever you choose, Event Hubs is a cloud service similar to Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="0dd2a-127">While [Apache Kafka](https://kafka.apache.org/) is software, which you can run wherever you choose, Event Hubs is a cloud service similar to Azure Blob Storage.</span></span> <span data-ttu-id="0dd2a-128">There are no servers or networks to manage and no brokers to configure.</span><span class="sxs-lookup"><span data-stu-id="0dd2a-128">There are no servers or networks to manage and no brokers to configure.</span></span> <span data-ttu-id="0dd2a-129">You create a namespace, which is an FQDN in which your topics live, and then create Event Hubs or topics within that namespace.</span><span class="sxs-lookup"><span data-stu-id="0dd2a-129">You create a namespace, which is an FQDN in which your topics live, and then create Event Hubs or topics within that namespace.</span></span> <span data-ttu-id="0dd2a-130">For more information about Event Hubs and namespaces, see [Event Hubs features](event-hubs-features.md#namespace).</span><span class="sxs-lookup"><span data-stu-id="0dd2a-130">For more information about Event Hubs and namespaces, see [Event Hubs features](event-hubs-features.md#namespace).</span></span> <span data-ttu-id="0dd2a-131">As a cloud service, Event Hubs uses a single stable virtual IP address as the endpoint, so clients do not need to know about the brokers or machines within a cluster.</span><span class="sxs-lookup"><span data-stu-id="0dd2a-131">As a cloud service, Event Hubs uses a single stable virtual IP address as the endpoint, so clients do not need to know about the brokers or machines within a cluster.</span></span> 

<span data-ttu-id="0dd2a-132">Scale in Event Hubs is controlled by how many throughput units you purchase, with each throughput unit entitling you to 1 MB per second, or 1000 events per second of ingress.</span><span class="sxs-lookup"><span data-stu-id="0dd2a-132">Scale in Event Hubs is controlled by how many throughput units you purchase, with each throughput unit entitling you to 1 MB per second, or 1000 events per second of ingress.</span></span> <span data-ttu-id="0dd2a-133">By default, Event Hubs scales up throughput units when you reach your limit with the [Auto-Inflate](event-hubs-auto-inflate.md) feature; this feature also works with the Event Hubs for Kafka feature.</span><span class="sxs-lookup"><span data-stu-id="0dd2a-133">By default, Event Hubs scales up throughput units when you reach your limit with the [Auto-Inflate](event-hubs-auto-inflate.md) feature; this feature also works with the Event Hubs for Kafka feature.</span></span> 

### <a name="security-and-authentication"></a><span data-ttu-id="0dd2a-134">Security and authentication</span><span class="sxs-lookup"><span data-stu-id="0dd2a-134">Security and authentication</span></span>

<span data-ttu-id="0dd2a-135">Azure Event Hubs requires SSL or TLS for all communication and uses Shared Access Signatures (SAS) for authentication.</span><span class="sxs-lookup"><span data-stu-id="0dd2a-135">Azure Event Hubs requires SSL or TLS for all communication and uses Shared Access Signatures (SAS) for authentication.</span></span> <span data-ttu-id="0dd2a-136">This requirement is also true for a Kafka endpoint within Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="0dd2a-136">This requirement is also true for a Kafka endpoint within Event Hubs.</span></span> <span data-ttu-id="0dd2a-137">For compatibility with Kafka, Event Hubs uses SASL PLAIN for authentication and SASL SSL for transport security.</span><span class="sxs-lookup"><span data-stu-id="0dd2a-137">For compatibility with Kafka, Event Hubs uses SASL PLAIN for authentication and SASL SSL for transport security.</span></span> <span data-ttu-id="0dd2a-138">For more information about security in Event Hubs, see [Event Hubs authentication and security](event-hubs-authentication-and-security-model-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0dd2a-138">For more information about security in Event Hubs, see [Event Hubs authentication and security](event-hubs-authentication-and-security-model-overview.md).</span></span>

## <a name="other-event-hubs-features-available-for-kafka"></a><span data-ttu-id="0dd2a-139">Other Event Hubs features available for Kafka</span><span class="sxs-lookup"><span data-stu-id="0dd2a-139">Other Event Hubs features available for Kafka</span></span>

<span data-ttu-id="0dd2a-140">The Event Hubs for Kafka feature enables you to write with one protocol and read with another, so that your current Kafka producers can continue publishing via Kafka, and you can add readers with Event Hubs, such as Azure Stream Analytics or Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="0dd2a-140">The Event Hubs for Kafka feature enables you to write with one protocol and read with another, so that your current Kafka producers can continue publishing via Kafka, and you can add readers with Event Hubs, such as Azure Stream Analytics or Azure Functions.</span></span> <span data-ttu-id="0dd2a-141">Additionally, Event Hubs features such as [Capture](event-hubs-capture-overview.md) and [Geo Disaster-Recovery](event-hubs-geo-dr.md) also work with the Event Hubs for Kafka feature.</span><span class="sxs-lookup"><span data-stu-id="0dd2a-141">Additionally, Event Hubs features such as [Capture](event-hubs-capture-overview.md) and [Geo Disaster-Recovery](event-hubs-geo-dr.md) also work with the Event Hubs for Kafka feature.</span></span>

## <a name="features-that-are-not-supported-in-the-preview"></a><span data-ttu-id="0dd2a-142">Features that are not supported in the preview</span><span class="sxs-lookup"><span data-stu-id="0dd2a-142">Features that are not supported in the preview</span></span>

<span data-ttu-id="0dd2a-143">For the public preview of the Event Hubs for Kafka integration, the following Kafka features are not supported:</span><span class="sxs-lookup"><span data-stu-id="0dd2a-143">For the public preview of the Event Hubs for Kafka integration, the following Kafka features are not supported:</span></span>

*   <span data-ttu-id="0dd2a-144">Idempotent producer</span><span class="sxs-lookup"><span data-stu-id="0dd2a-144">Idempotent producer</span></span>
*   <span data-ttu-id="0dd2a-145">Transaction</span><span class="sxs-lookup"><span data-stu-id="0dd2a-145">Transaction</span></span>
*   <span data-ttu-id="0dd2a-146">Compression</span><span class="sxs-lookup"><span data-stu-id="0dd2a-146">Compression</span></span>
*   <span data-ttu-id="0dd2a-147">Size-based retention</span><span class="sxs-lookup"><span data-stu-id="0dd2a-147">Size-based retention</span></span>
*   <span data-ttu-id="0dd2a-148">Log compaction</span><span class="sxs-lookup"><span data-stu-id="0dd2a-148">Log compaction</span></span>
*   <span data-ttu-id="0dd2a-149">Adding partitions to an existing topic</span><span class="sxs-lookup"><span data-stu-id="0dd2a-149">Adding partitions to an existing topic</span></span>
*   <span data-ttu-id="0dd2a-150">HTTP Kafka API support</span><span class="sxs-lookup"><span data-stu-id="0dd2a-150">HTTP Kafka API support</span></span>
*   <span data-ttu-id="0dd2a-151">Kafka Connect</span><span class="sxs-lookup"><span data-stu-id="0dd2a-151">Kafka Connect</span></span>
*   <span data-ttu-id="0dd2a-152">Kafka Streams</span><span class="sxs-lookup"><span data-stu-id="0dd2a-152">Kafka Streams</span></span>

## <a name="next-steps"></a><span data-ttu-id="0dd2a-153">Next steps</span><span class="sxs-lookup"><span data-stu-id="0dd2a-153">Next steps</span></span>

<span data-ttu-id="0dd2a-154">This article provided an introduction to Event Hubs for Kafka.</span><span class="sxs-lookup"><span data-stu-id="0dd2a-154">This article provided an introduction to Event Hubs for Kafka.</span></span> <span data-ttu-id="0dd2a-155">To learn more, see the following links:</span><span class="sxs-lookup"><span data-stu-id="0dd2a-155">To learn more, see the following links:</span></span>

* [<span data-ttu-id="0dd2a-156">How to create Kafka enabled Event Hubs</span><span class="sxs-lookup"><span data-stu-id="0dd2a-156">How to create Kafka enabled Event Hubs</span></span>](event-hubs-create-kafka-enabled.md)
* [<span data-ttu-id="0dd2a-157">Stream into Event Hubs from your Kafka applications</span><span class="sxs-lookup"><span data-stu-id="0dd2a-157">Stream into Event Hubs from your Kafka applications</span></span>](event-hubs-quickstart-kafka-enabled-event-hubs.md)
* <span data-ttu-id="0dd2a-158">Get started with an [Event Hubs tutorial](event-hubs-dotnet-standard-getstarted-send.md)</span><span class="sxs-lookup"><span data-stu-id="0dd2a-158">Get started with an [Event Hubs tutorial](event-hubs-dotnet-standard-getstarted-send.md)</span></span>
* [<span data-ttu-id="0dd2a-159">Event Hubs FAQ</span><span class="sxs-lookup"><span data-stu-id="0dd2a-159">Event Hubs FAQ</span></span>](event-hubs-faq.md)

 
 

