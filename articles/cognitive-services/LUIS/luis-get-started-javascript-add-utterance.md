---
title: Quickstart learning how to add utterances to a LUIS app using JavaScript  - Azure Cognitive Services| Microsoft Docs
description: In this quickstart, you learn to call a LUIS app using JavaScript.
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: quickstart
ms.date: 08/24/2018
ms.author: diberry
ms.openlocfilehash: 0920a194d3e9c93883b88b7131f7e81dc8fb3302
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871419"
---
# <a name="quickstart-change-model-using-javascript"></a><span data-ttu-id="a511f-103">Quickstart: Change model using JavaScript</span><span class="sxs-lookup"><span data-stu-id="a511f-103">Quickstart: Change model using JavaScript</span></span>

[!INCLUDE [Quickstart introduction for change model](../../../includes/cognitive-services-luis-qs-endpoint-intro-para.md)]

## <a name="prerequisites"></a><span data-ttu-id="a511f-104">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a511f-104">Prerequisites</span></span>

[!INCLUDE [Quickstart prerequisites for changing model](../../../includes/cognitive-services-luis-qs-change-model-prereq.md)]
* <span data-ttu-id="a511f-105">[Visual Studio Code](https://code.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="a511f-105">[Visual Studio Code](https://code.visualstudio.com/).</span></span>

[!INCLUDE [Code is available in LUIS-Samples Github repo](../../../includes/cognitive-services-luis-qs-change-model-luis-repo-note.md)]

## <a name="example-utterances-json-file"></a><span data-ttu-id="a511f-106">Example utterances JSON file</span><span class="sxs-lookup"><span data-stu-id="a511f-106">Example utterances JSON file</span></span>

[!INCLUDE [Quickstart explanation of example utterance JSON file](../../../includes/cognitive-services-luis-qs-change-model-json-ex-utt.md)]


## <a name="create-quickstart-code"></a><span data-ttu-id="a511f-107">Create quickstart code</span><span class="sxs-lookup"><span data-stu-id="a511f-107">Create quickstart code</span></span>

<span data-ttu-id="a511f-108">Create `add-utterances.html` and add the following code:</span><span class="sxs-lookup"><span data-stu-id="a511f-108">Create `add-utterances.html` and add the following code:</span></span>

   [!code-html[Html code](~/samples-luis/documentation-samples/quickstarts/change-model/javascript/add-utterance.html "Javascript code")]

## <a name="run-code"></a><span data-ttu-id="a511f-109">Run code</span><span class="sxs-lookup"><span data-stu-id="a511f-109">Run code</span></span>

1. <span data-ttu-id="a511f-110">Open the file in a browser.</span><span class="sxs-lookup"><span data-stu-id="a511f-110">Open the file in a browser.</span></span>

2. <span data-ttu-id="a511f-111">Add your LUIS authoring ID, your LUIS application ID.</span><span class="sxs-lookup"><span data-stu-id="a511f-111">Add your LUIS authoring ID, your LUIS application ID.</span></span>

3. <span data-ttu-id="a511f-112">Modify the **array of utterances** to add to your application.</span><span class="sxs-lookup"><span data-stu-id="a511f-112">Modify the **array of utterances** to add to your application.</span></span> <span data-ttu-id="a511f-113">They are stored in the utteranceJSON variable.</span><span class="sxs-lookup"><span data-stu-id="a511f-113">They are stored in the utteranceJSON variable.</span></span> <span data-ttu-id="a511f-114">Change these values for your own domain and utterance needs.</span><span class="sxs-lookup"><span data-stu-id="a511f-114">Change these values for your own domain and utterance needs.</span></span> 

    ```json
    // example batch utterances
    var utteranceJSON = [
        {
            "text": "go to Seattle",
            "intentName": "BookFlight",
            "entityLabels": [
                {
                    "entityName": "Location::LocationTo",
                    "startCharIndex": 6,
                    "endCharIndex": 12
                }
            ]
        }
    ,
        {
            "text": "book a flight",
            "intentName": "BookFlight",
            "entityLabels": []
        }
    ];
    ```

4. <span data-ttu-id="a511f-115">Select the `Upload utterance` button.</span><span class="sxs-lookup"><span data-stu-id="a511f-115">Select the `Upload utterance` button.</span></span> <span data-ttu-id="a511f-116">The LUIS results are displayed below the buttons.</span><span class="sxs-lookup"><span data-stu-id="a511f-116">The LUIS results are displayed below the buttons.</span></span>

5. <span data-ttu-id="a511f-117">Select the `Train model` button to train your application with these new utterances.</span><span class="sxs-lookup"><span data-stu-id="a511f-117">Select the `Train model` button to train your application with these new utterances.</span></span>

6. <span data-ttu-id="a511f-118">Select the `Train Status` button to see the training status.</span><span class="sxs-lookup"><span data-stu-id="a511f-118">Select the `Train Status` button to see the training status.</span></span> 

    ![Add-utterances.html](./media/luis-quickstart-javascript-add-utterance/add-utterance.png)

## <a name="clean-up-resources"></a><span data-ttu-id="a511f-120">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="a511f-120">Clean up resources</span></span>
<span data-ttu-id="a511f-121">When you are done with the quickstart, remove all the files created in this quickstart.</span><span class="sxs-lookup"><span data-stu-id="a511f-121">When you are done with the quickstart, remove all the files created in this quickstart.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="a511f-122">Next steps</span><span class="sxs-lookup"><span data-stu-id="a511f-122">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="a511f-123">Integrate LUIS with a bot</span><span class="sxs-lookup"><span data-stu-id="a511f-123">Integrate LUIS with a bot</span></span>](luis-csharp-tutorial-build-bot-framework-sample.md)
