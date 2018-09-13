---
title: Create Hadoop cluster with secure transfer storage accounts in Azure HDInsight
description: Learn how to create HDInsight clusters with secure transfer enabled Azure storage accounts.
services: hdinsight
author: jasonwhowell
ms.author: jasonh
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 07/24/2018
ms.openlocfilehash: 253455d892d38a6e8356b775306b238ebd566da4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869543"
---
# <a name="create-hadoop-cluster-with-secure-transfer-storage-accounts-in-azure-hdinsight"></a><span data-ttu-id="a8f1d-103">Create Hadoop cluster with secure transfer storage accounts in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="a8f1d-103">Create Hadoop cluster with secure transfer storage accounts in Azure HDInsight</span></span>

<span data-ttu-id="a8f1d-104">The [Secure transfer required](../storage/common/storage-require-secure-transfer.md) feature enhances the security of your Azure Storage account by enforcing all requests to your account through a secure connection.</span><span class="sxs-lookup"><span data-stu-id="a8f1d-104">The [Secure transfer required](../storage/common/storage-require-secure-transfer.md) feature enhances the security of your Azure Storage account by enforcing all requests to your account through a secure connection.</span></span> <span data-ttu-id="a8f1d-105">This feature and the wasbs scheme are only supported by HDInsight cluster version 3.6 or newer.</span><span class="sxs-lookup"><span data-stu-id="a8f1d-105">This feature and the wasbs scheme are only supported by HDInsight cluster version 3.6 or newer.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="a8f1d-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a8f1d-106">Prerequisites</span></span>
<span data-ttu-id="a8f1d-107">Before you begin this tutorial, you must have:</span><span class="sxs-lookup"><span data-stu-id="a8f1d-107">Before you begin this tutorial, you must have:</span></span>

* <span data-ttu-id="a8f1d-108">**Azure subscription**: To create a free one-month trial account, browse to [azure.microsoft.com/free](https://azure.microsoft.com/free).</span><span class="sxs-lookup"><span data-stu-id="a8f1d-108">**Azure subscription**: To create a free one-month trial account, browse to [azure.microsoft.com/free](https://azure.microsoft.com/free).</span></span>
* <span data-ttu-id="a8f1d-109">**An Azure Storage account with secure transfer enabled**.</span><span class="sxs-lookup"><span data-stu-id="a8f1d-109">**An Azure Storage account with secure transfer enabled**.</span></span> <span data-ttu-id="a8f1d-110">For the instructions, see [Create a storage account](../storage/common/storage-quickstart-create-account.md) and [Require secure transfer](../storage/common/storage-require-secure-transfer.md).</span><span class="sxs-lookup"><span data-stu-id="a8f1d-110">For the instructions, see [Create a storage account](../storage/common/storage-quickstart-create-account.md) and [Require secure transfer](../storage/common/storage-require-secure-transfer.md).</span></span>
* <span data-ttu-id="a8f1d-111">**A Blob container on the storage account**.</span><span class="sxs-lookup"><span data-stu-id="a8f1d-111">**A Blob container on the storage account**.</span></span> 

## <a name="create-cluster"></a><span data-ttu-id="a8f1d-112">Create cluster</span><span class="sxs-lookup"><span data-stu-id="a8f1d-112">Create cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]


<span data-ttu-id="a8f1d-113">In this section, you create a Hadoop cluster in HDInsight using an [Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="a8f1d-113">In this section, you create a Hadoop cluster in HDInsight using an [Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span> <span data-ttu-id="a8f1d-114">The template is located in [Github](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-existing-default-storage-account/).</span><span class="sxs-lookup"><span data-stu-id="a8f1d-114">The template is located in [Github](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-existing-default-storage-account/).</span></span> <span data-ttu-id="a8f1d-115">Resource Manager template experience is not required for following this tutorial.</span><span class="sxs-lookup"><span data-stu-id="a8f1d-115">Resource Manager template experience is not required for following this tutorial.</span></span> <span data-ttu-id="a8f1d-116">For other cluster creation methods and understanding the properties used in this tutorial, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="a8f1d-116">For other cluster creation methods and understanding the properties used in this tutorial, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

1. <span data-ttu-id="a8f1d-117">Click the following image to sign in to Azure and open the Resource Manager template in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="a8f1d-117">Click the following image to sign in to Azure and open the Resource Manager template in the Azure portal.</span></span> 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-with-existing-default-storage-account%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hadoop-linux-tutorial-get-started/deploy-to-azure.png" alt="Deploy to Azure"></a>

2. <span data-ttu-id="a8f1d-118">Follow the instructions to create the cluster with the following specifications:</span><span class="sxs-lookup"><span data-stu-id="a8f1d-118">Follow the instructions to create the cluster with the following specifications:</span></span> 

    - <span data-ttu-id="a8f1d-119">Specify HDInsight version 3.6.</span><span class="sxs-lookup"><span data-stu-id="a8f1d-119">Specify HDInsight version 3.6.</span></span>  <span data-ttu-id="a8f1d-120">Version 3.6 or newer is required.</span><span class="sxs-lookup"><span data-stu-id="a8f1d-120">Version 3.6 or newer is required.</span></span>
    - <span data-ttu-id="a8f1d-121">Specify a secure transfer enabled storage account.</span><span class="sxs-lookup"><span data-stu-id="a8f1d-121">Specify a secure transfer enabled storage account.</span></span>
    - <span data-ttu-id="a8f1d-122">Use short name for the storage account.</span><span class="sxs-lookup"><span data-stu-id="a8f1d-122">Use short name for the storage account.</span></span>
    - <span data-ttu-id="a8f1d-123">Both the storage account and the blob container must be created beforehand.</span><span class="sxs-lookup"><span data-stu-id="a8f1d-123">Both the storage account and the blob container must be created beforehand.</span></span> 

    <span data-ttu-id="a8f1d-124">For the instructions, see [Create cluster](hadoop/apache-hadoop-linux-tutorial-get-started.md#create-cluster).</span><span class="sxs-lookup"><span data-stu-id="a8f1d-124">For the instructions, see [Create cluster](hadoop/apache-hadoop-linux-tutorial-get-started.md#create-cluster).</span></span> 

<span data-ttu-id="a8f1d-125">If you use script action to provide your own configuration files, you must use wasbs in the following settings:</span><span class="sxs-lookup"><span data-stu-id="a8f1d-125">If you use script action to provide your own configuration files, you must use wasbs in the following settings:</span></span>

- <span data-ttu-id="a8f1d-126">fs.defaultFS (core-site)</span><span class="sxs-lookup"><span data-stu-id="a8f1d-126">fs.defaultFS (core-site)</span></span>
- <span data-ttu-id="a8f1d-127">spark.eventLog.dir</span><span class="sxs-lookup"><span data-stu-id="a8f1d-127">spark.eventLog.dir</span></span> 
- <span data-ttu-id="a8f1d-128">spark.history.fs.logDirectory</span><span class="sxs-lookup"><span data-stu-id="a8f1d-128">spark.history.fs.logDirectory</span></span>

## <a name="add-additional-storage-accounts"></a><span data-ttu-id="a8f1d-129">Add additional storage accounts</span><span class="sxs-lookup"><span data-stu-id="a8f1d-129">Add additional storage accounts</span></span>

<span data-ttu-id="a8f1d-130">There are several options to add additional secure transfer enabled storage accounts:</span><span class="sxs-lookup"><span data-stu-id="a8f1d-130">There are several options to add additional secure transfer enabled storage accounts:</span></span>

- <span data-ttu-id="a8f1d-131">Modify the Azure Resource Manager template in the last section.</span><span class="sxs-lookup"><span data-stu-id="a8f1d-131">Modify the Azure Resource Manager template in the last section.</span></span>
- <span data-ttu-id="a8f1d-132">Create a cluster using the [Azure portal](https://portal.azure.com) and specify linked storage account.</span><span class="sxs-lookup"><span data-stu-id="a8f1d-132">Create a cluster using the [Azure portal](https://portal.azure.com) and specify linked storage account.</span></span>
- <span data-ttu-id="a8f1d-133">Use script action to add additional secure transfer enabled storage accounts to an existing HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="a8f1d-133">Use script action to add additional secure transfer enabled storage accounts to an existing HDInsight cluster.</span></span>  <span data-ttu-id="a8f1d-134">For more information, see [Add additional storage accounts to HDInsight](hdinsight-hadoop-add-storage.md).</span><span class="sxs-lookup"><span data-stu-id="a8f1d-134">For more information, see [Add additional storage accounts to HDInsight](hdinsight-hadoop-add-storage.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a8f1d-135">Next steps</span><span class="sxs-lookup"><span data-stu-id="a8f1d-135">Next steps</span></span>
<span data-ttu-id="a8f1d-136">In this tutorial, you have learned how to create an HDInsight cluster, and enable secure transfer to the storage accounts.</span><span class="sxs-lookup"><span data-stu-id="a8f1d-136">In this tutorial, you have learned how to create an HDInsight cluster, and enable secure transfer to the storage accounts.</span></span>

<span data-ttu-id="a8f1d-137">To learn more about analyzing data with HDInsight, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="a8f1d-137">To learn more about analyzing data with HDInsight, see the following articles:</span></span>

* <span data-ttu-id="a8f1d-138">To learn more about using Hive with HDInsight, including how to perform Hive queries from Visual Studio, see [Use Hive with HDInsight][hdinsight-use-hive].</span><span class="sxs-lookup"><span data-stu-id="a8f1d-138">To learn more about using Hive with HDInsight, including how to perform Hive queries from Visual Studio, see [Use Hive with HDInsight][hdinsight-use-hive].</span></span>
* <span data-ttu-id="a8f1d-139">To learn about Pig, a language used to transform data, see [Use Pig with HDInsight][hdinsight-use-pig].</span><span class="sxs-lookup"><span data-stu-id="a8f1d-139">To learn about Pig, a language used to transform data, see [Use Pig with HDInsight][hdinsight-use-pig].</span></span>
* <span data-ttu-id="a8f1d-140">To learn about MapReduce, a way to write programs that process data on Hadoop, see [Use MapReduce with HDInsight][hdinsight-use-mapreduce].</span><span class="sxs-lookup"><span data-stu-id="a8f1d-140">To learn about MapReduce, a way to write programs that process data on Hadoop, see [Use MapReduce with HDInsight][hdinsight-use-mapreduce].</span></span>
* <span data-ttu-id="a8f1d-141">To learn about using the HDInsight Tools for Visual Studio to analyze data on HDInsight, see [Get started using Visual Studio Hadoop tools for HDInsight](hadoop/apache-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="a8f1d-141">To learn about using the HDInsight Tools for Visual Studio to analyze data on HDInsight, see [Get started using Visual Studio Hadoop tools for HDInsight](hadoop/apache-hadoop-visual-studio-tools-get-started.md).</span></span>

<span data-ttu-id="a8f1d-142">To learn more about how HDInsight stores data or how to get data into HDInsight, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="a8f1d-142">To learn more about how HDInsight stores data or how to get data into HDInsight, see the following articles:</span></span>

* <span data-ttu-id="a8f1d-143">For information on how HDInsight uses Azure Storage, see [Use Azure Storage with HDInsight](hdinsight-hadoop-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="a8f1d-143">For information on how HDInsight uses Azure Storage, see [Use Azure Storage with HDInsight](hdinsight-hadoop-use-blob-storage.md).</span></span>
* <span data-ttu-id="a8f1d-144">For information on how to upload data to HDInsight, see [Upload data to HDInsight][hdinsight-upload-data].</span><span class="sxs-lookup"><span data-stu-id="a8f1d-144">For information on how to upload data to HDInsight, see [Upload data to HDInsight][hdinsight-upload-data].</span></span>

<span data-ttu-id="a8f1d-145">To learn more about creating or managing an HDInsight cluster, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="a8f1d-145">To learn more about creating or managing an HDInsight cluster, see the following articles:</span></span>

* <span data-ttu-id="a8f1d-146">To learn about managing your Linux-based HDInsight cluster, see [Manage HDInsight clusters using Ambari](hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="a8f1d-146">To learn about managing your Linux-based HDInsight cluster, see [Manage HDInsight clusters using Ambari](hdinsight-hadoop-manage-ambari.md).</span></span>
* <span data-ttu-id="a8f1d-147">To learn more about the options you can select when creating an HDInsight cluster, see [Creating HDInsight on Linux using custom options](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="a8f1d-147">To learn more about the options you can select when creating an HDInsight cluster, see [Creating HDInsight on Linux using custom options](hdinsight-hadoop-provision-linux-clusters.md).</span></span>
* <span data-ttu-id="a8f1d-148">If you are familiar with Linux, and Hadoop, but want to know specifics about Hadoop on the HDInsight, see [Working with HDInsight on Linux](hdinsight-hadoop-linux-information.md).</span><span class="sxs-lookup"><span data-stu-id="a8f1d-148">If you are familiar with Linux, and Hadoop, but want to know specifics about Hadoop on the HDInsight, see [Working with HDInsight on Linux](hdinsight-hadoop-linux-information.md).</span></span> <span data-ttu-id="a8f1d-149">This article provides information such as:</span><span class="sxs-lookup"><span data-stu-id="a8f1d-149">This article provides information such as:</span></span>
  
  * <span data-ttu-id="a8f1d-150">URLs for services hosted on the cluster, such as Ambari and WebHCat</span><span class="sxs-lookup"><span data-stu-id="a8f1d-150">URLs for services hosted on the cluster, such as Ambari and WebHCat</span></span>
  * <span data-ttu-id="a8f1d-151">The location of Hadoop files and examples on the local file system</span><span class="sxs-lookup"><span data-stu-id="a8f1d-151">The location of Hadoop files and examples on the local file system</span></span>
  * <span data-ttu-id="a8f1d-152">The use of Azure Storage (WASB) instead of HDFS as the default data store</span><span class="sxs-lookup"><span data-stu-id="a8f1d-152">The use of Azure Storage (WASB) instead of HDFS as the default data store</span></span>

[1]: ../HDInsight/hadoop/apache-hadoop-visual-studio-tools-get-started.md

[hdinsight-provision]: hdinsight-provision-linux-clusters.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-mapreduce]:hadoop/hdinsight-use-mapreduce.md
[hdinsight-use-hive]:hadoop/hdinsight-use-hive.md
[hdinsight-use-pig]:hadoop/hdinsight-use-pig.md
