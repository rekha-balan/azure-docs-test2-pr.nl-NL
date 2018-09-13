---
title: Use Apache Kafka on HDInsight with Azure IoT Hub
description: Learn how to use Apache Kafka on HDInsight with Azure IoT Hub. The Kafka Connect Azure IoT Hub project provides a source and sink connector for Kafka. The source connector can read data from IoT Hub, and the sink connector writes to IoT Hub.
services: hdinsight
ms.service: hdinsight
author: jasonwhowell
ms.author: jasonh
ms.reviewer: jasonh
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 05/15/2018
ms.openlocfilehash: 282fc6a1525238fba05c4f472b74d7eb55a49130
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857509"
---
# <a name="use-apache-kafka-on-hdinsight-with-azure-iot-hub"></a><span data-ttu-id="634fa-105">Use Apache Kafka on HDInsight with Azure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="634fa-105">Use Apache Kafka on HDInsight with Azure IoT Hub</span></span>

<span data-ttu-id="634fa-106">Learn how to use the [Kafka Connect Azure IoT Hub](https://github.com/Azure/toketi-kafka-connect-iothub) connector to move data between Apache Kafka on HDInsight and Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="634fa-106">Learn how to use the [Kafka Connect Azure IoT Hub](https://github.com/Azure/toketi-kafka-connect-iothub) connector to move data between Apache Kafka on HDInsight and Azure IoT Hub.</span></span> <span data-ttu-id="634fa-107">In this document, you learn how to run the IoT Hub connector from an edge node in the cluster.</span><span class="sxs-lookup"><span data-stu-id="634fa-107">In this document, you learn how to run the IoT Hub connector from an edge node in the cluster.</span></span>

<span data-ttu-id="634fa-108">The Kafka Connect API allows you to implement connectors that continuously pull data into Kafka, or push data from Kafka to another system.</span><span class="sxs-lookup"><span data-stu-id="634fa-108">The Kafka Connect API allows you to implement connectors that continuously pull data into Kafka, or push data from Kafka to another system.</span></span> <span data-ttu-id="634fa-109">The [Kafka Connect Azure IoT Hub](https://github.com/Azure/toketi-kafka-connect-iothub) is a connector that pulls data from Azure IoT Hub into Kafka.</span><span class="sxs-lookup"><span data-stu-id="634fa-109">The [Kafka Connect Azure IoT Hub](https://github.com/Azure/toketi-kafka-connect-iothub) is a connector that pulls data from Azure IoT Hub into Kafka.</span></span> <span data-ttu-id="634fa-110">It can also push data from Kafka to the IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="634fa-110">It can also push data from Kafka to the IoT Hub.</span></span> 

<span data-ttu-id="634fa-111">When pulling from the IoT Hub, you use a __source__ connector.</span><span class="sxs-lookup"><span data-stu-id="634fa-111">When pulling from the IoT Hub, you use a __source__ connector.</span></span> <span data-ttu-id="634fa-112">When pushing to IoT Hub, you use a __sink__ connector.</span><span class="sxs-lookup"><span data-stu-id="634fa-112">When pushing to IoT Hub, you use a __sink__ connector.</span></span> <span data-ttu-id="634fa-113">The IoT Hub connector provides both the source and sink connectors.</span><span class="sxs-lookup"><span data-stu-id="634fa-113">The IoT Hub connector provides both the source and sink connectors.</span></span>

<span data-ttu-id="634fa-114">The following diagram shows the data flow between Azure IoT Hub and Kafka on HDInsight when using the connector.</span><span class="sxs-lookup"><span data-stu-id="634fa-114">The following diagram shows the data flow between Azure IoT Hub and Kafka on HDInsight when using the connector.</span></span>

![Image showing data flowing from IoT Hub to Kafka through the connector](./media/apache-kafka-connector-iot-hub/iot-hub-kafka-connector-hdinsight.png)

<span data-ttu-id="634fa-116">For more information on the Connect API, see [https://kafka.apache.org/documentation/#connect](https://kafka.apache.org/documentation/#connect).</span><span class="sxs-lookup"><span data-stu-id="634fa-116">For more information on the Connect API, see [https://kafka.apache.org/documentation/#connect](https://kafka.apache.org/documentation/#connect).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="634fa-117">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="634fa-117">Prerequisites</span></span>

* <span data-ttu-id="634fa-118">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="634fa-118">An Azure subscription.</span></span> <span data-ttu-id="634fa-119">If you don’t have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="634fa-119">If you don’t have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

* <span data-ttu-id="634fa-120">A Kafka on HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="634fa-120">A Kafka on HDInsight cluster.</span></span> <span data-ttu-id="634fa-121">For more information, see the [Kafka on HDInsight quickstart](apache-kafka-get-started.md) document.</span><span class="sxs-lookup"><span data-stu-id="634fa-121">For more information, see the [Kafka on HDInsight quickstart](apache-kafka-get-started.md) document.</span></span>

* <span data-ttu-id="634fa-122">An edge node in the Kafka cluster.</span><span class="sxs-lookup"><span data-stu-id="634fa-122">An edge node in the Kafka cluster.</span></span> <span data-ttu-id="634fa-123">For more information, see the [Use edge nodes with HDInsight](../hdinsight-apps-use-edge-node.md) document.</span><span class="sxs-lookup"><span data-stu-id="634fa-123">For more information, see the [Use edge nodes with HDInsight](../hdinsight-apps-use-edge-node.md) document.</span></span>

* <span data-ttu-id="634fa-124">An Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="634fa-124">An Azure IoT Hub.</span></span> <span data-ttu-id="634fa-125">For this tutorial, I recommend the [Connect Raspberry Pi online simulator to Azure IoT Hub](https://docs.microsoft.com/azure/iot-hub/iot-hub-raspberry-pi-web-simulator-get-started) document.</span><span class="sxs-lookup"><span data-stu-id="634fa-125">For this tutorial, I recommend the [Connect Raspberry Pi online simulator to Azure IoT Hub](https://docs.microsoft.com/azure/iot-hub/iot-hub-raspberry-pi-web-simulator-get-started) document.</span></span>

* <span data-ttu-id="634fa-126">An SSH client.</span><span class="sxs-lookup"><span data-stu-id="634fa-126">An SSH client.</span></span> <span data-ttu-id="634fa-127">The steps in this document use SSH to connect to the cluster.</span><span class="sxs-lookup"><span data-stu-id="634fa-127">The steps in this document use SSH to connect to the cluster.</span></span> <span data-ttu-id="634fa-128">For more information, see the [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md) document.</span><span class="sxs-lookup"><span data-stu-id="634fa-128">For more information, see the [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

## <a name="install-the-connector"></a><span data-ttu-id="634fa-129">Install the connector</span><span class="sxs-lookup"><span data-stu-id="634fa-129">Install the connector</span></span>

1. <span data-ttu-id="634fa-130">Download the latest release of the Kafka Connect for Azure IoT Hub from [https://github.com/Azure/toketi-kafka-connect-iothub/releases/](https://github.com/Azure/toketi-kafka-connect-iothub/releases).</span><span class="sxs-lookup"><span data-stu-id="634fa-130">Download the latest release of the Kafka Connect for Azure IoT Hub from [https://github.com/Azure/toketi-kafka-connect-iothub/releases/](https://github.com/Azure/toketi-kafka-connect-iothub/releases).</span></span>

2. <span data-ttu-id="634fa-131">To upload the .jar file to the edge node of your Kafka on HDInsight cluster, use the following command:</span><span class="sxs-lookup"><span data-stu-id="634fa-131">To upload the .jar file to the edge node of your Kafka on HDInsight cluster, use the following command:</span></span>

    > [!NOTE]
    > <span data-ttu-id="634fa-132">Replace `sshuser` with the SSH user account for your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="634fa-132">Replace `sshuser` with the SSH user account for your HDInsight cluster.</span></span> <span data-ttu-id="634fa-133">Replace `new-edgenode` with the edge node name.</span><span class="sxs-lookup"><span data-stu-id="634fa-133">Replace `new-edgenode` with the edge node name.</span></span> <span data-ttu-id="634fa-134">Replace `clustername` with the cluster name.</span><span class="sxs-lookup"><span data-stu-id="634fa-134">Replace `clustername` with the cluster name.</span></span> <span data-ttu-id="634fa-135">For more information on the SSH endpoint for the edge node, see the [Used edge nodes with HDInsight](../hdinsight-apps-use-edge-node.md#access-an-edge-node) document.</span><span class="sxs-lookup"><span data-stu-id="634fa-135">For more information on the SSH endpoint for the edge node, see the [Used edge nodes with HDInsight](../hdinsight-apps-use-edge-node.md#access-an-edge-node) document.</span></span>

    ```bash
    scp kafka-connect-iothub-assembly*.jar sshuser@new-edgenode.clustername-ssh.azurehdinsight.net:
    ```

3. <span data-ttu-id="634fa-136">Once the file copy completes, connect to the edge node using SSH:</span><span class="sxs-lookup"><span data-stu-id="634fa-136">Once the file copy completes, connect to the edge node using SSH:</span></span>

    ```bash
    ssh sshuser@new-edgenode.clustername-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="634fa-137">For more information, see the [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md) document.</span><span class="sxs-lookup"><span data-stu-id="634fa-137">For more information, see the [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

4. <span data-ttu-id="634fa-138">To install the connector into the Kafka `libs` directory, use the following command:</span><span class="sxs-lookup"><span data-stu-id="634fa-138">To install the connector into the Kafka `libs` directory, use the following command:</span></span>

    ```bash
    sudo mv kafka-connect-iothub-assembly*.jar /usr/hdp/current/kafka-broker/libs/
    ```

> [!TIP]
> <span data-ttu-id="634fa-139">If you run into problems with the rest of the steps in this document when using a pre-built .jar file, try building the package from source.</span><span class="sxs-lookup"><span data-stu-id="634fa-139">If you run into problems with the rest of the steps in this document when using a pre-built .jar file, try building the package from source.</span></span>
>
> <span data-ttu-id="634fa-140">To build the connector, you must have a Scala development environment with the [Scala build tool](http://www.scala-sbt.org/).</span><span class="sxs-lookup"><span data-stu-id="634fa-140">To build the connector, you must have a Scala development environment with the [Scala build tool](http://www.scala-sbt.org/).</span></span>
>
> 1. <span data-ttu-id="634fa-141">Download the source for the connector from [https://github.com/Azure/toketi-kafka-connect-iothub/](https://github.com/Azure/toketi-kafka-connect-iothub/) to your development environment.</span><span class="sxs-lookup"><span data-stu-id="634fa-141">Download the source for the connector from [https://github.com/Azure/toketi-kafka-connect-iothub/](https://github.com/Azure/toketi-kafka-connect-iothub/) to your development environment.</span></span>
>
> 2. <span data-ttu-id="634fa-142">From a command-prompt in the project directory, use the following command to build and package the project:</span><span class="sxs-lookup"><span data-stu-id="634fa-142">From a command-prompt in the project directory, use the following command to build and package the project:</span></span>
>
>    ```bash
>    sbt assembly
>    ```
>
>    <span data-ttu-id="634fa-143">This command creates a file named `kafka-connect-iothub-assembly_2.11-0.6.jar` in the `target/scala-2.11` directory for the project.</span><span class="sxs-lookup"><span data-stu-id="634fa-143">This command creates a file named `kafka-connect-iothub-assembly_2.11-0.6.jar` in the `target/scala-2.11` directory for the project.</span></span>

## <a name="configure-kafka"></a><span data-ttu-id="634fa-144">Configure Kafka</span><span class="sxs-lookup"><span data-stu-id="634fa-144">Configure Kafka</span></span>

<span data-ttu-id="634fa-145">From an SSH connection to the edge node, use the following steps to configure Kafka to run the connector in standalone mode:</span><span class="sxs-lookup"><span data-stu-id="634fa-145">From an SSH connection to the edge node, use the following steps to configure Kafka to run the connector in standalone mode:</span></span>

1. <span data-ttu-id="634fa-146">Save the cluster name to a variable.</span><span class="sxs-lookup"><span data-stu-id="634fa-146">Save the cluster name to a variable.</span></span> <span data-ttu-id="634fa-147">Using a variable makes it easier to copy/paste the other commands in this section:</span><span class="sxs-lookup"><span data-stu-id="634fa-147">Using a variable makes it easier to copy/paste the other commands in this section:</span></span>

    ```bash
    read -p "Enter the Kafka on HDInsight cluster name: " CLUSTERNAME
    ```

2. <span data-ttu-id="634fa-148">Install the `jq` utility.</span><span class="sxs-lookup"><span data-stu-id="634fa-148">Install the `jq` utility.</span></span> <span data-ttu-id="634fa-149">This utility makes it easier to process JSON documents returned from Ambari queries:</span><span class="sxs-lookup"><span data-stu-id="634fa-149">This utility makes it easier to process JSON documents returned from Ambari queries:</span></span>

    ```bash
    sudo apt -y install jq
    ```

3. <span data-ttu-id="634fa-150">Get the address of the Kafka brokers.</span><span class="sxs-lookup"><span data-stu-id="634fa-150">Get the address of the Kafka brokers.</span></span> <span data-ttu-id="634fa-151">There may be many brokers in your cluster, but you only need to reference one or two.</span><span class="sxs-lookup"><span data-stu-id="634fa-151">There may be many brokers in your cluster, but you only need to reference one or two.</span></span> <span data-ttu-id="634fa-152">To get the address of two broker hosts, use the following command:</span><span class="sxs-lookup"><span data-stu-id="634fa-152">To get the address of two broker hosts, use the following command:</span></span>

    ```bash
    export KAFKABROKERS=`curl -sS -u admin -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`
    echo $KAFKABROKERS
    ```

    <span data-ttu-id="634fa-153">When prompted, enter the password for the cluster login (admin) account.</span><span class="sxs-lookup"><span data-stu-id="634fa-153">When prompted, enter the password for the cluster login (admin) account.</span></span> <span data-ttu-id="634fa-154">The value returned is similar to the following text:</span><span class="sxs-lookup"><span data-stu-id="634fa-154">The value returned is similar to the following text:</span></span>

    `wn0-kafka.w5ijyohcxt5uvdhhuaz5ra4u5f.ex.internal.cloudapp.net:9092,wn1-kafka.w5ijyohcxt5uvdhhuaz5ra4u5f.ex.internal.cloudapp.net:9092`

4. <span data-ttu-id="634fa-155">Get the address of the Zookeeper nodes.</span><span class="sxs-lookup"><span data-stu-id="634fa-155">Get the address of the Zookeeper nodes.</span></span> <span data-ttu-id="634fa-156">There are several Zookeeper nodes in the cluster, but you only need to reference one or two.</span><span class="sxs-lookup"><span data-stu-id="634fa-156">There are several Zookeeper nodes in the cluster, but you only need to reference one or two.</span></span> <span data-ttu-id="634fa-157">To get the address of two Zookeeper nodes, use the following command:</span><span class="sxs-lookup"><span data-stu-id="634fa-157">To get the address of two Zookeeper nodes, use the following command:</span></span>

    ```bash
    export KAFKAZKHOSTS=`curl -sS -u admin -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`
    ```

5. <span data-ttu-id="634fa-158">When running the connector in standalone mode, the `/usr/hdp/current/kafka-broker/config/connect-standalone.properties` file is used to communicate with the Kafka brokers.</span><span class="sxs-lookup"><span data-stu-id="634fa-158">When running the connector in standalone mode, the `/usr/hdp/current/kafka-broker/config/connect-standalone.properties` file is used to communicate with the Kafka brokers.</span></span> <span data-ttu-id="634fa-159">To edit the `connect-standalone.properties` file, use the following command:</span><span class="sxs-lookup"><span data-stu-id="634fa-159">To edit the `connect-standalone.properties` file, use the following command:</span></span>

    ```bash
    sudo nano /usr/hdp/current/kafka-broker/config/connect-standalone.properties
    ```

    * <span data-ttu-id="634fa-160">To configure the standalone configuration for the edge node to find the Kafka brokers, find the line that begins with `bootstrap.servers=`.</span><span class="sxs-lookup"><span data-stu-id="634fa-160">To configure the standalone configuration for the edge node to find the Kafka brokers, find the line that begins with `bootstrap.servers=`.</span></span> <span data-ttu-id="634fa-161">Replace the `localhost:9092` value with the broker hosts from the previous step.</span><span class="sxs-lookup"><span data-stu-id="634fa-161">Replace the `localhost:9092` value with the broker hosts from the previous step.</span></span>

    * <span data-ttu-id="634fa-162">Change the `key.converter=` and `value.converter=` lines to the following values:</span><span class="sxs-lookup"><span data-stu-id="634fa-162">Change the `key.converter=` and `value.converter=` lines to the following values:</span></span>

        ```text
        key.converter=org.apache.kafka.connect.storage.StringConverter
        value.converter=org.apache.kafka.connect.storage.StringConverter
        ```

        > [!IMPORTANT]
        > <span data-ttu-id="634fa-163">This change allows you to test using the console producer included with Kafka.</span><span class="sxs-lookup"><span data-stu-id="634fa-163">This change allows you to test using the console producer included with Kafka.</span></span> <span data-ttu-id="634fa-164">You may need different converters for other producers and consumers.</span><span class="sxs-lookup"><span data-stu-id="634fa-164">You may need different converters for other producers and consumers.</span></span> <span data-ttu-id="634fa-165">For information on using other converter values, see [https://github.com/Azure/toketi-kafka-connect-iothub/blob/master/README_Sink.md](https://github.com/Azure/toketi-kafka-connect-iothub/blob/master/README_Sink.md).</span><span class="sxs-lookup"><span data-stu-id="634fa-165">For information on using other converter values, see [https://github.com/Azure/toketi-kafka-connect-iothub/blob/master/README_Sink.md](https://github.com/Azure/toketi-kafka-connect-iothub/blob/master/README_Sink.md).</span></span>

    * <span data-ttu-id="634fa-166">Add a line at the end of the file that contains the following text:</span><span class="sxs-lookup"><span data-stu-id="634fa-166">Add a line at the end of the file that contains the following text:</span></span>

        ```text
        consumer.max.poll.records=10
        ```

        > [!TIP]
        > <span data-ttu-id="634fa-167">This change is to prevent timeouts in the sink connector by limiting it to 10 records at a time.</span><span class="sxs-lookup"><span data-stu-id="634fa-167">This change is to prevent timeouts in the sink connector by limiting it to 10 records at a time.</span></span> <span data-ttu-id="634fa-168">For more information, see [https://github.com/Azure/toketi-kafka-connect-iothub/blob/master/README_Sink.md](https://github.com/Azure/toketi-kafka-connect-iothub/blob/master/README_Sink.md).</span><span class="sxs-lookup"><span data-stu-id="634fa-168">For more information, see [https://github.com/Azure/toketi-kafka-connect-iothub/blob/master/README_Sink.md](https://github.com/Azure/toketi-kafka-connect-iothub/blob/master/README_Sink.md).</span></span>

6. <span data-ttu-id="634fa-169">To save the file, use __Ctrl + X__, __Y__, and then __Enter__.</span><span class="sxs-lookup"><span data-stu-id="634fa-169">To save the file, use __Ctrl + X__, __Y__, and then __Enter__.</span></span>

7. <span data-ttu-id="634fa-170">To create the topics used by the connector, use the following commands:</span><span class="sxs-lookup"><span data-stu-id="634fa-170">To create the topics used by the connector, use the following commands:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic iotin --zookeeper $KAFKAZKHOSTS

    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic iotout --zookeeper $KAFKAZKHOSTS
    ```

    <span data-ttu-id="634fa-171">To verify that the `iotin` and `iotout` topics exist, use the following command:</span><span class="sxs-lookup"><span data-stu-id="634fa-171">To verify that the `iotin` and `iotout` topics exist, use the following command:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $KAFKAZKHOSTS
    ```

    <span data-ttu-id="634fa-172">The `iotin` topic is used to receive messages from IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="634fa-172">The `iotin` topic is used to receive messages from IoT Hub.</span></span> <span data-ttu-id="634fa-173">The `iotout` topic is used to send messages to IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="634fa-173">The `iotout` topic is used to send messages to IoT Hub.</span></span>

## <a name="get-iot-hub-connection-information"></a><span data-ttu-id="634fa-174">Get IoT Hub connection information</span><span class="sxs-lookup"><span data-stu-id="634fa-174">Get IoT Hub connection information</span></span>

<span data-ttu-id="634fa-175">To retrieve IoT hub information used by the connector, use the following steps:</span><span class="sxs-lookup"><span data-stu-id="634fa-175">To retrieve IoT hub information used by the connector, use the following steps:</span></span>

1. <span data-ttu-id="634fa-176">Get the Event Hub-compatible endpoint and Event Hub-compatible endpoint name for your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="634fa-176">Get the Event Hub-compatible endpoint and Event Hub-compatible endpoint name for your IoT hub.</span></span> <span data-ttu-id="634fa-177">To get this information, use one of the following methods:</span><span class="sxs-lookup"><span data-stu-id="634fa-177">To get this information, use one of the following methods:</span></span>

    * <span data-ttu-id="634fa-178">__From the [Azure portal](https://portal.azure.com/)__, use the following steps:</span><span class="sxs-lookup"><span data-stu-id="634fa-178">__From the [Azure portal](https://portal.azure.com/)__, use the following steps:</span></span>

        1. <span data-ttu-id="634fa-179">Navigate to your IoT Hub and select __Endpoints__.</span><span class="sxs-lookup"><span data-stu-id="634fa-179">Navigate to your IoT Hub and select __Endpoints__.</span></span>
        2. <span data-ttu-id="634fa-180">From __Built-in endpoints__, select __Events__.</span><span class="sxs-lookup"><span data-stu-id="634fa-180">From __Built-in endpoints__, select __Events__.</span></span>
        3. <span data-ttu-id="634fa-181">From __Properties__, copy the value of the following fields:</span><span class="sxs-lookup"><span data-stu-id="634fa-181">From __Properties__, copy the value of the following fields:</span></span>

            * <span data-ttu-id="634fa-182">__Event Hub-compatible name__</span><span class="sxs-lookup"><span data-stu-id="634fa-182">__Event Hub-compatible name__</span></span>
            * <span data-ttu-id="634fa-183">__Event Hub-compatible endpoint__</span><span class="sxs-lookup"><span data-stu-id="634fa-183">__Event Hub-compatible endpoint__</span></span>
            * <span data-ttu-id="634fa-184">__Partitions__</span><span class="sxs-lookup"><span data-stu-id="634fa-184">__Partitions__</span></span>

        > [!IMPORTANT]
        > <span data-ttu-id="634fa-185">The endpoint value from the portal may contain extra text that is not needed in this example.</span><span class="sxs-lookup"><span data-stu-id="634fa-185">The endpoint value from the portal may contain extra text that is not needed in this example.</span></span> <span data-ttu-id="634fa-186">Extract the text that matches this pattern `sb://<randomnamespace>.servicebus.windows.net/`.</span><span class="sxs-lookup"><span data-stu-id="634fa-186">Extract the text that matches this pattern `sb://<randomnamespace>.servicebus.windows.net/`.</span></span>

    * <span data-ttu-id="634fa-187">__From the [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli)__, use the following command:</span><span class="sxs-lookup"><span data-stu-id="634fa-187">__From the [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli)__, use the following command:</span></span>

        ```azure-cli
        az iot hub show --name myhubname --query "{EventHubCompatibleName:properties.eventHubEndpoints.events.path,EventHubCompatibleEndpoint:properties.eventHubEndpoints.events.endpoint,Partitions:properties.eventHubEndpoints.events.partitionCount}"
        ```

        <span data-ttu-id="634fa-188">Replace `myhubname` with the name of your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="634fa-188">Replace `myhubname` with the name of your IoT hub.</span></span> <span data-ttu-id="634fa-189">The response is similar to the following text:</span><span class="sxs-lookup"><span data-stu-id="634fa-189">The response is similar to the following text:</span></span>

        ```text
        "EventHubCompatibleEndpoint": "sb://ihsuprodbnres006dednamespace.servicebus.windows.net/",
        "EventHubCompatibleName": "iothub-ehub-myhub08-207673-d44b2a856e",
        "Partitions": 2
        ```

2. <span data-ttu-id="634fa-190">Get the __shared access policy__ and __key__.</span><span class="sxs-lookup"><span data-stu-id="634fa-190">Get the __shared access policy__ and __key__.</span></span> <span data-ttu-id="634fa-191">For this example, use the __service__ key.</span><span class="sxs-lookup"><span data-stu-id="634fa-191">For this example, use the __service__ key.</span></span> <span data-ttu-id="634fa-192">To get this information, use one of the following methods:</span><span class="sxs-lookup"><span data-stu-id="634fa-192">To get this information, use one of the following methods:</span></span>

    * <span data-ttu-id="634fa-193">__From the [Azure portal](https://portal.azure.com/)__, use the following steps:</span><span class="sxs-lookup"><span data-stu-id="634fa-193">__From the [Azure portal](https://portal.azure.com/)__, use the following steps:</span></span>

        1. <span data-ttu-id="634fa-194">Select __Shared access policies__, and then select __service__.</span><span class="sxs-lookup"><span data-stu-id="634fa-194">Select __Shared access policies__, and then select __service__.</span></span>
        2. <span data-ttu-id="634fa-195">Copy the __Primary key__ value.</span><span class="sxs-lookup"><span data-stu-id="634fa-195">Copy the __Primary key__ value.</span></span>
        3. <span data-ttu-id="634fa-196">Copy the __Connection string--primary key__ value.</span><span class="sxs-lookup"><span data-stu-id="634fa-196">Copy the __Connection string--primary key__ value.</span></span>

    * <span data-ttu-id="634fa-197">__From the [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli)__, use the following command:</span><span class="sxs-lookup"><span data-stu-id="634fa-197">__From the [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli)__, use the following command:</span></span>

        1. <span data-ttu-id="634fa-198">To get the primary key value, use the following command:</span><span class="sxs-lookup"><span data-stu-id="634fa-198">To get the primary key value, use the following command:</span></span>

            ```azure-cli
            az iot hub policy show --hub-name myhubname --name service --query "primaryKey"
            ```

            <span data-ttu-id="634fa-199">Replace `myhubname` with the name of your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="634fa-199">Replace `myhubname` with the name of your IoT hub.</span></span> <span data-ttu-id="634fa-200">The response is the primary key to the `service` policy for this hub.</span><span class="sxs-lookup"><span data-stu-id="634fa-200">The response is the primary key to the `service` policy for this hub.</span></span>

        2. <span data-ttu-id="634fa-201">To get the connection string for the `service` policy, use the following command:</span><span class="sxs-lookup"><span data-stu-id="634fa-201">To get the connection string for the `service` policy, use the following command:</span></span>

            ```azure-cli
            az iot hub show-connection-string --name myhubname --policy-name service --query "connectionString"
            ```

            <span data-ttu-id="634fa-202">Replace `myhubname` with the name of your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="634fa-202">Replace `myhubname` with the name of your IoT hub.</span></span> <span data-ttu-id="634fa-203">The response is the connection string for the `service` policy.</span><span class="sxs-lookup"><span data-stu-id="634fa-203">The response is the connection string for the `service` policy.</span></span>

## <a name="configure-the-source-connection"></a><span data-ttu-id="634fa-204">Configure the source connection</span><span class="sxs-lookup"><span data-stu-id="634fa-204">Configure the source connection</span></span>

<span data-ttu-id="634fa-205">To configure the source to work with your IoT Hub, perform the following actions from an SSH connection to the edge node:</span><span class="sxs-lookup"><span data-stu-id="634fa-205">To configure the source to work with your IoT Hub, perform the following actions from an SSH connection to the edge node:</span></span>

1. <span data-ttu-id="634fa-206">Create a copy of the `connect-iot-source.properties` file in the `/usr/hdp/current/kafka-broker/config/` directory.</span><span class="sxs-lookup"><span data-stu-id="634fa-206">Create a copy of the `connect-iot-source.properties` file in the `/usr/hdp/current/kafka-broker/config/` directory.</span></span> <span data-ttu-id="634fa-207">To download the file from the toketi-kafka-connect-iothub project, use the following command:</span><span class="sxs-lookup"><span data-stu-id="634fa-207">To download the file from the toketi-kafka-connect-iothub project, use the following command:</span></span>

    ```bash
    sudo wget -P /usr/hdp/current/kafka-broker/config/ https://raw.githubusercontent.com/Azure/toketi-kafka-connect-iothub/master/connect-iothub-source.properties
    ```

2. <span data-ttu-id="634fa-208">To edit the `connect-iot-source.properties` file and add the IoT hub information, use the following command:</span><span class="sxs-lookup"><span data-stu-id="634fa-208">To edit the `connect-iot-source.properties` file and add the IoT hub information, use the following command:</span></span>

    ```bash
    sudo nano /usr/hdp/current/kafka-broker/config/connect-iothub-source.properties
    ```

    <span data-ttu-id="634fa-209">In the editor, find and change the following entries:</span><span class="sxs-lookup"><span data-stu-id="634fa-209">In the editor, find and change the following entries:</span></span>

    * <span data-ttu-id="634fa-210">`Kafka.Topic=PLACEHOLDER`: Replace `PLACEHOLDER` with `iotin`.</span><span class="sxs-lookup"><span data-stu-id="634fa-210">`Kafka.Topic=PLACEHOLDER`: Replace `PLACEHOLDER` with `iotin`.</span></span> <span data-ttu-id="634fa-211">Messages received from IoT hub are placed in the `iotin` topic.</span><span class="sxs-lookup"><span data-stu-id="634fa-211">Messages received from IoT hub are placed in the `iotin` topic.</span></span>
    * <span data-ttu-id="634fa-212">`IotHub.EventHubCompatibleName=PLACEHOLDER`: Replace `PLACEHOLDER` with the Event Hub-compatible name.</span><span class="sxs-lookup"><span data-stu-id="634fa-212">`IotHub.EventHubCompatibleName=PLACEHOLDER`: Replace `PLACEHOLDER` with the Event Hub-compatible name.</span></span>
    * <span data-ttu-id="634fa-213">`IotHub.EventHubCompatibleEndpoint=PLACEHOLDER`: Replace `PLACEHOLDER` with the Event Hub-compatible endpoint.</span><span class="sxs-lookup"><span data-stu-id="634fa-213">`IotHub.EventHubCompatibleEndpoint=PLACEHOLDER`: Replace `PLACEHOLDER` with the Event Hub-compatible endpoint.</span></span>
    * <span data-ttu-id="634fa-214">`IotHub.Partitions=PLACEHOLDER`: Replace `PLACEHOLDER` with the number of partitions from the previous steps.</span><span class="sxs-lookup"><span data-stu-id="634fa-214">`IotHub.Partitions=PLACEHOLDER`: Replace `PLACEHOLDER` with the number of partitions from the previous steps.</span></span>
    * <span data-ttu-id="634fa-215">`IotHub.AccessKeyName=PLACEHOLDER`: Replace `PLACEHOLDER` with `service`.</span><span class="sxs-lookup"><span data-stu-id="634fa-215">`IotHub.AccessKeyName=PLACEHOLDER`: Replace `PLACEHOLDER` with `service`.</span></span>
    * <span data-ttu-id="634fa-216">`IotHub.AccessKeyValue=PLACEHOLDER`: Replace `PLACEHOLDER` with the primary key of the `service` policy.</span><span class="sxs-lookup"><span data-stu-id="634fa-216">`IotHub.AccessKeyValue=PLACEHOLDER`: Replace `PLACEHOLDER` with the primary key of the `service` policy.</span></span>
    * <span data-ttu-id="634fa-217">`IotHub.StartType=PLACEHOLDER`: Replace `PLACEHOLDER` with a UTC date.</span><span class="sxs-lookup"><span data-stu-id="634fa-217">`IotHub.StartType=PLACEHOLDER`: Replace `PLACEHOLDER` with a UTC date.</span></span> <span data-ttu-id="634fa-218">This date is when the connector starts checking for messages.</span><span class="sxs-lookup"><span data-stu-id="634fa-218">This date is when the connector starts checking for messages.</span></span> <span data-ttu-id="634fa-219">The date format is `yyyy-mm-ddThh:mm:ssZ`.</span><span class="sxs-lookup"><span data-stu-id="634fa-219">The date format is `yyyy-mm-ddThh:mm:ssZ`.</span></span>
    * <span data-ttu-id="634fa-220">`BatchSize=100`: Replace `100` with `5`.</span><span class="sxs-lookup"><span data-stu-id="634fa-220">`BatchSize=100`: Replace `100` with `5`.</span></span> <span data-ttu-id="634fa-221">This change causes the connector to read messages into Kafka once there are five new messages in IoT hub.</span><span class="sxs-lookup"><span data-stu-id="634fa-221">This change causes the connector to read messages into Kafka once there are five new messages in IoT hub.</span></span>

    <span data-ttu-id="634fa-222">For an example configuration, see [https://github.com/Azure/toketi-kafka-connect-iothub/blob/master/README_Source.md](https://github.com/Azure/toketi-kafka-connect-iothub/blob/master/README_Source.md).</span><span class="sxs-lookup"><span data-stu-id="634fa-222">For an example configuration, see [https://github.com/Azure/toketi-kafka-connect-iothub/blob/master/README_Source.md](https://github.com/Azure/toketi-kafka-connect-iothub/blob/master/README_Source.md).</span></span>

3. <span data-ttu-id="634fa-223">To save changes, use __Ctrl + X__, __Y__, and then __Enter__.</span><span class="sxs-lookup"><span data-stu-id="634fa-223">To save changes, use __Ctrl + X__, __Y__, and then __Enter__.</span></span>

<span data-ttu-id="634fa-224">For more information on configuring the connector source, see [https://github.com/Azure/toketi-kafka-connect-iothub/blob/master/README_Source.md](https://github.com/Azure/toketi-kafka-connect-iothub/blob/master/README_Source.md).</span><span class="sxs-lookup"><span data-stu-id="634fa-224">For more information on configuring the connector source, see [https://github.com/Azure/toketi-kafka-connect-iothub/blob/master/README_Source.md](https://github.com/Azure/toketi-kafka-connect-iothub/blob/master/README_Source.md).</span></span>

## <a name="configure-the-sink-connection"></a><span data-ttu-id="634fa-225">Configure the sink connection</span><span class="sxs-lookup"><span data-stu-id="634fa-225">Configure the sink connection</span></span>

<span data-ttu-id="634fa-226">To configure the sink connection to work with your IoT Hub, perform the following actions from an SSH connection to the edge node:</span><span class="sxs-lookup"><span data-stu-id="634fa-226">To configure the sink connection to work with your IoT Hub, perform the following actions from an SSH connection to the edge node:</span></span>

1. <span data-ttu-id="634fa-227">Create a copy of the `connect-iothub-sink.properties` file in the `/usr/hdp/current/kafka-broker/config/` directory.</span><span class="sxs-lookup"><span data-stu-id="634fa-227">Create a copy of the `connect-iothub-sink.properties` file in the `/usr/hdp/current/kafka-broker/config/` directory.</span></span> <span data-ttu-id="634fa-228">To download the file from the toketi-kafka-connect-iothub project, use the following command:</span><span class="sxs-lookup"><span data-stu-id="634fa-228">To download the file from the toketi-kafka-connect-iothub project, use the following command:</span></span>

    ```bash
    sudo wget -P /usr/hdp/current/kafka-broker/config/ https://raw.githubusercontent.com/Azure/toketi-kafka-connect-iothub/master/connect-iothub-sink.properties
    ```

2. <span data-ttu-id="634fa-229">To edit the `connect-iothub-sink.properties` file and add the IoT hub information, use the following command:</span><span class="sxs-lookup"><span data-stu-id="634fa-229">To edit the `connect-iothub-sink.properties` file and add the IoT hub information, use the following command:</span></span>

    ```bash
    sudo nano /usr/hdp/current/kafka-broker/config/connect-iothub-sink.properties
    ```

    <span data-ttu-id="634fa-230">In the editor, find and change the following entries:</span><span class="sxs-lookup"><span data-stu-id="634fa-230">In the editor, find and change the following entries:</span></span>

    * <span data-ttu-id="634fa-231">`topics=PLACEHOLDER`: Replace `PLACEHOLDER` with `iotout`.</span><span class="sxs-lookup"><span data-stu-id="634fa-231">`topics=PLACEHOLDER`: Replace `PLACEHOLDER` with `iotout`.</span></span> <span data-ttu-id="634fa-232">Messages written to `iotout` topic are forwarded to the IoT hub.</span><span class="sxs-lookup"><span data-stu-id="634fa-232">Messages written to `iotout` topic are forwarded to the IoT hub.</span></span>
    * <span data-ttu-id="634fa-233">`IotHub.ConnectionString=PLACEHOLDER`: Replace `PLACEHOLDER` with the connection string for the `service` policy.</span><span class="sxs-lookup"><span data-stu-id="634fa-233">`IotHub.ConnectionString=PLACEHOLDER`: Replace `PLACEHOLDER` with the connection string for the `service` policy.</span></span>

    <span data-ttu-id="634fa-234">For an example configuration, see [https://github.com/Azure/toketi-kafka-connect-iothub/blob/master/README_Sink.md](https://github.com/Azure/toketi-kafka-connect-iothub/blob/master/README_Sink.md).</span><span class="sxs-lookup"><span data-stu-id="634fa-234">For an example configuration, see [https://github.com/Azure/toketi-kafka-connect-iothub/blob/master/README_Sink.md](https://github.com/Azure/toketi-kafka-connect-iothub/blob/master/README_Sink.md).</span></span>

3. <span data-ttu-id="634fa-235">To save changes, use __Ctrl + X__, __Y__, and then __Enter__.</span><span class="sxs-lookup"><span data-stu-id="634fa-235">To save changes, use __Ctrl + X__, __Y__, and then __Enter__.</span></span>

<span data-ttu-id="634fa-236">For more information on configuring the connector sink, see [https://github.com/Azure/toketi-kafka-connect-iothub/blob/master/README_Sink.md](https://github.com/Azure/toketi-kafka-connect-iothub/blob/master/README_Sink.md).</span><span class="sxs-lookup"><span data-stu-id="634fa-236">For more information on configuring the connector sink, see [https://github.com/Azure/toketi-kafka-connect-iothub/blob/master/README_Sink.md](https://github.com/Azure/toketi-kafka-connect-iothub/blob/master/README_Sink.md).</span></span>

## <a name="start-the-source-connector"></a><span data-ttu-id="634fa-237">Start the source connector</span><span class="sxs-lookup"><span data-stu-id="634fa-237">Start the source connector</span></span>

<span data-ttu-id="634fa-238">To start the source connector, use the following command from an SSH connection to the edge node:</span><span class="sxs-lookup"><span data-stu-id="634fa-238">To start the source connector, use the following command from an SSH connection to the edge node:</span></span>

```bash
/usr/hdp/current/kafka-broker/bin/connect-standalone.sh /usr/hdp/current/kafka-broker/config/connect-standalone.properties /usr/hdp/current/kafka-broker/config/connect-iothub-source.properties
```

<span data-ttu-id="634fa-239">Once the connector starts, send messages to IoT hub from your device(s).</span><span class="sxs-lookup"><span data-stu-id="634fa-239">Once the connector starts, send messages to IoT hub from your device(s).</span></span> <span data-ttu-id="634fa-240">As the connector reads messages from the IoT hub and stores them in the Kafka topic, it logs information to the console:</span><span class="sxs-lookup"><span data-stu-id="634fa-240">As the connector reads messages from the IoT hub and stores them in the Kafka topic, it logs information to the console:</span></span>

```text
[2017-08-29 20:15:46,112] INFO Polling for data - Obtained 5 SourceRecords from IotHub (com.microsoft.azure.iot.kafka.co
nnect.IotHubSourceTask:39)
[2017-08-29 20:15:54,106] INFO Finished WorkerSourceTask{id=AzureIotHubConnector-0} commitOffsets successfully in 4 ms (
org.apache.kafka.connect.runtime.WorkerSourceTask:356)
```

> [!NOTE]
> <span data-ttu-id="634fa-241">You may see several warnings as the connector starts.</span><span class="sxs-lookup"><span data-stu-id="634fa-241">You may see several warnings as the connector starts.</span></span> <span data-ttu-id="634fa-242">These warnings do not cause problems with receiving messages from IoT hub.</span><span class="sxs-lookup"><span data-stu-id="634fa-242">These warnings do not cause problems with receiving messages from IoT hub.</span></span>

<span data-ttu-id="634fa-243">To stop the connector, use __Ctrl + C__.</span><span class="sxs-lookup"><span data-stu-id="634fa-243">To stop the connector, use __Ctrl + C__.</span></span>

## <a name="start-the-sink-connector"></a><span data-ttu-id="634fa-244">Start the sink connector</span><span class="sxs-lookup"><span data-stu-id="634fa-244">Start the sink connector</span></span>

<span data-ttu-id="634fa-245">From an SSH connection to the edge node, use the following command to start the sink connector in standalone mode:</span><span class="sxs-lookup"><span data-stu-id="634fa-245">From an SSH connection to the edge node, use the following command to start the sink connector in standalone mode:</span></span>

```bash
/usr/hdp/current/kafka-broker/bin/connect-standalone.sh /usr/hdp/current/kafka-broker/config/connect-standalone.properties /usr/hdp/current/kafka-broker/config/connect-iothub-sink.properties
```

<span data-ttu-id="634fa-246">As the connector runs, information similar to the following text is displayed:</span><span class="sxs-lookup"><span data-stu-id="634fa-246">As the connector runs, information similar to the following text is displayed:</span></span>

```text
[2017-08-30 17:49:16,150] INFO Started tasks to send 1 messages to devices. (com.microsoft.azure.iot.kafka.connect.sink.
IotHubSinkTask:47)
[2017-08-30 17:49:16,150] INFO WorkerSinkTask{id=AzureIotHubSinkConnector-0} Committing offsets (org.apache.kafka.connec
t.runtime.WorkerSinkTask:262)
```

> [!NOTE]
> <span data-ttu-id="634fa-247">You may notice several warnings as the connector starts.</span><span class="sxs-lookup"><span data-stu-id="634fa-247">You may notice several warnings as the connector starts.</span></span> <span data-ttu-id="634fa-248">You can safely ignore these.</span><span class="sxs-lookup"><span data-stu-id="634fa-248">You can safely ignore these.</span></span>

<span data-ttu-id="634fa-249">To send messages through the connector, use the following steps:</span><span class="sxs-lookup"><span data-stu-id="634fa-249">To send messages through the connector, use the following steps:</span></span>

1. <span data-ttu-id="634fa-250">Open another SSH session to the Kafka cluster:</span><span class="sxs-lookup"><span data-stu-id="634fa-250">Open another SSH session to the Kafka cluster:</span></span>

    ```bash
    ssh sshuser@new-edgenode.clustername-ssh.azurehdinsight.net
    ```
2. <span data-ttu-id="634fa-251">To send messages to the `iotout` topic, use the following command:</span><span class="sxs-lookup"><span data-stu-id="634fa-251">To send messages to the `iotout` topic, use the following command:</span></span>

    > [!WARNING]
    > <span data-ttu-id="634fa-252">Since this is a new SSH connection, the `$KAFKABROKERS` variable does not contain any information.</span><span class="sxs-lookup"><span data-stu-id="634fa-252">Since this is a new SSH connection, the `$KAFKABROKERS` variable does not contain any information.</span></span> <span data-ttu-id="634fa-253">To set it, use one of the following methods:</span><span class="sxs-lookup"><span data-stu-id="634fa-253">To set it, use one of the following methods:</span></span>
    >
    > * <span data-ttu-id="634fa-254">Use the first three steps in the [Configure Kafka](#configure-kafka) section.</span><span class="sxs-lookup"><span data-stu-id="634fa-254">Use the first three steps in the [Configure Kafka](#configure-kafka) section.</span></span>
    > * <span data-ttu-id="634fa-255">Use `echo $KAFKABROKERS` from the previous SSH connection to get the values, and then replace `$KAFKABROKERS` in the following command with the actual values.</span><span class="sxs-lookup"><span data-stu-id="634fa-255">Use `echo $KAFKABROKERS` from the previous SSH connection to get the values, and then replace `$KAFKABROKERS` in the following command with the actual values.</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-producer.sh --broker-list $KAFKABROKERS --topic iotout
    ```

    <span data-ttu-id="634fa-256">This command does not return you to the normal Bash prompt.</span><span class="sxs-lookup"><span data-stu-id="634fa-256">This command does not return you to the normal Bash prompt.</span></span> <span data-ttu-id="634fa-257">Instead, it sends keyboard input to the `iotout` topic.</span><span class="sxs-lookup"><span data-stu-id="634fa-257">Instead, it sends keyboard input to the `iotout` topic.</span></span>

3. <span data-ttu-id="634fa-258">To send a message to your device, paste a JSON document into the SSH session for the `kafka-console-producer`.</span><span class="sxs-lookup"><span data-stu-id="634fa-258">To send a message to your device, paste a JSON document into the SSH session for the `kafka-console-producer`.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="634fa-259">You must set the value of the `"deviceId"` entry to the ID of your device.</span><span class="sxs-lookup"><span data-stu-id="634fa-259">You must set the value of the `"deviceId"` entry to the ID of your device.</span></span> <span data-ttu-id="634fa-260">In the following example, the device is named `fakepi`:</span><span class="sxs-lookup"><span data-stu-id="634fa-260">In the following example, the device is named `fakepi`:</span></span>

    ```text
    {"messageId":"msg1","message":"Turn On","deviceId":"fakepi"}
    ```

    <span data-ttu-id="634fa-261">The schema for this JSON document is described in more detail at [https://github.com/Azure/toketi-kafka-connect-iothub/blob/master/README_Sink.md](https://github.com/Azure/toketi-kafka-connect-iothub/blob/master/README_Sink.md).</span><span class="sxs-lookup"><span data-stu-id="634fa-261">The schema for this JSON document is described in more detail at [https://github.com/Azure/toketi-kafka-connect-iothub/blob/master/README_Sink.md](https://github.com/Azure/toketi-kafka-connect-iothub/blob/master/README_Sink.md).</span></span>

    <span data-ttu-id="634fa-262">If you are using the simulated Raspberry Pi device, and it is running, the following message is logged by the device:</span><span class="sxs-lookup"><span data-stu-id="634fa-262">If you are using the simulated Raspberry Pi device, and it is running, the following message is logged by the device:</span></span>

    ```text
    Receive message: Turn On
    ```

    <span data-ttu-id="634fa-263">Resend the JSON document, but change the value of the `"message"` entry.</span><span class="sxs-lookup"><span data-stu-id="634fa-263">Resend the JSON document, but change the value of the `"message"` entry.</span></span> <span data-ttu-id="634fa-264">The new value is logged by the device.</span><span class="sxs-lookup"><span data-stu-id="634fa-264">The new value is logged by the device.</span></span>

<span data-ttu-id="634fa-265">For more information on using the sink connector, see [https://github.com/Azure/toketi-kafka-connect-iothub/blob/master/README_Sink.md](https://github.com/Azure/toketi-kafka-connect-iothub/blob/master/README_Sink.md).</span><span class="sxs-lookup"><span data-stu-id="634fa-265">For more information on using the sink connector, see [https://github.com/Azure/toketi-kafka-connect-iothub/blob/master/README_Sink.md](https://github.com/Azure/toketi-kafka-connect-iothub/blob/master/README_Sink.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="634fa-266">Next steps</span><span class="sxs-lookup"><span data-stu-id="634fa-266">Next steps</span></span>

<span data-ttu-id="634fa-267">In this document, you learned how to use the Kafka Connect API to start the IoT Kafka Connector on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="634fa-267">In this document, you learned how to use the Kafka Connect API to start the IoT Kafka Connector on HDInsight.</span></span> <span data-ttu-id="634fa-268">Use the following links to discover other ways to work with Kafka:</span><span class="sxs-lookup"><span data-stu-id="634fa-268">Use the following links to discover other ways to work with Kafka:</span></span>

* [<span data-ttu-id="634fa-269">Use Apache Spark with Kafka on HDInsight</span><span class="sxs-lookup"><span data-stu-id="634fa-269">Use Apache Spark with Kafka on HDInsight</span></span>](../hdinsight-apache-spark-with-kafka.md)
* [<span data-ttu-id="634fa-270">Use Apache Storm with Kafka on HDInsight</span><span class="sxs-lookup"><span data-stu-id="634fa-270">Use Apache Storm with Kafka on HDInsight</span></span>](../hdinsight-apache-storm-with-kafka.md)
