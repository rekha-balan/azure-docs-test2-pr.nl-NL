---
title: HDInsight Spark walkthroughs using PySpark and Scala on Azure | Microsoft Docs
description: Examples of the Team Data Science Process that walk through the use of PySpark and Scala on an Azure HDInsight Spark to do predictive analytics.
services: machine-learning
documentationcenter: ''
author: deguhath
manager: jhubbard
editor: cgronlun
ms.assetid: ''
ms.service: machine-learning
ms.component: team-data-science-process
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/04/2017
ms.author: deguhath
ms.openlocfilehash: 05f8748be8fd14bef212ee7bd5c2320f1b577536
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866353"
---
# <a name="hdinsight-spark-data-science-walkthroughs-using-pyspark-and-scala-on-azure"></a>HDInsight Spark data science walkthroughs using PySpark and Scala on Azure

These walkthroughs use PySpark and Scala on an Azure Spark cluster to do predictive analytics. They follow the steps outlined in the Team Data Science Process. For an overview of the Team Data Science Process, see [Data Science Process](overview.md). For an overview of Spark on HDInsight, see [Introduction to Spark on HDInsight](../../hdinsight/spark/apache-spark-overview.md).

Additional data science walkthroughs that execute the Team Data Science Process are grouped by the **platform** that they use. See [Walkthroughs executing the Team Data Science Process](walkthroughs.md) for an itemization of these examples.

## <a name="predict-taxi-tips-using-pyspark-on-azure-spark"></a>Predict taxi tips using PySpark on Azure Spark

The [Use Spark on Azure HDInsight](spark-overview.md) walkthrough uses data from New York taxis to predict whether a tip is paid and the range of amounts expected to be paid. It uses the Team Data Science Process in a scenario using an [Azure HDInsight Spark cluster](https://azure.microsoft.com/services/hdinsight/) to store, explore, and feature engineer data from the publicly available NYC taxi trip and fare dataset. This overview topic sets you up with an HDInsight Spark cluster and the Jupyter  PySpark notebooks used in the rest of the walkthrough. These notebooks show you how to explore your data and then how to create and consume models. The advanced data exploration and modeling notebook shows how to include cross-validation, hyper-parameter sweeping, and model evaluation.

### <a name="data-exploration-and-modeling-with-spark"></a>Data Exploration and modeling with Spark 
Explore the dataset and create, score, and evaluate the machine learning models by working through the [Create binary classification and regression models for data with the Spark MLlib toolkit](spark-data-exploration-modeling.md) topic.

### <a name="model-consumption"></a>Model consumption
To learn how to score the classification and regression models created in this topic, see [Score and evaluate Spark-built machine learning models](spark-model-consumption.md).

### <a name="cross-validation-and-hyperparameter-sweeping"></a>Cross-validation and hyperparameter sweeping
See [Advanced data exploration and modeling with Spark](spark-advanced-data-exploration-modeling.md) on how models can be trained using cross-validation and hyper-parameter sweeping.


## <a name="predict-taxi-tips-using-scala-on-azure-spark"></a>Predict taxi tips using Scala on Azure Spark

The [Use Scala with Spark on Azure](scala-walkthrough.md) walkthrough uses data from New York taxis to predict whether a tip is paid and the range of amounts expected to be paid. It shows how to use Scala for supervised machine learning tasks with the Spark machine learning library (MLlib) and SparkML packages on an Azure HDInsight Spark cluster. It walks you through the tasks that constitute the [Data Science Process](http://aka.ms/datascienceprocess): data ingestion and exploration, visualization, feature engineering, modeling, and model consumption. The models built include logistic and linear regression, random forests, and gradient boosted trees.


## <a name="next-steps"></a>Next steps

For a discussion of the key components that comprise the Team Data Science Process, see [Team Data Science Process overview](overview.md).

For a discussion of the Team Data Science Process lifecycle that you can use to structure your data science projects, see [Team Data Science Process lifecycle](lifecycle.md). The lifecycle outlines the steps, from start to finish, that projects usually follow when they are executed. 

