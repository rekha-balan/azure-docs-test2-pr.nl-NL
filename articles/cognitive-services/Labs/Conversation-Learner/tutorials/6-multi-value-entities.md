---
title: How to use multi-value entities with a Conversation Learner model - Microsoft Cognitive Services | Microsoft Docs
titleSuffix: Azure
description: Learn how to use multi-value entities with a Conversation Learner model.
services: cognitive-services
author: v-jaswel
manager: nolachar
ms.service: cognitive-services
ms.component: conversation-learner
ms.topic: article
ms.date: 04/30/2018
ms.author: v-jaswel
ms.openlocfilehash: 6193a515f0d8136e0d420b7554cf26fee8f50953
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865759"
---
# <a name="how-to-use-multi-value-entities-with-a-conversation-learner-model"></a>How to use multi-value entities with a Conversation Learner model
This tutorial shows the "multi-value" property of entities.

## <a name="video"></a>Video

[![Tutorial 6 Preview](http://aka.ms/cl-tutorial-06-preview)](http://aka.ms/blis-tutorial-06)

##<a name="requirements"></a>Requirements
This tutorial requires that the general tutorial bot is running

    npm run tutorial-general

## <a name="details"></a>Details
An entity which is "multi-value" accumulates values in a list, rather than storing a single value.  This is useful for entities where the user can specify more than one value, such as toppings on a pizza.

Concretely, if an entity is marked as "multi-value", then each recognized instance of the entity will be appended to a list in the bot's memory (rather than overwriting a single entity value).

## <a name="steps"></a>Steps

### <a name="create-the-model"></a>Create the model

1. In the Web UI, click New Model
2. In Name, enter MultiValueEntities. Then click Create.

### <a name="create-an-entity"></a>Create an entity

1. Click Entities, then New Entity.
2. In Entity Name, enter Toppings.
3. Check Multi-valued.
    - Multi-value entities accumulate one or more values in the entity.
2. Check Negatable.  
    - This will allow the user to remove toppings from their list of accumulated pizza toppings.
3. Click Create.

![](../media/tutorial6_entities.PNG)

### <a name="create-two-actions"></a>Create two actions

1. Click Actions, then New Action
2. In Response, type 'What toppings do you want?'.
3. In Disqualifying Entities, enter Toppings.
3. Click Create

Then create the second action.

1. Click Actions, then New Action to create a second action.
3. In Response, type 'Here are your toppings: $Toppings'.
4. Click Create

Now you have two actions.

![](../media/tutorial6_actions.PNG)

### <a name="train-the-bot"></a>Train the bot

1. Click Train Dialogs, then New Train Dialog.
2. Type 'hello'.
3. Click Score Actions, and Select 'What toppings do you want?'
2. Enter 'mushrooms and cheese'. 
    - You can label zero, one or more than one of the entities.
3. Click 'mushrooms', and select Toppings.
4. Click 'cheese', and select Toppings.
5. Click Score Actions
    - The two values are now present in the Toppings entity. 
6. Select 'Here are your toppings: $Toppings'.

We can add more to this:

7. Enter 'add peppers'.
    - Click on 'peppers' under Entity Detection, and select Toppings.
3. Click Score Actions.
    - 'peppers' now shows up as an additional value in Toppings.
6. Select 'Here are your toppings: $Toppings'.

Let's remove a topping and add one:

2. Type 'remove peppers and add sausage'.
1. Click on 'peppers' and click on the red x to remove it.
2. Click on 'peppers' and select '-Toppings'.
3. Click Score Actions.
    - 'peppers' has been deleted and 'sausage' has been added.
6. Select 'Here are your toppings: $Toppings'.

Now let's try removing everything:

6. Enter 'remove mushrooms, remove cheese, and remove sausage'.
7. Click on each of the three, and select '-Toppings'.
7. Click Score Actions.
    - All toppings are cleared.
2. Select 'What toppings do you want?'
3. Click Done Teaching

![](../media/tutorial6_dialogs.PNG)

## <a name="next-steps"></a>Next steps

> [!div class="nextstepaction"]
> [Built-in entities](./7-built-in-entities.md)
