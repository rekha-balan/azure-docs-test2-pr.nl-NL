---
title: How to use the "expected entity" property of Conversation Learner actions - Microsoft Cognitive Services | Microsoft Docs
titleSuffix: Azure
description: Learn how to use the "expected entity" property of a Conversation Learner model.
services: cognitive-services
author: v-jaswel
manager: nolachar
ms.service: cognitive-services
ms.component: conversation-learner
ms.topic: article
ms.date: 04/30/2018
ms.author: v-jaswel
ms.openlocfilehash: a43c52143f936eaefd4383714b1c67b6b74d34e8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871101"
---
# <a name="how-to-use-the-expected-entity-property-of-actions"></a><span data-ttu-id="d3156-103">How to use the "Expected entity" property of actions</span><span class="sxs-lookup"><span data-stu-id="d3156-103">How to use the "Expected entity" property of actions</span></span>

<span data-ttu-id="d3156-104">This tutorial demonstrates the "expected entity" field of actions.</span><span class="sxs-lookup"><span data-stu-id="d3156-104">This tutorial demonstrates the "expected entity" field of actions.</span></span>

## <a name="video"></a><span data-ttu-id="d3156-105">Video</span><span class="sxs-lookup"><span data-stu-id="d3156-105">Video</span></span>

<span data-ttu-id="d3156-106">[![Tutorial 4 Preview](http://aka.ms/cl-tutorial-04-preview)](http://aka.ms/blis-tutorial-04)</span><span class="sxs-lookup"><span data-stu-id="d3156-106">[![Tutorial 4 Preview](http://aka.ms/cl-tutorial-04-preview)](http://aka.ms/blis-tutorial-04)</span></span>

## <a name="requirements"></a><span data-ttu-id="d3156-107">Requirements</span><span class="sxs-lookup"><span data-stu-id="d3156-107">Requirements</span></span>
<span data-ttu-id="d3156-108">This tutorial requires that the general tutorial bot is running</span><span class="sxs-lookup"><span data-stu-id="d3156-108">This tutorial requires that the general tutorial bot is running</span></span>

    npm run tutorial-general

## <a name="details"></a><span data-ttu-id="d3156-109">Details</span><span class="sxs-lookup"><span data-stu-id="d3156-109">Details</span></span>
<span data-ttu-id="d3156-110">Use the "expected entity" field of an action to communicate to the system that you expect the user's response to an action will be to state an entity.</span><span class="sxs-lookup"><span data-stu-id="d3156-110">Use the "expected entity" field of an action to communicate to the system that you expect the user's response to an action will be to state an entity.</span></span>

<span data-ttu-id="d3156-111">Concretely, if the "expected entity" field of an action is set to $entity, then on the next user utterance, the system will:</span><span class="sxs-lookup"><span data-stu-id="d3156-111">Concretely, if the "expected entity" field of an action is set to $entity, then on the next user utterance, the system will:</span></span>

1. <span data-ttu-id="d3156-112">First, as usual, attempt to find entities using the machine-learning based entity extraction model</span><span class="sxs-lookup"><span data-stu-id="d3156-112">First, as usual, attempt to find entities using the machine-learning based entity extraction model</span></span>
2. <span data-ttu-id="d3156-113">If no entities are found in step 1, then -- as a heuristic -- assign the whole user utterance to $entity.</span><span class="sxs-lookup"><span data-stu-id="d3156-113">If no entities are found in step 1, then -- as a heuristic -- assign the whole user utterance to $entity.</span></span>
3. <span data-ttu-id="d3156-114">Call `EntityDetectionCallback` as usual, and proceed to action selection.</span><span class="sxs-lookup"><span data-stu-id="d3156-114">Call `EntityDetectionCallback` as usual, and proceed to action selection.</span></span>

## <a name="steps"></a><span data-ttu-id="d3156-115">Steps</span><span class="sxs-lookup"><span data-stu-id="d3156-115">Steps</span></span>

### <a name="create-the-model"></a><span data-ttu-id="d3156-116">Create the model</span><span class="sxs-lookup"><span data-stu-id="d3156-116">Create the model</span></span>

1. <span data-ttu-id="d3156-117">In the Web UI, click New Model</span><span class="sxs-lookup"><span data-stu-id="d3156-117">In the Web UI, click New Model</span></span>
2. <span data-ttu-id="d3156-118">In Name, enter ExpectedEntities.</span><span class="sxs-lookup"><span data-stu-id="d3156-118">In Name, enter ExpectedEntities.</span></span> <span data-ttu-id="d3156-119">Then click Create.</span><span class="sxs-lookup"><span data-stu-id="d3156-119">Then click Create.</span></span>

### <a name="create-an-entity"></a><span data-ttu-id="d3156-120">Create an entity</span><span class="sxs-lookup"><span data-stu-id="d3156-120">Create an entity</span></span>

1. <span data-ttu-id="d3156-121">Click Entities, then New Entity.</span><span class="sxs-lookup"><span data-stu-id="d3156-121">Click Entities, then New Entity.</span></span>
2. <span data-ttu-id="d3156-122">In Entity Name, enter name.</span><span class="sxs-lookup"><span data-stu-id="d3156-122">In Entity Name, enter name.</span></span>
3. <span data-ttu-id="d3156-123">Click Create</span><span class="sxs-lookup"><span data-stu-id="d3156-123">Click Create</span></span>

> [!NOTE]
> <span data-ttu-id="d3156-124">The entity type is 'custom'.</span><span class="sxs-lookup"><span data-stu-id="d3156-124">The entity type is 'custom'.</span></span> <span data-ttu-id="d3156-125">This value means that the entity can be trained.</span><span class="sxs-lookup"><span data-stu-id="d3156-125">This value means that the entity can be trained.</span></span>  <span data-ttu-id="d3156-126">There are also pre-built entities, meaning that their behavior cannot be adjusted.</span><span class="sxs-lookup"><span data-stu-id="d3156-126">There are also pre-built entities, meaning that their behavior cannot be adjusted.</span></span>  <span data-ttu-id="d3156-127">These entities are covered in the [Pre-Built Entities tutorial](./7-built-in-entities.md).</span><span class="sxs-lookup"><span data-stu-id="d3156-127">These entities are covered in the [Pre-Built Entities tutorial](./7-built-in-entities.md).</span></span>

![](../media/tutorial4_entities.PNG)

### <a name="create-two-actions"></a><span data-ttu-id="d3156-128">Create two actions</span><span class="sxs-lookup"><span data-stu-id="d3156-128">Create two actions</span></span>

1. <span data-ttu-id="d3156-129">Click Actions, then New Action.</span><span class="sxs-lookup"><span data-stu-id="d3156-129">Click Actions, then New Action.</span></span>
2. <span data-ttu-id="d3156-130">In Response, type 'What's your name?'.</span><span class="sxs-lookup"><span data-stu-id="d3156-130">In Response, type 'What's your name?'.</span></span>
3. <span data-ttu-id="d3156-131">In Expected Entities, enter $name.</span><span class="sxs-lookup"><span data-stu-id="d3156-131">In Expected Entities, enter $name.</span></span> <span data-ttu-id="d3156-132">Click Save.</span><span class="sxs-lookup"><span data-stu-id="d3156-132">Click Save.</span></span>
    - <span data-ttu-id="d3156-133">This value means that if this question is asked, and the user response does not have any entities detected, the bot should assume the whole of the user's response is this entity.</span><span class="sxs-lookup"><span data-stu-id="d3156-133">This value means that if this question is asked, and the user response does not have any entities detected, the bot should assume the whole of the user's response is this entity.</span></span>
2. <span data-ttu-id="d3156-134">Click Actions, then New Action to create a second action.</span><span class="sxs-lookup"><span data-stu-id="d3156-134">Click Actions, then New Action to create a second action.</span></span>
3. <span data-ttu-id="d3156-135">In Response, type 'Hello $name'.</span><span class="sxs-lookup"><span data-stu-id="d3156-135">In Response, type 'Hello $name'.</span></span>
    - <span data-ttu-id="d3156-136">Note that the entity is automatically added as a required entity.</span><span class="sxs-lookup"><span data-stu-id="d3156-136">Note that the entity is automatically added as a required entity.</span></span> 
4. <span data-ttu-id="d3156-137">Click Save.</span><span class="sxs-lookup"><span data-stu-id="d3156-137">Click Save.</span></span>

<span data-ttu-id="d3156-138">Now you have two actions.</span><span class="sxs-lookup"><span data-stu-id="d3156-138">Now you have two actions.</span></span>

![](../media/tutorial4_actions.PNG)

### <a name="train-the-bot"></a><span data-ttu-id="d3156-139">Train the bot</span><span class="sxs-lookup"><span data-stu-id="d3156-139">Train the bot</span></span>

1. <span data-ttu-id="d3156-140">Click Train Dialogs, then New Train Dialog.</span><span class="sxs-lookup"><span data-stu-id="d3156-140">Click Train Dialogs, then New Train Dialog.</span></span>
2. <span data-ttu-id="d3156-141">Type 'hello'.</span><span class="sxs-lookup"><span data-stu-id="d3156-141">Type 'hello'.</span></span>
3. <span data-ttu-id="d3156-142">Click Score Actions, and Select 'What's your name?'</span><span class="sxs-lookup"><span data-stu-id="d3156-142">Click Score Actions, and Select 'What's your name?'</span></span>
    - <span data-ttu-id="d3156-143">The response 'Hello $name' cannot be selected, because it requires the entity $name to be defined, and $name is not in the bot's memory.</span><span class="sxs-lookup"><span data-stu-id="d3156-143">The response 'Hello $name' cannot be selected, because it requires the entity $name to be defined, and $name is not in the bot's memory.</span></span>
2. <span data-ttu-id="d3156-144">Enter 'david'.</span><span class="sxs-lookup"><span data-stu-id="d3156-144">Enter 'david'.</span></span> 
    - <span data-ttu-id="d3156-145">The name is highlighted as an entity.</span><span class="sxs-lookup"><span data-stu-id="d3156-145">The name is highlighted as an entity.</span></span> <span data-ttu-id="d3156-146">This is because of the heuristic we set up above to select the response as the entity.</span><span class="sxs-lookup"><span data-stu-id="d3156-146">This is because of the heuristic we set up above to select the response as the entity.</span></span>
5. <span data-ttu-id="d3156-147">Click Score Actions</span><span class="sxs-lookup"><span data-stu-id="d3156-147">Click Score Actions</span></span>
    - <span data-ttu-id="d3156-148">The name value is now in the bot's memory.</span><span class="sxs-lookup"><span data-stu-id="d3156-148">The name value is now in the bot's memory.</span></span>
    - <span data-ttu-id="d3156-149">'Hello $name' is now available as a response.</span><span class="sxs-lookup"><span data-stu-id="d3156-149">'Hello $name' is now available as a response.</span></span> 
6. <span data-ttu-id="d3156-150">Select 'Hello $name'.</span><span class="sxs-lookup"><span data-stu-id="d3156-150">Select 'Hello $name'.</span></span>
7. <span data-ttu-id="d3156-151">Click Done Teaching.</span><span class="sxs-lookup"><span data-stu-id="d3156-151">Click Done Teaching.</span></span>

<span data-ttu-id="d3156-152">Here are two examples where the machine-learning entity extraction model identifies a name, so the "expected entity" heuristic isn't triggered.</span><span class="sxs-lookup"><span data-stu-id="d3156-152">Here are two examples where the machine-learning entity extraction model identifies a name, so the "expected entity" heuristic isn't triggered.</span></span>

1. <span data-ttu-id="d3156-153">Click New Train Dialog.</span><span class="sxs-lookup"><span data-stu-id="d3156-153">Click New Train Dialog.</span></span>
2. <span data-ttu-id="d3156-154">Enter 'my name is david'.</span><span class="sxs-lookup"><span data-stu-id="d3156-154">Enter 'my name is david'.</span></span>
    - <span data-ttu-id="d3156-155">The model identifies david as the name entity because it has seen this word before.</span><span class="sxs-lookup"><span data-stu-id="d3156-155">The model identifies david as the name entity because it has seen this word before.</span></span>
2. <span data-ttu-id="d3156-156">Click Score Actions</span><span class="sxs-lookup"><span data-stu-id="d3156-156">Click Score Actions</span></span>
3. <span data-ttu-id="d3156-157">Select 'Hello $name'.</span><span class="sxs-lookup"><span data-stu-id="d3156-157">Select 'Hello $name'.</span></span>
4. <span data-ttu-id="d3156-158">Enter 'my name is susan'.</span><span class="sxs-lookup"><span data-stu-id="d3156-158">Enter 'my name is susan'.</span></span>
    - <span data-ttu-id="d3156-159">The model identifies susan as the name since it has seen this pattern already.</span><span class="sxs-lookup"><span data-stu-id="d3156-159">The model identifies susan as the name since it has seen this pattern already.</span></span>
2. <span data-ttu-id="d3156-160">Click Score Actions.</span><span class="sxs-lookup"><span data-stu-id="d3156-160">Click Score Actions.</span></span>
2. <span data-ttu-id="d3156-161">Select 'Hello susan'.</span><span class="sxs-lookup"><span data-stu-id="d3156-161">Select 'Hello susan'.</span></span>
3. <span data-ttu-id="d3156-162">Click Done Teaching.</span><span class="sxs-lookup"><span data-stu-id="d3156-162">Click Done Teaching.</span></span>

<span data-ttu-id="d3156-163">In the following examples, the "expected entity" heuristic triggers, but is incorrect.</span><span class="sxs-lookup"><span data-stu-id="d3156-163">In the following examples, the "expected entity" heuristic triggers, but is incorrect.</span></span> <span data-ttu-id="d3156-164">The examples then show how to make a correction.</span><span class="sxs-lookup"><span data-stu-id="d3156-164">The examples then show how to make a correction.</span></span>

1. <span data-ttu-id="d3156-165">Type in 'call me jose'.</span><span class="sxs-lookup"><span data-stu-id="d3156-165">Type in 'call me jose'.</span></span>
    - <span data-ttu-id="d3156-166">The model does not recognize the name as an entity.</span><span class="sxs-lookup"><span data-stu-id="d3156-166">The model does not recognize the name as an entity.</span></span>
2. <span data-ttu-id="d3156-167">Click on jose, and select name.</span><span class="sxs-lookup"><span data-stu-id="d3156-167">Click on jose, and select name.</span></span>
3. <span data-ttu-id="d3156-168">Click Score Actions.</span><span class="sxs-lookup"><span data-stu-id="d3156-168">Click Score Actions.</span></span>
4. <span data-ttu-id="d3156-169">Select hello $name.</span><span class="sxs-lookup"><span data-stu-id="d3156-169">Select hello $name.</span></span>
5. <span data-ttu-id="d3156-170">Click Done Teaching.</span><span class="sxs-lookup"><span data-stu-id="d3156-170">Click Done Teaching.</span></span>
1. <span data-ttu-id="d3156-171">Click New Train Dialog.</span><span class="sxs-lookup"><span data-stu-id="d3156-171">Click New Train Dialog.</span></span>
2. <span data-ttu-id="d3156-172">Enter 'hello'.</span><span class="sxs-lookup"><span data-stu-id="d3156-172">Enter 'hello'.</span></span>
3. <span data-ttu-id="d3156-173">In response to 'what's your name', enter 'I am called frank'.</span><span class="sxs-lookup"><span data-stu-id="d3156-173">In response to 'what's your name', enter 'I am called frank'.</span></span>
    - <span data-ttu-id="d3156-174">The entire phrase is highlighted.</span><span class="sxs-lookup"><span data-stu-id="d3156-174">The entire phrase is highlighted.</span></span> <span data-ttu-id="d3156-175">This is because the statistical model did not find a name, so the heuristic fired and selected the entire answer as the name entity.</span><span class="sxs-lookup"><span data-stu-id="d3156-175">This is because the statistical model did not find a name, so the heuristic fired and selected the entire answer as the name entity.</span></span>
2. <span data-ttu-id="d3156-176">To correct it, click on the highlighted phrase, then click on the red x.</span><span class="sxs-lookup"><span data-stu-id="d3156-176">To correct it, click on the highlighted phrase, then click on the red x.</span></span> 
3. <span data-ttu-id="d3156-177">Click to select frank, then click on name.</span><span class="sxs-lookup"><span data-stu-id="d3156-177">Click to select frank, then click on name.</span></span>
2. <span data-ttu-id="d3156-178">Click Score Actions</span><span class="sxs-lookup"><span data-stu-id="d3156-178">Click Score Actions</span></span>
3. <span data-ttu-id="d3156-179">Select 'Hello $name'.</span><span class="sxs-lookup"><span data-stu-id="d3156-179">Select 'Hello $name'.</span></span>
4. <span data-ttu-id="d3156-180">Click Done Teaching.</span><span class="sxs-lookup"><span data-stu-id="d3156-180">Click Done Teaching.</span></span>

![](../media/tutorial4_dialogs.PNG)

## <a name="next-steps"></a><span data-ttu-id="d3156-181">Next steps</span><span class="sxs-lookup"><span data-stu-id="d3156-181">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d3156-182">Negatable entities</span><span class="sxs-lookup"><span data-stu-id="d3156-182">Negatable entities</span></span>](./5-negatable-entities.md)
