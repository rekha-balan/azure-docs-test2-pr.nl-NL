---
title: How to use alternative inputs with Conversation Learner - Microsoft Cognitive Services | Microsoft Docs
titleSuffix: Azure
description: Learn how to use alternative inputs with Conversation Learner.
services: cognitive-services
author: v-jaswel
manager: nolachar
ms.service: cognitive-services
ms.component: conversation-learner
ms.topic: article
ms.date: 04/30/2018
ms.author: v-jaswel
ms.openlocfilehash: 8d3b3f419ceacbb9a6fe2b19cf68ea6873de536f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966517"
---
# <a name="how-to-use-alternative-inputs"></a><span data-ttu-id="0bf00-103">How to use alternative inputs</span><span class="sxs-lookup"><span data-stu-id="0bf00-103">How to use alternative inputs</span></span>

<span data-ttu-id="0bf00-104">This tutorial shows how to use the "alternative inputs" field for user input in the teaching interface.</span><span class="sxs-lookup"><span data-stu-id="0bf00-104">This tutorial shows how to use the "alternative inputs" field for user input in the teaching interface.</span></span>

## <a name="video"></a><span data-ttu-id="0bf00-105">Video</span><span class="sxs-lookup"><span data-stu-id="0bf00-105">Video</span></span>

<span data-ttu-id="0bf00-106">[![Tutorial 8 Preview](http://aka.ms/cl-tutorial-08-preview)](http://aka.ms/blis-tutorial-08)</span><span class="sxs-lookup"><span data-stu-id="0bf00-106">[![Tutorial 8 Preview](http://aka.ms/cl-tutorial-08-preview)](http://aka.ms/blis-tutorial-08)</span></span>

## <a name="requirements"></a><span data-ttu-id="0bf00-107">Requirements</span><span class="sxs-lookup"><span data-stu-id="0bf00-107">Requirements</span></span>
<span data-ttu-id="0bf00-108">This tutorial requires that the general tutorial bot is running</span><span class="sxs-lookup"><span data-stu-id="0bf00-108">This tutorial requires that the general tutorial bot is running</span></span>

    npm run tutorial-general

## <a name="details"></a><span data-ttu-id="0bf00-109">Details</span><span class="sxs-lookup"><span data-stu-id="0bf00-109">Details</span></span>
<span data-ttu-id="0bf00-110">"Alternative inputs" are alternate user utterances which the user could have said at a particular point in a training dialog.</span><span class="sxs-lookup"><span data-stu-id="0bf00-110">"Alternative inputs" are alternate user utterances which the user could have said at a particular point in a training dialog.</span></span> <span data-ttu-id="0bf00-111">Alternative inputs allow you to more compactly specify variations of what a user might say, without having to list each variation in a separate training dialog.</span><span class="sxs-lookup"><span data-stu-id="0bf00-111">Alternative inputs allow you to more compactly specify variations of what a user might say, without having to list each variation in a separate training dialog.</span></span>

## <a name="steps"></a><span data-ttu-id="0bf00-112">Steps</span><span class="sxs-lookup"><span data-stu-id="0bf00-112">Steps</span></span>

### <a name="create-the-model"></a><span data-ttu-id="0bf00-113">Create the model</span><span class="sxs-lookup"><span data-stu-id="0bf00-113">Create the model</span></span>

1. <span data-ttu-id="0bf00-114">In the Web UI, click New Model</span><span class="sxs-lookup"><span data-stu-id="0bf00-114">In the Web UI, click New Model</span></span>
2. <span data-ttu-id="0bf00-115">In Name, enter AlternativeInputs.</span><span class="sxs-lookup"><span data-stu-id="0bf00-115">In Name, enter AlternativeInputs.</span></span> <span data-ttu-id="0bf00-116">Then click Create.</span><span class="sxs-lookup"><span data-stu-id="0bf00-116">Then click Create.</span></span>

### <a name="create-an-entity"></a><span data-ttu-id="0bf00-117">Create an entity</span><span class="sxs-lookup"><span data-stu-id="0bf00-117">Create an entity</span></span>

1. <span data-ttu-id="0bf00-118">Click Entities, then New Entity.</span><span class="sxs-lookup"><span data-stu-id="0bf00-118">Click Entities, then New Entity.</span></span>
2. <span data-ttu-id="0bf00-119">In Entity Name, enter city.</span><span class="sxs-lookup"><span data-stu-id="0bf00-119">In Entity Name, enter city.</span></span>
3. <span data-ttu-id="0bf00-120">Click Create.</span><span class="sxs-lookup"><span data-stu-id="0bf00-120">Click Create.</span></span>

### <a name="create-three-actions"></a><span data-ttu-id="0bf00-121">Create three actions</span><span class="sxs-lookup"><span data-stu-id="0bf00-121">Create three actions</span></span>

1. <span data-ttu-id="0bf00-122">Click Actions, then New Action</span><span class="sxs-lookup"><span data-stu-id="0bf00-122">Click Actions, then New Action</span></span>
2. <span data-ttu-id="0bf00-123">In Response, type 'Which city do you want?'.</span><span class="sxs-lookup"><span data-stu-id="0bf00-123">In Response, type 'Which city do you want?'.</span></span>
3. <span data-ttu-id="0bf00-124">In Disqualifying Entities, enter $city.</span><span class="sxs-lookup"><span data-stu-id="0bf00-124">In Disqualifying Entities, enter $city.</span></span>
3. <span data-ttu-id="0bf00-125">Click Create</span><span class="sxs-lookup"><span data-stu-id="0bf00-125">Click Create</span></span>

<span data-ttu-id="0bf00-126">Then create the second action:</span><span class="sxs-lookup"><span data-stu-id="0bf00-126">Then create the second action:</span></span>

1. <span data-ttu-id="0bf00-127">Click Actions, then New Action.</span><span class="sxs-lookup"><span data-stu-id="0bf00-127">Click Actions, then New Action.</span></span>
3. <span data-ttu-id="0bf00-128">In Response, type 'The weather in $city is probably sunny'.</span><span class="sxs-lookup"><span data-stu-id="0bf00-128">In Response, type 'The weather in $city is probably sunny'.</span></span>
4. <span data-ttu-id="0bf00-129">Required Entities, enter $city.</span><span class="sxs-lookup"><span data-stu-id="0bf00-129">Required Entities, enter $city.</span></span>
4. <span data-ttu-id="0bf00-130">Click Create.</span><span class="sxs-lookup"><span data-stu-id="0bf00-130">Click Create.</span></span>

<span data-ttu-id="0bf00-131">Create the third action:</span><span class="sxs-lookup"><span data-stu-id="0bf00-131">Create the third action:</span></span>

1. <span data-ttu-id="0bf00-132">Click Actions, then New Action.</span><span class="sxs-lookup"><span data-stu-id="0bf00-132">Click Actions, then New Action.</span></span>
3. <span data-ttu-id="0bf00-133">In Response, type 'Try asking for the weather'.</span><span class="sxs-lookup"><span data-stu-id="0bf00-133">In Response, type 'Try asking for the weather'.</span></span>
    - <span data-ttu-id="0bf00-134">This would be in response to user's question such as 'what can the system do?'</span><span class="sxs-lookup"><span data-stu-id="0bf00-134">This would be in response to user's question such as 'what can the system do?'</span></span>
4. <span data-ttu-id="0bf00-135">In Disqualifying Entities, enter $city.</span><span class="sxs-lookup"><span data-stu-id="0bf00-135">In Disqualifying Entities, enter $city.</span></span>
4. <span data-ttu-id="0bf00-136">Click Create</span><span class="sxs-lookup"><span data-stu-id="0bf00-136">Click Create</span></span>

<span data-ttu-id="0bf00-137">You now have three actions.</span><span class="sxs-lookup"><span data-stu-id="0bf00-137">You now have three actions.</span></span>

### <a name="train-the-bot"></a><span data-ttu-id="0bf00-138">Train the bot</span><span class="sxs-lookup"><span data-stu-id="0bf00-138">Train the bot</span></span>

1. <span data-ttu-id="0bf00-139">Click Train Dialogs, then New Train Dialog.</span><span class="sxs-lookup"><span data-stu-id="0bf00-139">Click Train Dialogs, then New Train Dialog.</span></span>
2. <span data-ttu-id="0bf00-140">Type 'what's the weather'.</span><span class="sxs-lookup"><span data-stu-id="0bf00-140">Type 'what's the weather'.</span></span>
3. <span data-ttu-id="0bf00-141">Click Score Actions, and Select 'Which city do you want?'</span><span class="sxs-lookup"><span data-stu-id="0bf00-141">Click Score Actions, and Select 'Which city do you want?'</span></span>
2. <span data-ttu-id="0bf00-142">Enter 'denver'.</span><span class="sxs-lookup"><span data-stu-id="0bf00-142">Enter 'denver'.</span></span>
3. <span data-ttu-id="0bf00-143">Double-click on 'denver', and select city.</span><span class="sxs-lookup"><span data-stu-id="0bf00-143">Double-click on 'denver', and select city.</span></span>
    - <span data-ttu-id="0bf00-144">This marks it as a city entity.</span><span class="sxs-lookup"><span data-stu-id="0bf00-144">This marks it as a city entity.</span></span>
5. <span data-ttu-id="0bf00-145">Click Score Actions</span><span class="sxs-lookup"><span data-stu-id="0bf00-145">Click Score Actions</span></span>
    - <span data-ttu-id="0bf00-146">'denver' is now present in the city entity.</span><span class="sxs-lookup"><span data-stu-id="0bf00-146">'denver' is now present in the city entity.</span></span> 
6. <span data-ttu-id="0bf00-147">Select 'The weather in $city is probably sunny'.</span><span class="sxs-lookup"><span data-stu-id="0bf00-147">Select 'The weather in $city is probably sunny'.</span></span>
7. <span data-ttu-id="0bf00-148">Click Done Teaching.</span><span class="sxs-lookup"><span data-stu-id="0bf00-148">Click Done Teaching.</span></span>

<span data-ttu-id="0bf00-149">Add another example dialog:</span><span class="sxs-lookup"><span data-stu-id="0bf00-149">Add another example dialog:</span></span>

1. <span data-ttu-id="0bf00-150">Click New Action, then New Train Dialog.</span><span class="sxs-lookup"><span data-stu-id="0bf00-150">Click New Action, then New Train Dialog.</span></span>
2. <span data-ttu-id="0bf00-151">Type 'what can you do?'.</span><span class="sxs-lookup"><span data-stu-id="0bf00-151">Type 'what can you do?'.</span></span>
3. <span data-ttu-id="0bf00-152">Click Score Actions, and Select 'Try asking for the weather'</span><span class="sxs-lookup"><span data-stu-id="0bf00-152">Click Score Actions, and Select 'Try asking for the weather'</span></span>
2. <span data-ttu-id="0bf00-153">Enter 'What's the weather in seattle'.</span><span class="sxs-lookup"><span data-stu-id="0bf00-153">Enter 'What's the weather in seattle'.</span></span>
3. <span data-ttu-id="0bf00-154">Double-click on 'seattle', and select city.</span><span class="sxs-lookup"><span data-stu-id="0bf00-154">Double-click on 'seattle', and select city.</span></span>
    - <span data-ttu-id="0bf00-155">This marks it as a city entity.</span><span class="sxs-lookup"><span data-stu-id="0bf00-155">This marks it as a city entity.</span></span>
5. <span data-ttu-id="0bf00-156">Click Score Actions</span><span class="sxs-lookup"><span data-stu-id="0bf00-156">Click Score Actions</span></span>
    - <span data-ttu-id="0bf00-157">'seattle' is now present in the city entity.</span><span class="sxs-lookup"><span data-stu-id="0bf00-157">'seattle' is now present in the city entity.</span></span> 
6. <span data-ttu-id="0bf00-158">Select 'The weather in $city is probably sunny'.</span><span class="sxs-lookup"><span data-stu-id="0bf00-158">Select 'The weather in $city is probably sunny'.</span></span>
7. <span data-ttu-id="0bf00-159">Click Done Teaching.</span><span class="sxs-lookup"><span data-stu-id="0bf00-159">Click Done Teaching.</span></span>

<span data-ttu-id="0bf00-160">Let's see what happens if the user says something semantically similar to the above:</span><span class="sxs-lookup"><span data-stu-id="0bf00-160">Let's see what happens if the user says something semantically similar to the above:</span></span>

1. <span data-ttu-id="0bf00-161">Click New Action, then New Train Dialog.</span><span class="sxs-lookup"><span data-stu-id="0bf00-161">Click New Action, then New Train Dialog.</span></span>
2. <span data-ttu-id="0bf00-162">Type 'help'.</span><span class="sxs-lookup"><span data-stu-id="0bf00-162">Type 'help'.</span></span>
3. <span data-ttu-id="0bf00-163">Click Score Actions.</span><span class="sxs-lookup"><span data-stu-id="0bf00-163">Click Score Actions.</span></span>
    - <span data-ttu-id="0bf00-164">The scores for the two potential responses are very close.</span><span class="sxs-lookup"><span data-stu-id="0bf00-164">The scores for the two potential responses are very close.</span></span> <span data-ttu-id="0bf00-165">This tells us the model is confused about the boundary between the two actions.</span><span class="sxs-lookup"><span data-stu-id="0bf00-165">This tells us the model is confused about the boundary between the two actions.</span></span>
6. <span data-ttu-id="0bf00-166">Click Abandon Teaching and Confirm.</span><span class="sxs-lookup"><span data-stu-id="0bf00-166">Click Abandon Teaching and Confirm.</span></span>

![](../media/tutorial8_closescores.png)

<span data-ttu-id="0bf00-167">In this case, it would help to add alternative inputs to dialogs.</span><span class="sxs-lookup"><span data-stu-id="0bf00-167">In this case, it would help to add alternative inputs to dialogs.</span></span> <span data-ttu-id="0bf00-168">You can add them as you are doing the teaching.</span><span class="sxs-lookup"><span data-stu-id="0bf00-168">You can add them as you are doing the teaching.</span></span> <span data-ttu-id="0bf00-169">You can also go back and add them later.</span><span class="sxs-lookup"><span data-stu-id="0bf00-169">You can also go back and add them later.</span></span>

2. <span data-ttu-id="0bf00-170">Click on 'What can you do?'</span><span class="sxs-lookup"><span data-stu-id="0bf00-170">Click on 'What can you do?'</span></span> <span data-ttu-id="0bf00-171">in Train Dialogs.</span><span class="sxs-lookup"><span data-stu-id="0bf00-171">in Train Dialogs.</span></span>
2. <span data-ttu-id="0bf00-172">In the dialog, click on 'what can you do?'</span><span class="sxs-lookup"><span data-stu-id="0bf00-172">In the dialog, click on 'what can you do?'</span></span> <span data-ttu-id="0bf00-173">to select it.</span><span class="sxs-lookup"><span data-stu-id="0bf00-173">to select it.</span></span>
    1. <span data-ttu-id="0bf00-174">In the right pane, under Entity Detection, in the Add alternative input enter a couple of alternatives:</span><span class="sxs-lookup"><span data-stu-id="0bf00-174">In the right pane, under Entity Detection, in the Add alternative input enter a couple of alternatives:</span></span>
    1. <span data-ttu-id="0bf00-175">Enter 'what are my choices?'</span><span class="sxs-lookup"><span data-stu-id="0bf00-175">Enter 'what are my choices?'</span></span>
    2. <span data-ttu-id="0bf00-176">Enter 'Tell me my choices'.</span><span class="sxs-lookup"><span data-stu-id="0bf00-176">Enter 'Tell me my choices'.</span></span>
    3. <span data-ttu-id="0bf00-177">Enter 'help'</span><span class="sxs-lookup"><span data-stu-id="0bf00-177">Enter 'help'</span></span>
    1. <span data-ttu-id="0bf00-178">click Submit Changes.</span><span class="sxs-lookup"><span data-stu-id="0bf00-178">click Submit Changes.</span></span>


![](../media/tutorial8_helpalternates.png)

2. <span data-ttu-id="0bf00-179">Now click on 'what's the weather in seattle'.</span><span class="sxs-lookup"><span data-stu-id="0bf00-179">Now click on 'what's the weather in seattle'.</span></span>
    1. <span data-ttu-id="0bf00-180">In Add alternative input, enter 'forecast for seattle'.</span><span class="sxs-lookup"><span data-stu-id="0bf00-180">In Add alternative input, enter 'forecast for seattle'.</span></span>
    2. <span data-ttu-id="0bf00-181">Double-click on 'seattle', and select city.</span><span class="sxs-lookup"><span data-stu-id="0bf00-181">Double-click on 'seattle', and select city.</span></span> <span data-ttu-id="0bf00-182">The entities for alternative inputs should be present and have the same set of entities.</span><span class="sxs-lookup"><span data-stu-id="0bf00-182">The entities for alternative inputs should be present and have the same set of entities.</span></span> <span data-ttu-id="0bf00-183">It is fine if the content of the entities is different.</span><span class="sxs-lookup"><span data-stu-id="0bf00-183">It is fine if the content of the entities is different.</span></span>
    3. <span data-ttu-id="0bf00-184">In Add alternative input, enter 'will it rain today in denver'.</span><span class="sxs-lookup"><span data-stu-id="0bf00-184">In Add alternative input, enter 'will it rain today in denver'.</span></span>
    4. <span data-ttu-id="0bf00-185">Click on 'denver', and select city.</span><span class="sxs-lookup"><span data-stu-id="0bf00-185">Click on 'denver', and select city.</span></span>
    5. <span data-ttu-id="0bf00-186">click Submit Changes and Done.</span><span class="sxs-lookup"><span data-stu-id="0bf00-186">click Submit Changes and Done.</span></span>


<span data-ttu-id="0bf00-187">Let's add alternate inputs to the first dialog:</span><span class="sxs-lookup"><span data-stu-id="0bf00-187">Let's add alternate inputs to the first dialog:</span></span>

1. <span data-ttu-id="0bf00-188">Click Train Dialogs.</span><span class="sxs-lookup"><span data-stu-id="0bf00-188">Click Train Dialogs.</span></span>
2. <span data-ttu-id="0bf00-189">Click on the dialog starting with 'what's the weather'.</span><span class="sxs-lookup"><span data-stu-id="0bf00-189">Click on the dialog starting with 'what's the weather'.</span></span>
2. <span data-ttu-id="0bf00-190">Click to select 'what's the weather' in the left pane:</span><span class="sxs-lookup"><span data-stu-id="0bf00-190">Click to select 'what's the weather' in the left pane:</span></span>
    1. <span data-ttu-id="0bf00-191">In Add alternative input, enter 'weather forecast'.</span><span class="sxs-lookup"><span data-stu-id="0bf00-191">In Add alternative input, enter 'weather forecast'.</span></span>
    2. <span data-ttu-id="0bf00-192">Enter 'will it rain?'</span><span class="sxs-lookup"><span data-stu-id="0bf00-192">Enter 'will it rain?'</span></span>
    3. <span data-ttu-id="0bf00-193">Click Submit Changes.</span><span class="sxs-lookup"><span data-stu-id="0bf00-193">Click Submit Changes.</span></span>
4. <span data-ttu-id="0bf00-194">Click to select 'denver' in the left pane:</span><span class="sxs-lookup"><span data-stu-id="0bf00-194">Click to select 'denver' in the left pane:</span></span>
    1. <span data-ttu-id="0bf00-195">In Add alternative input, enter 'for denver'.</span><span class="sxs-lookup"><span data-stu-id="0bf00-195">In Add alternative input, enter 'for denver'.</span></span>
    2. <span data-ttu-id="0bf00-196">Enter 'forecast for austin'.</span><span class="sxs-lookup"><span data-stu-id="0bf00-196">Enter 'forecast for austin'.</span></span>
        - <span data-ttu-id="0bf00-197">The full phrase is highlighted.</span><span class="sxs-lookup"><span data-stu-id="0bf00-197">The full phrase is highlighted.</span></span> <span data-ttu-id="0bf00-198">Click on the phrase, then red x.</span><span class="sxs-lookup"><span data-stu-id="0bf00-198">Click on the phrase, then red x.</span></span> <span data-ttu-id="0bf00-199">Then select austin, and click on city.</span><span class="sxs-lookup"><span data-stu-id="0bf00-199">Then select austin, and click on city.</span></span>
        - <span data-ttu-id="0bf00-200">Click Submit Changes</span><span class="sxs-lookup"><span data-stu-id="0bf00-200">Click Submit Changes</span></span>
    1. <span data-ttu-id="0bf00-201">Click Done which will cause the model to retrain.</span><span class="sxs-lookup"><span data-stu-id="0bf00-201">Click Done which will cause the model to retrain.</span></span>

![](../media/tutorial8_altcities.png)

<span data-ttu-id="0bf00-202">Let's try the variations:</span><span class="sxs-lookup"><span data-stu-id="0bf00-202">Let's try the variations:</span></span>

1. <span data-ttu-id="0bf00-203">Click New Train Dialog.</span><span class="sxs-lookup"><span data-stu-id="0bf00-203">Click New Train Dialog.</span></span>
2. <span data-ttu-id="0bf00-204">Type 'what are you capabilities'.</span><span class="sxs-lookup"><span data-stu-id="0bf00-204">Type 'what are you capabilities'.</span></span>
3. <span data-ttu-id="0bf00-205">Click Score Actions.</span><span class="sxs-lookup"><span data-stu-id="0bf00-205">Click Score Actions.</span></span>
    - <span data-ttu-id="0bf00-206">The scores are now more decisive on the next action which indicates the certainty of the model.</span><span class="sxs-lookup"><span data-stu-id="0bf00-206">The scores are now more decisive on the next action which indicates the certainty of the model.</span></span>
2. <span data-ttu-id="0bf00-207">Select 'Try asking for weather'.</span><span class="sxs-lookup"><span data-stu-id="0bf00-207">Select 'Try asking for weather'.</span></span>
6. <span data-ttu-id="0bf00-208">Click Done Teaching</span><span class="sxs-lookup"><span data-stu-id="0bf00-208">Click Done Teaching</span></span>

<span data-ttu-id="0bf00-209">You have now seen how alternative inputs can be used to indicate other things the user might have said.</span><span class="sxs-lookup"><span data-stu-id="0bf00-209">You have now seen how alternative inputs can be used to indicate other things the user might have said.</span></span> <span data-ttu-id="0bf00-210">They help you avoid creating many dialogs, which in many ways are the same, by collapsing them into a single dialog and enumerating what the user can say.</span><span class="sxs-lookup"><span data-stu-id="0bf00-210">They help you avoid creating many dialogs, which in many ways are the same, by collapsing them into a single dialog and enumerating what the user can say.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0bf00-211">Next steps</span><span class="sxs-lookup"><span data-stu-id="0bf00-211">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0bf00-212">Log dialogs</span><span class="sxs-lookup"><span data-stu-id="0bf00-212">Log dialogs</span></span>](./9-log-dialogs.md)
