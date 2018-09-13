---
title: Advanced data exploration and modeling with Spark | Microsoft Docs
description: Use HDInsight Spark to do data exploration and train binary classification and regression models using cross-validation and hyperparameter optimization.
services: machine-learning
documentationcenter: ''
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: f90d9a80-4eaf-437b-a914-23514390cd60
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/15/2017
ms.author: deguhath;bradsev;gokuma
ms.openlocfilehash: dcba731509d0d30f1becf21e726a05029fc32154
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662598"
---
# <a name="advanced-data-exploration-and-modeling-with-spark"></a><span data-ttu-id="aeaf1-103">Advanced data exploration and modeling with Spark</span><span class="sxs-lookup"><span data-stu-id="aeaf1-103">Advanced data exploration and modeling with Spark</span></span>
[!INCLUDE [machine-learning-spark-modeling](../../includes/machine-learning-spark-modeling.md)]

<span data-ttu-id="aeaf1-104">This walkthrough uses HDInsight Spark to do data exploration and train binary classification and regression models using cross-validation and hyperparameter optimization on a sample of the NYC taxi trip and fare 2013 dataset.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-104">This walkthrough uses HDInsight Spark to do data exploration and train binary classification and regression models using cross-validation and hyperparameter optimization on a sample of the NYC taxi trip and fare 2013 dataset.</span></span> <span data-ttu-id="aeaf1-105">It walks you through the steps of the [Data Science Process](http://aka.ms/datascienceprocess), end-to-end, using an HDInsight Spark cluster for processing and Azure blobs to store the data and the models.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-105">It walks you through the steps of the [Data Science Process](http://aka.ms/datascienceprocess), end-to-end, using an HDInsight Spark cluster for processing and Azure blobs to store the data and the models.</span></span> <span data-ttu-id="aeaf1-106">The process explores and visualizes data brought in from an Azure Storage Blob and then prepares the data to build predictive models.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-106">The process explores and visualizes data brought in from an Azure Storage Blob and then prepares the data to build predictive models.</span></span> <span data-ttu-id="aeaf1-107">Python has been used to code the solution and to show the relevant plots.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-107">Python has been used to code the solution and to show the relevant plots.</span></span> <span data-ttu-id="aeaf1-108">These models are build using the Spark MLlib toolkit to do binary classification and regression modeling tasks.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-108">These models are build using the Spark MLlib toolkit to do binary classification and regression modeling tasks.</span></span> 

* <span data-ttu-id="aeaf1-109">The **binary classification** task is to predict whether or not a tip is paid for the trip.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-109">The **binary classification** task is to predict whether or not a tip is paid for the trip.</span></span> 
* <span data-ttu-id="aeaf1-110">The **regression** task is to predict the amount of the tip based on other tip features.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-110">The **regression** task is to predict the amount of the tip based on other tip features.</span></span> 

<span data-ttu-id="aeaf1-111">The modeling steps also contain code showing how to train, evaluate, and save each type of model.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-111">The modeling steps also contain code showing how to train, evaluate, and save each type of model.</span></span> <span data-ttu-id="aeaf1-112">The topic covers some of the same ground as the [Data exploration and modeling with Spark](machine-learning-data-science-spark-data-exploration-modeling.md) topic.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-112">The topic covers some of the same ground as the [Data exploration and modeling with Spark](machine-learning-data-science-spark-data-exploration-modeling.md) topic.</span></span> <span data-ttu-id="aeaf1-113">But it is more "advanced" in that it also uses cross-validation with hyperparameter sweeping to train optimally accurate classification and regression models.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-113">But it is more "advanced" in that it also uses cross-validation with hyperparameter sweeping to train optimally accurate classification and regression models.</span></span> 

<span data-ttu-id="aeaf1-114">**Cross-validation (CV)** is a technique that assesses how well a model trained on a known set of data generalizes to predicting the features of datasets on which it has not been trained.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-114">**Cross-validation (CV)** is a technique that assesses how well a model trained on a known set of data generalizes to predicting the features of datasets on which it has not been trained.</span></span>  <span data-ttu-id="aeaf1-115">A common implementation used here is to divide a dataset into K folds and then train the model in a round-robin fashion on all but one of the folds.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-115">A common implementation used here is to divide a dataset into K folds and then train the model in a round-robin fashion on all but one of the folds.</span></span> <span data-ttu-id="aeaf1-116">The ability of the model to prediction accurately when tested against the independent dataset in this fold not used to train the model is assessed.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-116">The ability of the model to prediction accurately when tested against the independent dataset in this fold not used to train the model is assessed.</span></span>

<span data-ttu-id="aeaf1-117">**Hyperparameter optimization** is the problem of choosing a set of hyperparameters for a learning algorithm, usually with the goal of optimizing a measure of the algorithm's performance on an independent data set.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-117">**Hyperparameter optimization** is the problem of choosing a set of hyperparameters for a learning algorithm, usually with the goal of optimizing a measure of the algorithm's performance on an independent data set.</span></span> <span data-ttu-id="aeaf1-118">**Hyperparameters** are values that must be specified outside of the model training procedure.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-118">**Hyperparameters** are values that must be specified outside of the model training procedure.</span></span> <span data-ttu-id="aeaf1-119">Assumptions about these values can impact the flexibility and accuracy of the models.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-119">Assumptions about these values can impact the flexibility and accuracy of the models.</span></span> <span data-ttu-id="aeaf1-120">Decision trees have hyperparameters, for example, such as the desired depth and number of leaves in the tree.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-120">Decision trees have hyperparameters, for example, such as the desired depth and number of leaves in the tree.</span></span> <span data-ttu-id="aeaf1-121">Support Vector Machines (SVMs) require setting a misclassification penalty term.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-121">Support Vector Machines (SVMs) require setting a misclassification penalty term.</span></span> 

<span data-ttu-id="aeaf1-122">A common way to perform hyperparameter optimization used here is a grid search, or a **parameter sweep**.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-122">A common way to perform hyperparameter optimization used here is a grid search, or a **parameter sweep**.</span></span> <span data-ttu-id="aeaf1-123">This consists of performing an exhaustive search through the values a specified subset of the hyperparameter space for a learning algorithm.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-123">This consists of performing an exhaustive search through the values a specified subset of the hyperparameter space for a learning algorithm.</span></span> <span data-ttu-id="aeaf1-124">Cross validation can supply a performance metric to sort out the optimal results produced by the grid search algorithm.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-124">Cross validation can supply a performance metric to sort out the optimal results produced by the grid search algorithm.</span></span> <span data-ttu-id="aeaf1-125">CV used with hyperparameter sweeping helps limit problems like overfitting a model to training data so that the model retains the capacity to apply to the general set of data from which the training data was extracted.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-125">CV used with hyperparameter sweeping helps limit problems like overfitting a model to training data so that the model retains the capacity to apply to the general set of data from which the training data was extracted.</span></span>

<span data-ttu-id="aeaf1-126">The models we use include logistic and linear regression, random forests, and gradient boosted trees:</span><span class="sxs-lookup"><span data-stu-id="aeaf1-126">The models we use include logistic and linear regression, random forests, and gradient boosted trees:</span></span>

* <span data-ttu-id="aeaf1-127">[Linear regression with SGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) is a linear regression model that uses a Stochastic Gradient Descent (SGD) method and for optimization and feature scaling to predict the tip amounts paid.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-127">[Linear regression with SGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) is a linear regression model that uses a Stochastic Gradient Descent (SGD) method and for optimization and feature scaling to predict the tip amounts paid.</span></span> 
* <span data-ttu-id="aeaf1-128">[Logistic regression with LBFGS](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.classification.LogisticRegressionWithLBFGS) or "logit" regression, is a regression model that can be used when the dependent variable is categorical to do data classification.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-128">[Logistic regression with LBFGS](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.classification.LogisticRegressionWithLBFGS) or "logit" regression, is a regression model that can be used when the dependent variable is categorical to do data classification.</span></span> <span data-ttu-id="aeaf1-129">LBFGS is a quasi-Newton optimization algorithm that approximates the Broyden–Fletcher–Goldfarb–Shanno (BFGS) algorithm using a limited amount of computer memory and that is widely used in machine learning.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-129">LBFGS is a quasi-Newton optimization algorithm that approximates the Broyden–Fletcher–Goldfarb–Shanno (BFGS) algorithm using a limited amount of computer memory and that is widely used in machine learning.</span></span>
* <span data-ttu-id="aeaf1-130">[Random forests](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) are ensembles of decision trees.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-130">[Random forests](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) are ensembles of decision trees.</span></span>  <span data-ttu-id="aeaf1-131">They combine many decision trees to reduce the risk of overfitting.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-131">They combine many decision trees to reduce the risk of overfitting.</span></span> <span data-ttu-id="aeaf1-132">Random forests are used for regression and classification and can handle categorical features and can be extended to the multiclass classification setting.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-132">Random forests are used for regression and classification and can handle categorical features and can be extended to the multiclass classification setting.</span></span> <span data-ttu-id="aeaf1-133">They do not require feature scaling and are able to capture non-linearities and feature interactions.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-133">They do not require feature scaling and are able to capture non-linearities and feature interactions.</span></span> <span data-ttu-id="aeaf1-134">Random forests are one of the most successful machine learning models for classification and regression.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-134">Random forests are one of the most successful machine learning models for classification and regression.</span></span>
* <span data-ttu-id="aeaf1-135">[Gradient boosted trees](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) are ensembles of decision trees.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-135">[Gradient boosted trees](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) are ensembles of decision trees.</span></span> <span data-ttu-id="aeaf1-136">GBTs train decision trees iteratively to minimize a loss function.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-136">GBTs train decision trees iteratively to minimize a loss function.</span></span> <span data-ttu-id="aeaf1-137">GBTs are used for regression and classification and can handle categorical features, do not require feature scaling, and are able to capture non-linearities and feature interactions.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-137">GBTs are used for regression and classification and can handle categorical features, do not require feature scaling, and are able to capture non-linearities and feature interactions.</span></span> <span data-ttu-id="aeaf1-138">They can also be used in a multiclass-classification setting.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-138">They can also be used in a multiclass-classification setting.</span></span>

<span data-ttu-id="aeaf1-139">Modeling examples using CV and Hyperparameter sweep are shown for the binary classification problem.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-139">Modeling examples using CV and Hyperparameter sweep are shown for the binary classification problem.</span></span> <span data-ttu-id="aeaf1-140">Simpler examples (without parameter sweeps) are presented in the main topic for regression tasks.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-140">Simpler examples (without parameter sweeps) are presented in the main topic for regression tasks.</span></span> <span data-ttu-id="aeaf1-141">But in the appendix, validation using elastic net for linear regression and CV with parameter sweep using for random forest regression are also presented.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-141">But in the appendix, validation using elastic net for linear regression and CV with parameter sweep using for random forest regression are also presented.</span></span> <span data-ttu-id="aeaf1-142">The **elastic net** is a regularized regression method for fitting linear regression models that linearly combines the L1 and L2 metrics as penalties of the [lasso](https://en.wikipedia.org/wiki/Lasso%20%28statistics%29) and [ridge](https://en.wikipedia.org/wiki/Tikhonov_regularization) methods.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-142">The **elastic net** is a regularized regression method for fitting linear regression models that linearly combines the L1 and L2 metrics as penalties of the [lasso](https://en.wikipedia.org/wiki/Lasso%20%28statistics%29) and [ridge](https://en.wikipedia.org/wiki/Tikhonov_regularization) methods.</span></span>   

> [!NOTE]
> <span data-ttu-id="aeaf1-143">Although the Spark MLlib toolkit is designed to work on large datasets, a relatively small sample (~30 Mb using 170K rows, about 0.1% of the original NYC dataset) is used here for convenience.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-143">Although the Spark MLlib toolkit is designed to work on large datasets, a relatively small sample (~30 Mb using 170K rows, about 0.1% of the original NYC dataset) is used here for convenience.</span></span> <span data-ttu-id="aeaf1-144">The exercise given here runs efficiently (in about 10 minutes) on an HDInsight cluster with 2 worker nodes.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-144">The exercise given here runs efficiently (in about 10 minutes) on an HDInsight cluster with 2 worker nodes.</span></span> <span data-ttu-id="aeaf1-145">The same code, with minor modifications, can be used to process larger data-sets, with appropriate modifications for caching data in memory and changing the cluster size.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-145">The same code, with minor modifications, can be used to process larger data-sets, with appropriate modifications for caching data in memory and changing the cluster size.</span></span>
> 
> 

## <a name="setup-spark-clusters-and-notebooks"></a><span data-ttu-id="aeaf1-146">Setup: Spark clusters and notebooks</span><span class="sxs-lookup"><span data-stu-id="aeaf1-146">Setup: Spark clusters and notebooks</span></span>
<span data-ttu-id="aeaf1-147">Setup steps and code are provided in this walkthrough for using an HDInsight Spark 1.6.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-147">Setup steps and code are provided in this walkthrough for using an HDInsight Spark 1.6.</span></span> <span data-ttu-id="aeaf1-148">But Jupyter notebooks are provided for both HDInsight Spark 1.6 and Spark 2.0 clusters.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-148">But Jupyter notebooks are provided for both HDInsight Spark 1.6 and Spark 2.0 clusters.</span></span> <span data-ttu-id="aeaf1-149">A description of the notebooks and links to them are provided in the [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) for the GitHub repository containing them.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-149">A description of the notebooks and links to them are provided in the [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) for the GitHub repository containing them.</span></span> <span data-ttu-id="aeaf1-150">Moreover, the code here and in the linked notebooks is generic and should work on any Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-150">Moreover, the code here and in the linked notebooks is generic and should work on any Spark cluster.</span></span> <span data-ttu-id="aeaf1-151">If you are not using HDInsight Spark, the cluster setup and management steps may be slightly different from what is shown here.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-151">If you are not using HDInsight Spark, the cluster setup and management steps may be slightly different from what is shown here.</span></span> <span data-ttu-id="aeaf1-152">For convenience, here are the links to the Jupyter notebooks for Spark 1.6 and 2.0 to be run in the pyspark kernel of the Jupyter Notebook server:</span><span class="sxs-lookup"><span data-stu-id="aeaf1-152">For convenience, here are the links to the Jupyter notebooks for Spark 1.6 and 2.0 to be run in the pyspark kernel of the Jupyter Notebook server:</span></span>

### <a name="spark-16-notebooks"></a><span data-ttu-id="aeaf1-153">Spark 1.6 notebooks</span><span class="sxs-lookup"><span data-stu-id="aeaf1-153">Spark 1.6 notebooks</span></span>

<span data-ttu-id="aeaf1-154">[pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): Includes topics in notebook #1, and model development using hyperparameter tuning and cross-validation.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-154">[pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): Includes topics in notebook #1, and model development using hyperparameter tuning and cross-validation.</span></span>

### <a name="spark-20-notebooks"></a><span data-ttu-id="aeaf1-155">Spark 2.0 notebooks</span><span class="sxs-lookup"><span data-stu-id="aeaf1-155">Spark 2.0 notebooks</span></span>

<span data-ttu-id="aeaf1-156">[Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): This file provides information on how to perform data exploration, modeling, and scoring in Spark 2.0 clusters.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-156">[Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): This file provides information on how to perform data exploration, modeling, and scoring in Spark 2.0 clusters.</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="setup-storage-locations-libraries-and-the-preset-spark-context"></a><span data-ttu-id="aeaf1-157">Setup: storage locations, libraries, and the preset Spark context</span><span class="sxs-lookup"><span data-stu-id="aeaf1-157">Setup: storage locations, libraries, and the preset Spark context</span></span>
<span data-ttu-id="aeaf1-158">Spark is able to read and write to Azure Storage Blob (also known as WASB).</span><span class="sxs-lookup"><span data-stu-id="aeaf1-158">Spark is able to read and write to Azure Storage Blob (also known as WASB).</span></span> <span data-ttu-id="aeaf1-159">So any of your existing data stored there can be processed using Spark and the results stored again in WASB.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-159">So any of your existing data stored there can be processed using Spark and the results stored again in WASB.</span></span>

<span data-ttu-id="aeaf1-160">To save models or files in WASB, the path needs to be specified properly.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-160">To save models or files in WASB, the path needs to be specified properly.</span></span> <span data-ttu-id="aeaf1-161">The default container attached to the Spark cluster can be referenced using a path beginning with: "wasb:///".</span><span class="sxs-lookup"><span data-stu-id="aeaf1-161">The default container attached to the Spark cluster can be referenced using a path beginning with: "wasb:///".</span></span> <span data-ttu-id="aeaf1-162">Other locations are referenced by “wasb://”.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-162">Other locations are referenced by “wasb://”.</span></span>

### <a name="set-directory-paths-for-storage-locations-in-wasb"></a><span data-ttu-id="aeaf1-163">Set directory paths for storage locations in WASB</span><span class="sxs-lookup"><span data-stu-id="aeaf1-163">Set directory paths for storage locations in WASB</span></span>
<span data-ttu-id="aeaf1-164">The following code sample specifies the location of the data to be read and the path for the model storage directory to which the model output is saved:</span><span class="sxs-lookup"><span data-stu-id="aeaf1-164">The following code sample specifies the location of the data to be read and the path for the model storage directory to which the model output is saved:</span></span>

    # SET PATHS TO FILE LOCATIONS: DATA AND MODEL STORAGE

    # LOCATION OF TRAINING DATA
    taxi_train_file_loc = "wasb://mllibwalkthroughs@cdspsparksamples.blob.core.windows.net/Data/NYCTaxi/JoinedTaxiTripFare.Point1Pct.Train.tsv";


    # SET THE MODEL STORAGE DIRECTORY PATH 
    # NOTE THAT THE FINAL BACKSLASH IN THE PATH IS NEEDED.
    modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/";

    # PRINT START TIME
    import datetime
    datetime.datetime.now()

<span data-ttu-id="aeaf1-165">**OUTPUT**</span><span class="sxs-lookup"><span data-stu-id="aeaf1-165">**OUTPUT**</span></span>

<span data-ttu-id="aeaf1-166">datetime.datetime(2016, 4, 18, 17, 36, 27, 832799)</span><span class="sxs-lookup"><span data-stu-id="aeaf1-166">datetime.datetime(2016, 4, 18, 17, 36, 27, 832799)</span></span>

### <a name="import-libraries"></a><span data-ttu-id="aeaf1-167">Import libraries</span><span class="sxs-lookup"><span data-stu-id="aeaf1-167">Import libraries</span></span>
<span data-ttu-id="aeaf1-168">Import necessary libraries with the following code:</span><span class="sxs-lookup"><span data-stu-id="aeaf1-168">Import necessary libraries with the following code:</span></span>

    # LOAD PYSPARK LIBRARIES
    import pyspark
    from pyspark import SparkConf
    from pyspark import SparkContext
    from pyspark.sql import SQLContext
    import matplotlib
    import matplotlib.pyplot as plt
    from pyspark.sql import Row
    from pyspark.sql.functions import UserDefinedFunction
    from pyspark.sql.types import *
    import atexit
    from numpy import array
    import numpy as np
    import datetime


### <a name="preset-spark-context-and-pyspark-magics"></a><span data-ttu-id="aeaf1-169">Preset Spark context and PySpark magics</span><span class="sxs-lookup"><span data-stu-id="aeaf1-169">Preset Spark context and PySpark magics</span></span>
<span data-ttu-id="aeaf1-170">The PySpark kernels that are provided with Jupyter notebooks have a preset context.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-170">The PySpark kernels that are provided with Jupyter notebooks have a preset context.</span></span> <span data-ttu-id="aeaf1-171">So you do not need to set the Spark or Hive contexts explicitly before you start working with the application you are developing.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-171">So you do not need to set the Spark or Hive contexts explicitly before you start working with the application you are developing.</span></span> <span data-ttu-id="aeaf1-172">These contexts are available for you by default.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-172">These contexts are available for you by default.</span></span> <span data-ttu-id="aeaf1-173">These contexts are:</span><span class="sxs-lookup"><span data-stu-id="aeaf1-173">These contexts are:</span></span>

* <span data-ttu-id="aeaf1-174">sc - for Spark</span><span class="sxs-lookup"><span data-stu-id="aeaf1-174">sc - for Spark</span></span> 
* <span data-ttu-id="aeaf1-175">sqlContext - for Hive</span><span class="sxs-lookup"><span data-stu-id="aeaf1-175">sqlContext - for Hive</span></span>

<span data-ttu-id="aeaf1-176">The PySpark kernel provides some predefined “magics”, which are special commands that you can call with %%.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-176">The PySpark kernel provides some predefined “magics”, which are special commands that you can call with %%.</span></span> <span data-ttu-id="aeaf1-177">There are two such commands that are used in these code samples.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-177">There are two such commands that are used in these code samples.</span></span>

* <span data-ttu-id="aeaf1-178">**%%local** Specifies that the code in subsequent lines is to be executed locally.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-178">**%%local** Specifies that the code in subsequent lines is to be executed locally.</span></span> <span data-ttu-id="aeaf1-179">Code must be valid Python code.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-179">Code must be valid Python code.</span></span>
* <span data-ttu-id="aeaf1-180">**%%sql -o <variable name>** Executes a Hive query against the sqlContext.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-180">**%%sql -o <variable name>** Executes a Hive query against the sqlContext.</span></span> <span data-ttu-id="aeaf1-181">If the -o parameter is passed, the result of the query is persisted in the %%local Python context as a Pandas DataFrame.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-181">If the -o parameter is passed, the result of the query is persisted in the %%local Python context as a Pandas DataFrame.</span></span>

<span data-ttu-id="aeaf1-182">For more information on the kernels for Jupyter notebooks and the predefined "magics" that they provide, see [Kernels available for Jupyter notebooks with HDInsight Spark Linux clusters on HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="aeaf1-182">For more information on the kernels for Jupyter notebooks and the predefined "magics" that they provide, see [Kernels available for Jupyter notebooks with HDInsight Spark Linux clusters on HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

## <a name="data-ingestion-from-public-blob"></a><span data-ttu-id="aeaf1-183">Data ingestion from public blob:</span><span class="sxs-lookup"><span data-stu-id="aeaf1-183">Data ingestion from public blob:</span></span>
<span data-ttu-id="aeaf1-184">The first step in the data science process is to ingest the data to be analyzed from sources where it resides into your data exploration and modeling environment.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-184">The first step in the data science process is to ingest the data to be analyzed from sources where it resides into your data exploration and modeling environment.</span></span> <span data-ttu-id="aeaf1-185">This environment is Spark in this walkthrough.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-185">This environment is Spark in this walkthrough.</span></span> <span data-ttu-id="aeaf1-186">This section contains the code to complete a series of tasks:</span><span class="sxs-lookup"><span data-stu-id="aeaf1-186">This section contains the code to complete a series of tasks:</span></span>

* <span data-ttu-id="aeaf1-187">ingest the data sample to be modeled</span><span class="sxs-lookup"><span data-stu-id="aeaf1-187">ingest the data sample to be modeled</span></span>
* <span data-ttu-id="aeaf1-188">read in the input dataset (stored as a .tsv file)</span><span class="sxs-lookup"><span data-stu-id="aeaf1-188">read in the input dataset (stored as a .tsv file)</span></span>
* <span data-ttu-id="aeaf1-189">format and clean the data</span><span class="sxs-lookup"><span data-stu-id="aeaf1-189">format and clean the data</span></span>
* <span data-ttu-id="aeaf1-190">create and cache objects (RDDs or data-frames) in memory</span><span class="sxs-lookup"><span data-stu-id="aeaf1-190">create and cache objects (RDDs or data-frames) in memory</span></span>
* <span data-ttu-id="aeaf1-191">register it as a temp-table in SQL-context.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-191">register it as a temp-table in SQL-context.</span></span>

<span data-ttu-id="aeaf1-192">Here is the code for data ingestion.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-192">Here is the code for data ingestion.</span></span>

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # IMPORT FILE FROM PUBLIC BLOB
    taxi_train_file = sc.textFile(taxi_train_file_loc)

    # GET SCHEMA OF THE FILE FROM HEADER
    schema_string = taxi_train_file.first()
    fields = [StructField(field_name, StringType(), True) for field_name in schema_string.split('\t')]
    fields[7].dataType = IntegerType() #Pickup hour
    fields[8].dataType = IntegerType() # Pickup week
    fields[9].dataType = IntegerType() # Weekday
    fields[10].dataType = IntegerType() # Passenger count
    fields[11].dataType = FloatType() # Trip time in secs
    fields[12].dataType = FloatType() # Trip distance
    fields[19].dataType = FloatType() # Fare amount
    fields[20].dataType = FloatType() # Surcharge
    fields[21].dataType = FloatType() # Mta_tax
    fields[22].dataType = FloatType() # Tip amount
    fields[23].dataType = FloatType() # Tolls amount
    fields[24].dataType = FloatType() # Total amount
    fields[25].dataType = IntegerType() # Tipped or not
    fields[26].dataType = IntegerType() # Tip class
    taxi_schema = StructType(fields)

    # PARSE FIELDS AND CONVERT DATA TYPE FOR SOME FIELDS
    taxi_header = taxi_train_file.filter(lambda l: "medallion" in l)
    taxi_temp = taxi_train_file.subtract(taxi_header).map(lambda k: k.split("\t"))\
            .map(lambda p: (p[0],p[1],p[2],p[3],p[4],p[5],p[6],int(p[7]),int(p[8]),int(p[9]),int(p[10]),
                            float(p[11]),float(p[12]),p[13],p[14],p[15],p[16],p[17],p[18],float(p[19]),
                            float(p[20]),float(p[21]),float(p[22]),float(p[23]),float(p[24]),int(p[25]),int(p[26])))


    # CREATE DATA FRAME
    taxi_train_df = sqlContext.createDataFrame(taxi_temp, taxi_schema)

    # CREATE A CLEANED DATA-FRAME BY DROPPING SOME UN-NECESSARY COLUMNS & FILTERING FOR UNDESIRED VALUES OR OUTLIERS
    taxi_df_train_cleaned = taxi_train_df.drop('medallion').drop('hack_license').drop('store_and_fwd_flag').drop('pickup_datetime')\
        .drop('dropoff_datetime').drop('pickup_longitude').drop('pickup_latitude').drop('dropoff_latitude')\
        .drop('dropoff_longitude').drop('tip_class').drop('total_amount').drop('tolls_amount').drop('mta_tax')\
        .drop('direct_distance').drop('surcharge')\
        .filter("passenger_count > 0 and passenger_count < 8 AND payment_type in ('CSH', 'CRD') AND tip_amount >= 0 AND tip_amount < 30 AND fare_amount >= 1 AND fare_amount < 150 AND trip_distance > 0 AND trip_distance < 100 AND trip_time_in_secs > 30 AND trip_time_in_secs < 7200" )

    # CACHE & MATERIALIZE DATA-FRAME IN MEMORY. GOING THROUGH AND COUNTING NUMBER OF ROWS MATERIALIZES THE DATA-FRAME IN MEMORY
    taxi_df_train_cleaned.cache()
    taxi_df_train_cleaned.count()

    # REGISTER DATA-FRAME AS A TEMP-TABLE IN SQL-CONTEXT
    taxi_df_train_cleaned.registerTempTable("taxi_train")

    # PRINT HOW MUCH TIME IT TOOK TO RUN THE CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="aeaf1-193">**OUTPUT**</span><span class="sxs-lookup"><span data-stu-id="aeaf1-193">**OUTPUT**</span></span>

<span data-ttu-id="aeaf1-194">Time taken to execute above cell: 276.62 seconds</span><span class="sxs-lookup"><span data-stu-id="aeaf1-194">Time taken to execute above cell: 276.62 seconds</span></span>

## <a name="data-exploration--visualization"></a><span data-ttu-id="aeaf1-195">Data exploration & visualization</span><span class="sxs-lookup"><span data-stu-id="aeaf1-195">Data exploration & visualization</span></span>
<span data-ttu-id="aeaf1-196">Once the data has been brought into Spark, the next step in the data science process is to gain deeper understanding of the data through exploration and visualization.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-196">Once the data has been brought into Spark, the next step in the data science process is to gain deeper understanding of the data through exploration and visualization.</span></span> <span data-ttu-id="aeaf1-197">In this section, we examine the taxi data using SQL queries and plot the target variables and prospective features for visual inspection.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-197">In this section, we examine the taxi data using SQL queries and plot the target variables and prospective features for visual inspection.</span></span> <span data-ttu-id="aeaf1-198">Specifically, we plot the frequency of passenger counts in taxi trips, the frequency of tip amounts, and how tips vary by payment amount and type.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-198">Specifically, we plot the frequency of passenger counts in taxi trips, the frequency of tip amounts, and how tips vary by payment amount and type.</span></span>

### <a name="plot-a-histogram-of-passenger-count-frequencies-in-the-sample-of-taxi-trips"></a><span data-ttu-id="aeaf1-199">Plot a histogram of passenger count frequencies in the sample of taxi trips</span><span class="sxs-lookup"><span data-stu-id="aeaf1-199">Plot a histogram of passenger count frequencies in the sample of taxi trips</span></span>
<span data-ttu-id="aeaf1-200">This code and subsequent snippets use SQL magic to query the sample and local magic to plot the data.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-200">This code and subsequent snippets use SQL magic to query the sample and local magic to plot the data.</span></span>

* <span data-ttu-id="aeaf1-201">**SQL magic (`%%sql`)** The HDInsight PySpark kernel supports easy inline HiveQL queries against the sqlContext.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-201">**SQL magic (`%%sql`)** The HDInsight PySpark kernel supports easy inline HiveQL queries against the sqlContext.</span></span> <span data-ttu-id="aeaf1-202">The (-o VARIABLE_NAME) argument persists the output of the SQL query as a Pandas DataFrame on the Jupyter server.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-202">The (-o VARIABLE_NAME) argument persists the output of the SQL query as a Pandas DataFrame on the Jupyter server.</span></span> <span data-ttu-id="aeaf1-203">This means it is available in the local mode.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-203">This means it is available in the local mode.</span></span>
* <span data-ttu-id="aeaf1-204">The **`%%local` magic** is used to run code locally on the Jupyter server, which is the headnode of the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-204">The **`%%local` magic** is used to run code locally on the Jupyter server, which is the headnode of the HDInsight cluster.</span></span> <span data-ttu-id="aeaf1-205">Typically, you use `%%local` magic after the `%%sql -o` magic is used to run a query.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-205">Typically, you use `%%local` magic after the `%%sql -o` magic is used to run a query.</span></span> <span data-ttu-id="aeaf1-206">The -o parameter would persist the output of the SQL query locally.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-206">The -o parameter would persist the output of the SQL query locally.</span></span> <span data-ttu-id="aeaf1-207">Then the `%%local` magic triggers the next set of code snippets to run locally against the output of the SQL queries that has been persisted locally.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-207">Then the `%%local` magic triggers the next set of code snippets to run locally against the output of the SQL queries that has been persisted locally.</span></span> <span data-ttu-id="aeaf1-208">The output is automatically visualized after you run the code.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-208">The output is automatically visualized after you run the code.</span></span>

<span data-ttu-id="aeaf1-209">This query retrieves the trips by passenger count.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-209">This query retrieves the trips by passenger count.</span></span> 

    # PLOT FREQUENCY OF PASSENGER COUNTS IN TAXI TRIPS

    # SQL QUERY
    %%sql -q -o sqlResults
    SELECT passenger_count, COUNT(*) as trip_counts FROM taxi_train WHERE passenger_count > 0 and passenger_count < 7 GROUP BY passenger_count


<span data-ttu-id="aeaf1-210">This code creates a local data-frame from the query output and plots the data.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-210">This code creates a local data-frame from the query output and plots the data.</span></span> <span data-ttu-id="aeaf1-211">The `%%local` magic creates a local data-frame, `sqlResults`, which can be used for plotting with matplotlib.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-211">The `%%local` magic creates a local data-frame, `sqlResults`, which can be used for plotting with matplotlib.</span></span> 

> [!NOTE]
> <span data-ttu-id="aeaf1-212">This PySpark magic is used multiple times in this walkthrough.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-212">This PySpark magic is used multiple times in this walkthrough.</span></span> <span data-ttu-id="aeaf1-213">If the amount of data is large, you should sample to create a data-frame that can fit in local memory.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-213">If the amount of data is large, you should sample to create a data-frame that can fit in local memory.</span></span>
> 
> 

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER
    %%local

    # USE THE JUPYTER AUTO-PLOTTING FEATURE TO CREATE INTERACTIVE FIGURES. 
    # CLICK ON THE TYPE OF PLOT TO BE GENERATED (E.G. LINE, AREA, BAR ETC.)
    sqlResults

<span data-ttu-id="aeaf1-214">Here is the code to plot the trips by passenger counts</span><span class="sxs-lookup"><span data-stu-id="aeaf1-214">Here is the code to plot the trips by passenger counts</span></span>

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    import matplotlib.pyplot as plt
    %matplotlib inline

    # PLOT PASSENGER NUMBER VS TRIP COUNTS
    x_labels = sqlResults['passenger_count'].values
    fig = sqlResults[['trip_counts']].plot(kind='bar', facecolor='lightblue')
    fig.set_xticklabels(x_labels)
    fig.set_title('Counts of trips by passenger count')
    fig.set_xlabel('Passenger count in trips')
    fig.set_ylabel('Trip counts')
    plt.show()

<span data-ttu-id="aeaf1-215">**OUTPUT**</span><span class="sxs-lookup"><span data-stu-id="aeaf1-215">**OUTPUT**</span></span>

![Frequency of trips by passenger count](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-spark-advanced-data-exploration-modeling/frequency-of-trips-by-passenger-count.png)

<span data-ttu-id="aeaf1-217">You can select among several different types of visualizations (Table, Pie, Line, Area, or Bar) by using the **Type** menu buttons in the notebook.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-217">You can select among several different types of visualizations (Table, Pie, Line, Area, or Bar) by using the **Type** menu buttons in the notebook.</span></span> <span data-ttu-id="aeaf1-218">The Bar plot is shown here.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-218">The Bar plot is shown here.</span></span>

### <a name="plot-a-histogram-of-tip-amounts-and-how-tip-amount-varies-by-passenger-count-and-fare-amounts"></a><span data-ttu-id="aeaf1-219">Plot a histogram of tip amounts and how tip amount varies by passenger count and fare amounts.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-219">Plot a histogram of tip amounts and how tip amount varies by passenger count and fare amounts.</span></span>
<span data-ttu-id="aeaf1-220">Use a SQL query to sample data..</span><span class="sxs-lookup"><span data-stu-id="aeaf1-220">Use a SQL query to sample data..</span></span>

    # SQL SQUERY
    %%sql -q -o sqlResults
        SELECT fare_amount, passenger_count, tip_amount, tipped
        FROM taxi_train 
        WHERE passenger_count > 0 
        AND passenger_count < 7
        AND fare_amount > 0 
        AND fare_amount < 200
        AND payment_type in ('CSH', 'CRD')
        AND tip_amount > 0 
        AND tip_amount < 25


<span data-ttu-id="aeaf1-221">This code cell uses the SQL query to create three plots the data.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-221">This code cell uses the SQL query to create three plots the data.</span></span>

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    %matplotlib inline

    # TIP BY PAYMENT TYPE AND PASSENGER COUNT
    ax1 = resultsPDDF[['tip_amount']].plot(kind='hist', bins=25, facecolor='lightblue')
    ax1.set_title('Tip amount distribution')
    ax1.set_xlabel('Tip Amount ($)')
    ax1.set_ylabel('Counts')
    plt.suptitle('')
    plt.show()

    # TIP BY PASSENGER COUNT
    ax2 = resultsPDDF.boxplot(column=['tip_amount'], by=['passenger_count'])
    ax2.set_title('Tip amount ($) by Passenger count')
    ax2.set_xlabel('Passenger count')
    ax2.set_ylabel('Tip Amount ($)')
    plt.suptitle('')
    plt.show()

    # TIP AMOUNT BY FARE AMOUNT, POINTS ARE SCALED BY PASSENGER COUNT
    ax = resultsPDDF.plot(kind='scatter', x= 'fare_amount', y = 'tip_amount', c='blue', alpha = 0.10, s=5*(resultsPDDF.passenger_count))
    ax.set_title('Tip amount by Fare amount ($)')
    ax.set_xlabel('Fare Amount')
    ax.set_ylabel('Tip Amount')
    plt.axis([-2, 120, -2, 30])
    plt.show()


<span data-ttu-id="aeaf1-222">**OUTPUT:**</span><span class="sxs-lookup"><span data-stu-id="aeaf1-222">**OUTPUT:**</span></span> 

![Tip amount distribution](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-spark-advanced-data-exploration-modeling/tip-amount-distribution.png)

![Tip amount by passenger count](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-spark-advanced-data-exploration-modeling/tip-amount-by-passenger-count.png)

![Tip amount by fare Amount](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-spark-advanced-data-exploration-modeling/tip-amount-by-fare-amount.png)

## <a name="feature-engineering-transformation-and-data-preparation-for-modeling"></a><span data-ttu-id="aeaf1-226">Feature engineering, transformation, and data preparation for modeling</span><span class="sxs-lookup"><span data-stu-id="aeaf1-226">Feature engineering, transformation, and data preparation for modeling</span></span>
<span data-ttu-id="aeaf1-227">This section describes and provides the code for procedures used to prepare data for use in ML modeling.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-227">This section describes and provides the code for procedures used to prepare data for use in ML modeling.</span></span> <span data-ttu-id="aeaf1-228">It shows how to do the following tasks:</span><span class="sxs-lookup"><span data-stu-id="aeaf1-228">It shows how to do the following tasks:</span></span>

* <span data-ttu-id="aeaf1-229">Create a new feature by partitioning hours into traffic time bins</span><span class="sxs-lookup"><span data-stu-id="aeaf1-229">Create a new feature by partitioning hours into traffic time bins</span></span>
* <span data-ttu-id="aeaf1-230">Index and on-hot encode categorical features</span><span class="sxs-lookup"><span data-stu-id="aeaf1-230">Index and on-hot encode categorical features</span></span>
* <span data-ttu-id="aeaf1-231">Create labeled point objects for input into ML functions</span><span class="sxs-lookup"><span data-stu-id="aeaf1-231">Create labeled point objects for input into ML functions</span></span>
* <span data-ttu-id="aeaf1-232">Create a random sub-sampling of the data and split it into training and testing sets</span><span class="sxs-lookup"><span data-stu-id="aeaf1-232">Create a random sub-sampling of the data and split it into training and testing sets</span></span>
* <span data-ttu-id="aeaf1-233">Feature scaling</span><span class="sxs-lookup"><span data-stu-id="aeaf1-233">Feature scaling</span></span>
* <span data-ttu-id="aeaf1-234">Cache objects in memory</span><span class="sxs-lookup"><span data-stu-id="aeaf1-234">Cache objects in memory</span></span>

### <a name="create-a-new-feature-by-partitioning-traffic-times-into-bins"></a><span data-ttu-id="aeaf1-235">Create a new feature by partitioning traffic times into bins</span><span class="sxs-lookup"><span data-stu-id="aeaf1-235">Create a new feature by partitioning traffic times into bins</span></span>
<span data-ttu-id="aeaf1-236">This code shows how to create a new feature by partitioning traffic times into bins and then how to cache the resulting data frame in memory.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-236">This code shows how to create a new feature by partitioning traffic times into bins and then how to cache the resulting data frame in memory.</span></span> <span data-ttu-id="aeaf1-237">Caching leads to improved execution time where Resilient Distributed Datasets (RDDs) and data-frames are used repeatedly.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-237">Caching leads to improved execution time where Resilient Distributed Datasets (RDDs) and data-frames are used repeatedly.</span></span> <span data-ttu-id="aeaf1-238">So, we cache RDDs and data-frames at several stages in this walkthrough.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-238">So, we cache RDDs and data-frames at several stages in this walkthrough.</span></span>

    # CREATE FOUR BUCKETS FOR TRAFFIC TIMES
    sqlStatement = """
        SELECT *,
        CASE
         WHEN (pickup_hour <= 6 OR pickup_hour >= 20) THEN "Night" 
         WHEN (pickup_hour >= 7 AND pickup_hour <= 10) THEN "AMRush" 
         WHEN (pickup_hour >= 11 AND pickup_hour <= 15) THEN "Afternoon"
         WHEN (pickup_hour >= 16 AND pickup_hour <= 19) THEN "PMRush"
        END as TrafficTimeBins
        FROM taxi_train 
    """
    taxi_df_train_with_newFeatures = sqlContext.sql(sqlStatement)

    # CACHE DATA-FRAME IN MEMORY & MATERIALIZE DF IN MEMORY
    # THE .COUNT() GOES THROUGH THE ENTIRE DATA-FRAME,
    # MATERIALIZES IT IN MEMORY, AND GIVES THE COUNT OF ROWS.
    taxi_df_train_with_newFeatures.cache()
    taxi_df_train_with_newFeatures.count()

<span data-ttu-id="aeaf1-239">**OUTPUT**</span><span class="sxs-lookup"><span data-stu-id="aeaf1-239">**OUTPUT**</span></span>

<span data-ttu-id="aeaf1-240">126050</span><span class="sxs-lookup"><span data-stu-id="aeaf1-240">126050</span></span>

### <a name="index-and-one-hot-encode-categorical-features"></a><span data-ttu-id="aeaf1-241">Index and one-hot encode categorical features</span><span class="sxs-lookup"><span data-stu-id="aeaf1-241">Index and one-hot encode categorical features</span></span>
<span data-ttu-id="aeaf1-242">This section shows how to index or encode categorical features for input into the modeling functions.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-242">This section shows how to index or encode categorical features for input into the modeling functions.</span></span> <span data-ttu-id="aeaf1-243">The modeling and predict functions of MLlib require that features with categorical input data be indexed or encoded prior to use.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-243">The modeling and predict functions of MLlib require that features with categorical input data be indexed or encoded prior to use.</span></span> 

<span data-ttu-id="aeaf1-244">Depending on the model, you need to index or encode them in different ways.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-244">Depending on the model, you need to index or encode them in different ways.</span></span> <span data-ttu-id="aeaf1-245">For example, Logistic and Linear Regression models require one-hot encoding, where, for example, a feature with three categories can be expanded into three feature columns, with each containing 0 or 1 depending on the category of an observation.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-245">For example, Logistic and Linear Regression models require one-hot encoding, where, for example, a feature with three categories can be expanded into three feature columns, with each containing 0 or 1 depending on the category of an observation.</span></span> <span data-ttu-id="aeaf1-246">MLlib provides [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) function to do one-hot encoding.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-246">MLlib provides [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) function to do one-hot encoding.</span></span> <span data-ttu-id="aeaf1-247">This encoder maps a column of label indices to a column of binary vectors, with at most a single one-value.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-247">This encoder maps a column of label indices to a column of binary vectors, with at most a single one-value.</span></span> <span data-ttu-id="aeaf1-248">This encoding allows algorithms that expect numerical valued features, such as logistic regression, to be applied to categorical features.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-248">This encoding allows algorithms that expect numerical valued features, such as logistic regression, to be applied to categorical features.</span></span>

<span data-ttu-id="aeaf1-249">Here is the code to index and encode categorical features:</span><span class="sxs-lookup"><span data-stu-id="aeaf1-249">Here is the code to index and encode categorical features:</span></span>

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.ml.feature import OneHotEncoder, StringIndexer, VectorAssembler, OneHotEncoder, VectorIndexer

    # INDEX AND ENCODE VENDOR_ID
    stringIndexer = StringIndexer(inputCol="vendor_id", outputCol="vendorIndex")
    model = stringIndexer.fit(taxi_df_train_with_newFeatures) # Input data-frame is the cleaned one from above
    indexed = model.transform(taxi_df_train_with_newFeatures)
    encoder = OneHotEncoder(dropLast=False, inputCol="vendorIndex", outputCol="vendorVec")
    encoded1 = encoder.transform(indexed)

    # INDEX AND ENCODE RATE_CODE
    stringIndexer = StringIndexer(inputCol="rate_code", outputCol="rateIndex")
    model = stringIndexer.fit(encoded1)
    indexed = model.transform(encoded1)
    encoder = OneHotEncoder(dropLast=False, inputCol="rateIndex", outputCol="rateVec")
    encoded2 = encoder.transform(indexed)

    # INDEX AND ENCODE PAYMENT_TYPE
    stringIndexer = StringIndexer(inputCol="payment_type", outputCol="paymentIndex")
    model = stringIndexer.fit(encoded2)
    indexed = model.transform(encoded2)
    encoder = OneHotEncoder(dropLast=False, inputCol="paymentIndex", outputCol="paymentVec")
    encoded3 = encoder.transform(indexed)

    # INDEX AND TRAFFIC TIME BINS
    stringIndexer = StringIndexer(inputCol="TrafficTimeBins", outputCol="TrafficTimeBinsIndex")
    model = stringIndexer.fit(encoded3)
    indexed = model.transform(encoded3)
    encoder = OneHotEncoder(dropLast=False, inputCol="TrafficTimeBinsIndex", outputCol="TrafficTimeBinsVec")
    encodedFinal = encoder.transform(indexed)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="aeaf1-250">**OUTPUT**</span><span class="sxs-lookup"><span data-stu-id="aeaf1-250">**OUTPUT**</span></span>

<span data-ttu-id="aeaf1-251">Time taken to execute above cell: 3.14 seconds</span><span class="sxs-lookup"><span data-stu-id="aeaf1-251">Time taken to execute above cell: 3.14 seconds</span></span>

### <a name="create-labeled-point-objects-for-input-into-ml-functions"></a><span data-ttu-id="aeaf1-252">Create labeled point objects for input into ML functions</span><span class="sxs-lookup"><span data-stu-id="aeaf1-252">Create labeled point objects for input into ML functions</span></span>
<span data-ttu-id="aeaf1-253">This section contains code that shows how to index categorical text data as a labeled point data type and how to encode it.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-253">This section contains code that shows how to index categorical text data as a labeled point data type and how to encode it.</span></span> <span data-ttu-id="aeaf1-254">This prepares it to be used to train and test MLlib logistic regression and other classification models.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-254">This prepares it to be used to train and test MLlib logistic regression and other classification models.</span></span> <span data-ttu-id="aeaf1-255">Labeled point objects are Resilient Distributed Datasets (RDD) formatted in a way that is needed as input data by most of ML algorithms in MLlib.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-255">Labeled point objects are Resilient Distributed Datasets (RDD) formatted in a way that is needed as input data by most of ML algorithms in MLlib.</span></span> <span data-ttu-id="aeaf1-256">A [labeled point](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) is a local vector, either dense or sparse, associated with a label/response.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-256">A [labeled point](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) is a local vector, either dense or sparse, associated with a label/response.</span></span>

<span data-ttu-id="aeaf1-257">Here is the code to index and encode text features for binary classification.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-257">Here is the code to index and encode text features for binary classification.</span></span>

    # FUNCTIONS FOR BINARY CLASSIFICATION

    # LOAD LIBRARIES
    from pyspark.mllib.regression import LabeledPoint
    from numpy import array

    # INDEXING CATEGORICAL TEXT FEATURES FOR INPUT INTO TREE-BASED MODELS
    def parseRowIndexingBinary(line):
        features = np.array([line.paymentIndex, line.vendorIndex, line.rateIndex, line.pickup_hour, line.weekday,
                             line.passenger_count, line.trip_time_in_secs, line.trip_distance, line.fare_amount])
        labPt = LabeledPoint(line.tipped, features)
        return  labPt

    # ONE-HOT ENCODING OF CATEGORICAL TEXT FEATURES FOR INPUT INTO LOGISTIC RERESSION MODELS
    def parseRowOneHotBinary(line):
        features = np.concatenate((np.array([line.pickup_hour, line.weekday, line.passenger_count,
                                            line.trip_time_in_secs, line.trip_distance, line.fare_amount]), 
                                   line.vendorVec.toArray(), line.rateVec.toArray(), line.paymentVec.toArray()), axis=0)
        labPt = LabeledPoint(line.tipped, features)
        return  labPt


<span data-ttu-id="aeaf1-258">Here is the code to encode and index categorical text features for linear regression analysis.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-258">Here is the code to encode and index categorical text features for linear regression analysis.</span></span>

    # FUNCTIONS FOR REGRESSION WITH TIP AMOUNT AS TARGET VARIABLE

    # ONE-HOT ENCODING OF CATEGORICAL TEXT FEATURES FOR INPUT INTO TREE-BASED MODELS
    def parseRowIndexingRegression(line):
        features = np.array([line.paymentIndex, line.vendorIndex, line.rateIndex, line.TrafficTimeBinsIndex, 
                             line.pickup_hour, line.weekday, line.passenger_count, line.trip_time_in_secs, 
                             line.trip_distance, line.fare_amount])
        labPt = LabeledPoint(line.tip_amount, features)
        return  labPt

    # INDEXING CATEGORICAL TEXT FEATURES FOR INPUT INTO LINEAR REGRESSION MODELS
    def parseRowOneHotRegression(line):
        features = np.concatenate((np.array([line.pickup_hour, line.weekday, line.passenger_count,
                                            line.trip_time_in_secs, line.trip_distance, line.fare_amount]), 
                                            line.vendorVec.toArray(), line.rateVec.toArray(), 
                                            line.paymentVec.toArray(), line.TrafficTimeBinsVec.toArray()), axis=0)
        labPt = LabeledPoint(line.tip_amount, features)
        return  labPt


### <a name="create-a-random-sub-sampling-of-the-data-and-split-it-into-training-and-testing-sets"></a><span data-ttu-id="aeaf1-259">Create a random sub-sampling of the data and split it into training and testing sets</span><span class="sxs-lookup"><span data-stu-id="aeaf1-259">Create a random sub-sampling of the data and split it into training and testing sets</span></span>
<span data-ttu-id="aeaf1-260">This code creates a random sampling of the data (25% is used here).</span><span class="sxs-lookup"><span data-stu-id="aeaf1-260">This code creates a random sampling of the data (25% is used here).</span></span> <span data-ttu-id="aeaf1-261">Although it is not required for this example due to the size of the dataset, we demonstrate how you can sample the data here.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-261">Although it is not required for this example due to the size of the dataset, we demonstrate how you can sample the data here.</span></span> <span data-ttu-id="aeaf1-262">Then you know how to use it for your own problem if needed.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-262">Then you know how to use it for your own problem if needed.</span></span> <span data-ttu-id="aeaf1-263">When samples are large, this can save significant time while training models.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-263">When samples are large, this can save significant time while training models.</span></span> <span data-ttu-id="aeaf1-264">Next we split the sample into a training part (75% here) and a testing part (25% here) to use in classification and regression modeling.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-264">Next we split the sample into a training part (75% here) and a testing part (25% here) to use in classification and regression modeling.</span></span>

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # SPECIFY SAMPLING AND SPLITTING FRACTIONS
    from pyspark.sql.functions import rand

    samplingFraction = 0.25;
    trainingFraction = 0.75; testingFraction = (1-trainingFraction);
    seed = 1234;
    encodedFinalSampled = encodedFinal.sample(False, samplingFraction, seed=seed)

    # SPLIT SAMPLED DATA-FRAME INTO TRAIN/TEST, WITH A RANDOM COLUMN ADDED FOR DOING CV (SHOWN LATER)
    # INCLUDE RAND COLUMN FOR CREATING CROSS-VALIDATION FOLDS
    dfTmpRand = encodedFinalSampled.select("*", rand(0).alias("rand"));
    trainData, testData = dfTmpRand.randomSplit([trainingFraction, testingFraction], seed=seed);

    # CACHE TRAIN AND TEST DATA
    trainData.cache()
    testData.cache()

    # FOR BINARY CLASSIFICATION TRAINING AND TESTING
    indexedTRAINbinary = trainData.map(parseRowIndexingBinary)
    indexedTESTbinary = testData.map(parseRowIndexingBinary)
    oneHotTRAINbinary = trainData.map(parseRowOneHotBinary)
    oneHotTESTbinary = testData.map(parseRowOneHotBinary)

    # FOR REGRESSION TRAINING AND TESTING
    indexedTRAINreg = trainData.map(parseRowIndexingRegression)
    indexedTESTreg = testData.map(parseRowIndexingRegression)
    oneHotTRAINreg = trainData.map(parseRowOneHotRegression)
    oneHotTESTreg = testData.map(parseRowOneHotRegression)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="aeaf1-265">**OUTPUT**</span><span class="sxs-lookup"><span data-stu-id="aeaf1-265">**OUTPUT**</span></span>

<span data-ttu-id="aeaf1-266">Time taken to execute above cell: 0.31 seconds</span><span class="sxs-lookup"><span data-stu-id="aeaf1-266">Time taken to execute above cell: 0.31 seconds</span></span>

### <a name="feature-scaling"></a><span data-ttu-id="aeaf1-267">Feature scaling</span><span class="sxs-lookup"><span data-stu-id="aeaf1-267">Feature scaling</span></span>
<span data-ttu-id="aeaf1-268">Feature scaling, also known as data normalization, insures that features with widely disbursed values are not given excessive weigh in the objective function.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-268">Feature scaling, also known as data normalization, insures that features with widely disbursed values are not given excessive weigh in the objective function.</span></span> <span data-ttu-id="aeaf1-269">The code for feature scaling uses the [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) to scale the features to unit variance.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-269">The code for feature scaling uses the [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) to scale the features to unit variance.</span></span> <span data-ttu-id="aeaf1-270">It is provided by MLlib for use in linear regression with Stochastic Gradient Descent (SGD).</span><span class="sxs-lookup"><span data-stu-id="aeaf1-270">It is provided by MLlib for use in linear regression with Stochastic Gradient Descent (SGD).</span></span> <span data-ttu-id="aeaf1-271">SGD is a popular algorithm for training a wide range of other machine learning models such as regularized regressions or support vector machines (SVM).</span><span class="sxs-lookup"><span data-stu-id="aeaf1-271">SGD is a popular algorithm for training a wide range of other machine learning models such as regularized regressions or support vector machines (SVM).</span></span>   

> [!TIP]
> <span data-ttu-id="aeaf1-272">We have found the LinearRegressionWithSGD algorithm to be sensitive to feature scaling.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-272">We have found the LinearRegressionWithSGD algorithm to be sensitive to feature scaling.</span></span>   
> 
> 

<span data-ttu-id="aeaf1-273">Here is the code to scale variables for use with the regularized linear SGD algorithm.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-273">Here is the code to scale variables for use with the regularized linear SGD algorithm.</span></span>

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.regression import LabeledPoint
    from pyspark.mllib.linalg import Vectors
    from pyspark.mllib.feature import StandardScaler, StandardScalerModel
    from pyspark.mllib.util import MLUtils

    # SCALE VARIABLES FOR REGULARIZED LINEAR SGD ALGORITHM
    label = oneHotTRAINreg.map(lambda x: x.label)
    features = oneHotTRAINreg.map(lambda x: x.features)
    scaler = StandardScaler(withMean=False, withStd=True).fit(features)
    dataTMP = label.zip(scaler.transform(features.map(lambda x: Vectors.dense(x.toArray()))))
    oneHotTRAINregScaled = dataTMP.map(lambda x: LabeledPoint(x[0], x[1]))

    label = oneHotTESTreg.map(lambda x: x.label)
    features = oneHotTESTreg.map(lambda x: x.features)
    scaler = StandardScaler(withMean=False, withStd=True).fit(features)
    dataTMP = label.zip(scaler.transform(features.map(lambda x: Vectors.dense(x.toArray()))))
    oneHotTESTregScaled = dataTMP.map(lambda x: LabeledPoint(x[0], x[1]))

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="aeaf1-274">**OUTPUT**</span><span class="sxs-lookup"><span data-stu-id="aeaf1-274">**OUTPUT**</span></span>

<span data-ttu-id="aeaf1-275">Time taken to execute above cell: 11.67 seconds</span><span class="sxs-lookup"><span data-stu-id="aeaf1-275">Time taken to execute above cell: 11.67 seconds</span></span>

### <a name="cache-objects-in-memory"></a><span data-ttu-id="aeaf1-276">Cache objects in memory</span><span class="sxs-lookup"><span data-stu-id="aeaf1-276">Cache objects in memory</span></span>
<span data-ttu-id="aeaf1-277">The time taken for training and testing of ML algorithms can be reduced by caching the input data frame objects used for classification, regression and, scaled features.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-277">The time taken for training and testing of ML algorithms can be reduced by caching the input data frame objects used for classification, regression and, scaled features.</span></span>

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # FOR BINARY CLASSIFICATION TRAINING AND TESTING
    indexedTRAINbinary.cache()
    indexedTESTbinary.cache()
    oneHotTRAINbinary.cache()
    oneHotTESTbinary.cache()

    # FOR REGRESSION TRAINING AND TESTING
    indexedTRAINreg.cache()
    indexedTESTreg.cache()
    oneHotTRAINreg.cache()
    oneHotTESTreg.cache()

    # SCALED FEATURES
    oneHotTRAINregScaled.cache()
    oneHotTESTregScaled.cache()

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="aeaf1-278">**OUTPUT**</span><span class="sxs-lookup"><span data-stu-id="aeaf1-278">**OUTPUT**</span></span> 

<span data-ttu-id="aeaf1-279">Time taken to execute above cell: 0.13 seconds</span><span class="sxs-lookup"><span data-stu-id="aeaf1-279">Time taken to execute above cell: 0.13 seconds</span></span>

## <a name="predict-whether-or-not-a-tip-is-paid-with-binary-classification-models"></a><span data-ttu-id="aeaf1-280">Predict whether or not a tip is paid with binary classification models</span><span class="sxs-lookup"><span data-stu-id="aeaf1-280">Predict whether or not a tip is paid with binary classification models</span></span>
<span data-ttu-id="aeaf1-281">This section shows how use three models for the binary classification task of predicting whether or not a tip is paid for a taxi trip.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-281">This section shows how use three models for the binary classification task of predicting whether or not a tip is paid for a taxi trip.</span></span> <span data-ttu-id="aeaf1-282">The models presented are:</span><span class="sxs-lookup"><span data-stu-id="aeaf1-282">The models presented are:</span></span>

* <span data-ttu-id="aeaf1-283">Logistic regression</span><span class="sxs-lookup"><span data-stu-id="aeaf1-283">Logistic regression</span></span> 
* <span data-ttu-id="aeaf1-284">Random forest</span><span class="sxs-lookup"><span data-stu-id="aeaf1-284">Random forest</span></span>
* <span data-ttu-id="aeaf1-285">Gradient Boosting Trees</span><span class="sxs-lookup"><span data-stu-id="aeaf1-285">Gradient Boosting Trees</span></span>

<span data-ttu-id="aeaf1-286">Each model building code section is split into steps:</span><span class="sxs-lookup"><span data-stu-id="aeaf1-286">Each model building code section is split into steps:</span></span> 

1. <span data-ttu-id="aeaf1-287">**Model training** data with one parameter set</span><span class="sxs-lookup"><span data-stu-id="aeaf1-287">**Model training** data with one parameter set</span></span>
2. <span data-ttu-id="aeaf1-288">**Model evaluation** on a test data set with metrics</span><span class="sxs-lookup"><span data-stu-id="aeaf1-288">**Model evaluation** on a test data set with metrics</span></span>
3. <span data-ttu-id="aeaf1-289">**Saving model** in blob for future consumption</span><span class="sxs-lookup"><span data-stu-id="aeaf1-289">**Saving model** in blob for future consumption</span></span>

<span data-ttu-id="aeaf1-290">We show how to do cross-validation (CV) with parameter sweeping in two ways:</span><span class="sxs-lookup"><span data-stu-id="aeaf1-290">We show how to do cross-validation (CV) with parameter sweeping in two ways:</span></span>

1. <span data-ttu-id="aeaf1-291">Using **generic** custom code which can be applied to any algorithm in MLlib and to any parameter sets in an algorithm.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-291">Using **generic** custom code which can be applied to any algorithm in MLlib and to any parameter sets in an algorithm.</span></span> 
2. <span data-ttu-id="aeaf1-292">Using the **pySpark CrossValidator pipeline function**.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-292">Using the **pySpark CrossValidator pipeline function**.</span></span> <span data-ttu-id="aeaf1-293">Note that CrossValidator has a few limitations for Spark 1.5.0:</span><span class="sxs-lookup"><span data-stu-id="aeaf1-293">Note that CrossValidator has a few limitations for Spark 1.5.0:</span></span> 
   
   * <span data-ttu-id="aeaf1-294">Pipeline models cannot be saved/persisted for future consumption.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-294">Pipeline models cannot be saved/persisted for future consumption.</span></span>
   * <span data-ttu-id="aeaf1-295">Cannot be used for every parameter in a model.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-295">Cannot be used for every parameter in a model.</span></span>
   * <span data-ttu-id="aeaf1-296">Cannot be used for every MLlib algorithm.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-296">Cannot be used for every MLlib algorithm.</span></span>

### <a name="generic-cross-validation-and-hyperparameter-sweeping-used-with-the-logistic-regression-algorithm-for-binary-classification"></a><span data-ttu-id="aeaf1-297">Generic cross validation and hyperparameter sweeping used with the logistic regression algorithm for binary classification</span><span class="sxs-lookup"><span data-stu-id="aeaf1-297">Generic cross validation and hyperparameter sweeping used with the logistic regression algorithm for binary classification</span></span>
<span data-ttu-id="aeaf1-298">The code in this section shows how to train, evaluate, and save a logistic regression model with [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) that predicts whether or not a tip is paid for a trip in the NYC taxi trip and fare dataset.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-298">The code in this section shows how to train, evaluate, and save a logistic regression model with [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) that predicts whether or not a tip is paid for a trip in the NYC taxi trip and fare dataset.</span></span> <span data-ttu-id="aeaf1-299">The model is trained using cross validation (CV) and hyperparameter sweeping implemented with custom code that can be applied to any of the learning algorithms in MLlib.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-299">The model is trained using cross validation (CV) and hyperparameter sweeping implemented with custom code that can be applied to any of the learning algorithms in MLlib.</span></span>   

> [!NOTE]
> <span data-ttu-id="aeaf1-300">The execution of this custom CV code can take several minutes.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-300">The execution of this custom CV code can take several minutes.</span></span>
> 
> 

<span data-ttu-id="aeaf1-301">**Train the logistic regression model using CV and hyperparameter sweeping**</span><span class="sxs-lookup"><span data-stu-id="aeaf1-301">**Train the logistic regression model using CV and hyperparameter sweeping**</span></span>

    # LOGISTIC REGRESSION CLASSIFICATION WITH CV AND HYPERPARAMETER SWEEPING

    # GET ACCURACY FOR HYPERPARAMETERS BASED ON CROSS-VALIDATION IN TRAINING DATA-SET

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD LIBRARIES
    from pyspark.mllib.classification import LogisticRegressionWithLBFGS 
    from pyspark.mllib.evaluation import BinaryClassificationMetrics

    # CREATE PARAMETER GRID FOR LOGISTIC REGRESSION PARAMETER SWEEP
    from sklearn.grid_search import ParameterGrid
    grid = [{'regParam': [0.01, 0.1], 'iterations': [5, 10], 'regType': ["l1", "l2"], 'tolerance': [1e-3, 1e-4]}]
    paramGrid = list(ParameterGrid(grid))
    numModels = len(paramGrid)

    # SET NUM FOLDS AND NUM PARAMETER SETS TO SWEEP ON
    nFolds = 3;
    h = 1.0 / nFolds;
    metricSum = np.zeros(numModels);

    # BEGIN CV WITH PARAMETER SWEEP
    for i in range(nFolds):
        # Create training and x-validation sets
        validateLB = i * h
        validateUB = (i + 1) * h
        condition = (trainData["rand"] >= validateLB) & (trainData["rand"] < validateUB)
        validation = trainData.filter(condition)
        # Create LabeledPoints from data-frames
        if i > 0:
            trainCVLabPt.unpersist()
            validationLabPt.unpersist()
        trainCV = trainData.filter(~condition)
        trainCVLabPt = trainCV.map(parseRowOneHotBinary)
        trainCVLabPt.cache()
        validationLabPt = validation.map(parseRowOneHotBinary)
        validationLabPt.cache()
        # For parameter sets compute metrics from x-validation
        for j in range(numModels):
            regt = paramGrid[j]['regType']
            regp = paramGrid[j]['regParam']
            iters = paramGrid[j]['iterations']
            tol = paramGrid[j]['tolerance']
            # Train logistic regression model with hypermarameter set
            model = LogisticRegressionWithLBFGS.train(trainCVLabPt, regType=regt, iterations=iters,  
                                                      regParam=regp, tolerance = tol, intercept=True)
            predictionAndLabels = validationLabPt.map(lambda lp: (float(model.predict(lp.features)), lp.label))
            # Use ROC-AUC as accuracy metrics
            validMetrics = BinaryClassificationMetrics(predictionAndLabels)
            metric = validMetrics.areaUnderROC
            metricSum[j] += metric

    avgAcc = metricSum / nFolds;
    bestParam = paramGrid[np.argmax(avgAcc)];

    # UNPERSIST OBJECTS
    trainCVLabPt.unpersist()
    validationLabPt.unpersist()

    # TRAIN ON FULL TRAIING SET USING BEST PARAMETERS FROM CV/PARAMETER SWEEP
    logitBest = LogisticRegressionWithLBFGS.train(oneHotTRAINbinary, regType=bestParam['regType'], 
                                                  iterations=bestParam['iterations'], 
                                                  regParam=bestParam['regParam'], tolerance = bestParam['tolerance'], 
                                                  intercept=True)


    # PRINT COEFFICIENTS AND INTERCEPT OF THE MODEL
    # NOTE: There are 20 coefficient terms for the 10 features, 
    #       and the different categories for features: vendorVec (2), rateVec, paymentVec (6), TrafficTimeBinsVec (4)
    print("Coefficients: " + str(logitBest.weights))
    print("Intercept: " + str(logitBest.intercept))

    # PRINT ELAPSED TIME    
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="aeaf1-302">**OUTPUT**</span><span class="sxs-lookup"><span data-stu-id="aeaf1-302">**OUTPUT**</span></span>

<span data-ttu-id="aeaf1-303">Coefficients: [0.0082065285375, -0.0223675576104, -0.0183812028036, -3.48124578069e-05, -0.00247646947233, -0.00165897881503, 0.0675394837328, -0.111823113101, -0.324609912762, -0.204549780032, -1.36499216354, 0.591088507921, -0.664263411392, -1.00439726852, 3.46567827545, -3.51025855172, -0.0471341112232, -0.043521833294, 0.000243375810385, 0.054518719222]</span><span class="sxs-lookup"><span data-stu-id="aeaf1-303">Coefficients: [0.0082065285375, -0.0223675576104, -0.0183812028036, -3.48124578069e-05, -0.00247646947233, -0.00165897881503, 0.0675394837328, -0.111823113101, -0.324609912762, -0.204549780032, -1.36499216354, 0.591088507921, -0.664263411392, -1.00439726852, 3.46567827545, -3.51025855172, -0.0471341112232, -0.043521833294, 0.000243375810385, 0.054518719222]</span></span>

<span data-ttu-id="aeaf1-304">Intercept: -0.0111216486893</span><span class="sxs-lookup"><span data-stu-id="aeaf1-304">Intercept: -0.0111216486893</span></span>

<span data-ttu-id="aeaf1-305">Time taken to execute above cell: 14.43 seconds</span><span class="sxs-lookup"><span data-stu-id="aeaf1-305">Time taken to execute above cell: 14.43 seconds</span></span>

<span data-ttu-id="aeaf1-306">**Evaluate the binary classification model with standard metrics**</span><span class="sxs-lookup"><span data-stu-id="aeaf1-306">**Evaluate the binary classification model with standard metrics**</span></span>

<span data-ttu-id="aeaf1-307">The code in this section shows how to evaluate a logistic regression model against a test data-set, including a plot of the ROC curve.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-307">The code in this section shows how to evaluate a logistic regression model against a test data-set, including a plot of the ROC curve.</span></span>

    # RECORD START TIME
    timestart = datetime.datetime.now()

    #IMPORT LIBRARIES
    from sklearn.metrics import roc_curve,auc
    from pyspark.mllib.evaluation import BinaryClassificationMetrics
    from pyspark.mllib.evaluation import MulticlassMetrics

    # PREDICT ON TEST DATA WITH BEST/FINAL MODEL
    predictionAndLabels = oneHotTESTbinary.map(lambda lp: (float(logitBest.predict(lp.features)), lp.label))

    # INSTANTIATE METRICS OBJECT
    metrics = BinaryClassificationMetrics(predictionAndLabels)

    # AREA UNDER PRECISION-RECALL CURVE
    print("Area under PR = %s" % metrics.areaUnderPR)

    # AREA UNDER ROC CURVE
    print("Area under ROC = %s" % metrics.areaUnderROC)
    metrics = MulticlassMetrics(predictionAndLabels)

    # OVERALL STATISTICS
    precision = metrics.precision()
    recall = metrics.recall()
    f1Score = metrics.fMeasure()
    print("Summary Stats")
    print("Precision = %s" % precision)
    print("Recall = %s" % recall)
    print("F1 Score = %s" % f1Score)

    # OUTPUT PROBABILITIES AND REGISTER TEMP TABLE
    logitBest.clearThreshold(); # This clears threshold for classification (0.5) and outputs probabilities
    predictionAndLabelsDF = predictionAndLabels.toDF()
    predictionAndLabelsDF.registerTempTable("tmp_results");

    # PRINT ELAPSED TIME    
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="aeaf1-308">**OUTPUT**</span><span class="sxs-lookup"><span data-stu-id="aeaf1-308">**OUTPUT**</span></span>

<span data-ttu-id="aeaf1-309">Area under PR = 0.985336538462</span><span class="sxs-lookup"><span data-stu-id="aeaf1-309">Area under PR = 0.985336538462</span></span>

<span data-ttu-id="aeaf1-310">Area under ROC = 0.983383274312</span><span class="sxs-lookup"><span data-stu-id="aeaf1-310">Area under ROC = 0.983383274312</span></span>

<span data-ttu-id="aeaf1-311">Summary Stats</span><span class="sxs-lookup"><span data-stu-id="aeaf1-311">Summary Stats</span></span>

<span data-ttu-id="aeaf1-312">Precision = 0.984174341679</span><span class="sxs-lookup"><span data-stu-id="aeaf1-312">Precision = 0.984174341679</span></span>

<span data-ttu-id="aeaf1-313">Recall = 0.984174341679</span><span class="sxs-lookup"><span data-stu-id="aeaf1-313">Recall = 0.984174341679</span></span>

<span data-ttu-id="aeaf1-314">F1 Score = 0.984174341679</span><span class="sxs-lookup"><span data-stu-id="aeaf1-314">F1 Score = 0.984174341679</span></span>

<span data-ttu-id="aeaf1-315">Time taken to execute above cell: 2.67 seconds</span><span class="sxs-lookup"><span data-stu-id="aeaf1-315">Time taken to execute above cell: 2.67 seconds</span></span>

<span data-ttu-id="aeaf1-316">**Plot the ROC curve.**</span><span class="sxs-lookup"><span data-stu-id="aeaf1-316">**Plot the ROC curve.**</span></span>

<span data-ttu-id="aeaf1-317">The *predictionAndLabelsDF* is registered as a table, *tmp_results*, in the previous cell.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-317">The *predictionAndLabelsDF* is registered as a table, *tmp_results*, in the previous cell.</span></span> <span data-ttu-id="aeaf1-318">*tmp_results* can be used to do queries and output results into the sqlResults data-frame for plotting.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-318">*tmp_results* can be used to do queries and output results into the sqlResults data-frame for plotting.</span></span> <span data-ttu-id="aeaf1-319">Here is the code.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-319">Here is the code.</span></span>

    # QUERY RESULTS                              
    %%sql -q -o sqlResults
    SELECT * from tmp_results


<span data-ttu-id="aeaf1-320">Here is the code to make predictions and plot the ROC-curve.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-320">Here is the code to make predictions and plot the ROC-curve.</span></span>

    # MAKE PREDICTIONS AND PLOT ROC-CURVE

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER AND IMPORT LIBRARIES                              
    %%local
    %matplotlib inline
    from sklearn.metrics import roc_curve,auc

    #PREDICTIONS
    predictions_pddf = sqlResults.rename(columns={'_1': 'probability', '_2': 'label'})
    prob = predictions_pddf["probability"] 
    fpr, tpr, thresholds = roc_curve(predictions_pddf['label'], prob, pos_label=1);
    roc_auc = auc(fpr, tpr)

    # PLOT ROC CURVES
    plt.figure(figsize=(5,5))
    plt.plot(fpr, tpr, label='ROC curve (area = %0.2f)' % roc_auc)
    plt.plot([0, 1], [0, 1], 'k--')
    plt.xlim([0.0, 1.0])
    plt.ylim([0.0, 1.05])
    plt.xlabel('False Positive Rate')
    plt.ylabel('True Positive Rate')
    plt.title('ROC Curve')
    plt.legend(loc="lower right")
    plt.show()


<span data-ttu-id="aeaf1-321">**OUTPUT**</span><span class="sxs-lookup"><span data-stu-id="aeaf1-321">**OUTPUT**</span></span>

![Logistic regression ROC curve for generic approach](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-spark-advanced-data-exploration-modeling/logistic-regression-roc-curve.png)

<span data-ttu-id="aeaf1-323">**Persist model in a blob for future consumption**</span><span class="sxs-lookup"><span data-stu-id="aeaf1-323">**Persist model in a blob for future consumption**</span></span>

<span data-ttu-id="aeaf1-324">The code in this section shows how to save the logistic regression model for consumption.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-324">The code in this section shows how to save the logistic regression model for consumption.</span></span>

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.classification import LogisticRegressionModel

    # PERSIST MODEL
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    logisticregressionfilename = "LogisticRegressionWithLBFGS_" + datestamp;
    dirfilename = modelDir + logisticregressionfilename;

    logitBest.save(sc, dirfilename);

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds";


<span data-ttu-id="aeaf1-325">**OUTPUT**</span><span class="sxs-lookup"><span data-stu-id="aeaf1-325">**OUTPUT**</span></span>

<span data-ttu-id="aeaf1-326">Time taken to execute above cell: 34.57 seconds</span><span class="sxs-lookup"><span data-stu-id="aeaf1-326">Time taken to execute above cell: 34.57 seconds</span></span>

### <a name="use-mllibs-crossvalidator-pipeline-function-with-logistic-regression-elastic-regression-model"></a><span data-ttu-id="aeaf1-327">Use MLlib's CrossValidator pipeline function with logistic regression (Elastic regression) model</span><span class="sxs-lookup"><span data-stu-id="aeaf1-327">Use MLlib's CrossValidator pipeline function with logistic regression (Elastic regression) model</span></span>
<span data-ttu-id="aeaf1-328">The code in this section shows how to train, evaluate, and save a logistic regression model with [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) that predicts whether or not a tip is paid for a trip in the NYC taxi trip and fare dataset.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-328">The code in this section shows how to train, evaluate, and save a logistic regression model with [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) that predicts whether or not a tip is paid for a trip in the NYC taxi trip and fare dataset.</span></span> <span data-ttu-id="aeaf1-329">The model is trained using cross validation (CV) and hyperparameter sweeping implemented with the MLlib CrossValidator pipeline function for CV with parameter sweep.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-329">The model is trained using cross validation (CV) and hyperparameter sweeping implemented with the MLlib CrossValidator pipeline function for CV with parameter sweep.</span></span>   

> [!NOTE]
> <span data-ttu-id="aeaf1-330">The execution of this MLlib CV code can take several minutes.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-330">The execution of this MLlib CV code can take several minutes.</span></span>
> 
> 

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.ml.classification import LogisticRegression
    from pyspark.ml import Pipeline
    from pyspark.ml.evaluation import BinaryClassificationEvaluator
    from pyspark.ml.tuning import CrossValidator, ParamGridBuilder
    from sklearn.metrics import roc_curve,auc

    # DEFINE ALGORITHM / MODEL
    lr = LogisticRegression()

    # DEFINE GRID PARAMETERS
    paramGrid = ParamGridBuilder().addGrid(lr.regParam, (0.01, 0.1))\
                                  .addGrid(lr.maxIter, (5, 10))\
                                  .addGrid(lr.tol, (1e-4, 1e-5))\
                                  .addGrid(lr.elasticNetParam, (0.25,0.75))\
                                  .build()

    # DEFINE CV WITH PARAMETER SWEEP
    cv = CrossValidator(estimator= lr,
                        estimatorParamMaps=paramGrid,
                        evaluator=BinaryClassificationEvaluator(),
                        numFolds=3)

    # CONVERT TO DATA-FRAME: THIS DOES NOT RUN ON RDDs
    trainDataFrame = sqlContext.createDataFrame(oneHotTRAINbinary, ["features", "label"])

    # TRAIN WITH CROSS-VALIDATION
    cv_model = cv.fit(trainDataFrame)


    ## PREDICT AND EVALUATE ON TEST DATA-SET

    # USE TEST DATASET FOR PREDICTION
    testDataFrame = sqlContext.createDataFrame(oneHotTESTbinary, ["features", "label"])
    test_predictions = cv_model.transform(testDataFrame)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds";

<span data-ttu-id="aeaf1-331">**OUTPUT**</span><span class="sxs-lookup"><span data-stu-id="aeaf1-331">**OUTPUT**</span></span>

<span data-ttu-id="aeaf1-332">Time taken to execute above cell: 107.98 seconds</span><span class="sxs-lookup"><span data-stu-id="aeaf1-332">Time taken to execute above cell: 107.98 seconds</span></span>

<span data-ttu-id="aeaf1-333">**Plot the ROC curve.**</span><span class="sxs-lookup"><span data-stu-id="aeaf1-333">**Plot the ROC curve.**</span></span>

<span data-ttu-id="aeaf1-334">The *predictionAndLabelsDF* is registered as a table, *tmp_results*, in the previous cell.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-334">The *predictionAndLabelsDF* is registered as a table, *tmp_results*, in the previous cell.</span></span> <span data-ttu-id="aeaf1-335">*tmp_results* can be used to do queries and output results into the sqlResults data-frame for plotting.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-335">*tmp_results* can be used to do queries and output results into the sqlResults data-frame for plotting.</span></span> <span data-ttu-id="aeaf1-336">Here is the code.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-336">Here is the code.</span></span>

    # QUERY RESULTS
    %%sql -q -o sqlResults
    SELECT label, prediction, probability from tmp_results

<span data-ttu-id="aeaf1-337">Here is the code to plot the ROC curve.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-337">Here is the code to plot the ROC curve.</span></span>

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER AND IMPORT LIBRARIES 
    %%local
    from sklearn.metrics import roc_curve,auc

    # ROC CURVE
    prob = [x["values"][1] for x in sqlResults["probability"]]
    fpr, tpr, thresholds = roc_curve(sqlResults['label'], prob, pos_label=1);
    roc_auc = auc(fpr, tpr)

    #PLOT
    plt.figure(figsize=(5,5))
    plt.plot(fpr, tpr, label='ROC curve (area = %0.2f)' % roc_auc)
    plt.plot([0, 1], [0, 1], 'k--')
    plt.xlim([0.0, 1.0])
    plt.ylim([0.0, 1.05])
    plt.xlabel('False Positive Rate')
    plt.ylabel('True Positive Rate')
    plt.title('ROC Curve')
    plt.legend(loc="lower right")
    plt.show()


<span data-ttu-id="aeaf1-338">**OUTPUT**</span><span class="sxs-lookup"><span data-stu-id="aeaf1-338">**OUTPUT**</span></span>

![Logistic regression ROC curve using MLlib's CrossValidator](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-spark-advanced-data-exploration-modeling/mllib-crossvalidator-roc-curve.png)

### <a name="random-forest-classification"></a><span data-ttu-id="aeaf1-340">Random forest classification</span><span class="sxs-lookup"><span data-stu-id="aeaf1-340">Random forest classification</span></span>
<span data-ttu-id="aeaf1-341">The code in this section shows how to train, evaluate, and save a random forest regression that predicts whether or not a tip is paid for a trip in the NYC taxi trip and fare dataset.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-341">The code in this section shows how to train, evaluate, and save a random forest regression that predicts whether or not a tip is paid for a trip in the NYC taxi trip and fare dataset.</span></span>

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import RandomForest, RandomForestModel
    from pyspark.mllib.util import MLUtils
    from pyspark.mllib.evaluation import BinaryClassificationMetrics
    from pyspark.mllib.evaluation import MulticlassMetrics

    # SPECIFY NUMBER OF CATEGORIES FOR CATEGORICAL FEATURES. FEATURE #0 HAS 2 CATEGORIES, FEATURE #2 HAS 2 CATEGORIES, AND SO ON
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}

    # TRAIN RANDOMFOREST MODEL
    rfModel = RandomForest.trainClassifier(indexedTRAINbinary, numClasses=2, 
                                           categoricalFeaturesInfo=categoricalFeaturesInfo,
                                           numTrees=25, featureSubsetStrategy="auto",
                                           impurity='gini', maxDepth=5, maxBins=32)
    ## UN-COMMENT IF YOU WANT TO PRING TREES
    #print('Learned classification forest model:')
    #print(rfModel.toDebugString())

    # PREDICT ON TEST DATA AND EVALUATE
    predictions = rfModel.predict(indexedTESTbinary.map(lambda x: x.features))
    predictionAndLabels = indexedTESTbinary.map(lambda lp: lp.label).zip(predictions)

    # AREA UNDER ROC CURVE
    metrics = BinaryClassificationMetrics(predictionAndLabels)
    print("Area under ROC = %s" % metrics.areaUnderROC)

    # PERSIST MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    rfclassificationfilename = "RandomForestClassification_" + datestamp;
    dirfilename = modelDir + rfclassificationfilename;

    rfModel.save(sc, dirfilename);

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="aeaf1-342">**OUTPUT**</span><span class="sxs-lookup"><span data-stu-id="aeaf1-342">**OUTPUT**</span></span>

<span data-ttu-id="aeaf1-343">Area under ROC = 0.985336538462</span><span class="sxs-lookup"><span data-stu-id="aeaf1-343">Area under ROC = 0.985336538462</span></span>

<span data-ttu-id="aeaf1-344">Time taken to execute above cell: 26.72 seconds</span><span class="sxs-lookup"><span data-stu-id="aeaf1-344">Time taken to execute above cell: 26.72 seconds</span></span>

### <a name="gradient-boosting-trees-classification"></a><span data-ttu-id="aeaf1-345">Gradient boosting trees classification</span><span class="sxs-lookup"><span data-stu-id="aeaf1-345">Gradient boosting trees classification</span></span>
<span data-ttu-id="aeaf1-346">The code in this section shows how to train, evaluate, and save a gradient boosting trees model that predicts whether or not a tip is paid for a trip in the NYC taxi trip and fare dataset.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-346">The code in this section shows how to train, evaluate, and save a gradient boosting trees model that predicts whether or not a tip is paid for a trip in the NYC taxi trip and fare dataset.</span></span>

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel

    # SPECIFY NUMBER OF CATEGORIES FOR CATEGORICAL FEATURES. FEATURE #0 HAS 2 CATEGORIES, FEATURE #2 HAS 2 CATEGORIES, AND SO ON
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}

    gbtModel = GradientBoostedTrees.trainClassifier(indexedTRAINbinary, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                                    numIterations=10)
    ## UNCOMMENT IF YOU WANT TO PRINT TREE DETAILS
    #print('Learned classification GBT model:')
    #print(bgtModel.toDebugString())

    # PREDICT ON TEST DATA AND EVALUATE
    predictions = gbtModel.predict(indexedTESTbinary.map(lambda x: x.features))
    predictionAndLabels = indexedTESTbinary.map(lambda lp: lp.label).zip(predictions)

    # Area under ROC curve
    metrics = BinaryClassificationMetrics(predictionAndLabels)
    print("Area under ROC = %s" % metrics.areaUnderROC)

    # PERSIST MODEL IN A BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btclassificationfilename = "GradientBoostingTreeClassification_" + datestamp;
    dirfilename = modelDir + btclassificationfilename;

    gbtModel.save(sc, dirfilename)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="aeaf1-347">**OUTPUT**</span><span class="sxs-lookup"><span data-stu-id="aeaf1-347">**OUTPUT**</span></span>

<span data-ttu-id="aeaf1-348">Area under ROC = 0.985336538462</span><span class="sxs-lookup"><span data-stu-id="aeaf1-348">Area under ROC = 0.985336538462</span></span>

<span data-ttu-id="aeaf1-349">Time taken to execute above cell: 28.13 seconds</span><span class="sxs-lookup"><span data-stu-id="aeaf1-349">Time taken to execute above cell: 28.13 seconds</span></span>

## <a name="predict-tip-amount-with-regression-models-not-using-cv"></a><span data-ttu-id="aeaf1-350">Predict tip amount with regression models (not using CV)</span><span class="sxs-lookup"><span data-stu-id="aeaf1-350">Predict tip amount with regression models (not using CV)</span></span>
<span data-ttu-id="aeaf1-351">This section shows how use three models for the regression task: predict the tip amount paid for a taxi trip based on other tip features.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-351">This section shows how use three models for the regression task: predict the tip amount paid for a taxi trip based on other tip features.</span></span> <span data-ttu-id="aeaf1-352">The models presented are:</span><span class="sxs-lookup"><span data-stu-id="aeaf1-352">The models presented are:</span></span>

* <span data-ttu-id="aeaf1-353">Regularized linear regression</span><span class="sxs-lookup"><span data-stu-id="aeaf1-353">Regularized linear regression</span></span>
* <span data-ttu-id="aeaf1-354">Random forest</span><span class="sxs-lookup"><span data-stu-id="aeaf1-354">Random forest</span></span>
* <span data-ttu-id="aeaf1-355">Gradient Boosting Trees</span><span class="sxs-lookup"><span data-stu-id="aeaf1-355">Gradient Boosting Trees</span></span>

<span data-ttu-id="aeaf1-356">These models were described in the introduction.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-356">These models were described in the introduction.</span></span> <span data-ttu-id="aeaf1-357">Each model building code section is split into steps:</span><span class="sxs-lookup"><span data-stu-id="aeaf1-357">Each model building code section is split into steps:</span></span> 

1. <span data-ttu-id="aeaf1-358">**Model training** data with one parameter set</span><span class="sxs-lookup"><span data-stu-id="aeaf1-358">**Model training** data with one parameter set</span></span>
2. <span data-ttu-id="aeaf1-359">**Model evaluation** on a test data set with metrics</span><span class="sxs-lookup"><span data-stu-id="aeaf1-359">**Model evaluation** on a test data set with metrics</span></span>
3. <span data-ttu-id="aeaf1-360">**Saving model** in blob for future consumption</span><span class="sxs-lookup"><span data-stu-id="aeaf1-360">**Saving model** in blob for future consumption</span></span>   

> <span data-ttu-id="aeaf1-361">AZURE NOTE: Cross-validation is not used with the three regression models in this section, since this was shown in detail for the logistic regression models.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-361">AZURE NOTE: Cross-validation is not used with the three regression models in this section, since this was shown in detail for the logistic regression models.</span></span> <span data-ttu-id="aeaf1-362">An example showing how to use CV with Elastic Net for linear regression is provided in the Appendix of this topic.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-362">An example showing how to use CV with Elastic Net for linear regression is provided in the Appendix of this topic.</span></span>
> 
> <span data-ttu-id="aeaf1-363">AZURE NOTE: In our experience, there can be issues with convergence of LinearRegressionWithSGD models, and parameters need to be changed/optimized carefully for obtaining a valid model.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-363">AZURE NOTE: In our experience, there can be issues with convergence of LinearRegressionWithSGD models, and parameters need to be changed/optimized carefully for obtaining a valid model.</span></span> <span data-ttu-id="aeaf1-364">Scaling of variables significantly helps with convergence.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-364">Scaling of variables significantly helps with convergence.</span></span> <span data-ttu-id="aeaf1-365">Elastic net regression, shown in the Appendix to this topic, can also be used instead of LinearRegressionWithSGD.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-365">Elastic net regression, shown in the Appendix to this topic, can also be used instead of LinearRegressionWithSGD.</span></span>
> 
> 

### <a name="linear-regression-with-sgd"></a><span data-ttu-id="aeaf1-366">Linear regression with SGD</span><span class="sxs-lookup"><span data-stu-id="aeaf1-366">Linear regression with SGD</span></span>
<span data-ttu-id="aeaf1-367">The code in this section shows how to use scaled features to train a linear regression that uses stochastic gradient descent (SGD) for optimization, and how to score, evaluate, and save the model in Azure Blob Storage (WASB).</span><span class="sxs-lookup"><span data-stu-id="aeaf1-367">The code in this section shows how to use scaled features to train a linear regression that uses stochastic gradient descent (SGD) for optimization, and how to score, evaluate, and save the model in Azure Blob Storage (WASB).</span></span>

> [!TIP]
> <span data-ttu-id="aeaf1-368">In our experience, there can be issues with the convergence of LinearRegressionWithSGD models, and parameters need to be changed/optimized carefully for obtaining a valid model.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-368">In our experience, there can be issues with the convergence of LinearRegressionWithSGD models, and parameters need to be changed/optimized carefully for obtaining a valid model.</span></span> <span data-ttu-id="aeaf1-369">Scaling of variables significantly helps with convergence.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-369">Scaling of variables significantly helps with convergence.</span></span>
> 
> 

    # LINEAR REGRESSION WITH SGD 

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD LIBRARIES
    from pyspark.mllib.regression import LabeledPoint, LinearRegressionWithSGD, LinearRegressionModel
    from pyspark.mllib.evaluation import RegressionMetrics
    from scipy import stats

    # USE SCALED FEATURES TO TRAIN MODEL
    linearModel = LinearRegressionWithSGD.train(oneHotTRAINregScaled, iterations=100, step = 0.1, regType='l2', regParam=0.1, intercept = True)

    # PRINT COEFFICIENTS AND INTERCEPT OF THE MODEL
    # NOTE: There are 20 coefficient terms for the 10 features, 
    #       and the different categories for features: vendorVec (2), rateVec, paymentVec (6), TrafficTimeBinsVec (4)
    print("Coefficients: " + str(linearModel.weights))
    print("Intercept: " + str(linearModel.intercept))

    # SCORE ON SCALED TEST DATA-SET & EVALUATE
    predictionAndLabels = oneHotTESTregScaled.map(lambda lp: (float(linearModel.predict(lp.features)), lp.label))
    testMetrics = RegressionMetrics(predictionAndLabels)

    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # SAVE MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    linearregressionfilename = "LinearRegressionWithSGD_" + datestamp;
    dirfilename = modelDir + linearregressionfilename;

    linearModel.save(sc, dirfilename)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="aeaf1-370">**OUTPUT**</span><span class="sxs-lookup"><span data-stu-id="aeaf1-370">**OUTPUT**</span></span>

<span data-ttu-id="aeaf1-371">Coefficients: [0.0141707753435, -0.0252930927087, -0.0231442517137, 0.247070902996, 0.312544147152, 0.360296120645, 0.0122079566092, -0.00456498588241, -0.0898228505177, 0.0714046248793, 0.102171263868, 0.100022455632, -0.00289545676449, -0.00791124681938, 0.54396316518, -0.536293513569, 0.0119076553369, -0.0173039244582, 0.0119632796147, 0.00146764882502]</span><span class="sxs-lookup"><span data-stu-id="aeaf1-371">Coefficients: [0.0141707753435, -0.0252930927087, -0.0231442517137, 0.247070902996, 0.312544147152, 0.360296120645, 0.0122079566092, -0.00456498588241, -0.0898228505177, 0.0714046248793, 0.102171263868, 0.100022455632, -0.00289545676449, -0.00791124681938, 0.54396316518, -0.536293513569, 0.0119076553369, -0.0173039244582, 0.0119632796147, 0.00146764882502]</span></span>

<span data-ttu-id="aeaf1-372">Intercept: 0.854507624459</span><span class="sxs-lookup"><span data-stu-id="aeaf1-372">Intercept: 0.854507624459</span></span>

<span data-ttu-id="aeaf1-373">RMSE = 1.23485131376</span><span class="sxs-lookup"><span data-stu-id="aeaf1-373">RMSE = 1.23485131376</span></span>

<span data-ttu-id="aeaf1-374">R-sqr = 0.597963951127</span><span class="sxs-lookup"><span data-stu-id="aeaf1-374">R-sqr = 0.597963951127</span></span>

<span data-ttu-id="aeaf1-375">Time taken to execute above cell: 38.62 seconds</span><span class="sxs-lookup"><span data-stu-id="aeaf1-375">Time taken to execute above cell: 38.62 seconds</span></span>

### <a name="random-forest-regression"></a><span data-ttu-id="aeaf1-376">Random Forest regression</span><span class="sxs-lookup"><span data-stu-id="aeaf1-376">Random Forest regression</span></span>
<span data-ttu-id="aeaf1-377">The code in this section shows how to train, evaluate, and save a random forest model that predicts tip amount for the NYC taxi trip data.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-377">The code in this section shows how to train, evaluate, and save a random forest model that predicts tip amount for the NYC taxi trip data.</span></span>   

> [!NOTE]
> <span data-ttu-id="aeaf1-378">Cross-validation with parameter sweeping using custom code is provided in the appendix.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-378">Cross-validation with parameter sweeping using custom code is provided in the appendix.</span></span>
> 
> 

    #PREDICT TIP AMOUNTS USING RANDOM FOREST

    # RECORD START TIME
    timestart= datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import RandomForest, RandomForestModel
    from pyspark.mllib.util import MLUtils
    from pyspark.mllib.evaluation import RegressionMetrics


    # TRAIN MODEL
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}
    rfModel = RandomForest.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                        numTrees=25, featureSubsetStrategy="auto",
                                        impurity='variance', maxDepth=10, maxBins=32)
    # UN-COMMENT IF YOU WANT TO PRING TREES
    #print('Learned classification forest model:')
    #print(rfModel.toDebugString())

    # PREDICT AND EVALUATE ON TEST DATA-SET
    predictions = rfModel.predict(indexedTESTreg.map(lambda x: x.features))
    predictionAndLabels = oneHotTESTreg.map(lambda lp: lp.label).zip(predictions)

    testMetrics = RegressionMetrics(predictionAndLabels)
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # SAVE MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    rfregressionfilename = "RandomForestRegression_" + datestamp;
    dirfilename = modelDir + rfregressionfilename;

    rfModel.save(sc, dirfilename);

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="aeaf1-379">**OUTPUT**</span><span class="sxs-lookup"><span data-stu-id="aeaf1-379">**OUTPUT**</span></span>

<span data-ttu-id="aeaf1-380">RMSE = 0.931981967875</span><span class="sxs-lookup"><span data-stu-id="aeaf1-380">RMSE = 0.931981967875</span></span>

<span data-ttu-id="aeaf1-381">R-sqr = 0.733445485802</span><span class="sxs-lookup"><span data-stu-id="aeaf1-381">R-sqr = 0.733445485802</span></span>

<span data-ttu-id="aeaf1-382">Time taken to execute above cell: 25.98 seconds</span><span class="sxs-lookup"><span data-stu-id="aeaf1-382">Time taken to execute above cell: 25.98 seconds</span></span>

### <a name="gradient-boosting-trees-regression"></a><span data-ttu-id="aeaf1-383">Gradient boosting trees regression</span><span class="sxs-lookup"><span data-stu-id="aeaf1-383">Gradient boosting trees regression</span></span>
<span data-ttu-id="aeaf1-384">The code in this section shows how to train, evaluate, and save a gradient boosting trees model that predicts tip amount for the NYC taxi trip data.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-384">The code in this section shows how to train, evaluate, and save a gradient boosting trees model that predicts tip amount for the NYC taxi trip data.</span></span>

<span data-ttu-id="aeaf1-385">\*\*Train and evaluate \*\*</span><span class="sxs-lookup"><span data-stu-id="aeaf1-385">\*\*Train and evaluate \*\*</span></span>

    #PREDICT TIP AMOUNTS USING GRADIENT BOOSTING TREES

    # RECORD START TIME
    timestart= datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel
    from pyspark.mllib.util import MLUtils

    # TRAIN MODEL
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}
    gbtModel = GradientBoostedTrees.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo, 
                                                    numIterations=10, maxBins=32, maxDepth = 4, learningRate=0.1)

    # EVALUATE A TEST DATA-SET
    predictions = gbtModel.predict(indexedTESTreg.map(lambda x: x.features))
    predictionAndLabels = indexedTESTreg.map(lambda lp: lp.label).zip(predictions)

    testMetrics = RegressionMetrics(predictionAndLabels)
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # PLOT SCATTER-PLOT BETWEEN ACTUAL AND PREDICTED TIP VALUES
    test_predictions= sqlContext.createDataFrame(predictionAndLabels)
    test_predictions_pddf = test_predictions.toPandas()

    # SAVE MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btregressionfilename = "GradientBoostingTreeRegression_" + datestamp;
    dirfilename = modelDir + btregressionfilename;
    gbtModel.save(sc, dirfilename)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="aeaf1-386">**OUTPUT**</span><span class="sxs-lookup"><span data-stu-id="aeaf1-386">**OUTPUT**</span></span>

<span data-ttu-id="aeaf1-387">RMSE = 0.928172197114</span><span class="sxs-lookup"><span data-stu-id="aeaf1-387">RMSE = 0.928172197114</span></span>

<span data-ttu-id="aeaf1-388">R-sqr = 0.732680354389</span><span class="sxs-lookup"><span data-stu-id="aeaf1-388">R-sqr = 0.732680354389</span></span>

<span data-ttu-id="aeaf1-389">Time taken to execute above cell: 20.9 seconds</span><span class="sxs-lookup"><span data-stu-id="aeaf1-389">Time taken to execute above cell: 20.9 seconds</span></span>

<span data-ttu-id="aeaf1-390">**Plot**</span><span class="sxs-lookup"><span data-stu-id="aeaf1-390">**Plot**</span></span>

<span data-ttu-id="aeaf1-391">*tmp_results* is registered as a Hive table in the previous cell.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-391">*tmp_results* is registered as a Hive table in the previous cell.</span></span> <span data-ttu-id="aeaf1-392">Results from the table are output into the *sqlResults* data-frame for plotting.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-392">Results from the table are output into the *sqlResults* data-frame for plotting.</span></span> <span data-ttu-id="aeaf1-393">Here is the code</span><span class="sxs-lookup"><span data-stu-id="aeaf1-393">Here is the code</span></span>

    # PLOT SCATTER-PLOT BETWEEN ACTUAL AND PREDICTED TIP VALUES

    # SELECT RESULTS
    %%sql -q -o sqlResults
    SELECT * from tmp_results


<span data-ttu-id="aeaf1-394">Here is the code to plot the data using the Jupyter server.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-394">Here is the code to plot the data using the Jupyter server.</span></span>

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    import numpy as np

    # PLOT
    ax = sqlResults.plot(kind='scatter', figsize = (6,6), x='_1', y='_2', color='blue', alpha = 0.25, label='Actual vs. predicted');
    fit = np.polyfit(sqlResults['_1'], sqlResults['_2'], deg=1)
    ax.set_title('Actual vs. Predicted Tip Amounts ($)')
    ax.set_xlabel("Actual")
    ax.set_ylabel("Predicted")
    ax.plot(sqlResults['_1'], fit[0] * sqlResults['_1'] + fit[1], color='magenta')
    plt.axis([-1, 15, -1, 15])
    plt.show(ax)

![Actual-vs-predicted-tip-amounts](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-spark-advanced-data-exploration-modeling/actual-vs-predicted-tips.png)

## <a name="appendix-additional-regression-tasks-using-cross-validation-with-parameter-sweeps"></a><span data-ttu-id="aeaf1-396">Appendix: Additional regression tasks using cross validation with parameter sweeps</span><span class="sxs-lookup"><span data-stu-id="aeaf1-396">Appendix: Additional regression tasks using cross validation with parameter sweeps</span></span>
<span data-ttu-id="aeaf1-397">This appendix contains code showing how to do CV using Elastic net for linear regression and how to do CV with parameter sweep using custom code for random forest regression.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-397">This appendix contains code showing how to do CV using Elastic net for linear regression and how to do CV with parameter sweep using custom code for random forest regression.</span></span>

### <a name="cross-validation-using-elastic-net-for-linear-regression"></a><span data-ttu-id="aeaf1-398">Cross validation using Elastic net for linear regression</span><span class="sxs-lookup"><span data-stu-id="aeaf1-398">Cross validation using Elastic net for linear regression</span></span>
<span data-ttu-id="aeaf1-399">The code in this section shows how to do cross validation using Elastic net for linear regression and how to evaluate the model against test data.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-399">The code in this section shows how to do cross validation using Elastic net for linear regression and how to evaluate the model against test data.</span></span>

    ###  CV USING ELASTIC NET FOR LINEAR REGRESSION

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.ml.regression import LinearRegression
    from pyspark.ml import Pipeline
    from pyspark.ml.evaluation import RegressionEvaluator
    from pyspark.ml.tuning import CrossValidator, ParamGridBuilder

    # DEFINE ALGORITHM/MODEL
    lr = LinearRegression()

    # DEFINE GRID PARAMETERS
    paramGrid = ParamGridBuilder().addGrid(lr.regParam, (0.01, 0.1))\
                                  .addGrid(lr.maxIter, (5, 10))\
                                  .addGrid(lr.tol, (1e-4, 1e-5))\
                                  .addGrid(lr.elasticNetParam, (0.25,0.75))\
                                  .build() 

    # DEFINE PIPELINE 
    # SIMPLY THE MODEL HERE, WITHOUT TRANSFORMATIONS
    pipeline = Pipeline(stages=[lr])

    # DEFINE CV WITH PARAMETER SWEEP
    cv = CrossValidator(estimator= lr,
                        estimatorParamMaps=paramGrid,
                        evaluator=RegressionEvaluator(),
                        numFolds=3)

    # CONVERT TO DATA FRAME, AS CROSSVALIDATOR WON'T RUN ON RDDS
    trainDataFrame = sqlContext.createDataFrame(oneHotTRAINreg, ["features", "label"])

    # TRAIN WITH CROSS-VALIDATION
    cv_model = cv.fit(trainDataFrame)


    # EVALUATE MODEL ON TEST SET
    testDataFrame = sqlContext.createDataFrame(oneHotTESTreg, ["features", "label"])

    # MAKE PREDICTIONS ON TEST DOCUMENTS
    # cvModel uses the best model found (lrModel).
    predictionAndLabels = cv_model.transform(testDataFrame)

    # CONVERT TO DF AND SAVE REGISER DF AS TABLE
    predictionAndLabels.registerTempTable("tmp_results");

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="aeaf1-400">**OUTPUT**</span><span class="sxs-lookup"><span data-stu-id="aeaf1-400">**OUTPUT**</span></span>

<span data-ttu-id="aeaf1-401">Time taken to execute above cell: 161.21  seconds</span><span class="sxs-lookup"><span data-stu-id="aeaf1-401">Time taken to execute above cell: 161.21  seconds</span></span>

<span data-ttu-id="aeaf1-402">**Evaluate with R-SQR metric**</span><span class="sxs-lookup"><span data-stu-id="aeaf1-402">**Evaluate with R-SQR metric**</span></span>

<span data-ttu-id="aeaf1-403">*tmp_results* is registered as a Hive table in the previous cell.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-403">*tmp_results* is registered as a Hive table in the previous cell.</span></span> <span data-ttu-id="aeaf1-404">Results from the table are output into the *sqlResults* data-frame for plotting.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-404">Results from the table are output into the *sqlResults* data-frame for plotting.</span></span> <span data-ttu-id="aeaf1-405">Here is the code</span><span class="sxs-lookup"><span data-stu-id="aeaf1-405">Here is the code</span></span>

    # SELECT RESULTS
    %%sql -q -o sqlResults
    SELECT label,prediction from tmp_results


<span data-ttu-id="aeaf1-406">Here is the code to calculate R-sqr.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-406">Here is the code to calculate R-sqr.</span></span>

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    from scipy import stats

    #R-SQR TEST METRIC
    corstats = stats.linregress(sqlResults['label'],sqlResults['prediction'])
    r2 = (corstats[2]*corstats[2])
    print("R-sqr = %s" % r2)


<span data-ttu-id="aeaf1-407">**OUTPUT**</span><span class="sxs-lookup"><span data-stu-id="aeaf1-407">**OUTPUT**</span></span>

<span data-ttu-id="aeaf1-408">R-sqr = 0.619184907088</span><span class="sxs-lookup"><span data-stu-id="aeaf1-408">R-sqr = 0.619184907088</span></span>

### <a name="cross-validation-with-parameter-sweep-using-custom-code-for-random-forest-regression"></a><span data-ttu-id="aeaf1-409">Cross validation with parameter sweep using custom code for random forest regression</span><span class="sxs-lookup"><span data-stu-id="aeaf1-409">Cross validation with parameter sweep using custom code for random forest regression</span></span>
<span data-ttu-id="aeaf1-410">The code in this section shows how to do cross validation with parameter sweep using custom code for random forest regression and how to evaluate the model against test data.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-410">The code in this section shows how to do cross validation with parameter sweep using custom code for random forest regression and how to evaluate the model against test data.</span></span>

    # RECORD START TIME
    timestart= datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    # GET ACCURARY FOR HYPERPARAMETERS BASED ON CROSS-VALIDATION IN TRAINING DATA-SET
    from pyspark.mllib.tree import RandomForest, RandomForestModel
    from pyspark.mllib.util import MLUtils
    from pyspark.mllib.evaluation import RegressionMetrics
    from sklearn.grid_search import ParameterGrid

    ## CREATE PARAMETER GRID
    grid = [{'maxDepth': [5,10], 'numTrees': [25,50]}]
    paramGrid = list(ParameterGrid(grid))

    ## SPECIFY LEVELS OF CATEGORICAL VARIBLES
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}

    # SPECIFY NUMFOLDS AND ARRAY TO HOLD METRICS
    nFolds = 3;
    numModels = len(paramGrid)
    h = 1.0 / nFolds;
    metricSum = np.zeros(numModels);

    for i in range(nFolds):
        # Create training and x-validation sets
        validateLB = i * h
        validateUB = (i + 1) * h
        condition = (trainData["rand"] >= validateLB) & (trainData["rand"] < validateUB)
        validation = trainData.filter(condition)
        # Create labeled points from data-frames
        if i > 0:
            trainCVLabPt.unpersist()
            validationLabPt.unpersist()
        trainCV = trainData.filter(~condition)
        trainCVLabPt = trainCV.map(parseRowIndexingRegression)
        trainCVLabPt.cache()
        validationLabPt = validation.map(parseRowIndexingRegression)
        validationLabPt.cache()
        # For parameter sets compute metrics from x-validation
        for j in range(numModels):
            maxD = paramGrid[j]['maxDepth']
            numT = paramGrid[j]['numTrees']
            # Train logistic regression model with hypermarameter set
            rfModel = RandomForest.trainRegressor(trainCVLabPt, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                        numTrees=numT, featureSubsetStrategy="auto",
                                        impurity='variance', maxDepth=maxD, maxBins=32)
            predictions = rfModel.predict(validationLabPt.map(lambda x: x.features))
            predictionAndLabels = validationLabPt.map(lambda lp: lp.label).zip(predictions)
            # Use ROC-AUC as accuracy metrics
            validMetrics = RegressionMetrics(predictionAndLabels)
            metric = validMetrics.rootMeanSquaredError
            metricSum[j] += metric

    avgAcc = metricSum/nFolds;
    bestParam = paramGrid[np.argmin(avgAcc)];

    # UNPERSIST OBJECTS
    trainCVLabPt.unpersist()
    validationLabPt.unpersist()

    ## TRAIN FINAL MODL WIHT BEST PARAMETERS
    rfModel = RandomForest.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                        numTrees=bestParam['numTrees'], featureSubsetStrategy="auto",
                                        impurity='variance', maxDepth=bestParam['maxDepth'], maxBins=32)

    # EVALUATE MODEL ON TEST DATA
    predictions = rfModel.predict(indexedTESTreg.map(lambda x: x.features))
    predictionAndLabels = indexedTESTreg.map(lambda lp: lp.label).zip(predictions)

    #PRINT TEST METRICS
    testMetrics = RegressionMetrics(predictionAndLabels)
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="aeaf1-411">**OUTPUT**</span><span class="sxs-lookup"><span data-stu-id="aeaf1-411">**OUTPUT**</span></span>

<span data-ttu-id="aeaf1-412">RMSE = 0.906972198262</span><span class="sxs-lookup"><span data-stu-id="aeaf1-412">RMSE = 0.906972198262</span></span>

<span data-ttu-id="aeaf1-413">R-sqr = 0.740751197012</span><span class="sxs-lookup"><span data-stu-id="aeaf1-413">R-sqr = 0.740751197012</span></span>

<span data-ttu-id="aeaf1-414">Time taken to execute above cell: 69.17 seconds</span><span class="sxs-lookup"><span data-stu-id="aeaf1-414">Time taken to execute above cell: 69.17 seconds</span></span>

### <a name="clean-up-objects-from-memory-and-print-model-locations"></a><span data-ttu-id="aeaf1-415">Clean up objects from memory and print model locations</span><span class="sxs-lookup"><span data-stu-id="aeaf1-415">Clean up objects from memory and print model locations</span></span>
<span data-ttu-id="aeaf1-416">Use `unpersist()` to delete objects cached in memory.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-416">Use `unpersist()` to delete objects cached in memory.</span></span>

    # UNPERSIST OBJECTS CACHED IN MEMORY

    # REMOVE ORIGINAL DFs
    taxi_df_train_cleaned.unpersist()
    taxi_df_train_with_newFeatures.unpersist()
    trainData.unpersist()
    trainData.unpersist()

    # FOR BINARY CLASSIFICATION TRAINING AND TESTING
    indexedTRAINbinary.unpersist()
    indexedTESTbinary.unpersist()
    oneHotTRAINbinary.unpersist()
    oneHotTESTbinary.unpersist()

    # FOR REGRESSION TRAINING AND TESTING
    indexedTRAINreg.unpersist()
    indexedTESTreg.unpersist()
    oneHotTRAINreg.unpersist()
    oneHotTESTreg.unpersist()

    # SCALED FEATURES
    oneHotTRAINregScaled.unpersist()
    oneHotTESTregScaled.unpersist()


<span data-ttu-id="aeaf1-417">**OUTPUT**</span><span class="sxs-lookup"><span data-stu-id="aeaf1-417">**OUTPUT**</span></span>

<span data-ttu-id="aeaf1-418">PythonRDD[122] at RDD at PythonRDD.scala: 43</span><span class="sxs-lookup"><span data-stu-id="aeaf1-418">PythonRDD[122] at RDD at PythonRDD.scala: 43</span></span>

<span data-ttu-id="aeaf1-419">\*\*Printout path to model files to be used in the consumption notebook.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-419">\*\*Printout path to model files to be used in the consumption notebook.</span></span> <span data-ttu-id="aeaf1-420">\*\* To consume and score an independent data-set, you need to copy and paste these file names in the "Consumption notebook".</span><span class="sxs-lookup"><span data-stu-id="aeaf1-420">\*\* To consume and score an independent data-set, you need to copy and paste these file names in the "Consumption notebook".</span></span>

    # PRINT MODEL FILE LOCATIONS FOR CONSUMPTION
    print "logisticRegFileLoc = modelDir + \"" + logisticregressionfilename + "\"";
    print "linearRegFileLoc = modelDir + \"" + linearregressionfilename + "\"";
    print "randomForestClassificationFileLoc = modelDir + \"" + rfclassificationfilename + "\"";
    print "randomForestRegFileLoc = modelDir + \"" + rfregressionfilename + "\"";
    print "BoostedTreeClassificationFileLoc = modelDir + \"" + btclassificationfilename + "\"";
    print "BoostedTreeRegressionFileLoc = modelDir + \"" + btregressionfilename + "\"";


<span data-ttu-id="aeaf1-421">**OUTPUT**</span><span class="sxs-lookup"><span data-stu-id="aeaf1-421">**OUTPUT**</span></span>

<span data-ttu-id="aeaf1-422">logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-05-0316_47_30.096528"</span><span class="sxs-lookup"><span data-stu-id="aeaf1-422">logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-05-0316_47_30.096528"</span></span>

<span data-ttu-id="aeaf1-423">linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-05-0316_51_28.433670"</span><span class="sxs-lookup"><span data-stu-id="aeaf1-423">linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-05-0316_51_28.433670"</span></span>

<span data-ttu-id="aeaf1-424">randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-05-0316_50_17.454440"</span><span class="sxs-lookup"><span data-stu-id="aeaf1-424">randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-05-0316_50_17.454440"</span></span>

<span data-ttu-id="aeaf1-425">randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-05-0316_51_57.331730"</span><span class="sxs-lookup"><span data-stu-id="aeaf1-425">randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-05-0316_51_57.331730"</span></span>

<span data-ttu-id="aeaf1-426">BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-05-0316_50_40.138809"</span><span class="sxs-lookup"><span data-stu-id="aeaf1-426">BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-05-0316_50_40.138809"</span></span>

<span data-ttu-id="aeaf1-427">BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-05-0316_52_18.827237"</span><span class="sxs-lookup"><span data-stu-id="aeaf1-427">BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-05-0316_52_18.827237"</span></span>

## <a name="whats-next"></a><span data-ttu-id="aeaf1-428">What's next?</span><span class="sxs-lookup"><span data-stu-id="aeaf1-428">What's next?</span></span>
<span data-ttu-id="aeaf1-429">Now that you have created regression and classification models with the Spark MlLib, you are ready to learn how to score and evaluate these models.</span><span class="sxs-lookup"><span data-stu-id="aeaf1-429">Now that you have created regression and classification models with the Spark MlLib, you are ready to learn how to score and evaluate these models.</span></span>

<span data-ttu-id="aeaf1-430">**Model consumption:** To learn how to score and evaluate the classification and regression models created in this topic, see [Score and evaluate Spark-built machine learning models](machine-learning-data-science-spark-model-consumption.md).</span><span class="sxs-lookup"><span data-stu-id="aeaf1-430">**Model consumption:** To learn how to score and evaluate the classification and regression models created in this topic, see [Score and evaluate Spark-built machine learning models](machine-learning-data-science-spark-model-consumption.md).</span></span>








