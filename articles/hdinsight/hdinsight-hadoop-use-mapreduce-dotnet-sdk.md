---
title: Submit MapReduce jobs using HDInsight .NET SDK | Microsoft Docs
description: Learn how to submit MapReduce jobs to Azure HDInsight Hadoop using HDInsight .NET SDK.
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: ''
tags: azure-portal
author: mumian
ms.assetid: c85e44b0-85fd-4185-ad1c-c34a9fe5ef44
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/03/2017
ms.author: jgao
ms.openlocfilehash: a7d072232b3be4ae19876c90c477ca52d8eb063d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552902"
---
# <a name="run-mapreduce-jobs-using-hdinsight-net-sdk"></a><span data-ttu-id="e63ee-103">Run MapReduce jobs using HDInsight .NET SDK</span><span class="sxs-lookup"><span data-stu-id="e63ee-103">Run MapReduce jobs using HDInsight .NET SDK</span></span>
[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

<span data-ttu-id="e63ee-104">Learn how to submit MapReduce jobs using HDInsight .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="e63ee-104">Learn how to submit MapReduce jobs using HDInsight .NET SDK.</span></span> <span data-ttu-id="e63ee-105">HDInsight clusters come with a jar file with some MapReduce samples.</span><span class="sxs-lookup"><span data-stu-id="e63ee-105">HDInsight clusters come with a jar file with some MapReduce samples.</span></span> <span data-ttu-id="e63ee-106">The jar file is */example/jars/hadoop-mapreduce-examples.jar*.</span><span class="sxs-lookup"><span data-stu-id="e63ee-106">The jar file is */example/jars/hadoop-mapreduce-examples.jar*.</span></span>  <span data-ttu-id="e63ee-107">One of the samples is *wordcount*.</span><span class="sxs-lookup"><span data-stu-id="e63ee-107">One of the samples is *wordcount*.</span></span> <span data-ttu-id="e63ee-108">You develop a C# console application to submit a wordcount job.</span><span class="sxs-lookup"><span data-stu-id="e63ee-108">You develop a C# console application to submit a wordcount job.</span></span>  <span data-ttu-id="e63ee-109">The job reads the */example/data/gutenberg/davinci.txt* file, and outputs the results to */example/data/davinciwordcount*.</span><span class="sxs-lookup"><span data-stu-id="e63ee-109">The job reads the */example/data/gutenberg/davinci.txt* file, and outputs the results to */example/data/davinciwordcount*.</span></span>  <span data-ttu-id="e63ee-110">If you want to rerun the application, you must clean up the output folder.</span><span class="sxs-lookup"><span data-stu-id="e63ee-110">If you want to rerun the application, you must clean up the output folder.</span></span>

> [!NOTE]
> <span data-ttu-id="e63ee-111">The steps in this article must be performed from a Windows client.</span><span class="sxs-lookup"><span data-stu-id="e63ee-111">The steps in this article must be performed from a Windows client.</span></span> <span data-ttu-id="e63ee-112">For information on using a Linux, OS X, or Unix client to work with Hive, use the tab selector shown on the top of the article.</span><span class="sxs-lookup"><span data-stu-id="e63ee-112">For information on using a Linux, OS X, or Unix client to work with Hive, use the tab selector shown on the top of the article.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="e63ee-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e63ee-113">Prerequisites</span></span>
<span data-ttu-id="e63ee-114">Before you begin this article, you must have the following:</span><span class="sxs-lookup"><span data-stu-id="e63ee-114">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="e63ee-115">**A Hadoop cluster in HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="e63ee-115">**A Hadoop cluster in HDInsight**.</span></span> <span data-ttu-id="e63ee-116">See [Get started using Linux-based Hadoop in HDInsight](hdinsight-use-sqoop.md#create-cluster-and-sql-database).</span><span class="sxs-lookup"><span data-stu-id="e63ee-116">See [Get started using Linux-based Hadoop in HDInsight](hdinsight-use-sqoop.md#create-cluster-and-sql-database).</span></span>
* <span data-ttu-id="e63ee-117">**Visual Studio 2013/2015/2017**.</span><span class="sxs-lookup"><span data-stu-id="e63ee-117">**Visual Studio 2013/2015/2017**.</span></span>

## <a name="submit-mapreduce-jobs-using-hdinsight-net-sdk"></a><span data-ttu-id="e63ee-118">Submit MapReduce jobs using HDInsight .NET SDK</span><span class="sxs-lookup"><span data-stu-id="e63ee-118">Submit MapReduce jobs using HDInsight .NET SDK</span></span>
<span data-ttu-id="e63ee-119">The HDInsight .NET SDK provides .NET client libraries, which makes it easier to work with HDInsight clusters from .NET.</span><span class="sxs-lookup"><span data-stu-id="e63ee-119">The HDInsight .NET SDK provides .NET client libraries, which makes it easier to work with HDInsight clusters from .NET.</span></span> 

<span data-ttu-id="e63ee-120">**To Submit jobs**</span><span class="sxs-lookup"><span data-stu-id="e63ee-120">**To Submit jobs**</span></span>

1. <span data-ttu-id="e63ee-121">Create a C# console application in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e63ee-121">Create a C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="e63ee-122">From the Nuget Package Manager Console, run the following command.</span><span class="sxs-lookup"><span data-stu-id="e63ee-122">From the Nuget Package Manager Console, run the following command.</span></span>
   
        Install-Package Microsoft.Azure.Management.HDInsight.Job
3. <span data-ttu-id="e63ee-123">Use the following code:</span><span class="sxs-lookup"><span data-stu-id="e63ee-123">Use the following code:</span></span>
   
        using System.Collections.Generic;
        using System.IO;
        using System.Text;
        using System.Threading;
        using Microsoft.Azure.Management.HDInsight.Job;
        using Microsoft.Azure.Management.HDInsight.Job.Models;
        using Hyak.Common;
   
        namespace SubmitHDInsightJobDotNet
        {
            class Program
            {
                private static HDInsightJobManagementClient _hdiJobManagementClient;
   
                private const string ExistingClusterName = "<Your HDInsight Cluster Name>";
                private const string ExistingClusterUri = ExistingClusterName + ".azurehdinsight.net";
                private const string ExistingClusterUsername = "<Cluster Username>";
                private const string ExistingClusterPassword = "<Cluster User Password>";
   
                private const string DefaultStorageAccountName = "<Default Storage Account Name>"; //<StorageAccountName>.blob.core.windows.net
                private const string DefaultStorageAccountKey = "<Default Storage Account Key>";
                private const string DefaultStorageContainerName = "<Default Blob Container Name>";
   
                static void Main(string[] args)
                {
                    System.Console.WriteLine("The application is running ...");
   
                    var clusterCredentials = new BasicAuthenticationCloudCredentials { Username = ExistingClusterUsername, Password = ExistingClusterPassword };
                    _hdiJobManagementClient = new HDInsightJobManagementClient(ExistingClusterUri, clusterCredentials);
   
                    SubmitMRJob();
   
                    System.Console.WriteLine("Press ENTER to continue ...");
                    System.Console.ReadLine();
                }
   
                private static void SubmitMRJob()
                {
                    List<string> args = new List<string> { { "/example/data/gutenberg/davinci.txt" }, { "/example/data/davinciwordcount" } };
   
                    var paras = new MapReduceJobSubmissionParameters
                    {
                        JarFile = @"/example/jars/hadoop-mapreduce-examples.jar",
                        JarClass = "wordcount",
                        Arguments = args
                    };
   
                    System.Console.WriteLine("Submitting the MR job to the cluster...");
                    var jobResponse = _hdiJobManagementClient.JobManagement.SubmitMapReduceJob(paras);
                    var jobId = jobResponse.JobSubmissionJsonResponse.Id;
                    System.Console.WriteLine("Response status code is " + jobResponse.StatusCode);
                    System.Console.WriteLine("JobId is " + jobId);
   
                    System.Console.WriteLine("Waiting for the job completion ...");
   
                    // Wait for job completion
                    var jobDetail = _hdiJobManagementClient.JobManagement.GetJob(jobId).JobDetail;
                    while (!jobDetail.Status.JobComplete)
                    {
                        Thread.Sleep(1000);
                        jobDetail = _hdiJobManagementClient.JobManagement.GetJob(jobId).JobDetail;
                    }
   
                    // Get job output
                    var storageAccess = new AzureStorageAccess(DefaultStorageAccountName, DefaultStorageAccountKey,
                        DefaultStorageContainerName);
                    var output = (jobDetail.ExitValue == 0)
                        ? _hdiJobManagementClient.JobManagement.GetJobOutput(jobId, storageAccess) // fetch stdout output in case of success
                        : _hdiJobManagementClient.JobManagement.GetJobErrorLogs(jobId, storageAccess); // fetch stderr output in case of failure
   
                    System.Console.WriteLine("Job output is: ");
   
                    using (var reader = new StreamReader(output, Encoding.UTF8))
                    {
                        string value = reader.ReadToEnd();
                        System.Console.WriteLine(value);
                    }
                }
            }
        }
4. <span data-ttu-id="e63ee-124">Press **F5** to run the application.</span><span class="sxs-lookup"><span data-stu-id="e63ee-124">Press **F5** to run the application.</span></span>

<span data-ttu-id="e63ee-125">To run the job again, you must change the job output folder name, in the sample, it is "/example/data/davinciwordcount".</span><span class="sxs-lookup"><span data-stu-id="e63ee-125">To run the job again, you must change the job output folder name, in the sample, it is "/example/data/davinciwordcount".</span></span>

<span data-ttu-id="e63ee-126">When the job completes successfully, the output is blank.</span><span class="sxs-lookup"><span data-stu-id="e63ee-126">When the job completes successfully, the output is blank.</span></span> <span data-ttu-id="e63ee-127">To see the result of the MapReduce job, use the Azure portal to explore the default storage container in the Blob storage.</span><span class="sxs-lookup"><span data-stu-id="e63ee-127">To see the result of the MapReduce job, use the Azure portal to explore the default storage container in the Blob storage.</span></span>  <span data-ttu-id="e63ee-128">The file name is "part-r-00000".</span><span class="sxs-lookup"><span data-stu-id="e63ee-128">The file name is "part-r-00000".</span></span>

## <a name="next-steps"></a><span data-ttu-id="e63ee-129">Next steps</span><span class="sxs-lookup"><span data-stu-id="e63ee-129">Next steps</span></span>
<span data-ttu-id="e63ee-130">In this article, you have learned several ways to create an HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="e63ee-130">In this article, you have learned several ways to create an HDInsight cluster.</span></span> <span data-ttu-id="e63ee-131">To learn more, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="e63ee-131">To learn more, see the following articles:</span></span>

* <span data-ttu-id="e63ee-132">For submitting a Hive job, see [Run Hive queries using HDInsight .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="e63ee-132">For submitting a Hive job, see [Run Hive queries using HDInsight .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span></span>
* <span data-ttu-id="e63ee-133">For creating HDInsight clusters, see [Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="e63ee-133">For creating HDInsight clusters, see [Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>
* <span data-ttu-id="e63ee-134">For managing HDInsight clusters, see [Manage Hadoop clusters in HDInsight](hdinsight-administer-use-portal-linux.md).</span><span class="sxs-lookup"><span data-stu-id="e63ee-134">For managing HDInsight clusters, see [Manage Hadoop clusters in HDInsight](hdinsight-administer-use-portal-linux.md).</span></span>
* <span data-ttu-id="e63ee-135">For learning the HDInsight .NET SDK, see [HDInsight .NET SDK reference](https://msdn.microsoft.com/library/mt271028.aspx).</span><span class="sxs-lookup"><span data-stu-id="e63ee-135">For learning the HDInsight .NET SDK, see [HDInsight .NET SDK reference](https://msdn.microsoft.com/library/mt271028.aspx).</span></span>
* <span data-ttu-id="e63ee-136">For non-interactive authenticate to Azure, see [Create non-interactive authentication .NET HDInsight applications](hdinsight-create-non-interactive-authentication-dotnet-applications.md).</span><span class="sxs-lookup"><span data-stu-id="e63ee-136">For non-interactive authenticate to Azure, see [Create non-interactive authentication .NET HDInsight applications](hdinsight-create-non-interactive-authentication-dotnet-applications.md).</span></span>

