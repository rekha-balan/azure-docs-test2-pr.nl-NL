---
title: Tutorial to create a LUIS app to get location data - Azure | Microsoft Docs
description: In this tutorial, learn how to create a simple LUIS app using intents and a hierarchical entity to extract data.
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: luis
ms.topic: tutorial
ms.date: 08/02/2018
ms.author: diberry
ms.openlocfilehash: 65c7aabb984ad0a6b3e77d0f98003803821e06cc
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867842"
---
# <a name="tutorial-5-add-hierarchical-entity"></a><span data-ttu-id="73749-103">Tutorial: 5.</span><span class="sxs-lookup"><span data-stu-id="73749-103">Tutorial: 5.</span></span> <span data-ttu-id="73749-104">Add hierarchical entity</span><span class="sxs-lookup"><span data-stu-id="73749-104">Add hierarchical entity</span></span>
<span data-ttu-id="73749-105">In this tutorial, create an app that demonstrates how to find related pieces of data based on context.</span><span class="sxs-lookup"><span data-stu-id="73749-105">In this tutorial, create an app that demonstrates how to find related pieces of data based on context.</span></span> 

<!-- green checkmark -->
> [!div class="checklist"]
> * <span data-ttu-id="73749-106">Understand hierarchical entities and contextually learned children</span><span class="sxs-lookup"><span data-stu-id="73749-106">Understand hierarchical entities and contextually learned children</span></span> 
> * <span data-ttu-id="73749-107">Use LUIS app in Human Resources (HR) domain</span><span class="sxs-lookup"><span data-stu-id="73749-107">Use LUIS app in Human Resources (HR) domain</span></span> 
> * <span data-ttu-id="73749-108">Add location hierarchical entity with origin and destination children</span><span class="sxs-lookup"><span data-stu-id="73749-108">Add location hierarchical entity with origin and destination children</span></span>
> * <span data-ttu-id="73749-109">Train, and publish app</span><span class="sxs-lookup"><span data-stu-id="73749-109">Train, and publish app</span></span>
> * <span data-ttu-id="73749-110">Query endpoint of app to see LUIS JSON response including hierarchical children</span><span class="sxs-lookup"><span data-stu-id="73749-110">Query endpoint of app to see LUIS JSON response including hierarchical children</span></span> 

[!INCLUDE [LUIS Free account](../../../includes/cognitive-services-luis-free-key-short.md)]

## <a name="before-you-begin"></a><span data-ttu-id="73749-111">Before you begin</span><span class="sxs-lookup"><span data-stu-id="73749-111">Before you begin</span></span>
<span data-ttu-id="73749-112">If you don't have the Human Resources app from the [list entities](luis-quickstart-intent-and-list-entity.md) tutorial, [import](luis-how-to-start-new-app.md#import-new-app) the JSON into a new app in the [LUIS](luis-reference-regions.md#luis-website) website.</span><span class="sxs-lookup"><span data-stu-id="73749-112">If you don't have the Human Resources app from the [list entities](luis-quickstart-intent-and-list-entity.md) tutorial, [import](luis-how-to-start-new-app.md#import-new-app) the JSON into a new app in the [LUIS](luis-reference-regions.md#luis-website) website.</span></span> <span data-ttu-id="73749-113">The app to import is found in the [LUIS-Samples](https://github.com/Microsoft/LUIS-Samples/blob/master/documentation-samples/quickstarts/custom-domain-list-HumanResources.json) Github repository.</span><span class="sxs-lookup"><span data-stu-id="73749-113">The app to import is found in the [LUIS-Samples](https://github.com/Microsoft/LUIS-Samples/blob/master/documentation-samples/quickstarts/custom-domain-list-HumanResources.json) Github repository.</span></span>

<span data-ttu-id="73749-114">If you want to keep the original Human Resources app, clone the version on the [Settings](luis-how-to-manage-versions.md#clone-a-version) page, and name it `hier`.</span><span class="sxs-lookup"><span data-stu-id="73749-114">If you want to keep the original Human Resources app, clone the version on the [Settings](luis-how-to-manage-versions.md#clone-a-version) page, and name it `hier`.</span></span> <span data-ttu-id="73749-115">Cloning is a great way to play with various LUIS features without affecting the original version.</span><span class="sxs-lookup"><span data-stu-id="73749-115">Cloning is a great way to play with various LUIS features without affecting the original version.</span></span> 

## <a name="purpose-of-the-app-with-this-entity"></a><span data-ttu-id="73749-116">Purpose of the app with this entity</span><span class="sxs-lookup"><span data-stu-id="73749-116">Purpose of the app with this entity</span></span>
<span data-ttu-id="73749-117">This app determines where an employee is to be moved from the origin location (building and office) to the destination location (building and office).</span><span class="sxs-lookup"><span data-stu-id="73749-117">This app determines where an employee is to be moved from the origin location (building and office) to the destination location (building and office).</span></span> <span data-ttu-id="73749-118">It uses the hierarchical entity to determine the locations within the utterance.</span><span class="sxs-lookup"><span data-stu-id="73749-118">It uses the hierarchical entity to determine the locations within the utterance.</span></span> 

<span data-ttu-id="73749-119">The hierarchical entity is a good fit for this type of data because the two pieces of data:</span><span class="sxs-lookup"><span data-stu-id="73749-119">The hierarchical entity is a good fit for this type of data because the two pieces of data:</span></span>

* <span data-ttu-id="73749-120">Are related to each other in the context of the utterance.</span><span class="sxs-lookup"><span data-stu-id="73749-120">Are related to each other in the context of the utterance.</span></span>
* <span data-ttu-id="73749-121">Use specific word choice to indicate each location.</span><span class="sxs-lookup"><span data-stu-id="73749-121">Use specific word choice to indicate each location.</span></span> <span data-ttu-id="73749-122">Examples of these words include: from/to, leaving/headed to, away from/toward.</span><span class="sxs-lookup"><span data-stu-id="73749-122">Examples of these words include: from/to, leaving/headed to, away from/toward.</span></span>
* <span data-ttu-id="73749-123">Both locations are frequently in the same utterance.</span><span class="sxs-lookup"><span data-stu-id="73749-123">Both locations are frequently in the same utterance.</span></span> 

<span data-ttu-id="73749-124">The purpose of the **hierarchical** entity is to find related data within the utterance based on context.</span><span class="sxs-lookup"><span data-stu-id="73749-124">The purpose of the **hierarchical** entity is to find related data within the utterance based on context.</span></span> <span data-ttu-id="73749-125">Consider the following utterance:</span><span class="sxs-lookup"><span data-stu-id="73749-125">Consider the following utterance:</span></span>

```JSON
mv Jill Jones from a-2349 to b-1298
```
<span data-ttu-id="73749-126">The utterance has two locations specified, `a-2349` and `b-1298`.</span><span class="sxs-lookup"><span data-stu-id="73749-126">The utterance has two locations specified, `a-2349` and `b-1298`.</span></span> <span data-ttu-id="73749-127">Assume that the letter corresponds to a building name and the number indicates the office within that building.</span><span class="sxs-lookup"><span data-stu-id="73749-127">Assume that the letter corresponds to a building name and the number indicates the office within that building.</span></span> <span data-ttu-id="73749-128">It makes sense that they are both grouped as children of a hierarchical entity, `Locations` because both pieces of data need to be extracted from the utterance and they are related to each other.</span><span class="sxs-lookup"><span data-stu-id="73749-128">It makes sense that they are both grouped as children of a hierarchical entity, `Locations` because both pieces of data need to be extracted from the utterance and they are related to each other.</span></span> 
 
<span data-ttu-id="73749-129">If only one child (origin or destination) of a hierarchical entity is present, it is still extracted.</span><span class="sxs-lookup"><span data-stu-id="73749-129">If only one child (origin or destination) of a hierarchical entity is present, it is still extracted.</span></span> <span data-ttu-id="73749-130">All children do not need to be found for just one, or some, to be extracted.</span><span class="sxs-lookup"><span data-stu-id="73749-130">All children do not need to be found for just one, or some, to be extracted.</span></span> 

## <a name="remove-prebuilt-number-entity-from-app"></a><span data-ttu-id="73749-131">Remove prebuilt number entity from app</span><span class="sxs-lookup"><span data-stu-id="73749-131">Remove prebuilt number entity from app</span></span>
<span data-ttu-id="73749-132">In order to see the entire utterance and mark the hierarchical children, temporarily remove the prebuilt number entity.</span><span class="sxs-lookup"><span data-stu-id="73749-132">In order to see the entire utterance and mark the hierarchical children, temporarily remove the prebuilt number entity.</span></span>

1. <span data-ttu-id="73749-133">Make sure your Human Resources app is in the **Build** section of LUIS.</span><span class="sxs-lookup"><span data-stu-id="73749-133">Make sure your Human Resources app is in the **Build** section of LUIS.</span></span> <span data-ttu-id="73749-134">You can change to this section by selecting **Build** on the top, right menu bar.</span><span class="sxs-lookup"><span data-stu-id="73749-134">You can change to this section by selecting **Build** on the top, right menu bar.</span></span> 

2. <span data-ttu-id="73749-135">Select **Entities** from the left menu.</span><span class="sxs-lookup"><span data-stu-id="73749-135">Select **Entities** from the left menu.</span></span>

3. <span data-ttu-id="73749-136">Select the ellipsis (***...***) button to the right of the number entity in the list.</span><span class="sxs-lookup"><span data-stu-id="73749-136">Select the ellipsis (***...***) button to the right of the number entity in the list.</span></span> <span data-ttu-id="73749-137">Select **Delete**.</span><span class="sxs-lookup"><span data-stu-id="73749-137">Select **Delete**.</span></span> 

    <span data-ttu-id="73749-138">[ ![Screenshot of LUIS app on entities list page, with delete button highlighted for Number prebuilt entity](./media/luis-quickstart-intent-and-hier-entity/hr-delete-number-prebuilt.png)](./media/luis-quickstart-intent-and-hier-entity/hr-delete-number-prebuilt.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="73749-138">[ ![Screenshot of LUIS app on entities list page, with delete button highlighted for Number prebuilt entity](./media/luis-quickstart-intent-and-hier-entity/hr-delete-number-prebuilt.png)](./media/luis-quickstart-intent-and-hier-entity/hr-delete-number-prebuilt.png#lightbox)</span></span>


## <a name="add-utterances-to-moveemployee-intent"></a><span data-ttu-id="73749-139">Add utterances to MoveEmployee intent</span><span class="sxs-lookup"><span data-stu-id="73749-139">Add utterances to MoveEmployee intent</span></span>

1. <span data-ttu-id="73749-140">Select **Intents** from the left menu.</span><span class="sxs-lookup"><span data-stu-id="73749-140">Select **Intents** from the left menu.</span></span>

2. <span data-ttu-id="73749-141">Select **MoveEmployee** from the list of intents.</span><span class="sxs-lookup"><span data-stu-id="73749-141">Select **MoveEmployee** from the list of intents.</span></span>

    <span data-ttu-id="73749-142">[ ![Screenshot of LUIS app with MoveEmployee intent highlighted in left menu](./media/luis-quickstart-intent-and-hier-entity/hr-intents-list-moveemployee.png)](./media/luis-quickstart-intent-and-hier-entity/hr-intents-list-moveemployee.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="73749-142">[ ![Screenshot of LUIS app with MoveEmployee intent highlighted in left menu](./media/luis-quickstart-intent-and-hier-entity/hr-intents-list-moveemployee.png)](./media/luis-quickstart-intent-and-hier-entity/hr-intents-list-moveemployee.png#lightbox)</span></span>

3. <span data-ttu-id="73749-143">Add the following example utterances:</span><span class="sxs-lookup"><span data-stu-id="73749-143">Add the following example utterances:</span></span>

    |<span data-ttu-id="73749-144">Example utterances</span><span class="sxs-lookup"><span data-stu-id="73749-144">Example utterances</span></span>|
    |--|
    |<span data-ttu-id="73749-145">Move John W. Smith **to** a-2345</span><span class="sxs-lookup"><span data-stu-id="73749-145">Move John W. Smith **to** a-2345</span></span>|
    |<span data-ttu-id="73749-146">Direct Jill Jones **to** b-3499</span><span class="sxs-lookup"><span data-stu-id="73749-146">Direct Jill Jones **to** b-3499</span></span>|
    |<span data-ttu-id="73749-147">Organize the move of x23456 **from** hh-2345 **to** e-0234</span><span class="sxs-lookup"><span data-stu-id="73749-147">Organize the move of x23456 **from** hh-2345 **to** e-0234</span></span>|
    |<span data-ttu-id="73749-148">Begin paperwork to set x12345 **leaving** a-3459 **headed to** f-34567</span><span class="sxs-lookup"><span data-stu-id="73749-148">Begin paperwork to set x12345 **leaving** a-3459 **headed to** f-34567</span></span>|
    |<span data-ttu-id="73749-149">Displace 425-555-0000 **away from** g-2323 **toward** hh-2345</span><span class="sxs-lookup"><span data-stu-id="73749-149">Displace 425-555-0000 **away from** g-2323 **toward** hh-2345</span></span>|

    <span data-ttu-id="73749-150">[ ![Screenshot of LUIS with new utterances in MoveEmployee intent](./media/luis-quickstart-intent-and-hier-entity/hr-enter-utterances.png)](./media/luis-quickstart-intent-and-hier-entity/hr-enter-utterances.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="73749-150">[ ![Screenshot of LUIS with new utterances in MoveEmployee intent](./media/luis-quickstart-intent-and-hier-entity/hr-enter-utterances.png)](./media/luis-quickstart-intent-and-hier-entity/hr-enter-utterances.png#lightbox)</span></span>

    <span data-ttu-id="73749-151">In the [list entity](luis-quickstart-intent-and-list-entity.md) tutorial, an employee could be designated by name, email address, phone extension, mobile phone number, or U.S. federal social security number.</span><span class="sxs-lookup"><span data-stu-id="73749-151">In the [list entity](luis-quickstart-intent-and-list-entity.md) tutorial, an employee could be designated by name, email address, phone extension, mobile phone number, or U.S. federal social security number.</span></span> <span data-ttu-id="73749-152">These employee numbers are used in the utterances.</span><span class="sxs-lookup"><span data-stu-id="73749-152">These employee numbers are used in the utterances.</span></span> <span data-ttu-id="73749-153">The previous example utterances include different ways to note the origin and destination locations, marked in bold.</span><span class="sxs-lookup"><span data-stu-id="73749-153">The previous example utterances include different ways to note the origin and destination locations, marked in bold.</span></span> <span data-ttu-id="73749-154">A couple of the utterances only have destinations on purpose.</span><span class="sxs-lookup"><span data-stu-id="73749-154">A couple of the utterances only have destinations on purpose.</span></span> <span data-ttu-id="73749-155">This helps LUIS understand how those locations are placed in the utterance when the origin is not specified.</span><span class="sxs-lookup"><span data-stu-id="73749-155">This helps LUIS understand how those locations are placed in the utterance when the origin is not specified.</span></span>     

## <a name="create-a-location-entity"></a><span data-ttu-id="73749-156">Create a location entity</span><span class="sxs-lookup"><span data-stu-id="73749-156">Create a location entity</span></span>
<span data-ttu-id="73749-157">LUIS needs to understand what a location is by labeling the origin and destination in the utterances.</span><span class="sxs-lookup"><span data-stu-id="73749-157">LUIS needs to understand what a location is by labeling the origin and destination in the utterances.</span></span> <span data-ttu-id="73749-158">If you need to see the utterance in the token (raw) view, select the toggle in the bar above the utterances labeled **Entities View**.</span><span class="sxs-lookup"><span data-stu-id="73749-158">If you need to see the utterance in the token (raw) view, select the toggle in the bar above the utterances labeled **Entities View**.</span></span> <span data-ttu-id="73749-159">After you toggle the switch, the control is labeled **Tokens View**.</span><span class="sxs-lookup"><span data-stu-id="73749-159">After you toggle the switch, the control is labeled **Tokens View**.</span></span>

1. <span data-ttu-id="73749-160">In the utterance, `Displace 425-555-0000 away from g-2323 toward hh-2345`, select the word `g-2323`.</span><span class="sxs-lookup"><span data-stu-id="73749-160">In the utterance, `Displace 425-555-0000 away from g-2323 toward hh-2345`, select the word `g-2323`.</span></span> <span data-ttu-id="73749-161">A drop-down menu appears with a text box at the top.</span><span class="sxs-lookup"><span data-stu-id="73749-161">A drop-down menu appears with a text box at the top.</span></span> <span data-ttu-id="73749-162">Enter the entity name `Locations` in the text box then select **Create new entity** in the drop-down menu.</span><span class="sxs-lookup"><span data-stu-id="73749-162">Enter the entity name `Locations` in the text box then select **Create new entity** in the drop-down menu.</span></span> 

    <span data-ttu-id="73749-163">[![](media/luis-quickstart-intent-and-hier-entity/hr-create-new-entity-1.png "Screenshot of creating new entity on intent page")](media/luis-quickstart-intent-and-hier-entity/hr-create-new-entity-1.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="73749-163">[![](media/luis-quickstart-intent-and-hier-entity/hr-create-new-entity-1.png "Screenshot of creating new entity on intent page")](media/luis-quickstart-intent-and-hier-entity/hr-create-new-entity-1.png#lightbox)</span></span>

2. <span data-ttu-id="73749-164">In the pop-up window, select the **Hierarchical** entity type with `Origin` and `Destination` as the child entities.</span><span class="sxs-lookup"><span data-stu-id="73749-164">In the pop-up window, select the **Hierarchical** entity type with `Origin` and `Destination` as the child entities.</span></span> <span data-ttu-id="73749-165">Select **Done**.</span><span class="sxs-lookup"><span data-stu-id="73749-165">Select **Done**.</span></span>

    <span data-ttu-id="73749-166">![](media/luis-quickstart-intent-and-hier-entity/hr-create-new-entity-2.png "Screenshot of entity creation pop-up dialog for new Location entity")</span><span class="sxs-lookup"><span data-stu-id="73749-166">![](media/luis-quickstart-intent-and-hier-entity/hr-create-new-entity-2.png "Screenshot of entity creation pop-up dialog for new Location entity")</span></span>

3. <span data-ttu-id="73749-167">The label for `g-2323` is marked as `Locations` because LUIS doesn't know if the term was the origin or destination, or neither.</span><span class="sxs-lookup"><span data-stu-id="73749-167">The label for `g-2323` is marked as `Locations` because LUIS doesn't know if the term was the origin or destination, or neither.</span></span> <span data-ttu-id="73749-168">Select `g-2323`, then select **Locations**, then follow the menu to the right and select `Origin`.</span><span class="sxs-lookup"><span data-stu-id="73749-168">Select `g-2323`, then select **Locations**, then follow the menu to the right and select `Origin`.</span></span>

    <span data-ttu-id="73749-169">[![](media/luis-quickstart-intent-and-hier-entity/hr-label-entity.png "Screenshot of entity labeling pop-up dialog to change locations entity child")](media/luis-quickstart-intent-and-hier-entity/hr-label-entity.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="73749-169">[![](media/luis-quickstart-intent-and-hier-entity/hr-label-entity.png "Screenshot of entity labeling pop-up dialog to change locations entity child")](media/luis-quickstart-intent-and-hier-entity/hr-label-entity.png#lightbox)</span></span>

5. <span data-ttu-id="73749-170">Label the other locations in all the other utterances by selecting the building and office in the utterance, then selecting Locations, then following the menu to the right to select `Origin` or `Destination`.</span><span class="sxs-lookup"><span data-stu-id="73749-170">Label the other locations in all the other utterances by selecting the building and office in the utterance, then selecting Locations, then following the menu to the right to select `Origin` or `Destination`.</span></span> <span data-ttu-id="73749-171">When all locations are labeled, the utterances in **Tokens View** begin to look like a pattern.</span><span class="sxs-lookup"><span data-stu-id="73749-171">When all locations are labeled, the utterances in **Tokens View** begin to look like a pattern.</span></span> 

    <span data-ttu-id="73749-172">[![](media/luis-quickstart-intent-and-hier-entity/hr-entities-labeled.png "Screenshot of Locations entity labeled in utterances")](media/luis-quickstart-intent-and-hier-entity/hr-entities-labeled.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="73749-172">[![](media/luis-quickstart-intent-and-hier-entity/hr-entities-labeled.png "Screenshot of Locations entity labeled in utterances")](media/luis-quickstart-intent-and-hier-entity/hr-entities-labeled.png#lightbox)</span></span>

## <a name="add-prebuilt-number-entity-to-app"></a><span data-ttu-id="73749-173">Add prebuilt number entity to app</span><span class="sxs-lookup"><span data-stu-id="73749-173">Add prebuilt number entity to app</span></span>
<span data-ttu-id="73749-174">Add the prebuilt number entity back to the application.</span><span class="sxs-lookup"><span data-stu-id="73749-174">Add the prebuilt number entity back to the application.</span></span>

1. <span data-ttu-id="73749-175">Select **Entities** from the left navigation menu.</span><span class="sxs-lookup"><span data-stu-id="73749-175">Select **Entities** from the left navigation menu.</span></span>

2. <span data-ttu-id="73749-176">Select **Manage prebuilt entities** button.</span><span class="sxs-lookup"><span data-stu-id="73749-176">Select **Manage prebuilt entities** button.</span></span>

    <span data-ttu-id="73749-177">[ ![Screenshot of Entities list with Manage prebuilt entities highlighted](./media/luis-quickstart-intent-and-hier-entity/hr-manage-prebuilt-button.png)](./media/luis-quickstart-intent-and-hier-entity/hr-manage-prebuilt-button.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="73749-177">[ ![Screenshot of Entities list with Manage prebuilt entities highlighted](./media/luis-quickstart-intent-and-hier-entity/hr-manage-prebuilt-button.png)](./media/luis-quickstart-intent-and-hier-entity/hr-manage-prebuilt-button.png#lightbox)</span></span>

3. <span data-ttu-id="73749-178">Select **number** from the list of prebuilt entities then select **Done**.</span><span class="sxs-lookup"><span data-stu-id="73749-178">Select **number** from the list of prebuilt entities then select **Done**.</span></span>

    ![Screenshot of number select in prebuilt entities dialog](./media/luis-quickstart-intent-and-hier-entity/hr-add-number-back-ddl.png)

## <a name="train-the-luis-app"></a><span data-ttu-id="73749-180">Train the LUIS app</span><span class="sxs-lookup"><span data-stu-id="73749-180">Train the LUIS app</span></span>

[!INCLUDE [LUIS How to Train steps](../../../includes/cognitive-services-luis-tutorial-how-to-train.md)]

## <a name="publish-the-app-to-get-the-endpoint-url"></a><span data-ttu-id="73749-181">Publish the app to get the endpoint URL</span><span class="sxs-lookup"><span data-stu-id="73749-181">Publish the app to get the endpoint URL</span></span>

[!INCLUDE [LUIS How to Publish steps](../../../includes/cognitive-services-luis-tutorial-how-to-publish.md)]

## <a name="query-the-endpoint-with-a-different-utterance"></a><span data-ttu-id="73749-182">Query the endpoint with a different utterance</span><span class="sxs-lookup"><span data-stu-id="73749-182">Query the endpoint with a different utterance</span></span>

1. [!INCLUDE [LUIS How to get endpoint first step](../../../includes/cognitive-services-luis-tutorial-how-to-get-endpoint.md)]


2. <span data-ttu-id="73749-183">Go to the end of the URL in the address bar and enter `Please relocation jill-jones@mycompany.com from x-2345 to g-23456`.</span><span class="sxs-lookup"><span data-stu-id="73749-183">Go to the end of the URL in the address bar and enter `Please relocation jill-jones@mycompany.com from x-2345 to g-23456`.</span></span> <span data-ttu-id="73749-184">The last querystring parameter is `q`, the utterance **query**.</span><span class="sxs-lookup"><span data-stu-id="73749-184">The last querystring parameter is `q`, the utterance **query**.</span></span> <span data-ttu-id="73749-185">This utterance is not the same as any of the labeled utterances so it is a good test and should return the `MoveEmployee` intent with the hierarchical entity extracted.</span><span class="sxs-lookup"><span data-stu-id="73749-185">This utterance is not the same as any of the labeled utterances so it is a good test and should return the `MoveEmployee` intent with the hierarchical entity extracted.</span></span>

  ```JSON
  {
    "query": "Please relocation jill-jones@mycompany.com from x-2345 to g-23456",
    "topScoringIntent": {
      "intent": "MoveEmployee",
      "score": 0.9966052
    },
    "intents": [
      {
        "intent": "MoveEmployee",
        "score": 0.9966052
      },
      {
        "intent": "Utilities.Stop",
        "score": 0.0325253047
      },
      {
        "intent": "FindForm",
        "score": 0.006137873
      },
      {
        "intent": "GetJobInformation",
        "score": 0.00462633232
      },
      {
        "intent": "Utilities.StartOver",
        "score": 0.00415637763
      },
      {
        "intent": "ApplyForJob",
        "score": 0.00382325822
      },
      {
        "intent": "Utilities.Help",
        "score": 0.00249120337
      },
      {
        "intent": "None",
        "score": 0.00130756292
      },
      {
        "intent": "Utilities.Cancel",
        "score": 0.00119622645
      },
      {
        "intent": "Utilities.Confirm",
        "score": 1.26910036E-05
      }
    ],
    "entities": [
      {
        "entity": "jill - jones @ mycompany . com",
        "type": "Employee",
        "startIndex": 18,
        "endIndex": 41,
        "resolution": {
          "values": [
            "Employee-45612"
          ]
        }
      },
      {
        "entity": "x - 2345",
        "type": "Locations::Origin",
        "startIndex": 48,
        "endIndex": 53,
        "score": 0.8520272
      },
      {
        "entity": "g - 23456",
        "type": "Locations::Destination",
        "startIndex": 58,
        "endIndex": 64,
        "score": 0.974032
      },
      {
        "entity": "-2345",
        "type": "builtin.number",
        "startIndex": 49,
        "endIndex": 53,
        "resolution": {
          "value": "-2345"
        }
      },
      {
        "entity": "-23456",
        "type": "builtin.number",
        "startIndex": 59,
        "endIndex": 64,
        "resolution": {
          "value": "-23456"
        }
      }
    ]
  }
  ```

## <a name="could-you-have-used-a-regular-expression-for-each-location"></a><span data-ttu-id="73749-186">Could you have used a regular expression for each location?</span><span class="sxs-lookup"><span data-stu-id="73749-186">Could you have used a regular expression for each location?</span></span>
<span data-ttu-id="73749-187">Yes, create the regular expression with origin and destination roles and use it in a pattern.</span><span class="sxs-lookup"><span data-stu-id="73749-187">Yes, create the regular expression with origin and destination roles and use it in a pattern.</span></span>

<span data-ttu-id="73749-188">The locations in this example, such as `a-1234`, follow a specific format of one or two letters with a dash then a series of 4 or 5 numerals.</span><span class="sxs-lookup"><span data-stu-id="73749-188">The locations in this example, such as `a-1234`, follow a specific format of one or two letters with a dash then a series of 4 or 5 numerals.</span></span> <span data-ttu-id="73749-189">This data can be described as a regular expression entity with a role for each location.</span><span class="sxs-lookup"><span data-stu-id="73749-189">This data can be described as a regular expression entity with a role for each location.</span></span> <span data-ttu-id="73749-190">Roles are available for patterns.</span><span class="sxs-lookup"><span data-stu-id="73749-190">Roles are available for patterns.</span></span> <span data-ttu-id="73749-191">You can create patterns based on these utterances, then create a regular expression for the location format and add it to the patterns.</span><span class="sxs-lookup"><span data-stu-id="73749-191">You can create patterns based on these utterances, then create a regular expression for the location format and add it to the patterns.</span></span> <!-- Go to this tutorial to see how that is done -->

## <a name="patterns-with-roles"></a><span data-ttu-id="73749-192">Patterns with roles</span><span class="sxs-lookup"><span data-stu-id="73749-192">Patterns with roles</span></span>

[!INCLUDE [LUIS Compare hierarchical entities to patterns with roles](../../../includes/cognitive-services-luis-hier-roles.md)]

## <a name="what-has-this-luis-app-accomplished"></a><span data-ttu-id="73749-193">What has this LUIS app accomplished?</span><span class="sxs-lookup"><span data-stu-id="73749-193">What has this LUIS app accomplished?</span></span>
<span data-ttu-id="73749-194">This app, with just a few intents and a hierarchical entity, identified a natural language query intention and returned the extracted data.</span><span class="sxs-lookup"><span data-stu-id="73749-194">This app, with just a few intents and a hierarchical entity, identified a natural language query intention and returned the extracted data.</span></span> 

<span data-ttu-id="73749-195">Your chatbot now has enough information to determine the primary action, `MoveEmployee`, and the location information found in the utterance.</span><span class="sxs-lookup"><span data-stu-id="73749-195">Your chatbot now has enough information to determine the primary action, `MoveEmployee`, and the location information found in the utterance.</span></span> 

## <a name="where-is-this-luis-data-used"></a><span data-ttu-id="73749-196">Where is this LUIS data used?</span><span class="sxs-lookup"><span data-stu-id="73749-196">Where is this LUIS data used?</span></span> 
<span data-ttu-id="73749-197">LUIS is done with this request.</span><span class="sxs-lookup"><span data-stu-id="73749-197">LUIS is done with this request.</span></span> <span data-ttu-id="73749-198">The calling application, such as a chatbot, can take the topScoringIntent result and the data from the entity to take the next step.</span><span class="sxs-lookup"><span data-stu-id="73749-198">The calling application, such as a chatbot, can take the topScoringIntent result and the data from the entity to take the next step.</span></span> <span data-ttu-id="73749-199">LUIS doesn't do that programmatic work for the bot or calling application.</span><span class="sxs-lookup"><span data-stu-id="73749-199">LUIS doesn't do that programmatic work for the bot or calling application.</span></span> <span data-ttu-id="73749-200">LUIS only determines what the user's intention is.</span><span class="sxs-lookup"><span data-stu-id="73749-200">LUIS only determines what the user's intention is.</span></span> 

## <a name="clean-up-resources"></a><span data-ttu-id="73749-201">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="73749-201">Clean up resources</span></span>

[!INCLUDE [LUIS How to clean up resources](../../../includes/cognitive-services-luis-tutorial-how-to-clean-up-resources.md)]

## <a name="next-steps"></a><span data-ttu-id="73749-202">Next steps</span><span class="sxs-lookup"><span data-stu-id="73749-202">Next steps</span></span>
> [!div class="nextstepaction"] 
> [<span data-ttu-id="73749-203">Learn how to add a composite entity</span><span class="sxs-lookup"><span data-stu-id="73749-203">Learn how to add a composite entity</span></span>](luis-tutorial-composite-entity.md) 