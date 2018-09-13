---
title: High availability with Apache Kafka - Azure HDInsight
description: Learn how to ensure high availability with Apache Kafka on Azure HDInsight. Learn how to rebalance partition replicas in Kafka so that they are on different fault domains within the Azure region that contains HDInsight.
services: hdinsight
ms.service: hdinsight
author: jasonwhowell
ms.author: jasonh
ms.reviewer: jasonh
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 05/01/2018
ms.openlocfilehash: bd3b02d54e0a65411e45f0422a0d245645d59096
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965444"
---
# <a name="high-availability-of-your-data-with-apache-kafka-on-hdinsight"></a><span data-ttu-id="c2860-104">High availability of your data with Apache Kafka on HDInsight</span><span class="sxs-lookup"><span data-stu-id="c2860-104">High availability of your data with Apache Kafka on HDInsight</span></span>

<span data-ttu-id="c2860-105">Learn how to configure partition replicas for Kafka topics to take advantage of underlying hardware rack configuration.</span><span class="sxs-lookup"><span data-stu-id="c2860-105">Learn how to configure partition replicas for Kafka topics to take advantage of underlying hardware rack configuration.</span></span> <span data-ttu-id="c2860-106">This configuration ensures the availability of data stored in Apache Kafka on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c2860-106">This configuration ensures the availability of data stored in Apache Kafka on HDInsight.</span></span>

## <a name="fault-and-update-domains-with-kafka"></a><span data-ttu-id="c2860-107">Fault and update domains with Kafka</span><span class="sxs-lookup"><span data-stu-id="c2860-107">Fault and update domains with Kafka</span></span>

<span data-ttu-id="c2860-108">A fault domain is a logical grouping of underlying hardware in an Azure data center.</span><span class="sxs-lookup"><span data-stu-id="c2860-108">A fault domain is a logical grouping of underlying hardware in an Azure data center.</span></span> <span data-ttu-id="c2860-109">Each fault domain shares a common power source and network switch.</span><span class="sxs-lookup"><span data-stu-id="c2860-109">Each fault domain shares a common power source and network switch.</span></span> <span data-ttu-id="c2860-110">The virtual machines and managed disks that implement the nodes within an HDInsight cluster are distributed across these fault domains.</span><span class="sxs-lookup"><span data-stu-id="c2860-110">The virtual machines and managed disks that implement the nodes within an HDInsight cluster are distributed across these fault domains.</span></span> <span data-ttu-id="c2860-111">This architecture limits the potential impact of physical hardware failures.</span><span class="sxs-lookup"><span data-stu-id="c2860-111">This architecture limits the potential impact of physical hardware failures.</span></span>

<span data-ttu-id="c2860-112">Each Azure region has a specific number of fault domains.</span><span class="sxs-lookup"><span data-stu-id="c2860-112">Each Azure region has a specific number of fault domains.</span></span> <span data-ttu-id="c2860-113">For a list of domains and the number of fault domains they contain, see the [Availability sets](../../virtual-machines/windows/regions-and-availability.md#availability-sets) documentation.</span><span class="sxs-lookup"><span data-stu-id="c2860-113">For a list of domains and the number of fault domains they contain, see the [Availability sets](../../virtual-machines/windows/regions-and-availability.md#availability-sets) documentation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c2860-114">Kafka is not aware of fault domains.</span><span class="sxs-lookup"><span data-stu-id="c2860-114">Kafka is not aware of fault domains.</span></span> <span data-ttu-id="c2860-115">When you create a topic in Kafka, it may store all partition replicas in the same fault domain.</span><span class="sxs-lookup"><span data-stu-id="c2860-115">When you create a topic in Kafka, it may store all partition replicas in the same fault domain.</span></span> <span data-ttu-id="c2860-116">To solve this problem, HDInsight provides the [Kafka partition rebalance tool](https://github.com/hdinsight/hdinsight-kafka-tools).</span><span class="sxs-lookup"><span data-stu-id="c2860-116">To solve this problem, HDInsight provides the [Kafka partition rebalance tool](https://github.com/hdinsight/hdinsight-kafka-tools).</span></span>

## <a name="when-to-rebalance-partition-replicas"></a><span data-ttu-id="c2860-117">When to rebalance partition replicas</span><span class="sxs-lookup"><span data-stu-id="c2860-117">When to rebalance partition replicas</span></span>

<span data-ttu-id="c2860-118">To ensure the highest availability of your Kafka data, you should rebalance the partition replicas for your topic at the following times:</span><span class="sxs-lookup"><span data-stu-id="c2860-118">To ensure the highest availability of your Kafka data, you should rebalance the partition replicas for your topic at the following times:</span></span>

* <span data-ttu-id="c2860-119">When a new topic or partition is created</span><span class="sxs-lookup"><span data-stu-id="c2860-119">When a new topic or partition is created</span></span>

* <span data-ttu-id="c2860-120">When you scale up a cluster</span><span class="sxs-lookup"><span data-stu-id="c2860-120">When you scale up a cluster</span></span>

## <a name="replication-factor"></a><span data-ttu-id="c2860-121">Replication factor</span><span class="sxs-lookup"><span data-stu-id="c2860-121">Replication factor</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c2860-122">We recommend using an Azure region that contains three fault domains, and using a replication factor of 3.</span><span class="sxs-lookup"><span data-stu-id="c2860-122">We recommend using an Azure region that contains three fault domains, and using a replication factor of 3.</span></span>

<span data-ttu-id="c2860-123">If you must use a region that contains only two fault domains, use a replication factor of 4 to spread the replicas evenly across the two fault domains.</span><span class="sxs-lookup"><span data-stu-id="c2860-123">If you must use a region that contains only two fault domains, use a replication factor of 4 to spread the replicas evenly across the two fault domains.</span></span>

<span data-ttu-id="c2860-124">For an example of creating topics and setting the replication factor, see the [Start with Kafka on HDInsight](apache-kafka-get-started.md) document.</span><span class="sxs-lookup"><span data-stu-id="c2860-124">For an example of creating topics and setting the replication factor, see the [Start with Kafka on HDInsight](apache-kafka-get-started.md) document.</span></span>

## <a name="how-to-rebalance-partition-replicas"></a><span data-ttu-id="c2860-125">How to rebalance partition replicas</span><span class="sxs-lookup"><span data-stu-id="c2860-125">How to rebalance partition replicas</span></span>

<span data-ttu-id="c2860-126">Use the [Kafka partition rebalance tool](https://github.com/hdinsight/hdinsight-kafka-tools) to rebalance selected topics.</span><span class="sxs-lookup"><span data-stu-id="c2860-126">Use the [Kafka partition rebalance tool](https://github.com/hdinsight/hdinsight-kafka-tools) to rebalance selected topics.</span></span> <span data-ttu-id="c2860-127">This tool must be ran from an SSH session to the head node of your Kafka cluster.</span><span class="sxs-lookup"><span data-stu-id="c2860-127">This tool must be ran from an SSH session to the head node of your Kafka cluster.</span></span>

<span data-ttu-id="c2860-128">For more information on connecting to HDInsight using SSH, see the [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md) document.</span><span class="sxs-lookup"><span data-stu-id="c2860-128">For more information on connecting to HDInsight using SSH, see the [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c2860-129">Next steps</span><span class="sxs-lookup"><span data-stu-id="c2860-129">Next steps</span></span>

* [<span data-ttu-id="c2860-130">Scalability of Kafka on HDInsight</span><span class="sxs-lookup"><span data-stu-id="c2860-130">Scalability of Kafka on HDInsight</span></span>](apache-kafka-scalability.md)
* [<span data-ttu-id="c2860-131">Mirroring with Kafka on HDInsight</span><span class="sxs-lookup"><span data-stu-id="c2860-131">Mirroring with Kafka on HDInsight</span></span>](apache-kafka-mirroring.md)
