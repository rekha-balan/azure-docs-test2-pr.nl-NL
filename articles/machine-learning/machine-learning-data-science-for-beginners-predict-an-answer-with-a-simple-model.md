---
title: Predict an answer with a simple regression model - Azure | Microsoft Docs
description: How to create a simple regression model to predict a price in Data Science for Beginners video 4. Includes a linear regression with target data.
keywords: create a model,simple model,price prediction,simple regression model
services: machine-learning
documentationcenter: na
author: cjgronlund
manager: jhubbard
editor: cjgronlund
ms.assetid: a28f1fab-e2d8-4663-aa7d-ca3530c8b525
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/09/2017
ms.author: cgronlun;garye
ms.openlocfilehash: 641582663b36d5f7e4def099c31813d9a9b4c6c3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551728"
---
# <a name="predict-an-answer-with-a-simple-model"></a><span data-ttu-id="51af5-105">Predict an answer with a simple model</span><span class="sxs-lookup"><span data-stu-id="51af5-105">Predict an answer with a simple model</span></span>
## <a name="video-4-data-science-for-beginners-series"></a><span data-ttu-id="51af5-106">Video 4: Data Science for Beginners series</span><span class="sxs-lookup"><span data-stu-id="51af5-106">Video 4: Data Science for Beginners series</span></span>
<span data-ttu-id="51af5-107">Learn how to create a simple regression model to predict the price of a diamond in Data Science for Beginners video 4.</span><span class="sxs-lookup"><span data-stu-id="51af5-107">Learn how to create a simple regression model to predict the price of a diamond in Data Science for Beginners video 4.</span></span> <span data-ttu-id="51af5-108">We'll draw a regression model with target data.</span><span class="sxs-lookup"><span data-stu-id="51af5-108">We'll draw a regression model with target data.</span></span>

<span data-ttu-id="51af5-109">To get the most out of the series, watch them all.</span><span class="sxs-lookup"><span data-stu-id="51af5-109">To get the most out of the series, watch them all.</span></span> [<span data-ttu-id="51af5-110">Go to the list of videos</span><span class="sxs-lookup"><span data-stu-id="51af5-110">Go to the list of videos</span></span>](#other-videos-in-this-series)

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/data-science-for-beginners-series-predict-an-answer-with-a-simple-model/player]
>
>

## <a name="other-videos-in-this-series"></a><span data-ttu-id="51af5-111">Other videos in this series</span><span class="sxs-lookup"><span data-stu-id="51af5-111">Other videos in this series</span></span>
<span data-ttu-id="51af5-112">*Data Science for Beginners* is a quick introduction to data science in five short videos.</span><span class="sxs-lookup"><span data-stu-id="51af5-112">*Data Science for Beginners* is a quick introduction to data science in five short videos.</span></span>

* <span data-ttu-id="51af5-113">Video 1: [The 5 questions data science answers](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) *(5 min 14 sec)*</span><span class="sxs-lookup"><span data-stu-id="51af5-113">Video 1: [The 5 questions data science answers](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) *(5 min 14 sec)*</span></span>
* <span data-ttu-id="51af5-114">Video 2: [Is your data ready for data science?](machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science.md)</span><span class="sxs-lookup"><span data-stu-id="51af5-114">Video 2: [Is your data ready for data science?](machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science.md)</span></span> <span data-ttu-id="51af5-115">*(4 min 56 sec)*</span><span class="sxs-lookup"><span data-stu-id="51af5-115">*(4 min 56 sec)*</span></span>
* <span data-ttu-id="51af5-116">Video 3: [Ask a question you can answer with data](machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data.md) *(4 min 17 sec)*</span><span class="sxs-lookup"><span data-stu-id="51af5-116">Video 3: [Ask a question you can answer with data](machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data.md) *(4 min 17 sec)*</span></span>
* <span data-ttu-id="51af5-117">Video 4: Predict an answer with a simple model</span><span class="sxs-lookup"><span data-stu-id="51af5-117">Video 4: Predict an answer with a simple model</span></span>
* <span data-ttu-id="51af5-118">Video 5: [Copy other people's work to do data science](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) *(3 min 18 sec)*</span><span class="sxs-lookup"><span data-stu-id="51af5-118">Video 5: [Copy other people's work to do data science](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) *(3 min 18 sec)*</span></span>

## <a name="transcript-predict-an-answer-with-a-simple-model"></a><span data-ttu-id="51af5-119">Transcript: Predict an answer with a simple model</span><span class="sxs-lookup"><span data-stu-id="51af5-119">Transcript: Predict an answer with a simple model</span></span>
<span data-ttu-id="51af5-120">Welcome to the fourth video in the "Data Science for Beginners" series.</span><span class="sxs-lookup"><span data-stu-id="51af5-120">Welcome to the fourth video in the "Data Science for Beginners" series.</span></span> <span data-ttu-id="51af5-121">In this one, we'll build a simple model and make a prediction.</span><span class="sxs-lookup"><span data-stu-id="51af5-121">In this one, we'll build a simple model and make a prediction.</span></span>

<span data-ttu-id="51af5-122">A *model* is a simplified story about our data.</span><span class="sxs-lookup"><span data-stu-id="51af5-122">A *model* is a simplified story about our data.</span></span> <span data-ttu-id="51af5-123">I'll show you what I mean.</span><span class="sxs-lookup"><span data-stu-id="51af5-123">I'll show you what I mean.</span></span>

## <a name="collect-relevant-accurate-connected-enough-data"></a><span data-ttu-id="51af5-124">Collect relevant, accurate, connected, enough data</span><span class="sxs-lookup"><span data-stu-id="51af5-124">Collect relevant, accurate, connected, enough data</span></span>
<span data-ttu-id="51af5-125">Say I want to shop for a diamond.</span><span class="sxs-lookup"><span data-stu-id="51af5-125">Say I want to shop for a diamond.</span></span> <span data-ttu-id="51af5-126">I have a ring that belonged to my grandmother with a setting for a 1.35 carat diamond, and I want to get an idea of how much it will cost.</span><span class="sxs-lookup"><span data-stu-id="51af5-126">I have a ring that belonged to my grandmother with a setting for a 1.35 carat diamond, and I want to get an idea of how much it will cost.</span></span> <span data-ttu-id="51af5-127">I take a notepad and pen into the jewelry store, and I write down the price of all of the diamonds in the case and how much they weigh in carats.</span><span class="sxs-lookup"><span data-stu-id="51af5-127">I take a notepad and pen into the jewelry store, and I write down the price of all of the diamonds in the case and how much they weigh in carats.</span></span> <span data-ttu-id="51af5-128">Starting with the first diamond - it's 1.01 carats and $7,366.</span><span class="sxs-lookup"><span data-stu-id="51af5-128">Starting with the first diamond - it's 1.01 carats and $7,366.</span></span>

<span data-ttu-id="51af5-129">Now I go through and do this for all the other diamonds in the store.</span><span class="sxs-lookup"><span data-stu-id="51af5-129">Now I go through and do this for all the other diamonds in the store.</span></span>

![Columns of diamond data](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/diamond-data.png)

<span data-ttu-id="51af5-131">Notice that our list has two columns.</span><span class="sxs-lookup"><span data-stu-id="51af5-131">Notice that our list has two columns.</span></span> <span data-ttu-id="51af5-132">Each column has a different attribute - weight in carats and price - and each row is a single data point that represents a single diamond.</span><span class="sxs-lookup"><span data-stu-id="51af5-132">Each column has a different attribute - weight in carats and price - and each row is a single data point that represents a single diamond.</span></span>

<span data-ttu-id="51af5-133">We've actually created a small data set here - a table.</span><span class="sxs-lookup"><span data-stu-id="51af5-133">We've actually created a small data set here - a table.</span></span> <span data-ttu-id="51af5-134">Notice that it meets our criteria for quality:</span><span class="sxs-lookup"><span data-stu-id="51af5-134">Notice that it meets our criteria for quality:</span></span>

* <span data-ttu-id="51af5-135">The data is **relevant** - weight is definitely related to price</span><span class="sxs-lookup"><span data-stu-id="51af5-135">The data is **relevant** - weight is definitely related to price</span></span>
* <span data-ttu-id="51af5-136">It's **accurate** - we double-checked the prices that we write down</span><span class="sxs-lookup"><span data-stu-id="51af5-136">It's **accurate** - we double-checked the prices that we write down</span></span>
* <span data-ttu-id="51af5-137">It's **connected** - there are no blank spaces in either of these columns</span><span class="sxs-lookup"><span data-stu-id="51af5-137">It's **connected** - there are no blank spaces in either of these columns</span></span>
* <span data-ttu-id="51af5-138">And, as we'll see, it's **enough** data to answer our question</span><span class="sxs-lookup"><span data-stu-id="51af5-138">And, as we'll see, it's **enough** data to answer our question</span></span>

## <a name="ask-a-sharp-question"></a><span data-ttu-id="51af5-139">Ask a sharp question</span><span class="sxs-lookup"><span data-stu-id="51af5-139">Ask a sharp question</span></span>
<span data-ttu-id="51af5-140">Now we'll pose our question in a sharp way: "How much will it cost to buy a 1.35 carat diamond?"</span><span class="sxs-lookup"><span data-stu-id="51af5-140">Now we'll pose our question in a sharp way: "How much will it cost to buy a 1.35 carat diamond?"</span></span>

<span data-ttu-id="51af5-141">Our list doesn't have a 1.35 carat diamond in it, so we'll have to use the rest of our data to get an answer to the question.</span><span class="sxs-lookup"><span data-stu-id="51af5-141">Our list doesn't have a 1.35 carat diamond in it, so we'll have to use the rest of our data to get an answer to the question.</span></span>

## <a name="plot-the-existing-data"></a><span data-ttu-id="51af5-142">Plot the existing data</span><span class="sxs-lookup"><span data-stu-id="51af5-142">Plot the existing data</span></span>
<span data-ttu-id="51af5-143">The first thing we'll do is draw a horizontal number line, called an axis, to chart the weights.</span><span class="sxs-lookup"><span data-stu-id="51af5-143">The first thing we'll do is draw a horizontal number line, called an axis, to chart the weights.</span></span> <span data-ttu-id="51af5-144">The range of the weights is 0 to 2, so we'll draw a line that covers that range and put ticks for each half carat.</span><span class="sxs-lookup"><span data-stu-id="51af5-144">The range of the weights is 0 to 2, so we'll draw a line that covers that range and put ticks for each half carat.</span></span>

<span data-ttu-id="51af5-145">Next we'll draw a vertical axis to record the price and connect it to the horizontal weight axis.</span><span class="sxs-lookup"><span data-stu-id="51af5-145">Next we'll draw a vertical axis to record the price and connect it to the horizontal weight axis.</span></span> <span data-ttu-id="51af5-146">This will be in units of dollars.</span><span class="sxs-lookup"><span data-stu-id="51af5-146">This will be in units of dollars.</span></span> <span data-ttu-id="51af5-147">Now we have a set of coordinate axes.</span><span class="sxs-lookup"><span data-stu-id="51af5-147">Now we have a set of coordinate axes.</span></span>

![Weight and price axes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/weight-and-price-axes.png)

<span data-ttu-id="51af5-149">We're going to take this data now and turn it into a *scatter plot*.</span><span class="sxs-lookup"><span data-stu-id="51af5-149">We're going to take this data now and turn it into a *scatter plot*.</span></span> <span data-ttu-id="51af5-150">This is a great way to visualize numerical data sets.</span><span class="sxs-lookup"><span data-stu-id="51af5-150">This is a great way to visualize numerical data sets.</span></span>

<span data-ttu-id="51af5-151">For the first data point, we eyeball a vertical line at 1.01 carats.</span><span class="sxs-lookup"><span data-stu-id="51af5-151">For the first data point, we eyeball a vertical line at 1.01 carats.</span></span> <span data-ttu-id="51af5-152">Then, we eyeball a horizontal line at $7,366.</span><span class="sxs-lookup"><span data-stu-id="51af5-152">Then, we eyeball a horizontal line at $7,366.</span></span> <span data-ttu-id="51af5-153">Where they meet, we draw a dot.</span><span class="sxs-lookup"><span data-stu-id="51af5-153">Where they meet, we draw a dot.</span></span> <span data-ttu-id="51af5-154">This represents our first diamond.</span><span class="sxs-lookup"><span data-stu-id="51af5-154">This represents our first diamond.</span></span>

<span data-ttu-id="51af5-155">Now we go through each diamond on this list and do the same thing.</span><span class="sxs-lookup"><span data-stu-id="51af5-155">Now we go through each diamond on this list and do the same thing.</span></span> <span data-ttu-id="51af5-156">When we're through, this is what we get: a bunch of dots, one for each diamond.</span><span class="sxs-lookup"><span data-stu-id="51af5-156">When we're through, this is what we get: a bunch of dots, one for each diamond.</span></span>

![Scatter plot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/scatter-plot.png)

## <a name="draw-the-model-through-the-data-points"></a><span data-ttu-id="51af5-158">Draw the model through the data points</span><span class="sxs-lookup"><span data-stu-id="51af5-158">Draw the model through the data points</span></span>
<span data-ttu-id="51af5-159">Now if you look at the dots and squint, the collection looks like a fat, fuzzy line.</span><span class="sxs-lookup"><span data-stu-id="51af5-159">Now if you look at the dots and squint, the collection looks like a fat, fuzzy line.</span></span> <span data-ttu-id="51af5-160">We can take our marker and draw a straight line through it.</span><span class="sxs-lookup"><span data-stu-id="51af5-160">We can take our marker and draw a straight line through it.</span></span>

<span data-ttu-id="51af5-161">By drawing a line, we created a *model*.</span><span class="sxs-lookup"><span data-stu-id="51af5-161">By drawing a line, we created a *model*.</span></span> <span data-ttu-id="51af5-162">Think of this as taking the real world and making a simplistic cartoon version of it.</span><span class="sxs-lookup"><span data-stu-id="51af5-162">Think of this as taking the real world and making a simplistic cartoon version of it.</span></span> <span data-ttu-id="51af5-163">Now the cartoon is wrong - the line doesn't go through all the data points.</span><span class="sxs-lookup"><span data-stu-id="51af5-163">Now the cartoon is wrong - the line doesn't go through all the data points.</span></span> <span data-ttu-id="51af5-164">But, it's a useful simplification.</span><span class="sxs-lookup"><span data-stu-id="51af5-164">But, it's a useful simplification.</span></span>

![Linear regression line](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/linear-regression-line.png)

<span data-ttu-id="51af5-166">The fact that all the dots don't go exactly through the line is OK.</span><span class="sxs-lookup"><span data-stu-id="51af5-166">The fact that all the dots don't go exactly through the line is OK.</span></span> <span data-ttu-id="51af5-167">Data scientists explain this by saying that there's the model - that's the line - and then each dot has some *noise* or *variance* associated with it.</span><span class="sxs-lookup"><span data-stu-id="51af5-167">Data scientists explain this by saying that there's the model - that's the line - and then each dot has some *noise* or *variance* associated with it.</span></span> <span data-ttu-id="51af5-168">There's the underlying perfect relationship, and then there's the gritty, real world that adds noise and uncertainty.</span><span class="sxs-lookup"><span data-stu-id="51af5-168">There's the underlying perfect relationship, and then there's the gritty, real world that adds noise and uncertainty.</span></span>

<span data-ttu-id="51af5-169">Because we're trying to answer the question *How much?* this is called a *regression*.</span><span class="sxs-lookup"><span data-stu-id="51af5-169">Because we're trying to answer the question *How much?* this is called a *regression*.</span></span> <span data-ttu-id="51af5-170">And because we're using a straight line, it's a *linear regression*.</span><span class="sxs-lookup"><span data-stu-id="51af5-170">And because we're using a straight line, it's a *linear regression*.</span></span>

## <a name="use-the-model-to-find-the-answer"></a><span data-ttu-id="51af5-171">Use the model to find the answer</span><span class="sxs-lookup"><span data-stu-id="51af5-171">Use the model to find the answer</span></span>
<span data-ttu-id="51af5-172">Now we have a model and we ask it our question: How much will a 1.35 carat diamond cost?</span><span class="sxs-lookup"><span data-stu-id="51af5-172">Now we have a model and we ask it our question: How much will a 1.35 carat diamond cost?</span></span>

<span data-ttu-id="51af5-173">To answer our question, we eyeball 1.35 carats and draw a vertical line.</span><span class="sxs-lookup"><span data-stu-id="51af5-173">To answer our question, we eyeball 1.35 carats and draw a vertical line.</span></span> <span data-ttu-id="51af5-174">Where it crosses the model line, we eyeball a horizontal line to the dollar axis.</span><span class="sxs-lookup"><span data-stu-id="51af5-174">Where it crosses the model line, we eyeball a horizontal line to the dollar axis.</span></span> <span data-ttu-id="51af5-175">It hits right at 10,000.</span><span class="sxs-lookup"><span data-stu-id="51af5-175">It hits right at 10,000.</span></span> <span data-ttu-id="51af5-176">Boom!</span><span class="sxs-lookup"><span data-stu-id="51af5-176">Boom!</span></span> <span data-ttu-id="51af5-177">That's the answer: A 1.35 carat diamond costs about $10,000.</span><span class="sxs-lookup"><span data-stu-id="51af5-177">That's the answer: A 1.35 carat diamond costs about $10,000.</span></span>

![Find the answer on the model](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/find-the-answer.png)

## <a name="create-a-confidence-interval"></a><span data-ttu-id="51af5-179">Create a confidence interval</span><span class="sxs-lookup"><span data-stu-id="51af5-179">Create a confidence interval</span></span>
<span data-ttu-id="51af5-180">It's natural to wonder how precise this prediction is.</span><span class="sxs-lookup"><span data-stu-id="51af5-180">It's natural to wonder how precise this prediction is.</span></span> <span data-ttu-id="51af5-181">It's useful to know whether the 1.35 carat diamond will be very close to $10,000, or a lot higher or lower.</span><span class="sxs-lookup"><span data-stu-id="51af5-181">It's useful to know whether the 1.35 carat diamond will be very close to $10,000, or a lot higher or lower.</span></span> <span data-ttu-id="51af5-182">To figure this out, let's draw an envelope around the regression line that includes most of the dots.</span><span class="sxs-lookup"><span data-stu-id="51af5-182">To figure this out, let's draw an envelope around the regression line that includes most of the dots.</span></span> <span data-ttu-id="51af5-183">This envelope is called our *confidence interval*: We're pretty confident that prices fall within this envelope, because in the past most of them have.</span><span class="sxs-lookup"><span data-stu-id="51af5-183">This envelope is called our *confidence interval*: We're pretty confident that prices fall within this envelope, because in the past most of them have.</span></span> <span data-ttu-id="51af5-184">We can draw two more horizontal lines from where the 1.35 carat line crosses the top and the bottom of that envelope.</span><span class="sxs-lookup"><span data-stu-id="51af5-184">We can draw two more horizontal lines from where the 1.35 carat line crosses the top and the bottom of that envelope.</span></span>

![Confidence interval](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/confidence-interval.png)

<span data-ttu-id="51af5-186">Now we can say something about our confidence interval:  We can say confidently that the price of a 1.35 carat diamond is about $10,000 - but it might be as low as $8,000 and it might be as high as $12,000.</span><span class="sxs-lookup"><span data-stu-id="51af5-186">Now we can say something about our confidence interval:  We can say confidently that the price of a 1.35 carat diamond is about $10,000 - but it might be as low as $8,000 and it might be as high as $12,000.</span></span>

## <a name="were-done-with-no-math-or-computers"></a><span data-ttu-id="51af5-187">We're done, with no math or computers</span><span class="sxs-lookup"><span data-stu-id="51af5-187">We're done, with no math or computers</span></span>
<span data-ttu-id="51af5-188">We did what data scientists get paid to do, and we did it just by drawing:</span><span class="sxs-lookup"><span data-stu-id="51af5-188">We did what data scientists get paid to do, and we did it just by drawing:</span></span>

* <span data-ttu-id="51af5-189">We asked a question that we could answer with data</span><span class="sxs-lookup"><span data-stu-id="51af5-189">We asked a question that we could answer with data</span></span>
* <span data-ttu-id="51af5-190">We built a *model* using *linear regression*</span><span class="sxs-lookup"><span data-stu-id="51af5-190">We built a *model* using *linear regression*</span></span>
* <span data-ttu-id="51af5-191">We made a *prediction*, complete with a *confidence interval*</span><span class="sxs-lookup"><span data-stu-id="51af5-191">We made a *prediction*, complete with a *confidence interval*</span></span>

<span data-ttu-id="51af5-192">And we didn't use math or computers to do it.</span><span class="sxs-lookup"><span data-stu-id="51af5-192">And we didn't use math or computers to do it.</span></span>

<span data-ttu-id="51af5-193">Now if we'd had more information, like...</span><span class="sxs-lookup"><span data-stu-id="51af5-193">Now if we'd had more information, like...</span></span>

* <span data-ttu-id="51af5-194">the cut of the diamond</span><span class="sxs-lookup"><span data-stu-id="51af5-194">the cut of the diamond</span></span>
* <span data-ttu-id="51af5-195">color variations (how close the diamond is to being white)</span><span class="sxs-lookup"><span data-stu-id="51af5-195">color variations (how close the diamond is to being white)</span></span>
* <span data-ttu-id="51af5-196">the number of inclusions in the diamond</span><span class="sxs-lookup"><span data-stu-id="51af5-196">the number of inclusions in the diamond</span></span>

<span data-ttu-id="51af5-197">...then we would have had more columns.</span><span class="sxs-lookup"><span data-stu-id="51af5-197">...then we would have had more columns.</span></span> <span data-ttu-id="51af5-198">In that case, math becomes helpful.</span><span class="sxs-lookup"><span data-stu-id="51af5-198">In that case, math becomes helpful.</span></span> <span data-ttu-id="51af5-199">If you have more than two columns, it's hard to draw dots on paper.</span><span class="sxs-lookup"><span data-stu-id="51af5-199">If you have more than two columns, it's hard to draw dots on paper.</span></span> <span data-ttu-id="51af5-200">The math lets you fit that line or that plane to your data very nicely.</span><span class="sxs-lookup"><span data-stu-id="51af5-200">The math lets you fit that line or that plane to your data very nicely.</span></span>

<span data-ttu-id="51af5-201">Also, if instead of just a handful of diamonds, we had two thousand or two million, then you can do that work much faster with a computer.</span><span class="sxs-lookup"><span data-stu-id="51af5-201">Also, if instead of just a handful of diamonds, we had two thousand or two million, then you can do that work much faster with a computer.</span></span>

<span data-ttu-id="51af5-202">Today, we've talked about how to do linear regression, and we made a prediction using data.</span><span class="sxs-lookup"><span data-stu-id="51af5-202">Today, we've talked about how to do linear regression, and we made a prediction using data.</span></span>

<span data-ttu-id="51af5-203">Be sure to check out the other videos in "Data Science for Beginners" from Microsoft Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="51af5-203">Be sure to check out the other videos in "Data Science for Beginners" from Microsoft Azure Machine Learning.</span></span>

## <a name="next-steps"></a><span data-ttu-id="51af5-204">Next steps</span><span class="sxs-lookup"><span data-stu-id="51af5-204">Next steps</span></span>
* [<span data-ttu-id="51af5-205">Try a first data science experiment with Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="51af5-205">Try a first data science experiment with Machine Learning Studio</span></span>](machine-learning-create-experiment.md)
* [<span data-ttu-id="51af5-206">Get an introduction to Machine Learning on Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="51af5-206">Get an introduction to Machine Learning on Microsoft Azure</span></span>](machine-learning-what-is-machine-learning.md)






