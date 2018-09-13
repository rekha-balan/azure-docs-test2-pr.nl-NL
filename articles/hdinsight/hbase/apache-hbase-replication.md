---
title: Set up HBase cluster replication in Azure virtual networks
description: Learn how to set up HBase replication from one HDInsight version to another for load balancing, high availability, zero-downtime migration and updates, and disaster recovery.
services: hdinsight,virtual-network
author: jasonwhowell
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 05/11/2018
ms.author: jasonh
ms.openlocfilehash: e3c4abaf2c06940e2f4102437805b23159eddf16
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968039"
---
# <a name="set-up-hbase-cluster-replication-in-azure-virtual-networks"></a><span data-ttu-id="1a225-103">Set up HBase cluster replication in Azure virtual networks</span><span class="sxs-lookup"><span data-stu-id="1a225-103">Set up HBase cluster replication in Azure virtual networks</span></span>

<span data-ttu-id="1a225-104">Learn how to set up HBase replication within a virtual network, or between two virtual networks in Azure.</span><span class="sxs-lookup"><span data-stu-id="1a225-104">Learn how to set up HBase replication within a virtual network, or between two virtual networks in Azure.</span></span>

<span data-ttu-id="1a225-105">Cluster replication uses a source-push methodology.</span><span class="sxs-lookup"><span data-stu-id="1a225-105">Cluster replication uses a source-push methodology.</span></span> <span data-ttu-id="1a225-106">An HBase cluster can be a source or a destination, or it can fulfill both roles at once.</span><span class="sxs-lookup"><span data-stu-id="1a225-106">An HBase cluster can be a source or a destination, or it can fulfill both roles at once.</span></span> <span data-ttu-id="1a225-107">Replication is asynchronous.</span><span class="sxs-lookup"><span data-stu-id="1a225-107">Replication is asynchronous.</span></span> <span data-ttu-id="1a225-108">The goal of replication is eventual consistency.</span><span class="sxs-lookup"><span data-stu-id="1a225-108">The goal of replication is eventual consistency.</span></span> <span data-ttu-id="1a225-109">When the source receives an edit to a column family when replication is enabled, the edit is propagated to all destination clusters.</span><span class="sxs-lookup"><span data-stu-id="1a225-109">When the source receives an edit to a column family when replication is enabled, the edit is propagated to all destination clusters.</span></span> <span data-ttu-id="1a225-110">When data is replicated from one cluster to another, the source cluster and all clusters that have already consumed the data are tracked, to prevent replication loops.</span><span class="sxs-lookup"><span data-stu-id="1a225-110">When data is replicated from one cluster to another, the source cluster and all clusters that have already consumed the data are tracked, to prevent replication loops.</span></span>

<span data-ttu-id="1a225-111">In this tutorial, you set up a source-destination replication.</span><span class="sxs-lookup"><span data-stu-id="1a225-111">In this tutorial, you set up a source-destination replication.</span></span> <span data-ttu-id="1a225-112">For other cluster topologies, see the [Apache HBase reference guide](http://hbase.apache.org/book.html#_cluster_replication).</span><span class="sxs-lookup"><span data-stu-id="1a225-112">For other cluster topologies, see the [Apache HBase reference guide](http://hbase.apache.org/book.html#_cluster_replication).</span></span>

<span data-ttu-id="1a225-113">The following are HBase replication usage cases for a single virtual network:</span><span class="sxs-lookup"><span data-stu-id="1a225-113">The following are HBase replication usage cases for a single virtual network:</span></span>

* <span data-ttu-id="1a225-114">Load balancing.</span><span class="sxs-lookup"><span data-stu-id="1a225-114">Load balancing.</span></span> <span data-ttu-id="1a225-115">For example, you can run scans or MapReduce jobs on the destination cluster, and ingest data on the source cluster.</span><span class="sxs-lookup"><span data-stu-id="1a225-115">For example, you can run scans or MapReduce jobs on the destination cluster, and ingest data on the source cluster.</span></span>
* <span data-ttu-id="1a225-116">Adding high availability.</span><span class="sxs-lookup"><span data-stu-id="1a225-116">Adding high availability.</span></span>
* <span data-ttu-id="1a225-117">Migrating data from one HBase cluster to another.</span><span class="sxs-lookup"><span data-stu-id="1a225-117">Migrating data from one HBase cluster to another.</span></span>
* <span data-ttu-id="1a225-118">Upgrading an Azure HDInsight cluster from one version to another.</span><span class="sxs-lookup"><span data-stu-id="1a225-118">Upgrading an Azure HDInsight cluster from one version to another.</span></span>

<span data-ttu-id="1a225-119">The following are HBase replication usage cases for two virtual networks:</span><span class="sxs-lookup"><span data-stu-id="1a225-119">The following are HBase replication usage cases for two virtual networks:</span></span>

* <span data-ttu-id="1a225-120">Setting up disaster recovery.</span><span class="sxs-lookup"><span data-stu-id="1a225-120">Setting up disaster recovery.</span></span>
* <span data-ttu-id="1a225-121">Load balancing and partitioning the application.</span><span class="sxs-lookup"><span data-stu-id="1a225-121">Load balancing and partitioning the application.</span></span>
* <span data-ttu-id="1a225-122">Adding high availability.</span><span class="sxs-lookup"><span data-stu-id="1a225-122">Adding high availability.</span></span>

<span data-ttu-id="1a225-123">You can replicate clusters by using [script action](../hdinsight-hadoop-customize-cluster-linux.md) scripts from [GitHub](https://github.com/Azure/hbase-utils/tree/master/replication).</span><span class="sxs-lookup"><span data-stu-id="1a225-123">You can replicate clusters by using [script action](../hdinsight-hadoop-customize-cluster-linux.md) scripts from [GitHub](https://github.com/Azure/hbase-utils/tree/master/replication).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1a225-124">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="1a225-124">Prerequisites</span></span>
<span data-ttu-id="1a225-125">Before you begin this tutorial, you must have an Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="1a225-125">Before you begin this tutorial, you must have an Azure subscription.</span></span> <span data-ttu-id="1a225-126">See [Get an Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="1a225-126">See [Get an Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

## <a name="set-up-the-environments"></a><span data-ttu-id="1a225-127">Set up the environments</span><span class="sxs-lookup"><span data-stu-id="1a225-127">Set up the environments</span></span>

<span data-ttu-id="1a225-128">You have three configuration options:</span><span class="sxs-lookup"><span data-stu-id="1a225-128">You have three configuration options:</span></span>

- <span data-ttu-id="1a225-129">Two HBase clusters in one Azure virtual network.</span><span class="sxs-lookup"><span data-stu-id="1a225-129">Two HBase clusters in one Azure virtual network.</span></span>
- <span data-ttu-id="1a225-130">Two HBase clusters in two different virtual networks in the same region.</span><span class="sxs-lookup"><span data-stu-id="1a225-130">Two HBase clusters in two different virtual networks in the same region.</span></span>
- <span data-ttu-id="1a225-131">Two HBase clusters in two different virtual networks in two different regions (geo-replication).</span><span class="sxs-lookup"><span data-stu-id="1a225-131">Two HBase clusters in two different virtual networks in two different regions (geo-replication).</span></span>

<span data-ttu-id="1a225-132">This article covers the geo-replication scenario.</span><span class="sxs-lookup"><span data-stu-id="1a225-132">This article covers the geo-replication scenario.</span></span>

<span data-ttu-id="1a225-133">To help you set up the environments, we have created some [Azure Resource Manager templates](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1a225-133">To help you set up the environments, we have created some [Azure Resource Manager templates](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="1a225-134">If you prefer to set up the environments by using other methods, see:</span><span class="sxs-lookup"><span data-stu-id="1a225-134">If you prefer to set up the environments by using other methods, see:</span></span>

- [<span data-ttu-id="1a225-135">Create Hadoop clusters in HDInsight</span><span class="sxs-lookup"><span data-stu-id="1a225-135">Create Hadoop clusters in HDInsight</span></span>](../hdinsight-hadoop-provision-linux-clusters.md)
- [<span data-ttu-id="1a225-136">Create HBase clusters in Azure Virtual Network</span><span class="sxs-lookup"><span data-stu-id="1a225-136">Create HBase clusters in Azure Virtual Network</span></span>](apache-hbase-provision-vnet.md)

### <a name="set-up-two-virtual-networks-in-two-different-regions"></a><span data-ttu-id="1a225-137">Set up two virtual networks in two different regions</span><span class="sxs-lookup"><span data-stu-id="1a225-137">Set up two virtual networks in two different regions</span></span>

<span data-ttu-id="1a225-138">To use a template that creates two virtual networks in two different regions and the VPN connection between the VNets, select the following **Deploy to Azure** button.</span><span class="sxs-lookup"><span data-stu-id="1a225-138">To use a template that creates two virtual networks in two different regions and the VPN connection between the VNets, select the following **Deploy to Azure** button.</span></span> <span data-ttu-id="1a225-139">The template definition is stored in a [public blob storage](https://hditutorialdata.blob.core.windows.net/hbaseha/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="1a225-139">The template definition is stored in a [public blob storage](https://hditutorialdata.blob.core.windows.net/hbaseha/azuredeploy.json).</span></span>

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Fhbaseha%2Fazuredeploy.json" target="_blank"><img src="./media/apache-hbase-replication/deploy-to-azure.png" alt="Deploy to Azure"></a>

<span data-ttu-id="1a225-140">Some of the hard-coded values in the template:</span><span class="sxs-lookup"><span data-stu-id="1a225-140">Some of the hard-coded values in the template:</span></span>

<span data-ttu-id="1a225-141">**VNet 1**</span><span class="sxs-lookup"><span data-stu-id="1a225-141">**VNet 1**</span></span>

| <span data-ttu-id="1a225-142">Property</span><span class="sxs-lookup"><span data-stu-id="1a225-142">Property</span></span> | <span data-ttu-id="1a225-143">Value</span><span class="sxs-lookup"><span data-stu-id="1a225-143">Value</span></span> |
|----------|-------|
| <span data-ttu-id="1a225-144">Location</span><span class="sxs-lookup"><span data-stu-id="1a225-144">Location</span></span> | <span data-ttu-id="1a225-145">West US</span><span class="sxs-lookup"><span data-stu-id="1a225-145">West US</span></span> |
| <span data-ttu-id="1a225-146">VNet name</span><span class="sxs-lookup"><span data-stu-id="1a225-146">VNet name</span></span> | <span data-ttu-id="1a225-147">&lt;ClusterNamePrevix>-vnet1</span><span class="sxs-lookup"><span data-stu-id="1a225-147">&lt;ClusterNamePrevix>-vnet1</span></span> |
| <span data-ttu-id="1a225-148">Address space prefix</span><span class="sxs-lookup"><span data-stu-id="1a225-148">Address space prefix</span></span> | <span data-ttu-id="1a225-149">10.1.0.0/16</span><span class="sxs-lookup"><span data-stu-id="1a225-149">10.1.0.0/16</span></span> |
| <span data-ttu-id="1a225-150">Subnet name</span><span class="sxs-lookup"><span data-stu-id="1a225-150">Subnet name</span></span> | <span data-ttu-id="1a225-151">subnet 1</span><span class="sxs-lookup"><span data-stu-id="1a225-151">subnet 1</span></span> |
| <span data-ttu-id="1a225-152">Subnet prefix</span><span class="sxs-lookup"><span data-stu-id="1a225-152">Subnet prefix</span></span> | <span data-ttu-id="1a225-153">10.1.0.0/24</span><span class="sxs-lookup"><span data-stu-id="1a225-153">10.1.0.0/24</span></span> |
| <span data-ttu-id="1a225-154">Subnet (gateway) name</span><span class="sxs-lookup"><span data-stu-id="1a225-154">Subnet (gateway) name</span></span> | <span data-ttu-id="1a225-155">GatewaySubnet (can't be changed)</span><span class="sxs-lookup"><span data-stu-id="1a225-155">GatewaySubnet (can't be changed)</span></span> |
| <span data-ttu-id="1a225-156">Subnet (gateway) prefix</span><span class="sxs-lookup"><span data-stu-id="1a225-156">Subnet (gateway) prefix</span></span> | <span data-ttu-id="1a225-157">10.1.255.0/27</span><span class="sxs-lookup"><span data-stu-id="1a225-157">10.1.255.0/27</span></span> |
| <span data-ttu-id="1a225-158">Gateway name</span><span class="sxs-lookup"><span data-stu-id="1a225-158">Gateway name</span></span> | <span data-ttu-id="1a225-159">vnet1gw</span><span class="sxs-lookup"><span data-stu-id="1a225-159">vnet1gw</span></span> |
| <span data-ttu-id="1a225-160">Gateway type</span><span class="sxs-lookup"><span data-stu-id="1a225-160">Gateway type</span></span> | <span data-ttu-id="1a225-161">Vpn</span><span class="sxs-lookup"><span data-stu-id="1a225-161">Vpn</span></span> |
| <span data-ttu-id="1a225-162">Gateway VPN type</span><span class="sxs-lookup"><span data-stu-id="1a225-162">Gateway VPN type</span></span> | <span data-ttu-id="1a225-163">RouteBased</span><span class="sxs-lookup"><span data-stu-id="1a225-163">RouteBased</span></span> |
| <span data-ttu-id="1a225-164">Gateway SKU</span><span class="sxs-lookup"><span data-stu-id="1a225-164">Gateway SKU</span></span> | <span data-ttu-id="1a225-165">Basic</span><span class="sxs-lookup"><span data-stu-id="1a225-165">Basic</span></span> |
| <span data-ttu-id="1a225-166">Gateway IP</span><span class="sxs-lookup"><span data-stu-id="1a225-166">Gateway IP</span></span> | <span data-ttu-id="1a225-167">vnet1gwip</span><span class="sxs-lookup"><span data-stu-id="1a225-167">vnet1gwip</span></span> |

<span data-ttu-id="1a225-168">**VNet 2**</span><span class="sxs-lookup"><span data-stu-id="1a225-168">**VNet 2**</span></span>

| <span data-ttu-id="1a225-169">Property</span><span class="sxs-lookup"><span data-stu-id="1a225-169">Property</span></span> | <span data-ttu-id="1a225-170">Value</span><span class="sxs-lookup"><span data-stu-id="1a225-170">Value</span></span> |
|----------|-------|
| <span data-ttu-id="1a225-171">Location</span><span class="sxs-lookup"><span data-stu-id="1a225-171">Location</span></span> | <span data-ttu-id="1a225-172">East US</span><span class="sxs-lookup"><span data-stu-id="1a225-172">East US</span></span> |
| <span data-ttu-id="1a225-173">VNet name</span><span class="sxs-lookup"><span data-stu-id="1a225-173">VNet name</span></span> | <span data-ttu-id="1a225-174">&lt;ClusterNamePrevix>-vnet2</span><span class="sxs-lookup"><span data-stu-id="1a225-174">&lt;ClusterNamePrevix>-vnet2</span></span> |
| <span data-ttu-id="1a225-175">Address space prefix</span><span class="sxs-lookup"><span data-stu-id="1a225-175">Address space prefix</span></span> | <span data-ttu-id="1a225-176">10.2.0.0/16</span><span class="sxs-lookup"><span data-stu-id="1a225-176">10.2.0.0/16</span></span> |
| <span data-ttu-id="1a225-177">Subnet name</span><span class="sxs-lookup"><span data-stu-id="1a225-177">Subnet name</span></span> | <span data-ttu-id="1a225-178">subnet 1</span><span class="sxs-lookup"><span data-stu-id="1a225-178">subnet 1</span></span> |
| <span data-ttu-id="1a225-179">Subnet prefix</span><span class="sxs-lookup"><span data-stu-id="1a225-179">Subnet prefix</span></span> | <span data-ttu-id="1a225-180">10.2.0.0/24</span><span class="sxs-lookup"><span data-stu-id="1a225-180">10.2.0.0/24</span></span> |
| <span data-ttu-id="1a225-181">Subnet (gateway) name</span><span class="sxs-lookup"><span data-stu-id="1a225-181">Subnet (gateway) name</span></span> | <span data-ttu-id="1a225-182">GatewaySubnet (can't be changed)</span><span class="sxs-lookup"><span data-stu-id="1a225-182">GatewaySubnet (can't be changed)</span></span> |
| <span data-ttu-id="1a225-183">Subnet (gateway) prefix</span><span class="sxs-lookup"><span data-stu-id="1a225-183">Subnet (gateway) prefix</span></span> | <span data-ttu-id="1a225-184">10.2.255.0/27</span><span class="sxs-lookup"><span data-stu-id="1a225-184">10.2.255.0/27</span></span> |
| <span data-ttu-id="1a225-185">Gateway name</span><span class="sxs-lookup"><span data-stu-id="1a225-185">Gateway name</span></span> | <span data-ttu-id="1a225-186">vnet2gw</span><span class="sxs-lookup"><span data-stu-id="1a225-186">vnet2gw</span></span> |
| <span data-ttu-id="1a225-187">Gateway type</span><span class="sxs-lookup"><span data-stu-id="1a225-187">Gateway type</span></span> | <span data-ttu-id="1a225-188">Vpn</span><span class="sxs-lookup"><span data-stu-id="1a225-188">Vpn</span></span> |
| <span data-ttu-id="1a225-189">Gateway VPN type</span><span class="sxs-lookup"><span data-stu-id="1a225-189">Gateway VPN type</span></span> | <span data-ttu-id="1a225-190">RouteBased</span><span class="sxs-lookup"><span data-stu-id="1a225-190">RouteBased</span></span> |
| <span data-ttu-id="1a225-191">Gateway SKU</span><span class="sxs-lookup"><span data-stu-id="1a225-191">Gateway SKU</span></span> | <span data-ttu-id="1a225-192">Basic</span><span class="sxs-lookup"><span data-stu-id="1a225-192">Basic</span></span> |
| <span data-ttu-id="1a225-193">Gateway IP</span><span class="sxs-lookup"><span data-stu-id="1a225-193">Gateway IP</span></span> | <span data-ttu-id="1a225-194">vnet1gwip</span><span class="sxs-lookup"><span data-stu-id="1a225-194">vnet1gwip</span></span> |

## <a name="setup-dns"></a><span data-ttu-id="1a225-195">Setup DNS</span><span class="sxs-lookup"><span data-stu-id="1a225-195">Setup DNS</span></span>

<span data-ttu-id="1a225-196">In the last section, the template creates an Ubuntu virtual machine in each of the two virtual networks.</span><span class="sxs-lookup"><span data-stu-id="1a225-196">In the last section, the template creates an Ubuntu virtual machine in each of the two virtual networks.</span></span>  <span data-ttu-id="1a225-197">In this section, you install Bind on the two DNS virtual machines, and then configure the DNS forwarding on the two virtual machines.</span><span class="sxs-lookup"><span data-stu-id="1a225-197">In this section, you install Bind on the two DNS virtual machines, and then configure the DNS forwarding on the two virtual machines.</span></span>

<span data-ttu-id="1a225-198">To install Bind, yon need to find the public IP address of the two DNS virtual machines.</span><span class="sxs-lookup"><span data-stu-id="1a225-198">To install Bind, yon need to find the public IP address of the two DNS virtual machines.</span></span>

1. <span data-ttu-id="1a225-199">Open the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1a225-199">Open the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="1a225-200">Open the DNS virtual machine by selecting **Resources groups > [resource group name] > [vnet1DNS]**.</span><span class="sxs-lookup"><span data-stu-id="1a225-200">Open the DNS virtual machine by selecting **Resources groups > [resource group name] > [vnet1DNS]**.</span></span>  <span data-ttu-id="1a225-201">The resource group name is the one you create in the last procedure.</span><span class="sxs-lookup"><span data-stu-id="1a225-201">The resource group name is the one you create in the last procedure.</span></span> <span data-ttu-id="1a225-202">The default DNS virtual machine names are *vnet1DNS* and *vnet2NDS*.</span><span class="sxs-lookup"><span data-stu-id="1a225-202">The default DNS virtual machine names are *vnet1DNS* and *vnet2NDS*.</span></span>
3. <span data-ttu-id="1a225-203">Select **Properties** to open the properties page of the virtual network.</span><span class="sxs-lookup"><span data-stu-id="1a225-203">Select **Properties** to open the properties page of the virtual network.</span></span>
4. <span data-ttu-id="1a225-204">Write down the **Public IP address**, and also verify the **Private IP address**.</span><span class="sxs-lookup"><span data-stu-id="1a225-204">Write down the **Public IP address**, and also verify the **Private IP address**.</span></span>  <span data-ttu-id="1a225-205">The private IP address shall be **10.1.0.4** for vnet1DNS and **10.2.0.4** for vnet2DNS.</span><span class="sxs-lookup"><span data-stu-id="1a225-205">The private IP address shall be **10.1.0.4** for vnet1DNS and **10.2.0.4** for vnet2DNS.</span></span>  

<span data-ttu-id="1a225-206">To install Bind, use the following procedure:</span><span class="sxs-lookup"><span data-stu-id="1a225-206">To install Bind, use the following procedure:</span></span>

1. <span data-ttu-id="1a225-207">Use SSH to connect to the __public IP address__ of the DNS virtual machine.</span><span class="sxs-lookup"><span data-stu-id="1a225-207">Use SSH to connect to the __public IP address__ of the DNS virtual machine.</span></span> <span data-ttu-id="1a225-208">The following example connects to a virtual machine at 40.68.254.142:</span><span class="sxs-lookup"><span data-stu-id="1a225-208">The following example connects to a virtual machine at 40.68.254.142:</span></span>

    ```bash
    ssh sshuser@40.68.254.142
    ```

    <span data-ttu-id="1a225-209">Replace `sshuser` with the SSH user account you specified when creating the DNS virtual machine.</span><span class="sxs-lookup"><span data-stu-id="1a225-209">Replace `sshuser` with the SSH user account you specified when creating the DNS virtual machine.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1a225-210">There are a variety of ways to obtain the `ssh` utility.</span><span class="sxs-lookup"><span data-stu-id="1a225-210">There are a variety of ways to obtain the `ssh` utility.</span></span> <span data-ttu-id="1a225-211">On Linux, Unix, and macOS, it is provided as part of the operating system.</span><span class="sxs-lookup"><span data-stu-id="1a225-211">On Linux, Unix, and macOS, it is provided as part of the operating system.</span></span> <span data-ttu-id="1a225-212">If you are using Windows, consider one of the following options:</span><span class="sxs-lookup"><span data-stu-id="1a225-212">If you are using Windows, consider one of the following options:</span></span>
    >
    > * [<span data-ttu-id="1a225-213">Azure Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="1a225-213">Azure Cloud Shell</span></span>](../../cloud-shell/quickstart.md)
    > * [<span data-ttu-id="1a225-214">Bash on Ubuntu on Windows 10</span><span class="sxs-lookup"><span data-stu-id="1a225-214">Bash on Ubuntu on Windows 10</span></span>](https://msdn.microsoft.com/commandline/wsl/about)
    > * [<span data-ttu-id="1a225-215">Git (https://git-scm.com/)</span><span class="sxs-lookup"><span data-stu-id="1a225-215">Git (https://git-scm.com/)</span></span>](https://git-scm.com/)
    > * [<span data-ttu-id="1a225-216">OpenSSH (https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)</span><span class="sxs-lookup"><span data-stu-id="1a225-216">OpenSSH (https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)</span></span>](https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)

2. <span data-ttu-id="1a225-217">To install Bind, use the following commands from the SSH session:</span><span class="sxs-lookup"><span data-stu-id="1a225-217">To install Bind, use the following commands from the SSH session:</span></span>

    ```bash
    sudo apt-get update -y
    sudo apt-get install bind9 -y
    ```

3. <span data-ttu-id="1a225-218">To configure Bind to forward name resolution requests to your on-prem DNS server, use the following text as the contents of the `/etc/bind/named.conf.options` file:</span><span class="sxs-lookup"><span data-stu-id="1a225-218">To configure Bind to forward name resolution requests to your on-prem DNS server, use the following text as the contents of the `/etc/bind/named.conf.options` file:</span></span>

    ```
    acl goodclients {
        10.1.0.0/16; # Replace with the IP address range of the virtual network 1
        10.2.0.0/16; # Replace with the IP address range of the virtual network 2
        localhost;
        localhost;
    };
    
    options {
        directory "/var/cache/bind";
        recursion yes;
        allow-query { goodclients; };

        forwarders {
            168.63.129.16 #This is the Azure DNS server
        };

        dnssec-validation auto;

        auth-nxdomain no;    # conform to RFC1035
        listen-on-v6 { any; };
    };
    ```
    
    > [!IMPORTANT]
    > <span data-ttu-id="1a225-219">Replace the values in the `goodclients` section with the IP address range of the two virtual networks.</span><span class="sxs-lookup"><span data-stu-id="1a225-219">Replace the values in the `goodclients` section with the IP address range of the two virtual networks.</span></span> <span data-ttu-id="1a225-220">This section defines the addresses that this DNS server accepts requests from.</span><span class="sxs-lookup"><span data-stu-id="1a225-220">This section defines the addresses that this DNS server accepts requests from.</span></span>

    <span data-ttu-id="1a225-221">To edit this file, use the following command:</span><span class="sxs-lookup"><span data-stu-id="1a225-221">To edit this file, use the following command:</span></span>

    ```bash
    sudo nano /etc/bind/named.conf.options
    ```

    <span data-ttu-id="1a225-222">To save the file, use __Ctrl+X__, __Y__, and then __Enter__.</span><span class="sxs-lookup"><span data-stu-id="1a225-222">To save the file, use __Ctrl+X__, __Y__, and then __Enter__.</span></span>

4. <span data-ttu-id="1a225-223">From the SSH session, use the following command:</span><span class="sxs-lookup"><span data-stu-id="1a225-223">From the SSH session, use the following command:</span></span>

    ```bash
    hostname -f
    ```

    <span data-ttu-id="1a225-224">This command returns a value similar to the following text:</span><span class="sxs-lookup"><span data-stu-id="1a225-224">This command returns a value similar to the following text:</span></span>

        vnet1DNS.icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net

    <span data-ttu-id="1a225-225">The `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` text is the __DNS suffix__ for this virtual network.</span><span class="sxs-lookup"><span data-stu-id="1a225-225">The `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` text is the __DNS suffix__ for this virtual network.</span></span> <span data-ttu-id="1a225-226">Save this value, as it is used later.</span><span class="sxs-lookup"><span data-stu-id="1a225-226">Save this value, as it is used later.</span></span>

    <span data-ttu-id="1a225-227">You must also find out the DNS suffix from the other DNS server.</span><span class="sxs-lookup"><span data-stu-id="1a225-227">You must also find out the DNS suffix from the other DNS server.</span></span> <span data-ttu-id="1a225-228">You need it in the next step.</span><span class="sxs-lookup"><span data-stu-id="1a225-228">You need it in the next step.</span></span>

5. <span data-ttu-id="1a225-229">To configure Bind to resolve DNS names for resources within the virtual network, use the following text as the contents of the `/etc/bind/named.conf.local` file:</span><span class="sxs-lookup"><span data-stu-id="1a225-229">To configure Bind to resolve DNS names for resources within the virtual network, use the following text as the contents of the `/etc/bind/named.conf.local` file:</span></span>

    ```
    // Replace the following with the DNS suffix for your virtual network
    zone "v5ant3az2hbe1edzthhvwwkcse.bx.internal.cloudapp.net" {
            type forward;
            forwarders {10.2.0.4;}; # The Azure recursive resolver
    };
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="1a225-230">You must replace the `v5ant3az2hbe1edzthhvwwkcse.bx.internal.cloudapp.net` with the DNS suffix of the other virtual network.</span><span class="sxs-lookup"><span data-stu-id="1a225-230">You must replace the `v5ant3az2hbe1edzthhvwwkcse.bx.internal.cloudapp.net` with the DNS suffix of the other virtual network.</span></span> <span data-ttu-id="1a225-231">And the forwarder IP is the private IP address of the DNS server in the other virtual network.</span><span class="sxs-lookup"><span data-stu-id="1a225-231">And the forwarder IP is the private IP address of the DNS server in the other virtual network.</span></span>

    <span data-ttu-id="1a225-232">To edit this file, use the following command:</span><span class="sxs-lookup"><span data-stu-id="1a225-232">To edit this file, use the following command:</span></span>

    ```bash
    sudo nano /etc/bind/named.conf.local
    ```

    <span data-ttu-id="1a225-233">To save the file, use __Ctrl+X__, __Y__, and then __Enter__.</span><span class="sxs-lookup"><span data-stu-id="1a225-233">To save the file, use __Ctrl+X__, __Y__, and then __Enter__.</span></span>

6. <span data-ttu-id="1a225-234">To start Bind, use the following command:</span><span class="sxs-lookup"><span data-stu-id="1a225-234">To start Bind, use the following command:</span></span>

    ```bash
    sudo service bind9 restart
    ```

7. <span data-ttu-id="1a225-235">To verify that bind can resolve the names of resources in the other virtual network, use the following commands:</span><span class="sxs-lookup"><span data-stu-id="1a225-235">To verify that bind can resolve the names of resources in the other virtual network, use the following commands:</span></span>

    ```bash
    sudo apt install dnsutils
    nslookup vnet2dns.v5ant3az2hbe1edzthhvwwkcse.bx.internal.cloudapp.net 10.2.0.4
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="1a225-236">Replace `vnet2dns.v5ant3az2hbe1edzthhvwwkcse.bx.internal.cloudapp.net` with the fully qualified domain name (FQDN) of the DNS virtual machine in the other network.</span><span class="sxs-lookup"><span data-stu-id="1a225-236">Replace `vnet2dns.v5ant3az2hbe1edzthhvwwkcse.bx.internal.cloudapp.net` with the fully qualified domain name (FQDN) of the DNS virtual machine in the other network.</span></span>
    >
    > <span data-ttu-id="1a225-237">Replace `10.2.0.4` with the __internal IP address__ of your custom DNS server in the other virtual network.</span><span class="sxs-lookup"><span data-stu-id="1a225-237">Replace `10.2.0.4` with the __internal IP address__ of your custom DNS server in the other virtual network.</span></span>

    <span data-ttu-id="1a225-238">The response appears similar to the following text:</span><span class="sxs-lookup"><span data-stu-id="1a225-238">The response appears similar to the following text:</span></span>

    ```
    Server:         10.2.0.4
    Address:        10.2.0.4#53
    
    Non-authoritative answer:
    Name:   vnet2dns.v5ant3az2hbe1edzthhvwwkcse.bx.internal.cloudapp.net
    Address: 10.2.0.4
    ```

    <span data-ttu-id="1a225-239">Until now, you cannot look up the IP address from the other network without specified DNS server IP address.</span><span class="sxs-lookup"><span data-stu-id="1a225-239">Until now, you cannot look up the IP address from the other network without specified DNS server IP address.</span></span>

### <a name="configure-the-virtual-network-to-use-the-custom-dns-server"></a><span data-ttu-id="1a225-240">Configure the virtual network to use the custom DNS server</span><span class="sxs-lookup"><span data-stu-id="1a225-240">Configure the virtual network to use the custom DNS server</span></span>

<span data-ttu-id="1a225-241">To configure the virtual network to use the custom DNS server instead of the Azure recursive resolver, use the following steps:</span><span class="sxs-lookup"><span data-stu-id="1a225-241">To configure the virtual network to use the custom DNS server instead of the Azure recursive resolver, use the following steps:</span></span>

1. <span data-ttu-id="1a225-242">In the [Azure portal](https://portal.azure.com), select the virtual network, and then select __DNS Servers__.</span><span class="sxs-lookup"><span data-stu-id="1a225-242">In the [Azure portal](https://portal.azure.com), select the virtual network, and then select __DNS Servers__.</span></span>

2. <span data-ttu-id="1a225-243">Select __Custom__, and enter the __internal IP address__ of the custom DNS server.</span><span class="sxs-lookup"><span data-stu-id="1a225-243">Select __Custom__, and enter the __internal IP address__ of the custom DNS server.</span></span> <span data-ttu-id="1a225-244">Finally, select __Save__.</span><span class="sxs-lookup"><span data-stu-id="1a225-244">Finally, select __Save__.</span></span>

6. <span data-ttu-id="1a225-245">Open the DNS server virtual machine in vnet1, and click **Restart**.</span><span class="sxs-lookup"><span data-stu-id="1a225-245">Open the DNS server virtual machine in vnet1, and click **Restart**.</span></span>  <span data-ttu-id="1a225-246">You must restart all the virtual machines in the virtual network to make the DNS configuration to take effect.</span><span class="sxs-lookup"><span data-stu-id="1a225-246">You must restart all the virtual machines in the virtual network to make the DNS configuration to take effect.</span></span>
7. <span data-ttu-id="1a225-247">Repeat steps configure the custom DNS server for vnet2.</span><span class="sxs-lookup"><span data-stu-id="1a225-247">Repeat steps configure the custom DNS server for vnet2.</span></span>

<span data-ttu-id="1a225-248">To test the DNS configuration, you can connect to the two DNS virtual machines using SSH, and ping the DNS server of the other virtual network by using its host name.</span><span class="sxs-lookup"><span data-stu-id="1a225-248">To test the DNS configuration, you can connect to the two DNS virtual machines using SSH, and ping the DNS server of the other virtual network by using its host name.</span></span> <span data-ttu-id="1a225-249">If it doesn't work, use the following command to check DNS status:</span><span class="sxs-lookup"><span data-stu-id="1a225-249">If it doesn't work, use the following command to check DNS status:</span></span>

```bash
sudo service bind9 status
```

## <a name="create-hbase-clusters"></a><span data-ttu-id="1a225-250">Create HBase clusters</span><span class="sxs-lookup"><span data-stu-id="1a225-250">Create HBase clusters</span></span>

<span data-ttu-id="1a225-251">Create an HBase cluster in each of the two virtual networks with the following configuration:</span><span class="sxs-lookup"><span data-stu-id="1a225-251">Create an HBase cluster in each of the two virtual networks with the following configuration:</span></span>

- <span data-ttu-id="1a225-252">**Resource group name**: use the same resource group name as you created the virtual networks.</span><span class="sxs-lookup"><span data-stu-id="1a225-252">**Resource group name**: use the same resource group name as you created the virtual networks.</span></span>
- <span data-ttu-id="1a225-253">**Cluster type**: HBase</span><span class="sxs-lookup"><span data-stu-id="1a225-253">**Cluster type**: HBase</span></span>
- <span data-ttu-id="1a225-254">**Version**: HBase 1.1.2 (HDI 3.6)</span><span class="sxs-lookup"><span data-stu-id="1a225-254">**Version**: HBase 1.1.2 (HDI 3.6)</span></span>
- <span data-ttu-id="1a225-255">**Location**: Use the same location as the virtual network.</span><span class="sxs-lookup"><span data-stu-id="1a225-255">**Location**: Use the same location as the virtual network.</span></span>  <span data-ttu-id="1a225-256">By default, vnet1 is *West US*, and vnet2 is *East US*.</span><span class="sxs-lookup"><span data-stu-id="1a225-256">By default, vnet1 is *West US*, and vnet2 is *East US*.</span></span>
- <span data-ttu-id="1a225-257">**Storage**: Create a new storage account for the cluster.</span><span class="sxs-lookup"><span data-stu-id="1a225-257">**Storage**: Create a new storage account for the cluster.</span></span>
- <span data-ttu-id="1a225-258">**Virtual network** (from Advanced settings on the portal): Select vnet1 you created in the last procedure.</span><span class="sxs-lookup"><span data-stu-id="1a225-258">**Virtual network** (from Advanced settings on the portal): Select vnet1 you created in the last procedure.</span></span>
- <span data-ttu-id="1a225-259">**Subnet**: The default name used in the template is **subnet1**.</span><span class="sxs-lookup"><span data-stu-id="1a225-259">**Subnet**: The default name used in the template is **subnet1**.</span></span>

<span data-ttu-id="1a225-260">To ensure the environment is configured correctly, you must be able to ping the headnode's FQDN between the two clusters.</span><span class="sxs-lookup"><span data-stu-id="1a225-260">To ensure the environment is configured correctly, you must be able to ping the headnode's FQDN between the two clusters.</span></span>

## <a name="load-test-data"></a><span data-ttu-id="1a225-261">Load test data</span><span class="sxs-lookup"><span data-stu-id="1a225-261">Load test data</span></span>

<span data-ttu-id="1a225-262">When you replicate a cluster, you must specify the tables that you want to replicate.</span><span class="sxs-lookup"><span data-stu-id="1a225-262">When you replicate a cluster, you must specify the tables that you want to replicate.</span></span> <span data-ttu-id="1a225-263">In this section, you load some data into the source cluster.</span><span class="sxs-lookup"><span data-stu-id="1a225-263">In this section, you load some data into the source cluster.</span></span> <span data-ttu-id="1a225-264">In the next section, you will enable replication between the two clusters.</span><span class="sxs-lookup"><span data-stu-id="1a225-264">In the next section, you will enable replication between the two clusters.</span></span>

<span data-ttu-id="1a225-265">To create a **Contacts** table and insert some data in the table, follow the instructions at [HBase tutorial: Get started using Apache HBase in HDInsight](apache-hbase-tutorial-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="1a225-265">To create a **Contacts** table and insert some data in the table, follow the instructions at [HBase tutorial: Get started using Apache HBase in HDInsight](apache-hbase-tutorial-get-started-linux.md).</span></span>

## <a name="enable-replication"></a><span data-ttu-id="1a225-266">Enable replication</span><span class="sxs-lookup"><span data-stu-id="1a225-266">Enable replication</span></span>

<span data-ttu-id="1a225-267">The following steps describe how to call the script action script from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="1a225-267">The following steps describe how to call the script action script from the Azure portal.</span></span> <span data-ttu-id="1a225-268">For information about running a script action by using Azure PowerShell and the Azure command-line tool (Azure CLI), see [Customize HDInsight clusters by using script action](../hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="1a225-268">For information about running a script action by using Azure PowerShell and the Azure command-line tool (Azure CLI), see [Customize HDInsight clusters by using script action](../hdinsight-hadoop-customize-cluster-linux.md).</span></span>

<span data-ttu-id="1a225-269">**To enable HBase replication from the Azure portal**</span><span class="sxs-lookup"><span data-stu-id="1a225-269">**To enable HBase replication from the Azure portal**</span></span>

1. <span data-ttu-id="1a225-270">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1a225-270">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="1a225-271">Open the source HBase cluster.</span><span class="sxs-lookup"><span data-stu-id="1a225-271">Open the source HBase cluster.</span></span>
3. <span data-ttu-id="1a225-272">In the cluster menu, select **Script Actions**.</span><span class="sxs-lookup"><span data-stu-id="1a225-272">In the cluster menu, select **Script Actions**.</span></span>
4. <span data-ttu-id="1a225-273">At the top of the page, select **Submit New**.</span><span class="sxs-lookup"><span data-stu-id="1a225-273">At the top of the page, select **Submit New**.</span></span>
5. <span data-ttu-id="1a225-274">Select or enter the following information:</span><span class="sxs-lookup"><span data-stu-id="1a225-274">Select or enter the following information:</span></span>

  1. <span data-ttu-id="1a225-275">**Name**: Enter **Enable replication**.</span><span class="sxs-lookup"><span data-stu-id="1a225-275">**Name**: Enter **Enable replication**.</span></span>
  2. <span data-ttu-id="1a225-276">**Bash Script URL**: Enter **https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_enable_replication.sh**.</span><span class="sxs-lookup"><span data-stu-id="1a225-276">**Bash Script URL**: Enter **https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_enable_replication.sh**.</span></span>
  3.  <span data-ttu-id="1a225-277">**Head**: Ensure this is selected.</span><span class="sxs-lookup"><span data-stu-id="1a225-277">**Head**: Ensure this is selected.</span></span> <span data-ttu-id="1a225-278">Clear the other node types.</span><span class="sxs-lookup"><span data-stu-id="1a225-278">Clear the other node types.</span></span>
  4. <span data-ttu-id="1a225-279">**Parameters**: The following sample parameters enable replication for all existing tables, and then copy all data from the source cluster to the destination cluster:</span><span class="sxs-lookup"><span data-stu-id="1a225-279">**Parameters**: The following sample parameters enable replication for all existing tables, and then copy all data from the source cluster to the destination cluster:</span></span>

          -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -copydata
    
    >[!note]
    >
    > <span data-ttu-id="1a225-280">Use hostname instead of FQDN for both the source and destination cluster DNS name.</span><span class="sxs-lookup"><span data-stu-id="1a225-280">Use hostname instead of FQDN for both the source and destination cluster DNS name.</span></span>

6. <span data-ttu-id="1a225-281">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="1a225-281">Select **Create**.</span></span> <span data-ttu-id="1a225-282">The script can take a while to run, especially when you use the **-copydata** argument.</span><span class="sxs-lookup"><span data-stu-id="1a225-282">The script can take a while to run, especially when you use the **-copydata** argument.</span></span>

<span data-ttu-id="1a225-283">Required arguments:</span><span class="sxs-lookup"><span data-stu-id="1a225-283">Required arguments:</span></span>

|<span data-ttu-id="1a225-284">Name</span><span class="sxs-lookup"><span data-stu-id="1a225-284">Name</span></span>|<span data-ttu-id="1a225-285">Description</span><span class="sxs-lookup"><span data-stu-id="1a225-285">Description</span></span>|
|----|-----------|
|<span data-ttu-id="1a225-286">-s, --src-cluster</span><span class="sxs-lookup"><span data-stu-id="1a225-286">-s, --src-cluster</span></span> | <span data-ttu-id="1a225-287">Specifies the DNS name of the source HBase cluster.</span><span class="sxs-lookup"><span data-stu-id="1a225-287">Specifies the DNS name of the source HBase cluster.</span></span> <span data-ttu-id="1a225-288">For example: -s hbsrccluster, --src-cluster=hbsrccluster</span><span class="sxs-lookup"><span data-stu-id="1a225-288">For example: -s hbsrccluster, --src-cluster=hbsrccluster</span></span> |
|<span data-ttu-id="1a225-289">-d, --dst-cluster</span><span class="sxs-lookup"><span data-stu-id="1a225-289">-d, --dst-cluster</span></span> | <span data-ttu-id="1a225-290">Specifies the DNS name of the destination (replica) HBase cluster.</span><span class="sxs-lookup"><span data-stu-id="1a225-290">Specifies the DNS name of the destination (replica) HBase cluster.</span></span> <span data-ttu-id="1a225-291">For example: -s dsthbcluster, --src-cluster=dsthbcluster</span><span class="sxs-lookup"><span data-stu-id="1a225-291">For example: -s dsthbcluster, --src-cluster=dsthbcluster</span></span> |
|<span data-ttu-id="1a225-292">-sp, --src-ambari-password</span><span class="sxs-lookup"><span data-stu-id="1a225-292">-sp, --src-ambari-password</span></span> | <span data-ttu-id="1a225-293">Specifies the admin password for Ambari on the source HBase cluster.</span><span class="sxs-lookup"><span data-stu-id="1a225-293">Specifies the admin password for Ambari on the source HBase cluster.</span></span> |
|<span data-ttu-id="1a225-294">-dp, --dst-ambari-password</span><span class="sxs-lookup"><span data-stu-id="1a225-294">-dp, --dst-ambari-password</span></span> | <span data-ttu-id="1a225-295">Specifies the admin password for Ambari on the destination HBase cluster.</span><span class="sxs-lookup"><span data-stu-id="1a225-295">Specifies the admin password for Ambari on the destination HBase cluster.</span></span>|

<span data-ttu-id="1a225-296">Optional arguments:</span><span class="sxs-lookup"><span data-stu-id="1a225-296">Optional arguments:</span></span>

|<span data-ttu-id="1a225-297">Name</span><span class="sxs-lookup"><span data-stu-id="1a225-297">Name</span></span>|<span data-ttu-id="1a225-298">Description</span><span class="sxs-lookup"><span data-stu-id="1a225-298">Description</span></span>|
|----|-----------|
|<span data-ttu-id="1a225-299">-su, --src-ambari-user</span><span class="sxs-lookup"><span data-stu-id="1a225-299">-su, --src-ambari-user</span></span> | <span data-ttu-id="1a225-300">Specifies the admin user name for Ambari on the source HBase cluster.</span><span class="sxs-lookup"><span data-stu-id="1a225-300">Specifies the admin user name for Ambari on the source HBase cluster.</span></span> <span data-ttu-id="1a225-301">The default value is **admin**.</span><span class="sxs-lookup"><span data-stu-id="1a225-301">The default value is **admin**.</span></span> |
|<span data-ttu-id="1a225-302">-du, --dst-ambari-user</span><span class="sxs-lookup"><span data-stu-id="1a225-302">-du, --dst-ambari-user</span></span> | <span data-ttu-id="1a225-303">Specifies the admin user name for Ambari on the destination HBase cluster.</span><span class="sxs-lookup"><span data-stu-id="1a225-303">Specifies the admin user name for Ambari on the destination HBase cluster.</span></span> <span data-ttu-id="1a225-304">The default value is **admin**.</span><span class="sxs-lookup"><span data-stu-id="1a225-304">The default value is **admin**.</span></span> |
|<span data-ttu-id="1a225-305">-t, --table-list</span><span class="sxs-lookup"><span data-stu-id="1a225-305">-t, --table-list</span></span> | <span data-ttu-id="1a225-306">Specifies the tables to be replicated.</span><span class="sxs-lookup"><span data-stu-id="1a225-306">Specifies the tables to be replicated.</span></span> <span data-ttu-id="1a225-307">For example: --table-list="table1;table2;table3".</span><span class="sxs-lookup"><span data-stu-id="1a225-307">For example: --table-list="table1;table2;table3".</span></span> <span data-ttu-id="1a225-308">If you don't specify tables, all existing HBase tables are replicated.</span><span class="sxs-lookup"><span data-stu-id="1a225-308">If you don't specify tables, all existing HBase tables are replicated.</span></span>|
|<span data-ttu-id="1a225-309">-m, --machine</span><span class="sxs-lookup"><span data-stu-id="1a225-309">-m, --machine</span></span> | <span data-ttu-id="1a225-310">Specifies the head node where the script action runs.</span><span class="sxs-lookup"><span data-stu-id="1a225-310">Specifies the head node where the script action runs.</span></span> <span data-ttu-id="1a225-311">The value is either **hn1** or **hn0**.</span><span class="sxs-lookup"><span data-stu-id="1a225-311">The value is either **hn1** or **hn0**.</span></span> <span data-ttu-id="1a225-312">Because the **hn0** head node typically is busier, we recommend using **hn1**.</span><span class="sxs-lookup"><span data-stu-id="1a225-312">Because the **hn0** head node typically is busier, we recommend using **hn1**.</span></span> <span data-ttu-id="1a225-313">Use this option when you're running the $0 script as a script action from the HDInsight portal or Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1a225-313">Use this option when you're running the $0 script as a script action from the HDInsight portal or Azure PowerShell.</span></span>|
|<span data-ttu-id="1a225-314">-cp, -copydata</span><span class="sxs-lookup"><span data-stu-id="1a225-314">-cp, -copydata</span></span> | <span data-ttu-id="1a225-315">Enables the migration of existing data on the tables where replication is enabled.</span><span class="sxs-lookup"><span data-stu-id="1a225-315">Enables the migration of existing data on the tables where replication is enabled.</span></span> |
|<span data-ttu-id="1a225-316">-rpm, -replicate-phoenix-meta</span><span class="sxs-lookup"><span data-stu-id="1a225-316">-rpm, -replicate-phoenix-meta</span></span> | <span data-ttu-id="1a225-317">Enables replication on Phoenix system tables.</span><span class="sxs-lookup"><span data-stu-id="1a225-317">Enables replication on Phoenix system tables.</span></span> <br><br><span data-ttu-id="1a225-318">*Use this option with caution.*</span><span class="sxs-lookup"><span data-stu-id="1a225-318">*Use this option with caution.*</span></span> <span data-ttu-id="1a225-319">We recommend that you re-create Phoenix tables on replica clusters before you use this script.</span><span class="sxs-lookup"><span data-stu-id="1a225-319">We recommend that you re-create Phoenix tables on replica clusters before you use this script.</span></span> |
|<span data-ttu-id="1a225-320">-h, --help</span><span class="sxs-lookup"><span data-stu-id="1a225-320">-h, --help</span></span> | <span data-ttu-id="1a225-321">Displays usage information.</span><span class="sxs-lookup"><span data-stu-id="1a225-321">Displays usage information.</span></span> |

<span data-ttu-id="1a225-322">The `print_usage()` section of the [script](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_enable_replication.sh) has a detailed explanation of parameters.</span><span class="sxs-lookup"><span data-stu-id="1a225-322">The `print_usage()` section of the [script](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_enable_replication.sh) has a detailed explanation of parameters.</span></span>

<span data-ttu-id="1a225-323">After the script action is successfully deployed, you can use SSH to connect to the destination HBase cluster, and then verify that the data has been replicated.</span><span class="sxs-lookup"><span data-stu-id="1a225-323">After the script action is successfully deployed, you can use SSH to connect to the destination HBase cluster, and then verify that the data has been replicated.</span></span>

### <a name="replication-scenarios"></a><span data-ttu-id="1a225-324">Replication scenarios</span><span class="sxs-lookup"><span data-stu-id="1a225-324">Replication scenarios</span></span>

<span data-ttu-id="1a225-325">The following list shows you some general usage cases and their parameter settings:</span><span class="sxs-lookup"><span data-stu-id="1a225-325">The following list shows you some general usage cases and their parameter settings:</span></span>

- <span data-ttu-id="1a225-326">**Enable replication on all tables between the two clusters**.</span><span class="sxs-lookup"><span data-stu-id="1a225-326">**Enable replication on all tables between the two clusters**.</span></span> <span data-ttu-id="1a225-327">This scenario does not require copying or migrating existing data in the tables, and it does not use Phoenix tables.</span><span class="sxs-lookup"><span data-stu-id="1a225-327">This scenario does not require copying or migrating existing data in the tables, and it does not use Phoenix tables.</span></span> <span data-ttu-id="1a225-328">Use the following parameters:</span><span class="sxs-lookup"><span data-stu-id="1a225-328">Use the following parameters:</span></span>

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password>  

- <span data-ttu-id="1a225-329">**Enable replication on specific tables**.</span><span class="sxs-lookup"><span data-stu-id="1a225-329">**Enable replication on specific tables**.</span></span> <span data-ttu-id="1a225-330">To enable replication on table1, table2, and table3, use the following parameters:</span><span class="sxs-lookup"><span data-stu-id="1a225-330">To enable replication on table1, table2, and table3, use the following parameters:</span></span>

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3"

- <span data-ttu-id="1a225-331">**Enable replication on specific tables, and copy the existing data**.</span><span class="sxs-lookup"><span data-stu-id="1a225-331">**Enable replication on specific tables, and copy the existing data**.</span></span> <span data-ttu-id="1a225-332">To enable replication on table1, table2, and table3, use the following parameters:</span><span class="sxs-lookup"><span data-stu-id="1a225-332">To enable replication on table1, table2, and table3, use the following parameters:</span></span>

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3" -copydata

- <span data-ttu-id="1a225-333">**Enable replication on all tables, and replicate Phoenix metadata from source to destination**.</span><span class="sxs-lookup"><span data-stu-id="1a225-333">**Enable replication on all tables, and replicate Phoenix metadata from source to destination**.</span></span> <span data-ttu-id="1a225-334">Phoenix metadata replication is not perfect.</span><span class="sxs-lookup"><span data-stu-id="1a225-334">Phoenix metadata replication is not perfect.</span></span> <span data-ttu-id="1a225-335">Use it with caution.</span><span class="sxs-lookup"><span data-stu-id="1a225-335">Use it with caution.</span></span> <span data-ttu-id="1a225-336">Use the following parameters:</span><span class="sxs-lookup"><span data-stu-id="1a225-336">Use the following parameters:</span></span>

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3" -replicate-phoenix-meta

## <a name="copy-and-migrate-data"></a><span data-ttu-id="1a225-337">Copy and migrate data</span><span class="sxs-lookup"><span data-stu-id="1a225-337">Copy and migrate data</span></span>

<span data-ttu-id="1a225-338">There are two separate script action scripts available for copying or migrating data after replication is enabled:</span><span class="sxs-lookup"><span data-stu-id="1a225-338">There are two separate script action scripts available for copying or migrating data after replication is enabled:</span></span>

- <span data-ttu-id="1a225-339">[Script for small tables](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_copy_table.sh) (tables that are a few gigabytes in size, and overall copy is expected to finish in less than one hour)</span><span class="sxs-lookup"><span data-stu-id="1a225-339">[Script for small tables](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_copy_table.sh) (tables that are a few gigabytes in size, and overall copy is expected to finish in less than one hour)</span></span>

- <span data-ttu-id="1a225-340">[Script for large tables](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/nohup_hdi_copy_table.sh) (tables that are expected to take longer than one hour to copy)</span><span class="sxs-lookup"><span data-stu-id="1a225-340">[Script for large tables](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/nohup_hdi_copy_table.sh) (tables that are expected to take longer than one hour to copy)</span></span>

<span data-ttu-id="1a225-341">You can follow the same procedure that's described in [Enable replication](#enable-replication) to call the script action.</span><span class="sxs-lookup"><span data-stu-id="1a225-341">You can follow the same procedure that's described in [Enable replication](#enable-replication) to call the script action.</span></span> <span data-ttu-id="1a225-342">Use the following parameters:</span><span class="sxs-lookup"><span data-stu-id="1a225-342">Use the following parameters:</span></span>

    -m hn1 -t <table1:start_timestamp:end_timestamp;table2:start_timestamp:end_timestamp;...> -p <replication_peer> [-everythingTillNow]

<span data-ttu-id="1a225-343">The `print_usage()` section of the [script](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_copy_table.sh) has a detailed description of parameters.</span><span class="sxs-lookup"><span data-stu-id="1a225-343">The `print_usage()` section of the [script](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_copy_table.sh) has a detailed description of parameters.</span></span>

### <a name="scenarios"></a><span data-ttu-id="1a225-344">Scenarios</span><span class="sxs-lookup"><span data-stu-id="1a225-344">Scenarios</span></span>

- <span data-ttu-id="1a225-345">**Copy specific tables (test1, test2, and test3) for all rows edited until now (current time stamp)**:</span><span class="sxs-lookup"><span data-stu-id="1a225-345">**Copy specific tables (test1, test2, and test3) for all rows edited until now (current time stamp)**:</span></span>

        -m hn1 -t "test1::;test2::;test3::" -p "zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure" -everythingTillNow
  <span data-ttu-id="1a225-346">Or:</span><span class="sxs-lookup"><span data-stu-id="1a225-346">Or:</span></span>

        -m hn1 -t "test1::;test2::;test3::" --replication-peer="zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure" -everythingTillNow


- <span data-ttu-id="1a225-347">**Copy specific tables with a specified time range**:</span><span class="sxs-lookup"><span data-stu-id="1a225-347">**Copy specific tables with a specified time range**:</span></span>

        -m hn1 -t "table1:0:452256397;table2:14141444:452256397" -p "zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure"


## <a name="disable-replication"></a><span data-ttu-id="1a225-348">Disable replication</span><span class="sxs-lookup"><span data-stu-id="1a225-348">Disable replication</span></span>

<span data-ttu-id="1a225-349">To disable replication, use another script action script from [GitHub](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh).</span><span class="sxs-lookup"><span data-stu-id="1a225-349">To disable replication, use another script action script from [GitHub](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh).</span></span> <span data-ttu-id="1a225-350">You can follow the same procedure that's described in [Enable replication](#enable-replication) to call the script action.</span><span class="sxs-lookup"><span data-stu-id="1a225-350">You can follow the same procedure that's described in [Enable replication](#enable-replication) to call the script action.</span></span> <span data-ttu-id="1a225-351">Use the following parameters:</span><span class="sxs-lookup"><span data-stu-id="1a225-351">Use the following parameters:</span></span>

    -m hn1 -s <source cluster DNS name> -sp <source cluster Ambari password> <-all|-t "table1;table2;...">  

<span data-ttu-id="1a225-352">The `print_usage()` section of the [script](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh) has a detailed explanation of parameters.</span><span class="sxs-lookup"><span data-stu-id="1a225-352">The `print_usage()` section of the [script](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh) has a detailed explanation of parameters.</span></span>

### <a name="scenarios"></a><span data-ttu-id="1a225-353">Scenarios</span><span class="sxs-lookup"><span data-stu-id="1a225-353">Scenarios</span></span>

- <span data-ttu-id="1a225-354">**Disable replication on all tables**:</span><span class="sxs-lookup"><span data-stu-id="1a225-354">**Disable replication on all tables**:</span></span>

        -m hn1 -s <source cluster DNS name> -sp Mypassword\!789 -all
  <span data-ttu-id="1a225-355">or</span><span class="sxs-lookup"><span data-stu-id="1a225-355">or</span></span>

        --src-cluster=<source cluster DNS name> --dst-cluster=<destination cluster DNS name> --src-ambari-user=<source cluster Ambari user name> --src-ambari-password=<source cluster Ambari password>

- <span data-ttu-id="1a225-356">**Disable replication on specified tables (table1, table2, and table3)**:</span><span class="sxs-lookup"><span data-stu-id="1a225-356">**Disable replication on specified tables (table1, table2, and table3)**:</span></span>

        -m hn1 -s <source cluster DNS name> -sp <source cluster Ambari password> -t "table1;table2;table3"

## <a name="next-steps"></a><span data-ttu-id="1a225-357">Next steps</span><span class="sxs-lookup"><span data-stu-id="1a225-357">Next steps</span></span>

<span data-ttu-id="1a225-358">In this tutorial, you learned how to set up HBase replication within a virtual network, or between two virtual networks.</span><span class="sxs-lookup"><span data-stu-id="1a225-358">In this tutorial, you learned how to set up HBase replication within a virtual network, or between two virtual networks.</span></span> <span data-ttu-id="1a225-359">To learn more about HDInsight and HBase, see these articles:</span><span class="sxs-lookup"><span data-stu-id="1a225-359">To learn more about HDInsight and HBase, see these articles:</span></span>

* [<span data-ttu-id="1a225-360">Get started with Apache HBase in HDInsight</span><span class="sxs-lookup"><span data-stu-id="1a225-360">Get started with Apache HBase in HDInsight</span></span>](./apache-hbase-tutorial-get-started-linux.md)
* [<span data-ttu-id="1a225-361">HDInsight HBase overview</span><span class="sxs-lookup"><span data-stu-id="1a225-361">HDInsight HBase overview</span></span>](./apache-hbase-overview.md)
* [<span data-ttu-id="1a225-362">Create HBase clusters in Azure Virtual Network</span><span class="sxs-lookup"><span data-stu-id="1a225-362">Create HBase clusters in Azure Virtual Network</span></span>](./apache-hbase-provision-vnet.md)

