---
title: Analyze natural language text in Language Understanding (LUIS) using GO - Azure Cognitive Services | Microsoft Docs
description: In this quickstart, use an available public LUIS app to determine a user's intention from conversational text. Using GO, send the user's intention as text to the public app's HTTP prediction endpoint. At the endpoint, LUIS applies the public app's model to analyze the natural language text for meaning, determining overall intent and extracting data relevant to the app's subject domain.
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: quickstart
ms.date: 08/23/2018
ms.author: diberry
ms.openlocfilehash: b00d815b712d98136b474d1e73afe7e35d1c7ef4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855612"
---
# <a name="quickstart-call-a-luis-endpoint-using-go"></a><span data-ttu-id="e2b4f-105">Quickstart: Call a LUIS endpoint using Go</span><span class="sxs-lookup"><span data-stu-id="e2b4f-105">Quickstart: Call a LUIS endpoint using Go</span></span>

[!INCLUDE [Quickstart introduction for endpoint](../../../includes/cognitive-services-luis-qs-endpoint-intro-para.md)]

## <a name="prerequisites"></a><span data-ttu-id="e2b4f-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e2b4f-106">Prerequisites</span></span>

* <span data-ttu-id="e2b4f-107">[Go](https://golang.org/) programming language</span><span class="sxs-lookup"><span data-stu-id="e2b4f-107">[Go](https://golang.org/) programming language</span></span>  
* [<span data-ttu-id="e2b4f-108">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="e2b4f-108">Visual Studio Code</span></span>](https://code.visualstudio.com/)
* <span data-ttu-id="e2b4f-109">Public app ID: df67dcdb-c37d-46af-88e1-8b97951ca1c2</span><span class="sxs-lookup"><span data-stu-id="e2b4f-109">Public app ID: df67dcdb-c37d-46af-88e1-8b97951ca1c2</span></span>

[!INCLUDE [Use authoring key for endpoint](../../../includes/cognitive-services-luis-qs-endpoint-luis-repo-note.md)]

## <a name="get-luis-key"></a><span data-ttu-id="e2b4f-110">Get LUIS key</span><span class="sxs-lookup"><span data-stu-id="e2b4f-110">Get LUIS key</span></span>

[!INCLUDE [Use authoring key for endpoint](../../../includes/cognitive-services-luis-qs-endpoint-get-key-para.md)]

## <a name="analyze-text-with-browser"></a><span data-ttu-id="e2b4f-111">Analyze text with browser</span><span class="sxs-lookup"><span data-stu-id="e2b4f-111">Analyze text with browser</span></span>

[!INCLUDE [Use authoring key for endpoint](../../../includes/cognitive-services-luis-qs-endpoint-browser-para.md)]

## <a name="analyze-text-with-go"></a><span data-ttu-id="e2b4f-112">Analyze text with Go</span><span class="sxs-lookup"><span data-stu-id="e2b4f-112">Analyze text with Go</span></span>

<span data-ttu-id="e2b4f-113">You can use Go to access the same results you saw in the browser window in the previous step.</span><span class="sxs-lookup"><span data-stu-id="e2b4f-113">You can use Go to access the same results you saw in the browser window in the previous step.</span></span> 

1. <span data-ttu-id="e2b4f-114">Create a new file named `endpoint.go`.</span><span class="sxs-lookup"><span data-stu-id="e2b4f-114">Create a new file named `endpoint.go`.</span></span> <span data-ttu-id="e2b4f-115">Add the following code:</span><span class="sxs-lookup"><span data-stu-id="e2b4f-115">Add the following code:</span></span>
    
   [!code-go[Go code that calls a LUIS endpoint](~/samples-luis/documentation-samples/quickstarts/analyze-text/go/endpoint.go?range=36-98)]

2. <span data-ttu-id="e2b4f-116">With a command prompt in the same directory as where you created the file, enter `go build endpoint.go` to compile the Go file.</span><span class="sxs-lookup"><span data-stu-id="e2b4f-116">With a command prompt in the same directory as where you created the file, enter `go build endpoint.go` to compile the Go file.</span></span> <span data-ttu-id="e2b4f-117">The command prompt does not return any information for a successful build.</span><span class="sxs-lookup"><span data-stu-id="e2b4f-117">The command prompt does not return any information for a successful build.</span></span>

3. <span data-ttu-id="e2b4f-118">Run the Go application from the command line by entering the following text in the command prompt:</span><span class="sxs-lookup"><span data-stu-id="e2b4f-118">Run the Go application from the command line by entering the following text in the command prompt:</span></span> 

    ```CMD
    go run endpoint.go -appID df67dcdb-c37d-46af-88e1-8b97951ca1c2 -endpointKey <add-your-key> -region westus
    ```
    
    <span data-ttu-id="e2b4f-119">Replace `<add-your-key>` with the value of your key.</span><span class="sxs-lookup"><span data-stu-id="e2b4f-119">Replace `<add-your-key>` with the value of your key.</span></span>  
    
    <span data-ttu-id="e2b4f-120">The command prompt response is:</span><span class="sxs-lookup"><span data-stu-id="e2b4f-120">The command prompt response is:</span></span> 
    
    ```CMD
    appID has value df67dcdb-c37d-46af-88e1-8b97951ca1c2
    endpointKey has value xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
    region has value westus
    utterance has value turn on the bedroom light
    response
    {
        "query": "turn on the bedroom light",
        "topScoringIntent": {
            "intent": "HomeAutomation.TurnOn",
            "score": 0.809439957
        },
        "entities": [
            {
            "entity": "bedroom",
            "type": "HomeAutomation.Room",
            "startIndex": 12,
            "endIndex": 18,
            "score": 0.8065475
            }
        ]
    }
    ```
    
## <a name="luis-keys"></a><span data-ttu-id="e2b4f-121">LUIS keys</span><span class="sxs-lookup"><span data-stu-id="e2b4f-121">LUIS keys</span></span>

[!INCLUDE [Use authoring key for endpoint](../../../includes/cognitive-services-luis-qs-endpoint-key-usage-para.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="e2b4f-122">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="e2b4f-122">Clean up resources</span></span>
<span data-ttu-id="e2b4f-123">Close the Go file and remove it from the file system.</span><span class="sxs-lookup"><span data-stu-id="e2b4f-123">Close the Go file and remove it from the file system.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="e2b4f-124">Next steps</span><span class="sxs-lookup"><span data-stu-id="e2b4f-124">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="e2b4f-125">Add utterances</span><span class="sxs-lookup"><span data-stu-id="e2b4f-125">Add utterances</span></span>](luis-get-started-go-add-utterance.md)