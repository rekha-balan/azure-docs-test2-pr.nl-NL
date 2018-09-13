---
title: Use Apache Storm with Power BI | Microsoft Docs
description: Create a Power BI report using data from a C# topology running on an Apache Storm cluster in HDInsight.
services: hdinsight
documentationcenter: ''
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 36fe3b9c-5232-4464-8d75-95403b6da7a1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/01/2017
ms.author: larryfr
ms.openlocfilehash: 8592a5950b554c61897952671dfa04aad98c0888
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551042"
---
# <a name="use-power-bi-to-visualize-data-from-an-apache-storm-topology"></a><span data-ttu-id="39d51-103">Use Power BI to visualize data from an Apache Storm topology</span><span class="sxs-lookup"><span data-stu-id="39d51-103">Use Power BI to visualize data from an Apache Storm topology</span></span>

<span data-ttu-id="39d51-104">Power BI allows you to visually display data as reports.</span><span class="sxs-lookup"><span data-stu-id="39d51-104">Power BI allows you to visually display data as reports.</span></span> <span data-ttu-id="39d51-105">This document provides an example of how to use Apache Storm on HDInsight to generate data for Power BI.</span><span class="sxs-lookup"><span data-stu-id="39d51-105">This document provides an example of how to use Apache Storm on HDInsight to generate data for Power BI.</span></span>

> [!NOTE]
> <span data-ttu-id="39d51-106">While the steps in this document rely on a Windows development environment with Visual Studio, the compiled project can be submitted to either a Linux or Windows-based HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="39d51-106">While the steps in this document rely on a Windows development environment with Visual Studio, the compiled project can be submitted to either a Linux or Windows-based HDInsight cluster.</span></span> <span data-ttu-id="39d51-107">Only Linux-based clusters created after 10/28/2016 support SCP.NET topologies.</span><span class="sxs-lookup"><span data-stu-id="39d51-107">Only Linux-based clusters created after 10/28/2016 support SCP.NET topologies.</span></span>
>
> <span data-ttu-id="39d51-108">To use a C# topology with a Linux-based cluster, update the Microsoft.SCP.Net.SDK NuGet package used by your project to version 0.10.0.6 or higher.</span><span class="sxs-lookup"><span data-stu-id="39d51-108">To use a C# topology with a Linux-based cluster, update the Microsoft.SCP.Net.SDK NuGet package used by your project to version 0.10.0.6 or higher.</span></span> <span data-ttu-id="39d51-109">The version of the package must also match the major version of Storm installed on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="39d51-109">The version of the package must also match the major version of Storm installed on HDInsight.</span></span> <span data-ttu-id="39d51-110">For example, Storm on HDInsight versions 3.3 and 3.4 use Storm version 0.10.x, while HDInsight 3.5 uses Storm 1.0.x.</span><span class="sxs-lookup"><span data-stu-id="39d51-110">For example, Storm on HDInsight versions 3.3 and 3.4 use Storm version 0.10.x, while HDInsight 3.5 uses Storm 1.0.x.</span></span>
>
> <span data-ttu-id="39d51-111">C# topologies on Linux-based clusters must use .NET 4.5, and use Mono to run on the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="39d51-111">C# topologies on Linux-based clusters must use .NET 4.5, and use Mono to run on the HDInsight cluster.</span></span> <span data-ttu-id="39d51-112">Most things work.</span><span class="sxs-lookup"><span data-stu-id="39d51-112">Most things work.</span></span> <span data-ttu-id="39d51-113">However you should check the [Mono Compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) document for potential incompatibilities.</span><span class="sxs-lookup"><span data-stu-id="39d51-113">However you should check the [Mono Compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) document for potential incompatibilities.</span></span>
>
> <span data-ttu-id="39d51-114">For a Java version of this project, which works with Linux-based or Windows-based HDInsight, see [Process events from Azure Event Hubs with Storm on HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).</span><span class="sxs-lookup"><span data-stu-id="39d51-114">For a Java version of this project, which works with Linux-based or Windows-based HDInsight, see [Process events from Azure Event Hubs with Storm on HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="39d51-115">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="39d51-115">Prerequisites</span></span>

* <span data-ttu-id="39d51-116">An Azure Active Directory user with [Power BI](https://powerbi.com) access.</span><span class="sxs-lookup"><span data-stu-id="39d51-116">An Azure Active Directory user with [Power BI](https://powerbi.com) access.</span></span>
* <span data-ttu-id="39d51-117">An HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="39d51-117">An HDInsight cluster.</span></span> <span data-ttu-id="39d51-118">For more information, see [Get started with Storm on HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="39d51-118">For more information, see [Get started with Storm on HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="39d51-119">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="39d51-119">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="39d51-120">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span><span class="sxs-lookup"><span data-stu-id="39d51-120">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span></span>

* <span data-ttu-id="39d51-121">Visual Studio (one of the following versions)</span><span class="sxs-lookup"><span data-stu-id="39d51-121">Visual Studio (one of the following versions)</span></span>

  * <span data-ttu-id="39d51-122">Visual Studio 2012 with [update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span><span class="sxs-lookup"><span data-stu-id="39d51-122">Visual Studio 2012 with [update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span></span>
  * <span data-ttu-id="39d51-123">Visual Studio 2013 with [update 4](http://www.microsoft.com/download/details.aspx?id=44921) or [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?linkid=517284&clcid=0x409)</span><span class="sxs-lookup"><span data-stu-id="39d51-123">Visual Studio 2013 with [update 4](http://www.microsoft.com/download/details.aspx?id=44921) or [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?linkid=517284&clcid=0x409)</span></span>
  * [<span data-ttu-id="39d51-124">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="39d51-124">Visual Studio 2015</span></span>](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
  * <span data-ttu-id="39d51-125">Visual Studio 2017 (any edition)</span><span class="sxs-lookup"><span data-stu-id="39d51-125">Visual Studio 2017 (any edition)</span></span>

* <span data-ttu-id="39d51-126">The HDInsight Tools for Visual Studio: See [Get started using the HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) for information on installation information.</span><span class="sxs-lookup"><span data-stu-id="39d51-126">The HDInsight Tools for Visual Studio: See [Get started using the HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) for information on installation information.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="39d51-127">How it works</span><span class="sxs-lookup"><span data-stu-id="39d51-127">How it works</span></span>

<span data-ttu-id="39d51-128">This example contains a C# Storm topology that randomly generates Internet Information Services (IIS) log data.</span><span class="sxs-lookup"><span data-stu-id="39d51-128">This example contains a C# Storm topology that randomly generates Internet Information Services (IIS) log data.</span></span> <span data-ttu-id="39d51-129">This data is then written to a SQL Database, and from there it is used to generate reports in Power BI.</span><span class="sxs-lookup"><span data-stu-id="39d51-129">This data is then written to a SQL Database, and from there it is used to generate reports in Power BI.</span></span>

<span data-ttu-id="39d51-130">The following files implement the main functionality of this example:</span><span class="sxs-lookup"><span data-stu-id="39d51-130">The following files implement the main functionality of this example:</span></span>

* <span data-ttu-id="39d51-131">**SqlAzureBolt.cs**: Writes information produced in the Storm topology to SQL Database.</span><span class="sxs-lookup"><span data-stu-id="39d51-131">**SqlAzureBolt.cs**: Writes information produced in the Storm topology to SQL Database.</span></span>
* <span data-ttu-id="39d51-132">**IISLogsTable.sql**: The Transact-SQL statements used to generate the database that the data is stored in.</span><span class="sxs-lookup"><span data-stu-id="39d51-132">**IISLogsTable.sql**: The Transact-SQL statements used to generate the database that the data is stored in.</span></span>

> [!WARNING]
> <span data-ttu-id="39d51-133">Create the table in SQL Database before starting the topology on your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="39d51-133">Create the table in SQL Database before starting the topology on your HDInsight cluster.</span></span>

## <a name="download-the-example"></a><span data-ttu-id="39d51-134">Download the example</span><span class="sxs-lookup"><span data-stu-id="39d51-134">Download the example</span></span>

<span data-ttu-id="39d51-135">Download the [HDInsight C# Storm Power BI example](https://github.com/Azure-Samples/hdinsight-dotnet-storm-powerbi).</span><span class="sxs-lookup"><span data-stu-id="39d51-135">Download the [HDInsight C# Storm Power BI example](https://github.com/Azure-Samples/hdinsight-dotnet-storm-powerbi).</span></span> <span data-ttu-id="39d51-136">To download it, either fork/clone it using [git](http://git-scm.com/), or use the **Download** link to download a .zip of the archive.</span><span class="sxs-lookup"><span data-stu-id="39d51-136">To download it, either fork/clone it using [git](http://git-scm.com/), or use the **Download** link to download a .zip of the archive.</span></span>

## <a name="create-a-database"></a><span data-ttu-id="39d51-137">Create a database</span><span class="sxs-lookup"><span data-stu-id="39d51-137">Create a database</span></span>

1. <span data-ttu-id="39d51-138">To create a database, use the steps in the [SQL Database tutorial](../sql-database/sql-database-get-started.md) document.</span><span class="sxs-lookup"><span data-stu-id="39d51-138">To create a database, use the steps in the [SQL Database tutorial](../sql-database/sql-database-get-started.md) document.</span></span>

2. <span data-ttu-id="39d51-139">Connect to the database by following the steps in the [Connect to a SQL Database with Visual Studio](../sql-database/sql-database-connect-query.md) document.</span><span class="sxs-lookup"><span data-stu-id="39d51-139">Connect to the database by following the steps in the [Connect to a SQL Database with Visual Studio](../sql-database/sql-database-connect-query.md) document.</span></span>

3. <span data-ttu-id="39d51-140">In Object Explorer, right-click the database and select  **New Query**.</span><span class="sxs-lookup"><span data-stu-id="39d51-140">In Object Explorer, right-click the database and select  **New Query**.</span></span> <span data-ttu-id="39d51-141">Paste the contents of the **IISLogsTable.sql** file included in the downloaded project into the query window, and then use Ctrl + Shift + E to execute the query.</span><span class="sxs-lookup"><span data-stu-id="39d51-141">Paste the contents of the **IISLogsTable.sql** file included in the downloaded project into the query window, and then use Ctrl + Shift + E to execute the query.</span></span> <span data-ttu-id="39d51-142">You should receive a message that the commands completed successfully.</span><span class="sxs-lookup"><span data-stu-id="39d51-142">You should receive a message that the commands completed successfully.</span></span>

## <a name="configure-the-sample"></a><span data-ttu-id="39d51-143">Configure the sample</span><span class="sxs-lookup"><span data-stu-id="39d51-143">Configure the sample</span></span>

1. <span data-ttu-id="39d51-144">From the [Azure portal](https://portal.azure.com), select your SQL database.</span><span class="sxs-lookup"><span data-stu-id="39d51-144">From the [Azure portal](https://portal.azure.com), select your SQL database.</span></span> <span data-ttu-id="39d51-145">From the **Essentials** section of the SQL database blade, select **Show database connection strings**.</span><span class="sxs-lookup"><span data-stu-id="39d51-145">From the **Essentials** section of the SQL database blade, select **Show database connection strings**.</span></span> <span data-ttu-id="39d51-146">From the list that appears, copy the **ADO.NET (SQL authentication)** information.</span><span class="sxs-lookup"><span data-stu-id="39d51-146">From the list that appears, copy the **ADO.NET (SQL authentication)** information.</span></span>

2. <span data-ttu-id="39d51-147">Open the sample in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="39d51-147">Open the sample in Visual Studio.</span></span> <span data-ttu-id="39d51-148">From **Solution Explorer**, open the **App.config** file, and then find the following entry:</span><span class="sxs-lookup"><span data-stu-id="39d51-148">From **Solution Explorer**, open the **App.config** file, and then find the following entry:</span></span>

        <add key="SqlAzureConnectionString" value="##TOBEFILLED##" />

    <span data-ttu-id="39d51-149">Replace the **##TOBEFILLED##** value with the database connection string copied in the previous step.</span><span class="sxs-lookup"><span data-stu-id="39d51-149">Replace the **##TOBEFILLED##** value with the database connection string copied in the previous step.</span></span> <span data-ttu-id="39d51-150">Replace **{your\_username}** and **{your\_password}** with the username and password for the database.</span><span class="sxs-lookup"><span data-stu-id="39d51-150">Replace **{your\_username}** and **{your\_password}** with the username and password for the database.</span></span>

3. <span data-ttu-id="39d51-151">Save and close the files.</span><span class="sxs-lookup"><span data-stu-id="39d51-151">Save and close the files.</span></span>

## <a name="deploy-the-sample"></a><span data-ttu-id="39d51-152">Deploy the sample</span><span class="sxs-lookup"><span data-stu-id="39d51-152">Deploy the sample</span></span>

1. <span data-ttu-id="39d51-153">From **Solution Explorer**, right-click the **StormToSQL** project and select **Submit to Storm on HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="39d51-153">From **Solution Explorer**, right-click the **StormToSQL** project and select **Submit to Storm on HDInsight**.</span></span> <span data-ttu-id="39d51-154">Select the HDInsight cluster from the **Storm Cluster** dropdown dialog.</span><span class="sxs-lookup"><span data-stu-id="39d51-154">Select the HDInsight cluster from the **Storm Cluster** dropdown dialog.</span></span>

   > [!NOTE]
   > <span data-ttu-id="39d51-155">It may take a few seconds for the **Storm Cluster** dropdown to populate with server names.</span><span class="sxs-lookup"><span data-stu-id="39d51-155">It may take a few seconds for the **Storm Cluster** dropdown to populate with server names.</span></span>
   >
   > <span data-ttu-id="39d51-156">If prompted, enter the login credentials for your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="39d51-156">If prompted, enter the login credentials for your Azure subscription.</span></span> <span data-ttu-id="39d51-157">If you have more than one subscription, log in to the one that contains your Storm on HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="39d51-157">If you have more than one subscription, log in to the one that contains your Storm on HDInsight cluster.</span></span>

2. <span data-ttu-id="39d51-158">When the topology has been submitted, the __Topology Viewer__ appears.</span><span class="sxs-lookup"><span data-stu-id="39d51-158">When the topology has been submitted, the __Topology Viewer__ appears.</span></span> <span data-ttu-id="39d51-159">To view this topology, select the SqlAzureWriterTopology entry from the list.</span><span class="sxs-lookup"><span data-stu-id="39d51-159">To view this topology, select the SqlAzureWriterTopology entry from the list.</span></span>

    ![The topologies, with the topology selected](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-storm-power-bi-topology/topologyview.png)

    <span data-ttu-id="39d51-161">You can use this view to see information on the topology, or double-click an entry (such as the SqlAzureBolt) to see information specific to a component in the topology.</span><span class="sxs-lookup"><span data-stu-id="39d51-161">You can use this view to see information on the topology, or double-click an entry (such as the SqlAzureBolt) to see information specific to a component in the topology.</span></span>

3. <span data-ttu-id="39d51-162">After the topology has ran for a few minutes, return to the SQL query window you used to create the database.</span><span class="sxs-lookup"><span data-stu-id="39d51-162">After the topology has ran for a few minutes, return to the SQL query window you used to create the database.</span></span> <span data-ttu-id="39d51-163">Replace the existing statements with the following query:</span><span class="sxs-lookup"><span data-stu-id="39d51-163">Replace the existing statements with the following query:</span></span>

        select * from iislogs;

    <span data-ttu-id="39d51-164">Use Ctrl + Shift + E to execute the query, and you should receive results similar to the following:</span><span class="sxs-lookup"><span data-stu-id="39d51-164">Use Ctrl + Shift + E to execute the query, and you should receive results similar to the following:</span></span>

        1    2016-05-27 17:57:14.797    255.255.255.255    /bar    GET    200
        2    2016-05-27 17:57:14.843    127.0.0.1    /spam/eggs    POST    500
        3    2016-05-27 17:57:14.850    123.123.123.123    /eggs    DELETE    200
        4    2016-05-27 17:57:14.853    127.0.0.1    /foo    POST    404
        5    2016-05-27 17:57:14.853    10.9.8.7    /bar    GET    200
        6    2016-05-27 17:57:14.857    192.168.1.1    /spam    DELETE    200

    <span data-ttu-id="39d51-165">This data has been written from the Storm topology.</span><span class="sxs-lookup"><span data-stu-id="39d51-165">This data has been written from the Storm topology.</span></span>

## <a name="create-a-report"></a><span data-ttu-id="39d51-166">Create a report</span><span class="sxs-lookup"><span data-stu-id="39d51-166">Create a report</span></span>

1. <span data-ttu-id="39d51-167">Connect to the [Azure SQL Database connector](https://app.powerbi.com/getdata/bigdata/azure-sql-database-with-live-connect) for Power BI.</span><span class="sxs-lookup"><span data-stu-id="39d51-167">Connect to the [Azure SQL Database connector](https://app.powerbi.com/getdata/bigdata/azure-sql-database-with-live-connect) for Power BI.</span></span>

2. <span data-ttu-id="39d51-168">Within **Databases**, select **Get**.</span><span class="sxs-lookup"><span data-stu-id="39d51-168">Within **Databases**, select **Get**.</span></span>

3. <span data-ttu-id="39d51-169">Select **Azure SQL Database**, and then select **Connect**.</span><span class="sxs-lookup"><span data-stu-id="39d51-169">Select **Azure SQL Database**, and then select **Connect**.</span></span>

4. <span data-ttu-id="39d51-170">Enter the information to connect to your Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="39d51-170">Enter the information to connect to your Azure SQL Database.</span></span> <span data-ttu-id="39d51-171">You can find this information by visiting the [Azure portal](https://portal.azure.com) and selecting your SQL database.</span><span class="sxs-lookup"><span data-stu-id="39d51-171">You can find this information by visiting the [Azure portal](https://portal.azure.com) and selecting your SQL database.</span></span>

   > [!NOTE]
   > <span data-ttu-id="39d51-172">You can also set the refresh interval and custom filters by using **Enable Advanced Options** from the connect dialog.</span><span class="sxs-lookup"><span data-stu-id="39d51-172">You can also set the refresh interval and custom filters by using **Enable Advanced Options** from the connect dialog.</span></span>

5. <span data-ttu-id="39d51-173">After you've connected, you will see a new dataset with the same name as the database you connected to.</span><span class="sxs-lookup"><span data-stu-id="39d51-173">After you've connected, you will see a new dataset with the same name as the database you connected to.</span></span> <span data-ttu-id="39d51-174">Select the dataset to begin designing a report.</span><span class="sxs-lookup"><span data-stu-id="39d51-174">Select the dataset to begin designing a report.</span></span>

6. <span data-ttu-id="39d51-175">From **Fields**, expand the **IISLOGS** entry.</span><span class="sxs-lookup"><span data-stu-id="39d51-175">From **Fields**, expand the **IISLOGS** entry.</span></span> <span data-ttu-id="39d51-176">Select the checkbox for **URISTEM**.</span><span class="sxs-lookup"><span data-stu-id="39d51-176">Select the checkbox for **URISTEM**.</span></span> <span data-ttu-id="39d51-177">This creates a report that lists the URI stems (/foo, /bar, etc.) logged in the database.</span><span class="sxs-lookup"><span data-stu-id="39d51-177">This creates a report that lists the URI stems (/foo, /bar, etc.) logged in the database.</span></span>

    ![Creating a report](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-storm-power-bi-topology/createreport.png)

7. <span data-ttu-id="39d51-179">Next, drag **METHOD** to the report.</span><span class="sxs-lookup"><span data-stu-id="39d51-179">Next, drag **METHOD** to the report.</span></span> <span data-ttu-id="39d51-180">The report will update to list the stems and the corresponding HTTP method used for the HTTP request.</span><span class="sxs-lookup"><span data-stu-id="39d51-180">The report will update to list the stems and the corresponding HTTP method used for the HTTP request.</span></span>

    ![adding the method data](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-storm-power-bi-topology/uristemandmethod.png)

8. <span data-ttu-id="39d51-182">From the **Visualizations** column, select the **Fields** icon, and then select the down arrow next to **METHOD** in the **Values** section.</span><span class="sxs-lookup"><span data-stu-id="39d51-182">From the **Visualizations** column, select the **Fields** icon, and then select the down arrow next to **METHOD** in the **Values** section.</span></span> <span data-ttu-id="39d51-183">From the list that appears, select **Count**.</span><span class="sxs-lookup"><span data-stu-id="39d51-183">From the list that appears, select **Count**.</span></span> <span data-ttu-id="39d51-184">This changes the report to list a count of how many times a specific URI has been accessed.</span><span class="sxs-lookup"><span data-stu-id="39d51-184">This changes the report to list a count of how many times a specific URI has been accessed.</span></span>

    ![Changing to a count of methods](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-storm-power-bi-topology/count.png)

9. <span data-ttu-id="39d51-186">Next, select the **Stacked column chart** to change how the information is displayed.</span><span class="sxs-lookup"><span data-stu-id="39d51-186">Next, select the **Stacked column chart** to change how the information is displayed.</span></span>

    ![Changing to a stacked chart](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-storm-power-bi-topology/stackedcolumn.png)

10. <span data-ttu-id="39d51-188">To save the report, select **Save** and enter a name for the report.</span><span class="sxs-lookup"><span data-stu-id="39d51-188">To save the report, select **Save** and enter a name for the report.</span></span>

## <a name="stop-the-topology"></a><span data-ttu-id="39d51-189">Stop the topology</span><span class="sxs-lookup"><span data-stu-id="39d51-189">Stop the topology</span></span>

<span data-ttu-id="39d51-190">The topology continues to run until you stop it or delete the Storm on HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="39d51-190">The topology continues to run until you stop it or delete the Storm on HDInsight cluster.</span></span> <span data-ttu-id="39d51-191">Perform the following steps to stop the topology.</span><span class="sxs-lookup"><span data-stu-id="39d51-191">Perform the following steps to stop the topology.</span></span>

1. <span data-ttu-id="39d51-192">In Visual Studio, return to the topology viewer and select the topology.</span><span class="sxs-lookup"><span data-stu-id="39d51-192">In Visual Studio, return to the topology viewer and select the topology.</span></span>

2. <span data-ttu-id="39d51-193">Select the **Kill** button to stop the topology.</span><span class="sxs-lookup"><span data-stu-id="39d51-193">Select the **Kill** button to stop the topology.</span></span>

    ![Kill button on the topology summary](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-storm-power-bi-topology/killtopology.png)

## <a name="delete-your-cluster"></a><span data-ttu-id="39d51-195">Delete your cluster</span><span class="sxs-lookup"><span data-stu-id="39d51-195">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="39d51-196">Next steps</span><span class="sxs-lookup"><span data-stu-id="39d51-196">Next steps</span></span>

<span data-ttu-id="39d51-197">In this document, you learned how to send data from a Storm topology to SQL Database, then visualize the data using Power BI.</span><span class="sxs-lookup"><span data-stu-id="39d51-197">In this document, you learned how to send data from a Storm topology to SQL Database, then visualize the data using Power BI.</span></span> <span data-ttu-id="39d51-198">For information on how to work with other Azure technologies using Storm on HDInsight, see the following:</span><span class="sxs-lookup"><span data-stu-id="39d51-198">For information on how to work with other Azure technologies using Storm on HDInsight, see the following:</span></span>

* [<span data-ttu-id="39d51-199">Example topologies for Storm on HDInsight</span><span class="sxs-lookup"><span data-stu-id="39d51-199">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)






