---
title: Stream into Azure Event Hubs for Apache Kafka | Microsoft Docs
description: Stream into Event Hubs using the Kafka protocol and APIs.
services: event-hubs
documentationcenter: ''
author: basilhariri
manager: timlt
ms.service: event-hubs
ms.devlang: na
ms.topic: quickstart
ms.custom: mvc
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2018
ms.author: bahariri
ms.openlocfilehash: 90d9f3620f954da42add08a0aebf779a95c7e7a3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965656"
---
# <a name="stream-into-event-hubs-for-the-apache-kafka"></a><span data-ttu-id="8cc36-103">Stream into Event Hubs for the Apache Kafka</span><span class="sxs-lookup"><span data-stu-id="8cc36-103">Stream into Event Hubs for the Apache Kafka</span></span>
<span data-ttu-id="8cc36-104">This quickstart shows how to stream into Kafka-enabled Event Hubs without changing your protocol clients or running your own clusters.</span><span class="sxs-lookup"><span data-stu-id="8cc36-104">This quickstart shows how to stream into Kafka-enabled Event Hubs without changing your protocol clients or running your own clusters.</span></span> <span data-ttu-id="8cc36-105">You learn how to use your producers and consumers to talk to Kafka-enabled Event Hubs with just a configuration change in your applications.</span><span class="sxs-lookup"><span data-stu-id="8cc36-105">You learn how to use your producers and consumers to talk to Kafka-enabled Event Hubs with just a configuration change in your applications.</span></span> <span data-ttu-id="8cc36-106">Azure Event Hubs supports [Apache Kafka version 1.0.](https://kafka.apache.org/10/documentation.html)</span><span class="sxs-lookup"><span data-stu-id="8cc36-106">Azure Event Hubs supports [Apache Kafka version 1.0.](https://kafka.apache.org/10/documentation.html)</span></span>

> [!NOTE]
> <span data-ttu-id="8cc36-107">This sample is available on [GitHub](https://github.com/Azure/azure-event-hubs)</span><span class="sxs-lookup"><span data-stu-id="8cc36-107">This sample is available on [GitHub](https://github.com/Azure/azure-event-hubs)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8cc36-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="8cc36-108">Prerequisites</span></span>

<span data-ttu-id="8cc36-109">To complete this quickstart, make sure you have the following prerequisites:</span><span class="sxs-lookup"><span data-stu-id="8cc36-109">To complete this quickstart, make sure you have the following prerequisites:</span></span>

* <span data-ttu-id="8cc36-110">Read through the [Event Hubs for Apache Kafka](event-hubs-for-kafka-ecosystem-overview.md) article.</span><span class="sxs-lookup"><span data-stu-id="8cc36-110">Read through the [Event Hubs for Apache Kafka](event-hubs-for-kafka-ecosystem-overview.md) article.</span></span>
* <span data-ttu-id="8cc36-111">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="8cc36-111">An Azure subscription.</span></span> <span data-ttu-id="8cc36-112">If you do not have one, create a [free account](https://azure.microsoft.com/free/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio) before you begin.</span><span class="sxs-lookup"><span data-stu-id="8cc36-112">If you do not have one, create a [free account](https://azure.microsoft.com/free/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio) before you begin.</span></span>
* <span data-ttu-id="8cc36-113">[Java Development Kit (JDK) 1.7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="8cc36-113">[Java Development Kit (JDK) 1.7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span>
* <span data-ttu-id="8cc36-114">[Download](http://maven.apache.org/download.cgi) and [install](http://maven.apache.org/install.html) a Maven binary archive.</span><span class="sxs-lookup"><span data-stu-id="8cc36-114">[Download](http://maven.apache.org/download.cgi) and [install](http://maven.apache.org/install.html) a Maven binary archive.</span></span>
* [<span data-ttu-id="8cc36-115">Git</span><span class="sxs-lookup"><span data-stu-id="8cc36-115">Git</span></span>](https://www.git-scm.com/)
* [<span data-ttu-id="8cc36-116">A Kafka enabled Event Hubs namespace</span><span class="sxs-lookup"><span data-stu-id="8cc36-116">A Kafka enabled Event Hubs namespace</span></span>](event-hubs-create.md)

## <a name="create-a-kafka-enabled-event-hubs-namespace"></a><span data-ttu-id="8cc36-117">Create a Kafka enabled Event Hubs namespace</span><span class="sxs-lookup"><span data-stu-id="8cc36-117">Create a Kafka enabled Event Hubs namespace</span></span>

1. <span data-ttu-id="8cc36-118">Sign in to the [Azure portal][Azure portal], and click **Create a resource** at the top left of the screen.</span><span class="sxs-lookup"><span data-stu-id="8cc36-118">Sign in to the [Azure portal][Azure portal], and click **Create a resource** at the top left of the screen.</span></span>

2. <span data-ttu-id="8cc36-119">Search for Event Hubs and select the options shown here:</span><span class="sxs-lookup"><span data-stu-id="8cc36-119">Search for Event Hubs and select the options shown here:</span></span>
    
    ![Search for Event Hubs in the portal](./media/event-hubs-create-kafka-enabled/event-hubs-create-event-hubs.png)
 
3. <span data-ttu-id="8cc36-121">Provide a unique name and enable Kafka on the namespace.</span><span class="sxs-lookup"><span data-stu-id="8cc36-121">Provide a unique name and enable Kafka on the namespace.</span></span> <span data-ttu-id="8cc36-122">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="8cc36-122">Click **Create**.</span></span>
    
    ![Create a namespace](./media/event-hubs-create-kafka-enabled/create-kafka-namespace.png)
 
4. <span data-ttu-id="8cc36-124">Once the namespace is created, on the **Settings** tab click **Shared access policies** to get the connection string.</span><span class="sxs-lookup"><span data-stu-id="8cc36-124">Once the namespace is created, on the **Settings** tab click **Shared access policies** to get the connection string.</span></span>

    ![Click Shared access policies](./media/event-hubs-create/create-event-hub7.png)

5. <span data-ttu-id="8cc36-126">You can choose the default **RootManageSharedAccessKey**, or add a new policy.</span><span class="sxs-lookup"><span data-stu-id="8cc36-126">You can choose the default **RootManageSharedAccessKey**, or add a new policy.</span></span> <span data-ttu-id="8cc36-127">Click the policy name and copy the connection string.</span><span class="sxs-lookup"><span data-stu-id="8cc36-127">Click the policy name and copy the connection string.</span></span> 
    
    ![Select a policy](./media/event-hubs-create/create-event-hub8.png)
 
6. <span data-ttu-id="8cc36-129">Add this connection string to your Kafka application configuration.</span><span class="sxs-lookup"><span data-stu-id="8cc36-129">Add this connection string to your Kafka application configuration.</span></span>

<span data-ttu-id="8cc36-130">You can now stream events from your applications that use the Kafka protocol into Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="8cc36-130">You can now stream events from your applications that use the Kafka protocol into Event Hubs.</span></span>

## <a name="send-and-receive-messages-with-kafka-in-event-hubs"></a><span data-ttu-id="8cc36-131">Send and receive messages with Kafka in Event Hubs</span><span class="sxs-lookup"><span data-stu-id="8cc36-131">Send and receive messages with Kafka in Event Hubs</span></span>

1. <span data-ttu-id="8cc36-132">Clone the [Azure Event Hubs repository](https://github.com/Azure/azure-event-hubs).</span><span class="sxs-lookup"><span data-stu-id="8cc36-132">Clone the [Azure Event Hubs repository](https://github.com/Azure/azure-event-hubs).</span></span>

2. <span data-ttu-id="8cc36-133">Navigate to `azure-event-hubs/samples/kafka/quickstart/producer`.</span><span class="sxs-lookup"><span data-stu-id="8cc36-133">Navigate to `azure-event-hubs/samples/kafka/quickstart/producer`.</span></span>

3. <span data-ttu-id="8cc36-134">Update the configuration details for the producer in `src/main/resources/producer.config` as follows:</span><span class="sxs-lookup"><span data-stu-id="8cc36-134">Update the configuration details for the producer in `src/main/resources/producer.config` as follows:</span></span>

    ```xml
    bootstrap.servers={YOUR.EVENTHUBS.FQDN}:9093
    security.protocol=SASL_SSL
    sasl.mechanism=PLAIN
    sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required username="$ConnectionString" password="{YOUR.EVENTHUBS.CONNECTION.STRING}";
    ```
4. <span data-ttu-id="8cc36-135">Run the producer code and stream into Kafka-enabled Event Hubs:</span><span class="sxs-lookup"><span data-stu-id="8cc36-135">Run the producer code and stream into Kafka-enabled Event Hubs:</span></span>
   
    ```shell
    mvn clean package
    mvn exec:java -Dexec.mainClass="TestProducer"                                    
    ```
5. <span data-ttu-id="8cc36-136">Navigate to `azure-event-hubs/samples/kafka/quickstart/consumer`.</span><span class="sxs-lookup"><span data-stu-id="8cc36-136">Navigate to `azure-event-hubs/samples/kafka/quickstart/consumer`.</span></span>

6. <span data-ttu-id="8cc36-137">Update the configuration details for the consumer in `src/main/resources/consumer.config` as follows:</span><span class="sxs-lookup"><span data-stu-id="8cc36-137">Update the configuration details for the consumer in `src/main/resources/consumer.config` as follows:</span></span>
   
    ```xml
    bootstrap.servers={YOUR.EVENTHUBS.FQDN}:9093
    security.protocol=SASL_SSL
    sasl.mechanism=PLAIN
    sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required username="$ConnectionString" password="{YOUR.EVENTHUBS.CONNECTION.STRING}";
    ```

7. <span data-ttu-id="8cc36-138">Run the consumer code and process from Kafka enabled Event Hubs using your Kafka clients:</span><span class="sxs-lookup"><span data-stu-id="8cc36-138">Run the consumer code and process from Kafka enabled Event Hubs using your Kafka clients:</span></span>

    ```java
    mvn clean package
    mvn exec:java -Dexec.mainClass="TestConsumer"                                    
    ```

<span data-ttu-id="8cc36-139">If your Event Hubs Kafka cluster has events, you now start receiving them from the consumer.</span><span class="sxs-lookup"><span data-stu-id="8cc36-139">If your Event Hubs Kafka cluster has events, you now start receiving them from the consumer.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8cc36-140">Next steps</span><span class="sxs-lookup"><span data-stu-id="8cc36-140">Next steps</span></span>
<span data-ttu-id="8cc36-141">In this article, you learned how to stream into Kafka-enabled Event Hubs without changing your protocol clients or running your own clusters.</span><span class="sxs-lookup"><span data-stu-id="8cc36-141">In this article, you learned how to stream into Kafka-enabled Event Hubs without changing your protocol clients or running your own clusters.</span></span> <span data-ttu-id="8cc36-142">To learn more, continue with the following tutorial:</span><span class="sxs-lookup"><span data-stu-id="8cc36-142">To learn more, continue with the following tutorial:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="8cc36-143">Use Kafka MirrorMaker with Event Hubs</span><span class="sxs-lookup"><span data-stu-id="8cc36-143">Use Kafka MirrorMaker with Event Hubs</span></span>](event-hubs-kafka-mirror-maker-tutorial.md)
