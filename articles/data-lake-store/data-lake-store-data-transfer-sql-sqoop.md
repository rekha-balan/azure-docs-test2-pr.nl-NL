---
title: Copy data between Data Lake Store and Azure SQL database using Sqoop | Microsoft Docs
description: Use Sqoop to copy data between Azure SQL Database and Data Lake Store
services: data-lake-store
documentationcenter: ''
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 3f914b2a-83cc-4950-b3f7-69c921851683
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/06/2017
ms.author: nitinme
ms.openlocfilehash: 7f165111cd089d5f32f309235dcbc24d11fb5d64
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563321"
---
# <a name="copy-data-between-data-lake-store-and-azure-sql-database-using-sqoop"></a><span data-ttu-id="2b955-103">Copy data between Data Lake Store and Azure SQL database using Sqoop</span><span class="sxs-lookup"><span data-stu-id="2b955-103">Copy data between Data Lake Store and Azure SQL database using Sqoop</span></span>
<span data-ttu-id="2b955-104">Learn how to use Apache Sqoop to import and export data between Azure SQL Database and Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="2b955-104">Learn how to use Apache Sqoop to import and export data between Azure SQL Database and Data Lake Store.</span></span>

## <a name="what-is-sqoop"></a><span data-ttu-id="2b955-105">What is Sqoop?</span><span class="sxs-lookup"><span data-stu-id="2b955-105">What is Sqoop?</span></span>
<span data-ttu-id="2b955-106">Big data applications are a natural choice for processing unstructured and semi-structured data, such as logs and files.</span><span class="sxs-lookup"><span data-stu-id="2b955-106">Big data applications are a natural choice for processing unstructured and semi-structured data, such as logs and files.</span></span> <span data-ttu-id="2b955-107">However, there may also be a need to process structured data that is stored in relational databases.</span><span class="sxs-lookup"><span data-stu-id="2b955-107">However, there may also be a need to process structured data that is stored in relational databases.</span></span>

<span data-ttu-id="2b955-108">[Apache Sqoop](https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html) is a tool designed to transfer data between  relational databases and a big data repository, such as Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="2b955-108">[Apache Sqoop](https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html) is a tool designed to transfer data between  relational databases and a big data repository, such as Data Lake Store.</span></span> <span data-ttu-id="2b955-109">You can use it to import data from a relational database management system (RDBMS) such as Azure SQL Database into Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="2b955-109">You can use it to import data from a relational database management system (RDBMS) such as Azure SQL Database into Data Lake Store.</span></span> <span data-ttu-id="2b955-110">You can then transform and analyze the data using big data workloads and then export the data back into an RDBMS.</span><span class="sxs-lookup"><span data-stu-id="2b955-110">You can then transform and analyze the data using big data workloads and then export the data back into an RDBMS.</span></span> <span data-ttu-id="2b955-111">In this tutorial, you use an Azure SQL Database as your relational database to import/export from.</span><span class="sxs-lookup"><span data-stu-id="2b955-111">In this tutorial, you use an Azure SQL Database as your relational database to import/export from.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2b955-112">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="2b955-112">Prerequisites</span></span>
<span data-ttu-id="2b955-113">Before you begin this article, you must have the following:</span><span class="sxs-lookup"><span data-stu-id="2b955-113">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="2b955-114">**An Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="2b955-114">**An Azure subscription**.</span></span> <span data-ttu-id="2b955-115">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2b955-115">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="2b955-116">**An Azure Data Lake Store account**.</span><span class="sxs-lookup"><span data-stu-id="2b955-116">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="2b955-117">For instructions on how to create one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="2b955-117">For instructions on how to create one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>
* <span data-ttu-id="2b955-118">**Azure HDInsight cluster** with access to a Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="2b955-118">**Azure HDInsight cluster** with access to a Data Lake Store account.</span></span> <span data-ttu-id="2b955-119">See [Create an HDInsight cluster with Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="2b955-119">See [Create an HDInsight cluster with Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md).</span></span> <span data-ttu-id="2b955-120">This article assumes you have an HDInsight Linux cluster with Data Lake Store access.</span><span class="sxs-lookup"><span data-stu-id="2b955-120">This article assumes you have an HDInsight Linux cluster with Data Lake Store access.</span></span>
* <span data-ttu-id="2b955-121">**Azure SQL Database**.</span><span class="sxs-lookup"><span data-stu-id="2b955-121">**Azure SQL Database**.</span></span> <span data-ttu-id="2b955-122">For instructions on how to create one, see [Create an Azure SQL database](../sql-database/sql-database-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="2b955-122">For instructions on how to create one, see [Create an Azure SQL database](../sql-database/sql-database-get-started.md)</span></span>

## <a name="do-you-learn-fast-with-videos"></a><span data-ttu-id="2b955-123">Do you learn fast with videos?</span><span class="sxs-lookup"><span data-stu-id="2b955-123">Do you learn fast with videos?</span></span>
<span data-ttu-id="2b955-124">[Watch this video](https://mix.office.com/watch/1butcdjxmu114) on how to copy data between Azure Storage Blobs and Data Lake Store using DistCp.</span><span class="sxs-lookup"><span data-stu-id="2b955-124">[Watch this video](https://mix.office.com/watch/1butcdjxmu114) on how to copy data between Azure Storage Blobs and Data Lake Store using DistCp.</span></span>

## <a name="create-sample-tables-in-the-azure-sql-database"></a><span data-ttu-id="2b955-125">Create sample tables in the Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="2b955-125">Create sample tables in the Azure SQL Database</span></span>
1. <span data-ttu-id="2b955-126">To start with, create two sample tables in the Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="2b955-126">To start with, create two sample tables in the Azure SQL Database.</span></span> <span data-ttu-id="2b955-127">Use [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) or Visual Studio to connect to the Azure SQL Database and then run the following queries.</span><span class="sxs-lookup"><span data-stu-id="2b955-127">Use [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) or Visual Studio to connect to the Azure SQL Database and then run the following queries.</span></span>

    <span data-ttu-id="2b955-128">**Create Table1**</span><span class="sxs-lookup"><span data-stu-id="2b955-128">**Create Table1**</span></span>

        CREATE TABLE [dbo].[Table1](
        [ID] [int] NOT NULL,
        [FName] [nvarchar](50) NOT NULL,
        [LName] [nvarchar](50) NOT NULL,
         CONSTRAINT [PK_Table_4] PRIMARY KEY CLUSTERED
            (
                   [ID] ASC
            )
        ) ON [PRIMARY]
        GO

    <span data-ttu-id="2b955-129">**Create Table2**</span><span class="sxs-lookup"><span data-stu-id="2b955-129">**Create Table2**</span></span>

        CREATE TABLE [dbo].[Table2](
        [ID] [int] NOT NULL,
        [FName] [nvarchar](50) NOT NULL,
        [LName] [nvarchar](50) NOT NULL,
         CONSTRAINT [PK_Table_4] PRIMARY KEY CLUSTERED
            (
                   [ID] ASC
            )
        ) ON [PRIMARY]
        GO
2. <span data-ttu-id="2b955-130">In **Table1**, add some sample data.</span><span class="sxs-lookup"><span data-stu-id="2b955-130">In **Table1**, add some sample data.</span></span> <span data-ttu-id="2b955-131">Leave **Table2** empty.</span><span class="sxs-lookup"><span data-stu-id="2b955-131">Leave **Table2** empty.</span></span> <span data-ttu-id="2b955-132">We will import data from **Table1** into Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="2b955-132">We will import data from **Table1** into Data Lake Store.</span></span> <span data-ttu-id="2b955-133">Then, we will export data from Data Lake Store into **Table2**.</span><span class="sxs-lookup"><span data-stu-id="2b955-133">Then, we will export data from Data Lake Store into **Table2**.</span></span> <span data-ttu-id="2b955-134">Run the following snippet.</span><span class="sxs-lookup"><span data-stu-id="2b955-134">Run the following snippet.</span></span>

        INSERT INTO [dbo].[Table1] VALUES (1,'Neal','Kell'), (2,'Lila','Fulton'), (3, 'Erna','Myers'), (4,'Annette','Simpson');


## <a name="use-sqoop-from-an-hdinsight-cluster-with-access-to-data-lake-store"></a><span data-ttu-id="2b955-135">Use Sqoop from an HDInsight cluster with access to Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="2b955-135">Use Sqoop from an HDInsight cluster with access to Data Lake Store</span></span>
<span data-ttu-id="2b955-136">An HDInsight cluster already has the Sqoop packages available.</span><span class="sxs-lookup"><span data-stu-id="2b955-136">An HDInsight cluster already has the Sqoop packages available.</span></span> <span data-ttu-id="2b955-137">If you have configured the HDInsight cluster to use Data Lake Store as an additional storage, you can use Sqoop (without any configuration changes) to import/export data between a relational database (in this example, Azure SQL Database) and a Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="2b955-137">If you have configured the HDInsight cluster to use Data Lake Store as an additional storage, you can use Sqoop (without any configuration changes) to import/export data between a relational database (in this example, Azure SQL Database) and a Data Lake Store account.</span></span>

1. <span data-ttu-id="2b955-138">For this tutorial, we assume you created a Linux cluster so you should use SSH to connect to the cluster.</span><span class="sxs-lookup"><span data-stu-id="2b955-138">For this tutorial, we assume you created a Linux cluster so you should use SSH to connect to the cluster.</span></span> <span data-ttu-id="2b955-139">See [Connect to a Linux-based HDInsight cluster](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="2b955-139">See [Connect to a Linux-based HDInsight cluster](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>
2. <span data-ttu-id="2b955-140">Verify whether you can access the Data Lake Store account from the cluster.</span><span class="sxs-lookup"><span data-stu-id="2b955-140">Verify whether you can access the Data Lake Store account from the cluster.</span></span> <span data-ttu-id="2b955-141">Run the following command from the SSH prompt:</span><span class="sxs-lookup"><span data-stu-id="2b955-141">Run the following command from the SSH prompt:</span></span>

        hdfs dfs -ls adl://<data_lake_store_account>.azuredatalakestore.net/

    <span data-ttu-id="2b955-142">This should provide a list of files/folders in the Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="2b955-142">This should provide a list of files/folders in the Data Lake Store account.</span></span>

### <a name="import-data-from-azure-sql-database-into-data-lake-store"></a><span data-ttu-id="2b955-143">Import data from Azure SQL Database into Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="2b955-143">Import data from Azure SQL Database into Data Lake Store</span></span>
1. <span data-ttu-id="2b955-144">Navigate to the directory where Sqoop packages are available.</span><span class="sxs-lookup"><span data-stu-id="2b955-144">Navigate to the directory where Sqoop packages are available.</span></span> <span data-ttu-id="2b955-145">Typically, this will be at `/usr/hdp/<version>/sqoop/bin`.</span><span class="sxs-lookup"><span data-stu-id="2b955-145">Typically, this will be at `/usr/hdp/<version>/sqoop/bin`.</span></span>
2. <span data-ttu-id="2b955-146">Import the data from **Table1** into the Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="2b955-146">Import the data from **Table1** into the Data Lake Store account.</span></span> <span data-ttu-id="2b955-147">Use the following syntax:</span><span class="sxs-lookup"><span data-stu-id="2b955-147">Use the following syntax:</span></span>

        sqoop-import --connect "jdbc:sqlserver://<sql-database-server-name>.database.windows.net:1433;username=<username>@<sql-database-server-name>;password=<password>;database=<sql-database-name>" --table Table1 --target-dir adl://<data-lake-store-name>.azuredatalakestore.net/Sqoop/SqoopImportTable1

    <span data-ttu-id="2b955-148">Note that **sql-database-server-name** placeholder represents the name of the server where the Azure SQL database is running.</span><span class="sxs-lookup"><span data-stu-id="2b955-148">Note that **sql-database-server-name** placeholder represents the name of the server where the Azure SQL database is running.</span></span> <span data-ttu-id="2b955-149">**sql-database-name** placeholder represents the actual database name.</span><span class="sxs-lookup"><span data-stu-id="2b955-149">**sql-database-name** placeholder represents the actual database name.</span></span>

    <span data-ttu-id="2b955-150">For example,</span><span class="sxs-lookup"><span data-stu-id="2b955-150">For example,</span></span>


        sqoop-import --connect "jdbc:sqlserver://mysqoopserver.database.windows.net:1433;username=nitinme@mysqoopserver;password=<password>;database=mysqoopdatabase" --table Table1 --target-dir adl://myadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1

1. <span data-ttu-id="2b955-151">Verify that the data has been transferred to the Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="2b955-151">Verify that the data has been transferred to the Data Lake Store account.</span></span> <span data-ttu-id="2b955-152">Run the following command:</span><span class="sxs-lookup"><span data-stu-id="2b955-152">Run the following command:</span></span>

        hdfs dfs -ls adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/

    <span data-ttu-id="2b955-153">You should see the following output.</span><span class="sxs-lookup"><span data-stu-id="2b955-153">You should see the following output.</span></span>


        -rwxrwxrwx   0 sshuser hdfs          0 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/_SUCCESS
        -rwxrwxrwx   0 sshuser hdfs         12 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00000
        -rwxrwxrwx   0 sshuser hdfs         14 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00001
        -rwxrwxrwx   0 sshuser hdfs         13 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00002
        -rwxrwxrwx   0 sshuser hdfs         18 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00003

    <span data-ttu-id="2b955-154">Each **part-m-**\* file corresponds to a row in the source table, **Table1**.</span><span class="sxs-lookup"><span data-stu-id="2b955-154">Each **part-m-**\* file corresponds to a row in the source table, **Table1**.</span></span> <span data-ttu-id="2b955-155">You can view the contents of the part-m-\* files to verify.</span><span class="sxs-lookup"><span data-stu-id="2b955-155">You can view the contents of the part-m-\* files to verify.</span></span>


### <a name="export-data-from-data-lake-store-into-azure-sql-database"></a><span data-ttu-id="2b955-156">Export data from Data Lake Store into Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="2b955-156">Export data from Data Lake Store into Azure SQL Database</span></span>
1. <span data-ttu-id="2b955-157">Export the data from Data Lake Store account to the empty table, **Table2**, in the Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="2b955-157">Export the data from Data Lake Store account to the empty table, **Table2**, in the Azure SQL Database.</span></span> <span data-ttu-id="2b955-158">Use the following syntax.</span><span class="sxs-lookup"><span data-stu-id="2b955-158">Use the following syntax.</span></span>

        sqoop-export --connect "jdbc:sqlserver://<sql-database-server-name>.database.windows.net:1433;username=<username>@<sql-database-server-name>;password=<password>;database=<sql-database-name>" --table Table2 --export-dir adl://<data-lake-store-name>.azuredatalakestore.net/Sqoop/SqoopImportTable1 --input-fields-terminated-by ","

    <span data-ttu-id="2b955-159">For example,</span><span class="sxs-lookup"><span data-stu-id="2b955-159">For example,</span></span>


        sqoop-export --connect "jdbc:sqlserver://mysqoopserver.database.windows.net:1433;username=nitinme@mysqoopserver;password=<password>;database=mysqoopdatabase" --table Table2 --export-dir adl://myadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1 --input-fields-terminated-by ","

1. <span data-ttu-id="2b955-160">Verify that the data was uploaded to the SQL Database table.</span><span class="sxs-lookup"><span data-stu-id="2b955-160">Verify that the data was uploaded to the SQL Database table.</span></span> <span data-ttu-id="2b955-161">Use [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) or Visual Studio to connect to the Azure SQL Database and then run the following query.</span><span class="sxs-lookup"><span data-stu-id="2b955-161">Use [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) or Visual Studio to connect to the Azure SQL Database and then run the following query.</span></span>

        SELECT * FROM TABLE2

    <span data-ttu-id="2b955-162">This should have the following output.</span><span class="sxs-lookup"><span data-stu-id="2b955-162">This should have the following output.</span></span>

         ID  FName   LName
        ------------------
        1    Neal    Kell
        2    Lila    Fulton
        3    Erna    Myers
        4    Annette    Simpson

## <a name="performance-considerations-while-using-sqoop"></a><span data-ttu-id="2b955-163">Performance considerations while using Sqoop</span><span class="sxs-lookup"><span data-stu-id="2b955-163">Performance considerations while using Sqoop</span></span>

<span data-ttu-id="2b955-164">For performance tuning your Sqoop job to copy data to Data Lake Store, see [Sqoop performance document](https://blogs.msdn.microsoft.com/bigdatasupport/2015/02/17/sqoop-job-performance-tuning-in-hdinsight-hadoop/).</span><span class="sxs-lookup"><span data-stu-id="2b955-164">For performance tuning your Sqoop job to copy data to Data Lake Store, see [Sqoop performance document](https://blogs.msdn.microsoft.com/bigdatasupport/2015/02/17/sqoop-job-performance-tuning-in-hdinsight-hadoop/).</span></span>

## <a name="see-also"></a><span data-ttu-id="2b955-165">See also</span><span class="sxs-lookup"><span data-stu-id="2b955-165">See also</span></span>
* [<span data-ttu-id="2b955-166">Copy data from Azure Storage Blobs to Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="2b955-166">Copy data from Azure Storage Blobs to Data Lake Store</span></span>](data-lake-store-copy-data-azure-storage-blob.md)
* [<span data-ttu-id="2b955-167">Secure data in Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="2b955-167">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="2b955-168">Use Azure Data Lake Analytics with Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="2b955-168">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="2b955-169">Use Azure HDInsight with Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="2b955-169">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
