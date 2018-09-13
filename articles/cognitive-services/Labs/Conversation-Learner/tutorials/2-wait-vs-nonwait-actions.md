---
title: How to use wait and non-wait actions with a Conversation Learner model - Microsoft Cognitive Services| Microsoft Docs
titleSuffix: Azure
description: Learn how to use wait and non-wait actions with a Conversation Learner model.
services: cognitive-services
author: v-jaswel
manager: nolachar
ms.service: cognitive-services
ms.component: conversation-learner
ms.topic: article
ms.date: 04/30/2018
ms.author: v-jaswel
ms.openlocfilehash: a8f7ccf79e750c9f3c21c25c50c3e275db7e4195
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857569"
---
# <a name="wait-and-non-wait-actions"></a><span data-ttu-id="f531d-103">Wait and non-wait actions</span><span class="sxs-lookup"><span data-stu-id="f531d-103">Wait and non-wait actions</span></span>

<span data-ttu-id="f531d-104">This tutorial shows the difference between wait actions and non-wait actions in the Conversation Learner.</span><span class="sxs-lookup"><span data-stu-id="f531d-104">This tutorial shows the difference between wait actions and non-wait actions in the Conversation Learner.</span></span>

## <a name="video"></a><span data-ttu-id="f531d-105">Video</span><span class="sxs-lookup"><span data-stu-id="f531d-105">Video</span></span>

<span data-ttu-id="f531d-106">[![Tutorial 2 Preview](http://aka.ms/cl-tutorial-02-preview)](http://aka.ms/blis-tutorial-02)</span><span class="sxs-lookup"><span data-stu-id="f531d-106">[![Tutorial 2 Preview](http://aka.ms/cl-tutorial-02-preview)](http://aka.ms/blis-tutorial-02)</span></span>

## <a name="requirements"></a><span data-ttu-id="f531d-107">Requirements</span><span class="sxs-lookup"><span data-stu-id="f531d-107">Requirements</span></span>
<span data-ttu-id="f531d-108">This tutorial requires that the general tutorial bot is running</span><span class="sxs-lookup"><span data-stu-id="f531d-108">This tutorial requires that the general tutorial bot is running</span></span>

    npm run tutorial-general

## <a name="details"></a><span data-ttu-id="f531d-109">Details</span><span class="sxs-lookup"><span data-stu-id="f531d-109">Details</span></span>

- <span data-ttu-id="f531d-110">Wait action: After the system takes a "wait" action, it will stop taking actions and wait for user input.</span><span class="sxs-lookup"><span data-stu-id="f531d-110">Wait action: After the system takes a "wait" action, it will stop taking actions and wait for user input.</span></span>
- <span data-ttu-id="f531d-111">Non-wait action: After the system takes a "non-wait" action, it will immediately choose another action (without waiting for user inpu first).</span><span class="sxs-lookup"><span data-stu-id="f531d-111">Non-wait action: After the system takes a "non-wait" action, it will immediately choose another action (without waiting for user inpu first).</span></span>

## <a name="steps"></a><span data-ttu-id="f531d-112">Steps</span><span class="sxs-lookup"><span data-stu-id="f531d-112">Steps</span></span>

### <a name="create-a-new-model"></a><span data-ttu-id="f531d-113">Create a new model</span><span class="sxs-lookup"><span data-stu-id="f531d-113">Create a new model</span></span>

1. <span data-ttu-id="f531d-114">In the Web UI, click New Model</span><span class="sxs-lookup"><span data-stu-id="f531d-114">In the Web UI, click New Model</span></span>
2. <span data-ttu-id="f531d-115">In Name, enter WaitNonWait.</span><span class="sxs-lookup"><span data-stu-id="f531d-115">In Name, enter WaitNonWait.</span></span> <span data-ttu-id="f531d-116">Then click Create.</span><span class="sxs-lookup"><span data-stu-id="f531d-116">Then click Create.</span></span>

### <a name="create-the-first-wait-action"></a><span data-ttu-id="f531d-117">Create the first Wait action</span><span class="sxs-lookup"><span data-stu-id="f531d-117">Create the first Wait action</span></span>

1. <span data-ttu-id="f531d-118">Click Actions, then New Action.</span><span class="sxs-lookup"><span data-stu-id="f531d-118">Click Actions, then New Action.</span></span>
2. <span data-ttu-id="f531d-119">In Response, enter 'Which animal do you want?'.</span><span class="sxs-lookup"><span data-stu-id="f531d-119">In Response, enter 'Which animal do you want?'.</span></span>
    - <span data-ttu-id="f531d-120">This is a Wait action, so leave the Wait for Response box checked.</span><span class="sxs-lookup"><span data-stu-id="f531d-120">This is a Wait action, so leave the Wait for Response box checked.</span></span>
3. <span data-ttu-id="f531d-121">Click Create.</span><span class="sxs-lookup"><span data-stu-id="f531d-121">Click Create.</span></span>

### <a name="create-a-non-wait-action"></a><span data-ttu-id="f531d-122">Create a Non-Wait action</span><span class="sxs-lookup"><span data-stu-id="f531d-122">Create a Non-Wait action</span></span>

1. <span data-ttu-id="f531d-123">Click New Action</span><span class="sxs-lookup"><span data-stu-id="f531d-123">Click New Action</span></span>
2. <span data-ttu-id="f531d-124">In Response, type 'Cows say moo'.</span><span class="sxs-lookup"><span data-stu-id="f531d-124">In Response, type 'Cows say moo'.</span></span>
3. <span data-ttu-id="f531d-125">Un-check the Wait for Response check-box.</span><span class="sxs-lookup"><span data-stu-id="f531d-125">Un-check the Wait for Response check-box.</span></span>
4. <span data-ttu-id="f531d-126">Click Create</span><span class="sxs-lookup"><span data-stu-id="f531d-126">Click Create</span></span>

### <a name="create-a-second-non-wait-action"></a><span data-ttu-id="f531d-127">Create a second Non-Wait action</span><span class="sxs-lookup"><span data-stu-id="f531d-127">Create a second Non-Wait action</span></span>

1. <span data-ttu-id="f531d-128">Click New Action</span><span class="sxs-lookup"><span data-stu-id="f531d-128">Click New Action</span></span>
2. <span data-ttu-id="f531d-129">In Response, type 'Ducks say quack'.</span><span class="sxs-lookup"><span data-stu-id="f531d-129">In Response, type 'Ducks say quack'.</span></span>
3. <span data-ttu-id="f531d-130">Un-check the Wait for Response check-box.</span><span class="sxs-lookup"><span data-stu-id="f531d-130">Un-check the Wait for Response check-box.</span></span>
4. <span data-ttu-id="f531d-131">Click Create</span><span class="sxs-lookup"><span data-stu-id="f531d-131">Click Create</span></span>

![](../media/tutorial2_actions.PNG)

### <a name="train-the-bot"></a><span data-ttu-id="f531d-132">Train the bot</span><span class="sxs-lookup"><span data-stu-id="f531d-132">Train the bot</span></span>

1. <span data-ttu-id="f531d-133">Click Train Dialogs, then New Train Dialog.</span><span class="sxs-lookup"><span data-stu-id="f531d-133">Click Train Dialogs, then New Train Dialog.</span></span>
2. <span data-ttu-id="f531d-134">Type 'hello'</span><span class="sxs-lookup"><span data-stu-id="f531d-134">Type 'hello'</span></span>
3. <span data-ttu-id="f531d-135">Click Score Actions, and Select 'Which animal do you want?'.</span><span class="sxs-lookup"><span data-stu-id="f531d-135">Click Score Actions, and Select 'Which animal do you want?'.</span></span>
4. <span data-ttu-id="f531d-136">Enter 'cow'</span><span class="sxs-lookup"><span data-stu-id="f531d-136">Enter 'cow'</span></span>
5. <span data-ttu-id="f531d-137">Click Score Actions, and Select 'Cows say moo'.</span><span class="sxs-lookup"><span data-stu-id="f531d-137">Click Score Actions, and Select 'Cows say moo'.</span></span>
    - <span data-ttu-id="f531d-138">The bot will not wait for input, and will take the next action.</span><span class="sxs-lookup"><span data-stu-id="f531d-138">The bot will not wait for input, and will take the next action.</span></span>
2. <span data-ttu-id="f531d-139">Select 'Which animal do you want?'.</span><span class="sxs-lookup"><span data-stu-id="f531d-139">Select 'Which animal do you want?'.</span></span>
3. <span data-ttu-id="f531d-140">Enter 'duck'</span><span class="sxs-lookup"><span data-stu-id="f531d-140">Enter 'duck'</span></span>
5. <span data-ttu-id="f531d-141">Click Score Actions, and Select 'Ducks say quack'.</span><span class="sxs-lookup"><span data-stu-id="f531d-141">Click Score Actions, and Select 'Ducks say quack'.</span></span>

![](../media/tutorial2_dialogs.PNG)

> [!NOTE]
> <span data-ttu-id="f531d-142">The sequence of the bot responses with regards to wait and non-wait actions.</span><span class="sxs-lookup"><span data-stu-id="f531d-142">The sequence of the bot responses with regards to wait and non-wait actions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f531d-143">Next steps</span><span class="sxs-lookup"><span data-stu-id="f531d-143">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f531d-144">Introduction to entities</span><span class="sxs-lookup"><span data-stu-id="f531d-144">Introduction to entities</span></span>](./3-introduction-to-entities.md)
