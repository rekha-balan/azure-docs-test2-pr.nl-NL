---
title: Create Azure HDInsight (Hadoop) using PowerShell | Microsoft Docs
description: Learn how to create Hadoop, HBase, Storm, or Spark clusters on Linux for HDInsight by using Azure PowerShell.
services: hdinsight
documentationcenter: ''
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 4208deca-d64a-45e1-8948-2673d5d7678c
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 02/06/2017
ms.author: nitinme
ms.openlocfilehash: a9bd1938c6b0aad2c08d063fd892fea2f8aad56e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553999"
---
# <a name="create-linux-based-clusters-in-hdinsight-using-azure-powershell"></a><span data-ttu-id="80daf-103">Create Linux-based clusters in HDInsight using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="80daf-103">Create Linux-based clusters in HDInsight using Azure PowerShell</span></span>

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="80daf-104">Azure PowerShell is a powerful scripting environment that you can use to control and automate the deployment and management of your workloads in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="80daf-104">Azure PowerShell is a powerful scripting environment that you can use to control and automate the deployment and management of your workloads in Microsoft Azure.</span></span> <span data-ttu-id="80daf-105">This document provides information about how to create a Linux-based HDInsight cluster by using Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="80daf-105">This document provides information about how to create a Linux-based HDInsight cluster by using Azure PowerShell.</span></span> <span data-ttu-id="80daf-106">It also includes an example script.</span><span class="sxs-lookup"><span data-stu-id="80daf-106">It also includes an example script.</span></span>

> [!NOTE]
> <span data-ttu-id="80daf-107">Azure PowerShell is only available on Windows clients.</span><span class="sxs-lookup"><span data-stu-id="80daf-107">Azure PowerShell is only available on Windows clients.</span></span> <span data-ttu-id="80daf-108">If you are using a Linux, Unix, or Mac OS X client, see [Create a Linux-based HDInsight cluster using Azure CLI](hdinsight-hadoop-create-linux-clusters-azure-cli.md) for information about using the Azure CLI to create a cluster.</span><span class="sxs-lookup"><span data-stu-id="80daf-108">If you are using a Linux, Unix, or Mac OS X client, see [Create a Linux-based HDInsight cluster using Azure CLI](hdinsight-hadoop-create-linux-clusters-azure-cli.md) for information about using the Azure CLI to create a cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="80daf-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="80daf-109">Prerequisites</span></span>
<span data-ttu-id="80daf-110">You must have the following before starting this procedure:</span><span class="sxs-lookup"><span data-stu-id="80daf-110">You must have the following before starting this procedure:</span></span>

* <span data-ttu-id="80daf-111">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="80daf-111">An Azure subscription.</span></span> <span data-ttu-id="80daf-112">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="80daf-112">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* [<span data-ttu-id="80daf-113">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="80daf-113">Azure PowerShell</span></span>](https://docs.microsoft.com/powershell/azure/install-azurerm-ps)

    > [!IMPORTANT]
    > <span data-ttu-id="80daf-114">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and was removed on January 1, 2017.</span><span class="sxs-lookup"><span data-stu-id="80daf-114">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and was removed on January 1, 2017.</span></span> <span data-ttu-id="80daf-115">The steps in this document use the new HDInsight cmdlets that work with Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="80daf-115">The steps in this document use the new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="80daf-116">Please follow the steps in [Install Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) to install the latest version of Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="80daf-116">Please follow the steps in [Install Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) to install the latest version of Azure PowerShell.</span></span> <span data-ttu-id="80daf-117">If you have scripts that need to be modified to use the new cmdlets that work with Azure Resource Manager, see [Migrating to Azure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span><span class="sxs-lookup"><span data-stu-id="80daf-117">If you have scripts that need to be modified to use the new cmdlets that work with Azure Resource Manager, see [Migrating to Azure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

### <a name="access-control-requirements"></a><span data-ttu-id="80daf-118">Access control requirements</span><span class="sxs-lookup"><span data-stu-id="80daf-118">Access control requirements</span></span>

[!INCLUDE [access-control](../../includes/hdinsight-access-control-requirements.md)]

## <a name="create-cluster"></a><span data-ttu-id="80daf-119">Create cluster</span><span class="sxs-lookup"><span data-stu-id="80daf-119">Create cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="80daf-120">To create an HDInsight cluster by using Azure PowerShell, you must complete the following procedures:</span><span class="sxs-lookup"><span data-stu-id="80daf-120">To create an HDInsight cluster by using Azure PowerShell, you must complete the following procedures:</span></span>

* <span data-ttu-id="80daf-121">Create an Azure resource group</span><span class="sxs-lookup"><span data-stu-id="80daf-121">Create an Azure resource group</span></span>
* <span data-ttu-id="80daf-122">Create an Azure Storage account</span><span class="sxs-lookup"><span data-stu-id="80daf-122">Create an Azure Storage account</span></span>
* <span data-ttu-id="80daf-123">Create an Azure Blob container</span><span class="sxs-lookup"><span data-stu-id="80daf-123">Create an Azure Blob container</span></span>
* <span data-ttu-id="80daf-124">Create an HDInsight cluster</span><span class="sxs-lookup"><span data-stu-id="80daf-124">Create an HDInsight cluster</span></span>

<span data-ttu-id="80daf-125">The two most important parameters that you must set to create Linux clusters are the ones that specify the OS type and the SSH user details:</span><span class="sxs-lookup"><span data-stu-id="80daf-125">The two most important parameters that you must set to create Linux clusters are the ones that specify the OS type and the SSH user details:</span></span>

* <span data-ttu-id="80daf-126">Make sure you specify the **-OSType** parameter as **Linux**.</span><span class="sxs-lookup"><span data-stu-id="80daf-126">Make sure you specify the **-OSType** parameter as **Linux**.</span></span>
* <span data-ttu-id="80daf-127">To use SSH for remote sessions on the clusters, you can specify the SSH user password or the SSH public key.</span><span class="sxs-lookup"><span data-stu-id="80daf-127">To use SSH for remote sessions on the clusters, you can specify the SSH user password or the SSH public key.</span></span> <span data-ttu-id="80daf-128">If you specify both the SSH user password and the SSH public key, the key will be ignored.</span><span class="sxs-lookup"><span data-stu-id="80daf-128">If you specify both the SSH user password and the SSH public key, the key will be ignored.</span></span> <span data-ttu-id="80daf-129">If you want to use the SSH key for remote sessions, you must specify a blank SSH password when prompted for one.</span><span class="sxs-lookup"><span data-stu-id="80daf-129">If you want to use the SSH key for remote sessions, you must specify a blank SSH password when prompted for one.</span></span> <span data-ttu-id="80daf-130">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="80daf-130">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="80daf-131">The following script demonstrates how to create a new cluster:</span><span class="sxs-lookup"><span data-stu-id="80daf-131">The following script demonstrates how to create a new cluster:</span></span>

    $token ="<SpecifyAnUniqueString>"
    $subscriptionID = "<SubscriptionName>"        # Provide your Subscription Name

    $resourceGroupName = $token + "rg"      # Provide a Resource Group name
    $clusterName = $token
    $defaultStorageAccountName = $token + "store"   # Provide a Storage account name
    $defaultStorageContainerName = $token + "container"
    $location = "East US 2"     # Change the location if needed
    $clusterNodes = 1           # The number of nodes in the HDInsight cluster

    # Sign in to Azure
    Login-AzureRmAccount

    # Select the subscription to use if you have multiple subscriptions
    Select-AzureRmSubscription -SubscriptionId $subscriptionID

    # Create an Azure Resource Group
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location

    # Create an Azure Storage account and container used as the default storage
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -StorageAccountName $defaultStorageAccountName `
        -Location $location `
        -Type Standard_LRS
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -Name $defaultStorageAccountName -ResourceGroupName $resourceGroupName)[0].Value
    $destContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey
    New-AzureStorageContainer -Name $defaultStorageContainerName -Context $destContext

    # Create an HDInsight cluster
    $credentials = Get-Credential -Message "Enter Cluster user credentials" -UserName "admin"
    $sshCredentials = Get-Credential -Message "Enter SSH user credentials"

    # The location of the HDInsight cluster must be in the same data center as the Storage account.
    $location = Get-AzureRmStorageAccount -ResourceGroupName $resourceGroupName -StorageAccountName $defaultStorageAccountName | %{$_.Location}

    New-AzureRmHDInsightCluster `
        -ClusterName $clusterName `
        -ResourceGroupName $resourceGroupName `
        -HttpCredential $credentials `
        -Location $location `
        -DefaultStorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultStorageContainer $defaultStorageContainerName  `
        -ClusterSizeInNodes $clusterNodes `
        -ClusterType Hadoop `
        -OSType Linux `
        -Version "3.4" `
        -SshCredential $sshCredentials

<span data-ttu-id="80daf-132">The values you specify for **$clusterCredentials** are used to create the Hadoop user account for the cluster.</span><span class="sxs-lookup"><span data-stu-id="80daf-132">The values you specify for **$clusterCredentials** are used to create the Hadoop user account for the cluster.</span></span> <span data-ttu-id="80daf-133">Use this account to connect to the cluster.</span><span class="sxs-lookup"><span data-stu-id="80daf-133">Use this account to connect to the cluster.</span></span>

<span data-ttu-id="80daf-134">The values you specify for **$sshCredentials** are used to create the SSH user for the cluster.</span><span class="sxs-lookup"><span data-stu-id="80daf-134">The values you specify for **$sshCredentials** are used to create the SSH user for the cluster.</span></span> <span data-ttu-id="80daf-135">Use this account to start a remote SSH session on the cluster and run jobs.</span><span class="sxs-lookup"><span data-stu-id="80daf-135">Use this account to start a remote SSH session on the cluster and run jobs.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="80daf-136">In this script, you must specify the number of worker nodes that will be in the cluster.</span><span class="sxs-lookup"><span data-stu-id="80daf-136">In this script, you must specify the number of worker nodes that will be in the cluster.</span></span> <span data-ttu-id="80daf-137">If you plan to use more than 32 worker nodes (either at cluster creation or by scaling the cluster after creation), you must also specify a head node size with at least 8 cores and 14 GB of RAM.</span><span class="sxs-lookup"><span data-stu-id="80daf-137">If you plan to use more than 32 worker nodes (either at cluster creation or by scaling the cluster after creation), you must also specify a head node size with at least 8 cores and 14 GB of RAM.</span></span>
>
> <span data-ttu-id="80daf-138">For more information on node sizes and associated costs, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="80daf-138">For more information on node sizes and associated costs, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

<span data-ttu-id="80daf-139">It can take up to 20 minutes to create a cluster.</span><span class="sxs-lookup"><span data-stu-id="80daf-139">It can take up to 20 minutes to create a cluster.</span></span>

## <a name="create-cluster-configuration-object"></a><span data-ttu-id="80daf-140">Create cluster: Configuration object</span><span class="sxs-lookup"><span data-stu-id="80daf-140">Create cluster: Configuration object</span></span>

<span data-ttu-id="80daf-141">You can also create an HDInsight configuration object using `New-AzureRmHDInsightClusterConfig` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="80daf-141">You can also create an HDInsight configuration object using `New-AzureRmHDInsightClusterConfig` cmdlet.</span></span> <span data-ttu-id="80daf-142">You can then modify this configuration object to enable additional configuration options for your cluster.</span><span class="sxs-lookup"><span data-stu-id="80daf-142">You can then modify this configuration object to enable additional configuration options for your cluster.</span></span> <span data-ttu-id="80daf-143">Finally, use the `-Config` parameter of the `New-AzureRmHDInsightCluster` cmdlet to use the configuration.</span><span class="sxs-lookup"><span data-stu-id="80daf-143">Finally, use the `-Config` parameter of the `New-AzureRmHDInsightCluster` cmdlet to use the configuration.</span></span>

<span data-ttu-id="80daf-144">The following script creates a configuration object to configure an R Server on HDInsight cluster type.</span><span class="sxs-lookup"><span data-stu-id="80daf-144">The following script creates a configuration object to configure an R Server on HDInsight cluster type.</span></span> <span data-ttu-id="80daf-145">The configuration enables an edge node, RStudio, and an additional storage account.</span><span class="sxs-lookup"><span data-stu-id="80daf-145">The configuration enables an edge node, RStudio, and an additional storage account.</span></span>

    # Create another storage account used as additional storage account
    $additionalStorageAccountName = $token + "store2"
    New-AzureRmStorageAccount -ResourceGroupName $resourceGroupName `
        -StorageAccountName $additionalStorageAccountName `
        -Location $location `
        -Type Standard_LRS
    $additionalStorageAccountKey = (Get-AzureRmStorageAccountKey -Name $additionalStorageAccountName -ResourceGroupName $resourceGroupName)[0].Value

    # Create a new configuration for RServer cluster type
    # Use -EdgeNodeSize to set the size of the edge node for RServer clusters
    # if you want a specific size. Otherwise, the default size is used.
    $config = New-AzureRmHDInsightClusterConfig `
        -ClusterType "RServer" `
        -EdgeNodeSize "Standard_D12_v2"

    # Add RStudio to the configuration
    $rserverConfig = @{"RStudio"="true"}
    $config = $config | Add-AzureRmHDInsightConfigValues `
        -RServer $rserverConfig

    # Add an additional storage account
    Add-AzureRmHDInsightStorage -Config $config -StorageAccountName "$additionalStorageAccountName.blob.core.windows.net" -StorageAccountKey $additionalStorageAccountKey

    # Create a new HDInsight cluster
    New-AzureRmHDInsightCluster `
        -ClusterName $clusterName `
        -ResourceGroupName $resourceGroupName `
        -HttpCredential $credentials `
        -Location $location `
        -DefaultStorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultStorageContainer $defaultStorageContainerName  `
        -ClusterSizeInNodes $clusterNodes `
        -OSType Linux `
        -Version "3.5" `
        -SshCredential $sshCredentials `
        -Config $config

> [!WARNING]
> <span data-ttu-id="80daf-146">Using a storage account in a different location than the HDInsight cluster is not supported.</span><span class="sxs-lookup"><span data-stu-id="80daf-146">Using a storage account in a different location than the HDInsight cluster is not supported.</span></span> <span data-ttu-id="80daf-147">When using this example, create the additional storage account in the same location as the server.</span><span class="sxs-lookup"><span data-stu-id="80daf-147">When using this example, create the additional storage account in the same location as the server.</span></span>

## <a name="customize-clusters"></a><span data-ttu-id="80daf-148">Customize clusters</span><span class="sxs-lookup"><span data-stu-id="80daf-148">Customize clusters</span></span>

* <span data-ttu-id="80daf-149">See [Customize HDInsight clusters using Bootstrap](hdinsight-hadoop-customize-cluster-bootstrap.md#use-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="80daf-149">See [Customize HDInsight clusters using Bootstrap](hdinsight-hadoop-customize-cluster-bootstrap.md#use-azure-powershell).</span></span>
* <span data-ttu-id="80daf-150">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="80daf-150">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

## <a name="delete-the-cluster"></a><span data-ttu-id="80daf-151">Delete the cluster</span><span class="sxs-lookup"><span data-stu-id="80daf-151">Delete the cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="80daf-152">Next steps</span><span class="sxs-lookup"><span data-stu-id="80daf-152">Next steps</span></span>

<span data-ttu-id="80daf-153">Now that you have successfully created an HDInsight cluster, use the following resources to learn how to work with your cluster.</span><span class="sxs-lookup"><span data-stu-id="80daf-153">Now that you have successfully created an HDInsight cluster, use the following resources to learn how to work with your cluster.</span></span>

### <a name="hadoop-clusters"></a><span data-ttu-id="80daf-154">Hadoop clusters</span><span class="sxs-lookup"><span data-stu-id="80daf-154">Hadoop clusters</span></span>

* [<span data-ttu-id="80daf-155">Use Hive with HDInsight</span><span class="sxs-lookup"><span data-stu-id="80daf-155">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="80daf-156">Use Pig with HDInsight</span><span class="sxs-lookup"><span data-stu-id="80daf-156">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="80daf-157">Use MapReduce with HDInsight</span><span class="sxs-lookup"><span data-stu-id="80daf-157">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a><span data-ttu-id="80daf-158">HBase clusters</span><span class="sxs-lookup"><span data-stu-id="80daf-158">HBase clusters</span></span>

* [<span data-ttu-id="80daf-159">Get started with HBase on HDInsight</span><span class="sxs-lookup"><span data-stu-id="80daf-159">Get started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started-linux.md)
* [<span data-ttu-id="80daf-160">Develop Java applications for HBase on HDInsight</span><span class="sxs-lookup"><span data-stu-id="80daf-160">Develop Java applications for HBase on HDInsight</span></span>](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a><span data-ttu-id="80daf-161">Storm clusters</span><span class="sxs-lookup"><span data-stu-id="80daf-161">Storm clusters</span></span>

* [<span data-ttu-id="80daf-162">Develop Java topologies for Storm on HDInsight</span><span class="sxs-lookup"><span data-stu-id="80daf-162">Develop Java topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="80daf-163">Use Python components in Storm on HDInsight</span><span class="sxs-lookup"><span data-stu-id="80daf-163">Use Python components in Storm on HDInsight</span></span>](hdinsight-storm-develop-python-topology.md)
* [<span data-ttu-id="80daf-164">Deploy and monitor topologies with Storm on HDInsight</span><span class="sxs-lookup"><span data-stu-id="80daf-164">Deploy and monitor topologies with Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology-linux.md)

### <a name="spark-clusters"></a><span data-ttu-id="80daf-165">Spark clusters</span><span class="sxs-lookup"><span data-stu-id="80daf-165">Spark clusters</span></span>

* [<span data-ttu-id="80daf-166">Create a standalone application using Scala</span><span class="sxs-lookup"><span data-stu-id="80daf-166">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="80daf-167">Run jobs remotely on a Spark cluster using Livy</span><span class="sxs-lookup"><span data-stu-id="80daf-167">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)
* [<span data-ttu-id="80daf-168">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span><span class="sxs-lookup"><span data-stu-id="80daf-168">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="80daf-169">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span><span class="sxs-lookup"><span data-stu-id="80daf-169">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="80daf-170">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span><span class="sxs-lookup"><span data-stu-id="80daf-170">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)

