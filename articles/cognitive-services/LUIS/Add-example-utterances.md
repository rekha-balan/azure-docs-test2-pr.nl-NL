---
title: Add example utterances in LUIS apps | Microsoft Docs
description: Learn how to add utterances in Language Understanding Intelligent Services (LUIS) applications.
services: cognitive-services
author: cahann
manager: hsalama
ms.service: cognitive-services
ms.technology: luis
ms.topic: article
ms.date: 03/01/2017
ms.author: cahann
ms.openlocfilehash: 4098cf8b9fc52bc973e451c5336398e57af8f888
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551222"
---
# <a name="add-example-utterances"></a><span data-ttu-id="e0492-103">Add example utterances</span><span class="sxs-lookup"><span data-stu-id="e0492-103">Add example utterances</span></span>

<span data-ttu-id="e0492-104">Utterances are sentences representing examples of user queries or commands that your application is expected to receive and interpret.</span><span class="sxs-lookup"><span data-stu-id="e0492-104">Utterances are sentences representing examples of user queries or commands that your application is expected to receive and interpret.</span></span> <span data-ttu-id="e0492-105">You need to add example utterances for each intent in your app.</span><span class="sxs-lookup"><span data-stu-id="e0492-105">You need to add example utterances for each intent in your app.</span></span> <span data-ttu-id="e0492-106">LUIS learns from these utterances and your app is able to generalise and understand similar contexts.</span><span class="sxs-lookup"><span data-stu-id="e0492-106">LUIS learns from these utterances and your app is able to generalise and understand similar contexts.</span></span> <span data-ttu-id="e0492-107">By constantly adding more utterances and labeling them, you are enhancing your application’s language learning experience.</span><span class="sxs-lookup"><span data-stu-id="e0492-107">By constantly adding more utterances and labeling them, you are enhancing your application’s language learning experience.</span></span> 

<span data-ttu-id="e0492-108">For each intent, add example utterances that trigger this intent and include as many utterance variations as you expect users to say.</span><span class="sxs-lookup"><span data-stu-id="e0492-108">For each intent, add example utterances that trigger this intent and include as many utterance variations as you expect users to say.</span></span> <span data-ttu-id="e0492-109">The more relevant & diverse examples you add to the intent, the better intent prediction you’ll get from your app.</span><span class="sxs-lookup"><span data-stu-id="e0492-109">The more relevant & diverse examples you add to the intent, the better intent prediction you’ll get from your app.</span></span> <span data-ttu-id="e0492-110">For example, the utterance “book me a flight to Paris” may have variations such as “Reserve me a flight to Paris”, "book me a ticket to Paris", "Get me a ticket to Paris”, "Fly me to Paris", and "Take me on a flight to Paris".</span><span class="sxs-lookup"><span data-stu-id="e0492-110">For example, the utterance “book me a flight to Paris” may have variations such as “Reserve me a flight to Paris”, "book me a ticket to Paris", "Get me a ticket to Paris”, "Fly me to Paris", and "Take me on a flight to Paris".</span></span>

<span data-ttu-id="e0492-111">Utterances are added to an intent on the **Utterances** tab of the intent page.</span><span class="sxs-lookup"><span data-stu-id="e0492-111">Utterances are added to an intent on the **Utterances** tab of the intent page.</span></span> <span data-ttu-id="e0492-112">The following steps describe how to add example utterances to an intent (e.g. "BookFlight" intent in the TravelAgent app).</span><span class="sxs-lookup"><span data-stu-id="e0492-112">The following steps describe how to add example utterances to an intent (e.g. "BookFlight" intent in the TravelAgent app).</span></span> 

<span data-ttu-id="e0492-113">**To add utterance:**</span><span class="sxs-lookup"><span data-stu-id="e0492-113">**To add utterance:**</span></span>

1. <span data-ttu-id="e0492-114">Open the TravelAgent app by clicking its name on **My Apps** page, and then click **Intents** in the left panel.</span><span class="sxs-lookup"><span data-stu-id="e0492-114">Open the TravelAgent app by clicking its name on **My Apps** page, and then click **Intents** in the left panel.</span></span> 

2. <span data-ttu-id="e0492-115">On the **Intents** page, click the intent name "BookFlight" to open its details page, with **Utterances** as the current tab, like the screen below.</span><span class="sxs-lookup"><span data-stu-id="e0492-115">On the **Intents** page, click the intent name "BookFlight" to open its details page, with **Utterances** as the current tab, like the screen below.</span></span>

    ![Intent Details page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/IntentDetails-UtterancesTab1.JPG) 

3. <span data-ttu-id="e0492-117">Type “book me 2 adult business tickets to Paris tomorrow on Air France” as a new utterance in the text box, and then press Enter.</span><span class="sxs-lookup"><span data-stu-id="e0492-117">Type “book me 2 adult business tickets to Paris tomorrow on Air France” as a new utterance in the text box, and then press Enter.</span></span> <span data-ttu-id="e0492-118">Note that LUIS converts all utterances to lower case.</span><span class="sxs-lookup"><span data-stu-id="e0492-118">Note that LUIS converts all utterances to lower case.</span></span>

    ![Intent Details page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/IntentDetails-UtterancesTab.JPG) 

4. <span data-ttu-id="e0492-120">Repeat the previous step to add more example utterances.</span><span class="sxs-lookup"><span data-stu-id="e0492-120">Repeat the previous step to add more example utterances.</span></span> 
5.  <span data-ttu-id="e0492-121">Click **Save** to save the added utterances in the utterances list.</span><span class="sxs-lookup"><span data-stu-id="e0492-121">Click **Save** to save the added utterances in the utterances list.</span></span>

<span data-ttu-id="e0492-122">Utterances are added to the utterances list in the current intent.</span><span class="sxs-lookup"><span data-stu-id="e0492-122">Utterances are added to the utterances list in the current intent.</span></span> <span data-ttu-id="e0492-123">To delete one or more utterances from the list, select them and click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="e0492-123">To delete one or more utterances from the list, select them and click **Delete**.</span></span>

## <a name="label-utterances"></a><span data-ttu-id="e0492-124">Label utterances</span><span class="sxs-lookup"><span data-stu-id="e0492-124">Label utterances</span></span>
<span data-ttu-id="e0492-125">After adding utterances, your next step is to label them.</span><span class="sxs-lookup"><span data-stu-id="e0492-125">After adding utterances, your next step is to label them.</span></span> <span data-ttu-id="e0492-126">Utterances are labeled in terms of intents and entities.</span><span class="sxs-lookup"><span data-stu-id="e0492-126">Utterances are labeled in terms of intents and entities.</span></span> 
### <a name="intent-label"></a><span data-ttu-id="e0492-127">Intent label</span><span class="sxs-lookup"><span data-stu-id="e0492-127">Intent label</span></span>
<span data-ttu-id="e0492-128">Adding an utterance in an intent page means that it is labeled under this intent.</span><span class="sxs-lookup"><span data-stu-id="e0492-128">Adding an utterance in an intent page means that it is labeled under this intent.</span></span> <span data-ttu-id="e0492-129">That's how an utterance gets an intent label.</span><span class="sxs-lookup"><span data-stu-id="e0492-129">That's how an utterance gets an intent label.</span></span> <span data-ttu-id="e0492-130">You can change the intent label of one or more utterances by moving them to another intent.</span><span class="sxs-lookup"><span data-stu-id="e0492-130">You can change the intent label of one or more utterances by moving them to another intent.</span></span> <span data-ttu-id="e0492-131">To do this, select the utterances, click **Reassign Intent**, and then select the intent where you want to move them.</span><span class="sxs-lookup"><span data-stu-id="e0492-131">To do this, select the utterances, click **Reassign Intent**, and then select the intent where you want to move them.</span></span> 
### <a name="entity-label"></a><span data-ttu-id="e0492-132">Entity label</span><span class="sxs-lookup"><span data-stu-id="e0492-132">Entity label</span></span>
<span data-ttu-id="e0492-133">There are different types of entities; custom entities and prebuilt entities.</span><span class="sxs-lookup"><span data-stu-id="e0492-133">There are different types of entities; custom entities and prebuilt entities.</span></span> <span data-ttu-id="e0492-134">You need to label custom entities only, **because prebuilt entities are detected and labeled automatically by your app.**</span><span class="sxs-lookup"><span data-stu-id="e0492-134">You need to label custom entities only, **because prebuilt entities are detected and labeled automatically by your app.**</span></span> 

<span data-ttu-id="e0492-135">For example, in the utterance "book me 2 adult business tickets to Paris tomorrow on Air France" that you've just added to "Bookflight" intent in TravelAgent app, before you start labeling entities in this utterance, if you have already added number and datetime as prebuilt entities, you'll notice that "2" and "tomorrow" were automatically detected as prebuilt entities, where "2" is labeled as "number" and "tomorrow" as "datetime".</span><span class="sxs-lookup"><span data-stu-id="e0492-135">For example, in the utterance "book me 2 adult business tickets to Paris tomorrow on Air France" that you've just added to "Bookflight" intent in TravelAgent app, before you start labeling entities in this utterance, if you have already added number and datetime as prebuilt entities, you'll notice that "2" and "tomorrow" were automatically detected as prebuilt entities, where "2" is labeled as "number" and "tomorrow" as "datetime".</span></span> <span data-ttu-id="e0492-136">This will look like the following screenshot.</span><span class="sxs-lookup"><span data-stu-id="e0492-136">This will look like the following screenshot.</span></span>

![Prebuilt Entity Labeling](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/LabelingEntities-prebuilt.JPG)

<span data-ttu-id="e0492-138">To Learn more about prebuilt entities and how to add them, see [Add entities](Add-entities.md).</span><span class="sxs-lookup"><span data-stu-id="e0492-138">To Learn more about prebuilt entities and how to add them, see [Add entities](Add-entities.md).</span></span>

<span data-ttu-id="e0492-139">In the following procedure, we'll label custom entities (simple, hierarchical and composite entities) in the utterance "book me 2 adult business tickets to Paris tomorrow on Air France".</span><span class="sxs-lookup"><span data-stu-id="e0492-139">In the following procedure, we'll label custom entities (simple, hierarchical and composite entities) in the utterance "book me 2 adult business tickets to Paris tomorrow on Air France".</span></span>

1. <span data-ttu-id="e0492-140">Select "Air France" in the utterance mentioned above to label it as entity.</span><span class="sxs-lookup"><span data-stu-id="e0492-140">Select "Air France" in the utterance mentioned above to label it as entity.</span></span>

    >[!NOTE]
    ><span data-ttu-id="e0492-141">When selecting words to label them as entities:</span><span class="sxs-lookup"><span data-stu-id="e0492-141">When selecting words to label them as entities:</span></span>
    >* <span data-ttu-id="e0492-142">For a single word, just click it.</span><span class="sxs-lookup"><span data-stu-id="e0492-142">For a single word, just click it.</span></span> 
    >* <span data-ttu-id="e0492-143">For a set of two or more words, click at the beginning and then at the end of the set.</span><span class="sxs-lookup"><span data-stu-id="e0492-143">For a set of two or more words, click at the beginning and then at the end of the set.</span></span>

2. <span data-ttu-id="e0492-144">In the entity drop-down box that appears, you can either click an existing entity (if available) to select it, or add a new entity by typing its name in the text box and clicking **Create entity**.</span><span class="sxs-lookup"><span data-stu-id="e0492-144">In the entity drop-down box that appears, you can either click an existing entity (if available) to select it, or add a new entity by typing its name in the text box and clicking **Create entity**.</span></span> <span data-ttu-id="e0492-145">Now, we'll create the simple entity "Airline".</span><span class="sxs-lookup"><span data-stu-id="e0492-145">Now, we'll create the simple entity "Airline".</span></span> <span data-ttu-id="e0492-146">Type "Airline" in the text box and then click **Create entity**.</span><span class="sxs-lookup"><span data-stu-id="e0492-146">Type "Airline" in the text box and then click **Create entity**.</span></span>
 
    ![Simple Entity Labeling](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/LabelingEntities-CreateSimple.JPG)
 
    >[!NOTE]
    ><span data-ttu-id="e0492-148">This way is used to create a simple entity on the spot (while labeling utterances).</span><span class="sxs-lookup"><span data-stu-id="e0492-148">This way is used to create a simple entity on the spot (while labeling utterances).</span></span> <span data-ttu-id="e0492-149">More complicated entities (e.g. hierarchical and composite) can only be created from the **Entities** page.</span><span class="sxs-lookup"><span data-stu-id="e0492-149">More complicated entities (e.g. hierarchical and composite) can only be created from the **Entities** page.</span></span> <span data-ttu-id="e0492-150">For more instructions, see [Add entities](Add-entities.md).</span><span class="sxs-lookup"><span data-stu-id="e0492-150">For more instructions, see [Add entities](Add-entities.md).</span></span> 

3. <span data-ttu-id="e0492-151">Click "Paris" in the same utterance, then click "ToLocation" in the entity drop-down box as the entity label.</span><span class="sxs-lookup"><span data-stu-id="e0492-151">Click "Paris" in the same utterance, then click "ToLocation" in the entity drop-down box as the entity label.</span></span> <span data-ttu-id="e0492-152">"ToLocation" is a hierarchical entity that must be added on the **Entities** page.</span><span class="sxs-lookup"><span data-stu-id="e0492-152">"ToLocation" is a hierarchical entity that must be added on the **Entities** page.</span></span> <span data-ttu-id="e0492-153">To learn more about hierarchical entities and how to add them, see [Add entities](Add-entities.md).</span><span class="sxs-lookup"><span data-stu-id="e0492-153">To learn more about hierarchical entities and how to add them, see [Add entities](Add-entities.md).</span></span>

    ![Hierarchical Entity Labeling](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/LabelingEntities-Hierarchical.JPG)

4. <span data-ttu-id="e0492-155">Click "2" (labeled as "number") and then click **Remove label** in the drop-down box.</span><span class="sxs-lookup"><span data-stu-id="e0492-155">Click "2" (labeled as "number") and then click **Remove label** in the drop-down box.</span></span> <span data-ttu-id="e0492-156">We remove this label as we do not want "2" to be interpreted individually, but to be part in a composite entity that we're going to label now.</span><span class="sxs-lookup"><span data-stu-id="e0492-156">We remove this label as we do not want "2" to be interpreted individually, but to be part in a composite entity that we're going to label now.</span></span>

5. <span data-ttu-id="e0492-157">Select the phrase "2 adult business" by clicking at the beginning and at the end of the phrase, then click "TicketsOrder" in the drop-down box.</span><span class="sxs-lookup"><span data-stu-id="e0492-157">Select the phrase "2 adult business" by clicking at the beginning and at the end of the phrase, then click "TicketsOrder" in the drop-down box.</span></span> <span data-ttu-id="e0492-158">"TicketsOrder" is a composite entity that must be added on the **Entities** page.</span><span class="sxs-lookup"><span data-stu-id="e0492-158">"TicketsOrder" is a composite entity that must be added on the **Entities** page.</span></span> <span data-ttu-id="e0492-159">To learn more about composite entities and how to add them, see [Add entities](Add-entities.md).</span><span class="sxs-lookup"><span data-stu-id="e0492-159">To learn more about composite entities and how to add them, see [Add entities](Add-entities.md).</span></span> 

    ![Composite Entity Labeling](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/LabelingEntities-Composite.JPG)

5. <span data-ttu-id="e0492-161">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="e0492-161">Click **Save**.</span></span>


<span data-ttu-id="e0492-162">**To remove an entity label:**</span><span class="sxs-lookup"><span data-stu-id="e0492-162">**To remove an entity label:**</span></span>

* <span data-ttu-id="e0492-163">Click the entity you want to remove its label and click **Remove label** in the entity drop-down box that appears.</span><span class="sxs-lookup"><span data-stu-id="e0492-163">Click the entity you want to remove its label and click **Remove label** in the entity drop-down box that appears.</span></span> <span data-ttu-id="e0492-164">Then, click **Save** to save this change.</span><span class="sxs-lookup"><span data-stu-id="e0492-164">Then, click **Save** to save this change.</span></span>

## <a name="search-in-utterances"></a><span data-ttu-id="e0492-165">Search in utterances</span><span class="sxs-lookup"><span data-stu-id="e0492-165">Search in utterances</span></span>
<span data-ttu-id="e0492-166">Searching allows you to find utterances that contain a specific text (words/phrases).</span><span class="sxs-lookup"><span data-stu-id="e0492-166">Searching allows you to find utterances that contain a specific text (words/phrases).</span></span> <span data-ttu-id="e0492-167">For example, sometimes you will notice an error that involves a particular word, and may want to find all the examples including it.</span><span class="sxs-lookup"><span data-stu-id="e0492-167">For example, sometimes you will notice an error that involves a particular word, and may want to find all the examples including it.</span></span> 

<span data-ttu-id="e0492-168">**To search in utterances:**</span><span class="sxs-lookup"><span data-stu-id="e0492-168">**To search in utterances:**</span></span>

* <span data-ttu-id="e0492-169">Type the search text in the search box at the top right corner of the utterances list and press Enter.</span><span class="sxs-lookup"><span data-stu-id="e0492-169">Type the search text in the search box at the top right corner of the utterances list and press Enter.</span></span> <span data-ttu-id="e0492-170">The utterances list will be updated to display only the utterances including your search text.</span><span class="sxs-lookup"><span data-stu-id="e0492-170">The utterances list will be updated to display only the utterances including your search text.</span></span> <span data-ttu-id="e0492-171">For example, in the following screenshot, only the utterances which contain the search word "reserve" is displayed.</span><span class="sxs-lookup"><span data-stu-id="e0492-171">For example, in the following screenshot, only the utterances which contain the search word "reserve" is displayed.</span></span> 

    ![Search in utterances](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/Search-Utter.JPG)

<span data-ttu-id="e0492-173">To cancel the search and restore your full list of utterances, delete the search text you've just typed.</span><span class="sxs-lookup"><span data-stu-id="e0492-173">To cancel the search and restore your full list of utterances, delete the search text you've just typed.</span></span>

 
## <a name="filter-utterances"></a><span data-ttu-id="e0492-174">Filter utterances</span><span class="sxs-lookup"><span data-stu-id="e0492-174">Filter utterances</span></span>
<span data-ttu-id="e0492-175">When you have a large number of utterances, it is useful to filter utterances in order to limit their view based on one or more filtering criteria.</span><span class="sxs-lookup"><span data-stu-id="e0492-175">When you have a large number of utterances, it is useful to filter utterances in order to limit their view based on one or more filtering criteria.</span></span> 

<span data-ttu-id="e0492-176">You can apply one or more filters on utterances, as needed.</span><span class="sxs-lookup"><span data-stu-id="e0492-176">You can apply one or more filters on utterances, as needed.</span></span> <span data-ttu-id="e0492-177">These are the available filters that you can use:</span><span class="sxs-lookup"><span data-stu-id="e0492-177">These are the available filters that you can use:</span></span>

- <span data-ttu-id="e0492-178">**Selected:** displays only the currently selected utterances.</span><span class="sxs-lookup"><span data-stu-id="e0492-178">**Selected:** displays only the currently selected utterances.</span></span>
- <span data-ttu-id="e0492-179">**Changed:** displays only utterances which contain unsaved changes.</span><span class="sxs-lookup"><span data-stu-id="e0492-179">**Changed:** displays only utterances which contain unsaved changes.</span></span> 
- <span data-ttu-id="e0492-180">**Errors:** displays only utterances which contain errors.</span><span class="sxs-lookup"><span data-stu-id="e0492-180">**Errors:** displays only utterances which contain errors.</span></span>
- <span data-ttu-id="e0492-181">**Entity:** displays only utterances that contain a specific entity.</span><span class="sxs-lookup"><span data-stu-id="e0492-181">**Entity:** displays only utterances that contain a specific entity.</span></span> 

>[!NOTE]
><span data-ttu-id="e0492-182">Utterances which contain unsaved changes are highlighted in light yellow.</span><span class="sxs-lookup"><span data-stu-id="e0492-182">Utterances which contain unsaved changes are highlighted in light yellow.</span></span> <span data-ttu-id="e0492-183">You can click **Save** to save changes or **Discard** to discard changes.</span><span class="sxs-lookup"><span data-stu-id="e0492-183">You can click **Save** to save changes or **Discard** to discard changes.</span></span>

<span data-ttu-id="e0492-184">**To apply filter(s):**</span><span class="sxs-lookup"><span data-stu-id="e0492-184">**To apply filter(s):**</span></span>

1. <span data-ttu-id="e0492-185">Click the filter button</span><span class="sxs-lookup"><span data-stu-id="e0492-185">Click the filter button</span></span> ![Filter button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/Filter-button.jpg)<span data-ttu-id="e0492-187">, at the top right corner of the utterances list, to display all filters.</span><span class="sxs-lookup"><span data-stu-id="e0492-187">, at the top right corner of the utterances list, to display all filters.</span></span>
2. <span data-ttu-id="e0492-188">Click on the filter(s) that you want to apply on utterances.</span><span class="sxs-lookup"><span data-stu-id="e0492-188">Click on the filter(s) that you want to apply on utterances.</span></span> <span data-ttu-id="e0492-189">For the **Entity** filter, select the entity by which you want to filter utterances.</span><span class="sxs-lookup"><span data-stu-id="e0492-189">For the **Entity** filter, select the entity by which you want to filter utterances.</span></span> 

    ![Filtering utterances](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/Filtering-utterances.JPG)

<span data-ttu-id="e0492-191">The applied filters appear as green buttons at the top left corner of the utterances list.</span><span class="sxs-lookup"><span data-stu-id="e0492-191">The applied filters appear as green buttons at the top left corner of the utterances list.</span></span> 

* <span data-ttu-id="e0492-192">To clear an applied filter, click its button at the top left corner.</span><span class="sxs-lookup"><span data-stu-id="e0492-192">To clear an applied filter, click its button at the top left corner.</span></span>
* <span data-ttu-id="e0492-193">To clear all applied filters, click all their corresponding buttons, or just click the filter button</span><span class="sxs-lookup"><span data-stu-id="e0492-193">To clear all applied filters, click all their corresponding buttons, or just click the filter button</span></span> ![Filter button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/Filter-button.jpg)<span data-ttu-id="e0492-195">.</span><span class="sxs-lookup"><span data-stu-id="e0492-195">.</span></span>


## <a name="choose-labels-view-in-utterances"></a><span data-ttu-id="e0492-196">Choose labels view in utterances</span><span class="sxs-lookup"><span data-stu-id="e0492-196">Choose labels view in utterances</span></span>
<span data-ttu-id="e0492-197">You can control how you see the words labeled as entities in the utterances by selecting one of the available views for labeled entities.</span><span class="sxs-lookup"><span data-stu-id="e0492-197">You can control how you see the words labeled as entities in the utterances by selecting one of the available views for labeled entities.</span></span>  <span data-ttu-id="e0492-198">At the top of the utterances list, select a view from the **Labels view** list.</span><span class="sxs-lookup"><span data-stu-id="e0492-198">At the top of the utterances list, select a view from the **Labels view** list.</span></span> <span data-ttu-id="e0492-199">These are the available views:</span><span class="sxs-lookup"><span data-stu-id="e0492-199">These are the available views:</span></span>

 * <span data-ttu-id="e0492-200">**Entities:** Shows entity-labeled words in tagged format (entity labels), enclosed in square brackets, with only composite entities displayed as normal text between curly brackets.</span><span class="sxs-lookup"><span data-stu-id="e0492-200">**Entities:** Shows entity-labeled words in tagged format (entity labels), enclosed in square brackets, with only composite entities displayed as normal text between curly brackets.</span></span> 
  
    ![Entities View](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/Labels-view1.JPG)
  
 * <span data-ttu-id="e0492-202">**Tokens:** Shows all entity-labeled words in text format (normal text), enclosed in square brackets except composite entities in curly brackets.</span><span class="sxs-lookup"><span data-stu-id="e0492-202">**Tokens:** Shows all entity-labeled words in text format (normal text), enclosed in square brackets except composite entities in curly brackets.</span></span> 
 
    ![Tokens View](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/Labels-view2.JPG)
 
 * <span data-ttu-id="e0492-204">**Composite entities:** Shows only the words labeled as composite entities in tagged format (entity labels), enclosed in curly brackets.</span><span class="sxs-lookup"><span data-stu-id="e0492-204">**Composite entities:** Shows only the words labeled as composite entities in tagged format (entity labels), enclosed in curly brackets.</span></span>
   
    ![Composite Entities View](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/Labels-view3.JPG)


<span data-ttu-id="e0492-206">You can press <kbd>Ctrl+E</kbd> to quickly switch between views.</span><span class="sxs-lookup"><span data-stu-id="e0492-206">You can press <kbd>Ctrl+E</kbd> to quickly switch between views.</span></span> 













