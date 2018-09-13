---
title: Use Apache Kafka with Storm on HDInsight | Microsoft Docs
description: Apache Kafka is installed with Apache Storm on HDInsight. Learn how to write to Kafka, and then read from it, using the KafkaBolt and KafkaSpout components provided with Storm. Also learn how to use the Flux framework to define and submit Storm topologies.
services: hdinsight
documentationcenter: ''
author: Blackmist
manager: paulettm
editor: cgronlun
ms.assetid: e4941329-1580-4cd8-b82e-a2258802c1a7
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/20/2017
ms.author: larryfr
ms.openlocfilehash: 73f989c2d9d34767710a0eb41cfe344cfcea5b1e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564730"
---
# <a name="use-apache-kafka-preview-with-storm-on-hdinsight"></a><span data-ttu-id="fd0dc-105">Use Apache Kafka (preview) with Storm on HDInsight</span><span class="sxs-lookup"><span data-stu-id="fd0dc-105">Use Apache Kafka (preview) with Storm on HDInsight</span></span>

<span data-ttu-id="fd0dc-106">Apache Kafka is a publish-subscribe messaging solution that is available with HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-106">Apache Kafka is a publish-subscribe messaging solution that is available with HDInsight.</span></span> <span data-ttu-id="fd0dc-107">Apache Storm is a distributed system that can be used to analyze data in real-time.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-107">Apache Storm is a distributed system that can be used to analyze data in real-time.</span></span> <span data-ttu-id="fd0dc-108">This document demonstrates how you can use Storm on HDInsight to read and process data from Kafka on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-108">This document demonstrates how you can use Storm on HDInsight to read and process data from Kafka on HDInsight.</span></span> <span data-ttu-id="fd0dc-109">The example in this document uses a Java-based Storm topology that relies on the Kafka spout and bolt components available with Apache Storm.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-109">The example in this document uses a Java-based Storm topology that relies on the Kafka spout and bolt components available with Apache Storm.</span></span>

> [!NOTE]
> <span data-ttu-id="fd0dc-110">The steps in this document create an Azure resource group that contains both a Storm on HDInsight and a Kafka on HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-110">The steps in this document create an Azure resource group that contains both a Storm on HDInsight and a Kafka on HDInsight cluster.</span></span> <span data-ttu-id="fd0dc-111">These clusters are both located within an Azure Virtual Network, which allows the Storm cluster to directly communicate with the Kafka cluster.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-111">These clusters are both located within an Azure Virtual Network, which allows the Storm cluster to directly communicate with the Kafka cluster.</span></span>
> 
> <span data-ttu-id="fd0dc-112">When you are done with the steps in this document, remember to delete the clusters to avoid excess charges.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-112">When you are done with the steps in this document, remember to delete the clusters to avoid excess charges.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fd0dc-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="fd0dc-113">Prerequisites</span></span>

* <span data-ttu-id="fd0dc-114">[Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 1.8 or higher.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-114">[Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 1.8 or higher.</span></span> <span data-ttu-id="fd0dc-115">Or an equivalent such as [OpenJDK](http://openjdk.java.net/).</span><span class="sxs-lookup"><span data-stu-id="fd0dc-115">Or an equivalent such as [OpenJDK](http://openjdk.java.net/).</span></span>
  
    > [!NOTE]
    > <span data-ttu-id="fd0dc-116">The steps in this document use an HDInsight 3.5 cluster, which uses Java 8.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-116">The steps in this document use an HDInsight 3.5 cluster, which uses Java 8.</span></span>

* <span data-ttu-id="fd0dc-117">[Maven 3.x](http://maven.apache.org/) - A build management package for Java applications.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-117">[Maven 3.x](http://maven.apache.org/) - A build management package for Java applications.</span></span>

* <span data-ttu-id="fd0dc-118">A text editor or Java IDE</span><span class="sxs-lookup"><span data-stu-id="fd0dc-118">A text editor or Java IDE</span></span>

* <span data-ttu-id="fd0dc-119">An SSH client (you need the `ssh` and `scp` commands) - For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="fd0dc-119">An SSH client (you need the `ssh` and `scp` commands) - For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <a name="create-the-clusters"></a><span data-ttu-id="fd0dc-120">Create the clusters</span><span class="sxs-lookup"><span data-stu-id="fd0dc-120">Create the clusters</span></span>

<span data-ttu-id="fd0dc-121">Apache Kafka on HDInsight does not provide access to the Kafka brokers over the public internet.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-121">Apache Kafka on HDInsight does not provide access to the Kafka brokers over the public internet.</span></span> <span data-ttu-id="fd0dc-122">Anything that talks to Kafka must be in the same Azure virtual network as the nodes in the Kafka cluster.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-122">Anything that talks to Kafka must be in the same Azure virtual network as the nodes in the Kafka cluster.</span></span> <span data-ttu-id="fd0dc-123">For this example, both the Kafka and Storm clusters are located in an Azure virtual network.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-123">For this example, both the Kafka and Storm clusters are located in an Azure virtual network.</span></span> <span data-ttu-id="fd0dc-124">The following diagram shows how communication flows between the clusters:</span><span class="sxs-lookup"><span data-stu-id="fd0dc-124">The following diagram shows how communication flows between the clusters:</span></span>

![Diagram of Storm and Kafka clusters in an Azure virtual network](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-storm-with-kafka/storm-kafka-vnet.png)

> [!NOTE]
> <span data-ttu-id="fd0dc-126">Though Kafka itself is limited to communication within the virtual network, other services on the cluster such as SSH and Ambari can be accessed over the internet.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-126">Though Kafka itself is limited to communication within the virtual network, other services on the cluster such as SSH and Ambari can be accessed over the internet.</span></span> <span data-ttu-id="fd0dc-127">For more information on the public ports available with HDInsight, see [Ports and URIs used by HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span><span class="sxs-lookup"><span data-stu-id="fd0dc-127">For more information on the public ports available with HDInsight, see [Ports and URIs used by HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span></span>


<span data-ttu-id="fd0dc-128">While you can create an Azure virtual network, Kafka, and Storm clusters manually, it's easier to use an Azure Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-128">While you can create an Azure virtual network, Kafka, and Storm clusters manually, it's easier to use an Azure Resource Manager template.</span></span> <span data-ttu-id="fd0dc-129">Use the following steps to deploy an Azure virtual network, Kafka, and Storm clusters to your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-129">Use the following steps to deploy an Azure virtual network, Kafka, and Storm clusters to your Azure subscription.</span></span>

1. <span data-ttu-id="fd0dc-130">Use the following button to sign in to Azure and open the template in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-130">Use the following button to sign in to Azure and open the template in the Azure portal.</span></span>
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-storm-cluster-in-vnet.json" target="_blank"><img src="https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-storm-with-kafka/deploy-to-azure.png" alt="Deploy to Azure"></a>
   
    <span data-ttu-id="fd0dc-131">The Azure Resource Manager template is located at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-storm-cluster-in-vnet.json**.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-131">The Azure Resource Manager template is located at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-storm-cluster-in-vnet.json**.</span></span>

2. <span data-ttu-id="fd0dc-132">Use the following guidance to populate the entries on the **Custom deployment** blade:</span><span class="sxs-lookup"><span data-stu-id="fd0dc-132">Use the following guidance to populate the entries on the **Custom deployment** blade:</span></span>
   
    ![HDInsight custom deployment](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-storm-with-kafka/parameters.png)

    * <span data-ttu-id="fd0dc-134">**Resource group**: Create a group or select an existing one.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-134">**Resource group**: Create a group or select an existing one.</span></span> <span data-ttu-id="fd0dc-135">This group contains the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-135">This group contains the HDInsight cluster.</span></span>
   
    * <span data-ttu-id="fd0dc-136">**Location**: Select a location geographically close to you.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-136">**Location**: Select a location geographically close to you.</span></span> <span data-ttu-id="fd0dc-137">This location must match the location in the __SETTINGS__ section.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-137">This location must match the location in the __SETTINGS__ section.</span></span>

    * <span data-ttu-id="fd0dc-138">**Base Cluster Name**: This value is used as the base name for the Storm and Kafka clusters.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-138">**Base Cluster Name**: This value is used as the base name for the Storm and Kafka clusters.</span></span> <span data-ttu-id="fd0dc-139">For example, entering **hdi** creates a Storm cluster named **storm-hdi** and a Kafka cluster named **kafka-hdi**.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-139">For example, entering **hdi** creates a Storm cluster named **storm-hdi** and a Kafka cluster named **kafka-hdi**.</span></span>
   
    * <span data-ttu-id="fd0dc-140">**Cluster Login User Name**: The admin user name for the Storm and Kafka clusters.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-140">**Cluster Login User Name**: The admin user name for the Storm and Kafka clusters.</span></span>
   
    * <span data-ttu-id="fd0dc-141">**Cluster Login Password**: The admin user password for the Storm and Kafka clusters.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-141">**Cluster Login Password**: The admin user password for the Storm and Kafka clusters.</span></span>
    
    * <span data-ttu-id="fd0dc-142">**SSH User Name**: The SSH user to create for the Storm and Kafka clusters.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-142">**SSH User Name**: The SSH user to create for the Storm and Kafka clusters.</span></span>
    
    * <span data-ttu-id="fd0dc-143">**SSH Password**: The password for the SSH user for the Storm and Kafka clusters.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-143">**SSH Password**: The password for the SSH user for the Storm and Kafka clusters.</span></span>
    
    * <span data-ttu-id="fd0dc-144">**Location**: The region that the clusters are created in.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-144">**Location**: The region that the clusters are created in.</span></span>

3. <span data-ttu-id="fd0dc-145">Read the **Terms and Conditions**, and then select **I agree to the terms and conditions stated above**.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-145">Read the **Terms and Conditions**, and then select **I agree to the terms and conditions stated above**.</span></span>

4. <span data-ttu-id="fd0dc-146">Finally, check **Pin to dashboard** and then select **Purchase**.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-146">Finally, check **Pin to dashboard** and then select **Purchase**.</span></span> <span data-ttu-id="fd0dc-147">It takes about 20 minutes to create the clusters.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-147">It takes about 20 minutes to create the clusters.</span></span>

<span data-ttu-id="fd0dc-148">Once the resources have been created, you are redirected to a blade for the resource group that contains the clusters and web dashboard.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-148">Once the resources have been created, you are redirected to a blade for the resource group that contains the clusters and web dashboard.</span></span>

![Resource group blade for the vnet and clusters](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-storm-with-kafka/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="fd0dc-150">Notice that the names of the HDInsight clusters are **storm-BASENAME** and **kafka-BASENAME**, where BASENAME is the name you provided to the template.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-150">Notice that the names of the HDInsight clusters are **storm-BASENAME** and **kafka-BASENAME**, where BASENAME is the name you provided to the template.</span></span> <span data-ttu-id="fd0dc-151">You use these names in later steps when connecting to the clusters.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-151">You use these names in later steps when connecting to the clusters.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="fd0dc-152">Get the code</span><span class="sxs-lookup"><span data-stu-id="fd0dc-152">Get the code</span></span>

<span data-ttu-id="fd0dc-153">The code for the example described in this document is available at [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka).</span><span class="sxs-lookup"><span data-stu-id="fd0dc-153">The code for the example described in this document is available at [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka).</span></span>

## <a name="understanding-the-code"></a><span data-ttu-id="fd0dc-154">Understanding the code</span><span class="sxs-lookup"><span data-stu-id="fd0dc-154">Understanding the code</span></span>

<span data-ttu-id="fd0dc-155">This project contains two topologies:</span><span class="sxs-lookup"><span data-stu-id="fd0dc-155">This project contains two topologies:</span></span>

* <span data-ttu-id="fd0dc-156">**KafkaWriter**: Defined by the **writer.yaml** file, this topology writes random sentences to Kafka using the KafkaBolt provided with Apache Storm.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-156">**KafkaWriter**: Defined by the **writer.yaml** file, this topology writes random sentences to Kafka using the KafkaBolt provided with Apache Storm.</span></span>
  
    <span data-ttu-id="fd0dc-157">This topology uses a custom **SentenceSpout** component to generate random sentences.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-157">This topology uses a custom **SentenceSpout** component to generate random sentences.</span></span>

* <span data-ttu-id="fd0dc-158">**KafkaReader**: Defined by the **reader.yaml** file, this topology reads data from Kafka using the KafkaSpout provided with Apache Storm, then logs the data to stdout.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-158">**KafkaReader**: Defined by the **reader.yaml** file, this topology reads data from Kafka using the KafkaSpout provided with Apache Storm, then logs the data to stdout.</span></span>
  
    <span data-ttu-id="fd0dc-159">This topology uses a custom **PrinterBolt** component to log data read from Kafka.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-159">This topology uses a custom **PrinterBolt** component to log data read from Kafka.</span></span>

### <a name="flux"></a><span data-ttu-id="fd0dc-160">Flux</span><span class="sxs-lookup"><span data-stu-id="fd0dc-160">Flux</span></span>

<span data-ttu-id="fd0dc-161">The topologies are defined using [Flux](https://storm.apache.org/releases/1.0.1/flux.html).</span><span class="sxs-lookup"><span data-stu-id="fd0dc-161">The topologies are defined using [Flux](https://storm.apache.org/releases/1.0.1/flux.html).</span></span> <span data-ttu-id="fd0dc-162">Flux was introduced in Storm 0.10.x and allows you to separate the topology configuration from the code.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-162">Flux was introduced in Storm 0.10.x and allows you to separate the topology configuration from the code.</span></span> <span data-ttu-id="fd0dc-163">For Topologies that use the Flux framework, the topology is defined in a YAML file.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-163">For Topologies that use the Flux framework, the topology is defined in a YAML file.</span></span> <span data-ttu-id="fd0dc-164">The YAML file can be included as part of the topology, or can be specified when you submit the topology to the Storm server.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-164">The YAML file can be included as part of the topology, or can be specified when you submit the topology to the Storm server.</span></span> <span data-ttu-id="fd0dc-165">Flux also supports variable substitution at run-time, which is used in this example.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-165">Flux also supports variable substitution at run-time, which is used in this example.</span></span>

<span data-ttu-id="fd0dc-166">Both topologies expect the following environment variables:</span><span class="sxs-lookup"><span data-stu-id="fd0dc-166">Both topologies expect the following environment variables:</span></span>

* <span data-ttu-id="fd0dc-167">**KAFKATOPIC**: The name of the Kafka topic that the topologies read/write to.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-167">**KAFKATOPIC**: The name of the Kafka topic that the topologies read/write to.</span></span>

* <span data-ttu-id="fd0dc-168">**KAFKABROKERS**: The hosts that the Kafka brokers run on.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-168">**KAFKABROKERS**: The hosts that the Kafka brokers run on.</span></span> <span data-ttu-id="fd0dc-169">The broker information is used by the KafkaBolt when writing to Kafka.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-169">The broker information is used by the KafkaBolt when writing to Kafka.</span></span>

* <span data-ttu-id="fd0dc-170">**KAFKAZKHOSTS**: The hosts that Zookeeper runs on.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-170">**KAFKAZKHOSTS**: The hosts that Zookeeper runs on.</span></span>

<span data-ttu-id="fd0dc-171">The steps in this document demonstrate how to set these environment variables.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-171">The steps in this document demonstrate how to set these environment variables.</span></span>

## <a name="create-a-kafka-topic"></a><span data-ttu-id="fd0dc-172">Create a Kafka topic</span><span class="sxs-lookup"><span data-stu-id="fd0dc-172">Create a Kafka topic</span></span>

1. <span data-ttu-id="fd0dc-173">Connect to the Kafka cluster using SSH.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-173">Connect to the Kafka cluster using SSH.</span></span> <span data-ttu-id="fd0dc-174">Replace `USERNAME` with the SSH user name used when creating the cluster.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-174">Replace `USERNAME` with the SSH user name used when creating the cluster.</span></span> <span data-ttu-id="fd0dc-175">Replace `BASENAME` with the base name used when creating the cluster.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-175">Replace `BASENAME` with the base name used when creating the cluster.</span></span>
   
        ssh USERNAME@kafka-BASENAME-ssh.azurehdinsight.net
   
    <span data-ttu-id="fd0dc-176">When prompted, enter the password you used when creating the clusters.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-176">When prompted, enter the password you used when creating the clusters.</span></span>
   
    <span data-ttu-id="fd0dc-177">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="fd0dc-177">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="fd0dc-178">From the SSH connection to the Kafka cluster, use the following commands to set variables for the HTTP login and cluster name.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-178">From the SSH connection to the Kafka cluster, use the following commands to set variables for the HTTP login and cluster name.</span></span> <span data-ttu-id="fd0dc-179">These values are used by other steps in this section.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-179">These values are used by other steps in this section.</span></span>

  ```bash
  ADMIN='admin' #replace with the name of the admin account for the cluster
  PASSWORD='password' #replace with the password for the admin account
  ```

3. <span data-ttu-id="fd0dc-180">Use the following commands to install the `jq` utility, retrieve the cluster name, and set the `KAFKAZKHOSTS` variable:</span><span class="sxs-lookup"><span data-stu-id="fd0dc-180">Use the following commands to install the `jq` utility, retrieve the cluster name, and set the `KAFKAZKHOSTS` variable:</span></span>

  ```bash
  sudo apt -y install jq
  CLUSTERNAME=`curl -u $ADMIN:$PASSWORD -G "http://headnodehost:8080/api/v1/clusters" | jq -r '.items[].Clusters.cluster_name'`
  KAFKAZKHOSTS=`curl -u $ADMIN:$PASSWORD -G "http://headnodehost:8080/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER" | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")'`
  ```

    <span data-ttu-id="fd0dc-181">Use the following command to retrieve the cluster name:</span><span class="sxs-lookup"><span data-stu-id="fd0dc-181">Use the following command to retrieve the cluster name:</span></span>

  ```bash
  echo $CLUSTERNAME
  ```

    <span data-ttu-id="fd0dc-182">The output of this command is similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="fd0dc-182">The output of this command is similar to the following example:</span></span>

  ```bash
  kafka-myhdi
  ```

    <span data-ttu-id="fd0dc-183">Use the following command to verify that `KAFKAZKHOSTS` is set correctly:</span><span class="sxs-lookup"><span data-stu-id="fd0dc-183">Use the following command to verify that `KAFKAZKHOSTS` is set correctly:</span></span>

  ```bash
  echo $KAFKAZKHOSTS
  ```

    <span data-ttu-id="fd0dc-184">The output of this command is similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="fd0dc-184">The output of this command is similar to the following example:</span></span>

  ```bash
  zk0-kafka.eahjefxxp1netdbyklgqj5y1ud.ex.internal.cloudapp.net:2181,zk2-kafka.eahjefxxp1netdbyklgqj5y1ud.ex.internal.cloudapp.net:2181,zk3-kafka.eahjefxxp1netdbyklgqj5y1ud.ex.internal.cloudapp.net:2181
  ```

    <span data-ttu-id="fd0dc-185">Save the Kafka cluster name and the Zookeeper host information, as these values are used when starting the topology on the Storm cluster.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-185">Save the Kafka cluster name and the Zookeeper host information, as these values are used when starting the topology on the Storm cluster.</span></span>

    > [!NOTE]
    > <span data-ttu-id="fd0dc-186">The previous commands use __http://headnodehost:8080/__, which connects to Ambari directly.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-186">The previous commands use __http://headnodehost:8080/__, which connects to Ambari directly.</span></span> <span data-ttu-id="fd0dc-187">If you need to retrieve this information from outside the cluster, over the internet, you must use __https://kafka-BASENAME.azurehdinsight.net/__ instead.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-187">If you need to retrieve this information from outside the cluster, over the internet, you must use __https://kafka-BASENAME.azurehdinsight.net/__ instead.</span></span>

4. <span data-ttu-id="fd0dc-188">Use the following command to create a topic in Kafka:</span><span class="sxs-lookup"><span data-stu-id="fd0dc-188">Use the following command to create a topic in Kafka:</span></span>

  ```bash
  /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 2 --partitions 8 --topic stormtest --zookeeper $KAFKAZKHOSTS
  ```

    <span data-ttu-id="fd0dc-189">This command connects to Zookeeper using the host information stored in `$KAFKAZKHOSTS`, and then creates a Kafka topic named **stormtest**.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-189">This command connects to Zookeeper using the host information stored in `$KAFKAZKHOSTS`, and then creates a Kafka topic named **stormtest**.</span></span> <span data-ttu-id="fd0dc-190">You can verify that the topic was created by using the following command to list topics:</span><span class="sxs-lookup"><span data-stu-id="fd0dc-190">You can verify that the topic was created by using the following command to list topics:</span></span>

  ```bash
  /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $KAFKAZKHOSTS
  ```

    <span data-ttu-id="fd0dc-191">The output of this command lists Kafka topics, which should contain the new **stormtest** topic.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-191">The output of this command lists Kafka topics, which should contain the new **stormtest** topic.</span></span>

<span data-ttu-id="fd0dc-192">Leave the SSH connection to the Kafka cluster active, as you can use it to verify that the Storm topology is writing messages to the topic.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-192">Leave the SSH connection to the Kafka cluster active, as you can use it to verify that the Storm topology is writing messages to the topic.</span></span>

## <a name="download-and-compile-the-project"></a><span data-ttu-id="fd0dc-193">Download and compile the project</span><span class="sxs-lookup"><span data-stu-id="fd0dc-193">Download and compile the project</span></span>

1. <span data-ttu-id="fd0dc-194">On your development environment, download the project from [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka), open a command-line, and change directories to the location that you downloaded the project.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-194">On your development environment, download the project from [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka), open a command-line, and change directories to the location that you downloaded the project.</span></span>

    <span data-ttu-id="fd0dc-195">Take a few moments to look over the code and understand how the project works.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-195">Take a few moments to look over the code and understand how the project works.</span></span>

2. <span data-ttu-id="fd0dc-196">From the **hdinsight-storm-java-kafka** directory, use the following command to compile the project and create a package for deployment:</span><span class="sxs-lookup"><span data-stu-id="fd0dc-196">From the **hdinsight-storm-java-kafka** directory, use the following command to compile the project and create a package for deployment:</span></span>

  ```bash
  mvn clean package
  ```

    <span data-ttu-id="fd0dc-197">The package process creates a file named `KafkaTopology-1.0-SNAPSHOT.jar` in the `target` directory.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-197">The package process creates a file named `KafkaTopology-1.0-SNAPSHOT.jar` in the `target` directory.</span></span>

3. <span data-ttu-id="fd0dc-198">Use the following commands to copy the package to your Storm on HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-198">Use the following commands to copy the package to your Storm on HDInsight cluster.</span></span> <span data-ttu-id="fd0dc-199">Replace **USERNAME** with the SSH user name for the cluster.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-199">Replace **USERNAME** with the SSH user name for the cluster.</span></span> <span data-ttu-id="fd0dc-200">Replace **BASENAME** with the base name you used when creating the cluster.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-200">Replace **BASENAME** with the base name you used when creating the cluster.</span></span>

  ```bash
  scp ./target/KafkaTopology-1.0-SNAPSHOT.jar USERNAME@storm-BASENAME-ssh.azurehdinsight.net:KafkaTopology-1.0-SNAPSHOT.jar
  ```

    <span data-ttu-id="fd0dc-201">When prompted, enter the password you used when creating the clusters.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-201">When prompted, enter the password you used when creating the clusters.</span></span>

4. <span data-ttu-id="fd0dc-202">Use the following command to copy the `set-env-variables.sh` file from the `scripts` directory of the project to the Storm cluster:</span><span class="sxs-lookup"><span data-stu-id="fd0dc-202">Use the following command to copy the `set-env-variables.sh` file from the `scripts` directory of the project to the Storm cluster:</span></span>

  ```bash
  scp ./scripts/set-env-variables.sh USERNAME@storm-BASENAME-ssh.azurehdinsight.net:set-env-variables.sh
  ```

    <span data-ttu-id="fd0dc-203">This script is used to set the environment variables that the Storm topologies use to communicate with the Kafka cluster.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-203">This script is used to set the environment variables that the Storm topologies use to communicate with the Kafka cluster.</span></span>

## <a name="start-the-writer"></a><span data-ttu-id="fd0dc-204">Start the writer</span><span class="sxs-lookup"><span data-stu-id="fd0dc-204">Start the writer</span></span>

1. <span data-ttu-id="fd0dc-205">Use the following to connect to the Storm cluster using SSH.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-205">Use the following to connect to the Storm cluster using SSH.</span></span> <span data-ttu-id="fd0dc-206">Replace **USERNAME** with the SSH user name used when creating the cluster.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-206">Replace **USERNAME** with the SSH user name used when creating the cluster.</span></span> <span data-ttu-id="fd0dc-207">Replace **BASENAME** with the base name used when creating the cluster.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-207">Replace **BASENAME** with the base name used when creating the cluster.</span></span>

  ```bash
  ssh USERNAME@storm-BASENAME-ssh.azurehdinsight.net
  ```

    <span data-ttu-id="fd0dc-208">When prompted, enter the password you used when creating the clusters.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-208">When prompted, enter the password you used when creating the clusters.</span></span>
   
    <span data-ttu-id="fd0dc-209">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="fd0dc-209">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="fd0dc-210">From the SSH connection to the Storm cluster, use the following commands to run the `set-env-variables.sh` script:</span><span class="sxs-lookup"><span data-stu-id="fd0dc-210">From the SSH connection to the Storm cluster, use the following commands to run the `set-env-variables.sh` script:</span></span>

  ```bash
  chmod +x set-env-variables.sh
  . ./set-env-variables.sh KAFKACLUSTERNAME PASSWORD
  ```

    <span data-ttu-id="fd0dc-211">Replace __KAFKACLUSTERNAME__ with the name of the Kafka cluster.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-211">Replace __KAFKACLUSTERNAME__ with the name of the Kafka cluster.</span></span> <span data-ttu-id="fd0dc-212">Replace __PASSWORD__ with the admin login password for the Kafka cluster.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-212">Replace __PASSWORD__ with the admin login password for the Kafka cluster.</span></span>

    <span data-ttu-id="fd0dc-213">The script connects to the Kafka cluster and retrieves a list of the Kafka broker and Zookeeper hosts.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-213">The script connects to the Kafka cluster and retrieves a list of the Kafka broker and Zookeeper hosts.</span></span> <span data-ttu-id="fd0dc-214">The information is then stored in environment variables that are used by the Storm topologies.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-214">The information is then stored in environment variables that are used by the Storm topologies.</span></span>

    <span data-ttu-id="fd0dc-215">The output of the script is similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="fd0dc-215">The output of the script is similar to the following example:</span></span>

        Checking for jq: install ok installed
        Exporting variables:
        $KAFKATOPIC=stormtest
        $KAFKABROKERS=wn0-storm.4rf4ncirvydube02fuj0gpxp4e.ex.internal.cloudapp.net:9092,wn1-storm.4rf4ncirvydube02fuj0gpxp4e.ex.internal.cloudapp.net:9092
        $KAFKAZKHOSTS=zk1-storm.4rf4ncirvydube02fuj0gpxp4e.ex.internal.cloudapp.net:2181,zk3-storm.4rf4ncirvydube02fuj0gpxp4e.ex.internal.cloudapp.net:2181,zk5-storm.4rf4ncirvydube02fuj0gpxp4e.ex.internal.cloudapp.net:2181

3. <span data-ttu-id="fd0dc-216">From the SSH connection to the Storm cluster, use the following command to start the writer topology:</span><span class="sxs-lookup"><span data-stu-id="fd0dc-216">From the SSH connection to the Storm cluster, use the following command to start the writer topology:</span></span>

        storm jar KafkaTopology-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writer.yaml -e

    <span data-ttu-id="fd0dc-217">The parameters used with this command are:</span><span class="sxs-lookup"><span data-stu-id="fd0dc-217">The parameters used with this command are:</span></span>

    * <span data-ttu-id="fd0dc-218">`org.apache.storm.flux.Flux`: Use Flux to configure and run this topology.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-218">`org.apache.storm.flux.Flux`: Use Flux to configure and run this topology.</span></span>

    * <span data-ttu-id="fd0dc-219">`--remote`: Submit the topology to Nimbus.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-219">`--remote`: Submit the topology to Nimbus.</span></span> <span data-ttu-id="fd0dc-220">The topology is distributed across the worker nodes in the cluster.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-220">The topology is distributed across the worker nodes in the cluster.</span></span>

    * <span data-ttu-id="fd0dc-221">`-R /writer.yaml`: Use the `writer.yaml` file to configure the topology.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-221">`-R /writer.yaml`: Use the `writer.yaml` file to configure the topology.</span></span> <span data-ttu-id="fd0dc-222">`-R` indicates that this resource is included in the jar file.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-222">`-R` indicates that this resource is included in the jar file.</span></span> <span data-ttu-id="fd0dc-223">It's in the root of the jar, so `/writer.yaml` is the path to it.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-223">It's in the root of the jar, so `/writer.yaml` is the path to it.</span></span>

    * <span data-ttu-id="fd0dc-224">`-e`: Use environment variable substitution.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-224">`-e`: Use environment variable substitution.</span></span> <span data-ttu-id="fd0dc-225">Flux picks up the $KAFKABROKERS and $KAFKATOPIC values you set previously, and uses them in the reader.yaml file in place of the `${ENV-KAFKABROKER}` and `${ENV-KAFKATOPIC}` entries.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-225">Flux picks up the $KAFKABROKERS and $KAFKATOPIC values you set previously, and uses them in the reader.yaml file in place of the `${ENV-KAFKABROKER}` and `${ENV-KAFKATOPIC}` entries.</span></span>

5. <span data-ttu-id="fd0dc-226">Once the topology has started, switch to the SSH connection to the Kafka cluster and use the following command to view messages written to the **stormtest** topic:</span><span class="sxs-lookup"><span data-stu-id="fd0dc-226">Once the topology has started, switch to the SSH connection to the Kafka cluster and use the following command to view messages written to the **stormtest** topic:</span></span>

  ```bash
  /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --zookeeper $KAFKAZKHOSTS --from-beginning --topic stormtest
  ```

    <span data-ttu-id="fd0dc-227">This command uses a script shipped with Kafka to monitor the topic.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-227">This command uses a script shipped with Kafka to monitor the topic.</span></span> <span data-ttu-id="fd0dc-228">After a moment, it should start returning random sentences that have been written to the topic.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-228">After a moment, it should start returning random sentences that have been written to the topic.</span></span> <span data-ttu-id="fd0dc-229">The output is similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="fd0dc-229">The output is similar to the following example:</span></span>

        i am at two with nature             
        an apple a day keeps the doctor away
        snow white and the seven dwarfs     
        the cow jumped over the moon        
        an apple a day keeps the doctor away
        an apple a day keeps the doctor away
        the cow jumped over the moon        
        an apple a day keeps the doctor away
        an apple a day keeps the doctor away
        four score and seven years ago      
        snow white and the seven dwarfs     
        snow white and the seven dwarfs     
        i am at two with nature             
        an apple a day keeps the doctor away

    <span data-ttu-id="fd0dc-230">Use Ctrl+c to stop the script.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-230">Use Ctrl+c to stop the script.</span></span>

## <a name="start-the-reader"></a><span data-ttu-id="fd0dc-231">Start the reader</span><span class="sxs-lookup"><span data-stu-id="fd0dc-231">Start the reader</span></span>

1. <span data-ttu-id="fd0dc-232">From the SSH session to the Storm cluster, use the following command to start the reader topology:</span><span class="sxs-lookup"><span data-stu-id="fd0dc-232">From the SSH session to the Storm cluster, use the following command to start the reader topology:</span></span>

  ```bash
  storm jar KafkaTopology-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /reader.yaml -e
  ```

2. <span data-ttu-id="fd0dc-233">Once the topology starts, open the Storm UI.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-233">Once the topology starts, open the Storm UI.</span></span> <span data-ttu-id="fd0dc-234">This web UI is located at https://storm-BASENAME.azurehdinsight.net/stormui.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-234">This web UI is located at https://storm-BASENAME.azurehdinsight.net/stormui.</span></span> <span data-ttu-id="fd0dc-235">Replace __BASENAME__ with the base name used when the cluster was created.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-235">Replace __BASENAME__ with the base name used when the cluster was created.</span></span> 

    <span data-ttu-id="fd0dc-236">When prompted, use the admin login name (default, `admin`) and password used when the cluster was created.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-236">When prompted, use the admin login name (default, `admin`) and password used when the cluster was created.</span></span> <span data-ttu-id="fd0dc-237">You will see a web page similar to the following image:</span><span class="sxs-lookup"><span data-stu-id="fd0dc-237">You will see a web page similar to the following image:</span></span>

    ![Storm UI](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-storm-with-kafka/stormui.png)

3. <span data-ttu-id="fd0dc-239">From the Storm UI, select the __kafka-reader__ link in the __Topology Summary__ section to display information about the __kafka-reader__ topology.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-239">From the Storm UI, select the __kafka-reader__ link in the __Topology Summary__ section to display information about the __kafka-reader__ topology.</span></span>

    ![Topology summary section of the Storm web UI](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-storm-with-kafka/topology-summary.png)

4. <span data-ttu-id="fd0dc-241">Select the __logger-bolt__ link in the __Bolts (All time)__ section to display information about the instances of the logger-bolt component.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-241">Select the __logger-bolt__ link in the __Bolts (All time)__ section to display information about the instances of the logger-bolt component.</span></span>

    ![Logger-bolt link in the bolts section](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-storm-with-kafka/bolts.png)

5. <span data-ttu-id="fd0dc-243">In the __Executors__ section, select a link in the __Port__ column to display logging information about this instance of the component.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-243">In the __Executors__ section, select a link in the __Port__ column to display logging information about this instance of the component.</span></span>

    ![Executors link](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-storm-with-kafka/executors.png)

    <span data-ttu-id="fd0dc-245">The log contains a log of the data read from the Kafka topic.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-245">The log contains a log of the data read from the Kafka topic.</span></span> <span data-ttu-id="fd0dc-246">The information in the log is similar to the following text:</span><span class="sxs-lookup"><span data-stu-id="fd0dc-246">The information in the log is similar to the following text:</span></span>

        2016-11-04 17:47:14.907 c.m.e.LoggerBolt [INFO] Received data: four score and seven years ago
        2016-11-04 17:47:14.907 STDIO [INFO] the cow jumped over the moon
        2016-11-04 17:47:14.908 c.m.e.LoggerBolt [INFO] Received data: the cow jumped over the moon
        2016-11-04 17:47:14.911 STDIO [INFO] snow white and the seven dwarfs
        2016-11-04 17:47:14.911 c.m.e.LoggerBolt [INFO] Received data: snow white and the seven dwarfs
        2016-11-04 17:47:14.932 STDIO [INFO] snow white and the seven dwarfs
        2016-11-04 17:47:14.932 c.m.e.LoggerBolt [INFO] Received data: snow white and the seven dwarfs
        2016-11-04 17:47:14.969 STDIO [INFO] an apple a day keeps the doctor away
        2016-11-04 17:47:14.970 c.m.e.LoggerBolt [INFO] Received data: an apple a day keeps the doctor away

## <a name="stop-the-topologies"></a><span data-ttu-id="fd0dc-247">Stop the topologies</span><span class="sxs-lookup"><span data-stu-id="fd0dc-247">Stop the topologies</span></span>

<span data-ttu-id="fd0dc-248">From an SSH session to the Storm cluster, use the following commands to stop the Storm topologies:</span><span class="sxs-lookup"><span data-stu-id="fd0dc-248">From an SSH session to the Storm cluster, use the following commands to stop the Storm topologies:</span></span>

  ```bash
  storm kill kafka-writer
  storm kill kafka-reader
  ```

## <a name="delete-the-cluster"></a><span data-ttu-id="fd0dc-249">Delete the cluster</span><span class="sxs-lookup"><span data-stu-id="fd0dc-249">Delete the cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="fd0dc-250">Since the steps in this document create both clusters in the same Azure resource group, you can delete the resource group in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-250">Since the steps in this document create both clusters in the same Azure resource group, you can delete the resource group in the Azure portal.</span></span> <span data-ttu-id="fd0dc-251">This removes all resources created by following this document, the Azure Virtual Network, and storage account used by the clusters.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-251">This removes all resources created by following this document, the Azure Virtual Network, and storage account used by the clusters.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fd0dc-252">Next steps</span><span class="sxs-lookup"><span data-stu-id="fd0dc-252">Next steps</span></span>

<span data-ttu-id="fd0dc-253">For more example topologies that can be used with Storm on HDInsight, see [Example Storm topologies and components](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="fd0dc-253">For more example topologies that can be used with Storm on HDInsight, see [Example Storm topologies and components](hdinsight-storm-example-topology.md).</span></span>

<span data-ttu-id="fd0dc-254">For information on deploying and monitoring topologies on Linux-based HDInsight, see [Deploy and manage Apache Storm topologies on Linux-based HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md)</span><span class="sxs-lookup"><span data-stu-id="fd0dc-254">For information on deploying and monitoring topologies on Linux-based HDInsight, see [Deploy and manage Apache Storm topologies on Linux-based HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md)</span></span>









