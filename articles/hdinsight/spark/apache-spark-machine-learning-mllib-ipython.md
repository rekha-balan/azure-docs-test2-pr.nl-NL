---
title: Machine learning example with Spark MLlib on HDInsight - Azure
description: Learn how to use Spark MLlib to create a machine learning app that analyzes a dataset using classification through logistic regression.
keywords: spark machine learning, spark machine learning example
services: hdinsight
author: jasonwhowell
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.topic: conceptual
ms.date: 05/18/2018
ms.author: jasonh
ms.openlocfilehash: 78f9240e6b01bafc68b71d20044c7ec7458cc972
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871645"
---
# <a name="use-spark-mllib-to-build-a-machine-learning-application-and-analyze-a-dataset"></a><span data-ttu-id="282d6-104">Use Spark MLlib to build a machine learning application and analyze a dataset</span><span class="sxs-lookup"><span data-stu-id="282d6-104">Use Spark MLlib to build a machine learning application and analyze a dataset</span></span>

<span data-ttu-id="282d6-105">Learn how to use Spark [MLlib](https://spark.apache.org/mllib/) to create a machine learning application to do simple predictive analysis on an open dataset.</span><span class="sxs-lookup"><span data-stu-id="282d6-105">Learn how to use Spark [MLlib](https://spark.apache.org/mllib/) to create a machine learning application to do simple predictive analysis on an open dataset.</span></span> <span data-ttu-id="282d6-106">From Spark's built-in machine learning libraries, this example uses *classification* through logistic regression.</span><span class="sxs-lookup"><span data-stu-id="282d6-106">From Spark's built-in machine learning libraries, this example uses *classification* through logistic regression.</span></span> 

> [!TIP]
> <span data-ttu-id="282d6-107">This example is also available as a Jupyter notebook on a Spark (Linux) cluster that you create in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="282d6-107">This example is also available as a Jupyter notebook on a Spark (Linux) cluster that you create in HDInsight.</span></span> <span data-ttu-id="282d6-108">The notebook experience lets you run the Python snippets from the notebook itself.</span><span class="sxs-lookup"><span data-stu-id="282d6-108">The notebook experience lets you run the Python snippets from the notebook itself.</span></span> <span data-ttu-id="282d6-109">To follow the tutorial from within a notebook, create a Spark cluster and launch a Jupyter notebook (`https://CLUSTERNAME.azurehdinsight.net/jupyter`).</span><span class="sxs-lookup"><span data-stu-id="282d6-109">To follow the tutorial from within a notebook, create a Spark cluster and launch a Jupyter notebook (`https://CLUSTERNAME.azurehdinsight.net/jupyter`).</span></span> <span data-ttu-id="282d6-110">Then, run the notebook **Spark Machine Learning - Predictive analysis on food inspection data using MLlib.ipynb** under the **Python** folder.</span><span class="sxs-lookup"><span data-stu-id="282d6-110">Then, run the notebook **Spark Machine Learning - Predictive analysis on food inspection data using MLlib.ipynb** under the **Python** folder.</span></span>
>
>

<span data-ttu-id="282d6-111">MLlib is a core Spark library that provides many utilities useful for machine learning tasks, including utilities that are suitable for:</span><span class="sxs-lookup"><span data-stu-id="282d6-111">MLlib is a core Spark library that provides many utilities useful for machine learning tasks, including utilities that are suitable for:</span></span>

* <span data-ttu-id="282d6-112">Classification</span><span class="sxs-lookup"><span data-stu-id="282d6-112">Classification</span></span>
* <span data-ttu-id="282d6-113">Regression</span><span class="sxs-lookup"><span data-stu-id="282d6-113">Regression</span></span>
* <span data-ttu-id="282d6-114">Clustering</span><span class="sxs-lookup"><span data-stu-id="282d6-114">Clustering</span></span>
* <span data-ttu-id="282d6-115">Topic modeling</span><span class="sxs-lookup"><span data-stu-id="282d6-115">Topic modeling</span></span>
* <span data-ttu-id="282d6-116">Singular value decomposition (SVD) and principal component analysis (PCA)</span><span class="sxs-lookup"><span data-stu-id="282d6-116">Singular value decomposition (SVD) and principal component analysis (PCA)</span></span>
* <span data-ttu-id="282d6-117">Hypothesis testing and calculating sample statistics</span><span class="sxs-lookup"><span data-stu-id="282d6-117">Hypothesis testing and calculating sample statistics</span></span>

## <a name="understand-classification-and-logistic-regression"></a><span data-ttu-id="282d6-118">Understand classification and logistic regression</span><span class="sxs-lookup"><span data-stu-id="282d6-118">Understand classification and logistic regression</span></span>
<span data-ttu-id="282d6-119">*Classification*, a popular machine learning task, is the process of sorting input data into categories.</span><span class="sxs-lookup"><span data-stu-id="282d6-119">*Classification*, a popular machine learning task, is the process of sorting input data into categories.</span></span> <span data-ttu-id="282d6-120">It is the job of a classification algorithm to figure out how to assign "labels" to input data that you provide.</span><span class="sxs-lookup"><span data-stu-id="282d6-120">It is the job of a classification algorithm to figure out how to assign "labels" to input data that you provide.</span></span> <span data-ttu-id="282d6-121">For example, you could think of a machine learning algorithm that accepts stock information as input and divides the stock into two categories: stocks that you should sell and stocks that you should keep.</span><span class="sxs-lookup"><span data-stu-id="282d6-121">For example, you could think of a machine learning algorithm that accepts stock information as input and divides the stock into two categories: stocks that you should sell and stocks that you should keep.</span></span>

<span data-ttu-id="282d6-122">Logistic regression is the algorithm that you use for classification.</span><span class="sxs-lookup"><span data-stu-id="282d6-122">Logistic regression is the algorithm that you use for classification.</span></span> <span data-ttu-id="282d6-123">Spark's logistic regression API is useful for *binary classification*, or classifying input data into one of two groups.</span><span class="sxs-lookup"><span data-stu-id="282d6-123">Spark's logistic regression API is useful for *binary classification*, or classifying input data into one of two groups.</span></span> <span data-ttu-id="282d6-124">For more information about logistic regressions, see [Wikipedia](https://en.wikipedia.org/wiki/Logistic_regression).</span><span class="sxs-lookup"><span data-stu-id="282d6-124">For more information about logistic regressions, see [Wikipedia](https://en.wikipedia.org/wiki/Logistic_regression).</span></span>

<span data-ttu-id="282d6-125">In summary, the process of logistic regression produces a *logistic function* that can be used to predict the probability that an input vector belongs in one group or the other.</span><span class="sxs-lookup"><span data-stu-id="282d6-125">In summary, the process of logistic regression produces a *logistic function* that can be used to predict the probability that an input vector belongs in one group or the other.</span></span>  

## <a name="predictive-analysis-example-on-food-inspection-data"></a><span data-ttu-id="282d6-126">Predictive analysis example on food inspection data</span><span class="sxs-lookup"><span data-stu-id="282d6-126">Predictive analysis example on food inspection data</span></span>
<span data-ttu-id="282d6-127">In this example, you use Spark to perform some predictive analysis on food inspection data (**Food_Inspections1.csv**) that was acquired through the [City of Chicago data portal](https://data.cityofchicago.org/).</span><span class="sxs-lookup"><span data-stu-id="282d6-127">In this example, you use Spark to perform some predictive analysis on food inspection data (**Food_Inspections1.csv**) that was acquired through the [City of Chicago data portal](https://data.cityofchicago.org/).</span></span> <span data-ttu-id="282d6-128">This dataset contains information about food establishment inspections that were conducted in Chicago, including information about each establishment, the violations found (if any), and the results of the inspection.</span><span class="sxs-lookup"><span data-stu-id="282d6-128">This dataset contains information about food establishment inspections that were conducted in Chicago, including information about each establishment, the violations found (if any), and the results of the inspection.</span></span> <span data-ttu-id="282d6-129">The CSV data file is already available in the storage account associated with the cluster at **/HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections1.csv**.</span><span class="sxs-lookup"><span data-stu-id="282d6-129">The CSV data file is already available in the storage account associated with the cluster at **/HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections1.csv**.</span></span>

<span data-ttu-id="282d6-130">In the steps below, you develop a model to see what it takes to pass or fail a food inspection.</span><span class="sxs-lookup"><span data-stu-id="282d6-130">In the steps below, you develop a model to see what it takes to pass or fail a food inspection.</span></span>

## <a name="create-a-spark-mllib-machine-learning-app"></a><span data-ttu-id="282d6-131">Create a Spark MLlib machine learning app</span><span class="sxs-lookup"><span data-stu-id="282d6-131">Create a Spark MLlib machine learning app</span></span>

1. <span data-ttu-id="282d6-132">Create a Jupyter notebook using the PySpark kernel.</span><span class="sxs-lookup"><span data-stu-id="282d6-132">Create a Jupyter notebook using the PySpark kernel.</span></span> <span data-ttu-id="282d6-133">For the instructions, see [Create a Jupyter notebook](./apache-spark-jupyter-spark-sql.md#create-a-jupyter-notebook).</span><span class="sxs-lookup"><span data-stu-id="282d6-133">For the instructions, see [Create a Jupyter notebook](./apache-spark-jupyter-spark-sql.md#create-a-jupyter-notebook).</span></span>

2. <span data-ttu-id="282d6-134">Import the types required for this application.</span><span class="sxs-lookup"><span data-stu-id="282d6-134">Import the types required for this application.</span></span> <span data-ttu-id="282d6-135">Copy and paste the following code into an empty cell, and then press **SHIRT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="282d6-135">Copy and paste the following code into an empty cell, and then press **SHIRT + ENTER**.</span></span>

    ```PySpark
    from pyspark.ml import Pipeline
    from pyspark.ml.classification import LogisticRegression
    from pyspark.ml.feature import HashingTF, Tokenizer
    from pyspark.sql import Row
    from pyspark.sql.functions import UserDefinedFunction
    from pyspark.sql.types import *
    ```
    <span data-ttu-id="282d6-136">Because of the PySpark kernel, you do not need to create any contexts explicitly.</span><span class="sxs-lookup"><span data-stu-id="282d6-136">Because of the PySpark kernel, you do not need to create any contexts explicitly.</span></span> <span data-ttu-id="282d6-137">The Spark and Hive contexts are automatically created for you when you run the first code cell.</span><span class="sxs-lookup"><span data-stu-id="282d6-137">The Spark and Hive contexts are automatically created for you when you run the first code cell.</span></span> 

## <a name="construct-the-input-dataframe"></a><span data-ttu-id="282d6-138">Construct the input dataframe</span><span class="sxs-lookup"><span data-stu-id="282d6-138">Construct the input dataframe</span></span>

<span data-ttu-id="282d6-139">Because the raw data is in a CSV format, you can use the Spark context to pull the file into memory as unstructured text, and then use Python's CSV library to parse each line of the data.</span><span class="sxs-lookup"><span data-stu-id="282d6-139">Because the raw data is in a CSV format, you can use the Spark context to pull the file into memory as unstructured text, and then use Python's CSV library to parse each line of the data.</span></span>

1. <span data-ttu-id="282d6-140">Run the following lines to create a Resilient Distributed Dataset (RDD) by importing and parsing the input data.</span><span class="sxs-lookup"><span data-stu-id="282d6-140">Run the following lines to create a Resilient Distributed Dataset (RDD) by importing and parsing the input data.</span></span>

    ```PySpark
    def csvParse(s):
        import csv
        from StringIO import StringIO
        sio = StringIO(s)
        value = csv.reader(sio).next()
        sio.close()
        return value
    
    inspections = sc.textFile('wasb:///HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections1.csv')\
                    .map(csvParse)
    ```

2. <span data-ttu-id="282d6-141">Run the following code to retrieve one row from the RDD, so you can take a look of the data schema:</span><span class="sxs-lookup"><span data-stu-id="282d6-141">Run the following code to retrieve one row from the RDD, so you can take a look of the data schema:</span></span>

    ```PySpark
    inspections.take(1)
    ```

    <span data-ttu-id="282d6-142">The output is:</span><span class="sxs-lookup"><span data-stu-id="282d6-142">The output is:</span></span>

    ```
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
    ```

    <span data-ttu-id="282d6-143">The output gives you an idea of the schema of the input file.</span><span class="sxs-lookup"><span data-stu-id="282d6-143">The output gives you an idea of the schema of the input file.</span></span> <span data-ttu-id="282d6-144">It includes the name of every establishment, the type of establishment, the address, the data of the inspections, and the location, among other things.</span><span class="sxs-lookup"><span data-stu-id="282d6-144">It includes the name of every establishment, the type of establishment, the address, the data of the inspections, and the location, among other things.</span></span> 

3. <span data-ttu-id="282d6-145">Run the following code to create a dataframe (*df*) and a temporary table (*CountResults*) with a few columns that are useful for the predictive analysis.</span><span class="sxs-lookup"><span data-stu-id="282d6-145">Run the following code to create a dataframe (*df*) and a temporary table (*CountResults*) with a few columns that are useful for the predictive analysis.</span></span> <span data-ttu-id="282d6-146">`sqlContext` is used to perform transformations on structured data.</span><span class="sxs-lookup"><span data-stu-id="282d6-146">`sqlContext` is used to perform transformations on structured data.</span></span> 

    ```PySpark
    schema = StructType([
    StructField("id", IntegerType(), False),
    StructField("name", StringType(), False),
    StructField("results", StringType(), False),
    StructField("violations", StringType(), True)])
    
    df = spark.createDataFrame(inspections.map(lambda l: (int(l[0]), l[1], l[12], l[13])) , schema)
    df.registerTempTable('CountResults')
    ```

    <span data-ttu-id="282d6-147">The four columns of interest in the dataframe are **id**, **name**, **results**, and **violations**.</span><span class="sxs-lookup"><span data-stu-id="282d6-147">The four columns of interest in the dataframe are **id**, **name**, **results**, and **violations**.</span></span>

4. <span data-ttu-id="282d6-148">Run the following code to get a small sample of the data:</span><span class="sxs-lookup"><span data-stu-id="282d6-148">Run the following code to get a small sample of the data:</span></span>

    ```PySpark
    df.show(5)
    ```

    <span data-ttu-id="282d6-149">The output is:</span><span class="sxs-lookup"><span data-stu-id="282d6-149">The output is:</span></span>

    ```
    +------+--------------------+-------+--------------------+
    |    id|                name|results|          violations|
    +------+--------------------+-------+--------------------+
    |413707|       LUNA PARK INC|   Fail|24. DISH WASHING ...|
    |391234|       CAFE SELMARIE|   Fail|2. FACILITIES TO ...|
    |413751|          MANCHU WOK|   Pass|33. FOOD AND NON-...|
    |413708|BENCHMARK HOSPITA...|   Pass|                    |
    |413722|           JJ BURGER|   Pass|                    |
    +------+--------------------+-------+--------------------+
    ```

## <a name="understand-the-data"></a><span data-ttu-id="282d6-150">Understand the data</span><span class="sxs-lookup"><span data-stu-id="282d6-150">Understand the data</span></span>

<span data-ttu-id="282d6-151">Let's start to get a sense of what the dataset contains.</span><span class="sxs-lookup"><span data-stu-id="282d6-151">Let's start to get a sense of what the dataset contains.</span></span> 

1. <span data-ttu-id="282d6-152">Run the following code to show the distinct values in the **results** column:</span><span class="sxs-lookup"><span data-stu-id="282d6-152">Run the following code to show the distinct values in the **results** column:</span></span>

    ```PySpark
    df.select('results').distinct().show()
    ```

    <span data-ttu-id="282d6-153">The output is:</span><span class="sxs-lookup"><span data-stu-id="282d6-153">The output is:</span></span>

    ```
    +--------------------+
    |             results|
    +--------------------+
    |                Fail|
    |Business Not Located|
    |                Pass|
    |  Pass w/ Conditions|
    |     Out of Business|
    +--------------------+
    ```

2. <span data-ttu-id="282d6-154">Run the following code to visualize the distribution of these results:</span><span class="sxs-lookup"><span data-stu-id="282d6-154">Run the following code to visualize the distribution of these results:</span></span>

    ```PySpark
    %%sql -o countResultsdf
    SELECT results, COUNT(results) AS cnt FROM CountResults GROUP BY results
    ```

    <span data-ttu-id="282d6-155">The `%%sql` magic followed by `-o countResultsdf` ensures that the output of the query is persisted locally on the Jupyter server (typically the headnode of the cluster).</span><span class="sxs-lookup"><span data-stu-id="282d6-155">The `%%sql` magic followed by `-o countResultsdf` ensures that the output of the query is persisted locally on the Jupyter server (typically the headnode of the cluster).</span></span> <span data-ttu-id="282d6-156">The output is persisted as a [Pandas](http://pandas.pydata.org/) dataframe with the specified name **countResultsdf**.</span><span class="sxs-lookup"><span data-stu-id="282d6-156">The output is persisted as a [Pandas](http://pandas.pydata.org/) dataframe with the specified name **countResultsdf**.</span></span> <span data-ttu-id="282d6-157">For more information about the `%%sql` magic, and other magics available with the PySpark kernel, see [Kernels available on Jupyter notebooks with Spark HDInsight clusters](apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span><span class="sxs-lookup"><span data-stu-id="282d6-157">For more information about the `%%sql` magic, and other magics available with the PySpark kernel, see [Kernels available on Jupyter notebooks with Spark HDInsight clusters](apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>

    <span data-ttu-id="282d6-158">The output is:</span><span class="sxs-lookup"><span data-stu-id="282d6-158">The output is:</span></span>

    <span data-ttu-id="282d6-159">![SQL query output](./media/apache-spark-machine-learning-mllib-ipython/spark-machine-learning-query-output.png "SQL query output")</span><span class="sxs-lookup"><span data-stu-id="282d6-159">![SQL query output](./media/apache-spark-machine-learning-mllib-ipython/spark-machine-learning-query-output.png "SQL query output")</span></span>


3. <span data-ttu-id="282d6-160">You can also use [Matplotlib](https://en.wikipedia.org/wiki/Matplotlib), a library used to construct visualization of data, to create a plot.</span><span class="sxs-lookup"><span data-stu-id="282d6-160">You can also use [Matplotlib](https://en.wikipedia.org/wiki/Matplotlib), a library used to construct visualization of data, to create a plot.</span></span> <span data-ttu-id="282d6-161">Because the plot must be created from the locally persisted **countResultsdf** dataframe, the code snippet must begin with the `%%local` magic.</span><span class="sxs-lookup"><span data-stu-id="282d6-161">Because the plot must be created from the locally persisted **countResultsdf** dataframe, the code snippet must begin with the `%%local` magic.</span></span> <span data-ttu-id="282d6-162">This ensures that the code is run locally on the Jupyter server.</span><span class="sxs-lookup"><span data-stu-id="282d6-162">This ensures that the code is run locally on the Jupyter server.</span></span>

    ```PySpark
    %%local
    %matplotlib inline
    import matplotlib.pyplot as plt

    labels = countResultsdf['results']
    sizes = countResultsdf['cnt']
    colors = ['turquoise', 'seagreen', 'mediumslateblue', 'palegreen', 'coral']
    plt.pie(sizes, labels=labels, autopct='%1.1f%%', colors=colors)
    plt.axis('equal')
    ```

    <span data-ttu-id="282d6-163">The output is:</span><span class="sxs-lookup"><span data-stu-id="282d6-163">The output is:</span></span>

    <span data-ttu-id="282d6-164">![Spark machine learning application output - pie chart with five distinct inspection results](./media/apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-1.png "Spark machine learning result output")</span><span class="sxs-lookup"><span data-stu-id="282d6-164">![Spark machine learning application output - pie chart with five distinct inspection results](./media/apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-1.png "Spark machine learning result output")</span></span>

    <span data-ttu-id="282d6-165">There are 5 distinct results that an inspection can have:</span><span class="sxs-lookup"><span data-stu-id="282d6-165">There are 5 distinct results that an inspection can have:</span></span>

    - <span data-ttu-id="282d6-166">Business not located</span><span class="sxs-lookup"><span data-stu-id="282d6-166">Business not located</span></span>
    - <span data-ttu-id="282d6-167">Fail</span><span class="sxs-lookup"><span data-stu-id="282d6-167">Fail</span></span>
    - <span data-ttu-id="282d6-168">Pass</span><span class="sxs-lookup"><span data-stu-id="282d6-168">Pass</span></span>
    - <span data-ttu-id="282d6-169">Pass w/ conditions</span><span class="sxs-lookup"><span data-stu-id="282d6-169">Pass w/ conditions</span></span>
    - <span data-ttu-id="282d6-170">Out of Business</span><span class="sxs-lookup"><span data-stu-id="282d6-170">Out of Business</span></span>

    <span data-ttu-id="282d6-171">To predict a food inspection outcome, you need to develop a model based on the violations.</span><span class="sxs-lookup"><span data-stu-id="282d6-171">To predict a food inspection outcome, you need to develop a model based on the violations.</span></span> <span data-ttu-id="282d6-172">Because logistic regression is a binary classification method, it makes sense to group the result data into two categories: **Fail** and **Pass**:</span><span class="sxs-lookup"><span data-stu-id="282d6-172">Because logistic regression is a binary classification method, it makes sense to group the result data into two categories: **Fail** and **Pass**:</span></span>

    - <span data-ttu-id="282d6-173">Pass</span><span class="sxs-lookup"><span data-stu-id="282d6-173">Pass</span></span>
        - <span data-ttu-id="282d6-174">Pass</span><span class="sxs-lookup"><span data-stu-id="282d6-174">Pass</span></span>
        - <span data-ttu-id="282d6-175">Pass w/ conditions</span><span class="sxs-lookup"><span data-stu-id="282d6-175">Pass w/ conditions</span></span>
    - <span data-ttu-id="282d6-176">Fail</span><span class="sxs-lookup"><span data-stu-id="282d6-176">Fail</span></span>
        - <span data-ttu-id="282d6-177">Fail</span><span class="sxs-lookup"><span data-stu-id="282d6-177">Fail</span></span>
    - <span data-ttu-id="282d6-178">Discard</span><span class="sxs-lookup"><span data-stu-id="282d6-178">Discard</span></span>
        - <span data-ttu-id="282d6-179">Business not located</span><span class="sxs-lookup"><span data-stu-id="282d6-179">Business not located</span></span>
        - <span data-ttu-id="282d6-180">Out of Business</span><span class="sxs-lookup"><span data-stu-id="282d6-180">Out of Business</span></span>

    <span data-ttu-id="282d6-181">Data with the other results ("Business Not Located" or "Out of Business") are not useful, and they make up a very small percentage of the results anyway.</span><span class="sxs-lookup"><span data-stu-id="282d6-181">Data with the other results ("Business Not Located" or "Out of Business") are not useful, and they make up a very small percentage of the results anyway.</span></span>

4. <span data-ttu-id="282d6-182">Run the following code to convert the existing dataframe(`df`) into a new dataframe where each inspection is represented as a label-violations pair.</span><span class="sxs-lookup"><span data-stu-id="282d6-182">Run the following code to convert the existing dataframe(`df`) into a new dataframe where each inspection is represented as a label-violations pair.</span></span> <span data-ttu-id="282d6-183">In this case, a label of `0.0` represents a failure, a label of `1.0` represents a success, and a label of `-1.0` represents some results besides those two.</span><span class="sxs-lookup"><span data-stu-id="282d6-183">In this case, a label of `0.0` represents a failure, a label of `1.0` represents a success, and a label of `-1.0` represents some results besides those two.</span></span> 

    ```PySpark
    def labelForResults(s):
        if s == 'Fail':
            return 0.0
        elif s == 'Pass w/ Conditions' or s == 'Pass':
            return 1.0
        else:
            return -1.0
    label = UserDefinedFunction(labelForResults, DoubleType())
    labeledData = df.select(label(df.results).alias('label'), df.violations).where('label >= 0')
    ```

5. <span data-ttu-id="282d6-184">Run the following code to show one row of the labeled data:</span><span class="sxs-lookup"><span data-stu-id="282d6-184">Run the following code to show one row of the labeled data:</span></span>

    ```PySpark
    labeledData.take(1)
    ```

    <span data-ttu-id="282d6-185">The output is:</span><span class="sxs-lookup"><span data-stu-id="282d6-185">The output is:</span></span>

    ```
    [Row(label=0.0, violations=u"41. PREMISES MAINTAINED FREE OF LITTER, UNNECESSARY ARTICLES, CLEANING  EQUIPMENT PROPERLY STORED - Comments: All parts of the food establishment and all parts of the property used in connection with the operation of the establishment shall be kept neat and clean and should not produce any offensive odors.  REMOVE MATTRESS FROM SMALL DUMPSTER. | 35. WALLS, CEILINGS, ATTACHED EQUIPMENT CONSTRUCTED PER CODE: GOOD REPAIR, SURFACES CLEAN AND DUST-LESS CLEANING METHODS - Comments: The walls and ceilings shall be in good repair and easily cleaned.  REPAIR MISALIGNED DOORS AND DOOR NEAR ELEVATOR.  DETAIL CLEAN BLACK MOLD LIKE SUBSTANCE FROM WALLS BY BOTH DISH MACHINES.  REPAIR OR REMOVE BASEBOARD UNDER DISH MACHINE (LEFT REAR KITCHEN). SEAL ALL GAPS.  REPLACE MILK CRATES USED IN WALK IN COOLERS AND STORAGE AREAS WITH PROPER SHELVING AT LEAST 6' OFF THE FLOOR.  | 38. VENTILATION: ROOMS AND EQUIPMENT VENTED AS REQUIRED: PLUMBING: INSTALLED AND MAINTAINED - Comments: The flow of air discharged from kitchen fans shall always be through a duct to a point above the roofline.  REPAIR BROKEN VENTILATION IN MEN'S AND WOMEN'S WASHROOMS NEXT TO DINING AREA. | 32. FOOD AND NON-FOOD CONTACT SURFACES PROPERLY DESIGNED, CONSTRUCTED AND MAINTAINED - Comments: All food and non-food contact equipment and utensils shall be smooth, easily cleanable, and durable, and shall be in good repair.  REPAIR DAMAGED PLUG ON LEFT SIDE OF 2 COMPARTMENT SINK.  REPAIR SELF CLOSER ON BOTTOM LEFT DOOR OF 4 DOOR PREP UNIT NEXT TO OFFICE.")]
    ```

## <a name="create-a-logistic-regression-model-from-the-input-dataframe"></a><span data-ttu-id="282d6-186">Create a logistic regression model from the input dataframe</span><span class="sxs-lookup"><span data-stu-id="282d6-186">Create a logistic regression model from the input dataframe</span></span>

<span data-ttu-id="282d6-187">The final task is to convert the labeled data into a format that can be analyzed by logistic regression.</span><span class="sxs-lookup"><span data-stu-id="282d6-187">The final task is to convert the labeled data into a format that can be analyzed by logistic regression.</span></span> <span data-ttu-id="282d6-188">The input to a logistic regression algorithm needs be a set of *label-feature vector pairs*, where the "feature vector" is a vector of numbers representing the input point.</span><span class="sxs-lookup"><span data-stu-id="282d6-188">The input to a logistic regression algorithm needs be a set of *label-feature vector pairs*, where the "feature vector" is a vector of numbers representing the input point.</span></span> <span data-ttu-id="282d6-189">So, you need to convert the "violations" column, which is semi-structured and contains many comments in free-text, to an array of real numbers that a machine could easily understand.</span><span class="sxs-lookup"><span data-stu-id="282d6-189">So, you need to convert the "violations" column, which is semi-structured and contains many comments in free-text, to an array of real numbers that a machine could easily understand.</span></span>

<span data-ttu-id="282d6-190">One standard machine learning approach for processing natural language is to assign each distinct word an "index", and then pass a vector to the machine learning algorithm such that each index's value contains the relative frequency of that word in the text string.</span><span class="sxs-lookup"><span data-stu-id="282d6-190">One standard machine learning approach for processing natural language is to assign each distinct word an "index", and then pass a vector to the machine learning algorithm such that each index's value contains the relative frequency of that word in the text string.</span></span>

<span data-ttu-id="282d6-191">MLlib provides an easy way to perform this operation.</span><span class="sxs-lookup"><span data-stu-id="282d6-191">MLlib provides an easy way to perform this operation.</span></span> <span data-ttu-id="282d6-192">First, "tokenize" each violations string to get the individual words in each string.</span><span class="sxs-lookup"><span data-stu-id="282d6-192">First, "tokenize" each violations string to get the individual words in each string.</span></span> <span data-ttu-id="282d6-193">Then, use a `HashingTF` to convert each set of tokens into a feature vector that can then be passed to the logistic regression algorithm to construct a model.</span><span class="sxs-lookup"><span data-stu-id="282d6-193">Then, use a `HashingTF` to convert each set of tokens into a feature vector that can then be passed to the logistic regression algorithm to construct a model.</span></span> <span data-ttu-id="282d6-194">You conduct all of these steps in sequence using a "pipeline".</span><span class="sxs-lookup"><span data-stu-id="282d6-194">You conduct all of these steps in sequence using a "pipeline".</span></span>

```PySpark
tokenizer = Tokenizer(inputCol="violations", outputCol="words")
hashingTF = HashingTF(inputCol=tokenizer.getOutputCol(), outputCol="features")
lr = LogisticRegression(maxIter=10, regParam=0.01)
pipeline = Pipeline(stages=[tokenizer, hashingTF, lr])

model = pipeline.fit(labeledData)
```

## <a name="evaluate-the-model-using-another-dataset"></a><span data-ttu-id="282d6-195">Evaluate the model using another dataset</span><span class="sxs-lookup"><span data-stu-id="282d6-195">Evaluate the model using another dataset</span></span>

<span data-ttu-id="282d6-196">You can use the model you created earlier to *predict* what the results of new inspections will be, based on the violations that were observed.</span><span class="sxs-lookup"><span data-stu-id="282d6-196">You can use the model you created earlier to *predict* what the results of new inspections will be, based on the violations that were observed.</span></span> <span data-ttu-id="282d6-197">You trained this model on the dataset **Food_Inspections1.csv**.</span><span class="sxs-lookup"><span data-stu-id="282d6-197">You trained this model on the dataset **Food_Inspections1.csv**.</span></span> <span data-ttu-id="282d6-198">You can use a second dataset, **Food_Inspections2.csv**, to *evaluate* the strength of this model on the new data.</span><span class="sxs-lookup"><span data-stu-id="282d6-198">You can use a second dataset, **Food_Inspections2.csv**, to *evaluate* the strength of this model on the new data.</span></span> <span data-ttu-id="282d6-199">This second data set (**Food_Inspections2.csv**) is in the default storage container associated with the cluster.</span><span class="sxs-lookup"><span data-stu-id="282d6-199">This second data set (**Food_Inspections2.csv**) is in the default storage container associated with the cluster.</span></span>

1. <span data-ttu-id="282d6-200">Run the following code to create a new dataframe, **predictionsDf** that contains the prediction generated by the model.</span><span class="sxs-lookup"><span data-stu-id="282d6-200">Run the following code to create a new dataframe, **predictionsDf** that contains the prediction generated by the model.</span></span> <span data-ttu-id="282d6-201">The snippet also creates a temporary table called **Predictions** based on the dataframe.</span><span class="sxs-lookup"><span data-stu-id="282d6-201">The snippet also creates a temporary table called **Predictions** based on the dataframe.</span></span>

    ```PySpark
    testData = sc.textFile('wasb:///HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections2.csv')\
                .map(csvParse) \
                .map(lambda l: (int(l[0]), l[1], l[12], l[13]))
    testDf = spark.createDataFrame(testData, schema).where("results = 'Fail' OR results = 'Pass' OR results = 'Pass w/ Conditions'")
    predictionsDf = model.transform(testDf)
    predictionsDf.registerTempTable('Predictions')
    predictionsDf.columns
    ```

    <span data-ttu-id="282d6-202">You should see an output like the following:</span><span class="sxs-lookup"><span data-stu-id="282d6-202">You should see an output like the following:</span></span>

    ```
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
    ```

1. <span data-ttu-id="282d6-203">Look at one of the predictions.</span><span class="sxs-lookup"><span data-stu-id="282d6-203">Look at one of the predictions.</span></span> <span data-ttu-id="282d6-204">Run this snippet:</span><span class="sxs-lookup"><span data-stu-id="282d6-204">Run this snippet:</span></span>

    ```PySpark
    predictionsDf.take(1)
    ```

   <span data-ttu-id="282d6-205">There is a prediction for the first entry in the test data set.</span><span class="sxs-lookup"><span data-stu-id="282d6-205">There is a prediction for the first entry in the test data set.</span></span>
1. <span data-ttu-id="282d6-206">The `model.transform()` method applies the same transformation to any new data with the same schema, and arrive at a prediction of how to classify the data.</span><span class="sxs-lookup"><span data-stu-id="282d6-206">The `model.transform()` method applies the same transformation to any new data with the same schema, and arrive at a prediction of how to classify the data.</span></span> <span data-ttu-id="282d6-207">You can do some simple statistics to get a sense of how accurate the predictions were:</span><span class="sxs-lookup"><span data-stu-id="282d6-207">You can do some simple statistics to get a sense of how accurate the predictions were:</span></span>

    ```PySpark
    numSuccesses = predictionsDf.where("""(prediction = 0 AND results = 'Fail') OR
                                            (prediction = 1 AND (results = 'Pass' OR
                                                                results = 'Pass w/ Conditions'))""").count()
    numInspections = predictionsDf.count()

    print "There were", numInspections, "inspections and there were", numSuccesses, "successful predictions"
    print "This is a", str((float(numSuccesses) / float(numInspections)) * 100) + "%", "success rate"
    ```

    <span data-ttu-id="282d6-208">The output looks like the following:</span><span class="sxs-lookup"><span data-stu-id="282d6-208">The output looks like the following:</span></span>

    ```
    # -----------------
    # THIS IS AN OUTPUT
    # -----------------

    There were 9315 inspections and there were 8087 successful predictions
    This is a 86.8169618894% success rate
    ```

    <span data-ttu-id="282d6-209">Using logistic regression with Spark gives you an accurate model of the relationship between violations descriptions in English and whether a given business would pass or fail a food inspection.</span><span class="sxs-lookup"><span data-stu-id="282d6-209">Using logistic regression with Spark gives you an accurate model of the relationship between violations descriptions in English and whether a given business would pass or fail a food inspection.</span></span>

## <a name="create-a-visual-representation-of-the-prediction"></a><span data-ttu-id="282d6-210">Create a visual representation of the prediction</span><span class="sxs-lookup"><span data-stu-id="282d6-210">Create a visual representation of the prediction</span></span>
<span data-ttu-id="282d6-211">You can now construct a final visualization to help you reason about the results of this test.</span><span class="sxs-lookup"><span data-stu-id="282d6-211">You can now construct a final visualization to help you reason about the results of this test.</span></span>

1. <span data-ttu-id="282d6-212">You start by extracting the different predictions and results from the **Predictions** temporary table created earlier.</span><span class="sxs-lookup"><span data-stu-id="282d6-212">You start by extracting the different predictions and results from the **Predictions** temporary table created earlier.</span></span> <span data-ttu-id="282d6-213">The following queries separate the output as *true_positive*, *false_positive*, *true_negative*, and *false_negative*.</span><span class="sxs-lookup"><span data-stu-id="282d6-213">The following queries separate the output as *true_positive*, *false_positive*, *true_negative*, and *false_negative*.</span></span> <span data-ttu-id="282d6-214">In the queries below, you turn off visualization by using `-q` and also save the output (by using `-o`) as dataframes that can be then used with the `%%local` magic.</span><span class="sxs-lookup"><span data-stu-id="282d6-214">In the queries below, you turn off visualization by using `-q` and also save the output (by using `-o`) as dataframes that can be then used with the `%%local` magic.</span></span>

    ```PySpark
    %%sql -q -o true_positive
    SELECT count(*) AS cnt FROM Predictions WHERE prediction = 0 AND results = 'Fail'
    ```

    ```PySpark
    %%sql -q -o false_positive
    SELECT count(*) AS cnt FROM Predictions WHERE prediction = 0 AND (results = 'Pass' OR results = 'Pass w/ Conditions')
    ```

    ```PySpark
    %%sql -q -o true_negative
    SELECT count(*) AS cnt FROM Predictions WHERE prediction = 1 AND results = 'Fail'
    ```

    ```PySpark
    %%sql -q -o false_negative
    SELECT count(*) AS cnt FROM Predictions WHERE prediction = 1 AND (results = 'Pass' OR results = 'Pass w/ Conditions')
    ```

1. <span data-ttu-id="282d6-215">Finally, use the following snippet to generate the plot using **Matplotlib**.</span><span class="sxs-lookup"><span data-stu-id="282d6-215">Finally, use the following snippet to generate the plot using **Matplotlib**.</span></span>

    ```PySpark
    %%local
    %matplotlib inline
    import matplotlib.pyplot as plt

    labels = ['True positive', 'False positive', 'True negative', 'False negative']
    sizes = [true_positive['cnt'], false_positive['cnt'], false_negative['cnt'], true_negative['cnt']]
    colors = ['turquoise', 'seagreen', 'mediumslateblue', 'palegreen', 'coral']
    plt.pie(sizes, labels=labels, autopct='%1.1f%%', colors=colors)
    plt.axis('equal')
    ```

    <span data-ttu-id="282d6-216">You should see the following output:</span><span class="sxs-lookup"><span data-stu-id="282d6-216">You should see the following output:</span></span>

    <span data-ttu-id="282d6-217">![Spark machine learning application output - pie chart percentages of failed food inspections.](./media/apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-2.png "Spark machine learning result output")</span><span class="sxs-lookup"><span data-stu-id="282d6-217">![Spark machine learning application output - pie chart percentages of failed food inspections.](./media/apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-2.png "Spark machine learning result output")</span></span>

    <span data-ttu-id="282d6-218">In this chart, a "positive" result refers to the failed food inspection, while a negative result refers to a passed inspection.</span><span class="sxs-lookup"><span data-stu-id="282d6-218">In this chart, a "positive" result refers to the failed food inspection, while a negative result refers to a passed inspection.</span></span>

## <a name="shut-down-the-notebook"></a><span data-ttu-id="282d6-219">Shut down the notebook</span><span class="sxs-lookup"><span data-stu-id="282d6-219">Shut down the notebook</span></span>
<span data-ttu-id="282d6-220">After you have finished running the application, you should shut down the notebook to release the resources.</span><span class="sxs-lookup"><span data-stu-id="282d6-220">After you have finished running the application, you should shut down the notebook to release the resources.</span></span> <span data-ttu-id="282d6-221">To do so, from the **File** menu on the notebook, click **Close and Halt**.</span><span class="sxs-lookup"><span data-stu-id="282d6-221">To do so, from the **File** menu on the notebook, click **Close and Halt**.</span></span> <span data-ttu-id="282d6-222">This shuts down and closes the notebook.</span><span class="sxs-lookup"><span data-stu-id="282d6-222">This shuts down and closes the notebook.</span></span>

## <a name="seealso"></a><span data-ttu-id="282d6-223">See also</span><span class="sxs-lookup"><span data-stu-id="282d6-223">See also</span></span>
* [<span data-ttu-id="282d6-224">Overview: Apache Spark on Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="282d6-224">Overview: Apache Spark on Azure HDInsight</span></span>](apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="282d6-225">Scenarios</span><span class="sxs-lookup"><span data-stu-id="282d6-225">Scenarios</span></span>
* [<span data-ttu-id="282d6-226">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span><span class="sxs-lookup"><span data-stu-id="282d6-226">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](apache-spark-use-bi-tools.md)
* [<span data-ttu-id="282d6-227">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span><span class="sxs-lookup"><span data-stu-id="282d6-227">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="282d6-228">Website log analysis using Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="282d6-228">Website log analysis using Spark in HDInsight</span></span>](apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="282d6-229">Create and run applications</span><span class="sxs-lookup"><span data-stu-id="282d6-229">Create and run applications</span></span>
* [<span data-ttu-id="282d6-230">Create a standalone application using Scala</span><span class="sxs-lookup"><span data-stu-id="282d6-230">Create a standalone application using Scala</span></span>](apache-spark-create-standalone-application.md)
* [<span data-ttu-id="282d6-231">Run jobs remotely on a Spark cluster using Livy</span><span class="sxs-lookup"><span data-stu-id="282d6-231">Run jobs remotely on a Spark cluster using Livy</span></span>](apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="282d6-232">Tools and extensions</span><span class="sxs-lookup"><span data-stu-id="282d6-232">Tools and extensions</span></span>
* [<span data-ttu-id="282d6-233">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applications</span><span class="sxs-lookup"><span data-stu-id="282d6-233">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applications</span></span>](apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="282d6-234">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span><span class="sxs-lookup"><span data-stu-id="282d6-234">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="282d6-235">Use Zeppelin notebooks with a Spark cluster on HDInsight</span><span class="sxs-lookup"><span data-stu-id="282d6-235">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="282d6-236">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span><span class="sxs-lookup"><span data-stu-id="282d6-236">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="282d6-237">Use external packages with Jupyter notebooks</span><span class="sxs-lookup"><span data-stu-id="282d6-237">Use external packages with Jupyter notebooks</span></span>](apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="282d6-238">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span><span class="sxs-lookup"><span data-stu-id="282d6-238">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="282d6-239">Manage resources</span><span class="sxs-lookup"><span data-stu-id="282d6-239">Manage resources</span></span>
* [<span data-ttu-id="282d6-240">Manage resources for the Apache Spark cluster in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="282d6-240">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](apache-spark-resource-manager.md)
* [<span data-ttu-id="282d6-241">Track and debug jobs running on an Apache Spark cluster in HDInsight</span><span class="sxs-lookup"><span data-stu-id="282d6-241">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](apache-spark-job-debugging.md)
