---
title: Copy others' data science examples – Azure Machine Learning  | Microsoft Docs
description: 'Trade secret of data science: Get others to do your work for you. Get machine learning examples from the Azure AI Gallery.'
keywords: data science examples,machine learning example,clustering algorithm,clustering algorithm example
services: machine-learning
documentationcenter: na
author: heatherbshapiro
ms.author: hshapiro
manager: hjerez
editor: cjgronlund
ms.assetid: ec2be823-c325-4ad8-b8b2-3e664f1a44b4
ms.service: machine-learning
ms.component: studio
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/05/2018
ms.openlocfilehash: 84c6f4a1cedc0a04ee820f1de60f51e653f28425
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865093"
---
# <a name="copy-other-peoples-work-to-do-data-science"></a><span data-ttu-id="e3180-105">Copy other people's work to do data science</span><span class="sxs-lookup"><span data-stu-id="e3180-105">Copy other people's work to do data science</span></span>
## <a name="video-5-data-science-for-beginners-series"></a><span data-ttu-id="e3180-106">Video 5: Data Science for Beginners series</span><span class="sxs-lookup"><span data-stu-id="e3180-106">Video 5: Data Science for Beginners series</span></span>
<span data-ttu-id="e3180-107">One of the trade secrets of data science is getting other people to do your work for you.</span><span class="sxs-lookup"><span data-stu-id="e3180-107">One of the trade secrets of data science is getting other people to do your work for you.</span></span> <span data-ttu-id="e3180-108">Find a clustering algorithm example in Azure AI Gallery to use for your own machine learning experiment.</span><span class="sxs-lookup"><span data-stu-id="e3180-108">Find a clustering algorithm example in Azure AI Gallery to use for your own machine learning experiment.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e3180-109">**Cortana Intelligence Gallery** was renamed **Azure AI Gallery**.</span><span class="sxs-lookup"><span data-stu-id="e3180-109">**Cortana Intelligence Gallery** was renamed **Azure AI Gallery**.</span></span> <span data-ttu-id="e3180-110">As a result, text and images in this transcript vary slightly from the video, which uses the former name.</span><span class="sxs-lookup"><span data-stu-id="e3180-110">As a result, text and images in this transcript vary slightly from the video, which uses the former name.</span></span>
>

<span data-ttu-id="e3180-111">To get the most out of the series, watch them all.</span><span class="sxs-lookup"><span data-stu-id="e3180-111">To get the most out of the series, watch them all.</span></span> [<span data-ttu-id="e3180-112">Go to the list of videos</span><span class="sxs-lookup"><span data-stu-id="e3180-112">Go to the list of videos</span></span>](#other-videos-in-this-series)
<br>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/data-science-for-beginners-series-copy-other-peoples-work-to-do-data-science/player]
>
>

## <a name="other-videos-in-this-series"></a><span data-ttu-id="e3180-113">Other videos in this series</span><span class="sxs-lookup"><span data-stu-id="e3180-113">Other videos in this series</span></span>
<span data-ttu-id="e3180-114">*Data Science for Beginners* is a quick introduction to data science in five short videos.</span><span class="sxs-lookup"><span data-stu-id="e3180-114">*Data Science for Beginners* is a quick introduction to data science in five short videos.</span></span>

* <span data-ttu-id="e3180-115">Video 1: [The 5 questions data science answers](data-science-for-beginners-the-5-questions-data-science-answers.md) *(5 min 14 sec)*</span><span class="sxs-lookup"><span data-stu-id="e3180-115">Video 1: [The 5 questions data science answers](data-science-for-beginners-the-5-questions-data-science-answers.md) *(5 min 14 sec)*</span></span>
* <span data-ttu-id="e3180-116">Video 2: [Is your data ready for data science?](data-science-for-beginners-is-your-data-ready-for-data-science.md)</span><span class="sxs-lookup"><span data-stu-id="e3180-116">Video 2: [Is your data ready for data science?](data-science-for-beginners-is-your-data-ready-for-data-science.md)</span></span> <span data-ttu-id="e3180-117">*(4 min 56 sec)*</span><span class="sxs-lookup"><span data-stu-id="e3180-117">*(4 min 56 sec)*</span></span>
* <span data-ttu-id="e3180-118">Video 3: [Ask a question you can answer with data](data-science-for-beginners-ask-a-question-you-can-answer-with-data.md) *(4 min 17 sec)*</span><span class="sxs-lookup"><span data-stu-id="e3180-118">Video 3: [Ask a question you can answer with data](data-science-for-beginners-ask-a-question-you-can-answer-with-data.md) *(4 min 17 sec)*</span></span>
* <span data-ttu-id="e3180-119">Video 4: [Predict an answer with a simple model](data-science-for-beginners-predict-an-answer-with-a-simple-model.md) *(7 min 42 sec)*</span><span class="sxs-lookup"><span data-stu-id="e3180-119">Video 4: [Predict an answer with a simple model](data-science-for-beginners-predict-an-answer-with-a-simple-model.md) *(7 min 42 sec)*</span></span>
* <span data-ttu-id="e3180-120">Video 5: Copy other people's work to do data science</span><span class="sxs-lookup"><span data-stu-id="e3180-120">Video 5: Copy other people's work to do data science</span></span>

## <a name="transcript-copy-other-peoples-work-to-do-data-science"></a><span data-ttu-id="e3180-121">Transcript: Copy other people's work to do data science</span><span class="sxs-lookup"><span data-stu-id="e3180-121">Transcript: Copy other people's work to do data science</span></span>
<span data-ttu-id="e3180-122">Welcome to the fifth video in the series "Data Science for Beginners."</span><span class="sxs-lookup"><span data-stu-id="e3180-122">Welcome to the fifth video in the series "Data Science for Beginners."</span></span>

<span data-ttu-id="e3180-123">In this one, you’ll discover a place to find examples that you can borrow from as a starting point for your own work.</span><span class="sxs-lookup"><span data-stu-id="e3180-123">In this one, you’ll discover a place to find examples that you can borrow from as a starting point for your own work.</span></span> <span data-ttu-id="e3180-124">You might get the most out of this video if you first watch the earlier videos in this series.</span><span class="sxs-lookup"><span data-stu-id="e3180-124">You might get the most out of this video if you first watch the earlier videos in this series.</span></span>

<span data-ttu-id="e3180-125">One of the trade secrets of data science is getting other people to do your work for you.</span><span class="sxs-lookup"><span data-stu-id="e3180-125">One of the trade secrets of data science is getting other people to do your work for you.</span></span>

## <a name="find-examples-in-the-azure-ai-gallery"></a><span data-ttu-id="e3180-126">Find examples in the Azure AI Gallery</span><span class="sxs-lookup"><span data-stu-id="e3180-126">Find examples in the Azure AI Gallery</span></span>

<span data-ttu-id="e3180-127">Microsoft has a cloud-based service called [Azure Machine Learning Studio](https://azure.microsoft.com/services/machine-learning-studio/) that you're welcome to try for free.</span><span class="sxs-lookup"><span data-stu-id="e3180-127">Microsoft has a cloud-based service called [Azure Machine Learning Studio](https://azure.microsoft.com/services/machine-learning-studio/) that you're welcome to try for free.</span></span> <span data-ttu-id="e3180-128">It provides you with a workspace where you can experiment with different machine learning algorithms, and, when you've got your solution worked out, you can launch it as a web service.</span><span class="sxs-lookup"><span data-stu-id="e3180-128">It provides you with a workspace where you can experiment with different machine learning algorithms, and, when you've got your solution worked out, you can launch it as a web service.</span></span>

<span data-ttu-id="e3180-129">Part of this service is something called the **[Azure AI Gallery](https://gallery.cortanaintelligence.com/)**.</span><span class="sxs-lookup"><span data-stu-id="e3180-129">Part of this service is something called the **[Azure AI Gallery](https://gallery.cortanaintelligence.com/)**.</span></span> <span data-ttu-id="e3180-130">It contains resources, including a collection of Azure Machine Learning experiments, or models, that people have built and contributed for others to use.</span><span class="sxs-lookup"><span data-stu-id="e3180-130">It contains resources, including a collection of Azure Machine Learning experiments, or models, that people have built and contributed for others to use.</span></span> <span data-ttu-id="e3180-131">These experiments are a great way to leverage the thought and hard work of others to get you started on your own solutions.</span><span class="sxs-lookup"><span data-stu-id="e3180-131">These experiments are a great way to leverage the thought and hard work of others to get you started on your own solutions.</span></span> <span data-ttu-id="e3180-132">Everyone is welcome to browse through it.</span><span class="sxs-lookup"><span data-stu-id="e3180-132">Everyone is welcome to browse through it.</span></span>

![Azure AI Gallery](./media/data-science-for-beginners-copy-other-peoples-work-to-do-data-science/azure-ai-gallery.png)

<span data-ttu-id="e3180-134">If you click **Experiments** at the top, you'll see a number of the most recent and popular experiments in the gallery.</span><span class="sxs-lookup"><span data-stu-id="e3180-134">If you click **Experiments** at the top, you'll see a number of the most recent and popular experiments in the gallery.</span></span> <span data-ttu-id="e3180-135">You can search through the rest of experiments by clicking **Browse All** at the top of the screen, and there you can enter search terms and choose search filters.</span><span class="sxs-lookup"><span data-stu-id="e3180-135">You can search through the rest of experiments by clicking **Browse All** at the top of the screen, and there you can enter search terms and choose search filters.</span></span>

## <a name="find-and-use-a-clustering-algorithm-example"></a><span data-ttu-id="e3180-136">Find and use a clustering algorithm example</span><span class="sxs-lookup"><span data-stu-id="e3180-136">Find and use a clustering algorithm example</span></span>
<span data-ttu-id="e3180-137">So, for instance, let's say you want to see an example of how clustering works, so you search for **"clustering sweep"** experiments.</span><span class="sxs-lookup"><span data-stu-id="e3180-137">So, for instance, let's say you want to see an example of how clustering works, so you search for **"clustering sweep"** experiments.</span></span>

![Search for clustering experiments](./media/data-science-for-beginners-copy-other-peoples-work-to-do-data-science/search-for-clustering-experiments.png)

<span data-ttu-id="e3180-139">Here's an interesting one that someone contributed to the gallery.</span><span class="sxs-lookup"><span data-stu-id="e3180-139">Here's an interesting one that someone contributed to the gallery.</span></span>

![Clustering experiment](./media/data-science-for-beginners-copy-other-peoples-work-to-do-data-science/clustering-experiment.png)

<span data-ttu-id="e3180-141">Click on that experiment and you get a web page that describes the work that this contributor did, along with some of their results.</span><span class="sxs-lookup"><span data-stu-id="e3180-141">Click on that experiment and you get a web page that describes the work that this contributor did, along with some of their results.</span></span>

![Clustering experiment description page](./media/data-science-for-beginners-copy-other-peoples-work-to-do-data-science/clustering-experiment-description-page.png)

<span data-ttu-id="e3180-143">Notice the link that says **Open in Studio**.</span><span class="sxs-lookup"><span data-stu-id="e3180-143">Notice the link that says **Open in Studio**.</span></span>

![Open in Studio button](./media/data-science-for-beginners-copy-other-peoples-work-to-do-data-science/open-in-studio.png)

<span data-ttu-id="e3180-145">I can click on that and it takes me right to **Azure Machine Learning Studio**.</span><span class="sxs-lookup"><span data-stu-id="e3180-145">I can click on that and it takes me right to **Azure Machine Learning Studio**.</span></span> <span data-ttu-id="e3180-146">It creates a copy of the experiment and puts it in my own workspace.</span><span class="sxs-lookup"><span data-stu-id="e3180-146">It creates a copy of the experiment and puts it in my own workspace.</span></span> <span data-ttu-id="e3180-147">This includes the contributor's dataset, all the processing that they did, all of the algorithms that they used, and how they saved out the results.</span><span class="sxs-lookup"><span data-stu-id="e3180-147">This includes the contributor's dataset, all the processing that they did, all of the algorithms that they used, and how they saved out the results.</span></span>

![Open a Gallery experiment in Machine Learning Studio - clustering algorithm example](./media/data-science-for-beginners-copy-other-peoples-work-to-do-data-science/cluster-experiment-open-in-studio.png)

<span data-ttu-id="e3180-149">And now I have a starting point.</span><span class="sxs-lookup"><span data-stu-id="e3180-149">And now I have a starting point.</span></span> <span data-ttu-id="e3180-150">I can swap out their data for my own and do my own tweaking of the model.</span><span class="sxs-lookup"><span data-stu-id="e3180-150">I can swap out their data for my own and do my own tweaking of the model.</span></span> <span data-ttu-id="e3180-151">This gives me a running start, and it lets me build on the work of people who really know what they’re doing.</span><span class="sxs-lookup"><span data-stu-id="e3180-151">This gives me a running start, and it lets me build on the work of people who really know what they’re doing.</span></span>

## <a name="find-experiments-that-demonstrate-machine-learning-techniques"></a><span data-ttu-id="e3180-152">Find experiments that demonstrate machine learning techniques</span><span class="sxs-lookup"><span data-stu-id="e3180-152">Find experiments that demonstrate machine learning techniques</span></span>
<span data-ttu-id="e3180-153">There are other experiments in the [Azure AI Gallery](https://gallery.cortanaintelligence.com) that were contributed specifically to provide how-to examples for people new to data science.</span><span class="sxs-lookup"><span data-stu-id="e3180-153">There are other experiments in the [Azure AI Gallery](https://gallery.cortanaintelligence.com) that were contributed specifically to provide how-to examples for people new to data science.</span></span> <span data-ttu-id="e3180-154">For instance, there's an experiment in the gallery that demonstrates how to handle missing values ([Methods for handling missing values](https://gallery.cortanaintelligence.com/Experiment/Methods-for-handling-missing-values-1)).</span><span class="sxs-lookup"><span data-stu-id="e3180-154">For instance, there's an experiment in the gallery that demonstrates how to handle missing values ([Methods for handling missing values](https://gallery.cortanaintelligence.com/Experiment/Methods-for-handling-missing-values-1)).</span></span> <span data-ttu-id="e3180-155">It walks you through 15 different ways of substituting empty values, and talks about the benefits of each method and when to use it.</span><span class="sxs-lookup"><span data-stu-id="e3180-155">It walks you through 15 different ways of substituting empty values, and talks about the benefits of each method and when to use it.</span></span>

![Gallery experiments open in Machine Learning Studio - methods for missing values](./media/data-science-for-beginners-copy-other-peoples-work-to-do-data-science/experiment-methods-for-handling-missing-values.png)

<span data-ttu-id="e3180-157">[Azure AI Gallery](https://gallery.cortanaintelligence.com) is a place to find working experiments that you can use as a starting point for your own solutions.</span><span class="sxs-lookup"><span data-stu-id="e3180-157">[Azure AI Gallery](https://gallery.cortanaintelligence.com) is a place to find working experiments that you can use as a starting point for your own solutions.</span></span>

<span data-ttu-id="e3180-158">Be sure to check out the other videos in "Data Science for Beginners" from Microsoft Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="e3180-158">Be sure to check out the other videos in "Data Science for Beginners" from Microsoft Azure Machine Learning.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e3180-159">Next steps</span><span class="sxs-lookup"><span data-stu-id="e3180-159">Next steps</span></span>
* [<span data-ttu-id="e3180-160">Try your first data science experiment with Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="e3180-160">Try your first data science experiment with Azure Machine Learning</span></span>](create-experiment.md)
* [<span data-ttu-id="e3180-161">Get an introduction to Machine Learning on Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="e3180-161">Get an introduction to Machine Learning on Microsoft Azure</span></span>](what-is-machine-learning.md)
