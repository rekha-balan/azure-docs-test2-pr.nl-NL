---
title: Quickstart change model and train LUIS app using Go - Azure Cognitive Services | Microsoft Docs
description: In this Go quickstart, add example utterances to a Home Automation app and train the app. Example utterances are conversational user text mapped to an intent. By providing example utterances for intents, you teach LUIS what kinds of user-supplied text belongs to which intent.
titleSuffix: Microsoft Cognitive Services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: quickstart
ms.date: 08/24/2018
ms.author: diberry
ms.openlocfilehash: da57a7e46cccbf0a9b34b3961a831e7982160e6b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867937"
---
# <a name="quickstart-change-model-using-go"></a><span data-ttu-id="37765-105">Quickstart: Change model using Go</span><span class="sxs-lookup"><span data-stu-id="37765-105">Quickstart: Change model using Go</span></span>

[!INCLUDE [Quickstart introduction for endpoint](../../../includes/cognitive-services-luis-qs-endpoint-intro-para.md)]

## <a name="prerequisites"></a><span data-ttu-id="37765-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="37765-106">Prerequisites</span></span>

[!INCLUDE [Quickstart introduction for endpoint](../../../includes/cognitive-services-luis-qs-change-model-prereq.md)]
* <span data-ttu-id="37765-107">[Go](https://golang.org/) programming language installed.</span><span class="sxs-lookup"><span data-stu-id="37765-107">[Go](https://golang.org/) programming language installed.</span></span>
* [<span data-ttu-id="37765-108">VSCode</span><span class="sxs-lookup"><span data-stu-id="37765-108">VSCode</span></span>](https://code.visualstudio.com) 

[!INCLUDE [Quickstart introduction for endpoint](../../../includes/cognitive-services-luis-qs-change-model-luis-repo-note.md)]

## <a name="example-utterances-json-file"></a><span data-ttu-id="37765-109">Example utterances JSON file</span><span class="sxs-lookup"><span data-stu-id="37765-109">Example utterances JSON file</span></span>

[!INCLUDE [Quickstart introduction for endpoint](../../../includes/cognitive-services-luis-qs-change-model-json-ex-utt.md)]

## <a name="create-quickstart-code"></a><span data-ttu-id="37765-110">Create quickstart code</span><span class="sxs-lookup"><span data-stu-id="37765-110">Create quickstart code</span></span> 

1. <span data-ttu-id="37765-111">Create `add-utterances.go` with VSCode.</span><span class="sxs-lookup"><span data-stu-id="37765-111">Create `add-utterances.go` with VSCode.</span></span> 

2. <span data-ttu-id="37765-112">Add dependencies.</span><span class="sxs-lookup"><span data-stu-id="37765-112">Add dependencies.</span></span> 

   [!code-go[Add dependencies.](~/samples-luis/documentation-samples/quickstarts/change-model/go/add-utterances.go?range=2-10 "Add dependencies.")]

3. <span data-ttu-id="37765-113">Add generic HTTP request function, which includes passing authoring key in header.</span><span class="sxs-lookup"><span data-stu-id="37765-113">Add generic HTTP request function, which includes passing authoring key in header.</span></span> 

   [!code-go[Add HTTP request function which includes passing authoring key in header. ](~/samples-luis/documentation-samples/quickstarts/change-model/go/add-utterances.go?range=12-36 "Add HTTP request function, which includes passing authoring key in header. ")]

4. <span data-ttu-id="37765-114">Add example utterances from JSON file.</span><span class="sxs-lookup"><span data-stu-id="37765-114">Add example utterances from JSON file.</span></span>

   [!code-go[Add example utterances from JSON file.](~/samples-luis/documentation-samples/quickstarts/change-model/go/add-utterances.go?range=62-76 "Add example utterances from JSON file.")]

5. <span data-ttu-id="37765-115">Request training.</span><span class="sxs-lookup"><span data-stu-id="37765-115">Request training.</span></span> <span data-ttu-id="37765-116">Uses a helper function to set the VERB for the same route as training status.</span><span class="sxs-lookup"><span data-stu-id="37765-116">Uses a helper function to set the VERB for the same route as training status.</span></span> 

   [!code-go[Request training. ](~/samples-luis/documentation-samples/quickstarts/change-model/go/add-utterances.go?range=77-86 "Request training. ")]

6. <span data-ttu-id="37765-117">Request training status.</span><span class="sxs-lookup"><span data-stu-id="37765-117">Request training status.</span></span> <span data-ttu-id="37765-118">Uses a helper function to set the VERB for the same route as request training.</span><span class="sxs-lookup"><span data-stu-id="37765-118">Uses a helper function to set the VERB for the same route as request training.</span></span> 

   [!code-go[Request training status. ](~/samples-luis/documentation-samples/quickstarts/change-model/go/add-utterances.go?range=87-90 "Request training status. ")]

7. <span data-ttu-id="37765-119">Add main function to handle command-line parsing.</span><span class="sxs-lookup"><span data-stu-id="37765-119">Add main function to handle command-line parsing.</span></span>

   [!code-go[Add main function to handle command line parsing. ](~/samples-luis/documentation-samples/quickstarts/change-model/go/add-utterances.go?range=38-60 "Add main function to handle command-line parsing.")]

## <a name="add-an-utterance-from-the-command-line-train-and-get-status"></a><span data-ttu-id="37765-120">Add an utterance from the command line, train, and get status</span><span class="sxs-lookup"><span data-stu-id="37765-120">Add an utterance from the command line, train, and get status</span></span>

1. <span data-ttu-id="37765-121">From a command prompt in the directory where you created the Go file, enter `go build add-utterances.go` to compile the Go file.</span><span class="sxs-lookup"><span data-stu-id="37765-121">From a command prompt in the directory where you created the Go file, enter `go build add-utterances.go` to compile the Go file.</span></span> <span data-ttu-id="37765-122">The command prompt does not return any information for a successful build.</span><span class="sxs-lookup"><span data-stu-id="37765-122">The command prompt does not return any information for a successful build.</span></span>

2. <span data-ttu-id="37765-123">Run the Go application from the command line by entering the following text in the command prompt:</span><span class="sxs-lookup"><span data-stu-id="37765-123">Run the Go application from the command line by entering the following text in the command prompt:</span></span> 

    ```CMD
    add-utterances -appID <your-app-id> -authoringKey <add-your-authoring-key> -version <your-version-id> -region westus -utteranceFile utterances.json

    ```

    <span data-ttu-id="37765-124">Replace `<add-your-authoring-key>` with the value of your authoring key (also known as the starter key).</span><span class="sxs-lookup"><span data-stu-id="37765-124">Replace `<add-your-authoring-key>` with the value of your authoring key (also known as the starter key).</span></span> <span data-ttu-id="37765-125">Replace `<your-app-id>` with the value of your app ID.</span><span class="sxs-lookup"><span data-stu-id="37765-125">Replace `<your-app-id>` with the value of your app ID.</span></span> <span data-ttu-id="37765-126">Replace `<your-version-id>` with the value of your version.</span><span class="sxs-lookup"><span data-stu-id="37765-126">Replace `<your-version-id>` with the value of your version.</span></span> <span data-ttu-id="37765-127">Default version is `0.1`.</span><span class="sxs-lookup"><span data-stu-id="37765-127">Default version is `0.1`.</span></span>

    <span data-ttu-id="37765-128">This command-prompt displays the results:</span><span class="sxs-lookup"><span data-stu-id="37765-128">This command-prompt displays the results:</span></span>

    ```CMD
    add example utterances requested
    [
        {
            "text": "go lang 1",
            "intentName": "None",
            "entityLabels": []
        }
    ,
        {
            "text": "go lang 2",
            "intentName": "None",
            "entityLabels": []
        }
    ]
    201
    [
        {
            "value": {
                "ExampleId": 77783998,
                "UtteranceText": "go lang 1"
            },
            "hasError": false
        },
        {
            "value": {
                "ExampleId": 77783999,
                "UtteranceText": "go lang 2"
            },
            "hasError": false
        }
    ]
    training selected
    202
    {"statusId":9,"status":"Queued"}
    training status selected
    200
    [
        {
            "modelId": "c52d6509-9261-459e-90bc-b3c872ee4a4b",
            "details": {
                "statusId": 3,
                "status": "InProgress",
                "exampleCount": 24
            }
        },
        {
            "modelId": "5119cbe8-97a1-4c1f-85e6-6449f3a38d77",
            "details": {
                "statusId": 3,
                "status": "InProgress",
                "exampleCount": 24
            }
        },
        {
            "modelId": "01e6b6bc-9872-47f9-8a52-da510cddfafe",
            "details": {
                "statusId": 3,
                "status": "InProgress",
                "exampleCount": 24
            }
        },
        {
            "modelId": "33b409b2-32b0-4b0c-9e91-31c6cfaf93fb",
            "details": {
                "statusId": 3,
                "status": "InProgress",
                "exampleCount": 24
            }
        },
        {
            "modelId": "1fb210be-2a19-496d-bb72-e0c2dd35cbc1",
            "details": {
                "statusId": 3,
                "status": "InProgress",
                "exampleCount": 24
            }
        },
        {
            "modelId": "3d098beb-a1aa-423f-a0ae-ce08ced216d6",
            "details": {
                "statusId": 3,
                "status": "InProgress",
                "exampleCount": 24
            }
        },
        {
            "modelId": "cce854f8-8f8f-4ed9-a7df-44dfea562f62",
            "details": {
                "statusId": 3,
                "status": "InProgress",
                "exampleCount": 24
            }
        },
        {
            "modelId": "4d97bf0d-5213-4502-9712-2d6e77c96045",
            "details": {
                "statusId": 3,
                "status": "InProgress",
                "exampleCount": 24
            }
        }
    ]
    ```

    <span data-ttu-id="37765-129">This response includes the HTTP status code for each of the three HTTP calls as well as any JSON response returned in the body of the response.</span><span class="sxs-lookup"><span data-stu-id="37765-129">This response includes the HTTP status code for each of the three HTTP calls as well as any JSON response returned in the body of the response.</span></span> 

## <a name="clean-up-resources"></a><span data-ttu-id="37765-130">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="37765-130">Clean up resources</span></span>
<span data-ttu-id="37765-131">When you are done with the quickstart, remove all the files created in this quickstart.</span><span class="sxs-lookup"><span data-stu-id="37765-131">When you are done with the quickstart, remove all the files created in this quickstart.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="37765-132">Next steps</span><span class="sxs-lookup"><span data-stu-id="37765-132">Next steps</span></span>
> [!div class="nextstepaction"] 
> [<span data-ttu-id="37765-133">Build an app with a custom domain</span><span class="sxs-lookup"><span data-stu-id="37765-133">Build an app with a custom domain</span></span>](luis-quickstart-intents-only.md) 