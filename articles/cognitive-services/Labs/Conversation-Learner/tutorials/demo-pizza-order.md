---
title: Demo Conversation Learner model, pizza order - Microsoft Cognitive Services | Microsoft Docs
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
ms.openlocfilehash: 052ef249f3367a562e5598b90533c0e52ed75df4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869745"
---
# <a name="demo-pizza-order"></a><span data-ttu-id="5c910-103">Demo: Pizza order</span><span class="sxs-lookup"><span data-stu-id="5c910-103">Demo: Pizza order</span></span>
<span data-ttu-id="5c910-104">This demo illustrates a pizza ordering bot.</span><span class="sxs-lookup"><span data-stu-id="5c910-104">This demo illustrates a pizza ordering bot.</span></span> <span data-ttu-id="5c910-105">It supports ordering of a single pizza with this functionality:</span><span class="sxs-lookup"><span data-stu-id="5c910-105">It supports ordering of a single pizza with this functionality:</span></span>

- <span data-ttu-id="5c910-106">recognizing pizza toppings in user utterances</span><span class="sxs-lookup"><span data-stu-id="5c910-106">recognizing pizza toppings in user utterances</span></span>
- <span data-ttu-id="5c910-107">checking if pizza toppings are in stock or out of stock, and responding appropriately</span><span class="sxs-lookup"><span data-stu-id="5c910-107">checking if pizza toppings are in stock or out of stock, and responding appropriately</span></span>
- <span data-ttu-id="5c910-108">remembering pizza toppings from a previous order, and offering to - start a new order with the same toppings</span><span class="sxs-lookup"><span data-stu-id="5c910-108">remembering pizza toppings from a previous order, and offering to - start a new order with the same toppings</span></span>

## <a name="video"></a><span data-ttu-id="5c910-109">Video</span><span class="sxs-lookup"><span data-stu-id="5c910-109">Video</span></span>

<span data-ttu-id="5c910-110">[![Demo Pizza Preview](http://aka.ms/cl-demo-pizza-preview)](http://aka.ms/blis-demo-pizza)</span><span class="sxs-lookup"><span data-stu-id="5c910-110">[![Demo Pizza Preview](http://aka.ms/cl-demo-pizza-preview)](http://aka.ms/blis-demo-pizza)</span></span>

## <a name="requirements"></a><span data-ttu-id="5c910-111">Requirements</span><span class="sxs-lookup"><span data-stu-id="5c910-111">Requirements</span></span>
<span data-ttu-id="5c910-112">This tutorial requires that the pizza order bot is running</span><span class="sxs-lookup"><span data-stu-id="5c910-112">This tutorial requires that the pizza order bot is running</span></span>

    npm run demo-pizza

### <a name="open-the-demo"></a><span data-ttu-id="5c910-113">Open the demo</span><span class="sxs-lookup"><span data-stu-id="5c910-113">Open the demo</span></span>

<span data-ttu-id="5c910-114">In the Model list of the web UI, click on TutorialDemo Pizza Order.</span><span class="sxs-lookup"><span data-stu-id="5c910-114">In the Model list of the web UI, click on TutorialDemo Pizza Order.</span></span> 

## <a name="entities"></a><span data-ttu-id="5c910-115">Entities</span><span class="sxs-lookup"><span data-stu-id="5c910-115">Entities</span></span>

<span data-ttu-id="5c910-116">You have created three entities.</span><span class="sxs-lookup"><span data-stu-id="5c910-116">You have created three entities.</span></span>

- <span data-ttu-id="5c910-117">Toppings: this entity will accumulate the toppings the user asked for.</span><span class="sxs-lookup"><span data-stu-id="5c910-117">Toppings: this entity will accumulate the toppings the user asked for.</span></span> <span data-ttu-id="5c910-118">It includes the valid toppings that are in stock.</span><span class="sxs-lookup"><span data-stu-id="5c910-118">It includes the valid toppings that are in stock.</span></span> <span data-ttu-id="5c910-119">It checks to see if a topping is in or out of stock.</span><span class="sxs-lookup"><span data-stu-id="5c910-119">It checks to see if a topping is in or out of stock.</span></span>
- <span data-ttu-id="5c910-120">OutofStock: this entity is used to communicate back to the user that their selected topping is not in stock.</span><span class="sxs-lookup"><span data-stu-id="5c910-120">OutofStock: this entity is used to communicate back to the user that their selected topping is not in stock.</span></span>
- <span data-ttu-id="5c910-121">LastToppings: once an order is placed, this entity is used to offer to the user the list of toppings on their order.</span><span class="sxs-lookup"><span data-stu-id="5c910-121">LastToppings: once an order is placed, this entity is used to offer to the user the list of toppings on their order.</span></span>

![](../media/tutorial_pizza_entities.PNG)

### <a name="actions"></a><span data-ttu-id="5c910-122">Actions</span><span class="sxs-lookup"><span data-stu-id="5c910-122">Actions</span></span>

<span data-ttu-id="5c910-123">You have created a set of actions including asking the user what they want on their pizza, telling them what they have added so far, and so on.</span><span class="sxs-lookup"><span data-stu-id="5c910-123">You have created a set of actions including asking the user what they want on their pizza, telling them what they have added so far, and so on.</span></span>

<span data-ttu-id="5c910-124">There are also two API calls:</span><span class="sxs-lookup"><span data-stu-id="5c910-124">There are also two API calls:</span></span>

- <span data-ttu-id="5c910-125">FinalizeOrder: to place the order for the pizza</span><span class="sxs-lookup"><span data-stu-id="5c910-125">FinalizeOrder: to place the order for the pizza</span></span>
- <span data-ttu-id="5c910-126">UseLastToppings: to migrate the toppings from previous order</span><span class="sxs-lookup"><span data-stu-id="5c910-126">UseLastToppings: to migrate the toppings from previous order</span></span> 

![](../media/tutorial_pizza_actions.PNG)

### <a name="training-dialogs"></a><span data-ttu-id="5c910-127">Training Dialogs</span><span class="sxs-lookup"><span data-stu-id="5c910-127">Training Dialogs</span></span>
<span data-ttu-id="5c910-128">You have defined a handful of training dialogs.</span><span class="sxs-lookup"><span data-stu-id="5c910-128">You have defined a handful of training dialogs.</span></span> 

![](../media/tutorial_pizza_dialogs.PNG)

<span data-ttu-id="5c910-129">As an example, let's try a teaching session.</span><span class="sxs-lookup"><span data-stu-id="5c910-129">As an example, let's try a teaching session.</span></span>

1. <span data-ttu-id="5c910-130">Click Train Dialogs, then New Train Dialog.</span><span class="sxs-lookup"><span data-stu-id="5c910-130">Click Train Dialogs, then New Train Dialog.</span></span>
1. <span data-ttu-id="5c910-131">Enter 'order a pizza'.</span><span class="sxs-lookup"><span data-stu-id="5c910-131">Enter 'order a pizza'.</span></span>
2. <span data-ttu-id="5c910-132">Click Score Action.</span><span class="sxs-lookup"><span data-stu-id="5c910-132">Click Score Action.</span></span>
3. <span data-ttu-id="5c910-133">Click to Select 'what would you like on your pizza?'</span><span class="sxs-lookup"><span data-stu-id="5c910-133">Click to Select 'what would you like on your pizza?'</span></span>
4. <span data-ttu-id="5c910-134">Enter 'mushrooms and cheese'.</span><span class="sxs-lookup"><span data-stu-id="5c910-134">Enter 'mushrooms and cheese'.</span></span>
    - <span data-ttu-id="5c910-135">Notice LUIS has labeled both as Toppings.</span><span class="sxs-lookup"><span data-stu-id="5c910-135">Notice LUIS has labeled both as Toppings.</span></span> <span data-ttu-id="5c910-136">If that was not correct, you could click to highlight, then correct it.</span><span class="sxs-lookup"><span data-stu-id="5c910-136">If that was not correct, you could click to highlight, then correct it.</span></span>
    - <span data-ttu-id="5c910-137">The '+' sign next to the entity means that it is being added to the set of toppings.</span><span class="sxs-lookup"><span data-stu-id="5c910-137">The '+' sign next to the entity means that it is being added to the set of toppings.</span></span>
5. <span data-ttu-id="5c910-138">Click Score Actions.</span><span class="sxs-lookup"><span data-stu-id="5c910-138">Click Score Actions.</span></span>
    - <span data-ttu-id="5c910-139">Notice `mushrooms` and `cheese` are not in the memory for Toppings.</span><span class="sxs-lookup"><span data-stu-id="5c910-139">Notice `mushrooms` and `cheese` are not in the memory for Toppings.</span></span>
3. <span data-ttu-id="5c910-140">Click to Select 'you have $Toppings on your pizza'</span><span class="sxs-lookup"><span data-stu-id="5c910-140">Click to Select 'you have $Toppings on your pizza'</span></span>
    - <span data-ttu-id="5c910-141">Notice this is a non-wait action so the bot will ask for the next action.</span><span class="sxs-lookup"><span data-stu-id="5c910-141">Notice this is a non-wait action so the bot will ask for the next action.</span></span>
6. <span data-ttu-id="5c910-142">Select 'Would you like anything else?'</span><span class="sxs-lookup"><span data-stu-id="5c910-142">Select 'Would you like anything else?'</span></span>
7. <span data-ttu-id="5c910-143">Enter 'remove mushrooms and add peppers'.</span><span class="sxs-lookup"><span data-stu-id="5c910-143">Enter 'remove mushrooms and add peppers'.</span></span>
    - <span data-ttu-id="5c910-144">Notice `mushroom` has a '-' sign next to it, for it to be removed.</span><span class="sxs-lookup"><span data-stu-id="5c910-144">Notice `mushroom` has a '-' sign next to it, for it to be removed.</span></span> <span data-ttu-id="5c910-145">And `peppers` has a '+' sign next to it, to add it to the toppings.</span><span class="sxs-lookup"><span data-stu-id="5c910-145">And `peppers` has a '+' sign next to it, to add it to the toppings.</span></span>
2. <span data-ttu-id="5c910-146">Click Score Action.</span><span class="sxs-lookup"><span data-stu-id="5c910-146">Click Score Action.</span></span>
    - <span data-ttu-id="5c910-147">Notice `peppers` is now in bold as it is new.</span><span class="sxs-lookup"><span data-stu-id="5c910-147">Notice `peppers` is now in bold as it is new.</span></span> <span data-ttu-id="5c910-148">And `mushrooms` has been crossed out.</span><span class="sxs-lookup"><span data-stu-id="5c910-148">And `mushrooms` has been crossed out.</span></span>
8. <span data-ttu-id="5c910-149">Click to Select 'you have $Toppings on your pizza'</span><span class="sxs-lookup"><span data-stu-id="5c910-149">Click to Select 'you have $Toppings on your pizza'</span></span>
6. <span data-ttu-id="5c910-150">Select 'Would you like anything else?'</span><span class="sxs-lookup"><span data-stu-id="5c910-150">Select 'Would you like anything else?'</span></span>
7. <span data-ttu-id="5c910-151">Enter 'add peas'.</span><span class="sxs-lookup"><span data-stu-id="5c910-151">Enter 'add peas'.</span></span>
    - <span data-ttu-id="5c910-152">`Peas` is an example of a topping which is out of stock.</span><span class="sxs-lookup"><span data-stu-id="5c910-152">`Peas` is an example of a topping which is out of stock.</span></span> <span data-ttu-id="5c910-153">It is still labeled as a topping.</span><span class="sxs-lookup"><span data-stu-id="5c910-153">It is still labeled as a topping.</span></span>
2. <span data-ttu-id="5c910-154">Click Score Action.</span><span class="sxs-lookup"><span data-stu-id="5c910-154">Click Score Action.</span></span>
    - <span data-ttu-id="5c910-155">`Peas` shows up as OutOfStock.</span><span class="sxs-lookup"><span data-stu-id="5c910-155">`Peas` shows up as OutOfStock.</span></span>
    - <span data-ttu-id="5c910-156">To see how this happened, open the code at `C:\<\installedpath>\src\demos\demoPizzaOrder.ts`.</span><span class="sxs-lookup"><span data-stu-id="5c910-156">To see how this happened, open the code at `C:\<\installedpath>\src\demos\demoPizzaOrder.ts`.</span></span> <span data-ttu-id="5c910-157">Look at the EntityDetectionCallback method.</span><span class="sxs-lookup"><span data-stu-id="5c910-157">Look at the EntityDetectionCallback method.</span></span> <span data-ttu-id="5c910-158">This method is called after each topping to see if it is in stock.</span><span class="sxs-lookup"><span data-stu-id="5c910-158">This method is called after each topping to see if it is in stock.</span></span> <span data-ttu-id="5c910-159">If not, it clears it from the set of toppings and adds to the OutOfStock entity.</span><span class="sxs-lookup"><span data-stu-id="5c910-159">If not, it clears it from the set of toppings and adds to the OutOfStock entity.</span></span> <span data-ttu-id="5c910-160">The inStock variable is defined above that method which has the list of in-stock toppings.</span><span class="sxs-lookup"><span data-stu-id="5c910-160">The inStock variable is defined above that method which has the list of in-stock toppings.</span></span>
6. <span data-ttu-id="5c910-161">Select 'We don't have $OutOfStock'.</span><span class="sxs-lookup"><span data-stu-id="5c910-161">Select 'We don't have $OutOfStock'.</span></span>
7. <span data-ttu-id="5c910-162">Select 'Would you like anything else?'</span><span class="sxs-lookup"><span data-stu-id="5c910-162">Select 'Would you like anything else?'</span></span>
8. <span data-ttu-id="5c910-163">Enter 'no'.</span><span class="sxs-lookup"><span data-stu-id="5c910-163">Enter 'no'.</span></span>
9. <span data-ttu-id="5c910-164">Click Score Action.</span><span class="sxs-lookup"><span data-stu-id="5c910-164">Click Score Action.</span></span>
10. <span data-ttu-id="5c910-165">Select 'FinalizeOrder' API call.</span><span class="sxs-lookup"><span data-stu-id="5c910-165">Select 'FinalizeOrder' API call.</span></span> 
    - <span data-ttu-id="5c910-166">This will call the 'FinalizeOrder' function defined in code.</span><span class="sxs-lookup"><span data-stu-id="5c910-166">This will call the 'FinalizeOrder' function defined in code.</span></span> <span data-ttu-id="5c910-167">This clears toppings, and returns 'your order is on its way'.</span><span class="sxs-lookup"><span data-stu-id="5c910-167">This clears toppings, and returns 'your order is on its way'.</span></span> 
2. <span data-ttu-id="5c910-168">Enter 'order another'.</span><span class="sxs-lookup"><span data-stu-id="5c910-168">Enter 'order another'.</span></span> <span data-ttu-id="5c910-169">We are starting a new order.</span><span class="sxs-lookup"><span data-stu-id="5c910-169">We are starting a new order.</span></span>
9. <span data-ttu-id="5c910-170">Click Score Action.</span><span class="sxs-lookup"><span data-stu-id="5c910-170">Click Score Action.</span></span>
    - <span data-ttu-id="5c910-171">'cheese' and 'peppers' are in the memory as toppings from the last order.</span><span class="sxs-lookup"><span data-stu-id="5c910-171">'cheese' and 'peppers' are in the memory as toppings from the last order.</span></span>
1. <span data-ttu-id="5c910-172">Select 'Would you like $LastToppings'.</span><span class="sxs-lookup"><span data-stu-id="5c910-172">Select 'Would you like $LastToppings'.</span></span>
2. <span data-ttu-id="5c910-173">Enter 'yes'</span><span class="sxs-lookup"><span data-stu-id="5c910-173">Enter 'yes'</span></span>
3. <span data-ttu-id="5c910-174">Click Score Action.</span><span class="sxs-lookup"><span data-stu-id="5c910-174">Click Score Action.</span></span>
    - <span data-ttu-id="5c910-175">The bot wants to take the UseLastToppings action.</span><span class="sxs-lookup"><span data-stu-id="5c910-175">The bot wants to take the UseLastToppings action.</span></span> <span data-ttu-id="5c910-176">That is the second of the two callback methods.</span><span class="sxs-lookup"><span data-stu-id="5c910-176">That is the second of the two callback methods.</span></span> <span data-ttu-id="5c910-177">It will copy the last order's toppings into toppings and clear last toppings.</span><span class="sxs-lookup"><span data-stu-id="5c910-177">It will copy the last order's toppings into toppings and clear last toppings.</span></span> <span data-ttu-id="5c910-178">This is a way of remembering the last order, and if the user says they want another pizza, providing those toppings as options.</span><span class="sxs-lookup"><span data-stu-id="5c910-178">This is a way of remembering the last order, and if the user says they want another pizza, providing those toppings as options.</span></span>
2. <span data-ttu-id="5c910-179">Click to Select 'you have $Toppings on your pizza'.</span><span class="sxs-lookup"><span data-stu-id="5c910-179">Click to Select 'you have $Toppings on your pizza'.</span></span>
3. <span data-ttu-id="5c910-180">Select 'Would you like anything else?'</span><span class="sxs-lookup"><span data-stu-id="5c910-180">Select 'Would you like anything else?'</span></span>
8. <span data-ttu-id="5c910-181">Enter 'no'.</span><span class="sxs-lookup"><span data-stu-id="5c910-181">Enter 'no'.</span></span>
4. <span data-ttu-id="5c910-182">Click Done Teaching.</span><span class="sxs-lookup"><span data-stu-id="5c910-182">Click Done Teaching.</span></span>

![](../media/tutorial_pizza_callbackcode.PNG)

![](../media/tutorial_pizza_apicalls.PNG)

## <a name="next-steps"></a><span data-ttu-id="5c910-183">Next steps</span><span class="sxs-lookup"><span data-stu-id="5c910-183">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="5c910-184">Demo - VR app launcher</span><span class="sxs-lookup"><span data-stu-id="5c910-184">Demo - VR app launcher</span></span>](./demo-vr-app-launcher.md)
