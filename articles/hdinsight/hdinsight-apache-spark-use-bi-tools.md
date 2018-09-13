---
title: Use BI tools with Apache Spark on Azure HDInsight | Microsoft Docs
description: Step-by-step instructions on how to use notebooks with Apache Spark to create schemas on raw data, save them as tables, and then use BI tools on the table for data analytics
services: hdinsight
documentationcenter: ''
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 1448b536-9bc8-46bc-bbc6-d7001623642a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/13/2017
ms.author: nitinme
ms.openlocfilehash: 371bb90ee246294a65ee316300eac29c59275239
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551662"
---
# <a name="use-bi-tools-with-apache-spark-cluster-on-azure-hdinsight"></a><span data-ttu-id="e0f5c-103">Use BI tools with Apache Spark cluster on Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="e0f5c-103">Use BI tools with Apache Spark cluster on Azure HDInsight</span></span>

<span data-ttu-id="e0f5c-104">Learn how to use Apache Spark in Azure HDInsight to analyze a raw sample data set and then use BI tools to visualize the data.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-104">Learn how to use Apache Spark in Azure HDInsight to analyze a raw sample data set and then use BI tools to visualize the data.</span></span> <span data-ttu-id="e0f5c-105">This article demonstrates how to use BI tools such as Power BI and Tableau with HDInsight Spark clusters.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-105">This article demonstrates how to use BI tools such as Power BI and Tableau with HDInsight Spark clusters.</span></span>

> [!NOTE]
> <span data-ttu-id="e0f5c-106">Connectivity with BI tools described in this article is not supported on Spark 2.1 on Azure HDInsight 3.6 Preview.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-106">Connectivity with BI tools described in this article is not supported on Spark 2.1 on Azure HDInsight 3.6 Preview.</span></span> <span data-ttu-id="e0f5c-107">Only Spark versions 1.6 and 2.0 (HDInsight 3.4, 3.5 respectively) are supported.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-107">Only Spark versions 1.6 and 2.0 (HDInsight 3.4, 3.5 respectively) are supported.</span></span>
>

<span data-ttu-id="e0f5c-108">This tutorial is also available as a Jupyter notebook on a Spark (Linux) cluster that you create in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-108">This tutorial is also available as a Jupyter notebook on a Spark (Linux) cluster that you create in HDInsight.</span></span> <span data-ttu-id="e0f5c-109">The notebook experience lets you run the Python snippets from the notebook itself.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-109">The notebook experience lets you run the Python snippets from the notebook itself.</span></span> <span data-ttu-id="e0f5c-110">To perform the tutorial from within a notebook, create a Spark cluster, launch a Jupyter notebook (`https://CLUSTERNAME.azurehdinsight.net/jupyter`), and then run the notebook **Use BI tools with Apache Spark on HDInsight.ipynb** under the **Python** folder.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-110">To perform the tutorial from within a notebook, create a Spark cluster, launch a Jupyter notebook (`https://CLUSTERNAME.azurehdinsight.net/jupyter`), and then run the notebook **Use BI tools with Apache Spark on HDInsight.ipynb** under the **Python** folder.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e0f5c-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e0f5c-111">Prerequisites</span></span>

* <span data-ttu-id="e0f5c-112">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-112">An Azure subscription.</span></span> <span data-ttu-id="e0f5c-113">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="e0f5c-113">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="e0f5c-114">An Apache Spark cluster on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-114">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="e0f5c-115">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="e0f5c-115">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>


## <a name="hivetable"></a><span data-ttu-id="e0f5c-116">Save raw data as a table</span><span class="sxs-lookup"><span data-stu-id="e0f5c-116">Save raw data as a table</span></span>

<span data-ttu-id="e0f5c-117">In this section, we use the [Jupyter](https://jupyter.org) notebook from an HDInsight Spark cluster to run jobs that process your raw sample data and save it as a table.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-117">In this section, we use the [Jupyter](https://jupyter.org) notebook from an HDInsight Spark cluster to run jobs that process your raw sample data and save it as a table.</span></span> <span data-ttu-id="e0f5c-118">The sample data is a .csv file (hvac.csv) available on all clusters by default.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-118">The sample data is a .csv file (hvac.csv) available on all clusters by default.</span></span>

<span data-ttu-id="e0f5c-119">Once your data is saved as a table, in the next section we use BI tools to connect to the table and do further visualizations.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-119">Once your data is saved as a table, in the next section we use BI tools to connect to the table and do further visualizations.</span></span>

1. <span data-ttu-id="e0f5c-120">From the [Azure portal](https://portal.azure.com/), from the startboard, click the tile for your Spark cluster (if you pinned it to the startboard).</span><span class="sxs-lookup"><span data-stu-id="e0f5c-120">From the [Azure portal](https://portal.azure.com/), from the startboard, click the tile for your Spark cluster (if you pinned it to the startboard).</span></span> <span data-ttu-id="e0f5c-121">You can also navigate to your cluster under **Browse All** > **HDInsight Clusters**.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-121">You can also navigate to your cluster under **Browse All** > **HDInsight Clusters**.</span></span>   
2. <span data-ttu-id="e0f5c-122">From the Spark cluster blade, click **Cluster Dashboard**, and then click **Jupyter Notebook**.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-122">From the Spark cluster blade, click **Cluster Dashboard**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="e0f5c-123">If prompted, enter the admin credentials for the cluster.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-123">If prompted, enter the admin credentials for the cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="e0f5c-124">You may also reach the Jupyter Notebook for your cluster by opening the following URL in your browser.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-124">You may also reach the Jupyter Notebook for your cluster by opening the following URL in your browser.</span></span> <span data-ttu-id="e0f5c-125">Replace **CLUSTERNAME** with the name of your cluster:</span><span class="sxs-lookup"><span data-stu-id="e0f5c-125">Replace **CLUSTERNAME** with the name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >

3. <span data-ttu-id="e0f5c-126">Create a notebook.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-126">Create a notebook.</span></span> <span data-ttu-id="e0f5c-127">Click **New**, and then click **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-127">Click **New**, and then click **PySpark**.</span></span>

    <span data-ttu-id="e0f5c-128">![Create a Jupyter notebook](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-use-bi-tools/hdispark.note.jupyter.createnotebook.png "Create a Jupyter notebook")</span><span class="sxs-lookup"><span data-stu-id="e0f5c-128">![Create a Jupyter notebook](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-use-bi-tools/hdispark.note.jupyter.createnotebook.png "Create a Jupyter notebook")</span></span>

4. <span data-ttu-id="e0f5c-129">A new notebook is created and opened with the name Untitled.pynb.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-129">A new notebook is created and opened with the name Untitled.pynb.</span></span> <span data-ttu-id="e0f5c-130">Click the notebook name at the top, and enter a friendly name.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-130">Click the notebook name at the top, and enter a friendly name.</span></span>

    <span data-ttu-id="e0f5c-131">![Provide a name for the notebook](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-use-bi-tools/hdispark.note.jupyter.notebook.name.png "Provide a name for the notebook")</span><span class="sxs-lookup"><span data-stu-id="e0f5c-131">![Provide a name for the notebook](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-use-bi-tools/hdispark.note.jupyter.notebook.name.png "Provide a name for the notebook")</span></span>

5. <span data-ttu-id="e0f5c-132">Because you created a notebook using the PySpark kernel, you do not need to create any contexts explicitly.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-132">Because you created a notebook using the PySpark kernel, you do not need to create any contexts explicitly.</span></span> <span data-ttu-id="e0f5c-133">The Spark and Hive contexts are automatically created for you when you run the first code cell.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-133">The Spark and Hive contexts are automatically created for you when you run the first code cell.</span></span> <span data-ttu-id="e0f5c-134">You can start by importing the types required for this scenario.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-134">You can start by importing the types required for this scenario.</span></span> <span data-ttu-id="e0f5c-135">To do so, place the cursor in the cell and press **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-135">To do so, place the cursor in the cell and press **SHIFT + ENTER**.</span></span>

        from pyspark.sql import *

6. <span data-ttu-id="e0f5c-136">Load sample data into a temporary table.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-136">Load sample data into a temporary table.</span></span> <span data-ttu-id="e0f5c-137">When you create a Spark cluster in HDInsight, the sample data file, **hvac.csv**, is copied to the associated storage account under **\HdiSamples\HdiSamples\SensorSampleData\hvac**.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-137">When you create a Spark cluster in HDInsight, the sample data file, **hvac.csv**, is copied to the associated storage account under **\HdiSamples\HdiSamples\SensorSampleData\hvac**.</span></span>

    <span data-ttu-id="e0f5c-138">In an empty cell, paste the following snippet and press **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-138">In an empty cell, paste the following snippet and press **SHIFT + ENTER**.</span></span> <span data-ttu-id="e0f5c-139">This snippet registers the data into a table called **hvac**.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-139">This snippet registers the data into a table called **hvac**.</span></span>

        # Create an RDD from sample data
        hvacText = sc.textFile("wasbs:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

        # Create a schema for our data
        Entry = Row('Date', 'Time', 'TargetTemp', 'ActualTemp', 'BuildingID')

        # Parse the data and create a schema
        hvacParts = hvacText.map(lambda s: s.split(',')).filter(lambda s: s[0] != 'Date')
        hvac = hvacParts.map(lambda p: Entry(str(p[0]), str(p[1]), int(p[2]), int(p[3]), int(p[6])))

        # Infer the schema and create a table       
        hvacTable = sqlContext.createDataFrame(hvac)
        hvacTable.registerTempTable('hvactemptable')
        dfw = DataFrameWriter(hvacTable)
        dfw.saveAsTable('hvac')

7. <span data-ttu-id="e0f5c-140">Verify that the table was successfully created.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-140">Verify that the table was successfully created.</span></span> <span data-ttu-id="e0f5c-141">You can use the `%%sql` magic to run Hive queries directly.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-141">You can use the `%%sql` magic to run Hive queries directly.</span></span> <span data-ttu-id="e0f5c-142">For more information about the `%%sql` magic, and other magics available with the PySpark kernel, see [Kernels available on Jupyter notebooks with Spark HDInsight clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span><span class="sxs-lookup"><span data-stu-id="e0f5c-142">For more information about the `%%sql` magic, and other magics available with the PySpark kernel, see [Kernels available on Jupyter notebooks with Spark HDInsight clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>

        %%sql
        SHOW TABLES

    <span data-ttu-id="e0f5c-143">You see an output like shown below:</span><span class="sxs-lookup"><span data-stu-id="e0f5c-143">You see an output like shown below:</span></span>

        +---------------+-------------+
        |tableName      |isTemporary  |
        +---------------+-------------+
        |hvactemptable  |true        |
        |hivesampletable|false        |
        |hvac           |false        |
        +---------------+-------------+

    <span data-ttu-id="e0f5c-144">Only the tables that have false under the **isTemporary** column are hive tables that are stored in the metastore and can be accessed from the BI tools.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-144">Only the tables that have false under the **isTemporary** column are hive tables that are stored in the metastore and can be accessed from the BI tools.</span></span> <span data-ttu-id="e0f5c-145">In this tutorial, we connect to the **hvac** table we created.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-145">In this tutorial, we connect to the **hvac** table we created.</span></span>

8. <span data-ttu-id="e0f5c-146">Verify that the table contains the intended data.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-146">Verify that the table contains the intended data.</span></span> <span data-ttu-id="e0f5c-147">In an empty cell in the notebook, copy the following snippet and press **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-147">In an empty cell in the notebook, copy the following snippet and press **SHIFT + ENTER**.</span></span>

        %%sql
        SELECT * FROM hvac LIMIT 10

9. <span data-ttu-id="e0f5c-148">Shut down the notebook to release the resources.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-148">Shut down the notebook to release the resources.</span></span> <span data-ttu-id="e0f5c-149">To do so, from the **File** menu on the notebook, click **Close and Halt**.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-149">To do so, from the **File** menu on the notebook, click **Close and Halt**.</span></span>

## <a name="powerbi"></a><span data-ttu-id="e0f5c-150">Use Power BI</span><span class="sxs-lookup"><span data-stu-id="e0f5c-150">Use Power BI</span></span>

<span data-ttu-id="e0f5c-151">Once you have saved the data as a table, you can use Power BI to connect to the data and visualize it to create reports, dashboards, etc.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-151">Once you have saved the data as a table, you can use Power BI to connect to the data and visualize it to create reports, dashboards, etc.</span></span>

1. <span data-ttu-id="e0f5c-152">Make sure you have access to Power BI.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-152">Make sure you have access to Power BI.</span></span> <span data-ttu-id="e0f5c-153">You can get a free preview subscription of Power BI from [http://www.powerbi.com/](http://www.powerbi.com/).</span><span class="sxs-lookup"><span data-stu-id="e0f5c-153">You can get a free preview subscription of Power BI from [http://www.powerbi.com/](http://www.powerbi.com/).</span></span>

2. <span data-ttu-id="e0f5c-154">Sign in to [Power BI](http://www.powerbi.com/).</span><span class="sxs-lookup"><span data-stu-id="e0f5c-154">Sign in to [Power BI](http://www.powerbi.com/).</span></span>

3. <span data-ttu-id="e0f5c-155">From the bottom of the left pane, click **Get Data**.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-155">From the bottom of the left pane, click **Get Data**.</span></span>

4. <span data-ttu-id="e0f5c-156">On the **Get Data** page, under **Import or Connect to Data**, for **Databases**, click **Get**.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-156">On the **Get Data** page, under **Import or Connect to Data**, for **Databases**, click **Get**.</span></span>

    <span data-ttu-id="e0f5c-157">![Get data into Power BI](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-use-bi-tools/hdispark.powerbi.get.data.png "Get data into Power BI")</span><span class="sxs-lookup"><span data-stu-id="e0f5c-157">![Get data into Power BI](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-use-bi-tools/hdispark.powerbi.get.data.png "Get data into Power BI")</span></span>

5. <span data-ttu-id="e0f5c-158">On the next screen, click **Spark on Azure HDInsight** and then click **Connect**.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-158">On the next screen, click **Spark on Azure HDInsight** and then click **Connect**.</span></span> <span data-ttu-id="e0f5c-159">When prompted, enter the cluster URL (`mysparkcluster.azurehdinsight.net`) and the credentials to connect to the cluster.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-159">When prompted, enter the cluster URL (`mysparkcluster.azurehdinsight.net`) and the credentials to connect to the cluster.</span></span>

    <span data-ttu-id="e0f5c-160">![Connect to Spark](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-use-bi-tools/power-bi-connect-to-spark.png "Get data into Power BI")</span><span class="sxs-lookup"><span data-stu-id="e0f5c-160">![Connect to Spark](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-use-bi-tools/power-bi-connect-to-spark.png "Get data into Power BI")</span></span>

    <span data-ttu-id="e0f5c-161">After the connection is established, Power BI starts importing data from the Spark cluster on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-161">After the connection is established, Power BI starts importing data from the Spark cluster on HDInsight.</span></span>

6. <span data-ttu-id="e0f5c-162">Power BI imports the data and adds a **Spark** dataset under the **Datasets** heading.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-162">Power BI imports the data and adds a **Spark** dataset under the **Datasets** heading.</span></span> <span data-ttu-id="e0f5c-163">Click the data set to open a new worksheet to visualize the data.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-163">Click the data set to open a new worksheet to visualize the data.</span></span> <span data-ttu-id="e0f5c-164">You can also save the worksheet as a report.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-164">You can also save the worksheet as a report.</span></span> <span data-ttu-id="e0f5c-165">To save a worksheet, from the **File** menu, click **Save**.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-165">To save a worksheet, from the **File** menu, click **Save**.</span></span>

    <span data-ttu-id="e0f5c-166">![Spark tile on Power BI dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-use-bi-tools/hdispark.powerbi.tile.png "Spark tile on Power BI dashboard")</span><span class="sxs-lookup"><span data-stu-id="e0f5c-166">![Spark tile on Power BI dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-use-bi-tools/hdispark.powerbi.tile.png "Spark tile on Power BI dashboard")</span></span>
7. <span data-ttu-id="e0f5c-167">Notice that the **Fields** list on the right lists the **hvac** table you created earlier.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-167">Notice that the **Fields** list on the right lists the **hvac** table you created earlier.</span></span> <span data-ttu-id="e0f5c-168">Expand the table to see the fields in the table, as you defined in notebook earlier.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-168">Expand the table to see the fields in the table, as you defined in notebook earlier.</span></span>

      <span data-ttu-id="e0f5c-169">![List Hive tables](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-use-bi-tools/hdispark.powerbi.display.tables.png "List Hive tables")</span><span class="sxs-lookup"><span data-stu-id="e0f5c-169">![List Hive tables](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-use-bi-tools/hdispark.powerbi.display.tables.png "List Hive tables")</span></span>

8. <span data-ttu-id="e0f5c-170">Build a visualization to show the variance between target temperature and actual temperature for each building.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-170">Build a visualization to show the variance between target temperature and actual temperature for each building.</span></span> <span data-ttu-id="e0f5c-171">To visualize yoru data, select **Area Chart** (shown in red box).</span><span class="sxs-lookup"><span data-stu-id="e0f5c-171">To visualize yoru data, select **Area Chart** (shown in red box).</span></span> <span data-ttu-id="e0f5c-172">To define the axis, drag-and-drop the **BuildingID** field under **Axis**, and **ActualTemp**/**TargetTemp** fields under **Value**.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-172">To define the axis, drag-and-drop the **BuildingID** field under **Axis**, and **ActualTemp**/**TargetTemp** fields under **Value**.</span></span>

    <span data-ttu-id="e0f5c-173">![Create visualizations](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-use-bi-tools/hdispark.powerbi.visual1.png "Create visualizations")</span><span class="sxs-lookup"><span data-stu-id="e0f5c-173">![Create visualizations](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-use-bi-tools/hdispark.powerbi.visual1.png "Create visualizations")</span></span>

9. <span data-ttu-id="e0f5c-174">By default the visualization shows the sum for **ActualTemp** and **TargetTemp**.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-174">By default the visualization shows the sum for **ActualTemp** and **TargetTemp**.</span></span> <span data-ttu-id="e0f5c-175">For both the fields, from the drop-down, select **Average** to get an average of actual and target temperatures for both buildings.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-175">For both the fields, from the drop-down, select **Average** to get an average of actual and target temperatures for both buildings.</span></span>

    ![Create visualizations](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-use-bi-tools/hdispark.powerbi.visual2.png)

10. <span data-ttu-id="e0f5c-177">Your data visualization should be similar to the one in the screenshot.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-177">Your data visualization should be similar to the one in the screenshot.</span></span> <span data-ttu-id="e0f5c-178">Move your cursor over the visualization to get tool tips with relevant data.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-178">Move your cursor over the visualization to get tool tips with relevant data.</span></span>

    ![Create visualizations](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-use-bi-tools/hdispark.powerbi.visual3.png)

11. <span data-ttu-id="e0f5c-180">Click **Save** from the top menu and provide a report name.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-180">Click **Save** from the top menu and provide a report name.</span></span> <span data-ttu-id="e0f5c-181">You can also pin the visual.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-181">You can also pin the visual.</span></span> <span data-ttu-id="e0f5c-182">When you pin a visualization, it is stored on your dashboard so you can track the latest value at a glance.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-182">When you pin a visualization, it is stored on your dashboard so you can track the latest value at a glance.</span></span>

   <span data-ttu-id="e0f5c-183">You can add as many visualizations as you want for the same dataset and pin them to the dashboard for a snapshot of your data.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-183">You can add as many visualizations as you want for the same dataset and pin them to the dashboard for a snapshot of your data.</span></span> <span data-ttu-id="e0f5c-184">Also, Spark clusters on HDInsight are connected to Power BI with direct connect.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-184">Also, Spark clusters on HDInsight are connected to Power BI with direct connect.</span></span> <span data-ttu-id="e0f5c-185">This ensures that Power BI always has the most up-to-date data from your cluster so you do not need to schedule refreshes for the dataset.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-185">This ensures that Power BI always has the most up-to-date data from your cluster so you do not need to schedule refreshes for the dataset.</span></span>

## <a name="tableau"></a><span data-ttu-id="e0f5c-186">Use Tableau Desktop to analyze data in the table</span><span class="sxs-lookup"><span data-stu-id="e0f5c-186">Use Tableau Desktop to analyze data in the table</span></span>

> [!NOTE]
> <span data-ttu-id="e0f5c-187">This section is applicable only for Spark 1.5.2 clusters created in Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-187">This section is applicable only for Spark 1.5.2 clusters created in Azure HDInsight.</span></span>
>
>

1. <span data-ttu-id="e0f5c-188">Install [Tableau Desktop](http://www.tableau.com/products/desktop) on the computer where you are running this tutorial.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-188">Install [Tableau Desktop](http://www.tableau.com/products/desktop) on the computer where you are running this tutorial.</span></span>

2. <span data-ttu-id="e0f5c-189">Make sure that computer also has Microsoft Spark ODBC driver installed.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-189">Make sure that computer also has Microsoft Spark ODBC driver installed.</span></span> <span data-ttu-id="e0f5c-190">You can install the driver from [here](http://go.microsoft.com/fwlink/?LinkId=616229).</span><span class="sxs-lookup"><span data-stu-id="e0f5c-190">You can install the driver from [here](http://go.microsoft.com/fwlink/?LinkId=616229).</span></span>

1. <span data-ttu-id="e0f5c-191">Launch Tableau Desktop.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-191">Launch Tableau Desktop.</span></span> <span data-ttu-id="e0f5c-192">In the left pane, from the list of server to connect to, click **Spark SQL**.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-192">In the left pane, from the list of server to connect to, click **Spark SQL**.</span></span> <span data-ttu-id="e0f5c-193">If Spark SQL is not listed by default in the left pane, you can find it by click **More Servers**.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-193">If Spark SQL is not listed by default in the left pane, you can find it by click **More Servers**.</span></span>
2. <span data-ttu-id="e0f5c-194">In the Spark SQL connection dialog box, provide the values as shown in the screenshot, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-194">In the Spark SQL connection dialog box, provide the values as shown in the screenshot, and then click **OK**.</span></span>

    <span data-ttu-id="e0f5c-195">![Connect to a Spark cluster](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-use-bi-tools/hdispark.tableau.connect.png "Connect to a Spark cluster")</span><span class="sxs-lookup"><span data-stu-id="e0f5c-195">![Connect to a Spark cluster](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-use-bi-tools/hdispark.tableau.connect.png "Connect to a Spark cluster")</span></span>

    <span data-ttu-id="e0f5c-196">The authentication drop-down lists **Microsoft Azure HDInsight Service** as an option, only if you installed the [Microsoft Spark ODBC Driver](http://go.microsoft.com/fwlink/?LinkId=616229) on the computer.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-196">The authentication drop-down lists **Microsoft Azure HDInsight Service** as an option, only if you installed the [Microsoft Spark ODBC Driver](http://go.microsoft.com/fwlink/?LinkId=616229) on the computer.</span></span>
3. <span data-ttu-id="e0f5c-197">On the next screen, from the **Schema** drop-down, click the **Find** icon, and then click **default**.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-197">On the next screen, from the **Schema** drop-down, click the **Find** icon, and then click **default**.</span></span>

    <span data-ttu-id="e0f5c-198">![Find schema](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-use-bi-tools/hdispark.tableau.find.schema.png "Find schema")</span><span class="sxs-lookup"><span data-stu-id="e0f5c-198">![Find schema](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-use-bi-tools/hdispark.tableau.find.schema.png "Find schema")</span></span>
4. <span data-ttu-id="e0f5c-199">For the **Table** field, click the **Find** icon again to list all the Hive tables available in the cluster.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-199">For the **Table** field, click the **Find** icon again to list all the Hive tables available in the cluster.</span></span> <span data-ttu-id="e0f5c-200">You should see the **hvac** table you created earlier using the notebook.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-200">You should see the **hvac** table you created earlier using the notebook.</span></span>

    <span data-ttu-id="e0f5c-201">![Find tables](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-use-bi-tools/hdispark.tableau.find.table.png "Find tables")</span><span class="sxs-lookup"><span data-stu-id="e0f5c-201">![Find tables](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-use-bi-tools/hdispark.tableau.find.table.png "Find tables")</span></span>
5. <span data-ttu-id="e0f5c-202">Drag and drop the table to the top box on the right.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-202">Drag and drop the table to the top box on the right.</span></span> <span data-ttu-id="e0f5c-203">Tableau imports the data and displays the schema as highlighted by the red box.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-203">Tableau imports the data and displays the schema as highlighted by the red box.</span></span>

    <span data-ttu-id="e0f5c-204">![Add tables to Tableau](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-use-bi-tools/hdispark.tableau.drag.table.png "Add tables to Tableau")</span><span class="sxs-lookup"><span data-stu-id="e0f5c-204">![Add tables to Tableau](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-use-bi-tools/hdispark.tableau.drag.table.png "Add tables to Tableau")</span></span>
6. <span data-ttu-id="e0f5c-205">Click the **Sheet1** tab at the bottom left.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-205">Click the **Sheet1** tab at the bottom left.</span></span> <span data-ttu-id="e0f5c-206">Make a visualization that shows the average target and actual temperatures for all buildings for each date.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-206">Make a visualization that shows the average target and actual temperatures for all buildings for each date.</span></span> <span data-ttu-id="e0f5c-207">Drag **Date** and **Building ID** to **Columns** and **Actual Temp**/**Target Temp** to **Rows**.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-207">Drag **Date** and **Building ID** to **Columns** and **Actual Temp**/**Target Temp** to **Rows**.</span></span> <span data-ttu-id="e0f5c-208">Under **Marks**, select **Area** to use an area map visualization.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-208">Under **Marks**, select **Area** to use an area map visualization.</span></span>

     <span data-ttu-id="e0f5c-209">![Add fields for visualization](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-use-bi-tools/hdispark.tableau.drag.fields.png "Add fields for visualization")</span><span class="sxs-lookup"><span data-stu-id="e0f5c-209">![Add fields for visualization](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-use-bi-tools/hdispark.tableau.drag.fields.png "Add fields for visualization")</span></span>
7. <span data-ttu-id="e0f5c-210">By default, the temperature fields are shown as aggregate.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-210">By default, the temperature fields are shown as aggregate.</span></span> <span data-ttu-id="e0f5c-211">If you want to show the average temperatures instead, you can do so from the drop-down, as shown below.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-211">If you want to show the average temperatures instead, you can do so from the drop-down, as shown below.</span></span>

    <span data-ttu-id="e0f5c-212">![Take average of temperature](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-use-bi-tools/hdispark.tableau.temp.avg.png "Take average of temperature")</span><span class="sxs-lookup"><span data-stu-id="e0f5c-212">![Take average of temperature](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-use-bi-tools/hdispark.tableau.temp.avg.png "Take average of temperature")</span></span>
8. <span data-ttu-id="e0f5c-213">You can also super-impose one temperature map over the other to get a better feel of difference between target and actual temperatures.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-213">You can also super-impose one temperature map over the other to get a better feel of difference between target and actual temperatures.</span></span> <span data-ttu-id="e0f5c-214">Move the mouse to the corner of the lower area map till you see the handle shape highlighted in a red circle.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-214">Move the mouse to the corner of the lower area map till you see the handle shape highlighted in a red circle.</span></span> <span data-ttu-id="e0f5c-215">Drag the map to the other map on the top and release the mouse when you see the shape highlighted in red rectangle.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-215">Drag the map to the other map on the top and release the mouse when you see the shape highlighted in red rectangle.</span></span>

    <span data-ttu-id="e0f5c-216">![Merge maps](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-use-bi-tools/hdispark.tableau.merge.png "Merge maps")</span><span class="sxs-lookup"><span data-stu-id="e0f5c-216">![Merge maps](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-use-bi-tools/hdispark.tableau.merge.png "Merge maps")</span></span>

     <span data-ttu-id="e0f5c-217">Your data visualization should change as shown in the screenshot:</span><span class="sxs-lookup"><span data-stu-id="e0f5c-217">Your data visualization should change as shown in the screenshot:</span></span>

    <span data-ttu-id="e0f5c-218">![Visualization](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-use-bi-tools/hdispark.tableau.final.visual.png "Visualization")</span><span class="sxs-lookup"><span data-stu-id="e0f5c-218">![Visualization](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-use-bi-tools/hdispark.tableau.final.visual.png "Visualization")</span></span>
9. <span data-ttu-id="e0f5c-219">Click **Save** to save the worksheet.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-219">Click **Save** to save the worksheet.</span></span> <span data-ttu-id="e0f5c-220">You can create dashboards and add one or more sheets to it.</span><span class="sxs-lookup"><span data-stu-id="e0f5c-220">You can create dashboards and add one or more sheets to it.</span></span>

## <a name="seealso"></a><span data-ttu-id="e0f5c-221">See also</span><span class="sxs-lookup"><span data-stu-id="e0f5c-221">See also</span></span>
* [<span data-ttu-id="e0f5c-222">Overview: Apache Spark on Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="e0f5c-222">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="e0f5c-223">Scenarios</span><span class="sxs-lookup"><span data-stu-id="e0f5c-223">Scenarios</span></span>
* [<span data-ttu-id="e0f5c-224">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span><span class="sxs-lookup"><span data-stu-id="e0f5c-224">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="e0f5c-225">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span><span class="sxs-lookup"><span data-stu-id="e0f5c-225">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="e0f5c-226">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span><span class="sxs-lookup"><span data-stu-id="e0f5c-226">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="e0f5c-227">Website log analysis using Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="e0f5c-227">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="e0f5c-228">Create and run applications</span><span class="sxs-lookup"><span data-stu-id="e0f5c-228">Create and run applications</span></span>
* [<span data-ttu-id="e0f5c-229">Create a standalone application using Scala</span><span class="sxs-lookup"><span data-stu-id="e0f5c-229">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="e0f5c-230">Run jobs remotely on a Spark cluster using Livy</span><span class="sxs-lookup"><span data-stu-id="e0f5c-230">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="e0f5c-231">Tools and extensions</span><span class="sxs-lookup"><span data-stu-id="e0f5c-231">Tools and extensions</span></span>
* [<span data-ttu-id="e0f5c-232">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applications</span><span class="sxs-lookup"><span data-stu-id="e0f5c-232">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="e0f5c-233">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span><span class="sxs-lookup"><span data-stu-id="e0f5c-233">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="e0f5c-234">Use Zeppelin notebooks with a Spark cluster on HDInsight</span><span class="sxs-lookup"><span data-stu-id="e0f5c-234">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-use-zeppelin-notebook.md)
* [<span data-ttu-id="e0f5c-235">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span><span class="sxs-lookup"><span data-stu-id="e0f5c-235">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="e0f5c-236">Use external packages with Jupyter notebooks</span><span class="sxs-lookup"><span data-stu-id="e0f5c-236">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="e0f5c-237">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span><span class="sxs-lookup"><span data-stu-id="e0f5c-237">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="e0f5c-238">Manage resources</span><span class="sxs-lookup"><span data-stu-id="e0f5c-238">Manage resources</span></span>
* [<span data-ttu-id="e0f5c-239">Manage resources for the Apache Spark cluster in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="e0f5c-239">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="e0f5c-240">Track and debug jobs running on an Apache Spark cluster in HDInsight</span><span class="sxs-lookup"><span data-stu-id="e0f5c-240">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md


[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-management-portal]: https://manage.windowsazure.com/
[azure-create-storageaccount]: storage-create-storage-account.md

















