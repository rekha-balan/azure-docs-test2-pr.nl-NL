---
title: Learn to use Data Lake (HDInsight) Tools for Visual Studio | Microsoft Docs
description: Learn how to install and use Data Lake (HDInsight) Tools for Visual Studio to connect to a Hadoop cluster and run a Hive query.
keywords: hadoop tools,hive query,visual studio
services: HDInsight
documentationcenter: ''
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: ce9c572a-1e98-46bf-9581-13a9767f1fa5
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/07/2017
ms.author: jgao
ms.openlocfilehash: 9ab1bab6610bf055428a324223bc722230116fe8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554578"
---
# <a name="get-started-using-azure-data-lake-hdinsight-tools-for-visual-studio-to-run-a-hive-query"></a><span data-ttu-id="82050-104">Get started using Azure Data Lake (HDInsight) Tools for Visual Studio to run a Hive query</span><span class="sxs-lookup"><span data-stu-id="82050-104">Get started using Azure Data Lake (HDInsight) Tools for Visual Studio to run a Hive query</span></span>
<span data-ttu-id="82050-105">Learn how to use Data Lake (HDInsight) Tools for Visual Studio to connect to HDInsight clusters and submit Hive queries.</span><span class="sxs-lookup"><span data-stu-id="82050-105">Learn how to use Data Lake (HDInsight) Tools for Visual Studio to connect to HDInsight clusters and submit Hive queries.</span></span> <span data-ttu-id="82050-106">For more information about using HDInsight, see [Introduction to HDInsight][hdinsight.introduction] and [Get started with HDInsight][hdinsight.get.started].</span><span class="sxs-lookup"><span data-stu-id="82050-106">For more information about using HDInsight, see [Introduction to HDInsight][hdinsight.introduction] and [Get started with HDInsight][hdinsight.get.started].</span></span> <span data-ttu-id="82050-107">For more information about connecting to a Storm cluster, see [Develop C# topologies for Apache Storm on HDInsight using Visual Studio][hdinsight.storm.visual.studio.tools].</span><span class="sxs-lookup"><span data-stu-id="82050-107">For more information about connecting to a Storm cluster, see [Develop C# topologies for Apache Storm on HDInsight using Visual Studio][hdinsight.storm.visual.studio.tools].</span></span>

<span data-ttu-id="82050-108">Data Lake Tools for Visual Studio can be used to access both Data Lake Analytics and HDInsight.</span><span class="sxs-lookup"><span data-stu-id="82050-108">Data Lake Tools for Visual Studio can be used to access both Data Lake Analytics and HDInsight.</span></span>  <span data-ttu-id="82050-109">For the information about Data Lake Tools, see [Tutorial: develop U-SQL scripts using Data Lake Tools for Visual Studio](../data-lake-analytics/data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="82050-109">For the information about Data Lake Tools, see [Tutorial: develop U-SQL scripts using Data Lake Tools for Visual Studio](../data-lake-analytics/data-lake-analytics-data-lake-tools-get-started.md).</span></span>

<span data-ttu-id="82050-110">**Prerequisites**</span><span class="sxs-lookup"><span data-stu-id="82050-110">**Prerequisites**</span></span>

<span data-ttu-id="82050-111">To complete this tutorial and use the Data Lake Tools in Visual Studio, you'll need the following:</span><span class="sxs-lookup"><span data-stu-id="82050-111">To complete this tutorial and use the Data Lake Tools in Visual Studio, you'll need the following:</span></span>

* <span data-ttu-id="82050-112">An Azure HDInsight cluster: To create one, see [Get started using Linux-based HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="82050-112">An Azure HDInsight cluster: To create one, see [Get started using Linux-based HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md)</span></span>
* <span data-ttu-id="82050-113">A workstation with the following software:</span><span class="sxs-lookup"><span data-stu-id="82050-113">A workstation with the following software:</span></span>
  
  * <span data-ttu-id="82050-114">Windows 10, Windows 8.1, Windows 8, or Windows 7.</span><span class="sxs-lookup"><span data-stu-id="82050-114">Windows 10, Windows 8.1, Windows 8, or Windows 7.</span></span>
  * <span data-ttu-id="82050-115">Visual Studio 2013/2015/2017.</span><span class="sxs-lookup"><span data-stu-id="82050-115">Visual Studio 2013/2015/2017.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="82050-116">Currently, the Data Lake Tools for Visual Studio only come with the English version.</span><span class="sxs-lookup"><span data-stu-id="82050-116">Currently, the Data Lake Tools for Visual Studio only come with the English version.</span></span>
    > 
    > 

## <a name="install-data-lake-tools-for-visual-studio"></a><span data-ttu-id="82050-117">Install Data Lake Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="82050-117">Install Data Lake Tools for Visual Studio</span></span>

<span data-ttu-id="82050-118">Data Lake Tools is installed by default for Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="82050-118">Data Lake Tools is installed by default for Visual Studio 2017.</span></span> <span data-ttu-id="82050-119">For older versions, you can install it using the [Web Platform Installer](https://www.microsoft.com/web/downloads/).</span><span class="sxs-lookup"><span data-stu-id="82050-119">For older versions, you can install it using the [Web Platform Installer](https://www.microsoft.com/web/downloads/).</span></span> <span data-ttu-id="82050-120">You must choose the one that matches your version of Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="82050-120">You must choose the one that matches your version of Visual Studio.</span></span> <span data-ttu-id="82050-121">If you don't have Visual Studio installed, you can install the latest Visual Studio Community and Azure SDK using the [Web Platform Installer](https://www.microsoft.com/web/downloads/):</span><span class="sxs-lookup"><span data-stu-id="82050-121">If you don't have Visual Studio installed, you can install the latest Visual Studio Community and Azure SDK using the [Web Platform Installer](https://www.microsoft.com/web/downloads/):</span></span>

![Data Lake Tools for Visual Studio Web Platform installer.][1]

## <a name="connect-to-azure-subscriptions"></a><span data-ttu-id="82050-123">Connect to Azure subscriptions</span><span class="sxs-lookup"><span data-stu-id="82050-123">Connect to Azure subscriptions</span></span>
<span data-ttu-id="82050-124">Data Lake Tools for Visual Studio allows you to connect to your HDInsight clusters, perform some basic management operations, and run Hive queries.</span><span class="sxs-lookup"><span data-stu-id="82050-124">Data Lake Tools for Visual Studio allows you to connect to your HDInsight clusters, perform some basic management operations, and run Hive queries.</span></span>

> [!NOTE]
> <span data-ttu-id="82050-125">For information on connecting to a generic Hadoop cluster, see [Write and submit Hive queries using Visual Studio](http://blogs.msdn.com/b/xiaoyong/archive/2015/05/04/how-to-write-and-submit-hive-queries-using-visual-studio.aspx).</span><span class="sxs-lookup"><span data-stu-id="82050-125">For information on connecting to a generic Hadoop cluster, see [Write and submit Hive queries using Visual Studio](http://blogs.msdn.com/b/xiaoyong/archive/2015/05/04/how-to-write-and-submit-hive-queries-using-visual-studio.aspx).</span></span>
> 
> 

<span data-ttu-id="82050-126">**To connect to your Azure subscription**</span><span class="sxs-lookup"><span data-stu-id="82050-126">**To connect to your Azure subscription**</span></span>

1. <span data-ttu-id="82050-127">Open Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="82050-127">Open Visual Studio.</span></span>
2. <span data-ttu-id="82050-128">From the **View** menu, click **Server Explorer** to open the Server Explorer window.</span><span class="sxs-lookup"><span data-stu-id="82050-128">From the **View** menu, click **Server Explorer** to open the Server Explorer window.</span></span>
3. <span data-ttu-id="82050-129">Expand **Azure**, and then expand **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="82050-129">Expand **Azure**, and then expand **HDInsight**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="82050-130">Notice the **HDInsight Task List** window should be open.</span><span class="sxs-lookup"><span data-stu-id="82050-130">Notice the **HDInsight Task List** window should be open.</span></span> <span data-ttu-id="82050-131">If you don't see it, click **Other Windows** from the **View** menu, and then click **HDInsight Task List Window**.</span><span class="sxs-lookup"><span data-stu-id="82050-131">If you don't see it, click **Other Windows** from the **View** menu, and then click **HDInsight Task List Window**.</span></span>  
   > 
   > 
4. <span data-ttu-id="82050-132">Enter your Azure subscription credentials, and then click **Sign In**.</span><span class="sxs-lookup"><span data-stu-id="82050-132">Enter your Azure subscription credentials, and then click **Sign In**.</span></span> <span data-ttu-id="82050-133">This is only required if you have never connected to the Azure subscription from Visual Studio on this workstation.</span><span class="sxs-lookup"><span data-stu-id="82050-133">This is only required if you have never connected to the Azure subscription from Visual Studio on this workstation.</span></span>
5. <span data-ttu-id="82050-134">In Server Explorer, you'll see a list of existing HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="82050-134">In Server Explorer, you'll see a list of existing HDInsight clusters.</span></span> <span data-ttu-id="82050-135">If you don't have any clusters, you can create one by using the Azure portal, Azure PowerShell, or the HDInsight SDK.</span><span class="sxs-lookup"><span data-stu-id="82050-135">If you don't have any clusters, you can create one by using the Azure portal, Azure PowerShell, or the HDInsight SDK.</span></span> <span data-ttu-id="82050-136">For more information, see [Create HDInsight clusters][hdinsight-create-clusters].</span><span class="sxs-lookup"><span data-stu-id="82050-136">For more information, see [Create HDInsight clusters][hdinsight-create-clusters].</span></span>
   
   ![Data Lake Tools for Visual Studio Server Explorer cluster list][5]
6. <span data-ttu-id="82050-138">Expand an HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="82050-138">Expand an HDInsight cluster.</span></span> <span data-ttu-id="82050-139">You'll see **Hive Databases**, a default storage account, linked storage accounts, and **Hadoop Service log**.</span><span class="sxs-lookup"><span data-stu-id="82050-139">You'll see **Hive Databases**, a default storage account, linked storage accounts, and **Hadoop Service log**.</span></span> <span data-ttu-id="82050-140">You can further expand the entities.</span><span class="sxs-lookup"><span data-stu-id="82050-140">You can further expand the entities.</span></span>

<span data-ttu-id="82050-141">After you've connected to your Azure subscription, you'll be able to do the following:</span><span class="sxs-lookup"><span data-stu-id="82050-141">After you've connected to your Azure subscription, you'll be able to do the following:</span></span>

<span data-ttu-id="82050-142">**To connect to the Azure portal from Visual Studio**</span><span class="sxs-lookup"><span data-stu-id="82050-142">**To connect to the Azure portal from Visual Studio**</span></span>

* <span data-ttu-id="82050-143">From Server Explorer, expand **Azure** > **HDInsight**, right-click an HDInsight cluster, and then click **Manage Cluster in Azure portal**.</span><span class="sxs-lookup"><span data-stu-id="82050-143">From Server Explorer, expand **Azure** > **HDInsight**, right-click an HDInsight cluster, and then click **Manage Cluster in Azure portal**.</span></span>

<span data-ttu-id="82050-144">**To ask questions and provide feedback from Visual Studio**</span><span class="sxs-lookup"><span data-stu-id="82050-144">**To ask questions and provide feedback from Visual Studio**</span></span>

* <span data-ttu-id="82050-145">From the **Tools** menu, click **HDInsight**, and then click **MSDN Forum** to ask questions, or click **Give Feedback**.</span><span class="sxs-lookup"><span data-stu-id="82050-145">From the **Tools** menu, click **HDInsight**, and then click **MSDN Forum** to ask questions, or click **Give Feedback**.</span></span>

## <a name="navigate-the-linked-resources"></a><span data-ttu-id="82050-146">Navigate the linked resources</span><span class="sxs-lookup"><span data-stu-id="82050-146">Navigate the linked resources</span></span>
<span data-ttu-id="82050-147">From Server Explorer, you can see the default storage account and any linked storage accounts.</span><span class="sxs-lookup"><span data-stu-id="82050-147">From Server Explorer, you can see the default storage account and any linked storage accounts.</span></span> <span data-ttu-id="82050-148">If you expand the default storage account, you can see the containers on the storage account.</span><span class="sxs-lookup"><span data-stu-id="82050-148">If you expand the default storage account, you can see the containers on the storage account.</span></span> <span data-ttu-id="82050-149">The default storage account and the default container are marked.</span><span class="sxs-lookup"><span data-stu-id="82050-149">The default storage account and the default container are marked.</span></span> <span data-ttu-id="82050-150">You can also right-click any of the containers to view the contents.</span><span class="sxs-lookup"><span data-stu-id="82050-150">You can also right-click any of the containers to view the contents.</span></span>

![Data Lake Tools for Visual Studio server explorer cluster list][2]

<span data-ttu-id="82050-152">After opening a container, you can use the following buttons to upload, delete, and download blobs:</span><span class="sxs-lookup"><span data-stu-id="82050-152">After opening a container, you can use the following buttons to upload, delete, and download blobs:</span></span>

![Data Lake Tools for Visual Studio server explorer blob operations](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.blob.operations.png)

## <a name="run-a-hive-query"></a><span data-ttu-id="82050-154">Run a Hive query</span><span class="sxs-lookup"><span data-stu-id="82050-154">Run a Hive query</span></span>
<span data-ttu-id="82050-155">[Apache Hive][apache.hive] is a data warehouse infrastructure built on Hadoop for providing data summarization, queries, and analysis.</span><span class="sxs-lookup"><span data-stu-id="82050-155">[Apache Hive][apache.hive] is a data warehouse infrastructure built on Hadoop for providing data summarization, queries, and analysis.</span></span> <span data-ttu-id="82050-156">Data Lake Tools for Visual Studio supports running Hive queries from Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="82050-156">Data Lake Tools for Visual Studio supports running Hive queries from Visual Studio.</span></span> <span data-ttu-id="82050-157">For more information about Hive, see [Use Hive with HDInsight][hdinsight.hive].</span><span class="sxs-lookup"><span data-stu-id="82050-157">For more information about Hive, see [Use Hive with HDInsight][hdinsight.hive].</span></span>

<span data-ttu-id="82050-158">It is time consuming to test Hive script against an HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="82050-158">It is time consuming to test Hive script against an HDInsight cluster.</span></span> <span data-ttu-id="82050-159">It could take several minutes or more.</span><span class="sxs-lookup"><span data-stu-id="82050-159">It could take several minutes or more.</span></span> <span data-ttu-id="82050-160">Data Lake Tools for Visual Studio is capable of validating Hive script locally without connecting to a live cluster.</span><span class="sxs-lookup"><span data-stu-id="82050-160">Data Lake Tools for Visual Studio is capable of validating Hive script locally without connecting to a live cluster.</span></span>

<span data-ttu-id="82050-161">Data Lake Tools for Visual Studio also enables users to see what’s inside the Hive job by collecting and surfacing the YARN logs of certain Hive jobs.</span><span class="sxs-lookup"><span data-stu-id="82050-161">Data Lake Tools for Visual Studio also enables users to see what’s inside the Hive job by collecting and surfacing the YARN logs of certain Hive jobs.</span></span>

### <a name="view-the-hivesampletable"></a><span data-ttu-id="82050-162">View the **hivesampletable**</span><span class="sxs-lookup"><span data-stu-id="82050-162">View the **hivesampletable**</span></span>
<span data-ttu-id="82050-163">All HDInsight clusters come with a sample Hive table called *hivesampletable*.</span><span class="sxs-lookup"><span data-stu-id="82050-163">All HDInsight clusters come with a sample Hive table called *hivesampletable*.</span></span> <span data-ttu-id="82050-164">We'll use this table to show you how to list Hive tables, view the table schemas, and list the rows in the Hive table.</span><span class="sxs-lookup"><span data-stu-id="82050-164">We'll use this table to show you how to list Hive tables, view the table schemas, and list the rows in the Hive table.</span></span>

<span data-ttu-id="82050-165">**To list Hive tables and view Hive table schema**</span><span class="sxs-lookup"><span data-stu-id="82050-165">**To list Hive tables and view Hive table schema**</span></span>

1. <span data-ttu-id="82050-166">From **Server Explorer**, expand **Azure** > **HDInsight** > the cluster of your choice > **Hive Databases** > **Default** > **hivesampletable** to see the table schema.</span><span class="sxs-lookup"><span data-stu-id="82050-166">From **Server Explorer**, expand **Azure** > **HDInsight** > the cluster of your choice > **Hive Databases** > **Default** > **hivesampletable** to see the table schema.</span></span>
2. <span data-ttu-id="82050-167">Right-click **hivesampletable**, and then click **View Top 100 Rows** to list the rows.</span><span class="sxs-lookup"><span data-stu-id="82050-167">Right-click **hivesampletable**, and then click **View Top 100 Rows** to list the rows.</span></span> <span data-ttu-id="82050-168">It is equivalent to running the following Hive query using Hive ODBC driver:</span><span class="sxs-lookup"><span data-stu-id="82050-168">It is equivalent to running the following Hive query using Hive ODBC driver:</span></span>
   
     <span data-ttu-id="82050-169">SELECT \* FROM hivesampletable LIMIT 100</span><span class="sxs-lookup"><span data-stu-id="82050-169">SELECT \* FROM hivesampletable LIMIT 100</span></span>
   
   <span data-ttu-id="82050-170">You can customize the row count.</span><span class="sxs-lookup"><span data-stu-id="82050-170">You can customize the row count.</span></span>
   
   ![Data Lake Tools: HDInsight Hive Visual Studio schema query][6]

### <a name="create-hive-tables"></a><span data-ttu-id="82050-172">Create Hive tables</span><span class="sxs-lookup"><span data-stu-id="82050-172">Create Hive tables</span></span>
<span data-ttu-id="82050-173">You can use the GUI to create a Hive table or use Hive queries.</span><span class="sxs-lookup"><span data-stu-id="82050-173">You can use the GUI to create a Hive table or use Hive queries.</span></span> <span data-ttu-id="82050-174">For information about using Hive queries, see [Run Hive queries](#run.queries).</span><span class="sxs-lookup"><span data-stu-id="82050-174">For information about using Hive queries, see [Run Hive queries](#run.queries).</span></span>

<span data-ttu-id="82050-175">**To create a Hive table**</span><span class="sxs-lookup"><span data-stu-id="82050-175">**To create a Hive table**</span></span>

1. <span data-ttu-id="82050-176">From **Server Explorer**, expand **Azure** > **HDInsight Clusters** an HDInsight cluster > **Hive Databases**, then right-click **default**, and click **Create Table**.</span><span class="sxs-lookup"><span data-stu-id="82050-176">From **Server Explorer**, expand **Azure** > **HDInsight Clusters** an HDInsight cluster > **Hive Databases**, then right-click **default**, and click **Create Table**.</span></span>
2. <span data-ttu-id="82050-177">Configure the table.</span><span class="sxs-lookup"><span data-stu-id="82050-177">Configure the table.</span></span>
3. <span data-ttu-id="82050-178">Click **Create Table** to submit the job to create the new Hive table.</span><span class="sxs-lookup"><span data-stu-id="82050-178">Click **Create Table** to submit the job to create the new Hive table.</span></span>
   
    ![Data Lake Tools: HDInsight Visual Studio Tools create hive table][7]

### <a name="run.queries"></a><span data-ttu-id="82050-180">Validate and run Hive queries</span><span class="sxs-lookup"><span data-stu-id="82050-180">Validate and run Hive queries</span></span>
<span data-ttu-id="82050-181">There are two ways to create and run Hive queries:</span><span class="sxs-lookup"><span data-stu-id="82050-181">There are two ways to create and run Hive queries:</span></span>

* <span data-ttu-id="82050-182">Create ad-hoc queries</span><span class="sxs-lookup"><span data-stu-id="82050-182">Create ad-hoc queries</span></span>
* <span data-ttu-id="82050-183">Create a Hive application</span><span class="sxs-lookup"><span data-stu-id="82050-183">Create a Hive application</span></span>

<span data-ttu-id="82050-184">**To create, validate, and run ad-hoc queries**</span><span class="sxs-lookup"><span data-stu-id="82050-184">**To create, validate, and run ad-hoc queries**</span></span>

1. <span data-ttu-id="82050-185">From **Server Explorer**, expand **Azure**, and then expand **HDInsight Clusters**.</span><span class="sxs-lookup"><span data-stu-id="82050-185">From **Server Explorer**, expand **Azure**, and then expand **HDInsight Clusters**.</span></span>
2. <span data-ttu-id="82050-186">Right-click the cluster where you want to run the query, and then click **Write a Hive Query**.</span><span class="sxs-lookup"><span data-stu-id="82050-186">Right-click the cluster where you want to run the query, and then click **Write a Hive Query**.</span></span>
3. <span data-ttu-id="82050-187">Enter the Hive queries.</span><span class="sxs-lookup"><span data-stu-id="82050-187">Enter the Hive queries.</span></span> <span data-ttu-id="82050-188">Notice the Hive editor supports IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="82050-188">Notice the Hive editor supports IntelliSense.</span></span> <span data-ttu-id="82050-189">Data Lake Tools for Visual Studio supports loading the remote metadata when you are editing your Hive script.</span><span class="sxs-lookup"><span data-stu-id="82050-189">Data Lake Tools for Visual Studio supports loading the remote metadata when you are editing your Hive script.</span></span> <span data-ttu-id="82050-190">For example, when you type "SELECT \* FROM", the IntelliSense lists all the suggested table names.</span><span class="sxs-lookup"><span data-stu-id="82050-190">For example, when you type "SELECT \* FROM", the IntelliSense lists all the suggested table names.</span></span> <span data-ttu-id="82050-191">When a table name is specified, the column names are listed by the IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="82050-191">When a table name is specified, the column names are listed by the IntelliSense.</span></span> <span data-ttu-id="82050-192">The tools support almost all Hive DML statements, subqueries, and the built-in UDFs.</span><span class="sxs-lookup"><span data-stu-id="82050-192">The tools support almost all Hive DML statements, subqueries, and the built-in UDFs.</span></span>
   
    ![Data Lake Tools: HDInsight Visual Studio Tools IntelliSense][13]
   
    ![Data Lake Tools: HDInsight Visual Studio Tools IntelliSense][14]
   
   > [!NOTE]
   > <span data-ttu-id="82050-195">Only the metadata of the clusters that is selected in HDInsight Toolbar will be suggested.</span><span class="sxs-lookup"><span data-stu-id="82050-195">Only the metadata of the clusters that is selected in HDInsight Toolbar will be suggested.</span></span>
   > 
   > 
4. <span data-ttu-id="82050-196">(Optional): Click **Validate Script** to check the script syntax errors.</span><span class="sxs-lookup"><span data-stu-id="82050-196">(Optional): Click **Validate Script** to check the script syntax errors.</span></span>
   
    ![Data Lake Tools: Data Lake Tools for Visual Studio local validation][10]
5. <span data-ttu-id="82050-198">Click **Submit** or **Submit (Advanced)**.</span><span class="sxs-lookup"><span data-stu-id="82050-198">Click **Submit** or **Submit (Advanced)**.</span></span> <span data-ttu-id="82050-199">With the advanced submit option, you'll configure **Job Name**, **Arguments**, **Additional Configurations**, and **Status Directory** for the script:</span><span class="sxs-lookup"><span data-stu-id="82050-199">With the advanced submit option, you'll configure **Job Name**, **Arguments**, **Additional Configurations**, and **Status Directory** for the script:</span></span>
   
    ![HDInsight Hadoop hive query][9]
   
    <span data-ttu-id="82050-201">After you submit the job, you see a **Hive Job Summary** window.</span><span class="sxs-lookup"><span data-stu-id="82050-201">After you submit the job, you see a **Hive Job Summary** window.</span></span>
   
    ![Summary of an HDInsight Hadoop Hive query][8]
6. <span data-ttu-id="82050-203">Use the **Refresh** button to update the status until the job status changes to **Completed**.</span><span class="sxs-lookup"><span data-stu-id="82050-203">Use the **Refresh** button to update the status until the job status changes to **Completed**.</span></span>
7. <span data-ttu-id="82050-204">Click the links at the bottom to see the following: **Job Query**, **Job Output**, **Job log**, or **Yarn log**.</span><span class="sxs-lookup"><span data-stu-id="82050-204">Click the links at the bottom to see the following: **Job Query**, **Job Output**, **Job log**, or **Yarn log**.</span></span>

<span data-ttu-id="82050-205">**To create and run a Hive solution**</span><span class="sxs-lookup"><span data-stu-id="82050-205">**To create and run a Hive solution**</span></span>

1. <span data-ttu-id="82050-206">From the **FILE** menu, click **New**, and then click **Project**.</span><span class="sxs-lookup"><span data-stu-id="82050-206">From the **FILE** menu, click **New**, and then click **Project**.</span></span>
2. <span data-ttu-id="82050-207">Select **HDInsight** from the left pane, select **Hive Application** in the middle pane, enter the properties, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="82050-207">Select **HDInsight** from the left pane, select **Hive Application** in the middle pane, enter the properties, and then click **OK**.</span></span>
   
    ![Data Lake Tools: HDInsight Visual Studio Tools new hive project][11]
3. <span data-ttu-id="82050-209">From **Solution Explorer**, double-click **Script.hql** to open it.</span><span class="sxs-lookup"><span data-stu-id="82050-209">From **Solution Explorer**, double-click **Script.hql** to open it.</span></span>
4. <span data-ttu-id="82050-210">To validate the Hive script, you can click the **Validate Script** button, or right-click the script in the Hive editor, and then click **Validate Script** from the context menu.</span><span class="sxs-lookup"><span data-stu-id="82050-210">To validate the Hive script, you can click the **Validate Script** button, or right-click the script in the Hive editor, and then click **Validate Script** from the context menu.</span></span>

### <a name="view-hive-jobs"></a><span data-ttu-id="82050-211">View Hive jobs</span><span class="sxs-lookup"><span data-stu-id="82050-211">View Hive jobs</span></span>
<span data-ttu-id="82050-212">You can view job queries, job output, job logs, and Yarn logs for Hive jobs.</span><span class="sxs-lookup"><span data-stu-id="82050-212">You can view job queries, job output, job logs, and Yarn logs for Hive jobs.</span></span> <span data-ttu-id="82050-213">For more information, see the previous screenshot.</span><span class="sxs-lookup"><span data-stu-id="82050-213">For more information, see the previous screenshot.</span></span>

<span data-ttu-id="82050-214">The most recent release of the tools allows you to see what’s inside your Hive jobs by collecting and surfacing  YARN logs.</span><span class="sxs-lookup"><span data-stu-id="82050-214">The most recent release of the tools allows you to see what’s inside your Hive jobs by collecting and surfacing  YARN logs.</span></span> <span data-ttu-id="82050-215">A YARN log can help you investigating performance issues.</span><span class="sxs-lookup"><span data-stu-id="82050-215">A YARN log can help you investigating performance issues.</span></span> <span data-ttu-id="82050-216">For more information about how HDInsight collects YARN logs, see [Access HDInsight Application Logs Programmatically][hdinsight.access.application.logs].</span><span class="sxs-lookup"><span data-stu-id="82050-216">For more information about how HDInsight collects YARN logs, see [Access HDInsight Application Logs Programmatically][hdinsight.access.application.logs].</span></span>

<span data-ttu-id="82050-217">**To view Hive jobs**</span><span class="sxs-lookup"><span data-stu-id="82050-217">**To view Hive jobs**</span></span>

1. <span data-ttu-id="82050-218">From **Server Explorer**, expand **Azure**, and then expand **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="82050-218">From **Server Explorer**, expand **Azure**, and then expand **HDInsight**.</span></span>
2. <span data-ttu-id="82050-219">Right-click an HDInsight cluster, and then click **View Jobs**.</span><span class="sxs-lookup"><span data-stu-id="82050-219">Right-click an HDInsight cluster, and then click **View Jobs**.</span></span> <span data-ttu-id="82050-220">You'll see a list of the Hive jobs that ran on the cluster.</span><span class="sxs-lookup"><span data-stu-id="82050-220">You'll see a list of the Hive jobs that ran on the cluster.</span></span>
3. <span data-ttu-id="82050-221">Click a job in the job list to select it, and then use the **Hive Job Summary** window to open **Job Query**, **Job Output**, **Job Log**, or **Yarn log**.</span><span class="sxs-lookup"><span data-stu-id="82050-221">Click a job in the job list to select it, and then use the **Hive Job Summary** window to open **Job Query**, **Job Output**, **Job Log**, or **Yarn log**.</span></span>
   
    ![Data Lake Tools: HDInsight Visual Studio Tools view Hive jobs][12]

### <a name="faster-path-hive-execution-via-hiveserver2"></a><span data-ttu-id="82050-223">Faster path Hive execution via HiveServer2</span><span class="sxs-lookup"><span data-stu-id="82050-223">Faster path Hive execution via HiveServer2</span></span>
> [!NOTE]
> <span data-ttu-id="82050-224">This feature only works on HDInsight cluster version 3.2 and newer.</span><span class="sxs-lookup"><span data-stu-id="82050-224">This feature only works on HDInsight cluster version 3.2 and newer.</span></span>
> 
> 

<span data-ttu-id="82050-225">The Data Lake Tools used to submit Hive jobs via [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) (also known as Templeton).</span><span class="sxs-lookup"><span data-stu-id="82050-225">The Data Lake Tools used to submit Hive jobs via [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) (also known as Templeton).</span></span> <span data-ttu-id="82050-226">It took a long time to return job details and error information.</span><span class="sxs-lookup"><span data-stu-id="82050-226">It took a long time to return job details and error information.</span></span>
<span data-ttu-id="82050-227">In order to solve this performance issue, the Data Lake Tools executes Hive jobs directly in the cluster through HiveServer2, so that it bypasses RDP/SSH.</span><span class="sxs-lookup"><span data-stu-id="82050-227">In order to solve this performance issue, the Data Lake Tools executes Hive jobs directly in the cluster through HiveServer2, so that it bypasses RDP/SSH.</span></span>
<span data-ttu-id="82050-228">In addition to better performance, users can also view Hive on Tez graphs, and the Task details.</span><span class="sxs-lookup"><span data-stu-id="82050-228">In addition to better performance, users can also view Hive on Tez graphs, and the Task details.</span></span>

<span data-ttu-id="82050-229">For HDInsight cluster version 3.2 or later, you can see an **Execute via HiveServer2** button:</span><span class="sxs-lookup"><span data-stu-id="82050-229">For HDInsight cluster version 3.2 or later, you can see an **Execute via HiveServer2** button:</span></span>

![Data Lake visual studio Tools execute via hiveserver2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.execute.via.hiveserver2.png)

<span data-ttu-id="82050-231">And you can see the logs streamed back in real-time and see the job graphs if the Hive query is executed in Tez.</span><span class="sxs-lookup"><span data-stu-id="82050-231">And you can see the logs streamed back in real-time and see the job graphs if the Hive query is executed in Tez.</span></span>

![Data Lake visual studio Tools fast path hive execution](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.fast.path.hive.execution.png)

<span data-ttu-id="82050-233">**Difference between executing queries via HiveServer2 and Submitting Queries via WebHCat**</span><span class="sxs-lookup"><span data-stu-id="82050-233">**Difference between executing queries via HiveServer2 and Submitting Queries via WebHCat**</span></span>

<span data-ttu-id="82050-234">Even though executing queries via HiveServer2 has many performance benefits, it has several limitations.</span><span class="sxs-lookup"><span data-stu-id="82050-234">Even though executing queries via HiveServer2 has many performance benefits, it has several limitations.</span></span> <span data-ttu-id="82050-235">Some of the limitations are not suitable for production usage.</span><span class="sxs-lookup"><span data-stu-id="82050-235">Some of the limitations are not suitable for production usage.</span></span> <span data-ttu-id="82050-236">The following table shows the differences:</span><span class="sxs-lookup"><span data-stu-id="82050-236">The following table shows the differences:</span></span>

|  | <span data-ttu-id="82050-237">Executing via HiveServer2</span><span class="sxs-lookup"><span data-stu-id="82050-237">Executing via HiveServer2</span></span> | <span data-ttu-id="82050-238">Submitting via WebHCat</span><span class="sxs-lookup"><span data-stu-id="82050-238">Submitting via WebHCat</span></span> |
| --- | --- | --- |
| <span data-ttu-id="82050-239">Execute queries</span><span class="sxs-lookup"><span data-stu-id="82050-239">Execute queries</span></span> |<span data-ttu-id="82050-240">Eliminates the overhead in WebHCat (which launches a MapReduce Job named “TempletonControllerJob”).</span><span class="sxs-lookup"><span data-stu-id="82050-240">Eliminates the overhead in WebHCat (which launches a MapReduce Job named “TempletonControllerJob”).</span></span> |<span data-ttu-id="82050-241">As long as a query is executed via WebHCat, WebHCat will launch a MapReduce job which introduces additional latency.</span><span class="sxs-lookup"><span data-stu-id="82050-241">As long as a query is executed via WebHCat, WebHCat will launch a MapReduce job which introduces additional latency.</span></span> |
| <span data-ttu-id="82050-242">Stream logs back</span><span class="sxs-lookup"><span data-stu-id="82050-242">Stream logs back</span></span> |<span data-ttu-id="82050-243">In near real-time.</span><span class="sxs-lookup"><span data-stu-id="82050-243">In near real-time.</span></span> |<span data-ttu-id="82050-244">The job execution logs are available only when the job is finished.</span><span class="sxs-lookup"><span data-stu-id="82050-244">The job execution logs are available only when the job is finished.</span></span> |
| <span data-ttu-id="82050-245">View job history</span><span class="sxs-lookup"><span data-stu-id="82050-245">View job history</span></span> |<span data-ttu-id="82050-246">If a query is executed via HiveServer2, its job history (job log, job output) is not preserved.</span><span class="sxs-lookup"><span data-stu-id="82050-246">If a query is executed via HiveServer2, its job history (job log, job output) is not preserved.</span></span> <span data-ttu-id="82050-247">The application can be viewed in YARN UI with limited information.</span><span class="sxs-lookup"><span data-stu-id="82050-247">The application can be viewed in YARN UI with limited information.</span></span> |<span data-ttu-id="82050-248">If a query is executed via WebHCat, it’s job history (job log, job output) is preserved and can be viewed using Visual Studio/HDInsight SDK/PowerShell.</span><span class="sxs-lookup"><span data-stu-id="82050-248">If a query is executed via WebHCat, it’s job history (job log, job output) is preserved and can be viewed using Visual Studio/HDInsight SDK/PowerShell.</span></span> |
| <span data-ttu-id="82050-249">Close window</span><span class="sxs-lookup"><span data-stu-id="82050-249">Close window</span></span> |<span data-ttu-id="82050-250">Executing via HiveServer2 is a “synchronous” way so you must keep the windows open; if the windows are closed then the query execution will be canceled.</span><span class="sxs-lookup"><span data-stu-id="82050-250">Executing via HiveServer2 is a “synchronous” way so you must keep the windows open; if the windows are closed then the query execution will be canceled.</span></span> |<span data-ttu-id="82050-251">Submitting via WebHCat is a “asynchronous” way so you can submit the query via WebHCat and close Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="82050-251">Submitting via WebHCat is a “asynchronous” way so you can submit the query via WebHCat and close Visual Studio.</span></span> <span data-ttu-id="82050-252">You can come back and see the results at any time.</span><span class="sxs-lookup"><span data-stu-id="82050-252">You can come back and see the results at any time.</span></span> |

### <a name="tez-hive-job-performance-graph"></a><span data-ttu-id="82050-253">Tez Hive job performance graph</span><span class="sxs-lookup"><span data-stu-id="82050-253">Tez Hive job performance graph</span></span>
<span data-ttu-id="82050-254">The Data Lake Tools support showing performance graphs for the Hive jobs ran by the Tez execution engine.</span><span class="sxs-lookup"><span data-stu-id="82050-254">The Data Lake Tools support showing performance graphs for the Hive jobs ran by the Tez execution engine.</span></span> <span data-ttu-id="82050-255">For information on enabling Tez, see [use Hive in HDInsight][hdinsight.hive].</span><span class="sxs-lookup"><span data-stu-id="82050-255">For information on enabling Tez, see [use Hive in HDInsight][hdinsight.hive].</span></span> <span data-ttu-id="82050-256">After you submit a Hive job in Visual Studio, Visual Studio shows you the graph when the job is completed.</span><span class="sxs-lookup"><span data-stu-id="82050-256">After you submit a Hive job in Visual Studio, Visual Studio shows you the graph when the job is completed.</span></span>  <span data-ttu-id="82050-257">You might need to click the **Refresh** button to get the latest job status.</span><span class="sxs-lookup"><span data-stu-id="82050-257">You might need to click the **Refresh** button to get the latest job status.</span></span>

> [!NOTE]
> <span data-ttu-id="82050-258">This feature is only available for HDInsight cluster version above 3.2.4.593, and can only work for completed jobs (if you submitted your job through WebHCat; this graph will show when you execute your query through HiveServer2).</span><span class="sxs-lookup"><span data-stu-id="82050-258">This feature is only available for HDInsight cluster version above 3.2.4.593, and can only work for completed jobs (if you submitted your job through WebHCat; this graph will show when you execute your query through HiveServer2).</span></span> <span data-ttu-id="82050-259">This works for both Windows and Linux-based clusters.</span><span class="sxs-lookup"><span data-stu-id="82050-259">This works for both Windows and Linux-based clusters.</span></span>
> 
> 

![hadoop hive tez performance graph](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.hive.tez.performance.graph.png)

<span data-ttu-id="82050-261">To help you understand your Hive query better, the tools add the Hive Operator view in this release.</span><span class="sxs-lookup"><span data-stu-id="82050-261">To help you understand your Hive query better, the tools add the Hive Operator view in this release.</span></span> <span data-ttu-id="82050-262">You just need to double-click on the vertices of the job graph and you can see all the operators inside the vertex.</span><span class="sxs-lookup"><span data-stu-id="82050-262">You just need to double-click on the vertices of the job graph and you can see all the operators inside the vertex.</span></span> <span data-ttu-id="82050-263">You can also hover on a particular operator to view more details of this operator.</span><span class="sxs-lookup"><span data-stu-id="82050-263">You can also hover on a particular operator to view more details of this operator.</span></span>

### <a name="task-execution-view-for-hive-on-tez-jobs"></a><span data-ttu-id="82050-264">Task execution view for Hive on Tez jobs</span><span class="sxs-lookup"><span data-stu-id="82050-264">Task execution view for Hive on Tez jobs</span></span>
<span data-ttu-id="82050-265">The Task execution view for Hive on Tez jobs can be used to get structured & visualized information for Hive jobs, and get more job details.</span><span class="sxs-lookup"><span data-stu-id="82050-265">The Task execution view for Hive on Tez jobs can be used to get structured & visualized information for Hive jobs, and get more job details.</span></span> <span data-ttu-id="82050-266">When there are performance issues, you can use the view to get further details.</span><span class="sxs-lookup"><span data-stu-id="82050-266">When there are performance issues, you can use the view to get further details.</span></span> <span data-ttu-id="82050-267">For example, how each task operates and the detailed information about each task (data read/write, schedule/start/end time, etc.), so that you can tune job configurations or system architecture based on the visualized information.</span><span class="sxs-lookup"><span data-stu-id="82050-267">For example, how each task operates and the detailed information about each task (data read/write, schedule/start/end time, etc.), so that you can tune job configurations or system architecture based on the visualized information.</span></span>

![Data Lake Visual Studio Tools task execution view](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.task.execution.view.png)

## <a name="run-pig-scripts"></a><span data-ttu-id="82050-269">Run Pig scripts</span><span class="sxs-lookup"><span data-stu-id="82050-269">Run Pig scripts</span></span>
<span data-ttu-id="82050-270">Data Lake Tools for Visual Studio supports creating and submit Pig scripts to HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="82050-270">Data Lake Tools for Visual Studio supports creating and submit Pig scripts to HDInsight clusters.</span></span> <span data-ttu-id="82050-271">Users can create a Pig project from template, and then submit the script to HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="82050-271">Users can create a Pig project from template, and then submit the script to HDInsight clusters.</span></span>

## <a name="feedbacks--known-issues"></a><span data-ttu-id="82050-272">Feedbacks & Known issues</span><span class="sxs-lookup"><span data-stu-id="82050-272">Feedbacks & Known issues</span></span>
* <span data-ttu-id="82050-273">Currently HiveServer2 results are displayed in pure text fashion which is not ideal.</span><span class="sxs-lookup"><span data-stu-id="82050-273">Currently HiveServer2 results are displayed in pure text fashion which is not ideal.</span></span> <span data-ttu-id="82050-274">We are working on fixing that.</span><span class="sxs-lookup"><span data-stu-id="82050-274">We are working on fixing that.</span></span>
* <span data-ttu-id="82050-275">If the results are started with NULL values, currently the results are not shown.</span><span class="sxs-lookup"><span data-stu-id="82050-275">If the results are started with NULL values, currently the results are not shown.</span></span> <span data-ttu-id="82050-276">We have fixed this issue and if you are blocked on this issue, feel free to drop us an email or contact support team.</span><span class="sxs-lookup"><span data-stu-id="82050-276">We have fixed this issue and if you are blocked on this issue, feel free to drop us an email or contact support team.</span></span>
* <span data-ttu-id="82050-277">The HQL script created by Visual Studio is encoded depending on user’s local region setting.</span><span class="sxs-lookup"><span data-stu-id="82050-277">The HQL script created by Visual Studio is encoded depending on user’s local region setting.</span></span> <span data-ttu-id="82050-278">It may not execute correctly if user uploads the script to cluster as binary.</span><span class="sxs-lookup"><span data-stu-id="82050-278">It may not execute correctly if user uploads the script to cluster as binary.</span></span>

## <a name="next-steps"></a><span data-ttu-id="82050-279">Next steps</span><span class="sxs-lookup"><span data-stu-id="82050-279">Next steps</span></span>
<span data-ttu-id="82050-280">In this article, you learned how to connect to HDInsight clusters from Visual Studio, using the Data Lake (HDInsight) Tools package, and how to run a Hive query.</span><span class="sxs-lookup"><span data-stu-id="82050-280">In this article, you learned how to connect to HDInsight clusters from Visual Studio, using the Data Lake (HDInsight) Tools package, and how to run a Hive query.</span></span> <span data-ttu-id="82050-281">For more information, see:</span><span class="sxs-lookup"><span data-stu-id="82050-281">For more information, see:</span></span>

* <span data-ttu-id="82050-282">[Use Hadoop Hive in HDInsight][hdinsight.hive]</span><span class="sxs-lookup"><span data-stu-id="82050-282">[Use Hadoop Hive in HDInsight][hdinsight.hive]</span></span>
* <span data-ttu-id="82050-283">[Get started using Hadoop in HDInsight][hdinsight.get.started]</span><span class="sxs-lookup"><span data-stu-id="82050-283">[Get started using Hadoop in HDInsight][hdinsight.get.started]</span></span>
* <span data-ttu-id="82050-284">[Submit Hadoop jobs in HDInsight][hdinsight.submit.jobs]</span><span class="sxs-lookup"><span data-stu-id="82050-284">[Submit Hadoop jobs in HDInsight][hdinsight.submit.jobs]</span></span>
* <span data-ttu-id="82050-285">[Analyze Twitter data with Hadoop in HDInsight][hdinsight.analyze.twitter.data]</span><span class="sxs-lookup"><span data-stu-id="82050-285">[Analyze Twitter data with Hadoop in HDInsight][hdinsight.analyze.twitter.data]</span></span>

<!--Anchors-->
[Installation]: #installation
[Connect to your Azure subscription]: #connect-to-your-azure-subscription
[Navigate the linked resources]: #navigate-the-linked-resources
[Run Hive queries]: #run-hive-queries
[Next steps]: #next-steps

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.wpi.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.linked.resources.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.server.explorer.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.hive.schema.png
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.create.hive.table.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.run.hive.job.summary.png
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.submit.jobs.advanced.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.validate.hive.script.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.new.hive.project.png
[12]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.view.hive.jobs.png
[13]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.intellisense.table.names.png
[14]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.intellisense.column.names.png


<!--Link references-->
[hdinsight-create-clusters]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight.introduction]: hdinsight-hadoop-introduction.md
[hdinsight.get.started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight.hive]: hdinsight-use-hive.md
[hdinsight.submit.jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight.analyze.twitter.data]: hdinsight-analyze-twitter-data.md
[hdinsight.storm.visual.studio.tools]: hdinsight-storm-develop-csharp-visual-studio-topology.md
[hdinsight.access.application.logs]: hdinsight-hadoop-access-yarn-app-logs.md

[apache.hive]: http://hive.apache.org

















