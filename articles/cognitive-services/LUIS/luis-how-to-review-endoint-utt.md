---
title: Review endpoint utterances  for Language Understanding (LUIS)
titleSuffix: Azure Cognitive Services
description: The breakthrough feature of LUIS is the concept of active learning. Once your LUIS has endpoint queries, active learning improves the quality of the results by selects utterances that it is unsure of. If you label these utterances, train, and publish, then LUIS identifies utterances more accurately.
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: article
ms.date: 09/06/2018
ms.author: diberry
ms.openlocfilehash: 3ec791d534fb73a9d88f2dcdb81e445d6c26ab69
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868682"
---
# <a name="review-endpoint-utterances"></a><span data-ttu-id="8a87a-105">Review endpoint utterances</span><span class="sxs-lookup"><span data-stu-id="8a87a-105">Review endpoint utterances</span></span>

<span data-ttu-id="8a87a-106">The breakthrough feature of LUIS is the [concept](luis-concept-review-endpoint-utterances.md) of active learning.</span><span class="sxs-lookup"><span data-stu-id="8a87a-106">The breakthrough feature of LUIS is the [concept](luis-concept-review-endpoint-utterances.md) of active learning.</span></span> <span data-ttu-id="8a87a-107">Once your LUIS has endpoint queries, LUIS uses active learning to improve the quality of the results.</span><span class="sxs-lookup"><span data-stu-id="8a87a-107">Once your LUIS has endpoint queries, LUIS uses active learning to improve the quality of the results.</span></span> <span data-ttu-id="8a87a-108">In the active learning process, LUIS examines all the endpoint utterances, and selects utterances that it is unsure of.</span><span class="sxs-lookup"><span data-stu-id="8a87a-108">In the active learning process, LUIS examines all the endpoint utterances, and selects utterances that it is unsure of.</span></span> <span data-ttu-id="8a87a-109">If you label these utterances, train, and publish, then LUIS identifies utterances more accurately.</span><span class="sxs-lookup"><span data-stu-id="8a87a-109">If you label these utterances, train, and publish, then LUIS identifies utterances more accurately.</span></span> 

## <a name="filter-utterances"></a><span data-ttu-id="8a87a-110">Filter utterances</span><span class="sxs-lookup"><span data-stu-id="8a87a-110">Filter utterances</span></span>
1. <span data-ttu-id="8a87a-111">Open your app (for example, TravelAgent) by selecting its name on **My Apps** page, then select **Build** in the top bar.</span><span class="sxs-lookup"><span data-stu-id="8a87a-111">Open your app (for example, TravelAgent) by selecting its name on **My Apps** page, then select **Build** in the top bar.</span></span>

2. <span data-ttu-id="8a87a-112">Under the **Improve app performance**, select **Review endpoint utterances**.</span><span class="sxs-lookup"><span data-stu-id="8a87a-112">Under the **Improve app performance**, select **Review endpoint utterances**.</span></span>

3. <span data-ttu-id="8a87a-113">On the **Review endpoint utterances** page, select in the **Filter list by intent or entity** text box.</span><span class="sxs-lookup"><span data-stu-id="8a87a-113">On the **Review endpoint utterances** page, select in the **Filter list by intent or entity** text box.</span></span> <span data-ttu-id="8a87a-114">This drop-down list includes all intents under **INTENTS** and all entities under **ENTITIES**.</span><span class="sxs-lookup"><span data-stu-id="8a87a-114">This drop-down list includes all intents under **INTENTS** and all entities under **ENTITIES**.</span></span>

    ![Utterances filter](./media/label-suggested-utterances/filter.png)

4. <span data-ttu-id="8a87a-116">Select a category (intents or entities) in the drop-down list and review the utterances.</span><span class="sxs-lookup"><span data-stu-id="8a87a-116">Select a category (intents or entities) in the drop-down list and review the utterances.</span></span>

    ![Intent utterances](./media/label-suggested-utterances/intent-utterances.png)

## <a name="label-entities"></a><span data-ttu-id="8a87a-118">Label entities</span><span class="sxs-lookup"><span data-stu-id="8a87a-118">Label entities</span></span>
<span data-ttu-id="8a87a-119">LUIS replaces entity tokens (words) with entity names highlighted in blue.</span><span class="sxs-lookup"><span data-stu-id="8a87a-119">LUIS replaces entity tokens (words) with entity names highlighted in blue.</span></span> <span data-ttu-id="8a87a-120">If an utterance has unlabeled entities, label them in the utterance.</span><span class="sxs-lookup"><span data-stu-id="8a87a-120">If an utterance has unlabeled entities, label them in the utterance.</span></span> 

1. <span data-ttu-id="8a87a-121">Select on the word(s) in the utterance.</span><span class="sxs-lookup"><span data-stu-id="8a87a-121">Select on the word(s) in the utterance.</span></span> 

2. <span data-ttu-id="8a87a-122">Select an entity from the list.</span><span class="sxs-lookup"><span data-stu-id="8a87a-122">Select an entity from the list.</span></span>

    ![Label entity](./media/label-suggested-utterances/label-entity.png)

## <a name="align-single-utterance"></a><span data-ttu-id="8a87a-124">Align single utterance</span><span class="sxs-lookup"><span data-stu-id="8a87a-124">Align single utterance</span></span>

<span data-ttu-id="8a87a-125">Each utterance has a suggested intent displayed in the **Aligned intent** column.</span><span class="sxs-lookup"><span data-stu-id="8a87a-125">Each utterance has a suggested intent displayed in the **Aligned intent** column.</span></span> 

1. <span data-ttu-id="8a87a-126">If you agree with that suggestion, select on the check mark.</span><span class="sxs-lookup"><span data-stu-id="8a87a-126">If you agree with that suggestion, select on the check mark.</span></span>

    ![Keep aligned intent](./media/label-suggested-utterances/align-intent-check.png)

2. <span data-ttu-id="8a87a-128">If you disagree with the suggestion, select the correct intent from the aligned intent drop-down list, then select on the check mark to the right of the aligned intent.</span><span class="sxs-lookup"><span data-stu-id="8a87a-128">If you disagree with the suggestion, select the correct intent from the aligned intent drop-down list, then select on the check mark to the right of the aligned intent.</span></span> 

    ![Align intent](./media/label-suggested-utterances/align-intent.png)

3. <span data-ttu-id="8a87a-130">After you select on the check mark, the utterance is removed from the list.</span><span class="sxs-lookup"><span data-stu-id="8a87a-130">After you select on the check mark, the utterance is removed from the list.</span></span> 

## <a name="align-several-utterances"></a><span data-ttu-id="8a87a-131">Align several utterances</span><span class="sxs-lookup"><span data-stu-id="8a87a-131">Align several utterances</span></span>

<span data-ttu-id="8a87a-132">To align several utterances, check the box to the left of the utterances, then select on the **Add selected** button.</span><span class="sxs-lookup"><span data-stu-id="8a87a-132">To align several utterances, check the box to the left of the utterances, then select on the **Add selected** button.</span></span> 

![Align several](./media/label-suggested-utterances/add-selected.png)

## <a name="verify-aligned-intent"></a><span data-ttu-id="8a87a-134">Verify aligned intent</span><span class="sxs-lookup"><span data-stu-id="8a87a-134">Verify aligned intent</span></span>
<span data-ttu-id="8a87a-135">You can verify the utterance was aligned with the correct intent by going to the **Intents** page, select the intent name, and reviewing the utterances.</span><span class="sxs-lookup"><span data-stu-id="8a87a-135">You can verify the utterance was aligned with the correct intent by going to the **Intents** page, select the intent name, and reviewing the utterances.</span></span> <span data-ttu-id="8a87a-136">The utterance from **Review endpoint utterances** is in the list.</span><span class="sxs-lookup"><span data-stu-id="8a87a-136">The utterance from **Review endpoint utterances** is in the list.</span></span>

## <a name="delete-utterance"></a><span data-ttu-id="8a87a-137">Delete utterance</span><span class="sxs-lookup"><span data-stu-id="8a87a-137">Delete utterance</span></span>
<span data-ttu-id="8a87a-138">Each utterance can be deleted from the review list.</span><span class="sxs-lookup"><span data-stu-id="8a87a-138">Each utterance can be deleted from the review list.</span></span> <span data-ttu-id="8a87a-139">Once deleted, it will not appear in the list again.</span><span class="sxs-lookup"><span data-stu-id="8a87a-139">Once deleted, it will not appear in the list again.</span></span> <span data-ttu-id="8a87a-140">This is true even if the user enters the same utterance from the endpoint.</span><span class="sxs-lookup"><span data-stu-id="8a87a-140">This is true even if the user enters the same utterance from the endpoint.</span></span> 

<span data-ttu-id="8a87a-141">If you are unsure if you should delete the utterance, either move it to the None intent, or create a new intent such as "miscellaneous" and move the utterance to that intent.</span><span class="sxs-lookup"><span data-stu-id="8a87a-141">If you are unsure if you should delete the utterance, either move it to the None intent, or create a new intent such as "miscellaneous" and move the utterance to that intent.</span></span> 

## <a name="delete-several-utterances"></a><span data-ttu-id="8a87a-142">Delete several utterances</span><span class="sxs-lookup"><span data-stu-id="8a87a-142">Delete several utterances</span></span>
<span data-ttu-id="8a87a-143">To delete several utterances, select each item and select on the trash bin to the right of the **Add selected** button.</span><span class="sxs-lookup"><span data-stu-id="8a87a-143">To delete several utterances, select each item and select on the trash bin to the right of the **Add selected** button.</span></span>

![Delete several](./media/label-suggested-utterances/delete-several.png)

## <a name="next-steps"></a><span data-ttu-id="8a87a-145">Next steps</span><span class="sxs-lookup"><span data-stu-id="8a87a-145">Next steps</span></span>

<span data-ttu-id="8a87a-146">To test how performance improves after you label suggested utterances, you can access the test console by selecting **Test** in the top panel.</span><span class="sxs-lookup"><span data-stu-id="8a87a-146">To test how performance improves after you label suggested utterances, you can access the test console by selecting **Test** in the top panel.</span></span> <span data-ttu-id="8a87a-147">For instructions on how to test your app using the test console, see [Train and test your app](luis-interactive-test.md).</span><span class="sxs-lookup"><span data-stu-id="8a87a-147">For instructions on how to test your app using the test console, see [Train and test your app](luis-interactive-test.md).</span></span>
