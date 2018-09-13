---
title: Tutorial creating a LUIS app to get regular-expression matched data - Azure | Microsoft Docs
description: In this tutorial, learn how to create a simple LUIS app using intents and a regular expression entity to extract data.
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: luis
ms.topic: tutorial
ms.date: 08/02/2018
ms.author: diberry
ms.openlocfilehash: 9672215c8cc5f95775e3b7fba74b27379a58ff49
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869655"
---
# <a name="tutorial-3-add-regular-expression-entity"></a><span data-ttu-id="d821e-103">Tutorial: 3.</span><span class="sxs-lookup"><span data-stu-id="d821e-103">Tutorial: 3.</span></span> <span data-ttu-id="d821e-104">Add regular expression entity</span><span class="sxs-lookup"><span data-stu-id="d821e-104">Add regular expression entity</span></span>
<span data-ttu-id="d821e-105">In this tutorial, create an app that demonstrates how to extract consistently formatted data from an utterance using the **Regular Expression** entity.</span><span class="sxs-lookup"><span data-stu-id="d821e-105">In this tutorial, create an app that demonstrates how to extract consistently formatted data from an utterance using the **Regular Expression** entity.</span></span>


<!-- green checkmark -->
> [!div class="checklist"]
> * <span data-ttu-id="d821e-106">Understand regular expression entities</span><span class="sxs-lookup"><span data-stu-id="d821e-106">Understand regular expression entities</span></span> 
> * <span data-ttu-id="d821e-107">Use a LUIS app for a Human Resources (HR) domain with FindForm intent</span><span class="sxs-lookup"><span data-stu-id="d821e-107">Use a LUIS app for a Human Resources (HR) domain with FindForm intent</span></span>
> * <span data-ttu-id="d821e-108">Add regular expression entity to extract Form number from utterance</span><span class="sxs-lookup"><span data-stu-id="d821e-108">Add regular expression entity to extract Form number from utterance</span></span>
> * <span data-ttu-id="d821e-109">Train, and publish app</span><span class="sxs-lookup"><span data-stu-id="d821e-109">Train, and publish app</span></span>
> * <span data-ttu-id="d821e-110">Query endpoint of app to see LUIS JSON response</span><span class="sxs-lookup"><span data-stu-id="d821e-110">Query endpoint of app to see LUIS JSON response</span></span>

[!INCLUDE [LUIS Free account](../../../includes/cognitive-services-luis-free-key-short.md)]

## <a name="before-you-begin"></a><span data-ttu-id="d821e-111">Before you begin</span><span class="sxs-lookup"><span data-stu-id="d821e-111">Before you begin</span></span>
<span data-ttu-id="d821e-112">If you do not have the Human Resources app from the [prebuilt entities](luis-tutorial-prebuilt-intents-entities.md) tutorial, [import](luis-how-to-start-new-app.md#import-new-app) the JSON into a new app in the [LUIS](luis-reference-regions.md#luis-website) website, from the [LUIS-Samples](https://github.com/Microsoft/LUIS-Samples/blob/master/documentation-samples/quickstarts/custom-domain-prebuilts-HumanResources.json) Github repository.</span><span class="sxs-lookup"><span data-stu-id="d821e-112">If you do not have the Human Resources app from the [prebuilt entities](luis-tutorial-prebuilt-intents-entities.md) tutorial, [import](luis-how-to-start-new-app.md#import-new-app) the JSON into a new app in the [LUIS](luis-reference-regions.md#luis-website) website, from the [LUIS-Samples](https://github.com/Microsoft/LUIS-Samples/blob/master/documentation-samples/quickstarts/custom-domain-prebuilts-HumanResources.json) Github repository.</span></span>

<span data-ttu-id="d821e-113">If you want to keep the original Human Resources app, clone the version on the [Settings](luis-how-to-manage-versions.md#clone-a-version) page, and name it `regex`.</span><span class="sxs-lookup"><span data-stu-id="d821e-113">If you want to keep the original Human Resources app, clone the version on the [Settings](luis-how-to-manage-versions.md#clone-a-version) page, and name it `regex`.</span></span> <span data-ttu-id="d821e-114">Cloning is a great way to play with various LUIS features without affecting the original version.</span><span class="sxs-lookup"><span data-stu-id="d821e-114">Cloning is a great way to play with various LUIS features without affecting the original version.</span></span> 


## <a name="purpose-of-the-regular-expression-entity"></a><span data-ttu-id="d821e-115">Purpose of the regular expression entity</span><span class="sxs-lookup"><span data-stu-id="d821e-115">Purpose of the regular expression entity</span></span>
<span data-ttu-id="d821e-116">The purpose of an entity is to get important data contained in the utterance.</span><span class="sxs-lookup"><span data-stu-id="d821e-116">The purpose of an entity is to get important data contained in the utterance.</span></span> <span data-ttu-id="d821e-117">The app's use of the regular expression entity is to pull out formatted Human Resources (HR) Form numbers from an utterance.</span><span class="sxs-lookup"><span data-stu-id="d821e-117">The app's use of the regular expression entity is to pull out formatted Human Resources (HR) Form numbers from an utterance.</span></span> <span data-ttu-id="d821e-118">It is not machine-learned.</span><span class="sxs-lookup"><span data-stu-id="d821e-118">It is not machine-learned.</span></span> 

<span data-ttu-id="d821e-119">Simple example utterances include:</span><span class="sxs-lookup"><span data-stu-id="d821e-119">Simple example utterances include:</span></span>

```
Where is HRF-123456?
Who authored HRF-123234?
HRF-456098 is published in French?
```

<span data-ttu-id="d821e-120">Abbreviated or slang versions of utterances include:</span><span class="sxs-lookup"><span data-stu-id="d821e-120">Abbreviated or slang versions of utterances include:</span></span>

```
HRF-456098
HRF-456098 date?
HRF-456098 title?
```
 
<span data-ttu-id="d821e-121">The regular expression entity to match the form number is `hrf-[0-9]{6}`.</span><span class="sxs-lookup"><span data-stu-id="d821e-121">The regular expression entity to match the form number is `hrf-[0-9]{6}`.</span></span> <span data-ttu-id="d821e-122">This regular expression matches the literal characters `hrf -` but ignores case and culture variants.</span><span class="sxs-lookup"><span data-stu-id="d821e-122">This regular expression matches the literal characters `hrf -` but ignores case and culture variants.</span></span> <span data-ttu-id="d821e-123">It matches digits 0-9, for 6 digits exactly.</span><span class="sxs-lookup"><span data-stu-id="d821e-123">It matches digits 0-9, for 6 digits exactly.</span></span>

<span data-ttu-id="d821e-124">HRF stands for human resources form.</span><span class="sxs-lookup"><span data-stu-id="d821e-124">HRF stands for human resources form.</span></span>

### <a name="tokenization-with-hyphens"></a><span data-ttu-id="d821e-125">Tokenization with hyphens</span><span class="sxs-lookup"><span data-stu-id="d821e-125">Tokenization with hyphens</span></span>
<span data-ttu-id="d821e-126">LUIS tokenizes the utterance when the utterance is added to an intent.</span><span class="sxs-lookup"><span data-stu-id="d821e-126">LUIS tokenizes the utterance when the utterance is added to an intent.</span></span> <span data-ttu-id="d821e-127">The tokenization for these utterances adds spaces before and after the hyphen, `Where is HRF - 123456?`  The regular expression is applied to the utterance in its raw form, before it is tokenized.</span><span class="sxs-lookup"><span data-stu-id="d821e-127">The tokenization for these utterances adds spaces before and after the hyphen, `Where is HRF - 123456?`  The regular expression is applied to the utterance in its raw form, before it is tokenized.</span></span> <span data-ttu-id="d821e-128">Because it is applied to the _raw_ form, the regular expression doesn't have to deal with word boundaries.</span><span class="sxs-lookup"><span data-stu-id="d821e-128">Because it is applied to the _raw_ form, the regular expression doesn't have to deal with word boundaries.</span></span> 


## <a name="add-findform-intent"></a><span data-ttu-id="d821e-129">Add FindForm intent</span><span class="sxs-lookup"><span data-stu-id="d821e-129">Add FindForm intent</span></span>

1. <span data-ttu-id="d821e-130">Make sure your Human Resources app is in the **Build** section of LUIS.</span><span class="sxs-lookup"><span data-stu-id="d821e-130">Make sure your Human Resources app is in the **Build** section of LUIS.</span></span> <span data-ttu-id="d821e-131">You can change to this section by selecting **Build** on the top, right menu bar.</span><span class="sxs-lookup"><span data-stu-id="d821e-131">You can change to this section by selecting **Build** on the top, right menu bar.</span></span> 

2. <span data-ttu-id="d821e-132">Select **Create new intent**.</span><span class="sxs-lookup"><span data-stu-id="d821e-132">Select **Create new intent**.</span></span> 

3. <span data-ttu-id="d821e-133">Enter `FindForm` in the pop-up dialog box then select **Done**.</span><span class="sxs-lookup"><span data-stu-id="d821e-133">Enter `FindForm` in the pop-up dialog box then select **Done**.</span></span> 

    ![Screenshot of create new intent dialog with Utilities in the search box](./media/luis-quickstart-intents-regex-entity/create-new-intent-ddl.png)

4. <span data-ttu-id="d821e-135">Add example utterances to the intent.</span><span class="sxs-lookup"><span data-stu-id="d821e-135">Add example utterances to the intent.</span></span>

    |<span data-ttu-id="d821e-136">Example utterances</span><span class="sxs-lookup"><span data-stu-id="d821e-136">Example utterances</span></span>|
    |--|
    |<span data-ttu-id="d821e-137">What is the URL for hrf-123456?</span><span class="sxs-lookup"><span data-stu-id="d821e-137">What is the URL for hrf-123456?</span></span>|
    |<span data-ttu-id="d821e-138">Where is hrf-345678?</span><span class="sxs-lookup"><span data-stu-id="d821e-138">Where is hrf-345678?</span></span>|
    |<span data-ttu-id="d821e-139">When was hrf-456098 updated?</span><span class="sxs-lookup"><span data-stu-id="d821e-139">When was hrf-456098 updated?</span></span>|
    |<span data-ttu-id="d821e-140">Did John Smith update hrf-234639 last week?</span><span class="sxs-lookup"><span data-stu-id="d821e-140">Did John Smith update hrf-234639 last week?</span></span>|
    |<span data-ttu-id="d821e-141">How many version of hrf-345123 are there?</span><span class="sxs-lookup"><span data-stu-id="d821e-141">How many version of hrf-345123 are there?</span></span>|
    |<span data-ttu-id="d821e-142">Who needs to authorize form hrf-123456?</span><span class="sxs-lookup"><span data-stu-id="d821e-142">Who needs to authorize form hrf-123456?</span></span>|
    |<span data-ttu-id="d821e-143">How many people need to sign off on hrf-345678?</span><span class="sxs-lookup"><span data-stu-id="d821e-143">How many people need to sign off on hrf-345678?</span></span>|
    |<span data-ttu-id="d821e-144">hrf-234123 date?</span><span class="sxs-lookup"><span data-stu-id="d821e-144">hrf-234123 date?</span></span>|
    |<span data-ttu-id="d821e-145">author of hrf-546234?</span><span class="sxs-lookup"><span data-stu-id="d821e-145">author of hrf-546234?</span></span>|
    |<span data-ttu-id="d821e-146">title of hrf-456234?</span><span class="sxs-lookup"><span data-stu-id="d821e-146">title of hrf-456234?</span></span>|

    <span data-ttu-id="d821e-147">[ ![Screenshot of Intent page with new utterances highlighted](./media/luis-quickstart-intents-regex-entity/findform-intent.png) ](./media/luis-quickstart-intents-regex-entity/findform-intent.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="d821e-147">[ ![Screenshot of Intent page with new utterances highlighted](./media/luis-quickstart-intents-regex-entity/findform-intent.png) ](./media/luis-quickstart-intents-regex-entity/findform-intent.png#lightbox)</span></span>

    <span data-ttu-id="d821e-148">The application has prebuilt number entity added from the previous tutorial, so each form number is tagged.</span><span class="sxs-lookup"><span data-stu-id="d821e-148">The application has prebuilt number entity added from the previous tutorial, so each form number is tagged.</span></span> <span data-ttu-id="d821e-149">This may be enough for your client application but the number won't be labeled with the type of number.</span><span class="sxs-lookup"><span data-stu-id="d821e-149">This may be enough for your client application but the number won't be labeled with the type of number.</span></span> <span data-ttu-id="d821e-150">Creating a new entity with an appropriate name allows the client application to process the entity appropriately when it is returned from LUIS.</span><span class="sxs-lookup"><span data-stu-id="d821e-150">Creating a new entity with an appropriate name allows the client application to process the entity appropriately when it is returned from LUIS.</span></span>

## <a name="create-an-hrf-number-regular-expression-entity"></a><span data-ttu-id="d821e-151">Create an HRF-number regular expression entity</span><span class="sxs-lookup"><span data-stu-id="d821e-151">Create an HRF-number regular expression entity</span></span> 
<span data-ttu-id="d821e-152">Create a regular expression entity to tell LUIS what an HRF-number format is in the following steps:</span><span class="sxs-lookup"><span data-stu-id="d821e-152">Create a regular expression entity to tell LUIS what an HRF-number format is in the following steps:</span></span>

1. <span data-ttu-id="d821e-153">Select **Entities** in the left panel.</span><span class="sxs-lookup"><span data-stu-id="d821e-153">Select **Entities** in the left panel.</span></span>

2. <span data-ttu-id="d821e-154">Select **Create new entity** button on the Entities Page.</span><span class="sxs-lookup"><span data-stu-id="d821e-154">Select **Create new entity** button on the Entities Page.</span></span> 

3. <span data-ttu-id="d821e-155">In the pop-up dialog, enter the new entity name `HRF-number`, select **RegEx** as the entity type, enter `hrf-[0-9]{6}` as the Regex, and then select **Done**.</span><span class="sxs-lookup"><span data-stu-id="d821e-155">In the pop-up dialog, enter the new entity name `HRF-number`, select **RegEx** as the entity type, enter `hrf-[0-9]{6}` as the Regex, and then select **Done**.</span></span>

    ![Screenshot of pop-up dialog setting new entity properties](./media/luis-quickstart-intents-regex-entity/create-regex-entity.png)

4. <span data-ttu-id="d821e-157">Select **Intents**, then **FindForm** intent to see the regular expression labeled in the utterances.</span><span class="sxs-lookup"><span data-stu-id="d821e-157">Select **Intents**, then **FindForm** intent to see the regular expression labeled in the utterances.</span></span> 

    <span data-ttu-id="d821e-158">[![Screenshot of Label utterance with existing entity and regex pattern](./media/luis-quickstart-intents-regex-entity/labeled-utterances-for-entity.png)](./media/luis-quickstart-intents-regex-entity/labeled-utterances-for-entity.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="d821e-158">[![Screenshot of Label utterance with existing entity and regex pattern](./media/luis-quickstart-intents-regex-entity/labeled-utterances-for-entity.png)](./media/luis-quickstart-intents-regex-entity/labeled-utterances-for-entity.png#lightbox)</span></span>

    <span data-ttu-id="d821e-159">Because the entity is not a machine-learned entity, the label is applied to the utterances and displayed in the LUIS website as soon as it is created.</span><span class="sxs-lookup"><span data-stu-id="d821e-159">Because the entity is not a machine-learned entity, the label is applied to the utterances and displayed in the LUIS website as soon as it is created.</span></span>

## <a name="train-the-luis-app"></a><span data-ttu-id="d821e-160">Train the LUIS app</span><span class="sxs-lookup"><span data-stu-id="d821e-160">Train the LUIS app</span></span>

[!INCLUDE [LUIS How to Train steps](../../../includes/cognitive-services-luis-tutorial-how-to-train.md)]

## <a name="publish-the-app-to-get-the-endpoint-url"></a><span data-ttu-id="d821e-161">Publish the app to get the endpoint URL</span><span class="sxs-lookup"><span data-stu-id="d821e-161">Publish the app to get the endpoint URL</span></span>

[!INCLUDE [LUIS How to Publish steps](../../../includes/cognitive-services-luis-tutorial-how-to-publish.md)]

## <a name="query-the-endpoint-with-a-different-utterance"></a><span data-ttu-id="d821e-162">Query the endpoint with a different utterance</span><span class="sxs-lookup"><span data-stu-id="d821e-162">Query the endpoint with a different utterance</span></span>

1. [!INCLUDE [LUIS How to get endpoint first step](../../../includes/cognitive-services-luis-tutorial-how-to-get-endpoint.md)]

2. <span data-ttu-id="d821e-163">Go to the end of the URL in the address and enter `When were HRF-123456 and hrf-234567 published in the last year?`.</span><span class="sxs-lookup"><span data-stu-id="d821e-163">Go to the end of the URL in the address and enter `When were HRF-123456 and hrf-234567 published in the last year?`.</span></span> <span data-ttu-id="d821e-164">The last querystring parameter is `q`, the utterance **query**.</span><span class="sxs-lookup"><span data-stu-id="d821e-164">The last querystring parameter is `q`, the utterance **query**.</span></span> <span data-ttu-id="d821e-165">This utterance is not the same as any of the labeled utterances so it is a good test and should return the `FindForm` intent with the two form numbers of `HRF-123456` and `hrf-234567`.</span><span class="sxs-lookup"><span data-stu-id="d821e-165">This utterance is not the same as any of the labeled utterances so it is a good test and should return the `FindForm` intent with the two form numbers of `HRF-123456` and `hrf-234567`.</span></span>

    ```
    {
      "query": "When were HRF-123456 and hrf-234567 published in the last year?",
      "topScoringIntent": {
        "intent": "FindForm",
        "score": 0.9993477
      },
      "intents": [
        {
          "intent": "FindForm",
          "score": 0.9993477
        },
        {
          "intent": "ApplyForJob",
          "score": 0.0206110049
        },
        {
          "intent": "GetJobInformation",
          "score": 0.00533067342
        },
        {
          "intent": "Utilities.StartOver",
          "score": 0.004215215
        },
        {
          "intent": "Utilities.Help",
          "score": 0.00209096959
        },
        {
          "intent": "None",
          "score": 0.0017655947
        },
        {
          "intent": "Utilities.Stop",
          "score": 0.00109490135
        },
        {
          "intent": "Utilities.Confirm",
          "score": 0.0005704638
        },
        {
          "intent": "Utilities.Cancel",
          "score": 0.000525338168
        }
      ],
      "entities": [
        {
          "entity": "last year",
          "type": "builtin.datetimeV2.daterange",
          "startIndex": 53,
          "endIndex": 61,
          "resolution": {
            "values": [
              {
                "timex": "2017",
                "type": "daterange",
                "start": "2017-01-01",
                "end": "2018-01-01"
              }
            ]
          }
        },
        {
          "entity": "hrf-123456",
          "type": "HRF-number",
          "startIndex": 10,
          "endIndex": 19
        },
        {
          "entity": "hrf-234567",
          "type": "HRF-number",
          "startIndex": 25,
          "endIndex": 34
        },
        {
          "entity": "-123456",
          "type": "builtin.number",
          "startIndex": 13,
          "endIndex": 19,
          "resolution": {
            "value": "-123456"
          }
        },
        {
          "entity": "-234567",
          "type": "builtin.number",
          "startIndex": 28,
          "endIndex": 34,
          "resolution": {
            "value": "-234567"
          }
        }
      ]
    }
    ```

    <span data-ttu-id="d821e-166">The numbers in the utterance are returned twice, once as the new entity `hrf-number`, and once as a prebuilt entity, `number`.</span><span class="sxs-lookup"><span data-stu-id="d821e-166">The numbers in the utterance are returned twice, once as the new entity `hrf-number`, and once as a prebuilt entity, `number`.</span></span> <span data-ttu-id="d821e-167">An utterance can have more than one entity, and more than one of the same type of entity, as this example shows.</span><span class="sxs-lookup"><span data-stu-id="d821e-167">An utterance can have more than one entity, and more than one of the same type of entity, as this example shows.</span></span> <span data-ttu-id="d821e-168">By using a regular expression entity, LUIS extracts named data, which is more programmatically helpful to the client application receiving the JSON response.</span><span class="sxs-lookup"><span data-stu-id="d821e-168">By using a regular expression entity, LUIS extracts named data, which is more programmatically helpful to the client application receiving the JSON response.</span></span>

## <a name="what-has-this-luis-app-accomplished"></a><span data-ttu-id="d821e-169">What has this LUIS app accomplished?</span><span class="sxs-lookup"><span data-stu-id="d821e-169">What has this LUIS app accomplished?</span></span>
<span data-ttu-id="d821e-170">This app identified the intention and returned the extracted data.</span><span class="sxs-lookup"><span data-stu-id="d821e-170">This app identified the intention and returned the extracted data.</span></span> 

<span data-ttu-id="d821e-171">Your chatbot now has enough information to determine the primary action, `FindForm`, and which form numbers were in the search.</span><span class="sxs-lookup"><span data-stu-id="d821e-171">Your chatbot now has enough information to determine the primary action, `FindForm`, and which form numbers were in the search.</span></span> 

## <a name="where-is-this-luis-data-used"></a><span data-ttu-id="d821e-172">Where is this LUIS data used?</span><span class="sxs-lookup"><span data-stu-id="d821e-172">Where is this LUIS data used?</span></span> 
<span data-ttu-id="d821e-173">LUIS is done with this request.</span><span class="sxs-lookup"><span data-stu-id="d821e-173">LUIS is done with this request.</span></span> <span data-ttu-id="d821e-174">The calling application, such as a chatbot, can take the topScoringIntent result and the form numbers and search a third-party API.</span><span class="sxs-lookup"><span data-stu-id="d821e-174">The calling application, such as a chatbot, can take the topScoringIntent result and the form numbers and search a third-party API.</span></span> <span data-ttu-id="d821e-175">LUIS doesn't do that work.</span><span class="sxs-lookup"><span data-stu-id="d821e-175">LUIS doesn't do that work.</span></span> <span data-ttu-id="d821e-176">LUIS only determines what the user's intention is and extracts data about that intention.</span><span class="sxs-lookup"><span data-stu-id="d821e-176">LUIS only determines what the user's intention is and extracts data about that intention.</span></span> 

## <a name="clean-up-resources"></a><span data-ttu-id="d821e-177">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="d821e-177">Clean up resources</span></span>

[!INCLUDE [LUIS How to clean up resources](../../../includes/cognitive-services-luis-tutorial-how-to-clean-up-resources.md)]

## <a name="next-steps"></a><span data-ttu-id="d821e-178">Next steps</span><span class="sxs-lookup"><span data-stu-id="d821e-178">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d821e-179">Learn about the list entity</span><span class="sxs-lookup"><span data-stu-id="d821e-179">Learn about the list entity</span></span>](luis-quickstart-intent-and-list-entity.md)

