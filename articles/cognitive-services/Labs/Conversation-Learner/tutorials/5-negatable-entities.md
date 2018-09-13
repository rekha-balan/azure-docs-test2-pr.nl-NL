---
title: How to use negatable entities with a Conversation Learner model - Microsoft Cognitive Services | Microsoft Docs
titleSuffix: Azure
description: Learn how to use negatable entities with a Conversation Learner model.
services: cognitive-services
author: v-jaswel
manager: nolachar
ms.service: cognitive-services
ms.component: conversation-learner
ms.topic: article
ms.date: 04/30/2018
ms.author: v-jaswel
ms.openlocfilehash: 2fd00d53755e44e3a3d86782c40aa6a53ff4d378
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855567"
---
# <a name="how-to-use-negatable-entities-with-a-conversation-learner-model"></a><span data-ttu-id="cc6e0-103">How to use negatable entities with a Conversation Learner model</span><span class="sxs-lookup"><span data-stu-id="cc6e0-103">How to use negatable entities with a Conversation Learner model</span></span>

<span data-ttu-id="cc6e0-104">This tutorial demonstrates the "negatable" property of entities.</span><span class="sxs-lookup"><span data-stu-id="cc6e0-104">This tutorial demonstrates the "negatable" property of entities.</span></span>

## <a name="video"></a><span data-ttu-id="cc6e0-105">Video</span><span class="sxs-lookup"><span data-stu-id="cc6e0-105">Video</span></span>

<span data-ttu-id="cc6e0-106">[![Tutorial 5 Preview](http://aka.ms/cl-tutorial-05-preview)](http://aka.ms/blis-tutorial-05)</span><span class="sxs-lookup"><span data-stu-id="cc6e0-106">[![Tutorial 5 Preview](http://aka.ms/cl-tutorial-05-preview)](http://aka.ms/blis-tutorial-05)</span></span>

## <a name="requirements"></a><span data-ttu-id="cc6e0-107">Requirements</span><span class="sxs-lookup"><span data-stu-id="cc6e0-107">Requirements</span></span>
<span data-ttu-id="cc6e0-108">This tutorial requires that the general tutorial bot is running</span><span class="sxs-lookup"><span data-stu-id="cc6e0-108">This tutorial requires that the general tutorial bot is running</span></span>

    npm run tutorial-general

## <a name="details"></a><span data-ttu-id="cc6e0-109">Details</span><span class="sxs-lookup"><span data-stu-id="cc6e0-109">Details</span></span>
<span data-ttu-id="cc6e0-110">Mark an action as "negatable" if the user can "clear" an entity value, as in "No, I do not want $entity" or "no, not $entity."</span><span class="sxs-lookup"><span data-stu-id="cc6e0-110">Mark an action as "negatable" if the user can "clear" an entity value, as in "No, I do not want $entity" or "no, not $entity."</span></span> <span data-ttu-id="cc6e0-111">For example, "no, I do not want to leave from Boston."</span><span class="sxs-lookup"><span data-stu-id="cc6e0-111">For example, "no, I do not want to leave from Boston."</span></span>

<span data-ttu-id="cc6e0-112">Concretely, if the "negatable" property of an entity is set:</span><span class="sxs-lookup"><span data-stu-id="cc6e0-112">Concretely, if the "negatable" property of an entity is set:</span></span>

- <span data-ttu-id="cc6e0-113">When labeling entity mentions, allow you to label both normal (positive) instances of an entity, and a "negative" instances of the entity</span><span class="sxs-lookup"><span data-stu-id="cc6e0-113">When labeling entity mentions, allow you to label both normal (positive) instances of an entity, and a "negative" instances of the entity</span></span>
- <span data-ttu-id="cc6e0-114">LUIS learns two entity models: one for positive instances, and a second for negative instances</span><span class="sxs-lookup"><span data-stu-id="cc6e0-114">LUIS learns two entity models: one for positive instances, and a second for negative instances</span></span>
- <span data-ttu-id="cc6e0-115">The effect of a negative instance of an entity is to clear that value from the entity variable (if it exists)</span><span class="sxs-lookup"><span data-stu-id="cc6e0-115">The effect of a negative instance of an entity is to clear that value from the entity variable (if it exists)</span></span>

## <a name="steps"></a><span data-ttu-id="cc6e0-116">Steps</span><span class="sxs-lookup"><span data-stu-id="cc6e0-116">Steps</span></span>

### <a name="create-the-model"></a><span data-ttu-id="cc6e0-117">Create the model</span><span class="sxs-lookup"><span data-stu-id="cc6e0-117">Create the model</span></span>

1. <span data-ttu-id="cc6e0-118">In the Web UI, click New Model</span><span class="sxs-lookup"><span data-stu-id="cc6e0-118">In the Web UI, click New Model</span></span>
2. <span data-ttu-id="cc6e0-119">In Name, enter NegatableEntity.</span><span class="sxs-lookup"><span data-stu-id="cc6e0-119">In Name, enter NegatableEntity.</span></span> <span data-ttu-id="cc6e0-120">Then click Create.</span><span class="sxs-lookup"><span data-stu-id="cc6e0-120">Then click Create.</span></span>

### <a name="create-an-entity"></a><span data-ttu-id="cc6e0-121">Create an entity</span><span class="sxs-lookup"><span data-stu-id="cc6e0-121">Create an entity</span></span>

1. <span data-ttu-id="cc6e0-122">Click Entities, then New Entity.</span><span class="sxs-lookup"><span data-stu-id="cc6e0-122">Click Entities, then New Entity.</span></span>
2. <span data-ttu-id="cc6e0-123">In Entity Name, enter name.</span><span class="sxs-lookup"><span data-stu-id="cc6e0-123">In Entity Name, enter name.</span></span>
3. <span data-ttu-id="cc6e0-124">Check Negatable.</span><span class="sxs-lookup"><span data-stu-id="cc6e0-124">Check Negatable.</span></span>
    - <span data-ttu-id="cc6e0-125">This property indicates the user will be able to provide a value for the entity, or say something is *not* the value of the entity.</span><span class="sxs-lookup"><span data-stu-id="cc6e0-125">This property indicates the user will be able to provide a value for the entity, or say something is *not* the value of the entity.</span></span> <span data-ttu-id="cc6e0-126">In the latter case, this will result in deleting a matching value of the entity.</span><span class="sxs-lookup"><span data-stu-id="cc6e0-126">In the latter case, this will result in deleting a matching value of the entity.</span></span>
3. <span data-ttu-id="cc6e0-127">Click Create.</span><span class="sxs-lookup"><span data-stu-id="cc6e0-127">Click Create.</span></span>

![](../media/tutorial5_entities.PNG)

### <a name="create-two-actions"></a><span data-ttu-id="cc6e0-128">Create two actions</span><span class="sxs-lookup"><span data-stu-id="cc6e0-128">Create two actions</span></span>

1. <span data-ttu-id="cc6e0-129">Click Actions, then New Action</span><span class="sxs-lookup"><span data-stu-id="cc6e0-129">Click Actions, then New Action</span></span>
2. <span data-ttu-id="cc6e0-130">In Response, type 'I don't know your name'.</span><span class="sxs-lookup"><span data-stu-id="cc6e0-130">In Response, type 'I don't know your name'.</span></span>
3. <span data-ttu-id="cc6e0-131">In Disqualifying Entities, enter name.</span><span class="sxs-lookup"><span data-stu-id="cc6e0-131">In Disqualifying Entities, enter name.</span></span>
3. <span data-ttu-id="cc6e0-132">Click Create</span><span class="sxs-lookup"><span data-stu-id="cc6e0-132">Click Create</span></span>

<span data-ttu-id="cc6e0-133">Then create the second action.</span><span class="sxs-lookup"><span data-stu-id="cc6e0-133">Then create the second action.</span></span>

1. <span data-ttu-id="cc6e0-134">Click Actions, then New Action to create a second action.</span><span class="sxs-lookup"><span data-stu-id="cc6e0-134">Click Actions, then New Action to create a second action.</span></span>
3. <span data-ttu-id="cc6e0-135">In Response, type 'I know your name.</span><span class="sxs-lookup"><span data-stu-id="cc6e0-135">In Response, type 'I know your name.</span></span> <span data-ttu-id="cc6e0-136">It is $name'.</span><span class="sxs-lookup"><span data-stu-id="cc6e0-136">It is $name'.</span></span>
4. <span data-ttu-id="cc6e0-137">Click Create</span><span class="sxs-lookup"><span data-stu-id="cc6e0-137">Click Create</span></span>

<span data-ttu-id="cc6e0-138">Now you have two actions.</span><span class="sxs-lookup"><span data-stu-id="cc6e0-138">Now you have two actions.</span></span>

![](../media/tutorial5_actions.PNG)

### <a name="train-the-bot"></a><span data-ttu-id="cc6e0-139">Train the bot</span><span class="sxs-lookup"><span data-stu-id="cc6e0-139">Train the bot</span></span>

1. <span data-ttu-id="cc6e0-140">Click Train Dialogs, then New Train Dialog.</span><span class="sxs-lookup"><span data-stu-id="cc6e0-140">Click Train Dialogs, then New Train Dialog.</span></span>
2. <span data-ttu-id="cc6e0-141">Type 'hello'.</span><span class="sxs-lookup"><span data-stu-id="cc6e0-141">Type 'hello'.</span></span>
3. <span data-ttu-id="cc6e0-142">Click Score Actions, and Select 'I don't know your name'</span><span class="sxs-lookup"><span data-stu-id="cc6e0-142">Click Score Actions, and Select 'I don't know your name'</span></span>
    - <span data-ttu-id="cc6e0-143">The score is 100% because it is the only valid action.</span><span class="sxs-lookup"><span data-stu-id="cc6e0-143">The score is 100% because it is the only valid action.</span></span>
2. <span data-ttu-id="cc6e0-144">Enter 'my name is david'</span><span class="sxs-lookup"><span data-stu-id="cc6e0-144">Enter 'my name is david'</span></span>
3. <span data-ttu-id="cc6e0-145">Select 'david', and choose the label '+name'</span><span class="sxs-lookup"><span data-stu-id="cc6e0-145">Select 'david', and choose the label '+name'</span></span>
    - <span data-ttu-id="cc6e0-146">There are two instances of 'name': '+name' and '-name'.</span><span class="sxs-lookup"><span data-stu-id="cc6e0-146">There are two instances of 'name': '+name' and '-name'.</span></span>  <span data-ttu-id="cc6e0-147">(+) Plus adds or overwrites the value.</span><span class="sxs-lookup"><span data-stu-id="cc6e0-147">(+) Plus adds or overwrites the value.</span></span> <span data-ttu-id="cc6e0-148">(-) Minus removes the value.</span><span class="sxs-lookup"><span data-stu-id="cc6e0-148">(-) Minus removes the value.</span></span>
5. <span data-ttu-id="cc6e0-149">Click Score Actions</span><span class="sxs-lookup"><span data-stu-id="cc6e0-149">Click Score Actions</span></span>
    - <span data-ttu-id="cc6e0-150">The name value is now in the bot's memory.</span><span class="sxs-lookup"><span data-stu-id="cc6e0-150">The name value is now in the bot's memory.</span></span>
    - <span data-ttu-id="cc6e0-151">'I know your name.</span><span class="sxs-lookup"><span data-stu-id="cc6e0-151">'I know your name.</span></span> <span data-ttu-id="cc6e0-152">It is $name' is the only available response.</span><span class="sxs-lookup"><span data-stu-id="cc6e0-152">It is $name' is the only available response.</span></span> 
6. <span data-ttu-id="cc6e0-153">Select 'I know your name.</span><span class="sxs-lookup"><span data-stu-id="cc6e0-153">Select 'I know your name.</span></span> <span data-ttu-id="cc6e0-154">It is $name'.</span><span class="sxs-lookup"><span data-stu-id="cc6e0-154">It is $name'.</span></span>

<span data-ttu-id="cc6e0-155">Let's try clearing the negatable entity:</span><span class="sxs-lookup"><span data-stu-id="cc6e0-155">Let's try clearing the negatable entity:</span></span>

7. <span data-ttu-id="cc6e0-156">Enter 'my name is not david'.</span><span class="sxs-lookup"><span data-stu-id="cc6e0-156">Enter 'my name is not david'.</span></span>
    - <span data-ttu-id="cc6e0-157">Notice 'not' is selected as name based on the previous pattern.</span><span class="sxs-lookup"><span data-stu-id="cc6e0-157">Notice 'not' is selected as name based on the previous pattern.</span></span> <span data-ttu-id="cc6e0-158">This label is incorrect.</span><span class="sxs-lookup"><span data-stu-id="cc6e0-158">This label is incorrect.</span></span>
2. <span data-ttu-id="cc6e0-159">Click on 'not', then the red x.</span><span class="sxs-lookup"><span data-stu-id="cc6e0-159">Click on 'not', then the red x.</span></span> 
3. <span data-ttu-id="cc6e0-160">Click on 'david'.</span><span class="sxs-lookup"><span data-stu-id="cc6e0-160">Click on 'david'.</span></span>
    - <span data-ttu-id="cc6e0-161">This is now a negative entity communicating that this is not the value of the name entity.</span><span class="sxs-lookup"><span data-stu-id="cc6e0-161">This is now a negative entity communicating that this is not the value of the name entity.</span></span>
2. <span data-ttu-id="cc6e0-162">Select '-name'.</span><span class="sxs-lookup"><span data-stu-id="cc6e0-162">Select '-name'.</span></span>
3. <span data-ttu-id="cc6e0-163">Click Score Actions.</span><span class="sxs-lookup"><span data-stu-id="cc6e0-163">Click Score Actions.</span></span>
    - <span data-ttu-id="cc6e0-164">Notice the value has been cleared from memory.</span><span class="sxs-lookup"><span data-stu-id="cc6e0-164">Notice the value has been cleared from memory.</span></span>
2. <span data-ttu-id="cc6e0-165">Select 'I don't know your name', which is the only action.</span><span class="sxs-lookup"><span data-stu-id="cc6e0-165">Select 'I don't know your name', which is the only action.</span></span>

<span data-ttu-id="cc6e0-166">Next we show how a new value for the name can be entered.</span><span class="sxs-lookup"><span data-stu-id="cc6e0-166">Next we show how a new value for the name can be entered.</span></span>

3. <span data-ttu-id="cc6e0-167">Enter 'john' as the name.</span><span class="sxs-lookup"><span data-stu-id="cc6e0-167">Enter 'john' as the name.</span></span> <span data-ttu-id="cc6e0-168">Then select 'john' and click on name.</span><span class="sxs-lookup"><span data-stu-id="cc6e0-168">Then select 'john' and click on name.</span></span>
4. <span data-ttu-id="cc6e0-169">Click Score Actions.</span><span class="sxs-lookup"><span data-stu-id="cc6e0-169">Click Score Actions.</span></span>
5. <span data-ttu-id="cc6e0-170">Select 'I know your name.</span><span class="sxs-lookup"><span data-stu-id="cc6e0-170">Select 'I know your name.</span></span> <span data-ttu-id="cc6e0-171">It is $name'.</span><span class="sxs-lookup"><span data-stu-id="cc6e0-171">It is $name'.</span></span>

<span data-ttu-id="cc6e0-172">Now try replacing the entered name.</span><span class="sxs-lookup"><span data-stu-id="cc6e0-172">Now try replacing the entered name.</span></span>

6. <span data-ttu-id="cc6e0-173">Enter 'my name is susan'.</span><span class="sxs-lookup"><span data-stu-id="cc6e0-173">Enter 'my name is susan'.</span></span>
7. <span data-ttu-id="cc6e0-174">Select 'I know your name.</span><span class="sxs-lookup"><span data-stu-id="cc6e0-174">Select 'I know your name.</span></span> <span data-ttu-id="cc6e0-175">It is $name'.</span><span class="sxs-lookup"><span data-stu-id="cc6e0-175">It is $name'.</span></span>
7. <span data-ttu-id="cc6e0-176">Click Score Actions.</span><span class="sxs-lookup"><span data-stu-id="cc6e0-176">Click Score Actions.</span></span>
8. <span data-ttu-id="cc6e0-177">Notice **susan** has overwritten **john** in the entity values.</span><span class="sxs-lookup"><span data-stu-id="cc6e0-177">Notice **susan** has overwritten **john** in the entity values.</span></span>
9. <span data-ttu-id="cc6e0-178">Enter 'my name is not susan'.</span><span class="sxs-lookup"><span data-stu-id="cc6e0-178">Enter 'my name is not susan'.</span></span>
    - <span data-ttu-id="cc6e0-179">Notice the system has labeled this as a negative instance.</span><span class="sxs-lookup"><span data-stu-id="cc6e0-179">Notice the system has labeled this as a negative instance.</span></span>
2. <span data-ttu-id="cc6e0-180">Click Score Actions.</span><span class="sxs-lookup"><span data-stu-id="cc6e0-180">Click Score Actions.</span></span>
3. <span data-ttu-id="cc6e0-181">Select 'I don't know your name', which is the only action.</span><span class="sxs-lookup"><span data-stu-id="cc6e0-181">Select 'I don't know your name', which is the only action.</span></span>
7. <span data-ttu-id="cc6e0-182">Click Done Teaching.</span><span class="sxs-lookup"><span data-stu-id="cc6e0-182">Click Done Teaching.</span></span>

![](../media/tutorial5_dialogs.PNG)

## <a name="next-steps"></a><span data-ttu-id="cc6e0-183">Next steps</span><span class="sxs-lookup"><span data-stu-id="cc6e0-183">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="cc6e0-184">Multi-value entities</span><span class="sxs-lookup"><span data-stu-id="cc6e0-184">Multi-value entities</span></span>](./6-multi-value-entities.md)
