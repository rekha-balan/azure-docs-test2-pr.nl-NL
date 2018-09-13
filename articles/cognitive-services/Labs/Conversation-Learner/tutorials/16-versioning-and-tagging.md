---
title: How to use versioning and tagging with a Conversation Learner model - Microsoft Cognitive Services | Microsoft Docs
titleSuffix: Azure
description: Learn how to use versioning and tagging with a Conversation Learner model.
services: cognitive-services
author: v-jaswel
manager: nolachar
ms.service: cognitive-services
ms.component: conversation-learner
ms.topic: article
ms.date: 04/30/2018
ms.author: v-jaswel
ms.openlocfilehash: c7f23d989cbfa0ece9e404a0fe0feb68cf5fddb2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867786"
---
# <a name="how-to-use-versioning-and-tagging"></a><span data-ttu-id="13e4e-103">How to use versioning and tagging</span><span class="sxs-lookup"><span data-stu-id="13e4e-103">How to use versioning and tagging</span></span>

<span data-ttu-id="13e4e-104">This tutorial illustrates how to tag versions of your Conversation Learner model, and set which version is “live”.</span><span class="sxs-lookup"><span data-stu-id="13e4e-104">This tutorial illustrates how to tag versions of your Conversation Learner model, and set which version is “live”.</span></span>  

## <a name="requirements"></a><span data-ttu-id="13e4e-105">Requirements</span><span class="sxs-lookup"><span data-stu-id="13e4e-105">Requirements</span></span>
<span data-ttu-id="13e4e-106">This tutorial requires using the bot emulator to create log dialogs, not the Log Dialog Web UI.</span><span class="sxs-lookup"><span data-stu-id="13e4e-106">This tutorial requires using the bot emulator to create log dialogs, not the Log Dialog Web UI.</span></span>  

<span data-ttu-id="13e4e-107">This tutorial requires that the general tutorial bot is running:</span><span class="sxs-lookup"><span data-stu-id="13e4e-107">This tutorial requires that the general tutorial bot is running:</span></span>

    npm run tutorial-general

## <a name="details"></a><span data-ttu-id="13e4e-108">Details</span><span class="sxs-lookup"><span data-stu-id="13e4e-108">Details</span></span>

<span data-ttu-id="13e4e-109">When editing, you are always editing the tag called “master” -- you can create tagged versions from master (which essentially take a snapshot of master), but you cannot edit tagged versions.</span><span class="sxs-lookup"><span data-stu-id="13e4e-109">When editing, you are always editing the tag called “master” -- you can create tagged versions from master (which essentially take a snapshot of master), but you cannot edit tagged versions.</span></span>

## <a name="steps"></a><span data-ttu-id="13e4e-110">Steps</span><span class="sxs-lookup"><span data-stu-id="13e4e-110">Steps</span></span>

### <a name="install-the-bot-framework-emulator"></a><span data-ttu-id="13e4e-111">Install the Bot framework emulator</span><span class="sxs-lookup"><span data-stu-id="13e4e-111">Install the Bot framework emulator</span></span>

- <span data-ttu-id="13e4e-112">Go to [https://github.com/Microsoft/BotFramework-Emulator](https://github.com/Microsoft/BotFramework-Emulator).</span><span class="sxs-lookup"><span data-stu-id="13e4e-112">Go to [https://github.com/Microsoft/BotFramework-Emulator](https://github.com/Microsoft/BotFramework-Emulator).</span></span>
- <span data-ttu-id="13e4e-113">Download and install the emulator.</span><span class="sxs-lookup"><span data-stu-id="13e4e-113">Download and install the emulator.</span></span>

### <a name="create-an-model"></a><span data-ttu-id="13e4e-114">Create an model</span><span class="sxs-lookup"><span data-stu-id="13e4e-114">Create an model</span></span>

1. <span data-ttu-id="13e4e-115">Click New Model</span><span class="sxs-lookup"><span data-stu-id="13e4e-115">Click New Model</span></span>
2. <span data-ttu-id="13e4e-116">In the Name field, enter Tutorial-16-Versioning</span><span class="sxs-lookup"><span data-stu-id="13e4e-116">In the Name field, enter Tutorial-16-Versioning</span></span>
3. <span data-ttu-id="13e4e-117">Click Create</span><span class="sxs-lookup"><span data-stu-id="13e4e-117">Click Create</span></span> 
4. <span data-ttu-id="13e4e-118">Click Settings</span><span class="sxs-lookup"><span data-stu-id="13e4e-118">Click Settings</span></span>
5. <span data-ttu-id="13e4e-119">Copy the Model ID</span><span class="sxs-lookup"><span data-stu-id="13e4e-119">Copy the Model ID</span></span>

### <a name="configure-the-emulator"></a><span data-ttu-id="13e4e-120">Configure the emulator</span><span class="sxs-lookup"><span data-stu-id="13e4e-120">Configure the emulator</span></span>

- <span data-ttu-id="13e4e-121">In the Conversation Learner root folder, open the .env file.</span><span class="sxs-lookup"><span data-stu-id="13e4e-121">In the Conversation Learner root folder, open the .env file.</span></span>
- <span data-ttu-id="13e4e-122">Paste the Model ID as the value of CONVERSATION_LEARNER_MODEL_ID</span><span class="sxs-lookup"><span data-stu-id="13e4e-122">Paste the Model ID as the value of CONVERSATION_LEARNER_MODEL_ID</span></span>
- <span data-ttu-id="13e4e-123">Restart the Conversation Learner service by exiting from the command prompt, and rerunning:</span><span class="sxs-lookup"><span data-stu-id="13e4e-123">Restart the Conversation Learner service by exiting from the command prompt, and rerunning:</span></span>
 
    <span data-ttu-id="13e4e-124">npm run tutorial-general</span><span class="sxs-lookup"><span data-stu-id="13e4e-124">npm run tutorial-general</span></span> 

### <a name="actions"></a><span data-ttu-id="13e4e-125">Actions</span><span class="sxs-lookup"><span data-stu-id="13e4e-125">Actions</span></span>

<span data-ttu-id="13e4e-126">Let's create an action:</span><span class="sxs-lookup"><span data-stu-id="13e4e-126">Let's create an action:</span></span>

1. <span data-ttu-id="13e4e-127">Switch to the Web UI.</span><span class="sxs-lookup"><span data-stu-id="13e4e-127">Switch to the Web UI.</span></span>
1. <span data-ttu-id="13e4e-128">Click Actions, then New Action.</span><span class="sxs-lookup"><span data-stu-id="13e4e-128">Click Actions, then New Action.</span></span>
2. <span data-ttu-id="13e4e-129">In Response, enter “hi there (version 1)”.</span><span class="sxs-lookup"><span data-stu-id="13e4e-129">In Response, enter “hi there (version 1)”.</span></span>
3. <span data-ttu-id="13e4e-130">Click Save.</span><span class="sxs-lookup"><span data-stu-id="13e4e-130">Click Save.</span></span>


![](../media/tutorial16_action1.PNG)

<span data-ttu-id="13e4e-131">Create a new tag:</span><span class="sxs-lookup"><span data-stu-id="13e4e-131">Create a new tag:</span></span>

3. <span data-ttu-id="13e4e-132">Click on “settings” and create a new “tag”.</span><span class="sxs-lookup"><span data-stu-id="13e4e-132">Click on “settings” and create a new “tag”.</span></span>
    - <span data-ttu-id="13e4e-133">Call it “version 1”</span><span class="sxs-lookup"><span data-stu-id="13e4e-133">Call it “version 1”</span></span>
4. <span data-ttu-id="13e4e-134">Set “version 1” to be “live”.</span><span class="sxs-lookup"><span data-stu-id="13e4e-134">Set “version 1” to be “live”.</span></span>  
    - <span data-ttu-id="13e4e-135">The effect of setting the live tag to "version 1" is that channels using this bot will use the “version 1” tag.</span><span class="sxs-lookup"><span data-stu-id="13e4e-135">The effect of setting the live tag to "version 1" is that channels using this bot will use the “version 1” tag.</span></span>
    - <span data-ttu-id="13e4e-136">Tagged versions of models are not affected by edits (changing actions, entities, adding train dialogs).</span><span class="sxs-lookup"><span data-stu-id="13e4e-136">Tagged versions of models are not affected by edits (changing actions, entities, adding train dialogs).</span></span>  
    - <span data-ttu-id="13e4e-137">Edits to an model (changing actions, entities, adding train dialogs) are always made on the "master" tag.</span><span class="sxs-lookup"><span data-stu-id="13e4e-137">Edits to an model (changing actions, entities, adding train dialogs) are always made on the "master" tag.</span></span>  <span data-ttu-id="13e4e-138">In other words, "master" is the only tag that can change; other tags are fixed snapshots.</span><span class="sxs-lookup"><span data-stu-id="13e4e-138">In other words, "master" is the only tag that can change; other tags are fixed snapshots.</span></span>
    - <span data-ttu-id="13e4e-139">Log dialogs in the Conversation Learner UI always use master (not the live tag).</span><span class="sxs-lookup"><span data-stu-id="13e4e-139">Log dialogs in the Conversation Learner UI always use master (not the live tag).</span></span>

![](../media/tutorial16_v1_create.PNG)

<span data-ttu-id="13e4e-140">The version has been created in settings:</span><span class="sxs-lookup"><span data-stu-id="13e4e-140">The version has been created in settings:</span></span>

![](../media/tutorial16_settings.PNG)

<span data-ttu-id="13e4e-141">Let's add a second action:</span><span class="sxs-lookup"><span data-stu-id="13e4e-141">Let's add a second action:</span></span>

1. <span data-ttu-id="13e4e-142">Click Actions, then New Action.</span><span class="sxs-lookup"><span data-stu-id="13e4e-142">Click Actions, then New Action.</span></span>
2. <span data-ttu-id="13e4e-143">In Response, enter “bye bye (version 2)”.</span><span class="sxs-lookup"><span data-stu-id="13e4e-143">In Response, enter “bye bye (version 2)”.</span></span>

<span data-ttu-id="13e4e-144">Edit the first action:</span><span class="sxs-lookup"><span data-stu-id="13e4e-144">Edit the first action:</span></span>

1. <span data-ttu-id="13e4e-145">Click Actions.</span><span class="sxs-lookup"><span data-stu-id="13e4e-145">Click Actions.</span></span>
2. <span data-ttu-id="13e4e-146">Under Actions, click on "hi there (version 1)".</span><span class="sxs-lookup"><span data-stu-id="13e4e-146">Under Actions, click on "hi there (version 1)".</span></span>
3. <span data-ttu-id="13e4e-147">Change the Response to "hi there (version 2)".</span><span class="sxs-lookup"><span data-stu-id="13e4e-147">Change the Response to "hi there (version 2)".</span></span>

![](../media/tutorial16_hi_there_v2.PNG)

### <a name="switch-to-the-bot-emulator"></a><span data-ttu-id="13e4e-148">Switch to the bot emulator</span><span class="sxs-lookup"><span data-stu-id="13e4e-148">Switch to the bot emulator</span></span>

1. <span data-ttu-id="13e4e-149">In the bot UI, enter "goodbye".</span><span class="sxs-lookup"><span data-stu-id="13e4e-149">In the bot UI, enter "goodbye".</span></span>
2. <span data-ttu-id="13e4e-150">The bot responds with "hi there (version 1)".</span><span class="sxs-lookup"><span data-stu-id="13e4e-150">The bot responds with "hi there (version 1)".</span></span>
    - <span data-ttu-id="13e4e-151">This shows the version 1 is "live".</span><span class="sxs-lookup"><span data-stu-id="13e4e-151">This shows the version 1 is "live".</span></span> 

![](../media/tutorial16_bf_response.PNG)

### <a name="switch-to-the-web-ui"></a><span data-ttu-id="13e4e-152">Switch to the Web UI</span><span class="sxs-lookup"><span data-stu-id="13e4e-152">Switch to the Web UI</span></span>

1. <span data-ttu-id="13e4e-153">Click on Log Dialogs (If you don't see any dialogs, click the refresh button).</span><span class="sxs-lookup"><span data-stu-id="13e4e-153">Click on Log Dialogs (If you don't see any dialogs, click the refresh button).</span></span>
2. <span data-ttu-id="13e4e-154">Click on "hi there (version 2)"</span><span class="sxs-lookup"><span data-stu-id="13e4e-154">Click on "hi there (version 2)"</span></span>

> [!NOTE]
> <span data-ttu-id="13e4e-155">We can make corrections by choosing from all currently available actions.</span><span class="sxs-lookup"><span data-stu-id="13e4e-155">We can make corrections by choosing from all currently available actions.</span></span> <span data-ttu-id="13e4e-156">These edits will be made to the master.</span><span class="sxs-lookup"><span data-stu-id="13e4e-156">These edits will be made to the master.</span></span>

<span data-ttu-id="13e4e-157">You have now seen how versioning works, and how you can interact with the bot using the Bot framework emulator.</span><span class="sxs-lookup"><span data-stu-id="13e4e-157">You have now seen how versioning works, and how you can interact with the bot using the Bot framework emulator.</span></span>

## <a name="next-steps"></a><span data-ttu-id="13e4e-158">Next steps</span><span class="sxs-lookup"><span data-stu-id="13e4e-158">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="13e4e-159">Demo - password reset</span><span class="sxs-lookup"><span data-stu-id="13e4e-159">Demo - password reset</span></span>](./demo-password-reset.md)
