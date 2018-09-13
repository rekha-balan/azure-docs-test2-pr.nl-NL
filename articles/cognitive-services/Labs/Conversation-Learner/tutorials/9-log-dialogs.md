---
title: How to log dialogs in a Conversation Learner model - Microsoft Cognitive Services | Microsoft Docs
titleSuffix: Azure
description: Learn how to log dialogs in a Conversation Learner model.
services: cognitive-services
author: v-jaswel
manager: nolachar
ms.service: cognitive-services
ms.component: conversation-learner
ms.topic: article
ms.date: 04/30/2018
ms.author: v-jaswel
ms.openlocfilehash: 6ceeb9683a979256a8a52347fc74ab758fd1d348
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857112"
---
# <a name="how-to-log-dialogs-in-a-conversation-learner-model"></a><span data-ttu-id="22639-103">How to log dialogs in a Conversation Learner model</span><span class="sxs-lookup"><span data-stu-id="22639-103">How to log dialogs in a Conversation Learner model</span></span>

<span data-ttu-id="22639-104">This tutorial shows how to do end-user testing within the Conversation Learner interface; how dialogs are logged; and how to make corrections to logged dialogs in order to improve your model.</span><span class="sxs-lookup"><span data-stu-id="22639-104">This tutorial shows how to do end-user testing within the Conversation Learner interface; how dialogs are logged; and how to make corrections to logged dialogs in order to improve your model.</span></span>

## <a name="video"></a><span data-ttu-id="22639-105">Video</span><span class="sxs-lookup"><span data-stu-id="22639-105">Video</span></span>

<span data-ttu-id="22639-106">[![Tutorial 9 Preview](http://aka.ms/cl-tutorial-09-preview)](http://aka.ms/blis-tutorial-09)</span><span class="sxs-lookup"><span data-stu-id="22639-106">[![Tutorial 9 Preview](http://aka.ms/cl-tutorial-09-preview)](http://aka.ms/blis-tutorial-09)</span></span>

## <a name="requirements"></a><span data-ttu-id="22639-107">Requirements</span><span class="sxs-lookup"><span data-stu-id="22639-107">Requirements</span></span>
<span data-ttu-id="22639-108">This tutorial requires that the general tutorial bot is running</span><span class="sxs-lookup"><span data-stu-id="22639-108">This tutorial requires that the general tutorial bot is running</span></span>

    npm run tutorial-general

## <a name="details"></a><span data-ttu-id="22639-109">Details</span><span class="sxs-lookup"><span data-stu-id="22639-109">Details</span></span>
<span data-ttu-id="22639-110">You can use the log dialogs to review and make corrections to dialogs conducted with end users.</span><span class="sxs-lookup"><span data-stu-id="22639-110">You can use the log dialogs to review and make corrections to dialogs conducted with end users.</span></span>  <span data-ttu-id="22639-111">Specifically, you can fix entity labels and action selections to improve the performance of the trained model and overall system.</span><span class="sxs-lookup"><span data-stu-id="22639-111">Specifically, you can fix entity labels and action selections to improve the performance of the trained model and overall system.</span></span> 

## <a name="steps"></a><span data-ttu-id="22639-112">Steps</span><span class="sxs-lookup"><span data-stu-id="22639-112">Steps</span></span>

### <a name="create-the-model"></a><span data-ttu-id="22639-113">Create the model</span><span class="sxs-lookup"><span data-stu-id="22639-113">Create the model</span></span>

1. <span data-ttu-id="22639-114">In the Web UI, click New Model</span><span class="sxs-lookup"><span data-stu-id="22639-114">In the Web UI, click New Model</span></span>
2. <span data-ttu-id="22639-115">In Name, enter LogDialogs.</span><span class="sxs-lookup"><span data-stu-id="22639-115">In Name, enter LogDialogs.</span></span> <span data-ttu-id="22639-116">Then click Create.</span><span class="sxs-lookup"><span data-stu-id="22639-116">Then click Create.</span></span>

### <a name="create-an-entity"></a><span data-ttu-id="22639-117">Create an entity</span><span class="sxs-lookup"><span data-stu-id="22639-117">Create an entity</span></span>

1. <span data-ttu-id="22639-118">Click Entities, then New Entity.</span><span class="sxs-lookup"><span data-stu-id="22639-118">Click Entities, then New Entity.</span></span>
2. <span data-ttu-id="22639-119">In Entity Name, enter city.</span><span class="sxs-lookup"><span data-stu-id="22639-119">In Entity Name, enter city.</span></span>
3. <span data-ttu-id="22639-120">Click Create.</span><span class="sxs-lookup"><span data-stu-id="22639-120">Click Create.</span></span>

### <a name="create-two-actions"></a><span data-ttu-id="22639-121">Create two actions</span><span class="sxs-lookup"><span data-stu-id="22639-121">Create two actions</span></span>

1. <span data-ttu-id="22639-122">Click Actions, then New Action</span><span class="sxs-lookup"><span data-stu-id="22639-122">Click Actions, then New Action</span></span>
2. <span data-ttu-id="22639-123">In Response, type 'Which city?'.</span><span class="sxs-lookup"><span data-stu-id="22639-123">In Response, type 'Which city?'.</span></span>
3. <span data-ttu-id="22639-124">In Disqualifying Entities, enter $city.</span><span class="sxs-lookup"><span data-stu-id="22639-124">In Disqualifying Entities, enter $city.</span></span>
3. <span data-ttu-id="22639-125">Click Create</span><span class="sxs-lookup"><span data-stu-id="22639-125">Click Create</span></span>

<span data-ttu-id="22639-126">Then create the second action:</span><span class="sxs-lookup"><span data-stu-id="22639-126">Then create the second action:</span></span>

1. <span data-ttu-id="22639-127">Click Actions, then New Action.</span><span class="sxs-lookup"><span data-stu-id="22639-127">Click Actions, then New Action.</span></span>
3. <span data-ttu-id="22639-128">In Response, type 'The weather in $city is probably sunny'.</span><span class="sxs-lookup"><span data-stu-id="22639-128">In Response, type 'The weather in $city is probably sunny'.</span></span>
4. <span data-ttu-id="22639-129">Required Entities, enter $city.</span><span class="sxs-lookup"><span data-stu-id="22639-129">Required Entities, enter $city.</span></span>
4. <span data-ttu-id="22639-130">Click Create.</span><span class="sxs-lookup"><span data-stu-id="22639-130">Click Create.</span></span>

<span data-ttu-id="22639-131">You now have two actions.</span><span class="sxs-lookup"><span data-stu-id="22639-131">You now have two actions.</span></span>

### <a name="train-the-bot"></a><span data-ttu-id="22639-132">Train the bot</span><span class="sxs-lookup"><span data-stu-id="22639-132">Train the bot</span></span>

1. <span data-ttu-id="22639-133">Click Train Dialogs, then New Train Dialog.</span><span class="sxs-lookup"><span data-stu-id="22639-133">Click Train Dialogs, then New Train Dialog.</span></span>
2. <span data-ttu-id="22639-134">Type 'what's the weather'.</span><span class="sxs-lookup"><span data-stu-id="22639-134">Type 'what's the weather'.</span></span>
3. <span data-ttu-id="22639-135">Click Score Actions, and Select 'Which city?'</span><span class="sxs-lookup"><span data-stu-id="22639-135">Click Score Actions, and Select 'Which city?'</span></span>
2. <span data-ttu-id="22639-136">Enter 'Seattle'.</span><span class="sxs-lookup"><span data-stu-id="22639-136">Enter 'Seattle'.</span></span>
3. <span data-ttu-id="22639-137">Double-click on 'Seattle', and select city.</span><span class="sxs-lookup"><span data-stu-id="22639-137">Double-click on 'Seattle', and select city.</span></span>
    - <span data-ttu-id="22639-138">This marks it as a city entity.</span><span class="sxs-lookup"><span data-stu-id="22639-138">This marks it as a city entity.</span></span>
5. <span data-ttu-id="22639-139">Click Score Actions</span><span class="sxs-lookup"><span data-stu-id="22639-139">Click Score Actions</span></span>
6. <span data-ttu-id="22639-140">Select 'The weather in $city is probably sunny'.</span><span class="sxs-lookup"><span data-stu-id="22639-140">Select 'The weather in $city is probably sunny'.</span></span>
7. <span data-ttu-id="22639-141">Click Done Teaching.</span><span class="sxs-lookup"><span data-stu-id="22639-141">Click Done Teaching.</span></span>

<span data-ttu-id="22639-142">Add another example dialog:</span><span class="sxs-lookup"><span data-stu-id="22639-142">Add another example dialog:</span></span>

1. <span data-ttu-id="22639-143">Click New Action, then New Train Dialog.</span><span class="sxs-lookup"><span data-stu-id="22639-143">Click New Action, then New Train Dialog.</span></span>
2. <span data-ttu-id="22639-144">Type 'what's the weather in Seattle?'.</span><span class="sxs-lookup"><span data-stu-id="22639-144">Type 'what's the weather in Seattle?'.</span></span> <span data-ttu-id="22639-145">Notice Seattle is tagged as an entity.</span><span class="sxs-lookup"><span data-stu-id="22639-145">Notice Seattle is tagged as an entity.</span></span>
5. <span data-ttu-id="22639-146">Click Score Actions</span><span class="sxs-lookup"><span data-stu-id="22639-146">Click Score Actions</span></span> 
6. <span data-ttu-id="22639-147">Select 'The weather in $city is probably sunny'.</span><span class="sxs-lookup"><span data-stu-id="22639-147">Select 'The weather in $city is probably sunny'.</span></span>
7. <span data-ttu-id="22639-148">Click Done Teaching.</span><span class="sxs-lookup"><span data-stu-id="22639-148">Click Done Teaching.</span></span>

### <a name="try-the-bot-as-the-user"></a><span data-ttu-id="22639-149">Try the bot as the user</span><span class="sxs-lookup"><span data-stu-id="22639-149">Try the bot as the user</span></span>
<span data-ttu-id="22639-150">Let's imagine that we have deployed this bot to users.</span><span class="sxs-lookup"><span data-stu-id="22639-150">Let's imagine that we have deployed this bot to users.</span></span>

1. <span data-ttu-id="22639-151">Click on Log Dialogs.</span><span class="sxs-lookup"><span data-stu-id="22639-151">Click on Log Dialogs.</span></span>
2. <span data-ttu-id="22639-152">Click New Chat Session.</span><span class="sxs-lookup"><span data-stu-id="22639-152">Click New Chat Session.</span></span>
    - <span data-ttu-id="22639-153">This presents the bot as the user would experience it in the web chat control on the left of the UI.</span><span class="sxs-lookup"><span data-stu-id="22639-153">This presents the bot as the user would experience it in the web chat control on the left of the UI.</span></span> <span data-ttu-id="22639-154">You can ignore the white-space area on the right.</span><span class="sxs-lookup"><span data-stu-id="22639-154">You can ignore the white-space area on the right.</span></span>
3. <span data-ttu-id="22639-155">Type 'hello'.</span><span class="sxs-lookup"><span data-stu-id="22639-155">Type 'hello'.</span></span>
4. <span data-ttu-id="22639-156">Bot response: 'which city?'</span><span class="sxs-lookup"><span data-stu-id="22639-156">Bot response: 'which city?'</span></span>
4. <span data-ttu-id="22639-157">Type 'Boston'.</span><span class="sxs-lookup"><span data-stu-id="22639-157">Type 'Boston'.</span></span>
5. <span data-ttu-id="22639-158">Bot response: 'which city?'</span><span class="sxs-lookup"><span data-stu-id="22639-158">Bot response: 'which city?'</span></span>
    - <span data-ttu-id="22639-159">This doesn't seem right.</span><span class="sxs-lookup"><span data-stu-id="22639-159">This doesn't seem right.</span></span> <span data-ttu-id="22639-160">So let's save this dialog.</span><span class="sxs-lookup"><span data-stu-id="22639-160">So let's save this dialog.</span></span>
2. <span data-ttu-id="22639-161">Click Done Testing.</span><span class="sxs-lookup"><span data-stu-id="22639-161">Click Done Testing.</span></span>

<span data-ttu-id="22639-162">Let's start a new session:</span><span class="sxs-lookup"><span data-stu-id="22639-162">Let's start a new session:</span></span>

2. <span data-ttu-id="22639-163">Click New Chat Session.</span><span class="sxs-lookup"><span data-stu-id="22639-163">Click New Chat Session.</span></span>
3. <span data-ttu-id="22639-164">Type 'forecast for Boston'.</span><span class="sxs-lookup"><span data-stu-id="22639-164">Type 'forecast for Boston'.</span></span>
4. <span data-ttu-id="22639-165">Bot response: 'which city?'</span><span class="sxs-lookup"><span data-stu-id="22639-165">Bot response: 'which city?'</span></span>
2. <span data-ttu-id="22639-166">Click Done Teaching.</span><span class="sxs-lookup"><span data-stu-id="22639-166">Click Done Teaching.</span></span>

<span data-ttu-id="22639-167">Now let's make corrections to the second dialog:</span><span class="sxs-lookup"><span data-stu-id="22639-167">Now let's make corrections to the second dialog:</span></span>

1. <span data-ttu-id="22639-168">Click on 'forecast for Boston' under Log Dialogs.</span><span class="sxs-lookup"><span data-stu-id="22639-168">Click on 'forecast for Boston' under Log Dialogs.</span></span>
    - <span data-ttu-id="22639-169">This opens the conversation.</span><span class="sxs-lookup"><span data-stu-id="22639-169">This opens the conversation.</span></span>
    - <span data-ttu-id="22639-170">If you click on the user side of the conversation (here on 'forecast for Boston'), you can change entity labels.</span><span class="sxs-lookup"><span data-stu-id="22639-170">If you click on the user side of the conversation (here on 'forecast for Boston'), you can change entity labels.</span></span>
    - <span data-ttu-id="22639-171">If you click on the system side (here on 'which city'), you can change which action is selected.</span><span class="sxs-lookup"><span data-stu-id="22639-171">If you click on the system side (here on 'which city'), you can change which action is selected.</span></span>
5. <span data-ttu-id="22639-172">Click on 'forecast for Boston'.</span><span class="sxs-lookup"><span data-stu-id="22639-172">Click on 'forecast for Boston'.</span></span> 
    - <span data-ttu-id="22639-173">The root cause here is that Boston was not tagged as an entity.</span><span class="sxs-lookup"><span data-stu-id="22639-173">The root cause here is that Boston was not tagged as an entity.</span></span> <span data-ttu-id="22639-174">We need to change that.</span><span class="sxs-lookup"><span data-stu-id="22639-174">We need to change that.</span></span>
    - <span data-ttu-id="22639-175">Double-click on 'Boston', then select city.</span><span class="sxs-lookup"><span data-stu-id="22639-175">Double-click on 'Boston', then select city.</span></span>
    - <span data-ttu-id="22639-176">Click Submit Changes, and click Save.</span><span class="sxs-lookup"><span data-stu-id="22639-176">Click Submit Changes, and click Save.</span></span> <span data-ttu-id="22639-177">This will create a training dialog based on the changes you made, and drop you into training dialogs at the point of the change you made.</span><span class="sxs-lookup"><span data-stu-id="22639-177">This will create a training dialog based on the changes you made, and drop you into training dialogs at the point of the change you made.</span></span>
6. <span data-ttu-id="22639-178">Select 'The weather in $city is probably sunny.'</span><span class="sxs-lookup"><span data-stu-id="22639-178">Select 'The weather in $city is probably sunny.'</span></span>
7. <span data-ttu-id="22639-179">Click Done Teaching.</span><span class="sxs-lookup"><span data-stu-id="22639-179">Click Done Teaching.</span></span> <span data-ttu-id="22639-180">If you go to Train Dialogs now, you will see the new action is added.</span><span class="sxs-lookup"><span data-stu-id="22639-180">If you go to Train Dialogs now, you will see the new action is added.</span></span>

![](../media/tutorial9_logdiag1.PNG)

<span data-ttu-id="22639-181">Now let's make corrections to the other dialog:</span><span class="sxs-lookup"><span data-stu-id="22639-181">Now let's make corrections to the other dialog:</span></span>

1. <span data-ttu-id="22639-182">Click on 'hello' under Log Dialogs.</span><span class="sxs-lookup"><span data-stu-id="22639-182">Click on 'hello' under Log Dialogs.</span></span>
    - <span data-ttu-id="22639-183">This opens the conversation.</span><span class="sxs-lookup"><span data-stu-id="22639-183">This opens the conversation.</span></span>
3. <span data-ttu-id="22639-184">The response to 'hello' is 'which city'.</span><span class="sxs-lookup"><span data-stu-id="22639-184">The response to 'hello' is 'which city'.</span></span> <span data-ttu-id="22639-185">But we want to change that to something that makes more sense.</span><span class="sxs-lookup"><span data-stu-id="22639-185">But we want to change that to something that makes more sense.</span></span> <span data-ttu-id="22639-186">A better answer would be something like 'hello, I'm the weather bot'.</span><span class="sxs-lookup"><span data-stu-id="22639-186">A better answer would be something like 'hello, I'm the weather bot'.</span></span> <span data-ttu-id="22639-187">But there is no action that does that so we have to create one.</span><span class="sxs-lookup"><span data-stu-id="22639-187">But there is no action that does that so we have to create one.</span></span>
4. <span data-ttu-id="22639-188">Click on Action.</span><span class="sxs-lookup"><span data-stu-id="22639-188">Click on Action.</span></span>
    - <span data-ttu-id="22639-189">In the Response, type 'I'm the weather bot.</span><span class="sxs-lookup"><span data-stu-id="22639-189">In the Response, type 'I'm the weather bot.</span></span> <span data-ttu-id="22639-190">I can help with forecasts.'</span><span class="sxs-lookup"><span data-stu-id="22639-190">I can help with forecasts.'</span></span>
6. <span data-ttu-id="22639-191">Un-check the Wait for Response check-box to make it a non-wait action.</span><span class="sxs-lookup"><span data-stu-id="22639-191">Un-check the Wait for Response check-box to make it a non-wait action.</span></span>
7. <span data-ttu-id="22639-192">Click Create.</span><span class="sxs-lookup"><span data-stu-id="22639-192">Click Create.</span></span>
8. <span data-ttu-id="22639-193">Then click to Select this new action.</span><span class="sxs-lookup"><span data-stu-id="22639-193">Then click to Select this new action.</span></span> <span data-ttu-id="22639-194">Then click Save.</span><span class="sxs-lookup"><span data-stu-id="22639-194">Then click Save.</span></span>
    - <span data-ttu-id="22639-195">This brings you back to that point in the training session.</span><span class="sxs-lookup"><span data-stu-id="22639-195">This brings you back to that point in the training session.</span></span>
6. <span data-ttu-id="22639-196">Click to Select 'which city?'</span><span class="sxs-lookup"><span data-stu-id="22639-196">Click to Select 'which city?'</span></span>
7. <span data-ttu-id="22639-197">Type in 'Boston'.</span><span class="sxs-lookup"><span data-stu-id="22639-197">Type in 'Boston'.</span></span> <span data-ttu-id="22639-198">Double-click to tag Boston as an entity if not already.</span><span class="sxs-lookup"><span data-stu-id="22639-198">Double-click to tag Boston as an entity if not already.</span></span>
8. <span data-ttu-id="22639-199">Click Score Actions.</span><span class="sxs-lookup"><span data-stu-id="22639-199">Click Score Actions.</span></span>
9. <span data-ttu-id="22639-200">Click to Select 'The weather in $city is probably sunny.'</span><span class="sxs-lookup"><span data-stu-id="22639-200">Click to Select 'The weather in $city is probably sunny.'</span></span>
10. <span data-ttu-id="22639-201">Click Done Teaching.</span><span class="sxs-lookup"><span data-stu-id="22639-201">Click Done Teaching.</span></span>

![](../media/tutorial9_addnewaction.PNG)

## <a name="next-steps"></a><span data-ttu-id="22639-202">Next steps</span><span class="sxs-lookup"><span data-stu-id="22639-202">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="22639-203">Entity detection callback</span><span class="sxs-lookup"><span data-stu-id="22639-203">Entity detection callback</span></span>](./10-entity-detection-callback.md)
