---
title: Copy data to and from WASB into Azure Data Lake Storage Gen1 using Distcp| Microsoft Docs
description: Use Distcp tool to copy data to and from Azure Storage Blobs to Azure Data Lake Storage Gen1
services: data-lake-store
documentationcenter: ''
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: ae2e9506-69dd-4b95-8759-4dadca37ea70
ms.service: data-lake-store
ms.devlang: na
ms.topic: conceptual
ms.date: 05/29/2018
ms.author: nitinme
ms.openlocfilehash: 9740de34fe7cf7d06af1803cc6d77d7e89bbb73f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44827411"
---
# <a name="use-distcp-to-copy-data-between-azure-storage-blobs-and-azure-data-lake-storage-gen1"></a><span data-ttu-id="7a093-103">Use Distcp to copy data between Azure Storage Blobs and Azure Data Lake Storage Gen1</span><span class="sxs-lookup"><span data-stu-id="7a093-103">Use Distcp to copy data between Azure Storage Blobs and Azure Data Lake Storage Gen1</span></span>
> [!div class="op_single_selector"]
> * [Using DistCp](data-lake-store-copy-data-wasb-distcp.md)
> * [Using AdlCopy](data-lake-store-copy-data-azure-storage-blob.md)
>
>

<span data-ttu-id="7a093-106">If you have an HDInsight cluster with access to Azure Data Lake Storage Gen1, you can use Hadoop ecosystem tools like Distcp to copy data **to and from** an HDInsight cluster storage (WASB) into a Data Lake Storage Gen1 account.</span><span class="sxs-lookup"><span data-stu-id="7a093-106">If you have an HDInsight cluster with access to Azure Data Lake Storage Gen1, you can use Hadoop ecosystem tools like Distcp to copy data **to and from** an HDInsight cluster storage (WASB) into a Data Lake Storage Gen1 account.</span></span> <span data-ttu-id="7a093-107">This article provides instructions on how use the Distcp tool.</span><span class="sxs-lookup"><span data-stu-id="7a093-107">This article provides instructions on how use the Distcp tool.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7a093-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="7a093-108">Prerequisites</span></span>

* <span data-ttu-id="7a093-109">**An Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="7a093-109">**An Azure subscription**.</span></span> <span data-ttu-id="7a093-110">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7a093-110">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="7a093-111">**An Azure Data Lake Storage Gen1 account**.</span><span class="sxs-lookup"><span data-stu-id="7a093-111">**An Azure Data Lake Storage Gen1 account**.</span></span> <span data-ttu-id="7a093-112">For instructions on how to create one, see [Get started with Azure Data Lake Storage Gen1](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="7a093-112">For instructions on how to create one, see [Get started with Azure Data Lake Storage Gen1](data-lake-store-get-started-portal.md)</span></span>
* <span data-ttu-id="7a093-113">**Azure HDInsight cluster** with access to a Data Lake Storage Gen1 account.</span><span class="sxs-lookup"><span data-stu-id="7a093-113">**Azure HDInsight cluster** with access to a Data Lake Storage Gen1 account.</span></span> <span data-ttu-id="7a093-114">See [Create an HDInsight cluster with Data Lake Storage Gen1](data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="7a093-114">See [Create an HDInsight cluster with Data Lake Storage Gen1](data-lake-store-hdinsight-hadoop-use-portal.md).</span></span> <span data-ttu-id="7a093-115">Make sure you enable Remote Desktop for the cluster.</span><span class="sxs-lookup"><span data-stu-id="7a093-115">Make sure you enable Remote Desktop for the cluster.</span></span>

## <a name="do-you-learn-fast-with-videos"></a><span data-ttu-id="7a093-116">Do you learn fast with videos?</span><span class="sxs-lookup"><span data-stu-id="7a093-116">Do you learn fast with videos?</span></span>
<span data-ttu-id="7a093-117">[Watch this video](https://mix.office.com/watch/1liuojvdx6sie) on how to copy data between Azure Storage Blobs and Data Lake Storage Gen1 using DistCp.</span><span class="sxs-lookup"><span data-stu-id="7a093-117">[Watch this video](https://mix.office.com/watch/1liuojvdx6sie) on how to copy data between Azure Storage Blobs and Data Lake Storage Gen1 using DistCp.</span></span>

## <a name="use-distcp-from-an-hdinsight-linux-cluster"></a><span data-ttu-id="7a093-118">Use Distcp from an HDInsight Linux cluster</span><span class="sxs-lookup"><span data-stu-id="7a093-118">Use Distcp from an HDInsight Linux cluster</span></span>

<span data-ttu-id="7a093-119">An HDInsight cluster comes with the Distcp utility, which can be used to copy data from different sources into an HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="7a093-119">An HDInsight cluster comes with the Distcp utility, which can be used to copy data from different sources into an HDInsight cluster.</span></span> <span data-ttu-id="7a093-120">If you have configured the HDInsight cluster to use Data Lake Storage Gen1 as additional storage, the Distcp utility can be used out-of-the-box to copy data to and from a Data Lake Storage Gen1 account as well.</span><span class="sxs-lookup"><span data-stu-id="7a093-120">If you have configured the HDInsight cluster to use Data Lake Storage Gen1 as additional storage, the Distcp utility can be used out-of-the-box to copy data to and from a Data Lake Storage Gen1 account as well.</span></span> <span data-ttu-id="7a093-121">In this section, we look at how to use the Distcp utility.</span><span class="sxs-lookup"><span data-stu-id="7a093-121">In this section, we look at how to use the Distcp utility.</span></span>

1. <span data-ttu-id="7a093-122">From your desktop, use SSH to connect to the cluster.</span><span class="sxs-lookup"><span data-stu-id="7a093-122">From your desktop, use SSH to connect to the cluster.</span></span> <span data-ttu-id="7a093-123">See [Connect to a Linux-based HDInsight cluster](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="7a093-123">See [Connect to a Linux-based HDInsight cluster](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span></span> <span data-ttu-id="7a093-124">Run the commands from the SSH prompt.</span><span class="sxs-lookup"><span data-stu-id="7a093-124">Run the commands from the SSH prompt.</span></span>

2. <span data-ttu-id="7a093-125">Verify whether you can access the Azure Storage Blobs (WASB).</span><span class="sxs-lookup"><span data-stu-id="7a093-125">Verify whether you can access the Azure Storage Blobs (WASB).</span></span> <span data-ttu-id="7a093-126">Run the following command:</span><span class="sxs-lookup"><span data-stu-id="7a093-126">Run the following command:</span></span>

        hdfs dfs –ls wasb://<container_name>@<storage_account_name>.blob.core.windows.net/

    <span data-ttu-id="7a093-127">The output should provide a list of contents in the storage blob.</span><span class="sxs-lookup"><span data-stu-id="7a093-127">The output should provide a list of contents in the storage blob.</span></span>

3. <span data-ttu-id="7a093-128">Similarly, verify whether you can access the Data Lake Storage Gen1 account from the cluster.</span><span class="sxs-lookup"><span data-stu-id="7a093-128">Similarly, verify whether you can access the Data Lake Storage Gen1 account from the cluster.</span></span> <span data-ttu-id="7a093-129">Run the following command:</span><span class="sxs-lookup"><span data-stu-id="7a093-129">Run the following command:</span></span>

        hdfs dfs -ls adl://<data_lake_storage_gen1_account>.azuredatalakestore.net:443/

    <span data-ttu-id="7a093-130">The output should provide a list of files/folders in the Data Lake Storage Gen1 account.</span><span class="sxs-lookup"><span data-stu-id="7a093-130">The output should provide a list of files/folders in the Data Lake Storage Gen1 account.</span></span>

4. <span data-ttu-id="7a093-131">Use Distcp to copy data from WASB to a Data Lake Storage Gen1 account.</span><span class="sxs-lookup"><span data-stu-id="7a093-131">Use Distcp to copy data from WASB to a Data Lake Storage Gen1 account.</span></span>

        hadoop distcp wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg adl://<data_lake_storage_gen1_account>.azuredatalakestore.net:443/myfolder

    <span data-ttu-id="7a093-132">The command copies the contents of the **/example/data/gutenberg/** folder in WASB to **/myfolder** in the Data Lake Storage Gen1 account.</span><span class="sxs-lookup"><span data-stu-id="7a093-132">The command copies the contents of the **/example/data/gutenberg/** folder in WASB to **/myfolder** in the Data Lake Storage Gen1 account.</span></span>

5. <span data-ttu-id="7a093-133">Similarly, use Distcp to copy data from Data Lake Storage Gen1 account to WASB.</span><span class="sxs-lookup"><span data-stu-id="7a093-133">Similarly, use Distcp to copy data from Data Lake Storage Gen1 account to WASB.</span></span>

        hadoop distcp adl://<data_lake_storage_gen1_account>.azuredatalakestore.net:443/myfolder wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg

    <span data-ttu-id="7a093-134">THe command copies the contents of **/myfolder** in the Data Lake Storage Gen1 account to **/example/data/gutenberg/** folder in WASB.</span><span class="sxs-lookup"><span data-stu-id="7a093-134">THe command copies the contents of **/myfolder** in the Data Lake Storage Gen1 account to **/example/data/gutenberg/** folder in WASB.</span></span>

## <a name="performance-considerations-while-using-distcp"></a><span data-ttu-id="7a093-135">Performance considerations while using DistCp</span><span class="sxs-lookup"><span data-stu-id="7a093-135">Performance considerations while using DistCp</span></span>

<span data-ttu-id="7a093-136">Because DistCp’s lowest granularity is a single file, setting the maximum number of simultaneous copies is the most important parameter to optimize it against Data Lake Storage Gen1.</span><span class="sxs-lookup"><span data-stu-id="7a093-136">Because DistCp’s lowest granularity is a single file, setting the maximum number of simultaneous copies is the most important parameter to optimize it against Data Lake Storage Gen1.</span></span> <span data-ttu-id="7a093-137">Number of simultaneous copies is controlled by setting the number of mappers (‘m’) parameter on the command line.</span><span class="sxs-lookup"><span data-stu-id="7a093-137">Number of simultaneous copies is controlled by setting the number of mappers (‘m’) parameter on the command line.</span></span> <span data-ttu-id="7a093-138">This parameter specifies the maximum number of mappers that are used to copy data.</span><span class="sxs-lookup"><span data-stu-id="7a093-138">This parameter specifies the maximum number of mappers that are used to copy data.</span></span> <span data-ttu-id="7a093-139">Default value is 20.</span><span class="sxs-lookup"><span data-stu-id="7a093-139">Default value is 20.</span></span>

<span data-ttu-id="7a093-140">**Example**</span><span class="sxs-lookup"><span data-stu-id="7a093-140">**Example**</span></span>

    hadoop distcp wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg adl://<data_lake_storage_gen1_account>.azuredatalakestore.net:443/myfolder -m 100

### <a name="how-do-i-determine-the-number-of-mappers-to-use"></a><span data-ttu-id="7a093-141">How do I determine the number of mappers to use?</span><span class="sxs-lookup"><span data-stu-id="7a093-141">How do I determine the number of mappers to use?</span></span>

<span data-ttu-id="7a093-142">Here's some guidance that you can use.</span><span class="sxs-lookup"><span data-stu-id="7a093-142">Here's some guidance that you can use.</span></span>

* <span data-ttu-id="7a093-143">**Step 1: Determine total YARN memory** - The first step is to determine the YARN memory available to the cluster where you run the DistCp job.</span><span class="sxs-lookup"><span data-stu-id="7a093-143">**Step 1: Determine total YARN memory** - The first step is to determine the YARN memory available to the cluster where you run the DistCp job.</span></span> <span data-ttu-id="7a093-144">This information is available in the Ambari portal associated with the cluster.</span><span class="sxs-lookup"><span data-stu-id="7a093-144">This information is available in the Ambari portal associated with the cluster.</span></span> <span data-ttu-id="7a093-145">Navigate to YARN and view the Configs tab to see the YARN memory.</span><span class="sxs-lookup"><span data-stu-id="7a093-145">Navigate to YARN and view the Configs tab to see the YARN memory.</span></span> <span data-ttu-id="7a093-146">To get the total YARN memory, multiply the YARN memory per node with the number of nodes you have in your cluster.</span><span class="sxs-lookup"><span data-stu-id="7a093-146">To get the total YARN memory, multiply the YARN memory per node with the number of nodes you have in your cluster.</span></span>

* <span data-ttu-id="7a093-147">**Step 2: Calculate the number of mappers** - The value of **m** is equal to the quotient of total YARN memory divided by the YARN container size.</span><span class="sxs-lookup"><span data-stu-id="7a093-147">**Step 2: Calculate the number of mappers** - The value of **m** is equal to the quotient of total YARN memory divided by the YARN container size.</span></span> <span data-ttu-id="7a093-148">The YARN container size information is available in the Ambari portal as well.</span><span class="sxs-lookup"><span data-stu-id="7a093-148">The YARN container size information is available in the Ambari portal as well.</span></span> <span data-ttu-id="7a093-149">Navigate to YARN and view the Configs tab. The YARN container size is displayed in this window.</span><span class="sxs-lookup"><span data-stu-id="7a093-149">Navigate to YARN and view the Configs tab. The YARN container size is displayed in this window.</span></span> <span data-ttu-id="7a093-150">The equation to arrive at the number of mappers (**m**) is</span><span class="sxs-lookup"><span data-stu-id="7a093-150">The equation to arrive at the number of mappers (**m**) is</span></span>

        m = (number of nodes * YARN memory for each node) / YARN container size

<span data-ttu-id="7a093-151">**Example**</span><span class="sxs-lookup"><span data-stu-id="7a093-151">**Example**</span></span>

<span data-ttu-id="7a093-152">Let’s assume that you have a 4 D14v2s nodes in the cluster and you are trying to transfer 10 TB of data from 10 different folders.</span><span class="sxs-lookup"><span data-stu-id="7a093-152">Let’s assume that you have a 4 D14v2s nodes in the cluster and you are trying to transfer 10 TB of data from 10 different folders.</span></span> <span data-ttu-id="7a093-153">Each of the folders contains varying amounts of data and the file sizes within each folder are different.</span><span class="sxs-lookup"><span data-stu-id="7a093-153">Each of the folders contains varying amounts of data and the file sizes within each folder are different.</span></span>

* <span data-ttu-id="7a093-154">Total YARN memory - From the Ambari portal you determine that the YARN memory is 96 GB for a D14 node.</span><span class="sxs-lookup"><span data-stu-id="7a093-154">Total YARN memory - From the Ambari portal you determine that the YARN memory is 96 GB for a D14 node.</span></span> <span data-ttu-id="7a093-155">So, total YARN memory for four node cluster is:</span><span class="sxs-lookup"><span data-stu-id="7a093-155">So, total YARN memory for four node cluster is:</span></span> 

        YARN memory = 4 * 96GB = 384GB

* <span data-ttu-id="7a093-156">Number of mappers - From the Ambari portal you determine that the YARN container size is 3072 for a D14 cluster node.</span><span class="sxs-lookup"><span data-stu-id="7a093-156">Number of mappers - From the Ambari portal you determine that the YARN container size is 3072 for a D14 cluster node.</span></span> <span data-ttu-id="7a093-157">So, number of mappers is:</span><span class="sxs-lookup"><span data-stu-id="7a093-157">So, number of mappers is:</span></span>

        m = (4 nodes * 96GB) / 3072MB = 128 mappers

<span data-ttu-id="7a093-158">If other applications are using memory, then you can choose to only use a portion of your cluster’s YARN memory for DistCp.</span><span class="sxs-lookup"><span data-stu-id="7a093-158">If other applications are using memory, then you can choose to only use a portion of your cluster’s YARN memory for DistCp.</span></span>

### <a name="copying-large-datasets"></a><span data-ttu-id="7a093-159">Copying large datasets</span><span class="sxs-lookup"><span data-stu-id="7a093-159">Copying large datasets</span></span>

<span data-ttu-id="7a093-160">When the size of the dataset to be moved is large (for example, >1 TB) or if you have many different folders, you should consider using multiple DistCp jobs.</span><span class="sxs-lookup"><span data-stu-id="7a093-160">When the size of the dataset to be moved is large (for example, >1 TB) or if you have many different folders, you should consider using multiple DistCp jobs.</span></span> <span data-ttu-id="7a093-161">There is likely no performance gain, but it spreads out the jobs so that if any job fails, you only need to restart that specific job rather than the entire job.</span><span class="sxs-lookup"><span data-stu-id="7a093-161">There is likely no performance gain, but it spreads out the jobs so that if any job fails, you only need to restart that specific job rather than the entire job.</span></span>

### <a name="limitations"></a><span data-ttu-id="7a093-162">Limitations</span><span class="sxs-lookup"><span data-stu-id="7a093-162">Limitations</span></span>

* <span data-ttu-id="7a093-163">DistCp tries to create mappers that are similar in size to optimize performance.</span><span class="sxs-lookup"><span data-stu-id="7a093-163">DistCp tries to create mappers that are similar in size to optimize performance.</span></span> <span data-ttu-id="7a093-164">Increasing the number of mappers may not always increase performance.</span><span class="sxs-lookup"><span data-stu-id="7a093-164">Increasing the number of mappers may not always increase performance.</span></span>

* <span data-ttu-id="7a093-165">DistCp is limited to only one mapper per file.</span><span class="sxs-lookup"><span data-stu-id="7a093-165">DistCp is limited to only one mapper per file.</span></span> <span data-ttu-id="7a093-166">Therefore, you should not have more mappers than you have files.</span><span class="sxs-lookup"><span data-stu-id="7a093-166">Therefore, you should not have more mappers than you have files.</span></span> <span data-ttu-id="7a093-167">Since DistCp can only assign one mapper to a file, this limits the amount of concurrency that can be used to copy large files.</span><span class="sxs-lookup"><span data-stu-id="7a093-167">Since DistCp can only assign one mapper to a file, this limits the amount of concurrency that can be used to copy large files.</span></span>

* <span data-ttu-id="7a093-168">If you have a small number of large files, then you should split them into 256 MB file chunks to give you more potential concurrency.</span><span class="sxs-lookup"><span data-stu-id="7a093-168">If you have a small number of large files, then you should split them into 256 MB file chunks to give you more potential concurrency.</span></span> 
 
* <span data-ttu-id="7a093-169">If you are copying from an Azure Blob Storage account, your copy job may be throttled on the blob storage side.</span><span class="sxs-lookup"><span data-stu-id="7a093-169">If you are copying from an Azure Blob Storage account, your copy job may be throttled on the blob storage side.</span></span> <span data-ttu-id="7a093-170">This degrades the performance of your copy job.</span><span class="sxs-lookup"><span data-stu-id="7a093-170">This degrades the performance of your copy job.</span></span> <span data-ttu-id="7a093-171">To learn more about the limits of Azure Blob Storage, see Azure Storage limits at [Azure subscription and service limits](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="7a093-171">To learn more about the limits of Azure Blob Storage, see Azure Storage limits at [Azure subscription and service limits](../azure-subscription-service-limits.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="7a093-172">See also</span><span class="sxs-lookup"><span data-stu-id="7a093-172">See also</span></span>
* [<span data-ttu-id="7a093-173">Copy data from Azure Storage Blobs to Data Lake Storage Gen1</span><span class="sxs-lookup"><span data-stu-id="7a093-173">Copy data from Azure Storage Blobs to Data Lake Storage Gen1</span></span>](data-lake-store-copy-data-azure-storage-blob.md)
* [<span data-ttu-id="7a093-174">Secure data in Data Lake Storage Gen1</span><span class="sxs-lookup"><span data-stu-id="7a093-174">Secure data in Data Lake Storage Gen1</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="7a093-175">Use Azure Data Lake Analytics with Data Lake Storage Gen1</span><span class="sxs-lookup"><span data-stu-id="7a093-175">Use Azure Data Lake Analytics with Data Lake Storage Gen1</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="7a093-176">Use Azure HDInsight with Data Lake Storage Gen1</span><span class="sxs-lookup"><span data-stu-id="7a093-176">Use Azure HDInsight with Data Lake Storage Gen1</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
