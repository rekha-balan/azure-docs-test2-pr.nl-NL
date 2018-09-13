---
title: Tutorial create a LUIS app that returns key phrases - Azure | Microsoft Docs
description: In this tutorial, learn how to add and return keyPhrase entity to your LUIS app to analyze utterances for key subject matter.
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: luis
ms.topic: tutorial
ms.date: 08/02/2018
ms.author: diberry
ms.openlocfilehash: ef7a1c81f453a8d4ff9526a4844518782e152c4f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865033"
---
# <a name="tutorial-8-add-keyphrase-entity"></a><span data-ttu-id="46928-103">Tutorial: 8.</span><span class="sxs-lookup"><span data-stu-id="46928-103">Tutorial: 8.</span></span> <span data-ttu-id="46928-104">Add keyPhrase entity</span><span class="sxs-lookup"><span data-stu-id="46928-104">Add keyPhrase entity</span></span> 
<span data-ttu-id="46928-105">In this tutorial, use an app that demonstrates how to extract key subject matter from utterances.</span><span class="sxs-lookup"><span data-stu-id="46928-105">In this tutorial, use an app that demonstrates how to extract key subject matter from utterances.</span></span>

<!-- green checkmark -->
> [!div class="checklist"]
> * <span data-ttu-id="46928-106">Understand keyPhrase entities</span><span class="sxs-lookup"><span data-stu-id="46928-106">Understand keyPhrase entities</span></span> 
> * <span data-ttu-id="46928-107">Use LUIS app in Human Resources (HR) domain</span><span class="sxs-lookup"><span data-stu-id="46928-107">Use LUIS app in Human Resources (HR) domain</span></span> 
> * <span data-ttu-id="46928-108">Add keyPhrase entity to extract content from utterance</span><span class="sxs-lookup"><span data-stu-id="46928-108">Add keyPhrase entity to extract content from utterance</span></span>
> * <span data-ttu-id="46928-109">Train, and publish app</span><span class="sxs-lookup"><span data-stu-id="46928-109">Train, and publish app</span></span>
> * <span data-ttu-id="46928-110">Query endpoint of app to see LUIS JSON response including key phrases</span><span class="sxs-lookup"><span data-stu-id="46928-110">Query endpoint of app to see LUIS JSON response including key phrases</span></span>

[!INCLUDE [LUIS Free account](../../../includes/cognitive-services-luis-free-key-short.md)]

## <a name="before-you-begin"></a><span data-ttu-id="46928-111">Before you begin</span><span class="sxs-lookup"><span data-stu-id="46928-111">Before you begin</span></span>
<span data-ttu-id="46928-112">If you don't have the Human Resources app from the [simple entity](luis-quickstart-primary-and-secondary-data.md) tutorial, [import](luis-how-to-start-new-app.md#import-new-app) the JSON into a new app in the [LUIS](luis-reference-regions.md#luis-website) website.</span><span class="sxs-lookup"><span data-stu-id="46928-112">If you don't have the Human Resources app from the [simple entity](luis-quickstart-primary-and-secondary-data.md) tutorial, [import](luis-how-to-start-new-app.md#import-new-app) the JSON into a new app in the [LUIS](luis-reference-regions.md#luis-website) website.</span></span> <span data-ttu-id="46928-113">The app to import is found in the [LUIS-Samples](https://github.com/Microsoft/LUIS-Samples/blob/master/documentation-samples/quickstarts/custom-domain-simple-HumanResources.json) Github repository.</span><span class="sxs-lookup"><span data-stu-id="46928-113">The app to import is found in the [LUIS-Samples](https://github.com/Microsoft/LUIS-Samples/blob/master/documentation-samples/quickstarts/custom-domain-simple-HumanResources.json) Github repository.</span></span>

<span data-ttu-id="46928-114">If you want to keep the original Human Resources app, clone the version on the [Settings](luis-how-to-manage-versions.md#clone-a-version) page, and name it `keyphrase`.</span><span class="sxs-lookup"><span data-stu-id="46928-114">If you want to keep the original Human Resources app, clone the version on the [Settings](luis-how-to-manage-versions.md#clone-a-version) page, and name it `keyphrase`.</span></span> <span data-ttu-id="46928-115">Cloning is a great way to play with various LUIS features without affecting the original version.</span><span class="sxs-lookup"><span data-stu-id="46928-115">Cloning is a great way to play with various LUIS features without affecting the original version.</span></span> 

## <a name="keyphrase-entity-extraction"></a><span data-ttu-id="46928-116">keyPhrase entity extraction</span><span class="sxs-lookup"><span data-stu-id="46928-116">keyPhrase entity extraction</span></span>
<span data-ttu-id="46928-117">Key subject matter is provided by the prebuilt entity, **keyPhrase**.</span><span class="sxs-lookup"><span data-stu-id="46928-117">Key subject matter is provided by the prebuilt entity, **keyPhrase**.</span></span> <span data-ttu-id="46928-118">This entity returns key subject matter in the utterance.</span><span class="sxs-lookup"><span data-stu-id="46928-118">This entity returns key subject matter in the utterance.</span></span>

<span data-ttu-id="46928-119">The following utterances show examples of key phrases:</span><span class="sxs-lookup"><span data-stu-id="46928-119">The following utterances show examples of key phrases:</span></span>

|<span data-ttu-id="46928-120">Utterance</span><span class="sxs-lookup"><span data-stu-id="46928-120">Utterance</span></span>|<span data-ttu-id="46928-121">keyPhrase entity values</span><span class="sxs-lookup"><span data-stu-id="46928-121">keyPhrase entity values</span></span>|
|--|--|
|<span data-ttu-id="46928-122">Is there a new medical plan with a lower deductible offered next year?</span><span class="sxs-lookup"><span data-stu-id="46928-122">Is there a new medical plan with a lower deductible offered next year?</span></span>|<span data-ttu-id="46928-123">"lower deductible"</span><span class="sxs-lookup"><span data-stu-id="46928-123">"lower deductible"</span></span><br><span data-ttu-id="46928-124">"new medical plan"</span><span class="sxs-lookup"><span data-stu-id="46928-124">"new medical plan"</span></span><br><span data-ttu-id="46928-125">"year"</span><span class="sxs-lookup"><span data-stu-id="46928-125">"year"</span></span>|
|<span data-ttu-id="46928-126">Is vision therapy covered in the high deductible medical plan?</span><span class="sxs-lookup"><span data-stu-id="46928-126">Is vision therapy covered in the high deductible medical plan?</span></span>|<span data-ttu-id="46928-127">"high deductible medical plan"</span><span class="sxs-lookup"><span data-stu-id="46928-127">"high deductible medical plan"</span></span><br><span data-ttu-id="46928-128">"vision therapy"</span><span class="sxs-lookup"><span data-stu-id="46928-128">"vision therapy"</span></span>|

<span data-ttu-id="46928-129">Your client application can use these values, along with other extracted entities, to decide the next step in the conversation.</span><span class="sxs-lookup"><span data-stu-id="46928-129">Your client application can use these values, along with other extracted entities, to decide the next step in the conversation.</span></span>

## <a name="add-keyphrase-entity"></a><span data-ttu-id="46928-130">Add keyPhrase entity</span><span class="sxs-lookup"><span data-stu-id="46928-130">Add keyPhrase entity</span></span> 
<span data-ttu-id="46928-131">Add keyPhrase prebuilt entity to extract subject matter from utterances.</span><span class="sxs-lookup"><span data-stu-id="46928-131">Add keyPhrase prebuilt entity to extract subject matter from utterances.</span></span>

1. <span data-ttu-id="46928-132">Make sure your Human Resources app is in the **Build** section of LUIS.</span><span class="sxs-lookup"><span data-stu-id="46928-132">Make sure your Human Resources app is in the **Build** section of LUIS.</span></span> <span data-ttu-id="46928-133">You can change to this section by selecting **Build** on the top, right menu bar.</span><span class="sxs-lookup"><span data-stu-id="46928-133">You can change to this section by selecting **Build** on the top, right menu bar.</span></span> 

2. <span data-ttu-id="46928-134">Select **Entities** from the left menu.</span><span class="sxs-lookup"><span data-stu-id="46928-134">Select **Entities** from the left menu.</span></span>

    <span data-ttu-id="46928-135">[ ![Screenshot of Entities highlighted in left nav of Build section](./media/luis-quickstart-intent-and-key-phrase/hr-select-entities-button.png)](./media/luis-quickstart-intent-and-key-phrase/hr-select-entities-button.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="46928-135">[ ![Screenshot of Entities highlighted in left nav of Build section](./media/luis-quickstart-intent-and-key-phrase/hr-select-entities-button.png)](./media/luis-quickstart-intent-and-key-phrase/hr-select-entities-button.png#lightbox)</span></span>

3. <span data-ttu-id="46928-136">Select **Manage prebuilt entities**.</span><span class="sxs-lookup"><span data-stu-id="46928-136">Select **Manage prebuilt entities**.</span></span>

    <span data-ttu-id="46928-137">[ ![Screenshot of Entities list pop-up dialog](./media/luis-quickstart-intent-and-key-phrase/hr-manage-prebuilt-entities.png)](./media/luis-quickstart-intent-and-key-phrase/hr-manage-prebuilt-entities.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="46928-137">[ ![Screenshot of Entities list pop-up dialog](./media/luis-quickstart-intent-and-key-phrase/hr-manage-prebuilt-entities.png)](./media/luis-quickstart-intent-and-key-phrase/hr-manage-prebuilt-entities.png#lightbox)</span></span>

4. <span data-ttu-id="46928-138">In the pop-up dialog, Select **keyPhrase**, then select **Done**.</span><span class="sxs-lookup"><span data-stu-id="46928-138">In the pop-up dialog, Select **keyPhrase**, then select **Done**.</span></span> 

    <span data-ttu-id="46928-139">[ ![Screenshot of Entities list pop-up dialog](./media/luis-quickstart-intent-and-key-phrase/hr-add-or-remove-prebuilt-entities.png)](./media/luis-quickstart-intent-and-key-phrase/hr-add-or-remove-prebuilt-entities.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="46928-139">[ ![Screenshot of Entities list pop-up dialog](./media/luis-quickstart-intent-and-key-phrase/hr-add-or-remove-prebuilt-entities.png)](./media/luis-quickstart-intent-and-key-phrase/hr-add-or-remove-prebuilt-entities.png#lightbox)</span></span>

    <!-- TBD: asking Carol
    You won't see these entities labeled in utterances on the intents pages. 
    -->
5. <span data-ttu-id="46928-140">Select **Intents** from the left menu, then select the **Utilities.Confirm** intent.</span><span class="sxs-lookup"><span data-stu-id="46928-140">Select **Intents** from the left menu, then select the **Utilities.Confirm** intent.</span></span> <span data-ttu-id="46928-141">The keyPhrase entity is labeled in several utterances.</span><span class="sxs-lookup"><span data-stu-id="46928-141">The keyPhrase entity is labeled in several utterances.</span></span> 

    <span data-ttu-id="46928-142">[ ![Screenshot of Utilities.Confirm intent with keyPhrases labeled in utterances](./media/luis-quickstart-intent-and-key-phrase/hr-keyphrase-labeled.png)](./media/luis-quickstart-intent-and-key-phrase/hr-keyphrase-labeled.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="46928-142">[ ![Screenshot of Utilities.Confirm intent with keyPhrases labeled in utterances](./media/luis-quickstart-intent-and-key-phrase/hr-keyphrase-labeled.png)](./media/luis-quickstart-intent-and-key-phrase/hr-keyphrase-labeled.png#lightbox)</span></span>

## <a name="train-the-luis-app"></a><span data-ttu-id="46928-143">Train the LUIS app</span><span class="sxs-lookup"><span data-stu-id="46928-143">Train the LUIS app</span></span>

[!INCLUDE [LUIS How to Train steps](../../../includes/cognitive-services-luis-tutorial-how-to-train.md)]

## <a name="publish-app-to-endpoint"></a><span data-ttu-id="46928-144">Publish app to endpoint</span><span class="sxs-lookup"><span data-stu-id="46928-144">Publish app to endpoint</span></span>

[!INCLUDE [LUIS How to Publish steps](../../../includes/cognitive-services-luis-tutorial-how-to-publish.md)]


## <a name="query-the-endpoint-with-an-utterance"></a><span data-ttu-id="46928-145">Query the endpoint with an utterance</span><span class="sxs-lookup"><span data-stu-id="46928-145">Query the endpoint with an utterance</span></span>

1. [!INCLUDE [LUIS How to get endpoint first step](../../../includes/cognitive-services-luis-tutorial-how-to-get-endpoint.md)]

2. <span data-ttu-id="46928-146">Go to the end of the URL in the address and enter `does form hrf-123456 cover the new dental benefits and medical plan`.</span><span class="sxs-lookup"><span data-stu-id="46928-146">Go to the end of the URL in the address and enter `does form hrf-123456 cover the new dental benefits and medical plan`.</span></span> <span data-ttu-id="46928-147">The last querystring parameter is `q`, the utterance **query**.</span><span class="sxs-lookup"><span data-stu-id="46928-147">The last querystring parameter is `q`, the utterance **query**.</span></span> 

```
{
  "query": "does form hrf-123456 cover the new dental benefits and medical plan",
  "topScoringIntent": {
    "intent": "FindForm",
    "score": 0.9300641
  },
  "intents": [
    {
      "intent": "FindForm",
      "score": 0.9300641
    },
    {
      "intent": "ApplyForJob",
      "score": 0.0359598845
    },
    {
      "intent": "GetJobInformation",
      "score": 0.0141798034
    },
    {
      "intent": "MoveEmployee",
      "score": 0.0112197418
    },
    {
      "intent": "Utilities.StartOver",
      "score": 0.00507669244
    },
    {
      "intent": "None",
      "score": 0.00238501839
    },
    {
      "intent": "Utilities.Help",
      "score": 0.00202810857
    },
    {
      "intent": "Utilities.Stop",
      "score": 0.00102957746
    },
    {
      "intent": "Utilities.Cancel",
      "score": 0.0008688423
    },
    {
      "intent": "Utilities.Confirm",
      "score": 3.557994E-05
    }
  ],
  "entities": [
    {
      "entity": "hrf-123456",
      "type": "HRF-number",git 
      "startIndex": 10,
      "endIndex": 19
    },
    {
      "entity": "new dental benefits",
      "type": "builtin.keyPhrase",
      "startIndex": 31,
      "endIndex": 49
    },
    {
      "entity": "medical plan",
      "type": "builtin.keyPhrase",
      "startIndex": 55,
      "endIndex": 66
    },
    {
      "entity": "hrf",
      "type": "builtin.keyPhrase",
      "startIndex": 10,
      "endIndex": 12
    },
    {
      "entity": "-123456",
      "type": "builtin.number",
      "startIndex": 13,
      "endIndex": 19,
      "resolution": {
        "value": "-123456"
      }
    }
  ]
}
```

<span data-ttu-id="46928-148">While searching for a form, the user provided more information than was necessary to find the form.</span><span class="sxs-lookup"><span data-stu-id="46928-148">While searching for a form, the user provided more information than was necessary to find the form.</span></span> <span data-ttu-id="46928-149">The additional information is returned as **builtin.keyPhrase**.</span><span class="sxs-lookup"><span data-stu-id="46928-149">The additional information is returned as **builtin.keyPhrase**.</span></span> <span data-ttu-id="46928-150">The client application can use this additional information for a follow-up question, such as "Would you like to talk to a Human Resource representative about new dental benefits" or provide a menu with more options including "More information about new dental benefits or medical plan."</span><span class="sxs-lookup"><span data-stu-id="46928-150">The client application can use this additional information for a follow-up question, such as "Would you like to talk to a Human Resource representative about new dental benefits" or provide a menu with more options including "More information about new dental benefits or medical plan."</span></span>

## <a name="what-has-this-luis-app-accomplished"></a><span data-ttu-id="46928-151">What has this LUIS app accomplished?</span><span class="sxs-lookup"><span data-stu-id="46928-151">What has this LUIS app accomplished?</span></span>
<span data-ttu-id="46928-152">This app, with keyPhrase entity detection, identified a natural language query intention and returned the extracted data including the main subject matter.</span><span class="sxs-lookup"><span data-stu-id="46928-152">This app, with keyPhrase entity detection, identified a natural language query intention and returned the extracted data including the main subject matter.</span></span> 

<span data-ttu-id="46928-153">Your chatbot now has enough information to determine the next step in the conversation.</span><span class="sxs-lookup"><span data-stu-id="46928-153">Your chatbot now has enough information to determine the next step in the conversation.</span></span> 

## <a name="where-is-this-luis-data-used"></a><span data-ttu-id="46928-154">Where is this LUIS data used?</span><span class="sxs-lookup"><span data-stu-id="46928-154">Where is this LUIS data used?</span></span> 
<span data-ttu-id="46928-155">LUIS is done with this request.</span><span class="sxs-lookup"><span data-stu-id="46928-155">LUIS is done with this request.</span></span> <span data-ttu-id="46928-156">The calling application, such as a chatbot, can take the topScoringIntent result and the keyPhrase data from the utterance to take the next step.</span><span class="sxs-lookup"><span data-stu-id="46928-156">The calling application, such as a chatbot, can take the topScoringIntent result and the keyPhrase data from the utterance to take the next step.</span></span> <span data-ttu-id="46928-157">LUIS doesn't do that programmatic work for the bot or calling application.</span><span class="sxs-lookup"><span data-stu-id="46928-157">LUIS doesn't do that programmatic work for the bot or calling application.</span></span> <span data-ttu-id="46928-158">LUIS only determines what the user's intention is.</span><span class="sxs-lookup"><span data-stu-id="46928-158">LUIS only determines what the user's intention is.</span></span> 

## <a name="clean-up-resources"></a><span data-ttu-id="46928-159">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="46928-159">Clean up resources</span></span>

[!INCLUDE [LUIS How to clean up resources](../../../includes/cognitive-services-luis-tutorial-how-to-clean-up-resources.md)]

## <a name="next-steps"></a><span data-ttu-id="46928-160">Next steps</span><span class="sxs-lookup"><span data-stu-id="46928-160">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="46928-161">Add sentiment analysis to app</span><span class="sxs-lookup"><span data-stu-id="46928-161">Add sentiment analysis to app</span></span>](luis-quickstart-intent-and-sentiment-analysis.md)