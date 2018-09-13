---
title: Analyze natural language text in Language Understanding (LUIS) using Java - Cognitive Services - Azure Cognitive Services | Microsoft Docs
description: In this quickstart, use an available public LUIS app to determine a user's intention from conversational text. Using Java, send the user's intention as text to the public app's HTTP prediction endpoint. At the endpoint, LUIS applies the public app's model to analyze the natural language text for meaning, determining overall intent and extracting data relevant to the app's subject domain.
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: quickstart
ms.date: 06/27/2018
ms.author: diberry
ms.openlocfilehash: 4dd5437940994a2f264b5a11baebcd67fdddb43d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869316"
---
# <a name="quickstart-analyze-text-using-java"></a><span data-ttu-id="9095c-105">Quickstart: Analyze text using Java</span><span class="sxs-lookup"><span data-stu-id="9095c-105">Quickstart: Analyze text using Java</span></span>

[!INCLUDE [Quickstart introduction for endpoint](../../../includes/cognitive-services-luis-qs-endpoint-intro-para.md)]

<a name="create-luis-subscription-key"></a>

## <a name="prerequisites"></a><span data-ttu-id="9095c-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="9095c-106">Prerequisites</span></span>

* <span data-ttu-id="9095c-107">[JDK SE](http://www.oracle.com/technetwork/java/javase/downloads/index.html)  (Java Development Kit, Standard Edition)</span><span class="sxs-lookup"><span data-stu-id="9095c-107">[JDK SE](http://www.oracle.com/technetwork/java/javase/downloads/index.html)  (Java Development Kit, Standard Edition)</span></span>
* [<span data-ttu-id="9095c-108">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="9095c-108">Visual Studio Code</span></span>](https://code.visualstudio.com/)
* <span data-ttu-id="9095c-109">Public app ID: df67dcdb-c37d-46af-88e1-8b97951ca1c2</span><span class="sxs-lookup"><span data-stu-id="9095c-109">Public app ID: df67dcdb-c37d-46af-88e1-8b97951ca1c2</span></span>


[!INCLUDE [Use authoring key for endpoint](../../../includes/cognitive-services-luis-qs-endpoint-luis-repo-note.md)]

## <a name="get-luis-key"></a><span data-ttu-id="9095c-110">Get LUIS key</span><span class="sxs-lookup"><span data-stu-id="9095c-110">Get LUIS key</span></span>

[!INCLUDE [Use authoring key for endpoint](../../../includes/cognitive-services-luis-qs-endpoint-get-key-para.md)]

## <a name="analyze-text-with-browser"></a><span data-ttu-id="9095c-111">Analyze text with browser</span><span class="sxs-lookup"><span data-stu-id="9095c-111">Analyze text with browser</span></span>

[!INCLUDE [Use authoring key for endpoint](../../../includes/cognitive-services-luis-qs-endpoint-browser-para.md)]

## <a name="analyze-text-with-java"></a><span data-ttu-id="9095c-112">Analyze text with Java</span><span class="sxs-lookup"><span data-stu-id="9095c-112">Analyze text with Java</span></span> 

<span data-ttu-id="9095c-113">You can use Java to access the same results you saw in the browser window in the previous step.</span><span class="sxs-lookup"><span data-stu-id="9095c-113">You can use Java to access the same results you saw in the browser window in the previous step.</span></span> 

1. <span data-ttu-id="9095c-114">Copy the following code to create a class in a file named `LuisGetRequest.java`:</span><span class="sxs-lookup"><span data-stu-id="9095c-114">Copy the following code to create a class in a file named `LuisGetRequest.java`:</span></span>

   [!code-java[Console app code that calls a LUIS endpoint](~/samples-luis/documentation-samples/quickstarts/analyze-text/java/call-endpoint.java)]

2. <span data-ttu-id="9095c-115">Replace the value of the `YOUR-KEY` variable with your LUIS key.</span><span class="sxs-lookup"><span data-stu-id="9095c-115">Replace the value of the `YOUR-KEY` variable with your LUIS key.</span></span>

3. <span data-ttu-id="9095c-116">Compile the java program with `javac -cp ":lib/*" LuisGetRequest.java`.</span><span class="sxs-lookup"><span data-stu-id="9095c-116">Compile the java program with `javac -cp ":lib/*" LuisGetRequest.java`.</span></span> 

4. <span data-ttu-id="9095c-117">Run the application with `java -cp ":lib/*" LuisGetRequest.java`.</span><span class="sxs-lookup"><span data-stu-id="9095c-117">Run the application with `java -cp ":lib/*" LuisGetRequest.java`.</span></span> <span data-ttu-id="9095c-118">It displays the same JSON that you saw earlier in the browser window.</span><span class="sxs-lookup"><span data-stu-id="9095c-118">It displays the same JSON that you saw earlier in the browser window.</span></span>

    ![Console window displays JSON result from LUIS](./media/luis-get-started-java-get-intent/console-turn-on.png)
    
## <a name="luis-keys"></a><span data-ttu-id="9095c-120">LUIS keys</span><span class="sxs-lookup"><span data-stu-id="9095c-120">LUIS keys</span></span>

[!INCLUDE [Use authoring key for endpoint](../../../includes/cognitive-services-luis-qs-endpoint-key-usage-para.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="9095c-121">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="9095c-121">Clean up resources</span></span>

<span data-ttu-id="9095c-122">Delete the Java file.</span><span class="sxs-lookup"><span data-stu-id="9095c-122">Delete the Java file.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="9095c-123">Next steps</span><span class="sxs-lookup"><span data-stu-id="9095c-123">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="9095c-124">Add utterances</span><span class="sxs-lookup"><span data-stu-id="9095c-124">Add utterances</span></span>](luis-get-started-java-add-utterance.md)