---
title: Use Apache Spark to analyze data in Azure Data Lake Store | Microsoft Docs
description: Run Spark jobs to analyze data stored in Azure Data Lake Store
services: hdinsight
documentationcenter: ''
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 1f174323-c17b-428c-903d-04f0e272784c
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/21/2017
ms.author: nitinme
ms.openlocfilehash: 6b727ab98b7f8699686b218a4bd5e8015e026ead
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563875"
---
# <a name="use-hdinsight-spark-cluster-to-analyze-data-in-data-lake-store"></a><span data-ttu-id="b032b-103">Use HDInsight Spark cluster to analyze data in Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="b032b-103">Use HDInsight Spark cluster to analyze data in Data Lake Store</span></span>

<span data-ttu-id="b032b-104">In this tutorial, you use Jupyter notebook available with HDInsight Spark clusters to run a job that reads data from a Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="b032b-104">In this tutorial, you use Jupyter notebook available with HDInsight Spark clusters to run a job that reads data from a Data Lake Store account.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b032b-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b032b-105">Prerequisites</span></span>

* <span data-ttu-id="b032b-106">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="b032b-106">An Azure subscription.</span></span> <span data-ttu-id="b032b-107">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b032b-107">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="b032b-108">Azure Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="b032b-108">Azure Data Lake Store account.</span></span> <span data-ttu-id="b032b-109">Follow the instructions at [Get started with Azure Data Lake Store using the Azure Portal](../data-lake-store/data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b032b-109">Follow the instructions at [Get started with Azure Data Lake Store using the Azure Portal](../data-lake-store/data-lake-store-get-started-portal.md).</span></span>

* <span data-ttu-id="b032b-110">Azure HDInsight Spark cluster with Data Lake Store as storage.</span><span class="sxs-lookup"><span data-stu-id="b032b-110">Azure HDInsight Spark cluster with Data Lake Store as storage.</span></span> <span data-ttu-id="b032b-111">Follow the instructions at [Create an HDInsight cluster with Data Lake Store using Azure Portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b032b-111">Follow the instructions at [Create an HDInsight cluster with Data Lake Store using Azure Portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

    
## <a name="prepare-the-data"></a><span data-ttu-id="b032b-112">Prepare the data</span><span class="sxs-lookup"><span data-stu-id="b032b-112">Prepare the data</span></span>

> [!NOTE]
> <span data-ttu-id="b032b-113">You do not need to perform this step if you have created the HDInsight cluster with Data Lake Store as default storage.</span><span class="sxs-lookup"><span data-stu-id="b032b-113">You do not need to perform this step if you have created the HDInsight cluster with Data Lake Store as default storage.</span></span> <span data-ttu-id="b032b-114">The cluster creation processes adds some sample data in the Data Lake Store account that you specify while creating the cluster.</span><span class="sxs-lookup"><span data-stu-id="b032b-114">The cluster creation processes adds some sample data in the Data Lake Store account that you specify while creating the cluster.</span></span> <span data-ttu-id="b032b-115">Skip to the section [Use HDInsight Spark cluster with Data Lake Store](#use-an-hdinsight-spark-cluster-with-data-lake-store).</span><span class="sxs-lookup"><span data-stu-id="b032b-115">Skip to the section [Use HDInsight Spark cluster with Data Lake Store](#use-an-hdinsight-spark-cluster-with-data-lake-store).</span></span>
>
>

<span data-ttu-id="b032b-116">If you created an HDInsight cluster with Data Lake Store as additional storage and Azure Storage Blob as default storage, you should first copy over some sample data to the Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="b032b-116">If you created an HDInsight cluster with Data Lake Store as additional storage and Azure Storage Blob as default storage, you should first copy over some sample data to the Data Lake Store account.</span></span> <span data-ttu-id="b032b-117">You can use the sample data from the Azure Storage Blob associated with the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="b032b-117">You can use the sample data from the Azure Storage Blob associated with the HDInsight cluster.</span></span> <span data-ttu-id="b032b-118">You can use the [ADLCopy tool](http://aka.ms/downloadadlcopy) to do so.</span><span class="sxs-lookup"><span data-stu-id="b032b-118">You can use the [ADLCopy tool](http://aka.ms/downloadadlcopy) to do so.</span></span> <span data-ttu-id="b032b-119">Download and install the tool from the link.</span><span class="sxs-lookup"><span data-stu-id="b032b-119">Download and install the tool from the link.</span></span>

1. <span data-ttu-id="b032b-120">Open a command prompt and navigate to the directory where AdlCopy is installed, typically `%HOMEPATH%\Documents\adlcopy`.</span><span class="sxs-lookup"><span data-stu-id="b032b-120">Open a command prompt and navigate to the directory where AdlCopy is installed, typically `%HOMEPATH%\Documents\adlcopy`.</span></span>

2. <span data-ttu-id="b032b-121">Run the following command to copy a specific blob from the source container to a Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="b032b-121">Run the following command to copy a specific blob from the source container to a Data Lake Store:</span></span>

        AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/<blob name> /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container>

    <span data-ttu-id="b032b-122">Copy the **HVAC.csv** sample data file at **/HdiSamples/HdiSamples/SensorSampleData/hvac/** to the Azure Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="b032b-122">Copy the **HVAC.csv** sample data file at **/HdiSamples/HdiSamples/SensorSampleData/hvac/** to the Azure Data Lake Store account.</span></span> <span data-ttu-id="b032b-123">The code snippet should look like:</span><span class="sxs-lookup"><span data-stu-id="b032b-123">The code snippet should look like:</span></span>

        AdlCopy /Source https://mydatastore.blob.core.windows.net/mysparkcluster/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv /dest swebhdfs://mydatalakestore.azuredatalakestore.net/hvac/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ==

   > [!WARNING]
   > <span data-ttu-id="b032b-124">Make sure you the file and path names are in the proper case.</span><span class="sxs-lookup"><span data-stu-id="b032b-124">Make sure you the file and path names are in the proper case.</span></span>
   >
   >
3. <span data-ttu-id="b032b-125">You will be prompted to enter the credentials for the Azure subscription under which you have your Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="b032b-125">You will be prompted to enter the credentials for the Azure subscription under which you have your Data Lake Store account.</span></span> <span data-ttu-id="b032b-126">You will see an output similar to the following:</span><span class="sxs-lookup"><span data-stu-id="b032b-126">You will see an output similar to the following:</span></span>

        Initializing Copy.
        Copy Started.
        100% data copied.
        Copy Completed. 1 file copied.

    <span data-ttu-id="b032b-127">The data file (**HVAC.csv**) will be copied under a folder **/hvac** in the Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="b032b-127">The data file (**HVAC.csv**) will be copied under a folder **/hvac** in the Data Lake Store account.</span></span>

## <a name="use-an-hdinsight-spark-cluster-with-data-lake-store"></a><span data-ttu-id="b032b-128">Use an HDInsight Spark cluster with Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="b032b-128">Use an HDInsight Spark cluster with Data Lake Store</span></span>

1. <span data-ttu-id="b032b-129">From the [Azure Portal](https://portal.azure.com/), from the startboard, click the tile for your Spark cluster (if you pinned it to the startboard).</span><span class="sxs-lookup"><span data-stu-id="b032b-129">From the [Azure Portal](https://portal.azure.com/), from the startboard, click the tile for your Spark cluster (if you pinned it to the startboard).</span></span> <span data-ttu-id="b032b-130">You can also navigate to your cluster under **Browse All** > **HDInsight Clusters**.</span><span class="sxs-lookup"><span data-stu-id="b032b-130">You can also navigate to your cluster under **Browse All** > **HDInsight Clusters**.</span></span>

2. <span data-ttu-id="b032b-131">From the Spark cluster blade, click **Quick Links**, and then from the **Cluster Dashboard** blade, click **Jupyter Notebook**.</span><span class="sxs-lookup"><span data-stu-id="b032b-131">From the Spark cluster blade, click **Quick Links**, and then from the **Cluster Dashboard** blade, click **Jupyter Notebook**.</span></span> <span data-ttu-id="b032b-132">If prompted, enter the admin credentials for the cluster.</span><span class="sxs-lookup"><span data-stu-id="b032b-132">If prompted, enter the admin credentials for the cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="b032b-133">You may also reach the Jupyter Notebook for your cluster by opening the following URL in your browser.</span><span class="sxs-lookup"><span data-stu-id="b032b-133">You may also reach the Jupyter Notebook for your cluster by opening the following URL in your browser.</span></span> <span data-ttu-id="b032b-134">Replace **CLUSTERNAME** with the name of your cluster:</span><span class="sxs-lookup"><span data-stu-id="b032b-134">Replace **CLUSTERNAME** with the name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >

3. <span data-ttu-id="b032b-135">Create a new notebook.</span><span class="sxs-lookup"><span data-stu-id="b032b-135">Create a new notebook.</span></span> <span data-ttu-id="b032b-136">Click **New**, and then click **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="b032b-136">Click **New**, and then click **PySpark**.</span></span>

    <span data-ttu-id="b032b-137">![Create a new Jupyter notebook](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-use-with-data-lake-store/hdispark.note.jupyter.createnotebook.png "Create a new Jupyter notebook")</span><span class="sxs-lookup"><span data-stu-id="b032b-137">![Create a new Jupyter notebook](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-use-with-data-lake-store/hdispark.note.jupyter.createnotebook.png "Create a new Jupyter notebook")</span></span>

4. <span data-ttu-id="b032b-138">Because you created a notebook using the PySpark kernel, you do not need to create any contexts explicitly.</span><span class="sxs-lookup"><span data-stu-id="b032b-138">Because you created a notebook using the PySpark kernel, you do not need to create any contexts explicitly.</span></span> <span data-ttu-id="b032b-139">The Spark and Hive contexts will be automatically created for you when you run the first code cell.</span><span class="sxs-lookup"><span data-stu-id="b032b-139">The Spark and Hive contexts will be automatically created for you when you run the first code cell.</span></span> <span data-ttu-id="b032b-140">You can start by importing the types required for this scenario.</span><span class="sxs-lookup"><span data-stu-id="b032b-140">You can start by importing the types required for this scenario.</span></span> <span data-ttu-id="b032b-141">To do so, paste the following code snippet in a cell and press **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="b032b-141">To do so, paste the following code snippet in a cell and press **SHIFT + ENTER**.</span></span>

        from pyspark.sql.types import *

    <span data-ttu-id="b032b-142">Every time you run a job in Jupyter, your web browser window title will show a **(Busy)** status along with the notebook title.</span><span class="sxs-lookup"><span data-stu-id="b032b-142">Every time you run a job in Jupyter, your web browser window title will show a **(Busy)** status along with the notebook title.</span></span> <span data-ttu-id="b032b-143">You will also see a solid circle next to the **PySpark** text in the top-right corner.</span><span class="sxs-lookup"><span data-stu-id="b032b-143">You will also see a solid circle next to the **PySpark** text in the top-right corner.</span></span> <span data-ttu-id="b032b-144">After the job is completed, this will change to a hollow circle.</span><span class="sxs-lookup"><span data-stu-id="b032b-144">After the job is completed, this will change to a hollow circle.</span></span>

     <span data-ttu-id="b032b-145">![Status of a Jupyter notebook job](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-use-with-data-lake-store/hdispark.jupyter.job.status.png "Status of a Jupyter notebook job")</span><span class="sxs-lookup"><span data-stu-id="b032b-145">![Status of a Jupyter notebook job](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-use-with-data-lake-store/hdispark.jupyter.job.status.png "Status of a Jupyter notebook job")</span></span>

5. <span data-ttu-id="b032b-146">Load sample data into a temporary table using the **HVAC.csv** file you copied to the Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="b032b-146">Load sample data into a temporary table using the **HVAC.csv** file you copied to the Data Lake Store account.</span></span> <span data-ttu-id="b032b-147">You can access the data in the Data Lake Store account using the following URL pattern.</span><span class="sxs-lookup"><span data-stu-id="b032b-147">You can access the data in the Data Lake Store account using the following URL pattern.</span></span>

    * <span data-ttu-id="b032b-148">If you have Data Lake Store as default storage, HVAC.csv will be at the path similar to the following URL:</span><span class="sxs-lookup"><span data-stu-id="b032b-148">If you have Data Lake Store as default storage, HVAC.csv will be at the path similar to the following URL:</span></span>

            adl://<data_lake_store_name>.azuredatalakestore.net/<cluster_root>/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv

        <span data-ttu-id="b032b-149">Or, you could also use a shortened format such as the following:</span><span class="sxs-lookup"><span data-stu-id="b032b-149">Or, you could also use a shortened format such as the following:</span></span>

            adl:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv

    * <span data-ttu-id="b032b-150">If you have Data Lake Store as additional storage, HVAC.csv will be at the location where you copied it, such as:</span><span class="sxs-lookup"><span data-stu-id="b032b-150">If you have Data Lake Store as additional storage, HVAC.csv will be at the location where you copied it, such as:</span></span>

            adl://<data_lake_store_name>.azuredatalakestore.net/<path_to_file>

     <span data-ttu-id="b032b-151">In an empty cell, paste the following code example, replace **MYDATALAKESTORE** with your Data Lake Store account name, and press **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="b032b-151">In an empty cell, paste the following code example, replace **MYDATALAKESTORE** with your Data Lake Store account name, and press **SHIFT + ENTER**.</span></span> <span data-ttu-id="b032b-152">This code example registers the data into a temporary table called **hvac**.</span><span class="sxs-lookup"><span data-stu-id="b032b-152">This code example registers the data into a temporary table called **hvac**.</span></span>

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

6. <span data-ttu-id="b032b-153">Because you are using a PySpark kernel, you can now directly run a SQL query on the temporary table **hvac** that you just created by using the `%%sql` magic.</span><span class="sxs-lookup"><span data-stu-id="b032b-153">Because you are using a PySpark kernel, you can now directly run a SQL query on the temporary table **hvac** that you just created by using the `%%sql` magic.</span></span> <span data-ttu-id="b032b-154">For more information about the `%%sql` magic, as well as other magics available with the PySpark kernel, see [Kernels available on Jupyter notebooks with Spark HDInsight clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span><span class="sxs-lookup"><span data-stu-id="b032b-154">For more information about the `%%sql` magic, as well as other magics available with the PySpark kernel, see [Kernels available on Jupyter notebooks with Spark HDInsight clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>

        %%sql
        SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"

7. <span data-ttu-id="b032b-155">Once the job is completed successfully, the following tabular output is displayed by default.</span><span class="sxs-lookup"><span data-stu-id="b032b-155">Once the job is completed successfully, the following tabular output is displayed by default.</span></span>

      <span data-ttu-id="b032b-156">![Table output of query result](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-use-with-data-lake-store/tabular.output.png "Table output of query result")</span><span class="sxs-lookup"><span data-stu-id="b032b-156">![Table output of query result](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-use-with-data-lake-store/tabular.output.png "Table output of query result")</span></span>

     <span data-ttu-id="b032b-157">You can also see the results in other visualizations as well.</span><span class="sxs-lookup"><span data-stu-id="b032b-157">You can also see the results in other visualizations as well.</span></span> <span data-ttu-id="b032b-158">For example, an area graph for the same output would look like the following.</span><span class="sxs-lookup"><span data-stu-id="b032b-158">For example, an area graph for the same output would look like the following.</span></span>

     <span data-ttu-id="b032b-159">![Area graph of query result](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-use-with-data-lake-store/area.output.png "Area graph of query result")</span><span class="sxs-lookup"><span data-stu-id="b032b-159">![Area graph of query result](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-use-with-data-lake-store/area.output.png "Area graph of query result")</span></span>

8. <span data-ttu-id="b032b-160">After you have finished running the application, you should shutdown the notebook to release the resources.</span><span class="sxs-lookup"><span data-stu-id="b032b-160">After you have finished running the application, you should shutdown the notebook to release the resources.</span></span> <span data-ttu-id="b032b-161">To do so, from the **File** menu on the notebook, click **Close and Halt**.</span><span class="sxs-lookup"><span data-stu-id="b032b-161">To do so, from the **File** menu on the notebook, click **Close and Halt**.</span></span> <span data-ttu-id="b032b-162">This will shutdown and close the notebook.</span><span class="sxs-lookup"><span data-stu-id="b032b-162">This will shutdown and close the notebook.</span></span>


## <a name="next-steps"></a><span data-ttu-id="b032b-163">Next steps</span><span class="sxs-lookup"><span data-stu-id="b032b-163">Next steps</span></span>

* [<span data-ttu-id="b032b-164">Create a standalone Scala application to run on Apache Spark cluster</span><span class="sxs-lookup"><span data-stu-id="b032b-164">Create a standalone Scala application to run on Apache Spark cluster</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="b032b-165">Use HDInsight Tools in Azure Toolkit for IntelliJ to create Spark applications for HDInsight Spark Linux cluster</span><span class="sxs-lookup"><span data-stu-id="b032b-165">Use HDInsight Tools in Azure Toolkit for IntelliJ to create Spark applications for HDInsight Spark Linux cluster</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="b032b-166">Use HDInsight Tools in Azure Toolkit for Eclipse to create Spark applications for HDInsight Spark Linux cluster</span><span class="sxs-lookup"><span data-stu-id="b032b-166">Use HDInsight Tools in Azure Toolkit for Eclipse to create Spark applications for HDInsight Spark Linux cluster</span></span>](hdinsight-apache-spark-eclipse-tool-plugin.md)




