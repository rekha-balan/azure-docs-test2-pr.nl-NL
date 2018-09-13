---
title: How to use entities with a Conversation Learner model - Microsoft Cognitive Services | Microsoft Docs
titleSuffix: Azure
description: Learn how to use entities with a Conversation Learner model.
services: cognitive-services
author: v-jaswel
manager: nolachar
ms.service: cognitive-services
ms.component: conversation-learner
ms.topic: article
ms.date: 04/30/2018
ms.author: v-jaswel
ms.openlocfilehash: f851d43d69999a848dea01c9457a379adb63353b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968978"
---
# <a name="introduction-to-entities"></a><span data-ttu-id="c66e7-103">Introduction to entities</span><span class="sxs-lookup"><span data-stu-id="c66e7-103">Introduction to entities</span></span>

<span data-ttu-id="c66e7-104">This tutorial introduces entities, and shows how to use the "Disqualifying entities" and "Required entities" fields in actions.</span><span class="sxs-lookup"><span data-stu-id="c66e7-104">This tutorial introduces entities, and shows how to use the "Disqualifying entities" and "Required entities" fields in actions.</span></span>

## <a name="video"></a><span data-ttu-id="c66e7-105">Video</span><span class="sxs-lookup"><span data-stu-id="c66e7-105">Video</span></span>

<span data-ttu-id="c66e7-106">[![Tutorial 3 Preview](http://aka.ms/cl-tutorial-03-preview)](http://aka.ms/blis-tutorial-03)</span><span class="sxs-lookup"><span data-stu-id="c66e7-106">[![Tutorial 3 Preview](http://aka.ms/cl-tutorial-03-preview)](http://aka.ms/blis-tutorial-03)</span></span>

## <a name="requirements"></a><span data-ttu-id="c66e7-107">Requirements</span><span class="sxs-lookup"><span data-stu-id="c66e7-107">Requirements</span></span>

<span data-ttu-id="c66e7-108">This tutorial requires that the general tutorial bot is running</span><span class="sxs-lookup"><span data-stu-id="c66e7-108">This tutorial requires that the general tutorial bot is running</span></span>

    npm run tutorial-general

## <a name="details"></a><span data-ttu-id="c66e7-109">Details</span><span class="sxs-lookup"><span data-stu-id="c66e7-109">Details</span></span>

<span data-ttu-id="c66e7-110">This tutorial illustrates two common uses for entities.</span><span class="sxs-lookup"><span data-stu-id="c66e7-110">This tutorial illustrates two common uses for entities.</span></span>  <span data-ttu-id="c66e7-111">First, entities can extract substrings from a user message, such as identifying a city in "what's the weather in Seattle?".</span><span class="sxs-lookup"><span data-stu-id="c66e7-111">First, entities can extract substrings from a user message, such as identifying a city in "what's the weather in Seattle?".</span></span>  <span data-ttu-id="c66e7-112">Second, entities can constrain when actions are available.</span><span class="sxs-lookup"><span data-stu-id="c66e7-112">Second, entities can constrain when actions are available.</span></span>  <span data-ttu-id="c66e7-113">Specifically, an action can list an entity as being "required" or "disqualifying":</span><span class="sxs-lookup"><span data-stu-id="c66e7-113">Specifically, an action can list an entity as being "required" or "disqualifying":</span></span>
- <span data-ttu-id="c66e7-114">An action's required entities must be present in the bot's memory in order for the action to be available</span><span class="sxs-lookup"><span data-stu-id="c66e7-114">An action's required entities must be present in the bot's memory in order for the action to be available</span></span>
- <span data-ttu-id="c66e7-115">Disqualifying entities must *not* be present in the bot's memory in order for the action to be available</span><span class="sxs-lookup"><span data-stu-id="c66e7-115">Disqualifying entities must *not* be present in the bot's memory in order for the action to be available</span></span>

<span data-ttu-id="c66e7-116">Other tutorials cover other aspects of entities, such as pre-built entities, multi-value and negatable entities, programmatic entities, and manipulating entities in code.</span><span class="sxs-lookup"><span data-stu-id="c66e7-116">Other tutorials cover other aspects of entities, such as pre-built entities, multi-value and negatable entities, programmatic entities, and manipulating entities in code.</span></span>

## <a name="steps"></a><span data-ttu-id="c66e7-117">Steps</span><span class="sxs-lookup"><span data-stu-id="c66e7-117">Steps</span></span>

### <a name="create-the-model"></a><span data-ttu-id="c66e7-118">Create the model</span><span class="sxs-lookup"><span data-stu-id="c66e7-118">Create the model</span></span>

1. <span data-ttu-id="c66e7-119">In the Web UI, click New Model</span><span class="sxs-lookup"><span data-stu-id="c66e7-119">In the Web UI, click New Model</span></span>
2. <span data-ttu-id="c66e7-120">In Name, enter IntroToEntities.</span><span class="sxs-lookup"><span data-stu-id="c66e7-120">In Name, enter IntroToEntities.</span></span> <span data-ttu-id="c66e7-121">Then click Create.</span><span class="sxs-lookup"><span data-stu-id="c66e7-121">Then click Create.</span></span>

### <a name="create-entity"></a><span data-ttu-id="c66e7-122">Create entity</span><span class="sxs-lookup"><span data-stu-id="c66e7-122">Create entity</span></span>

1. <span data-ttu-id="c66e7-123">Click Entities, then New Entity.</span><span class="sxs-lookup"><span data-stu-id="c66e7-123">Click Entities, then New Entity.</span></span>
2. <span data-ttu-id="c66e7-124">In Entity Name, enter city.</span><span class="sxs-lookup"><span data-stu-id="c66e7-124">In Entity Name, enter city.</span></span>
3. <span data-ttu-id="c66e7-125">Click Create</span><span class="sxs-lookup"><span data-stu-id="c66e7-125">Click Create</span></span>

> [!NOTE]
> <span data-ttu-id="c66e7-126">The entity type is 'custom' -- this means that the entity can be trained.</span><span class="sxs-lookup"><span data-stu-id="c66e7-126">The entity type is 'custom' -- this means that the entity can be trained.</span></span>  <span data-ttu-id="c66e7-127">There are also pre-built entities, meaning that their behavior cannot be adjusted -- these are covered in another tutorial.</span><span class="sxs-lookup"><span data-stu-id="c66e7-127">There are also pre-built entities, meaning that their behavior cannot be adjusted -- these are covered in another tutorial.</span></span>

### <a name="create-two-actions"></a><span data-ttu-id="c66e7-128">Create two actions</span><span class="sxs-lookup"><span data-stu-id="c66e7-128">Create two actions</span></span>

1. <span data-ttu-id="c66e7-129">Click Actions, then New Action</span><span class="sxs-lookup"><span data-stu-id="c66e7-129">Click Actions, then New Action</span></span>
2. <span data-ttu-id="c66e7-130">In Response, type 'I don't know what city you want'.</span><span class="sxs-lookup"><span data-stu-id="c66e7-130">In Response, type 'I don't know what city you want'.</span></span>
3. <span data-ttu-id="c66e7-131">In Disqualifying Entities, enter $city.</span><span class="sxs-lookup"><span data-stu-id="c66e7-131">In Disqualifying Entities, enter $city.</span></span> <span data-ttu-id="c66e7-132">Click Save.</span><span class="sxs-lookup"><span data-stu-id="c66e7-132">Click Save.</span></span>
    - <span data-ttu-id="c66e7-133">This means that if this entity is defined in bot's memory, then this action will *not* be available.</span><span class="sxs-lookup"><span data-stu-id="c66e7-133">This means that if this entity is defined in bot's memory, then this action will *not* be available.</span></span>
2. <span data-ttu-id="c66e7-134">Click Actions, then New Action to create a second action.</span><span class="sxs-lookup"><span data-stu-id="c66e7-134">Click Actions, then New Action to create a second action.</span></span>
3. <span data-ttu-id="c66e7-135">In Response, type 'The weather in the $city is probably sunny'.</span><span class="sxs-lookup"><span data-stu-id="c66e7-135">In Response, type 'The weather in the $city is probably sunny'.</span></span>
4. <span data-ttu-id="c66e7-136">In Required Entities, city entity has been added automatically since it was referred to.</span><span class="sxs-lookup"><span data-stu-id="c66e7-136">In Required Entities, city entity has been added automatically since it was referred to.</span></span>
5. <span data-ttu-id="c66e7-137">Click Save</span><span class="sxs-lookup"><span data-stu-id="c66e7-137">Click Save</span></span>

<span data-ttu-id="c66e7-138">Now you have two actions.</span><span class="sxs-lookup"><span data-stu-id="c66e7-138">Now you have two actions.</span></span>

![](../media/tutorial3_actions.PNG)

### <a name="train-the-bot"></a><span data-ttu-id="c66e7-139">Train the bot</span><span class="sxs-lookup"><span data-stu-id="c66e7-139">Train the bot</span></span>

1. <span data-ttu-id="c66e7-140">Click Train Dialogs, then New Train Dialog.</span><span class="sxs-lookup"><span data-stu-id="c66e7-140">Click Train Dialogs, then New Train Dialog.</span></span>
2. <span data-ttu-id="c66e7-141">Type 'hello'.</span><span class="sxs-lookup"><span data-stu-id="c66e7-141">Type 'hello'.</span></span>
3. <span data-ttu-id="c66e7-142">Click Score Actions, and Select 'I don't know what city you want?'</span><span class="sxs-lookup"><span data-stu-id="c66e7-142">Click Score Actions, and Select 'I don't know what city you want?'</span></span>
    - <span data-ttu-id="c66e7-143">The response where the city entity is required cannot be selected because the city entity is not defined in bot's memory.</span><span class="sxs-lookup"><span data-stu-id="c66e7-143">The response where the city entity is required cannot be selected because the city entity is not defined in bot's memory.</span></span>
2. <span data-ttu-id="c66e7-144">Select 'I don't know what city you want'.</span><span class="sxs-lookup"><span data-stu-id="c66e7-144">Select 'I don't know what city you want'.</span></span>
4. <span data-ttu-id="c66e7-145">Enter 'seattle'.</span><span class="sxs-lookup"><span data-stu-id="c66e7-145">Enter 'seattle'.</span></span> <span data-ttu-id="c66e7-146">Highlight seattle, then click city.</span><span class="sxs-lookup"><span data-stu-id="c66e7-146">Highlight seattle, then click city.</span></span>
5. <span data-ttu-id="c66e7-147">Click Score Actions</span><span class="sxs-lookup"><span data-stu-id="c66e7-147">Click Score Actions</span></span>
    - <span data-ttu-id="c66e7-148">City value is now in the bot's memory.</span><span class="sxs-lookup"><span data-stu-id="c66e7-148">City value is now in the bot's memory.</span></span>
    - <span data-ttu-id="c66e7-149">'Weather in $city is probably sunny' is now available as a response.</span><span class="sxs-lookup"><span data-stu-id="c66e7-149">'Weather in $city is probably sunny' is now available as a response.</span></span> 
6. <span data-ttu-id="c66e7-150">Select 'Weather in $city is probably sunny'.</span><span class="sxs-lookup"><span data-stu-id="c66e7-150">Select 'Weather in $city is probably sunny'.</span></span>

<span data-ttu-id="c66e7-151">Let's say user enters 'repeat that'.</span><span class="sxs-lookup"><span data-stu-id="c66e7-151">Let's say user enters 'repeat that'.</span></span> 
1. <span data-ttu-id="c66e7-152">Type that and enter.</span><span class="sxs-lookup"><span data-stu-id="c66e7-152">Type that and enter.</span></span> <span data-ttu-id="c66e7-153">City entity and its value is in memory and available.</span><span class="sxs-lookup"><span data-stu-id="c66e7-153">City entity and its value is in memory and available.</span></span>
2. <span data-ttu-id="c66e7-154">Select 'Weather in $city is probably sunny'.</span><span class="sxs-lookup"><span data-stu-id="c66e7-154">Select 'Weather in $city is probably sunny'.</span></span>

![](../media/tutorial3_entities.PNG)

<span data-ttu-id="c66e7-155">You have now created an entity and labeled instances of it in user messages.</span><span class="sxs-lookup"><span data-stu-id="c66e7-155">You have now created an entity and labeled instances of it in user messages.</span></span>  <span data-ttu-id="c66e7-156">You've also used the presence/absence of the entity in the bot's memory to control when actions are available, via the action's disqualifying and required entities fields.</span><span class="sxs-lookup"><span data-stu-id="c66e7-156">You've also used the presence/absence of the entity in the bot's memory to control when actions are available, via the action's disqualifying and required entities fields.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c66e7-157">Next steps</span><span class="sxs-lookup"><span data-stu-id="c66e7-157">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c66e7-158">Expected entity</span><span class="sxs-lookup"><span data-stu-id="c66e7-158">Expected entity</span></span>](./4-expected-entity.md)
