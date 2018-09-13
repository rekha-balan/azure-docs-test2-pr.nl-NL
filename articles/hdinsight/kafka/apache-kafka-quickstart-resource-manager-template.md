---
title: Start with Apache Kafka - Azure HDInsight Quickstart
description: In this quickstart, you learn how to create an Apache Kafka cluster on Azure HDInsight using the Azure portal. You also learn about Kafka topics, subscribers, and consumers.
services: hdinsight
ms.service: hdinsight
author: jasonwhowell
ms.author: jasonh
ms.custom: mvc,hdinsightactive
ms.topic: quickstart
ms.date: 04/16/2018
ms.openlocfilehash: e8f8ad9b7cc14d6a3d28832e4d14ef55e8c530c6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864711"
---
# <a name="quickstart-create-a-kafka-on-hdinsight-cluster"></a><span data-ttu-id="1ad3b-104">Quickstart: Create a Kafka on HDInsight cluster</span><span class="sxs-lookup"><span data-stu-id="1ad3b-104">Quickstart: Create a Kafka on HDInsight cluster</span></span>

<span data-ttu-id="1ad3b-105">Kafka is an open-source, distributed streaming platform.</span><span class="sxs-lookup"><span data-stu-id="1ad3b-105">Kafka is an open-source, distributed streaming platform.</span></span> <span data-ttu-id="1ad3b-106">It's often used as a message broker, as it provides functionality similar to a publish-subscribe message queue.</span><span class="sxs-lookup"><span data-stu-id="1ad3b-106">It's often used as a message broker, as it provides functionality similar to a publish-subscribe message queue.</span></span> 

<span data-ttu-id="1ad3b-107">In this quickstart, you learn how to create an [Apache Kafka](https://kafka.apache.org) cluster using an Azure Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="1ad3b-107">In this quickstart, you learn how to create an [Apache Kafka](https://kafka.apache.org) cluster using an Azure Resource Manager template.</span></span> <span data-ttu-id="1ad3b-108">You also learn how to use included utilities to send and receive messages using Kafka.</span><span class="sxs-lookup"><span data-stu-id="1ad3b-108">You also learn how to use included utilities to send and receive messages using Kafka.</span></span>

[!INCLUDE [delete-cluster-warning](../../../includes/hdinsight-delete-cluster-warning.md)]

> [!IMPORTANT]
> <span data-ttu-id="1ad3b-109">The Kafka API can only be accessed by resources inside the same virtual network.</span><span class="sxs-lookup"><span data-stu-id="1ad3b-109">The Kafka API can only be accessed by resources inside the same virtual network.</span></span> <span data-ttu-id="1ad3b-110">In this quickstart, you access the cluster directly using SSH.</span><span class="sxs-lookup"><span data-stu-id="1ad3b-110">In this quickstart, you access the cluster directly using SSH.</span></span> <span data-ttu-id="1ad3b-111">To connect other services, networks, or virtual machines to Kafka, you must first create a virtual network and then create the resources within the network.</span><span class="sxs-lookup"><span data-stu-id="1ad3b-111">To connect other services, networks, or virtual machines to Kafka, you must first create a virtual network and then create the resources within the network.</span></span>
>
> <span data-ttu-id="1ad3b-112">For more information, see the [Connect to Kafka using a virtual network](apache-kafka-connect-vpn-gateway.md) document.</span><span class="sxs-lookup"><span data-stu-id="1ad3b-112">For more information, see the [Connect to Kafka using a virtual network](apache-kafka-connect-vpn-gateway.md) document.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1ad3b-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="1ad3b-113">Prerequisites</span></span>

* <span data-ttu-id="1ad3b-114">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="1ad3b-114">An Azure subscription.</span></span> <span data-ttu-id="1ad3b-115">If you don’t have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="1ad3b-115">If you don’t have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

* <span data-ttu-id="1ad3b-116">An SSH client.</span><span class="sxs-lookup"><span data-stu-id="1ad3b-116">An SSH client.</span></span> <span data-ttu-id="1ad3b-117">The steps in this document use SSH to connect to the cluster.</span><span class="sxs-lookup"><span data-stu-id="1ad3b-117">The steps in this document use SSH to connect to the cluster.</span></span>

    <span data-ttu-id="1ad3b-118">The `ssh` command is provided by default on Linux, Unix, and macOS systems.</span><span class="sxs-lookup"><span data-stu-id="1ad3b-118">The `ssh` command is provided by default on Linux, Unix, and macOS systems.</span></span> <span data-ttu-id="1ad3b-119">On Windows 10, use one of the following methods to install the `ssh` command:</span><span class="sxs-lookup"><span data-stu-id="1ad3b-119">On Windows 10, use one of the following methods to install the `ssh` command:</span></span>

    * <span data-ttu-id="1ad3b-120">Use the [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/quickstart).</span><span class="sxs-lookup"><span data-stu-id="1ad3b-120">Use the [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/quickstart).</span></span> <span data-ttu-id="1ad3b-121">The cloud shell provides the `ssh` command, and can be configured to use either Bash or PowerShell as the shell environment.</span><span class="sxs-lookup"><span data-stu-id="1ad3b-121">The cloud shell provides the `ssh` command, and can be configured to use either Bash or PowerShell as the shell environment.</span></span>

    * <span data-ttu-id="1ad3b-122">[Install the Windows Subsystem for Linux](https://docs.microsoft.com/windows/wsl/install-win10).</span><span class="sxs-lookup"><span data-stu-id="1ad3b-122">[Install the Windows Subsystem for Linux](https://docs.microsoft.com/windows/wsl/install-win10).</span></span> <span data-ttu-id="1ad3b-123">The Linux distributions available through the Microsoft Store provide the `ssh` command.</span><span class="sxs-lookup"><span data-stu-id="1ad3b-123">The Linux distributions available through the Microsoft Store provide the `ssh` command.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="1ad3b-124">The steps in this document assume that you are using one of the SSH clients mentioned above.</span><span class="sxs-lookup"><span data-stu-id="1ad3b-124">The steps in this document assume that you are using one of the SSH clients mentioned above.</span></span> <span data-ttu-id="1ad3b-125">If you are using a different SSH client and encounter problems, please consult the documentation for your SSH client.</span><span class="sxs-lookup"><span data-stu-id="1ad3b-125">If you are using a different SSH client and encounter problems, please consult the documentation for your SSH client.</span></span>
    >
    > <span data-ttu-id="1ad3b-126">For more information, see the [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md) document.</span><span class="sxs-lookup"><span data-stu-id="1ad3b-126">For more information, see the [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

## <a name="create-a-kafka-cluster"></a><span data-ttu-id="1ad3b-127">Create a Kafka cluster</span><span class="sxs-lookup"><span data-stu-id="1ad3b-127">Create a Kafka cluster</span></span>

1. <span data-ttu-id="1ad3b-128">Click the following image to open the template in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="1ad3b-128">Click the following image to open the template in the Azure portal.</span></span>

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure-Samples%2Fhdinsight-kafka-java-get-started%2Fmaster%2Fazuredeploy.json" target="_blank"><img src="./media/apache-kafka-quickstart-resource-manager-template/deploy-to-azure.png" alt="Deploy to Azure"></a>

2. <span data-ttu-id="1ad3b-129">To create the Kafka cluster, use the following values:</span><span class="sxs-lookup"><span data-stu-id="1ad3b-129">To create the Kafka cluster, use the following values:</span></span>

    | <span data-ttu-id="1ad3b-130">Property</span><span class="sxs-lookup"><span data-stu-id="1ad3b-130">Property</span></span> | <span data-ttu-id="1ad3b-131">Value</span><span class="sxs-lookup"><span data-stu-id="1ad3b-131">Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="1ad3b-132">Subscription</span><span class="sxs-lookup"><span data-stu-id="1ad3b-132">Subscription</span></span> | <span data-ttu-id="1ad3b-133">Your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="1ad3b-133">Your Azure subscription.</span></span> |
    | <span data-ttu-id="1ad3b-134">Resource group</span><span class="sxs-lookup"><span data-stu-id="1ad3b-134">Resource group</span></span> | <span data-ttu-id="1ad3b-135">The resource group that the cluster is created in.</span><span class="sxs-lookup"><span data-stu-id="1ad3b-135">The resource group that the cluster is created in.</span></span> |
    | <span data-ttu-id="1ad3b-136">Location</span><span class="sxs-lookup"><span data-stu-id="1ad3b-136">Location</span></span> | <span data-ttu-id="1ad3b-137">The Azure region that the cluster is created in.</span><span class="sxs-lookup"><span data-stu-id="1ad3b-137">The Azure region that the cluster is created in.</span></span> |
    | <span data-ttu-id="1ad3b-138">Cluster Name</span><span class="sxs-lookup"><span data-stu-id="1ad3b-138">Cluster Name</span></span> | <span data-ttu-id="1ad3b-139">The name of the Kafka cluster.</span><span class="sxs-lookup"><span data-stu-id="1ad3b-139">The name of the Kafka cluster.</span></span> |
    | <span data-ttu-id="1ad3b-140">Cluster Login User Name</span><span class="sxs-lookup"><span data-stu-id="1ad3b-140">Cluster Login User Name</span></span> | <span data-ttu-id="1ad3b-141">The account name used to login to HTTPs-based services on hosted on the cluster.</span><span class="sxs-lookup"><span data-stu-id="1ad3b-141">The account name used to login to HTTPs-based services on hosted on the cluster.</span></span> |
    | <span data-ttu-id="1ad3b-142">Cluster Login Password</span><span class="sxs-lookup"><span data-stu-id="1ad3b-142">Cluster Login Password</span></span> | <span data-ttu-id="1ad3b-143">The password for the login user name.</span><span class="sxs-lookup"><span data-stu-id="1ad3b-143">The password for the login user name.</span></span> |
    | <span data-ttu-id="1ad3b-144">SSH User Name</span><span class="sxs-lookup"><span data-stu-id="1ad3b-144">SSH User Name</span></span> | <span data-ttu-id="1ad3b-145">The SSH user name.</span><span class="sxs-lookup"><span data-stu-id="1ad3b-145">The SSH user name.</span></span> <span data-ttu-id="1ad3b-146">This account can access the cluster using SSH.</span><span class="sxs-lookup"><span data-stu-id="1ad3b-146">This account can access the cluster using SSH.</span></span> |
    | <span data-ttu-id="1ad3b-147">SSH Password</span><span class="sxs-lookup"><span data-stu-id="1ad3b-147">SSH Password</span></span> | <span data-ttu-id="1ad3b-148">The password for the SSH user.</span><span class="sxs-lookup"><span data-stu-id="1ad3b-148">The password for the SSH user.</span></span> |

    ![A screenshot of the template properties](./media/apache-kafka-quickstart-resource-manager-template/kafka-template-parameters.png)

3. <span data-ttu-id="1ad3b-150">Select **I agree to the terms and conditions stated above**, select **Pin to dashboard**, and then click **Purchase**.</span><span class="sxs-lookup"><span data-stu-id="1ad3b-150">Select **I agree to the terms and conditions stated above**, select **Pin to dashboard**, and then click **Purchase**.</span></span>

> [!NOTE]
> <span data-ttu-id="1ad3b-151">It can take up to 20 minutes to create the cluster.</span><span class="sxs-lookup"><span data-stu-id="1ad3b-151">It can take up to 20 minutes to create the cluster.</span></span>

## <a name="connect-to-the-cluster"></a><span data-ttu-id="1ad3b-152">Connect to the cluster</span><span class="sxs-lookup"><span data-stu-id="1ad3b-152">Connect to the cluster</span></span>

1. <span data-ttu-id="1ad3b-153">To connect to the primary head node of the Kafka cluster, use the following command.</span><span class="sxs-lookup"><span data-stu-id="1ad3b-153">To connect to the primary head node of the Kafka cluster, use the following command.</span></span> <span data-ttu-id="1ad3b-154">Replace `sshuser` with the SSH user name.</span><span class="sxs-lookup"><span data-stu-id="1ad3b-154">Replace `sshuser` with the SSH user name.</span></span> <span data-ttu-id="1ad3b-155">Replace `mykafka` with the name of your Kafka cluster</span><span class="sxs-lookup"><span data-stu-id="1ad3b-155">Replace `mykafka` with the name of your Kafka cluster</span></span>

    ```bash
    ssh sshuser@mykafka-ssh.azurehdinsight.net
    ```

2. <span data-ttu-id="1ad3b-156">When you first connect to the cluster, your SSH client may display a warning that the authenticity of the host can't be established.</span><span class="sxs-lookup"><span data-stu-id="1ad3b-156">When you first connect to the cluster, your SSH client may display a warning that the authenticity of the host can't be established.</span></span> <span data-ttu-id="1ad3b-157">When prompted type __yes__, and then press __Enter__ to add the host to your SSH client's trusted server list.</span><span class="sxs-lookup"><span data-stu-id="1ad3b-157">When prompted type __yes__, and then press __Enter__ to add the host to your SSH client's trusted server list.</span></span>

3. <span data-ttu-id="1ad3b-158">When prompted, enter the password for the SSH user.</span><span class="sxs-lookup"><span data-stu-id="1ad3b-158">When prompted, enter the password for the SSH user.</span></span>

<span data-ttu-id="1ad3b-159">Once connected, you see information similar to the following text:</span><span class="sxs-lookup"><span data-stu-id="1ad3b-159">Once connected, you see information similar to the following text:</span></span>

```text
Authorized uses only. All activity may be monitored and reported.
Welcome to Ubuntu 16.04.4 LTS (GNU/Linux 4.13.0-1011-azure x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

83 packages can be updated.
37 updates are security updates.



Welcome to Kafka on HDInsight.

Last login: Thu Mar 29 13:25:27 2018 from 108.252.109.241
ssuhuser@hn0-mykafk:~$
```

## <a id="getkafkainfo"></a><span data-ttu-id="1ad3b-160">Get the Zookeeper and Broker host information</span><span class="sxs-lookup"><span data-stu-id="1ad3b-160">Get the Zookeeper and Broker host information</span></span>

<span data-ttu-id="1ad3b-161">When working with Kafka, you must know the *Zookeeper* and *Broker* hosts.</span><span class="sxs-lookup"><span data-stu-id="1ad3b-161">When working with Kafka, you must know the *Zookeeper* and *Broker* hosts.</span></span> <span data-ttu-id="1ad3b-162">These hosts are used with the Kafka API and many of the utilities that ship with Kafka.</span><span class="sxs-lookup"><span data-stu-id="1ad3b-162">These hosts are used with the Kafka API and many of the utilities that ship with Kafka.</span></span>

<span data-ttu-id="1ad3b-163">In this section, you get the host information from the Ambari REST API on the cluster.</span><span class="sxs-lookup"><span data-stu-id="1ad3b-163">In this section, you get the host information from the Ambari REST API on the cluster.</span></span>

1. <span data-ttu-id="1ad3b-164">From the SSH connection to the cluster, use the following command to install the `jq` utility.</span><span class="sxs-lookup"><span data-stu-id="1ad3b-164">From the SSH connection to the cluster, use the following command to install the `jq` utility.</span></span> <span data-ttu-id="1ad3b-165">This utility is used to parse JSON documents, and is useful in retrieving the host information:</span><span class="sxs-lookup"><span data-stu-id="1ad3b-165">This utility is used to parse JSON documents, and is useful in retrieving the host information:</span></span>
   
    ```bash
    sudo apt -y install jq
    ```

2. <span data-ttu-id="1ad3b-166">To set an environment variable to the cluster name, use the following command:</span><span class="sxs-lookup"><span data-stu-id="1ad3b-166">To set an environment variable to the cluster name, use the following command:</span></span>

    ```bash
    read -p "Enter the Kafka on HDInsight cluster name: " CLUSTERNAME
    ```

    <span data-ttu-id="1ad3b-167">When prompted, enter the name of the Kafka cluster.</span><span class="sxs-lookup"><span data-stu-id="1ad3b-167">When prompted, enter the name of the Kafka cluster.</span></span>

3. <span data-ttu-id="1ad3b-168">To set an environment variable with Zookeeper host information, use the following command:</span><span class="sxs-lookup"><span data-stu-id="1ad3b-168">To set an environment variable with Zookeeper host information, use the following command:</span></span>

    ```bash
    export KAFKAZKHOSTS=`curl -sS -u admin -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`
    ```

    <span data-ttu-id="1ad3b-169">When prompted, enter the password for the cluster login account (not the SSH account).</span><span class="sxs-lookup"><span data-stu-id="1ad3b-169">When prompted, enter the password for the cluster login account (not the SSH account).</span></span>

    > [!NOTE]
    > <span data-ttu-id="1ad3b-170">This command retrieves all Zookeeper hosts, then returns only the first two entries.</span><span class="sxs-lookup"><span data-stu-id="1ad3b-170">This command retrieves all Zookeeper hosts, then returns only the first two entries.</span></span> <span data-ttu-id="1ad3b-171">This is because you want some redundancy in case one host is unreachable.</span><span class="sxs-lookup"><span data-stu-id="1ad3b-171">This is because you want some redundancy in case one host is unreachable.</span></span>

4. <span data-ttu-id="1ad3b-172">To verify that the environment variable is set correctly, use the following command:</span><span class="sxs-lookup"><span data-stu-id="1ad3b-172">To verify that the environment variable is set correctly, use the following command:</span></span>

    ```bash
     echo '$KAFKAZKHOSTS='$KAFKAZKHOSTS
    ```

    <span data-ttu-id="1ad3b-173">This command returns information similar to the following text:</span><span class="sxs-lookup"><span data-stu-id="1ad3b-173">This command returns information similar to the following text:</span></span>

    `zk0-kafka.eahjefxxp1netdbyklgqj5y1ud.ex.internal.cloudapp.net:2181,zk2-kafka.eahjefxxp1netdbyklgqj5y1ud.ex.internal.cloudapp.net:2181`

5. <span data-ttu-id="1ad3b-174">To set an environment variable with Kafka broker host information, use the following command:</span><span class="sxs-lookup"><span data-stu-id="1ad3b-174">To set an environment variable with Kafka broker host information, use the following command:</span></span>

    ```bash
    export KAFKABROKERS=`curl -sS -u admin -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`
    ```

    <span data-ttu-id="1ad3b-175">When prompted, enter the password for the cluster login account (not the SSH account).</span><span class="sxs-lookup"><span data-stu-id="1ad3b-175">When prompted, enter the password for the cluster login account (not the SSH account).</span></span>

6. <span data-ttu-id="1ad3b-176">To verify that the environment variable is set correctly, use the following command:</span><span class="sxs-lookup"><span data-stu-id="1ad3b-176">To verify that the environment variable is set correctly, use the following command:</span></span>

    ```bash   
    echo '$KAFKABROKERS='$KAFKABROKERS
    ```

    <span data-ttu-id="1ad3b-177">This command returns information similar to the following text:</span><span class="sxs-lookup"><span data-stu-id="1ad3b-177">This command returns information similar to the following text:</span></span>
   
    `wn1-kafka.eahjefxxp1netdbyklgqj5y1ud.cx.internal.cloudapp.net:9092,wn0-kafka.eahjefxxp1netdbyklgqj5y1ud.cx.internal.cloudapp.net:9092`

## <a name="manage-kafka-topics"></a><span data-ttu-id="1ad3b-178">Manage Kafka topics</span><span class="sxs-lookup"><span data-stu-id="1ad3b-178">Manage Kafka topics</span></span>

<span data-ttu-id="1ad3b-179">Kafka stores streams of data in *topics*.</span><span class="sxs-lookup"><span data-stu-id="1ad3b-179">Kafka stores streams of data in *topics*.</span></span> <span data-ttu-id="1ad3b-180">You can use the `kafka-topics.sh` utility to manage topics.</span><span class="sxs-lookup"><span data-stu-id="1ad3b-180">You can use the `kafka-topics.sh` utility to manage topics.</span></span>

* <span data-ttu-id="1ad3b-181">**To create a topic**, use the following command in the SSH connection:</span><span class="sxs-lookup"><span data-stu-id="1ad3b-181">**To create a topic**, use the following command in the SSH connection:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic test --zookeeper $KAFKAZKHOSTS
    ```

    <span data-ttu-id="1ad3b-182">This command connects to Zookeeper using the host information stored in `$KAFKAZKHOSTS`.</span><span class="sxs-lookup"><span data-stu-id="1ad3b-182">This command connects to Zookeeper using the host information stored in `$KAFKAZKHOSTS`.</span></span> <span data-ttu-id="1ad3b-183">It then creates a Kafka topic named **test**.</span><span class="sxs-lookup"><span data-stu-id="1ad3b-183">It then creates a Kafka topic named **test**.</span></span> 

    * <span data-ttu-id="1ad3b-184">Data stored in this topic is partitioned across eight partitions.</span><span class="sxs-lookup"><span data-stu-id="1ad3b-184">Data stored in this topic is partitioned across eight partitions.</span></span>

    * <span data-ttu-id="1ad3b-185">Each partition is replicated across three worker nodes in the cluster.</span><span class="sxs-lookup"><span data-stu-id="1ad3b-185">Each partition is replicated across three worker nodes in the cluster.</span></span>

        > [!IMPORTANT]
        > <span data-ttu-id="1ad3b-186">If you created the cluster in an Azure region that provides three fault domains, use a replication factor of 3.</span><span class="sxs-lookup"><span data-stu-id="1ad3b-186">If you created the cluster in an Azure region that provides three fault domains, use a replication factor of 3.</span></span> <span data-ttu-id="1ad3b-187">Otherwise, use a replication factor of 4.</span><span class="sxs-lookup"><span data-stu-id="1ad3b-187">Otherwise, use a replication factor of 4.</span></span>
        
        <span data-ttu-id="1ad3b-188">In regions with three fault domains, a replication factor of 3 allows replicas to be spread across the fault domains.</span><span class="sxs-lookup"><span data-stu-id="1ad3b-188">In regions with three fault domains, a replication factor of 3 allows replicas to be spread across the fault domains.</span></span> <span data-ttu-id="1ad3b-189">In regions with two fault domains, a replication factor of four spreads the replicas evenly across the domains.</span><span class="sxs-lookup"><span data-stu-id="1ad3b-189">In regions with two fault domains, a replication factor of four spreads the replicas evenly across the domains.</span></span>
        
        <span data-ttu-id="1ad3b-190">For information on the number of fault domains in a region, see the [Availability of Linux virtual machines](../../virtual-machines/windows/manage-availability.md#use-managed-disks-for-vms-in-an-availability-set) document.</span><span class="sxs-lookup"><span data-stu-id="1ad3b-190">For information on the number of fault domains in a region, see the [Availability of Linux virtual machines](../../virtual-machines/windows/manage-availability.md#use-managed-disks-for-vms-in-an-availability-set) document.</span></span>

        > [!IMPORTANT] 
        > <span data-ttu-id="1ad3b-191">Kafka is not aware of Azure fault domains.</span><span class="sxs-lookup"><span data-stu-id="1ad3b-191">Kafka is not aware of Azure fault domains.</span></span> <span data-ttu-id="1ad3b-192">When creating partition replicas for topics, it may not distribute replicas properly for high availability.</span><span class="sxs-lookup"><span data-stu-id="1ad3b-192">When creating partition replicas for topics, it may not distribute replicas properly for high availability.</span></span>

        <span data-ttu-id="1ad3b-193">To ensure high availability, use the [Kafka partition rebalance tool](https://github.com/hdinsight/hdinsight-kafka-tools).</span><span class="sxs-lookup"><span data-stu-id="1ad3b-193">To ensure high availability, use the [Kafka partition rebalance tool](https://github.com/hdinsight/hdinsight-kafka-tools).</span></span> <span data-ttu-id="1ad3b-194">This tool must be ran from an SSH connection to the head node of your Kafka cluster.</span><span class="sxs-lookup"><span data-stu-id="1ad3b-194">This tool must be ran from an SSH connection to the head node of your Kafka cluster.</span></span>

        <span data-ttu-id="1ad3b-195">For the highest availability of your Kafka data, you should rebalance the partition replicas for your topic when:</span><span class="sxs-lookup"><span data-stu-id="1ad3b-195">For the highest availability of your Kafka data, you should rebalance the partition replicas for your topic when:</span></span>

        * <span data-ttu-id="1ad3b-196">You create a new topic or partition</span><span class="sxs-lookup"><span data-stu-id="1ad3b-196">You create a new topic or partition</span></span>

        * <span data-ttu-id="1ad3b-197">You scale up a cluster</span><span class="sxs-lookup"><span data-stu-id="1ad3b-197">You scale up a cluster</span></span>

* <span data-ttu-id="1ad3b-198">**To list topics**, use the following command:</span><span class="sxs-lookup"><span data-stu-id="1ad3b-198">**To list topics**, use the following command:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $KAFKAZKHOSTS
    ```

    <span data-ttu-id="1ad3b-199">This command lists the topics available on the Kafka cluster.</span><span class="sxs-lookup"><span data-stu-id="1ad3b-199">This command lists the topics available on the Kafka cluster.</span></span>

* <span data-ttu-id="1ad3b-200">**To delete a topic**, use the following command:</span><span class="sxs-lookup"><span data-stu-id="1ad3b-200">**To delete a topic**, use the following command:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --delete --topic topicname --zookeeper $KAFKAZKHOSTS
    ```

    <span data-ttu-id="1ad3b-201">This command deletes the topic named `topicname`.</span><span class="sxs-lookup"><span data-stu-id="1ad3b-201">This command deletes the topic named `topicname`.</span></span>

    > [!WARNING]
    > <span data-ttu-id="1ad3b-202">If you delete the `test` topic created earlier, then you must recreate it.</span><span class="sxs-lookup"><span data-stu-id="1ad3b-202">If you delete the `test` topic created earlier, then you must recreate it.</span></span> <span data-ttu-id="1ad3b-203">It is used by steps later in this document.</span><span class="sxs-lookup"><span data-stu-id="1ad3b-203">It is used by steps later in this document.</span></span>

<span data-ttu-id="1ad3b-204">For more information on the commands available with the `kafka-topics.sh` utility, use the following command:</span><span class="sxs-lookup"><span data-stu-id="1ad3b-204">For more information on the commands available with the `kafka-topics.sh` utility, use the following command:</span></span>

```bash
/usr/hdp/current/kafka-broker/bin/kafka-topics.sh
```

## <a name="produce-and-consume-records"></a><span data-ttu-id="1ad3b-205">Produce and consume records</span><span class="sxs-lookup"><span data-stu-id="1ad3b-205">Produce and consume records</span></span>

<span data-ttu-id="1ad3b-206">Kafka stores *records* in topics.</span><span class="sxs-lookup"><span data-stu-id="1ad3b-206">Kafka stores *records* in topics.</span></span> <span data-ttu-id="1ad3b-207">Records are produced by *producers*, and consumed by *consumers*.</span><span class="sxs-lookup"><span data-stu-id="1ad3b-207">Records are produced by *producers*, and consumed by *consumers*.</span></span> <span data-ttu-id="1ad3b-208">Producers and consumers communicate with the *Kafka broker* service.</span><span class="sxs-lookup"><span data-stu-id="1ad3b-208">Producers and consumers communicate with the *Kafka broker* service.</span></span> <span data-ttu-id="1ad3b-209">Each worker node in your HDInsight cluster is a Kafka broker host.</span><span class="sxs-lookup"><span data-stu-id="1ad3b-209">Each worker node in your HDInsight cluster is a Kafka broker host.</span></span>

<span data-ttu-id="1ad3b-210">To store records into the test topic you created earlier, and then read them using a consumer, use the following steps:</span><span class="sxs-lookup"><span data-stu-id="1ad3b-210">To store records into the test topic you created earlier, and then read them using a consumer, use the following steps:</span></span>

1. <span data-ttu-id="1ad3b-211">To write records to the topic, use the `kafka-console-producer.sh` utility from the SSH connection:</span><span class="sxs-lookup"><span data-stu-id="1ad3b-211">To write records to the topic, use the `kafka-console-producer.sh` utility from the SSH connection:</span></span>
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-producer.sh --broker-list $KAFKABROKERS --topic test
    ```
   
    <span data-ttu-id="1ad3b-212">After this command, you arrive at an empty line.</span><span class="sxs-lookup"><span data-stu-id="1ad3b-212">After this command, you arrive at an empty line.</span></span>

2. <span data-ttu-id="1ad3b-213">Type a text message on the empty line and hit enter.</span><span class="sxs-lookup"><span data-stu-id="1ad3b-213">Type a text message on the empty line and hit enter.</span></span> <span data-ttu-id="1ad3b-214">Enter a few messages this way, and then use **Ctrl + C** to return to the normal prompt.</span><span class="sxs-lookup"><span data-stu-id="1ad3b-214">Enter a few messages this way, and then use **Ctrl + C** to return to the normal prompt.</span></span> <span data-ttu-id="1ad3b-215">Each line is sent as a separate record to the Kafka topic.</span><span class="sxs-lookup"><span data-stu-id="1ad3b-215">Each line is sent as a separate record to the Kafka topic.</span></span>

3. <span data-ttu-id="1ad3b-216">To read records from the topic, use the `kafka-console-consumer.sh` utility from the SSH connection:</span><span class="sxs-lookup"><span data-stu-id="1ad3b-216">To read records from the topic, use the `kafka-console-consumer.sh` utility from the SSH connection:</span></span>
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --bootstrap-server $KAFKABROKERS --topic test --from-beginning
    ```
   
    <span data-ttu-id="1ad3b-217">This command retrieves the records from the topic and displays them.</span><span class="sxs-lookup"><span data-stu-id="1ad3b-217">This command retrieves the records from the topic and displays them.</span></span> <span data-ttu-id="1ad3b-218">Using `--from-beginning` tells the consumer to start from the beginning of the stream, so all records are retrieved.</span><span class="sxs-lookup"><span data-stu-id="1ad3b-218">Using `--from-beginning` tells the consumer to start from the beginning of the stream, so all records are retrieved.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1ad3b-219">If you are using an older version of Kafka, replace `--bootstrap-server $KAFKABROKERS` with `--zookeeper $KAFKAZKHOSTS`.</span><span class="sxs-lookup"><span data-stu-id="1ad3b-219">If you are using an older version of Kafka, replace `--bootstrap-server $KAFKABROKERS` with `--zookeeper $KAFKAZKHOSTS`.</span></span>

4. <span data-ttu-id="1ad3b-220">Use __Ctrl + C__ to stop the consumer.</span><span class="sxs-lookup"><span data-stu-id="1ad3b-220">Use __Ctrl + C__ to stop the consumer.</span></span>

<span data-ttu-id="1ad3b-221">You can also programmatically create producers and consumers.</span><span class="sxs-lookup"><span data-stu-id="1ad3b-221">You can also programmatically create producers and consumers.</span></span> <span data-ttu-id="1ad3b-222">For an example of using this API, see the [Kafka Producer and Consumer API with HDInsight](apache-kafka-producer-consumer-api.md) document.</span><span class="sxs-lookup"><span data-stu-id="1ad3b-222">For an example of using this API, see the [Kafka Producer and Consumer API with HDInsight](apache-kafka-producer-consumer-api.md) document.</span></span>

## <a name="troubleshoot"></a><span data-ttu-id="1ad3b-223">Troubleshoot</span><span class="sxs-lookup"><span data-stu-id="1ad3b-223">Troubleshoot</span></span>

<span data-ttu-id="1ad3b-224">If you run into issues with creating HDInsight clusters, see [access control requirements](../hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="1ad3b-224">If you run into issues with creating HDInsight clusters, see [access control requirements](../hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="1ad3b-225">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="1ad3b-225">Clean up resources</span></span>

<span data-ttu-id="1ad3b-226">If you wish to clean up the resources created by this quickstart, you can delete the resource group.</span><span class="sxs-lookup"><span data-stu-id="1ad3b-226">If you wish to clean up the resources created by this quickstart, you can delete the resource group.</span></span> <span data-ttu-id="1ad3b-227">Deleting the resource group also deletes the associated HDInsight cluster, and any other resources associated with the resource group.</span><span class="sxs-lookup"><span data-stu-id="1ad3b-227">Deleting the resource group also deletes the associated HDInsight cluster, and any other resources associated with the resource group.</span></span>

<span data-ttu-id="1ad3b-228">To remove the resource group using the Azure portal:</span><span class="sxs-lookup"><span data-stu-id="1ad3b-228">To remove the resource group using the Azure portal:</span></span>

1. <span data-ttu-id="1ad3b-229">In the Azure portal, expand the menu on the left side to open the menu of services, and then choose __Resource Groups__ to display the list of your resource groups.</span><span class="sxs-lookup"><span data-stu-id="1ad3b-229">In the Azure portal, expand the menu on the left side to open the menu of services, and then choose __Resource Groups__ to display the list of your resource groups.</span></span>
2. <span data-ttu-id="1ad3b-230">Locate the resource group to delete, and then right-click the __More__ button (...) on the right side of the listing.</span><span class="sxs-lookup"><span data-stu-id="1ad3b-230">Locate the resource group to delete, and then right-click the __More__ button (...) on the right side of the listing.</span></span>
3. <span data-ttu-id="1ad3b-231">Select __Delete resource group__, and then confirm.</span><span class="sxs-lookup"><span data-stu-id="1ad3b-231">Select __Delete resource group__, and then confirm.</span></span>

> [!WARNING]
> <span data-ttu-id="1ad3b-232">HDInsight cluster billing starts once a cluster is created and stops when the cluster is deleted.</span><span class="sxs-lookup"><span data-stu-id="1ad3b-232">HDInsight cluster billing starts once a cluster is created and stops when the cluster is deleted.</span></span> <span data-ttu-id="1ad3b-233">Billing is pro-rated per minute, so you should always delete your cluster when it is no longer in use.</span><span class="sxs-lookup"><span data-stu-id="1ad3b-233">Billing is pro-rated per minute, so you should always delete your cluster when it is no longer in use.</span></span>
> 
> <span data-ttu-id="1ad3b-234">Deleting a Kafka on HDInsight cluster deletes any data stored in Kafka.</span><span class="sxs-lookup"><span data-stu-id="1ad3b-234">Deleting a Kafka on HDInsight cluster deletes any data stored in Kafka.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1ad3b-235">Next steps</span><span class="sxs-lookup"><span data-stu-id="1ad3b-235">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1ad3b-236">Use Apache Spark with Kafka</span><span class="sxs-lookup"><span data-stu-id="1ad3b-236">Use Apache Spark with Kafka</span></span>](../hdinsight-apache-kafka-spark-structured-streaming.md)

