---
title: How to use session callbacks with a Conversation Learner model - Microsoft Cognitive Services | Microsoft Docs
titleSuffix: Azure
description: Learn how to use session callbacks with a Conversation Learner model.
services: cognitive-services
author: v-jaswel
manager: nolachar
ms.service: cognitive-services
ms.component: conversation-learner
ms.topic: article
ms.date: 04/30/2018
ms.author: v-jaswel
ms.openlocfilehash: 0f51b232470e4e4da3f25d40d025dd3b09dd1204
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871342"
---
# <a name="how-to-use-session-callbacks-with-a-conversation-learner-model"></a><span data-ttu-id="5e7e9-103">How to use session callbacks with a Conversation Learner model</span><span class="sxs-lookup"><span data-stu-id="5e7e9-103">How to use session callbacks with a Conversation Learner model</span></span>

<span data-ttu-id="5e7e9-104">This tutorial illustrates the onSessionStart and onSessionEnd callbacks.</span><span class="sxs-lookup"><span data-stu-id="5e7e9-104">This tutorial illustrates the onSessionStart and onSessionEnd callbacks.</span></span>

## <a name="video"></a><span data-ttu-id="5e7e9-105">Video</span><span class="sxs-lookup"><span data-stu-id="5e7e9-105">Video</span></span>

<span data-ttu-id="5e7e9-106">[![Tutorial 11 Preview](http://aka.ms/cl-tutorial-11-preview)](http://aka.ms/blis-tutorial-11)</span><span class="sxs-lookup"><span data-stu-id="5e7e9-106">[![Tutorial 11 Preview](http://aka.ms/cl-tutorial-11-preview)](http://aka.ms/blis-tutorial-11)</span></span>

## <a name="requirements"></a><span data-ttu-id="5e7e9-107">Requirements</span><span class="sxs-lookup"><span data-stu-id="5e7e9-107">Requirements</span></span>
<span data-ttu-id="5e7e9-108">This tutorial requires that the `tutorialSessionCallbacks` bot is running.</span><span class="sxs-lookup"><span data-stu-id="5e7e9-108">This tutorial requires that the `tutorialSessionCallbacks` bot is running.</span></span>

    npm run tutorial-session-callbacks

## <a name="details"></a><span data-ttu-id="5e7e9-109">Details</span><span class="sxs-lookup"><span data-stu-id="5e7e9-109">Details</span></span>
<span data-ttu-id="5e7e9-110">This tutorial covers the concept of a session, how sessions are handled by default, and how you can override that behavior.</span><span class="sxs-lookup"><span data-stu-id="5e7e9-110">This tutorial covers the concept of a session, how sessions are handled by default, and how you can override that behavior.</span></span>

<span data-ttu-id="5e7e9-111">A session is one conversation with the bot.</span><span class="sxs-lookup"><span data-stu-id="5e7e9-111">A session is one conversation with the bot.</span></span> <span data-ttu-id="5e7e9-112">It can have multiple turns, but there are no long breaks in the conversation (for example, 30 minutes).</span><span class="sxs-lookup"><span data-stu-id="5e7e9-112">It can have multiple turns, but there are no long breaks in the conversation (for example, 30 minutes).</span></span>  <span data-ttu-id="5e7e9-113">See the help page on "Limits" for the default session timeout duration.</span><span class="sxs-lookup"><span data-stu-id="5e7e9-113">See the help page on "Limits" for the default session timeout duration.</span></span>

<span data-ttu-id="5e7e9-114">If there are long breaks, then the bot will go to its next session.</span><span class="sxs-lookup"><span data-stu-id="5e7e9-114">If there are long breaks, then the bot will go to its next session.</span></span>  <span data-ttu-id="5e7e9-115">Starting a new session puts the recurrent neural network into its initial state.</span><span class="sxs-lookup"><span data-stu-id="5e7e9-115">Starting a new session puts the recurrent neural network into its initial state.</span></span>  <span data-ttu-id="5e7e9-116">By default, it also clears all entity values, although this behavior can be changed (illustrated below).</span><span class="sxs-lookup"><span data-stu-id="5e7e9-116">By default, it also clears all entity values, although this behavior can be changed (illustrated below).</span></span>

### <a name="open-the-demo"></a><span data-ttu-id="5e7e9-117">Open the demo</span><span class="sxs-lookup"><span data-stu-id="5e7e9-117">Open the demo</span></span>

<span data-ttu-id="5e7e9-118">In the Model list, click on Tutorial-11-SessionCallbacks.</span><span class="sxs-lookup"><span data-stu-id="5e7e9-118">In the Model list, click on Tutorial-11-SessionCallbacks.</span></span> 

### <a name="entities"></a><span data-ttu-id="5e7e9-119">Entities</span><span class="sxs-lookup"><span data-stu-id="5e7e9-119">Entities</span></span>

<span data-ttu-id="5e7e9-120">Four entities are defined in the model.</span><span class="sxs-lookup"><span data-stu-id="5e7e9-120">Four entities are defined in the model.</span></span>

![](../media/tutorial11_entities.PNG)

<span data-ttu-id="5e7e9-121">One thing to note is that BotName is a Programmatic Entity.</span><span class="sxs-lookup"><span data-stu-id="5e7e9-121">One thing to note is that BotName is a Programmatic Entity.</span></span>  <span data-ttu-id="5e7e9-122">This entity will be set by the bot at session start time.</span><span class="sxs-lookup"><span data-stu-id="5e7e9-122">This entity will be set by the bot at session start time.</span></span>

### <a name="actions"></a><span data-ttu-id="5e7e9-123">Actions</span><span class="sxs-lookup"><span data-stu-id="5e7e9-123">Actions</span></span>

<span data-ttu-id="5e7e9-124">Four actions are defined in the model.</span><span class="sxs-lookup"><span data-stu-id="5e7e9-124">Four actions are defined in the model.</span></span>

![](../media/tutorial11_actions.PNG)

<span data-ttu-id="5e7e9-125">First, this tutorial will show how to control entity values at the start of the session -- for example, setting the BotName entity before the user says anything.</span><span class="sxs-lookup"><span data-stu-id="5e7e9-125">First, this tutorial will show how to control entity values at the start of the session -- for example, setting the BotName entity before the user says anything.</span></span>

<span data-ttu-id="5e7e9-126">Second, this tutorial will show how to persist values from one session to the next.</span><span class="sxs-lookup"><span data-stu-id="5e7e9-126">Second, this tutorial will show how to persist values from one session to the next.</span></span>  <span data-ttu-id="5e7e9-127">In this tutorial, we assume the user's name and phone number remain the same from one session to the next, but that their location may change.</span><span class="sxs-lookup"><span data-stu-id="5e7e9-127">In this tutorial, we assume the user's name and phone number remain the same from one session to the next, but that their location may change.</span></span>  <span data-ttu-id="5e7e9-128">We therefore persist name and phone number across sessions, but clear user location.</span><span class="sxs-lookup"><span data-stu-id="5e7e9-128">We therefore persist name and phone number across sessions, but clear user location.</span></span>

### <a name="train-dialog"></a><span data-ttu-id="5e7e9-129">Train Dialog</span><span class="sxs-lookup"><span data-stu-id="5e7e9-129">Train Dialog</span></span>

<span data-ttu-id="5e7e9-130">Here is an example dialog.</span><span class="sxs-lookup"><span data-stu-id="5e7e9-130">Here is an example dialog.</span></span> <span data-ttu-id="5e7e9-131">This is one session - that is, there are no long breaks in this dialog.</span><span class="sxs-lookup"><span data-stu-id="5e7e9-131">This is one session - that is, there are no long breaks in this dialog.</span></span>

![](../media/tutorial11_traindialog.PNG)

### <a name="code-for-the-callbacks"></a><span data-ttu-id="5e7e9-132">Code for the callbacks</span><span class="sxs-lookup"><span data-stu-id="5e7e9-132">Code for the callbacks</span></span>

<span data-ttu-id="5e7e9-133">The code for the callback methods is in the file: c:\<installedpath>\src\demos\tutorialSessionCallbacks.ts.</span><span class="sxs-lookup"><span data-stu-id="5e7e9-133">The code for the callback methods is in the file: c:\<installedpath>\src\demos\tutorialSessionCallbacks.ts.</span></span>

![](../media/tutorial11_code.PNG)

<span data-ttu-id="5e7e9-134">Both of these methods are optional.</span><span class="sxs-lookup"><span data-stu-id="5e7e9-134">Both of these methods are optional.</span></span>

- <span data-ttu-id="5e7e9-135">OnSessionStartCallback: this method sets the BotName entity.</span><span class="sxs-lookup"><span data-stu-id="5e7e9-135">OnSessionStartCallback: this method sets the BotName entity.</span></span>
- <span data-ttu-id="5e7e9-136">OnSessionEndCallback: you can specify what you want to preserve.</span><span class="sxs-lookup"><span data-stu-id="5e7e9-136">OnSessionEndCallback: you can specify what you want to preserve.</span></span> <span data-ttu-id="5e7e9-137">This will clear all entities except user name and user phone.</span><span class="sxs-lookup"><span data-stu-id="5e7e9-137">This will clear all entities except user name and user phone.</span></span>

### <a name="try-the-bot"></a><span data-ttu-id="5e7e9-138">Try the bot</span><span class="sxs-lookup"><span data-stu-id="5e7e9-138">Try the bot</span></span>

<span data-ttu-id="5e7e9-139">Switch to the Web UI, and click on Log Dialogs.</span><span class="sxs-lookup"><span data-stu-id="5e7e9-139">Switch to the Web UI, and click on Log Dialogs.</span></span>

1. <span data-ttu-id="5e7e9-140">Enter 'hello'.</span><span class="sxs-lookup"><span data-stu-id="5e7e9-140">Enter 'hello'.</span></span>
2. <span data-ttu-id="5e7e9-141">System: 'Hi, I'm Botty.</span><span class="sxs-lookup"><span data-stu-id="5e7e9-141">System: 'Hi, I'm Botty.</span></span> <span data-ttu-id="5e7e9-142">What's your name?'</span><span class="sxs-lookup"><span data-stu-id="5e7e9-142">What's your name?'</span></span> <span data-ttu-id="5e7e9-143">which has the name Botty coming from the OnSessionStartCallback.</span><span class="sxs-lookup"><span data-stu-id="5e7e9-143">which has the name Botty coming from the OnSessionStartCallback.</span></span>
3. <span data-ttu-id="5e7e9-144">Enter 'jason'.</span><span class="sxs-lookup"><span data-stu-id="5e7e9-144">Enter 'jason'.</span></span>
4. <span data-ttu-id="5e7e9-145">System: 'Hi jason.</span><span class="sxs-lookup"><span data-stu-id="5e7e9-145">System: 'Hi jason.</span></span> <span data-ttu-id="5e7e9-146">What's your phone number?'</span><span class="sxs-lookup"><span data-stu-id="5e7e9-146">What's your phone number?'</span></span>
5. <span data-ttu-id="5e7e9-147">Enter '555-555-5555'.</span><span class="sxs-lookup"><span data-stu-id="5e7e9-147">Enter '555-555-5555'.</span></span>
6. <span data-ttu-id="5e7e9-148">System: 'Can you tell Botty your location, jason?'</span><span class="sxs-lookup"><span data-stu-id="5e7e9-148">System: 'Can you tell Botty your location, jason?'</span></span>
7. <span data-ttu-id="5e7e9-149">Type 'Redmond'.</span><span class="sxs-lookup"><span data-stu-id="5e7e9-149">Type 'Redmond'.</span></span>

<span data-ttu-id="5e7e9-150">This is one session.</span><span class="sxs-lookup"><span data-stu-id="5e7e9-150">This is one session.</span></span> <span data-ttu-id="5e7e9-151">To start a new session, we need to end this session.</span><span class="sxs-lookup"><span data-stu-id="5e7e9-151">To start a new session, we need to end this session.</span></span> 

1. <span data-ttu-id="5e7e9-152">Click Session Timeout.</span><span class="sxs-lookup"><span data-stu-id="5e7e9-152">Click Session Timeout.</span></span> <span data-ttu-id="5e7e9-153">This will move you to the next session.</span><span class="sxs-lookup"><span data-stu-id="5e7e9-153">This will move you to the next session.</span></span>
    - <span data-ttu-id="5e7e9-154">The "Session Timeout" button is provided for debugging purposes.</span><span class="sxs-lookup"><span data-stu-id="5e7e9-154">The "Session Timeout" button is provided for debugging purposes.</span></span>  <span data-ttu-id="5e7e9-155">In an actual session, a long pause would need to occur, of approximately 30 minutes.</span><span class="sxs-lookup"><span data-stu-id="5e7e9-155">In an actual session, a long pause would need to occur, of approximately 30 minutes.</span></span>  <span data-ttu-id="5e7e9-156">See the help page on "Limits" for the default session timeout duration.</span><span class="sxs-lookup"><span data-stu-id="5e7e9-156">See the help page on "Limits" for the default session timeout duration.</span></span>
1. <span data-ttu-id="5e7e9-157">Enter 'hi'.</span><span class="sxs-lookup"><span data-stu-id="5e7e9-157">Enter 'hi'.</span></span>
2. <span data-ttu-id="5e7e9-158">System: 'Can you tell Botty your location, jason?'</span><span class="sxs-lookup"><span data-stu-id="5e7e9-158">System: 'Can you tell Botty your location, jason?'</span></span>
    - <span data-ttu-id="5e7e9-159">The system has remembered the name and phone number.</span><span class="sxs-lookup"><span data-stu-id="5e7e9-159">The system has remembered the name and phone number.</span></span>
2. <span data-ttu-id="5e7e9-160">Enter a new location: 'Seattle'.</span><span class="sxs-lookup"><span data-stu-id="5e7e9-160">Enter a new location: 'Seattle'.</span></span>
3. <span data-ttu-id="5e7e9-161">System: 'So, jason you are in Seattle'.</span><span class="sxs-lookup"><span data-stu-id="5e7e9-161">System: 'So, jason you are in Seattle'.</span></span>
4. <span data-ttu-id="5e7e9-162">Click Done Testing.</span><span class="sxs-lookup"><span data-stu-id="5e7e9-162">Click Done Testing.</span></span>

<span data-ttu-id="5e7e9-163">Let's switch back to Log Dialogs.</span><span class="sxs-lookup"><span data-stu-id="5e7e9-163">Let's switch back to Log Dialogs.</span></span> <span data-ttu-id="5e7e9-164">Notice the last conversation has split into two because each log dialog corresponds to one session.</span><span class="sxs-lookup"><span data-stu-id="5e7e9-164">Notice the last conversation has split into two because each log dialog corresponds to one session.</span></span>  

![](../media/tutorial11_splitdialogs.PNG)

- <span data-ttu-id="5e7e9-165">In the first interaction, Botty is set, but name and phone number are not.</span><span class="sxs-lookup"><span data-stu-id="5e7e9-165">In the first interaction, Botty is set, but name and phone number are not.</span></span>
- <span data-ttu-id="5e7e9-166">The second interaction shows the name and phone number.</span><span class="sxs-lookup"><span data-stu-id="5e7e9-166">The second interaction shows the name and phone number.</span></span>

<span data-ttu-id="5e7e9-167">You have now seen how sessions are handled by default, and how you can override the default behavior.</span><span class="sxs-lookup"><span data-stu-id="5e7e9-167">You have now seen how sessions are handled by default, and how you can override the default behavior.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="5e7e9-168">Next steps</span><span class="sxs-lookup"><span data-stu-id="5e7e9-168">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="5e7e9-169">API calls</span><span class="sxs-lookup"><span data-stu-id="5e7e9-169">API calls</span></span>](./12-api-calls.md)
