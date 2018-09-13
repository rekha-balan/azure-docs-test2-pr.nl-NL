---
title: Copy data to and from WASB into Data Lake Store using Distcp| Microsoft Docs
description: Use Distcp tool to copy data to and from Azure Storage Blobs to Data Lake Store
services: data-lake-store
documentationcenter: ''
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: ae2e9506-69dd-4b95-8759-4dadca37ea70
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/06/2017
ms.author: nitinme
ms.openlocfilehash: 12aea210308636677ba2905887ddd24dc5c35238
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550078"
---
# <a name="use-distcp-to-copy-data-between-azure-storage-blobs-and-data-lake-store"></a><span data-ttu-id="2b055-103">Use Distcp to copy data between Azure Storage Blobs and Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="2b055-103">Use Distcp to copy data between Azure Storage Blobs and Data Lake Store</span></span>
> [!div class="op_single_selector"]
> * [Using DistCp](data-lake-store-copy-data-wasb-distcp.md)
> * [Using AdlCopy](data-lake-store-copy-data-azure-storage-blob.md)
>
>

<span data-ttu-id="2b055-106">Once you have created an HDInsight cluster that has access to a Data Lake Store account, you can use Hadoop ecosystem tools like Distcp to copy data **to and from** an HDInsight cluster storage (WASB) into a Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="2b055-106">Once you have created an HDInsight cluster that has access to a Data Lake Store account, you can use Hadoop ecosystem tools like Distcp to copy data **to and from** an HDInsight cluster storage (WASB) into a Data Lake Store account.</span></span> <span data-ttu-id="2b055-107">This article provides instructions on how to achieve this.</span><span class="sxs-lookup"><span data-stu-id="2b055-107">This article provides instructions on how to achieve this.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2b055-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="2b055-108">Prerequisites</span></span>
<span data-ttu-id="2b055-109">Before you begin this article, you must have the following:</span><span class="sxs-lookup"><span data-stu-id="2b055-109">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="2b055-110">**An Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="2b055-110">**An Azure subscription**.</span></span> <span data-ttu-id="2b055-111">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2b055-111">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="2b055-112">**An Azure Data Lake Store account**.</span><span class="sxs-lookup"><span data-stu-id="2b055-112">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="2b055-113">For instructions on how to create one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="2b055-113">For instructions on how to create one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>
* <span data-ttu-id="2b055-114">**Azure HDInsight cluster** with access to a Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="2b055-114">**Azure HDInsight cluster** with access to a Data Lake Store account.</span></span> <span data-ttu-id="2b055-115">See [Create an HDInsight cluster with Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="2b055-115">See [Create an HDInsight cluster with Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md).</span></span> <span data-ttu-id="2b055-116">Make sure you enable Remote Desktop for the cluster.</span><span class="sxs-lookup"><span data-stu-id="2b055-116">Make sure you enable Remote Desktop for the cluster.</span></span>

## <a name="do-you-learn-fast-with-videos"></a><span data-ttu-id="2b055-117">Do you learn fast with videos?</span><span class="sxs-lookup"><span data-stu-id="2b055-117">Do you learn fast with videos?</span></span>
<span data-ttu-id="2b055-118">[Watch this video](https://mix.office.com/watch/1liuojvdx6sie) on how to copy data between Azure Storage Blobs and Data Lake Store using DistCp.</span><span class="sxs-lookup"><span data-stu-id="2b055-118">[Watch this video](https://mix.office.com/watch/1liuojvdx6sie) on how to copy data between Azure Storage Blobs and Data Lake Store using DistCp.</span></span>

## <a name="use-distcp-from-an-hdinsight-linux-cluster"></a><span data-ttu-id="2b055-119">Use Distcp from an HDInsight Linux cluster</span><span class="sxs-lookup"><span data-stu-id="2b055-119">Use Distcp from an HDInsight Linux cluster</span></span>

<span data-ttu-id="2b055-120">An HDInsight cluster comes with the Distcp utility, which can be used to copy data from different sources into an HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="2b055-120">An HDInsight cluster comes with the Distcp utility, which can be used to copy data from different sources into an HDInsight cluster.</span></span> <span data-ttu-id="2b055-121">If you have configured the HDInsight cluster to use Data Lake Store as an additional storage, the Distcp utility can be used out-of-the-box to copy data to and from a Data Lake Store account as well.</span><span class="sxs-lookup"><span data-stu-id="2b055-121">If you have configured the HDInsight cluster to use Data Lake Store as an additional storage, the Distcp utility can be used out-of-the-box to copy data to and from a Data Lake Store account as well.</span></span> <span data-ttu-id="2b055-122">In this section we look at how to use the Distcp utility.</span><span class="sxs-lookup"><span data-stu-id="2b055-122">In this section we look at how to use the Distcp utility.</span></span>

1. <span data-ttu-id="2b055-123">From your desktop, use SSH to connect to the cluster.</span><span class="sxs-lookup"><span data-stu-id="2b055-123">From your desktop, use SSH to connect to the cluster.</span></span> <span data-ttu-id="2b055-124">See [Connect to a Linux-based HDInsight cluster](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="2b055-124">See [Connect to a Linux-based HDInsight cluster](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span></span> <span data-ttu-id="2b055-125">Run the commands from the SSH prompt.</span><span class="sxs-lookup"><span data-stu-id="2b055-125">Run the commands from the SSH prompt.</span></span>

2. <span data-ttu-id="2b055-126">Verify whether you can access the Azure Storage Blobs (WASB).</span><span class="sxs-lookup"><span data-stu-id="2b055-126">Verify whether you can access the Azure Storage Blobs (WASB).</span></span> <span data-ttu-id="2b055-127">Run the following command:</span><span class="sxs-lookup"><span data-stu-id="2b055-127">Run the following command:</span></span>

        hdfs dfs –ls wasb://<container_name>@<storage_account_name>.blob.core.windows.net/

    <span data-ttu-id="2b055-128">This should provide a list of contents in the storage blob.</span><span class="sxs-lookup"><span data-stu-id="2b055-128">This should provide a list of contents in the storage blob.</span></span>
3. <span data-ttu-id="2b055-129">Similarly, verify whether you can access the Data Lake Store account from the cluster.</span><span class="sxs-lookup"><span data-stu-id="2b055-129">Similarly, verify whether you can access the Data Lake Store account from the cluster.</span></span> <span data-ttu-id="2b055-130">Run the following command:</span><span class="sxs-lookup"><span data-stu-id="2b055-130">Run the following command:</span></span>

        hdfs dfs -ls adl://<data_lake_store_account>.azuredatalakestore.net:443/

    <span data-ttu-id="2b055-131">This should provide a list of files/folders in the Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="2b055-131">This should provide a list of files/folders in the Data Lake Store account.</span></span>
4. <span data-ttu-id="2b055-132">Use Distcp to copy data from WASB to a Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="2b055-132">Use Distcp to copy data from WASB to a Data Lake Store account.</span></span>

        hadoop distcp wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder

    <span data-ttu-id="2b055-133">This will copy the contents of the **/example/data/gutenberg/** folder in WASB to **/myfolder** in the Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="2b055-133">This will copy the contents of the **/example/data/gutenberg/** folder in WASB to **/myfolder** in the Data Lake Store account.</span></span>
5. <span data-ttu-id="2b055-134">Similarly, use Distcp to copy data from Data Lake Store account to WASB.</span><span class="sxs-lookup"><span data-stu-id="2b055-134">Similarly, use Distcp to copy data from Data Lake Store account to WASB.</span></span>

        hadoop distcp adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg

    <span data-ttu-id="2b055-135">This will copy the contents of **/myfolder** in the Data Lake Store account to **/example/data/gutenberg/** folder in WASB.</span><span class="sxs-lookup"><span data-stu-id="2b055-135">This will copy the contents of **/myfolder** in the Data Lake Store account to **/example/data/gutenberg/** folder in WASB.</span></span>

## <a name="performance-considerations-while-using-distcp"></a><span data-ttu-id="2b055-136">Performance considerations while using DistCp</span><span class="sxs-lookup"><span data-stu-id="2b055-136">Performance considerations while using DistCp</span></span>

<span data-ttu-id="2b055-137">Because DistCp’s lowest granularity is a single file, setting the maximum number of simultaneous copies is the most important parameter to optimize it against Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="2b055-137">Because DistCp’s lowest granularity is a single file, setting the maximum number of simultaneous copies is the most important parameter to optimize it against Data Lake Store.</span></span> <span data-ttu-id="2b055-138">This is controlled by setting the number of mappers (‘m’) parameter on the command line.</span><span class="sxs-lookup"><span data-stu-id="2b055-138">This is controlled by setting the number of mappers (‘m’) parameter on the command line.</span></span> <span data-ttu-id="2b055-139">This parameter specifies the maximum number of mappers that will be used to copy data.</span><span class="sxs-lookup"><span data-stu-id="2b055-139">This parameter specifies the maximum number of mappers that will be used to copy data.</span></span> <span data-ttu-id="2b055-140">Default value is 20.</span><span class="sxs-lookup"><span data-stu-id="2b055-140">Default value is 20.</span></span>

<span data-ttu-id="2b055-141">**Example**</span><span class="sxs-lookup"><span data-stu-id="2b055-141">**Example**</span></span>

    hadoop distcp wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder -m 100

### <a name="how-do-i-determine-the-number-of-mappers-to-use"></a><span data-ttu-id="2b055-142">How do I determine the number of mappers to use?</span><span class="sxs-lookup"><span data-stu-id="2b055-142">How do I determine the number of mappers to use?</span></span>

<span data-ttu-id="2b055-143">Here's some guidance that you can use.</span><span class="sxs-lookup"><span data-stu-id="2b055-143">Here's some guidance that you can use.</span></span>

* <span data-ttu-id="2b055-144">**Step 1: Determine total YARN memory** - The first step is to determine the YARN memory available to the cluster where you run the DistCp job.</span><span class="sxs-lookup"><span data-stu-id="2b055-144">**Step 1: Determine total YARN memory** - The first step is to determine the YARN memory available to the cluster where you run the DistCp job.</span></span> <span data-ttu-id="2b055-145">This information is available in the Ambari portal associated with the cluster.</span><span class="sxs-lookup"><span data-stu-id="2b055-145">This information is available in the Ambari portal associated with the cluster.</span></span> <span data-ttu-id="2b055-146">Navigate to YARN and view the Configs tab to see the YARN memory.</span><span class="sxs-lookup"><span data-stu-id="2b055-146">Navigate to YARN and view the Configs tab to see the YARN memory.</span></span> <span data-ttu-id="2b055-147">To get the total YARN memory, multiply the YARN memory per node with the number of nodes you have in your cluster.</span><span class="sxs-lookup"><span data-stu-id="2b055-147">To get the total YARN memory, multiply the YARN memory per node with the number of nodes you have in your cluster.</span></span>

* <span data-ttu-id="2b055-148">**Step 2: Calculate the number of mappers** - The value of **m** is equal to the quotient of total YARN memory divided by the YARN container size.</span><span class="sxs-lookup"><span data-stu-id="2b055-148">**Step 2: Calculate the number of mappers** - The value of **m** is equal to the quotient of total YARN memory divided by the YARN container size.</span></span> <span data-ttu-id="2b055-149">The YARN container size information is available in the Ambari portal as well.</span><span class="sxs-lookup"><span data-stu-id="2b055-149">The YARN container size information is available in the Ambari portal as well.</span></span> <span data-ttu-id="2b055-150">Navigate to YARN and view the Configs tab. The YARN container size is displayed in this window.</span><span class="sxs-lookup"><span data-stu-id="2b055-150">Navigate to YARN and view the Configs tab. The YARN container size is displayed in this window.</span></span> <span data-ttu-id="2b055-151">The equation to arrive at the number of mappers (**m**) is</span><span class="sxs-lookup"><span data-stu-id="2b055-151">The equation to arrive at the number of mappers (**m**) is</span></span>

        m = (number of nodes * YARN memory for each node) / YARN container size

<span data-ttu-id="2b055-152">**Example**</span><span class="sxs-lookup"><span data-stu-id="2b055-152">**Example**</span></span>

<span data-ttu-id="2b055-153">Let’s assume that you have a 4 D14v2s nodes in the cluster and you are trying to transfer 10TB of data from 10 different folders.</span><span class="sxs-lookup"><span data-stu-id="2b055-153">Let’s assume that you have a 4 D14v2s nodes in the cluster and you are trying to transfer 10TB of data from 10 different folders.</span></span> <span data-ttu-id="2b055-154">Each of the folders contain varying amounts of data and the file sizes within each folder are different.</span><span class="sxs-lookup"><span data-stu-id="2b055-154">Each of the folders contain varying amounts of data and the file sizes within each folder are different.</span></span>

* <span data-ttu-id="2b055-155">Total YARN memory - From the Ambari portal you determine that the YARN memory is 96GB for a D14 node.</span><span class="sxs-lookup"><span data-stu-id="2b055-155">Total YARN memory - From the Ambari portal you determine that the YARN memory is 96GB for a D14 node.</span></span> <span data-ttu-id="2b055-156">So, total YARN memory for 4 node cluster is:</span><span class="sxs-lookup"><span data-stu-id="2b055-156">So, total YARN memory for 4 node cluster is:</span></span> 

        YARN memory = 4 * 96GB = 384GB

* <span data-ttu-id="2b055-157">Number of mappers - From the Ambari portal you determine that the YARN container size is 3072 for a D14 cluster node.</span><span class="sxs-lookup"><span data-stu-id="2b055-157">Number of mappers - From the Ambari portal you determine that the YARN container size is 3072 for a D14 cluster node.</span></span> <span data-ttu-id="2b055-158">So, number of mappers is:</span><span class="sxs-lookup"><span data-stu-id="2b055-158">So, number of mappers is:</span></span>

        m = (4 nodes * 96GB) / 3072MB = 128 mappers

<span data-ttu-id="2b055-159">If other applications are using memory, then you can choose to only use a portion of your cluster’s YARN memory for DistCp.</span><span class="sxs-lookup"><span data-stu-id="2b055-159">If other applications are using memory, then you can choose to only use a portion of your cluster’s YARN memory for DistCp.</span></span>

### <a name="copying-large-datasets"></a><span data-ttu-id="2b055-160">Copying large datasets</span><span class="sxs-lookup"><span data-stu-id="2b055-160">Copying large datasets</span></span>

<span data-ttu-id="2b055-161">When the size of the dataset to be moved is very large (e.g. >1TB) or if you have many different folders, you should consider using multiple DistCp jobs.</span><span class="sxs-lookup"><span data-stu-id="2b055-161">When the size of the dataset to be moved is very large (e.g. >1TB) or if you have many different folders, you should consider using multiple DistCp jobs.</span></span> <span data-ttu-id="2b055-162">There is likely no performance gain, but it will spread out the jobs so that if any job fails, you will only need to restart that specific job rather than the entire job.</span><span class="sxs-lookup"><span data-stu-id="2b055-162">There is likely no performance gain, but it will spread out the jobs so that if any job fails, you will only need to restart that specific job rather than the entire job.</span></span>

### <a name="limitations"></a><span data-ttu-id="2b055-163">Limitations</span><span class="sxs-lookup"><span data-stu-id="2b055-163">Limitations</span></span>

* <span data-ttu-id="2b055-164">DistCp tries to create mappers that are similar in size to optimize performance.</span><span class="sxs-lookup"><span data-stu-id="2b055-164">DistCp tries to create mappers that are similar in size to optimize performance.</span></span> <span data-ttu-id="2b055-165">Increasing the number of mappers may not always increase performance.</span><span class="sxs-lookup"><span data-stu-id="2b055-165">Increasing the number of mappers may not always increase performance.</span></span>

* <span data-ttu-id="2b055-166">DistCp is limited to only one mapper per file.</span><span class="sxs-lookup"><span data-stu-id="2b055-166">DistCp is limited to only one mapper per file.</span></span> <span data-ttu-id="2b055-167">Therefore, you should not have more mappers than you have files.</span><span class="sxs-lookup"><span data-stu-id="2b055-167">Therefore, you should not have more mappers than you have files.</span></span> <span data-ttu-id="2b055-168">Since DistCp can only assign one mapper to a file, this limits the amount of concurrency that can be used to copy large files.</span><span class="sxs-lookup"><span data-stu-id="2b055-168">Since DistCp can only assign one mapper to a file, this limits the amount of concurrency that can be used to copy large files.</span></span>

* <span data-ttu-id="2b055-169">If you have a small number of large files, then you should split them into 256MB file chunks to give you more potential concurrency.</span><span class="sxs-lookup"><span data-stu-id="2b055-169">If you have a small number of large files, then you should split them into 256MB file chunks to give you more potential concurrency.</span></span> 
 
* <span data-ttu-id="2b055-170">If you are copying from an Azure Blob Storage account, your copy job may be throttled on the blob storage side.</span><span class="sxs-lookup"><span data-stu-id="2b055-170">If you are copying from an Azure Blob Storage account, your copy job may be throttled on the blob storage side.</span></span> <span data-ttu-id="2b055-171">This will degrade the performance of your copy job.</span><span class="sxs-lookup"><span data-stu-id="2b055-171">This will degrade the performance of your copy job.</span></span> <span data-ttu-id="2b055-172">To learn more about the limits of Azure Blob Storage, see Azure Storage limits at [Azure subscription and service limits](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="2b055-172">To learn more about the limits of Azure Blob Storage, see Azure Storage limits at [Azure subscription and service limits](../azure-subscription-service-limits.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="2b055-173">See also</span><span class="sxs-lookup"><span data-stu-id="2b055-173">See also</span></span>
* [<span data-ttu-id="2b055-174">Copy data from Azure Storage Blobs to Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="2b055-174">Copy data from Azure Storage Blobs to Data Lake Store</span></span>](data-lake-store-copy-data-azure-storage-blob.md)
* [<span data-ttu-id="2b055-175">Secure data in Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="2b055-175">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="2b055-176">Use Azure Data Lake Analytics with Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="2b055-176">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="2b055-177">Use Azure HDInsight with Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="2b055-177">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
