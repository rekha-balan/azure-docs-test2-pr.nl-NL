---
title: How to use cards with a Conversation Learner model, part 1 - Microsoft Cognitive Services | Microsoft Docs
titleSuffix: Azure
description: Learn how to use cards with a Conversation Learner model.
services: cognitive-services
author: v-jaswel
manager: nolachar
ms.service: cognitive-services
ms.component: conversation-learner
ms.topic: article
ms.date: 04/30/2018
ms.author: v-jaswel
ms.openlocfilehash: 988a2433f098f41bca4796299825293efd4de44b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870114"
---
# <a name="how-to-use-cards-part-1-of-2"></a>How to use cards (part 1 of 2)

This tutorial shows how to add and use a simple card in your bot.

> [!NOTE]
> Currently Conversation Learner expects your card definition files to be located in a directory called "cards" which is present in the directory where the bot is started. We will make this configurable in the future.

## <a name="video"></a>Video

[![Tutorial 13 Preview](http://aka.ms/cl-tutorial-13-preview)](http://aka.ms/blis-tutorial-13)

## <a name="requirements"></a>Requirements
This tutorial requires that the general tutorial bot is running

    npm run tutorial-general

## <a name="details"></a>Details

Cards are UI elements that allow the user to select an option in the conversation. 

### <a name="open-the-demo"></a>Open the demo

In the Model list of the web UI, click on Tutorial-13-Cards-1. 

### <a name="the-card"></a>The Card

The card definition is at the following location: C:\<installedpath\>\src\cards\prompt.json.

The system expects to find your card definitions in this cards directory.

![](../media/tutorial13_prompt.PNG)

> [!NOTE]
> Notice the body type `TextBlock` and the `{{question}}` placeholder in the text field.
> There are two submit buttons and the text that gets submitted for each.

### <a name="actions"></a>Actions

We have created three actions. As you see below, the first action is a card.

![](../media/tutorial13_actions.PNG)

Let's see how the card action type was created:

![](../media/tutorial13_cardaction.PNG)

> [!NOTE]
> The question input, and buttons 1 and 2. Those are template references in the card where you enter the question and the respective answers. You can also reference and use entities or a mixture of text and entities.

The eye icon shows you what the card looks like.

### <a name="train-dialog"></a>Train Dialog

Let's walk through a teaching dialog.

1. Click Train Dialogs, then New Train Dialog.
1. Enter 'hi'.
2. Click Score Action.
3. Click to Select 'Prompt go left or right'.
    - Clicking 'left' or 'right' is equivalent to user typing in 'left' or 'right' respectively. 
4. Click Score Actions.
4. Click to Select 'left'. This is a non-wait action.
6. Click to Select 'Prompt go left or right'.
4. Click 'right'.
5. Click Score Actions.
3. Click to Select 'Right'
6. Click to Select 'Prompt go left or right'.
4. Click Done Testing.

You have now seen how cards work. They are defined in the cards directory as json templates. The templates will surface in the UI which you can populate using a string or an entity or a mix of both.

## <a name="next-steps"></a>Next steps

> [!div class="nextstepaction"]
> [Cards part 2](./14-cards-2.md)
