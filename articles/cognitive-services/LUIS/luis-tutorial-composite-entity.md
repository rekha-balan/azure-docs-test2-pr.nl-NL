---
title: Tutorial creating a composite entity to extract complex data - Azure | Microsoft Docs
description: Learn how to create a composite entity in your LUIS app to extract different types of entity data.
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: luis
ms.topic: article
ms.date: 08/02/2018
ms.author: diberry
ms.openlocfilehash: 17a8110624975d8053ad69c5bf30477e6d715ee8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866351"
---
# <a name="tutorial-6-add-composite-entity"></a><span data-ttu-id="79ca0-103">Tutorial: 6.</span><span class="sxs-lookup"><span data-stu-id="79ca0-103">Tutorial: 6.</span></span> <span data-ttu-id="79ca0-104">Add Composite entity</span><span class="sxs-lookup"><span data-stu-id="79ca0-104">Add Composite entity</span></span> 
<span data-ttu-id="79ca0-105">In this tutorial, add a composite entity to bundle extracted data into a containing entity.</span><span class="sxs-lookup"><span data-stu-id="79ca0-105">In this tutorial, add a composite entity to bundle extracted data into a containing entity.</span></span>

<span data-ttu-id="79ca0-106">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="79ca0-106">In this tutorial, you learn how to:</span></span>

<!-- green checkmark -->
> [!div class="checklist"]
> * <span data-ttu-id="79ca0-107">Understand composite entities</span><span class="sxs-lookup"><span data-stu-id="79ca0-107">Understand composite entities</span></span> 
> * <span data-ttu-id="79ca0-108">Add composite entity to extract data</span><span class="sxs-lookup"><span data-stu-id="79ca0-108">Add composite entity to extract data</span></span>
> * <span data-ttu-id="79ca0-109">Train, and publish app</span><span class="sxs-lookup"><span data-stu-id="79ca0-109">Train, and publish app</span></span>
> * <span data-ttu-id="79ca0-110">Query endpoint of app to see LUIS JSON response</span><span class="sxs-lookup"><span data-stu-id="79ca0-110">Query endpoint of app to see LUIS JSON response</span></span>

[!INCLUDE [LUIS Free account](../../../includes/cognitive-services-luis-free-key-short.md)]

## <a name="before-you-begin"></a><span data-ttu-id="79ca0-111">Before you begin</span><span class="sxs-lookup"><span data-stu-id="79ca0-111">Before you begin</span></span>
<span data-ttu-id="79ca0-112">If you don't have the Human Resources app from the [hierarchical entity](luis-quickstart-intent-and-hier-entity.md) tutorial, [import](luis-how-to-start-new-app.md#import-new-app) the JSON into a new app in the [LUIS](luis-reference-regions.md#luis-website) website.</span><span class="sxs-lookup"><span data-stu-id="79ca0-112">If you don't have the Human Resources app from the [hierarchical entity](luis-quickstart-intent-and-hier-entity.md) tutorial, [import](luis-how-to-start-new-app.md#import-new-app) the JSON into a new app in the [LUIS](luis-reference-regions.md#luis-website) website.</span></span> <span data-ttu-id="79ca0-113">The app to import is found in the [LUIS-Samples](https://github.com/Microsoft/LUIS-Samples/blob/master/documentation-samples/quickstarts/custom-domain-hier-HumanResources.json) Github repository.</span><span class="sxs-lookup"><span data-stu-id="79ca0-113">The app to import is found in the [LUIS-Samples](https://github.com/Microsoft/LUIS-Samples/blob/master/documentation-samples/quickstarts/custom-domain-hier-HumanResources.json) Github repository.</span></span>

<span data-ttu-id="79ca0-114">If you want to keep the original Human Resources app, clone the version on the [Settings](luis-how-to-manage-versions.md#clone-a-version) page, and name it `composite`.</span><span class="sxs-lookup"><span data-stu-id="79ca0-114">If you want to keep the original Human Resources app, clone the version on the [Settings](luis-how-to-manage-versions.md#clone-a-version) page, and name it `composite`.</span></span> <span data-ttu-id="79ca0-115">Cloning is a great way to play with various LUIS features without affecting the original version.</span><span class="sxs-lookup"><span data-stu-id="79ca0-115">Cloning is a great way to play with various LUIS features without affecting the original version.</span></span>  

## <a name="composite-entity-is-a-logical-grouping"></a><span data-ttu-id="79ca0-116">Composite entity is a logical grouping</span><span class="sxs-lookup"><span data-stu-id="79ca0-116">Composite entity is a logical grouping</span></span> 
<span data-ttu-id="79ca0-117">The purpose of the composite entity is to group related entities into a parent category entity.</span><span class="sxs-lookup"><span data-stu-id="79ca0-117">The purpose of the composite entity is to group related entities into a parent category entity.</span></span> <span data-ttu-id="79ca0-118">The information exists as separate entities before a composite is created.</span><span class="sxs-lookup"><span data-stu-id="79ca0-118">The information exists as separate entities before a composite is created.</span></span> <span data-ttu-id="79ca0-119">It is similar to hierarchical entity but can contain more types of entities.</span><span class="sxs-lookup"><span data-stu-id="79ca0-119">It is similar to hierarchical entity but can contain more types of entities.</span></span> 

 <span data-ttu-id="79ca0-120">Create a composite entity when the separate entities can be logically grouped and this logical grouping is helpful to the client application.</span><span class="sxs-lookup"><span data-stu-id="79ca0-120">Create a composite entity when the separate entities can be logically grouped and this logical grouping is helpful to the client application.</span></span> 

<span data-ttu-id="79ca0-121">In this app, the employee name is defined in the **Employee** list entity and includes synonyms of name, email address, company phone extension, mobile phone number, and U.S. Federal tax ID.</span><span class="sxs-lookup"><span data-stu-id="79ca0-121">In this app, the employee name is defined in the **Employee** list entity and includes synonyms of name, email address, company phone extension, mobile phone number, and U.S. Federal tax ID.</span></span> 

<span data-ttu-id="79ca0-122">The **MoveEmployee** intent has example utterances to request an employee be moved from one building and office to another.</span><span class="sxs-lookup"><span data-stu-id="79ca0-122">The **MoveEmployee** intent has example utterances to request an employee be moved from one building and office to another.</span></span> <span data-ttu-id="79ca0-123">Building names are alphabetic: "A", "B", etc. while offices are numeric: "1234", "13245".</span><span class="sxs-lookup"><span data-stu-id="79ca0-123">Building names are alphabetic: "A", "B", etc. while offices are numeric: "1234", "13245".</span></span> 

<span data-ttu-id="79ca0-124">Example utterances in the **MoveEmployee** intent include:</span><span class="sxs-lookup"><span data-stu-id="79ca0-124">Example utterances in the **MoveEmployee** intent include:</span></span>

|<span data-ttu-id="79ca0-125">Example utterances</span><span class="sxs-lookup"><span data-stu-id="79ca0-125">Example utterances</span></span>|
|--|
|<span data-ttu-id="79ca0-126">Move John W .</span><span class="sxs-lookup"><span data-stu-id="79ca0-126">Move John W .</span></span> <span data-ttu-id="79ca0-127">Smith to a-2345</span><span class="sxs-lookup"><span data-stu-id="79ca0-127">Smith to a-2345</span></span>|
|<span data-ttu-id="79ca0-128">shift x12345 to h-1234 tomorrow</span><span class="sxs-lookup"><span data-stu-id="79ca0-128">shift x12345 to h-1234 tomorrow</span></span>|
 
<span data-ttu-id="79ca0-129">The move request should include at least the employee (using any synonym), and the final building and office location.</span><span class="sxs-lookup"><span data-stu-id="79ca0-129">The move request should include at least the employee (using any synonym), and the final building and office location.</span></span> <span data-ttu-id="79ca0-130">The request can also include the originating office as well as a date the move should happen.</span><span class="sxs-lookup"><span data-stu-id="79ca0-130">The request can also include the originating office as well as a date the move should happen.</span></span> 

<span data-ttu-id="79ca0-131">The extracted data from the endpoint should contain this information and return it at in a `RequestEmployeeMove` composite entity.</span><span class="sxs-lookup"><span data-stu-id="79ca0-131">The extracted data from the endpoint should contain this information and return it at in a `RequestEmployeeMove` composite entity.</span></span> 

## <a name="create-composite-entity"></a><span data-ttu-id="79ca0-132">Create composite entity</span><span class="sxs-lookup"><span data-stu-id="79ca0-132">Create composite entity</span></span>
1. <span data-ttu-id="79ca0-133">Make sure your Human Resources app is in the **Build** section of LUIS.</span><span class="sxs-lookup"><span data-stu-id="79ca0-133">Make sure your Human Resources app is in the **Build** section of LUIS.</span></span> <span data-ttu-id="79ca0-134">You can change to this section by selecting **Build** on the top, right menu bar.</span><span class="sxs-lookup"><span data-stu-id="79ca0-134">You can change to this section by selecting **Build** on the top, right menu bar.</span></span> 

2. <span data-ttu-id="79ca0-135">On the **Intents** page, select **MoveEmployee** intent.</span><span class="sxs-lookup"><span data-stu-id="79ca0-135">On the **Intents** page, select **MoveEmployee** intent.</span></span> 

3. <span data-ttu-id="79ca0-136">Select the magnifying glass icon on the tool bar to filter the utterances list.</span><span class="sxs-lookup"><span data-stu-id="79ca0-136">Select the magnifying glass icon on the tool bar to filter the utterances list.</span></span> 

    <span data-ttu-id="79ca0-137">[![](media/luis-tutorial-composite-entity/hr-moveemployee-magglass.png "Screenshot of LUIS on 'MoveEmployee' intent with magnifying glass button highlighted")](media/luis-tutorial-composite-entity/hr-moveemployee-magglass.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="79ca0-137">[![](media/luis-tutorial-composite-entity/hr-moveemployee-magglass.png "Screenshot of LUIS on 'MoveEmployee' intent with magnifying glass button highlighted")](media/luis-tutorial-composite-entity/hr-moveemployee-magglass.png#lightbox)</span></span>

4. <span data-ttu-id="79ca0-138">Enter `tomorrow` in the filter textbox to find the utterance `shift x12345 to h-1234 tomorrow`.</span><span class="sxs-lookup"><span data-stu-id="79ca0-138">Enter `tomorrow` in the filter textbox to find the utterance `shift x12345 to h-1234 tomorrow`.</span></span>

    <span data-ttu-id="79ca0-139">[![](media/luis-tutorial-composite-entity/hr-filter-by-tomorrow.png "Screenshot of LUIS on 'MoveEmployee' intent with filter of 'tomorrow' highlighted")](media/luis-tutorial-composite-entity/hr-filter-by-tomorrow.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="79ca0-139">[![](media/luis-tutorial-composite-entity/hr-filter-by-tomorrow.png "Screenshot of LUIS on 'MoveEmployee' intent with filter of 'tomorrow' highlighted")](media/luis-tutorial-composite-entity/hr-filter-by-tomorrow.png#lightbox)</span></span>

    <span data-ttu-id="79ca0-140">Another method is to filter the entity by datetimeV2, by selecting **Entity filters** then select **datetimeV2** from the list.</span><span class="sxs-lookup"><span data-stu-id="79ca0-140">Another method is to filter the entity by datetimeV2, by selecting **Entity filters** then select **datetimeV2** from the list.</span></span> 

5. <span data-ttu-id="79ca0-141">Select the first entity, `Employee`, then select **Wrap in composite entity** in the pop-up menu list.</span><span class="sxs-lookup"><span data-stu-id="79ca0-141">Select the first entity, `Employee`, then select **Wrap in composite entity** in the pop-up menu list.</span></span> 

    <span data-ttu-id="79ca0-142">[![](media/luis-tutorial-composite-entity/hr-create-entity-1.png "Screenshot of LUIS on 'MoveEmployee' intent selecting first entity in composite highlighted")](media/luis-tutorial-composite-entity/hr-create-entity-1.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="79ca0-142">[![](media/luis-tutorial-composite-entity/hr-create-entity-1.png "Screenshot of LUIS on 'MoveEmployee' intent selecting first entity in composite highlighted")](media/luis-tutorial-composite-entity/hr-create-entity-1.png#lightbox)</span></span>


6. <span data-ttu-id="79ca0-143">Then immediately select the last entity, `datetimeV2` in the utterance.</span><span class="sxs-lookup"><span data-stu-id="79ca0-143">Then immediately select the last entity, `datetimeV2` in the utterance.</span></span> <span data-ttu-id="79ca0-144">A green bar is drawn under the selected words indicating a composite entity.</span><span class="sxs-lookup"><span data-stu-id="79ca0-144">A green bar is drawn under the selected words indicating a composite entity.</span></span> <span data-ttu-id="79ca0-145">In the pop-up menu, enter the composite name `RequestEmployeeMove` then select **Create new composite** on in the pop-up menu.</span><span class="sxs-lookup"><span data-stu-id="79ca0-145">In the pop-up menu, enter the composite name `RequestEmployeeMove` then select **Create new composite** on in the pop-up menu.</span></span> 

    <span data-ttu-id="79ca0-146">[![](media/luis-tutorial-composite-entity/hr-create-entity-2.png "Screenshot of LUIS on 'MoveEmployee' intent selecting last entity in composite and creating entity highlighted")](media/luis-tutorial-composite-entity/hr-create-entity-2.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="79ca0-146">[![](media/luis-tutorial-composite-entity/hr-create-entity-2.png "Screenshot of LUIS on 'MoveEmployee' intent selecting last entity in composite and creating entity highlighted")](media/luis-tutorial-composite-entity/hr-create-entity-2.png#lightbox)</span></span>

7. <span data-ttu-id="79ca0-147">In **What type of entity do you want to create?**, almost all the fields required are in the list.</span><span class="sxs-lookup"><span data-stu-id="79ca0-147">In **What type of entity do you want to create?**, almost all the fields required are in the list.</span></span> <span data-ttu-id="79ca0-148">Only the originating location is missing.</span><span class="sxs-lookup"><span data-stu-id="79ca0-148">Only the originating location is missing.</span></span> <span data-ttu-id="79ca0-149">Select **Add a child entity**, select **Locations::Origin** from the list of existing entities, then select **Done**.</span><span class="sxs-lookup"><span data-stu-id="79ca0-149">Select **Add a child entity**, select **Locations::Origin** from the list of existing entities, then select **Done**.</span></span> 

    ![Screenshot of LUIS on 'MoveEmployee' intent adding another entity in pop-up window](media/luis-tutorial-composite-entity/hr-create-entity-ddl.png)

8. <span data-ttu-id="79ca0-151">Select the magnifying glass on the toolbar to remove the filter.</span><span class="sxs-lookup"><span data-stu-id="79ca0-151">Select the magnifying glass on the toolbar to remove the filter.</span></span> 

## <a name="label-example-utterances-with-composite-entity"></a><span data-ttu-id="79ca0-152">Label example utterances with composite entity</span><span class="sxs-lookup"><span data-stu-id="79ca0-152">Label example utterances with composite entity</span></span>
1. <span data-ttu-id="79ca0-153">In each example utterance, select the left-most entity that should be in the composite.</span><span class="sxs-lookup"><span data-stu-id="79ca0-153">In each example utterance, select the left-most entity that should be in the composite.</span></span> <span data-ttu-id="79ca0-154">Then select **Wrap in composite entity**.</span><span class="sxs-lookup"><span data-stu-id="79ca0-154">Then select **Wrap in composite entity**.</span></span>

    <span data-ttu-id="79ca0-155">[![](media/luis-tutorial-composite-entity/hr-label-entity-1.png "Screenshot of LUIS on 'MoveEmployee' intent selecting first entity in composite highlighted")](media/luis-tutorial-composite-entity/hr-label-entity-1.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="79ca0-155">[![](media/luis-tutorial-composite-entity/hr-label-entity-1.png "Screenshot of LUIS on 'MoveEmployee' intent selecting first entity in composite highlighted")](media/luis-tutorial-composite-entity/hr-label-entity-1.png#lightbox)</span></span>

2. <span data-ttu-id="79ca0-156">Select the last word in the composite entity then select **RequestEmployeeMove** from the pop-up menu.</span><span class="sxs-lookup"><span data-stu-id="79ca0-156">Select the last word in the composite entity then select **RequestEmployeeMove** from the pop-up menu.</span></span> 

    <span data-ttu-id="79ca0-157">[![](media/luis-tutorial-composite-entity/hr-label-entity-2.png "Screenshot of LUIS on 'MoveEmployee' intent selecting last entity in composite highlighted")](media/luis-tutorial-composite-entity/hr-label-entity-2.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="79ca0-157">[![](media/luis-tutorial-composite-entity/hr-label-entity-2.png "Screenshot of LUIS on 'MoveEmployee' intent selecting last entity in composite highlighted")](media/luis-tutorial-composite-entity/hr-label-entity-2.png#lightbox)</span></span>

3. <span data-ttu-id="79ca0-158">Verify all utterances in the intent are labeled with the composite entity.</span><span class="sxs-lookup"><span data-stu-id="79ca0-158">Verify all utterances in the intent are labeled with the composite entity.</span></span> 

    <span data-ttu-id="79ca0-159">[![](media/luis-tutorial-composite-entity/hr-all-utterances-labeled.png "Screenshot of LUIS on 'MoveEmployee' with all utterances labeled")](media/luis-tutorial-composite-entity/hr-all-utterances-labeled.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="79ca0-159">[![](media/luis-tutorial-composite-entity/hr-all-utterances-labeled.png "Screenshot of LUIS on 'MoveEmployee' with all utterances labeled")](media/luis-tutorial-composite-entity/hr-all-utterances-labeled.png#lightbox)</span></span>

## <a name="train-the-luis-app"></a><span data-ttu-id="79ca0-160">Train the LUIS app</span><span class="sxs-lookup"><span data-stu-id="79ca0-160">Train the LUIS app</span></span>

[!INCLUDE [LUIS How to Train steps](../../../includes/cognitive-services-luis-tutorial-how-to-train.md)]

## <a name="publish-the-app-to-get-the-endpoint-url"></a><span data-ttu-id="79ca0-161">Publish the app to get the endpoint URL</span><span class="sxs-lookup"><span data-stu-id="79ca0-161">Publish the app to get the endpoint URL</span></span>

[!INCLUDE [LUIS How to Publish steps](../../../includes/cognitive-services-luis-tutorial-how-to-publish.md)]

## <a name="query-the-endpoint"></a><span data-ttu-id="79ca0-162">Query the endpoint</span><span class="sxs-lookup"><span data-stu-id="79ca0-162">Query the endpoint</span></span> 

1. [!INCLUDE [LUIS How to get endpoint first step](../../../includes/cognitive-services-luis-tutorial-how-to-get-endpoint.md)]

2. <span data-ttu-id="79ca0-163">Go to the end of the URL in the address and enter `Move Jill Jones from a-1234 to z-2345 on March 3 2 p.m.`.</span><span class="sxs-lookup"><span data-stu-id="79ca0-163">Go to the end of the URL in the address and enter `Move Jill Jones from a-1234 to z-2345 on March 3 2 p.m.`.</span></span> <span data-ttu-id="79ca0-164">The last querystring parameter is `q`, the utterance query.</span><span class="sxs-lookup"><span data-stu-id="79ca0-164">The last querystring parameter is `q`, the utterance query.</span></span> 

    <span data-ttu-id="79ca0-165">Since this test is to verify the composite is extracted correctly, a test can either include an existing sample utterance or a new utterance.</span><span class="sxs-lookup"><span data-stu-id="79ca0-165">Since this test is to verify the composite is extracted correctly, a test can either include an existing sample utterance or a new utterance.</span></span> <span data-ttu-id="79ca0-166">A good test is to include all the child entities in the composite entity.</span><span class="sxs-lookup"><span data-stu-id="79ca0-166">A good test is to include all the child entities in the composite entity.</span></span>

    ```JSON
    {
      "query": "Move Jill Jones from a-1234 to z-2345 on March 3  2 p.m",
      "topScoringIntent": {
        "intent": "MoveEmployee",
        "score": 0.9959525
      },
      "intents": [
        {
          "intent": "MoveEmployee",
          "score": 0.9959525
        },
        {
          "intent": "GetJobInformation",
          "score": 0.009858314
        },
        {
          "intent": "ApplyForJob",
          "score": 0.00728598563
        },
        {
          "intent": "FindForm",
          "score": 0.0058053555
        },
        {
          "intent": "Utilities.StartOver",
          "score": 0.005371796
        },
        {
          "intent": "Utilities.Help",
          "score": 0.00266987388
        },
        {
          "intent": "None",
          "score": 0.00123299169
        },
        {
          "intent": "Utilities.Cancel",
          "score": 0.00116407464
        },
        {
          "intent": "Utilities.Confirm",
          "score": 0.00102653319
        },
        {
          "intent": "Utilities.Stop",
          "score": 0.0006628214
        }
      ],
      "entities": [
        {
          "entity": "march 3 2 p.m",
          "type": "builtin.datetimeV2.datetime",
          "startIndex": 41,
          "endIndex": 54,
          "resolution": {
            "values": [
              {
                "timex": "XXXX-03-03T14",
                "type": "datetime",
                "value": "2018-03-03 14:00:00"
              },
              {
                "timex": "XXXX-03-03T14",
                "type": "datetime",
                "value": "2019-03-03 14:00:00"
              }
            ]
          }
        },
        {
          "entity": "jill jones",
          "type": "Employee",
          "startIndex": 5,
          "endIndex": 14,
          "resolution": {
            "values": [
              "Employee-45612"
            ]
          }
        },
        {
          "entity": "z - 2345",
          "type": "Locations::Destination",
          "startIndex": 31,
          "endIndex": 36,
          "score": 0.9690751
        },
        {
          "entity": "a - 1234",
          "type": "Locations::Origin",
          "startIndex": 21,
          "endIndex": 26,
          "score": 0.9713137
        },
        {
          "entity": "-1234",
          "type": "builtin.number",
          "startIndex": 22,
          "endIndex": 26,
          "resolution": {
            "value": "-1234"
          }
        },
        {
          "entity": "-2345",
          "type": "builtin.number",
          "startIndex": 32,
          "endIndex": 36,
          "resolution": {
            "value": "-2345"
          }
        },
        {
          "entity": "3",
          "type": "builtin.number",
          "startIndex": 47,
          "endIndex": 47,
          "resolution": {
            "value": "3"
          }
        },
        {
          "entity": "2",
          "type": "builtin.number",
          "startIndex": 50,
          "endIndex": 50,
          "resolution": {
            "value": "2"
          }
        },
        {
          "entity": "jill jones from a - 1234 to z - 2345 on march 3 2 p . m",
          "type": "requestemployeemove",
          "startIndex": 5,
          "endIndex": 54,
          "score": 0.4027723
        }
      ],
      "compositeEntities": [
        {
          "parentType": "requestemployeemove",
          "value": "jill jones from a - 1234 to z - 2345 on march 3 2 p . m",
          "children": [
            {
              "type": "builtin.datetimeV2.datetime",
              "value": "march 3 2 p.m"
            },
            {
              "type": "Locations::Destination",
              "value": "z - 2345"
            },
            {
              "type": "Employee",
              "value": "jill jones"
            },
            {
              "type": "Locations::Origin",
              "value": "a - 1234"
            }
          ]
        }
      ],
      "sentimentAnalysis": {
        "label": "neutral",
        "score": 0.5
      }
    }
    ```

  <span data-ttu-id="79ca0-167">This utterance returns a composite entities array.</span><span class="sxs-lookup"><span data-stu-id="79ca0-167">This utterance returns a composite entities array.</span></span> <span data-ttu-id="79ca0-168">Each entity is given a type and value.</span><span class="sxs-lookup"><span data-stu-id="79ca0-168">Each entity is given a type and value.</span></span> <span data-ttu-id="79ca0-169">To find more precision for each child entity, use the combination of type and value from the composite array item to find the corresponding item in the entities array.</span><span class="sxs-lookup"><span data-stu-id="79ca0-169">To find more precision for each child entity, use the combination of type and value from the composite array item to find the corresponding item in the entities array.</span></span>  

## <a name="what-has-this-luis-app-accomplished"></a><span data-ttu-id="79ca0-170">What has this LUIS app accomplished?</span><span class="sxs-lookup"><span data-stu-id="79ca0-170">What has this LUIS app accomplished?</span></span>
<span data-ttu-id="79ca0-171">This app identified a natural language query intention and returned the extracted data as a named group.</span><span class="sxs-lookup"><span data-stu-id="79ca0-171">This app identified a natural language query intention and returned the extracted data as a named group.</span></span> 

<span data-ttu-id="79ca0-172">Your chatbot now has enough information to determine the primary action and the related details in the utterance.</span><span class="sxs-lookup"><span data-stu-id="79ca0-172">Your chatbot now has enough information to determine the primary action and the related details in the utterance.</span></span> 

## <a name="where-is-this-luis-data-used"></a><span data-ttu-id="79ca0-173">Where is this LUIS data used?</span><span class="sxs-lookup"><span data-stu-id="79ca0-173">Where is this LUIS data used?</span></span> 
<span data-ttu-id="79ca0-174">LUIS is done with this request.</span><span class="sxs-lookup"><span data-stu-id="79ca0-174">LUIS is done with this request.</span></span> <span data-ttu-id="79ca0-175">The calling application, such as a chatbot, can take the topScoringIntent result and the data from the entity to take the next step.</span><span class="sxs-lookup"><span data-stu-id="79ca0-175">The calling application, such as a chatbot, can take the topScoringIntent result and the data from the entity to take the next step.</span></span> <span data-ttu-id="79ca0-176">LUIS doesn't do that programmatic work for the bot or calling application.</span><span class="sxs-lookup"><span data-stu-id="79ca0-176">LUIS doesn't do that programmatic work for the bot or calling application.</span></span> <span data-ttu-id="79ca0-177">LUIS only determines what the user's intention is.</span><span class="sxs-lookup"><span data-stu-id="79ca0-177">LUIS only determines what the user's intention is.</span></span> 

## <a name="clean-up-resources"></a><span data-ttu-id="79ca0-178">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="79ca0-178">Clean up resources</span></span>

[!INCLUDE [LUIS How to clean up resources](../../../includes/cognitive-services-luis-tutorial-how-to-clean-up-resources.md)]

## <a name="next-steps"></a><span data-ttu-id="79ca0-179">Next steps</span><span class="sxs-lookup"><span data-stu-id="79ca0-179">Next steps</span></span>
> [!div class="nextstepaction"] 
> [<span data-ttu-id="79ca0-180">Learn how to add a simple entity with a phrase list</span><span class="sxs-lookup"><span data-stu-id="79ca0-180">Learn how to add a simple entity with a phrase list</span></span>](luis-quickstart-primary-and-secondary-data.md)  