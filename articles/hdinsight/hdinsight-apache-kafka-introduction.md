---
title: An introduction to Apache Kafka on HDInsight | Microsoft Docs
description: Learn about Apache Kafka on HDInsight. What it is, what it does, and where to find examples and getting started information.
services: hdinsight
documentationcenter: ''
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: f284b6e3-5f3b-4a50-b455-917e77588069
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 02/09/2017
ms.author: larryfr
ms.openlocfilehash: a3ceca6cd0f470a5cd6849c345867f094b870a85
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662131"
---
# <a name="introducing-apache-kafka-on-hdinsight-preview"></a><span data-ttu-id="4b446-104">Introducing Apache Kafka on HDInsight (preview)</span><span class="sxs-lookup"><span data-stu-id="4b446-104">Introducing Apache Kafka on HDInsight (preview)</span></span>

<span data-ttu-id="4b446-105">[Apache Kafka](https://kafka.apache.org) is an open-source distributed streaming platform that can be used to build real-time streaming data pipelines and applications.</span><span class="sxs-lookup"><span data-stu-id="4b446-105">[Apache Kafka](https://kafka.apache.org) is an open-source distributed streaming platform that can be used to build real-time streaming data pipelines and applications.</span></span> <span data-ttu-id="4b446-106">Kafka also provides message broker functionality similar to a message queue, where you can publish and subscribe to named data streams.</span><span class="sxs-lookup"><span data-stu-id="4b446-106">Kafka also provides message broker functionality similar to a message queue, where you can publish and subscribe to named data streams.</span></span> <span data-ttu-id="4b446-107">Kafka on HDInsight provides you with a managed, highly scalable, and highly available service in the Microsoft Azure cloud.</span><span class="sxs-lookup"><span data-stu-id="4b446-107">Kafka on HDInsight provides you with a managed, highly scalable, and highly available service in the Microsoft Azure cloud.</span></span>

## <a name="why-use-kafka-on-hdinsight"></a><span data-ttu-id="4b446-108">Why use Kafka on HDInsight?</span><span class="sxs-lookup"><span data-stu-id="4b446-108">Why use Kafka on HDInsight?</span></span>

<span data-ttu-id="4b446-109">Kafka provides the following features:</span><span class="sxs-lookup"><span data-stu-id="4b446-109">Kafka provides the following features:</span></span>

* <span data-ttu-id="4b446-110">Publish-subscribe messaging pattern: Kafka provides a Producer API for publishing records to a Kafka topic.</span><span class="sxs-lookup"><span data-stu-id="4b446-110">Publish-subscribe messaging pattern: Kafka provides a Producer API for publishing records to a Kafka topic.</span></span> <span data-ttu-id="4b446-111">The Consumer API is used when subscribing to a topic.</span><span class="sxs-lookup"><span data-stu-id="4b446-111">The Consumer API is used when subscribing to a topic.</span></span>

* <span data-ttu-id="4b446-112">Stream processing: Kafka is often used with Apache Storm or Spark for real-time stream processing.</span><span class="sxs-lookup"><span data-stu-id="4b446-112">Stream processing: Kafka is often used with Apache Storm or Spark for real-time stream processing.</span></span> <span data-ttu-id="4b446-113">Kafka 0.10.0.0 (HDInsight version 3.5) introduced a streaming API that allows you to build streaming solutions without requiring Storm or Spark.</span><span class="sxs-lookup"><span data-stu-id="4b446-113">Kafka 0.10.0.0 (HDInsight version 3.5) introduced a streaming API that allows you to build streaming solutions without requiring Storm or Spark.</span></span>

* <span data-ttu-id="4b446-114">Horizontal scale: Kafka partitions streams across the nodes in the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="4b446-114">Horizontal scale: Kafka partitions streams across the nodes in the HDInsight cluster.</span></span> <span data-ttu-id="4b446-115">Consumer processes can be associated with individual partitions to provide load balancing when consuming records.</span><span class="sxs-lookup"><span data-stu-id="4b446-115">Consumer processes can be associated with individual partitions to provide load balancing when consuming records.</span></span>

* <span data-ttu-id="4b446-116">In-order delivery: Within each partition, records are stored in the stream in the order that they were received.</span><span class="sxs-lookup"><span data-stu-id="4b446-116">In-order delivery: Within each partition, records are stored in the stream in the order that they were received.</span></span> <span data-ttu-id="4b446-117">By associating one consumer process per partition, you can guarantee that records are processed in-order.</span><span class="sxs-lookup"><span data-stu-id="4b446-117">By associating one consumer process per partition, you can guarantee that records are processed in-order.</span></span>

* <span data-ttu-id="4b446-118">Fault-tolerant: Partitions can be replicated between nodes to provide fault tolerance.</span><span class="sxs-lookup"><span data-stu-id="4b446-118">Fault-tolerant: Partitions can be replicated between nodes to provide fault tolerance.</span></span>

## <a name="use-cases"></a><span data-ttu-id="4b446-119">Use cases</span><span class="sxs-lookup"><span data-stu-id="4b446-119">Use cases</span></span>

* <span data-ttu-id="4b446-120">**Messaging**: Since it supports the publish-subscribe message pattern, Kafka is often used as a message broker.</span><span class="sxs-lookup"><span data-stu-id="4b446-120">**Messaging**: Since it supports the publish-subscribe message pattern, Kafka is often used as a message broker.</span></span>

* <span data-ttu-id="4b446-121">**Activity tracking**: Since Kafka provides in-order logging of records, it can be used to track and re-create activities.</span><span class="sxs-lookup"><span data-stu-id="4b446-121">**Activity tracking**: Since Kafka provides in-order logging of records, it can be used to track and re-create activities.</span></span> <span data-ttu-id="4b446-122">For example, user actions on a web site or within an application.</span><span class="sxs-lookup"><span data-stu-id="4b446-122">For example, user actions on a web site or within an application.</span></span>

* <span data-ttu-id="4b446-123">**Aggregation**: Using stream processing, you can aggregate information from different streams to combine and centralize the information into operational data.</span><span class="sxs-lookup"><span data-stu-id="4b446-123">**Aggregation**: Using stream processing, you can aggregate information from different streams to combine and centralize the information into operational data.</span></span>

* <span data-ttu-id="4b446-124">**Transformation**: Using stream processing, you can combine and enrich data from multiple input topics into one or more output topics.</span><span class="sxs-lookup"><span data-stu-id="4b446-124">**Transformation**: Using stream processing, you can combine and enrich data from multiple input topics into one or more output topics.</span></span>

## <a name="where-do-i-start"></a><span data-ttu-id="4b446-125">Where do I start?</span><span class="sxs-lookup"><span data-stu-id="4b446-125">Where do I start?</span></span>

<span data-ttu-id="4b446-126">See [Get started with Kafka on HDInsight](hdinsight-apache-kafka-get-started.md) for steps on creating a Kafka cluster and using Kafka, including Java-based examples of using the producer, consumer, and streaming API</span><span class="sxs-lookup"><span data-stu-id="4b446-126">See [Get started with Kafka on HDInsight](hdinsight-apache-kafka-get-started.md) for steps on creating a Kafka cluster and using Kafka, including Java-based examples of using the producer, consumer, and streaming API</span></span>

## <a name="next-steps"></a><span data-ttu-id="4b446-127">Next steps</span><span class="sxs-lookup"><span data-stu-id="4b446-127">Next steps</span></span>

<span data-ttu-id="4b446-128">Use the following links to learn how to use Apache Kafka on HDInsight:</span><span class="sxs-lookup"><span data-stu-id="4b446-128">Use the following links to learn how to use Apache Kafka on HDInsight:</span></span>

* [<span data-ttu-id="4b446-129">Get started with Kafka on HDInsight</span><span class="sxs-lookup"><span data-stu-id="4b446-129">Get started with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-get-started.md)

* [<span data-ttu-id="4b446-130">Use MirrorMaker to create a replica of Kafka on HDInsight</span><span class="sxs-lookup"><span data-stu-id="4b446-130">Use MirrorMaker to create a replica of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)

* [<span data-ttu-id="4b446-131">Use Apache Storm with Kafka on HDInsight</span><span class="sxs-lookup"><span data-stu-id="4b446-131">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)

* [<span data-ttu-id="4b446-132">Use Apache Spark with Kafka on HDInsight</span><span class="sxs-lookup"><span data-stu-id="4b446-132">Use Apache Spark with Kafka on HDInsight</span></span>](hdinsight-apache-spark-with-kafka.md)

* [<span data-ttu-id="4b446-133">Connect to Kafka through an Azure Virtual Network</span><span class="sxs-lookup"><span data-stu-id="4b446-133">Connect to Kafka through an Azure Virtual Network</span></span>](hdinsight-apache-kafka-connect-vpn-gateway.md)