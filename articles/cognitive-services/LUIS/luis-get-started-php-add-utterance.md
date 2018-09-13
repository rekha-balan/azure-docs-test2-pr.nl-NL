---
title: Quickstart change model and train LUIS app using PHP - Azure Cognitive Services | Microsoft Docs
description: In this PHP quickstart, add example utterances to a Home Automation app and train the app. Example utterances are conversational user text mapped to an intent. By providing example utterances for intents, you teach LUIS what kinds of user-supplied text belongs to which intent.
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: quickstart
ms.date: 08/24/2018
ms.author: diberry
ms.openlocfilehash: 31840f34b99bbb474776ce81a7f87df94a0e338e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868844"
---
# <a name="quickstart-change-model-using-php"></a><span data-ttu-id="255e4-105">Quickstart: Change model using PHP</span><span class="sxs-lookup"><span data-stu-id="255e4-105">Quickstart: Change model using PHP</span></span> 

[!INCLUDE [Quickstart introduction for change model](../../../includes/cognitive-services-luis-qs-endpoint-intro-para.md)]

## <a name="prerequisites"></a><span data-ttu-id="255e4-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="255e4-106">Prerequisites</span></span>

[!INCLUDE [Quickstart prerequisites for changing model](../../../includes/cognitive-services-luis-qs-change-model-prereq.md)]
* <span data-ttu-id="255e4-107">Latest [**PHP**](http://php.net/).</span><span class="sxs-lookup"><span data-stu-id="255e4-107">Latest [**PHP**](http://php.net/).</span></span>
* <span data-ttu-id="255e4-108">Make sure openssl is available as a dependency for PHP.</span><span class="sxs-lookup"><span data-stu-id="255e4-108">Make sure openssl is available as a dependency for PHP.</span></span>  

[!INCLUDE [Code is available in LUIS-Samples Github repo](../../../includes/cognitive-services-luis-qs-change-model-luis-repo-note.md)]

## <a name="example-utterances-json-file"></a><span data-ttu-id="255e4-109">Example utterances JSON file</span><span class="sxs-lookup"><span data-stu-id="255e4-109">Example utterances JSON file</span></span>

[!INCLUDE [Quickstart explanation of example utterance JSON file](../../../includes/cognitive-services-luis-qs-change-model-json-ex-utt.md)]

## <a name="create-quickstart-code"></a><span data-ttu-id="255e4-110">Create quickstart code</span><span class="sxs-lookup"><span data-stu-id="255e4-110">Create quickstart code</span></span> 

<span data-ttu-id="255e4-111">Add the dependencies to the file named `add-utterances.php`.</span><span class="sxs-lookup"><span data-stu-id="255e4-111">Add the dependencies to the file named `add-utterances.php`.</span></span>

   [!code-php[PHP and LUIS Dependencies](~/samples-luis/documentation-samples/quickstarts/change-model/php/add-utterances.php?range=1-22 "PHP and LUIS Dependencies")]

<span data-ttu-id="255e4-112">Add the GET request used for training status.</span><span class="sxs-lookup"><span data-stu-id="255e4-112">Add the GET request used for training status.</span></span>

   [!code-php[SendGet](~/samples-luis/documentation-samples/quickstarts/change-model/php/add-utterances.php?range=24-43 "SendGet")]

<span data-ttu-id="255e4-113">Add the POST request used to create utterances or start training.</span><span class="sxs-lookup"><span data-stu-id="255e4-113">Add the POST request used to create utterances or start training.</span></span> 

   [!code-php[SendPost](~/samples-luis/documentation-samples/quickstarts/change-model/php/add-utterances.php?range=45-65 "SendPost")]

<span data-ttu-id="255e4-114">Add the `AddUtterances` function.</span><span class="sxs-lookup"><span data-stu-id="255e4-114">Add the `AddUtterances` function.</span></span>

   [!code-php[AddUtterances method](~/samples-luis/documentation-samples/quickstarts/change-model/php/add-utterances.php?range=67-72 "AddUtterances method")]


<span data-ttu-id="255e4-115">Add the `Train` function.</span><span class="sxs-lookup"><span data-stu-id="255e4-115">Add the `Train` function.</span></span> 

   [!code-php[Train](~/samples-luis/documentation-samples/quickstarts/change-model/php/add-utterances.php?range=74-81 "Train")]

<span data-ttu-id="255e4-116">Add the `Status` function.</span><span class="sxs-lookup"><span data-stu-id="255e4-116">Add the `Status` function.</span></span>

   [!code-php[Status](~/samples-luis/documentation-samples/quickstarts/change-model/php/add-utterances.php?range=83-87 "Status")]

<span data-ttu-id="255e4-117">To manage the command-line arguments, add the main code block.</span><span class="sxs-lookup"><span data-stu-id="255e4-117">To manage the command-line arguments, add the main code block.</span></span>

   [!code-php[Main code](~/samples-luis/documentation-samples/quickstarts/change-model/php/add-utterances.php?range=89-93 "Main code")]

## <a name="run-code"></a><span data-ttu-id="255e4-118">Run code</span><span class="sxs-lookup"><span data-stu-id="255e4-118">Run code</span></span>

<span data-ttu-id="255e4-119">Run the application from a command line with PHP.</span><span class="sxs-lookup"><span data-stu-id="255e4-119">Run the application from a command line with PHP.</span></span>

### <a name="add-an-utterance-from-the-command-line"></a><span data-ttu-id="255e4-120">Add an utterance from the command line</span><span class="sxs-lookup"><span data-stu-id="255e4-120">Add an utterance from the command line</span></span>

<span data-ttu-id="255e4-121">Run the application from a command line with PHP.</span><span class="sxs-lookup"><span data-stu-id="255e4-121">Run the application from a command line with PHP.</span></span>

<span data-ttu-id="255e4-122">Calling `add-utterances.php` adds the utterances, trains, and gets training status.</span><span class="sxs-lookup"><span data-stu-id="255e4-122">Calling `add-utterances.php` adds the utterances, trains, and gets training status.</span></span>

```CMD
> php add-utterances.php 
```

<span data-ttu-id="255e4-123">The following JSON is returned from the add utterances API call.</span><span class="sxs-lookup"><span data-stu-id="255e4-123">The following JSON is returned from the add utterances API call.</span></span> <span data-ttu-id="255e4-124">The `response` field is in this format for utterances that was added.</span><span class="sxs-lookup"><span data-stu-id="255e4-124">The `response` field is in this format for utterances that was added.</span></span> <span data-ttu-id="255e4-125">The `hasError` is false, indicating the utterance was added.</span><span class="sxs-lookup"><span data-stu-id="255e4-125">The `hasError` is false, indicating the utterance was added.</span></span>  

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

<span data-ttu-id="255e4-126">The following shows the result of a successful request to train:</span><span class="sxs-lookup"><span data-stu-id="255e4-126">The following shows the result of a successful request to train:</span></span>

```json
{
    "request": null,
    "response": {
        "statusId": 9,
        "status": "Queued"
    }
}
```


```JSON
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

## <a name="clean-up-resources"></a><span data-ttu-id="255e4-127">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="255e4-127">Clean up resources</span></span>

<span data-ttu-id="255e4-128">When you are done with the quickstart, remove all the files created in this quickstart.</span><span class="sxs-lookup"><span data-stu-id="255e4-128">When you are done with the quickstart, remove all the files created in this quickstart.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="255e4-129">Next steps</span><span class="sxs-lookup"><span data-stu-id="255e4-129">Next steps</span></span>
> [!div class="nextstepaction"] 
> [<span data-ttu-id="255e4-130">Build a LUIS app programmatically</span><span class="sxs-lookup"><span data-stu-id="255e4-130">Build a LUIS app programmatically</span></span>](luis-tutorial-node-import-utterances-csv.md)