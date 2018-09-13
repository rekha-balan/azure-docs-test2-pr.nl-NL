---
title: How to use branching and undo operations with a Conversation Learner model - Microsoft Cognitive Services | Microsoft Docs
titleSuffix: Azure
description: Learn how to use branching and undo operations with a Conversation Learner model.
services: cognitive-services
author: v-jaswel
manager: nolachar
ms.service: cognitive-services
ms.component: conversation-learner
ms.topic: article
ms.date: 04/30/2018
ms.author: v-jaswel
ms.openlocfilehash: 05140693026e21a73b756ed0ea7bc9936bef067e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864359"
---
# <a name="how-to-use-branching-and-undo-operations"></a><span data-ttu-id="78dfe-103">How to use branching and undo operations</span><span class="sxs-lookup"><span data-stu-id="78dfe-103">How to use branching and undo operations</span></span>
<span data-ttu-id="78dfe-104">In this tutorial, we will go over undo and branching operations.</span><span class="sxs-lookup"><span data-stu-id="78dfe-104">In this tutorial, we will go over undo and branching operations.</span></span>


## <a name="details"></a><span data-ttu-id="78dfe-105">Details</span><span class="sxs-lookup"><span data-stu-id="78dfe-105">Details</span></span>
- <span data-ttu-id="78dfe-106">Undo: allows the developer to “undo” a user input or action choice.</span><span class="sxs-lookup"><span data-stu-id="78dfe-106">Undo: allows the developer to “undo” a user input or action choice.</span></span> <span data-ttu-id="78dfe-107">Behind the scenes, “undo” actually creates a new dialog and re-plays it up to the previous step.</span><span class="sxs-lookup"><span data-stu-id="78dfe-107">Behind the scenes, “undo” actually creates a new dialog and re-plays it up to the previous step.</span></span>  <span data-ttu-id="78dfe-108">This means that the entity detection callback and API calls in the dialog will be called again.</span><span class="sxs-lookup"><span data-stu-id="78dfe-108">This means that the entity detection callback and API calls in the dialog will be called again.</span></span>

- <span data-ttu-id="78dfe-109">Branch: creates a new train dialog which begins in the same way as an existing train dialog – this saves the effort of manually re-entering dialog turns.</span><span class="sxs-lookup"><span data-stu-id="78dfe-109">Branch: creates a new train dialog which begins in the same way as an existing train dialog – this saves the effort of manually re-entering dialog turns.</span></span> <span data-ttu-id="78dfe-110">Behind the scenes, “branch” creates a new dialog and re-plays the existing train dialog up to the selected step.</span><span class="sxs-lookup"><span data-stu-id="78dfe-110">Behind the scenes, “branch” creates a new dialog and re-plays the existing train dialog up to the selected step.</span></span>  <span data-ttu-id="78dfe-111">This means that the entity detection callback and API calls in the dialog will be called again.</span><span class="sxs-lookup"><span data-stu-id="78dfe-111">This means that the entity detection callback and API calls in the dialog will be called again.</span></span>


## <a name="requirements"></a><span data-ttu-id="78dfe-112">Requirements</span><span class="sxs-lookup"><span data-stu-id="78dfe-112">Requirements</span></span>
<span data-ttu-id="78dfe-113">This tutorial requires that the pizza order bot is running:</span><span class="sxs-lookup"><span data-stu-id="78dfe-113">This tutorial requires that the pizza order bot is running:</span></span>

    npm run demo-pizza

### <a name="open-the-demo"></a><span data-ttu-id="78dfe-114">Open the demo</span><span class="sxs-lookup"><span data-stu-id="78dfe-114">Open the demo</span></span>

<span data-ttu-id="78dfe-115">In the Model list of the web UI, click on TutorialDemo Pizza Order.</span><span class="sxs-lookup"><span data-stu-id="78dfe-115">In the Model list of the web UI, click on TutorialDemo Pizza Order.</span></span> 

<span data-ttu-id="78dfe-116">For details on the Pizza Order demo, see the Pizza order tutorial.</span><span class="sxs-lookup"><span data-stu-id="78dfe-116">For details on the Pizza Order demo, see the Pizza order tutorial.</span></span>

## <a name="undo"></a><span data-ttu-id="78dfe-117">Undo</span><span class="sxs-lookup"><span data-stu-id="78dfe-117">Undo</span></span>

<span data-ttu-id="78dfe-118">We will undo part of the dialog, and recreate it from that step.</span><span class="sxs-lookup"><span data-stu-id="78dfe-118">We will undo part of the dialog, and recreate it from that step.</span></span>

### <a name="training-dialogs"></a><span data-ttu-id="78dfe-119">Training Dialogs</span><span class="sxs-lookup"><span data-stu-id="78dfe-119">Training Dialogs</span></span>
<span data-ttu-id="78dfe-120">Let's start a training session.</span><span class="sxs-lookup"><span data-stu-id="78dfe-120">Let's start a training session.</span></span> 

1. <span data-ttu-id="78dfe-121">Click Train Dialogs, then New Train Dialog.</span><span class="sxs-lookup"><span data-stu-id="78dfe-121">Click Train Dialogs, then New Train Dialog.</span></span>
1. <span data-ttu-id="78dfe-122">Enter 'order a pizza'.</span><span class="sxs-lookup"><span data-stu-id="78dfe-122">Enter 'order a pizza'.</span></span>
2. <span data-ttu-id="78dfe-123">Click Score Action.</span><span class="sxs-lookup"><span data-stu-id="78dfe-123">Click Score Action.</span></span>
3. <span data-ttu-id="78dfe-124">Click to Select 'what would you like on your pizza?'</span><span class="sxs-lookup"><span data-stu-id="78dfe-124">Click to Select 'what would you like on your pizza?'</span></span>
4. <span data-ttu-id="78dfe-125">Enter 'mushrooms and cheese'.</span><span class="sxs-lookup"><span data-stu-id="78dfe-125">Enter 'mushrooms and cheese'.</span></span>
5. <span data-ttu-id="78dfe-126">Click Score Actions.</span><span class="sxs-lookup"><span data-stu-id="78dfe-126">Click Score Actions.</span></span>
3. <span data-ttu-id="78dfe-127">Click to Select 'you have $Toppings on your pizza'.</span><span class="sxs-lookup"><span data-stu-id="78dfe-127">Click to Select 'you have $Toppings on your pizza'.</span></span>
6. <span data-ttu-id="78dfe-128">Select 'Would you like anything else?'</span><span class="sxs-lookup"><span data-stu-id="78dfe-128">Select 'Would you like anything else?'</span></span>
7. <span data-ttu-id="78dfe-129">Enter 'remove mushrooms and add peppers'.</span><span class="sxs-lookup"><span data-stu-id="78dfe-129">Enter 'remove mushrooms and add peppers'.</span></span>
    - <span data-ttu-id="78dfe-130">Select mushrooms and un-check the Toppings entity.</span><span class="sxs-lookup"><span data-stu-id="78dfe-130">Select mushrooms and un-check the Toppings entity.</span></span> <span data-ttu-id="78dfe-131">We are creating an action that we will undo.</span><span class="sxs-lookup"><span data-stu-id="78dfe-131">We are creating an action that we will undo.</span></span>
2. <span data-ttu-id="78dfe-132">Click Undo Step.</span><span class="sxs-lookup"><span data-stu-id="78dfe-132">Click Undo Step.</span></span>
    - <span data-ttu-id="78dfe-133">The last entry is removed, and we are back at 'Would you like anything else?'</span><span class="sxs-lookup"><span data-stu-id="78dfe-133">The last entry is removed, and we are back at 'Would you like anything else?'</span></span>  <span data-ttu-id="78dfe-134">(screenshot below)</span><span class="sxs-lookup"><span data-stu-id="78dfe-134">(screenshot below)</span></span>
2. <span data-ttu-id="78dfe-135">Enter 'remove mushrooms and add peppers'.</span><span class="sxs-lookup"><span data-stu-id="78dfe-135">Enter 'remove mushrooms and add peppers'.</span></span>
8. <span data-ttu-id="78dfe-136">Click to Select 'you have $Toppings on your pizza'</span><span class="sxs-lookup"><span data-stu-id="78dfe-136">Click to Select 'you have $Toppings on your pizza'</span></span>
    - <span data-ttu-id="78dfe-137">Make sure both entities are selected correctly.</span><span class="sxs-lookup"><span data-stu-id="78dfe-137">Make sure both entities are selected correctly.</span></span>
2. <span data-ttu-id="78dfe-138">Click Score Action.</span><span class="sxs-lookup"><span data-stu-id="78dfe-138">Click Score Action.</span></span> <span data-ttu-id="78dfe-139">You can continue with the corrected dialog now.</span><span class="sxs-lookup"><span data-stu-id="78dfe-139">You can continue with the corrected dialog now.</span></span>
4. <span data-ttu-id="78dfe-140">Click Done Teaching.</span><span class="sxs-lookup"><span data-stu-id="78dfe-140">Click Done Teaching.</span></span>

<span data-ttu-id="78dfe-141">You have now seen how to use undo to remove a user input and action.</span><span class="sxs-lookup"><span data-stu-id="78dfe-141">You have now seen how to use undo to remove a user input and action.</span></span>

![](../media/tutorial15_undo.PNG)

## <a name="branch"></a><span data-ttu-id="78dfe-142">Branch</span><span class="sxs-lookup"><span data-stu-id="78dfe-142">Branch</span></span>

<span data-ttu-id="78dfe-143">As an example, let's open an existing train dialog, and create another train dialog by branching.</span><span class="sxs-lookup"><span data-stu-id="78dfe-143">As an example, let's open an existing train dialog, and create another train dialog by branching.</span></span>

1. <span data-ttu-id="78dfe-144">Click Train Dialogs, then 'new order' to open the existing dialog.</span><span class="sxs-lookup"><span data-stu-id="78dfe-144">Click Train Dialogs, then 'new order' to open the existing dialog.</span></span> 
2. <span data-ttu-id="78dfe-145">Click on the last 'no' in the dialog (see screenshot below).</span><span class="sxs-lookup"><span data-stu-id="78dfe-145">Click on the last 'no' in the dialog (see screenshot below).</span></span>
3. <span data-ttu-id="78dfe-146">Click Branch.</span><span class="sxs-lookup"><span data-stu-id="78dfe-146">Click Branch.</span></span>
    - <span data-ttu-id="78dfe-147">'no' gets removed, and the entire dialog up to that point is copied into a new one.</span><span class="sxs-lookup"><span data-stu-id="78dfe-147">'no' gets removed, and the entire dialog up to that point is copied into a new one.</span></span> 
    - <span data-ttu-id="78dfe-148">This saves you re-entering the preceding turns to explore a new "branch" from this point.</span><span class="sxs-lookup"><span data-stu-id="78dfe-148">This saves you re-entering the preceding turns to explore a new "branch" from this point.</span></span>
1. <span data-ttu-id="78dfe-149">Enter 'yes'.</span><span class="sxs-lookup"><span data-stu-id="78dfe-149">Enter 'yes'.</span></span>
2. <span data-ttu-id="78dfe-150">Click Score Action.</span><span class="sxs-lookup"><span data-stu-id="78dfe-150">Click Score Action.</span></span>
3. <span data-ttu-id="78dfe-151">Select 'You have $Toppings on your pizza'.</span><span class="sxs-lookup"><span data-stu-id="78dfe-151">Select 'You have $Toppings on your pizza'.</span></span>
6. <span data-ttu-id="78dfe-152">Select 'Would you like anything else?'</span><span class="sxs-lookup"><span data-stu-id="78dfe-152">Select 'Would you like anything else?'</span></span>
7. <span data-ttu-id="78dfe-153">Enter 'no'.</span><span class="sxs-lookup"><span data-stu-id="78dfe-153">Enter 'no'.</span></span>
4. <span data-ttu-id="78dfe-154">Click Done Teaching.</span><span class="sxs-lookup"><span data-stu-id="78dfe-154">Click Done Teaching.</span></span>

![](../media/tutorial15_branch.PNG)

## <a name="next-steps"></a><span data-ttu-id="78dfe-155">Next steps</span><span class="sxs-lookup"><span data-stu-id="78dfe-155">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="78dfe-156">Versioning and tagging</span><span class="sxs-lookup"><span data-stu-id="78dfe-156">Versioning and tagging</span></span>](./16-versioning-and-tagging.md)
