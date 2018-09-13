---
title: How to use Conversation Learner with other bot building technologies - Microsoft Cognitive Services | Microsoft Docs
titleSuffix: Azure
description: Learn how to use Conversation Learner with other bot building technologies.
services: cognitive-services
author: mattm
manager: larsliden
ms.service: cognitive-services
ms.component: conversation-learner
ms.topic: article
ms.date: 07/13/2018
ms.author: v-jaswel
ms.openlocfilehash: a03596ff8383a085314508d4a25d0ba89bcc3094
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870149"
---
# <a name="how-to-use-conversation-learner-with-other-bot-building-technologies"></a><span data-ttu-id="16c6a-103">How to use Conversation Learner with other bot building technologies</span><span class="sxs-lookup"><span data-stu-id="16c6a-103">How to use Conversation Learner with other bot building technologies</span></span>

<span data-ttu-id="16c6a-104">This tutorial covers how to use Conversation Learner with other bot building technologies and how memory (or state) can be shared between these technologies</span><span class="sxs-lookup"><span data-stu-id="16c6a-104">This tutorial covers how to use Conversation Learner with other bot building technologies and how memory (or state) can be shared between these technologies</span></span> 

## <a name="video"></a><span data-ttu-id="16c6a-105">Video</span><span class="sxs-lookup"><span data-stu-id="16c6a-105">Video</span></span>

<span data-ttu-id="16c6a-106">[![Tutorial 15 Preview](http://aka.ms/cl-tutorial-15-preview)](http://aka.ms/blis-tutorial-15)</span><span class="sxs-lookup"><span data-stu-id="16c6a-106">[![Tutorial 15 Preview](http://aka.ms/cl-tutorial-15-preview)](http://aka.ms/blis-tutorial-15)</span></span>

## <a name="requirements"></a><span data-ttu-id="16c6a-107">Requirements</span><span class="sxs-lookup"><span data-stu-id="16c6a-107">Requirements</span></span>
<span data-ttu-id="16c6a-108">This tutorial requires using the bot emulator to create log dialogs, not the Log Dialog Web UI.</span><span class="sxs-lookup"><span data-stu-id="16c6a-108">This tutorial requires using the bot emulator to create log dialogs, not the Log Dialog Web UI.</span></span>  

<span data-ttu-id="16c6a-109">This tutorial requires that the hybrid tutorial bot is running:</span><span class="sxs-lookup"><span data-stu-id="16c6a-109">This tutorial requires that the hybrid tutorial bot is running:</span></span>

    npm run tutorial-hybrid

## <a name="details"></a><span data-ttu-id="16c6a-110">Details</span><span class="sxs-lookup"><span data-stu-id="16c6a-110">Details</span></span>

<span data-ttu-id="16c6a-111">While Conversation Learner is in control, all state relative to the Conversation Learner Session must be stored in the Conversation Learner’s memory manager.</span><span class="sxs-lookup"><span data-stu-id="16c6a-111">While Conversation Learner is in control, all state relative to the Conversation Learner Session must be stored in the Conversation Learner’s memory manager.</span></span> <span data-ttu-id="16c6a-112">This is necessary as the machine learning uses the state to determine how to drive the conversation.</span><span class="sxs-lookup"><span data-stu-id="16c6a-112">This is necessary as the machine learning uses the state to determine how to drive the conversation.</span></span> <span data-ttu-id="16c6a-113">External state can be passed into the Conversation Learner in the OnSessionStartCallback that is called when the session begins.</span><span class="sxs-lookup"><span data-stu-id="16c6a-113">External state can be passed into the Conversation Learner in the OnSessionStartCallback that is called when the session begins.</span></span> <span data-ttu-id="16c6a-114">Internal can be returned out by the OnSessionEndCallback when the session terminates.</span><span class="sxs-lookup"><span data-stu-id="16c6a-114">Internal can be returned out by the OnSessionEndCallback when the session terminates.</span></span>

<span data-ttu-id="16c6a-115">You can almost think of Conversation Learner as a function call that takes some initial state and returns values.</span><span class="sxs-lookup"><span data-stu-id="16c6a-115">You can almost think of Conversation Learner as a function call that takes some initial state and returns values.</span></span>

<span data-ttu-id="16c6a-116">In this example, you will create a hybrid bot using two different systems:</span><span class="sxs-lookup"><span data-stu-id="16c6a-116">In this example, you will create a hybrid bot using two different systems:</span></span>
1. <span data-ttu-id="16c6a-117">A Conversation Learner Model</span><span class="sxs-lookup"><span data-stu-id="16c6a-117">A Conversation Learner Model</span></span> <br />
<span data-ttu-id="16c6a-118">Uses conversation learner model to determine the next action of the bot based on the current session.</span><span class="sxs-lookup"><span data-stu-id="16c6a-118">Uses conversation learner model to determine the next action of the bot based on the current session.</span></span>
<span data-ttu-id="16c6a-119">This part of the bot takes one piece of initial state `isOpen` (which indicates whether a store is open or closed) and returns another piece of state `purchaseItem` (the name of an item the user purchases.)</span><span class="sxs-lookup"><span data-stu-id="16c6a-119">This part of the bot takes one piece of initial state `isOpen` (which indicates whether a store is open or closed) and returns another piece of state `purchaseItem` (the name of an item the user purchases.)</span></span>

2. <span data-ttu-id="16c6a-120">Text matching</span><span class="sxs-lookup"><span data-stu-id="16c6a-120">Text matching</span></span> <br />
<span data-ttu-id="16c6a-121">Simply looks at incoming text for specific strings and responds.</span><span class="sxs-lookup"><span data-stu-id="16c6a-121">Simply looks at incoming text for specific strings and responds.</span></span>
<span data-ttu-id="16c6a-122">This part of the bot manages the Bots' other storage mechanisms and is responsible for starting the CL session.</span><span class="sxs-lookup"><span data-stu-id="16c6a-122">This part of the bot manages the Bots' other storage mechanisms and is responsible for starting the CL session.</span></span> <span data-ttu-id="16c6a-123">Specifically it manages three variables: `usingConversationLearner`, `storeIsOpen`, and `purchaseItem`.</span><span class="sxs-lookup"><span data-stu-id="16c6a-123">Specifically it manages three variables: `usingConversationLearner`, `storeIsOpen`, and `purchaseItem`.</span></span>

<span data-ttu-id="16c6a-124">Let’s start by taking a look at the model used in this demo.</span><span class="sxs-lookup"><span data-stu-id="16c6a-124">Let’s start by taking a look at the model used in this demo.</span></span>

### <a name="open-the-demo"></a><span data-ttu-id="16c6a-125">Open the demo</span><span class="sxs-lookup"><span data-stu-id="16c6a-125">Open the demo</span></span>

<span data-ttu-id="16c6a-126">In the model list of the web UI, click on Tutorial-15-Hybrid.</span><span class="sxs-lookup"><span data-stu-id="16c6a-126">In the model list of the web UI, click on Tutorial-15-Hybrid.</span></span>

## <a name="entities"></a><span data-ttu-id="16c6a-127">Entities</span><span class="sxs-lookup"><span data-stu-id="16c6a-127">Entities</span></span>

<span data-ttu-id="16c6a-128">Open the entities page and notice two entities: `isOpen` and `purchaseItem`</span><span class="sxs-lookup"><span data-stu-id="16c6a-128">Open the entities page and notice two entities: `isOpen` and `purchaseItem`</span></span>

<span data-ttu-id="16c6a-129">To understand how these entities are used, open the file: `C:\<installedpath\>\src\demos\tutorialHybrid.ts` to look at the callbacks.</span><span class="sxs-lookup"><span data-stu-id="16c6a-129">To understand how these entities are used, open the file: `C:\<installedpath\>\src\demos\tutorialHybrid.ts` to look at the callbacks.</span></span>

<span data-ttu-id="16c6a-130">Notice that the code in `OnSessionStartCallback` copies the value of `storeIsOpen` from BotBuilder conversation storage as the value of the `isOpen` entity so it is available to Conversation Learner.</span><span class="sxs-lookup"><span data-stu-id="16c6a-130">Notice that the code in `OnSessionStartCallback` copies the value of `storeIsOpen` from BotBuilder conversation storage as the value of the `isOpen` entity so it is available to Conversation Learner.</span></span> <span data-ttu-id="16c6a-131">See the following code:</span><span class="sxs-lookup"><span data-stu-id="16c6a-131">See the following code:</span></span>

![](../media/tutorial17_sessionstart.PNG)

<span data-ttu-id="16c6a-132">Likewise, the code in `OnSessionEndCallback` (if the session was ended due to a learned activity and not merely a timeout) copies the value of entity `purchaseItem` out to BotBuilder storage `purchaseItem`.</span><span class="sxs-lookup"><span data-stu-id="16c6a-132">Likewise, the code in `OnSessionEndCallback` (if the session was ended due to a learned activity and not merely a timeout) copies the value of entity `purchaseItem` out to BotBuilder storage `purchaseItem`.</span></span> <span data-ttu-id="16c6a-133">See the following code:</span><span class="sxs-lookup"><span data-stu-id="16c6a-133">See the following code:</span></span>

![](../media/tutorial17_sessionend.PNG)

<span data-ttu-id="16c6a-134">Now let's look at the Actions.</span><span class="sxs-lookup"><span data-stu-id="16c6a-134">Now let's look at the Actions.</span></span>

## <a name="actions"></a><span data-ttu-id="16c6a-135">Actions</span><span class="sxs-lookup"><span data-stu-id="16c6a-135">Actions</span></span>

<span data-ttu-id="16c6a-136">Notice the model has four actions.</span><span class="sxs-lookup"><span data-stu-id="16c6a-136">Notice the model has four actions.</span></span>

<span data-ttu-id="16c6a-137">The intended rules for the actions are as follows:</span><span class="sxs-lookup"><span data-stu-id="16c6a-137">The intended rules for the actions are as follows:</span></span>

- <span data-ttu-id="16c6a-138">If the `isOpen` entity is set, the Bot will ask "What would you like to buy?"</span><span class="sxs-lookup"><span data-stu-id="16c6a-138">If the `isOpen` entity is set, the Bot will ask "What would you like to buy?"</span></span> <span data-ttu-id="16c6a-139">and store that in the `puchaseItem` slot</span><span class="sxs-lookup"><span data-stu-id="16c6a-139">and store that in the `puchaseItem` slot</span></span>
- <span data-ttu-id="16c6a-140">If `isOpen` isn’t set, the Bot will say "I’m sorry we’re closed"</span><span class="sxs-lookup"><span data-stu-id="16c6a-140">If `isOpen` isn’t set, the Bot will say "I’m sorry we’re closed"</span></span>
- <span data-ttu-id="16c6a-141">The other two Actions are of the type `END_SESSION`.</span><span class="sxs-lookup"><span data-stu-id="16c6a-141">The other two Actions are of the type `END_SESSION`.</span></span>
- <span data-ttu-id="16c6a-142">The END_SESSION Action indicates to ConversationLearner that the conversation has completed.</span><span class="sxs-lookup"><span data-stu-id="16c6a-142">The END_SESSION Action indicates to ConversationLearner that the conversation has completed.</span></span>

### <a name="overall-bot-logic"></a><span data-ttu-id="16c6a-143">Overall Bot Logic</span><span class="sxs-lookup"><span data-stu-id="16c6a-143">Overall Bot Logic</span></span>

<span data-ttu-id="16c6a-144">First you see that if the Bot state’s `usingConversationLearner` flag has been set, we pass control to Conversation Learner.</span><span class="sxs-lookup"><span data-stu-id="16c6a-144">First you see that if the Bot state’s `usingConversationLearner` flag has been set, we pass control to Conversation Learner.</span></span> <span data-ttu-id="16c6a-145">If not, we pass control to something else.</span><span class="sxs-lookup"><span data-stu-id="16c6a-145">If not, we pass control to something else.</span></span>  <span data-ttu-id="16c6a-146">In this example, we’re showing simple text matching, but this could be any other Bot technology including LUIS, QnA maker and even another instance of Conversation Learner.</span><span class="sxs-lookup"><span data-stu-id="16c6a-146">In this example, we’re showing simple text matching, but this could be any other Bot technology including LUIS, QnA maker and even another instance of Conversation Learner.</span></span>

<span data-ttu-id="16c6a-147">We need a way for the user to open and close the store, so we do a string compare with "open store" and "close store" and set the "storeIsOpen" flag.</span><span class="sxs-lookup"><span data-stu-id="16c6a-147">We need a way for the user to open and close the store, so we do a string compare with "open store" and "close store" and set the "storeIsOpen" flag.</span></span>

<span data-ttu-id="16c6a-148">Next, we need a way to trigger handing control over to our Conversation Learner Model.</span><span class="sxs-lookup"><span data-stu-id="16c6a-148">Next, we need a way to trigger handing control over to our Conversation Learner Model.</span></span> <span data-ttu-id="16c6a-149">When we match to the "shop" string we do the following:</span><span class="sxs-lookup"><span data-stu-id="16c6a-149">When we match to the "shop" string we do the following:</span></span>
- <span data-ttu-id="16c6a-150">Set the `usingConversationLearner` flag in the Bot’s memory.</span><span class="sxs-lookup"><span data-stu-id="16c6a-150">Set the `usingConversationLearner` flag in the Bot’s memory.</span></span>
- <span data-ttu-id="16c6a-151">Call the "StartSession" method on our Conversation Learner Model.</span><span class="sxs-lookup"><span data-stu-id="16c6a-151">Call the "StartSession" method on our Conversation Learner Model.</span></span>  <span data-ttu-id="16c6a-152">This will trigger the "onSessionStartCallback" which will initialize the `isOpen` entity value</span><span class="sxs-lookup"><span data-stu-id="16c6a-152">This will trigger the "onSessionStartCallback" which will initialize the `isOpen` entity value</span></span>

<span data-ttu-id="16c6a-153">See below:</span><span class="sxs-lookup"><span data-stu-id="16c6a-153">See below:</span></span>

![](../media/tutorial17_useConversationLearner.PNG)

<span data-ttu-id="16c6a-154">We also do a text match to "history" which will display that last purchase item.</span><span class="sxs-lookup"><span data-stu-id="16c6a-154">We also do a text match to "history" which will display that last purchase item.</span></span>
<span data-ttu-id="16c6a-155">Finally, if anything else is typed, we display the available user commands</span><span class="sxs-lookup"><span data-stu-id="16c6a-155">Finally, if anything else is typed, we display the available user commands</span></span>

## <a name="train-dialog"></a><span data-ttu-id="16c6a-156">Train Dialog</span><span class="sxs-lookup"><span data-stu-id="16c6a-156">Train Dialog</span></span>

<span data-ttu-id="16c6a-157">For this tutorial, the model is already pre-trained.</span><span class="sxs-lookup"><span data-stu-id="16c6a-157">For this tutorial, the model is already pre-trained.</span></span>  <span data-ttu-id="16c6a-158">We will test the full bot to see the effect of the start and end session callbacks in practice.</span><span class="sxs-lookup"><span data-stu-id="16c6a-158">We will test the full bot to see the effect of the start and end session callbacks in practice.</span></span>

## <a name="testing-the-bot"></a><span data-ttu-id="16c6a-159">Testing the Bot</span><span class="sxs-lookup"><span data-stu-id="16c6a-159">Testing the Bot</span></span>

<span data-ttu-id="16c6a-160">Unlike single Conversation Leaner model bots you won’t be able to test this in the Conversation Learner UI as it can only show what’s handled by the Conversation Learner Model.</span><span class="sxs-lookup"><span data-stu-id="16c6a-160">Unlike single Conversation Leaner model bots you won’t be able to test this in the Conversation Learner UI as it can only show what’s handled by the Conversation Learner Model.</span></span>

### <a name="install-the-bot-framework-emulator"></a><span data-ttu-id="16c6a-161">Install the Bot framework emulator</span><span class="sxs-lookup"><span data-stu-id="16c6a-161">Install the Bot framework emulator</span></span>

- <span data-ttu-id="16c6a-162">Go to [https://github.com/Microsoft/BotFramework-Emulator](https://github.com/Microsoft/BotFramework-Emulator).</span><span class="sxs-lookup"><span data-stu-id="16c6a-162">Go to [https://github.com/Microsoft/BotFramework-Emulator](https://github.com/Microsoft/BotFramework-Emulator).</span></span>
- <span data-ttu-id="16c6a-163">Download and install the emulator.</span><span class="sxs-lookup"><span data-stu-id="16c6a-163">Download and install the emulator.</span></span>

### <a name="configure-the-emulator"></a><span data-ttu-id="16c6a-164">Configure the emulator</span><span class="sxs-lookup"><span data-stu-id="16c6a-164">Configure the emulator</span></span>

- <span data-ttu-id="16c6a-165">Open the emulator and ensure the URL is targeting the same port your bot is running on.</span><span class="sxs-lookup"><span data-stu-id="16c6a-165">Open the emulator and ensure the URL is targeting the same port your bot is running on.</span></span> <span data-ttu-id="16c6a-166">Likely: `http://localhost:3978/api/messages`</span><span class="sxs-lookup"><span data-stu-id="16c6a-166">Likely: `http://localhost:3978/api/messages`</span></span>

### <a name="test"></a><span data-ttu-id="16c6a-167">Test</span><span class="sxs-lookup"><span data-stu-id="16c6a-167">Test</span></span> 

#### <a name="scenario-1-store-is-closed"></a><span data-ttu-id="16c6a-168">Scenario 1: Store is closed</span><span class="sxs-lookup"><span data-stu-id="16c6a-168">Scenario 1: Store is closed</span></span>
1. <span data-ttu-id="16c6a-169">Enter 'shop'.</span><span class="sxs-lookup"><span data-stu-id="16c6a-169">Enter 'shop'.</span></span> <span data-ttu-id="16c6a-170">This is handled by the text matching and will give control to the Conversation Learner model.</span><span class="sxs-lookup"><span data-stu-id="16c6a-170">This is handled by the text matching and will give control to the Conversation Learner model.</span></span>
2. <span data-ttu-id="16c6a-171">Enter 'hello'.</span><span class="sxs-lookup"><span data-stu-id="16c6a-171">Enter 'hello'.</span></span>  <span data-ttu-id="16c6a-172">Because `isOpen` value is not set, the bot will say "I’m sorry we’re closed" and end the session.</span><span class="sxs-lookup"><span data-stu-id="16c6a-172">Because `isOpen` value is not set, the bot will say "I’m sorry we’re closed" and end the session.</span></span>

#### <a name="scenario-2-store-is-open"></a><span data-ttu-id="16c6a-173">Scenario 2: Store is open</span><span class="sxs-lookup"><span data-stu-id="16c6a-173">Scenario 2: Store is open</span></span>
3. <span data-ttu-id="16c6a-174">Enter 'open store'.</span><span class="sxs-lookup"><span data-stu-id="16c6a-174">Enter 'open store'.</span></span>  <span data-ttu-id="16c6a-175">This will set the `isOpen` to true.</span><span class="sxs-lookup"><span data-stu-id="16c6a-175">This will set the `isOpen` to true.</span></span>
4. <span data-ttu-id="16c6a-176">Enter 'shop'.</span><span class="sxs-lookup"><span data-stu-id="16c6a-176">Enter 'shop'.</span></span>
5. <span data-ttu-id="16c6a-177">Enter 'hello'.</span><span class="sxs-lookup"><span data-stu-id="16c6a-177">Enter 'hello'.</span></span>  <span data-ttu-id="16c6a-178">Because `isOpen` value is set to true, the bot will say "What would you like to buy?"</span><span class="sxs-lookup"><span data-stu-id="16c6a-178">Because `isOpen` value is set to true, the bot will say "What would you like to buy?"</span></span>
6. <span data-ttu-id="16c6a-179">Enter 'chair'.</span><span class="sxs-lookup"><span data-stu-id="16c6a-179">Enter 'chair'.</span></span> <span data-ttu-id="16c6a-180">'chair' will be saved into CL memory as the entity `purchaseItem`.</span><span class="sxs-lookup"><span data-stu-id="16c6a-180">'chair' will be saved into CL memory as the entity `purchaseItem`.</span></span> <span data-ttu-id="16c6a-181">The end session callback is invoked which copies this value out to the conversation store.</span><span class="sxs-lookup"><span data-stu-id="16c6a-181">The end session callback is invoked which copies this value out to the conversation store.</span></span>
7. <span data-ttu-id="16c6a-182">Enter 'history'.</span><span class="sxs-lookup"><span data-stu-id="16c6a-182">Enter 'history'.</span></span>  <span data-ttu-id="16c6a-183">The bot will say 'You bought chair' as this was your last `purchaseItem`.</span><span class="sxs-lookup"><span data-stu-id="16c6a-183">The bot will say 'You bought chair' as this was your last `purchaseItem`.</span></span>

## <a name="conclusion"></a><span data-ttu-id="16c6a-184">Conclusion</span><span class="sxs-lookup"><span data-stu-id="16c6a-184">Conclusion</span></span>

<span data-ttu-id="16c6a-185">With what you have learned above you should be able to combine Conversation Learner with any other Bot technology</span><span class="sxs-lookup"><span data-stu-id="16c6a-185">With what you have learned above you should be able to combine Conversation Learner with any other Bot technology</span></span>
