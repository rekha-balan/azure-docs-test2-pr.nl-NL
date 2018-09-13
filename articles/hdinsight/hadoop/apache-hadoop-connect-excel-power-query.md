---
title: Connect Excel to Hadoop with Power Query - Azure HDInsight
description: Learn how to take advantage of business intelligence components and use Power Query for Excel to access data stored in Hadoop on HDInsight.
services: hdinsight
author: jasonwhowell
ms.author: jasonh
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 05/16/2018
ms.openlocfilehash: 45014592cd648ee1a7b75fa59babf8571c151269
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870266"
---
# <a name="connect-excel-to-hadoop-by-using-power-query"></a>Connect Excel to Hadoop by using Power Query
One key feature of the Microsoft big-data solution is the integration of Microsoft business intelligence (BI) components with Hadoop clusters in Azure HDInsight. A primary example is the ability to connect Excel to the Azure Storage account that contains the data associated with your Hadoop cluster by using the Microsoft Power Query for Excel add-in. This article walks you through how to set up and use Power Query to query data associated with a Hadoop cluster managed with HDInsight.

### <a name="prerequisites"></a>Prerequisites
Before you begin this article, you must have the following items:

* **An HDInsight cluster**. To configure one, see [Get started with Azure HDInsight][hdinsight-get-started].
* **A workstation** that is running Windows 7, Windows Server 2008 R2, or a later operating system.
* **Office 2016, Office 2013 Professional Plus, Office 365 ProPlus, Excel 2013 Standalone, or Office 2010 Professional Plus**.

## <a name="install-power-query"></a>Install Power Query
Power Query can import data that has been output or that has been generated by a Hadoop job running on an HDInsight cluster.

In Excel 2016, Power Query has been integrated into the Data ribbon under the Get & Transform section. For older Excel versions, download Microsoft Power Query for Excel from the [Microsoft Download Center][powerquery-download] and install it.

## <a name="import-hdinsight-data-into-excel"></a>Import HDInsight data into Excel
The Power Query add-in for Excel makes it easy to import data from your HDInsight cluster into Excel, where BI tools such as PowerPivot and Power Map can be used to inspect, analyze, and present the data.

**To import data from an HDInsight cluster**

1. Open Excel.
2. Create a new blank workbook.
3. Perform the following steps based on the Excel version:

    - Excel 2016

        - Click the **Data** menu, click **Get Data** from the **Get & Transform Data** ribbon, click **From Azure**, and then click **From Azure HDInsight(HDFS)**.

        ![HDI.PowerQuery.SelectHdiSource](./media/apache-hadoop-connect-excel-power-query/hdi.powerquery.selecthdisource.excel2016.png)

    - Excel 2013/2010

        - Click the **Power Query** menu, click **From Azure**, and then click **From Microsoft Azure HDInsight**.
   
        ![HDI.PowerQuery.SelectHdiSource][image-hdi-powerquery-hdi-source]
       
        **Note:** If you don't see the **Power Query** menu, go to **File** > **Options** > **Add-Ins**, and select **COM Add-ins** from the drop-down **Manage** box at the bottom of the page. Select the **Go...** button and verify that the box for the Power Query for Excel add-in has been checked.
       
        **Note:** Power Query also allows you to import data from HDFS by clicking **From Other Sources**.
4. For **Account Name**, enter the name of the Azure Blob storage account associated with your cluster, and then click **OK**. This account can be the [default storage account](../hdinsight-administer-use-management-portal.md#find-the-default-storage-account) or a linked storage account.  The format is *https://&lt;StorageAccountName>.blob.core.windows.net/*.
5. For **Account Key**, enter the key for the Blob storage account, and then click **Save**. (You need to enter the account information only the first time you access this store.)
6. In the **Navigator** pane on the left of the Query Editor, double-click the Blob storage container name. By default, the container name is the same name as the cluster name.
7. Locate **HiveSampleData.txt** in the **Name** column (the folder path is **../hive/warehouse/hivesampletable/**), and then click **Binary** on the left of HiveSampleData.txt. HiveSampleData.txt comes with all the cluster. Optionally, you can use your own file.
   
    ![HDI.PowerQuery.ImportData][image-hdi-powerquery-importdata]
8. If you want, you can rename the column names. When you are ready, click **Close & Load**.  The data has been loaded to your workbook:
   
    ![HDI.PowerQuery.ImportedTable][image-hdi-powerquery-imported-table]

## <a name="next-steps"></a>Next steps
In this article, you learned how to use Power Query to retrieve data from HDInsight into Excel. Similarly, you can retrieve data from HDInsight into Azure SQL Database. It is also possible to upload data into HDInsight. To learn more, see the following articles:

* [Visualize Hive data with Microsoft Power BI in Azure HDInsight](apache-hadoop-connect-hive-power-bi.md).
* [Visualize Interactive Query Hive data with Power BI in Azure HDInsight](../interactive-query/apache-hadoop-connect-hive-power-bi-directquery.md).
* [Use Zeppelin to run Hive queries in Azure HDInsight ](./../hdinsight-connect-hive-zeppelin.md).
* [Connect Excel to HDInsight with the Microsoft Hive ODBC Driver](apache-hadoop-connect-excel-hive-odbc-driver.md).
* [Connect to Azure HDInsight and run Hive queries using Data Lake Tools for Visual Studio](apache-hadoop-visual-studio-tools-get-started.md).
* [Use Azure HDInsight Tool for Visual Studio Code](../hdinsight-for-vscode.md).
* [Upload data to HDInsight](./../hdinsight-upload-data.md).

[image-hdi-powerquery-hdi-source]: ./media/apache-hadoop-connect-excel-power-query/hdi.powerquery.selecthdisource.png
[image-hdi-powerquery-importdata]: ./media/apache-hadoop-connect-excel-power-query/hdi.powerquery.importdata.png
[image-hdi-powerquery-imported-table]: ./media/apache-hadoop-connect-excel-power-query/hdi.powerquery.importedtable.PNG

[powerquery-download]: http://go.microsoft.com/fwlink/?LinkID=286689