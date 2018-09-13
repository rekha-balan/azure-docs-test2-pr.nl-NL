---
title: Cognitive Services Speech SDK Troubleshooting
description: Trouble Shooting Cognitive Services Speech SDK
titleSuffix: Microsoft Cognitive Services
services: cognitive-services
author: wolfma61
ms.service: cognitive-services
ms.component: speech-service
ms.topic: article
ms.date: 05/07/2018
ms.author: wolfma
ms.openlocfilehash: ff8aba562cfd2d6d54c708ee7fdc4c6ca7185f29
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869953"
---
# <a name="troubleshooting-speech-services-sdk"></a><span data-ttu-id="084c6-103">Troubleshooting Speech Services SDK</span><span class="sxs-lookup"><span data-stu-id="084c6-103">Troubleshooting Speech Services SDK</span></span>

<span data-ttu-id="084c6-104">This article provides information to help you solve issues you might encounter when using the Speech SDK.</span><span class="sxs-lookup"><span data-stu-id="084c6-104">This article provides information to help you solve issues you might encounter when using the Speech SDK.</span></span>

## <a name="error-websocket-upgrade-failed-with-an-authentication-error-403"></a><span data-ttu-id="084c6-105">Error `WebSocket Upgrade failed with an authentication error (403).`</span><span class="sxs-lookup"><span data-stu-id="084c6-105">Error `WebSocket Upgrade failed with an authentication error (403).`</span></span>

<span data-ttu-id="084c6-106">You may have the wrong endpoint for your region or service.</span><span class="sxs-lookup"><span data-stu-id="084c6-106">You may have the wrong endpoint for your region or service.</span></span> <span data-ttu-id="084c6-107">Double-check the URI to make sure it is correct.</span><span class="sxs-lookup"><span data-stu-id="084c6-107">Double-check the URI to make sure it is correct.</span></span> <span data-ttu-id="084c6-108">Also see the next section, as this could also be a problem with your subscription key or authorization token.</span><span class="sxs-lookup"><span data-stu-id="084c6-108">Also see the next section, as this could also be a problem with your subscription key or authorization token.</span></span>

## <a name="error-http-403-forbidden-or-error-http-401-unauthorized"></a><span data-ttu-id="084c6-109">Error `HTTP 403 Forbidden` or Error `HTTP 401 Unauthorized`</span><span class="sxs-lookup"><span data-stu-id="084c6-109">Error `HTTP 403 Forbidden` or Error `HTTP 401 Unauthorized`</span></span>

<span data-ttu-id="084c6-110">This error is often caused by authentication issues.</span><span class="sxs-lookup"><span data-stu-id="084c6-110">This error is often caused by authentication issues.</span></span> <span data-ttu-id="084c6-111">Connection requests without a valid `Ocp-Apim-Subscription-Key` or `Authorization` header are rejected with status 401 or 403.</span><span class="sxs-lookup"><span data-stu-id="084c6-111">Connection requests without a valid `Ocp-Apim-Subscription-Key` or `Authorization` header are rejected with status 401 or 403.</span></span>

* <span data-ttu-id="084c6-112">If you are using a subscription key for authentication, the cause could be:</span><span class="sxs-lookup"><span data-stu-id="084c6-112">If you are using a subscription key for authentication, the cause could be:</span></span>

    - <span data-ttu-id="084c6-113">the subscription key is missing or invalid</span><span class="sxs-lookup"><span data-stu-id="084c6-113">the subscription key is missing or invalid</span></span>
    - <span data-ttu-id="084c6-114">you have exceeded your subscription's usage quota</span><span class="sxs-lookup"><span data-stu-id="084c6-114">you have exceeded your subscription's usage quota</span></span>

* <span data-ttu-id="084c6-115">If you are using an authorization token for authentication, the cause could be:</span><span class="sxs-lookup"><span data-stu-id="084c6-115">If you are using an authorization token for authentication, the cause could be:</span></span>

    - <span data-ttu-id="084c6-116">the authorization token is invalid</span><span class="sxs-lookup"><span data-stu-id="084c6-116">the authorization token is invalid</span></span>
    - <span data-ttu-id="084c6-117">the authorization token is expired</span><span class="sxs-lookup"><span data-stu-id="084c6-117">the authorization token is expired</span></span>

### <a name="validate-your-subscription-key"></a><span data-ttu-id="084c6-118">Validate your subscription key</span><span class="sxs-lookup"><span data-stu-id="084c6-118">Validate your subscription key</span></span>

<span data-ttu-id="084c6-119">You can verify to make sure you have a valid subscription key by running one of the commands below.</span><span class="sxs-lookup"><span data-stu-id="084c6-119">You can verify to make sure you have a valid subscription key by running one of the commands below.</span></span>

> [!NOTE]
> <span data-ttu-id="084c6-120">Replace `YOUR_SUBSCRIPTION_KEY` and `YOUR_REGION` with your own subscription key and associated region, respectively.</span><span class="sxs-lookup"><span data-stu-id="084c6-120">Replace `YOUR_SUBSCRIPTION_KEY` and `YOUR_REGION` with your own subscription key and associated region, respectively.</span></span>

* <span data-ttu-id="084c6-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="084c6-121">PowerShell</span></span>

    ```Powershell
    $FetchTokenHeader = @{
      'Content-type'='application/x-www-form-urlencoded'
      'Content-Length'= '0'
      'Ocp-Apim-Subscription-Key' = 'YOUR_SUBSCRIPTION_KEY'
    }
    $OAuthToken = Invoke-RestMethod -Method POST -Uri https://YOUR_REGION.api.cognitive.microsoft.com/sts/v1.0/issueToken -Headers $FetchTokenHeader
    $OAuthToken
    ```

* <span data-ttu-id="084c6-122">cURL</span><span class="sxs-lookup"><span data-stu-id="084c6-122">cURL</span></span>

    ```
    curl -v -X POST "https://YOUR_REGION.api.cognitive.microsoft.com/sts/v1.0/issueToken" -H "Ocp-Apim-Subscription-Key: YOUR_SUBSCRIPTION_KEY" -H "Content-type: application/x-www-form-urlencoded" -H "Content-Length: 0"
    ```

### <a name="validate-an-authorization-token"></a><span data-ttu-id="084c6-123">Validate an authorization token</span><span class="sxs-lookup"><span data-stu-id="084c6-123">Validate an authorization token</span></span>

<span data-ttu-id="084c6-124">If you use an authorization token for authentication, run one of the following commands to verify that the authorization token is still valid.</span><span class="sxs-lookup"><span data-stu-id="084c6-124">If you use an authorization token for authentication, run one of the following commands to verify that the authorization token is still valid.</span></span> <span data-ttu-id="084c6-125">Tokens are valid for 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="084c6-125">Tokens are valid for 10 minutes.</span></span>

> [!NOTE]
> <span data-ttu-id="084c6-126">Replace `YOUR_AUDIO_FILE` with the path to your prerecorded audio file, `YOUR_ACCESS_TOKEN` with the authorization token returned in the previous step, and `YOUR_REGION` with the correct region.</span><span class="sxs-lookup"><span data-stu-id="084c6-126">Replace `YOUR_AUDIO_FILE` with the path to your prerecorded audio file, `YOUR_ACCESS_TOKEN` with the authorization token returned in the previous step, and `YOUR_REGION` with the correct region.</span></span>

* <span data-ttu-id="084c6-127">PowerShell</span><span class="sxs-lookup"><span data-stu-id="084c6-127">PowerShell</span></span>

    ```Powershell
    $SpeechServiceURI =
    'https://YOUR_REGION.stt.speech.microsoft.com/speech/recognition/interactive/cognitiveservices/v1?language=en-US'
    
    # $OAuthToken is the authorization token returned by the token service.
    $RecoRequestHeader = @{
      'Authorization' = 'Bearer '+ $OAuthToken
      'Transfer-Encoding' = 'chunked'
      'Content-type' = 'audio/wav; codec=audio/pcm; samplerate=16000'
    }
    
    # Read audio into byte array
    $audioBytes = [System.IO.File]::ReadAllBytes("YOUR_AUDIO_FILE")
    
    $RecoResponse = Invoke-RestMethod -Method POST -Uri $SpeechServiceURI -Headers $RecoRequestHeader -Body $audioBytes
    
    # Show the result
    $RecoResponse
    ```

* <span data-ttu-id="084c6-128">cURL</span><span class="sxs-lookup"><span data-stu-id="084c6-128">cURL</span></span>

    ```
    curl -v -X POST "https://YOUR_REGION.stt.speech.microsoft.com/speech/recognition/interactive/cognitiveservices/v1?language=en-US" -H "Authorization: Bearer YOUR_ACCESS_TOKEN" -H "Transfer-Encoding: chunked" -H "Content-type: audio/wav; codec=audio/pcm; samplerate=16000" --data-binary @YOUR_AUDIO_FILE
    ```

---

## <a name="error-http-400-bad-request"></a><span data-ttu-id="084c6-129">Error `HTTP 400 Bad Request`</span><span class="sxs-lookup"><span data-stu-id="084c6-129">Error `HTTP 400 Bad Request`</span></span>

<span data-ttu-id="084c6-130">This error usually occurs when the request body contains invalid audio data.</span><span class="sxs-lookup"><span data-stu-id="084c6-130">This error usually occurs when the request body contains invalid audio data.</span></span> <span data-ttu-id="084c6-131">Only `WAV` format is supported.</span><span class="sxs-lookup"><span data-stu-id="084c6-131">Only `WAV` format is supported.</span></span> <span data-ttu-id="084c6-132">Also check the request's headers to make sure you are specifying an appropriate `Content-Type` and `Content-Length`.</span><span class="sxs-lookup"><span data-stu-id="084c6-132">Also check the request's headers to make sure you are specifying an appropriate `Content-Type` and `Content-Length`.</span></span>

## <a name="error-http-408-request-timeout"></a><span data-ttu-id="084c6-133">Error `HTTP 408 Request Timeout`</span><span class="sxs-lookup"><span data-stu-id="084c6-133">Error `HTTP 408 Request Timeout`</span></span>

<span data-ttu-id="084c6-134">The error is most likely because no audio data is being sent to the service.</span><span class="sxs-lookup"><span data-stu-id="084c6-134">The error is most likely because no audio data is being sent to the service.</span></span> <span data-ttu-id="084c6-135">This error could also be caused by network issues.</span><span class="sxs-lookup"><span data-stu-id="084c6-135">This error could also be caused by network issues.</span></span>

## <a name="the-recognitionstatus-in-the-response-is-initialsilencetimeout"></a><span data-ttu-id="084c6-136">The `RecognitionStatus` in the response is `InitialSilenceTimeout`</span><span class="sxs-lookup"><span data-stu-id="084c6-136">The `RecognitionStatus` in the response is `InitialSilenceTimeout`</span></span>

<span data-ttu-id="084c6-137">Audio data is usually the reason causing the issue.</span><span class="sxs-lookup"><span data-stu-id="084c6-137">Audio data is usually the reason causing the issue.</span></span> <span data-ttu-id="084c6-138">For example:</span><span class="sxs-lookup"><span data-stu-id="084c6-138">For example:</span></span>

* <span data-ttu-id="084c6-139">There is a long stretch of silence at the beginning of the audio.</span><span class="sxs-lookup"><span data-stu-id="084c6-139">There is a long stretch of silence at the beginning of the audio.</span></span> <span data-ttu-id="084c6-140">The service will stop the recognition after a few seconds and return `InitialSilenceTimeout`.</span><span class="sxs-lookup"><span data-stu-id="084c6-140">The service will stop the recognition after a few seconds and return `InitialSilenceTimeout`.</span></span>
* <span data-ttu-id="084c6-141">The audio uses an unsupported codec format, which causes the audio data to be treated as silence.</span><span class="sxs-lookup"><span data-stu-id="084c6-141">The audio uses an unsupported codec format, which causes the audio data to be treated as silence.</span></span>

## <a name="next-steps"></a><span data-ttu-id="084c6-142">Next steps</span><span class="sxs-lookup"><span data-stu-id="084c6-142">Next steps</span></span>

* [<span data-ttu-id="084c6-143">Release notes</span><span class="sxs-lookup"><span data-stu-id="084c6-143">Release notes</span></span>](releasenotes.md)

