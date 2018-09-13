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
# <a name="get-started-using-azure-data-lake-hdinsight-tools-for-visual-studio-to-run-a-hive-query"></a>Get started using Azure Data Lake (HDInsight) Tools for Visual Studio to run a Hive query
Learn how to use Data Lake (HDInsight) Tools for Visual Studio to connect to HDInsight clusters and submit Hive queries. For more information about using HDInsight, see [Introduction to HDInsight][hdinsight.introduction] and [Get started with HDInsight][hdinsight.get.started]. For more information about connecting to a Storm cluster, see [Develop C# topologies for Apache Storm on HDInsight using Visual Studio][hdinsight.storm.visual.studio.tools].

Data Lake Tools for Visual Studio can be used to access both Data Lake Analytics and HDInsight.  For the information about Data Lake Tools, see [Tutorial: develop U-SQL scripts using Data Lake Tools for Visual Studio](../data-lake-analytics/data-lake-analytics-data-lake-tools-get-started.md).

**Prerequisites**

To complete this tutorial and use the Data Lake Tools in Visual Studio, you'll need the following:

* An Azure HDInsight cluster: To create one, see [Get started using Linux-based HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md)
* A workstation with the following software:
  
  * Windows 10, Windows 8.1, Windows 8, or Windows 7.
  * Visual Studio 2013/2015/2017.
    
    > [!NOTE]
    > Currently, the Data Lake Tools for Visual Studio only come with the English version.
    > 
    > 

## <a name="install-data-lake-tools-for-visual-studio"></a>Install Data Lake Tools for Visual Studio

Data Lake Tools is installed by default for Visual Studio 2017. For older versions, you can install it using the [Web Platform Installer](https://www.microsoft.com/web/downloads/). You must choose the one that matches your version of Visual Studio. If you don't have Visual Studio installed, you can install the latest Visual Studio Community and Azure SDK using the [Web Platform Installer](https://www.microsoft.com/web/downloads/):

![Data Lake Tools for Visual Studio Web Platform installer.][1]

## <a name="connect-to-azure-subscriptions"></a>Connect to Azure subscriptions
Data Lake Tools for Visual Studio allows you to connect to your HDInsight clusters, perform some basic management operations, and run Hive queries.

> [!NOTE]
> For information on connecting to a generic Hadoop cluster, see [Write and submit Hive queries using Visual Studio](http://blogs.msdn.com/b/xiaoyong/archive/2015/05/04/how-to-write-and-submit-hive-queries-using-visual-studio.aspx).
> 
> 

**To connect to your Azure subscription**

1. Open Visual Studio.
2. From the **View** menu, click **Server Explorer** to open the Server Explorer window.
3. Expand **Azure**, and then expand **HDInsight**.
   
   > [!NOTE]
   > Notice the **HDInsight Task List** window should be open. If you don't see it, click **Other Windows** from the **View** menu, and then click **HDInsight Task List Window**.  
   > 
   > 
4. Enter your Azure subscription credentials, and then click **Sign In**. This is only required if you have never connected to the Azure subscription from Visual Studio on this workstation.
5. In Server Explorer, you'll see a list of existing HDInsight clusters. If you don't have any clusters, you can create one by using the Azure portal, Azure PowerShell, or the HDInsight SDK. For more information, see [Create HDInsight clusters][hdinsight-create-clusters].
   
   ![Data Lake Tools for Visual Studio Server Explorer cluster list][5]
6. Expand an HDInsight cluster. You'll see **Hive Databases**, a default storage account, linked storage accounts, and **Hadoop Service log**. You can further expand the entities.

After you've connected to your Azure subscription, you'll be able to do the following:

**To connect to the Azure portal from Visual Studio**

* From Server Explorer, expand **Azure** > **HDInsight**, right-click an HDInsight cluster, and then click **Manage Cluster in Azure portal**.

**To ask questions and provide feedback from Visual Studio**

* From the **Tools** menu, click **HDInsight**, and then click **MSDN Forum** to ask questions, or click **Give Feedback**.

## <a name="navigate-the-linked-resources"></a>Navigate the linked resources
From Server Explorer, you can see the default storage account and any linked storage accounts. If you expand the default storage account, you can see the containers on the storage account. The default storage account and the default container are marked. You can also right-click any of the containers to view the contents.

![Data Lake Tools for Visual Studio server explorer cluster list][2]

After opening a container, you can use the following buttons to upload, delete, and download blobs:

![Data Lake Tools for Visual Studio server explorer blob operations](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.blob.operations.png)

## <a name="run-a-hive-query"></a>Run a Hive query
[Apache Hive][apache.hive] is a data warehouse infrastructure built on Hadoop for providing data summarization, queries, and analysis. Data Lake Tools for Visual Studio supports running Hive queries from Visual Studio. For more information about Hive, see [Use Hive with HDInsight][hdinsight.hive].

It is time consuming to test Hive script against an HDInsight cluster. It could take several minutes or more. Data Lake Tools for Visual Studio is capable of validating Hive script locally without connecting to a live cluster.

Data Lake Tools for Visual Studio also enables users to see what’s inside the Hive job by collecting and surfacing the YARN logs of certain Hive jobs.

### <a name="view-the-hivesampletable"></a>View the **hivesampletable**
All HDInsight clusters come with a sample Hive table called *hivesampletable*. We'll use this table to show you how to list Hive tables, view the table schemas, and list the rows in the Hive table.

**To list Hive tables and view Hive table schema**

1. From **Server Explorer**, expand **Azure** > **HDInsight** > the cluster of your choice > **Hive Databases** > **Default** > **hivesampletable** to see the table schema.
2. Right-click **hivesampletable**, and then click **View Top 100 Rows** to list the rows. It is equivalent to running the following Hive query using Hive ODBC driver:
   
     SELECT * FROM hivesampletable LIMIT 100
   
   You can customize the row count.
   
   ![Data Lake Tools: HDInsight Hive Visual Studio schema query][6]

### <a name="create-hive-tables"></a>Create Hive tables
You can use the GUI to create a Hive table or use Hive queries. For information about using Hive queries, see [Run Hive queries](#run.queries).

**To create a Hive table**

1. From **Server Explorer**, expand **Azure** > **HDInsight Clusters** an HDInsight cluster > **Hive Databases**, then right-click **default**, and click **Create Table**.
2. Configure the table.
3. Click **Create Table** to submit the job to create the new Hive table.
   
    ![Data Lake Tools: HDInsight Visual Studio Tools create hive table][7]

### <a name="run.queries"></a>Validate and run Hive queries
There are two ways to create and run Hive queries:

* Create ad-hoc queries
* Create a Hive application

**To create, validate, and run ad-hoc queries**

1. From **Server Explorer**, expand **Azure**, and then expand **HDInsight Clusters**.
2. Right-click the cluster where you want to run the query, and then click **Write a Hive Query**.
3. Enter the Hive queries. Notice the Hive editor supports IntelliSense. Data Lake Tools for Visual Studio supports loading the remote metadata when you are editing your Hive script. For example, when you type "SELECT * FROM", the IntelliSense lists all the suggested table names. When a table name is specified, the column names are listed by the IntelliSense. The tools support almost all Hive DML statements, subqueries, and the built-in UDFs.
   
    ![Data Lake Tools: HDInsight Visual Studio Tools IntelliSense][13]
   
    ![Data Lake Tools: HDInsight Visual Studio Tools IntelliSense][14]
   
   > [!NOTE]
   > Only the metadata of the clusters that is selected in HDInsight Toolbar will be suggested.
   > 
   > 
4. (Optional): Click **Validate Script** to check the script syntax errors.
   
    ![Data Lake Tools: Data Lake Tools for Visual Studio local validation][10]
5. Click **Submit** or **Submit (Advanced)**. With the advanced submit option, you'll configure **Job Name**, **Arguments**, **Additional Configurations**, and **Status Directory** for the script:
   
    ![HDInsight Hadoop hive query][9]
   
    After you submit the job, you see a **Hive Job Summary** window.
   
    ![Summary of an HDInsight Hadoop Hive query][8]
6. Use the **Refresh** button to update the status until the job status changes to **Completed**.
7. Click the links at the bottom to see the following: **Job Query**, **Job Output**, **Job log**, or **Yarn log**.

**To create and run a Hive solution**

1. From the **FILE** menu, click **New**, and then click **Project**.
2. Select **HDInsight** from the left pane, select **Hive Application** in the middle pane, enter the properties, and then click **OK**.
   
    ![Data Lake Tools: HDInsight Visual Studio Tools new hive project][11]
3. From **Solution Explorer**, double-click **Script.hql** to open it.
4. To validate the Hive script, you can click the **Validate Script** button, or right-click the script in the Hive editor, and then click **Validate Script** from the context menu.

### <a name="view-hive-jobs"></a>View Hive jobs
You can view job queries, job output, job logs, and Yarn logs for Hive jobs. For more information, see the previous screenshot.

The most recent release of the tools allows you to see what’s inside your Hive jobs by collecting and surfacing  YARN logs. A YARN log can help you investigating performance issues. For more information about how HDInsight collects YARN logs, see [Access HDInsight Application Logs Programmatically][hdinsight.access.application.logs].

**To view Hive jobs**

1. From **Server Explorer**, expand **Azure**, and then expand **HDInsight**.
2. Right-click an HDInsight cluster, and then click **View Jobs**. You'll see a list of the Hive jobs that ran on the cluster.
3. Click a job in the job list to select it, and then use the **Hive Job Summary** window to open **Job Query**, **Job Output**, **Job Log**, or **Yarn log**.
   
    ![Data Lake Tools: HDInsight Visual Studio Tools view Hive jobs][12]

### <a name="faster-path-hive-execution-via-hiveserver2"></a>Faster path Hive execution via HiveServer2
> [!NOTE]
> This feature only works on HDInsight cluster version 3.2 and newer.
> 
> 

The Data Lake Tools used to submit Hive jobs via [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) (also known as Templeton). It took a long time to return job details and error information.
In order to solve this performance issue, the Data Lake Tools executes Hive jobs directly in the cluster through HiveServer2, so that it bypasses RDP/SSH.
In addition to better performance, users can also view Hive on Tez graphs, and the Task details.

For HDInsight cluster version 3.2 or later, you can see an **Execute via HiveServer2** button:

![Data Lake visual studio Tools execute via hiveserver2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.execute.via.hiveserver2.png)

And you can see the logs streamed back in real-time and see the job graphs if the Hive query is executed in Tez.

![Data Lake visual studio Tools fast path hive execution](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.fast.path.hive.execution.png)

**Difference between executing queries via HiveServer2 and Submitting Queries via WebHCat**

Even though executing queries via HiveServer2 has many performance benefits, it has several limitations. Some of the limitations are not suitable for production usage. The following table shows the differences:

|  | Executing via HiveServer2 | Submitting via WebHCat |
| --- | --- | --- |
| Execute queries |Eliminates the overhead in WebHCat (which launches a MapReduce Job named “TempletonControllerJob”). |As long as a query is executed via WebHCat, WebHCat will launch a MapReduce job which introduces additional latency. |
| Stream logs back |In near real-time. |The job execution logs are available only when the job is finished. |
| View job history |If a query is executed via HiveServer2, its job history (job log, job output) is not preserved. The application can be viewed in YARN UI with limited information. |If a query is executed via WebHCat, it’s job history (job log, job output) is preserved and can be viewed using Visual Studio/HDInsight SDK/PowerShell. |
| Close window |Executing via HiveServer2 is a “synchronous” way so you must keep the windows open; if the windows are closed then the query execution will be canceled. |Submitting via WebHCat is a “asynchronous” way so you can submit the query via WebHCat and close Visual Studio. You can come back and see the results at any time. |

### <a name="tez-hive-job-performance-graph"></a>Tez Hive job performance graph
The Data Lake Tools support showing performance graphs for the Hive jobs ran by the Tez execution engine. For information on enabling Tez, see [use Hive in HDInsight][hdinsight.hive]. After you submit a Hive job in Visual Studio, Visual Studio shows you the graph when the job is completed.  You might need to click the **Refresh** button to get the latest job status.

> [!NOTE]
> This feature is only available for HDInsight cluster version above 3.2.4.593, and can only work for completed jobs (if you submitted your job through WebHCat; this graph will show when you execute your query through HiveServer2). This works for both Windows and Linux-based clusters.
> 
> 

![hadoop hive tez performance graph](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.hive.tez.performance.graph.png)

To help you understand your Hive query better, the tools add the Hive Operator view in this release. You just need to double-click on the vertices of the job graph and you can see all the operators inside the vertex. You can also hover on a particular operator to view more details of this operator.

### <a name="task-execution-view-for-hive-on-tez-jobs"></a>Task execution view for Hive on Tez jobs
The Task execution view for Hive on Tez jobs can be used to get structured & visualized information for Hive jobs, and get more job details. When there are performance issues, you can use the view to get further details. For example, how each task operates and the detailed information about each task (data read/write, schedule/start/end time, etc.), so that you can tune job configurations or system architecture based on the visualized information.

![Data Lake Visual Studio Tools task execution view](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.task.execution.view.png)

## <a name="run-pig-scripts"></a>Run Pig scripts
Data Lake Tools for Visual Studio supports creating and submit Pig scripts to HDInsight clusters. Users can create a Pig project from template, and then submit the script to HDInsight clusters.

## <a name="feedbacks--known-issues"></a>Feedbacks & Known issues
* Currently HiveServer2 results are displayed in pure text fashion which is not ideal. We are working on fixing that.
* If the results are started with NULL values, currently the results are not shown. We have fixed this issue and if you are blocked on this issue, feel free to drop us an email or contact support team.
* The HQL script created by Visual Studio is encoded depending on user’s local region setting. It may not execute correctly if user uploads the script to cluster as binary.

## <a name="next-steps"></a>Next steps
In this article, you learned how to connect to HDInsight clusters from Visual Studio, using the Data Lake (HDInsight) Tools package, and how to run a Hive query. For more information, see:

* [Use Hadoop Hive in HDInsight][hdinsight.hive]
* [Get started using Hadoop in HDInsight][hdinsight.get.started]
* [Submit Hadoop jobs in HDInsight][hdinsight.submit.jobs]
* [Analyze Twitter data with Hadoop in HDInsight][hdinsight.analyze.twitter.data]

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

















