---
title: Tutorial using patterns to improve LUIS predictions - Azure | Microsoft Docs
titleSuffix: Cognitive Services
description: In this tutorial, use pattern for intents to improve LUIS intent and entity predictions.
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.technology: luis
ms.topic: article
ms.date: 07/30/2018
ms.author: diberry
ms.openlocfilehash: 9c14f2121cd83cec802f4fd4a92661d58eb7efb3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864722"
---
# <a name="tutorial-improve-app-with-patterns"></a><span data-ttu-id="2b67a-103">Tutorial: Improve app with patterns</span><span class="sxs-lookup"><span data-stu-id="2b67a-103">Tutorial: Improve app with patterns</span></span>

<span data-ttu-id="2b67a-104">In this tutorial, use patterns to increase intent and entity prediction.</span><span class="sxs-lookup"><span data-stu-id="2b67a-104">In this tutorial, use patterns to increase intent and entity prediction.</span></span>  

> [!div class="checklist"]
* <span data-ttu-id="2b67a-105">How to identify that a pattern would help your app</span><span class="sxs-lookup"><span data-stu-id="2b67a-105">How to identify that a pattern would help your app</span></span>
* <span data-ttu-id="2b67a-106">How to create a pattern</span><span class="sxs-lookup"><span data-stu-id="2b67a-106">How to create a pattern</span></span>
* <span data-ttu-id="2b67a-107">How to verify pattern prediction improvements</span><span class="sxs-lookup"><span data-stu-id="2b67a-107">How to verify pattern prediction improvements</span></span>

[!INCLUDE [LUIS Free account](../../../includes/cognitive-services-luis-free-key-short.md)]

## <a name="before-you-begin"></a><span data-ttu-id="2b67a-108">Before you begin</span><span class="sxs-lookup"><span data-stu-id="2b67a-108">Before you begin</span></span>

<span data-ttu-id="2b67a-109">If you don't have the Human Resources app from the [batch test](luis-tutorial-batch-testing.md) tutorial, [import](luis-how-to-start-new-app.md#import-new-app) the JSON into a new app in the [LUIS](luis-reference-regions.md#luis-website) website.</span><span class="sxs-lookup"><span data-stu-id="2b67a-109">If you don't have the Human Resources app from the [batch test](luis-tutorial-batch-testing.md) tutorial, [import](luis-how-to-start-new-app.md#import-new-app) the JSON into a new app in the [LUIS](luis-reference-regions.md#luis-website) website.</span></span> <span data-ttu-id="2b67a-110">The app to import is found in the [LUIS-Samples](https://github.com/Microsoft/LUIS-Samples/blob/master/documentation-samples/quickstarts/custom-domain-batchtest-HumanResources.json) GitHub repository.</span><span class="sxs-lookup"><span data-stu-id="2b67a-110">The app to import is found in the [LUIS-Samples](https://github.com/Microsoft/LUIS-Samples/blob/master/documentation-samples/quickstarts/custom-domain-batchtest-HumanResources.json) GitHub repository.</span></span>

<span data-ttu-id="2b67a-111">If you want to keep the original Human Resources app, clone the version on the [Settings](luis-how-to-manage-versions.md#clone-a-version) page, and name it `patterns`.</span><span class="sxs-lookup"><span data-stu-id="2b67a-111">If you want to keep the original Human Resources app, clone the version on the [Settings](luis-how-to-manage-versions.md#clone-a-version) page, and name it `patterns`.</span></span> <span data-ttu-id="2b67a-112">Cloning is a great way to play with various LUIS features without affecting the original version.</span><span class="sxs-lookup"><span data-stu-id="2b67a-112">Cloning is a great way to play with various LUIS features without affecting the original version.</span></span> 

## <a name="patterns-teach-luis-common-utterances-with-fewer-examples"></a><span data-ttu-id="2b67a-113">Patterns teach LUIS common utterances with fewer examples</span><span class="sxs-lookup"><span data-stu-id="2b67a-113">Patterns teach LUIS common utterances with fewer examples</span></span>

<span data-ttu-id="2b67a-114">Because of the nature of the Human Resource domain, there are a few common ways of asking about employee relationships in organizations.</span><span class="sxs-lookup"><span data-stu-id="2b67a-114">Because of the nature of the Human Resource domain, there are a few common ways of asking about employee relationships in organizations.</span></span> <span data-ttu-id="2b67a-115">For example:</span><span class="sxs-lookup"><span data-stu-id="2b67a-115">For example:</span></span>

|<span data-ttu-id="2b67a-116">Utterances</span><span class="sxs-lookup"><span data-stu-id="2b67a-116">Utterances</span></span>|
|--|
|<span data-ttu-id="2b67a-117">Who does Jill Jones report to?</span><span class="sxs-lookup"><span data-stu-id="2b67a-117">Who does Jill Jones report to?</span></span>|
|<span data-ttu-id="2b67a-118">Who reports to Jill Jones?</span><span class="sxs-lookup"><span data-stu-id="2b67a-118">Who reports to Jill Jones?</span></span>|

<span data-ttu-id="2b67a-119">These utterances are too close to determine the contextual uniqueness of each without providing many utterance examples.</span><span class="sxs-lookup"><span data-stu-id="2b67a-119">These utterances are too close to determine the contextual uniqueness of each without providing many utterance examples.</span></span> <span data-ttu-id="2b67a-120">By adding a pattern for an intent, LUIS learns common utterance patterns for an intent without supplying many utterance examples.</span><span class="sxs-lookup"><span data-stu-id="2b67a-120">By adding a pattern for an intent, LUIS learns common utterance patterns for an intent without supplying many utterance examples.</span></span> 

<span data-ttu-id="2b67a-121">Example template utterances for this intent include:</span><span class="sxs-lookup"><span data-stu-id="2b67a-121">Example template utterances for this intent include:</span></span>

|<span data-ttu-id="2b67a-122">Example template utterances</span><span class="sxs-lookup"><span data-stu-id="2b67a-122">Example template utterances</span></span>|
|--|
|<span data-ttu-id="2b67a-123">Who does {Employee} report to?</span><span class="sxs-lookup"><span data-stu-id="2b67a-123">Who does {Employee} report to?</span></span>|
|<span data-ttu-id="2b67a-124">Who reports to {Employee}?</span><span class="sxs-lookup"><span data-stu-id="2b67a-124">Who reports to {Employee}?</span></span>|

<span data-ttu-id="2b67a-125">The pattern is provided by way of a template utterance example, which includes syntax to identify entities and ignorable text.</span><span class="sxs-lookup"><span data-stu-id="2b67a-125">The pattern is provided by way of a template utterance example, which includes syntax to identify entities and ignorable text.</span></span> <span data-ttu-id="2b67a-126">A pattern is a combination of regular expression matching and machine learning.</span><span class="sxs-lookup"><span data-stu-id="2b67a-126">A pattern is a combination of regular expression matching and machine learning.</span></span>  <span data-ttu-id="2b67a-127">The template utterance example, along with the intent utterances, give LUIS a better understanding of what utterances fit the intent.</span><span class="sxs-lookup"><span data-stu-id="2b67a-127">The template utterance example, along with the intent utterances, give LUIS a better understanding of what utterances fit the intent.</span></span>

<span data-ttu-id="2b67a-128">In order for a pattern to be matched to an utterance, the entities within the utterance have to match the entities in the template utterance first.</span><span class="sxs-lookup"><span data-stu-id="2b67a-128">In order for a pattern to be matched to an utterance, the entities within the utterance have to match the entities in the template utterance first.</span></span> <span data-ttu-id="2b67a-129">However, the template doesn't help predict entities, only intents.</span><span class="sxs-lookup"><span data-stu-id="2b67a-129">However, the template doesn't help predict entities, only intents.</span></span> 

<span data-ttu-id="2b67a-130">**While patterns allow you to provide fewer example utterances, if the entities are not detected, the pattern does not match.**</span><span class="sxs-lookup"><span data-stu-id="2b67a-130">**While patterns allow you to provide fewer example utterances, if the entities are not detected, the pattern does not match.**</span></span>

<span data-ttu-id="2b67a-131">Remember that employees were created in the [list entity tutorial](luis-quickstart-intent-and-list-entity.md).</span><span class="sxs-lookup"><span data-stu-id="2b67a-131">Remember that employees were created in the [list entity tutorial](luis-quickstart-intent-and-list-entity.md).</span></span>

## <a name="create-new-intents-and-their-utterances"></a><span data-ttu-id="2b67a-132">Create new intents and their utterances</span><span class="sxs-lookup"><span data-stu-id="2b67a-132">Create new intents and their utterances</span></span>

<span data-ttu-id="2b67a-133">Add two new intents: `OrgChart-Manager` and `OrgChart-Reports`.</span><span class="sxs-lookup"><span data-stu-id="2b67a-133">Add two new intents: `OrgChart-Manager` and `OrgChart-Reports`.</span></span> <span data-ttu-id="2b67a-134">Once LUIS returns a prediction to the client app, the intent name can be used as a function name in the client app and that the Employee entity could be used as a parameter to that function.</span><span class="sxs-lookup"><span data-stu-id="2b67a-134">Once LUIS returns a prediction to the client app, the intent name can be used as a function name in the client app and that the Employee entity could be used as a parameter to that function.</span></span>

```Javascript
OrgChart-Manager(employee){
    ///
}
```

1. <span data-ttu-id="2b67a-135">Make sure your Human Resources app is in the **Build** section of LUIS.</span><span class="sxs-lookup"><span data-stu-id="2b67a-135">Make sure your Human Resources app is in the **Build** section of LUIS.</span></span> <span data-ttu-id="2b67a-136">You can change to this section by selecting **Build** on the top, right menu bar.</span><span class="sxs-lookup"><span data-stu-id="2b67a-136">You can change to this section by selecting **Build** on the top, right menu bar.</span></span> 

2. <span data-ttu-id="2b67a-137">On the **Intents** page, select **Create new intent**.</span><span class="sxs-lookup"><span data-stu-id="2b67a-137">On the **Intents** page, select **Create new intent**.</span></span> 

3. <span data-ttu-id="2b67a-138">Enter `OrgChart-Manager` in the pop-up dialog box then select **Done**.</span><span class="sxs-lookup"><span data-stu-id="2b67a-138">Enter `OrgChart-Manager` in the pop-up dialog box then select **Done**.</span></span>

    ![Create new message pop-up window](media/luis-tutorial-pattern/hr-create-new-intent-popup.png)

4. <span data-ttu-id="2b67a-140">Add example utterances to the intent.</span><span class="sxs-lookup"><span data-stu-id="2b67a-140">Add example utterances to the intent.</span></span>

    |<span data-ttu-id="2b67a-141">Example utterances</span><span class="sxs-lookup"><span data-stu-id="2b67a-141">Example utterances</span></span>|
    |--|
    |<span data-ttu-id="2b67a-142">Who is John W. Smith the subordinate of?</span><span class="sxs-lookup"><span data-stu-id="2b67a-142">Who is John W. Smith the subordinate of?</span></span>|
    |<span data-ttu-id="2b67a-143">Who does John W. Smith report to?</span><span class="sxs-lookup"><span data-stu-id="2b67a-143">Who does John W. Smith report to?</span></span>|
    |<span data-ttu-id="2b67a-144">Who is John W. Smith's manager?</span><span class="sxs-lookup"><span data-stu-id="2b67a-144">Who is John W. Smith's manager?</span></span>|
    |<span data-ttu-id="2b67a-145">Who does Jill Jones directly report to?</span><span class="sxs-lookup"><span data-stu-id="2b67a-145">Who does Jill Jones directly report to?</span></span>|
    |<span data-ttu-id="2b67a-146">Who is Jill Jones supervisor?</span><span class="sxs-lookup"><span data-stu-id="2b67a-146">Who is Jill Jones supervisor?</span></span>|

    <span data-ttu-id="2b67a-147">[![Screenshot of LUIS adding new utterances to intent](media/luis-tutorial-pattern/hr-orgchart-manager-intent.png "Screenshot of LUIS adding new utterances to intent")](media/luis-tutorial-pattern/hr-orgchart-manager-intent.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="2b67a-147">[![Screenshot of LUIS adding new utterances to intent](media/luis-tutorial-pattern/hr-orgchart-manager-intent.png "Screenshot of LUIS adding new utterances to intent")](media/luis-tutorial-pattern/hr-orgchart-manager-intent.png#lightbox)</span></span>

    <span data-ttu-id="2b67a-148">Don't worry if the keyPhrase entity is labeled in the utterances of the intent instead of the employee entity.</span><span class="sxs-lookup"><span data-stu-id="2b67a-148">Don't worry if the keyPhrase entity is labeled in the utterances of the intent instead of the employee entity.</span></span> <span data-ttu-id="2b67a-149">Both are correctly predicted in the Test pane and at the endpoint.</span><span class="sxs-lookup"><span data-stu-id="2b67a-149">Both are correctly predicted in the Test pane and at the endpoint.</span></span> 

5. <span data-ttu-id="2b67a-150">Select **Intents** in the left navigation.</span><span class="sxs-lookup"><span data-stu-id="2b67a-150">Select **Intents** in the left navigation.</span></span>

6. <span data-ttu-id="2b67a-151">Select **Create new intent**.</span><span class="sxs-lookup"><span data-stu-id="2b67a-151">Select **Create new intent**.</span></span> 

7. <span data-ttu-id="2b67a-152">Enter `OrgChart-Reports` in the pop-up dialog box then select **Done**.</span><span class="sxs-lookup"><span data-stu-id="2b67a-152">Enter `OrgChart-Reports` in the pop-up dialog box then select **Done**.</span></span>

8. <span data-ttu-id="2b67a-153">Add example utterances to the intent.</span><span class="sxs-lookup"><span data-stu-id="2b67a-153">Add example utterances to the intent.</span></span>

    |<span data-ttu-id="2b67a-154">Example utterances</span><span class="sxs-lookup"><span data-stu-id="2b67a-154">Example utterances</span></span>|
    |--|
    |<span data-ttu-id="2b67a-155">Who are John W. Smith's subordinates?</span><span class="sxs-lookup"><span data-stu-id="2b67a-155">Who are John W. Smith's subordinates?</span></span>|
    |<span data-ttu-id="2b67a-156">Who reports to John W. Smith?</span><span class="sxs-lookup"><span data-stu-id="2b67a-156">Who reports to John W. Smith?</span></span>|
    |<span data-ttu-id="2b67a-157">Who does John W. Smith manage?</span><span class="sxs-lookup"><span data-stu-id="2b67a-157">Who does John W. Smith manage?</span></span>|
    |<span data-ttu-id="2b67a-158">Who are Jill Jones direct reports?</span><span class="sxs-lookup"><span data-stu-id="2b67a-158">Who are Jill Jones direct reports?</span></span>|
    |<span data-ttu-id="2b67a-159">Who does Jill Jones supervise?</span><span class="sxs-lookup"><span data-stu-id="2b67a-159">Who does Jill Jones supervise?</span></span>|

## <a name="caution-about-example-utterance-quantity"></a><span data-ttu-id="2b67a-160">Caution about example utterance quantity</span><span class="sxs-lookup"><span data-stu-id="2b67a-160">Caution about example utterance quantity</span></span>

<span data-ttu-id="2b67a-161">The quantity of example utterances in these intents is not enough to train LUIS properly.</span><span class="sxs-lookup"><span data-stu-id="2b67a-161">The quantity of example utterances in these intents is not enough to train LUIS properly.</span></span> <span data-ttu-id="2b67a-162">In a real-world app, each intent should have a minimum of 15 utterances with a variety of word choice and utterance length.</span><span class="sxs-lookup"><span data-stu-id="2b67a-162">In a real-world app, each intent should have a minimum of 15 utterances with a variety of word choice and utterance length.</span></span> <span data-ttu-id="2b67a-163">These few utterances are selected specifically to highlight patterns.</span><span class="sxs-lookup"><span data-stu-id="2b67a-163">These few utterances are selected specifically to highlight patterns.</span></span> 

## <a name="train-the-luis-app"></a><span data-ttu-id="2b67a-164">Train the LUIS app</span><span class="sxs-lookup"><span data-stu-id="2b67a-164">Train the LUIS app</span></span>

[!INCLUDE [LUIS How to Train steps](../../../includes/cognitive-services-luis-tutorial-how-to-train.md)]

## <a name="publish-the-app-to-get-the-endpoint-url"></a><span data-ttu-id="2b67a-165">Publish the app to get the endpoint URL</span><span class="sxs-lookup"><span data-stu-id="2b67a-165">Publish the app to get the endpoint URL</span></span>

[!INCLUDE [LUIS How to Publish steps](../../../includes/cognitive-services-luis-tutorial-how-to-publish.md)]

## <a name="query-the-endpoint-with-a-different-utterance"></a><span data-ttu-id="2b67a-166">Query the endpoint with a different utterance</span><span class="sxs-lookup"><span data-stu-id="2b67a-166">Query the endpoint with a different utterance</span></span>

1. [!INCLUDE [LUIS How to get endpoint first step](../../../includes/cognitive-services-luis-tutorial-how-to-get-endpoint.md)]

2. <span data-ttu-id="2b67a-167">Go to the end of the URL in the address and enter `Who is the boss of Jill Jones?`.</span><span class="sxs-lookup"><span data-stu-id="2b67a-167">Go to the end of the URL in the address and enter `Who is the boss of Jill Jones?`.</span></span> <span data-ttu-id="2b67a-168">The last querystring parameter is `q`, the utterance **query**.</span><span class="sxs-lookup"><span data-stu-id="2b67a-168">The last querystring parameter is `q`, the utterance **query**.</span></span> 

    ```JSON
    {
        "query": "who is the boss of jill jones?",
        "topScoringIntent": {
            "intent": "OrgChart-Manager",
            "score": 0.353984952
        },
        "intents": [
            {
                "intent": "OrgChart-Manager",
                "score": 0.353984952
            },
            {
                "intent": "OrgChart-Reports",
                "score": 0.214128986
            },
            {
                "intent": "EmployeeFeedback",
                "score": 0.08434003
            },
            {
                "intent": "MoveEmployee",
                "score": 0.019131
            },
            {
                "intent": "GetJobInformation",
                "score": 0.004819009
            },
            {
                "intent": "Utilities.Confirm",
                "score": 0.0043958663
            },
            {
                "intent": "Utilities.StartOver",
                "score": 0.00312064588
            },
            {
                "intent": "Utilities.Cancel",
                "score": 0.002265454
            },
            {
                "intent": "Utilities.Help",
                "score": 0.00133465114
            },
            {
                "intent": "None",
                "score": 0.0011388344
            },
            {
                "intent": "Utilities.Stop",
                "score": 0.00111166481
            },
            {
                "intent": "FindForm",
                "score": 0.0008900076
            },
            {
                "intent": "ApplyForJob",
                "score": 0.0007836131
            }
        ],
        "entities": [
            {
                "entity": "jill jones",
                "type": "Employee",
                "startIndex": 19,
                "endIndex": 28,
                "resolution": {
                    "values": [
                        "Employee-45612"
                    ]
                }
            },
            {
                "entity": "boss of jill jones",
                "type": "builtin.keyPhrase",
                "startIndex": 11,
                "endIndex": 28
            }
        ]
    }
    ```

<span data-ttu-id="2b67a-169">Did this query succeed?</span><span class="sxs-lookup"><span data-stu-id="2b67a-169">Did this query succeed?</span></span> <span data-ttu-id="2b67a-170">For this training cycle it did succeed.</span><span class="sxs-lookup"><span data-stu-id="2b67a-170">For this training cycle it did succeed.</span></span> <span data-ttu-id="2b67a-171">The scores of the two top intents are close.</span><span class="sxs-lookup"><span data-stu-id="2b67a-171">The scores of the two top intents are close.</span></span> <span data-ttu-id="2b67a-172">Because LUIS training is not exactly the same each time, there is a bit of variation, these two scores could invert on the next training cycle.</span><span class="sxs-lookup"><span data-stu-id="2b67a-172">Because LUIS training is not exactly the same each time, there is a bit of variation, these two scores could invert on the next training cycle.</span></span> <span data-ttu-id="2b67a-173">The result is that the wrong intent could be returned.</span><span class="sxs-lookup"><span data-stu-id="2b67a-173">The result is that the wrong intent could be returned.</span></span> 

<span data-ttu-id="2b67a-174">Use patterns to make the correct intent's score significantly higher in percentage and farther from the next highest score.</span><span class="sxs-lookup"><span data-stu-id="2b67a-174">Use patterns to make the correct intent's score significantly higher in percentage and farther from the next highest score.</span></span> 

<span data-ttu-id="2b67a-175">Leave this second browser window open.</span><span class="sxs-lookup"><span data-stu-id="2b67a-175">Leave this second browser window open.</span></span> <span data-ttu-id="2b67a-176">You use it again later in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="2b67a-176">You use it again later in the tutorial.</span></span> 

## <a name="add-the-template-utterances"></a><span data-ttu-id="2b67a-177">Add the template utterances</span><span class="sxs-lookup"><span data-stu-id="2b67a-177">Add the template utterances</span></span>

1. <span data-ttu-id="2b67a-178">Select **Build** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="2b67a-178">Select **Build** in the top menu.</span></span>

2. <span data-ttu-id="2b67a-179">In the left navigation, under **Improve app performance**, select **Patterns** from the left navigation.</span><span class="sxs-lookup"><span data-stu-id="2b67a-179">In the left navigation, under **Improve app performance**, select **Patterns** from the left navigation.</span></span>

3. <span data-ttu-id="2b67a-180">Select the **OrgChart-Manager** intent, then enter the following template utterances, one at a time, selecting enter after each template utterance:</span><span class="sxs-lookup"><span data-stu-id="2b67a-180">Select the **OrgChart-Manager** intent, then enter the following template utterances, one at a time, selecting enter after each template utterance:</span></span>

    |<span data-ttu-id="2b67a-181">Template utterances</span><span class="sxs-lookup"><span data-stu-id="2b67a-181">Template utterances</span></span>|
    |:--|
    |<span data-ttu-id="2b67a-182">Who is {Employee} the subordinate of[?]</span><span class="sxs-lookup"><span data-stu-id="2b67a-182">Who is {Employee} the subordinate of[?]</span></span>|
    |<span data-ttu-id="2b67a-183">Who does {Employee} report to[?]</span><span class="sxs-lookup"><span data-stu-id="2b67a-183">Who does {Employee} report to[?]</span></span>|
    |<span data-ttu-id="2b67a-184">Who is {Employee}['s] manager[?]</span><span class="sxs-lookup"><span data-stu-id="2b67a-184">Who is {Employee}['s] manager[?]</span></span>|
    |<span data-ttu-id="2b67a-185">Who does {Employee} directly report to[?]</span><span class="sxs-lookup"><span data-stu-id="2b67a-185">Who does {Employee} directly report to[?]</span></span>|
    |<span data-ttu-id="2b67a-186">Who is {Employee}['s] supervisor[?]</span><span class="sxs-lookup"><span data-stu-id="2b67a-186">Who is {Employee}['s] supervisor[?]</span></span>|
    |<span data-ttu-id="2b67a-187">Who is the boss of {Employee}[?]</span><span class="sxs-lookup"><span data-stu-id="2b67a-187">Who is the boss of {Employee}[?]</span></span>|

    <span data-ttu-id="2b67a-188">The `{Employee}` syntax marks the entity location within the template utterance as well as which entity it is.</span><span class="sxs-lookup"><span data-stu-id="2b67a-188">The `{Employee}` syntax marks the entity location within the template utterance as well as which entity it is.</span></span> 

    <span data-ttu-id="2b67a-189">Entities with roles use syntax that includes the role name, and are covered in a [separate tutorial for roles](luis-tutorial-pattern-roles.md).</span><span class="sxs-lookup"><span data-stu-id="2b67a-189">Entities with roles use syntax that includes the role name, and are covered in a [separate tutorial for roles](luis-tutorial-pattern-roles.md).</span></span> 

    <span data-ttu-id="2b67a-190">The optional syntax, `[]`, marks words or punctuation that are optional.</span><span class="sxs-lookup"><span data-stu-id="2b67a-190">The optional syntax, `[]`, marks words or punctuation that are optional.</span></span> <span data-ttu-id="2b67a-191">LUIS matches the utterance, ignoring the optional text inside the brackets.</span><span class="sxs-lookup"><span data-stu-id="2b67a-191">LUIS matches the utterance, ignoring the optional text inside the brackets.</span></span>

    <span data-ttu-id="2b67a-192">If you type the template utterance, LUIS helps you fill in the entity when you enter the left curly bracket, `{`.</span><span class="sxs-lookup"><span data-stu-id="2b67a-192">If you type the template utterance, LUIS helps you fill in the entity when you enter the left curly bracket, `{`.</span></span>

    <span data-ttu-id="2b67a-193">[![Screenshot of entering template utterances for intent](./media/luis-tutorial-pattern/hr-pattern-missing-entity.png)](./media/luis-tutorial-pattern/hr-pattern-missing-entity.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="2b67a-193">[![Screenshot of entering template utterances for intent](./media/luis-tutorial-pattern/hr-pattern-missing-entity.png)](./media/luis-tutorial-pattern/hr-pattern-missing-entity.png#lightbox)</span></span>

4. <span data-ttu-id="2b67a-194">Select the **OrgChart-Reports** intent, then enter the following template utterances, one at a time, selecting enter after each template utterance:</span><span class="sxs-lookup"><span data-stu-id="2b67a-194">Select the **OrgChart-Reports** intent, then enter the following template utterances, one at a time, selecting enter after each template utterance:</span></span>

    |<span data-ttu-id="2b67a-195">Template utterances</span><span class="sxs-lookup"><span data-stu-id="2b67a-195">Template utterances</span></span>|
    |:--|
    |<span data-ttu-id="2b67a-196">Who are {Employee}['s] subordinates[?]</span><span class="sxs-lookup"><span data-stu-id="2b67a-196">Who are {Employee}['s] subordinates[?]</span></span>|
    |<span data-ttu-id="2b67a-197">Who reports to {Employee}[?]</span><span class="sxs-lookup"><span data-stu-id="2b67a-197">Who reports to {Employee}[?]</span></span>|
    |<span data-ttu-id="2b67a-198">Who does {Employee} manage[?]</span><span class="sxs-lookup"><span data-stu-id="2b67a-198">Who does {Employee} manage[?]</span></span>|
    |<span data-ttu-id="2b67a-199">Who are {Employee} direct reports[?]</span><span class="sxs-lookup"><span data-stu-id="2b67a-199">Who are {Employee} direct reports[?]</span></span>|
    |<span data-ttu-id="2b67a-200">Who does {Employee} supervise[?]</span><span class="sxs-lookup"><span data-stu-id="2b67a-200">Who does {Employee} supervise[?]</span></span>|
    |<span data-ttu-id="2b67a-201">Who does {Employee} boss[?]</span><span class="sxs-lookup"><span data-stu-id="2b67a-201">Who does {Employee} boss[?]</span></span>|

## <a name="query-endpoint-when-patterns-are-used"></a><span data-ttu-id="2b67a-202">Query endpoint when patterns are used</span><span class="sxs-lookup"><span data-stu-id="2b67a-202">Query endpoint when patterns are used</span></span>

1. <span data-ttu-id="2b67a-203">Train and publish the app again.</span><span class="sxs-lookup"><span data-stu-id="2b67a-203">Train and publish the app again.</span></span>

2. <span data-ttu-id="2b67a-204">Switch browser tabs back to the endpoint URL tab.</span><span class="sxs-lookup"><span data-stu-id="2b67a-204">Switch browser tabs back to the endpoint URL tab.</span></span>

3. <span data-ttu-id="2b67a-205">Go to the end of the URL in the address and enter `Who is the boss of Jill Jones?` as the utterance.</span><span class="sxs-lookup"><span data-stu-id="2b67a-205">Go to the end of the URL in the address and enter `Who is the boss of Jill Jones?` as the utterance.</span></span> <span data-ttu-id="2b67a-206">The last querystring parameter is `q`, the utterance **query**.</span><span class="sxs-lookup"><span data-stu-id="2b67a-206">The last querystring parameter is `q`, the utterance **query**.</span></span> 

    ```JSON
    {
        "query": "who is the boss of jill jones?",
        "topScoringIntent": {
            "intent": "OrgChart-Manager",
            "score": 0.9999989
        },
        "intents": [
            {
                "intent": "OrgChart-Manager",
                "score": 0.9999989
            },
            {
                "intent": "OrgChart-Reports",
                "score": 7.616303E-05
            },
            {
                "intent": "EmployeeFeedback",
                "score": 7.84204349E-06
            },
            {
                "intent": "GetJobInformation",
                "score": 1.20674213E-06
            },
            {
                "intent": "MoveEmployee",
                "score": 7.91245157E-07
            },
            {
                "intent": "None",
                "score": 3.875E-09
            },
            {
                "intent": "Utilities.StartOver",
                "score": 1.49E-09
            },
            {
                "intent": "Utilities.Confirm",
                "score": 1.34545453E-09
            },
            {
                "intent": "Utilities.Help",
                "score": 1.34545453E-09
            },
            {
                "intent": "Utilities.Stop",
                "score": 1.34545453E-09
            },
            {
                "intent": "Utilities.Cancel",
                "score": 1.225E-09
            },
            {
                "intent": "FindForm",
                "score": 1.123077E-09
            },
            {
                "intent": "ApplyForJob",
                "score": 5.625E-10
            }
        ],
        "entities": [
            {
                "entity": "jill jones",
                "type": "Employee",
                "startIndex": 19,
                "endIndex": 28,
                "resolution": {
                    "values": [
                        "Employee-45612"
                    ]
                },
                "role": ""
            },
            {
                "entity": "boss of jill jones",
                "type": "builtin.keyPhrase",
                "startIndex": 11,
                "endIndex": 28
            }
        ]
    }
    ```

<span data-ttu-id="2b67a-207">The intent prediction is now significantly higher.</span><span class="sxs-lookup"><span data-stu-id="2b67a-207">The intent prediction is now significantly higher.</span></span>

## <a name="working-with-optional-text-and-prebuilt-entities"></a><span data-ttu-id="2b67a-208">Working with optional text and prebuilt entities</span><span class="sxs-lookup"><span data-stu-id="2b67a-208">Working with optional text and prebuilt entities</span></span>

<span data-ttu-id="2b67a-209">The previous pattern template utterances in this tutorial had a few examples of optional text such as the possessive use of the letter s, `'s`, and the use of the question mark, `?`.</span><span class="sxs-lookup"><span data-stu-id="2b67a-209">The previous pattern template utterances in this tutorial had a few examples of optional text such as the possessive use of the letter s, `'s`, and the use of the question mark, `?`.</span></span> <span data-ttu-id="2b67a-210">Suppose the endpoint utterances show that managers and Human Resources representatives are looking for historical data as well as planned employee moves within the company happening at a future date.</span><span class="sxs-lookup"><span data-stu-id="2b67a-210">Suppose the endpoint utterances show that managers and Human Resources representatives are looking for historical data as well as planned employee moves within the company happening at a future date.</span></span>

<span data-ttu-id="2b67a-211">Example utterances are:</span><span class="sxs-lookup"><span data-stu-id="2b67a-211">Example utterances are:</span></span>

|<span data-ttu-id="2b67a-212">Intent</span><span class="sxs-lookup"><span data-stu-id="2b67a-212">Intent</span></span>|<span data-ttu-id="2b67a-213">Example utterances with optional text and prebuilt entities</span><span class="sxs-lookup"><span data-stu-id="2b67a-213">Example utterances with optional text and prebuilt entities</span></span>|
|:--|:--|
|<span data-ttu-id="2b67a-214">OrgChart-Manager</span><span class="sxs-lookup"><span data-stu-id="2b67a-214">OrgChart-Manager</span></span>|`Who was Jill Jones manager on March 3?`|
|<span data-ttu-id="2b67a-215">OrgChart-Manager</span><span class="sxs-lookup"><span data-stu-id="2b67a-215">OrgChart-Manager</span></span>|`Who is Jill Jones manager now?`|
|<span data-ttu-id="2b67a-216">OrgChart-Manager</span><span class="sxs-lookup"><span data-stu-id="2b67a-216">OrgChart-Manager</span></span>|`Who will be Jill Jones manager in a month?`|
|<span data-ttu-id="2b67a-217">OrgChart-Manager</span><span class="sxs-lookup"><span data-stu-id="2b67a-217">OrgChart-Manager</span></span>|`Who will be Jill Jones manager on March 3?`|

<span data-ttu-id="2b67a-218">Each of these examples uses a verb tense, `was`, `is`, `will be`, as well as a date, `March 3`, `now`, and `in a month`, that LUIS needs to predict correctly.</span><span class="sxs-lookup"><span data-stu-id="2b67a-218">Each of these examples uses a verb tense, `was`, `is`, `will be`, as well as a date, `March 3`, `now`, and `in a month`, that LUIS needs to predict correctly.</span></span> <span data-ttu-id="2b67a-219">Notice that the last two examples use almost the same text except for `in` and `on`.</span><span class="sxs-lookup"><span data-stu-id="2b67a-219">Notice that the last two examples use almost the same text except for `in` and `on`.</span></span>

<span data-ttu-id="2b67a-220">Example template utterances:</span><span class="sxs-lookup"><span data-stu-id="2b67a-220">Example template utterances:</span></span>
|<span data-ttu-id="2b67a-221">Intent</span><span class="sxs-lookup"><span data-stu-id="2b67a-221">Intent</span></span>|<span data-ttu-id="2b67a-222">Example utterances with optional text and prebuilt entities</span><span class="sxs-lookup"><span data-stu-id="2b67a-222">Example utterances with optional text and prebuilt entities</span></span>|
|:--|:--|
|<span data-ttu-id="2b67a-223">OrgChart-Manager</span><span class="sxs-lookup"><span data-stu-id="2b67a-223">OrgChart-Manager</span></span>|<span data-ttu-id="2b67a-224">`who was {Employee}['s] manager [[on]{datetimeV2}?`]</span><span class="sxs-lookup"><span data-stu-id="2b67a-224">`who was {Employee}['s] manager [[on]{datetimeV2}?`]</span></span>|
|<span data-ttu-id="2b67a-225">OrgChart-Manager</span><span class="sxs-lookup"><span data-stu-id="2b67a-225">OrgChart-Manager</span></span>|`who is {Employee}['s] manager [[on]{datetimeV2}?]`|
|<span data-ttu-id="2b67a-226">OrgChart-Manager</span><span class="sxs-lookup"><span data-stu-id="2b67a-226">OrgChart-Manager</span></span>|`who will be {Employee}['s] manager [[in]{datetimeV2}?]`|
|<span data-ttu-id="2b67a-227">OrgChart-Manager</span><span class="sxs-lookup"><span data-stu-id="2b67a-227">OrgChart-Manager</span></span>|`who will be {Employee}['s] manager [[on]{datetimeV2}?]`|

<span data-ttu-id="2b67a-228">The use of the optional syntax of square brackets, `[]`, makes this optional text easy to add to the template utterance and can be nested up to a second level, `[[]]`, and include entities or text.</span><span class="sxs-lookup"><span data-stu-id="2b67a-228">The use of the optional syntax of square brackets, `[]`, makes this optional text easy to add to the template utterance and can be nested up to a second level, `[[]]`, and include entities or text.</span></span>

<span data-ttu-id="2b67a-229">**Question: Why couldn't the last two example utterances combine into a single template utterance?**</span><span class="sxs-lookup"><span data-stu-id="2b67a-229">**Question: Why couldn't the last two example utterances combine into a single template utterance?**</span></span> <span data-ttu-id="2b67a-230">The pattern template doesn't support OR syntax.</span><span class="sxs-lookup"><span data-stu-id="2b67a-230">The pattern template doesn't support OR syntax.</span></span> <span data-ttu-id="2b67a-231">In order to catch both the `in` version and the `on` version, each needs to be a separate template utterance.</span><span class="sxs-lookup"><span data-stu-id="2b67a-231">In order to catch both the `in` version and the `on` version, each needs to be a separate template utterance.</span></span>

<span data-ttu-id="2b67a-232">**Question: Why are all the `w` letters, the first letter in each template utterance, lowercase? Shouldn't they be optionally upper or lowercase?**</span><span class="sxs-lookup"><span data-stu-id="2b67a-232">**Question: Why are all the `w` letters, the first letter in each template utterance, lowercase? Shouldn't they be optionally upper or lowercase?**</span></span> <span data-ttu-id="2b67a-233">The utterance submitted to the query endpoint, by the client application, is converted into lowercase.</span><span class="sxs-lookup"><span data-stu-id="2b67a-233">The utterance submitted to the query endpoint, by the client application, is converted into lowercase.</span></span> <span data-ttu-id="2b67a-234">The template utterance can be uppercase or lowercase and the endpoint utterance can also be either.</span><span class="sxs-lookup"><span data-stu-id="2b67a-234">The template utterance can be uppercase or lowercase and the endpoint utterance can also be either.</span></span> <span data-ttu-id="2b67a-235">The comparison is always done after the conversion to lowercase.</span><span class="sxs-lookup"><span data-stu-id="2b67a-235">The comparison is always done after the conversion to lowercase.</span></span>

<span data-ttu-id="2b67a-236">**Question: Why isn't prebuilt number part of the template utterance if March 3 is predicted both as number `3` and date `March 3`?**</span><span class="sxs-lookup"><span data-stu-id="2b67a-236">**Question: Why isn't prebuilt number part of the template utterance if March 3 is predicted both as number `3` and date `March 3`?**</span></span> <span data-ttu-id="2b67a-237">The template utterance contextually is using a date, either literally as in `March 3` or abstracted as `in a month`.</span><span class="sxs-lookup"><span data-stu-id="2b67a-237">The template utterance contextually is using a date, either literally as in `March 3` or abstracted as `in a month`.</span></span> <span data-ttu-id="2b67a-238">A date can contain a number but a number may not necessarily be seen as a date.</span><span class="sxs-lookup"><span data-stu-id="2b67a-238">A date can contain a number but a number may not necessarily be seen as a date.</span></span> <span data-ttu-id="2b67a-239">Always use the entity that best represents the type you want returned in the prediction JSON results.</span><span class="sxs-lookup"><span data-stu-id="2b67a-239">Always use the entity that best represents the type you want returned in the prediction JSON results.</span></span>  

<span data-ttu-id="2b67a-240">**Question: What about poorly phrased utterances such as `Who will {Employee}['s] manager be on March 3?`.**</span><span class="sxs-lookup"><span data-stu-id="2b67a-240">**Question: What about poorly phrased utterances such as `Who will {Employee}['s] manager be on March 3?`.**</span></span> <span data-ttu-id="2b67a-241">Grammatically different verb tenses such as this where the `will` and `be` are separated need to be a new template utterance.</span><span class="sxs-lookup"><span data-stu-id="2b67a-241">Grammatically different verb tenses such as this where the `will` and `be` are separated need to be a new template utterance.</span></span> <span data-ttu-id="2b67a-242">The existing template utterance will not match it.</span><span class="sxs-lookup"><span data-stu-id="2b67a-242">The existing template utterance will not match it.</span></span> <span data-ttu-id="2b67a-243">While the intent of the utterance hasn't changed, the word placement in the utterance has changed.</span><span class="sxs-lookup"><span data-stu-id="2b67a-243">While the intent of the utterance hasn't changed, the word placement in the utterance has changed.</span></span> <span data-ttu-id="2b67a-244">This change impacts the prediction in LUIS.</span><span class="sxs-lookup"><span data-stu-id="2b67a-244">This change impacts the prediction in LUIS.</span></span>

<span data-ttu-id="2b67a-245">**Remember: entities are found first, then the pattern is matched.**</span><span class="sxs-lookup"><span data-stu-id="2b67a-245">**Remember: entities are found first, then the pattern is matched.**</span></span>

## <a name="edit-the-existing-pattern-template-utterance"></a><span data-ttu-id="2b67a-246">Edit the existing pattern template utterance</span><span class="sxs-lookup"><span data-stu-id="2b67a-246">Edit the existing pattern template utterance</span></span>

1. <span data-ttu-id="2b67a-247">On the LUIS website, select **Build** in the top menu then select **Patterns** in the left menu.</span><span class="sxs-lookup"><span data-stu-id="2b67a-247">On the LUIS website, select **Build** in the top menu then select **Patterns** in the left menu.</span></span> 

2. <span data-ttu-id="2b67a-248">Find the existing template utterance, `Who is {Employee}['s] manager[?]`, and select the ellipsis (***...***) to the right.</span><span class="sxs-lookup"><span data-stu-id="2b67a-248">Find the existing template utterance, `Who is {Employee}['s] manager[?]`, and select the ellipsis (***...***) to the right.</span></span> 

3. <span data-ttu-id="2b67a-249">Select **Edit** from the pop-up menu.</span><span class="sxs-lookup"><span data-stu-id="2b67a-249">Select **Edit** from the pop-up menu.</span></span> 

4. <span data-ttu-id="2b67a-250">Change the template utterance to: `who is {Employee}['s] manager [[on]{datetimeV2}?]]`</span><span class="sxs-lookup"><span data-stu-id="2b67a-250">Change the template utterance to: `who is {Employee}['s] manager [[on]{datetimeV2}?]]`</span></span>

## <a name="add-new-pattern-template-utterances"></a><span data-ttu-id="2b67a-251">Add new pattern template utterances</span><span class="sxs-lookup"><span data-stu-id="2b67a-251">Add new pattern template utterances</span></span>

1. <span data-ttu-id="2b67a-252">While still in the **Patterns** section of **Build**, add several new pattern template utterances.</span><span class="sxs-lookup"><span data-stu-id="2b67a-252">While still in the **Patterns** section of **Build**, add several new pattern template utterances.</span></span> <span data-ttu-id="2b67a-253">Select **OrgChart-Manager** from the Intent drop-down menu and enter each of the following template utterances:</span><span class="sxs-lookup"><span data-stu-id="2b67a-253">Select **OrgChart-Manager** from the Intent drop-down menu and enter each of the following template utterances:</span></span>

    |<span data-ttu-id="2b67a-254">Intent</span><span class="sxs-lookup"><span data-stu-id="2b67a-254">Intent</span></span>|<span data-ttu-id="2b67a-255">Example utterances with optional text and prebuilt entities</span><span class="sxs-lookup"><span data-stu-id="2b67a-255">Example utterances with optional text and prebuilt entities</span></span>|
    |--|--|
    |<span data-ttu-id="2b67a-256">OrgChart-Manager</span><span class="sxs-lookup"><span data-stu-id="2b67a-256">OrgChart-Manager</span></span>|`who was {Employee}['s] manager [[on]{datetimeV2}?]`|
    |<span data-ttu-id="2b67a-257">OrgChart-Manager</span><span class="sxs-lookup"><span data-stu-id="2b67a-257">OrgChart-Manager</span></span>|`who is {Employee}['s] manager [[on]{datetimeV2}?]`|
    |<span data-ttu-id="2b67a-258">OrgChart-Manager</span><span class="sxs-lookup"><span data-stu-id="2b67a-258">OrgChart-Manager</span></span>|`who will be {Employee}['s] manager [[in]{datetimeV2}?]`|
    |<span data-ttu-id="2b67a-259">OrgChart-Manager</span><span class="sxs-lookup"><span data-stu-id="2b67a-259">OrgChart-Manager</span></span>|`who will be {Employee}['s] manager [[on]{datetimeV2}?]`|

2. <span data-ttu-id="2b67a-260">Train the app.</span><span class="sxs-lookup"><span data-stu-id="2b67a-260">Train the app.</span></span>

3. <span data-ttu-id="2b67a-261">Select **Test** at the top of the panel to open the testing panel.</span><span class="sxs-lookup"><span data-stu-id="2b67a-261">Select **Test** at the top of the panel to open the testing panel.</span></span> 

4. <span data-ttu-id="2b67a-262">Enter several test utterances to verify that the pattern is matched and the intent score is significantly high.</span><span class="sxs-lookup"><span data-stu-id="2b67a-262">Enter several test utterances to verify that the pattern is matched and the intent score is significantly high.</span></span> 

    <span data-ttu-id="2b67a-263">After you enter the first utterance, select **Inspect** under the result so you can see all the prediction results.</span><span class="sxs-lookup"><span data-stu-id="2b67a-263">After you enter the first utterance, select **Inspect** under the result so you can see all the prediction results.</span></span>

    |<span data-ttu-id="2b67a-264">Utterance</span><span class="sxs-lookup"><span data-stu-id="2b67a-264">Utterance</span></span>|
    |--|
    |<span data-ttu-id="2b67a-265">Who will be Jill Jones manager</span><span class="sxs-lookup"><span data-stu-id="2b67a-265">Who will be Jill Jones manager</span></span>|
    |<span data-ttu-id="2b67a-266">who will be jill jones's manager</span><span class="sxs-lookup"><span data-stu-id="2b67a-266">who will be jill jones's manager</span></span>|
    |<span data-ttu-id="2b67a-267">Who will be Jill Jones's manager?</span><span class="sxs-lookup"><span data-stu-id="2b67a-267">Who will be Jill Jones's manager?</span></span>|
    |<span data-ttu-id="2b67a-268">who will be Jill jones manager on March 3</span><span class="sxs-lookup"><span data-stu-id="2b67a-268">who will be Jill jones manager on March 3</span></span>|
    |<span data-ttu-id="2b67a-269">Who will be Jill Jones manager next Month</span><span class="sxs-lookup"><span data-stu-id="2b67a-269">Who will be Jill Jones manager next Month</span></span>|
    |<span data-ttu-id="2b67a-270">Who will be Jill Jones manager in a month?</span><span class="sxs-lookup"><span data-stu-id="2b67a-270">Who will be Jill Jones manager in a month?</span></span>|

<span data-ttu-id="2b67a-271">All of these utterances found the entities inside, therefore they match the same pattern, and have a high prediction score.</span><span class="sxs-lookup"><span data-stu-id="2b67a-271">All of these utterances found the entities inside, therefore they match the same pattern, and have a high prediction score.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="2b67a-272">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="2b67a-272">Clean up resources</span></span>

[!INCLUDE [LUIS How to clean up resources](../../../includes/cognitive-services-luis-tutorial-how-to-clean-up-resources.md)]

## <a name="next-steps"></a><span data-ttu-id="2b67a-273">Next steps</span><span class="sxs-lookup"><span data-stu-id="2b67a-273">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2b67a-274">Learn how to use roles with a pattern</span><span class="sxs-lookup"><span data-stu-id="2b67a-274">Learn how to use roles with a pattern</span></span>](luis-tutorial-pattern-roles.md)