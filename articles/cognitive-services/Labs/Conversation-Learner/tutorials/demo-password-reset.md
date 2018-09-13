---
title: Demo Conversation Learner model, password reset - Microsoft Cognitive Services | Microsoft Docs
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
ms.openlocfilehash: f633dd375d690a1c3e66a2a6e02ae69665dbe960
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865395"
---
# <a name="demo-password-reset"></a>Demo: Password reset
This demo illustrates a simple technical support bot that can help with password resets. 

It shows how Conversation Learner can learn non-trivial dialog flows, multi-turn sequences, including an out-of-domain class. This demonstration does not use any code or entities.

## <a name="video"></a>Video

[![Demo Password Preview](http://aka.ms/cl-demo-password-preview)](http://aka.ms/blis-demo-password)

## <a name="requirements"></a>Requirements
This tutorial requires that the password reset bot is running

    npm run demo-password

### <a name="open-the-demo"></a>Open the demo

In the Model list of the web UI, click on Tutorial Demo Password Reset. 

### <a name="actions"></a>Actions

We have created set of actions where the user is looking for help with their password including solutions.

![](../media/tutorial_pw_reset_actions.PNG)

### <a name="training-dialogs"></a>Training Dialogs

There are a number of training dialogs. There are also demonstrations of an out of domain class -- for example, user requests like 'driving directions' are out of domain; the bot has been given examples of a few out of domain requests and can respond with 'I can't help with that.'

![](../media/tutorial_pw_reset_entities.PNG)

As an example, let's try a teaching session.

1. Click Train Dialogs, then New Train Dialog.
1. Enter 'I lost my password'.
2. Click Score Action.
3. Click to Select 'Is that for your local account or Microsoft account?'
4. Enter 'Local account'.
5. Click Score Actions.
3. Click to Select 'Which version of Windows do you have?'
4. Enter 'Windows 8'.
5. click Score Actions.
6. Select 'SOLUTION: how to reset password on Windows 8.'
4. Click Done Teaching.

Let's try how the bot can learn an out-of-domain class.

1. Click Train Dialogs, then New Train Dialog.
1. Enter 'web search'.
    - This is an example of out-of-domain class. 
2. Click Score Action.
3. Click to Select 'Sorry, I can't help with that.'
    - Notice the score for this option is currently low. But after a little more teaching, the score will get higher.
4. Click Done Teaching.

You have now seen how to create a basic technical support demo, and how it can learn to provide solutions, and also handle out of sample queries.

## <a name="next-steps"></a>Next steps

> [!div class="nextstepaction"]
> [Demo - pizza order](./demo-pizza-order.md)
