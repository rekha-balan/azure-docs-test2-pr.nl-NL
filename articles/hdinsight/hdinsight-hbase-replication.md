---
title: Configure HBase replication | Microsoft Docs
description: Learn how to configure HBase replication for load balancing, high availability, zero-downtime migration/update from one HDInsight version to another, and disaster recovery.
services: hdinsight,virtual-network
documentationcenter: ''
author: mumian
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 02/22/2017
ms.author: jgao
ms.openlocfilehash: a6e984f31c4d87f9ee3a81817bb4b1ba5e530c8d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555837"
---
# <a name="configure-hbase-replication"></a><span data-ttu-id="b520a-103">Configure HBase replication</span><span class="sxs-lookup"><span data-stu-id="b520a-103">Configure HBase replication</span></span>

<span data-ttu-id="b520a-104">Learn how to configure HBase replication within one virtual network (VNet) or between two virtual networks.</span><span class="sxs-lookup"><span data-stu-id="b520a-104">Learn how to configure HBase replication within one virtual network (VNet) or between two virtual networks.</span></span>

<span data-ttu-id="b520a-105">Cluster replication uses a source-push methodology.</span><span class="sxs-lookup"><span data-stu-id="b520a-105">Cluster replication uses a source-push methodology.</span></span> <span data-ttu-id="b520a-106">An HBase cluster can be a source or a destination, or it can fulfill both roles at once.</span><span class="sxs-lookup"><span data-stu-id="b520a-106">An HBase cluster can be a source or a destination, or it can fulfill both roles at once.</span></span> <span data-ttu-id="b520a-107">Replication is asynchronous, and the goal of replication is eventual consistency.</span><span class="sxs-lookup"><span data-stu-id="b520a-107">Replication is asynchronous, and the goal of replication is eventual consistency.</span></span> <span data-ttu-id="b520a-108">When the source receives an edit to a column family with replication enabled, that edit is propagated to all destination clusters.</span><span class="sxs-lookup"><span data-stu-id="b520a-108">When the source receives an edit to a column family with replication enabled, that edit is propagated to all destination clusters.</span></span> <span data-ttu-id="b520a-109">When data is replicated from one cluster to another, the source cluster and all clusters that have already consumed the data are tracked to prevent replication loops.</span><span class="sxs-lookup"><span data-stu-id="b520a-109">When data is replicated from one cluster to another, the source cluster and all clusters that have already consumed the data are tracked to prevent replication loops.</span></span>

<span data-ttu-id="b520a-110">In this tutorial, you will configure a source-destination replication.</span><span class="sxs-lookup"><span data-stu-id="b520a-110">In this tutorial, you will configure a source-destination replication.</span></span> <span data-ttu-id="b520a-111">For other cluster topologies, see [Apache HBase Reference Guide](http://hbase.apache.org/book.html#_cluster_replication).</span><span class="sxs-lookup"><span data-stu-id="b520a-111">For other cluster topologies, see [Apache HBase Reference Guide](http://hbase.apache.org/book.html#_cluster_replication).</span></span>

<span data-ttu-id="b520a-112">HBase replication usage cases for a single virtual network:</span><span class="sxs-lookup"><span data-stu-id="b520a-112">HBase replication usage cases for a single virtual network:</span></span>

* <span data-ttu-id="b520a-113">Load balancing--for example, running scans or MapReduce jobs on the destination cluster and ingesting data on the source cluster</span><span class="sxs-lookup"><span data-stu-id="b520a-113">Load balancing--for example, running scans or MapReduce jobs on the destination cluster and ingesting data on the source cluster</span></span>
* <span data-ttu-id="b520a-114">High availability</span><span class="sxs-lookup"><span data-stu-id="b520a-114">High availability</span></span>
* <span data-ttu-id="b520a-115">Migrating data from one HBase cluster to another</span><span class="sxs-lookup"><span data-stu-id="b520a-115">Migrating data from one HBase cluster to another</span></span>
* <span data-ttu-id="b520a-116">Upgrading an Azure HDInsight cluster from one version to another</span><span class="sxs-lookup"><span data-stu-id="b520a-116">Upgrading an Azure HDInsight cluster from one version to another</span></span>

<span data-ttu-id="b520a-117">HBase replication usage cases for two virtual networks:</span><span class="sxs-lookup"><span data-stu-id="b520a-117">HBase replication usage cases for two virtual networks:</span></span>

* <span data-ttu-id="b520a-118">Disaster recovery</span><span class="sxs-lookup"><span data-stu-id="b520a-118">Disaster recovery</span></span>
* <span data-ttu-id="b520a-119">Load balancing and partitioning the application</span><span class="sxs-lookup"><span data-stu-id="b520a-119">Load balancing and partitioning the application</span></span>
* <span data-ttu-id="b520a-120">High availability</span><span class="sxs-lookup"><span data-stu-id="b520a-120">High availability</span></span>

<span data-ttu-id="b520a-121">You replicate clusters by using [script action](hdinsight-hadoop-customize-cluster-linux.md) scripts located at [GitHub](https://github.com/Azure/hbase-utils/tree/master/replication).</span><span class="sxs-lookup"><span data-stu-id="b520a-121">You replicate clusters by using [script action](hdinsight-hadoop-customize-cluster-linux.md) scripts located at [GitHub](https://github.com/Azure/hbase-utils/tree/master/replication).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b520a-122">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b520a-122">Prerequisites</span></span>
<span data-ttu-id="b520a-123">Before you begin this tutorial, you must have an Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="b520a-123">Before you begin this tutorial, you must have an Azure subscription.</span></span> <span data-ttu-id="b520a-124">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="b520a-124">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

## <a name="configure-the-environments"></a><span data-ttu-id="b520a-125">Configure the environments</span><span class="sxs-lookup"><span data-stu-id="b520a-125">Configure the environments</span></span>

<span data-ttu-id="b520a-126">There are three possible configurations:</span><span class="sxs-lookup"><span data-stu-id="b520a-126">There are three possible configurations:</span></span>

- <span data-ttu-id="b520a-127">Two HBase clusters in one Azure virtual network</span><span class="sxs-lookup"><span data-stu-id="b520a-127">Two HBase clusters in one Azure virtual network</span></span>
- <span data-ttu-id="b520a-128">Two HBase clusters in two different virtual networks in the same region</span><span class="sxs-lookup"><span data-stu-id="b520a-128">Two HBase clusters in two different virtual networks in the same region</span></span>
- <span data-ttu-id="b520a-129">Two HBase clusters in two different virtual networks in two different regions (geo-replication)</span><span class="sxs-lookup"><span data-stu-id="b520a-129">Two HBase clusters in two different virtual networks in two different regions (geo-replication)</span></span>

<span data-ttu-id="b520a-130">To make it easier to configure the environments, we have created some [Azure Resource Manager templates](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b520a-130">To make it easier to configure the environments, we have created some [Azure Resource Manager templates](../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="b520a-131">If you prefer to configure the environments by using other methods, see:</span><span class="sxs-lookup"><span data-stu-id="b520a-131">If you prefer to configure the environments by using other methods, see:</span></span>

- [<span data-ttu-id="b520a-132">Create Linux-based Hadoop clusters in HDInsight</span><span class="sxs-lookup"><span data-stu-id="b520a-132">Create Linux-based Hadoop clusters in HDInsight</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
- [<span data-ttu-id="b520a-133">Create HBase clusters in Azure Virtual Network</span><span class="sxs-lookup"><span data-stu-id="b520a-133">Create HBase clusters in Azure Virtual Network</span></span>](hdinsight-hbase-provision-vnet.md)

### <a name="configure-one-virtual-network"></a><span data-ttu-id="b520a-134">Configure one virtual network</span><span class="sxs-lookup"><span data-stu-id="b520a-134">Configure one virtual network</span></span>

<span data-ttu-id="b520a-135">Click the following image to create two HBase clusters in the same virtual network.</span><span class="sxs-lookup"><span data-stu-id="b520a-135">Click the following image to create two HBase clusters in the same virtual network.</span></span> <span data-ttu-id="b520a-136">The template is stored in [Azure QuickStart Templates](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-one-vnet/).</span><span class="sxs-lookup"><span data-stu-id="b520a-136">The template is stored in [Azure QuickStart Templates](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-one-vnet/).</span></span>

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-replication-one-vnet%2Fazuredeploy.json" target="_blank"><img src="https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy to Azure"></a>

### <a name="configure-two-virtual-networks-in-the-same-region"></a><span data-ttu-id="b520a-137">Configure two virtual networks in the same region</span><span class="sxs-lookup"><span data-stu-id="b520a-137">Configure two virtual networks in the same region</span></span>

<span data-ttu-id="b520a-138">Click the following image to create two virtual networks with VNet peering and two HBase clusters in the same region.</span><span class="sxs-lookup"><span data-stu-id="b520a-138">Click the following image to create two virtual networks with VNet peering and two HBase clusters in the same region.</span></span> <span data-ttu-id="b520a-139">The template is stored in [Azure QuickStart Templates](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-two-vnets-same-region/).</span><span class="sxs-lookup"><span data-stu-id="b520a-139">The template is stored in [Azure QuickStart Templates](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-two-vnets-same-region/).</span></span>

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-replication-two-vnets-same-region%2Fazuredeploy.json" target="_blank"><img src="https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy to Azure"></a>



<span data-ttu-id="b520a-140">This scenario requires [VNet peering](../virtual-network/virtual-network-peering-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b520a-140">This scenario requires [VNet peering](../virtual-network/virtual-network-peering-overview.md).</span></span> <span data-ttu-id="b520a-141">The template enables VNet peering.</span><span class="sxs-lookup"><span data-stu-id="b520a-141">The template enables VNet peering.</span></span>   

<span data-ttu-id="b520a-142">HBase replication uses IP addresses of the ZooKeeper VMs.</span><span class="sxs-lookup"><span data-stu-id="b520a-142">HBase replication uses IP addresses of the ZooKeeper VMs.</span></span> <span data-ttu-id="b520a-143">You must configure static IP addresses for the destination HBase ZooKeeper nodes.</span><span class="sxs-lookup"><span data-stu-id="b520a-143">You must configure static IP addresses for the destination HBase ZooKeeper nodes.</span></span>

<span data-ttu-id="b520a-144">**To configure static IP addresses**</span><span class="sxs-lookup"><span data-stu-id="b520a-144">**To configure static IP addresses**</span></span>

1. <span data-ttu-id="b520a-145">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b520a-145">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b520a-146">From the left menu, click **Resource Groups**.</span><span class="sxs-lookup"><span data-stu-id="b520a-146">From the left menu, click **Resource Groups**.</span></span>
3. <span data-ttu-id="b520a-147">Click your resource group that contains the destination HBase cluster.</span><span class="sxs-lookup"><span data-stu-id="b520a-147">Click your resource group that contains the destination HBase cluster.</span></span> <span data-ttu-id="b520a-148">This is the resource group that you specified when you used the Resource Manager template to create the environment.</span><span class="sxs-lookup"><span data-stu-id="b520a-148">This is the resource group that you specified when you used the Resource Manager template to create the environment.</span></span> <span data-ttu-id="b520a-149">You can use the filter to narrow down the list.</span><span class="sxs-lookup"><span data-stu-id="b520a-149">You can use the filter to narrow down the list.</span></span> <span data-ttu-id="b520a-150">You can see a list of resources that contains the two virtual networks.</span><span class="sxs-lookup"><span data-stu-id="b520a-150">You can see a list of resources that contains the two virtual networks.</span></span>
4. <span data-ttu-id="b520a-151">Click the virtual network that contains the destination HBase cluster.</span><span class="sxs-lookup"><span data-stu-id="b520a-151">Click the virtual network that contains the destination HBase cluster.</span></span> <span data-ttu-id="b520a-152">For example, click **xxxx-vnet2**.</span><span class="sxs-lookup"><span data-stu-id="b520a-152">For example, click **xxxx-vnet2**.</span></span> <span data-ttu-id="b520a-153">You can see three devices with names that start with **nic-zookeepermode-**.</span><span class="sxs-lookup"><span data-stu-id="b520a-153">You can see three devices with names that start with **nic-zookeepermode-**.</span></span> <span data-ttu-id="b520a-154">Those devices are the three ZooKeeper VMs.</span><span class="sxs-lookup"><span data-stu-id="b520a-154">Those devices are the three ZooKeeper VMs.</span></span>
5. <span data-ttu-id="b520a-155">Click one of the ZooKeeper VMs.</span><span class="sxs-lookup"><span data-stu-id="b520a-155">Click one of the ZooKeeper VMs.</span></span>
6. <span data-ttu-id="b520a-156">Click **IP configurations**.</span><span class="sxs-lookup"><span data-stu-id="b520a-156">Click **IP configurations**.</span></span>
7. <span data-ttu-id="b520a-157">Click **ipConfig1** from the list.</span><span class="sxs-lookup"><span data-stu-id="b520a-157">Click **ipConfig1** from the list.</span></span>
8. <span data-ttu-id="b520a-158">Click **Static**, and write down the actual IP address.</span><span class="sxs-lookup"><span data-stu-id="b520a-158">Click **Static**, and write down the actual IP address.</span></span> <span data-ttu-id="b520a-159">You will need the IP address when you run the script action to enable replication.</span><span class="sxs-lookup"><span data-stu-id="b520a-159">You will need the IP address when you run the script action to enable replication.</span></span>

  ![HDInsight HBase Replication ZooKeeper static IP](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hbase-replication/hdinsight-hbase-replication-zookeeper-static-ip.png)

9. <span data-ttu-id="b520a-161">Repeat step 6 to set the static IP address for the other two ZooKeeper nodes.</span><span class="sxs-lookup"><span data-stu-id="b520a-161">Repeat step 6 to set the static IP address for the other two ZooKeeper nodes.</span></span>

<span data-ttu-id="b520a-162">For the cross-VNet scenario, you must use the **-ip** switch when calling the **hdi_enable_replication.sh** script action.</span><span class="sxs-lookup"><span data-stu-id="b520a-162">For the cross-VNet scenario, you must use the **-ip** switch when calling the **hdi_enable_replication.sh** script action.</span></span>

### <a name="configure-two-virtual-networks-in-two-different-regions"></a><span data-ttu-id="b520a-163">Configure two virtual networks in two different regions</span><span class="sxs-lookup"><span data-stu-id="b520a-163">Configure two virtual networks in two different regions</span></span>

<span data-ttu-id="b520a-164">Click the following image to create two virtual networks in two different regions.</span><span class="sxs-lookup"><span data-stu-id="b520a-164">Click the following image to create two virtual networks in two different regions.</span></span> <span data-ttu-id="b520a-165">The template is stored in a public Azure Blob container.</span><span class="sxs-lookup"><span data-stu-id="b520a-165">The template is stored in a public Azure Blob container.</span></span>

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Fhbaseha%2Fdeploy-hbase-geo-replication.json" target="_blank"><img src="https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy to Azure"></a>

<span data-ttu-id="b520a-166">Create a VPN gateway between the two virtual networks.</span><span class="sxs-lookup"><span data-stu-id="b520a-166">Create a VPN gateway between the two virtual networks.</span></span> <span data-ttu-id="b520a-167">For instructions, see [Create a VNet with a site-to-site connection](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b520a-167">For instructions, see [Create a VNet with a site-to-site connection](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md).</span></span>

<span data-ttu-id="b520a-168">HBase replication uses IP addresses of the ZooKeeper VMs.</span><span class="sxs-lookup"><span data-stu-id="b520a-168">HBase replication uses IP addresses of the ZooKeeper VMs.</span></span> <span data-ttu-id="b520a-169">You must configure static IP addresses for the destination HBase ZooKeeper nodes.</span><span class="sxs-lookup"><span data-stu-id="b520a-169">You must configure static IP addresses for the destination HBase ZooKeeper nodes.</span></span> <span data-ttu-id="b520a-170">To configure static IP, see the "Configure two virtual networks in the same region" section in this article.</span><span class="sxs-lookup"><span data-stu-id="b520a-170">To configure static IP, see the "Configure two virtual networks in the same region" section in this article.</span></span>

<span data-ttu-id="b520a-171">For the cross-VNet scenario, you must use the **-ip** switch when calling the **hdi_enable_replication.sh** script action.</span><span class="sxs-lookup"><span data-stu-id="b520a-171">For the cross-VNet scenario, you must use the **-ip** switch when calling the **hdi_enable_replication.sh** script action.</span></span>

## <a name="load-test-data"></a><span data-ttu-id="b520a-172">Load test data</span><span class="sxs-lookup"><span data-stu-id="b520a-172">Load test data</span></span>

<span data-ttu-id="b520a-173">When you replicate a cluster, you must specify the tables to replicate.</span><span class="sxs-lookup"><span data-stu-id="b520a-173">When you replicate a cluster, you must specify the tables to replicate.</span></span> <span data-ttu-id="b520a-174">In this section, you will load some data into the source cluster.</span><span class="sxs-lookup"><span data-stu-id="b520a-174">In this section, you will load some data into the source cluster.</span></span> <span data-ttu-id="b520a-175">In the next section, you will enable replication between the two clusters.</span><span class="sxs-lookup"><span data-stu-id="b520a-175">In the next section, you will enable replication between the two clusters.</span></span>

<span data-ttu-id="b520a-176">Follow the instructions in [HBase tutorial: Get started using Apache HBase with Linux-based Hadoop in HDInsight](hdinsight-hbase-tutorial-get-started-linux.md) to create a **Contacts** table and insert some data into the table.</span><span class="sxs-lookup"><span data-stu-id="b520a-176">Follow the instructions in [HBase tutorial: Get started using Apache HBase with Linux-based Hadoop in HDInsight](hdinsight-hbase-tutorial-get-started-linux.md) to create a **Contacts** table and insert some data into the table.</span></span>

## <a name="enable-replication"></a><span data-ttu-id="b520a-177">Enable replication</span><span class="sxs-lookup"><span data-stu-id="b520a-177">Enable replication</span></span>

<span data-ttu-id="b520a-178">The following steps show how to call the script action script from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="b520a-178">The following steps show how to call the script action script from the Azure portal.</span></span> <span data-ttu-id="b520a-179">For running a script action by using Azure PowerShell and the Azure command-line interface (CLI), see [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="b520a-179">For running a script action by using Azure PowerShell and the Azure command-line interface (CLI), see [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

<span data-ttu-id="b520a-180">**To enable HBase replication from the Azure portal**</span><span class="sxs-lookup"><span data-stu-id="b520a-180">**To enable HBase replication from the Azure portal**</span></span>

1. <span data-ttu-id="b520a-181">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b520a-181">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b520a-182">Open the source HBase cluster.</span><span class="sxs-lookup"><span data-stu-id="b520a-182">Open the source HBase cluster.</span></span>
3. <span data-ttu-id="b520a-183">From the cluster menu, click **Script Actions**.</span><span class="sxs-lookup"><span data-stu-id="b520a-183">From the cluster menu, click **Script Actions**.</span></span>
4. <span data-ttu-id="b520a-184">Click **Submit New** from the top of the blade.</span><span class="sxs-lookup"><span data-stu-id="b520a-184">Click **Submit New** from the top of the blade.</span></span>
5. <span data-ttu-id="b520a-185">Select or enter the following information:</span><span class="sxs-lookup"><span data-stu-id="b520a-185">Select or enter the following information:</span></span>

  - <span data-ttu-id="b520a-186">**Name**: Enter **Enable replication**.</span><span class="sxs-lookup"><span data-stu-id="b520a-186">**Name**: Enter **Enable replication**.</span></span>
  - <span data-ttu-id="b520a-187">**Bash Script URL**: Enter **https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_enable_replication.sh**.</span><span class="sxs-lookup"><span data-stu-id="b520a-187">**Bash Script URL**: Enter **https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_enable_replication.sh**.</span></span>
  - <span data-ttu-id="b520a-188">**Head**: Selected.</span><span class="sxs-lookup"><span data-stu-id="b520a-188">**Head**: Selected.</span></span> <span data-ttu-id="b520a-189">Clear the other node types.</span><span class="sxs-lookup"><span data-stu-id="b520a-189">Clear the other node types.</span></span>
  - <span data-ttu-id="b520a-190">**Parameters**: The following sample parameters enable replication for all the existing tables and copy all the data from the source cluster to the destination cluster:</span><span class="sxs-lookup"><span data-stu-id="b520a-190">**Parameters**: The following sample parameters enable replication for all the existing tables and copy all the data from the source cluster to the destination cluster:</span></span>

            -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -copydata

6. <span data-ttu-id="b520a-191">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="b520a-191">Click **Create**.</span></span> <span data-ttu-id="b520a-192">The script can take some time, especially when the -copydata argument is used.</span><span class="sxs-lookup"><span data-stu-id="b520a-192">The script can take some time, especially when the -copydata argument is used.</span></span>

<span data-ttu-id="b520a-193">Required arguments:</span><span class="sxs-lookup"><span data-stu-id="b520a-193">Required arguments:</span></span>

|<span data-ttu-id="b520a-194">Name</span><span class="sxs-lookup"><span data-stu-id="b520a-194">Name</span></span>|<span data-ttu-id="b520a-195">Description</span><span class="sxs-lookup"><span data-stu-id="b520a-195">Description</span></span>|
|----|-----------|
|<span data-ttu-id="b520a-196">-s, --src-cluster</span><span class="sxs-lookup"><span data-stu-id="b520a-196">-s, --src-cluster</span></span> | <span data-ttu-id="b520a-197">Specify the DNS name of the source HBase cluster.</span><span class="sxs-lookup"><span data-stu-id="b520a-197">Specify the DNS name of the source HBase cluster.</span></span> <span data-ttu-id="b520a-198">For example: -s hbsrccluster, --src-cluster=hbsrccluster</span><span class="sxs-lookup"><span data-stu-id="b520a-198">For example: -s hbsrccluster, --src-cluster=hbsrccluster</span></span> |
|<span data-ttu-id="b520a-199">-d, --dst-cluster</span><span class="sxs-lookup"><span data-stu-id="b520a-199">-d, --dst-cluster</span></span> | <span data-ttu-id="b520a-200">Specify the DNS name of the destination (replica) HBase cluster.</span><span class="sxs-lookup"><span data-stu-id="b520a-200">Specify the DNS name of the destination (replica) HBase cluster.</span></span> <span data-ttu-id="b520a-201">For example: -s dsthbcluster, --src-cluster=dsthbcluster</span><span class="sxs-lookup"><span data-stu-id="b520a-201">For example: -s dsthbcluster, --src-cluster=dsthbcluster</span></span> |
|<span data-ttu-id="b520a-202">-sp, --src-ambari-password</span><span class="sxs-lookup"><span data-stu-id="b520a-202">-sp, --src-ambari-password</span></span> | <span data-ttu-id="b520a-203">Specify the admin password for Ambari on the source HBase cluster.</span><span class="sxs-lookup"><span data-stu-id="b520a-203">Specify the admin password for Ambari on the source HBase cluster.</span></span> |
|<span data-ttu-id="b520a-204">-dp, --dst-ambari-password</span><span class="sxs-lookup"><span data-stu-id="b520a-204">-dp, --dst-ambari-password</span></span> | <span data-ttu-id="b520a-205">Specify the admin password for Ambari on the destination HBase cluster.</span><span class="sxs-lookup"><span data-stu-id="b520a-205">Specify the admin password for Ambari on the destination HBase cluster.</span></span>|

<span data-ttu-id="b520a-206">Optional arguments:</span><span class="sxs-lookup"><span data-stu-id="b520a-206">Optional arguments:</span></span>

|<span data-ttu-id="b520a-207">Name</span><span class="sxs-lookup"><span data-stu-id="b520a-207">Name</span></span>|<span data-ttu-id="b520a-208">Description</span><span class="sxs-lookup"><span data-stu-id="b520a-208">Description</span></span>|
|----|-----------|
|<span data-ttu-id="b520a-209">-su, --src-ambari-user</span><span class="sxs-lookup"><span data-stu-id="b520a-209">-su, --src-ambari-user</span></span> | <span data-ttu-id="b520a-210">Specify the admin username for Ambari on the source HBase cluster.</span><span class="sxs-lookup"><span data-stu-id="b520a-210">Specify the admin username for Ambari on the source HBase cluster.</span></span> <span data-ttu-id="b520a-211">The default value is **admin**.</span><span class="sxs-lookup"><span data-stu-id="b520a-211">The default value is **admin**.</span></span> |
|<span data-ttu-id="b520a-212">-du, --dst-ambari-user</span><span class="sxs-lookup"><span data-stu-id="b520a-212">-du, --dst-ambari-user</span></span> | <span data-ttu-id="b520a-213">Specify the admin username for Ambari on the destination HBase cluster.</span><span class="sxs-lookup"><span data-stu-id="b520a-213">Specify the admin username for Ambari on the destination HBase cluster.</span></span> <span data-ttu-id="b520a-214">The default value is **admin**.</span><span class="sxs-lookup"><span data-stu-id="b520a-214">The default value is **admin**.</span></span> |
|<span data-ttu-id="b520a-215">-t, --table-list</span><span class="sxs-lookup"><span data-stu-id="b520a-215">-t, --table-list</span></span> | <span data-ttu-id="b520a-216">Specify the tables to be replicated.</span><span class="sxs-lookup"><span data-stu-id="b520a-216">Specify the tables to be replicated.</span></span> <span data-ttu-id="b520a-217">For example: --table-list="table1;table2;table3".</span><span class="sxs-lookup"><span data-stu-id="b520a-217">For example: --table-list="table1;table2;table3".</span></span> <span data-ttu-id="b520a-218">If you don't specify tables, all existing HBase tables are replicated.</span><span class="sxs-lookup"><span data-stu-id="b520a-218">If you don't specify tables, all existing HBase tables are replicated.</span></span>|
|<span data-ttu-id="b520a-219">-m, --machine</span><span class="sxs-lookup"><span data-stu-id="b520a-219">-m, --machine</span></span> | <span data-ttu-id="b520a-220">Specify the head node where the script action will run.</span><span class="sxs-lookup"><span data-stu-id="b520a-220">Specify the head node where the script action will run.</span></span> <span data-ttu-id="b520a-221">The value is either hn1 or hn0.</span><span class="sxs-lookup"><span data-stu-id="b520a-221">The value is either hn1 or hn0.</span></span> <span data-ttu-id="b520a-222">Because hn0 is usually busier, we recommend using hn1.</span><span class="sxs-lookup"><span data-stu-id="b520a-222">Because hn0 is usually busier, we recommend using hn1.</span></span> <span data-ttu-id="b520a-223">You use this option when you're running the $0 script as a script action from the HDInsight portal or Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b520a-223">You use this option when you're running the $0 script as a script action from the HDInsight portal or Azure PowerShell.</span></span>|
|<span data-ttu-id="b520a-224">-ip</span><span class="sxs-lookup"><span data-stu-id="b520a-224">-ip</span></span> | <span data-ttu-id="b520a-225">This argument is required when you're enabling replication between two virtual networks.</span><span class="sxs-lookup"><span data-stu-id="b520a-225">This argument is required when you're enabling replication between two virtual networks.</span></span> <span data-ttu-id="b520a-226">This argument acts as a switch to use the static IPs of ZooKeeper nodes from replica clusters instead of FQDN names.</span><span class="sxs-lookup"><span data-stu-id="b520a-226">This argument acts as a switch to use the static IPs of ZooKeeper nodes from replica clusters instead of FQDN names.</span></span> <span data-ttu-id="b520a-227">The static IPs need to be preconfigured before you enable replication.</span><span class="sxs-lookup"><span data-stu-id="b520a-227">The static IPs need to be preconfigured before you enable replication.</span></span> |
|<span data-ttu-id="b520a-228">-cp, -copydata</span><span class="sxs-lookup"><span data-stu-id="b520a-228">-cp, -copydata</span></span> | <span data-ttu-id="b520a-229">Enable the migration of existing data on the tables where replication is enabled.</span><span class="sxs-lookup"><span data-stu-id="b520a-229">Enable the migration of existing data on the tables where replication is enabled.</span></span> |
|<span data-ttu-id="b520a-230">-rpm, -replicate-phoenix-meta</span><span class="sxs-lookup"><span data-stu-id="b520a-230">-rpm, -replicate-phoenix-meta</span></span> | <span data-ttu-id="b520a-231">Enable replication on Phoenix system tables.</span><span class="sxs-lookup"><span data-stu-id="b520a-231">Enable replication on Phoenix system tables.</span></span> <br><br><span data-ttu-id="b520a-232">*Use this option with caution.*</span><span class="sxs-lookup"><span data-stu-id="b520a-232">*Use this option with caution.*</span></span> <span data-ttu-id="b520a-233">We recommend that you re-create Phoenix tables on replica clusters before you use this script.</span><span class="sxs-lookup"><span data-stu-id="b520a-233">We recommend that you re-create Phoenix tables on replica clusters before you use this script.</span></span> |
|<span data-ttu-id="b520a-234">-h, --help</span><span class="sxs-lookup"><span data-stu-id="b520a-234">-h, --help</span></span> | <span data-ttu-id="b520a-235">Display usage information.</span><span class="sxs-lookup"><span data-stu-id="b520a-235">Display usage information.</span></span> |

<span data-ttu-id="b520a-236">The print_usage() section of the [script](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_enable_replication.sh) provides a detailed explanation of parameters.</span><span class="sxs-lookup"><span data-stu-id="b520a-236">The print_usage() section of the [script](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_enable_replication.sh) provides a detailed explanation of parameters.</span></span>

<span data-ttu-id="b520a-237">After the script action is successfully deployed, you can use SSH to connect to the destination HBase cluster, and verify the data has been replicated.</span><span class="sxs-lookup"><span data-stu-id="b520a-237">After the script action is successfully deployed, you can use SSH to connect to the destination HBase cluster, and verify the data has been replicated.</span></span>

### <a name="replication-scenarios"></a><span data-ttu-id="b520a-238">Replication scenarios</span><span class="sxs-lookup"><span data-stu-id="b520a-238">Replication scenarios</span></span>

<span data-ttu-id="b520a-239">The following list shows you some general usage cases and their parameter settings:</span><span class="sxs-lookup"><span data-stu-id="b520a-239">The following list shows you some general usage cases and their parameter settings:</span></span>

- <span data-ttu-id="b520a-240">**Enable replication on all tables between the two clusters**.</span><span class="sxs-lookup"><span data-stu-id="b520a-240">**Enable replication on all tables between the two clusters**.</span></span> <span data-ttu-id="b520a-241">This scenario does not require the copy/migration of existing data on the tables, and it does not use Phoenix tables.</span><span class="sxs-lookup"><span data-stu-id="b520a-241">This scenario does not require the copy/migration of existing data on the tables, and it does not use Phoenix tables.</span></span> <span data-ttu-id="b520a-242">Use the following parameters:</span><span class="sxs-lookup"><span data-stu-id="b520a-242">Use the following parameters:</span></span>

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password>  

- <span data-ttu-id="b520a-243">**Enable replication on specific tables**.</span><span class="sxs-lookup"><span data-stu-id="b520a-243">**Enable replication on specific tables**.</span></span> <span data-ttu-id="b520a-244">Use the following parameters to enable replication on table1, table2, and table3:</span><span class="sxs-lookup"><span data-stu-id="b520a-244">Use the following parameters to enable replication on table1, table2, and table3:</span></span>

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3"

- <span data-ttu-id="b520a-245">**Enable replication on specific tables and copy the existing data**.</span><span class="sxs-lookup"><span data-stu-id="b520a-245">**Enable replication on specific tables and copy the existing data**.</span></span> <span data-ttu-id="b520a-246">Use the following parameters to enable replication on table1, table2, and table3:</span><span class="sxs-lookup"><span data-stu-id="b520a-246">Use the following parameters to enable replication on table1, table2, and table3:</span></span>

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3" -copydata

- <span data-ttu-id="b520a-247">**Enable replication on all tables with replicating phoenix metadata from source to destination**.</span><span class="sxs-lookup"><span data-stu-id="b520a-247">**Enable replication on all tables with replicating phoenix metadata from source to destination**.</span></span> <span data-ttu-id="b520a-248">Phoenix metadata replication is not perfect and should be enabled with caution.</span><span class="sxs-lookup"><span data-stu-id="b520a-248">Phoenix metadata replication is not perfect and should be enabled with caution.</span></span>

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3" -replicate-phoenix-meta

## <a name="copy-and-migrate-data"></a><span data-ttu-id="b520a-249">Copy and migrate data</span><span class="sxs-lookup"><span data-stu-id="b520a-249">Copy and migrate data</span></span>

<span data-ttu-id="b520a-250">There are two separate script action scripts for copying/migrating data after replication is enabled:</span><span class="sxs-lookup"><span data-stu-id="b520a-250">There are two separate script action scripts for copying/migrating data after replication is enabled:</span></span>

- <span data-ttu-id="b520a-251">[Script for small tables](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_copy_table.sh) (a few gigabytes in size, and overall copy is expected to finish in less than one hour)</span><span class="sxs-lookup"><span data-stu-id="b520a-251">[Script for small tables](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_copy_table.sh) (a few gigabytes in size, and overall copy is expected to finish in less than one hour)</span></span>

- <span data-ttu-id="b520a-252">[Script for large tables](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/nohup_hdi_copy_table.sh) (expected to take longer than one hour to copy)</span><span class="sxs-lookup"><span data-stu-id="b520a-252">[Script for large tables](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/nohup_hdi_copy_table.sh) (expected to take longer than one hour to copy)</span></span>

<span data-ttu-id="b520a-253">You can follow the same procedure in [Enable replication](#enable-replication) to call the script action with the following parameters:</span><span class="sxs-lookup"><span data-stu-id="b520a-253">You can follow the same procedure in [Enable replication](#enable-replication) to call the script action with the following parameters:</span></span>

    -m hn1 -t <table1:start_timestamp:end_timestamp;table2:start_timestamp:end_timestamp;...> -p <replication_peer> [-everythingTillNow]

<span data-ttu-id="b520a-254">The print_usage() section of the [script](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_copy_table.sh) provides a detailed description of parameters.</span><span class="sxs-lookup"><span data-stu-id="b520a-254">The print_usage() section of the [script](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_copy_table.sh) provides a detailed description of parameters.</span></span>

### <a name="scenarios"></a><span data-ttu-id="b520a-255">Scenarios</span><span class="sxs-lookup"><span data-stu-id="b520a-255">Scenarios</span></span>

- <span data-ttu-id="b520a-256">**Copy specific tables (test1, test2, and test3) for all rows edited till now (current time stamp)**:</span><span class="sxs-lookup"><span data-stu-id="b520a-256">**Copy specific tables (test1, test2, and test3) for all rows edited till now (current time stamp)**:</span></span>

        -m hn1 -t "test1::;test2::;test3::" -p "zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure" -everythingTillNow
  <span data-ttu-id="b520a-257">or</span><span class="sxs-lookup"><span data-stu-id="b520a-257">or</span></span>

        -m hn1 -t "test1::;test2::;test3::" --replication-peer="zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure" -everythingTillNow


- <span data-ttu-id="b520a-258">**Copy specific tables with specified time range**:</span><span class="sxs-lookup"><span data-stu-id="b520a-258">**Copy specific tables with specified time range**:</span></span>

        -m hn1 -t "table1:0:452256397;table2:14141444:452256397" -p "zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure"


## <a name="disable-replication"></a><span data-ttu-id="b520a-259">Disable replication</span><span class="sxs-lookup"><span data-stu-id="b520a-259">Disable replication</span></span>

<span data-ttu-id="b520a-260">To disable replication, you use another script action script located at [GitHub](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh).</span><span class="sxs-lookup"><span data-stu-id="b520a-260">To disable replication, you use another script action script located at [GitHub](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh).</span></span> <span data-ttu-id="b520a-261">You can follow the same procedure in [Enable replication](#enable-replication) to call the script action with the following parameters:</span><span class="sxs-lookup"><span data-stu-id="b520a-261">You can follow the same procedure in [Enable replication](#enable-replication) to call the script action with the following parameters:</span></span>

    -m hn1 -s <source cluster DNS name> -sp <source cluster Ambari Password> <-all|-t "table1;table2;...">  

<span data-ttu-id="b520a-262">The print_usage() section of the [script](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh) provides a detailed explanation of parameters.</span><span class="sxs-lookup"><span data-stu-id="b520a-262">The print_usage() section of the [script](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh) provides a detailed explanation of parameters.</span></span>

### <a name="scenarios"></a><span data-ttu-id="b520a-263">Scenarios</span><span class="sxs-lookup"><span data-stu-id="b520a-263">Scenarios</span></span>

- <span data-ttu-id="b520a-264">**Disable replication on all tables**:</span><span class="sxs-lookup"><span data-stu-id="b520a-264">**Disable replication on all tables**:</span></span>

        -m hn1 -s <source cluster DNS name> -sp Mypassword\!789 -all
  <span data-ttu-id="b520a-265">or</span><span class="sxs-lookup"><span data-stu-id="b520a-265">or</span></span>

        --src-cluster=<source cluster DNS name> --dst-cluster=<destination cluster DNS name> --src-ambari-user=<source cluster Ambari username> --src-ambari-password=<source cluster Ambari password>

- <span data-ttu-id="b520a-266">**Disable replication on specified tables (table1, table2, and table3)**:</span><span class="sxs-lookup"><span data-stu-id="b520a-266">**Disable replication on specified tables (table1, table2, and table3)**:</span></span>

        -m hn1 -s <source cluster DNS name> -sp <source cluster Ambari password> -t "table1;table2;table3"

## <a name="next-steps"></a><span data-ttu-id="b520a-267">Next steps</span><span class="sxs-lookup"><span data-stu-id="b520a-267">Next steps</span></span>

<span data-ttu-id="b520a-268">In this tutorial, you learned how to configure HBase replication across two datacenters.</span><span class="sxs-lookup"><span data-stu-id="b520a-268">In this tutorial, you learned how to configure HBase replication across two datacenters.</span></span> <span data-ttu-id="b520a-269">To learn more about HDInsight and HBase, see:</span><span class="sxs-lookup"><span data-stu-id="b520a-269">To learn more about HDInsight and HBase, see:</span></span>

* <span data-ttu-id="b520a-270">[Get started with Apache HBase in HDInsight][hdinsight-hbase-get-started]</span><span class="sxs-lookup"><span data-stu-id="b520a-270">[Get started with Apache HBase in HDInsight][hdinsight-hbase-get-started]</span></span>
* <span data-ttu-id="b520a-271">[HDInsight HBase overview][hdinsight-hbase-overview]</span><span class="sxs-lookup"><span data-stu-id="b520a-271">[HDInsight HBase overview][hdinsight-hbase-overview]</span></span>
* <span data-ttu-id="b520a-272">[Create HBase clusters in Azure Virtual Network][hdinsight-hbase-provision-vnet]</span><span class="sxs-lookup"><span data-stu-id="b520a-272">[Create HBase clusters in Azure Virtual Network][hdinsight-hbase-provision-vnet]</span></span>
* <span data-ttu-id="b520a-273">[Analyze real-time Twitter sentiment with HBase][hdinsight-hbase-twitter-sentiment]</span><span class="sxs-lookup"><span data-stu-id="b520a-273">[Analyze real-time Twitter sentiment with HBase][hdinsight-hbase-twitter-sentiment]</span></span>
* <span data-ttu-id="b520a-274">[Analyzing sensor data with Storm and HBase in HDInsight (Hadoop)][hdinsight-sensor-data]</span><span class="sxs-lookup"><span data-stu-id="b520a-274">[Analyzing sensor data with Storm and HBase in HDInsight (Hadoop)][hdinsight-sensor-data]</span></span>

[hdinsight-hbase-geo-replication-vnet]: hdinsight-hbase-geo-replication-configure-vnets.md
[hdinsight-hbase-geo-replication-dns]: ../hdinsight-hbase-geo-replication-configure-VNet.md


[img-vnet-diagram]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hbase-geo-replication/HDInsight.HBase.Replication.Network.diagram.png

[powershell-install]: /powershell/azureps-cmdlets-docs
[hdinsight-hbase-get-started]: hdinsight-hbase-tutorial-get-started-linux.md
[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md
[hdinsight-sensor-data]: hdinsight-storm-sensor-data-analysis.md
[hdinsight-hbase-overview]: hdinsight-hbase-overview.md
[hdinsight-hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md





