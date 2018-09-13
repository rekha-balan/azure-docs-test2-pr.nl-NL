---
title: High availability features of HDInsight (Hadoop) | Microsoft Docs
description: Learn how Linux-based HDInsight clusters improve reliability and availability by using an additional head node. Learn how this impacts Hadoop services such as Ambari and Hive, as well as how to individually connect to each head node using SSH.
services: hdinsight
editor: cgronlun
manager: jhubbard
author: Blackmist
documentationcenter: ''
tags: azure-portal
ms.assetid: 99c9f59c-cf6b-4529-99d1-bf060435e8d4
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 04/03/2017
ms.author: larryfr
ms.openlocfilehash: 58a92b434b09475ff0f1ec32a3cbdbdc221c38c3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551332"
---
# <a name="availability-and-reliability-of-hadoop-clusters-in-hdinsight"></a><span data-ttu-id="a73e6-104">Availability and reliability of Hadoop clusters in HDInsight</span><span class="sxs-lookup"><span data-stu-id="a73e6-104">Availability and reliability of Hadoop clusters in HDInsight</span></span>

<span data-ttu-id="a73e6-105">HDInsight clusters provide two head nodes to increase the availability and reliability of Hadoop services and jobs running.</span><span class="sxs-lookup"><span data-stu-id="a73e6-105">HDInsight clusters provide two head nodes to increase the availability and reliability of Hadoop services and jobs running.</span></span>

<span data-ttu-id="a73e6-106">Hadoop achieves high availability and reliability by keeping copies of services and data on multiple nodes in a cluster.</span><span class="sxs-lookup"><span data-stu-id="a73e6-106">Hadoop achieves high availability and reliability by keeping copies of services and data on multiple nodes in a cluster.</span></span> <span data-ttu-id="a73e6-107">However standard distributions of Hadoop typically have only a single head node.</span><span class="sxs-lookup"><span data-stu-id="a73e6-107">However standard distributions of Hadoop typically have only a single head node.</span></span> <span data-ttu-id="a73e6-108">Any outage of the single head node can cause the cluster to stop working.</span><span class="sxs-lookup"><span data-stu-id="a73e6-108">Any outage of the single head node can cause the cluster to stop working.</span></span> <span data-ttu-id="a73e6-109">This is not a problem with HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a73e6-109">This is not a problem with HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a73e6-110">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="a73e6-110">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="a73e6-111">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span><span class="sxs-lookup"><span data-stu-id="a73e6-111">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span></span>

## <a name="understanding-the-nodes"></a><span data-ttu-id="a73e6-112">Understanding the nodes</span><span class="sxs-lookup"><span data-stu-id="a73e6-112">Understanding the nodes</span></span>

<span data-ttu-id="a73e6-113">Nodes in an HDInsight cluster are implemented using Azure Virtual Machines.</span><span class="sxs-lookup"><span data-stu-id="a73e6-113">Nodes in an HDInsight cluster are implemented using Azure Virtual Machines.</span></span> <span data-ttu-id="a73e6-114">If a node fails, it is taken offline and a new node is created to replace the failed node.</span><span class="sxs-lookup"><span data-stu-id="a73e6-114">If a node fails, it is taken offline and a new node is created to replace the failed node.</span></span> <span data-ttu-id="a73e6-115">While the node is offline, another node of the same type is used until the new node is brought online.</span><span class="sxs-lookup"><span data-stu-id="a73e6-115">While the node is offline, another node of the same type is used until the new node is brought online.</span></span>

> [!NOTE]
> <span data-ttu-id="a73e6-116">If the node is analyzing data when it fails, its progress on the job is lost.</span><span class="sxs-lookup"><span data-stu-id="a73e6-116">If the node is analyzing data when it fails, its progress on the job is lost.</span></span> <span data-ttu-id="a73e6-117">The job is resubmitted to another node.</span><span class="sxs-lookup"><span data-stu-id="a73e6-117">The job is resubmitted to another node.</span></span>

<span data-ttu-id="a73e6-118">The following sections discuss the individual node types used with HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a73e6-118">The following sections discuss the individual node types used with HDInsight.</span></span> <span data-ttu-id="a73e6-119">Not all node types are used for a cluster type.</span><span class="sxs-lookup"><span data-stu-id="a73e6-119">Not all node types are used for a cluster type.</span></span> <span data-ttu-id="a73e6-120">For example, a Hadoop cluster type does not have any Nimbus nodes.</span><span class="sxs-lookup"><span data-stu-id="a73e6-120">For example, a Hadoop cluster type does not have any Nimbus nodes.</span></span> <span data-ttu-id="a73e6-121">For more information on nodes used by HDInsight cluster types, see the Cluster types section of the [Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types) document.</span><span class="sxs-lookup"><span data-stu-id="a73e6-121">For more information on nodes used by HDInsight cluster types, see the Cluster types section of the [Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types) document.</span></span>

### <a name="head-nodes"></a><span data-ttu-id="a73e6-122">Head nodes</span><span class="sxs-lookup"><span data-stu-id="a73e6-122">Head nodes</span></span>

<span data-ttu-id="a73e6-123">Both head nodes are active and running within the HDInsight cluster simultaneously.</span><span class="sxs-lookup"><span data-stu-id="a73e6-123">Both head nodes are active and running within the HDInsight cluster simultaneously.</span></span> <span data-ttu-id="a73e6-124">Some services, such as HDFS or YARN, are only 'active' on one head node at any given time.</span><span class="sxs-lookup"><span data-stu-id="a73e6-124">Some services, such as HDFS or YARN, are only 'active' on one head node at any given time.</span></span> <span data-ttu-id="a73e6-125">Other services such as HiveServer2 or Hive MetaStore are active on both head nodes at the same time.</span><span class="sxs-lookup"><span data-stu-id="a73e6-125">Other services such as HiveServer2 or Hive MetaStore are active on both head nodes at the same time.</span></span>

<span data-ttu-id="a73e6-126">Head nodes (and other nodes in HDInsight) have a numeric value as part of the hostname of the node.</span><span class="sxs-lookup"><span data-stu-id="a73e6-126">Head nodes (and other nodes in HDInsight) have a numeric value as part of the hostname of the node.</span></span> <span data-ttu-id="a73e6-127">For example, `hn0-CLUSTERNAME` or `hn4-CLUSTERNAME`.</span><span class="sxs-lookup"><span data-stu-id="a73e6-127">For example, `hn0-CLUSTERNAME` or `hn4-CLUSTERNAME`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a73e6-128">Do not associate the numeric value with whether a node is primary or secondary.</span><span class="sxs-lookup"><span data-stu-id="a73e6-128">Do not associate the numeric value with whether a node is primary or secondary.</span></span> <span data-ttu-id="a73e6-129">The numeric value is only present to provide a unique name for each node.</span><span class="sxs-lookup"><span data-stu-id="a73e6-129">The numeric value is only present to provide a unique name for each node.</span></span>

### <a name="nimbus-nodes"></a><span data-ttu-id="a73e6-130">Nimbus Nodes</span><span class="sxs-lookup"><span data-stu-id="a73e6-130">Nimbus Nodes</span></span>

<span data-ttu-id="a73e6-131">For Storm clusters, the Nimbus nodes provide similar functionality to the Hadoop JobTracker by distributing and monitoring processing across worker nodes.</span><span class="sxs-lookup"><span data-stu-id="a73e6-131">For Storm clusters, the Nimbus nodes provide similar functionality to the Hadoop JobTracker by distributing and monitoring processing across worker nodes.</span></span> <span data-ttu-id="a73e6-132">HDInsight provides 2 Nimbus nodes for the Storm cluster type.</span><span class="sxs-lookup"><span data-stu-id="a73e6-132">HDInsight provides 2 Nimbus nodes for the Storm cluster type.</span></span>

### <a name="zookeeper-nodes"></a><span data-ttu-id="a73e6-133">Zookeeper nodes</span><span class="sxs-lookup"><span data-stu-id="a73e6-133">Zookeeper nodes</span></span>

<span data-ttu-id="a73e6-134">[ZooKeeper](http://zookeeper.apache.org/) nodes are used for leader election of master services on head nodes, and to insure that services, data (worker) nodes, and gateways know which head node a master service is active on.</span><span class="sxs-lookup"><span data-stu-id="a73e6-134">[ZooKeeper](http://zookeeper.apache.org/) nodes are used for leader election of master services on head nodes, and to insure that services, data (worker) nodes, and gateways know which head node a master service is active on.</span></span> <span data-ttu-id="a73e6-135">By default, HDInsight provides three ZooKeeper nodes.</span><span class="sxs-lookup"><span data-stu-id="a73e6-135">By default, HDInsight provides three ZooKeeper nodes.</span></span>

### <a name="worker-nodes"></a><span data-ttu-id="a73e6-136">Worker nodes</span><span class="sxs-lookup"><span data-stu-id="a73e6-136">Worker nodes</span></span>

<span data-ttu-id="a73e6-137">Worker nodes perform the actual data analysis when a job is submitted to the cluster.</span><span class="sxs-lookup"><span data-stu-id="a73e6-137">Worker nodes perform the actual data analysis when a job is submitted to the cluster.</span></span> <span data-ttu-id="a73e6-138">If a worker node fails, the task that it was performing is submitted to another worker node.</span><span class="sxs-lookup"><span data-stu-id="a73e6-138">If a worker node fails, the task that it was performing is submitted to another worker node.</span></span> <span data-ttu-id="a73e6-139">By default, HDInsight creates four worker nodes.</span><span class="sxs-lookup"><span data-stu-id="a73e6-139">By default, HDInsight creates four worker nodes.</span></span> <span data-ttu-id="a73e6-140">You can change this number to suit your needs both during and after cluster creation.</span><span class="sxs-lookup"><span data-stu-id="a73e6-140">You can change this number to suit your needs both during and after cluster creation.</span></span>

### <a name="edge-node"></a><span data-ttu-id="a73e6-141">Edge node</span><span class="sxs-lookup"><span data-stu-id="a73e6-141">Edge node</span></span>

<span data-ttu-id="a73e6-142">An edge node does not actively participate in data analysis within the cluster, but is instead used by developers or data scientists when working with Hadoop.</span><span class="sxs-lookup"><span data-stu-id="a73e6-142">An edge node does not actively participate in data analysis within the cluster, but is instead used by developers or data scientists when working with Hadoop.</span></span> <span data-ttu-id="a73e6-143">The edge node lives in the same Azure Virtual Network as the other nodes in the cluster, and can directly access all other nodes.</span><span class="sxs-lookup"><span data-stu-id="a73e6-143">The edge node lives in the same Azure Virtual Network as the other nodes in the cluster, and can directly access all other nodes.</span></span> <span data-ttu-id="a73e6-144">Since it is not involved in analyzing data for the cluster, it can be used without any concern of taking resources away from critical Hadoop services or analysis jobs.</span><span class="sxs-lookup"><span data-stu-id="a73e6-144">Since it is not involved in analyzing data for the cluster, it can be used without any concern of taking resources away from critical Hadoop services or analysis jobs.</span></span>

<span data-ttu-id="a73e6-145">Currently, R Server on HDInsight is the only cluster type that provides an edge node by default.</span><span class="sxs-lookup"><span data-stu-id="a73e6-145">Currently, R Server on HDInsight is the only cluster type that provides an edge node by default.</span></span> <span data-ttu-id="a73e6-146">For R Server on HDInsight, the edge node is used test R code locally on the node before submitting it to the cluster for distributed processing.</span><span class="sxs-lookup"><span data-stu-id="a73e6-146">For R Server on HDInsight, the edge node is used test R code locally on the node before submitting it to the cluster for distributed processing.</span></span>

<span data-ttu-id="a73e6-147">For information on using an edge node with cluster types other than R Server, see the [Use edge nodes in HDInsight](hdinsight-apps-use-edge-node.md) document.</span><span class="sxs-lookup"><span data-stu-id="a73e6-147">For information on using an edge node with cluster types other than R Server, see the [Use edge nodes in HDInsight](hdinsight-apps-use-edge-node.md) document.</span></span>

## <a name="accessing-the-nodes"></a><span data-ttu-id="a73e6-148">Accessing the nodes</span><span class="sxs-lookup"><span data-stu-id="a73e6-148">Accessing the nodes</span></span>

<span data-ttu-id="a73e6-149">Access to the cluster over the internet is provided through a public gateway.</span><span class="sxs-lookup"><span data-stu-id="a73e6-149">Access to the cluster over the internet is provided through a public gateway.</span></span> <span data-ttu-id="a73e6-150">Access is limited to connecting to the head nodes and (if one exists) the edge node.</span><span class="sxs-lookup"><span data-stu-id="a73e6-150">Access is limited to connecting to the head nodes and (if one exists) the edge node.</span></span> <span data-ttu-id="a73e6-151">Access to services running on the head nodes is not effected by having multiple head nodes.</span><span class="sxs-lookup"><span data-stu-id="a73e6-151">Access to services running on the head nodes is not effected by having multiple head nodes.</span></span> <span data-ttu-id="a73e6-152">The public gateway routes requests to the head node that hosts the requested service.</span><span class="sxs-lookup"><span data-stu-id="a73e6-152">The public gateway routes requests to the head node that hosts the requested service.</span></span> <span data-ttu-id="a73e6-153">For example, if Ambari is currently hosted on the secondary head node, the gateway routes incoming requests for Ambari to that node.</span><span class="sxs-lookup"><span data-stu-id="a73e6-153">For example, if Ambari is currently hosted on the secondary head node, the gateway routes incoming requests for Ambari to that node.</span></span>

<span data-ttu-id="a73e6-154">Access over the public gateway is limited to port 443 (HTTPS), 22, and 23.</span><span class="sxs-lookup"><span data-stu-id="a73e6-154">Access over the public gateway is limited to port 443 (HTTPS), 22, and 23.</span></span>

* <span data-ttu-id="a73e6-155">Port __443__ is used to access Ambari and other web UI or REST APIs hosted on the head nodes.</span><span class="sxs-lookup"><span data-stu-id="a73e6-155">Port __443__ is used to access Ambari and other web UI or REST APIs hosted on the head nodes.</span></span>

* <span data-ttu-id="a73e6-156">Port __22__ is used to access the primary head node or edge node with SSH.</span><span class="sxs-lookup"><span data-stu-id="a73e6-156">Port __22__ is used to access the primary head node or edge node with SSH.</span></span>

* <span data-ttu-id="a73e6-157">Port __23__ is used to access the secondary head node with SSH.</span><span class="sxs-lookup"><span data-stu-id="a73e6-157">Port __23__ is used to access the secondary head node with SSH.</span></span> <span data-ttu-id="a73e6-158">For example, `ssh username@mycluster-ssh.azurehdinsight.net` connects to the primary head node of the cluster named **mycluster**.</span><span class="sxs-lookup"><span data-stu-id="a73e6-158">For example, `ssh username@mycluster-ssh.azurehdinsight.net` connects to the primary head node of the cluster named **mycluster**.</span></span>

<span data-ttu-id="a73e6-159">For more information on using SSH, see the [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span><span class="sxs-lookup"><span data-stu-id="a73e6-159">For more information on using SSH, see the [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

### <a name="internal-fully-qualified-domain-names-fqdn"></a><span data-ttu-id="a73e6-160">Internal fully qualified domain names (FQDN)</span><span class="sxs-lookup"><span data-stu-id="a73e6-160">Internal fully qualified domain names (FQDN)</span></span>

<span data-ttu-id="a73e6-161">Nodes in an HDInsight cluster have an internal IP address and FQDN that can only be accessed from the cluster.</span><span class="sxs-lookup"><span data-stu-id="a73e6-161">Nodes in an HDInsight cluster have an internal IP address and FQDN that can only be accessed from the cluster.</span></span> <span data-ttu-id="a73e6-162">When accessing services on the cluster using the internal FQDN or IP address, you should use Ambari to verify the IP or FQDN to use when accessing the service.</span><span class="sxs-lookup"><span data-stu-id="a73e6-162">When accessing services on the cluster using the internal FQDN or IP address, you should use Ambari to verify the IP or FQDN to use when accessing the service.</span></span>

<span data-ttu-id="a73e6-163">For example, the Oozie service can only run on one head node, and using the `oozie` command from an SSH session requires the URL to the service.</span><span class="sxs-lookup"><span data-stu-id="a73e6-163">For example, the Oozie service can only run on one head node, and using the `oozie` command from an SSH session requires the URL to the service.</span></span> <span data-ttu-id="a73e6-164">This URL can be retrieved from Ambari by using the following command:</span><span class="sxs-lookup"><span data-stu-id="a73e6-164">This URL can be retrieved from Ambari by using the following command:</span></span>

    curl -u admin:PASSWORD "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations?type=oozie-site&tag=TOPOLOGY_RESOLVED" | grep oozie.base.url

<span data-ttu-id="a73e6-165">This command returns a value similar to the following command, which contains the internal URL to use with the `oozie` command:</span><span class="sxs-lookup"><span data-stu-id="a73e6-165">This command returns a value similar to the following command, which contains the internal URL to use with the `oozie` command:</span></span>

    "oozie.base.url": "http://hn0-CLUSTERNAME-randomcharacters.cx.internal.cloudapp.net:11000/oozie"

<span data-ttu-id="a73e6-166">For more information on working with the Ambari REST API, see [Monitor and Manage HDInsight using the Ambari REST API](hdinsight-hadoop-manage-ambari-rest-api.md).</span><span class="sxs-lookup"><span data-stu-id="a73e6-166">For more information on working with the Ambari REST API, see [Monitor and Manage HDInsight using the Ambari REST API](hdinsight-hadoop-manage-ambari-rest-api.md).</span></span>

### <a name="accessing-other-node-types"></a><span data-ttu-id="a73e6-167">Accessing other node types</span><span class="sxs-lookup"><span data-stu-id="a73e6-167">Accessing other node types</span></span>

<span data-ttu-id="a73e6-168">You can connect to nodes that are not directly accessible over the internet by using the following methods:</span><span class="sxs-lookup"><span data-stu-id="a73e6-168">You can connect to nodes that are not directly accessible over the internet by using the following methods:</span></span>

* <span data-ttu-id="a73e6-169">**SSH**: Once connected to a head node using SSH, you can then use SSH from the head node to connect to other nodes in the cluster.</span><span class="sxs-lookup"><span data-stu-id="a73e6-169">**SSH**: Once connected to a head node using SSH, you can then use SSH from the head node to connect to other nodes in the cluster.</span></span> <span data-ttu-id="a73e6-170">For more information, see the [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span><span class="sxs-lookup"><span data-stu-id="a73e6-170">For more information, see the [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

* <span data-ttu-id="a73e6-171">**SSH Tunnel**: If you need to access a web service hosted on one of the nodes that is not exposed to the internet, you must use an SSH tunne.</span><span class="sxs-lookup"><span data-stu-id="a73e6-171">**SSH Tunnel**: If you need to access a web service hosted on one of the nodes that is not exposed to the internet, you must use an SSH tunne.</span></span> <span data-ttu-id="a73e6-172">For more information, see the [Use an SSH tunnel with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span><span class="sxs-lookup"><span data-stu-id="a73e6-172">For more information, see the [Use an SSH tunnel with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

* <span data-ttu-id="a73e6-173">**Azure Virtual Network**: If your HDInsight cluster is part of an Azure Virtual Network, any resource on the same Virtual Network can directly access all nodes in the cluster.</span><span class="sxs-lookup"><span data-stu-id="a73e6-173">**Azure Virtual Network**: If your HDInsight cluster is part of an Azure Virtual Network, any resource on the same Virtual Network can directly access all nodes in the cluster.</span></span> <span data-ttu-id="a73e6-174">For more information, see the [Extend HDInsight using Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md) document.</span><span class="sxs-lookup"><span data-stu-id="a73e6-174">For more information, see the [Extend HDInsight using Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md) document.</span></span>

## <a name="how-to-check-on-a-service-status"></a><span data-ttu-id="a73e6-175">How to check on a service status</span><span class="sxs-lookup"><span data-stu-id="a73e6-175">How to check on a service status</span></span>

<span data-ttu-id="a73e6-176">To check the status of services that run on the head nodes, use the Ambari Web UI or the Ambari REST API.</span><span class="sxs-lookup"><span data-stu-id="a73e6-176">To check the status of services that run on the head nodes, use the Ambari Web UI or the Ambari REST API.</span></span>

### <a name="ambari-web-ui"></a><span data-ttu-id="a73e6-177">Ambari Web UI</span><span class="sxs-lookup"><span data-stu-id="a73e6-177">Ambari Web UI</span></span>

<span data-ttu-id="a73e6-178">The Ambari Web UI is viewable at https://CLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="a73e6-178">The Ambari Web UI is viewable at https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="a73e6-179">Replace **CLUSTERNAME** with the name of your cluster.</span><span class="sxs-lookup"><span data-stu-id="a73e6-179">Replace **CLUSTERNAME** with the name of your cluster.</span></span> <span data-ttu-id="a73e6-180">If prompted, enter the HTTP user credentials for your cluster.</span><span class="sxs-lookup"><span data-stu-id="a73e6-180">If prompted, enter the HTTP user credentials for your cluster.</span></span> <span data-ttu-id="a73e6-181">The default HTTP user name is **admin** and the password is the password you entered when creating the cluster.</span><span class="sxs-lookup"><span data-stu-id="a73e6-181">The default HTTP user name is **admin** and the password is the password you entered when creating the cluster.</span></span>

<span data-ttu-id="a73e6-182">When you arrive on the Ambari page, the installed services are listed on the left of the page.</span><span class="sxs-lookup"><span data-stu-id="a73e6-182">When you arrive on the Ambari page, the installed services are listed on the left of the page.</span></span>

![Installed services](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-high-availability-linux/services.png)

<span data-ttu-id="a73e6-184">There are a series of icons that may appear next to a service to indicate status.</span><span class="sxs-lookup"><span data-stu-id="a73e6-184">There are a series of icons that may appear next to a service to indicate status.</span></span> <span data-ttu-id="a73e6-185">Any alerts related to a service can be viewed using the **Alerts** link at the top of the page.</span><span class="sxs-lookup"><span data-stu-id="a73e6-185">Any alerts related to a service can be viewed using the **Alerts** link at the top of the page.</span></span> <span data-ttu-id="a73e6-186">You can select each service to view more information on it.</span><span class="sxs-lookup"><span data-stu-id="a73e6-186">You can select each service to view more information on it.</span></span>

<span data-ttu-id="a73e6-187">While the service page provides information on the status and configuration of each service, it does not provide information on which head node the service is running on.</span><span class="sxs-lookup"><span data-stu-id="a73e6-187">While the service page provides information on the status and configuration of each service, it does not provide information on which head node the service is running on.</span></span> <span data-ttu-id="a73e6-188">To view this information, use the **Hosts** link at the top of the page.</span><span class="sxs-lookup"><span data-stu-id="a73e6-188">To view this information, use the **Hosts** link at the top of the page.</span></span> <span data-ttu-id="a73e6-189">This page displays hosts within the cluster, including the head nodes.</span><span class="sxs-lookup"><span data-stu-id="a73e6-189">This page displays hosts within the cluster, including the head nodes.</span></span>

![hosts list](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-high-availability-linux/hosts.png)

<span data-ttu-id="a73e6-191">Selecting the link for one of the head nodes displays the services and components running on that node.</span><span class="sxs-lookup"><span data-stu-id="a73e6-191">Selecting the link for one of the head nodes displays the services and components running on that node.</span></span>

![Component status](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-high-availability-linux/nodeservices.png)

<span data-ttu-id="a73e6-193">For more information on using Ambari, see [Monitor and manage HDInsight using the Ambari Web UI](hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="a73e6-193">For more information on using Ambari, see [Monitor and manage HDInsight using the Ambari Web UI](hdinsight-hadoop-manage-ambari.md).</span></span>

### <a name="ambari-rest-api"></a><span data-ttu-id="a73e6-194">Ambari REST API</span><span class="sxs-lookup"><span data-stu-id="a73e6-194">Ambari REST API</span></span>

<span data-ttu-id="a73e6-195">The Ambari REST API is available over the internet, and the public gateway handles routing requests to the head node that is currently hosting the REST API.</span><span class="sxs-lookup"><span data-stu-id="a73e6-195">The Ambari REST API is available over the internet, and the public gateway handles routing requests to the head node that is currently hosting the REST API.</span></span>

<span data-ttu-id="a73e6-196">You can use the following command to check the state of a service through the Ambari REST API:</span><span class="sxs-lookup"><span data-stu-id="a73e6-196">You can use the following command to check the state of a service through the Ambari REST API:</span></span>

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICENAME?fields=ServiceInfo/state

* <span data-ttu-id="a73e6-197">Replace **PASSWORD** with the HTTP user (admin) account password</span><span class="sxs-lookup"><span data-stu-id="a73e6-197">Replace **PASSWORD** with the HTTP user (admin) account password</span></span>
* <span data-ttu-id="a73e6-198">Replace **CLUSTERNAME** with the name of the cluster</span><span class="sxs-lookup"><span data-stu-id="a73e6-198">Replace **CLUSTERNAME** with the name of the cluster</span></span>
* <span data-ttu-id="a73e6-199">Replace **SERVICENAME** with the name of the service to check the status of</span><span class="sxs-lookup"><span data-stu-id="a73e6-199">Replace **SERVICENAME** with the name of the service to check the status of</span></span>

<span data-ttu-id="a73e6-200">For example, to check the status of the **HDFS** service on a cluster named **mycluster**, with a password of **password**, you would use the following command:</span><span class="sxs-lookup"><span data-stu-id="a73e6-200">For example, to check the status of the **HDFS** service on a cluster named **mycluster**, with a password of **password**, you would use the following command:</span></span>

    curl -u admin:password https://mycluster.azurehdinsight.net/api/v1/clusters/mycluster/services/HDFS?fields=ServiceInfo/state

<span data-ttu-id="a73e6-201">The response is similar to the following JSON:</span><span class="sxs-lookup"><span data-stu-id="a73e6-201">The response is similar to the following JSON:</span></span>

    {
      "href" : "http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8080/api/v1/clusters/mycluster/services/HDFS?fields=ServiceInfo/state",
      "ServiceInfo" : {
        "cluster_name" : "mycluster",
        "service_name" : "HDFS",
        "state" : "STARTED"
      }
    }

<span data-ttu-id="a73e6-202">The URL tells us that the service is currently running on a head node named **hn0-CLUSTERNAME**.</span><span class="sxs-lookup"><span data-stu-id="a73e6-202">The URL tells us that the service is currently running on a head node named **hn0-CLUSTERNAME**.</span></span>

<span data-ttu-id="a73e6-203">The state tells us that the service is currently running, or **STARTED**.</span><span class="sxs-lookup"><span data-stu-id="a73e6-203">The state tells us that the service is currently running, or **STARTED**.</span></span>

<span data-ttu-id="a73e6-204">If you do not know what services are installed on the cluster, you can use the following command to retrieve a list:</span><span class="sxs-lookup"><span data-stu-id="a73e6-204">If you do not know what services are installed on the cluster, you can use the following command to retrieve a list:</span></span>

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services

<span data-ttu-id="a73e6-205">For more information on working with the Ambari REST API, see [Monitor and Manage HDInsight using the Ambari REST API](hdinsight-hadoop-manage-ambari-rest-api.md).</span><span class="sxs-lookup"><span data-stu-id="a73e6-205">For more information on working with the Ambari REST API, see [Monitor and Manage HDInsight using the Ambari REST API](hdinsight-hadoop-manage-ambari-rest-api.md).</span></span>

#### <a name="service-components"></a><span data-ttu-id="a73e6-206">Service components</span><span class="sxs-lookup"><span data-stu-id="a73e6-206">Service components</span></span>

<span data-ttu-id="a73e6-207">Services may contain components that you wish to check the status of individually.</span><span class="sxs-lookup"><span data-stu-id="a73e6-207">Services may contain components that you wish to check the status of individually.</span></span> <span data-ttu-id="a73e6-208">For example, HDFS contains the NameNode component.</span><span class="sxs-lookup"><span data-stu-id="a73e6-208">For example, HDFS contains the NameNode component.</span></span> <span data-ttu-id="a73e6-209">To view information on a component, the command would be:</span><span class="sxs-lookup"><span data-stu-id="a73e6-209">To view information on a component, the command would be:</span></span>

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICE/components/component

<span data-ttu-id="a73e6-210">If you do not know what components are provided by a service, you can use the following command to retrieve a list:</span><span class="sxs-lookup"><span data-stu-id="a73e6-210">If you do not know what components are provided by a service, you can use the following command to retrieve a list:</span></span>

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICE/components/component

## <a name="how-to-access-log-files-on-the-head-nodes"></a><span data-ttu-id="a73e6-211">How to access log files on the head nodes</span><span class="sxs-lookup"><span data-stu-id="a73e6-211">How to access log files on the head nodes</span></span>

### <a name="ssh"></a><span data-ttu-id="a73e6-212">SSH</span><span class="sxs-lookup"><span data-stu-id="a73e6-212">SSH</span></span>

<span data-ttu-id="a73e6-213">While connected to a head node through SSH, log files can be found under **/var/log**.</span><span class="sxs-lookup"><span data-stu-id="a73e6-213">While connected to a head node through SSH, log files can be found under **/var/log**.</span></span> <span data-ttu-id="a73e6-214">For example, **/var/log/hadoop-yarn/yarn** contain logs for YARN.</span><span class="sxs-lookup"><span data-stu-id="a73e6-214">For example, **/var/log/hadoop-yarn/yarn** contain logs for YARN.</span></span>

<span data-ttu-id="a73e6-215">Each head node can have unique log entries, so you should check the logs on both.</span><span class="sxs-lookup"><span data-stu-id="a73e6-215">Each head node can have unique log entries, so you should check the logs on both.</span></span>

### <a name="sftp"></a><span data-ttu-id="a73e6-216">SFTP</span><span class="sxs-lookup"><span data-stu-id="a73e6-216">SFTP</span></span>

<span data-ttu-id="a73e6-217">You can also connect to the head node using the SSH File Transfer Protocol or Secure File Transfer Protocol (SFTP), and download the log files directly.</span><span class="sxs-lookup"><span data-stu-id="a73e6-217">You can also connect to the head node using the SSH File Transfer Protocol or Secure File Transfer Protocol (SFTP), and download the log files directly.</span></span>

<span data-ttu-id="a73e6-218">Similar to using an SSH client, when connecting to the cluster you must provide the SSH user account name and the SSH address of the cluster.</span><span class="sxs-lookup"><span data-stu-id="a73e6-218">Similar to using an SSH client, when connecting to the cluster you must provide the SSH user account name and the SSH address of the cluster.</span></span> <span data-ttu-id="a73e6-219">For example, `sftp username@mycluster-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="a73e6-219">For example, `sftp username@mycluster-ssh.azurehdinsight.net`.</span></span> <span data-ttu-id="a73e6-220">You must provide the password for the account when prompted, or provide a public key using the `-i` parameter.</span><span class="sxs-lookup"><span data-stu-id="a73e6-220">You must provide the password for the account when prompted, or provide a public key using the `-i` parameter.</span></span>

<span data-ttu-id="a73e6-221">Once connected, you are presented with a `sftp>` prompt.</span><span class="sxs-lookup"><span data-stu-id="a73e6-221">Once connected, you are presented with a `sftp>` prompt.</span></span> <span data-ttu-id="a73e6-222">From this prompt, you can change directories, upload, and download files.</span><span class="sxs-lookup"><span data-stu-id="a73e6-222">From this prompt, you can change directories, upload, and download files.</span></span> <span data-ttu-id="a73e6-223">For example, the following commands change directories to the **/var/log/hadoop/hdfs** directory and then download all files in the directory.</span><span class="sxs-lookup"><span data-stu-id="a73e6-223">For example, the following commands change directories to the **/var/log/hadoop/hdfs** directory and then download all files in the directory.</span></span>

    cd /var/log/hadoop/hdfs
    get *

<span data-ttu-id="a73e6-224">For a list of available commands, enter `help` at the `sftp>` prompt.</span><span class="sxs-lookup"><span data-stu-id="a73e6-224">For a list of available commands, enter `help` at the `sftp>` prompt.</span></span>

> [!NOTE]
> <span data-ttu-id="a73e6-225">There are also graphical interfaces that allow you to visualize the file system when connected using SFTP.</span><span class="sxs-lookup"><span data-stu-id="a73e6-225">There are also graphical interfaces that allow you to visualize the file system when connected using SFTP.</span></span> <span data-ttu-id="a73e6-226">For example, [MobaXTerm](http://mobaxterm.mobatek.net/) allows you to browse the file system using an interface similar to Windows Explorer.</span><span class="sxs-lookup"><span data-stu-id="a73e6-226">For example, [MobaXTerm](http://mobaxterm.mobatek.net/) allows you to browse the file system using an interface similar to Windows Explorer.</span></span>

### <a name="ambari"></a><span data-ttu-id="a73e6-227">Ambari</span><span class="sxs-lookup"><span data-stu-id="a73e6-227">Ambari</span></span>

> [!NOTE]
> <span data-ttu-id="a73e6-228">To access log files using Ambari, you must use an SSH tunnel.</span><span class="sxs-lookup"><span data-stu-id="a73e6-228">To access log files using Ambari, you must use an SSH tunnel.</span></span> <span data-ttu-id="a73e6-229">The web interface for the individual services are not exposed publicly on the Internet.</span><span class="sxs-lookup"><span data-stu-id="a73e6-229">The web interface for the individual services are not exposed publicly on the Internet.</span></span> <span data-ttu-id="a73e6-230">For information on using an SSH tunnel, see [Use SSH Tunneling to access Ambari web UI, ResourceManager, JobHistory, NameNode, Oozie, and other web UIs](hdinsight-linux-ambari-ssh-tunnel.md).</span><span class="sxs-lookup"><span data-stu-id="a73e6-230">For information on using an SSH tunnel, see [Use SSH Tunneling to access Ambari web UI, ResourceManager, JobHistory, NameNode, Oozie, and other web UIs](hdinsight-linux-ambari-ssh-tunnel.md).</span></span>

<span data-ttu-id="a73e6-231">From the Ambari Web UI, select the service you wish to view logs for (for example, YARN).</span><span class="sxs-lookup"><span data-stu-id="a73e6-231">From the Ambari Web UI, select the service you wish to view logs for (for example, YARN).</span></span> <span data-ttu-id="a73e6-232">Then use **Quick Links** to select which head node to view the logs for.</span><span class="sxs-lookup"><span data-stu-id="a73e6-232">Then use **Quick Links** to select which head node to view the logs for.</span></span>

![Using quick links to view logs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-high-availability-linux/viewlogs.png)

## <a name="how-to-configure-the-node-size"></a><span data-ttu-id="a73e6-234">How to configure the node size</span><span class="sxs-lookup"><span data-stu-id="a73e6-234">How to configure the node size</span></span>

<span data-ttu-id="a73e6-235">The size of a node can only be selected during cluster creation.</span><span class="sxs-lookup"><span data-stu-id="a73e6-235">The size of a node can only be selected during cluster creation.</span></span> <span data-ttu-id="a73e6-236">You can find a list of the different VM sizes available for HDInsight, including the core, memory, and local storage for each, on the [HDInsight pricing page](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="a73e6-236">You can find a list of the different VM sizes available for HDInsight, including the core, memory, and local storage for each, on the [HDInsight pricing page](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

<span data-ttu-id="a73e6-237">When creating a new cluster, you can specify the size of the nodes.</span><span class="sxs-lookup"><span data-stu-id="a73e6-237">When creating a new cluster, you can specify the size of the nodes.</span></span> <span data-ttu-id="a73e6-238">The following information provides guidance on how to specify the size using the [Azure portal][preview-portal], [Azure PowerShell][azure-powershell], and the [Azure CLI][azure-cli]:</span><span class="sxs-lookup"><span data-stu-id="a73e6-238">The following information provides guidance on how to specify the size using the [Azure portal][preview-portal], [Azure PowerShell][azure-powershell], and the [Azure CLI][azure-cli]:</span></span>

* <span data-ttu-id="a73e6-239">**Azure portal**: When creating a cluster, you can set the size of the nodes used by the cluster:</span><span class="sxs-lookup"><span data-stu-id="a73e6-239">**Azure portal**: When creating a cluster, you can set the size of the nodes used by the cluster:</span></span>

    ![Image of cluster creation wizard with node size selection](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-high-availability-linux/headnodesize.png)

* <span data-ttu-id="a73e6-241">**Azure CLI**: When using the `azure hdinsight cluster create` command, you can set the size of the head, worker, and ZooKeeper nodes by using the `--headNodeSize`, `--workerNodeSize`, and `--zookeeperNodeSize` parameters.</span><span class="sxs-lookup"><span data-stu-id="a73e6-241">**Azure CLI**: When using the `azure hdinsight cluster create` command, you can set the size of the head, worker, and ZooKeeper nodes by using the `--headNodeSize`, `--workerNodeSize`, and `--zookeeperNodeSize` parameters.</span></span>

* <span data-ttu-id="a73e6-242">**Azure PowerShell**: When using the `New-AzureRmHDInsightCluster` cmdlet, you can set the size of the head, worker, and ZooKeeper nodes by using the `-HeadNodeVMSize`, `-WorkerNodeSize`, and `-ZookeeperNodeSize` parameters.</span><span class="sxs-lookup"><span data-stu-id="a73e6-242">**Azure PowerShell**: When using the `New-AzureRmHDInsightCluster` cmdlet, you can set the size of the head, worker, and ZooKeeper nodes by using the `-HeadNodeVMSize`, `-WorkerNodeSize`, and `-ZookeeperNodeSize` parameters.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a73e6-243">Next steps</span><span class="sxs-lookup"><span data-stu-id="a73e6-243">Next steps</span></span>

<span data-ttu-id="a73e6-244">Use the following links to learn more about things mentioned in this document.</span><span class="sxs-lookup"><span data-stu-id="a73e6-244">Use the following links to learn more about things mentioned in this document.</span></span>

* [<span data-ttu-id="a73e6-245">Ambari REST Reference</span><span class="sxs-lookup"><span data-stu-id="a73e6-245">Ambari REST Reference</span></span>](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md)
* [<span data-ttu-id="a73e6-246">Install and configure the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="a73e6-246">Install and configure the Azure CLI</span></span>](../cli-install-nodejs.md)
* [<span data-ttu-id="a73e6-247">Install and configure Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="a73e6-247">Install and configure Azure PowerShell</span></span>](/powershell/azureps-cmdlets-docs)
* [<span data-ttu-id="a73e6-248">Manage HDInsight using Ambari</span><span class="sxs-lookup"><span data-stu-id="a73e6-248">Manage HDInsight using Ambari</span></span>](hdinsight-hadoop-manage-ambari.md)
* [<span data-ttu-id="a73e6-249">Provision Linux-based HDInsight clusters</span><span class="sxs-lookup"><span data-stu-id="a73e6-249">Provision Linux-based HDInsight clusters</span></span>](hdinsight-hadoop-provision-linux-clusters.md)

[preview-portal]: https://portal.azure.com/
[azure-powershell]: /powershell/azureps-cmdlets-docs
[azure-cli]: ../cli-install-nodejs.md





