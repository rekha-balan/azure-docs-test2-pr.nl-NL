---
title: Get started with Apache Kafka on HDInsight | Microsoft Docs
description: Learn the basics of creating and working with Kafka on HDInsight.
services: hdinsight
documentationcenter: ''
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 43585abf-bec1-4322-adde-6db21de98d7f
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: ''
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 02/14/2017
ms.author: larryfr
ms.openlocfilehash: 7c05538840b19d7776fb2dfbaf1123d71eec3c9b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540714"
---
# <a name="get-started-with-apache-kafka-preview-on-hdinsight"></a><span data-ttu-id="f9fca-103">Get started with Apache Kafka (preview) on HDInsight</span><span class="sxs-lookup"><span data-stu-id="f9fca-103">Get started with Apache Kafka (preview) on HDInsight</span></span>

<span data-ttu-id="f9fca-104">[Apache Kafka](https://kafka.apache.org) is an open-source distributed streaming platform that is available with HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f9fca-104">[Apache Kafka](https://kafka.apache.org) is an open-source distributed streaming platform that is available with HDInsight.</span></span> <span data-ttu-id="f9fca-105">It is often used as a message broker, as it provides functionality similar to a publish-subscribe message queue.</span><span class="sxs-lookup"><span data-stu-id="f9fca-105">It is often used as a message broker, as it provides functionality similar to a publish-subscribe message queue.</span></span> <span data-ttu-id="f9fca-106">In this document, you learn how to create a Kafka on HDInsight cluster and then send and receive data from a Java application.</span><span class="sxs-lookup"><span data-stu-id="f9fca-106">In this document, you learn how to create a Kafka on HDInsight cluster and then send and receive data from a Java application.</span></span>

> [!NOTE]
> <span data-ttu-id="f9fca-107">There are currently two versions of Kafka available with HDInsight; 0.9.0 (HDInsight 3.4) and 0.10.0 (HDInsight 3.5).</span><span class="sxs-lookup"><span data-stu-id="f9fca-107">There are currently two versions of Kafka available with HDInsight; 0.9.0 (HDInsight 3.4) and 0.10.0 (HDInsight 3.5).</span></span> <span data-ttu-id="f9fca-108">The steps in this document assume that you are using Kafka on HDInsight 3.5.</span><span class="sxs-lookup"><span data-stu-id="f9fca-108">The steps in this document assume that you are using Kafka on HDInsight 3.5.</span></span>

## <a name="prerequisite"></a><span data-ttu-id="f9fca-109">Prerequisite</span><span class="sxs-lookup"><span data-stu-id="f9fca-109">Prerequisite</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="f9fca-110">You must have the following to successfully complete this Apache Kafka tutorial:</span><span class="sxs-lookup"><span data-stu-id="f9fca-110">You must have the following to successfully complete this Apache Kafka tutorial:</span></span>

* <span data-ttu-id="f9fca-111">**An Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="f9fca-111">**An Azure subscription**.</span></span> <span data-ttu-id="f9fca-112">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="f9fca-112">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

* <span data-ttu-id="f9fca-113">**Familiarity with SSH and SCP**.</span><span class="sxs-lookup"><span data-stu-id="f9fca-113">**Familiarity with SSH and SCP**.</span></span> <span data-ttu-id="f9fca-114">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="f9fca-114">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="f9fca-115">[Java JDK 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) or an equivalent, such as OpenJDK.</span><span class="sxs-lookup"><span data-stu-id="f9fca-115">[Java JDK 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) or an equivalent, such as OpenJDK.</span></span>

* [<span data-ttu-id="f9fca-116">Apache Maven</span><span class="sxs-lookup"><span data-stu-id="f9fca-116">Apache Maven</span></span>](http://maven.apache.org/) 

### <a name="access-control-requirements"></a><span data-ttu-id="f9fca-117">Access control requirements</span><span class="sxs-lookup"><span data-stu-id="f9fca-117">Access control requirements</span></span>

[!INCLUDE [access-control](../../includes/hdinsight-access-control-requirements.md)]

## <a name="create-a-kafka-cluster"></a><span data-ttu-id="f9fca-118">Create a Kafka cluster</span><span class="sxs-lookup"><span data-stu-id="f9fca-118">Create a Kafka cluster</span></span>

<span data-ttu-id="f9fca-119">Use the following steps to create a Kafka on HDInsight cluster:</span><span class="sxs-lookup"><span data-stu-id="f9fca-119">Use the following steps to create a Kafka on HDInsight cluster:</span></span>

1. <span data-ttu-id="f9fca-120">From the [Azure portal](https://portal.azure.com), select **+ NEW**, **Intelligence + Analytics**, and then select **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="f9fca-120">From the [Azure portal](https://portal.azure.com), select **+ NEW**, **Intelligence + Analytics**, and then select **HDInsight**.</span></span>
   
    ![Create a HDInsight cluster](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-kafka-get-started/create-hdinsight.png)

2. <span data-ttu-id="f9fca-122">From the **Basics** blade, enter the following information:</span><span class="sxs-lookup"><span data-stu-id="f9fca-122">From the **Basics** blade, enter the following information:</span></span>

    * <span data-ttu-id="f9fca-123">**Cluster Name**: The name of the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="f9fca-123">**Cluster Name**: The name of the HDInsight cluster.</span></span>
    * <span data-ttu-id="f9fca-124">**Subscription**: Select the subscription to use.</span><span class="sxs-lookup"><span data-stu-id="f9fca-124">**Subscription**: Select the subscription to use.</span></span>
    * <span data-ttu-id="f9fca-125">**Cluster login username** and **Cluster login password**: The login when accessing the cluster over HTTPS.</span><span class="sxs-lookup"><span data-stu-id="f9fca-125">**Cluster login username** and **Cluster login password**: The login when accessing the cluster over HTTPS.</span></span> <span data-ttu-id="f9fca-126">You use these credentials to access services such as the Ambari Web UI or REST API.</span><span class="sxs-lookup"><span data-stu-id="f9fca-126">You use these credentials to access services such as the Ambari Web UI or REST API.</span></span>
    * <span data-ttu-id="f9fca-127">**Secure Shell (SSH) username**: The login used when accessing the cluster over SSH.</span><span class="sxs-lookup"><span data-stu-id="f9fca-127">**Secure Shell (SSH) username**: The login used when accessing the cluster over SSH.</span></span> <span data-ttu-id="f9fca-128">By default the password is the same as the cluster login password.</span><span class="sxs-lookup"><span data-stu-id="f9fca-128">By default the password is the same as the cluster login password.</span></span>
    * <span data-ttu-id="f9fca-129">**Resource Group**: The resource group to create the cluster in.</span><span class="sxs-lookup"><span data-stu-id="f9fca-129">**Resource Group**: The resource group to create the cluster in.</span></span>
    * <span data-ttu-id="f9fca-130">**Location**: The Azure region to create the cluster in.</span><span class="sxs-lookup"><span data-stu-id="f9fca-130">**Location**: The Azure region to create the cluster in.</span></span>
   
    ![Select subscription](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-kafka-get-started/hdinsight-basic-configuration.png)

3. <span data-ttu-id="f9fca-132">Select **Cluster type**, and then set the following values on the **Cluster configuration** blade:</span><span class="sxs-lookup"><span data-stu-id="f9fca-132">Select **Cluster type**, and then set the following values on the **Cluster configuration** blade:</span></span>
   
    * <span data-ttu-id="f9fca-133">**Cluster Type**: Kafka</span><span class="sxs-lookup"><span data-stu-id="f9fca-133">**Cluster Type**: Kafka</span></span>

    * <span data-ttu-id="f9fca-134">**Version**: Kafka 0.10.0 (HDI 3.5)</span><span class="sxs-lookup"><span data-stu-id="f9fca-134">**Version**: Kafka 0.10.0 (HDI 3.5)</span></span>

    * <span data-ttu-id="f9fca-135">**Cluster Tier**: Standard</span><span class="sxs-lookup"><span data-stu-id="f9fca-135">**Cluster Tier**: Standard</span></span>
     
    <span data-ttu-id="f9fca-136">Finally, use the **Select** button to save settings.</span><span class="sxs-lookup"><span data-stu-id="f9fca-136">Finally, use the **Select** button to save settings.</span></span>
     
    ![Select cluster type](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-kafka-get-started/set-hdinsight-cluster-type.png)

    > [!NOTE]
    > <span data-ttu-id="f9fca-138">If your Azure subscription does not have access to the Kafka preview, instructions on how to gain access to the preview are displayed.</span><span class="sxs-lookup"><span data-stu-id="f9fca-138">If your Azure subscription does not have access to the Kafka preview, instructions on how to gain access to the preview are displayed.</span></span> <span data-ttu-id="f9fca-139">The instructions displayed are similar to the following image:</span><span class="sxs-lookup"><span data-stu-id="f9fca-139">The instructions displayed are similar to the following image:</span></span>
    >
    > ![preview message: if you would like to deploy a managed Apache Kafka cluster on HDInsight, email us to request preview access](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-kafka-get-started/no-kafka-preview.png)

4. <span data-ttu-id="f9fca-141">After selecting the cluster type, use the __Select__ button to set the cluster type.</span><span class="sxs-lookup"><span data-stu-id="f9fca-141">After selecting the cluster type, use the __Select__ button to set the cluster type.</span></span> <span data-ttu-id="f9fca-142">Next, use the __Next__ button to finish basic configuration.</span><span class="sxs-lookup"><span data-stu-id="f9fca-142">Next, use the __Next__ button to finish basic configuration.</span></span>

5. <span data-ttu-id="f9fca-143">From the **Storage** blade, select or create a Storage account.</span><span class="sxs-lookup"><span data-stu-id="f9fca-143">From the **Storage** blade, select or create a Storage account.</span></span> <span data-ttu-id="f9fca-144">For the steps in this document, leave the other fields on this blade at the default values.</span><span class="sxs-lookup"><span data-stu-id="f9fca-144">For the steps in this document, leave the other fields on this blade at the default values.</span></span> <span data-ttu-id="f9fca-145">Use the __Next__ button to save storage configuration.</span><span class="sxs-lookup"><span data-stu-id="f9fca-145">Use the __Next__ button to save storage configuration.</span></span>

    ![Set the storage account settings for HDInsight](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-kafka-get-started/set-hdinsight-storage-account.png)

6. <span data-ttu-id="f9fca-147">From the **Summary** blade, review the configuration for the cluster.</span><span class="sxs-lookup"><span data-stu-id="f9fca-147">From the **Summary** blade, review the configuration for the cluster.</span></span> <span data-ttu-id="f9fca-148">Use the __Edit__ links to change any settings that are incorrect.</span><span class="sxs-lookup"><span data-stu-id="f9fca-148">Use the __Edit__ links to change any settings that are incorrect.</span></span> <span data-ttu-id="f9fca-149">Finally, use the__Create__ button to create the cluster.</span><span class="sxs-lookup"><span data-stu-id="f9fca-149">Finally, use the__Create__ button to create the cluster.</span></span>
   
    ![Cluster configuration summary](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-kafka-get-started/hdinsight-configuration-summary.png)
   
    > [!NOTE]
    > <span data-ttu-id="f9fca-151">It can take up to 20 minutes to create the cluster.</span><span class="sxs-lookup"><span data-stu-id="f9fca-151">It can take up to 20 minutes to create the cluster.</span></span>

## <a name="connect-to-the-cluster"></a><span data-ttu-id="f9fca-152">Connect to the cluster</span><span class="sxs-lookup"><span data-stu-id="f9fca-152">Connect to the cluster</span></span>

<span data-ttu-id="f9fca-153">From your client, use SSH to connect to the cluster.</span><span class="sxs-lookup"><span data-stu-id="f9fca-153">From your client, use SSH to connect to the cluster.</span></span> <span data-ttu-id="f9fca-154">If you are using a Linux, Unix, MacOS, or Bash on Windows 10, use the following command:</span><span class="sxs-lookup"><span data-stu-id="f9fca-154">If you are using a Linux, Unix, MacOS, or Bash on Windows 10, use the following command:</span></span>

```ssh SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net```

<span data-ttu-id="f9fca-155">Replace **SSHUSER** with the SSH username you provided during cluster creation.</span><span class="sxs-lookup"><span data-stu-id="f9fca-155">Replace **SSHUSER** with the SSH username you provided during cluster creation.</span></span> <span data-ttu-id="f9fca-156">Replace **CLUSTERNAME** with the name of the cluster.</span><span class="sxs-lookup"><span data-stu-id="f9fca-156">Replace **CLUSTERNAME** with the name of the cluster.</span></span>

<span data-ttu-id="f9fca-157">When prompted, enter the password you used for the SSH account.</span><span class="sxs-lookup"><span data-stu-id="f9fca-157">When prompted, enter the password you used for the SSH account.</span></span>

<span data-ttu-id="f9fca-158">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="f9fca-158">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

##<a id="getkafkainfo"></a><span data-ttu-id="f9fca-159">Get the Zookeeper and Broker host information</span><span class="sxs-lookup"><span data-stu-id="f9fca-159">Get the Zookeeper and Broker host information</span></span>

<span data-ttu-id="f9fca-160">When working with Kafka, you must know two host values; the *Zookeeper* hosts and the *Broker* hosts.</span><span class="sxs-lookup"><span data-stu-id="f9fca-160">When working with Kafka, you must know two host values; the *Zookeeper* hosts and the *Broker* hosts.</span></span> <span data-ttu-id="f9fca-161">These hosts are used with the Kafka API and many of the utilities that ship with Kafka.</span><span class="sxs-lookup"><span data-stu-id="f9fca-161">These hosts are used with the Kafka API and many of the utilities that ship with Kafka.</span></span>

<span data-ttu-id="f9fca-162">Use the following steps to create environment variables that contain the host information.</span><span class="sxs-lookup"><span data-stu-id="f9fca-162">Use the following steps to create environment variables that contain the host information.</span></span> <span data-ttu-id="f9fca-163">These environment variables are used in the steps in this document.</span><span class="sxs-lookup"><span data-stu-id="f9fca-163">These environment variables are used in the steps in this document.</span></span>

1. <span data-ttu-id="f9fca-164">From an SSH connection to the cluster, use the following command to install the `jq` utility.</span><span class="sxs-lookup"><span data-stu-id="f9fca-164">From an SSH connection to the cluster, use the following command to install the `jq` utility.</span></span> <span data-ttu-id="f9fca-165">This utility is used to parse JSON documents, and is useful in retrieving the broker host information:</span><span class="sxs-lookup"><span data-stu-id="f9fca-165">This utility is used to parse JSON documents, and is useful in retrieving the broker host information:</span></span>
   
    ```bash
    sudo apt -y install jq
    ```

2. <span data-ttu-id="f9fca-166">use the following commands to set the environment variables with information retrieved from Ambari.</span><span class="sxs-lookup"><span data-stu-id="f9fca-166">use the following commands to set the environment variables with information retrieved from Ambari.</span></span> <span data-ttu-id="f9fca-167">Replace __KAFKANAME__ with the name of the Kafka cluster.</span><span class="sxs-lookup"><span data-stu-id="f9fca-167">Replace __KAFKANAME__ with the name of the Kafka cluster.</span></span> <span data-ttu-id="f9fca-168">Replace __PASSWORD__ with the login (admin) password you used when creating the cluster.</span><span class="sxs-lookup"><span data-stu-id="f9fca-168">Replace __PASSWORD__ with the login (admin) password you used when creating the cluster.</span></span>

    ```bash
    export KAFKAZKHOSTS=`curl --silent -u admin:'PASSWORD' -G http://headnodehost:8080/api/v1/clusters/KAFKANAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")'`

    export KAFKABROKERS=`curl --silent -u admin:'PASSWORD' -G http://headnodehost:8080/api/v1/clusters/KAFKANAME/services/HDFS/components/DATANODE | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")'`

    echo '$KAFKAZKHOSTS='$KAFKAZKHOSTS
    echo '$KAFKABROKERS='$KAFKABROKERS
    ```

    <span data-ttu-id="f9fca-169">The following text is an example of the contents of `$KAFKAZKHOSTS`:</span><span class="sxs-lookup"><span data-stu-id="f9fca-169">The following text is an example of the contents of `$KAFKAZKHOSTS`:</span></span>
   
    `zk0-kafka.eahjefxxp1netdbyklgqj5y1ud.ex.internal.cloudapp.net:2181,zk2-kafka.eahjefxxp1netdbyklgqj5y1ud.ex.internal.cloudapp.net:2181,zk3-kafka.eahjefxxp1netdbyklgqj5y1ud.ex.internal.cloudapp.net:2181`
   
    <span data-ttu-id="f9fca-170">The following text is an example of the contents of `$KAFKABROKERS`:</span><span class="sxs-lookup"><span data-stu-id="f9fca-170">The following text is an example of the contents of `$KAFKABROKERS`:</span></span>
   
    `wn1-kafka.eahjefxxp1netdbyklgqj5y1ud.cx.internal.cloudapp.net:9092,wn0-kafka.eahjefxxp1netdbyklgqj5y1ud.cx.internal.cloudapp.net:9092`
   
    > [!WARNING]
    > <span data-ttu-id="f9fca-171">Do not rely on the information returned from this session to always be accurate.</span><span class="sxs-lookup"><span data-stu-id="f9fca-171">Do not rely on the information returned from this session to always be accurate.</span></span> <span data-ttu-id="f9fca-172">If you scale the cluster, new brokers are added or removed.</span><span class="sxs-lookup"><span data-stu-id="f9fca-172">If you scale the cluster, new brokers are added or removed.</span></span> <span data-ttu-id="f9fca-173">If a failure occurs and a node is replaced, the host name for the node may change.</span><span class="sxs-lookup"><span data-stu-id="f9fca-173">If a failure occurs and a node is replaced, the host name for the node may change.</span></span> 
    > 
    > <span data-ttu-id="f9fca-174">You should retrieve the Zookeeper and broker hosts information shortly before you use it to ensure you have valid information.</span><span class="sxs-lookup"><span data-stu-id="f9fca-174">You should retrieve the Zookeeper and broker hosts information shortly before you use it to ensure you have valid information.</span></span>

## <a name="create-a-topic"></a><span data-ttu-id="f9fca-175">Create a topic</span><span class="sxs-lookup"><span data-stu-id="f9fca-175">Create a topic</span></span>

<span data-ttu-id="f9fca-176">Kafka stores streams of data in categories called *topics*.</span><span class="sxs-lookup"><span data-stu-id="f9fca-176">Kafka stores streams of data in categories called *topics*.</span></span> <span data-ttu-id="f9fca-177">From An SSH connection to a cluster headnode, use a script provided with Kafka to create a topic:</span><span class="sxs-lookup"><span data-stu-id="f9fca-177">From An SSH connection to a cluster headnode, use a script provided with Kafka to create a topic:</span></span>

```bash
/usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 2 --partitions 8 --topic test --zookeeper $KAFKAZKHOSTS
```

<span data-ttu-id="f9fca-178">This command connects to Zookeeper using the host information stored in `$KAFKAZKHOSTS`, and then create Kafka topic named **test**.</span><span class="sxs-lookup"><span data-stu-id="f9fca-178">This command connects to Zookeeper using the host information stored in `$KAFKAZKHOSTS`, and then create Kafka topic named **test**.</span></span> <span data-ttu-id="f9fca-179">You can verify that the topic was created by using the following script to list topics:</span><span class="sxs-lookup"><span data-stu-id="f9fca-179">You can verify that the topic was created by using the following script to list topics:</span></span>

```bash
/usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $KAFKAZKHOSTS
```

<span data-ttu-id="f9fca-180">The output of this command lists Kafka topics, which contains the **test** topic.</span><span class="sxs-lookup"><span data-stu-id="f9fca-180">The output of this command lists Kafka topics, which contains the **test** topic.</span></span>

## <a name="produce-and-consume-records"></a><span data-ttu-id="f9fca-181">Produce and consume records</span><span class="sxs-lookup"><span data-stu-id="f9fca-181">Produce and consume records</span></span>

<span data-ttu-id="f9fca-182">Kafka stores *records* in topics.</span><span class="sxs-lookup"><span data-stu-id="f9fca-182">Kafka stores *records* in topics.</span></span> <span data-ttu-id="f9fca-183">Records are produced by *producers*, and consumed by *consumers*.</span><span class="sxs-lookup"><span data-stu-id="f9fca-183">Records are produced by *producers*, and consumed by *consumers*.</span></span> <span data-ttu-id="f9fca-184">Producers retrieve records from Kafka *brokers*.</span><span class="sxs-lookup"><span data-stu-id="f9fca-184">Producers retrieve records from Kafka *brokers*.</span></span> <span data-ttu-id="f9fca-185">Each worker node in your HDInsight cluster is a Kafka broker.</span><span class="sxs-lookup"><span data-stu-id="f9fca-185">Each worker node in your HDInsight cluster is a Kafka broker.</span></span>

<span data-ttu-id="f9fca-186">Use the following steps to store records into the test topic you created earlier, and then read them using a consumer:</span><span class="sxs-lookup"><span data-stu-id="f9fca-186">Use the following steps to store records into the test topic you created earlier, and then read them using a consumer:</span></span>

1. <span data-ttu-id="f9fca-187">From the SSH session, use a script provided with Kafka to write records to the topic:</span><span class="sxs-lookup"><span data-stu-id="f9fca-187">From the SSH session, use a script provided with Kafka to write records to the topic:</span></span>
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-producer.sh --broker-list $KAFKABROKERS --topic test
    ```
   
    <span data-ttu-id="f9fca-188">You are not returned to the prompt after this command.</span><span class="sxs-lookup"><span data-stu-id="f9fca-188">You are not returned to the prompt after this command.</span></span> <span data-ttu-id="f9fca-189">Instead, type a few text messages and then use **Ctrl + C** to stop sending to the topic.</span><span class="sxs-lookup"><span data-stu-id="f9fca-189">Instead, type a few text messages and then use **Ctrl + C** to stop sending to the topic.</span></span> <span data-ttu-id="f9fca-190">Each line is sent as a separate record.</span><span class="sxs-lookup"><span data-stu-id="f9fca-190">Each line is sent as a separate record.</span></span>

2. <span data-ttu-id="f9fca-191">Use a script provided with Kafka to read records from the topic:</span><span class="sxs-lookup"><span data-stu-id="f9fca-191">Use a script provided with Kafka to read records from the topic:</span></span>
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --zookeeper $KAFKAZKHOSTS --topic test --from-beginning
    ```
   
    <span data-ttu-id="f9fca-192">This retrieves the records from the topic and display them.</span><span class="sxs-lookup"><span data-stu-id="f9fca-192">This retrieves the records from the topic and display them.</span></span> <span data-ttu-id="f9fca-193">Using `--from-beginning` tells the consumer to start from the beginning of the stream, so all records are retrieved.</span><span class="sxs-lookup"><span data-stu-id="f9fca-193">Using `--from-beginning` tells the consumer to start from the beginning of the stream, so all records are retrieved.</span></span>

3. <span data-ttu-id="f9fca-194">Use __Ctrl + C__ to stop the consumer.</span><span class="sxs-lookup"><span data-stu-id="f9fca-194">Use __Ctrl + C__ to stop the consumer.</span></span>

## <a name="producer-and-consumer-api"></a><span data-ttu-id="f9fca-195">Producer and consumer API</span><span class="sxs-lookup"><span data-stu-id="f9fca-195">Producer and consumer API</span></span>

<span data-ttu-id="f9fca-196">You can also programmatically produce and consume records using the [Kafka APIs](http://kafka.apache.org/documentation#api).</span><span class="sxs-lookup"><span data-stu-id="f9fca-196">You can also programmatically produce and consume records using the [Kafka APIs](http://kafka.apache.org/documentation#api).</span></span> <span data-ttu-id="f9fca-197">Use the following steps to download, build a Java-based producer and consumer:</span><span class="sxs-lookup"><span data-stu-id="f9fca-197">Use the following steps to download, build a Java-based producer and consumer:</span></span>

1. <span data-ttu-id="f9fca-198">Download the examples from [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started).</span><span class="sxs-lookup"><span data-stu-id="f9fca-198">Download the examples from [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started).</span></span> <span data-ttu-id="f9fca-199">For the producer/consumer example, use the project in the `Producer-Consumer` directory.</span><span class="sxs-lookup"><span data-stu-id="f9fca-199">For the producer/consumer example, use the project in the `Producer-Consumer` directory.</span></span> <span data-ttu-id="f9fca-200">This example contains the following classes:</span><span class="sxs-lookup"><span data-stu-id="f9fca-200">This example contains the following classes:</span></span>
   
    * <span data-ttu-id="f9fca-201">**Run** - starts either the consumer or producer.</span><span class="sxs-lookup"><span data-stu-id="f9fca-201">**Run** - starts either the consumer or producer.</span></span>

    * <span data-ttu-id="f9fca-202">**Producer** - stores 1,000,000 records to the topic.</span><span class="sxs-lookup"><span data-stu-id="f9fca-202">**Producer** - stores 1,000,000 records to the topic.</span></span>

    * <span data-ttu-id="f9fca-203">**Consumer** - reads records from the topic.</span><span class="sxs-lookup"><span data-stu-id="f9fca-203">**Consumer** - reads records from the topic.</span></span>

2. <span data-ttu-id="f9fca-204">From the command line in your development environment, change directories to the location of the `Producer-Consumer` directory of the example and then use the following command to create a jar package:</span><span class="sxs-lookup"><span data-stu-id="f9fca-204">From the command line in your development environment, change directories to the location of the `Producer-Consumer` directory of the example and then use the following command to create a jar package:</span></span>
   
    ```
    mvn clean package
    ```
   
    <span data-ttu-id="f9fca-205">This command creates a directory named `target`, that contains a file named `kafka-producer-consumer-1.0-SNAPSHOT.jar`.</span><span class="sxs-lookup"><span data-stu-id="f9fca-205">This command creates a directory named `target`, that contains a file named `kafka-producer-consumer-1.0-SNAPSHOT.jar`.</span></span>

3. <span data-ttu-id="f9fca-206">Use the following commands to copy the `kafka-producer-consumer-1.0-SNAPSHOT.jar` file to your HDInsight cluster:</span><span class="sxs-lookup"><span data-stu-id="f9fca-206">Use the following commands to copy the `kafka-producer-consumer-1.0-SNAPSHOT.jar` file to your HDInsight cluster:</span></span>
   
    ```bash
    scp ./target/kafka-producer-consumer-1.0-SNAPSHOT.jar SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net:kafka-producer-consumer.jar
    ```
   
    <span data-ttu-id="f9fca-207">Replace **SSHUSER** with the SSH user for your cluster, and replace **CLUSTERNAME** with the name of your cluster.</span><span class="sxs-lookup"><span data-stu-id="f9fca-207">Replace **SSHUSER** with the SSH user for your cluster, and replace **CLUSTERNAME** with the name of your cluster.</span></span> <span data-ttu-id="f9fca-208">When prompted enter the password for the SSH user.</span><span class="sxs-lookup"><span data-stu-id="f9fca-208">When prompted enter the password for the SSH user.</span></span>

4. <span data-ttu-id="f9fca-209">Once the `scp` command finishes copying the file, connect to the cluster using SSH, and then use the following to write records to the test topic you created earlier.</span><span class="sxs-lookup"><span data-stu-id="f9fca-209">Once the `scp` command finishes copying the file, connect to the cluster using SSH, and then use the following to write records to the test topic you created earlier.</span></span>
   
    ```bash
    ./kafka-producer-consumer.jar producer $KAFKABROKERS
    ```
   
    <span data-ttu-id="f9fca-210">This command starts the producer and write records.</span><span class="sxs-lookup"><span data-stu-id="f9fca-210">This command starts the producer and write records.</span></span> <span data-ttu-id="f9fca-211">A counter is displayed so you can see how many records have been written.</span><span class="sxs-lookup"><span data-stu-id="f9fca-211">A counter is displayed so you can see how many records have been written.</span></span>

    > [!NOTE]
    > <span data-ttu-id="f9fca-212">If you receive a permission denied error, use the following command to make the file executable: ```chmod +x kafka-producer-consumer.jar```</span><span class="sxs-lookup"><span data-stu-id="f9fca-212">If you receive a permission denied error, use the following command to make the file executable: ```chmod +x kafka-producer-consumer.jar```</span></span>

5. <span data-ttu-id="f9fca-213">Once the process has finished, use the following command to read from the topic:</span><span class="sxs-lookup"><span data-stu-id="f9fca-213">Once the process has finished, use the following command to read from the topic:</span></span>
   
    ```bash
    ./kafka-producer-consumer.jar consumer $KAFKABROKERS
    ```
   
    <span data-ttu-id="f9fca-214">The records read, along with a count of records, is displayed.</span><span class="sxs-lookup"><span data-stu-id="f9fca-214">The records read, along with a count of records, is displayed.</span></span> <span data-ttu-id="f9fca-215">You may see a few more than 1,000,000 logged as you sent several records to the topic using a script in an earlier step.</span><span class="sxs-lookup"><span data-stu-id="f9fca-215">You may see a few more than 1,000,000 logged as you sent several records to the topic using a script in an earlier step.</span></span>

6. <span data-ttu-id="f9fca-216">Use __Ctrl + C__ to exit the consumer.</span><span class="sxs-lookup"><span data-stu-id="f9fca-216">Use __Ctrl + C__ to exit the consumer.</span></span>

### <a name="multiple-consumers"></a><span data-ttu-id="f9fca-217">Multiple consumers</span><span class="sxs-lookup"><span data-stu-id="f9fca-217">Multiple consumers</span></span>

<span data-ttu-id="f9fca-218">An important concept with Kafka is that consumers use a consumer group (defined by a group id) when reading records.</span><span class="sxs-lookup"><span data-stu-id="f9fca-218">An important concept with Kafka is that consumers use a consumer group (defined by a group id) when reading records.</span></span> <span data-ttu-id="f9fca-219">Using the same group with multiple consumers results in load balanced reads from a topic.</span><span class="sxs-lookup"><span data-stu-id="f9fca-219">Using the same group with multiple consumers results in load balanced reads from a topic.</span></span> <span data-ttu-id="f9fca-220">Each consumer in the group receives a portion of the records.</span><span class="sxs-lookup"><span data-stu-id="f9fca-220">Each consumer in the group receives a portion of the records.</span></span> <span data-ttu-id="f9fca-221">To see this process in action, use the following steps:</span><span class="sxs-lookup"><span data-stu-id="f9fca-221">To see this process in action, use the following steps:</span></span>

1. <span data-ttu-id="f9fca-222">Open a new SSH session to the cluster, so that you have two of them.</span><span class="sxs-lookup"><span data-stu-id="f9fca-222">Open a new SSH session to the cluster, so that you have two of them.</span></span> <span data-ttu-id="f9fca-223">In each session, use the following to start a consumer with the same consumer group id:</span><span class="sxs-lookup"><span data-stu-id="f9fca-223">In each session, use the following to start a consumer with the same consumer group id:</span></span>
   
    ```bash
    ./kafka-producer-consumer.jar consumer $KAFKABROKERS mygroup
    ```

    > [!NOTE]
    > <span data-ttu-id="f9fca-224">Since this is a new SSH session, you must to use the commands in the [Get the Zookeeper and Broker host information](#getkafkainfo) section to set `$KAFKABROKERS`.</span><span class="sxs-lookup"><span data-stu-id="f9fca-224">Since this is a new SSH session, you must to use the commands in the [Get the Zookeeper and Broker host information](#getkafkainfo) section to set `$KAFKABROKERS`.</span></span>

2. <span data-ttu-id="f9fca-225">Watch as each session counts the records it receives from the topic.</span><span class="sxs-lookup"><span data-stu-id="f9fca-225">Watch as each session counts the records it receives from the topic.</span></span> <span data-ttu-id="f9fca-226">The total of both sessions should be the same as you received previously from one consumer.</span><span class="sxs-lookup"><span data-stu-id="f9fca-226">The total of both sessions should be the same as you received previously from one consumer.</span></span>

<span data-ttu-id="f9fca-227">Consumption by clients within the same group is handled through the partitions for the topic.</span><span class="sxs-lookup"><span data-stu-id="f9fca-227">Consumption by clients within the same group is handled through the partitions for the topic.</span></span> <span data-ttu-id="f9fca-228">For the `test` topic created earlier, it has eight partitions.</span><span class="sxs-lookup"><span data-stu-id="f9fca-228">For the `test` topic created earlier, it has eight partitions.</span></span> <span data-ttu-id="f9fca-229">If you open eight SSH sessions and launch a consumer in all sessions, each consumer reads records from a single partition for the topic.</span><span class="sxs-lookup"><span data-stu-id="f9fca-229">If you open eight SSH sessions and launch a consumer in all sessions, each consumer reads records from a single partition for the topic.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f9fca-230">There cannot be more consumer instances in a consumer group than partitions.</span><span class="sxs-lookup"><span data-stu-id="f9fca-230">There cannot be more consumer instances in a consumer group than partitions.</span></span> <span data-ttu-id="f9fca-231">In this example, one consumer group can contain up to 8 consumers since that is the number of partitions in the topic.</span><span class="sxs-lookup"><span data-stu-id="f9fca-231">In this example, one consumer group can contain up to 8 consumers since that is the number of partitions in the topic.</span></span> <span data-ttu-id="f9fca-232">Or you can have multiple consumer groups, each with no more than 8 consumers.</span><span class="sxs-lookup"><span data-stu-id="f9fca-232">Or you can have multiple consumer groups, each with no more than 8 consumers.</span></span>

<span data-ttu-id="f9fca-233">Records stored in Kafka are stored in the order they are received within a partition.</span><span class="sxs-lookup"><span data-stu-id="f9fca-233">Records stored in Kafka are stored in the order they are received within a partition.</span></span> <span data-ttu-id="f9fca-234">To achieve in-ordered delivery for records *within a partition*, create a consumer group where the number of consumer instances matches the number of partitions.</span><span class="sxs-lookup"><span data-stu-id="f9fca-234">To achieve in-ordered delivery for records *within a partition*, create a consumer group where the number of consumer instances matches the number of partitions.</span></span> <span data-ttu-id="f9fca-235">To achieve in-ordered delivery for records *within the topic*, create a consumer group with only one consumer instance.</span><span class="sxs-lookup"><span data-stu-id="f9fca-235">To achieve in-ordered delivery for records *within the topic*, create a consumer group with only one consumer instance.</span></span>

## <a name="streaming-api"></a><span data-ttu-id="f9fca-236">Streaming API</span><span class="sxs-lookup"><span data-stu-id="f9fca-236">Streaming API</span></span>

<span data-ttu-id="f9fca-237">The streaming API was added to Kafka in version 0.10.0; earlier versions rely on Apache Spark or Storm for stream processing.</span><span class="sxs-lookup"><span data-stu-id="f9fca-237">The streaming API was added to Kafka in version 0.10.0; earlier versions rely on Apache Spark or Storm for stream processing.</span></span>

1. <span data-ttu-id="f9fca-238">If you haven't already done so, download the examples from [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started) to your development environment.</span><span class="sxs-lookup"><span data-stu-id="f9fca-238">If you haven't already done so, download the examples from [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started) to your development environment.</span></span> <span data-ttu-id="f9fca-239">For the streaming example, use the project in the `streaming` directory.</span><span class="sxs-lookup"><span data-stu-id="f9fca-239">For the streaming example, use the project in the `streaming` directory.</span></span>
   
    <span data-ttu-id="f9fca-240">This project contains only one class, `Stream`, which reads records from the `test` topic created previously.</span><span class="sxs-lookup"><span data-stu-id="f9fca-240">This project contains only one class, `Stream`, which reads records from the `test` topic created previously.</span></span> <span data-ttu-id="f9fca-241">It counts the words read, and emits each word and count to a topic named `wordcounts`.</span><span class="sxs-lookup"><span data-stu-id="f9fca-241">It counts the words read, and emits each word and count to a topic named `wordcounts`.</span></span> <span data-ttu-id="f9fca-242">The `wordcounts` topic is created in a later step in this section.</span><span class="sxs-lookup"><span data-stu-id="f9fca-242">The `wordcounts` topic is created in a later step in this section.</span></span>

2. <span data-ttu-id="f9fca-243">From the command line in your development environment, change directories to the location of the `Streaming` directory, and then use the following command to create a jar package:</span><span class="sxs-lookup"><span data-stu-id="f9fca-243">From the command line in your development environment, change directories to the location of the `Streaming` directory, and then use the following command to create a jar package:</span></span>
   
    ```
    mvn clean package
    ```
   
    <span data-ttu-id="f9fca-244">This command creates a directory named `target`, which contains a file named `kafka-streaming-1.0-SNAPSHOT.jar`.</span><span class="sxs-lookup"><span data-stu-id="f9fca-244">This command creates a directory named `target`, which contains a file named `kafka-streaming-1.0-SNAPSHOT.jar`.</span></span>

3. <span data-ttu-id="f9fca-245">Use the following commands to copy the `kafka-streaming-1.0-SNAPSHOT.jar` file to your HDInsight cluster:</span><span class="sxs-lookup"><span data-stu-id="f9fca-245">Use the following commands to copy the `kafka-streaming-1.0-SNAPSHOT.jar` file to your HDInsight cluster:</span></span>
   
    ```bash
    scp ./target/kafka-streaming-1.0-SNAPSHOT.jar SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net:kafka-streaming.jar
    ```
   
    <span data-ttu-id="f9fca-246">Replace **SSHUSER** with the SSH user for your cluster, and replace **CLUSTERNAME** with the name of your cluster.</span><span class="sxs-lookup"><span data-stu-id="f9fca-246">Replace **SSHUSER** with the SSH user for your cluster, and replace **CLUSTERNAME** with the name of your cluster.</span></span> <span data-ttu-id="f9fca-247">When prompted enter the password for the SSH user.</span><span class="sxs-lookup"><span data-stu-id="f9fca-247">When prompted enter the password for the SSH user.</span></span>

4. <span data-ttu-id="f9fca-248">Once the `scp` command finishes copying the file, connect to the cluster using SSH, and then use the following command to create the `wordcounts` topic:</span><span class="sxs-lookup"><span data-stu-id="f9fca-248">Once the `scp` command finishes copying the file, connect to the cluster using SSH, and then use the following command to create the `wordcounts` topic:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 2 --partitions 8 --topic wordcounts --zookeeper $KAFKAZKHOSTS
    ```

5. <span data-ttu-id="f9fca-249">Next, start the streaming process by using the following command:</span><span class="sxs-lookup"><span data-stu-id="f9fca-249">Next, start the streaming process by using the following command:</span></span>
   
    ```bash
    ./kafka-streaming.jar $KAFKABROKERS $KAFKAZKHOSTS 2>/dev/null &
    ```
   
    <span data-ttu-id="f9fca-250">This command starts the streaming process in the background.</span><span class="sxs-lookup"><span data-stu-id="f9fca-250">This command starts the streaming process in the background.</span></span>

6. <span data-ttu-id="f9fca-251">Use the following command to send messages to the `test` topic.</span><span class="sxs-lookup"><span data-stu-id="f9fca-251">Use the following command to send messages to the `test` topic.</span></span> <span data-ttu-id="f9fca-252">These messages are processed by the streaming example:</span><span class="sxs-lookup"><span data-stu-id="f9fca-252">These messages are processed by the streaming example:</span></span>
   
    ```bash
    ./kafka-producer-consumer.jar producer $KAFKABROKERS &>/dev/null &
    ```

7. <span data-ttu-id="f9fca-253">Use the following command to view the output that is written to the `wordcounts` topic by the streaming process:</span><span class="sxs-lookup"><span data-stu-id="f9fca-253">Use the following command to view the output that is written to the `wordcounts` topic by the streaming process:</span></span>
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --zookeeper $KAFKAZKHOSTS --topic wordcounts --from-beginning --formatter kafka.tools.DefaultMessageFormatter --property print.key=true --property key.deserializer=org.apache.kafka.common.serialization.StringDeserializer --property value.deserializer=org.apache.kafka.common.serialization.LongDeserializer
    ```
   
    > [!NOTE]
    > <span data-ttu-id="f9fca-254">To view the data, you must tell the consumer to print the key and the deserializer to use for the key and value.</span><span class="sxs-lookup"><span data-stu-id="f9fca-254">To view the data, you must tell the consumer to print the key and the deserializer to use for the key and value.</span></span> <span data-ttu-id="f9fca-255">The key name is the word, and the key value contains the count.</span><span class="sxs-lookup"><span data-stu-id="f9fca-255">The key name is the word, and the key value contains the count.</span></span>
   
    <span data-ttu-id="f9fca-256">The output is similar to the following text:</span><span class="sxs-lookup"><span data-stu-id="f9fca-256">The output is similar to the following text:</span></span>
   
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
        a       13805
        snow    13637
   
    > [!NOTE]
    > <span data-ttu-id="f9fca-257">The count increments each time a word is encountered.</span><span class="sxs-lookup"><span data-stu-id="f9fca-257">The count increments each time a word is encountered.</span></span>

7. <span data-ttu-id="f9fca-258">Use the __Ctrl + C__ to exit the consumer, then use the `fg` command to bring the streaming background task back to the foreground.</span><span class="sxs-lookup"><span data-stu-id="f9fca-258">Use the __Ctrl + C__ to exit the consumer, then use the `fg` command to bring the streaming background task back to the foreground.</span></span> <span data-ttu-id="f9fca-259">Use __Ctrl + C__ to exit it also.</span><span class="sxs-lookup"><span data-stu-id="f9fca-259">Use __Ctrl + C__ to exit it also.</span></span>

## <a name="delete-the-cluster"></a><span data-ttu-id="f9fca-260">Delete the cluster</span><span class="sxs-lookup"><span data-stu-id="f9fca-260">Delete the cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="f9fca-261">Next steps</span><span class="sxs-lookup"><span data-stu-id="f9fca-261">Next steps</span></span>

<span data-ttu-id="f9fca-262">In this document, you have learned the basics of working with Apache Kafka on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f9fca-262">In this document, you have learned the basics of working with Apache Kafka on HDInsight.</span></span> <span data-ttu-id="f9fca-263">Use the following to learn more about working with Kafka:</span><span class="sxs-lookup"><span data-stu-id="f9fca-263">Use the following to learn more about working with Kafka:</span></span>

* <span data-ttu-id="f9fca-264">[Apache Kafka documentation](http://kafka.apache.org/documentation.html) at kafka.apache.org.</span><span class="sxs-lookup"><span data-stu-id="f9fca-264">[Apache Kafka documentation](http://kafka.apache.org/documentation.html) at kafka.apache.org.</span></span>
* [<span data-ttu-id="f9fca-265">Use MirrorMaker to create a replica of Kafka on HDInsight</span><span class="sxs-lookup"><span data-stu-id="f9fca-265">Use MirrorMaker to create a replica of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)
* [<span data-ttu-id="f9fca-266">Use Apache Storm with Kafka on HDInsight</span><span class="sxs-lookup"><span data-stu-id="f9fca-266">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)
* [<span data-ttu-id="f9fca-267">Use Apache Spark with Kafka on HDInsight</span><span class="sxs-lookup"><span data-stu-id="f9fca-267">Use Apache Spark with Kafka on HDInsight</span></span>](hdinsight-apache-spark-with-kafka.md)
* [<span data-ttu-id="f9fca-268">Connect to Kafka through an Azure Virtual Network</span><span class="sxs-lookup"><span data-stu-id="f9fca-268">Connect to Kafka through an Azure Virtual Network</span></span>](hdinsight-apache-kafka-connect-vpn-gateway.md)





