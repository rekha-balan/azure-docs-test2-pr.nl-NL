---
title: How to add pre-built entities to a Conversation Learner model - Microsoft Cognitive Services | Microsoft Docs
titleSuffix: Azure
description: Learn how to add pre-built entities to a Conversation Learner model.
services: cognitive-services
author: v-jaswel
manager: nolachar
ms.service: cognitive-services
ms.component: conversation-learner
ms.topic: article
ms.date: 04/30/2018
ms.author: v-jaswel
ms.openlocfilehash: 84d73add5586aaaf130253a8122a4152e39bcbe9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864485"
---
# <a name="how-to-add-pre-built-entities"></a><span data-ttu-id="556d3-103">How to add pre-built entities</span><span class="sxs-lookup"><span data-stu-id="556d3-103">How to add pre-built entities</span></span>
<span data-ttu-id="556d3-104">This tutorial shows how to add "pre-built" entities to your Conversation Learner model.</span><span class="sxs-lookup"><span data-stu-id="556d3-104">This tutorial shows how to add "pre-built" entities to your Conversation Learner model.</span></span>

## <a name="video"></a><span data-ttu-id="556d3-105">Video</span><span class="sxs-lookup"><span data-stu-id="556d3-105">Video</span></span>

<span data-ttu-id="556d3-106">[![Tutorial 7 Preview](http://aka.ms/cl-tutorial-07-preview)](http://aka.ms/blis-tutorial-07)</span><span class="sxs-lookup"><span data-stu-id="556d3-106">[![Tutorial 7 Preview](http://aka.ms/cl-tutorial-07-preview)](http://aka.ms/blis-tutorial-07)</span></span>

## <a name="requirements"></a><span data-ttu-id="556d3-107">Requirements</span><span class="sxs-lookup"><span data-stu-id="556d3-107">Requirements</span></span>
<span data-ttu-id="556d3-108">This tutorial requires that the general tutorial bot is running</span><span class="sxs-lookup"><span data-stu-id="556d3-108">This tutorial requires that the general tutorial bot is running</span></span>

    npm run tutorial-general

## <a name="details"></a><span data-ttu-id="556d3-109">Details</span><span class="sxs-lookup"><span data-stu-id="556d3-109">Details</span></span>

<span data-ttu-id="556d3-110">Pre-built entities recognize common types of entities, such as numbers, dates, monetary amounts, and others.</span><span class="sxs-lookup"><span data-stu-id="556d3-110">Pre-built entities recognize common types of entities, such as numbers, dates, monetary amounts, and others.</span></span>  <span data-ttu-id="556d3-111">Unlike custom entities, they work "out-of-the-box" and do not require any training.</span><span class="sxs-lookup"><span data-stu-id="556d3-111">Unlike custom entities, they work "out-of-the-box" and do not require any training.</span></span>  <span data-ttu-id="556d3-112">Unlike custom entities, their behavior cannot be changed.</span><span class="sxs-lookup"><span data-stu-id="556d3-112">Unlike custom entities, their behavior cannot be changed.</span></span>  <span data-ttu-id="556d3-113">By default, pre-built entities are multi-valued - that is, the bot's memory will accumulate every identified instance of the entity.</span><span class="sxs-lookup"><span data-stu-id="556d3-113">By default, pre-built entities are multi-valued - that is, the bot's memory will accumulate every identified instance of the entity.</span></span>

## <a name="steps"></a><span data-ttu-id="556d3-114">Steps</span><span class="sxs-lookup"><span data-stu-id="556d3-114">Steps</span></span>

### <a name="create-the-model"></a><span data-ttu-id="556d3-115">Create the model</span><span class="sxs-lookup"><span data-stu-id="556d3-115">Create the model</span></span>

1. <span data-ttu-id="556d3-116">In the Web UI, click New Model</span><span class="sxs-lookup"><span data-stu-id="556d3-116">In the Web UI, click New Model</span></span>
2. <span data-ttu-id="556d3-117">In Name, enter BuiltInEntities.</span><span class="sxs-lookup"><span data-stu-id="556d3-117">In Name, enter BuiltInEntities.</span></span> <span data-ttu-id="556d3-118">Then click Create.</span><span class="sxs-lookup"><span data-stu-id="556d3-118">Then click Create.</span></span>

### <a name="create-an-entity"></a><span data-ttu-id="556d3-119">Create an entity</span><span class="sxs-lookup"><span data-stu-id="556d3-119">Create an entity</span></span>

1. <span data-ttu-id="556d3-120">Click Entities, then New Entity.</span><span class="sxs-lookup"><span data-stu-id="556d3-120">Click Entities, then New Entity.</span></span>
2. <span data-ttu-id="556d3-121">Click on EntityType drop-down, and select datetimev2.</span><span class="sxs-lookup"><span data-stu-id="556d3-121">Click on EntityType drop-down, and select datetimev2.</span></span>
    - <span data-ttu-id="556d3-122">Programmable and Negatable options are disabled, because they do not apply to pre-build entities.</span><span class="sxs-lookup"><span data-stu-id="556d3-122">Programmable and Negatable options are disabled, because they do not apply to pre-build entities.</span></span>
3. <span data-ttu-id="556d3-123">Click Create.</span><span class="sxs-lookup"><span data-stu-id="556d3-123">Click Create.</span></span>

![](../media/tutorial7_entities.PNG)

### <a name="create-two-actions"></a><span data-ttu-id="556d3-124">Create two actions</span><span class="sxs-lookup"><span data-stu-id="556d3-124">Create two actions</span></span>

1. <span data-ttu-id="556d3-125">Click Actions, then New Action</span><span class="sxs-lookup"><span data-stu-id="556d3-125">Click Actions, then New Action</span></span>
2. <span data-ttu-id="556d3-126">In Response, type 'The date is $luis-datetimev2'.</span><span class="sxs-lookup"><span data-stu-id="556d3-126">In Response, type 'The date is $luis-datetimev2'.</span></span>
3. <span data-ttu-id="556d3-127">Click Create.</span><span class="sxs-lookup"><span data-stu-id="556d3-127">Click Create.</span></span>

![](../media/tutorial7_actions.PNG)

<span data-ttu-id="556d3-128">Then create the second action:</span><span class="sxs-lookup"><span data-stu-id="556d3-128">Then create the second action:</span></span>

1. <span data-ttu-id="556d3-129">Click Actions, then New Action to create a second action.</span><span class="sxs-lookup"><span data-stu-id="556d3-129">Click Actions, then New Action to create a second action.</span></span>
3. <span data-ttu-id="556d3-130">In Response, type 'What's the date?'.</span><span class="sxs-lookup"><span data-stu-id="556d3-130">In Response, type 'What's the date?'.</span></span>
4. <span data-ttu-id="556d3-131">In Disqualifying Entities, enter 'luis-datetimev2'.</span><span class="sxs-lookup"><span data-stu-id="556d3-131">In Disqualifying Entities, enter 'luis-datetimev2'.</span></span>
4. <span data-ttu-id="556d3-132">Click Create</span><span class="sxs-lookup"><span data-stu-id="556d3-132">Click Create</span></span>

![](../media/tutorial7_actions2.PNG)

<span data-ttu-id="556d3-133">Now you have two actions.</span><span class="sxs-lookup"><span data-stu-id="556d3-133">Now you have two actions.</span></span>

### <a name="train-the-bot"></a><span data-ttu-id="556d3-134">Train the bot</span><span class="sxs-lookup"><span data-stu-id="556d3-134">Train the bot</span></span>

1. <span data-ttu-id="556d3-135">Click Train Dialogs, then New Train Dialog.</span><span class="sxs-lookup"><span data-stu-id="556d3-135">Click Train Dialogs, then New Train Dialog.</span></span>
2. <span data-ttu-id="556d3-136">Type 'hello'.</span><span class="sxs-lookup"><span data-stu-id="556d3-136">Type 'hello'.</span></span>
3. <span data-ttu-id="556d3-137">Click Score Actions, and Select 'What's the date?'</span><span class="sxs-lookup"><span data-stu-id="556d3-137">Click Score Actions, and Select 'What's the date?'</span></span>
2. <span data-ttu-id="556d3-138">Enter 'today'.</span><span class="sxs-lookup"><span data-stu-id="556d3-138">Enter 'today'.</span></span> 
    - <span data-ttu-id="556d3-139">Notice today is tagged, and shows up in the second line since it is a pre-built entity and non-editable.</span><span class="sxs-lookup"><span data-stu-id="556d3-139">Notice today is tagged, and shows up in the second line since it is a pre-built entity and non-editable.</span></span>
5. <span data-ttu-id="556d3-140">Click Score Actions</span><span class="sxs-lookup"><span data-stu-id="556d3-140">Click Score Actions</span></span>
    - <span data-ttu-id="556d3-141">Notice the date now appears in Entity Memory section.</span><span class="sxs-lookup"><span data-stu-id="556d3-141">Notice the date now appears in Entity Memory section.</span></span> 
    - <span data-ttu-id="556d3-142">If you mouse over the date, you will see the additional data provided by LUIS, which is usable and can further be manipulated in code.</span><span class="sxs-lookup"><span data-stu-id="556d3-142">If you mouse over the date, you will see the additional data provided by LUIS, which is usable and can further be manipulated in code.</span></span> 
6. <span data-ttu-id="556d3-143">Select 'The date is $luis-datetimev2'.</span><span class="sxs-lookup"><span data-stu-id="556d3-143">Select 'The date is $luis-datetimev2'.</span></span>
7. <span data-ttu-id="556d3-144">Click Done Teaching</span><span class="sxs-lookup"><span data-stu-id="556d3-144">Click Done Teaching</span></span>

## <a name="next-steps"></a><span data-ttu-id="556d3-145">Next steps</span><span class="sxs-lookup"><span data-stu-id="556d3-145">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="556d3-146">Alternative inputs</span><span class="sxs-lookup"><span data-stu-id="556d3-146">Alternative inputs</span></span>](./8-alternative-inputs.md)
