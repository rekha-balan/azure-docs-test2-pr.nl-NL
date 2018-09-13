---
title: Use Apache Spark to analyze data in Azure Data Lake Store
description: Run Spark jobs to analyze data stored in Azure Data Lake Store
services: hdinsight
ms.service: hdinsight
author: jasonwhowell
ms.author: jasonh
ms.reviewer: jasonh
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 02/21/2018
ms.openlocfilehash: aae63b06999c0b8eafa0d42608d32a4d467a900c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864594"
---
# <a name="use-hdinsight-spark-cluster-to-analyze-data-in-data-lake-store"></a><span data-ttu-id="fbef6-103">Use HDInsight Spark cluster to analyze data in Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="fbef6-103">Use HDInsight Spark cluster to analyze data in Data Lake Store</span></span>

<span data-ttu-id="fbef6-104">In this tutorial, you use Jupyter notebook available with HDInsight Spark clusters to run a job that reads data from a Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="fbef6-104">In this tutorial, you use Jupyter notebook available with HDInsight Spark clusters to run a job that reads data from a Data Lake Store account.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fbef6-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="fbef6-105">Prerequisites</span></span>

* <span data-ttu-id="fbef6-106">Azure Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="fbef6-106">Azure Data Lake Store account.</span></span> <span data-ttu-id="fbef6-107">Follow the instructions at [Get started with Azure Data Lake Store using the Azure portal](../../data-lake-store/data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="fbef6-107">Follow the instructions at [Get started with Azure Data Lake Store using the Azure portal](../../data-lake-store/data-lake-store-get-started-portal.md).</span></span>

* <span data-ttu-id="fbef6-108">Azure HDInsight Spark cluster with Data Lake Store as storage.</span><span class="sxs-lookup"><span data-stu-id="fbef6-108">Azure HDInsight Spark cluster with Data Lake Store as storage.</span></span> <span data-ttu-id="fbef6-109">Follow the instructions at [Quickstart: Set up clusters in HDInsight](../../storage/data-lake-storage/quickstart-create-connect-hdi-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="fbef6-109">Follow the instructions at [Quickstart: Set up clusters in HDInsight](../../storage/data-lake-storage/quickstart-create-connect-hdi-cluster.md).</span></span>

    
## <a name="prepare-the-data"></a><span data-ttu-id="fbef6-110">Prepare the data</span><span class="sxs-lookup"><span data-stu-id="fbef6-110">Prepare the data</span></span>

> [!NOTE]
> <span data-ttu-id="fbef6-111">You do not need to perform this step if you have created the HDInsight cluster with Data Lake Store as default storage.</span><span class="sxs-lookup"><span data-stu-id="fbef6-111">You do not need to perform this step if you have created the HDInsight cluster with Data Lake Store as default storage.</span></span> <span data-ttu-id="fbef6-112">The cluster creation process adds some sample data in the Data Lake Store account that you specify while creating the cluster.</span><span class="sxs-lookup"><span data-stu-id="fbef6-112">The cluster creation process adds some sample data in the Data Lake Store account that you specify while creating the cluster.</span></span> <span data-ttu-id="fbef6-113">Skip to the section [Use HDInsight Spark cluster with Data Lake Store](#use-an-hdinsight-spark-cluster-with-data-lake-store).</span><span class="sxs-lookup"><span data-stu-id="fbef6-113">Skip to the section [Use HDInsight Spark cluster with Data Lake Store](#use-an-hdinsight-spark-cluster-with-data-lake-store).</span></span>
>
>

<span data-ttu-id="fbef6-114">If you created an HDInsight cluster with Data Lake Store as additional storage and Azure Storage Blob as default storage, you should first copy over some sample data to the Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="fbef6-114">If you created an HDInsight cluster with Data Lake Store as additional storage and Azure Storage Blob as default storage, you should first copy over some sample data to the Data Lake Store account.</span></span> <span data-ttu-id="fbef6-115">You can use the sample data from the Azure Storage Blob associated with the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="fbef6-115">You can use the sample data from the Azure Storage Blob associated with the HDInsight cluster.</span></span> <span data-ttu-id="fbef6-116">You can use the [ADLCopy tool](http://aka.ms/downloadadlcopy) to do so.</span><span class="sxs-lookup"><span data-stu-id="fbef6-116">You can use the [ADLCopy tool](http://aka.ms/downloadadlcopy) to do so.</span></span> <span data-ttu-id="fbef6-117">Download and install the tool from the link.</span><span class="sxs-lookup"><span data-stu-id="fbef6-117">Download and install the tool from the link.</span></span>

1. <span data-ttu-id="fbef6-118">Open a command prompt and navigate to the directory where AdlCopy is installed, typically `%HOMEPATH%\Documents\adlcopy`.</span><span class="sxs-lookup"><span data-stu-id="fbef6-118">Open a command prompt and navigate to the directory where AdlCopy is installed, typically `%HOMEPATH%\Documents\adlcopy`.</span></span>

2. <span data-ttu-id="fbef6-119">Run the following command to copy a specific blob from the source container to a Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="fbef6-119">Run the following command to copy a specific blob from the source container to a Data Lake Store:</span></span>

        AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/<blob name> /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container>

    <span data-ttu-id="fbef6-120">Copy the **HVAC.csv** sample data file at **/HdiSamples/HdiSamples/SensorSampleData/hvac/** to the Azure Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="fbef6-120">Copy the **HVAC.csv** sample data file at **/HdiSamples/HdiSamples/SensorSampleData/hvac/** to the Azure Data Lake Store account.</span></span> <span data-ttu-id="fbef6-121">The code snippet should look like:</span><span class="sxs-lookup"><span data-stu-id="fbef6-121">The code snippet should look like:</span></span>

        AdlCopy /Source https://mydatastore.blob.core.windows.net/mysparkcluster/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv /dest swebhdfs://mydatalakestore.azuredatalakestore.net/hvac/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ==

   > [!WARNING]
   > <span data-ttu-id="fbef6-122">Make sure you the file and path names are in the proper case.</span><span class="sxs-lookup"><span data-stu-id="fbef6-122">Make sure you the file and path names are in the proper case.</span></span>
   >
   >
3. <span data-ttu-id="fbef6-123">You are prompted to enter the credentials for the Azure subscription under which you have your Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="fbef6-123">You are prompted to enter the credentials for the Azure subscription under which you have your Data Lake Store account.</span></span> <span data-ttu-id="fbef6-124">You see an output similar to the following snippet:</span><span class="sxs-lookup"><span data-stu-id="fbef6-124">You see an output similar to the following snippet:</span></span>

        Initializing Copy.
        Copy Started.
        100% data copied.
        Copy Completed. 1 file copied.

    <span data-ttu-id="fbef6-125">The data file (**HVAC.csv**) will be copied under a folder **/hvac** in the Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="fbef6-125">The data file (**HVAC.csv**) will be copied under a folder **/hvac** in the Data Lake Store account.</span></span>

## <a name="use-an-hdinsight-spark-cluster-with-data-lake-store"></a><span data-ttu-id="fbef6-126">Use an HDInsight Spark cluster with Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="fbef6-126">Use an HDInsight Spark cluster with Data Lake Store</span></span>

1. <span data-ttu-id="fbef6-127">From the [Azure Portal](https://portal.azure.com/), from the startboard, click the tile for your Spark cluster (if you pinned it to the startboard).</span><span class="sxs-lookup"><span data-stu-id="fbef6-127">From the [Azure Portal](https://portal.azure.com/), from the startboard, click the tile for your Spark cluster (if you pinned it to the startboard).</span></span> <span data-ttu-id="fbef6-128">You can also navigate to your cluster under **Browse All** > **HDInsight Clusters**.</span><span class="sxs-lookup"><span data-stu-id="fbef6-128">You can also navigate to your cluster under **Browse All** > **HDInsight Clusters**.</span></span>

2. <span data-ttu-id="fbef6-129">From the Spark cluster blade, click **Quick Links**, and then from the **Cluster Dashboard** blade, click **Jupyter Notebook**.</span><span class="sxs-lookup"><span data-stu-id="fbef6-129">From the Spark cluster blade, click **Quick Links**, and then from the **Cluster Dashboard** blade, click **Jupyter Notebook**.</span></span> <span data-ttu-id="fbef6-130">If prompted, enter the admin credentials for the cluster.</span><span class="sxs-lookup"><span data-stu-id="fbef6-130">If prompted, enter the admin credentials for the cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="fbef6-131">You may also reach the Jupyter Notebook for your cluster by opening the following URL in your browser.</span><span class="sxs-lookup"><span data-stu-id="fbef6-131">You may also reach the Jupyter Notebook for your cluster by opening the following URL in your browser.</span></span> <span data-ttu-id="fbef6-132">Replace **CLUSTERNAME** with the name of your cluster:</span><span class="sxs-lookup"><span data-stu-id="fbef6-132">Replace **CLUSTERNAME** with the name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >

3. <span data-ttu-id="fbef6-133">Create a new notebook.</span><span class="sxs-lookup"><span data-stu-id="fbef6-133">Create a new notebook.</span></span> <span data-ttu-id="fbef6-134">Click **New**, and then click **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="fbef6-134">Click **New**, and then click **PySpark**.</span></span>

    <span data-ttu-id="fbef6-135">![Create a new Jupyter notebook](./media/apache-spark-use-with-data-lake-store/hdinsight-create-jupyter-notebook.png "Create a new Jupyter notebook")</span><span class="sxs-lookup"><span data-stu-id="fbef6-135">![Create a new Jupyter notebook](./media/apache-spark-use-with-data-lake-store/hdinsight-create-jupyter-notebook.png "Create a new Jupyter notebook")</span></span>

4. <span data-ttu-id="fbef6-136">Because you created a notebook using the PySpark kernel, you do not need to create any contexts explicitly.</span><span class="sxs-lookup"><span data-stu-id="fbef6-136">Because you created a notebook using the PySpark kernel, you do not need to create any contexts explicitly.</span></span> <span data-ttu-id="fbef6-137">The Spark and Hive contexts will be automatically created for you when you run the first code cell.</span><span class="sxs-lookup"><span data-stu-id="fbef6-137">The Spark and Hive contexts will be automatically created for you when you run the first code cell.</span></span> <span data-ttu-id="fbef6-138">You can start by importing the types required for this scenario.</span><span class="sxs-lookup"><span data-stu-id="fbef6-138">You can start by importing the types required for this scenario.</span></span> <span data-ttu-id="fbef6-139">To do so, paste the following code snippet in a cell and press **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="fbef6-139">To do so, paste the following code snippet in a cell and press **SHIFT + ENTER**.</span></span>

        from pyspark.sql.types import *

    <span data-ttu-id="fbef6-140">Every time you run a job in Jupyter, your web browser window title will show a **(Busy)** status along with the notebook title.</span><span class="sxs-lookup"><span data-stu-id="fbef6-140">Every time you run a job in Jupyter, your web browser window title will show a **(Busy)** status along with the notebook title.</span></span> <span data-ttu-id="fbef6-141">You will also see a solid circle next to the **PySpark** text in the top-right corner.</span><span class="sxs-lookup"><span data-stu-id="fbef6-141">You will also see a solid circle next to the **PySpark** text in the top-right corner.</span></span> <span data-ttu-id="fbef6-142">After the job is completed, this will change to a hollow circle.</span><span class="sxs-lookup"><span data-stu-id="fbef6-142">After the job is completed, this will change to a hollow circle.</span></span>

     <span data-ttu-id="fbef6-143">![Status of a Jupyter notebook job](./media/apache-spark-use-with-data-lake-store/hdinsight-jupyter-job-status.png "Status of a Jupyter notebook job")</span><span class="sxs-lookup"><span data-stu-id="fbef6-143">![Status of a Jupyter notebook job](./media/apache-spark-use-with-data-lake-store/hdinsight-jupyter-job-status.png "Status of a Jupyter notebook job")</span></span>

5. <span data-ttu-id="fbef6-144">Load sample data into a temporary table using the **HVAC.csv** file you copied to the Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="fbef6-144">Load sample data into a temporary table using the **HVAC.csv** file you copied to the Data Lake Store account.</span></span> <span data-ttu-id="fbef6-145">You can access the data in the Data Lake Store account using the following URL pattern.</span><span class="sxs-lookup"><span data-stu-id="fbef6-145">You can access the data in the Data Lake Store account using the following URL pattern.</span></span>

    * <span data-ttu-id="fbef6-146">If you have Data Lake Store as default storage, HVAC.csv will be at the path similar to the following URL:</span><span class="sxs-lookup"><span data-stu-id="fbef6-146">If you have Data Lake Store as default storage, HVAC.csv will be at the path similar to the following URL:</span></span>

            adl://<data_lake_store_name>.azuredatalakestore.net/<cluster_root>/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv

        <span data-ttu-id="fbef6-147">Or, you could also use a shortened format such as the following:</span><span class="sxs-lookup"><span data-stu-id="fbef6-147">Or, you could also use a shortened format such as the following:</span></span>

            adl:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv

    * <span data-ttu-id="fbef6-148">If you have Data Lake Store as additional storage, HVAC.csv will be at the location where you copied it, such as:</span><span class="sxs-lookup"><span data-stu-id="fbef6-148">If you have Data Lake Store as additional storage, HVAC.csv will be at the location where you copied it, such as:</span></span>

            adl://<data_lake_store_name>.azuredatalakestore.net/<path_to_file>

     <span data-ttu-id="fbef6-149">In an empty cell, paste the following code example, replace **MYDATALAKESTORE** with your Data Lake Store account name, and press **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="fbef6-149">In an empty cell, paste the following code example, replace **MYDATALAKESTORE** with your Data Lake Store account name, and press **SHIFT + ENTER**.</span></span> <span data-ttu-id="fbef6-150">This code example registers the data into a temporary table called **hvac**.</span><span class="sxs-lookup"><span data-stu-id="fbef6-150">This code example registers the data into a temporary table called **hvac**.</span></span>

            # Load the data. The path below assumes Data Lake Store is default storage for the Spark cluster
            hvacText = sc.textFile("adl://MYDATALAKESTORE.azuredatalakestore.net/cluster/mysparkcluster/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

            # Create the schema
            hvacSchema = StructType([StructField("date", StringType(), False),StructField("time", StringType(), False),StructField("targettemp", IntegerType(), False),StructField("actualtemp", IntegerType(), False),StructField("buildingID", StringType(), False)])

            # Parse the data in hvacText
            hvac = hvacText.map(lambda s: s.split(",")).filter(lambda s: s[0] != "Date").map(lambda s:(str(s[0]), str(s[1]), int(s[2]), int(s[3]), str(s[6]) ))

            # Create a data frame
            hvacdf = sqlContext.createDataFrame(hvac,hvacSchema)

            # Register the data fram as a table to run queries against
            hvacdf.registerTempTable("hvac")

6. <span data-ttu-id="fbef6-151">Because you are using a PySpark kernel, you can now directly run a SQL query on the temporary table **hvac** that you just created by using the `%%sql` magic.</span><span class="sxs-lookup"><span data-stu-id="fbef6-151">Because you are using a PySpark kernel, you can now directly run a SQL query on the temporary table **hvac** that you just created by using the `%%sql` magic.</span></span> <span data-ttu-id="fbef6-152">For more information about the `%%sql` magic, as well as other magics available with the PySpark kernel, see [Kernels available on Jupyter notebooks with Spark HDInsight clusters](apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span><span class="sxs-lookup"><span data-stu-id="fbef6-152">For more information about the `%%sql` magic, as well as other magics available with the PySpark kernel, see [Kernels available on Jupyter notebooks with Spark HDInsight clusters](apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>

        %%sql
        SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"

7. <span data-ttu-id="fbef6-153">Once the job is completed successfully, the following tabular output is displayed by default.</span><span class="sxs-lookup"><span data-stu-id="fbef6-153">Once the job is completed successfully, the following tabular output is displayed by default.</span></span>

      <span data-ttu-id="fbef6-154">![Table output of query result](./media/apache-spark-use-with-data-lake-store/jupyter-tabular-output.png "Table output of query result")</span><span class="sxs-lookup"><span data-stu-id="fbef6-154">![Table output of query result](./media/apache-spark-use-with-data-lake-store/jupyter-tabular-output.png "Table output of query result")</span></span>

     <span data-ttu-id="fbef6-155">You can also see the results in other visualizations as well.</span><span class="sxs-lookup"><span data-stu-id="fbef6-155">You can also see the results in other visualizations as well.</span></span> <span data-ttu-id="fbef6-156">For example, an area graph for the same output would look like the following.</span><span class="sxs-lookup"><span data-stu-id="fbef6-156">For example, an area graph for the same output would look like the following.</span></span>

     <span data-ttu-id="fbef6-157">![Area graph of query result](./media/apache-spark-use-with-data-lake-store/jupyter-area-output.png "Area graph of query result")</span><span class="sxs-lookup"><span data-stu-id="fbef6-157">![Area graph of query result](./media/apache-spark-use-with-data-lake-store/jupyter-area-output.png "Area graph of query result")</span></span>

8. <span data-ttu-id="fbef6-158">After you have finished running the application, you should shutdown the notebook to release the resources.</span><span class="sxs-lookup"><span data-stu-id="fbef6-158">After you have finished running the application, you should shutdown the notebook to release the resources.</span></span> <span data-ttu-id="fbef6-159">To do so, from the **File** menu on the notebook, click **Close and Halt**.</span><span class="sxs-lookup"><span data-stu-id="fbef6-159">To do so, from the **File** menu on the notebook, click **Close and Halt**.</span></span> <span data-ttu-id="fbef6-160">This will shutdown and close the notebook.</span><span class="sxs-lookup"><span data-stu-id="fbef6-160">This will shutdown and close the notebook.</span></span>


## <a name="next-steps"></a><span data-ttu-id="fbef6-161">Next steps</span><span class="sxs-lookup"><span data-stu-id="fbef6-161">Next steps</span></span>

* [<span data-ttu-id="fbef6-162">Create a standalone Scala application to run on Apache Spark cluster</span><span class="sxs-lookup"><span data-stu-id="fbef6-162">Create a standalone Scala application to run on Apache Spark cluster</span></span>](apache-spark-create-standalone-application.md)
* [<span data-ttu-id="fbef6-163">Use HDInsight Tools in Azure Toolkit for IntelliJ to create Spark applications for HDInsight Spark Linux cluster</span><span class="sxs-lookup"><span data-stu-id="fbef6-163">Use HDInsight Tools in Azure Toolkit for IntelliJ to create Spark applications for HDInsight Spark Linux cluster</span></span>](apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="fbef6-164">Use HDInsight Tools in Azure Toolkit for Eclipse to create Spark applications for HDInsight Spark Linux cluster</span><span class="sxs-lookup"><span data-stu-id="fbef6-164">Use HDInsight Tools in Azure Toolkit for Eclipse to create Spark applications for HDInsight Spark Linux cluster</span></span>](apache-spark-eclipse-tool-plugin.md)
