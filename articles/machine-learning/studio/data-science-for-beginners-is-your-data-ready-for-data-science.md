---
title: Is your data ready for data science? Data evaluation - Azure Machine Learning | Microsoft Docs
description: Four criteria your data needs to meet to be ready for data science. This video has concrete examples to help with basic data evaluation.
keywords: relevant data,evaluate data,prepare data,data criteria,data ready
services: machine-learning
documentationcenter: na
author: heatherbshapiro
ms.author: hshapiro
manager: hjerez
editor: cjgronlund
ms.assetid: d502062c-da70-4b21-9054-0bfd9902612e
ms.service: machine-learning
ms.component: studio
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/03/2018
ms.openlocfilehash: 5ab3c7716485053432240cb74be8ebc60c9ad274
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865525"
---
# <a name="is-your-data-ready-for-data-science"></a><span data-ttu-id="755bc-106">Is your data ready for data science?</span><span class="sxs-lookup"><span data-stu-id="755bc-106">Is your data ready for data science?</span></span>
## <a name="video-2-data-science-for-beginners-series"></a><span data-ttu-id="755bc-107">Video 2: Data Science for Beginners series</span><span class="sxs-lookup"><span data-stu-id="755bc-107">Video 2: Data Science for Beginners series</span></span>
<span data-ttu-id="755bc-108">Learn how to evaluate your data to make sure it meets basic criteria to be ready for data science.</span><span class="sxs-lookup"><span data-stu-id="755bc-108">Learn how to evaluate your data to make sure it meets basic criteria to be ready for data science.</span></span>

<span data-ttu-id="755bc-109">To get the most out of the series, watch them all.</span><span class="sxs-lookup"><span data-stu-id="755bc-109">To get the most out of the series, watch them all.</span></span> [<span data-ttu-id="755bc-110">Go to the list of videos</span><span class="sxs-lookup"><span data-stu-id="755bc-110">Go to the list of videos</span></span>](#other-videos-in-this-series)
<br>

> [!VIDEO https://channel9.msdn.com/Shows/SupervisionNotRequired/9/player]
>
>

## <a name="other-videos-in-this-series"></a><span data-ttu-id="755bc-111">Other videos in this series</span><span class="sxs-lookup"><span data-stu-id="755bc-111">Other videos in this series</span></span>
<span data-ttu-id="755bc-112">*Data Science for Beginners* is a quick introduction to data science in five short videos.</span><span class="sxs-lookup"><span data-stu-id="755bc-112">*Data Science for Beginners* is a quick introduction to data science in five short videos.</span></span>

* <span data-ttu-id="755bc-113">Video 1: [The 5 questions data science answers](data-science-for-beginners-the-5-questions-data-science-answers.md) *(5 min 14 sec)*</span><span class="sxs-lookup"><span data-stu-id="755bc-113">Video 1: [The 5 questions data science answers](data-science-for-beginners-the-5-questions-data-science-answers.md) *(5 min 14 sec)*</span></span>
* <span data-ttu-id="755bc-114">Video 2: Is your data ready for data science?</span><span class="sxs-lookup"><span data-stu-id="755bc-114">Video 2: Is your data ready for data science?</span></span>
* <span data-ttu-id="755bc-115">Video 3: [Ask a question you can answer with data](data-science-for-beginners-ask-a-question-you-can-answer-with-data.md) *(4 min 17 sec)*</span><span class="sxs-lookup"><span data-stu-id="755bc-115">Video 3: [Ask a question you can answer with data](data-science-for-beginners-ask-a-question-you-can-answer-with-data.md) *(4 min 17 sec)*</span></span>
* <span data-ttu-id="755bc-116">Video 4: [Predict an answer with a simple model](data-science-for-beginners-predict-an-answer-with-a-simple-model.md) *(7 min 42 sec)*</span><span class="sxs-lookup"><span data-stu-id="755bc-116">Video 4: [Predict an answer with a simple model](data-science-for-beginners-predict-an-answer-with-a-simple-model.md) *(7 min 42 sec)*</span></span>
* <span data-ttu-id="755bc-117">Video 5: [Copy other people's work to do data science](data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) *(3 min 18 sec)*</span><span class="sxs-lookup"><span data-stu-id="755bc-117">Video 5: [Copy other people's work to do data science](data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) *(3 min 18 sec)*</span></span>

## <a name="transcript-is-your-data-ready-for-data-science"></a><span data-ttu-id="755bc-118">Transcript: Is your data ready for data science?</span><span class="sxs-lookup"><span data-stu-id="755bc-118">Transcript: Is your data ready for data science?</span></span>
<span data-ttu-id="755bc-119">Welcome to "Is your data ready for data science?"</span><span class="sxs-lookup"><span data-stu-id="755bc-119">Welcome to "Is your data ready for data science?"</span></span> <span data-ttu-id="755bc-120">the second video in the series *Data Science for Beginners*.</span><span class="sxs-lookup"><span data-stu-id="755bc-120">the second video in the series *Data Science for Beginners*.</span></span>  

<span data-ttu-id="755bc-121">Before data science can give you the answers you want, you have to give it some high-quality raw materials to work with.</span><span class="sxs-lookup"><span data-stu-id="755bc-121">Before data science can give you the answers you want, you have to give it some high-quality raw materials to work with.</span></span> <span data-ttu-id="755bc-122">Just like making a pizza, the better the ingredients you start with, the better the final product.</span><span class="sxs-lookup"><span data-stu-id="755bc-122">Just like making a pizza, the better the ingredients you start with, the better the final product.</span></span> 

## <a name="criteria-for-data"></a><span data-ttu-id="755bc-123">Criteria for data</span><span class="sxs-lookup"><span data-stu-id="755bc-123">Criteria for data</span></span>
<span data-ttu-id="755bc-124">In data science, there are certain ingredients that must be pulled together including:</span><span class="sxs-lookup"><span data-stu-id="755bc-124">In data science, there are certain ingredients that must be pulled together including:</span></span>

* <span data-ttu-id="755bc-125">Relevant</span><span class="sxs-lookup"><span data-stu-id="755bc-125">Relevant</span></span>
* <span data-ttu-id="755bc-126">Connected</span><span class="sxs-lookup"><span data-stu-id="755bc-126">Connected</span></span>
* <span data-ttu-id="755bc-127">Accurate</span><span class="sxs-lookup"><span data-stu-id="755bc-127">Accurate</span></span>
* <span data-ttu-id="755bc-128">Enough to work with</span><span class="sxs-lookup"><span data-stu-id="755bc-128">Enough to work with</span></span>

## <a name="is-your-data-relevant"></a><span data-ttu-id="755bc-129">Is your data relevant?</span><span class="sxs-lookup"><span data-stu-id="755bc-129">Is your data relevant?</span></span>
<span data-ttu-id="755bc-130">So the first ingredient - you need data that's relevant.</span><span class="sxs-lookup"><span data-stu-id="755bc-130">So the first ingredient - you need data that's relevant.</span></span>

![Relevant data vs. irrelevant data - evaluate data](./media/data-science-for-beginners-is-your-data-ready-for-data-science/relevant-and-irrelevant-data.png)

<span data-ttu-id="755bc-132">On the left, the table presents the blood alcohol level of seven people tested outside a Boston bar, the Red Sox batting average in their last game, and the price of milk in the nearest convenience store.</span><span class="sxs-lookup"><span data-stu-id="755bc-132">On the left, the table presents the blood alcohol level of seven people tested outside a Boston bar, the Red Sox batting average in their last game, and the price of milk in the nearest convenience store.</span></span>

<span data-ttu-id="755bc-133">This is all perfectly legitimate data.</span><span class="sxs-lookup"><span data-stu-id="755bc-133">This is all perfectly legitimate data.</span></span> <span data-ttu-id="755bc-134">It’s only fault is that it isn’t relevant.</span><span class="sxs-lookup"><span data-stu-id="755bc-134">It’s only fault is that it isn’t relevant.</span></span> <span data-ttu-id="755bc-135">There's no obvious relationship between these numbers.</span><span class="sxs-lookup"><span data-stu-id="755bc-135">There's no obvious relationship between these numbers.</span></span> <span data-ttu-id="755bc-136">If someone gave you the current price of milk and the Red Sox batting average, there's no way you could guess their blood alcohol content.</span><span class="sxs-lookup"><span data-stu-id="755bc-136">If someone gave you the current price of milk and the Red Sox batting average, there's no way you could guess their blood alcohol content.</span></span>

<span data-ttu-id="755bc-137">Now look at the table on the right.</span><span class="sxs-lookup"><span data-stu-id="755bc-137">Now look at the table on the right.</span></span> <span data-ttu-id="755bc-138">This time each person’s body mass was measured as well as the number of drinks they’ve had.</span><span class="sxs-lookup"><span data-stu-id="755bc-138">This time each person’s body mass was measured as well as the number of drinks they’ve had.</span></span>  <span data-ttu-id="755bc-139">The numbers in each row are now relevant to each other.</span><span class="sxs-lookup"><span data-stu-id="755bc-139">The numbers in each row are now relevant to each other.</span></span> <span data-ttu-id="755bc-140">If I gave you my body mass and the number of Margaritas I've had, you could make a guess at my blood alcohol content.</span><span class="sxs-lookup"><span data-stu-id="755bc-140">If I gave you my body mass and the number of Margaritas I've had, you could make a guess at my blood alcohol content.</span></span>

## <a name="do-you-have-connected-data"></a><span data-ttu-id="755bc-141">Do you have connected data?</span><span class="sxs-lookup"><span data-stu-id="755bc-141">Do you have connected data?</span></span>
<span data-ttu-id="755bc-142">The next ingredient is connected data.</span><span class="sxs-lookup"><span data-stu-id="755bc-142">The next ingredient is connected data.</span></span>

![Connected data vs. disconnected data - data criteria, data ready](./media/data-science-for-beginners-is-your-data-ready-for-data-science/connected-vs-disconnected-data.png)

<span data-ttu-id="755bc-144">Here is some relevant data on the quality of hamburgers: grill temperature, patty weight, and rating in the local food magazine.</span><span class="sxs-lookup"><span data-stu-id="755bc-144">Here is some relevant data on the quality of hamburgers: grill temperature, patty weight, and rating in the local food magazine.</span></span> <span data-ttu-id="755bc-145">But notice the gaps in the table on the left.</span><span class="sxs-lookup"><span data-stu-id="755bc-145">But notice the gaps in the table on the left.</span></span>

<span data-ttu-id="755bc-146">Most data sets are missing some values.</span><span class="sxs-lookup"><span data-stu-id="755bc-146">Most data sets are missing some values.</span></span> <span data-ttu-id="755bc-147">It's common to have holes like this and there are ways to work around them.</span><span class="sxs-lookup"><span data-stu-id="755bc-147">It's common to have holes like this and there are ways to work around them.</span></span> <span data-ttu-id="755bc-148">But if there's too much missing, your data begins to look like Swiss cheese.</span><span class="sxs-lookup"><span data-stu-id="755bc-148">But if there's too much missing, your data begins to look like Swiss cheese.</span></span>

<span data-ttu-id="755bc-149">If you look at the table on the left, there's so much missing data, it's hard to come up with any kind of relationship between grill temperature and patty weight.</span><span class="sxs-lookup"><span data-stu-id="755bc-149">If you look at the table on the left, there's so much missing data, it's hard to come up with any kind of relationship between grill temperature and patty weight.</span></span> <span data-ttu-id="755bc-150">This example shows disconnected data.</span><span class="sxs-lookup"><span data-stu-id="755bc-150">This example shows disconnected data.</span></span>

<span data-ttu-id="755bc-151">The table on the right, though, is full and complete - an example of connected data.</span><span class="sxs-lookup"><span data-stu-id="755bc-151">The table on the right, though, is full and complete - an example of connected data.</span></span>

## <a name="is-your-data-accurate"></a><span data-ttu-id="755bc-152">Is your data accurate?</span><span class="sxs-lookup"><span data-stu-id="755bc-152">Is your data accurate?</span></span>
<span data-ttu-id="755bc-153">The next ingredient is accuracy.</span><span class="sxs-lookup"><span data-stu-id="755bc-153">The next ingredient is accuracy.</span></span> <span data-ttu-id="755bc-154">Here are four targets to hit.</span><span class="sxs-lookup"><span data-stu-id="755bc-154">Here are four targets to hit.</span></span>

![Accurate data vs. inaccurate data - data criteria](./media/data-science-for-beginners-is-your-data-ready-for-data-science/inaccurate-vs-accurate-data.png)

<span data-ttu-id="755bc-156">Look at the target in the upper right.</span><span class="sxs-lookup"><span data-stu-id="755bc-156">Look at the target in the upper right.</span></span> <span data-ttu-id="755bc-157">There is a tight grouping right around the bulls eye.</span><span class="sxs-lookup"><span data-stu-id="755bc-157">There is a tight grouping right around the bulls eye.</span></span> <span data-ttu-id="755bc-158">That, of course, is accurate.</span><span class="sxs-lookup"><span data-stu-id="755bc-158">That, of course, is accurate.</span></span> <span data-ttu-id="755bc-159">Oddly, in the language of data science, performance on the target right below it is also considered accurate.</span><span class="sxs-lookup"><span data-stu-id="755bc-159">Oddly, in the language of data science, performance on the target right below it is also considered accurate.</span></span>

<span data-ttu-id="755bc-160">If you mapped out the center of these arrows, you'd see that it's very close to the bulls eye.</span><span class="sxs-lookup"><span data-stu-id="755bc-160">If you mapped out the center of these arrows, you'd see that it's very close to the bulls eye.</span></span> <span data-ttu-id="755bc-161">The arrows are spread out all around the target, so they're considered imprecise, but they're centered around the bulls eye, so they're considered accurate.</span><span class="sxs-lookup"><span data-stu-id="755bc-161">The arrows are spread out all around the target, so they're considered imprecise, but they're centered around the bulls eye, so they're considered accurate.</span></span>

<span data-ttu-id="755bc-162">Now look at the upper-left target.</span><span class="sxs-lookup"><span data-stu-id="755bc-162">Now look at the upper-left target.</span></span> <span data-ttu-id="755bc-163">Here the arrows hit very close together, a tight grouping.</span><span class="sxs-lookup"><span data-stu-id="755bc-163">Here the arrows hit very close together, a tight grouping.</span></span> <span data-ttu-id="755bc-164">They're precise, but they're inaccurate because the center is way off the bulls eye.</span><span class="sxs-lookup"><span data-stu-id="755bc-164">They're precise, but they're inaccurate because the center is way off the bulls eye.</span></span> <span data-ttu-id="755bc-165">The arrows in the bottom-left target are both inaccurate and imprecise.</span><span class="sxs-lookup"><span data-stu-id="755bc-165">The arrows in the bottom-left target are both inaccurate and imprecise.</span></span> <span data-ttu-id="755bc-166">This archer needs more practice.</span><span class="sxs-lookup"><span data-stu-id="755bc-166">This archer needs more practice.</span></span>

## <a name="do-you-have-enough-data-to-work-with"></a><span data-ttu-id="755bc-167">Do you have enough data to work with?</span><span class="sxs-lookup"><span data-stu-id="755bc-167">Do you have enough data to work with?</span></span>
<span data-ttu-id="755bc-168">Finally, ingredient #4 is sufficient data.</span><span class="sxs-lookup"><span data-stu-id="755bc-168">Finally, ingredient #4 is sufficient data.</span></span>

![Do you have enough data for analysis?](./media/data-science-for-beginners-is-your-data-ready-for-data-science/barely-enough-data.png)

<span data-ttu-id="755bc-171">Think of each data point in your table as being a brush stroke in a painting.</span><span class="sxs-lookup"><span data-stu-id="755bc-171">Think of each data point in your table as being a brush stroke in a painting.</span></span> <span data-ttu-id="755bc-172">If you have only a few of them, the painting can be fuzzy - it's hard to tell what it is.</span><span class="sxs-lookup"><span data-stu-id="755bc-172">If you have only a few of them, the painting can be fuzzy - it's hard to tell what it is.</span></span>

<span data-ttu-id="755bc-173">If you add some more brush strokes, then your painting starts to get a little sharper.</span><span class="sxs-lookup"><span data-stu-id="755bc-173">If you add some more brush strokes, then your painting starts to get a little sharper.</span></span>

<span data-ttu-id="755bc-174">When you have barely enough strokes, you only see enough to make some broad decisions.</span><span class="sxs-lookup"><span data-stu-id="755bc-174">When you have barely enough strokes, you only see enough to make some broad decisions.</span></span> <span data-ttu-id="755bc-175">Is it somewhere I might want to visit?</span><span class="sxs-lookup"><span data-stu-id="755bc-175">Is it somewhere I might want to visit?</span></span> <span data-ttu-id="755bc-176">It looks bright, that looks like clean water – yes, that’s where I’m going on vacation.</span><span class="sxs-lookup"><span data-stu-id="755bc-176">It looks bright, that looks like clean water – yes, that’s where I’m going on vacation.</span></span>

<span data-ttu-id="755bc-177">As you add more data, the picture becomes clearer and you can make more detailed decisions.</span><span class="sxs-lookup"><span data-stu-id="755bc-177">As you add more data, the picture becomes clearer and you can make more detailed decisions.</span></span> <span data-ttu-id="755bc-178">Now you can look at the three hotels on the left bank.</span><span class="sxs-lookup"><span data-stu-id="755bc-178">Now you can look at the three hotels on the left bank.</span></span> <span data-ttu-id="755bc-179">You can notice the architectural features of the one in the foreground.</span><span class="sxs-lookup"><span data-stu-id="755bc-179">You can notice the architectural features of the one in the foreground.</span></span> <span data-ttu-id="755bc-180">You might even choose to stay on the third floor because of the view.</span><span class="sxs-lookup"><span data-stu-id="755bc-180">You might even choose to stay on the third floor because of the view.</span></span>

<span data-ttu-id="755bc-181">With data that's relevant, connected, accurate, and enough, you have all the ingredients needed to do some high-quality data science.</span><span class="sxs-lookup"><span data-stu-id="755bc-181">With data that's relevant, connected, accurate, and enough, you have all the ingredients needed to do some high-quality data science.</span></span>

<span data-ttu-id="755bc-182">Be sure to check out the other four videos in *Data Science for Beginners* from Microsoft Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="755bc-182">Be sure to check out the other four videos in *Data Science for Beginners* from Microsoft Azure Machine Learning.</span></span>

## <a name="next-steps"></a><span data-ttu-id="755bc-183">Next steps</span><span class="sxs-lookup"><span data-stu-id="755bc-183">Next steps</span></span>
* [<span data-ttu-id="755bc-184">Try a first data science experiment with Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="755bc-184">Try a first data science experiment with Machine Learning Studio</span></span>](create-experiment.md)
* [<span data-ttu-id="755bc-185">Get an introduction to Machine Learning on Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="755bc-185">Get an introduction to Machine Learning on Microsoft Azure</span></span>](what-is-machine-learning.md)
