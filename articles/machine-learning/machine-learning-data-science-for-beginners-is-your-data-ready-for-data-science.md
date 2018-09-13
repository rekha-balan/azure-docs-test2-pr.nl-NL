---
title: Is your data ready for data science? Data evaluation - Azure | Microsoft Docs
description: Learn the 4 criteria for data to be ready for data science. Data Science for Beginners video 2 has concrete examples to help with basic data evaluation.
keywords: relevant data,evaluate data,prepare data,data criteria,data ready
services: machine-learning
documentationcenter: na
author: cjgronlund
manager: jhubbard
editor: cjgronlund
ms.assetid: d502062c-da70-4b21-9054-0bfd9902612e
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/09/2017
ms.author: cgronlun;garye
ms.openlocfilehash: 09651839c2a30042e41ae33a5d77fa72ce8b22e2
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556061"
---
# <a name="is-your-data-ready-for-data-science"></a><span data-ttu-id="f90ca-106">Is your data ready for data science?</span><span class="sxs-lookup"><span data-stu-id="f90ca-106">Is your data ready for data science?</span></span>
## <a name="video-2-data-science-for-beginners-series"></a><span data-ttu-id="f90ca-107">Video 2: Data Science for Beginners series</span><span class="sxs-lookup"><span data-stu-id="f90ca-107">Video 2: Data Science for Beginners series</span></span>
<span data-ttu-id="f90ca-108">Learn how to evaluate your data to make sure it meets basic criteria to be ready for data science.</span><span class="sxs-lookup"><span data-stu-id="f90ca-108">Learn how to evaluate your data to make sure it meets basic criteria to be ready for data science.</span></span>

<span data-ttu-id="f90ca-109">To get the most out of the series, watch them all.</span><span class="sxs-lookup"><span data-stu-id="f90ca-109">To get the most out of the series, watch them all.</span></span> [<span data-ttu-id="f90ca-110">Go to the list of videos</span><span class="sxs-lookup"><span data-stu-id="f90ca-110">Go to the list of videos</span></span>](#other-videos-in-this-series)

> [!VIDEO https://channel9.msdn.com/Shows/SupervisionNotRequired/9/player]
>
>

## <a name="other-videos-in-this-series"></a><span data-ttu-id="f90ca-111">Other videos in this series</span><span class="sxs-lookup"><span data-stu-id="f90ca-111">Other videos in this series</span></span>
<span data-ttu-id="f90ca-112">*Data Science for Beginners* is a quick introduction to data science in five short videos.</span><span class="sxs-lookup"><span data-stu-id="f90ca-112">*Data Science for Beginners* is a quick introduction to data science in five short videos.</span></span>

* <span data-ttu-id="f90ca-113">Video 1: [The 5 questions data science answers](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) *(5 min 14 sec)*</span><span class="sxs-lookup"><span data-stu-id="f90ca-113">Video 1: [The 5 questions data science answers](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) *(5 min 14 sec)*</span></span>
* <span data-ttu-id="f90ca-114">Video 2: Is your data ready for data science?</span><span class="sxs-lookup"><span data-stu-id="f90ca-114">Video 2: Is your data ready for data science?</span></span>
* <span data-ttu-id="f90ca-115">Video 3: [Ask a question you can answer with data](machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data.md) *(4 min 17 sec)*</span><span class="sxs-lookup"><span data-stu-id="f90ca-115">Video 3: [Ask a question you can answer with data](machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data.md) *(4 min 17 sec)*</span></span>
* <span data-ttu-id="f90ca-116">Video 4: [Predict an answer with a simple model](machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model.md) *(7 min 42 sec)*</span><span class="sxs-lookup"><span data-stu-id="f90ca-116">Video 4: [Predict an answer with a simple model](machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model.md) *(7 min 42 sec)*</span></span>
* <span data-ttu-id="f90ca-117">Video 5: [Copy other people's work to do data science](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) *(3 min 18 sec)*</span><span class="sxs-lookup"><span data-stu-id="f90ca-117">Video 5: [Copy other people's work to do data science](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) *(3 min 18 sec)*</span></span>

## <a name="transcript-is-your-data-ready-for-data-science"></a><span data-ttu-id="f90ca-118">Transcript: Is your data ready for data science?</span><span class="sxs-lookup"><span data-stu-id="f90ca-118">Transcript: Is your data ready for data science?</span></span>
<span data-ttu-id="f90ca-119">Welcome to "Is your data ready for data science?"</span><span class="sxs-lookup"><span data-stu-id="f90ca-119">Welcome to "Is your data ready for data science?"</span></span> <span data-ttu-id="f90ca-120">the second video in the series *Data Science for Beginners*.</span><span class="sxs-lookup"><span data-stu-id="f90ca-120">the second video in the series *Data Science for Beginners*.</span></span>  

<span data-ttu-id="f90ca-121">Before data science can give you the answers you want, you have to give it some high-quality raw materials to work with.</span><span class="sxs-lookup"><span data-stu-id="f90ca-121">Before data science can give you the answers you want, you have to give it some high-quality raw materials to work with.</span></span> <span data-ttu-id="f90ca-122">Just like making a pizza, the better the ingredients you start with, the better the final product.</span><span class="sxs-lookup"><span data-stu-id="f90ca-122">Just like making a pizza, the better the ingredients you start with, the better the final product.</span></span>

## <a name="criteria-for-data"></a><span data-ttu-id="f90ca-123">Criteria for data</span><span class="sxs-lookup"><span data-stu-id="f90ca-123">Criteria for data</span></span>
<span data-ttu-id="f90ca-124">So, in the case of data science, there are some ingredients that we need to pull together.</span><span class="sxs-lookup"><span data-stu-id="f90ca-124">So, in the case of data science, there are some ingredients that we need to pull together.</span></span>

<span data-ttu-id="f90ca-125">We need data that is:</span><span class="sxs-lookup"><span data-stu-id="f90ca-125">We need data that is:</span></span>

* <span data-ttu-id="f90ca-126">Relevant</span><span class="sxs-lookup"><span data-stu-id="f90ca-126">Relevant</span></span>
* <span data-ttu-id="f90ca-127">Connected</span><span class="sxs-lookup"><span data-stu-id="f90ca-127">Connected</span></span>
* <span data-ttu-id="f90ca-128">Accurate</span><span class="sxs-lookup"><span data-stu-id="f90ca-128">Accurate</span></span>
* <span data-ttu-id="f90ca-129">Enough to work with</span><span class="sxs-lookup"><span data-stu-id="f90ca-129">Enough to work with</span></span>

## <a name="is-your-data-relevant"></a><span data-ttu-id="f90ca-130">Is your data relevant?</span><span class="sxs-lookup"><span data-stu-id="f90ca-130">Is your data relevant?</span></span>
<span data-ttu-id="f90ca-131">So the first ingredient - we need data that's relevant.</span><span class="sxs-lookup"><span data-stu-id="f90ca-131">So the first ingredient - we need data that's relevant.</span></span>

![Relevant data vs. irrelevant data - evaluate data](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science/machine-learning-data-science-relevant-and-irrelevant-data.png)

<span data-ttu-id="f90ca-133">Look at the table on the left.</span><span class="sxs-lookup"><span data-stu-id="f90ca-133">Look at the table on the left.</span></span> <span data-ttu-id="f90ca-134">We met seven people outside of Boston bars, measured their blood alcohol level, the Red Sox batting average in their last game, and the price of milk in the nearest convenience store.</span><span class="sxs-lookup"><span data-stu-id="f90ca-134">We met seven people outside of Boston bars, measured their blood alcohol level, the Red Sox batting average in their last game, and the price of milk in the nearest convenience store.</span></span>

<span data-ttu-id="f90ca-135">This is all perfectly legitimate data.</span><span class="sxs-lookup"><span data-stu-id="f90ca-135">This is all perfectly legitimate data.</span></span> <span data-ttu-id="f90ca-136">It’s only fault is that it isn’t relevant.</span><span class="sxs-lookup"><span data-stu-id="f90ca-136">It’s only fault is that it isn’t relevant.</span></span> <span data-ttu-id="f90ca-137">There's no obvious relationship between these numbers.</span><span class="sxs-lookup"><span data-stu-id="f90ca-137">There's no obvious relationship between these numbers.</span></span> <span data-ttu-id="f90ca-138">If I gave you the current price of milk and the Red Sox batting average, there's no way you could guess my blood alcohol content.</span><span class="sxs-lookup"><span data-stu-id="f90ca-138">If I gave you the current price of milk and the Red Sox batting average, there's no way you could guess my blood alcohol content.</span></span>

<span data-ttu-id="f90ca-139">Now look at the table on the right.</span><span class="sxs-lookup"><span data-stu-id="f90ca-139">Now look at the table on the right.</span></span> <span data-ttu-id="f90ca-140">This time we measured each person’s body mass and counted the number of drinks they’ve had.</span><span class="sxs-lookup"><span data-stu-id="f90ca-140">This time we measured each person’s body mass and counted the number of drinks they’ve had.</span></span>  <span data-ttu-id="f90ca-141">The numbers in each row are now relevant to each other.</span><span class="sxs-lookup"><span data-stu-id="f90ca-141">The numbers in each row are now relevant to each other.</span></span> <span data-ttu-id="f90ca-142">If I gave you my body mass and the number of Margaritas I've had, you could make a guess at my blood alcohol content.</span><span class="sxs-lookup"><span data-stu-id="f90ca-142">If I gave you my body mass and the number of Margaritas I've had, you could make a guess at my blood alcohol content.</span></span>

## <a name="do-you-have-connected-data"></a><span data-ttu-id="f90ca-143">Do you have connected data?</span><span class="sxs-lookup"><span data-stu-id="f90ca-143">Do you have connected data?</span></span>
<span data-ttu-id="f90ca-144">The next ingredient is connected data.</span><span class="sxs-lookup"><span data-stu-id="f90ca-144">The next ingredient is connected data.</span></span>

![Connected data vs. disconnected data - data criteria, data ready](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science/machine-learning-data-science-connected-vs-disconnected-data.png)

<span data-ttu-id="f90ca-146">Here is some relevant data on the quality of hamburgers: grill temperature, patty weight, and rating in the local food magazine.</span><span class="sxs-lookup"><span data-stu-id="f90ca-146">Here is some relevant data on the quality of hamburgers: grill temperature, patty weight, and rating in the local food magazine.</span></span> <span data-ttu-id="f90ca-147">But notice the gaps in the table on the left.</span><span class="sxs-lookup"><span data-stu-id="f90ca-147">But notice the gaps in the table on the left.</span></span>

<span data-ttu-id="f90ca-148">Most data sets are missing some values.</span><span class="sxs-lookup"><span data-stu-id="f90ca-148">Most data sets are missing some values.</span></span> <span data-ttu-id="f90ca-149">It's common to have holes like this and there are ways to work around them.</span><span class="sxs-lookup"><span data-stu-id="f90ca-149">It's common to have holes like this and there are ways to work around them.</span></span> <span data-ttu-id="f90ca-150">But if there's too much missing, your data begins to look like Swiss cheese.</span><span class="sxs-lookup"><span data-stu-id="f90ca-150">But if there's too much missing, your data begins to look like Swiss cheese.</span></span>

<span data-ttu-id="f90ca-151">If you look at the table on the left, there's so much missing data, it's hard to come up with any kind of relationship between grill temperature and patty weight.</span><span class="sxs-lookup"><span data-stu-id="f90ca-151">If you look at the table on the left, there's so much missing data, it's hard to come up with any kind of relationship between grill temperature and patty weight.</span></span> <span data-ttu-id="f90ca-152">This is an example of disconnected data.</span><span class="sxs-lookup"><span data-stu-id="f90ca-152">This is an example of disconnected data.</span></span>

<span data-ttu-id="f90ca-153">The table on the right, though, is full and complete - an example of connected data.</span><span class="sxs-lookup"><span data-stu-id="f90ca-153">The table on the right, though, is full and complete - an example of connected data.</span></span>

## <a name="is-your-data-accurate"></a><span data-ttu-id="f90ca-154">Is your data accurate?</span><span class="sxs-lookup"><span data-stu-id="f90ca-154">Is your data accurate?</span></span>
<span data-ttu-id="f90ca-155">The next ingredient we need is accuracy.</span><span class="sxs-lookup"><span data-stu-id="f90ca-155">The next ingredient we need is accuracy.</span></span> <span data-ttu-id="f90ca-156">Here are four targets that we’d like to hit with arrows.</span><span class="sxs-lookup"><span data-stu-id="f90ca-156">Here are four targets that we’d like to hit with arrows.</span></span>

![Accurate data vs. inaccurate data - data criteria](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science/machine-learning-data-science-inaccurate-vs-accurate-data.png)

<span data-ttu-id="f90ca-158">Look at the target in the upper right.</span><span class="sxs-lookup"><span data-stu-id="f90ca-158">Look at the target in the upper right.</span></span> <span data-ttu-id="f90ca-159">We’ve got a tight grouping right around the bullseye.</span><span class="sxs-lookup"><span data-stu-id="f90ca-159">We’ve got a tight grouping right around the bullseye.</span></span> <span data-ttu-id="f90ca-160">That, of course, is accurate.</span><span class="sxs-lookup"><span data-stu-id="f90ca-160">That, of course, is accurate.</span></span> <span data-ttu-id="f90ca-161">Oddly, in the language of data science, our performance on the target right below it is also considered accurate.</span><span class="sxs-lookup"><span data-stu-id="f90ca-161">Oddly, in the language of data science, our performance on the target right below it is also considered accurate.</span></span>

<span data-ttu-id="f90ca-162">If you were to map out the center of these arrows, you'd see that it's very close to the bullseye.</span><span class="sxs-lookup"><span data-stu-id="f90ca-162">If you were to map out the center of these arrows, you'd see that it's very close to the bullseye.</span></span> <span data-ttu-id="f90ca-163">The arrows are spread out all around the target, so they're considered imprecise, but they're centered around the bullseye, so they're considered accurate.</span><span class="sxs-lookup"><span data-stu-id="f90ca-163">The arrows are spread out all around the target, so they're considered imprecise, but they're centered around the bullseye, so they're considered accurate.</span></span>

<span data-ttu-id="f90ca-164">Now look at the upper-left target.</span><span class="sxs-lookup"><span data-stu-id="f90ca-164">Now look at the upper-left target.</span></span> <span data-ttu-id="f90ca-165">Here our arrows hit very close together, a tight grouping.</span><span class="sxs-lookup"><span data-stu-id="f90ca-165">Here our arrows hit very close together, a tight grouping.</span></span> <span data-ttu-id="f90ca-166">They're precise, but they're inaccurate because the center is way off the bullseye.</span><span class="sxs-lookup"><span data-stu-id="f90ca-166">They're precise, but they're inaccurate because the center is way off the bullseye.</span></span> <span data-ttu-id="f90ca-167">And, of course, the arrows in the bottom-left target are both inaccurate and imprecise.</span><span class="sxs-lookup"><span data-stu-id="f90ca-167">And, of course, the arrows in the bottom-left target are both inaccurate and imprecise.</span></span> <span data-ttu-id="f90ca-168">This archer needs more practice.</span><span class="sxs-lookup"><span data-stu-id="f90ca-168">This archer needs more practice.</span></span>

## <a name="do-you-have-enough-data-to-work-with"></a><span data-ttu-id="f90ca-169">Do you have enough data to work with?</span><span class="sxs-lookup"><span data-stu-id="f90ca-169">Do you have enough data to work with?</span></span>
<span data-ttu-id="f90ca-170">Finally, ingredient #4 - we need to have enough data.</span><span class="sxs-lookup"><span data-stu-id="f90ca-170">Finally, ingredient #4 - we need to have enough data.</span></span>

![Do you have enough data for analysis?](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science/machine-learning-data-science-barely-enough-data.png)

<span data-ttu-id="f90ca-173">Think of each data point in your table as being a brush stroke in a painting.</span><span class="sxs-lookup"><span data-stu-id="f90ca-173">Think of each data point in your table as being a brush stroke in a painting.</span></span> <span data-ttu-id="f90ca-174">If you have only a few of them, the painting can be pretty fuzzy - it's hard to tell what it is.</span><span class="sxs-lookup"><span data-stu-id="f90ca-174">If you have only a few of them, the painting can be pretty fuzzy - it's hard to tell what it is.</span></span>

<span data-ttu-id="f90ca-175">If you add some more brush strokes, then your painting starts to get a little sharper.</span><span class="sxs-lookup"><span data-stu-id="f90ca-175">If you add some more brush strokes, then your painting starts to get a little sharper.</span></span>

<span data-ttu-id="f90ca-176">When you have barely enough strokes, you can see just enough to make some broad decisions.</span><span class="sxs-lookup"><span data-stu-id="f90ca-176">When you have barely enough strokes, you can see just enough to make some broad decisions.</span></span> <span data-ttu-id="f90ca-177">Is it somewhere I might want to visit?</span><span class="sxs-lookup"><span data-stu-id="f90ca-177">Is it somewhere I might want to visit?</span></span> <span data-ttu-id="f90ca-178">It looks bright, that looks like clean water – yes, that’s where I’m going on vacation.</span><span class="sxs-lookup"><span data-stu-id="f90ca-178">It looks bright, that looks like clean water – yes, that’s where I’m going on vacation.</span></span>

<span data-ttu-id="f90ca-179">As you add more data, the picture becomes clearer and you can make more detailed decisions.</span><span class="sxs-lookup"><span data-stu-id="f90ca-179">As you add more data, the picture becomes clearer and you can make more detailed decisions.</span></span> <span data-ttu-id="f90ca-180">Now I can look at the three hotels on the left bank.</span><span class="sxs-lookup"><span data-stu-id="f90ca-180">Now I can look at the three hotels on the left bank.</span></span> <span data-ttu-id="f90ca-181">You know, I really like the architectural features of the one in the foreground.</span><span class="sxs-lookup"><span data-stu-id="f90ca-181">You know, I really like the architectural features of the one in the foreground.</span></span> <span data-ttu-id="f90ca-182">I’ll stay there, on the third floor.</span><span class="sxs-lookup"><span data-stu-id="f90ca-182">I’ll stay there, on the third floor.</span></span>

<span data-ttu-id="f90ca-183">With data that's relevant, connected, accurate, and enough, we have all the ingredients we need to do some high-quality data science.</span><span class="sxs-lookup"><span data-stu-id="f90ca-183">With data that's relevant, connected, accurate, and enough, we have all the ingredients we need to do some high-quality data science.</span></span>

<span data-ttu-id="f90ca-184">Be sure to check out the other four videos in *Data Science for Beginners* from Microsoft Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="f90ca-184">Be sure to check out the other four videos in *Data Science for Beginners* from Microsoft Azure Machine Learning.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f90ca-185">Next steps</span><span class="sxs-lookup"><span data-stu-id="f90ca-185">Next steps</span></span>
* [<span data-ttu-id="f90ca-186">Try a first data science experiment with Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="f90ca-186">Try a first data science experiment with Machine Learning Studio</span></span>](machine-learning-create-experiment.md)
* [<span data-ttu-id="f90ca-187">Get an introduction to Machine Learning on Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="f90ca-187">Get an introduction to Machine Learning on Microsoft Azure</span></span>](machine-learning-what-is-machine-learning.md)




