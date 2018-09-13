---
title: Data Science using Scala and Spark on Azure | Microsoft Docs
description: How to use Scala for supervised machine learning tasks with the Spark scalable MLlib and Spark ML packages on an Azure HDInsight Spark cluster.
services: machine-learning
documentationcenter: ''
author: deguhath
manager: cgronlun
editor: cgronlun
ms.assetid: a7c97153-583e-48fe-b301-365123db3780
ms.service: machine-learning
ms.component: team-data-science-process
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/13/2017
ms.author: deguhath
ms.openlocfilehash: 16e4af4dd7f5c2bd14d70cc28225dfc750ce3bea
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969339"
---
# <a name="data-science-using-scala-and-spark-on-azure"></a><span data-ttu-id="63609-103">Data Science using Scala and Spark on Azure</span><span class="sxs-lookup"><span data-stu-id="63609-103">Data Science using Scala and Spark on Azure</span></span>
<span data-ttu-id="63609-104">This article shows you how to use Scala for supervised machine learning tasks with the Spark scalable MLlib and Spark ML packages on an Azure HDInsight Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="63609-104">This article shows you how to use Scala for supervised machine learning tasks with the Spark scalable MLlib and Spark ML packages on an Azure HDInsight Spark cluster.</span></span> <span data-ttu-id="63609-105">It walks you through the tasks that constitute the [Data Science process](http://aka.ms/datascienceprocess): data ingestion and exploration, visualization, feature engineering, modeling, and model consumption.</span><span class="sxs-lookup"><span data-stu-id="63609-105">It walks you through the tasks that constitute the [Data Science process](http://aka.ms/datascienceprocess): data ingestion and exploration, visualization, feature engineering, modeling, and model consumption.</span></span> <span data-ttu-id="63609-106">The models in the article include logistic and linear regression, random forests, and gradient-boosted trees (GBTs), in addition to two common supervised machine learning tasks:</span><span class="sxs-lookup"><span data-stu-id="63609-106">The models in the article include logistic and linear regression, random forests, and gradient-boosted trees (GBTs), in addition to two common supervised machine learning tasks:</span></span>

* <span data-ttu-id="63609-107">Regression problem: Prediction of the tip amount ($) for a taxi trip</span><span class="sxs-lookup"><span data-stu-id="63609-107">Regression problem: Prediction of the tip amount ($) for a taxi trip</span></span>
* <span data-ttu-id="63609-108">Binary classification: Prediction of tip or no tip (1/0) for a taxi trip</span><span class="sxs-lookup"><span data-stu-id="63609-108">Binary classification: Prediction of tip or no tip (1/0) for a taxi trip</span></span>

<span data-ttu-id="63609-109">The modeling process requires training and evaluation on a test data set and relevant accuracy metrics.</span><span class="sxs-lookup"><span data-stu-id="63609-109">The modeling process requires training and evaluation on a test data set and relevant accuracy metrics.</span></span> <span data-ttu-id="63609-110">In this article, you can learn how to store these models in Azure Blob storage and how to score and evaluate their predictive performance.</span><span class="sxs-lookup"><span data-stu-id="63609-110">In this article, you can learn how to store these models in Azure Blob storage and how to score and evaluate their predictive performance.</span></span> <span data-ttu-id="63609-111">This article also covers the more advanced topics of how to optimize models by using cross-validation and hyper-parameter sweeping.</span><span class="sxs-lookup"><span data-stu-id="63609-111">This article also covers the more advanced topics of how to optimize models by using cross-validation and hyper-parameter sweeping.</span></span> <span data-ttu-id="63609-112">The data used is a sample of the 2013 NYC taxi trip and fare data set available on GitHub.</span><span class="sxs-lookup"><span data-stu-id="63609-112">The data used is a sample of the 2013 NYC taxi trip and fare data set available on GitHub.</span></span>

<span data-ttu-id="63609-113">[Scala](http://www.scala-lang.org/), a language based on the Java virtual machine, integrates object-oriented and functional language concepts.</span><span class="sxs-lookup"><span data-stu-id="63609-113">[Scala](http://www.scala-lang.org/), a language based on the Java virtual machine, integrates object-oriented and functional language concepts.</span></span> <span data-ttu-id="63609-114">It's a scalable language that is well suited to distributed processing in the cloud, and runs on Azure Spark clusters.</span><span class="sxs-lookup"><span data-stu-id="63609-114">It's a scalable language that is well suited to distributed processing in the cloud, and runs on Azure Spark clusters.</span></span>

<span data-ttu-id="63609-115">[Spark](http://spark.apache.org/) is an open-source parallel-processing framework that supports in-memory processing to boost the performance of big data analytics applications.</span><span class="sxs-lookup"><span data-stu-id="63609-115">[Spark](http://spark.apache.org/) is an open-source parallel-processing framework that supports in-memory processing to boost the performance of big data analytics applications.</span></span> <span data-ttu-id="63609-116">The Spark processing engine is built for speed, ease of use, and sophisticated analytics.</span><span class="sxs-lookup"><span data-stu-id="63609-116">The Spark processing engine is built for speed, ease of use, and sophisticated analytics.</span></span> <span data-ttu-id="63609-117">Spark's in-memory distributed computation capabilities make it a good choice for iterative algorithms in machine learning and graph computations.</span><span class="sxs-lookup"><span data-stu-id="63609-117">Spark's in-memory distributed computation capabilities make it a good choice for iterative algorithms in machine learning and graph computations.</span></span> <span data-ttu-id="63609-118">The [spark.ml](http://spark.apache.org/docs/latest/ml-guide.html) package provides a uniform set of high-level APIs built on top of data frames that can help you create and tune practical machine learning pipelines.</span><span class="sxs-lookup"><span data-stu-id="63609-118">The [spark.ml](http://spark.apache.org/docs/latest/ml-guide.html) package provides a uniform set of high-level APIs built on top of data frames that can help you create and tune practical machine learning pipelines.</span></span> <span data-ttu-id="63609-119">[MLlib](http://spark.apache.org/mllib/) is Spark's scalable machine learning library, which brings modeling capabilities to this distributed environment.</span><span class="sxs-lookup"><span data-stu-id="63609-119">[MLlib](http://spark.apache.org/mllib/) is Spark's scalable machine learning library, which brings modeling capabilities to this distributed environment.</span></span>

<span data-ttu-id="63609-120">[HDInsight Spark](../../hdinsight/spark/apache-spark-overview.md) is the Azure-hosted offering of open-source Spark.</span><span class="sxs-lookup"><span data-stu-id="63609-120">[HDInsight Spark](../../hdinsight/spark/apache-spark-overview.md) is the Azure-hosted offering of open-source Spark.</span></span> <span data-ttu-id="63609-121">It also includes support for Jupyter Scala notebooks on the Spark cluster, and can run Spark SQL interactive queries to transform, filter, and visualize data stored in Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="63609-121">It also includes support for Jupyter Scala notebooks on the Spark cluster, and can run Spark SQL interactive queries to transform, filter, and visualize data stored in Azure Blob storage.</span></span> <span data-ttu-id="63609-122">The Scala code snippets in this article that provide the solutions and show the relevant plots to visualize the data run in Jupyter notebooks installed on the Spark clusters.</span><span class="sxs-lookup"><span data-stu-id="63609-122">The Scala code snippets in this article that provide the solutions and show the relevant plots to visualize the data run in Jupyter notebooks installed on the Spark clusters.</span></span> <span data-ttu-id="63609-123">The modeling steps in these topics have code that shows you how to train, evaluate, save, and consume each type of model.</span><span class="sxs-lookup"><span data-stu-id="63609-123">The modeling steps in these topics have code that shows you how to train, evaluate, save, and consume each type of model.</span></span>

<span data-ttu-id="63609-124">The setup steps and code in this article are for Azure HDInsight 3.4 Spark 1.6.</span><span class="sxs-lookup"><span data-stu-id="63609-124">The setup steps and code in this article are for Azure HDInsight 3.4 Spark 1.6.</span></span> <span data-ttu-id="63609-125">However, the code in this article and in the [Scala Jupyter Notebook](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Scala/Exploration%20Modeling%20and%20Scoring%20using%20Scala.ipynb) are generic and should work on any Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="63609-125">However, the code in this article and in the [Scala Jupyter Notebook](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Scala/Exploration%20Modeling%20and%20Scoring%20using%20Scala.ipynb) are generic and should work on any Spark cluster.</span></span> <span data-ttu-id="63609-126">The cluster setup and management steps might be slightly different from what is shown in this article if you are not using HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="63609-126">The cluster setup and management steps might be slightly different from what is shown in this article if you are not using HDInsight Spark.</span></span>

> [!NOTE]
> <span data-ttu-id="63609-127">For a topic that shows you how to use Python rather than Scala to complete tasks for an end-to-end Data Science process, see [Data Science using Spark on Azure HDInsight](spark-overview.md).</span><span class="sxs-lookup"><span data-stu-id="63609-127">For a topic that shows you how to use Python rather than Scala to complete tasks for an end-to-end Data Science process, see [Data Science using Spark on Azure HDInsight](spark-overview.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="63609-128">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="63609-128">Prerequisites</span></span>
* <span data-ttu-id="63609-129">You must have an Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="63609-129">You must have an Azure subscription.</span></span> <span data-ttu-id="63609-130">If you do not already have one, [get an Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="63609-130">If you do not already have one, [get an Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="63609-131">You need an Azure HDInsight 3.4 Spark 1.6 cluster to complete the following procedures.</span><span class="sxs-lookup"><span data-stu-id="63609-131">You need an Azure HDInsight 3.4 Spark 1.6 cluster to complete the following procedures.</span></span> <span data-ttu-id="63609-132">To create a cluster, see the instructions in [Get started: Create Apache Spark on Azure HDInsight](../../hdinsight/spark/apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="63609-132">To create a cluster, see the instructions in [Get started: Create Apache Spark on Azure HDInsight](../../hdinsight/spark/apache-spark-jupyter-spark-sql.md).</span></span> <span data-ttu-id="63609-133">Set the cluster type and version on the **Select Cluster Type** menu.</span><span class="sxs-lookup"><span data-stu-id="63609-133">Set the cluster type and version on the **Select Cluster Type** menu.</span></span>

![HDInsight cluster type configuration](./media/scala-walkthrough/spark-cluster-on-portal.png)

> [!INCLUDE [delete-cluster-warning](../../../includes/hdinsight-delete-cluster-warning.md)]
> 
> 

<span data-ttu-id="63609-135">For a description of the NYC taxi trip data and instructions on how to execute code from a Jupyter notebook on the Spark cluster, see the relevant sections in [Overview of Data Science using Spark on Azure HDInsight](spark-overview.md).</span><span class="sxs-lookup"><span data-stu-id="63609-135">For a description of the NYC taxi trip data and instructions on how to execute code from a Jupyter notebook on the Spark cluster, see the relevant sections in [Overview of Data Science using Spark on Azure HDInsight](spark-overview.md).</span></span>  

## <a name="execute-scala-code-from-a-jupyter-notebook-on-the-spark-cluster"></a><span data-ttu-id="63609-136">Execute Scala code from a Jupyter notebook on the Spark cluster</span><span class="sxs-lookup"><span data-stu-id="63609-136">Execute Scala code from a Jupyter notebook on the Spark cluster</span></span>
<span data-ttu-id="63609-137">You can launch a Jupyter notebook from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="63609-137">You can launch a Jupyter notebook from the Azure portal.</span></span> <span data-ttu-id="63609-138">Find the Spark cluster on your dashboard, and then click it to enter the management page for your cluster.</span><span class="sxs-lookup"><span data-stu-id="63609-138">Find the Spark cluster on your dashboard, and then click it to enter the management page for your cluster.</span></span> <span data-ttu-id="63609-139">Next, click **Cluster Dashboards**, and then click **Jupyter Notebook** to open the notebook associated with the Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="63609-139">Next, click **Cluster Dashboards**, and then click **Jupyter Notebook** to open the notebook associated with the Spark cluster.</span></span>

![Cluster dashboard and Jupyter notebooks](./media/scala-walkthrough/spark-jupyter-on-portal.png)

<span data-ttu-id="63609-141">You also can access Jupyter notebooks at https://&lt;clustername&gt;.azurehdinsight.net/jupyter.</span><span class="sxs-lookup"><span data-stu-id="63609-141">You also can access Jupyter notebooks at https://&lt;clustername&gt;.azurehdinsight.net/jupyter.</span></span> <span data-ttu-id="63609-142">Replace *clustername* with the name of your cluster.</span><span class="sxs-lookup"><span data-stu-id="63609-142">Replace *clustername* with the name of your cluster.</span></span> <span data-ttu-id="63609-143">You need the password for your administrator account to access the Jupyter notebooks.</span><span class="sxs-lookup"><span data-stu-id="63609-143">You need the password for your administrator account to access the Jupyter notebooks.</span></span>

![Go to Jupyter notebooks by using the cluster name](./media/scala-walkthrough/spark-jupyter-notebook.png)

<span data-ttu-id="63609-145">Select **Scala** to see a directory that has a few examples of prepackaged notebooks that use the PySpark API.</span><span class="sxs-lookup"><span data-stu-id="63609-145">Select **Scala** to see a directory that has a few examples of prepackaged notebooks that use the PySpark API.</span></span> <span data-ttu-id="63609-146">The Exploration Modeling and Scoring using Scala.ipynb notebook that contains the code samples for this suite of Spark topics is available on [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/Spark/Scala).</span><span class="sxs-lookup"><span data-stu-id="63609-146">The Exploration Modeling and Scoring using Scala.ipynb notebook that contains the code samples for this suite of Spark topics is available on [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/Spark/Scala).</span></span>

<span data-ttu-id="63609-147">You can upload the notebook directly from GitHub to the Jupyter Notebook server on your Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="63609-147">You can upload the notebook directly from GitHub to the Jupyter Notebook server on your Spark cluster.</span></span> <span data-ttu-id="63609-148">On your Jupyter home page, click the **Upload** button.</span><span class="sxs-lookup"><span data-stu-id="63609-148">On your Jupyter home page, click the **Upload** button.</span></span> <span data-ttu-id="63609-149">In the file explorer, paste the GitHub (raw content) URL of the Scala notebook, and then click **Open**.</span><span class="sxs-lookup"><span data-stu-id="63609-149">In the file explorer, paste the GitHub (raw content) URL of the Scala notebook, and then click **Open**.</span></span> <span data-ttu-id="63609-150">The Scala notebook is available at the following URL:</span><span class="sxs-lookup"><span data-stu-id="63609-150">The Scala notebook is available at the following URL:</span></span>

[<span data-ttu-id="63609-151">Exploration-Modeling-and-Scoring-using-Scala.ipynb</span><span class="sxs-lookup"><span data-stu-id="63609-151">Exploration-Modeling-and-Scoring-using-Scala.ipynb</span></span>](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Scala/Exploration-Modeling-and-Scoring-using-Scala.ipynb)

## <a name="setup-preset-spark-and-hive-contexts-spark-magics-and-spark-libraries"></a><span data-ttu-id="63609-152">Setup: Preset Spark and Hive contexts, Spark magics, and Spark libraries</span><span class="sxs-lookup"><span data-stu-id="63609-152">Setup: Preset Spark and Hive contexts, Spark magics, and Spark libraries</span></span>
### <a name="preset-spark-and-hive-contexts"></a><span data-ttu-id="63609-153">Preset Spark and Hive contexts</span><span class="sxs-lookup"><span data-stu-id="63609-153">Preset Spark and Hive contexts</span></span>
    # SET THE START TIME
    import java.util.Calendar
    val beginningTime = Calendar.getInstance().getTime()


<span data-ttu-id="63609-154">The Spark kernels that are provided with Jupyter notebooks have preset contexts.</span><span class="sxs-lookup"><span data-stu-id="63609-154">The Spark kernels that are provided with Jupyter notebooks have preset contexts.</span></span> <span data-ttu-id="63609-155">You don't need to explicitly set the Spark or Hive contexts before you start working with the application you are developing.</span><span class="sxs-lookup"><span data-stu-id="63609-155">You don't need to explicitly set the Spark or Hive contexts before you start working with the application you are developing.</span></span> <span data-ttu-id="63609-156">The preset contexts are:</span><span class="sxs-lookup"><span data-stu-id="63609-156">The preset contexts are:</span></span>

* <span data-ttu-id="63609-157">`sc` for SparkContext</span><span class="sxs-lookup"><span data-stu-id="63609-157">`sc` for SparkContext</span></span>
* <span data-ttu-id="63609-158">`sqlContext` for HiveContext</span><span class="sxs-lookup"><span data-stu-id="63609-158">`sqlContext` for HiveContext</span></span>

### <a name="spark-magics"></a><span data-ttu-id="63609-159">Spark magics</span><span class="sxs-lookup"><span data-stu-id="63609-159">Spark magics</span></span>
<span data-ttu-id="63609-160">The Spark kernel provides some predefined “magics,” which are special commands that you can call with `%%`.</span><span class="sxs-lookup"><span data-stu-id="63609-160">The Spark kernel provides some predefined “magics,” which are special commands that you can call with `%%`.</span></span> <span data-ttu-id="63609-161">Two of these commands are used in the following code samples.</span><span class="sxs-lookup"><span data-stu-id="63609-161">Two of these commands are used in the following code samples.</span></span>

* <span data-ttu-id="63609-162">`%%local` specifies that the code in subsequent lines will be executed locally.</span><span class="sxs-lookup"><span data-stu-id="63609-162">`%%local` specifies that the code in subsequent lines will be executed locally.</span></span> <span data-ttu-id="63609-163">The code must be valid Scala code.</span><span class="sxs-lookup"><span data-stu-id="63609-163">The code must be valid Scala code.</span></span>
* <span data-ttu-id="63609-164">`%%sql -o <variable name>` executes a Hive query against `sqlContext`.</span><span class="sxs-lookup"><span data-stu-id="63609-164">`%%sql -o <variable name>` executes a Hive query against `sqlContext`.</span></span> <span data-ttu-id="63609-165">If the `-o` parameter is passed, the result of the query is persisted in the `%%local` Scala context as a Spark data frame.</span><span class="sxs-lookup"><span data-stu-id="63609-165">If the `-o` parameter is passed, the result of the query is persisted in the `%%local` Scala context as a Spark data frame.</span></span>

<span data-ttu-id="63609-166">For more information about the kernels for Jupyter notebooks and their predefined "magics" that you call with `%%` (for example, `%%local`), see [Kernels available for Jupyter notebooks with HDInsight Spark Linux clusters on HDInsight](../../hdinsight/spark/apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="63609-166">For more information about the kernels for Jupyter notebooks and their predefined "magics" that you call with `%%` (for example, `%%local`), see [Kernels available for Jupyter notebooks with HDInsight Spark Linux clusters on HDInsight](../../hdinsight/spark/apache-spark-jupyter-notebook-kernels.md).</span></span>

### <a name="import-libraries"></a><span data-ttu-id="63609-167">Import libraries</span><span class="sxs-lookup"><span data-stu-id="63609-167">Import libraries</span></span>
<span data-ttu-id="63609-168">Import the Spark, MLlib, and other libraries you'll need by using the following code.</span><span class="sxs-lookup"><span data-stu-id="63609-168">Import the Spark, MLlib, and other libraries you'll need by using the following code.</span></span>

    # IMPORT SPARK AND JAVA LIBRARIES
    import org.apache.spark.sql.SQLContext
    import org.apache.spark.sql.functions._
    import java.text.SimpleDateFormat
    import java.util.Calendar
    import sqlContext.implicits._
    import org.apache.spark.sql.Row

    # IMPORT SPARK SQL FUNCTIONS
    import org.apache.spark.sql.types.{StructType, StructField, StringType, IntegerType, FloatType, DoubleType}
    import org.apache.spark.sql.functions.rand

    # IMPORT SPARK ML FUNCTIONS
    import org.apache.spark.ml.Pipeline
    import org.apache.spark.ml.feature.{StringIndexer, VectorAssembler, OneHotEncoder, VectorIndexer, Binarizer}
    import org.apache.spark.ml.tuning.{ParamGridBuilder, TrainValidationSplit, CrossValidator}
    import org.apache.spark.ml.regression.{LinearRegression, LinearRegressionModel, RandomForestRegressor, RandomForestRegressionModel, GBTRegressor, GBTRegressionModel}
    import org.apache.spark.ml.classification.{LogisticRegression, LogisticRegressionModel, RandomForestClassifier, RandomForestClassificationModel, GBTClassifier, GBTClassificationModel}
    import org.apache.spark.ml.evaluation.{BinaryClassificationEvaluator, RegressionEvaluator, MulticlassClassificationEvaluator}

    # IMPORT SPARK MLLIB FUNCTIONS
    import org.apache.spark.mllib.linalg.{Vector, Vectors}
    import org.apache.spark.mllib.util.MLUtils
    import org.apache.spark.mllib.classification.{LogisticRegressionWithLBFGS, LogisticRegressionModel}
    import org.apache.spark.mllib.regression.{LabeledPoint, LinearRegressionWithSGD, LinearRegressionModel}
    import org.apache.spark.mllib.tree.{GradientBoostedTrees, RandomForest}
    import org.apache.spark.mllib.tree.configuration.BoostingStrategy
    import org.apache.spark.mllib.tree.model.{GradientBoostedTreesModel, RandomForestModel, Predict}
    import org.apache.spark.mllib.evaluation.{BinaryClassificationMetrics, MulticlassMetrics, RegressionMetrics}

    # SPECIFY SQLCONTEXT
    val sqlContext = new SQLContext(sc)


## <a name="data-ingestion"></a><span data-ttu-id="63609-169">Data ingestion</span><span class="sxs-lookup"><span data-stu-id="63609-169">Data ingestion</span></span>
<span data-ttu-id="63609-170">The first step in the Data Science process is to ingest the data that you want to analyze.</span><span class="sxs-lookup"><span data-stu-id="63609-170">The first step in the Data Science process is to ingest the data that you want to analyze.</span></span> <span data-ttu-id="63609-171">You bring the data from external sources or systems where it resides into your data exploration and modeling environment.</span><span class="sxs-lookup"><span data-stu-id="63609-171">You bring the data from external sources or systems where it resides into your data exploration and modeling environment.</span></span> <span data-ttu-id="63609-172">In this article, the data you ingest is a joined 0.1% sample of the taxi trip and fare file (stored as a .tsv file).</span><span class="sxs-lookup"><span data-stu-id="63609-172">In this article, the data you ingest is a joined 0.1% sample of the taxi trip and fare file (stored as a .tsv file).</span></span> <span data-ttu-id="63609-173">The data exploration and modeling environment is Spark.</span><span class="sxs-lookup"><span data-stu-id="63609-173">The data exploration and modeling environment is Spark.</span></span> <span data-ttu-id="63609-174">This section contains the code to complete the following series of tasks:</span><span class="sxs-lookup"><span data-stu-id="63609-174">This section contains the code to complete the following series of tasks:</span></span>

1. <span data-ttu-id="63609-175">Set directory paths for data and model storage.</span><span class="sxs-lookup"><span data-stu-id="63609-175">Set directory paths for data and model storage.</span></span>
2. <span data-ttu-id="63609-176">Read in the input data set (stored as a .tsv file).</span><span class="sxs-lookup"><span data-stu-id="63609-176">Read in the input data set (stored as a .tsv file).</span></span>
3. <span data-ttu-id="63609-177">Define a schema for the data and clean the data.</span><span class="sxs-lookup"><span data-stu-id="63609-177">Define a schema for the data and clean the data.</span></span>
4. <span data-ttu-id="63609-178">Create a cleaned data frame and cache it in memory.</span><span class="sxs-lookup"><span data-stu-id="63609-178">Create a cleaned data frame and cache it in memory.</span></span>
5. <span data-ttu-id="63609-179">Register the data as a temporary table in SQLContext.</span><span class="sxs-lookup"><span data-stu-id="63609-179">Register the data as a temporary table in SQLContext.</span></span>
6. <span data-ttu-id="63609-180">Query the table and import the results into a data frame.</span><span class="sxs-lookup"><span data-stu-id="63609-180">Query the table and import the results into a data frame.</span></span>

### <a name="set-directory-paths-for-storage-locations-in-azure-blob-storage"></a><span data-ttu-id="63609-181">Set directory paths for storage locations in Azure Blob storage</span><span class="sxs-lookup"><span data-stu-id="63609-181">Set directory paths for storage locations in Azure Blob storage</span></span>
<span data-ttu-id="63609-182">Spark can read and write to Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="63609-182">Spark can read and write to Azure Blob storage.</span></span> <span data-ttu-id="63609-183">You can use Spark to process any of your existing data, and then store the results again in Blob storage.</span><span class="sxs-lookup"><span data-stu-id="63609-183">You can use Spark to process any of your existing data, and then store the results again in Blob storage.</span></span>

<span data-ttu-id="63609-184">To save models or files in Blob storage, you need to properly specify the path.</span><span class="sxs-lookup"><span data-stu-id="63609-184">To save models or files in Blob storage, you need to properly specify the path.</span></span> <span data-ttu-id="63609-185">Reference the default container attached to the Spark cluster by using a path that begins with `wasb:///`.</span><span class="sxs-lookup"><span data-stu-id="63609-185">Reference the default container attached to the Spark cluster by using a path that begins with `wasb:///`.</span></span> <span data-ttu-id="63609-186">Reference other locations by using `wasb://`.</span><span class="sxs-lookup"><span data-stu-id="63609-186">Reference other locations by using `wasb://`.</span></span>

<span data-ttu-id="63609-187">The following code sample specifies the location of the input data to be read and the path to Blob storage that is attached to the Spark cluster where the model will be saved.</span><span class="sxs-lookup"><span data-stu-id="63609-187">The following code sample specifies the location of the input data to be read and the path to Blob storage that is attached to the Spark cluster where the model will be saved.</span></span>

    # SET PATHS TO DATA AND MODEL FILE LOCATIONS
    # INGEST DATA AND SPECIFY HEADERS FOR COLUMNS
    val taxi_train_file = sc.textFile("wasb://mllibwalkthroughs@cdspsparksamples.blob.core.windows.net/Data/NYCTaxi/JoinedTaxiTripFare.Point1Pct.Train.tsv")
    val header = taxi_train_file.first;

    # SET THE MODEL STORAGE DIRECTORY PATH
    # NOTE THAT THE FINAL BACKSLASH IN THE PATH IS REQUIRED.
    val modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/";


### <a name="import-data-create-an-rdd-and-define-a-data-frame-according-to-the-schema"></a><span data-ttu-id="63609-188">Import data, create an RDD, and define a data frame according to the schema</span><span class="sxs-lookup"><span data-stu-id="63609-188">Import data, create an RDD, and define a data frame according to the schema</span></span>
    # RECORD THE START TIME
    val starttime = Calendar.getInstance().getTime()

    # DEFINE THE SCHEMA BASED ON THE HEADER OF THE FILE
    val sqlContext = new SQLContext(sc)
    val taxi_schema = StructType(
        Array(
            StructField("medallion", StringType, true),
            StructField("hack_license", StringType, true),
            StructField("vendor_id", StringType, true),
            StructField("rate_code", DoubleType, true),
            StructField("store_and_fwd_flag", StringType, true),
            StructField("pickup_datetime", StringType, true),
            StructField("dropoff_datetime", StringType, true),
            StructField("pickup_hour", DoubleType, true),
            StructField("pickup_week", DoubleType, true),
            StructField("weekday", DoubleType, true),
            StructField("passenger_count", DoubleType, true),
            StructField("trip_time_in_secs", DoubleType, true),
            StructField("trip_distance", DoubleType, true),
            StructField("pickup_longitude", DoubleType, true),
            StructField("pickup_latitude", DoubleType, true),
            StructField("dropoff_longitude", DoubleType, true),
            StructField("dropoff_latitude", DoubleType, true),
            StructField("direct_distance", StringType, true),
            StructField("payment_type", StringType, true),
            StructField("fare_amount", DoubleType, true),
            StructField("surcharge", DoubleType, true),
            StructField("mta_tax", DoubleType, true),
            StructField("tip_amount", DoubleType, true),
            StructField("tolls_amount", DoubleType, true),
            StructField("total_amount", DoubleType, true),
            StructField("tipped", DoubleType, true),
            StructField("tip_class", DoubleType, true)
            )
        )

    # CAST VARIABLES ACCORDING TO THE SCHEMA
    val taxi_temp = (taxi_train_file.map(_.split("\t"))
                            .filter((r) => r(0) != "medallion")
                            .map(p => Row(p(0), p(1), p(2),
                                p(3).toDouble, p(4), p(5), p(6), p(7).toDouble, p(8).toDouble, p(9).toDouble, p(10).toDouble,
                                p(11).toDouble, p(12).toDouble, p(13).toDouble, p(14).toDouble, p(15).toDouble, p(16).toDouble,
                                p(17), p(18), p(19).toDouble, p(20).toDouble, p(21).toDouble, p(22).toDouble,
                                p(23).toDouble, p(24).toDouble, p(25).toDouble, p(26).toDouble)))


    # CREATE AN INITIAL DATA FRAME AND DROP COLUMNS, AND THEN CREATE A CLEANED DATA FRAME BY FILTERING FOR UNWANTED VALUES OR OUTLIERS
    val taxi_train_df = sqlContext.createDataFrame(taxi_temp, taxi_schema)

    val taxi_df_train_cleaned = (taxi_train_df.drop(taxi_train_df.col("medallion"))
            .drop(taxi_train_df.col("hack_license")).drop(taxi_train_df.col("store_and_fwd_flag"))
            .drop(taxi_train_df.col("pickup_datetime")).drop(taxi_train_df.col("dropoff_datetime"))
            .drop(taxi_train_df.col("pickup_longitude")).drop(taxi_train_df.col("pickup_latitude"))
            .drop(taxi_train_df.col("dropoff_longitude")).drop(taxi_train_df.col("dropoff_latitude"))
            .drop(taxi_train_df.col("surcharge")).drop(taxi_train_df.col("mta_tax"))
            .drop(taxi_train_df.col("direct_distance")).drop(taxi_train_df.col("tolls_amount"))
            .drop(taxi_train_df.col("total_amount")).drop(taxi_train_df.col("tip_class"))
            .filter("passenger_count > 0 and passenger_count < 8 AND payment_type in ('CSH', 'CRD') AND tip_amount >= 0 AND tip_amount < 30 AND fare_amount >= 1 AND fare_amount < 150 AND trip_distance > 0 AND trip_distance < 100 AND trip_time_in_secs > 30 AND trip_time_in_secs < 7200"));

    # CACHE AND MATERIALIZE THE CLEANED DATA FRAME IN MEMORY
    taxi_df_train_cleaned.cache()
    taxi_df_train_cleaned.count()

    # REGISTER THE DATA FRAME AS A TEMPORARY TABLE IN SQLCONTEXT
    taxi_df_train_cleaned.registerTempTable("taxi_train")

    # GET THE TIME TO RUN THE CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken to run the above cell: " + elapsedtime + " seconds.");


<span data-ttu-id="63609-189">**Output:**</span><span class="sxs-lookup"><span data-stu-id="63609-189">**Output:**</span></span>

<span data-ttu-id="63609-190">Time to run the cell: 8 seconds.</span><span class="sxs-lookup"><span data-stu-id="63609-190">Time to run the cell: 8 seconds.</span></span>

### <a name="query-the-table-and-import-results-in-a-data-frame"></a><span data-ttu-id="63609-191">Query the table and import results in a data frame</span><span class="sxs-lookup"><span data-stu-id="63609-191">Query the table and import results in a data frame</span></span>
<span data-ttu-id="63609-192">Next, query the table for fare, passenger, and tip data; filter out corrupt and outlying data; and print several rows.</span><span class="sxs-lookup"><span data-stu-id="63609-192">Next, query the table for fare, passenger, and tip data; filter out corrupt and outlying data; and print several rows.</span></span>

    # QUERY THE DATA
    val sqlStatement = """
        SELECT fare_amount, passenger_count, tip_amount, tipped
        FROM taxi_train
        WHERE passenger_count > 0 AND passenger_count < 7
        AND fare_amount > 0 AND fare_amount < 200
        AND payment_type in ('CSH', 'CRD')
        AND tip_amount > 0 AND tip_amount < 25
    """
    val sqlResultsDF = sqlContext.sql(sqlStatement)

    # SHOW ONLY THE TOP THREE ROWS
    sqlResultsDF.show(3)

<span data-ttu-id="63609-193">**Output:**</span><span class="sxs-lookup"><span data-stu-id="63609-193">**Output:**</span></span>

| <span data-ttu-id="63609-194">fare_amount</span><span class="sxs-lookup"><span data-stu-id="63609-194">fare_amount</span></span> | <span data-ttu-id="63609-195">passenger_count</span><span class="sxs-lookup"><span data-stu-id="63609-195">passenger_count</span></span> | <span data-ttu-id="63609-196">tip_amount</span><span class="sxs-lookup"><span data-stu-id="63609-196">tip_amount</span></span> | <span data-ttu-id="63609-197">tipped</span><span class="sxs-lookup"><span data-stu-id="63609-197">tipped</span></span> |
| --- | --- | --- | --- |
|        <span data-ttu-id="63609-198">13.5</span><span class="sxs-lookup"><span data-stu-id="63609-198">13.5</span></span> |<span data-ttu-id="63609-199">1.0</span><span class="sxs-lookup"><span data-stu-id="63609-199">1.0</span></span> |<span data-ttu-id="63609-200">2.9</span><span class="sxs-lookup"><span data-stu-id="63609-200">2.9</span></span> |<span data-ttu-id="63609-201">1.0</span><span class="sxs-lookup"><span data-stu-id="63609-201">1.0</span></span> |
|        <span data-ttu-id="63609-202">16.0</span><span class="sxs-lookup"><span data-stu-id="63609-202">16.0</span></span> |<span data-ttu-id="63609-203">2.0</span><span class="sxs-lookup"><span data-stu-id="63609-203">2.0</span></span> |<span data-ttu-id="63609-204">3.4</span><span class="sxs-lookup"><span data-stu-id="63609-204">3.4</span></span> |<span data-ttu-id="63609-205">1.0</span><span class="sxs-lookup"><span data-stu-id="63609-205">1.0</span></span> |
|        <span data-ttu-id="63609-206">10.5</span><span class="sxs-lookup"><span data-stu-id="63609-206">10.5</span></span> |<span data-ttu-id="63609-207">2.0</span><span class="sxs-lookup"><span data-stu-id="63609-207">2.0</span></span> |<span data-ttu-id="63609-208">1.0</span><span class="sxs-lookup"><span data-stu-id="63609-208">1.0</span></span> |<span data-ttu-id="63609-209">1.0</span><span class="sxs-lookup"><span data-stu-id="63609-209">1.0</span></span> |

## <a name="data-exploration-and-visualization"></a><span data-ttu-id="63609-210">Data exploration and visualization</span><span class="sxs-lookup"><span data-stu-id="63609-210">Data exploration and visualization</span></span>
<span data-ttu-id="63609-211">After you bring the data into Spark, the next step in the Data Science process is to gain a deeper understanding of the data through exploration and visualization.</span><span class="sxs-lookup"><span data-stu-id="63609-211">After you bring the data into Spark, the next step in the Data Science process is to gain a deeper understanding of the data through exploration and visualization.</span></span> <span data-ttu-id="63609-212">In this section, you examine the taxi data by using SQL queries.</span><span class="sxs-lookup"><span data-stu-id="63609-212">In this section, you examine the taxi data by using SQL queries.</span></span> <span data-ttu-id="63609-213">Then, import the results into a data frame to plot the target variables and prospective features for visual inspection by using the auto-visualization feature of Jupyter.</span><span class="sxs-lookup"><span data-stu-id="63609-213">Then, import the results into a data frame to plot the target variables and prospective features for visual inspection by using the auto-visualization feature of Jupyter.</span></span>

### <a name="use-local-and-sql-magic-to-plot-data"></a><span data-ttu-id="63609-214">Use local and SQL magic to plot data</span><span class="sxs-lookup"><span data-stu-id="63609-214">Use local and SQL magic to plot data</span></span>
<span data-ttu-id="63609-215">By default, the output of any code snippet that you run from a Jupyter notebook is available within the context of the session that is persisted on the worker nodes.</span><span class="sxs-lookup"><span data-stu-id="63609-215">By default, the output of any code snippet that you run from a Jupyter notebook is available within the context of the session that is persisted on the worker nodes.</span></span> <span data-ttu-id="63609-216">If you want to save a trip to the worker nodes for every computation, and if all the data that you need for your computation is available locally on the Jupyter server node (which is the head node), you can use the `%%local` magic to run the code snippet on the Jupyter server.</span><span class="sxs-lookup"><span data-stu-id="63609-216">If you want to save a trip to the worker nodes for every computation, and if all the data that you need for your computation is available locally on the Jupyter server node (which is the head node), you can use the `%%local` magic to run the code snippet on the Jupyter server.</span></span>

* <span data-ttu-id="63609-217">**SQL magic** (`%%sql`).</span><span class="sxs-lookup"><span data-stu-id="63609-217">**SQL magic** (`%%sql`).</span></span> <span data-ttu-id="63609-218">The HDInsight Spark kernel supports easy inline HiveQL queries against SQLContext.</span><span class="sxs-lookup"><span data-stu-id="63609-218">The HDInsight Spark kernel supports easy inline HiveQL queries against SQLContext.</span></span> <span data-ttu-id="63609-219">The (`-o VARIABLE_NAME`) argument persists the output of the SQL query as a Pandas data frame on the Jupyter server.</span><span class="sxs-lookup"><span data-stu-id="63609-219">The (`-o VARIABLE_NAME`) argument persists the output of the SQL query as a Pandas data frame on the Jupyter server.</span></span> <span data-ttu-id="63609-220">This means it'll be available in the local mode.</span><span class="sxs-lookup"><span data-stu-id="63609-220">This means it'll be available in the local mode.</span></span>
* <span data-ttu-id="63609-221">`%%local` **magic**.</span><span class="sxs-lookup"><span data-stu-id="63609-221">`%%local` **magic**.</span></span> <span data-ttu-id="63609-222">The `%%local` magic runs the code locally on the Jupyter server, which is the head node of the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="63609-222">The `%%local` magic runs the code locally on the Jupyter server, which is the head node of the HDInsight cluster.</span></span> <span data-ttu-id="63609-223">Typically, you use `%%local` magic in conjunction with the `%%sql` magic with the `-o` parameter.</span><span class="sxs-lookup"><span data-stu-id="63609-223">Typically, you use `%%local` magic in conjunction with the `%%sql` magic with the `-o` parameter.</span></span> <span data-ttu-id="63609-224">The `-o` parameter would persist the output of the SQL query locally, and then `%%local` magic would trigger the next set of code snippet to run locally against the output of the SQL queries that is persisted locally.</span><span class="sxs-lookup"><span data-stu-id="63609-224">The `-o` parameter would persist the output of the SQL query locally, and then `%%local` magic would trigger the next set of code snippet to run locally against the output of the SQL queries that is persisted locally.</span></span>

### <a name="query-the-data-by-using-sql"></a><span data-ttu-id="63609-225">Query the data by using SQL</span><span class="sxs-lookup"><span data-stu-id="63609-225">Query the data by using SQL</span></span>
<span data-ttu-id="63609-226">This query retrieves the taxi trips by fare amount, passenger count, and tip amount.</span><span class="sxs-lookup"><span data-stu-id="63609-226">This query retrieves the taxi trips by fare amount, passenger count, and tip amount.</span></span>

    # RUN THE SQL QUERY
    %%sql -q -o sqlResults
    SELECT fare_amount, passenger_count, tip_amount, tipped FROM taxi_train WHERE passenger_count > 0 AND passenger_count < 7 AND fare_amount > 0 AND fare_amount < 200 AND payment_type in ('CSH', 'CRD') AND tip_amount > 0 AND tip_amount < 25

<span data-ttu-id="63609-227">In the following code, the `%%local` magic creates a local data frame, sqlResults.</span><span class="sxs-lookup"><span data-stu-id="63609-227">In the following code, the `%%local` magic creates a local data frame, sqlResults.</span></span> <span data-ttu-id="63609-228">You can use sqlResults to plot by using matplotlib.</span><span class="sxs-lookup"><span data-stu-id="63609-228">You can use sqlResults to plot by using matplotlib.</span></span>

> [!TIP]
> <span data-ttu-id="63609-229">Local magic is used multiple times in this article.</span><span class="sxs-lookup"><span data-stu-id="63609-229">Local magic is used multiple times in this article.</span></span> <span data-ttu-id="63609-230">If your data set is large, please sample to create a data frame that can fit in local memory.</span><span class="sxs-lookup"><span data-stu-id="63609-230">If your data set is large, please sample to create a data frame that can fit in local memory.</span></span>
> 
> 

### <a name="plot-the-data"></a><span data-ttu-id="63609-231">Plot the data</span><span class="sxs-lookup"><span data-stu-id="63609-231">Plot the data</span></span>
<span data-ttu-id="63609-232">You can plot by using Python code after the data frame is in local context as a Pandas data frame.</span><span class="sxs-lookup"><span data-stu-id="63609-232">You can plot by using Python code after the data frame is in local context as a Pandas data frame.</span></span>

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER
    %%local

    # USE THE JUPYTER AUTO-PLOTTING FEATURE TO CREATE INTERACTIVE FIGURES.
    # CLICK THE TYPE OF PLOT TO GENERATE (LINE, AREA, BAR, ETC.)
    sqlResults


 <span data-ttu-id="63609-233">The Spark kernel automatically visualizes the output of SQL (HiveQL) queries after you run the code.</span><span class="sxs-lookup"><span data-stu-id="63609-233">The Spark kernel automatically visualizes the output of SQL (HiveQL) queries after you run the code.</span></span> <span data-ttu-id="63609-234">You can choose between several types of visualizations:</span><span class="sxs-lookup"><span data-stu-id="63609-234">You can choose between several types of visualizations:</span></span>

* <span data-ttu-id="63609-235">Table</span><span class="sxs-lookup"><span data-stu-id="63609-235">Table</span></span>
* <span data-ttu-id="63609-236">Pie</span><span class="sxs-lookup"><span data-stu-id="63609-236">Pie</span></span>
* <span data-ttu-id="63609-237">Line</span><span class="sxs-lookup"><span data-stu-id="63609-237">Line</span></span>
* <span data-ttu-id="63609-238">Area</span><span class="sxs-lookup"><span data-stu-id="63609-238">Area</span></span>
* <span data-ttu-id="63609-239">Bar</span><span class="sxs-lookup"><span data-stu-id="63609-239">Bar</span></span>

<span data-ttu-id="63609-240">Here's the code to plot the data:</span><span class="sxs-lookup"><span data-stu-id="63609-240">Here's the code to plot the data:</span></span>

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    import matplotlib.pyplot as plt
    %matplotlib inline

    # PLOT TIP BY PAYMENT TYPE AND PASSENGER COUNT
    ax1 = sqlResults[['tip_amount']].plot(kind='hist', bins=25, facecolor='lightblue')
    ax1.set_title('Tip amount distribution')
    ax1.set_xlabel('Tip Amount ($)')
    ax1.set_ylabel('Counts')
    plt.suptitle('')
    plt.show()

    # PLOT TIP BY PASSENGER COUNT
    ax2 = sqlResults.boxplot(column=['tip_amount'], by=['passenger_count'])
    ax2.set_title('Tip amount by Passenger count')
    ax2.set_xlabel('Passenger count')
    ax2.set_ylabel('Tip Amount ($)')
    plt.suptitle('')
    plt.show()

    # PLOT TIP AMOUNT BY FARE AMOUNT; SCALE POINTS BY PASSENGER COUNT
    ax = sqlResults.plot(kind='scatter', x= 'fare_amount', y = 'tip_amount', c='blue', alpha = 0.10, s=5*(sqlResults.passenger_count))
    ax.set_title('Tip amount by Fare amount')
    ax.set_xlabel('Fare Amount ($)')
    ax.set_ylabel('Tip Amount ($)')
    plt.axis([-2, 80, -2, 20])
    plt.show()


<span data-ttu-id="63609-241">**Output:**</span><span class="sxs-lookup"><span data-stu-id="63609-241">**Output:**</span></span>

![Tip amount histogram](./media/scala-walkthrough/plot-tip-amount-histogram.png)

![Tip amount by passenger count](./media/scala-walkthrough/plot-tip-amount-by-passenger-count.png)

![Tip amount by fare amount](./media/scala-walkthrough/plot-tip-amount-by-fare-amount.png)

## <a name="create-features-and-transform-features-and-then-prep-data-for-input-into-modeling-functions"></a><span data-ttu-id="63609-245">Create features and transform features, and then prep data for input into modeling functions</span><span class="sxs-lookup"><span data-stu-id="63609-245">Create features and transform features, and then prep data for input into modeling functions</span></span>
<span data-ttu-id="63609-246">For tree-based modeling functions from Spark ML and MLlib, you have to prepare target and features by using a variety of techniques, such as binning, indexing, one-hot encoding, and vectorization.</span><span class="sxs-lookup"><span data-stu-id="63609-246">For tree-based modeling functions from Spark ML and MLlib, you have to prepare target and features by using a variety of techniques, such as binning, indexing, one-hot encoding, and vectorization.</span></span> <span data-ttu-id="63609-247">Here are the procedures to follow in this section:</span><span class="sxs-lookup"><span data-stu-id="63609-247">Here are the procedures to follow in this section:</span></span>

1. <span data-ttu-id="63609-248">Create a new feature by **binning** hours into traffic time buckets.</span><span class="sxs-lookup"><span data-stu-id="63609-248">Create a new feature by **binning** hours into traffic time buckets.</span></span>
2. <span data-ttu-id="63609-249">Apply **indexing and one-hot encoding** to categorical features.</span><span class="sxs-lookup"><span data-stu-id="63609-249">Apply **indexing and one-hot encoding** to categorical features.</span></span>
3. <span data-ttu-id="63609-250">**Sample and split the data set** into training and test fractions.</span><span class="sxs-lookup"><span data-stu-id="63609-250">**Sample and split the data set** into training and test fractions.</span></span>
4. <span data-ttu-id="63609-251">**Specify training variable and features**, and then create indexed or one-hot encoded training and testing input labeled point resilient distributed datasets (RDDs) or data frames.</span><span class="sxs-lookup"><span data-stu-id="63609-251">**Specify training variable and features**, and then create indexed or one-hot encoded training and testing input labeled point resilient distributed datasets (RDDs) or data frames.</span></span>
5. <span data-ttu-id="63609-252">Automatically **categorize and vectorize features and targets** to use as inputs for machine learning models.</span><span class="sxs-lookup"><span data-stu-id="63609-252">Automatically **categorize and vectorize features and targets** to use as inputs for machine learning models.</span></span>

### <a name="create-a-new-feature-by-binning-hours-into-traffic-time-buckets"></a><span data-ttu-id="63609-253">Create a new feature by binning hours into traffic time buckets</span><span class="sxs-lookup"><span data-stu-id="63609-253">Create a new feature by binning hours into traffic time buckets</span></span>
<span data-ttu-id="63609-254">This code shows you how to create a new feature by binning hours into traffic time buckets and how to cache the resulting data frame in memory.</span><span class="sxs-lookup"><span data-stu-id="63609-254">This code shows you how to create a new feature by binning hours into traffic time buckets and how to cache the resulting data frame in memory.</span></span> <span data-ttu-id="63609-255">Where RDDs and data frames are used repeatedly, caching leads to improved execution times.</span><span class="sxs-lookup"><span data-stu-id="63609-255">Where RDDs and data frames are used repeatedly, caching leads to improved execution times.</span></span> <span data-ttu-id="63609-256">Accordingly, you'll cache RDDs and data frames at several stages in the following procedures.</span><span class="sxs-lookup"><span data-stu-id="63609-256">Accordingly, you'll cache RDDs and data frames at several stages in the following procedures.</span></span>

    # CREATE FOUR BUCKETS FOR TRAFFIC TIMES
    val sqlStatement = """
        SELECT *,
        CASE
         WHEN (pickup_hour <= 6 OR pickup_hour >= 20) THEN "Night"
         WHEN (pickup_hour >= 7 AND pickup_hour <= 10) THEN "AMRush"
         WHEN (pickup_hour >= 11 AND pickup_hour <= 15) THEN "Afternoon"
         WHEN (pickup_hour >= 16 AND pickup_hour <= 19) THEN "PMRush"
        END as TrafficTimeBins
        FROM taxi_train
    """
    val taxi_df_train_with_newFeatures = sqlContext.sql(sqlStatement)

    # CACHE THE DATA FRAME IN MEMORY AND MATERIALIZE THE DATA FRAME IN MEMORY
    taxi_df_train_with_newFeatures.cache()
    taxi_df_train_with_newFeatures.count()


### <a name="indexing-and-one-hot-encoding-of-categorical-features"></a><span data-ttu-id="63609-257">Indexing and one-hot encoding of categorical features</span><span class="sxs-lookup"><span data-stu-id="63609-257">Indexing and one-hot encoding of categorical features</span></span>
<span data-ttu-id="63609-258">The modeling and predict functions of MLlib require features with categorical input data to be indexed or encoded prior to use.</span><span class="sxs-lookup"><span data-stu-id="63609-258">The modeling and predict functions of MLlib require features with categorical input data to be indexed or encoded prior to use.</span></span> <span data-ttu-id="63609-259">This section shows you how to index or encode categorical features for input into the modeling functions.</span><span class="sxs-lookup"><span data-stu-id="63609-259">This section shows you how to index or encode categorical features for input into the modeling functions.</span></span>

<span data-ttu-id="63609-260">You need to index or encode your models in different ways, depending on the model.</span><span class="sxs-lookup"><span data-stu-id="63609-260">You need to index or encode your models in different ways, depending on the model.</span></span> <span data-ttu-id="63609-261">For example, logistic and linear regression models require one-hot encoding.</span><span class="sxs-lookup"><span data-stu-id="63609-261">For example, logistic and linear regression models require one-hot encoding.</span></span> <span data-ttu-id="63609-262">For example, a feature with three categories can be expanded into three feature columns.</span><span class="sxs-lookup"><span data-stu-id="63609-262">For example, a feature with three categories can be expanded into three feature columns.</span></span> <span data-ttu-id="63609-263">Each column would contain 0 or 1 depending on the category of an observation.</span><span class="sxs-lookup"><span data-stu-id="63609-263">Each column would contain 0 or 1 depending on the category of an observation.</span></span> <span data-ttu-id="63609-264">MLlib provides the [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) function for one-hot encoding.</span><span class="sxs-lookup"><span data-stu-id="63609-264">MLlib provides the [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) function for one-hot encoding.</span></span> <span data-ttu-id="63609-265">This encoder maps a column of label indices to a column of binary vectors with at most a single one-value.</span><span class="sxs-lookup"><span data-stu-id="63609-265">This encoder maps a column of label indices to a column of binary vectors with at most a single one-value.</span></span> <span data-ttu-id="63609-266">With this encoding, algorithms that expect numerical valued features, such as logistic regression, can be applied to categorical features.</span><span class="sxs-lookup"><span data-stu-id="63609-266">With this encoding, algorithms that expect numerical valued features, such as logistic regression, can be applied to categorical features.</span></span>

<span data-ttu-id="63609-267">Here you transform only four variables to show examples, which are character strings.</span><span class="sxs-lookup"><span data-stu-id="63609-267">Here you transform only four variables to show examples, which are character strings.</span></span> <span data-ttu-id="63609-268">You also can index other variables, such as weekday, represented by numerical values, as categorical variables.</span><span class="sxs-lookup"><span data-stu-id="63609-268">You also can index other variables, such as weekday, represented by numerical values, as categorical variables.</span></span>

<span data-ttu-id="63609-269">For indexing, use `StringIndexer()`, and for one-hot encoding, use `OneHotEncoder()` functions from MLlib.</span><span class="sxs-lookup"><span data-stu-id="63609-269">For indexing, use `StringIndexer()`, and for one-hot encoding, use `OneHotEncoder()` functions from MLlib.</span></span> <span data-ttu-id="63609-270">Here is the code to index and encode categorical features:</span><span class="sxs-lookup"><span data-stu-id="63609-270">Here is the code to index and encode categorical features:</span></span>

    # CREATE INDEXES AND ONE-HOT ENCODED VECTORS FOR SEVERAL CATEGORICAL FEATURES

    # RECORD THE START TIME
    val starttime = Calendar.getInstance().getTime()

    # INDEX AND ENCODE VENDOR_ID
    val stringIndexer = new StringIndexer().setInputCol("vendor_id").setOutputCol("vendorIndex").fit(taxi_df_train_with_newFeatures)
    val indexed = stringIndexer.transform(taxi_df_train_with_newFeatures)
    val encoder = new OneHotEncoder().setInputCol("vendorIndex").setOutputCol("vendorVec")
    val encoded1 = encoder.transform(indexed)

    # INDEX AND ENCODE RATE_CODE
    val stringIndexer = new StringIndexer().setInputCol("rate_code").setOutputCol("rateIndex").fit(encoded1)
    val indexed = stringIndexer.transform(encoded1)
    val encoder = new OneHotEncoder().setInputCol("rateIndex").setOutputCol("rateVec")
    val encoded2 = encoder.transform(indexed)

    # INDEX AND ENCODE PAYMENT_TYPE
    val stringIndexer = new StringIndexer().setInputCol("payment_type").setOutputCol("paymentIndex").fit(encoded2)
    val indexed = stringIndexer.transform(encoded2)
    val encoder = new OneHotEncoder().setInputCol("paymentIndex").setOutputCol("paymentVec")
    val encoded3 = encoder.transform(indexed)

    # INDEX AND TRAFFIC TIME BINS
    val stringIndexer = new StringIndexer().setInputCol("TrafficTimeBins").setOutputCol("TrafficTimeBinsIndex").fit(encoded3)
    val indexed = stringIndexer.transform(encoded3)
    val encoder = new OneHotEncoder().setInputCol("TrafficTimeBinsIndex").setOutputCol("TrafficTimeBinsVec")
    val encodedFinal = encoder.transform(indexed)

    # GET THE TIME TO RUN THE CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken to run the above cell: " + elapsedtime + " seconds.");


<span data-ttu-id="63609-271">**Output:**</span><span class="sxs-lookup"><span data-stu-id="63609-271">**Output:**</span></span>

<span data-ttu-id="63609-272">Time to run the cell: 4 seconds.</span><span class="sxs-lookup"><span data-stu-id="63609-272">Time to run the cell: 4 seconds.</span></span>

### <a name="sample-and-split-the-data-set-into-training-and-test-fractions"></a><span data-ttu-id="63609-273">Sample and split the data set into training and test fractions</span><span class="sxs-lookup"><span data-stu-id="63609-273">Sample and split the data set into training and test fractions</span></span>
<span data-ttu-id="63609-274">This code creates a random sampling of the data (25%, in this example).</span><span class="sxs-lookup"><span data-stu-id="63609-274">This code creates a random sampling of the data (25%, in this example).</span></span> <span data-ttu-id="63609-275">Although sampling is not required for this example due to the size of the data set, the article shows you how you can sample so that you know how to use it for your own problems when needed.</span><span class="sxs-lookup"><span data-stu-id="63609-275">Although sampling is not required for this example due to the size of the data set, the article shows you how you can sample so that you know how to use it for your own problems when needed.</span></span> <span data-ttu-id="63609-276">When samples are large, this can save significant time while you train models.</span><span class="sxs-lookup"><span data-stu-id="63609-276">When samples are large, this can save significant time while you train models.</span></span> <span data-ttu-id="63609-277">Next, split the sample into a training part (75%, in this example) and a testing part (25%, in this example) to use in classification and regression modeling.</span><span class="sxs-lookup"><span data-stu-id="63609-277">Next, split the sample into a training part (75%, in this example) and a testing part (25%, in this example) to use in classification and regression modeling.</span></span>

<span data-ttu-id="63609-278">Add a random number (between 0 and 1) to each row (in a "rand" column) that can be used to select cross-validation folds during training.</span><span class="sxs-lookup"><span data-stu-id="63609-278">Add a random number (between 0 and 1) to each row (in a "rand" column) that can be used to select cross-validation folds during training.</span></span>

    # RECORD THE START TIME
    val starttime = Calendar.getInstance().getTime()

    # SPECIFY SAMPLING AND SPLITTING FRACTIONS
    val samplingFraction = 0.25;
    val trainingFraction = 0.75;
    val testingFraction = (1-trainingFraction);
    val seed = 1234;
    val encodedFinalSampledTmp = encodedFinal.sample(withReplacement = false, fraction = samplingFraction, seed = seed)
    val sampledDFcount = encodedFinalSampledTmp.count().toInt

    val generateRandomDouble = udf(() => {
        scala.util.Random.nextDouble
    })

    # ADD A RANDOM NUMBER FOR CROSS-VALIDATION
    val encodedFinalSampled = encodedFinalSampledTmp.withColumn("rand", generateRandomDouble());

    # SPLIT THE SAMPLED DATA FRAME INTO TRAIN AND TEST, WITH A RANDOM COLUMN ADDED FOR DOING CROSS-VALIDATION (SHOWN LATER)
    # INCLUDE A RANDOM COLUMN FOR CREATING CROSS-VALIDATION FOLDS
    val splits = encodedFinalSampled.randomSplit(Array(trainingFraction, testingFraction), seed = seed)
    val trainData = splits(0)
    val testData = splits(1)

    # GET THE TIME TO RUN THE CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken to run the above cell: " + elapsedtime + " seconds.");


<span data-ttu-id="63609-279">**Output:**</span><span class="sxs-lookup"><span data-stu-id="63609-279">**Output:**</span></span>

<span data-ttu-id="63609-280">Time to run the cell: 2 seconds.</span><span class="sxs-lookup"><span data-stu-id="63609-280">Time to run the cell: 2 seconds.</span></span>

### <a name="specify-training-variable-and-features-and-then-create-indexed-or-one-hot-encoded-training-and-testing-input-labeled-point-rdds-or-data-frames"></a><span data-ttu-id="63609-281">Specify training variable and features, and then create indexed or one-hot encoded training and testing input labeled point RDDs or data frames</span><span class="sxs-lookup"><span data-stu-id="63609-281">Specify training variable and features, and then create indexed or one-hot encoded training and testing input labeled point RDDs or data frames</span></span>
<span data-ttu-id="63609-282">This section contains code that shows you how to index categorical text data as a labeled point data type, and encode it so you can use it to train and test MLlib logistic regression and other classification models.</span><span class="sxs-lookup"><span data-stu-id="63609-282">This section contains code that shows you how to index categorical text data as a labeled point data type, and encode it so you can use it to train and test MLlib logistic regression and other classification models.</span></span> <span data-ttu-id="63609-283">Labeled point objects are RDDs that are formatted in a way that is needed as input data by most of machine learning algorithms in MLlib.</span><span class="sxs-lookup"><span data-stu-id="63609-283">Labeled point objects are RDDs that are formatted in a way that is needed as input data by most of machine learning algorithms in MLlib.</span></span> <span data-ttu-id="63609-284">A [labeled point](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) is a local vector, either dense or sparse, associated with a label/response.</span><span class="sxs-lookup"><span data-stu-id="63609-284">A [labeled point](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) is a local vector, either dense or sparse, associated with a label/response.</span></span>

<span data-ttu-id="63609-285">In this code, you specify the target (dependent) variable and the features to use to train models.</span><span class="sxs-lookup"><span data-stu-id="63609-285">In this code, you specify the target (dependent) variable and the features to use to train models.</span></span> <span data-ttu-id="63609-286">Then, you create indexed or one-hot encoded training and testing input labeled point RDDs or data frames.</span><span class="sxs-lookup"><span data-stu-id="63609-286">Then, you create indexed or one-hot encoded training and testing input labeled point RDDs or data frames.</span></span>

    # RECORD THE START TIME
    val starttime = Calendar.getInstance().getTime()

    # MAP NAMES OF FEATURES AND TARGETS FOR CLASSIFICATION AND REGRESSION PROBLEMS
    val featuresIndOneHot = List("paymentVec", "vendorVec", "rateVec", "TrafficTimeBinsVec", "pickup_hour", "weekday", "passenger_count", "trip_time_in_secs", "trip_distance", "fare_amount").map(encodedFinalSampled.columns.indexOf(_))
    val featuresIndIndex = List("paymentIndex", "vendorIndex", "rateIndex", "TrafficTimeBinsIndex", "pickup_hour", "weekday", "passenger_count", "trip_time_in_secs", "trip_distance", "fare_amount").map(encodedFinalSampled.columns.indexOf(_))

    # SPECIFY THE TARGET FOR CLASSIFICATION ('tipped') AND REGRESSION ('tip_amount') PROBLEMS
    val targetIndBinary = List("tipped").map(encodedFinalSampled.columns.indexOf(_))
    val targetIndRegression = List("tip_amount").map(encodedFinalSampled.columns.indexOf(_))

    # CREATE INDEXED LABELED POINT RDD OBJECTS
    val indexedTRAINbinary = trainData.rdd.map(r => LabeledPoint(r.getDouble(targetIndBinary(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)))
    val indexedTESTbinary = testData.rdd.map(r => LabeledPoint(r.getDouble(targetIndBinary(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)))
    val indexedTRAINreg = trainData.rdd.map(r => LabeledPoint(r.getDouble(targetIndRegression(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)))
    val indexedTESTreg = testData.rdd.map(r => LabeledPoint(r.getDouble(targetIndRegression(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)))

    # CREATE INDEXED DATA FRAMES THAT YOU CAN USE TO TRAIN BY USING SPARK ML FUNCTIONS
    val indexedTRAINbinaryDF = indexedTRAINbinary.toDF()
    val indexedTESTbinaryDF = indexedTESTbinary.toDF()
    val indexedTRAINregDF = indexedTRAINreg.toDF()
    val indexedTESTregDF = indexedTESTreg.toDF()

    # CREATE ONE-HOT ENCODED (VECTORIZED) DATA FRAMES THAT YOU CAN USE TO TRAIN BY USING SPARK ML FUNCTIONS
    val assemblerOneHot = new VectorAssembler().setInputCols(Array("paymentVec", "vendorVec", "rateVec", "TrafficTimeBinsVec", "pickup_hour", "weekday", "passenger_count", "trip_time_in_secs", "trip_distance", "fare_amount")).setOutputCol("features")
    val OneHotTRAIN = assemblerOneHot.transform(trainData)
    val OneHotTEST = assemblerOneHot.transform(testData)

    # GET THE TIME TO RUN THE CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken to run the above cell: " + elapsedtime + " seconds.");


<span data-ttu-id="63609-287">**Output:**</span><span class="sxs-lookup"><span data-stu-id="63609-287">**Output:**</span></span>

<span data-ttu-id="63609-288">Time to run the cell: 4 seconds.</span><span class="sxs-lookup"><span data-stu-id="63609-288">Time to run the cell: 4 seconds.</span></span>

### <a name="automatically-categorize-and-vectorize-features-and-targets-to-use-as-inputs-for-machine-learning-models"></a><span data-ttu-id="63609-289">Automatically categorize and vectorize features and targets to use as inputs for machine learning models</span><span class="sxs-lookup"><span data-stu-id="63609-289">Automatically categorize and vectorize features and targets to use as inputs for machine learning models</span></span>
<span data-ttu-id="63609-290">Use Spark ML to categorize the target and features to use in tree-based modeling functions.</span><span class="sxs-lookup"><span data-stu-id="63609-290">Use Spark ML to categorize the target and features to use in tree-based modeling functions.</span></span> <span data-ttu-id="63609-291">The code completes two tasks:</span><span class="sxs-lookup"><span data-stu-id="63609-291">The code completes two tasks:</span></span>

* <span data-ttu-id="63609-292">Creates a binary target for classification by assigning a value of 0 or 1 to each data point between 0 and 1 by using a threshold value of 0.5.</span><span class="sxs-lookup"><span data-stu-id="63609-292">Creates a binary target for classification by assigning a value of 0 or 1 to each data point between 0 and 1 by using a threshold value of 0.5.</span></span>
* <span data-ttu-id="63609-293">Automatically categorizes features.</span><span class="sxs-lookup"><span data-stu-id="63609-293">Automatically categorizes features.</span></span> <span data-ttu-id="63609-294">If the number of distinct numerical values for any feature is less than 32, that feature is categorized.</span><span class="sxs-lookup"><span data-stu-id="63609-294">If the number of distinct numerical values for any feature is less than 32, that feature is categorized.</span></span>

<span data-ttu-id="63609-295">Here's the code for these two tasks.</span><span class="sxs-lookup"><span data-stu-id="63609-295">Here's the code for these two tasks.</span></span>

    # CATEGORIZE FEATURES AND BINARIZE THE TARGET FOR THE BINARY CLASSIFICATION PROBLEM

    # TRAIN DATA
    val indexer = new VectorIndexer().setInputCol("features").setOutputCol("featuresCat").setMaxCategories(32)
    val indexerModel = indexer.fit(indexedTRAINbinaryDF)
    val indexedTrainwithCatFeat = indexerModel.transform(indexedTRAINbinaryDF)
    val binarizer: Binarizer = new Binarizer().setInputCol("label").setOutputCol("labelBin").setThreshold(0.5)
    val indexedTRAINwithCatFeatBinTarget = binarizer.transform(indexedTrainwithCatFeat)

    # TEST DATA
    val indexerModel = indexer.fit(indexedTESTbinaryDF)
    val indexedTrainwithCatFeat = indexerModel.transform(indexedTESTbinaryDF)
    val binarizer: Binarizer = new Binarizer().setInputCol("label").setOutputCol("labelBin").setThreshold(0.5)
    val indexedTESTwithCatFeatBinTarget = binarizer.transform(indexedTrainwithCatFeat)

    # CATEGORIZE FEATURES FOR THE REGRESSION PROBLEM
    # CREATE PROPERLY INDEXED AND CATEGORIZED DATA FRAMES FOR TREE-BASED MODELS

    # TRAIN DATA
    val indexer = new VectorIndexer().setInputCol("features").setOutputCol("featuresCat").setMaxCategories(32)
    val indexerModel = indexer.fit(indexedTRAINregDF)
    val indexedTRAINwithCatFeat = indexerModel.transform(indexedTRAINregDF)

    # TEST DATA
    val indexerModel = indexer.fit(indexedTESTbinaryDF)
    val indexedTESTwithCatFeat = indexerModel.transform(indexedTESTregDF)



## <a name="binary-classification-model-predict-whether-a-tip-should-be-paid"></a><span data-ttu-id="63609-296">Binary classification model: Predict whether a tip should be paid</span><span class="sxs-lookup"><span data-stu-id="63609-296">Binary classification model: Predict whether a tip should be paid</span></span>
<span data-ttu-id="63609-297">In this section, you create three types of binary classification models to predict whether or not a tip should be paid:</span><span class="sxs-lookup"><span data-stu-id="63609-297">In this section, you create three types of binary classification models to predict whether or not a tip should be paid:</span></span>

* <span data-ttu-id="63609-298">A **logistic regression model** by using the Spark ML `LogisticRegression()` function</span><span class="sxs-lookup"><span data-stu-id="63609-298">A **logistic regression model** by using the Spark ML `LogisticRegression()` function</span></span>
* <span data-ttu-id="63609-299">A **random forest classification model** by using the Spark ML `RandomForestClassifier()` function</span><span class="sxs-lookup"><span data-stu-id="63609-299">A **random forest classification model** by using the Spark ML `RandomForestClassifier()` function</span></span>
* <span data-ttu-id="63609-300">A **gradient boosting tree classification model** by using the MLlib `GradientBoostedTrees()` function</span><span class="sxs-lookup"><span data-stu-id="63609-300">A **gradient boosting tree classification model** by using the MLlib `GradientBoostedTrees()` function</span></span>

### <a name="create-a-logistic-regression-model"></a><span data-ttu-id="63609-301">Create a logistic regression model</span><span class="sxs-lookup"><span data-stu-id="63609-301">Create a logistic regression model</span></span>
<span data-ttu-id="63609-302">Next, create a logistic regression model by using the Spark ML `LogisticRegression()` function.</span><span class="sxs-lookup"><span data-stu-id="63609-302">Next, create a logistic regression model by using the Spark ML `LogisticRegression()` function.</span></span> <span data-ttu-id="63609-303">You create the model building code in a series of steps:</span><span class="sxs-lookup"><span data-stu-id="63609-303">You create the model building code in a series of steps:</span></span>

1. <span data-ttu-id="63609-304">**Train the model** data with one parameter set.</span><span class="sxs-lookup"><span data-stu-id="63609-304">**Train the model** data with one parameter set.</span></span>
2. <span data-ttu-id="63609-305">**Evaluate the model** on a test data set with metrics.</span><span class="sxs-lookup"><span data-stu-id="63609-305">**Evaluate the model** on a test data set with metrics.</span></span>
3. <span data-ttu-id="63609-306">**Save the model** in Blob storage for future consumption.</span><span class="sxs-lookup"><span data-stu-id="63609-306">**Save the model** in Blob storage for future consumption.</span></span>
4. <span data-ttu-id="63609-307">**Score the model** against test data.</span><span class="sxs-lookup"><span data-stu-id="63609-307">**Score the model** against test data.</span></span>
5. <span data-ttu-id="63609-308">**Plot the results** with receiver operating characteristic (ROC) curves.</span><span class="sxs-lookup"><span data-stu-id="63609-308">**Plot the results** with receiver operating characteristic (ROC) curves.</span></span>

<span data-ttu-id="63609-309">Here's the code for these procedures:</span><span class="sxs-lookup"><span data-stu-id="63609-309">Here's the code for these procedures:</span></span>

    # CREATE A LOGISTIC REGRESSION MODEL
    val lr = new LogisticRegression().setLabelCol("tipped").setFeaturesCol("features").setMaxIter(10).setRegParam(0.3).setElasticNetParam(0.8)
    val lrModel = lr.fit(OneHotTRAIN)

    # PREDICT ON THE TEST DATA SET
    val predictions = lrModel.transform(OneHotTEST)

    # SELECT `BinaryClassificationEvaluator()` TO COMPUTE THE TEST ERROR
    val evaluator = new BinaryClassificationEvaluator().setLabelCol("tipped").setRawPredictionCol("probability").setMetricName("areaUnderROC")
    val ROC = evaluator.evaluate(predictions)
    println("ROC on test data = " + ROC)

    # SAVE THE MODEL
    val datestamp = Calendar.getInstance().getTime().toString.replaceAll(" ", ".").replaceAll(":", "_");
    val modelName = "LogisticRegression__"
    val filename = modelDir.concat(modelName).concat(datestamp)
    lrModel.save(filename);

<span data-ttu-id="63609-310">Load, score, and save the results.</span><span class="sxs-lookup"><span data-stu-id="63609-310">Load, score, and save the results.</span></span>

    # RECORD THE START TIME
    val starttime = Calendar.getInstance().getTime()

    # LOAD THE SAVED MODEL AND SCORE THE TEST DATA SET
    val savedModel = org.apache.spark.ml.classification.LogisticRegressionModel.load(filename)
    println(s"Coefficients: ${savedModel.coefficients} Intercept: ${savedModel.intercept}")

    # SCORE THE MODEL ON THE TEST DATA
    val predictions = savedModel.transform(OneHotTEST).select("tipped","probability","rawPrediction")
    predictions.registerTempTable("testResults")

    # SELECT `BinaryClassificationEvaluator()` TO COMPUTE THE TEST ERROR
    val evaluator = new BinaryClassificationEvaluator().setLabelCol("tipped").setRawPredictionCol("probability").setMetricName("areaUnderROC")
    val ROC = evaluator.evaluate(predictions)

    # GET THE TIME TO RUN THE CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken to run the above cell: " + elapsedtime + " seconds.");

    # PRINT THE ROC RESULTS
    println("ROC on test data = " + ROC)


<span data-ttu-id="63609-311">**Output:**</span><span class="sxs-lookup"><span data-stu-id="63609-311">**Output:**</span></span>

<span data-ttu-id="63609-312">ROC on test data = 0.9827381497557599</span><span class="sxs-lookup"><span data-stu-id="63609-312">ROC on test data = 0.9827381497557599</span></span>

<span data-ttu-id="63609-313">Use Python on local Pandas data frames to plot the ROC curve.</span><span class="sxs-lookup"><span data-stu-id="63609-313">Use Python on local Pandas data frames to plot the ROC curve.</span></span>

    # QUERY THE RESULTS
    %%sql -q -o sqlResults
    SELECT tipped, probability from testResults


    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    %matplotlib inline
    from sklearn.metrics import roc_curve,auc

    sqlResults['probFloat'] = sqlResults.apply(lambda row: row['probability'].values()[0][1], axis=1)
    predictions_pddf = sqlResults[["tipped","probFloat"]]

    # PREDICT THE ROC CURVE
    # predictions_pddf = sqlResults.rename(columns={'_1': 'probability', 'tipped': 'label'})
    prob = predictions_pddf["probFloat"]
    fpr, tpr, thresholds = roc_curve(predictions_pddf['tipped'], prob, pos_label=1);
    roc_auc = auc(fpr, tpr)

    # PLOT THE ROC CURVE
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


<span data-ttu-id="63609-314">**Output:**</span><span class="sxs-lookup"><span data-stu-id="63609-314">**Output:**</span></span>

![Tip or no tip ROC curve](./media/scala-walkthrough/plot-roc-curve-tip-or-not.png)

### <a name="create-a-random-forest-classification-model"></a><span data-ttu-id="63609-316">Create a random forest classification model</span><span class="sxs-lookup"><span data-stu-id="63609-316">Create a random forest classification model</span></span>
<span data-ttu-id="63609-317">Next, create a random forest classification model by using the Spark ML `RandomForestClassifier()` function, and then evaluate the model on test data.</span><span class="sxs-lookup"><span data-stu-id="63609-317">Next, create a random forest classification model by using the Spark ML `RandomForestClassifier()` function, and then evaluate the model on test data.</span></span>

    # RECORD THE START TIME
    val starttime = Calendar.getInstance().getTime()

    # CREATE THE RANDOM FOREST CLASSIFIER MODEL
    val rf = new RandomForestClassifier().setLabelCol("labelBin").setFeaturesCol("featuresCat").setNumTrees(10).setSeed(1234)

    # FIT THE MODEL
    val rfModel = rf.fit(indexedTRAINwithCatFeatBinTarget)
    val predictions = rfModel.transform(indexedTESTwithCatFeatBinTarget)

    # EVALUATE THE MODEL
    val evaluator = new MulticlassClassificationEvaluator().setLabelCol("label").setPredictionCol("prediction").setMetricName("f1")
    val Test_f1Score = evaluator.evaluate(predictions)
    println("F1 score on test data: " + Test_f1Score);

    # GET THE TIME TO RUN THE CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken to run the above cell: " + elapsedtime + " seconds.");

    # CALCULATE BINARY CLASSIFICATION EVALUATION METRICS
    val evaluator = new BinaryClassificationEvaluator().setLabelCol("label").setRawPredictionCol("probability").setMetricName("areaUnderROC")
    val ROC = evaluator.evaluate(predictions)
    println("ROC on test data = " + ROC)


<span data-ttu-id="63609-318">**Output:**</span><span class="sxs-lookup"><span data-stu-id="63609-318">**Output:**</span></span>

<span data-ttu-id="63609-319">ROC on test data = 0.9847103571552683</span><span class="sxs-lookup"><span data-stu-id="63609-319">ROC on test data = 0.9847103571552683</span></span>

### <a name="create-a-gbt-classification-model"></a><span data-ttu-id="63609-320">Create a GBT classification model</span><span class="sxs-lookup"><span data-stu-id="63609-320">Create a GBT classification model</span></span>
<span data-ttu-id="63609-321">Next, create a GBT classification model by using MLlib's `GradientBoostedTrees()` function, and then evaluate the model on test data.</span><span class="sxs-lookup"><span data-stu-id="63609-321">Next, create a GBT classification model by using MLlib's `GradientBoostedTrees()` function, and then evaluate the model on test data.</span></span>

    # TRAIN A GBT CLASSIFICATION MODEL BY USING MLLIB AND A LABELED POINT

    # RECORD THE START TIME
    val starttime = Calendar.getInstance().getTime()

    # DEFINE THE GBT CLASSIFICATION MODEL
    val boostingStrategy = BoostingStrategy.defaultParams("Classification")
    boostingStrategy.numIterations = 20
    boostingStrategy.treeStrategy.numClasses = 2
    boostingStrategy.treeStrategy.maxDepth = 5
    boostingStrategy.treeStrategy.categoricalFeaturesInfo = Map[Int, Int]((0,2),(1,2),(2,6),(3,4))

    # TRAIN THE MODEL
    val gbtModel = GradientBoostedTrees.train(indexedTRAINbinary, boostingStrategy)

    # SAVE THE MODEL IN BLOB STORAGE
    val datestamp = Calendar.getInstance().getTime().toString.replaceAll(" ", ".").replaceAll(":", "_");
    val modelName = "GBT_Classification__"
    val filename = modelDir.concat(modelName).concat(datestamp)
    gbtModel.save(sc, filename);

    # EVALUATE THE MODEL ON TEST INSTANCES AND THE COMPUTE TEST ERROR
    val labelAndPreds = indexedTESTbinary.map { point =>
      val prediction = gbtModel.predict(point.features)
      (point.label, prediction)
    }
    val testErr = labelAndPreds.filter(r => r._1 != r._2).count.toDouble / indexedTRAINbinary.count()
    //println("Learned classification GBT model:\n" + gbtModel.toDebugString)
    println("Test Error = " + testErr)

    # USE BINARY AND MULTICLASS METRICS TO EVALUATE THE MODEL ON THE TEST DATA
    val metrics = new MulticlassMetrics(labelAndPreds)
    println(s"Precision: ${metrics.precision}")
    println(s"Recall: ${metrics.recall}")
    println(s"F1 Score: ${metrics.fMeasure}")

    val metrics = new BinaryClassificationMetrics(labelAndPreds)
    println(s"Area under PR curve: ${metrics.areaUnderPR}")
    println(s"Area under ROC curve: ${metrics.areaUnderROC}")

    # GET THE TIME TO RUN THE CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken to run the above cell: " + elapsedtime + " seconds.");

    # PRINT THE ROC METRIC
    println(s"Area under ROC curve: ${metrics.areaUnderROC}")


<span data-ttu-id="63609-322">**Output:**</span><span class="sxs-lookup"><span data-stu-id="63609-322">**Output:**</span></span>

<span data-ttu-id="63609-323">Area under ROC curve: 0.9846895479241554</span><span class="sxs-lookup"><span data-stu-id="63609-323">Area under ROC curve: 0.9846895479241554</span></span>

## <a name="regression-model-predict-tip-amount"></a><span data-ttu-id="63609-324">Regression model: Predict tip amount</span><span class="sxs-lookup"><span data-stu-id="63609-324">Regression model: Predict tip amount</span></span>
<span data-ttu-id="63609-325">In this section, you create two types of regression models to predict the tip amount:</span><span class="sxs-lookup"><span data-stu-id="63609-325">In this section, you create two types of regression models to predict the tip amount:</span></span>

* <span data-ttu-id="63609-326">A **regularized linear regression model** by using the Spark ML `LinearRegression()` function.</span><span class="sxs-lookup"><span data-stu-id="63609-326">A **regularized linear regression model** by using the Spark ML `LinearRegression()` function.</span></span> <span data-ttu-id="63609-327">You'll save the model and evaluate the model on test data.</span><span class="sxs-lookup"><span data-stu-id="63609-327">You'll save the model and evaluate the model on test data.</span></span>
* <span data-ttu-id="63609-328">A **gradient-boosting tree regression model** by using the Spark ML `GBTRegressor()` function.</span><span class="sxs-lookup"><span data-stu-id="63609-328">A **gradient-boosting tree regression model** by using the Spark ML `GBTRegressor()` function.</span></span>

### <a name="create-a-regularized-linear-regression-model"></a><span data-ttu-id="63609-329">Create a regularized linear regression model</span><span class="sxs-lookup"><span data-stu-id="63609-329">Create a regularized linear regression model</span></span>
    # RECORD THE START TIME
    val starttime = Calendar.getInstance().getTime()

    # CREATE A REGULARIZED LINEAR REGRESSION MODEL BY USING THE SPARK ML FUNCTION AND DATA FRAMES
    val lr = new LinearRegression().setLabelCol("tip_amount").setFeaturesCol("features").setMaxIter(10).setRegParam(0.3).setElasticNetParam(0.8)

    # FIT THE MODEL BY USING DATA FRAMES
    val lrModel = lr.fit(OneHotTRAIN)
    println(s"Coefficients: ${lrModel.coefficients} Intercept: ${lrModel.intercept}")

    # SUMMARIZE THE MODEL OVER THE TRAINING SET AND PRINT METRICS
    val trainingSummary = lrModel.summary
    println(s"numIterations: ${trainingSummary.totalIterations}")
    println(s"objectiveHistory: ${trainingSummary.objectiveHistory.toList}")
    trainingSummary.residuals.show()
    println(s"RMSE: ${trainingSummary.rootMeanSquaredError}")
    println(s"r2: ${trainingSummary.r2}")

    # SAVE THE MODEL IN AZURE BLOB STORAGE
    val datestamp = Calendar.getInstance().getTime().toString.replaceAll(" ", ".").replaceAll(":", "_");
    val modelName = "LinearRegression__"
    val filename = modelDir.concat(modelName).concat(datestamp)
    lrModel.save(filename);

    # PRINT THE COEFFICIENTS
    println(s"Coefficients: ${lrModel.coefficients} Intercept: ${lrModel.intercept}")

    # SCORE THE MODEL ON TEST DATA
    val predictions = lrModel.transform(OneHotTEST)

    # EVALUATE THE MODEL ON TEST DATA
    val evaluator = new RegressionEvaluator().setLabelCol("tip_amount").setPredictionCol("prediction").setMetricName("r2")
    val r2 = evaluator.evaluate(predictions)
    println("R-sqr on test data = " + r2)

    # GET THE TIME TO RUN THE CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken to run the above cell: " + elapsedtime + " seconds.");


<span data-ttu-id="63609-330">**Output:**</span><span class="sxs-lookup"><span data-stu-id="63609-330">**Output:**</span></span>

<span data-ttu-id="63609-331">Time to run the cell: 13 seconds.</span><span class="sxs-lookup"><span data-stu-id="63609-331">Time to run the cell: 13 seconds.</span></span>

    # LOAD A SAVED LINEAR REGRESSION MODEL FROM BLOB STORAGE AND SCORE A TEST DATA SET

    # RECORD THE START TIME
    val starttime = Calendar.getInstance().getTime()

    # LOAD A SAVED LINEAR REGRESSION MODEL FROM AZURE BLOB STORAGE
    val savedModel = org.apache.spark.ml.regression.LinearRegressionModel.load(filename)
    println(s"Coefficients: ${savedModel.coefficients} Intercept: ${savedModel.intercept}")

    # SCORE THE MODEL ON TEST DATA
    val predictions = savedModel.transform(OneHotTEST).select("tip_amount","prediction")
    predictions.registerTempTable("testResults")

    # EVALUATE THE MODEL ON TEST DATA
    val evaluator = new RegressionEvaluator().setLabelCol("tip_amount").setPredictionCol("prediction").setMetricName("r2")
    val r2 = evaluator.evaluate(predictions)
    println("R-sqr on test data = " + r2)

    # GET THE TIME TO RUN THE CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken to run the above cell: " + elapsedtime + " seconds.");

    # PRINT THE RESULTS
    println("R-sqr on test data = " + r2)


<span data-ttu-id="63609-332">**Output:**</span><span class="sxs-lookup"><span data-stu-id="63609-332">**Output:**</span></span>

<span data-ttu-id="63609-333">R-sqr on test data = 0.5960320470835743</span><span class="sxs-lookup"><span data-stu-id="63609-333">R-sqr on test data = 0.5960320470835743</span></span>

<span data-ttu-id="63609-334">Next, query the test results as a data frame and use AutoVizWidget and matplotlib to visualize it.</span><span class="sxs-lookup"><span data-stu-id="63609-334">Next, query the test results as a data frame and use AutoVizWidget and matplotlib to visualize it.</span></span>

    # RUN A SQL QUERY
    %%sql -q -o sqlResults
    select * from testResults

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER
    %%local

    # USE THE JUPYTER AUTO-PLOTTING FEATURE TO CREATE INTERACTIVE FIGURES
    # CLICK THE TYPE OF PLOT TO GENERATE (LINE, AREA, BAR, AND SO ON)
    sqlResults

<span data-ttu-id="63609-335">The code creates a local data frame from the query output and plots the data.</span><span class="sxs-lookup"><span data-stu-id="63609-335">The code creates a local data frame from the query output and plots the data.</span></span> <span data-ttu-id="63609-336">The `%%local` magic creates a local data frame, `sqlResults`, which you can use to plot with matplotlib.</span><span class="sxs-lookup"><span data-stu-id="63609-336">The `%%local` magic creates a local data frame, `sqlResults`, which you can use to plot with matplotlib.</span></span>

> [!NOTE]
> <span data-ttu-id="63609-337">This Spark magic is used multiple times in this article.</span><span class="sxs-lookup"><span data-stu-id="63609-337">This Spark magic is used multiple times in this article.</span></span> <span data-ttu-id="63609-338">If the amount of data is large, you should sample to create a data frame that can fit in local memory.</span><span class="sxs-lookup"><span data-stu-id="63609-338">If the amount of data is large, you should sample to create a data frame that can fit in local memory.</span></span>
> 
> 

<span data-ttu-id="63609-339">Create plots by using Python matplotlib.</span><span class="sxs-lookup"><span data-stu-id="63609-339">Create plots by using Python matplotlib.</span></span>

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    sqlResults
    %matplotlib inline
    import numpy as np

    # PLOT THE RESULTS
    ax = sqlResults.plot(kind='scatter', figsize = (6,6), x='tip_amount', y='prediction', color='blue', alpha = 0.25, label='Actual vs. predicted');
    fit = np.polyfit(sqlResults['tip_amount'], sqlResults['prediction'], deg=1)
    ax.set_title('Actual vs. Predicted Tip Amounts ($)')
    ax.set_xlabel("Actual")
    ax.set_ylabel("Predicted")
    #ax.plot(sqlResults['tip_amount'], fit[0] * sqlResults['prediction'] + fit[1], color='magenta')
    plt.axis([-1, 15, -1, 8])
    plt.show(ax)

<span data-ttu-id="63609-340">**Output:**</span><span class="sxs-lookup"><span data-stu-id="63609-340">**Output:**</span></span>

![Tip amount: Actual vs. predicted](./media/scala-walkthrough/plot-actual-vs-predicted-tip-amount.png)

### <a name="create-a-gbt-regression-model"></a><span data-ttu-id="63609-342">Create a GBT regression model</span><span class="sxs-lookup"><span data-stu-id="63609-342">Create a GBT regression model</span></span>
<span data-ttu-id="63609-343">Create a GBT regression model by using the Spark ML `GBTRegressor()` function, and then evaluate the model on test data.</span><span class="sxs-lookup"><span data-stu-id="63609-343">Create a GBT regression model by using the Spark ML `GBTRegressor()` function, and then evaluate the model on test data.</span></span>

<span data-ttu-id="63609-344">[Gradient-boosted trees](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) are ensembles of decision trees.</span><span class="sxs-lookup"><span data-stu-id="63609-344">[Gradient-boosted trees](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) are ensembles of decision trees.</span></span> <span data-ttu-id="63609-345">GBTs train decision trees iteratively to minimize a loss function.</span><span class="sxs-lookup"><span data-stu-id="63609-345">GBTs train decision trees iteratively to minimize a loss function.</span></span> <span data-ttu-id="63609-346">You can use GBTs for regression and classification.</span><span class="sxs-lookup"><span data-stu-id="63609-346">You can use GBTs for regression and classification.</span></span> <span data-ttu-id="63609-347">They can handle categorical features, do not require feature scaling, and can capture nonlinearities and feature interactions.</span><span class="sxs-lookup"><span data-stu-id="63609-347">They can handle categorical features, do not require feature scaling, and can capture nonlinearities and feature interactions.</span></span> <span data-ttu-id="63609-348">You also can use them in a multiclass-classification setting.</span><span class="sxs-lookup"><span data-stu-id="63609-348">You also can use them in a multiclass-classification setting.</span></span>

    # RECORD THE START TIME
    val starttime = Calendar.getInstance().getTime()

    # TRAIN A GBT REGRESSION MODEL
    val gbt = new GBTRegressor().setLabelCol("label").setFeaturesCol("featuresCat").setMaxIter(10)
    val gbtModel = gbt.fit(indexedTRAINwithCatFeat)

    # MAKE PREDICTIONS
    val predictions = gbtModel.transform(indexedTESTwithCatFeat)

    # COMPUTE TEST SET R2
    val evaluator = new RegressionEvaluator().setLabelCol("label").setPredictionCol("prediction").setMetricName("r2")
    val Test_R2 = evaluator.evaluate(predictions)


    # GET THE TIME TO RUN THE CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken to run the above cell: " + elapsedtime + " seconds.");

    # PRINT THE RESULTS
    println("Test R-sqr is: " + Test_R2);


<span data-ttu-id="63609-349">**Output:**</span><span class="sxs-lookup"><span data-stu-id="63609-349">**Output:**</span></span>

<span data-ttu-id="63609-350">Test R-sqr is: 0.7655383534596654</span><span class="sxs-lookup"><span data-stu-id="63609-350">Test R-sqr is: 0.7655383534596654</span></span>

## <a name="advanced-modeling-utilities-for-optimization"></a><span data-ttu-id="63609-351">Advanced modeling utilities for optimization</span><span class="sxs-lookup"><span data-stu-id="63609-351">Advanced modeling utilities for optimization</span></span>
<span data-ttu-id="63609-352">In this section, you use machine learning utilities that developers frequently use for model optimization.</span><span class="sxs-lookup"><span data-stu-id="63609-352">In this section, you use machine learning utilities that developers frequently use for model optimization.</span></span> <span data-ttu-id="63609-353">Specifically, you can optimize machine learning models three different ways by using parameter sweeping and cross-validation:</span><span class="sxs-lookup"><span data-stu-id="63609-353">Specifically, you can optimize machine learning models three different ways by using parameter sweeping and cross-validation:</span></span>

* <span data-ttu-id="63609-354">Split the data into train and validation sets, optimize the model by using hyper-parameter sweeping on a training set, and evaluate on a validation set (linear regression)</span><span class="sxs-lookup"><span data-stu-id="63609-354">Split the data into train and validation sets, optimize the model by using hyper-parameter sweeping on a training set, and evaluate on a validation set (linear regression)</span></span>
* <span data-ttu-id="63609-355">Optimize the model by using cross-validation and hyper-parameter sweeping by using Spark ML's CrossValidator function (binary classification)</span><span class="sxs-lookup"><span data-stu-id="63609-355">Optimize the model by using cross-validation and hyper-parameter sweeping by using Spark ML's CrossValidator function (binary classification)</span></span>
* <span data-ttu-id="63609-356">Optimize the model by using custom cross-validation and parameter-sweeping code to use any machine learning function and parameter set (linear regression)</span><span class="sxs-lookup"><span data-stu-id="63609-356">Optimize the model by using custom cross-validation and parameter-sweeping code to use any machine learning function and parameter set (linear regression)</span></span>

<span data-ttu-id="63609-357">**Cross-validation** is a technique that assesses how well a model trained on a known set of data will generalize to predict the features of data sets on which it has not been trained.</span><span class="sxs-lookup"><span data-stu-id="63609-357">**Cross-validation** is a technique that assesses how well a model trained on a known set of data will generalize to predict the features of data sets on which it has not been trained.</span></span> <span data-ttu-id="63609-358">The general idea behind this technique is that a model is trained on a data set of known data, and then the accuracy of its predictions is tested against an independent data set.</span><span class="sxs-lookup"><span data-stu-id="63609-358">The general idea behind this technique is that a model is trained on a data set of known data, and then the accuracy of its predictions is tested against an independent data set.</span></span> <span data-ttu-id="63609-359">A common implementation is to divide a data set into *k*-folds, and then train the model in a round-robin fashion on all but one of the folds.</span><span class="sxs-lookup"><span data-stu-id="63609-359">A common implementation is to divide a data set into *k*-folds, and then train the model in a round-robin fashion on all but one of the folds.</span></span>

<span data-ttu-id="63609-360">**Hyper-parameter optimization** is the problem of choosing a set of hyper-parameters for a learning algorithm, usually with the goal of optimizing a measure of the algorithm's performance on an independent data set.</span><span class="sxs-lookup"><span data-stu-id="63609-360">**Hyper-parameter optimization** is the problem of choosing a set of hyper-parameters for a learning algorithm, usually with the goal of optimizing a measure of the algorithm's performance on an independent data set.</span></span> <span data-ttu-id="63609-361">A hyper-parameter is a value that you must specify outside the model training procedure.</span><span class="sxs-lookup"><span data-stu-id="63609-361">A hyper-parameter is a value that you must specify outside the model training procedure.</span></span> <span data-ttu-id="63609-362">Assumptions about hyper-parameter values can affect the flexibility and accuracy of the model.</span><span class="sxs-lookup"><span data-stu-id="63609-362">Assumptions about hyper-parameter values can affect the flexibility and accuracy of the model.</span></span> <span data-ttu-id="63609-363">Decision trees have hyper-parameters, for example, such as the desired depth and number of leaves in the tree.</span><span class="sxs-lookup"><span data-stu-id="63609-363">Decision trees have hyper-parameters, for example, such as the desired depth and number of leaves in the tree.</span></span> <span data-ttu-id="63609-364">You must set a misclassification penalty term for a support vector machine (SVM).</span><span class="sxs-lookup"><span data-stu-id="63609-364">You must set a misclassification penalty term for a support vector machine (SVM).</span></span>

<span data-ttu-id="63609-365">A common way to perform hyper-parameter optimization is to use a grid search, also called a **parameter sweep**.</span><span class="sxs-lookup"><span data-stu-id="63609-365">A common way to perform hyper-parameter optimization is to use a grid search, also called a **parameter sweep**.</span></span> <span data-ttu-id="63609-366">In a grid search, an exhaustive search is performed through the values of a specified subset of the hyper-parameter space for a learning algorithm.</span><span class="sxs-lookup"><span data-stu-id="63609-366">In a grid search, an exhaustive search is performed through the values of a specified subset of the hyper-parameter space for a learning algorithm.</span></span> <span data-ttu-id="63609-367">Cross-validation can supply a performance metric to sort out the optimal results produced by the grid search algorithm.</span><span class="sxs-lookup"><span data-stu-id="63609-367">Cross-validation can supply a performance metric to sort out the optimal results produced by the grid search algorithm.</span></span> <span data-ttu-id="63609-368">If you use cross-validation hyper-parameter sweeping, you can help limit problems like overfitting a model to training data.</span><span class="sxs-lookup"><span data-stu-id="63609-368">If you use cross-validation hyper-parameter sweeping, you can help limit problems like overfitting a model to training data.</span></span> <span data-ttu-id="63609-369">This way, the model retains the capacity to apply to the general set of data from which the training data was extracted.</span><span class="sxs-lookup"><span data-stu-id="63609-369">This way, the model retains the capacity to apply to the general set of data from which the training data was extracted.</span></span>

### <a name="optimize-a-linear-regression-model-with-hyper-parameter-sweeping"></a><span data-ttu-id="63609-370">Optimize a linear regression model with hyper-parameter sweeping</span><span class="sxs-lookup"><span data-stu-id="63609-370">Optimize a linear regression model with hyper-parameter sweeping</span></span>
<span data-ttu-id="63609-371">Next, split data into train and validation sets, use hyper-parameter sweeping on a training set to optimize the model, and evaluate on a validation set (linear regression).</span><span class="sxs-lookup"><span data-stu-id="63609-371">Next, split data into train and validation sets, use hyper-parameter sweeping on a training set to optimize the model, and evaluate on a validation set (linear regression).</span></span>

    # RECORD THE START TIME
    val starttime = Calendar.getInstance().getTime()

    # RENAME `tip_amount` AS A LABEL
    val OneHotTRAINLabeled = OneHotTRAIN.select("tip_amount","features").withColumnRenamed(existingName="tip_amount",newName="label")
    val OneHotTESTLabeled = OneHotTEST.select("tip_amount","features").withColumnRenamed(existingName="tip_amount",newName="label")
    OneHotTRAINLabeled.cache()
    OneHotTESTLabeled.cache()

    # DEFINE THE ESTIMATOR FUNCTION: `THE LinearRegression()` FUNCTION
    val lr = new LinearRegression().setLabelCol("label").setFeaturesCol("features").setMaxIter(10)

    # DEFINE THE PARAMETER GRID
    val paramGrid = new ParamGridBuilder().addGrid(lr.regParam, Array(0.1, 0.01, 0.001)).addGrid(lr.fitIntercept).addGrid(lr.elasticNetParam, Array(0.1, 0.5, 0.9)).build()

    # DEFINE THE PIPELINE WITH A TRAIN/TEST VALIDATION SPLIT (75% IN THE TRAINING SET), AND THEN THE SPECIFY ESTIMATOR, EVALUATOR, AND PARAMETER GRID
    val trainPct = 0.75
    val trainValidationSplit = new TrainValidationSplit().setEstimator(lr).setEvaluator(new RegressionEvaluator).setEstimatorParamMaps(paramGrid).setTrainRatio(trainPct)

    # RUN THE TRAIN VALIDATION SPLIT AND CHOOSE THE BEST SET OF PARAMETERS
    val model = trainValidationSplit.fit(OneHotTRAINLabeled)

    # MAKE PREDICTIONS ON THE TEST DATA BY USING THE MODEL WITH THE COMBINATION OF PARAMETERS THAT PERFORMS THE BEST
    val testResults = model.transform(OneHotTESTLabeled).select("label", "prediction")

    # COMPUTE TEST SET R2
    val evaluator = new RegressionEvaluator().setLabelCol("label").setPredictionCol("prediction").setMetricName("r2")
    val Test_R2 = evaluator.evaluate(testResults)

    # GET THE TIME TO RUN THE CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken to run the above cell: " + elapsedtime + " seconds.");

    println("Test R-sqr is: " + Test_R2);


<span data-ttu-id="63609-372">**Output:**</span><span class="sxs-lookup"><span data-stu-id="63609-372">**Output:**</span></span>

<span data-ttu-id="63609-373">Test R-sqr is: 0.6226484708501209</span><span class="sxs-lookup"><span data-stu-id="63609-373">Test R-sqr is: 0.6226484708501209</span></span>

### <a name="optimize-the-binary-classification-model-by-using-cross-validation-and-hyper-parameter-sweeping"></a><span data-ttu-id="63609-374">Optimize the binary classification model by using cross-validation and hyper-parameter sweeping</span><span class="sxs-lookup"><span data-stu-id="63609-374">Optimize the binary classification model by using cross-validation and hyper-parameter sweeping</span></span>
<span data-ttu-id="63609-375">This section shows you how to optimize a binary classification model by using cross-validation and hyper-parameter sweeping.</span><span class="sxs-lookup"><span data-stu-id="63609-375">This section shows you how to optimize a binary classification model by using cross-validation and hyper-parameter sweeping.</span></span> <span data-ttu-id="63609-376">This uses the Spark ML `CrossValidator` function.</span><span class="sxs-lookup"><span data-stu-id="63609-376">This uses the Spark ML `CrossValidator` function.</span></span>

    # RECORD THE START TIME
    val starttime = Calendar.getInstance().getTime()

    # CREATE DATA FRAMES WITH PROPERLY LABELED COLUMNS TO USE WITH THE TRAIN AND TEST SPLIT
    val indexedTRAINwithCatFeatBinTargetRF = indexedTRAINwithCatFeatBinTarget.select("labelBin","featuresCat").withColumnRenamed(existingName="labelBin",newName="label").withColumnRenamed(existingName="featuresCat",newName="features")
    val indexedTESTwithCatFeatBinTargetRF = indexedTESTwithCatFeatBinTarget.select("labelBin","featuresCat").withColumnRenamed(existingName="labelBin",newName="label").withColumnRenamed(existingName="featuresCat",newName="features")
    indexedTRAINwithCatFeatBinTargetRF.cache()
    indexedTESTwithCatFeatBinTargetRF.cache()

    # DEFINE THE ESTIMATOR FUNCTION
    val rf = new RandomForestClassifier().setLabelCol("label").setFeaturesCol("features").setImpurity("gini").setSeed(1234).setFeatureSubsetStrategy("auto").setMaxBins(32)

    # DEFINE THE PARAMETER GRID
    val paramGrid = new ParamGridBuilder().addGrid(rf.maxDepth, Array(4,8)).addGrid(rf.numTrees, Array(5,10)).addGrid(rf.minInstancesPerNode, Array(100,300)).build()

    # SPECIFY THE NUMBER OF FOLDS
    val numFolds = 3

    # DEFINE THE TRAIN/TEST VALIDATION SPLIT (75% IN THE TRAINING SET)
    val CrossValidator = new CrossValidator().setEstimator(rf).setEvaluator(new BinaryClassificationEvaluator).setEstimatorParamMaps(paramGrid).setNumFolds(numFolds)

    # RUN THE TRAIN VALIDATION SPLIT AND CHOOSE THE BEST SET OF PARAMETERS
    val model = CrossValidator.fit(indexedTRAINwithCatFeatBinTargetRF)

    # MAKE PREDICTIONS ON THE TEST DATA BY USING THE MODEL WITH THE COMBINATION OF PARAMETERS THAT PERFORMS THE BEST
    val testResults = model.transform(indexedTESTwithCatFeatBinTargetRF).select("label", "prediction")

    # COMPUTE THE TEST F1 SCORE
    val evaluator = new MulticlassClassificationEvaluator().setLabelCol("label").setPredictionCol("prediction").setMetricName("f1")
    val Test_f1Score = evaluator.evaluate(testResults)

    # GET THE TIME TO RUN THE CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken to run the above cell: " + elapsedtime + " seconds.");


<span data-ttu-id="63609-377">**Output:**</span><span class="sxs-lookup"><span data-stu-id="63609-377">**Output:**</span></span>

<span data-ttu-id="63609-378">Time to run the cell: 33 seconds.</span><span class="sxs-lookup"><span data-stu-id="63609-378">Time to run the cell: 33 seconds.</span></span>

### <a name="optimize-the-linear-regression-model-by-using-custom-cross-validation-and-parameter-sweeping-code"></a><span data-ttu-id="63609-379">Optimize the linear regression model by using custom cross-validation and parameter-sweeping code</span><span class="sxs-lookup"><span data-stu-id="63609-379">Optimize the linear regression model by using custom cross-validation and parameter-sweeping code</span></span>
<span data-ttu-id="63609-380">Next, optimize the model by using custom code, and identify the best model parameters by using the criterion of highest accuracy.</span><span class="sxs-lookup"><span data-stu-id="63609-380">Next, optimize the model by using custom code, and identify the best model parameters by using the criterion of highest accuracy.</span></span> <span data-ttu-id="63609-381">Then, create the final model, evaluate the model on test data, and save the model in Blob storage.</span><span class="sxs-lookup"><span data-stu-id="63609-381">Then, create the final model, evaluate the model on test data, and save the model in Blob storage.</span></span> <span data-ttu-id="63609-382">Finally, load the model, score test data, and evaluate accuracy.</span><span class="sxs-lookup"><span data-stu-id="63609-382">Finally, load the model, score test data, and evaluate accuracy.</span></span>

    # RECORD THE START TIME
    val starttime = Calendar.getInstance().getTime()

    # DEFINE THE PARAMETER GRID AND THE NUMBER OF FOLDS
    val paramGrid = new ParamGridBuilder().addGrid(rf.maxDepth, Array(5,10)).addGrid(rf.numTrees, Array(10,25,50)).build()

    val nFolds = 3
    val numModels = paramGrid.size
    val numParamsinGrid = 2

    # SPECIFY THE NUMBER OF CATEGORIES FOR CATEGORICAL VARIABLES
    val categoricalFeaturesInfo = Map[Int, Int]((0,2),(1,2),(2,6),(3,4))

    var maxDepth = -1
    var numTrees = -1
    var param = ""
    var paramval = -1
    var validateLB = -1.0
    var validateUB = -1.0
    val h = 1.0 / nFolds;
    val RMSE  = Array.fill(numModels)(0.0)

    # CREATE K-FOLDS
    val splits = MLUtils.kFold(indexedTRAINbinary, numFolds = nFolds, seed=1234)


    # LOOP THROUGH K-FOLDS AND THE PARAMETER GRID TO GET AND IDENTIFY THE BEST PARAMETER SET BY LEVEL OF ACCURACY
    for (i <- 0 to (nFolds-1)) {
        validateLB = i * h
        validateUB = (i + 1) * h
        val validationCV = trainData.filter($"rand" >= validateLB  && $"rand" < validateUB)
        val trainCV = trainData.filter($"rand" < validateLB  || $"rand" >= validateUB)
        val validationLabPt = validationCV.rdd.map(r => LabeledPoint(r.getDouble(targetIndRegression(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)));
        val trainCVLabPt = trainCV.rdd.map(r => LabeledPoint(r.getDouble(targetIndRegression(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)));
        validationLabPt.cache()
        trainCVLabPt.cache()

        for (nParamSets <- 0 to (numModels-1)) {
            for (nParams <- 0 to (numParamsinGrid-1)) {
                param = paramGrid(nParamSets).toSeq(nParams).param.toString.split("__")(1)
                paramval = paramGrid(nParamSets).toSeq(nParams).value.toString.toInt
                if (param == "maxDepth") {maxDepth = paramval}
                if (param == "numTrees") {numTrees = paramval}
            }
            val rfModel = RandomForest.trainRegressor(trainCVLabPt, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                                      numTrees=numTrees, maxDepth=maxDepth,
                                                      featureSubsetStrategy="auto",impurity="variance", maxBins=32)
            val labelAndPreds = validationLabPt.map { point =>
                                                     val prediction = rfModel.predict(point.features)
                                                     ( prediction, point.label )
                                                    }
            val validMetrics = new RegressionMetrics(labelAndPreds)
            val rmse = validMetrics.rootMeanSquaredError
            RMSE(nParamSets) += rmse
        }
        validationLabPt.unpersist();
        trainCVLabPt.unpersist();
    }
    val minRMSEindex = RMSE.indexOf(RMSE.min)

    # GET THE BEST PARAMETERS FROM A CROSS-VALIDATION AND PARAMETER SWEEP
    var best_maxDepth = -1
    var best_numTrees = -1
    for (nParams <- 0 to (numParamsinGrid-1)) {
        param = paramGrid(minRMSEindex).toSeq(nParams).param.toString.split("__")(1)
        paramval = paramGrid(minRMSEindex).toSeq(nParams).value.toString.toInt
        if (param == "maxDepth") {best_maxDepth = paramval}
        if (param == "numTrees") {best_numTrees = paramval}
    }

    # CREATE THE BEST MODEL WITH THE BEST PARAMETERS AND A FULL TRAINING DATA SET
    val best_rfModel = RandomForest.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                                      numTrees=best_numTrees, maxDepth=best_maxDepth,
                                                      featureSubsetStrategy="auto",impurity="variance", maxBins=32)

    # SAVE THE BEST RANDOM FOREST MODEL IN BLOB STORAGE
    val datestamp = Calendar.getInstance().getTime().toString.replaceAll(" ", ".").replaceAll(":", "_");
    val modelName = "BestCV_RF_Regression__"
    val filename = modelDir.concat(modelName).concat(datestamp)
    best_rfModel.save(sc, filename);

    # PREDICT ON THE TRAINING SET WITH THE BEST MODEL AND THEN EVALUATE
    val labelAndPreds = indexedTESTreg.map { point =>
                                            val prediction = best_rfModel.predict(point.features)
                                            ( prediction, point.label )
                                           }

    val test_rmse = new RegressionMetrics(labelAndPreds).rootMeanSquaredError
    val test_rsqr = new RegressionMetrics(labelAndPreds).r2

    # GET THE TIME TO RUN THE CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken to run the above cell: " + elapsedtime + " seconds.");


    # LOAD THE MODEL
    val savedRFModel = RandomForestModel.load(sc, filename)

    val labelAndPreds = indexedTESTreg.map { point =>
                                            val prediction = savedRFModel.predict(point.features)
                                            ( prediction, point.label )
                                           }
    # TEST THE MODEL
    val test_rmse = new RegressionMetrics(labelAndPreds).rootMeanSquaredError
    val test_rsqr = new RegressionMetrics(labelAndPreds).r2


<span data-ttu-id="63609-383">**Output:**</span><span class="sxs-lookup"><span data-stu-id="63609-383">**Output:**</span></span>

<span data-ttu-id="63609-384">Time to run the cell: 61 seconds.</span><span class="sxs-lookup"><span data-stu-id="63609-384">Time to run the cell: 61 seconds.</span></span>

## <a name="consume-spark-built-machine-learning-models-automatically-with-scala"></a><span data-ttu-id="63609-385">Consume Spark-built machine learning models automatically with Scala</span><span class="sxs-lookup"><span data-stu-id="63609-385">Consume Spark-built machine learning models automatically with Scala</span></span>
<span data-ttu-id="63609-386">For an overview of topics that walk you through the tasks that comprise the Data Science process in Azure, see [Team Data Science Process](http://aka.ms/datascienceprocess).</span><span class="sxs-lookup"><span data-stu-id="63609-386">For an overview of topics that walk you through the tasks that comprise the Data Science process in Azure, see [Team Data Science Process](http://aka.ms/datascienceprocess).</span></span>

<span data-ttu-id="63609-387">[Team Data Science Process walkthroughs](walkthroughs.md) describes other end-to-end walkthroughs that demonstrate the steps in the Team Data Science Process for specific scenarios.</span><span class="sxs-lookup"><span data-stu-id="63609-387">[Team Data Science Process walkthroughs](walkthroughs.md) describes other end-to-end walkthroughs that demonstrate the steps in the Team Data Science Process for specific scenarios.</span></span> <span data-ttu-id="63609-388">The walkthroughs also illustrate how to combine cloud and on-premises tools and services into a workflow or pipeline to create an intelligent application.</span><span class="sxs-lookup"><span data-stu-id="63609-388">The walkthroughs also illustrate how to combine cloud and on-premises tools and services into a workflow or pipeline to create an intelligent application.</span></span>

<span data-ttu-id="63609-389">[Score Spark-built machine learning models](spark-model-consumption.md) shows you how to use Scala code to automatically load and score new data sets with machine learning models built in Spark and saved in Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="63609-389">[Score Spark-built machine learning models](spark-model-consumption.md) shows you how to use Scala code to automatically load and score new data sets with machine learning models built in Spark and saved in Azure Blob storage.</span></span> <span data-ttu-id="63609-390">You can follow the instructions provided there, and simply replace the Python code with Scala code in this article for automated consumption.</span><span class="sxs-lookup"><span data-stu-id="63609-390">You can follow the instructions provided there, and simply replace the Python code with Scala code in this article for automated consumption.</span></span>

