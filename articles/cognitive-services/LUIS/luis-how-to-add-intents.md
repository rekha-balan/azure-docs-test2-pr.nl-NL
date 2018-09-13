---
title: Add intents in LUIS applications | Microsoft Docs
description: Use Language Understanding (LUIS) to add intents to help apps understand user requests and react to them properly.
services: cognitive-services
author: diberry
manager: cjgronlund
ms.component: language-understanding
ms.topic: article
ms.date: 05/07/2018
ms.author: diberry
ms.service: cognitive-services
ms.openlocfilehash: 0ebf15ea49467674ab3c56aa7983131593cf5c9a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857932"
---
# <a name="manage-intents"></a><span data-ttu-id="a225a-103">Manage intents</span><span class="sxs-lookup"><span data-stu-id="a225a-103">Manage intents</span></span> 
<span data-ttu-id="a225a-104">Add [intents](luis-concept-intent.md) to your LUIS app to identify groups of questions or commands that have the same intentions.</span><span class="sxs-lookup"><span data-stu-id="a225a-104">Add [intents](luis-concept-intent.md) to your LUIS app to identify groups of questions or commands that have the same intentions.</span></span> 

<span data-ttu-id="a225a-105">You add and manage your intents from the **Intents** page, available from **Intents** in LUIS's left panel.</span><span class="sxs-lookup"><span data-stu-id="a225a-105">You add and manage your intents from the **Intents** page, available from **Intents** in LUIS's left panel.</span></span> 

<span data-ttu-id="a225a-106">The following procedure demonstrates how to add the "Bookflight" intent in the TravelAgent app.</span><span class="sxs-lookup"><span data-stu-id="a225a-106">The following procedure demonstrates how to add the "Bookflight" intent in the TravelAgent app.</span></span>

## <a name="add-intent"></a><span data-ttu-id="a225a-107">Add intent</span><span class="sxs-lookup"><span data-stu-id="a225a-107">Add intent</span></span>

1. <span data-ttu-id="a225a-108">Open your app (for example, TravelAgent) by clicking its name on **My Apps** page, and then click **Intents** in the left panel.</span><span class="sxs-lookup"><span data-stu-id="a225a-108">Open your app (for example, TravelAgent) by clicking its name on **My Apps** page, and then click **Intents** in the left panel.</span></span> 
2. <span data-ttu-id="a225a-109">On the **Intents** page, click **Create new intent**.</span><span class="sxs-lookup"><span data-stu-id="a225a-109">On the **Intents** page, click **Create new intent**.</span></span>

    ![Intents List](./media/luis-how-to-add-intents/IntentsList.png)
3. <span data-ttu-id="a225a-111">In the **Create new intent** dialog box, type the intent name "BookFlight" and click **Done**.</span><span class="sxs-lookup"><span data-stu-id="a225a-111">In the **Create new intent** dialog box, type the intent name "BookFlight" and click **Done**.</span></span>

    ![Add Intent](./media/luis-how-to-add-intents/Addintent-dialogbox.png)

    <span data-ttu-id="a225a-113">On the intent details page of the newly added intent, [add utterances](#add-an-utterance-on-intent-page).</span><span class="sxs-lookup"><span data-stu-id="a225a-113">On the intent details page of the newly added intent, [add utterances](#add-an-utterance-on-intent-page).</span></span>

## <a name="rename-intent"></a><span data-ttu-id="a225a-114">Rename intent</span><span class="sxs-lookup"><span data-stu-id="a225a-114">Rename intent</span></span>

1. <span data-ttu-id="a225a-115">On the **Intent** page, click the Rename icon ![Rename Intent](./media/luis-how-to-add-intents/Rename-Intent-btn.png) next to the intent name.</span><span class="sxs-lookup"><span data-stu-id="a225a-115">On the **Intent** page, click the Rename icon ![Rename Intent](./media/luis-how-to-add-intents/Rename-Intent-btn.png) next to the intent name.</span></span> 

2. <span data-ttu-id="a225a-116">On the **Intent** page, the current intent name is shown in a dialog box.</span><span class="sxs-lookup"><span data-stu-id="a225a-116">On the **Intent** page, the current intent name is shown in a dialog box.</span></span> <span data-ttu-id="a225a-117">Edit the intent name and press enter.</span><span class="sxs-lookup"><span data-stu-id="a225a-117">Edit the intent name and press enter.</span></span> <span data-ttu-id="a225a-118">The new name is saved and displayed on the intent page.</span><span class="sxs-lookup"><span data-stu-id="a225a-118">The new name is saved and displayed on the intent page.</span></span>

    ![Edit Intent](./media/luis-how-to-add-intents/EditIntent-dialogbox.png)

## <a name="delete-intent"></a><span data-ttu-id="a225a-120">Delete intent</span><span class="sxs-lookup"><span data-stu-id="a225a-120">Delete intent</span></span>
<span data-ttu-id="a225a-121">When deleting an intent other than the None intent, you can choose to add all the utterances to the None intent.</span><span class="sxs-lookup"><span data-stu-id="a225a-121">When deleting an intent other than the None intent, you can choose to add all the utterances to the None intent.</span></span> <span data-ttu-id="a225a-122">This is useful if you need to move the utterances instead of deleting them.</span><span class="sxs-lookup"><span data-stu-id="a225a-122">This is useful if you need to move the utterances instead of deleting them.</span></span>   

1. <span data-ttu-id="a225a-123">On the **Intent** page, click the **Delete Intent** button next to the right of the intent name.</span><span class="sxs-lookup"><span data-stu-id="a225a-123">On the **Intent** page, click the **Delete Intent** button next to the right of the intent name.</span></span> 

    ![Delete Intent Button](./media/luis-how-to-add-intents/DeleteIntent.png)

2. <span data-ttu-id="a225a-125">Click the "Ok" button on the confirmation dialog box.</span><span class="sxs-lookup"><span data-stu-id="a225a-125">Click the "Ok" button on the confirmation dialog box.</span></span>

<!--
    TBD: waiting for confirmation about which delete dialog is going to be in //BUILD

    ![Delete Intent Dialog](./media/luis-how-to-add-intents/DeleteIntent-Confirmation.png)
-->


## <a name="add-an-utterance-on-intent-page"></a><span data-ttu-id="a225a-126">Add an utterance on intent page</span><span class="sxs-lookup"><span data-stu-id="a225a-126">Add an utterance on intent page</span></span>

<span data-ttu-id="a225a-127">On the intent page, enter a relevant utterance you expect from your users, such as `book 2 adult business tickets to Paris tomorrow on Air France` in the text box below the intent name, and then press Enter.</span><span class="sxs-lookup"><span data-stu-id="a225a-127">On the intent page, enter a relevant utterance you expect from your users, such as `book 2 adult business tickets to Paris tomorrow on Air France` in the text box below the intent name, and then press Enter.</span></span> 
 
>[!NOTE]
><span data-ttu-id="a225a-128">LUIS converts all utterances to lowercase.</span><span class="sxs-lookup"><span data-stu-id="a225a-128">LUIS converts all utterances to lowercase.</span></span>

![Screenshot of Intents details page, with utterance highlighted](./media/luis-how-to-add-intents/add-new-utterance-to-intent.png) 

<span data-ttu-id="a225a-130">Utterances are added to the utterances list for the current intent.</span><span class="sxs-lookup"><span data-stu-id="a225a-130">Utterances are added to the utterances list for the current intent.</span></span> <span data-ttu-id="a225a-131">Once an utterance is added, [label any entities](luis-how-to-add-example-utterances.md) within the utterances and [train](luis-how-to-train.md) your app.</span><span class="sxs-lookup"><span data-stu-id="a225a-131">Once an utterance is added, [label any entities](luis-how-to-add-example-utterances.md) within the utterances and [train](luis-how-to-train.md) your app.</span></span> 

## <a name="create-a-pattern-from-an-utterance"></a><span data-ttu-id="a225a-132">Create a pattern from an utterance</span><span class="sxs-lookup"><span data-stu-id="a225a-132">Create a pattern from an utterance</span></span>
<span data-ttu-id="a225a-133">See [Add pattern from existing utterance on intent or entity page](luis-how-to-model-intent-pattern.md#add-pattern-from-existing-utterance-on-intent-or-entity-page).</span><span class="sxs-lookup"><span data-stu-id="a225a-133">See [Add pattern from existing utterance on intent or entity page](luis-how-to-model-intent-pattern.md#add-pattern-from-existing-utterance-on-intent-or-entity-page).</span></span>

## <a name="edit-an-utterance-on-intent-page"></a><span data-ttu-id="a225a-134">Edit an utterance on intent page</span><span class="sxs-lookup"><span data-stu-id="a225a-134">Edit an utterance on intent page</span></span>

<span data-ttu-id="a225a-135">To edit an utterance, select the ellipsis (***...***) button at the right end of the line for that utterance, and then select **Edit**.</span><span class="sxs-lookup"><span data-stu-id="a225a-135">To edit an utterance, select the ellipsis (***...***) button at the right end of the line for that utterance, and then select **Edit**.</span></span> <span data-ttu-id="a225a-136">Modify the text then press Enter on the keyboard.</span><span class="sxs-lookup"><span data-stu-id="a225a-136">Modify the text then press Enter on the keyboard.</span></span>

![Screenshot of Intents details page, with ellipsis button highlighted](./media/luis-how-to-add-intents/edit-utterance.png) 

## <a name="reassign-utterances-on-intent-page"></a><span data-ttu-id="a225a-138">Reassign utterances on intent page</span><span class="sxs-lookup"><span data-stu-id="a225a-138">Reassign utterances on intent page</span></span>
<span data-ttu-id="a225a-139">You can change the intent of one or more utterances by reassigning them to another intent.</span><span class="sxs-lookup"><span data-stu-id="a225a-139">You can change the intent of one or more utterances by reassigning them to another intent.</span></span> 

<span data-ttu-id="a225a-140">To reassign a single utterance to a different intent, at the right end of the utterance's row, select the correct intent name under the **Labeled intent** column.</span><span class="sxs-lookup"><span data-stu-id="a225a-140">To reassign a single utterance to a different intent, at the right end of the utterance's row, select the correct intent name under the **Labeled intent** column.</span></span> <span data-ttu-id="a225a-141">The utterance is removed from the current intent's utterance list.</span><span class="sxs-lookup"><span data-stu-id="a225a-141">The utterance is removed from the current intent's utterance list.</span></span> 

![Screenshot of BookFlight intent page with an utterance's intent under Labeled intent column selected](./media/luis-how-to-add-intents/reassign-1-utterance.png)

<span data-ttu-id="a225a-143">To change the intent of several utterances, select the checkboxes to the left of the utterances, and then select **Reassign intent**.</span><span class="sxs-lookup"><span data-stu-id="a225a-143">To change the intent of several utterances, select the checkboxes to the left of the utterances, and then select **Reassign intent**.</span></span> <span data-ttu-id="a225a-144">Select the correct intent from the list.</span><span class="sxs-lookup"><span data-stu-id="a225a-144">Select the correct intent from the list.</span></span>

![Screenshot of BookFlight intent page with an utterance checked and the Reassign intent button highlighted](./media/luis-how-to-add-intents/delete-several-utterances.png) 

## <a name="delete-utterances-on-intent-page"></a><span data-ttu-id="a225a-146">Delete utterances on intent page</span><span class="sxs-lookup"><span data-stu-id="a225a-146">Delete utterances on intent page</span></span>

<span data-ttu-id="a225a-147">To delete an utterance, select the ellipsis (***...***) button at the right end of the line for that utterance, and then select **Delete**.</span><span class="sxs-lookup"><span data-stu-id="a225a-147">To delete an utterance, select the ellipsis (***...***) button at the right end of the line for that utterance, and then select **Delete**.</span></span> <span data-ttu-id="a225a-148">The utterance is removed from the list and the LUIS app.</span><span class="sxs-lookup"><span data-stu-id="a225a-148">The utterance is removed from the list and the LUIS app.</span></span>

![Screenshot of Intents details page, with Delete option highlighted](./media/luis-how-to-add-intents/delete-utterance-ddl.png)

<span data-ttu-id="a225a-150">To delete several utterances:</span><span class="sxs-lookup"><span data-stu-id="a225a-150">To delete several utterances:</span></span>

1. <span data-ttu-id="a225a-151">Select the checkboxes to the left of the utterances, and then select **Delete utterances(s)**.</span><span class="sxs-lookup"><span data-stu-id="a225a-151">Select the checkboxes to the left of the utterances, and then select **Delete utterances(s)**.</span></span> 

    ![Screenshot of Intents details page, with utterances checked and Delete utterance(s) button highlighted](./media/luis-how-to-add-intents/delete-several-utterances.png)

2. <span data-ttu-id="a225a-153">Select **Done** in the **Delete utterances?** pop-up dialog.</span><span class="sxs-lookup"><span data-stu-id="a225a-153">Select **Done** in the **Delete utterances?** pop-up dialog.</span></span>

## <a name="search-in-utterances-on-intent-page"></a><span data-ttu-id="a225a-154">Search in utterances on intent page</span><span class="sxs-lookup"><span data-stu-id="a225a-154">Search in utterances on intent page</span></span>
<span data-ttu-id="a225a-155">In an intent, you can search for utterances that contain text (words or phrases).</span><span class="sxs-lookup"><span data-stu-id="a225a-155">In an intent, you can search for utterances that contain text (words or phrases).</span></span> <span data-ttu-id="a225a-156">For example, you might notice an error that involves a particular word, and you want to find all examples that include that particular word.</span><span class="sxs-lookup"><span data-stu-id="a225a-156">For example, you might notice an error that involves a particular word, and you want to find all examples that include that particular word.</span></span> 

1. <span data-ttu-id="a225a-157">Select the magnifying glass icon in the toolbar.</span><span class="sxs-lookup"><span data-stu-id="a225a-157">Select the magnifying glass icon in the toolbar.</span></span>

    ![Screenshot of Intents page, with search icon of magnifying glass highlighted](./media/luis-how-to-add-intents/magnifying-glass.png)

2. <span data-ttu-id="a225a-159">A search textbox appears.</span><span class="sxs-lookup"><span data-stu-id="a225a-159">A search textbox appears.</span></span> <span data-ttu-id="a225a-160">Type the word or phrase in the search box at the top right corner of the utterances list.</span><span class="sxs-lookup"><span data-stu-id="a225a-160">Type the word or phrase in the search box at the top right corner of the utterances list.</span></span> <span data-ttu-id="a225a-161">The utterances list updates, to display only the utterances that include your search text.</span><span class="sxs-lookup"><span data-stu-id="a225a-161">The utterances list updates, to display only the utterances that include your search text.</span></span> 

    ![Screenshot of Intents page, with search textbox highlighted](./media/luis-how-to-add-intents/search-textbox.png)

    <span data-ttu-id="a225a-163">To cancel the search and restore your full list of utterances, delete the search text you've typed.</span><span class="sxs-lookup"><span data-stu-id="a225a-163">To cancel the search and restore your full list of utterances, delete the search text you've typed.</span></span> <span data-ttu-id="a225a-164">To close the search textbox, select the magnifying glass icon in the toolbar again.</span><span class="sxs-lookup"><span data-stu-id="a225a-164">To close the search textbox, select the magnifying glass icon in the toolbar again.</span></span>

## <a name="prediction-discrepancy-errors-on-intent-page"></a><span data-ttu-id="a225a-165">Prediction discrepancy errors on intent page</span><span class="sxs-lookup"><span data-stu-id="a225a-165">Prediction discrepancy errors on intent page</span></span>
<span data-ttu-id="a225a-166">An utterance in an intent might have a discrepancy between the selected intent and the prediction score.</span><span class="sxs-lookup"><span data-stu-id="a225a-166">An utterance in an intent might have a discrepancy between the selected intent and the prediction score.</span></span> <span data-ttu-id="a225a-167">LUIS indicates this discrepancy with a red box around the score.</span><span class="sxs-lookup"><span data-stu-id="a225a-167">LUIS indicates this discrepancy with a red box around the score.</span></span> 

![Screenshot of BookFlight Intent page, with prediction discrepancy score highlighted](./media/luis-how-to-add-intents/score-discrepancy.png) 

## <a name="filter-by-intent-prediction-discrepancy-errors-on-intent-page"></a><span data-ttu-id="a225a-169">Filter by intent prediction discrepancy errors on intent page</span><span class="sxs-lookup"><span data-stu-id="a225a-169">Filter by intent prediction discrepancy errors on intent page</span></span>
<span data-ttu-id="a225a-170">To filter the utterance list to only utterances with an intent prediction discrepancy, toggle from **Show All** to **Errors only** in the toolbar.</span><span class="sxs-lookup"><span data-stu-id="a225a-170">To filter the utterance list to only utterances with an intent prediction discrepancy, toggle from **Show All** to **Errors only** in the toolbar.</span></span> 

## <a name="filter-by-entity-type-on-intent-page"></a><span data-ttu-id="a225a-171">Filter by entity type on intent page</span><span class="sxs-lookup"><span data-stu-id="a225a-171">Filter by entity type on intent page</span></span>
<span data-ttu-id="a225a-172">Use the **Entity filters** drop-down on the toolbar to filter the utterances by entity.</span><span class="sxs-lookup"><span data-stu-id="a225a-172">Use the **Entity filters** drop-down on the toolbar to filter the utterances by entity.</span></span> 

![Screenshot of Intents page, with entity type filter highlighted](./media/luis-how-to-add-intents/filter-by-entities.png) 

<span data-ttu-id="a225a-174">To remove the filter, select the blue filter box with that word or phrase under the toolbar.</span><span class="sxs-lookup"><span data-stu-id="a225a-174">To remove the filter, select the blue filter box with that word or phrase under the toolbar.</span></span>  
<!-- TBD: waiting for ux fix - bug in ux of prebuit entity number -- when filtering by it, it doesn't show the list -->

## <a name="switch-to-token-view-on-intent-page"></a><span data-ttu-id="a225a-175">Switch to token view on intent page</span><span class="sxs-lookup"><span data-stu-id="a225a-175">Switch to token view on intent page</span></span>
<span data-ttu-id="a225a-176">Toggle **Tokens View** to view the tokens instead of the entity type names.</span><span class="sxs-lookup"><span data-stu-id="a225a-176">Toggle **Tokens View** to view the tokens instead of the entity type names.</span></span> <span data-ttu-id="a225a-177">On the keyboard, you can also use **Control+E** to toggle the view.</span><span class="sxs-lookup"><span data-stu-id="a225a-177">On the keyboard, you can also use **Control+E** to toggle the view.</span></span> 

![Screenshot of BookFlight intent, with Token View highlighted](./media/luis-how-to-add-intents/toggle-tokens-view.png)

## <a name="train-your-app-after-changing-model-with-intents"></a><span data-ttu-id="a225a-179">Train your app after changing model with intents</span><span class="sxs-lookup"><span data-stu-id="a225a-179">Train your app after changing model with intents</span></span>
<span data-ttu-id="a225a-180">After you add, edit, or remove intents, [train](luis-how-to-train.md) and [publish](luis-how-to-publish-app.md) your app for your changes to affect endpoint queries.</span><span class="sxs-lookup"><span data-stu-id="a225a-180">After you add, edit, or remove intents, [train](luis-how-to-train.md) and [publish](luis-how-to-publish-app.md) your app for your changes to affect endpoint queries.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="a225a-181">Next steps</span><span class="sxs-lookup"><span data-stu-id="a225a-181">Next steps</span></span>

<span data-ttu-id="a225a-182">After adding intents to your app, your next task is to start adding [example utterances](luis-how-to-add-example-utterances.md) for the intents you've added.</span><span class="sxs-lookup"><span data-stu-id="a225a-182">After adding intents to your app, your next task is to start adding [example utterances](luis-how-to-add-example-utterances.md) for the intents you've added.</span></span> 
