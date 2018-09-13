---
title: Label entities automatically with a list entity using Nodejs | Microsoft Docs
description: Learn how to add a list entity to help LUIS label variations of a word or phrase.
services: cognitive-services
author: diberry
titleSuffix: Azure
manager: cjgronlund
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: article
ms.date: 02/21/2018
ms.author: diberry
ms.openlocfilehash: ef49e9e3b294cc81a53a23439d3e21c79d1369bd
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969179"
---
# <a name="use-a-list-entity-to-increase-entity-detection"></a><span data-ttu-id="a4b63-103">Use a list entity to increase entity detection</span><span class="sxs-lookup"><span data-stu-id="a4b63-103">Use a list entity to increase entity detection</span></span> 
<span data-ttu-id="a4b63-104">This tutorial demonstrates the use of a [list entity](luis-concept-entity-types.md) to increase entity detection.</span><span class="sxs-lookup"><span data-stu-id="a4b63-104">This tutorial demonstrates the use of a [list entity](luis-concept-entity-types.md) to increase entity detection.</span></span> <span data-ttu-id="a4b63-105">List entities do not need to be labeled as they are an exact match of terms.</span><span class="sxs-lookup"><span data-stu-id="a4b63-105">List entities do not need to be labeled as they are an exact match of terms.</span></span>  

<span data-ttu-id="a4b63-106">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="a4b63-106">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
* <span data-ttu-id="a4b63-107">Create a list entity</span><span class="sxs-lookup"><span data-stu-id="a4b63-107">Create a list entity</span></span> 
* <span data-ttu-id="a4b63-108">Add normalized values and synonyms</span><span class="sxs-lookup"><span data-stu-id="a4b63-108">Add normalized values and synonyms</span></span>
* <span data-ttu-id="a4b63-109">Validate improved entity identification</span><span class="sxs-lookup"><span data-stu-id="a4b63-109">Validate improved entity identification</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a4b63-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a4b63-110">Prerequisites</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a4b63-111">Latest [Node.js](https://nodejs.org)</span><span class="sxs-lookup"><span data-stu-id="a4b63-111">Latest [Node.js](https://nodejs.org)</span></span>
> * <span data-ttu-id="a4b63-112">[HomeAutomation LUIS app](luis-get-started-create-app.md).</span><span class="sxs-lookup"><span data-stu-id="a4b63-112">[HomeAutomation LUIS app](luis-get-started-create-app.md).</span></span> <span data-ttu-id="a4b63-113">If you do not have the Home Automation app created, create a new app, and add the Prebuilt Domain **HomeAutomation**.</span><span class="sxs-lookup"><span data-stu-id="a4b63-113">If you do not have the Home Automation app created, create a new app, and add the Prebuilt Domain **HomeAutomation**.</span></span> <span data-ttu-id="a4b63-114">Train and publish the app.</span><span class="sxs-lookup"><span data-stu-id="a4b63-114">Train and publish the app.</span></span> 
> * <span data-ttu-id="a4b63-115">[AuthoringKey](luis-concept-keys.md#authoring-key), [EndpointKey](luis-concept-keys.md#endpoint-key) (if querying many times), app ID, version ID, and [region](luis-reference-regions.md) for the LUIS app.</span><span class="sxs-lookup"><span data-stu-id="a4b63-115">[AuthoringKey](luis-concept-keys.md#authoring-key), [EndpointKey](luis-concept-keys.md#endpoint-key) (if querying many times), app ID, version ID, and [region](luis-reference-regions.md) for the LUIS app.</span></span>

> [!Tip]
> <span data-ttu-id="a4b63-116">If you do not already have a subscription, you can register for a [free account](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="a4b63-116">If you do not already have a subscription, you can register for a [free account](https://azure.microsoft.com/free/).</span></span>

<span data-ttu-id="a4b63-117">All of the code in this tutorial is available on the [LUIS-Samples github repository](https://github.com/Microsoft/LUIS-Samples/tree/master/documentation-samples/tutorial-list-entity).</span><span class="sxs-lookup"><span data-stu-id="a4b63-117">All of the code in this tutorial is available on the [LUIS-Samples github repository](https://github.com/Microsoft/LUIS-Samples/tree/master/documentation-samples/tutorial-list-entity).</span></span> 

## <a name="use-homeautomation-app"></a><span data-ttu-id="a4b63-118">Use HomeAutomation app</span><span class="sxs-lookup"><span data-stu-id="a4b63-118">Use HomeAutomation app</span></span>
<span data-ttu-id="a4b63-119">The HomeAutomation app gives you control of devices such as lights, entertainment systems, and environment controls such as heating and cooling.</span><span class="sxs-lookup"><span data-stu-id="a4b63-119">The HomeAutomation app gives you control of devices such as lights, entertainment systems, and environment controls such as heating and cooling.</span></span> <span data-ttu-id="a4b63-120">These systems have several different names that can include Manufacturer names, nicknames, acronyms, and slang.</span><span class="sxs-lookup"><span data-stu-id="a4b63-120">These systems have several different names that can include Manufacturer names, nicknames, acronyms, and slang.</span></span> 

<span data-ttu-id="a4b63-121">One system that has many names across different cultures and demographics is the thermostat.</span><span class="sxs-lookup"><span data-stu-id="a4b63-121">One system that has many names across different cultures and demographics is the thermostat.</span></span> <span data-ttu-id="a4b63-122">A thermostat can control both cooling and heating systems for a house or building.</span><span class="sxs-lookup"><span data-stu-id="a4b63-122">A thermostat can control both cooling and heating systems for a house or building.</span></span>

<span data-ttu-id="a4b63-123">Ideally the following utterances should resolve to the Prebuilt entity **HomeAutomation.Device**:</span><span class="sxs-lookup"><span data-stu-id="a4b63-123">Ideally the following utterances should resolve to the Prebuilt entity **HomeAutomation.Device**:</span></span>

|#|<span data-ttu-id="a4b63-124">utterance</span><span class="sxs-lookup"><span data-stu-id="a4b63-124">utterance</span></span>|<span data-ttu-id="a4b63-125">entity identified</span><span class="sxs-lookup"><span data-stu-id="a4b63-125">entity identified</span></span>|<span data-ttu-id="a4b63-126">score</span><span class="sxs-lookup"><span data-stu-id="a4b63-126">score</span></span>|
|--|--|--|--|
|<span data-ttu-id="a4b63-127">1</span><span class="sxs-lookup"><span data-stu-id="a4b63-127">1</span></span>|<span data-ttu-id="a4b63-128">turn on the ac</span><span class="sxs-lookup"><span data-stu-id="a4b63-128">turn on the ac</span></span>|<span data-ttu-id="a4b63-129">HomeAutomation.Device - "ac"</span><span class="sxs-lookup"><span data-stu-id="a4b63-129">HomeAutomation.Device - "ac"</span></span>|<span data-ttu-id="a4b63-130">0.8748562</span><span class="sxs-lookup"><span data-stu-id="a4b63-130">0.8748562</span></span>|
|<span data-ttu-id="a4b63-131">2</span><span class="sxs-lookup"><span data-stu-id="a4b63-131">2</span></span>|<span data-ttu-id="a4b63-132">turn up the heat</span><span class="sxs-lookup"><span data-stu-id="a4b63-132">turn up the heat</span></span>|<span data-ttu-id="a4b63-133">HomeAutomation.Device - "heat"</span><span class="sxs-lookup"><span data-stu-id="a4b63-133">HomeAutomation.Device - "heat"</span></span>|<span data-ttu-id="a4b63-134">0.784990132</span><span class="sxs-lookup"><span data-stu-id="a4b63-134">0.784990132</span></span>|
|<span data-ttu-id="a4b63-135">3</span><span class="sxs-lookup"><span data-stu-id="a4b63-135">3</span></span>|<span data-ttu-id="a4b63-136">make it colder</span><span class="sxs-lookup"><span data-stu-id="a4b63-136">make it colder</span></span>|||

<span data-ttu-id="a4b63-137">The first two utterances map to different devices.</span><span class="sxs-lookup"><span data-stu-id="a4b63-137">The first two utterances map to different devices.</span></span> <span data-ttu-id="a4b63-138">The third utterance, "make it colder", doesn't map to a device but instead requests a result.</span><span class="sxs-lookup"><span data-stu-id="a4b63-138">The third utterance, "make it colder", doesn't map to a device but instead requests a result.</span></span> <span data-ttu-id="a4b63-139">LUIS doesn't know that the term, "colder", means the thermostat is the requested device.</span><span class="sxs-lookup"><span data-stu-id="a4b63-139">LUIS doesn't know that the term, "colder", means the thermostat is the requested device.</span></span> <span data-ttu-id="a4b63-140">Ideally, LUIS should resolve all of these utterances to the same device.</span><span class="sxs-lookup"><span data-stu-id="a4b63-140">Ideally, LUIS should resolve all of these utterances to the same device.</span></span> 

## <a name="use-a-list-entity"></a><span data-ttu-id="a4b63-141">Use a list entity</span><span class="sxs-lookup"><span data-stu-id="a4b63-141">Use a list entity</span></span>
<span data-ttu-id="a4b63-142">The HomeAutomation.Device entity is great for a small number of devices or with few variations of the names.</span><span class="sxs-lookup"><span data-stu-id="a4b63-142">The HomeAutomation.Device entity is great for a small number of devices or with few variations of the names.</span></span> <span data-ttu-id="a4b63-143">For an office building or campus, the device names grow beyond the usefulness of the HomeAutomation.Device entity.</span><span class="sxs-lookup"><span data-stu-id="a4b63-143">For an office building or campus, the device names grow beyond the usefulness of the HomeAutomation.Device entity.</span></span> 

<span data-ttu-id="a4b63-144">A **list entity** is a good choice for this scenario because the set of terms for a device in a building or campus is a known set, even if it is a huge set.</span><span class="sxs-lookup"><span data-stu-id="a4b63-144">A **list entity** is a good choice for this scenario because the set of terms for a device in a building or campus is a known set, even if it is a huge set.</span></span> <span data-ttu-id="a4b63-145">By using a list entity, LUIS can receive any possible value in the set for the thermostat, and resolve it down to just the single device "thermostat".</span><span class="sxs-lookup"><span data-stu-id="a4b63-145">By using a list entity, LUIS can receive any possible value in the set for the thermostat, and resolve it down to just the single device "thermostat".</span></span> 

<span data-ttu-id="a4b63-146">This tutorial is going to create an entity list with the thermostat.</span><span class="sxs-lookup"><span data-stu-id="a4b63-146">This tutorial is going to create an entity list with the thermostat.</span></span> <span data-ttu-id="a4b63-147">The alternative names for a thermostat in this tutorial are:</span><span class="sxs-lookup"><span data-stu-id="a4b63-147">The alternative names for a thermostat in this tutorial are:</span></span> 

|<span data-ttu-id="a4b63-148">alternative names for thermostat</span><span class="sxs-lookup"><span data-stu-id="a4b63-148">alternative names for thermostat</span></span>|
|--|
| <span data-ttu-id="a4b63-149">ac</span><span class="sxs-lookup"><span data-stu-id="a4b63-149">ac</span></span> |
| <span data-ttu-id="a4b63-150">a/c</span><span class="sxs-lookup"><span data-stu-id="a4b63-150">a/c</span></span>|
| <span data-ttu-id="a4b63-151">a-c</span><span class="sxs-lookup"><span data-stu-id="a4b63-151">a-c</span></span>|
|<span data-ttu-id="a4b63-152">heater</span><span class="sxs-lookup"><span data-stu-id="a4b63-152">heater</span></span>|
|<span data-ttu-id="a4b63-153">hot</span><span class="sxs-lookup"><span data-stu-id="a4b63-153">hot</span></span>|
|<span data-ttu-id="a4b63-154">hotter</span><span class="sxs-lookup"><span data-stu-id="a4b63-154">hotter</span></span>|
|<span data-ttu-id="a4b63-155">cold</span><span class="sxs-lookup"><span data-stu-id="a4b63-155">cold</span></span>|
|<span data-ttu-id="a4b63-156">colder</span><span class="sxs-lookup"><span data-stu-id="a4b63-156">colder</span></span>|

<span data-ttu-id="a4b63-157">If LUIS needs to determine a new alternative often, then a [phrase list](luis-concept-feature.md#how-to-use-phrase-lists) is a better answer.</span><span class="sxs-lookup"><span data-stu-id="a4b63-157">If LUIS needs to determine a new alternative often, then a [phrase list](luis-concept-feature.md#how-to-use-phrase-lists) is a better answer.</span></span>

## <a name="create-a-list-entity"></a><span data-ttu-id="a4b63-158">Create a list entity</span><span class="sxs-lookup"><span data-stu-id="a4b63-158">Create a list entity</span></span>
<span data-ttu-id="a4b63-159">Create a Node.js file and copy the following code into it.</span><span class="sxs-lookup"><span data-stu-id="a4b63-159">Create a Node.js file and copy the following code into it.</span></span> <span data-ttu-id="a4b63-160">Change the authoringKey, appId, versionId, and region values.</span><span class="sxs-lookup"><span data-stu-id="a4b63-160">Change the authoringKey, appId, versionId, and region values.</span></span>

   [!code-javascript[Create DevicesList List Entity](~/samples-luis/documentation-samples/tutorial-list-entity/add-entity-list.js "Create DevicesList List Entity")]

<span data-ttu-id="a4b63-161">Use the following command to install the NPM dependencies and run the code to create the list entity:</span><span class="sxs-lookup"><span data-stu-id="a4b63-161">Use the following command to install the NPM dependencies and run the code to create the list entity:</span></span>

```Javascript
npm install && node add-entity-list.js
```

<span data-ttu-id="a4b63-162">The output of the run is the ID of the list entity:</span><span class="sxs-lookup"><span data-stu-id="a4b63-162">The output of the run is the ID of the list entity:</span></span>

```Javascript
026e92b3-4834-484f-8608-6114a83b03a6
```
## <a name="train-the-model"></a><span data-ttu-id="a4b63-163">Train the model</span><span class="sxs-lookup"><span data-stu-id="a4b63-163">Train the model</span></span>
<span data-ttu-id="a4b63-164">Train LUIS in order for the new list to affect the query results.</span><span class="sxs-lookup"><span data-stu-id="a4b63-164">Train LUIS in order for the new list to affect the query results.</span></span> <span data-ttu-id="a4b63-165">Training is a two-part process of training, then checking status if the training is done.</span><span class="sxs-lookup"><span data-stu-id="a4b63-165">Training is a two-part process of training, then checking status if the training is done.</span></span> <span data-ttu-id="a4b63-166">An app with many models may take a few moments to train.</span><span class="sxs-lookup"><span data-stu-id="a4b63-166">An app with many models may take a few moments to train.</span></span> <span data-ttu-id="a4b63-167">The following code trains the app then waits until the training is successful.</span><span class="sxs-lookup"><span data-stu-id="a4b63-167">The following code trains the app then waits until the training is successful.</span></span> <span data-ttu-id="a4b63-168">The code uses a wait-and-retry strategy to avoid the 429 "Too many requests" error.</span><span class="sxs-lookup"><span data-stu-id="a4b63-168">The code uses a wait-and-retry strategy to avoid the 429 "Too many requests" error.</span></span> 

<span data-ttu-id="a4b63-169">Create a Node.js file and copy the following code into it.</span><span class="sxs-lookup"><span data-stu-id="a4b63-169">Create a Node.js file and copy the following code into it.</span></span> <span data-ttu-id="a4b63-170">Change the authoringKey, appId, versionId, and region values.</span><span class="sxs-lookup"><span data-stu-id="a4b63-170">Change the authoringKey, appId, versionId, and region values.</span></span>

   [!code-javascript[Train LUIS](~/samples-luis/documentation-samples/tutorial-list-entity/train.js "Train LUIS")]

<span data-ttu-id="a4b63-171">Use the following command to run the code to train the app:</span><span class="sxs-lookup"><span data-stu-id="a4b63-171">Use the following command to run the code to train the app:</span></span>

```Javascript
node train.js
```

<span data-ttu-id="a4b63-172">The output of the run is the status of each iteration of the training of the LUIS models.</span><span class="sxs-lookup"><span data-stu-id="a4b63-172">The output of the run is the status of each iteration of the training of the LUIS models.</span></span> <span data-ttu-id="a4b63-173">The following execution required only one check of training:</span><span class="sxs-lookup"><span data-stu-id="a4b63-173">The following execution required only one check of training:</span></span>

```Javascript
1 trained = true
[ { modelId: '2c549f95-867a-4189-9c35-44b95c78b70f',
    details: { statusId: 2, status: 'UpToDate', exampleCount: 45 } },
  { modelId: '5530e900-571d-40ec-9c78-63e66b50c7d4',
    details: { statusId: 2, status: 'UpToDate', exampleCount: 45 } },
  { modelId: '519faa39-ae1a-4d98-965c-abff6f743fe6',
    details: { statusId: 2, status: 'UpToDate', exampleCount: 45 } },
  { modelId: '9671a485-36a9-46d5-aacd-b16d05115415',
    details: { statusId: 2, status: 'UpToDate', exampleCount: 45 } },
  { modelId: '9ef7d891-54ab-48bf-8112-c34dcd75d5e2',
    details: { statusId: 2, status: 'UpToDate', exampleCount: 45 } },
  { modelId: '8e16a660-8781-4abf-bf3d-f296ebe1bf2d',
    details: { statusId: 2, status: 'UpToDate', exampleCount: 45 } } ]

```
## <a name="publish-the-model"></a><span data-ttu-id="a4b63-174">Publish the model</span><span class="sxs-lookup"><span data-stu-id="a4b63-174">Publish the model</span></span>
<span data-ttu-id="a4b63-175">Publish so the list entity is available from the endpoint.</span><span class="sxs-lookup"><span data-stu-id="a4b63-175">Publish so the list entity is available from the endpoint.</span></span>

<span data-ttu-id="a4b63-176">Create a Node.js file and copy the following code into it.</span><span class="sxs-lookup"><span data-stu-id="a4b63-176">Create a Node.js file and copy the following code into it.</span></span> <span data-ttu-id="a4b63-177">Change the endpointKey, appId, and region values.</span><span class="sxs-lookup"><span data-stu-id="a4b63-177">Change the endpointKey, appId, and region values.</span></span> <span data-ttu-id="a4b63-178">You can use your authoringKey if you do not plan to call this file beyond your quota limit.</span><span class="sxs-lookup"><span data-stu-id="a4b63-178">You can use your authoringKey if you do not plan to call this file beyond your quota limit.</span></span>

   [!code-javascript[Publish LUIS](~/samples-luis/documentation-samples/tutorial-list-entity/publish.js "Publish LUIS")]

<span data-ttu-id="a4b63-179">Use the following command to run the code to query the app:</span><span class="sxs-lookup"><span data-stu-id="a4b63-179">Use the following command to run the code to query the app:</span></span>

```Javascript
node publish.js
```

<span data-ttu-id="a4b63-180">The following output includes the endpoint url for any queries.</span><span class="sxs-lookup"><span data-stu-id="a4b63-180">The following output includes the endpoint url for any queries.</span></span> <span data-ttu-id="a4b63-181">Real JSON results would include the real appID.</span><span class="sxs-lookup"><span data-stu-id="a4b63-181">Real JSON results would include the real appID.</span></span> 

```JSON
{ 
  versionId: null,
  isStaging: false,
  endpointUrl: 'https://westus.api.cognitive.microsoft.com/luis/v2.0/apps/<appID>',
  region: null,
  assignedEndpointKey: null,
  endpointRegion: 'westus',
  publishedDateTime: '2018-01-29T22:17:38Z' }
}
```

## <a name="query-the-app"></a><span data-ttu-id="a4b63-182">Query the app</span><span class="sxs-lookup"><span data-stu-id="a4b63-182">Query the app</span></span> 
<span data-ttu-id="a4b63-183">Query the app from the endpoint to prove that the list entity helps LUIS determine the device type.</span><span class="sxs-lookup"><span data-stu-id="a4b63-183">Query the app from the endpoint to prove that the list entity helps LUIS determine the device type.</span></span>

<span data-ttu-id="a4b63-184">Create a Node.js file and copy the following code into it.</span><span class="sxs-lookup"><span data-stu-id="a4b63-184">Create a Node.js file and copy the following code into it.</span></span> <span data-ttu-id="a4b63-185">Change the endpointKey, appId, and region values.</span><span class="sxs-lookup"><span data-stu-id="a4b63-185">Change the endpointKey, appId, and region values.</span></span> <span data-ttu-id="a4b63-186">You can use your authoringKey if you do not plan to call this file beyond your quota limit.</span><span class="sxs-lookup"><span data-stu-id="a4b63-186">You can use your authoringKey if you do not plan to call this file beyond your quota limit.</span></span>

   [!code-javascript[Query LUIS](~/samples-luis/documentation-samples/tutorial-list-entity/query.js "Query LUIS")]

<span data-ttu-id="a4b63-187">Use the following command to run the code and query the app:</span><span class="sxs-lookup"><span data-stu-id="a4b63-187">Use the following command to run the code and query the app:</span></span>

```Javascript
node train.js
```

<span data-ttu-id="a4b63-188">The output is the query results.</span><span class="sxs-lookup"><span data-stu-id="a4b63-188">The output is the query results.</span></span> <span data-ttu-id="a4b63-189">Because the code added the **verbose** name/value pair to the query string, the output includes all intents and their scores:</span><span class="sxs-lookup"><span data-stu-id="a4b63-189">Because the code added the **verbose** name/value pair to the query string, the output includes all intents and their scores:</span></span>

```JSON
{
  "query": "turn up the heat",
  "topScoringIntent": {
    "intent": "HomeAutomation.TurnOn",
    "score": 0.139018849
  },
  "intents": [
    {
      "intent": "HomeAutomation.TurnOn",
      "score": 0.139018849
    },
    {
      "intent": "None",
      "score": 0.120624863
    },
    {
      "intent": "HomeAutomation.TurnOff",
      "score": 0.06746891
    }
  ],
  "entities": [
    {
      "entity": "heat",
      "type": "HomeAutomation.Device",
      "startIndex": 12,
      "endIndex": 15,
      "score": 0.784990132
    },
    {
      "entity": "heat",
      "type": "DevicesList",
      "startIndex": 12,
      "endIndex": 15,
      "resolution": {
        "values": [
          "Thermostat"
        ]
      }
    }
  ]
}
```

<span data-ttu-id="a4b63-190">The specific device of **Thermostat** is identified with a result-oriented query of "turn up the heat".</span><span class="sxs-lookup"><span data-stu-id="a4b63-190">The specific device of **Thermostat** is identified with a result-oriented query of "turn up the heat".</span></span> <span data-ttu-id="a4b63-191">Since the original HomeAutomation.Device entity is still in the app, you can see its results as well.</span><span class="sxs-lookup"><span data-stu-id="a4b63-191">Since the original HomeAutomation.Device entity is still in the app, you can see its results as well.</span></span> 

<span data-ttu-id="a4b63-192">Try the other two utterances to see that they are also returned as a thermostat.</span><span class="sxs-lookup"><span data-stu-id="a4b63-192">Try the other two utterances to see that they are also returned as a thermostat.</span></span> 

|#|<span data-ttu-id="a4b63-193">utterance</span><span class="sxs-lookup"><span data-stu-id="a4b63-193">utterance</span></span>|<span data-ttu-id="a4b63-194">entity</span><span class="sxs-lookup"><span data-stu-id="a4b63-194">entity</span></span>|<span data-ttu-id="a4b63-195">type</span><span class="sxs-lookup"><span data-stu-id="a4b63-195">type</span></span>|<span data-ttu-id="a4b63-196">value</span><span class="sxs-lookup"><span data-stu-id="a4b63-196">value</span></span>|
|--|--|--|--|--|
|<span data-ttu-id="a4b63-197">1</span><span class="sxs-lookup"><span data-stu-id="a4b63-197">1</span></span>|<span data-ttu-id="a4b63-198">turn on the ac</span><span class="sxs-lookup"><span data-stu-id="a4b63-198">turn on the ac</span></span>| <span data-ttu-id="a4b63-199">ac</span><span class="sxs-lookup"><span data-stu-id="a4b63-199">ac</span></span> | <span data-ttu-id="a4b63-200">DevicesList</span><span class="sxs-lookup"><span data-stu-id="a4b63-200">DevicesList</span></span> | <span data-ttu-id="a4b63-201">Thermostat</span><span class="sxs-lookup"><span data-stu-id="a4b63-201">Thermostat</span></span>|
|<span data-ttu-id="a4b63-202">2</span><span class="sxs-lookup"><span data-stu-id="a4b63-202">2</span></span>|<span data-ttu-id="a4b63-203">turn up the heat</span><span class="sxs-lookup"><span data-stu-id="a4b63-203">turn up the heat</span></span>|<span data-ttu-id="a4b63-204">heat</span><span class="sxs-lookup"><span data-stu-id="a4b63-204">heat</span></span>| <span data-ttu-id="a4b63-205">DevicesList</span><span class="sxs-lookup"><span data-stu-id="a4b63-205">DevicesList</span></span> |<span data-ttu-id="a4b63-206">Thermostat</span><span class="sxs-lookup"><span data-stu-id="a4b63-206">Thermostat</span></span>|
|<span data-ttu-id="a4b63-207">3</span><span class="sxs-lookup"><span data-stu-id="a4b63-207">3</span></span>|<span data-ttu-id="a4b63-208">make it colder</span><span class="sxs-lookup"><span data-stu-id="a4b63-208">make it colder</span></span>|<span data-ttu-id="a4b63-209">colder</span><span class="sxs-lookup"><span data-stu-id="a4b63-209">colder</span></span>|<span data-ttu-id="a4b63-210">DevicesList</span><span class="sxs-lookup"><span data-stu-id="a4b63-210">DevicesList</span></span>|<span data-ttu-id="a4b63-211">Thermostat</span><span class="sxs-lookup"><span data-stu-id="a4b63-211">Thermostat</span></span>|

## <a name="next-steps"></a><span data-ttu-id="a4b63-212">Next steps</span><span class="sxs-lookup"><span data-stu-id="a4b63-212">Next steps</span></span>

<span data-ttu-id="a4b63-213">You can create another List entity to expand device locations to rooms, floors, or buildings.</span><span class="sxs-lookup"><span data-stu-id="a4b63-213">You can create another List entity to expand device locations to rooms, floors, or buildings.</span></span> 
