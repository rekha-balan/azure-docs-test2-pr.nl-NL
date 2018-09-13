---
title: Introduction to Apache Storm on HDInsight | Microsoft Docs
description: Get an introduction to Apache Storm on HDInsight.
services: hdinsight
documentationcenter: ''
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 72d54080-1e48-4a5e-aa50-cce4ffc85077
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/31/2017
ms.author: larryfr
ms.openlocfilehash: eb110e64b802bae2540fdbb6229a9f06c87a8279
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552336"
---
# <a name="introduction-to-apache-storm-on-hdinsight-real-time-analytics-for-hadoop"></a><span data-ttu-id="07d21-103">Introduction to Apache Storm on HDInsight: Real-time analytics for Hadoop</span><span class="sxs-lookup"><span data-stu-id="07d21-103">Introduction to Apache Storm on HDInsight: Real-time analytics for Hadoop</span></span>

<span data-ttu-id="07d21-104">You can create distributed, real-time analytics solutions by using Apache Storm on Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="07d21-104">You can create distributed, real-time analytics solutions by using Apache Storm on Azure HDInsight.</span></span>

<span data-ttu-id="07d21-105">Storm is a distributed, fault-tolerant, open-source computation system.</span><span class="sxs-lookup"><span data-stu-id="07d21-105">Storm is a distributed, fault-tolerant, open-source computation system.</span></span> <span data-ttu-id="07d21-106">You can use Storm to process data in real time with Hadoop.</span><span class="sxs-lookup"><span data-stu-id="07d21-106">You can use Storm to process data in real time with Hadoop.</span></span> <span data-ttu-id="07d21-107">Storm solutions can also provide guaranteed processing of data, with the ability to replay data that was not successfully processed the first time.</span><span class="sxs-lookup"><span data-stu-id="07d21-107">Storm solutions can also provide guaranteed processing of data, with the ability to replay data that was not successfully processed the first time.</span></span>

## <a name="how-does-storm-work"></a><span data-ttu-id="07d21-108">How does Storm work?</span><span class="sxs-lookup"><span data-stu-id="07d21-108">How does Storm work?</span></span>

<span data-ttu-id="07d21-109">Storm runs topologies instead of the MapReduce jobs that you might be familiar with in HDInsight or Hadoop.</span><span class="sxs-lookup"><span data-stu-id="07d21-109">Storm runs topologies instead of the MapReduce jobs that you might be familiar with in HDInsight or Hadoop.</span></span> <span data-ttu-id="07d21-110">Topologies are composed of multiple components that are arranged in a directed acyclic graph (DAG).</span><span class="sxs-lookup"><span data-stu-id="07d21-110">Topologies are composed of multiple components that are arranged in a directed acyclic graph (DAG).</span></span> <span data-ttu-id="07d21-111">The following diagram illustrates how data flows between components in a basic word-count topology:</span><span class="sxs-lookup"><span data-stu-id="07d21-111">The following diagram illustrates how data flows between components in a basic word-count topology:</span></span>

![Example of how components are arranged in a Storm topology](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-storm-overview/wordcount-topology.png)

* <span data-ttu-id="07d21-113">Spout components bring data into a topology.</span><span class="sxs-lookup"><span data-stu-id="07d21-113">Spout components bring data into a topology.</span></span> <span data-ttu-id="07d21-114">They emit one or more streams into the topology.</span><span class="sxs-lookup"><span data-stu-id="07d21-114">They emit one or more streams into the topology.</span></span>

* <span data-ttu-id="07d21-115">Bolt components consume streams emitted from spouts or other bolts.</span><span class="sxs-lookup"><span data-stu-id="07d21-115">Bolt components consume streams emitted from spouts or other bolts.</span></span> <span data-ttu-id="07d21-116">Bolts might optionally emit new streams into the topology.</span><span class="sxs-lookup"><span data-stu-id="07d21-116">Bolts might optionally emit new streams into the topology.</span></span> <span data-ttu-id="07d21-117">Bolts are also responsible for writing data to persistent storage, such as HDFS or HBase.</span><span class="sxs-lookup"><span data-stu-id="07d21-117">Bolts are also responsible for writing data to persistent storage, such as HDFS or HBase.</span></span>

## <a name="why-use-storm-on-hdinsight"></a><span data-ttu-id="07d21-118">Why use Storm on HDInsight?</span><span class="sxs-lookup"><span data-stu-id="07d21-118">Why use Storm on HDInsight?</span></span>

<span data-ttu-id="07d21-119">Storm on HDInsight provides the following key benefits:</span><span class="sxs-lookup"><span data-stu-id="07d21-119">Storm on HDInsight provides the following key benefits:</span></span>

* <span data-ttu-id="07d21-120">Performs as a managed service with an SLA of 99.9 percent uptime.</span><span class="sxs-lookup"><span data-stu-id="07d21-120">Performs as a managed service with an SLA of 99.9 percent uptime.</span></span>

* <span data-ttu-id="07d21-121">Supports easy customization by running scripts against a cluster during or after creation.</span><span class="sxs-lookup"><span data-stu-id="07d21-121">Supports easy customization by running scripts against a cluster during or after creation.</span></span> <span data-ttu-id="07d21-122">For more information, see [Customize HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="07d21-122">For more information, see [Customize HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

* <span data-ttu-id="07d21-123">Uses various languages.</span><span class="sxs-lookup"><span data-stu-id="07d21-123">Uses various languages.</span></span> <span data-ttu-id="07d21-124">You can write Storm components in the language of your choice, such as Java, C#, and Python.</span><span class="sxs-lookup"><span data-stu-id="07d21-124">You can write Storm components in the language of your choice, such as Java, C#, and Python.</span></span>

    * <span data-ttu-id="07d21-125">Integrates Visual Studio with HDInsight for the development, management, and monitoring of C# topologies.</span><span class="sxs-lookup"><span data-stu-id="07d21-125">Integrates Visual Studio with HDInsight for the development, management, and monitoring of C# topologies.</span></span> <span data-ttu-id="07d21-126">For more information, see [Develop C# Storm topologies with the HDInsight Tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="07d21-126">For more information, see [Develop C# Storm topologies with the HDInsight Tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

    * <span data-ttu-id="07d21-127">Supports the Trident Java interface.</span><span class="sxs-lookup"><span data-stu-id="07d21-127">Supports the Trident Java interface.</span></span> <span data-ttu-id="07d21-128">You can create Storm topologies that support exactly once processing of messages, transactional datastore persistence, and a set of common stream analytics operations.</span><span class="sxs-lookup"><span data-stu-id="07d21-128">You can create Storm topologies that support exactly once processing of messages, transactional datastore persistence, and a set of common stream analytics operations.</span></span>

*  <span data-ttu-id="07d21-129">Scales clusters up and down easily.</span><span class="sxs-lookup"><span data-stu-id="07d21-129">Scales clusters up and down easily.</span></span> <span data-ttu-id="07d21-130">You can add or remove worker nodes with no impact to running Storm topologies.</span><span class="sxs-lookup"><span data-stu-id="07d21-130">You can add or remove worker nodes with no impact to running Storm topologies.</span></span>

* <span data-ttu-id="07d21-131">Integrates with the following Azure services:</span><span class="sxs-lookup"><span data-stu-id="07d21-131">Integrates with the following Azure services:</span></span>

    * <span data-ttu-id="07d21-132">Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="07d21-132">Azure Event Hubs</span></span>

    * <span data-ttu-id="07d21-133">Azure Virtual Network</span><span class="sxs-lookup"><span data-stu-id="07d21-133">Azure Virtual Network</span></span>

    * <span data-ttu-id="07d21-134">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="07d21-134">Azure SQL Database</span></span>

    * <span data-ttu-id="07d21-135">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="07d21-135">Azure Storage</span></span>

    * <span data-ttu-id="07d21-136">Azure DocumentDB</span><span class="sxs-lookup"><span data-stu-id="07d21-136">Azure DocumentDB</span></span>

* <span data-ttu-id="07d21-137">Securely combines the capabilities of multiple HDInsight clusters by using Virtual Network.</span><span class="sxs-lookup"><span data-stu-id="07d21-137">Securely combines the capabilities of multiple HDInsight clusters by using Virtual Network.</span></span> <span data-ttu-id="07d21-138">You can create analytic pipelines that use HDInsight, HBase, or Hadoop clusters.</span><span class="sxs-lookup"><span data-stu-id="07d21-138">You can create analytic pipelines that use HDInsight, HBase, or Hadoop clusters.</span></span>

<span data-ttu-id="07d21-139">For a list of companies that are using Storm for their real-time analytics solutions, see [Companies using Apache Storm](https://storm.apache.org/documentation/Powered-By.html).</span><span class="sxs-lookup"><span data-stu-id="07d21-139">For a list of companies that are using Storm for their real-time analytics solutions, see [Companies using Apache Storm](https://storm.apache.org/documentation/Powered-By.html).</span></span>

<span data-ttu-id="07d21-140">To get started using Storm, see [Get started with Storm on HDInsight][gettingstarted].</span><span class="sxs-lookup"><span data-stu-id="07d21-140">To get started using Storm, see [Get started with Storm on HDInsight][gettingstarted].</span></span>

## <a name="ease-of-creation"></a><span data-ttu-id="07d21-141">Ease of creation</span><span class="sxs-lookup"><span data-stu-id="07d21-141">Ease of creation</span></span>

<span data-ttu-id="07d21-142">You can provision a new Storm cluster on HDInsight in minutes.</span><span class="sxs-lookup"><span data-stu-id="07d21-142">You can provision a new Storm cluster on HDInsight in minutes.</span></span> <span data-ttu-id="07d21-143">For more information on creating a Storm cluster, see [Get started with Storm on HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="07d21-143">For more information on creating a Storm cluster, see [Get started with Storm on HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md).</span></span>

## <a name="ease-of-use"></a><span data-ttu-id="07d21-144">Ease of use</span><span class="sxs-lookup"><span data-stu-id="07d21-144">Ease of use</span></span>

* <span data-ttu-id="07d21-145">__Secure Shell (SSH) connectivity__: You can access the head nodes of your HDInsight cluster over the Internet by using SSH.</span><span class="sxs-lookup"><span data-stu-id="07d21-145">__Secure Shell (SSH) connectivity__: You can access the head nodes of your HDInsight cluster over the Internet by using SSH.</span></span> <span data-ttu-id="07d21-146">You can run commands directly on your cluster by using SSH.</span><span class="sxs-lookup"><span data-stu-id="07d21-146">You can run commands directly on your cluster by using SSH.</span></span>

  <span data-ttu-id="07d21-147">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="07d21-147">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="07d21-148">__Web connectivity__: HDInsight clusters provide the Ambari web UI.</span><span class="sxs-lookup"><span data-stu-id="07d21-148">__Web connectivity__: HDInsight clusters provide the Ambari web UI.</span></span> <span data-ttu-id="07d21-149">You can easily monitor, configure, and manage services on your cluster by using the Ambari web UI.</span><span class="sxs-lookup"><span data-stu-id="07d21-149">You can easily monitor, configure, and manage services on your cluster by using the Ambari web UI.</span></span> <span data-ttu-id="07d21-150">Storm on HDInsight also provides the Storm UI.</span><span class="sxs-lookup"><span data-stu-id="07d21-150">Storm on HDInsight also provides the Storm UI.</span></span> <span data-ttu-id="07d21-151">You can monitor and manage running Storm topologies from your browser by using the Storm UI.</span><span class="sxs-lookup"><span data-stu-id="07d21-151">You can monitor and manage running Storm topologies from your browser by using the Storm UI.</span></span>

  <span data-ttu-id="07d21-152">For more information, see [Manage HDInsight using the Ambari Web UI](hdinsight-hadoop-manage-ambari.md) and [Monitor and manage using the Storm UI](hdinsight-storm-deploy-monitor-topology-linux.md#monitor-and-manage-storm-ui).</span><span class="sxs-lookup"><span data-stu-id="07d21-152">For more information, see [Manage HDInsight using the Ambari Web UI](hdinsight-hadoop-manage-ambari.md) and [Monitor and manage using the Storm UI](hdinsight-storm-deploy-monitor-topology-linux.md#monitor-and-manage-storm-ui).</span></span>

* <span data-ttu-id="07d21-153">__Azure PowerShell and Azure CLI__: PowerShell and CLI both provide command-line utilities that you can use from your client system to work with HDInsight and other Azure services.</span><span class="sxs-lookup"><span data-stu-id="07d21-153">__Azure PowerShell and Azure CLI__: PowerShell and CLI both provide command-line utilities that you can use from your client system to work with HDInsight and other Azure services.</span></span>

* <span data-ttu-id="07d21-154">__Visual Studio integration__: Azure Data Lake Tools for Visual Studio include project templates for creating C# Storm topologies by using the SCP.Net framework.</span><span class="sxs-lookup"><span data-stu-id="07d21-154">__Visual Studio integration__: Azure Data Lake Tools for Visual Studio include project templates for creating C# Storm topologies by using the SCP.Net framework.</span></span> <span data-ttu-id="07d21-155">Data Lake Tools also provide tools to deploy, monitor, and manage solutions with Storm on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="07d21-155">Data Lake Tools also provide tools to deploy, monitor, and manage solutions with Storm on HDInsight.</span></span>

  <span data-ttu-id="07d21-156">For more information, see [Develop C# Storm topologies with the HDInsight Tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="07d21-156">For more information, see [Develop C# Storm topologies with the HDInsight Tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

## <a name="integration-with-other-azure-services"></a><span data-ttu-id="07d21-157">Integration with other Azure services</span><span class="sxs-lookup"><span data-stu-id="07d21-157">Integration with other Azure services</span></span>

* <span data-ttu-id="07d21-158">__Azure Data Lake Store__: For an example of using Data Lake Store with Storm, see [Use Azure Data Lake Store with Apache Storm on HDInsight](hdinsight-storm-write-data-lake-store.md).</span><span class="sxs-lookup"><span data-stu-id="07d21-158">__Azure Data Lake Store__: For an example of using Data Lake Store with Storm, see [Use Azure Data Lake Store with Apache Storm on HDInsight](hdinsight-storm-write-data-lake-store.md).</span></span>

* <span data-ttu-id="07d21-159">__Event Hubs__: For an example of using Event Hubs with Storm, see the following documents:</span><span class="sxs-lookup"><span data-stu-id="07d21-159">__Event Hubs__: For an example of using Event Hubs with Storm, see the following documents:</span></span>

    * [<span data-ttu-id="07d21-160">Develop a Java-based topology for Storm on HDInsight</span><span class="sxs-lookup"><span data-stu-id="07d21-160">Develop a Java-based topology for Storm on HDInsight</span></span>](hdinsight-storm-develop-java-topology.md)

    * [<span data-ttu-id="07d21-161">Process events from Azure Event Hubs with Storm on HDInsight (C#)</span><span class="sxs-lookup"><span data-stu-id="07d21-161">Process events from Azure Event Hubs with Storm on HDInsight (C#)</span></span>](hdinsight-storm-develop-csharp-event-hub-topology.md)

* <span data-ttu-id="07d21-162">__SQL Database__, __DocumentDB__, __Event Hubs__, and __HBase__: Template examples are included in the Data Lake Tools for Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="07d21-162">__SQL Database__, __DocumentDB__, __Event Hubs__, and __HBase__: Template examples are included in the Data Lake Tools for Visual Studio.</span></span> <span data-ttu-id="07d21-163">For more information, see [Develop a C# topology for Storm on HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="07d21-163">For more information, see [Develop a C# topology for Storm on HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

## <a name="reliability"></a><span data-ttu-id="07d21-164">Reliability</span><span class="sxs-lookup"><span data-stu-id="07d21-164">Reliability</span></span>

<span data-ttu-id="07d21-165">Storm guarantees that each incoming message is always fully processed, even when the data analysis is spread over hundreds of nodes.</span><span class="sxs-lookup"><span data-stu-id="07d21-165">Storm guarantees that each incoming message is always fully processed, even when the data analysis is spread over hundreds of nodes.</span></span>

<span data-ttu-id="07d21-166">The Nimbus node provides functionality similar to the Hadoop JobTracker, and it assigns tasks to other nodes in a cluster through Zookeeper.</span><span class="sxs-lookup"><span data-stu-id="07d21-166">The Nimbus node provides functionality similar to the Hadoop JobTracker, and it assigns tasks to other nodes in a cluster through Zookeeper.</span></span> <span data-ttu-id="07d21-167">Zookeeper nodes provide coordination for a cluster and facilitate communication between Nimbus and the Supervisor process on the worker nodes.</span><span class="sxs-lookup"><span data-stu-id="07d21-167">Zookeeper nodes provide coordination for a cluster and facilitate communication between Nimbus and the Supervisor process on the worker nodes.</span></span> <span data-ttu-id="07d21-168">If one processing node goes down, the Nimbus node is informed, and it assigns the task and associated data to another node.</span><span class="sxs-lookup"><span data-stu-id="07d21-168">If one processing node goes down, the Nimbus node is informed, and it assigns the task and associated data to another node.</span></span>

<span data-ttu-id="07d21-169">The default configuration for Storm is to have only one Nimbus node.</span><span class="sxs-lookup"><span data-stu-id="07d21-169">The default configuration for Storm is to have only one Nimbus node.</span></span> <span data-ttu-id="07d21-170">Storm on HDInsight runs two Nimbus nodes.</span><span class="sxs-lookup"><span data-stu-id="07d21-170">Storm on HDInsight runs two Nimbus nodes.</span></span> <span data-ttu-id="07d21-171">If the primary node fails, the HDInsight cluster switches to the secondary node while the primary node is recovered.</span><span class="sxs-lookup"><span data-stu-id="07d21-171">If the primary node fails, the HDInsight cluster switches to the secondary node while the primary node is recovered.</span></span> <span data-ttu-id="07d21-172">The following diagram illustrates the task flow configuration for Storm on HDInsight:</span><span class="sxs-lookup"><span data-stu-id="07d21-172">The following diagram illustrates the task flow configuration for Storm on HDInsight:</span></span>

![Diagram of nimbus, zookeeper, and supervisor](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-storm-overview/nimbus.png)

## <a name="scale"></a><span data-ttu-id="07d21-174">Scale</span><span class="sxs-lookup"><span data-stu-id="07d21-174">Scale</span></span>

<span data-ttu-id="07d21-175">Although you can specify the number of nodes in your cluster during creation, you might want to grow or shrink the cluster to match workload.</span><span class="sxs-lookup"><span data-stu-id="07d21-175">Although you can specify the number of nodes in your cluster during creation, you might want to grow or shrink the cluster to match workload.</span></span> <span data-ttu-id="07d21-176">You can change the number of nodes in all HDInsight clusters, even while processing data.</span><span class="sxs-lookup"><span data-stu-id="07d21-176">You can change the number of nodes in all HDInsight clusters, even while processing data.</span></span>

> [!NOTE]
> <span data-ttu-id="07d21-177">To take advantage of new nodes added through scaling, you need to rebalance topologies started before the cluster size was increased.</span><span class="sxs-lookup"><span data-stu-id="07d21-177">To take advantage of new nodes added through scaling, you need to rebalance topologies started before the cluster size was increased.</span></span>

## <a name="support"></a><span data-ttu-id="07d21-178">Support</span><span class="sxs-lookup"><span data-stu-id="07d21-178">Support</span></span>

<span data-ttu-id="07d21-179">Storm on HDInsight comes with full enterprise-level continuous support.</span><span class="sxs-lookup"><span data-stu-id="07d21-179">Storm on HDInsight comes with full enterprise-level continuous support.</span></span> <span data-ttu-id="07d21-180">Storm on HDInsight also has an SLA of 99.9 percent.</span><span class="sxs-lookup"><span data-stu-id="07d21-180">Storm on HDInsight also has an SLA of 99.9 percent.</span></span> <span data-ttu-id="07d21-181">That means we guarantee that a cluster has external connectivity at least 99.9 percent of the time.</span><span class="sxs-lookup"><span data-stu-id="07d21-181">That means we guarantee that a cluster has external connectivity at least 99.9 percent of the time.</span></span>

<span data-ttu-id="07d21-182">For more information, see [Azure support](https://azure.microsoft.com/support/options/).</span><span class="sxs-lookup"><span data-stu-id="07d21-182">For more information, see [Azure support](https://azure.microsoft.com/support/options/).</span></span>

## <a name="common-use-cases"></a><span data-ttu-id="07d21-183">Common use cases</span><span class="sxs-lookup"><span data-stu-id="07d21-183">Common use cases</span></span>

<span data-ttu-id="07d21-184">The following are some common scenarios for which you might use Storm on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="07d21-184">The following are some common scenarios for which you might use Storm on HDInsight.</span></span> 

* <span data-ttu-id="07d21-185">Internet of Things (IoT)</span><span class="sxs-lookup"><span data-stu-id="07d21-185">Internet of Things (IoT)</span></span>
* <span data-ttu-id="07d21-186">Fraud detection</span><span class="sxs-lookup"><span data-stu-id="07d21-186">Fraud detection</span></span>
* <span data-ttu-id="07d21-187">Social analytics</span><span class="sxs-lookup"><span data-stu-id="07d21-187">Social analytics</span></span>
* <span data-ttu-id="07d21-188">Extraction, transformation, and loading (ETL)</span><span class="sxs-lookup"><span data-stu-id="07d21-188">Extraction, transformation, and loading (ETL)</span></span>
* <span data-ttu-id="07d21-189">Network monitoring</span><span class="sxs-lookup"><span data-stu-id="07d21-189">Network monitoring</span></span>
* <span data-ttu-id="07d21-190">Search</span><span class="sxs-lookup"><span data-stu-id="07d21-190">Search</span></span>
* <span data-ttu-id="07d21-191">Mobile engagement</span><span class="sxs-lookup"><span data-stu-id="07d21-191">Mobile engagement</span></span>

<span data-ttu-id="07d21-192">For information about real-world scenarios, see the [How companies are using Storm](https://storm.apache.org/documentation/Powered-By.html) document.</span><span class="sxs-lookup"><span data-stu-id="07d21-192">For information about real-world scenarios, see the [How companies are using Storm](https://storm.apache.org/documentation/Powered-By.html) document.</span></span>

## <a name="development"></a><span data-ttu-id="07d21-193">Development</span><span class="sxs-lookup"><span data-stu-id="07d21-193">Development</span></span>

<span data-ttu-id="07d21-194">.NET developers can design and implement topologies in C# by using Data Lake Tools for Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="07d21-194">.NET developers can design and implement topologies in C# by using Data Lake Tools for Visual Studio.</span></span> <span data-ttu-id="07d21-195">You can also create hybrid topologies that use Java and C# components.</span><span class="sxs-lookup"><span data-stu-id="07d21-195">You can also create hybrid topologies that use Java and C# components.</span></span>

<span data-ttu-id="07d21-196">For more information, see [Develop C# topologies for Storm on HDInsight using Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="07d21-196">For more information, see [Develop C# topologies for Storm on HDInsight using Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

<span data-ttu-id="07d21-197">You can also develop Java solutions by using the IDE of your choice.</span><span class="sxs-lookup"><span data-stu-id="07d21-197">You can also develop Java solutions by using the IDE of your choice.</span></span> <span data-ttu-id="07d21-198">For more information, see [Develop Java topologies for Storm on HDInsight](hdinsight-storm-develop-java-topology.md).</span><span class="sxs-lookup"><span data-stu-id="07d21-198">For more information, see [Develop Java topologies for Storm on HDInsight](hdinsight-storm-develop-java-topology.md).</span></span>

<span data-ttu-id="07d21-199">Python can also be used to develop Storm components.</span><span class="sxs-lookup"><span data-stu-id="07d21-199">Python can also be used to develop Storm components.</span></span> <span data-ttu-id="07d21-200">For more information, see [Develop Storm topologies using Python on HDInsight](hdinsight-storm-develop-python-topology.md).</span><span class="sxs-lookup"><span data-stu-id="07d21-200">For more information, see [Develop Storm topologies using Python on HDInsight](hdinsight-storm-develop-python-topology.md).</span></span>

## <a name="common-development-patterns"></a><span data-ttu-id="07d21-201">Common development patterns</span><span class="sxs-lookup"><span data-stu-id="07d21-201">Common development patterns</span></span>

### <a name="guaranteed-message-processing"></a><span data-ttu-id="07d21-202">Guaranteed message processing</span><span class="sxs-lookup"><span data-stu-id="07d21-202">Guaranteed message processing</span></span>

<span data-ttu-id="07d21-203">Storm can provide different levels of guaranteed message processing.</span><span class="sxs-lookup"><span data-stu-id="07d21-203">Storm can provide different levels of guaranteed message processing.</span></span> <span data-ttu-id="07d21-204">For example, a basic Storm application can guarantee at-least-once processing, and Trident can guarantee exactly once processing.</span><span class="sxs-lookup"><span data-stu-id="07d21-204">For example, a basic Storm application can guarantee at-least-once processing, and Trident can guarantee exactly once processing.</span></span>

<span data-ttu-id="07d21-205">For more information, see [Guarantees on data processing](https://storm.apache.org/about/guarantees-data-processing.html) at apache.org.</span><span class="sxs-lookup"><span data-stu-id="07d21-205">For more information, see [Guarantees on data processing](https://storm.apache.org/about/guarantees-data-processing.html) at apache.org.</span></span>

### <a name="ibasicbolt"></a><span data-ttu-id="07d21-206">IBasicBolt</span><span class="sxs-lookup"><span data-stu-id="07d21-206">IBasicBolt</span></span>

<span data-ttu-id="07d21-207">The pattern of reading an input tuple, emitting zero or more tuples, and then acking the input tuple immediately at the end of the execute method is common.</span><span class="sxs-lookup"><span data-stu-id="07d21-207">The pattern of reading an input tuple, emitting zero or more tuples, and then acking the input tuple immediately at the end of the execute method is common.</span></span> <span data-ttu-id="07d21-208">Storm provides the [IBasicBolt](https://storm.apache.org/apidocs/backtype/storm/topology/IBasicBolt.html) interface to automate this pattern.</span><span class="sxs-lookup"><span data-stu-id="07d21-208">Storm provides the [IBasicBolt](https://storm.apache.org/apidocs/backtype/storm/topology/IBasicBolt.html) interface to automate this pattern.</span></span>

### <a name="joins"></a><span data-ttu-id="07d21-209">Joins</span><span class="sxs-lookup"><span data-stu-id="07d21-209">Joins</span></span>

<span data-ttu-id="07d21-210">How data streams are joined varies between applications.</span><span class="sxs-lookup"><span data-stu-id="07d21-210">How data streams are joined varies between applications.</span></span> <span data-ttu-id="07d21-211">For example, you can join each tuple from multiple streams into one new stream, or you can join only batches of tuples for a specific window.</span><span class="sxs-lookup"><span data-stu-id="07d21-211">For example, you can join each tuple from multiple streams into one new stream, or you can join only batches of tuples for a specific window.</span></span> <span data-ttu-id="07d21-212">Either way, joining can be accomplished by using [fieldsGrouping](http://javadox.com/org.apache.storm/storm-core/0.9.1-incubating/backtype/storm/topology/InputDeclarer.html#fieldsGrouping%28java.lang.String,%20backtype.storm.tuple.Fields%29), which is a way of defining how tuples are routed to bolts.</span><span class="sxs-lookup"><span data-stu-id="07d21-212">Either way, joining can be accomplished by using [fieldsGrouping](http://javadox.com/org.apache.storm/storm-core/0.9.1-incubating/backtype/storm/topology/InputDeclarer.html#fieldsGrouping%28java.lang.String,%20backtype.storm.tuple.Fields%29), which is a way of defining how tuples are routed to bolts.</span></span>

<span data-ttu-id="07d21-213">In the following Java example, fieldsGrouping is used to route tuples that originate from components "1", "2", and "3" to the MyJoiner bolt:</span><span class="sxs-lookup"><span data-stu-id="07d21-213">In the following Java example, fieldsGrouping is used to route tuples that originate from components "1", "2", and "3" to the MyJoiner bolt:</span></span>

    builder.setBolt("join", new MyJoiner(), parallelism) .fieldsGrouping("1", new Fields("joinfield1", "joinfield2")) .fieldsGrouping("2", new Fields("joinfield1", "joinfield2")) .fieldsGrouping("3", new Fields("joinfield1", "joinfield2"));

### <a name="batches"></a><span data-ttu-id="07d21-214">Batches</span><span class="sxs-lookup"><span data-stu-id="07d21-214">Batches</span></span>

<span data-ttu-id="07d21-215">Storm provides an internal timing mechanism known as a "tick tuple," which can be used to emit a batch every X seconds.</span><span class="sxs-lookup"><span data-stu-id="07d21-215">Storm provides an internal timing mechanism known as a "tick tuple," which can be used to emit a batch every X seconds.</span></span>

<span data-ttu-id="07d21-216">For an example of using a tick tuple from a C# component, see [PartialBoltCount.cs](https://github.com/hdinsight/hdinsight-storm-examples/blob/3b2c960549cac122e8874931df4801f0934fffa7/EventCountExample/EventCountTopology/src/main/java/com/microsoft/hdinsight/storm/examples/PartialCountBolt.java).</span><span class="sxs-lookup"><span data-stu-id="07d21-216">For an example of using a tick tuple from a C# component, see [PartialBoltCount.cs](https://github.com/hdinsight/hdinsight-storm-examples/blob/3b2c960549cac122e8874931df4801f0934fffa7/EventCountExample/EventCountTopology/src/main/java/com/microsoft/hdinsight/storm/examples/PartialCountBolt.java).</span></span>

<span data-ttu-id="07d21-217">Trident is based on processing batches of tuples.</span><span class="sxs-lookup"><span data-stu-id="07d21-217">Trident is based on processing batches of tuples.</span></span>

### <a name="caches"></a><span data-ttu-id="07d21-218">Caches</span><span class="sxs-lookup"><span data-stu-id="07d21-218">Caches</span></span>

<span data-ttu-id="07d21-219">In-memory caching is often used as a mechanism for speeding up processing because it keeps frequently used assets in memory.</span><span class="sxs-lookup"><span data-stu-id="07d21-219">In-memory caching is often used as a mechanism for speeding up processing because it keeps frequently used assets in memory.</span></span> <span data-ttu-id="07d21-220">Because a topology is distributed across multiple nodes, and multiple processes within each node, you should consider using [fieldsGrouping](http://javadox.com/org.apache.storm/storm-core/0.9.1-incubating/backtype/storm/topology/InputDeclarer.html#fieldsGrouping%28java.lang.String,%20backtype.storm.tuple.Fields%29).</span><span class="sxs-lookup"><span data-stu-id="07d21-220">Because a topology is distributed across multiple nodes, and multiple processes within each node, you should consider using [fieldsGrouping](http://javadox.com/org.apache.storm/storm-core/0.9.1-incubating/backtype/storm/topology/InputDeclarer.html#fieldsGrouping%28java.lang.String,%20backtype.storm.tuple.Fields%29).</span></span> <span data-ttu-id="07d21-221">Use `fieldsGrouping` to ensure that tuples containing the fields that are used for cache lookup are always routed to the same process.</span><span class="sxs-lookup"><span data-stu-id="07d21-221">Use `fieldsGrouping` to ensure that tuples containing the fields that are used for cache lookup are always routed to the same process.</span></span> <span data-ttu-id="07d21-222">This grouping functionality avoids duplication of cache entries across processes.</span><span class="sxs-lookup"><span data-stu-id="07d21-222">This grouping functionality avoids duplication of cache entries across processes.</span></span>

### <a name="stream-top-n"></a><span data-ttu-id="07d21-223">Stream "top N"</span><span class="sxs-lookup"><span data-stu-id="07d21-223">Stream "top N"</span></span>

<span data-ttu-id="07d21-224">When your topology depends on calculating a top N value, calculate the top N value in parallel.</span><span class="sxs-lookup"><span data-stu-id="07d21-224">When your topology depends on calculating a top N value, calculate the top N value in parallel.</span></span> <span data-ttu-id="07d21-225">Then merge the output from those calculations into a global value.</span><span class="sxs-lookup"><span data-stu-id="07d21-225">Then merge the output from those calculations into a global value.</span></span> <span data-ttu-id="07d21-226">This operation can be done by using [fieldsGrouping](http://javadox.com/org.apache.storm/storm-core/0.9.1-incubating/backtype/storm/topology/InputDeclarer.html#fieldsGrouping%28java.lang.String,%20backtype.storm.tuple.Fields%29) to route by field for parallel processing, and then route to a bolt that globally determines the top N value.</span><span class="sxs-lookup"><span data-stu-id="07d21-226">This operation can be done by using [fieldsGrouping](http://javadox.com/org.apache.storm/storm-core/0.9.1-incubating/backtype/storm/topology/InputDeclarer.html#fieldsGrouping%28java.lang.String,%20backtype.storm.tuple.Fields%29) to route by field for parallel processing, and then route to a bolt that globally determines the top N value.</span></span>

<span data-ttu-id="07d21-227">For an example of calculating a top N value, see the [RollingTopWords](https://github.com/nathanmarz/storm-starter/blob/master/src/jvm/storm/starter/RollingTopWords.java) example.</span><span class="sxs-lookup"><span data-stu-id="07d21-227">For an example of calculating a top N value, see the [RollingTopWords](https://github.com/nathanmarz/storm-starter/blob/master/src/jvm/storm/starter/RollingTopWords.java) example.</span></span>

## <a name="logging"></a><span data-ttu-id="07d21-228">Logging</span><span class="sxs-lookup"><span data-stu-id="07d21-228">Logging</span></span>

<span data-ttu-id="07d21-229">Storm uses Apache Log4j to log information.</span><span class="sxs-lookup"><span data-stu-id="07d21-229">Storm uses Apache Log4j to log information.</span></span> <span data-ttu-id="07d21-230">By default, a large amount of data is logged, and it can be difficult to sort through the information.</span><span class="sxs-lookup"><span data-stu-id="07d21-230">By default, a large amount of data is logged, and it can be difficult to sort through the information.</span></span> <span data-ttu-id="07d21-231">You can include a logging configuration file as part of your Storm topology to control logging behavior.</span><span class="sxs-lookup"><span data-stu-id="07d21-231">You can include a logging configuration file as part of your Storm topology to control logging behavior.</span></span>

<span data-ttu-id="07d21-232">For an example topology that demonstrates how to configure logging, see [Java-based WordCount](hdinsight-storm-develop-java-topology.md) example for Storm on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="07d21-232">For an example topology that demonstrates how to configure logging, see [Java-based WordCount](hdinsight-storm-develop-java-topology.md) example for Storm on HDInsight.</span></span>

## <a name="next-steps"></a><span data-ttu-id="07d21-233">Next steps</span><span class="sxs-lookup"><span data-stu-id="07d21-233">Next steps</span></span>

<span data-ttu-id="07d21-234">Learn more about real-time analytics solutions with Storm on HDInsight:</span><span class="sxs-lookup"><span data-stu-id="07d21-234">Learn more about real-time analytics solutions with Storm on HDInsight:</span></span>

* <span data-ttu-id="07d21-235">[Get started with Storm on HDInsight][gettingstarted]</span><span class="sxs-lookup"><span data-stu-id="07d21-235">[Get started with Storm on HDInsight][gettingstarted]</span></span>
* [<span data-ttu-id="07d21-236">Example topologies for Storm on HDInsight</span><span class="sxs-lookup"><span data-stu-id="07d21-236">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)

[stormtrident]: https://storm.apache.org/documentation/Trident-API-Overview.html
[samoa]: http://yahooeng.tumblr.com/post/65453012905/introducing-samoa-an-open-source-platform-for-mining
[apachetutorial]: https://storm.apache.org/documentation/Tutorial.html
[gettingstarted]: hdinsight-apache-storm-tutorial-get-started-linux.md


