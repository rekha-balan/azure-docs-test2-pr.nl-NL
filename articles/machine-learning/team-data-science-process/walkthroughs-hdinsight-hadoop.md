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
# <a name="hdinsight-hadoop-data-science-walkthroughs-using-hive-on-azure"></a><span data-ttu-id="f17ce-103">HDInsight Hadoop data science walkthroughs using Hive on Azure</span><span class="sxs-lookup"><span data-stu-id="f17ce-103">HDInsight Hadoop data science walkthroughs using Hive on Azure</span></span> 

<span data-ttu-id="f17ce-104">These walkthroughs use Hive with an HDInsight Hadoop cluster to do predictive analytics.</span><span class="sxs-lookup"><span data-stu-id="f17ce-104">These walkthroughs use Hive with an HDInsight Hadoop cluster to do predictive analytics.</span></span> <span data-ttu-id="f17ce-105">They follow the steps outlined in the Team Data Science Process.</span><span class="sxs-lookup"><span data-stu-id="f17ce-105">They follow the steps outlined in the Team Data Science Process.</span></span> <span data-ttu-id="f17ce-106">For an overview of the Team Data Science Process, see [Data Science Process](overview.md).</span><span class="sxs-lookup"><span data-stu-id="f17ce-106">For an overview of the Team Data Science Process, see [Data Science Process](overview.md).</span></span> <span data-ttu-id="f17ce-107">For an introduction to Azure HDInsight, see [Introduction to Azure HDInsight, the Hadoop technology stack, and Hadoop clusters](../../hdinsight/hadoop/apache-hadoop-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f17ce-107">For an introduction to Azure HDInsight, see [Introduction to Azure HDInsight, the Hadoop technology stack, and Hadoop clusters](../../hdinsight/hadoop/apache-hadoop-introduction.md).</span></span>

<span data-ttu-id="f17ce-108">Additional data science walkthroughs that execute the Team Data Science Process are grouped by the **platform** that they use.</span><span class="sxs-lookup"><span data-stu-id="f17ce-108">Additional data science walkthroughs that execute the Team Data Science Process are grouped by the **platform** that they use.</span></span> <span data-ttu-id="f17ce-109">See [Walkthroughs executing the Team Data Science Process](walkthroughs.md) for an itemization of these examples.</span><span class="sxs-lookup"><span data-stu-id="f17ce-109">See [Walkthroughs executing the Team Data Science Process](walkthroughs.md) for an itemization of these examples.</span></span>


## <a name="predict-taxi-tips-using-hive-with-hdinsight-hadoop"></a><span data-ttu-id="f17ce-110">Predict taxi tips using Hive with HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="f17ce-110">Predict taxi tips using Hive with HDInsight Hadoop</span></span>

<span data-ttu-id="f17ce-111">The [Use HDInsight Hadoop clusters](hive-walkthrough.md) walkthrough uses data from New York taxis to predict:</span><span class="sxs-lookup"><span data-stu-id="f17ce-111">The [Use HDInsight Hadoop clusters](hive-walkthrough.md) walkthrough uses data from New York taxis to predict:</span></span> 

- <span data-ttu-id="f17ce-112">Whether a tip is paid</span><span class="sxs-lookup"><span data-stu-id="f17ce-112">Whether a tip is paid</span></span> 
- <span data-ttu-id="f17ce-113">The distribution of tip amounts</span><span class="sxs-lookup"><span data-stu-id="f17ce-113">The distribution of tip amounts</span></span>

<span data-ttu-id="f17ce-114">The scenario is implemented using Hive with an [Azure HDInsight Hadoop cluster](https://azure.microsoft.com/services/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="f17ce-114">The scenario is implemented using Hive with an [Azure HDInsight Hadoop cluster](https://azure.microsoft.com/services/hdinsight/).</span></span> <span data-ttu-id="f17ce-115">You learn how to store, explore, and feature engineer data from a publicly available NYC taxi trip and fare dataset.</span><span class="sxs-lookup"><span data-stu-id="f17ce-115">You learn how to store, explore, and feature engineer data from a publicly available NYC taxi trip and fare dataset.</span></span> <span data-ttu-id="f17ce-116">You also use Azure Machine Learning to build and deploy the models.</span><span class="sxs-lookup"><span data-stu-id="f17ce-116">You also use Azure Machine Learning to build and deploy the models.</span></span>

## <a name="predict-advertisement-clicks-using-hive-with-hdinsight-hadoop"></a><span data-ttu-id="f17ce-117">Predict advertisement clicks using Hive with HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="f17ce-117">Predict advertisement clicks using Hive with HDInsight Hadoop</span></span>

<span data-ttu-id="f17ce-118">The [Use Azure HDInsight Hadoop Clusters on a 1-TB dataset](hive-criteo-walkthrough.md) walkthrough uses a publicly available [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) click dataset to predict whether a tip is paid and the range of amounts expected.</span><span class="sxs-lookup"><span data-stu-id="f17ce-118">The [Use Azure HDInsight Hadoop Clusters on a 1-TB dataset](hive-criteo-walkthrough.md) walkthrough uses a publicly available [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) click dataset to predict whether a tip is paid and the range of amounts expected.</span></span> <span data-ttu-id="f17ce-119">The scenario is implemented using Hive with an [Azure HDInsight Hadoop cluster](https://azure.microsoft.com/services/hdinsight/) to store, explore, feature engineer, and down sample data.</span><span class="sxs-lookup"><span data-stu-id="f17ce-119">The scenario is implemented using Hive with an [Azure HDInsight Hadoop cluster](https://azure.microsoft.com/services/hdinsight/) to store, explore, feature engineer, and down sample data.</span></span> <span data-ttu-id="f17ce-120">It uses Azure Machine Learning to build, train, and score a binary classification model predicting whether a user clicks on an advertisement.</span><span class="sxs-lookup"><span data-stu-id="f17ce-120">It uses Azure Machine Learning to build, train, and score a binary classification model predicting whether a user clicks on an advertisement.</span></span> <span data-ttu-id="f17ce-121">The walkthrough concludes showing how to publish one of these models as a Web service.</span><span class="sxs-lookup"><span data-stu-id="f17ce-121">The walkthrough concludes showing how to publish one of these models as a Web service.</span></span>


## <a name="next-steps"></a><span data-ttu-id="f17ce-122">Next steps</span><span class="sxs-lookup"><span data-stu-id="f17ce-122">Next steps</span></span>

<span data-ttu-id="f17ce-123">For a discussion of the key components that comprise the Team Data Science Process, see [Team Data Science Process overview](overview.md).</span><span class="sxs-lookup"><span data-stu-id="f17ce-123">For a discussion of the key components that comprise the Team Data Science Process, see [Team Data Science Process overview](overview.md).</span></span>

<span data-ttu-id="f17ce-124">For a discussion of the Team Data Science Process lifecycle that you can use to structure your data science projects, see [Team Data Science Process lifecycle](lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="f17ce-124">For a discussion of the Team Data Science Process lifecycle that you can use to structure your data science projects, see [Team Data Science Process lifecycle](lifecycle.md).</span></span> <span data-ttu-id="f17ce-125">The lifecycle outlines the steps, from start to finish, that projects usually follow when they are executed.</span><span class="sxs-lookup"><span data-stu-id="f17ce-125">The lifecycle outlines the steps, from start to finish, that projects usually follow when they are executed.</span></span> 

