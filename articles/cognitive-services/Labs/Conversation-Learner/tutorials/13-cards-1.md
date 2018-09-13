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
# <a name="how-to-use-cards-part-1-of-2"></a><span data-ttu-id="2fb08-103">How to use cards (part 1 of 2)</span><span class="sxs-lookup"><span data-stu-id="2fb08-103">How to use cards (part 1 of 2)</span></span>

<span data-ttu-id="2fb08-104">This tutorial shows how to add and use a simple card in your bot.</span><span class="sxs-lookup"><span data-stu-id="2fb08-104">This tutorial shows how to add and use a simple card in your bot.</span></span>

> [!NOTE]
> <span data-ttu-id="2fb08-105">Currently Conversation Learner expects your card definition files to be located in a directory called "cards" which is present in the directory where the bot is started.</span><span class="sxs-lookup"><span data-stu-id="2fb08-105">Currently Conversation Learner expects your card definition files to be located in a directory called "cards" which is present in the directory where the bot is started.</span></span> <span data-ttu-id="2fb08-106">We will make this configurable in the future.</span><span class="sxs-lookup"><span data-stu-id="2fb08-106">We will make this configurable in the future.</span></span>

## <a name="video"></a><span data-ttu-id="2fb08-107">Video</span><span class="sxs-lookup"><span data-stu-id="2fb08-107">Video</span></span>

<span data-ttu-id="2fb08-108">[![Tutorial 13 Preview](http://aka.ms/cl-tutorial-13-preview)](http://aka.ms/blis-tutorial-13)</span><span class="sxs-lookup"><span data-stu-id="2fb08-108">[![Tutorial 13 Preview](http://aka.ms/cl-tutorial-13-preview)](http://aka.ms/blis-tutorial-13)</span></span>

## <a name="requirements"></a><span data-ttu-id="2fb08-109">Requirements</span><span class="sxs-lookup"><span data-stu-id="2fb08-109">Requirements</span></span>
<span data-ttu-id="2fb08-110">This tutorial requires that the general tutorial bot is running</span><span class="sxs-lookup"><span data-stu-id="2fb08-110">This tutorial requires that the general tutorial bot is running</span></span>

    npm run tutorial-general

## <a name="details"></a><span data-ttu-id="2fb08-111">Details</span><span class="sxs-lookup"><span data-stu-id="2fb08-111">Details</span></span>

<span data-ttu-id="2fb08-112">Cards are UI elements that allow the user to select an option in the conversation.</span><span class="sxs-lookup"><span data-stu-id="2fb08-112">Cards are UI elements that allow the user to select an option in the conversation.</span></span> 

### <a name="open-the-demo"></a><span data-ttu-id="2fb08-113">Open the demo</span><span class="sxs-lookup"><span data-stu-id="2fb08-113">Open the demo</span></span>

<span data-ttu-id="2fb08-114">In the Model list of the web UI, click on Tutorial-13-Cards-1.</span><span class="sxs-lookup"><span data-stu-id="2fb08-114">In the Model list of the web UI, click on Tutorial-13-Cards-1.</span></span> 

### <a name="the-card"></a><span data-ttu-id="2fb08-115">The Card</span><span class="sxs-lookup"><span data-stu-id="2fb08-115">The Card</span></span>

<span data-ttu-id="2fb08-116">The card definition is at the following location: C:\<installedpath\>\src\cards\prompt.json.</span><span class="sxs-lookup"><span data-stu-id="2fb08-116">The card definition is at the following location: C:\<installedpath\>\src\cards\prompt.json.</span></span>

<span data-ttu-id="2fb08-117">The system expects to find your card definitions in this cards directory.</span><span class="sxs-lookup"><span data-stu-id="2fb08-117">The system expects to find your card definitions in this cards directory.</span></span>

![](../media/tutorial13_prompt.PNG)

> [!NOTE]
> <span data-ttu-id="2fb08-118">Notice the body type `TextBlock` and the `{{question}}` placeholder in the text field.</span><span class="sxs-lookup"><span data-stu-id="2fb08-118">Notice the body type `TextBlock` and the `{{question}}` placeholder in the text field.</span></span>
> <span data-ttu-id="2fb08-119">There are two submit buttons and the text that gets submitted for each.</span><span class="sxs-lookup"><span data-stu-id="2fb08-119">There are two submit buttons and the text that gets submitted for each.</span></span>

### <a name="actions"></a><span data-ttu-id="2fb08-120">Actions</span><span class="sxs-lookup"><span data-stu-id="2fb08-120">Actions</span></span>

<span data-ttu-id="2fb08-121">We have created three actions.</span><span class="sxs-lookup"><span data-stu-id="2fb08-121">We have created three actions.</span></span> <span data-ttu-id="2fb08-122">As you see below, the first action is a card.</span><span class="sxs-lookup"><span data-stu-id="2fb08-122">As you see below, the first action is a card.</span></span>

![](../media/tutorial13_actions.PNG)

<span data-ttu-id="2fb08-123">Let's see how the card action type was created:</span><span class="sxs-lookup"><span data-stu-id="2fb08-123">Let's see how the card action type was created:</span></span>

![](../media/tutorial13_cardaction.PNG)

> [!NOTE]
> <span data-ttu-id="2fb08-124">The question input, and buttons 1 and 2.</span><span class="sxs-lookup"><span data-stu-id="2fb08-124">The question input, and buttons 1 and 2.</span></span> <span data-ttu-id="2fb08-125">Those are template references in the card where you enter the question and the respective answers.</span><span class="sxs-lookup"><span data-stu-id="2fb08-125">Those are template references in the card where you enter the question and the respective answers.</span></span> <span data-ttu-id="2fb08-126">You can also reference and use entities or a mixture of text and entities.</span><span class="sxs-lookup"><span data-stu-id="2fb08-126">You can also reference and use entities or a mixture of text and entities.</span></span>

<span data-ttu-id="2fb08-127">The eye icon shows you what the card looks like.</span><span class="sxs-lookup"><span data-stu-id="2fb08-127">The eye icon shows you what the card looks like.</span></span>

### <a name="train-dialog"></a><span data-ttu-id="2fb08-128">Train Dialog</span><span class="sxs-lookup"><span data-stu-id="2fb08-128">Train Dialog</span></span>

<span data-ttu-id="2fb08-129">Let's walk through a teaching dialog.</span><span class="sxs-lookup"><span data-stu-id="2fb08-129">Let's walk through a teaching dialog.</span></span>

1. <span data-ttu-id="2fb08-130">Click Train Dialogs, then New Train Dialog.</span><span class="sxs-lookup"><span data-stu-id="2fb08-130">Click Train Dialogs, then New Train Dialog.</span></span>
1. <span data-ttu-id="2fb08-131">Enter 'hi'.</span><span class="sxs-lookup"><span data-stu-id="2fb08-131">Enter 'hi'.</span></span>
2. <span data-ttu-id="2fb08-132">Click Score Action.</span><span class="sxs-lookup"><span data-stu-id="2fb08-132">Click Score Action.</span></span>
3. <span data-ttu-id="2fb08-133">Click to Select 'Prompt go left or right'.</span><span class="sxs-lookup"><span data-stu-id="2fb08-133">Click to Select 'Prompt go left or right'.</span></span>
    - <span data-ttu-id="2fb08-134">Clicking 'left' or 'right' is equivalent to user typing in 'left' or 'right' respectively.</span><span class="sxs-lookup"><span data-stu-id="2fb08-134">Clicking 'left' or 'right' is equivalent to user typing in 'left' or 'right' respectively.</span></span> 
4. <span data-ttu-id="2fb08-135">Click Score Actions.</span><span class="sxs-lookup"><span data-stu-id="2fb08-135">Click Score Actions.</span></span>
4. <span data-ttu-id="2fb08-136">Click to Select 'left'.</span><span class="sxs-lookup"><span data-stu-id="2fb08-136">Click to Select 'left'.</span></span> <span data-ttu-id="2fb08-137">This is a non-wait action.</span><span class="sxs-lookup"><span data-stu-id="2fb08-137">This is a non-wait action.</span></span>
6. <span data-ttu-id="2fb08-138">Click to Select 'Prompt go left or right'.</span><span class="sxs-lookup"><span data-stu-id="2fb08-138">Click to Select 'Prompt go left or right'.</span></span>
4. <span data-ttu-id="2fb08-139">Click 'right'.</span><span class="sxs-lookup"><span data-stu-id="2fb08-139">Click 'right'.</span></span>
5. <span data-ttu-id="2fb08-140">Click Score Actions.</span><span class="sxs-lookup"><span data-stu-id="2fb08-140">Click Score Actions.</span></span>
3. <span data-ttu-id="2fb08-141">Click to Select 'Right'</span><span class="sxs-lookup"><span data-stu-id="2fb08-141">Click to Select 'Right'</span></span>
6. <span data-ttu-id="2fb08-142">Click to Select 'Prompt go left or right'.</span><span class="sxs-lookup"><span data-stu-id="2fb08-142">Click to Select 'Prompt go left or right'.</span></span>
4. <span data-ttu-id="2fb08-143">Click Done Testing.</span><span class="sxs-lookup"><span data-stu-id="2fb08-143">Click Done Testing.</span></span>

<span data-ttu-id="2fb08-144">You have now seen how cards work.</span><span class="sxs-lookup"><span data-stu-id="2fb08-144">You have now seen how cards work.</span></span> <span data-ttu-id="2fb08-145">They are defined in the cards directory as json templates.</span><span class="sxs-lookup"><span data-stu-id="2fb08-145">They are defined in the cards directory as json templates.</span></span> <span data-ttu-id="2fb08-146">The templates will surface in the UI which you can populate using a string or an entity or a mix of both.</span><span class="sxs-lookup"><span data-stu-id="2fb08-146">The templates will surface in the UI which you can populate using a string or an entity or a mix of both.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2fb08-147">Next steps</span><span class="sxs-lookup"><span data-stu-id="2fb08-147">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2fb08-148">Cards part 2</span><span class="sxs-lookup"><span data-stu-id="2fb08-148">Cards part 2</span></span>](./14-cards-2.md)
