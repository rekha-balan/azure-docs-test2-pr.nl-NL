---
title: Get started with the Microsoft Speech Recognition API in JavaScript | Microsoft Docs
description: Use the Microsoft Speech Recognition API in Cognitive Services to develop applications that continuously convert spoken audio to text.
services: cognitive-services
author: zhouwangzw
manager: wolfma
ms.service: cognitive-services
ms.component: bing-speech
ms.topic: article
ms.date: 12/21/2017
ms.author: zhouwang
ms.openlocfilehash: 04332c453d22122e65a758a65b09e17300e07f02
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867736"
---
# <a name="get-started-with-the-speech-recognition-api-in-javascript"></a><span data-ttu-id="0b484-103">Get started with the Speech Recognition API in JavaScript</span><span class="sxs-lookup"><span data-stu-id="0b484-103">Get started with the Speech Recognition API in JavaScript</span></span>

<span data-ttu-id="0b484-104">You can develop applications that convert spoken audio to text by using the Speech Recognition API.</span><span class="sxs-lookup"><span data-stu-id="0b484-104">You can develop applications that convert spoken audio to text by using the Speech Recognition API.</span></span> <span data-ttu-id="0b484-105">The JavaScript client library uses the [Speech Service WebSocket protocol](../API-Reference-REST/websocketprotocol.md), which allows you to talk and receive transcribed text simultaneously.</span><span class="sxs-lookup"><span data-stu-id="0b484-105">The JavaScript client library uses the [Speech Service WebSocket protocol](../API-Reference-REST/websocketprotocol.md), which allows you to talk and receive transcribed text simultaneously.</span></span> <span data-ttu-id="0b484-106">This article helps you to get started with the Speech Recognition API in JavaScript.</span><span class="sxs-lookup"><span data-stu-id="0b484-106">This article helps you to get started with the Speech Recognition API in JavaScript.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0b484-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="0b484-107">Prerequisites</span></span>

### <a name="subscribe-to-the-speech-recognition-api-and-get-a-free-trial-subscription-key"></a><span data-ttu-id="0b484-108">Subscribe to the Speech Recognition API, and get a free trial subscription key</span><span class="sxs-lookup"><span data-stu-id="0b484-108">Subscribe to the Speech Recognition API, and get a free trial subscription key</span></span>

<span data-ttu-id="0b484-109">The Speech API is part of Cognitive Services.</span><span class="sxs-lookup"><span data-stu-id="0b484-109">The Speech API is part of Cognitive Services.</span></span> <span data-ttu-id="0b484-110">You can get free trial subscription keys from the [Cognitive Services subscription](https://azure.microsoft.com/try/cognitive-services/) page.</span><span class="sxs-lookup"><span data-stu-id="0b484-110">You can get free trial subscription keys from the [Cognitive Services subscription](https://azure.microsoft.com/try/cognitive-services/) page.</span></span> <span data-ttu-id="0b484-111">After you select the Speech API, select **Get API Key** to get the key.</span><span class="sxs-lookup"><span data-stu-id="0b484-111">After you select the Speech API, select **Get API Key** to get the key.</span></span> <span data-ttu-id="0b484-112">It returns a primary and secondary key.</span><span class="sxs-lookup"><span data-stu-id="0b484-112">It returns a primary and secondary key.</span></span> <span data-ttu-id="0b484-113">Both keys are tied to the same quota, so you can use either key.</span><span class="sxs-lookup"><span data-stu-id="0b484-113">Both keys are tied to the same quota, so you can use either key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0b484-114">Get a subscription key.</span><span class="sxs-lookup"><span data-stu-id="0b484-114">Get a subscription key.</span></span> <span data-ttu-id="0b484-115">Before you can use Speech client libraries, you must have a [subscription key](https://azure.microsoft.com/try/cognitive-services/).</span><span class="sxs-lookup"><span data-stu-id="0b484-115">Before you can use Speech client libraries, you must have a [subscription key](https://azure.microsoft.com/try/cognitive-services/).</span></span>

## <a name="get-started"></a><span data-ttu-id="0b484-116">Get started</span><span class="sxs-lookup"><span data-stu-id="0b484-116">Get started</span></span>

<span data-ttu-id="0b484-117">In this section we will walk you through the necessary steps to load a sample HTML page.</span><span class="sxs-lookup"><span data-stu-id="0b484-117">In this section we will walk you through the necessary steps to load a sample HTML page.</span></span> <span data-ttu-id="0b484-118">The sample is located in our [github repository](https://github.com/Azure-Samples/SpeechToText-WebSockets-Javascript).</span><span class="sxs-lookup"><span data-stu-id="0b484-118">The sample is located in our [github repository](https://github.com/Azure-Samples/SpeechToText-WebSockets-Javascript).</span></span> <span data-ttu-id="0b484-119">You can **open the sample directly** from the repository, or **open the sample from a local copy** of the repository.</span><span class="sxs-lookup"><span data-stu-id="0b484-119">You can **open the sample directly** from the repository, or **open the sample from a local copy** of the repository.</span></span> 

> [!NOTE]
> <span data-ttu-id="0b484-120">Some browsers block microphone access on un-secure origin.</span><span class="sxs-lookup"><span data-stu-id="0b484-120">Some browsers block microphone access on un-secure origin.</span></span> <span data-ttu-id="0b484-121">So, it is recommended to host the 'sample'/'your app' on https to get it working on all supported browsers.</span><span class="sxs-lookup"><span data-stu-id="0b484-121">So, it is recommended to host the 'sample'/'your app' on https to get it working on all supported browsers.</span></span> 

### <a name="open-the-sample-directly"></a><span data-ttu-id="0b484-122">Open the sample directly</span><span class="sxs-lookup"><span data-stu-id="0b484-122">Open the sample directly</span></span>

<span data-ttu-id="0b484-123">Acquire a subscription key as described above.</span><span class="sxs-lookup"><span data-stu-id="0b484-123">Acquire a subscription key as described above.</span></span> <span data-ttu-id="0b484-124">Then open the [link to the sample](https://htmlpreview.github.io/?https://github.com/Azure-Samples/SpeechToText-WebSockets-Javascript/blob/preview/samples/browser/Sample.html).</span><span class="sxs-lookup"><span data-stu-id="0b484-124">Then open the [link to the sample](https://htmlpreview.github.io/?https://github.com/Azure-Samples/SpeechToText-WebSockets-Javascript/blob/preview/samples/browser/Sample.html).</span></span> <span data-ttu-id="0b484-125">This will load the page into your default browser (Rendered using [htmlPreview](https://github.com/htmlpreview/htmlpreview.github.com)).</span><span class="sxs-lookup"><span data-stu-id="0b484-125">This will load the page into your default browser (Rendered using [htmlPreview](https://github.com/htmlpreview/htmlpreview.github.com)).</span></span>

### <a name="open-the-sample-from-a-local-copy"></a><span data-ttu-id="0b484-126">Open the sample from a local copy</span><span class="sxs-lookup"><span data-stu-id="0b484-126">Open the sample from a local copy</span></span>

<span data-ttu-id="0b484-127">To try the sample locally, clone this repository:</span><span class="sxs-lookup"><span data-stu-id="0b484-127">To try the sample locally, clone this repository:</span></span>

```
git clone https://github.com/Azure-Samples/SpeechToText-WebSockets-Javascript
```

<span data-ttu-id="0b484-128">compile the TypeScript sources and bundle them into a single JavaScript file ([npm](https://www.npmjs.com/) needs to be installed on your machine).</span><span class="sxs-lookup"><span data-stu-id="0b484-128">compile the TypeScript sources and bundle them into a single JavaScript file ([npm](https://www.npmjs.com/) needs to be installed on your machine).</span></span> <span data-ttu-id="0b484-129">Change into the root of the cloned repository and run the commands:</span><span class="sxs-lookup"><span data-stu-id="0b484-129">Change into the root of the cloned repository and run the commands:</span></span>

```
cd SpeechToText-WebSockets-Javascript && npm run bundle
```

<span data-ttu-id="0b484-130">Open `samples\browser\Sample.html` in your favorite browser.</span><span class="sxs-lookup"><span data-stu-id="0b484-130">Open `samples\browser\Sample.html` in your favorite browser.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0b484-131">Next steps</span><span class="sxs-lookup"><span data-stu-id="0b484-131">Next steps</span></span>

<span data-ttu-id="0b484-132">More information on how to include the SDK into your own webpage is available [here](https://github.com/Azure-Samples/SpeechToText-WebSockets-Javascript).</span><span class="sxs-lookup"><span data-stu-id="0b484-132">More information on how to include the SDK into your own webpage is available [here](https://github.com/Azure-Samples/SpeechToText-WebSockets-Javascript).</span></span>

## <a name="remarks"></a><span data-ttu-id="0b484-133">Remarks</span><span class="sxs-lookup"><span data-stu-id="0b484-133">Remarks</span></span>

- <span data-ttu-id="0b484-134">The Speech Recognition API supports three [recognition modes](../concepts.md#recognition-modes).</span><span class="sxs-lookup"><span data-stu-id="0b484-134">The Speech Recognition API supports three [recognition modes](../concepts.md#recognition-modes).</span></span> <span data-ttu-id="0b484-135">You can switch the mode by updating the **Setup()** function found in the Sample.html file.</span><span class="sxs-lookup"><span data-stu-id="0b484-135">You can switch the mode by updating the **Setup()** function found in the Sample.html file.</span></span> <span data-ttu-id="0b484-136">The sample sets the mode to `Interactive` by default.</span><span class="sxs-lookup"><span data-stu-id="0b484-136">The sample sets the mode to `Interactive` by default.</span></span> <span data-ttu-id="0b484-137">To change the mode, update the parameter `SR.RecognitionMode.Interactive` to another mode.</span><span class="sxs-lookup"><span data-stu-id="0b484-137">To change the mode, update the parameter `SR.RecognitionMode.Interactive` to another mode.</span></span> <span data-ttu-id="0b484-138">For example, change the parameter to  `SR.RecognitionMode.Conversation`.</span><span class="sxs-lookup"><span data-stu-id="0b484-138">For example, change the parameter to  `SR.RecognitionMode.Conversation`.</span></span>
- <span data-ttu-id="0b484-139">For a complete list of supported languages, see [Supported languages](../API-Reference-REST/supportedlanguages.md).</span><span class="sxs-lookup"><span data-stu-id="0b484-139">For a complete list of supported languages, see [Supported languages](../API-Reference-REST/supportedlanguages.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="0b484-140">Related topics</span><span class="sxs-lookup"><span data-stu-id="0b484-140">Related topics</span></span>

- [<span data-ttu-id="0b484-141">JavaScript Speech Recognition API sample repository</span><span class="sxs-lookup"><span data-stu-id="0b484-141">JavaScript Speech Recognition API sample repository</span></span>](https://github.com/Azure-Samples/SpeechToText-WebSockets-Javascript)
- [<span data-ttu-id="0b484-142">Get started with the REST API</span><span class="sxs-lookup"><span data-stu-id="0b484-142">Get started with the REST API</span></span>](GetStartedREST.md)
