---
title: Integrate LUIS with a bot using the Bot Builder SDK for Node.js in Azure | Microsoft Docs
description: Build a bot integrated with a LUIS application using the Bot Framework.
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: article
ms.date: 03/06/2018
ms.author: diberry
ms.openlocfilehash: 6d6937105b11d94138b51660dc9f3c5e682e19bc
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868952"
---
# <a name="integrate-luis-with-a-bot-using-the-bot-builder-sdk-for-nodejs"></a><span data-ttu-id="df12b-103">Integrate LUIS with a bot using the Bot Builder SDK for Node.js</span><span class="sxs-lookup"><span data-stu-id="df12b-103">Integrate LUIS with a bot using the Bot Builder SDK for Node.js</span></span>

<span data-ttu-id="df12b-104">This tutorial walks you through building a bot with the [Bot Framework][BotFramework] that's integrated with a LUIS app.</span><span class="sxs-lookup"><span data-stu-id="df12b-104">This tutorial walks you through building a bot with the [Bot Framework][BotFramework] that's integrated with a LUIS app.</span></span>

## <a name="prerequisite"></a><span data-ttu-id="df12b-105">Prerequisite</span><span class="sxs-lookup"><span data-stu-id="df12b-105">Prerequisite</span></span>

<span data-ttu-id="df12b-106">Before you create the bot, follow the steps in [Create an app](./luis-get-started-create-app.md) to build the LUIS app that it uses.</span><span class="sxs-lookup"><span data-stu-id="df12b-106">Before you create the bot, follow the steps in [Create an app](./luis-get-started-create-app.md) to build the LUIS app that it uses.</span></span>

<span data-ttu-id="df12b-107">The bot responds to intents from the HomeAutomation domain that are in the LUIS app.</span><span class="sxs-lookup"><span data-stu-id="df12b-107">The bot responds to intents from the HomeAutomation domain that are in the LUIS app.</span></span> <span data-ttu-id="df12b-108">For each of these intents, the LUIS app provides an intent that maps to it.</span><span class="sxs-lookup"><span data-stu-id="df12b-108">For each of these intents, the LUIS app provides an intent that maps to it.</span></span> <span data-ttu-id="df12b-109">The bot provides a dialog that handles the intent that LUIS detects.</span><span class="sxs-lookup"><span data-stu-id="df12b-109">The bot provides a dialog that handles the intent that LUIS detects.</span></span>

| <span data-ttu-id="df12b-110">Intent</span><span class="sxs-lookup"><span data-stu-id="df12b-110">Intent</span></span> | <span data-ttu-id="df12b-111">Example utterance</span><span class="sxs-lookup"><span data-stu-id="df12b-111">Example utterance</span></span> | <span data-ttu-id="df12b-112">Bot functionality</span><span class="sxs-lookup"><span data-stu-id="df12b-112">Bot functionality</span></span> |
|:----:|:----------:|---|
| <span data-ttu-id="df12b-113">HomeAutomation.TurnOn</span><span class="sxs-lookup"><span data-stu-id="df12b-113">HomeAutomation.TurnOn</span></span> | <span data-ttu-id="df12b-114">Turn on the lights.</span><span class="sxs-lookup"><span data-stu-id="df12b-114">Turn on the lights.</span></span> | <span data-ttu-id="df12b-115">The bot invokes the `TurnOnDialog` when the `HomeAutomation.TurnOn` is detected.</span><span class="sxs-lookup"><span data-stu-id="df12b-115">The bot invokes the `TurnOnDialog` when the `HomeAutomation.TurnOn` is detected.</span></span> <span data-ttu-id="df12b-116">This dialog is where you'd invoke an IoT service to turn on a device and tell the user that the device has been turned on.</span><span class="sxs-lookup"><span data-stu-id="df12b-116">This dialog is where you'd invoke an IoT service to turn on a device and tell the user that the device has been turned on.</span></span> |
| <span data-ttu-id="df12b-117">HomeAutomation.TurnOff</span><span class="sxs-lookup"><span data-stu-id="df12b-117">HomeAutomation.TurnOff</span></span> | <span data-ttu-id="df12b-118">Turn off the bedroom lights.</span><span class="sxs-lookup"><span data-stu-id="df12b-118">Turn off the bedroom lights.</span></span> | <span data-ttu-id="df12b-119">The bot invokes the `TurnOffDialog` when the `HomeAutomation.TurnOff` is detected.</span><span class="sxs-lookup"><span data-stu-id="df12b-119">The bot invokes the `TurnOffDialog` when the `HomeAutomation.TurnOff` is detected.</span></span> <span data-ttu-id="df12b-120">This dialog where you'd invoke an IoT service to turn off a device and tell the user that the device has been turned off.</span><span class="sxs-lookup"><span data-stu-id="df12b-120">This dialog where you'd invoke an IoT service to turn off a device and tell the user that the device has been turned off.</span></span> |


## <a name="create-a-language-understanding-bot-with-bot-service"></a><span data-ttu-id="df12b-121">Create a Language Understanding bot with Bot Service</span><span class="sxs-lookup"><span data-stu-id="df12b-121">Create a Language Understanding bot with Bot Service</span></span>

1. <span data-ttu-id="df12b-122">In the [Azure portal](https://portal.azure.com), select **Create new resource** in the menu blade and select **See all**.</span><span class="sxs-lookup"><span data-stu-id="df12b-122">In the [Azure portal](https://portal.azure.com), select **Create new resource** in the menu blade and select **See all**.</span></span>

    ![Create new resource](./media/luis-tutorial-node-bot/bot-service-creation.png)

2. <span data-ttu-id="df12b-124">In the search box, search for **Web App Bot**.</span><span class="sxs-lookup"><span data-stu-id="df12b-124">In the search box, search for **Web App Bot**.</span></span> 

    ![Create new resource](./media/luis-tutorial-node-bot/bot-service-selection.png)

3. <span data-ttu-id="df12b-126">In the **Bot Service** blade, provide the required information, and select **Create**.</span><span class="sxs-lookup"><span data-stu-id="df12b-126">In the **Bot Service** blade, provide the required information, and select **Create**.</span></span> <span data-ttu-id="df12b-127">This creates and deploys the bot service and LUIS app to Azure.</span><span class="sxs-lookup"><span data-stu-id="df12b-127">This creates and deploys the bot service and LUIS app to Azure.</span></span> <span data-ttu-id="df12b-128">If you want to use [speech priming](https://docs.microsoft.com/bot-framework/bot-service-manage-speech-priming), review [region requirements](luis-resources-faq.md#what-luis-regions-support-bot-framework-speech-priming) before creating your bot.</span><span class="sxs-lookup"><span data-stu-id="df12b-128">If you want to use [speech priming](https://docs.microsoft.com/bot-framework/bot-service-manage-speech-priming), review [region requirements](luis-resources-faq.md#what-luis-regions-support-bot-framework-speech-priming) before creating your bot.</span></span> 
    * <span data-ttu-id="df12b-129">Set **App name** to your bot’s name.</span><span class="sxs-lookup"><span data-stu-id="df12b-129">Set **App name** to your bot’s name.</span></span> <span data-ttu-id="df12b-130">The name is used as the subdomain when your bot is deployed to the cloud (for example, mynotesbot.azurewebsites.net).</span><span class="sxs-lookup"><span data-stu-id="df12b-130">The name is used as the subdomain when your bot is deployed to the cloud (for example, mynotesbot.azurewebsites.net).</span></span> <!-- This name is also used as the name of the LUIS app associated with your bot. Copy it to use later, to find the LUIS app associated with the bot. -->
    * <span data-ttu-id="df12b-131">Select the subscription, [resource group](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview), App service plan, and [location](https://azure.microsoft.com/regions/).</span><span class="sxs-lookup"><span data-stu-id="df12b-131">Select the subscription, [resource group](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview), App service plan, and [location](https://azure.microsoft.com/regions/).</span></span>
    * <span data-ttu-id="df12b-132">Select the **Language understanding (Node.js)** template for the **Bot template** field.</span><span class="sxs-lookup"><span data-stu-id="df12b-132">Select the **Language understanding (Node.js)** template for the **Bot template** field.</span></span>
    * <span data-ttu-id="df12b-133">Select the **LUIS App Location**.</span><span class="sxs-lookup"><span data-stu-id="df12b-133">Select the **LUIS App Location**.</span></span> <span data-ttu-id="df12b-134">This is the authoring [region][LUIS] the app is created in.</span><span class="sxs-lookup"><span data-stu-id="df12b-134">This is the authoring [region][LUIS] the app is created in.</span></span>
    * <span data-ttu-id="df12b-135">Select the confirmation checkbox for the legal notice.</span><span class="sxs-lookup"><span data-stu-id="df12b-135">Select the confirmation checkbox for the legal notice.</span></span> <span data-ttu-id="df12b-136">The terms of the legal notice are below the checkbox.</span><span class="sxs-lookup"><span data-stu-id="df12b-136">The terms of the legal notice are below the checkbox.</span></span>

    ![Bot Service blade](./media/luis-tutorial-node-bot/bot-service-setting-callout-template.png)


4. <span data-ttu-id="df12b-138">Confirm that the bot service has been deployed.</span><span class="sxs-lookup"><span data-stu-id="df12b-138">Confirm that the bot service has been deployed.</span></span>
    * <span data-ttu-id="df12b-139">Select Notifications (the bell icon that is located along the top edge of the Azure portal).</span><span class="sxs-lookup"><span data-stu-id="df12b-139">Select Notifications (the bell icon that is located along the top edge of the Azure portal).</span></span> <span data-ttu-id="df12b-140">The notification will change from **Deployment started** to **Deployment succeeded**.</span><span class="sxs-lookup"><span data-stu-id="df12b-140">The notification will change from **Deployment started** to **Deployment succeeded**.</span></span>
    * <span data-ttu-id="df12b-141">After the notification changes to **Deployment succeeded**, select **Go to resource** on that notification.</span><span class="sxs-lookup"><span data-stu-id="df12b-141">After the notification changes to **Deployment succeeded**, select **Go to resource** on that notification.</span></span>

## <a name="try-the-default-bot"></a><span data-ttu-id="df12b-142">Try the default bot</span><span class="sxs-lookup"><span data-stu-id="df12b-142">Try the default bot</span></span>

<span data-ttu-id="df12b-143">Confirm that the bot has been deployed by checking the **Notifications**.</span><span class="sxs-lookup"><span data-stu-id="df12b-143">Confirm that the bot has been deployed by checking the **Notifications**.</span></span> <span data-ttu-id="df12b-144">The notifications will change from **Deployment in progress...** to **Deployment succeeded**.</span><span class="sxs-lookup"><span data-stu-id="df12b-144">The notifications will change from **Deployment in progress...** to **Deployment succeeded**.</span></span> <span data-ttu-id="df12b-145">Select **Go to resource** button to open the bot's resources blade.</span><span class="sxs-lookup"><span data-stu-id="df12b-145">Select **Go to resource** button to open the bot's resources blade.</span></span>

<!-- this step isn't supposed to be necessary -->
## <a name="install-npm-resources"></a><span data-ttu-id="df12b-146">Install NPM resources</span><span class="sxs-lookup"><span data-stu-id="df12b-146">Install NPM resources</span></span>
<span data-ttu-id="df12b-147">Install NPM packages with the following steps:</span><span class="sxs-lookup"><span data-stu-id="df12b-147">Install NPM packages with the following steps:</span></span>

1. <span data-ttu-id="df12b-148">Select **Build** from the **Bot Management** section of the Web App Bot.</span><span class="sxs-lookup"><span data-stu-id="df12b-148">Select **Build** from the **Bot Management** section of the Web App Bot.</span></span> 

2. <span data-ttu-id="df12b-149">A new, second browser window opens.</span><span class="sxs-lookup"><span data-stu-id="df12b-149">A new, second browser window opens.</span></span> <span data-ttu-id="df12b-150">Select **Open online code editor**.</span><span class="sxs-lookup"><span data-stu-id="df12b-150">Select **Open online code editor**.</span></span>

3. <span data-ttu-id="df12b-151">In the top navigation bar, select the web app bot name `homeautomationluisbot`.</span><span class="sxs-lookup"><span data-stu-id="df12b-151">In the top navigation bar, select the web app bot name `homeautomationluisbot`.</span></span> 

4. <span data-ttu-id="df12b-152">In the drop-down list, select **Open Kudu Console**.</span><span class="sxs-lookup"><span data-stu-id="df12b-152">In the drop-down list, select **Open Kudu Console**.</span></span>

5. <span data-ttu-id="df12b-153">A new browser window opens.</span><span class="sxs-lookup"><span data-stu-id="df12b-153">A new browser window opens.</span></span> <span data-ttu-id="df12b-154">In the console, enter the following command:</span><span class="sxs-lookup"><span data-stu-id="df12b-154">In the console, enter the following command:</span></span>

    ```
    cd site\wwwroot && npm install
    ```

    <span data-ttu-id="df12b-155">Wait for the install process to finish.</span><span class="sxs-lookup"><span data-stu-id="df12b-155">Wait for the install process to finish.</span></span> <span data-ttu-id="df12b-156">Return to the first browser window.</span><span class="sxs-lookup"><span data-stu-id="df12b-156">Return to the first browser window.</span></span> 

## <a name="test-in-web-chat"></a><span data-ttu-id="df12b-157">Test in Web Chat</span><span class="sxs-lookup"><span data-stu-id="df12b-157">Test in Web Chat</span></span>
<span data-ttu-id="df12b-158">Once the bot is registered, select **Test in Web Chat** to open the Web Chat pane.</span><span class="sxs-lookup"><span data-stu-id="df12b-158">Once the bot is registered, select **Test in Web Chat** to open the Web Chat pane.</span></span> <span data-ttu-id="df12b-159">Type "hello" in Web Chat.</span><span class="sxs-lookup"><span data-stu-id="df12b-159">Type "hello" in Web Chat.</span></span>

  ![Test the bot in Web Chat](./media/luis-tutorial-node-bot/bot-service-web-chat.png)

<span data-ttu-id="df12b-161">The bot responds by saying "You have reached Greeting.</span><span class="sxs-lookup"><span data-stu-id="df12b-161">The bot responds by saying "You have reached Greeting.</span></span> <span data-ttu-id="df12b-162">You said: hello".</span><span class="sxs-lookup"><span data-stu-id="df12b-162">You said: hello".</span></span> <span data-ttu-id="df12b-163">This confirms that the bot has received your message and passed it to a default LUIS app that it created.</span><span class="sxs-lookup"><span data-stu-id="df12b-163">This confirms that the bot has received your message and passed it to a default LUIS app that it created.</span></span> <span data-ttu-id="df12b-164">This default LUIS app detected a Greeting intent.</span><span class="sxs-lookup"><span data-stu-id="df12b-164">This default LUIS app detected a Greeting intent.</span></span> <span data-ttu-id="df12b-165">In the next step, you'll connect the bot to the LUIS app you previously created instead of the default LUIS app.</span><span class="sxs-lookup"><span data-stu-id="df12b-165">In the next step, you'll connect the bot to the LUIS app you previously created instead of the default LUIS app.</span></span>

## <a name="connect-your-luis-app-to-the-bot"></a><span data-ttu-id="df12b-166">Connect your LUIS app to the bot</span><span class="sxs-lookup"><span data-stu-id="df12b-166">Connect your LUIS app to the bot</span></span>

<span data-ttu-id="df12b-167">Open **Application Settings** in the first browser window and edit the **LuisAppId** field to contain the application ID of your LUIS app.</span><span class="sxs-lookup"><span data-stu-id="df12b-167">Open **Application Settings** in the first browser window and edit the **LuisAppId** field to contain the application ID of your LUIS app.</span></span>

  ![Update the LUIS app ID in Azure](./media/luis-tutorial-node-bot/bot-service-app-id.png)

<span data-ttu-id="df12b-169">If you don't have the LUIS app ID, log in to the [LUIS](luis-reference-regions.md) website using the same account you use to log in to Azure.</span><span class="sxs-lookup"><span data-stu-id="df12b-169">If you don't have the LUIS app ID, log in to the [LUIS](luis-reference-regions.md) website using the same account you use to log in to Azure.</span></span> <span data-ttu-id="df12b-170">Select on **My apps**.</span><span class="sxs-lookup"><span data-stu-id="df12b-170">Select on **My apps**.</span></span> 

1. <span data-ttu-id="df12b-171">Find the LUIS app you previously created, that contains the intents and entities from the HomeAutomation domain.</span><span class="sxs-lookup"><span data-stu-id="df12b-171">Find the LUIS app you previously created, that contains the intents and entities from the HomeAutomation domain.</span></span>

2. <span data-ttu-id="df12b-172">In the **Settings** page for the LUIS app, find and copy the app ID.</span><span class="sxs-lookup"><span data-stu-id="df12b-172">In the **Settings** page for the LUIS app, find and copy the app ID.</span></span>

3. <span data-ttu-id="df12b-173">If you haven't trained the app, select the **Train** button in the upper right to train your app.</span><span class="sxs-lookup"><span data-stu-id="df12b-173">If you haven't trained the app, select the **Train** button in the upper right to train your app.</span></span>

4. <span data-ttu-id="df12b-174">If you haven't published the app, select **PUBLISH** in the top navigation bar to open the **Publish** page.</span><span class="sxs-lookup"><span data-stu-id="df12b-174">If you haven't published the app, select **PUBLISH** in the top navigation bar to open the **Publish** page.</span></span> <span data-ttu-id="df12b-175">Select the Production slot and the **Publish** button.</span><span class="sxs-lookup"><span data-stu-id="df12b-175">Select the Production slot and the **Publish** button.</span></span>

## <a name="modify-the-bot-code"></a><span data-ttu-id="df12b-176">Modify the bot code</span><span class="sxs-lookup"><span data-stu-id="df12b-176">Modify the bot code</span></span>

<span data-ttu-id="df12b-177">Go to the second browser window if it is still open or in the first browser window, select **Build** and then select **Open online code editor**.</span><span class="sxs-lookup"><span data-stu-id="df12b-177">Go to the second browser window if it is still open or in the first browser window, select **Build** and then select **Open online code editor**.</span></span>

   ![Open online code editor](./media/luis-tutorial-node-bot/bot-service-build.png)

<span data-ttu-id="df12b-179">In the code editor, open `app.js`.</span><span class="sxs-lookup"><span data-stu-id="df12b-179">In the code editor, open `app.js`.</span></span> <span data-ttu-id="df12b-180">It contains the following code:</span><span class="sxs-lookup"><span data-stu-id="df12b-180">It contains the following code:</span></span>

```javascript
/*-----------------------------------------------------------------------------
A simple Language Understanding (LUIS) bot for the Microsoft Bot Framework. 
-----------------------------------------------------------------------------*/

var restify = require('restify');
var builder = require('botbuilder');
var botbuilder_azure = require("botbuilder-azure");

// Setup Restify Server
var server = restify.createServer();
server.listen(process.env.port || process.env.PORT || 3978, function () {
   console.log('%s listening to %s', server.name, server.url); 
});
  
// Create chat connector for communicating with the Bot Framework Service
var connector = new builder.ChatConnector({
    appId: process.env.MicrosoftAppId,
    appPassword: process.env.MicrosoftAppPassword,
    openIdMetadata: process.env.BotOpenIdMetadata 
});

// Listen for messages from users 
server.post('/api/messages', connector.listen());

/*----------------------------------------------------------------------------------------
* Bot Storage: This is a great spot to register the private state storage for your bot. 
* We provide adapters for Azure Table, CosmosDb, SQL Azure, or you can implement your own!
* For samples and documentation, see: https://github.com/Microsoft/BotBuilder-Azure
* ---------------------------------------------------------------------------------------- */

var tableName = 'botdata';
var azureTableClient = new botbuilder_azure.AzureTableClient(tableName, process.env['AzureWebJobsStorage']);
var tableStorage = new botbuilder_azure.AzureBotStorage({ gzipData: false }, azureTableClient);

// Create your bot with a function to receive messages from the user
// This default message handler is invoked if the user's utterance doesn't
// match any intents handled by other dialogs.
var bot = new builder.UniversalBot(connector, function (session, args) {
    session.send('You reached the default message handler. You said \'%s\'.', session.message.text);
});

bot.set('storage', tableStorage);

// Make sure you add code to validate these fields
var luisAppId = process.env.LuisAppId;
var luisAPIKey = process.env.LuisAPIKey;
var luisAPIHostName = process.env.LuisAPIHostName || 'westus.api.cognitive.microsoft.com';

const LuisModelUrl = 'https://' + luisAPIHostName + '/luis/v2.0/apps/' + luisAppId + '?subscription-key=' + luisAPIKey;

// Create a recognizer that gets intents from LUIS, and add it to the bot
var recognizer = new builder.LuisRecognizer(LuisModelUrl);
bot.recognizer(recognizer);

// Add a dialog for each intent that the LUIS app recognizes.
// See https://docs.microsoft.com/bot-framework/nodejs/bot-builder-nodejs-recognize-intent-luis 
bot.dialog('GreetingDialog',
    (session) => {
        session.send('You reached the Greeting intent. You said \'%s\'.', session.message.text);
        session.endDialog();
    }
).triggerAction({
    matches: 'Greeting'
})

bot.dialog('HelpDialog',
    (session) => {
        session.send('You reached the Help intent. You said \'%s\'.', session.message.text);
        session.endDialog();
    }
).triggerAction({
    matches: 'Help'
})

bot.dialog('CancelDialog',
    (session) => {
        session.send('You reached the Cancel intent. You said \'%s\'.', session.message.text);
        session.endDialog();
    }
).triggerAction({
    matches: 'Cancel'
})
```

<span data-ttu-id="df12b-181">The existing intents in the app.js are ignored.</span><span class="sxs-lookup"><span data-stu-id="df12b-181">The existing intents in the app.js are ignored.</span></span> <span data-ttu-id="df12b-182">You can leave them.</span><span class="sxs-lookup"><span data-stu-id="df12b-182">You can leave them.</span></span> 

## <a name="add-a-dialog-that-matches-homeautomationturnon"></a><span data-ttu-id="df12b-183">Add a dialog that matches HomeAutomation.TurnOn</span><span class="sxs-lookup"><span data-stu-id="df12b-183">Add a dialog that matches HomeAutomation.TurnOn</span></span>

<span data-ttu-id="df12b-184">Copy the following code and add it to `app.js`.</span><span class="sxs-lookup"><span data-stu-id="df12b-184">Copy the following code and add it to `app.js`.</span></span>

```javascript
bot.dialog('TurnOn',
    (session) => {
        session.send('You reached the TurnOn intent. You said \'%s\'.', session.message.text);
        session.endDialog();
    }
).triggerAction({
    matches: 'HomeAutomation.TurnOn'
})
```

<span data-ttu-id="df12b-185">The [matches][matches] option on the [triggerAction][triggerAction] attached to the dialog specifies the name of the intent.</span><span class="sxs-lookup"><span data-stu-id="df12b-185">The [matches][matches] option on the [triggerAction][triggerAction] attached to the dialog specifies the name of the intent.</span></span> <span data-ttu-id="df12b-186">The recognizer runs each time the bot receives an utterance from the user.</span><span class="sxs-lookup"><span data-stu-id="df12b-186">The recognizer runs each time the bot receives an utterance from the user.</span></span> <span data-ttu-id="df12b-187">If the highest scoring intent that it detects matches a `triggerAction` bound to a dialog, the bot invokes that dialog.</span><span class="sxs-lookup"><span data-stu-id="df12b-187">If the highest scoring intent that it detects matches a `triggerAction` bound to a dialog, the bot invokes that dialog.</span></span>

## <a name="add-a-dialog-that-matches-homeautomationturnoff"></a><span data-ttu-id="df12b-188">Add a dialog that matches HomeAutomation.TurnOff</span><span class="sxs-lookup"><span data-stu-id="df12b-188">Add a dialog that matches HomeAutomation.TurnOff</span></span>

<span data-ttu-id="df12b-189">Copy the following code and add it to `app.js`.</span><span class="sxs-lookup"><span data-stu-id="df12b-189">Copy the following code and add it to `app.js`.</span></span>

```javascript
bot.dialog('TurnOff',
    (session) => {
        session.send('You reached the TurnOff intent. You said \'%s\'.', session.message.text);
        session.endDialog();
    }
).triggerAction({
    matches: 'HomeAutomation.TurnOff'
})
```
## <a name="test-the-bot"></a><span data-ttu-id="df12b-190">Test the bot</span><span class="sxs-lookup"><span data-stu-id="df12b-190">Test the bot</span></span>

<span data-ttu-id="df12b-191">In the Azure Portal, select on **Test in Web Chat** to test the bot.</span><span class="sxs-lookup"><span data-stu-id="df12b-191">In the Azure Portal, select on **Test in Web Chat** to test the bot.</span></span> <span data-ttu-id="df12b-192">Try type messages like "Turn on the lights", and "turn off my heater" to invoke the intents that you added to it.</span><span class="sxs-lookup"><span data-stu-id="df12b-192">Try type messages like "Turn on the lights", and "turn off my heater" to invoke the intents that you added to it.</span></span>
   <span data-ttu-id="df12b-193">![Test HomeAutomation bot in Web Chat](./media/luis-tutorial-node-bot/bot-service-chat-results.png)</span><span class="sxs-lookup"><span data-stu-id="df12b-193">![Test HomeAutomation bot in Web Chat](./media/luis-tutorial-node-bot/bot-service-chat-results.png)</span></span>

> [!TIP]
> <span data-ttu-id="df12b-194">If you find that your bot doesn't always recognize the correct intent or entities, improve your LUIS app's performance by giving it more example utterances to train it.</span><span class="sxs-lookup"><span data-stu-id="df12b-194">If you find that your bot doesn't always recognize the correct intent or entities, improve your LUIS app's performance by giving it more example utterances to train it.</span></span> <span data-ttu-id="df12b-195">You can retrain your LUIS app without any modification to your bot's code.</span><span class="sxs-lookup"><span data-stu-id="df12b-195">You can retrain your LUIS app without any modification to your bot's code.</span></span> <span data-ttu-id="df12b-196">See [Add example utterances](https://docs.microsoft.com/azure/cognitive-services/LUIS/add-example-utterances) and [train and test your LUIS app](https://docs.microsoft.com/azure/cognitive-services/LUIS/luis-interactive-test).</span><span class="sxs-lookup"><span data-stu-id="df12b-196">See [Add example utterances](https://docs.microsoft.com/azure/cognitive-services/LUIS/add-example-utterances) and [train and test your LUIS app](https://docs.microsoft.com/azure/cognitive-services/LUIS/luis-interactive-test).</span></span>

## <a name="learn-more-about-bot-framework"></a><span data-ttu-id="df12b-197">Learn more about Bot Framework</span><span class="sxs-lookup"><span data-stu-id="df12b-197">Learn more about Bot Framework</span></span>
<span data-ttu-id="df12b-198">Learn more about [Bot Framework](https://dev.botframework.com/) and the [3.x](https://github.com/Microsoft/BotBuilder) and [4.x](https://github.com/Microsoft/botbuilder-js) SDKs.</span><span class="sxs-lookup"><span data-stu-id="df12b-198">Learn more about [Bot Framework](https://dev.botframework.com/) and the [3.x](https://github.com/Microsoft/BotBuilder) and [4.x](https://github.com/Microsoft/botbuilder-js) SDKs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="df12b-199">Next steps</span><span class="sxs-lookup"><span data-stu-id="df12b-199">Next steps</span></span>

<span data-ttu-id="df12b-200"><!-- From trying the bot, you can see that the recognizer can trigger interruption of the currently active dialog. Allowing and handling interruptions is a flexible design that accounts for what users really do. Learn more about the various actions you can associate with a recognized intent.--> You can try to add other intents, like Help, Cancel, and Greeting, to the LUIS app.</span><span class="sxs-lookup"><span data-stu-id="df12b-200"><!-- From trying the bot, you can see that the recognizer can trigger interruption of the currently active dialog. Allowing and handling interruptions is a flexible design that accounts for what users really do. Learn more about the various actions you can associate with a recognized intent.--> You can try to add other intents, like Help, Cancel, and Greeting, to the LUIS app.</span></span> <span data-ttu-id="df12b-201">Then add dialogs for the new intents and test them using the bot.</span><span class="sxs-lookup"><span data-stu-id="df12b-201">Then add dialogs for the new intents and test them using the bot.</span></span> 

<!-- 
> [!NOTE] 
> The default LUIS app that the template created contains example utterances for Cancel, Greeting, and Help intents. In the list of apps, find the app that begins with the name specified in **App name** in the **Bot Service** blade when you created the Bot Service. -->

> [!div class="nextstepaction"]
> <span data-ttu-id="df12b-202">[Add intents](./luis-how-to-add-intents.md)
> [Speech priming](https://docs.microsoft.com/bot-framework/bot-service-manage-speech-priming)</span><span class="sxs-lookup"><span data-stu-id="df12b-202">[Add intents](./luis-how-to-add-intents.md)
[Speech priming](https://docs.microsoft.com/bot-framework/bot-service-manage-speech-priming)</span></span>


[intentDialog]: https://docs.botframework.com/node/builder/chat-reference/classes/_botbuilder_d_.intentdialog.html

[intentDialog_matches]: https://docs.botframework.com/node/builder/chat-reference/classes/_botbuilder_d_.intentdialog.html#matches 

[NotesSample]: https://github.com/Microsoft/BotFramework-Samples/tree/master/docs-samples/Node/basics-naturalLanguage

[triggerAction]: https://docs.botframework.com/en-us/node/builder/chat-reference/classes/_botbuilder_d_.dialog.html#triggeraction

[confirmPrompt]: https://docs.botframework.com/node/builder/chat-reference/interfaces/_botbuilder_d_.itriggeractionoptions.html#confirmprompt

[waterfall]: bot-builder-nodejs-dialog-manage-conversation-flow.md#manage-conversation-flow-with-a-waterfall

[session_userData]: https://docs.botframework.com/node/builder/chat-reference/classes/_botbuilder_d_.session.html#userdata

[EntityRecognizer_findEntity]: https://docs.botframework.com/node/builder/chat-reference/classes/_botbuilder_d_.entityrecognizer.html#findentity

[matches]: https://docs.botframework.com/en-us/node/builder/chat-reference/interfaces/_botbuilder_d_.itriggeractionoptions.html#matches

[LUISAzureDocs]: https://docs.microsoft.com/azure/cognitive-services/LUIS/Home

[Dialog]: https://docs.botframework.com/node/builder/chat-reference/classes/_botbuilder_d_.dialog.html

[IntentRecognizerSetOptions]: https://docs.botframework.com/node/builder/chat-reference/interfaces/_botbuilder_d_.iintentrecognizersetoptions.html

[LuisRecognizer]: https://docs.botframework.com/node/builder/chat-reference/classes/_botbuilder_d_.luisrecognizer

[LUISConcepts]: https://docs.botframework.com/node/builder/guides/understanding-natural-language/

[DisambiguationSample]: https://github.com/Microsoft/BotBuilder/tree/master/Node/examples/feature-onDisambiguateRoute

[IDisambiguateRouteHandler]: https://docs.botframework.com/node/builder/chat-reference/interfaces/_botbuilder_d_.idisambiguateroutehandler.html

[RegExpRecognizer]: https://docs.botframework.com/node/builder/chat-reference/classes/_botbuilder_d_.regexprecognizer.html

[AlarmBot]: https://github.com/Microsoft/BotBuilder/blob/master/Node/examples/basics-naturalLanguage/app.js

[LUISBotSample]: https://github.com/Microsoft/BotBuilder-Samples/tree/master/Node/intelligence-LUIS

[UniversalBot]: https://docs.botframework.com/node/builder/chat-reference/classes/_botbuilder_d_.universalbot.html


<!-- Old Links -->
[Github-BotFramework-Emulator-Download]: https://aka.ms/bot-framework-emulator
[Github-LUIS-Samples]: https://github.com/Microsoft/LUIS-Samples
[Github-LUIS-Samples-node-hotel-bot]: https://github.com/Microsoft/LUIS-Samples/tree/master/bot-integration-samples/hotel-finder/nodejs
[NodeJs]: https://nodejs.org/
[BFPortal]: https://dev.botframework.com/
[RegisterInstructions]: https://docs.microsoft.com/bot-framework/portal-register-bot
[BotFramework]: https://docs.microsoft.com/bot-framework/
[LUIS]: https://docs.microsoft.com/azure/cognitive-services/luis/luis-reference-regions

