---
title: How to use cards with a Conversation Learner model, part 2 - Microsoft Cognitive Services | Microsoft Docs
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
ms.openlocfilehash: 1c7c88742c69041594006add76f7e3c642c64dec
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865016"
---
# <a name="how-to-use-cards-part-1-of-2"></a><span data-ttu-id="65356-103">How to use cards (part 1 of 2)</span><span class="sxs-lookup"><span data-stu-id="65356-103">How to use cards (part 1 of 2)</span></span>
<span data-ttu-id="65356-104">This tutorial shows how to add a fillable form card to your bot.</span><span class="sxs-lookup"><span data-stu-id="65356-104">This tutorial shows how to add a fillable form card to your bot.</span></span> <span data-ttu-id="65356-105">It will show how form fields move into entities.</span><span class="sxs-lookup"><span data-stu-id="65356-105">It will show how form fields move into entities.</span></span>

<span data-ttu-id="65356-106">Conversation Learner expects your card definition files to be located in a directory called "cards", which is present in the directory where the bot is started.</span><span class="sxs-lookup"><span data-stu-id="65356-106">Conversation Learner expects your card definition files to be located in a directory called "cards", which is present in the directory where the bot is started.</span></span>

## <a name="video"></a><span data-ttu-id="65356-107">Video</span><span class="sxs-lookup"><span data-stu-id="65356-107">Video</span></span>

<span data-ttu-id="65356-108">[![Tutorial 14 Preview](http://aka.ms/cl-tutorial-14-preview)](http://aka.ms/blis-tutorial-14)</span><span class="sxs-lookup"><span data-stu-id="65356-108">[![Tutorial 14 Preview](http://aka.ms/cl-tutorial-14-preview)](http://aka.ms/blis-tutorial-14)</span></span>

## <a name="requirements"></a><span data-ttu-id="65356-109">Requirements</span><span class="sxs-lookup"><span data-stu-id="65356-109">Requirements</span></span>
<span data-ttu-id="65356-110">This tutorial requires that the general tutorial bot is running</span><span class="sxs-lookup"><span data-stu-id="65356-110">This tutorial requires that the general tutorial bot is running</span></span>

    npm run tutorial-general

## <a name="details"></a><span data-ttu-id="65356-111">Details</span><span class="sxs-lookup"><span data-stu-id="65356-111">Details</span></span>

<span data-ttu-id="65356-112">Cards are UI elements that allow the user to select an option in the conversation.</span><span class="sxs-lookup"><span data-stu-id="65356-112">Cards are UI elements that allow the user to select an option in the conversation.</span></span> 

### <a name="open-the-demo"></a><span data-ttu-id="65356-113">Open the demo</span><span class="sxs-lookup"><span data-stu-id="65356-113">Open the demo</span></span>

<span data-ttu-id="65356-114">In the Model list of the web UI, click on Tutorial-14-Cards-2.</span><span class="sxs-lookup"><span data-stu-id="65356-114">In the Model list of the web UI, click on Tutorial-14-Cards-2.</span></span> 

### <a name="the-card"></a><span data-ttu-id="65356-115">The Card</span><span class="sxs-lookup"><span data-stu-id="65356-115">The Card</span></span>

<span data-ttu-id="65356-116">The card definition is at the following location: C:\<installedpath\>\src\cards\shippingAddress.json.</span><span class="sxs-lookup"><span data-stu-id="65356-116">The card definition is at the following location: C:\<installedpath\>\src\cards\shippingAddress.json.</span></span>

<span data-ttu-id="65356-117">This card collects three fields of the shipping address: city, street, and state.</span><span class="sxs-lookup"><span data-stu-id="65356-117">This card collects three fields of the shipping address: city, street, and state.</span></span>

![](../media/tutorial14_card.PNG)

### <a name="actions"></a><span data-ttu-id="65356-118">Actions</span><span class="sxs-lookup"><span data-stu-id="65356-118">Actions</span></span>

<span data-ttu-id="65356-119">We have created three actions.</span><span class="sxs-lookup"><span data-stu-id="65356-119">We have created three actions.</span></span> <span data-ttu-id="65356-120">As you see below, the first action is a card.</span><span class="sxs-lookup"><span data-stu-id="65356-120">As you see below, the first action is a card.</span></span>

![](../media/tutorial14_actions.PNG)

<span data-ttu-id="65356-121">Let's see how the card action type was created:</span><span class="sxs-lookup"><span data-stu-id="65356-121">Let's see how the card action type was created:</span></span>

- <span data-ttu-id="65356-122">Notice Address-Street, where the type is of Input.text and its ID.</span><span class="sxs-lookup"><span data-stu-id="65356-122">Notice Address-Street, where the type is of Input.text and its ID.</span></span>
- <span data-ttu-id="65356-123">Similarly, there is Address-City and a drop-down with ID of Address-State.</span><span class="sxs-lookup"><span data-stu-id="65356-123">Similarly, there is Address-City and a drop-down with ID of Address-State.</span></span>

<span data-ttu-id="65356-124">The Ids are important as when the fields are populated and submitted, those are the entity names that will receive those values in the bot.</span><span class="sxs-lookup"><span data-stu-id="65356-124">The Ids are important as when the fields are populated and submitted, those are the entity names that will receive those values in the bot.</span></span>

## <a name="entities"></a><span data-ttu-id="65356-125">Entities</span><span class="sxs-lookup"><span data-stu-id="65356-125">Entities</span></span>
<span data-ttu-id="65356-126">We have defined three entities matching the card as we saw above.</span><span class="sxs-lookup"><span data-stu-id="65356-126">We have defined three entities matching the card as we saw above.</span></span>

![](../media/tutorial14_entities.PNG)

## <a name="actions"></a><span data-ttu-id="65356-127">Actions</span><span class="sxs-lookup"><span data-stu-id="65356-127">Actions</span></span>

<span data-ttu-id="65356-128">We have defined two actions.</span><span class="sxs-lookup"><span data-stu-id="65356-128">We have defined two actions.</span></span>

![](../media/tutorial14_actions.PNG)

- <span data-ttu-id="65356-129">The first is the shipping address card where the Action Type is CARD and Template is selected from the dropdown as shippingAddress.</span><span class="sxs-lookup"><span data-stu-id="65356-129">The first is the shipping address card where the Action Type is CARD and Template is selected from the dropdown as shippingAddress.</span></span>
- <span data-ttu-id="65356-130">The second is a simple action to read back the shipping address.</span><span class="sxs-lookup"><span data-stu-id="65356-130">The second is a simple action to read back the shipping address.</span></span>

![](../media/tutorial14_sa_card.PNG)

### <a name="train-dialog"></a><span data-ttu-id="65356-131">Train Dialog</span><span class="sxs-lookup"><span data-stu-id="65356-131">Train Dialog</span></span>

<span data-ttu-id="65356-132">Let's walk through a teaching dialog.</span><span class="sxs-lookup"><span data-stu-id="65356-132">Let's walk through a teaching dialog.</span></span>

1. <span data-ttu-id="65356-133">Click Train Dialogs, then New Train Dialog.</span><span class="sxs-lookup"><span data-stu-id="65356-133">Click Train Dialogs, then New Train Dialog.</span></span>
1. <span data-ttu-id="65356-134">Enter 'hi'.</span><span class="sxs-lookup"><span data-stu-id="65356-134">Enter 'hi'.</span></span>
2. <span data-ttu-id="65356-135">Click Score Action.</span><span class="sxs-lookup"><span data-stu-id="65356-135">Click Score Action.</span></span>
3. <span data-ttu-id="65356-136">Click to Select 'Shipping Address'.</span><span class="sxs-lookup"><span data-stu-id="65356-136">Click to Select 'Shipping Address'.</span></span>
4. <span data-ttu-id="65356-137">Fill in the card and submit.</span><span class="sxs-lookup"><span data-stu-id="65356-137">Fill in the card and submit.</span></span>
    - <span data-ttu-id="65356-138">Notice those values have now been moved into the entity memory.</span><span class="sxs-lookup"><span data-stu-id="65356-138">Notice those values have now been moved into the entity memory.</span></span> <span data-ttu-id="65356-139">No parsing is needed as the form already partitioned the inputs.</span><span class="sxs-lookup"><span data-stu-id="65356-139">No parsing is needed as the form already partitioned the inputs.</span></span>
5. <span data-ttu-id="65356-140">Click Score Actions.</span><span class="sxs-lookup"><span data-stu-id="65356-140">Click Score Actions.</span></span>
3. <span data-ttu-id="65356-141">Click to Select 'Shipping to $Address...".</span><span class="sxs-lookup"><span data-stu-id="65356-141">Click to Select 'Shipping to $Address...".</span></span>
4. <span data-ttu-id="65356-142">Click Done Testing.</span><span class="sxs-lookup"><span data-stu-id="65356-142">Click Done Testing.</span></span>

![](../media/tutorial14_train_dialog.PNG)

<span data-ttu-id="65356-143">You have now seen how to get values from the card that has fillable fields and dropdowns, and to capture and collect them in bot entities.</span><span class="sxs-lookup"><span data-stu-id="65356-143">You have now seen how to get values from the card that has fillable fields and dropdowns, and to capture and collect them in bot entities.</span></span>

## <a name="next-steps"></a><span data-ttu-id="65356-144">Next steps</span><span class="sxs-lookup"><span data-stu-id="65356-144">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="65356-145">Branching and undo</span><span class="sxs-lookup"><span data-stu-id="65356-145">Branching and undo</span></span>](./15-branching-and-undo.md)
