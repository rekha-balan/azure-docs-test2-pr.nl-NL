---
title: An introduction to Apache Kafka on HDInsight - Azure
description: 'Learn about Apache Kafka on HDInsight: What it is, what it does, and where to find examples and getting started information.'
services: hdinsight
ms.service: hdinsight
author: jasonwhowell
ms.author: jasonh
ms.reviewer: jasonh
ms.custom: hdinsightactive
ms.topic: overview
ms.date: 04/11/2018
ms.openlocfilehash: 4aa6fd4e469ec2185df82cdb994862f4f7b5d896
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869446"
---
# <a name="what-is-apache-kafka-on-hdinsight"></a><span data-ttu-id="4f9d9-103">What is Apache Kafka on HDInsight?</span><span class="sxs-lookup"><span data-stu-id="4f9d9-103">What is Apache Kafka on HDInsight?</span></span>

<span data-ttu-id="4f9d9-104">[Apache Kafka](https://kafka.apache.org) is an open-source distributed streaming platform that can be used to build real-time streaming data pipelines and applications.</span><span class="sxs-lookup"><span data-stu-id="4f9d9-104">[Apache Kafka](https://kafka.apache.org) is an open-source distributed streaming platform that can be used to build real-time streaming data pipelines and applications.</span></span> <span data-ttu-id="4f9d9-105">Kafka also provides message broker functionality similar to a message queue, where you can publish and subscribe to named data streams.</span><span class="sxs-lookup"><span data-stu-id="4f9d9-105">Kafka also provides message broker functionality similar to a message queue, where you can publish and subscribe to named data streams.</span></span> 

<span data-ttu-id="4f9d9-106">The following are specific characteristics of Kafka on HDInsight:</span><span class="sxs-lookup"><span data-stu-id="4f9d9-106">The following are specific characteristics of Kafka on HDInsight:</span></span>

* <span data-ttu-id="4f9d9-107">It is a managed service that provides a simplified configuration process.</span><span class="sxs-lookup"><span data-stu-id="4f9d9-107">It is a managed service that provides a simplified configuration process.</span></span> <span data-ttu-id="4f9d9-108">The result is a configuration that is tested and supported by Microsoft.</span><span class="sxs-lookup"><span data-stu-id="4f9d9-108">The result is a configuration that is tested and supported by Microsoft.</span></span>

* <span data-ttu-id="4f9d9-109">Microsoft provides a 99.9% Service Level Agreement (SLA) on Kafka uptime.</span><span class="sxs-lookup"><span data-stu-id="4f9d9-109">Microsoft provides a 99.9% Service Level Agreement (SLA) on Kafka uptime.</span></span> <span data-ttu-id="4f9d9-110">For more information, see the [SLA information for HDInsight](https://azure.microsoft.com/support/legal/sla/hdinsight/v1_0/) document.</span><span class="sxs-lookup"><span data-stu-id="4f9d9-110">For more information, see the [SLA information for HDInsight](https://azure.microsoft.com/support/legal/sla/hdinsight/v1_0/) document.</span></span>

* <span data-ttu-id="4f9d9-111">It uses Azure Managed Disks as the backing store for Kafka.</span><span class="sxs-lookup"><span data-stu-id="4f9d9-111">It uses Azure Managed Disks as the backing store for Kafka.</span></span> <span data-ttu-id="4f9d9-112">Managed Disks can provide up to 16 TB of storage per Kafka broker.</span><span class="sxs-lookup"><span data-stu-id="4f9d9-112">Managed Disks can provide up to 16 TB of storage per Kafka broker.</span></span> <span data-ttu-id="4f9d9-113">For information on configuring managed disks with Kafka on HDInsight, see [Increase scalability of Kafka on HDInsight](apache-kafka-scalability.md).</span><span class="sxs-lookup"><span data-stu-id="4f9d9-113">For information on configuring managed disks with Kafka on HDInsight, see [Increase scalability of Kafka on HDInsight](apache-kafka-scalability.md).</span></span>

    <span data-ttu-id="4f9d9-114">For more information on managed disks, see [Azure Managed Disks](../../virtual-machines/windows/managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4f9d9-114">For more information on managed disks, see [Azure Managed Disks](../../virtual-machines/windows/managed-disks-overview.md).</span></span>

* <span data-ttu-id="4f9d9-115">Kafka was designed with a single dimensional view of a rack.</span><span class="sxs-lookup"><span data-stu-id="4f9d9-115">Kafka was designed with a single dimensional view of a rack.</span></span> <span data-ttu-id="4f9d9-116">Azure separates a rack into two dimensions - Update Domains (UD) and Fault Domains (FD).</span><span class="sxs-lookup"><span data-stu-id="4f9d9-116">Azure separates a rack into two dimensions - Update Domains (UD) and Fault Domains (FD).</span></span> <span data-ttu-id="4f9d9-117">Microsoft provides tools that rebalance Kafka partitions and replicas across UDs and FDs.</span><span class="sxs-lookup"><span data-stu-id="4f9d9-117">Microsoft provides tools that rebalance Kafka partitions and replicas across UDs and FDs.</span></span> 

    <span data-ttu-id="4f9d9-118">For more information, see [High availability with Kafka on HDInsight](apache-kafka-high-availability.md).</span><span class="sxs-lookup"><span data-stu-id="4f9d9-118">For more information, see [High availability with Kafka on HDInsight](apache-kafka-high-availability.md).</span></span>

* <span data-ttu-id="4f9d9-119">HDInsight allows you to change the number of worker nodes (which host the Kafka-broker) after cluster creation.</span><span class="sxs-lookup"><span data-stu-id="4f9d9-119">HDInsight allows you to change the number of worker nodes (which host the Kafka-broker) after cluster creation.</span></span> <span data-ttu-id="4f9d9-120">Scaling can be performed from the Azure portal, Azure PowerShell, and other Azure management interfaces.</span><span class="sxs-lookup"><span data-stu-id="4f9d9-120">Scaling can be performed from the Azure portal, Azure PowerShell, and other Azure management interfaces.</span></span> <span data-ttu-id="4f9d9-121">For Kafka, you should rebalance partition replicas after scaling operations.</span><span class="sxs-lookup"><span data-stu-id="4f9d9-121">For Kafka, you should rebalance partition replicas after scaling operations.</span></span> <span data-ttu-id="4f9d9-122">Rebalancing partitions allows Kafka to take advantage of the new number of worker nodes.</span><span class="sxs-lookup"><span data-stu-id="4f9d9-122">Rebalancing partitions allows Kafka to take advantage of the new number of worker nodes.</span></span>

    <span data-ttu-id="4f9d9-123">For more information, see [High availability with Kafka on HDInsight](apache-kafka-high-availability.md).</span><span class="sxs-lookup"><span data-stu-id="4f9d9-123">For more information, see [High availability with Kafka on HDInsight](apache-kafka-high-availability.md).</span></span>

* <span data-ttu-id="4f9d9-124">Azure Log Analytics can be used to monitor Kafka on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4f9d9-124">Azure Log Analytics can be used to monitor Kafka on HDInsight.</span></span> <span data-ttu-id="4f9d9-125">Log Analytics surfaces virtual machine level information, such as disk and NIC metrics, and JMX metrics from Kafka.</span><span class="sxs-lookup"><span data-stu-id="4f9d9-125">Log Analytics surfaces virtual machine level information, such as disk and NIC metrics, and JMX metrics from Kafka.</span></span>

    <span data-ttu-id="4f9d9-126">For more information, see [Analyze logs for Kafka on HDInsight](apache-kafka-log-analytics-operations-management.md).</span><span class="sxs-lookup"><span data-stu-id="4f9d9-126">For more information, see [Analyze logs for Kafka on HDInsight](apache-kafka-log-analytics-operations-management.md).</span></span>

### <a name="kafka-on-hdinsight-architecture"></a><span data-ttu-id="4f9d9-127">Kafka on HDInsight architecture</span><span class="sxs-lookup"><span data-stu-id="4f9d9-127">Kafka on HDInsight architecture</span></span>

<span data-ttu-id="4f9d9-128">The following diagram shows a typical Kafka configuration that uses consumer groups, partitioning, and replication to offer parallel reading of events with fault tolerance:</span><span class="sxs-lookup"><span data-stu-id="4f9d9-128">The following diagram shows a typical Kafka configuration that uses consumer groups, partitioning, and replication to offer parallel reading of events with fault tolerance:</span></span>

![Kafka cluster configuration diagram](./media/apache-kafka-introduction/kafka-cluster.png)

<span data-ttu-id="4f9d9-130">Apache ZooKeeper manages the state of the Kafka cluster.</span><span class="sxs-lookup"><span data-stu-id="4f9d9-130">Apache ZooKeeper manages the state of the Kafka cluster.</span></span> <span data-ttu-id="4f9d9-131">Zookeeper is built for concurrent, resilient, and low-latency transactions.</span><span class="sxs-lookup"><span data-stu-id="4f9d9-131">Zookeeper is built for concurrent, resilient, and low-latency transactions.</span></span> 

<span data-ttu-id="4f9d9-132">Kafka stores records (data) in **topics**.</span><span class="sxs-lookup"><span data-stu-id="4f9d9-132">Kafka stores records (data) in **topics**.</span></span> <span data-ttu-id="4f9d9-133">Records are produced by **producers**, and consumed by **consumers**.</span><span class="sxs-lookup"><span data-stu-id="4f9d9-133">Records are produced by **producers**, and consumed by **consumers**.</span></span> <span data-ttu-id="4f9d9-134">Producers send records to Kafka **brokers**.</span><span class="sxs-lookup"><span data-stu-id="4f9d9-134">Producers send records to Kafka **brokers**.</span></span> <span data-ttu-id="4f9d9-135">Each worker node in your HDInsight cluster is a Kafka broker.</span><span class="sxs-lookup"><span data-stu-id="4f9d9-135">Each worker node in your HDInsight cluster is a Kafka broker.</span></span> 

<span data-ttu-id="4f9d9-136">Topics partition records across brokers.</span><span class="sxs-lookup"><span data-stu-id="4f9d9-136">Topics partition records across brokers.</span></span> <span data-ttu-id="4f9d9-137">When consuming records, you can use up to one consumer per partition to achieve parallel processing of the data.</span><span class="sxs-lookup"><span data-stu-id="4f9d9-137">When consuming records, you can use up to one consumer per partition to achieve parallel processing of the data.</span></span>

<span data-ttu-id="4f9d9-138">Replication is employed to duplicate partitions across nodes, protecting against node (broker) outages.</span><span class="sxs-lookup"><span data-stu-id="4f9d9-138">Replication is employed to duplicate partitions across nodes, protecting against node (broker) outages.</span></span> <span data-ttu-id="4f9d9-139">A partition denoted with an *(L)* in the diagram is the leader for the given partition.</span><span class="sxs-lookup"><span data-stu-id="4f9d9-139">A partition denoted with an *(L)* in the diagram is the leader for the given partition.</span></span> <span data-ttu-id="4f9d9-140">Producer traffic is routed to the leader of each node, using the state managed by ZooKeeper.</span><span class="sxs-lookup"><span data-stu-id="4f9d9-140">Producer traffic is routed to the leader of each node, using the state managed by ZooKeeper.</span></span>

## <a name="why-use-kafka-on-hdinsight"></a><span data-ttu-id="4f9d9-141">Why use Kafka on HDInsight?</span><span class="sxs-lookup"><span data-stu-id="4f9d9-141">Why use Kafka on HDInsight?</span></span>

<span data-ttu-id="4f9d9-142">The following are common tasks and patterns that can be performed using Kafka on HDInsight:</span><span class="sxs-lookup"><span data-stu-id="4f9d9-142">The following are common tasks and patterns that can be performed using Kafka on HDInsight:</span></span>

* <span data-ttu-id="4f9d9-143">**Replication of Kafka data**: Kafka provides the MirrorMaker utility, which replicates data between Kafka clusters.</span><span class="sxs-lookup"><span data-stu-id="4f9d9-143">**Replication of Kafka data**: Kafka provides the MirrorMaker utility, which replicates data between Kafka clusters.</span></span>

    <span data-ttu-id="4f9d9-144">For information on using MirrorMaker, see [Replicate Kafka topics with Kafka on HDInsight](apache-kafka-mirroring.md).</span><span class="sxs-lookup"><span data-stu-id="4f9d9-144">For information on using MirrorMaker, see [Replicate Kafka topics with Kafka on HDInsight](apache-kafka-mirroring.md).</span></span>

* <span data-ttu-id="4f9d9-145">**Publish-subscribe messaging pattern**: Kafka provides a Producer API for publishing records to a Kafka topic.</span><span class="sxs-lookup"><span data-stu-id="4f9d9-145">**Publish-subscribe messaging pattern**: Kafka provides a Producer API for publishing records to a Kafka topic.</span></span> <span data-ttu-id="4f9d9-146">The Consumer API is used when subscribing to a topic.</span><span class="sxs-lookup"><span data-stu-id="4f9d9-146">The Consumer API is used when subscribing to a topic.</span></span>

    <span data-ttu-id="4f9d9-147">For more information, see [Start with Kafka on HDInsight](apache-kafka-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="4f9d9-147">For more information, see [Start with Kafka on HDInsight](apache-kafka-get-started.md).</span></span>

* <span data-ttu-id="4f9d9-148">**Stream processing**: Kafka is often used with Apache Storm or Spark for real-time stream processing.</span><span class="sxs-lookup"><span data-stu-id="4f9d9-148">**Stream processing**: Kafka is often used with Apache Storm or Spark for real-time stream processing.</span></span> <span data-ttu-id="4f9d9-149">Kafka 0.10.0.0 (HDInsight version 3.5 and 3.6) introduced a streaming API that allows you to build streaming solutions without requiring Storm or Spark.</span><span class="sxs-lookup"><span data-stu-id="4f9d9-149">Kafka 0.10.0.0 (HDInsight version 3.5 and 3.6) introduced a streaming API that allows you to build streaming solutions without requiring Storm or Spark.</span></span>

    <span data-ttu-id="4f9d9-150">For more information, see [Start with Kafka on HDInsight](apache-kafka-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="4f9d9-150">For more information, see [Start with Kafka on HDInsight](apache-kafka-get-started.md).</span></span>

* <span data-ttu-id="4f9d9-151">**Horizontal scale**: Kafka partitions streams across the nodes in the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="4f9d9-151">**Horizontal scale**: Kafka partitions streams across the nodes in the HDInsight cluster.</span></span> <span data-ttu-id="4f9d9-152">Consumer processes can be associated with individual partitions to provide load balancing when consuming records.</span><span class="sxs-lookup"><span data-stu-id="4f9d9-152">Consumer processes can be associated with individual partitions to provide load balancing when consuming records.</span></span>

    <span data-ttu-id="4f9d9-153">For more information, see [Start with Kafka on HDInsight](apache-kafka-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="4f9d9-153">For more information, see [Start with Kafka on HDInsight](apache-kafka-get-started.md).</span></span>

* <span data-ttu-id="4f9d9-154">**In-order delivery**: Within each partition, records are stored in the stream in the order that they were received.</span><span class="sxs-lookup"><span data-stu-id="4f9d9-154">**In-order delivery**: Within each partition, records are stored in the stream in the order that they were received.</span></span> <span data-ttu-id="4f9d9-155">By associating one consumer process per partition, you can guarantee that records are processed in-order.</span><span class="sxs-lookup"><span data-stu-id="4f9d9-155">By associating one consumer process per partition, you can guarantee that records are processed in-order.</span></span>

    <span data-ttu-id="4f9d9-156">For more information, see [Start with Kafka on HDInsight](apache-kafka-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="4f9d9-156">For more information, see [Start with Kafka on HDInsight](apache-kafka-get-started.md).</span></span>

## <a name="use-cases"></a><span data-ttu-id="4f9d9-157">Use cases</span><span class="sxs-lookup"><span data-stu-id="4f9d9-157">Use cases</span></span>

* <span data-ttu-id="4f9d9-158">**Messaging**: Since it supports the publish-subscribe message pattern, Kafka is often used as a message broker.</span><span class="sxs-lookup"><span data-stu-id="4f9d9-158">**Messaging**: Since it supports the publish-subscribe message pattern, Kafka is often used as a message broker.</span></span>

* <span data-ttu-id="4f9d9-159">**Activity tracking**: Since Kafka provides in-order logging of records, it can be used to track and re-create activities.</span><span class="sxs-lookup"><span data-stu-id="4f9d9-159">**Activity tracking**: Since Kafka provides in-order logging of records, it can be used to track and re-create activities.</span></span> <span data-ttu-id="4f9d9-160">For example, user actions on a web site or within an application.</span><span class="sxs-lookup"><span data-stu-id="4f9d9-160">For example, user actions on a web site or within an application.</span></span>

* <span data-ttu-id="4f9d9-161">**Aggregation**: Using stream processing, you can aggregate information from different streams to combine and centralize the information into operational data.</span><span class="sxs-lookup"><span data-stu-id="4f9d9-161">**Aggregation**: Using stream processing, you can aggregate information from different streams to combine and centralize the information into operational data.</span></span>

* <span data-ttu-id="4f9d9-162">**Transformation**: Using stream processing, you can combine and enrich data from multiple input topics into one or more output topics.</span><span class="sxs-lookup"><span data-stu-id="4f9d9-162">**Transformation**: Using stream processing, you can combine and enrich data from multiple input topics into one or more output topics.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4f9d9-163">Next steps</span><span class="sxs-lookup"><span data-stu-id="4f9d9-163">Next steps</span></span>

<span data-ttu-id="4f9d9-164">Use the following links to learn how to use Apache Kafka on HDInsight:</span><span class="sxs-lookup"><span data-stu-id="4f9d9-164">Use the following links to learn how to use Apache Kafka on HDInsight:</span></span>

* [<span data-ttu-id="4f9d9-165">Quickstart: Create Kafka on HDInsight</span><span class="sxs-lookup"><span data-stu-id="4f9d9-165">Quickstart: Create Kafka on HDInsight</span></span>](apache-kafka-get-started.md)

* [<span data-ttu-id="4f9d9-166">Tutorial: Use Apache Spark with Kafka on HDInsight</span><span class="sxs-lookup"><span data-stu-id="4f9d9-166">Tutorial: Use Apache Spark with Kafka on HDInsight</span></span>](../hdinsight-apache-spark-with-kafka.md)

* [<span data-ttu-id="4f9d9-167">Tutorial: Use Apache Storm with Kafka on HDInsight</span><span class="sxs-lookup"><span data-stu-id="4f9d9-167">Tutorial: Use Apache Storm with Kafka on HDInsight</span></span>](../hdinsight-apache-storm-with-kafka.md)
