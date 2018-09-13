---
title: Run Hive queries using HDInsight .NET SDK | Microsoft Docs
description: Learn how to submit Hadoop jobs to Azure HDInsight Hadoop using HDInsight .NET SDK.
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: ''
tags: azure-portal
author: mumian
ms.assetid: 4e291890-f8b4-426c-b5e8-d4fd512ff042
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/03/2017
ms.author: jgao
ms.openlocfilehash: 8164d1594bda5aa750fc88d20b96f9cd5976179c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550601"
---
# <a name="run-hive-queries-using-hdinsight-net-sdk"></a><span data-ttu-id="d8cf9-103">Run Hive queries using HDInsight .NET SDK</span><span class="sxs-lookup"><span data-stu-id="d8cf9-103">Run Hive queries using HDInsight .NET SDK</span></span>
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="d8cf9-104">Learn how to submit Hive queries using HDInsight .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="d8cf9-104">Learn how to submit Hive queries using HDInsight .NET SDK.</span></span>

> [!NOTE]
> <span data-ttu-id="d8cf9-105">The steps in this article must be performed from a Windows client.</span><span class="sxs-lookup"><span data-stu-id="d8cf9-105">The steps in this article must be performed from a Windows client.</span></span> <span data-ttu-id="d8cf9-106">For information on using a Linux, OS X, or Unix client to work with Hive, use the tab selector shown on the top of the article.</span><span class="sxs-lookup"><span data-stu-id="d8cf9-106">For information on using a Linux, OS X, or Unix client to work with Hive, use the tab selector shown on the top of the article.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="d8cf9-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d8cf9-107">Prerequisites</span></span>
<span data-ttu-id="d8cf9-108">Before you begin this article, you must have the following items:</span><span class="sxs-lookup"><span data-stu-id="d8cf9-108">Before you begin this article, you must have the following items:</span></span>

* <span data-ttu-id="d8cf9-109">**A Hadoop cluster in HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="d8cf9-109">**A Hadoop cluster in HDInsight**.</span></span> <span data-ttu-id="d8cf9-110">See [Get started using Linux-based Hadoop in HDInsight](hdinsight-use-sqoop.md#create-cluster-and-sql-database).</span><span class="sxs-lookup"><span data-stu-id="d8cf9-110">See [Get started using Linux-based Hadoop in HDInsight](hdinsight-use-sqoop.md#create-cluster-and-sql-database).</span></span>
* <span data-ttu-id="d8cf9-111">**Visual Studio 2013/2015/2017**.</span><span class="sxs-lookup"><span data-stu-id="d8cf9-111">**Visual Studio 2013/2015/2017**.</span></span>

## <a name="submit-hive-queries-using-hdinsight-net-sdk"></a><span data-ttu-id="d8cf9-112">Submit Hive queries using HDInsight .NET SDK</span><span class="sxs-lookup"><span data-stu-id="d8cf9-112">Submit Hive queries using HDInsight .NET SDK</span></span>
<span data-ttu-id="d8cf9-113">The HDInsight .NET SDK provides .NET client libraries, which makes it easier to work with HDInsight clusters from .NET.</span><span class="sxs-lookup"><span data-stu-id="d8cf9-113">The HDInsight .NET SDK provides .NET client libraries, which makes it easier to work with HDInsight clusters from .NET.</span></span> 

<span data-ttu-id="d8cf9-114">**To Submit jobs**</span><span class="sxs-lookup"><span data-stu-id="d8cf9-114">**To Submit jobs**</span></span>

1. <span data-ttu-id="d8cf9-115">Create a C# console application in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d8cf9-115">Create a C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="d8cf9-116">From the Nuget Package Manager Console, run the following command:</span><span class="sxs-lookup"><span data-stu-id="d8cf9-116">From the Nuget Package Manager Console, run the following command:</span></span>
   
        Install-Package Microsoft.Azure.Management.HDInsight.Job
3. <span data-ttu-id="d8cf9-117">Use the following code:</span><span class="sxs-lookup"><span data-stu-id="d8cf9-117">Use the following code:</span></span>

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
                    Dictionary<string, string> defines = new Dictionary<string, string> { { "hive.execution.engine", "ravi" }, { "hive.exec.reducers.max", "1" } };
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
4. <span data-ttu-id="d8cf9-118">Press **F5** to run the application.</span><span class="sxs-lookup"><span data-stu-id="d8cf9-118">Press **F5** to run the application.</span></span>

<span data-ttu-id="d8cf9-119">The output of the application shall be similar to:</span><span class="sxs-lookup"><span data-stu-id="d8cf9-119">The output of the application shall be similar to:</span></span>

![HDInsight Hadoop Hive job output](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-use-hive-dotnet-sdk/hdinsight-hadoop-use-hive-net-sdk-output.png)

## <a name="next-steps"></a><span data-ttu-id="d8cf9-121">Next steps</span><span class="sxs-lookup"><span data-stu-id="d8cf9-121">Next steps</span></span>
<span data-ttu-id="d8cf9-122">In this article, you have learned several ways to create an HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="d8cf9-122">In this article, you have learned several ways to create an HDInsight cluster.</span></span> <span data-ttu-id="d8cf9-123">To learn more, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="d8cf9-123">To learn more, see the following articles:</span></span>

* <span data-ttu-id="d8cf9-124">[Get started with Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="d8cf9-124">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="d8cf9-125">[Create Hadoop clusters in HDInsight][hdinsight-provision]</span><span class="sxs-lookup"><span data-stu-id="d8cf9-125">[Create Hadoop clusters in HDInsight][hdinsight-provision]</span></span>
* [<span data-ttu-id="d8cf9-126">Manage Hadoop clusters in HDInsight by using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="d8cf9-126">Manage Hadoop clusters in HDInsight by using the Azure portal</span></span>](hdinsight-administer-use-management-portal.md)
* [<span data-ttu-id="d8cf9-127">HDInsight .NET SDK reference</span><span class="sxs-lookup"><span data-stu-id="d8cf9-127">HDInsight .NET SDK reference</span></span>](https://msdn.microsoft.com/library/mt271028.aspx)
* [<span data-ttu-id="d8cf9-128">Use Pig with HDInsight</span><span class="sxs-lookup"><span data-stu-id="d8cf9-128">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="d8cf9-129">Use Sqoop with HDInsight</span><span class="sxs-lookup"><span data-stu-id="d8cf9-129">Use Sqoop with HDInsight</span></span>](hdinsight-use-sqoop-mac-linux.md)
* [<span data-ttu-id="d8cf9-130">Create non-interactive authentication .NET HDInsight applications</span><span class="sxs-lookup"><span data-stu-id="d8cf9-130">Create non-interactive authentication .NET HDInsight applications</span></span>](hdinsight-create-non-interactive-authentication-dotnet-applications.md)

[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md



