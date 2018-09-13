---
title: Demo Conversation Learner model, virtual reality app launcher - Microsoft Cognitive Services | Microsoft Docs
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
ms.openlocfilehash: 896ec007c03e30e5c20a5344430be040271bc00b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864893"
---
# <a name="demo-virtual-reality-app-launcher"></a><span data-ttu-id="80e61-103">Demo: Virtual reality app launcher</span><span class="sxs-lookup"><span data-stu-id="80e61-103">Demo: Virtual reality app launcher</span></span>

<span data-ttu-id="80e61-104">This demo illustrates a virtual reality model launcher, which supports commands such as "start Skype and put in on the wall."</span><span class="sxs-lookup"><span data-stu-id="80e61-104">This demo illustrates a virtual reality model launcher, which supports commands such as "start Skype and put in on the wall."</span></span> <span data-ttu-id="80e61-105">A user needs to say an app name and location in order to launch the app.</span><span class="sxs-lookup"><span data-stu-id="80e61-105">A user needs to say an app name and location in order to launch the app.</span></span> <span data-ttu-id="80e61-106">Model launching is handled by an API call.</span><span class="sxs-lookup"><span data-stu-id="80e61-106">Model launching is handled by an API call.</span></span> <span data-ttu-id="80e61-107">When an app name is recognized from the user, the entityDetectionCallback checks whether the requested app matches one or more apps in the list of installed apps.</span><span class="sxs-lookup"><span data-stu-id="80e61-107">When an app name is recognized from the user, the entityDetectionCallback checks whether the requested app matches one or more apps in the list of installed apps.</span></span> <span data-ttu-id="80e61-108">It handles the case where the requested app is not installed, and where the app name is ambiguous (matches more than one installed app).</span><span class="sxs-lookup"><span data-stu-id="80e61-108">It handles the case where the requested app is not installed, and where the app name is ambiguous (matches more than one installed app).</span></span>

## <a name="video"></a><span data-ttu-id="80e61-109">Video</span><span class="sxs-lookup"><span data-stu-id="80e61-109">Video</span></span>

<span data-ttu-id="80e61-110">[![Demo VR App Preview](http://aka.ms/cl-demo-vrapp-preview)](http://aka.ms/blis-demo-vrapp)</span><span class="sxs-lookup"><span data-stu-id="80e61-110">[![Demo VR App Preview](http://aka.ms/cl-demo-vrapp-preview)](http://aka.ms/blis-demo-vrapp)</span></span>

## <a name="requirements"></a><span data-ttu-id="80e61-111">Requirements</span><span class="sxs-lookup"><span data-stu-id="80e61-111">Requirements</span></span>

<span data-ttu-id="80e61-112">This tutorial requires that the VRAppLauncher bot is running:</span><span class="sxs-lookup"><span data-stu-id="80e61-112">This tutorial requires that the VRAppLauncher bot is running:</span></span>

    npm run demo-vrapp
    
### <a name="open-the-demo"></a><span data-ttu-id="80e61-113">Open the demo</span><span class="sxs-lookup"><span data-stu-id="80e61-113">Open the demo</span></span>

<span data-ttu-id="80e61-114">In the Model list of the web UI, click on VRAppLauncher.</span><span class="sxs-lookup"><span data-stu-id="80e61-114">In the Model list of the web UI, click on VRAppLauncher.</span></span> 

## <a name="entities"></a><span data-ttu-id="80e61-115">Entities</span><span class="sxs-lookup"><span data-stu-id="80e61-115">Entities</span></span>

<span data-ttu-id="80e61-116">We have created four entities:</span><span class="sxs-lookup"><span data-stu-id="80e61-116">We have created four entities:</span></span>

- <span data-ttu-id="80e61-117">AppName: for example Skype</span><span class="sxs-lookup"><span data-stu-id="80e61-117">AppName: for example Skype</span></span>
- <span data-ttu-id="80e61-118">PlacementLocation: for example wall</span><span class="sxs-lookup"><span data-stu-id="80e61-118">PlacementLocation: for example wall</span></span>
- <span data-ttu-id="80e61-119">UnknownAppName: a programmatic entity that the system sets when it doesn't recognize an entity name the user says, for example because it hasn't been installed.</span><span class="sxs-lookup"><span data-stu-id="80e61-119">UnknownAppName: a programmatic entity that the system sets when it doesn't recognize an entity name the user says, for example because it hasn't been installed.</span></span>
- <span data-ttu-id="80e61-120">DisAmbigAppNames: an array of two or more installed app names that match what the user said.</span><span class="sxs-lookup"><span data-stu-id="80e61-120">DisAmbigAppNames: an array of two or more installed app names that match what the user said.</span></span> 

![](../media/tutorial_vrapplauncher_entities.PNG)

### <a name="actions"></a><span data-ttu-id="80e61-121">Actions</span><span class="sxs-lookup"><span data-stu-id="80e61-121">Actions</span></span>

<span data-ttu-id="80e61-122">We have created a set of actions that includes an API called LaunchApp, which will start the function call to launch an app.</span><span class="sxs-lookup"><span data-stu-id="80e61-122">We have created a set of actions that includes an API called LaunchApp, which will start the function call to launch an app.</span></span>

![](../media/tutorial_vrapplauncher_actions.PNG)

### <a name="training-dialogs"></a><span data-ttu-id="80e61-123">Training Dialogs</span><span class="sxs-lookup"><span data-stu-id="80e61-123">Training Dialogs</span></span>
<span data-ttu-id="80e61-124">We have defined a number of training dialogs.</span><span class="sxs-lookup"><span data-stu-id="80e61-124">We have defined a number of training dialogs.</span></span>

![](../media/tutorial_vrapplauncher_dialogs.PNG)

<span data-ttu-id="80e61-125">As an example, let's try a teaching session.</span><span class="sxs-lookup"><span data-stu-id="80e61-125">As an example, let's try a teaching session.</span></span>

1. <span data-ttu-id="80e61-126">Click Train Dialogs, then New Train Dialog.</span><span class="sxs-lookup"><span data-stu-id="80e61-126">Click Train Dialogs, then New Train Dialog.</span></span>
1. <span data-ttu-id="80e61-127">Enter 'hi'.</span><span class="sxs-lookup"><span data-stu-id="80e61-127">Enter 'hi'.</span></span>
2. <span data-ttu-id="80e61-128">Click Score Action.</span><span class="sxs-lookup"><span data-stu-id="80e61-128">Click Score Action.</span></span>
3. <span data-ttu-id="80e61-129">Click to Select 'which app do you want to start?'</span><span class="sxs-lookup"><span data-stu-id="80e61-129">Click to Select 'which app do you want to start?'</span></span>
4. <span data-ttu-id="80e61-130">Enter 'outlook'.</span><span class="sxs-lookup"><span data-stu-id="80e61-130">Enter 'outlook'.</span></span>
    - <span data-ttu-id="80e61-131">LUIS recognizes it as an entity.</span><span class="sxs-lookup"><span data-stu-id="80e61-131">LUIS recognizes it as an entity.</span></span>
5. <span data-ttu-id="80e61-132">Click Score Actions.</span><span class="sxs-lookup"><span data-stu-id="80e61-132">Click Score Actions.</span></span>
3. <span data-ttu-id="80e61-133">Click to Select 'where do you want it placed?'</span><span class="sxs-lookup"><span data-stu-id="80e61-133">Click to Select 'where do you want it placed?'</span></span>
4. <span data-ttu-id="80e61-134">Enter 'on the wall'.</span><span class="sxs-lookup"><span data-stu-id="80e61-134">Enter 'on the wall'.</span></span>
    - <span data-ttu-id="80e61-135">LUIS recognizes it as a PlacementLocation.</span><span class="sxs-lookup"><span data-stu-id="80e61-135">LUIS recognizes it as a PlacementLocation.</span></span>
2. <span data-ttu-id="80e61-136">Enter Score Actions.</span><span class="sxs-lookup"><span data-stu-id="80e61-136">Enter Score Actions.</span></span>
6. <span data-ttu-id="80e61-137">Select 'LaunchApp'</span><span class="sxs-lookup"><span data-stu-id="80e61-137">Select 'LaunchApp'</span></span>
7. <span data-ttu-id="80e61-138">System: 'starting outlook on the wall'.</span><span class="sxs-lookup"><span data-stu-id="80e61-138">System: 'starting outlook on the wall'.</span></span>
    - <span data-ttu-id="80e61-139">This triggered an API call.</span><span class="sxs-lookup"><span data-stu-id="80e61-139">This triggered an API call.</span></span> <span data-ttu-id="80e61-140">The code for this call is at C:\<\installedpath>\src\demos\demoVRAppLauncher.ts.</span><span class="sxs-lookup"><span data-stu-id="80e61-140">The code for this call is at C:\<\installedpath>\src\demos\demoVRAppLauncher.ts.</span></span> <span data-ttu-id="80e61-141">However, it does not actually contain the code to launch Outlook for this demo.</span><span class="sxs-lookup"><span data-stu-id="80e61-141">However, it does not actually contain the code to launch Outlook for this demo.</span></span>
    - <span data-ttu-id="80e61-142">It clears the AppName and PlacementLocation entities.</span><span class="sxs-lookup"><span data-stu-id="80e61-142">It clears the AppName and PlacementLocation entities.</span></span> <span data-ttu-id="80e61-143">The returns the above string as response.</span><span class="sxs-lookup"><span data-stu-id="80e61-143">The returns the above string as response.</span></span>
4. <span data-ttu-id="80e61-144">Click Done Teaching.</span><span class="sxs-lookup"><span data-stu-id="80e61-144">Click Done Teaching.</span></span>

![](../media/tutorial_vrapplauncher_callbackcode.PNG)

<span data-ttu-id="80e61-145">Let's start another training session for handling unknown and ambiguous entities.</span><span class="sxs-lookup"><span data-stu-id="80e61-145">Let's start another training session for handling unknown and ambiguous entities.</span></span>

1. <span data-ttu-id="80e61-146">Click New Train Dialog.</span><span class="sxs-lookup"><span data-stu-id="80e61-146">Click New Train Dialog.</span></span>
1. <span data-ttu-id="80e61-147">Enter 'start OneNote'.</span><span class="sxs-lookup"><span data-stu-id="80e61-147">Enter 'start OneNote'.</span></span> 
    - <span data-ttu-id="80e61-148">The model recognizes OneNote as an app name.</span><span class="sxs-lookup"><span data-stu-id="80e61-148">The model recognizes OneNote as an app name.</span></span> <span data-ttu-id="80e61-149">The `EntityDetectionCallback` function defined in the code resolves the name entered by the user to an app name by matching it to the app list defined in the code.</span><span class="sxs-lookup"><span data-stu-id="80e61-149">The `EntityDetectionCallback` function defined in the code resolves the name entered by the user to an app name by matching it to the app list defined in the code.</span></span> <span data-ttu-id="80e61-150">It then returns the set of all matching apps.</span><span class="sxs-lookup"><span data-stu-id="80e61-150">It then returns the set of all matching apps.</span></span> 
    - <span data-ttu-id="80e61-151">If the list of matches is zero, that means the app is not installed.</span><span class="sxs-lookup"><span data-stu-id="80e61-151">If the list of matches is zero, that means the app is not installed.</span></span> <span data-ttu-id="80e61-152">It puts it in unknownAppName.</span><span class="sxs-lookup"><span data-stu-id="80e61-152">It puts it in unknownAppName.</span></span>
    - <span data-ttu-id="80e61-153">If it finds more than one app, it copies them into the `DisambigAppNames` and clears the AppName entity.</span><span class="sxs-lookup"><span data-stu-id="80e61-153">If it finds more than one app, it copies them into the `DisambigAppNames` and clears the AppName entity.</span></span>
2. <span data-ttu-id="80e61-154">Click Score Action.</span><span class="sxs-lookup"><span data-stu-id="80e61-154">Click Score Action.</span></span>
3. <span data-ttu-id="80e61-155">Click to Select 'Sorry, I don't know the app $UknownAppName.'</span><span class="sxs-lookup"><span data-stu-id="80e61-155">Click to Select 'Sorry, I don't know the app $UknownAppName.'</span></span>
4. <span data-ttu-id="80e61-156">Enter 'start Amazon'.</span><span class="sxs-lookup"><span data-stu-id="80e61-156">Enter 'start Amazon'.</span></span> <span data-ttu-id="80e61-157">We'll try the other path.</span><span class="sxs-lookup"><span data-stu-id="80e61-157">We'll try the other path.</span></span>
5. <span data-ttu-id="80e61-158">Click Score Actions.</span><span class="sxs-lookup"><span data-stu-id="80e61-158">Click Score Actions.</span></span>
    - <span data-ttu-id="80e61-159">Amazon Video and Amazon Music are now in `DisambigAppNames` memory, and OneNote has been cleared.</span><span class="sxs-lookup"><span data-stu-id="80e61-159">Amazon Video and Amazon Music are now in `DisambigAppNames` memory, and OneNote has been cleared.</span></span>
3. <span data-ttu-id="80e61-160">Click to Select 'There are few apps that sound like that...'</span><span class="sxs-lookup"><span data-stu-id="80e61-160">Click to Select 'There are few apps that sound like that...'</span></span>
    - <span data-ttu-id="80e61-161">The score is not very high because we have only defined a few training dialogs up to this point.</span><span class="sxs-lookup"><span data-stu-id="80e61-161">The score is not very high because we have only defined a few training dialogs up to this point.</span></span> <span data-ttu-id="80e61-162">Defining more training dialogs would make the model more decisive.</span><span class="sxs-lookup"><span data-stu-id="80e61-162">Defining more training dialogs would make the model more decisive.</span></span>
2. <span data-ttu-id="80e61-163">Enter Score Actions.</span><span class="sxs-lookup"><span data-stu-id="80e61-163">Enter Score Actions.</span></span>
4. <span data-ttu-id="80e61-164">Click Done Teaching.</span><span class="sxs-lookup"><span data-stu-id="80e61-164">Click Done Teaching.</span></span>

<span data-ttu-id="80e61-165">You have now seen how to do entity resolution.</span><span class="sxs-lookup"><span data-stu-id="80e61-165">You have now seen how to do entity resolution.</span></span> <span data-ttu-id="80e61-166">The demo also illustrated API callbacks and showed a template for collecting information, checking for presence and ambiguity, and taking the correct action accordingly.</span><span class="sxs-lookup"><span data-stu-id="80e61-166">The demo also illustrated API callbacks and showed a template for collecting information, checking for presence and ambiguity, and taking the correct action accordingly.</span></span>

## <a name="next-steps"></a><span data-ttu-id="80e61-167">Next steps</span><span class="sxs-lookup"><span data-stu-id="80e61-167">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="80e61-168">Deploying a Conversation Learner bot</span><span class="sxs-lookup"><span data-stu-id="80e61-168">Deploying a Conversation Learner bot</span></span>](../deploy-to-bf.md)
