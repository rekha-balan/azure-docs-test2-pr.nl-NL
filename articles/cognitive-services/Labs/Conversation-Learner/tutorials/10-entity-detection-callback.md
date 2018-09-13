---
title: How to use entity detection callback with a Conversation Learner model - Microsoft Cognitive Services | Microsoft Docs
titleSuffix: Azure
description: Learn how to use entity detection callback with a Conversation Learner model.
services: cognitive-services
author: v-jaswel
manager: nolachar
ms.service: cognitive-services
ms.component: conversation-learner
ms.topic: article
ms.date: 04/30/2018
ms.author: v-jaswel
ms.openlocfilehash: f168018a23d03ffb957da2dd1f67881420a21208
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867601"
---
# <a name="how-to-use-entity-detection-callback"></a><span data-ttu-id="e3b15-103">How to use entity detection callback</span><span class="sxs-lookup"><span data-stu-id="e3b15-103">How to use entity detection callback</span></span>

<span data-ttu-id="e3b15-104">This tutorial shows the entity detection callback, and illustrates a common pattern for resolving entities.</span><span class="sxs-lookup"><span data-stu-id="e3b15-104">This tutorial shows the entity detection callback, and illustrates a common pattern for resolving entities.</span></span>

## <a name="video"></a><span data-ttu-id="e3b15-105">Video</span><span class="sxs-lookup"><span data-stu-id="e3b15-105">Video</span></span>

<span data-ttu-id="e3b15-106">[![Tutorial 10 Preview](http://aka.ms/cl-tutorial-10-preview)](http://aka.ms/blis-tutorial-10)</span><span class="sxs-lookup"><span data-stu-id="e3b15-106">[![Tutorial 10 Preview](http://aka.ms/cl-tutorial-10-preview)](http://aka.ms/blis-tutorial-10)</span></span>

## <a name="requirements"></a><span data-ttu-id="e3b15-107">Requirements</span><span class="sxs-lookup"><span data-stu-id="e3b15-107">Requirements</span></span>
<span data-ttu-id="e3b15-108">This tutorial requires that the `tutorialEntityDetectionCallback` bot is running.</span><span class="sxs-lookup"><span data-stu-id="e3b15-108">This tutorial requires that the `tutorialEntityDetectionCallback` bot is running.</span></span>

    npm run tutorial-entity-detection

## <a name="details"></a><span data-ttu-id="e3b15-109">Details</span><span class="sxs-lookup"><span data-stu-id="e3b15-109">Details</span></span>
<span data-ttu-id="e3b15-110">Entity detection callback enables using custom code to handle business rules related to entities.</span><span class="sxs-lookup"><span data-stu-id="e3b15-110">Entity detection callback enables using custom code to handle business rules related to entities.</span></span> <span data-ttu-id="e3b15-111">This demo uses callbacks and Programmatic Entities to resolve the city name entered by the user to a canonical name -- for example, resolving "the big apple" to "new york".</span><span class="sxs-lookup"><span data-stu-id="e3b15-111">This demo uses callbacks and Programmatic Entities to resolve the city name entered by the user to a canonical name -- for example, resolving "the big apple" to "new york".</span></span>

### <a name="open-the-demo"></a><span data-ttu-id="e3b15-112">Open the demo</span><span class="sxs-lookup"><span data-stu-id="e3b15-112">Open the demo</span></span>

<span data-ttu-id="e3b15-113">In the model list, click on Tutorial-10-EntityDetectionCallback.</span><span class="sxs-lookup"><span data-stu-id="e3b15-113">In the model list, click on Tutorial-10-EntityDetectionCallback.</span></span> 

### <a name="entities"></a><span data-ttu-id="e3b15-114">Entities</span><span class="sxs-lookup"><span data-stu-id="e3b15-114">Entities</span></span>

<span data-ttu-id="e3b15-115">Three entities are defined in the model.</span><span class="sxs-lookup"><span data-stu-id="e3b15-115">Three entities are defined in the model.</span></span>

![](../media/tutorial10_entities.PNG)

1. <span data-ttu-id="e3b15-116">City is a custom entity that the user will provide as text input.</span><span class="sxs-lookup"><span data-stu-id="e3b15-116">City is a custom entity that the user will provide as text input.</span></span>
2. <span data-ttu-id="e3b15-117">CityUnknown is a Programmatic Entity.</span><span class="sxs-lookup"><span data-stu-id="e3b15-117">CityUnknown is a Programmatic Entity.</span></span> <span data-ttu-id="e3b15-118">This entity will get populated by the system.</span><span class="sxs-lookup"><span data-stu-id="e3b15-118">This entity will get populated by the system.</span></span> <span data-ttu-id="e3b15-119">It will copy the user input if the system does not know which city it is.</span><span class="sxs-lookup"><span data-stu-id="e3b15-119">It will copy the user input if the system does not know which city it is.</span></span>
3. <span data-ttu-id="e3b15-120">CityResolved is the city that the system does know about.</span><span class="sxs-lookup"><span data-stu-id="e3b15-120">CityResolved is the city that the system does know about.</span></span> <span data-ttu-id="e3b15-121">This entity will be city's canonical name for example 'the big apple' will resolve to 'new york'.</span><span class="sxs-lookup"><span data-stu-id="e3b15-121">This entity will be city's canonical name for example 'the big apple' will resolve to 'new york'.</span></span>

### <a name="actions"></a><span data-ttu-id="e3b15-122">Actions</span><span class="sxs-lookup"><span data-stu-id="e3b15-122">Actions</span></span>

<span data-ttu-id="e3b15-123">Three actions are defined in the model.</span><span class="sxs-lookup"><span data-stu-id="e3b15-123">Three actions are defined in the model.</span></span>

![](../media/tutorial10_actions.PNG)

1. <span data-ttu-id="e3b15-124">The first action is 'Which city do you want?'</span><span class="sxs-lookup"><span data-stu-id="e3b15-124">The first action is 'Which city do you want?'</span></span>
2. <span data-ttu-id="e3b15-125">The second is 'I don't know this city, $CityUknown.</span><span class="sxs-lookup"><span data-stu-id="e3b15-125">The second is 'I don't know this city, $CityUknown.</span></span> <span data-ttu-id="e3b15-126">Which city do you want?'</span><span class="sxs-lookup"><span data-stu-id="e3b15-126">Which city do you want?'</span></span>
3. <span data-ttu-id="e3b15-127">The third is 'You said $City, and I resolved that to $CityResolved.'</span><span class="sxs-lookup"><span data-stu-id="e3b15-127">The third is 'You said $City, and I resolved that to $CityResolved.'</span></span>

### <a name="callback-code"></a><span data-ttu-id="e3b15-128">Callback code</span><span class="sxs-lookup"><span data-stu-id="e3b15-128">Callback code</span></span>

<span data-ttu-id="e3b15-129">Let's look at the code.</span><span class="sxs-lookup"><span data-stu-id="e3b15-129">Let's look at the code.</span></span> <span data-ttu-id="e3b15-130">You can find the EntityDetectionCallback method in the C:\<installedpath>\src\demos\tutorialSessionCallbacks.ts file.</span><span class="sxs-lookup"><span data-stu-id="e3b15-130">You can find the EntityDetectionCallback method in the C:\<installedpath>\src\demos\tutorialSessionCallbacks.ts file.</span></span>

![](../media/tutorial10_callbackcode.PNG)

<span data-ttu-id="e3b15-131">This function gets called after entity resolution has occurred.</span><span class="sxs-lookup"><span data-stu-id="e3b15-131">This function gets called after entity resolution has occurred.</span></span>
 
- <span data-ttu-id="e3b15-132">The first thing it will do is clear $CityUknown.</span><span class="sxs-lookup"><span data-stu-id="e3b15-132">The first thing it will do is clear $CityUknown.</span></span> <span data-ttu-id="e3b15-133">$CityUknown will only persist for a single turn as it always gets cleared at the beginning.</span><span class="sxs-lookup"><span data-stu-id="e3b15-133">$CityUknown will only persist for a single turn as it always gets cleared at the beginning.</span></span>
- <span data-ttu-id="e3b15-134">Then, get the list of cities that have been recognized.</span><span class="sxs-lookup"><span data-stu-id="e3b15-134">Then, get the list of cities that have been recognized.</span></span> <span data-ttu-id="e3b15-135">Take the first one, and attempt to resolve it.</span><span class="sxs-lookup"><span data-stu-id="e3b15-135">Take the first one, and attempt to resolve it.</span></span>
- <span data-ttu-id="e3b15-136">The function that resolves it (resolveCity) is defined further above in the code.</span><span class="sxs-lookup"><span data-stu-id="e3b15-136">The function that resolves it (resolveCity) is defined further above in the code.</span></span> <span data-ttu-id="e3b15-137">It has a list of canonical city names.</span><span class="sxs-lookup"><span data-stu-id="e3b15-137">It has a list of canonical city names.</span></span> <span data-ttu-id="e3b15-138">It finds the city name in the list, it returns it.</span><span class="sxs-lookup"><span data-stu-id="e3b15-138">It finds the city name in the list, it returns it.</span></span> <span data-ttu-id="e3b15-139">Else, it looks in 'cityMap' and returns the mapped name.</span><span class="sxs-lookup"><span data-stu-id="e3b15-139">Else, it looks in 'cityMap' and returns the mapped name.</span></span> <span data-ttu-id="e3b15-140">If it cannot find a city, it returns null.</span><span class="sxs-lookup"><span data-stu-id="e3b15-140">If it cannot find a city, it returns null.</span></span>
- <span data-ttu-id="e3b15-141">Finally, if the city has resolved to a name, we store it in $CityKnown entity.</span><span class="sxs-lookup"><span data-stu-id="e3b15-141">Finally, if the city has resolved to a name, we store it in $CityKnown entity.</span></span> <span data-ttu-id="e3b15-142">Else, clear what the user has said and populate $CityUknown entity.</span><span class="sxs-lookup"><span data-stu-id="e3b15-142">Else, clear what the user has said and populate $CityUknown entity.</span></span>

### <a name="train-dialogs"></a><span data-ttu-id="e3b15-143">Train Dialogs</span><span class="sxs-lookup"><span data-stu-id="e3b15-143">Train Dialogs</span></span>

1. <span data-ttu-id="e3b15-144">Click Train Dialogs, then New Train Dialog.</span><span class="sxs-lookup"><span data-stu-id="e3b15-144">Click Train Dialogs, then New Train Dialog.</span></span>
2. <span data-ttu-id="e3b15-145">Type 'hello'.</span><span class="sxs-lookup"><span data-stu-id="e3b15-145">Type 'hello'.</span></span>
3. <span data-ttu-id="e3b15-146">Click Score Actions, and Select 'Which city do you want?'</span><span class="sxs-lookup"><span data-stu-id="e3b15-146">Click Score Actions, and Select 'Which city do you want?'</span></span>
2. <span data-ttu-id="e3b15-147">Enter 'new york'.</span><span class="sxs-lookup"><span data-stu-id="e3b15-147">Enter 'new york'.</span></span>
    - <span data-ttu-id="e3b15-148">The text is recognized as a city entity.</span><span class="sxs-lookup"><span data-stu-id="e3b15-148">The text is recognized as a city entity.</span></span>
5. <span data-ttu-id="e3b15-149">Click Score Actions</span><span class="sxs-lookup"><span data-stu-id="e3b15-149">Click Score Actions</span></span>
    - <span data-ttu-id="e3b15-150">`City` and `CityResolved` have been populated.</span><span class="sxs-lookup"><span data-stu-id="e3b15-150">`City` and `CityResolved` have been populated.</span></span>
6. <span data-ttu-id="e3b15-151">Select 'You said $City, and I resolved that to $CityResolved'.</span><span class="sxs-lookup"><span data-stu-id="e3b15-151">Select 'You said $City, and I resolved that to $CityResolved'.</span></span>
7. <span data-ttu-id="e3b15-152">Click Done Teaching.</span><span class="sxs-lookup"><span data-stu-id="e3b15-152">Click Done Teaching.</span></span>

<span data-ttu-id="e3b15-153">Add another example dialog:</span><span class="sxs-lookup"><span data-stu-id="e3b15-153">Add another example dialog:</span></span>

1. <span data-ttu-id="e3b15-154">Click New Train Dialog.</span><span class="sxs-lookup"><span data-stu-id="e3b15-154">Click New Train Dialog.</span></span>
2. <span data-ttu-id="e3b15-155">Type 'hello'.</span><span class="sxs-lookup"><span data-stu-id="e3b15-155">Type 'hello'.</span></span>
3. <span data-ttu-id="e3b15-156">Click Score Actions, and Select 'Which city do you want?'</span><span class="sxs-lookup"><span data-stu-id="e3b15-156">Click Score Actions, and Select 'Which city do you want?'</span></span>
2. <span data-ttu-id="e3b15-157">Enter 'big apple'.</span><span class="sxs-lookup"><span data-stu-id="e3b15-157">Enter 'big apple'.</span></span>
    - <span data-ttu-id="e3b15-158">The text is recognized as a city entity.</span><span class="sxs-lookup"><span data-stu-id="e3b15-158">The text is recognized as a city entity.</span></span>
5. <span data-ttu-id="e3b15-159">Click Score Actions</span><span class="sxs-lookup"><span data-stu-id="e3b15-159">Click Score Actions</span></span>
    - <span data-ttu-id="e3b15-160">`CityResolved` shows the effect of code running.</span><span class="sxs-lookup"><span data-stu-id="e3b15-160">`CityResolved` shows the effect of code running.</span></span>
6. <span data-ttu-id="e3b15-161">Select 'You said $City, and I resolved that to $CityResolved'.</span><span class="sxs-lookup"><span data-stu-id="e3b15-161">Select 'You said $City, and I resolved that to $CityResolved'.</span></span>
7. <span data-ttu-id="e3b15-162">Click Done Teaching.</span><span class="sxs-lookup"><span data-stu-id="e3b15-162">Click Done Teaching.</span></span>

<span data-ttu-id="e3b15-163">Add another example dialog:</span><span class="sxs-lookup"><span data-stu-id="e3b15-163">Add another example dialog:</span></span>

1. <span data-ttu-id="e3b15-164">Click New Train Dialog.</span><span class="sxs-lookup"><span data-stu-id="e3b15-164">Click New Train Dialog.</span></span>
2. <span data-ttu-id="e3b15-165">Type 'hello'.</span><span class="sxs-lookup"><span data-stu-id="e3b15-165">Type 'hello'.</span></span>
3. <span data-ttu-id="e3b15-166">Click Score Actions, and Select 'Which city do you want?'</span><span class="sxs-lookup"><span data-stu-id="e3b15-166">Click Score Actions, and Select 'Which city do you want?'</span></span>
2. <span data-ttu-id="e3b15-167">Enter 'foo'.</span><span class="sxs-lookup"><span data-stu-id="e3b15-167">Enter 'foo'.</span></span>
    - <span data-ttu-id="e3b15-168">This is an example of a city the system does not know.</span><span class="sxs-lookup"><span data-stu-id="e3b15-168">This is an example of a city the system does not know.</span></span> 
5. <span data-ttu-id="e3b15-169">Click Score Actions</span><span class="sxs-lookup"><span data-stu-id="e3b15-169">Click Score Actions</span></span>
6. <span data-ttu-id="e3b15-170">Select 'I don't know this city, $CityUknown.</span><span class="sxs-lookup"><span data-stu-id="e3b15-170">Select 'I don't know this city, $CityUknown.</span></span> <span data-ttu-id="e3b15-171">Which city do you want?'.</span><span class="sxs-lookup"><span data-stu-id="e3b15-171">Which city do you want?'.</span></span>
7. <span data-ttu-id="e3b15-172">Enter 'new york'.</span><span class="sxs-lookup"><span data-stu-id="e3b15-172">Enter 'new york'.</span></span>
8. <span data-ttu-id="e3b15-173">Click Score Actions.</span><span class="sxs-lookup"><span data-stu-id="e3b15-173">Click Score Actions.</span></span>
    - <span data-ttu-id="e3b15-174">`CityUknown` has been cleared, and `CityResolved` is populated.</span><span class="sxs-lookup"><span data-stu-id="e3b15-174">`CityUknown` has been cleared, and `CityResolved` is populated.</span></span>
6. <span data-ttu-id="e3b15-175">Select 'You said $City, and I resolved that to $CityResolved'.</span><span class="sxs-lookup"><span data-stu-id="e3b15-175">Select 'You said $City, and I resolved that to $CityResolved'.</span></span>
7. <span data-ttu-id="e3b15-176">Click Done Teaching.</span><span class="sxs-lookup"><span data-stu-id="e3b15-176">Click Done Teaching.</span></span>

![](../media/tutorial10_bigapple.PNG)

## <a name="next-steps"></a><span data-ttu-id="e3b15-177">Next steps</span><span class="sxs-lookup"><span data-stu-id="e3b15-177">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e3b15-178">Session callbacks</span><span class="sxs-lookup"><span data-stu-id="e3b15-178">Session callbacks</span></span>](./11-session-callbacks.md)
