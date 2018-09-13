---
title: A predictive solution for credit risk with Machine Learning | Microsoft Docs
description: A detailed walkthrough showing how to create a predictive analytics solution for credit risk assessment in Azure Machine Learning Studio.
keywords: credit risk, predictive analytics solution,risk assessment
services: machine-learning
documentationcenter: ''
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 43300854-a14e-4cd2-9bb1-c55c779e0e93
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: e1af999b2fde8ffa2a0ffd1b88230f0aaab32b37
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44671923"
---
# <a name="walkthrough-develop-a-predictive-analytics-solution-for-credit-risk-assessment-in-azure-machine-learning"></a><span data-ttu-id="051fc-104">Walkthrough: Develop a predictive analytics solution for credit risk assessment in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="051fc-104">Walkthrough: Develop a predictive analytics solution for credit risk assessment in Azure Machine Learning</span></span>

<span data-ttu-id="051fc-105">In this walkthrough, we take an extended look at the process of developing a predictive analytics solution in Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="051fc-105">In this walkthrough, we take an extended look at the process of developing a predictive analytics solution in Machine Learning Studio.</span></span> <span data-ttu-id="051fc-106">We develop a simple model in Machine Learning Studio, and then deploy it as an Azure Machine Learning web service where the model can make predictions using new data.</span><span class="sxs-lookup"><span data-stu-id="051fc-106">We develop a simple model in Machine Learning Studio, and then deploy it as an Azure Machine Learning web service where the model can make predictions using new data.</span></span> 

<span data-ttu-id="051fc-107">This walkthrough assumes that you've used Machine Learning Studio at least once before, and that you have some understanding of machine learning concepts.</span><span class="sxs-lookup"><span data-stu-id="051fc-107">This walkthrough assumes that you've used Machine Learning Studio at least once before, and that you have some understanding of machine learning concepts.</span></span> <span data-ttu-id="051fc-108">But it doesn't assume you're an expert in either.</span><span class="sxs-lookup"><span data-stu-id="051fc-108">But it doesn't assume you're an expert in either.</span></span>

<span data-ttu-id="051fc-109">If you've never used **Azure Machine Learning Studio** before, you might want to start with the tutorial, [Create your first data science experiment in Azure Machine Learning Studio](machine-learning-create-experiment.md).</span><span class="sxs-lookup"><span data-stu-id="051fc-109">If you've never used **Azure Machine Learning Studio** before, you might want to start with the tutorial, [Create your first data science experiment in Azure Machine Learning Studio](machine-learning-create-experiment.md).</span></span> <span data-ttu-id="051fc-110">That tutorial takes you through Machine Learning Studio for the first time.</span><span class="sxs-lookup"><span data-stu-id="051fc-110">That tutorial takes you through Machine Learning Studio for the first time.</span></span> <span data-ttu-id="051fc-111">It shows you the basics of how to drag-and-drop modules onto your experiment, connect them together, run the experiment, and look at the results.</span><span class="sxs-lookup"><span data-stu-id="051fc-111">It shows you the basics of how to drag-and-drop modules onto your experiment, connect them together, run the experiment, and look at the results.</span></span> <span data-ttu-id="051fc-112">Another tool that may be helpful for getting started is a diagram that gives an overview of the capabilities of Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="051fc-112">Another tool that may be helpful for getting started is a diagram that gives an overview of the capabilities of Machine Learning Studio.</span></span> <span data-ttu-id="051fc-113">You can download and print it from here: [Overview diagram of Azure Machine Learning Studio capabilities](machine-learning-studio-overview-diagram.md).</span><span class="sxs-lookup"><span data-stu-id="051fc-113">You can download and print it from here: [Overview diagram of Azure Machine Learning Studio capabilities](machine-learning-studio-overview-diagram.md).</span></span>
 
<span data-ttu-id="051fc-114">If you're new to the field of machine learning in general, there's a video series that might be helpful to you.</span><span class="sxs-lookup"><span data-stu-id="051fc-114">If you're new to the field of machine learning in general, there's a video series that might be helpful to you.</span></span> <span data-ttu-id="051fc-115">It's called [Data Science for Beginners](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) and it can give you a great introduction to machine learning using everyday language and concepts.</span><span class="sxs-lookup"><span data-stu-id="051fc-115">It's called [Data Science for Beginners](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) and it can give you a great introduction to machine learning using everyday language and concepts.</span></span>


[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
 

## <a name="the-problem"></a><span data-ttu-id="051fc-116">The problem</span><span class="sxs-lookup"><span data-stu-id="051fc-116">The problem</span></span>

<span data-ttu-id="051fc-117">Suppose you need to predict an individual's credit risk based on the information they gave on a credit application.</span><span class="sxs-lookup"><span data-stu-id="051fc-117">Suppose you need to predict an individual's credit risk based on the information they gave on a credit application.</span></span>  

<span data-ttu-id="051fc-118">Credit risk assessment is a complex problem, but we can simplify it a bit for this walkthrough.</span><span class="sxs-lookup"><span data-stu-id="051fc-118">Credit risk assessment is a complex problem, but we can simplify it a bit for this walkthrough.</span></span> <span data-ttu-id="051fc-119">We'll use it as an example of how you can create a predictive analytics solution using Microsoft Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="051fc-119">We'll use it as an example of how you can create a predictive analytics solution using Microsoft Azure Machine Learning.</span></span> <span data-ttu-id="051fc-120">To do this, we use Azure Machine Learning Studio and a Machine Learning web service.</span><span class="sxs-lookup"><span data-stu-id="051fc-120">To do this, we use Azure Machine Learning Studio and a Machine Learning web service.</span></span>  

## <a name="the-solution"></a><span data-ttu-id="051fc-121">The solution</span><span class="sxs-lookup"><span data-stu-id="051fc-121">The solution</span></span>

<span data-ttu-id="051fc-122">In this detailed walkthrough, we start with publicly available credit risk data and develop and train a predictive model based on that data.</span><span class="sxs-lookup"><span data-stu-id="051fc-122">In this detailed walkthrough, we start with publicly available credit risk data and develop and train a predictive model based on that data.</span></span> <span data-ttu-id="051fc-123">Then we deploy the model as a web service so it can be used by others for credit risk assessment.</span><span class="sxs-lookup"><span data-stu-id="051fc-123">Then we deploy the model as a web service so it can be used by others for credit risk assessment.</span></span>

<span data-ttu-id="051fc-124">To create this credit risk assessment solution, we follow these steps:</span><span class="sxs-lookup"><span data-stu-id="051fc-124">To create this credit risk assessment solution, we follow these steps:</span></span>  

1. [<span data-ttu-id="051fc-125">Create a Machine Learning workspace</span><span class="sxs-lookup"><span data-stu-id="051fc-125">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="051fc-126">Upload existing data</span><span class="sxs-lookup"><span data-stu-id="051fc-126">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="051fc-127">Create an experiment</span><span class="sxs-lookup"><span data-stu-id="051fc-127">Create an experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="051fc-128">Train and evaluate the models</span><span class="sxs-lookup"><span data-stu-id="051fc-128">Train and evaluate the models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="051fc-129">Deploy the web service</span><span class="sxs-lookup"><span data-stu-id="051fc-129">Deploy the web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="051fc-130">Access the web service</span><span class="sxs-lookup"><span data-stu-id="051fc-130">Access the web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

> [!TIP] 
> <span data-ttu-id="051fc-131">You can find a working copy of the experiment that we develop in this walkthrough in the [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="051fc-131">You can find a working copy of the experiment that we develop in this walkthrough in the [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="051fc-132">Go to **[Walkthrough - Credit risk prediction](https://gallery.cortanaintelligence.com/Experiment/Walkthrough-Credit-risk-prediction-1)** and click **Open in Studio** to download a copy of the experiment into your Machine Learning Studio workspace.</span><span class="sxs-lookup"><span data-stu-id="051fc-132">Go to **[Walkthrough - Credit risk prediction](https://gallery.cortanaintelligence.com/Experiment/Walkthrough-Credit-risk-prediction-1)** and click **Open in Studio** to download a copy of the experiment into your Machine Learning Studio workspace.</span></span>
> 
> <span data-ttu-id="051fc-133">This walkthrough is based on a simplified version of the sample experiment, [Binary Classification: Credit risk prediction](http://go.microsoft.com/fwlink/?LinkID=525270), also available in the [Gallery](http://gallery.cortanaintelligence.com/).</span><span class="sxs-lookup"><span data-stu-id="051fc-133">This walkthrough is based on a simplified version of the sample experiment, [Binary Classification: Credit risk prediction](http://go.microsoft.com/fwlink/?LinkID=525270), also available in the [Gallery](http://gallery.cortanaintelligence.com/).</span></span>
