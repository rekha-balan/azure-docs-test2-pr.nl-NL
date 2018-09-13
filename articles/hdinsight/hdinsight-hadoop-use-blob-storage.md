---
title: Query data from HDFS-compatible Azure storage | Microsoft Docs
description: Learn how to query data from Azure storage and Azure Data Lake Store to store results of your analysis.
keywords: blob storage,hdfs,structured data,unstructured data, data lake store
services: hdinsight,storage
documentationcenter: ''
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 1d2e65f2-16de-449e-915f-3ffbc230f815
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 02/27/2017
ms.author: jgao
ms.openlocfilehash: 7bedea99839bb7c2c2174a8b612b71c9590f149f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554223"
---
# <a name="use-hdfs-compatible-storage-with-hadoop-in-hdinsight"></a><span data-ttu-id="c9a30-104">Use HDFS-compatible storage with Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="c9a30-104">Use HDFS-compatible storage with Hadoop in HDInsight</span></span>

<span data-ttu-id="c9a30-105">To analyze data in HDInsight cluster, you can store the data either in Azure Storage, Azure Data Lake Store, or both.</span><span class="sxs-lookup"><span data-stu-id="c9a30-105">To analyze data in HDInsight cluster, you can store the data either in Azure Storage, Azure Data Lake Store, or both.</span></span> <span data-ttu-id="c9a30-106">Both storage options enable you to safely delete HDInsight clusters that are used for computation without losing user data.</span><span class="sxs-lookup"><span data-stu-id="c9a30-106">Both storage options enable you to safely delete HDInsight clusters that are used for computation without losing user data.</span></span>

<span data-ttu-id="c9a30-107">Hadoop supports a notion of the default file system.</span><span class="sxs-lookup"><span data-stu-id="c9a30-107">Hadoop supports a notion of the default file system.</span></span> <span data-ttu-id="c9a30-108">The default file system implies a default scheme and authority.</span><span class="sxs-lookup"><span data-stu-id="c9a30-108">The default file system implies a default scheme and authority.</span></span> <span data-ttu-id="c9a30-109">It can also be used to resolve relative paths.</span><span class="sxs-lookup"><span data-stu-id="c9a30-109">It can also be used to resolve relative paths.</span></span> <span data-ttu-id="c9a30-110">During the HDInsight cluster creation process, you can specify a blob container in Azure Storage as the default file system, or with HDInsight 3.5, you can select either Azure Storage or Azure Data Lake Store as the default files system.</span><span class="sxs-lookup"><span data-stu-id="c9a30-110">During the HDInsight cluster creation process, you can specify a blob container in Azure Storage as the default file system, or with HDInsight 3.5, you can select either Azure Storage or Azure Data Lake Store as the default files system.</span></span>

<span data-ttu-id="c9a30-111">In this article, you learn how the two storage options work with HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="c9a30-111">In this article, you learn how the two storage options work with HDInsight clusters.</span></span> <span data-ttu-id="c9a30-112">For more information about creating an HDInsight cluster, see [Get Started with HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c9a30-112">For more information about creating an HDInsight cluster, see [Get Started with HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>

## <a name="using-azure-storage-with-hdinsight-clusters"></a><span data-ttu-id="c9a30-113">Using Azure storage with HDInsight clusters</span><span class="sxs-lookup"><span data-stu-id="c9a30-113">Using Azure storage with HDInsight clusters</span></span>

<span data-ttu-id="c9a30-114">Azure storage is a robust, general-purpose storage solution that integrates seamlessly with HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c9a30-114">Azure storage is a robust, general-purpose storage solution that integrates seamlessly with HDInsight.</span></span> <span data-ttu-id="c9a30-115">HDInsight can use a blob container in Azure Storage as the default file system for the cluster.</span><span class="sxs-lookup"><span data-stu-id="c9a30-115">HDInsight can use a blob container in Azure Storage as the default file system for the cluster.</span></span> <span data-ttu-id="c9a30-116">Through a Hadoop distributed file system (HDFS) interface, the full set of components in HDInsight can operate directly on structured or unstructured data stored as blobs.</span><span class="sxs-lookup"><span data-stu-id="c9a30-116">Through a Hadoop distributed file system (HDFS) interface, the full set of components in HDInsight can operate directly on structured or unstructured data stored as blobs.</span></span>

> [!WARNING]
> <span data-ttu-id="c9a30-117">There are several options avaialble when creating an Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="c9a30-117">There are several options avaialble when creating an Azure Storage account.</span></span> <span data-ttu-id="c9a30-118">The following table provides information on what options are supported with HDInsight:</span><span class="sxs-lookup"><span data-stu-id="c9a30-118">The following table provides information on what options are supported with HDInsight:</span></span>
> 
> | <span data-ttu-id="c9a30-119">Storage account type</span><span class="sxs-lookup"><span data-stu-id="c9a30-119">Storage account type</span></span> | <span data-ttu-id="c9a30-120">Storage tier</span><span class="sxs-lookup"><span data-stu-id="c9a30-120">Storage tier</span></span> | <span data-ttu-id="c9a30-121">Supported with HDInsight</span><span class="sxs-lookup"><span data-stu-id="c9a30-121">Supported with HDInsight</span></span> |
> | ------- | ------- | ------- |
> | <span data-ttu-id="c9a30-122">General-purpose Storage Account</span><span class="sxs-lookup"><span data-stu-id="c9a30-122">General-purpose Storage Account</span></span> | <span data-ttu-id="c9a30-123">Standard</span><span class="sxs-lookup"><span data-stu-id="c9a30-123">Standard</span></span> | <span data-ttu-id="c9a30-124">__Yes__</span><span class="sxs-lookup"><span data-stu-id="c9a30-124">__Yes__</span></span> |
> | &nbsp; | <span data-ttu-id="c9a30-125">Premium</span><span class="sxs-lookup"><span data-stu-id="c9a30-125">Premium</span></span> | <span data-ttu-id="c9a30-126">No</span><span class="sxs-lookup"><span data-stu-id="c9a30-126">No</span></span> |
> | <span data-ttu-id="c9a30-127">Blob Storage Account</span><span class="sxs-lookup"><span data-stu-id="c9a30-127">Blob Storage Account</span></span> | <span data-ttu-id="c9a30-128">Hot</span><span class="sxs-lookup"><span data-stu-id="c9a30-128">Hot</span></span> | <span data-ttu-id="c9a30-129">No</span><span class="sxs-lookup"><span data-stu-id="c9a30-129">No</span></span> |
> | &nbsp; | <span data-ttu-id="c9a30-130">Cool</span><span class="sxs-lookup"><span data-stu-id="c9a30-130">Cool</span></span> | <span data-ttu-id="c9a30-131">No</span><span class="sxs-lookup"><span data-stu-id="c9a30-131">No</span></span> |

### <a name="hdinsight-storage-architecture"></a><span data-ttu-id="c9a30-132">HDInsight storage architecture</span><span class="sxs-lookup"><span data-stu-id="c9a30-132">HDInsight storage architecture</span></span>
<span data-ttu-id="c9a30-133">The following diagram provides an abstract view of the HDInsight storage architecture:</span><span class="sxs-lookup"><span data-stu-id="c9a30-133">The following diagram provides an abstract view of the HDInsight storage architecture:</span></span>

<span data-ttu-id="c9a30-134">![Hadoop clusters use the HDFS API to access and store structured and unstructured data in Blob storage.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-use-blob-storage/HDI.WASB.Arch.png "HDInsight Storage Architecture")</span><span class="sxs-lookup"><span data-stu-id="c9a30-134">![Hadoop clusters use the HDFS API to access and store structured and unstructured data in Blob storage.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-use-blob-storage/HDI.WASB.Arch.png "HDInsight Storage Architecture")</span></span>

<span data-ttu-id="c9a30-135">HDInsight provides access to the distributed file system that is locally attached to the compute nodes.</span><span class="sxs-lookup"><span data-stu-id="c9a30-135">HDInsight provides access to the distributed file system that is locally attached to the compute nodes.</span></span> <span data-ttu-id="c9a30-136">This file system can be accessed by using the fully qualified URI, for example:</span><span class="sxs-lookup"><span data-stu-id="c9a30-136">This file system can be accessed by using the fully qualified URI, for example:</span></span>

    hdfs://<namenodehost>/<path>

<span data-ttu-id="c9a30-137">In addition, HDInsight provides the ability to access data that is stored in Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="c9a30-137">In addition, HDInsight provides the ability to access data that is stored in Azure Storage.</span></span> <span data-ttu-id="c9a30-138">The syntax is:</span><span class="sxs-lookup"><span data-stu-id="c9a30-138">The syntax is:</span></span>

    wasb[s]://<containername>@<accountname>.blob.core.windows.net/<path>

<span data-ttu-id="c9a30-139">Here are some considerations when using Azure Storage account with HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="c9a30-139">Here are some considerations when using Azure Storage account with HDInsight clusters.</span></span>

* <span data-ttu-id="c9a30-140">**Containers in the storage accounts that are connected to a cluster:** Because the account name and key are associated with the cluster during creation, you have full access to the blobs in those containers.</span><span class="sxs-lookup"><span data-stu-id="c9a30-140">**Containers in the storage accounts that are connected to a cluster:** Because the account name and key are associated with the cluster during creation, you have full access to the blobs in those containers.</span></span>

* <span data-ttu-id="c9a30-141">**Public containers or public blobs in storage accounts that are NOT connected to a cluster:** You have read-only permission to the blobs in the containers.</span><span class="sxs-lookup"><span data-stu-id="c9a30-141">**Public containers or public blobs in storage accounts that are NOT connected to a cluster:** You have read-only permission to the blobs in the containers.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="c9a30-142">Public containers allow you to get a list of all blobs that are available in that container and get container metadata.</span><span class="sxs-lookup"><span data-stu-id="c9a30-142">Public containers allow you to get a list of all blobs that are available in that container and get container metadata.</span></span> <span data-ttu-id="c9a30-143">Public blobs allow you to access the blobs only if you know the exact URL.</span><span class="sxs-lookup"><span data-stu-id="c9a30-143">Public blobs allow you to access the blobs only if you know the exact URL.</span></span> <span data-ttu-id="c9a30-144">For more information, see <a href="http://msdn.microsoft.com/library/windowsazure/dd179354.aspx">Restrict access to containers and blobs</a>.</span><span class="sxs-lookup"><span data-stu-id="c9a30-144">For more information, see <a href="http://msdn.microsoft.com/library/windowsazure/dd179354.aspx">Restrict access to containers and blobs</a>.</span></span>
  > 
  > 
* <span data-ttu-id="c9a30-145">**Private containers in storage accounts that are NOT connected to a cluster:** You can't access the blobs in the containers unless you define the storage account when you submit the WebHCat jobs.</span><span class="sxs-lookup"><span data-stu-id="c9a30-145">**Private containers in storage accounts that are NOT connected to a cluster:** You can't access the blobs in the containers unless you define the storage account when you submit the WebHCat jobs.</span></span> <span data-ttu-id="c9a30-146">This is explained later in this article.</span><span class="sxs-lookup"><span data-stu-id="c9a30-146">This is explained later in this article.</span></span>

<span data-ttu-id="c9a30-147">The storage accounts that are defined in the creation process and their keys are stored in %HADOOP_HOME%/conf/core-site.xml on the cluster nodes.</span><span class="sxs-lookup"><span data-stu-id="c9a30-147">The storage accounts that are defined in the creation process and their keys are stored in %HADOOP_HOME%/conf/core-site.xml on the cluster nodes.</span></span> <span data-ttu-id="c9a30-148">The default behavior of HDInsight is to use the storage accounts defined in the core-site.xml file.</span><span class="sxs-lookup"><span data-stu-id="c9a30-148">The default behavior of HDInsight is to use the storage accounts defined in the core-site.xml file.</span></span> <span data-ttu-id="c9a30-149">It is not recommended to directly edit the core-site.xml file because the cluster head node(master) may be reimaged or migrated at any time, and any changes to this file are not persisted.</span><span class="sxs-lookup"><span data-stu-id="c9a30-149">It is not recommended to directly edit the core-site.xml file because the cluster head node(master) may be reimaged or migrated at any time, and any changes to this file are not persisted.</span></span>

<span data-ttu-id="c9a30-150">Multiple WebHCat jobs, including Hive, MapReduce, Hadoop streaming, and Pig, can carry a description of storage accounts and metadata with them.</span><span class="sxs-lookup"><span data-stu-id="c9a30-150">Multiple WebHCat jobs, including Hive, MapReduce, Hadoop streaming, and Pig, can carry a description of storage accounts and metadata with them.</span></span> <span data-ttu-id="c9a30-151">(This currently works for Pig with storage accounts, but not for metadata.) In the [Access blobs using Azure PowerShell](#powershell) section of this article, there is a sample of this feature.</span><span class="sxs-lookup"><span data-stu-id="c9a30-151">(This currently works for Pig with storage accounts, but not for metadata.) In the [Access blobs using Azure PowerShell](#powershell) section of this article, there is a sample of this feature.</span></span> <span data-ttu-id="c9a30-152">For more information, see [Using an HDInsight Cluster with Alternate Storage Accounts and Metastores](http://social.technet.microsoft.com/wiki/contents/articles/23256.using-an-hdinsight-cluster-with-alternate-storage-accounts-and-metastores.aspx).</span><span class="sxs-lookup"><span data-stu-id="c9a30-152">For more information, see [Using an HDInsight Cluster with Alternate Storage Accounts and Metastores](http://social.technet.microsoft.com/wiki/contents/articles/23256.using-an-hdinsight-cluster-with-alternate-storage-accounts-and-metastores.aspx).</span></span>

<span data-ttu-id="c9a30-153">Blobs can be used for structured and unstructured data.</span><span class="sxs-lookup"><span data-stu-id="c9a30-153">Blobs can be used for structured and unstructured data.</span></span> <span data-ttu-id="c9a30-154">Blob containers store data as key/value pairs, and there is no directory hierarchy.</span><span class="sxs-lookup"><span data-stu-id="c9a30-154">Blob containers store data as key/value pairs, and there is no directory hierarchy.</span></span> <span data-ttu-id="c9a30-155">However the slash character ( / ) can be used within the key name to make it appear as if a file is stored within a directory structure.</span><span class="sxs-lookup"><span data-stu-id="c9a30-155">However the slash character ( / ) can be used within the key name to make it appear as if a file is stored within a directory structure.</span></span> <span data-ttu-id="c9a30-156">For example, a blob's key may be *input/log1.txt*.</span><span class="sxs-lookup"><span data-stu-id="c9a30-156">For example, a blob's key may be *input/log1.txt*.</span></span> <span data-ttu-id="c9a30-157">No actual *input* directory exists, but due to the presence of the slash character in the key name, it has the appearance of a file path.</span><span class="sxs-lookup"><span data-stu-id="c9a30-157">No actual *input* directory exists, but due to the presence of the slash character in the key name, it has the appearance of a file path.</span></span>

### <a id="benefits"></a><span data-ttu-id="c9a30-158">Benefits of Azure Storage</span><span class="sxs-lookup"><span data-stu-id="c9a30-158">Benefits of Azure Storage</span></span>
<span data-ttu-id="c9a30-159">The implied performance cost of not co-locating compute clusters and storage resources is mitigated by the way the compute clusters are created close to the storage account resources inside the Azure region, where the high-speed network makes it very efficient for the compute nodes to access the data inside Azure storage.</span><span class="sxs-lookup"><span data-stu-id="c9a30-159">The implied performance cost of not co-locating compute clusters and storage resources is mitigated by the way the compute clusters are created close to the storage account resources inside the Azure region, where the high-speed network makes it very efficient for the compute nodes to access the data inside Azure storage.</span></span>

<span data-ttu-id="c9a30-160">There are several benefits associated with storing the data in Azure storage instead of HDFS:</span><span class="sxs-lookup"><span data-stu-id="c9a30-160">There are several benefits associated with storing the data in Azure storage instead of HDFS:</span></span>

* <span data-ttu-id="c9a30-161">**Data reuse and sharing:** The data in HDFS is located inside the compute cluster.</span><span class="sxs-lookup"><span data-stu-id="c9a30-161">**Data reuse and sharing:** The data in HDFS is located inside the compute cluster.</span></span> <span data-ttu-id="c9a30-162">Only the applications that have access to the compute cluster can use the data by using HDFS APIs.</span><span class="sxs-lookup"><span data-stu-id="c9a30-162">Only the applications that have access to the compute cluster can use the data by using HDFS APIs.</span></span> <span data-ttu-id="c9a30-163">The data in Azure storage can be accessed either through the HDFS APIs or through the [Blob Storage REST APIs][blob-storage-restAPI].</span><span class="sxs-lookup"><span data-stu-id="c9a30-163">The data in Azure storage can be accessed either through the HDFS APIs or through the [Blob Storage REST APIs][blob-storage-restAPI].</span></span> <span data-ttu-id="c9a30-164">Thus, a larger set of applications (including other HDInsight clusters) and tools can be used to produce and consume the data.</span><span class="sxs-lookup"><span data-stu-id="c9a30-164">Thus, a larger set of applications (including other HDInsight clusters) and tools can be used to produce and consume the data.</span></span>
* <span data-ttu-id="c9a30-165">**Data archiving:** Storing data in Azure storage enables the HDInsight clusters used for computation to be safely deleted without losing user data.</span><span class="sxs-lookup"><span data-stu-id="c9a30-165">**Data archiving:** Storing data in Azure storage enables the HDInsight clusters used for computation to be safely deleted without losing user data.</span></span>
* <span data-ttu-id="c9a30-166">**Data storage cost:** Storing data in DFS for the long term is more costly than storing the data in Azure storage because the cost of a compute cluster is higher than the cost of Azure storage.</span><span class="sxs-lookup"><span data-stu-id="c9a30-166">**Data storage cost:** Storing data in DFS for the long term is more costly than storing the data in Azure storage because the cost of a compute cluster is higher than the cost of Azure storage.</span></span> <span data-ttu-id="c9a30-167">In addition, because the data does not have to be reloaded for every compute cluster generation, you are also saving data loading costs.</span><span class="sxs-lookup"><span data-stu-id="c9a30-167">In addition, because the data does not have to be reloaded for every compute cluster generation, you are also saving data loading costs.</span></span>
* <span data-ttu-id="c9a30-168">**Elastic scale-out:** Although HDFS provides you with a scaled-out file system, the scale is determined by the number of nodes that you create for your cluster.</span><span class="sxs-lookup"><span data-stu-id="c9a30-168">**Elastic scale-out:** Although HDFS provides you with a scaled-out file system, the scale is determined by the number of nodes that you create for your cluster.</span></span> <span data-ttu-id="c9a30-169">Changing the scale can become a more complicated process than relying on the elastic scaling capabilities that you get automatically in Azure storage.</span><span class="sxs-lookup"><span data-stu-id="c9a30-169">Changing the scale can become a more complicated process than relying on the elastic scaling capabilities that you get automatically in Azure storage.</span></span>
* <span data-ttu-id="c9a30-170">**Geo-replication:** Your Azure storage can be geo-replicated.</span><span class="sxs-lookup"><span data-stu-id="c9a30-170">**Geo-replication:** Your Azure storage can be geo-replicated.</span></span> <span data-ttu-id="c9a30-171">Although this gives you geographic recovery and data redundancy, a failover to the geo-replicated location severely impacts your performance, and it may incur additional costs.</span><span class="sxs-lookup"><span data-stu-id="c9a30-171">Although this gives you geographic recovery and data redundancy, a failover to the geo-replicated location severely impacts your performance, and it may incur additional costs.</span></span> <span data-ttu-id="c9a30-172">So our recommendation is to choose the geo-replication wisely and only if the value of the data is worth the additional cost.</span><span class="sxs-lookup"><span data-stu-id="c9a30-172">So our recommendation is to choose the geo-replication wisely and only if the value of the data is worth the additional cost.</span></span>

<span data-ttu-id="c9a30-173">Certain MapReduce jobs and packages may create intermediate results that you don't really want to store in Azure storage.</span><span class="sxs-lookup"><span data-stu-id="c9a30-173">Certain MapReduce jobs and packages may create intermediate results that you don't really want to store in Azure storage.</span></span> <span data-ttu-id="c9a30-174">In that case, you can elect to store the data in the local HDFS.</span><span class="sxs-lookup"><span data-stu-id="c9a30-174">In that case, you can elect to store the data in the local HDFS.</span></span> <span data-ttu-id="c9a30-175">In fact, HDInsight uses DFS for several of these intermediate results in Hive jobs and other processes.</span><span class="sxs-lookup"><span data-stu-id="c9a30-175">In fact, HDInsight uses DFS for several of these intermediate results in Hive jobs and other processes.</span></span>

> [!NOTE]
> <span data-ttu-id="c9a30-176">Most HDFS commands (for example, <b>ls</b>, <b>copyFromLocal</b> and <b>mkdir</b>) still work as expected.</span><span class="sxs-lookup"><span data-stu-id="c9a30-176">Most HDFS commands (for example, <b>ls</b>, <b>copyFromLocal</b> and <b>mkdir</b>) still work as expected.</span></span> <span data-ttu-id="c9a30-177">Only the commands that are specific to the native HDFS implementation (which is referred to as DFS), such as <b>fschk</b> and <b>dfsadmin</b>, show different behavior in Azure storage.</span><span class="sxs-lookup"><span data-stu-id="c9a30-177">Only the commands that are specific to the native HDFS implementation (which is referred to as DFS), such as <b>fschk</b> and <b>dfsadmin</b>, show different behavior in Azure storage.</span></span>
> 
> 

### <a name="create-blob-containers"></a><span data-ttu-id="c9a30-178">Create Blob containers</span><span class="sxs-lookup"><span data-stu-id="c9a30-178">Create Blob containers</span></span>
<span data-ttu-id="c9a30-179">To use blobs, you first create an [Azure Storage account][azure-storage-create].</span><span class="sxs-lookup"><span data-stu-id="c9a30-179">To use blobs, you first create an [Azure Storage account][azure-storage-create].</span></span> <span data-ttu-id="c9a30-180">As part of this, you specify an Azure region where the storage account is created.</span><span class="sxs-lookup"><span data-stu-id="c9a30-180">As part of this, you specify an Azure region where the storage account is created.</span></span> <span data-ttu-id="c9a30-181">The cluster and the storage account must be hosted in the same region.</span><span class="sxs-lookup"><span data-stu-id="c9a30-181">The cluster and the storage account must be hosted in the same region.</span></span> <span data-ttu-id="c9a30-182">The Hive metastore SQL Server database and Oozie metastore SQL Server database must also be located in the same region.</span><span class="sxs-lookup"><span data-stu-id="c9a30-182">The Hive metastore SQL Server database and Oozie metastore SQL Server database must also be located in the same region.</span></span>

<span data-ttu-id="c9a30-183">Wherever it lives, each blob you create belongs to a container in your Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="c9a30-183">Wherever it lives, each blob you create belongs to a container in your Azure Storage account.</span></span> <span data-ttu-id="c9a30-184">This container may be an existing blob that was created outside of HDInsight, or it may be a container that is created for an HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="c9a30-184">This container may be an existing blob that was created outside of HDInsight, or it may be a container that is created for an HDInsight cluster.</span></span>

<span data-ttu-id="c9a30-185">The default Blob container stores cluster specific information such as job history and logs.</span><span class="sxs-lookup"><span data-stu-id="c9a30-185">The default Blob container stores cluster specific information such as job history and logs.</span></span> <span data-ttu-id="c9a30-186">Don't share a default Blob container with multiple HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="c9a30-186">Don't share a default Blob container with multiple HDInsight clusters.</span></span> <span data-ttu-id="c9a30-187">This might corrupt job history.</span><span class="sxs-lookup"><span data-stu-id="c9a30-187">This might corrupt job history.</span></span> <span data-ttu-id="c9a30-188">It is recommended to use a different container for each cluster and put shared data on a linked storage account specified in deployment of all relevant clusters rather than the default storage account.</span><span class="sxs-lookup"><span data-stu-id="c9a30-188">It is recommended to use a different container for each cluster and put shared data on a linked storage account specified in deployment of all relevant clusters rather than the default storage account.</span></span> <span data-ttu-id="c9a30-189">For more information on configuring linked storage accounts, see [Create HDInsight clusters][hdinsight-creation].</span><span class="sxs-lookup"><span data-stu-id="c9a30-189">For more information on configuring linked storage accounts, see [Create HDInsight clusters][hdinsight-creation].</span></span> <span data-ttu-id="c9a30-190">However you can reuse a default storage container after the original HDInsight cluster has been deleted.</span><span class="sxs-lookup"><span data-stu-id="c9a30-190">However you can reuse a default storage container after the original HDInsight cluster has been deleted.</span></span> <span data-ttu-id="c9a30-191">For HBase clusters, you can actually retain the HBase table schema and data by create a new HBase cluster using the default blob container that is used by an HBase cluster that has been deleted.</span><span class="sxs-lookup"><span data-stu-id="c9a30-191">For HBase clusters, you can actually retain the HBase table schema and data by create a new HBase cluster using the default blob container that is used by an HBase cluster that has been deleted.</span></span>

#### <a name="using-the-azure-portal"></a><span data-ttu-id="c9a30-192">Using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="c9a30-192">Using the Azure portal</span></span>
<span data-ttu-id="c9a30-193">When creating an HDInsight cluster from the Portal, you have the options (as shown below) to provide the storage account details.</span><span class="sxs-lookup"><span data-stu-id="c9a30-193">When creating an HDInsight cluster from the Portal, you have the options (as shown below) to provide the storage account details.</span></span> <span data-ttu-id="c9a30-194">You can also specify whether you want an additional storage account associated with the cluster, and if so, choose from Data Lake Store or another Azure Storage blob as the additional storage.</span><span class="sxs-lookup"><span data-stu-id="c9a30-194">You can also specify whether you want an additional storage account associated with the cluster, and if so, choose from Data Lake Store or another Azure Storage blob as the additional storage.</span></span>

![HDInsight hadoop creation data source](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-use-blob-storage/hdinsight.provision.data.source.png)

> [!WARNING]
> <span data-ttu-id="c9a30-196">Using an additional storage account in a different location than the HDInsight cluster is not supported.</span><span class="sxs-lookup"><span data-stu-id="c9a30-196">Using an additional storage account in a different location than the HDInsight cluster is not supported.</span></span>

#### <a name="using-azure-cli"></a><span data-ttu-id="c9a30-197">Using Azure CLI</span><span class="sxs-lookup"><span data-stu-id="c9a30-197">Using Azure CLI</span></span>
[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

<span data-ttu-id="c9a30-198">If you have [installed and configured the Azure CLI](../cli-install-nodejs.md), the following command can be used to a storage account and container.</span><span class="sxs-lookup"><span data-stu-id="c9a30-198">If you have [installed and configured the Azure CLI](../cli-install-nodejs.md), the following command can be used to a storage account and container.</span></span>

    azure storage account create <storageaccountname> --type LRS

> [!NOTE]
> <span data-ttu-id="c9a30-199">The `--type` parameter indicates how the storage account is replicated.</span><span class="sxs-lookup"><span data-stu-id="c9a30-199">The `--type` parameter indicates how the storage account is replicated.</span></span> <span data-ttu-id="c9a30-200">For more information, see [Azure Storage Replication](../storage/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="c9a30-200">For more information, see [Azure Storage Replication](../storage/storage-redundancy.md).</span></span> <span data-ttu-id="c9a30-201">Don't use ZRS as ZRS doesn't support page blob, file, table or queue.</span><span class="sxs-lookup"><span data-stu-id="c9a30-201">Don't use ZRS as ZRS doesn't support page blob, file, table or queue.</span></span>
> 
> 

<span data-ttu-id="c9a30-202">You are prompted to specify the geographic region that the storage account is created in.</span><span class="sxs-lookup"><span data-stu-id="c9a30-202">You are prompted to specify the geographic region that the storage account is created in.</span></span> <span data-ttu-id="c9a30-203">You should create the storage account in the same region that you plan on creating your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="c9a30-203">You should create the storage account in the same region that you plan on creating your HDInsight cluster.</span></span>

<span data-ttu-id="c9a30-204">Once the storage account is created, use the following command to retrieve the storage account keys:</span><span class="sxs-lookup"><span data-stu-id="c9a30-204">Once the storage account is created, use the following command to retrieve the storage account keys:</span></span>

    azure storage account keys list <storageaccountname>

<span data-ttu-id="c9a30-205">To create a container, use the following command:</span><span class="sxs-lookup"><span data-stu-id="c9a30-205">To create a container, use the following command:</span></span>

    azure storage container create <containername> --account-name <storageaccountname> --account-key <storageaccountkey>

#### <a name="using-azure-powershell"></a><span data-ttu-id="c9a30-206">Using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="c9a30-206">Using Azure PowerShell</span></span>
<span data-ttu-id="c9a30-207">If you [installed and configured Azure PowerShell][powershell-install], you can use the following from the Azure PowerShell prompt to create a storage account and container:</span><span class="sxs-lookup"><span data-stu-id="c9a30-207">If you [installed and configured Azure PowerShell][powershell-install], you can use the following from the Azure PowerShell prompt to create a storage account and container:</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

    $SubscriptionID = "<Your Azure Subscription ID>"
    $ResourceGroupName = "<New Azure Resource Group Name>"
    $Location = "EAST US 2"

    $StorageAccountName = "<New Azure Storage Account Name>"
    $containerName = "<New Azure Blob Container Name>"

    Add-AzureRmAccount
    Select-AzureRmSubscription -SubscriptionId $SubscriptionID

    # Create resource group
    New-AzureRmResourceGroup -name $ResourceGroupName -Location $Location

    # Create default storage account
    New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageAccountName -Location $Location -Type Standard_LRS 

    # Create default blob containers
    $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -StorageAccountName $StorageAccountName)[0].Value
    $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey  
    New-AzureStorageContainer -Name $containerName -Context $destContext

### <a name="address-files-in-azure-storage"></a><span data-ttu-id="c9a30-208">Address files in Azure storage</span><span class="sxs-lookup"><span data-stu-id="c9a30-208">Address files in Azure storage</span></span>
<span data-ttu-id="c9a30-209">The URI scheme for accessing files in Azure storage from HDInsight is:</span><span class="sxs-lookup"><span data-stu-id="c9a30-209">The URI scheme for accessing files in Azure storage from HDInsight is:</span></span>

    wasb[s]://<BlobStorageContainerName>@<StorageAccountName>.blob.core.windows.net/<path>

<span data-ttu-id="c9a30-210">The URI scheme provides unencrypted access (with the *wasb:* prefix) and SSL encrypted access (with *wasbs*).</span><span class="sxs-lookup"><span data-stu-id="c9a30-210">The URI scheme provides unencrypted access (with the *wasb:* prefix) and SSL encrypted access (with *wasbs*).</span></span> <span data-ttu-id="c9a30-211">We recommend using *wasbs* wherever possible, even when accessing data that lives inside the same region in Azure.</span><span class="sxs-lookup"><span data-stu-id="c9a30-211">We recommend using *wasbs* wherever possible, even when accessing data that lives inside the same region in Azure.</span></span>

<span data-ttu-id="c9a30-212">The &lt;BlobStorageContainerName&gt; identifies the name of the blob container in Azure storage.</span><span class="sxs-lookup"><span data-stu-id="c9a30-212">The &lt;BlobStorageContainerName&gt; identifies the name of the blob container in Azure storage.</span></span>
<span data-ttu-id="c9a30-213">The &lt;StorageAccountName&gt; identifies the Azure Storage account name.</span><span class="sxs-lookup"><span data-stu-id="c9a30-213">The &lt;StorageAccountName&gt; identifies the Azure Storage account name.</span></span> <span data-ttu-id="c9a30-214">A fully qualified domain name (FQDN) is required.</span><span class="sxs-lookup"><span data-stu-id="c9a30-214">A fully qualified domain name (FQDN) is required.</span></span>

<span data-ttu-id="c9a30-215">If neither &lt;BlobStorageContainerName&gt; nor &lt;StorageAccountName&gt; has been specified, the default file system is used.</span><span class="sxs-lookup"><span data-stu-id="c9a30-215">If neither &lt;BlobStorageContainerName&gt; nor &lt;StorageAccountName&gt; has been specified, the default file system is used.</span></span> <span data-ttu-id="c9a30-216">For the files on the default file system, you can use a relative path or an absolute path.</span><span class="sxs-lookup"><span data-stu-id="c9a30-216">For the files on the default file system, you can use a relative path or an absolute path.</span></span> <span data-ttu-id="c9a30-217">For example, the *hadoop-mapreduce-examples.jar* file that comes with HDInsight clusters can be referred to by using one of the following:</span><span class="sxs-lookup"><span data-stu-id="c9a30-217">For example, the *hadoop-mapreduce-examples.jar* file that comes with HDInsight clusters can be referred to by using one of the following:</span></span>

    wasbs://mycontainer@myaccount.blob.core.windows.net/example/jars/hadoop-mapreduce-examples.jar
    wasbs:///example/jars/hadoop-mapreduce-examples.jar
    /example/jars/hadoop-mapreduce-examples.jar

> [!NOTE]
> <span data-ttu-id="c9a30-218">The file name is <i>hadoop-examples.jar</i> in HDInsight versions 2.1 and 1.6 clusters.</span><span class="sxs-lookup"><span data-stu-id="c9a30-218">The file name is <i>hadoop-examples.jar</i> in HDInsight versions 2.1 and 1.6 clusters.</span></span>
> 
> 

<span data-ttu-id="c9a30-219">The &lt;path&gt; is the file or directory HDFS path name.</span><span class="sxs-lookup"><span data-stu-id="c9a30-219">The &lt;path&gt; is the file or directory HDFS path name.</span></span> <span data-ttu-id="c9a30-220">Because containers in Azure storage are simply key-value stores, there is no true hierarchical file system.</span><span class="sxs-lookup"><span data-stu-id="c9a30-220">Because containers in Azure storage are simply key-value stores, there is no true hierarchical file system.</span></span> <span data-ttu-id="c9a30-221">A slash character ( / ) inside a blob key is interpreted as a directory separator.</span><span class="sxs-lookup"><span data-stu-id="c9a30-221">A slash character ( / ) inside a blob key is interpreted as a directory separator.</span></span> <span data-ttu-id="c9a30-222">For example, the blob name for *hadoop-mapreduce-examples.jar* is:</span><span class="sxs-lookup"><span data-stu-id="c9a30-222">For example, the blob name for *hadoop-mapreduce-examples.jar* is:</span></span>

    example/jars/hadoop-mapreduce-examples.jar

> [!NOTE]
> <span data-ttu-id="c9a30-223">When working with blobs outside of HDInsight, most utilities do not recognize the WASB format and instead expect a basic path format, such as `example/jars/hadoop-mapreduce-examples.jar`.</span><span class="sxs-lookup"><span data-stu-id="c9a30-223">When working with blobs outside of HDInsight, most utilities do not recognize the WASB format and instead expect a basic path format, such as `example/jars/hadoop-mapreduce-examples.jar`.</span></span>
> 
> 

### <a name="access-blobs-using-azure-cli"></a><span data-ttu-id="c9a30-224">Access blobs using Azure CLI</span><span class="sxs-lookup"><span data-stu-id="c9a30-224">Access blobs using Azure CLI</span></span>
<span data-ttu-id="c9a30-225">Use the following command to list the blob-related commands:</span><span class="sxs-lookup"><span data-stu-id="c9a30-225">Use the following command to list the blob-related commands:</span></span>

    azure storage blob

<span data-ttu-id="c9a30-226">**Example of using Azure CLI to upload a file**</span><span class="sxs-lookup"><span data-stu-id="c9a30-226">**Example of using Azure CLI to upload a file**</span></span>

    azure storage blob upload <sourcefilename> <containername> <blobname> --account-name <storageaccountname> --account-key <storageaccountkey>

<span data-ttu-id="c9a30-227">**Example of using Azure CLI to download a file**</span><span class="sxs-lookup"><span data-stu-id="c9a30-227">**Example of using Azure CLI to download a file**</span></span>

    azure storage blob download <containername> <blobname> <destinationfilename> --account-name <storageaccountname> --account-key <storageaccountkey>

<span data-ttu-id="c9a30-228">**Example of using Azure CLI to delete a file**</span><span class="sxs-lookup"><span data-stu-id="c9a30-228">**Example of using Azure CLI to delete a file**</span></span>

    azure storage blob delete <containername> <blobname> --account-name <storageaccountname> --account-key <storageaccountkey>

<span data-ttu-id="c9a30-229">**Example of using Azure CLI to list files**</span><span class="sxs-lookup"><span data-stu-id="c9a30-229">**Example of using Azure CLI to list files**</span></span>

    azure storage blob list <containername> <blobname|prefix> --account-name <storageaccountname> --account-key <storageaccountkey>

### <a name="access-blobs-using-azure-powershell"></a><span data-ttu-id="c9a30-230">Access blobs using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="c9a30-230">Access blobs using Azure PowerShell</span></span>
> [!NOTE]
> <span data-ttu-id="c9a30-231">The commands in this section provide a basic example of using PowerShell to access data stored in blobs.</span><span class="sxs-lookup"><span data-stu-id="c9a30-231">The commands in this section provide a basic example of using PowerShell to access data stored in blobs.</span></span> <span data-ttu-id="c9a30-232">For a more full-featured example that is customized for working with HDInsight, see the [HDInsight Tools](https://github.com/Blackmist/hdinsight-tools).</span><span class="sxs-lookup"><span data-stu-id="c9a30-232">For a more full-featured example that is customized for working with HDInsight, see the [HDInsight Tools](https://github.com/Blackmist/hdinsight-tools).</span></span>
> 
> 

<span data-ttu-id="c9a30-233">Use the following command to list the blob-related cmdlets:</span><span class="sxs-lookup"><span data-stu-id="c9a30-233">Use the following command to list the blob-related cmdlets:</span></span>

    Get-Command *blob*

![List of blob-related PowerShell cmdlets.][img-hdi-powershell-blobcommands]

#### <a name="upload-files"></a><span data-ttu-id="c9a30-235">Upload files</span><span class="sxs-lookup"><span data-stu-id="c9a30-235">Upload files</span></span>
<span data-ttu-id="c9a30-236">See [Upload data to HDInsight][hdinsight-upload-data].</span><span class="sxs-lookup"><span data-stu-id="c9a30-236">See [Upload data to HDInsight][hdinsight-upload-data].</span></span>

#### <a name="download-files"></a><span data-ttu-id="c9a30-237">Download files</span><span class="sxs-lookup"><span data-stu-id="c9a30-237">Download files</span></span>
<span data-ttu-id="c9a30-238">The following script downloads a block blob to the current folder.</span><span class="sxs-lookup"><span data-stu-id="c9a30-238">The following script downloads a block blob to the current folder.</span></span> <span data-ttu-id="c9a30-239">Before running the script, change the directory to a folder where you have write permissions.</span><span class="sxs-lookup"><span data-stu-id="c9a30-239">Before running the script, change the directory to a folder where you have write permissions.</span></span>

    $resourceGroupName = "<AzureResourceGroupName>"
    $storageAccountName = "<AzureStorageAccountName>"   # The storage account used for the default file system specified at creation.
    $containerName = "<BlobStorageContainerName>"  # The default file system container has the same name as the cluster.
    $blob = "example/data/sample.log" # The name of the blob to be downloaded.

    # Use Add-AzureAccount if you haven't connected to your Azure subscription
    Login-AzureRmAccount 
    Select-AzureRmSubscription -SubscriptionID "<Your Azure Subscription ID>"

    Write-Host "Create a context object ... " -ForegroundColor Green
    $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey  

    Write-Host "Download the blob ..." -ForegroundColor Green
    Get-AzureStorageBlobContent -Container $ContainerName -Blob $blob -Context $storageContext -Force

    Write-Host "List the downloaded file ..." -ForegroundColor Green
    cat "./$blob"

<span data-ttu-id="c9a30-240">Providing the resource group name and the cluster name, you can use the following code:</span><span class="sxs-lookup"><span data-stu-id="c9a30-240">Providing the resource group name and the cluster name, you can use the following code:</span></span>

    $resourceGroupName = "<AzureResourceGroupName>"
    $clusterName = "<HDInsightClusterName>"
    $blob = "example/data/sample.log" # The name of the blob to be downloaded.

    $cluster = Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName
    $defaultStorageAccount = $cluster.DefaultStorageAccount -replace '.blob.core.windows.net'
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccount)[0].Value
    $defaultStorageContainer = $cluster.DefaultStorageContainer
    $storageContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccount -StorageAccountKey $defaultStorageAccountKey 

    Write-Host "Download the blob ..." -ForegroundColor Green
    Get-AzureStorageBlobContent -Container $defaultStorageContainer -Blob $blob -Context $storageContext -Force

#### <a name="delete-files"></a><span data-ttu-id="c9a30-241">Delete files</span><span class="sxs-lookup"><span data-stu-id="c9a30-241">Delete files</span></span>
    Remove-AzureStorageBlob -Container $containerName -Context $storageContext -blob $blob

#### <a name="list-files"></a><span data-ttu-id="c9a30-242">List files</span><span class="sxs-lookup"><span data-stu-id="c9a30-242">List files</span></span>
    Get-AzureStorageBlob -Container $containerName -Context $storageContext -prefix "example/data/"

#### <a name="run-hive-queries-using-an-undefined-storage-account"></a><span data-ttu-id="c9a30-243">Run Hive queries using an undefined storage account</span><span class="sxs-lookup"><span data-stu-id="c9a30-243">Run Hive queries using an undefined storage account</span></span>
<span data-ttu-id="c9a30-244">This example shows how to list a folder from storage account that is not defined during the creating process.</span><span class="sxs-lookup"><span data-stu-id="c9a30-244">This example shows how to list a folder from storage account that is not defined during the creating process.</span></span>
<span data-ttu-id="c9a30-245">$clusterName = "<HDInsightClusterName>"</span><span class="sxs-lookup"><span data-stu-id="c9a30-245">$clusterName = "<HDInsightClusterName>"</span></span>

    $undefinedStorageAccount = "<UnboundedStorageAccountUnderTheSameSubscription>"
    $undefinedContainer = "<UnboundedBlobContainerAssociatedWithTheStorageAccount>"

    $undefinedStorageKey = Get-AzureStorageKey $undefinedStorageAccount | %{ $_.Primary }

    Use-AzureRmHDInsightCluster $clusterName

    $defines = @{}
    $defines.Add("fs.azure.account.key.$undefinedStorageAccount.blob.core.windows.net", $undefinedStorageKey)

    Invoke-AzureRmHDInsightHiveJob -Defines $defines -Query "dfs -ls wasbs://$undefinedContainer@$undefinedStorageAccount.blob.core.windows.net/;"


### <a name="using-additional-storage-accounts"></a><span data-ttu-id="c9a30-246">Using additional storage accounts</span><span class="sxs-lookup"><span data-stu-id="c9a30-246">Using additional storage accounts</span></span>

<span data-ttu-id="c9a30-247">While creating an HDInsight cluster you specify the Azure Storage account you want to associate with it.</span><span class="sxs-lookup"><span data-stu-id="c9a30-247">While creating an HDInsight cluster you specify the Azure Storage account you want to associate with it.</span></span> <span data-ttu-id="c9a30-248">In addition to this storage account, you can add additional storage accounts from the same Azure subscription or different Azure subscriptions during the creation process or after a cluster has been created.</span><span class="sxs-lookup"><span data-stu-id="c9a30-248">In addition to this storage account, you can add additional storage accounts from the same Azure subscription or different Azure subscriptions during the creation process or after a cluster has been created.</span></span> <span data-ttu-id="c9a30-249">For instructions about adding additional storage accounts, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="c9a30-249">For instructions about adding additional storage accounts, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

> [!WARNING]
> <span data-ttu-id="c9a30-250">Using an additional storage account in a different location than the HDInsight cluster is not supported.</span><span class="sxs-lookup"><span data-stu-id="c9a30-250">Using an additional storage account in a different location than the HDInsight cluster is not supported.</span></span>

## <a name="using-azure-data-lake-store-with-hdinsight-clusters"></a><span data-ttu-id="c9a30-251">Using Azure Data Lake Store with HDInsight clusters</span><span class="sxs-lookup"><span data-stu-id="c9a30-251">Using Azure Data Lake Store with HDInsight clusters</span></span>

<span data-ttu-id="c9a30-252">HDInsight clusters can use Azure Data Lake Store in two ways:</span><span class="sxs-lookup"><span data-stu-id="c9a30-252">HDInsight clusters can use Azure Data Lake Store in two ways:</span></span>

* <span data-ttu-id="c9a30-253">Azure Data Lake Store as the default storage</span><span class="sxs-lookup"><span data-stu-id="c9a30-253">Azure Data Lake Store as the default storage</span></span>
* <span data-ttu-id="c9a30-254">Azure Data Lake Store as additional storage, with Azure Storage Blob as default storage.</span><span class="sxs-lookup"><span data-stu-id="c9a30-254">Azure Data Lake Store as additional storage, with Azure Storage Blob as default storage.</span></span>

> [!NOTE]
> <span data-ttu-id="c9a30-255">Azure Data Lake Store is always accessed through a secure channel, so there is no `adls` filesystem scheme name.</span><span class="sxs-lookup"><span data-stu-id="c9a30-255">Azure Data Lake Store is always accessed through a secure channel, so there is no `adls` filesystem scheme name.</span></span> <span data-ttu-id="c9a30-256">You always use `adl`.</span><span class="sxs-lookup"><span data-stu-id="c9a30-256">You always use `adl`.</span></span>
> 
> 

### <a name="using-azure-data-lake-store-as-default-storage"></a><span data-ttu-id="c9a30-257">Using Azure Data Lake Store as default storage</span><span class="sxs-lookup"><span data-stu-id="c9a30-257">Using Azure Data Lake Store as default storage</span></span>

<span data-ttu-id="c9a30-258">When HDInsight is deployed with Azure Data Lake Store as default storage, the cluster-related files are stored in Azure Data Lake store in the following location:</span><span class="sxs-lookup"><span data-stu-id="c9a30-258">When HDInsight is deployed with Azure Data Lake Store as default storage, the cluster-related files are stored in Azure Data Lake store in the following location:</span></span>

    adl://mydatalakestore/<cluster_root_path>/

<span data-ttu-id="c9a30-259">where `<cluster_root_path>` is the name of a folder you create in Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="c9a30-259">where `<cluster_root_path>` is the name of a folder you create in Azure Data Lake Store.</span></span> <span data-ttu-id="c9a30-260">By specifying a root path for each cluster, you can use the same Azure Data Lake Store account for more than one cluster.</span><span class="sxs-lookup"><span data-stu-id="c9a30-260">By specifying a root path for each cluster, you can use the same Azure Data Lake Store account for more than one cluster.</span></span> <span data-ttu-id="c9a30-261">So, you can have a setup where:</span><span class="sxs-lookup"><span data-stu-id="c9a30-261">So, you can have a setup where:</span></span>

* <span data-ttu-id="c9a30-262">Cluster1 can use the path `adl://mydatalakestore/cluster1storage`</span><span class="sxs-lookup"><span data-stu-id="c9a30-262">Cluster1 can use the path `adl://mydatalakestore/cluster1storage`</span></span>
* <span data-ttu-id="c9a30-263">Cluster2 can use the path `adl://mydatalakestore/cluster2storage`</span><span class="sxs-lookup"><span data-stu-id="c9a30-263">Cluster2 can use the path `adl://mydatalakestore/cluster2storage`</span></span>

<span data-ttu-id="c9a30-264">Notice that both the clusters use the same Data Lake Store account **mydatalakestore**.</span><span class="sxs-lookup"><span data-stu-id="c9a30-264">Notice that both the clusters use the same Data Lake Store account **mydatalakestore**.</span></span> <span data-ttu-id="c9a30-265">Each cluster has access to its own root filesystem in Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="c9a30-265">Each cluster has access to its own root filesystem in Data Lake Store.</span></span> <span data-ttu-id="c9a30-266">The Azure portal deployment experience in particular prompts you to use a folder name such as **/clusters/\<clustername>** for the root path.</span><span class="sxs-lookup"><span data-stu-id="c9a30-266">The Azure portal deployment experience in particular prompts you to use a folder name such as **/clusters/\<clustername>** for the root path.</span></span>

#### <a name="accessing-files-from-the-cluster"></a><span data-ttu-id="c9a30-267">Accessing files from the cluster</span><span class="sxs-lookup"><span data-stu-id="c9a30-267">Accessing files from the cluster</span></span>

<span data-ttu-id="c9a30-268">There are a number of ways you can access the files in Azure Data Lake Store from an HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="c9a30-268">There are a number of ways you can access the files in Azure Data Lake Store from an HDInsight cluster.</span></span>

* <span data-ttu-id="c9a30-269">**Using the fully qualified name**.</span><span class="sxs-lookup"><span data-stu-id="c9a30-269">**Using the fully qualified name**.</span></span> <span data-ttu-id="c9a30-270">With this approach, you provide the full path to the file that you want to access.</span><span class="sxs-lookup"><span data-stu-id="c9a30-270">With this approach, you provide the full path to the file that you want to access.</span></span>

        adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/<file_path>

* <span data-ttu-id="c9a30-271">**Using the shortened path format**.</span><span class="sxs-lookup"><span data-stu-id="c9a30-271">**Using the shortened path format**.</span></span> <span data-ttu-id="c9a30-272">With this approach, you replace the path up to the cluster root with adl:///.</span><span class="sxs-lookup"><span data-stu-id="c9a30-272">With this approach, you replace the path up to the cluster root with adl:///.</span></span> <span data-ttu-id="c9a30-273">So, in the example above, you can replace `adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/` with `adl:///`.</span><span class="sxs-lookup"><span data-stu-id="c9a30-273">So, in the example above, you can replace `adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/` with `adl:///`.</span></span>

        adl:///<file path>

* <span data-ttu-id="c9a30-274">**Using the relative path**.</span><span class="sxs-lookup"><span data-stu-id="c9a30-274">**Using the relative path**.</span></span> <span data-ttu-id="c9a30-275">With this approach, you only provide the relative path to the file that you want to access.</span><span class="sxs-lookup"><span data-stu-id="c9a30-275">With this approach, you only provide the relative path to the file that you want to access.</span></span> <span data-ttu-id="c9a30-276">For example, if the complete path to the file is:</span><span class="sxs-lookup"><span data-stu-id="c9a30-276">For example, if the complete path to the file is:</span></span>

        adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/example/data/sample.log

    <span data-ttu-id="c9a30-277">You can access the same sample.log file by using this relative path instead.</span><span class="sxs-lookup"><span data-stu-id="c9a30-277">You can access the same sample.log file by using this relative path instead.</span></span>

        /example/data/sample.log

### <a name="using-azure-data-lake-store-as-additional-storage"></a><span data-ttu-id="c9a30-278">Using Azure Data Lake Store as additional storage</span><span class="sxs-lookup"><span data-stu-id="c9a30-278">Using Azure Data Lake Store as additional storage</span></span>

<span data-ttu-id="c9a30-279">You can use Data Lake Store as additional storage for the cluster as well.</span><span class="sxs-lookup"><span data-stu-id="c9a30-279">You can use Data Lake Store as additional storage for the cluster as well.</span></span> <span data-ttu-id="c9a30-280">In such cases, the cluster default storage can either be an Azure Storage Blob or an Azure Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="c9a30-280">In such cases, the cluster default storage can either be an Azure Storage Blob or an Azure Data Lake Store account.</span></span> <span data-ttu-id="c9a30-281">If you are running HDInsight jobs against the data stored in Azure Data Lake Store as additional storage, you must use the fully-qualified path to the files.</span><span class="sxs-lookup"><span data-stu-id="c9a30-281">If you are running HDInsight jobs against the data stored in Azure Data Lake Store as additional storage, you must use the fully-qualified path to the files.</span></span> <span data-ttu-id="c9a30-282">For example:</span><span class="sxs-lookup"><span data-stu-id="c9a30-282">For example:</span></span>

    adl://mydatalakestore.azuredatalakestore.net/<file_path>

<span data-ttu-id="c9a30-283">Note that there's no **cluster_root_path** in the URL now.</span><span class="sxs-lookup"><span data-stu-id="c9a30-283">Note that there's no **cluster_root_path** in the URL now.</span></span> <span data-ttu-id="c9a30-284">That's because Data Lake Store is not a default storage in this case so all you need to do is provide the path to the files.</span><span class="sxs-lookup"><span data-stu-id="c9a30-284">That's because Data Lake Store is not a default storage in this case so all you need to do is provide the path to the files.</span></span>


### <a name="creating-hdinsight-clusters-with-access-to-data-lake-store"></a><span data-ttu-id="c9a30-285">Creating HDInsight clusters with access to Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="c9a30-285">Creating HDInsight clusters with access to Data Lake Store</span></span>

<span data-ttu-id="c9a30-286">Follow the links below for detailed instructions on how to create HDInsight clusters with access to Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="c9a30-286">Follow the links below for detailed instructions on how to create HDInsight clusters with access to Data Lake Store.</span></span>

* [<span data-ttu-id="c9a30-287">Using Portal</span><span class="sxs-lookup"><span data-stu-id="c9a30-287">Using Portal</span></span>](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md)
* [<span data-ttu-id="c9a30-288">Using PowerShell (with Data Lake Store as default storage)</span><span class="sxs-lookup"><span data-stu-id="c9a30-288">Using PowerShell (with Data Lake Store as default storage)</span></span>](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
* [<span data-ttu-id="c9a30-289">Using PowerShell (with Data Lake Store as additional storage)</span><span class="sxs-lookup"><span data-stu-id="c9a30-289">Using PowerShell (with Data Lake Store as additional storage)</span></span>](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell.md)
* [<span data-ttu-id="c9a30-290">Using Azure templates</span><span class="sxs-lookup"><span data-stu-id="c9a30-290">Using Azure templates</span></span>](../data-lake-store/data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)


## <a name="next-steps"></a><span data-ttu-id="c9a30-291">Next steps</span><span class="sxs-lookup"><span data-stu-id="c9a30-291">Next steps</span></span>
<span data-ttu-id="c9a30-292">In this article, you learned how to use HDFS-compatible Azure storage and Azure Data Lake Store with HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c9a30-292">In this article, you learned how to use HDFS-compatible Azure storage and Azure Data Lake Store with HDInsight.</span></span> <span data-ttu-id="c9a30-293">This allows you to build scalable, long-term, archiving data acquisition solutions and use HDInsight to unlock the information inside the stored structured and unstructured data.</span><span class="sxs-lookup"><span data-stu-id="c9a30-293">This allows you to build scalable, long-term, archiving data acquisition solutions and use HDInsight to unlock the information inside the stored structured and unstructured data.</span></span>

<span data-ttu-id="c9a30-294">For more information, see:</span><span class="sxs-lookup"><span data-stu-id="c9a30-294">For more information, see:</span></span>

* <span data-ttu-id="c9a30-295">[Get started with Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="c9a30-295">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* [<span data-ttu-id="c9a30-296">Get started with Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="c9a30-296">Get started with Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-get-started-portal.md)
* <span data-ttu-id="c9a30-297">[Upload data to HDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="c9a30-297">[Upload data to HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="c9a30-298">[Use Hive with HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="c9a30-298">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="c9a30-299">[Use Pig with HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="c9a30-299">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="c9a30-300">[Use Azure Storage Shared Access Signatures to restrict access to data with HDInsight][hdinsight-use-sas]</span><span class="sxs-lookup"><span data-stu-id="c9a30-300">[Use Azure Storage Shared Access Signatures to restrict access to data with HDInsight][hdinsight-use-sas]</span></span>

[hdinsight-use-sas]: hdinsight-storage-sharedaccesssignature-permissions.md
[powershell-install]: /powershell/azureps-cmdlets-docs
[hdinsight-creation]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md

[blob-storage-restAPI]: http://msdn.microsoft.com/library/windowsazure/dd135733.aspx
[azure-storage-create]: ../storage/storage-create-storage-account.md

[img-hdi-powershell-blobcommands]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-use-blob-storage/HDI.PowerShell.BlobCommands.png
[img-hdi-quick-create]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-use-blob-storage/HDI.QuickCreateCluster.png
[img-hdi-custom-create-storage-account]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-use-blob-storage/HDI.CustomCreateStorageAccount.png  





