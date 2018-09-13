---
title: Frequently Asked Questions about the Text Analytics API - Azure Cognitive Services | Microsoft Docs
description: Get answers to common questions about Microsoft Cognitive Services Text Analytics API on Azure.
services: cognitive-services
author: HeidiSteen
manager: cgronlun
ms.service: cognitive-services
ms.component: text-analytics
ms.topic: conceptual
ms.date: 3/07/2018
ms.author: heidist
ms.openlocfilehash: bf82899b4317f0f5ce0f6ca5096dccef7cddd931
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870605"
---
# <a name="frequently-asked-questions-faq-about-the-text-analytics-api"></a><span data-ttu-id="c0b22-103">Frequently Asked Questions (FAQ) about the Text Analytics API</span><span class="sxs-lookup"><span data-stu-id="c0b22-103">Frequently Asked Questions (FAQ) about the Text Analytics API</span></span>

 <span data-ttu-id="c0b22-104">Find answers to commonly asked questions about concepts, code, and scenarios related to the Text Analytics API for Microsoft Cognitive Services on Azure.</span><span class="sxs-lookup"><span data-stu-id="c0b22-104">Find answers to commonly asked questions about concepts, code, and scenarios related to the Text Analytics API for Microsoft Cognitive Services on Azure.</span></span>

## <a name="can-text-analytics-identify-sarcasm"></a><span data-ttu-id="c0b22-105">Can Text Analytics identify sarcasm?</span><span class="sxs-lookup"><span data-stu-id="c0b22-105">Can Text Analytics identify sarcasm?</span></span>

<span data-ttu-id="c0b22-106">Analysis is for positive-negative sentiment rather than mood detection.</span><span class="sxs-lookup"><span data-stu-id="c0b22-106">Analysis is for positive-negative sentiment rather than mood detection.</span></span>

<span data-ttu-id="c0b22-107">There is always some degree of imprecision in sentiment analysis, but the model is most useful when there is no hidden meaning or subtext to the content.</span><span class="sxs-lookup"><span data-stu-id="c0b22-107">There is always some degree of imprecision in sentiment analysis, but the model is most useful when there is no hidden meaning or subtext to the content.</span></span> <span data-ttu-id="c0b22-108">Irony, sarcasm, humor, and similarly nuanced content rely on cultural context and norms to convey intent.</span><span class="sxs-lookup"><span data-stu-id="c0b22-108">Irony, sarcasm, humor, and similarly nuanced content rely on cultural context and norms to convey intent.</span></span> <span data-ttu-id="c0b22-109">This type of content is among the most challenging to analyze.</span><span class="sxs-lookup"><span data-stu-id="c0b22-109">This type of content is among the most challenging to analyze.</span></span> <span data-ttu-id="c0b22-110">Typically, the greatest discrepancy between a given score produced by the analyzer and a subjective assessment by a human is for content with nuanced meaning.</span><span class="sxs-lookup"><span data-stu-id="c0b22-110">Typically, the greatest discrepancy between a given score produced by the analyzer and a subjective assessment by a human is for content with nuanced meaning.</span></span>

## <a name="can-i-add-my-own-training-data-or-models"></a><span data-ttu-id="c0b22-111">Can I add my own training data or models?</span><span class="sxs-lookup"><span data-stu-id="c0b22-111">Can I add my own training data or models?</span></span>

<span data-ttu-id="c0b22-112">No, the models are pretrained.</span><span class="sxs-lookup"><span data-stu-id="c0b22-112">No, the models are pretrained.</span></span> <span data-ttu-id="c0b22-113">The only operations available on uploaded data are scoring, key phrase extraction, and language detection.</span><span class="sxs-lookup"><span data-stu-id="c0b22-113">The only operations available on uploaded data are scoring, key phrase extraction, and language detection.</span></span> <span data-ttu-id="c0b22-114">We do not host custom models.</span><span class="sxs-lookup"><span data-stu-id="c0b22-114">We do not host custom models.</span></span> <span data-ttu-id="c0b22-115">If you want to create and host custom machine learning models, consider the [machine learning capabilities in Microsoft R Server](https://docs.microsoft.com/r-server/r/concept-what-is-the-microsoftml-package).</span><span class="sxs-lookup"><span data-stu-id="c0b22-115">If you want to create and host custom machine learning models, consider the [machine learning capabilities in Microsoft R Server](https://docs.microsoft.com/r-server/r/concept-what-is-the-microsoftml-package).</span></span>

## <a name="can-i-request-additional-languages"></a><span data-ttu-id="c0b22-116">Can I request additional languages?</span><span class="sxs-lookup"><span data-stu-id="c0b22-116">Can I request additional languages?</span></span>

<span data-ttu-id="c0b22-117">Sentiment analysis and key phrase extraction are available for a [select number of languages](text-analytics-supported-languages.md).</span><span class="sxs-lookup"><span data-stu-id="c0b22-117">Sentiment analysis and key phrase extraction are available for a [select number of languages](text-analytics-supported-languages.md).</span></span> <span data-ttu-id="c0b22-118">Natural language processing is complex and requires substantial testing before new functionality can be released.</span><span class="sxs-lookup"><span data-stu-id="c0b22-118">Natural language processing is complex and requires substantial testing before new functionality can be released.</span></span> <span data-ttu-id="c0b22-119">For this reason, we avoid pre-announcing support so that no one takes a dependency on functionality that needs more time to mature.</span><span class="sxs-lookup"><span data-stu-id="c0b22-119">For this reason, we avoid pre-announcing support so that no one takes a dependency on functionality that needs more time to mature.</span></span> 

<span data-ttu-id="c0b22-120">To help us prioritize which languages to work on next, vote for specific languages on [User Voice](https://cognitive.uservoice.com/forums/555922-text-analytics).</span><span class="sxs-lookup"><span data-stu-id="c0b22-120">To help us prioritize which languages to work on next, vote for specific languages on [User Voice](https://cognitive.uservoice.com/forums/555922-text-analytics).</span></span> 

## <a name="why-does-key-phrase-extraction-return-some-words-but-not-others"></a><span data-ttu-id="c0b22-121">Why does key phrase extraction return some words but not others?</span><span class="sxs-lookup"><span data-stu-id="c0b22-121">Why does key phrase extraction return some words but not others?</span></span>

<span data-ttu-id="c0b22-122">Key phrase extraction eliminates non-essential words and standalone adjectives.</span><span class="sxs-lookup"><span data-stu-id="c0b22-122">Key phrase extraction eliminates non-essential words and standalone adjectives.</span></span> <span data-ttu-id="c0b22-123">Adjective-noun combinations, such as "spectacular views" or "foggy weather" are returned together.</span><span class="sxs-lookup"><span data-stu-id="c0b22-123">Adjective-noun combinations, such as "spectacular views" or "foggy weather" are returned together.</span></span>

<span data-ttu-id="c0b22-124">Generally, output consists of nouns and objects of the sentence.</span><span class="sxs-lookup"><span data-stu-id="c0b22-124">Generally, output consists of nouns and objects of the sentence.</span></span> <span data-ttu-id="c0b22-125">Output is listed in order of importance, with the first phrase being the most important.</span><span class="sxs-lookup"><span data-stu-id="c0b22-125">Output is listed in order of importance, with the first phrase being the most important.</span></span> <span data-ttu-id="c0b22-126">Importance is measured by the number of times a particular concept is mentioned, or the relation of that element to other elements in the text.</span><span class="sxs-lookup"><span data-stu-id="c0b22-126">Importance is measured by the number of times a particular concept is mentioned, or the relation of that element to other elements in the text.</span></span>

## <a name="why-does-output-vary-given-identical-inputs"></a><span data-ttu-id="c0b22-127">Why does output vary, given identical inputs?</span><span class="sxs-lookup"><span data-stu-id="c0b22-127">Why does output vary, given identical inputs?</span></span>

<span data-ttu-id="c0b22-128">Improvements to models and algorithms are announced if the change is major, or quietly slipstreamed into the service if the update is minor.</span><span class="sxs-lookup"><span data-stu-id="c0b22-128">Improvements to models and algorithms are announced if the change is major, or quietly slipstreamed into the service if the update is minor.</span></span> <span data-ttu-id="c0b22-129">Over time, you might find that the same text input results in a different sentiment score or key phrase output.</span><span class="sxs-lookup"><span data-stu-id="c0b22-129">Over time, you might find that the same text input results in a different sentiment score or key phrase output.</span></span> <span data-ttu-id="c0b22-130">This is a normal and intentional consequence of using managed machine learning resources in the cloud.</span><span class="sxs-lookup"><span data-stu-id="c0b22-130">This is a normal and intentional consequence of using managed machine learning resources in the cloud.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c0b22-131">Next steps</span><span class="sxs-lookup"><span data-stu-id="c0b22-131">Next steps</span></span>

<span data-ttu-id="c0b22-132">Is your question about a missing feature or functionality?</span><span class="sxs-lookup"><span data-stu-id="c0b22-132">Is your question about a missing feature or functionality?</span></span> <span data-ttu-id="c0b22-133">Consider requesting or voting for it on our [UserVoice web site](https://cognitive.uservoice.com/forums/555922-text-analytics).</span><span class="sxs-lookup"><span data-stu-id="c0b22-133">Consider requesting or voting for it on our [UserVoice web site](https://cognitive.uservoice.com/forums/555922-text-analytics).</span></span>

## <a name="see-also"></a><span data-ttu-id="c0b22-134">See also</span><span class="sxs-lookup"><span data-stu-id="c0b22-134">See also</span></span>

 <span data-ttu-id="c0b22-135">[StackOverflow: Text Analytics API](https://stackoverflow.com/questions/tagged/text-analytics-api) </span><span class="sxs-lookup"><span data-stu-id="c0b22-135">[StackOverflow: Text Analytics API](https://stackoverflow.com/questions/tagged/text-analytics-api) </span></span>  
 [<span data-ttu-id="c0b22-136">StackOverflow: Cognitive Services</span><span class="sxs-lookup"><span data-stu-id="c0b22-136">StackOverflow: Cognitive Services</span></span>](http://stackoverflow.com/questions/tagged/microsoft-cognitive)
