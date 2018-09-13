---
title: Text Analytics API in Microsoft Cognitive Services | Microsoft Docs
description: Use the Text Analytics API for sentiment analysis, key phrase extraction, topic detection for English text, and much more.
services: cognitive-services
author: LuisCabrer
manager: mwinkle
ms.service: cognitive-services
ms.technology: text-analytics
ms.topic: article
ms.date: 04/06/2016
ms.author: luisca
ms.openlocfilehash: c3b7eb2823a2d766809d567a1ef8184ffbd9139a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552893"
---
# <a name="text-analytics-documentation"></a><span data-ttu-id="5002c-103">Text Analytics Documentation</span><span class="sxs-lookup"><span data-stu-id="5002c-103">Text Analytics Documentation</span></span>

<span data-ttu-id="5002c-104">**Description**</span><span class="sxs-lookup"><span data-stu-id="5002c-104">**Description**</span></span>

<span data-ttu-id="5002c-105">Understanding and analyzing unstructured text is an increasingly popular field and includes a wide spectrum of problems such as sentiment analysis, key phrase extraction, topic modeling/extraction, aspect extraction and more.</span><span class="sxs-lookup"><span data-stu-id="5002c-105">Understanding and analyzing unstructured text is an increasingly popular field and includes a wide spectrum of problems such as sentiment analysis, key phrase extraction, topic modeling/extraction, aspect extraction and more.</span></span>

<span data-ttu-id="5002c-106">Text Analytics API is a suite of text analytics services built with Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="5002c-106">Text Analytics API is a suite of text analytics services built with Azure Machine Learning.</span></span> <span data-ttu-id="5002c-107">We currently offer APIs for sentiment analysis, key phrase extraction and topic detection for English text, as well as language detection for 120 languages.In this initial preview release, we offer APIs for sentiment analysis and key phrase extraction of English text.</span><span class="sxs-lookup"><span data-stu-id="5002c-107">We currently offer APIs for sentiment analysis, key phrase extraction and topic detection for English text, as well as language detection for 120 languages.In this initial preview release, we offer APIs for sentiment analysis and key phrase extraction of English text.</span></span> <span data-ttu-id="5002c-108">No labeled or training data is needed to use the service - just bring your text data.</span><span class="sxs-lookup"><span data-stu-id="5002c-108">No labeled or training data is needed to use the service - just bring your text data.</span></span> <span data-ttu-id="5002c-109">This service is based on research and engineering that originated in Microsoft Research and which has been battle-tested and improved over the past few years by product teams such as Bing and Office.</span><span class="sxs-lookup"><span data-stu-id="5002c-109">This service is based on research and engineering that originated in Microsoft Research and which has been battle-tested and improved over the past few years by product teams such as Bing and Office.</span></span>

<span data-ttu-id="5002c-110">**Sentiment Analysis**</span><span class="sxs-lookup"><span data-stu-id="5002c-110">**Sentiment Analysis**</span></span>

<span data-ttu-id="5002c-111">Let's say you run a website to sell handicrafts.</span><span class="sxs-lookup"><span data-stu-id="5002c-111">Let's say you run a website to sell handicrafts.</span></span> <span data-ttu-id="5002c-112">Your users submit feedback on your site, and you'd like to find out what users think of your brand, and how that changes over time as you release new products and features to your site.</span><span class="sxs-lookup"><span data-stu-id="5002c-112">Your users submit feedback on your site, and you'd like to find out what users think of your brand, and how that changes over time as you release new products and features to your site.</span></span> <span data-ttu-id="5002c-113">Sentiment analysis can help here - given a piece of text, the Azure ML Text Analytics service returns a score between 0 and 1 denoting overall sentiment in the input text.</span><span class="sxs-lookup"><span data-stu-id="5002c-113">Sentiment analysis can help here - given a piece of text, the Azure ML Text Analytics service returns a score between 0 and 1 denoting overall sentiment in the input text.</span></span> <span data-ttu-id="5002c-114">Scores close to 1 indicate positive sentiment, while scores close to 0 indicate negative sentiment.</span><span class="sxs-lookup"><span data-stu-id="5002c-114">Scores close to 1 indicate positive sentiment, while scores close to 0 indicate negative sentiment.</span></span>

<span data-ttu-id="5002c-115">Sentiment score is generated using classification techniques.</span><span class="sxs-lookup"><span data-stu-id="5002c-115">Sentiment score is generated using classification techniques.</span></span> <span data-ttu-id="5002c-116">The input features to the classifier include n-grams, features generated from part-of-speech tags, and embedded words.</span><span class="sxs-lookup"><span data-stu-id="5002c-116">The input features to the classifier include n-grams, features generated from part-of-speech tags, and embedded words.</span></span> <span data-ttu-id="5002c-117">The classifier was trained in part using Sentiment140 data.</span><span class="sxs-lookup"><span data-stu-id="5002c-117">The classifier was trained in part using Sentiment140 data.</span></span>

<span data-ttu-id="5002c-118">**Key Phrase Extraction**</span><span class="sxs-lookup"><span data-stu-id="5002c-118">**Key Phrase Extraction**</span></span>

<span data-ttu-id="5002c-119">This service can also extract key phrases, which denote the main talking points in the text.</span><span class="sxs-lookup"><span data-stu-id="5002c-119">This service can also extract key phrases, which denote the main talking points in the text.</span></span> <span data-ttu-id="5002c-120">We employ techniques from Microsoft Office's sophisticated Natural Language Processing toolkit.</span><span class="sxs-lookup"><span data-stu-id="5002c-120">We employ techniques from Microsoft Office's sophisticated Natural Language Processing toolkit.</span></span>

<span data-ttu-id="5002c-121">For example, for the input text ‘The manual transmission is a bit twitchy.</span><span class="sxs-lookup"><span data-stu-id="5002c-121">For example, for the input text ‘The manual transmission is a bit twitchy.</span></span> <span data-ttu-id="5002c-122">Also, the vehicle is old-school’, the service would return the main talking points: ‘manual transmission’, ‘vehicle’ and ‘old-school’.</span><span class="sxs-lookup"><span data-stu-id="5002c-122">Also, the vehicle is old-school’, the service would return the main talking points: ‘manual transmission’, ‘vehicle’ and ‘old-school’.</span></span>

<span data-ttu-id="5002c-123">**Topic Detection**</span><span class="sxs-lookup"><span data-stu-id="5002c-123">**Topic Detection**</span></span>

<span data-ttu-id="5002c-124">This is a new service which returns the topics which have been detected in multiple text articles.</span><span class="sxs-lookup"><span data-stu-id="5002c-124">This is a new service which returns the topics which have been detected in multiple text articles.</span></span> <span data-ttu-id="5002c-125">The service is designed to work well for short, human written text such as reviews and user feedback, and can help you to understand the main issues or suggestions that customers are mentioning.</span><span class="sxs-lookup"><span data-stu-id="5002c-125">The service is designed to work well for short, human written text such as reviews and user feedback, and can help you to understand the main issues or suggestions that customers are mentioning.</span></span>

<span data-ttu-id="5002c-126">**Language Detection**</span><span class="sxs-lookup"><span data-stu-id="5002c-126">**Language Detection**</span></span>

<span data-ttu-id="5002c-127">The service can be used to detect which language the input text is written in.</span><span class="sxs-lookup"><span data-stu-id="5002c-127">The service can be used to detect which language the input text is written in.</span></span>



