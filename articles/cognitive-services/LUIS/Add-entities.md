---
title: Add entities in LUIS apps | Microsoft Docs
description: Add entities (key data in your application's domain) in Language Understanding Intelligent Services (LUIS) apps.
services: cognitive-services
author: cahann
manager: hsalama
ms.service: cognitive-services
ms.technology: luis
ms.topic: article
ms.date: 03/01/2017
ms.author: cahann
ms.openlocfilehash: 212239613428bd0a2fa62493cb059e09f31440e0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549154"
---
# <a name="add-entities"></a><span data-ttu-id="350e9-103">Add Entities</span><span class="sxs-lookup"><span data-stu-id="350e9-103">Add Entities</span></span>
<span data-ttu-id="350e9-104">Entities are key data in your application’s domain.</span><span class="sxs-lookup"><span data-stu-id="350e9-104">Entities are key data in your application’s domain.</span></span> <span data-ttu-id="350e9-105">An entity represents a class including a collection of similar objects (places, things, people, events or concepts).</span><span class="sxs-lookup"><span data-stu-id="350e9-105">An entity represents a class including a collection of similar objects (places, things, people, events or concepts).</span></span> <span data-ttu-id="350e9-106">Entities describe information relevant to the intent, and sometimes they are essential for your app to perform its task.</span><span class="sxs-lookup"><span data-stu-id="350e9-106">Entities describe information relevant to the intent, and sometimes they are essential for your app to perform its task.</span></span> <span data-ttu-id="350e9-107">For example, a News Search app may include entities such as “topic”, “source”, “keyword” and “publishing date”, which are key data to search for news.</span><span class="sxs-lookup"><span data-stu-id="350e9-107">For example, a News Search app may include entities such as “topic”, “source”, “keyword” and “publishing date”, which are key data to search for news.</span></span> <span data-ttu-id="350e9-108">In a travel booking app, the “location”, “date”, "airline", "travel class" and "tickets" are key information for flight booking (relevant to the "Bookflight" intent).</span><span class="sxs-lookup"><span data-stu-id="350e9-108">In a travel booking app, the “location”, “date”, "airline", "travel class" and "tickets" are key information for flight booking (relevant to the "Bookflight" intent).</span></span> <span data-ttu-id="350e9-109">So, we'll add them as entities.</span><span class="sxs-lookup"><span data-stu-id="350e9-109">So, we'll add them as entities.</span></span> 

<span data-ttu-id="350e9-110">You do not need to create entities for every concept in your app, but only for those required for the app to take action.</span><span class="sxs-lookup"><span data-stu-id="350e9-110">You do not need to create entities for every concept in your app, but only for those required for the app to take action.</span></span> <span data-ttu-id="350e9-111">You can add up to **10** entities in a single LUIS app.</span><span class="sxs-lookup"><span data-stu-id="350e9-111">You can add up to **10** entities in a single LUIS app.</span></span> 

<span data-ttu-id="350e9-112">You can add, edit or delete entities in your app through the **Entities list** on the **Entities** page.</span><span class="sxs-lookup"><span data-stu-id="350e9-112">You can add, edit or delete entities in your app through the **Entities list** on the **Entities** page.</span></span> <span data-ttu-id="350e9-113">Luis offers many types of entities; prebuilt entities, custom machine learned entities and close list entities.</span><span class="sxs-lookup"><span data-stu-id="350e9-113">Luis offers many types of entities; prebuilt entities, custom machine learned entities and close list entities.</span></span>


## <a name="add-prebuilt-entities"></a><span data-ttu-id="350e9-114">Add Prebuilt Entities</span><span class="sxs-lookup"><span data-stu-id="350e9-114">Add Prebuilt Entities</span></span>
<span data-ttu-id="350e9-115">LUIS provides a set of prebuilt (system-defined) entities, covering many examples of the most common knowledge concepts such as date, age, temperature, percentage, dimension, cardinal and ordinal numbers, etc.</span><span class="sxs-lookup"><span data-stu-id="350e9-115">LUIS provides a set of prebuilt (system-defined) entities, covering many examples of the most common knowledge concepts such as date, age, temperature, percentage, dimension, cardinal and ordinal numbers, etc.</span></span>  

<span data-ttu-id="350e9-116">For example, the TravelAgent app may receive a request like "Book me a flight to Boston on May 4".</span><span class="sxs-lookup"><span data-stu-id="350e9-116">For example, the TravelAgent app may receive a request like "Book me a flight to Boston on May 4".</span></span> <span data-ttu-id="350e9-117">This will require your app to understand date and time words in order to interpret the request properly.</span><span class="sxs-lookup"><span data-stu-id="350e9-117">This will require your app to understand date and time words in order to interpret the request properly.</span></span> <span data-ttu-id="350e9-118">Rather than creating entities for such concepts from scratch, you can enable a ready-made prebuilt entity called "datetime".</span><span class="sxs-lookup"><span data-stu-id="350e9-118">Rather than creating entities for such concepts from scratch, you can enable a ready-made prebuilt entity called "datetime".</span></span> 

<span data-ttu-id="350e9-119">As another example, a travel booking request like “Book me the first flight to Boston” might be sent to your app.</span><span class="sxs-lookup"><span data-stu-id="350e9-119">As another example, a travel booking request like “Book me the first flight to Boston” might be sent to your app.</span></span> <span data-ttu-id="350e9-120">This requires understanding of ordinal words (e.g. first, second).</span><span class="sxs-lookup"><span data-stu-id="350e9-120">This requires understanding of ordinal words (e.g. first, second).</span></span> <span data-ttu-id="350e9-121">Therefore, you must add a prebuilt entity called "ordinal", for your app to recognize ordinal numbers.</span><span class="sxs-lookup"><span data-stu-id="350e9-121">Therefore, you must add a prebuilt entity called "ordinal", for your app to recognize ordinal numbers.</span></span>

<span data-ttu-id="350e9-122">For a full list of prebuilt entities and their use, see [Prebuilt Entities List](Pre-builtEntities.md).</span><span class="sxs-lookup"><span data-stu-id="350e9-122">For a full list of prebuilt entities and their use, see [Prebuilt Entities List](Pre-builtEntities.md).</span></span>

<span data-ttu-id="350e9-123">**To add a prebuilt entity:**</span><span class="sxs-lookup"><span data-stu-id="350e9-123">**To add a prebuilt entity:**</span></span>

1. <span data-ttu-id="350e9-124">Open the TravelAgent app by clicking its name on **My Apps** page, and then click **Entities** in the left panel.</span><span class="sxs-lookup"><span data-stu-id="350e9-124">Open the TravelAgent app by clicking its name on **My Apps** page, and then click **Entities** in the left panel.</span></span> 
2. <span data-ttu-id="350e9-125">On the **Entities** page, click **Add prebuilt entity**.</span><span class="sxs-lookup"><span data-stu-id="350e9-125">On the **Entities** page, click **Add prebuilt entity**.</span></span>

    ![Entities Page - Add first entity](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/EntitiesPage-AddFirstEntity.JPG)
3. <span data-ttu-id="350e9-127">In **Add prebuilt entities** dialog box, click the prebuilt entity you want to add  (e.g. “datetime”), and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="350e9-127">In **Add prebuilt entities** dialog box, click the prebuilt entity you want to add  (e.g. “datetime”), and then click **Save**.</span></span>

    ![Add prebuilt entity dialog box](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/AddPrebuilt-Dialogbox.JPG)


## <a name="add-custom-entities"></a><span data-ttu-id="350e9-129">Add Custom Entities</span><span class="sxs-lookup"><span data-stu-id="350e9-129">Add Custom Entities</span></span>
<span data-ttu-id="350e9-130">Custom entities are the entities you create in your app.</span><span class="sxs-lookup"><span data-stu-id="350e9-130">Custom entities are the entities you create in your app.</span></span> <span data-ttu-id="350e9-131">There are three types of custom entities:</span><span class="sxs-lookup"><span data-stu-id="350e9-131">There are three types of custom entities:</span></span>

* <span data-ttu-id="350e9-132">**Simple:** a generic entity.</span><span class="sxs-lookup"><span data-stu-id="350e9-132">**Simple:** a generic entity.</span></span>
* <span data-ttu-id="350e9-133">**Hierarchical:** a parent including children (sub-types) which are dependent on the parent.</span><span class="sxs-lookup"><span data-stu-id="350e9-133">**Hierarchical:** a parent including children (sub-types) which are dependent on the parent.</span></span>
* <span data-ttu-id="350e9-134">**Composite:** a compound of two or more separate entities combined together forming a composite and treated as a single entity.</span><span class="sxs-lookup"><span data-stu-id="350e9-134">**Composite:** a compound of two or more separate entities combined together forming a composite and treated as a single entity.</span></span>


### <a name="simple-entities"></a><span data-ttu-id="350e9-135">Simple Entities</span><span class="sxs-lookup"><span data-stu-id="350e9-135">Simple Entities</span></span>
<span data-ttu-id="350e9-136">A simple entity is a generic entity that describes a single concept.</span><span class="sxs-lookup"><span data-stu-id="350e9-136">A simple entity is a generic entity that describes a single concept.</span></span> <span data-ttu-id="350e9-137">In the example of the TravelAgent app, a user may say "Book me a flight to London tomorrow on British Airways", where "British Airways" is the name of an airline company.</span><span class="sxs-lookup"><span data-stu-id="350e9-137">In the example of the TravelAgent app, a user may say "Book me a flight to London tomorrow on British Airways", where "British Airways" is the name of an airline company.</span></span> <span data-ttu-id="350e9-138">In order to capture the notion of airline names, let's create the entity "Airline".</span><span class="sxs-lookup"><span data-stu-id="350e9-138">In order to capture the notion of airline names, let's create the entity "Airline".</span></span> 

<span data-ttu-id="350e9-139">**To add a simple entity:**</span><span class="sxs-lookup"><span data-stu-id="350e9-139">**To add a simple entity:**</span></span>

1. <span data-ttu-id="350e9-140">Open the TravelAgent app by clicking its name on **My Apps** page, and then click **Entities** in the left panel.</span><span class="sxs-lookup"><span data-stu-id="350e9-140">Open the TravelAgent app by clicking its name on **My Apps** page, and then click **Entities** in the left panel.</span></span> 
2. <span data-ttu-id="350e9-141">On the **Entities** page, click **Add custom entity**.</span><span class="sxs-lookup"><span data-stu-id="350e9-141">On the **Entities** page, click **Add custom entity**.</span></span>
3. <span data-ttu-id="350e9-142">In the **Add Entity** dialog box, type "Airline" in the **Entity name** box,  select **Simple** from the **Entity type** list, and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="350e9-142">In the **Add Entity** dialog box, type "Airline" in the **Entity name** box,  select **Simple** from the **Entity type** list, and then click **Save**.</span></span>

    ![Add Entity Dialog box - Simple](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/AddSimpleEntity.jpg)


### <a name="hierarchical-entities"></a><span data-ttu-id="350e9-144">Hierarchical Entities</span><span class="sxs-lookup"><span data-stu-id="350e9-144">Hierarchical Entities</span></span>
<span data-ttu-id="350e9-145">You can define relationships between entities based on hereditary hierarchical patterns, where the generic entity acts as the parent and the children are sub-types under the parent, and they share the same characteristics.</span><span class="sxs-lookup"><span data-stu-id="350e9-145">You can define relationships between entities based on hereditary hierarchical patterns, where the generic entity acts as the parent and the children are sub-types under the parent, and they share the same characteristics.</span></span> <span data-ttu-id="350e9-146">For example, in the TravelAgent app, you can add three hierarchical entities:</span><span class="sxs-lookup"><span data-stu-id="350e9-146">For example, in the TravelAgent app, you can add three hierarchical entities:</span></span>

* <span data-ttu-id="350e9-147">“Location”, including the entity children “FromLocation” and “ToLocation”, representing source and destination locations.</span><span class="sxs-lookup"><span data-stu-id="350e9-147">“Location”, including the entity children “FromLocation” and “ToLocation”, representing source and destination locations.</span></span>
* <span data-ttu-id="350e9-148">"TravelClass", including the travel classes as children ("first", "business" and "economy")</span><span class="sxs-lookup"><span data-stu-id="350e9-148">"TravelClass", including the travel classes as children ("first", "business" and "economy")</span></span>
* <span data-ttu-id="350e9-149">"Category", including ticket categories ("adult", "child" and "infant").</span><span class="sxs-lookup"><span data-stu-id="350e9-149">"Category", including ticket categories ("adult", "child" and "infant").</span></span>

<span data-ttu-id="350e9-150">Do the following steps to add hierarchical entities and make sure to add the children at the same time you are creating the parent entity.</span><span class="sxs-lookup"><span data-stu-id="350e9-150">Do the following steps to add hierarchical entities and make sure to add the children at the same time you are creating the parent entity.</span></span> <span data-ttu-id="350e9-151">You can add up to 10 entity children for each parent.</span><span class="sxs-lookup"><span data-stu-id="350e9-151">You can add up to 10 entity children for each parent.</span></span>

<span data-ttu-id="350e9-152">**To add a hierarchical entity:**</span><span class="sxs-lookup"><span data-stu-id="350e9-152">**To add a hierarchical entity:**</span></span>

1. <span data-ttu-id="350e9-153">Open the TravelAgent app by clicking its name on **My Apps** page, and then click **Entities** in the left panel.</span><span class="sxs-lookup"><span data-stu-id="350e9-153">Open the TravelAgent app by clicking its name on **My Apps** page, and then click **Entities** in the left panel.</span></span> 
2. <span data-ttu-id="350e9-154">On the **Entities** page, click **Add custom entity**.</span><span class="sxs-lookup"><span data-stu-id="350e9-154">On the **Entities** page, click **Add custom entity**.</span></span>
3. <span data-ttu-id="350e9-155">In the **Add Entity** dialog box, type "Location" in the **Entity name** box, and then select **Hierarchical** from the **Entity type** list.</span><span class="sxs-lookup"><span data-stu-id="350e9-155">In the **Add Entity** dialog box, type "Location" in the **Entity name** box, and then select **Hierarchical** from the **Entity type** list.</span></span>

    ![Add hierarchical entity](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/AddHierarchicalEntity.JPG)

4. <span data-ttu-id="350e9-157">Click **Add Child**, and then type "FromLocation" in **Child #1** box.</span><span class="sxs-lookup"><span data-stu-id="350e9-157">Click **Add Child**, and then type "FromLocation" in **Child #1** box.</span></span> 
5. <span data-ttu-id="350e9-158">Click **Add Child**, and then type "ToLocation" in **Child #2** box.</span><span class="sxs-lookup"><span data-stu-id="350e9-158">Click **Add Child**, and then type "ToLocation" in **Child #2** box.</span></span> 
    >[!NOTE]
    ><span data-ttu-id="350e9-159">To delete a child (in case of a mistake), click the trash bin icon next to it.</span><span class="sxs-lookup"><span data-stu-id="350e9-159">To delete a child (in case of a mistake), click the trash bin icon next to it.</span></span>

6. <span data-ttu-id="350e9-160">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="350e9-160">Click **Save**.</span></span>

 
### <a name="composite-entities"></a><span data-ttu-id="350e9-161">Composite Entities</span><span class="sxs-lookup"><span data-stu-id="350e9-161">Composite Entities</span></span>
<span data-ttu-id="350e9-162">You can also define relationships between entities based on associative patterns by creating “composite entities”.</span><span class="sxs-lookup"><span data-stu-id="350e9-162">You can also define relationships between entities based on associative patterns by creating “composite entities”.</span></span> <span data-ttu-id="350e9-163">A composite entity is created by combining two or more existing entities (simple or hierarchical) and treating them as one entity.</span><span class="sxs-lookup"><span data-stu-id="350e9-163">A composite entity is created by combining two or more existing entities (simple or hierarchical) and treating them as one entity.</span></span> <span data-ttu-id="350e9-164">Unlike a hierarchical entity, the composite entity and the children forming it are not in a parent-child relationship; they are independent of each other and they do not share common characteristics.</span><span class="sxs-lookup"><span data-stu-id="350e9-164">Unlike a hierarchical entity, the composite entity and the children forming it are not in a parent-child relationship; they are independent of each other and they do not share common characteristics.</span></span> <span data-ttu-id="350e9-165">The composite pattern enables your app to identify entities, not only individually, but also in groups.</span><span class="sxs-lookup"><span data-stu-id="350e9-165">The composite pattern enables your app to identify entities, not only individually, but also in groups.</span></span> 

<span data-ttu-id="350e9-166">In the TravelAgent app example, a user may say “Book 2 adult business tickets to Paris next Monday”.</span><span class="sxs-lookup"><span data-stu-id="350e9-166">In the TravelAgent app example, a user may say “Book 2 adult business tickets to Paris next Monday”.</span></span> <span data-ttu-id="350e9-167">In this example, we can create a composite entity called “TicketsOrder”, including three children entities: “number”, “category” and "class" which describe the tickets to be booked.</span><span class="sxs-lookup"><span data-stu-id="350e9-167">In this example, we can create a composite entity called “TicketsOrder”, including three children entities: “number”, “category” and "class" which describe the tickets to be booked.</span></span> <span data-ttu-id="350e9-168">Before creating a composite entity, you must first add the entities forming it, if they do not already exist.</span><span class="sxs-lookup"><span data-stu-id="350e9-168">Before creating a composite entity, you must first add the entities forming it, if they do not already exist.</span></span> 

<span data-ttu-id="350e9-169">**To add the entities forming the composite:**</span><span class="sxs-lookup"><span data-stu-id="350e9-169">**To add the entities forming the composite:**</span></span>

1. <span data-ttu-id="350e9-170">Add the prebuilt entity “number”.</span><span class="sxs-lookup"><span data-stu-id="350e9-170">Add the prebuilt entity “number”.</span></span> <span data-ttu-id="350e9-171">For instructions, see the Add Prebuilt Entities section above.</span><span class="sxs-lookup"><span data-stu-id="350e9-171">For instructions, see the Add Prebuilt Entities section above.</span></span> 
2. <span data-ttu-id="350e9-172">Add the hierarchical entity "Category", including the sub-types: “adult”, “child” and “infant”, and "TravelClass" including "first", "business" and "economy".</span><span class="sxs-lookup"><span data-stu-id="350e9-172">Add the hierarchical entity "Category", including the sub-types: “adult”, “child” and “infant”, and "TravelClass" including "first", "business" and "economy".</span></span> <span data-ttu-id="350e9-173">For more info, see the Hierarchical Entities section above.</span><span class="sxs-lookup"><span data-stu-id="350e9-173">For more info, see the Hierarchical Entities section above.</span></span> 

<span data-ttu-id="350e9-174">**To add the composite entity:**</span><span class="sxs-lookup"><span data-stu-id="350e9-174">**To add the composite entity:**</span></span>

1. <span data-ttu-id="350e9-175">Open the TravelAgent app by clicking its name on **My Apps** page and click **Entities** in the app's left panel.</span><span class="sxs-lookup"><span data-stu-id="350e9-175">Open the TravelAgent app by clicking its name on **My Apps** page and click **Entities** in the app's left panel.</span></span>
2. <span data-ttu-id="350e9-176">On the **Entities** page, click **Add custom entity**.</span><span class="sxs-lookup"><span data-stu-id="350e9-176">On the **Entities** page, click **Add custom entity**.</span></span>
3. <span data-ttu-id="350e9-177">In the **Add Entity** dialog box, type "TicketsOrder" in the **Entity name** box, and then select **Composite** from the **Entity type** list.</span><span class="sxs-lookup"><span data-stu-id="350e9-177">In the **Add Entity** dialog box, type "TicketsOrder" in the **Entity name** box, and then select **Composite** from the **Entity type** list.</span></span> <span data-ttu-id="350e9-178">Click on the add child link to add new child.</span><span class="sxs-lookup"><span data-stu-id="350e9-178">Click on the add child link to add new child.</span></span>
4. <span data-ttu-id="350e9-179">In **Child #1**, select the entity "number" from the list.</span><span class="sxs-lookup"><span data-stu-id="350e9-179">In **Child #1**, select the entity "number" from the list.</span></span>
5. <span data-ttu-id="350e9-180">In **Child #2**, select the parent entity "Category" from the list.</span><span class="sxs-lookup"><span data-stu-id="350e9-180">In **Child #2**, select the parent entity "Category" from the list.</span></span> 
6. <span data-ttu-id="350e9-181">In **Child #3**, select the parent entity "TravelClass" from the list.</span><span class="sxs-lookup"><span data-stu-id="350e9-181">In **Child #3**, select the parent entity "TravelClass" from the list.</span></span> 

    ![Add composite entity](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/AddCompositeEntity.jpg)

7. <span data-ttu-id="350e9-183">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="350e9-183">Click **Save**.</span></span>

    >[!NOTE]
    ><span data-ttu-id="350e9-184">To delete a child (in case of a mistake), click the trash icon next to it.</span><span class="sxs-lookup"><span data-stu-id="350e9-184">To delete a child (in case of a mistake), click the trash icon next to it.</span></span>


## <a name="editdelete-entities"></a><span data-ttu-id="350e9-185">Edit/Delete Entities</span><span class="sxs-lookup"><span data-stu-id="350e9-185">Edit/Delete Entities</span></span>
<span data-ttu-id="350e9-186">You can edit or delete entities from the **Entities list** on the **Entities** page of your app.</span><span class="sxs-lookup"><span data-stu-id="350e9-186">You can edit or delete entities from the **Entities list** on the **Entities** page of your app.</span></span> 

<span data-ttu-id="350e9-187">**To edit an entity:**</span><span class="sxs-lookup"><span data-stu-id="350e9-187">**To edit an entity:**</span></span>

1. <span data-ttu-id="350e9-188">On the **Entities** page, click the entity in the **Entities list**.</span><span class="sxs-lookup"><span data-stu-id="350e9-188">On the **Entities** page, click the entity in the **Entities list**.</span></span>
2. <span data-ttu-id="350e9-189">In the **Edit Entity** dialog box, you can edit the entity name and children names, or add more children (for hierarchical/composite entities), but the entity type is not editable.</span><span class="sxs-lookup"><span data-stu-id="350e9-189">In the **Edit Entity** dialog box, you can edit the entity name and children names, or add more children (for hierarchical/composite entities), but the entity type is not editable.</span></span> 

    ![Edit Entity dialog box](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/EditEntity-dialogbox.JPG)

3. <span data-ttu-id="350e9-191">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="350e9-191">Click **Save**.</span></span>

<span data-ttu-id="350e9-192">**To delete an entity:**</span><span class="sxs-lookup"><span data-stu-id="350e9-192">**To delete an entity:**</span></span>

* <span data-ttu-id="350e9-193">In the **Entities list**, click the trash bin icon next to the entity you want to delete.</span><span class="sxs-lookup"><span data-stu-id="350e9-193">In the **Entities list**, click the trash bin icon next to the entity you want to delete.</span></span> <span data-ttu-id="350e9-194">Then, click **OK** in the confirmation message to confirm deletion.</span><span class="sxs-lookup"><span data-stu-id="350e9-194">Then, click **OK** in the confirmation message to confirm deletion.</span></span>
 
    ![Delete Entity](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/DeleteEntity-Confirmation.jpg)

    >[!NOTE]
    >* <span data-ttu-id="350e9-196">Deleting a hierarchical entity deletes all its children entities.</span><span class="sxs-lookup"><span data-stu-id="350e9-196">Deleting a hierarchical entity deletes all its children entities.</span></span>
    >* <span data-ttu-id="350e9-197">Deleting a composite entity deletes only the composite and breaks the composite relationship, but doesn't delete the entities forming it.</span><span class="sxs-lookup"><span data-stu-id="350e9-197">Deleting a composite entity deletes only the composite and breaks the composite relationship, but doesn't delete the entities forming it.</span></span>


## <a name="review-labeled-utterances-for-entities"></a><span data-ttu-id="350e9-198">Review Labeled Utterances for Entities</span><span class="sxs-lookup"><span data-stu-id="350e9-198">Review Labeled Utterances for Entities</span></span>
<span data-ttu-id="350e9-199">To review the labeled utterances that contain a specific entity, click the **Labeled Utterances** tab on the **Entities** page, and choose the entity for which you want to display all labeled utterances.</span><span class="sxs-lookup"><span data-stu-id="350e9-199">To review the labeled utterances that contain a specific entity, click the **Labeled Utterances** tab on the **Entities** page, and choose the entity for which you want to display all labeled utterances.</span></span> <span data-ttu-id="350e9-200">You can modify entity labels in labeled utterances, if required, and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="350e9-200">You can modify entity labels in labeled utterances, if required, and then click **Save**.</span></span>

![Labeled Utterances for an entity](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/Entities-LabeledUtter.JPG)

<span data-ttu-id="350e9-202">Now that you have added intents, utterances and entities, you have a basic LUIS app ready to be trained and tested for publishing.</span><span class="sxs-lookup"><span data-stu-id="350e9-202">Now that you have added intents, utterances and entities, you have a basic LUIS app ready to be trained and tested for publishing.</span></span> <span data-ttu-id="350e9-203">For more information on how to train and test your app, [click here](Train-Test.md).</span><span class="sxs-lookup"><span data-stu-id="350e9-203">For more information on how to train and test your app, [click here](Train-Test.md).</span></span>
 








