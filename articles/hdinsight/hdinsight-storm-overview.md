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
# <a name="introduction-to-apache-storm-on-hdinsight-real-time-analytics-for-hadoop"></a>Introduction to Apache Storm on HDInsight: Real-time analytics for Hadoop

You can create distributed, real-time analytics solutions by using Apache Storm on Azure HDInsight.

Storm is a distributed, fault-tolerant, open-source computation system. You can use Storm to process data in real time with Hadoop. Storm solutions can also provide guaranteed processing of data, with the ability to replay data that was not successfully processed the first time.

## <a name="how-does-storm-work"></a>How does Storm work?

Storm runs topologies instead of the MapReduce jobs that you might be familiar with in HDInsight or Hadoop. Topologies are composed of multiple components that are arranged in a directed acyclic graph (DAG). The following diagram illustrates how data flows between components in a basic word-count topology:

![Example of how components are arranged in a Storm topology](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-storm-overview/wordcount-topology.png)

* Spout components bring data into a topology. They emit one or more streams into the topology.

* Bolt components consume streams emitted from spouts or other bolts. Bolts might optionally emit new streams into the topology. Bolts are also responsible for writing data to persistent storage, such as HDFS or HBase.

## <a name="why-use-storm-on-hdinsight"></a>Why use Storm on HDInsight?

Storm on HDInsight provides the following key benefits:

* Performs as a managed service with an SLA of 99.9 percent uptime.

* Supports easy customization by running scripts against a cluster during or after creation. For more information, see [Customize HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md).

* Uses various languages. You can write Storm components in the language of your choice, such as Java, C#, and Python.

    * Integrates Visual Studio with HDInsight for the development, management, and monitoring of C# topologies. For more information, see [Develop C# Storm topologies with the HDInsight Tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).

    * Supports the Trident Java interface. You can create Storm topologies that support exactly once processing of messages, transactional datastore persistence, and a set of common stream analytics operations.

*  Scales clusters up and down easily. You can add or remove worker nodes with no impact to running Storm topologies.

* Integrates with the following Azure services:

    * Azure Event Hubs

    * Azure Virtual Network

    * Azure SQL Database

    * Azure Storage

    * Azure DocumentDB

* Securely combines the capabilities of multiple HDInsight clusters by using Virtual Network. You can create analytic pipelines that use HDInsight, HBase, or Hadoop clusters.

For a list of companies that are using Storm for their real-time analytics solutions, see [Companies using Apache Storm](https://storm.apache.org/documentation/Powered-By.html).

To get started using Storm, see [Get started with Storm on HDInsight][gettingstarted].

## <a name="ease-of-creation"></a>Ease of creation

You can provision a new Storm cluster on HDInsight in minutes. For more information on creating a Storm cluster, see [Get started with Storm on HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md).

## <a name="ease-of-use"></a>Ease of use

* __Secure Shell (SSH) connectivity__: You can access the head nodes of your HDInsight cluster over the Internet by using SSH. You can run commands directly on your cluster by using SSH.

  For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

* __Web connectivity__: HDInsight clusters provide the Ambari web UI. You can easily monitor, configure, and manage services on your cluster by using the Ambari web UI. Storm on HDInsight also provides the Storm UI. You can monitor and manage running Storm topologies from your browser by using the Storm UI.

  For more information, see [Manage HDInsight using the Ambari Web UI](hdinsight-hadoop-manage-ambari.md) and [Monitor and manage using the Storm UI](hdinsight-storm-deploy-monitor-topology-linux.md#monitor-and-manage-storm-ui).

* __Azure PowerShell and Azure CLI__: PowerShell and CLI both provide command-line utilities that you can use from your client system to work with HDInsight and other Azure services.

* __Visual Studio integration__: Azure Data Lake Tools for Visual Studio include project templates for creating C# Storm topologies by using the SCP.Net framework. Data Lake Tools also provide tools to deploy, monitor, and manage solutions with Storm on HDInsight.

  For more information, see [Develop C# Storm topologies with the HDInsight Tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).

## <a name="integration-with-other-azure-services"></a>Integration with other Azure services

* __Azure Data Lake Store__: For an example of using Data Lake Store with Storm, see [Use Azure Data Lake Store with Apache Storm on HDInsight](hdinsight-storm-write-data-lake-store.md).

* __Event Hubs__: For an example of using Event Hubs with Storm, see the following documents:

    * [Develop a Java-based topology for Storm on HDInsight](hdinsight-storm-develop-java-topology.md)

    * [Process events from Azure Event Hubs with Storm on HDInsight (C#)](hdinsight-storm-develop-csharp-event-hub-topology.md)

* __SQL Database__, __DocumentDB__, __Event Hubs__, and __HBase__: Template examples are included in the Data Lake Tools for Visual Studio. For more information, see [Develop a C# topology for Storm on HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md).

## <a name="reliability"></a>Reliability

Storm guarantees that each incoming message is always fully processed, even when the data analysis is spread over hundreds of nodes.

The Nimbus node provides functionality similar to the Hadoop JobTracker, and it assigns tasks to other nodes in a cluster through Zookeeper. Zookeeper nodes provide coordination for a cluster and facilitate communication between Nimbus and the Supervisor process on the worker nodes. If one processing node goes down, the Nimbus node is informed, and it assigns the task and associated data to another node.

The default configuration for Storm is to have only one Nimbus node. Storm on HDInsight runs two Nimbus nodes. If the primary node fails, the HDInsight cluster switches to the secondary node while the primary node is recovered. The following diagram illustrates the task flow configuration for Storm on HDInsight:

![Diagram of nimbus, zookeeper, and supervisor](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-storm-overview/nimbus.png)

## <a name="scale"></a>Scale

Although you can specify the number of nodes in your cluster during creation, you might want to grow or shrink the cluster to match workload. You can change the number of nodes in all HDInsight clusters, even while processing data.

> [!NOTE]
> To take advantage of new nodes added through scaling, you need to rebalance topologies started before the cluster size was increased.

## <a name="support"></a>Support

Storm on HDInsight comes with full enterprise-level continuous support. Storm on HDInsight also has an SLA of 99.9 percent. That means we guarantee that a cluster has external connectivity at least 99.9 percent of the time.

For more information, see [Azure support](https://azure.microsoft.com/support/options/).

## <a name="common-use-cases"></a>Common use cases

The following are some common scenarios for which you might use Storm on HDInsight. 

* Internet of Things (IoT)
* Fraud detection
* Social analytics
* Extraction, transformation, and loading (ETL)
* Network monitoring
* Search
* Mobile engagement

For information about real-world scenarios, see the [How companies are using Storm](https://storm.apache.org/documentation/Powered-By.html) document.

## <a name="development"></a>Development

.NET developers can design and implement topologies in C# by using Data Lake Tools for Visual Studio. You can also create hybrid topologies that use Java and C# components.

For more information, see [Develop C# topologies for Storm on HDInsight using Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).

You can also develop Java solutions by using the IDE of your choice. For more information, see [Develop Java topologies for Storm on HDInsight](hdinsight-storm-develop-java-topology.md).

Python can also be used to develop Storm components. For more information, see [Develop Storm topologies using Python on HDInsight](hdinsight-storm-develop-python-topology.md).

## <a name="common-development-patterns"></a>Common development patterns

### <a name="guaranteed-message-processing"></a>Guaranteed message processing

Storm can provide different levels of guaranteed message processing. For example, a basic Storm application can guarantee at-least-once processing, and Trident can guarantee exactly once processing.

For more information, see [Guarantees on data processing](https://storm.apache.org/about/guarantees-data-processing.html) at apache.org.

### <a name="ibasicbolt"></a>IBasicBolt

The pattern of reading an input tuple, emitting zero or more tuples, and then acking the input tuple immediately at the end of the execute method is common. Storm provides the [IBasicBolt](https://storm.apache.org/apidocs/backtype/storm/topology/IBasicBolt.html) interface to automate this pattern.

### <a name="joins"></a>Joins

How data streams are joined varies between applications. For example, you can join each tuple from multiple streams into one new stream, or you can join only batches of tuples for a specific window. Either way, joining can be accomplished by using [fieldsGrouping](http://javadox.com/org.apache.storm/storm-core/0.9.1-incubating/backtype/storm/topology/InputDeclarer.html#fieldsGrouping%28java.lang.String,%20backtype.storm.tuple.Fields%29), which is a way of defining how tuples are routed to bolts.

In the following Java example, fieldsGrouping is used to route tuples that originate from components "1", "2", and "3" to the MyJoiner bolt:

    builder.setBolt("join", new MyJoiner(), parallelism) .fieldsGrouping("1", new Fields("joinfield1", "joinfield2")) .fieldsGrouping("2", new Fields("joinfield1", "joinfield2")) .fieldsGrouping("3", new Fields("joinfield1", "joinfield2"));

### <a name="batches"></a>Batches

Storm provides an internal timing mechanism known as a "tick tuple," which can be used to emit a batch every X seconds.

For an example of using a tick tuple from a C# component, see [PartialBoltCount.cs](https://github.com/hdinsight/hdinsight-storm-examples/blob/3b2c960549cac122e8874931df4801f0934fffa7/EventCountExample/EventCountTopology/src/main/java/com/microsoft/hdinsight/storm/examples/PartialCountBolt.java).

Trident is based on processing batches of tuples.

### <a name="caches"></a>Caches

In-memory caching is often used as a mechanism for speeding up processing because it keeps frequently used assets in memory. Because a topology is distributed across multiple nodes, and multiple processes within each node, you should consider using [fieldsGrouping](http://javadox.com/org.apache.storm/storm-core/0.9.1-incubating/backtype/storm/topology/InputDeclarer.html#fieldsGrouping%28java.lang.String,%20backtype.storm.tuple.Fields%29). Use `fieldsGrouping` to ensure that tuples containing the fields that are used for cache lookup are always routed to the same process. This grouping functionality avoids duplication of cache entries across processes.

### <a name="stream-top-n"></a>Stream "top N"

When your topology depends on calculating a top N value, calculate the top N value in parallel. Then merge the output from those calculations into a global value. This operation can be done by using [fieldsGrouping](http://javadox.com/org.apache.storm/storm-core/0.9.1-incubating/backtype/storm/topology/InputDeclarer.html#fieldsGrouping%28java.lang.String,%20backtype.storm.tuple.Fields%29) to route by field for parallel processing, and then route to a bolt that globally determines the top N value.

For an example of calculating a top N value, see the [RollingTopWords](https://github.com/nathanmarz/storm-starter/blob/master/src/jvm/storm/starter/RollingTopWords.java) example.

## <a name="logging"></a>Logging

Storm uses Apache Log4j to log information. By default, a large amount of data is logged, and it can be difficult to sort through the information. You can include a logging configuration file as part of your Storm topology to control logging behavior.

For an example topology that demonstrates how to configure logging, see [Java-based WordCount](hdinsight-storm-develop-java-topology.md) example for Storm on HDInsight.

## <a name="next-steps"></a>Next steps

Learn more about real-time analytics solutions with Storm on HDInsight:

* [Get started with Storm on HDInsight][gettingstarted]
* [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md)

[stormtrident]: https://storm.apache.org/documentation/Trident-API-Overview.html
[samoa]: http://yahooeng.tumblr.com/post/65453012905/introducing-samoa-an-open-source-platform-for-mining
[apachetutorial]: https://storm.apache.org/documentation/Tutorial.html
[gettingstarted]: hdinsight-apache-storm-tutorial-get-started-linux.md


