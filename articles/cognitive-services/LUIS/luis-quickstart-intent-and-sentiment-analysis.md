---
title: Tutorial to create a LUIS app that returns sentiment analysis - Azure | Microsoft Docs
description: In this tutorial, learn how to add sentiment analysis to your LUIS app to analyze utterances for positive, negative, and neutral feelings.
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: luis
ms.topic: tutorial
ms.date: 08/02/2018
ms.author: diberry
ms.openlocfilehash: a89755bcc0ed5ef8bee4ed00b99c73993a57bcb9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868522"
---
# <a name="tutorial-9--add-sentiment-analysis"></a><span data-ttu-id="04eec-103">Tutorial: 9.</span><span class="sxs-lookup"><span data-stu-id="04eec-103">Tutorial: 9.</span></span>  <span data-ttu-id="04eec-104">Add sentiment analysis</span><span class="sxs-lookup"><span data-stu-id="04eec-104">Add sentiment analysis</span></span>
<span data-ttu-id="04eec-105">In this tutorial, create an app that demonstrates how to extract positive, negative, and neutral sentiment from utterances.</span><span class="sxs-lookup"><span data-stu-id="04eec-105">In this tutorial, create an app that demonstrates how to extract positive, negative, and neutral sentiment from utterances.</span></span>

<!-- green checkmark -->
> [!div class="checklist"]
> * <span data-ttu-id="04eec-106">Understand sentiment analysis</span><span class="sxs-lookup"><span data-stu-id="04eec-106">Understand sentiment analysis</span></span>
> * <span data-ttu-id="04eec-107">Use LUIS app in Human Resources (HR) domain</span><span class="sxs-lookup"><span data-stu-id="04eec-107">Use LUIS app in Human Resources (HR) domain</span></span> 
> * <span data-ttu-id="04eec-108">Add sentiment analysis</span><span class="sxs-lookup"><span data-stu-id="04eec-108">Add sentiment analysis</span></span>
> * <span data-ttu-id="04eec-109">Train, and publish app</span><span class="sxs-lookup"><span data-stu-id="04eec-109">Train, and publish app</span></span>
> * <span data-ttu-id="04eec-110">Query endpoint of app to see LUIS JSON response</span><span class="sxs-lookup"><span data-stu-id="04eec-110">Query endpoint of app to see LUIS JSON response</span></span> 

[!INCLUDE [LUIS Free account](../../../includes/cognitive-services-luis-free-key-short.md)]

## <a name="before-you-begin"></a><span data-ttu-id="04eec-111">Before you begin</span><span class="sxs-lookup"><span data-stu-id="04eec-111">Before you begin</span></span>
<span data-ttu-id="04eec-112">If you don't have the Human Resources app from the [prebuilt keyPhrase entity](luis-quickstart-intent-and-key-phrase.md) tutorial, [import](luis-how-to-start-new-app.md#import-new-app) the JSON into a new app in the [LUIS](luis-reference-regions.md#luis-website) website.</span><span class="sxs-lookup"><span data-stu-id="04eec-112">If you don't have the Human Resources app from the [prebuilt keyPhrase entity](luis-quickstart-intent-and-key-phrase.md) tutorial, [import](luis-how-to-start-new-app.md#import-new-app) the JSON into a new app in the [LUIS](luis-reference-regions.md#luis-website) website.</span></span> <span data-ttu-id="04eec-113">The app to import is found in the [LUIS-Samples](https://github.com/Microsoft/LUIS-Samples/blob/master/documentation-samples/quickstarts/custom-domain-keyphrase-HumanResources.json) Github repository.</span><span class="sxs-lookup"><span data-stu-id="04eec-113">The app to import is found in the [LUIS-Samples](https://github.com/Microsoft/LUIS-Samples/blob/master/documentation-samples/quickstarts/custom-domain-keyphrase-HumanResources.json) Github repository.</span></span>

<span data-ttu-id="04eec-114">If you want to keep the original Human Resources app, clone the version on the [Settings](luis-how-to-manage-versions.md#clone-a-version) page, and name it `sentiment`.</span><span class="sxs-lookup"><span data-stu-id="04eec-114">If you want to keep the original Human Resources app, clone the version on the [Settings](luis-how-to-manage-versions.md#clone-a-version) page, and name it `sentiment`.</span></span> <span data-ttu-id="04eec-115">Cloning is a great way to play with various LUIS features without affecting the original version.</span><span class="sxs-lookup"><span data-stu-id="04eec-115">Cloning is a great way to play with various LUIS features without affecting the original version.</span></span> 

## <a name="sentiment-analysis"></a><span data-ttu-id="04eec-116">Sentiment analysis</span><span class="sxs-lookup"><span data-stu-id="04eec-116">Sentiment analysis</span></span>
<span data-ttu-id="04eec-117">Sentiment analysis is the ability to determine if a user's utterance is positive, negative, or neutral.</span><span class="sxs-lookup"><span data-stu-id="04eec-117">Sentiment analysis is the ability to determine if a user's utterance is positive, negative, or neutral.</span></span> 

<span data-ttu-id="04eec-118">The following utterances show examples of sentiment:</span><span class="sxs-lookup"><span data-stu-id="04eec-118">The following utterances show examples of sentiment:</span></span>

|<span data-ttu-id="04eec-119">Sentiment</span><span class="sxs-lookup"><span data-stu-id="04eec-119">Sentiment</span></span>|<span data-ttu-id="04eec-120">Score</span><span class="sxs-lookup"><span data-stu-id="04eec-120">Score</span></span>|<span data-ttu-id="04eec-121">Utterance</span><span class="sxs-lookup"><span data-stu-id="04eec-121">Utterance</span></span>|
|:--|:--|:--|
|<span data-ttu-id="04eec-122">positive</span><span class="sxs-lookup"><span data-stu-id="04eec-122">positive</span></span>|<span data-ttu-id="04eec-123">0.91</span><span class="sxs-lookup"><span data-stu-id="04eec-123">0.91</span></span> |<span data-ttu-id="04eec-124">John W. Smith did a great job on the presentation in Paris.</span><span class="sxs-lookup"><span data-stu-id="04eec-124">John W. Smith did a great job on the presentation in Paris.</span></span>|
|<span data-ttu-id="04eec-125">positive</span><span class="sxs-lookup"><span data-stu-id="04eec-125">positive</span></span>|<span data-ttu-id="04eec-126">0.84</span><span class="sxs-lookup"><span data-stu-id="04eec-126">0.84</span></span> |<span data-ttu-id="04eec-127">jill-jones@mycompany.com did fabulous work on the Parker sales pitch.</span><span class="sxs-lookup"><span data-stu-id="04eec-127">jill-jones@mycompany.com did fabulous work on the Parker sales pitch.</span></span>|

<span data-ttu-id="04eec-128">Sentiment analysis is an app setting that applies to every utterance.</span><span class="sxs-lookup"><span data-stu-id="04eec-128">Sentiment analysis is an app setting that applies to every utterance.</span></span> <span data-ttu-id="04eec-129">You do not have to find the words indicating sentiment in the utterance and label them because sentiment analysis applies to the entire utterance.</span><span class="sxs-lookup"><span data-stu-id="04eec-129">You do not have to find the words indicating sentiment in the utterance and label them because sentiment analysis applies to the entire utterance.</span></span> 

## <a name="add-employeefeedback-intent"></a><span data-ttu-id="04eec-130">Add EmployeeFeedback intent</span><span class="sxs-lookup"><span data-stu-id="04eec-130">Add EmployeeFeedback intent</span></span> 
<span data-ttu-id="04eec-131">Add a new intent to capture employee feedback from members of the company.</span><span class="sxs-lookup"><span data-stu-id="04eec-131">Add a new intent to capture employee feedback from members of the company.</span></span> 

1. <span data-ttu-id="04eec-132">Make sure your Human Resources app is in the **Build** section of LUIS.</span><span class="sxs-lookup"><span data-stu-id="04eec-132">Make sure your Human Resources app is in the **Build** section of LUIS.</span></span> <span data-ttu-id="04eec-133">You can change to this section by selecting **Build** on the top, right menu bar.</span><span class="sxs-lookup"><span data-stu-id="04eec-133">You can change to this section by selecting **Build** on the top, right menu bar.</span></span> 

    <span data-ttu-id="04eec-134">[ ![Screenshot of LUIS app with Build hightlighted in top, right navigation bar](./media/luis-quickstart-intent-and-sentiment-analysis/hr-first-image.png)](./media/luis-quickstart-intent-and-sentiment-analysis/hr-first-image.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="04eec-134">[ ![Screenshot of LUIS app with Build hightlighted in top, right navigation bar](./media/luis-quickstart-intent-and-sentiment-analysis/hr-first-image.png)](./media/luis-quickstart-intent-and-sentiment-analysis/hr-first-image.png#lightbox)</span></span>

2. <span data-ttu-id="04eec-135">Select **Create new intent**.</span><span class="sxs-lookup"><span data-stu-id="04eec-135">Select **Create new intent**.</span></span>

    <span data-ttu-id="04eec-136">[ ![Screenshot of LUIS app with Build hightlighted in top, right navigation bar](./media/luis-quickstart-intent-and-sentiment-analysis/hr-create-new-intent.png)](./media/luis-quickstart-intent-and-sentiment-analysis/hr-create-new-intent.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="04eec-136">[ ![Screenshot of LUIS app with Build hightlighted in top, right navigation bar](./media/luis-quickstart-intent-and-sentiment-analysis/hr-create-new-intent.png)](./media/luis-quickstart-intent-and-sentiment-analysis/hr-create-new-intent.png#lightbox)</span></span>

3. <span data-ttu-id="04eec-137">Name the new intent  name `EmployeeFeedback`.</span><span class="sxs-lookup"><span data-stu-id="04eec-137">Name the new intent  name `EmployeeFeedback`.</span></span>

    ![Create new intent dialog box with EmployeeFeedback as name](./media/luis-quickstart-intent-and-sentiment-analysis/hr-create-new-intent-ddl.png)

4. <span data-ttu-id="04eec-139">Add several utterances that indicate an employee doing something well or an area that needs improvement:</span><span class="sxs-lookup"><span data-stu-id="04eec-139">Add several utterances that indicate an employee doing something well or an area that needs improvement:</span></span>

    <span data-ttu-id="04eec-140">Remember in this Human Resources app, employees are defined in the list entity, `Employee`, by the name, email, phone extension number, mobile phone number, and their U.S. federal social security number.</span><span class="sxs-lookup"><span data-stu-id="04eec-140">Remember in this Human Resources app, employees are defined in the list entity, `Employee`, by the name, email, phone extension number, mobile phone number, and their U.S. federal social security number.</span></span> 

    |<span data-ttu-id="04eec-141">Utterances</span><span class="sxs-lookup"><span data-stu-id="04eec-141">Utterances</span></span>|
    |--|
    |<span data-ttu-id="04eec-142">425-555-1212 did a nice job of welcoming back a co-worker from maternity leave</span><span class="sxs-lookup"><span data-stu-id="04eec-142">425-555-1212 did a nice job of welcoming back a co-worker from maternity leave</span></span>|
    |<span data-ttu-id="04eec-143">234-56-7891 did a great job of comforting a co-worker in their time of grief.</span><span class="sxs-lookup"><span data-stu-id="04eec-143">234-56-7891 did a great job of comforting a co-worker in their time of grief.</span></span>|
    |<span data-ttu-id="04eec-144">jill-jones@mycompany.com didn't have all the required invoices for the paperwork.</span><span class="sxs-lookup"><span data-stu-id="04eec-144">jill-jones@mycompany.com didn't have all the required invoices for the paperwork.</span></span>|
    |<span data-ttu-id="04eec-145">john.w.smith@mycompany.com turned in the required forms a month late with no signatures</span><span class="sxs-lookup"><span data-stu-id="04eec-145">john.w.smith@mycompany.com turned in the required forms a month late with no signatures</span></span>|
    |<span data-ttu-id="04eec-146">x23456 didn't make it to the important marketing off-site meeting.</span><span class="sxs-lookup"><span data-stu-id="04eec-146">x23456 didn't make it to the important marketing off-site meeting.</span></span>|
    |<span data-ttu-id="04eec-147">x12345 missed the meeting for June reviews.</span><span class="sxs-lookup"><span data-stu-id="04eec-147">x12345 missed the meeting for June reviews.</span></span>|
    |<span data-ttu-id="04eec-148">Jill Jones rocked the sales pitch at Harvard</span><span class="sxs-lookup"><span data-stu-id="04eec-148">Jill Jones rocked the sales pitch at Harvard</span></span>|
    |<span data-ttu-id="04eec-149">John W. Smith did a great job on the presentation at Stanford</span><span class="sxs-lookup"><span data-stu-id="04eec-149">John W. Smith did a great job on the presentation at Stanford</span></span>|

    <span data-ttu-id="04eec-150">[ ![Screenshot of LUIS app with example utterances in EmployeeFeedback intent](./media/luis-quickstart-intent-and-sentiment-analysis/hr-utterance-examples.png)](./media/luis-quickstart-intent-and-sentiment-analysis/hr-utterance-examples.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="04eec-150">[ ![Screenshot of LUIS app with example utterances in EmployeeFeedback intent](./media/luis-quickstart-intent-and-sentiment-analysis/hr-utterance-examples.png)](./media/luis-quickstart-intent-and-sentiment-analysis/hr-utterance-examples.png#lightbox)</span></span>

## <a name="train-the-luis-app"></a><span data-ttu-id="04eec-151">Train the LUIS app</span><span class="sxs-lookup"><span data-stu-id="04eec-151">Train the LUIS app</span></span>

[!INCLUDE [LUIS How to Train steps](../../../includes/cognitive-services-luis-tutorial-how-to-train.md)]

## <a name="configure-app-to-include-sentiment-analysis"></a><span data-ttu-id="04eec-152">Configure app to include sentiment analysis</span><span class="sxs-lookup"><span data-stu-id="04eec-152">Configure app to include sentiment analysis</span></span>
<span data-ttu-id="04eec-153">Configure sentiment analysis on the **Publish** page.</span><span class="sxs-lookup"><span data-stu-id="04eec-153">Configure sentiment analysis on the **Publish** page.</span></span> 

1. <span data-ttu-id="04eec-154">Select **Publish** in the top right navigation.</span><span class="sxs-lookup"><span data-stu-id="04eec-154">Select **Publish** in the top right navigation.</span></span>

    ![<span data-ttu-id="04eec-155">Screenshot of Intent page with Publish button expanded</span><span class="sxs-lookup"><span data-stu-id="04eec-155">Screenshot of Intent page with Publish button expanded</span></span> ](./media/luis-quickstart-intent-and-sentiment-analysis/hr-publish-button-in-top-nav-highlighted.png)

2. <span data-ttu-id="04eec-156">Select **Enable Sentiment Analysis**.</span><span class="sxs-lookup"><span data-stu-id="04eec-156">Select **Enable Sentiment Analysis**.</span></span> 

## <a name="publish-app-to-endpoint"></a><span data-ttu-id="04eec-157">Publish app to endpoint</span><span class="sxs-lookup"><span data-stu-id="04eec-157">Publish app to endpoint</span></span>

[!INCLUDE [LUIS How to Publish steps](../../../includes/cognitive-services-luis-tutorial-how-to-publish.md)]

## <a name="query-the-endpoint-with-an-utterance"></a><span data-ttu-id="04eec-158">Query the endpoint with an utterance</span><span class="sxs-lookup"><span data-stu-id="04eec-158">Query the endpoint with an utterance</span></span>

1. [!INCLUDE [LUIS How to get endpoint first step](../../../includes/cognitive-services-luis-tutorial-how-to-get-endpoint.md)]

2. <span data-ttu-id="04eec-159">Go to the end of the URL in the address and enter `Jill Jones work with the media team on the public portal was amazing`.</span><span class="sxs-lookup"><span data-stu-id="04eec-159">Go to the end of the URL in the address and enter `Jill Jones work with the media team on the public portal was amazing`.</span></span> <span data-ttu-id="04eec-160">The last querystring parameter is `q`, the utterance **query**.</span><span class="sxs-lookup"><span data-stu-id="04eec-160">The last querystring parameter is `q`, the utterance **query**.</span></span> <span data-ttu-id="04eec-161">This utterance is not the same as any of the labeled utterances so it is a good test and should return the `EmployeeFeedback` intent with the sentiment analysis extracted.</span><span class="sxs-lookup"><span data-stu-id="04eec-161">This utterance is not the same as any of the labeled utterances so it is a good test and should return the `EmployeeFeedback` intent with the sentiment analysis extracted.</span></span>

```
{
  "query": "Jill Jones work with the media team on the public portal was amazing",
  "topScoringIntent": {
    "intent": "EmployeeFeedback",
    "score": 0.4983256
  },
  "intents": [
    {
      "intent": "EmployeeFeedback",
      "score": 0.4983256
    },
    {
      "intent": "MoveEmployee",
      "score": 0.06617523
    },
    {
      "intent": "GetJobInformation",
      "score": 0.04631853
    },
    {
      "intent": "ApplyForJob",
      "score": 0.0103248553
    },
    {
      "intent": "Utilities.StartOver",
      "score": 0.007531875
    },
    {
      "intent": "FindForm",
      "score": 0.00344597152
    },
    {
      "intent": "Utilities.Help",
      "score": 0.00337914471
    },
    {
      "intent": "Utilities.Cancel",
      "score": 0.0026357458
    },
    {
      "intent": "None",
      "score": 0.00214573368
    },
    {
      "intent": "Utilities.Stop",
      "score": 0.00157622492
    },
    {
      "intent": "Utilities.Confirm",
      "score": 7.379545E-05
    }
  ],
  "entities": [
    {
      "entity": "jill jones",
      "type": "Employee",
      "startIndex": 0,
      "endIndex": 9,
      "resolution": {
        "values": [
          "Employee-45612"
        ]
      }
    },
    {
      "entity": "media team",
      "type": "builtin.keyPhrase",
      "startIndex": 25,
      "endIndex": 34
    },
    {
      "entity": "public portal",
      "type": "builtin.keyPhrase",
      "startIndex": 43,
      "endIndex": 55
    },
    {
      "entity": "jill jones",
      "type": "builtin.keyPhrase",
      "startIndex": 0,
      "endIndex": 9
    }
  ],
  "sentimentAnalysis": {
    "label": "positive",
    "score": 0.8694164
  }
}
```

<span data-ttu-id="04eec-162">The sentimentAnalysis is positive with a score of 0.86.</span><span class="sxs-lookup"><span data-stu-id="04eec-162">The sentimentAnalysis is positive with a score of 0.86.</span></span> 

## <a name="what-has-this-luis-app-accomplished"></a><span data-ttu-id="04eec-163">What has this LUIS app accomplished?</span><span class="sxs-lookup"><span data-stu-id="04eec-163">What has this LUIS app accomplished?</span></span>
<span data-ttu-id="04eec-164">This app, with sentiment analysis enabled, identified a natural language query intention and returned the extracted data including the overall sentiment as a score.</span><span class="sxs-lookup"><span data-stu-id="04eec-164">This app, with sentiment analysis enabled, identified a natural language query intention and returned the extracted data including the overall sentiment as a score.</span></span> 

<span data-ttu-id="04eec-165">Your chatbot now has enough information to determine the next step in the conversation.</span><span class="sxs-lookup"><span data-stu-id="04eec-165">Your chatbot now has enough information to determine the next step in the conversation.</span></span> 

## <a name="where-is-this-luis-data-used"></a><span data-ttu-id="04eec-166">Where is this LUIS data used?</span><span class="sxs-lookup"><span data-stu-id="04eec-166">Where is this LUIS data used?</span></span> 
<span data-ttu-id="04eec-167">LUIS is done with this request.</span><span class="sxs-lookup"><span data-stu-id="04eec-167">LUIS is done with this request.</span></span> <span data-ttu-id="04eec-168">The calling application, such as a chatbot, can take the topScoringIntent result and the sentiment data from the utterance to take the next step.</span><span class="sxs-lookup"><span data-stu-id="04eec-168">The calling application, such as a chatbot, can take the topScoringIntent result and the sentiment data from the utterance to take the next step.</span></span> <span data-ttu-id="04eec-169">LUIS doesn't do that programmatic work for the bot or calling application.</span><span class="sxs-lookup"><span data-stu-id="04eec-169">LUIS doesn't do that programmatic work for the bot or calling application.</span></span> <span data-ttu-id="04eec-170">LUIS only determines what the user's intention is.</span><span class="sxs-lookup"><span data-stu-id="04eec-170">LUIS only determines what the user's intention is.</span></span> 

## <a name="clean-up-resources"></a><span data-ttu-id="04eec-171">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="04eec-171">Clean up resources</span></span>

[!INCLUDE [LUIS How to clean up resources](../../../includes/cognitive-services-luis-tutorial-how-to-clean-up-resources.md)]

## <a name="next-steps"></a><span data-ttu-id="04eec-172">Next steps</span><span class="sxs-lookup"><span data-stu-id="04eec-172">Next steps</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="04eec-173">Review endpoint utterances in the HR app</span><span class="sxs-lookup"><span data-stu-id="04eec-173">Review endpoint utterances in the HR app</span></span>](luis-tutorial-review-endpoint-utterances.md) 

