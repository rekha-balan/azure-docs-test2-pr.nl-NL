---
title: 'Tutorial: Apache Kafka with Storm on HDInsight - Azure '
description: Learn how to create a streaming pipeline using Apache Storm and Apache Kafka on HDInsight. In this tutorial, you use the KafkaBolt and KafkaSpout components to stream data from Kafka.
services: hdinsight
author: jasonwhowell
ms.author: jasonh
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: tutorial
ms.date: 05/21/2018
ms.openlocfilehash: 7aa8f0b62459c376113bca5a0c58cc7dd3b5280c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44791627"
---
# <a name="tutorial-use-apache-storm-with-kafka-on-hdinsight"></a><span data-ttu-id="10b8f-104">Tutorial: Use Apache Storm with Kafka on HDInsight</span><span class="sxs-lookup"><span data-stu-id="10b8f-104">Tutorial: Use Apache Storm with Kafka on HDInsight</span></span>

<span data-ttu-id="10b8f-105">This tutorial demonstrates how to use an Apache Storm topology to read and write data with Apache Kafka on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="10b8f-105">This tutorial demonstrates how to use an Apache Storm topology to read and write data with Apache Kafka on HDInsight.</span></span> <span data-ttu-id="10b8f-106">This tutorial also demonstrates how to persist data to the HDFS-compatible storage on the Storm cluster.</span><span class="sxs-lookup"><span data-stu-id="10b8f-106">This tutorial also demonstrates how to persist data to the HDFS-compatible storage on the Storm cluster.</span></span>

<span data-ttu-id="10b8f-107">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="10b8f-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="10b8f-108">Storm and Kafka</span><span class="sxs-lookup"><span data-stu-id="10b8f-108">Storm and Kafka</span></span>
> * <span data-ttu-id="10b8f-109">Understanding the code</span><span class="sxs-lookup"><span data-stu-id="10b8f-109">Understanding the code</span></span>
> * <span data-ttu-id="10b8f-110">Create Kafka and Storm clusters</span><span class="sxs-lookup"><span data-stu-id="10b8f-110">Create Kafka and Storm clusters</span></span>
> * <span data-ttu-id="10b8f-111">Build the topology</span><span class="sxs-lookup"><span data-stu-id="10b8f-111">Build the topology</span></span>
> * <span data-ttu-id="10b8f-112">Configure the topology</span><span class="sxs-lookup"><span data-stu-id="10b8f-112">Configure the topology</span></span>
> * <span data-ttu-id="10b8f-113">Create the Kafka topic</span><span class="sxs-lookup"><span data-stu-id="10b8f-113">Create the Kafka topic</span></span>
> * <span data-ttu-id="10b8f-114">Start the topologies</span><span class="sxs-lookup"><span data-stu-id="10b8f-114">Start the topologies</span></span>
> * <span data-ttu-id="10b8f-115">Stop the topologies</span><span class="sxs-lookup"><span data-stu-id="10b8f-115">Stop the topologies</span></span>
> * <span data-ttu-id="10b8f-116">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="10b8f-116">Clean up resources</span></span>

## <a name="prerequisites"></a><span data-ttu-id="10b8f-117">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="10b8f-117">Prerequisites</span></span>

* <span data-ttu-id="10b8f-118">Familiarity with creating Kafka topics.</span><span class="sxs-lookup"><span data-stu-id="10b8f-118">Familiarity with creating Kafka topics.</span></span> <span data-ttu-id="10b8f-119">For more information, see the [Kafka on HDInsight quickstart](./kafka/apache-kafka-get-started.md) document.</span><span class="sxs-lookup"><span data-stu-id="10b8f-119">For more information, see the [Kafka on HDInsight quickstart](./kafka/apache-kafka-get-started.md) document.</span></span>

* <span data-ttu-id="10b8f-120">Familiarity with building and deploying Storm solutions (topologies).</span><span class="sxs-lookup"><span data-stu-id="10b8f-120">Familiarity with building and deploying Storm solutions (topologies).</span></span> <span data-ttu-id="10b8f-121">Specifically, topologies that use the Flux framework.</span><span class="sxs-lookup"><span data-stu-id="10b8f-121">Specifically, topologies that use the Flux framework.</span></span> <span data-ttu-id="10b8f-122">For more information, see the [Create a Storm topology in Java](./storm/apache-storm-develop-java-topology.md) document.</span><span class="sxs-lookup"><span data-stu-id="10b8f-122">For more information, see the [Create a Storm topology in Java](./storm/apache-storm-develop-java-topology.md) document.</span></span>

* <span data-ttu-id="10b8f-123">[Java JDK 1.8](http://www.oracle.com/technetwork/pt/java/javase/downloads/jdk8-downloads-2133151.html) or higher.</span><span class="sxs-lookup"><span data-stu-id="10b8f-123">[Java JDK 1.8](http://www.oracle.com/technetwork/pt/java/javase/downloads/jdk8-downloads-2133151.html) or higher.</span></span> <span data-ttu-id="10b8f-124">HDInsight 3.5 or higher require Java 8.</span><span class="sxs-lookup"><span data-stu-id="10b8f-124">HDInsight 3.5 or higher require Java 8.</span></span>

* [<span data-ttu-id="10b8f-125">Maven 3.x</span><span class="sxs-lookup"><span data-stu-id="10b8f-125">Maven 3.x</span></span>](https://maven.apache.org/download.cgi)

* <span data-ttu-id="10b8f-126">An SSH client (you need the `ssh` and `scp` commands) - For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="10b8f-126">An SSH client (you need the `ssh` and `scp` commands) - For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="10b8f-127">The following environment variables may be set when you install Java and the JDK on your development workstation.</span><span class="sxs-lookup"><span data-stu-id="10b8f-127">The following environment variables may be set when you install Java and the JDK on your development workstation.</span></span> <span data-ttu-id="10b8f-128">However, you should check that they exist and that they contain the correct values for your system.</span><span class="sxs-lookup"><span data-stu-id="10b8f-128">However, you should check that they exist and that they contain the correct values for your system.</span></span>

* <span data-ttu-id="10b8f-129">`JAVA_HOME` - should point to the directory where the JDK is installed.</span><span class="sxs-lookup"><span data-stu-id="10b8f-129">`JAVA_HOME` - should point to the directory where the JDK is installed.</span></span>
* <span data-ttu-id="10b8f-130">`PATH` - should contain the following paths:</span><span class="sxs-lookup"><span data-stu-id="10b8f-130">`PATH` - should contain the following paths:</span></span>
  
    * <span data-ttu-id="10b8f-131">`JAVA_HOME` (or the equivalent path).</span><span class="sxs-lookup"><span data-stu-id="10b8f-131">`JAVA_HOME` (or the equivalent path).</span></span>
    * <span data-ttu-id="10b8f-132">`JAVA_HOME\bin` (or the equivalent path).</span><span class="sxs-lookup"><span data-stu-id="10b8f-132">`JAVA_HOME\bin` (or the equivalent path).</span></span>
    * <span data-ttu-id="10b8f-133">The directory where Maven is installed.</span><span class="sxs-lookup"><span data-stu-id="10b8f-133">The directory where Maven is installed.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="10b8f-134">The steps in this document require an Azure resource group that contains both a Storm on HDInsight and a Kafka on HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="10b8f-134">The steps in this document require an Azure resource group that contains both a Storm on HDInsight and a Kafka on HDInsight cluster.</span></span> <span data-ttu-id="10b8f-135">These clusters are both located within an Azure Virtual Network, which allows the Storm cluster to directly communicate with the Kafka cluster.</span><span class="sxs-lookup"><span data-stu-id="10b8f-135">These clusters are both located within an Azure Virtual Network, which allows the Storm cluster to directly communicate with the Kafka cluster.</span></span>
> 
> <span data-ttu-id="10b8f-136">For your convenience, this document links to a template that can create all the required Azure resources.</span><span class="sxs-lookup"><span data-stu-id="10b8f-136">For your convenience, this document links to a template that can create all the required Azure resources.</span></span> 
>
> <span data-ttu-id="10b8f-137">For more information on using HDInsight in a virtual network, see the [Extend HDInsight using a virtual network](hdinsight-extend-hadoop-virtual-network.md) document.</span><span class="sxs-lookup"><span data-stu-id="10b8f-137">For more information on using HDInsight in a virtual network, see the [Extend HDInsight using a virtual network](hdinsight-extend-hadoop-virtual-network.md) document.</span></span>

## <a name="storm-and-kafka"></a><span data-ttu-id="10b8f-138">Storm and Kafka</span><span class="sxs-lookup"><span data-stu-id="10b8f-138">Storm and Kafka</span></span>

<span data-ttu-id="10b8f-139">Apache Storm provides the several components for working with Kafka.</span><span class="sxs-lookup"><span data-stu-id="10b8f-139">Apache Storm provides the several components for working with Kafka.</span></span> <span data-ttu-id="10b8f-140">The following components are used in this tutorial:</span><span class="sxs-lookup"><span data-stu-id="10b8f-140">The following components are used in this tutorial:</span></span>

* <span data-ttu-id="10b8f-141">`org.apache.storm.kafka.KafkaSpout`: This component reads data from Kafka.</span><span class="sxs-lookup"><span data-stu-id="10b8f-141">`org.apache.storm.kafka.KafkaSpout`: This component reads data from Kafka.</span></span> <span data-ttu-id="10b8f-142">This component relies on the following components:</span><span class="sxs-lookup"><span data-stu-id="10b8f-142">This component relies on the following components:</span></span>

    * <span data-ttu-id="10b8f-143">`org.apache.storm.kafka.SpoutConfig`: Provides configuration for the spout component.</span><span class="sxs-lookup"><span data-stu-id="10b8f-143">`org.apache.storm.kafka.SpoutConfig`: Provides configuration for the spout component.</span></span>

    * <span data-ttu-id="10b8f-144">`org.apache.storm.spout.SchemeAsMultiScheme` and `org.apache.storm.kafka.StringScheme`: How the data from Kafka is transformed into a Storm tuple.</span><span class="sxs-lookup"><span data-stu-id="10b8f-144">`org.apache.storm.spout.SchemeAsMultiScheme` and `org.apache.storm.kafka.StringScheme`: How the data from Kafka is transformed into a Storm tuple.</span></span>

* <span data-ttu-id="10b8f-145">`org.apache.storm.kafka.bolt.KafkaBolt`: This component writes data to Kafka.</span><span class="sxs-lookup"><span data-stu-id="10b8f-145">`org.apache.storm.kafka.bolt.KafkaBolt`: This component writes data to Kafka.</span></span> <span data-ttu-id="10b8f-146">This component relies on the following components:</span><span class="sxs-lookup"><span data-stu-id="10b8f-146">This component relies on the following components:</span></span>

    * <span data-ttu-id="10b8f-147">`org.apache.storm.kafka.bolt.selector.DefaultTopicSelector`: Describes the topic that is written to.</span><span class="sxs-lookup"><span data-stu-id="10b8f-147">`org.apache.storm.kafka.bolt.selector.DefaultTopicSelector`: Describes the topic that is written to.</span></span>

    * <span data-ttu-id="10b8f-148">`org.apache.kafka.common.serialization.StringSerializer`: Configures the bolt to serialize data as a string value.</span><span class="sxs-lookup"><span data-stu-id="10b8f-148">`org.apache.kafka.common.serialization.StringSerializer`: Configures the bolt to serialize data as a string value.</span></span>

    * <span data-ttu-id="10b8f-149">`org.apache.storm.kafka.bolt.mapper.FieldNameBasedTupleToKafkaMapper`: Maps from the tuple data structure used inside the Storm topology to fields stored in Kafka.</span><span class="sxs-lookup"><span data-stu-id="10b8f-149">`org.apache.storm.kafka.bolt.mapper.FieldNameBasedTupleToKafkaMapper`: Maps from the tuple data structure used inside the Storm topology to fields stored in Kafka.</span></span>

<span data-ttu-id="10b8f-150">These components are available in the `org.apache.storm : storm-kafka` package.</span><span class="sxs-lookup"><span data-stu-id="10b8f-150">These components are available in the `org.apache.storm : storm-kafka` package.</span></span> <span data-ttu-id="10b8f-151">Use the package version that matches the Storm version.</span><span class="sxs-lookup"><span data-stu-id="10b8f-151">Use the package version that matches the Storm version.</span></span> <span data-ttu-id="10b8f-152">For HDInsight 3.6, the Storm version is 1.1.0.</span><span class="sxs-lookup"><span data-stu-id="10b8f-152">For HDInsight 3.6, the Storm version is 1.1.0.</span></span>
<span data-ttu-id="10b8f-153">You also need the `org.apache.kafka : kafka_2.10` package, which contains additional Kafka components.</span><span class="sxs-lookup"><span data-stu-id="10b8f-153">You also need the `org.apache.kafka : kafka_2.10` package, which contains additional Kafka components.</span></span> <span data-ttu-id="10b8f-154">Use the package version that matches the Kafka version.</span><span class="sxs-lookup"><span data-stu-id="10b8f-154">Use the package version that matches the Kafka version.</span></span> <span data-ttu-id="10b8f-155">For HDInsight 3.6, the Kafka version is 0.10.0.0.</span><span class="sxs-lookup"><span data-stu-id="10b8f-155">For HDInsight 3.6, the Kafka version is 0.10.0.0.</span></span>

<span data-ttu-id="10b8f-156">The following XML is the dependency declaration in the `pom.xml` for a Maven project:</span><span class="sxs-lookup"><span data-stu-id="10b8f-156">The following XML is the dependency declaration in the `pom.xml` for a Maven project:</span></span>

```xml
<!-- Storm components for talking to Kafka -->
<dependency>
    <groupId>org.apache.storm</groupId>
    <artifactId>storm-kafka</artifactId>
    <version>1.1.0</version>
</dependency>
<!-- needs to be the same Kafka version as used on your cluster -->
<dependency>
    <groupId>org.apache.kafka</groupId>
    <artifactId>kafka_2.10</artifactId>
    <version>0.10.0.0</version>
    <!-- Exclude components that are loaded from the Storm cluster at runtime -->
    <exclusions>
        <exclusion>
            <groupId>org.apache.zookeeper</groupId>
            <artifactId>zookeeper</artifactId>
        </exclusion>
        <exclusion>
            <groupId>log4j</groupId>
            <artifactId>log4j</artifactId>
        </exclusion>
        <exclusion>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-log4j12</artifactId>
        </exclusion>
    </exclusions>
</dependency>
```

## <a name="understanding-the-code"></a><span data-ttu-id="10b8f-157">Understanding the code</span><span class="sxs-lookup"><span data-stu-id="10b8f-157">Understanding the code</span></span>

<span data-ttu-id="10b8f-158">The code used in this document is available at [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka).</span><span class="sxs-lookup"><span data-stu-id="10b8f-158">The code used in this document is available at [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka).</span></span>

<span data-ttu-id="10b8f-159">There are two topologies provided with this tutorial:</span><span class="sxs-lookup"><span data-stu-id="10b8f-159">There are two topologies provided with this tutorial:</span></span>

* <span data-ttu-id="10b8f-160">Kafka-writer: Generates random sentences and stores them to Kafka.</span><span class="sxs-lookup"><span data-stu-id="10b8f-160">Kafka-writer: Generates random sentences and stores them to Kafka.</span></span>

* <span data-ttu-id="10b8f-161">Kafka-reader: Reads data from Kafka and then stores it to the HDFS compatible file store for the Storm cluster.</span><span class="sxs-lookup"><span data-stu-id="10b8f-161">Kafka-reader: Reads data from Kafka and then stores it to the HDFS compatible file store for the Storm cluster.</span></span>

    > [!WARNING] 
    > <span data-ttu-id="10b8f-162">To enable the Storm to work with the HDFS compatible storage used by HDInsight, a script action is required.</span><span class="sxs-lookup"><span data-stu-id="10b8f-162">To enable the Storm to work with the HDFS compatible storage used by HDInsight, a script action is required.</span></span> <span data-ttu-id="10b8f-163">The script installs several jar files to the `extlib` path for Storm.</span><span class="sxs-lookup"><span data-stu-id="10b8f-163">The script installs several jar files to the `extlib` path for Storm.</span></span> <span data-ttu-id="10b8f-164">The template in this tutorial automatically uses the script during cluster creation.</span><span class="sxs-lookup"><span data-stu-id="10b8f-164">The template in this tutorial automatically uses the script during cluster creation.</span></span>
    >
    > <span data-ttu-id="10b8f-165">If you do not use the template in this document to create the Storm cluster, then you must manually apply the script action to your cluster.</span><span class="sxs-lookup"><span data-stu-id="10b8f-165">If you do not use the template in this document to create the Storm cluster, then you must manually apply the script action to your cluster.</span></span>
    >
    > <span data-ttu-id="10b8f-166">The script action is located at `https://hdiconfigactions2.blob.core.windows.net/stormextlib/stormextlib.sh` and is applied to the supervisor and nimbus nodes of the Storm cluster.</span><span class="sxs-lookup"><span data-stu-id="10b8f-166">The script action is located at `https://hdiconfigactions2.blob.core.windows.net/stormextlib/stormextlib.sh` and is applied to the supervisor and nimbus nodes of the Storm cluster.</span></span> <span data-ttu-id="10b8f-167">For more information on using script actions, see the [Customize HDInsight using script actions](hdinsight-hadoop-customize-cluster-linux.md) document.</span><span class="sxs-lookup"><span data-stu-id="10b8f-167">For more information on using script actions, see the [Customize HDInsight using script actions](hdinsight-hadoop-customize-cluster-linux.md) document.</span></span>

<span data-ttu-id="10b8f-168">The topologies are defined using [Flux](https://storm.apache.org/releases/1.1.2/flux.html).</span><span class="sxs-lookup"><span data-stu-id="10b8f-168">The topologies are defined using [Flux](https://storm.apache.org/releases/1.1.2/flux.html).</span></span> <span data-ttu-id="10b8f-169">Flux was introduced in Storm 0.10.x and allows you to separate the topology configuration from the code.</span><span class="sxs-lookup"><span data-stu-id="10b8f-169">Flux was introduced in Storm 0.10.x and allows you to separate the topology configuration from the code.</span></span> <span data-ttu-id="10b8f-170">For Topologies that use the Flux framework, the topology is defined in a YAML file.</span><span class="sxs-lookup"><span data-stu-id="10b8f-170">For Topologies that use the Flux framework, the topology is defined in a YAML file.</span></span> <span data-ttu-id="10b8f-171">The YAML file can be included as part of the topology.</span><span class="sxs-lookup"><span data-stu-id="10b8f-171">The YAML file can be included as part of the topology.</span></span> <span data-ttu-id="10b8f-172">It can also be a standalone file used when you submit the topology.</span><span class="sxs-lookup"><span data-stu-id="10b8f-172">It can also be a standalone file used when you submit the topology.</span></span> <span data-ttu-id="10b8f-173">Flux also supports variable substitution at run-time, which is used in this example.</span><span class="sxs-lookup"><span data-stu-id="10b8f-173">Flux also supports variable substitution at run-time, which is used in this example.</span></span>

<span data-ttu-id="10b8f-174">The following parameters are set at run time for these topologies:</span><span class="sxs-lookup"><span data-stu-id="10b8f-174">The following parameters are set at run time for these topologies:</span></span>

* <span data-ttu-id="10b8f-175">`${kafka.topic}`: The name of the Kafka topic that the topologies read/write to.</span><span class="sxs-lookup"><span data-stu-id="10b8f-175">`${kafka.topic}`: The name of the Kafka topic that the topologies read/write to.</span></span>

* <span data-ttu-id="10b8f-176">`${kafka.broker.hosts}`: The hosts that the Kafka brokers run on.</span><span class="sxs-lookup"><span data-stu-id="10b8f-176">`${kafka.broker.hosts}`: The hosts that the Kafka brokers run on.</span></span> <span data-ttu-id="10b8f-177">The broker information is used by the KafkaBolt when writing to Kafka.</span><span class="sxs-lookup"><span data-stu-id="10b8f-177">The broker information is used by the KafkaBolt when writing to Kafka.</span></span>

* <span data-ttu-id="10b8f-178">`${kafka.zookeeper.hosts}`: The hosts that Zookeeper runs on in the Kafka cluster.</span><span class="sxs-lookup"><span data-stu-id="10b8f-178">`${kafka.zookeeper.hosts}`: The hosts that Zookeeper runs on in the Kafka cluster.</span></span>

* <span data-ttu-id="10b8f-179">`${hdfs.url}`: The file system URL for the HDFSBolt component.</span><span class="sxs-lookup"><span data-stu-id="10b8f-179">`${hdfs.url}`: The file system URL for the HDFSBolt component.</span></span> <span data-ttu-id="10b8f-180">Indicates whether the data is written to an Azure Storage account or Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="10b8f-180">Indicates whether the data is written to an Azure Storage account or Azure Data Lake Store.</span></span>

* <span data-ttu-id="10b8f-181">`${hdfs.write.dir}`: The directory that data is written to.</span><span class="sxs-lookup"><span data-stu-id="10b8f-181">`${hdfs.write.dir}`: The directory that data is written to.</span></span>

<span data-ttu-id="10b8f-182">For more information on Flux topologies, see [https://storm.apache.org/releases/1.1.2/flux.html](https://storm.apache.org/releases/1.1.2/flux.html).</span><span class="sxs-lookup"><span data-stu-id="10b8f-182">For more information on Flux topologies, see [https://storm.apache.org/releases/1.1.2/flux.html](https://storm.apache.org/releases/1.1.2/flux.html).</span></span>

### <a name="kafka-writer"></a><span data-ttu-id="10b8f-183">Kafka-writer</span><span class="sxs-lookup"><span data-stu-id="10b8f-183">Kafka-writer</span></span>

<span data-ttu-id="10b8f-184">In the Kafka-writer topology, the Kafka bolt component takes two string values as parameters.</span><span class="sxs-lookup"><span data-stu-id="10b8f-184">In the Kafka-writer topology, the Kafka bolt component takes two string values as parameters.</span></span> <span data-ttu-id="10b8f-185">These parameters indicate which tuple fields the bolt sends to Kafka as __key__ and __message__ values.</span><span class="sxs-lookup"><span data-stu-id="10b8f-185">These parameters indicate which tuple fields the bolt sends to Kafka as __key__ and __message__ values.</span></span> <span data-ttu-id="10b8f-186">The key is used to partition data in Kafka.</span><span class="sxs-lookup"><span data-stu-id="10b8f-186">The key is used to partition data in Kafka.</span></span> <span data-ttu-id="10b8f-187">The message is the data being stored.</span><span class="sxs-lookup"><span data-stu-id="10b8f-187">The message is the data being stored.</span></span>

<span data-ttu-id="10b8f-188">In this example, the `com.microsoft.example.SentenceSpout` component emits a tuple that contains two fields, `key` and `message`.</span><span class="sxs-lookup"><span data-stu-id="10b8f-188">In this example, the `com.microsoft.example.SentenceSpout` component emits a tuple that contains two fields, `key` and `message`.</span></span> <span data-ttu-id="10b8f-189">The Kafka bolt extracts these fields and sends the data in them to Kafka.</span><span class="sxs-lookup"><span data-stu-id="10b8f-189">The Kafka bolt extracts these fields and sends the data in them to Kafka.</span></span>

<span data-ttu-id="10b8f-190">The fields don't have to use the names `key` and `message`.</span><span class="sxs-lookup"><span data-stu-id="10b8f-190">The fields don't have to use the names `key` and `message`.</span></span> <span data-ttu-id="10b8f-191">These names are used in this project to make the mapping easier to understand.</span><span class="sxs-lookup"><span data-stu-id="10b8f-191">These names are used in this project to make the mapping easier to understand.</span></span>

<span data-ttu-id="10b8f-192">The following YAML is the definition for the Kafka-writer component:</span><span class="sxs-lookup"><span data-stu-id="10b8f-192">The following YAML is the definition for the Kafka-writer component:</span></span>

```yaml
# kafka-writer
---

# topology definition
# name to be used when submitting
name: "kafka-writer"

# Components - constructors, property setters, and builder arguments.
# Currently, components must be declared in the order they are referenced
components:
  # Topic selector for KafkaBolt
  - id: "topicSelector"
    className: "org.apache.storm.kafka.bolt.selector.DefaultTopicSelector"
    constructorArgs:
      - "${kafka.topic}"

  # Mapper for KafkaBolt
  - id: "kafkaMapper"
    className: "org.apache.storm.kafka.bolt.mapper.FieldNameBasedTupleToKafkaMapper"
    constructorArgs:
      - "key"
      - "message"

  # Producer properties for KafkaBolt
  - id: "producerProperties"
    className: "java.util.Properties"
    configMethods:
      - name: "put"
        args:
          - "bootstrap.servers"
          - "${kafka.broker.hosts}"
      - name: "put"
        args:
          - "acks"
          - "1"
      - name: "put"
        args:
          - "key.serializer"
          - "org.apache.kafka.common.serialization.StringSerializer"
      - name: "put"
        args:
          - "value.serializer"
          - "org.apache.kafka.common.serialization.StringSerializer"
 

# Topology configuration
config:
  topology.workers: 2

# Spout definitions
spouts:
  - id: "sentence-spout"
    className: "com.microsoft.example.SentenceSpout"
    parallelism: 8

# Bolt definitions
bolts:
  - id: "kafka-bolt"
    className: "org.apache.storm.kafka.bolt.KafkaBolt"
    parallelism: 8
    configMethods:
    - name: "withProducerProperties"
      args: [ref: "producerProperties"]
    - name: "withTopicSelector"
      args: [ref: "topicSelector"]
    - name: "withTupleToKafkaMapper"
      args: [ref: "kafkaMapper"]

# Stream definitions

streams:
  - name: "spout --> kafka" # Streams data from the sentence spout to the Kafka bolt
    from: "sentence-spout"
    to: "kafka-bolt"
    grouping:
      type: SHUFFLE
```

### <a name="kafka-reader"></a><span data-ttu-id="10b8f-193">Kafka-reader</span><span class="sxs-lookup"><span data-stu-id="10b8f-193">Kafka-reader</span></span>

<span data-ttu-id="10b8f-194">In the Kafka-reader topology, the spout component reads data from Kafka as string values.</span><span class="sxs-lookup"><span data-stu-id="10b8f-194">In the Kafka-reader topology, the spout component reads data from Kafka as string values.</span></span> <span data-ttu-id="10b8f-195">The data is then written the Storm log by the logging component and to the HDFS compatible file system for the Storm cluster by the HDFS bolt component.</span><span class="sxs-lookup"><span data-stu-id="10b8f-195">The data is then written the Storm log by the logging component and to the HDFS compatible file system for the Storm cluster by the HDFS bolt component.</span></span>

```yaml
# kafka-reader
---

# topology definition
# name to be used when submitting
name: "kafka-reader"

# Components - constructors, property setters, and builder arguments.
# Currently, components must be declared in the order they are referenced
components:
  # Convert data from Kafka into string tuples in storm
  - id: "stringScheme"
    className: "org.apache.storm.kafka.StringScheme"
  - id: "stringMultiScheme"
    className: "org.apache.storm.spout.SchemeAsMultiScheme"
    constructorArgs:
      - ref: "stringScheme"

  - id: "zkHosts"
    className: "org.apache.storm.kafka.ZkHosts"
    constructorArgs:
      - "${kafka.zookeeper.hosts}"

  # Spout configuration
  - id: "spoutConfig"
    className: "org.apache.storm.kafka.SpoutConfig"
    constructorArgs:
      # brokerHosts
      - ref: "zkHosts"
      # topic
      - "${kafka.topic}"
      # zkRoot
      - ""
      # id
      - "readerid"
    properties:
      - name: "scheme"
        ref: "stringMultiScheme"

    # How often to sync files to HDFS; every 1000 tuples.
  - id: "syncPolicy"
    className: "org.apache.storm.hdfs.bolt.sync.CountSyncPolicy"
    constructorArgs:
      - 1

  # Rotate files when they hit 5 MB
  - id: "rotationPolicy"
    className: "org.apache.storm.hdfs.bolt.rotation.FileSizeRotationPolicy"
    constructorArgs:
      - 5
      - "KB"

  # File format; read the directory from filters at run time, and use a .txt extension when writing.
  - id: "fileNameFormat"
    className: "org.apache.storm.hdfs.bolt.format.DefaultFileNameFormat"
    configMethods:
      - name: "withPath"
        args: ["${hdfs.write.dir}"]
      - name: "withExtension"
        args: [".txt"]

  # Internal file format; fields delimited by `|`.
  - id: "recordFormat"
    className: "org.apache.storm.hdfs.bolt.format.DelimitedRecordFormat"
    configMethods:
      - name: "withFieldDelimiter"
        args: ["|"]

# Topology configuration
config:
  topology.workers: 2

# Spout definitions
spouts:
  - id: "kafka-spout"
    className: "org.apache.storm.kafka.KafkaSpout"
    constructorArgs:
      - ref: "spoutConfig"
    # Set to the number of partitions for the topic
    parallelism: 8

# Bolt definitions
bolts:
  - id: "logger-bolt"
    className: "com.microsoft.example.LoggerBolt"
    parallelism: 1
  
  - id: "hdfs-bolt"
    className: "org.apache.storm.hdfs.bolt.HdfsBolt"
    configMethods:
      - name: "withConfigKey"
        args: ["hdfs.config"]
      - name: "withFsUrl"
        args: ["${hdfs.url}"]
      - name: "withFileNameFormat"
        args: [ref: "fileNameFormat"]
      - name: "withRecordFormat"
        args: [ref: "recordFormat"]
      - name: "withRotationPolicy"
        args: [ref: "rotationPolicy"]
      - name: "withSyncPolicy"
        args: [ref: "syncPolicy"]
    parallelism: 1

# Stream definitions

streams:
  # Stream data to log
  - name: "kafka --> log" # name isn't used (placeholder for logging, UI, etc.)
    from: "kafka-spout"
    to: "logger-bolt"
    grouping:
      type: SHUFFLE
  
  # stream data to file
  - name: "kafka --> hdfs"
    from: "kafka-spout"
    to: "hdfs-bolt"
    grouping:
      type: SHUFFLE
```

### <a name="property-substitutions"></a><span data-ttu-id="10b8f-196">Property substitutions</span><span class="sxs-lookup"><span data-stu-id="10b8f-196">Property substitutions</span></span>

<span data-ttu-id="10b8f-197">The project contains a file named `dev.properties` that is used to pass parameters used by the topologies.</span><span class="sxs-lookup"><span data-stu-id="10b8f-197">The project contains a file named `dev.properties` that is used to pass parameters used by the topologies.</span></span> <span data-ttu-id="10b8f-198">It defines the following properties:</span><span class="sxs-lookup"><span data-stu-id="10b8f-198">It defines the following properties:</span></span>

| <span data-ttu-id="10b8f-199">dev.properties file</span><span class="sxs-lookup"><span data-stu-id="10b8f-199">dev.properties file</span></span> | <span data-ttu-id="10b8f-200">Description</span><span class="sxs-lookup"><span data-stu-id="10b8f-200">Description</span></span> |
| --- | --- |
| `kafka.zookeeper.hosts` | <span data-ttu-id="10b8f-201">The Zookeeper hosts for the Kafka cluster.</span><span class="sxs-lookup"><span data-stu-id="10b8f-201">The Zookeeper hosts for the Kafka cluster.</span></span> |
| `kafka.broker.hosts` | <span data-ttu-id="10b8f-202">The Kafka broker hosts (worker nodes).</span><span class="sxs-lookup"><span data-stu-id="10b8f-202">The Kafka broker hosts (worker nodes).</span></span> |
| `kafka.topic` | <span data-ttu-id="10b8f-203">The Kafka topic that the topologies use.</span><span class="sxs-lookup"><span data-stu-id="10b8f-203">The Kafka topic that the topologies use.</span></span> |
| `hdfs.write.dir` | <span data-ttu-id="10b8f-204">The directory that the Kafka-reader topology writes to.</span><span class="sxs-lookup"><span data-stu-id="10b8f-204">The directory that the Kafka-reader topology writes to.</span></span> |
| `hdfs.url` | <span data-ttu-id="10b8f-205">The file system used by the Storm cluster.</span><span class="sxs-lookup"><span data-stu-id="10b8f-205">The file system used by the Storm cluster.</span></span> <span data-ttu-id="10b8f-206">For Azure Storage accounts, use a value of `wasb:///`.</span><span class="sxs-lookup"><span data-stu-id="10b8f-206">For Azure Storage accounts, use a value of `wasb:///`.</span></span> <span data-ttu-id="10b8f-207">For Azure Data Lake Store, use a value of `adl:///`.</span><span class="sxs-lookup"><span data-stu-id="10b8f-207">For Azure Data Lake Store, use a value of `adl:///`.</span></span> |

## <a name="create-the-clusters"></a><span data-ttu-id="10b8f-208">Create the clusters</span><span class="sxs-lookup"><span data-stu-id="10b8f-208">Create the clusters</span></span>

<span data-ttu-id="10b8f-209">Apache Kafka on HDInsight does not provide access to the Kafka brokers over the public internet.</span><span class="sxs-lookup"><span data-stu-id="10b8f-209">Apache Kafka on HDInsight does not provide access to the Kafka brokers over the public internet.</span></span> <span data-ttu-id="10b8f-210">Anything that uses Kafka must be in the same Azure virtual network.</span><span class="sxs-lookup"><span data-stu-id="10b8f-210">Anything that uses Kafka must be in the same Azure virtual network.</span></span> <span data-ttu-id="10b8f-211">In this tutorial, both the Kafka and Storm clusters are located in the same Azure virtual network.</span><span class="sxs-lookup"><span data-stu-id="10b8f-211">In this tutorial, both the Kafka and Storm clusters are located in the same Azure virtual network.</span></span> 

<span data-ttu-id="10b8f-212">The following diagram shows how communication flows between Storm and Kafka:</span><span class="sxs-lookup"><span data-stu-id="10b8f-212">The following diagram shows how communication flows between Storm and Kafka:</span></span>

![Diagram of Storm and Kafka clusters in an Azure virtual network](./media/hdinsight-apache-storm-with-kafka/storm-kafka-vnet.png)

> [!NOTE]
> <span data-ttu-id="10b8f-214">Other services on the cluster such as SSH and Ambari can be accessed over the internet.</span><span class="sxs-lookup"><span data-stu-id="10b8f-214">Other services on the cluster such as SSH and Ambari can be accessed over the internet.</span></span> <span data-ttu-id="10b8f-215">For more information on the public ports available with HDInsight, see [Ports and URIs used by HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span><span class="sxs-lookup"><span data-stu-id="10b8f-215">For more information on the public ports available with HDInsight, see [Ports and URIs used by HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span></span>

<span data-ttu-id="10b8f-216">To create an Azure Virtual Network, and then create the Kafka and Storm clusters within it, use the following steps:</span><span class="sxs-lookup"><span data-stu-id="10b8f-216">To create an Azure Virtual Network, and then create the Kafka and Storm clusters within it, use the following steps:</span></span>

1. <span data-ttu-id="10b8f-217">Use the following button to sign in to Azure and open the template in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="10b8f-217">Use the following button to sign in to Azure and open the template in the Azure portal.</span></span>
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure-Samples%2Fhdinsight-storm-java-kafka%2Fmaster%2Fcreate-kafka-storm-clusters-in-vnet.json" target="_blank"><img src="./media/hdinsight-apache-storm-with-kafka/deploy-to-azure.png" alt="Deploy to Azure"></a>
   
    <span data-ttu-id="10b8f-218">The Azure Resource Manager template is located at **https://github.com/Azure-Samples/hdinsight-storm-java-kafka/blob/master/create-kafka-storm-clusters-in-vnet.json**.</span><span class="sxs-lookup"><span data-stu-id="10b8f-218">The Azure Resource Manager template is located at **https://github.com/Azure-Samples/hdinsight-storm-java-kafka/blob/master/create-kafka-storm-clusters-in-vnet.json**.</span></span> <span data-ttu-id="10b8f-219">It creates the following resources:</span><span class="sxs-lookup"><span data-stu-id="10b8f-219">It creates the following resources:</span></span>
    
    * <span data-ttu-id="10b8f-220">Azure resource group</span><span class="sxs-lookup"><span data-stu-id="10b8f-220">Azure resource group</span></span>
    * <span data-ttu-id="10b8f-221">Azure Virtual Network</span><span class="sxs-lookup"><span data-stu-id="10b8f-221">Azure Virtual Network</span></span>
    * <span data-ttu-id="10b8f-222">Azure Storage account</span><span class="sxs-lookup"><span data-stu-id="10b8f-222">Azure Storage account</span></span>
    * <span data-ttu-id="10b8f-223">Kafka on HDInsight version 3.6 (three worker nodes)</span><span class="sxs-lookup"><span data-stu-id="10b8f-223">Kafka on HDInsight version 3.6 (three worker nodes)</span></span>
    * <span data-ttu-id="10b8f-224">Storm on HDInsight version 3.6 (three worker nodes)</span><span class="sxs-lookup"><span data-stu-id="10b8f-224">Storm on HDInsight version 3.6 (three worker nodes)</span></span>

  > [!WARNING]
  > <span data-ttu-id="10b8f-225">To guarantee availability of Kafka on HDInsight, your cluster must contain at least three worker nodes.</span><span class="sxs-lookup"><span data-stu-id="10b8f-225">To guarantee availability of Kafka on HDInsight, your cluster must contain at least three worker nodes.</span></span> <span data-ttu-id="10b8f-226">This template creates a Kafka cluster that contains three worker nodes.</span><span class="sxs-lookup"><span data-stu-id="10b8f-226">This template creates a Kafka cluster that contains three worker nodes.</span></span>

2. <span data-ttu-id="10b8f-227">Use the following guidance to populate the entries on the **Custom deployment** section:</span><span class="sxs-lookup"><span data-stu-id="10b8f-227">Use the following guidance to populate the entries on the **Custom deployment** section:</span></span>

    2. <span data-ttu-id="10b8f-228">Use the following information to populate the entries on the **Customized template** section:</span><span class="sxs-lookup"><span data-stu-id="10b8f-228">Use the following information to populate the entries on the **Customized template** section:</span></span>

    | <span data-ttu-id="10b8f-229">Setting</span><span class="sxs-lookup"><span data-stu-id="10b8f-229">Setting</span></span> | <span data-ttu-id="10b8f-230">Value</span><span class="sxs-lookup"><span data-stu-id="10b8f-230">Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="10b8f-231">Subscription</span><span class="sxs-lookup"><span data-stu-id="10b8f-231">Subscription</span></span> | <span data-ttu-id="10b8f-232">Your Azure subscription</span><span class="sxs-lookup"><span data-stu-id="10b8f-232">Your Azure subscription</span></span> |
    | <span data-ttu-id="10b8f-233">Resource group</span><span class="sxs-lookup"><span data-stu-id="10b8f-233">Resource group</span></span> | <span data-ttu-id="10b8f-234">The resource group that contains the resources.</span><span class="sxs-lookup"><span data-stu-id="10b8f-234">The resource group that contains the resources.</span></span> |
    | <span data-ttu-id="10b8f-235">Location</span><span class="sxs-lookup"><span data-stu-id="10b8f-235">Location</span></span> | <span data-ttu-id="10b8f-236">The Azure region that the resources are created in.</span><span class="sxs-lookup"><span data-stu-id="10b8f-236">The Azure region that the resources are created in.</span></span> |
    | <span data-ttu-id="10b8f-237">Kafka Cluster Name</span><span class="sxs-lookup"><span data-stu-id="10b8f-237">Kafka Cluster Name</span></span> | <span data-ttu-id="10b8f-238">The name of the Kafka cluster.</span><span class="sxs-lookup"><span data-stu-id="10b8f-238">The name of the Kafka cluster.</span></span> |
    | <span data-ttu-id="10b8f-239">Storm Cluster Name</span><span class="sxs-lookup"><span data-stu-id="10b8f-239">Storm Cluster Name</span></span> | <span data-ttu-id="10b8f-240">The name of the Storm cluster.</span><span class="sxs-lookup"><span data-stu-id="10b8f-240">The name of the Storm cluster.</span></span> |
    | <span data-ttu-id="10b8f-241">Cluster Login User Name</span><span class="sxs-lookup"><span data-stu-id="10b8f-241">Cluster Login User Name</span></span> | <span data-ttu-id="10b8f-242">The admin user name for the clusters.</span><span class="sxs-lookup"><span data-stu-id="10b8f-242">The admin user name for the clusters.</span></span> |
    | <span data-ttu-id="10b8f-243">Cluster Login Password</span><span class="sxs-lookup"><span data-stu-id="10b8f-243">Cluster Login Password</span></span> | <span data-ttu-id="10b8f-244">The admin user password for the clusters.</span><span class="sxs-lookup"><span data-stu-id="10b8f-244">The admin user password for the clusters.</span></span> |
    | <span data-ttu-id="10b8f-245">SSH User Name</span><span class="sxs-lookup"><span data-stu-id="10b8f-245">SSH User Name</span></span> | <span data-ttu-id="10b8f-246">The SSH user to create for the clusters.</span><span class="sxs-lookup"><span data-stu-id="10b8f-246">The SSH user to create for the clusters.</span></span> |
    | <span data-ttu-id="10b8f-247">SSH Password</span><span class="sxs-lookup"><span data-stu-id="10b8f-247">SSH Password</span></span> | <span data-ttu-id="10b8f-248">The password for the SSH user.</span><span class="sxs-lookup"><span data-stu-id="10b8f-248">The password for the SSH user.</span></span> |
   
    ![Picture of the template parameters](./media/hdinsight-apache-storm-with-kafka/storm-kafka-template.png)

3. <span data-ttu-id="10b8f-250">Read the **Terms and Conditions**, and then select **I agree to the terms and conditions stated above**.</span><span class="sxs-lookup"><span data-stu-id="10b8f-250">Read the **Terms and Conditions**, and then select **I agree to the terms and conditions stated above**.</span></span>

4. <span data-ttu-id="10b8f-251">Finally, check **Pin to dashboard** and then select **Purchase**.</span><span class="sxs-lookup"><span data-stu-id="10b8f-251">Finally, check **Pin to dashboard** and then select **Purchase**.</span></span>

> [!NOTE]
> <span data-ttu-id="10b8f-252">It can take up to 20 minutes to create the clusters.</span><span class="sxs-lookup"><span data-stu-id="10b8f-252">It can take up to 20 minutes to create the clusters.</span></span>

## <a name="build-the-topology"></a><span data-ttu-id="10b8f-253">Build the topology</span><span class="sxs-lookup"><span data-stu-id="10b8f-253">Build the topology</span></span>

1. <span data-ttu-id="10b8f-254">On your development environment, download the project from [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka), open a command-line, and change directories to the location that you downloaded the project.</span><span class="sxs-lookup"><span data-stu-id="10b8f-254">On your development environment, download the project from [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka), open a command-line, and change directories to the location that you downloaded the project.</span></span>

2. <span data-ttu-id="10b8f-255">From the **hdinsight-storm-java-kafka** directory, use the following command to compile the project and create a package for deployment:</span><span class="sxs-lookup"><span data-stu-id="10b8f-255">From the **hdinsight-storm-java-kafka** directory, use the following command to compile the project and create a package for deployment:</span></span>

  ```bash
  mvn clean package
  ```

    <span data-ttu-id="10b8f-256">The package process creates a file named `KafkaTopology-1.0-SNAPSHOT.jar` in the `target` directory.</span><span class="sxs-lookup"><span data-stu-id="10b8f-256">The package process creates a file named `KafkaTopology-1.0-SNAPSHOT.jar` in the `target` directory.</span></span>

3. <span data-ttu-id="10b8f-257">Use the following commands to copy the package to your Storm on HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="10b8f-257">Use the following commands to copy the package to your Storm on HDInsight cluster.</span></span> <span data-ttu-id="10b8f-258">Replace `sshuser` with the SSH user name for the cluster.</span><span class="sxs-lookup"><span data-stu-id="10b8f-258">Replace `sshuser` with the SSH user name for the cluster.</span></span> <span data-ttu-id="10b8f-259">Replace `stormclustername` with the name of the __Storm__ cluster.</span><span class="sxs-lookup"><span data-stu-id="10b8f-259">Replace `stormclustername` with the name of the __Storm__ cluster.</span></span>

  ```bash
  scp ./target/KafkaTopology-1.0-SNAPSHOT.jar sshuser@stormclustername-ssh.azurehdinsight.net:KafkaTopology-1.0-SNAPSHOT.jar
  ```

    <span data-ttu-id="10b8f-260">When prompted, enter the password you used when creating the clusters.</span><span class="sxs-lookup"><span data-stu-id="10b8f-260">When prompted, enter the password you used when creating the clusters.</span></span>

## <a name="configure-the-topology"></a><span data-ttu-id="10b8f-261">Configure the topology</span><span class="sxs-lookup"><span data-stu-id="10b8f-261">Configure the topology</span></span>

1. <span data-ttu-id="10b8f-262">Use one of the following methods to discover the Kafka broker hosts for the **Kafka** on HDInsight cluster:</span><span class="sxs-lookup"><span data-stu-id="10b8f-262">Use one of the following methods to discover the Kafka broker hosts for the **Kafka** on HDInsight cluster:</span></span>

    ```powershell
    $creds = Get-Credential -UserName "admin" -Message "Enter the HDInsight login"
    $clusterName = Read-Host -Prompt "Enter the Kafka cluster name"
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/KAFKA/components/KAFKA_BROKER" `
        -Credential $creds `
        -UseBasicParsing
    $respObj = ConvertFrom-Json $resp.Content
    $brokerHosts = $respObj.host_components.HostRoles.host_name[0..1]
    ($brokerHosts -join ":9092,") + ":9092"
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="10b8f-263">The following Bash example assumes that `$CLUSTERNAME` contains the name of the __Kafka__ cluster name.</span><span class="sxs-lookup"><span data-stu-id="10b8f-263">The following Bash example assumes that `$CLUSTERNAME` contains the name of the __Kafka__ cluster name.</span></span> <span data-ttu-id="10b8f-264">It also assumes that [jq](https://stedolan.github.io/jq/) version 1.5 or greater is installed.</span><span class="sxs-lookup"><span data-stu-id="10b8f-264">It also assumes that [jq](https://stedolan.github.io/jq/) version 1.5 or greater is installed.</span></span> <span data-ttu-id="10b8f-265">When prompted, enter the password for the cluster login account.</span><span class="sxs-lookup"><span data-stu-id="10b8f-265">When prompted, enter the password for the cluster login account.</span></span>

    ```bash
    curl -su admin -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER" | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2
    ```

    <span data-ttu-id="10b8f-266">The value returned is similar to the following text:</span><span class="sxs-lookup"><span data-stu-id="10b8f-266">The value returned is similar to the following text:</span></span>

        wn0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092,wn1-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092

    > [!IMPORTANT]
    > <span data-ttu-id="10b8f-267">While there may be more than two broker hosts for your cluster, you do not need to provide a full list of all hosts to clients.</span><span class="sxs-lookup"><span data-stu-id="10b8f-267">While there may be more than two broker hosts for your cluster, you do not need to provide a full list of all hosts to clients.</span></span> <span data-ttu-id="10b8f-268">One or two is enough.</span><span class="sxs-lookup"><span data-stu-id="10b8f-268">One or two is enough.</span></span>

2. <span data-ttu-id="10b8f-269">Use one of the following methods to discover the Zookeeper hosts for the __Kafka__ on HDInsight cluster:</span><span class="sxs-lookup"><span data-stu-id="10b8f-269">Use one of the following methods to discover the Zookeeper hosts for the __Kafka__ on HDInsight cluster:</span></span>

    ```powershell
    $creds = Get-Credential -UserName "admin" -Message "Enter the HDInsight login"
    $clusterName = Read-Host -Prompt "Enter the Kafka cluster name"
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/ZOOKEEPER/components/ZOOKEEPER_SERVER" `
        -Credential $creds `
        -UseBasicParsing
    $respObj = ConvertFrom-Json $resp.Content
    $zookeeperHosts = $respObj.host_components.HostRoles.host_name[0..1]
    ($zookeeperHosts -join ":2181,") + ":2181"
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="10b8f-270">The following Bash example assumes that `$CLUSTERNAME` contains the name of the __Kafka__ cluster.</span><span class="sxs-lookup"><span data-stu-id="10b8f-270">The following Bash example assumes that `$CLUSTERNAME` contains the name of the __Kafka__ cluster.</span></span> <span data-ttu-id="10b8f-271">It also assumes that [jq](https://stedolan.github.io/jq/) is installed.</span><span class="sxs-lookup"><span data-stu-id="10b8f-271">It also assumes that [jq](https://stedolan.github.io/jq/) is installed.</span></span> <span data-ttu-id="10b8f-272">When prompted, enter the password for the cluster login account.</span><span class="sxs-lookup"><span data-stu-id="10b8f-272">When prompted, enter the password for the cluster login account.</span></span>

    ```bash
    curl -su admin -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER" | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2
    ```

    <span data-ttu-id="10b8f-273">The value returned is similar to the following text:</span><span class="sxs-lookup"><span data-stu-id="10b8f-273">The value returned is similar to the following text:</span></span>

        zk0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181,zk2-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181

    > [!IMPORTANT]
    > <span data-ttu-id="10b8f-274">While there are more than two Zookeeper nodes, you do not need to provide a full list of all hosts to clients.</span><span class="sxs-lookup"><span data-stu-id="10b8f-274">While there are more than two Zookeeper nodes, you do not need to provide a full list of all hosts to clients.</span></span> <span data-ttu-id="10b8f-275">One or two is enough.</span><span class="sxs-lookup"><span data-stu-id="10b8f-275">One or two is enough.</span></span>

    <span data-ttu-id="10b8f-276">Save this value, as it is used later.</span><span class="sxs-lookup"><span data-stu-id="10b8f-276">Save this value, as it is used later.</span></span>

3. <span data-ttu-id="10b8f-277">Edit the `dev.properties` file in the root of the project.</span><span class="sxs-lookup"><span data-stu-id="10b8f-277">Edit the `dev.properties` file in the root of the project.</span></span> <span data-ttu-id="10b8f-278">Add the Broker and Zookeeper hosts information for the __Kafka__ cluster to the matching lines in this file.</span><span class="sxs-lookup"><span data-stu-id="10b8f-278">Add the Broker and Zookeeper hosts information for the __Kafka__ cluster to the matching lines in this file.</span></span> <span data-ttu-id="10b8f-279">The following example is configured using the sample values from the previous steps:</span><span class="sxs-lookup"><span data-stu-id="10b8f-279">The following example is configured using the sample values from the previous steps:</span></span>

        kafka.zookeeper.hosts: zk0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181,zk2-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181
        kafka.broker.hosts: wn0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092,wn1-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092
        kafka.topic: stormtopic

    > [!IMPORTANT]
    > <span data-ttu-id="10b8f-280">The `hdfs.url` entry is configured for a cluster that uses an Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="10b8f-280">The `hdfs.url` entry is configured for a cluster that uses an Azure Storage account.</span></span> <span data-ttu-id="10b8f-281">To use this topology with a Storm cluster that uses Data Lake Store, change this value from `wasb` to `adl`.</span><span class="sxs-lookup"><span data-stu-id="10b8f-281">To use this topology with a Storm cluster that uses Data Lake Store, change this value from `wasb` to `adl`.</span></span>

4. <span data-ttu-id="10b8f-282">Save the `dev.properties` file and then use the following command to upload it to the **Storm** cluster:</span><span class="sxs-lookup"><span data-stu-id="10b8f-282">Save the `dev.properties` file and then use the following command to upload it to the **Storm** cluster:</span></span>

     ```bash
    scp dev.properties USERNAME@storm-BASENAME-ssh.azurehdinsight.net:dev.properties
    ```

    <span data-ttu-id="10b8f-283">Replace **USERNAME** with the SSH user name for the cluster.</span><span class="sxs-lookup"><span data-stu-id="10b8f-283">Replace **USERNAME** with the SSH user name for the cluster.</span></span> <span data-ttu-id="10b8f-284">Replace **BASENAME** with the base name you used when creating the cluster.</span><span class="sxs-lookup"><span data-stu-id="10b8f-284">Replace **BASENAME** with the base name you used when creating the cluster.</span></span>

## <a name="create-the-kafka-topic"></a><span data-ttu-id="10b8f-285">Create the Kafka topic</span><span class="sxs-lookup"><span data-stu-id="10b8f-285">Create the Kafka topic</span></span>

<span data-ttu-id="10b8f-286">Kafka stores data into a _topic_.</span><span class="sxs-lookup"><span data-stu-id="10b8f-286">Kafka stores data into a _topic_.</span></span> <span data-ttu-id="10b8f-287">You must create the topic before starting the Storm topologies.</span><span class="sxs-lookup"><span data-stu-id="10b8f-287">You must create the topic before starting the Storm topologies.</span></span> <span data-ttu-id="10b8f-288">To create the topology, use the following steps:</span><span class="sxs-lookup"><span data-stu-id="10b8f-288">To create the topology, use the following steps:</span></span>

1. <span data-ttu-id="10b8f-289">Connect to the __Kafka__ cluster through SSH by using the following command.</span><span class="sxs-lookup"><span data-stu-id="10b8f-289">Connect to the __Kafka__ cluster through SSH by using the following command.</span></span> <span data-ttu-id="10b8f-290">Replace `sshuser` with the SSH user name used when creating the cluster.</span><span class="sxs-lookup"><span data-stu-id="10b8f-290">Replace `sshuser` with the SSH user name used when creating the cluster.</span></span> <span data-ttu-id="10b8f-291">Replace `kafkaclustername` with the name of the Kafka cluster:</span><span class="sxs-lookup"><span data-stu-id="10b8f-291">Replace `kafkaclustername` with the name of the Kafka cluster:</span></span>

    ```bash
    ssh sshuser@kafkaclustername-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="10b8f-292">When prompted, enter the password you used when creating the clusters.</span><span class="sxs-lookup"><span data-stu-id="10b8f-292">When prompted, enter the password you used when creating the clusters.</span></span>
   
    <span data-ttu-id="10b8f-293">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="10b8f-293">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="10b8f-294">To create the Kafka topic, use the following command.</span><span class="sxs-lookup"><span data-stu-id="10b8f-294">To create the Kafka topic, use the following command.</span></span> <span data-ttu-id="10b8f-295">Replace `$KAFKAZKHOSTS` with the Zookeeper host information you used when configuring the topology:</span><span class="sxs-lookup"><span data-stu-id="10b8f-295">Replace `$KAFKAZKHOSTS` with the Zookeeper host information you used when configuring the topology:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic stormtopic --zookeeper $KAFKAZKHOSTS
    ```

    <span data-ttu-id="10b8f-296">This command connects to Zookeeper for the Kafka cluster and creates a new topic named `stormtopic`.</span><span class="sxs-lookup"><span data-stu-id="10b8f-296">This command connects to Zookeeper for the Kafka cluster and creates a new topic named `stormtopic`.</span></span> <span data-ttu-id="10b8f-297">This topic is used by the Storm topologies.</span><span class="sxs-lookup"><span data-stu-id="10b8f-297">This topic is used by the Storm topologies.</span></span>

## <a name="start-the-writer"></a><span data-ttu-id="10b8f-298">Start the writer</span><span class="sxs-lookup"><span data-stu-id="10b8f-298">Start the writer</span></span>

1. <span data-ttu-id="10b8f-299">Use the following to connect to the **Storm** cluster using SSH.</span><span class="sxs-lookup"><span data-stu-id="10b8f-299">Use the following to connect to the **Storm** cluster using SSH.</span></span> <span data-ttu-id="10b8f-300">Replace `sshuser` with the SSH user name used when creating the cluster.</span><span class="sxs-lookup"><span data-stu-id="10b8f-300">Replace `sshuser` with the SSH user name used when creating the cluster.</span></span> <span data-ttu-id="10b8f-301">Replace `stormclustername` with the name the Storm cluster:</span><span class="sxs-lookup"><span data-stu-id="10b8f-301">Replace `stormclustername` with the name the Storm cluster:</span></span>

    ```bash
    ssh sshuser@stormclustername-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="10b8f-302">When prompted, enter the password you used when creating the clusters.</span><span class="sxs-lookup"><span data-stu-id="10b8f-302">When prompted, enter the password you used when creating the clusters.</span></span>
   
    <span data-ttu-id="10b8f-303">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="10b8f-303">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="10b8f-304">From the SSH connection to the Storm cluster, use the following command to start the writer topology:</span><span class="sxs-lookup"><span data-stu-id="10b8f-304">From the SSH connection to the Storm cluster, use the following command to start the writer topology:</span></span>

    ```bash
    storm jar KafkaTopology-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writer.yaml --filter dev.properties
    ```

    <span data-ttu-id="10b8f-305">The parameters used with this command are:</span><span class="sxs-lookup"><span data-stu-id="10b8f-305">The parameters used with this command are:</span></span>

    * <span data-ttu-id="10b8f-306">`org.apache.storm.flux.Flux`: Use Flux to configure and run this topology.</span><span class="sxs-lookup"><span data-stu-id="10b8f-306">`org.apache.storm.flux.Flux`: Use Flux to configure and run this topology.</span></span>

    * <span data-ttu-id="10b8f-307">`--remote`: Submit the topology to Nimbus.</span><span class="sxs-lookup"><span data-stu-id="10b8f-307">`--remote`: Submit the topology to Nimbus.</span></span> <span data-ttu-id="10b8f-308">The topology is distributed across the worker nodes in the cluster.</span><span class="sxs-lookup"><span data-stu-id="10b8f-308">The topology is distributed across the worker nodes in the cluster.</span></span>

    * <span data-ttu-id="10b8f-309">`-R /writer.yaml`: Use the `writer.yaml` file to configure the topology.</span><span class="sxs-lookup"><span data-stu-id="10b8f-309">`-R /writer.yaml`: Use the `writer.yaml` file to configure the topology.</span></span> <span data-ttu-id="10b8f-310">`-R` indicates that this resource is included in the jar file.</span><span class="sxs-lookup"><span data-stu-id="10b8f-310">`-R` indicates that this resource is included in the jar file.</span></span> <span data-ttu-id="10b8f-311">It's in the root of the jar, so `/writer.yaml` is the path to it.</span><span class="sxs-lookup"><span data-stu-id="10b8f-311">It's in the root of the jar, so `/writer.yaml` is the path to it.</span></span>

    * <span data-ttu-id="10b8f-312">`--filter`: Populate entries in the `writer.yaml` topology using values in the `dev.properties` file.</span><span class="sxs-lookup"><span data-stu-id="10b8f-312">`--filter`: Populate entries in the `writer.yaml` topology using values in the `dev.properties` file.</span></span> <span data-ttu-id="10b8f-313">For example, the value of the `kafka.topic` entry in the file is used to replace the `${kafka.topic}` entry in the topology definition.</span><span class="sxs-lookup"><span data-stu-id="10b8f-313">For example, the value of the `kafka.topic` entry in the file is used to replace the `${kafka.topic}` entry in the topology definition.</span></span>

## <a name="start-the-reader"></a><span data-ttu-id="10b8f-314">Start the reader</span><span class="sxs-lookup"><span data-stu-id="10b8f-314">Start the reader</span></span>

1. <span data-ttu-id="10b8f-315">From the SSH session to the Storm cluster, use the following command to start the reader topology:</span><span class="sxs-lookup"><span data-stu-id="10b8f-315">From the SSH session to the Storm cluster, use the following command to start the reader topology:</span></span>

  ```bash
  storm jar KafkaTopology-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /reader.yaml --filter dev.properties
  ```

2. <span data-ttu-id="10b8f-316">Wait a minute and then use the following command to view the files created by the reader topology:</span><span class="sxs-lookup"><span data-stu-id="10b8f-316">Wait a minute and then use the following command to view the files created by the reader topology:</span></span>

    ```bash
    hdfs dfs -ls /stormdata
    ```

    <span data-ttu-id="10b8f-317">The output is similar to the following text:</span><span class="sxs-lookup"><span data-stu-id="10b8f-317">The output is similar to the following text:</span></span>

        Found 173 items
        -rw-r--r--   1 storm supergroup       5137 2018-04-09 19:00 /stormdata/hdfs-bolt-4-0-1523300453088.txt
        -rw-r--r--   1 storm supergroup       5128 2018-04-09 19:00 /stormdata/hdfs-bolt-4-1-1523300453624.txt
        -rw-r--r--   1 storm supergroup       5131 2018-04-09 19:00 /stormdata/hdfs-bolt-4-10-1523300455170.txt
        ...

3. <span data-ttu-id="10b8f-318">To view the contents of the file, use the following command.</span><span class="sxs-lookup"><span data-stu-id="10b8f-318">To view the contents of the file, use the following command.</span></span> <span data-ttu-id="10b8f-319">Replace `filename.txt` with the name of a file:</span><span class="sxs-lookup"><span data-stu-id="10b8f-319">Replace `filename.txt` with the name of a file:</span></span>

    ```bash
    hdfs dfs -cat /stormdata/filename.txt
    ```

    <span data-ttu-id="10b8f-320">The following text is an example of the file contents:</span><span class="sxs-lookup"><span data-stu-id="10b8f-320">The following text is an example of the file contents:</span></span>

        four score and seven years ago
        snow white and the seven dwarfs
        i am at two with nature
        snow white and the seven dwarfs
        i am at two with nature
        four score and seven years ago
        an apple a day keeps the doctor away

## <a name="stop-the-topologies"></a><span data-ttu-id="10b8f-321">Stop the topologies</span><span class="sxs-lookup"><span data-stu-id="10b8f-321">Stop the topologies</span></span>

<span data-ttu-id="10b8f-322">From an SSH session to the Storm cluster, use the following commands to stop the Storm topologies:</span><span class="sxs-lookup"><span data-stu-id="10b8f-322">From an SSH session to the Storm cluster, use the following commands to stop the Storm topologies:</span></span>

  ```bash
  storm kill kafka-writer
  storm kill kafka-reader
  ```

## <a name="clean-up-resources"></a><span data-ttu-id="10b8f-323">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="10b8f-323">Clean up resources</span></span>

<span data-ttu-id="10b8f-324">To clean up the resources created by this tutorial, you can delete the resource group.</span><span class="sxs-lookup"><span data-stu-id="10b8f-324">To clean up the resources created by this tutorial, you can delete the resource group.</span></span> <span data-ttu-id="10b8f-325">Deleting the resource group also deletes the associated HDInsight cluster, and any other resources associated with the resource group.</span><span class="sxs-lookup"><span data-stu-id="10b8f-325">Deleting the resource group also deletes the associated HDInsight cluster, and any other resources associated with the resource group.</span></span>

<span data-ttu-id="10b8f-326">To remove the resource group using the Azure portal:</span><span class="sxs-lookup"><span data-stu-id="10b8f-326">To remove the resource group using the Azure portal:</span></span>

1. <span data-ttu-id="10b8f-327">In the Azure portal, expand the menu on the left side to open the menu of services, and then choose __Resource Groups__ to display the list of your resource groups.</span><span class="sxs-lookup"><span data-stu-id="10b8f-327">In the Azure portal, expand the menu on the left side to open the menu of services, and then choose __Resource Groups__ to display the list of your resource groups.</span></span>
2. <span data-ttu-id="10b8f-328">Locate the resource group to delete, and then right-click the __More__ button (...) on the right side of the listing.</span><span class="sxs-lookup"><span data-stu-id="10b8f-328">Locate the resource group to delete, and then right-click the __More__ button (...) on the right side of the listing.</span></span>
3. <span data-ttu-id="10b8f-329">Select __Delete resource group__, and then confirm.</span><span class="sxs-lookup"><span data-stu-id="10b8f-329">Select __Delete resource group__, and then confirm.</span></span>

> [!WARNING]
> <span data-ttu-id="10b8f-330">HDInsight cluster billing starts once a cluster is created and stops when the cluster is deleted.</span><span class="sxs-lookup"><span data-stu-id="10b8f-330">HDInsight cluster billing starts once a cluster is created and stops when the cluster is deleted.</span></span> <span data-ttu-id="10b8f-331">Billing is pro-rated per minute, so you should always delete your cluster when it is no longer in use.</span><span class="sxs-lookup"><span data-stu-id="10b8f-331">Billing is pro-rated per minute, so you should always delete your cluster when it is no longer in use.</span></span>
> 
> <span data-ttu-id="10b8f-332">Deleting a Kafka on HDInsight cluster deletes any data stored in Kafka.</span><span class="sxs-lookup"><span data-stu-id="10b8f-332">Deleting a Kafka on HDInsight cluster deletes any data stored in Kafka.</span></span>

## <a name="next-steps"></a><span data-ttu-id="10b8f-333">Next steps</span><span class="sxs-lookup"><span data-stu-id="10b8f-333">Next steps</span></span>

<span data-ttu-id="10b8f-334">In this tutorial, you learned how to use a Storm topology to write to and read from Kafka on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="10b8f-334">In this tutorial, you learned how to use a Storm topology to write to and read from Kafka on HDInsight.</span></span> <span data-ttu-id="10b8f-335">You also learned how to store data to the HDFS compatible storage used by HDInsight.</span><span class="sxs-lookup"><span data-stu-id="10b8f-335">You also learned how to store data to the HDFS compatible storage used by HDInsight.</span></span>

<span data-ttu-id="10b8f-336">To learn more about using Kafka on HDInsight, see the [Use Kafka Producer and Consumer API](kafka/apache-kafka-producer-consumer-api.md) document.</span><span class="sxs-lookup"><span data-stu-id="10b8f-336">To learn more about using Kafka on HDInsight, see the [Use Kafka Producer and Consumer API](kafka/apache-kafka-producer-consumer-api.md) document.</span></span>

<span data-ttu-id="10b8f-337">For information on deploying and monitoring topologies on Linux-based HDInsight, see [Deploy and manage Apache Storm topologies on Linux-based HDInsight](storm/apache-storm-deploy-monitor-topology-linux.md)</span><span class="sxs-lookup"><span data-stu-id="10b8f-337">For information on deploying and monitoring topologies on Linux-based HDInsight, see [Deploy and manage Apache Storm topologies on Linux-based HDInsight](storm/apache-storm-deploy-monitor-topology-linux.md)</span></span>
