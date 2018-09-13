---
title: Mirror your Apache Kafka on HDInsight cluster | Microsoft Docs
description: Learn how to use Kafka's mirroring feature to maintain a replica of a Kafka on HDInsight cluster by mirroring topics to a secondary cluster.
services: hdinsight
documentationcenter: ''
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 015d276e-f678-4f2b-9572-75553c56625b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 02/13/2017
ms.author: larryfr
ms.openlocfilehash: 999150bed0638f5ff2cf9047c3035916d4e64c1b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44548906"
---
# <a name="use-mirrormaker-to-create-a-replica-of-a-kafka-on-hdinsight-cluster-preview"></a><span data-ttu-id="57e09-103">Use MirrorMaker to create a replica of a Kafka on HDInsight cluster (preview)</span><span class="sxs-lookup"><span data-stu-id="57e09-103">Use MirrorMaker to create a replica of a Kafka on HDInsight cluster (preview)</span></span>

<span data-ttu-id="57e09-104">Apache Kafka includes a mirroring feature, which allows you to replicate topics from one Kafka cluster to another.</span><span class="sxs-lookup"><span data-stu-id="57e09-104">Apache Kafka includes a mirroring feature, which allows you to replicate topics from one Kafka cluster to another.</span></span> <span data-ttu-id="57e09-105">For example, replicating records between Kafka cluster in different Azure regions.</span><span class="sxs-lookup"><span data-stu-id="57e09-105">For example, replicating records between Kafka cluster in different Azure regions.</span></span>

<span data-ttu-id="57e09-106">Mirroring can be ran as a continuous process, or used intermittently as a method of migrating data from one cluster to another.</span><span class="sxs-lookup"><span data-stu-id="57e09-106">Mirroring can be ran as a continuous process, or used intermittently as a method of migrating data from one cluster to another.</span></span>

> [!WARNING]
> <span data-ttu-id="57e09-107">Mirroring should not be considered as a means to achieve fault-tolerance.</span><span class="sxs-lookup"><span data-stu-id="57e09-107">Mirroring should not be considered as a means to achieve fault-tolerance.</span></span> <span data-ttu-id="57e09-108">The offset to items within a topic are different between the source and destination clusters, so clients cannot use the two interchangeably.</span><span class="sxs-lookup"><span data-stu-id="57e09-108">The offset to items within a topic are different between the source and destination clusters, so clients cannot use the two interchangeably.</span></span>
> 
> <span data-ttu-id="57e09-109">If you are concerned about fault tolerance, you should set replication for the topics within your cluster.</span><span class="sxs-lookup"><span data-stu-id="57e09-109">If you are concerned about fault tolerance, you should set replication for the topics within your cluster.</span></span> <span data-ttu-id="57e09-110">For more information, see [Get started with Kafka on HDInsight](hdinsight-apache-kafka-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="57e09-110">For more information, see [Get started with Kafka on HDInsight](hdinsight-apache-kafka-get-started.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="57e09-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="57e09-111">Prerequisites</span></span>

* <span data-ttu-id="57e09-112">An Azure Virtual Network: The source and destination Kafka clusters must be able to directly communicate with each other.</span><span class="sxs-lookup"><span data-stu-id="57e09-112">An Azure Virtual Network: The source and destination Kafka clusters must be able to directly communicate with each other.</span></span> <span data-ttu-id="57e09-113">HDInsight does not expose Kafka APIs publicly on the internet, so both the source and destination clusters must exist in the same Azure Virtual Network.</span><span class="sxs-lookup"><span data-stu-id="57e09-113">HDInsight does not expose Kafka APIs publicly on the internet, so both the source and destination clusters must exist in the same Azure Virtual Network.</span></span>

* <span data-ttu-id="57e09-114">Two Kafka clusters: This document uses an Azure Resource Manager template to create two Kafka on HDInsight clusters within an Azure Virtual Network.</span><span class="sxs-lookup"><span data-stu-id="57e09-114">Two Kafka clusters: This document uses an Azure Resource Manager template to create two Kafka on HDInsight clusters within an Azure Virtual Network.</span></span>

## <a name="how-does-mirroring-work"></a><span data-ttu-id="57e09-115">How does mirroring work?</span><span class="sxs-lookup"><span data-stu-id="57e09-115">How does mirroring work?</span></span>

<span data-ttu-id="57e09-116">Mirroring works by using the MirrorMaker tool (part of Apache Kafka) to consume records from topics on the source cluster and then create a local copy on the destination cluster.</span><span class="sxs-lookup"><span data-stu-id="57e09-116">Mirroring works by using the MirrorMaker tool (part of Apache Kafka) to consume records from topics on the source cluster and then create a local copy on the destination cluster.</span></span> <span data-ttu-id="57e09-117">MirrorMaker uses one (or more) *consumers* that read from the source cluster, and a *producer* that writes to the local (destination) cluster.</span><span class="sxs-lookup"><span data-stu-id="57e09-117">MirrorMaker uses one (or more) *consumers* that read from the source cluster, and a *producer* that writes to the local (destination) cluster.</span></span>

<span data-ttu-id="57e09-118">The following diagram illustrates the Mirroring process:</span><span class="sxs-lookup"><span data-stu-id="57e09-118">The following diagram illustrates the Mirroring process:</span></span>

![Diagram of the mirroring process](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-kafka-mirroring/kafka-mirroring.png)

<span data-ttu-id="57e09-120">The source and destination clusters can be different in the number of nodes and partitions, and offsets within the topics are different also.</span><span class="sxs-lookup"><span data-stu-id="57e09-120">The source and destination clusters can be different in the number of nodes and partitions, and offsets within the topics are different also.</span></span> <span data-ttu-id="57e09-121">Mirroring maintains the key value that is used for partitioning, so record order is preserved on a per-key basis.</span><span class="sxs-lookup"><span data-stu-id="57e09-121">Mirroring maintains the key value that is used for partitioning, so record order is preserved on a per-key basis.</span></span>

### <a name="mirroring-between-networks"></a><span data-ttu-id="57e09-122">Mirroring between networks</span><span class="sxs-lookup"><span data-stu-id="57e09-122">Mirroring between networks</span></span>

<span data-ttu-id="57e09-123">If you need to mirror between Kafka clusters in different networks, there are the following additional considerations:</span><span class="sxs-lookup"><span data-stu-id="57e09-123">If you need to mirror between Kafka clusters in different networks, there are the following additional considerations:</span></span>

* <span data-ttu-id="57e09-124">**Gateways**: The networks must be able to communicate at the TCPIP level.</span><span class="sxs-lookup"><span data-stu-id="57e09-124">**Gateways**: The networks must be able to communicate at the TCPIP level.</span></span>

* <span data-ttu-id="57e09-125">**Name resolution**: The Kafka clusters in each network must be able to connect to each other by using hostnames.</span><span class="sxs-lookup"><span data-stu-id="57e09-125">**Name resolution**: The Kafka clusters in each network must be able to connect to each other by using hostnames.</span></span> <span data-ttu-id="57e09-126">This may require a Domain Name System (DNS) server in each network that is configured to forward requests to the other networks.</span><span class="sxs-lookup"><span data-stu-id="57e09-126">This may require a Domain Name System (DNS) server in each network that is configured to forward requests to the other networks.</span></span> 
  
    <span data-ttu-id="57e09-127">When creating an Azure Virtual Network, instead of using the automatic DNS provided with the network, you must specify a custom DNS server and the IP address for the server.</span><span class="sxs-lookup"><span data-stu-id="57e09-127">When creating an Azure Virtual Network, instead of using the automatic DNS provided with the network, you must specify a custom DNS server and the IP address for the server.</span></span> <span data-ttu-id="57e09-128">After the Virtual Network has been created, you must then create an Azure Virtual Machine that uses that IP address, then install and configure DNS software on it.</span><span class="sxs-lookup"><span data-stu-id="57e09-128">After the Virtual Network has been created, you must then create an Azure Virtual Machine that uses that IP address, then install and configure DNS software on it.</span></span>
  
    > [!WARNING]
    > <span data-ttu-id="57e09-129">Create and configure the custom DNS server before installing HDInsight into the Virtual Network.</span><span class="sxs-lookup"><span data-stu-id="57e09-129">Create and configure the custom DNS server before installing HDInsight into the Virtual Network.</span></span> <span data-ttu-id="57e09-130">There is no additional configuration required for HDInsight to use the DNS server configured for the Virtual Network.</span><span class="sxs-lookup"><span data-stu-id="57e09-130">There is no additional configuration required for HDInsight to use the DNS server configured for the Virtual Network.</span></span>

<span data-ttu-id="57e09-131">For more information on connecting two Azure Virtual Networks, see [Configure a VNet-to-VNet connection](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="57e09-131">For more information on connecting two Azure Virtual Networks, see [Configure a VNet-to-VNet connection](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).</span></span>

## <a name="create-kafka-clusters"></a><span data-ttu-id="57e09-132">Create Kafka clusters</span><span class="sxs-lookup"><span data-stu-id="57e09-132">Create Kafka clusters</span></span>

<span data-ttu-id="57e09-133">Apache Kafka on HDInsight does not provide access to the Kafka service over the public internet.</span><span class="sxs-lookup"><span data-stu-id="57e09-133">Apache Kafka on HDInsight does not provide access to the Kafka service over the public internet.</span></span> <span data-ttu-id="57e09-134">Anything that talks to Kafka must be in the same Azure virtual network as the nodes in the Kafka cluster.</span><span class="sxs-lookup"><span data-stu-id="57e09-134">Anything that talks to Kafka must be in the same Azure virtual network as the nodes in the Kafka cluster.</span></span> <span data-ttu-id="57e09-135">For this example, both the Kafka source and destination clusters are located in an Azure virtual network.</span><span class="sxs-lookup"><span data-stu-id="57e09-135">For this example, both the Kafka source and destination clusters are located in an Azure virtual network.</span></span> <span data-ttu-id="57e09-136">The following diagram shows how communication flows between the clusters:</span><span class="sxs-lookup"><span data-stu-id="57e09-136">The following diagram shows how communication flows between the clusters:</span></span>

![Diagram of source and destination Kafka clusters in an Azure virtual network](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-kafka-mirroring/spark-kafka-vnet.png)

> [!NOTE]
> <span data-ttu-id="57e09-138">Though Kafka itself is limited to communication within the virtual network, other services on the cluster such as SSH and Ambari can be accessed over the internet.</span><span class="sxs-lookup"><span data-stu-id="57e09-138">Though Kafka itself is limited to communication within the virtual network, other services on the cluster such as SSH and Ambari can be accessed over the internet.</span></span> <span data-ttu-id="57e09-139">For more information on the public ports available with HDInsight, see [Ports and URIs used by HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span><span class="sxs-lookup"><span data-stu-id="57e09-139">For more information on the public ports available with HDInsight, see [Ports and URIs used by HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span></span>

<span data-ttu-id="57e09-140">While you can create an Azure virtual network and Kafka clusters manually, it's easier to use an Azure Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="57e09-140">While you can create an Azure virtual network and Kafka clusters manually, it's easier to use an Azure Resource Manager template.</span></span> <span data-ttu-id="57e09-141">Use the following steps to deploy an Azure virtual network and two Kafka clusters to your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="57e09-141">Use the following steps to deploy an Azure virtual network and two Kafka clusters to your Azure subscription.</span></span>

1. <span data-ttu-id="57e09-142">Use the following button to sign in to Azure and open the template in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="57e09-142">Use the following button to sign in to Azure and open the template in the Azure portal.</span></span>
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-mirror-cluster-in-vnet.json" target="_blank"><img src="https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-kafka-mirroring/deploy-to-azure.png" alt="Deploy to Azure"></a>
   
    <span data-ttu-id="57e09-143">The Azure Resource Manager template is located at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet.json**.</span><span class="sxs-lookup"><span data-stu-id="57e09-143">The Azure Resource Manager template is located at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet.json**.</span></span>

2. <span data-ttu-id="57e09-144">Use the following information to populate the entries on the **Custom deployment** blade:</span><span class="sxs-lookup"><span data-stu-id="57e09-144">Use the following information to populate the entries on the **Custom deployment** blade:</span></span>
    
    ![HDInsight custom deployment](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-kafka-mirroring/parameters.png)
    
    * <span data-ttu-id="57e09-146">**Resource group**: Create a group or select an existing one.</span><span class="sxs-lookup"><span data-stu-id="57e09-146">**Resource group**: Create a group or select an existing one.</span></span> <span data-ttu-id="57e09-147">This group contains the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="57e09-147">This group contains the HDInsight cluster.</span></span>

    * <span data-ttu-id="57e09-148">**Location**: Select a location geographically close to you.</span><span class="sxs-lookup"><span data-stu-id="57e09-148">**Location**: Select a location geographically close to you.</span></span> <span data-ttu-id="57e09-149">This location must match the location in the __SETTINGS__ section.</span><span class="sxs-lookup"><span data-stu-id="57e09-149">This location must match the location in the __SETTINGS__ section.</span></span>
     
    * <span data-ttu-id="57e09-150">**Base Cluster Name**: This value is used as the base name for the Kafka clusters.</span><span class="sxs-lookup"><span data-stu-id="57e09-150">**Base Cluster Name**: This value is used as the base name for the Kafka clusters.</span></span> <span data-ttu-id="57e09-151">For example, entering **hdi** creates clusters named **source-hdi** and **dest-hdi**.</span><span class="sxs-lookup"><span data-stu-id="57e09-151">For example, entering **hdi** creates clusters named **source-hdi** and **dest-hdi**.</span></span>

    * <span data-ttu-id="57e09-152">**Cluster Login User Name**: The admin user name for the source and destination Kafka clusters.</span><span class="sxs-lookup"><span data-stu-id="57e09-152">**Cluster Login User Name**: The admin user name for the source and destination Kafka clusters.</span></span>

    * <span data-ttu-id="57e09-153">**Cluster Login Password**: The admin user password for the source and destination Kafka clusters.</span><span class="sxs-lookup"><span data-stu-id="57e09-153">**Cluster Login Password**: The admin user password for the source and destination Kafka clusters.</span></span>

    * <span data-ttu-id="57e09-154">**SSH User Name**: The SSH user to create for the source and destination Kafka clusters.</span><span class="sxs-lookup"><span data-stu-id="57e09-154">**SSH User Name**: The SSH user to create for the source and destination Kafka clusters.</span></span>

    * <span data-ttu-id="57e09-155">**SSH Password**: The password for the SSH user for the source and destination Kafka clusters.</span><span class="sxs-lookup"><span data-stu-id="57e09-155">**SSH Password**: The password for the SSH user for the source and destination Kafka clusters.</span></span>

    * <span data-ttu-id="57e09-156">**Location**: The region that the clusters are created in.</span><span class="sxs-lookup"><span data-stu-id="57e09-156">**Location**: The region that the clusters are created in.</span></span>

3. <span data-ttu-id="57e09-157">Read the **Terms and Conditions**, and then select **I agree to the terms and conditions stated above**.</span><span class="sxs-lookup"><span data-stu-id="57e09-157">Read the **Terms and Conditions**, and then select **I agree to the terms and conditions stated above**.</span></span>

4. <span data-ttu-id="57e09-158">Finally, check **Pin to dashboard** and then select **Purchase**.</span><span class="sxs-lookup"><span data-stu-id="57e09-158">Finally, check **Pin to dashboard** and then select **Purchase**.</span></span> <span data-ttu-id="57e09-159">It takes about 20 minutes to create the clusters.</span><span class="sxs-lookup"><span data-stu-id="57e09-159">It takes about 20 minutes to create the clusters.</span></span>

<span data-ttu-id="57e09-160">Once the resources have been created, you are redirected to a blade for the resource group that contains the clusters and web dashboard.</span><span class="sxs-lookup"><span data-stu-id="57e09-160">Once the resources have been created, you are redirected to a blade for the resource group that contains the clusters and web dashboard.</span></span>

![Resource group blade for the vnet and clusters](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-kafka-mirroring/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="57e09-162">Notice that the names of the HDInsight clusters are **source-BASENAME** and **dest-BASENAME**, where BASENAME is the name you provided to the template.</span><span class="sxs-lookup"><span data-stu-id="57e09-162">Notice that the names of the HDInsight clusters are **source-BASENAME** and **dest-BASENAME**, where BASENAME is the name you provided to the template.</span></span> <span data-ttu-id="57e09-163">You use these names in later steps when connecting to the clusters.</span><span class="sxs-lookup"><span data-stu-id="57e09-163">You use these names in later steps when connecting to the clusters.</span></span>

## <a name="create-topics"></a><span data-ttu-id="57e09-164">Create topics</span><span class="sxs-lookup"><span data-stu-id="57e09-164">Create topics</span></span>

1. <span data-ttu-id="57e09-165">Connect to the **source** cluster using SSH:</span><span class="sxs-lookup"><span data-stu-id="57e09-165">Connect to the **source** cluster using SSH:</span></span>
   
        ssh sshuser@source-BASENAME-ssh.azurehdinsight.net
   
    <span data-ttu-id="57e09-166">Replace **sshuser** with the SSH user name used when creating the cluster.</span><span class="sxs-lookup"><span data-stu-id="57e09-166">Replace **sshuser** with the SSH user name used when creating the cluster.</span></span> <span data-ttu-id="57e09-167">Replace **BASENAME** with the base name used when creating the cluster.</span><span class="sxs-lookup"><span data-stu-id="57e09-167">Replace **BASENAME** with the base name used when creating the cluster.</span></span>
   
    <span data-ttu-id="57e09-168">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="57e09-168">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="57e09-169">Use the following command to find the Zookeeper hosts, set the `SOURCE_ZKHOSTS` variable, and then create several new topics named `testtopic`:</span><span class="sxs-lookup"><span data-stu-id="57e09-169">Use the following command to find the Zookeeper hosts, set the `SOURCE_ZKHOSTS` variable, and then create several new topics named `testtopic`:</span></span>
   
    ```bash
    SOURCE_ZKHOSTS=`grep -R zk /etc/hadoop/conf/yarn-site.xml | grep 2181 | grep -oPm1 "(?<=<value>)[^<]+"`
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 2 --partitions 8 --topic testtopic --zookeeper $SOURCE_ZKHOSTS
    ```

3. <span data-ttu-id="57e09-170">Use the following command to verify that the topic was created:</span><span class="sxs-lookup"><span data-stu-id="57e09-170">Use the following command to verify that the topic was created:</span></span>
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $SOURCE_ZKHOSTS
    ```
   
    <span data-ttu-id="57e09-171">The response contains `testtopic`.</span><span class="sxs-lookup"><span data-stu-id="57e09-171">The response contains `testtopic`.</span></span>

4. <span data-ttu-id="57e09-172">Use the following to view the Zookeeper host information for this (the **source**) cluster:</span><span class="sxs-lookup"><span data-stu-id="57e09-172">Use the following to view the Zookeeper host information for this (the **source**) cluster:</span></span>
   
    ```bash
    echo $SOURCE_ZKHOSTS
    ```
   
 <span data-ttu-id="57e09-173">This returns information similar to the following text:</span><span class="sxs-lookup"><span data-stu-id="57e09-173">This returns information similar to the following text:</span></span>
   
       zk0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:2181,zk1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:2181,zk6-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:2181
   
 <span data-ttu-id="57e09-174">Save this information.</span><span class="sxs-lookup"><span data-stu-id="57e09-174">Save this information.</span></span> <span data-ttu-id="57e09-175">It is used in the next section.</span><span class="sxs-lookup"><span data-stu-id="57e09-175">It is used in the next section.</span></span>

## <a name="configure-mirroring"></a><span data-ttu-id="57e09-176">Configure mirroring</span><span class="sxs-lookup"><span data-stu-id="57e09-176">Configure mirroring</span></span>

1. <span data-ttu-id="57e09-177">Connect to the **destination** cluster using a different SSH session:</span><span class="sxs-lookup"><span data-stu-id="57e09-177">Connect to the **destination** cluster using a different SSH session:</span></span>
   
        ssh sshuser@dest-BASENAME-ssh.azurehdinsight.net
   
    <span data-ttu-id="57e09-178">Replace **sshuser** with the SSH user name used when creating the cluster.</span><span class="sxs-lookup"><span data-stu-id="57e09-178">Replace **sshuser** with the SSH user name used when creating the cluster.</span></span> <span data-ttu-id="57e09-179">Replace **BASENAME** with the base name used when creating the cluster.</span><span class="sxs-lookup"><span data-stu-id="57e09-179">Replace **BASENAME** with the base name used when creating the cluster.</span></span>
   
    <span data-ttu-id="57e09-180">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="57e09-180">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="57e09-181">Use the following command to create a `consumer.properties` file that describes how to communicate with the **source** cluster:</span><span class="sxs-lookup"><span data-stu-id="57e09-181">Use the following command to create a `consumer.properties` file that describes how to communicate with the **source** cluster:</span></span>
   
    ```bash
    nano consumer.properties
    ```
   
    <span data-ttu-id="57e09-182">Use the following text as the contents of the `consumer.properties` file:</span><span class="sxs-lookup"><span data-stu-id="57e09-182">Use the following text as the contents of the `consumer.properties` file:</span></span>
   
        zookeeper.connect=SOURCE_ZKHOSTS
        group.id=mirrorgroup
   
    <span data-ttu-id="57e09-183">Replace **SOURCE_ZKHOSTS** with the Zookeeper hosts information from the **source** cluster.</span><span class="sxs-lookup"><span data-stu-id="57e09-183">Replace **SOURCE_ZKHOSTS** with the Zookeeper hosts information from the **source** cluster.</span></span>
   
    <span data-ttu-id="57e09-184">This file describes the consumer information to use when reading from the source Kafka cluster.</span><span class="sxs-lookup"><span data-stu-id="57e09-184">This file describes the consumer information to use when reading from the source Kafka cluster.</span></span> <span data-ttu-id="57e09-185">For more information consumer configuration, see [Consumer Configs](https://kafka.apache.org/documentation#consumerconfigs) at kafka.apache.org.</span><span class="sxs-lookup"><span data-stu-id="57e09-185">For more information consumer configuration, see [Consumer Configs](https://kafka.apache.org/documentation#consumerconfigs) at kafka.apache.org.</span></span>
   
    <span data-ttu-id="57e09-186">Use **Ctrl + X**, **Y**, and Enter to save the file.</span><span class="sxs-lookup"><span data-stu-id="57e09-186">Use **Ctrl + X**, **Y**, and Enter to save the file.</span></span>

3. <span data-ttu-id="57e09-187">Before configuring the producer that communicates with the destination cluster, you must find the broker hosts for the **destination** cluster.</span><span class="sxs-lookup"><span data-stu-id="57e09-187">Before configuring the producer that communicates with the destination cluster, you must find the broker hosts for the **destination** cluster.</span></span> <span data-ttu-id="57e09-188">Use the following commands to retrieve this information:</span><span class="sxs-lookup"><span data-stu-id="57e09-188">Use the following commands to retrieve this information:</span></span>
   
    ```bash
    sudo apt -y install jq
    DEST_BROKERHOSTS=`sudo bash -c 'ls /var/lib/ambari-agent/data/command-[0-9]*.json' | tail -n 1 | xargs sudo cat | jq -r '["\(.clusterHostInfo.kafka_broker_hosts[]):9092"] | join(",")'`
    echo $DEST_BROKERHOSTS
    ```
   
    <span data-ttu-id="57e09-189">These commands return information similar to the following:</span><span class="sxs-lookup"><span data-stu-id="57e09-189">These commands return information similar to the following:</span></span>
   
        wn0-dest.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn1-dest.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092

4. <span data-ttu-id="57e09-190">Use the following to create a `producer.properties` file that describes how to communicate with the **destination** cluster:</span><span class="sxs-lookup"><span data-stu-id="57e09-190">Use the following to create a `producer.properties` file that describes how to communicate with the **destination** cluster:</span></span>

    ```bash
    nano producer.properties
    ```

    <span data-ttu-id="57e09-191">Use the following text as the contents of the `producer.properties` file:</span><span class="sxs-lookup"><span data-stu-id="57e09-191">Use the following text as the contents of the `producer.properties` file:</span></span>
   
        bootstrap.servers=DEST_BROKERS
        compression.type=none
   
    <span data-ttu-id="57e09-192">Replace **DEST_BROKERS** with the broker information from the previous step.</span><span class="sxs-lookup"><span data-stu-id="57e09-192">Replace **DEST_BROKERS** with the broker information from the previous step.</span></span> 
   
    <span data-ttu-id="57e09-193">For more information producer configuration, see [Producer Configs](https://kafka.apache.org/documentation#producerconfigs) at kafka.apache.org.</span><span class="sxs-lookup"><span data-stu-id="57e09-193">For more information producer configuration, see [Producer Configs](https://kafka.apache.org/documentation#producerconfigs) at kafka.apache.org.</span></span>

## <a name="start-mirrormaker"></a><span data-ttu-id="57e09-194">Start MirrorMaker</span><span class="sxs-lookup"><span data-stu-id="57e09-194">Start MirrorMaker</span></span>

1. <span data-ttu-id="57e09-195">From the SSH connection to the **destination** cluster, use the following command to start the MirrorMaker process:</span><span class="sxs-lookup"><span data-stu-id="57e09-195">From the SSH connection to the **destination** cluster, use the following command to start the MirrorMaker process:</span></span>
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-run-class.sh kafka.tools.MirrorMaker --consumer.config consumer.properties --producer.config producer.properties --whitelist testtopic --num.streams 4
    ```
   
    <span data-ttu-id="57e09-196">The parameters used in this example are:</span><span class="sxs-lookup"><span data-stu-id="57e09-196">The parameters used in this example are:</span></span>
   
    * <span data-ttu-id="57e09-197">**--consumer.config**: Specifies the file that contains consumer properties.</span><span class="sxs-lookup"><span data-stu-id="57e09-197">**--consumer.config**: Specifies the file that contains consumer properties.</span></span> <span data-ttu-id="57e09-198">These properties are used to create a consumer that reads from the *source* Kafka cluster.</span><span class="sxs-lookup"><span data-stu-id="57e09-198">These properties are used to create a consumer that reads from the *source* Kafka cluster.</span></span>

    * <span data-ttu-id="57e09-199">**--producer.config**: Specifies the file that contains producer properties.</span><span class="sxs-lookup"><span data-stu-id="57e09-199">**--producer.config**: Specifies the file that contains producer properties.</span></span> <span data-ttu-id="57e09-200">These properties are used to create a producer that writes to the *destination* Kafka cluster.</span><span class="sxs-lookup"><span data-stu-id="57e09-200">These properties are used to create a producer that writes to the *destination* Kafka cluster.</span></span>

    * <span data-ttu-id="57e09-201">**--whitelist**: A list of topics that MirrorMaker replicates from the source cluster to the destination.</span><span class="sxs-lookup"><span data-stu-id="57e09-201">**--whitelist**: A list of topics that MirrorMaker replicates from the source cluster to the destination.</span></span>
    
    * <span data-ttu-id="57e09-202">**--num.streams**: The number of consumer threads to create.</span><span class="sxs-lookup"><span data-stu-id="57e09-202">**--num.streams**: The number of consumer threads to create.</span></span>
     
    <span data-ttu-id="57e09-203">On startup, MirrorMaker returns information similar to the following text:</span><span class="sxs-lookup"><span data-stu-id="57e09-203">On startup, MirrorMaker returns information similar to the following text:</span></span>
        
    ```
    {metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-3, security.protocol=PLAINTEXT}{metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-0, security.protocol=PLAINTEXT}
    metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-kafka.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-2, security.protocol=PLAINTEXT}
    metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-1, security.protocol=PLAINTEXT}
    ```

2. <span data-ttu-id="57e09-204">From the SSH connection to the **source** cluster, use the following command to start a producer and send messages to the topic:</span><span class="sxs-lookup"><span data-stu-id="57e09-204">From the SSH connection to the **source** cluster, use the following command to start a producer and send messages to the topic:</span></span>
    
    ```bash
    sudo apt -y install jq
    SOURCE_BROKERHOSTS=`sudo bash -c 'ls /var/lib/ambari-agent/data/command-[0-9]*.json' | tail -n 1 | xargs sudo cat | jq -r '["\(.clusterHostInfo.kafka_broker_hosts[]):9092"] | join(",")'`
    /usr/hdp/current/kafka-broker/bin/kafka-console-producer.sh --broker-list $SOURCE_BROKERHOSTS --topic testtopic
    ```

 <span data-ttu-id="57e09-205">When you arrive at a blank line with a cursor, type in a few text messages.</span><span class="sxs-lookup"><span data-stu-id="57e09-205">When you arrive at a blank line with a cursor, type in a few text messages.</span></span> <span data-ttu-id="57e09-206">These are sent to the topic on the **source** cluster.</span><span class="sxs-lookup"><span data-stu-id="57e09-206">These are sent to the topic on the **source** cluster.</span></span> <span data-ttu-id="57e09-207">When done, use **Ctrl + C** to end the producer process.</span><span class="sxs-lookup"><span data-stu-id="57e09-207">When done, use **Ctrl + C** to end the producer process.</span></span>

3. <span data-ttu-id="57e09-208">From the SSH connection to the **destination** cluster, use **Ctrl + C** to end the MirrorMaker process.</span><span class="sxs-lookup"><span data-stu-id="57e09-208">From the SSH connection to the **destination** cluster, use **Ctrl + C** to end the MirrorMaker process.</span></span> <span data-ttu-id="57e09-209">Then use the following commands to verify that the `testtopic` topic was created, and that data in the topic was replicated to this mirror:</span><span class="sxs-lookup"><span data-stu-id="57e09-209">Then use the following commands to verify that the `testtopic` topic was created, and that data in the topic was replicated to this mirror:</span></span>
    
    ```bash
    DEST_ZKHOSTS=`grep -R zk /etc/hadoop/conf/yarn-site.xml | grep 2181 | grep -oPm1 "(?<=<value>)[^<]+"`
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $DEST_ZKHOSTS
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --zookeeper $DEST_ZKHOSTS --topic testtopic --from-beginning
    ```
    
  <span data-ttu-id="57e09-210">The list of topics now includes `testtopic`, which is created when MirrorMaster mirrors the topic from the source cluster to the destination.</span><span class="sxs-lookup"><span data-stu-id="57e09-210">The list of topics now includes `testtopic`, which is created when MirrorMaster mirrors the topic from the source cluster to the destination.</span></span> <span data-ttu-id="57e09-211">The messages retrieved from the topic are the same as entered on the source cluster.</span><span class="sxs-lookup"><span data-stu-id="57e09-211">The messages retrieved from the topic are the same as entered on the source cluster.</span></span>

## <a name="delete-the-cluster"></a><span data-ttu-id="57e09-212">Delete the cluster</span><span class="sxs-lookup"><span data-stu-id="57e09-212">Delete the cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="57e09-213">Since the steps in this document create both clusters in the same Azure resource group, you can delete the resource group in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="57e09-213">Since the steps in this document create both clusters in the same Azure resource group, you can delete the resource group in the Azure portal.</span></span> <span data-ttu-id="57e09-214">Deleting the resource group removes all resources created by following this document, the Azure Virtual Network, and storage account used by the clusters.</span><span class="sxs-lookup"><span data-stu-id="57e09-214">Deleting the resource group removes all resources created by following this document, the Azure Virtual Network, and storage account used by the clusters.</span></span>

## <a name="next-steps"></a><span data-ttu-id="57e09-215">Next Steps</span><span class="sxs-lookup"><span data-stu-id="57e09-215">Next Steps</span></span>

<span data-ttu-id="57e09-216">In this document, you learned how to use MirrorMaker to create a replica of a Kafka cluster.</span><span class="sxs-lookup"><span data-stu-id="57e09-216">In this document, you learned how to use MirrorMaker to create a replica of a Kafka cluster.</span></span> <span data-ttu-id="57e09-217">Use the following links to discover other ways to work with Kafka:</span><span class="sxs-lookup"><span data-stu-id="57e09-217">Use the following links to discover other ways to work with Kafka:</span></span>

* <span data-ttu-id="57e09-218">[Apache Kafka MirrorMaker documentation](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=27846330) at cwiki.apache.org.</span><span class="sxs-lookup"><span data-stu-id="57e09-218">[Apache Kafka MirrorMaker documentation](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=27846330) at cwiki.apache.org.</span></span>
* [<span data-ttu-id="57e09-219">Get started with Apache Kafka on HDInsight</span><span class="sxs-lookup"><span data-stu-id="57e09-219">Get started with Apache Kafka on HDInsight</span></span>](hdinsight-apache-kafka-get-started.md)
* [<span data-ttu-id="57e09-220">Use Apache Spark with Kafka on HDInsight</span><span class="sxs-lookup"><span data-stu-id="57e09-220">Use Apache Spark with Kafka on HDInsight</span></span>](hdinsight-apache-spark-with-kafka.md)
* [<span data-ttu-id="57e09-221">Use Apache Storm with Kafka on HDInsight</span><span class="sxs-lookup"><span data-stu-id="57e09-221">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)
* [<span data-ttu-id="57e09-222">Connect to Kafka through an Azure Virtual Network</span><span class="sxs-lookup"><span data-stu-id="57e09-222">Connect to Kafka through an Azure Virtual Network</span></span>](hdinsight-apache-kafka-connect-vpn-gateway.md)





