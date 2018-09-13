---
title: (deprecated) Machine learning web services examples built with R - Azure | Microsoft Docs
description: (deprecated) Find a useful set of web services examples created with R code and Machine Learning, and published to the Azure Marketplace.
keywords: csharp,r code,web services examples
services: machine-learning
documentationcenter: ''
author: jaymathe
manager: jhubbard
editor: cgronlun
ms.assetid: 97d66cb7-6a84-4ae9-8095-0b5f5ba82d7f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: deprecated
ms.date: 01/06/2017
ms.author: jaymathe
ROBOTS: NOINDEX, NOFOLLOW
ms.openlocfilehash: b080ab4eadcff6943481f9d8b7bcc78b410c3c9c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551523"
---
# <a name="deprecated-web-services-examples-using-r-code-on-azure-machine-learning-and-published-to-microsoft-azure-marketplace"></a><span data-ttu-id="eddfb-104">(deprecated) Web services examples using R code on Azure Machine Learning and published to Microsoft Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="eddfb-104">(deprecated) Web services examples using R code on Azure Machine Learning and published to Microsoft Azure Marketplace</span></span>

> [!NOTE]
> <span data-ttu-id="eddfb-105">The Microsoft DataMarket is being retired and these APIs have been deprecated.</span><span class="sxs-lookup"><span data-stu-id="eddfb-105">The Microsoft DataMarket is being retired and these APIs have been deprecated.</span></span> 
> 
> <span data-ttu-id="eddfb-106">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="eddfb-106">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="eddfb-107">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="eddfb-107">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="eddfb-108">In this article are example web services were created using Azure Machine Learning and published to the Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="eddfb-108">In this article are example web services were created using Azure Machine Learning and published to the Azure Marketplace.</span></span> <span data-ttu-id="eddfb-109">Each web service example has a comprehensive document attached, embedding sample data sets for testing the services and explaining how the user can create a similar service themselves.</span><span class="sxs-lookup"><span data-stu-id="eddfb-109">Each web service example has a comprehensive document attached, embedding sample data sets for testing the services and explaining how the user can create a similar service themselves.</span></span> 

<span data-ttu-id="eddfb-110">In Azure Machine Learning Studio, users can write R code and with a few clicks, publish it as a web service for applications and devices to consume around the world.</span><span class="sxs-lookup"><span data-stu-id="eddfb-110">In Azure Machine Learning Studio, users can write R code and with a few clicks, publish it as a web service for applications and devices to consume around the world.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="eddfb-111">From producing simple calculators that provide statistical functionality to creating a custom text-mining sentiment analysis predictor, both new and experienced R users can benefit from the ease with which users of Azure Machine Learning can operationalize R code.</span><span class="sxs-lookup"><span data-stu-id="eddfb-111">From producing simple calculators that provide statistical functionality to creating a custom text-mining sentiment analysis predictor, both new and experienced R users can benefit from the ease with which users of Azure Machine Learning can operationalize R code.</span></span> <span data-ttu-id="eddfb-112">While these web services could be consumed by users, potentially through a mobile app or a website, the purpose of these web services examples is to show how Machine Learning can operationalize R scripts for analytical purposes and be used to create web services on top of R code.</span><span class="sxs-lookup"><span data-stu-id="eddfb-112">While these web services could be consumed by users, potentially through a mobile app or a website, the purpose of these web services examples is to show how Machine Learning can operationalize R scripts for analytical purposes and be used to create web services on top of R code.</span></span>

<span data-ttu-id="eddfb-113">Each example includes a C# example for web service consumption.</span><span class="sxs-lookup"><span data-stu-id="eddfb-113">Each example includes a C# example for web service consumption.</span></span>

![Diagram of R code in Azure Machine Learning: R solutions for proprietary use or published to the Azure Marketplace.][1]

<span data-ttu-id="eddfb-115">Consider the following scenarios.</span><span class="sxs-lookup"><span data-stu-id="eddfb-115">Consider the following scenarios.</span></span>

## <a name="scenario-1-generic-model"></a><span data-ttu-id="eddfb-116">Scenario 1: Generic model</span><span class="sxs-lookup"><span data-stu-id="eddfb-116">Scenario 1: Generic model</span></span>
<span data-ttu-id="eddfb-117">A user works with a generic model that can be applied to a new user’s data, such as a basic forecasting of time series data or a custom-built R method with advanced analytics.</span><span class="sxs-lookup"><span data-stu-id="eddfb-117">A user works with a generic model that can be applied to a new user’s data, such as a basic forecasting of time series data or a custom-built R method with advanced analytics.</span></span> <span data-ttu-id="eddfb-118">This user publishes the model as a web service for others to consume with their data.</span><span class="sxs-lookup"><span data-stu-id="eddfb-118">This user publishes the model as a web service for others to consume with their data.</span></span>

* [<span data-ttu-id="eddfb-119">Binary Classifier</span><span class="sxs-lookup"><span data-stu-id="eddfb-119">Binary Classifier</span></span>](machine-learning-r-csharp-binary-classifier.md)
* [<span data-ttu-id="eddfb-120">Cluster Model</span><span class="sxs-lookup"><span data-stu-id="eddfb-120">Cluster Model</span></span>](machine-learning-r-csharp-cluster-model.md)
* [<span data-ttu-id="eddfb-121">Multivariate Linear Regression</span><span class="sxs-lookup"><span data-stu-id="eddfb-121">Multivariate Linear Regression</span></span>](machine-learning-r-csharp-multivariate-linear-regression.md)
* [<span data-ttu-id="eddfb-122">Forecasting - Exponential Smoothing</span><span class="sxs-lookup"><span data-stu-id="eddfb-122">Forecasting - Exponential Smoothing</span></span>](machine-learning-r-csharp-forecasting-exponential-smoothing.md)
* [<span data-ttu-id="eddfb-123">ETS + STL Forecasting</span><span class="sxs-lookup"><span data-stu-id="eddfb-123">ETS + STL Forecasting</span></span>](machine-learning-r-csharp-retail-demand-forecasting.md)
* [<span data-ttu-id="eddfb-124">Forecasting - Autoregressive Integrated Moving Average (ARIMA)</span><span class="sxs-lookup"><span data-stu-id="eddfb-124">Forecasting - Autoregressive Integrated Moving Average (ARIMA)</span></span>](machine-learning-r-csharp-arima.md)
* [<span data-ttu-id="eddfb-125">Survival Analysis</span><span class="sxs-lookup"><span data-stu-id="eddfb-125">Survival Analysis</span></span>](machine-learning-r-csharp-survival-analysis.md)

## <a name="scenario-2-trained-model--specific-data"></a><span data-ttu-id="eddfb-126">Scenario 2: Trained model – specific data</span><span class="sxs-lookup"><span data-stu-id="eddfb-126">Scenario 2: Trained model – specific data</span></span>
<span data-ttu-id="eddfb-127">A user has data that provides useful predictions through R code, such as a large sample of personality questionnaires clustered through a k-means algorithm to predict the user’s personality type, or health survey data that can be used to predict an individual’s risk for lung cancer with a survival analysis R package.</span><span class="sxs-lookup"><span data-stu-id="eddfb-127">A user has data that provides useful predictions through R code, such as a large sample of personality questionnaires clustered through a k-means algorithm to predict the user’s personality type, or health survey data that can be used to predict an individual’s risk for lung cancer with a survival analysis R package.</span></span> <span data-ttu-id="eddfb-128">The user publishes the data through a web service that predicts a new user’s outcome.</span><span class="sxs-lookup"><span data-stu-id="eddfb-128">The user publishes the data through a web service that predicts a new user’s outcome.</span></span>

## <a name="scenario-3-trained-model--generic-data"></a><span data-ttu-id="eddfb-129">Scenario 3: Trained model – generic data</span><span class="sxs-lookup"><span data-stu-id="eddfb-129">Scenario 3: Trained model – generic data</span></span>
<span data-ttu-id="eddfb-130">A user has generic data (such as a text corpus) that allows a web service to be built and applied generically across different types of use cases and scenarios.</span><span class="sxs-lookup"><span data-stu-id="eddfb-130">A user has generic data (such as a text corpus) that allows a web service to be built and applied generically across different types of use cases and scenarios.</span></span>

* [<span data-ttu-id="eddfb-131">Lexicon Based Sentiment Analysis</span><span class="sxs-lookup"><span data-stu-id="eddfb-131">Lexicon Based Sentiment Analysis</span></span>](machine-learning-r-csharp-lexicon-based-sentiment-analysis.md)

## <a name="scenario-4-advanced-calculator"></a><span data-ttu-id="eddfb-132">Scenario 4: Advanced calculator</span><span class="sxs-lookup"><span data-stu-id="eddfb-132">Scenario 4: Advanced calculator</span></span>
<span data-ttu-id="eddfb-133">A user provides advanced calculations or simulations that don’t require any trained model or fitting of a model to the user’s data.</span><span class="sxs-lookup"><span data-stu-id="eddfb-133">A user provides advanced calculations or simulations that don’t require any trained model or fitting of a model to the user’s data.</span></span>

* [<span data-ttu-id="eddfb-134">Difference in Proportions Test</span><span class="sxs-lookup"><span data-stu-id="eddfb-134">Difference in Proportions Test</span></span>](machine-learning-r-csharp-difference-in-two-proportions.md)
* [<span data-ttu-id="eddfb-135">Normal Distribution Suite</span><span class="sxs-lookup"><span data-stu-id="eddfb-135">Normal Distribution Suite</span></span>](machine-learning-r-csharp-normal-distribution.md)
* [<span data-ttu-id="eddfb-136">Binomial Distribution Suite</span><span class="sxs-lookup"><span data-stu-id="eddfb-136">Binomial Distribution Suite</span></span>](machine-learning-r-csharp-binomial-distribution.md)

## <a name="faq"></a><span data-ttu-id="eddfb-137">FAQ</span><span class="sxs-lookup"><span data-stu-id="eddfb-137">FAQ</span></span>
<span data-ttu-id="eddfb-138">For frequently asked questions on consumption of the web service or publishing to the Marketplace, see [here](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="eddfb-138">For frequently asked questions on consumption of the web service or publishing to the Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-r-csharp-web-service-examples/machine-learning-r-code-options-for-using-and-sharing-cloud.png




