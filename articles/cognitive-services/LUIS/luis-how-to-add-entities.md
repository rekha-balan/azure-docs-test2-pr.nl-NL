---
title: Add entities in LUIS apps | Microsoft Docs
titleSuffix: Azure
description: Add entities (key data in your application's domain) in Language Understanding (LUIS) apps.
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: article
ms.date: 05/07/2018
ms.author: diberry
ms.openlocfilehash: e97f9a5391799849983bd98db5400e0a842627b7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866227"
---
# <a name="manage-entities"></a><span data-ttu-id="8e2cb-103">Manage entities</span><span class="sxs-lookup"><span data-stu-id="8e2cb-103">Manage entities</span></span>
<span data-ttu-id="8e2cb-104">After you identify your app's [intents](luis-concept-intent.md), you need to [label example utterances](luis-concept-utterance.md) with [entities](luis-concept-entity-types.md).</span><span class="sxs-lookup"><span data-stu-id="8e2cb-104">After you identify your app's [intents](luis-concept-intent.md), you need to [label example utterances](luis-concept-utterance.md) with [entities](luis-concept-entity-types.md).</span></span> <span data-ttu-id="8e2cb-105">Entities are the important pieces of a command or question, and may be essential for your client app to perform its task.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-105">Entities are the important pieces of a command or question, and may be essential for your client app to perform its task.</span></span> 

<span data-ttu-id="8e2cb-106">You can add, edit, or delete entities in your app through the **Entities list** on the **Entities** page.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-106">You can add, edit, or delete entities in your app through the **Entities list** on the **Entities** page.</span></span> <span data-ttu-id="8e2cb-107">LUIS offers two main types of entities: [prebuilt entities](luis-reference-prebuilt-entities.md), and your own custom entities.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-107">LUIS offers two main types of entities: [prebuilt entities](luis-reference-prebuilt-entities.md), and your own custom entities.</span></span>

<span data-ttu-id="8e2cb-108">The following sections are only available inside a LUIS app, from the **Build** section.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-108">The following sections are only available inside a LUIS app, from the **Build** section.</span></span> <span data-ttu-id="8e2cb-109">The **Build** link is in the top navigation bar.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-109">The **Build** link is in the top navigation bar.</span></span> <span data-ttu-id="8e2cb-110">Once inside the **Build** section, select **Entities** from the left navigation menu.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-110">Once inside the **Build** section, select **Entities** from the left navigation menu.</span></span> <span data-ttu-id="8e2cb-111">Once an entity is added to the application, if the entity is machine-learned, you can [label the entity](luis-how-to-add-example-utterances.md) inside the utterance.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-111">Once an entity is added to the application, if the entity is machine-learned, you can [label the entity](luis-how-to-add-example-utterances.md) inside the utterance.</span></span> <span data-ttu-id="8e2cb-112">Once the app is trained and published, you can receive entity data [extracted](luis-concept-data-extraction.md) from the prediction.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-112">Once the app is trained and published, you can receive entity data [extracted](luis-concept-data-extraction.md) from the prediction.</span></span> 

## <a name="add-prebuilt-entity"></a><span data-ttu-id="8e2cb-113">Add prebuilt entity</span><span class="sxs-lookup"><span data-stu-id="8e2cb-113">Add prebuilt entity</span></span>
<span data-ttu-id="8e2cb-114">Prebuilt entities are defined in the [Recognizers-Text](https://github.com/Microsoft/Recognizers-Text) project.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-114">Prebuilt entities are defined in the [Recognizers-Text](https://github.com/Microsoft/Recognizers-Text) project.</span></span> <span data-ttu-id="8e2cb-115">Common prebuilt entities added to an application are *number* and *datetimeV2*.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-115">Common prebuilt entities added to an application are *number* and *datetimeV2*.</span></span> 

1. <span data-ttu-id="8e2cb-116">In your app, from the **Build** section, and then click **Entities** in the left panel.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-116">In your app, from the **Build** section, and then click **Entities** in the left panel.</span></span>
 
2. <span data-ttu-id="8e2cb-117">On the **Entities** page, select **Manage prebuilt entities**.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-117">On the **Entities** page, select **Manage prebuilt entities**.</span></span>

    ![Screenshot of adding prebuilt entity on Entities Page](./media/add-entities/manage-prebuilt-entities-button.png)

3. <span data-ttu-id="8e2cb-119">In **Add or remove prebuilt entities** dialog box, select the **number** and **datetimeV2** prebuilt entities.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-119">In **Add or remove prebuilt entities** dialog box, select the **number** and **datetimeV2** prebuilt entities.</span></span> <span data-ttu-id="8e2cb-120">Then select **Done**.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-120">Then select **Done**.</span></span>

    ![Screenshot of Add prebuilt entity dialog box](./media/add-entities/list-of-prebuilt-entities.png)

    <span data-ttu-id="8e2cb-122">See [Data Extraction](luis-concept-data-extraction.md#prebuilt-entity-data) to learn more about extracting the prebuilt entity from the endpoint JSON query response.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-122">See [Data Extraction](luis-concept-data-extraction.md#prebuilt-entity-data) to learn more about extracting the prebuilt entity from the endpoint JSON query response.</span></span>

## <a name="add-simple-entities"></a><span data-ttu-id="8e2cb-123">Add simple entities</span><span class="sxs-lookup"><span data-stu-id="8e2cb-123">Add simple entities</span></span>
<span data-ttu-id="8e2cb-124">A simple entity is a generic entity that describes a single concept.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-124">A simple entity is a generic entity that describes a single concept.</span></span> 

1. <span data-ttu-id="8e2cb-125">In your app, from the **Build** section, and then click **Entities** in the left panel, and then select **Create new entity**.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-125">In your app, from the **Build** section, and then click **Entities** in the left panel, and then select **Create new entity**.</span></span>

    ![Screenshot of Entities page with Create new entity button highlighted](./media/add-entities/create-new-entity-button.png)

2. <span data-ttu-id="8e2cb-127">In the pop-up dialog box, type `Airline` in the **Entity name** box,  select **Simple** from the **Entity type** list, and then select **Done**.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-127">In the pop-up dialog box, type `Airline` in the **Entity name** box,  select **Simple** from the **Entity type** list, and then select **Done**.</span></span>

    ![Screenshot of dialog box for creating Airline simple entity](./media/add-entities/create-simple-airline-entity.png)

    <span data-ttu-id="8e2cb-129">See [Data Extraction](luis-concept-data-extraction.md#simple-entity-data) to learn more about extracting the simple entity from the endpoint JSON query response.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-129">See [Data Extraction](luis-concept-data-extraction.md#simple-entity-data) to learn more about extracting the simple entity from the endpoint JSON query response.</span></span> <span data-ttu-id="8e2cb-130">Try the simple entity [quickstart](luis-quickstart-primary-and-secondary-data.md) to learn more about how to use a simple entity.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-130">Try the simple entity [quickstart](luis-quickstart-primary-and-secondary-data.md) to learn more about how to use a simple entity.</span></span>

## <a name="add-regular-expression-entities"></a><span data-ttu-id="8e2cb-131">Add regular expression entities</span><span class="sxs-lookup"><span data-stu-id="8e2cb-131">Add regular expression entities</span></span>
<span data-ttu-id="8e2cb-132">A regular expression entity is used to pull out data from the utterance based on a regular expression you provide.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-132">A regular expression entity is used to pull out data from the utterance based on a regular expression you provide.</span></span> 

1. <span data-ttu-id="8e2cb-133">In your app, select **Entities** from the left navigation, and then select **Create new entity**.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-133">In your app, select **Entities** from the left navigation, and then select **Create new entity**.</span></span>

2. <span data-ttu-id="8e2cb-134">In the pop-up dialog box, , type `AirFrance Flight` in the **Entity name** box,  select **Regular expression** from the **Entity type** list, enter the regular expression `AFR[0-9]{3,4}`, and then select **Done**.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-134">In the pop-up dialog box, , type `AirFrance Flight` in the **Entity name** box,  select **Regular expression** from the **Entity type** list, enter the regular expression `AFR[0-9]{3,4}`, and then select **Done**.</span></span> 

    <span data-ttu-id="8e2cb-135">This AirFrance Flight regular expression expects three characters, literally `AFR`, then 3 or 4 digits.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-135">This AirFrance Flight regular expression expects three characters, literally `AFR`, then 3 or 4 digits.</span></span> <span data-ttu-id="8e2cb-136">The digits can be any number between 0 and 9.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-136">The digits can be any number between 0 and 9.</span></span> <span data-ttu-id="8e2cb-137">The regular expression matches AirFrance flight numbers such as: "AFR101", "ARF1302", and "AFR5006".</span><span class="sxs-lookup"><span data-stu-id="8e2cb-137">The regular expression matches AirFrance flight numbers such as: "AFR101", "ARF1302", and "AFR5006".</span></span> <span data-ttu-id="8e2cb-138">See [Data Extraction](luis-concept-data-extraction.md) to learn more about extracting the entity from the endpoint JSON query response.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-138">See [Data Extraction](luis-concept-data-extraction.md) to learn more about extracting the entity from the endpoint JSON query response.</span></span>

    ![Image of dialog box to create regular expression entity](./media/add-entities/regex-entity-create-dialog.png)

    <span data-ttu-id="8e2cb-140">See [Data Extraction](luis-concept-data-extraction.md#regular-expression-entity-data) to learn more about extracting the regular expression entity from the endpoint JSON query response.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-140">See [Data Extraction](luis-concept-data-extraction.md#regular-expression-entity-data) to learn more about extracting the regular expression entity from the endpoint JSON query response.</span></span> <span data-ttu-id="8e2cb-141">Try the regular expression entity [quickstart](luis-quickstart-intents-regex-entity.md) to learn more about how to use a regular expression entity.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-141">Try the regular expression entity [quickstart](luis-quickstart-intents-regex-entity.md) to learn more about how to use a regular expression entity.</span></span>

## <a name="add-hierarchical-entities"></a><span data-ttu-id="8e2cb-142">Add hierarchical entities</span><span class="sxs-lookup"><span data-stu-id="8e2cb-142">Add hierarchical entities</span></span>
<span data-ttu-id="8e2cb-143">A hierarchical entity is a category of contextually learned and conceptually related entities.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-143">A hierarchical entity is a category of contextually learned and conceptually related entities.</span></span> <span data-ttu-id="8e2cb-144">In the following example, the entity contains origin and destination locations.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-144">In the following example, the entity contains origin and destination locations.</span></span> 

<span data-ttu-id="8e2cb-145">In the utterance `Book 2 tickets from Seattle to Cairo`, Seattle is the origin location and Cairo is the destination location.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-145">In the utterance `Book 2 tickets from Seattle to Cairo`, Seattle is the origin location and Cairo is the destination location.</span></span> <span data-ttu-id="8e2cb-146">Each location is contextually different and learned from word order and word choice in the utterance.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-146">Each location is contextually different and learned from word order and word choice in the utterance.</span></span>

<span data-ttu-id="8e2cb-147">To add hierarchical entities, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="8e2cb-147">To add hierarchical entities, complete the following steps:</span></span> 

1. <span data-ttu-id="8e2cb-148">In your app, select **Entities** from the left navigation, and then select **Create new entity**.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-148">In your app, select **Entities** from the left navigation, and then select **Create new entity**.</span></span>

2. <span data-ttu-id="8e2cb-149">In the pop-up dialog box, type `Location` in the **Entity name** box, and then select **Hierarchical** from the **Entity type** list.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-149">In the pop-up dialog box, type `Location` in the **Entity name** box, and then select **Hierarchical** from the **Entity type** list.</span></span>

    ![Add hierarchical entity](./media/add-entities/hier-location-entity-creation.png)

3. <span data-ttu-id="8e2cb-151">Select **Add Child**, and then type "Origin" in **Child #1** box.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-151">Select **Add Child**, and then type "Origin" in **Child #1** box.</span></span> 

4. <span data-ttu-id="8e2cb-152">Select **Add Child**, and then type "Destination" in **Child #2** box.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-152">Select **Add Child**, and then type "Destination" in **Child #2** box.</span></span> <span data-ttu-id="8e2cb-153">Select **Done**.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-153">Select **Done**.</span></span>
5. 
    >[!NOTE]
    ><span data-ttu-id="8e2cb-154">To delete a child, select the trash bin icon next to it.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-154">To delete a child, select the trash bin icon next to it.</span></span>

    >[!CAUTION]
    ><span data-ttu-id="8e2cb-155">Child entity names must be unique across all entities in a single app.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-155">Child entity names must be unique across all entities in a single app.</span></span> <span data-ttu-id="8e2cb-156">Two different hierarchical entities may not contain child entities with the same name.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-156">Two different hierarchical entities may not contain child entities with the same name.</span></span> 

    <span data-ttu-id="8e2cb-157">See [Data Extraction](luis-concept-data-extraction.md#hierarchical-entity-data) to learn more about extracting the hierarchical entity from the endpoint JSON query response.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-157">See [Data Extraction](luis-concept-data-extraction.md#hierarchical-entity-data) to learn more about extracting the hierarchical entity from the endpoint JSON query response.</span></span> <span data-ttu-id="8e2cb-158">Try the hierarchical entity [quickstart](luis-quickstart-intent-and-hier-entity.md) to learn more about how to use a hierarchical entity.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-158">Try the hierarchical entity [quickstart](luis-quickstart-intent-and-hier-entity.md) to learn more about how to use a hierarchical entity.</span></span>

## <a name="add-composite-entities"></a><span data-ttu-id="8e2cb-159">Add composite entities</span><span class="sxs-lookup"><span data-stu-id="8e2cb-159">Add composite entities</span></span>
<span data-ttu-id="8e2cb-160">You can define relationships between several existing entities by creating a composite entity.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-160">You can define relationships between several existing entities by creating a composite entity.</span></span> <span data-ttu-id="8e2cb-161">In the following example, the entity contains count of tickets, origin, and destination locations.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-161">In the following example, the entity contains count of tickets, origin, and destination locations.</span></span> 

<span data-ttu-id="8e2cb-162">In the utterance `Book 2 tickets from Seattle to Cairo`, the number 2 is matched to a prebuilt entity, Seattle is the origin location and Cairo is the destination location.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-162">In the utterance `Book 2 tickets from Seattle to Cairo`, the number 2 is matched to a prebuilt entity, Seattle is the origin location and Cairo is the destination location.</span></span> <span data-ttu-id="8e2cb-163">Each entity is part of a larger, parent entity after the composite entity is created.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-163">Each entity is part of a larger, parent entity after the composite entity is created.</span></span>

1. <span data-ttu-id="8e2cb-164">In your app, add the prebuilt entity **number**.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-164">In your app, add the prebuilt entity **number**.</span></span> <span data-ttu-id="8e2cb-165">For instructions, see [Add Prebuilt Entities](#add-prebuilt-entity).</span><span class="sxs-lookup"><span data-stu-id="8e2cb-165">For instructions, see [Add Prebuilt Entities](#add-prebuilt-entity).</span></span> 

2. <span data-ttu-id="8e2cb-166">Add the hierarchical entity `Location`, including the subtypes: `origin`, `destination`.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-166">Add the hierarchical entity `Location`, including the subtypes: `origin`, `destination`.</span></span> <span data-ttu-id="8e2cb-167">For more instructions, see [Add hierarchical entities](#add-hierarchical-entities).</span><span class="sxs-lookup"><span data-stu-id="8e2cb-167">For more instructions, see [Add hierarchical entities](#add-hierarchical-entities).</span></span> 

3. <span data-ttu-id="8e2cb-168">Select **Entities** from the left navigation, and then select **Create new entity**.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-168">Select **Entities** from the left navigation, and then select **Create new entity**.</span></span>

4. <span data-ttu-id="8e2cb-169">In the pop-up dialog box, type `TicketsOrder` in the **Entity name** box, and then select **Composite** from the **Entity type** list.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-169">In the pop-up dialog box, type `TicketsOrder` in the **Entity name** box, and then select **Composite** from the **Entity type** list.</span></span>

5. <span data-ttu-id="8e2cb-170">Select **Add Child** to add a new child.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-170">Select **Add Child** to add a new child.</span></span>

6. <span data-ttu-id="8e2cb-171">In **Child #1**, select the entity **number** from the list.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-171">In **Child #1**, select the entity **number** from the list.</span></span>

7. <span data-ttu-id="8e2cb-172">In **Child #2**, select the entity **Location::Origin** from the list.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-172">In **Child #2**, select the entity **Location::Origin** from the list.</span></span> 

8. <span data-ttu-id="8e2cb-173">In **Child #3**, select the entity **Location::Destination** from the list.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-173">In **Child #3**, select the entity **Location::Destination** from the list.</span></span> 

9. <span data-ttu-id="8e2cb-174">Select **Done**.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-174">Select **Done**.</span></span>

    ![Image of dialog box to create a composite entity](./media/add-entities/ticketsorder-composite-entity.png)

    >[!NOTE]
    ><span data-ttu-id="8e2cb-176">To delete a child, select the trash button next to it.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-176">To delete a child, select the trash button next to it.</span></span>

    <span data-ttu-id="8e2cb-177">See [Data Extraction](luis-concept-data-extraction.md#composite-entity-data) to learn more about extracting the composite entity from the endpoint JSON query response.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-177">See [Data Extraction](luis-concept-data-extraction.md#composite-entity-data) to learn more about extracting the composite entity from the endpoint JSON query response.</span></span> <span data-ttu-id="8e2cb-178">Try the composite entity [tutorial](luis-tutorial-composite-entity.md) to learn more about how to use a composite entity.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-178">Try the composite entity [tutorial](luis-tutorial-composite-entity.md) to learn more about how to use a composite entity.</span></span>


## <a name="add-patternany-entities"></a><span data-ttu-id="8e2cb-179">Add Pattern.any entities</span><span class="sxs-lookup"><span data-stu-id="8e2cb-179">Add Pattern.any entities</span></span>
<span data-ttu-id="8e2cb-180">[Pattern.any](luis-concept-entity-types.md) entities are only valid in [patterns](luis-how-to-model-intent-pattern.md).</span><span class="sxs-lookup"><span data-stu-id="8e2cb-180">[Pattern.any](luis-concept-entity-types.md) entities are only valid in [patterns](luis-how-to-model-intent-pattern.md).</span></span> <span data-ttu-id="8e2cb-181">This entity helps LUIS find the end of entities of varying length and word choice.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-181">This entity helps LUIS find the end of entities of varying length and word choice.</span></span> <span data-ttu-id="8e2cb-182">Because this entity is used in a pattern, LUIS knows where the end of the entity is in the utterance.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-182">Because this entity is used in a pattern, LUIS knows where the end of the entity is in the utterance.</span></span>

<span data-ttu-id="8e2cb-183">If an app has a `FindBookInfo` intent, the title of the book may interfere with the intent prediction.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-183">If an app has a `FindBookInfo` intent, the title of the book may interfere with the intent prediction.</span></span> <span data-ttu-id="8e2cb-184">In order to clarify which words are in the book title, use a Pattern.any within a pattern.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-184">In order to clarify which words are in the book title, use a Pattern.any within a pattern.</span></span> <span data-ttu-id="8e2cb-185">The LUIS prediction begins with the utterance.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-185">The LUIS prediction begins with the utterance.</span></span> <span data-ttu-id="8e2cb-186">First, the utterance is checked and matched for entities, when the entities are found, then the pattern is checked and matched.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-186">First, the utterance is checked and matched for entities, when the entities are found, then the pattern is checked and matched.</span></span> 

<span data-ttu-id="8e2cb-187">In the utterance `Who wrote the book Ask and when was it published?`, the book title, Ask, is tricky because it is not contextually obvious where the title ends and where the rest of the utterance begins.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-187">In the utterance `Who wrote the book Ask and when was it published?`, the book title, Ask, is tricky because it is not contextually obvious where the title ends and where the rest of the utterance begins.</span></span> <span data-ttu-id="8e2cb-188">Book titles can be any order of words including a single word, complex phrases with punctuation, and nonsensical ordering of words.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-188">Book titles can be any order of words including a single word, complex phrases with punctuation, and nonsensical ordering of words.</span></span> <span data-ttu-id="8e2cb-189">A pattern allows you to create an entity where the full and exact entity can be extracted.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-189">A pattern allows you to create an entity where the full and exact entity can be extracted.</span></span> <span data-ttu-id="8e2cb-190">Once the book title is found, the `FindBookInfo` intent is predicted because that is the intent for the pattern.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-190">Once the book title is found, the `FindBookInfo` intent is predicted because that is the intent for the pattern.</span></span>

1. <span data-ttu-id="8e2cb-191">In your app, from the **Build** section, and then click **Entities** in the left panel, and then select **Create new entity**.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-191">In your app, from the **Build** section, and then click **Entities** in the left panel, and then select **Create new entity**.</span></span>

2. <span data-ttu-id="8e2cb-192">In the **Add Entity** dialog box, type `BookTitle` in the **Entity name** box and select **Pattern.any** as the **Entity type**.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-192">In the **Add Entity** dialog box, type `BookTitle` in the **Entity name** box and select **Pattern.any** as the **Entity type**.</span></span>
 
    ![Screenshot of creating a pattern.any entity](./media/add-entities/create-pattern-any-entity.png)

    <span data-ttu-id="8e2cb-194">To use the pattern.any entity, add a pattern on the **Patterns** page (under the **Improve app performance** section) with the correct curly brace syntax, such as "For **{BookTitle}** who is the author?".</span><span class="sxs-lookup"><span data-stu-id="8e2cb-194">To use the pattern.any entity, add a pattern on the **Patterns** page (under the **Improve app performance** section) with the correct curly brace syntax, such as "For **{BookTitle}** who is the author?".</span></span>

    <span data-ttu-id="8e2cb-195">See [Data Extraction](luis-concept-data-extraction.md#patternany-entity-data) to learn more about extracting the Pattern.any entity from the endpoint JSON query response.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-195">See [Data Extraction](luis-concept-data-extraction.md#patternany-entity-data) to learn more about extracting the Pattern.any entity from the endpoint JSON query response.</span></span> <span data-ttu-id="8e2cb-196">Try the [Pattern](luis-tutorial-pattern.md) tutorial to learn more about how to use a Pattern.any entity.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-196">Try the [Pattern](luis-tutorial-pattern.md) tutorial to learn more about how to use a Pattern.any entity.</span></span>

<span data-ttu-id="8e2cb-197">If you find that your pattern, when it includes a Pattern.any, extracts entities incorrectly, use an [explicit list](luis-concept-patterns.md#explicit-lists) to correct this problem.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-197">If you find that your pattern, when it includes a Pattern.any, extracts entities incorrectly, use an [explicit list](luis-concept-patterns.md#explicit-lists) to correct this problem.</span></span> 

## <a name="add-role-to-pattern-based-entity"></a><span data-ttu-id="8e2cb-198">Add role to pattern-based entity</span><span class="sxs-lookup"><span data-stu-id="8e2cb-198">Add role to pattern-based entity</span></span>
<span data-ttu-id="8e2cb-199">A role is a named subtype of an entity based on context.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-199">A role is a named subtype of an entity based on context.</span></span> <span data-ttu-id="8e2cb-200">It is comparable to a [hierarchical](#add-hierarchical-entities) entity but roles are only used in [patterns](luis-how-to-model-intent-pattern.md).</span><span class="sxs-lookup"><span data-stu-id="8e2cb-200">It is comparable to a [hierarchical](#add-hierarchical-entities) entity but roles are only used in [patterns](luis-how-to-model-intent-pattern.md).</span></span> 

<span data-ttu-id="8e2cb-201">For example, a plane ticket has an *origin city* and a *destination city*, but both are cities.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-201">For example, a plane ticket has an *origin city* and a *destination city*, but both are cities.</span></span> <span data-ttu-id="8e2cb-202">LUIS determines that both are cities and can determine origin and destination cities based on context of word order and word choice.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-202">LUIS determines that both are cities and can determine origin and destination cities based on context of word order and word choice.</span></span> 

<span data-ttu-id="8e2cb-203">The syntax for a role is **{Entity name:Role name}** where the entity name is followed by a colon, then the role name.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-203">The syntax for a role is **{Entity name:Role name}** where the entity name is followed by a colon, then the role name.</span></span> <span data-ttu-id="8e2cb-204">For example, "Book a ticket from {Location:Origin} to {Location:Destination}".</span><span class="sxs-lookup"><span data-stu-id="8e2cb-204">For example, "Book a ticket from {Location:Origin} to {Location:Destination}".</span></span>

1. <span data-ttu-id="8e2cb-205">In your app, from the **Build** section, and then select **Entities** in the left panel.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-205">In your app, from the **Build** section, and then select **Entities** in the left panel.</span></span>

2. <span data-ttu-id="8e2cb-206">Select **Create new entity**.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-206">Select **Create new entity**.</span></span> <span data-ttu-id="8e2cb-207">Enter the name of `Location`.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-207">Enter the name of `Location`.</span></span> <span data-ttu-id="8e2cb-208">Select the type **Simple** and select **Done**</span><span class="sxs-lookup"><span data-stu-id="8e2cb-208">Select the type **Simple** and select **Done**</span></span>

3. <span data-ttu-id="8e2cb-209">Select **Entities** from the left panel, then select the new entity **Location** created in step 2.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-209">Select **Entities** from the left panel, then select the new entity **Location** created in step 2.</span></span>

4. <span data-ttu-id="8e2cb-210">In the **Role name** textbox, enter the name of the role `Origin` and enter.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-210">In the **Role name** textbox, enter the name of the role `Origin` and enter.</span></span> <span data-ttu-id="8e2cb-211">Add a second role name of `Destination`.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-211">Add a second role name of `Destination`.</span></span> <span data-ttu-id="8e2cb-212">As an example, a plane trip can have an origin and a destination city.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-212">As an example, a plane trip can have an origin and a destination city.</span></span> <span data-ttu-id="8e2cb-213">The two roles are "Origin" and "Destination".</span><span class="sxs-lookup"><span data-stu-id="8e2cb-213">The two roles are "Origin" and "Destination".</span></span>

    ![Screenshot of adding Origin role to Location entity](./media/add-entities/roles-enter-role-name-text.png)

    <span data-ttu-id="8e2cb-215">See [Data Extraction](luis-concept-data-extraction.md) to learn more about extracting roles from the endpoint JSON query response.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-215">See [Data Extraction](luis-concept-data-extraction.md) to learn more about extracting roles from the endpoint JSON query response.</span></span> <span data-ttu-id="8e2cb-216">Try the pattern tutorial to learn more about how to use a Pattern.any entity.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-216">Try the pattern tutorial to learn more about how to use a Pattern.any entity.</span></span>

## <a name="add-list-entities"></a><span data-ttu-id="8e2cb-217">Add list entities</span><span class="sxs-lookup"><span data-stu-id="8e2cb-217">Add list entities</span></span>
<span data-ttu-id="8e2cb-218">List entities represent a fixed, closed set of related words in your system.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-218">List entities represent a fixed, closed set of related words in your system.</span></span> 

<span data-ttu-id="8e2cb-219">For a drinks list entity, you can have two normalized values: water and soda pop.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-219">For a drinks list entity, you can have two normalized values: water and soda pop.</span></span> <span data-ttu-id="8e2cb-220">Each normalized name has synonyms.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-220">Each normalized name has synonyms.</span></span> <span data-ttu-id="8e2cb-221">For water, synonyms are H20, gas, flat.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-221">For water, synonyms are H20, gas, flat.</span></span> <span data-ttu-id="8e2cb-222">For soda pop, synonyms are fruit, cola, ginger.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-222">For soda pop, synonyms are fruit, cola, ginger.</span></span> <span data-ttu-id="8e2cb-223">You don't have to know all the values when you create the entity.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-223">You don't have to know all the values when you create the entity.</span></span> <span data-ttu-id="8e2cb-224">You can add more after reviewing real user utterances with synonyms.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-224">You can add more after reviewing real user utterances with synonyms.</span></span>

|<span data-ttu-id="8e2cb-225">Normalized name</span><span class="sxs-lookup"><span data-stu-id="8e2cb-225">Normalized name</span></span>|<span data-ttu-id="8e2cb-226">Synonyms</span><span class="sxs-lookup"><span data-stu-id="8e2cb-226">Synonyms</span></span>|
|--|--|
|<span data-ttu-id="8e2cb-227">Water</span><span class="sxs-lookup"><span data-stu-id="8e2cb-227">Water</span></span>|<span data-ttu-id="8e2cb-228">H20, gas, flat</span><span class="sxs-lookup"><span data-stu-id="8e2cb-228">H20, gas, flat</span></span>|
|<span data-ttu-id="8e2cb-229">Soda pop</span><span class="sxs-lookup"><span data-stu-id="8e2cb-229">Soda pop</span></span>|<span data-ttu-id="8e2cb-230">Fruit, cola, ginger</span><span class="sxs-lookup"><span data-stu-id="8e2cb-230">Fruit, cola, ginger</span></span>|

1. <span data-ttu-id="8e2cb-231">In your app, from the **Build** section, and then click **Entities** in the left panel, and then select **Create new entity**.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-231">In your app, from the **Build** section, and then click **Entities** in the left panel, and then select **Create new entity**.</span></span>

2. <span data-ttu-id="8e2cb-232">In the **Add Entity** dialog box, type `Drinks` in the **Entity name** box and select **List** as the **Entity type**.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-232">In the **Add Entity** dialog box, type `Drinks` in the **Entity name** box and select **List** as the **Entity type**.</span></span> <span data-ttu-id="8e2cb-233">Select **Done**.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-233">Select **Done**.</span></span>
 
    ![Image of dialog box creating Drinks list entity](./media/add-entities/menu-list-dialog.png)
  
3.  <span data-ttu-id="8e2cb-235">The list entity page allows you to add normalized names.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-235">The list entity page allows you to add normalized names.</span></span> <span data-ttu-id="8e2cb-236">In the **Values** textbox, enter an item for the list, such as `Water` for the drinks list then press Enter on the keyboard.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-236">In the **Values** textbox, enter an item for the list, such as `Water` for the drinks list then press Enter on the keyboard.</span></span> 

    ![Screenshot of Drinks list entity with water normalized value in textbox](./media/add-entities/entity-list-normalized-name.png)

4. <span data-ttu-id="8e2cb-238">To the right of the normalized value **water**, enter synonyms `h20`, `flat`, and `gas`, pressing Enter on the keyboard after each item.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-238">To the right of the normalized value **water**, enter synonyms `h20`, `flat`, and `gas`, pressing Enter on the keyboard after each item.</span></span>

    ![Screenshot of Drinks list entity with synonym items for water highlighted](./media/add-entities/menu-list-synonyms.png)

5. <span data-ttu-id="8e2cb-240">If you want more normalized items for the list, select **Recommend** to see options from the [semantic dictionary](luis-glossary.md#semantic-dictionary).</span><span class="sxs-lookup"><span data-stu-id="8e2cb-240">If you want more normalized items for the list, select **Recommend** to see options from the [semantic dictionary](luis-glossary.md#semantic-dictionary).</span></span>

    ![Screenshot of Drink list entity with Recommended items highlighted](./media/add-entities/entity-list-recommended-list.png)

6. <span data-ttu-id="8e2cb-242">Select an item in the recommended list to add it as a normalized value or select **Add all** to add all the items.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-242">Select an item in the recommended list to add it as a normalized value or select **Add all** to add all the items.</span></span> 

    ![Screenshot of Drink list entity with recommended item of beer and Add all button highlighted](./media/add-entities/list-entity-add-suggestions.png)

    <span data-ttu-id="8e2cb-244">See [Data Extraction](luis-concept-data-extraction.md#list-entity-data) to learn more about extracting list entities from the endpoint JSON query response.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-244">See [Data Extraction](luis-concept-data-extraction.md#list-entity-data) to learn more about extracting list entities from the endpoint JSON query response.</span></span> <span data-ttu-id="8e2cb-245">Try the [quickstart](luis-quickstart-intent-and-list-entity.md) to learn more about how to use a list entity.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-245">Try the [quickstart](luis-quickstart-intent-and-list-entity.md) to learn more about how to use a list entity.</span></span>

## <a name="import-list-entity-values"></a><span data-ttu-id="8e2cb-246">Import list entity values</span><span class="sxs-lookup"><span data-stu-id="8e2cb-246">Import list entity values</span></span>
<span data-ttu-id="8e2cb-247">You can import values into an existing list entity.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-247">You can import values into an existing list entity.</span></span>

 1. <span data-ttu-id="8e2cb-248">On the list entity page, select **Import Lists**.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-248">On the list entity page, select **Import Lists**.</span></span>

 2. <span data-ttu-id="8e2cb-249">In **Import New Entries** dialog box, select **Choose File** and select the JSON file that includes the list.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-249">In **Import New Entries** dialog box, select **Choose File** and select the JSON file that includes the list.</span></span>

    ![Screenshot of Import list entity values pop-up dialog box](./media/add-entities/menu-list-import-json-dialog-with-file.png)

    >[!NOTE]
    ><span data-ttu-id="8e2cb-251">LUIS imports files with the extension ".json" only.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-251">LUIS imports files with the extension ".json" only.</span></span>

 3. <span data-ttu-id="8e2cb-252">To learn about the supported list syntax in JSON, select **Learn about supported list syntax** to expand the dialog and display an example of allowed syntax.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-252">To learn about the supported list syntax in JSON, select **Learn about supported list syntax** to expand the dialog and display an example of allowed syntax.</span></span> <span data-ttu-id="8e2cb-253">To collapse the dialog and hide syntax, select the link title again.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-253">To collapse the dialog and hide syntax, select the link title again.</span></span>

 4. <span data-ttu-id="8e2cb-254">Select **Done**.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-254">Select **Done**.</span></span>

    <span data-ttu-id="8e2cb-255">An example of valid json for a **Colors** list entity is shown in the following JSON-formatted code:</span><span class="sxs-lookup"><span data-stu-id="8e2cb-255">An example of valid json for a **Colors** list entity is shown in the following JSON-formatted code:</span></span>

    ```
    [
        {
            "canonicalForm": "Blue",
            "list": [
                "navy",
                "royal",
                "baby"
            ]
        },
        {
            "canonicalForm": "Green",
            "list": [
                "kelly",
                "forest",
                "avacado"
            ]
        }
    ]  
    ```

## <a name="edit-entity-name"></a><span data-ttu-id="8e2cb-256">Edit entity name</span><span class="sxs-lookup"><span data-stu-id="8e2cb-256">Edit entity name</span></span>
1. <span data-ttu-id="8e2cb-257">On the **Entities** list page, select the entity in the list.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-257">On the **Entities** list page, select the entity in the list.</span></span> <span data-ttu-id="8e2cb-258">This action takes you to the **Entity** page.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-258">This action takes you to the **Entity** page.</span></span>

2. <span data-ttu-id="8e2cb-259">On the **Entity** page, you edit the entity name by selecting the edit icon next to the entity name.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-259">On the **Entity** page, you edit the entity name by selecting the edit icon next to the entity name.</span></span> <span data-ttu-id="8e2cb-260">The entity type is not editable.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-260">The entity type is not editable.</span></span> 

## <a name="delete-entity"></a><span data-ttu-id="8e2cb-261">Delete entity</span><span class="sxs-lookup"><span data-stu-id="8e2cb-261">Delete entity</span></span>

<span data-ttu-id="8e2cb-262">On the **Entity** page, select the **Delete Entity** button.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-262">On the **Entity** page, select the **Delete Entity** button.</span></span> <span data-ttu-id="8e2cb-263">Then, select **Ok** in the confirmation message to confirm deletion.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-263">Then, select **Ok** in the confirmation message to confirm deletion.</span></span>
 
![Screenshot of Location entity page with Delete Entity button highlighted](./media/add-entities/entity-delete.png)

>[!NOTE]
>* <span data-ttu-id="8e2cb-265">Deleting a hierarchical entity deletes all its children entities.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-265">Deleting a hierarchical entity deletes all its children entities.</span></span>
>* <span data-ttu-id="8e2cb-266">Deleting a composite entity deletes only the composite and breaks the composite relationship, but doesn't delete the entities forming it.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-266">Deleting a composite entity deletes only the composite and breaks the composite relationship, but doesn't delete the entities forming it.</span></span>

## <a name="changing-entity-type"></a><span data-ttu-id="8e2cb-267">Changing entity type</span><span class="sxs-lookup"><span data-stu-id="8e2cb-267">Changing entity type</span></span>
<span data-ttu-id="8e2cb-268">LUIS does not allow you to change the type of the entity because it doesn't know what to add or remove to construct that entity.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-268">LUIS does not allow you to change the type of the entity because it doesn't know what to add or remove to construct that entity.</span></span> <span data-ttu-id="8e2cb-269">In order to change the type, it is better to create a new entity of the correct type with a slightly different name.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-269">In order to change the type, it is better to create a new entity of the correct type with a slightly different name.</span></span> <span data-ttu-id="8e2cb-270">Once the entity is created, in each utterance, remove the old labeled entity name and add the new entity name.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-270">Once the entity is created, in each utterance, remove the old labeled entity name and add the new entity name.</span></span> <span data-ttu-id="8e2cb-271">Once all the utterances have been relabeled, delete the old entity.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-271">Once all the utterances have been relabeled, delete the old entity.</span></span> 

## <a name="create-a-pattern-from-an-utterance"></a><span data-ttu-id="8e2cb-272">Create a pattern from an utterance</span><span class="sxs-lookup"><span data-stu-id="8e2cb-272">Create a pattern from an utterance</span></span>
<span data-ttu-id="8e2cb-273">See [Add pattern from existing utterance on intent or entity page](luis-how-to-model-intent-pattern.md#add-pattern-from-existing-utterance-on-intent-or-entity-page).</span><span class="sxs-lookup"><span data-stu-id="8e2cb-273">See [Add pattern from existing utterance on intent or entity page](luis-how-to-model-intent-pattern.md#add-pattern-from-existing-utterance-on-intent-or-entity-page).</span></span>

## <a name="search-utterances"></a><span data-ttu-id="8e2cb-274">Search utterances</span><span class="sxs-lookup"><span data-stu-id="8e2cb-274">Search utterances</span></span>
<span data-ttu-id="8e2cb-275">You can search and filter utterances with the magnifying glass icon on the toolbar.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-275">You can search and filter utterances with the magnifying glass icon on the toolbar.</span></span> 

## <a name="train-your-app-after-changing-model-with-entities"></a><span data-ttu-id="8e2cb-276">Train your app after changing model with entities</span><span class="sxs-lookup"><span data-stu-id="8e2cb-276">Train your app after changing model with entities</span></span>
<span data-ttu-id="8e2cb-277">After you add, edit, or remove entities, [train](luis-how-to-train.md) and [publish](luis-how-to-publish-app.md) your app for your changes to affect endpoint queries.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-277">After you add, edit, or remove entities, [train](luis-how-to-train.md) and [publish](luis-how-to-publish-app.md) your app for your changes to affect endpoint queries.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="8e2cb-278">Next steps</span><span class="sxs-lookup"><span data-stu-id="8e2cb-278">Next steps</span></span>
<span data-ttu-id="8e2cb-279">Now that you have added intents, utterances and entities, you have a basic LUIS app.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-279">Now that you have added intents, utterances and entities, you have a basic LUIS app.</span></span> <span data-ttu-id="8e2cb-280">Learn how to [train](luis-how-to-train.md), [test](luis-interactive-test.md), and [publish](luis-how-to-publish-app.md) your app.</span><span class="sxs-lookup"><span data-stu-id="8e2cb-280">Learn how to [train](luis-how-to-train.md), [test](luis-interactive-test.md), and [publish](luis-how-to-publish-app.md) your app.</span></span>
 
