---
title: Copy machine learning sample experiments | Microsoft Docs
description: Learn how to use sample machine learning experiments to create new experiments with Cortana Intelligence Gallery and Microsoft Azure Machine Learning.
services: machine-learning
documentationcenter: ''
author: cjgronlund
manager: jhubbard
editor: cgronlun
ms.assetid: 81e6c1d8-682c-4db3-bfd5-d7bfb1150ff3
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 02/13/2017
ms.author: cgronlun;olgali
ms.openlocfilehash: 0bf9cb6069e261f316bf43f8a9776329c9bb0628
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556053"
---
# <a name="copy-sample-experiments-to-create-new-machine-learning-experiments"></a><span data-ttu-id="2da11-103">Copy sample experiments to create new machine learning experiments</span><span class="sxs-lookup"><span data-stu-id="2da11-103">Copy sample experiments to create new machine learning experiments</span></span>
<span data-ttu-id="2da11-104">Learn how to start with sample experiments from [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/) instead of creating machine learning experiments from scratch.</span><span class="sxs-lookup"><span data-stu-id="2da11-104">Learn how to start with sample experiments from [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/) instead of creating machine learning experiments from scratch.</span></span> <span data-ttu-id="2da11-105">You can use the samples to build your own machine learning solution.</span><span class="sxs-lookup"><span data-stu-id="2da11-105">You can use the samples to build your own machine learning solution.</span></span>

<span data-ttu-id="2da11-106">In the gallery are sample experiments by the Microsoft Azure Machine Learning team as well as samples shared by the Machine Learning community.</span><span class="sxs-lookup"><span data-stu-id="2da11-106">In the gallery are sample experiments by the Microsoft Azure Machine Learning team as well as samples shared by the Machine Learning community.</span></span> <span data-ttu-id="2da11-107">You also can ask questions or post comments about experiments.</span><span class="sxs-lookup"><span data-stu-id="2da11-107">You also can ask questions or post comments about experiments.</span></span>

<span data-ttu-id="2da11-108">To see how to use the gallery, watch the 3-minute video [Copy other people's work to do data science](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) from the series [Data Science for Beginners](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md).</span><span class="sxs-lookup"><span data-stu-id="2da11-108">To see how to use the gallery, watch the 3-minute video [Copy other people's work to do data science](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) from the series [Data Science for Beginners](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="find-an-experiment-to-copy-in-cortana-intelligence-gallery"></a><span data-ttu-id="2da11-109">Find an experiment to copy in Cortana Intelligence Gallery</span><span class="sxs-lookup"><span data-stu-id="2da11-109">Find an experiment to copy in Cortana Intelligence Gallery</span></span>
<span data-ttu-id="2da11-110">To see what experiments are available, go to the [Gallery](https://gallery.cortanaintelligence.com/) and click **Experiments** at the top of the page.</span><span class="sxs-lookup"><span data-stu-id="2da11-110">To see what experiments are available, go to the [Gallery](https://gallery.cortanaintelligence.com/) and click **Experiments** at the top of the page.</span></span>

### <a name="find-the-newest-or-most-popular-experiments"></a><span data-ttu-id="2da11-111">Find the newest or most popular experiments</span><span class="sxs-lookup"><span data-stu-id="2da11-111">Find the newest or most popular experiments</span></span>
<span data-ttu-id="2da11-112">On this page, you can see **Recently added** experiments, or scroll down to look at **What's popular** or the latest **Popular Microsoft experiments**.</span><span class="sxs-lookup"><span data-stu-id="2da11-112">On this page, you can see **Recently added** experiments, or scroll down to look at **What's popular** or the latest **Popular Microsoft experiments**.</span></span>

### <a name="look-for-an-experiment-that-meets-specific-requirements"></a><span data-ttu-id="2da11-113">Look for an experiment that meets specific requirements</span><span class="sxs-lookup"><span data-stu-id="2da11-113">Look for an experiment that meets specific requirements</span></span>
<span data-ttu-id="2da11-114">To browse all experiments:</span><span class="sxs-lookup"><span data-stu-id="2da11-114">To browse all experiments:</span></span>

1. <span data-ttu-id="2da11-115">Click **Browse all** at the top of the page.</span><span class="sxs-lookup"><span data-stu-id="2da11-115">Click **Browse all** at the top of the page.</span></span>
2. <span data-ttu-id="2da11-116">Under **Refine by** in the **Categories** section, select **Experiment** to see all the experiments in the Gallery.</span><span class="sxs-lookup"><span data-stu-id="2da11-116">Under **Refine by** in the **Categories** section, select **Experiment** to see all the experiments in the Gallery.</span></span>
3. <span data-ttu-id="2da11-117">You can find experiments that meet your requirements a couple different ways:</span><span class="sxs-lookup"><span data-stu-id="2da11-117">You can find experiments that meet your requirements a couple different ways:</span></span>
   * <span data-ttu-id="2da11-118">**Select filters on the left.**</span><span class="sxs-lookup"><span data-stu-id="2da11-118">**Select filters on the left.**</span></span> <span data-ttu-id="2da11-119">For example, to browse experiments that use a PCA-based anomaly detection algorithm, select **Experiment** under **Categories**, and **PCA-Based Anomaly Detection** under **Algorithms Used**.</span><span class="sxs-lookup"><span data-stu-id="2da11-119">For example, to browse experiments that use a PCA-based anomaly detection algorithm, select **Experiment** under **Categories**, and **PCA-Based Anomaly Detection** under **Algorithms Used**.</span></span> <span data-ttu-id="2da11-120">(If you don't see that algorithm, click **Show all** at the bottom of the list.)</span><span class="sxs-lookup"><span data-stu-id="2da11-120">(If you don't see that algorithm, click **Show all** at the bottom of the list.)</span></span><br></br>
     <span data-ttu-id="2da11-121">![Select filters](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-sample-experiments/refine-the-view.png)</span><span class="sxs-lookup"><span data-stu-id="2da11-121">![Select filters](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-sample-experiments/refine-the-view.png)</span></span>
   * <span data-ttu-id="2da11-122">**Use the search box.**</span><span class="sxs-lookup"><span data-stu-id="2da11-122">**Use the search box.**</span></span> <span data-ttu-id="2da11-123">For example, to find experiments contributed by Microsoft related to digit recognition that use a two-class support vector machine algorithm, enter "digit recognition" in the search box.</span><span class="sxs-lookup"><span data-stu-id="2da11-123">For example, to find experiments contributed by Microsoft related to digit recognition that use a two-class support vector machine algorithm, enter "digit recognition" in the search box.</span></span> <span data-ttu-id="2da11-124">Then, select the filters **Experiment**, **Microsoft content only**, and **Two-Class Support Vector Machine**:</span><span class="sxs-lookup"><span data-stu-id="2da11-124">Then, select the filters **Experiment**, **Microsoft content only**, and **Two-Class Support Vector Machine**:</span></span><br></br>
     <span data-ttu-id="2da11-125">![Use the search box](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-sample-experiments/search-for-experiments.png)</span><span class="sxs-lookup"><span data-stu-id="2da11-125">![Use the search box](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-sample-experiments/search-for-experiments.png)</span></span>
4. <span data-ttu-id="2da11-126">Click an experiment to learn more about it.</span><span class="sxs-lookup"><span data-stu-id="2da11-126">Click an experiment to learn more about it.</span></span>
5. <span data-ttu-id="2da11-127">To run and/or modify the experiment, click **Open in Studio** on the experiment's page.</span><span class="sxs-lookup"><span data-stu-id="2da11-127">To run and/or modify the experiment, click **Open in Studio** on the experiment's page.</span></span> <br></br>

    ![Example experiment](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-sample-experiments/example-experiment.png)

    > [!NOTE]
    > <span data-ttu-id="2da11-129">When you open an experiment in Machine Learning Studio for the first time, you can try it for free or buy an Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="2da11-129">When you open an experiment in Machine Learning Studio for the first time, you can try it for free or buy an Azure subscription.</span></span> [<span data-ttu-id="2da11-130">Learn about the Machine Learning Studio free trial vs. paid service</span><span class="sxs-lookup"><span data-stu-id="2da11-130">Learn about the Machine Learning Studio free trial vs. paid service</span></span>](https://azure.microsoft.com/pricing/details/machine-learning/)
    >
    >

## <a name="use-a-template-in-machine-learning-studio"></a><span data-ttu-id="2da11-131">Use a template in Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="2da11-131">Use a template in Machine Learning Studio</span></span>
<span data-ttu-id="2da11-132">You also can create a new experiment in Machine Learning Studio using a Gallery sample as a template.</span><span class="sxs-lookup"><span data-stu-id="2da11-132">You also can create a new experiment in Machine Learning Studio using a Gallery sample as a template.</span></span>

1. <span data-ttu-id="2da11-133">Sign in with your Microsoft account credentials to the [Studio](https://studio.azureml.net), and then click **New** to create an experiment.</span><span class="sxs-lookup"><span data-stu-id="2da11-133">Sign in with your Microsoft account credentials to the [Studio](https://studio.azureml.net), and then click **New** to create an experiment.</span></span>
2. <span data-ttu-id="2da11-134">Browse through the sample content and click one.</span><span class="sxs-lookup"><span data-stu-id="2da11-134">Browse through the sample content and click one.</span></span>

<span data-ttu-id="2da11-135">A new experiment is created in your workspace using the sample experiment as a template.</span><span class="sxs-lookup"><span data-stu-id="2da11-135">A new experiment is created in your workspace using the sample experiment as a template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2da11-136">Next steps</span><span class="sxs-lookup"><span data-stu-id="2da11-136">Next steps</span></span>
* [<span data-ttu-id="2da11-137">Import data from various sources</span><span class="sxs-lookup"><span data-stu-id="2da11-137">Import data from various sources</span></span>](machine-learning-data-science-import-data.md)
* [<span data-ttu-id="2da11-138">Quickstart tutorial for the R language in Machine Learning</span><span class="sxs-lookup"><span data-stu-id="2da11-138">Quickstart tutorial for the R language in Machine Learning</span></span>](machine-learning-r-quickstart.md)
* [<span data-ttu-id="2da11-139">Deploy a Machine Learning web service</span><span class="sxs-lookup"><span data-stu-id="2da11-139">Deploy a Machine Learning web service</span></span>](machine-learning-publish-a-machine-learning-web-service.md)



