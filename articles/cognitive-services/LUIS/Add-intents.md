---
title: Add intents in LUIS applications | Microsoft Docs
description: Use Language Understanding Intelligent Services (LUIS) to add intents to help apps understand user requests and react to them properly.
services: cognitive-services
author: cahann
manager: hsalama
ms.service: cognitive-services
ms.technology: luis
ms.topic: article
ms.date: 03/01/2017
ms.author: cahann
ms.openlocfilehash: 0f971f25e0de8be3fe4955ac66ff9e5903408ba9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554878"
---
# <a name="add-intents"></a><span data-ttu-id="c8f99-103">Add Intents</span><span class="sxs-lookup"><span data-stu-id="c8f99-103">Add Intents</span></span> 
<span data-ttu-id="c8f99-104">Intents are the intentions or desired actions conveyed through the utterances (sentences).</span><span class="sxs-lookup"><span data-stu-id="c8f99-104">Intents are the intentions or desired actions conveyed through the utterances (sentences).</span></span> <span data-ttu-id="c8f99-105">Intents match user requests with the actions that should be taken by your app.</span><span class="sxs-lookup"><span data-stu-id="c8f99-105">Intents match user requests with the actions that should be taken by your app.</span></span> <span data-ttu-id="c8f99-106">So, you must add intents to help your app understand user requests and react to them properly.</span><span class="sxs-lookup"><span data-stu-id="c8f99-106">So, you must add intents to help your app understand user requests and react to them properly.</span></span> 

<span data-ttu-id="c8f99-107">All applications come with the predefined intent, **"None"**.</span><span class="sxs-lookup"><span data-stu-id="c8f99-107">All applications come with the predefined intent, **"None"**.</span></span> <span data-ttu-id="c8f99-108">You should teach it to recognize user statements that are irrelevant to the app, for example if a user says "Get me a great cookie recipe" in a TravelAgent app.</span><span class="sxs-lookup"><span data-stu-id="c8f99-108">You should teach it to recognize user statements that are irrelevant to the app, for example if a user says "Get me a great cookie recipe" in a TravelAgent app.</span></span>

<span data-ttu-id="c8f99-109">You can add up to 80 intents in a single LUIS app.</span><span class="sxs-lookup"><span data-stu-id="c8f99-109">You can add up to 80 intents in a single LUIS app.</span></span> <span data-ttu-id="c8f99-110">You add and manage your intents from the **Intents** page that is accessed by clicking **Intents** in your application's left panel.</span><span class="sxs-lookup"><span data-stu-id="c8f99-110">You add and manage your intents from the **Intents** page that is accessed by clicking **Intents** in your application's left panel.</span></span> 

<span data-ttu-id="c8f99-111">In the following procedure, we'll start adding the "Bookflight" intent in the TravelAgent app as an example to explain the steps of adding an intent.</span><span class="sxs-lookup"><span data-stu-id="c8f99-111">In the following procedure, we'll start adding the "Bookflight" intent in the TravelAgent app as an example to explain the steps of adding an intent.</span></span>

<span data-ttu-id="c8f99-112">**To add intent:**</span><span class="sxs-lookup"><span data-stu-id="c8f99-112">**To add intent:**</span></span>

1. <span data-ttu-id="c8f99-113">Open your app (e.g. TravelAgent) by clicking its name on **My Apps** page, and then click **Intents** in the left panel.</span><span class="sxs-lookup"><span data-stu-id="c8f99-113">Open your app (e.g. TravelAgent) by clicking its name on **My Apps** page, and then click **Intents** in the left panel.</span></span> 
2. <span data-ttu-id="c8f99-114">On the **Intents** page, click **Add intent**.</span><span class="sxs-lookup"><span data-stu-id="c8f99-114">On the **Intents** page, click **Add intent**.</span></span>

    ![Intents List](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/IntentsList.JPG)
3. <span data-ttu-id="c8f99-116">In the **Add Intent** dialog box, type the intent name "BookFlight" and click **Save**.</span><span class="sxs-lookup"><span data-stu-id="c8f99-116">In the **Add Intent** dialog box, type the intent name "BookFlight" and click **Save**.</span></span>

    ![Add Intent](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/Addintent-dialogbox.JPG)

<span data-ttu-id="c8f99-118">This will take you directly to the intent details page of the newly added intent "Bookflight", like the screenshot below, in order to add utterances for this intent.</span><span class="sxs-lookup"><span data-stu-id="c8f99-118">This will take you directly to the intent details page of the newly added intent "Bookflight", like the screenshot below, in order to add utterances for this intent.</span></span> <span data-ttu-id="c8f99-119">For instructions on adding utterances, see [Add example utterances](Add-example-utterances.md).</span><span class="sxs-lookup"><span data-stu-id="c8f99-119">For instructions on adding utterances, see [Add example utterances](Add-example-utterances.md).</span></span>

![Intent Details page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/IntentDetails-UtterancesTab1.JPG)



## <a name="manage-your-intents"></a><span data-ttu-id="c8f99-121">Manage your intents</span><span class="sxs-lookup"><span data-stu-id="c8f99-121">Manage your intents</span></span>
<span data-ttu-id="c8f99-122">You can view a list of all your intents and manage them on the **Intents** page, where you can add new intents, rename and delete existing ones or access intent details for editing.</span><span class="sxs-lookup"><span data-stu-id="c8f99-122">You can view a list of all your intents and manage them on the **Intents** page, where you can add new intents, rename and delete existing ones or access intent details for editing.</span></span> 

![Intents List](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/IntentsList-added.JPG)

<span data-ttu-id="c8f99-124">**To rename an intent:**</span><span class="sxs-lookup"><span data-stu-id="c8f99-124">**To rename an intent:**</span></span>

1. <span data-ttu-id="c8f99-125">On the **Intents** page, click the Rename icon ![Rename Intent](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/Rename-Intent-btn.JPG) next to the intent you want to rename.</span><span class="sxs-lookup"><span data-stu-id="c8f99-125">On the **Intents** page, click the Rename icon ![Rename Intent](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/Rename-Intent-btn.JPG) next to the intent you want to rename.</span></span> 

2. <span data-ttu-id="c8f99-126">In the **Edit Intent** dialog box, edit the intent name and click **Save**.</span><span class="sxs-lookup"><span data-stu-id="c8f99-126">In the **Edit Intent** dialog box, edit the intent name and click **Save**.</span></span>

    ![Edit Intent](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/EditIntent-dialogbox.JPG)


<span data-ttu-id="c8f99-128">**To delete an intent:**</span><span class="sxs-lookup"><span data-stu-id="c8f99-128">**To delete an intent:**</span></span>
 
* <span data-ttu-id="c8f99-129">On the **Intents** page, click the trash bin icon ![Delete intent](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/trashbin-button.JPG) next to the intent you want to delete.</span><span class="sxs-lookup"><span data-stu-id="c8f99-129">On the **Intents** page, click the trash bin icon ![Delete intent](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/trashbin-button.JPG) next to the intent you want to delete.</span></span>


<span data-ttu-id="c8f99-130">**To access intent details for editing:**</span><span class="sxs-lookup"><span data-stu-id="c8f99-130">**To access intent details for editing:**</span></span>

* <span data-ttu-id="c8f99-131">On the **Intents** page, click the intent name which you want to access its details.</span><span class="sxs-lookup"><span data-stu-id="c8f99-131">On the **Intents** page, click the intent name which you want to access its details.</span></span>


<span data-ttu-id="c8f99-132">After adding intents to your app, now your next task is to start adding example utterances for the intents you've added.</span><span class="sxs-lookup"><span data-stu-id="c8f99-132">After adding intents to your app, now your next task is to start adding example utterances for the intents you've added.</span></span> <span data-ttu-id="c8f99-133">For instructions, see [Add example utterances](Add-example-utterances.md).</span><span class="sxs-lookup"><span data-stu-id="c8f99-133">For instructions, see [Add example utterances](Add-example-utterances.md).</span></span>







