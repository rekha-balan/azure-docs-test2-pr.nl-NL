---
title: Submit MapReduce jobs using HDInsight .NET SDK - Azure
description: Learn how to submit MapReduce jobs to Azure HDInsight Hadoop using HDInsight .NET SDK.
ms.reviewer: jasonh
services: hdinsight
author: jasonwhowell
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 05/16/2018
ms.author: jasonh
ms.openlocfilehash: b2a79b73015419dc48a1a731e01ac9c8e1fc27f8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856154"
---
# <a name="run-mapreduce-jobs-using-hdinsight-net-sdk"></a><span data-ttu-id="4ba3f-103">Run MapReduce jobs using HDInsight .NET SDK</span><span class="sxs-lookup"><span data-stu-id="4ba3f-103">Run MapReduce jobs using HDInsight .NET SDK</span></span>
[!INCLUDE [mapreduce-selector](../../../includes/hdinsight-selector-use-mapreduce.md)]

<span data-ttu-id="4ba3f-104">Learn how to submit MapReduce jobs using HDInsight .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="4ba3f-104">Learn how to submit MapReduce jobs using HDInsight .NET SDK.</span></span> <span data-ttu-id="4ba3f-105">HDInsight clusters come with a jar file with some MapReduce samples.</span><span class="sxs-lookup"><span data-stu-id="4ba3f-105">HDInsight clusters come with a jar file with some MapReduce samples.</span></span> <span data-ttu-id="4ba3f-106">The jar file is */example/jars/hadoop-mapreduce-examples.jar*.</span><span class="sxs-lookup"><span data-stu-id="4ba3f-106">The jar file is */example/jars/hadoop-mapreduce-examples.jar*.</span></span>  <span data-ttu-id="4ba3f-107">One of the samples is *wordcount*.</span><span class="sxs-lookup"><span data-stu-id="4ba3f-107">One of the samples is *wordcount*.</span></span> <span data-ttu-id="4ba3f-108">You develop a C# console application to submit a wordcount job.</span><span class="sxs-lookup"><span data-stu-id="4ba3f-108">You develop a C# console application to submit a wordcount job.</span></span>  <span data-ttu-id="4ba3f-109">The job reads the */example/data/gutenberg/davinci.txt* file, and outputs the results to */example/data/davinciwordcount*.</span><span class="sxs-lookup"><span data-stu-id="4ba3f-109">The job reads the */example/data/gutenberg/davinci.txt* file, and outputs the results to */example/data/davinciwordcount*.</span></span>  <span data-ttu-id="4ba3f-110">If you want to rerun the application, you must clean up the output folder.</span><span class="sxs-lookup"><span data-stu-id="4ba3f-110">If you want to rerun the application, you must clean up the output folder.</span></span>

> [!NOTE]
> <span data-ttu-id="4ba3f-111">The steps in this article must be performed from a Windows client.</span><span class="sxs-lookup"><span data-stu-id="4ba3f-111">The steps in this article must be performed from a Windows client.</span></span> <span data-ttu-id="4ba3f-112">For information on using a Linux, OS X, or Unix client to work with Hive, use the tab selector shown on the top of the article.</span><span class="sxs-lookup"><span data-stu-id="4ba3f-112">For information on using a Linux, OS X, or Unix client to work with Hive, use the tab selector shown on the top of the article.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="4ba3f-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="4ba3f-113">Prerequisites</span></span>
<span data-ttu-id="4ba3f-114">Before you begin this article, you must have the following items:</span><span class="sxs-lookup"><span data-stu-id="4ba3f-114">Before you begin this article, you must have the following items:</span></span>

* <span data-ttu-id="4ba3f-115">**A Hadoop cluster in HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="4ba3f-115">**A Hadoop cluster in HDInsight**.</span></span> <span data-ttu-id="4ba3f-116">See [Get started using Linux-based Hadoop in HDInsight](apache-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="4ba3f-116">See [Get started using Linux-based Hadoop in HDInsight](apache-hadoop-linux-tutorial-get-started.md).</span></span>
* <span data-ttu-id="4ba3f-117">**Visual Studio 2013/2015/2017**.</span><span class="sxs-lookup"><span data-stu-id="4ba3f-117">**Visual Studio 2013/2015/2017**.</span></span>

## <a name="submit-mapreduce-jobs-using-hdinsight-net-sdk"></a><span data-ttu-id="4ba3f-118">Submit MapReduce jobs using HDInsight .NET SDK</span><span class="sxs-lookup"><span data-stu-id="4ba3f-118">Submit MapReduce jobs using HDInsight .NET SDK</span></span>
<span data-ttu-id="4ba3f-119">The HDInsight .NET SDK provides .NET client libraries, which makes it easier to work with HDInsight clusters from .NET.</span><span class="sxs-lookup"><span data-stu-id="4ba3f-119">The HDInsight .NET SDK provides .NET client libraries, which makes it easier to work with HDInsight clusters from .NET.</span></span> 

<span data-ttu-id="4ba3f-120">**To Submit jobs**</span><span class="sxs-lookup"><span data-stu-id="4ba3f-120">**To Submit jobs**</span></span>

1. <span data-ttu-id="4ba3f-121">Create a C# console application in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4ba3f-121">Create a C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="4ba3f-122">From the NuGet Package Manager Console, run the following command:</span><span class="sxs-lookup"><span data-stu-id="4ba3f-122">From the NuGet Package Manager Console, run the following command:</span></span>

    ```   
    Install-Package Microsoft.Azure.Management.HDInsight.Job
    ```
3. <span data-ttu-id="4ba3f-123">Use the following code:</span><span class="sxs-lookup"><span data-stu-id="4ba3f-123">Use the following code:</span></span>

    ```csharp
    using System.Collections.Generic;
    using System.IO;
    using System.Text;
    using System.Threading;
    using Microsoft.Azure.Management.HDInsight.Job;
    using Microsoft.Azure.Management.HDInsight.Job.Models;
    using Hyak.Common;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;

    namespace SubmitHDInsightJobDotNet
    {
        class Program
        {
            private static HDInsightJobManagementClient _hdiJobManagementClient;

            private const string existingClusterName = "<Your HDInsight Cluster Name>";
            private const string existingClusterUri = existingClusterName + ".azurehdinsight.net";
            private const string existingClusterUsername = "<Cluster Username>";
            private const string existingClusterPassword = "<Cluster User Password>";

            private const string defaultStorageAccountName = "<Default Storage Account Name>"; //<StorageAccountName>.blob.core.windows.net
            private const string defaultStorageAccountKey = "<Default Storage Account Key>";
            private const string defaultStorageContainerName = "<Default Blob Container Name>";

            private const string sourceFile = "/example/data/gutenberg/davinci.txt";  
            private const string outputFolder = "/example/data/davinciwordcount";

            static void Main(string[] args)
            {
                System.Console.WriteLine("The application is running ...");

                var clusterCredentials = new BasicAuthenticationCloudCredentials { Username = existingClusterUsername, Password = existingClusterPassword };
                _hdiJobManagementClient = new HDInsightJobManagementClient(existingClusterUri, clusterCredentials);

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
                System.Console.WriteLine("Job output is: ");
                var storageAccess = new AzureStorageAccess(defaultStorageAccountName, defaultStorageAccountKey,
                    defaultStorageContainerName);
    
                if (jobDetail.ExitValue == 0)
                {
                    // Create the storage account object
                    CloudStorageAccount storageAccount = CloudStorageAccount.Parse("DefaultEndpointsProtocol=https;AccountName=" + 
                        defaultStorageAccountName + 
                        ";AccountKey=" + defaultStorageAccountKey);
    
                    // Create the blob client.
                    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    
                    // Retrieve reference to a previously created container.
                    CloudBlobContainer container = blobClient.GetContainerReference(defaultStorageContainerName);
    
                    CloudBlockBlob blockBlob = container.GetBlockBlobReference(outputFolder.Substring(1) + "/part-r-00000");
    
                    using (var stream = blockBlob.OpenRead())
                    {
                        using (StreamReader reader = new StreamReader(stream))
                        {
                            while (!reader.EndOfStream)
                            {
                                System.Console.WriteLine(reader.ReadLine());
                            }
                        }
                    }
                }
                else
                {
                    // fetch stderr output in case of failure
                    var output = _hdiJobManagementClient.JobManagement.GetJobErrorLogs(jobId, storageAccess); 
    
                    using (var reader = new StreamReader(output, Encoding.UTF8))
                    {
                        string value = reader.ReadToEnd();
                        System.Console.WriteLine(value);
                    }
    
                }
            }
        }
    }
    ```

4. <span data-ttu-id="4ba3f-124">Press **F5** to run the application.</span><span class="sxs-lookup"><span data-stu-id="4ba3f-124">Press **F5** to run the application.</span></span>

<span data-ttu-id="4ba3f-125">To run the job again, you must change the job output folder name, in the sample, it is "/example/data/davinciwordcount".</span><span class="sxs-lookup"><span data-stu-id="4ba3f-125">To run the job again, you must change the job output folder name, in the sample, it is "/example/data/davinciwordcount".</span></span>

<span data-ttu-id="4ba3f-126">When the job completes successfully, the application prints the content of the output file "part-r-00000".</span><span class="sxs-lookup"><span data-stu-id="4ba3f-126">When the job completes successfully, the application prints the content of the output file "part-r-00000".</span></span>

## <a name="next-steps"></a><span data-ttu-id="4ba3f-127">Next steps</span><span class="sxs-lookup"><span data-stu-id="4ba3f-127">Next steps</span></span>
<span data-ttu-id="4ba3f-128">In this article, you have learned several ways to create an HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="4ba3f-128">In this article, you have learned several ways to create an HDInsight cluster.</span></span> <span data-ttu-id="4ba3f-129">To learn more, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="4ba3f-129">To learn more, see the following articles:</span></span>

* <span data-ttu-id="4ba3f-130">For submitting a Hive job, see [Run Hive queries using HDInsight .NET SDK](apache-hadoop-use-hive-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="4ba3f-130">For submitting a Hive job, see [Run Hive queries using HDInsight .NET SDK](apache-hadoop-use-hive-dotnet-sdk.md).</span></span>
* <span data-ttu-id="4ba3f-131">For creating HDInsight clusters, see [Create Linux-based Hadoop clusters in HDInsight](../hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="4ba3f-131">For creating HDInsight clusters, see [Create Linux-based Hadoop clusters in HDInsight](../hdinsight-hadoop-provision-linux-clusters.md).</span></span>
* <span data-ttu-id="4ba3f-132">For managing HDInsight clusters, see [Manage Hadoop clusters in HDInsight](../hdinsight-administer-use-portal-linux.md).</span><span class="sxs-lookup"><span data-stu-id="4ba3f-132">For managing HDInsight clusters, see [Manage Hadoop clusters in HDInsight](../hdinsight-administer-use-portal-linux.md).</span></span>
* <span data-ttu-id="4ba3f-133">For learning the HDInsight .NET SDK, see [HDInsight .NET SDK reference](https://docs.microsoft.com/dotnet/api/overview/azure/hdinsight).</span><span class="sxs-lookup"><span data-stu-id="4ba3f-133">For learning the HDInsight .NET SDK, see [HDInsight .NET SDK reference](https://docs.microsoft.com/dotnet/api/overview/azure/hdinsight).</span></span>
* <span data-ttu-id="4ba3f-134">For non-interactive authenticate to Azure, see [Create non-interactive authentication .NET HDInsight applications](../hdinsight-create-non-interactive-authentication-dotnet-applications.md).</span><span class="sxs-lookup"><span data-stu-id="4ba3f-134">For non-interactive authenticate to Azure, see [Create non-interactive authentication .NET HDInsight applications](../hdinsight-create-non-interactive-authentication-dotnet-applications.md).</span></span>

