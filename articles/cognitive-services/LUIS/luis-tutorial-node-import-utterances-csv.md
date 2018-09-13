---
title: Build a LUIS app programmatically using Node.js | Microsoft Docs
titleSuffix: Azure
description: Learn how to build a LUIS app programmatically from preexisting data in CSV format using the LUIS Authoring API.
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: article
ms.date: 02/21/2018
ms.author: diberry
ms.openlocfilehash: 42b9800c94171ecbd2dadf30bb2ce2f342063552
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869364"
---
# <a name="build-a-luis-app-programmatically-using-nodejs"></a><span data-ttu-id="1f285-103">Build a LUIS app programmatically using Node.js</span><span class="sxs-lookup"><span data-stu-id="1f285-103">Build a LUIS app programmatically using Node.js</span></span>

<span data-ttu-id="1f285-104">LUIS provides a programmatic API that does everything that the [LUIS](luis-reference-regions.md) website does.</span><span class="sxs-lookup"><span data-stu-id="1f285-104">LUIS provides a programmatic API that does everything that the [LUIS](luis-reference-regions.md) website does.</span></span> <span data-ttu-id="1f285-105">This can save time when you have pre-existing data and it would be faster to create a LUIS app programmatically than by entering information by hand.</span><span class="sxs-lookup"><span data-stu-id="1f285-105">This can save time when you have pre-existing data and it would be faster to create a LUIS app programmatically than by entering information by hand.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="1f285-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="1f285-106">Prerequisites</span></span>

* <span data-ttu-id="1f285-107">Log in to the [LUIS](luis-reference-regions.md) website and find your [authoring key](luis-concept-keys.md#authoring-key) in Account Settings.</span><span class="sxs-lookup"><span data-stu-id="1f285-107">Log in to the [LUIS](luis-reference-regions.md) website and find your [authoring key](luis-concept-keys.md#authoring-key) in Account Settings.</span></span> <span data-ttu-id="1f285-108">You use this key to call the Authoring APIs.</span><span class="sxs-lookup"><span data-stu-id="1f285-108">You use this key to call the Authoring APIs.</span></span>
* <span data-ttu-id="1f285-109">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="1f285-109">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>
* <span data-ttu-id="1f285-110">This tutorial starts with a CSV for a hypothetical company's log files of user requests.</span><span class="sxs-lookup"><span data-stu-id="1f285-110">This tutorial starts with a CSV for a hypothetical company's log files of user requests.</span></span> <span data-ttu-id="1f285-111">Download it [here](https://github.com/Microsoft/LUIS-Samples/blob/master/examples/build-app-programmatically-csv/IoT.csv).</span><span class="sxs-lookup"><span data-stu-id="1f285-111">Download it [here](https://github.com/Microsoft/LUIS-Samples/blob/master/examples/build-app-programmatically-csv/IoT.csv).</span></span>
* <span data-ttu-id="1f285-112">Install the latest Node.js with NPM.</span><span class="sxs-lookup"><span data-stu-id="1f285-112">Install the latest Node.js with NPM.</span></span> <span data-ttu-id="1f285-113">Download it from [here](https://nodejs.org/en/download/).</span><span class="sxs-lookup"><span data-stu-id="1f285-113">Download it from [here](https://nodejs.org/en/download/).</span></span>
* <span data-ttu-id="1f285-114">**[Recommended]** Visual Studio Code for IntelliSense and debugging, download it from [here](https://code.visualstudio.com/) for free.</span><span class="sxs-lookup"><span data-stu-id="1f285-114">**[Recommended]** Visual Studio Code for IntelliSense and debugging, download it from [here](https://code.visualstudio.com/) for free.</span></span>

## <a name="map-preexisting-data-to-intents-and-entities"></a><span data-ttu-id="1f285-115">Map preexisting data to intents and entities</span><span class="sxs-lookup"><span data-stu-id="1f285-115">Map preexisting data to intents and entities</span></span>
<span data-ttu-id="1f285-116">Even if you have a system that wasn't created with LUIS in mind, if it contains textual data that maps to different things users want to do, you might be able to come up with a mapping from the existing categories of user input to intents in LUIS.</span><span class="sxs-lookup"><span data-stu-id="1f285-116">Even if you have a system that wasn't created with LUIS in mind, if it contains textual data that maps to different things users want to do, you might be able to come up with a mapping from the existing categories of user input to intents in LUIS.</span></span> <span data-ttu-id="1f285-117">If you can identify important words or phrases in what the users said, these words might map to entities.</span><span class="sxs-lookup"><span data-stu-id="1f285-117">If you can identify important words or phrases in what the users said, these words might map to entities.</span></span>

<span data-ttu-id="1f285-118">Open the `IoT.csv` file.</span><span class="sxs-lookup"><span data-stu-id="1f285-118">Open the `IoT.csv` file.</span></span> <span data-ttu-id="1f285-119">It contains a log of user queries to a hypothetical home automation service, including how they were categorized, what the user said, and some columns with useful information pulled out of them.</span><span class="sxs-lookup"><span data-stu-id="1f285-119">It contains a log of user queries to a hypothetical home automation service, including how they were categorized, what the user said, and some columns with useful information pulled out of them.</span></span> 

![CSV file](./media/luis-tutorial-node-import-utterances-csv/csv.png) 

<span data-ttu-id="1f285-121">You see that the **RequestType** column could be intents, and the **Request** column shows an example utterance.</span><span class="sxs-lookup"><span data-stu-id="1f285-121">You see that the **RequestType** column could be intents, and the **Request** column shows an example utterance.</span></span> <span data-ttu-id="1f285-122">The other fields could be entities if they occur in the utterance.</span><span class="sxs-lookup"><span data-stu-id="1f285-122">The other fields could be entities if they occur in the utterance.</span></span> <span data-ttu-id="1f285-123">Because there are intents, entities, and example utterances, you have the requirements for a simple, sample app.</span><span class="sxs-lookup"><span data-stu-id="1f285-123">Because there are intents, entities, and example utterances, you have the requirements for a simple, sample app.</span></span>

## <a name="steps-to-generate-a-luis-app-from-non-luis-data"></a><span data-ttu-id="1f285-124">Steps to generate a LUIS app from non-LUIS data</span><span class="sxs-lookup"><span data-stu-id="1f285-124">Steps to generate a LUIS app from non-LUIS data</span></span>
<span data-ttu-id="1f285-125">To generate a new LUIS app from the source file, first you parse the data from the CSV file and convert this data to a format that you can upload to LUIS using the Authoring API.</span><span class="sxs-lookup"><span data-stu-id="1f285-125">To generate a new LUIS app from the source file, first you parse the data from the CSV file and convert this data to a format that you can upload to LUIS using the Authoring API.</span></span> <span data-ttu-id="1f285-126">From the parsed data, you gather information on what intents and entities are there.</span><span class="sxs-lookup"><span data-stu-id="1f285-126">From the parsed data, you gather information on what intents and entities are there.</span></span> <span data-ttu-id="1f285-127">Then you make API calls to create the app, and add intents and entities that were gathered from the parsed data.</span><span class="sxs-lookup"><span data-stu-id="1f285-127">Then you make API calls to create the app, and add intents and entities that were gathered from the parsed data.</span></span> <span data-ttu-id="1f285-128">Once you have created the LUIS app, you can add the example utterances from the parsed data.</span><span class="sxs-lookup"><span data-stu-id="1f285-128">Once you have created the LUIS app, you can add the example utterances from the parsed data.</span></span> <span data-ttu-id="1f285-129">You can see this flow in the last part of the following code.</span><span class="sxs-lookup"><span data-stu-id="1f285-129">You can see this flow in the last part of the following code.</span></span> <span data-ttu-id="1f285-130">Copy or [download](https://github.com/Microsoft/LUIS-Samples/blob/master/examples/build-app-programmatically-csv/index.js) this code and save it in `index.js`.</span><span class="sxs-lookup"><span data-stu-id="1f285-130">Copy or [download](https://github.com/Microsoft/LUIS-Samples/blob/master/examples/build-app-programmatically-csv/index.js) this code and save it in `index.js`.</span></span>

   [!code-javascript[Node.js code for calling the steps to build a LUIS app](~/samples-luis/examples/build-app-programmatically-csv/index.js)]


## <a name="parse-the-csv"></a><span data-ttu-id="1f285-131">Parse the CSV</span><span class="sxs-lookup"><span data-stu-id="1f285-131">Parse the CSV</span></span>

<span data-ttu-id="1f285-132">The column entries that contain the utterances in the CSV have to be parsed into a JSON format that LUIS can understand.</span><span class="sxs-lookup"><span data-stu-id="1f285-132">The column entries that contain the utterances in the CSV have to be parsed into a JSON format that LUIS can understand.</span></span> <span data-ttu-id="1f285-133">This JSON format must contain an `intentName` field that identifies the intent of the utterance.</span><span class="sxs-lookup"><span data-stu-id="1f285-133">This JSON format must contain an `intentName` field that identifies the intent of the utterance.</span></span> <span data-ttu-id="1f285-134">It must also contain an `entityLabels` field, which can be empty if there are no entities in the utterance.</span><span class="sxs-lookup"><span data-stu-id="1f285-134">It must also contain an `entityLabels` field, which can be empty if there are no entities in the utterance.</span></span> 

<span data-ttu-id="1f285-135">For example, the entry for "Turn on the lights" maps to this JSON:</span><span class="sxs-lookup"><span data-stu-id="1f285-135">For example, the entry for "Turn on the lights" maps to this JSON:</span></span>

```json
        {
            "text": "Turn on the lights",
            "intentName": "TurnOn",
            "entityLabels": [
                {
                    "entityName": "Operation",
                    "startCharIndex": 5,
                    "endCharIndex": 6
                },
                {
                    "entityName": "Device",
                    "startCharIndex": 12,
                    "endCharIndex": 17
                }
            ]
        }
```

<span data-ttu-id="1f285-136">In this example, the `intentName` comes from the user request under the **Request** column heading in the CSV file, and the `entityName` comes from the other columns with key information.</span><span class="sxs-lookup"><span data-stu-id="1f285-136">In this example, the `intentName` comes from the user request under the **Request** column heading in the CSV file, and the `entityName` comes from the other columns with key information.</span></span> <span data-ttu-id="1f285-137">For example, if there's an entry for **Operation** or **Device**, and that string also occurs in the actual request, then it can be labeled as an entity.</span><span class="sxs-lookup"><span data-stu-id="1f285-137">For example, if there's an entry for **Operation** or **Device**, and that string also occurs in the actual request, then it can be labeled as an entity.</span></span> <span data-ttu-id="1f285-138">The following code demonstrates this parsing process.</span><span class="sxs-lookup"><span data-stu-id="1f285-138">The following code demonstrates this parsing process.</span></span> <span data-ttu-id="1f285-139">You can copy or [download](https://github.com/Microsoft/LUIS-Samples/blob/master/examples/build-app-programmatically-csv/_parse.js) it and save it to `_parse.js`.</span><span class="sxs-lookup"><span data-stu-id="1f285-139">You can copy or [download](https://github.com/Microsoft/LUIS-Samples/blob/master/examples/build-app-programmatically-csv/_parse.js) it and save it to `_parse.js`.</span></span>

   [!code-javascript[Node.js code for parsing a CSV file to extract intents, entities, and labeled utterances](~/samples-luis/examples/build-app-programmatically-csv/_parse.js)]



## <a name="create-the-luis-app"></a><span data-ttu-id="1f285-140">Create the LUIS app</span><span class="sxs-lookup"><span data-stu-id="1f285-140">Create the LUIS app</span></span>
<span data-ttu-id="1f285-141">Once the data has been parsed into JSON, add it to a LUIS app.</span><span class="sxs-lookup"><span data-stu-id="1f285-141">Once the data has been parsed into JSON, add it to a LUIS app.</span></span> <span data-ttu-id="1f285-142">The following code creates the LUIS app.</span><span class="sxs-lookup"><span data-stu-id="1f285-142">The following code creates the LUIS app.</span></span> <span data-ttu-id="1f285-143">Copy or [download](https://github.com/Microsoft/LUIS-Samples/blob/master/examples/build-app-programmatically-csv/_create.js) it, and save it into `_create.js`.</span><span class="sxs-lookup"><span data-stu-id="1f285-143">Copy or [download](https://github.com/Microsoft/LUIS-Samples/blob/master/examples/build-app-programmatically-csv/_create.js) it, and save it into `_create.js`.</span></span>

   [!code-javascript[Node.js code for creating a LUIS app](~/samples-luis/examples/build-app-programmatically-csv/_create.js)]


## <a name="add-intents"></a><span data-ttu-id="1f285-144">Add intents</span><span class="sxs-lookup"><span data-stu-id="1f285-144">Add intents</span></span>
<span data-ttu-id="1f285-145">Once you have an app, you need to intents to it.</span><span class="sxs-lookup"><span data-stu-id="1f285-145">Once you have an app, you need to intents to it.</span></span> <span data-ttu-id="1f285-146">The following code creates the LUIS app.</span><span class="sxs-lookup"><span data-stu-id="1f285-146">The following code creates the LUIS app.</span></span> <span data-ttu-id="1f285-147">Copy or [download](https://github.com/Microsoft/LUIS-Samples/blob/master/examples/build-app-programmatically-csv/_intents.js) it, and save it into `_intents.js`.</span><span class="sxs-lookup"><span data-stu-id="1f285-147">Copy or [download](https://github.com/Microsoft/LUIS-Samples/blob/master/examples/build-app-programmatically-csv/_intents.js) it, and save it into `_intents.js`.</span></span>

   [!code-javascript[Node.js code for creating a series of intents](~/samples-luis/examples/build-app-programmatically-csv/_intents.js)]


## <a name="add-entities"></a><span data-ttu-id="1f285-148">Add entities</span><span class="sxs-lookup"><span data-stu-id="1f285-148">Add entities</span></span>
<span data-ttu-id="1f285-149">The following code adds the entities to the LUIS app.</span><span class="sxs-lookup"><span data-stu-id="1f285-149">The following code adds the entities to the LUIS app.</span></span> <span data-ttu-id="1f285-150">Copy or [download](https://github.com/Microsoft/LUIS-Samples/blob/master/examples/build-app-programmatically-csv/_entities.js) it, and save it into `_entities.js`.</span><span class="sxs-lookup"><span data-stu-id="1f285-150">Copy or [download](https://github.com/Microsoft/LUIS-Samples/blob/master/examples/build-app-programmatically-csv/_entities.js) it, and save it into `_entities.js`.</span></span>

   [!code-javascript[Node.js code for creating entities](~/samples-luis/examples/build-app-programmatically-csv/_entities.js)]
   


## <a name="add-utterances"></a><span data-ttu-id="1f285-151">Add utterances</span><span class="sxs-lookup"><span data-stu-id="1f285-151">Add utterances</span></span>
<span data-ttu-id="1f285-152">Once the entities and intents have been defined in the LUIS app, you can add the utterances.</span><span class="sxs-lookup"><span data-stu-id="1f285-152">Once the entities and intents have been defined in the LUIS app, you can add the utterances.</span></span> <span data-ttu-id="1f285-153">The following code uses the [Utterances_AddBatch](https://westus.dev.cognitive.microsoft.com/docs/services/5890b47c39e2bb17b84a55ff/operations/5890b47c39e2bb052c5b9c09) API, which allows you to add up to 100 utterances at a time.</span><span class="sxs-lookup"><span data-stu-id="1f285-153">The following code uses the [Utterances_AddBatch](https://westus.dev.cognitive.microsoft.com/docs/services/5890b47c39e2bb17b84a55ff/operations/5890b47c39e2bb052c5b9c09) API, which allows you to add up to 100 utterances at a time.</span></span>  <span data-ttu-id="1f285-154">Copy or [download](https://github.com/Microsoft/LUIS-Samples/blob/master/examples/build-app-programmatically-csv/_upload.js) it, and save it into `_upload.js`.</span><span class="sxs-lookup"><span data-stu-id="1f285-154">Copy or [download](https://github.com/Microsoft/LUIS-Samples/blob/master/examples/build-app-programmatically-csv/_upload.js) it, and save it into `_upload.js`.</span></span>

   [!code-javascript[Node.js code for adding utterances](~/samples-luis/examples/build-app-programmatically-csv/_upload.js)]


## <a name="run-the-code"></a><span data-ttu-id="1f285-155">Run the code</span><span class="sxs-lookup"><span data-stu-id="1f285-155">Run the code</span></span>


### <a name="install-nodejs-dependencies"></a><span data-ttu-id="1f285-156">Install Node.js dependencies</span><span class="sxs-lookup"><span data-stu-id="1f285-156">Install Node.js dependencies</span></span>
<span data-ttu-id="1f285-157">Install the Node.js dependencies from NPM in the terminal/command line.</span><span class="sxs-lookup"><span data-stu-id="1f285-157">Install the Node.js dependencies from NPM in the terminal/command line.</span></span>

````
> npm install
````

### <a name="change-configuration-settings"></a><span data-ttu-id="1f285-158">Change Configuration Settings</span><span class="sxs-lookup"><span data-stu-id="1f285-158">Change Configuration Settings</span></span>
<span data-ttu-id="1f285-159">In order to use this application, you need to change the values in the index.js file to your own endpoint key, and provide the name you want the app to have.</span><span class="sxs-lookup"><span data-stu-id="1f285-159">In order to use this application, you need to change the values in the index.js file to your own endpoint key, and provide the name you want the app to have.</span></span> <span data-ttu-id="1f285-160">You can also set the app's culture or change the version number.</span><span class="sxs-lookup"><span data-stu-id="1f285-160">You can also set the app's culture or change the version number.</span></span>

<span data-ttu-id="1f285-161">Open the index.js file, and change these values at the top of the file.</span><span class="sxs-lookup"><span data-stu-id="1f285-161">Open the index.js file, and change these values at the top of the file.</span></span>


````JavaScript
// Change these values
const LUIS_programmaticKey = "YOUR_PROGRAMMATIC_KEY";
const LUIS_appName = "Sample App";
const LUIS_appCulture = "en-us"; 
const LUIS_versionId = "0.1";
````
### <a name="run-the-script"></a><span data-ttu-id="1f285-162">Run the script</span><span class="sxs-lookup"><span data-stu-id="1f285-162">Run the script</span></span>
<span data-ttu-id="1f285-163">Run the script from a terminal/command line with Node.js.</span><span class="sxs-lookup"><span data-stu-id="1f285-163">Run the script from a terminal/command line with Node.js.</span></span>

````
> node index.js
````
<span data-ttu-id="1f285-164">or</span><span class="sxs-lookup"><span data-stu-id="1f285-164">or</span></span>
````
> npm start
````

### <a name="application-progress"></a><span data-ttu-id="1f285-165">Application progress</span><span class="sxs-lookup"><span data-stu-id="1f285-165">Application progress</span></span>
<span data-ttu-id="1f285-166">While the application is running, the command line shows progress.</span><span class="sxs-lookup"><span data-stu-id="1f285-166">While the application is running, the command line shows progress.</span></span> <span data-ttu-id="1f285-167">The command line output includes the format of the responses from LUIS.</span><span class="sxs-lookup"><span data-stu-id="1f285-167">The command line output includes the format of the responses from LUIS.</span></span>

````
> node index.js
intents: ["TurnOn","TurnOff","Dim","Other"]
entities: ["Operation","Device","Room"]
parse done
JSON file should contain utterances. Next step is to create an app with the intents and entities it found.
Called createApp, created app with ID 314b306c-0033-4e09-92ab-94fe5ed158a2
Called addIntents for intent named TurnOn.
Called addIntents for intent named TurnOff.
Called addIntents for intent named Dim.
Called addIntents for intent named Other.
Results of all calls to addIntent = [{"response":"e7eaf224-8c61-44ed-a6b0-2ab4dc56f1d0"},{"response":"a8a17efd-f01c-488d-ad44-a31a818cf7d7"},{"response":"bc7c32fc-14a0-4b72-bad4-d345d807f965"},{"response":"727a8d73-cd3b-4096-bc8d-d7cfba12eb44"}]
called addEntity for entity named Operation.
called addEntity for entity named Device.
called addEntity for entity named Room.
Results of all calls to addEntity= [{"response":"6a7e914f-911d-4c6c-a5bc-377afdce4390"},{"response":"56c35237-593d-47f6-9d01-2912fa488760"},{"response":"f1dd440c-2ce3-4a20-a817-a57273f169f3"}]
retrying add examples...

Results of add utterances = [{"response":[{"value":{"UtteranceText":"turn on the lights","ExampleId":-67649},"hasError":false},{"value":{"UtteranceText":"turn the heat on","ExampleId":-69067},"hasError":false},{"value":{"UtteranceText":"switch on the kitchen fan","ExampleId":-3395901},"hasError":false},{"value":{"UtteranceText":"turn off bedroom lights","ExampleId":-85402},"hasError":false},{"value":{"UtteranceText":"turn off air conditioning","ExampleId":-8991572},"hasError":false},{"value":{"UtteranceText":"kill the lights","ExampleId":-70124},"hasError":false},{"value":{"UtteranceText":"dim the lights","ExampleId":-174358},"hasError":false},{"value":{"UtteranceText":"hi how are you","ExampleId":-143722},"hasError":false},{"value":{"UtteranceText":"answer the phone","ExampleId":-69939},"hasError":false},{"value":{"UtteranceText":"are you there","ExampleId":-149588},"hasError":false},{"value":{"UtteranceText":"help","ExampleId":-81949},"hasError":false},{"value":{"UtteranceText":"testing the circuit","ExampleId":-11548708},"hasError":false}]}]
upload done
````




## <a name="open-the-luis-app"></a><span data-ttu-id="1f285-168">Open the LUIS app</span><span class="sxs-lookup"><span data-stu-id="1f285-168">Open the LUIS app</span></span>
<span data-ttu-id="1f285-169">Once the script completes, you can log in to [LUIS](luis-reference-regions.md) and see the LUIS app you created under **My Apps**.</span><span class="sxs-lookup"><span data-stu-id="1f285-169">Once the script completes, you can log in to [LUIS](luis-reference-regions.md) and see the LUIS app you created under **My Apps**.</span></span> <span data-ttu-id="1f285-170">You should be able to see the utterances you added under the **TurnOn**, **TurnOff**, and **None** intents.</span><span class="sxs-lookup"><span data-stu-id="1f285-170">You should be able to see the utterances you added under the **TurnOn**, **TurnOff**, and **None** intents.</span></span>

![TurnOn intent](./media/luis-tutorial-node-import-utterances-csv/imported-utterances-661.png)


## <a name="next-steps"></a><span data-ttu-id="1f285-172">Next steps</span><span class="sxs-lookup"><span data-stu-id="1f285-172">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1f285-173">Test and train your app in LUIS website</span><span class="sxs-lookup"><span data-stu-id="1f285-173">Test and train your app in LUIS website</span></span>](luis-interactive-test.md)

## <a name="additional-resources"></a><span data-ttu-id="1f285-174">Additional resources</span><span class="sxs-lookup"><span data-stu-id="1f285-174">Additional resources</span></span>

<span data-ttu-id="1f285-175">This sample application uses the following LUIS APIs:</span><span class="sxs-lookup"><span data-stu-id="1f285-175">This sample application uses the following LUIS APIs:</span></span>
- [<span data-ttu-id="1f285-176">create app</span><span class="sxs-lookup"><span data-stu-id="1f285-176">create app</span></span>](https://westus.dev.cognitive.microsoft.com/docs/services/5890b47c39e2bb17b84a55ff/operations/5890b47c39e2bb052c5b9c36)
- [<span data-ttu-id="1f285-177">add intents</span><span class="sxs-lookup"><span data-stu-id="1f285-177">add intents</span></span>](https://westus.dev.cognitive.microsoft.com/docs/services/5890b47c39e2bb17b84a55ff/operations/5890b47c39e2bb052c5b9c0c)
- [<span data-ttu-id="1f285-178">add entities</span><span class="sxs-lookup"><span data-stu-id="1f285-178">add entities</span></span>](https://westus.dev.cognitive.microsoft.com/docs/services/5890b47c39e2bb17b84a55ff/operations/5890b47c39e2bb052c5b9c0e) 
- [<span data-ttu-id="1f285-179">add utterances</span><span class="sxs-lookup"><span data-stu-id="1f285-179">add utterances</span></span>](https://westus.dev.cognitive.microsoft.com/docs/services/5890b47c39e2bb17b84a55ff/operations/5890b47c39e2bb052c5b9c09)