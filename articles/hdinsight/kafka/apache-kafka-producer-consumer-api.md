---
title: 'Tutorial: Use the Apache Kafka Producer and Consumer APIs - Azure HDInsight '
description: Learn how to use the Apache Kafka Producer and Consumer APIs with Kafka on HDInsight. In this tutorial, you learn how to use these APIs with Kafka on HDInsight from a Java application.
services: hdinsight
author: jasonwhowell
ms.author: jasonh
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: tutorial
ms.date: 04/16/2018
ms.openlocfilehash: c52f64c2508870bf061e144229cf26ab269c343b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857811"
---
# <a name="tutorial-use-the-apache-kafka-producer-and-consumer-apis"></a><span data-ttu-id="64d2f-104">Tutorial: Use the Apache Kafka Producer and Consumer APIs</span><span class="sxs-lookup"><span data-stu-id="64d2f-104">Tutorial: Use the Apache Kafka Producer and Consumer APIs</span></span>

<span data-ttu-id="64d2f-105">Learn how to use the Kafka Producer and Consumer APIs with Kafka on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="64d2f-105">Learn how to use the Kafka Producer and Consumer APIs with Kafka on HDInsight.</span></span>

<span data-ttu-id="64d2f-106">The Kafka Producer API allows applications to send streams of data to the Kafka cluster.</span><span class="sxs-lookup"><span data-stu-id="64d2f-106">The Kafka Producer API allows applications to send streams of data to the Kafka cluster.</span></span> <span data-ttu-id="64d2f-107">The Kafka Consumer API allows applications to read streams of data from the cluster.</span><span class="sxs-lookup"><span data-stu-id="64d2f-107">The Kafka Consumer API allows applications to read streams of data from the cluster.</span></span>

<span data-ttu-id="64d2f-108">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="64d2f-108">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="64d2f-109">Set up your development environment</span><span class="sxs-lookup"><span data-stu-id="64d2f-109">Set up your development environment</span></span>
> * <span data-ttu-id="64d2f-110">Set up your deployment environment</span><span class="sxs-lookup"><span data-stu-id="64d2f-110">Set up your deployment environment</span></span>
> * <span data-ttu-id="64d2f-111">Understand the code</span><span class="sxs-lookup"><span data-stu-id="64d2f-111">Understand the code</span></span>
> * <span data-ttu-id="64d2f-112">Build and deploy the application</span><span class="sxs-lookup"><span data-stu-id="64d2f-112">Build and deploy the application</span></span>
> * <span data-ttu-id="64d2f-113">Run the application on the cluster</span><span class="sxs-lookup"><span data-stu-id="64d2f-113">Run the application on the cluster</span></span>

<span data-ttu-id="64d2f-114">For more information on the APIs, see Apache documentation on the [Producer API](https://kafka.apache.org/documentation/#producerapi) and [Consumer API](https://kafka.apache.org/documentation/#consumerapi).</span><span class="sxs-lookup"><span data-stu-id="64d2f-114">For more information on the APIs, see Apache documentation on the [Producer API](https://kafka.apache.org/documentation/#producerapi) and [Consumer API](https://kafka.apache.org/documentation/#consumerapi).</span></span>

## <a name="set-up-your-development-environment"></a><span data-ttu-id="64d2f-115">Set up your development environment</span><span class="sxs-lookup"><span data-stu-id="64d2f-115">Set up your development environment</span></span>

<span data-ttu-id="64d2f-116">You must have the following components installed in your development environment:</span><span class="sxs-lookup"><span data-stu-id="64d2f-116">You must have the following components installed in your development environment:</span></span>

* <span data-ttu-id="64d2f-117">[Java JDK 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) or an equivalent, such as OpenJDK.</span><span class="sxs-lookup"><span data-stu-id="64d2f-117">[Java JDK 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) or an equivalent, such as OpenJDK.</span></span>

* [<span data-ttu-id="64d2f-118">Apache Maven</span><span class="sxs-lookup"><span data-stu-id="64d2f-118">Apache Maven</span></span>](http://maven.apache.org/)

* <span data-ttu-id="64d2f-119">An SSH client and the `scp` command.</span><span class="sxs-lookup"><span data-stu-id="64d2f-119">An SSH client and the `scp` command.</span></span> <span data-ttu-id="64d2f-120">For more information, see the [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md) document.</span><span class="sxs-lookup"><span data-stu-id="64d2f-120">For more information, see the [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

* <span data-ttu-id="64d2f-121">A text editor or Java IDE.</span><span class="sxs-lookup"><span data-stu-id="64d2f-121">A text editor or Java IDE.</span></span>

<span data-ttu-id="64d2f-122">The following environment variables may be set when you install Java and the JDK on your development workstation.</span><span class="sxs-lookup"><span data-stu-id="64d2f-122">The following environment variables may be set when you install Java and the JDK on your development workstation.</span></span> <span data-ttu-id="64d2f-123">However, you should check that they exist and that they contain the correct values for your system.</span><span class="sxs-lookup"><span data-stu-id="64d2f-123">However, you should check that they exist and that they contain the correct values for your system.</span></span>

* <span data-ttu-id="64d2f-124">`JAVA_HOME` - should point to the directory where the JDK is installed.</span><span class="sxs-lookup"><span data-stu-id="64d2f-124">`JAVA_HOME` - should point to the directory where the JDK is installed.</span></span>
* <span data-ttu-id="64d2f-125">`PATH` - should contain the following paths:</span><span class="sxs-lookup"><span data-stu-id="64d2f-125">`PATH` - should contain the following paths:</span></span>
  
    * <span data-ttu-id="64d2f-126">`JAVA_HOME` (or the equivalent path).</span><span class="sxs-lookup"><span data-stu-id="64d2f-126">`JAVA_HOME` (or the equivalent path).</span></span>
    * <span data-ttu-id="64d2f-127">`JAVA_HOME\bin` (or the equivalent path).</span><span class="sxs-lookup"><span data-stu-id="64d2f-127">`JAVA_HOME\bin` (or the equivalent path).</span></span>
    * <span data-ttu-id="64d2f-128">The directory where Maven is installed.</span><span class="sxs-lookup"><span data-stu-id="64d2f-128">The directory where Maven is installed.</span></span>

## <a name="set-up-your-deployment-environment"></a><span data-ttu-id="64d2f-129">Set up your deployment environment</span><span class="sxs-lookup"><span data-stu-id="64d2f-129">Set up your deployment environment</span></span>

<span data-ttu-id="64d2f-130">This tutorial requires Kafka on HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="64d2f-130">This tutorial requires Kafka on HDInsight 3.6.</span></span> <span data-ttu-id="64d2f-131">To learn how to create a Kafka on HDInsight cluster, see the [Start with Kafka on HDInsight](apache-kafka-get-started.md) document.</span><span class="sxs-lookup"><span data-stu-id="64d2f-131">To learn how to create a Kafka on HDInsight cluster, see the [Start with Kafka on HDInsight](apache-kafka-get-started.md) document.</span></span>

## <a name="understand-the-code"></a><span data-ttu-id="64d2f-132">Understand the code</span><span class="sxs-lookup"><span data-stu-id="64d2f-132">Understand the code</span></span>

<span data-ttu-id="64d2f-133">The example application is located at [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started), in the `Producer-Consumer` subdirectory.</span><span class="sxs-lookup"><span data-stu-id="64d2f-133">The example application is located at [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started), in the `Producer-Consumer` subdirectory.</span></span> <span data-ttu-id="64d2f-134">The application consists primarily of four files:</span><span class="sxs-lookup"><span data-stu-id="64d2f-134">The application consists primarily of four files:</span></span>

* <span data-ttu-id="64d2f-135">`pom.xml`: This file defines the project dependencies, Java version, and packaging methods.</span><span class="sxs-lookup"><span data-stu-id="64d2f-135">`pom.xml`: This file defines the project dependencies, Java version, and packaging methods.</span></span>
* <span data-ttu-id="64d2f-136">`Producer.java`: This file sends 1 million (1,000,000) random sentences to Kafka using the producer API.</span><span class="sxs-lookup"><span data-stu-id="64d2f-136">`Producer.java`: This file sends 1 million (1,000,000) random sentences to Kafka using the producer API.</span></span>
* <span data-ttu-id="64d2f-137">`Consumer.java`: This file uses the consumer API to read data from Kafka and emit it to STDOUT.</span><span class="sxs-lookup"><span data-stu-id="64d2f-137">`Consumer.java`: This file uses the consumer API to read data from Kafka and emit it to STDOUT.</span></span>
* <span data-ttu-id="64d2f-138">`Run.java`: The command-line interface used to run the producer and consumer code.</span><span class="sxs-lookup"><span data-stu-id="64d2f-138">`Run.java`: The command-line interface used to run the producer and consumer code.</span></span>

### <a name="pomxml"></a><span data-ttu-id="64d2f-139">Pom.xml</span><span class="sxs-lookup"><span data-stu-id="64d2f-139">Pom.xml</span></span>

<span data-ttu-id="64d2f-140">The important things to understand in the `pom.xml` file are:</span><span class="sxs-lookup"><span data-stu-id="64d2f-140">The important things to understand in the `pom.xml` file are:</span></span>

* <span data-ttu-id="64d2f-141">Dependencies: This project relies on the Kafka producer and consumer APIs, which are provided by the `kafka-clients` package.</span><span class="sxs-lookup"><span data-stu-id="64d2f-141">Dependencies: This project relies on the Kafka producer and consumer APIs, which are provided by the `kafka-clients` package.</span></span> <span data-ttu-id="64d2f-142">The following XML code defines this dependency:</span><span class="sxs-lookup"><span data-stu-id="64d2f-142">The following XML code defines this dependency:</span></span>

    ```xml
    <!-- Kafka client for producer/consumer operations -->
    <dependency>
      <groupId>org.apache.kafka</groupId>
      <artifactId>kafka-clients</artifactId>
      <version>${kafka.version}</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="64d2f-143">The `${kafka.version}` entry is declared in the `<properties>..</properties>` section of `pom.xml`, and is configured to the Kafka version of the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="64d2f-143">The `${kafka.version}` entry is declared in the `<properties>..</properties>` section of `pom.xml`, and is configured to the Kafka version of the HDInsight cluster.</span></span>

* <span data-ttu-id="64d2f-144">Plugins: Maven plugins provide various capabilities.</span><span class="sxs-lookup"><span data-stu-id="64d2f-144">Plugins: Maven plugins provide various capabilities.</span></span> <span data-ttu-id="64d2f-145">In this project, the following plugins are used:</span><span class="sxs-lookup"><span data-stu-id="64d2f-145">In this project, the following plugins are used:</span></span>

    * <span data-ttu-id="64d2f-146">`maven-compiler-plugin`: Used to set the Java version used by the project to 8.</span><span class="sxs-lookup"><span data-stu-id="64d2f-146">`maven-compiler-plugin`: Used to set the Java version used by the project to 8.</span></span> <span data-ttu-id="64d2f-147">This is the version of Java used by HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="64d2f-147">This is the version of Java used by HDInsight 3.6.</span></span>
    * <span data-ttu-id="64d2f-148">`maven-shade-plugin`: Used to generate an uber jar that contains this application as well as any dependencies.</span><span class="sxs-lookup"><span data-stu-id="64d2f-148">`maven-shade-plugin`: Used to generate an uber jar that contains this application as well as any dependencies.</span></span> <span data-ttu-id="64d2f-149">It is also used to set the entry point of the application, so that you can directly run the Jar file without having to specify the main class.</span><span class="sxs-lookup"><span data-stu-id="64d2f-149">It is also used to set the entry point of the application, so that you can directly run the Jar file without having to specify the main class.</span></span>

### <a name="producerjava"></a><span data-ttu-id="64d2f-150">Producer.java</span><span class="sxs-lookup"><span data-stu-id="64d2f-150">Producer.java</span></span>

<span data-ttu-id="64d2f-151">The producer communicates with the Kafka broker hosts (worker nodes) to store data into a Kafka topic.</span><span class="sxs-lookup"><span data-stu-id="64d2f-151">The producer communicates with the Kafka broker hosts (worker nodes) to store data into a Kafka topic.</span></span> <span data-ttu-id="64d2f-152">The following code snippet from is from the `Producer.java` file:</span><span class="sxs-lookup"><span data-stu-id="64d2f-152">The following code snippet from is from the `Producer.java` file:</span></span>

```java
package com.microsoft.example;

import org.apache.kafka.clients.producer.KafkaProducer;
import org.apache.kafka.clients.producer.ProducerRecord;
import java.util.Properties;
import java.util.Random;
import java.io.IOException;

public class Producer
{
    public static void produce(String brokers) throws IOException
    {

        // Set properties used to configure the producer
        Properties properties = new Properties();
        // Set the brokers (bootstrap servers)
        properties.setProperty("bootstrap.servers", brokers);
        // Set how to serialize key/value pairs
        properties.setProperty("key.serializer","org.apache.kafka.common.serialization.StringSerializer");
        properties.setProperty("value.serializer","org.apache.kafka.common.serialization.StringSerializer");
        KafkaProducer<String, String> producer = new KafkaProducer<>(properties);

        // So we can generate random sentences
        Random random = new Random();
        String[] sentences = new String[] {
                "the cow jumped over the moon",
                "an apple a day keeps the doctor away",
                "four score and seven years ago",
                "snow white and the seven dwarfs",
                "i am at two with nature"
        };

        String progressAnimation = "|/-\\";
        // Produce a bunch of records
        for(int i = 0; i < 1000000; i++) {
            // Pick a sentence at random
            String sentence = sentences[random.nextInt(sentences.length)];
            // Send the sentence to the test topic
            producer.send(new ProducerRecord<String, String>("test", sentence));
            String progressBar = "\r" + progressAnimation.charAt(i % progressAnimation.length()) + " " + i;
            System.out.write(progressBar.getBytes());
        }
    }
}
```

<span data-ttu-id="64d2f-153">This code connects to the Kafka broker hosts (worker nodes), and then sends 1,000,000 sentences to Kafka using the Producer API.</span><span class="sxs-lookup"><span data-stu-id="64d2f-153">This code connects to the Kafka broker hosts (worker nodes), and then sends 1,000,000 sentences to Kafka using the Producer API.</span></span>

### <a name="consumerjava"></a><span data-ttu-id="64d2f-154">Consumer.java</span><span class="sxs-lookup"><span data-stu-id="64d2f-154">Consumer.java</span></span>

<span data-ttu-id="64d2f-155">The consumer communicates with the Kafka broker hosts (worker nodes), and reads records in a loop.</span><span class="sxs-lookup"><span data-stu-id="64d2f-155">The consumer communicates with the Kafka broker hosts (worker nodes), and reads records in a loop.</span></span> <span data-ttu-id="64d2f-156">The following code snippet is from the `Consumer.java` file:</span><span class="sxs-lookup"><span data-stu-id="64d2f-156">The following code snippet is from the `Consumer.java` file:</span></span>

```java
package com.microsoft.example;

import org.apache.kafka.clients.consumer.KafkaConsumer;
import org.apache.kafka.clients.consumer.ConsumerRecords;
import org.apache.kafka.clients.consumer.ConsumerRecord;
import java.util.Properties;
import java.util.Arrays;

public class Consumer {
    public static void consume(String brokers, String groupId) {
        // Create a consumer
        KafkaConsumer<String, String> consumer;
        // Configure the consumer
        Properties properties = new Properties();
        // Point it to the brokers
        properties.setProperty("bootstrap.servers", brokers);
        // Set the consumer group (all consumers must belong to a group).
        properties.setProperty("group.id", groupId);
        // Set how to serialize key/value pairs
        properties.setProperty("key.deserializer","org.apache.kafka.common.serialization.StringDeserializer");
        properties.setProperty("value.deserializer","org.apache.kafka.common.serialization.StringDeserializer");
        // When a group is first created, it has no offset stored to start reading from. This tells it to start
        // with the earliest record in the stream.
        properties.setProperty("auto.offset.reset","earliest");
        consumer = new KafkaConsumer<>(properties);

        // Subscribe to the 'test' topic
        consumer.subscribe(Arrays.asList("test"));

        // Loop until ctrl + c
        int count = 0;
        while(true) {
            // Poll for records
            ConsumerRecords<String, String> records = consumer.poll(200);
            // Did we get any?
            if (records.count() == 0) {
                // timeout/nothing to read
            } else {
                // Yes, loop over records
                for(ConsumerRecord<String, String> record: records) {
                    // Display record and count
                    count += 1;
                    System.out.println( count + ": " + record.value());
                }
            }
        }
    }
}
```

<span data-ttu-id="64d2f-157">In this code, the consumer is configured to read from the start of the topic (`auto.offset.reset` is set to `earliest`.)</span><span class="sxs-lookup"><span data-stu-id="64d2f-157">In this code, the consumer is configured to read from the start of the topic (`auto.offset.reset` is set to `earliest`.)</span></span>

### <a name="runjava"></a><span data-ttu-id="64d2f-158">Run.java</span><span class="sxs-lookup"><span data-stu-id="64d2f-158">Run.java</span></span>

<span data-ttu-id="64d2f-159">The `Run.java` file provides a command line interface that runs either the producer or consumer code.</span><span class="sxs-lookup"><span data-stu-id="64d2f-159">The `Run.java` file provides a command line interface that runs either the producer or consumer code.</span></span> <span data-ttu-id="64d2f-160">You must provide the Kafka broker host information as a parameter.</span><span class="sxs-lookup"><span data-stu-id="64d2f-160">You must provide the Kafka broker host information as a parameter.</span></span> <span data-ttu-id="64d2f-161">You can optionally include a group id value, which is used by the consumer process.</span><span class="sxs-lookup"><span data-stu-id="64d2f-161">You can optionally include a group id value, which is used by the consumer process.</span></span> <span data-ttu-id="64d2f-162">If you create multiple consumer instances using the same group id, they will load balance reading from the topic.</span><span class="sxs-lookup"><span data-stu-id="64d2f-162">If you create multiple consumer instances using the same group id, they will load balance reading from the topic.</span></span>

```java
package com.microsoft.example;

import java.io.IOException;
import java.util.UUID;

// Handle starting producer or consumer
public class Run {
    public static void main(String[] args) throws IOException {
        if(args.length < 2) {
            usage();
        }

        // Get the brokers
        String brokers = args[1];
        switch(args[0].toLowerCase()) {
            case "producer":
                Producer.produce(brokers);
                break;
            case "consumer":
                // Either a groupId was passed in, or we need a random one
                String groupId;
                if(args.length == 3) {
                    groupId = args[2];
                } else {
                    groupId = UUID.randomUUID().toString();
                }
                Consumer.consume(brokers, groupId);
                break;
            default:
                usage();
        }
        System.exit(0);
    }
    // Display usage
    public static void usage() {
        System.out.println("Usage:");
        System.out.println("kafka-example.jar <producer|consumer> brokerhosts [groupid]");
        System.exit(1);
    }
}
```

## <a name="build-and-deploy-the-example"></a><span data-ttu-id="64d2f-163">Build and deploy the example</span><span class="sxs-lookup"><span data-stu-id="64d2f-163">Build and deploy the example</span></span>

1. <span data-ttu-id="64d2f-164">Download the examples from [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started).</span><span class="sxs-lookup"><span data-stu-id="64d2f-164">Download the examples from [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started).</span></span>

2. <span data-ttu-id="64d2f-165">Change directories to the location of the `Producer-Consumer` directory and use the following command:</span><span class="sxs-lookup"><span data-stu-id="64d2f-165">Change directories to the location of the `Producer-Consumer` directory and use the following command:</span></span>

    ```
    mvn clean package
    ```

    <span data-ttu-id="64d2f-166">This command creates a directory named `target`, that contains a file named `kafka-producer-consumer-1.0-SNAPSHOT.jar`.</span><span class="sxs-lookup"><span data-stu-id="64d2f-166">This command creates a directory named `target`, that contains a file named `kafka-producer-consumer-1.0-SNAPSHOT.jar`.</span></span>

3. <span data-ttu-id="64d2f-167">Use the following commands to copy the `kafka-producer-consumer-1.0-SNAPSHOT.jar` file to your HDInsight cluster:</span><span class="sxs-lookup"><span data-stu-id="64d2f-167">Use the following commands to copy the `kafka-producer-consumer-1.0-SNAPSHOT.jar` file to your HDInsight cluster:</span></span>
   
    ```bash
    scp ./target/kafka-producer-consumer-1.0-SNAPSHOT.jar SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net:kafka-producer-consumer.jar
    ```
   
    <span data-ttu-id="64d2f-168">Replace **SSHUSER** with the SSH user for your cluster, and replace **CLUSTERNAME** with the name of your cluster.</span><span class="sxs-lookup"><span data-stu-id="64d2f-168">Replace **SSHUSER** with the SSH user for your cluster, and replace **CLUSTERNAME** with the name of your cluster.</span></span> <span data-ttu-id="64d2f-169">When prompted enter the password for the SSH user.</span><span class="sxs-lookup"><span data-stu-id="64d2f-169">When prompted enter the password for the SSH user.</span></span>

## <a id="run"></a> <span data-ttu-id="64d2f-170">Run the example</span><span class="sxs-lookup"><span data-stu-id="64d2f-170">Run the example</span></span>

1. <span data-ttu-id="64d2f-171">To open an SSH connection to the cluster, use the following command:</span><span class="sxs-lookup"><span data-stu-id="64d2f-171">To open an SSH connection to the cluster, use the following command:</span></span>

    ```bash
    ssh SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="64d2f-172">Replace **SSHUSER** with the SSH user for your cluster, and replace **CLUSTERNAME** with the name of your cluster.</span><span class="sxs-lookup"><span data-stu-id="64d2f-172">Replace **SSHUSER** with the SSH user for your cluster, and replace **CLUSTERNAME** with the name of your cluster.</span></span> <span data-ttu-id="64d2f-173">If prompted, enter the password for the SSH user account.</span><span class="sxs-lookup"><span data-stu-id="64d2f-173">If prompted, enter the password for the SSH user account.</span></span> <span data-ttu-id="64d2f-174">For more information on using `scp` with HDInsight, see [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="64d2f-174">For more information on using `scp` with HDInsight, see [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="64d2f-175">To create the Kafka topics that are used by this example, use the following steps:</span><span class="sxs-lookup"><span data-stu-id="64d2f-175">To create the Kafka topics that are used by this example, use the following steps:</span></span>

    1. <span data-ttu-id="64d2f-176">To save the cluster name to a variable and install a JSON parsing utility (`jq`), use the following commands.</span><span class="sxs-lookup"><span data-stu-id="64d2f-176">To save the cluster name to a variable and install a JSON parsing utility (`jq`), use the following commands.</span></span> <span data-ttu-id="64d2f-177">When prompted, enter the Kafka cluster name:</span><span class="sxs-lookup"><span data-stu-id="64d2f-177">When prompted, enter the Kafka cluster name:</span></span>
    
        ```bash
        sudo apt -y install jq
        read -p 'Enter your Kafka cluster name:' CLUSTERNAME
        ```
    
    2. <span data-ttu-id="64d2f-178">To get the Kafka broker hosts and the Zookeeper hosts, use the following commands.</span><span class="sxs-lookup"><span data-stu-id="64d2f-178">To get the Kafka broker hosts and the Zookeeper hosts, use the following commands.</span></span> <span data-ttu-id="64d2f-179">When prompted, enter the password for the cluster login (admin) account.</span><span class="sxs-lookup"><span data-stu-id="64d2f-179">When prompted, enter the password for the cluster login (admin) account.</span></span>
    
        ```bash
        export KAFKAZKHOSTS=`curl -sS -u admin -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`; \
        export KAFKABROKERS=`curl -sS -u admin -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`; \
        ```

    3. <span data-ttu-id="64d2f-180">To create the `test` topic, use the following command:</span><span class="sxs-lookup"><span data-stu-id="64d2f-180">To create the `test` topic, use the following command:</span></span>

        ```bash
        /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic test --zookeeper $KAFKAZKHOSTS
        ```
    4. <span data-ttu-id="64d2f-181">You can also use the jar file to create a topic.</span><span class="sxs-lookup"><span data-stu-id="64d2f-181">You can also use the jar file to create a topic.</span></span> <span data-ttu-id="64d2f-182">For example to create `test2` topic, use the following command:</span><span class="sxs-lookup"><span data-stu-id="64d2f-182">For example to create `test2` topic, use the following command:</span></span>

        ```bash
        java -jar kafka-producer-consumer.jar create test2 $KAFKABROKERS
        ```

3. <span data-ttu-id="64d2f-183">To run the producer and write data to the topic, use the following command:</span><span class="sxs-lookup"><span data-stu-id="64d2f-183">To run the producer and write data to the topic, use the following command:</span></span>

    ```bash
    java -jar kafka-producer-consumer.jar producer test $KAFKABROKERS
    ```

4. <span data-ttu-id="64d2f-184">Once the producer has finished, use the following command to read from the topic:</span><span class="sxs-lookup"><span data-stu-id="64d2f-184">Once the producer has finished, use the following command to read from the topic:</span></span>
   
    ```bash
    java -jar kafka-producer-consumer.jar consumer test $KAFKABROKERS
    ```
   
    <span data-ttu-id="64d2f-185">The records read, along with a count of records, is displayed.</span><span class="sxs-lookup"><span data-stu-id="64d2f-185">The records read, along with a count of records, is displayed.</span></span>

5. <span data-ttu-id="64d2f-186">Use __Ctrl + C__ to exit the consumer.</span><span class="sxs-lookup"><span data-stu-id="64d2f-186">Use __Ctrl + C__ to exit the consumer.</span></span>

### <a name="multiple-consumers"></a><span data-ttu-id="64d2f-187">Multiple consumers</span><span class="sxs-lookup"><span data-stu-id="64d2f-187">Multiple consumers</span></span>

<span data-ttu-id="64d2f-188">Kafka consumers use a consumer group when reading records.</span><span class="sxs-lookup"><span data-stu-id="64d2f-188">Kafka consumers use a consumer group when reading records.</span></span> <span data-ttu-id="64d2f-189">Using the same group with multiple consumers results in load balanced reads from a topic.</span><span class="sxs-lookup"><span data-stu-id="64d2f-189">Using the same group with multiple consumers results in load balanced reads from a topic.</span></span> <span data-ttu-id="64d2f-190">Each consumer in the group receives a portion of the records.</span><span class="sxs-lookup"><span data-stu-id="64d2f-190">Each consumer in the group receives a portion of the records.</span></span>

<span data-ttu-id="64d2f-191">The consumer application accepts a parameter that is used as the group ID.</span><span class="sxs-lookup"><span data-stu-id="64d2f-191">The consumer application accepts a parameter that is used as the group ID.</span></span> <span data-ttu-id="64d2f-192">For example, the following command starts a consumer using a group ID of `mygroup`:</span><span class="sxs-lookup"><span data-stu-id="64d2f-192">For example, the following command starts a consumer using a group ID of `mygroup`:</span></span>
   
```bash
java -jar kafka-producer-consumer.jar consumer test $KAFKABROKERS mygroup
```

<span data-ttu-id="64d2f-193">To see this process in action, use the following command:</span><span class="sxs-lookup"><span data-stu-id="64d2f-193">To see this process in action, use the following command:</span></span>

```bash
tmux new-session 'java -jar kafka-producer-consumer.jar consumer test $KAFKABROKERS mygroup' \; split-w
indow -h 'java -jar kafka-producer-consumer.jar consumer test $KAFKABROKERS mygroup' \; attach
```

<span data-ttu-id="64d2f-194">This command uses `tmux` to split the terminal into two columns.</span><span class="sxs-lookup"><span data-stu-id="64d2f-194">This command uses `tmux` to split the terminal into two columns.</span></span> <span data-ttu-id="64d2f-195">A consumer is started in each column, with the same group ID value.</span><span class="sxs-lookup"><span data-stu-id="64d2f-195">A consumer is started in each column, with the same group ID value.</span></span> <span data-ttu-id="64d2f-196">Once the consumers finish reading, notice that each read only a portion of the records.</span><span class="sxs-lookup"><span data-stu-id="64d2f-196">Once the consumers finish reading, notice that each read only a portion of the records.</span></span> <span data-ttu-id="64d2f-197">Use __Ctrl + C __ twice to exit `tmux`.</span><span class="sxs-lookup"><span data-stu-id="64d2f-197">Use __Ctrl + C __ twice to exit `tmux`.</span></span>

<span data-ttu-id="64d2f-198">Consumption by clients within the same group is handled through the partitions for the topic.</span><span class="sxs-lookup"><span data-stu-id="64d2f-198">Consumption by clients within the same group is handled through the partitions for the topic.</span></span> <span data-ttu-id="64d2f-199">For the `test` topic created earlier, it has eight partitions.</span><span class="sxs-lookup"><span data-stu-id="64d2f-199">For the `test` topic created earlier, it has eight partitions.</span></span> <span data-ttu-id="64d2f-200">If you start eight consumers, each consumer reads records from a single partition for the topic.</span><span class="sxs-lookup"><span data-stu-id="64d2f-200">If you start eight consumers, each consumer reads records from a single partition for the topic.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="64d2f-201">There cannot be more consumer instances in a consumer group than partitions.</span><span class="sxs-lookup"><span data-stu-id="64d2f-201">There cannot be more consumer instances in a consumer group than partitions.</span></span> <span data-ttu-id="64d2f-202">In this example, one consumer group can contain up to eight consumers since that is the number of partitions in the topic.</span><span class="sxs-lookup"><span data-stu-id="64d2f-202">In this example, one consumer group can contain up to eight consumers since that is the number of partitions in the topic.</span></span> <span data-ttu-id="64d2f-203">Or you can have multiple consumer groups, each with no more than eight consumers.</span><span class="sxs-lookup"><span data-stu-id="64d2f-203">Or you can have multiple consumer groups, each with no more than eight consumers.</span></span>

<span data-ttu-id="64d2f-204">Records stored in Kafka are stored in the order they are received within a partition.</span><span class="sxs-lookup"><span data-stu-id="64d2f-204">Records stored in Kafka are stored in the order they are received within a partition.</span></span> <span data-ttu-id="64d2f-205">To achieve in-ordered delivery for records *within a partition*, create a consumer group where the number of consumer instances matches the number of partitions.</span><span class="sxs-lookup"><span data-stu-id="64d2f-205">To achieve in-ordered delivery for records *within a partition*, create a consumer group where the number of consumer instances matches the number of partitions.</span></span> <span data-ttu-id="64d2f-206">To achieve in-ordered delivery for records *within the topic*, create a consumer group with only one consumer instance.</span><span class="sxs-lookup"><span data-stu-id="64d2f-206">To achieve in-ordered delivery for records *within the topic*, create a consumer group with only one consumer instance.</span></span>

## <a name="next-steps"></a><span data-ttu-id="64d2f-207">Next steps</span><span class="sxs-lookup"><span data-stu-id="64d2f-207">Next steps</span></span>

<span data-ttu-id="64d2f-208">In this document, you learned how to use the Kafka Producer and Consumer API with Kafka on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="64d2f-208">In this document, you learned how to use the Kafka Producer and Consumer API with Kafka on HDInsight.</span></span> <span data-ttu-id="64d2f-209">Use the following to learn more about working with Kafka:</span><span class="sxs-lookup"><span data-stu-id="64d2f-209">Use the following to learn more about working with Kafka:</span></span>

* [<span data-ttu-id="64d2f-210">Analyze Kafka logs</span><span class="sxs-lookup"><span data-stu-id="64d2f-210">Analyze Kafka logs</span></span>](apache-kafka-log-analytics-operations-management.md)
* [<span data-ttu-id="64d2f-211">Replicate data between Kafka clusters</span><span class="sxs-lookup"><span data-stu-id="64d2f-211">Replicate data between Kafka clusters</span></span>](apache-kafka-mirroring.md)
* [<span data-ttu-id="64d2f-212">Kafka Streams API with HDInsight</span><span class="sxs-lookup"><span data-stu-id="64d2f-212">Kafka Streams API with HDInsight</span></span>](apache-kafka-streams-api.md)
