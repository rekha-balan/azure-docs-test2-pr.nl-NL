---
title: Mirror Apache Kafka topics - Azure HDInsight
description: Learn how to use Apache Kafka's mirroring feature to maintain a replica of a Kafka on HDInsight cluster by mirroring topics to a secondary cluster.
services: hdinsight
author: jasonwhowell
ms.author: jasonh
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 05/01/2018
ms.openlocfilehash: 9f8204eb29566aaae9170c21b8dde33aa3178384
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966973"
---
# <a name="use-mirrormaker-to-replicate-apache-kafka-topics-with-kafka-on-hdinsight"></a><span data-ttu-id="0e72c-103">Use MirrorMaker to replicate Apache Kafka topics with Kafka on HDInsight</span><span class="sxs-lookup"><span data-stu-id="0e72c-103">Use MirrorMaker to replicate Apache Kafka topics with Kafka on HDInsight</span></span>

<span data-ttu-id="0e72c-104">Learn how to use Apache Kafka's mirroring feature to replicate topics to a secondary cluster.</span><span class="sxs-lookup"><span data-stu-id="0e72c-104">Learn how to use Apache Kafka's mirroring feature to replicate topics to a secondary cluster.</span></span> <span data-ttu-id="0e72c-105">Mirroring can be ran as a continuous process, or used intermittently as a method of migrating data from one cluster to another.</span><span class="sxs-lookup"><span data-stu-id="0e72c-105">Mirroring can be ran as a continuous process, or used intermittently as a method of migrating data from one cluster to another.</span></span>

<span data-ttu-id="0e72c-106">In this example, mirroring is used to replicate topics between two HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="0e72c-106">In this example, mirroring is used to replicate topics between two HDInsight clusters.</span></span> <span data-ttu-id="0e72c-107">Both clusters are in an Azure Virtual Network in the same region.</span><span class="sxs-lookup"><span data-stu-id="0e72c-107">Both clusters are in an Azure Virtual Network in the same region.</span></span>

> [!WARNING]
> <span data-ttu-id="0e72c-108">Mirroring should not be considered as a means to achieve fault-tolerance.</span><span class="sxs-lookup"><span data-stu-id="0e72c-108">Mirroring should not be considered as a means to achieve fault-tolerance.</span></span> <span data-ttu-id="0e72c-109">The offset to items within a topic are different between the source and destination clusters, so clients cannot use the two interchangeably.</span><span class="sxs-lookup"><span data-stu-id="0e72c-109">The offset to items within a topic are different between the source and destination clusters, so clients cannot use the two interchangeably.</span></span>
>
> <span data-ttu-id="0e72c-110">If you are concerned about fault tolerance, you should set replication for the topics within your cluster.</span><span class="sxs-lookup"><span data-stu-id="0e72c-110">If you are concerned about fault tolerance, you should set replication for the topics within your cluster.</span></span> <span data-ttu-id="0e72c-111">For more information, see [Get started with Kafka on HDInsight](apache-kafka-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="0e72c-111">For more information, see [Get started with Kafka on HDInsight](apache-kafka-get-started.md).</span></span>

## <a name="how-kafka-mirroring-works"></a><span data-ttu-id="0e72c-112">How Kafka mirroring works</span><span class="sxs-lookup"><span data-stu-id="0e72c-112">How Kafka mirroring works</span></span>

<span data-ttu-id="0e72c-113">Mirroring works by using the MirrorMaker tool (part of Apache Kafka) to consume records from topics on the source cluster and then create a local copy on the destination cluster.</span><span class="sxs-lookup"><span data-stu-id="0e72c-113">Mirroring works by using the MirrorMaker tool (part of Apache Kafka) to consume records from topics on the source cluster and then create a local copy on the destination cluster.</span></span> <span data-ttu-id="0e72c-114">MirrorMaker uses one (or more) *consumers* that read from the source cluster, and a *producer* that writes to the local (destination) cluster.</span><span class="sxs-lookup"><span data-stu-id="0e72c-114">MirrorMaker uses one (or more) *consumers* that read from the source cluster, and a *producer* that writes to the local (destination) cluster.</span></span>

<span data-ttu-id="0e72c-115">The following diagram illustrates the Mirroring process:</span><span class="sxs-lookup"><span data-stu-id="0e72c-115">The following diagram illustrates the Mirroring process:</span></span>

![Diagram of the mirroring process](./media/apache-kafka-mirroring/kafka-mirroring.png)

<span data-ttu-id="0e72c-117">Apache Kafka on HDInsight does not provide access to the Kafka service over the public internet.</span><span class="sxs-lookup"><span data-stu-id="0e72c-117">Apache Kafka on HDInsight does not provide access to the Kafka service over the public internet.</span></span> <span data-ttu-id="0e72c-118">Kafka producers or consumers must be in the same Azure virtual network as the nodes in the Kafka cluster.</span><span class="sxs-lookup"><span data-stu-id="0e72c-118">Kafka producers or consumers must be in the same Azure virtual network as the nodes in the Kafka cluster.</span></span> <span data-ttu-id="0e72c-119">For this example, both the Kafka source and destination clusters are located in an Azure virtual network.</span><span class="sxs-lookup"><span data-stu-id="0e72c-119">For this example, both the Kafka source and destination clusters are located in an Azure virtual network.</span></span> <span data-ttu-id="0e72c-120">The following diagram shows how communication flows between the clusters:</span><span class="sxs-lookup"><span data-stu-id="0e72c-120">The following diagram shows how communication flows between the clusters:</span></span>

![Diagram of source and destination Kafka clusters in an Azure virtual network](./media/apache-kafka-mirroring/spark-kafka-vnet.png)

<span data-ttu-id="0e72c-122">The source and destination clusters can be different in the number of nodes and partitions, and offsets within the topics are different also.</span><span class="sxs-lookup"><span data-stu-id="0e72c-122">The source and destination clusters can be different in the number of nodes and partitions, and offsets within the topics are different also.</span></span> <span data-ttu-id="0e72c-123">Mirroring maintains the key value that is used for partitioning, so record order is preserved on a per-key basis.</span><span class="sxs-lookup"><span data-stu-id="0e72c-123">Mirroring maintains the key value that is used for partitioning, so record order is preserved on a per-key basis.</span></span>

### <a name="mirroring-across-network-boundaries"></a><span data-ttu-id="0e72c-124">Mirroring across network boundaries</span><span class="sxs-lookup"><span data-stu-id="0e72c-124">Mirroring across network boundaries</span></span>

<span data-ttu-id="0e72c-125">If you need to mirror between Kafka clusters in different networks, there are the following additional considerations:</span><span class="sxs-lookup"><span data-stu-id="0e72c-125">If you need to mirror between Kafka clusters in different networks, there are the following additional considerations:</span></span>

* <span data-ttu-id="0e72c-126">**Gateways**: The networks must be able to communicate at the TCPIP level.</span><span class="sxs-lookup"><span data-stu-id="0e72c-126">**Gateways**: The networks must be able to communicate at the TCPIP level.</span></span>

* <span data-ttu-id="0e72c-127">**Name resolution**: The Kafka clusters in each network must be able to connect to each other by using hostnames.</span><span class="sxs-lookup"><span data-stu-id="0e72c-127">**Name resolution**: The Kafka clusters in each network must be able to connect to each other by using hostnames.</span></span> <span data-ttu-id="0e72c-128">This may require a Domain Name System (DNS) server in each network that is configured to forward requests to the other networks.</span><span class="sxs-lookup"><span data-stu-id="0e72c-128">This may require a Domain Name System (DNS) server in each network that is configured to forward requests to the other networks.</span></span>

    <span data-ttu-id="0e72c-129">When creating an Azure Virtual Network, instead of using the automatic DNS provided with the network, you must specify a custom DNS server and the IP address for the server.</span><span class="sxs-lookup"><span data-stu-id="0e72c-129">When creating an Azure Virtual Network, instead of using the automatic DNS provided with the network, you must specify a custom DNS server and the IP address for the server.</span></span> <span data-ttu-id="0e72c-130">After the Virtual Network has been created, you must then create an Azure Virtual Machine that uses that IP address, then install and configure DNS software on it.</span><span class="sxs-lookup"><span data-stu-id="0e72c-130">After the Virtual Network has been created, you must then create an Azure Virtual Machine that uses that IP address, then install and configure DNS software on it.</span></span>

    > [!WARNING]
    > <span data-ttu-id="0e72c-131">Create and configure the custom DNS server before installing HDInsight into the Virtual Network.</span><span class="sxs-lookup"><span data-stu-id="0e72c-131">Create and configure the custom DNS server before installing HDInsight into the Virtual Network.</span></span> <span data-ttu-id="0e72c-132">There is no additional configuration required for HDInsight to use the DNS server configured for the Virtual Network.</span><span class="sxs-lookup"><span data-stu-id="0e72c-132">There is no additional configuration required for HDInsight to use the DNS server configured for the Virtual Network.</span></span>

<span data-ttu-id="0e72c-133">For more information on connecting two Azure Virtual Networks, see [Configure a VNet-to-VNet connection](../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="0e72c-133">For more information on connecting two Azure Virtual Networks, see [Configure a VNet-to-VNet connection](../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).</span></span>

## <a name="create-kafka-clusters"></a><span data-ttu-id="0e72c-134">Create Kafka clusters</span><span class="sxs-lookup"><span data-stu-id="0e72c-134">Create Kafka clusters</span></span>

<span data-ttu-id="0e72c-135">While you can create an Azure virtual network and Kafka clusters manually, it's easier to use an Azure Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="0e72c-135">While you can create an Azure virtual network and Kafka clusters manually, it's easier to use an Azure Resource Manager template.</span></span> <span data-ttu-id="0e72c-136">Use the following steps to deploy an Azure virtual network and two Kafka clusters to your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="0e72c-136">Use the following steps to deploy an Azure virtual network and two Kafka clusters to your Azure subscription.</span></span>

1. <span data-ttu-id="0e72c-137">Use the following button to sign in to Azure and open the template in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="0e72c-137">Use the following button to sign in to Azure and open the template in the Azure portal.</span></span>
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json" target="_blank"><img src="./media/apache-kafka-mirroring/deploy-to-azure.png" alt="Deploy to Azure"></a>
   
    <span data-ttu-id="0e72c-138">The Azure Resource Manager template is located at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json**.</span><span class="sxs-lookup"><span data-stu-id="0e72c-138">The Azure Resource Manager template is located at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json**.</span></span>

    > [!WARNING]
    > <span data-ttu-id="0e72c-139">To guarantee availability of Kafka on HDInsight, your cluster must contain at least three worker nodes.</span><span class="sxs-lookup"><span data-stu-id="0e72c-139">To guarantee availability of Kafka on HDInsight, your cluster must contain at least three worker nodes.</span></span> <span data-ttu-id="0e72c-140">This template creates a Kafka cluster that contains three worker nodes.</span><span class="sxs-lookup"><span data-stu-id="0e72c-140">This template creates a Kafka cluster that contains three worker nodes.</span></span>

2. <span data-ttu-id="0e72c-141">Use the following information to populate the entries on the **Custom deployment** blade:</span><span class="sxs-lookup"><span data-stu-id="0e72c-141">Use the following information to populate the entries on the **Custom deployment** blade:</span></span>
    
    ![HDInsight custom deployment](./media/apache-kafka-mirroring/parameters.png)
    
    * <span data-ttu-id="0e72c-143">**Resource group**: Create a group or select an existing one.</span><span class="sxs-lookup"><span data-stu-id="0e72c-143">**Resource group**: Create a group or select an existing one.</span></span> <span data-ttu-id="0e72c-144">This group contains the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="0e72c-144">This group contains the HDInsight cluster.</span></span>

    * <span data-ttu-id="0e72c-145">**Location**: Select a location geographically close to you.</span><span class="sxs-lookup"><span data-stu-id="0e72c-145">**Location**: Select a location geographically close to you.</span></span>
     
    * <span data-ttu-id="0e72c-146">**Base Cluster Name**: This value is used as the base name for the Kafka clusters.</span><span class="sxs-lookup"><span data-stu-id="0e72c-146">**Base Cluster Name**: This value is used as the base name for the Kafka clusters.</span></span> <span data-ttu-id="0e72c-147">For example, entering **hdi** creates clusters named **source-hdi** and **dest-hdi**.</span><span class="sxs-lookup"><span data-stu-id="0e72c-147">For example, entering **hdi** creates clusters named **source-hdi** and **dest-hdi**.</span></span>

    * <span data-ttu-id="0e72c-148">**Cluster Login User Name**: The admin user name for the source and destination Kafka clusters.</span><span class="sxs-lookup"><span data-stu-id="0e72c-148">**Cluster Login User Name**: The admin user name for the source and destination Kafka clusters.</span></span>

    * <span data-ttu-id="0e72c-149">**Cluster Login Password**: The admin user password for the source and destination Kafka clusters.</span><span class="sxs-lookup"><span data-stu-id="0e72c-149">**Cluster Login Password**: The admin user password for the source and destination Kafka clusters.</span></span>

    * <span data-ttu-id="0e72c-150">**SSH User Name**: The SSH user to create for the source and destination Kafka clusters.</span><span class="sxs-lookup"><span data-stu-id="0e72c-150">**SSH User Name**: The SSH user to create for the source and destination Kafka clusters.</span></span>

    * <span data-ttu-id="0e72c-151">**SSH Password**: The password for the SSH user for the source and destination Kafka clusters.</span><span class="sxs-lookup"><span data-stu-id="0e72c-151">**SSH Password**: The password for the SSH user for the source and destination Kafka clusters.</span></span>

3. <span data-ttu-id="0e72c-152">Read the **Terms and Conditions**, and then select **I agree to the terms and conditions stated above**.</span><span class="sxs-lookup"><span data-stu-id="0e72c-152">Read the **Terms and Conditions**, and then select **I agree to the terms and conditions stated above**.</span></span>

4. <span data-ttu-id="0e72c-153">Finally, check **Pin to dashboard** and then select **Purchase**.</span><span class="sxs-lookup"><span data-stu-id="0e72c-153">Finally, check **Pin to dashboard** and then select **Purchase**.</span></span> <span data-ttu-id="0e72c-154">It takes about 20 minutes to create the clusters.</span><span class="sxs-lookup"><span data-stu-id="0e72c-154">It takes about 20 minutes to create the clusters.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0e72c-155">The name of the HDInsight clusters are **source-BASENAME** and **dest-BASENAME**, where BASENAME is the name you provided to the template.</span><span class="sxs-lookup"><span data-stu-id="0e72c-155">The name of the HDInsight clusters are **source-BASENAME** and **dest-BASENAME**, where BASENAME is the name you provided to the template.</span></span> <span data-ttu-id="0e72c-156">You use these names in later steps when connecting to the clusters.</span><span class="sxs-lookup"><span data-stu-id="0e72c-156">You use these names in later steps when connecting to the clusters.</span></span>

## <a name="create-topics"></a><span data-ttu-id="0e72c-157">Create topics</span><span class="sxs-lookup"><span data-stu-id="0e72c-157">Create topics</span></span>

1. <span data-ttu-id="0e72c-158">Connect to the **source** cluster using SSH:</span><span class="sxs-lookup"><span data-stu-id="0e72c-158">Connect to the **source** cluster using SSH:</span></span>

    ```bash
    ssh sshuser@source-BASENAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="0e72c-159">Replace **sshuser** with the SSH user name used when creating the cluster.</span><span class="sxs-lookup"><span data-stu-id="0e72c-159">Replace **sshuser** with the SSH user name used when creating the cluster.</span></span> <span data-ttu-id="0e72c-160">Replace **BASENAME** with the base name used when creating the cluster.</span><span class="sxs-lookup"><span data-stu-id="0e72c-160">Replace **BASENAME** with the base name used when creating the cluster.</span></span>

    <span data-ttu-id="0e72c-161">For information, see [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="0e72c-161">For information, see [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="0e72c-162">Use the following commands to find the Zookeeper hosts for the source cluster:</span><span class="sxs-lookup"><span data-stu-id="0e72c-162">Use the following commands to find the Zookeeper hosts for the source cluster:</span></span>

    ```bash
    # Install jq if it is not installed
    sudo apt -y install jq
    # get the zookeeper hosts for the source cluster
    export SOURCE_ZKHOSTS=`curl -sS -u admin -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`
    ```

    <span data-ttu-id="0e72c-163">Replace `$CLUSTERNAME` with the name of the source cluster.</span><span class="sxs-lookup"><span data-stu-id="0e72c-163">Replace `$CLUSTERNAME` with the name of the source cluster.</span></span> <span data-ttu-id="0e72c-164">When prompted, enter the password for the cluster login (admin) account.</span><span class="sxs-lookup"><span data-stu-id="0e72c-164">When prompted, enter the password for the cluster login (admin) account.</span></span>

3. <span data-ttu-id="0e72c-165">To create a topic named `testtopic`, use the following command:</span><span class="sxs-lookup"><span data-stu-id="0e72c-165">To create a topic named `testtopic`, use the following command:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 2 --partitions 8 --topic testtopic --zookeeper $SOURCE_ZKHOSTS
    ```

3. <span data-ttu-id="0e72c-166">Use the following command to verify that the topic was created:</span><span class="sxs-lookup"><span data-stu-id="0e72c-166">Use the following command to verify that the topic was created:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $SOURCE_ZKHOSTS
    ```

    <span data-ttu-id="0e72c-167">The response contains `testtopic`.</span><span class="sxs-lookup"><span data-stu-id="0e72c-167">The response contains `testtopic`.</span></span>

4. <span data-ttu-id="0e72c-168">Use the following to view the Zookeeper host information for this (the **source**) cluster:</span><span class="sxs-lookup"><span data-stu-id="0e72c-168">Use the following to view the Zookeeper host information for this (the **source**) cluster:</span></span>

    ```bash
    echo $SOURCE_ZKHOSTS
    ```

    <span data-ttu-id="0e72c-169">This returns information similar to the following text:</span><span class="sxs-lookup"><span data-stu-id="0e72c-169">This returns information similar to the following text:</span></span>

    `zk0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:2181,zk1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:2181`

    <span data-ttu-id="0e72c-170">Save this information.</span><span class="sxs-lookup"><span data-stu-id="0e72c-170">Save this information.</span></span> <span data-ttu-id="0e72c-171">It is used in the next section.</span><span class="sxs-lookup"><span data-stu-id="0e72c-171">It is used in the next section.</span></span>

## <a name="configure-mirroring"></a><span data-ttu-id="0e72c-172">Configure mirroring</span><span class="sxs-lookup"><span data-stu-id="0e72c-172">Configure mirroring</span></span>

1. <span data-ttu-id="0e72c-173">Connect to the **destination** cluster using a different SSH session:</span><span class="sxs-lookup"><span data-stu-id="0e72c-173">Connect to the **destination** cluster using a different SSH session:</span></span>

    ```bash
    ssh sshuser@dest-BASENAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="0e72c-174">Replace **sshuser** with the SSH user name used when creating the cluster.</span><span class="sxs-lookup"><span data-stu-id="0e72c-174">Replace **sshuser** with the SSH user name used when creating the cluster.</span></span> <span data-ttu-id="0e72c-175">Replace **BASENAME** with the base name used when creating the cluster.</span><span class="sxs-lookup"><span data-stu-id="0e72c-175">Replace **BASENAME** with the base name used when creating the cluster.</span></span>

    <span data-ttu-id="0e72c-176">For information, see [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="0e72c-176">For information, see [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="0e72c-177">A `consumer.properties` file is used to configure communication with the **source** cluster.</span><span class="sxs-lookup"><span data-stu-id="0e72c-177">A `consumer.properties` file is used to configure communication with the **source** cluster.</span></span> <span data-ttu-id="0e72c-178">To create the file, use the following command:</span><span class="sxs-lookup"><span data-stu-id="0e72c-178">To create the file, use the following command:</span></span>

    ```bash
    nano consumer.properties
    ```

    <span data-ttu-id="0e72c-179">Use the following text as the contents of the `consumer.properties` file:</span><span class="sxs-lookup"><span data-stu-id="0e72c-179">Use the following text as the contents of the `consumer.properties` file:</span></span>

    ```yaml
    zookeeper.connect=SOURCE_ZKHOSTS
    group.id=mirrorgroup
    ```

    <span data-ttu-id="0e72c-180">Replace **SOURCE_ZKHOSTS** with the Zookeeper hosts information from the **source** cluster.</span><span class="sxs-lookup"><span data-stu-id="0e72c-180">Replace **SOURCE_ZKHOSTS** with the Zookeeper hosts information from the **source** cluster.</span></span>

    <span data-ttu-id="0e72c-181">This file describes the consumer information to use when reading from the source Kafka cluster.</span><span class="sxs-lookup"><span data-stu-id="0e72c-181">This file describes the consumer information to use when reading from the source Kafka cluster.</span></span> <span data-ttu-id="0e72c-182">For more information consumer configuration, see [Consumer Configs](https://kafka.apache.org/documentation#consumerconfigs) at kafka.apache.org.</span><span class="sxs-lookup"><span data-stu-id="0e72c-182">For more information consumer configuration, see [Consumer Configs](https://kafka.apache.org/documentation#consumerconfigs) at kafka.apache.org.</span></span>

    <span data-ttu-id="0e72c-183">To save the file, use **Ctrl + X**, **Y**, and then **Enter**.</span><span class="sxs-lookup"><span data-stu-id="0e72c-183">To save the file, use **Ctrl + X**, **Y**, and then **Enter**.</span></span>

3. <span data-ttu-id="0e72c-184">Before configuring the producer that communicates with the destination cluster, you must find the broker hosts for the **destination** cluster.</span><span class="sxs-lookup"><span data-stu-id="0e72c-184">Before configuring the producer that communicates with the destination cluster, you must find the broker hosts for the **destination** cluster.</span></span> <span data-ttu-id="0e72c-185">Use the following commands to retrieve this information:</span><span class="sxs-lookup"><span data-stu-id="0e72c-185">Use the following commands to retrieve this information:</span></span>

    ```bash
    sudo apt -y install jq
    DEST_BROKERHOSTS=`curl -sS -u admin -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`
    echo $DEST_BROKERHOSTS
    ```

    <span data-ttu-id="0e72c-186">Replace `$CLUSTERNAME` with the name of the destination cluster.</span><span class="sxs-lookup"><span data-stu-id="0e72c-186">Replace `$CLUSTERNAME` with the name of the destination cluster.</span></span> <span data-ttu-id="0e72c-187">When prompted, enter the password for the cluster login (admin) account.</span><span class="sxs-lookup"><span data-stu-id="0e72c-187">When prompted, enter the password for the cluster login (admin) account.</span></span>

    <span data-ttu-id="0e72c-188">The `echo` command returns information similar to the following text:</span><span class="sxs-lookup"><span data-stu-id="0e72c-188">The `echo` command returns information similar to the following text:</span></span>

        wn0-dest.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn1-dest.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092

4. <span data-ttu-id="0e72c-189">A `producer.properties` file is used to communicate the __destination__ cluster.</span><span class="sxs-lookup"><span data-stu-id="0e72c-189">A `producer.properties` file is used to communicate the __destination__ cluster.</span></span> <span data-ttu-id="0e72c-190">To create the file, use the following command:</span><span class="sxs-lookup"><span data-stu-id="0e72c-190">To create the file, use the following command:</span></span>

    ```bash
    nano producer.properties
    ```

    <span data-ttu-id="0e72c-191">Use the following text as the contents of the `producer.properties` file:</span><span class="sxs-lookup"><span data-stu-id="0e72c-191">Use the following text as the contents of the `producer.properties` file:</span></span>

    ```yaml
    bootstrap.servers=DEST_BROKERS
    compression.type=none
    ```

    <span data-ttu-id="0e72c-192">Replace **DEST_BROKERS** with the broker information from the previous step.</span><span class="sxs-lookup"><span data-stu-id="0e72c-192">Replace **DEST_BROKERS** with the broker information from the previous step.</span></span>

    <span data-ttu-id="0e72c-193">For more information producer configuration, see [Producer Configs](https://kafka.apache.org/documentation#producerconfigs) at kafka.apache.org.</span><span class="sxs-lookup"><span data-stu-id="0e72c-193">For more information producer configuration, see [Producer Configs](https://kafka.apache.org/documentation#producerconfigs) at kafka.apache.org.</span></span>

5. <span data-ttu-id="0e72c-194">Use the following commands to find the Zookeeper hosts for the destination cluster:</span><span class="sxs-lookup"><span data-stu-id="0e72c-194">Use the following commands to find the Zookeeper hosts for the destination cluster:</span></span>

    ```bash
    # Install jq if it is not installed
    sudo apt -y install jq
    # get the zookeeper hosts for the source cluster
    export DEST_ZKHOSTS=`curl -sS -u admin -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`
    ```

    <span data-ttu-id="0e72c-195">Replace `$CLUSTERNAME` with the name of the destination cluster.</span><span class="sxs-lookup"><span data-stu-id="0e72c-195">Replace `$CLUSTERNAME` with the name of the destination cluster.</span></span> <span data-ttu-id="0e72c-196">When prompted, enter the password for the cluster login (admin) account.</span><span class="sxs-lookup"><span data-stu-id="0e72c-196">When prompted, enter the password for the cluster login (admin) account.</span></span>

7. <span data-ttu-id="0e72c-197">The default configuration for Kafka on HDInsight does not allow the automatic creation of topics.</span><span class="sxs-lookup"><span data-stu-id="0e72c-197">The default configuration for Kafka on HDInsight does not allow the automatic creation of topics.</span></span> <span data-ttu-id="0e72c-198">You must use one of the following options before starting the Mirroring process:</span><span class="sxs-lookup"><span data-stu-id="0e72c-198">You must use one of the following options before starting the Mirroring process:</span></span>

    * <span data-ttu-id="0e72c-199">**Create the topics on the destination cluster**: This option also allows you to set the number of partitions and the replication factor.</span><span class="sxs-lookup"><span data-stu-id="0e72c-199">**Create the topics on the destination cluster**: This option also allows you to set the number of partitions and the replication factor.</span></span>

        <span data-ttu-id="0e72c-200">You can create topics ahead of time by using the following command:</span><span class="sxs-lookup"><span data-stu-id="0e72c-200">You can create topics ahead of time by using the following command:</span></span>

        ```bash
        /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 2 --partitions 8 --topic testtopic --zookeeper $DEST_ZKHOSTS
        ```

        <span data-ttu-id="0e72c-201">Replace `testtopic` with the name of the topic to create.</span><span class="sxs-lookup"><span data-stu-id="0e72c-201">Replace `testtopic` with the name of the topic to create.</span></span>

    * <span data-ttu-id="0e72c-202">**Configure the cluster for automatic topic creation**: This option allows MirrorMaker to automatically create topics, however it may create them with a different number of partitions or replication factor than the source topic.</span><span class="sxs-lookup"><span data-stu-id="0e72c-202">**Configure the cluster for automatic topic creation**: This option allows MirrorMaker to automatically create topics, however it may create them with a different number of partitions or replication factor than the source topic.</span></span>

        <span data-ttu-id="0e72c-203">To configure the destination cluster to automatically create topics, perform these steps:</span><span class="sxs-lookup"><span data-stu-id="0e72c-203">To configure the destination cluster to automatically create topics, perform these steps:</span></span>

        1. <span data-ttu-id="0e72c-204">From the [Azure portal](https://portal.azure.com), select the destination Kafka cluster.</span><span class="sxs-lookup"><span data-stu-id="0e72c-204">From the [Azure portal](https://portal.azure.com), select the destination Kafka cluster.</span></span>
        2. <span data-ttu-id="0e72c-205">From the cluster overview, select __Cluster dashboard__.</span><span class="sxs-lookup"><span data-stu-id="0e72c-205">From the cluster overview, select __Cluster dashboard__.</span></span> <span data-ttu-id="0e72c-206">Then select __HDInsight cluster dashboard__.</span><span class="sxs-lookup"><span data-stu-id="0e72c-206">Then select __HDInsight cluster dashboard__.</span></span> <span data-ttu-id="0e72c-207">When prompted, authenticate using the login (admin) credentials for the cluster.</span><span class="sxs-lookup"><span data-stu-id="0e72c-207">When prompted, authenticate using the login (admin) credentials for the cluster.</span></span>
        3. <span data-ttu-id="0e72c-208">Select the __Kafka__ service from the list on the left of the page.</span><span class="sxs-lookup"><span data-stu-id="0e72c-208">Select the __Kafka__ service from the list on the left of the page.</span></span>
        4. <span data-ttu-id="0e72c-209">Select __Configs__ in the middle of the page.</span><span class="sxs-lookup"><span data-stu-id="0e72c-209">Select __Configs__ in the middle of the page.</span></span>
        5. <span data-ttu-id="0e72c-210">In the __Filter__ field, enter a value of `auto.create`.</span><span class="sxs-lookup"><span data-stu-id="0e72c-210">In the __Filter__ field, enter a value of `auto.create`.</span></span> <span data-ttu-id="0e72c-211">This filters the list of properties and displays the `auto.create.topics.enable` setting.</span><span class="sxs-lookup"><span data-stu-id="0e72c-211">This filters the list of properties and displays the `auto.create.topics.enable` setting.</span></span>
        6. <span data-ttu-id="0e72c-212">Change the value of `auto.create.topics.enable` to true, and then select __Save__.</span><span class="sxs-lookup"><span data-stu-id="0e72c-212">Change the value of `auto.create.topics.enable` to true, and then select __Save__.</span></span> <span data-ttu-id="0e72c-213">Add a note, and then select __Save__ again.</span><span class="sxs-lookup"><span data-stu-id="0e72c-213">Add a note, and then select __Save__ again.</span></span>
        7. <span data-ttu-id="0e72c-214">Select the __Kafka__ service, select __Restart__, and then select __Restart all affected__.</span><span class="sxs-lookup"><span data-stu-id="0e72c-214">Select the __Kafka__ service, select __Restart__, and then select __Restart all affected__.</span></span> <span data-ttu-id="0e72c-215">When prompted, select __Confirm restart all__.</span><span class="sxs-lookup"><span data-stu-id="0e72c-215">When prompted, select __Confirm restart all__.</span></span>

## <a name="start-mirrormaker"></a><span data-ttu-id="0e72c-216">Start MirrorMaker</span><span class="sxs-lookup"><span data-stu-id="0e72c-216">Start MirrorMaker</span></span>

1. <span data-ttu-id="0e72c-217">From the SSH connection to the **destination** cluster, use the following command to start the MirrorMaker process:</span><span class="sxs-lookup"><span data-stu-id="0e72c-217">From the SSH connection to the **destination** cluster, use the following command to start the MirrorMaker process:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-run-class.sh kafka.tools.MirrorMaker --consumer.config consumer.properties --producer.config producer.properties --whitelist testtopic --num.streams 4
    ```

    <span data-ttu-id="0e72c-218">The parameters used in this example are:</span><span class="sxs-lookup"><span data-stu-id="0e72c-218">The parameters used in this example are:</span></span>

    * <span data-ttu-id="0e72c-219">**--consumer.config**: Specifies the file that contains consumer properties.</span><span class="sxs-lookup"><span data-stu-id="0e72c-219">**--consumer.config**: Specifies the file that contains consumer properties.</span></span> <span data-ttu-id="0e72c-220">These properties are used to create a consumer that reads from the *source* Kafka cluster.</span><span class="sxs-lookup"><span data-stu-id="0e72c-220">These properties are used to create a consumer that reads from the *source* Kafka cluster.</span></span>

    * <span data-ttu-id="0e72c-221">**--producer.config**: Specifies the file that contains producer properties.</span><span class="sxs-lookup"><span data-stu-id="0e72c-221">**--producer.config**: Specifies the file that contains producer properties.</span></span> <span data-ttu-id="0e72c-222">These properties are used to create a producer that writes to the *destination* Kafka cluster.</span><span class="sxs-lookup"><span data-stu-id="0e72c-222">These properties are used to create a producer that writes to the *destination* Kafka cluster.</span></span>

    * <span data-ttu-id="0e72c-223">**--whitelist**: A list of topics that MirrorMaker replicates from the source cluster to the destination.</span><span class="sxs-lookup"><span data-stu-id="0e72c-223">**--whitelist**: A list of topics that MirrorMaker replicates from the source cluster to the destination.</span></span>

    * <span data-ttu-id="0e72c-224">**--num.streams**: The number of consumer threads to create.</span><span class="sxs-lookup"><span data-stu-id="0e72c-224">**--num.streams**: The number of consumer threads to create.</span></span>

 <span data-ttu-id="0e72c-225">On startup, MirrorMaker returns information similar to the following text:</span><span class="sxs-lookup"><span data-stu-id="0e72c-225">On startup, MirrorMaker returns information similar to the following text:</span></span>

    ```json
    {metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-3, security.protocol=PLAINTEXT}{metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-0, security.protocol=PLAINTEXT}
    metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-kafka.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-2, security.protocol=PLAINTEXT}
    metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-1, security.protocol=PLAINTEXT}
    ```

2. <span data-ttu-id="0e72c-226">From the SSH connection to the **source** cluster, use the following command to start a producer and send messages to the topic:</span><span class="sxs-lookup"><span data-stu-id="0e72c-226">From the SSH connection to the **source** cluster, use the following command to start a producer and send messages to the topic:</span></span>

    ```bash
    SOURCE_BROKERHOSTS=`curl -sS -u admin -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`
    /usr/hdp/current/kafka-broker/bin/kafka-console-producer.sh --broker-list $SOURCE_BROKERHOSTS --topic testtopic
    ```

    <span data-ttu-id="0e72c-227">Replace `$CLUSTERNAME` with the name of the source cluster.</span><span class="sxs-lookup"><span data-stu-id="0e72c-227">Replace `$CLUSTERNAME` with the name of the source cluster.</span></span> <span data-ttu-id="0e72c-228">When prompted, enter the password for the cluster login (admin) account.</span><span class="sxs-lookup"><span data-stu-id="0e72c-228">When prompted, enter the password for the cluster login (admin) account.</span></span>

     <span data-ttu-id="0e72c-229">When you arrive at a blank line with a cursor, type in a few text messages.</span><span class="sxs-lookup"><span data-stu-id="0e72c-229">When you arrive at a blank line with a cursor, type in a few text messages.</span></span> <span data-ttu-id="0e72c-230">The messages are sent to the topic on the **source** cluster.</span><span class="sxs-lookup"><span data-stu-id="0e72c-230">The messages are sent to the topic on the **source** cluster.</span></span> <span data-ttu-id="0e72c-231">When done, use **Ctrl + C** to end the producer process.</span><span class="sxs-lookup"><span data-stu-id="0e72c-231">When done, use **Ctrl + C** to end the producer process.</span></span>

3. <span data-ttu-id="0e72c-232">From the SSH connection to the **destination** cluster, use **Ctrl + C** to end the MirrorMaker process.</span><span class="sxs-lookup"><span data-stu-id="0e72c-232">From the SSH connection to the **destination** cluster, use **Ctrl + C** to end the MirrorMaker process.</span></span> <span data-ttu-id="0e72c-233">It may take several seconds to end the process.</span><span class="sxs-lookup"><span data-stu-id="0e72c-233">It may take several seconds to end the process.</span></span> <span data-ttu-id="0e72c-234">To verify that the messages were replicated to the destination, use the following command:</span><span class="sxs-lookup"><span data-stu-id="0e72c-234">To verify that the messages were replicated to the destination, use the following command:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --zookeeper $DEST_ZKHOSTS --topic testtopic --from-beginning
    ```

    <span data-ttu-id="0e72c-235">Replace `$CLUSTERNAME` with the name of the destination cluster.</span><span class="sxs-lookup"><span data-stu-id="0e72c-235">Replace `$CLUSTERNAME` with the name of the destination cluster.</span></span> <span data-ttu-id="0e72c-236">When prompted, enter the password for the cluster login (admin) account.</span><span class="sxs-lookup"><span data-stu-id="0e72c-236">When prompted, enter the password for the cluster login (admin) account.</span></span>

    <span data-ttu-id="0e72c-237">The list of topics now includes `testtopic`, which is created when MirrorMaster mirrors the topic from the source cluster to the destination.</span><span class="sxs-lookup"><span data-stu-id="0e72c-237">The list of topics now includes `testtopic`, which is created when MirrorMaster mirrors the topic from the source cluster to the destination.</span></span> <span data-ttu-id="0e72c-238">The messages retrieved from the topic are the same as entered on the source cluster.</span><span class="sxs-lookup"><span data-stu-id="0e72c-238">The messages retrieved from the topic are the same as entered on the source cluster.</span></span>

## <a name="delete-the-cluster"></a><span data-ttu-id="0e72c-239">Delete the cluster</span><span class="sxs-lookup"><span data-stu-id="0e72c-239">Delete the cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="0e72c-240">Since the steps in this document create both clusters in the same Azure resource group, you can delete the resource group in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="0e72c-240">Since the steps in this document create both clusters in the same Azure resource group, you can delete the resource group in the Azure portal.</span></span> <span data-ttu-id="0e72c-241">Deleting the resource group removes all resources created by following this document, the Azure Virtual Network, and storage account used by the clusters.</span><span class="sxs-lookup"><span data-stu-id="0e72c-241">Deleting the resource group removes all resources created by following this document, the Azure Virtual Network, and storage account used by the clusters.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0e72c-242">Next Steps</span><span class="sxs-lookup"><span data-stu-id="0e72c-242">Next Steps</span></span>

<span data-ttu-id="0e72c-243">In this document, you learned how to use MirrorMaker to create a replica of a Kafka cluster.</span><span class="sxs-lookup"><span data-stu-id="0e72c-243">In this document, you learned how to use MirrorMaker to create a replica of a Kafka cluster.</span></span> <span data-ttu-id="0e72c-244">Use the following links to discover other ways to work with Kafka:</span><span class="sxs-lookup"><span data-stu-id="0e72c-244">Use the following links to discover other ways to work with Kafka:</span></span>

* <span data-ttu-id="0e72c-245">[Apache Kafka MirrorMaker documentation](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=27846330) at cwiki.apache.org.</span><span class="sxs-lookup"><span data-stu-id="0e72c-245">[Apache Kafka MirrorMaker documentation](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=27846330) at cwiki.apache.org.</span></span>
* [<span data-ttu-id="0e72c-246">Get started with Apache Kafka on HDInsight</span><span class="sxs-lookup"><span data-stu-id="0e72c-246">Get started with Apache Kafka on HDInsight</span></span>](apache-kafka-get-started.md)
* [<span data-ttu-id="0e72c-247">Use Apache Spark with Kafka on HDInsight</span><span class="sxs-lookup"><span data-stu-id="0e72c-247">Use Apache Spark with Kafka on HDInsight</span></span>](../hdinsight-apache-spark-with-kafka.md)
* [<span data-ttu-id="0e72c-248">Use Apache Storm with Kafka on HDInsight</span><span class="sxs-lookup"><span data-stu-id="0e72c-248">Use Apache Storm with Kafka on HDInsight</span></span>](../hdinsight-apache-storm-with-kafka.md)
* [<span data-ttu-id="0e72c-249">Connect to Kafka through an Azure Virtual Network</span><span class="sxs-lookup"><span data-stu-id="0e72c-249">Connect to Kafka through an Azure Virtual Network</span></span>](apache-kafka-connect-vpn-gateway.md)
