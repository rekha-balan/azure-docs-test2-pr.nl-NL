---
title: Add example utterances in LUIS apps
titleSuffix: Azure Cognitive Services
description: Learn how to add utterances in Language Understanding (LUIS) applications.
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: article
ms.date: 09/06/2018
ms.author: diberry
ms.openlocfilehash: eb859dfd2dca37415d074e8a0398be37fcc0a6b8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871418"
---
# <a name="add-example-utterances-and-label-with-entities"></a><span data-ttu-id="c3900-103">Add example utterances and label with entities</span><span class="sxs-lookup"><span data-stu-id="c3900-103">Add example utterances and label with entities</span></span>

<span data-ttu-id="c3900-104">Example utterances are text examples of user questions or commands.</span><span class="sxs-lookup"><span data-stu-id="c3900-104">Example utterances are text examples of user questions or commands.</span></span> <span data-ttu-id="c3900-105">To teach Language Understanding (LUIS), you need to add [example utterances](luis-concept-utterance.md) to an [intent](luis-concept-intent.md).</span><span class="sxs-lookup"><span data-stu-id="c3900-105">To teach Language Understanding (LUIS), you need to add [example utterances](luis-concept-utterance.md) to an [intent](luis-concept-intent.md).</span></span>

<span data-ttu-id="c3900-106">Generally, add an example utterance to an intent first, and then create entities and label utterances on the intent page.</span><span class="sxs-lookup"><span data-stu-id="c3900-106">Generally, add an example utterance to an intent first, and then create entities and label utterances on the intent page.</span></span> <span data-ttu-id="c3900-107">If you would rather create entities first, see [Add entities](luis-how-to-add-entities.md).</span><span class="sxs-lookup"><span data-stu-id="c3900-107">If you would rather create entities first, see [Add entities](luis-how-to-add-entities.md).</span></span>

## <a name="add-an-utterance"></a><span data-ttu-id="c3900-108">Add an utterance</span><span class="sxs-lookup"><span data-stu-id="c3900-108">Add an utterance</span></span>
<span data-ttu-id="c3900-109">On an intent page, enter a relevant example utterance you expect from your users, such as `book 2 adult business tickets to Paris tomorrow on Air France` in the text box below the intent name, and then press Enter.</span><span class="sxs-lookup"><span data-stu-id="c3900-109">On an intent page, enter a relevant example utterance you expect from your users, such as `book 2 adult business tickets to Paris tomorrow on Air France` in the text box below the intent name, and then press Enter.</span></span> 
 
>[!NOTE]
><span data-ttu-id="c3900-110">LUIS converts all utterances to lowercase.</span><span class="sxs-lookup"><span data-stu-id="c3900-110">LUIS converts all utterances to lowercase.</span></span>

![Screenshot of Intents details page, with utterance highlighted](./media/luis-how-to-add-example-utterances/add-new-utterance-to-intent.png) 

<span data-ttu-id="c3900-112">Utterances are added to the utterances list for the current intent.</span><span class="sxs-lookup"><span data-stu-id="c3900-112">Utterances are added to the utterances list for the current intent.</span></span> 

## <a name="ignoring-words-and-punctuation"></a><span data-ttu-id="c3900-113">Ignoring words and punctuation</span><span class="sxs-lookup"><span data-stu-id="c3900-113">Ignoring words and punctuation</span></span>
<span data-ttu-id="c3900-114">If you want to ignore specific words or punctuation in the example utterance, use a [pattern](luis-concept-patterns.md#pattern-syntax) with the _ignore_ syntax.</span><span class="sxs-lookup"><span data-stu-id="c3900-114">If you want to ignore specific words or punctuation in the example utterance, use a [pattern](luis-concept-patterns.md#pattern-syntax) with the _ignore_ syntax.</span></span> 

## <a name="add-simple-entity-label"></a><span data-ttu-id="c3900-115">Add simple entity label</span><span class="sxs-lookup"><span data-stu-id="c3900-115">Add simple entity label</span></span>
<span data-ttu-id="c3900-116">In the following procedure, you create and label custom entities within the following utterance on the intent page:</span><span class="sxs-lookup"><span data-stu-id="c3900-116">In the following procedure, you create and label custom entities within the following utterance on the intent page:</span></span>

```
book me 2 adult business tickets to Paris tomorrow on Air France
```

1. <span data-ttu-id="c3900-117">Select "Air France" in the utterance to label it as a simple entity.</span><span class="sxs-lookup"><span data-stu-id="c3900-117">Select "Air France" in the utterance to label it as a simple entity.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c3900-118">When selecting words to label them as entities:</span><span class="sxs-lookup"><span data-stu-id="c3900-118">When selecting words to label them as entities:</span></span>
    > * <span data-ttu-id="c3900-119">For a single word, just select it.</span><span class="sxs-lookup"><span data-stu-id="c3900-119">For a single word, just select it.</span></span> 
    > * <span data-ttu-id="c3900-120">For a set of two or more words, select at the beginning and then at the end of the set.</span><span class="sxs-lookup"><span data-stu-id="c3900-120">For a set of two or more words, select at the beginning and then at the end of the set.</span></span>

2. <span data-ttu-id="c3900-121">In the entity drop-down box that appears, you can either select an existing entity or add a new entity.</span><span class="sxs-lookup"><span data-stu-id="c3900-121">In the entity drop-down box that appears, you can either select an existing entity or add a new entity.</span></span> <span data-ttu-id="c3900-122">To add a new entity, type its name in the text box, and then select **Create new entity**.</span><span class="sxs-lookup"><span data-stu-id="c3900-122">To add a new entity, type its name in the text box, and then select **Create new entity**.</span></span> 
 
    ![Screenshot of Intents details page, with simple entity labeling option highlighted](./media/luis-how-to-add-example-utterances/create-airline-simple-entity.png)

3. <span data-ttu-id="c3900-124">In the **What type of entity do you want to create?** pop-up dialog box, verify the entity name and select the simple entity type, and then select **Done**.</span><span class="sxs-lookup"><span data-stu-id="c3900-124">In the **What type of entity do you want to create?** pop-up dialog box, verify the entity name and select the simple entity type, and then select **Done**.</span></span>

    ![Image of confirmation dialog](./media/luis-how-to-add-example-utterances/create-simple-airline-entity.png)

    <span data-ttu-id="c3900-126">See [Data Extraction](luis-concept-data-extraction.md#simple-entity-data) to learn more about extracting the simple entity from the endpoint JSON query response.</span><span class="sxs-lookup"><span data-stu-id="c3900-126">See [Data Extraction](luis-concept-data-extraction.md#simple-entity-data) to learn more about extracting the simple entity from the endpoint JSON query response.</span></span> <span data-ttu-id="c3900-127">Try the simple entity [quickstart](luis-quickstart-primary-and-secondary-data.md) to learn more about how to use a simple entity.</span><span class="sxs-lookup"><span data-stu-id="c3900-127">Try the simple entity [quickstart](luis-quickstart-primary-and-secondary-data.md) to learn more about how to use a simple entity.</span></span>


## <a name="add-list-entity-and-label"></a><span data-ttu-id="c3900-128">Add list entity and label</span><span class="sxs-lookup"><span data-stu-id="c3900-128">Add list entity and label</span></span>
<span data-ttu-id="c3900-129">List entities represent a fixed, closed set (exact text matches) of related words in your system.</span><span class="sxs-lookup"><span data-stu-id="c3900-129">List entities represent a fixed, closed set (exact text matches) of related words in your system.</span></span> 

<span data-ttu-id="c3900-130">For a drinks list entity, you can have two normalized values: water and soda pop.</span><span class="sxs-lookup"><span data-stu-id="c3900-130">For a drinks list entity, you can have two normalized values: water and soda pop.</span></span> <span data-ttu-id="c3900-131">Each normalized name has synonyms.</span><span class="sxs-lookup"><span data-stu-id="c3900-131">Each normalized name has synonyms.</span></span> <span data-ttu-id="c3900-132">For water, synonyms are H20, gas, flat.</span><span class="sxs-lookup"><span data-stu-id="c3900-132">For water, synonyms are H20, gas, flat.</span></span> <span data-ttu-id="c3900-133">For soda pop, synonyms are fruit, cola, ginger.</span><span class="sxs-lookup"><span data-stu-id="c3900-133">For soda pop, synonyms are fruit, cola, ginger.</span></span> <span data-ttu-id="c3900-134">You don't have to know all the values when you create the entity.</span><span class="sxs-lookup"><span data-stu-id="c3900-134">You don't have to know all the values when you create the entity.</span></span> <span data-ttu-id="c3900-135">You can add more after reviewing real user utterances with synonyms.</span><span class="sxs-lookup"><span data-stu-id="c3900-135">You can add more after reviewing real user utterances with synonyms.</span></span>

|<span data-ttu-id="c3900-136">Normalized name</span><span class="sxs-lookup"><span data-stu-id="c3900-136">Normalized name</span></span>|<span data-ttu-id="c3900-137">Synonyms</span><span class="sxs-lookup"><span data-stu-id="c3900-137">Synonyms</span></span>|
|--|--|
|<span data-ttu-id="c3900-138">Water</span><span class="sxs-lookup"><span data-stu-id="c3900-138">Water</span></span>|<span data-ttu-id="c3900-139">H20, gas, flat</span><span class="sxs-lookup"><span data-stu-id="c3900-139">H20, gas, flat</span></span>|
|<span data-ttu-id="c3900-140">Soda pop</span><span class="sxs-lookup"><span data-stu-id="c3900-140">Soda pop</span></span>|<span data-ttu-id="c3900-141">Fruit, cola, ginger</span><span class="sxs-lookup"><span data-stu-id="c3900-141">Fruit, cola, ginger</span></span>|

<span data-ttu-id="c3900-142">When creating a new list entity from the intent page, you are doing two things that may not be obvious.</span><span class="sxs-lookup"><span data-stu-id="c3900-142">When creating a new list entity from the intent page, you are doing two things that may not be obvious.</span></span> <span data-ttu-id="c3900-143">First, you are creating a new list by adding the first list item.</span><span class="sxs-lookup"><span data-stu-id="c3900-143">First, you are creating a new list by adding the first list item.</span></span> <span data-ttu-id="c3900-144">Second, the first list item is named with the word or phrase you selected from the utterance.</span><span class="sxs-lookup"><span data-stu-id="c3900-144">Second, the first list item is named with the word or phrase you selected from the utterance.</span></span> <span data-ttu-id="c3900-145">While you can change these later from the entity page, it may be faster to select an utterance that has the word that you want for the name of the list item.</span><span class="sxs-lookup"><span data-stu-id="c3900-145">While you can change these later from the entity page, it may be faster to select an utterance that has the word that you want for the name of the list item.</span></span>

<span data-ttu-id="c3900-146">For example, if you wanted to create a list of types of drink and you selected the word `h2o` from the utterance to create the entity, the list would have one item, whose name was h20.</span><span class="sxs-lookup"><span data-stu-id="c3900-146">For example, if you wanted to create a list of types of drink and you selected the word `h2o` from the utterance to create the entity, the list would have one item, whose name was h20.</span></span> <span data-ttu-id="c3900-147">If you wanted a more generic name, you should choose an utterance that uses the more generic name.</span><span class="sxs-lookup"><span data-stu-id="c3900-147">If you wanted a more generic name, you should choose an utterance that uses the more generic name.</span></span> 

1. <span data-ttu-id="c3900-148">In the utterance, select the word that is the first item in the list, and then enter the name of the list in the textbox, then select **Create new entity**.</span><span class="sxs-lookup"><span data-stu-id="c3900-148">In the utterance, select the word that is the first item in the list, and then enter the name of the list in the textbox, then select **Create new entity**.</span></span>   

    ![Screenshot of Intents details page, with Create new entity highlighted](./media/luis-how-to-add-example-utterances/create-drink-list-entity.png)

2. <span data-ttu-id="c3900-150">In the **What type of entity do you want to create?** dialog box, add synonyms of this list item.</span><span class="sxs-lookup"><span data-stu-id="c3900-150">In the **What type of entity do you want to create?** dialog box, add synonyms of this list item.</span></span> <span data-ttu-id="c3900-151">For the water item in a drink list, add `h20`, `perrier`, and `waters`, and select **Done**.</span><span class="sxs-lookup"><span data-stu-id="c3900-151">For the water item in a drink list, add `h20`, `perrier`, and `waters`, and select **Done**.</span></span> <span data-ttu-id="c3900-152">Notice that "waters" is added because the list synonyms are matched at the token level.</span><span class="sxs-lookup"><span data-stu-id="c3900-152">Notice that "waters" is added because the list synonyms are matched at the token level.</span></span> <span data-ttu-id="c3900-153">In the English culture, that level is at the word level so "waters" would not be matched to "water" unless it was in the list.</span><span class="sxs-lookup"><span data-stu-id="c3900-153">In the English culture, that level is at the word level so "waters" would not be matched to "water" unless it was in the list.</span></span> 

    ![Screenshot of What type of entity do you want to create dialog box](./media/luis-how-to-add-example-utterances/drink-list-ddl.png)

    <span data-ttu-id="c3900-155">This list of drinks has only one drink type, water.</span><span class="sxs-lookup"><span data-stu-id="c3900-155">This list of drinks has only one drink type, water.</span></span> <span data-ttu-id="c3900-156">You can add more drink types by labeling other utterances, or by editing the entity from the **Entities** in the left navigation.</span><span class="sxs-lookup"><span data-stu-id="c3900-156">You can add more drink types by labeling other utterances, or by editing the entity from the **Entities** in the left navigation.</span></span> <span data-ttu-id="c3900-157">[Editing](luis-how-to-add-entities.md#add-list-entities) the entities gives you the options of entering additional items with corresponding synonyms or [importing](luis-how-to-add-entities.md#import-list-entity-values) a list.</span><span class="sxs-lookup"><span data-stu-id="c3900-157">[Editing](luis-how-to-add-entities.md#add-list-entities) the entities gives you the options of entering additional items with corresponding synonyms or [importing](luis-how-to-add-entities.md#import-list-entity-values) a list.</span></span> 

    <span data-ttu-id="c3900-158">See [Data Extraction](luis-concept-data-extraction.md#list-entity-data) to learn more about extracting list entities from the endpoint JSON query response.</span><span class="sxs-lookup"><span data-stu-id="c3900-158">See [Data Extraction](luis-concept-data-extraction.md#list-entity-data) to learn more about extracting list entities from the endpoint JSON query response.</span></span> <span data-ttu-id="c3900-159">Try the [quickstart](luis-quickstart-intent-and-list-entity.md) to learn more about how to use a list entity.</span><span class="sxs-lookup"><span data-stu-id="c3900-159">Try the [quickstart](luis-quickstart-intent-and-list-entity.md) to learn more about how to use a list entity.</span></span>

## <a name="add-synonyms-to-the-list-entity"></a><span data-ttu-id="c3900-160">Add synonyms to the list entity</span><span class="sxs-lookup"><span data-stu-id="c3900-160">Add synonyms to the list entity</span></span> 
<span data-ttu-id="c3900-161">Add a synonym to the list entity by selecting the word or phrase in the utterance.</span><span class="sxs-lookup"><span data-stu-id="c3900-161">Add a synonym to the list entity by selecting the word or phrase in the utterance.</span></span> <span data-ttu-id="c3900-162">If you have a Drink list entity, and want to add `agua` as a synonym for water, follow the steps:</span><span class="sxs-lookup"><span data-stu-id="c3900-162">If you have a Drink list entity, and want to add `agua` as a synonym for water, follow the steps:</span></span>

<span data-ttu-id="c3900-163">In the utterance, select the synonymous word, such as `aqua` for water, then select the list entity name in the drop-down list, such as **Drink**, then select **Set as synonym**, then select the list item it is synonymous with, such as **water**.</span><span class="sxs-lookup"><span data-stu-id="c3900-163">In the utterance, select the synonymous word, such as `aqua` for water, then select the list entity name in the drop-down list, such as **Drink**, then select **Set as synonym**, then select the list item it is synonymous with, such as **water**.</span></span>

![Screenshot of Intents details page, with Create a new synonym highlighted](./media/luis-how-to-add-example-utterances/set-agua-as-synonym.png)

## <a name="create-new-item-for-list-entity"></a><span data-ttu-id="c3900-165">Create new item for list entity</span><span class="sxs-lookup"><span data-stu-id="c3900-165">Create new item for list entity</span></span>
<span data-ttu-id="c3900-166">Create a new item for an existing list entity by selecting the word or phrase in the utterance.</span><span class="sxs-lookup"><span data-stu-id="c3900-166">Create a new item for an existing list entity by selecting the word or phrase in the utterance.</span></span> <span data-ttu-id="c3900-167">If you have a Drink list, and want to add `tea` as a new item, follow the steps:</span><span class="sxs-lookup"><span data-stu-id="c3900-167">If you have a Drink list, and want to add `tea` as a new item, follow the steps:</span></span>

<span data-ttu-id="c3900-168">In the utterance, select the word for the new list item, such as `tea`, then select the list entity name in the drop-down list, such as **Drink**, then select **Create a new synonym**.</span><span class="sxs-lookup"><span data-stu-id="c3900-168">In the utterance, select the word for the new list item, such as `tea`, then select the list entity name in the drop-down list, such as **Drink**, then select **Create a new synonym**.</span></span> 

![Screenshot of adding new list item](./media/luis-how-to-add-example-utterances/list-entity-create-new-item.png)

<span data-ttu-id="c3900-170">The word is now highlighted in blue.</span><span class="sxs-lookup"><span data-stu-id="c3900-170">The word is now highlighted in blue.</span></span> <span data-ttu-id="c3900-171">If you hover over the word, a tag displays showing the list item name, such as tea.</span><span class="sxs-lookup"><span data-stu-id="c3900-171">If you hover over the word, a tag displays showing the list item name, such as tea.</span></span>

![Screenshot of new list item tag](./media/luis-how-to-add-example-utterances/list-entity-item-name-tag.png)

## <a name="wrap-entities-in-composite-label"></a><span data-ttu-id="c3900-173">Wrap entities in composite label</span><span class="sxs-lookup"><span data-stu-id="c3900-173">Wrap entities in composite label</span></span>
<span data-ttu-id="c3900-174">Composite entities are created from **Entities**.</span><span class="sxs-lookup"><span data-stu-id="c3900-174">Composite entities are created from **Entities**.</span></span> <span data-ttu-id="c3900-175">You can't create a composite entity from the Intent page.</span><span class="sxs-lookup"><span data-stu-id="c3900-175">You can't create a composite entity from the Intent page.</span></span> <span data-ttu-id="c3900-176">Once the composite entity is created, you can wrap the entities in an utterance on the Intent page.</span><span class="sxs-lookup"><span data-stu-id="c3900-176">Once the composite entity is created, you can wrap the entities in an utterance on the Intent page.</span></span> 

<span data-ttu-id="c3900-177">Assuming the utterance, `book 2 tickets from Seattle to Cairo`, a composite utterance can return entity information of the count of tickets (2), the origin (Seattle), and destination (Cairo) locations in a single parent entity.</span><span class="sxs-lookup"><span data-stu-id="c3900-177">Assuming the utterance, `book 2 tickets from Seattle to Cairo`, a composite utterance can return entity information of the count of tickets (2), the origin (Seattle), and destination (Cairo) locations in a single parent entity.</span></span> 

<span data-ttu-id="c3900-178">Follow these [steps](luis-how-to-add-entities.md#add-prebuilt-entity) to add the **number** prebuilt entity.</span><span class="sxs-lookup"><span data-stu-id="c3900-178">Follow these [steps](luis-how-to-add-entities.md#add-prebuilt-entity) to add the **number** prebuilt entity.</span></span> <span data-ttu-id="c3900-179">After the entity is created, the `2` in the utterance is blue, indicating it is a labeled entity.</span><span class="sxs-lookup"><span data-stu-id="c3900-179">After the entity is created, the `2` in the utterance is blue, indicating it is a labeled entity.</span></span> <span data-ttu-id="c3900-180">Prebuilt entities are labeled by LUIS.</span><span class="sxs-lookup"><span data-stu-id="c3900-180">Prebuilt entities are labeled by LUIS.</span></span> <span data-ttu-id="c3900-181">You can't add or remove the prebuilt entity label from a single utterance.</span><span class="sxs-lookup"><span data-stu-id="c3900-181">You can't add or remove the prebuilt entity label from a single utterance.</span></span> <span data-ttu-id="c3900-182">You can only add or remove all the prebuilt labels by adding or removing the prebuilt entity from the application.</span><span class="sxs-lookup"><span data-stu-id="c3900-182">You can only add or remove all the prebuilt labels by adding or removing the prebuilt entity from the application.</span></span>

<span data-ttu-id="c3900-183">Follow these [steps](#add-hierarchical-entity-and-label) to create a **Location** hierarchical entity.</span><span class="sxs-lookup"><span data-stu-id="c3900-183">Follow these [steps](#add-hierarchical-entity-and-label) to create a **Location** hierarchical entity.</span></span> <span data-ttu-id="c3900-184">Label the origin and destination locations in the example utterance.</span><span class="sxs-lookup"><span data-stu-id="c3900-184">Label the origin and destination locations in the example utterance.</span></span> 

<span data-ttu-id="c3900-185">Before you wrap the entities in a composite entity, make sure all the child entities are highlighted in blue, meaning they have been labeled in the utterance.</span><span class="sxs-lookup"><span data-stu-id="c3900-185">Before you wrap the entities in a composite entity, make sure all the child entities are highlighted in blue, meaning they have been labeled in the utterance.</span></span>

1. <span data-ttu-id="c3900-186">To wrap the individual entities into a composite, select the first labeled entity in the utterance for the composite entity.</span><span class="sxs-lookup"><span data-stu-id="c3900-186">To wrap the individual entities into a composite, select the first labeled entity in the utterance for the composite entity.</span></span> <span data-ttu-id="c3900-187">In the example utterance, `book 2 tickets from Seattle to Cairo`, the first entity is the number 2.</span><span class="sxs-lookup"><span data-stu-id="c3900-187">In the example utterance, `book 2 tickets from Seattle to Cairo`, the first entity is the number 2.</span></span> <span data-ttu-id="c3900-188">A drop-down list appears showing the choices for this selection.</span><span class="sxs-lookup"><span data-stu-id="c3900-188">A drop-down list appears showing the choices for this selection.</span></span>

    ![Screenshot of number selected and drop-down options highlighted](./media/luis-how-to-add-example-utterances/wrap-1.png)

2. <span data-ttu-id="c3900-190">Select **Wrap composite entity** from the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="c3900-190">Select **Wrap composite entity** from the drop-down list.</span></span> 

    ![Screenshot of drop-down options for wrapping composite entity with Wrap in composite entity highlighted](./media/luis-how-to-add-example-utterances/wrap-2.png)

3. <span data-ttu-id="c3900-192">Select the last word of the composite entity.</span><span class="sxs-lookup"><span data-stu-id="c3900-192">Select the last word of the composite entity.</span></span> <span data-ttu-id="c3900-193">In the utterance of this example, select "Location::Destination" (representing Cairo).</span><span class="sxs-lookup"><span data-stu-id="c3900-193">In the utterance of this example, select "Location::Destination" (representing Cairo).</span></span> <span data-ttu-id="c3900-194">The green line is now under all the words, including non-entity words, in the utterance that are the composite.</span><span class="sxs-lookup"><span data-stu-id="c3900-194">The green line is now under all the words, including non-entity words, in the utterance that are the composite.</span></span>

    ![Screenshot of BookFlight Intent page, with number highlighted](./media/luis-how-to-add-example-utterances/wrap-composite.png)

4. <span data-ttu-id="c3900-196">Select the composite entity name from the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="c3900-196">Select the composite entity name from the drop-down list.</span></span> <span data-ttu-id="c3900-197">For this example, that is **TicketOrder**.</span><span class="sxs-lookup"><span data-stu-id="c3900-197">For this example, that is **TicketOrder**.</span></span>

    ![Screenshot of wrapping words with composite entity, with composite entity name highlighted in drop-down list](./media/luis-how-to-add-example-utterances/wrap-4.png)

    <span data-ttu-id="c3900-199">When you wrap the entities correctly, a green line is under the entire phrase.</span><span class="sxs-lookup"><span data-stu-id="c3900-199">When you wrap the entities correctly, a green line is under the entire phrase.</span></span>

    ![Screenshot of utterance with composite entity highlighted](./media/luis-how-to-add-example-utterances/wrap-5.png)

    <span data-ttu-id="c3900-201">See [Data Extraction](luis-concept-data-extraction.md#composite-entity-data) to learn more about extracting the composite entity from the endpoint JSON query response.</span><span class="sxs-lookup"><span data-stu-id="c3900-201">See [Data Extraction](luis-concept-data-extraction.md#composite-entity-data) to learn more about extracting the composite entity from the endpoint JSON query response.</span></span> <span data-ttu-id="c3900-202">Try the composite entity [tutorial](luis-tutorial-composite-entity.md) to learn more about how to use a composite entity.</span><span class="sxs-lookup"><span data-stu-id="c3900-202">Try the composite entity [tutorial](luis-tutorial-composite-entity.md) to learn more about how to use a composite entity.</span></span>

## <a name="add-hierarchical-entity-and-label"></a><span data-ttu-id="c3900-203">Add hierarchical entity and label</span><span class="sxs-lookup"><span data-stu-id="c3900-203">Add hierarchical entity and label</span></span>
<span data-ttu-id="c3900-204">A hierarchical entity is a category of contextually learned and conceptually related entities.</span><span class="sxs-lookup"><span data-stu-id="c3900-204">A hierarchical entity is a category of contextually learned and conceptually related entities.</span></span> <span data-ttu-id="c3900-205">In the following example, the entity contains origin and destination locations.</span><span class="sxs-lookup"><span data-stu-id="c3900-205">In the following example, the entity contains origin and destination locations.</span></span> 

<span data-ttu-id="c3900-206">In the utterance `Book 2 tickets from Seattle to Cairo`, Seattle is the origin location and Cairo is the destination location.</span><span class="sxs-lookup"><span data-stu-id="c3900-206">In the utterance `Book 2 tickets from Seattle to Cairo`, Seattle is the origin location and Cairo is the destination location.</span></span> <span data-ttu-id="c3900-207">Each location is contextually different and learned from word order and word choice in the utterance.</span><span class="sxs-lookup"><span data-stu-id="c3900-207">Each location is contextually different and learned from word order and word choice in the utterance.</span></span>

1. <span data-ttu-id="c3900-208">On the Intent page, in the utterance, select "Seattle", then enter the entity name \`Location, and then select **Create new entity**.</span><span class="sxs-lookup"><span data-stu-id="c3900-208">On the Intent page, in the utterance, select "Seattle", then enter the entity name \`Location, and then select **Create new entity**.</span></span>

    ![Screenshot of Create Hierarchical Entity Labeling dialog box](./media/luis-how-to-add-example-utterances/create-hier-ent-1.png)

2. <span data-ttu-id="c3900-210">In the pop-up dialog box, select hierarchical for **Entity type**, then add `Origin` and `Destination` as children, and then select **Done**.</span><span class="sxs-lookup"><span data-stu-id="c3900-210">In the pop-up dialog box, select hierarchical for **Entity type**, then add `Origin` and `Destination` as children, and then select **Done**.</span></span>

    ![Screenshot of Intents details page, with ToLocation entity highlighted](./media/luis-how-to-add-example-utterances/create-location-hierarchical-entity.png)

3. <span data-ttu-id="c3900-212">The word in the utterance was labeled with the parent hierarchical entity.</span><span class="sxs-lookup"><span data-stu-id="c3900-212">The word in the utterance was labeled with the parent hierarchical entity.</span></span> <span data-ttu-id="c3900-213">You need to assign the word to a child entity.</span><span class="sxs-lookup"><span data-stu-id="c3900-213">You need to assign the word to a child entity.</span></span> <span data-ttu-id="c3900-214">Return to the utterance on the intent page.</span><span class="sxs-lookup"><span data-stu-id="c3900-214">Return to the utterance on the intent page.</span></span> <span data-ttu-id="c3900-215">Select the word, then from the drop-down list choose the entity name you created, and follow the menu to the right to choose the correct child entity.</span><span class="sxs-lookup"><span data-stu-id="c3900-215">Select the word, then from the drop-down list choose the entity name you created, and follow the menu to the right to choose the correct child entity.</span></span>

    ![Screenshot of Intents details page, with ToLocation entity highlighted](./media/luis-how-to-add-example-utterances/label-tolocation.png)

    >[!CAUTION]
    ><span data-ttu-id="c3900-217">Child entity names must be unique across all entities in a single app.</span><span class="sxs-lookup"><span data-stu-id="c3900-217">Child entity names must be unique across all entities in a single app.</span></span> <span data-ttu-id="c3900-218">Two different hierarchical entities may not contain child entities with the same name.</span><span class="sxs-lookup"><span data-stu-id="c3900-218">Two different hierarchical entities may not contain child entities with the same name.</span></span> 

    <span data-ttu-id="c3900-219">See [Data Extraction](luis-concept-data-extraction.md#hierarchical-entity-data) to learn more about extracting the hierarchical entity from the endpoint JSON query response.</span><span class="sxs-lookup"><span data-stu-id="c3900-219">See [Data Extraction](luis-concept-data-extraction.md#hierarchical-entity-data) to learn more about extracting the hierarchical entity from the endpoint JSON query response.</span></span> <span data-ttu-id="c3900-220">Try the hierarchical entity [quickstart](luis-quickstart-intent-and-hier-entity.md) to learn more about how to use a hierarchical entity.</span><span class="sxs-lookup"><span data-stu-id="c3900-220">Try the hierarchical entity [quickstart](luis-quickstart-intent-and-hier-entity.md) to learn more about how to use a hierarchical entity.</span></span>


## <a name="remove-entity-labels-from-utterances"></a><span data-ttu-id="c3900-221">Remove entity labels from utterances</span><span class="sxs-lookup"><span data-stu-id="c3900-221">Remove entity labels from utterances</span></span>
<span data-ttu-id="c3900-222">You can remove machine-learned entity labels from an utterance on the Intent page.</span><span class="sxs-lookup"><span data-stu-id="c3900-222">You can remove machine-learned entity labels from an utterance on the Intent page.</span></span> <span data-ttu-id="c3900-223">If the entity is not machine-learned, it can't be removed from an utterance.</span><span class="sxs-lookup"><span data-stu-id="c3900-223">If the entity is not machine-learned, it can't be removed from an utterance.</span></span> <span data-ttu-id="c3900-224">If you need to remove a non-machine-learned entity from the utterance, you need to delete the entity from the entire app.</span><span class="sxs-lookup"><span data-stu-id="c3900-224">If you need to remove a non-machine-learned entity from the utterance, you need to delete the entity from the entire app.</span></span> 

<span data-ttu-id="c3900-225">To remove a machine-learned entity label from an utterance, select the entity in the utterance.</span><span class="sxs-lookup"><span data-stu-id="c3900-225">To remove a machine-learned entity label from an utterance, select the entity in the utterance.</span></span> <span data-ttu-id="c3900-226">Then select **Remove Label** in the entity drop-down box that appears.</span><span class="sxs-lookup"><span data-stu-id="c3900-226">Then select **Remove Label** in the entity drop-down box that appears.</span></span>

![Screenshot of Intents details page, with Remove Label highlighted](./media/luis-how-to-add-example-utterances/remove-label.png) 

## <a name="add-prebuilt-entity-label"></a><span data-ttu-id="c3900-228">Add prebuilt entity label</span><span class="sxs-lookup"><span data-stu-id="c3900-228">Add prebuilt entity label</span></span>
<span data-ttu-id="c3900-229">If you add the prebuilt entities to your LUIS app, you don't need to label utterances with these entities.</span><span class="sxs-lookup"><span data-stu-id="c3900-229">If you add the prebuilt entities to your LUIS app, you don't need to label utterances with these entities.</span></span> <span data-ttu-id="c3900-230">To learn more about prebuilt entities and how to add them, see [Add entities](luis-how-to-add-entities.md#add-prebuilt-entity).</span><span class="sxs-lookup"><span data-stu-id="c3900-230">To learn more about prebuilt entities and how to add them, see [Add entities](luis-how-to-add-entities.md#add-prebuilt-entity).</span></span>

## <a name="add-regular-expression-entity-label"></a><span data-ttu-id="c3900-231">Add regular expression entity label</span><span class="sxs-lookup"><span data-stu-id="c3900-231">Add regular expression entity label</span></span>
<span data-ttu-id="c3900-232">If you add the regular expression entities to your LUIS app, you don't need to label utterances with these entities.</span><span class="sxs-lookup"><span data-stu-id="c3900-232">If you add the regular expression entities to your LUIS app, you don't need to label utterances with these entities.</span></span> <span data-ttu-id="c3900-233">To learn more about regular expression entities and how to add them, see [Add entities](luis-how-to-add-entities.md#add-regular-expression-entities).</span><span class="sxs-lookup"><span data-stu-id="c3900-233">To learn more about regular expression entities and how to add them, see [Add entities](luis-how-to-add-entities.md#add-regular-expression-entities).</span></span>

## <a name="create-a-pattern-from-an-utterance"></a><span data-ttu-id="c3900-234">Create a pattern from an utterance</span><span class="sxs-lookup"><span data-stu-id="c3900-234">Create a pattern from an utterance</span></span>
<span data-ttu-id="c3900-235">See [Add pattern from existing utterance on intent or entity page](luis-how-to-model-intent-pattern.md#add-pattern-from-existing-utterance-on-intent-or-entity-page).</span><span class="sxs-lookup"><span data-stu-id="c3900-235">See [Add pattern from existing utterance on intent or entity page](luis-how-to-model-intent-pattern.md#add-pattern-from-existing-utterance-on-intent-or-entity-page).</span></span>

## <a name="add-patternany-entity-label"></a><span data-ttu-id="c3900-236">Add pattern.any entity label</span><span class="sxs-lookup"><span data-stu-id="c3900-236">Add pattern.any entity label</span></span>
<span data-ttu-id="c3900-237">If you add the pattern.any entities to your LUIS app, you can't label utterances with these entities.</span><span class="sxs-lookup"><span data-stu-id="c3900-237">If you add the pattern.any entities to your LUIS app, you can't label utterances with these entities.</span></span> <span data-ttu-id="c3900-238">They are only valid in patterns.</span><span class="sxs-lookup"><span data-stu-id="c3900-238">They are only valid in patterns.</span></span> <span data-ttu-id="c3900-239">To learn more about pattern.any entities and how to add them, see [Add entities](luis-how-to-add-entities.md#add-patternany-entities).</span><span class="sxs-lookup"><span data-stu-id="c3900-239">To learn more about pattern.any entities and how to add them, see [Add entities](luis-how-to-add-entities.md#add-patternany-entities).</span></span>

<!--
Fix this - moved to luis-how-to-add-intents.md - how ?

## Search in utterances
## Prediction discrepancy errors
## Filter by intent prediction discrepancy errors
## Filter by entity type
## Switch to token view
## Delete utterances
## Edit an utterance
## Reassign utterances

-->
## <a name="train-your-app-after-changing-model-with-utterances"></a><span data-ttu-id="c3900-240">Train your app after changing model with utterances</span><span class="sxs-lookup"><span data-stu-id="c3900-240">Train your app after changing model with utterances</span></span>
<span data-ttu-id="c3900-241">After you add, edit, or remove utterances, [train](luis-how-to-train.md) and [publish](luis-how-to-publish-app.md) your app for your changes to affect endpoint queries.</span><span class="sxs-lookup"><span data-stu-id="c3900-241">After you add, edit, or remove utterances, [train](luis-how-to-train.md) and [publish](luis-how-to-publish-app.md) your app for your changes to affect endpoint queries.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="c3900-242">Next steps</span><span class="sxs-lookup"><span data-stu-id="c3900-242">Next steps</span></span>

<span data-ttu-id="c3900-243">After labeling utterances in your intents, you can now create a [composite entity](luis-how-to-add-entities.md).</span><span class="sxs-lookup"><span data-stu-id="c3900-243">After labeling utterances in your intents, you can now create a [composite entity](luis-how-to-add-entities.md).</span></span>
