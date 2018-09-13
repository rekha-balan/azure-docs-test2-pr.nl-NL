---
title: Using Akka Streams with Azure Event Hubs for Apache Kafka | Microsoft Docs
description: Connecting Akka Streams to a Kafka enabled Event Hub
services: event-hubs
documentationcenter: ''
author: basilhariri
manager: timlt
editor: ''
ms.assetid: ''
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.custom: mvc
ms.date: 08/06/2018
ms.author: bahariri
ms.openlocfilehash: 7c09656f62f3a8a2efd889cf28f12bd5a42e309a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857446"
---
# <a name="using-akka-streams-with-event-hubs-for-apache-kafka"></a><span data-ttu-id="736be-103">Using Akka Streams with Event Hubs for Apache Kafka</span><span class="sxs-lookup"><span data-stu-id="736be-103">Using Akka Streams with Event Hubs for Apache Kafka</span></span>
<span data-ttu-id="736be-104">This tutorial shows you how to connect Akka Streams to Kafka-enabled event hubs without changing your protocol clients or running your own clusters.</span><span class="sxs-lookup"><span data-stu-id="736be-104">This tutorial shows you how to connect Akka Streams to Kafka-enabled event hubs without changing your protocol clients or running your own clusters.</span></span> <span data-ttu-id="736be-105">Azure Event Hubs for the Kafka supports [Apache Kafka version 1.0.](https://kafka.apache.org/10/documentation.html)</span><span class="sxs-lookup"><span data-stu-id="736be-105">Azure Event Hubs for the Kafka supports [Apache Kafka version 1.0.](https://kafka.apache.org/10/documentation.html)</span></span>

<span data-ttu-id="736be-106">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="736be-106">In this tutorial, you learn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="736be-107">Create an Event Hubs namespace</span><span class="sxs-lookup"><span data-stu-id="736be-107">Create an Event Hubs namespace</span></span>
> * <span data-ttu-id="736be-108">Clone the example project</span><span class="sxs-lookup"><span data-stu-id="736be-108">Clone the example project</span></span>
> * <span data-ttu-id="736be-109">Run Flink producer</span><span class="sxs-lookup"><span data-stu-id="736be-109">Run Flink producer</span></span> 
> * <span data-ttu-id="736be-110">Run Flink consumer</span><span class="sxs-lookup"><span data-stu-id="736be-110">Run Flink consumer</span></span>

## <a name="prerequisites"></a><span data-ttu-id="736be-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="736be-111">Prerequisites</span></span>

<span data-ttu-id="736be-112">To complete this tutorial, make sure you have the following prerequisites:</span><span class="sxs-lookup"><span data-stu-id="736be-112">To complete this tutorial, make sure you have the following prerequisites:</span></span>

* <span data-ttu-id="736be-113">Read through the [Event Hubs for Apache Kafka](event-hubs-for-kafka-ecosystem-overview.md) article.</span><span class="sxs-lookup"><span data-stu-id="736be-113">Read through the [Event Hubs for Apache Kafka](event-hubs-for-kafka-ecosystem-overview.md) article.</span></span> 
* <span data-ttu-id="736be-114">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="736be-114">An Azure subscription.</span></span> <span data-ttu-id="736be-115">If you do not have one, create a [free account](https://azure.microsoft.com/free/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio) before you begin.</span><span class="sxs-lookup"><span data-stu-id="736be-115">If you do not have one, create a [free account](https://azure.microsoft.com/free/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio) before you begin.</span></span>
* [<span data-ttu-id="736be-116">Java Development Kit (JDK) 1.8+</span><span class="sxs-lookup"><span data-stu-id="736be-116">Java Development Kit (JDK) 1.8+</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/index.html)
    * <span data-ttu-id="736be-117">On Ubuntu, run `apt-get install default-jdk` to install the JDK.</span><span class="sxs-lookup"><span data-stu-id="736be-117">On Ubuntu, run `apt-get install default-jdk` to install the JDK.</span></span>
    * <span data-ttu-id="736be-118">Be sure to set the JAVA_HOME environment variable to point to the folder where the JDK is installed.</span><span class="sxs-lookup"><span data-stu-id="736be-118">Be sure to set the JAVA_HOME environment variable to point to the folder where the JDK is installed.</span></span>
* <span data-ttu-id="736be-119">[Download](http://maven.apache.org/download.cgi) and [install](http://maven.apache.org/install.html) a Maven binary archive</span><span class="sxs-lookup"><span data-stu-id="736be-119">[Download](http://maven.apache.org/download.cgi) and [install](http://maven.apache.org/install.html) a Maven binary archive</span></span>
    * <span data-ttu-id="736be-120">On Ubuntu, you can run `apt-get install maven` to install Maven.</span><span class="sxs-lookup"><span data-stu-id="736be-120">On Ubuntu, you can run `apt-get install maven` to install Maven.</span></span>
* [<span data-ttu-id="736be-121">Git</span><span class="sxs-lookup"><span data-stu-id="736be-121">Git</span></span>](https://www.git-scm.com/downloads)
    * <span data-ttu-id="736be-122">On Ubuntu, you can run `sudo apt-get install git` to install Git.</span><span class="sxs-lookup"><span data-stu-id="736be-122">On Ubuntu, you can run `sudo apt-get install git` to install Git.</span></span>

## <a name="create-an-event-hubs-namespace"></a><span data-ttu-id="736be-123">Create an Event Hubs namespace</span><span class="sxs-lookup"><span data-stu-id="736be-123">Create an Event Hubs namespace</span></span>

<span data-ttu-id="736be-124">An Event Hubs namespace is required to send or receive from any Event Hubs service.</span><span class="sxs-lookup"><span data-stu-id="736be-124">An Event Hubs namespace is required to send or receive from any Event Hubs service.</span></span> <span data-ttu-id="736be-125">See [Create Kafka Enabled Event Hubs](event-hubs-create-kafka-enabled.md) for information about getting an Event Hubs Kafka endpoint.</span><span class="sxs-lookup"><span data-stu-id="736be-125">See [Create Kafka Enabled Event Hubs](event-hubs-create-kafka-enabled.md) for information about getting an Event Hubs Kafka endpoint.</span></span> <span data-ttu-id="736be-126">Make sure to copy the Event Hubs connection string for later use.</span><span class="sxs-lookup"><span data-stu-id="736be-126">Make sure to copy the Event Hubs connection string for later use.</span></span>

## <a name="clone-the-example-project"></a><span data-ttu-id="736be-127">Clone the example project</span><span class="sxs-lookup"><span data-stu-id="736be-127">Clone the example project</span></span>

<span data-ttu-id="736be-128">Now that you have a Kafka-enabled Event Hubs connection string, clone the Azure Event Hubs repository and navigate to the `akka` subfolder:</span><span class="sxs-lookup"><span data-stu-id="736be-128">Now that you have a Kafka-enabled Event Hubs connection string, clone the Azure Event Hubs repository and navigate to the `akka` subfolder:</span></span>

```shell
git clone https://github.com/Azure/azure-event-hubs.git
cd azure-event-hubs/samples/kafka/akka
```

## <a name="run-akka-streams-producer"></a><span data-ttu-id="736be-129">Run Akka Streams producer</span><span class="sxs-lookup"><span data-stu-id="736be-129">Run Akka Streams producer</span></span>

<span data-ttu-id="736be-130">Using the provided Akka Streams producer example, send messages to the Event Hubs service.</span><span class="sxs-lookup"><span data-stu-id="736be-130">Using the provided Akka Streams producer example, send messages to the Event Hubs service.</span></span>

### <a name="provide-an-event-hubs-kafka-endpoint"></a><span data-ttu-id="736be-131">Provide an Event Hubs Kafka endpoint</span><span class="sxs-lookup"><span data-stu-id="736be-131">Provide an Event Hubs Kafka endpoint</span></span>

#### <a name="producer-applicationconf"></a><span data-ttu-id="736be-132">Producer application.conf</span><span class="sxs-lookup"><span data-stu-id="736be-132">Producer application.conf</span></span>

<span data-ttu-id="736be-133">Update the `bootstrap.servers` and `sasl.jaas.config` values in `producer/src/main/resources/application.conf` to direct the producer to the Event Hubs Kafka endpoint with the correct authentication.</span><span class="sxs-lookup"><span data-stu-id="736be-133">Update the `bootstrap.servers` and `sasl.jaas.config` values in `producer/src/main/resources/application.conf` to direct the producer to the Event Hubs Kafka endpoint with the correct authentication.</span></span>

```xml
akka.kafka.producer {
    #Akka Kafka producer properties can be defined here


    # Properties defined by org.apache.kafka.clients.producer.ProducerConfig
    # can be defined in this configuration section.
    kafka-clients {
        bootstrap.servers="{YOUR.EVENTHUBS.FQDN}:9093"
        sasl.mechanism=PLAIN
        security.protocol=SASL_SSL
        sasl.jaas.config="org.apache.kafka.common.security.plain.PlainLoginModule required username=\"$ConnectionString\" password=\"{YOUR.EVENTHUBS.CONNECTION.STRING}\";"
    }
}
```

### <a name="run-producer-from-the-command-line"></a><span data-ttu-id="736be-134">Run producer from the command line</span><span class="sxs-lookup"><span data-stu-id="736be-134">Run producer from the command line</span></span>

<span data-ttu-id="736be-135">To run the producer from the command line, generate the JAR and then run from within Maven (or generate the JAR using Maven, then run in Java by adding the necessary Kafka JAR(s) to the classpath):</span><span class="sxs-lookup"><span data-stu-id="736be-135">To run the producer from the command line, generate the JAR and then run from within Maven (or generate the JAR using Maven, then run in Java by adding the necessary Kafka JAR(s) to the classpath):</span></span>

```shell
mvn clean package
mvn exec:java -Dexec.mainClass="AkkaTestProducer"
```

<span data-ttu-id="736be-136">The producer begins sending events to the Kafka-enabled event hub at topic `test`, and prints the events to stdout.</span><span class="sxs-lookup"><span data-stu-id="736be-136">The producer begins sending events to the Kafka-enabled event hub at topic `test`, and prints the events to stdout.</span></span>

## <a name="run-akka-streams-consumer"></a><span data-ttu-id="736be-137">Run Akka Streams consumer</span><span class="sxs-lookup"><span data-stu-id="736be-137">Run Akka Streams consumer</span></span>

<span data-ttu-id="736be-138">Using the provided consumer example, receive messages from the Kafka-enabled event hubs.</span><span class="sxs-lookup"><span data-stu-id="736be-138">Using the provided consumer example, receive messages from the Kafka-enabled event hubs.</span></span>

### <a name="provide-an-event-hubs-kafka-endpoint"></a><span data-ttu-id="736be-139">Provide an Event Hubs Kafka endpoint</span><span class="sxs-lookup"><span data-stu-id="736be-139">Provide an Event Hubs Kafka endpoint</span></span>

#### <a name="consumer-applicationconf"></a><span data-ttu-id="736be-140">Consumer application.conf</span><span class="sxs-lookup"><span data-stu-id="736be-140">Consumer application.conf</span></span>

<span data-ttu-id="736be-141">Update the `bootstrap.servers` and `sasl.jaas.config` values in `consumer/src/main/resources/application.conf` to direct the consumer to the Event Hubs Kafka endpoint with the correct authentication.</span><span class="sxs-lookup"><span data-stu-id="736be-141">Update the `bootstrap.servers` and `sasl.jaas.config` values in `consumer/src/main/resources/application.conf` to direct the consumer to the Event Hubs Kafka endpoint with the correct authentication.</span></span>

```xml
akka.kafka.consumer {
    #Akka Kafka consumer properties defined here
    wakeup-timeout=60s

    # Properties defined by org.apache.kafka.clients.consumer.ConsumerConfig
    # defined in this configuration section.
    kafka-clients {
       request.timeout.ms=60000
       group.id=akka-example-consumer

       bootstrap.servers="{YOUR.EVENTHUBS.FQDN}:9093"
       sasl.mechanism=PLAIN
       security.protocol=SASL_SSL
       sasl.jaas.config="org.apache.kafka.common.security.plain.PlainLoginModule required username=\"$ConnectionString\" password=\"{YOUR.EVENTHUBS.CONNECTION.STRING}\";"
    }
}
```

### <a name="run-consumer-from-the-command-line"></a><span data-ttu-id="736be-142">Run consumer from the command line</span><span class="sxs-lookup"><span data-stu-id="736be-142">Run consumer from the command line</span></span>

<span data-ttu-id="736be-143">To run the consumer from the command line, generate the JAR and then run from within Maven (or generate the JAR using Maven, then run in Java by adding the necessary Kafka JAR(s) to the classpath):</span><span class="sxs-lookup"><span data-stu-id="736be-143">To run the consumer from the command line, generate the JAR and then run from within Maven (or generate the JAR using Maven, then run in Java by adding the necessary Kafka JAR(s) to the classpath):</span></span>

```shell
mvn clean package
mvn exec:java -Dexec.mainClass="AkkaTestConsumer"
```

<span data-ttu-id="736be-144">If the Kafka-enabled event hub has events (for instance, if your producer is also running), then the consumer begins receiving events from topic `test`.</span><span class="sxs-lookup"><span data-stu-id="736be-144">If the Kafka-enabled event hub has events (for instance, if your producer is also running), then the consumer begins receiving events from topic `test`.</span></span> 

<span data-ttu-id="736be-145">Check out the [Akka Streams Kafka Guide](https://doc.akka.io/docs/akka-stream-kafka/current/home.html) for more detailed information about Akka Streams.</span><span class="sxs-lookup"><span data-stu-id="736be-145">Check out the [Akka Streams Kafka Guide](https://doc.akka.io/docs/akka-stream-kafka/current/home.html) for more detailed information about Akka Streams.</span></span>

## <a name="next-steps"></a><span data-ttu-id="736be-146">Next steps</span><span class="sxs-lookup"><span data-stu-id="736be-146">Next steps</span></span>
<span data-ttu-id="736be-147">In this tutorial, you learned how to connect Akka Streams to Kafka-enabled event hubs without changing your protocol clients or running your own clusters.</span><span class="sxs-lookup"><span data-stu-id="736be-147">In this tutorial, you learned how to connect Akka Streams to Kafka-enabled event hubs without changing your protocol clients or running your own clusters.</span></span> <span data-ttu-id="736be-148">Azure Event Hubs for the Kafka supports [Apache Kafka version 1.0.](https://kafka.apache.org/10/documentation.html).</span><span class="sxs-lookup"><span data-stu-id="736be-148">Azure Event Hubs for the Kafka supports [Apache Kafka version 1.0.](https://kafka.apache.org/10/documentation.html).</span></span> <span data-ttu-id="736be-149">You did the following actions as part of this tutorial:</span><span class="sxs-lookup"><span data-stu-id="736be-149">You did the following actions as part of this tutorial:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="736be-150">Create an Event Hubs namespace</span><span class="sxs-lookup"><span data-stu-id="736be-150">Create an Event Hubs namespace</span></span>
> * <span data-ttu-id="736be-151">Clone the example project</span><span class="sxs-lookup"><span data-stu-id="736be-151">Clone the example project</span></span>
> * <span data-ttu-id="736be-152">Run Flink producer</span><span class="sxs-lookup"><span data-stu-id="736be-152">Run Flink producer</span></span> 
> * <span data-ttu-id="736be-153">Run Flink consumer</span><span class="sxs-lookup"><span data-stu-id="736be-153">Run Flink consumer</span></span>

<span data-ttu-id="736be-154">To learn more about Event Hubs and Event Hubs for Kafka, see the following topic:</span><span class="sxs-lookup"><span data-stu-id="736be-154">To learn more about Event Hubs and Event Hubs for Kafka, see the following topic:</span></span>  

* [<span data-ttu-id="736be-155">Learn about Event Hubs</span><span class="sxs-lookup"><span data-stu-id="736be-155">Learn about Event Hubs</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="736be-156">Learn about Event Hubs for Kafka</span><span class="sxs-lookup"><span data-stu-id="736be-156">Learn about Event Hubs for Kafka</span></span>](event-hubs-for-kafka-ecosystem-overview.md)
* <span data-ttu-id="736be-157">Use [MirrorMaker](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=27846330) to [stream events from Kafka on-prem to Kafka enabled Event Hubs on cloud.](event-hubs-kafka-mirror-maker-tutorial.md)</span><span class="sxs-lookup"><span data-stu-id="736be-157">Use [MirrorMaker](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=27846330) to [stream events from Kafka on-prem to Kafka enabled Event Hubs on cloud.](event-hubs-kafka-mirror-maker-tutorial.md)</span></span>
* <span data-ttu-id="736be-158">Learn how to stream into Kafka enabled Event Hubs using [native Kafka applications](event-hubs-quickstart-kafka-enabled-event-hubs.md) or [Apache Flink](event-hubs-kafka-flink-tutorial.md)</span><span class="sxs-lookup"><span data-stu-id="736be-158">Learn how to stream into Kafka enabled Event Hubs using [native Kafka applications](event-hubs-quickstart-kafka-enabled-event-hubs.md) or [Apache Flink](event-hubs-kafka-flink-tutorial.md)</span></span>
