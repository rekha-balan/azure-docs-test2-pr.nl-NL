---
title: Run Hive queries using HDInsight .NET SDK - Azure
description: Learn how to submit Hadoop jobs to Azure HDInsight Hadoop using HDInsight .NET SDK.
ms.reviewer: jasonh
services: hdinsight
author: jasonwhowell
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 05/16/2018
ms.author: jasonh
ms.openlocfilehash: ac02e67791cde4d67f126da46c86896fb80ee1b9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866569"
---
# <a name="run-hive-queries-using-hdinsight-net-sdk"></a><span data-ttu-id="b589c-103">Run Hive queries using HDInsight .NET SDK</span><span class="sxs-lookup"><span data-stu-id="b589c-103">Run Hive queries using HDInsight .NET SDK</span></span>
[!INCLUDE [hive-selector](../../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="b589c-104">Learn how to submit Hive queries using HDInsight .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="b589c-104">Learn how to submit Hive queries using HDInsight .NET SDK.</span></span> <span data-ttu-id="b589c-105">You write a C# program to submit a Hive query for listing Hive tables, and display the results.</span><span class="sxs-lookup"><span data-stu-id="b589c-105">You write a C# program to submit a Hive query for listing Hive tables, and display the results.</span></span>

> [!NOTE]
> <span data-ttu-id="b589c-106">The steps in this article must be performed from a Windows client.</span><span class="sxs-lookup"><span data-stu-id="b589c-106">The steps in this article must be performed from a Windows client.</span></span> <span data-ttu-id="b589c-107">For information on using a Linux, OS X, or Unix client to work with Hive, use the tab selector shown on the top of the article.</span><span class="sxs-lookup"><span data-stu-id="b589c-107">For information on using a Linux, OS X, or Unix client to work with Hive, use the tab selector shown on the top of the article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b589c-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b589c-108">Prerequisites</span></span>
<span data-ttu-id="b589c-109">Before you begin this article, you must have the following items:</span><span class="sxs-lookup"><span data-stu-id="b589c-109">Before you begin this article, you must have the following items:</span></span>

* <span data-ttu-id="b589c-110">**A Hadoop cluster in HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="b589c-110">**A Hadoop cluster in HDInsight**.</span></span> <span data-ttu-id="b589c-111">See [Get started using Linux-based Hadoop in HDInsight](apache-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="b589c-111">See [Get started using Linux-based Hadoop in HDInsight](apache-hadoop-linux-tutorial-get-started.md).</span></span>

    > [!WARNING]
    > <span data-ttu-id="b589c-112">As of September 15, 2017, the HDInsight .NET SDK only supports returning Hive query results from Azure Storage accounts.</span><span class="sxs-lookup"><span data-stu-id="b589c-112">As of September 15, 2017, the HDInsight .NET SDK only supports returning Hive query results from Azure Storage accounts.</span></span> <span data-ttu-id="b589c-113">If you use this example with an HDInsight cluster that uses Azure Data Lake Store as primary storage, you cannot retrieve search results using the .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="b589c-113">If you use this example with an HDInsight cluster that uses Azure Data Lake Store as primary storage, you cannot retrieve search results using the .NET SDK.</span></span>

* <span data-ttu-id="b589c-114">**Visual Studio 2013/2015/2017**.</span><span class="sxs-lookup"><span data-stu-id="b589c-114">**Visual Studio 2013/2015/2017**.</span></span>

## <a name="run-a-hive-query"></a><span data-ttu-id="b589c-115">Run a Hive Query</span><span class="sxs-lookup"><span data-stu-id="b589c-115">Run a Hive Query</span></span>
<span data-ttu-id="b589c-116">The HDInsight .NET SDK provides .NET client libraries, which makes it easier to work with HDInsight clusters from .NET.</span><span class="sxs-lookup"><span data-stu-id="b589c-116">The HDInsight .NET SDK provides .NET client libraries, which makes it easier to work with HDInsight clusters from .NET.</span></span> 

<span data-ttu-id="b589c-117">**To Submit jobs**</span><span class="sxs-lookup"><span data-stu-id="b589c-117">**To Submit jobs**</span></span>

1. <span data-ttu-id="b589c-118">Create a C# console application in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b589c-118">Create a C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="b589c-119">From the Nuget Package Manager Console, run the following command:</span><span class="sxs-lookup"><span data-stu-id="b589c-119">From the Nuget Package Manager Console, run the following command:</span></span>
   
        Install-Package Microsoft.Azure.Management.HDInsight.Job
3. <span data-ttu-id="b589c-120">Use the following code:</span><span class="sxs-lookup"><span data-stu-id="b589c-120">Use the following code:</span></span>

    ```csharp
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
                
                // Only Azure Storage accounts are supported by the SDK
                private const string DefaultStorageAccountName = "<Default Storage Account Name>";
                private const string DefaultStorageAccountKey = "<Default Storage Account Key>";
                private const string DefaultStorageContainerName = "<Default Blob Container Name>";
   
                static void Main(string[] args)
                {
                    System.Console.WriteLine("The application is running ...");
   
                    var clusterCredentials = new BasicAuthenticationCloudCredentials { Username = ExistingClusterUsername, Password = ExistingClusterPassword };
                    _hdiJobManagementClient = new HDInsightJobManagementClient(ExistingClusterUri, clusterCredentials);
   
                    SubmitHiveJob();
   
                    System.Console.WriteLine("Press ENTER to continue ...");
                    System.Console.ReadLine();
                }
   
                private static void SubmitHiveJob()
                {
                    Dictionary<string, string> defines = new Dictionary<string, string> { { "hive.execution.engine", "tez" }, { "hive.exec.reducers.max", "1" } };
                    List<string> args = new List<string> { { "argA" }, { "argB" } };
                    var parameters = new HiveJobSubmissionParameters
                    {
                        Query = "SHOW TABLES",
                        Defines = defines,
                        Arguments = args
                    };
   
                    System.Console.WriteLine("Submitting the Hive job to the cluster...");
                    var jobResponse = _hdiJobManagementClient.JobManagement.SubmitHiveJob(parameters);
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
    ```
4. <span data-ttu-id="b589c-121">Press **F5** to run the application.</span><span class="sxs-lookup"><span data-stu-id="b589c-121">Press **F5** to run the application.</span></span>

<span data-ttu-id="b589c-122">The output of the application shall be similar to:</span><span class="sxs-lookup"><span data-stu-id="b589c-122">The output of the application shall be similar to:</span></span>

![HDInsight Hadoop Hive job output](./media/apache-hadoop-use-hive-dotnet-sdk/hdinsight-hadoop-use-hive-net-sdk-output.png)

## <a name="next-steps"></a><span data-ttu-id="b589c-124">Next steps</span><span class="sxs-lookup"><span data-stu-id="b589c-124">Next steps</span></span>
<span data-ttu-id="b589c-125">In this article, you have learned several ways to create an HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="b589c-125">In this article, you have learned several ways to create an HDInsight cluster.</span></span> <span data-ttu-id="b589c-126">To learn more, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="b589c-126">To learn more, see the following articles:</span></span>

* [<span data-ttu-id="b589c-127">Get started with Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="b589c-127">Get started with Azure HDInsight</span></span>](apache-hadoop-linux-tutorial-get-started.md)
* [<span data-ttu-id="b589c-128">Create Hadoop clusters in HDInsight</span><span class="sxs-lookup"><span data-stu-id="b589c-128">Create Hadoop clusters in HDInsight</span></span>](../hdinsight-hadoop-provision-linux-clusters.md)
* [<span data-ttu-id="b589c-129">Manage Hadoop clusters in HDInsight by using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="b589c-129">Manage Hadoop clusters in HDInsight by using the Azure portal</span></span>](../hdinsight-administer-use-management-portal.md)
* [<span data-ttu-id="b589c-130">HDInsight .NET SDK reference</span><span class="sxs-lookup"><span data-stu-id="b589c-130">HDInsight .NET SDK reference</span></span>](https://docs.microsoft.com/dotnet/api/overview/azure/hdinsight)
* [<span data-ttu-id="b589c-131">Use Pig with HDInsight</span><span class="sxs-lookup"><span data-stu-id="b589c-131">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="b589c-132">Use Sqoop with HDInsight</span><span class="sxs-lookup"><span data-stu-id="b589c-132">Use Sqoop with HDInsight</span></span>](apache-hadoop-use-sqoop-mac-linux.md)
* [<span data-ttu-id="b589c-133">Create non-interactive authentication .NET HDInsight applications</span><span class="sxs-lookup"><span data-stu-id="b589c-133">Create non-interactive authentication .NET HDInsight applications</span></span>](../hdinsight-create-non-interactive-authentication-dotnet-applications.md)
 


