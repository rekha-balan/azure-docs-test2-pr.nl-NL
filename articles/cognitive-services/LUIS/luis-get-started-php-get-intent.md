---
title: Quickstart to Analyze natural language text in Language Understanding (LUIS) using PHP - Cognitive Services - Azure Cognitive Services | Microsoft Docs
description: In this quickstart, use an available public LUIS app to determine a user's intention from conversational text. Using PHP, send the user's intention as text to the public app's HTTP prediction endpoint. At the endpoint, LUIS applies the public app's model to analyze the natural language text for meaning, determining overall intent and extracting data relevant to the app's subject domain.
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: quickstart
ms.date: 08/23/2018
ms.author: diberry
ms.openlocfilehash: 80d9371cc36ca9ab6b25e79a78e15b7445f0084d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868576"
---
# <a name="quickstart-analyze-text-using-php"></a><span data-ttu-id="e9969-105">Quickstart: Analyze text using PHP</span><span class="sxs-lookup"><span data-stu-id="e9969-105">Quickstart: Analyze text using PHP</span></span>

[!INCLUDE [Quickstart introduction for endpoint](../../../includes/cognitive-services-luis-qs-endpoint-intro-para.md)]

<a name="create-luis-subscription-key"></a>

## <a name="prerequisites"></a><span data-ttu-id="e9969-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e9969-106">Prerequisites</span></span>

* <span data-ttu-id="e9969-107">[PHP](http://php.net/) programming language</span><span class="sxs-lookup"><span data-stu-id="e9969-107">[PHP](http://php.net/) programming language</span></span>
* [<span data-ttu-id="e9969-108">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="e9969-108">Visual Studio Code</span></span>](https://code.visualstudio.com/)
* <span data-ttu-id="e9969-109">Public app ID: df67dcdb-c37d-46af-88e1-8b97951ca1c2</span><span class="sxs-lookup"><span data-stu-id="e9969-109">Public app ID: df67dcdb-c37d-46af-88e1-8b97951ca1c2</span></span>


[!INCLUDE [Use authoring key for endpoint](../../../includes/cognitive-services-luis-qs-endpoint-luis-repo-note.md)]

## <a name="get-luis-key"></a><span data-ttu-id="e9969-110">Get LUIS key</span><span class="sxs-lookup"><span data-stu-id="e9969-110">Get LUIS key</span></span>

[!INCLUDE [Use authoring key for endpoint](../../../includes/cognitive-services-luis-qs-endpoint-get-key-para.md)]

## <a name="analyze-text-with-browser"></a><span data-ttu-id="e9969-111">Analyze text with browser</span><span class="sxs-lookup"><span data-stu-id="e9969-111">Analyze text with browser</span></span>

[!INCLUDE [Use authoring key for endpoint](../../../includes/cognitive-services-luis-qs-endpoint-browser-para.md)]

## <a name="analyze-text-with-php"></a><span data-ttu-id="e9969-112">Analyze text with PHP</span><span class="sxs-lookup"><span data-stu-id="e9969-112">Analyze text with PHP</span></span> 

<span data-ttu-id="e9969-113">You can use PHP to access the same results you saw in the browser window in the previous step.</span><span class="sxs-lookup"><span data-stu-id="e9969-113">You can use PHP to access the same results you saw in the browser window in the previous step.</span></span> 

1. <span data-ttu-id="e9969-114">Copy the code that follows and save it with filename `endpoint-call.php`:</span><span class="sxs-lookup"><span data-stu-id="e9969-114">Copy the code that follows and save it with filename `endpoint-call.php`:</span></span>

   [!code-php[PHP code that calls a LUIS endpoint](~/samples-luis/documentation-samples/quickstarts/analyze-text/php/endpoint-call.php)]

2. <span data-ttu-id="e9969-115">Replace `"YOUR-KEY"` with your endpoint key.</span><span class="sxs-lookup"><span data-stu-id="e9969-115">Replace `"YOUR-KEY"` with your endpoint key.</span></span>

3. <span data-ttu-id="e9969-116">Run the PHP application with `php endpoint-call.php`.</span><span class="sxs-lookup"><span data-stu-id="e9969-116">Run the PHP application with `php endpoint-call.php`.</span></span> <span data-ttu-id="e9969-117">It displays the same JSON that you saw earlier in the browser window.</span><span class="sxs-lookup"><span data-stu-id="e9969-117">It displays the same JSON that you saw earlier in the browser window.</span></span>

## <a name="luis-keys"></a><span data-ttu-id="e9969-118">LUIS keys</span><span class="sxs-lookup"><span data-stu-id="e9969-118">LUIS keys</span></span>

[!INCLUDE [Use authoring key for endpoint](../../../includes/cognitive-services-luis-qs-endpoint-key-usage-para.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="e9969-119">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="e9969-119">Clean up resources</span></span>

<span data-ttu-id="e9969-120">Delete the PHP file.</span><span class="sxs-lookup"><span data-stu-id="e9969-120">Delete the PHP file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e9969-121">Next steps</span><span class="sxs-lookup"><span data-stu-id="e9969-121">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e9969-122">Add utterances</span><span class="sxs-lookup"><span data-stu-id="e9969-122">Add utterances</span></span>](luis-get-started-php-add-utterance.md)