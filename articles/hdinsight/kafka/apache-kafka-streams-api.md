---
title: 'Tutorial: Use the Apache Kafka Streams API - Azure HDInsight '
description: Learn how to use the Apache Kafka Streams API with Kafka on HDInsight. This API enables you to perform stream processing between topics in Kafka.
services: hdinsight
ms.service: hdinsight
author: jasonwhowell
ms.author: jasonh
ms.reviewer: jasonh
ms.custom: hdinsightactive
ms.topic: tutorial
ms.date: 04/17/2018
ms.openlocfilehash: 0c1b45d7db53bd2eb7c9f058eb1c44c762886b80
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868032"
---
# <a name="tutorial-apache-kafka-streams-api"></a><span data-ttu-id="6a5ea-104">Tutorial: Apache Kafka streams API</span><span class="sxs-lookup"><span data-stu-id="6a5ea-104">Tutorial: Apache Kafka streams API</span></span>

<span data-ttu-id="6a5ea-105">Learn how to create an application that uses the Kafka Streams API and run it with Kafka on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6a5ea-105">Learn how to create an application that uses the Kafka Streams API and run it with Kafka on HDInsight.</span></span> 

<span data-ttu-id="6a5ea-106">The application used in this tutorial is a streaming word count.</span><span class="sxs-lookup"><span data-stu-id="6a5ea-106">The application used in this tutorial is a streaming word count.</span></span> <span data-ttu-id="6a5ea-107">It reads text data from a Kafka topic, extracts individual words, and then stores the word and count into another Kafka topic.</span><span class="sxs-lookup"><span data-stu-id="6a5ea-107">It reads text data from a Kafka topic, extracts individual words, and then stores the word and count into another Kafka topic.</span></span>

> [!NOTE]
> <span data-ttu-id="6a5ea-108">Kafka stream processing is often done using Apache Spark or Storm.</span><span class="sxs-lookup"><span data-stu-id="6a5ea-108">Kafka stream processing is often done using Apache Spark or Storm.</span></span> <span data-ttu-id="6a5ea-109">Kafka version 0.10.0 (in HDInsight 3.5 and 3.6) introduced the Kafka Streams API.</span><span class="sxs-lookup"><span data-stu-id="6a5ea-109">Kafka version 0.10.0 (in HDInsight 3.5 and 3.6) introduced the Kafka Streams API.</span></span> <span data-ttu-id="6a5ea-110">This API allows you to transform data streams between input and output topics.</span><span class="sxs-lookup"><span data-stu-id="6a5ea-110">This API allows you to transform data streams between input and output topics.</span></span> <span data-ttu-id="6a5ea-111">In some cases, this may be an alternative to creating a Spark or Storm streaming solution.</span><span class="sxs-lookup"><span data-stu-id="6a5ea-111">In some cases, this may be an alternative to creating a Spark or Storm streaming solution.</span></span> 
>
> <span data-ttu-id="6a5ea-112">For more information on Kafka Streams, see the [Intro to Streams](https://kafka.apache.org/10/documentation/streams/) documentation on Apache.org.</span><span class="sxs-lookup"><span data-stu-id="6a5ea-112">For more information on Kafka Streams, see the [Intro to Streams](https://kafka.apache.org/10/documentation/streams/) documentation on Apache.org.</span></span>

<span data-ttu-id="6a5ea-113">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="6a5ea-113">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6a5ea-114">Set up your development environment</span><span class="sxs-lookup"><span data-stu-id="6a5ea-114">Set up your development environment</span></span>
> * <span data-ttu-id="6a5ea-115">Understand the code</span><span class="sxs-lookup"><span data-stu-id="6a5ea-115">Understand the code</span></span>
> * <span data-ttu-id="6a5ea-116">Build and deploy the application</span><span class="sxs-lookup"><span data-stu-id="6a5ea-116">Build and deploy the application</span></span>
> * <span data-ttu-id="6a5ea-117">Configure Kafka topics</span><span class="sxs-lookup"><span data-stu-id="6a5ea-117">Configure Kafka topics</span></span>
> * <span data-ttu-id="6a5ea-118">Run the code</span><span class="sxs-lookup"><span data-stu-id="6a5ea-118">Run the code</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6a5ea-119">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="6a5ea-119">Prerequisites</span></span>

* <span data-ttu-id="6a5ea-120">A Kafka on HDInsight 3.6 cluster.</span><span class="sxs-lookup"><span data-stu-id="6a5ea-120">A Kafka on HDInsight 3.6 cluster.</span></span> <span data-ttu-id="6a5ea-121">To learn how to create a Kafka on HDInsight cluster, see the [Start with Kafka on HDInsight](apache-kafka-get-started.md) document.</span><span class="sxs-lookup"><span data-stu-id="6a5ea-121">To learn how to create a Kafka on HDInsight cluster, see the [Start with Kafka on HDInsight](apache-kafka-get-started.md) document.</span></span>

* <span data-ttu-id="6a5ea-122">Complete the steps in the [Kafka Consumer and Producer API](apache-kafka-producer-consumer-api.md) document.</span><span class="sxs-lookup"><span data-stu-id="6a5ea-122">Complete the steps in the [Kafka Consumer and Producer API](apache-kafka-producer-consumer-api.md) document.</span></span> <span data-ttu-id="6a5ea-123">The steps in this document use the example application and topics created in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="6a5ea-123">The steps in this document use the example application and topics created in this tutorial.</span></span>

## <a name="set-up-your-development-environment"></a><span data-ttu-id="6a5ea-124">Set up your development environment</span><span class="sxs-lookup"><span data-stu-id="6a5ea-124">Set up your development environment</span></span>

<span data-ttu-id="6a5ea-125">You must have the following components installed in your development environment:</span><span class="sxs-lookup"><span data-stu-id="6a5ea-125">You must have the following components installed in your development environment:</span></span>

* <span data-ttu-id="6a5ea-126">[Java JDK 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) or an equivalent, such as OpenJDK.</span><span class="sxs-lookup"><span data-stu-id="6a5ea-126">[Java JDK 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) or an equivalent, such as OpenJDK.</span></span>

* [<span data-ttu-id="6a5ea-127">Apache Maven</span><span class="sxs-lookup"><span data-stu-id="6a5ea-127">Apache Maven</span></span>](http://maven.apache.org/)

* <span data-ttu-id="6a5ea-128">An SSH client and the `scp` command.</span><span class="sxs-lookup"><span data-stu-id="6a5ea-128">An SSH client and the `scp` command.</span></span> <span data-ttu-id="6a5ea-129">For more information, see the [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md) document.</span><span class="sxs-lookup"><span data-stu-id="6a5ea-129">For more information, see the [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

## <a name="understand-the-code"></a><span data-ttu-id="6a5ea-130">Understand the code</span><span class="sxs-lookup"><span data-stu-id="6a5ea-130">Understand the code</span></span>

<span data-ttu-id="6a5ea-131">The example application is located at [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started), in the `Streaming` subdirectory.</span><span class="sxs-lookup"><span data-stu-id="6a5ea-131">The example application is located at [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started), in the `Streaming` subdirectory.</span></span> <span data-ttu-id="6a5ea-132">The application consists of two files:</span><span class="sxs-lookup"><span data-stu-id="6a5ea-132">The application consists of two files:</span></span>

* <span data-ttu-id="6a5ea-133">`pom.xml`: This file defines the project dependencies, Java version, and packaging methods.</span><span class="sxs-lookup"><span data-stu-id="6a5ea-133">`pom.xml`: This file defines the project dependencies, Java version, and packaging methods.</span></span>
* <span data-ttu-id="6a5ea-134">`Stream.java`: This file implements the streaming logic.</span><span class="sxs-lookup"><span data-stu-id="6a5ea-134">`Stream.java`: This file implements the streaming logic.</span></span>

### <a name="pomxml"></a><span data-ttu-id="6a5ea-135">Pom.xml</span><span class="sxs-lookup"><span data-stu-id="6a5ea-135">Pom.xml</span></span>

<span data-ttu-id="6a5ea-136">The important things to understand in the `pom.xml` file are:</span><span class="sxs-lookup"><span data-stu-id="6a5ea-136">The important things to understand in the `pom.xml` file are:</span></span>

* <span data-ttu-id="6a5ea-137">Dependencies: This project relies on the Kafka Streams API, which is provided by the `kafka-clients` package.</span><span class="sxs-lookup"><span data-stu-id="6a5ea-137">Dependencies: This project relies on the Kafka Streams API, which is provided by the `kafka-clients` package.</span></span> <span data-ttu-id="6a5ea-138">The following XML code defines this dependency:</span><span class="sxs-lookup"><span data-stu-id="6a5ea-138">The following XML code defines this dependency:</span></span>

    ```xml
    <!-- Kafka client for producer/consumer operations -->
    <dependency>
      <groupId>org.apache.kafka</groupId>
      <artifactId>kafka-clients</artifactId>
      <version>${kafka.version}</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="6a5ea-139">The `${kafka.version}` entry is declared in the `<properties>..</properties>` section of `pom.xml`, and is configured to the Kafka version of the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="6a5ea-139">The `${kafka.version}` entry is declared in the `<properties>..</properties>` section of `pom.xml`, and is configured to the Kafka version of the HDInsight cluster.</span></span>

* <span data-ttu-id="6a5ea-140">Plugins: Maven plugins provide various capabilities.</span><span class="sxs-lookup"><span data-stu-id="6a5ea-140">Plugins: Maven plugins provide various capabilities.</span></span> <span data-ttu-id="6a5ea-141">In this project, the following plugins are used:</span><span class="sxs-lookup"><span data-stu-id="6a5ea-141">In this project, the following plugins are used:</span></span>

    * <span data-ttu-id="6a5ea-142">`maven-compiler-plugin`: Used to set the Java version used by the project to 8.</span><span class="sxs-lookup"><span data-stu-id="6a5ea-142">`maven-compiler-plugin`: Used to set the Java version used by the project to 8.</span></span> <span data-ttu-id="6a5ea-143">Java 8 is required by HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="6a5ea-143">Java 8 is required by HDInsight 3.6.</span></span>
    * <span data-ttu-id="6a5ea-144">`maven-shade-plugin`: Used to generate an uber jar that contains this application as well as any dependencies.</span><span class="sxs-lookup"><span data-stu-id="6a5ea-144">`maven-shade-plugin`: Used to generate an uber jar that contains this application as well as any dependencies.</span></span> <span data-ttu-id="6a5ea-145">It is also used to set the entry point of the application, so that you can directly run the Jar file without having to specify the main class.</span><span class="sxs-lookup"><span data-stu-id="6a5ea-145">It is also used to set the entry point of the application, so that you can directly run the Jar file without having to specify the main class.</span></span>

### <a name="streamjava"></a><span data-ttu-id="6a5ea-146">Stream.java</span><span class="sxs-lookup"><span data-stu-id="6a5ea-146">Stream.java</span></span>

<span data-ttu-id="6a5ea-147">The `Stream.java` file uses the Streams API to implement a word count application.</span><span class="sxs-lookup"><span data-stu-id="6a5ea-147">The `Stream.java` file uses the Streams API to implement a word count application.</span></span> <span data-ttu-id="6a5ea-148">It reads data from a Kafka topic named `test` and writes the word counts into a topic named `wordcounts`.</span><span class="sxs-lookup"><span data-stu-id="6a5ea-148">It reads data from a Kafka topic named `test` and writes the word counts into a topic named `wordcounts`.</span></span>

<span data-ttu-id="6a5ea-149">The following code defines the word count application:</span><span class="sxs-lookup"><span data-stu-id="6a5ea-149">The following code defines the word count application:</span></span>

```java
package com.microsoft.example;

import org.apache.kafka.common.serialization.Serde;
import org.apache.kafka.common.serialization.Serdes;
import org.apache.kafka.streams.KafkaStreams;
import org.apache.kafka.streams.KeyValue;
import org.apache.kafka.streams.StreamsConfig;
import org.apache.kafka.streams.kstream.KStream;
import org.apache.kafka.streams.kstream.KStreamBuilder;

import java.util.Arrays;
import java.util.Properties;

public class Stream
{
    public static void main( String[] args ) {
        Properties streamsConfig = new Properties();
        // The name must be unique on the Kafka cluster
        streamsConfig.put(StreamsConfig.APPLICATION_ID_CONFIG, "wordcount-example");
        // Brokers
        streamsConfig.put(StreamsConfig.BOOTSTRAP_SERVERS_CONFIG, args[0]);
        // SerDes for key and values
        streamsConfig.put(StreamsConfig.KEY_SERDE_CLASS_CONFIG, Serdes.String().getClass().getName());
        streamsConfig.put(StreamsConfig.VALUE_SERDE_CLASS_CONFIG, Serdes.String().getClass().getName());

        // Serdes for the word and count
        Serde<String> stringSerde = Serdes.String();
        Serde<Long> longSerde = Serdes.Long();

        KStreamBuilder builder = new KStreamBuilder();
        KStream<String, String> sentences = builder.stream(stringSerde, stringSerde, "test");
        KStream<String, Long> wordCounts = sentences
                .flatMapValues(value -> Arrays.asList(value.toLowerCase().split("\\W+")))
                .map((key, word) -> new KeyValue<>(word, word))
                .countByKey("Counts")
                .toStream();
        wordCounts.to(stringSerde, longSerde, "wordcounts");

        KafkaStreams streams = new KafkaStreams(builder, streamsConfig);
        streams.start();

        Runtime.getRuntime().addShutdownHook(new Thread(streams::close));
    }
}
```


## <a name="build-and-deploy-the-example"></a><span data-ttu-id="6a5ea-150">Build and deploy the example</span><span class="sxs-lookup"><span data-stu-id="6a5ea-150">Build and deploy the example</span></span>

<span data-ttu-id="6a5ea-151">To build and deploy the project to your Kafka on HDInsight cluster, use the following steps:</span><span class="sxs-lookup"><span data-stu-id="6a5ea-151">To build and deploy the project to your Kafka on HDInsight cluster, use the following steps:</span></span>

1. <span data-ttu-id="6a5ea-152">Download the examples from [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started).</span><span class="sxs-lookup"><span data-stu-id="6a5ea-152">Download the examples from [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started).</span></span>

2. <span data-ttu-id="6a5ea-153">Change directories to the `Streaming` directory, and then use the following command to create a jar package:</span><span class="sxs-lookup"><span data-stu-id="6a5ea-153">Change directories to the `Streaming` directory, and then use the following command to create a jar package:</span></span>

    ```bash
    mvn clean package
    ```

    <span data-ttu-id="6a5ea-154">This command creates the package at `target/kafka-streaming-1.0-SNAPSHOT.jar`.</span><span class="sxs-lookup"><span data-stu-id="6a5ea-154">This command creates the package at `target/kafka-streaming-1.0-SNAPSHOT.jar`.</span></span>

3. <span data-ttu-id="6a5ea-155">Use the following command to copy the `kafka-streaming-1.0-SNAPSHOT.jar` file to your HDInsight cluster:</span><span class="sxs-lookup"><span data-stu-id="6a5ea-155">Use the following command to copy the `kafka-streaming-1.0-SNAPSHOT.jar` file to your HDInsight cluster:</span></span>
   
    ```bash
    scp ./target/kafka-streaming-1.0-SNAPSHOT.jar sshuser@clustername-ssh.azurehdinsight.net:kafka-streaming.jar
    ```
   
    <span data-ttu-id="6a5ea-156">Replace `sshuser` with the SSH user for your cluster, and replace `clustername` with the name of your cluster.</span><span class="sxs-lookup"><span data-stu-id="6a5ea-156">Replace `sshuser` with the SSH user for your cluster, and replace `clustername` with the name of your cluster.</span></span> <span data-ttu-id="6a5ea-157">If prompted, enter the password for the SSH user account.</span><span class="sxs-lookup"><span data-stu-id="6a5ea-157">If prompted, enter the password for the SSH user account.</span></span> <span data-ttu-id="6a5ea-158">For more information on using `scp` with HDInsight, see [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="6a5ea-158">For more information on using `scp` with HDInsight, see [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <a name="create-kafka-topics"></a><span data-ttu-id="6a5ea-159">Create Kafka topics</span><span class="sxs-lookup"><span data-stu-id="6a5ea-159">Create Kafka topics</span></span>

1. <span data-ttu-id="6a5ea-160">To open an SSH connection to the cluster, use the following command:</span><span class="sxs-lookup"><span data-stu-id="6a5ea-160">To open an SSH connection to the cluster, use the following command:</span></span>

    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="6a5ea-161">Replace `sshuser` with the SSH user for your cluster, and replace `clustername` with the name of your cluster.</span><span class="sxs-lookup"><span data-stu-id="6a5ea-161">Replace `sshuser` with the SSH user for your cluster, and replace `clustername` with the name of your cluster.</span></span> <span data-ttu-id="6a5ea-162">If prompted, enter the password for the SSH user account.</span><span class="sxs-lookup"><span data-stu-id="6a5ea-162">If prompted, enter the password for the SSH user account.</span></span> <span data-ttu-id="6a5ea-163">For more information on using `scp` with HDInsight, see [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="6a5ea-163">For more information on using `scp` with HDInsight, see [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="6a5ea-164">To save the cluster name to a variable and install a JSON parsing utility (`jq`), use the following commands.</span><span class="sxs-lookup"><span data-stu-id="6a5ea-164">To save the cluster name to a variable and install a JSON parsing utility (`jq`), use the following commands.</span></span> <span data-ttu-id="6a5ea-165">When prompted, enter the Kafka cluster name:</span><span class="sxs-lookup"><span data-stu-id="6a5ea-165">When prompted, enter the Kafka cluster name:</span></span>

    ```bash
    sudo apt -y install jq
    read -p 'Enter your Kafka cluster name:' CLUSTERNAME
    ```

3. <span data-ttu-id="6a5ea-166">To get the Kafka broker hosts and the Zookeeper hosts, use the following commands.</span><span class="sxs-lookup"><span data-stu-id="6a5ea-166">To get the Kafka broker hosts and the Zookeeper hosts, use the following commands.</span></span> <span data-ttu-id="6a5ea-167">When prompted, enter the password for the cluster login (admin) account.</span><span class="sxs-lookup"><span data-stu-id="6a5ea-167">When prompted, enter the password for the cluster login (admin) account.</span></span> <span data-ttu-id="6a5ea-168">You are prompted for the password twice.</span><span class="sxs-lookup"><span data-stu-id="6a5ea-168">You are prompted for the password twice.</span></span>

    ```bash
    export KAFKAZKHOSTS=`curl -sS -u admin -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`; \
    export KAFKABROKERS=`curl -sS -u admin -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`; \
    ```

4. <span data-ttu-id="6a5ea-169">To create the topics used by the streaming operation, use the following commands:</span><span class="sxs-lookup"><span data-stu-id="6a5ea-169">To create the topics used by the streaming operation, use the following commands:</span></span>

    > [!NOTE]
    > <span data-ttu-id="6a5ea-170">You may receive an error that the `test` topic already exists.</span><span class="sxs-lookup"><span data-stu-id="6a5ea-170">You may receive an error that the `test` topic already exists.</span></span> <span data-ttu-id="6a5ea-171">This is OK, as it may have been created in the Producer and Consumer API tutorial.</span><span class="sxs-lookup"><span data-stu-id="6a5ea-171">This is OK, as it may have been created in the Producer and Consumer API tutorial.</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic test --zookeeper $KAFKAZKHOSTS

    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic wordcounts --zookeeper $KAFKAZKHOSTS

    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic RekeyedIntermediateTopic --zookeeper $KAFKAZKHOSTS

    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic wordcount-example-Counts-changelog --zookeeper $KAFKAZKHOSTS
    ```

    <span data-ttu-id="6a5ea-172">The topics are used for the following purposes:</span><span class="sxs-lookup"><span data-stu-id="6a5ea-172">The topics are used for the following purposes:</span></span>

    * <span data-ttu-id="6a5ea-173">`test`: This topic is where records are received.</span><span class="sxs-lookup"><span data-stu-id="6a5ea-173">`test`: This topic is where records are received.</span></span> <span data-ttu-id="6a5ea-174">The streaming application reads from here.</span><span class="sxs-lookup"><span data-stu-id="6a5ea-174">The streaming application reads from here.</span></span>
    * <span data-ttu-id="6a5ea-175">`wordcounts`: This topic is where the streaming application stores its output.</span><span class="sxs-lookup"><span data-stu-id="6a5ea-175">`wordcounts`: This topic is where the streaming application stores its output.</span></span>
    * <span data-ttu-id="6a5ea-176">`RekeyedIntermediateTopic`: This topic is used to repartition data as the count is updated by the `countByKey` operator.</span><span class="sxs-lookup"><span data-stu-id="6a5ea-176">`RekeyedIntermediateTopic`: This topic is used to repartition data as the count is updated by the `countByKey` operator.</span></span>
    * <span data-ttu-id="6a5ea-177">`wordcount-example-Counts-changelog`: This topic is a state store used by the `countByKey` operation</span><span class="sxs-lookup"><span data-stu-id="6a5ea-177">`wordcount-example-Counts-changelog`: This topic is a state store used by the `countByKey` operation</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="6a5ea-178">Kafka on HDInsight can also be configured to automatically create topics.</span><span class="sxs-lookup"><span data-stu-id="6a5ea-178">Kafka on HDInsight can also be configured to automatically create topics.</span></span> <span data-ttu-id="6a5ea-179">For more information, see the [Configure automatic topic creation](apache-kafka-auto-create-topics.md) document.</span><span class="sxs-lookup"><span data-stu-id="6a5ea-179">For more information, see the [Configure automatic topic creation](apache-kafka-auto-create-topics.md) document.</span></span>

## <a name="run-the-code"></a><span data-ttu-id="6a5ea-180">Run the code</span><span class="sxs-lookup"><span data-stu-id="6a5ea-180">Run the code</span></span>

1. <span data-ttu-id="6a5ea-181">To start the streaming application as a background process, use the following command:</span><span class="sxs-lookup"><span data-stu-id="6a5ea-181">To start the streaming application as a background process, use the following command:</span></span>

    ```bash
    java -jar kafka-streaming.jar $KAFKABROKERS $KAFKAZKHOSTS &
    ```

    > [!NOTE]
    > <span data-ttu-id="6a5ea-182">You may get a warning about log4j.</span><span class="sxs-lookup"><span data-stu-id="6a5ea-182">You may get a warning about log4j.</span></span> <span data-ttu-id="6a5ea-183">You can ignore this.</span><span class="sxs-lookup"><span data-stu-id="6a5ea-183">You can ignore this.</span></span>

2. <span data-ttu-id="6a5ea-184">To send records to the `test` topic, use the following command to start the producer application:</span><span class="sxs-lookup"><span data-stu-id="6a5ea-184">To send records to the `test` topic, use the following command to start the producer application:</span></span>

    ```bash
    java -jar kafka-producer-consumer.jar producer test $KAFKABROKERS
    ```

3. <span data-ttu-id="6a5ea-185">Once the producer completes, use the following command to view the information stored in the `wordcounts` topic:</span><span class="sxs-lookup"><span data-stu-id="6a5ea-185">Once the producer completes, use the following command to view the information stored in the `wordcounts` topic:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --bootstrap-server $KAFKABROKERS --topic wordcounts --formatter kafka.tools.DefaultMessageFormatter --property print.key=true --property key.deserializer=org.apache.kafka.common.serialization.StringDeserializer --property value.deserializer=org.apache.kafka.common.serialization.LongDeserializer --from-beginning
    ```

    > [!NOTE]
    > <span data-ttu-id="6a5ea-186">The `--property` parameters tell the console consumer to print the key (word) along with the count (value).</span><span class="sxs-lookup"><span data-stu-id="6a5ea-186">The `--property` parameters tell the console consumer to print the key (word) along with the count (value).</span></span> <span data-ttu-id="6a5ea-187">This parameter also configures the deserializer to use when reading these values from Kafka.</span><span class="sxs-lookup"><span data-stu-id="6a5ea-187">This parameter also configures the deserializer to use when reading these values from Kafka.</span></span>

    <span data-ttu-id="6a5ea-188">The output is similar to the following text:</span><span class="sxs-lookup"><span data-stu-id="6a5ea-188">The output is similar to the following text:</span></span>
   
        dwarfs  13635
        ago     13664
        snow    13636
        dwarfs  13636
        ago     13665
        a       13803
        ago     13666
        a       13804
        ago     13667
        ago     13668
        jumped  13640
        jumped  13641
   
    > [!NOTE]
    > <span data-ttu-id="6a5ea-189">The parameter `--from-beginning` configures the consumer to start at the beginning of the records stored in the topic.</span><span class="sxs-lookup"><span data-stu-id="6a5ea-189">The parameter `--from-beginning` configures the consumer to start at the beginning of the records stored in the topic.</span></span> <span data-ttu-id="6a5ea-190">The count increments each time a word is encountered, so the topic contains multiple entries for each word, with an increasing count.</span><span class="sxs-lookup"><span data-stu-id="6a5ea-190">The count increments each time a word is encountered, so the topic contains multiple entries for each word, with an increasing count.</span></span>

7. <span data-ttu-id="6a5ea-191">Use the __Ctrl + C__ to exit the producer.</span><span class="sxs-lookup"><span data-stu-id="6a5ea-191">Use the __Ctrl + C__ to exit the producer.</span></span> <span data-ttu-id="6a5ea-192">Continue using __Ctrl + C__ to exit the application and the consumer.</span><span class="sxs-lookup"><span data-stu-id="6a5ea-192">Continue using __Ctrl + C__ to exit the application and the consumer.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6a5ea-193">Next steps</span><span class="sxs-lookup"><span data-stu-id="6a5ea-193">Next steps</span></span>

<span data-ttu-id="6a5ea-194">In this document, you learned how to use the Kafka Streams API with Kafka on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6a5ea-194">In this document, you learned how to use the Kafka Streams API with Kafka on HDInsight.</span></span> <span data-ttu-id="6a5ea-195">Use the following to learn more about working with Kafka:</span><span class="sxs-lookup"><span data-stu-id="6a5ea-195">Use the following to learn more about working with Kafka:</span></span>

* [<span data-ttu-id="6a5ea-196">Analyze Kafka logs</span><span class="sxs-lookup"><span data-stu-id="6a5ea-196">Analyze Kafka logs</span></span>](apache-kafka-log-analytics-operations-management.md)
* [<span data-ttu-id="6a5ea-197">Replicate data between Kafka clusters</span><span class="sxs-lookup"><span data-stu-id="6a5ea-197">Replicate data between Kafka clusters</span></span>](apache-kafka-mirroring.md)
