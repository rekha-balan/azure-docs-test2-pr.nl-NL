---
title: Use Hadoop Pig with .NET in HDInsight | Microsoft Docs
description: Learn how to use the .NET SDK for Hadoop to submit Pig jobs to Hadoop on HDInsight.
services: hdinsight
documentationcenter: .net
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: fa11d49a-328c-47e7-b16d-e7ed2a453195
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/03/2017
ms.author: larryfr
ms.openlocfilehash: 10e2f35bdaf1b6e00e3d8dde34dd5809a89cde30
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550779"
---
# <a name="run-pig-jobs-using-the-net-sdk-for-hadoop-in-hdinsight"></a><span data-ttu-id="e92d5-103">Run Pig jobs using the .NET SDK for Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="e92d5-103">Run Pig jobs using the .NET SDK for Hadoop in HDInsight</span></span>
[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="e92d5-104">This document provides an example of using the .NET SDK for Hadoop to submit Pig jobs to a Hadoop on HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="e92d5-104">This document provides an example of using the .NET SDK for Hadoop to submit Pig jobs to a Hadoop on HDInsight cluster.</span></span>

<span data-ttu-id="e92d5-105">The HDInsight .NET SDK provides .NET client libraries that makes it easier to work with HDInsight clusters from .NET.</span><span class="sxs-lookup"><span data-stu-id="e92d5-105">The HDInsight .NET SDK provides .NET client libraries that makes it easier to work with HDInsight clusters from .NET.</span></span> <span data-ttu-id="e92d5-106">Pig allows you to create MapReduce operations by modeling a series of data transformations.</span><span class="sxs-lookup"><span data-stu-id="e92d5-106">Pig allows you to create MapReduce operations by modeling a series of data transformations.</span></span> <span data-ttu-id="e92d5-107">In this document, you learn how to use a basic C# application to submit a Pig job to an HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="e92d5-107">In this document, you learn how to use a basic C# application to submit a Pig job to an HDInsight cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e92d5-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e92d5-108">Prerequisites</span></span>

<span data-ttu-id="e92d5-109">To complete the steps in this article, you need the following.</span><span class="sxs-lookup"><span data-stu-id="e92d5-109">To complete the steps in this article, you need the following.</span></span>

* <span data-ttu-id="e92d5-110">An Azure HDInsight (Hadoop on HDInsight) cluster (either Windows or Linux-based).</span><span class="sxs-lookup"><span data-stu-id="e92d5-110">An Azure HDInsight (Hadoop on HDInsight) cluster (either Windows or Linux-based).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="e92d5-111">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="e92d5-111">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="e92d5-112">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span><span class="sxs-lookup"><span data-stu-id="e92d5-112">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span></span>

* <span data-ttu-id="e92d5-113">Visual Studio 2012, 2013, 2015 or 2017.</span><span class="sxs-lookup"><span data-stu-id="e92d5-113">Visual Studio 2012, 2013, 2015 or 2017.</span></span>

## <a name="create-the-application"></a><span data-ttu-id="e92d5-114">Create the application</span><span class="sxs-lookup"><span data-stu-id="e92d5-114">Create the application</span></span>

<span data-ttu-id="e92d5-115">The HDInsight .NET SDK provides .NET client libraries, which makes it easier to work with HDInsight clusters from .NET.</span><span class="sxs-lookup"><span data-stu-id="e92d5-115">The HDInsight .NET SDK provides .NET client libraries, which makes it easier to work with HDInsight clusters from .NET.</span></span>

1. <span data-ttu-id="e92d5-116">From the **File** menu in Visual Studio, select **New** and then select **Project**.</span><span class="sxs-lookup"><span data-stu-id="e92d5-116">From the **File** menu in Visual Studio, select **New** and then select **Project**.</span></span>

2. <span data-ttu-id="e92d5-117">For the new project, type or select the following values:</span><span class="sxs-lookup"><span data-stu-id="e92d5-117">For the new project, type or select the following values:</span></span>

   | <span data-ttu-id="e92d5-118">Property</span><span class="sxs-lookup"><span data-stu-id="e92d5-118">Property</span></span> | <span data-ttu-id="e92d5-119">Value</span><span class="sxs-lookup"><span data-stu-id="e92d5-119">Value</span></span> |
   | ------ | ------ |
   | <span data-ttu-id="e92d5-120">Category</span><span class="sxs-lookup"><span data-stu-id="e92d5-120">Category</span></span> | <span data-ttu-id="e92d5-121">Templates/Visual C#/Windows</span><span class="sxs-lookup"><span data-stu-id="e92d5-121">Templates/Visual C#/Windows</span></span> |
   | <span data-ttu-id="e92d5-122">Template</span><span class="sxs-lookup"><span data-stu-id="e92d5-122">Template</span></span> | <span data-ttu-id="e92d5-123">Console Application</span><span class="sxs-lookup"><span data-stu-id="e92d5-123">Console Application</span></span> |
   | <span data-ttu-id="e92d5-124">Name</span><span class="sxs-lookup"><span data-stu-id="e92d5-124">Name</span></span> | <span data-ttu-id="e92d5-125">SubmitPigJob</span><span class="sxs-lookup"><span data-stu-id="e92d5-125">SubmitPigJob</span></span> |

3. <span data-ttu-id="e92d5-126">Click **OK** to create the project.</span><span class="sxs-lookup"><span data-stu-id="e92d5-126">Click **OK** to create the project.</span></span>

4. <span data-ttu-id="e92d5-127">From the **Tools** menu, select **Library Package Manager** or **Nuget Package Manager**, and then select **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="e92d5-127">From the **Tools** menu, select **Library Package Manager** or **Nuget Package Manager**, and then select **Package Manager Console**.</span></span>

5. <span data-ttu-id="e92d5-128">To install the .NET SDK packages, use the following command:</span><span class="sxs-lookup"><span data-stu-id="e92d5-128">To install the .NET SDK packages, use the following command:</span></span>

        Install-Package Microsoft.Azure.Management.HDInsight.Job

6. <span data-ttu-id="e92d5-129">From Solution Explorer, double-click **Program.cs** to open it.</span><span class="sxs-lookup"><span data-stu-id="e92d5-129">From Solution Explorer, double-click **Program.cs** to open it.</span></span> <span data-ttu-id="e92d5-130">Replace the existing code with the following.</span><span class="sxs-lookup"><span data-stu-id="e92d5-130">Replace the existing code with the following.</span></span>

    ```csharp
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

            static void Main(string[] args)
            {
                System.Console.WriteLine("The application is running ...");

                var clusterCredentials = new BasicAuthenticationCloudCredentials { Username = ExistingClusterUsername, Password = ExistingClusterPassword };
                _hdiJobManagementClient = new HDInsightJobManagementClient(ExistingClusterUri, clusterCredentials);

                SubmitPigJob();

                System.Console.WriteLine("Press ENTER to continue ...");
                System.Console.ReadLine();
            }

            private static void SubmitPigJob()
            {
                var parameters = new PigJobSubmissionParameters
                {
                    Query = @"LOGS = LOAD '/example/data/sample.log';
                                LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
                                FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
                                GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
                                FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
                                RESULT = order FREQUENCIES by COUNT desc;
                                DUMP RESULT;"
                };

                System.Console.WriteLine("Submitting the Pig job to the cluster...");
                var response = _hdiJobManagementClient.JobManagement.SubmitPigJob(parameters);
                System.Console.WriteLine("Validating that the response is as expected...");
                System.Console.WriteLine("Response status code is " + response.StatusCode);
                System.Console.WriteLine("Validating the response object...");
                System.Console.WriteLine("JobId is " + response.JobSubmissionJsonResponse.Id);
            }
        }
    }
    ```

7. <span data-ttu-id="e92d5-131">To start the application, press **F5**.</span><span class="sxs-lookup"><span data-stu-id="e92d5-131">To start the application, press **F5**.</span></span>

8. <span data-ttu-id="e92d5-132">To exit the application, press **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="e92d5-132">To exit the application, press **ENTER**.</span></span>

## <a name="summary"></a><span data-ttu-id="e92d5-133">Summary</span><span class="sxs-lookup"><span data-stu-id="e92d5-133">Summary</span></span>

<span data-ttu-id="e92d5-134">As you can see, the .NET SDK for Hadoop allows you to create .NET applications that submit Pig jobs to an HDInsight cluster, and monitor the job status.</span><span class="sxs-lookup"><span data-stu-id="e92d5-134">As you can see, the .NET SDK for Hadoop allows you to create .NET applications that submit Pig jobs to an HDInsight cluster, and monitor the job status.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e92d5-135">Next steps</span><span class="sxs-lookup"><span data-stu-id="e92d5-135">Next steps</span></span>

<span data-ttu-id="e92d5-136">For information on Pig in HDInsight, see [Use Pig with Hadoop on HDInsight](hdinsight-use-pig.md).</span><span class="sxs-lookup"><span data-stu-id="e92d5-136">For information on Pig in HDInsight, see [Use Pig with Hadoop on HDInsight](hdinsight-use-pig.md).</span></span>

<span data-ttu-id="e92d5-137">For more information on using Hadoop on HDInsight, see the following documents:</span><span class="sxs-lookup"><span data-stu-id="e92d5-137">For more information on using Hadoop on HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="e92d5-138">Use Hive with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="e92d5-138">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="e92d5-139">Use MapReduce with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="e92d5-139">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

[preview-portal]: https://portal.azure.com/
