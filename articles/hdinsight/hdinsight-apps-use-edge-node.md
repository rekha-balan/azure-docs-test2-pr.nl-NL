---
title: Use empty edge nodes in HDInsight | Microsoft Docs
description: How to add an ampty edge node to HDInsight cluster that can be used as a client, and to test/host your HDInsight applications.
services: hdinsight
editor: cgronlun
manager: jhubbard
author: mumian
tags: azure-portal
documentationcenter: ''
ms.assetid: cdc7d1b4-15d7-4d4d-a13f-c7d3a694b4fb
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/02/2017
ms.author: jgao
ms.openlocfilehash: 264e9c6f556b2e66233410673516d06a20d3ca66
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550410"
---
# <a name="use-empty-edge-nodes-in-hdinsight"></a><span data-ttu-id="f85c4-103">Use empty edge nodes in HDInsight</span><span class="sxs-lookup"><span data-stu-id="f85c4-103">Use empty edge nodes in HDInsight</span></span>

<span data-ttu-id="f85c4-104">Learn how to add an empty edge node to a Linux-based HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="f85c4-104">Learn how to add an empty edge node to a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="f85c4-105">An empty edge node is a Linux virtual machine with the same client tools installed and configured as in the headnodes, but with no hadoop services running.</span><span class="sxs-lookup"><span data-stu-id="f85c4-105">An empty edge node is a Linux virtual machine with the same client tools installed and configured as in the headnodes, but with no hadoop services running.</span></span> <span data-ttu-id="f85c4-106">You can use the edge node for accessing the cluster, testing your client applications, and hosting your client applications.</span><span class="sxs-lookup"><span data-stu-id="f85c4-106">You can use the edge node for accessing the cluster, testing your client applications, and hosting your client applications.</span></span> 

<span data-ttu-id="f85c4-107">You can add an empty edge node to an existing HDInsight cluster, to a new cluster when you create the cluster.</span><span class="sxs-lookup"><span data-stu-id="f85c4-107">You can add an empty edge node to an existing HDInsight cluster, to a new cluster when you create the cluster.</span></span> <span data-ttu-id="f85c4-108">Adding an empty edge node is done using Azure Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="f85c4-108">Adding an empty edge node is done using Azure Resource Manager template.</span></span>  <span data-ttu-id="f85c4-109">The following sample demonstrates how it is done using a template:</span><span class="sxs-lookup"><span data-stu-id="f85c4-109">The following sample demonstrates how it is done using a template:</span></span>

    "resources": [
        {
            "name": "[concat(parameters('clusterName'),'/', variables('applicationName'))]",
            "type": "Microsoft.HDInsight/clusters/applications",
            "apiVersion": "2015-03-01-preview",
            "dependsOn": [ "[concat('Microsoft.HDInsight/clusters/',parameters('clusterName'))]" ],
            "properties": {
                "marketPlaceIdentifier": "EmptyNode",
                "computeProfile": {
                    "roles": [{
                        "name": "edgenode",
                        "targetInstanceCount": 1,
                        "hardwareProfile": {
                            "vmSize": "Standard_D3"
                        }
                    }]
                },
                "installScriptActions": [{
                    "name": "[concat('emptynode','-' ,uniquestring(variables('applicationName')))]",
                    "uri": "[parameters('installScriptAction')]",
                    "roles": ["edgenode"]
                }],
                "uninstallScriptActions": [],
                "httpsEndpoints": [],
                "applicationType": "CustomApplication"
            }
        }
    ],

<span data-ttu-id="f85c4-110">As shown in the sample, you can optionally call a [script action](hdinsight-hadoop-customize-cluster-linux.md) to perform additional configuration, such as installing [Apache Hue](hdinsight-hadoop-hue-linux.md) in the edge node.</span><span class="sxs-lookup"><span data-stu-id="f85c4-110">As shown in the sample, you can optionally call a [script action](hdinsight-hadoop-customize-cluster-linux.md) to perform additional configuration, such as installing [Apache Hue](hdinsight-hadoop-hue-linux.md) in the edge node.</span></span>

<span data-ttu-id="f85c4-111">The edge node virtual machine size must meet the HDInsight cluster worker node vm size requirements.</span><span class="sxs-lookup"><span data-stu-id="f85c4-111">The edge node virtual machine size must meet the HDInsight cluster worker node vm size requirements.</span></span> <span data-ttu-id="f85c4-112">For the recommended worker node vm sizes, see [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).</span><span class="sxs-lookup"><span data-stu-id="f85c4-112">For the recommended worker node vm sizes, see [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).</span></span>

<span data-ttu-id="f85c4-113">After you have created an edge node, you can connect to the edge node using SSH, and run client tools to access the Hadoop cluster in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f85c4-113">After you have created an edge node, you can connect to the edge node using SSH, and run client tools to access the Hadoop cluster in HDInsight.</span></span>

## <a name="add-an-edge-node-to-an-existing-cluster"></a><span data-ttu-id="f85c4-114">Add an edge node to an existing cluster</span><span class="sxs-lookup"><span data-stu-id="f85c4-114">Add an edge node to an existing cluster</span></span>
<span data-ttu-id="f85c4-115">In this section, you use a Resource Manager template to add an edge node to an existing HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="f85c4-115">In this section, you use a Resource Manager template to add an edge node to an existing HDInsight cluster.</span></span>  <span data-ttu-id="f85c4-116">The Resource Manager template can be found in [GitHub](https://github.com/hdinsight/Iaas-Applications/tree/master/EmptyNode).</span><span class="sxs-lookup"><span data-stu-id="f85c4-116">The Resource Manager template can be found in [GitHub](https://github.com/hdinsight/Iaas-Applications/tree/master/EmptyNode).</span></span> <span data-ttu-id="f85c4-117">The Resource Manager template calls a script action script located at https://raw.githubusercontent.com/hdinsight/Iaas-Applications/master/EmptyNode/scripts/EmptyNodeSetup.sh. The script doesn't perform any actions.</span><span class="sxs-lookup"><span data-stu-id="f85c4-117">The Resource Manager template calls a script action script located at https://raw.githubusercontent.com/hdinsight/Iaas-Applications/master/EmptyNode/scripts/EmptyNodeSetup.sh. The script doesn't perform any actions.</span></span>  <span data-ttu-id="f85c4-118">This is to demonstrate calling script action from a Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="f85c4-118">This is to demonstrate calling script action from a Resource Manager template.</span></span>

<span data-ttu-id="f85c4-119">**To add an empty edge node to an existing cluster**</span><span class="sxs-lookup"><span data-stu-id="f85c4-119">**To add an empty edge node to an existing cluster**</span></span>

1. <span data-ttu-id="f85c4-120">Create an HDInsight cluster if you don't have one yet.</span><span class="sxs-lookup"><span data-stu-id="f85c4-120">Create an HDInsight cluster if you don't have one yet.</span></span>  <span data-ttu-id="f85c4-121">See [Hadoop tutorial: Get started using Linux-based Hadoop in HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f85c4-121">See [Hadoop tutorial: Get started using Linux-based Hadoop in HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>
2. <span data-ttu-id="f85c4-122">Click the following image to sign in to Azure and open the Azure Resource Manager template in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f85c4-122">Click the following image to sign in to Azure and open the Azure Resource Manager template in the Azure portal.</span></span> 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fhdinsight%2FIaas-Applications%2Fmaster%2FEmptyNode%2Fazuredeploy.json" target="_blank"><img src="https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apps-use-edge-node/deploy-to-azure.png" alt="Deploy to Azure"></a>
3. <span data-ttu-id="f85c4-123">Configure the following properties:</span><span class="sxs-lookup"><span data-stu-id="f85c4-123">Configure the following properties:</span></span>
   
   * <span data-ttu-id="f85c4-124">**Subscription**: Select an Azure subscription used for creating the cluster.</span><span class="sxs-lookup"><span data-stu-id="f85c4-124">**Subscription**: Select an Azure subscription used for creating the cluster.</span></span>
   * <span data-ttu-id="f85c4-125">**Resource group**: Select the resource group used for the existing HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="f85c4-125">**Resource group**: Select the resource group used for the existing HDInsight cluster.</span></span>
   * <span data-ttu-id="f85c4-126">**Location**: Select the location of the existing HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="f85c4-126">**Location**: Select the location of the existing HDInsight cluster.</span></span>
   * <span data-ttu-id="f85c4-127">**Cluster Name**: Enter the name of an existing HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="f85c4-127">**Cluster Name**: Enter the name of an existing HDInsight cluster.</span></span>
   * <span data-ttu-id="f85c4-128">**Edge Node Size**: Select one of the VM sizes.</span><span class="sxs-lookup"><span data-stu-id="f85c4-128">**Edge Node Size**: Select one of the VM sizes.</span></span> <span data-ttu-id="f85c4-129">The vm size must meet the worker node vm size requirements.</span><span class="sxs-lookup"><span data-stu-id="f85c4-129">The vm size must meet the worker node vm size requirements.</span></span> <span data-ttu-id="f85c4-130">For the recommended worker node vm sizes, see [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).</span><span class="sxs-lookup"><span data-stu-id="f85c4-130">For the recommended worker node vm sizes, see [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).</span></span>
   * <span data-ttu-id="f85c4-131">**Edge Node Prefix**: The default value is **new**.</span><span class="sxs-lookup"><span data-stu-id="f85c4-131">**Edge Node Prefix**: The default value is **new**.</span></span>  <span data-ttu-id="f85c4-132">Using the default value, the edge node name is **new-edgenode**.</span><span class="sxs-lookup"><span data-stu-id="f85c4-132">Using the default value, the edge node name is **new-edgenode**.</span></span>  <span data-ttu-id="f85c4-133">You can customize the prefix from the portal.</span><span class="sxs-lookup"><span data-stu-id="f85c4-133">You can customize the prefix from the portal.</span></span> <span data-ttu-id="f85c4-134">You can also customize the full name from the template.</span><span class="sxs-lookup"><span data-stu-id="f85c4-134">You can also customize the full name from the template.</span></span>
4. <span data-ttu-id="f85c4-135">Check **I agree to the terms and conditions stated above**, and then click  **Purchase** to create the edge node.</span><span class="sxs-lookup"><span data-stu-id="f85c4-135">Check **I agree to the terms and conditions stated above**, and then click  **Purchase** to create the edge node.</span></span>

## <a name="add-an-edge-node-when-creating-a-cluster"></a><span data-ttu-id="f85c4-136">Add an edge node when creating a cluster</span><span class="sxs-lookup"><span data-stu-id="f85c4-136">Add an edge node when creating a cluster</span></span>
<span data-ttu-id="f85c4-137">In this section, you use a Resource Manager template to create HDInsight cluster with an edge node.</span><span class="sxs-lookup"><span data-stu-id="f85c4-137">In this section, you use a Resource Manager template to create HDInsight cluster with an edge node.</span></span>  <span data-ttu-id="f85c4-138">The Resource Manager template can be found in the [Azure QuickStart Templates gallery](https://azure.microsoft.com/documentation/templates/101-hdinsight-linux-with-edge-node/).</span><span class="sxs-lookup"><span data-stu-id="f85c4-138">The Resource Manager template can be found in the [Azure QuickStart Templates gallery](https://azure.microsoft.com/documentation/templates/101-hdinsight-linux-with-edge-node/).</span></span> <span data-ttu-id="f85c4-139">The Resource Manager template calls a script action script located at https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-hdinsight-linux-with-edge-node/scripts/EmptyNodeSetup.sh. The script doesn't perform any actions.</span><span class="sxs-lookup"><span data-stu-id="f85c4-139">The Resource Manager template calls a script action script located at https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-hdinsight-linux-with-edge-node/scripts/EmptyNodeSetup.sh. The script doesn't perform any actions.</span></span>  <span data-ttu-id="f85c4-140">This is to demonstrate calling script action from a Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="f85c4-140">This is to demonstrate calling script action from a Resource Manager template.</span></span>

<span data-ttu-id="f85c4-141">**To add an empty edge node to an existing cluster**</span><span class="sxs-lookup"><span data-stu-id="f85c4-141">**To add an empty edge node to an existing cluster**</span></span>

1. <span data-ttu-id="f85c4-142">Create an HDInsight cluster if you don't have one yet.</span><span class="sxs-lookup"><span data-stu-id="f85c4-142">Create an HDInsight cluster if you don't have one yet.</span></span>  <span data-ttu-id="f85c4-143">See [Hadoop tutorial: Get started using Linux-based Hadoop in HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f85c4-143">See [Hadoop tutorial: Get started using Linux-based Hadoop in HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>
2. <span data-ttu-id="f85c4-144">Click the following image to sign in to Azure and open the Azure Resource Manager template in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f85c4-144">Click the following image to sign in to Azure and open the Azure Resource Manager template in the Azure portal.</span></span> 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-with-edge-node%2Fazuredeploy.json" target="_blank"><img src="https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apps-use-edge-node/deploy-to-azure.png" alt="Deploy to Azure"></a>
3. <span data-ttu-id="f85c4-145">Configure the following properties:</span><span class="sxs-lookup"><span data-stu-id="f85c4-145">Configure the following properties:</span></span>
   
   * <span data-ttu-id="f85c4-146">**Subscription**: Select an Azure subscription used for creating the cluster.</span><span class="sxs-lookup"><span data-stu-id="f85c4-146">**Subscription**: Select an Azure subscription used for creating the cluster.</span></span>
   * <span data-ttu-id="f85c4-147">**Resource group**: Create a new resource group used for the cluster.</span><span class="sxs-lookup"><span data-stu-id="f85c4-147">**Resource group**: Create a new resource group used for the cluster.</span></span>
   * <span data-ttu-id="f85c4-148">**Location**: Select a location for the resource group.</span><span class="sxs-lookup"><span data-stu-id="f85c4-148">**Location**: Select a location for the resource group.</span></span>
   * <span data-ttu-id="f85c4-149">**Cluster Name**: Enter a name for the new cluster to create.</span><span class="sxs-lookup"><span data-stu-id="f85c4-149">**Cluster Name**: Enter a name for the new cluster to create.</span></span>
   * <span data-ttu-id="f85c4-150">**Cluster Login User Name**: Enter the Hadoop HTTP user name.</span><span class="sxs-lookup"><span data-stu-id="f85c4-150">**Cluster Login User Name**: Enter the Hadoop HTTP user name.</span></span>  <span data-ttu-id="f85c4-151">The default name is **admin**.</span><span class="sxs-lookup"><span data-stu-id="f85c4-151">The default name is **admin**.</span></span>
   * <span data-ttu-id="f85c4-152">**Cluster Login Password**: Enter the Hadoop HTTP user password.</span><span class="sxs-lookup"><span data-stu-id="f85c4-152">**Cluster Login Password**: Enter the Hadoop HTTP user password.</span></span>
   * <span data-ttu-id="f85c4-153">**Ssh User Name**: Enter the SSH user name.</span><span class="sxs-lookup"><span data-stu-id="f85c4-153">**Ssh User Name**: Enter the SSH user name.</span></span> <span data-ttu-id="f85c4-154">The default name is **sshuser**.</span><span class="sxs-lookup"><span data-stu-id="f85c4-154">The default name is **sshuser**.</span></span>
   * <span data-ttu-id="f85c4-155">**Ssh Password**: Enter the SSH user password.</span><span class="sxs-lookup"><span data-stu-id="f85c4-155">**Ssh Password**: Enter the SSH user password.</span></span>
   * <span data-ttu-id="f85c4-156">**Install Script Action**: Keep the default value for going through this tutorial.</span><span class="sxs-lookup"><span data-stu-id="f85c4-156">**Install Script Action**: Keep the default value for going through this tutorial.</span></span>
     
     <span data-ttu-id="f85c4-157">Some properties have been hardcoded in the template: Cluster type, Cluster worker node count, Edge node size, and Edge node name.</span><span class="sxs-lookup"><span data-stu-id="f85c4-157">Some properties have been hardcoded in the template: Cluster type, Cluster worker node count, Edge node size, and Edge node name.</span></span>
4. <span data-ttu-id="f85c4-158">Check **I agree to the terms and conditions stated above**, and then click  **Purchase** to create the cluster with the edge node.</span><span class="sxs-lookup"><span data-stu-id="f85c4-158">Check **I agree to the terms and conditions stated above**, and then click  **Purchase** to create the cluster with the edge node.</span></span>

## <a name="access-an-edge-node"></a><span data-ttu-id="f85c4-159">Access an edge node</span><span class="sxs-lookup"><span data-stu-id="f85c4-159">Access an edge node</span></span>
<span data-ttu-id="f85c4-160">The edge node ssh endpoint is &lt;EdgeNodeName>.&lt;ClusterName>-ssh.azurehdinsight.net:22.</span><span class="sxs-lookup"><span data-stu-id="f85c4-160">The edge node ssh endpoint is &lt;EdgeNodeName>.&lt;ClusterName>-ssh.azurehdinsight.net:22.</span></span>  <span data-ttu-id="f85c4-161">For example, new-edgenode.myedgenode0914-ssh.azurehdinsight.net:22.</span><span class="sxs-lookup"><span data-stu-id="f85c4-161">For example, new-edgenode.myedgenode0914-ssh.azurehdinsight.net:22.</span></span>

<span data-ttu-id="f85c4-162">The edge node appears as an application on the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f85c4-162">The edge node appears as an application on the Azure portal.</span></span>  <span data-ttu-id="f85c4-163">The portal gives you the information to access the edge node using SSH.</span><span class="sxs-lookup"><span data-stu-id="f85c4-163">The portal gives you the information to access the edge node using SSH.</span></span>

<span data-ttu-id="f85c4-164">**To verify the edge node SSH endpoint**</span><span class="sxs-lookup"><span data-stu-id="f85c4-164">**To verify the edge node SSH endpoint**</span></span>

1. <span data-ttu-id="f85c4-165">Sign on to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f85c4-165">Sign on to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f85c4-166">Open the HDInsight cluster with an edge node.</span><span class="sxs-lookup"><span data-stu-id="f85c4-166">Open the HDInsight cluster with an edge node.</span></span>
3. <span data-ttu-id="f85c4-167">Click **Applications** from the cluster blade.</span><span class="sxs-lookup"><span data-stu-id="f85c4-167">Click **Applications** from the cluster blade.</span></span> <span data-ttu-id="f85c4-168">You shall see the edge node.</span><span class="sxs-lookup"><span data-stu-id="f85c4-168">You shall see the edge node.</span></span>  <span data-ttu-id="f85c4-169">The default name is **new-edgenode**.</span><span class="sxs-lookup"><span data-stu-id="f85c4-169">The default name is **new-edgenode**.</span></span>
4. <span data-ttu-id="f85c4-170">Click the edge node.</span><span class="sxs-lookup"><span data-stu-id="f85c4-170">Click the edge node.</span></span> <span data-ttu-id="f85c4-171">You shall see the SSH endpoint.</span><span class="sxs-lookup"><span data-stu-id="f85c4-171">You shall see the SSH endpoint.</span></span>

<span data-ttu-id="f85c4-172">**To use Hive on the edge node**</span><span class="sxs-lookup"><span data-stu-id="f85c4-172">**To use Hive on the edge node**</span></span>

1. <span data-ttu-id="f85c4-173">Use SSH to connect to the edge node.</span><span class="sxs-lookup"><span data-stu-id="f85c4-173">Use SSH to connect to the edge node.</span></span> <span data-ttu-id="f85c4-174">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="f85c4-174">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="f85c4-175">After you have connected to the edge node using SSH, use the following command to open the Hive console:</span><span class="sxs-lookup"><span data-stu-id="f85c4-175">After you have connected to the edge node using SSH, use the following command to open the Hive console:</span></span>
   
        hive
3. <span data-ttu-id="f85c4-176">Run the following command to show Hive tables in the cluster:</span><span class="sxs-lookup"><span data-stu-id="f85c4-176">Run the following command to show Hive tables in the cluster:</span></span>
   
        show tables;

## <a name="delete-an-edge-node"></a><span data-ttu-id="f85c4-177">Delete an edge node</span><span class="sxs-lookup"><span data-stu-id="f85c4-177">Delete an edge node</span></span>
<span data-ttu-id="f85c4-178">You can delete an edge node from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f85c4-178">You can delete an edge node from the Azure portal.</span></span>

<span data-ttu-id="f85c4-179">**To access an edge node**</span><span class="sxs-lookup"><span data-stu-id="f85c4-179">**To access an edge node**</span></span>

1. <span data-ttu-id="f85c4-180">Sign on to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f85c4-180">Sign on to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f85c4-181">Open the HDInsight cluster with an edge node.</span><span class="sxs-lookup"><span data-stu-id="f85c4-181">Open the HDInsight cluster with an edge node.</span></span>
3. <span data-ttu-id="f85c4-182">Click **Applications** from the cluster blade.</span><span class="sxs-lookup"><span data-stu-id="f85c4-182">Click **Applications** from the cluster blade.</span></span> <span data-ttu-id="f85c4-183">You shall see a list of edge nodes.</span><span class="sxs-lookup"><span data-stu-id="f85c4-183">You shall see a list of edge nodes.</span></span>  
4. <span data-ttu-id="f85c4-184">Right-click the edge node you want to delete, and then click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="f85c4-184">Right-click the edge node you want to delete, and then click **Delete**.</span></span>
5. <span data-ttu-id="f85c4-185">Click **Yes** to confirm.</span><span class="sxs-lookup"><span data-stu-id="f85c4-185">Click **Yes** to confirm.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f85c4-186">Next steps</span><span class="sxs-lookup"><span data-stu-id="f85c4-186">Next steps</span></span>
<span data-ttu-id="f85c4-187">In this article, you have learned how to add an edge node and how to access the edge node.</span><span class="sxs-lookup"><span data-stu-id="f85c4-187">In this article, you have learned how to add an edge node and how to access the edge node.</span></span> <span data-ttu-id="f85c4-188">To learn more, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="f85c4-188">To learn more, see the following articles:</span></span>

* <span data-ttu-id="f85c4-189">[Install HDInsight applications](hdinsight-apps-install-applications.md): Learn how to install an HDInsight application to your clusters.</span><span class="sxs-lookup"><span data-stu-id="f85c4-189">[Install HDInsight applications](hdinsight-apps-install-applications.md): Learn how to install an HDInsight application to your clusters.</span></span>
* <span data-ttu-id="f85c4-190">[Install custom HDInsight applications](hdinsight-apps-install-custom-applications.md): learn how to deploy an unpublished HDInsight application to HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f85c4-190">[Install custom HDInsight applications](hdinsight-apps-install-custom-applications.md): learn how to deploy an unpublished HDInsight application to HDInsight.</span></span>
* <span data-ttu-id="f85c4-191">[Publish HDInsight applications](hdinsight-apps-publish-applications.md): Learn how to publish your custom HDInsight applications to Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="f85c4-191">[Publish HDInsight applications](hdinsight-apps-publish-applications.md): Learn how to publish your custom HDInsight applications to Azure Marketplace.</span></span>
* <span data-ttu-id="f85c4-192">[MSDN: Install an HDInsight application](https://msdn.microsoft.com/library/mt706515.aspx): Learn how to define HDInsight applications.</span><span class="sxs-lookup"><span data-stu-id="f85c4-192">[MSDN: Install an HDInsight application](https://msdn.microsoft.com/library/mt706515.aspx): Learn how to define HDInsight applications.</span></span>
* <span data-ttu-id="f85c4-193">[Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md): learn how to use Script Action to install additional applications.</span><span class="sxs-lookup"><span data-stu-id="f85c4-193">[Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md): learn how to use Script Action to install additional applications.</span></span>
* <span data-ttu-id="f85c4-194">[Create Linux-based Hadoop clusters in HDInsight using Resource Manager templates](hdinsight-hadoop-create-linux-clusters-arm-templates.md): learn how to call Resource Manager templates to create HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="f85c4-194">[Create Linux-based Hadoop clusters in HDInsight using Resource Manager templates](hdinsight-hadoop-create-linux-clusters-arm-templates.md): learn how to call Resource Manager templates to create HDInsight clusters.</span></span>



