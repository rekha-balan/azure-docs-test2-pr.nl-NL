---
title: Sentiment Analysis using Deep Learning with Azure Machine Learning | Microsoft Docs
description: How to perform sentiment analysis using deep learning with Azure ML Workbench.
services: machine-learning
documentationcenter: ''
author: miprasad
manager: kristin.tolle
editor: miprasad
ms.assetid: ''
ms.reviewer: garyericson, jasonwhowell, mldocs
ms.service: machine-learning
ms.component: core
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/20/2018
ms.author: miprasad
ms.openlocfilehash: 97e3a621e291935db2e0c70eb2b596e77c7bffb7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856292"
---
# <a name="sentiment-analysis-using-deep-learning-with-azure-machine-learning"></a><span data-ttu-id="22ef8-103">Sentiment Analysis using Deep Learning with Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="22ef8-103">Sentiment Analysis using Deep Learning with Azure Machine Learning</span></span>

<span data-ttu-id="22ef8-104">Sentiment analysis is a well-known task in the realm of natural language processing.</span><span class="sxs-lookup"><span data-stu-id="22ef8-104">Sentiment analysis is a well-known task in the realm of natural language processing.</span></span> <span data-ttu-id="22ef8-105">Given a set of texts, the aim is to determine the sentiment of that text.</span><span class="sxs-lookup"><span data-stu-id="22ef8-105">Given a set of texts, the aim is to determine the sentiment of that text.</span></span> <span data-ttu-id="22ef8-106">The objective of this solution is to use Deep Learning for predicting sentiment from movie reviews.</span><span class="sxs-lookup"><span data-stu-id="22ef8-106">The objective of this solution is to use Deep Learning for predicting sentiment from movie reviews.</span></span>

<span data-ttu-id="22ef8-107">The solution is located at https://github.com/Azure/MachineLearningSamples-SentimentAnalysis</span><span class="sxs-lookup"><span data-stu-id="22ef8-107">The solution is located at https://github.com/Azure/MachineLearningSamples-SentimentAnalysis</span></span>

## <a name="link-to-the-gallery-github-repository"></a><span data-ttu-id="22ef8-108">Link to the Gallery GitHub repository</span><span class="sxs-lookup"><span data-stu-id="22ef8-108">Link to the Gallery GitHub repository</span></span>

<span data-ttu-id="22ef8-109">Follow this link to the public GitHub repository:</span><span class="sxs-lookup"><span data-stu-id="22ef8-109">Follow this link to the public GitHub repository:</span></span>

[https://github.com/Azure/MachineLearningSamples-SentimentAnalysis](https://github.com/Azure/MachineLearningSamples-SentimentAnalysis)

## <a name="use-case-overview"></a><span data-ttu-id="22ef8-110">Use case overview</span><span class="sxs-lookup"><span data-stu-id="22ef8-110">Use case overview</span></span>

<span data-ttu-id="22ef8-111">The explosion of data and the proliferation of mobile devices have created lots of opportunities for customers to express their feelings and attitudes about anything and everything at any time.</span><span class="sxs-lookup"><span data-stu-id="22ef8-111">The explosion of data and the proliferation of mobile devices have created lots of opportunities for customers to express their feelings and attitudes about anything and everything at any time.</span></span> <span data-ttu-id="22ef8-112">This opinion or "sentiment" is often generated through social channels in the form of reviews, chats, shares, likes, tweets, etc. The sentiment can be invaluable for businesses looking to improve products and services, make more informed decisions, and better promote their brands.</span><span class="sxs-lookup"><span data-stu-id="22ef8-112">This opinion or "sentiment" is often generated through social channels in the form of reviews, chats, shares, likes, tweets, etc. The sentiment can be invaluable for businesses looking to improve products and services, make more informed decisions, and better promote their brands.</span></span>

<span data-ttu-id="22ef8-113">To get value from sentiment analysis, businesses must have the ability to mine vast stores of unstructured social data for actionable insights.</span><span class="sxs-lookup"><span data-stu-id="22ef8-113">To get value from sentiment analysis, businesses must have the ability to mine vast stores of unstructured social data for actionable insights.</span></span> <span data-ttu-id="22ef8-114">In this sample, we develop deep learning models for performing sentiment analysis of movie reviews using AMLWorkbench</span><span class="sxs-lookup"><span data-stu-id="22ef8-114">In this sample, we develop deep learning models for performing sentiment analysis of movie reviews using AMLWorkbench</span></span>

## <a name="prerequisites"></a><span data-ttu-id="22ef8-115">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="22ef8-115">Prerequisites</span></span>

* <span data-ttu-id="22ef8-116">An [Azure account](https://azure.microsoft.com/free/) (free trials are available).</span><span class="sxs-lookup"><span data-stu-id="22ef8-116">An [Azure account](https://azure.microsoft.com/free/) (free trials are available).</span></span>

* <span data-ttu-id="22ef8-117">An installed copy of [Azure Machine Learning Workbench](../service/overview-what-is-azure-ml.md) following the [quick start installation guide](../service/quickstart-installation.md) to install the program and create a workspace.</span><span class="sxs-lookup"><span data-stu-id="22ef8-117">An installed copy of [Azure Machine Learning Workbench](../service/overview-what-is-azure-ml.md) following the [quick start installation guide](../service/quickstart-installation.md) to install the program and create a workspace.</span></span>

* <span data-ttu-id="22ef8-118">For operationalization, it is best if you have Docker engine installed and running locally.</span><span class="sxs-lookup"><span data-stu-id="22ef8-118">For operationalization, it is best if you have Docker engine installed and running locally.</span></span> <span data-ttu-id="22ef8-119">If not, you can use the cluster option.</span><span class="sxs-lookup"><span data-stu-id="22ef8-119">If not, you can use the cluster option.</span></span> <span data-ttu-id="22ef8-120">However, running an Azure Container Service (ACS) can be expensive.</span><span class="sxs-lookup"><span data-stu-id="22ef8-120">However, running an Azure Container Service (ACS) can be expensive.</span></span>

* <span data-ttu-id="22ef8-121">This Solution assumes that you are running Azure Machine Learning Workbench on Windows 10 with Docker engine locally installed.</span><span class="sxs-lookup"><span data-stu-id="22ef8-121">This Solution assumes that you are running Azure Machine Learning Workbench on Windows 10 with Docker engine locally installed.</span></span> <span data-ttu-id="22ef8-122">On a macOS, the instruction is largely the same.</span><span class="sxs-lookup"><span data-stu-id="22ef8-122">On a macOS, the instruction is largely the same.</span></span>

## <a name="data-description"></a><span data-ttu-id="22ef8-123">Data description</span><span class="sxs-lookup"><span data-stu-id="22ef8-123">Data description</span></span>

<span data-ttu-id="22ef8-124">The dataset used for this sample is a small hand-crafted dataset and is located in the [data folder](https://github.com/Azure/MachineLearningSamples-SentimentAnalysis/tree/master/data).</span><span class="sxs-lookup"><span data-stu-id="22ef8-124">The dataset used for this sample is a small hand-crafted dataset and is located in the [data folder](https://github.com/Azure/MachineLearningSamples-SentimentAnalysis/tree/master/data).</span></span>

<span data-ttu-id="22ef8-125">The first column contains movie reviews and the second column contains their sentiment (0 - negative and 1 - positive).</span><span class="sxs-lookup"><span data-stu-id="22ef8-125">The first column contains movie reviews and the second column contains their sentiment (0 - negative and 1 - positive).</span></span> <span data-ttu-id="22ef8-126">The dataset is merely used for demonstration purposes but typically to get robust sentiment scores, you need a large dataset.</span><span class="sxs-lookup"><span data-stu-id="22ef8-126">The dataset is merely used for demonstration purposes but typically to get robust sentiment scores, you need a large dataset.</span></span> <span data-ttu-id="22ef8-127">For example, the [IMDB Movie reviews sentiment classification problem](https://keras.io/datasets/#datasets ) from Keras consists of a dataset of 25,000 movies reviews from IMDB, labeled by sentiment (positive or negative).</span><span class="sxs-lookup"><span data-stu-id="22ef8-127">For example, the [IMDB Movie reviews sentiment classification problem](https://keras.io/datasets/#datasets ) from Keras consists of a dataset of 25,000 movies reviews from IMDB, labeled by sentiment (positive or negative).</span></span> <span data-ttu-id="22ef8-128">The intention of this lab is to show you how to perform sentiment analysis using deep learning with AMLWorkbench.</span><span class="sxs-lookup"><span data-stu-id="22ef8-128">The intention of this lab is to show you how to perform sentiment analysis using deep learning with AMLWorkbench.</span></span>

## <a name="scenario-structure"></a><span data-ttu-id="22ef8-129">Scenario structure</span><span class="sxs-lookup"><span data-stu-id="22ef8-129">Scenario structure</span></span>

<span data-ttu-id="22ef8-130">The folder structure is arranged as follows:</span><span class="sxs-lookup"><span data-stu-id="22ef8-130">The folder structure is arranged as follows:</span></span>

1. <span data-ttu-id="22ef8-131">All the code related to sentiment analysis using AMLWorkbench is in the root folder</span><span class="sxs-lookup"><span data-stu-id="22ef8-131">All the code related to sentiment analysis using AMLWorkbench is in the root folder</span></span>
2. <span data-ttu-id="22ef8-132">data: Contains the dataset used in the solution</span><span class="sxs-lookup"><span data-stu-id="22ef8-132">data: Contains the dataset used in the solution</span></span>
3. <span data-ttu-id="22ef8-133">docs: Contains all the hands-on labs</span><span class="sxs-lookup"><span data-stu-id="22ef8-133">docs: Contains all the hands-on labs</span></span>

<span data-ttu-id="22ef8-134">The order of Hands-on Labs to carry out the solution is as follows:</span><span class="sxs-lookup"><span data-stu-id="22ef8-134">The order of Hands-on Labs to carry out the solution is as follows:</span></span>

| <span data-ttu-id="22ef8-135">Order</span><span class="sxs-lookup"><span data-stu-id="22ef8-135">Order</span></span>| <span data-ttu-id="22ef8-136">File Name</span><span class="sxs-lookup"><span data-stu-id="22ef8-136">File Name</span></span> | <span data-ttu-id="22ef8-137">Related Files</span><span class="sxs-lookup"><span data-stu-id="22ef8-137">Related Files</span></span> |
|--|-----------|------|
| <span data-ttu-id="22ef8-138">1</span><span class="sxs-lookup"><span data-stu-id="22ef8-138">1</span></span> | [`SentimentAnalysisDataPreparation.md`](https://github.com/Azure/MachineLearningSamples-SentimentAnalysis/blob/master/docs/SentimentAnalysisDataPreparation.md) | <span data-ttu-id="22ef8-139">'data/sampleReviews.txt'</span><span class="sxs-lookup"><span data-stu-id="22ef8-139">'data/sampleReviews.txt'</span></span> |
| <span data-ttu-id="22ef8-140">2</span><span class="sxs-lookup"><span data-stu-id="22ef8-140">2</span></span> | [`SentimentAnalysisModelingKeras.md`](https://github.com/Azure/MachineLearningSamples-SentimentAnalysis/blob/master/docs/SentimentAnalysisModelingKeras.md) | <span data-ttu-id="22ef8-141">'SentimentExtraction.py'</span><span class="sxs-lookup"><span data-stu-id="22ef8-141">'SentimentExtraction.py'</span></span> |
| <span data-ttu-id="22ef8-142">3</span><span class="sxs-lookup"><span data-stu-id="22ef8-142">3</span></span> | [`SentimentAnalysisOperationalization.md`](https://github.com/Azure/MachineLearningSamples-SentimentAnalysis/blob/master/docs/SentimentAnalysisOperationalization.md) | <span data-ttu-id="22ef8-143">'Operaionalization'</span><span class="sxs-lookup"><span data-stu-id="22ef8-143">'Operaionalization'</span></span> |

## <a name="conclusion"></a><span data-ttu-id="22ef8-144">Conclusion</span><span class="sxs-lookup"><span data-stu-id="22ef8-144">Conclusion</span></span>

<span data-ttu-id="22ef8-145">In conclusion, this solution introduces you to using Deep Learning to perform sentiment analysis with the Azure Machine Learning Workbench.</span><span class="sxs-lookup"><span data-stu-id="22ef8-145">In conclusion, this solution introduces you to using Deep Learning to perform sentiment analysis with the Azure Machine Learning Workbench.</span></span> <span data-ttu-id="22ef8-146">We also operationalize using HDF5 models.</span><span class="sxs-lookup"><span data-stu-id="22ef8-146">We also operationalize using HDF5 models.</span></span>
