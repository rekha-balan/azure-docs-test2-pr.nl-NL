---
title: Analyze natural language text in Language Understanding (LUIS) using Ruby - Cognitive Services - Azure Cognitive Services | Microsoft Docs
description: In this quickstart, use an available public LUIS app to determine a user's intention from conversational text. Using Ruby, send the user's intention as text to the public app's HTTP prediction endpoint. At the endpoint, LUIS applies the public app's model to analyze the natural language text for meaning, determining overall intent and extracting data relevant to the app's subject domain.
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: quickstart
ms.date: 08/23/2018
ms.author: diberry
ms.openlocfilehash: 0909c1dd056570a275b3042674d251c637413cae
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868492"
---
# <a name="quickstart-analyze-text-using-ruby"></a><span data-ttu-id="2aa66-105">Quickstart: Analyze text using Ruby</span><span class="sxs-lookup"><span data-stu-id="2aa66-105">Quickstart: Analyze text using Ruby</span></span>

[!INCLUDE [Quickstart introduction for endpoint](../../../includes/cognitive-services-luis-qs-endpoint-intro-para.md)]

## <a name="prerequisites"></a><span data-ttu-id="2aa66-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="2aa66-106">Prerequisites</span></span>

* <span data-ttu-id="2aa66-107">[Ruby](https://www.ruby-lang.org/) programming language</span><span class="sxs-lookup"><span data-stu-id="2aa66-107">[Ruby](https://www.ruby-lang.org/) programming language</span></span>
* [<span data-ttu-id="2aa66-108">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="2aa66-108">Visual Studio Code</span></span>](https://code.visualstudio.com/)
* <span data-ttu-id="2aa66-109">Public app ID: df67dcdb-c37d-46af-88e1-8b97951ca1c2</span><span class="sxs-lookup"><span data-stu-id="2aa66-109">Public app ID: df67dcdb-c37d-46af-88e1-8b97951ca1c2</span></span>


[!INCLUDE [Use authoring key for endpoint](../../../includes/cognitive-services-luis-qs-endpoint-luis-repo-note.md)]

<a name="create-luis-subscription-key"></a>

## <a name="get-luis-key"></a><span data-ttu-id="2aa66-110">Get LUIS key</span><span class="sxs-lookup"><span data-stu-id="2aa66-110">Get LUIS key</span></span>

[!INCLUDE [Use authoring key for endpoint](../../../includes/cognitive-services-luis-qs-endpoint-get-key-para.md)]

## <a name="analyze-text-with-browser"></a><span data-ttu-id="2aa66-111">Analyze text with browser</span><span class="sxs-lookup"><span data-stu-id="2aa66-111">Analyze text with browser</span></span>

[!INCLUDE [Use authoring key for endpoint](../../../includes/cognitive-services-luis-qs-endpoint-browser-para.md)]

## <a name="analyze-text-with-ruby"></a><span data-ttu-id="2aa66-112">Analyze text with Ruby</span><span class="sxs-lookup"><span data-stu-id="2aa66-112">Analyze text with Ruby</span></span> 

<span data-ttu-id="2aa66-113">You can use Ruby to access the same results you saw in the browser window in the previous step.</span><span class="sxs-lookup"><span data-stu-id="2aa66-113">You can use Ruby to access the same results you saw in the browser window in the previous step.</span></span> 

1. <span data-ttu-id="2aa66-114">Copy the code that follows and save it into a file named `endpoint-call.rb`:</span><span class="sxs-lookup"><span data-stu-id="2aa66-114">Copy the code that follows and save it into a file named `endpoint-call.rb`:</span></span>

   [!code-ruby[Ruby code that calls a LUIS endpoint](~/samples-luis/documentation-samples/quickstarts/analyze-text/ruby/endpoint-call.rb)]

2. <span data-ttu-id="2aa66-115">Replace `"YOUR-KEY"` with your endpoint key.</span><span class="sxs-lookup"><span data-stu-id="2aa66-115">Replace `"YOUR-KEY"` with your endpoint key.</span></span>

3. <span data-ttu-id="2aa66-116">Run the Ruby application at the command-line with `ruby endpoint-call.rb`.</span><span class="sxs-lookup"><span data-stu-id="2aa66-116">Run the Ruby application at the command-line with `ruby endpoint-call.rb`.</span></span> <span data-ttu-id="2aa66-117">It displays the same JSON that you saw earlier in the browser window.</span><span class="sxs-lookup"><span data-stu-id="2aa66-117">It displays the same JSON that you saw earlier in the browser window.</span></span>

    ```
    LUIS query: turn on the left light
    
    Request URI: https://westus.api.cognitive.microsoft.com/luis/v2.0/apps/df67dcdb-c37d-46af-88e1-8b97951ca1c2?q=turn+on+the+left+light&timezoneOffset=0&verbose=false&spellCheck=false&staging=false
    
    JSON Response:
    
    {
      "query": "turn on the left light",
      "topScoringIntent": {
        "intent": "HomeAutomation.TurnOn",
        "score": 0.933549
      },
      "entities": [
        {
          "entity": "left",
          "type": "HomeAutomation.Room",
          "startIndex": 12,
          "endIndex": 15,
          "score": 0.540835142
        }
      ]
    }
```

## <a name="clean-up-resources"></a><span data-ttu-id="2aa66-118">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="2aa66-118">Clean up resources</span></span>

<span data-ttu-id="2aa66-119">Delete Ruby file.</span><span class="sxs-lookup"><span data-stu-id="2aa66-119">Delete Ruby file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2aa66-120">Next steps</span><span class="sxs-lookup"><span data-stu-id="2aa66-120">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2aa66-121">Add utterances</span><span class="sxs-lookup"><span data-stu-id="2aa66-121">Add utterances</span></span>](luis-get-started-ruby-add-utterance.md)