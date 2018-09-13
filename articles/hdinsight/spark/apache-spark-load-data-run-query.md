---
title: 'Tutorial: Load data and run queries on an Apache Spark cluster in Azure HDInsight '
description: Learn how to load data and run interactive queries on Spark clusters in Azure HDInsight.
services: azure-hdinsight
author: jasonwhowell
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive,mvc
ms.topic: tutorial
ms.author: jasonh
ms.date: 05/17/2018
ms.openlocfilehash: d59f04c5dde522f3d193f345ac59147ece9d86f0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864407"
---
# <a name="tutorial-load-data-and-run-queries-on-an-apache-spark-cluster-in-azure-hdinsight"></a><span data-ttu-id="bac20-103">Tutorial: Load data and run queries on an Apache Spark cluster in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="bac20-103">Tutorial: Load data and run queries on an Apache Spark cluster in Azure HDInsight</span></span>

<span data-ttu-id="bac20-104">In this tutorial, you learn how to use create a dataframe from a csv file, and how to run interactive Spark SQL queries against an Apache Spark cluster in Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bac20-104">In this tutorial, you learn how to use create a dataframe from a csv file, and how to run interactive Spark SQL queries against an Apache Spark cluster in Azure HDInsight.</span></span> <span data-ttu-id="bac20-105">In Spark, a dataframe is a distributed collection of data organized into named columns.</span><span class="sxs-lookup"><span data-stu-id="bac20-105">In Spark, a dataframe is a distributed collection of data organized into named columns.</span></span> <span data-ttu-id="bac20-106">Dataframe is conceptually equivalent to a table in a relational database or a data frame in R/Python.</span><span class="sxs-lookup"><span data-stu-id="bac20-106">Dataframe is conceptually equivalent to a table in a relational database or a data frame in R/Python.</span></span>
 
<span data-ttu-id="bac20-107">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="bac20-107">In this tutorial, you learn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="bac20-108">Create a dataframe from a csv file</span><span class="sxs-lookup"><span data-stu-id="bac20-108">Create a dataframe from a csv file</span></span>
> * <span data-ttu-id="bac20-109">Run queries on the dataframe</span><span class="sxs-lookup"><span data-stu-id="bac20-109">Run queries on the dataframe</span></span>

<span data-ttu-id="bac20-110">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span><span class="sxs-lookup"><span data-stu-id="bac20-110">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bac20-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="bac20-111">Prerequisites</span></span>

* <span data-ttu-id="bac20-112">Complete [Create an Apache Spark cluster in Azure HDInsight](apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="bac20-112">Complete [Create an Apache Spark cluster in Azure HDInsight](apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="create-a-dataframe-from-a-csv-file"></a><span data-ttu-id="bac20-113">Create a dataframe from a csv file</span><span class="sxs-lookup"><span data-stu-id="bac20-113">Create a dataframe from a csv file</span></span>

<span data-ttu-id="bac20-114">Applications can create dataframes from an existing Resilient Distributed Dataset (RDD), from a Hive table, or from data sources using the SQLContext object.</span><span class="sxs-lookup"><span data-stu-id="bac20-114">Applications can create dataframes from an existing Resilient Distributed Dataset (RDD), from a Hive table, or from data sources using the SQLContext object.</span></span> <span data-ttu-id="bac20-115">The following screenshot shows a snapshot of the HVAC.csv file used in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="bac20-115">The following screenshot shows a snapshot of the HVAC.csv file used in this tutorial.</span></span> <span data-ttu-id="bac20-116">The csv file comes with all HDInsight Spark clusters.</span><span class="sxs-lookup"><span data-stu-id="bac20-116">The csv file comes with all HDInsight Spark clusters.</span></span> <span data-ttu-id="bac20-117">The data captures the temperature variations of some buildings.</span><span class="sxs-lookup"><span data-stu-id="bac20-117">The data captures the temperature variations of some buildings.</span></span>
    
<span data-ttu-id="bac20-118">![Snapshot of data for interactive Spark SQL query](./media/apache-spark-load-data-run-query/hdinsight-spark-sample-data-interactive-spark-sql-query.png "Snapshot of data for interactive Spark SQL query")</span><span class="sxs-lookup"><span data-stu-id="bac20-118">![Snapshot of data for interactive Spark SQL query](./media/apache-spark-load-data-run-query/hdinsight-spark-sample-data-interactive-spark-sql-query.png "Snapshot of data for interactive Spark SQL query")</span></span>


1. <span data-ttu-id="bac20-119">Open the Jupyter notebook that you created in the prerequisites section.</span><span class="sxs-lookup"><span data-stu-id="bac20-119">Open the Jupyter notebook that you created in the prerequisites section.</span></span>
2. <span data-ttu-id="bac20-120">Paste the following code in an empty cell of the notebook, and then press **SHIFT + ENTER** to run the code.</span><span class="sxs-lookup"><span data-stu-id="bac20-120">Paste the following code in an empty cell of the notebook, and then press **SHIFT + ENTER** to run the code.</span></span> <span data-ttu-id="bac20-121">The code imports the types required for this scenario:</span><span class="sxs-lookup"><span data-stu-id="bac20-121">The code imports the types required for this scenario:</span></span>

    ```PySpark
    from pyspark.sql import *
    from pyspark.sql.types import *
    ```

    <span data-ttu-id="bac20-122">When running an interactive query in Jupyter, the web browser window or tab caption shows a **(Busy)** status along with the notebook title.</span><span class="sxs-lookup"><span data-stu-id="bac20-122">When running an interactive query in Jupyter, the web browser window or tab caption shows a **(Busy)** status along with the notebook title.</span></span> <span data-ttu-id="bac20-123">You also see a solid circle next to the **PySpark** text in the top-right corner.</span><span class="sxs-lookup"><span data-stu-id="bac20-123">You also see a solid circle next to the **PySpark** text in the top-right corner.</span></span> <span data-ttu-id="bac20-124">After the job is completed, it changes to a hollow circle.</span><span class="sxs-lookup"><span data-stu-id="bac20-124">After the job is completed, it changes to a hollow circle.</span></span>

    <span data-ttu-id="bac20-125">![Status of interactive Spark SQL query](./media/apache-spark-load-data-run-query/hdinsight-spark-interactive-spark-query-status.png "Status of interactive Spark SQL query")</span><span class="sxs-lookup"><span data-stu-id="bac20-125">![Status of interactive Spark SQL query](./media/apache-spark-load-data-run-query/hdinsight-spark-interactive-spark-query-status.png "Status of interactive Spark SQL query")</span></span>

3. <span data-ttu-id="bac20-126">Run the following code to create a dataframe and a temporary table (**hvac**) by running the following code.</span><span class="sxs-lookup"><span data-stu-id="bac20-126">Run the following code to create a dataframe and a temporary table (**hvac**) by running the following code.</span></span> 

    ```PySpark
    # Create an RDD from sample data
    csvFile = spark.read.csv('wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv', header=True, inferSchema=True)
    csvFile.write.saveAsTable("hvac")
    ```

    > [!NOTE]
    > <span data-ttu-id="bac20-127">By using the PySpark kernel to create a notebook, the SQL contexts are automatically created for you when you run the first code cell.</span><span class="sxs-lookup"><span data-stu-id="bac20-127">By using the PySpark kernel to create a notebook, the SQL contexts are automatically created for you when you run the first code cell.</span></span> <span data-ttu-id="bac20-128">You do not need to explicitly create any contexts.</span><span class="sxs-lookup"><span data-stu-id="bac20-128">You do not need to explicitly create any contexts.</span></span>


## <a name="run-queries-on-the-dataframe"></a><span data-ttu-id="bac20-129">Run queries on the dataframe</span><span class="sxs-lookup"><span data-stu-id="bac20-129">Run queries on the dataframe</span></span>

<span data-ttu-id="bac20-130">Once the table is created, you can run an interactive query on the data.</span><span class="sxs-lookup"><span data-stu-id="bac20-130">Once the table is created, you can run an interactive query on the data.</span></span>

1. <span data-ttu-id="bac20-131">Run the following code in an empty cell of the notebook:</span><span class="sxs-lookup"><span data-stu-id="bac20-131">Run the following code in an empty cell of the notebook:</span></span>

    ```PySpark
    %%sql
    SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"
    ```

   <span data-ttu-id="bac20-132">Because the PySpark kernel is used in the notebook, you can now directly run an interactive SQL query on the temporary table **hvac**.</span><span class="sxs-lookup"><span data-stu-id="bac20-132">Because the PySpark kernel is used in the notebook, you can now directly run an interactive SQL query on the temporary table **hvac**.</span></span>

   <span data-ttu-id="bac20-133">The following tabular output is displayed.</span><span class="sxs-lookup"><span data-stu-id="bac20-133">The following tabular output is displayed.</span></span>

     <span data-ttu-id="bac20-134">![Table output of interactive Spark query result](./media/apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result.png "Table output of interactive Spark query result")</span><span class="sxs-lookup"><span data-stu-id="bac20-134">![Table output of interactive Spark query result](./media/apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result.png "Table output of interactive Spark query result")</span></span>

3. <span data-ttu-id="bac20-135">You can also see the results in other visualizations as well.</span><span class="sxs-lookup"><span data-stu-id="bac20-135">You can also see the results in other visualizations as well.</span></span> <span data-ttu-id="bac20-136">To see an area graph for the same output, select **Area** then set other values as shown.</span><span class="sxs-lookup"><span data-stu-id="bac20-136">To see an area graph for the same output, select **Area** then set other values as shown.</span></span>

    <span data-ttu-id="bac20-137">![Area graph of interactive Spark query result](./media/apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result-area-chart.png "Area graph of interactive Spark query result")</span><span class="sxs-lookup"><span data-stu-id="bac20-137">![Area graph of interactive Spark query result](./media/apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result-area-chart.png "Area graph of interactive Spark query result")</span></span>

10. <span data-ttu-id="bac20-138">From the **File** menu on the notebook, select **Save and Checkpoint**.</span><span class="sxs-lookup"><span data-stu-id="bac20-138">From the **File** menu on the notebook, select **Save and Checkpoint**.</span></span> 

11. <span data-ttu-id="bac20-139">If you're starting the [next tutorial](apache-spark-use-bi-tools.md) now, leave the notebook open.</span><span class="sxs-lookup"><span data-stu-id="bac20-139">If you're starting the [next tutorial](apache-spark-use-bi-tools.md) now, leave the notebook open.</span></span> <span data-ttu-id="bac20-140">If not, shut down the notebook to release the cluster resources: from the **File** menu on the notebook, selectx **Close and Halt**.</span><span class="sxs-lookup"><span data-stu-id="bac20-140">If not, shut down the notebook to release the cluster resources: from the **File** menu on the notebook, selectx **Close and Halt**.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="bac20-141">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="bac20-141">Clean up resources</span></span>

<span data-ttu-id="bac20-142">With HDInsight, your data is stored in Azure Storage or Azure Data Lake Store, so you can safely delete a cluster when it is not in use.</span><span class="sxs-lookup"><span data-stu-id="bac20-142">With HDInsight, your data is stored in Azure Storage or Azure Data Lake Store, so you can safely delete a cluster when it is not in use.</span></span> <span data-ttu-id="bac20-143">You are also charged for an HDInsight cluster, even when it is not in use.</span><span class="sxs-lookup"><span data-stu-id="bac20-143">You are also charged for an HDInsight cluster, even when it is not in use.</span></span> <span data-ttu-id="bac20-144">Since the charges for the cluster are many times more than the charges for storage, it makes economic sense to delete clusters when they are not in use.</span><span class="sxs-lookup"><span data-stu-id="bac20-144">Since the charges for the cluster are many times more than the charges for storage, it makes economic sense to delete clusters when they are not in use.</span></span> <span data-ttu-id="bac20-145">If you plan to work on the next tutorial immediately, you might want to keep the cluster.</span><span class="sxs-lookup"><span data-stu-id="bac20-145">If you plan to work on the next tutorial immediately, you might want to keep the cluster.</span></span>

<span data-ttu-id="bac20-146">Open the cluster in the Azure portal, and select **Delete**.</span><span class="sxs-lookup"><span data-stu-id="bac20-146">Open the cluster in the Azure portal, and select **Delete**.</span></span>

<span data-ttu-id="bac20-147">![Delete HDInsight cluster](./media/apache-spark-load-data-run-query/hdinsight-azure-portal-delete-cluster.png "Delete HDInsight cluster")</span><span class="sxs-lookup"><span data-stu-id="bac20-147">![Delete HDInsight cluster](./media/apache-spark-load-data-run-query/hdinsight-azure-portal-delete-cluster.png "Delete HDInsight cluster")</span></span>

<span data-ttu-id="bac20-148">You can also select the resource group name to open the resource group page, and then select **Delete resource group**.</span><span class="sxs-lookup"><span data-stu-id="bac20-148">You can also select the resource group name to open the resource group page, and then select **Delete resource group**.</span></span> <span data-ttu-id="bac20-149">By deleting the resource group, you delete both the HDInsight Spark cluster, and the default storage account.</span><span class="sxs-lookup"><span data-stu-id="bac20-149">By deleting the resource group, you delete both the HDInsight Spark cluster, and the default storage account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bac20-150">Next steps</span><span class="sxs-lookup"><span data-stu-id="bac20-150">Next steps</span></span>

<span data-ttu-id="bac20-151">In this tutorial, you learned how to:</span><span class="sxs-lookup"><span data-stu-id="bac20-151">In this tutorial, you learned how to:</span></span>

* <span data-ttu-id="bac20-152">Create a Spark dataframe.</span><span class="sxs-lookup"><span data-stu-id="bac20-152">Create a Spark dataframe.</span></span>
* <span data-ttu-id="bac20-153">Run Spark SQL against the dataframe.</span><span class="sxs-lookup"><span data-stu-id="bac20-153">Run Spark SQL against the dataframe.</span></span>

<span data-ttu-id="bac20-154">Advance to the next article to see how the data you registered in Spark can be pulled into a BI analytics tool such as Power BI.</span><span class="sxs-lookup"><span data-stu-id="bac20-154">Advance to the next article to see how the data you registered in Spark can be pulled into a BI analytics tool such as Power BI.</span></span> 
> [!div class="nextstepaction"]
> [<span data-ttu-id="bac20-155">Analyze data using BI tools</span><span class="sxs-lookup"><span data-stu-id="bac20-155">Analyze data using BI tools</span></span>](apache-spark-use-bi-tools.md)

