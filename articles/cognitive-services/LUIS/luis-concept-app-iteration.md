---
title: Understand LUIS iterative app design - Language Understanding
description: LUIS learns best in an iterative cycle of model changes, utterance examples, publishing, and gathering data from endpoint queries.  LUIS apps require design iterations to train LUIS to get the best data extraction.
titleSuffix: Azure Cognitive Services
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: article
ms.date: 02/12/2018
ms.author: diberry
ms.openlocfilehash: 7c267d53c9057ac05427ff14a7e3c25d56ab1f62
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866923"
---
# <a name="authoring-cycle"></a><span data-ttu-id="c40db-104">Authoring cycle</span><span class="sxs-lookup"><span data-stu-id="c40db-104">Authoring cycle</span></span>
<span data-ttu-id="c40db-105">LUIS learns best in an iterative cycle of model changes, utterance examples, publishing, and gathering data from endpoint queries.</span><span class="sxs-lookup"><span data-stu-id="c40db-105">LUIS learns best in an iterative cycle of model changes, utterance examples, publishing, and gathering data from endpoint queries.</span></span> 

![Authoring cycle](./media/luis-concept-app-iteration/iteration.png)

## <a name="building-a-luis-model"></a><span data-ttu-id="c40db-107">Building a LUIS model</span><span class="sxs-lookup"><span data-stu-id="c40db-107">Building a LUIS model</span></span>
<span data-ttu-id="c40db-108">The model's purpose is to figure out what the user is asking for (the intention or intent) and what parts of the question provide details (entities) that help determine the answer.</span><span class="sxs-lookup"><span data-stu-id="c40db-108">The model's purpose is to figure out what the user is asking for (the intention or intent) and what parts of the question provide details (entities) that help determine the answer.</span></span> 

<span data-ttu-id="c40db-109">The model needs to be specific to the app domain in order to determine words and phrases that are relevant as well as typical word ordering.</span><span class="sxs-lookup"><span data-stu-id="c40db-109">The model needs to be specific to the app domain in order to determine words and phrases that are relevant as well as typical word ordering.</span></span> 

<span data-ttu-id="c40db-110">The model includes intent, entities.</span><span class="sxs-lookup"><span data-stu-id="c40db-110">The model includes intent, entities.</span></span> 

## <a name="add-training-examples"></a><span data-ttu-id="c40db-111">Add training examples</span><span class="sxs-lookup"><span data-stu-id="c40db-111">Add training examples</span></span>
<span data-ttu-id="c40db-112">LUIS needs example utterances in the intents.</span><span class="sxs-lookup"><span data-stu-id="c40db-112">LUIS needs example utterances in the intents.</span></span> <span data-ttu-id="c40db-113">The examples need enough variation of word choice and word order to be able to determine which intent the utterance is meant for.</span><span class="sxs-lookup"><span data-stu-id="c40db-113">The examples need enough variation of word choice and word order to be able to determine which intent the utterance is meant for.</span></span> <span data-ttu-id="c40db-114">Each example utterance needs to have any required data labeled as entities.</span><span class="sxs-lookup"><span data-stu-id="c40db-114">Each example utterance needs to have any required data labeled as entities.</span></span> 

<span data-ttu-id="c40db-115">You instruct LUIS to ignore utterances that are not relevant to your app's domain by assigning the utterance to the **None** intent.</span><span class="sxs-lookup"><span data-stu-id="c40db-115">You instruct LUIS to ignore utterances that are not relevant to your app's domain by assigning the utterance to the **None** intent.</span></span> <span data-ttu-id="c40db-116">Any words or phrases you do not need pulled out of an utterance do not need to be labeled.</span><span class="sxs-lookup"><span data-stu-id="c40db-116">Any words or phrases you do not need pulled out of an utterance do not need to be labeled.</span></span> <span data-ttu-id="c40db-117">There is no label for words or phrases to ignore.</span><span class="sxs-lookup"><span data-stu-id="c40db-117">There is no label for words or phrases to ignore.</span></span> 
<!--
## Not just yet
Do not add features such as a [phrase list](luis-concept-feature.md) feature in your first cycle. Phrase lists are phrases that would be specific to your app's subject area.  
-->
## <a name="train-and-publish-the-app"></a><span data-ttu-id="c40db-118">Train and publish the app</span><span class="sxs-lookup"><span data-stu-id="c40db-118">Train and publish the app</span></span>
<span data-ttu-id="c40db-119">Once you have 10 to 15 different utterances in each intent, with the required entities labeled, you train LUIS, then publish to get your endpoints.</span><span class="sxs-lookup"><span data-stu-id="c40db-119">Once you have 10 to 15 different utterances in each intent, with the required entities labeled, you train LUIS, then publish to get your endpoints.</span></span> <span data-ttu-id="c40db-120">Make sure to create your app and publish your app so that it is available in the [endpoint regions](luis-reference-regions.md) you need.</span><span class="sxs-lookup"><span data-stu-id="c40db-120">Make sure to create your app and publish your app so that it is available in the [endpoint regions](luis-reference-regions.md) you need.</span></span> 

## <a name="https-endpoint-testing"></a><span data-ttu-id="c40db-121">HTTPS endpoint testing</span><span class="sxs-lookup"><span data-stu-id="c40db-121">HTTPS endpoint testing</span></span>
<span data-ttu-id="c40db-122">You can test your LUIS app from the HTTPS endpoint listed on the **[Publish](luis-how-to-publish-app.md)** page.</span><span class="sxs-lookup"><span data-stu-id="c40db-122">You can test your LUIS app from the HTTPS endpoint listed on the **[Publish](luis-how-to-publish-app.md)** page.</span></span> <span data-ttu-id="c40db-123">Testing from the endpoint allows LUIS to choose any utterances with low-confidence for review.</span><span class="sxs-lookup"><span data-stu-id="c40db-123">Testing from the endpoint allows LUIS to choose any utterances with low-confidence for review.</span></span>  

## <a name="recycle"></a><span data-ttu-id="c40db-124">Recycle</span><span class="sxs-lookup"><span data-stu-id="c40db-124">Recycle</span></span>
<span data-ttu-id="c40db-125">When you are done with a cycle of authoring, you can begin again.</span><span class="sxs-lookup"><span data-stu-id="c40db-125">When you are done with a cycle of authoring, you can begin again.</span></span> <span data-ttu-id="c40db-126">Start with reviewing endpoint utterances LUIS marked with low-confidence.</span><span class="sxs-lookup"><span data-stu-id="c40db-126">Start with reviewing endpoint utterances LUIS marked with low-confidence.</span></span> <span data-ttu-id="c40db-127">Check these utterances for both intent and entity.</span><span class="sxs-lookup"><span data-stu-id="c40db-127">Check these utterances for both intent and entity.</span></span> <span data-ttu-id="c40db-128">Once you review utterances, the review list should be empty.</span><span class="sxs-lookup"><span data-stu-id="c40db-128">Once you review utterances, the review list should be empty.</span></span>  

## <a name="batch-testing"></a><span data-ttu-id="c40db-129">Batch testing</span><span class="sxs-lookup"><span data-stu-id="c40db-129">Batch testing</span></span>
<span data-ttu-id="c40db-130">Batch testing is a way to see how many example utterances are scored by LUIS.</span><span class="sxs-lookup"><span data-stu-id="c40db-130">Batch testing is a way to see how many example utterances are scored by LUIS.</span></span> <span data-ttu-id="c40db-131">The examples should be new to LUIS and should be correctly labeled with intent and entities you want LUIS to find.</span><span class="sxs-lookup"><span data-stu-id="c40db-131">The examples should be new to LUIS and should be correctly labeled with intent and entities you want LUIS to find.</span></span> <span data-ttu-id="c40db-132">The test results indicate how well LUIS would perform on that set of utterances.</span><span class="sxs-lookup"><span data-stu-id="c40db-132">The test results indicate how well LUIS would perform on that set of utterances.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="c40db-133">Next steps</span><span class="sxs-lookup"><span data-stu-id="c40db-133">Next steps</span></span>

<span data-ttu-id="c40db-134">Learn concepts about [collaboration](luis-concept-collaborator.md).</span><span class="sxs-lookup"><span data-stu-id="c40db-134">Learn concepts about [collaboration](luis-concept-collaborator.md).</span></span>