---
title: Tutorial using pattern.any entity to improve LUIS predictions - Azure | Microsoft Docs
titleSuffix: Cognitive Services
description: In this tutorial, use the pattern.any entity to improve LUIS intent and entity predictions.
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.technology: luis
ms.topic: article
ms.date: 08/02/2018
ms.author: diberry
ms.openlocfilehash: 43f169ae11191c2e98c4538189bce781821de980
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968918"
---
# <a name="tutorial-improve-app-with-patternany-entity"></a><span data-ttu-id="f10da-103">Tutorial: Improve app with pattern.any entity</span><span class="sxs-lookup"><span data-stu-id="f10da-103">Tutorial: Improve app with pattern.any entity</span></span>

<span data-ttu-id="f10da-104">In this tutorial, use the pattern.any entity to increase intent and entity prediction.</span><span class="sxs-lookup"><span data-stu-id="f10da-104">In this tutorial, use the pattern.any entity to increase intent and entity prediction.</span></span>  

> [!div class="checklist"]
* <span data-ttu-id="f10da-105">Learn when and how to use pattern.any</span><span class="sxs-lookup"><span data-stu-id="f10da-105">Learn when and how to use pattern.any</span></span>
* <span data-ttu-id="f10da-106">Create pattern that uses pattern.any</span><span class="sxs-lookup"><span data-stu-id="f10da-106">Create pattern that uses pattern.any</span></span>
* <span data-ttu-id="f10da-107">How to verify prediction improvements</span><span class="sxs-lookup"><span data-stu-id="f10da-107">How to verify prediction improvements</span></span>

[!INCLUDE [LUIS Free account](../../../includes/cognitive-services-luis-free-key-short.md)]

## <a name="before-you-begin"></a><span data-ttu-id="f10da-108">Before you begin</span><span class="sxs-lookup"><span data-stu-id="f10da-108">Before you begin</span></span>
<span data-ttu-id="f10da-109">If you don't have the Human Resources app from the [pattern roles](luis-tutorial-pattern-roles.md) tutorial, [import](luis-how-to-start-new-app.md#import-new-app) the JSON into a new app in the [LUIS](luis-reference-regions.md#luis-website) website.</span><span class="sxs-lookup"><span data-stu-id="f10da-109">If you don't have the Human Resources app from the [pattern roles](luis-tutorial-pattern-roles.md) tutorial, [import](luis-how-to-start-new-app.md#import-new-app) the JSON into a new app in the [LUIS](luis-reference-regions.md#luis-website) website.</span></span> <span data-ttu-id="f10da-110">The app to import is found in the [LUIS-Samples](https://github.com/Microsoft/LUIS-Samples/blob/master/documentation-samples/quickstarts/custom-domain-roles-HumanResources.json) GitHub repository.</span><span class="sxs-lookup"><span data-stu-id="f10da-110">The app to import is found in the [LUIS-Samples](https://github.com/Microsoft/LUIS-Samples/blob/master/documentation-samples/quickstarts/custom-domain-roles-HumanResources.json) GitHub repository.</span></span>

<span data-ttu-id="f10da-111">If you want to keep the original Human Resources app, clone the version on the [Settings](luis-how-to-manage-versions.md#clone-a-version) page, and name it `patt-any`.</span><span class="sxs-lookup"><span data-stu-id="f10da-111">If you want to keep the original Human Resources app, clone the version on the [Settings](luis-how-to-manage-versions.md#clone-a-version) page, and name it `patt-any`.</span></span> <span data-ttu-id="f10da-112">Cloning is a great way to play with various LUIS features without affecting the original version.</span><span class="sxs-lookup"><span data-stu-id="f10da-112">Cloning is a great way to play with various LUIS features without affecting the original version.</span></span> 

## <a name="the-purpose-of-patternany"></a><span data-ttu-id="f10da-113">The purpose of pattern.any</span><span class="sxs-lookup"><span data-stu-id="f10da-113">The purpose of pattern.any</span></span>
<span data-ttu-id="f10da-114">The pattern.any entity allows you to find free form data where the wording of the entity makes it difficult to determine the end of the entity from the rest of the utterance.</span><span class="sxs-lookup"><span data-stu-id="f10da-114">The pattern.any entity allows you to find free form data where the wording of the entity makes it difficult to determine the end of the entity from the rest of the utterance.</span></span> 

<span data-ttu-id="f10da-115">This Human Resources app helps employees find company forms.</span><span class="sxs-lookup"><span data-stu-id="f10da-115">This Human Resources app helps employees find company forms.</span></span> <span data-ttu-id="f10da-116">Forms were added in the [regular expression tutorial](luis-quickstart-intents-regex-entity.md).</span><span class="sxs-lookup"><span data-stu-id="f10da-116">Forms were added in the [regular expression tutorial](luis-quickstart-intents-regex-entity.md).</span></span> <span data-ttu-id="f10da-117">The form names from that tutorial used a regular expression to extract a form name that was well-formatted such as the form names in bold in the following utterance table:</span><span class="sxs-lookup"><span data-stu-id="f10da-117">The form names from that tutorial used a regular expression to extract a form name that was well-formatted such as the form names in bold in the following utterance table:</span></span>

|<span data-ttu-id="f10da-118">Utterance</span><span class="sxs-lookup"><span data-stu-id="f10da-118">Utterance</span></span>|
|--|
|<span data-ttu-id="f10da-119">Where is **HRF-123456**?</span><span class="sxs-lookup"><span data-stu-id="f10da-119">Where is **HRF-123456**?</span></span>|
|<span data-ttu-id="f10da-120">Who authored **HRF-123234**?</span><span class="sxs-lookup"><span data-stu-id="f10da-120">Who authored **HRF-123234**?</span></span>|
|<span data-ttu-id="f10da-121">**HRF-456098** is published in French?</span><span class="sxs-lookup"><span data-stu-id="f10da-121">**HRF-456098** is published in French?</span></span>|

<span data-ttu-id="f10da-122">However, each form has both a formatted name, used in the preceding table, as well as a friendly name, such as `Request relocation from employee new to the company 2018 version 5`.</span><span class="sxs-lookup"><span data-stu-id="f10da-122">However, each form has both a formatted name, used in the preceding table, as well as a friendly name, such as `Request relocation from employee new to the company 2018 version 5`.</span></span> 

<span data-ttu-id="f10da-123">Utterances with the friendly form name look like:</span><span class="sxs-lookup"><span data-stu-id="f10da-123">Utterances with the friendly form name look like:</span></span>

|<span data-ttu-id="f10da-124">Utterance</span><span class="sxs-lookup"><span data-stu-id="f10da-124">Utterance</span></span>|
|--|
|<span data-ttu-id="f10da-125">Where is **Request relocation from employee new to the company 2018 version 5**?</span><span class="sxs-lookup"><span data-stu-id="f10da-125">Where is **Request relocation from employee new to the company 2018 version 5**?</span></span>|
|<span data-ttu-id="f10da-126">Who authored **"Request relocation from employee new to the company 2018 version 5"**?</span><span class="sxs-lookup"><span data-stu-id="f10da-126">Who authored **"Request relocation from employee new to the company 2018 version 5"**?</span></span>|
|<span data-ttu-id="f10da-127">**Request relocation from employee new to the company 2018 version 5** is published in French?</span><span class="sxs-lookup"><span data-stu-id="f10da-127">**Request relocation from employee new to the company 2018 version 5** is published in French?</span></span>|

<span data-ttu-id="f10da-128">The varying length includes phrases that may confuse LUIS about where the entity ends.</span><span class="sxs-lookup"><span data-stu-id="f10da-128">The varying length includes phrases that may confuse LUIS about where the entity ends.</span></span> <span data-ttu-id="f10da-129">Using a Pattern.any entity in a pattern allows you to specify the beginning and end of the form name so LUIS correctly extracts the form name.</span><span class="sxs-lookup"><span data-stu-id="f10da-129">Using a Pattern.any entity in a pattern allows you to specify the beginning and end of the form name so LUIS correctly extracts the form name.</span></span>

<span data-ttu-id="f10da-130">**While patterns allow you to provide fewer example utterances, if the entities are not detected, the pattern does not match.**</span><span class="sxs-lookup"><span data-stu-id="f10da-130">**While patterns allow you to provide fewer example utterances, if the entities are not detected, the pattern does not match.**</span></span>

## <a name="add-example-utterances-to-the-existing-intent-findform"></a><span data-ttu-id="f10da-131">Add example utterances to the existing intent FindForm</span><span class="sxs-lookup"><span data-stu-id="f10da-131">Add example utterances to the existing intent FindForm</span></span> 
<span data-ttu-id="f10da-132">Remove the prebuilt keyPhrase entity if it is difficult to create and label the FormName entity.</span><span class="sxs-lookup"><span data-stu-id="f10da-132">Remove the prebuilt keyPhrase entity if it is difficult to create and label the FormName entity.</span></span> 

1. <span data-ttu-id="f10da-133">Select **Build** from the top navigation, then select **Intents** from left navigation.</span><span class="sxs-lookup"><span data-stu-id="f10da-133">Select **Build** from the top navigation, then select **Intents** from left navigation.</span></span>

2. <span data-ttu-id="f10da-134">Select **FindForm** from the intents list.</span><span class="sxs-lookup"><span data-stu-id="f10da-134">Select **FindForm** from the intents list.</span></span>

3. <span data-ttu-id="f10da-135">Add some example utterances:</span><span class="sxs-lookup"><span data-stu-id="f10da-135">Add some example utterances:</span></span>

    |<span data-ttu-id="f10da-136">Example utterance</span><span class="sxs-lookup"><span data-stu-id="f10da-136">Example utterance</span></span>|
    |--|
    |<span data-ttu-id="f10da-137">Where is the form **What to do when a fire breaks out in the Lab** and who needs to sign it after I read it?</span><span class="sxs-lookup"><span data-stu-id="f10da-137">Where is the form **What to do when a fire breaks out in the Lab** and who needs to sign it after I read it?</span></span>|
    |<span data-ttu-id="f10da-138">Where is **Request relocation from employee new to the company** on the server?</span><span class="sxs-lookup"><span data-stu-id="f10da-138">Where is **Request relocation from employee new to the company** on the server?</span></span>|
    |<span data-ttu-id="f10da-139">Who authored "**Health and wellness requests on the main campus**" and what is the most current version?</span><span class="sxs-lookup"><span data-stu-id="f10da-139">Who authored "**Health and wellness requests on the main campus**" and what is the most current version?</span></span>|
    |<span data-ttu-id="f10da-140">I'm looking for the form named "**Office move request including physical assets**".</span><span class="sxs-lookup"><span data-stu-id="f10da-140">I'm looking for the form named "**Office move request including physical assets**".</span></span> |

    <span data-ttu-id="f10da-141">Without a Pattern.any entity, it would be difficult for LUIS to understand where the form title ends because of the many variations of form names.</span><span class="sxs-lookup"><span data-stu-id="f10da-141">Without a Pattern.any entity, it would be difficult for LUIS to understand where the form title ends because of the many variations of form names.</span></span>

## <a name="create-a-patternany-entity"></a><span data-ttu-id="f10da-142">Create a Pattern.any entity</span><span class="sxs-lookup"><span data-stu-id="f10da-142">Create a Pattern.any entity</span></span>
<span data-ttu-id="f10da-143">The Pattern.any entity extracts entities of varying length.</span><span class="sxs-lookup"><span data-stu-id="f10da-143">The Pattern.any entity extracts entities of varying length.</span></span> <span data-ttu-id="f10da-144">It only works in a pattern because the pattern marks the beginning and end of the entity.</span><span class="sxs-lookup"><span data-stu-id="f10da-144">It only works in a pattern because the pattern marks the beginning and end of the entity.</span></span> <span data-ttu-id="f10da-145">If you find that your pattern, when it includes a Pattern.any, extracts entities incorrectly, use an [explicit list](luis-concept-patterns.md#explicit-lists) to correct this problem.</span><span class="sxs-lookup"><span data-stu-id="f10da-145">If you find that your pattern, when it includes a Pattern.any, extracts entities incorrectly, use an [explicit list](luis-concept-patterns.md#explicit-lists) to correct this problem.</span></span> 

1. <span data-ttu-id="f10da-146">Select **Entities** in the left navigation.</span><span class="sxs-lookup"><span data-stu-id="f10da-146">Select **Entities** in the left navigation.</span></span>

2. <span data-ttu-id="f10da-147">Select **Create new entity**, enter the name `FormName`, and select **Pattern.any** as the type.</span><span class="sxs-lookup"><span data-stu-id="f10da-147">Select **Create new entity**, enter the name `FormName`, and select **Pattern.any** as the type.</span></span> <span data-ttu-id="f10da-148">Select **Done**.</span><span class="sxs-lookup"><span data-stu-id="f10da-148">Select **Done**.</span></span> 

    <span data-ttu-id="f10da-149">You can't label the entity in the intent because a Pattern.any is only valid in a pattern.</span><span class="sxs-lookup"><span data-stu-id="f10da-149">You can't label the entity in the intent because a Pattern.any is only valid in a pattern.</span></span> 

    <span data-ttu-id="f10da-150">If you want the extracted data to include other entities such as number or datetimeV2, you need to create a composite entity that includes the Pattern.any, as well as number and datetimeV2.</span><span class="sxs-lookup"><span data-stu-id="f10da-150">If you want the extracted data to include other entities such as number or datetimeV2, you need to create a composite entity that includes the Pattern.any, as well as number and datetimeV2.</span></span>

## <a name="add-a-pattern-that-uses-the-patternany"></a><span data-ttu-id="f10da-151">Add a pattern that uses the Pattern.any</span><span class="sxs-lookup"><span data-stu-id="f10da-151">Add a pattern that uses the Pattern.any</span></span>

1. <span data-ttu-id="f10da-152">Select **Patterns** from the left navigation.</span><span class="sxs-lookup"><span data-stu-id="f10da-152">Select **Patterns** from the left navigation.</span></span>

2. <span data-ttu-id="f10da-153">Select the **FindForm** intent.</span><span class="sxs-lookup"><span data-stu-id="f10da-153">Select the **FindForm** intent.</span></span>

3. <span data-ttu-id="f10da-154">Enter the following template utterances, which use the new entity:</span><span class="sxs-lookup"><span data-stu-id="f10da-154">Enter the following template utterances, which use the new entity:</span></span>

    |<span data-ttu-id="f10da-155">Template utterances</span><span class="sxs-lookup"><span data-stu-id="f10da-155">Template utterances</span></span>|
    |--|
    |<span data-ttu-id="f10da-156">Where is the form ["]{FormName}["] and who needs to sign it after I read it[?]</span><span class="sxs-lookup"><span data-stu-id="f10da-156">Where is the form ["]{FormName}["] and who needs to sign it after I read it[?]</span></span>|
    |<span data-ttu-id="f10da-157">Where is ["]{FormName}["] on the server[?]</span><span class="sxs-lookup"><span data-stu-id="f10da-157">Where is ["]{FormName}["] on the server[?]</span></span>|
    |<span data-ttu-id="f10da-158">Who authored ["]{FormName}["] and what is the most current version[?]</span><span class="sxs-lookup"><span data-stu-id="f10da-158">Who authored ["]{FormName}["] and what is the most current version[?]</span></span>|
    |<span data-ttu-id="f10da-159">I'm looking for the form named ["]{FormName}["][.]</span><span class="sxs-lookup"><span data-stu-id="f10da-159">I'm looking for the form named ["]{FormName}["][.]</span></span>|

    <span data-ttu-id="f10da-160">If you want to account for variations of the form such as single quotes instead of double quotes or a period instead of a question mark, create a new pattern for each variation.</span><span class="sxs-lookup"><span data-stu-id="f10da-160">If you want to account for variations of the form such as single quotes instead of double quotes or a period instead of a question mark, create a new pattern for each variation.</span></span>

4. <span data-ttu-id="f10da-161">If you removed the keyPhrase entity, add it back to the app.</span><span class="sxs-lookup"><span data-stu-id="f10da-161">If you removed the keyPhrase entity, add it back to the app.</span></span> 

## <a name="train-the-luis-app"></a><span data-ttu-id="f10da-162">Train the LUIS app</span><span class="sxs-lookup"><span data-stu-id="f10da-162">Train the LUIS app</span></span>

[!INCLUDE [LUIS How to Train steps](../../../includes/cognitive-services-luis-tutorial-how-to-train.md)]

## <a name="test-the-new-pattern-for-free-form-data-extraction"></a><span data-ttu-id="f10da-163">Test the new pattern for free-form data extraction</span><span class="sxs-lookup"><span data-stu-id="f10da-163">Test the new pattern for free-form data extraction</span></span>
1. <span data-ttu-id="f10da-164">Select **Test** from the top bar to open the test panel.</span><span class="sxs-lookup"><span data-stu-id="f10da-164">Select **Test** from the top bar to open the test panel.</span></span> 

2. <span data-ttu-id="f10da-165">Enter the following utterance:</span><span class="sxs-lookup"><span data-stu-id="f10da-165">Enter the following utterance:</span></span> 

    `Where is the form Understand your responsibilities as a member of the community and who needs to sign it after I read it?`

3. <span data-ttu-id="f10da-166">Select **Inspect** under the result to see the test results for entity and intent.</span><span class="sxs-lookup"><span data-stu-id="f10da-166">Select **Inspect** under the result to see the test results for entity and intent.</span></span>

    <span data-ttu-id="f10da-167">The entity `FormName` is found first, then the pattern is found, determining the intent.</span><span class="sxs-lookup"><span data-stu-id="f10da-167">The entity `FormName` is found first, then the pattern is found, determining the intent.</span></span> <span data-ttu-id="f10da-168">If you have a test result where the entities are not detected, and therefore the pattern is not found, you need to add more example utterances on the intent (not the pattern).</span><span class="sxs-lookup"><span data-stu-id="f10da-168">If you have a test result where the entities are not detected, and therefore the pattern is not found, you need to add more example utterances on the intent (not the pattern).</span></span>

4. <span data-ttu-id="f10da-169">Close the test panel by selecting the **Test** button in the top navigation.</span><span class="sxs-lookup"><span data-stu-id="f10da-169">Close the test panel by selecting the **Test** button in the top navigation.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="f10da-170">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="f10da-170">Clean up resources</span></span>

[!INCLUDE [LUIS How to clean up resources](../../../includes/cognitive-services-luis-tutorial-how-to-clean-up-resources.md)]

## <a name="next-steps"></a><span data-ttu-id="f10da-171">Next steps</span><span class="sxs-lookup"><span data-stu-id="f10da-171">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f10da-172">Learn how to use roles with a pattern</span><span class="sxs-lookup"><span data-stu-id="f10da-172">Learn how to use roles with a pattern</span></span>](luis-tutorial-pattern-roles.md)