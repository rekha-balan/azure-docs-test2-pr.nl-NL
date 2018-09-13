---
title: Use MLlib library in Spark to build machine learning applications on Azure HDInsight | Microsoft Docs
description: Step-by-step instructions on how to use MLlib library in Apache Spark to build machine learning applications
services: hdinsight
documentationcenter: ''
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: c0fd4baa-946d-4e03-ad2c-a03491bd90c8
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/07/2017
ms.author: nitinme
ms.openlocfilehash: e1a756dd8baa6ed26c9f5f5436638e836d9258b6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554942"
---
# <a name="machine-learning-predictive-analysis-on-food-inspection-data-using-mllib-with-apache-spark-cluster-on-hdinsight"></a><span data-ttu-id="dca8e-103">Machine learning: Predictive analysis on food inspection data using MLlib with Apache Spark cluster on HDInsight</span><span class="sxs-lookup"><span data-stu-id="dca8e-103">Machine learning: Predictive analysis on food inspection data using MLlib with Apache Spark cluster on HDInsight</span></span>

> [!TIP]
> <span data-ttu-id="dca8e-104">This tutorial is also available as a Jupyter notebook on a Spark (Linux) cluster that you create in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="dca8e-104">This tutorial is also available as a Jupyter notebook on a Spark (Linux) cluster that you create in HDInsight.</span></span> <span data-ttu-id="dca8e-105">The notebook experience lets you run the Python snippets from the notebook itself.</span><span class="sxs-lookup"><span data-stu-id="dca8e-105">The notebook experience lets you run the Python snippets from the notebook itself.</span></span> <span data-ttu-id="dca8e-106">To perform the tutorial from within a notebook, create a Spark cluster, launch a Jupyter notebook (`https://CLUSTERNAME.azurehdinsight.net/jupyter`), and then run the notebook **Spark Machine Learning - Predictive analysis on food inspection data using MLLib.ipynb** under the **Python** folder.</span><span class="sxs-lookup"><span data-stu-id="dca8e-106">To perform the tutorial from within a notebook, create a Spark cluster, launch a Jupyter notebook (`https://CLUSTERNAME.azurehdinsight.net/jupyter`), and then run the notebook **Spark Machine Learning - Predictive analysis on food inspection data using MLLib.ipynb** under the **Python** folder.</span></span>
>
>

<span data-ttu-id="dca8e-107">This article demonstrates how to use **MLLib**, Spark's built-in machine learning libraries, to perform a simple predictive analysis on an open dataset.</span><span class="sxs-lookup"><span data-stu-id="dca8e-107">This article demonstrates how to use **MLLib**, Spark's built-in machine learning libraries, to perform a simple predictive analysis on an open dataset.</span></span> <span data-ttu-id="dca8e-108">MLLib is a core Spark library that provides a number of utilities that are useful for machine learning tasks, including utilities that are suitable for:</span><span class="sxs-lookup"><span data-stu-id="dca8e-108">MLLib is a core Spark library that provides a number of utilities that are useful for machine learning tasks, including utilities that are suitable for:</span></span>

* <span data-ttu-id="dca8e-109">Classification</span><span class="sxs-lookup"><span data-stu-id="dca8e-109">Classification</span></span>
* <span data-ttu-id="dca8e-110">Regression</span><span class="sxs-lookup"><span data-stu-id="dca8e-110">Regression</span></span>
* <span data-ttu-id="dca8e-111">Clustering</span><span class="sxs-lookup"><span data-stu-id="dca8e-111">Clustering</span></span>
* <span data-ttu-id="dca8e-112">Topic modeling</span><span class="sxs-lookup"><span data-stu-id="dca8e-112">Topic modeling</span></span>
* <span data-ttu-id="dca8e-113">Singular value decomposition (SVD) and principal component analysis (PCA)</span><span class="sxs-lookup"><span data-stu-id="dca8e-113">Singular value decomposition (SVD) and principal component analysis (PCA)</span></span>
* <span data-ttu-id="dca8e-114">Hypothesis testing and calculating sample statistics</span><span class="sxs-lookup"><span data-stu-id="dca8e-114">Hypothesis testing and calculating sample statistics</span></span>

<span data-ttu-id="dca8e-115">This article presents a simple approach to *classification* through logistic regression.</span><span class="sxs-lookup"><span data-stu-id="dca8e-115">This article presents a simple approach to *classification* through logistic regression.</span></span>

## <a name="what-are-classification-and-logistic-regression"></a><span data-ttu-id="dca8e-116">What are classification and logistic regression?</span><span class="sxs-lookup"><span data-stu-id="dca8e-116">What are classification and logistic regression?</span></span>
<span data-ttu-id="dca8e-117">*Classification*, a very common machine learning task, is the process of sorting input data into categories.</span><span class="sxs-lookup"><span data-stu-id="dca8e-117">*Classification*, a very common machine learning task, is the process of sorting input data into categories.</span></span> <span data-ttu-id="dca8e-118">It is the job of a classification algorithm to figure out how to assign "labels" to input data that you provide.</span><span class="sxs-lookup"><span data-stu-id="dca8e-118">It is the job of a classification algorithm to figure out how to assign "labels" to input data that you provide.</span></span> <span data-ttu-id="dca8e-119">For example, you could think of a machine learning algorithm that accepts stock information as input and divides the stock into two categories: stocks which you should sell and stocks which you should retain.</span><span class="sxs-lookup"><span data-stu-id="dca8e-119">For example, you could think of a machine learning algorithm that accepts stock information as input and divides the stock into two categories: stocks which you should sell and stocks which you should retain.</span></span>

<span data-ttu-id="dca8e-120">Logistic regression is the algorithm that you use for classification.</span><span class="sxs-lookup"><span data-stu-id="dca8e-120">Logistic regression is the algorithm that you use for classification.</span></span> <span data-ttu-id="dca8e-121">Spark's logistic regression API is useful for *binary classification*, or classifying input data into one of two groups.</span><span class="sxs-lookup"><span data-stu-id="dca8e-121">Spark's logistic regression API is useful for *binary classification*, or classifying input data into one of two groups.</span></span> <span data-ttu-id="dca8e-122">For more information about logistic regressions, see [Wikipedia](https://en.wikipedia.org/wiki/Logistic_regression).</span><span class="sxs-lookup"><span data-stu-id="dca8e-122">For more information about logistic regressions, see [Wikipedia](https://en.wikipedia.org/wiki/Logistic_regression).</span></span>

<span data-ttu-id="dca8e-123">In summary, the process of logistic regression produces a *logistic function* that can be used to predict the probability that an input vector belongs in one group or the other.</span><span class="sxs-lookup"><span data-stu-id="dca8e-123">In summary, the process of logistic regression produces a *logistic function* that can be used to predict the probability that an input vector belongs in one group or the other.</span></span>  

## <a name="what-are-we-trying-to-accomplish-in-this-article"></a><span data-ttu-id="dca8e-124">What are we trying to accomplish in this article?</span><span class="sxs-lookup"><span data-stu-id="dca8e-124">What are we trying to accomplish in this article?</span></span>
<span data-ttu-id="dca8e-125">You will use Spark to perform some predictive analysis on food inspection data (**Food_Inspections1.csv**) that was acquired through the [City of Chicago data portal](https://data.cityofchicago.org/).</span><span class="sxs-lookup"><span data-stu-id="dca8e-125">You will use Spark to perform some predictive analysis on food inspection data (**Food_Inspections1.csv**) that was acquired through the [City of Chicago data portal](https://data.cityofchicago.org/).</span></span> <span data-ttu-id="dca8e-126">This dataset contains information about food inspections that were conducted in Chicago, including information about each food establishment that was inspected, the violations that were found (if any), and the results of the inspection.</span><span class="sxs-lookup"><span data-stu-id="dca8e-126">This dataset contains information about food inspections that were conducted in Chicago, including information about each food establishment that was inspected, the violations that were found (if any), and the results of the inspection.</span></span> <span data-ttu-id="dca8e-127">The CSV data file is already available in the storage account associated with the cluster at **/HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections1.csv**.</span><span class="sxs-lookup"><span data-stu-id="dca8e-127">The CSV data file is already available in the storage account associated with the cluster at **/HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections1.csv**.</span></span>

<span data-ttu-id="dca8e-128">In the steps below, you develop a model to see what it takes to pass or fail a food inspection.</span><span class="sxs-lookup"><span data-stu-id="dca8e-128">In the steps below, you develop a model to see what it takes to pass or fail a food inspection.</span></span>

## <a name="start-building-a-machine-learning-application-using-spark-mllib"></a><span data-ttu-id="dca8e-129">Start building a machine learning application using Spark MLlib</span><span class="sxs-lookup"><span data-stu-id="dca8e-129">Start building a machine learning application using Spark MLlib</span></span>
1. <span data-ttu-id="dca8e-130">From the [Azure Portal](https://portal.azure.com/), from the startboard, click the tile for your Spark cluster (if you pinned it to the startboard).</span><span class="sxs-lookup"><span data-stu-id="dca8e-130">From the [Azure Portal](https://portal.azure.com/), from the startboard, click the tile for your Spark cluster (if you pinned it to the startboard).</span></span> <span data-ttu-id="dca8e-131">You can also navigate to your cluster under **Browse All** > **HDInsight Clusters**.</span><span class="sxs-lookup"><span data-stu-id="dca8e-131">You can also navigate to your cluster under **Browse All** > **HDInsight Clusters**.</span></span>   
1. <span data-ttu-id="dca8e-132">From the Spark cluster blade, click **Cluster Dashboard**, and then click **Jupyter Notebook**.</span><span class="sxs-lookup"><span data-stu-id="dca8e-132">From the Spark cluster blade, click **Cluster Dashboard**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="dca8e-133">If prompted, enter the admin credentials for the cluster.</span><span class="sxs-lookup"><span data-stu-id="dca8e-133">If prompted, enter the admin credentials for the cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="dca8e-134">You may also reach the Jupyter Notebook for your cluster by opening the following URL in your browser.</span><span class="sxs-lookup"><span data-stu-id="dca8e-134">You may also reach the Jupyter Notebook for your cluster by opening the following URL in your browser.</span></span> <span data-ttu-id="dca8e-135">Replace **CLUSTERNAME** with the name of your cluster:</span><span class="sxs-lookup"><span data-stu-id="dca8e-135">Replace **CLUSTERNAME** with the name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
1. <span data-ttu-id="dca8e-136">Create a new notebook.</span><span class="sxs-lookup"><span data-stu-id="dca8e-136">Create a new notebook.</span></span> <span data-ttu-id="dca8e-137">Click **New**, and then click **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="dca8e-137">Click **New**, and then click **PySpark**.</span></span>

    <span data-ttu-id="dca8e-138">![Create a new Jupyter notebook](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-machine-learning-mllib-ipython/hdispark.note.jupyter.createnotebook.png "Create a new Jupyter notebook")</span><span class="sxs-lookup"><span data-stu-id="dca8e-138">![Create a new Jupyter notebook](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-machine-learning-mllib-ipython/hdispark.note.jupyter.createnotebook.png "Create a new Jupyter notebook")</span></span>
1. <span data-ttu-id="dca8e-139">A new notebook is created and opened with the name Untitled.pynb.</span><span class="sxs-lookup"><span data-stu-id="dca8e-139">A new notebook is created and opened with the name Untitled.pynb.</span></span> <span data-ttu-id="dca8e-140">Click the notebook name at the top, and enter a friendly name.</span><span class="sxs-lookup"><span data-stu-id="dca8e-140">Click the notebook name at the top, and enter a friendly name.</span></span>

    <span data-ttu-id="dca8e-141">![Provide a name for the notebook](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-machine-learning-mllib-ipython/hdispark.note.jupyter.notebook.name.png "Provide a name for the notebook")</span><span class="sxs-lookup"><span data-stu-id="dca8e-141">![Provide a name for the notebook](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-machine-learning-mllib-ipython/hdispark.note.jupyter.notebook.name.png "Provide a name for the notebook")</span></span>
1. <span data-ttu-id="dca8e-142">Because you created a notebook using the PySpark kernel, you do not need to create any contexts explicitly.</span><span class="sxs-lookup"><span data-stu-id="dca8e-142">Because you created a notebook using the PySpark kernel, you do not need to create any contexts explicitly.</span></span> <span data-ttu-id="dca8e-143">The Spark and Hive contexts will be automatically created for you when you run the first code cell.</span><span class="sxs-lookup"><span data-stu-id="dca8e-143">The Spark and Hive contexts will be automatically created for you when you run the first code cell.</span></span> <span data-ttu-id="dca8e-144">You can start building your machine learning application by importing the types required for this scenario.</span><span class="sxs-lookup"><span data-stu-id="dca8e-144">You can start building your machine learning application by importing the types required for this scenario.</span></span> <span data-ttu-id="dca8e-145">To do so, place the cursor in the cell and press **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="dca8e-145">To do so, place the cursor in the cell and press **SHIFT + ENTER**.</span></span>

        from pyspark.ml import Pipeline
        from pyspark.ml.classification import LogisticRegression
        from pyspark.ml.feature import HashingTF, Tokenizer
        from pyspark.sql import Row
        from pyspark.sql.functions import UserDefinedFunction
        from pyspark.sql.types import *

## <a name="construct-an-input-dataframe"></a><span data-ttu-id="dca8e-146">Construct an input dataframe</span><span class="sxs-lookup"><span data-stu-id="dca8e-146">Construct an input dataframe</span></span>
<span data-ttu-id="dca8e-147">We can use `sqlContext` to perform transformations on structured data.</span><span class="sxs-lookup"><span data-stu-id="dca8e-147">We can use `sqlContext` to perform transformations on structured data.</span></span> <span data-ttu-id="dca8e-148">The first task is to load the sample data ((**Food_Inspections1.csv**)) into a Spark SQL *dataframe*.</span><span class="sxs-lookup"><span data-stu-id="dca8e-148">The first task is to load the sample data ((**Food_Inspections1.csv**)) into a Spark SQL *dataframe*.</span></span>

1. <span data-ttu-id="dca8e-149">Because the raw data is in a CSV format, we need to use the Spark context to pull every line of the file into memory as unstructured text; then, you use Python's CSV library to parse each line individually.</span><span class="sxs-lookup"><span data-stu-id="dca8e-149">Because the raw data is in a CSV format, we need to use the Spark context to pull every line of the file into memory as unstructured text; then, you use Python's CSV library to parse each line individually.</span></span>

        def csvParse(s):
            import csv
            from StringIO import StringIO
            sio = StringIO(s)
            value = csv.reader(sio).next()
            sio.close()
            return value

        inspections = sc.textFile('wasbs:///HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections1.csv')\
                        .map(csvParse)
1. <span data-ttu-id="dca8e-150">We now have the CSV file as an RDD.</span><span class="sxs-lookup"><span data-stu-id="dca8e-150">We now have the CSV file as an RDD.</span></span> <span data-ttu-id="dca8e-151">Let us retrieve one row from the RDD to understand the schema of the data.</span><span class="sxs-lookup"><span data-stu-id="dca8e-151">Let us retrieve one row from the RDD to understand the schema of the data.</span></span>

        inspections.take(1)

    <span data-ttu-id="dca8e-152">You should see an output like the following:</span><span class="sxs-lookup"><span data-stu-id="dca8e-152">You should see an output like the following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        [['413707',
          'LUNA PARK INC',
          'LUNA PARK  DAY CARE',
          '2049789',
          "Children's Services Facility",
          'Risk 1 (High)',
          '3250 W FOSTER AVE ',
          'CHICAGO',
          'IL',
          '60625',
          '09/21/2010',
          'License-Task Force',
          'Fail',
          '24. DISH WASHING FACILITIES: PROPERLY DESIGNED, CONSTRUCTED, MAINTAINED, INSTALLED, LOCATED AND OPERATED - Comments: All dishwashing machines must be of a type that complies with all requirements of the plumbing section of the Municipal Code of Chicago and Rules and Regulation of the Board of Health. OBSEVERD THE 3 COMPARTMENT SINK BACKING UP INTO THE 1ST AND 2ND COMPARTMENT WITH CLEAR WATER AND SLOWLY DRAINING OUT. INST NEED HAVE IT REPAIR. CITATION ISSUED, SERIOUS VIOLATION 7-38-030 H000062369-10 COURT DATE 10-28-10 TIME 1 P.M. ROOM 107 400 W. SURPERIOR. | 36. LIGHTING: REQUIRED MINIMUM FOOT-CANDLES OF LIGHT PROVIDED, FIXTURES SHIELDED - Comments: Shielding to protect against broken glass falling into food shall be provided for all artificial lighting sources in preparation, service, and display facilities. LIGHT SHIELD ARE MISSING UNDER HOOD OF  COOKING EQUIPMENT AND NEED TO REPLACE LIGHT UNDER UNIT. 4 LIGHTS ARE OUT IN THE REAR CHILDREN AREA,IN THE KINDERGARDEN CLASS ROOM. 2 LIGHT ARE OUT EAST REAR, LIGHT FRONT WEST ROOM. NEED TO REPLACE ALL LIGHT THAT ARE NOT WORKING. | 35. WALLS, CEILINGS, ATTACHED EQUIPMENT CONSTRUCTED PER CODE: GOOD REPAIR, SURFACES CLEAN AND DUST-LESS CLEANING METHODS - Comments: The walls and ceilings shall be in good repair and easily cleaned. MISSING CEILING TILES WITH STAINS IN WEST,EAST, IN FRONT AREA WEST, AND BY THE 15MOS AREA. NEED TO BE REPLACED. | 32. FOOD AND NON-FOOD CONTACT SURFACES PROPERLY DESIGNED, CONSTRUCTED AND MAINTAINED - Comments: All food and non-food contact equipment and utensils shall be smooth, easily cleanable, and durable, and shall be in good repair. SPLASH GUARDED ARE NEEDED BY THE EXPOSED HAND SINK IN THE KITCHEN AREA | 34. FLOORS: CONSTRUCTED PER CODE, CLEANED, GOOD REPAIR, COVING INSTALLED, DUST-LESS CLEANING METHODS USED - Comments: The floors shall be constructed per code, be smooth and easily cleaned, and be kept clean and in good repair. INST NEED TO ELEVATE ALL FOOD ITEMS 6INCH OFF THE FLOOR 6 INCH AWAY FORM WALL.  ',
          '41.97583445690982',
          '-87.7107455232781',
          '(41.97583445690982, -87.7107455232781)']]
1. <span data-ttu-id="dca8e-153">The above output gives us an idea of the schema of the input file; the file includes the name of every establishment, the type of establishment, the address, the data of the inspections, and the location, among other things.</span><span class="sxs-lookup"><span data-stu-id="dca8e-153">The above output gives us an idea of the schema of the input file; the file includes the name of every establishment, the type of establishment, the address, the data of the inspections, and the location, among other things.</span></span> <span data-ttu-id="dca8e-154">Let's select a few columns that will be useful for our predictive analysis and group the results as a dataframe, which we then use to create a temporary table.</span><span class="sxs-lookup"><span data-stu-id="dca8e-154">Let's select a few columns that will be useful for our predictive analysis and group the results as a dataframe, which we then use to create a temporary table.</span></span>

        schema = StructType([
        StructField("id", IntegerType(), False),
        StructField("name", StringType(), False),
        StructField("results", StringType(), False),
        StructField("violations", StringType(), True)])

        df = sqlContext.createDataFrame(inspections.map(lambda l: (int(l[0]), l[1], l[12], l[13])) , schema)
        df.registerTempTable('CountResults')
1. <span data-ttu-id="dca8e-155">We now have a *dataframe*, `df` on which we can perform our analysis.</span><span class="sxs-lookup"><span data-stu-id="dca8e-155">We now have a *dataframe*, `df` on which we can perform our analysis.</span></span> <span data-ttu-id="dca8e-156">We also have a temporary table call **CountResults**.</span><span class="sxs-lookup"><span data-stu-id="dca8e-156">We also have a temporary table call **CountResults**.</span></span> <span data-ttu-id="dca8e-157">We've included 4 columns of interest in the dataframe: **id**, **name**, **results**, and **violations**.</span><span class="sxs-lookup"><span data-stu-id="dca8e-157">We've included 4 columns of interest in the dataframe: **id**, **name**, **results**, and **violations**.</span></span>

    <span data-ttu-id="dca8e-158">Let's get a small sample of the data:</span><span class="sxs-lookup"><span data-stu-id="dca8e-158">Let's get a small sample of the data:</span></span>

        df.show(5)

    <span data-ttu-id="dca8e-159">You should see an output like the following:</span><span class="sxs-lookup"><span data-stu-id="dca8e-159">You should see an output like the following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        +------+--------------------+-------+--------------------+
        |    id|                name|results|          violations|
        +------+--------------------+-------+--------------------+
        |413707|       LUNA PARK INC|   Fail|24. DISH WASHING ...|
        |391234|       CAFE SELMARIE|   Fail|2. FACILITIES TO ...|
        |413751|          MANCHU WOK|   Pass|33. FOOD AND NON-...|
        |413708|BENCHMARK HOSPITA...|   Pass|                    |
        |413722|           JJ BURGER|   Pass|                    |
        +------+--------------------+-------+--------------------+

## <a name="understand-the-data"></a><span data-ttu-id="dca8e-160">Understand the data</span><span class="sxs-lookup"><span data-stu-id="dca8e-160">Understand the data</span></span>
1. <span data-ttu-id="dca8e-161">Let's start to get a sense of what our dataset contains.</span><span class="sxs-lookup"><span data-stu-id="dca8e-161">Let's start to get a sense of what our dataset contains.</span></span> <span data-ttu-id="dca8e-162">For example, what are the different values in the **results** column?</span><span class="sxs-lookup"><span data-stu-id="dca8e-162">For example, what are the different values in the **results** column?</span></span>

        df.select('results').distinct().show()

    <span data-ttu-id="dca8e-163">You should see an output like the following:</span><span class="sxs-lookup"><span data-stu-id="dca8e-163">You should see an output like the following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        +--------------------+
        |             results|
        +--------------------+
        |                Fail|
        |Business Not Located|
        |                Pass|
        |  Pass w/ Conditions|
        |     Out of Business|
        +--------------------+
1. <span data-ttu-id="dca8e-164">A quick visualization can help us reason about the distribution of these outcomes.</span><span class="sxs-lookup"><span data-stu-id="dca8e-164">A quick visualization can help us reason about the distribution of these outcomes.</span></span> <span data-ttu-id="dca8e-165">We already have the data in a temporary table **CountResults**.</span><span class="sxs-lookup"><span data-stu-id="dca8e-165">We already have the data in a temporary table **CountResults**.</span></span> <span data-ttu-id="dca8e-166">You can run the following SQL query against the table to get a better understanding of how the results are distributed.</span><span class="sxs-lookup"><span data-stu-id="dca8e-166">You can run the following SQL query against the table to get a better understanding of how the results are distributed.</span></span>

        %%sql -o countResultsdf
        SELECT results, COUNT(results) AS cnt FROM CountResults GROUP BY results

    <span data-ttu-id="dca8e-167">The `%%sql` magic followed by `-o countResultsdf` ensures that the output of the query is persisted locally on the Jupyter server (typically the headnode of the cluster).</span><span class="sxs-lookup"><span data-stu-id="dca8e-167">The `%%sql` magic followed by `-o countResultsdf` ensures that the output of the query is persisted locally on the Jupyter server (typically the headnode of the cluster).</span></span> <span data-ttu-id="dca8e-168">The output is persisted as a [Pandas](http://pandas.pydata.org/) dataframe with the specified name **countResultsdf**.</span><span class="sxs-lookup"><span data-stu-id="dca8e-168">The output is persisted as a [Pandas](http://pandas.pydata.org/) dataframe with the specified name **countResultsdf**.</span></span>

    <span data-ttu-id="dca8e-169">You should see an output like the following:</span><span class="sxs-lookup"><span data-stu-id="dca8e-169">You should see an output like the following:</span></span>

    <span data-ttu-id="dca8e-170">![SQL query output](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-machine-learning-mllib-ipython/query.output.png "SQL query output")</span><span class="sxs-lookup"><span data-stu-id="dca8e-170">![SQL query output](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-machine-learning-mllib-ipython/query.output.png "SQL query output")</span></span>

    <span data-ttu-id="dca8e-171">For more information about the `%%sql` magic, as well as other magics available with the PySpark kernel, see [Kernels available on Jupyter notebooks with Spark HDInsight clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span><span class="sxs-lookup"><span data-stu-id="dca8e-171">For more information about the `%%sql` magic, as well as other magics available with the PySpark kernel, see [Kernels available on Jupyter notebooks with Spark HDInsight clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>
1. <span data-ttu-id="dca8e-172">You can also use Matplotlib, a library used to construct visualization of data, to create a plot.</span><span class="sxs-lookup"><span data-stu-id="dca8e-172">You can also use Matplotlib, a library used to construct visualization of data, to create a plot.</span></span> <span data-ttu-id="dca8e-173">Because the plot must be created from the locally persisted **countResultsdf** dataframe, the code snippet must begin with the `%%local` magic.</span><span class="sxs-lookup"><span data-stu-id="dca8e-173">Because the plot must be created from the locally persisted **countResultsdf** dataframe, the code snippet must begin with the `%%local` magic.</span></span> <span data-ttu-id="dca8e-174">This ensures that the code is run locally on the Jupyter server.</span><span class="sxs-lookup"><span data-stu-id="dca8e-174">This ensures that the code is run locally on the Jupyter server.</span></span>

        %%local
        %matplotlib inline
        import matplotlib.pyplot as plt

        labels = countResultsdf['results']
        sizes = countResultsdf['cnt']
        colors = ['turquoise', 'seagreen', 'mediumslateblue', 'palegreen', 'coral']
        plt.pie(sizes, labels=labels, autopct='%1.1f%%', colors=colors)
        plt.axis('equal')

    <span data-ttu-id="dca8e-175">You should see an output like the following:</span><span class="sxs-lookup"><span data-stu-id="dca8e-175">You should see an output like the following:</span></span>

    ![Result output](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-machine-learning-mllib-ipython/output_13_1.png)
1. <span data-ttu-id="dca8e-177">You can see that there are 5 distinct results that an inspection can have:</span><span class="sxs-lookup"><span data-stu-id="dca8e-177">You can see that there are 5 distinct results that an inspection can have:</span></span>

   * <span data-ttu-id="dca8e-178">Business not located</span><span class="sxs-lookup"><span data-stu-id="dca8e-178">Business not located</span></span>
   * <span data-ttu-id="dca8e-179">Fail</span><span class="sxs-lookup"><span data-stu-id="dca8e-179">Fail</span></span>
   * <span data-ttu-id="dca8e-180">Pass</span><span class="sxs-lookup"><span data-stu-id="dca8e-180">Pass</span></span>
   * <span data-ttu-id="dca8e-181">Pss w/ conditions, and</span><span class="sxs-lookup"><span data-stu-id="dca8e-181">Pss w/ conditions, and</span></span>
   * <span data-ttu-id="dca8e-182">Out of Business</span><span class="sxs-lookup"><span data-stu-id="dca8e-182">Out of Business</span></span>

     <span data-ttu-id="dca8e-183">Let us develop a model that can guess the outcome of a food inspection, given the violations.</span><span class="sxs-lookup"><span data-stu-id="dca8e-183">Let us develop a model that can guess the outcome of a food inspection, given the violations.</span></span> <span data-ttu-id="dca8e-184">Since logistic regression is a binary classification method, it makes sense to group our data into two categories: **Fail** and **Pass**.</span><span class="sxs-lookup"><span data-stu-id="dca8e-184">Since logistic regression is a binary classification method, it makes sense to group our data into two categories: **Fail** and **Pass**.</span></span> <span data-ttu-id="dca8e-185">A "Pass w/ Conditions" is still a Pass, so when we train the model, we will consider the two results equivalent.</span><span class="sxs-lookup"><span data-stu-id="dca8e-185">A "Pass w/ Conditions" is still a Pass, so when we train the model, we will consider the two results equivalent.</span></span> <span data-ttu-id="dca8e-186">Data with the other results ("Business Not Located", "Out of Business") are not useful so we will remove them from our training set.</span><span class="sxs-lookup"><span data-stu-id="dca8e-186">Data with the other results ("Business Not Located", "Out of Business") are not useful so we will remove them from our training set.</span></span> <span data-ttu-id="dca8e-187">This should be okay since these two categories make up a very small percentage of the results anyway.</span><span class="sxs-lookup"><span data-stu-id="dca8e-187">This should be okay since these two categories make up a very small percentage of the results anyway.</span></span>
1. <span data-ttu-id="dca8e-188">Let us go ahead and convert our existing dataframe(`df`) into a new dataframe where each inspection is represented as a label-violations pair.</span><span class="sxs-lookup"><span data-stu-id="dca8e-188">Let us go ahead and convert our existing dataframe(`df`) into a new dataframe where each inspection is represented as a label-violations pair.</span></span> <span data-ttu-id="dca8e-189">In our case, a label of `0.0` represents a failure, a label of `1.0` represents a success, and a label of `-1.0` represents some results besides those two.</span><span class="sxs-lookup"><span data-stu-id="dca8e-189">In our case, a label of `0.0` represents a failure, a label of `1.0` represents a success, and a label of `-1.0` represents some results besides those two.</span></span> <span data-ttu-id="dca8e-190">We will filter those other results out when computing the new data frame.</span><span class="sxs-lookup"><span data-stu-id="dca8e-190">We will filter those other results out when computing the new data frame.</span></span>

        def labelForResults(s):
            if s == 'Fail':
                return 0.0
            elif s == 'Pass w/ Conditions' or s == 'Pass':
                return 1.0
            else:
                return -1.0
        label = UserDefinedFunction(labelForResults, DoubleType())
        labeledData = df.select(label(df.results).alias('label'), df.violations).where('label >= 0')

    <span data-ttu-id="dca8e-191">Let's retrieve one row from the labeled data to see what it looks like.</span><span class="sxs-lookup"><span data-stu-id="dca8e-191">Let's retrieve one row from the labeled data to see what it looks like.</span></span>

        labeledData.take(1)

    <span data-ttu-id="dca8e-192">You should see an output like the following:</span><span class="sxs-lookup"><span data-stu-id="dca8e-192">You should see an output like the following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        [Row(label=0.0, violations=u"41. PREMISES MAINTAINED FREE OF LITTER, UNNECESSARY ARTICLES, CLEANING  EQUIPMENT PROPERLY STORED - Comments: All parts of the food establishment and all parts of the property used in connection with the operation of the establishment shall be kept neat and clean and should not produce any offensive odors.  REMOVE MATTRESS FROM SMALL DUMPSTER. | 35. WALLS, CEILINGS, ATTACHED EQUIPMENT CONSTRUCTED PER CODE: GOOD REPAIR, SURFACES CLEAN AND DUST-LESS CLEANING METHODS - Comments: The walls and ceilings shall be in good repair and easily cleaned.  REPAIR MISALIGNED DOORS AND DOOR NEAR ELEVATOR.  DETAIL CLEAN BLACK MOLD LIKE SUBSTANCE FROM WALLS BY BOTH DISH MACHINES.  REPAIR OR REMOVE BASEBOARD UNDER DISH MACHINE (LEFT REAR KITCHEN). SEAL ALL GAPS.  REPLACE MILK CRATES USED IN WALK IN COOLERS AND STORAGE AREAS WITH PROPER SHELVING AT LEAST 6' OFF THE FLOOR.  | 38. VENTILATION: ROOMS AND EQUIPMENT VENTED AS REQUIRED: PLUMBING: INSTALLED AND MAINTAINED - Comments: The flow of air discharged from kitchen fans shall always be through a duct to a point above the roofline.  REPAIR BROKEN VENTILATION IN MEN'S AND WOMEN'S WASHROOMS NEXT TO DINING AREA. | 32. FOOD AND NON-FOOD CONTACT SURFACES PROPERLY DESIGNED, CONSTRUCTED AND MAINTAINED - Comments: All food and non-food contact equipment and utensils shall be smooth, easily cleanable, and durable, and shall be in good repair.  REPAIR DAMAGED PLUG ON LEFT SIDE OF 2 COMPARTMENT SINK.  REPAIR SELF CLOSER ON BOTTOM LEFT DOOR OF 4 DOOR PREP UNIT NEXT TO OFFICE.")]

## <a name="create-a-logistic-regression-model-from-the-input-dataframe"></a><span data-ttu-id="dca8e-193">Create a logistic regression model from the input dataframe</span><span class="sxs-lookup"><span data-stu-id="dca8e-193">Create a logistic regression model from the input dataframe</span></span>
<span data-ttu-id="dca8e-194">Our final task is to convert the labeled data into a format that can be analyzed by logistic regression.</span><span class="sxs-lookup"><span data-stu-id="dca8e-194">Our final task is to convert the labeled data into a format that can be analyzed by logistic regression.</span></span> <span data-ttu-id="dca8e-195">The input to a logistic regression algorithm should be a set of *label-feature vector pairs*, where the "feature vector" is a vector of numbers that represents the input point in some way.</span><span class="sxs-lookup"><span data-stu-id="dca8e-195">The input to a logistic regression algorithm should be a set of *label-feature vector pairs*, where the "feature vector" is a vector of numbers that represents the input point in some way.</span></span> <span data-ttu-id="dca8e-196">So, we need a way to convert the "violations" column, which is semi-structured and contains a lot of comments in free-text, to an array of real numbers that a machine could easily understand.</span><span class="sxs-lookup"><span data-stu-id="dca8e-196">So, we need a way to convert the "violations" column, which is semi-structured and contains a lot of comments in free-text, to an array of real numbers that a machine could easily understand.</span></span>

<span data-ttu-id="dca8e-197">One standard machine learning approach for processing natural language is to assign each distinct word an "index", and then pass a vector to the machine learning algorithm such that each index's value contains the relative frequency of that word in the text string.</span><span class="sxs-lookup"><span data-stu-id="dca8e-197">One standard machine learning approach for processing natural language is to assign each distinct word an "index", and then pass a vector to the machine learning algorithm such that each index's value contains the relative frequency of that word in the text string.</span></span>

<span data-ttu-id="dca8e-198">MLLib provides an easy way to perform this operation.</span><span class="sxs-lookup"><span data-stu-id="dca8e-198">MLLib provides an easy way to perform this operation.</span></span> <span data-ttu-id="dca8e-199">First, we'll "tokenize" each violations string to get the individual words in each string, and then we'll use a `HashingTF` to convert each set of tokens into a feature vector which can then be passed to the logistic regression algorithm to construct a model.</span><span class="sxs-lookup"><span data-stu-id="dca8e-199">First, we'll "tokenize" each violations string to get the individual words in each string, and then we'll use a `HashingTF` to convert each set of tokens into a feature vector which can then be passed to the logistic regression algorithm to construct a model.</span></span> <span data-ttu-id="dca8e-200">We'll conduct all of these steps in sequence using a "pipeline".</span><span class="sxs-lookup"><span data-stu-id="dca8e-200">We'll conduct all of these steps in sequence using a "pipeline".</span></span>

    tokenizer = Tokenizer(inputCol="violations", outputCol="words")
    hashingTF = HashingTF(inputCol=tokenizer.getOutputCol(), outputCol="features")
    lr = LogisticRegression(maxIter=10, regParam=0.01)
    pipeline = Pipeline(stages=[tokenizer, hashingTF, lr])

    model = pipeline.fit(labeledData)

## <a name="evaluate-the-model-on-a-separate-test-dataset"></a><span data-ttu-id="dca8e-201">Evaluate the model on a separate test dataset</span><span class="sxs-lookup"><span data-stu-id="dca8e-201">Evaluate the model on a separate test dataset</span></span>
<span data-ttu-id="dca8e-202">We can use the model we created earlier to *predict* what the results of new inspections will be, based on the violations that were observed.</span><span class="sxs-lookup"><span data-stu-id="dca8e-202">We can use the model we created earlier to *predict* what the results of new inspections will be, based on the violations that were observed.</span></span> <span data-ttu-id="dca8e-203">We trained this model on the dataset **Food_Inspections1.csv**.</span><span class="sxs-lookup"><span data-stu-id="dca8e-203">We trained this model on the dataset **Food_Inspections1.csv**.</span></span> <span data-ttu-id="dca8e-204">Let us use a second dataset, **Food_Inspections2.csv**, to *evaluate* the strength of this model on new data.</span><span class="sxs-lookup"><span data-stu-id="dca8e-204">Let us use a second dataset, **Food_Inspections2.csv**, to *evaluate* the strength of this model on new data.</span></span> <span data-ttu-id="dca8e-205">This second data set (**Food_Inspections2.csv**) should already be in the default storage container associated with the cluster.</span><span class="sxs-lookup"><span data-stu-id="dca8e-205">This second data set (**Food_Inspections2.csv**) should already be in the default storage container associated with the cluster.</span></span>

1. <span data-ttu-id="dca8e-206">The snippet below creates a new dataframe, **predictionsDf** that contains the prediction generated by the model.</span><span class="sxs-lookup"><span data-stu-id="dca8e-206">The snippet below creates a new dataframe, **predictionsDf** that contains the prediction generated by the model.</span></span> <span data-ttu-id="dca8e-207">The snippet also creates a temporary table **Predictions** based on the dataframe.</span><span class="sxs-lookup"><span data-stu-id="dca8e-207">The snippet also creates a temporary table **Predictions** based on the dataframe.</span></span>

        testData = sc.textFile('wasbs:///HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections2.csv')\
                 .map(csvParse) \
                 .map(lambda l: (int(l[0]), l[1], l[12], l[13]))
        testDf = sqlContext.createDataFrame(testData, schema).where("results = 'Fail' OR results = 'Pass' OR results = 'Pass w/ Conditions'")
        predictionsDf = model.transform(testDf)
        predictionsDf.registerTempTable('Predictions')
        predictionsDf.columns

    <span data-ttu-id="dca8e-208">You should see an output like the following:</span><span class="sxs-lookup"><span data-stu-id="dca8e-208">You should see an output like the following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        ['id',
         'name',
         'results',
         'violations',
         'words',
         'features',
         'rawPrediction',
         'probability',
         'prediction']
1. <span data-ttu-id="dca8e-209">Look at one of the predictions.</span><span class="sxs-lookup"><span data-stu-id="dca8e-209">Look at one of the predictions.</span></span> <span data-ttu-id="dca8e-210">Run this snippet:</span><span class="sxs-lookup"><span data-stu-id="dca8e-210">Run this snippet:</span></span>

        predictionsDf.take(1)

    <span data-ttu-id="dca8e-211">You will see the prediction for the first entry in the test data set.</span><span class="sxs-lookup"><span data-stu-id="dca8e-211">You will see the prediction for the first entry in the test data set.</span></span>
1. <span data-ttu-id="dca8e-212">The `model.transform()` method will apply the same transformation to any new data with the same schema, and arrive at a prediction of how to classify the data.</span><span class="sxs-lookup"><span data-stu-id="dca8e-212">The `model.transform()` method will apply the same transformation to any new data with the same schema, and arrive at a prediction of how to classify the data.</span></span> <span data-ttu-id="dca8e-213">We can do some simple statistics to get a sense of how accurate our predictions were:</span><span class="sxs-lookup"><span data-stu-id="dca8e-213">We can do some simple statistics to get a sense of how accurate our predictions were:</span></span>

        numSuccesses = predictionsDf.where("""(prediction = 0 AND results = 'Fail') OR
                                              (prediction = 1 AND (results = 'Pass' OR
                                                                   results = 'Pass w/ Conditions'))""").count()
        numInspections = predictionsDf.count()

        print "There were", numInspections, "inspections and there were", numSuccesses, "successful predictions"
        print "This is a", str((float(numSuccesses) / float(numInspections)) * 100) + "%", "success rate"

    <span data-ttu-id="dca8e-214">The output looks like the following:</span><span class="sxs-lookup"><span data-stu-id="dca8e-214">The output looks like the following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        There were 9315 inspections and there were 8087 successful predictions
        This is a 86.8169618894% success rate

    <span data-ttu-id="dca8e-215">Using logistic regression with Spark gives us an accurate model of the relationship between violations descriptions in English and whether a given business would pass or fail a food inspection.</span><span class="sxs-lookup"><span data-stu-id="dca8e-215">Using logistic regression with Spark gives us an accurate model of the relationship between violations descriptions in English and whether a given business would pass or fail a food inspection.</span></span>

## <a name="create-a-visual-representation-of-the-prediction"></a><span data-ttu-id="dca8e-216">Create a visual representation of the prediction</span><span class="sxs-lookup"><span data-stu-id="dca8e-216">Create a visual representation of the prediction</span></span>
<span data-ttu-id="dca8e-217">We can now construct a final visualization to help us reason about the results of this test.</span><span class="sxs-lookup"><span data-stu-id="dca8e-217">We can now construct a final visualization to help us reason about the results of this test.</span></span>

1. <span data-ttu-id="dca8e-218">We start by extracting the different predictions and results from the **Predictions** temporary table created earlier.</span><span class="sxs-lookup"><span data-stu-id="dca8e-218">We start by extracting the different predictions and results from the **Predictions** temporary table created earlier.</span></span> <span data-ttu-id="dca8e-219">The following queries separate the output as *true_positive*, *false_positive*, *true_negative*, and *false_negative*.</span><span class="sxs-lookup"><span data-stu-id="dca8e-219">The following queries separate the output as *true_positive*, *false_positive*, *true_negative*, and *false_negative*.</span></span> <span data-ttu-id="dca8e-220">In the queries below, we turn off visualization by using `-q` and also save the output (by using `-o`) as dataframes that can be then used with the `%%local` magic.</span><span class="sxs-lookup"><span data-stu-id="dca8e-220">In the queries below, we turn off visualization by using `-q` and also save the output (by using `-o`) as dataframes that can be then used with the `%%local` magic.</span></span>

        %%sql -q -o true_positive
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 0 AND results = 'Fail'

        %%sql -q -o false_positive
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 0 AND (results = 'Pass' OR results = 'Pass w/ Conditions')

        %%sql -q -o true_negative
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 1 AND results = 'Fail'

        %%sql -q -o false_negative
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 1 AND (results = 'Pass' OR results = 'Pass w/ Conditions')
1. <span data-ttu-id="dca8e-221">Finally, use the following snippet to generate the plot using **Matplotlib**.</span><span class="sxs-lookup"><span data-stu-id="dca8e-221">Finally, use the following snippet to generate the plot using **Matplotlib**.</span></span>

        %%local
        %matplotlib inline
        import matplotlib.pyplot as plt

        labels = ['True positive', 'False positive', 'True negative', 'False negative']
        sizes = [true_positive['cnt'], false_positive['cnt'], false_negative['cnt'], true_negative['cnt']]
        colors = ['turquoise', 'seagreen', 'mediumslateblue', 'palegreen', 'coral']
        plt.pie(sizes, labels=labels, autopct='%1.1f%%', colors=colors)
        plt.axis('equal')

    <span data-ttu-id="dca8e-222">You should see the following output.</span><span class="sxs-lookup"><span data-stu-id="dca8e-222">You should see the following output.</span></span>

    ![Prediction output](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-machine-learning-mllib-ipython/output_26_1.png)

    <span data-ttu-id="dca8e-224">In this chart, a "positive" result refers to the failed food inspection, while a negative result refers to a passed inspection.</span><span class="sxs-lookup"><span data-stu-id="dca8e-224">In this chart, a "positive" result refers to the failed food inspection, while a negative result refers to a passed inspection.</span></span>

## <a name="shut-down-the-notebook"></a><span data-ttu-id="dca8e-225">Shut down the notebook</span><span class="sxs-lookup"><span data-stu-id="dca8e-225">Shut down the notebook</span></span>
<span data-ttu-id="dca8e-226">After you have finished running the application, you should shutdown the notebook to release the resources.</span><span class="sxs-lookup"><span data-stu-id="dca8e-226">After you have finished running the application, you should shutdown the notebook to release the resources.</span></span> <span data-ttu-id="dca8e-227">To do so, from the **File** menu on the notebook, click **Close and Halt**.</span><span class="sxs-lookup"><span data-stu-id="dca8e-227">To do so, from the **File** menu on the notebook, click **Close and Halt**.</span></span> <span data-ttu-id="dca8e-228">This will shutdown and close the notebook.</span><span class="sxs-lookup"><span data-stu-id="dca8e-228">This will shutdown and close the notebook.</span></span>

## <a name="seealso"></a><span data-ttu-id="dca8e-229">See also</span><span class="sxs-lookup"><span data-stu-id="dca8e-229">See also</span></span>
* [<span data-ttu-id="dca8e-230">Overview: Apache Spark on Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="dca8e-230">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="dca8e-231">Scenarios</span><span class="sxs-lookup"><span data-stu-id="dca8e-231">Scenarios</span></span>
* [<span data-ttu-id="dca8e-232">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span><span class="sxs-lookup"><span data-stu-id="dca8e-232">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="dca8e-233">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span><span class="sxs-lookup"><span data-stu-id="dca8e-233">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="dca8e-234">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span><span class="sxs-lookup"><span data-stu-id="dca8e-234">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="dca8e-235">Website log analysis using Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="dca8e-235">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="dca8e-236">Create and run applications</span><span class="sxs-lookup"><span data-stu-id="dca8e-236">Create and run applications</span></span>
* [<span data-ttu-id="dca8e-237">Create a standalone application using Scala</span><span class="sxs-lookup"><span data-stu-id="dca8e-237">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="dca8e-238">Run jobs remotely on a Spark cluster using Livy</span><span class="sxs-lookup"><span data-stu-id="dca8e-238">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="dca8e-239">Tools and extensions</span><span class="sxs-lookup"><span data-stu-id="dca8e-239">Tools and extensions</span></span>
* [<span data-ttu-id="dca8e-240">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applicatons</span><span class="sxs-lookup"><span data-stu-id="dca8e-240">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="dca8e-241">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span><span class="sxs-lookup"><span data-stu-id="dca8e-241">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="dca8e-242">Use Zeppelin notebooks with a Spark cluster on HDInsight</span><span class="sxs-lookup"><span data-stu-id="dca8e-242">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-use-zeppelin-notebook.md)
* [<span data-ttu-id="dca8e-243">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span><span class="sxs-lookup"><span data-stu-id="dca8e-243">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="dca8e-244">Use external packages with Jupyter notebooks</span><span class="sxs-lookup"><span data-stu-id="dca8e-244">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="dca8e-245">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span><span class="sxs-lookup"><span data-stu-id="dca8e-245">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="dca8e-246">Manage resources</span><span class="sxs-lookup"><span data-stu-id="dca8e-246">Manage resources</span></span>
* [<span data-ttu-id="dca8e-247">Manage resources for the Apache Spark cluster in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="dca8e-247">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="dca8e-248">Track and debug jobs running on an Apache Spark cluster in HDInsight</span><span class="sxs-lookup"><span data-stu-id="dca8e-248">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)





