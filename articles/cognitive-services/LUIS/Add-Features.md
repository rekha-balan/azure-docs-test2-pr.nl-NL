---
title: Add features in LUIS applications | Microsoft Docs
description: Use Language Understanding Intelligent Services (LUIS) to add app features that can improve the detection or prediction of intents and entities.
services: cognitive-services
author: cahann
manager: hsalama
ms.service: cognitive-services
ms.technology: luis
ms.topic: article
ms.date: 03/01/2017
ms.author: cahann
ms.openlocfilehash: fa13fbff59c2d99f6aa7bdfae11144454c3e9000
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556490"
---
# <a name="add-features"></a><span data-ttu-id="aa751-103">Add Features</span><span class="sxs-lookup"><span data-stu-id="aa751-103">Add Features</span></span>

<span data-ttu-id="aa751-104">Features help you improve the detection or prediction of intents and entities in utterances.</span><span class="sxs-lookup"><span data-stu-id="aa751-104">Features help you improve the detection or prediction of intents and entities in utterances.</span></span> <span data-ttu-id="aa751-105">For example, when your app fails to identify an entity, adding a “phrase list” feature with some or all of the entity’s potential values will improve the detection of this entity.</span><span class="sxs-lookup"><span data-stu-id="aa751-105">For example, when your app fails to identify an entity, adding a “phrase list” feature with some or all of the entity’s potential values will improve the detection of this entity.</span></span> <span data-ttu-id="aa751-106">Also, adding a “pattern” feature helps your application easily recognize regular patterns that are frequently used in your application's domain, such as the pattern of flight numbers in a travel app or product codes in a shopping app.</span><span class="sxs-lookup"><span data-stu-id="aa751-106">Also, adding a “pattern” feature helps your application easily recognize regular patterns that are frequently used in your application's domain, such as the pattern of flight numbers in a travel app or product codes in a shopping app.</span></span> 


## <a name="phrase-list-features"></a><span data-ttu-id="aa751-107">Phrase list features</span><span class="sxs-lookup"><span data-stu-id="aa751-107">Phrase list features</span></span>
<span data-ttu-id="aa751-108">You can create a “phrase list” including a group of values (words or phrases) that belong to the same class and must be treated similarly (e.g. names of cities or products), so that what LUIS learns about one of them will be automatically applied to the others as well.</span><span class="sxs-lookup"><span data-stu-id="aa751-108">You can create a “phrase list” including a group of values (words or phrases) that belong to the same class and must be treated similarly (e.g. names of cities or products), so that what LUIS learns about one of them will be automatically applied to the others as well.</span></span> <span data-ttu-id="aa751-109">For example in the TravelAgent app, London, Paris, Cairo, etc. can be values of a phrase list named as “Cities”.</span><span class="sxs-lookup"><span data-stu-id="aa751-109">For example in the TravelAgent app, London, Paris, Cairo, etc. can be values of a phrase list named as “Cities”.</span></span> <span data-ttu-id="aa751-110">If you label one of these values as an entity, others will mostly be predicted the same.</span><span class="sxs-lookup"><span data-stu-id="aa751-110">If you label one of these values as an entity, others will mostly be predicted the same.</span></span> 

<span data-ttu-id="aa751-111">LUIS may be unable to recognize rare and proprietary words, as well as foreign words (out of the culture of the app), and therefore they should be added to a phrase list feature.</span><span class="sxs-lookup"><span data-stu-id="aa751-111">LUIS may be unable to recognize rare and proprietary words, as well as foreign words (out of the culture of the app), and therefore they should be added to a phrase list feature.</span></span> 

<span data-ttu-id="aa751-112">**To add a phrase list:**</span><span class="sxs-lookup"><span data-stu-id="aa751-112">**To add a phrase list:**</span></span>

1. <span data-ttu-id="aa751-113">Open your app by clicking its name on **My Apps** page, and then click **Features** in your app's left panel.</span><span class="sxs-lookup"><span data-stu-id="aa751-113">Open your app by clicking its name on **My Apps** page, and then click **Features** in your app's left panel.</span></span> 
2. <span data-ttu-id="aa751-114">On the **Features** page, click **Add phrase list**.</span><span class="sxs-lookup"><span data-stu-id="aa751-114">On the **Features** page, click **Add phrase list**.</span></span> 
 
    ![Features page - Phrase List Features tab](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/Features.JPG)
3. <span data-ttu-id="aa751-116">In the **Add Phrase List** dialog box, type "Cities" as the name of the phrase list in the **Phrase list name** text box.</span><span class="sxs-lookup"><span data-stu-id="aa751-116">In the **Add Phrase List** dialog box, type "Cities" as the name of the phrase list in the **Phrase list name** text box.</span></span>
4. <span data-ttu-id="aa751-117">In **Phrase list values**, type the values you want to include in the phrase list, separated by **commas** (e.g. London, Paris, Seattle, Berlin, Dubai, Cairo)</span><span class="sxs-lookup"><span data-stu-id="aa751-117">In **Phrase list values**, type the values you want to include in the phrase list, separated by **commas** (e.g. London, Paris, Seattle, Berlin, Dubai, Cairo)</span></span>  

    ![Add phrase list dialog box](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/Features-AddPhraseList.JPG)
5. <span data-ttu-id="aa751-119">Click **Is exchangeable**if the added phrase list values are alternatives that can be used interchangeably.</span><span class="sxs-lookup"><span data-stu-id="aa751-119">Click **Is exchangeable**if the added phrase list values are alternatives that can be used interchangeably.</span></span>
6. <span data-ttu-id="aa751-120">Click **Is active** if you want this phrase list to be active (i.e. applicable and used) in your app.</span><span class="sxs-lookup"><span data-stu-id="aa751-120">Click **Is active** if you want this phrase list to be active (i.e. applicable and used) in your app.</span></span>
7. <span data-ttu-id="aa751-121">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="aa751-121">Click **Save**.</span></span> <span data-ttu-id="aa751-122">The phrase list will be added to phrase list features on the **Features** page.</span><span class="sxs-lookup"><span data-stu-id="aa751-122">The phrase list will be added to phrase list features on the **Features** page.</span></span> 

<span data-ttu-id="aa751-123">**To edit a phrase list:**</span><span class="sxs-lookup"><span data-stu-id="aa751-123">**To edit a phrase list:**</span></span>

* <span data-ttu-id="aa751-124">Click the phrase list name in the list of phrase list features.</span><span class="sxs-lookup"><span data-stu-id="aa751-124">Click the phrase list name in the list of phrase list features.</span></span> <span data-ttu-id="aa751-125">In the **Edit Phrase List** dialog box that opens, make the required editing changes and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="aa751-125">In the **Edit Phrase List** dialog box that opens, make the required editing changes and then click **Save**.</span></span>

    ![Edit Phrase List dialog box](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/Features-EditPhraseList.JPG)

<span data-ttu-id="aa751-127">**To delete a phrase list:**</span><span class="sxs-lookup"><span data-stu-id="aa751-127">**To delete a phrase list:**</span></span> 

* <span data-ttu-id="aa751-128">Click the trash bin icon</span><span class="sxs-lookup"><span data-stu-id="aa751-128">Click the trash bin icon</span></span> ![Trash bin button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/trashbin-button.JPG) <span data-ttu-id="aa751-130">next to the phrase list name in the list of phrase list features.</span><span class="sxs-lookup"><span data-stu-id="aa751-130">next to the phrase list name in the list of phrase list features.</span></span>

## <a name="pattern-features"></a><span data-ttu-id="aa751-131">Pattern features</span><span class="sxs-lookup"><span data-stu-id="aa751-131">Pattern features</span></span>
<span data-ttu-id="aa751-132">You can create a structured “pattern” to represent a certain class of objects (e.g. flight numbers, product codes, etc.).</span><span class="sxs-lookup"><span data-stu-id="aa751-132">You can create a structured “pattern” to represent a certain class of objects (e.g. flight numbers, product codes, etc.).</span></span> <span data-ttu-id="aa751-133">A pattern is defined in regular expression (Regex).</span><span class="sxs-lookup"><span data-stu-id="aa751-133">A pattern is defined in regular expression (Regex).</span></span> <span data-ttu-id="aa751-134">This will help LUIS easily recognize the string of the defined pattern in utterances, and thus classify it correctly.</span><span class="sxs-lookup"><span data-stu-id="aa751-134">This will help LUIS easily recognize the string of the defined pattern in utterances, and thus classify it correctly.</span></span> <span data-ttu-id="aa751-135">For example, in a travel app, flight numbers might follow a regular pattern of two letters followed by three digits.</span><span class="sxs-lookup"><span data-stu-id="aa751-135">For example, in a travel app, flight numbers might follow a regular pattern of two letters followed by three digits.</span></span> 


<span data-ttu-id="aa751-136">**To add a pattern:**</span><span class="sxs-lookup"><span data-stu-id="aa751-136">**To add a pattern:**</span></span>

1. <span data-ttu-id="aa751-137">Open your app by clicking its name on **My Apps** page, and then click **Features** in your app's left panel.</span><span class="sxs-lookup"><span data-stu-id="aa751-137">Open your app by clicking its name on **My Apps** page, and then click **Features** in your app's left panel.</span></span> 
2. <span data-ttu-id="aa751-138">On the **Features** page, click the **Pattern Features** tab, and then click **Add Pattern Feature**.</span><span class="sxs-lookup"><span data-stu-id="aa751-138">On the **Features** page, click the **Pattern Features** tab, and then click **Add Pattern Feature**.</span></span>

    ![Features page - Pattern Features tab](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/Features-patternTab.JPG)
3. <span data-ttu-id="aa751-140">In the **Add Pattern** dialog box, type "Flight number" in the **Pattern name** text box.</span><span class="sxs-lookup"><span data-stu-id="aa751-140">In the **Add Pattern** dialog box, type "Flight number" in the **Pattern name** text box.</span></span>
4.  <span data-ttu-id="aa751-141">To learn about the supported regex syntax, click **learn about supported regex syntax** to expand the dialog and display it, as in the screen below.</span><span class="sxs-lookup"><span data-stu-id="aa751-141">To learn about the supported regex syntax, click **learn about supported regex syntax** to expand the dialog and display it, as in the screen below.</span></span> <span data-ttu-id="aa751-142">To collapse the dialog and hide syntax, click it again.</span><span class="sxs-lookup"><span data-stu-id="aa751-142">To collapse the dialog and hide syntax, click it again.</span></span>

    ![The supported regex syntax](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/Features-Pattern-RegexSyntax.JPG)
5. <span data-ttu-id="aa751-144">In the **Pattern value** text box, type [A-Za-z]{2}[0-9]{3} as the value of the flight number pattern.</span><span class="sxs-lookup"><span data-stu-id="aa751-144">In the **Pattern value** text box, type [A-Za-z]{2}[0-9]{3} as the value of the flight number pattern.</span></span>

    ![Add pattern feature](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/Features-AddPattern.JPG)
6. <span data-ttu-id="aa751-146">Click **Is active** if you want this pattern to be active (i.e. applicable and used) in your app.</span><span class="sxs-lookup"><span data-stu-id="aa751-146">Click **Is active** if you want this pattern to be active (i.e. applicable and used) in your app.</span></span> <span data-ttu-id="aa751-147">A feature is active by default.</span><span class="sxs-lookup"><span data-stu-id="aa751-147">A feature is active by default.</span></span>
7. <span data-ttu-id="aa751-148">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="aa751-148">Click **Save**.</span></span> <span data-ttu-id="aa751-149">The pattern will be added to pattern features on the **Features** page.</span><span class="sxs-lookup"><span data-stu-id="aa751-149">The pattern will be added to pattern features on the **Features** page.</span></span>

<span data-ttu-id="aa751-150">**To edit a pattern:**</span><span class="sxs-lookup"><span data-stu-id="aa751-150">**To edit a pattern:**</span></span>

* <span data-ttu-id="aa751-151">Click the pattern name in the list of pattern features.</span><span class="sxs-lookup"><span data-stu-id="aa751-151">Click the pattern name in the list of pattern features.</span></span> <span data-ttu-id="aa751-152">In the **Edit Pattern** dialog box that opens, make the required editing changes and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="aa751-152">In the **Edit Pattern** dialog box that opens, make the required editing changes and then click **Save**.</span></span>

    ![Edit Pattern dialog box](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/Features-EditPattern.JPG)

<span data-ttu-id="aa751-154">**To delete a pattern:**</span><span class="sxs-lookup"><span data-stu-id="aa751-154">**To delete a pattern:**</span></span> 

* <span data-ttu-id="aa751-155">Click the trash icon button</span><span class="sxs-lookup"><span data-stu-id="aa751-155">Click the trash icon button</span></span> ![Trash bin button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/trashbin-button.JPG) <span data-ttu-id="aa751-157">next to the pattern name in the list of pattern features.</span><span class="sxs-lookup"><span data-stu-id="aa751-157">next to the pattern name in the list of pattern features.</span></span>









