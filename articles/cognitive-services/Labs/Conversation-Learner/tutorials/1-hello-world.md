---
title: How to create a "Hello World" Conversation Learner model - Microsoft Cognitive Services | Microsoft Docs
titleSuffix: Azure
description: Learn how to create a "Hello World" Conversation Learner model.
services: cognitive-services
author: v-jaswel
manager: nolachar
ms.service: cognitive-services
ms.component: conversation-learner
ms.topic: article
ms.date: 04/30/2018
ms.author: v-jaswel
ms.openlocfilehash: 70b8f25bd699cbdb069892d65bf766ef3953f59d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969126"
---
# <a name="how-to-create-a-hello-world-model-with-conversation-learner"></a><span data-ttu-id="76d87-103">How to create a "Hello World" model with Conversation Learner</span><span class="sxs-lookup"><span data-stu-id="76d87-103">How to create a "Hello World" model with Conversation Learner</span></span>

<span data-ttu-id="76d87-104">This tutorial shows how to get started with Conversation Learner, including creating actions, teaching interactively, and making corrections of logged dialogs from end users.</span><span class="sxs-lookup"><span data-stu-id="76d87-104">This tutorial shows how to get started with Conversation Learner, including creating actions, teaching interactively, and making corrections of logged dialogs from end users.</span></span>

## <a name="video"></a><span data-ttu-id="76d87-105">Video</span><span class="sxs-lookup"><span data-stu-id="76d87-105">Video</span></span>

<span data-ttu-id="76d87-106">[![Tutorial 1 Preview](http://aka.ms/cl-tutorial-01-preview)](http://aka.ms/blis-tutorial-01)</span><span class="sxs-lookup"><span data-stu-id="76d87-106">[![Tutorial 1 Preview](http://aka.ms/cl-tutorial-01-preview)](http://aka.ms/blis-tutorial-01)</span></span>


## <a name="requirements"></a><span data-ttu-id="76d87-107">Requirements</span><span class="sxs-lookup"><span data-stu-id="76d87-107">Requirements</span></span>
<span data-ttu-id="76d87-108">If you haven't already, first ensure all setup steps have been completed, including creating a `.env` file with your LUIS authoring key.</span><span class="sxs-lookup"><span data-stu-id="76d87-108">If you haven't already, first ensure all setup steps have been completed, including creating a `.env` file with your LUIS authoring key.</span></span>  <span data-ttu-id="76d87-109">See [Quickstart](https://github.com/Microsoft/ConversationLearner-Samples) for details.</span><span class="sxs-lookup"><span data-stu-id="76d87-109">See [Quickstart](https://github.com/Microsoft/ConversationLearner-Samples) for details.</span></span>

<span data-ttu-id="76d87-110">This tutorial requires that the general tutorial bot is running</span><span class="sxs-lookup"><span data-stu-id="76d87-110">This tutorial requires that the general tutorial bot is running</span></span>

    npm run tutorial-general

## <a name="steps"></a><span data-ttu-id="76d87-111">Steps</span><span class="sxs-lookup"><span data-stu-id="76d87-111">Steps</span></span>

<span data-ttu-id="76d87-112">Start on the home page in the Web UI.</span><span class="sxs-lookup"><span data-stu-id="76d87-112">Start on the home page in the Web UI.</span></span>

### <a name="create-the-model"></a><span data-ttu-id="76d87-113">Create the model</span><span class="sxs-lookup"><span data-stu-id="76d87-113">Create the model</span></span>
1. <span data-ttu-id="76d87-114">Click New Model</span><span class="sxs-lookup"><span data-stu-id="76d87-114">Click New Model</span></span>
2. <span data-ttu-id="76d87-115">In the Name field, enter Hello World</span><span class="sxs-lookup"><span data-stu-id="76d87-115">In the Name field, enter Hello World</span></span>
3. <span data-ttu-id="76d87-116">Click Create</span><span class="sxs-lookup"><span data-stu-id="76d87-116">Click Create</span></span>

### <a name="create-an-action"></a><span data-ttu-id="76d87-117">Create an Action</span><span class="sxs-lookup"><span data-stu-id="76d87-117">Create an Action</span></span>

1. <span data-ttu-id="76d87-118">Click on the Hello World model to start it</span><span class="sxs-lookup"><span data-stu-id="76d87-118">Click on the Hello World model to start it</span></span>
2. <span data-ttu-id="76d87-119">Click Actions, then New Action</span><span class="sxs-lookup"><span data-stu-id="76d87-119">Click Actions, then New Action</span></span>
    - <span data-ttu-id="76d87-120">An Action can be a text message that Conversation Learner returns to the user, an API call, or a card.</span><span class="sxs-lookup"><span data-stu-id="76d87-120">An Action can be a text message that Conversation Learner returns to the user, an API call, or a card.</span></span>
3. <span data-ttu-id="76d87-121">In Response, type 'Hello World!'</span><span class="sxs-lookup"><span data-stu-id="76d87-121">In Response, type 'Hello World!'</span></span>
    - <span data-ttu-id="76d87-122">This is the response that the bot will return</span><span class="sxs-lookup"><span data-stu-id="76d87-122">This is the response that the bot will return</span></span>
4. <span data-ttu-id="76d87-123">Click Create</span><span class="sxs-lookup"><span data-stu-id="76d87-123">Click Create</span></span>

<span data-ttu-id="76d87-124">You have created the first thing that the bot can do i.e. return a text response.</span><span class="sxs-lookup"><span data-stu-id="76d87-124">You have created the first thing that the bot can do i.e. return a text response.</span></span>

### <a name="train-the-bot"></a><span data-ttu-id="76d87-125">Train the bot</span><span class="sxs-lookup"><span data-stu-id="76d87-125">Train the bot</span></span>

#### <a name="create-the-first-dialog"></a><span data-ttu-id="76d87-126">Create the first dialog</span><span class="sxs-lookup"><span data-stu-id="76d87-126">Create the first dialog</span></span>

1. <span data-ttu-id="76d87-127">Click Train Dialogs, then New Train Dialog</span><span class="sxs-lookup"><span data-stu-id="76d87-127">Click Train Dialogs, then New Train Dialog</span></span>
2. <span data-ttu-id="76d87-128">Enter an example of what the user will say in the begging of the conversation, for example, 'hello'.</span><span class="sxs-lookup"><span data-stu-id="76d87-128">Enter an example of what the user will say in the begging of the conversation, for example, 'hello'.</span></span>
3. <span data-ttu-id="76d87-129">Click Score Actions</span><span class="sxs-lookup"><span data-stu-id="76d87-129">Click Score Actions</span></span>
4. <span data-ttu-id="76d87-130">Select 'Hello World!'</span><span class="sxs-lookup"><span data-stu-id="76d87-130">Select 'Hello World!'</span></span>
    - <span data-ttu-id="76d87-131">This creates a one-turn example dialog.</span><span class="sxs-lookup"><span data-stu-id="76d87-131">This creates a one-turn example dialog.</span></span> 
2. <span data-ttu-id="76d87-132">Enter 'goodbye'</span><span class="sxs-lookup"><span data-stu-id="76d87-132">Enter 'goodbye'</span></span>
3. <span data-ttu-id="76d87-133">Click Score Actions</span><span class="sxs-lookup"><span data-stu-id="76d87-133">Click Score Actions</span></span>
4. <span data-ttu-id="76d87-134">click Add Action, then enter 'Goodbye!'</span><span class="sxs-lookup"><span data-stu-id="76d87-134">click Add Action, then enter 'Goodbye!'</span></span> <span data-ttu-id="76d87-135">in Response, then click 'Create'</span><span class="sxs-lookup"><span data-stu-id="76d87-135">in Response, then click 'Create'</span></span>
5. <span data-ttu-id="76d87-136">Click Done Teaching.</span><span class="sxs-lookup"><span data-stu-id="76d87-136">Click Done Teaching.</span></span> <span data-ttu-id="76d87-137">This will end this training dialog.</span><span class="sxs-lookup"><span data-stu-id="76d87-137">This will end this training dialog.</span></span>

<span data-ttu-id="76d87-138">Now you have one teaching dialog in the system.</span><span class="sxs-lookup"><span data-stu-id="76d87-138">Now you have one teaching dialog in the system.</span></span>

#### <a name="continue-teaching-the-bot"></a><span data-ttu-id="76d87-139">Continue teaching the bot</span><span class="sxs-lookup"><span data-stu-id="76d87-139">Continue teaching the bot</span></span>
<span data-ttu-id="76d87-140">Let's do one more training, and see how the bot responds.</span><span class="sxs-lookup"><span data-stu-id="76d87-140">Let's do one more training, and see how the bot responds.</span></span>

1. <span data-ttu-id="76d87-141">Click New Train Dialog</span><span class="sxs-lookup"><span data-stu-id="76d87-141">Click New Train Dialog</span></span>
2. <span data-ttu-id="76d87-142">Enter 'hi there'</span><span class="sxs-lookup"><span data-stu-id="76d87-142">Enter 'hi there'</span></span>
    - <span data-ttu-id="76d87-143">This is similar to the first dialog, and we expect to get a good score from the bot.</span><span class="sxs-lookup"><span data-stu-id="76d87-143">This is similar to the first dialog, and we expect to get a good score from the bot.</span></span>
2. <span data-ttu-id="76d87-144">Click Score Action</span><span class="sxs-lookup"><span data-stu-id="76d87-144">Click Score Action</span></span>
    - <span data-ttu-id="76d87-145">The position and score may not still be accurate enough and require additional teaching.</span><span class="sxs-lookup"><span data-stu-id="76d87-145">The position and score may not still be accurate enough and require additional teaching.</span></span>
3. <span data-ttu-id="76d87-146">Click Select next to 'Hello World!'</span><span class="sxs-lookup"><span data-stu-id="76d87-146">Click Select next to 'Hello World!'</span></span>
4. <span data-ttu-id="76d87-147">Then enter 'bye'</span><span class="sxs-lookup"><span data-stu-id="76d87-147">Then enter 'bye'</span></span>
5. <span data-ttu-id="76d87-148">Click Score Actions</span><span class="sxs-lookup"><span data-stu-id="76d87-148">Click Score Actions</span></span>
6. <span data-ttu-id="76d87-149">Select 'Goodbye!'</span><span class="sxs-lookup"><span data-stu-id="76d87-149">Select 'Goodbye!'</span></span>
7. <span data-ttu-id="76d87-150">Click Done Teaching</span><span class="sxs-lookup"><span data-stu-id="76d87-150">Click Done Teaching</span></span>

![](../media/tutorial1_actions.PNG)

<span data-ttu-id="76d87-151">We will do another teaching session to see how the bot is working.</span><span class="sxs-lookup"><span data-stu-id="76d87-151">We will do another teaching session to see how the bot is working.</span></span>

<span data-ttu-id="76d87-152">Repeat the above steps using 'hi', and 'byebye', and note the changes in position and score of the bots response when you click Score Action.</span><span class="sxs-lookup"><span data-stu-id="76d87-152">Repeat the above steps using 'hi', and 'byebye', and note the changes in position and score of the bots response when you click Score Action.</span></span>

<span data-ttu-id="76d87-153">You can now repeat the steps using 'howdy' and 'good bye', and note that the scoring shows improvements in scores indicating the bot has learned this interaction.</span><span class="sxs-lookup"><span data-stu-id="76d87-153">You can now repeat the steps using 'howdy' and 'good bye', and note that the scoring shows improvements in scores indicating the bot has learned this interaction.</span></span>

![](../media/tutorial1_dialogs.PNG)

### <a name="test-the-bot-as-an-end-user"></a><span data-ttu-id="76d87-154">Test the bot as an end user</span><span class="sxs-lookup"><span data-stu-id="76d87-154">Test the bot as an end user</span></span>

1. <span data-ttu-id="76d87-155">Click Log Dialogs, then New Log Dialog</span><span class="sxs-lookup"><span data-stu-id="76d87-155">Click Log Dialogs, then New Log Dialog</span></span>
2. <span data-ttu-id="76d87-156">Type 'hello there'</span><span class="sxs-lookup"><span data-stu-id="76d87-156">Type 'hello there'</span></span>
3. <span data-ttu-id="76d87-157">Then 'bye'</span><span class="sxs-lookup"><span data-stu-id="76d87-157">Then 'bye'</span></span>

<span data-ttu-id="76d87-158">You can also try starting a conversation with 'bye', and note the bot's response.</span><span class="sxs-lookup"><span data-stu-id="76d87-158">You can also try starting a conversation with 'bye', and note the bot's response.</span></span>

### <a name="view-conversations-in-the-log-dialogs"></a><span data-ttu-id="76d87-159">View conversations in the Log Dialogs</span><span class="sxs-lookup"><span data-stu-id="76d87-159">View conversations in the Log Dialogs</span></span>

<span data-ttu-id="76d87-160">In Log Dialogs, you can view the list of conversations, update, and save the interactions as training dialogs.</span><span class="sxs-lookup"><span data-stu-id="76d87-160">In Log Dialogs, you can view the list of conversations, update, and save the interactions as training dialogs.</span></span> <span data-ttu-id="76d87-161">To do that:</span><span class="sxs-lookup"><span data-stu-id="76d87-161">To do that:</span></span>

1. <span data-ttu-id="76d87-162">Click on the log of a conversation</span><span class="sxs-lookup"><span data-stu-id="76d87-162">Click on the log of a conversation</span></span>
2. <span data-ttu-id="76d87-163">If the conversation looks good, click on the last action e.g. 'Goodbye'.</span><span class="sxs-lookup"><span data-stu-id="76d87-163">If the conversation looks good, click on the last action e.g. 'Goodbye'.</span></span>
3. <span data-ttu-id="76d87-164">Click to select the suggested response.</span><span class="sxs-lookup"><span data-stu-id="76d87-164">Click to select the suggested response.</span></span> 
    - <span data-ttu-id="76d87-165">You can also select or add another action.</span><span class="sxs-lookup"><span data-stu-id="76d87-165">You can also select or add another action.</span></span>
4. <span data-ttu-id="76d87-166">Then click Done to save this as a training dialog.</span><span class="sxs-lookup"><span data-stu-id="76d87-166">Then click Done to save this as a training dialog.</span></span>

## <a name="next-steps"></a><span data-ttu-id="76d87-167">Next steps</span><span class="sxs-lookup"><span data-stu-id="76d87-167">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="76d87-168">Wait and non-wait actions</span><span class="sxs-lookup"><span data-stu-id="76d87-168">Wait and non-wait actions</span></span>](./2-wait-vs-nonwait-actions.md)