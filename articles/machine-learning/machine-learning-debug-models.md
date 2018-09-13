---
title: Debug your Model in Azure Machine Learning | Microsoft Docs
description: How to debug errors produced by Train Model and Score Model modules in Azure Machine Learning.
services: machine-learning
documentationcenter: ''
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 629dc45e-ac1e-4b7d-b120-08813dc448be
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bradsev;garye
ms.openlocfilehash: 42a032a253544641a835838a07ce4db3e8fcdb9a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551142"
---
# <a name="debug-your-model-in-azure-machine-learning"></a><span data-ttu-id="1a1fa-103">Debug your Model in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="1a1fa-103">Debug your Model in Azure Machine Learning</span></span>

<span data-ttu-id="1a1fa-104">This article explains the potential reasons why either of the following two failures might be encountered when running a model:</span><span class="sxs-lookup"><span data-stu-id="1a1fa-104">This article explains the potential reasons why either of the following two failures might be encountered when running a model:</span></span>

* <span data-ttu-id="1a1fa-105">the [Train Model][train-model] module produces an error</span><span class="sxs-lookup"><span data-stu-id="1a1fa-105">the [Train Model][train-model] module produces an error</span></span> 
* <span data-ttu-id="1a1fa-106">the [Score Model][score-model] module produces incorrect results</span><span class="sxs-lookup"><span data-stu-id="1a1fa-106">the [Score Model][score-model] module produces incorrect results</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="train-model-module-produces-an-error"></a><span data-ttu-id="1a1fa-107">Train Model Module produces an error</span><span class="sxs-lookup"><span data-stu-id="1a1fa-107">Train Model Module produces an error</span></span>

![image1](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-debug-models/train_model-1.png)

<span data-ttu-id="1a1fa-109">The [Train Model][train-model] Module expects two inputs:</span><span class="sxs-lookup"><span data-stu-id="1a1fa-109">The [Train Model][train-model] Module expects two inputs:</span></span>

1. <span data-ttu-id="1a1fa-110">The type of machine learning model from the collection of models provided by Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="1a1fa-110">The type of machine learning model from the collection of models provided by Azure Machine Learning.</span></span>
2. <span data-ttu-id="1a1fa-111">The training data with a specified Label column which specifies the variable to predict (the other columns are assumed to be Features).</span><span class="sxs-lookup"><span data-stu-id="1a1fa-111">The training data with a specified Label column which specifies the variable to predict (the other columns are assumed to be Features).</span></span>

<span data-ttu-id="1a1fa-112">This module can produce an error in the following cases:</span><span class="sxs-lookup"><span data-stu-id="1a1fa-112">This module can produce an error in the following cases:</span></span>

1. <span data-ttu-id="1a1fa-113">The Label column is specified incorrectly.</span><span class="sxs-lookup"><span data-stu-id="1a1fa-113">The Label column is specified incorrectly.</span></span> <span data-ttu-id="1a1fa-114">This can happen if either more than one column is selected as the Label or an incorrect column index is selected.</span><span class="sxs-lookup"><span data-stu-id="1a1fa-114">This can happen if either more than one column is selected as the Label or an incorrect column index is selected.</span></span> <span data-ttu-id="1a1fa-115">For example, the second case would apply if a column index of 30 is used with an input dataset which has only 25 columns.</span><span class="sxs-lookup"><span data-stu-id="1a1fa-115">For example, the second case would apply if a column index of 30 is used with an input dataset which has only 25 columns.</span></span>

2. <span data-ttu-id="1a1fa-116">The dataset does not contain any Feature columns.</span><span class="sxs-lookup"><span data-stu-id="1a1fa-116">The dataset does not contain any Feature columns.</span></span> <span data-ttu-id="1a1fa-117">For example, if the input dataset has only one column, which is marked as the Label column, there would be no features with which to build the model.</span><span class="sxs-lookup"><span data-stu-id="1a1fa-117">For example, if the input dataset has only one column, which is marked as the Label column, there would be no features with which to build the model.</span></span> <span data-ttu-id="1a1fa-118">In this case, the [Train Model][train-model] module produces an error.</span><span class="sxs-lookup"><span data-stu-id="1a1fa-118">In this case, the [Train Model][train-model] module produces an error.</span></span>

3. <span data-ttu-id="1a1fa-119">The input dataset (Features or Label) contains Infinity as a value.</span><span class="sxs-lookup"><span data-stu-id="1a1fa-119">The input dataset (Features or Label) contains Infinity as a value.</span></span>

## <a name="score-model-module-produces-incorrect-results"></a><span data-ttu-id="1a1fa-120">Score Model Module produces incorrect results</span><span class="sxs-lookup"><span data-stu-id="1a1fa-120">Score Model Module produces incorrect results</span></span>

![image2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-debug-models/train_test-2.png)

<span data-ttu-id="1a1fa-122">In a typical training/testing experiment for supervised learning, the [Split Data][split] module divides the original dataset into two parts: one part is used to train the model and one part is used to score how well the trained model performs.</span><span class="sxs-lookup"><span data-stu-id="1a1fa-122">In a typical training/testing experiment for supervised learning, the [Split Data][split] module divides the original dataset into two parts: one part is used to train the model and one part is used to score how well the trained model performs.</span></span> <span data-ttu-id="1a1fa-123">The trained model is then used to score the test data, after which the results are evaluated to determine the accuracy of the model.</span><span class="sxs-lookup"><span data-stu-id="1a1fa-123">The trained model is then used to score the test data, after which the results are evaluated to determine the accuracy of the model.</span></span>

<span data-ttu-id="1a1fa-124">The [Score Model][score-model] module requires two inputs:</span><span class="sxs-lookup"><span data-stu-id="1a1fa-124">The [Score Model][score-model] module requires two inputs:</span></span>

1. <span data-ttu-id="1a1fa-125">A trained model output from the [Train Model][train-model] module.</span><span class="sxs-lookup"><span data-stu-id="1a1fa-125">A trained model output from the [Train Model][train-model] module.</span></span>
2. <span data-ttu-id="1a1fa-126">A scoring dataset that is different from the dataset used to train the model.</span><span class="sxs-lookup"><span data-stu-id="1a1fa-126">A scoring dataset that is different from the dataset used to train the model.</span></span>

<span data-ttu-id="1a1fa-127">It's possible that even though the experiment succeeds, the [Score Model][score-model] module produces incorrect results.</span><span class="sxs-lookup"><span data-stu-id="1a1fa-127">It's possible that even though the experiment succeeds, the [Score Model][score-model] module produces incorrect results.</span></span> <span data-ttu-id="1a1fa-128">Several scenarios may cause this to happen:</span><span class="sxs-lookup"><span data-stu-id="1a1fa-128">Several scenarios may cause this to happen:</span></span>

1. <span data-ttu-id="1a1fa-129">If the specified Label is categorical and a regression model is trained on the data, an incorrect output would be produced by the [Score Model][score-model] module.</span><span class="sxs-lookup"><span data-stu-id="1a1fa-129">If the specified Label is categorical and a regression model is trained on the data, an incorrect output would be produced by the [Score Model][score-model] module.</span></span> <span data-ttu-id="1a1fa-130">This is because regression requires a continuous response variable.</span><span class="sxs-lookup"><span data-stu-id="1a1fa-130">This is because regression requires a continuous response variable.</span></span> <span data-ttu-id="1a1fa-131">In this case, it would be more suitable to use a classification model.</span><span class="sxs-lookup"><span data-stu-id="1a1fa-131">In this case, it would be more suitable to use a classification model.</span></span> 

2. <span data-ttu-id="1a1fa-132">Similarly, if a classification model is trained on a dataset having floating point numbers in the Label column, it may produce undesirable results.</span><span class="sxs-lookup"><span data-stu-id="1a1fa-132">Similarly, if a classification model is trained on a dataset having floating point numbers in the Label column, it may produce undesirable results.</span></span> <span data-ttu-id="1a1fa-133">This is because classification requires a discrete response variable that only allows values that range over a finite, and usually somewhat small, set of classes.</span><span class="sxs-lookup"><span data-stu-id="1a1fa-133">This is because classification requires a discrete response variable that only allows values that range over a finite, and usually somewhat small, set of classes.</span></span>

3. <span data-ttu-id="1a1fa-134">If the scoring dataset does not contain all the features used to train the model, the [Score Model][score-model] produces an error.</span><span class="sxs-lookup"><span data-stu-id="1a1fa-134">If the scoring dataset does not contain all the features used to train the model, the [Score Model][score-model] produces an error.</span></span>

4. <span data-ttu-id="1a1fa-135">If a row in the scoring dataset contains a missing value or an infinite value for any of its features, the [Score Model][score-model] will not produce any output corresponding to that row.</span><span class="sxs-lookup"><span data-stu-id="1a1fa-135">If a row in the scoring dataset contains a missing value or an infinite value for any of its features, the [Score Model][score-model] will not produce any output corresponding to that row.</span></span>

5. <span data-ttu-id="1a1fa-136">The [Score Model][score-model] may produce identical outputs for all rows in the scoring dataset.</span><span class="sxs-lookup"><span data-stu-id="1a1fa-136">The [Score Model][score-model] may produce identical outputs for all rows in the scoring dataset.</span></span> <span data-ttu-id="1a1fa-137">This could occur, for example, when attempting classification using Decision Forests if the minimum number of samples per leaf node is chosen to be more than the number of training examples available.</span><span class="sxs-lookup"><span data-stu-id="1a1fa-137">This could occur, for example, when attempting classification using Decision Forests if the minimum number of samples per leaf node is chosen to be more than the number of training examples available.</span></span>

<!-- Module References -->
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/



