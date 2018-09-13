---
title: Create Azure HDInsight (Hadoop) using the command-line | Microsoft Docs
description: Learn how to create HDInsight clusters using the cross-platform Azure CLI 1.0.
services: hdinsight
documentationcenter: ''
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 50b01483-455c-4d87-b754-2229005a8ab9
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/04/2017
ms.author: larryfr
ms.openlocfilehash: 995aacb5d243eb50df0cf35e68a1a931bd010c53
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554208"
---
# <a name="create-hdinsight-clusters-using-the-azure-cli"></a><span data-ttu-id="7c30a-103">Create HDInsight clusters using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="7c30a-103">Create HDInsight clusters using the Azure CLI</span></span>

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="7c30a-104">The steps in this document walk-through creating a HDInsight 3.5 cluster using the Azure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="7c30a-104">The steps in this document walk-through creating a HDInsight 3.5 cluster using the Azure CLI 1.0.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7c30a-105">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="7c30a-105">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="7c30a-106">For more information, see [HDInsight 3.2 and 3.3 deprecation](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span><span class="sxs-lookup"><span data-stu-id="7c30a-106">For more information, see [HDInsight 3.2 and 3.3 deprecation](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="7c30a-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="7c30a-107">Prerequisites</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

* <span data-ttu-id="7c30a-108">**An Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="7c30a-108">**An Azure subscription**.</span></span> <span data-ttu-id="7c30a-109">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="7c30a-109">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

* <span data-ttu-id="7c30a-110">**Azure CLI**.</span><span class="sxs-lookup"><span data-stu-id="7c30a-110">**Azure CLI**.</span></span> <span data-ttu-id="7c30a-111">The steps in this document were last tested with Azure CLI version 0.10.1.</span><span class="sxs-lookup"><span data-stu-id="7c30a-111">The steps in this document were last tested with Azure CLI version 0.10.1.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="7c30a-112">The steps in this document do not work with Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="7c30a-112">The steps in this document do not work with Azure CLI 2.0.</span></span> <span data-ttu-id="7c30a-113">Azure CLI 2.0 does not support creating an HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="7c30a-113">Azure CLI 2.0 does not support creating an HDInsight cluster.</span></span>

### <a name="access-control-requirements"></a><span data-ttu-id="7c30a-114">Access control requirements</span><span class="sxs-lookup"><span data-stu-id="7c30a-114">Access control requirements</span></span>

[!INCLUDE [access-control](../../includes/hdinsight-access-control-requirements.md)]

## <a name="log-in-to-your-azure-subscription"></a><span data-ttu-id="7c30a-115">Log in to your Azure subscription</span><span class="sxs-lookup"><span data-stu-id="7c30a-115">Log in to your Azure subscription</span></span>

<span data-ttu-id="7c30a-116">Follow the steps documented in [Connect to an Azure subscription from the Azure Command-Line Interface (Azure CLI)](../xplat-cli-connect.md) and connect to your subscription using the **login** method.</span><span class="sxs-lookup"><span data-stu-id="7c30a-116">Follow the steps documented in [Connect to an Azure subscription from the Azure Command-Line Interface (Azure CLI)](../xplat-cli-connect.md) and connect to your subscription using the **login** method.</span></span>

## <a name="create-a-cluster"></a><span data-ttu-id="7c30a-117">Create a cluster</span><span class="sxs-lookup"><span data-stu-id="7c30a-117">Create a cluster</span></span>

<span data-ttu-id="7c30a-118">The following steps should be performed from a command-prompt, shell, or terminal session after installing and configuring the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="7c30a-118">The following steps should be performed from a command-prompt, shell, or terminal session after installing and configuring the Azure CLI.</span></span>

1. <span data-ttu-id="7c30a-119">Use the following command to authenticate to your Azure subscription:</span><span class="sxs-lookup"><span data-stu-id="7c30a-119">Use the following command to authenticate to your Azure subscription:</span></span>

        azure login

    <span data-ttu-id="7c30a-120">You are prompted to provide your name and password.</span><span class="sxs-lookup"><span data-stu-id="7c30a-120">You are prompted to provide your name and password.</span></span> <span data-ttu-id="7c30a-121">If you have multiple Azure subscriptions, use `azure account set <subscriptionname>` to set the subscription that the Azure CLI commands use.</span><span class="sxs-lookup"><span data-stu-id="7c30a-121">If you have multiple Azure subscriptions, use `azure account set <subscriptionname>` to set the subscription that the Azure CLI commands use.</span></span>

2. <span data-ttu-id="7c30a-122">Switch to Azure Resource Manager mode using the following command:</span><span class="sxs-lookup"><span data-stu-id="7c30a-122">Switch to Azure Resource Manager mode using the following command:</span></span>

        azure config mode arm

3. <span data-ttu-id="7c30a-123">Create a resource group.</span><span class="sxs-lookup"><span data-stu-id="7c30a-123">Create a resource group.</span></span> <span data-ttu-id="7c30a-124">This resource group contains the HDInsight cluster and associated storage account.</span><span class="sxs-lookup"><span data-stu-id="7c30a-124">This resource group contains the HDInsight cluster and associated storage account.</span></span>

        azure group create groupname location

    * <span data-ttu-id="7c30a-125">Replace **groupname** with a unique name for the group.</span><span class="sxs-lookup"><span data-stu-id="7c30a-125">Replace **groupname** with a unique name for the group.</span></span>

    * <span data-ttu-id="7c30a-126">Replace **location** with the geographic region that you want to create the group in.</span><span class="sxs-lookup"><span data-stu-id="7c30a-126">Replace **location** with the geographic region that you want to create the group in.</span></span>

       <span data-ttu-id="7c30a-127">For a list of valid locations, use the `azure location list` command, and then use one of the locations from the **Name** column.</span><span class="sxs-lookup"><span data-stu-id="7c30a-127">For a list of valid locations, use the `azure location list` command, and then use one of the locations from the **Name** column.</span></span>

4. <span data-ttu-id="7c30a-128">Create a storage account.</span><span class="sxs-lookup"><span data-stu-id="7c30a-128">Create a storage account.</span></span> <span data-ttu-id="7c30a-129">This storage account is used as the default storage for the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="7c30a-129">This storage account is used as the default storage for the HDInsight cluster.</span></span>

        azure storage account create -g groupname --sku-name RAGRS -l location --kind Storage storagename

    * <span data-ttu-id="7c30a-130">Replace **groupname** with the name of the group created in the previous step.</span><span class="sxs-lookup"><span data-stu-id="7c30a-130">Replace **groupname** with the name of the group created in the previous step.</span></span>

    * <span data-ttu-id="7c30a-131">Replace **location** with the same location used in the previous step.</span><span class="sxs-lookup"><span data-stu-id="7c30a-131">Replace **location** with the same location used in the previous step.</span></span>

    * <span data-ttu-id="7c30a-132">Replace **storagename** with a unique name for the storage account.</span><span class="sxs-lookup"><span data-stu-id="7c30a-132">Replace **storagename** with a unique name for the storage account.</span></span>

        > [!NOTE]
        > <span data-ttu-id="7c30a-133">For more information on the parameters used in this command, use `azure storage account create -h` to view help for this command.</span><span class="sxs-lookup"><span data-stu-id="7c30a-133">For more information on the parameters used in this command, use `azure storage account create -h` to view help for this command.</span></span>

5. <span data-ttu-id="7c30a-134">Retrieve the key used to access the storage account.</span><span class="sxs-lookup"><span data-stu-id="7c30a-134">Retrieve the key used to access the storage account.</span></span>

        azure storage account keys list -g groupname storagename

    * <span data-ttu-id="7c30a-135">Replace **groupname** with the resource group name.</span><span class="sxs-lookup"><span data-stu-id="7c30a-135">Replace **groupname** with the resource group name.</span></span>
    * <span data-ttu-id="7c30a-136">Replace **storagename** with the name of the storage account.</span><span class="sxs-lookup"><span data-stu-id="7c30a-136">Replace **storagename** with the name of the storage account.</span></span>

     <span data-ttu-id="7c30a-137">In the data that is returned, save the **key** value for **key1**.</span><span class="sxs-lookup"><span data-stu-id="7c30a-137">In the data that is returned, save the **key** value for **key1**.</span></span>

6. <span data-ttu-id="7c30a-138">Create an HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="7c30a-138">Create an HDInsight cluster.</span></span>

        azure hdinsight cluster create -g groupname -l location -y Linux --clusterType Hadoop --defaultStorageAccountName storagename.blob.core.windows.net --defaultStorageAccountKey storagekey --defaultStorageContainer clustername --workerNodeCount 2 --userName admin --password httppassword --sshUserName sshuser --sshPassword sshuserpassword clustername

    * <span data-ttu-id="7c30a-139">Replace **groupname** with the resource group name.</span><span class="sxs-lookup"><span data-stu-id="7c30a-139">Replace **groupname** with the resource group name.</span></span>

    * <span data-ttu-id="7c30a-140">Replace **Hadoop** with the cluster type that you wish to create.</span><span class="sxs-lookup"><span data-stu-id="7c30a-140">Replace **Hadoop** with the cluster type that you wish to create.</span></span> <span data-ttu-id="7c30a-141">For example, Hadoop, HBase, Storm, or Spark.</span><span class="sxs-lookup"><span data-stu-id="7c30a-141">For example, Hadoop, HBase, Storm, or Spark.</span></span>

     > [!IMPORTANT]
     > <span data-ttu-id="7c30a-142">HDInsight clusters come in various types, which correspond to the workload or technology that the cluster is tuned for.</span><span class="sxs-lookup"><span data-stu-id="7c30a-142">HDInsight clusters come in various types, which correspond to the workload or technology that the cluster is tuned for.</span></span> <span data-ttu-id="7c30a-143">There is no supported method to create a cluster that combines multiple types, such as Storm and HBase on one cluster.</span><span class="sxs-lookup"><span data-stu-id="7c30a-143">There is no supported method to create a cluster that combines multiple types, such as Storm and HBase on one cluster.</span></span>

    * <span data-ttu-id="7c30a-144">Replace **location** with the same location used in previous steps.</span><span class="sxs-lookup"><span data-stu-id="7c30a-144">Replace **location** with the same location used in previous steps.</span></span>

    * <span data-ttu-id="7c30a-145">Replace **storagename** with the storage account name.</span><span class="sxs-lookup"><span data-stu-id="7c30a-145">Replace **storagename** with the storage account name.</span></span>

    * <span data-ttu-id="7c30a-146">Replace **storagekey** with the key obtained in the previous step.</span><span class="sxs-lookup"><span data-stu-id="7c30a-146">Replace **storagekey** with the key obtained in the previous step.</span></span>

    * <span data-ttu-id="7c30a-147">For the `--defaultStorageContainer` parameter, use the same name as you are using for the cluster.</span><span class="sxs-lookup"><span data-stu-id="7c30a-147">For the `--defaultStorageContainer` parameter, use the same name as you are using for the cluster.</span></span>

    * <span data-ttu-id="7c30a-148">Replace **admin** and **httppassword** with the name and password you wish to use when accessing the cluster through HTTPS.</span><span class="sxs-lookup"><span data-stu-id="7c30a-148">Replace **admin** and **httppassword** with the name and password you wish to use when accessing the cluster through HTTPS.</span></span>

    * <span data-ttu-id="7c30a-149">Replace **sshuser** and **sshuserpassword** with the username and password you wish to use when accessing the cluster using SSH</span><span class="sxs-lookup"><span data-stu-id="7c30a-149">Replace **sshuser** and **sshuserpassword** with the username and password you wish to use when accessing the cluster using SSH</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="7c30a-150">This example creates a cluster with two worker notes.</span><span class="sxs-lookup"><span data-stu-id="7c30a-150">This example creates a cluster with two worker notes.</span></span> <span data-ttu-id="7c30a-151">If you plan on more than 32 worker nodes (during cluster creation or by scaling the cluster,) then you must select a head node size with at least 8 cores and 14-GB RAM.</span><span class="sxs-lookup"><span data-stu-id="7c30a-151">If you plan on more than 32 worker nodes (during cluster creation or by scaling the cluster,) then you must select a head node size with at least 8 cores and 14-GB RAM.</span></span> <span data-ttu-id="7c30a-152">You can set the head node size by using the `--headNodeSize` parameter.</span><span class="sxs-lookup"><span data-stu-id="7c30a-152">You can set the head node size by using the `--headNodeSize` parameter.</span></span>
    >
    > <span data-ttu-id="7c30a-153">For more information on node sizes and associated costs, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="7c30a-153">For more information on node sizes and associated costs, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

    <span data-ttu-id="7c30a-154">It may take several minutes for the cluster creation process to finish.</span><span class="sxs-lookup"><span data-stu-id="7c30a-154">It may take several minutes for the cluster creation process to finish.</span></span> <span data-ttu-id="7c30a-155">Usually around 15.</span><span class="sxs-lookup"><span data-stu-id="7c30a-155">Usually around 15.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7c30a-156">Next steps</span><span class="sxs-lookup"><span data-stu-id="7c30a-156">Next steps</span></span>

<span data-ttu-id="7c30a-157">Now that you have successfully created an HDInsight cluster using the Azure CLI, use the following to learn how to work with your cluster:</span><span class="sxs-lookup"><span data-stu-id="7c30a-157">Now that you have successfully created an HDInsight cluster using the Azure CLI, use the following to learn how to work with your cluster:</span></span>

### <a name="hadoop-clusters"></a><span data-ttu-id="7c30a-158">Hadoop clusters</span><span class="sxs-lookup"><span data-stu-id="7c30a-158">Hadoop clusters</span></span>

* [<span data-ttu-id="7c30a-159">Use Hive with HDInsight</span><span class="sxs-lookup"><span data-stu-id="7c30a-159">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="7c30a-160">Use Pig with HDInsight</span><span class="sxs-lookup"><span data-stu-id="7c30a-160">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="7c30a-161">Use MapReduce with HDInsight</span><span class="sxs-lookup"><span data-stu-id="7c30a-161">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a><span data-ttu-id="7c30a-162">HBase clusters</span><span class="sxs-lookup"><span data-stu-id="7c30a-162">HBase clusters</span></span>

* [<span data-ttu-id="7c30a-163">Get started with HBase on HDInsight</span><span class="sxs-lookup"><span data-stu-id="7c30a-163">Get started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started-linux.md)
* [<span data-ttu-id="7c30a-164">Develop Java applications for HBase on HDInsight</span><span class="sxs-lookup"><span data-stu-id="7c30a-164">Develop Java applications for HBase on HDInsight</span></span>](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a><span data-ttu-id="7c30a-165">Storm clusters</span><span class="sxs-lookup"><span data-stu-id="7c30a-165">Storm clusters</span></span>

* [<span data-ttu-id="7c30a-166">Develop Java topologies for Storm on HDInsight</span><span class="sxs-lookup"><span data-stu-id="7c30a-166">Develop Java topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="7c30a-167">Use Python components in Storm on HDInsight</span><span class="sxs-lookup"><span data-stu-id="7c30a-167">Use Python components in Storm on HDInsight</span></span>](hdinsight-storm-develop-python-topology.md)
* [<span data-ttu-id="7c30a-168">Deploy and monitor topologies with Storm on HDInsight</span><span class="sxs-lookup"><span data-stu-id="7c30a-168">Deploy and monitor topologies with Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology-linux.md)
