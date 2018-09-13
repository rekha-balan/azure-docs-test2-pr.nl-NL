---
title: Tutorial to review endpoint utterances in Language Understanding (LUIS) - Azure | Microsoft Docs
description: In this tutorial, learn how to review endpoint utterances in the Human Resources (HR) domain in LUIS.
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: luis
ms.topic: tutorial
ms.date: 08/03/2018
ms.author: diberry
ms.openlocfilehash: db44bfad5ece59ed3373699c10d6134201bf1879
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870841"
---
# <a name="tutorial-review-endpoint-utterances"></a><span data-ttu-id="2f83c-103">Tutorial: Review endpoint utterances</span><span class="sxs-lookup"><span data-stu-id="2f83c-103">Tutorial: Review endpoint utterances</span></span>
<span data-ttu-id="2f83c-104">In this tutorial, improve app predictions by verifying or correcting utterances received via the LUIS HTTP endpoint.</span><span class="sxs-lookup"><span data-stu-id="2f83c-104">In this tutorial, improve app predictions by verifying or correcting utterances received via the LUIS HTTP endpoint.</span></span> 

<!-- green checkmark -->
> [!div class="checklist"]
> * <span data-ttu-id="2f83c-105">Understand reviewing endpoint utterances</span><span class="sxs-lookup"><span data-stu-id="2f83c-105">Understand reviewing endpoint utterances</span></span> 
> * <span data-ttu-id="2f83c-106">Use LUIS app for the Human Resources (HR) domain</span><span class="sxs-lookup"><span data-stu-id="2f83c-106">Use LUIS app for the Human Resources (HR) domain</span></span> 
> * <span data-ttu-id="2f83c-107">Review endpoint utterances</span><span class="sxs-lookup"><span data-stu-id="2f83c-107">Review endpoint utterances</span></span>
> * <span data-ttu-id="2f83c-108">Train, and publish app</span><span class="sxs-lookup"><span data-stu-id="2f83c-108">Train, and publish app</span></span>
> * <span data-ttu-id="2f83c-109">Query endpoint of app to see LUIS JSON response</span><span class="sxs-lookup"><span data-stu-id="2f83c-109">Query endpoint of app to see LUIS JSON response</span></span>

[!INCLUDE [LUIS Free account](../../../includes/cognitive-services-luis-free-key-short.md)]

## <a name="before-you-begin"></a><span data-ttu-id="2f83c-110">Before you begin</span><span class="sxs-lookup"><span data-stu-id="2f83c-110">Before you begin</span></span>
<span data-ttu-id="2f83c-111">If you don't have the Human Resources app from the [sentiment](luis-quickstart-intent-and-sentiment-analysis.md) tutorial, import the app from [LUIS-Samples](https://github.com/Microsoft/LUIS-Samples/blob/master/documentation-samples/quickstarts/custom-domain-sentiment-HumanResources.json) Github repository.</span><span class="sxs-lookup"><span data-stu-id="2f83c-111">If you don't have the Human Resources app from the [sentiment](luis-quickstart-intent-and-sentiment-analysis.md) tutorial, import the app from [LUIS-Samples](https://github.com/Microsoft/LUIS-Samples/blob/master/documentation-samples/quickstarts/custom-domain-sentiment-HumanResources.json) Github repository.</span></span> <span data-ttu-id="2f83c-112">If you use this tutorial as a new, imported app, you also need to train, publish, then add the utterances to the endpoint with a [script](https://github.com/Microsoft/LUIS-Samples/blob/master/examples/demo-upload-endpoint-utterances/endpoint.js) or from the endpoint in a browser.</span><span class="sxs-lookup"><span data-stu-id="2f83c-112">If you use this tutorial as a new, imported app, you also need to train, publish, then add the utterances to the endpoint with a [script](https://github.com/Microsoft/LUIS-Samples/blob/master/examples/demo-upload-endpoint-utterances/endpoint.js) or from the endpoint in a browser.</span></span> <span data-ttu-id="2f83c-113">The utterances to add are:</span><span class="sxs-lookup"><span data-stu-id="2f83c-113">The utterances to add are:</span></span>

   [!code-nodejs[Node.js code showing endpoint utterances to add](~/samples-luis/examples/demo-upload-endpoint-utterances/endpoint.js?range=15-26)]

<span data-ttu-id="2f83c-114">If you want to keep the original Human Resources app, clone the version on the [Settings](luis-how-to-manage-versions.md#clone-a-version) page, and name it `review`.</span><span class="sxs-lookup"><span data-stu-id="2f83c-114">If you want to keep the original Human Resources app, clone the version on the [Settings](luis-how-to-manage-versions.md#clone-a-version) page, and name it `review`.</span></span> <span data-ttu-id="2f83c-115">Cloning is a great way to play with various LUIS features without affecting the original version.</span><span class="sxs-lookup"><span data-stu-id="2f83c-115">Cloning is a great way to play with various LUIS features without affecting the original version.</span></span> 

<span data-ttu-id="2f83c-116">If you have all the versions of the app, through the series of tutorials, you may be surprised to see that the **Review endpoint utterances** list doesn't change, based on the version.</span><span class="sxs-lookup"><span data-stu-id="2f83c-116">If you have all the versions of the app, through the series of tutorials, you may be surprised to see that the **Review endpoint utterances** list doesn't change, based on the version.</span></span> <span data-ttu-id="2f83c-117">There is a single pool of utterances to review, regardless of which version the utterance you are actively editing or which version of the app was published at the endpoint.</span><span class="sxs-lookup"><span data-stu-id="2f83c-117">There is a single pool of utterances to review, regardless of which version the utterance you are actively editing or which version of the app was published at the endpoint.</span></span> 

## <a name="purpose-of-reviewing-endpoint-utterances"></a><span data-ttu-id="2f83c-118">Purpose of reviewing endpoint utterances</span><span class="sxs-lookup"><span data-stu-id="2f83c-118">Purpose of reviewing endpoint utterances</span></span>
<span data-ttu-id="2f83c-119">This review process is another way for LUIS to learn your app domain.</span><span class="sxs-lookup"><span data-stu-id="2f83c-119">This review process is another way for LUIS to learn your app domain.</span></span> <span data-ttu-id="2f83c-120">LUIS selected the utterances in the review list.</span><span class="sxs-lookup"><span data-stu-id="2f83c-120">LUIS selected the utterances in the review list.</span></span> <span data-ttu-id="2f83c-121">This list is:</span><span class="sxs-lookup"><span data-stu-id="2f83c-121">This list is:</span></span>

* <span data-ttu-id="2f83c-122">Specific to the app.</span><span class="sxs-lookup"><span data-stu-id="2f83c-122">Specific to the app.</span></span>
* <span data-ttu-id="2f83c-123">Is meant to improve the app's prediction accuracy.</span><span class="sxs-lookup"><span data-stu-id="2f83c-123">Is meant to improve the app's prediction accuracy.</span></span> 
* <span data-ttu-id="2f83c-124">Should be reviewed on a periodic basis.</span><span class="sxs-lookup"><span data-stu-id="2f83c-124">Should be reviewed on a periodic basis.</span></span> 

<span data-ttu-id="2f83c-125">By reviewing the endpoint utterances, you verify or correct the utterance's predicted intent.</span><span class="sxs-lookup"><span data-stu-id="2f83c-125">By reviewing the endpoint utterances, you verify or correct the utterance's predicted intent.</span></span> <span data-ttu-id="2f83c-126">You also label custom entities that were not predicted.</span><span class="sxs-lookup"><span data-stu-id="2f83c-126">You also label custom entities that were not predicted.</span></span> 

## <a name="review-endpoint-utterances"></a><span data-ttu-id="2f83c-127">Review endpoint utterances</span><span class="sxs-lookup"><span data-stu-id="2f83c-127">Review endpoint utterances</span></span>

1. <span data-ttu-id="2f83c-128">Make sure your Human Resources app is in the **Build** section of LUIS.</span><span class="sxs-lookup"><span data-stu-id="2f83c-128">Make sure your Human Resources app is in the **Build** section of LUIS.</span></span> <span data-ttu-id="2f83c-129">You can change to this section by selecting **Build** on the top, right menu bar.</span><span class="sxs-lookup"><span data-stu-id="2f83c-129">You can change to this section by selecting **Build** on the top, right menu bar.</span></span> 

2. <span data-ttu-id="2f83c-130">Select **Review endpoint utterances** from the left navigation.</span><span class="sxs-lookup"><span data-stu-id="2f83c-130">Select **Review endpoint utterances** from the left navigation.</span></span> <span data-ttu-id="2f83c-131">The list is filtered for the **ApplyForJob** intent.</span><span class="sxs-lookup"><span data-stu-id="2f83c-131">The list is filtered for the **ApplyForJob** intent.</span></span> 

    <span data-ttu-id="2f83c-132">[ ![Screenshot of Review endpoint utterances button in left navigation](./media/luis-tutorial-review-endpoint-utterances/entities-view-endpoint-utterances.png)](./media/luis-tutorial-review-endpoint-utterances/entities-view-endpoint-utterances.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="2f83c-132">[ ![Screenshot of Review endpoint utterances button in left navigation](./media/luis-tutorial-review-endpoint-utterances/entities-view-endpoint-utterances.png)](./media/luis-tutorial-review-endpoint-utterances/entities-view-endpoint-utterances.png#lightbox)</span></span>

3. <span data-ttu-id="2f83c-133">Toggle the **Entities view** to see the labeled entities.</span><span class="sxs-lookup"><span data-stu-id="2f83c-133">Toggle the **Entities view** to see the labeled entities.</span></span> 
    
    <span data-ttu-id="2f83c-134">[ ![Screenshot of Review endpoint utterances with Entities view toggle highlighted](./media/luis-tutorial-review-endpoint-utterances/select-entities-view.png)](./media/luis-tutorial-review-endpoint-utterances/select-entities-view.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="2f83c-134">[ ![Screenshot of Review endpoint utterances with Entities view toggle highlighted](./media/luis-tutorial-review-endpoint-utterances/select-entities-view.png)](./media/luis-tutorial-review-endpoint-utterances/select-entities-view.png#lightbox)</span></span>

    |<span data-ttu-id="2f83c-135">Utterance</span><span class="sxs-lookup"><span data-stu-id="2f83c-135">Utterance</span></span>|<span data-ttu-id="2f83c-136">Correct intent</span><span class="sxs-lookup"><span data-stu-id="2f83c-136">Correct intent</span></span>|<span data-ttu-id="2f83c-137">Missing entities</span><span class="sxs-lookup"><span data-stu-id="2f83c-137">Missing entities</span></span>|
    |:--|:--|:--|
    |<span data-ttu-id="2f83c-138">I'm looking for a job with Natural Language Processing</span><span class="sxs-lookup"><span data-stu-id="2f83c-138">I'm looking for a job with Natural Language Processing</span></span>|<span data-ttu-id="2f83c-139">GetJobInfo</span><span class="sxs-lookup"><span data-stu-id="2f83c-139">GetJobInfo</span></span>|<span data-ttu-id="2f83c-140">Job - "Natural Language Process"</span><span class="sxs-lookup"><span data-stu-id="2f83c-140">Job - "Natural Language Process"</span></span>|

    <span data-ttu-id="2f83c-141">This utterance is not in the correct intent and has a score less than 50%.</span><span class="sxs-lookup"><span data-stu-id="2f83c-141">This utterance is not in the correct intent and has a score less than 50%.</span></span> <span data-ttu-id="2f83c-142">The **ApplyForJob** intent has 21 utterances compared to the seven utterances in **GetJobInformation**.</span><span class="sxs-lookup"><span data-stu-id="2f83c-142">The **ApplyForJob** intent has 21 utterances compared to the seven utterances in **GetJobInformation**.</span></span> <span data-ttu-id="2f83c-143">Along with aligning the endpoint utterance correctly, more utterances should be added to the **GetJobInformation** intent.</span><span class="sxs-lookup"><span data-stu-id="2f83c-143">Along with aligning the endpoint utterance correctly, more utterances should be added to the **GetJobInformation** intent.</span></span> <span data-ttu-id="2f83c-144">That is left as an exercise for you to complete on your own.</span><span class="sxs-lookup"><span data-stu-id="2f83c-144">That is left as an exercise for you to complete on your own.</span></span> <span data-ttu-id="2f83c-145">Each intent, except for the **None** intent, should have roughly the same number of example utterances.</span><span class="sxs-lookup"><span data-stu-id="2f83c-145">Each intent, except for the **None** intent, should have roughly the same number of example utterances.</span></span> <span data-ttu-id="2f83c-146">The **None** intent should have 10% of the total utterances in the app.</span><span class="sxs-lookup"><span data-stu-id="2f83c-146">The **None** intent should have 10% of the total utterances in the app.</span></span> 

    <span data-ttu-id="2f83c-147">When you are in **Tokens View**, you can hover over any blue text to the utterance to see the predicted entity name.</span><span class="sxs-lookup"><span data-stu-id="2f83c-147">When you are in **Tokens View**, you can hover over any blue text to the utterance to see the predicted entity name.</span></span> 

4. <span data-ttu-id="2f83c-148">For the intent `I'm looking for a job with Natual Language Processing`, select the correct intent, **GetJobInformation** in the **Aligned intent** column.</span><span class="sxs-lookup"><span data-stu-id="2f83c-148">For the intent `I'm looking for a job with Natual Language Processing`, select the correct intent, **GetJobInformation** in the **Aligned intent** column.</span></span> 

    <span data-ttu-id="2f83c-149">[ ![Screenshot of Review endpoint utterances aligning utterance to intent](./media/luis-tutorial-review-endpoint-utterances/align-intent-1.png)](./media/luis-tutorial-review-endpoint-utterances/align-intent-1.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="2f83c-149">[ ![Screenshot of Review endpoint utterances aligning utterance to intent](./media/luis-tutorial-review-endpoint-utterances/align-intent-1.png)](./media/luis-tutorial-review-endpoint-utterances/align-intent-1.png#lightbox)</span></span>

5. <span data-ttu-id="2f83c-150">In the same utterance, the entity for `Natural Language Processing` is keyPhrase.</span><span class="sxs-lookup"><span data-stu-id="2f83c-150">In the same utterance, the entity for `Natural Language Processing` is keyPhrase.</span></span> <span data-ttu-id="2f83c-151">This should be a **Job** entity instead.</span><span class="sxs-lookup"><span data-stu-id="2f83c-151">This should be a **Job** entity instead.</span></span> <span data-ttu-id="2f83c-152">Select `Natural Language Processing` then select the **Job** entity from the list.</span><span class="sxs-lookup"><span data-stu-id="2f83c-152">Select `Natural Language Processing` then select the **Job** entity from the list.</span></span>

    <span data-ttu-id="2f83c-153">[ ![Screenshot of Review endpoint utterances labeling entity in utterance](./media/luis-tutorial-review-endpoint-utterances/label-entity.png)](./media/luis-tutorial-review-endpoint-utterances/label-entity.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="2f83c-153">[ ![Screenshot of Review endpoint utterances labeling entity in utterance](./media/luis-tutorial-review-endpoint-utterances/label-entity.png)](./media/luis-tutorial-review-endpoint-utterances/label-entity.png#lightbox)</span></span>

6. <span data-ttu-id="2f83c-154">On the same line, select the circled checkmark in the **Add to aligned intent** column.</span><span class="sxs-lookup"><span data-stu-id="2f83c-154">On the same line, select the circled checkmark in the **Add to aligned intent** column.</span></span> 

    <span data-ttu-id="2f83c-155">[ ![Screenshot of finalizing utterance alignment in intent](./media/luis-tutorial-review-endpoint-utterances/align-utterance.png)](./media/luis-tutorial-review-endpoint-utterances/align-utterance.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="2f83c-155">[ ![Screenshot of finalizing utterance alignment in intent](./media/luis-tutorial-review-endpoint-utterances/align-utterance.png)](./media/luis-tutorial-review-endpoint-utterances/align-utterance.png#lightbox)</span></span>

    <span data-ttu-id="2f83c-156">This action moves the utterance from the **Review endpoint utterances** to the **GetJobInformation** intent.</span><span class="sxs-lookup"><span data-stu-id="2f83c-156">This action moves the utterance from the **Review endpoint utterances** to the **GetJobInformation** intent.</span></span> <span data-ttu-id="2f83c-157">The endpoint utterance is now an example utterance for that intent.</span><span class="sxs-lookup"><span data-stu-id="2f83c-157">The endpoint utterance is now an example utterance for that intent.</span></span> 

7. <span data-ttu-id="2f83c-158">Review the remaining utterances in this intent, labeling utterances and correcting the **Aligned intent**, if these are incorrect.</span><span class="sxs-lookup"><span data-stu-id="2f83c-158">Review the remaining utterances in this intent, labeling utterances and correcting the **Aligned intent**, if these are incorrect.</span></span>

8. <span data-ttu-id="2f83c-159">When all the utterances are correct, select the checkbox on each row, then select **Add selected** to align the utterances correctly.</span><span class="sxs-lookup"><span data-stu-id="2f83c-159">When all the utterances are correct, select the checkbox on each row, then select **Add selected** to align the utterances correctly.</span></span> 

    <span data-ttu-id="2f83c-160">[ ![Screenshot of finalizing remaining utterances to aligned intent](./media/luis-tutorial-review-endpoint-utterances/finalize-utterance-alignment.png)](./media/luis-tutorial-review-endpoint-utterances/finalize-utterance-alignment.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="2f83c-160">[ ![Screenshot of finalizing remaining utterances to aligned intent](./media/luis-tutorial-review-endpoint-utterances/finalize-utterance-alignment.png)](./media/luis-tutorial-review-endpoint-utterances/finalize-utterance-alignment.png#lightbox)</span></span>

9. <span data-ttu-id="2f83c-161">The list should no longer have those utterances.</span><span class="sxs-lookup"><span data-stu-id="2f83c-161">The list should no longer have those utterances.</span></span> <span data-ttu-id="2f83c-162">If more utterances appear, continue to work through the list, correcting intents and labeling any missing entities, until it is empty.</span><span class="sxs-lookup"><span data-stu-id="2f83c-162">If more utterances appear, continue to work through the list, correcting intents and labeling any missing entities, until it is empty.</span></span> <span data-ttu-id="2f83c-163">Select the next intent in the Filter list, then continue correcting utterances and labeling entities.</span><span class="sxs-lookup"><span data-stu-id="2f83c-163">Select the next intent in the Filter list, then continue correcting utterances and labeling entities.</span></span> <span data-ttu-id="2f83c-164">Remember the last step of each intent is to either select **Add to aligned intent** on the utterance row or check the box by each intent and select **Add selected** above the table.</span><span class="sxs-lookup"><span data-stu-id="2f83c-164">Remember the last step of each intent is to either select **Add to aligned intent** on the utterance row or check the box by each intent and select **Add selected** above the table.</span></span> 

    <span data-ttu-id="2f83c-165">This is a very small app.</span><span class="sxs-lookup"><span data-stu-id="2f83c-165">This is a very small app.</span></span> <span data-ttu-id="2f83c-166">The review process takes only a few minutes.</span><span class="sxs-lookup"><span data-stu-id="2f83c-166">The review process takes only a few minutes.</span></span>

## <a name="add-new-job-name-to-phrase-list"></a><span data-ttu-id="2f83c-167">Add new job name to phrase list</span><span class="sxs-lookup"><span data-stu-id="2f83c-167">Add new job name to phrase list</span></span>
<span data-ttu-id="2f83c-168">Keep the phrase list current with any newly discovered job names.</span><span class="sxs-lookup"><span data-stu-id="2f83c-168">Keep the phrase list current with any newly discovered job names.</span></span> 

1. <span data-ttu-id="2f83c-169">Select **Phrase lists** from left navigation.</span><span class="sxs-lookup"><span data-stu-id="2f83c-169">Select **Phrase lists** from left navigation.</span></span>

2. <span data-ttu-id="2f83c-170">Select the **Jobs** phrase list.</span><span class="sxs-lookup"><span data-stu-id="2f83c-170">Select the **Jobs** phrase list.</span></span>

3. <span data-ttu-id="2f83c-171">Add `Natural Language Processing` as a value then select **Save**.</span><span class="sxs-lookup"><span data-stu-id="2f83c-171">Add `Natural Language Processing` as a value then select **Save**.</span></span> 

## <a name="train-the-luis-app"></a><span data-ttu-id="2f83c-172">Train the LUIS app</span><span class="sxs-lookup"><span data-stu-id="2f83c-172">Train the LUIS app</span></span>

<span data-ttu-id="2f83c-173">LUIS doesn't know about the changes until it is trained.</span><span class="sxs-lookup"><span data-stu-id="2f83c-173">LUIS doesn't know about the changes until it is trained.</span></span> 

[!INCLUDE [LUIS How to Train steps](../../../includes/cognitive-services-luis-tutorial-how-to-train.md)]

## <a name="publish-the-app-to-get-the-endpoint-url"></a><span data-ttu-id="2f83c-174">Publish the app to get the endpoint URL</span><span class="sxs-lookup"><span data-stu-id="2f83c-174">Publish the app to get the endpoint URL</span></span>

<span data-ttu-id="2f83c-175">If you imported this app, you need to select **Sentiment analysis**.</span><span class="sxs-lookup"><span data-stu-id="2f83c-175">If you imported this app, you need to select **Sentiment analysis**.</span></span>

[!INCLUDE [LUIS How to Publish steps](../../../includes/cognitive-services-luis-tutorial-how-to-publish.md)]

## <a name="query-the-endpoint-with-an-utterance"></a><span data-ttu-id="2f83c-176">Query the endpoint with an utterance</span><span class="sxs-lookup"><span data-stu-id="2f83c-176">Query the endpoint with an utterance</span></span>

<span data-ttu-id="2f83c-177">Try an utterance close to the corrected utterance.</span><span class="sxs-lookup"><span data-stu-id="2f83c-177">Try an utterance close to the corrected utterance.</span></span> 

1. [!INCLUDE [LUIS How to get endpoint first step](../../../includes/cognitive-services-luis-tutorial-how-to-get-endpoint.md)]

2. <span data-ttu-id="2f83c-178">Go to the end of the URL in the address and enter `Are there any natural language processing jobs in my department right now?`.</span><span class="sxs-lookup"><span data-stu-id="2f83c-178">Go to the end of the URL in the address and enter `Are there any natural language processing jobs in my department right now?`.</span></span> <span data-ttu-id="2f83c-179">The last querystring parameter is `q`, the utterance **query**.</span><span class="sxs-lookup"><span data-stu-id="2f83c-179">The last querystring parameter is `q`, the utterance **query**.</span></span> 

  ```JSON
  {
    "query": "are there any natural language processing jobs in my department right now?",
    "topScoringIntent": {
      "intent": "GetJobInformation",
      "score": 0.9247605
    },
    "intents": [
      {
        "intent": "GetJobInformation",
        "score": 0.9247605
      },
      {
        "intent": "ApplyForJob",
        "score": 0.129989788
      },
      {
        "intent": "FindForm",
        "score": 0.006438211
      },
      {
        "intent": "EmployeeFeedback",
        "score": 0.00408575451
      },
      {
        "intent": "Utilities.StartOver",
        "score": 0.00194211153
      },
      {
        "intent": "None",
        "score": 0.00166400627
      },
      {
        "intent": "Utilities.Help",
        "score": 0.00118593348
      },
      {
        "intent": "MoveEmployee",
        "score": 0.0007885918
      },
      {
        "intent": "Utilities.Cancel",
        "score": 0.0006373631
      },
      {
        "intent": "Utilities.Stop",
        "score": 0.0005980781
      },
      {
        "intent": "Utilities.Confirm",
        "score": 3.719905E-05
      }
    ],
    "entities": [
      {
        "entity": "right now",
        "type": "builtin.datetimeV2.datetime",
        "startIndex": 64,
        "endIndex": 72,
        "resolution": {
          "values": [
            {
              "timex": "PRESENT_REF",
              "type": "datetime",
              "value": "2018-07-05 15:23:18"
            }
          ]
        }
      },
      {
        "entity": "natural language processing",
        "type": "Job",
        "startIndex": 14,
        "endIndex": 40,
        "score": 0.9869922
      },
      {
        "entity": "natural language processing jobs",
        "type": "builtin.keyPhrase",
        "startIndex": 14,
        "endIndex": 45
      },
      {
        "entity": "department",
        "type": "builtin.keyPhrase",
        "startIndex": 53,
        "endIndex": 62
      }
    ],
    "sentimentAnalysis": {
      "label": "positive",
      "score": 0.8251864
    }
  }
  }
  ```

  <span data-ttu-id="2f83c-180">The correct intent was predicted with a high score and the **Job** entity is detected as `natural language processing`.</span><span class="sxs-lookup"><span data-stu-id="2f83c-180">The correct intent was predicted with a high score and the **Job** entity is detected as `natural language processing`.</span></span> 

## <a name="can-reviewing-be-replaced-by-adding-more-utterances"></a><span data-ttu-id="2f83c-181">Can reviewing be replaced by adding more utterances?</span><span class="sxs-lookup"><span data-stu-id="2f83c-181">Can reviewing be replaced by adding more utterances?</span></span> 
<span data-ttu-id="2f83c-182">You may wonder why not add more example utterances.</span><span class="sxs-lookup"><span data-stu-id="2f83c-182">You may wonder why not add more example utterances.</span></span> <span data-ttu-id="2f83c-183">What is the purpose of reviewing endpoint utterances?</span><span class="sxs-lookup"><span data-stu-id="2f83c-183">What is the purpose of reviewing endpoint utterances?</span></span> <span data-ttu-id="2f83c-184">In a real-world LUIS app, the endpoint utterances are from users with word choice and arrangement you haven't used yet.</span><span class="sxs-lookup"><span data-stu-id="2f83c-184">In a real-world LUIS app, the endpoint utterances are from users with word choice and arrangement you haven't used yet.</span></span> <span data-ttu-id="2f83c-185">If you had used the same word choice and arrangement, the original prediction would have a higher percentage.</span><span class="sxs-lookup"><span data-stu-id="2f83c-185">If you had used the same word choice and arrangement, the original prediction would have a higher percentage.</span></span> 

## <a name="why-is-the-top-intent-on-the-utterance-list"></a><span data-ttu-id="2f83c-186">Why is the top intent on the utterance list?</span><span class="sxs-lookup"><span data-stu-id="2f83c-186">Why is the top intent on the utterance list?</span></span> 
<span data-ttu-id="2f83c-187">Some of the endpoint utterances will have a high percentage in the review list.</span><span class="sxs-lookup"><span data-stu-id="2f83c-187">Some of the endpoint utterances will have a high percentage in the review list.</span></span> <span data-ttu-id="2f83c-188">You still need to review and verify those utterances.</span><span class="sxs-lookup"><span data-stu-id="2f83c-188">You still need to review and verify those utterances.</span></span> <span data-ttu-id="2f83c-189">They are on the list because the next highest intent had a score too close to the top intent score.</span><span class="sxs-lookup"><span data-stu-id="2f83c-189">They are on the list because the next highest intent had a score too close to the top intent score.</span></span> 

## <a name="what-has-this-tutorial-accomplished"></a><span data-ttu-id="2f83c-190">What has this tutorial accomplished?</span><span class="sxs-lookup"><span data-stu-id="2f83c-190">What has this tutorial accomplished?</span></span>
<span data-ttu-id="2f83c-191">This app prediction accuracy has increased by reviewing utterances from the endpoint.</span><span class="sxs-lookup"><span data-stu-id="2f83c-191">This app prediction accuracy has increased by reviewing utterances from the endpoint.</span></span> 

## <a name="clean-up-resources"></a><span data-ttu-id="2f83c-192">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="2f83c-192">Clean up resources</span></span>

[!INCLUDE [LUIS How to clean up resources](../../../includes/cognitive-services-luis-tutorial-how-to-clean-up-resources.md)]

## <a name="next-steps"></a><span data-ttu-id="2f83c-193">Next steps</span><span class="sxs-lookup"><span data-stu-id="2f83c-193">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2f83c-194">Learn how to use patterns</span><span class="sxs-lookup"><span data-stu-id="2f83c-194">Learn how to use patterns</span></span>](luis-tutorial-pattern.md)
