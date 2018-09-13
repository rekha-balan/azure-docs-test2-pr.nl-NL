---
title: Use Apache Spark to build machine learning applications on Azure HDInsight | Microsoft Docs
description: Step-by-step instructions on how to use notebooks with Apache Spark to build machine learning applications
services: hdinsight
documentationcenter: ''
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: f584ca5e-abee-4b7c-ae58-2e45dfc56bf4
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: nitinme
ms.openlocfilehash: 33c93287c1689055c9fc7ba4c2fdd55273f7e6cd
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551658"
---
# <a name="build-machine-learning-applications-to-run-on-apache-spark-clusters-on-hdinsight"></a><span data-ttu-id="56cdc-103">Build Machine Learning applications to run on Apache Spark clusters on HDInsight</span><span class="sxs-lookup"><span data-stu-id="56cdc-103">Build Machine Learning applications to run on Apache Spark clusters on HDInsight</span></span>

<span data-ttu-id="56cdc-104">Learn how to build a machine learning application using an Apache Spark cluster in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="56cdc-104">Learn how to build a machine learning application using an Apache Spark cluster in HDInsight.</span></span> <span data-ttu-id="56cdc-105">This article shows how to use the Jupyter notebook available with the cluster to build and test our application.</span><span class="sxs-lookup"><span data-stu-id="56cdc-105">This article shows how to use the Jupyter notebook available with the cluster to build and test our application.</span></span> <span data-ttu-id="56cdc-106">The application uses the sample HVAC.csv data that is available on all clusters by default.</span><span class="sxs-lookup"><span data-stu-id="56cdc-106">The application uses the sample HVAC.csv data that is available on all clusters by default.</span></span>

<span data-ttu-id="56cdc-107">**Prerequisites:**</span><span class="sxs-lookup"><span data-stu-id="56cdc-107">**Prerequisites:**</span></span>

<span data-ttu-id="56cdc-108">You must have the following:</span><span class="sxs-lookup"><span data-stu-id="56cdc-108">You must have the following:</span></span>

* <span data-ttu-id="56cdc-109">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="56cdc-109">An Azure subscription.</span></span> <span data-ttu-id="56cdc-110">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="56cdc-110">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="56cdc-111">An Apache Spark cluster on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="56cdc-111">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="56cdc-112">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="56cdc-112">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span> 

## <a name="data"></a><span data-ttu-id="56cdc-113">Show me the data</span><span class="sxs-lookup"><span data-stu-id="56cdc-113">Show me the data</span></span>
<span data-ttu-id="56cdc-114">Before we start building the application, let us understand the structure of the data and the kind of analysis we will do on the data.</span><span class="sxs-lookup"><span data-stu-id="56cdc-114">Before we start building the application, let us understand the structure of the data and the kind of analysis we will do on the data.</span></span> 

<span data-ttu-id="56cdc-115">In this article, we use the sample **HVAC.csv** data file that is available in the Azure Storage account that you associated with the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="56cdc-115">In this article, we use the sample **HVAC.csv** data file that is available in the Azure Storage account that you associated with the HDInsight cluster.</span></span> <span data-ttu-id="56cdc-116">Within the storage account, the file is at **\HdiSamples\HdiSamples\SensorSampleData\hvac**.</span><span class="sxs-lookup"><span data-stu-id="56cdc-116">Within the storage account, the file is at **\HdiSamples\HdiSamples\SensorSampleData\hvac**.</span></span> <span data-ttu-id="56cdc-117">Download and open the CSV file to get a snapshot of the data.</span><span class="sxs-lookup"><span data-stu-id="56cdc-117">Download and open the CSV file to get a snapshot of the data.</span></span>  

<span data-ttu-id="56cdc-118">![HVAC data snapshot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-ipython-notebook-machine-learning/hdispark.ml.show.data.png "Snapshot of the HVAC data")</span><span class="sxs-lookup"><span data-stu-id="56cdc-118">![HVAC data snapshot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-ipython-notebook-machine-learning/hdispark.ml.show.data.png "Snapshot of the HVAC data")</span></span>

<span data-ttu-id="56cdc-119">The data shows the target temperature and the actual temperature of a building that has HVAC systems installed.</span><span class="sxs-lookup"><span data-stu-id="56cdc-119">The data shows the target temperature and the actual temperature of a building that has HVAC systems installed.</span></span> <span data-ttu-id="56cdc-120">Let's assume the **System** column represents the system ID and the **SystemAge** column represents the number of years the HVAC system has been in place at the building.</span><span class="sxs-lookup"><span data-stu-id="56cdc-120">Let's assume the **System** column represents the system ID and the **SystemAge** column represents the number of years the HVAC system has been in place at the building.</span></span>

<span data-ttu-id="56cdc-121">We use this data to predict whether a building will be hotter or colder based on the target temperature, given a system ID and system age.</span><span class="sxs-lookup"><span data-stu-id="56cdc-121">We use this data to predict whether a building will be hotter or colder based on the target temperature, given a system ID and system age.</span></span>

## <a name="app"></a><span data-ttu-id="56cdc-122">Write a machine learning application using Spark MLlib</span><span class="sxs-lookup"><span data-stu-id="56cdc-122">Write a machine learning application using Spark MLlib</span></span>
<span data-ttu-id="56cdc-123">In this application we use a Spark ML pipeline to perform a document classification.</span><span class="sxs-lookup"><span data-stu-id="56cdc-123">In this application we use a Spark ML pipeline to perform a document classification.</span></span> <span data-ttu-id="56cdc-124">In the pipeline, we split the document into words, convert the words into a numerical feature vector, and finally build a prediction model using the feature vectors and labels.</span><span class="sxs-lookup"><span data-stu-id="56cdc-124">In the pipeline, we split the document into words, convert the words into a numerical feature vector, and finally build a prediction model using the feature vectors and labels.</span></span> <span data-ttu-id="56cdc-125">Perform the following steps to create the application.</span><span class="sxs-lookup"><span data-stu-id="56cdc-125">Perform the following steps to create the application.</span></span>

1. <span data-ttu-id="56cdc-126">From the [Azure Portal](https://portal.azure.com/), from the startboard, click the tile for your Spark cluster (if you pinned it to the startboard).</span><span class="sxs-lookup"><span data-stu-id="56cdc-126">From the [Azure Portal](https://portal.azure.com/), from the startboard, click the tile for your Spark cluster (if you pinned it to the startboard).</span></span> <span data-ttu-id="56cdc-127">You can also navigate to your cluster under **Browse All** > **HDInsight Clusters**.</span><span class="sxs-lookup"><span data-stu-id="56cdc-127">You can also navigate to your cluster under **Browse All** > **HDInsight Clusters**.</span></span>   
2. <span data-ttu-id="56cdc-128">From the Spark cluster blade, click **Cluster Dashboard**, and then click **Jupyter Notebook**.</span><span class="sxs-lookup"><span data-stu-id="56cdc-128">From the Spark cluster blade, click **Cluster Dashboard**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="56cdc-129">If prompted, enter the admin credentials for the cluster.</span><span class="sxs-lookup"><span data-stu-id="56cdc-129">If prompted, enter the admin credentials for the cluster.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="56cdc-130">You may also reach the Jupyter Notebook for your cluster by opening the following URL in your browser.</span><span class="sxs-lookup"><span data-stu-id="56cdc-130">You may also reach the Jupyter Notebook for your cluster by opening the following URL in your browser.</span></span> <span data-ttu-id="56cdc-131">Replace **CLUSTERNAME** with the name of your cluster:</span><span class="sxs-lookup"><span data-stu-id="56cdc-131">Replace **CLUSTERNAME** with the name of your cluster:</span></span>
   > 
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   > 
   > 
3. <span data-ttu-id="56cdc-132">Create a new notebook.</span><span class="sxs-lookup"><span data-stu-id="56cdc-132">Create a new notebook.</span></span> <span data-ttu-id="56cdc-133">Click **New**, and then click **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="56cdc-133">Click **New**, and then click **PySpark**.</span></span>
   
    <span data-ttu-id="56cdc-134">![Create a new Jupyter notebook](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-ipython-notebook-machine-learning/hdispark.note.jupyter.createnotebook.png "Create a new Jupyter notebook")</span><span class="sxs-lookup"><span data-stu-id="56cdc-134">![Create a new Jupyter notebook](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-ipython-notebook-machine-learning/hdispark.note.jupyter.createnotebook.png "Create a new Jupyter notebook")</span></span>
4. <span data-ttu-id="56cdc-135">A new notebook is created and opened with the name Untitled.pynb.</span><span class="sxs-lookup"><span data-stu-id="56cdc-135">A new notebook is created and opened with the name Untitled.pynb.</span></span> <span data-ttu-id="56cdc-136">Click the notebook name at the top, and enter a friendly name.</span><span class="sxs-lookup"><span data-stu-id="56cdc-136">Click the notebook name at the top, and enter a friendly name.</span></span>
   
    <span data-ttu-id="56cdc-137">![Provide a name for the notebook](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-ipython-notebook-machine-learning/hdispark.note.jupyter.notebook.name.png "Provide a name for the notebook")</span><span class="sxs-lookup"><span data-stu-id="56cdc-137">![Provide a name for the notebook](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-ipython-notebook-machine-learning/hdispark.note.jupyter.notebook.name.png "Provide a name for the notebook")</span></span>
5. <span data-ttu-id="56cdc-138">Because you created a notebook using the PySpark kernel, you do not need to create any contexts explicitly.</span><span class="sxs-lookup"><span data-stu-id="56cdc-138">Because you created a notebook using the PySpark kernel, you do not need to create any contexts explicitly.</span></span> <span data-ttu-id="56cdc-139">The Spark and Hive contexts will be automatically created for you when you run the first code cell.</span><span class="sxs-lookup"><span data-stu-id="56cdc-139">The Spark and Hive contexts will be automatically created for you when you run the first code cell.</span></span> <span data-ttu-id="56cdc-140">You can start by importing the types that are required for this scenario.</span><span class="sxs-lookup"><span data-stu-id="56cdc-140">You can start by importing the types that are required for this scenario.</span></span> <span data-ttu-id="56cdc-141">Paste the following snippet in an empty cell, and then press **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="56cdc-141">Paste the following snippet in an empty cell, and then press **SHIFT + ENTER**.</span></span> 
   
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
6. <span data-ttu-id="56cdc-142">You must now load the data (hvac.csv), parse it, and use it to train the model.</span><span class="sxs-lookup"><span data-stu-id="56cdc-142">You must now load the data (hvac.csv), parse it, and use it to train the model.</span></span> <span data-ttu-id="56cdc-143">For this, you define a function that checks whether the actual temperature of the building is greater than the target temperature.</span><span class="sxs-lookup"><span data-stu-id="56cdc-143">For this, you define a function that checks whether the actual temperature of the building is greater than the target temperature.</span></span> <span data-ttu-id="56cdc-144">If the actual temperature is greater, the building is hot, denoted by the value **1.0**.</span><span class="sxs-lookup"><span data-stu-id="56cdc-144">If the actual temperature is greater, the building is hot, denoted by the value **1.0**.</span></span> <span data-ttu-id="56cdc-145">If the actual temperature is lesser, the building is cold, denoted by the value **0.0**.</span><span class="sxs-lookup"><span data-stu-id="56cdc-145">If the actual temperature is lesser, the building is cold, denoted by the value **0.0**.</span></span> 
   
    <span data-ttu-id="56cdc-146">Paste the following snippet in an empty cell and press **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="56cdc-146">Paste the following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>

        # List the structure of data for better understanding. Because the data will be
        # loaded as an array, this structure makes it easy to understand what each element
        # in the array corresponds to

        # 0 Date
        # 1 Time
        # 2 TargetTemp
        # 3 ActualTemp
        # 4 System
        # 5 SystemAge
        # 6 BuildingID

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
        data = sc.textFile("wasbs:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

        documents = data.filter(lambda s: "Date" not in s).map(parseDocument)
        training = documents.toDF()


1. <span data-ttu-id="56cdc-147">Configure the Spark machine learning pipeline that consists of three stages: tokenizer, hashingTF, and lr.</span><span class="sxs-lookup"><span data-stu-id="56cdc-147">Configure the Spark machine learning pipeline that consists of three stages: tokenizer, hashingTF, and lr.</span></span> <span data-ttu-id="56cdc-148">For more information about what is a pipeline and how it works see <a href="http://spark.apache.org/docs/latest/ml-guide.html#how-it-works" target="_blank">Spark machine learning pipeline</a>.</span><span class="sxs-lookup"><span data-stu-id="56cdc-148">For more information about what is a pipeline and how it works see <a href="http://spark.apache.org/docs/latest/ml-guide.html#how-it-works" target="_blank">Spark machine learning pipeline</a>.</span></span>
   
    <span data-ttu-id="56cdc-149">Paste the following snippet in an empty cell and press **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="56cdc-149">Paste the following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
        tokenizer = Tokenizer(inputCol="SystemInfo", outputCol="words")
        hashingTF = HashingTF(inputCol=tokenizer.getOutputCol(), outputCol="features")
        lr = LogisticRegression(maxIter=10, regParam=0.01)
        pipeline = Pipeline(stages=[tokenizer, hashingTF, lr])
2. <span data-ttu-id="56cdc-150">Fit the pipeline to the training document.</span><span class="sxs-lookup"><span data-stu-id="56cdc-150">Fit the pipeline to the training document.</span></span> <span data-ttu-id="56cdc-151">Paste the following snippet in an empty cell and press **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="56cdc-151">Paste the following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
        model = pipeline.fit(training)
3. <span data-ttu-id="56cdc-152">Verify the training document to checkpoint your progress with the application.</span><span class="sxs-lookup"><span data-stu-id="56cdc-152">Verify the training document to checkpoint your progress with the application.</span></span> <span data-ttu-id="56cdc-153">Paste the following snippet in an empty cell and press **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="56cdc-153">Paste the following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
        training.show()
   
    <span data-ttu-id="56cdc-154">This should give the output similar to the following:</span><span class="sxs-lookup"><span data-stu-id="56cdc-154">This should give the output similar to the following:</span></span>
   
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

    <span data-ttu-id="56cdc-155">Go back and verify the output against the raw CSV file.</span><span class="sxs-lookup"><span data-stu-id="56cdc-155">Go back and verify the output against the raw CSV file.</span></span> <span data-ttu-id="56cdc-156">For example, the first row the CSV file has this data:</span><span class="sxs-lookup"><span data-stu-id="56cdc-156">For example, the first row the CSV file has this data:</span></span>

    <span data-ttu-id="56cdc-157">![HVAC data snapshot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-ipython-notebook-machine-learning/hdispark.ml.show.data.first.row.png "Snapshot of the HVAC data")</span><span class="sxs-lookup"><span data-stu-id="56cdc-157">![HVAC data snapshot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-ipython-notebook-machine-learning/hdispark.ml.show.data.first.row.png "Snapshot of the HVAC data")</span></span>

    <span data-ttu-id="56cdc-158">Notice how the actual temperature is less than the target temperature suggesting the building is cold.</span><span class="sxs-lookup"><span data-stu-id="56cdc-158">Notice how the actual temperature is less than the target temperature suggesting the building is cold.</span></span> <span data-ttu-id="56cdc-159">Hence in the training output, the value for **label** in the first row is **0.0**, which means the building is not hot.</span><span class="sxs-lookup"><span data-stu-id="56cdc-159">Hence in the training output, the value for **label** in the first row is **0.0**, which means the building is not hot.</span></span>

1. <span data-ttu-id="56cdc-160">Prepare a data set to run the trained model against.</span><span class="sxs-lookup"><span data-stu-id="56cdc-160">Prepare a data set to run the trained model against.</span></span> <span data-ttu-id="56cdc-161">To do so, we would pass on a system ID and system age (denoted as **SystemInfo** in the training output), and the model would predict whether the building with that system ID and system age would be hotter (denoted by 1.0) or cooler (denoted by 0.0).</span><span class="sxs-lookup"><span data-stu-id="56cdc-161">To do so, we would pass on a system ID and system age (denoted as **SystemInfo** in the training output), and the model would predict whether the building with that system ID and system age would be hotter (denoted by 1.0) or cooler (denoted by 0.0).</span></span>
   
   <span data-ttu-id="56cdc-162">Paste the following snippet in an empty cell and press **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="56cdc-162">Paste the following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
       # SystemInfo here is a combination of system ID followed by system age
       Document = Row("id", "SystemInfo")
       test = sc.parallelize([(1L, "20 25"),
                     (2L, "4 15"),
                     (3L, "16 9"),
                     (4L, "9 22"),
                     (5L, "17 10"),
                     (6L, "7 22")]) \
           .map(lambda x: Document(*x)).toDF() 
2. <span data-ttu-id="56cdc-163">Finally, make predictions on the test data.</span><span class="sxs-lookup"><span data-stu-id="56cdc-163">Finally, make predictions on the test data.</span></span> <span data-ttu-id="56cdc-164">Paste the following snippet in an empty cell and press **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="56cdc-164">Paste the following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
        # Make predictions on test documents and print columns of interest
        prediction = model.transform(test)
        selected = prediction.select("SystemInfo", "prediction", "probability")
        for row in selected.collect():
            print row
3. <span data-ttu-id="56cdc-165">You should see an output similar to the following:</span><span class="sxs-lookup"><span data-stu-id="56cdc-165">You should see an output similar to the following:</span></span>
   
       Row(SystemInfo=u'20 25', prediction=1.0, probability=DenseVector([0.4999, 0.5001]))
       Row(SystemInfo=u'4 15', prediction=0.0, probability=DenseVector([0.5016, 0.4984]))
       Row(SystemInfo=u'16 9', prediction=1.0, probability=DenseVector([0.4785, 0.5215]))
       Row(SystemInfo=u'9 22', prediction=1.0, probability=DenseVector([0.4549, 0.5451]))
       Row(SystemInfo=u'17 10', prediction=1.0, probability=DenseVector([0.4925, 0.5075]))
       Row(SystemInfo=u'7 22', prediction=0.0, probability=DenseVector([0.5015, 0.4985]))
   
   <span data-ttu-id="56cdc-166">From the first row in the prediction, you can see that for an HVAC system with ID 20 and system age of 25 years, the building will be hot (**prediction=1.0**).</span><span class="sxs-lookup"><span data-stu-id="56cdc-166">From the first row in the prediction, you can see that for an HVAC system with ID 20 and system age of 25 years, the building will be hot (**prediction=1.0**).</span></span> <span data-ttu-id="56cdc-167">The first value for DenseVector (0.49999) corresponds to the  prediction 0.0 and the second value (0.5001) corresponds to the prediction 1.0.</span><span class="sxs-lookup"><span data-stu-id="56cdc-167">The first value for DenseVector (0.49999) corresponds to the  prediction 0.0 and the second value (0.5001) corresponds to the prediction 1.0.</span></span> <span data-ttu-id="56cdc-168">In the output, even though the second value is only marginally higher, the model shows **prediction=1.0**.</span><span class="sxs-lookup"><span data-stu-id="56cdc-168">In the output, even though the second value is only marginally higher, the model shows **prediction=1.0**.</span></span>
4. <span data-ttu-id="56cdc-169">After you have finished running the application, you should shutdown the notebook to release the resources.</span><span class="sxs-lookup"><span data-stu-id="56cdc-169">After you have finished running the application, you should shutdown the notebook to release the resources.</span></span> <span data-ttu-id="56cdc-170">To do so, from the **File** menu on the notebook, click **Close and Halt**.</span><span class="sxs-lookup"><span data-stu-id="56cdc-170">To do so, from the **File** menu on the notebook, click **Close and Halt**.</span></span> <span data-ttu-id="56cdc-171">This will shutdown and close the notebook.</span><span class="sxs-lookup"><span data-stu-id="56cdc-171">This will shutdown and close the notebook.</span></span>

## <a name="anaconda"></a><span data-ttu-id="56cdc-172">Use Anaconda scikit-learn library for Machine Learning</span><span class="sxs-lookup"><span data-stu-id="56cdc-172">Use Anaconda scikit-learn library for Machine Learning</span></span>
<span data-ttu-id="56cdc-173">Apache Spark clusters on HDInsight include Anaconda libraries.</span><span class="sxs-lookup"><span data-stu-id="56cdc-173">Apache Spark clusters on HDInsight include Anaconda libraries.</span></span> <span data-ttu-id="56cdc-174">This also includes the **scikit-learn** library for machine learning.</span><span class="sxs-lookup"><span data-stu-id="56cdc-174">This also includes the **scikit-learn** library for machine learning.</span></span> <span data-ttu-id="56cdc-175">The library also includes various data sets that you can use to build sample applications directly from a Jupyter notebook.</span><span class="sxs-lookup"><span data-stu-id="56cdc-175">The library also includes various data sets that you can use to build sample applications directly from a Jupyter notebook.</span></span> <span data-ttu-id="56cdc-176">For examples on using the scikit-learn library, see [http://scikit-learn.org/stable/auto_examples/index.html](http://scikit-learn.org/stable/auto_examples/index.html).</span><span class="sxs-lookup"><span data-stu-id="56cdc-176">For examples on using the scikit-learn library, see [http://scikit-learn.org/stable/auto_examples/index.html](http://scikit-learn.org/stable/auto_examples/index.html).</span></span>

## <a name="seealso"></a><span data-ttu-id="56cdc-177">See also</span><span class="sxs-lookup"><span data-stu-id="56cdc-177">See also</span></span>
* [<span data-ttu-id="56cdc-178">Overview: Apache Spark on Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="56cdc-178">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="56cdc-179">Scenarios</span><span class="sxs-lookup"><span data-stu-id="56cdc-179">Scenarios</span></span>
* [<span data-ttu-id="56cdc-180">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span><span class="sxs-lookup"><span data-stu-id="56cdc-180">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="56cdc-181">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span><span class="sxs-lookup"><span data-stu-id="56cdc-181">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="56cdc-182">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span><span class="sxs-lookup"><span data-stu-id="56cdc-182">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="56cdc-183">Website log analysis using Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="56cdc-183">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="56cdc-184">Create and run applications</span><span class="sxs-lookup"><span data-stu-id="56cdc-184">Create and run applications</span></span>
* [<span data-ttu-id="56cdc-185">Create a standalone application using Scala</span><span class="sxs-lookup"><span data-stu-id="56cdc-185">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="56cdc-186">Run jobs remotely on a Spark cluster using Livy</span><span class="sxs-lookup"><span data-stu-id="56cdc-186">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="56cdc-187">Tools and extensions</span><span class="sxs-lookup"><span data-stu-id="56cdc-187">Tools and extensions</span></span>
* [<span data-ttu-id="56cdc-188">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applicatons</span><span class="sxs-lookup"><span data-stu-id="56cdc-188">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="56cdc-189">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span><span class="sxs-lookup"><span data-stu-id="56cdc-189">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="56cdc-190">Use Zeppelin notebooks with a Spark cluster on HDInsight</span><span class="sxs-lookup"><span data-stu-id="56cdc-190">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-use-zeppelin-notebook.md)
* [<span data-ttu-id="56cdc-191">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span><span class="sxs-lookup"><span data-stu-id="56cdc-191">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="56cdc-192">Use external packages with Jupyter notebooks</span><span class="sxs-lookup"><span data-stu-id="56cdc-192">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="56cdc-193">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span><span class="sxs-lookup"><span data-stu-id="56cdc-193">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="56cdc-194">Manage resources</span><span class="sxs-lookup"><span data-stu-id="56cdc-194">Manage resources</span></span>
* [<span data-ttu-id="56cdc-195">Manage resources for the Apache Spark cluster in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="56cdc-195">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="56cdc-196">Track and debug jobs running on an Apache Spark cluster in HDInsight</span><span class="sxs-lookup"><span data-stu-id="56cdc-196">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-weblogs-sample]: hdinsight-hive-analyze-website-log.md
[hdinsight-sensor-data-sample]: hdinsight-hive-analyze-sensor-data.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-management-portal]: https://manage.windowsazure.com/
[azure-create-storageaccount]: storage-create-storage-account.md




