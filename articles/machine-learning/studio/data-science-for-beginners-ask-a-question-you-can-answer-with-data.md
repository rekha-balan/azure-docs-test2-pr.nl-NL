---
title: Ask a question data can answer - data science problems - Azure Machine Learning | Microsoft Docs
description: Learn how to formulate a sharp data science question in Data Science for Beginners video 3. Includes a comparison of classification and regression questions.
keywords: data science problems,data science questions,formulate questions,regression questions,classification questions,sharp question
services: machine-learning
documentationcenter: na
author: heatherbshapiro
ms.author: hshapiro
manager: hjerez
editor: cjgronlund
ms.assetid: 5b9501e3-9964-417a-8ffc-8913103da77b
ms.service: machine-learning
ms.component: studio
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/03/2018
ms.openlocfilehash: 2078f7e84522a40cf6fcf6dff860d24307084467
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966441"
---
# <a name="ask-a-question-you-can-answer-with-data"></a><span data-ttu-id="8f131-105">Ask a question you can answer with data</span><span class="sxs-lookup"><span data-stu-id="8f131-105">Ask a question you can answer with data</span></span>
## <a name="video-3-data-science-for-beginners-series"></a><span data-ttu-id="8f131-106">Video 3: Data Science for Beginners series</span><span class="sxs-lookup"><span data-stu-id="8f131-106">Video 3: Data Science for Beginners series</span></span>
<span data-ttu-id="8f131-107">Learn how to formulate a data science problem into a question in Data Science for Beginners video 3.</span><span class="sxs-lookup"><span data-stu-id="8f131-107">Learn how to formulate a data science problem into a question in Data Science for Beginners video 3.</span></span> <span data-ttu-id="8f131-108">This video includes a comparison of questions for classification and regression algorithms.</span><span class="sxs-lookup"><span data-stu-id="8f131-108">This video includes a comparison of questions for classification and regression algorithms.</span></span>

<span data-ttu-id="8f131-109">To get the most out of the series, watch them all.</span><span class="sxs-lookup"><span data-stu-id="8f131-109">To get the most out of the series, watch them all.</span></span> [<span data-ttu-id="8f131-110">Go to the list of videos</span><span class="sxs-lookup"><span data-stu-id="8f131-110">Go to the list of videos</span></span>](#other-videos-in-this-series)
<br>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Data-science-for-beginners-Ask-a-question-you-can-answer-with-data/player]
>
>

## <a name="other-videos-in-this-series"></a><span data-ttu-id="8f131-111">Other videos in this series</span><span class="sxs-lookup"><span data-stu-id="8f131-111">Other videos in this series</span></span>
<span data-ttu-id="8f131-112">*Data Science for Beginners* is a quick introduction to data science in five short videos.</span><span class="sxs-lookup"><span data-stu-id="8f131-112">*Data Science for Beginners* is a quick introduction to data science in five short videos.</span></span>

* <span data-ttu-id="8f131-113">Video 1: [The 5 questions data science answers](data-science-for-beginners-the-5-questions-data-science-answers.md) *(5 min 14 sec)*</span><span class="sxs-lookup"><span data-stu-id="8f131-113">Video 1: [The 5 questions data science answers](data-science-for-beginners-the-5-questions-data-science-answers.md) *(5 min 14 sec)*</span></span>
* <span data-ttu-id="8f131-114">Video 2: [Is your data ready for data science?](data-science-for-beginners-is-your-data-ready-for-data-science.md)</span><span class="sxs-lookup"><span data-stu-id="8f131-114">Video 2: [Is your data ready for data science?](data-science-for-beginners-is-your-data-ready-for-data-science.md)</span></span> <span data-ttu-id="8f131-115">*(4 min 56 sec)*</span><span class="sxs-lookup"><span data-stu-id="8f131-115">*(4 min 56 sec)*</span></span>
* <span data-ttu-id="8f131-116">Video 3: Ask a question you can answer with data</span><span class="sxs-lookup"><span data-stu-id="8f131-116">Video 3: Ask a question you can answer with data</span></span>
* <span data-ttu-id="8f131-117">Video 4: [Predict an answer with a simple model](data-science-for-beginners-predict-an-answer-with-a-simple-model.md) *(7 min 42 sec)*</span><span class="sxs-lookup"><span data-stu-id="8f131-117">Video 4: [Predict an answer with a simple model](data-science-for-beginners-predict-an-answer-with-a-simple-model.md) *(7 min 42 sec)*</span></span>
* <span data-ttu-id="8f131-118">Video 5: [Copy other people's work to do data science](data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) *(3 min 18 sec)*</span><span class="sxs-lookup"><span data-stu-id="8f131-118">Video 5: [Copy other people's work to do data science](data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) *(3 min 18 sec)*</span></span>

## <a name="transcript-ask-a-question-you-can-answer-with-data"></a><span data-ttu-id="8f131-119">Transcript: Ask a question you can answer with data</span><span class="sxs-lookup"><span data-stu-id="8f131-119">Transcript: Ask a question you can answer with data</span></span>
<span data-ttu-id="8f131-120">Welcome to the third video in the series "Data Science for Beginners."</span><span class="sxs-lookup"><span data-stu-id="8f131-120">Welcome to the third video in the series "Data Science for Beginners."</span></span>  

<span data-ttu-id="8f131-121">In this one, you'll get some tips for formulating a question you can answer with data.</span><span class="sxs-lookup"><span data-stu-id="8f131-121">In this one, you'll get some tips for formulating a question you can answer with data.</span></span>

<span data-ttu-id="8f131-122">You might get more out of this video, if you first watch the two earlier videos in this series: "The 5 questions data science can answer" and "Is your data is ready for data science?"</span><span class="sxs-lookup"><span data-stu-id="8f131-122">You might get more out of this video, if you first watch the two earlier videos in this series: "The 5 questions data science can answer" and "Is your data is ready for data science?"</span></span>

## <a name="ask-a-sharp-question"></a><span data-ttu-id="8f131-123">Ask a sharp question</span><span class="sxs-lookup"><span data-stu-id="8f131-123">Ask a sharp question</span></span>
<span data-ttu-id="8f131-124">We've talked about how data science is the process of using names (also called categories or labels) and numbers to predict an answer to a question.</span><span class="sxs-lookup"><span data-stu-id="8f131-124">We've talked about how data science is the process of using names (also called categories or labels) and numbers to predict an answer to a question.</span></span> <span data-ttu-id="8f131-125">But it can't be just any question; it has to be a *sharp question.*</span><span class="sxs-lookup"><span data-stu-id="8f131-125">But it can't be just any question; it has to be a *sharp question.*</span></span>

<span data-ttu-id="8f131-126">A vague question doesn't have to be answered with a name or a number.</span><span class="sxs-lookup"><span data-stu-id="8f131-126">A vague question doesn't have to be answered with a name or a number.</span></span> <span data-ttu-id="8f131-127">A sharp question must.</span><span class="sxs-lookup"><span data-stu-id="8f131-127">A sharp question must.</span></span>

<span data-ttu-id="8f131-128">Imagine you found a magic lamp with a genie who will truthfully answer any question you ask.</span><span class="sxs-lookup"><span data-stu-id="8f131-128">Imagine you found a magic lamp with a genie who will truthfully answer any question you ask.</span></span> <span data-ttu-id="8f131-129">But it's a mischievous genie, and he'll try to make his answer as vague and confusing as he can get away with.</span><span class="sxs-lookup"><span data-stu-id="8f131-129">But it's a mischievous genie, and he'll try to make his answer as vague and confusing as he can get away with.</span></span> <span data-ttu-id="8f131-130">You want to pin him down with a question so airtight that he can't help but tell you what you want to know.</span><span class="sxs-lookup"><span data-stu-id="8f131-130">You want to pin him down with a question so airtight that he can't help but tell you what you want to know.</span></span>

<span data-ttu-id="8f131-131">If you were to ask a vague question, like "What's going to happen with my stock?", the genie might answer, "The price will change".</span><span class="sxs-lookup"><span data-stu-id="8f131-131">If you were to ask a vague question, like "What's going to happen with my stock?", the genie might answer, "The price will change".</span></span> <span data-ttu-id="8f131-132">That's a truthful answer, but it's not very helpful.</span><span class="sxs-lookup"><span data-stu-id="8f131-132">That's a truthful answer, but it's not very helpful.</span></span>

<span data-ttu-id="8f131-133">But if you were to ask a sharp question, like "What will my stock's sale price be next week?", the genie can't help but give you a specific answer and predict a sale price.</span><span class="sxs-lookup"><span data-stu-id="8f131-133">But if you were to ask a sharp question, like "What will my stock's sale price be next week?", the genie can't help but give you a specific answer and predict a sale price.</span></span>

## <a name="examples-of-your-answer-target-data"></a><span data-ttu-id="8f131-134">Examples of your answer: Target data</span><span class="sxs-lookup"><span data-stu-id="8f131-134">Examples of your answer: Target data</span></span>
<span data-ttu-id="8f131-135">Once you formulate your question, check to see whether you have examples of the answer in your data.</span><span class="sxs-lookup"><span data-stu-id="8f131-135">Once you formulate your question, check to see whether you have examples of the answer in your data.</span></span>

<span data-ttu-id="8f131-136">If our question is "What will my stock's sale price be next week?"</span><span class="sxs-lookup"><span data-stu-id="8f131-136">If our question is "What will my stock's sale price be next week?"</span></span> <span data-ttu-id="8f131-137">then we have to make sure our data includes the stock price history.</span><span class="sxs-lookup"><span data-stu-id="8f131-137">then we have to make sure our data includes the stock price history.</span></span>

<span data-ttu-id="8f131-138">If our question is "Which car in my fleet is going to fail first?"</span><span class="sxs-lookup"><span data-stu-id="8f131-138">If our question is "Which car in my fleet is going to fail first?"</span></span> <span data-ttu-id="8f131-139">then we have to make sure our data includes information about previous failures.</span><span class="sxs-lookup"><span data-stu-id="8f131-139">then we have to make sure our data includes information about previous failures.</span></span>

![Target data - examples of your answer.](./media/data-science-for-beginners-ask-a-question-you-can-answer-with-data/target-data.png)

<span data-ttu-id="8f131-142">These examples of answers are called a target.</span><span class="sxs-lookup"><span data-stu-id="8f131-142">These examples of answers are called a target.</span></span> <span data-ttu-id="8f131-143">A target is what we are trying to predict about future data points, whether it's a category or a number.</span><span class="sxs-lookup"><span data-stu-id="8f131-143">A target is what we are trying to predict about future data points, whether it's a category or a number.</span></span>

<span data-ttu-id="8f131-144">If you don't have any target data, you'll need to get some.</span><span class="sxs-lookup"><span data-stu-id="8f131-144">If you don't have any target data, you'll need to get some.</span></span> <span data-ttu-id="8f131-145">You won't be able to answer your question without it.</span><span class="sxs-lookup"><span data-stu-id="8f131-145">You won't be able to answer your question without it.</span></span>

## <a name="reformulate-your-question"></a><span data-ttu-id="8f131-146">Reformulate your question</span><span class="sxs-lookup"><span data-stu-id="8f131-146">Reformulate your question</span></span>
<span data-ttu-id="8f131-147">Sometimes you can reword your question to get a more useful answer.</span><span class="sxs-lookup"><span data-stu-id="8f131-147">Sometimes you can reword your question to get a more useful answer.</span></span>

<span data-ttu-id="8f131-148">The question "Is this data point A or B?"</span><span class="sxs-lookup"><span data-stu-id="8f131-148">The question "Is this data point A or B?"</span></span> <span data-ttu-id="8f131-149">predicts the category (or name or label) of something.</span><span class="sxs-lookup"><span data-stu-id="8f131-149">predicts the category (or name or label) of something.</span></span> <span data-ttu-id="8f131-150">To answer it, we use a *classification algorithm*.</span><span class="sxs-lookup"><span data-stu-id="8f131-150">To answer it, we use a *classification algorithm*.</span></span>

<span data-ttu-id="8f131-151">The question "How much?"</span><span class="sxs-lookup"><span data-stu-id="8f131-151">The question "How much?"</span></span> <span data-ttu-id="8f131-152">or "How many?"</span><span class="sxs-lookup"><span data-stu-id="8f131-152">or "How many?"</span></span> <span data-ttu-id="8f131-153">predicts an amount.</span><span class="sxs-lookup"><span data-stu-id="8f131-153">predicts an amount.</span></span> <span data-ttu-id="8f131-154">To answer it we use a *regression algorithm*.</span><span class="sxs-lookup"><span data-stu-id="8f131-154">To answer it we use a *regression algorithm*.</span></span>

<span data-ttu-id="8f131-155">To see how we can transform these, let's look at the question, "Which news story is the most interesting to this reader?"</span><span class="sxs-lookup"><span data-stu-id="8f131-155">To see how we can transform these, let's look at the question, "Which news story is the most interesting to this reader?"</span></span> <span data-ttu-id="8f131-156">It asks for a prediction of a single choice from many possibilities - in other words "Is this A or B or C or D?"</span><span class="sxs-lookup"><span data-stu-id="8f131-156">It asks for a prediction of a single choice from many possibilities - in other words "Is this A or B or C or D?"</span></span> <span data-ttu-id="8f131-157">- and would use a classification algorithm.</span><span class="sxs-lookup"><span data-stu-id="8f131-157">- and would use a classification algorithm.</span></span>

<span data-ttu-id="8f131-158">But, this question may be easier to answer if you reword it as "How interesting is each story on this list to this reader?"</span><span class="sxs-lookup"><span data-stu-id="8f131-158">But, this question may be easier to answer if you reword it as "How interesting is each story on this list to this reader?"</span></span> <span data-ttu-id="8f131-159">Now you can give each article a numerical score, and then it's easy to identify the highest-scoring article.</span><span class="sxs-lookup"><span data-stu-id="8f131-159">Now you can give each article a numerical score, and then it's easy to identify the highest-scoring article.</span></span> <span data-ttu-id="8f131-160">This is a rephrasing of the classification question into a regression question or How much?</span><span class="sxs-lookup"><span data-stu-id="8f131-160">This is a rephrasing of the classification question into a regression question or How much?</span></span>

![Reformulate your question.](./media/data-science-for-beginners-ask-a-question-you-can-answer-with-data/classification-question-vs-regression-question.png)

<span data-ttu-id="8f131-163">How you ask a question is a clue to which algorithm can give you an answer.</span><span class="sxs-lookup"><span data-stu-id="8f131-163">How you ask a question is a clue to which algorithm can give you an answer.</span></span>

<span data-ttu-id="8f131-164">You'll find that certain families of algorithms - like the ones in our news story example - are closely related.</span><span class="sxs-lookup"><span data-stu-id="8f131-164">You'll find that certain families of algorithms - like the ones in our news story example - are closely related.</span></span> <span data-ttu-id="8f131-165">You can reformulate your question to use the algorithm that gives you the most useful answer.</span><span class="sxs-lookup"><span data-stu-id="8f131-165">You can reformulate your question to use the algorithm that gives you the most useful answer.</span></span>

<span data-ttu-id="8f131-166">But, most important, ask that sharp question - the question that you can answer with data.</span><span class="sxs-lookup"><span data-stu-id="8f131-166">But, most important, ask that sharp question - the question that you can answer with data.</span></span> <span data-ttu-id="8f131-167">And be sure you have the right data to answer it.</span><span class="sxs-lookup"><span data-stu-id="8f131-167">And be sure you have the right data to answer it.</span></span>

<span data-ttu-id="8f131-168">We've talked about some basic principles for asking a question you can answer with data.</span><span class="sxs-lookup"><span data-stu-id="8f131-168">We've talked about some basic principles for asking a question you can answer with data.</span></span>

<span data-ttu-id="8f131-169">Be sure to check out the other videos in "Data Science for Beginners" from Microsoft Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="8f131-169">Be sure to check out the other videos in "Data Science for Beginners" from Microsoft Azure Machine Learning.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8f131-170">Next steps</span><span class="sxs-lookup"><span data-stu-id="8f131-170">Next steps</span></span>
* [<span data-ttu-id="8f131-171">Try a first data science experiment with Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="8f131-171">Try a first data science experiment with Machine Learning Studio</span></span>](create-experiment.md)
* [<span data-ttu-id="8f131-172">Get an introduction to Machine Learning on Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="8f131-172">Get an introduction to Machine Learning on Microsoft Azure</span></span>](what-is-machine-learning.md)
