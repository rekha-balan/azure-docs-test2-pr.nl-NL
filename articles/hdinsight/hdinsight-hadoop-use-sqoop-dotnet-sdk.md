---
title: Run Sqoop jobs using .NET and Azure HDInsight | Microsoft Docs
description: Learn how to use HDInsight .NET SDK to run Sqoop import and export between an Hadoop cluster and an Azure SQL database.
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: ''
tags: azure-portal
author: mumian
ms.assetid: 87bacd13-7775-4b71-91da-161cb6224a96
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: jgao
ms.openlocfilehash: 9e23af6b239642fd9f5fb57e7e0d86506903a63f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556798"
---
# <a name="run-sqoop-jobs-using-net-sdk-for-hadoop-in-hdinsight"></a><span data-ttu-id="cec42-103">Run Sqoop jobs using .NET SDK for Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="cec42-103">Run Sqoop jobs using .NET SDK for Hadoop in HDInsight</span></span>
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="cec42-104">Learn how to use HDInsight .NET SDK to run Sqoop jobs in HDInsight to import and export between HDInsight cluster and Azure SQL database or SQL Server database.</span><span class="sxs-lookup"><span data-stu-id="cec42-104">Learn how to use HDInsight .NET SDK to run Sqoop jobs in HDInsight to import and export between HDInsight cluster and Azure SQL database or SQL Server database.</span></span>

> [!NOTE]
> <span data-ttu-id="cec42-105">The steps in this article can be used with either a Windows-based or Linux-based HDInsight cluster; however, these steps will only work from a Windows client.</span><span class="sxs-lookup"><span data-stu-id="cec42-105">The steps in this article can be used with either a Windows-based or Linux-based HDInsight cluster; however, these steps will only work from a Windows client.</span></span> <span data-ttu-id="cec42-106">Use the tab selector on the top of this article to choose other methods.</span><span class="sxs-lookup"><span data-stu-id="cec42-106">Use the tab selector on the top of this article to choose other methods.</span></span>
> 
> 

### <a name="prerequisites"></a><span data-ttu-id="cec42-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="cec42-107">Prerequisites</span></span>
<span data-ttu-id="cec42-108">Before you begin this tutorial, you must have the following:</span><span class="sxs-lookup"><span data-stu-id="cec42-108">Before you begin this tutorial, you must have the following:</span></span>

* <span data-ttu-id="cec42-109">**A Hadoop cluster in HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="cec42-109">**A Hadoop cluster in HDInsight**.</span></span> <span data-ttu-id="cec42-110">See [Create cluster and SQL database](hdinsight-use-sqoop.md#create-cluster-and-sql-database).</span><span class="sxs-lookup"><span data-stu-id="cec42-110">See [Create cluster and SQL database](hdinsight-use-sqoop.md#create-cluster-and-sql-database).</span></span>

## <a name="run-sqoop-using-net-sdk"></a><span data-ttu-id="cec42-111">Run Sqoop using .NET SDK</span><span class="sxs-lookup"><span data-stu-id="cec42-111">Run Sqoop using .NET SDK</span></span>
<span data-ttu-id="cec42-112">The HDInsight .NET SDK provides .NET client libraries, which makes it easier to work with HDInsight clusters from .NET.</span><span class="sxs-lookup"><span data-stu-id="cec42-112">The HDInsight .NET SDK provides .NET client libraries, which makes it easier to work with HDInsight clusters from .NET.</span></span> <span data-ttu-id="cec42-113">In this section, you will create a C# console application to export the hivesampletable to the SQL Database table you created earlier in this tutorials.</span><span class="sxs-lookup"><span data-stu-id="cec42-113">In this section, you will create a C# console application to export the hivesampletable to the SQL Database table you created earlier in this tutorials.</span></span>

<span data-ttu-id="cec42-114">**To submit a Sqoop job**</span><span class="sxs-lookup"><span data-stu-id="cec42-114">**To submit a Sqoop job**</span></span>

1. <span data-ttu-id="cec42-115">Create a C# console application in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cec42-115">Create a C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="cec42-116">From the Visual Studio Package Manager Console, run the following Nuget command to import the package.</span><span class="sxs-lookup"><span data-stu-id="cec42-116">From the Visual Studio Package Manager Console, run the following Nuget command to import the package.</span></span>
   
        Install-Package Microsoft.Azure.Management.HDInsight.Job
3. <span data-ttu-id="cec42-117">Use the following code in the Program.cs file:</span><span class="sxs-lookup"><span data-stu-id="cec42-117">Use the following code in the Program.cs file:</span></span>
   
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
4. <span data-ttu-id="cec42-118">Press **F5** to run the program.</span><span class="sxs-lookup"><span data-stu-id="cec42-118">Press **F5** to run the program.</span></span> 

## <a name="limitations"></a><span data-ttu-id="cec42-119">Limitations</span><span class="sxs-lookup"><span data-stu-id="cec42-119">Limitations</span></span>
* <span data-ttu-id="cec42-120">Bulk export - With Linux-based HDInsight, the Sqoop connector used to export data to Microsoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span><span class="sxs-lookup"><span data-stu-id="cec42-120">Bulk export - With Linux-based HDInsight, the Sqoop connector used to export data to Microsoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>
* <span data-ttu-id="cec42-121">Batching - With Linux-based HDInsight, When using the `-batch` switch when performing inserts, Sqoop will perform multiple inserts instead of batching the insert operations.</span><span class="sxs-lookup"><span data-stu-id="cec42-121">Batching - With Linux-based HDInsight, When using the `-batch` switch when performing inserts, Sqoop will perform multiple inserts instead of batching the insert operations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cec42-122">Next steps</span><span class="sxs-lookup"><span data-stu-id="cec42-122">Next steps</span></span>
<span data-ttu-id="cec42-123">Now you have learned how to use Sqoop.</span><span class="sxs-lookup"><span data-stu-id="cec42-123">Now you have learned how to use Sqoop.</span></span> <span data-ttu-id="cec42-124">To learn more, see:</span><span class="sxs-lookup"><span data-stu-id="cec42-124">To learn more, see:</span></span>

* <span data-ttu-id="cec42-125">[Use Oozie with HDInsight](hdinsight-use-oozie.md): Use Sqoop action in an Oozie workflow.</span><span class="sxs-lookup"><span data-stu-id="cec42-125">[Use Oozie with HDInsight](hdinsight-use-oozie.md): Use Sqoop action in an Oozie workflow.</span></span>
* <span data-ttu-id="cec42-126">[Analyze flight delay data using HDInsight](hdinsight-analyze-flight-delay-data.md): Use Hive to analyze flight delay data, and then use Sqoop to export data to an Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="cec42-126">[Analyze flight delay data using HDInsight](hdinsight-analyze-flight-delay-data.md): Use Hive to analyze flight delay data, and then use Sqoop to export data to an Azure SQL database.</span></span>
* <span data-ttu-id="cec42-127">[Upload data to HDInsight](hdinsight-upload-data.md): Find other methods for uploading data to HDInsight/Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="cec42-127">[Upload data to HDInsight](hdinsight-upload-data.md): Find other methods for uploading data to HDInsight/Azure Blob storage.</span></span>

