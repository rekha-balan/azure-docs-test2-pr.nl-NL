---
title: 'Tutorial: Build a Spark machine learning application in Azure HDInsight'
description: Step-by-step instructions on how to build Apache Spark machine learning application in HDInsight Spark clusters using Jupyter notebook.
services: hdinsight
ms.service: hdinsight
author: jasonwhowell
ms.reviewer: jasonh
ms.custom: hdinsightactive,mvc
ms.topic: tutorial
ms.date: 05/07/2018
ms.author: jasonh
ms.openlocfilehash: 4da8b0ddd8f8197d9aa8a79e5b63ac8fd90b4172
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856722"
---
# <a name="tutorial-build-a-spark-machine-learning-application-in-hdinsight"></a><span data-ttu-id="fdcd9-103">Tutorial: Build a Spark machine learning application in HDInsight</span><span class="sxs-lookup"><span data-stu-id="fdcd9-103">Tutorial: Build a Spark machine learning application in HDInsight</span></span> 

<span data-ttu-id="fdcd9-104">In this tutorial, you learn how to use the Jupyter notebook to build an Apache Spark machine learning application for Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fdcd9-104">In this tutorial, you learn how to use the Jupyter notebook to build an Apache Spark machine learning application for Azure HDInsight.</span></span> 

<span data-ttu-id="fdcd9-105">[MLlib](https://spark.apache.org/docs/1.1.0/mllib-guide.html) is Spark’s scalable machine learning library consisting of common learning algorithms and utilities, including classification, regression, clustering, collaborative filtering, dimensionality reduction, as well as underlying optimization primitives.</span><span class="sxs-lookup"><span data-stu-id="fdcd9-105">[MLlib](https://spark.apache.org/docs/1.1.0/mllib-guide.html) is Spark’s scalable machine learning library consisting of common learning algorithms and utilities, including classification, regression, clustering, collaborative filtering, dimensionality reduction, as well as underlying optimization primitives.</span></span>

<span data-ttu-id="fdcd9-106">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="fdcd9-106">In this tutorial, you learn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="fdcd9-107">Develop a Spark machine learning application</span><span class="sxs-lookup"><span data-stu-id="fdcd9-107">Develop a Spark machine learning application</span></span>

<span data-ttu-id="fdcd9-108">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span><span class="sxs-lookup"><span data-stu-id="fdcd9-108">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fdcd9-109">Prerequisites:</span><span class="sxs-lookup"><span data-stu-id="fdcd9-109">Prerequisites:</span></span>

<span data-ttu-id="fdcd9-110">You must have the following item:</span><span class="sxs-lookup"><span data-stu-id="fdcd9-110">You must have the following item:</span></span>

* <span data-ttu-id="fdcd9-111">Complete [Create an Apache Spark cluster in Azure HDInsight](apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="fdcd9-111">Complete [Create an Apache Spark cluster in Azure HDInsight](apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="understand-the-data-set"></a><span data-ttu-id="fdcd9-112">Understand the data set</span><span class="sxs-lookup"><span data-stu-id="fdcd9-112">Understand the data set</span></span>

<span data-ttu-id="fdcd9-113">The application uses the sample HVAC.csv data that is available on all clusters by default.</span><span class="sxs-lookup"><span data-stu-id="fdcd9-113">The application uses the sample HVAC.csv data that is available on all clusters by default.</span></span> <span data-ttu-id="fdcd9-114">The file is located at **\HdiSamples\HdiSamples\SensorSampleData\hvac**.</span><span class="sxs-lookup"><span data-stu-id="fdcd9-114">The file is located at **\HdiSamples\HdiSamples\SensorSampleData\hvac**.</span></span> <span data-ttu-id="fdcd9-115">The data shows the target temperature and the actual temperature of some buildings that have HVAC systems installed.</span><span class="sxs-lookup"><span data-stu-id="fdcd9-115">The data shows the target temperature and the actual temperature of some buildings that have HVAC systems installed.</span></span> <span data-ttu-id="fdcd9-116">The **System** column represents the system ID and the **SystemAge** column represents the number of years the HVAC system has been in place at the building.</span><span class="sxs-lookup"><span data-stu-id="fdcd9-116">The **System** column represents the system ID and the **SystemAge** column represents the number of years the HVAC system has been in place at the building.</span></span> <span data-ttu-id="fdcd9-117">Using the data, you can predict whether a building will be hotter or colder based on the target temperature, given a system ID, and system age.</span><span class="sxs-lookup"><span data-stu-id="fdcd9-117">Using the data, you can predict whether a building will be hotter or colder based on the target temperature, given a system ID, and system age.</span></span>

<span data-ttu-id="fdcd9-118">![Snapshot of data used for Spark machine learning example](./media/apache-spark-ipython-notebook-machine-learning/spark-machine-learning-understand-data.png "Snapshot of data used for Spark machine learning example")</span><span class="sxs-lookup"><span data-stu-id="fdcd9-118">![Snapshot of data used for Spark machine learning example](./media/apache-spark-ipython-notebook-machine-learning/spark-machine-learning-understand-data.png "Snapshot of data used for Spark machine learning example")</span></span>

## <a name="develop-a-spark-machine-learning-application-using-spark-mllib"></a><span data-ttu-id="fdcd9-119">Develop a Spark machine learning application using Spark MLlib</span><span class="sxs-lookup"><span data-stu-id="fdcd9-119">Develop a Spark machine learning application using Spark MLlib</span></span>

<span data-ttu-id="fdcd9-120">In this application, you use a Spark [ML pipeline](https://spark.apache.org/docs/2.2.0/ml-pipeline.html) to perform a document classification.</span><span class="sxs-lookup"><span data-stu-id="fdcd9-120">In this application, you use a Spark [ML pipeline](https://spark.apache.org/docs/2.2.0/ml-pipeline.html) to perform a document classification.</span></span> <span data-ttu-id="fdcd9-121">ML Pipelines provide a uniform set of high-level APIs built on top of DataFrames that help users create and tune practical machine learning pipelines.</span><span class="sxs-lookup"><span data-stu-id="fdcd9-121">ML Pipelines provide a uniform set of high-level APIs built on top of DataFrames that help users create and tune practical machine learning pipelines.</span></span> <span data-ttu-id="fdcd9-122">In the pipeline, you split the document into words, convert the words into a numerical feature vector, and finally build a prediction model using the feature vectors and labels.</span><span class="sxs-lookup"><span data-stu-id="fdcd9-122">In the pipeline, you split the document into words, convert the words into a numerical feature vector, and finally build a prediction model using the feature vectors and labels.</span></span> <span data-ttu-id="fdcd9-123">Perform the following steps to create the application.</span><span class="sxs-lookup"><span data-stu-id="fdcd9-123">Perform the following steps to create the application.</span></span>

1. <span data-ttu-id="fdcd9-124">Create a Jupyter notebook using the PySpark kernel.</span><span class="sxs-lookup"><span data-stu-id="fdcd9-124">Create a Jupyter notebook using the PySpark kernel.</span></span> <span data-ttu-id="fdcd9-125">For the instructions, see [Create a Jupyter notebook](./apache-spark-jupyter-spark-sql.md#create-a-jupyter-notebook).</span><span class="sxs-lookup"><span data-stu-id="fdcd9-125">For the instructions, see [Create a Jupyter notebook](./apache-spark-jupyter-spark-sql.md#create-a-jupyter-notebook).</span></span>
2. <span data-ttu-id="fdcd9-126">Import the types required for this scenario.</span><span class="sxs-lookup"><span data-stu-id="fdcd9-126">Import the types required for this scenario.</span></span> <span data-ttu-id="fdcd9-127">Paste the following snippet in an empty cell, and then press **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="fdcd9-127">Paste the following snippet in an empty cell, and then press **SHIFT + ENTER**.</span></span> 

    ```PySpark
    from pyspark.ml import Pipeline
    from pyspark.ml.classification import LogisticRegression
    from pyspark.ml.feature import HashingTF, Tokenizer
    from pyspark.sql import Row

    import os
    import sys
    from pyspark.sql.types import *

    from pyspark.mllib.classification import LogisticRegressionWithSGD
    from pyspark.mllib.regression import LabeledPoint
    from numpy import array
    ```
3. <span data-ttu-id="fdcd9-128">Load the data (hvac.csv), parse it, and use it to train the model.</span><span class="sxs-lookup"><span data-stu-id="fdcd9-128">Load the data (hvac.csv), parse it, and use it to train the model.</span></span> 

    ```PySpark
    # Define a type called LabelDocument
    LabeledDocument = Row("BuildingID", "SystemInfo", "label")

    # Define a function that parses the raw CSV file and returns an object of type LabeledDocument
    def parseDocument(line):
        values = [str(x) for x in line.split(',')]
        if (values[3] > values[2]):
            hot = 1.0
        else:
            hot = 0.0        

        textValue = str(values[4]) + " " + str(values[5])

        return LabeledDocument((values[6]), textValue, hot)

    # Load the raw HVAC.csv file, parse it using the function
    data = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

    documents = data.filter(lambda s: "Date" not in s).map(parseDocument)
    training = documents.toDF()
    ```

    <span data-ttu-id="fdcd9-129">In the code snippet, you define a function that compares the actual temperature with the target temperature.</span><span class="sxs-lookup"><span data-stu-id="fdcd9-129">In the code snippet, you define a function that compares the actual temperature with the target temperature.</span></span> <span data-ttu-id="fdcd9-130">If the actual temperature is greater, the building is hot, denoted by the value **1.0**.</span><span class="sxs-lookup"><span data-stu-id="fdcd9-130">If the actual temperature is greater, the building is hot, denoted by the value **1.0**.</span></span> <span data-ttu-id="fdcd9-131">Otherwise the building is cold, denoted by the value **0.0**.</span><span class="sxs-lookup"><span data-stu-id="fdcd9-131">Otherwise the building is cold, denoted by the value **0.0**.</span></span> 

4. <span data-ttu-id="fdcd9-132">Configure the Spark machine learning pipeline that consists of three stages: tokenizer, hashingTF, and lr.</span><span class="sxs-lookup"><span data-stu-id="fdcd9-132">Configure the Spark machine learning pipeline that consists of three stages: tokenizer, hashingTF, and lr.</span></span> 

    ```PySpark
    tokenizer = Tokenizer(inputCol="SystemInfo", outputCol="words")
    hashingTF = HashingTF(inputCol=tokenizer.getOutputCol(), outputCol="features")
    lr = LogisticRegression(maxIter=10, regParam=0.01)
    pipeline = Pipeline(stages=[tokenizer, hashingTF, lr])
    ```

    <span data-ttu-id="fdcd9-133">For more information about pipeline and how it works, see <a href="http://spark.apache.org/docs/latest/ml-guide.html#how-it-works" target="_blank">Spark machine learning pipeline</a>.</span><span class="sxs-lookup"><span data-stu-id="fdcd9-133">For more information about pipeline and how it works, see <a href="http://spark.apache.org/docs/latest/ml-guide.html#how-it-works" target="_blank">Spark machine learning pipeline</a>.</span></span>

5. <span data-ttu-id="fdcd9-134">Fit the pipeline to the training document.</span><span class="sxs-lookup"><span data-stu-id="fdcd9-134">Fit the pipeline to the training document.</span></span>
   
    ```PySpark
    model = pipeline.fit(training)
    ```

6. <span data-ttu-id="fdcd9-135">Verify the training document to checkpoint your progress with the application.</span><span class="sxs-lookup"><span data-stu-id="fdcd9-135">Verify the training document to checkpoint your progress with the application.</span></span>
   
    ```PySpark
    training.show()
    ```
   
    <span data-ttu-id="fdcd9-136">The output is similar to:</span><span class="sxs-lookup"><span data-stu-id="fdcd9-136">The output is similar to:</span></span>

    ```
    +----------+----------+-----+
    |BuildingID|SystemInfo|label|
    +----------+----------+-----+
    |         4|     13 20|  0.0|
    |        17|      3 20|  0.0|
    |        18|     17 20|  1.0|
    |        15|      2 23|  0.0|
    |         3|      16 9|  1.0|
    |         4|     13 28|  0.0|
    |         2|     12 24|  0.0|
    |        16|     20 26|  1.0|
    |         9|      16 9|  1.0|
    |        12|       6 5|  0.0|
    |        15|     10 17|  1.0|
    |         7|      2 11|  0.0|
    |        15|      14 2|  1.0|
    |         6|       3 2|  0.0|
    |        20|     19 22|  0.0|
    |         8|     19 11|  0.0|
    |         6|      15 7|  0.0|
    |        13|      12 5|  0.0|
    |         4|      8 22|  0.0|
    |         7|      17 5|  0.0|
    +----------+----------+-----+
    ```

    <span data-ttu-id="fdcd9-137">Comparing the output against the raw CSV file.</span><span class="sxs-lookup"><span data-stu-id="fdcd9-137">Comparing the output against the raw CSV file.</span></span> <span data-ttu-id="fdcd9-138">For example, the first row the CSV file has this data:</span><span class="sxs-lookup"><span data-stu-id="fdcd9-138">For example, the first row the CSV file has this data:</span></span>

    <span data-ttu-id="fdcd9-139">![Output data snapshot for Spark machine learning example](./media/apache-spark-ipython-notebook-machine-learning/spark-machine-learning-output-data.png "Output data snapshot for Spark machine learning example")</span><span class="sxs-lookup"><span data-stu-id="fdcd9-139">![Output data snapshot for Spark machine learning example](./media/apache-spark-ipython-notebook-machine-learning/spark-machine-learning-output-data.png "Output data snapshot for Spark machine learning example")</span></span>

    <span data-ttu-id="fdcd9-140">Notice how the actual temperature is less than the target temperature suggesting the building is cold.</span><span class="sxs-lookup"><span data-stu-id="fdcd9-140">Notice how the actual temperature is less than the target temperature suggesting the building is cold.</span></span> <span data-ttu-id="fdcd9-141">Hence in the training output, the value for **label** in the first row is **0.0**, which means the building is not hot.</span><span class="sxs-lookup"><span data-stu-id="fdcd9-141">Hence in the training output, the value for **label** in the first row is **0.0**, which means the building is not hot.</span></span>

7. <span data-ttu-id="fdcd9-142">Prepare a data set to run the trained model against.</span><span class="sxs-lookup"><span data-stu-id="fdcd9-142">Prepare a data set to run the trained model against.</span></span> <span data-ttu-id="fdcd9-143">To do so, you pass on a system ID and system age (denoted as **SystemInfo** in the training output), and the model predicts whether the building with that system ID and system age will be hotter (denoted by 1.0) or cooler (denoted by 0.0).</span><span class="sxs-lookup"><span data-stu-id="fdcd9-143">To do so, you pass on a system ID and system age (denoted as **SystemInfo** in the training output), and the model predicts whether the building with that system ID and system age will be hotter (denoted by 1.0) or cooler (denoted by 0.0).</span></span>
   
    ```PySpark   
    # SystemInfo here is a combination of system ID followed by system age
    Document = Row("id", "SystemInfo")
    test = sc.parallelize([(1L, "20 25"),
                    (2L, "4 15"),
                    (3L, "16 9"),
                    (4L, "9 22"),
                    (5L, "17 10"),
                    (6L, "7 22")]) \
        .map(lambda x: Document(*x)).toDF() 
    ```
8. <span data-ttu-id="fdcd9-144">Finally, make predictions on the test data.</span><span class="sxs-lookup"><span data-stu-id="fdcd9-144">Finally, make predictions on the test data.</span></span> 
   
    ```PySpark
    # Make predictions on test documents and print columns of interest
    prediction = model.transform(test)
    selected = prediction.select("SystemInfo", "prediction", "probability")
    for row in selected.collect():
        print row
    ```

    <span data-ttu-id="fdcd9-145">The output is similar to:</span><span class="sxs-lookup"><span data-stu-id="fdcd9-145">The output is similar to:</span></span>

    ```   
    Row(SystemInfo=u'20 25', prediction=1.0, probability=DenseVector([0.4999, 0.5001]))
    Row(SystemInfo=u'4 15', prediction=0.0, probability=DenseVector([0.5016, 0.4984]))
    Row(SystemInfo=u'16 9', prediction=1.0, probability=DenseVector([0.4785, 0.5215]))
    Row(SystemInfo=u'9 22', prediction=1.0, probability=DenseVector([0.4549, 0.5451]))
    Row(SystemInfo=u'17 10', prediction=1.0, probability=DenseVector([0.4925, 0.5075]))
    Row(SystemInfo=u'7 22', prediction=0.0, probability=DenseVector([0.5015, 0.4985]))
    ```
   
   <span data-ttu-id="fdcd9-146">From the first row in the prediction, you can see that for an HVAC system with ID 20 and system age of 25 years, the building is hot (**prediction=1.0**).</span><span class="sxs-lookup"><span data-stu-id="fdcd9-146">From the first row in the prediction, you can see that for an HVAC system with ID 20 and system age of 25 years, the building is hot (**prediction=1.0**).</span></span> <span data-ttu-id="fdcd9-147">The first value for DenseVector (0.49999) corresponds to the  prediction 0.0 and the second value (0.5001) corresponds to the prediction 1.0.</span><span class="sxs-lookup"><span data-stu-id="fdcd9-147">The first value for DenseVector (0.49999) corresponds to the  prediction 0.0 and the second value (0.5001) corresponds to the prediction 1.0.</span></span> <span data-ttu-id="fdcd9-148">In the output, even though the second value is only marginally higher, the model shows **prediction=1.0**.</span><span class="sxs-lookup"><span data-stu-id="fdcd9-148">In the output, even though the second value is only marginally higher, the model shows **prediction=1.0**.</span></span>
10. <span data-ttu-id="fdcd9-149">Shut down the notebook to release the resources.</span><span class="sxs-lookup"><span data-stu-id="fdcd9-149">Shut down the notebook to release the resources.</span></span> <span data-ttu-id="fdcd9-150">To do so, from the **File** menu on the notebook, select **Close and Halt**.</span><span class="sxs-lookup"><span data-stu-id="fdcd9-150">To do so, from the **File** menu on the notebook, select **Close and Halt**.</span></span> <span data-ttu-id="fdcd9-151">This action shuts down and closes the notebook.</span><span class="sxs-lookup"><span data-stu-id="fdcd9-151">This action shuts down and closes the notebook.</span></span>

## <a name="use-anaconda-scikit-learn-library-for-spark-machine-learning"></a><span data-ttu-id="fdcd9-152">Use Anaconda scikit-learn library for Spark machine learning</span><span class="sxs-lookup"><span data-stu-id="fdcd9-152">Use Anaconda scikit-learn library for Spark machine learning</span></span>
<span data-ttu-id="fdcd9-153">Apache Spark clusters in HDInsight include Anaconda libraries.</span><span class="sxs-lookup"><span data-stu-id="fdcd9-153">Apache Spark clusters in HDInsight include Anaconda libraries.</span></span> <span data-ttu-id="fdcd9-154">It also includes the **scikit-learn** library for machine learning.</span><span class="sxs-lookup"><span data-stu-id="fdcd9-154">It also includes the **scikit-learn** library for machine learning.</span></span> <span data-ttu-id="fdcd9-155">The library also includes various data sets that you can use to build sample applications directly from a Jupyter notebook.</span><span class="sxs-lookup"><span data-stu-id="fdcd9-155">The library also includes various data sets that you can use to build sample applications directly from a Jupyter notebook.</span></span> <span data-ttu-id="fdcd9-156">For examples on using the scikit-learn library, see [http://scikit-learn.org/stable/auto_examples/index.html](http://scikit-learn.org/stable/auto_examples/index.html).</span><span class="sxs-lookup"><span data-stu-id="fdcd9-156">For examples on using the scikit-learn library, see [http://scikit-learn.org/stable/auto_examples/index.html](http://scikit-learn.org/stable/auto_examples/index.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="fdcd9-157">Next steps</span><span class="sxs-lookup"><span data-stu-id="fdcd9-157">Next steps</span></span>

<span data-ttu-id="fdcd9-158">In this tutorial, you learned how to:</span><span class="sxs-lookup"><span data-stu-id="fdcd9-158">In this tutorial, you learned how to:</span></span>

* <span data-ttu-id="fdcd9-159">Develop a Spark machine learning application</span><span class="sxs-lookup"><span data-stu-id="fdcd9-159">Develop a Spark machine learning application</span></span>

<span data-ttu-id="fdcd9-160">Advance to the next tutorial to learn how to use IntelliJ IDEA for Spark jobs.</span><span class="sxs-lookup"><span data-stu-id="fdcd9-160">Advance to the next tutorial to learn how to use IntelliJ IDEA for Spark jobs.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="fdcd9-161">Create a Scala Maven appliction using IntelliJ</span><span class="sxs-lookup"><span data-stu-id="fdcd9-161">Create a Scala Maven appliction using IntelliJ</span></span>](./apache-spark-create-standalone-application.md)

