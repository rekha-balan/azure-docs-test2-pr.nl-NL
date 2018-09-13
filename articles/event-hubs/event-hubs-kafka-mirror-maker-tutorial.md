---
title: Use Apache Kafka MirrorMaker with Azure Event Hubs for Kafka Ecosystem | Microsoft Docs
description: Use Kafka MirrorMaker to mirror a Kafka cluster in Event Hubs.
services: event-hubs
documentationcenter: .net
author: basilhariri
manager: timlt
ms.service: event-hubs
ms.topic: mirror-maker
ms.custom: mvc
ms.date: 08/07/2018
ms.author: bahariri
ms.openlocfilehash: f3881d4448f44d44515ddb25072401d775d69b90
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857593"
---
# <a name="use-kafka-mirrormaker-with-event-hubs-for-apache-kafka"></a><span data-ttu-id="4ed54-103">Use Kafka MirrorMaker with Event Hubs for Apache Kafka</span><span class="sxs-lookup"><span data-stu-id="4ed54-103">Use Kafka MirrorMaker with Event Hubs for Apache Kafka</span></span>

<span data-ttu-id="4ed54-104">This tutorial shows how to mirror a Kafka broker in a Kafka enabled event hub using Kafka MirrorMaker.</span><span class="sxs-lookup"><span data-stu-id="4ed54-104">This tutorial shows how to mirror a Kafka broker in a Kafka enabled event hub using Kafka MirrorMaker.</span></span>

   ![Kafka MirrorMaker with Event Hubs](./media/event-hubs-kafka-mirror-maker-tutorial/evnent-hubs-mirror-maker1.png)

> [!NOTE]
> <span data-ttu-id="4ed54-106">This sample is available on [GitHub](https://github.com/Azure/azure-event-hubs)</span><span class="sxs-lookup"><span data-stu-id="4ed54-106">This sample is available on [GitHub](https://github.com/Azure/azure-event-hubs)</span></span>


<span data-ttu-id="4ed54-107">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="4ed54-107">In this tutorial, you learn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="4ed54-108">Create an Event Hubs namespace</span><span class="sxs-lookup"><span data-stu-id="4ed54-108">Create an Event Hubs namespace</span></span>
> * <span data-ttu-id="4ed54-109">Clone the example project</span><span class="sxs-lookup"><span data-stu-id="4ed54-109">Clone the example project</span></span>
> * <span data-ttu-id="4ed54-110">Set up a Kafka cluster</span><span class="sxs-lookup"><span data-stu-id="4ed54-110">Set up a Kafka cluster</span></span>
> * <span data-ttu-id="4ed54-111">Configure Kafka MirrorMaker</span><span class="sxs-lookup"><span data-stu-id="4ed54-111">Configure Kafka MirrorMaker</span></span>
> * <span data-ttu-id="4ed54-112">Run Kafka MirrorMaker</span><span class="sxs-lookup"><span data-stu-id="4ed54-112">Run Kafka MirrorMaker</span></span>

## <a name="introduction"></a><span data-ttu-id="4ed54-113">Introduction</span><span class="sxs-lookup"><span data-stu-id="4ed54-113">Introduction</span></span>
<span data-ttu-id="4ed54-114">One major consideration for modern cloud scale apps is the ability to update, improve, and change infrastructure without interrupting service.</span><span class="sxs-lookup"><span data-stu-id="4ed54-114">One major consideration for modern cloud scale apps is the ability to update, improve, and change infrastructure without interrupting service.</span></span> <span data-ttu-id="4ed54-115">This tutorial shows how a Kafka-enabled event hub and Kafka MirrorMaker can integrate an existing Kafka pipeline into Azure by "mirroring" the Kafka input stream in the Event Hubs service.</span><span class="sxs-lookup"><span data-stu-id="4ed54-115">This tutorial shows how a Kafka-enabled event hub and Kafka MirrorMaker can integrate an existing Kafka pipeline into Azure by "mirroring" the Kafka input stream in the Event Hubs service.</span></span> 

<span data-ttu-id="4ed54-116">An Azure Event Hubs Kafka endpoint enables you to connect to Azure Event Hubs using the Kafka protocol (that is, Kafka clients).</span><span class="sxs-lookup"><span data-stu-id="4ed54-116">An Azure Event Hubs Kafka endpoint enables you to connect to Azure Event Hubs using the Kafka protocol (that is, Kafka clients).</span></span> <span data-ttu-id="4ed54-117">By making minimal changes to a Kafka application, you can connect to Azure Event Hubs and enjoy the benefits of the Azure ecosystem.</span><span class="sxs-lookup"><span data-stu-id="4ed54-117">By making minimal changes to a Kafka application, you can connect to Azure Event Hubs and enjoy the benefits of the Azure ecosystem.</span></span> <span data-ttu-id="4ed54-118">Kafka enabled Event Hubs currently supports Kafka versions 1.0 and later.</span><span class="sxs-lookup"><span data-stu-id="4ed54-118">Kafka enabled Event Hubs currently supports Kafka versions 1.0 and later.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4ed54-119">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="4ed54-119">Prerequisites</span></span>

<span data-ttu-id="4ed54-120">To complete this tutorial, make sure you have:</span><span class="sxs-lookup"><span data-stu-id="4ed54-120">To complete this tutorial, make sure you have:</span></span>

* <span data-ttu-id="4ed54-121">Read through the [Event Hubs for Apache Kafka](event-hubs-for-kafka-ecosystem-overview.md) article.</span><span class="sxs-lookup"><span data-stu-id="4ed54-121">Read through the [Event Hubs for Apache Kafka](event-hubs-for-kafka-ecosystem-overview.md) article.</span></span> 
* <span data-ttu-id="4ed54-122">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="4ed54-122">An Azure subscription.</span></span> <span data-ttu-id="4ed54-123">If you do not have one, create a [free account](https://azure.microsoft.com/free/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio) before you begin.</span><span class="sxs-lookup"><span data-stu-id="4ed54-123">If you do not have one, create a [free account](https://azure.microsoft.com/free/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio) before you begin.</span></span>
* [<span data-ttu-id="4ed54-124">Java Development Kit (JDK) 1.7+</span><span class="sxs-lookup"><span data-stu-id="4ed54-124">Java Development Kit (JDK) 1.7+</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/index.html)
    * <span data-ttu-id="4ed54-125">On Ubuntu, run `apt-get install default-jdk` to install the JDK.</span><span class="sxs-lookup"><span data-stu-id="4ed54-125">On Ubuntu, run `apt-get install default-jdk` to install the JDK.</span></span>
    * <span data-ttu-id="4ed54-126">Be sure to set the JAVA_HOME environment variable to point to the folder where the JDK is installed.</span><span class="sxs-lookup"><span data-stu-id="4ed54-126">Be sure to set the JAVA_HOME environment variable to point to the folder where the JDK is installed.</span></span>
* <span data-ttu-id="4ed54-127">[Download](http://maven.apache.org/download.cgi) and [install](http://maven.apache.org/install.html) a Maven binary archive</span><span class="sxs-lookup"><span data-stu-id="4ed54-127">[Download](http://maven.apache.org/download.cgi) and [install](http://maven.apache.org/install.html) a Maven binary archive</span></span>
    * <span data-ttu-id="4ed54-128">On Ubuntu, you can run `apt-get install maven` to install Maven.</span><span class="sxs-lookup"><span data-stu-id="4ed54-128">On Ubuntu, you can run `apt-get install maven` to install Maven.</span></span>
* [<span data-ttu-id="4ed54-129">Git</span><span class="sxs-lookup"><span data-stu-id="4ed54-129">Git</span></span>](https://www.git-scm.com/downloads)
    * <span data-ttu-id="4ed54-130">On Ubuntu, you can run `sudo apt-get install git` to install Git.</span><span class="sxs-lookup"><span data-stu-id="4ed54-130">On Ubuntu, you can run `sudo apt-get install git` to install Git.</span></span>

## <a name="create-an-event-hubs-namespace"></a><span data-ttu-id="4ed54-131">Create an Event Hubs namespace</span><span class="sxs-lookup"><span data-stu-id="4ed54-131">Create an Event Hubs namespace</span></span>

<span data-ttu-id="4ed54-132">An Event Hubs namespace is required to send and receive from any Event Hubs service.</span><span class="sxs-lookup"><span data-stu-id="4ed54-132">An Event Hubs namespace is required to send and receive from any Event Hubs service.</span></span> <span data-ttu-id="4ed54-133">See [Creating a Kafka enabled Event Hub](event-hubs-create.md) for instructions on getting an Event Hubs Kafka endpoint.</span><span class="sxs-lookup"><span data-stu-id="4ed54-133">See [Creating a Kafka enabled Event Hub](event-hubs-create.md) for instructions on getting an Event Hubs Kafka endpoint.</span></span> <span data-ttu-id="4ed54-134">Make sure to copy the Event Hubs connection string for later use.</span><span class="sxs-lookup"><span data-stu-id="4ed54-134">Make sure to copy the Event Hubs connection string for later use.</span></span>

## <a name="clone-the-example-project"></a><span data-ttu-id="4ed54-135">Clone the example project</span><span class="sxs-lookup"><span data-stu-id="4ed54-135">Clone the example project</span></span>

<span data-ttu-id="4ed54-136">Now that you have a Kafka enabled Event Hubs connection string, clone the Azure Event Hubs repository and navigate to the `mirror-maker` subfolder:</span><span class="sxs-lookup"><span data-stu-id="4ed54-136">Now that you have a Kafka enabled Event Hubs connection string, clone the Azure Event Hubs repository and navigate to the `mirror-maker` subfolder:</span></span>

```shell
git clone https://github.com/Azure/azure-event-hubs.git
cd azure-event-hubs/samples/kafka/mirror-maker
```

## <a name="set-up-a-kafka-cluster"></a><span data-ttu-id="4ed54-137">Set up a Kafka cluster</span><span class="sxs-lookup"><span data-stu-id="4ed54-137">Set up a Kafka cluster</span></span>

<span data-ttu-id="4ed54-138">Use the [Kafka quickstart guide](https://kafka.apache.org/quickstart) to set up a cluster with the desired settings (or use an existing Kafka cluster).</span><span class="sxs-lookup"><span data-stu-id="4ed54-138">Use the [Kafka quickstart guide](https://kafka.apache.org/quickstart) to set up a cluster with the desired settings (or use an existing Kafka cluster).</span></span>

## <a name="configure-kafka-mirrormaker"></a><span data-ttu-id="4ed54-139">Configure Kafka MirrorMaker</span><span class="sxs-lookup"><span data-stu-id="4ed54-139">Configure Kafka MirrorMaker</span></span>

<span data-ttu-id="4ed54-140">Kafka MirrorMaker enables the "mirroring" of a stream.</span><span class="sxs-lookup"><span data-stu-id="4ed54-140">Kafka MirrorMaker enables the "mirroring" of a stream.</span></span> <span data-ttu-id="4ed54-141">Given source and destination Kafka clusters, MirrorMaker ensures any messages sent to the source cluster are received by both the source and destination clusters.</span><span class="sxs-lookup"><span data-stu-id="4ed54-141">Given source and destination Kafka clusters, MirrorMaker ensures any messages sent to the source cluster are received by both the source and destination clusters.</span></span> <span data-ttu-id="4ed54-142">This example shows how to mirror a source Kafka cluster with a destination Kafka-enabled event hub.</span><span class="sxs-lookup"><span data-stu-id="4ed54-142">This example shows how to mirror a source Kafka cluster with a destination Kafka-enabled event hub.</span></span> <span data-ttu-id="4ed54-143">This scenario can be used to send data from an existing Kafka pipeline to Event Hubs without interrupting the flow of data.</span><span class="sxs-lookup"><span data-stu-id="4ed54-143">This scenario can be used to send data from an existing Kafka pipeline to Event Hubs without interrupting the flow of data.</span></span> 

<span data-ttu-id="4ed54-144">For more detailed information on Kafka MirrorMaker, see the [Kafka Mirroring/MirrorMaker guide](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=27846330).</span><span class="sxs-lookup"><span data-stu-id="4ed54-144">For more detailed information on Kafka MirrorMaker, see the [Kafka Mirroring/MirrorMaker guide](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=27846330).</span></span>

<span data-ttu-id="4ed54-145">To configure Kafka MirrorMaker, give it a Kafka cluster as its consumer/source and a Kafka-enabled event hub as its producer/destination.</span><span class="sxs-lookup"><span data-stu-id="4ed54-145">To configure Kafka MirrorMaker, give it a Kafka cluster as its consumer/source and a Kafka-enabled event hub as its producer/destination.</span></span>

#### <a name="consumer-configuration"></a><span data-ttu-id="4ed54-146">Consumer configuration</span><span class="sxs-lookup"><span data-stu-id="4ed54-146">Consumer configuration</span></span>

<span data-ttu-id="4ed54-147">Update the consumer configuration file `source-kafka.config`, which tells MirrorMaker the properties of the source Kafka cluster.</span><span class="sxs-lookup"><span data-stu-id="4ed54-147">Update the consumer configuration file `source-kafka.config`, which tells MirrorMaker the properties of the source Kafka cluster.</span></span>

##### <a name="source-kafkaconfig"></a><span data-ttu-id="4ed54-148">source-kafka.config</span><span class="sxs-lookup"><span data-stu-id="4ed54-148">source-kafka.config</span></span>

```xml
bootstrap.servers={SOURCE.KAFKA.IP.ADDRESS1}:{SOURCE.KAFKA.PORT1},{SOURCE.KAFKA.IP.ADDRESS2}:{SOURCE.KAFKA.PORT2},etc
group.id=example-mirrormaker-group
exclude.internal.topics=true
client.id=mirror_maker_consumer
```

#### <a name="producer-configuration"></a><span data-ttu-id="4ed54-149">Producer configuration</span><span class="sxs-lookup"><span data-stu-id="4ed54-149">Producer configuration</span></span>

<span data-ttu-id="4ed54-150">Now update the producer configuration file `mirror-eventhub.config`, which tells MirrorMaker to send the duplicated (or "mirrored") data to the Event Hubs service.</span><span class="sxs-lookup"><span data-stu-id="4ed54-150">Now update the producer configuration file `mirror-eventhub.config`, which tells MirrorMaker to send the duplicated (or "mirrored") data to the Event Hubs service.</span></span> <span data-ttu-id="4ed54-151">Specifically, change `bootstrap.servers` and `sasl.jaas.config` to point to your Event Hubs Kafka endpoint.</span><span class="sxs-lookup"><span data-stu-id="4ed54-151">Specifically, change `bootstrap.servers` and `sasl.jaas.config` to point to your Event Hubs Kafka endpoint.</span></span> <span data-ttu-id="4ed54-152">The Event Hubs service requires secure (SASL) communication, which is achieved by setting the last three properties in the following configuration:</span><span class="sxs-lookup"><span data-stu-id="4ed54-152">The Event Hubs service requires secure (SASL) communication, which is achieved by setting the last three properties in the following configuration:</span></span> 

##### <a name="mirror-eventhubconfig"></a><span data-ttu-id="4ed54-153">mirror-eventhub.config</span><span class="sxs-lookup"><span data-stu-id="4ed54-153">mirror-eventhub.config</span></span>

```xml
bootstrap.servers={YOUR.EVENTHUBS.FQDN}:9093
client.id=mirror_maker_producer

#Required for Event Hubs
sasl.mechanism=PLAIN
security.protocol=SASL_SSL
sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required username="$ConnectionString" password="{YOUR.EVENTHUBS.CONNECTION.STRING}";
```

## <a name="run-kafka-mirrormaker"></a><span data-ttu-id="4ed54-154">Run Kafka MirrorMaker</span><span class="sxs-lookup"><span data-stu-id="4ed54-154">Run Kafka MirrorMaker</span></span>

<span data-ttu-id="4ed54-155">Run the Kafka MirrorMaker script from the root Kafka directory using the newly updated configuration files.</span><span class="sxs-lookup"><span data-stu-id="4ed54-155">Run the Kafka MirrorMaker script from the root Kafka directory using the newly updated configuration files.</span></span> <span data-ttu-id="4ed54-156">Make sure to either copy the config files to the root Kafka directory, or update their paths in the following command.</span><span class="sxs-lookup"><span data-stu-id="4ed54-156">Make sure to either copy the config files to the root Kafka directory, or update their paths in the following command.</span></span>

```shell
bin/kafka-mirror-maker.sh --consumer.config source-kafka.config --num.streams 1 --producer.config mirror-eventhub.config --whitelist=".*"
```

<span data-ttu-id="4ed54-157">To verify that events are reaching the Kafka-enabled event hub, see the ingress statistics in the [Azure portal](https://azure.microsoft.com/features/azure-portal/), or run a consumer against the event hub.</span><span class="sxs-lookup"><span data-stu-id="4ed54-157">To verify that events are reaching the Kafka-enabled event hub, see the ingress statistics in the [Azure portal](https://azure.microsoft.com/features/azure-portal/), or run a consumer against the event hub.</span></span>

<span data-ttu-id="4ed54-158">With MirrorMaker running, any events sent to the source Kafka cluster are received by both the Kafka cluster and the mirrored Kafka enabled event hub service.</span><span class="sxs-lookup"><span data-stu-id="4ed54-158">With MirrorMaker running, any events sent to the source Kafka cluster are received by both the Kafka cluster and the mirrored Kafka enabled event hub service.</span></span> <span data-ttu-id="4ed54-159">By using MirrorMaker and an Event Hubs Kafka endpoint, you can migrate an existing Kafka pipeline to the managed Azure Event Hubs service without changing the existing cluster or interrupting any ongoing data flow.</span><span class="sxs-lookup"><span data-stu-id="4ed54-159">By using MirrorMaker and an Event Hubs Kafka endpoint, you can migrate an existing Kafka pipeline to the managed Azure Event Hubs service without changing the existing cluster or interrupting any ongoing data flow.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4ed54-160">Next steps</span><span class="sxs-lookup"><span data-stu-id="4ed54-160">Next steps</span></span>

<span data-ttu-id="4ed54-161">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="4ed54-161">In this tutorial, you learn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="4ed54-162">Create an Event Hubs namespace</span><span class="sxs-lookup"><span data-stu-id="4ed54-162">Create an Event Hubs namespace</span></span>
> * <span data-ttu-id="4ed54-163">Clone the example project</span><span class="sxs-lookup"><span data-stu-id="4ed54-163">Clone the example project</span></span>
> * <span data-ttu-id="4ed54-164">Set up a Kafka cluster</span><span class="sxs-lookup"><span data-stu-id="4ed54-164">Set up a Kafka cluster</span></span>
> * <span data-ttu-id="4ed54-165">Configure Kafka MirrorMaker</span><span class="sxs-lookup"><span data-stu-id="4ed54-165">Configure Kafka MirrorMaker</span></span>
> * <span data-ttu-id="4ed54-166">Run Kafka MirrorMaker</span><span class="sxs-lookup"><span data-stu-id="4ed54-166">Run Kafka MirrorMaker</span></span>

<span data-ttu-id="4ed54-167">Advance to the next article to learn more about Event Hubs for Apache Kafka:</span><span class="sxs-lookup"><span data-stu-id="4ed54-167">Advance to the next article to learn more about Event Hubs for Apache Kafka:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4ed54-168">Use Apache Flink with Azure Event Hubs for Kafka</span><span class="sxs-lookup"><span data-stu-id="4ed54-168">Use Apache Flink with Azure Event Hubs for Kafka</span></span>](event-hubs-kafka-flink-tutorial.md)