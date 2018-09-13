---
title: Demo Conversation Learner model, password reset - Microsoft Cognitive Services | Microsoft Docs
titleSuffix: Azure
description: Learn how to create a demo Conversation Learner model.
services: cognitive-services
author: v-jaswel
manager: nolachar
ms.service: cognitive-services
ms.component: conversation-learner
ms.topic: article
ms.date: 04/30/2018
ms.author: v-jaswel
ms.openlocfilehash: f633dd375d690a1c3e66a2a6e02ae69665dbe960
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865395"
---
# <a name="demo-password-reset"></a><span data-ttu-id="f7a79-103">Demo: Password reset</span><span class="sxs-lookup"><span data-stu-id="f7a79-103">Demo: Password reset</span></span>
<span data-ttu-id="f7a79-104">This demo illustrates a simple technical support bot that can help with password resets.</span><span class="sxs-lookup"><span data-stu-id="f7a79-104">This demo illustrates a simple technical support bot that can help with password resets.</span></span> 

<span data-ttu-id="f7a79-105">It shows how Conversation Learner can learn non-trivial dialog flows, multi-turn sequences, including an out-of-domain class.</span><span class="sxs-lookup"><span data-stu-id="f7a79-105">It shows how Conversation Learner can learn non-trivial dialog flows, multi-turn sequences, including an out-of-domain class.</span></span> <span data-ttu-id="f7a79-106">This demonstration does not use any code or entities.</span><span class="sxs-lookup"><span data-stu-id="f7a79-106">This demonstration does not use any code or entities.</span></span>

## <a name="video"></a><span data-ttu-id="f7a79-107">Video</span><span class="sxs-lookup"><span data-stu-id="f7a79-107">Video</span></span>

<span data-ttu-id="f7a79-108">[![Demo Password Preview](http://aka.ms/cl-demo-password-preview)](http://aka.ms/blis-demo-password)</span><span class="sxs-lookup"><span data-stu-id="f7a79-108">[![Demo Password Preview](http://aka.ms/cl-demo-password-preview)](http://aka.ms/blis-demo-password)</span></span>

## <a name="requirements"></a><span data-ttu-id="f7a79-109">Requirements</span><span class="sxs-lookup"><span data-stu-id="f7a79-109">Requirements</span></span>
<span data-ttu-id="f7a79-110">This tutorial requires that the password reset bot is running</span><span class="sxs-lookup"><span data-stu-id="f7a79-110">This tutorial requires that the password reset bot is running</span></span>

    npm run demo-password

### <a name="open-the-demo"></a><span data-ttu-id="f7a79-111">Open the demo</span><span class="sxs-lookup"><span data-stu-id="f7a79-111">Open the demo</span></span>

<span data-ttu-id="f7a79-112">In the Model list of the web UI, click on Tutorial Demo Password Reset.</span><span class="sxs-lookup"><span data-stu-id="f7a79-112">In the Model list of the web UI, click on Tutorial Demo Password Reset.</span></span> 

### <a name="actions"></a><span data-ttu-id="f7a79-113">Actions</span><span class="sxs-lookup"><span data-stu-id="f7a79-113">Actions</span></span>

<span data-ttu-id="f7a79-114">We have created set of actions where the user is looking for help with their password including solutions.</span><span class="sxs-lookup"><span data-stu-id="f7a79-114">We have created set of actions where the user is looking for help with their password including solutions.</span></span>

![](../media/tutorial_pw_reset_actions.PNG)

### <a name="training-dialogs"></a><span data-ttu-id="f7a79-115">Training Dialogs</span><span class="sxs-lookup"><span data-stu-id="f7a79-115">Training Dialogs</span></span>

<span data-ttu-id="f7a79-116">There are a number of training dialogs.</span><span class="sxs-lookup"><span data-stu-id="f7a79-116">There are a number of training dialogs.</span></span> <span data-ttu-id="f7a79-117">There are also demonstrations of an out of domain class -- for example, user requests like 'driving directions' are out of domain; the bot has been given examples of a few out of domain requests and can respond with 'I can't help with that.'</span><span class="sxs-lookup"><span data-stu-id="f7a79-117">There are also demonstrations of an out of domain class -- for example, user requests like 'driving directions' are out of domain; the bot has been given examples of a few out of domain requests and can respond with 'I can't help with that.'</span></span>

![](../media/tutorial_pw_reset_entities.PNG)

<span data-ttu-id="f7a79-118">As an example, let's try a teaching session.</span><span class="sxs-lookup"><span data-stu-id="f7a79-118">As an example, let's try a teaching session.</span></span>

1. <span data-ttu-id="f7a79-119">Click Train Dialogs, then New Train Dialog.</span><span class="sxs-lookup"><span data-stu-id="f7a79-119">Click Train Dialogs, then New Train Dialog.</span></span>
1. <span data-ttu-id="f7a79-120">Enter 'I lost my password'.</span><span class="sxs-lookup"><span data-stu-id="f7a79-120">Enter 'I lost my password'.</span></span>
2. <span data-ttu-id="f7a79-121">Click Score Action.</span><span class="sxs-lookup"><span data-stu-id="f7a79-121">Click Score Action.</span></span>
3. <span data-ttu-id="f7a79-122">Click to Select 'Is that for your local account or Microsoft account?'</span><span class="sxs-lookup"><span data-stu-id="f7a79-122">Click to Select 'Is that for your local account or Microsoft account?'</span></span>
4. <span data-ttu-id="f7a79-123">Enter 'Local account'.</span><span class="sxs-lookup"><span data-stu-id="f7a79-123">Enter 'Local account'.</span></span>
5. <span data-ttu-id="f7a79-124">Click Score Actions.</span><span class="sxs-lookup"><span data-stu-id="f7a79-124">Click Score Actions.</span></span>
3. <span data-ttu-id="f7a79-125">Click to Select 'Which version of Windows do you have?'</span><span class="sxs-lookup"><span data-stu-id="f7a79-125">Click to Select 'Which version of Windows do you have?'</span></span>
4. <span data-ttu-id="f7a79-126">Enter 'Windows 8'.</span><span class="sxs-lookup"><span data-stu-id="f7a79-126">Enter 'Windows 8'.</span></span>
5. <span data-ttu-id="f7a79-127">click Score Actions.</span><span class="sxs-lookup"><span data-stu-id="f7a79-127">click Score Actions.</span></span>
6. <span data-ttu-id="f7a79-128">Select 'SOLUTION: how to reset password on Windows 8.'</span><span class="sxs-lookup"><span data-stu-id="f7a79-128">Select 'SOLUTION: how to reset password on Windows 8.'</span></span>
4. <span data-ttu-id="f7a79-129">Click Done Teaching.</span><span class="sxs-lookup"><span data-stu-id="f7a79-129">Click Done Teaching.</span></span>

<span data-ttu-id="f7a79-130">Let's try how the bot can learn an out-of-domain class.</span><span class="sxs-lookup"><span data-stu-id="f7a79-130">Let's try how the bot can learn an out-of-domain class.</span></span>

1. <span data-ttu-id="f7a79-131">Click Train Dialogs, then New Train Dialog.</span><span class="sxs-lookup"><span data-stu-id="f7a79-131">Click Train Dialogs, then New Train Dialog.</span></span>
1. <span data-ttu-id="f7a79-132">Enter 'web search'.</span><span class="sxs-lookup"><span data-stu-id="f7a79-132">Enter 'web search'.</span></span>
    - <span data-ttu-id="f7a79-133">This is an example of out-of-domain class.</span><span class="sxs-lookup"><span data-stu-id="f7a79-133">This is an example of out-of-domain class.</span></span> 
2. <span data-ttu-id="f7a79-134">Click Score Action.</span><span class="sxs-lookup"><span data-stu-id="f7a79-134">Click Score Action.</span></span>
3. <span data-ttu-id="f7a79-135">Click to Select 'Sorry, I can't help with that.'</span><span class="sxs-lookup"><span data-stu-id="f7a79-135">Click to Select 'Sorry, I can't help with that.'</span></span>
    - <span data-ttu-id="f7a79-136">Notice the score for this option is currently low.</span><span class="sxs-lookup"><span data-stu-id="f7a79-136">Notice the score for this option is currently low.</span></span> <span data-ttu-id="f7a79-137">But after a little more teaching, the score will get higher.</span><span class="sxs-lookup"><span data-stu-id="f7a79-137">But after a little more teaching, the score will get higher.</span></span>
4. <span data-ttu-id="f7a79-138">Click Done Teaching.</span><span class="sxs-lookup"><span data-stu-id="f7a79-138">Click Done Teaching.</span></span>

<span data-ttu-id="f7a79-139">You have now seen how to create a basic technical support demo, and how it can learn to provide solutions, and also handle out of sample queries.</span><span class="sxs-lookup"><span data-stu-id="f7a79-139">You have now seen how to create a basic technical support demo, and how it can learn to provide solutions, and also handle out of sample queries.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f7a79-140">Next steps</span><span class="sxs-lookup"><span data-stu-id="f7a79-140">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f7a79-141">Demo - pizza order</span><span class="sxs-lookup"><span data-stu-id="f7a79-141">Demo - pizza order</span></span>](./demo-pizza-order.md)
