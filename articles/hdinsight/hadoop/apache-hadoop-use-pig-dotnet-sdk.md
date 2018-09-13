---
title: Run Apache Pig jobs with .NET SDK for Hadoop - Azure HDInsight
description: Learn how to use the .NET SDK for Hadoop to submit Pig jobs to Hadoop on HDInsight.
services: hdinsight
author: jasonwhowell
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 05/01/2018
ms.author: jasonh
ms.openlocfilehash: 06d2633556e149f48c9750b5df0408b601bf3da3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865401"
---
# <a name="run-pig-jobs-using-the-net-sdk-for-hadoop-in-hdinsight"></a><span data-ttu-id="de21b-103">Run Pig jobs using the .NET SDK for Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="de21b-103">Run Pig jobs using the .NET SDK for Hadoop in HDInsight</span></span>

[!INCLUDE [pig-selector](../../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="de21b-104">Learn how to use the .NET SDK for Hadoop to submit Apache Pig jobs to Hadoop on Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="de21b-104">Learn how to use the .NET SDK for Hadoop to submit Apache Pig jobs to Hadoop on Azure HDInsight.</span></span>

<span data-ttu-id="de21b-105">The HDInsight .NET SDK provides .NET client libraries that makes it easier to work with HDInsight clusters from .NET.</span><span class="sxs-lookup"><span data-stu-id="de21b-105">The HDInsight .NET SDK provides .NET client libraries that makes it easier to work with HDInsight clusters from .NET.</span></span> <span data-ttu-id="de21b-106">Pig allows you to create MapReduce operations by modeling a series of data transformations.</span><span class="sxs-lookup"><span data-stu-id="de21b-106">Pig allows you to create MapReduce operations by modeling a series of data transformations.</span></span> <span data-ttu-id="de21b-107">In this document, you learn how to use a basic C# application to submit a Pig job to an HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="de21b-107">In this document, you learn how to use a basic C# application to submit a Pig job to an HDInsight cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="de21b-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="de21b-108">Prerequisites</span></span>

<span data-ttu-id="de21b-109">To complete the steps in this article, you need the following.</span><span class="sxs-lookup"><span data-stu-id="de21b-109">To complete the steps in this article, you need the following.</span></span>

* <span data-ttu-id="de21b-110">An Azure HDInsight (Hadoop on HDInsight) cluster (either Windows or Linux-based).</span><span class="sxs-lookup"><span data-stu-id="de21b-110">An Azure HDInsight (Hadoop on HDInsight) cluster (either Windows or Linux-based).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="de21b-111">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="de21b-111">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="de21b-112">For more information, see [HDInsight retirement on Windows](../hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="de21b-112">For more information, see [HDInsight retirement on Windows](../hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="de21b-113">Visual Studio 2012, 2013, 2015 or 2017.</span><span class="sxs-lookup"><span data-stu-id="de21b-113">Visual Studio 2012, 2013, 2015 or 2017.</span></span>

## <a name="create-the-application"></a><span data-ttu-id="de21b-114">Create the application</span><span class="sxs-lookup"><span data-stu-id="de21b-114">Create the application</span></span>

<span data-ttu-id="de21b-115">The HDInsight .NET SDK provides .NET client libraries, which makes it easier to work with HDInsight clusters from .NET.</span><span class="sxs-lookup"><span data-stu-id="de21b-115">The HDInsight .NET SDK provides .NET client libraries, which makes it easier to work with HDInsight clusters from .NET.</span></span>

1. <span data-ttu-id="de21b-116">From the **File** menu in Visual Studio, select **New** and then select **Project**.</span><span class="sxs-lookup"><span data-stu-id="de21b-116">From the **File** menu in Visual Studio, select **New** and then select **Project**.</span></span>

2. <span data-ttu-id="de21b-117">For the new project, type or select the following values:</span><span class="sxs-lookup"><span data-stu-id="de21b-117">For the new project, type or select the following values:</span></span>

   | <span data-ttu-id="de21b-118">Property</span><span class="sxs-lookup"><span data-stu-id="de21b-118">Property</span></span> | <span data-ttu-id="de21b-119">Value</span><span class="sxs-lookup"><span data-stu-id="de21b-119">Value</span></span> |
   | ------ | ------ |
   | <span data-ttu-id="de21b-120">Category</span><span class="sxs-lookup"><span data-stu-id="de21b-120">Category</span></span> | <span data-ttu-id="de21b-121">Templates/Visual C#/Windows</span><span class="sxs-lookup"><span data-stu-id="de21b-121">Templates/Visual C#/Windows</span></span> |
   | <span data-ttu-id="de21b-122">Template</span><span class="sxs-lookup"><span data-stu-id="de21b-122">Template</span></span> | <span data-ttu-id="de21b-123">Console Application</span><span class="sxs-lookup"><span data-stu-id="de21b-123">Console Application</span></span> |
   | <span data-ttu-id="de21b-124">Name</span><span class="sxs-lookup"><span data-stu-id="de21b-124">Name</span></span> | <span data-ttu-id="de21b-125">SubmitPigJob</span><span class="sxs-lookup"><span data-stu-id="de21b-125">SubmitPigJob</span></span> |

3. <span data-ttu-id="de21b-126">Click **OK** to create the project.</span><span class="sxs-lookup"><span data-stu-id="de21b-126">Click **OK** to create the project.</span></span>

4. <span data-ttu-id="de21b-127">From the **Tools** menu, select **Library Package Manager** or **NuGet Package Manager**, and then select **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="de21b-127">From the **Tools** menu, select **Library Package Manager** or **NuGet Package Manager**, and then select **Package Manager Console**.</span></span>

5. <span data-ttu-id="de21b-128">To install the .NET SDK packages, use the following command:</span><span class="sxs-lookup"><span data-stu-id="de21b-128">To install the .NET SDK packages, use the following command:</span></span>

        Install-Package Microsoft.Azure.Management.HDInsight.Job

6. <span data-ttu-id="de21b-129">From Solution Explorer, double-click **Program.cs** to open it.</span><span class="sxs-lookup"><span data-stu-id="de21b-129">From Solution Explorer, double-click **Program.cs** to open it.</span></span> <span data-ttu-id="de21b-130">Replace the existing code with the following.</span><span class="sxs-lookup"><span data-stu-id="de21b-130">Replace the existing code with the following.</span></span>

    ```csharp
    using Microsoft.Azure.Management.HDInsight.Job;
    using Microsoft.Azure.Management.HDInsight.Job.Models;
    using Hyak.Common;

    namespace SubmitPigJob
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

7. <span data-ttu-id="de21b-131">To start the application, press **F5**.</span><span class="sxs-lookup"><span data-stu-id="de21b-131">To start the application, press **F5**.</span></span>

8. <span data-ttu-id="de21b-132">To exit the application, press **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="de21b-132">To exit the application, press **ENTER**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="de21b-133">Next steps</span><span class="sxs-lookup"><span data-stu-id="de21b-133">Next steps</span></span>

<span data-ttu-id="de21b-134">For information on Pig in HDInsight, see [Use Pig with Hadoop on HDInsight](hdinsight-use-pig.md).</span><span class="sxs-lookup"><span data-stu-id="de21b-134">For information on Pig in HDInsight, see [Use Pig with Hadoop on HDInsight](hdinsight-use-pig.md).</span></span>

<span data-ttu-id="de21b-135">For more information on using Hadoop on HDInsight, see the following documents:</span><span class="sxs-lookup"><span data-stu-id="de21b-135">For more information on using Hadoop on HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="de21b-136">Use Hive with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="de21b-136">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="de21b-137">Use MapReduce with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="de21b-137">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

[preview-portal]: https://portal.azure.com/
