---
title: Azure Storage solutions for ML Services on HDInsight - Azure
description: Learn about the different storage options available with ML Services on HDInsight
services: hdinsight
ms.service: hdinsight
author: jasonwhowell
ms.author: jasonh
ms.reviewer: jasonh
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 06/27/2018
ms.openlocfilehash: 5bd5919efa84f2dd22929075b806747b413ac346
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870777"
---
# <a name="azure-storage-solutions-for-ml-services-on-azure-hdinsight"></a><span data-ttu-id="cb861-103">Azure Storage solutions for ML Services on Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="cb861-103">Azure Storage solutions for ML Services on Azure HDInsight</span></span>

<span data-ttu-id="cb861-104">ML Services on HDInsight can use a variety of storage solutions to persist data, code, or objects that contain results from analysis.</span><span class="sxs-lookup"><span data-stu-id="cb861-104">ML Services on HDInsight can use a variety of storage solutions to persist data, code, or objects that contain results from analysis.</span></span> <span data-ttu-id="cb861-105">These include the following options:</span><span class="sxs-lookup"><span data-stu-id="cb861-105">These include the following options:</span></span>

- [<span data-ttu-id="cb861-106">Azure Blob</span><span class="sxs-lookup"><span data-stu-id="cb861-106">Azure Blob</span></span>](https://azure.microsoft.com/services/storage/blobs/)
- [<span data-ttu-id="cb861-107">Azure Data Lake Storage</span><span class="sxs-lookup"><span data-stu-id="cb861-107">Azure Data Lake Storage</span></span>](https://azure.microsoft.com/services/data-lake-store/)
- [<span data-ttu-id="cb861-108">Azure File storage</span><span class="sxs-lookup"><span data-stu-id="cb861-108">Azure File storage</span></span>](https://azure.microsoft.com/services/storage/files/)

<span data-ttu-id="cb861-109">You also have the option of accessing multiple Azure storage accounts or containers with your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="cb861-109">You also have the option of accessing multiple Azure storage accounts or containers with your HDInsight cluster.</span></span> <span data-ttu-id="cb861-110">Azure File storage is a convenient data storage option for use on the edge node that enables you to mount an Azure Storage file share to, for example, the Linux file system.</span><span class="sxs-lookup"><span data-stu-id="cb861-110">Azure File storage is a convenient data storage option for use on the edge node that enables you to mount an Azure Storage file share to, for example, the Linux file system.</span></span> <span data-ttu-id="cb861-111">But Azure File shares can be mounted and used by any system that has a supported operating system such as Windows or Linux.</span><span class="sxs-lookup"><span data-stu-id="cb861-111">But Azure File shares can be mounted and used by any system that has a supported operating system such as Windows or Linux.</span></span> 

<span data-ttu-id="cb861-112">When you create a Hadoop cluster in HDInsight, you specify either an **Azure storage** account or a **Data Lake store**.</span><span class="sxs-lookup"><span data-stu-id="cb861-112">When you create a Hadoop cluster in HDInsight, you specify either an **Azure storage** account or a **Data Lake store**.</span></span> <span data-ttu-id="cb861-113">A specific storage container from that account holds the file system for the cluster that you create (for example, the Hadoop Distributed File System).</span><span class="sxs-lookup"><span data-stu-id="cb861-113">A specific storage container from that account holds the file system for the cluster that you create (for example, the Hadoop Distributed File System).</span></span> <span data-ttu-id="cb861-114">For more information and guidance, see:</span><span class="sxs-lookup"><span data-stu-id="cb861-114">For more information and guidance, see:</span></span>

- [<span data-ttu-id="cb861-115">Use Azure storage with HDInsight</span><span class="sxs-lookup"><span data-stu-id="cb861-115">Use Azure storage with HDInsight</span></span>](../hdinsight-hadoop-use-blob-storage.md)
- [<span data-ttu-id="cb861-116">Use Data Lake Store with Azure HDInsight clusters</span><span class="sxs-lookup"><span data-stu-id="cb861-116">Use Data Lake Store with Azure HDInsight clusters</span></span>](../hdinsight-hadoop-use-data-lake-store.md)

## <a name="use-azure-blob-storage-accounts-with-ml-services-cluster"></a><span data-ttu-id="cb861-117">Use Azure Blob storage accounts with ML Services cluster</span><span class="sxs-lookup"><span data-stu-id="cb861-117">Use Azure Blob storage accounts with ML Services cluster</span></span>

<span data-ttu-id="cb861-118">If you specified more than one storage account when creating your ML Services cluster, the following instructions explain how to use a secondary account for data access and operations on an ML Services cluster.</span><span class="sxs-lookup"><span data-stu-id="cb861-118">If you specified more than one storage account when creating your ML Services cluster, the following instructions explain how to use a secondary account for data access and operations on an ML Services cluster.</span></span> <span data-ttu-id="cb861-119">Assume the following storage accounts and container: **storage1** and a default container called **container1**, and **storage2** with **container2**.</span><span class="sxs-lookup"><span data-stu-id="cb861-119">Assume the following storage accounts and container: **storage1** and a default container called **container1**, and **storage2** with **container2**.</span></span>

> [!WARNING]
> <span data-ttu-id="cb861-120">For performance purposes, the HDInsight cluster is created in the same data center as the primary storage account that you specify.</span><span class="sxs-lookup"><span data-stu-id="cb861-120">For performance purposes, the HDInsight cluster is created in the same data center as the primary storage account that you specify.</span></span> <span data-ttu-id="cb861-121">Using a storage account in a different location than the HDInsight cluster is not supported.</span><span class="sxs-lookup"><span data-stu-id="cb861-121">Using a storage account in a different location than the HDInsight cluster is not supported.</span></span>

### <a name="use-the-default-storage-with-ml-services-on-hdinsight"></a><span data-ttu-id="cb861-122">Use the default storage with ML Services on HDInsight</span><span class="sxs-lookup"><span data-stu-id="cb861-122">Use the default storage with ML Services on HDInsight</span></span>

1. <span data-ttu-id="cb861-123">Using an SSH client, connect to the edge node of your cluster.</span><span class="sxs-lookup"><span data-stu-id="cb861-123">Using an SSH client, connect to the edge node of your cluster.</span></span> <span data-ttu-id="cb861-124">For information on using SSH with HDInsight clusters, see [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="cb861-124">For information on using SSH with HDInsight clusters, see [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>
  
2. <span data-ttu-id="cb861-125">Copy a sample file, mysamplefile.csv, to the /share directory.</span><span class="sxs-lookup"><span data-stu-id="cb861-125">Copy a sample file, mysamplefile.csv, to the /share directory.</span></span> 

        hadoop fs –mkdir /share
        hadoop fs –copyFromLocal mycsv.scv /share  

3. <span data-ttu-id="cb861-126">Switch to R Studio or another R console, and write R code to set the name node to **default** and location of the file you want to access.</span><span class="sxs-lookup"><span data-stu-id="cb861-126">Switch to R Studio or another R console, and write R code to set the name node to **default** and location of the file you want to access.</span></span>  

        myNameNode <- "default"
        myPort <- 0

        #Location of the data:  
        bigDataDirRoot <- "/share"  

        #Define Spark compute context:
        mySparkCluster <- RxSpark(nameNode=myNameNode, consoleOutput=TRUE)

        #Set compute context:
        rxSetComputeContext(mySparkCluster)

        #Define the Hadoop Distributed File System (HDFS) file system:
        hdfsFS <- RxHdfsFileSystem(hostName=myNameNode, port=myPort)

        #Specify the input file to analyze in HDFS:
        inputFile <-file.path(bigDataDirRoot,"mysamplefile.csv")

<span data-ttu-id="cb861-127">All the directory and file references point to the storage account `wasb://container1@storage1.blob.core.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="cb861-127">All the directory and file references point to the storage account `wasb://container1@storage1.blob.core.windows.net`.</span></span> <span data-ttu-id="cb861-128">This is the **default storage account** that's associated with the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="cb861-128">This is the **default storage account** that's associated with the HDInsight cluster.</span></span>

### <a name="use-the-additional-storage-with-ml-services-on-hdinsight"></a><span data-ttu-id="cb861-129">Use the additional storage with ML Services on HDInsight</span><span class="sxs-lookup"><span data-stu-id="cb861-129">Use the additional storage with ML Services on HDInsight</span></span>

<span data-ttu-id="cb861-130">Now, suppose you want to process a file called mysamplefile1.csv that's located in the  /private directory of **container2** in **storage2**.</span><span class="sxs-lookup"><span data-stu-id="cb861-130">Now, suppose you want to process a file called mysamplefile1.csv that's located in the  /private directory of **container2** in **storage2**.</span></span>

<span data-ttu-id="cb861-131">In your R code, point the name node reference to the **storage2** storage account.</span><span class="sxs-lookup"><span data-stu-id="cb861-131">In your R code, point the name node reference to the **storage2** storage account.</span></span>

    myNameNode <- "wasb://container2@storage2.blob.core.windows.net"
    myPort <- 0

    #Location of the data:
    bigDataDirRoot <- "/private"

    #Define Spark compute context:
    mySparkCluster <- RxSpark(consoleOutput=TRUE, nameNode=myNameNode, port=myPort)

    #Set compute context:
    rxSetComputeContext(mySparkCluster)

    #Define HDFS file system:
    hdfsFS <- RxHdfsFileSystem(hostName=myNameNode, port=myPort)

    #Specify the input file to analyze in HDFS:
    inputFile <-file.path(bigDataDirRoot,"mysamplefile1.csv")

<span data-ttu-id="cb861-132">All of the directory and file references now point to the storage account `wasb://container2@storage2.blob.core.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="cb861-132">All of the directory and file references now point to the storage account `wasb://container2@storage2.blob.core.windows.net`.</span></span> <span data-ttu-id="cb861-133">This is the **Name Node** that you’ve specified.</span><span class="sxs-lookup"><span data-stu-id="cb861-133">This is the **Name Node** that you’ve specified.</span></span>

<span data-ttu-id="cb861-134">You have to configure the /user/RevoShare/<SSH username> directory on **storage2** as follows:</span><span class="sxs-lookup"><span data-stu-id="cb861-134">You have to configure the /user/RevoShare/<SSH username> directory on **storage2** as follows:</span></span>


    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user
    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user/RevoShare
    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user/RevoShare/<RDP username>

## <a name="use-an-azure-data-lake-store-with-ml-services-cluster"></a><span data-ttu-id="cb861-135">Use an Azure Data Lake Store with ML Services cluster</span><span class="sxs-lookup"><span data-stu-id="cb861-135">Use an Azure Data Lake Store with ML Services cluster</span></span> 

<span data-ttu-id="cb861-136">To use Data Lake Store with your HDInsight cluster, you need to give your cluster access to each Azure Data Lake Store that you want to use.</span><span class="sxs-lookup"><span data-stu-id="cb861-136">To use Data Lake Store with your HDInsight cluster, you need to give your cluster access to each Azure Data Lake Store that you want to use.</span></span> <span data-ttu-id="cb861-137">For instructions on how to use the Azure portal to create a HDInsight cluster with an Azure Data Lake Store account as the default storage or as an additional store, see [Create an HDInsight cluster with Data Lake Store using Azure portal](../../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="cb861-137">For instructions on how to use the Azure portal to create a HDInsight cluster with an Azure Data Lake Store account as the default storage or as an additional store, see [Create an HDInsight cluster with Data Lake Store using Azure portal](../../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

<span data-ttu-id="cb861-138">You then use the store in your R script much like you did a secondary Azure storage account as described in the previous procedure.</span><span class="sxs-lookup"><span data-stu-id="cb861-138">You then use the store in your R script much like you did a secondary Azure storage account as described in the previous procedure.</span></span>

### <a name="add-cluster-access-to-your-azure-data-lake-stores"></a><span data-ttu-id="cb861-139">Add cluster access to your Azure Data Lake Stores</span><span class="sxs-lookup"><span data-stu-id="cb861-139">Add cluster access to your Azure Data Lake Stores</span></span>
<span data-ttu-id="cb861-140">You access a Data Lake store by using an Azure Active Directory (Azure AD) Service Principal that's associated with your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="cb861-140">You access a Data Lake store by using an Azure Active Directory (Azure AD) Service Principal that's associated with your HDInsight cluster.</span></span>

1. <span data-ttu-id="cb861-141">When you create your HDInsight cluster, select **Cluster AAD Identity** from the **Data Source** tab.</span><span class="sxs-lookup"><span data-stu-id="cb861-141">When you create your HDInsight cluster, select **Cluster AAD Identity** from the **Data Source** tab.</span></span>

2. <span data-ttu-id="cb861-142">In the **Cluster AAD Identity** dialog box, under **Select AD Service Principal**, select **Create new**.</span><span class="sxs-lookup"><span data-stu-id="cb861-142">In the **Cluster AAD Identity** dialog box, under **Select AD Service Principal**, select **Create new**.</span></span>

<span data-ttu-id="cb861-143">After you give the Service Principal a name and create a password for it, click **Manage ADLS Access** to associate the Service Principal with your Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="cb861-143">After you give the Service Principal a name and create a password for it, click **Manage ADLS Access** to associate the Service Principal with your Data Lake Store.</span></span>

<span data-ttu-id="cb861-144">It’s also possible to add cluster access to one or more Data Lake Store accounts following cluster creation.</span><span class="sxs-lookup"><span data-stu-id="cb861-144">It’s also possible to add cluster access to one or more Data Lake Store accounts following cluster creation.</span></span> <span data-ttu-id="cb861-145">Open the Azure portal entry for a Data Lake Store and go to **Data Explorer > Access > Add**.</span><span class="sxs-lookup"><span data-stu-id="cb861-145">Open the Azure portal entry for a Data Lake Store and go to **Data Explorer > Access > Add**.</span></span> 

### <a name="how-to-access-the-data-lake-store-from-ml-services-on-hdinsight"></a><span data-ttu-id="cb861-146">How to access the Data Lake store from ML Services on HDInsight</span><span class="sxs-lookup"><span data-stu-id="cb861-146">How to access the Data Lake store from ML Services on HDInsight</span></span>

<span data-ttu-id="cb861-147">Once you’ve given access to a Data Lake Store, you can use the store in ML Services cluster on HDInsight the way you would a secondary Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="cb861-147">Once you’ve given access to a Data Lake Store, you can use the store in ML Services cluster on HDInsight the way you would a secondary Azure storage account.</span></span> <span data-ttu-id="cb861-148">The only difference is that the prefix **wasb://** changes to **adl://** as follows:</span><span class="sxs-lookup"><span data-stu-id="cb861-148">The only difference is that the prefix **wasb://** changes to **adl://** as follows:</span></span>


    # Point to the ADL store (e.g. ADLtest)
    myNameNode <- "adl://rkadl1.azuredatalakestore.net"
    myPort <- 0

    # Location of the data (assumes a /share directory on the ADL account)
    bigDataDirRoot <- "/share"  

    # Define Spark compute context
    mySparkCluster <- RxSpark(consoleOutput=TRUE, nameNode=myNameNode, port=myPort)

    # Set compute context
    rxSetComputeContext(mySparkCluster)

    # Define HDFS file system
    hdfsFS <- RxHdfsFileSystem(hostName=myNameNode, port=myPort)

    # Specify the input file in HDFS to analyze
    inputFile <-file.path(bigDataDirRoot,"mysamplefile.csv")

<span data-ttu-id="cb861-149">The following commands are used to configure the Data Lake Store account with the RevoShare directory and add the sample .csv file from the previous example:</span><span class="sxs-lookup"><span data-stu-id="cb861-149">The following commands are used to configure the Data Lake Store account with the RevoShare directory and add the sample .csv file from the previous example:</span></span>


    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user
    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user/RevoShare
    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user/RevoShare/<user>

    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/share

    hadoop fs -copyFromLocal /usr/lib64/R Server-7.4.1/library/RevoScaleR/SampleData/mysamplefile.csv adl://rkadl1.azuredatalakestore.net/share

    hadoop fs –ls adl://rkadl1.azuredatalakestore.net/share


## <a name="use-azure-file-storage-with-ml-services-on-hdinsight"></a><span data-ttu-id="cb861-150">Use Azure File storage with ML Services on HDInsight</span><span class="sxs-lookup"><span data-stu-id="cb861-150">Use Azure File storage with ML Services on HDInsight</span></span>

<span data-ttu-id="cb861-151">There is also a convenient data storage option for use on the edge node called [Azure Files]((https://azure.microsoft.com/services/storage/files/).</span><span class="sxs-lookup"><span data-stu-id="cb861-151">There is also a convenient data storage option for use on the edge node called [Azure Files]((https://azure.microsoft.com/services/storage/files/).</span></span> <span data-ttu-id="cb861-152">It enables you to mount an Azure Storage file share to the Linux file system.</span><span class="sxs-lookup"><span data-stu-id="cb861-152">It enables you to mount an Azure Storage file share to the Linux file system.</span></span> <span data-ttu-id="cb861-153">This option can be handy for storing data files, R scripts, and result objects that might be needed later, especially when it makes sense to use the native file system on the edge node rather than HDFS.</span><span class="sxs-lookup"><span data-stu-id="cb861-153">This option can be handy for storing data files, R scripts, and result objects that might be needed later, especially when it makes sense to use the native file system on the edge node rather than HDFS.</span></span> 

<span data-ttu-id="cb861-154">A major benefit of Azure Files is that the file shares can be mounted and used by any system that has a supported OS such as Windows or Linux.</span><span class="sxs-lookup"><span data-stu-id="cb861-154">A major benefit of Azure Files is that the file shares can be mounted and used by any system that has a supported OS such as Windows or Linux.</span></span> <span data-ttu-id="cb861-155">For example, it can be used by another HDInsight cluster that you or someone on your team has, by an Azure VM, or even by an on-premises system.</span><span class="sxs-lookup"><span data-stu-id="cb861-155">For example, it can be used by another HDInsight cluster that you or someone on your team has, by an Azure VM, or even by an on-premises system.</span></span> <span data-ttu-id="cb861-156">For more information, see:</span><span class="sxs-lookup"><span data-stu-id="cb861-156">For more information, see:</span></span>

- [<span data-ttu-id="cb861-157">How to use Azure File storage with Linux</span><span class="sxs-lookup"><span data-stu-id="cb861-157">How to use Azure File storage with Linux</span></span>](../../storage/files/storage-how-to-use-files-linux.md)
- [<span data-ttu-id="cb861-158">How to use Azure File storage on Windows</span><span class="sxs-lookup"><span data-stu-id="cb861-158">How to use Azure File storage on Windows</span></span>](../../storage/files/storage-dotnet-how-to-use-files.md)


## <a name="next-steps"></a><span data-ttu-id="cb861-159">Next steps</span><span class="sxs-lookup"><span data-stu-id="cb861-159">Next steps</span></span>

* [<span data-ttu-id="cb861-160">Overview of ML Services cluster on HDInsight</span><span class="sxs-lookup"><span data-stu-id="cb861-160">Overview of ML Services cluster on HDInsight</span></span>](r-server-overview.md)
* [<span data-ttu-id="cb861-161">Get started with ML Services cluster on Hadoop</span><span class="sxs-lookup"><span data-stu-id="cb861-161">Get started with ML Services cluster on Hadoop</span></span>](r-server-get-started.md)
* [<span data-ttu-id="cb861-162">Compute context options for ML Services cluster on HDInsight</span><span class="sxs-lookup"><span data-stu-id="cb861-162">Compute context options for ML Services cluster on HDInsight</span></span>](r-server-compute-contexts.md)

