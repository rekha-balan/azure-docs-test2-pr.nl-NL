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
# <a name="how-to-use-versioning-and-tagging"></a>How to use versioning and tagging

This tutorial illustrates how to tag versions of your Conversation Learner model, and set which version is “live”.  

## <a name="requirements"></a>Requirements
This tutorial requires using the bot emulator to create log dialogs, not the Log Dialog Web UI.  

This tutorial requires that the general tutorial bot is running:

    npm run tutorial-general

## <a name="details"></a>Details

When editing, you are always editing the tag called “master” -- you can create tagged versions from master (which essentially take a snapshot of master), but you cannot edit tagged versions.

## <a name="steps"></a>Steps

### <a name="install-the-bot-framework-emulator"></a>Install the Bot framework emulator

- Go to [https://github.com/Microsoft/BotFramework-Emulator](https://github.com/Microsoft/BotFramework-Emulator).
- Download and install the emulator.

### <a name="create-an-model"></a>Create an model

1. Click New Model
2. In the Name field, enter Tutorial-16-Versioning
3. Click Create 
4. Click Settings
5. Copy the Model ID

### <a name="configure-the-emulator"></a>Configure the emulator

- In the Conversation Learner root folder, open the .env file.
- Paste the Model ID as the value of CONVERSATION_LEARNER_MODEL_ID
- Restart the Conversation Learner service by exiting from the command prompt, and rerunning:
 
    npm run tutorial-general 

### <a name="actions"></a>Actions

Let's create an action:

1. Switch to the Web UI.
1. Click Actions, then New Action.
2. In Response, enter “hi there (version 1)”.
3. Click Save.


![](../media/tutorial16_action1.PNG)

Create a new tag:

3. Click on “settings” and create a new “tag”.
    - Call it “version 1”
4. Set “version 1” to be “live”.  
    - The effect of setting the live tag to "version 1" is that channels using this bot will use the “version 1” tag.
    - Tagged versions of models are not affected by edits (changing actions, entities, adding train dialogs).  
    - Edits to an model (changing actions, entities, adding train dialogs) are always made on the "master" tag.  In other words, "master" is the only tag that can change; other tags are fixed snapshots.
    - Log dialogs in the Conversation Learner UI always use master (not the live tag).

![](../media/tutorial16_v1_create.PNG)

The version has been created in settings:

![](../media/tutorial16_settings.PNG)

Let's add a second action:

1. Click Actions, then New Action.
2. In Response, enter “bye bye (version 2)”.

Edit the first action:

1. Click Actions.
2. Under Actions, click on "hi there (version 1)".
3. Change the Response to "hi there (version 2)".

![](../media/tutorial16_hi_there_v2.PNG)

### <a name="switch-to-the-bot-emulator"></a>Switch to the bot emulator

1. In the bot UI, enter "goodbye".
2. The bot responds with "hi there (version 1)".
    - This shows the version 1 is "live". 

![](../media/tutorial16_bf_response.PNG)

### <a name="switch-to-the-web-ui"></a>Switch to the Web UI

1. Click on Log Dialogs (If you don't see any dialogs, click the refresh button).
2. Click on "hi there (version 2)"

> [!NOTE]
> We can make corrections by choosing from all currently available actions. These edits will be made to the master.

You have now seen how versioning works, and how you can interact with the bot using the Bot framework emulator.

## <a name="next-steps"></a>Next steps

> [!div class="nextstepaction"]
> [Demo - password reset](./demo-password-reset.md)
