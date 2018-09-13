---
title: How to use multi-value entities with a Conversation Learner model - Microsoft Cognitive Services | Microsoft Docs
titleSuffix: Azure
description: Learn how to use multi-value entities with a Conversation Learner model.
services: cognitive-services
author: v-jaswel
manager: nolachar
ms.service: cognitive-services
ms.component: conversation-learner
ms.topic: article
ms.date: 04/30/2018
ms.author: v-jaswel
ms.openlocfilehash: 6193a515f0d8136e0d420b7554cf26fee8f50953
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865759"
---
# <a name="how-to-use-multi-value-entities-with-a-conversation-learner-model"></a><span data-ttu-id="a0625-103">How to use multi-value entities with a Conversation Learner model</span><span class="sxs-lookup"><span data-stu-id="a0625-103">How to use multi-value entities with a Conversation Learner model</span></span>
<span data-ttu-id="a0625-104">This tutorial shows the "multi-value" property of entities.</span><span class="sxs-lookup"><span data-stu-id="a0625-104">This tutorial shows the "multi-value" property of entities.</span></span>

## <a name="video"></a><span data-ttu-id="a0625-105">Video</span><span class="sxs-lookup"><span data-stu-id="a0625-105">Video</span></span>

<span data-ttu-id="a0625-106">[![Tutorial 6 Preview](http://aka.ms/cl-tutorial-06-preview)](http://aka.ms/blis-tutorial-06)</span><span class="sxs-lookup"><span data-stu-id="a0625-106">[![Tutorial 6 Preview](http://aka.ms/cl-tutorial-06-preview)](http://aka.ms/blis-tutorial-06)</span></span>

##<a name="requirements"></a><span data-ttu-id="a0625-107">Requirements</span><span class="sxs-lookup"><span data-stu-id="a0625-107">Requirements</span></span>
<span data-ttu-id="a0625-108">This tutorial requires that the general tutorial bot is running</span><span class="sxs-lookup"><span data-stu-id="a0625-108">This tutorial requires that the general tutorial bot is running</span></span>

    npm run tutorial-general

## <a name="details"></a><span data-ttu-id="a0625-109">Details</span><span class="sxs-lookup"><span data-stu-id="a0625-109">Details</span></span>
<span data-ttu-id="a0625-110">An entity which is "multi-value" accumulates values in a list, rather than storing a single value.</span><span class="sxs-lookup"><span data-stu-id="a0625-110">An entity which is "multi-value" accumulates values in a list, rather than storing a single value.</span></span>  <span data-ttu-id="a0625-111">This is useful for entities where the user can specify more than one value, such as toppings on a pizza.</span><span class="sxs-lookup"><span data-stu-id="a0625-111">This is useful for entities where the user can specify more than one value, such as toppings on a pizza.</span></span>

<span data-ttu-id="a0625-112">Concretely, if an entity is marked as "multi-value", then each recognized instance of the entity will be appended to a list in the bot's memory (rather than overwriting a single entity value).</span><span class="sxs-lookup"><span data-stu-id="a0625-112">Concretely, if an entity is marked as "multi-value", then each recognized instance of the entity will be appended to a list in the bot's memory (rather than overwriting a single entity value).</span></span>

## <a name="steps"></a><span data-ttu-id="a0625-113">Steps</span><span class="sxs-lookup"><span data-stu-id="a0625-113">Steps</span></span>

### <a name="create-the-model"></a><span data-ttu-id="a0625-114">Create the model</span><span class="sxs-lookup"><span data-stu-id="a0625-114">Create the model</span></span>

1. <span data-ttu-id="a0625-115">In the Web UI, click New Model</span><span class="sxs-lookup"><span data-stu-id="a0625-115">In the Web UI, click New Model</span></span>
2. <span data-ttu-id="a0625-116">In Name, enter MultiValueEntities.</span><span class="sxs-lookup"><span data-stu-id="a0625-116">In Name, enter MultiValueEntities.</span></span> <span data-ttu-id="a0625-117">Then click Create.</span><span class="sxs-lookup"><span data-stu-id="a0625-117">Then click Create.</span></span>

### <a name="create-an-entity"></a><span data-ttu-id="a0625-118">Create an entity</span><span class="sxs-lookup"><span data-stu-id="a0625-118">Create an entity</span></span>

1. <span data-ttu-id="a0625-119">Click Entities, then New Entity.</span><span class="sxs-lookup"><span data-stu-id="a0625-119">Click Entities, then New Entity.</span></span>
2. <span data-ttu-id="a0625-120">In Entity Name, enter Toppings.</span><span class="sxs-lookup"><span data-stu-id="a0625-120">In Entity Name, enter Toppings.</span></span>
3. <span data-ttu-id="a0625-121">Check Multi-valued.</span><span class="sxs-lookup"><span data-stu-id="a0625-121">Check Multi-valued.</span></span>
    - <span data-ttu-id="a0625-122">Multi-value entities accumulate one or more values in the entity.</span><span class="sxs-lookup"><span data-stu-id="a0625-122">Multi-value entities accumulate one or more values in the entity.</span></span>
2. <span data-ttu-id="a0625-123">Check Negatable.</span><span class="sxs-lookup"><span data-stu-id="a0625-123">Check Negatable.</span></span>  
    - <span data-ttu-id="a0625-124">This will allow the user to remove toppings from their list of accumulated pizza toppings.</span><span class="sxs-lookup"><span data-stu-id="a0625-124">This will allow the user to remove toppings from their list of accumulated pizza toppings.</span></span>
3. <span data-ttu-id="a0625-125">Click Create.</span><span class="sxs-lookup"><span data-stu-id="a0625-125">Click Create.</span></span>

![](../media/tutorial6_entities.PNG)

### <a name="create-two-actions"></a><span data-ttu-id="a0625-126">Create two actions</span><span class="sxs-lookup"><span data-stu-id="a0625-126">Create two actions</span></span>

1. <span data-ttu-id="a0625-127">Click Actions, then New Action</span><span class="sxs-lookup"><span data-stu-id="a0625-127">Click Actions, then New Action</span></span>
2. <span data-ttu-id="a0625-128">In Response, type 'What toppings do you want?'.</span><span class="sxs-lookup"><span data-stu-id="a0625-128">In Response, type 'What toppings do you want?'.</span></span>
3. <span data-ttu-id="a0625-129">In Disqualifying Entities, enter Toppings.</span><span class="sxs-lookup"><span data-stu-id="a0625-129">In Disqualifying Entities, enter Toppings.</span></span>
3. <span data-ttu-id="a0625-130">Click Create</span><span class="sxs-lookup"><span data-stu-id="a0625-130">Click Create</span></span>

<span data-ttu-id="a0625-131">Then create the second action.</span><span class="sxs-lookup"><span data-stu-id="a0625-131">Then create the second action.</span></span>

1. <span data-ttu-id="a0625-132">Click Actions, then New Action to create a second action.</span><span class="sxs-lookup"><span data-stu-id="a0625-132">Click Actions, then New Action to create a second action.</span></span>
3. <span data-ttu-id="a0625-133">In Response, type 'Here are your toppings: $Toppings'.</span><span class="sxs-lookup"><span data-stu-id="a0625-133">In Response, type 'Here are your toppings: $Toppings'.</span></span>
4. <span data-ttu-id="a0625-134">Click Create</span><span class="sxs-lookup"><span data-stu-id="a0625-134">Click Create</span></span>

<span data-ttu-id="a0625-135">Now you have two actions.</span><span class="sxs-lookup"><span data-stu-id="a0625-135">Now you have two actions.</span></span>

![](../media/tutorial6_actions.PNG)

### <a name="train-the-bot"></a><span data-ttu-id="a0625-136">Train the bot</span><span class="sxs-lookup"><span data-stu-id="a0625-136">Train the bot</span></span>

1. <span data-ttu-id="a0625-137">Click Train Dialogs, then New Train Dialog.</span><span class="sxs-lookup"><span data-stu-id="a0625-137">Click Train Dialogs, then New Train Dialog.</span></span>
2. <span data-ttu-id="a0625-138">Type 'hello'.</span><span class="sxs-lookup"><span data-stu-id="a0625-138">Type 'hello'.</span></span>
3. <span data-ttu-id="a0625-139">Click Score Actions, and Select 'What toppings do you want?'</span><span class="sxs-lookup"><span data-stu-id="a0625-139">Click Score Actions, and Select 'What toppings do you want?'</span></span>
2. <span data-ttu-id="a0625-140">Enter 'mushrooms and cheese'.</span><span class="sxs-lookup"><span data-stu-id="a0625-140">Enter 'mushrooms and cheese'.</span></span> 
    - <span data-ttu-id="a0625-141">You can label zero, one or more than one of the entities.</span><span class="sxs-lookup"><span data-stu-id="a0625-141">You can label zero, one or more than one of the entities.</span></span>
3. <span data-ttu-id="a0625-142">Click 'mushrooms', and select Toppings.</span><span class="sxs-lookup"><span data-stu-id="a0625-142">Click 'mushrooms', and select Toppings.</span></span>
4. <span data-ttu-id="a0625-143">Click 'cheese', and select Toppings.</span><span class="sxs-lookup"><span data-stu-id="a0625-143">Click 'cheese', and select Toppings.</span></span>
5. <span data-ttu-id="a0625-144">Click Score Actions</span><span class="sxs-lookup"><span data-stu-id="a0625-144">Click Score Actions</span></span>
    - <span data-ttu-id="a0625-145">The two values are now present in the Toppings entity.</span><span class="sxs-lookup"><span data-stu-id="a0625-145">The two values are now present in the Toppings entity.</span></span> 
6. <span data-ttu-id="a0625-146">Select 'Here are your toppings: $Toppings'.</span><span class="sxs-lookup"><span data-stu-id="a0625-146">Select 'Here are your toppings: $Toppings'.</span></span>

<span data-ttu-id="a0625-147">We can add more to this:</span><span class="sxs-lookup"><span data-stu-id="a0625-147">We can add more to this:</span></span>

7. <span data-ttu-id="a0625-148">Enter 'add peppers'.</span><span class="sxs-lookup"><span data-stu-id="a0625-148">Enter 'add peppers'.</span></span>
    - <span data-ttu-id="a0625-149">Click on 'peppers' under Entity Detection, and select Toppings.</span><span class="sxs-lookup"><span data-stu-id="a0625-149">Click on 'peppers' under Entity Detection, and select Toppings.</span></span>
3. <span data-ttu-id="a0625-150">Click Score Actions.</span><span class="sxs-lookup"><span data-stu-id="a0625-150">Click Score Actions.</span></span>
    - <span data-ttu-id="a0625-151">'peppers' now shows up as an additional value in Toppings.</span><span class="sxs-lookup"><span data-stu-id="a0625-151">'peppers' now shows up as an additional value in Toppings.</span></span>
6. <span data-ttu-id="a0625-152">Select 'Here are your toppings: $Toppings'.</span><span class="sxs-lookup"><span data-stu-id="a0625-152">Select 'Here are your toppings: $Toppings'.</span></span>

<span data-ttu-id="a0625-153">Let's remove a topping and add one:</span><span class="sxs-lookup"><span data-stu-id="a0625-153">Let's remove a topping and add one:</span></span>

2. <span data-ttu-id="a0625-154">Type 'remove peppers and add sausage'.</span><span class="sxs-lookup"><span data-stu-id="a0625-154">Type 'remove peppers and add sausage'.</span></span>
1. <span data-ttu-id="a0625-155">Click on 'peppers' and click on the red x to remove it.</span><span class="sxs-lookup"><span data-stu-id="a0625-155">Click on 'peppers' and click on the red x to remove it.</span></span>
2. <span data-ttu-id="a0625-156">Click on 'peppers' and select '-Toppings'.</span><span class="sxs-lookup"><span data-stu-id="a0625-156">Click on 'peppers' and select '-Toppings'.</span></span>
3. <span data-ttu-id="a0625-157">Click Score Actions.</span><span class="sxs-lookup"><span data-stu-id="a0625-157">Click Score Actions.</span></span>
    - <span data-ttu-id="a0625-158">'peppers' has been deleted and 'sausage' has been added.</span><span class="sxs-lookup"><span data-stu-id="a0625-158">'peppers' has been deleted and 'sausage' has been added.</span></span>
6. <span data-ttu-id="a0625-159">Select 'Here are your toppings: $Toppings'.</span><span class="sxs-lookup"><span data-stu-id="a0625-159">Select 'Here are your toppings: $Toppings'.</span></span>

<span data-ttu-id="a0625-160">Now let's try removing everything:</span><span class="sxs-lookup"><span data-stu-id="a0625-160">Now let's try removing everything:</span></span>

6. <span data-ttu-id="a0625-161">Enter 'remove mushrooms, remove cheese, and remove sausage'.</span><span class="sxs-lookup"><span data-stu-id="a0625-161">Enter 'remove mushrooms, remove cheese, and remove sausage'.</span></span>
7. <span data-ttu-id="a0625-162">Click on each of the three, and select '-Toppings'.</span><span class="sxs-lookup"><span data-stu-id="a0625-162">Click on each of the three, and select '-Toppings'.</span></span>
7. <span data-ttu-id="a0625-163">Click Score Actions.</span><span class="sxs-lookup"><span data-stu-id="a0625-163">Click Score Actions.</span></span>
    - <span data-ttu-id="a0625-164">All toppings are cleared.</span><span class="sxs-lookup"><span data-stu-id="a0625-164">All toppings are cleared.</span></span>
2. <span data-ttu-id="a0625-165">Select 'What toppings do you want?'</span><span class="sxs-lookup"><span data-stu-id="a0625-165">Select 'What toppings do you want?'</span></span>
3. <span data-ttu-id="a0625-166">Click Done Teaching</span><span class="sxs-lookup"><span data-stu-id="a0625-166">Click Done Teaching</span></span>

![](../media/tutorial6_dialogs.PNG)

## <a name="next-steps"></a><span data-ttu-id="a0625-167">Next steps</span><span class="sxs-lookup"><span data-stu-id="a0625-167">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a0625-168">Built-in entities</span><span class="sxs-lookup"><span data-stu-id="a0625-168">Built-in entities</span></span>](./7-built-in-entities.md)
