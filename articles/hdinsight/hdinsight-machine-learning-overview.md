---
title: Machine learning overview - Azure HDInsight
description: Describes the machine learning options in HDInsight.
services: hdinsight
author: jasonwhowell
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 01/19/2018
ms.author: jasonh
ms.openlocfilehash: 10d4056ea9d78bd56710b7b5d67297b90232cf0b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864874"
---
# <a name="machine-learning-on-hdinsight"></a>Machine learning on HDInsight

HDInsight enables machine learning with big data, providing the ability to obtain valuable insight from large amounts (petabytes, or even exabytes) of structured, unstructured, and fast-moving data. There are several machine learning options  in HDInsight:  SparkML and MLlib, R, Hive, and the Microsoft Cognitive Toolkit.

## <a name="sparkml-and-mllib"></a>SparkML and MLlib

[HDInsight Spark](spark/apache-spark-overview.md) is an Azure-hosted offering of [Spark](http://spark.apache.org/), a unified, open source, parallel data processing framework supporting in-memory processing to boost big data analytics. The Spark processing engine is built for speed, ease of use, and sophisticated analytics. Spark's in-memory distributed computation capabilities make it a good choice for the iterative algorithms used in machine learning and graph computations. There are two scalable machine learning libraries that bring algorithmic modeling capabilities to this distributed environment: MLlib and SparkML. MLlib contains the original API built on top of RDDs. SparkML is a newer package that provides a higher-level API built on top of DataFrames for constructing ML pipelines. SparkML does not yet support all of the  features of MLlib, but is replacing MLlib as Spark's standard machine learning library.

The Microsoft Machine Learning library for Apache Spark is [MMLSpark](https://github.com/Azure/mmlspark). This library is designed to make data scientists more productive on Spark, increase the rate of experimentation, and leverage cutting-edge machine learning techniques, including deep learning, on very large datasets. MMLSpark provides a layer on top of SparkML's low-level APIs when building scalable ML models, such as indexing strings, coercing data into a layout expected by machine learning algorithms, and assembling feature vectors. The MMLSpark library simplifies these and other common tasks for building models in PySpark.

## <a name="r"></a>R

[R](https://www.r-project.org/) is currently the most popular statistical programming language in the world. It is an open source data visualization tool with a community of over 2.5 million users and growing. With its thriving user base, and over 8,000 contributed packages, R is a likely choice for many companies who need machine learning. You can create an HDInsight cluster with ML Services ready to be used with massive datasets and models. This capability provides data scientists and statisticians with a familiar R interface that can scale on-demand through HDInsight, without the overhead of cluster setup and maintenance.

![Training for prediction with R server](./media/hdinsight-machine-learning-overview/r-training.png)

The edge node of a cluster provides a convenient place to connect to the cluster and to run your R scripts.  You also have the option to run R scripts across the nodes of the cluster by using ScaleR’s Hadoop Map Reduce or Spark compute contexts.

With ML Services on HDInsight with Spark, you can parallelize training across the nodes of a cluster by using a Spark compute context. You can run R scripts directly on the edge node, using all available cores in parallel, as needed. Alternately, you can run your code from the edge node to kick off processing that is distributed across all nodes in the cluster. ML Services on HDInsight with Spark also enables parallelizing functions from open source R packages, if desired.

## <a name="azure-machine-learning-and-hive"></a>Azure Machine Learning and Hive

Azure Machine Learning provides tools to model predictive analytics, as well as a fully managed service you can use to deploy your predictive models as ready-to-consume web services. Azure Machine Learning is a  complete predictive analytics solution in the cloud that you can use to create, test, operationalize, and manage predictive models. Select from a large algorithm library, use a web-based studio for building models, and easily deploy your model as a web service.

![Making advanced analytics accessible to Hadoop with Microsoft Azure Machine Learning](./media/hdinsight-machine-learning-overview/hadoop-azure-ml.png)

Create features for data in an HDInsight Hadoop cluster using [Hive queries](../machine-learning/team-data-science-process/create-features-hive.md). *Feature engineering* attempts to increase the predictive power of learning algorithms by creating features from raw data that facilitate the learning process. You can run HiveQL queries from Azure ML, and access data processed in Hive and stored in blob storage, by using the [Import Data module](../machine-learning/studio/import-data.md).

## <a name="microsoft-cognitive-toolkit"></a>Microsoft Cognitive Toolkit

[Deep learning](https://www.microsoft.com/en-us/research/group/dltc/) is a branch of machine learning that uses neural networks, inspired by the biological processes of the human brain. Many researchers see deep learning as a promising approach for enhancing artificial intelligence. Examples of deep learning are spoken language translators, image recognition systems, and machine reasoning.

To help advance its own work in deep learning, Microsoft  developed the free, easy-to-use, open-source [Microsoft Cognitive Toolkit](https://www.microsoft.com/en-us/cognitive-toolkit/). This toolkit is being used  by a wide variety of Microsoft products, by companies worldwide with a need to deploy deep learning at scale, and by students interested in the latest algorithms and techniques. 

## <a name="see-also"></a>See also

### <a name="scenarios"></a>Scenarios

* [Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data](spark/apache-spark-ipython-notebook-machine-learning.md)
* [Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results](spark/apache-spark-machine-learning-mllib-ipython.md)
* [Generate movie recommendations with Mahout](hadoop/apache-hadoop-mahout-linux-mac.md)
* [Hive and Azure Machine Learning](../machine-learning/team-data-science-process/create-features-hive.md)
* [Hive and Azure Machine Learning end-to-end](../machine-learning/team-data-science-process/hive-walkthrough.md)
* [Machine learning with Spark on HDInsight](../machine-learning/team-data-science-process/spark-overview.md)

### <a name="deep-learning-resources"></a>Deep learning resources

* [Deep learning toolkit with Spark](https://blogs.technet.microsoft.com/machinelearning/2017/04/25/using-microsofts-deep-learning-toolkit-with-spark-on-azure-hdinsight-clusters/)
* [Embarrassingly parallel image classification with Cognitive toolkit + Tensorflow on Spark](https://blogs.technet.microsoft.com/machinelearning/2017/04/12/embarrassingly-parallel-image-classification-using-cognitive-toolkit-tensorflow-on-azure-hdinsight-spark/)