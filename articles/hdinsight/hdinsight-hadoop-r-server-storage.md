---
title: Azure Storage options for R Server on HDInsight | Microsoft Docs
description: Learn about the different storage options available to users with R Server on HDInsight
services: HDInsight
documentationcenter: ''
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 1cf30096-d3ca-45ea-b526-aa3954402f66
ms.service: HDInsight
ms.custom: hdinsightactive
ms.devlang: R
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 02/28/2017
ms.author: jeffstok
ms.openlocfilehash: 18dcb3a319f78639b27f9e70a2177423192e5958
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660770"
---
# <a name="azure-storage-options-for-r-server-on-hdinsight"></a><span data-ttu-id="c4eb8-103">Azure Storage options for R Server on HDInsight</span><span class="sxs-lookup"><span data-stu-id="c4eb8-103">Azure Storage options for R Server on HDInsight</span></span>
<span data-ttu-id="c4eb8-104">Microsoft R Server on HDInsight has access to both Azure Blob and [Azure Data Lake Storage](https://azure.microsoft.com/services/data-lake-store/), as a means of persisting data, code, result objects from analysis, and so on.</span><span class="sxs-lookup"><span data-stu-id="c4eb8-104">Microsoft R Server on HDInsight has access to both Azure Blob and [Azure Data Lake Storage](https://azure.microsoft.com/services/data-lake-store/), as a means of persisting data, code, result objects from analysis, and so on.</span></span>

<span data-ttu-id="c4eb8-105">When you create a Hadoop cluster in HDInsight, you specify either an Azure Storage account or a Data Lake store.</span><span class="sxs-lookup"><span data-stu-id="c4eb8-105">When you create a Hadoop cluster in HDInsight, you specify either an Azure Storage account or a Data Lake store.</span></span> <span data-ttu-id="c4eb8-106">A specific storage container from that account holds the file system for the cluster you create (for example, the Hadoop Distributed File System).</span><span class="sxs-lookup"><span data-stu-id="c4eb8-106">A specific storage container from that account holds the file system for the cluster you create (for example, the Hadoop Distributed File System).</span></span> <span data-ttu-id="c4eb8-107">For performance purposes, the HDInsight cluster is created in the same data center as the primary storage account that you specify.</span><span class="sxs-lookup"><span data-stu-id="c4eb8-107">For performance purposes, the HDInsight cluster is created in the same data center as the primary storage account that you specify.</span></span> <span data-ttu-id="c4eb8-108">For more information, see [Use Azure Blob storage with HDInsight](hdinsight-hadoop-use-blob-storage.md "Use Azure Blob storage with HDInsight").</span><span class="sxs-lookup"><span data-stu-id="c4eb8-108">For more information, see [Use Azure Blob storage with HDInsight](hdinsight-hadoop-use-blob-storage.md "Use Azure Blob storage with HDInsight").</span></span>   

## <a name="use-multiple-azure-blob-storage-accounts"></a><span data-ttu-id="c4eb8-109">Use multiple Azure Blob storage accounts</span><span class="sxs-lookup"><span data-stu-id="c4eb8-109">Use multiple Azure Blob storage accounts</span></span>
<span data-ttu-id="c4eb8-110">If necessary, you can access multiple Azure storage accounts or containers with your HDI cluster.</span><span class="sxs-lookup"><span data-stu-id="c4eb8-110">If necessary, you can access multiple Azure storage accounts or containers with your HDI cluster.</span></span> <span data-ttu-id="c4eb8-111">To do so, you need to specify the additional storage accounts in the UI when you create the cluster, and then follow these steps to use them in R.</span><span class="sxs-lookup"><span data-stu-id="c4eb8-111">To do so, you need to specify the additional storage accounts in the UI when you create the cluster, and then follow these steps to use them in R.</span></span>

> [!WARNING]
> <span data-ttu-id="c4eb8-112">Using a storage account in a different location than the HDInsight cluster is not supported.</span><span class="sxs-lookup"><span data-stu-id="c4eb8-112">Using a storage account in a different location than the HDInsight cluster is not supported.</span></span>

1. <span data-ttu-id="c4eb8-113">Create an HDInsight cluster with a storage account name of **storage1** and a default container called **container1**.</span><span class="sxs-lookup"><span data-stu-id="c4eb8-113">Create an HDInsight cluster with a storage account name of **storage1** and a default container called **container1**.</span></span>
2. <span data-ttu-id="c4eb8-114">Specify an additional storage account called **storage2**.</span><span class="sxs-lookup"><span data-stu-id="c4eb8-114">Specify an additional storage account called **storage2**.</span></span>  
3. <span data-ttu-id="c4eb8-115">Copy the mycsv.csv file to the /share directory, and perform analysis on that file.</span><span class="sxs-lookup"><span data-stu-id="c4eb8-115">Copy the mycsv.csv file to the /share directory, and perform analysis on that file.</span></span>  

        hadoop fs –mkdir /share
        hadoop fs –copyFromLocal myscsv.scv /share  

4. <span data-ttu-id="c4eb8-116">In R code, set the name node to **default,** and set your directory and file to process.</span><span class="sxs-lookup"><span data-stu-id="c4eb8-116">In R code, set the name node to **default,** and set your directory and file to process.</span></span>  

        myNameNode <- "default"
        myPort <- 0

    <span data-ttu-id="c4eb8-117">Location of the data:</span><span class="sxs-lookup"><span data-stu-id="c4eb8-117">Location of the data:</span></span>  

        bigDataDirRoot <- "/share"  

    <span data-ttu-id="c4eb8-118">Define Spark compute context:</span><span class="sxs-lookup"><span data-stu-id="c4eb8-118">Define Spark compute context:</span></span>

        mySparkCluster <- RxSpark(consoleOutput=TRUE)

    <span data-ttu-id="c4eb8-119">Set compute context:</span><span class="sxs-lookup"><span data-stu-id="c4eb8-119">Set compute context:</span></span>

        rxSetComputeContext(mySparkCluster)

    <span data-ttu-id="c4eb8-120">Define the Hadoop Distributed File System (HDFS) file system:</span><span class="sxs-lookup"><span data-stu-id="c4eb8-120">Define the Hadoop Distributed File System (HDFS) file system:</span></span>

        hdfsFS <- RxHdfsFileSystem(hostName=myNameNode, port=myPort)

    <span data-ttu-id="c4eb8-121">Specify the input file to analyze in HDFS:</span><span class="sxs-lookup"><span data-stu-id="c4eb8-121">Specify the input file to analyze in HDFS:</span></span>

        inputFile <-file.path(bigDataDirRoot,"mycsv.csv")

<span data-ttu-id="c4eb8-122">All of the directory and file references point to the storage account wasbs://container1@storage1.blob.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="c4eb8-122">All of the directory and file references point to the storage account wasbs://container1@storage1.blob.core.windows.net.</span></span> <span data-ttu-id="c4eb8-123">This is the **default storage account** that's associated with the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="c4eb8-123">This is the **default storage account** that's associated with the HDInsight cluster.</span></span>

<span data-ttu-id="c4eb8-124">Now, suppose you want to process a file called mySpecial.csv that's located in the  /private directory of **container2** in **storage2**.</span><span class="sxs-lookup"><span data-stu-id="c4eb8-124">Now, suppose you want to process a file called mySpecial.csv that's located in the  /private directory of **container2** in **storage2**.</span></span>

<span data-ttu-id="c4eb8-125">In your R code, point the name node reference to the **storage2** storage account.</span><span class="sxs-lookup"><span data-stu-id="c4eb8-125">In your R code, point the name node reference to the **storage2** storage account.</span></span>

````
myNameNode <- "wasbs://container2@storage2.blob.core.windows.net"
myPort <- 0
````

<span data-ttu-id="c4eb8-126">Location of the data:</span><span class="sxs-lookup"><span data-stu-id="c4eb8-126">Location of the data:</span></span>

````
bigDataDirRoot <- "/private"
````

<span data-ttu-id="c4eb8-127">Define Spark compute context:</span><span class="sxs-lookup"><span data-stu-id="c4eb8-127">Define Spark compute context:</span></span>

````
mySparkCluster <- RxSpark(consoleOutput=TRUE, nameNode=myNameNode, port=myPort)
````

<span data-ttu-id="c4eb8-128">Set compute context:</span><span class="sxs-lookup"><span data-stu-id="c4eb8-128">Set compute context:</span></span>

````
rxSetComputeContext(mySparkCluster)
````

<span data-ttu-id="c4eb8-129">Define HDFS file system:</span><span class="sxs-lookup"><span data-stu-id="c4eb8-129">Define HDFS file system:</span></span>

````
hdfsFS <- RxHdfsFileSystem(hostName=myNameNode, port=myPort)
````

<span data-ttu-id="c4eb8-130">Specify the input file to analyze in HDFS:</span><span class="sxs-lookup"><span data-stu-id="c4eb8-130">Specify the input file to analyze in HDFS:</span></span>

````
inputFile <-file.path(bigDataDirRoot,"mySpecial.csv")
````

<span data-ttu-id="c4eb8-131">All of the directory and file references now point to the storage account wasbs://container2@storage2.blob.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="c4eb8-131">All of the directory and file references now point to the storage account wasbs://container2@storage2.blob.core.windows.net.</span></span> <span data-ttu-id="c4eb8-132">This is the **Name Node** that you’ve specified.</span><span class="sxs-lookup"><span data-stu-id="c4eb8-132">This is the **Name Node** that you’ve specified.</span></span>

<span data-ttu-id="c4eb8-133">Note that you will have to configure the /user/RevoShare/<SSH username> directory on **storage2** as follows:</span><span class="sxs-lookup"><span data-stu-id="c4eb8-133">Note that you will have to configure the /user/RevoShare/<SSH username> directory on **storage2** as follows:</span></span>

````
hadoop fs -mkdir wasbs://container2@storage2.blob.core.windows.net/user
hadoop fs -mkdir wasbs://container2@storage2.blob.core.windows.net/user/RevoShare
hadoop fs -mkdir wasbs://container2@storage2.blob.core.windows.net/user/RevoShare/<RDP username>
````

## <a name="use-an-azure-data-lake-store"></a><span data-ttu-id="c4eb8-134">Use an Azure Data Lake store</span><span class="sxs-lookup"><span data-stu-id="c4eb8-134">Use an Azure Data Lake store</span></span>
<span data-ttu-id="c4eb8-135">To use Data Lake stores with your HDInsight account, you need to give your cluster access to each Azure Data Lake store that you want to use.</span><span class="sxs-lookup"><span data-stu-id="c4eb8-135">To use Data Lake stores with your HDInsight account, you need to give your cluster access to each Azure Data Lake store that you want to use.</span></span> <span data-ttu-id="c4eb8-136">You use the store in your R script much like you use a secondary storage account (as described in the previous procedure).</span><span class="sxs-lookup"><span data-stu-id="c4eb8-136">You use the store in your R script much like you use a secondary storage account (as described in the previous procedure).</span></span>

## <a name="add-cluster-access-to-your-azure-data-lake-stores"></a><span data-ttu-id="c4eb8-137">Add cluster access to your Azure Data Lake stores</span><span class="sxs-lookup"><span data-stu-id="c4eb8-137">Add cluster access to your Azure Data Lake stores</span></span>
<span data-ttu-id="c4eb8-138">You access a Data Lake store by using an Azure Active Directory (Azure AD) Service Principal that's associated with your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="c4eb8-138">You access a Data Lake store by using an Azure Active Directory (Azure AD) Service Principal that's associated with your HDInsight cluster.</span></span>

### <a name="to-add-a-service-principal"></a><span data-ttu-id="c4eb8-139">To add a Service Principal</span><span class="sxs-lookup"><span data-stu-id="c4eb8-139">To add a Service Principal</span></span>
<span data-ttu-id="c4eb8-140">1.When you create your HDInsight cluster, select **Cluster AAD Identity** from the **Data Source** tab.</span><span class="sxs-lookup"><span data-stu-id="c4eb8-140">1.When you create your HDInsight cluster, select **Cluster AAD Identity** from the **Data Source** tab.</span></span>

<span data-ttu-id="c4eb8-141">2.In the **Cluster AAD Identity** dialog box, under **Select AD Service Principal**, select **Create new**.</span><span class="sxs-lookup"><span data-stu-id="c4eb8-141">2.In the **Cluster AAD Identity** dialog box, under **Select AD Service Principal**, select **Create new**.</span></span>

<span data-ttu-id="c4eb8-142">After you give the Service Principal a name and create a password for it, click on **Manage ADLS Access** to associate the Service Principal with your Data Lake stores.</span><span class="sxs-lookup"><span data-stu-id="c4eb8-142">After you give the Service Principal a name and create a password for it, click on **Manage ADLS Access** to associate the Service Principal with your Data Lake stores.</span></span>

<span data-ttu-id="c4eb8-143">It’s also possible to add cluster access to one or more Data Lake stores following cluster creation by opening the Azure Portal entry for a Data Lake store and going to **Data Explorer > Access > Add**.</span><span class="sxs-lookup"><span data-stu-id="c4eb8-143">It’s also possible to add cluster access to one or more Data Lake stores following cluster creation by opening the Azure Portal entry for a Data Lake store and going to **Data Explorer > Access > Add**.</span></span> 

<span data-ttu-id="c4eb8-144">For additional detail on adding HDI cluster access to Data Lake stores see the article [Create an HDInsight cluster with Data Lake Store using Azure Portal](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-hdinsight-hadoop-use-portal#create-an-hdinsight-cluster-with-access-to-azure-data-lake-store)</span><span class="sxs-lookup"><span data-stu-id="c4eb8-144">For additional detail on adding HDI cluster access to Data Lake stores see the article [Create an HDInsight cluster with Data Lake Store using Azure Portal](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-hdinsight-hadoop-use-portal#create-an-hdinsight-cluster-with-access-to-azure-data-lake-store)</span></span>

## <a name="use-the-data-lake-store-with-r-server"></a><span data-ttu-id="c4eb8-145">Use the Data Lake store with R Server</span><span class="sxs-lookup"><span data-stu-id="c4eb8-145">Use the Data Lake store with R Server</span></span>
<span data-ttu-id="c4eb8-146">Once you’ve given access to a Data Lake store, you can use the store in R Server on HDInsight the way you would a secondary Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="c4eb8-146">Once you’ve given access to a Data Lake store, you can use the store in R Server on HDInsight the way you would a secondary Azure storage account.</span></span> <span data-ttu-id="c4eb8-147">The only difference is that the prefix **wasb://** changes to **adl://** as follows:</span><span class="sxs-lookup"><span data-stu-id="c4eb8-147">The only difference is that the prefix **wasb://** changes to **adl://** as follows:</span></span>

````
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
inputFile <-file.path(bigDataDirRoot,"AirlineDemoSmall.csv")

# Create factors for days of the week
colInfo <- list(DayOfWeek = list(type = "factor",
               levels = c("Monday", "Tuesday", "Wednesday", "Thursday",
                          "Friday", "Saturday", "Sunday")))

# Define the data source
airDS <- RxTextData(file = inputFile, missingValueString = "M",
                    colInfo  = colInfo, fileSystem = hdfsFS)

# Run a linear regression
model <- rxLinMod(ArrDelay~CRSDepTime+DayOfWeek, data = airDS)
````

<span data-ttu-id="c4eb8-148">Following are the commands that are used to configure the Data Lake storage account with the RevoShare directory and add the sample .csv file from the previous example:</span><span class="sxs-lookup"><span data-stu-id="c4eb8-148">Following are the commands that are used to configure the Data Lake storage account with the RevoShare directory and add the sample .csv file from the previous example:</span></span>

````
hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user
hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user/RevoShare
hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user/RevoShare/<user>

hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/share

hadoop fs -copyFromLocal /usr/lib64/R Server-7.4.1/library/RevoScaleR/SampleData/AirlineDemoSmall.csv adl://rkadl1.azuredatalakestore.net/share

hadoop fs –ls adl://rkadl1.azuredatalakestore.net/share
````

## <a name="use-azure-files-on-the-edge-node"></a><span data-ttu-id="c4eb8-149">Use Azure Files on the edge node</span><span class="sxs-lookup"><span data-stu-id="c4eb8-149">Use Azure Files on the edge node</span></span>
<span data-ttu-id="c4eb8-150">There is also a convenient data storage option for use on the edge node called [Azure Files](../storage/storage-how-to-use-files-linux.md "Azure Files").</span><span class="sxs-lookup"><span data-stu-id="c4eb8-150">There is also a convenient data storage option for use on the edge node called [Azure Files](../storage/storage-how-to-use-files-linux.md "Azure Files").</span></span> <span data-ttu-id="c4eb8-151">It enables you to mount an Azure Storage file share to the Linux file system.</span><span class="sxs-lookup"><span data-stu-id="c4eb8-151">It enables you to mount an Azure Storage file share to the Linux file system.</span></span> <span data-ttu-id="c4eb8-152">This can be handy for storing data files, R scripts, and result objects that might be needed later when it makes sense to use the native file system on the edge node rather than HDFS.</span><span class="sxs-lookup"><span data-stu-id="c4eb8-152">This can be handy for storing data files, R scripts, and result objects that might be needed later when it makes sense to use the native file system on the edge node rather than HDFS.</span></span>

<span data-ttu-id="c4eb8-153">A major benefit of Azure Files is that the file shares can be mounted and used by any system that has a supported OS such as Windows or Linux.</span><span class="sxs-lookup"><span data-stu-id="c4eb8-153">A major benefit of Azure Files is that the file shares can be mounted and used by any system that has a supported OS such as Windows or Linux.</span></span> <span data-ttu-id="c4eb8-154">For example, it can be used by another HDInsight cluster that you or someone on your team has, by an Azure VM, or even by an on-premises system.</span><span class="sxs-lookup"><span data-stu-id="c4eb8-154">For example, it can be used by another HDInsight cluster that you or someone on your team has, by an Azure VM, or even by an on-premises system.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c4eb8-155">Next steps</span><span class="sxs-lookup"><span data-stu-id="c4eb8-155">Next steps</span></span>
<span data-ttu-id="c4eb8-156">Now that you understand the Azure storage options, use the following links to discover other ways of working with R Server on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c4eb8-156">Now that you understand the Azure storage options, use the following links to discover other ways of working with R Server on HDInsight.</span></span>

* [<span data-ttu-id="c4eb8-157">Overview of R Server on HDInsight</span><span class="sxs-lookup"><span data-stu-id="c4eb8-157">Overview of R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-overview.md)
* [<span data-ttu-id="c4eb8-158">Get started with R server on Hadoop</span><span class="sxs-lookup"><span data-stu-id="c4eb8-158">Get started with R server on Hadoop</span></span>](hdinsight-hadoop-r-server-get-started.md)
* [<span data-ttu-id="c4eb8-159">Add RStudio Server to HDInsight (if not added during cluster creation)</span><span class="sxs-lookup"><span data-stu-id="c4eb8-159">Add RStudio Server to HDInsight (if not added during cluster creation)</span></span>](hdinsight-hadoop-r-server-install-r-studio.md)
* [<span data-ttu-id="c4eb8-160">Compute context options for R Server on HDInsight</span><span class="sxs-lookup"><span data-stu-id="c4eb8-160">Compute context options for R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-compute-contexts.md)

