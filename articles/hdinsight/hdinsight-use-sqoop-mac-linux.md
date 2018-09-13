---
title: Use Hadoop Sqoop in Linux-based HDInsight | Microsoft Docs
description: Learn how to run Sqoop import and export between a Linux-based Hadoop on HDInsight cluster and an Azure SQL database.
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: ''
author: Blackmist
tags: azure-portal
ms.assetid: 303649a5-4be5-4933-bf1d-4b232083c354
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/14/2017
ms.author: larryfr
ms.openlocfilehash: 6bb8058a74d3417c4972a9010ac9e17739f3e323
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662027"
---
# <a name="use-sqoop-with-hadoop-in-hdinsight-ssh"></a><span data-ttu-id="6da4a-103">Use Sqoop with Hadoop in HDInsight (SSH)</span><span class="sxs-lookup"><span data-stu-id="6da4a-103">Use Sqoop with Hadoop in HDInsight (SSH)</span></span>

[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="6da4a-104">Learn how to use Sqoop to import and export between an HDInsight cluster and Azure SQL Database or SQL Server database.</span><span class="sxs-lookup"><span data-stu-id="6da4a-104">Learn how to use Sqoop to import and export between an HDInsight cluster and Azure SQL Database or SQL Server database.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6da4a-105">The steps in this document only work with HDInsight clusters that use Linux.</span><span class="sxs-lookup"><span data-stu-id="6da4a-105">The steps in this document only work with HDInsight clusters that use Linux.</span></span> <span data-ttu-id="6da4a-106">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="6da4a-106">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="6da4a-107">For more information, see [HDInsight component versioning](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span><span class="sxs-lookup"><span data-stu-id="6da4a-107">For more information, see [HDInsight component versioning](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span></span>

## <a name="install-freetds"></a><span data-ttu-id="6da4a-108">Install FreeTDS</span><span class="sxs-lookup"><span data-stu-id="6da4a-108">Install FreeTDS</span></span>

1. <span data-ttu-id="6da4a-109">Use SSH to connect to the Linux-based HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="6da4a-109">Use SSH to connect to the Linux-based HDInsight cluster.</span></span> <span data-ttu-id="6da4a-110">The address to use when connecting is `CLUSTERNAME-ssh.azurehdinsight.net` and the port is `22`.</span><span class="sxs-lookup"><span data-stu-id="6da4a-110">The address to use when connecting is `CLUSTERNAME-ssh.azurehdinsight.net` and the port is `22`.</span></span>

    <span data-ttu-id="6da4a-111">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="6da4a-111">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="6da4a-112">Use the following command to install FreeTDS:</span><span class="sxs-lookup"><span data-stu-id="6da4a-112">Use the following command to install FreeTDS:</span></span>

        sudo apt-get --assume-yes install freetds-dev freetds-bin

    <span data-ttu-id="6da4a-113">FreeTDS is used in several steps to connect to SQL Database.</span><span class="sxs-lookup"><span data-stu-id="6da4a-113">FreeTDS is used in several steps to connect to SQL Database.</span></span>

## <a name="create-the-table-in-sql-database"></a><span data-ttu-id="6da4a-114">Create the table in SQL Database</span><span class="sxs-lookup"><span data-stu-id="6da4a-114">Create the table in SQL Database</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6da4a-115">If you are using the HDInsight cluster and SQL Database created in [Create cluster and SQL database](hdinsight-use-sqoop.md), ignore the steps in this section.</span><span class="sxs-lookup"><span data-stu-id="6da4a-115">If you are using the HDInsight cluster and SQL Database created in [Create cluster and SQL database](hdinsight-use-sqoop.md), ignore the steps in this section.</span></span> <span data-ttu-id="6da4a-116">The database and table were created as part of the steps in the [Create cluster and SQL database](hdinsight-use-sqoop.md) document.</span><span class="sxs-lookup"><span data-stu-id="6da4a-116">The database and table were created as part of the steps in the [Create cluster and SQL database](hdinsight-use-sqoop.md) document.</span></span>

1. <span data-ttu-id="6da4a-117">From the SSH session, use the following command to connect to the SQL Database server.</span><span class="sxs-lookup"><span data-stu-id="6da4a-117">From the SSH session, use the following command to connect to the SQL Database server.</span></span>

        TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D sqooptest

    <span data-ttu-id="6da4a-118">You receive output similar to the following text:</span><span class="sxs-lookup"><span data-stu-id="6da4a-118">You receive output similar to the following text:</span></span>

        locale is "en_US.UTF-8"
        locale charset is "UTF-8"
        using default charset "UTF-8"
        Default database being set to sqooptest
        1>

2. <span data-ttu-id="6da4a-119">At the `1>` prompt, enter the following query:</span><span class="sxs-lookup"><span data-stu-id="6da4a-119">At the `1>` prompt, enter the following query:</span></span>

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

    <span data-ttu-id="6da4a-120">When the `GO` statement is entered, the previous statements are evaluated.</span><span class="sxs-lookup"><span data-stu-id="6da4a-120">When the `GO` statement is entered, the previous statements are evaluated.</span></span> <span data-ttu-id="6da4a-121">First, the **mobiledata** table is created, then a clustered index is added to it (required by SQL Database.)</span><span class="sxs-lookup"><span data-stu-id="6da4a-121">First, the **mobiledata** table is created, then a clustered index is added to it (required by SQL Database.)</span></span>

    <span data-ttu-id="6da4a-122">Use the following query to verify that the table has been created:</span><span class="sxs-lookup"><span data-stu-id="6da4a-122">Use the following query to verify that the table has been created:</span></span>

        SELECT * FROM information_schema.tables
        GO

    <span data-ttu-id="6da4a-123">You see output similar to the following text:</span><span class="sxs-lookup"><span data-stu-id="6da4a-123">You see output similar to the following text:</span></span>

        TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
        sqooptest       dbo     mobiledata      BASE TABLE

3. <span data-ttu-id="6da4a-124">Enter `exit` at the `1>` prompt to exit the tsql utility.</span><span class="sxs-lookup"><span data-stu-id="6da4a-124">Enter `exit` at the `1>` prompt to exit the tsql utility.</span></span>

## <a name="sqoop-export"></a><span data-ttu-id="6da4a-125">Sqoop export</span><span class="sxs-lookup"><span data-stu-id="6da4a-125">Sqoop export</span></span>

1. <span data-ttu-id="6da4a-126">From the SSH connection to HDInsight, se the following command to verify that Sqoop can see your SQL Database:</span><span class="sxs-lookup"><span data-stu-id="6da4a-126">From the SSH connection to HDInsight, se the following command to verify that Sqoop can see your SQL Database:</span></span>

        sqoop list-databases --connect jdbc:sqlserver://<serverName>.database.windows.net:1433 --username <adminLogin> --password <adminPassword>

    <span data-ttu-id="6da4a-127">This command returns a list of databases, including the **sqooptest** database that you created earlier.</span><span class="sxs-lookup"><span data-stu-id="6da4a-127">This command returns a list of databases, including the **sqooptest** database that you created earlier.</span></span>

2. <span data-ttu-id="6da4a-128">Use the following command to export data from **hivesampletable** to the **mobiledata** table:</span><span class="sxs-lookup"><span data-stu-id="6da4a-128">Use the following command to export data from **hivesampletable** to the **mobiledata** table:</span></span>

        sqoop export --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=sqooptest' --username <adminLogin> --password <adminPassword> --table 'mobiledata' --export-dir 'wasbs:///hive/warehouse/hivesampletable' --fields-terminated-by '\t' -m 1

    <span data-ttu-id="6da4a-129">This command instructs Sqoop to connect to the **sqooptest** database.</span><span class="sxs-lookup"><span data-stu-id="6da4a-129">This command instructs Sqoop to connect to the **sqooptest** database.</span></span> <span data-ttu-id="6da4a-130">Sqoop then exports data from **wasbs:///hive/warehouse/hivesampletable** to the **mobiledata** table.</span><span class="sxs-lookup"><span data-stu-id="6da4a-130">Sqoop then exports data from **wasbs:///hive/warehouse/hivesampletable** to the **mobiledata** table.</span></span>

3. <span data-ttu-id="6da4a-131">After the command completes, use the following command to connect to the database using TSQL:</span><span class="sxs-lookup"><span data-stu-id="6da4a-131">After the command completes, use the following command to connect to the database using TSQL:</span></span>

        TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D sqooptest

    <span data-ttu-id="6da4a-132">Once connected, use the following statements to verify that the data was exported to the **mobiledata** table:</span><span class="sxs-lookup"><span data-stu-id="6da4a-132">Once connected, use the following statements to verify that the data was exported to the **mobiledata** table:</span></span>

        SELECT * FROM mobiledata
        GO

    <span data-ttu-id="6da4a-133">You should see a listing of data in the table.</span><span class="sxs-lookup"><span data-stu-id="6da4a-133">You should see a listing of data in the table.</span></span> <span data-ttu-id="6da4a-134">Type `exit` to exit the tsql utility.</span><span class="sxs-lookup"><span data-stu-id="6da4a-134">Type `exit` to exit the tsql utility.</span></span>

## <a name="sqoop-import"></a><span data-ttu-id="6da4a-135">Sqoop import</span><span class="sxs-lookup"><span data-stu-id="6da4a-135">Sqoop import</span></span>

1. <span data-ttu-id="6da4a-136">Use the following command to import data from the **mobiledata** table in SQL Database, to the **wasbs:///tutorials/usesqoop/importeddata** directory on HDInsight:</span><span class="sxs-lookup"><span data-stu-id="6da4a-136">Use the following command to import data from the **mobiledata** table in SQL Database, to the **wasbs:///tutorials/usesqoop/importeddata** directory on HDInsight:</span></span>

        sqoop import --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=sqooptest' --username <adminLogin> --password <adminPassword> --table 'mobiledata' --target-dir 'wasbs:///tutorials/usesqoop/importeddata' --fields-terminated-by '\t' --lines-terminated-by '\n' -m 1

    <span data-ttu-id="6da4a-137">The fields in the data are separated by a tab character, and the lines are terminated by a new-line character.</span><span class="sxs-lookup"><span data-stu-id="6da4a-137">The fields in the data are separated by a tab character, and the lines are terminated by a new-line character.</span></span>

2. <span data-ttu-id="6da4a-138">Once the import has completed, use the following command to list out the data in the new directory:</span><span class="sxs-lookup"><span data-stu-id="6da4a-138">Once the import has completed, use the following command to list out the data in the new directory:</span></span>

        hadoop fs -text wasbs:///tutorials/usesqoop/importeddata/part-m-00000

## <a name="using-sql-server"></a><span data-ttu-id="6da4a-139">Using SQL Server</span><span class="sxs-lookup"><span data-stu-id="6da4a-139">Using SQL Server</span></span>

<span data-ttu-id="6da4a-140">You can also use Sqoop to import and export data from SQL Server, either in your data center or on a Virtual Machine hosted in Azure.</span><span class="sxs-lookup"><span data-stu-id="6da4a-140">You can also use Sqoop to import and export data from SQL Server, either in your data center or on a Virtual Machine hosted in Azure.</span></span> <span data-ttu-id="6da4a-141">The differences between using SQL Database and SQL Server are:</span><span class="sxs-lookup"><span data-stu-id="6da4a-141">The differences between using SQL Database and SQL Server are:</span></span>

* <span data-ttu-id="6da4a-142">Both HDInsight and the SQL Server must be on the same Azure Virtual Network</span><span class="sxs-lookup"><span data-stu-id="6da4a-142">Both HDInsight and the SQL Server must be on the same Azure Virtual Network</span></span>

  > [!NOTE]
  > <span data-ttu-id="6da4a-143">HDInsight supports only location-based virtual networks, and it does not currently work with affinity group-based virtual networks.</span><span class="sxs-lookup"><span data-stu-id="6da4a-143">HDInsight supports only location-based virtual networks, and it does not currently work with affinity group-based virtual networks.</span></span>

    <span data-ttu-id="6da4a-144">When you are using SQL Server in your datacenter, you must configure the virtual network as *site-to-site* or *point-to-site*.</span><span class="sxs-lookup"><span data-stu-id="6da4a-144">When you are using SQL Server in your datacenter, you must configure the virtual network as *site-to-site* or *point-to-site*.</span></span>

  > [!NOTE]
  > <span data-ttu-id="6da4a-145">When using a **point-to-site** virtual network, SQL Server must be running the VPN client configuration application.</span><span class="sxs-lookup"><span data-stu-id="6da4a-145">When using a **point-to-site** virtual network, SQL Server must be running the VPN client configuration application.</span></span> <span data-ttu-id="6da4a-146">The VPN client is available from the **Dashboard** of your Azure virtual network configuration.</span><span class="sxs-lookup"><span data-stu-id="6da4a-146">The VPN client is available from the **Dashboard** of your Azure virtual network configuration.</span></span>

    <span data-ttu-id="6da4a-147">For more information Azure Virtual Network, see [Virtual Network Overview](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6da4a-147">For more information Azure Virtual Network, see [Virtual Network Overview](../virtual-network/virtual-networks-overview.md).</span></span>

* <span data-ttu-id="6da4a-148">SQL Server must be configured to allow SQL authentication.</span><span class="sxs-lookup"><span data-stu-id="6da4a-148">SQL Server must be configured to allow SQL authentication.</span></span> <span data-ttu-id="6da4a-149">For more information, see the [Choose an Authentication Mode](https://msdn.microsoft.com/ms144284.aspx) document.</span><span class="sxs-lookup"><span data-stu-id="6da4a-149">For more information, see the [Choose an Authentication Mode](https://msdn.microsoft.com/ms144284.aspx) document.</span></span>

* <span data-ttu-id="6da4a-150">You may have to configure SQL Server to accept remote connections.</span><span class="sxs-lookup"><span data-stu-id="6da4a-150">You may have to configure SQL Server to accept remote connections.</span></span> <span data-ttu-id="6da4a-151">For more information, see the [How to troubleshoot connecting to the SQL Server database engine](http://social.technet.microsoft.com/wiki/contents/articles/2102.how-to-troubleshoot-connecting-to-the-sql-server-database-engine.aspx) document.</span><span class="sxs-lookup"><span data-stu-id="6da4a-151">For more information, see the [How to troubleshoot connecting to the SQL Server database engine](http://social.technet.microsoft.com/wiki/contents/articles/2102.how-to-troubleshoot-connecting-to-the-sql-server-database-engine.aspx) document.</span></span>

* <span data-ttu-id="6da4a-152">Create the **sqooptest** database in SQL Server using a utility such as **SQL Server Management Studio** or **tsql**.</span><span class="sxs-lookup"><span data-stu-id="6da4a-152">Create the **sqooptest** database in SQL Server using a utility such as **SQL Server Management Studio** or **tsql**.</span></span> <span data-ttu-id="6da4a-153">The steps for using the Azure CLI only work for Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="6da4a-153">The steps for using the Azure CLI only work for Azure SQL Database.</span></span>

    <span data-ttu-id="6da4a-154">Use the following TSQL statements to create the **mobiledata** table:</span><span class="sxs-lookup"><span data-stu-id="6da4a-154">Use the following TSQL statements to create the **mobiledata** table:</span></span>

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

* <span data-ttu-id="6da4a-155">When connecting to the SQL Server from HDInsight, you may have to use the IP address of the SQL Server.</span><span class="sxs-lookup"><span data-stu-id="6da4a-155">When connecting to the SQL Server from HDInsight, you may have to use the IP address of the SQL Server.</span></span> <span data-ttu-id="6da4a-156">For example:</span><span class="sxs-lookup"><span data-stu-id="6da4a-156">For example:</span></span>

        sqoop import --connect 'jdbc:sqlserver://10.0.1.1:1433;database=sqooptest' --username <adminLogin> --password <adminPassword> --table 'mobiledata' --target-dir 'wasbs:///tutorials/usesqoop/importeddata' --fields-terminated-by '\t' --lines-terminated-by '\n' -m 1

## <a name="limitations"></a><span data-ttu-id="6da4a-157">Limitations</span><span class="sxs-lookup"><span data-stu-id="6da4a-157">Limitations</span></span>

* <span data-ttu-id="6da4a-158">Bulk export - With Linux-based HDInsight, the Sqoop connector used to export data to Microsoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span><span class="sxs-lookup"><span data-stu-id="6da4a-158">Bulk export - With Linux-based HDInsight, the Sqoop connector used to export data to Microsoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>

* <span data-ttu-id="6da4a-159">Batching - With Linux-based HDInsight, When using the `-batch` switch when performing inserts, Sqoop makes multiple inserts instead of batching the insert operations.</span><span class="sxs-lookup"><span data-stu-id="6da4a-159">Batching - With Linux-based HDInsight, When using the `-batch` switch when performing inserts, Sqoop makes multiple inserts instead of batching the insert operations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6da4a-160">Next steps</span><span class="sxs-lookup"><span data-stu-id="6da4a-160">Next steps</span></span>

<span data-ttu-id="6da4a-161">Now you have learned how to use Sqoop.</span><span class="sxs-lookup"><span data-stu-id="6da4a-161">Now you have learned how to use Sqoop.</span></span> <span data-ttu-id="6da4a-162">To learn more, see:</span><span class="sxs-lookup"><span data-stu-id="6da4a-162">To learn more, see:</span></span>

* <span data-ttu-id="6da4a-163">[Use Oozie with HDInsight][hdinsight-use-oozie]: Use Sqoop action in an Oozie workflow.</span><span class="sxs-lookup"><span data-stu-id="6da4a-163">[Use Oozie with HDInsight][hdinsight-use-oozie]: Use Sqoop action in an Oozie workflow.</span></span>
* <span data-ttu-id="6da4a-164">[Analyze flight delay data using HDInsight][hdinsight-analyze-flight-data]: Use Hive to analyze flight delay data, and then use Sqoop to export data to an Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="6da4a-164">[Analyze flight delay data using HDInsight][hdinsight-analyze-flight-data]: Use Hive to analyze flight delay data, and then use Sqoop to export data to an Azure SQL database.</span></span>
* <span data-ttu-id="6da4a-165">[Upload data to HDInsight][hdinsight-upload-data]: Find other methods for uploading data to HDInsight/Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="6da4a-165">[Upload data to HDInsight][hdinsight-upload-data]: Find other methods for uploading data to HDInsight/Azure Blob storage.</span></span>

[hdinsight-versions]:  hdinsight-component-versioning.md
[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-storage]: ../hdinsight-hadoop-use-blob-storage.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md

[sqldatabase-get-started]: ../sql-database-get-started.md
[sqldatabase-create-configue]: ../sql-database-create-configure.md

[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-install]: /powershell/azureps-cmdlets-docs
[powershell-script]: http://technet.microsoft.com/library/ee176949.aspx

[sqoop-user-guide-1.4.4]: https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html
