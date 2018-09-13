---
title: Test your LUIS app - Azure | Microsoft Docs
description: Use Language Understanding (LUIS) to continuously work on your application to refine it and improve its language understanding.
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: article
ms.date: 03/14/2018
ms.author: diberry
ms.openlocfilehash: fc84af35cc9ce9f8a4c2f67fade13d0c0e8ac6b9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869385"
---
# <a name="testing-in-luis"></a><span data-ttu-id="c7614-103">Testing in LUIS</span><span class="sxs-lookup"><span data-stu-id="c7614-103">Testing in LUIS</span></span>

<span data-ttu-id="c7614-104">Testing is the process of providing sample utterances to LUIS and getting a response of LUIS-recognized intents and entities.</span><span class="sxs-lookup"><span data-stu-id="c7614-104">Testing is the process of providing sample utterances to LUIS and getting a response of LUIS-recognized intents and entities.</span></span> 

<span data-ttu-id="c7614-105">You can [test](luis-interactive-test.md) LUIS interactively, one utterance at a time, or provide a [batch](luis-concept-batch-test.md) of utterances.</span><span class="sxs-lookup"><span data-stu-id="c7614-105">You can [test](luis-interactive-test.md) LUIS interactively, one utterance at a time, or provide a [batch](luis-concept-batch-test.md) of utterances.</span></span> <span data-ttu-id="c7614-106">With testing, you compare the current [active](luis-concept-version.md#active-version) model to the published model.</span><span class="sxs-lookup"><span data-stu-id="c7614-106">With testing, you compare the current [active](luis-concept-version.md#active-version) model to the published model.</span></span> 

<a name="A-test-score"></a>
<a name="Score-all-intents"></a>
<a name="E-(exponent)-notation"></a>
## <a name="what-is-a-score-in-testing"></a><span data-ttu-id="c7614-107">What is a score in testing?</span><span class="sxs-lookup"><span data-stu-id="c7614-107">What is a score in testing?</span></span>
<span data-ttu-id="c7614-108">See [Prediction score](luis-concept-prediction-score.md) concepts to learn more about prediction scores.</span><span class="sxs-lookup"><span data-stu-id="c7614-108">See [Prediction score](luis-concept-prediction-score.md) concepts to learn more about prediction scores.</span></span>

## <a name="interactive-testing"></a><span data-ttu-id="c7614-109">Interactive testing</span><span class="sxs-lookup"><span data-stu-id="c7614-109">Interactive testing</span></span>
<span data-ttu-id="c7614-110">Interactive testing is done from the **Test** panel of the website.</span><span class="sxs-lookup"><span data-stu-id="c7614-110">Interactive testing is done from the **Test** panel of the website.</span></span> <span data-ttu-id="c7614-111">You can enter an utterance to see how intents and entities are identified and scored.</span><span class="sxs-lookup"><span data-stu-id="c7614-111">You can enter an utterance to see how intents and entities are identified and scored.</span></span> <span data-ttu-id="c7614-112">If LUIS isn't predicting the intents and entities as you expect on an utterance in the testing pane, copy it to the **Intent** page as a new utterance.</span><span class="sxs-lookup"><span data-stu-id="c7614-112">If LUIS isn't predicting the intents and entities as you expect on an utterance in the testing pane, copy it to the **Intent** page as a new utterance.</span></span> <span data-ttu-id="c7614-113">Then label the parts of that utterance, and train LUIS.</span><span class="sxs-lookup"><span data-stu-id="c7614-113">Then label the parts of that utterance, and train LUIS.</span></span> 

## <a name="batch-testing"></a><span data-ttu-id="c7614-114">Batch testing</span><span class="sxs-lookup"><span data-stu-id="c7614-114">Batch testing</span></span>
<span data-ttu-id="c7614-115">See [batch testing](luis-concept-batch-test.md) if you are testing more than one utterance at a time.</span><span class="sxs-lookup"><span data-stu-id="c7614-115">See [batch testing](luis-concept-batch-test.md) if you are testing more than one utterance at a time.</span></span>

## <a name="endpoint-testing"></a><span data-ttu-id="c7614-116">Endpoint testing</span><span class="sxs-lookup"><span data-stu-id="c7614-116">Endpoint testing</span></span>
<span data-ttu-id="c7614-117">You can test using the [endpoint](luis-glossary.md#endpoint) with a maximum of two versions of your app.</span><span class="sxs-lookup"><span data-stu-id="c7614-117">You can test using the [endpoint](luis-glossary.md#endpoint) with a maximum of two versions of your app.</span></span> <span data-ttu-id="c7614-118">With your main or live version of your app set as the **production** endpoint, add a second version to the **staging** endpoint.</span><span class="sxs-lookup"><span data-stu-id="c7614-118">With your main or live version of your app set as the **production** endpoint, add a second version to the **staging** endpoint.</span></span> <span data-ttu-id="c7614-119">This approach gives you three versions of an utterance: the current model in the Test pane of the [LUIS](luis-reference-regions.md) website, and the two versions at the two different endpoints.</span><span class="sxs-lookup"><span data-stu-id="c7614-119">This approach gives you three versions of an utterance: the current model in the Test pane of the [LUIS](luis-reference-regions.md) website, and the two versions at the two different endpoints.</span></span> 

<span data-ttu-id="c7614-120">All endpoint testing counts toward your usage quota.</span><span class="sxs-lookup"><span data-stu-id="c7614-120">All endpoint testing counts toward your usage quota.</span></span> 

## <a name="do-not-log-tests"></a><span data-ttu-id="c7614-121">Do not log tests</span><span class="sxs-lookup"><span data-stu-id="c7614-121">Do not log tests</span></span>
<span data-ttu-id="c7614-122">If you test against an endpoint, and do not want the utterance logged, remember to use the `logging=false` query string configuration.</span><span class="sxs-lookup"><span data-stu-id="c7614-122">If you test against an endpoint, and do not want the utterance logged, remember to use the `logging=false` query string configuration.</span></span>

## <a name="where-to-find-utterances"></a><span data-ttu-id="c7614-123">Where to find utterances</span><span class="sxs-lookup"><span data-stu-id="c7614-123">Where to find utterances</span></span>
<span data-ttu-id="c7614-124">LUIS stores all logged utterances in the query log, available for download on the [LUIS](luis-reference-regions.md) website **Apps** list page, as well as the LUIS [authoring APIs](https://aka.ms/luis-authoring-apis).</span><span class="sxs-lookup"><span data-stu-id="c7614-124">LUIS stores all logged utterances in the query log, available for download on the [LUIS](luis-reference-regions.md) website **Apps** list page, as well as the LUIS [authoring APIs](https://aka.ms/luis-authoring-apis).</span></span> 

<span data-ttu-id="c7614-125">Any utterances LUIS is unsure of are listed in the **[Review endpoint utterances](luis-how-to-review-endoint-utt.md)** page of the [LUIS](luis-reference-regions.md) website.</span><span class="sxs-lookup"><span data-stu-id="c7614-125">Any utterances LUIS is unsure of are listed in the **[Review endpoint utterances](luis-how-to-review-endoint-utt.md)** page of the [LUIS](luis-reference-regions.md) website.</span></span> 

![Review endpoint utterances](./media/luis-concept-test/review-endpoint-utterances.png)
 
## <a name="remember-to-train"></a><span data-ttu-id="c7614-127">Remember to train</span><span class="sxs-lookup"><span data-stu-id="c7614-127">Remember to train</span></span>
<span data-ttu-id="c7614-128">Remember to [train](luis-how-to-train.md) LUIS after you make changes to the model.</span><span class="sxs-lookup"><span data-stu-id="c7614-128">Remember to [train](luis-how-to-train.md) LUIS after you make changes to the model.</span></span> <span data-ttu-id="c7614-129">Changes to the LUIS app are not seen in testing until the app is trained.</span><span class="sxs-lookup"><span data-stu-id="c7614-129">Changes to the LUIS app are not seen in testing until the app is trained.</span></span> 

## <a name="best-practices"></a><span data-ttu-id="c7614-130">Best practices</span><span class="sxs-lookup"><span data-stu-id="c7614-130">Best practices</span></span>
<span data-ttu-id="c7614-131">Learn [best practices](luis-concept-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="c7614-131">Learn [best practices](luis-concept-best-practices.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c7614-132">Next steps</span><span class="sxs-lookup"><span data-stu-id="c7614-132">Next steps</span></span>

* <span data-ttu-id="c7614-133">Learn more about [testing](luis-interactive-test.md) your utterances.</span><span class="sxs-lookup"><span data-stu-id="c7614-133">Learn more about [testing](luis-interactive-test.md) your utterances.</span></span>