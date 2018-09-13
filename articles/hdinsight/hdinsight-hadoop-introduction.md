---
title: What is Hadoop? Intro to Azure HDInsight | Microsoft Docs
description: Get an introduction to the Hadoop ecosystem and components on HDInsight. HDInsight includes Hadoop, Spark, HBase, and more for big data processing and analysis.
keywords: big data analysis,introduction to hadoop,what is hadoop,hadoop technology stack,hadoop ecosystem
services: hdinsight
documentationcenter: ''
author: cjgronlund
manager: jhubbard
editor: cgronlun
ms.assetid: e56a396a-1b39-43e0-b543-f2dee5b8dd3a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/14/2016
ms.author: cgronlun
ms.openlocfilehash: a29b4fccc2d9a2e2913467f3b1c28386e7caa807
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661239"
---
# <a name="an-introduction-to-the-hadoop-ecosystem-on-azure-hdinsight"></a>An introduction to the Hadoop ecosystem on Azure HDInsight
 This article provides an introduction to Hadoop on Azure HDInsight, its ecosystem, and big data. Learn about the Hadoop components, common terminology, and scenarios for big data analysis.

## <a name="what-is-hadoop-on-hdinsight"></a>What is Hadoop on HDInsight?
Hadoop refers to an ecosystem of open-source software that is a framework for distributed processing, storing, and analysis of big data sets on clusters of computers. Azure HDInsight makes the Hadoop components from the **Hortonworks Data Platform (HDP)** distribution available in the cloud, deploys managed clusters with high reliability and availability, and provides enterprise-grade security and governance with Active Directory.  

Apache Hadoop was the original open-source project for big data processing. Following was the development of related software and utilities considered part of the Hadoop technology stack, including Apache Hive, Apache HBase, Apache Spark, Apache Kafka, and many others. See [Overview of the Hadoop ecosystem in HDInsight](#overview) for details.

## <a name="what-is-big-data"></a>What is big data?
Big data describes any large body of digital information, from the text in a Twitter feed, to the sensor information from industrial equipment, to information about customer browsing and purchases on a website. Big data can be historical (meaning stored data) or real-time (meaning streamed directly from the source). Big data is being collected in ever-escalating volumes, at increasingly higher velocities, and in an expanding variety formats.

For big data to provide actionable intelligence or insight, you must collect relevant data and ask the right questions. You must also make sure the data is accessible, cleaned, analyzed, and then presented in a useful way. That's where big data analysis on Hadoop in HDInsight can help.

## <a name="overview"></a>Overview of the Hadoop ecosystem in HDInsight
HDInsight is a cloud distribution on Microsoft Azure of the rapidly expanding Apache Hadoop technology stack for big data analysis. It includes implementations of Apache Spark, HBase, Kafka, Storm, Pig, Hive, Interactive Hive, Sqoop, Oozie, Ambari, and so on. HDInsight also integrates with business intelligence (BI) tools such as Power BI, Excel, SQL Server Analysis Services, and SQL Server Reporting Services.

### <a name="hadoop-hbase-spark-kafka-interactive-hive-storm-customized-and-other-clusters"></a>Hadoop, HBase, Spark, Kafka, Interactive Hive, Storm, customized, and other clusters
HDInsight offers the following cluster types:

* **[Apache Hadoop](https://wiki.apache.org/hadoop)**: Provides reliable data storage with [HDFS](#hdfs), and a simple [MapReduce](#mapreduce) programming model to process and analyze data in parallel.
* **[Apache Spark](http://spark.apache.org/)**: A parallel processing framework that supports in-memory processing to boost the performance of big-data analysis applications, Spark works for SQL, streaming data, and machine learning. See [Overview: What is Apache Spark in HDInsight?](hdinsight-apache-spark-overview.md)
* **[Apache HBase](http://hbase.apache.org/)**: A NoSQL database built on Hadoop that provides random access and strong consistency for large amounts of unstructured and semi-structured data - potentially billions of rows times millions of columns. See [Overview of HBase on HDInsight](hdinsight-hbase-overview.md).
* **[Microsoft R Server](https://msdn.microsoft.com/en-us/microsoft-r/rserver)**: An enterprise-class server for hosting and managing parallel, distributed R processes. It provides data scientists, statisticians, and R programmers with on-demand access to scalable, distributed methods of analytics on HDInsight. See [Overview of R Server on HDInsight](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-r-server-overview).
* **[Apache Storm](https://storm.incubator.apache.org/)**: A distributed, real-time computation system for processing large streams of data fast. Storm is offered as a managed cluster in HDInsight. See [Analyze real-time sensor data using Storm and Hadoop](hdinsight-storm-sensor-data-analysis.md).
* **[Apache Interactive Hive preview (AKA: Live Long and Process)](https://cwiki.apache.org/confluence/display/Hive/LLAP)**: In-memory caching for interactive and faster Hive queries. See [Use Interactive Hive in HDInsight](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-use-interactive-hive).
* **[Apache Kafka preview](https://kafka.apache.org/)**: An open-source platform used for building streaming data pipelines and applications. Kafka also provides message-queue functionality that allows you to publish and subscribe to data streams. See [Introduction to Apache Kafka on HDInsight](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-kafka-introduction).
* **[Domain-joined clusters preview](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-domain-joined-introduction)**: A cluster joined to an Active Directory domain so that you can control access and provide governance for data.
* **[Custom clusters with script actions](hdinsight-hadoop-customize-cluster-linux.md)**: Clusters with scripts that run during provisioning and install additional components.

### <a name="example-customization-scripts"></a>Example customization scripts
Script actions are Bash scripts on Linux that run during cluster provisioning, and can be used to install additional components on the cluster.

The following example scripts are provided by the HDInsight team:

* [Hue](hdinsight-hadoop-hue-linux.md): A set of web applications used to interact with a cluster. Linux clusters only.
* [Giraph](hdinsight-hadoop-giraph-install-linux.md): Graph processing to model relationships between things or people.
* [R](hdinsight-hadoop-r-scripts-linux.md): An open-source language and environment for statistical computing used in machine learning.
* [Solr](hdinsight-hadoop-solr-install-linux.md): An enterprise-scale search platform that allows full-text search on data.

For information on developing your own Script Actions, see [Script Action development with HDInsight](hdinsight-hadoop-script-actions-linux.md).

## <a name="what-are-the-hadoop-components-and-utilities"></a>What are the Hadoop components and utilities?
The following components and utilities are included on HDInsight clusters.

* **[Ambari](#ambari)**: Cluster provisioning, management, monitoring, and utilities.
* **[Avro](#avro)** (Microsoft .NET Library for Avro): Data serialization for the Microsoft .NET environment.
* **[Hive & HCatalog](#hive)**: Structured Query Language (SQL)-like querying, and a table and storage management layer.
* **[Mahout](#mahout)**: For scalable machine learning applications.
* **[MapReduce](#mapreduce)**: Legacy framework for Hadoop distributed processing and resource management. See [YARN](#yarn), the next-generation resource framework.
* **[Oozie](#oozie)**: Workflow management.
* **[Phoenix](#phoenix)**: Relational database layer over HBase.
* **[Pig](#pig)**: Simpler scripting for MapReduce transformations.
* **[Sqoop](#sqoop)**: Data import and export.
* **[Tez](#tez)**: Allows data-intensive processes to run efficiently at scale.
* **[YARN](#yarn)**: Part of the Hadoop core library and next generation of the MapReduce software framework.
* **[ZooKeeper](#zookeeper)**: Coordination of processes in distributed systems.

> [!NOTE]
> For information on the specific components and version information, see [Hadoop components, versioning, and service offerings in HDInsight][component-versioning]
>
>

### <a name="ambari"></a>Ambari
Apache Ambari is for provisioning, managing and monitoring Apache Hadoop clusters. It includes an intuitive collection of operator tools and a robust set of APIs that hide the complexity of Hadoop, simplifying the operation of clusters. HDInsight clusters on Linux provide both the Ambari web UI and the Ambari REST API, while clusters on Windows provide a subset of the REST API. Ambari Views on HDInsight clusters allow plug-in UI capabilities.

See [Manage HDInsight clusters using Ambari](hdinsight-hadoop-manage-ambari.md) (Linux only), [Monitor Hadoop clusters in HDInsight using the Ambari API](hdinsight-monitor-use-ambari-api.md), and <a target="_blank" href="https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md">Apache Ambari API reference</a>.

### <a name="avro"></a>Avro (Microsoft .NET Library for Avro)
The Microsoft .NET Library for Avro implements the Apache Avro compact binary data interchange format for serialization for the Microsoft .NET environment. It uses <a target="_blank" href="http://www.json.org/">JavaScript Object Notation (JSON)</a> to define a language-agnostic schema that underwrites language interoperability, meaning data serialized in one language can be read in another. Detailed information on the format can be found in the <a target=_"blank" href="http://avro.apache.org/docs/current/spec.html">Apache Avro Specification</a>.
The format of Avro files supports the distributed MapReduce programming model. Files are “splittable”, meaning you can seek any point in a file and start reading from a particular block. To find out how, see [Serialize data with the Microsoft .NET Library for Avro](hdinsight-dotnet-avro-serialization.md).

### <a name="hdfs"></a>HDFS
Hadoop Distributed File System (HDFS) is a distributed file system that, with MapReduce and YARN, is the core of the Hadoop ecosystem. HDFS is the standard file system for Hadoop clusters on HDInsight.

### <a name="hive"></a>Hive & HCatalog
<a target="_blank" href="http://hive.apache.org/">Apache Hive</a> is data warehouse software built on Hadoop that allows you to query and manage large datasets in distributed storage by using a SQL-like language called HiveQL. Hive, like Pig, is an abstraction on top of MapReduce. When run, Hive translates queries into a series of MapReduce jobs. Hive is conceptually closer to a relational database management system than Pig, and is therefore appropriate for use with more structured data. For unstructured data, Pig is the better choice. See [Use Hive with Hadoop in HDInsight](hdinsight-use-hive.md).

<a target="_blank" href="https://cwiki.apache.org/confluence/display/Hive/HCatalog/">Apache HCatalog</a> is a table and storage management layer for Hadoop that presents you with a relational view of data. In HCatalog, you can read and write files in any format for which a Hive SerDe (serializer-deserializer) can be written.

### <a name="mahout"></a>Mahout
<a target="_blank" href="https://mahout.apache.org/">Apache Mahout</a> is a scalable library of machine learning algorithms that run on Hadoop. Using principles of statistics, machine learning applications teach systems to learn from data and to use past outcomes to determine future behavior. See [Generate movie recommendations using Mahout on Hadoop](hdinsight-mahout.md).

### <a name="mapreduce"></a>MapReduce
MapReduce is the legacy software framework for Hadoop for writing applications to batch process big data sets in parallel. A MapReduce job splits large datasets and organizes the data into key-value pairs for processing.

[YARN](#yarn) is the Hadoop next-generation resource manager and application framework, and is referred to as MapReduce 2.0. MapReduce jobs run on YARN.

For more information on MapReduce, see <a target="_blank" href="http://wiki.apache.org/hadoop/MapReduce">MapReduce</a> in the Hadoop Wiki.

### <a name="oozie"></a>Oozie
<a target="_blank" href="http://oozie.apache.org/">Apache Oozie</a> is a workflow coordination system that manages Hadoop jobs. It is integrated with the Hadoop stack and supports Hadoop jobs for MapReduce, Pig, Hive, and Sqoop. It can also be used to schedule jobs specific to a system, like Java programs or shell scripts. See [Use Oozie with Hadoop](hdinsight-use-oozie.md).

### <a name="phoenix"></a>Phoenix
<a  target="_blank" href="http://phoenix.apache.org/">Apache Phoenix</a> is a relational database layer over HBase. Phoenix includes a JDBC driver that allows you to query and manage SQL tables directly. Phoenix translates queries and other statements into native NoSQL API calls - instead of using MapReduce - thus enabling faster applications on top of NoSQL stores. See [Use Apache Phoenix and SQuirreL with HBase clusters](hdinsight-hbase-phoenix-squirrel.md).

### <a name="pig"></a>Pig
<a  target="_blank" href="http://pig.apache.org/">Apache Pig</a> is a high-level platform that allows you to perform complex MapReduce transformations on very large datasets by using a simple scripting language called Pig Latin. Pig translates the Pig Latin scripts so they’ll run within Hadoop. You can create User-Defined Functions (UDFs) to extend Pig Latin. See [Use Pig with Hadoop](hdinsight-use-pig.md).

### <a name="sqoop"></a>Sqoop
<a  target="_blank" href="http://sqoop.apache.org/">Apache Sqoop</a> is tool that transfers bulk data between Hadoop and relational databases such a SQL, or other structured data stores, as efficiently as possible. See [Use Sqoop with Hadoop](hdinsight-use-sqoop.md).

### <a name="tez"></a>Tez
<a  target="_blank" href="http://tez.apache.org/">Apache Tez</a> is an application framework built on Hadoop YARN that executes complex, acyclic graphs of general data processing. It's a more flexible and powerful successor to the MapReduce framework that allows data-intensive processes, such as Hive, to run more efficiently at scale. See ["Use Apache Tez for improved performance" in Use Hive and HiveQL](hdinsight-use-hive.md#usetez).

### <a name="yarn"></a>YARN
Apache YARN is the next generation of MapReduce (MapReduce 2.0, or MRv2) and supports data processing scenarios beyond MapReduce batch processing with greater scalability and real-time processing. YARN provides resource management and a distributed application framework. MapReduce jobs run on YARN.

To learn about YARN, see <a target="_blank" href="http://hadoop.apache.org/docs/current/hadoop-yarn/hadoop-yarn-site/YARN.html">Apache Hadoop NextGen MapReduce (YARN)</a>.

### <a name="zookeeper"></a>ZooKeeper
<a  target="_blank" href="http://zookeeper.apache.org/">Apache ZooKeeper</a> coordinates processes in large distributed systems by means of a shared hierarchical namespace of data registers (znodes). Znodes contain small amounts of meta information needed to coordinate processes: status, location, configuration, and so on.

## <a name="programming-languages-on-hdinsight"></a>Programming languages on HDInsight
HDInsight clusters--Hadoop, HBase, Storm, and Spark clusters--support a number of programming languages, but some aren't installed by default. For libraries, modules, or packages not installed by default, use a script action to install the component. See [Script action development with HDInsight](hdinsight-hadoop-script-actions-linux.md).

### <a name="default-programming-language-support"></a>Default programming language support
By default, HDInsight clusters support:

* Java
* Python

Additional languages can be installed using script actions: [Script action development with HDInsight](hdinsight-hadoop-script-actions-linux.md).

### <a name="java-virtual-machine-jvm-languages"></a>Java virtual machine (JVM) languages
Many languages other than Java can be run using a Java virtual machine (JVM); however, running some of these languages may require additional components installed on the cluster.

These JVM-based languages are supported on HDInsight clusters:

* Clojure
* Jython (Python for Java)
* Scala

### <a name="hadoop-specific-languages"></a>Hadoop-specific languages
HDInsight clusters support the following languages that are specific to the Hadoop ecosystem:

* Pig Latin for Pig jobs
* HiveQL for Hive jobs and SparkSQL

## <a name="advantage"></a>Advantages of Hadoop in the cloud
As part of the Azure cloud ecosystem, Hadoop in HDInsight offers a number of benefits, among them:

* Automatic provisioning of Hadoop clusters. HDInsight clusters are much easier to create than manually configuring Hadoop clusters. For details, see [Provision Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).
* State-of-the-art Hadoop components. For details, see [Hadoop components, versioning, and service offerings in HDInsight][component-versioning].
* High availability and reliability of clusters. See [Availability and reliability of Hadoop clusters in HDInsight](hdinsight-high-availability-linux.md) for details.
* Efficient and economical data storage with Azure Storage or Azure Data Lake Store, both Hadoop-compatible storage options. See [Use Azure Storage with Hadoop in HDInsight](hdinsight-hadoop-use-blob-storage.md) or [Use Data Lake Store with an HDInsight cluster](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-hdinsight-hadoop-use-portal) for details.
* Integration with other Azure services, including [Web apps](https://azure.microsoft.com/documentation/services/app-service/web/) and [SQL Database](https://azure.microsoft.com/documentation/services/sql-database/).
* Additional VM sizes and types for running HDInsight clusters. See [Hadoop components, versioning, and service offerings in HDInsight][component-versioning] for details.
* Cluster scaling. Cluster scaling enables you to change the number of nodes of a running HDInsight cluster without having to delete or re-create it.
* Virtual Network support. HDInsight clusters can be used with Azure Virtual Network to support isolation of cloud resources or hybrid scenarios that link cloud resources with those in your datacenter.
* Low entry cost. Start a [free trial](https://azure.microsoft.com/free/), or consult [HDInsight pricing details](https://azure.microsoft.com/pricing/details/hdinsight/).

To read more about the advantages on Hadoop in HDInsight, see the [Azure features page for HDInsight][marketing-page].

## <a name="hdinsight-standard-and-hdinsight-premium"></a>HDInsight Standard and HDInsight Premium
HDInsight provides big data cloud offerings in two categories, Standard and Premium. HDInsight Standard provides an enterprise-scale cluster that organizations can use to run their big data workloads. HDInsight Premium builds on that and provides advanced analytical and security capabilities for an HDInsight cluster. For more information, see [Azure HDInsight Premium](hdinsight-component-versioning.md#hdinsight-standard-and-hdinsight-premium)

## <a id="resources"></a>Resources for learning more about big-data analysis, Hadoop, and HDInsight
Build on this introduction to Hadoop in the cloud and big data analysis with the resources below.

### <a name="hadoop-documentation-for-hdinsight"></a>Hadoop documentation for HDInsight
* [HDInsight documentation](https://azure.microsoft.com/documentation/services/hdinsight/): The documentation page for Hadoop on Azure HDInsight with links to articles, videos, and more resources.
* [Get started with Hadoop in HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md): A quick-start tutorial for provisioning HDInsight Hadoop clusters and running sample Hive queries.
* [Get started with Spark in HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md): A quick-start tutorial for creating a Spark cluster and running interactive Spark SQL queries.
* [Use R Server on HDInsight](hdinsight-hadoop-r-server-get-started.md): Start using R Server in HDInsight Premium.
* [Provision HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md): Learn how to provision an HDInsight Hadoop cluster through the Azure portal, Azure CLI, or Azure PowerShell.

### <a name="apache-hadoop"></a>Apache Hadoop
* <a target="_blank" href="http://hadoop.apache.org/">Apache Hadoop</a>: Learn more about the Apache Hadoop software library, a framework that allows for the distributed processing of large datasets across clusters of computers.
* <a target="_blank" href="http://hadoop.apache.org/docs/r1.0.4/hdfs_design.html">HDFS</a>: Learn more about the architecture and design of the Hadoop Distributed File System, the primary storage system used by Hadoop applications.
* <a target="_blank" href="http://hadoop.apache.org/docs/r1.2.1/mapred_tutorial.html">MapReduce Tutorial</a>: Learn more about the programming framework for writing Hadoop applications that rapidly process large amounts of data in parallel on large clusters of compute nodes.

### <a name="microsoft-business-intelligence"></a>Microsoft business intelligence
Familiar business intelligence (BI) tools - such as Excel, PowerPivot, SQL Server Analysis Services, and SQL Server Reporting Services - retrieve, analyze, and report data integrated with HDInsight by using either the Power Query add-in or the Microsoft Hive ODBC Driver.

These BI tools can help in your big-data analysis:

* [Connect Excel to Hadoop with Power Query](hdinsight-connect-excel-power-query.md): Learn how to connect Excel to the Azure Storage account that stores the data associated with your HDInsight cluster by using Microsoft Power Query for Excel. Windows workstation required. Works with clusters on Linux or Windows.
* [Connect Excel to Hadoop with the Microsoft Hive ODBC Driver](hdinsight-connect-excel-hive-odbc-driver.md): Learn how to import data from HDInsight with the Microsoft Hive ODBC Driver. Windows workstation required. Works with clusters on Linux or Windows.
* [Microsoft Cloud Platform](http://www.microsoft.com/server-cloud/solutions/business-intelligence/default.aspx): Learn about Power BI for Office 365, download the SQL Server trial, and set up SharePoint Server 2013 and SQL Server BI.
* [SQL Server Analysis Services](http://msdn.microsoft.com/library/hh231701.aspx).
* [SQL Server Reporting Services](http://msdn.microsoft.com/library/ms159106.aspx).

[marketing-page]: https://azure.microsoft.com/services/hdinsight/
[component-versioning]: hdinsight-component-versioning.md
[zookeeper]: http://zookeeper.apache.org/
