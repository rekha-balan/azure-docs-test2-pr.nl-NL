---
title: Run Sqoop jobs by using .NET and HDInsight - Azure
description: Learn how to use the HDInsight .NET SDK to run Sqoop import and export between a Hadoop cluster and an Azure SQL database.
keywords: sqoop job
ms.reviewer: jasonh
services: hdinsight
author: jasonwhowell
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.topic: conceptual
ms.date: 05/16/2018
ms.author: jasonh
ms.openlocfilehash: ffcc2bff17fbe07c58df032dbb8994edb04ae5d0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867239"
---
# <a name="run-sqoop-jobs-by-using-net-sdk-for-hadoop-in-hdinsight"></a><span data-ttu-id="db738-104">Run Sqoop jobs by using .NET SDK for Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="db738-104">Run Sqoop jobs by using .NET SDK for Hadoop in HDInsight</span></span>
[!INCLUDE [sqoop-selector](../../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="db738-105">Learn how to use the Azure HDInsight .NET SDK to run Sqoop jobs in HDInsight to import and export between an HDInsight cluster and an Azure SQL database or SQL Server database.</span><span class="sxs-lookup"><span data-stu-id="db738-105">Learn how to use the Azure HDInsight .NET SDK to run Sqoop jobs in HDInsight to import and export between an HDInsight cluster and an Azure SQL database or SQL Server database.</span></span>

> [!NOTE]
> <span data-ttu-id="db738-106">Although you can use the procedures in this article with either a Windows-based or Linux-based HDInsight cluster, they work only from a Windows client.</span><span class="sxs-lookup"><span data-stu-id="db738-106">Although you can use the procedures in this article with either a Windows-based or Linux-based HDInsight cluster, they work only from a Windows client.</span></span> <span data-ttu-id="db738-107">To choose other methods, use the tab selector at the top of this article.</span><span class="sxs-lookup"><span data-stu-id="db738-107">To choose other methods, use the tab selector at the top of this article.</span></span>
> 

## <a name="prerequisites"></a><span data-ttu-id="db738-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="db738-108">Prerequisites</span></span>
<span data-ttu-id="db738-109">Before you begin this tutorial, you must have the following item:</span><span class="sxs-lookup"><span data-stu-id="db738-109">Before you begin this tutorial, you must have the following item:</span></span>

* <span data-ttu-id="db738-110">A Hadoop cluster in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="db738-110">A Hadoop cluster in HDInsight.</span></span> <span data-ttu-id="db738-111">For more information, see [Create a cluster and a SQL database](hdinsight-use-sqoop.md#create-cluster-and-sql-database).</span><span class="sxs-lookup"><span data-stu-id="db738-111">For more information, see [Create a cluster and a SQL database](hdinsight-use-sqoop.md#create-cluster-and-sql-database).</span></span>

## <a name="use-sqoop-on-hdinsight-clusters-with-the-net-sdk"></a><span data-ttu-id="db738-112">Use Sqoop on HDInsight clusters with the .NET SDK</span><span class="sxs-lookup"><span data-stu-id="db738-112">Use Sqoop on HDInsight clusters with the .NET SDK</span></span>
<span data-ttu-id="db738-113">The HDInsight .NET SDK provides .NET client libraries, so that it's easier to work with HDInsight clusters from .NET.</span><span class="sxs-lookup"><span data-stu-id="db738-113">The HDInsight .NET SDK provides .NET client libraries, so that it's easier to work with HDInsight clusters from .NET.</span></span> <span data-ttu-id="db738-114">In this section, you create a C# console application to export the hivesampletable to the Azure SQL Database table that you created earlier in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="db738-114">In this section, you create a C# console application to export the hivesampletable to the Azure SQL Database table that you created earlier in this tutorial.</span></span>

## <a name="submit-a-sqoop-job"></a><span data-ttu-id="db738-115">Submit a Sqoop job</span><span class="sxs-lookup"><span data-stu-id="db738-115">Submit a Sqoop job</span></span>

1. <span data-ttu-id="db738-116">Create a C# console application in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="db738-116">Create a C# console application in Visual Studio.</span></span>

2. <span data-ttu-id="db738-117">From the Visual Studio Package Manager console, import the package by running the following NuGet command:</span><span class="sxs-lookup"><span data-stu-id="db738-117">From the Visual Studio Package Manager console, import the package by running the following NuGet command:</span></span>
   
        Install-Package Microsoft.Azure.Management.HDInsight.Job

3. <span data-ttu-id="db738-118">Use the following code in the Program.cs file:</span><span class="sxs-lookup"><span data-stu-id="db738-118">Use the following code in the Program.cs file:</span></span>
   
        using System.Collections.Generic;
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
   
                    SubmitSqoopJob();
   
                    System.Console.WriteLine("Press ENTER to continue ...");
                    System.Console.ReadLine();
                }
   
                private static void SubmitSqoopJob()
                {
                    var sqlDatabaseServerName = "<SQLDatabaseServerName>";
                    var sqlDatabaseLogin = "<SQLDatabaseLogin>";
                    var sqlDatabaseLoginPassword = "<SQLDatabaseLoginPassword>";
                    var sqlDatabaseDatabaseName = "<DatabaseName>";
   
                    var tableName = "<TableName>";
                    var exportDir = "/tutorials/usesqoop/data";
   
                    // Connection string for using Azure SQL Database.
                    // Comment if using SQL Server
                    var connectionString = "jdbc:sqlserver://" + sqlDatabaseServerName + ".database.windows.net;user=" + sqlDatabaseLogin + "@" + sqlDatabaseServerName + ";password=" + sqlDatabaseLoginPassword + ";database=" + sqlDatabaseDatabaseName;
                    // Connection string for using SQL Server.
                    // Uncomment if using SQL Server
                    //var connectionString = "jdbc:sqlserver://" + sqlDatabaseServerName + ";user=" + sqlDatabaseLogin + ";password=" + sqlDatabaseLoginPassword + ";database=" + sqlDatabaseDatabaseName;
   
                    var parameters = new SqoopJobSubmissionParameters
                    {
                        Files = new List<string> { "/user/oozie/share/lib/sqoop/sqljdbc41.jar" }, // This line is required for Linux-based cluster.
                        Command = "export --connect " + connectionString + " --table " + tableName + "_mobile --export-dir " + exportDir + "_mobile --fields-terminated-by \\t -m 1"
                    };
   
                    System.Console.WriteLine("Submitting the Sqoop job to the cluster...");
                    var response = _hdiJobManagementClient.JobManagement.SubmitSqoopJob(parameters);
                    System.Console.WriteLine("Validating that the response is as expected...");
                    System.Console.WriteLine("Response status code is " + response.StatusCode);
                    System.Console.WriteLine("Validating the response object...");
                    System.Console.WriteLine("JobId is " + response.JobSubmissionJsonResponse.Id);
                }
            }
        }

4. <span data-ttu-id="db738-119">To run the program, select the **F5** key.</span><span class="sxs-lookup"><span data-stu-id="db738-119">To run the program, select the **F5** key.</span></span> 

## <a name="limitations"></a><span data-ttu-id="db738-120">Limitations</span><span class="sxs-lookup"><span data-stu-id="db738-120">Limitations</span></span>
<span data-ttu-id="db738-121">Linux-based HDInsight presents the following limitations:</span><span class="sxs-lookup"><span data-stu-id="db738-121">Linux-based HDInsight presents the following limitations:</span></span>

* <span data-ttu-id="db738-122">Bulk export: The Sqoop connector that's used to export data to Microsoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span><span class="sxs-lookup"><span data-stu-id="db738-122">Bulk export: The Sqoop connector that's used to export data to Microsoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>

* <span data-ttu-id="db738-123">Batching: By using the `-batch` switch when it performs inserts, Sqoop performs multiple inserts instead of batching the insert operations.</span><span class="sxs-lookup"><span data-stu-id="db738-123">Batching: By using the `-batch` switch when it performs inserts, Sqoop performs multiple inserts instead of batching the insert operations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="db738-124">Next steps</span><span class="sxs-lookup"><span data-stu-id="db738-124">Next steps</span></span>
<span data-ttu-id="db738-125">Now you have learned how to use Sqoop.</span><span class="sxs-lookup"><span data-stu-id="db738-125">Now you have learned how to use Sqoop.</span></span> <span data-ttu-id="db738-126">To learn more, see:</span><span class="sxs-lookup"><span data-stu-id="db738-126">To learn more, see:</span></span>

* <span data-ttu-id="db738-127">[Use Oozie with HDInsight](../hdinsight-use-oozie.md): Use Sqoop action in an Oozie workflow.</span><span class="sxs-lookup"><span data-stu-id="db738-127">[Use Oozie with HDInsight](../hdinsight-use-oozie.md): Use Sqoop action in an Oozie workflow.</span></span>
* <span data-ttu-id="db738-128">[Analyze flight delay data using HDInsight](../hdinsight-analyze-flight-delay-data.md): Use Hive to analyze flight delay data, and then use Sqoop to export data to an Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="db738-128">[Analyze flight delay data using HDInsight](../hdinsight-analyze-flight-delay-data.md): Use Hive to analyze flight delay data, and then use Sqoop to export data to an Azure SQL database.</span></span>
* <span data-ttu-id="db738-129">[Upload data to HDInsight](../hdinsight-upload-data.md): Find other methods for uploading data to HDInsight or Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="db738-129">[Upload data to HDInsight](../hdinsight-upload-data.md): Find other methods for uploading data to HDInsight or Azure Blob storage.</span></span>

