---
title: Use Apache Flink with Azure Event Hubs for Apache Kafka | Microsoft Docs
description: Connecting Apache Flink to a Kafka enabled event hub
services: event-hubs
documentationcenter: ''
author: basilhariri
manager: timlt
ms.service: event-hubs
ms.topic: article
ms.custom: mvc
ms.date: 08/06/2018
ms.author: bahariri
ms.openlocfilehash: b724ddfc1214ac17c2138dc9875896cf3353f0c7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867671"
---
# <a name="use-apache-flink-with-azure-event-hubs-for-apache-kafka"></a><span data-ttu-id="14132-103">Use Apache Flink with Azure Event Hubs for Apache Kafka</span><span class="sxs-lookup"><span data-stu-id="14132-103">Use Apache Flink with Azure Event Hubs for Apache Kafka</span></span>
<span data-ttu-id="14132-104">This tutorial shows you how to connect Apache Flink to Kafka-enabled event hubs without changing your protocol clients or running your own clusters.</span><span class="sxs-lookup"><span data-stu-id="14132-104">This tutorial shows you how to connect Apache Flink to Kafka-enabled event hubs without changing your protocol clients or running your own clusters.</span></span> <span data-ttu-id="14132-105">Azure Event Hubs supports [Apache Kafka version 1.0.](https://kafka.apache.org/10/documentation.html).</span><span class="sxs-lookup"><span data-stu-id="14132-105">Azure Event Hubs supports [Apache Kafka version 1.0.](https://kafka.apache.org/10/documentation.html).</span></span>

<span data-ttu-id="14132-106">One of the key benefits of using Apache Kafka is the ecosystem of frameworks it can connect to.</span><span class="sxs-lookup"><span data-stu-id="14132-106">One of the key benefits of using Apache Kafka is the ecosystem of frameworks it can connect to.</span></span> <span data-ttu-id="14132-107">Kafka enabled Event Hubs combines the flexibility of Kafka with the scalability, consistency, and support of the Azure ecosystem.</span><span class="sxs-lookup"><span data-stu-id="14132-107">Kafka enabled Event Hubs combines the flexibility of Kafka with the scalability, consistency, and support of the Azure ecosystem.</span></span>

<span data-ttu-id="14132-108">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="14132-108">In this tutorial, you learn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="14132-109">Create an Event Hubs namespace</span><span class="sxs-lookup"><span data-stu-id="14132-109">Create an Event Hubs namespace</span></span>
> * <span data-ttu-id="14132-110">Clone the example project</span><span class="sxs-lookup"><span data-stu-id="14132-110">Clone the example project</span></span>
> * <span data-ttu-id="14132-111">Run Flink producer</span><span class="sxs-lookup"><span data-stu-id="14132-111">Run Flink producer</span></span> 
> * <span data-ttu-id="14132-112">Run Flink consumer</span><span class="sxs-lookup"><span data-stu-id="14132-112">Run Flink consumer</span></span>

## <a name="prerequisites"></a><span data-ttu-id="14132-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="14132-113">Prerequisites</span></span>

<span data-ttu-id="14132-114">To complete this tutorial, make sure you have the following prerequisites:</span><span class="sxs-lookup"><span data-stu-id="14132-114">To complete this tutorial, make sure you have the following prerequisites:</span></span>

* <span data-ttu-id="14132-115">Read through the [Event Hubs for Apache Kafka](event-hubs-for-kafka-ecosystem-overview.md) article.</span><span class="sxs-lookup"><span data-stu-id="14132-115">Read through the [Event Hubs for Apache Kafka](event-hubs-for-kafka-ecosystem-overview.md) article.</span></span> 
* <span data-ttu-id="14132-116">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="14132-116">An Azure subscription.</span></span> <span data-ttu-id="14132-117">If you do not have one, create a [free account](https://azure.microsoft.com/free/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio) before you begin.</span><span class="sxs-lookup"><span data-stu-id="14132-117">If you do not have one, create a [free account](https://azure.microsoft.com/free/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio) before you begin.</span></span>
* [<span data-ttu-id="14132-118">Java Development Kit (JDK) 1.7+</span><span class="sxs-lookup"><span data-stu-id="14132-118">Java Development Kit (JDK) 1.7+</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/index.html)
    * <span data-ttu-id="14132-119">On Ubuntu, run `apt-get install default-jdk` to install the JDK.</span><span class="sxs-lookup"><span data-stu-id="14132-119">On Ubuntu, run `apt-get install default-jdk` to install the JDK.</span></span>
    * <span data-ttu-id="14132-120">Be sure to set the JAVA_HOME environment variable to point to the folder where the JDK is installed.</span><span class="sxs-lookup"><span data-stu-id="14132-120">Be sure to set the JAVA_HOME environment variable to point to the folder where the JDK is installed.</span></span>
* <span data-ttu-id="14132-121">[Download](http://maven.apache.org/download.cgi) and [install](http://maven.apache.org/install.html) a Maven binary archive</span><span class="sxs-lookup"><span data-stu-id="14132-121">[Download](http://maven.apache.org/download.cgi) and [install](http://maven.apache.org/install.html) a Maven binary archive</span></span>
    * <span data-ttu-id="14132-122">On Ubuntu, you can run `apt-get install maven` to install Maven.</span><span class="sxs-lookup"><span data-stu-id="14132-122">On Ubuntu, you can run `apt-get install maven` to install Maven.</span></span>
* [<span data-ttu-id="14132-123">Git</span><span class="sxs-lookup"><span data-stu-id="14132-123">Git</span></span>](https://www.git-scm.com/downloads)
    * <span data-ttu-id="14132-124">On Ubuntu, you can run `sudo apt-get install git` to install Git.</span><span class="sxs-lookup"><span data-stu-id="14132-124">On Ubuntu, you can run `sudo apt-get install git` to install Git.</span></span>

## <a name="create-an-event-hubs-namespace"></a><span data-ttu-id="14132-125">Create an Event Hubs namespace</span><span class="sxs-lookup"><span data-stu-id="14132-125">Create an Event Hubs namespace</span></span>

<span data-ttu-id="14132-126">An Event Hubs namespace is required to send or receive from any Event Hubs service.</span><span class="sxs-lookup"><span data-stu-id="14132-126">An Event Hubs namespace is required to send or receive from any Event Hubs service.</span></span> <span data-ttu-id="14132-127">See [Create Kafka Enabled Event Hubs](event-hubs-create-kafka-enabled.md) for information about getting an Event Hubs Kafka endpoint.</span><span class="sxs-lookup"><span data-stu-id="14132-127">See [Create Kafka Enabled Event Hubs](event-hubs-create-kafka-enabled.md) for information about getting an Event Hubs Kafka endpoint.</span></span> <span data-ttu-id="14132-128">Make sure to copy the Event Hubs connection string for later use.</span><span class="sxs-lookup"><span data-stu-id="14132-128">Make sure to copy the Event Hubs connection string for later use.</span></span>

## <a name="clone-the-example-project"></a><span data-ttu-id="14132-129">Clone the example project</span><span class="sxs-lookup"><span data-stu-id="14132-129">Clone the example project</span></span>

<span data-ttu-id="14132-130">Now that you have a Kafka-enabled Event Hubs connection string, clone the Azure Event Hubs repository and navigate to the `flink` subfolder:</span><span class="sxs-lookup"><span data-stu-id="14132-130">Now that you have a Kafka-enabled Event Hubs connection string, clone the Azure Event Hubs repository and navigate to the `flink` subfolder:</span></span>

```shell
git clone https://github.com/Azure/azure-event-hubs.git
cd azure-event-hubs/samples/kafka/flink
```

## <a name="run-flink-producer"></a><span data-ttu-id="14132-131">Run Flink producer</span><span class="sxs-lookup"><span data-stu-id="14132-131">Run Flink producer</span></span>

<span data-ttu-id="14132-132">Using the provided Flink producer example, send messages to the Event Hubs service.</span><span class="sxs-lookup"><span data-stu-id="14132-132">Using the provided Flink producer example, send messages to the Event Hubs service.</span></span>

### <a name="provide-an-event-hubs-kafka-endpoint"></a><span data-ttu-id="14132-133">Provide an Event Hubs Kafka endpoint</span><span class="sxs-lookup"><span data-stu-id="14132-133">Provide an Event Hubs Kafka endpoint</span></span>

#### <a name="producerconfig"></a><span data-ttu-id="14132-134">producer.config</span><span class="sxs-lookup"><span data-stu-id="14132-134">producer.config</span></span>

<span data-ttu-id="14132-135">Update the `bootstrap.servers` and `sasl.jaas.config` values in `producer/src/main/resources/producer.config` to direct the producer to the Event Hubs Kafka endpoint with the correct authentication.</span><span class="sxs-lookup"><span data-stu-id="14132-135">Update the `bootstrap.servers` and `sasl.jaas.config` values in `producer/src/main/resources/producer.config` to direct the producer to the Event Hubs Kafka endpoint with the correct authentication.</span></span>

```xml
bootstrap.servers={YOUR.EVENTHUBS.FQDN}:9093
client.id=FlinkExampleProducer
sasl.mechanism=PLAIN
security.protocol=SASL_SSL
sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required \
   username="$ConnectionString" \
   password="{YOUR.EVENTHUBS.CONNECTION.STRING}";
```

### <a name="run-producer-from-the-command-line"></a><span data-ttu-id="14132-136">Run producer from the command line</span><span class="sxs-lookup"><span data-stu-id="14132-136">Run producer from the command line</span></span>

<span data-ttu-id="14132-137">To run the producer from the command line, generate the JAR and then run from within Maven (or generate the JAR using Maven, then run in Java by adding the necessary Kafka JAR(s) to the classpath):</span><span class="sxs-lookup"><span data-stu-id="14132-137">To run the producer from the command line, generate the JAR and then run from within Maven (or generate the JAR using Maven, then run in Java by adding the necessary Kafka JAR(s) to the classpath):</span></span>

```shell
mvn clean package
mvn exec:java -Dexec.mainClass="FlinkTestProducer"
```

<span data-ttu-id="14132-138">The producer will now begin sending events to the Kafka enabled Event Hub at topic `test` and printing the events to stdout.</span><span class="sxs-lookup"><span data-stu-id="14132-138">The producer will now begin sending events to the Kafka enabled Event Hub at topic `test` and printing the events to stdout.</span></span>

## <a name="run-flink-consumer"></a><span data-ttu-id="14132-139">Run Flink consumer</span><span class="sxs-lookup"><span data-stu-id="14132-139">Run Flink consumer</span></span>

<span data-ttu-id="14132-140">Using the provided consumer example, receive messages from the Kafka enabled Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="14132-140">Using the provided consumer example, receive messages from the Kafka enabled Event Hubs.</span></span>

### <a name="provide-an-event-hubs-kafka-endpoint"></a><span data-ttu-id="14132-141">Provide an Event Hubs Kafka endpoint</span><span class="sxs-lookup"><span data-stu-id="14132-141">Provide an Event Hubs Kafka endpoint</span></span>

#### <a name="consumerconfig"></a><span data-ttu-id="14132-142">consumer.config</span><span class="sxs-lookup"><span data-stu-id="14132-142">consumer.config</span></span>

<span data-ttu-id="14132-143">Update the `bootstrap.servers` and `sasl.jaas.config` values in `consumer/src/main/resources/consumer.config` to direct the consumer to the Event Hubs Kafka endpoint with the correct authentication.</span><span class="sxs-lookup"><span data-stu-id="14132-143">Update the `bootstrap.servers` and `sasl.jaas.config` values in `consumer/src/main/resources/consumer.config` to direct the consumer to the Event Hubs Kafka endpoint with the correct authentication.</span></span>

```xml
bootstrap.servers={YOUR.EVENTHUBS.FQDN}:9093
group.id=FlinkExampleConsumer
sasl.mechanism=PLAIN
security.protocol=SASL_SSL
sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required \
   username="$ConnectionString" \
   password="{YOUR.EVENTHUBS.CONNECTION.STRING}";
```

### <a name="run-consumer-from-the-command-line"></a><span data-ttu-id="14132-144">Run consumer from the command line</span><span class="sxs-lookup"><span data-stu-id="14132-144">Run consumer from the command line</span></span>

<span data-ttu-id="14132-145">To run the consumer from the command line, generate the JAR and then run from within Maven (or generate the JAR using Maven, then run in Java by adding the necessary Kafka JAR(s) to the classpath):</span><span class="sxs-lookup"><span data-stu-id="14132-145">To run the consumer from the command line, generate the JAR and then run from within Maven (or generate the JAR using Maven, then run in Java by adding the necessary Kafka JAR(s) to the classpath):</span></span>

```shell
mvn clean package
mvn exec:java -Dexec.mainClass="FlinkTestConsumer"
```

<span data-ttu-id="14132-146">If the Kafka-enabled event hub has events (for example, if your producer is also running), then the consumer now begins receiving events from the topic `test`.</span><span class="sxs-lookup"><span data-stu-id="14132-146">If the Kafka-enabled event hub has events (for example, if your producer is also running), then the consumer now begins receiving events from the topic `test`.</span></span>

<span data-ttu-id="14132-147">Check out [Flink's Kafka Connector Guide](https://ci.apache.org/projects/flink/flink-docs-stable/dev/connectors/kafka.html) for more detailed information about connecting Flink to Kafka.</span><span class="sxs-lookup"><span data-stu-id="14132-147">Check out [Flink's Kafka Connector Guide](https://ci.apache.org/projects/flink/flink-docs-stable/dev/connectors/kafka.html) for more detailed information about connecting Flink to Kafka.</span></span>

## <a name="next-steps"></a><span data-ttu-id="14132-148">Next steps</span><span class="sxs-lookup"><span data-stu-id="14132-148">Next steps</span></span>
<span data-ttu-id="14132-149">In this tutorial, your learned how to connect Apache Flink to Kafka-enabled event hubs without changing your protocol clients or running your own clusters.</span><span class="sxs-lookup"><span data-stu-id="14132-149">In this tutorial, your learned how to connect Apache Flink to Kafka-enabled event hubs without changing your protocol clients or running your own clusters.</span></span> <span data-ttu-id="14132-150">You performed the following steps as part of this tutorial:</span><span class="sxs-lookup"><span data-stu-id="14132-150">You performed the following steps as part of this tutorial:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="14132-151">Create an Event Hubs namespace</span><span class="sxs-lookup"><span data-stu-id="14132-151">Create an Event Hubs namespace</span></span>
> * <span data-ttu-id="14132-152">Clone the example project</span><span class="sxs-lookup"><span data-stu-id="14132-152">Clone the example project</span></span>
> * <span data-ttu-id="14132-153">Run Flink producer</span><span class="sxs-lookup"><span data-stu-id="14132-153">Run Flink producer</span></span> 
> * <span data-ttu-id="14132-154">Run Flink consumer</span><span class="sxs-lookup"><span data-stu-id="14132-154">Run Flink consumer</span></span>

<span data-ttu-id="14132-155">Advance to the next article to learn more about Event Hubs for Apache Kafka:</span><span class="sxs-lookup"><span data-stu-id="14132-155">Advance to the next article to learn more about Event Hubs for Apache Kafka:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="14132-156">Use Akka Streams with Azure Event Hubs for Kafka</span><span class="sxs-lookup"><span data-stu-id="14132-156">Use Akka Streams with Azure Event Hubs for Kafka</span></span>](event-hubs-kafka-akka-streams-tutorial.md)