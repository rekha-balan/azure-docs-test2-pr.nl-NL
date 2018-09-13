---
title: Analyze natural language text in Language Understanding (LUIS) using Javascript - Cognitive Services - Azure Cognitive Services | Microsoft Docs
description: In this quickstart, use an available public LUIS app to determine a user's intention from conversational text. Using Javascript, send the user's intention as text to the public app's HTTP prediction endpoint. At the endpoint, LUIS applies the public app's model to analyze the natural language text for meaning, determining overall intent and extracting data relevant to the app's subject domain.
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: quickstart
ms.date: 08/23/2018
ms.author: diberry
ms.openlocfilehash: d787f744ff0fe7315553e9dd6f4465122f7e06b2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867032"
---
# <a name="quickstart-analyze-text-using-javascript"></a><span data-ttu-id="f24a3-105">Quickstart: Analyze text using Javascript</span><span class="sxs-lookup"><span data-stu-id="f24a3-105">Quickstart: Analyze text using Javascript</span></span>

[!INCLUDE [Quickstart introduction for endpoint](../../../includes/cognitive-services-luis-qs-endpoint-intro-para.md)]

<a name="create-luis-subscription-key"></a>

[!INCLUDE [Use authoring key for endpoint](../../../includes/cognitive-services-luis-qs-endpoint-luis-repo-note.md)]

## <a name="prerequisites"></a><span data-ttu-id="f24a3-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f24a3-106">Prerequisites</span></span>

* [<span data-ttu-id="f24a3-107">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="f24a3-107">Visual Studio Code</span></span>](https://code.visualstudio.com/)
* <span data-ttu-id="f24a3-108">Public app ID: df67dcdb-c37d-46af-88e1-8b97951ca1c2</span><span class="sxs-lookup"><span data-stu-id="f24a3-108">Public app ID: df67dcdb-c37d-46af-88e1-8b97951ca1c2</span></span>


## <a name="get-luis-key"></a><span data-ttu-id="f24a3-109">Get LUIS key</span><span class="sxs-lookup"><span data-stu-id="f24a3-109">Get LUIS key</span></span>

[!INCLUDE [Use authoring key for endpoint](../../../includes/cognitive-services-luis-qs-endpoint-get-key-para.md)]

## <a name="analyze-text-with-browser"></a><span data-ttu-id="f24a3-110">Analyze text with browser</span><span class="sxs-lookup"><span data-stu-id="f24a3-110">Analyze text with browser</span></span>

[!INCLUDE [Use authoring key for endpoint](../../../includes/cognitive-services-luis-qs-endpoint-browser-para.md)]

## <a name="analyze-text-with-javascript"></a><span data-ttu-id="f24a3-111">Analyze text with Javascript</span><span class="sxs-lookup"><span data-stu-id="f24a3-111">Analyze text with Javascript</span></span> 

<span data-ttu-id="f24a3-112">You can use Javascript to access the same results you saw in the browser window in the previous step.</span><span class="sxs-lookup"><span data-stu-id="f24a3-112">You can use Javascript to access the same results you saw in the browser window in the previous step.</span></span> 

1. <span data-ttu-id="f24a3-113">Copy the code that follows and save it into an HTML file:</span><span class="sxs-lookup"><span data-stu-id="f24a3-113">Copy the code that follows and save it into an HTML file:</span></span>

   [!code-html[Console app code that calls a LUIS endpoint](~/samples-luis/documentation-samples/quickstarts/analyze-text/javascript/call-endpoint.html)]

2. <span data-ttu-id="f24a3-114">Open the file in a browser.</span><span class="sxs-lookup"><span data-stu-id="f24a3-114">Open the file in a browser.</span></span> <span data-ttu-id="f24a3-115">Enter your LUIS endpoint key in the form and select **Submit**.</span><span class="sxs-lookup"><span data-stu-id="f24a3-115">Enter your LUIS endpoint key in the form and select **Submit**.</span></span>

    ![Html sample displayed in browser with LUIS results for Home Automation app](./media/luis-get-started-js-get-intent/html-results.png)

    <span data-ttu-id="f24a3-117">The result display under the form.</span><span class="sxs-lookup"><span data-stu-id="f24a3-117">The result display under the form.</span></span> 

## <a name="luis-keys"></a><span data-ttu-id="f24a3-118">LUIS keys</span><span class="sxs-lookup"><span data-stu-id="f24a3-118">LUIS keys</span></span>

[!INCLUDE [Use authoring key for endpoint](../../../includes/cognitive-services-luis-qs-endpoint-key-usage-para.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="f24a3-119">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="f24a3-119">Clean up resources</span></span>

<span data-ttu-id="f24a3-120">Delete the Javascript file.</span><span class="sxs-lookup"><span data-stu-id="f24a3-120">Delete the Javascript file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f24a3-121">Next steps</span><span class="sxs-lookup"><span data-stu-id="f24a3-121">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="f24a3-122">Add utterances</span><span class="sxs-lookup"><span data-stu-id="f24a3-122">Add utterances</span></span>](luis-get-started-javascript-add-utterance.md)
