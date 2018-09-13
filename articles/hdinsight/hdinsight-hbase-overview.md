---
title: What is HBase in HDInsight? | Microsoft Docs
description: An introduction to Apache HBase in HDInsight, a NoSQL database build on Hadoop. Learn about use cases and compare HBase to other Hadoop clusters.
keywords: bigtable,nosql,what is hbase
services: hdinsight
documentationcenter: ''
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: d2a76d53-133a-4849-a30c-88d9c794391c
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/22/2017
ms.author: jgao
ms.openlocfilehash: 45fb85f83570ed7d79e70dc6fb8f0fdabb7ea191
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550703"
---
# <a name="what-is-hbase-in-hdinsight-a-nosql-database-that-provides-bigtable-like-capabilities-for-hadoop"></a><span data-ttu-id="ef3fd-106">What is HBase in HDInsight: A NoSQL database that provides BigTable-like capabilities for Hadoop</span><span class="sxs-lookup"><span data-stu-id="ef3fd-106">What is HBase in HDInsight: A NoSQL database that provides BigTable-like capabilities for Hadoop</span></span>
<span data-ttu-id="ef3fd-107">Apache HBase is an open-source, NoSQL database that is built on Hadoop and modeled after Google BigTable.</span><span class="sxs-lookup"><span data-stu-id="ef3fd-107">Apache HBase is an open-source, NoSQL database that is built on Hadoop and modeled after Google BigTable.</span></span> <span data-ttu-id="ef3fd-108">HBase provides random access and strong consistency for large amounts of unstructured and semistructured data in a schemaless database organized by column families.</span><span class="sxs-lookup"><span data-stu-id="ef3fd-108">HBase provides random access and strong consistency for large amounts of unstructured and semistructured data in a schemaless database organized by column families.</span></span>

<span data-ttu-id="ef3fd-109">Data is stored in the rows of a table, and data within a row is grouped by column family.</span><span class="sxs-lookup"><span data-stu-id="ef3fd-109">Data is stored in the rows of a table, and data within a row is grouped by column family.</span></span> <span data-ttu-id="ef3fd-110">HBase is a schemaless database in the sense that neither the columns nor the type of data stored in them need to be defined before using them.</span><span class="sxs-lookup"><span data-stu-id="ef3fd-110">HBase is a schemaless database in the sense that neither the columns nor the type of data stored in them need to be defined before using them.</span></span> <span data-ttu-id="ef3fd-111">The open-source code scales linearly to handle petabytes of data on thousands of nodes.</span><span class="sxs-lookup"><span data-stu-id="ef3fd-111">The open-source code scales linearly to handle petabytes of data on thousands of nodes.</span></span> <span data-ttu-id="ef3fd-112">It can rely on data redundancy, batch processing, and other features that are provided by distributed applications in the Hadoop ecosystem.</span><span class="sxs-lookup"><span data-stu-id="ef3fd-112">It can rely on data redundancy, batch processing, and other features that are provided by distributed applications in the Hadoop ecosystem.</span></span>

## <a name="how-is-hbase-implemented-in-azure-hdinsight"></a><span data-ttu-id="ef3fd-113">How is HBase implemented in Azure HDInsight?</span><span class="sxs-lookup"><span data-stu-id="ef3fd-113">How is HBase implemented in Azure HDInsight?</span></span>
<span data-ttu-id="ef3fd-114">HDInsight HBase is offered as a managed cluster that is integrated into the Azure environment.</span><span class="sxs-lookup"><span data-stu-id="ef3fd-114">HDInsight HBase is offered as a managed cluster that is integrated into the Azure environment.</span></span> <span data-ttu-id="ef3fd-115">The clusters are configured to store data directly in Azure Storage, which provides low latency and increased elasticity in performance and cost choices.</span><span class="sxs-lookup"><span data-stu-id="ef3fd-115">The clusters are configured to store data directly in Azure Storage, which provides low latency and increased elasticity in performance and cost choices.</span></span> <span data-ttu-id="ef3fd-116">This enables customers to build interactive websites that work with large datasets, to build services that store sensor and telemetry data from millions of end points, and to analyze this data with Hadoop jobs.</span><span class="sxs-lookup"><span data-stu-id="ef3fd-116">This enables customers to build interactive websites that work with large datasets, to build services that store sensor and telemetry data from millions of end points, and to analyze this data with Hadoop jobs.</span></span> <span data-ttu-id="ef3fd-117">HBase and Hadoop are good starting points for big data project in Azure; in particular, they can enable real-time applications to work with large datasets.</span><span class="sxs-lookup"><span data-stu-id="ef3fd-117">HBase and Hadoop are good starting points for big data project in Azure; in particular, they can enable real-time applications to work with large datasets.</span></span>

<span data-ttu-id="ef3fd-118">The HDInsight implementation leverages the scale-out architecture of HBase to provide automatic sharding of tables, strong consistency for reads and writes, and automatic failover.</span><span class="sxs-lookup"><span data-stu-id="ef3fd-118">The HDInsight implementation leverages the scale-out architecture of HBase to provide automatic sharding of tables, strong consistency for reads and writes, and automatic failover.</span></span> <span data-ttu-id="ef3fd-119">Performance is enhanced by in-memory caching for reads and high-throughput streaming for writes.</span><span class="sxs-lookup"><span data-stu-id="ef3fd-119">Performance is enhanced by in-memory caching for reads and high-throughput streaming for writes.</span></span> <span data-ttu-id="ef3fd-120">HBase cluster can be created inside virtual network.</span><span class="sxs-lookup"><span data-stu-id="ef3fd-120">HBase cluster can be created inside virtual network.</span></span> <span data-ttu-id="ef3fd-121">For details, see  [Create HDInsight clusters on Azure Virtual Network][hbase-provision-vnet].</span><span class="sxs-lookup"><span data-stu-id="ef3fd-121">For details, see  [Create HDInsight clusters on Azure Virtual Network][hbase-provision-vnet].</span></span>

## <a name="how-is-data-managed-in-hdinsight-hbase"></a><span data-ttu-id="ef3fd-122">How is data managed in HDInsight HBase?</span><span class="sxs-lookup"><span data-stu-id="ef3fd-122">How is data managed in HDInsight HBase?</span></span>
<span data-ttu-id="ef3fd-123">Data can be managed in HBase by using the `create`, `get`, `put`, and `scan` commands from the HBase shell.</span><span class="sxs-lookup"><span data-stu-id="ef3fd-123">Data can be managed in HBase by using the `create`, `get`, `put`, and `scan` commands from the HBase shell.</span></span> <span data-ttu-id="ef3fd-124">Data is written to the database by using `put` and read by using `get`.</span><span class="sxs-lookup"><span data-stu-id="ef3fd-124">Data is written to the database by using `put` and read by using `get`.</span></span> <span data-ttu-id="ef3fd-125">The `scan` command is used to obtain data from multiple rows in a table.</span><span class="sxs-lookup"><span data-stu-id="ef3fd-125">The `scan` command is used to obtain data from multiple rows in a table.</span></span> <span data-ttu-id="ef3fd-126">Data can also be managed using the HBase C# API, which provides a client library on top of the HBase REST API.</span><span class="sxs-lookup"><span data-stu-id="ef3fd-126">Data can also be managed using the HBase C# API, which provides a client library on top of the HBase REST API.</span></span> <span data-ttu-id="ef3fd-127">An HBase database can also be queried by using Hive.</span><span class="sxs-lookup"><span data-stu-id="ef3fd-127">An HBase database can also be queried by using Hive.</span></span> <span data-ttu-id="ef3fd-128">For an introduction to these programming models, see [Get started using HBase with Hadoop in HDInsight][hbase-get-started].</span><span class="sxs-lookup"><span data-stu-id="ef3fd-128">For an introduction to these programming models, see [Get started using HBase with Hadoop in HDInsight][hbase-get-started].</span></span> <span data-ttu-id="ef3fd-129">Co-processors are also available, which allow data processing in the nodes that host the database.</span><span class="sxs-lookup"><span data-stu-id="ef3fd-129">Co-processors are also available, which allow data processing in the nodes that host the database.</span></span>

>
> [!NOTE]
> <span data-ttu-id="ef3fd-130">Thrift is not supported by HBase in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ef3fd-130">Thrift is not supported by HBase in HDInsight.</span></span>
>

## <a name="scenarios-use-cases-for-hbase"></a><span data-ttu-id="ef3fd-131">Scenarios: Use cases for HBase</span><span class="sxs-lookup"><span data-stu-id="ef3fd-131">Scenarios: Use cases for HBase</span></span>
<span data-ttu-id="ef3fd-132">The canonical use case for which BigTable (and by extension, HBase) was created was web search.</span><span class="sxs-lookup"><span data-stu-id="ef3fd-132">The canonical use case for which BigTable (and by extension, HBase) was created was web search.</span></span> <span data-ttu-id="ef3fd-133">Search engines build indexes that map terms to the web pages that contain them.</span><span class="sxs-lookup"><span data-stu-id="ef3fd-133">Search engines build indexes that map terms to the web pages that contain them.</span></span> <span data-ttu-id="ef3fd-134">But there are many other use cases that HBase is suitable for—several of which are itemized in this section.</span><span class="sxs-lookup"><span data-stu-id="ef3fd-134">But there are many other use cases that HBase is suitable for—several of which are itemized in this section.</span></span>

* <span data-ttu-id="ef3fd-135">Key-value store</span><span class="sxs-lookup"><span data-stu-id="ef3fd-135">Key-value store</span></span>
  
    <span data-ttu-id="ef3fd-136">HBase can be used as a key-value store, and it is suitable for managing message systems.</span><span class="sxs-lookup"><span data-stu-id="ef3fd-136">HBase can be used as a key-value store, and it is suitable for managing message systems.</span></span> <span data-ttu-id="ef3fd-137">Facebook uses HBase for their messaging system, and it is ideal for storing and managing Internet communications.</span><span class="sxs-lookup"><span data-stu-id="ef3fd-137">Facebook uses HBase for their messaging system, and it is ideal for storing and managing Internet communications.</span></span> <span data-ttu-id="ef3fd-138">WebTable uses HBase to search for and manage tables that are extracted from webpages.</span><span class="sxs-lookup"><span data-stu-id="ef3fd-138">WebTable uses HBase to search for and manage tables that are extracted from webpages.</span></span>
* <span data-ttu-id="ef3fd-139">Sensor data</span><span class="sxs-lookup"><span data-stu-id="ef3fd-139">Sensor data</span></span>
  
    <span data-ttu-id="ef3fd-140">HBase is useful for capturing data that is collected incrementally from various sources.</span><span class="sxs-lookup"><span data-stu-id="ef3fd-140">HBase is useful for capturing data that is collected incrementally from various sources.</span></span> <span data-ttu-id="ef3fd-141">This includes social analytics, time series, keeping interactive dashboards up-to-date with trends and counters, and managing audit log systems.</span><span class="sxs-lookup"><span data-stu-id="ef3fd-141">This includes social analytics, time series, keeping interactive dashboards up-to-date with trends and counters, and managing audit log systems.</span></span> <span data-ttu-id="ef3fd-142">Examples include Bloomberg trader terminal and the Open Time Series Database (OpenTSDB), which stores and provides access to metrics collected about the health of server systems.</span><span class="sxs-lookup"><span data-stu-id="ef3fd-142">Examples include Bloomberg trader terminal and the Open Time Series Database (OpenTSDB), which stores and provides access to metrics collected about the health of server systems.</span></span>
* <span data-ttu-id="ef3fd-143">Real-time query</span><span class="sxs-lookup"><span data-stu-id="ef3fd-143">Real-time query</span></span>
  
    <span data-ttu-id="ef3fd-144">[Phoenix](http://phoenix.apache.org/) is a SQL query engine for Apache HBase.</span><span class="sxs-lookup"><span data-stu-id="ef3fd-144">[Phoenix](http://phoenix.apache.org/) is a SQL query engine for Apache HBase.</span></span> <span data-ttu-id="ef3fd-145">It is accessed as a JDBC driver, and it enables querying and managing HBase tables by using SQL.</span><span class="sxs-lookup"><span data-stu-id="ef3fd-145">It is accessed as a JDBC driver, and it enables querying and managing HBase tables by using SQL.</span></span>
* <span data-ttu-id="ef3fd-146">HBase as a platform</span><span class="sxs-lookup"><span data-stu-id="ef3fd-146">HBase as a platform</span></span>
  
    <span data-ttu-id="ef3fd-147">Applications can run on top of HBase by using it as a datastore.</span><span class="sxs-lookup"><span data-stu-id="ef3fd-147">Applications can run on top of HBase by using it as a datastore.</span></span> <span data-ttu-id="ef3fd-148">Examples include Phoenix, OpenTSDB, Kiji, and Titan.</span><span class="sxs-lookup"><span data-stu-id="ef3fd-148">Examples include Phoenix, OpenTSDB, Kiji, and Titan.</span></span> <span data-ttu-id="ef3fd-149">Applications can also integrate with HBase.</span><span class="sxs-lookup"><span data-stu-id="ef3fd-149">Applications can also integrate with HBase.</span></span> <span data-ttu-id="ef3fd-150">Examples include Hive, Pig, Solr, Storm, Flume, Impala, Spark, Ganglia, and Drill.</span><span class="sxs-lookup"><span data-stu-id="ef3fd-150">Examples include Hive, Pig, Solr, Storm, Flume, Impala, Spark, Ganglia, and Drill.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ef3fd-151">Next steps</span><span class="sxs-lookup"><span data-stu-id="ef3fd-151">Next steps</span></span>
* <span data-ttu-id="ef3fd-152">[Get started using HBase with Hadoop in HDInsight][hbase-get-started]</span><span class="sxs-lookup"><span data-stu-id="ef3fd-152">[Get started using HBase with Hadoop in HDInsight][hbase-get-started]</span></span>
* <span data-ttu-id="ef3fd-153">[Create HDInsight clusters on Azure Virtual Network][hbase-provision-vnet]</span><span class="sxs-lookup"><span data-stu-id="ef3fd-153">[Create HDInsight clusters on Azure Virtual Network][hbase-provision-vnet]</span></span>
* [<span data-ttu-id="ef3fd-154">Configure HBase replication in HDInsight</span><span class="sxs-lookup"><span data-stu-id="ef3fd-154">Configure HBase replication in HDInsight</span></span>](hdinsight-hbase-replication.md)
* <span data-ttu-id="ef3fd-155">[Analyze Twitter sentiment with HBase in HDInsight][hbase-twitter-sentiment]</span><span class="sxs-lookup"><span data-stu-id="ef3fd-155">[Analyze Twitter sentiment with HBase in HDInsight][hbase-twitter-sentiment]</span></span>
* <span data-ttu-id="ef3fd-156">[Use Maven to build Java applications that use HBase with HDInsight (Hadoop)][hbase-build-java-maven]</span><span class="sxs-lookup"><span data-stu-id="ef3fd-156">[Use Maven to build Java applications that use HBase with HDInsight (Hadoop)][hbase-build-java-maven]</span></span>

## <a name="see-also"></a><span data-ttu-id="ef3fd-157">See also</span><span class="sxs-lookup"><span data-stu-id="ef3fd-157">See also</span></span>
* [<span data-ttu-id="ef3fd-158">Apache HBase</span><span class="sxs-lookup"><span data-stu-id="ef3fd-158">Apache HBase</span></span>](https://hbase.apache.org/)
* [<span data-ttu-id="ef3fd-159">Bigtable: A Distributed Storage System for Structured Data</span><span class="sxs-lookup"><span data-stu-id="ef3fd-159">Bigtable: A Distributed Storage System for Structured Data</span></span>](http://research.google.com/archive/bigtable.html)

[hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md

[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md

[hbase-build-java-maven]: hdinsight-hbase-build-java-maven.md

[hdinsight-use-hive]: hdinsight-use-hive.md

[hdinsight-storage]: ../hdinsight-hadoop-use-blob-storage.md

[hbase-get-started]: http://azure.microsoft.com/documentation/articles/hdinsight-hbase-get-started/

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-management-portal]: https://portal.azure.com/
[azure-create-storageaccount]: ../storage-create-storage-account.md

[apache-hadoop]: http://hadoop.apache.org/
