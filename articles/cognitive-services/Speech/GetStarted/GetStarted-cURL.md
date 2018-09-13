---
title: Get started with the Bing Speech API using cURL | Microsoft Docs
description: Apply the Bing Speech Recognition API in Microsoft Cognitive Services by using cURL to convert spoken audio to text.
services: cognitive-services
author: priyaravi20
manager: yanbo
ms.service: cognitive-services
ms.technology: speech
ms.topic: article
ms.date: 03/16/2017
ms.author: prrajan
ms.openlocfilehash: 9045906f1c6280010e59830e42494cb025e02e1d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563166"
---
# <a name="get-started-with-bing-speech-api-in-curl"></a><span data-ttu-id="1d73b-103">Get Started with Bing Speech API in cURL</span><span class="sxs-lookup"><span data-stu-id="1d73b-103">Get Started with Bing Speech API in cURL</span></span>

<span data-ttu-id="1d73b-104">Exercise Bing Speech Recognition API using cURL to convert spoken audio to text by sending audio to Microsoft’s servers in the cloud.</span><span class="sxs-lookup"><span data-stu-id="1d73b-104">Exercise Bing Speech Recognition API using cURL to convert spoken audio to text by sending audio to Microsoft’s servers in the cloud.</span></span> <span data-ttu-id="1d73b-105">The example below is **bash** commands that demonstrates the use of Microsoft Cognitive Services (formerly Project Oxford) Speech To Text API using **cURL**.</span><span class="sxs-lookup"><span data-stu-id="1d73b-105">The example below is **bash** commands that demonstrates the use of Microsoft Cognitive Services (formerly Project Oxford) Speech To Text API using **cURL**.</span></span>

<span data-ttu-id="1d73b-106">The Speech Recognition web example demonstrates the following features using a wav file or external microphone input:</span><span class="sxs-lookup"><span data-stu-id="1d73b-106">The Speech Recognition web example demonstrates the following features using a wav file or external microphone input:</span></span>
 * <span data-ttu-id="1d73b-107">Access token generation</span><span class="sxs-lookup"><span data-stu-id="1d73b-107">Access token generation</span></span>
 * <span data-ttu-id="1d73b-108">Short-form recognition This example assumes that **cURL** is available in your bash environment.</span><span class="sxs-lookup"><span data-stu-id="1d73b-108">Short-form recognition This example assumes that **cURL** is available in your bash environment.</span></span>

## <a name="Prerequisites"></a><span data-ttu-id="1d73b-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="1d73b-109">Prerequisites</span></span>
* #### <a name="platform-requirements"></a><span data-ttu-id="1d73b-110">Platform requirements</span><span class="sxs-lookup"><span data-stu-id="1d73b-110">Platform requirements</span></span>
<span data-ttu-id="1d73b-111">The below example has been developed in **bash**.</span><span class="sxs-lookup"><span data-stu-id="1d73b-111">The below example has been developed in **bash**.</span></span> <span data-ttu-id="1d73b-112">(Also works in git bash/zsh/etc)</span><span class="sxs-lookup"><span data-stu-id="1d73b-112">(Also works in git bash/zsh/etc)</span></span>

* #### <a name="subscribe-to-speech-api-and-get-a-free-trial-subscription-key"></a><span data-ttu-id="1d73b-113">Subscribe to Speech API and get a free trial subscription key</span><span class="sxs-lookup"><span data-stu-id="1d73b-113">Subscribe to Speech API and get a free trial subscription key</span></span>
<span data-ttu-id="1d73b-114">Before creating the example, you must subscribe to Speech API which is part of Microsoft Cognitive Services.</span><span class="sxs-lookup"><span data-stu-id="1d73b-114">Before creating the example, you must subscribe to Speech API which is part of Microsoft Cognitive Services.</span></span> <span data-ttu-id="1d73b-115">For subscription and key management details, see [Subscriptions](https://www.microsoft.com/cognitive-services/en-us/sign-up).</span><span class="sxs-lookup"><span data-stu-id="1d73b-115">For subscription and key management details, see [Subscriptions](https://www.microsoft.com/cognitive-services/en-us/sign-up).</span></span> <span data-ttu-id="1d73b-116">Both the primary and secondary key can be used in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="1d73b-116">Both the primary and secondary key can be used in this tutorial.</span></span>

## <a name="Step1"></a><span data-ttu-id="1d73b-117">Step 1: Generate an Access Token</span><span class="sxs-lookup"><span data-stu-id="1d73b-117">Step 1: Generate an Access Token</span></span>
1.  <span data-ttu-id="1d73b-118">Replace **your_subscription_key** with your own subscription key and run the command in **bash**.</span><span class="sxs-lookup"><span data-stu-id="1d73b-118">Replace **your_subscription_key** with your own subscription key and run the command in **bash**.</span></span>

    `curl -v -X POST "https://api.cognitive.microsoft.com/sts/v1.0/issueToken" -H "Content-type: application/x-www-form-urlencoded" -H "Content-Length: 0" -H "Ocp-Apim-Subscription-Key: your_subscription_key"`

2.  <span data-ttu-id="1d73b-119">The response is a string with the JSON Web Token (JWT) access token.</span><span class="sxs-lookup"><span data-stu-id="1d73b-119">The response is a string with the JSON Web Token (JWT) access token.</span></span>
    `JWT access token`

## <a name="Step2"></a><span data-ttu-id="1d73b-120">Step 2: Upload the Audio Binary</span><span class="sxs-lookup"><span data-stu-id="1d73b-120">Step 2: Upload the Audio Binary</span></span>
1. <span data-ttu-id="1d73b-121">Replace **your_instance_id**, **your_request_id**, **your_locale**, **your_device_os** in accordance to your own application</span><span class="sxs-lookup"><span data-stu-id="1d73b-121">Replace **your_instance_id**, **your_request_id**, **your_locale**, **your_device_os** in accordance to your own application</span></span>
2. <span data-ttu-id="1d73b-122">Replace **your_access_token** with the JWT access token retrieved from [Step 1](#Step1)</span><span class="sxs-lookup"><span data-stu-id="1d73b-122">Replace **your_access_token** with the JWT access token retrieved from [Step 1](#Step1)</span></span>
3. <span data-ttu-id="1d73b-123">Replace **your_wave_file** with the actual wave file</span><span class="sxs-lookup"><span data-stu-id="1d73b-123">Replace **your_wave_file** with the actual wave file</span></span>
4. <span data-ttu-id="1d73b-124">Run the command in **bash**</span><span class="sxs-lookup"><span data-stu-id="1d73b-124">Run the command in **bash**</span></span>

    `curl -v -X POST "https://speech.platform.bing.com/recognize?scenarios=smd&appid=D4D52672-91D7-4C74-8AD8-42B1D98141A5&locale=your_locale&device.os=your_device_os&version=3.0&format=json&instanceid=your_instance_id&requestid=your_request_id" -H 'Authorization: Bearer your_access_token' -H 'Content-type: audio/wav; codec="audio/pcm"; samplerate=16000' --data-binary @your_wave_file`

5. <span data-ttu-id="1d73b-125">Parse the Succcessful recognition response or Error response</span><span class="sxs-lookup"><span data-stu-id="1d73b-125">Parse the Succcessful recognition response or Error response</span></span>

## <a name="Related"></a><span data-ttu-id="1d73b-126">Related Topics</span><span class="sxs-lookup"><span data-stu-id="1d73b-126">Related Topics</span></span>
* [<span data-ttu-id="1d73b-127">Get Started with Bing Speech Recognition in C Sharp for .Net on Windows Desktop</span><span class="sxs-lookup"><span data-stu-id="1d73b-127">Get Started with Bing Speech Recognition in C Sharp for .Net on Windows Desktop</span></span>](GetStartedCSharpDesktop.md)
* [<span data-ttu-id="1d73b-128">Get Started with Bing Speech Recognition in Java on Android</span><span class="sxs-lookup"><span data-stu-id="1d73b-128">Get Started with Bing Speech Recognition in Java on Android</span></span>](GetStartedJavaAndroid.md)
* [<span data-ttu-id="1d73b-129">Get Started with Bing Speech Recognition in JavaScript</span><span class="sxs-lookup"><span data-stu-id="1d73b-129">Get Started with Bing Speech Recognition in JavaScript</span></span>](GetStartedJS.md)
* [<span data-ttu-id="1d73b-130">Get Started with Bing Speech Recognition in Objective C on iOS</span><span class="sxs-lookup"><span data-stu-id="1d73b-130">Get Started with Bing Speech Recognition in Objective C on iOS</span></span>](Get-Started-ObjectiveC-iOS.md)

<span data-ttu-id="1d73b-131">For questions, feedback, or suggestions about Microsoft Cognitive Services, feel free to reach out to us directly.</span><span class="sxs-lookup"><span data-stu-id="1d73b-131">For questions, feedback, or suggestions about Microsoft Cognitive Services, feel free to reach out to us directly.</span></span>

 * <span data-ttu-id="1d73b-132">Cognitive Services [UserVoice Forum](https://cognitive.uservoice.com/)</span><span class="sxs-lookup"><span data-stu-id="1d73b-132">Cognitive Services [UserVoice Forum](https://cognitive.uservoice.com/)</span></span>

### <a name="license"></a><span data-ttu-id="1d73b-133">License</span><span class="sxs-lookup"><span data-stu-id="1d73b-133">License</span></span>

<span data-ttu-id="1d73b-134">All Microsoft Cognitive Services SDKs and samples are licensed with the MIT License.</span><span class="sxs-lookup"><span data-stu-id="1d73b-134">All Microsoft Cognitive Services SDKs and samples are licensed with the MIT License.</span></span> <span data-ttu-id="1d73b-135">For more details, see [LICENSE](https://github.com/Microsoft/Cognitive-Speech-STT-JavaScript/blob/master/LICENSE.md).</span><span class="sxs-lookup"><span data-stu-id="1d73b-135">For more details, see [LICENSE](https://github.com/Microsoft/Cognitive-Speech-STT-JavaScript/blob/master/LICENSE.md).</span></span>
