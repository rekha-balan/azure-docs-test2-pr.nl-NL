---
title: Add pattern templates instead of more utterances in LUIS apps
titleSuffix: Azure Cognitive Services
description: Learn how to add pattern templates in Language Understanding (LUIS) applications to improve prediction accuracy.
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.technology: luis
ms.topic: article
ms.date: 09/06/2018
ms.author: diberry
ms.openlocfilehash: 0fc7c0d0cafef1bdb8d33c6ebfaa672c55101ee5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868577"
---
# <a name="how-to-add-patterns-to-improve-prediction-accuracy"></a><span data-ttu-id="b9620-103">How to add Patterns to improve prediction accuracy</span><span class="sxs-lookup"><span data-stu-id="b9620-103">How to add Patterns to improve prediction accuracy</span></span>
<span data-ttu-id="b9620-104">After a LUIS app receives endpoint utterances, use the [concept](luis-concept-patterns.md) of Patterns to improve prediction accuracy for utterances that reveal a pattern in word order and word choice.</span><span class="sxs-lookup"><span data-stu-id="b9620-104">After a LUIS app receives endpoint utterances, use the [concept](luis-concept-patterns.md) of Patterns to improve prediction accuracy for utterances that reveal a pattern in word order and word choice.</span></span> <span data-ttu-id="b9620-105">Patterns use [entities](luis-concept-entity-types.md) and their roles to extract data using specific pattern syntax.</span><span class="sxs-lookup"><span data-stu-id="b9620-105">Patterns use [entities](luis-concept-entity-types.md) and their roles to extract data using specific pattern syntax.</span></span> 

## <a name="add-template-utterance-to-create-pattern"></a><span data-ttu-id="b9620-106">Add template utterance to create pattern</span><span class="sxs-lookup"><span data-stu-id="b9620-106">Add template utterance to create pattern</span></span>
1. <span data-ttu-id="b9620-107">Open your app by selecting its name on **My Apps** page, and then select **Patterns** in the left panel, under **Improve app performance**.</span><span class="sxs-lookup"><span data-stu-id="b9620-107">Open your app by selecting its name on **My Apps** page, and then select **Patterns** in the left panel, under **Improve app performance**.</span></span>

    ![Screenshot of Patterns List](./media/luis-how-to-model-intent-pattern/patterns-1.png)

2. <span data-ttu-id="b9620-109">Select the correct intent for the pattern.</span><span class="sxs-lookup"><span data-stu-id="b9620-109">Select the correct intent for the pattern.</span></span> 

    ![Select intent](./media/luis-how-to-model-intent-pattern/patterns-2.png)

3. <span data-ttu-id="b9620-111">In the template textbox, type the template utterance and select Enter.</span><span class="sxs-lookup"><span data-stu-id="b9620-111">In the template textbox, type the template utterance and select Enter.</span></span> <span data-ttu-id="b9620-112">When you want to enter the entity name, use the correct pattern entity syntax.</span><span class="sxs-lookup"><span data-stu-id="b9620-112">When you want to enter the entity name, use the correct pattern entity syntax.</span></span> <span data-ttu-id="b9620-113">Begin the entity syntax with `{`.</span><span class="sxs-lookup"><span data-stu-id="b9620-113">Begin the entity syntax with `{`.</span></span> <span data-ttu-id="b9620-114">The list of entities displays.</span><span class="sxs-lookup"><span data-stu-id="b9620-114">The list of entities displays.</span></span> <span data-ttu-id="b9620-115">Select the correct entity, and then select Enter.</span><span class="sxs-lookup"><span data-stu-id="b9620-115">Select the correct entity, and then select Enter.</span></span> 

    ![Screenshot of entity for pattern](./media/luis-how-to-model-intent-pattern/patterns-3.png)

    <span data-ttu-id="b9620-117">If your entity includes a role, indicate the role with a single colon, `:`, after the entity name, such as `{Location:Origin}`.</span><span class="sxs-lookup"><span data-stu-id="b9620-117">If your entity includes a role, indicate the role with a single colon, `:`, after the entity name, such as `{Location:Origin}`.</span></span> <span data-ttu-id="b9620-118">The list of roles for the entities displays in a list.</span><span class="sxs-lookup"><span data-stu-id="b9620-118">The list of roles for the entities displays in a list.</span></span> <span data-ttu-id="b9620-119">Select the role, and then select Enter.</span><span class="sxs-lookup"><span data-stu-id="b9620-119">Select the role, and then select Enter.</span></span> 

    ![Screenshot of entity with role](./media/luis-how-to-model-intent-pattern/patterns-4.png)

    <span data-ttu-id="b9620-121">After you select the correct entity, finish entering the pattern, and then select Enter.</span><span class="sxs-lookup"><span data-stu-id="b9620-121">After you select the correct entity, finish entering the pattern, and then select Enter.</span></span> <span data-ttu-id="b9620-122">When you are done entering patterns, [train](luis-how-to-train.md) your app.</span><span class="sxs-lookup"><span data-stu-id="b9620-122">When you are done entering patterns, [train](luis-how-to-train.md) your app.</span></span>

    ![Screenshot of entered pattern with both types of entities](./media/luis-how-to-model-intent-pattern/patterns-5.png)

## <a name="search-patterns"></a><span data-ttu-id="b9620-124">Search patterns</span><span class="sxs-lookup"><span data-stu-id="b9620-124">Search patterns</span></span>
<span data-ttu-id="b9620-125">Searching allows you to find patterns that contain some given text.</span><span class="sxs-lookup"><span data-stu-id="b9620-125">Searching allows you to find patterns that contain some given text.</span></span>  

1. <span data-ttu-id="b9620-126">Select the magnifying glass icon.</span><span class="sxs-lookup"><span data-stu-id="b9620-126">Select the magnifying glass icon.</span></span>

    ![Screenshot of Patterns page with search tool icon highlighted](./media/luis-how-to-model-intent-pattern/search-icon.png)

    <span data-ttu-id="b9620-128">Type the search text in the search box at the top right corner of the patterns list and select Enter.</span><span class="sxs-lookup"><span data-stu-id="b9620-128">Type the search text in the search box at the top right corner of the patterns list and select Enter.</span></span> <span data-ttu-id="b9620-129">The patterns list is updated to display only the patterns including your search text.</span><span class="sxs-lookup"><span data-stu-id="b9620-129">The patterns list is updated to display only the patterns including your search text.</span></span>

    ![Screenshot of Patterns page with search text in search box highlighted](./media/luis-how-to-model-intent-pattern/search-text.png)

    <span data-ttu-id="b9620-131">To cancel the search and restore your full list of patterns, delete the search text you've typed.</span><span class="sxs-lookup"><span data-stu-id="b9620-131">To cancel the search and restore your full list of patterns, delete the search text you've typed.</span></span>

<!-- TBD: should I be able to click on the magnifying glass again to close the search box? It doesn't reset the list. -->

## <a name="edit-a-pattern"></a><span data-ttu-id="b9620-132">Edit a pattern</span><span class="sxs-lookup"><span data-stu-id="b9620-132">Edit a pattern</span></span>
1. <span data-ttu-id="b9620-133">To edit a pattern, select the ellipsis (***...***) button at the right end of the line for that pattern, then select **Edit**.</span><span class="sxs-lookup"><span data-stu-id="b9620-133">To edit a pattern, select the ellipsis (***...***) button at the right end of the line for that pattern, then select **Edit**.</span></span> 

    ![Screenshot of Edit menu item in pattern row](./media/luis-how-to-model-intent-pattern/patterns-three-dots.png) 

2. <span data-ttu-id="b9620-135">Enter any changes in the text box.</span><span class="sxs-lookup"><span data-stu-id="b9620-135">Enter any changes in the text box.</span></span> <span data-ttu-id="b9620-136">When you are done, select enter.</span><span class="sxs-lookup"><span data-stu-id="b9620-136">When you are done, select enter.</span></span> <span data-ttu-id="b9620-137">When you are done editing patterns, [train](luis-how-to-train.md) your app.</span><span class="sxs-lookup"><span data-stu-id="b9620-137">When you are done editing patterns, [train](luis-how-to-train.md) your app.</span></span>

    ![Screenshot of editing pattern](./media/luis-how-to-model-intent-pattern/edit-pattern.png)

## <a name="reassign-individual-pattern-to-different-intent"></a><span data-ttu-id="b9620-139">Reassign individual pattern to different intent</span><span class="sxs-lookup"><span data-stu-id="b9620-139">Reassign individual pattern to different intent</span></span>

<span data-ttu-id="b9620-140">To reassign a single pattern to a different intent, select the intent list box to the right of the pattern text, and select a different intent.</span><span class="sxs-lookup"><span data-stu-id="b9620-140">To reassign a single pattern to a different intent, select the intent list box to the right of the pattern text, and select a different intent.</span></span>

![Screenshot of reassigning individual pattern to different intent](./media/luis-how-to-model-intent-pattern/reassign-individual-pattern.png)

## <a name="reassign-several-patterns-to-different-intent"></a><span data-ttu-id="b9620-142">Reassign several patterns to different intent</span><span class="sxs-lookup"><span data-stu-id="b9620-142">Reassign several patterns to different intent</span></span>

<span data-ttu-id="b9620-143">To reassign several patterns to a different intent, select the checkbox to the left of each pattern or select the top checkbox.</span><span class="sxs-lookup"><span data-stu-id="b9620-143">To reassign several patterns to a different intent, select the checkbox to the left of each pattern or select the top checkbox.</span></span> <span data-ttu-id="b9620-144">The **Reassign intent** option displays on the tool bar.</span><span class="sxs-lookup"><span data-stu-id="b9620-144">The **Reassign intent** option displays on the tool bar.</span></span> <span data-ttu-id="b9620-145">Select the correct intent for the patterns.</span><span class="sxs-lookup"><span data-stu-id="b9620-145">Select the correct intent for the patterns.</span></span> 

![Screenshot of reassigning several patterns to different intent](./media/luis-how-to-model-intent-pattern/reassign-many-patterns.png)

## <a name="delete-a-single-pattern"></a><span data-ttu-id="b9620-147">Delete a single pattern</span><span class="sxs-lookup"><span data-stu-id="b9620-147">Delete a single pattern</span></span>

1. <span data-ttu-id="b9620-148">To delete a pattern, select the ellipsis (***...***) button at the right end of the line for that pattern, then select **Delete**.</span><span class="sxs-lookup"><span data-stu-id="b9620-148">To delete a pattern, select the ellipsis (***...***) button at the right end of the line for that pattern, then select **Delete**.</span></span> 

    ![Screenshot of Delete utterance](./media/luis-how-to-model-intent-pattern/patterns-three-dots-ddl.png)

2. <span data-ttu-id="b9620-150">Select **Ok** to confirm the deletion.</span><span class="sxs-lookup"><span data-stu-id="b9620-150">Select **Ok** to confirm the deletion.</span></span>

    ![Screenshot of Delete confirmation](./media/luis-how-to-model-intent-pattern/confirm-delete.png)

## <a name="delete-several-patterns"></a><span data-ttu-id="b9620-152">Delete several patterns</span><span class="sxs-lookup"><span data-stu-id="b9620-152">Delete several patterns</span></span>

1. <span data-ttu-id="b9620-153">To delete several patterns, select the checkbox to the left of each pattern or select the top checkbox.</span><span class="sxs-lookup"><span data-stu-id="b9620-153">To delete several patterns, select the checkbox to the left of each pattern or select the top checkbox.</span></span> <span data-ttu-id="b9620-154">The **Delete patterns(s)** option displays on the tool bar.</span><span class="sxs-lookup"><span data-stu-id="b9620-154">The **Delete patterns(s)** option displays on the tool bar.</span></span> <span data-ttu-id="b9620-155">Select **Delete patterns(s)**.</span><span class="sxs-lookup"><span data-stu-id="b9620-155">Select **Delete patterns(s)**.</span></span>  

    ![Screenshot of deleting several patterns](./media/luis-how-to-model-intent-pattern/delete-many-patterns.png)

2. <span data-ttu-id="b9620-157">The **Delete patterns** confirmation dialog appears.</span><span class="sxs-lookup"><span data-stu-id="b9620-157">The **Delete patterns** confirmation dialog appears.</span></span> <span data-ttu-id="b9620-158">Select **Ok** to finish the deletion.</span><span class="sxs-lookup"><span data-stu-id="b9620-158">Select **Ok** to finish the deletion.</span></span>

    ![Screenshot of deleting several patterns](./media/luis-how-to-model-intent-pattern/delete-many-patterns-confirmation.png)

## <a name="filter-pattern-list-by-entity"></a><span data-ttu-id="b9620-160">Filter pattern list by entity</span><span class="sxs-lookup"><span data-stu-id="b9620-160">Filter pattern list by entity</span></span>

<span data-ttu-id="b9620-161">To filter the list of patterns by a specific entity, select **Entity filters** in the toolbar above the patterns.</span><span class="sxs-lookup"><span data-stu-id="b9620-161">To filter the list of patterns by a specific entity, select **Entity filters** in the toolbar above the patterns.</span></span> 

![Screenshot of filtering patterns by entity](./media/luis-how-to-model-intent-pattern/filter-entities-1.png)

<span data-ttu-id="b9620-163">After the filter is applied, the entity name appears below the tool bar.</span><span class="sxs-lookup"><span data-stu-id="b9620-163">After the filter is applied, the entity name appears below the tool bar.</span></span> 

## <a name="filter-pattern-list-by-intent"></a><span data-ttu-id="b9620-164">Filter pattern list by intent</span><span class="sxs-lookup"><span data-stu-id="b9620-164">Filter pattern list by intent</span></span>

<span data-ttu-id="b9620-165">To filter the list of patterns by a specific intent, select **Intent filters** in the toolbar above the patterns.</span><span class="sxs-lookup"><span data-stu-id="b9620-165">To filter the list of patterns by a specific intent, select **Intent filters** in the toolbar above the patterns.</span></span> 

![Screenshot of filtering patterns by intent](./media/luis-how-to-model-intent-pattern/filter-intents-1.png)

<span data-ttu-id="b9620-167">After the filter is applied, the intent name appears below the tool bar.</span><span class="sxs-lookup"><span data-stu-id="b9620-167">After the filter is applied, the intent name appears below the tool bar.</span></span> 

## <a name="remove-entity-or-intent-filter"></a><span data-ttu-id="b9620-168">Remove entity or intent filter</span><span class="sxs-lookup"><span data-stu-id="b9620-168">Remove entity or intent filter</span></span>
<span data-ttu-id="b9620-169">When the pattern list is filtered, the entity or intent name appears below the toolbar.</span><span class="sxs-lookup"><span data-stu-id="b9620-169">When the pattern list is filtered, the entity or intent name appears below the toolbar.</span></span> <span data-ttu-id="b9620-170">To remove the filter, select the name.</span><span class="sxs-lookup"><span data-stu-id="b9620-170">To remove the filter, select the name.</span></span>

![Screenshot of filtered patterns by entity](./media/luis-how-to-model-intent-pattern/filter-entities-2.png)

<span data-ttu-id="b9620-172">The filter is removed and all patterns display.</span><span class="sxs-lookup"><span data-stu-id="b9620-172">The filter is removed and all patterns display.</span></span> 

## <a name="add-pattern-from-existing-utterance-on-intent-or-entity-page"></a><span data-ttu-id="b9620-173">Add pattern from existing utterance on intent or entity page</span><span class="sxs-lookup"><span data-stu-id="b9620-173">Add pattern from existing utterance on intent or entity page</span></span>
<span data-ttu-id="b9620-174">You can create a pattern from an existing utterance on either the **Intent** or **Entity** page.</span><span class="sxs-lookup"><span data-stu-id="b9620-174">You can create a pattern from an existing utterance on either the **Intent** or **Entity** page.</span></span> <span data-ttu-id="b9620-175">All utterances on any intent or entity page are displayed in a list with the right column providing access to utterance-level options such as **Edit**, **Delete**, and **Add as pattern**.</span><span class="sxs-lookup"><span data-stu-id="b9620-175">All utterances on any intent or entity page are displayed in a list with the right column providing access to utterance-level options such as **Edit**, **Delete**, and **Add as pattern**.</span></span>

1. <span data-ttu-id="b9620-176">On the selected row of the utterance, select the ellipsis (***...***) button to the right of the utterance, and select **Add as pattern**.</span><span class="sxs-lookup"><span data-stu-id="b9620-176">On the selected row of the utterance, select the ellipsis (***...***) button to the right of the utterance, and select **Add as pattern**.</span></span>

    <span data-ttu-id="b9620-177">[![](./media/luis-how-to-model-intent-pattern/add-pattern-from-utterance.png "Screenshot of utterances table with Add pattern highlighted in options menu")](./media/luis-how-to-model-intent-pattern/add-pattern-from-utterance.png)</span><span class="sxs-lookup"><span data-stu-id="b9620-177">[![](./media/luis-how-to-model-intent-pattern/add-pattern-from-utterance.png "Screenshot of utterances table with Add pattern highlighted in options menu")](./media/luis-how-to-model-intent-pattern/add-pattern-from-utterance.png)</span></span>

2. <span data-ttu-id="b9620-178">Modify the pattern according to the [syntax rules](luis-concept-patterns.md#pattern-syntax).</span><span class="sxs-lookup"><span data-stu-id="b9620-178">Modify the pattern according to the [syntax rules](luis-concept-patterns.md#pattern-syntax).</span></span> <span data-ttu-id="b9620-179">If the utterance you selected is labeled with entities, those entities are already in the pattern with the correct syntax.</span><span class="sxs-lookup"><span data-stu-id="b9620-179">If the utterance you selected is labeled with entities, those entities are already in the pattern with the correct syntax.</span></span>

    ![Screenshot of filtered patterns by entity](./media/luis-how-to-model-intent-pattern/confirm-patterns-modal.png)

## <a name="train-your-app-after-changing-model-with-patterns"></a><span data-ttu-id="b9620-181">Train your app after changing model with patterns</span><span class="sxs-lookup"><span data-stu-id="b9620-181">Train your app after changing model with patterns</span></span>
<span data-ttu-id="b9620-182">After you add, edit, remove, or reassign a pattern, [train](luis-how-to-train.md) and [publish](luis-how-to-publish-app.md) your app for your changes to affect endpoint queries.</span><span class="sxs-lookup"><span data-stu-id="b9620-182">After you add, edit, remove, or reassign a pattern, [train](luis-how-to-train.md) and [publish](luis-how-to-publish-app.md) your app for your changes to affect endpoint queries.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="b9620-183">Next steps</span><span class="sxs-lookup"><span data-stu-id="b9620-183">Next steps</span></span>

* <span data-ttu-id="b9620-184">Learn how to [build a pattern](luis-tutorial-pattern.md) with a pattern.any and roles.</span><span class="sxs-lookup"><span data-stu-id="b9620-184">Learn how to [build a pattern](luis-tutorial-pattern.md) with a pattern.any and roles.</span></span>
* <span data-ttu-id="b9620-185">Learn how to [train](luis-how-to-train.md) your app.</span><span class="sxs-lookup"><span data-stu-id="b9620-185">Learn how to [train](luis-how-to-train.md) your app.</span></span>