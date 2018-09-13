---
title: Analyze natural language text in Language Understanding (LUIS) using Node.js - Cognitive Services - Azure Cognitive Services | Microsoft Docs
description: In this quickstart, use an available public LUIS app to determine a user's intention from conversational text. Using Node.js, send the user's intention as text to the public app's HTTP prediction endpoint. At the endpoint, LUIS applies the public app's model to analyze the natural language text for meaning, determining overall intent and extracting data relevant to the app's subject domain.
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: quickstart
ms.date: 08/23/2018
ms.author: diberry
ms.openlocfilehash: b85b8ef19d4cc46d80d600d1cb4404edd71e2374
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857339"
---
# <a name="quickstart-analyze-text-using-nodejs"></a><span data-ttu-id="88dec-105">Quickstart: Analyze text using Node.js</span><span class="sxs-lookup"><span data-stu-id="88dec-105">Quickstart: Analyze text using Node.js</span></span>

[!INCLUDE [Quickstart introduction for endpoint](../../../includes/cognitive-services-luis-qs-endpoint-intro-para.md)]

<a name="create-luis-subscription-key"></a>

## <a name="prerequisites"></a><span data-ttu-id="88dec-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="88dec-106">Prerequisites</span></span>

* <span data-ttu-id="88dec-107">[Node.js](https://nodejs.org/) programming language</span><span class="sxs-lookup"><span data-stu-id="88dec-107">[Node.js](https://nodejs.org/) programming language</span></span> 
* [<span data-ttu-id="88dec-108">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="88dec-108">Visual Studio Code</span></span>](https://code.visualstudio.com/)
* <span data-ttu-id="88dec-109">Public app ID: df67dcdb-c37d-46af-88e1-8b97951ca1c2</span><span class="sxs-lookup"><span data-stu-id="88dec-109">Public app ID: df67dcdb-c37d-46af-88e1-8b97951ca1c2</span></span>


> [!NOTE] 
> <span data-ttu-id="88dec-110">The complete Node.js solution is available from the [**LUIS-Samples** Github repository](https://github.com/Microsoft/LUIS-Samples/blob/master/documentation-samples/quickstarts/analyze-text/node).</span><span class="sxs-lookup"><span data-stu-id="88dec-110">The complete Node.js solution is available from the [**LUIS-Samples** Github repository](https://github.com/Microsoft/LUIS-Samples/blob/master/documentation-samples/quickstarts/analyze-text/node).</span></span>

## <a name="get-luis-key"></a><span data-ttu-id="88dec-111">Get LUIS key</span><span class="sxs-lookup"><span data-stu-id="88dec-111">Get LUIS key</span></span>

[!INCLUDE [Use authoring key for endpoint](../../../includes/cognitive-services-luis-qs-endpoint-get-key-para.md)]

## <a name="analyze-text-with-browser"></a><span data-ttu-id="88dec-112">Analyze text with browser</span><span class="sxs-lookup"><span data-stu-id="88dec-112">Analyze text with browser</span></span>

[!INCLUDE [Use authoring key for endpoint](../../../includes/cognitive-services-luis-qs-endpoint-browser-para.md)]

## <a name="analyze-text-with-nodejs"></a><span data-ttu-id="88dec-113">Analyze text with Node.js</span><span class="sxs-lookup"><span data-stu-id="88dec-113">Analyze text with Node.js</span></span>

<span data-ttu-id="88dec-114">You can use Node.js to access the same results you saw in the browser window in the previous step.</span><span class="sxs-lookup"><span data-stu-id="88dec-114">You can use Node.js to access the same results you saw in the browser window in the previous step.</span></span>

1. <span data-ttu-id="88dec-115">Copy the following code snippet:</span><span class="sxs-lookup"><span data-stu-id="88dec-115">Copy the following code snippet:</span></span>

   [!code-nodejs[Console app code that calls a LUIS endpoint for Node.js](~/samples-luis/documentation-samples/quickstarts/analyze-text/node/call-endpoint.js)]

2. <span data-ttu-id="88dec-116">Create `.env` file with the following text or set these variables in the system environment:</span><span class="sxs-lookup"><span data-stu-id="88dec-116">Create `.env` file with the following text or set these variables in the system environment:</span></span>

    ```CMD
    LUIS_APP_ID=df67dcdb-c37d-46af-88e1-8b97951ca1c2
    LUIS_ENDPOINT_KEY=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
    ```

3. <span data-ttu-id="88dec-117">Set the `LUIS_ENDPOINT_KEY` environment variable to your key.</span><span class="sxs-lookup"><span data-stu-id="88dec-117">Set the `LUIS_ENDPOINT_KEY` environment variable to your key.</span></span>

4. <span data-ttu-id="88dec-118">Install dependencies by running the following command at the command-line: `npm install`.</span><span class="sxs-lookup"><span data-stu-id="88dec-118">Install dependencies by running the following command at the command-line: `npm install`.</span></span>

5. <span data-ttu-id="88dec-119">Run the code with `npm start`.</span><span class="sxs-lookup"><span data-stu-id="88dec-119">Run the code with `npm start`.</span></span> <span data-ttu-id="88dec-120">It displays the same values that you saw earlier in the browser window.</span><span class="sxs-lookup"><span data-stu-id="88dec-120">It displays the same values that you saw earlier in the browser window.</span></span>

## <a name="luis-keys"></a><span data-ttu-id="88dec-121">LUIS keys</span><span class="sxs-lookup"><span data-stu-id="88dec-121">LUIS keys</span></span>

[!INCLUDE [Use authoring key for endpoint](../../../includes/cognitive-services-luis-qs-endpoint-key-usage-para.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="88dec-122">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="88dec-122">Clean up resources</span></span>

<span data-ttu-id="88dec-123">Delete the Node.js file.</span><span class="sxs-lookup"><span data-stu-id="88dec-123">Delete the Node.js file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="88dec-124">Next steps</span><span class="sxs-lookup"><span data-stu-id="88dec-124">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="88dec-125">Add utterances</span><span class="sxs-lookup"><span data-stu-id="88dec-125">Add utterances</span></span>](luis-get-started-node-add-utterance.md)