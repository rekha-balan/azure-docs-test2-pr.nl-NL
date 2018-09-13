---
title: Create a simple app with two intents - Azure | Microsoft Docs
description: Learn how to create a simple LUIS app using two intents and no entities to identify user utterances in this quickstart.
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: tutorial
ms.date: 08/02/2018
ms.author: diberry
ms.openlocfilehash: 3f23ade2b0256c72c344e2a619227a79e3c79a47
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857929"
---
# <a name="tutorial-1-build-app-with-custom-domain"></a><span data-ttu-id="a1d6b-103">Tutorial: 1.</span><span class="sxs-lookup"><span data-stu-id="a1d6b-103">Tutorial: 1.</span></span> <span data-ttu-id="a1d6b-104">Build app with custom domain</span><span class="sxs-lookup"><span data-stu-id="a1d6b-104">Build app with custom domain</span></span>
<span data-ttu-id="a1d6b-105">In this tutorial, create an app that demonstrates how to use **intents** to determine the user's _intention_ based on the utterance (text) they submit to the app.</span><span class="sxs-lookup"><span data-stu-id="a1d6b-105">In this tutorial, create an app that demonstrates how to use **intents** to determine the user's _intention_ based on the utterance (text) they submit to the app.</span></span> <span data-ttu-id="a1d6b-106">When you're finished, you have a LUIS endpoint running in the cloud.</span><span class="sxs-lookup"><span data-stu-id="a1d6b-106">When you're finished, you have a LUIS endpoint running in the cloud.</span></span>

<span data-ttu-id="a1d6b-107">This app is the simplest type of LUIS app because it doesn't extract data from the utterances.</span><span class="sxs-lookup"><span data-stu-id="a1d6b-107">This app is the simplest type of LUIS app because it doesn't extract data from the utterances.</span></span> <span data-ttu-id="a1d6b-108">It only determines the user's intention of the utterance.</span><span class="sxs-lookup"><span data-stu-id="a1d6b-108">It only determines the user's intention of the utterance.</span></span>

<!-- green checkmark -->
> [!div class="checklist"]
> * <span data-ttu-id="a1d6b-109">Create a new app for a Human Resources (HR) domain</span><span class="sxs-lookup"><span data-stu-id="a1d6b-109">Create a new app for a Human Resources (HR) domain</span></span> 
> * <span data-ttu-id="a1d6b-110">Add GetJobInformation intent</span><span class="sxs-lookup"><span data-stu-id="a1d6b-110">Add GetJobInformation intent</span></span>
> * <span data-ttu-id="a1d6b-111">Add example utterances to GetJobInformation intent</span><span class="sxs-lookup"><span data-stu-id="a1d6b-111">Add example utterances to GetJobInformation intent</span></span> 
> * <span data-ttu-id="a1d6b-112">Train, and publish app</span><span class="sxs-lookup"><span data-stu-id="a1d6b-112">Train, and publish app</span></span>
> * <span data-ttu-id="a1d6b-113">Query endpoint of app to see LUIS JSON response</span><span class="sxs-lookup"><span data-stu-id="a1d6b-113">Query endpoint of app to see LUIS JSON response</span></span>
> * <span data-ttu-id="a1d6b-114">Add ApplyForJob intent</span><span class="sxs-lookup"><span data-stu-id="a1d6b-114">Add ApplyForJob intent</span></span>
> * <span data-ttu-id="a1d6b-115">Add example utterances to ApplyForJob intent</span><span class="sxs-lookup"><span data-stu-id="a1d6b-115">Add example utterances to ApplyForJob intent</span></span> 
> * <span data-ttu-id="a1d6b-116">Train, publish, and query endpoint again</span><span class="sxs-lookup"><span data-stu-id="a1d6b-116">Train, publish, and query endpoint again</span></span> 

[!INCLUDE [LUIS Free account](../../../includes/cognitive-services-luis-free-key-short.md)]

## <a name="purpose-of-the-app"></a><span data-ttu-id="a1d6b-117">Purpose of the app</span><span class="sxs-lookup"><span data-stu-id="a1d6b-117">Purpose of the app</span></span>
<span data-ttu-id="a1d6b-118">This app has a few intents.</span><span class="sxs-lookup"><span data-stu-id="a1d6b-118">This app has a few intents.</span></span> <span data-ttu-id="a1d6b-119">The first intent, **`GetJobInformation`**, identifies when a user wants information about jobs available inside a company.</span><span class="sxs-lookup"><span data-stu-id="a1d6b-119">The first intent, **`GetJobInformation`**, identifies when a user wants information about jobs available inside a company.</span></span> <span data-ttu-id="a1d6b-120">The second intent, **`None`**, identifies every other type of utterance.</span><span class="sxs-lookup"><span data-stu-id="a1d6b-120">The second intent, **`None`**, identifies every other type of utterance.</span></span> <span data-ttu-id="a1d6b-121">Later in the quickstart, a third intent, `ApplyForJob`, is added.</span><span class="sxs-lookup"><span data-stu-id="a1d6b-121">Later in the quickstart, a third intent, `ApplyForJob`, is added.</span></span> 

## <a name="create-a-new-app"></a><span data-ttu-id="a1d6b-122">Create a new app</span><span class="sxs-lookup"><span data-stu-id="a1d6b-122">Create a new app</span></span>
1. <span data-ttu-id="a1d6b-123">Log in to the [LUIS](luis-reference-regions.md#luis-website) website.</span><span class="sxs-lookup"><span data-stu-id="a1d6b-123">Log in to the [LUIS](luis-reference-regions.md#luis-website) website.</span></span> <span data-ttu-id="a1d6b-124">Make sure to log in to the [region](luis-reference-regions.md#publishing-regions) where you need the LUIS endpoints published.</span><span class="sxs-lookup"><span data-stu-id="a1d6b-124">Make sure to log in to the [region](luis-reference-regions.md#publishing-regions) where you need the LUIS endpoints published.</span></span>

2. <span data-ttu-id="a1d6b-125">On the [LUIS](luis-reference-regions.md#luis-website) website, select **Create new app**.</span><span class="sxs-lookup"><span data-stu-id="a1d6b-125">On the [LUIS](luis-reference-regions.md#luis-website) website, select **Create new app**.</span></span>  

    <span data-ttu-id="a1d6b-126">[![](media/luis-quickstart-intents-only/app-list.png "Screenshot of My Apps page")](media/luis-quickstart-intents-only/app-list.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="a1d6b-126">[![](media/luis-quickstart-intents-only/app-list.png "Screenshot of My Apps page")](media/luis-quickstart-intents-only/app-list.png#lightbox)</span></span>

3. <span data-ttu-id="a1d6b-127">In the pop-up dialog, enter the name `HumanResources`.</span><span class="sxs-lookup"><span data-stu-id="a1d6b-127">In the pop-up dialog, enter the name `HumanResources`.</span></span> <span data-ttu-id="a1d6b-128">This app covers questions about your company's Human Resources department.</span><span class="sxs-lookup"><span data-stu-id="a1d6b-128">This app covers questions about your company's Human Resources department.</span></span> <span data-ttu-id="a1d6b-129">That type of department handles issues related to employment such as positions in the company that need to be filled.</span><span class="sxs-lookup"><span data-stu-id="a1d6b-129">That type of department handles issues related to employment such as positions in the company that need to be filled.</span></span>

    ![LUIS new app](./media/luis-quickstart-intents-only/create-app.png)

4. <span data-ttu-id="a1d6b-131">When that process finishes, the app shows the **Intents** page with the **None** Intent.</span><span class="sxs-lookup"><span data-stu-id="a1d6b-131">When that process finishes, the app shows the **Intents** page with the **None** Intent.</span></span> 

## <a name="create-getjobinformation-intention"></a><span data-ttu-id="a1d6b-132">Create GetJobInformation intention</span><span class="sxs-lookup"><span data-stu-id="a1d6b-132">Create GetJobInformation intention</span></span>
1. <span data-ttu-id="a1d6b-133">Select **Create new intent**.</span><span class="sxs-lookup"><span data-stu-id="a1d6b-133">Select **Create new intent**.</span></span> <span data-ttu-id="a1d6b-134">Enter the new intent name `GetJobInformation`.</span><span class="sxs-lookup"><span data-stu-id="a1d6b-134">Enter the new intent name `GetJobInformation`.</span></span> <span data-ttu-id="a1d6b-135">This intent is predicted any time a user wants information about open jobs in your company.</span><span class="sxs-lookup"><span data-stu-id="a1d6b-135">This intent is predicted any time a user wants information about open jobs in your company.</span></span>

    <span data-ttu-id="a1d6b-136">![](media/luis-quickstart-intents-only/create-intent.png "Screenshot of New intent dialog")</span><span class="sxs-lookup"><span data-stu-id="a1d6b-136">![](media/luis-quickstart-intents-only/create-intent.png "Screenshot of New intent dialog")</span></span>

    <span data-ttu-id="a1d6b-137">By creating an intent, you are creating a category of information that you want to identify.</span><span class="sxs-lookup"><span data-stu-id="a1d6b-137">By creating an intent, you are creating a category of information that you want to identify.</span></span> <span data-ttu-id="a1d6b-138">Giving the category a name allows any other application that uses the LUIS query results to use that category name to find an appropriate answer.</span><span class="sxs-lookup"><span data-stu-id="a1d6b-138">Giving the category a name allows any other application that uses the LUIS query results to use that category name to find an appropriate answer.</span></span> <span data-ttu-id="a1d6b-139">LUIS doesn't answer these questions, only identify what type of information is being asked for in natural language.</span><span class="sxs-lookup"><span data-stu-id="a1d6b-139">LUIS doesn't answer these questions, only identify what type of information is being asked for in natural language.</span></span> 

2. <span data-ttu-id="a1d6b-140">Add seven utterances to this intent that you expect a user to ask for, such as:</span><span class="sxs-lookup"><span data-stu-id="a1d6b-140">Add seven utterances to this intent that you expect a user to ask for, such as:</span></span>

    | <span data-ttu-id="a1d6b-141">Example utterances</span><span class="sxs-lookup"><span data-stu-id="a1d6b-141">Example utterances</span></span>|
    |--|
    |<span data-ttu-id="a1d6b-142">Any new jobs posted today?</span><span class="sxs-lookup"><span data-stu-id="a1d6b-142">Any new jobs posted today?</span></span>|
    |<span data-ttu-id="a1d6b-143">What positions are available for Senior Engineers?</span><span class="sxs-lookup"><span data-stu-id="a1d6b-143">What positions are available for Senior Engineers?</span></span>|
    |<span data-ttu-id="a1d6b-144">Is there any work with databases?</span><span class="sxs-lookup"><span data-stu-id="a1d6b-144">Is there any work with databases?</span></span>|
    |<span data-ttu-id="a1d6b-145">Looking for a new situation with responsibilities in accounting</span><span class="sxs-lookup"><span data-stu-id="a1d6b-145">Looking for a new situation with responsibilities in accounting</span></span>|
    |<span data-ttu-id="a1d6b-146">Where is the job listings</span><span class="sxs-lookup"><span data-stu-id="a1d6b-146">Where is the job listings</span></span>|
    |<span data-ttu-id="a1d6b-147">New jobs?</span><span class="sxs-lookup"><span data-stu-id="a1d6b-147">New jobs?</span></span>|
    |<span data-ttu-id="a1d6b-148">Are there any new positions in the Seattle office?</span><span class="sxs-lookup"><span data-stu-id="a1d6b-148">Are there any new positions in the Seattle office?</span></span>|

    <span data-ttu-id="a1d6b-149">[![](media/luis-quickstart-intents-only/utterance-getstoreinfo.png "Screenshot of entering new utterances for MyStore intent")](media/luis-quickstart-intents-only/utterance-getstoreinfo.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="a1d6b-149">[![](media/luis-quickstart-intents-only/utterance-getstoreinfo.png "Screenshot of entering new utterances for MyStore intent")](media/luis-quickstart-intents-only/utterance-getstoreinfo.png#lightbox)</span></span>

3. <span data-ttu-id="a1d6b-150">The LUIS app currently has no utterances for the **None** intent.</span><span class="sxs-lookup"><span data-stu-id="a1d6b-150">The LUIS app currently has no utterances for the **None** intent.</span></span> <span data-ttu-id="a1d6b-151">It needs utterances that the app doesn't answer.</span><span class="sxs-lookup"><span data-stu-id="a1d6b-151">It needs utterances that the app doesn't answer.</span></span> <span data-ttu-id="a1d6b-152">Do not leave it empty.</span><span class="sxs-lookup"><span data-stu-id="a1d6b-152">Do not leave it empty.</span></span> <span data-ttu-id="a1d6b-153">Select **Intents** from the left panel.</span><span class="sxs-lookup"><span data-stu-id="a1d6b-153">Select **Intents** from the left panel.</span></span> 

4. <span data-ttu-id="a1d6b-154">Select the **None** intent.</span><span class="sxs-lookup"><span data-stu-id="a1d6b-154">Select the **None** intent.</span></span> <span data-ttu-id="a1d6b-155">Add three utterances that your user might enter but are not relevant to your app.</span><span class="sxs-lookup"><span data-stu-id="a1d6b-155">Add three utterances that your user might enter but are not relevant to your app.</span></span> <span data-ttu-id="a1d6b-156">If the app is about your Job postings, some good **None** utterances are:</span><span class="sxs-lookup"><span data-stu-id="a1d6b-156">If the app is about your Job postings, some good **None** utterances are:</span></span>

    | <span data-ttu-id="a1d6b-157">Example utterances</span><span class="sxs-lookup"><span data-stu-id="a1d6b-157">Example utterances</span></span>|
    |--|
    |<span data-ttu-id="a1d6b-158">Barking dogs are annoying</span><span class="sxs-lookup"><span data-stu-id="a1d6b-158">Barking dogs are annoying</span></span>|
    |<span data-ttu-id="a1d6b-159">Order a pizza for me</span><span class="sxs-lookup"><span data-stu-id="a1d6b-159">Order a pizza for me</span></span>|
    |<span data-ttu-id="a1d6b-160">Penguins in the ocean</span><span class="sxs-lookup"><span data-stu-id="a1d6b-160">Penguins in the ocean</span></span>|

    <span data-ttu-id="a1d6b-161">In the LUIS-calling application, such as a chatbot, if LUIS returns the **None** intent for an utterance, your bot can ask if the user wants to end the conversation.</span><span class="sxs-lookup"><span data-stu-id="a1d6b-161">In the LUIS-calling application, such as a chatbot, if LUIS returns the **None** intent for an utterance, your bot can ask if the user wants to end the conversation.</span></span> <span data-ttu-id="a1d6b-162">The chatbot can also give more directions for continuing the conversation if the user doesn't want to end it.</span><span class="sxs-lookup"><span data-stu-id="a1d6b-162">The chatbot can also give more directions for continuing the conversation if the user doesn't want to end it.</span></span> 

## <a name="train-and-publish-the-app"></a><span data-ttu-id="a1d6b-163">Train and publish the app</span><span class="sxs-lookup"><span data-stu-id="a1d6b-163">Train and publish the app</span></span>

[!INCLUDE [LUIS How to Train steps](../../../includes/cognitive-services-luis-tutorial-how-to-train.md)]

## <a name="publish-app-to-endpoint"></a><span data-ttu-id="a1d6b-164">Publish app to endpoint</span><span class="sxs-lookup"><span data-stu-id="a1d6b-164">Publish app to endpoint</span></span>

[!INCLUDE [LUIS How to Publish steps](../../../includes/cognitive-services-luis-tutorial-how-to-publish.md)] 

## <a name="query-endpoint-for-getjobinformation-intent"></a><span data-ttu-id="a1d6b-165">Query endpoint for GetJobInformation intent</span><span class="sxs-lookup"><span data-stu-id="a1d6b-165">Query endpoint for GetJobInformation intent</span></span>

1. [!INCLUDE [LUIS How to get endpoint first step](../../../includes/cognitive-services-luis-tutorial-how-to-get-endpoint.md)]

2. <span data-ttu-id="a1d6b-166">Go to the end of the URL in the address and enter `I'm looking for a job with Natual Language Processing`.</span><span class="sxs-lookup"><span data-stu-id="a1d6b-166">Go to the end of the URL in the address and enter `I'm looking for a job with Natual Language Processing`.</span></span> <span data-ttu-id="a1d6b-167">The last query string parameter is `q`, the utterance **query**.</span><span class="sxs-lookup"><span data-stu-id="a1d6b-167">The last query string parameter is `q`, the utterance **query**.</span></span> <span data-ttu-id="a1d6b-168">This utterance is not the same as any of the example utterances in step 4 so it is a good test and should return the `GetJobInformation` intent as the top scoring intent.</span><span class="sxs-lookup"><span data-stu-id="a1d6b-168">This utterance is not the same as any of the example utterances in step 4 so it is a good test and should return the `GetJobInformation` intent as the top scoring intent.</span></span> 

    ```
    {
      "query": "I'm looking for a job with Natual Language Processing",
      "topScoringIntent": {
        "intent": "GetJobInformation",
        "score": 0.8965092
      },
      "intents": [
        {
          "intent": "GetJobInformation",
          "score": 0.8965092
        },
        {
          "intent": "None",
          "score": 0.147104025
        }
      ],
      "entities": []
    }
    ```

## <a name="create-applyforjob-intention"></a><span data-ttu-id="a1d6b-169">Create ApplyForJob intention</span><span class="sxs-lookup"><span data-stu-id="a1d6b-169">Create ApplyForJob intention</span></span>
<span data-ttu-id="a1d6b-170">Return to the browser tab for the LUIS website and create a new intention to apply for a job.</span><span class="sxs-lookup"><span data-stu-id="a1d6b-170">Return to the browser tab for the LUIS website and create a new intention to apply for a job.</span></span>

1. <span data-ttu-id="a1d6b-171">Select **Build** from the top, right menu to return to app building.</span><span class="sxs-lookup"><span data-stu-id="a1d6b-171">Select **Build** from the top, right menu to return to app building.</span></span>

2. <span data-ttu-id="a1d6b-172">Select **Intents** from the left menu.</span><span class="sxs-lookup"><span data-stu-id="a1d6b-172">Select **Intents** from the left menu.</span></span>

3. <span data-ttu-id="a1d6b-173">Select **Create new intent** and enter the name `ApplyForJob`.</span><span class="sxs-lookup"><span data-stu-id="a1d6b-173">Select **Create new intent** and enter the name `ApplyForJob`.</span></span> 

    ![LUIS dialog to create new intent](./media/luis-quickstart-intents-only/create-applyforjob-intent.png)

4. <span data-ttu-id="a1d6b-175">Add several utterances to this intent that you expect a user to ask for, such as:</span><span class="sxs-lookup"><span data-stu-id="a1d6b-175">Add several utterances to this intent that you expect a user to ask for, such as:</span></span>

    | <span data-ttu-id="a1d6b-176">Example utterances</span><span class="sxs-lookup"><span data-stu-id="a1d6b-176">Example utterances</span></span>|
    |--|
    |<span data-ttu-id="a1d6b-177">I want to apply for the new accounting job</span><span class="sxs-lookup"><span data-stu-id="a1d6b-177">I want to apply for the new accounting job</span></span>|
    |<span data-ttu-id="a1d6b-178">Fill out application for Job 123456</span><span class="sxs-lookup"><span data-stu-id="a1d6b-178">Fill out application for Job 123456</span></span>|
    |<span data-ttu-id="a1d6b-179">Submit resume for engineering position</span><span class="sxs-lookup"><span data-stu-id="a1d6b-179">Submit resume for engineering position</span></span>|
    |<span data-ttu-id="a1d6b-180">Here is my c.v.</span><span class="sxs-lookup"><span data-stu-id="a1d6b-180">Here is my c.v.</span></span> <span data-ttu-id="a1d6b-181">for position 654234</span><span class="sxs-lookup"><span data-stu-id="a1d6b-181">for position 654234</span></span>|
    |<span data-ttu-id="a1d6b-182">Job 567890 and my paperwork</span><span class="sxs-lookup"><span data-stu-id="a1d6b-182">Job 567890 and my paperwork</span></span>|

    <span data-ttu-id="a1d6b-183">[![](media/luis-quickstart-intents-only/utterance-applyforjob.png "Screenshot of entering new utterances for ApplyForJob intent")](media/luis-quickstart-intents-only/utterance-applyforjob.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="a1d6b-183">[![](media/luis-quickstart-intents-only/utterance-applyforjob.png "Screenshot of entering new utterances for ApplyForJob intent")](media/luis-quickstart-intents-only/utterance-applyforjob.png#lightbox)</span></span>

    <span data-ttu-id="a1d6b-184">The labeled intent is outlined in red because LUIS is currently uncertain the intent is correct.</span><span class="sxs-lookup"><span data-stu-id="a1d6b-184">The labeled intent is outlined in red because LUIS is currently uncertain the intent is correct.</span></span> <span data-ttu-id="a1d6b-185">Training the app tells LUIS the utterances are on the correct intent.</span><span class="sxs-lookup"><span data-stu-id="a1d6b-185">Training the app tells LUIS the utterances are on the correct intent.</span></span> 

    <span data-ttu-id="a1d6b-186">[Train and publish](#train-and-publish-the-app) again.</span><span class="sxs-lookup"><span data-stu-id="a1d6b-186">[Train and publish](#train-and-publish-the-app) again.</span></span> 

## <a name="query-endpoint-for-applyforjob-intent"></a><span data-ttu-id="a1d6b-187">Query endpoint for ApplyForJob intent</span><span class="sxs-lookup"><span data-stu-id="a1d6b-187">Query endpoint for ApplyForJob intent</span></span>

1. [!INCLUDE [LUIS How to get endpoint first step](../../../includes/cognitive-services-luis-tutorial-how-to-get-endpoint.md)]

2. <span data-ttu-id="a1d6b-188">In the new browser window, enter `Can I submit my resume for job 235986` at the end of the URL.</span><span class="sxs-lookup"><span data-stu-id="a1d6b-188">In the new browser window, enter `Can I submit my resume for job 235986` at the end of the URL.</span></span> 

    ```
    {
      "query": "Can I submit my resume for job 235986",
      "topScoringIntent": {
        "intent": "ApplyForJob",
        "score": 0.9166808
      },
      "intents": [
        {
          "intent": "ApplyForJob",
          "score": 0.9166808
        },
        {
          "intent": "GetJobInformation",
          "score": 0.07162977
        },
        {
          "intent": "None",
          "score": 0.0262826588
        }
      ],
      "entities": []
    }
    ```

## <a name="what-has-this-luis-app-accomplished"></a><span data-ttu-id="a1d6b-189">What has this LUIS app accomplished?</span><span class="sxs-lookup"><span data-stu-id="a1d6b-189">What has this LUIS app accomplished?</span></span>
<span data-ttu-id="a1d6b-190">This app, with just a few intents, identified a natural language query that is of the same intention but worded differently.</span><span class="sxs-lookup"><span data-stu-id="a1d6b-190">This app, with just a few intents, identified a natural language query that is of the same intention but worded differently.</span></span> 

<span data-ttu-id="a1d6b-191">The JSON result identifies the top scoring intent.</span><span class="sxs-lookup"><span data-stu-id="a1d6b-191">The JSON result identifies the top scoring intent.</span></span> <span data-ttu-id="a1d6b-192">All scores are between 1 and 0, with the better score being close to 1.</span><span class="sxs-lookup"><span data-stu-id="a1d6b-192">All scores are between 1 and 0, with the better score being close to 1.</span></span> <span data-ttu-id="a1d6b-193">The `GetJobInformation` and `None` intents' score are much closer to zero.</span><span class="sxs-lookup"><span data-stu-id="a1d6b-193">The `GetJobInformation` and `None` intents' score are much closer to zero.</span></span> 

## <a name="where-is-this-luis-data-used"></a><span data-ttu-id="a1d6b-194">Where is this LUIS data used?</span><span class="sxs-lookup"><span data-stu-id="a1d6b-194">Where is this LUIS data used?</span></span> 
<span data-ttu-id="a1d6b-195">LUIS is done with this request.</span><span class="sxs-lookup"><span data-stu-id="a1d6b-195">LUIS is done with this request.</span></span> <span data-ttu-id="a1d6b-196">The calling application, such as a chatbot, can take the topScoringIntent result and either find information (not stored in LUIS) to answer the question or end the conversation.</span><span class="sxs-lookup"><span data-stu-id="a1d6b-196">The calling application, such as a chatbot, can take the topScoringIntent result and either find information (not stored in LUIS) to answer the question or end the conversation.</span></span> <span data-ttu-id="a1d6b-197">These are programmatic options for the bot or calling application.</span><span class="sxs-lookup"><span data-stu-id="a1d6b-197">These are programmatic options for the bot or calling application.</span></span> <span data-ttu-id="a1d6b-198">LUIS doesn't do that work.</span><span class="sxs-lookup"><span data-stu-id="a1d6b-198">LUIS doesn't do that work.</span></span> <span data-ttu-id="a1d6b-199">LUIS only determines what the user's intention is.</span><span class="sxs-lookup"><span data-stu-id="a1d6b-199">LUIS only determines what the user's intention is.</span></span> 

## <a name="clean-up-resources"></a><span data-ttu-id="a1d6b-200">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="a1d6b-200">Clean up resources</span></span>

[!INCLUDE [LUIS How to clean up resources](../../../includes/cognitive-services-luis-tutorial-how-to-clean-up-resources.md)]

## <a name="next-steps"></a><span data-ttu-id="a1d6b-201">Next steps</span><span class="sxs-lookup"><span data-stu-id="a1d6b-201">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a1d6b-202">Add prebuilt intents and entities to this app</span><span class="sxs-lookup"><span data-stu-id="a1d6b-202">Add prebuilt intents and entities to this app</span></span>](luis-tutorial-prebuilt-intents-entities.md)
