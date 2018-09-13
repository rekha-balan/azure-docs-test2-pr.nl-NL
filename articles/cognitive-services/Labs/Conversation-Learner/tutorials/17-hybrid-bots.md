---
title: How to use Conversation Learner with other bot building technologies - Microsoft Cognitive Services | Microsoft Docs
titleSuffix: Azure
description: Learn how to use Conversation Learner with other bot building technologies.
services: cognitive-services
author: mattm
manager: larsliden
ms.service: cognitive-services
ms.component: conversation-learner
ms.topic: article
ms.date: 07/13/2018
ms.author: v-jaswel
ms.openlocfilehash: a03596ff8383a085314508d4a25d0ba89bcc3094
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870149"
---
# <a name="how-to-use-conversation-learner-with-other-bot-building-technologies"></a>How to use Conversation Learner with other bot building technologies

This tutorial covers how to use Conversation Learner with other bot building technologies and how memory (or state) can be shared between these technologies 

## <a name="video"></a>Video

[![Tutorial 15 Preview](http://aka.ms/cl-tutorial-15-preview)](http://aka.ms/blis-tutorial-15)

## <a name="requirements"></a>Requirements
This tutorial requires using the bot emulator to create log dialogs, not the Log Dialog Web UI.  

This tutorial requires that the hybrid tutorial bot is running:

    npm run tutorial-hybrid

## <a name="details"></a>Details

While Conversation Learner is in control, all state relative to the Conversation Learner Session must be stored in the Conversation Learner’s memory manager. This is necessary as the machine learning uses the state to determine how to drive the conversation. External state can be passed into the Conversation Learner in the OnSessionStartCallback that is called when the session begins. Internal can be returned out by the OnSessionEndCallback when the session terminates.

You can almost think of Conversation Learner as a function call that takes some initial state and returns values.

In this example, you will create a hybrid bot using two different systems:
1. A Conversation Learner Model <br />
Uses conversation learner model to determine the next action of the bot based on the current session.
This part of the bot takes one piece of initial state `isOpen` (which indicates whether a store is open or closed) and returns another piece of state `purchaseItem` (the name of an item the user purchases.)

2. Text matching <br />
Simply looks at incoming text for specific strings and responds.
This part of the bot manages the Bots' other storage mechanisms and is responsible for starting the CL session. Specifically it manages three variables: `usingConversationLearner`, `storeIsOpen`, and `purchaseItem`.

Let’s start by taking a look at the model used in this demo.

### <a name="open-the-demo"></a>Open the demo

In the model list of the web UI, click on Tutorial-15-Hybrid.

## <a name="entities"></a>Entities

Open the entities page and notice two entities: `isOpen` and `purchaseItem`

To understand how these entities are used, open the file: `C:\<installedpath\>\src\demos\tutorialHybrid.ts` to look at the callbacks.

Notice that the code in `OnSessionStartCallback` copies the value of `storeIsOpen` from BotBuilder conversation storage as the value of the `isOpen` entity so it is available to Conversation Learner. See the following code:

![](../media/tutorial17_sessionstart.PNG)

Likewise, the code in `OnSessionEndCallback` (if the session was ended due to a learned activity and not merely a timeout) copies the value of entity `purchaseItem` out to BotBuilder storage `purchaseItem`. See the following code:

![](../media/tutorial17_sessionend.PNG)

Now let's look at the Actions.

## <a name="actions"></a>Actions

Notice the model has four actions.

The intended rules for the actions are as follows:

- If the `isOpen` entity is set, the Bot will ask "What would you like to buy?" and store that in the `puchaseItem` slot
- If `isOpen` isn’t set, the Bot will say "I’m sorry we’re closed"
- The other two Actions are of the type `END_SESSION`.
- The END_SESSION Action indicates to ConversationLearner that the conversation has completed.

### <a name="overall-bot-logic"></a>Overall Bot Logic

First you see that if the Bot state’s `usingConversationLearner` flag has been set, we pass control to Conversation Learner. If not, we pass control to something else.  In this example, we’re showing simple text matching, but this could be any other Bot technology including LUIS, QnA maker and even another instance of Conversation Learner.

We need a way for the user to open and close the store, so we do a string compare with "open store" and "close store" and set the "storeIsOpen" flag.

Next, we need a way to trigger handing control over to our Conversation Learner Model. When we match to the "shop" string we do the following:
- Set the `usingConversationLearner` flag in the Bot’s memory.
- Call the "StartSession" method on our Conversation Learner Model.  This will trigger the "onSessionStartCallback" which will initialize the `isOpen` entity value

See below:

![](../media/tutorial17_useConversationLearner.PNG)

We also do a text match to "history" which will display that last purchase item.
Finally, if anything else is typed, we display the available user commands

## <a name="train-dialog"></a>Train Dialog

For this tutorial, the model is already pre-trained.  We will test the full bot to see the effect of the start and end session callbacks in practice.

## <a name="testing-the-bot"></a>Testing the Bot

Unlike single Conversation Leaner model bots you won’t be able to test this in the Conversation Learner UI as it can only show what’s handled by the Conversation Learner Model.

### <a name="install-the-bot-framework-emulator"></a>Install the Bot framework emulator

- Go to [https://github.com/Microsoft/BotFramework-Emulator](https://github.com/Microsoft/BotFramework-Emulator).
- Download and install the emulator.

### <a name="configure-the-emulator"></a>Configure the emulator

- Open the emulator and ensure the URL is targeting the same port your bot is running on. Likely: `http://localhost:3978/api/messages`

### <a name="test"></a>Test 

#### <a name="scenario-1-store-is-closed"></a>Scenario 1: Store is closed
1. Enter 'shop'. This is handled by the text matching and will give control to the Conversation Learner model.
2. Enter 'hello'.  Because `isOpen` value is not set, the bot will say "I’m sorry we’re closed" and end the session.

#### <a name="scenario-2-store-is-open"></a>Scenario 2: Store is open
3. Enter 'open store'.  This will set the `isOpen` to true.
4. Enter 'shop'.
5. Enter 'hello'.  Because `isOpen` value is set to true, the bot will say "What would you like to buy?"
6. Enter 'chair'. 'chair' will be saved into CL memory as the entity `purchaseItem`. The end session callback is invoked which copies this value out to the conversation store.
7. Enter 'history'.  The bot will say 'You bought chair' as this was your last `purchaseItem`.

## <a name="conclusion"></a>Conclusion

With what you have learned above you should be able to combine Conversation Learner with any other Bot technology
