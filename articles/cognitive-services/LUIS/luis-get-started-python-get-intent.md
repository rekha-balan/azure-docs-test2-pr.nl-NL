---
title: Quickstart learning how to call a Language Understanding (LUIS) app using Python | Microsoft Docs
description: In this quickstart, you learn to call a LUIS app using Python.
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: quickstart
ms.date: 06/27/2018
ms.author: diberry
ms.openlocfilehash: bc7ae912d762a98c34b9a1b2d6a82d5630c4794b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870178"
---
# <a name="quickstart-call-a-luis-endpoint-using-python"></a><span data-ttu-id="b8f55-103">Quickstart: Call a LUIS endpoint using Python</span><span class="sxs-lookup"><span data-stu-id="b8f55-103">Quickstart: Call a LUIS endpoint using Python</span></span>
<span data-ttu-id="b8f55-104">In this quickstart, pass utterances to a LUIS endpoint and get intent and entities back.</span><span class="sxs-lookup"><span data-stu-id="b8f55-104">In this quickstart, pass utterances to a LUIS endpoint and get intent and entities back.</span></span>

<!-- green checkmark -->
<!--
> [!div class="checklist"]
> * Create LUIS subscription and copy key value for later use
> * View LUIS endpoint results from browser to public sample IoT app
> * Create Visual Studio C# console app to make HTTPS call to LUIS endpoint
-->

<span data-ttu-id="b8f55-105">For this article, you need a free [LUIS](luis-reference-regions.md#luis-website) account in order to author your LUIS application.</span><span class="sxs-lookup"><span data-stu-id="b8f55-105">For this article, you need a free [LUIS](luis-reference-regions.md#luis-website) account in order to author your LUIS application.</span></span>

<a name="create-luis-subscription-key"></a>
## <a name="create-luis-endpoint-key"></a><span data-ttu-id="b8f55-106">Create LUIS endpoint key</span><span class="sxs-lookup"><span data-stu-id="b8f55-106">Create LUIS endpoint key</span></span>
<span data-ttu-id="b8f55-107">You need a Cognitive Services API key to make calls to the sample LUIS app used in this walkthrough.</span><span class="sxs-lookup"><span data-stu-id="b8f55-107">You need a Cognitive Services API key to make calls to the sample LUIS app used in this walkthrough.</span></span> 

<span data-ttu-id="b8f55-108">To get an API key, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="b8f55-108">To get an API key, follow these steps:</span></span> 

1. <span data-ttu-id="b8f55-109">You first need to create a [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="b8f55-109">You first need to create a [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) in the Azure portal.</span></span> <span data-ttu-id="b8f55-110">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="b8f55-110">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

2. <span data-ttu-id="b8f55-111">Log in to the Azure portal at https://portal.azure.com.</span><span class="sxs-lookup"><span data-stu-id="b8f55-111">Log in to the Azure portal at https://portal.azure.com.</span></span> 

3. <span data-ttu-id="b8f55-112">Follow the steps in [Creating Endpoint Keys using Azure](./luis-how-to-azure-subscription.md) to get a key.</span><span class="sxs-lookup"><span data-stu-id="b8f55-112">Follow the steps in [Creating Endpoint Keys using Azure](./luis-how-to-azure-subscription.md) to get a key.</span></span>

4. <span data-ttu-id="b8f55-113">Go back to the [LUIS](luis-reference-regions.md) website and log in using your Azure account.</span><span class="sxs-lookup"><span data-stu-id="b8f55-113">Go back to the [LUIS](luis-reference-regions.md) website and log in using your Azure account.</span></span> 

    <span data-ttu-id="b8f55-114">[![](media/luis-get-started-node-get-intent/app-list.png "Screenshot of app list")](media/luis-get-started-node-get-intent/app-list.png)</span><span class="sxs-lookup"><span data-stu-id="b8f55-114">[![](media/luis-get-started-node-get-intent/app-list.png "Screenshot of app list")](media/luis-get-started-node-get-intent/app-list.png)</span></span>

## <a name="understand-what-luis-returns"></a><span data-ttu-id="b8f55-115">Understand what LUIS returns</span><span class="sxs-lookup"><span data-stu-id="b8f55-115">Understand what LUIS returns</span></span>

<span data-ttu-id="b8f55-116">To understand what a LUIS app returns, you can paste the URL of a sample LUIS app into a browser window.</span><span class="sxs-lookup"><span data-stu-id="b8f55-116">To understand what a LUIS app returns, you can paste the URL of a sample LUIS app into a browser window.</span></span> <span data-ttu-id="b8f55-117">The sample app is an IoT app that detects whether the user wants to turn on or turn off lights.</span><span class="sxs-lookup"><span data-stu-id="b8f55-117">The sample app is an IoT app that detects whether the user wants to turn on or turn off lights.</span></span>

1. <span data-ttu-id="b8f55-118">The endpoint of the sample app is in this format: `https://westus.api.cognitive.microsoft.com/luis/v2.0/apps/df67dcdb-c37d-46af-88e1-8b97951ca1c2?subscription-key=<YOUR_API_KEY>&verbose=false&q=turn%20on%20the%20bedroom%20light` Copy the URL and substitute your endpoint key for the value of the `subscription-key` field.</span><span class="sxs-lookup"><span data-stu-id="b8f55-118">The endpoint of the sample app is in this format: `https://westus.api.cognitive.microsoft.com/luis/v2.0/apps/df67dcdb-c37d-46af-88e1-8b97951ca1c2?subscription-key=<YOUR_API_KEY>&verbose=false&q=turn%20on%20the%20bedroom%20light` Copy the URL and substitute your endpoint key for the value of the `subscription-key` field.</span></span>
2. <span data-ttu-id="b8f55-119">Paste the URL into a browser window and press Enter.</span><span class="sxs-lookup"><span data-stu-id="b8f55-119">Paste the URL into a browser window and press Enter.</span></span> <span data-ttu-id="b8f55-120">The browser displays a JSON result that indicates that LUIS detects the `HomeAutomation.TurnOn` intent and the `HomeAutomation.Room` entity with the value `bedroom`.</span><span class="sxs-lookup"><span data-stu-id="b8f55-120">The browser displays a JSON result that indicates that LUIS detects the `HomeAutomation.TurnOn` intent and the `HomeAutomation.Room` entity with the value `bedroom`.</span></span>

    ![JSON result detects the intent TurnOn](./media/luis-get-started-node-get-intent/turn-on-bedroom.png)
3. <span data-ttu-id="b8f55-122">Change the value of the `q=` parameter in the URL to `turn off the living room light`, and press enter.</span><span class="sxs-lookup"><span data-stu-id="b8f55-122">Change the value of the `q=` parameter in the URL to `turn off the living room light`, and press enter.</span></span> <span data-ttu-id="b8f55-123">The result now indicates that the LUIS detected the `HomeAutomation.TurnOff` intent and the `HomeAutomation.Room` entity with value `living room`.</span><span class="sxs-lookup"><span data-stu-id="b8f55-123">The result now indicates that the LUIS detected the `HomeAutomation.TurnOff` intent and the `HomeAutomation.Room` entity with value `living room`.</span></span> 

    ![JSON result detects the intent TurnOff](./media/luis-get-started-node-get-intent/turn-off-living-room.png)


## <a name="consume-a-luis-result-using-the-endpoint-api-with-python"></a><span data-ttu-id="b8f55-125">Consume a LUIS result using the Endpoint API with Python</span><span class="sxs-lookup"><span data-stu-id="b8f55-125">Consume a LUIS result using the Endpoint API with Python</span></span>

<span data-ttu-id="b8f55-126">You can use Python to access the same results you saw in the browser window in the previous step.</span><span class="sxs-lookup"><span data-stu-id="b8f55-126">You can use Python to access the same results you saw in the browser window in the previous step.</span></span>

1. <span data-ttu-id="b8f55-127">Copy one of the following code snippets to a file called `quickstart-call-endpoint.py`:</span><span class="sxs-lookup"><span data-stu-id="b8f55-127">Copy one of the following code snippets to a file called `quickstart-call-endpoint.py`:</span></span>

   [!code-python[Console app code that calls a LUIS endpoint for Python 2.7](~/samples-luis/documentation-samples/quickstarts/analyze-text/python/2.x/quickstart-call-endpoint-2-7.py)]

   [!code-python[Console app code that calls a LUIS endpoint for Python 3.6](~/samples-luis/documentation-samples/quickstarts/analyze-text/python/3.x/quickstart-call-endpoint-3-6.py)]

2. <span data-ttu-id="b8f55-128">Replace the value of the `Ocp-Apim-Subscription-Key` field with your LUIS endpoint key.</span><span class="sxs-lookup"><span data-stu-id="b8f55-128">Replace the value of the `Ocp-Apim-Subscription-Key` field with your LUIS endpoint key.</span></span>

3. <span data-ttu-id="b8f55-129">Install dependencies with `pip install requests`.</span><span class="sxs-lookup"><span data-stu-id="b8f55-129">Install dependencies with `pip install requests`.</span></span>

4. <span data-ttu-id="b8f55-130">Run the script with `python ./quickstart-call-endpoint.py`.</span><span class="sxs-lookup"><span data-stu-id="b8f55-130">Run the script with `python ./quickstart-call-endpoint.py`.</span></span> <span data-ttu-id="b8f55-131">It displays the same JSON that you saw earlier in the browser window.</span><span class="sxs-lookup"><span data-stu-id="b8f55-131">It displays the same JSON that you saw earlier in the browser window.</span></span>
<!-- 
![Console window displays JSON result from LUIS](./media/luis-get-started-python-get-intent/console-turn-on.png)
-->

## <a name="clean-up-resources"></a><span data-ttu-id="b8f55-132">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="b8f55-132">Clean up resources</span></span>
<span data-ttu-id="b8f55-133">The two resources created in this tutorial are the LUIS endpoint key and the C# project.</span><span class="sxs-lookup"><span data-stu-id="b8f55-133">The two resources created in this tutorial are the LUIS endpoint key and the C# project.</span></span> <span data-ttu-id="b8f55-134">Delete the LUIS endpoint key from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="b8f55-134">Delete the LUIS endpoint key from the Azure portal.</span></span> <span data-ttu-id="b8f55-135">Close the Visual Studio project and remove the directory from the file system.</span><span class="sxs-lookup"><span data-stu-id="b8f55-135">Close the Visual Studio project and remove the directory from the file system.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="b8f55-136">Next steps</span><span class="sxs-lookup"><span data-stu-id="b8f55-136">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="b8f55-137">Add utterances</span><span class="sxs-lookup"><span data-stu-id="b8f55-137">Add utterances</span></span>](luis-get-started-python-add-utterance.md)