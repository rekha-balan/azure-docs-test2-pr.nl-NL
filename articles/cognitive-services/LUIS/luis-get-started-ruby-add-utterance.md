---
title: Quickstart change model and train LUIS app using Ruby - Azure Cognitive Services | Microsoft Docs
description: In this Ruby quickstart, add example utterances to a Home Automation app and train the app. Example utterances are conversational user text mapped to an intent. By providing example utterances for intents, you teach LUIS what kinds of user-supplied text belongs to which intent.
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: quickstart
ms.date: 08/24/2018
ms.author: diberry
ms.openlocfilehash: 537ebe2d008e313d2fb29d05143804c3478567e8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855978"
---
# <a name="quickstart-change-model-using-ruby"></a><span data-ttu-id="c0be6-105">Quickstart: Change model using Ruby</span><span class="sxs-lookup"><span data-stu-id="c0be6-105">Quickstart: Change model using Ruby</span></span>

[!INCLUDE [Quickstart introduction for change model](../../../includes/cognitive-services-luis-qs-endpoint-intro-para.md)]

## <a name="prerequisites"></a><span data-ttu-id="c0be6-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="c0be6-106">Prerequisites</span></span>

[!INCLUDE [Quickstart prerequisites for changing model](../../../includes/cognitive-services-luis-qs-change-model-prereq.md)]
* [<span data-ttu-id="c0be6-107">Ruby</span><span class="sxs-lookup"><span data-stu-id="c0be6-107">Ruby</span></span>](http://rubyinstaller.org/) 
* [<span data-ttu-id="c0be6-108">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="c0be6-108">Visual Studio Code</span></span>](https://code.visualstudio.com/)

[!INCLUDE [Code is available in LUIS-Samples Github repo](../../../includes/cognitive-services-luis-qs-change-model-luis-repo-note.md)]

## <a name="example-utterances-json-file"></a><span data-ttu-id="c0be6-109">Example utterances JSON file</span><span class="sxs-lookup"><span data-stu-id="c0be6-109">Example utterances JSON file</span></span>

[!INCLUDE [Quickstart explanation of example utterance JSON file](../../../includes/cognitive-services-luis-qs-change-model-json-ex-utt.md)]

## <a name="create-quickstart-code"></a><span data-ttu-id="c0be6-110">Create quickstart code</span><span class="sxs-lookup"><span data-stu-id="c0be6-110">Create quickstart code</span></span> 

<span data-ttu-id="c0be6-111">Add the dependencies to the file named `add-utterances.rb`.</span><span class="sxs-lookup"><span data-stu-id="c0be6-111">Add the dependencies to the file named `add-utterances.rb`.</span></span>

   [!code-ruby[Ruby and LUIS Dependencies](~/samples-luis/documentation-samples/quickstarts/change-model/ruby/add-utterances.rb?range=1-21 "Ruby and LUIS Dependencies")]

<span data-ttu-id="c0be6-112">Add the GET request used for training status.</span><span class="sxs-lookup"><span data-stu-id="c0be6-112">Add the GET request used for training status.</span></span>

   [!code-ruby[SendGet](~/samples-luis/documentation-samples/quickstarts/change-model/ruby/add-utterances.rb?range=23-33 "SendGet")]

<span data-ttu-id="c0be6-113">Add the POST request used to create utterances or start training.</span><span class="sxs-lookup"><span data-stu-id="c0be6-113">Add the POST request used to create utterances or start training.</span></span> 

   [!code-ruby[SendPost](~/samples-luis/documentation-samples/quickstarts/change-model/ruby/add-utterances.rb?range=35-47 "SendPost")]

<span data-ttu-id="c0be6-114">Add the `AddUtterances` function.</span><span class="sxs-lookup"><span data-stu-id="c0be6-114">Add the `AddUtterances` function.</span></span>

   [!code-ruby[AddUtterances method](~/samples-luis/documentation-samples/quickstarts/change-model/ruby/add-utterances.rb?range=49-54 "AddUtterances method")]


<span data-ttu-id="c0be6-115">Add the `Train` function.</span><span class="sxs-lookup"><span data-stu-id="c0be6-115">Add the `Train` function.</span></span> 

   [!code-ruby[Train](~/samples-luis/documentation-samples/quickstarts/change-model/ruby/add-utterances.rb?range=56-62 "Train")]

<span data-ttu-id="c0be6-116">Add the `Status` function.</span><span class="sxs-lookup"><span data-stu-id="c0be6-116">Add the `Status` function.</span></span>

   [!code-ruby[Status](~/samples-luis/documentation-samples/quickstarts/change-model/ruby/add-utterances.rb?range=64-68 "Status")]

<span data-ttu-id="c0be6-117">To manage arguments, add the main code.</span><span class="sxs-lookup"><span data-stu-id="c0be6-117">To manage arguments, add the main code.</span></span>

   [!code-ruby[Main code](~/samples-luis/documentation-samples/quickstarts/change-model/ruby/add-utterances.rb?range=70-72 "Main code")]

## <a name="run-code"></a><span data-ttu-id="c0be6-118">Run code</span><span class="sxs-lookup"><span data-stu-id="c0be6-118">Run code</span></span>

<span data-ttu-id="c0be6-119">Run the application from a command line with Ruby.</span><span class="sxs-lookup"><span data-stu-id="c0be6-119">Run the application from a command line with Ruby.</span></span>

### <a name="add-an-utterance-from-the-command-line"></a><span data-ttu-id="c0be6-120">Add an utterance from the command line</span><span class="sxs-lookup"><span data-stu-id="c0be6-120">Add an utterance from the command line</span></span>

<span data-ttu-id="c0be6-121">Calling `add-utterances.rb` adds the utterances, trains, and gets training status.</span><span class="sxs-lookup"><span data-stu-id="c0be6-121">Calling `add-utterances.rb` adds the utterances, trains, and gets training status.</span></span>

```CMD
> ruby add-utterances.rb 
```

<span data-ttu-id="c0be6-122">This result displays the results from calling the add utterances API.</span><span class="sxs-lookup"><span data-stu-id="c0be6-122">This result displays the results from calling the add utterances API.</span></span> <span data-ttu-id="c0be6-123">The `response` field is in this format for utterances that was added.</span><span class="sxs-lookup"><span data-stu-id="c0be6-123">The `response` field is in this format for utterances that was added.</span></span> <span data-ttu-id="c0be6-124">The `hasError` is false, indicating the utterance was added.</span><span class="sxs-lookup"><span data-stu-id="c0be6-124">The `hasError` is false, indicating the utterance was added.</span></span>  

```json
    "response": [
        {
            "value": {
                "UtteranceText": "go to seattle",
                "ExampleId": -5123383
            },
            "hasError": false
        },
        {
            "value": {
                "UtteranceText": "book a flight",
                "ExampleId": -169157
            },
            "hasError": false
        }
    ]
```

<span data-ttu-id="c0be6-125">The next response show the training queued.</span><span class="sxs-lookup"><span data-stu-id="c0be6-125">The next response show the training queued.</span></span> <span data-ttu-id="c0be6-126">Then the next response shows the status of each intent.</span><span class="sxs-lookup"><span data-stu-id="c0be6-126">Then the next response shows the status of each intent.</span></span> 

```
Requested training status.
[
   {
      "modelId": "eb2f117c-e10a-463e-90ea-1a0176660acc",
      "details": {
         "statusId": 0,
         "status": "Success",
         "exampleCount": 33,
         "trainingDateTime": "2017-11-20T18:09:11Z"
      }
   },
   {
      "modelId": "c1bdfbfc-e110-402e-b0cc-2af4112289fb",
      "details": {
         "statusId": 0,
         "status": "Success",
         "exampleCount": 33,
         "trainingDateTime": "2017-11-20T18:09:11Z"
      }
   },
   {
      "modelId": "863023ec-2c96-4d68-9c44-34c1cbde8bc9",
      "details": {
         "statusId": 0,
         "status": "Success",
         "exampleCount": 33,
         "trainingDateTime": "2017-11-20T18:09:11Z"
      }
   },
   {
      "modelId": "82702162-73ba-4ae9-a6f6-517b5244c555",
      "details": {
         "statusId": 0,
         "status": "Success",
         "exampleCount": 33,
         "trainingDateTime": "2017-11-20T18:09:11Z"
      }
   },
   {
      "modelId": "37121f4c-4853-467f-a9f3-6dfc8cad2763",
      "details": {
         "statusId": 0,
         "status": "Success",
         "exampleCount": 33,
         "trainingDateTime": "2017-11-20T18:09:11Z"
      }
   },
   {
      "modelId": "de421482-753e-42f5-a765-ad0a60f50d69",
      "details": {
         "statusId": 0,
         "status": "Success",
         "exampleCount": 33,
         "trainingDateTime": "2017-11-20T18:09:11Z"
      }
   },
   {
      "modelId": "80f58a45-86f2-4e18-be3d-b60a2c88312e",
      "details": {
         "statusId": 0,
         "status": "Success",
         "exampleCount": 33,
         "trainingDateTime": "2017-11-20T18:09:11Z"
      }
   },
   {
      "modelId": "c9eb9772-3b18-4d5f-a1e6-e0c31f91b390",
      "details": {
         "statusId": 0,
         "status": "Success",
         "exampleCount": 33,
         "trainingDateTime": "2017-11-20T18:09:11Z"
      }
   },
   {
      "modelId": "2afec2ff-7c01-4423-bb0e-e5f6935afae8",
      "details": {
         "statusId": 0,
         "status": "Success",
         "exampleCount": 33,
         "trainingDateTime": "2017-11-20T18:09:11Z"
      }
   },
   {
      "modelId": "95a81c87-0d7b-4251-8e07-f28d180886a1",
      "details": {
         "statusId": 0,
         "status": "Success",
         "exampleCount": 33,
         "trainingDateTime": "2017-11-20T18:09:11Z"
      }
   }
]
```

## <a name="clean-up-resources"></a><span data-ttu-id="c0be6-127">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="c0be6-127">Clean up resources</span></span>
<span data-ttu-id="c0be6-128">When you are done with the quickstart, remove all the files created in this quickstart.</span><span class="sxs-lookup"><span data-stu-id="c0be6-128">When you are done with the quickstart, remove all the files created in this quickstart.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="c0be6-129">Next steps</span><span class="sxs-lookup"><span data-stu-id="c0be6-129">Next steps</span></span>
> [!div class="nextstepaction"] 
> [<span data-ttu-id="c0be6-130">Build a LUIS app programmatically</span><span class="sxs-lookup"><span data-stu-id="c0be6-130">Build a LUIS app programmatically</span></span>](luis-tutorial-node-import-utterances-csv.md)