---
title: Create HBase clusters in a Virtual Network | Microsoft Docs
description: Get started using HBase in Azure HDInsight. Learn how to create HDInsight HBase clusters on Azure Virtual Network.
keywords: ''
services: hdinsight,virtual-network
documentationcenter: ''
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 8de8e446-f818-4e61-8fad-e9d38421e80d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 02/22/2017
ms.author: jgao
ms.openlocfilehash: 45e54dddd0b116ca97a98c1e596884c9fc3b2371
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549274"
---
# <a name="create-hbase-clusters-in-azure-virtual-network"></a><span data-ttu-id="176a6-104">Create HBase clusters in Azure Virtual Network</span><span class="sxs-lookup"><span data-stu-id="176a6-104">Create HBase clusters in Azure Virtual Network</span></span>
<span data-ttu-id="176a6-105">Learn how to create Azure HDInsight HBase clusters in an [Azure Virtual Network][1].</span><span class="sxs-lookup"><span data-stu-id="176a6-105">Learn how to create Azure HDInsight HBase clusters in an [Azure Virtual Network][1].</span></span>

<span data-ttu-id="176a6-106">With virtual network integration, HBase clusters can be deployed to the same virtual network as your applications so that applications can communicate with HBase directly.</span><span class="sxs-lookup"><span data-stu-id="176a6-106">With virtual network integration, HBase clusters can be deployed to the same virtual network as your applications so that applications can communicate with HBase directly.</span></span> <span data-ttu-id="176a6-107">The benefits include:</span><span class="sxs-lookup"><span data-stu-id="176a6-107">The benefits include:</span></span>

* <span data-ttu-id="176a6-108">Direct connectivity of the web application to the nodes of the HBase cluster, which enables communication via HBase Java remote procedure call (RPC) APIs.</span><span class="sxs-lookup"><span data-stu-id="176a6-108">Direct connectivity of the web application to the nodes of the HBase cluster, which enables communication via HBase Java remote procedure call (RPC) APIs.</span></span>
* <span data-ttu-id="176a6-109">Improved performance by not having your traffic go over multiple gateways and load-balancers.</span><span class="sxs-lookup"><span data-stu-id="176a6-109">Improved performance by not having your traffic go over multiple gateways and load-balancers.</span></span>
* <span data-ttu-id="176a6-110">The ability to process sensitive information in a more secure manner without exposing a public endpoint.</span><span class="sxs-lookup"><span data-stu-id="176a6-110">The ability to process sensitive information in a more secure manner without exposing a public endpoint.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="176a6-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="176a6-111">Prerequisites</span></span>
<span data-ttu-id="176a6-112">Before you begin this tutorial, you must have the following:</span><span class="sxs-lookup"><span data-stu-id="176a6-112">Before you begin this tutorial, you must have the following:</span></span>

* <span data-ttu-id="176a6-113">**An Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="176a6-113">**An Azure subscription**.</span></span> <span data-ttu-id="176a6-114">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="176a6-114">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="176a6-115">**A workstation with Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="176a6-115">**A workstation with Azure PowerShell**.</span></span> <span data-ttu-id="176a6-116">See [Install and use Azure PowerShell](https://azure.microsoft.com/documentation/videos/install-and-use-azure-powershell/).</span><span class="sxs-lookup"><span data-stu-id="176a6-116">See [Install and use Azure PowerShell](https://azure.microsoft.com/documentation/videos/install-and-use-azure-powershell/).</span></span>

## <a name="create-hbase-cluster-into-virtual-network"></a><span data-ttu-id="176a6-117">Create HBase cluster into virtual network</span><span class="sxs-lookup"><span data-stu-id="176a6-117">Create HBase cluster into virtual network</span></span>
<span data-ttu-id="176a6-118">In this section, you create a Linux-based HBase cluster with the dependent Azure Storage account in an Azure virtual network using an [Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="176a6-118">In this section, you create a Linux-based HBase cluster with the dependent Azure Storage account in an Azure virtual network using an [Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span> <span data-ttu-id="176a6-119">For other cluster creation methods and understanding the settings, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="176a6-119">For other cluster creation methods and understanding the settings, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span> <span data-ttu-id="176a6-120">For more information about using a template to create Hadoop clusters in HDInsight, see [Create Hadoop clusters in HDInsight using Azure Resource Manager templates](hdinsight-hadoop-create-windows-clusters-arm-templates.md)</span><span class="sxs-lookup"><span data-stu-id="176a6-120">For more information about using a template to create Hadoop clusters in HDInsight, see [Create Hadoop clusters in HDInsight using Azure Resource Manager templates](hdinsight-hadoop-create-windows-clusters-arm-templates.md)</span></span>

> [!NOTE]
> <span data-ttu-id="176a6-121">Some properties are hard-coded into the template.</span><span class="sxs-lookup"><span data-stu-id="176a6-121">Some properties are hard-coded into the template.</span></span> <span data-ttu-id="176a6-122">For example:</span><span class="sxs-lookup"><span data-stu-id="176a6-122">For example:</span></span>
>
> * <span data-ttu-id="176a6-123">**Location**: East US 2</span><span class="sxs-lookup"><span data-stu-id="176a6-123">**Location**: East US 2</span></span>
> * <span data-ttu-id="176a6-124">__Cluster version: 3.4</span><span class="sxs-lookup"><span data-stu-id="176a6-124">__Cluster version: 3.4</span></span>
> * <span data-ttu-id="176a6-125">**Cluster worker node count**: 4</span><span class="sxs-lookup"><span data-stu-id="176a6-125">**Cluster worker node count**: 4</span></span>
> * <span data-ttu-id="176a6-126">**Default storage account**: a unique string</span><span class="sxs-lookup"><span data-stu-id="176a6-126">**Default storage account**: a unique string</span></span>
> * <span data-ttu-id="176a6-127">**Virtual network name**: &lt;Cluster Name>-vnet</span><span class="sxs-lookup"><span data-stu-id="176a6-127">**Virtual network name**: &lt;Cluster Name>-vnet</span></span>
> * <span data-ttu-id="176a6-128">**Virtual network address space**: 10.0.0.0/16</span><span class="sxs-lookup"><span data-stu-id="176a6-128">**Virtual network address space**: 10.0.0.0/16</span></span>
> * <span data-ttu-id="176a6-129">**Subnet name**: subnet1</span><span class="sxs-lookup"><span data-stu-id="176a6-129">**Subnet name**: subnet1</span></span>
> * <span data-ttu-id="176a6-130">**Subnet address range**: 10.0.0.0/24</span><span class="sxs-lookup"><span data-stu-id="176a6-130">**Subnet address range**: 10.0.0.0/24</span></span>
>
> <span data-ttu-id="176a6-131">&lt;Cluster Name> is replaced with the cluster name you provide when using the template.</span><span class="sxs-lookup"><span data-stu-id="176a6-131">&lt;Cluster Name> is replaced with the cluster name you provide when using the template.</span></span>
>
>

1. <span data-ttu-id="176a6-132">Click the following image to open the template in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="176a6-132">Click the following image to open the template in the Azure portal.</span></span> <span data-ttu-id="176a6-133">The template is located in [Azure QuickStart Templates](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-linux-vnet/).</span><span class="sxs-lookup"><span data-stu-id="176a6-133">The template is located in [Azure QuickStart Templates](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-linux-vnet/).</span></span>

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-linux-vnet%2Fazuredeploy.json" target="_blank"><img src="https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hbase-provision-vnet/deploy-to-azure.png" alt="Deploy to Azure"></a>
2. <span data-ttu-id="176a6-134">From the **Custom deployment** blade, enter the following:</span><span class="sxs-lookup"><span data-stu-id="176a6-134">From the **Custom deployment** blade, enter the following:</span></span>

   * <span data-ttu-id="176a6-135">**Subscription**: Select an Azure subscription used to create the HDInsight cluster, the dependent Storage account and the Azure virtual network.</span><span class="sxs-lookup"><span data-stu-id="176a6-135">**Subscription**: Select an Azure subscription used to create the HDInsight cluster, the dependent Storage account and the Azure virtual network.</span></span>
   * <span data-ttu-id="176a6-136">**Resource group**: Select **Create new**, and specify a new resource group name.</span><span class="sxs-lookup"><span data-stu-id="176a6-136">**Resource group**: Select **Create new**, and specify a new resource group name.</span></span>
   * <span data-ttu-id="176a6-137">**Location**: Select a location for the resource group.</span><span class="sxs-lookup"><span data-stu-id="176a6-137">**Location**: Select a location for the resource group.</span></span>
   * <span data-ttu-id="176a6-138">**ClusterName**: Enter a name for the Hadoop cluster to be created.</span><span class="sxs-lookup"><span data-stu-id="176a6-138">**ClusterName**: Enter a name for the Hadoop cluster to be created.</span></span>
   * <span data-ttu-id="176a6-139">**Cluster login name and password**: The default login name is **admin**.</span><span class="sxs-lookup"><span data-stu-id="176a6-139">**Cluster login name and password**: The default login name is **admin**.</span></span>
   * <span data-ttu-id="176a6-140">**SSH username and password**: The default username is **sshuser**.</span><span class="sxs-lookup"><span data-stu-id="176a6-140">**SSH username and password**: The default username is **sshuser**.</span></span>  <span data-ttu-id="176a6-141">You can rename it.</span><span class="sxs-lookup"><span data-stu-id="176a6-141">You can rename it.</span></span>
   * <span data-ttu-id="176a6-142">**I agree to the terms and the conditions stated above**: (Select)</span><span class="sxs-lookup"><span data-stu-id="176a6-142">**I agree to the terms and the conditions stated above**: (Select)</span></span>
3. <span data-ttu-id="176a6-143">Click **Purchase**.</span><span class="sxs-lookup"><span data-stu-id="176a6-143">Click **Purchase**.</span></span> <span data-ttu-id="176a6-144">It takes about around 20 minutes to create a cluster.</span><span class="sxs-lookup"><span data-stu-id="176a6-144">It takes about around 20 minutes to create a cluster.</span></span> <span data-ttu-id="176a6-145">Once the cluster is created, you can click the cluster blade in the portal to open it.</span><span class="sxs-lookup"><span data-stu-id="176a6-145">Once the cluster is created, you can click the cluster blade in the portal to open it.</span></span>

<span data-ttu-id="176a6-146">After you complete the tutorial, you might want to delete the cluster.</span><span class="sxs-lookup"><span data-stu-id="176a6-146">After you complete the tutorial, you might want to delete the cluster.</span></span> <span data-ttu-id="176a6-147">With HDInsight, your data is stored in Azure Storage, so you can safely delete a cluster when it is not in use.</span><span class="sxs-lookup"><span data-stu-id="176a6-147">With HDInsight, your data is stored in Azure Storage, so you can safely delete a cluster when it is not in use.</span></span> <span data-ttu-id="176a6-148">You are also charged for an HDInsight cluster, even when it is not in use.</span><span class="sxs-lookup"><span data-stu-id="176a6-148">You are also charged for an HDInsight cluster, even when it is not in use.</span></span> <span data-ttu-id="176a6-149">Since the charges for the cluster are many times more than the charges for storage, it makes economic sense to delete clusters when they are not in use.</span><span class="sxs-lookup"><span data-stu-id="176a6-149">Since the charges for the cluster are many times more than the charges for storage, it makes economic sense to delete clusters when they are not in use.</span></span> <span data-ttu-id="176a6-150">For the instructions of deleting a cluster, see [Manage Hadoop clusters in HDInsight by using the Azure portal](hdinsight-administer-use-management-portal.md#delete-clusters).</span><span class="sxs-lookup"><span data-stu-id="176a6-150">For the instructions of deleting a cluster, see [Manage Hadoop clusters in HDInsight by using the Azure portal](hdinsight-administer-use-management-portal.md#delete-clusters).</span></span>

<span data-ttu-id="176a6-151">To begin working with your new HBase cluster, you can use the procedures found in [Get started using HBase with Hadoop in HDInsight](hdinsight-hbase-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="176a6-151">To begin working with your new HBase cluster, you can use the procedures found in [Get started using HBase with Hadoop in HDInsight](hdinsight-hbase-tutorial-get-started.md).</span></span>

## <a name="connect-to-the-hbase-cluster-using-hbase-java-rpc-apis"></a><span data-ttu-id="176a6-152">Connect to the HBase cluster using HBase Java RPC APIs</span><span class="sxs-lookup"><span data-stu-id="176a6-152">Connect to the HBase cluster using HBase Java RPC APIs</span></span>
1. <span data-ttu-id="176a6-153">Create an infrastructure as a service (IaaS) virtual machine into the same Azure virtual network and the same subnet.</span><span class="sxs-lookup"><span data-stu-id="176a6-153">Create an infrastructure as a service (IaaS) virtual machine into the same Azure virtual network and the same subnet.</span></span> <span data-ttu-id="176a6-154">For instructions on creating a new IaaS virtual machine, see [Create a Virtual Machine Running Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="176a6-154">For instructions on creating a new IaaS virtual machine, see [Create a Virtual Machine Running Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md).</span></span> <span data-ttu-id="176a6-155">When following the steps in this document, you must use the following for the Network configuration:</span><span class="sxs-lookup"><span data-stu-id="176a6-155">When following the steps in this document, you must use the following for the Network configuration:</span></span>

   * <span data-ttu-id="176a6-156">**Virtual network**: &lt;Cluster name>-vnet</span><span class="sxs-lookup"><span data-stu-id="176a6-156">**Virtual network**: &lt;Cluster name>-vnet</span></span>
   * <span data-ttu-id="176a6-157">**Subnet**: subnet1</span><span class="sxs-lookup"><span data-stu-id="176a6-157">**Subnet**: subnet1</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="176a6-158">Replace &lt;Cluster name> with the name you used when creating the HDInsight cluster in previous steps.</span><span class="sxs-lookup"><span data-stu-id="176a6-158">Replace &lt;Cluster name> with the name you used when creating the HDInsight cluster in previous steps.</span></span>
   >
   >

   <span data-ttu-id="176a6-159">Using these values, the virtual machine is placed in the same virtual network and subnet as the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="176a6-159">Using these values, the virtual machine is placed in the same virtual network and subnet as the HDInsight cluster.</span></span> <span data-ttu-id="176a6-160">This configuration allows them to directly communicate with each other.</span><span class="sxs-lookup"><span data-stu-id="176a6-160">This configuration allows them to directly communicate with each other.</span></span> <span data-ttu-id="176a6-161">There is a way to create an HDInsight cluster with an empty edge node.</span><span class="sxs-lookup"><span data-stu-id="176a6-161">There is a way to create an HDInsight cluster with an empty edge node.</span></span> <span data-ttu-id="176a6-162">The edge node can be used to manage the cluster.</span><span class="sxs-lookup"><span data-stu-id="176a6-162">The edge node can be used to manage the cluster.</span></span>  <span data-ttu-id="176a6-163">For more information, see [Use empty edge nodes in HDInsight](hdinsight-apps-use-edge-node.md).</span><span class="sxs-lookup"><span data-stu-id="176a6-163">For more information, see [Use empty edge nodes in HDInsight](hdinsight-apps-use-edge-node.md).</span></span>

2. <span data-ttu-id="176a6-164">When using a Java application to connect to HBase remotely, you must use the fully qualified domain name (FQDN).</span><span class="sxs-lookup"><span data-stu-id="176a6-164">When using a Java application to connect to HBase remotely, you must use the fully qualified domain name (FQDN).</span></span> <span data-ttu-id="176a6-165">To determine this, you must get the connection-specific DNS suffix of the HBase cluster.</span><span class="sxs-lookup"><span data-stu-id="176a6-165">To determine this, you must get the connection-specific DNS suffix of the HBase cluster.</span></span> <span data-ttu-id="176a6-166">To do that, you can use one of the following methods:</span><span class="sxs-lookup"><span data-stu-id="176a6-166">To do that, you can use one of the following methods:</span></span>

   * <span data-ttu-id="176a6-167">Use a Web browser to make an Ambari call:</span><span class="sxs-lookup"><span data-stu-id="176a6-167">Use a Web browser to make an Ambari call:</span></span>

     <span data-ttu-id="176a6-168">Browse to https://&lt;ClusterName>.azurehdinsight.net/api/v1/clusters/&lt;ClusterName>/hosts?minimal_response=true.</span><span class="sxs-lookup"><span data-stu-id="176a6-168">Browse to https://&lt;ClusterName>.azurehdinsight.net/api/v1/clusters/&lt;ClusterName>/hosts?minimal_response=true.</span></span> <span data-ttu-id="176a6-169">It turns a JSON file with the DNS suffixes.</span><span class="sxs-lookup"><span data-stu-id="176a6-169">It turns a JSON file with the DNS suffixes.</span></span>
   * <span data-ttu-id="176a6-170">Use the Ambari website:</span><span class="sxs-lookup"><span data-stu-id="176a6-170">Use the Ambari website:</span></span>

     1. <span data-ttu-id="176a6-171">Browse to  https://&lt;ClusterName>.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="176a6-171">Browse to  https://&lt;ClusterName>.azurehdinsight.net.</span></span>
     2. <span data-ttu-id="176a6-172">Click **Hosts** from the top menu.</span><span class="sxs-lookup"><span data-stu-id="176a6-172">Click **Hosts** from the top menu.</span></span>
   * <span data-ttu-id="176a6-173">Use Curl to make REST calls:</span><span class="sxs-lookup"><span data-stu-id="176a6-173">Use Curl to make REST calls:</span></span>

         curl -u <username>:<password> -k https://<clustername>.azurehdinsight.net/ambari/api/v1/clusters/<clustername>.azurehdinsight.net/services/hbase/components/hbrest

     <span data-ttu-id="176a6-174">In the JavaScript Object Notation (JSON) data returned, find the "host_name" entry.</span><span class="sxs-lookup"><span data-stu-id="176a6-174">In the JavaScript Object Notation (JSON) data returned, find the "host_name" entry.</span></span> <span data-ttu-id="176a6-175">This contains the FQDN for the nodes in the cluster.</span><span class="sxs-lookup"><span data-stu-id="176a6-175">This contains the FQDN for the nodes in the cluster.</span></span> <span data-ttu-id="176a6-176">For example:</span><span class="sxs-lookup"><span data-stu-id="176a6-176">For example:</span></span>

         ...
         "host_name": "wordkernode0.<clustername>.b1.cloudapp.net
         ...

     <span data-ttu-id="176a6-177">The portion of the domain name beginning with the cluster name is the DNS suffix.</span><span class="sxs-lookup"><span data-stu-id="176a6-177">The portion of the domain name beginning with the cluster name is the DNS suffix.</span></span> <span data-ttu-id="176a6-178">For example, mycluster.b1.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="176a6-178">For example, mycluster.b1.cloudapp.net.</span></span>
   * <span data-ttu-id="176a6-179">Use Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="176a6-179">Use Azure PowerShell</span></span>

     <span data-ttu-id="176a6-180">Use the following Azure PowerShell script to register the **Get-ClusterDetail** function, which can be used to return the DNS suffix:</span><span class="sxs-lookup"><span data-stu-id="176a6-180">Use the following Azure PowerShell script to register the **Get-ClusterDetail** function, which can be used to return the DNS suffix:</span></span>

         function Get-ClusterDetail(
             [String]
             [Parameter( Position=0, Mandatory=$true )]
             $ClusterDnsName,
             [String]
             [Parameter( Position=1, Mandatory=$true )]
             $Username,
             [String]
             [Parameter( Position=2, Mandatory=$true )]
             $Password,
             [String]
             [Parameter( Position=3, Mandatory=$true )]
             $PropertyName
             )
         {
         <#
             .SYNOPSIS
              Displays information to facilitate an HDInsight cluster-to-cluster scenario within the same virtual network.
             .Description
              This command shows the following 4 properties of an HDInsight cluster:
              1. ZookeeperQuorum (supports only HBase type cluster)
                 Shows the value of HBase property "hbase.zookeeper.quorum".
              2. ZookeeperClientPort (supports only HBase type cluster)
                 Shows the value of HBase property "hbase.zookeeper.property.clientPort".
              3. HBaseRestServers (supports only HBase type cluster)
                 Shows a list of host FQDNs that run the HBase REST server.
              4. FQDNSuffix (supports all cluster types)
                 Shows the FQDN suffix of hosts in the cluster.
             .EXAMPLE
              Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName ZookeeperQuorum
              This command shows the value of HBase property "hbase.zookeeper.quorum".
             .EXAMPLE
              Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName ZookeeperClientPort
              This command shows the value of HBase property "hbase.zookeeper.property.clientPort".
             .EXAMPLE
              Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName HBaseRestServers
              This command shows a list of host FQDNs that run the HBase REST server.
             .EXAMPLE
              Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName FQDNSuffix
              This command shows the FQDN suffix of hosts in the cluster.
         #>

             $DnsSuffix = ".azurehdinsight.net"

             $ClusterFQDN = $ClusterDnsName + $DnsSuffix
             $webclient = new-object System.Net.WebClient
             $webclient.Credentials = new-object System.Net.NetworkCredential($Username, $Password)

             if($PropertyName -eq "ZookeeperQuorum")
             {
                 $Url = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/configurations?type=hbase-site&tag=default&fields=items/properties/hbase.zookeeper.quorum"
                 $Response = $webclient.DownloadString($Url)
                 $JsonObject = $Response | ConvertFrom-Json
                 Write-host $JsonObject.items[0].properties.'hbase.zookeeper.quorum'
             }
             if($PropertyName -eq "ZookeeperClientPort")
             {
                 $Url = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/configurations?type=hbase-site&tag=default&fields=items/properties/hbase.zookeeper.property.clientPort"
                 $Response = $webclient.DownloadString($Url)
                 $JsonObject = $Response | ConvertFrom-Json
                 Write-host $JsonObject.items[0].properties.'hbase.zookeeper.property.clientPort'
             }
             if($PropertyName -eq "HBaseRestServers")
             {
                 $Url1 = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/configurations?type=hbase-site&tag=default&fields=items/properties/hbase.rest.port"
                 $Response1 = $webclient.DownloadString($Url1)
                 $JsonObject1 = $Response1 | ConvertFrom-Json
                 $PortNumber = $JsonObject1.items[0].properties.'hbase.rest.port'

                 $Url2 = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/services/hbase/components/hbrest"
                 $Response2 = $webclient.DownloadString($Url2)
                 $JsonObject2 = $Response2 | ConvertFrom-Json
                 foreach ($host_component in $JsonObject2.host_components)
                 {
                     $ConnectionString = $host_component.HostRoles.host_name + ":" + $PortNumber
                     Write-host $ConnectionString
                 }
             }
             if($PropertyName -eq "FQDNSuffix")
             {
                 $Url = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/services/YARN/components/RESOURCEMANAGER"
                 $Response = $webclient.DownloadString($Url)
                 $JsonObject = $Response | ConvertFrom-Json
                 $FQDN = $JsonObject.host_components[0].HostRoles.host_name
                 $pos = $FQDN.IndexOf(".")
                 $Suffix = $FQDN.Substring($pos + 1)
                 Write-host $Suffix
             }
         }

     <span data-ttu-id="176a6-181">After running the Azure PowerShell script, use the following command to return the DNS suffix by using the **Get-ClusterDetail** function.</span><span class="sxs-lookup"><span data-stu-id="176a6-181">After running the Azure PowerShell script, use the following command to return the DNS suffix by using the **Get-ClusterDetail** function.</span></span> <span data-ttu-id="176a6-182">Specify your HDInsight HBase cluster name, admin name, and admin password when using this command.</span><span class="sxs-lookup"><span data-stu-id="176a6-182">Specify your HDInsight HBase cluster name, admin name, and admin password when using this command.</span></span>

         Get-ClusterDetail -ClusterDnsName <yourclustername> -PropertyName FQDNSuffix -Username <clusteradmin> -Password <clusteradminpassword>

     <span data-ttu-id="176a6-183">This will return the DNS suffix.</span><span class="sxs-lookup"><span data-stu-id="176a6-183">This will return the DNS suffix.</span></span> <span data-ttu-id="176a6-184">For example, **yourclustername.b4.internal.cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="176a6-184">For example, **yourclustername.b4.internal.cloudapp.net**.</span></span>
   * <span data-ttu-id="176a6-185">Use RDP</span><span class="sxs-lookup"><span data-stu-id="176a6-185">Use RDP</span></span>

     <span data-ttu-id="176a6-186">You can also use Remote Desktop to connect to the HBase cluster (you will be connected to the head node) and run **ipconfig** from a command prompt to obtain the DNS suffix.</span><span class="sxs-lookup"><span data-stu-id="176a6-186">You can also use Remote Desktop to connect to the HBase cluster (you will be connected to the head node) and run **ipconfig** from a command prompt to obtain the DNS suffix.</span></span> <span data-ttu-id="176a6-187">For instructions on enabling Remote Desktop Protocol (RDP) and connecting to the cluster by using RDP, see [Manage Hadoop clusters in HDInsight using the Azure portal][hdinsight-admin-portal].</span><span class="sxs-lookup"><span data-stu-id="176a6-187">For instructions on enabling Remote Desktop Protocol (RDP) and connecting to the cluster by using RDP, see [Manage Hadoop clusters in HDInsight using the Azure portal][hdinsight-admin-portal].</span></span>

     ![hdinsight.hbase.dns.surffix][img-dns-surffix]

<!--
3.    Change the primary DNS suffix configuration of the virtual machine. This enables the virtual machine to automatically resolve the host name of the HBase cluster without explicit specification of the suffix. For example, the *workernode0* host name will be correctly resolved to workernode0 of the HBase cluster.

    To make the configuration change:

    1. RDP into the virtual machine.
    2. Open **Local Group Policy Editor**. The executable is gpedit.msc.
    3. Expand **Computer Configuration**, expand **Administrative Templates**, expand **Network**, and then click **DNS Client**.
    - Set **Primary DNS Suffix** to the value obtained in step 2:

        ![hdinsight.hbase.primary.dns.suffix][img-primary-dns-suffix]
    4. Click **OK**.
    5. Reboot the virtual machine.
-->

<span data-ttu-id="176a6-189">To verify that the virtual machine can communicate with the HBase cluster, use the command `ping headnode0.<dns suffix>` from the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="176a6-189">To verify that the virtual machine can communicate with the HBase cluster, use the command `ping headnode0.<dns suffix>` from the virtual machine.</span></span> <span data-ttu-id="176a6-190">For example, ping headnode0.mycluster.b1.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="176a6-190">For example, ping headnode0.mycluster.b1.cloudapp.net.</span></span>

<span data-ttu-id="176a6-191">To use this information in a Java application, you can follow the steps in [Use Maven to build Java applications that use HBase with HDInsight (Hadoop)](hdinsight-hbase-build-java-maven.md) to create an application.</span><span class="sxs-lookup"><span data-stu-id="176a6-191">To use this information in a Java application, you can follow the steps in [Use Maven to build Java applications that use HBase with HDInsight (Hadoop)](hdinsight-hbase-build-java-maven.md) to create an application.</span></span> <span data-ttu-id="176a6-192">To have the application connect to a remote HBase server, modify the **hbase-site.xml** file in this example to use the FQDN for Zookeeper.</span><span class="sxs-lookup"><span data-stu-id="176a6-192">To have the application connect to a remote HBase server, modify the **hbase-site.xml** file in this example to use the FQDN for Zookeeper.</span></span> <span data-ttu-id="176a6-193">For example:</span><span class="sxs-lookup"><span data-stu-id="176a6-193">For example:</span></span>

    <property>
        <name>hbase.zookeeper.quorum</name>
        <value>zookeeper0.<dns suffix>,zookeeper1.<dns suffix>,zookeeper2.<dns suffix></value>
    </property>

> [!NOTE]
> <span data-ttu-id="176a6-194">For more information on name resolution in Azure virtual networks, including how to use your own DNS server, see [Name Resolution (DNS)](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span><span class="sxs-lookup"><span data-stu-id="176a6-194">For more information on name resolution in Azure virtual networks, including how to use your own DNS server, see [Name Resolution (DNS)](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="176a6-195">Next steps</span><span class="sxs-lookup"><span data-stu-id="176a6-195">Next steps</span></span>
<span data-ttu-id="176a6-196">In this tutorial you learned how to create an HBase cluster.</span><span class="sxs-lookup"><span data-stu-id="176a6-196">In this tutorial you learned how to create an HBase cluster.</span></span> <span data-ttu-id="176a6-197">To learn more, see:</span><span class="sxs-lookup"><span data-stu-id="176a6-197">To learn more, see:</span></span>

* [<span data-ttu-id="176a6-198">Get started with HDInsight</span><span class="sxs-lookup"><span data-stu-id="176a6-198">Get started with HDInsight</span></span>](hdinsight-hadoop-linux-tutorial-get-started.md)
* [<span data-ttu-id="176a6-199">Use empty edge nodes in HDInsight</span><span class="sxs-lookup"><span data-stu-id="176a6-199">Use empty edge nodes in HDInsight</span></span>](hdinsight-apps-use-edge-node.md)
* [<span data-ttu-id="176a6-200">Configure HBase replication in HDInsight</span><span class="sxs-lookup"><span data-stu-id="176a6-200">Configure HBase replication in HDInsight</span></span>](hdinsight-hbase-replication.md)
* [<span data-ttu-id="176a6-201">Create Hadoop clusters in HDInsight</span><span class="sxs-lookup"><span data-stu-id="176a6-201">Create Hadoop clusters in HDInsight</span></span>](hdinsight-provision-clusters.md)
* [<span data-ttu-id="176a6-202">Get started using HBase with Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="176a6-202">Get started using HBase with Hadoop in HDInsight</span></span>](hdinsight-hbase-tutorial-get-started.md)
* [<span data-ttu-id="176a6-203">Analyze Twitter sentiment with HBase in HDInsight</span><span class="sxs-lookup"><span data-stu-id="176a6-203">Analyze Twitter sentiment with HBase in HDInsight</span></span>](hdinsight-hbase-analyze-twitter-sentiment.md)
* <span data-ttu-id="176a6-204">[Virtual Network Overview][vnet-overview]</span><span class="sxs-lookup"><span data-stu-id="176a6-204">[Virtual Network Overview][vnet-overview]</span></span>

[1]: http://azure.microsoft.com/services/virtual-network/
[2]: http://technet.microsoft.com/library/ee176961.aspx
[3]: http://technet.microsoft.com/library/hh847889.aspx

[hbase-get-started]: hdinsight-hbase-tutorial-get-started.md
[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md
[vnet-overview]: ../virtual-network/virtual-networks-overview.md
[vm-create]: ../virtual-machines/virtual-machines-windows-hero-tutorial.md

[azure-portal]: https://portal.azure.com
[azure-create-storageaccount]: ../storage-create-storage-account.md
[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp

[hdinsight-powershell-reference]: https://msdn.microsoft.com/library/dn858087.aspx


[twitter-streaming-api]: https://dev.twitter.com/docs/streaming-apis
[twitter-statuses-filter]: https://dev.twitter.com/docs/api/1.1/post/statuses/filter


[powershell-install]: /powershell/azureps-cmdlets-docs


[hdinsight-customize-cluster]: hdinsight-hadoop-customize-cluster.md
[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-storage-powershell]: ../hdinsight-hadoop-use-blob-storage.md#powershell
[hdinsight-analyze-flight-delay-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-storage]: ../hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md
[hdinsight-hive-odbc]: hdinsight-connect-excel-hive-ODBC-driver.md
[hdinsight-hbase-replication-dns]: hdinsight-hbase-geo-replication-configure-DNS.md

[img-dns-surffix]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hbase-provision-vnet/DNSSuffix.png
[img-primary-dns-suffix]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hbase-provision-vnet/PrimaryDNSSuffix.png
[img-provision-cluster-page1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hbase-provision-vnet/hbasewizard1.png "Provision details for the new HBase cluster"
[img-provision-cluster-page5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hbase-provision-vnet/hbasewizard5.png "Use Script Action to customize an HBase cluster"

[azure-preview-portal]: https://portal.azure.com





