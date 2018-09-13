---
title: Use Apache Spark to read and write data to Azure SQL database
description: Learn how to set up a connection between HDInsight Spark cluster and an Azure SQL database to read data, write data, and stream data into a SQL database
services: hdinsight
author: jasonwhowell
ms.author: jasonh
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 05/01/2018
ms.openlocfilehash: 2aec894da6b4e5ffd59fee12bc8476b25955c991
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864436"
---
# <a name="use-hdinsight-spark-cluster-to-read-and-write-data-to-azure-sql-database"></a><span data-ttu-id="dbd23-103">Use HDInsight Spark cluster to read and write data to Azure SQL database</span><span class="sxs-lookup"><span data-stu-id="dbd23-103">Use HDInsight Spark cluster to read and write data to Azure SQL database</span></span>

<span data-ttu-id="dbd23-104">Learn how to connect an Apache Spark cluster in Azure HDInsight with an Azure SQL database and then read, write, and stream data into the SQL database.</span><span class="sxs-lookup"><span data-stu-id="dbd23-104">Learn how to connect an Apache Spark cluster in Azure HDInsight with an Azure SQL database and then read, write, and stream data into the SQL database.</span></span> <span data-ttu-id="dbd23-105">The instructions in this article use a Jupyter notebook to run the Scala code snippets.</span><span class="sxs-lookup"><span data-stu-id="dbd23-105">The instructions in this article use a Jupyter notebook to run the Scala code snippets.</span></span> <span data-ttu-id="dbd23-106">However, you can create a standalone application in Scala or Python and perform the same tasks.</span><span class="sxs-lookup"><span data-stu-id="dbd23-106">However, you can create a standalone application in Scala or Python and perform the same tasks.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="dbd23-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="dbd23-107">Prerequisites</span></span>

* <span data-ttu-id="dbd23-108">**Azure HDInsight Spark cluster**.</span><span class="sxs-lookup"><span data-stu-id="dbd23-108">**Azure HDInsight Spark cluster**.</span></span>  <span data-ttu-id="dbd23-109">Follow the instructions at [Create an Apache Spark cluster in HDInsight](apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="dbd23-109">Follow the instructions at [Create an Apache Spark cluster in HDInsight](apache-spark-jupyter-spark-sql.md).</span></span>

* <span data-ttu-id="dbd23-110">**Azure SQL database**.</span><span class="sxs-lookup"><span data-stu-id="dbd23-110">**Azure SQL database**.</span></span> <span data-ttu-id="dbd23-111">Follow the instructions at [Create an Azure SQL database](../../sql-database/sql-database-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="dbd23-111">Follow the instructions at [Create an Azure SQL database](../../sql-database/sql-database-get-started-portal.md).</span></span> <span data-ttu-id="dbd23-112">Make sure you create a database with the sample **AdventureWorksLT** schema and data.</span><span class="sxs-lookup"><span data-stu-id="dbd23-112">Make sure you create a database with the sample **AdventureWorksLT** schema and data.</span></span> <span data-ttu-id="dbd23-113">Also, make sure you create a server-level firewall rule to allow your client's IP address to access the SQL database on the server.</span><span class="sxs-lookup"><span data-stu-id="dbd23-113">Also, make sure you create a server-level firewall rule to allow your client's IP address to access the SQL database on the server.</span></span> <span data-ttu-id="dbd23-114">The instructions to add the firewall rule is available in the same article.</span><span class="sxs-lookup"><span data-stu-id="dbd23-114">The instructions to add the firewall rule is available in the same article.</span></span> <span data-ttu-id="dbd23-115">Once you have created your Azure SQL database, make sure you keep the following values handy.</span><span class="sxs-lookup"><span data-stu-id="dbd23-115">Once you have created your Azure SQL database, make sure you keep the following values handy.</span></span> <span data-ttu-id="dbd23-116">You need them to connect to the database from a Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="dbd23-116">You need them to connect to the database from a Spark cluster.</span></span>

    * <span data-ttu-id="dbd23-117">Server name hosting the Azure SQL database</span><span class="sxs-lookup"><span data-stu-id="dbd23-117">Server name hosting the Azure SQL database</span></span>
    * <span data-ttu-id="dbd23-118">Azure SQL database name</span><span class="sxs-lookup"><span data-stu-id="dbd23-118">Azure SQL database name</span></span>
    * <span data-ttu-id="dbd23-119">Azure SQL database admin user name / password</span><span class="sxs-lookup"><span data-stu-id="dbd23-119">Azure SQL database admin user name / password</span></span>

* <span data-ttu-id="dbd23-120">**SQL Server Management Studio**.</span><span class="sxs-lookup"><span data-stu-id="dbd23-120">**SQL Server Management Studio**.</span></span> <span data-ttu-id="dbd23-121">Follow the instructions at [Use SSMS to connect and query data](../../sql-database/sql-database-connect-query-ssms.md).</span><span class="sxs-lookup"><span data-stu-id="dbd23-121">Follow the instructions at [Use SSMS to connect and query data](../../sql-database/sql-database-connect-query-ssms.md).</span></span>

## <a name="create-a-jupyter-notebook"></a><span data-ttu-id="dbd23-122">Create a Jupyter notebook</span><span class="sxs-lookup"><span data-stu-id="dbd23-122">Create a Jupyter notebook</span></span>

<span data-ttu-id="dbd23-123">Start by creating a Jupyter notebook associated with the Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="dbd23-123">Start by creating a Jupyter notebook associated with the Spark cluster.</span></span> <span data-ttu-id="dbd23-124">You use this notebook to run the code snippets used in this article.</span><span class="sxs-lookup"><span data-stu-id="dbd23-124">You use this notebook to run the code snippets used in this article.</span></span> 

1. <span data-ttu-id="dbd23-125">From the [Azure portal](https://portal.azure.com/), open your cluster.</span><span class="sxs-lookup"><span data-stu-id="dbd23-125">From the [Azure portal](https://portal.azure.com/), open your cluster.</span></span> 

1. <span data-ttu-id="dbd23-126">From the **Quick links** section, click **Cluster dashboards** to open the **Cluster dashboards** view.</span><span class="sxs-lookup"><span data-stu-id="dbd23-126">From the **Quick links** section, click **Cluster dashboards** to open the **Cluster dashboards** view.</span></span>  <span data-ttu-id="dbd23-127">If you don't see **Quick Links**, click **Overview** from the left menu on the blade.</span><span class="sxs-lookup"><span data-stu-id="dbd23-127">If you don't see **Quick Links**, click **Overview** from the left menu on the blade.</span></span>

    <span data-ttu-id="dbd23-128">![Cluster dashboard on Spark](./media/apache-spark-connect-to-sql-database/hdinsight-cluster-dashboard-on-spark.png "Cluster dashboard on Spark")</span><span class="sxs-lookup"><span data-stu-id="dbd23-128">![Cluster dashboard on Spark](./media/apache-spark-connect-to-sql-database/hdinsight-cluster-dashboard-on-spark.png "Cluster dashboard on Spark")</span></span> 

1. <span data-ttu-id="dbd23-129">Click **Jupyter Notebook**.</span><span class="sxs-lookup"><span data-stu-id="dbd23-129">Click **Jupyter Notebook**.</span></span> <span data-ttu-id="dbd23-130">If prompted, enter the admin credentials for the cluster.</span><span class="sxs-lookup"><span data-stu-id="dbd23-130">If prompted, enter the admin credentials for the cluster.</span></span>

    <span data-ttu-id="dbd23-131">![Jupyter notebook on Spark](./media/apache-spark-connect-to-sql-database/hdinsight-jupyter-notebook-on-spark.png "Jupyter notebook on Spark")</span><span class="sxs-lookup"><span data-stu-id="dbd23-131">![Jupyter notebook on Spark](./media/apache-spark-connect-to-sql-database/hdinsight-jupyter-notebook-on-spark.png "Jupyter notebook on Spark")</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="dbd23-132">You can also access the Jupyter notebook on Spark cluster by opening the following URL in your browser.</span><span class="sxs-lookup"><span data-stu-id="dbd23-132">You can also access the Jupyter notebook on Spark cluster by opening the following URL in your browser.</span></span> <span data-ttu-id="dbd23-133">Replace **CLUSTERNAME** with the name of your cluster:</span><span class="sxs-lookup"><span data-stu-id="dbd23-133">Replace **CLUSTERNAME** with the name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   > 
   > 

1. <span data-ttu-id="dbd23-134">In the Jupyter notebook, from the top-right corner, click **New**, and then click **Spark** to create a Scala notebook.</span><span class="sxs-lookup"><span data-stu-id="dbd23-134">In the Jupyter notebook, from the top-right corner, click **New**, and then click **Spark** to create a Scala notebook.</span></span> <span data-ttu-id="dbd23-135">Jupyter notebooks on HDInsight Spark cluster also provide the **PySpark** kernel for Python2 applications, and the **PySpark3** kernel for Python3 applications.</span><span class="sxs-lookup"><span data-stu-id="dbd23-135">Jupyter notebooks on HDInsight Spark cluster also provide the **PySpark** kernel for Python2 applications, and the **PySpark3** kernel for Python3 applications.</span></span> <span data-ttu-id="dbd23-136">For this article, we create a Scala notebook.</span><span class="sxs-lookup"><span data-stu-id="dbd23-136">For this article, we create a Scala notebook.</span></span>
   
    <span data-ttu-id="dbd23-137">![Kernels for Jupyter notebook on Spark](./media/apache-spark-connect-to-sql-database/kernel-jupyter-notebook-on-spark.png "Kernels for Jupyter notebook on Spark")</span><span class="sxs-lookup"><span data-stu-id="dbd23-137">![Kernels for Jupyter notebook on Spark](./media/apache-spark-connect-to-sql-database/kernel-jupyter-notebook-on-spark.png "Kernels for Jupyter notebook on Spark")</span></span>

    <span data-ttu-id="dbd23-138">For more information about the kernels, see [Use Jupyter notebook kernels with Apache Spark clusters in HDInsight](apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="dbd23-138">For more information about the kernels, see [Use Jupyter notebook kernels with Apache Spark clusters in HDInsight](apache-spark-jupyter-notebook-kernels.md).</span></span>

   > [!NOTE]
   > <span data-ttu-id="dbd23-139">In this article, we use a Spark (Scala) kernel because streaming data from Spark into SQL database is only supported in Scala and Java currently.</span><span class="sxs-lookup"><span data-stu-id="dbd23-139">In this article, we use a Spark (Scala) kernel because streaming data from Spark into SQL database is only supported in Scala and Java currently.</span></span> <span data-ttu-id="dbd23-140">Even though reading from and writing into SQL can be done using Python, for consistency in this article, we use Scala for all three operations.</span><span class="sxs-lookup"><span data-stu-id="dbd23-140">Even though reading from and writing into SQL can be done using Python, for consistency in this article, we use Scala for all three operations.</span></span>
   >

1. <span data-ttu-id="dbd23-141">This opens a new notebook with a default name, **Untitled**.</span><span class="sxs-lookup"><span data-stu-id="dbd23-141">This opens a new notebook with a default name, **Untitled**.</span></span> <span data-ttu-id="dbd23-142">Click the notebook name and enter a name of your choice.</span><span class="sxs-lookup"><span data-stu-id="dbd23-142">Click the notebook name and enter a name of your choice.</span></span>

    <span data-ttu-id="dbd23-143">![Provide a name for the notebook](./media/apache-spark-connect-to-sql-database/hdinsight-spark-jupyter-notebook-name.png "Provide a name for the notebook")</span><span class="sxs-lookup"><span data-stu-id="dbd23-143">![Provide a name for the notebook](./media/apache-spark-connect-to-sql-database/hdinsight-spark-jupyter-notebook-name.png "Provide a name for the notebook")</span></span>

<span data-ttu-id="dbd23-144">You can now start creating your application.</span><span class="sxs-lookup"><span data-stu-id="dbd23-144">You can now start creating your application.</span></span>
    
## <a name="read-data-from-azure-sql-database"></a><span data-ttu-id="dbd23-145">Read data from Azure SQL database</span><span class="sxs-lookup"><span data-stu-id="dbd23-145">Read data from Azure SQL database</span></span>

<span data-ttu-id="dbd23-146">In this section, you read data from a table (for example, **SalesLT.Address**) that exists in the AdventureWorks database.</span><span class="sxs-lookup"><span data-stu-id="dbd23-146">In this section, you read data from a table (for example, **SalesLT.Address**) that exists in the AdventureWorks database.</span></span>

1. <span data-ttu-id="dbd23-147">In a new Jupyter notebook, in a code cell, paste the following snippet and replace the placeholder values with the values for your Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="dbd23-147">In a new Jupyter notebook, in a code cell, paste the following snippet and replace the placeholder values with the values for your Azure SQL database.</span></span>

       // Declare the values for your Azure SQL database

       val jdbcUsername = "<SQL DB ADMIN USER>"
       val jdbcPassword = "<SQL DB ADMIN PWD>"
       val jdbcHostname = "<SQL SERVER NAME HOSTING SDL DB>" //typically, this is in the form or servername.database.windows.net
       val jdbcPort = 1433
       val jdbcDatabase ="<AZURE SQL DB NAME>"

    <span data-ttu-id="dbd23-148">Press **SHIFT + ENTER** to run the code cell.</span><span class="sxs-lookup"><span data-stu-id="dbd23-148">Press **SHIFT + ENTER** to run the code cell.</span></span>  

1. <span data-ttu-id="dbd23-149">Use the snippet below to build a JDBC URL that you can pass to the Spark dataframe APIs creates an `Properties` object to hold the parameters.</span><span class="sxs-lookup"><span data-stu-id="dbd23-149">Use the snippet below to build a JDBC URL that you can pass to the Spark dataframe APIs creates an `Properties` object to hold the parameters.</span></span> <span data-ttu-id="dbd23-150">Paste the snippet in a code cell and press **SHIFT + ENTER** to run.</span><span class="sxs-lookup"><span data-stu-id="dbd23-150">Paste the snippet in a code cell and press **SHIFT + ENTER** to run.</span></span>

       import java.util.Properties

       val jdbc_url = s"jdbc:sqlserver://${jdbcHostname}:${jdbcPort};database=${jdbcDatabase};encrypt=true;trustServerCertificate=false;hostNameInCertificate=*.database.windows.net;loginTimeout=60;"
       val connectionProperties = new Properties()
       connectionProperties.put("user", s"${jdbcUsername}")
       connectionProperties.put("password", s"${jdbcPassword}")         

1. <span data-ttu-id="dbd23-151">Use the snippet below to create a dataframe with the data from a table in your Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="dbd23-151">Use the snippet below to create a dataframe with the data from a table in your Azure SQL database.</span></span> <span data-ttu-id="dbd23-152">In this snippet, we use a **SalesLT.Address** table that is available as part of the **AdventureWorksLT** database.</span><span class="sxs-lookup"><span data-stu-id="dbd23-152">In this snippet, we use a **SalesLT.Address** table that is available as part of the **AdventureWorksLT** database.</span></span> <span data-ttu-id="dbd23-153">Paste the snippet in a code cell and press **SHIFT + ENTER** to run.</span><span class="sxs-lookup"><span data-stu-id="dbd23-153">Paste the snippet in a code cell and press **SHIFT + ENTER** to run.</span></span>

       val sqlTableDF = spark.read.jdbc(jdbc_url, "SalesLT.Address", connectionProperties)

1. <span data-ttu-id="dbd23-154">You can now perform operations on the dataframe, such as getting the data schema:</span><span class="sxs-lookup"><span data-stu-id="dbd23-154">You can now perform operations on the dataframe, such as getting the data schema:</span></span>

       sqlTableDF.printSchema
   
    <span data-ttu-id="dbd23-155">You see an output similar to the following:</span><span class="sxs-lookup"><span data-stu-id="dbd23-155">You see an output similar to the following:</span></span>

    <span data-ttu-id="dbd23-156">![Provide a name for the notebook](./media/apache-spark-connect-to-sql-database/read-from-sql-schema-output.png "Provide a name for the notebook")</span><span class="sxs-lookup"><span data-stu-id="dbd23-156">![Provide a name for the notebook](./media/apache-spark-connect-to-sql-database/read-from-sql-schema-output.png "Provide a name for the notebook")</span></span>

1. <span data-ttu-id="dbd23-157">You can also perform operations like, retrieve the top 10 rows.</span><span class="sxs-lookup"><span data-stu-id="dbd23-157">You can also perform operations like, retrieve the top 10 rows.</span></span>

       sqlTableDF.show(10)

1. <span data-ttu-id="dbd23-158">Or, retrieve specific columns from the dataset.</span><span class="sxs-lookup"><span data-stu-id="dbd23-158">Or, retrieve specific columns from the dataset.</span></span>

       sqlTableDF.select("AddressLine1", "City").show(10)

## <a name="write-data-into-azure-sql-database"></a><span data-ttu-id="dbd23-159">Write data into Azure SQL database</span><span class="sxs-lookup"><span data-stu-id="dbd23-159">Write data into Azure SQL database</span></span>

<span data-ttu-id="dbd23-160">In this section, we use a sample CSV file available on the cluster to create a table in Azure SQL database and populate it with data.</span><span class="sxs-lookup"><span data-stu-id="dbd23-160">In this section, we use a sample CSV file available on the cluster to create a table in Azure SQL database and populate it with data.</span></span> <span data-ttu-id="dbd23-161">The sample CSV file (**HVAC.csv**) is available on all HDInsight clusters at `HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv`.</span><span class="sxs-lookup"><span data-stu-id="dbd23-161">The sample CSV file (**HVAC.csv**) is available on all HDInsight clusters at `HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv`.</span></span>

1. <span data-ttu-id="dbd23-162">In a new Jupyter notebook, in a code cell, paste the following snippet and replace the placeholder values with the values for your Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="dbd23-162">In a new Jupyter notebook, in a code cell, paste the following snippet and replace the placeholder values with the values for your Azure SQL database.</span></span>

       // Declare the values for your Azure SQL database

       val jdbcUsername = "<SQL DB ADMIN USER>"
       val jdbcPassword = "<SQL DB ADMIN PWD>"
       val jdbcHostname = "<SQL SERVER NAME HOSTING SDL DB>" //typically, this is in the form or servername.database.windows.net
       val jdbcPort = 1433
       val jdbcDatabase ="<AZURE SQL DB NAME>"

    <span data-ttu-id="dbd23-163">Press **SHIFT + ENTER** to run the code cell.</span><span class="sxs-lookup"><span data-stu-id="dbd23-163">Press **SHIFT + ENTER** to run the code cell.</span></span>  

1. <span data-ttu-id="dbd23-164">The following snippet builds a JDBC URL that you can pass to the Spark dataframe APIs creates an `Properties` object to hold the parameters.</span><span class="sxs-lookup"><span data-stu-id="dbd23-164">The following snippet builds a JDBC URL that you can pass to the Spark dataframe APIs creates an `Properties` object to hold the parameters.</span></span> <span data-ttu-id="dbd23-165">Paste the snippet in a code cell and press **SHIFT + ENTER** to run.</span><span class="sxs-lookup"><span data-stu-id="dbd23-165">Paste the snippet in a code cell and press **SHIFT + ENTER** to run.</span></span>

       import java.util.Properties

       val jdbc_url = s"jdbc:sqlserver://${jdbcHostname}:${jdbcPort};database=${jdbcDatabase};encrypt=true;trustServerCertificate=false;hostNameInCertificate=*.database.windows.net;loginTimeout=60;"
       val connectionProperties = new Properties()
       connectionProperties.put("user", s"${jdbcUsername}")
       connectionProperties.put("password", s"${jdbcPassword}")

1. <span data-ttu-id="dbd23-166">Use the following snippet to extract the schema of the data in HVAC.csv and use the schema to load the data from the CSV in a dataframe, `readDf`.</span><span class="sxs-lookup"><span data-stu-id="dbd23-166">Use the following snippet to extract the schema of the data in HVAC.csv and use the schema to load the data from the CSV in a dataframe, `readDf`.</span></span> <span data-ttu-id="dbd23-167">Paste the snippet in a code cell and press **SHIFT + ENTER** to run.</span><span class="sxs-lookup"><span data-stu-id="dbd23-167">Paste the snippet in a code cell and press **SHIFT + ENTER** to run.</span></span>

       val userSchema = spark.read.option("header", "true").csv("wasbs:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv").schema
       val readDf = spark.read.format("csv").schema(userSchema).load("wasbs:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

1. <span data-ttu-id="dbd23-168">Use the `readDf` dataframe to create a temporary table, `temphvactable`.</span><span class="sxs-lookup"><span data-stu-id="dbd23-168">Use the `readDf` dataframe to create a temporary table, `temphvactable`.</span></span> <span data-ttu-id="dbd23-169">Then use the temporary table to create a hive table, `hvactable_hive`.</span><span class="sxs-lookup"><span data-stu-id="dbd23-169">Then use the temporary table to create a hive table, `hvactable_hive`.</span></span>

       readDf.createOrReplaceTempView("temphvactable")
       spark.sql("create table hvactable_hive as select * from temphvactable")

1. <span data-ttu-id="dbd23-170">Finally, use the hive table to create a table in Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="dbd23-170">Finally, use the hive table to create a table in Azure SQL database.</span></span> <span data-ttu-id="dbd23-171">The following snippet creates `hvactable` in Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="dbd23-171">The following snippet creates `hvactable` in Azure SQL database.</span></span>

       spark.table("hvactable_hive").write.jdbc(jdbc_url, "hvactable", connectionProperties)

1. <span data-ttu-id="dbd23-172">Connect to the Azure SQL database using SSMS and verify that you see a `dbo.hvactable` there.</span><span class="sxs-lookup"><span data-stu-id="dbd23-172">Connect to the Azure SQL database using SSMS and verify that you see a `dbo.hvactable` there.</span></span>

    <span data-ttu-id="dbd23-173">a.</span><span class="sxs-lookup"><span data-stu-id="dbd23-173">a.</span></span> <span data-ttu-id="dbd23-174">Start SSMS and connect to the Azure SQL database by providing connection details as shown in the screenshot below.</span><span class="sxs-lookup"><span data-stu-id="dbd23-174">Start SSMS and connect to the Azure SQL database by providing connection details as shown in the screenshot below.</span></span>

    <span data-ttu-id="dbd23-175">![Connect to SQL database using SSMS](./media/apache-spark-connect-to-sql-database/connect-to-sql-db-ssms.png "Connect to SQL database using SSMS")</span><span class="sxs-lookup"><span data-stu-id="dbd23-175">![Connect to SQL database using SSMS](./media/apache-spark-connect-to-sql-database/connect-to-sql-db-ssms.png "Connect to SQL database using SSMS")</span></span>

    <span data-ttu-id="dbd23-176">b.</span><span class="sxs-lookup"><span data-stu-id="dbd23-176">b.</span></span> <span data-ttu-id="dbd23-177">From the Object Explorer, expand the Azure SQL database and the Table node to see the **dbo.hvactable** created.</span><span class="sxs-lookup"><span data-stu-id="dbd23-177">From the Object Explorer, expand the Azure SQL database and the Table node to see the **dbo.hvactable** created.</span></span>

    <span data-ttu-id="dbd23-178">![Connect to SQL database using SSMS](./media/apache-spark-connect-to-sql-database/connect-to-sql-db-ssms-locate-table.png "Connect to SQL database using SSMS")</span><span class="sxs-lookup"><span data-stu-id="dbd23-178">![Connect to SQL database using SSMS](./media/apache-spark-connect-to-sql-database/connect-to-sql-db-ssms-locate-table.png "Connect to SQL database using SSMS")</span></span>

1. <span data-ttu-id="dbd23-179">Run a query in SSMS to see the columns in the table.</span><span class="sxs-lookup"><span data-stu-id="dbd23-179">Run a query in SSMS to see the columns in the table.</span></span>

        SELECT * from hvactable

## <a name="stream-data-into-azure-sql-database"></a><span data-ttu-id="dbd23-180">Stream data into Azure SQL database</span><span class="sxs-lookup"><span data-stu-id="dbd23-180">Stream data into Azure SQL database</span></span>

<span data-ttu-id="dbd23-181">In this section, we stream data into the **hvactable** that you already created in Azure SQL database in the previous section.</span><span class="sxs-lookup"><span data-stu-id="dbd23-181">In this section, we stream data into the **hvactable** that you already created in Azure SQL database in the previous section.</span></span>

1. <span data-ttu-id="dbd23-182">As a first step, make sure there are no records in the **hvactable**.</span><span class="sxs-lookup"><span data-stu-id="dbd23-182">As a first step, make sure there are no records in the **hvactable**.</span></span> <span data-ttu-id="dbd23-183">Using SSMS, run the following query on the table.</span><span class="sxs-lookup"><span data-stu-id="dbd23-183">Using SSMS, run the following query on the table.</span></span>

       DELETE FROM [dbo].[hvactable]

1. <span data-ttu-id="dbd23-184">Create a new Jupyter notebook on the HDInsight Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="dbd23-184">Create a new Jupyter notebook on the HDInsight Spark cluster.</span></span> <span data-ttu-id="dbd23-185">In a code cell, paste the following snippet and then press **SHIFT + ENTER**:</span><span class="sxs-lookup"><span data-stu-id="dbd23-185">In a code cell, paste the following snippet and then press **SHIFT + ENTER**:</span></span>

       import org.apache.spark.sql._
       import org.apache.spark.sql.types._
       import org.apache.spark.sql.functions._
       import org.apache.spark.sql.streaming._
       import java.sql.{Connection,DriverManager,ResultSet}

1. <span data-ttu-id="dbd23-186">We stream data from the **HVAC.csv** into the hvactable.</span><span class="sxs-lookup"><span data-stu-id="dbd23-186">We stream data from the **HVAC.csv** into the hvactable.</span></span> <span data-ttu-id="dbd23-187">HVAC.csv file is available on the cluster at */HdiSamples/HdiSamples/SensorSampleData/HVAC/*.</span><span class="sxs-lookup"><span data-stu-id="dbd23-187">HVAC.csv file is available on the cluster at */HdiSamples/HdiSamples/SensorSampleData/HVAC/*.</span></span> <span data-ttu-id="dbd23-188">In the following snippet, we first get the schema of the data to be streamed.</span><span class="sxs-lookup"><span data-stu-id="dbd23-188">In the following snippet, we first get the schema of the data to be streamed.</span></span> <span data-ttu-id="dbd23-189">Then, we create a streaming dataframe using that schema.</span><span class="sxs-lookup"><span data-stu-id="dbd23-189">Then, we create a streaming dataframe using that schema.</span></span> <span data-ttu-id="dbd23-190">Paste the snippet in a code cell and press **SHIFT + ENTER** to run.</span><span class="sxs-lookup"><span data-stu-id="dbd23-190">Paste the snippet in a code cell and press **SHIFT + ENTER** to run.</span></span>

       val userSchema = spark.read.option("header", "true").csv("wasbs:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv").schema
       val readStreamDf = spark.readStream.schema(userSchema).csv("wasbs:///HdiSamples/HdiSamples/SensorSampleData/hvac/") 
       readStreamDf.printSchema

1. <span data-ttu-id="dbd23-191">The output shows the schema of **HVAC.csv**.</span><span class="sxs-lookup"><span data-stu-id="dbd23-191">The output shows the schema of **HVAC.csv**.</span></span> <span data-ttu-id="dbd23-192">The **hvactable** has the same schema as well.</span><span class="sxs-lookup"><span data-stu-id="dbd23-192">The **hvactable** has the same schema as well.</span></span> <span data-ttu-id="dbd23-193">The output lists the columns in the table.</span><span class="sxs-lookup"><span data-stu-id="dbd23-193">The output lists the columns in the table.</span></span>

    <span data-ttu-id="dbd23-194">![Schema of table](./media/apache-spark-connect-to-sql-database/schema-of-table.png "Schema of table")</span><span class="sxs-lookup"><span data-stu-id="dbd23-194">![Schema of table](./media/apache-spark-connect-to-sql-database/schema-of-table.png "Schema of table")</span></span>

1. <span data-ttu-id="dbd23-195">Finally, use the following snippet to read data from the HVAC.csv and stream it into the **hvactable** in Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="dbd23-195">Finally, use the following snippet to read data from the HVAC.csv and stream it into the **hvactable** in Azure SQL database.</span></span> <span data-ttu-id="dbd23-196">Paste the snippet in a code cell, replace the placeholder values with the values for your Azure SQL database, and then press **SHIFT + ENTER** to run.</span><span class="sxs-lookup"><span data-stu-id="dbd23-196">Paste the snippet in a code cell, replace the placeholder values with the values for your Azure SQL database, and then press **SHIFT + ENTER** to run.</span></span>

       val WriteToSQLQuery  = readStreamDf.writeStream.foreach(new ForeachWriter[Row] {
          var connection:java.sql.Connection = _
          var statement:java.sql.Statement = _
          
          val jdbcUsername = "<SQL DB ADMIN USER>"
          val jdbcPassword = "<SQL DB ADMIN PWD>"
          val jdbcHostname = "<SQL SERVER NAME HOSTING SDL DB>" //typically, this is in the form or servername.database.windows.net
          val jdbcPort = 1433
          val jdbcDatabase ="<AZURE SQL DB NAME>"
          val driver = "com.microsoft.sqlserver.jdbc.SQLServerDriver"
          val jdbc_url = s"jdbc:sqlserver://${jdbcHostname}:${jdbcPort};database=${jdbcDatabase};encrypt=true;trustServerCertificate=false;hostNameInCertificate=*.database.windows.net;loginTimeout=30;"
  
         def open(partitionId: Long, version: Long):Boolean = {
           Class.forName(driver)
           connection = DriverManager.getConnection(jdbc_url, jdbcUsername, jdbcPassword)
           statement = connection.createStatement
           true
         }
  
         def process(value: Row): Unit = {
           val Date  = value(0)
           val Time = value(1)
           val TargetTemp = value(2)
           val ActualTemp = value(3)
           val System = value(4)
           val SystemAge = value(5)
           val BuildingID = value(6)  
    
           val valueStr = "'" + Date + "'," + "'" + Time + "'," + "'" + TargetTemp + "'," + "'" + ActualTemp + "'," + "'" + System + "'," + "'" + SystemAge + "'," + "'" + BuildingID + "'"
           statement.execute("INSERT INTO " + "dbo.hvactable" + " VALUES (" + valueStr + ")")   
           }

         def close(errorOrNull: Throwable): Unit = {
            connection.close
          }
         })
        
         var streamingQuery = WriteToSQLQuery.start()

1. <span data-ttu-id="dbd23-197">Verify that the data is being streamed into the **hvactable** by running the following query in SQL Server Management Studio (SSMS).</span><span class="sxs-lookup"><span data-stu-id="dbd23-197">Verify that the data is being streamed into the **hvactable** by running the following query in SQL Server Management Studio (SSMS).</span></span> <span data-ttu-id="dbd23-198">Everytime you run the query, it shows the number of rows in the table increasing.</span><span class="sxs-lookup"><span data-stu-id="dbd23-198">Everytime you run the query, it shows the number of rows in the table increasing.</span></span>

        SELECT COUNT(*) FROM hvactable

## <a name="next-steps"></a><span data-ttu-id="dbd23-199">Next steps</span><span class="sxs-lookup"><span data-stu-id="dbd23-199">Next steps</span></span>

* [<span data-ttu-id="dbd23-200">Use HDInsight Spark cluster to analyze data in Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="dbd23-200">Use HDInsight Spark cluster to analyze data in Data Lake Store</span></span>](apache-spark-use-with-data-lake-store.md)
* [<span data-ttu-id="dbd23-201">Process structured streaming events using EventHub</span><span class="sxs-lookup"><span data-stu-id="dbd23-201">Process structured streaming events using EventHub</span></span>](apache-spark-eventhub-structured-streaming.md)
* [<span data-ttu-id="dbd23-202">Use Spark Structured Streaming with Kafka on HDInsight</span><span class="sxs-lookup"><span data-stu-id="dbd23-202">Use Spark Structured Streaming with Kafka on HDInsight</span></span>](../hdinsight-apache-kafka-spark-structured-streaming.md)
