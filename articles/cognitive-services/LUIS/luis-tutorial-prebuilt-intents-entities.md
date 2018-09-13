---
title: Add prebuilt intents and entities to extract common data in Language Understanding - Azure | Microsoft Docs
description: Learn how to use prebuilt intents and entities to extract different types of entity data.
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: luis
ms.topic: tutorial
ms.date: 08/03/2018
ms.author: diberry
ms.openlocfilehash: 0e45b659508c71a9f1220ef5e76b9a95438fa1e6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868079"
---
# <a name="tutorial-2-add-prebuilt-intents-and-entities"></a><span data-ttu-id="e8225-103">Tutorial: 2.</span><span class="sxs-lookup"><span data-stu-id="e8225-103">Tutorial: 2.</span></span> <span data-ttu-id="e8225-104">Add prebuilt intents and entities</span><span class="sxs-lookup"><span data-stu-id="e8225-104">Add prebuilt intents and entities</span></span>
<span data-ttu-id="e8225-105">Add prebuilt intents and entities to the Human Resources tutorial app to quickly gain intent prediction and data extraction.</span><span class="sxs-lookup"><span data-stu-id="e8225-105">Add prebuilt intents and entities to the Human Resources tutorial app to quickly gain intent prediction and data extraction.</span></span> 

<span data-ttu-id="e8225-106">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="e8225-106">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
* <span data-ttu-id="e8225-107">Add prebuilt intents</span><span class="sxs-lookup"><span data-stu-id="e8225-107">Add prebuilt intents</span></span> 
* <span data-ttu-id="e8225-108">Add prebuilt entities datetimeV2 and number</span><span class="sxs-lookup"><span data-stu-id="e8225-108">Add prebuilt entities datetimeV2 and number</span></span>
* <span data-ttu-id="e8225-109">Train and publish</span><span class="sxs-lookup"><span data-stu-id="e8225-109">Train and publish</span></span>
* <span data-ttu-id="e8225-110">Query LUIS and receive prediction response</span><span class="sxs-lookup"><span data-stu-id="e8225-110">Query LUIS and receive prediction response</span></span>

[!INCLUDE [LUIS Free account](../../../includes/cognitive-services-luis-free-key-short.md)]

## <a name="before-you-begin"></a><span data-ttu-id="e8225-111">Before you begin</span><span class="sxs-lookup"><span data-stu-id="e8225-111">Before you begin</span></span>
<span data-ttu-id="e8225-112">If you do not have the [Human Resources](luis-quickstart-intents-only.md) app from the previous tutorial, [import](luis-how-to-start-new-app.md#import-new-app) the JSON into a new app in the [LUIS](luis-reference-regions.md#luis-website) website, from the [LUIS-Samples](https://github.com/Microsoft/LUIS-Samples/blob/master/documentation-samples/quickstarts/custom-domain-intent-only-HumanResources.json) Github repository.</span><span class="sxs-lookup"><span data-stu-id="e8225-112">If you do not have the [Human Resources](luis-quickstart-intents-only.md) app from the previous tutorial, [import](luis-how-to-start-new-app.md#import-new-app) the JSON into a new app in the [LUIS](luis-reference-regions.md#luis-website) website, from the [LUIS-Samples](https://github.com/Microsoft/LUIS-Samples/blob/master/documentation-samples/quickstarts/custom-domain-intent-only-HumanResources.json) Github repository.</span></span>

<span data-ttu-id="e8225-113">If you want to keep the original Human Resources app, clone the version on the [Settings](luis-how-to-manage-versions.md#clone-a-version) page, and name it `prebuilts`.</span><span class="sxs-lookup"><span data-stu-id="e8225-113">If you want to keep the original Human Resources app, clone the version on the [Settings](luis-how-to-manage-versions.md#clone-a-version) page, and name it `prebuilts`.</span></span> <span data-ttu-id="e8225-114">Cloning is a great way to play with various LUIS features without affecting the original version.</span><span class="sxs-lookup"><span data-stu-id="e8225-114">Cloning is a great way to play with various LUIS features without affecting the original version.</span></span> 

## <a name="add-prebuilt-intents"></a><span data-ttu-id="e8225-115">Add prebuilt intents</span><span class="sxs-lookup"><span data-stu-id="e8225-115">Add prebuilt intents</span></span>
<span data-ttu-id="e8225-116">LUIS provides several prebuilt intents to help with common user intentions.</span><span class="sxs-lookup"><span data-stu-id="e8225-116">LUIS provides several prebuilt intents to help with common user intentions.</span></span>  

1. <span data-ttu-id="e8225-117">Make sure your app is in the **Build** section of LUIS.</span><span class="sxs-lookup"><span data-stu-id="e8225-117">Make sure your app is in the **Build** section of LUIS.</span></span> <span data-ttu-id="e8225-118">You can change to this section by selecting **Build** on the top, right menu bar.</span><span class="sxs-lookup"><span data-stu-id="e8225-118">You can change to this section by selecting **Build** on the top, right menu bar.</span></span> 

2. <span data-ttu-id="e8225-119">Select **Add prebuilt domain intent**.</span><span class="sxs-lookup"><span data-stu-id="e8225-119">Select **Add prebuilt domain intent**.</span></span> 

    <span data-ttu-id="e8225-120">[ ![Screenshot of Intents page with Add prebuilt domain intent button highlighted](./media/luis-tutorial-prebuilt-intents-and-entities/add-prebuilt-domain-button.png) ](./media/luis-tutorial-prebuilt-intents-and-entities/add-prebuilt-domain-button.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="e8225-120">[ ![Screenshot of Intents page with Add prebuilt domain intent button highlighted](./media/luis-tutorial-prebuilt-intents-and-entities/add-prebuilt-domain-button.png) ](./media/luis-tutorial-prebuilt-intents-and-entities/add-prebuilt-domain-button.png#lightbox)</span></span>

3. <span data-ttu-id="e8225-121">Search for `Utilities`.</span><span class="sxs-lookup"><span data-stu-id="e8225-121">Search for `Utilities`.</span></span> 

    <span data-ttu-id="e8225-122">[ ![Screenshot of prebuilt intents dialog with Utilities in the search box](./media/luis-tutorial-prebuilt-intents-and-entities/prebuilt-intent-utilities.png)](./media/luis-tutorial-prebuilt-intents-and-entities/prebuilt-intent-utilities.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="e8225-122">[ ![Screenshot of prebuilt intents dialog with Utilities in the search box](./media/luis-tutorial-prebuilt-intents-and-entities/prebuilt-intent-utilities.png)](./media/luis-tutorial-prebuilt-intents-and-entities/prebuilt-intent-utilities.png#lightbox)</span></span>

4. <span data-ttu-id="e8225-123">Select the following intents and select **Done**:</span><span class="sxs-lookup"><span data-stu-id="e8225-123">Select the following intents and select **Done**:</span></span> 

    * <span data-ttu-id="e8225-124">Utilities.Cancel</span><span class="sxs-lookup"><span data-stu-id="e8225-124">Utilities.Cancel</span></span>
    * <span data-ttu-id="e8225-125">Utilities.Confirm</span><span class="sxs-lookup"><span data-stu-id="e8225-125">Utilities.Confirm</span></span>
    * <span data-ttu-id="e8225-126">Utilities.Help</span><span class="sxs-lookup"><span data-stu-id="e8225-126">Utilities.Help</span></span>
    * <span data-ttu-id="e8225-127">Utilities.StartOver</span><span class="sxs-lookup"><span data-stu-id="e8225-127">Utilities.StartOver</span></span>
    * <span data-ttu-id="e8225-128">Utilities.Stop</span><span class="sxs-lookup"><span data-stu-id="e8225-128">Utilities.Stop</span></span>


## <a name="add-prebuilt-entities"></a><span data-ttu-id="e8225-129">Add prebuilt entities</span><span class="sxs-lookup"><span data-stu-id="e8225-129">Add prebuilt entities</span></span>
<span data-ttu-id="e8225-130">LUIS provides several prebuilt entities for common data extraction.</span><span class="sxs-lookup"><span data-stu-id="e8225-130">LUIS provides several prebuilt entities for common data extraction.</span></span> 

1. <span data-ttu-id="e8225-131">Select **Entities** from the left navigation menu.</span><span class="sxs-lookup"><span data-stu-id="e8225-131">Select **Entities** from the left navigation menu.</span></span>

    <span data-ttu-id="e8225-132">[ ![Screenshot of Intents list with Entities highlighted in left navigation](./media/luis-tutorial-prebuilt-intents-and-entities/entities-navigation.png)](./media/luis-tutorial-prebuilt-intents-and-entities/entities-navigation.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="e8225-132">[ ![Screenshot of Intents list with Entities highlighted in left navigation](./media/luis-tutorial-prebuilt-intents-and-entities/entities-navigation.png)](./media/luis-tutorial-prebuilt-intents-and-entities/entities-navigation.png#lightbox)</span></span>

2. <span data-ttu-id="e8225-133">Select **Manage prebuilt entities** button.</span><span class="sxs-lookup"><span data-stu-id="e8225-133">Select **Manage prebuilt entities** button.</span></span>

    <span data-ttu-id="e8225-134">[ ![Screenshot of Entities list with Manage prebuilt entities highlighted](./media/luis-tutorial-prebuilt-intents-and-entities/manage-prebuilt-entities-button.png)](./media/luis-tutorial-prebuilt-intents-and-entities/manage-prebuilt-entities-button.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="e8225-134">[ ![Screenshot of Entities list with Manage prebuilt entities highlighted](./media/luis-tutorial-prebuilt-intents-and-entities/manage-prebuilt-entities-button.png)](./media/luis-tutorial-prebuilt-intents-and-entities/manage-prebuilt-entities-button.png#lightbox)</span></span>

3. <span data-ttu-id="e8225-135">Select **number** and **datetimeV2** from the list of prebuilt entities then select **Done**.</span><span class="sxs-lookup"><span data-stu-id="e8225-135">Select **number** and **datetimeV2** from the list of prebuilt entities then select **Done**.</span></span>

    ![Screenshot of number select in prebuilt entities dialog](./media/luis-tutorial-prebuilt-intents-and-entities/select-prebuilt-entities.png)

## <a name="train-and-publish-the-app"></a><span data-ttu-id="e8225-137">Train and publish the app</span><span class="sxs-lookup"><span data-stu-id="e8225-137">Train and publish the app</span></span>

[!INCLUDE [LUIS How to Train steps](../../../includes/cognitive-services-luis-tutorial-how-to-train.md)]

## <a name="publish-app-to-endpoint"></a><span data-ttu-id="e8225-138">Publish app to endpoint</span><span class="sxs-lookup"><span data-stu-id="e8225-138">Publish app to endpoint</span></span>

[!INCLUDE [LUIS How to Publish steps](../../../includes/cognitive-services-luis-tutorial-how-to-publish.md)]

## <a name="query-endpoint-with-an-utterance"></a><span data-ttu-id="e8225-139">Query endpoint with an utterance</span><span class="sxs-lookup"><span data-stu-id="e8225-139">Query endpoint with an utterance</span></span>

1. [!INCLUDE [LUIS How to get endpoint first step](../../../includes/cognitive-services-luis-tutorial-how-to-get-endpoint.md)]

2. <span data-ttu-id="e8225-140">Go to the end of the URL in the address and enter `I want to cancel on March 3`.</span><span class="sxs-lookup"><span data-stu-id="e8225-140">Go to the end of the URL in the address and enter `I want to cancel on March 3`.</span></span> <span data-ttu-id="e8225-141">The last query string parameter is `q`, the utterance **query**.</span><span class="sxs-lookup"><span data-stu-id="e8225-141">The last query string parameter is `q`, the utterance **query**.</span></span> 

    <span data-ttu-id="e8225-142">The result predicted the Utilities.Cancel intent and extracted the date of March 3 and the number 3.</span><span class="sxs-lookup"><span data-stu-id="e8225-142">The result predicted the Utilities.Cancel intent and extracted the date of March 3 and the number 3.</span></span> 

    ```
    {
      "query": "I want to cancel on March 3",
      "topScoringIntent": {
        "intent": "Utilities.Cancel",
        "score": 0.7818295
      },
      "intents": [
        {
          "intent": "Utilities.Cancel",
          "score": 0.7818295
        },
        {
          "intent": "ApplyForJob",
          "score": 0.0237864349
        },
        {
          "intent": "GetJobInformation",
          "score": 0.017576348
        },
        {
          "intent": "Utilities.StartOver",
          "score": 0.0130122062
        },
        {
          "intent": "Utilities.Help",
          "score": 0.006731322
        },
        {
          "intent": "None",
          "score": 0.00524190161
        },
        {
          "intent": "Utilities.Stop",
          "score": 0.004912514
        },
        {
          "intent": "Utilities.Confirm",
          "score": 0.00092950504
        }
      ],
      "entities": [
        {
          "entity": "march 3",
          "type": "builtin.datetimeV2.date",
          "startIndex": 20,
          "endIndex": 26,
          "resolution": {
            "values": [
              {
                "timex": "XXXX-03-03",
                "type": "date",
                "value": "2018-03-03"
              },
              {
                "timex": "XXXX-03-03",
                "type": "date",
                "value": "2019-03-03"
              }
            ]
          }
        },
        {
          "entity": "3",
          "type": "builtin.number",
          "startIndex": 26,
          "endIndex": 26,
          "resolution": {
            "value": "3"
          }
        }
      ]
    }
    ```

    <span data-ttu-id="e8225-143">There are two values for March 3 because the utterance didn't state if March 3 is in the past or in the future.</span><span class="sxs-lookup"><span data-stu-id="e8225-143">There are two values for March 3 because the utterance didn't state if March 3 is in the past or in the future.</span></span> <span data-ttu-id="e8225-144">It is up to the LUIS-calling application to make an assumption or ask for clarification, if that is needed.</span><span class="sxs-lookup"><span data-stu-id="e8225-144">It is up to the LUIS-calling application to make an assumption or ask for clarification, if that is needed.</span></span> 

    <span data-ttu-id="e8225-145">By easily and quickly adding prebuilt intents and entities, the client application can add conversation management and extract common datatypes.</span><span class="sxs-lookup"><span data-stu-id="e8225-145">By easily and quickly adding prebuilt intents and entities, the client application can add conversation management and extract common datatypes.</span></span> 

## <a name="clean-up-resources"></a><span data-ttu-id="e8225-146">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="e8225-146">Clean up resources</span></span>

[!INCLUDE [LUIS How to clean up resources](../../../includes/cognitive-services-luis-tutorial-how-to-clean-up-resources.md)]

## <a name="next-steps"></a><span data-ttu-id="e8225-147">Next steps</span><span class="sxs-lookup"><span data-stu-id="e8225-147">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e8225-148">Add a regular expression entity to the app</span><span class="sxs-lookup"><span data-stu-id="e8225-148">Add a regular expression entity to the app</span></span>](luis-quickstart-intents-regex-entity.md)

