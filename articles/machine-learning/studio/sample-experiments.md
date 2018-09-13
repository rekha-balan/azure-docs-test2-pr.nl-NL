---
title: Create experiments from machine learning examples - Azure | Microsoft Docs
description: Learn how to use example machine learning experiments to create new experiments with Azure AI Gallery and Azure Machine Learning.
keywords: machine learning examples, sample experiment, machine learning sample, AI examples
services: machine-learning
documentationcenter: ''
author: heatherbshapiro
ms.author: hshapiro
manager: hjerez
editor: cgronlun
ms.assetid: 81e6c1d8-682c-4db3-bfd5-d7bfb1150ff3
ms.service: machine-learning
ms.component: studio
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/05/2018
ms.openlocfilehash: 11cc4889690cb44cb621ed53f3e3614afcc57abf
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44858009"
---
# <a name="create-machine-learning-experiments-from-working-examples-in-azure-ai-gallery"></a><span data-ttu-id="412c5-104">Create machine learning experiments from working examples in Azure AI Gallery</span><span class="sxs-lookup"><span data-stu-id="412c5-104">Create machine learning experiments from working examples in Azure AI Gallery</span></span>

<span data-ttu-id="412c5-105">Learn how to start with example experiments from [Azure AI Gallery](https://gallery.cortanaintelligence.com/) instead of creating machine learning experiments from scratch.</span><span class="sxs-lookup"><span data-stu-id="412c5-105">Learn how to start with example experiments from [Azure AI Gallery](https://gallery.cortanaintelligence.com/) instead of creating machine learning experiments from scratch.</span></span> <span data-ttu-id="412c5-106">You can use the examples to build your own machine learning solution.</span><span class="sxs-lookup"><span data-stu-id="412c5-106">You can use the examples to build your own machine learning solution.</span></span>

<span data-ttu-id="412c5-107">The gallery has example experiments by the Microsoft Azure Machine Learning team as well as examples shared by the Machine Learning community.</span><span class="sxs-lookup"><span data-stu-id="412c5-107">The gallery has example experiments by the Microsoft Azure Machine Learning team as well as examples shared by the Machine Learning community.</span></span> <span data-ttu-id="412c5-108">You also can ask questions or post comments about experiments.</span><span class="sxs-lookup"><span data-stu-id="412c5-108">You also can ask questions or post comments about experiments.</span></span>

<span data-ttu-id="412c5-109">To see how to use the gallery, watch the 3-minute video [Copy other people's work to do data science](data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) from the series [Data Science for Beginners](data-science-for-beginners-the-5-questions-data-science-answers.md).</span><span class="sxs-lookup"><span data-stu-id="412c5-109">To see how to use the gallery, watch the 3-minute video [Copy other people's work to do data science](data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) from the series [Data Science for Beginners](data-science-for-beginners-the-5-questions-data-science-answers.md).</span></span>

[!INCLUDE [machine-learning-free-trial](../../../includes/machine-learning-free-trial.md)]

## <a name="find-an-experiment-to-copy-in-azure-ai-gallery"></a><span data-ttu-id="412c5-110">Find an experiment to copy in Azure AI Gallery</span><span class="sxs-lookup"><span data-stu-id="412c5-110">Find an experiment to copy in Azure AI Gallery</span></span>
<span data-ttu-id="412c5-111">To see what experiments are available, go to the [Gallery](https://gallery.cortanaintelligence.com/) and click **Experiments** at the top of the page.</span><span class="sxs-lookup"><span data-stu-id="412c5-111">To see what experiments are available, go to the [Gallery](https://gallery.cortanaintelligence.com/) and click **Experiments** at the top of the page.</span></span>

### <a name="find-the-newest-or-most-popular-experiments"></a><span data-ttu-id="412c5-112">Find the newest or most popular experiments</span><span class="sxs-lookup"><span data-stu-id="412c5-112">Find the newest or most popular experiments</span></span>
<span data-ttu-id="412c5-113">On this page, you can see **Recently added** experiments, or scroll down to look at **What's popular** or the latest **Popular Microsoft experiments**.</span><span class="sxs-lookup"><span data-stu-id="412c5-113">On this page, you can see **Recently added** experiments, or scroll down to look at **What's popular** or the latest **Popular Microsoft experiments**.</span></span>

### <a name="look-for-an-experiment-that-meets-specific-requirements"></a><span data-ttu-id="412c5-114">Look for an experiment that meets specific requirements</span><span class="sxs-lookup"><span data-stu-id="412c5-114">Look for an experiment that meets specific requirements</span></span>
<span data-ttu-id="412c5-115">To browse all experiments:</span><span class="sxs-lookup"><span data-stu-id="412c5-115">To browse all experiments:</span></span>

1. <span data-ttu-id="412c5-116">Click **Browse all** at the top of the page.</span><span class="sxs-lookup"><span data-stu-id="412c5-116">Click **Browse all** at the top of the page.</span></span>
2. <span data-ttu-id="412c5-117">On the left-hand side, under **Refine by** in the **Categories** section, select **Experiment** to see all the experiments in the Gallery.</span><span class="sxs-lookup"><span data-stu-id="412c5-117">On the left-hand side, under **Refine by** in the **Categories** section, select **Experiment** to see all the experiments in the Gallery.</span></span>
3. <span data-ttu-id="412c5-118">You can find experiments that meet your requirements a couple different ways:</span><span class="sxs-lookup"><span data-stu-id="412c5-118">You can find experiments that meet your requirements a couple different ways:</span></span>
   * <span data-ttu-id="412c5-119">**Select filters on the left.**</span><span class="sxs-lookup"><span data-stu-id="412c5-119">**Select filters on the left.**</span></span> <span data-ttu-id="412c5-120">For example, to browse experiments that use a PCA-based anomaly detection algorithm: Under **Categories** click **Experiment**.</span><span class="sxs-lookup"><span data-stu-id="412c5-120">For example, to browse experiments that use a PCA-based anomaly detection algorithm: Under **Categories** click **Experiment**.</span></span> <span data-ttu-id="412c5-121">Then, under **Algorithms Used**, click **Show all** and in the dialog box choose **PCA-Based Anomaly Detection**.</span><span class="sxs-lookup"><span data-stu-id="412c5-121">Then, under **Algorithms Used**, click **Show all** and in the dialog box choose **PCA-Based Anomaly Detection**.</span></span> <span data-ttu-id="412c5-122">You may have to scroll to see it.</span><span class="sxs-lookup"><span data-stu-id="412c5-122">You may have to scroll to see it.</span></span><br></br>
     <span data-ttu-id="412c5-123">![Select filters](./media/sample-experiments/choose-an-algorithm.png)</span><span class="sxs-lookup"><span data-stu-id="412c5-123">![Select filters](./media/sample-experiments/choose-an-algorithm.png)</span></span>
   * <span data-ttu-id="412c5-124">**Use the search box.**</span><span class="sxs-lookup"><span data-stu-id="412c5-124">**Use the search box.**</span></span> <span data-ttu-id="412c5-125">For example, to find experiments contributed by Microsoft related to digit recognition that use a two-class support vector machine algorithm, enter "digit recognition" in the search box.</span><span class="sxs-lookup"><span data-stu-id="412c5-125">For example, to find experiments contributed by Microsoft related to digit recognition that use a two-class support vector machine algorithm, enter "digit recognition" in the search box.</span></span> <span data-ttu-id="412c5-126">Then, select the filters **Experiment**, **Microsoft content only**, and **Two-Class Support Vector Machine**:</span><span class="sxs-lookup"><span data-stu-id="412c5-126">Then, select the filters **Experiment**, **Microsoft content only**, and **Two-Class Support Vector Machine**:</span></span><br></br>
     <span data-ttu-id="412c5-127">![Use the search box](./media/sample-experiments/search-for-experiments.png)</span><span class="sxs-lookup"><span data-stu-id="412c5-127">![Use the search box](./media/sample-experiments/search-for-experiments.png)</span></span>
4. <span data-ttu-id="412c5-128">Click an experiment to learn more about it.</span><span class="sxs-lookup"><span data-stu-id="412c5-128">Click an experiment to learn more about it.</span></span>
5. <span data-ttu-id="412c5-129">To run and/or modify the experiment, click **Open in Studio** on the experiment's page.</span><span class="sxs-lookup"><span data-stu-id="412c5-129">To run and/or modify the experiment, click **Open in Studio** on the experiment's page.</span></span> <br></br>

    ![Example experiment](./media/sample-experiments/example-experiment.png)

    > [!NOTE]
    > <span data-ttu-id="412c5-131">When you open an experiment in Machine Learning Studio for the first time, you can try it for free or buy an Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="412c5-131">When you open an experiment in Machine Learning Studio for the first time, you can try it for free or buy an Azure subscription.</span></span> [<span data-ttu-id="412c5-132">Learn about the Machine Learning Studio free trial vs. paid service</span><span class="sxs-lookup"><span data-stu-id="412c5-132">Learn about the Machine Learning Studio free trial vs. paid service</span></span>](https://azure.microsoft.com/pricing/details/machine-learning/)
    >
    >

## <a name="create-a-new-experiment-using-an-example-as-a-template"></a><span data-ttu-id="412c5-133">Create a new experiment using an example as a template</span><span class="sxs-lookup"><span data-stu-id="412c5-133">Create a new experiment using an example as a template</span></span>
<span data-ttu-id="412c5-134">You also can create a new experiment in Machine Learning Studio using a Gallery example as a template.</span><span class="sxs-lookup"><span data-stu-id="412c5-134">You also can create a new experiment in Machine Learning Studio using a Gallery example as a template.</span></span>

1. <span data-ttu-id="412c5-135">Sign in with your Microsoft account credentials to the [Studio](https://studio.azureml.net), and then click **New** to create an experiment.</span><span class="sxs-lookup"><span data-stu-id="412c5-135">Sign in with your Microsoft account credentials to the [Studio](https://studio.azureml.net), and then click **New** to create an experiment.</span></span>
2. <span data-ttu-id="412c5-136">Browse through the example content and click one.</span><span class="sxs-lookup"><span data-stu-id="412c5-136">Browse through the example content and click one.</span></span>

<span data-ttu-id="412c5-137">A new experiment is created in your Machine Learning Studio workspace using the example experiment as a template.</span><span class="sxs-lookup"><span data-stu-id="412c5-137">A new experiment is created in your Machine Learning Studio workspace using the example experiment as a template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="412c5-138">Next steps</span><span class="sxs-lookup"><span data-stu-id="412c5-138">Next steps</span></span>
* [<span data-ttu-id="412c5-139">Import data from various sources</span><span class="sxs-lookup"><span data-stu-id="412c5-139">Import data from various sources</span></span>](import-data.md)
* [<span data-ttu-id="412c5-140">Quickstart tutorial for the R language in Machine Learning</span><span class="sxs-lookup"><span data-stu-id="412c5-140">Quickstart tutorial for the R language in Machine Learning</span></span>](r-quickstart.md)
* [<span data-ttu-id="412c5-141">Deploy a Machine Learning web service</span><span class="sxs-lookup"><span data-stu-id="412c5-141">Deploy a Machine Learning web service</span></span>](publish-a-machine-learning-web-service.md)
