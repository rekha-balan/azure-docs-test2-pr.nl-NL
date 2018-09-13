---
title: Using C#, integrate LUIS with a bot using the Bot Builder SDK- Azure Cognitive Services| Microsoft Docs
description: Using C#, build a chat bot integrated with language understanding (LUIS). This chat bot uses the prebuilt HomeAutomation domain to quickly implement a bot solution.
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: article
ms.date: 08/13/2018
ms.author: diberry
ms.openlocfilehash: d0010ccf51fc688fa66e1be82c735ae38455509b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865311"
---
# <a name="web-app-bot-using-the-luis-template-for-c"></a><span data-ttu-id="1bf26-104">Web App Bot using the LUIS template for C#</span><span class="sxs-lookup"><span data-stu-id="1bf26-104">Web App Bot using the LUIS template for C#</span></span>

<span data-ttu-id="1bf26-105">Using C#, build a chat bot integrated with language understanding (LUIS).</span><span class="sxs-lookup"><span data-stu-id="1bf26-105">Using C#, build a chat bot integrated with language understanding (LUIS).</span></span> <span data-ttu-id="1bf26-106">This chat bot uses the prebuilt HomeAutomation domain to quickly implement a bot solution.</span><span class="sxs-lookup"><span data-stu-id="1bf26-106">This chat bot uses the prebuilt HomeAutomation domain to quickly implement a bot solution.</span></span> 

## <a name="prerequisite"></a><span data-ttu-id="1bf26-107">Prerequisite</span><span class="sxs-lookup"><span data-stu-id="1bf26-107">Prerequisite</span></span>

* <span data-ttu-id="1bf26-108">[HomeAutomation LUIS app](luis-get-started-create-app.md).</span><span class="sxs-lookup"><span data-stu-id="1bf26-108">[HomeAutomation LUIS app](luis-get-started-create-app.md).</span></span> <span data-ttu-id="1bf26-109">The intents from this LUIS app map to the bot's dialog handlers.</span><span class="sxs-lookup"><span data-stu-id="1bf26-109">The intents from this LUIS app map to the bot's dialog handlers.</span></span> 

## <a name="luis-homeautomation-intents"></a><span data-ttu-id="1bf26-110">LUIS HomeAutomation Intents</span><span class="sxs-lookup"><span data-stu-id="1bf26-110">LUIS HomeAutomation Intents</span></span>

| <span data-ttu-id="1bf26-111">Intent</span><span class="sxs-lookup"><span data-stu-id="1bf26-111">Intent</span></span> | <span data-ttu-id="1bf26-112">Example utterance</span><span class="sxs-lookup"><span data-stu-id="1bf26-112">Example utterance</span></span> | <span data-ttu-id="1bf26-113">Bot functionality</span><span class="sxs-lookup"><span data-stu-id="1bf26-113">Bot functionality</span></span> |
|:----:|:----------:|---|
| <span data-ttu-id="1bf26-114">HomeAutomation.TurnOn</span><span class="sxs-lookup"><span data-stu-id="1bf26-114">HomeAutomation.TurnOn</span></span> | <span data-ttu-id="1bf26-115">Turn on the lights.</span><span class="sxs-lookup"><span data-stu-id="1bf26-115">Turn on the lights.</span></span> | <span data-ttu-id="1bf26-116">When the LUIS intent `HomeAutomation.TurnOn` is detected, the bot invokes the `OnIntent` dialog handler.</span><span class="sxs-lookup"><span data-stu-id="1bf26-116">When the LUIS intent `HomeAutomation.TurnOn` is detected, the bot invokes the `OnIntent` dialog handler.</span></span> <span data-ttu-id="1bf26-117">This dialog is where you'd call an IoT service to turn on a device and tell the user that the device has been turned on.</span><span class="sxs-lookup"><span data-stu-id="1bf26-117">This dialog is where you'd call an IoT service to turn on a device and tell the user that the device has been turned on.</span></span> |
| <span data-ttu-id="1bf26-118">HomeAutomation.TurnOff</span><span class="sxs-lookup"><span data-stu-id="1bf26-118">HomeAutomation.TurnOff</span></span> | <span data-ttu-id="1bf26-119">Turn off the bedroom lights.</span><span class="sxs-lookup"><span data-stu-id="1bf26-119">Turn off the bedroom lights.</span></span> | <span data-ttu-id="1bf26-120">When the LUIS intent `HomeAutomation.TurnOff` is detected, the bot invokes the `OffIntent` dialog handler.</span><span class="sxs-lookup"><span data-stu-id="1bf26-120">When the LUIS intent `HomeAutomation.TurnOff` is detected, the bot invokes the `OffIntent` dialog handler.</span></span> <span data-ttu-id="1bf26-121">This dialog is where you'd call an IoT service to turn off a device and tell the user that the device has been turned off.</span><span class="sxs-lookup"><span data-stu-id="1bf26-121">This dialog is where you'd call an IoT service to turn off a device and tell the user that the device has been turned off.</span></span> |

## <a name="create-a-language-understanding-bot-with-bot-service"></a><span data-ttu-id="1bf26-122">Create a Language Understanding bot with Bot Service</span><span class="sxs-lookup"><span data-stu-id="1bf26-122">Create a Language Understanding bot with Bot Service</span></span>

1. <span data-ttu-id="1bf26-123">In the [Azure portal](https://portal.azure.com), select **Create new resource** in the top left menu.</span><span class="sxs-lookup"><span data-stu-id="1bf26-123">In the [Azure portal](https://portal.azure.com), select **Create new resource** in the top left menu.</span></span>

    ![Create new resource](./media/luis-tutorial-cscharp-web-bot/bot-service-creation.png)

2. <span data-ttu-id="1bf26-125">In the search box, search for **Web App Bot**.</span><span class="sxs-lookup"><span data-stu-id="1bf26-125">In the search box, search for **Web App Bot**.</span></span> 

    ![Create new resource](./media/luis-tutorial-cscharp-web-bot/bot-service-selection.png)

3. <span data-ttu-id="1bf26-127">In the Web App Bot window, click **Create**.</span><span class="sxs-lookup"><span data-stu-id="1bf26-127">In the Web App Bot window, click **Create**.</span></span>

4. <span data-ttu-id="1bf26-128">In **Bot Service**, provide the required information, and click **Create**.</span><span class="sxs-lookup"><span data-stu-id="1bf26-128">In **Bot Service**, provide the required information, and click **Create**.</span></span> <span data-ttu-id="1bf26-129">This creates and deploys the bot service and LUIS app to Azure.</span><span class="sxs-lookup"><span data-stu-id="1bf26-129">This creates and deploys the bot service and LUIS app to Azure.</span></span> <span data-ttu-id="1bf26-130">If you want to use [speech priming](https://docs.microsoft.com/bot-framework/bot-service-manage-speech-priming), review [region requirements](luis-resources-faq.md#what-luis-regions-support-bot-framework-speech-priming) before creating your bot.</span><span class="sxs-lookup"><span data-stu-id="1bf26-130">If you want to use [speech priming](https://docs.microsoft.com/bot-framework/bot-service-manage-speech-priming), review [region requirements](luis-resources-faq.md#what-luis-regions-support-bot-framework-speech-priming) before creating your bot.</span></span> 
    * <span data-ttu-id="1bf26-131">Set **App name** to your bot’s name.</span><span class="sxs-lookup"><span data-stu-id="1bf26-131">Set **App name** to your bot’s name.</span></span> <span data-ttu-id="1bf26-132">The name is used as the subdomain when your bot is deployed to the cloud (for example, mynotesbot.azurewebsites.net).</span><span class="sxs-lookup"><span data-stu-id="1bf26-132">The name is used as the subdomain when your bot is deployed to the cloud (for example, mynotesbot.azurewebsites.net).</span></span> <!-- This name is also used as the name of the LUIS app associated with your bot. Copy it to use later, to find the LUIS app associated with the bot. -->
    * <span data-ttu-id="1bf26-133">Select the subscription, [resource group](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview), App service plan, and [location](https://azure.microsoft.com/regions/).</span><span class="sxs-lookup"><span data-stu-id="1bf26-133">Select the subscription, [resource group](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview), App service plan, and [location](https://azure.microsoft.com/regions/).</span></span>
    * <span data-ttu-id="1bf26-134">Select the **Language understanding (C#)** template for the **Bot template** field.</span><span class="sxs-lookup"><span data-stu-id="1bf26-134">Select the **Language understanding (C#)** template for the **Bot template** field.</span></span>
    * <span data-ttu-id="1bf26-135">Select the **LUIS App Location**.</span><span class="sxs-lookup"><span data-stu-id="1bf26-135">Select the **LUIS App Location**.</span></span> <span data-ttu-id="1bf26-136">This is the authoring [region](luis-reference-regions.md) the app is created in.</span><span class="sxs-lookup"><span data-stu-id="1bf26-136">This is the authoring [region](luis-reference-regions.md) the app is created in.</span></span>
    * <span data-ttu-id="1bf26-137">Select the confirmation checkbox for the legal notice.</span><span class="sxs-lookup"><span data-stu-id="1bf26-137">Select the confirmation checkbox for the legal notice.</span></span> <span data-ttu-id="1bf26-138">The terms of the legal notice are below the checkbox.</span><span class="sxs-lookup"><span data-stu-id="1bf26-138">The terms of the legal notice are below the checkbox.</span></span>

    ![Bot Service](./media/luis-tutorial-cscharp-web-bot/bot-service-setting-callout-template.png)


5. <span data-ttu-id="1bf26-140">Confirm that the bot service has been deployed.</span><span class="sxs-lookup"><span data-stu-id="1bf26-140">Confirm that the bot service has been deployed.</span></span>
    * <span data-ttu-id="1bf26-141">Click Notifications (the bell icon that is located along the top edge of the Azure portal).</span><span class="sxs-lookup"><span data-stu-id="1bf26-141">Click Notifications (the bell icon that is located along the top edge of the Azure portal).</span></span> <span data-ttu-id="1bf26-142">The notification changes from **Deployment started** to **Deployment succeeded**.</span><span class="sxs-lookup"><span data-stu-id="1bf26-142">The notification changes from **Deployment started** to **Deployment succeeded**.</span></span>
    * <span data-ttu-id="1bf26-143">After the notification changes to **Deployment succeeded**, click **Go to resource** on that notification.</span><span class="sxs-lookup"><span data-stu-id="1bf26-143">After the notification changes to **Deployment succeeded**, click **Go to resource** on that notification.</span></span>

> [!Note]
> <span data-ttu-id="1bf26-144">This web app bot creation process also created a new LUIS app for you.</span><span class="sxs-lookup"><span data-stu-id="1bf26-144">This web app bot creation process also created a new LUIS app for you.</span></span> <span data-ttu-id="1bf26-145">It has been trained and published for you.</span><span class="sxs-lookup"><span data-stu-id="1bf26-145">It has been trained and published for you.</span></span> 

## <a name="try-the-default-bot"></a><span data-ttu-id="1bf26-146">Try the default bot</span><span class="sxs-lookup"><span data-stu-id="1bf26-146">Try the default bot</span></span>

<span data-ttu-id="1bf26-147">Confirm that the bot has been deployed by selecting the **Notifications** checkbox.</span><span class="sxs-lookup"><span data-stu-id="1bf26-147">Confirm that the bot has been deployed by selecting the **Notifications** checkbox.</span></span> <span data-ttu-id="1bf26-148">The notifications changes from **Deployment in progress...** to **Deployment succeeded**.</span><span class="sxs-lookup"><span data-stu-id="1bf26-148">The notifications changes from **Deployment in progress...** to **Deployment succeeded**.</span></span> <span data-ttu-id="1bf26-149">Click **Go to resource** button to open the bot's resources.</span><span class="sxs-lookup"><span data-stu-id="1bf26-149">Click **Go to resource** button to open the bot's resources.</span></span>

<span data-ttu-id="1bf26-150">Once the bot is deployed, click **Test in Web Chat** to open the Web Chat pane.</span><span class="sxs-lookup"><span data-stu-id="1bf26-150">Once the bot is deployed, click **Test in Web Chat** to open the Web Chat pane.</span></span> <span data-ttu-id="1bf26-151">Type "hello" in Web Chat.</span><span class="sxs-lookup"><span data-stu-id="1bf26-151">Type "hello" in Web Chat.</span></span>

  ![Test the bot in Web Chat](./media/luis-tutorial-cscharp-web-bot/bot-service-web-chat.png)

<span data-ttu-id="1bf26-153">The bot responds by saying "You have reached Greeting.</span><span class="sxs-lookup"><span data-stu-id="1bf26-153">The bot responds by saying "You have reached Greeting.</span></span> <span data-ttu-id="1bf26-154">You said: hello".</span><span class="sxs-lookup"><span data-stu-id="1bf26-154">You said: hello".</span></span>  <span data-ttu-id="1bf26-155">This response confirms that the bot has received your message and passed it to a default LUIS app that it created.</span><span class="sxs-lookup"><span data-stu-id="1bf26-155">This response confirms that the bot has received your message and passed it to a default LUIS app that it created.</span></span> <span data-ttu-id="1bf26-156">This default LUIS app detected a Greeting intent.</span><span class="sxs-lookup"><span data-stu-id="1bf26-156">This default LUIS app detected a Greeting intent.</span></span> <span data-ttu-id="1bf26-157">In the next step, you'll connect the bot to the LUIS app you previously created instead of the default LUIS app.</span><span class="sxs-lookup"><span data-stu-id="1bf26-157">In the next step, you'll connect the bot to the LUIS app you previously created instead of the default LUIS app.</span></span>

## <a name="connect-your-luis-app-to-the-bot"></a><span data-ttu-id="1bf26-158">Connect your LUIS app to the bot</span><span class="sxs-lookup"><span data-stu-id="1bf26-158">Connect your LUIS app to the bot</span></span>

<span data-ttu-id="1bf26-159">Open **Application Settings** and edit the **LuisAppId** field to contain the application ID of your LUIS app.</span><span class="sxs-lookup"><span data-stu-id="1bf26-159">Open **Application Settings** and edit the **LuisAppId** field to contain the application ID of your LUIS app.</span></span> <span data-ttu-id="1bf26-160">If you created your HomeAutomation LUIS app in a region other than West US, you need to change the **LuisAPIHostName** as well.</span><span class="sxs-lookup"><span data-stu-id="1bf26-160">If you created your HomeAutomation LUIS app in a region other than West US, you need to change the **LuisAPIHostName** as well.</span></span> <span data-ttu-id="1bf26-161">The **LuisAPIKey** is currently set to your authoring key.</span><span class="sxs-lookup"><span data-stu-id="1bf26-161">The **LuisAPIKey** is currently set to your authoring key.</span></span> <span data-ttu-id="1bf26-162">You change this to your endpoint key when your traffic exceeds the free tier quota.</span><span class="sxs-lookup"><span data-stu-id="1bf26-162">You change this to your endpoint key when your traffic exceeds the free tier quota.</span></span> 

  ![Update the LUIS app ID in Azure](./media/luis-tutorial-cscharp-web-bot/bot-service-app-settings.png)

> [!Note]
> <span data-ttu-id="1bf26-164">If you don't have the LUIS app ID of the [Home Automation app](luis-get-started-create-app.md), log in to the [LUIS](luis-reference-regions.md) website using the same account you use to log in to Azure.</span><span class="sxs-lookup"><span data-stu-id="1bf26-164">If you don't have the LUIS app ID of the [Home Automation app](luis-get-started-create-app.md), log in to the [LUIS](luis-reference-regions.md) website using the same account you use to log in to Azure.</span></span> 
> 1. <span data-ttu-id="1bf26-165">Click on **My apps**.</span><span class="sxs-lookup"><span data-stu-id="1bf26-165">Click on **My apps**.</span></span> 
> 2. <span data-ttu-id="1bf26-166">Find the LUIS app you previously created, that contains the intents and entities from the HomeAutomation domain.</span><span class="sxs-lookup"><span data-stu-id="1bf26-166">Find the LUIS app you previously created, that contains the intents and entities from the HomeAutomation domain.</span></span>
> 3. <span data-ttu-id="1bf26-167">In the **Settings** page for the LUIS app, find and copy the app ID.</span><span class="sxs-lookup"><span data-stu-id="1bf26-167">In the **Settings** page for the LUIS app, find and copy the app ID.</span></span> <span data-ttu-id="1bf26-168">Make sure it is [trained](luis-interactive-test.md) and [published](luis-how-to-publish-app.md).</span><span class="sxs-lookup"><span data-stu-id="1bf26-168">Make sure it is [trained](luis-interactive-test.md) and [published](luis-how-to-publish-app.md).</span></span> 

    > [!WARNING]
    > If you delete your app ID or LUIS key, the bot will stop working.

## <a name="modify-the-bot-code"></a><span data-ttu-id="1bf26-169">Modify the bot code</span><span class="sxs-lookup"><span data-stu-id="1bf26-169">Modify the bot code</span></span>

1. <span data-ttu-id="1bf26-170">Click **Build** and then click **Open online code editor**.</span><span class="sxs-lookup"><span data-stu-id="1bf26-170">Click **Build** and then click **Open online code editor**.</span></span>

   ![Open online code editor](./media/luis-tutorial-cscharp-web-bot/bot-service-build.png)

2. <span data-ttu-id="1bf26-172">Right click `build.cmd` and choose **Run from Console** to build the app.</span><span class="sxs-lookup"><span data-stu-id="1bf26-172">Right click `build.cmd` and choose **Run from Console** to build the app.</span></span> <span data-ttu-id="1bf26-173">There are several build steps the service completes automatically for you.</span><span class="sxs-lookup"><span data-stu-id="1bf26-173">There are several build steps the service completes automatically for you.</span></span> <span data-ttu-id="1bf26-174">The build is complete when it finished with "Finished successfully."</span><span class="sxs-lookup"><span data-stu-id="1bf26-174">The build is complete when it finished with "Finished successfully."</span></span>

3. <span data-ttu-id="1bf26-175">In the code editor, open `/Dialogs/BasicLuisDialog.cs`.</span><span class="sxs-lookup"><span data-stu-id="1bf26-175">In the code editor, open `/Dialogs/BasicLuisDialog.cs`.</span></span> <span data-ttu-id="1bf26-176">It contains the following code:</span><span class="sxs-lookup"><span data-stu-id="1bf26-176">It contains the following code:</span></span>

   [!code-csharp[Default BasicLuisDialog.cs](~/samples-luis/documentation-samples/tutorial-web-app-bot/csharp/Default_BasicLuisDialog.cs "Default BasicLuisDialog.cs")]

## <a name="change-code-to-homeautomation-intents"></a><span data-ttu-id="1bf26-177">Change code to HomeAutomation intents</span><span class="sxs-lookup"><span data-stu-id="1bf26-177">Change code to HomeAutomation intents</span></span>


1. <span data-ttu-id="1bf26-178">Remove the three intent attributes and methods for **Greeting**, **Cancel**, and **Help**.</span><span class="sxs-lookup"><span data-stu-id="1bf26-178">Remove the three intent attributes and methods for **Greeting**, **Cancel**, and **Help**.</span></span> <span data-ttu-id="1bf26-179">These intents are not used in the HomeAutomation prebuilt domain.</span><span class="sxs-lookup"><span data-stu-id="1bf26-179">These intents are not used in the HomeAutomation prebuilt domain.</span></span> <span data-ttu-id="1bf26-180">Make sure to keep the **None** intent attribute and method.</span><span class="sxs-lookup"><span data-stu-id="1bf26-180">Make sure to keep the **None** intent attribute and method.</span></span> 

2. <span data-ttu-id="1bf26-181">Add dependencies to the top of the file, with the other dependencies:</span><span class="sxs-lookup"><span data-stu-id="1bf26-181">Add dependencies to the top of the file, with the other dependencies:</span></span>

   [!code-csharp[Dependencies](~/samples-luis/documentation-samples/tutorial-web-app-bot/csharp/BasicLuisDialog.cs?range=4-5&dedent=8 "dependencies")]

3. <span data-ttu-id="1bf26-182">Add constants to manage strings at the top of the `BasicLuisDialog ` class:</span><span class="sxs-lookup"><span data-stu-id="1bf26-182">Add constants to manage strings at the top of the `BasicLuisDialog ` class:</span></span>

   [!code-csharp[Add Intent and Entity Constants](~/samples-luis/documentation-samples/tutorial-web-app-bot/csharp/BasicLuisDialog.cs?range=23-32&dedent=8 "Add Intent and Entity Constants")]

4. <span data-ttu-id="1bf26-183">Add the code for the new intents of `HomeAutomation.TurnOn` and `HomeAutomation.TurnOff` inside the `BasicLuisDialog ` class:</span><span class="sxs-lookup"><span data-stu-id="1bf26-183">Add the code for the new intents of `HomeAutomation.TurnOn` and `HomeAutomation.TurnOff` inside the `BasicLuisDialog ` class:</span></span>

   [!code-csharp[Add Intents](~/samples-luis/documentation-samples/tutorial-web-app-bot/csharp/BasicLuisDialog.cs?range=61-71&dedent=8 "Add Intents")]

5. <span data-ttu-id="1bf26-184">Add the code to get any entities found by LUIS inside the `BasicLuisDialog ` class:</span><span class="sxs-lookup"><span data-stu-id="1bf26-184">Add the code to get any entities found by LUIS inside the `BasicLuisDialog ` class:</span></span>

   [!code-csharp[Collect entities](~/samples-luis/documentation-samples/tutorial-web-app-bot/csharp/BasicLuisDialog.cs?range=34-53&dedent=8 "Collect entities")]

6. <span data-ttu-id="1bf26-185">Change **ShowLuisResult** method in the `BasicLuisDialog ` class to round the score, collect the entities, and display the response message in the chatbot:</span><span class="sxs-lookup"><span data-stu-id="1bf26-185">Change **ShowLuisResult** method in the `BasicLuisDialog ` class to round the score, collect the entities, and display the response message in the chatbot:</span></span>

   [!code-csharp[Display message in chatbot](~/samples-luis/documentation-samples/tutorial-web-app-bot/csharp/BasicLuisDialog.cs?range=73-83&dedent=8 "Display message in chatbot")]

## <a name="build-the-bot"></a><span data-ttu-id="1bf26-186">Build the bot</span><span class="sxs-lookup"><span data-stu-id="1bf26-186">Build the bot</span></span>
<span data-ttu-id="1bf26-187">In the code editor, right-click on `build.cmd` and select **Run from Console**.</span><span class="sxs-lookup"><span data-stu-id="1bf26-187">In the code editor, right-click on `build.cmd` and select **Run from Console**.</span></span>

![<span data-ttu-id="1bf26-188">Build Web bot</span><span class="sxs-lookup"><span data-stu-id="1bf26-188">Build Web bot</span></span> ](./media/luis-tutorial-cscharp-web-bot/bot-service-build-run-from-console.png)

<span data-ttu-id="1bf26-189">The code view is replaced with a terminal window showing the progress and results of the build.</span><span class="sxs-lookup"><span data-stu-id="1bf26-189">The code view is replaced with a terminal window showing the progress and results of the build.</span></span>

![Build Web bot success](./media/luis-tutorial-cscharp-web-bot/bot-service-build-success.png)

> [!TIP]
> <span data-ttu-id="1bf26-191">An alternative method to build the bot is to select the bot name in the top blue bar, and select **Open Kudu Console**.</span><span class="sxs-lookup"><span data-stu-id="1bf26-191">An alternative method to build the bot is to select the bot name in the top blue bar, and select **Open Kudu Console**.</span></span> <span data-ttu-id="1bf26-192">The console opens to **D:\home**.</span><span class="sxs-lookup"><span data-stu-id="1bf26-192">The console opens to **D:\home**.</span></span> 
> 
> <span data-ttu-id="1bf26-193">Change the directory to **D:\home\site\wwwroot** by typing: `cd site\wwwroot`</span><span class="sxs-lookup"><span data-stu-id="1bf26-193">Change the directory to **D:\home\site\wwwroot** by typing: `cd site\wwwroot`</span></span>
>
> <span data-ttu-id="1bf26-194">Run the build script by typing: `build.cmd`</span><span class="sxs-lookup"><span data-stu-id="1bf26-194">Run the build script by typing: `build.cmd`</span></span>

## <a name="test-the-bot"></a><span data-ttu-id="1bf26-195">Test the bot</span><span class="sxs-lookup"><span data-stu-id="1bf26-195">Test the bot</span></span>

<span data-ttu-id="1bf26-196">In the Azure portal, click on **Test in Web Chat** to test the bot.</span><span class="sxs-lookup"><span data-stu-id="1bf26-196">In the Azure portal, click on **Test in Web Chat** to test the bot.</span></span> <span data-ttu-id="1bf26-197">Type messages like "Turn on the lights", and "turn off my heater" to invoke the intents that you added to it.</span><span class="sxs-lookup"><span data-stu-id="1bf26-197">Type messages like "Turn on the lights", and "turn off my heater" to invoke the intents that you added to it.</span></span>

   ![Test HomeAutomation bot in Web Chat](./media/luis-tutorial-cscharp-web-bot/bot-service-chat-results.png)

> [!TIP]
> <span data-ttu-id="1bf26-199">You can retrain your LUIS app without any modification to your bot's code.</span><span class="sxs-lookup"><span data-stu-id="1bf26-199">You can retrain your LUIS app without any modification to your bot's code.</span></span> <span data-ttu-id="1bf26-200">See [Add example utterances](https://docs.microsoft.com/azure/cognitive-services/LUIS/add-example-utterances) and [train and test your LUIS app](https://docs.microsoft.com/azure/cognitive-services/LUIS/luis-interactive-test).</span><span class="sxs-lookup"><span data-stu-id="1bf26-200">See [Add example utterances](https://docs.microsoft.com/azure/cognitive-services/LUIS/add-example-utterances) and [train and test your LUIS app](https://docs.microsoft.com/azure/cognitive-services/LUIS/luis-interactive-test).</span></span> 

## <a name="download-the-bot-to-debug"></a><span data-ttu-id="1bf26-201">Download the bot to debug</span><span class="sxs-lookup"><span data-stu-id="1bf26-201">Download the bot to debug</span></span>
<span data-ttu-id="1bf26-202">If your bot isn't working, download the project to your local machine and continue [debugging](https://docs.microsoft.com/bot-framework/bot-service-debug-bot#debug-a-c-bot).</span><span class="sxs-lookup"><span data-stu-id="1bf26-202">If your bot isn't working, download the project to your local machine and continue [debugging](https://docs.microsoft.com/bot-framework/bot-service-debug-bot#debug-a-c-bot).</span></span> 

## <a name="learn-more-about-bot-framework"></a><span data-ttu-id="1bf26-203">Learn more about Bot Framework</span><span class="sxs-lookup"><span data-stu-id="1bf26-203">Learn more about Bot Framework</span></span>
<span data-ttu-id="1bf26-204">Learn more about [Bot Framework](https://dev.botframework.com/) and the [3.x](https://github.com/Microsoft/BotBuilder) and [4.x](https://github.com/Microsoft/botbuilder-dotnet) SDKs.</span><span class="sxs-lookup"><span data-stu-id="1bf26-204">Learn more about [Bot Framework](https://dev.botframework.com/) and the [3.x](https://github.com/Microsoft/BotBuilder) and [4.x](https://github.com/Microsoft/botbuilder-dotnet) SDKs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1bf26-205">Next steps</span><span class="sxs-lookup"><span data-stu-id="1bf26-205">Next steps</span></span>

<span data-ttu-id="1bf26-206">Add the LUIS intents and Bot service dialogs for handling **Help**, **Cancel**, and **Greeting** intents.</span><span class="sxs-lookup"><span data-stu-id="1bf26-206">Add the LUIS intents and Bot service dialogs for handling **Help**, **Cancel**, and **Greeting** intents.</span></span> <span data-ttu-id="1bf26-207">Remember to train, publish and to [build](#build-the-bot) the web app bot.</span><span class="sxs-lookup"><span data-stu-id="1bf26-207">Remember to train, publish and to [build](#build-the-bot) the web app bot.</span></span> <span data-ttu-id="1bf26-208">Both LUIS and the bot should have the same intents.</span><span class="sxs-lookup"><span data-stu-id="1bf26-208">Both LUIS and the bot should have the same intents.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="1bf26-209">[Add intents](./luis-how-to-add-intents.md)
> [Speech priming](https://docs.microsoft.com/bot-framework/bot-service-manage-speech-priming)</span><span class="sxs-lookup"><span data-stu-id="1bf26-209">[Add intents](./luis-how-to-add-intents.md)
[Speech priming](https://docs.microsoft.com/bot-framework/bot-service-manage-speech-priming)</span></span>


<!-- Links -->
[Github-BotFramework-Emulator-Download]: https://aka.ms/bot-framework-emulator
[Github-LUIS-Samples]: https://github.com/Microsoft/LUIS-Samples
[Github-LUIS-Samples-cs-hotel-bot]: https://github.com/Microsoft/LUIS-Samples/tree/master/bot-integration-samples/hotel-finder/csharp
[Github-LUIS-Samples-cs-hotel-bot-readme]: https://github.com/Microsoft/LUIS-Samples/blob/master/bot-integration-samples/hotel-finder/csharp/README.md
[BFPortal]: https://dev.botframework.com/
[RegisterInstructions]: https://docs.microsoft.com/bot-framework/portal-register-bot
[BotFramework]: https://docs.microsoft.com/bot-framework/
[VisualStudio]: https://www.visualstudio.com/

<!-- tested on Win10 -->
