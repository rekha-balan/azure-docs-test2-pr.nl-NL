---
title: HDInsight Hadoop data science walkthroughs using Hive on Azure  | Microsoft Docs
description: Examples of the Team Data Science Process that walk through the use of Hive on Azure HDInsight Hadoop to do predictive analytics.
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
ms.openlocfilehash: 8b7eead12b6546ad86f6ff0aa48f4754c00a4734
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871243"
---
# <a name="hdinsight-hadoop-data-science-walkthroughs-using-hive-on-azure"></a>HDInsight Hadoop data science walkthroughs using Hive on Azure 

These walkthroughs use Hive with an HDInsight Hadoop cluster to do predictive analytics. They follow the steps outlined in the Team Data Science Process. For an overview of the Team Data Science Process, see [Data Science Process](overview.md). For an introduction to Azure HDInsight, see [Introduction to Azure HDInsight, the Hadoop technology stack, and Hadoop clusters](../../hdinsight/hadoop/apache-hadoop-introduction.md).

Additional data science walkthroughs that execute the Team Data Science Process are grouped by the **platform** that they use. See [Walkthroughs executing the Team Data Science Process](walkthroughs.md) for an itemization of these examples.


## <a name="predict-taxi-tips-using-hive-with-hdinsight-hadoop"></a>Predict taxi tips using Hive with HDInsight Hadoop

The [Use HDInsight Hadoop clusters](hive-walkthrough.md) walkthrough uses data from New York taxis to predict: 

- Whether a tip is paid 
- The distribution of tip amounts

The scenario is implemented using Hive with an [Azure HDInsight Hadoop cluster](https://azure.microsoft.com/services/hdinsight/). You learn how to store, explore, and feature engineer data from a publicly available NYC taxi trip and fare dataset. You also use Azure Machine Learning to build and deploy the models.

## <a name="predict-advertisement-clicks-using-hive-with-hdinsight-hadoop"></a>Predict advertisement clicks using Hive with HDInsight Hadoop

The [Use Azure HDInsight Hadoop Clusters on a 1-TB dataset](hive-criteo-walkthrough.md) walkthrough uses a publicly available [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) click dataset to predict whether a tip is paid and the range of amounts expected. The scenario is implemented using Hive with an [Azure HDInsight Hadoop cluster](https://azure.microsoft.com/services/hdinsight/) to store, explore, feature engineer, and down sample data. It uses Azure Machine Learning to build, train, and score a binary classification model predicting whether a user clicks on an advertisement. The walkthrough concludes showing how to publish one of these models as a Web service.


## <a name="next-steps"></a>Next steps

For a discussion of the key components that comprise the Team Data Science Process, see [Team Data Science Process overview](overview.md).

For a discussion of the Team Data Science Process lifecycle that you can use to structure your data science projects, see [Team Data Science Process lifecycle](lifecycle.md). The lifecycle outlines the steps, from start to finish, that projects usually follow when they are executed. 
