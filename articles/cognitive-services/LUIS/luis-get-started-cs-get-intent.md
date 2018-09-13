---
title: Analyze natural language text in Language Understanding (LUIS) using C# - Azure Cognitive Services | Microsoft Docs
description: In this quickstart, use an available public LUIS app to determine a user's intention from conversational text. Using C#, send the user's intention as text to the public app's HTTP prediction endpoint. At the endpoint, LUIS applies the public app's model to analyze the natural language text for meaning, determining overall intent and extracting data relevant to the app's subject domain.
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: quickstart
ms.date: 08/23/2018
ms.author: diberry
ms.openlocfilehash: b6ddd48fc6bfa5c099e42f3717a2113f871b4f9a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871116"
---
# <a name="quickstart-analyze-text-using-c"></a><span data-ttu-id="cd2a5-105">Quickstart: Analyze text using C#</span><span class="sxs-lookup"><span data-stu-id="cd2a5-105">Quickstart: Analyze text using C#</span></span>

[!INCLUDE [Quickstart introduction for endpoint](../../../includes/cognitive-services-luis-qs-endpoint-intro-para.md)]

<a name="create-luis-subscription-key"></a>

## <a name="prerequisites"></a><span data-ttu-id="cd2a5-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="cd2a5-106">Prerequisites</span></span>

* [<span data-ttu-id="cd2a5-107">Visual Studio Community 2017 edition</span><span class="sxs-lookup"><span data-stu-id="cd2a5-107">Visual Studio Community 2017 edition</span></span>](https://visualstudio.microsoft.com/vs/community/)
* <span data-ttu-id="cd2a5-108">C# programming language (included with VS Community 2017)</span><span class="sxs-lookup"><span data-stu-id="cd2a5-108">C# programming language (included with VS Community 2017)</span></span>
* <span data-ttu-id="cd2a5-109">Public app ID: df67dcdb-c37d-46af-88e1-8b97951ca1c2</span><span class="sxs-lookup"><span data-stu-id="cd2a5-109">Public app ID: df67dcdb-c37d-46af-88e1-8b97951ca1c2</span></span>


[!INCLUDE [Use authoring key for endpoint](../../../includes/cognitive-services-luis-qs-endpoint-luis-repo-note.md)]

## <a name="get-luis-key"></a><span data-ttu-id="cd2a5-110">Get LUIS key</span><span class="sxs-lookup"><span data-stu-id="cd2a5-110">Get LUIS key</span></span>

[!INCLUDE [Use authoring key for endpoint](../../../includes/cognitive-services-luis-qs-endpoint-get-key-para.md)]

## <a name="analyze-text-with-browser"></a><span data-ttu-id="cd2a5-111">Analyze text with browser</span><span class="sxs-lookup"><span data-stu-id="cd2a5-111">Analyze text with browser</span></span>

[!INCLUDE [Use authoring key for endpoint](../../../includes/cognitive-services-luis-qs-endpoint-browser-para.md)]

## <a name="analyze-text-with-c"></a><span data-ttu-id="cd2a5-112">Analyze text with C#</span><span class="sxs-lookup"><span data-stu-id="cd2a5-112">Analyze text with C#</span></span> 

<span data-ttu-id="cd2a5-113">Use C# to query the prediction endpoint GET [API](https://westus.dev.cognitive.microsoft.com/docs/services/5819c76f40a6350ce09de1ac/operations/5819c77140a63516d81aee78) to get the same results as you saw in the browser window in the previous section.</span><span class="sxs-lookup"><span data-stu-id="cd2a5-113">Use C# to query the prediction endpoint GET [API](https://westus.dev.cognitive.microsoft.com/docs/services/5819c76f40a6350ce09de1ac/operations/5819c77140a63516d81aee78) to get the same results as you saw in the browser window in the previous section.</span></span> 

1. <span data-ttu-id="cd2a5-114">Create a new console application in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cd2a5-114">Create a new console application in Visual Studio.</span></span> 

    ![LUIS user settings menu access](media/luis-get-started-cs-get-intent/visual-studio-console-app.png)

2. <span data-ttu-id="cd2a5-116">In the Visual Studio project, in the Solutions Explorer, select **Add reference**, then select **System.Web** from the Assemblies tab.</span><span class="sxs-lookup"><span data-stu-id="cd2a5-116">In the Visual Studio project, in the Solutions Explorer, select **Add reference**, then select **System.Web** from the Assemblies tab.</span></span>

    ![LUIS user settings menu access](media/luis-get-started-cs-get-intent/add-system-dot-web-to-project.png)

3. <span data-ttu-id="cd2a5-118">Overwrite Program.cs with the following code:</span><span class="sxs-lookup"><span data-stu-id="cd2a5-118">Overwrite Program.cs with the following code:</span></span>
    
   [!code-csharp[Console app code that calls a LUIS endpoint](~/samples-luis/documentation-samples/quickstarts/analyze-text/csharp/Program.cs)]

4. <span data-ttu-id="cd2a5-119">Replace the value of `YOUR_KEY` with your LUIS key.</span><span class="sxs-lookup"><span data-stu-id="cd2a5-119">Replace the value of `YOUR_KEY` with your LUIS key.</span></span>

5. <span data-ttu-id="cd2a5-120">Build and run the console application.</span><span class="sxs-lookup"><span data-stu-id="cd2a5-120">Build and run the console application.</span></span> <span data-ttu-id="cd2a5-121">It displays the same JSON that you saw earlier in the browser window.</span><span class="sxs-lookup"><span data-stu-id="cd2a5-121">It displays the same JSON that you saw earlier in the browser window.</span></span>

    ![Console window displays JSON result from LUIS](./media/luis-get-started-cs-get-intent/console-turn-on.png)

## <a name="luis-keys"></a><span data-ttu-id="cd2a5-123">LUIS keys</span><span class="sxs-lookup"><span data-stu-id="cd2a5-123">LUIS keys</span></span>

[!INCLUDE [Use authoring key for endpoint](../../../includes/cognitive-services-luis-qs-endpoint-key-usage-para.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="cd2a5-124">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="cd2a5-124">Clean up resources</span></span>

<span data-ttu-id="cd2a5-125">When you are finished with this quickstart, close the Visual Studio project and remove the project directory from the file system.</span><span class="sxs-lookup"><span data-stu-id="cd2a5-125">When you are finished with this quickstart, close the Visual Studio project and remove the project directory from the file system.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="cd2a5-126">Next steps</span><span class="sxs-lookup"><span data-stu-id="cd2a5-126">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="cd2a5-127">Add utterances and train with C#</span><span class="sxs-lookup"><span data-stu-id="cd2a5-127">Add utterances and train with C#</span></span>](luis-get-started-cs-add-utterance.md)