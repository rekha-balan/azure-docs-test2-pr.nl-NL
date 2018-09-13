---
title: Get Started with the Bing Speech API using JavaScript | Microsoft Docs
description: Use the Bing Speech API in Microsoft Cognitive Services to develop basic JavaScript applications that convert spoken audio to text.
services: cognitive-services
author: priyaravi20
manager: yanbo
ms.service: cognitive-services
ms.technology: speech
ms.topic: article
ms.date: 12/09/2016
ms.author: prrajan
ms.openlocfilehash: 6791dc97937386a2abb3955e99dcb3b474c4085c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556498"
---
# <a name="get-started-with-bing-speech-api-in-javascript"></a><span data-ttu-id="3d900-103">Get Started with Bing Speech API in JavaScript</span><span class="sxs-lookup"><span data-stu-id="3d900-103">Get Started with Bing Speech API in JavaScript</span></span>

<span data-ttu-id="3d900-104">With Bing Speech API you can develop basic JavaScript applications that leverage Microsoft’s cloud servers to convert spoken audio to text.</span><span class="sxs-lookup"><span data-stu-id="3d900-104">With Bing Speech API you can develop basic JavaScript applications that leverage Microsoft’s cloud servers to convert spoken audio to text.</span></span> <span data-ttu-id="3d900-105">This article describes an example web application created in Visual Studio 2015 that demonstrates the use of Bing Speech API using Javascript.</span><span class="sxs-lookup"><span data-stu-id="3d900-105">This article describes an example web application created in Visual Studio 2015 that demonstrates the use of Bing Speech API using Javascript.</span></span>

<span data-ttu-id="3d900-106">The Speech Recognition example demonstrates the following features using a wav file or external microphone input:</span><span class="sxs-lookup"><span data-stu-id="3d900-106">The Speech Recognition example demonstrates the following features using a wav file or external microphone input:</span></span>
 * <span data-ttu-id="3d900-107">Short-form recognition</span><span class="sxs-lookup"><span data-stu-id="3d900-107">Short-form recognition</span></span>
 * <span data-ttu-id="3d900-108">Recognition with intent</span><span class="sxs-lookup"><span data-stu-id="3d900-108">Recognition with intent</span></span>

<span data-ttu-id="3d900-109">To use Speech.JS, simply host Speech.1.0.0.js on your website.</span><span class="sxs-lookup"><span data-stu-id="3d900-109">To use Speech.JS, simply host Speech.1.0.0.js on your website.</span></span> <span data-ttu-id="3d900-110">A 'minified' version of Speech.JS is also available Speech.1.0.0.min.js.</span><span class="sxs-lookup"><span data-stu-id="3d900-110">A 'minified' version of Speech.JS is also available Speech.1.0.0.min.js.</span></span>

<span data-ttu-id="3d900-111"><a name="Prerequisites"> </a></span><span class="sxs-lookup"><span data-stu-id="3d900-111"><a name="Prerequisites"> </a></span></span>
## <a name="prerequisites"></a><span data-ttu-id="3d900-112">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="3d900-112">Prerequisites</span></span>

#### <a name="platform-requirements"></a><span data-ttu-id="3d900-113">Platform requirements</span><span class="sxs-lookup"><span data-stu-id="3d900-113">Platform requirements</span></span>
<span data-ttu-id="3d900-114">The below example has been developed for the .NET Framework using [Visual Studio 2015, Community Edition](https://www.visualstudio.com/products/visual-studio-community-vs).</span><span class="sxs-lookup"><span data-stu-id="3d900-114">The below example has been developed for the .NET Framework using [Visual Studio 2015, Community Edition](https://www.visualstudio.com/products/visual-studio-community-vs).</span></span>

#### <a name="get-the-client-library-and-example"></a><span data-ttu-id="3d900-115">Get the client library and example</span><span class="sxs-lookup"><span data-stu-id="3d900-115">Get the client library and example</span></span>
<span data-ttu-id="3d900-116">You may download the Speech API client library and example through  [GitHub](https://github.com/Microsoft/Cognitive-Speech-STT-JavaScript).</span><span class="sxs-lookup"><span data-stu-id="3d900-116">You may download the Speech API client library and example through  [GitHub](https://github.com/Microsoft/Cognitive-Speech-STT-JavaScript).</span></span> <span data-ttu-id="3d900-117">The downloaded folder needs to be hosted locally on your machine to follow the below scenario.</span><span class="sxs-lookup"><span data-stu-id="3d900-117">The downloaded folder needs to be hosted locally on your machine to follow the below scenario.</span></span>

#### <a name="subscribe-to-speech-api-and-get-a-free-trial-subscription-key"></a><span data-ttu-id="3d900-118">Subscribe to Speech API and get a free trial subscription key</span><span class="sxs-lookup"><span data-stu-id="3d900-118">Subscribe to Speech API and get a free trial subscription key</span></span>
<span data-ttu-id="3d900-119">Before creating the example, you must subscribe to Speech API which is part of Microsoft Cognitive Services (previously Project Oxford).</span><span class="sxs-lookup"><span data-stu-id="3d900-119">Before creating the example, you must subscribe to Speech API which is part of Microsoft Cognitive Services (previously Project Oxford).</span></span> <span data-ttu-id="3d900-120">For subscription and key management details, see [Subscriptions](https://www.microsoft.com/cognitive-services/en-us/sign-up).</span><span class="sxs-lookup"><span data-stu-id="3d900-120">For subscription and key management details, see [Subscriptions](https://www.microsoft.com/cognitive-services/en-us/sign-up).</span></span> <span data-ttu-id="3d900-121">Both the primary and secondary key can be used in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="3d900-121">Both the primary and secondary key can be used in this tutorial.</span></span>

<span data-ttu-id="3d900-122"><a name="Step1"> </a></span><span class="sxs-lookup"><span data-stu-id="3d900-122"><a name="Step1"> </a></span></span>
## <a name="step-1-install-the-example-applicationa"></a><span data-ttu-id="3d900-123">Step 1: Install the Example Application</a></span><span class="sxs-lookup"><span data-stu-id="3d900-123">Step 1: Install the Example Application</a></span></span>
1.  <span data-ttu-id="3d900-124">Start Microsoft Visual Studio 2015 and click **File**, select **Open**, then **Project/Solution**.</span><span class="sxs-lookup"><span data-stu-id="3d900-124">Start Microsoft Visual Studio 2015 and click **File**, select **Open**, then **Project/Solution**.</span></span>
2.  <span data-ttu-id="3d900-125">Browse to the folder where you saved the downloaded Speech.JS files.</span><span class="sxs-lookup"><span data-stu-id="3d900-125">Browse to the folder where you saved the downloaded Speech.JS files.</span></span> <span data-ttu-id="3d900-126">Click on **Speech** and then the **Speech.JS**folder.</span><span class="sxs-lookup"><span data-stu-id="3d900-126">Click on **Speech** and then the **Speech.JS**folder.</span></span>
3.  <span data-ttu-id="3d900-127">Double-click to open the Visual Studio 2015 Solution (.sln) file named **Oxford.Speech.JS.sln**.</span><span class="sxs-lookup"><span data-stu-id="3d900-127">Double-click to open the Visual Studio 2015 Solution (.sln) file named **Oxford.Speech.JS.sln**.</span></span> <span data-ttu-id="3d900-128">This will open the solution in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3d900-128">This will open the solution in Visual Studio.</span></span>

<span data-ttu-id="3d900-129"><a name="Step2"> </a></span><span class="sxs-lookup"><span data-stu-id="3d900-129"><a name="Step2"> </a></span></span>
## <a name="step-2-build-the-example-application"></a><span data-ttu-id="3d900-130">Step 2: Build the Example Application</span><span class="sxs-lookup"><span data-stu-id="3d900-130">Step 2: Build the Example Application</span></span>
1.  <span data-ttu-id="3d900-131">Press Ctrl+Shift+B, or click **Build** on the ribbon menu, then select **Build Solution**.</span><span class="sxs-lookup"><span data-stu-id="3d900-131">Press Ctrl+Shift+B, or click **Build** on the ribbon menu, then select **Build Solution**.</span></span>

<span data-ttu-id="3d900-132"><a name="Step3"> </a></span><span class="sxs-lookup"><span data-stu-id="3d900-132"><a name="Step3"> </a></span></span>
## <a name="step-3-run-the-example-application"></a><span data-ttu-id="3d900-133">Step 3: Run the Example Application</span><span class="sxs-lookup"><span data-stu-id="3d900-133">Step 3: Run the Example Application</span></span>
1.  <span data-ttu-id="3d900-134">After the build is complete, choose the target browser you would like to use for running your Speech-to-Text web app.</span><span class="sxs-lookup"><span data-stu-id="3d900-134">After the build is complete, choose the target browser you would like to use for running your Speech-to-Text web app.</span></span>
<span data-ttu-id="3d900-135">![Speech choose emulator](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/Speech/Images/SelectEmulator.png)</span><span class="sxs-lookup"><span data-stu-id="3d900-135">![Speech choose emulator](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/Speech/Images/SelectEmulator.png)</span></span>
2.  <span data-ttu-id="3d900-136">Press **F5** or click **Start** on the ribbon menu to run the example.</span><span class="sxs-lookup"><span data-stu-id="3d900-136">Press **F5** or click **Start** on the ribbon menu to run the example.</span></span>
3.  <span data-ttu-id="3d900-137">Locate the **Cognitive Services Speech to Text** window with the **text edit box** reading **"Subscription"**.</span><span class="sxs-lookup"><span data-stu-id="3d900-137">Locate the **Cognitive Services Speech to Text** window with the **text edit box** reading **"Subscription"**.</span></span> <span data-ttu-id="3d900-138">Paste your subscription key into the subscription text box.</span><span class="sxs-lookup"><span data-stu-id="3d900-138">Paste your subscription key into the subscription text box.</span></span>
4. <span data-ttu-id="3d900-139">Check if you would like to use the Microphone as your voice input and what speech mode you would like to use by selecting a setting in the "Mode" drop-down box.</span><span class="sxs-lookup"><span data-stu-id="3d900-139">Check if you would like to use the Microphone as your voice input and what speech mode you would like to use by selecting a setting in the "Mode" drop-down box.</span></span>
5. <span data-ttu-id="3d900-140">For modes where you would like both Speech Recognition and Intent to work together, you need to first sign up for [Language Understanding Intelligent Service (LUIS)](https://www.luis.ai/), then set the key values in the fields "LUIS AppID" and "LUIS SubscriptionId".</span><span class="sxs-lookup"><span data-stu-id="3d900-140">For modes where you would like both Speech Recognition and Intent to work together, you need to first sign up for [Language Understanding Intelligent Service (LUIS)](https://www.luis.ai/), then set the key values in the fields "LUIS AppID" and "LUIS SubscriptionId".</span></span>

<span data-ttu-id="3d900-141"><a name="Related"> </a></span><span class="sxs-lookup"><span data-stu-id="3d900-141"><a name="Related"> </a></span></span>
## <a name="related-topics"></a><span data-ttu-id="3d900-142">Related Topics</span><span class="sxs-lookup"><span data-stu-id="3d900-142">Related Topics</span></span> 
* [<span data-ttu-id="3d900-143">Get Started with Bing Speech Recognition in C Sharp for .Net on Windows Desktop</span><span class="sxs-lookup"><span data-stu-id="3d900-143">Get Started with Bing Speech Recognition in C Sharp for .Net on Windows Desktop</span></span>](GetStartedCSharpDesktop.md)
* [<span data-ttu-id="3d900-144">Get started with Bing Speech Recognition and/or intent in Java on Android</span><span class="sxs-lookup"><span data-stu-id="3d900-144">Get started with Bing Speech Recognition and/or intent in Java on Android</span></span>](GetStartedJavaAndroid.md)
* [<span data-ttu-id="3d900-145">Get started with Bing Speech Recognition and/or intent in Objective C on iOS</span><span class="sxs-lookup"><span data-stu-id="3d900-145">Get started with Bing Speech Recognition and/or intent in Objective C on iOS</span></span>](Get-Started-ObjectiveC-iOS.md)
* [<span data-ttu-id="3d900-146">Get started with Bing Speech API in cURL</span><span class="sxs-lookup"><span data-stu-id="3d900-146">Get started with Bing Speech API in cURL</span></span>](GetStarted-cURL.md)

<span data-ttu-id="3d900-147">For questions, feedback, or suggestions about Microsoft Cognitive Services, feel free to reach out to us directly.</span><span class="sxs-lookup"><span data-stu-id="3d900-147">For questions, feedback, or suggestions about Microsoft Cognitive Services, feel free to reach out to us directly.</span></span>

* <span data-ttu-id="3d900-148">Cognitive Services [UserVoice Forum](https://cognitive.uservoice.com/)</span><span class="sxs-lookup"><span data-stu-id="3d900-148">Cognitive Services [UserVoice Forum](https://cognitive.uservoice.com/)</span></span>

#### <a name="license"></a><span data-ttu-id="3d900-149">License</span><span class="sxs-lookup"><span data-stu-id="3d900-149">License</span></span>

<span data-ttu-id="3d900-150">All Microsoft Cognitive Services SDKs and samples are licensed with the MIT License.</span><span class="sxs-lookup"><span data-stu-id="3d900-150">All Microsoft Cognitive Services SDKs and samples are licensed with the MIT License.</span></span> <span data-ttu-id="3d900-151">For more details, see [LICENSE](https://github.com/Microsoft/Cognitive-Speech-STT-JavaScript/blob/master/LICENSE.md).</span><span class="sxs-lookup"><span data-stu-id="3d900-151">For more details, see [LICENSE](https://github.com/Microsoft/Cognitive-Speech-STT-JavaScript/blob/master/LICENSE.md).</span></span>

