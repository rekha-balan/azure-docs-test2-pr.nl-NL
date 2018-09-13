---
title: Create your first Language Understanding (LUIS) app in 10 minutes - Cognitive Services LUIS | Microsoft Docs
description: In this quickstart, create a LUIS app that uses the prebuilt domain `HomeAutomation` for turning lights and appliances on and off. This prebuilt domain provides intents, entities, and example utterances for you. When you're finished, you'll have a LUIS endpoint running in the cloud.
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: quickstart
ms.date: 08/22/2018
ms.author: diberry
ms.openlocfilehash: 457f23936dec0cf85e9aebbf3e54bba37c2f3ca3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857994"
---
# <a name="quickstart-use-prebuilt-home-automation-app"></a><span data-ttu-id="974ac-105">Quickstart: Use prebuilt Home automation app</span><span class="sxs-lookup"><span data-stu-id="974ac-105">Quickstart: Use prebuilt Home automation app</span></span>

<span data-ttu-id="974ac-106">In this quickstart, create a LUIS app that uses the prebuilt domain `HomeAutomation` for turning lights and appliances on and off.</span><span class="sxs-lookup"><span data-stu-id="974ac-106">In this quickstart, create a LUIS app that uses the prebuilt domain `HomeAutomation` for turning lights and appliances on and off.</span></span> <span data-ttu-id="974ac-107">This prebuilt domain provides intents, entities, and example utterances for you.</span><span class="sxs-lookup"><span data-stu-id="974ac-107">This prebuilt domain provides intents, entities, and example utterances for you.</span></span> <span data-ttu-id="974ac-108">When you're finished, you'll have a LUIS endpoint running in the cloud.</span><span class="sxs-lookup"><span data-stu-id="974ac-108">When you're finished, you'll have a LUIS endpoint running in the cloud.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="974ac-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="974ac-109">Prerequisites</span></span>

<span data-ttu-id="974ac-110">For this article, you need a free LUIS account, created on the LUIS portal at [http://www.luis.ai](http://www.luis.ai).</span><span class="sxs-lookup"><span data-stu-id="974ac-110">For this article, you need a free LUIS account, created on the LUIS portal at [http://www.luis.ai](http://www.luis.ai).</span></span> 

## <a name="create-a-new-app"></a><span data-ttu-id="974ac-111">Create a new app</span><span class="sxs-lookup"><span data-stu-id="974ac-111">Create a new app</span></span>
<span data-ttu-id="974ac-112">You can create and manage your applications on **My Apps**.</span><span class="sxs-lookup"><span data-stu-id="974ac-112">You can create and manage your applications on **My Apps**.</span></span> 

1. <span data-ttu-id="974ac-113">Sign in to the LUIS portal.</span><span class="sxs-lookup"><span data-stu-id="974ac-113">Sign in to the LUIS portal.</span></span>

2. <span data-ttu-id="974ac-114">Select **Create new app**.</span><span class="sxs-lookup"><span data-stu-id="974ac-114">Select **Create new app**.</span></span>

    <span data-ttu-id="974ac-115">[![](media/luis-quickstart-new-app/app-list.png "Screenshot of app list")](media/luis-quickstart-new-app/app-list.png)</span><span class="sxs-lookup"><span data-stu-id="974ac-115">[![](media/luis-quickstart-new-app/app-list.png "Screenshot of app list")](media/luis-quickstart-new-app/app-list.png)</span></span>

3. <span data-ttu-id="974ac-116">In the dialog box, name your application "Home Automation".</span><span class="sxs-lookup"><span data-stu-id="974ac-116">In the dialog box, name your application "Home Automation".</span></span>

    <span data-ttu-id="974ac-117">[![](media/luis-quickstart-new-app/create-new-app-dialog.png "Screenshot of Create new app pop-up dialog")](media/luis-quickstart-new-app/create-new-app-dialog.png)</span><span class="sxs-lookup"><span data-stu-id="974ac-117">[![](media/luis-quickstart-new-app/create-new-app-dialog.png "Screenshot of Create new app pop-up dialog")](media/luis-quickstart-new-app/create-new-app-dialog.png)</span></span>

4. <span data-ttu-id="974ac-118">Choose your application culture.</span><span class="sxs-lookup"><span data-stu-id="974ac-118">Choose your application culture.</span></span> <span data-ttu-id="974ac-119">For this Home Automation app, choose English.</span><span class="sxs-lookup"><span data-stu-id="974ac-119">For this Home Automation app, choose English.</span></span> <span data-ttu-id="974ac-120">Then select **Done**.</span><span class="sxs-lookup"><span data-stu-id="974ac-120">Then select **Done**.</span></span> <span data-ttu-id="974ac-121">LUIS creates the Home Automation app.</span><span class="sxs-lookup"><span data-stu-id="974ac-121">LUIS creates the Home Automation app.</span></span> 

    >[!NOTE]
    ><span data-ttu-id="974ac-122">The culture cannot be changed once the application is created.</span><span class="sxs-lookup"><span data-stu-id="974ac-122">The culture cannot be changed once the application is created.</span></span> 

## <a name="add-prebuilt-domain"></a><span data-ttu-id="974ac-123">Add prebuilt domain</span><span class="sxs-lookup"><span data-stu-id="974ac-123">Add prebuilt domain</span></span>

<span data-ttu-id="974ac-124">Select **Prebuilt domains** in the left-side navigation pane.</span><span class="sxs-lookup"><span data-stu-id="974ac-124">Select **Prebuilt domains** in the left-side navigation pane.</span></span> <span data-ttu-id="974ac-125">Then search for "Home".</span><span class="sxs-lookup"><span data-stu-id="974ac-125">Then search for "Home".</span></span> <span data-ttu-id="974ac-126">Select **Add domain**.</span><span class="sxs-lookup"><span data-stu-id="974ac-126">Select **Add domain**.</span></span>

<span data-ttu-id="974ac-127">[![](media/luis-quickstart-new-app/home-automation.png "Screenshot of Home Automation domain called out in prebuilt domain menu")](media/luis-quickstart-new-app/home-automation.png)</span><span class="sxs-lookup"><span data-stu-id="974ac-127">[![](media/luis-quickstart-new-app/home-automation.png "Screenshot of Home Automation domain called out in prebuilt domain menu")](media/luis-quickstart-new-app/home-automation.png)</span></span>

<span data-ttu-id="974ac-128">When the domain is successfully added, the prebuilt domain box displays a **Remove domain** button.</span><span class="sxs-lookup"><span data-stu-id="974ac-128">When the domain is successfully added, the prebuilt domain box displays a **Remove domain** button.</span></span>

<span data-ttu-id="974ac-129">[![](media/luis-quickstart-new-app/remove-domain.png "Screenshot of Home Automation domain with remove button")](media/luis-quickstart-new-app/remove-domain.png)</span><span class="sxs-lookup"><span data-stu-id="974ac-129">[![](media/luis-quickstart-new-app/remove-domain.png "Screenshot of Home Automation domain with remove button")](media/luis-quickstart-new-app/remove-domain.png)</span></span>

## <a name="intents-and-entities"></a><span data-ttu-id="974ac-130">Intents and entities</span><span class="sxs-lookup"><span data-stu-id="974ac-130">Intents and entities</span></span>

<span data-ttu-id="974ac-131">Select **Intents** in the left-side navigation pane to review the HomeAutomation domain intents.</span><span class="sxs-lookup"><span data-stu-id="974ac-131">Select **Intents** in the left-side navigation pane to review the HomeAutomation domain intents.</span></span> 

<span data-ttu-id="974ac-132">[![](media/luis-quickstart-new-app/home-automation-intents.png "Screenshot of Intents list with Intent names in table highlighted")](media/luis-quickstart-new-app/home-automation-intents.png)</span><span class="sxs-lookup"><span data-stu-id="974ac-132">[![](media/luis-quickstart-new-app/home-automation-intents.png "Screenshot of Intents list with Intent names in table highlighted")](media/luis-quickstart-new-app/home-automation-intents.png)</span></span>

<span data-ttu-id="974ac-133">Each intent has sample utterances.</span><span class="sxs-lookup"><span data-stu-id="974ac-133">Each intent has sample utterances.</span></span>

> [!NOTE]
> <span data-ttu-id="974ac-134">**None** is an intent provided by all LUIS apps.</span><span class="sxs-lookup"><span data-stu-id="974ac-134">**None** is an intent provided by all LUIS apps.</span></span> <span data-ttu-id="974ac-135">You use it to handle utterances that don't correspond to functionality your app provides.</span><span class="sxs-lookup"><span data-stu-id="974ac-135">You use it to handle utterances that don't correspond to functionality your app provides.</span></span> 

<span data-ttu-id="974ac-136">Select the **HomeAutomation.TurnOff** intent.</span><span class="sxs-lookup"><span data-stu-id="974ac-136">Select the **HomeAutomation.TurnOff** intent.</span></span> <span data-ttu-id="974ac-137">You can see that the intent contains a list of utterances that are labeled with entities.</span><span class="sxs-lookup"><span data-stu-id="974ac-137">You can see that the intent contains a list of utterances that are labeled with entities.</span></span>

<span data-ttu-id="974ac-138">[![](media/luis-quickstart-new-app/home-automation-turnon.png "Screenshot of HomeAutomation.TurnOff intent")](media/luis-quickstart-new-app/home-automation-turnon.png)</span><span class="sxs-lookup"><span data-stu-id="974ac-138">[![](media/luis-quickstart-new-app/home-automation-turnon.png "Screenshot of HomeAutomation.TurnOff intent")](media/luis-quickstart-new-app/home-automation-turnon.png)</span></span>

## <a name="train-your-app"></a><span data-ttu-id="974ac-139">Train your app</span><span class="sxs-lookup"><span data-stu-id="974ac-139">Train your app</span></span>

<span data-ttu-id="974ac-140">Select **Train** in the top navigation.</span><span class="sxs-lookup"><span data-stu-id="974ac-140">Select **Train** in the top navigation.</span></span>

<span data-ttu-id="974ac-141">[![](media/luis-quickstart-new-app/trained.png "Screenshot of HomeAutomation.TurnOff intent with green success notification")](media/luis-quickstart-new-app/trained.png)</span><span class="sxs-lookup"><span data-stu-id="974ac-141">[![](media/luis-quickstart-new-app/trained.png "Screenshot of HomeAutomation.TurnOff intent with green success notification")](media/luis-quickstart-new-app/trained.png)</span></span>

## <a name="test-your-app"></a><span data-ttu-id="974ac-142">Test your app</span><span class="sxs-lookup"><span data-stu-id="974ac-142">Test your app</span></span>
<span data-ttu-id="974ac-143">Once you've trained your app, you can test it.</span><span class="sxs-lookup"><span data-stu-id="974ac-143">Once you've trained your app, you can test it.</span></span> <span data-ttu-id="974ac-144">Select **Test** in the top navigation.</span><span class="sxs-lookup"><span data-stu-id="974ac-144">Select **Test** in the top navigation.</span></span> <span data-ttu-id="974ac-145">Type a test utterance like "Turn off the lights" into the Interactive Testing pane, and press Enter.</span><span class="sxs-lookup"><span data-stu-id="974ac-145">Type a test utterance like "Turn off the lights" into the Interactive Testing pane, and press Enter.</span></span> 

```
Turn off the lights
```

<span data-ttu-id="974ac-146">Check that the top scoring intent corresponds to the intent you expected for each test utterance.</span><span class="sxs-lookup"><span data-stu-id="974ac-146">Check that the top scoring intent corresponds to the intent you expected for each test utterance.</span></span>

<span data-ttu-id="974ac-147">In this example, "Turn off the lights" is correctly identified as the top scoring intent of "HomeAutomation.TurnOff."</span><span class="sxs-lookup"><span data-stu-id="974ac-147">In this example, "Turn off the lights" is correctly identified as the top scoring intent of "HomeAutomation.TurnOff."</span></span>

<span data-ttu-id="974ac-148">[![](media/luis-quickstart-new-app/test.png "Screenshot of Test panel with utterance highlighted")](media/luis-quickstart-new-app/test.png)</span><span class="sxs-lookup"><span data-stu-id="974ac-148">[![](media/luis-quickstart-new-app/test.png "Screenshot of Test panel with utterance highlighted")](media/luis-quickstart-new-app/test.png)</span></span>


<span data-ttu-id="974ac-149">Select **Test** again to collapse the test pane.</span><span class="sxs-lookup"><span data-stu-id="974ac-149">Select **Test** again to collapse the test pane.</span></span> 

## <a name="publish-your-app"></a><span data-ttu-id="974ac-150">Publish your app</span><span class="sxs-lookup"><span data-stu-id="974ac-150">Publish your app</span></span>
<span data-ttu-id="974ac-151">Select **Publish** from the top navigation.</span><span class="sxs-lookup"><span data-stu-id="974ac-151">Select **Publish** from the top navigation.</span></span> 

<span data-ttu-id="974ac-152">[![](media/luis-quickstart-new-app/publish.png "Screenshot of app with publish button highlighted")](media/luis-quickstart-new-app/publish.png)</span><span class="sxs-lookup"><span data-stu-id="974ac-152">[![](media/luis-quickstart-new-app/publish.png "Screenshot of app with publish button highlighted")](media/luis-quickstart-new-app/publish.png)</span></span>

<span data-ttu-id="974ac-153">Select the Production slot and the **Publish** button.</span><span class="sxs-lookup"><span data-stu-id="974ac-153">Select the Production slot and the **Publish** button.</span></span>

<span data-ttu-id="974ac-154">The green notification bar at the top indicates the app successfully published.</span><span class="sxs-lookup"><span data-stu-id="974ac-154">The green notification bar at the top indicates the app successfully published.</span></span>

<span data-ttu-id="974ac-155">[![](media/luis-quickstart-new-app/published.png "Screenshot of app with publish success")](media/luis-quickstart-new-app/published.png)</span><span class="sxs-lookup"><span data-stu-id="974ac-155">[![](media/luis-quickstart-new-app/published.png "Screenshot of app with publish success")](media/luis-quickstart-new-app/published.png)</span></span>

<span data-ttu-id="974ac-156">After you've successfully published, you can use the endpoint URL displayed in the **Publish app** page.</span><span class="sxs-lookup"><span data-stu-id="974ac-156">After you've successfully published, you can use the endpoint URL displayed in the **Publish app** page.</span></span>

<span data-ttu-id="974ac-157">[![](media/luis-quickstart-new-app/endpoint.png "Screenshot of publish page with endpoint url highlighted")](media/luis-quickstart-new-app/endpoint.png)</span><span class="sxs-lookup"><span data-stu-id="974ac-157">[![](media/luis-quickstart-new-app/endpoint.png "Screenshot of publish page with endpoint url highlighted")](media/luis-quickstart-new-app/endpoint.png)</span></span>

## <a name="use-your-app"></a><span data-ttu-id="974ac-158">Use your app</span><span class="sxs-lookup"><span data-stu-id="974ac-158">Use your app</span></span>
<span data-ttu-id="974ac-159">You can test your published endpoint in a browser using the generated URL.</span><span class="sxs-lookup"><span data-stu-id="974ac-159">You can test your published endpoint in a browser using the generated URL.</span></span> <span data-ttu-id="974ac-160">Open this URL in your browser, set the URL parameter "&q" to your test query.</span><span class="sxs-lookup"><span data-stu-id="974ac-160">Open this URL in your browser, set the URL parameter "&q" to your test query.</span></span> <span data-ttu-id="974ac-161">For example, add `turn off the living room light` to the end of your URL, and then press Enter.</span><span class="sxs-lookup"><span data-stu-id="974ac-161">For example, add `turn off the living room light` to the end of your URL, and then press Enter.</span></span> <span data-ttu-id="974ac-162">The browser displays the JSON response of your HTTP endpoint.</span><span class="sxs-lookup"><span data-stu-id="974ac-162">The browser displays the JSON response of your HTTP endpoint.</span></span>


<span data-ttu-id="974ac-163">[![](media/luis-quickstart-new-app/turn-off-living-room.png "Screenshot of browser with JSON result detects the intent TurnOff")](media/luis-quickstart-new-app/turn-off-living-room.png)</span><span class="sxs-lookup"><span data-stu-id="974ac-163">[![](media/luis-quickstart-new-app/turn-off-living-room.png "Screenshot of browser with JSON result detects the intent TurnOff")](media/luis-quickstart-new-app/turn-off-living-room.png)</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="974ac-164">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="974ac-164">Clean up resources</span></span>
<span data-ttu-id="974ac-165">When no longer needed, delete the LUIS app.</span><span class="sxs-lookup"><span data-stu-id="974ac-165">When no longer needed, delete the LUIS app.</span></span> <span data-ttu-id="974ac-166">To do so, select the ellipsis (***...***) button to the right of the app name in the app list, select **Delete**.</span><span class="sxs-lookup"><span data-stu-id="974ac-166">To do so, select the ellipsis (***...***) button to the right of the app name in the app list, select **Delete**.</span></span> <span data-ttu-id="974ac-167">On the pop-up dialog **Delete app?**, select **Ok**.</span><span class="sxs-lookup"><span data-stu-id="974ac-167">On the pop-up dialog **Delete app?**, select **Ok**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="974ac-168">Next steps</span><span class="sxs-lookup"><span data-stu-id="974ac-168">Next steps</span></span>

<span data-ttu-id="974ac-169">You can call the endpoint from code:</span><span class="sxs-lookup"><span data-stu-id="974ac-169">You can call the endpoint from code:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="974ac-170">Call a LUIS endpoint using code</span><span class="sxs-lookup"><span data-stu-id="974ac-170">Call a LUIS endpoint using code</span></span>](luis-get-started-cs-get-intent.md)
