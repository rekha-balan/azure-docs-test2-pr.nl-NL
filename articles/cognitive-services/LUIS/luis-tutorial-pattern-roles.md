---
title: Tutorial using pattern roles to improve LUIS predictions - Azure | Microsoft Docs
titleSuffix: Cognitive Services
description: In this tutorial, use pattern roles for contextually related entities to improve LUIS predictions.
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.technology: luis
ms.topic: article
ms.date: 08/03/2018
ms.author: diberry
ms.openlocfilehash: 6f3e7c9db7bbdb6bc24d123208355fc7a1d8e7e8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869033"
---
# <a name="tutorial-improve-app-with-pattern-roles"></a><span data-ttu-id="fdbc6-103">Tutorial: Improve app with pattern roles</span><span class="sxs-lookup"><span data-stu-id="fdbc6-103">Tutorial: Improve app with pattern roles</span></span>

<span data-ttu-id="fdbc6-104">In this tutorial, use a simple entity with roles combined with patterns to increase intent and entity prediction.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-104">In this tutorial, use a simple entity with roles combined with patterns to increase intent and entity prediction.</span></span>  <span data-ttu-id="fdbc6-105">When using patterns, fewer example utterances are needed for the intent.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-105">When using patterns, fewer example utterances are needed for the intent.</span></span>

> [!div class="checklist"]
* <span data-ttu-id="fdbc6-106">Understand pattern roles</span><span class="sxs-lookup"><span data-stu-id="fdbc6-106">Understand pattern roles</span></span>
* <span data-ttu-id="fdbc6-107">Use simple entity with roles</span><span class="sxs-lookup"><span data-stu-id="fdbc6-107">Use simple entity with roles</span></span> 
* <span data-ttu-id="fdbc6-108">Create pattern for utterances using simple entity with roles</span><span class="sxs-lookup"><span data-stu-id="fdbc6-108">Create pattern for utterances using simple entity with roles</span></span>
* <span data-ttu-id="fdbc6-109">How to verify pattern prediction improvements</span><span class="sxs-lookup"><span data-stu-id="fdbc6-109">How to verify pattern prediction improvements</span></span>

[!INCLUDE [LUIS Free account](../../../includes/cognitive-services-luis-free-key-short.md)]

## <a name="before-you-begin"></a><span data-ttu-id="fdbc6-110">Before you begin</span><span class="sxs-lookup"><span data-stu-id="fdbc6-110">Before you begin</span></span>
<span data-ttu-id="fdbc6-111">If you don't have the Human Resources app from the [pattern](luis-tutorial-pattern.md) tutorial, [import](luis-how-to-start-new-app.md#import-new-app) the JSON into a new app in the [LUIS](luis-reference-regions.md#luis-website) website.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-111">If you don't have the Human Resources app from the [pattern](luis-tutorial-pattern.md) tutorial, [import](luis-how-to-start-new-app.md#import-new-app) the JSON into a new app in the [LUIS](luis-reference-regions.md#luis-website) website.</span></span> <span data-ttu-id="fdbc6-112">The app to import is found in the [LUIS-Samples](https://github.com/Microsoft/LUIS-Samples/blob/master/documentation-samples/quickstarts/custom-domain-patterns-HumanResources-v2.json) GitHub repository.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-112">The app to import is found in the [LUIS-Samples](https://github.com/Microsoft/LUIS-Samples/blob/master/documentation-samples/quickstarts/custom-domain-patterns-HumanResources-v2.json) GitHub repository.</span></span>

<span data-ttu-id="fdbc6-113">If you want to keep the original Human Resources app, clone the version on the [Settings](luis-how-to-manage-versions.md#clone-a-version) page, and name it `roles`.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-113">If you want to keep the original Human Resources app, clone the version on the [Settings](luis-how-to-manage-versions.md#clone-a-version) page, and name it `roles`.</span></span> <span data-ttu-id="fdbc6-114">Cloning is a great way to play with various LUIS features without affecting the original version.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-114">Cloning is a great way to play with various LUIS features without affecting the original version.</span></span> 

## <a name="the-purpose-of-roles"></a><span data-ttu-id="fdbc6-115">The purpose of roles</span><span class="sxs-lookup"><span data-stu-id="fdbc6-115">The purpose of roles</span></span>
<span data-ttu-id="fdbc6-116">The purpose of roles is to extract contextually-related entities in an utterance.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-116">The purpose of roles is to extract contextually-related entities in an utterance.</span></span> <span data-ttu-id="fdbc6-117">In the utterance, `Move new employee Robert Williams from Sacramento and San Francisco`, the origin city, and destination city values are related to each other and use common language to denote each location.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-117">In the utterance, `Move new employee Robert Williams from Sacramento and San Francisco`, the origin city, and destination city values are related to each other and use common language to denote each location.</span></span> 

<span data-ttu-id="fdbc6-118">When using patterns, any entities in the pattern must be detected _before_ the pattern matches the utterance.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-118">When using patterns, any entities in the pattern must be detected _before_ the pattern matches the utterance.</span></span> 

<span data-ttu-id="fdbc6-119">When you create a pattern, the first step is to select the intent for the pattern.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-119">When you create a pattern, the first step is to select the intent for the pattern.</span></span> <span data-ttu-id="fdbc6-120">By selecting the intent, if the pattern matches, the correct intent is always returned with a high score ( usually 99-100%).</span><span class="sxs-lookup"><span data-stu-id="fdbc6-120">By selecting the intent, if the pattern matches, the correct intent is always returned with a high score ( usually 99-100%).</span></span> 

### <a name="compare-hierarchical-entity-to-simple-entity-with-roles"></a><span data-ttu-id="fdbc6-121">Compare hierarchical entity to simple entity with roles</span><span class="sxs-lookup"><span data-stu-id="fdbc6-121">Compare hierarchical entity to simple entity with roles</span></span>

<span data-ttu-id="fdbc6-122">In the [hierarchical tutorial](luis-quickstart-intent-and-hier-entity.md), the **MoveEmployee** intent detected when to move an existing employee from one building and office to another.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-122">In the [hierarchical tutorial](luis-quickstart-intent-and-hier-entity.md), the **MoveEmployee** intent detected when to move an existing employee from one building and office to another.</span></span> <span data-ttu-id="fdbc6-123">The example utterances had origin and destination locations but did not use roles.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-123">The example utterances had origin and destination locations but did not use roles.</span></span> <span data-ttu-id="fdbc6-124">Instead, the origin and destination were children of the  hierarchical entity.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-124">Instead, the origin and destination were children of the  hierarchical entity.</span></span> 

<span data-ttu-id="fdbc6-125">In this tutorial, the Human Resources app detects utterances about moving new employees from one city to another.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-125">In this tutorial, the Human Resources app detects utterances about moving new employees from one city to another.</span></span> <span data-ttu-id="fdbc6-126">These two types of utterances are similar but solved with different LUIS abilities.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-126">These two types of utterances are similar but solved with different LUIS abilities.</span></span>

|<span data-ttu-id="fdbc6-127">Tutorial</span><span class="sxs-lookup"><span data-stu-id="fdbc6-127">Tutorial</span></span>|<span data-ttu-id="fdbc6-128">Example utterance</span><span class="sxs-lookup"><span data-stu-id="fdbc6-128">Example utterance</span></span>|<span data-ttu-id="fdbc6-129">Origin and destination locations</span><span class="sxs-lookup"><span data-stu-id="fdbc6-129">Origin and destination locations</span></span>|
|--|--|--|
|[<span data-ttu-id="fdbc6-130">Hierarchical (no roles)</span><span class="sxs-lookup"><span data-stu-id="fdbc6-130">Hierarchical (no roles)</span></span>](luis-quickstart-intent-and-hier-entity.md)|<span data-ttu-id="fdbc6-131">mv Jill Jones from **a-2349** to **b-1298**</span><span class="sxs-lookup"><span data-stu-id="fdbc6-131">mv Jill Jones from **a-2349** to **b-1298**</span></span>|<span data-ttu-id="fdbc6-132">a-2349, b-1298</span><span class="sxs-lookup"><span data-stu-id="fdbc6-132">a-2349, b-1298</span></span>|
|<span data-ttu-id="fdbc6-133">This tutorial (with roles)</span><span class="sxs-lookup"><span data-stu-id="fdbc6-133">This tutorial (with roles)</span></span>|<span data-ttu-id="fdbc6-134">Move Billy Patterson from **Yuma** to **Denver**.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-134">Move Billy Patterson from **Yuma** to **Denver**.</span></span>|<span data-ttu-id="fdbc6-135">Yuma, Denver</span><span class="sxs-lookup"><span data-stu-id="fdbc6-135">Yuma, Denver</span></span>|

<span data-ttu-id="fdbc6-136">You can't use the hierarchical entity in the pattern because only hierarchical parents are used in patterns.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-136">You can't use the hierarchical entity in the pattern because only hierarchical parents are used in patterns.</span></span> <span data-ttu-id="fdbc6-137">In order to return the named locations of origin and destination, you muse use a pattern.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-137">In order to return the named locations of origin and destination, you muse use a pattern.</span></span>

### <a name="simple-entity-for-new-employee-name"></a><span data-ttu-id="fdbc6-138">Simple entity for new employee name</span><span class="sxs-lookup"><span data-stu-id="fdbc6-138">Simple entity for new employee name</span></span>
<span data-ttu-id="fdbc6-139">The name of the new employee, Billy Patterson, is not part of the list entity **Employee** yet.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-139">The name of the new employee, Billy Patterson, is not part of the list entity **Employee** yet.</span></span> <span data-ttu-id="fdbc6-140">The new employee name is extracted first, in order to send the name to an external system to create the company credentials.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-140">The new employee name is extracted first, in order to send the name to an external system to create the company credentials.</span></span> <span data-ttu-id="fdbc6-141">After the company credentials are created, the employee credentials are added to the list entity **Employee**.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-141">After the company credentials are created, the employee credentials are added to the list entity **Employee**.</span></span>

<span data-ttu-id="fdbc6-142">The **Employee** list was created in the [list tutorial](luis-quickstart-intent-and-list-entity.md).</span><span class="sxs-lookup"><span data-stu-id="fdbc6-142">The **Employee** list was created in the [list tutorial](luis-quickstart-intent-and-list-entity.md).</span></span>

<span data-ttu-id="fdbc6-143">The **NewEmployee** entity is a simple entity with no roles.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-143">The **NewEmployee** entity is a simple entity with no roles.</span></span> 

### <a name="simple-entity-with-roles-for-relocation-cities"></a><span data-ttu-id="fdbc6-144">Simple entity with roles for relocation cities</span><span class="sxs-lookup"><span data-stu-id="fdbc6-144">Simple entity with roles for relocation cities</span></span>
<span data-ttu-id="fdbc6-145">The new employee and family need to be moved from the current city to a city where the fictitious company is located.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-145">The new employee and family need to be moved from the current city to a city where the fictitious company is located.</span></span> <span data-ttu-id="fdbc6-146">Because a new employee can come from any city, the locations need to be discovered.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-146">Because a new employee can come from any city, the locations need to be discovered.</span></span> <span data-ttu-id="fdbc6-147">A set list such as a list entity would not work because only the cities in the list would be extracted.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-147">A set list such as a list entity would not work because only the cities in the list would be extracted.</span></span>

<span data-ttu-id="fdbc6-148">The role names associated with the origin and destination cities need to be unique across all entities.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-148">The role names associated with the origin and destination cities need to be unique across all entities.</span></span> <span data-ttu-id="fdbc6-149">An easy way to make sure the roles are unique is to tie them to the containing entity through a naming strategy.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-149">An easy way to make sure the roles are unique is to tie them to the containing entity through a naming strategy.</span></span> <span data-ttu-id="fdbc6-150">The **NewEmployeeRelocation** entity is a simple entity with two roles: **NewEmployeeReloOrigin** and **NewEmployeeReloDestination**.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-150">The **NewEmployeeRelocation** entity is a simple entity with two roles: **NewEmployeeReloOrigin** and **NewEmployeeReloDestination**.</span></span>

### <a name="simple-entities-need-enough-examples-to-be-detected"></a><span data-ttu-id="fdbc6-151">Simple entities need enough examples to be detected</span><span class="sxs-lookup"><span data-stu-id="fdbc6-151">Simple entities need enough examples to be detected</span></span>
<span data-ttu-id="fdbc6-152">Because the example utterance `Move new employee Robert Williams from Sacramento and San Francisco` has only machine-learned entities, it is important to provide enough example utterances to the intent so the entities are detected.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-152">Because the example utterance `Move new employee Robert Williams from Sacramento and San Francisco` has only machine-learned entities, it is important to provide enough example utterances to the intent so the entities are detected.</span></span>  

<span data-ttu-id="fdbc6-153">**While patterns allow you to provide fewer example utterances, if the entities are not detected, the pattern does not match.**</span><span class="sxs-lookup"><span data-stu-id="fdbc6-153">**While patterns allow you to provide fewer example utterances, if the entities are not detected, the pattern does not match.**</span></span>

<span data-ttu-id="fdbc6-154">If you have difficulty with simple entity detection because it is a name such as a city, consider adding a phrase list of similar values.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-154">If you have difficulty with simple entity detection because it is a name such as a city, consider adding a phrase list of similar values.</span></span> <span data-ttu-id="fdbc6-155">This helps the detection of the city name by giving LUIS an additional signal about that type of word or phrase.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-155">This helps the detection of the city name by giving LUIS an additional signal about that type of word or phrase.</span></span> <span data-ttu-id="fdbc6-156">Phrase lists only help the pattern by helping with entity detection, which is necessary for the pattern to match.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-156">Phrase lists only help the pattern by helping with entity detection, which is necessary for the pattern to match.</span></span> 

## <a name="create-new-entities"></a><span data-ttu-id="fdbc6-157">Create new entities</span><span class="sxs-lookup"><span data-stu-id="fdbc6-157">Create new entities</span></span>
1. <span data-ttu-id="fdbc6-158">Select **Build** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-158">Select **Build** in the top menu.</span></span>

2. <span data-ttu-id="fdbc6-159">Select **Entities** from the left navigation.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-159">Select **Entities** from the left navigation.</span></span> 

3. <span data-ttu-id="fdbc6-160">Select **Create new entity**.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-160">Select **Create new entity**.</span></span>

4. <span data-ttu-id="fdbc6-161">In the pop-up window, enter `NewEmployee` as a **Simple** entity.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-161">In the pop-up window, enter `NewEmployee` as a **Simple** entity.</span></span>

5. <span data-ttu-id="fdbc6-162">Select **Create new entity**.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-162">Select **Create new entity**.</span></span>

6. <span data-ttu-id="fdbc6-163">In the pop-up window, enter `NewEmployeeRelocation` as a **Simple** entity.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-163">In the pop-up window, enter `NewEmployeeRelocation` as a **Simple** entity.</span></span>

7. <span data-ttu-id="fdbc6-164">Select **NewEmployeeRelocation** from the list of entities.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-164">Select **NewEmployeeRelocation** from the list of entities.</span></span> 

8. <span data-ttu-id="fdbc6-165">Enter the first role as `NewEmployeeReloOrigin` and select enter.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-165">Enter the first role as `NewEmployeeReloOrigin` and select enter.</span></span>

9. <span data-ttu-id="fdbc6-166">Enter the second role as `NewEmployeeReloDestination` and select enter.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-166">Enter the second role as `NewEmployeeReloDestination` and select enter.</span></span>

## <a name="create-new-intent"></a><span data-ttu-id="fdbc6-167">Create new intent</span><span class="sxs-lookup"><span data-stu-id="fdbc6-167">Create new intent</span></span>
<span data-ttu-id="fdbc6-168">Labeling the entities in these steps may be easier if the prebuilt keyPhrase entity is removed before beginning then added back after you are done with the steps in this section.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-168">Labeling the entities in these steps may be easier if the prebuilt keyPhrase entity is removed before beginning then added back after you are done with the steps in this section.</span></span> 

1. <span data-ttu-id="fdbc6-169">Select **Intents** from the left navigation.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-169">Select **Intents** from the left navigation.</span></span>

2. <span data-ttu-id="fdbc6-170">Select **Create new intent**.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-170">Select **Create new intent**.</span></span> 

3. <span data-ttu-id="fdbc6-171">Enter `NewEmployeeRelocationProcess` as the intent name in the pop-up dialog box.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-171">Enter `NewEmployeeRelocationProcess` as the intent name in the pop-up dialog box.</span></span>

4. <span data-ttu-id="fdbc6-172">Enter the following example utterances, labeling the new entities.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-172">Enter the following example utterances, labeling the new entities.</span></span> <span data-ttu-id="fdbc6-173">The entity and role values are in bold.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-173">The entity and role values are in bold.</span></span> <span data-ttu-id="fdbc6-174">Remember to switch to the **Tokens View** if you find it easier to label the text.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-174">Remember to switch to the **Tokens View** if you find it easier to label the text.</span></span> 

    <span data-ttu-id="fdbc6-175">You don't specify the role of the entity when labeling in the intent.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-175">You don't specify the role of the entity when labeling in the intent.</span></span> <span data-ttu-id="fdbc6-176">You do that later when creating the pattern.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-176">You do that later when creating the pattern.</span></span> 

    |<span data-ttu-id="fdbc6-177">Utterance</span><span class="sxs-lookup"><span data-stu-id="fdbc6-177">Utterance</span></span>|<span data-ttu-id="fdbc6-178">NewEmployee</span><span class="sxs-lookup"><span data-stu-id="fdbc6-178">NewEmployee</span></span>|<span data-ttu-id="fdbc6-179">NewEmployeeRelocation</span><span class="sxs-lookup"><span data-stu-id="fdbc6-179">NewEmployeeRelocation</span></span>|
    |--|--|--|
    |<span data-ttu-id="fdbc6-180">Move **Bob Jones** from **Seattle** to **Los Colinas**</span><span class="sxs-lookup"><span data-stu-id="fdbc6-180">Move **Bob Jones** from **Seattle** to **Los Colinas**</span></span>|<span data-ttu-id="fdbc6-181">Bob Jones</span><span class="sxs-lookup"><span data-stu-id="fdbc6-181">Bob Jones</span></span>|<span data-ttu-id="fdbc6-182">Seattle, Los Colinas</span><span class="sxs-lookup"><span data-stu-id="fdbc6-182">Seattle, Los Colinas</span></span>|
    |<span data-ttu-id="fdbc6-183">Move **Dave C. Cooper** from **Redmond** to **New York City**</span><span class="sxs-lookup"><span data-stu-id="fdbc6-183">Move **Dave C. Cooper** from **Redmond** to **New York City**</span></span>|<span data-ttu-id="fdbc6-184">Dave C. Cooper</span><span class="sxs-lookup"><span data-stu-id="fdbc6-184">Dave C. Cooper</span></span>|<span data-ttu-id="fdbc6-185">Redmond, New York City</span><span class="sxs-lookup"><span data-stu-id="fdbc6-185">Redmond, New York City</span></span>|
    |<span data-ttu-id="fdbc6-186">Move **Jim Paul Smith** from **Toronto** to **West Vancouver**</span><span class="sxs-lookup"><span data-stu-id="fdbc6-186">Move **Jim Paul Smith** from **Toronto** to **West Vancouver**</span></span>|<span data-ttu-id="fdbc6-187">Jim Paul Smith</span><span class="sxs-lookup"><span data-stu-id="fdbc6-187">Jim Paul Smith</span></span>|<span data-ttu-id="fdbc6-188">Toronto, West Vancouver</span><span class="sxs-lookup"><span data-stu-id="fdbc6-188">Toronto, West Vancouver</span></span>|
    |<span data-ttu-id="fdbc6-189">Move **J. Benson** from **Boston** to **Staines-upon-Thames**</span><span class="sxs-lookup"><span data-stu-id="fdbc6-189">Move **J. Benson** from **Boston** to **Staines-upon-Thames**</span></span>|<span data-ttu-id="fdbc6-190">J.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-190">J.</span></span> <span data-ttu-id="fdbc6-191">Benson</span><span class="sxs-lookup"><span data-stu-id="fdbc6-191">Benson</span></span>|<span data-ttu-id="fdbc6-192">Boston, Staines-upon-Thames</span><span class="sxs-lookup"><span data-stu-id="fdbc6-192">Boston, Staines-upon-Thames</span></span>|
    |<span data-ttu-id="fdbc6-193">Move **Travis "Trav" Hinton** from **Castelo Branco** to **Orlando**</span><span class="sxs-lookup"><span data-stu-id="fdbc6-193">Move **Travis "Trav" Hinton** from **Castelo Branco** to **Orlando**</span></span>|<span data-ttu-id="fdbc6-194">Travis "Trav" Hinton</span><span class="sxs-lookup"><span data-stu-id="fdbc6-194">Travis "Trav" Hinton</span></span>|<span data-ttu-id="fdbc6-195">Castelo Branco, Orlando</span><span class="sxs-lookup"><span data-stu-id="fdbc6-195">Castelo Branco, Orlando</span></span>|
    |<span data-ttu-id="fdbc6-196">Move **Trevor Nottington III** from **Aranda de Duero** to **Boise**</span><span class="sxs-lookup"><span data-stu-id="fdbc6-196">Move **Trevor Nottington III** from **Aranda de Duero** to **Boise**</span></span>|<span data-ttu-id="fdbc6-197">Trevor Nottington III</span><span class="sxs-lookup"><span data-stu-id="fdbc6-197">Trevor Nottington III</span></span>|<span data-ttu-id="fdbc6-198">Aranda de Duero, Boise</span><span class="sxs-lookup"><span data-stu-id="fdbc6-198">Aranda de Duero, Boise</span></span>|
    |<span data-ttu-id="fdbc6-199">Move **Dr. Greg Williams** from **Orlando** to **Ellicott City**</span><span class="sxs-lookup"><span data-stu-id="fdbc6-199">Move **Dr. Greg Williams** from **Orlando** to **Ellicott City**</span></span>|<span data-ttu-id="fdbc6-200">Dr. Greg Williams</span><span class="sxs-lookup"><span data-stu-id="fdbc6-200">Dr. Greg Williams</span></span>|<span data-ttu-id="fdbc6-201">Orlando, Ellicott City</span><span class="sxs-lookup"><span data-stu-id="fdbc6-201">Orlando, Ellicott City</span></span>|
    |<span data-ttu-id="fdbc6-202">Move **Robert "Bobby" Gregson** from **Kansas City** to **San Juan Capistrano**</span><span class="sxs-lookup"><span data-stu-id="fdbc6-202">Move **Robert "Bobby" Gregson** from **Kansas City** to **San Juan Capistrano**</span></span>|<span data-ttu-id="fdbc6-203">Robert "Bobby" Gregson</span><span class="sxs-lookup"><span data-stu-id="fdbc6-203">Robert "Bobby" Gregson</span></span>|<span data-ttu-id="fdbc6-204">Kansas City, San Juan Capistrano</span><span class="sxs-lookup"><span data-stu-id="fdbc6-204">Kansas City, San Juan Capistrano</span></span>|
    |<span data-ttu-id="fdbc6-205">Move **Patti Owens** from **Bellevue** to **Rockford**</span><span class="sxs-lookup"><span data-stu-id="fdbc6-205">Move **Patti Owens** from **Bellevue** to **Rockford**</span></span>|<span data-ttu-id="fdbc6-206">Patti Owens</span><span class="sxs-lookup"><span data-stu-id="fdbc6-206">Patti Owens</span></span>|<span data-ttu-id="fdbc6-207">Bellevue, Rockford</span><span class="sxs-lookup"><span data-stu-id="fdbc6-207">Bellevue, Rockford</span></span>|
    |<span data-ttu-id="fdbc6-208">Move **Janet Bartlet** from **Tuscan** to **Santa Fe**</span><span class="sxs-lookup"><span data-stu-id="fdbc6-208">Move **Janet Bartlet** from **Tuscan** to **Santa Fe**</span></span>|<span data-ttu-id="fdbc6-209">Janet Bartlet</span><span class="sxs-lookup"><span data-stu-id="fdbc6-209">Janet Bartlet</span></span>|<span data-ttu-id="fdbc6-210">Tuscan, Santa Fe</span><span class="sxs-lookup"><span data-stu-id="fdbc6-210">Tuscan, Santa Fe</span></span>|

    <span data-ttu-id="fdbc6-211">The employee name has a variety of prefix, word count, syntax, and suffix.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-211">The employee name has a variety of prefix, word count, syntax, and suffix.</span></span> <span data-ttu-id="fdbc6-212">This is important for LUIS to understand the variations of a new employee name.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-212">This is important for LUIS to understand the variations of a new employee name.</span></span> <span data-ttu-id="fdbc6-213">The city names also have a variety of word count and syntax.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-213">The city names also have a variety of word count and syntax.</span></span> <span data-ttu-id="fdbc6-214">This variety is important to teach LUIS how these entities may appear in a user's utterance.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-214">This variety is important to teach LUIS how these entities may appear in a user's utterance.</span></span> 
    
    <span data-ttu-id="fdbc6-215">If either entity had been of the same word count and no other variations, you would teach LUIS that this entity only has that word count and no other variations.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-215">If either entity had been of the same word count and no other variations, you would teach LUIS that this entity only has that word count and no other variations.</span></span> <span data-ttu-id="fdbc6-216">LUIS would not be able to correctly predict a broader set of variations because it was not shown any.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-216">LUIS would not be able to correctly predict a broader set of variations because it was not shown any.</span></span> 

    <span data-ttu-id="fdbc6-217">If you removed the keyPhrase entity, add it back to the app now.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-217">If you removed the keyPhrase entity, add it back to the app now.</span></span>

## <a name="train-the-luis-app"></a><span data-ttu-id="fdbc6-218">Train the LUIS app</span><span class="sxs-lookup"><span data-stu-id="fdbc6-218">Train the LUIS app</span></span>

[!INCLUDE [LUIS How to Train steps](../../../includes/cognitive-services-luis-tutorial-how-to-train.md)]

## <a name="publish-the-app-to-get-the-endpoint-url"></a><span data-ttu-id="fdbc6-219">Publish the app to get the endpoint URL</span><span class="sxs-lookup"><span data-stu-id="fdbc6-219">Publish the app to get the endpoint URL</span></span>

[!INCLUDE [LUIS How to Publish steps](../../../includes/cognitive-services-luis-tutorial-how-to-publish.md)]

## <a name="query-the-endpoint-without-pattern"></a><span data-ttu-id="fdbc6-220">Query the endpoint without pattern</span><span class="sxs-lookup"><span data-stu-id="fdbc6-220">Query the endpoint without pattern</span></span>

1. [!INCLUDE [LUIS How to get endpoint first step](../../../includes/cognitive-services-luis-tutorial-how-to-get-endpoint.md)] 

2. <span data-ttu-id="fdbc6-221">Go to the end of the URL in the address and enter `Move Wayne Berry from Miami to Mount Vernon`.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-221">Go to the end of the URL in the address and enter `Move Wayne Berry from Miami to Mount Vernon`.</span></span> <span data-ttu-id="fdbc6-222">The last querystring parameter is `q`, the utterance **query**.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-222">The last querystring parameter is `q`, the utterance **query**.</span></span> 

    ```JSON
    {
      "query": "Move Wayne Berry from Newark to Columbus",
      "topScoringIntent": {
        "intent": "NewEmployeeRelocationProcess",
        "score": 0.514479756
      },
      "intents": [
        {
          "intent": "NewEmployeeRelocationProcess",
          "score": 0.514479756
        },
        {
          "intent": "Utilities.Confirm",
          "score": 0.017118983
        },
        {
          "intent": "MoveEmployee",
          "score": 0.009982505
        },
        {
          "intent": "GetJobInformation",
          "score": 0.008637771
        },
        {
          "intent": "ApplyForJob",
          "score": 0.007115978
        },
        {
          "intent": "Utilities.StartOver",
          "score": 0.006120186
        },
        {
          "intent": "Utilities.Cancel",
          "score": 0.00452428637
        },
        {
          "intent": "None",
          "score": 0.00400899537
        },
        {
          "intent": "OrgChart-Reports",
          "score": 0.00240071164
        },
        {
          "intent": "Utilities.Help",
          "score": 0.001770991
        },
        {
          "intent": "EmployeeFeedback",
          "score": 0.001697356
        },
        {
          "intent": "OrgChart-Manager",
          "score": 0.00168116146
        },
        {
          "intent": "Utilities.Stop",
          "score": 0.00163952739
        },
        {
          "intent": "FindForm",
          "score": 0.00112958835
        }
      ],
      "entities": [
        {
          "entity": "wayne berry",
          "type": "NewEmployee",
          "startIndex": 5,
          "endIndex": 15,
          "score": 0.629158735
        },
        {
          "entity": "newark",
          "type": "NewEmployeeRelocation",
          "startIndex": 22,
          "endIndex": 27,
          "score": 0.638941
        }
      ]
    }  
    ```

<span data-ttu-id="fdbc6-223">The intent prediction score is only about 50%.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-223">The intent prediction score is only about 50%.</span></span> <span data-ttu-id="fdbc6-224">If your client application requires a higher number, this needs to be fixed.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-224">If your client application requires a higher number, this needs to be fixed.</span></span> <span data-ttu-id="fdbc6-225">The entities were not predicted either.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-225">The entities were not predicted either.</span></span>

<span data-ttu-id="fdbc6-226">Patterns will help the prediction score, however, the entities must be correctly predicted before the pattern matches the utterance.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-226">Patterns will help the prediction score, however, the entities must be correctly predicted before the pattern matches the utterance.</span></span> 

## <a name="add-a-pattern-that-uses-roles"></a><span data-ttu-id="fdbc6-227">Add a pattern that uses roles</span><span class="sxs-lookup"><span data-stu-id="fdbc6-227">Add a pattern that uses roles</span></span>
1. <span data-ttu-id="fdbc6-228">Select **Build** in the top navigation.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-228">Select **Build** in the top navigation.</span></span>

2. <span data-ttu-id="fdbc6-229">Select **Patterns** in the left navigation.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-229">Select **Patterns** in the left navigation.</span></span>

3. <span data-ttu-id="fdbc6-230">Select **NewEmployeeRelocationProcess** from the **Select an intent** drop-down list.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-230">Select **NewEmployeeRelocationProcess** from the **Select an intent** drop-down list.</span></span> 

4. <span data-ttu-id="fdbc6-231">Enter the following pattern: `move {NewEmployee} from {NewEmployeeRelocation:NewEmployeeReloOrigin} to {NewEmployeeRelocation:NewEmployeeReloDestination}[.]`</span><span class="sxs-lookup"><span data-stu-id="fdbc6-231">Enter the following pattern: `move {NewEmployee} from {NewEmployeeRelocation:NewEmployeeReloOrigin} to {NewEmployeeRelocation:NewEmployeeReloDestination}[.]`</span></span>

    <span data-ttu-id="fdbc6-232">If you train, publish, and query the endpoint, you may be disappointed to see that the entities are not found, so the pattern didn't match, therefore the prediction didn't improve.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-232">If you train, publish, and query the endpoint, you may be disappointed to see that the entities are not found, so the pattern didn't match, therefore the prediction didn't improve.</span></span> <span data-ttu-id="fdbc6-233">This is a consequence of not enough example utterances with labeled entities.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-233">This is a consequence of not enough example utterances with labeled entities.</span></span> <span data-ttu-id="fdbc6-234">Instead of adding more examples, add a phrase list to fix this problem.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-234">Instead of adding more examples, add a phrase list to fix this problem.</span></span>

## <a name="create-a-phrase-list-for-cities"></a><span data-ttu-id="fdbc6-235">Create a phrase list for Cities</span><span class="sxs-lookup"><span data-stu-id="fdbc6-235">Create a phrase list for Cities</span></span>
<span data-ttu-id="fdbc6-236">Cities, like people's names are tricky in that they can be any mix of words and punctuation.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-236">Cities, like people's names are tricky in that they can be any mix of words and punctuation.</span></span> <span data-ttu-id="fdbc6-237">But the cities of the region and world are known, so LUIS needs a phrase list of cities to begin learning.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-237">But the cities of the region and world are known, so LUIS needs a phrase list of cities to begin learning.</span></span> 

1. <span data-ttu-id="fdbc6-238">Select **Phrase list** from the **Improve app performance** section of the left menu.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-238">Select **Phrase list** from the **Improve app performance** section of the left menu.</span></span> 

2. <span data-ttu-id="fdbc6-239">Name the list `Cities` and add the following `values` for the list:</span><span class="sxs-lookup"><span data-stu-id="fdbc6-239">Name the list `Cities` and add the following `values` for the list:</span></span>

    |<span data-ttu-id="fdbc6-240">Values of phrase list</span><span class="sxs-lookup"><span data-stu-id="fdbc6-240">Values of phrase list</span></span>|
    |--|
    |<span data-ttu-id="fdbc6-241">Seattle</span><span class="sxs-lookup"><span data-stu-id="fdbc6-241">Seattle</span></span>|
    |<span data-ttu-id="fdbc6-242">San Diego</span><span class="sxs-lookup"><span data-stu-id="fdbc6-242">San Diego</span></span>|
    |<span data-ttu-id="fdbc6-243">New York City</span><span class="sxs-lookup"><span data-stu-id="fdbc6-243">New York City</span></span>|
    |<span data-ttu-id="fdbc6-244">Los Angeles</span><span class="sxs-lookup"><span data-stu-id="fdbc6-244">Los Angeles</span></span>|
    |<span data-ttu-id="fdbc6-245">Portland</span><span class="sxs-lookup"><span data-stu-id="fdbc6-245">Portland</span></span>|
    |<span data-ttu-id="fdbc6-246">Philadephia</span><span class="sxs-lookup"><span data-stu-id="fdbc6-246">Philadephia</span></span>|
    |<span data-ttu-id="fdbc6-247">Miami</span><span class="sxs-lookup"><span data-stu-id="fdbc6-247">Miami</span></span>|
    |<span data-ttu-id="fdbc6-248">Dallas</span><span class="sxs-lookup"><span data-stu-id="fdbc6-248">Dallas</span></span>|

    <span data-ttu-id="fdbc6-249">Do not add every city in the world or even every city in the region.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-249">Do not add every city in the world or even every city in the region.</span></span> <span data-ttu-id="fdbc6-250">LUIS needs to be able to generalize what a city is from the list.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-250">LUIS needs to be able to generalize what a city is from the list.</span></span> 

    <span data-ttu-id="fdbc6-251">Make sure to keep **These values are interchangeable** selected.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-251">Make sure to keep **These values are interchangeable** selected.</span></span> <span data-ttu-id="fdbc6-252">This setting means the words on the list on treated as synonyms.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-252">This setting means the words on the list on treated as synonyms.</span></span> <span data-ttu-id="fdbc6-253">This is exactly how they should be treated in the pattern.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-253">This is exactly how they should be treated in the pattern.</span></span>

    <span data-ttu-id="fdbc6-254">Remember [the last time](luis-quickstart-primary-and-secondary-data.md) the tutorial series created a phrase list was also to boost entity detection of a simple entity.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-254">Remember [the last time](luis-quickstart-primary-and-secondary-data.md) the tutorial series created a phrase list was also to boost entity detection of a simple entity.</span></span>  

3. <span data-ttu-id="fdbc6-255">Train and publish the app.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-255">Train and publish the app.</span></span>

## <a name="query-endpoint-for-pattern"></a><span data-ttu-id="fdbc6-256">Query endpoint for pattern</span><span class="sxs-lookup"><span data-stu-id="fdbc6-256">Query endpoint for pattern</span></span>
1. <span data-ttu-id="fdbc6-257">On the **Publish** page, select the **endpoint** link at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-257">On the **Publish** page, select the **endpoint** link at the bottom of the page.</span></span> <span data-ttu-id="fdbc6-258">This action opens another browser window with the endpoint URL in the address bar.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-258">This action opens another browser window with the endpoint URL in the address bar.</span></span> 

2. <span data-ttu-id="fdbc6-259">Go to the end of the URL in the address and enter `Move wayne berry from miami to mount vernon`.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-259">Go to the end of the URL in the address and enter `Move wayne berry from miami to mount vernon`.</span></span> <span data-ttu-id="fdbc6-260">The last querystring parameter is `q`, the utterance **query**.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-260">The last querystring parameter is `q`, the utterance **query**.</span></span> 

    ```JSON
    {
      "query": "Move Wayne Berry from Miami to Mount Vernon",
      "topScoringIntent": {
        "intent": "NewEmployeeRelocationProcess",
        "score": 0.9999999
      },
      "intents": [
        {
          "intent": "NewEmployeeRelocationProcess",
          "score": 0.9999999
        },
        {
          "intent": "Utilities.Confirm",
          "score": 1.49678385E-06
        },
        {
          "intent": "MoveEmployee",
          "score": 8.240291E-07
        },
        {
          "intent": "GetJobInformation",
          "score": 6.3131273E-07
        },
        {
          "intent": "None",
          "score": 4.25E-09
        },
        {
          "intent": "OrgChart-Manager",
          "score": 2.8E-09
        },
        {
          "intent": "OrgChart-Reports",
          "score": 2.8E-09
        },
        {
          "intent": "EmployeeFeedback",
          "score": 1.64E-09
        },
        {
          "intent": "Utilities.StartOver",
          "score": 1.64E-09
        },
        {
          "intent": "Utilities.Help",
          "score": 1.48181822E-09
        },
        {
          "intent": "Utilities.Stop",
          "score": 1.48181822E-09
        },
        {
          "intent": "Utilities.Cancel",
          "score": 1.35E-09
        },
        {
          "intent": "FindForm",
          "score": 1.23846156E-09
        },
        {
          "intent": "ApplyForJob",
          "score": 5.692308E-10
        }
      ],
      "entities": [
        {
          "entity": "wayne berry",
          "type": "builtin.keyPhrase",
          "startIndex": 5,
          "endIndex": 15
        },
        {
          "entity": "miami",
          "type": "builtin.keyPhrase",
          "startIndex": 22,
          "endIndex": 26
        },
        {
          "entity": "wayne berry",
          "type": "NewEmployee",
          "startIndex": 5,
          "endIndex": 15,
          "score": 0.9410646,
          "role": ""
        },
        {
          "entity": "miami",
          "type": "NewEmployeeRelocation",
          "startIndex": 22,
          "endIndex": 26,
          "score": 0.9853915,
          "role": "NewEmployeeReloOrigin"
        },
        {
          "entity": "mount vernon",
          "type": "NewEmployeeRelocation",
          "startIndex": 31,
          "endIndex": 42,
          "score": 0.986044347,
          "role": "NewEmployeeReloDestination"
        }
      ],
      "sentimentAnalysis": {
        "label": "neutral",
        "score": 0.5
      }
}
    ```

<span data-ttu-id="fdbc6-261">The intent score is now much higher and the role names are part of the entity response.</span><span class="sxs-lookup"><span data-stu-id="fdbc6-261">The intent score is now much higher and the role names are part of the entity response.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="fdbc6-262">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="fdbc6-262">Clean up resources</span></span>

[!INCLUDE [LUIS How to clean up resources](../../../includes/cognitive-services-luis-tutorial-how-to-clean-up-resources.md)]

## <a name="next-steps"></a><span data-ttu-id="fdbc6-263">Next steps</span><span class="sxs-lookup"><span data-stu-id="fdbc6-263">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="fdbc6-264">Learn best practices for LUIS apps</span><span class="sxs-lookup"><span data-stu-id="fdbc6-264">Learn best practices for LUIS apps</span></span>](luis-concept-best-practices.md)
