---
title: How to use API calls with a Conversation Learner model - Microsoft Cognitive Services | Microsoft Docs
titleSuffix: Azure
description: Learn how to use API calls with a Conversation Learner model.
services: cognitive-services
author: v-jaswel
manager: nolachar
ms.service: cognitive-services
ms.component: conversation-learner
ms.topic: article
ms.date: 04/30/2018
ms.author: v-jaswel
ms.openlocfilehash: 1d4013d736d8cfcb75874bc0c86d20b86ab4dd62
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868465"
---
# <a name="how-to-add-api-calls-to-a-conversation-learner-model"></a><span data-ttu-id="49ebc-103">How to add API calls to a Conversation Learner model</span><span class="sxs-lookup"><span data-stu-id="49ebc-103">How to add API calls to a Conversation Learner model</span></span>

<span data-ttu-id="49ebc-104">This tutorial shows how to add API calls to your model.</span><span class="sxs-lookup"><span data-stu-id="49ebc-104">This tutorial shows how to add API calls to your model.</span></span> <span data-ttu-id="49ebc-105">API calls are functions that you define and write in your bot, and which Conversation Learner can call.</span><span class="sxs-lookup"><span data-stu-id="49ebc-105">API calls are functions that you define and write in your bot, and which Conversation Learner can call.</span></span>

## <a name="video"></a><span data-ttu-id="49ebc-106">Video</span><span class="sxs-lookup"><span data-stu-id="49ebc-106">Video</span></span>

<span data-ttu-id="49ebc-107">[![Tutorial 12 Preview](http://aka.ms/cl-tutorial-12-preview)](http://aka.ms/blis-tutorial-12)</span><span class="sxs-lookup"><span data-stu-id="49ebc-107">[![Tutorial 12 Preview](http://aka.ms/cl-tutorial-12-preview)](http://aka.ms/blis-tutorial-12)</span></span>

## <a name="requirements"></a><span data-ttu-id="49ebc-108">Requirements</span><span class="sxs-lookup"><span data-stu-id="49ebc-108">Requirements</span></span>
<span data-ttu-id="49ebc-109">This tutorial requires that the "tutorialAPICalls.ts" bot is running.</span><span class="sxs-lookup"><span data-stu-id="49ebc-109">This tutorial requires that the "tutorialAPICalls.ts" bot is running.</span></span>

    npm run tutorial-api-calls

## <a name="details"></a><span data-ttu-id="49ebc-110">Details</span><span class="sxs-lookup"><span data-stu-id="49ebc-110">Details</span></span>

- <span data-ttu-id="49ebc-111">API calls can read and manipulate entities.</span><span class="sxs-lookup"><span data-stu-id="49ebc-111">API calls can read and manipulate entities.</span></span>
- <span data-ttu-id="49ebc-112">API calls have access to the memory manager object.</span><span class="sxs-lookup"><span data-stu-id="49ebc-112">API calls have access to the memory manager object.</span></span>
- <span data-ttu-id="49ebc-113">API calls can also take arguments -- this allows re-using the same API call to serve different purposes.</span><span class="sxs-lookup"><span data-stu-id="49ebc-113">API calls can also take arguments -- this allows re-using the same API call to serve different purposes.</span></span>

### <a name="open-the-demo"></a><span data-ttu-id="49ebc-114">Open the demo</span><span class="sxs-lookup"><span data-stu-id="49ebc-114">Open the demo</span></span>

<span data-ttu-id="49ebc-115">In the Model list of the web UI, click on Tutorial-12-APICalls.</span><span class="sxs-lookup"><span data-stu-id="49ebc-115">In the Model list of the web UI, click on Tutorial-12-APICalls.</span></span> 

### <a name="entities"></a><span data-ttu-id="49ebc-116">Entities</span><span class="sxs-lookup"><span data-stu-id="49ebc-116">Entities</span></span>

<span data-ttu-id="49ebc-117">We have defined one entity in the model called number.</span><span class="sxs-lookup"><span data-stu-id="49ebc-117">We have defined one entity in the model called number.</span></span>

![](../media/tutorial12_entities.PNG)

### <a name="api-calls"></a><span data-ttu-id="49ebc-118">API Calls</span><span class="sxs-lookup"><span data-stu-id="49ebc-118">API Calls</span></span>
<span data-ttu-id="49ebc-119">The code for the API calls is defined in the this file: C:\<installedpath\>\src\demos\tutorialAPICalls.ts.</span><span class="sxs-lookup"><span data-stu-id="49ebc-119">The code for the API calls is defined in the this file: C:\<installedpath\>\src\demos\tutorialAPICalls.ts.</span></span>

![](../media/tutorial12_apicalls.PNG)

- <span data-ttu-id="49ebc-120">The first API Callback is RandomGreeting.</span><span class="sxs-lookup"><span data-stu-id="49ebc-120">The first API Callback is RandomGreeting.</span></span> <span data-ttu-id="49ebc-121">It returns a random greeting defined in the greeting variable.</span><span class="sxs-lookup"><span data-stu-id="49ebc-121">It returns a random greeting defined in the greeting variable.</span></span>
- <span data-ttu-id="49ebc-122">The Multiply API callback: It will multiply two numbers provided by the user.</span><span class="sxs-lookup"><span data-stu-id="49ebc-122">The Multiply API callback: It will multiply two numbers provided by the user.</span></span> <span data-ttu-id="49ebc-123">It then returns the result of the multiplication of the two numbers.</span><span class="sxs-lookup"><span data-stu-id="49ebc-123">It then returns the result of the multiplication of the two numbers.</span></span> <span data-ttu-id="49ebc-124">This shows that API callbacks can take inputs.</span><span class="sxs-lookup"><span data-stu-id="49ebc-124">This shows that API callbacks can take inputs.</span></span> <span data-ttu-id="49ebc-125">Note that memory manager is the first argument.</span><span class="sxs-lookup"><span data-stu-id="49ebc-125">Note that memory manager is the first argument.</span></span> 
- <span data-ttu-id="49ebc-126">The ClearEntities API callback: clears the number entity to let the user enter the next number.</span><span class="sxs-lookup"><span data-stu-id="49ebc-126">The ClearEntities API callback: clears the number entity to let the user enter the next number.</span></span> <span data-ttu-id="49ebc-127">This illustrates how API calls can manipulate entities.</span><span class="sxs-lookup"><span data-stu-id="49ebc-127">This illustrates how API calls can manipulate entities.</span></span>

### <a name="actions"></a><span data-ttu-id="49ebc-128">Actions</span><span class="sxs-lookup"><span data-stu-id="49ebc-128">Actions</span></span>

<span data-ttu-id="49ebc-129">We have created four actions.</span><span class="sxs-lookup"><span data-stu-id="49ebc-129">We have created four actions.</span></span> 

![](../media/tutorial12_actions.PNG)

- <span data-ttu-id="49ebc-130">In addition to 'What number do you want to multiply by 12?'</span><span class="sxs-lookup"><span data-stu-id="49ebc-130">In addition to 'What number do you want to multiply by 12?'</span></span> <span data-ttu-id="49ebc-131">which is a communicative action, there are three different API calls that illustrate the typical API call patterns.</span><span class="sxs-lookup"><span data-stu-id="49ebc-131">which is a communicative action, there are three different API calls that illustrate the typical API call patterns.</span></span>

- <span data-ttu-id="49ebc-132">RandomGreeting: is a non-wait action.</span><span class="sxs-lookup"><span data-stu-id="49ebc-132">RandomGreeting: is a non-wait action.</span></span> <span data-ttu-id="49ebc-133">To set this up, in the Create Action Dialog, we selected the Action Type of API_LOCAL, then selected RandomGreeting.</span><span class="sxs-lookup"><span data-stu-id="49ebc-133">To set this up, in the Create Action Dialog, we selected the Action Type of API_LOCAL, then selected RandomGreeting.</span></span> 

![](../media/tutorial12_setupapicall.PNG)

<span data-ttu-id="49ebc-134">The refresh button next to the API is used if we were to stop the bot, and make any changes to the APIs.</span><span class="sxs-lookup"><span data-stu-id="49ebc-134">The refresh button next to the API is used if we were to stop the bot, and make any changes to the APIs.</span></span> <span data-ttu-id="49ebc-135">Clicking on refresh would pick up the latest changes.</span><span class="sxs-lookup"><span data-stu-id="49ebc-135">Clicking on refresh would pick up the latest changes.</span></span>

<span data-ttu-id="49ebc-136">Here's how we created the Multiply action: after selecting API_Local and API, we entered an entity ($number) for the first input value (num1string), and a value (12) for the second input value (num2string).</span><span class="sxs-lookup"><span data-stu-id="49ebc-136">Here's how we created the Multiply action: after selecting API_Local and API, we entered an entity ($number) for the first input value (num1string), and a value (12) for the second input value (num2string).</span></span> <span data-ttu-id="49ebc-137">This provides a level of indirection between the bot and the API calls so the same callback can be mapped to a few actions in the system and they differ on how the actions are assigned.</span><span class="sxs-lookup"><span data-stu-id="49ebc-137">This provides a level of indirection between the bot and the API calls so the same callback can be mapped to a few actions in the system and they differ on how the actions are assigned.</span></span>

![](../media/tutorial12_actionmultiply.PNG)

### <a name="train-dialog"></a><span data-ttu-id="49ebc-138">Train Dialog</span><span class="sxs-lookup"><span data-stu-id="49ebc-138">Train Dialog</span></span>

<span data-ttu-id="49ebc-139">Let's walk through a teaching dialog.</span><span class="sxs-lookup"><span data-stu-id="49ebc-139">Let's walk through a teaching dialog.</span></span>

1. <span data-ttu-id="49ebc-140">Click Train Dialogs, then New Train Dialog.</span><span class="sxs-lookup"><span data-stu-id="49ebc-140">Click Train Dialogs, then New Train Dialog.</span></span>
1. <span data-ttu-id="49ebc-141">Enter 'hi'.</span><span class="sxs-lookup"><span data-stu-id="49ebc-141">Enter 'hi'.</span></span>
2. <span data-ttu-id="49ebc-142">Click Score Action.</span><span class="sxs-lookup"><span data-stu-id="49ebc-142">Click Score Action.</span></span>
3. <span data-ttu-id="49ebc-143">Click to Select RandomGreeting.</span><span class="sxs-lookup"><span data-stu-id="49ebc-143">Click to Select RandomGreeting.</span></span> <span data-ttu-id="49ebc-144">This will execute the Random Greeting API call.</span><span class="sxs-lookup"><span data-stu-id="49ebc-144">This will execute the Random Greeting API call.</span></span>
3. <span data-ttu-id="49ebc-145">Click to Select 'What number to do you want to multiply by 12?'</span><span class="sxs-lookup"><span data-stu-id="49ebc-145">Click to Select 'What number to do you want to multiply by 12?'</span></span>
4. <span data-ttu-id="49ebc-146">Enter '8'.</span><span class="sxs-lookup"><span data-stu-id="49ebc-146">Enter '8'.</span></span> <span data-ttu-id="49ebc-147">Then click Score Actions.</span><span class="sxs-lookup"><span data-stu-id="49ebc-147">Then click Score Actions.</span></span>
4. <span data-ttu-id="49ebc-148">Select 'Multiply $number 12'.</span><span class="sxs-lookup"><span data-stu-id="49ebc-148">Select 'Multiply $number 12'.</span></span> <span data-ttu-id="49ebc-149">Note the result of the multiplication.</span><span class="sxs-lookup"><span data-stu-id="49ebc-149">Note the result of the multiplication.</span></span>
5. <span data-ttu-id="49ebc-150">Select 'Clear Entities'.</span><span class="sxs-lookup"><span data-stu-id="49ebc-150">Select 'Clear Entities'.</span></span>
    - <span data-ttu-id="49ebc-151">The `number` entity's value has been cleared.</span><span class="sxs-lookup"><span data-stu-id="49ebc-151">The `number` entity's value has been cleared.</span></span>
3. <span data-ttu-id="49ebc-152">Click to Select 'What number to do you want to multiply by 12?'</span><span class="sxs-lookup"><span data-stu-id="49ebc-152">Click to Select 'What number to do you want to multiply by 12?'</span></span>
4. <span data-ttu-id="49ebc-153">Click Done Testing.</span><span class="sxs-lookup"><span data-stu-id="49ebc-153">Click Done Testing.</span></span>

![](../media/tutorial12_dialog.PNG)

<span data-ttu-id="49ebc-154">You have now seen how to register API callbacks, their common patterns, and how to define arguments and associate values and entities in them.</span><span class="sxs-lookup"><span data-stu-id="49ebc-154">You have now seen how to register API callbacks, their common patterns, and how to define arguments and associate values and entities in them.</span></span>

## <a name="next-steps"></a><span data-ttu-id="49ebc-155">Next steps</span><span class="sxs-lookup"><span data-stu-id="49ebc-155">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="49ebc-156">Cards part 1</span><span class="sxs-lookup"><span data-stu-id="49ebc-156">Cards part 1</span></span>](./13-cards-1.md)
