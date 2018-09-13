---
title: How to Use MMLSpark Machine Learning | Microsoft Docs
description: Guide how to use MMLSpark library with Azure Machine Learning.
services: machine-learning
author: rastala
ms.author: roastala
manager: jhubbard
ms.reviewer: garyericson, jasonwhowell, mldocs
ms.service: machine-learning
ms.component: core
ms.workload: data-services
ms.topic: article
ms.date: 01/12/2018
ms.openlocfilehash: 654b2559518cd52978153310fbb1e89a91838a8a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866845"
---
# <a name="how-to-use-microsoft-machine-learning-library-for-apache-spark"></a><span data-ttu-id="fe2fd-103">How to Use Microsoft Machine Learning Library for Apache Spark</span><span class="sxs-lookup"><span data-stu-id="fe2fd-103">How to Use Microsoft Machine Learning Library for Apache Spark</span></span>

## <a name="introduction"></a><span data-ttu-id="fe2fd-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="fe2fd-104">Introduction</span></span>

<span data-ttu-id="fe2fd-105">[Microsoft Machine Learning Library for Apache Spark](https://github.com/Azure/mmlspark) (MMLSpark)  provides tools that let you easily create scalable machine learning models for large datasets.</span><span class="sxs-lookup"><span data-stu-id="fe2fd-105">[Microsoft Machine Learning Library for Apache Spark](https://github.com/Azure/mmlspark) (MMLSpark)  provides tools that let you easily create scalable machine learning models for large datasets.</span></span> <span data-ttu-id="fe2fd-106">It includes integration of SparkML pipelines with the [Microsoft Cognitive Toolkit ](https://github.com/Microsoft/CNTK) and [OpenCV](http://www.opencv.org/), enabling you to:</span><span class="sxs-lookup"><span data-stu-id="fe2fd-106">It includes integration of SparkML pipelines with the [Microsoft Cognitive Toolkit ](https://github.com/Microsoft/CNTK) and [OpenCV](http://www.opencv.org/), enabling you to:</span></span> 
 * <span data-ttu-id="fe2fd-107">Ingress and pre-process image data</span><span class="sxs-lookup"><span data-stu-id="fe2fd-107">Ingress and pre-process image data</span></span>
 * <span data-ttu-id="fe2fd-108">Featurize images and text using pre-trained deep learning models</span><span class="sxs-lookup"><span data-stu-id="fe2fd-108">Featurize images and text using pre-trained deep learning models</span></span>
 * <span data-ttu-id="fe2fd-109">Train and score classification and regression models using implicit featurization.</span><span class="sxs-lookup"><span data-stu-id="fe2fd-109">Train and score classification and regression models using implicit featurization.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fe2fd-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="fe2fd-110">Prerequisites</span></span>

<span data-ttu-id="fe2fd-111">To step through this how-to guide, you need to:</span><span class="sxs-lookup"><span data-stu-id="fe2fd-111">To step through this how-to guide, you need to:</span></span>
- [<span data-ttu-id="fe2fd-112">Install Azure Machine Learning Workbench</span><span class="sxs-lookup"><span data-stu-id="fe2fd-112">Install Azure Machine Learning Workbench</span></span>](../service/quickstart-installation.md)
- [<span data-ttu-id="fe2fd-113">Set up Azure HDInsight Spark cluster</span><span class="sxs-lookup"><span data-stu-id="fe2fd-113">Set up Azure HDInsight Spark cluster</span></span>](https://docs.microsoft.com/azure/hdinsight/hdinsight-apache-spark-jupyter-spark-sql)

## <a name="run-your-experiment-in-docker-container"></a><span data-ttu-id="fe2fd-114">Run Your Experiment in Docker Container</span><span class="sxs-lookup"><span data-stu-id="fe2fd-114">Run Your Experiment in Docker Container</span></span>

<span data-ttu-id="fe2fd-115">Your Azure Machine Learning Workbench is configured to use MMLSpark when you run experiments in Docker container, either locally or in remote VM.</span><span class="sxs-lookup"><span data-stu-id="fe2fd-115">Your Azure Machine Learning Workbench is configured to use MMLSpark when you run experiments in Docker container, either locally or in remote VM.</span></span> <span data-ttu-id="fe2fd-116">This capability allows you to easily debug and experiment with your PySpark models, before running them on scale on a cluster.</span><span class="sxs-lookup"><span data-stu-id="fe2fd-116">This capability allows you to easily debug and experiment with your PySpark models, before running them on scale on a cluster.</span></span> 

<span data-ttu-id="fe2fd-117">To get started using an example, create a new project, and select "MMLSpark on Adult Census" Gallery example.</span><span class="sxs-lookup"><span data-stu-id="fe2fd-117">To get started using an example, create a new project, and select "MMLSpark on Adult Census" Gallery example.</span></span> <span data-ttu-id="fe2fd-118">Select "Docker" as the compute context from the project dashboard, and click "Run."</span><span class="sxs-lookup"><span data-stu-id="fe2fd-118">Select "Docker" as the compute context from the project dashboard, and click "Run."</span></span> <span data-ttu-id="fe2fd-119">Azure Machine Learning Workbench builds the Docker container to run the PySpark program, and then executes the program.</span><span class="sxs-lookup"><span data-stu-id="fe2fd-119">Azure Machine Learning Workbench builds the Docker container to run the PySpark program, and then executes the program.</span></span>

<span data-ttu-id="fe2fd-120">After the run has completed, you can view the results in run history view of Azure Machine Learning Workbench.</span><span class="sxs-lookup"><span data-stu-id="fe2fd-120">After the run has completed, you can view the results in run history view of Azure Machine Learning Workbench.</span></span>

## <a name="install-mmlspark-on-azure-hdinsight-spark-cluster"></a><span data-ttu-id="fe2fd-121">Install MMLSpark on Azure HDInsight Spark Cluster.</span><span class="sxs-lookup"><span data-stu-id="fe2fd-121">Install MMLSpark on Azure HDInsight Spark Cluster.</span></span>

<span data-ttu-id="fe2fd-122">To complete this and the following step, you need to first [create an Azure HDInsight Spark cluster](https://docs.microsoft.com/azure/hdinsight/hdinsight-apache-spark-jupyter-spark-sql).</span><span class="sxs-lookup"><span data-stu-id="fe2fd-122">To complete this and the following step, you need to first [create an Azure HDInsight Spark cluster](https://docs.microsoft.com/azure/hdinsight/hdinsight-apache-spark-jupyter-spark-sql).</span></span>

<span data-ttu-id="fe2fd-123">By default, Azure Machine Learning Workbench installs MMLSpark package on your cluster when you run your experiment.</span><span class="sxs-lookup"><span data-stu-id="fe2fd-123">By default, Azure Machine Learning Workbench installs MMLSpark package on your cluster when you run your experiment.</span></span> <span data-ttu-id="fe2fd-124">You can control this behavior and install other Spark packages by editing a file named _aml_config/spark_dependencies.yml_ in your project folder.</span><span class="sxs-lookup"><span data-stu-id="fe2fd-124">You can control this behavior and install other Spark packages by editing a file named _aml_config/spark_dependencies.yml_ in your project folder.</span></span>

```
# Spark configuration properties.
configuration:
  "spark.app.name": "Azure ML Experiment"
  "spark.yarn.maxAppAttempts": 1

repositories:
  - "https://mmlspark.azureedge.net/maven"
packages:
  - group: "com.microsoft.ml.spark"
    artifact: "mmlspark_2.11"
    version: "0.9.9"
```

<span data-ttu-id="fe2fd-125">You can also install MMLSpark directly on your HDInsight Spark cluster using [Script Action](https://github.com/Azure/mmlspark#hdinsight).</span><span class="sxs-lookup"><span data-stu-id="fe2fd-125">You can also install MMLSpark directly on your HDInsight Spark cluster using [Script Action](https://github.com/Azure/mmlspark#hdinsight).</span></span>

## <a name="set-up-azure-hdinsight-spark-cluster-as-compute-target"></a><span data-ttu-id="fe2fd-126">Set up Azure HDInsight Spark Cluster as Compute Target</span><span class="sxs-lookup"><span data-stu-id="fe2fd-126">Set up Azure HDInsight Spark Cluster as Compute Target</span></span>

<span data-ttu-id="fe2fd-127">Open CLI window from Azure Machine Learning Workbench by going to "File" Menu and click "Open Command Prompt"</span><span class="sxs-lookup"><span data-stu-id="fe2fd-127">Open CLI window from Azure Machine Learning Workbench by going to "File" Menu and click "Open Command Prompt"</span></span>

<span data-ttu-id="fe2fd-128">In CLI Window, run following commands:</span><span class="sxs-lookup"><span data-stu-id="fe2fd-128">In CLI Window, run following commands:</span></span>

```
az ml computetarget attach cluster --name <myhdi> --address <myhdi-ssh.azurehdinsight.net> --username <sshusername> --password <sshpwd> 
```

```
az ml experiment prepare -c <myhdi>
```

<span data-ttu-id="fe2fd-129">Now the cluster is available as compute target for the project.</span><span class="sxs-lookup"><span data-stu-id="fe2fd-129">Now the cluster is available as compute target for the project.</span></span>

## <a name="run-experiment-on-azure-hdinsight-spark-cluster"></a><span data-ttu-id="fe2fd-130">Run experiment on Azure HDInsight Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="fe2fd-130">Run experiment on Azure HDInsight Spark cluster.</span></span>

<span data-ttu-id="fe2fd-131">Go back to the project dashboard of "MMLSpark on Adult Census" example.</span><span class="sxs-lookup"><span data-stu-id="fe2fd-131">Go back to the project dashboard of "MMLSpark on Adult Census" example.</span></span> <span data-ttu-id="fe2fd-132">Select your cluster as the compute target, and click run.</span><span class="sxs-lookup"><span data-stu-id="fe2fd-132">Select your cluster as the compute target, and click run.</span></span>

<span data-ttu-id="fe2fd-133">Azure Machine Learning Workbench submits the spark job to the cluster.</span><span class="sxs-lookup"><span data-stu-id="fe2fd-133">Azure Machine Learning Workbench submits the spark job to the cluster.</span></span> <span data-ttu-id="fe2fd-134">You can monitor the progress and view the results in run history view.</span><span class="sxs-lookup"><span data-stu-id="fe2fd-134">You can monitor the progress and view the results in run history view.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fe2fd-135">Next steps</span><span class="sxs-lookup"><span data-stu-id="fe2fd-135">Next steps</span></span>
<span data-ttu-id="fe2fd-136">For information about MMLSpark library, and examples, see [MMLSpark GitHub repository](https://github.com/Azure/mmlspark)</span><span class="sxs-lookup"><span data-stu-id="fe2fd-136">For information about MMLSpark library, and examples, see [MMLSpark GitHub repository](https://github.com/Azure/mmlspark)</span></span>

<span data-ttu-id="fe2fd-137">*Apache®, Apache Spark, and Spark® are either registered trademarks or trademarks of the Apache Software Foundation in the United States and/or other countries.*</span><span class="sxs-lookup"><span data-stu-id="fe2fd-137">*Apache®, Apache Spark, and Spark® are either registered trademarks or trademarks of the Apache Software Foundation in the United States and/or other countries.*</span></span>
