---
title: Apache Sqoop with Hadoop - Azure HDInsight
description: Learn how to use Apache Sqoop to import and export between Hadoop on HDInsight and an Azure SQL Database.
keywords: hadoop sqoop,sqoop
services: hdinsight
author: jasonwhowell
ms.author: jasonh
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.topic: conceptual
ms.date: 03/26/2018
ms.openlocfilehash: e9ee4ceb51b2de58010f3e6cf7feba9df64b9bad
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856554"
---
# <a name="use-apache-sqoop-to-import-and-export-data-between-hadoop-on-hdinsight-and-sql-database"></a><span data-ttu-id="682c7-104">Use Apache Sqoop to import and export data between Hadoop on HDInsight and SQL Database</span><span class="sxs-lookup"><span data-stu-id="682c7-104">Use Apache Sqoop to import and export data between Hadoop on HDInsight and SQL Database</span></span>

[!INCLUDE [sqoop-selector](../../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="682c7-105">Learn how to use Apache Sqoop to import and export between a Hadoop cluster in Azure HDInsight and Azure SQL Database or Microsoft SQL Server database.</span><span class="sxs-lookup"><span data-stu-id="682c7-105">Learn how to use Apache Sqoop to import and export between a Hadoop cluster in Azure HDInsight and Azure SQL Database or Microsoft SQL Server database.</span></span> <span data-ttu-id="682c7-106">The steps in this document use the `sqoop` command directly from the headnode of the Hadoop cluster.</span><span class="sxs-lookup"><span data-stu-id="682c7-106">The steps in this document use the `sqoop` command directly from the headnode of the Hadoop cluster.</span></span> <span data-ttu-id="682c7-107">You use SSH to connect to the head node and run the commands in this document.</span><span class="sxs-lookup"><span data-stu-id="682c7-107">You use SSH to connect to the head node and run the commands in this document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="682c7-108">The steps in this document only work with HDInsight clusters that use Linux.</span><span class="sxs-lookup"><span data-stu-id="682c7-108">The steps in this document only work with HDInsight clusters that use Linux.</span></span> <span data-ttu-id="682c7-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="682c7-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="682c7-110">For more information, see [HDInsight retirement on Windows](../hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="682c7-110">For more information, see [HDInsight retirement on Windows](../hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

> [!WARNING]
> <span data-ttu-id="682c7-111">The steps in this document assume that you have already created an Azure SQL Database named `sqooptest`.</span><span class="sxs-lookup"><span data-stu-id="682c7-111">The steps in this document assume that you have already created an Azure SQL Database named `sqooptest`.</span></span>
>
> <span data-ttu-id="682c7-112">This document provides T-SQL statements that are used to create and query a table in SQL Database.</span><span class="sxs-lookup"><span data-stu-id="682c7-112">This document provides T-SQL statements that are used to create and query a table in SQL Database.</span></span> <span data-ttu-id="682c7-113">There are many clients that you can use these statements with SQL Database.</span><span class="sxs-lookup"><span data-stu-id="682c7-113">There are many clients that you can use these statements with SQL Database.</span></span> <span data-ttu-id="682c7-114">We recommend the following clients:</span><span class="sxs-lookup"><span data-stu-id="682c7-114">We recommend the following clients:</span></span>
>
> * [<span data-ttu-id="682c7-115">SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="682c7-115">SQL Server Management Studio</span></span>](../../sql-database/sql-database-connect-query-ssms.md)
> * [<span data-ttu-id="682c7-116">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="682c7-116">Visual Studio Code</span></span>](../../sql-database/sql-database-connect-query-vscode.md)
> * <span data-ttu-id="682c7-117">The [sqlcmd](https://docs.microsoft.com/sql/tools/sqlcmd-utility) utility</span><span class="sxs-lookup"><span data-stu-id="682c7-117">The [sqlcmd](https://docs.microsoft.com/sql/tools/sqlcmd-utility) utility</span></span>

## <a name="create-the-table-in-sql-database"></a><span data-ttu-id="682c7-118">Create the table in SQL Database</span><span class="sxs-lookup"><span data-stu-id="682c7-118">Create the table in SQL Database</span></span>

> [!IMPORTANT]
> <span data-ttu-id="682c7-119">If you are using the HDInsight cluster and SQL Database created in [Create cluster and SQL database](hdinsight-use-sqoop.md), skip the steps in this section.</span><span class="sxs-lookup"><span data-stu-id="682c7-119">If you are using the HDInsight cluster and SQL Database created in [Create cluster and SQL database](hdinsight-use-sqoop.md), skip the steps in this section.</span></span> <span data-ttu-id="682c7-120">The database and table were created as part of the steps in the [Create cluster and SQL database](hdinsight-use-sqoop.md) document.</span><span class="sxs-lookup"><span data-stu-id="682c7-120">The database and table were created as part of the steps in the [Create cluster and SQL database](hdinsight-use-sqoop.md) document.</span></span>

<span data-ttu-id="682c7-121">Use a SQL client to connect to the `sqooptest` database in your SQL Database.</span><span class="sxs-lookup"><span data-stu-id="682c7-121">Use a SQL client to connect to the `sqooptest` database in your SQL Database.</span></span> <span data-ttu-id="682c7-122">Then use the following T-SQL to create a table named `mobiledata`:</span><span class="sxs-lookup"><span data-stu-id="682c7-122">Then use the following T-SQL to create a table named `mobiledata`:</span></span>

```sql
CREATE TABLE [dbo].[mobiledata](
[clientid] [nvarchar](50),
[querytime] [nvarchar](50),
[market] [nvarchar](50),
[deviceplatform] [nvarchar](50),
[devicemake] [nvarchar](50),
[devicemodel] [nvarchar](50),
[state] [nvarchar](50),
[country] [nvarchar](50),
[querydwelltime] [float],
[sessionid] [bigint],
[sessionpagevieworder] [bigint])
GO
CREATE CLUSTERED INDEX mobiledata_clustered_index on mobiledata(clientid)
GO
```

## <a name="sqoop-export"></a><span data-ttu-id="682c7-123">Sqoop export</span><span class="sxs-lookup"><span data-stu-id="682c7-123">Sqoop export</span></span>

1. <span data-ttu-id="682c7-124">Use SSH to connect to the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="682c7-124">Use SSH to connect to the HDInsight cluster.</span></span> <span data-ttu-id="682c7-125">For example, the following command connects to the primary headnode of a cluster named `mycluster`:</span><span class="sxs-lookup"><span data-stu-id="682c7-125">For example, the following command connects to the primary headnode of a cluster named `mycluster`:</span></span>

    ```bash
    ssh mycluster-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="682c7-126">For more information, see [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="682c7-126">For more information, see [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="682c7-127">To verify that Sqoop can see your SQL Database, use the following command:</span><span class="sxs-lookup"><span data-stu-id="682c7-127">To verify that Sqoop can see your SQL Database, use the following command:</span></span>

    ```bash
    sqoop list-databases --connect jdbc:sqlserver://<serverName>.database.windows.net:1433 --username <adminLogin> -P
    ```
    <span data-ttu-id="682c7-128">When prompted, enter the password for the SQL Database login.</span><span class="sxs-lookup"><span data-stu-id="682c7-128">When prompted, enter the password for the SQL Database login.</span></span>

    <span data-ttu-id="682c7-129">This command returns a list of databases, including the **sqooptest** database used earlier.</span><span class="sxs-lookup"><span data-stu-id="682c7-129">This command returns a list of databases, including the **sqooptest** database used earlier.</span></span>

3. <span data-ttu-id="682c7-130">To export data from the Hive **hivesampletable** table to the **mobiledata** table in SQL Database, use the following command:</span><span class="sxs-lookup"><span data-stu-id="682c7-130">To export data from the Hive **hivesampletable** table to the **mobiledata** table in SQL Database, use the following command:</span></span>

    ```bash
    sqoop export --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=sqooptest' --username <adminLogin> -P -table 'mobiledata' --hcatalog-table hivesampletable
    ```

4. <span data-ttu-id="682c7-131">To verify that data was exported, use the following query from your SQL client to view the exported data:</span><span class="sxs-lookup"><span data-stu-id="682c7-131">To verify that data was exported, use the following query from your SQL client to view the exported data:</span></span>

    ```sql
    SET ROWCOUNT 50;
    SELECT * FROM mobiledata;
    ```

    <span data-ttu-id="682c7-132">This command lists 50 rows that were imported into the table.</span><span class="sxs-lookup"><span data-stu-id="682c7-132">This command lists 50 rows that were imported into the table.</span></span>

## <a name="sqoop-import"></a><span data-ttu-id="682c7-133">Sqoop import</span><span class="sxs-lookup"><span data-stu-id="682c7-133">Sqoop import</span></span>

1. <span data-ttu-id="682c7-134">Use the following command to import data from the **mobiledata** table in SQL Database, to the **wasb:///tutorials/usesqoop/importeddata** directory on HDInsight:</span><span class="sxs-lookup"><span data-stu-id="682c7-134">Use the following command to import data from the **mobiledata** table in SQL Database, to the **wasb:///tutorials/usesqoop/importeddata** directory on HDInsight:</span></span>

    ```bash
    sqoop import --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=sqooptest' --username <adminLogin> -P --table 'mobiledata' --target-dir 'wasb:///tutorials/usesqoop/importeddata' --fields-terminated-by '\t' --lines-terminated-by '\n' -m 1
    ```

    <span data-ttu-id="682c7-135">The fields in the data are separated by a tab character, and the lines are terminated by a new-line character.</span><span class="sxs-lookup"><span data-stu-id="682c7-135">The fields in the data are separated by a tab character, and the lines are terminated by a new-line character.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="682c7-136">The `wasb:///` path works with clusters that use Azure Storage as the default cluster storage.</span><span class="sxs-lookup"><span data-stu-id="682c7-136">The `wasb:///` path works with clusters that use Azure Storage as the default cluster storage.</span></span> <span data-ttu-id="682c7-137">For clusters that use Azure Data Lake Store, use `adl:///` instead.</span><span class="sxs-lookup"><span data-stu-id="682c7-137">For clusters that use Azure Data Lake Store, use `adl:///` instead.</span></span>

2. <span data-ttu-id="682c7-138">Once the import has completed, use the following command to list out the data in the new directory:</span><span class="sxs-lookup"><span data-stu-id="682c7-138">Once the import has completed, use the following command to list out the data in the new directory:</span></span>

    ```bash
    hdfs dfs -text /tutorials/usesqoop/importeddata/part-m-00000
    ```

## <a name="using-sql-server"></a><span data-ttu-id="682c7-139">Using SQL Server</span><span class="sxs-lookup"><span data-stu-id="682c7-139">Using SQL Server</span></span>

<span data-ttu-id="682c7-140">You can also use Sqoop to import and export data from SQL Server.</span><span class="sxs-lookup"><span data-stu-id="682c7-140">You can also use Sqoop to import and export data from SQL Server.</span></span> <span data-ttu-id="682c7-141">The differences between using SQL Database and SQL Server are:</span><span class="sxs-lookup"><span data-stu-id="682c7-141">The differences between using SQL Database and SQL Server are:</span></span>

* <span data-ttu-id="682c7-142">Both HDInsight and SQL Server must be on the same Azure Virtual Network.</span><span class="sxs-lookup"><span data-stu-id="682c7-142">Both HDInsight and SQL Server must be on the same Azure Virtual Network.</span></span>

    <span data-ttu-id="682c7-143">For an example, see the [Connect HDInsight to your on-premises network](./../connect-on-premises-network.md) document.</span><span class="sxs-lookup"><span data-stu-id="682c7-143">For an example, see the [Connect HDInsight to your on-premises network](./../connect-on-premises-network.md) document.</span></span>

    <span data-ttu-id="682c7-144">For more information on using HDInsight with an Azure Virtual Network, see the [Extend HDInsight with Azure Virtual Network](../hdinsight-extend-hadoop-virtual-network.md) document.</span><span class="sxs-lookup"><span data-stu-id="682c7-144">For more information on using HDInsight with an Azure Virtual Network, see the [Extend HDInsight with Azure Virtual Network](../hdinsight-extend-hadoop-virtual-network.md) document.</span></span> <span data-ttu-id="682c7-145">For more information on Azure Virtual Network, see the [Virtual Network Overview](../../virtual-network/virtual-networks-overview.md) document.</span><span class="sxs-lookup"><span data-stu-id="682c7-145">For more information on Azure Virtual Network, see the [Virtual Network Overview](../../virtual-network/virtual-networks-overview.md) document.</span></span>

* <span data-ttu-id="682c7-146">SQL Server must be configured to allow SQL authentication.</span><span class="sxs-lookup"><span data-stu-id="682c7-146">SQL Server must be configured to allow SQL authentication.</span></span> <span data-ttu-id="682c7-147">For more information, see the [Choose an Authentication Mode](https://msdn.microsoft.com/ms144284.aspx) document.</span><span class="sxs-lookup"><span data-stu-id="682c7-147">For more information, see the [Choose an Authentication Mode](https://msdn.microsoft.com/ms144284.aspx) document.</span></span>

* <span data-ttu-id="682c7-148">You may have to configure SQL Server to accept remote connections.</span><span class="sxs-lookup"><span data-stu-id="682c7-148">You may have to configure SQL Server to accept remote connections.</span></span> <span data-ttu-id="682c7-149">For more information, see the [How to troubleshoot connecting to the SQL Server database engine](http://social.technet.microsoft.com/wiki/contents/articles/2102.how-to-troubleshoot-connecting-to-the-sql-server-database-engine.aspx) document.</span><span class="sxs-lookup"><span data-stu-id="682c7-149">For more information, see the [How to troubleshoot connecting to the SQL Server database engine](http://social.technet.microsoft.com/wiki/contents/articles/2102.how-to-troubleshoot-connecting-to-the-sql-server-database-engine.aspx) document.</span></span>

* <span data-ttu-id="682c7-150">Use the following Transact-SQL statements to create the **mobiledata** table:</span><span class="sxs-lookup"><span data-stu-id="682c7-150">Use the following Transact-SQL statements to create the **mobiledata** table:</span></span>

    ```sql
    CREATE TABLE [dbo].[mobiledata](
    [clientid] [nvarchar](50),
    [querytime] [nvarchar](50),
    [market] [nvarchar](50),
    [deviceplatform] [nvarchar](50),
    [devicemake] [nvarchar](50),
    [devicemodel] [nvarchar](50),
    [state] [nvarchar](50),
    [country] [nvarchar](50),
    [querydwelltime] [float],
    [sessionid] [bigint],
    [sessionpagevieworder] [bigint])
    ```

* <span data-ttu-id="682c7-151">When connecting to the SQL Server from HDInsight, you may have to use the IP address of the SQL Server.</span><span class="sxs-lookup"><span data-stu-id="682c7-151">When connecting to the SQL Server from HDInsight, you may have to use the IP address of the SQL Server.</span></span> <span data-ttu-id="682c7-152">For example:</span><span class="sxs-lookup"><span data-stu-id="682c7-152">For example:</span></span>

    ```bash
    sqoop import --connect 'jdbc:sqlserver://10.0.1.1:1433;database=sqooptest' --username <adminLogin> -P -table 'mobiledata' --target-dir 'wasb:///tutorials/usesqoop/importeddata' --fields-terminated-by '\t' --lines-terminated-by '\n' -m 1
    ```

## <a name="limitations"></a><span data-ttu-id="682c7-153">Limitations</span><span class="sxs-lookup"><span data-stu-id="682c7-153">Limitations</span></span>

* <span data-ttu-id="682c7-154">Bulk export - With Linux-based HDInsight, the Sqoop connector used to export data to Microsoft SQL Server or Azure SQL Database does not support bulk inserts.</span><span class="sxs-lookup"><span data-stu-id="682c7-154">Bulk export - With Linux-based HDInsight, the Sqoop connector used to export data to Microsoft SQL Server or Azure SQL Database does not support bulk inserts.</span></span>

* <span data-ttu-id="682c7-155">Batching - With Linux-based HDInsight, When using the `-batch` switch when performing inserts, Sqoop makes multiple inserts instead of batching the insert operations.</span><span class="sxs-lookup"><span data-stu-id="682c7-155">Batching - With Linux-based HDInsight, When using the `-batch` switch when performing inserts, Sqoop makes multiple inserts instead of batching the insert operations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="682c7-156">Next steps</span><span class="sxs-lookup"><span data-stu-id="682c7-156">Next steps</span></span>

<span data-ttu-id="682c7-157">Now you have learned how to use Sqoop.</span><span class="sxs-lookup"><span data-stu-id="682c7-157">Now you have learned how to use Sqoop.</span></span> <span data-ttu-id="682c7-158">To learn more, see:</span><span class="sxs-lookup"><span data-stu-id="682c7-158">To learn more, see:</span></span>

* <span data-ttu-id="682c7-159">[Use Oozie with HDInsight](../hdinsight-use-oozie.md): Use Sqoop action in an Oozie workflow.</span><span class="sxs-lookup"><span data-stu-id="682c7-159">[Use Oozie with HDInsight](../hdinsight-use-oozie.md): Use Sqoop action in an Oozie workflow.</span></span>
* <span data-ttu-id="682c7-160">[Analyze flight delay data using HDInsight](../hdinsight-analyze-flight-delay-data.md): Use Hive to analyze flight delay data, and then use Sqoop to export data to an Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="682c7-160">[Analyze flight delay data using HDInsight](../hdinsight-analyze-flight-delay-data.md): Use Hive to analyze flight delay data, and then use Sqoop to export data to an Azure SQL database.</span></span>
* <span data-ttu-id="682c7-161">[Upload data to HDInsight](../hdinsight-upload-data.md): Find other methods for uploading data to HDInsight/Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="682c7-161">[Upload data to HDInsight](../hdinsight-upload-data.md): Find other methods for uploading data to HDInsight/Azure Blob storage.</span></span>

[hdinsight-versions]:  ../hdinsight-component-versioning.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]:apache-hadoop-linux-tutorial-get-started.md
[hdinsight-storage]: ../hdinsight-hadoop-use-blob-storage.md
[hdinsight-submit-jobs]:submit-apache-hadoop-jobs-programmatically.md
[sqldatabase-get-started]: ../sql-database-get-started.md
[sqldatabase-create-configue]: ../sql-database-create-configure.md

[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-install]: /powershell/azureps-cmdlets-docs
[powershell-script]: http://technet.microsoft.com/library/ee176949.aspx

[sqoop-user-guide-1.4.4]: https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html
