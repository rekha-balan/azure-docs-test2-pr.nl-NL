---
title: Troubleshooting | Microsoft Docs
description: How to resolve issues when using Microsoft Speech Service.
services: cognitive-services
author: zhouwangzw
manager: wolfma
ms.service: cognitive-services
ms.component: bing-speech
ms.topic: article
ms.date: 09/15/2017
ms.author: zhouwang
ms.openlocfilehash: 04f3da19939d523d201d357b2b0293db1508431d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867038"
---
# <a name="troubleshooting"></a><span data-ttu-id="2255c-103">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="2255c-103">Troubleshooting</span></span>

## <a name="error-http-403-forbidden"></a><span data-ttu-id="2255c-104">Error `HTTP 403 Forbidden`</span><span class="sxs-lookup"><span data-stu-id="2255c-104">Error `HTTP 403 Forbidden`</span></span>

<span data-ttu-id="2255c-105">When using speech recognition API, it returns an `HTTP 403 Forbidden` error.</span><span class="sxs-lookup"><span data-stu-id="2255c-105">When using speech recognition API, it returns an `HTTP 403 Forbidden` error.</span></span>

### <a name="cause"></a><span data-ttu-id="2255c-106">Cause</span><span class="sxs-lookup"><span data-stu-id="2255c-106">Cause</span></span>

<span data-ttu-id="2255c-107">This error is often caused by authentication issues.</span><span class="sxs-lookup"><span data-stu-id="2255c-107">This error is often caused by authentication issues.</span></span> <span data-ttu-id="2255c-108">Connection requests without valid `Ocp-Apim-Subscription-Key` or `Authorization` header are rejected by the service with an `HTTP 403 Forbidden` response.</span><span class="sxs-lookup"><span data-stu-id="2255c-108">Connection requests without valid `Ocp-Apim-Subscription-Key` or `Authorization` header are rejected by the service with an `HTTP 403 Forbidden` response.</span></span>

<span data-ttu-id="2255c-109">If you are using subscription key for authentication, the reason could be</span><span class="sxs-lookup"><span data-stu-id="2255c-109">If you are using subscription key for authentication, the reason could be</span></span>

- <span data-ttu-id="2255c-110">the subscription key is missing or invalid</span><span class="sxs-lookup"><span data-stu-id="2255c-110">the subscription key is missing or invalid</span></span>
- <span data-ttu-id="2255c-111">the usage quota of the subscription key is exceeded</span><span class="sxs-lookup"><span data-stu-id="2255c-111">the usage quota of the subscription key is exceeded</span></span>
- <span data-ttu-id="2255c-112">the `Ocp-Apim-Subscription-Key` field is not set in the request header, when REST API is called</span><span class="sxs-lookup"><span data-stu-id="2255c-112">the `Ocp-Apim-Subscription-Key` field is not set in the request header, when REST API is called</span></span>

<span data-ttu-id="2255c-113">If you are using authorization token for authentication, the following reasons could cause the error.</span><span class="sxs-lookup"><span data-stu-id="2255c-113">If you are using authorization token for authentication, the following reasons could cause the error.</span></span>

- <span data-ttu-id="2255c-114">the `Authorization` header is missing in the request when using REST</span><span class="sxs-lookup"><span data-stu-id="2255c-114">the `Authorization` header is missing in the request when using REST</span></span>
- <span data-ttu-id="2255c-115">the authorization token specified in the Authorization header is invalid</span><span class="sxs-lookup"><span data-stu-id="2255c-115">the authorization token specified in the Authorization header is invalid</span></span>
- <span data-ttu-id="2255c-116">the authorization token is expired.</span><span class="sxs-lookup"><span data-stu-id="2255c-116">the authorization token is expired.</span></span> <span data-ttu-id="2255c-117">The access token has an expiry of 10 minutes</span><span class="sxs-lookup"><span data-stu-id="2255c-117">The access token has an expiry of 10 minutes</span></span>

<span data-ttu-id="2255c-118">For more information about authentication, see the [Authentication](How-to/how-to-authentication.md) page.</span><span class="sxs-lookup"><span data-stu-id="2255c-118">For more information about authentication, see the [Authentication](How-to/how-to-authentication.md) page.</span></span>

### <a name="troubleshooting-steps"></a><span data-ttu-id="2255c-119">Troubleshooting steps</span><span class="sxs-lookup"><span data-stu-id="2255c-119">Troubleshooting steps</span></span>

#### <a name="verify-that-your-subscription-key-is-valid"></a><span data-ttu-id="2255c-120">Verify that your subscription key is valid</span><span class="sxs-lookup"><span data-stu-id="2255c-120">Verify that your subscription key is valid</span></span>

<span data-ttu-id="2255c-121">You can run the following command for verification.</span><span class="sxs-lookup"><span data-stu-id="2255c-121">You can run the following command for verification.</span></span> <span data-ttu-id="2255c-122">Note to replace *YOUR_SUBSCRIPTION_KEY* with your own subscription key.</span><span class="sxs-lookup"><span data-stu-id="2255c-122">Note to replace *YOUR_SUBSCRIPTION_KEY* with your own subscription key.</span></span> <span data-ttu-id="2255c-123">If your subscription key is valid, you receive in the response the authorization token as a JSON Web Token (JWT).</span><span class="sxs-lookup"><span data-stu-id="2255c-123">If your subscription key is valid, you receive in the response the authorization token as a JSON Web Token (JWT).</span></span> <span data-ttu-id="2255c-124">Otherwise you get an error in response.</span><span class="sxs-lookup"><span data-stu-id="2255c-124">Otherwise you get an error in response.</span></span>

> [!NOTE]
> <span data-ttu-id="2255c-125">Replace `YOUR_SUBSCRIPTION_KEY` with your own subscription key.</span><span class="sxs-lookup"><span data-stu-id="2255c-125">Replace `YOUR_SUBSCRIPTION_KEY` with your own subscription key.</span></span>

# <a name="powershelltabpowershell"></a>[<span data-ttu-id="2255c-126">Powershell</span><span class="sxs-lookup"><span data-stu-id="2255c-126">Powershell</span></span>](#tab/Powershell)

```Powershell
$FetchTokenHeader = @{
  'Content-type'='application/x-www-form-urlencoded';
  'Content-Length'= '0';
  'Ocp-Apim-Subscription-Key' = 'YOUR_SUBSCRIPTION_KEY'
}

$OAuthToken = Invoke-RestMethod -Method POST -Uri https://api.cognitive.microsoft.com/sts/v1.0/issueToken -Headers $FetchTokenHeader

# show the token received
$OAuthToken

```

# <a name="curltabcurl"></a>[<span data-ttu-id="2255c-127">curl</span><span class="sxs-lookup"><span data-stu-id="2255c-127">curl</span></span>](#tab/curl)

<span data-ttu-id="2255c-128">The example uses curl on Linux with bash.</span><span class="sxs-lookup"><span data-stu-id="2255c-128">The example uses curl on Linux with bash.</span></span> <span data-ttu-id="2255c-129">If it is not available on your platform, you may need to install curl.</span><span class="sxs-lookup"><span data-stu-id="2255c-129">If it is not available on your platform, you may need to install curl.</span></span> <span data-ttu-id="2255c-130">The example should work also on Cygwin on Windows, Git Bash, zsh, and other shells.</span><span class="sxs-lookup"><span data-stu-id="2255c-130">The example should work also on Cygwin on Windows, Git Bash, zsh, and other shells.</span></span>

```
curl -v -X POST "https://api.cognitive.microsoft.com/sts/v1.0/issueToken" -H "Content-type: application/x-www-form-urlencoded" -H "Content-Length: 0" -H "Ocp-Apim-Subscription-Key: YOUR_SUBSCRIPTION_KEY"
```
---

<span data-ttu-id="2255c-131">Make sure that you use the same subscription key in your application or in the REST request as that is used above.</span><span class="sxs-lookup"><span data-stu-id="2255c-131">Make sure that you use the same subscription key in your application or in the REST request as that is used above.</span></span>

#### <a name="verify-the-authorization-token"></a><span data-ttu-id="2255c-132">Verify the authorization token</span><span class="sxs-lookup"><span data-stu-id="2255c-132">Verify the authorization token</span></span>

<span data-ttu-id="2255c-133">This step is only needed, if you use authorization token for authentication.</span><span class="sxs-lookup"><span data-stu-id="2255c-133">This step is only needed, if you use authorization token for authentication.</span></span> <span data-ttu-id="2255c-134">Run the following command to verify that the authorization token is still valid.</span><span class="sxs-lookup"><span data-stu-id="2255c-134">Run the following command to verify that the authorization token is still valid.</span></span> <span data-ttu-id="2255c-135">The command makes a POST request to the service, and expects a response message from the service.</span><span class="sxs-lookup"><span data-stu-id="2255c-135">The command makes a POST request to the service, and expects a response message from the service.</span></span> <span data-ttu-id="2255c-136">If you still receive HTTP `403 Forbidden` error, double-check the access token is set correctly and not expired.</span><span class="sxs-lookup"><span data-stu-id="2255c-136">If you still receive HTTP `403 Forbidden` error, double-check the access token is set correctly and not expired.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2255c-137">The token has an expiry of 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="2255c-137">The token has an expiry of 10 minutes.</span></span>
> [!NOTE]
> <span data-ttu-id="2255c-138">Replace `YOUR_AUDIO_FILE` with the path to your prerecorded audio file, and `YOUR_ACCESS_TOKEN` with the authorization token returned in the previous step.</span><span class="sxs-lookup"><span data-stu-id="2255c-138">Replace `YOUR_AUDIO_FILE` with the path to your prerecorded audio file, and `YOUR_ACCESS_TOKEN` with the authorization token returned in the previous step.</span></span>

# <a name="powershelltabpowershell"></a>[<span data-ttu-id="2255c-139">Powershell</span><span class="sxs-lookup"><span data-stu-id="2255c-139">Powershell</span></span>](#tab/Powershell)

```Powershell

$SpeechServiceURI =
'https://speech.platform.bing.com/speech/recognition/interactive/cognitiveservices/v1?language=en-us&format=detailed'

# $OAuthToken is the authrization token returned by the token service.
$RecoRequestHeader = @{
  'Authorization' = 'Bearer '+ $OAuthToken;
  'Transfer-Encoding' = 'chunked'
  'Content-type' = 'audio/wav; codec=audio/pcm; samplerate=16000'
}

# Read audio into byte array
$audioBytes = [System.IO.File]::ReadAllBytes("YOUR_AUDIO_FILE")

$RecoResponse = Invoke-RestMethod -Method POST -Uri $SpeechServiceURI -Headers $RecoRequestHeader -Body $audioBytes

# Show the result
$RecoResponse

```

# <a name="curltabcurl"></a>[<span data-ttu-id="2255c-140">curl</span><span class="sxs-lookup"><span data-stu-id="2255c-140">curl</span></span>](#tab/curl)

```
curl -v -X POST "https://speech.platform.bing.com/speech/recognition/interactive/cognitiveservices/v1?language=en-us&format=detailed" -H "Transfer-Encoding: chunked" -H "Authorization: Bearer YOUR_ACCESS_TOKEN" -H "Content-type: audio/wav; codec=audio/pcm; samplerate=16000" --data-binary @YOUR_AUDIO_FILE
```

---

## <a name="error-http-400-bad-request"></a><span data-ttu-id="2255c-141">Error `HTTP 400 Bad Request`</span><span class="sxs-lookup"><span data-stu-id="2255c-141">Error `HTTP 400 Bad Request`</span></span>

<span data-ttu-id="2255c-142">This reason is usually that the request body contains invalid audio data.</span><span class="sxs-lookup"><span data-stu-id="2255c-142">This reason is usually that the request body contains invalid audio data.</span></span> <span data-ttu-id="2255c-143">Currently we only support WAV file.</span><span class="sxs-lookup"><span data-stu-id="2255c-143">Currently we only support WAV file.</span></span>

## <a name="error-http-408-request-timeout"></a><span data-ttu-id="2255c-144">Error `HTTP 408 Request Timeout`</span><span class="sxs-lookup"><span data-stu-id="2255c-144">Error `HTTP 408 Request Timeout`</span></span>

<span data-ttu-id="2255c-145">The error is most likely because that no audio data is sent to the service and the service returns this error after timeout.</span><span class="sxs-lookup"><span data-stu-id="2255c-145">The error is most likely because that no audio data is sent to the service and the service returns this error after timeout.</span></span> <span data-ttu-id="2255c-146">For REST API, the audio data should be put in the request body.</span><span class="sxs-lookup"><span data-stu-id="2255c-146">For REST API, the audio data should be put in the request body.</span></span>

## <a name="the-recognitionstatus-in-the-response-is-initialsilencetimeout"></a><span data-ttu-id="2255c-147">The `RecognitionStatus` in the response is `InitialSilenceTimeout`</span><span class="sxs-lookup"><span data-stu-id="2255c-147">The `RecognitionStatus` in the response is `InitialSilenceTimeout`</span></span>

<span data-ttu-id="2255c-148">Audio data is usually the reason causing the issue.</span><span class="sxs-lookup"><span data-stu-id="2255c-148">Audio data is usually the reason causing the issue.</span></span> <span data-ttu-id="2255c-149">For example,</span><span class="sxs-lookup"><span data-stu-id="2255c-149">For example,</span></span>

- <span data-ttu-id="2255c-150">the audio has a long silence time at the beginning.</span><span class="sxs-lookup"><span data-stu-id="2255c-150">the audio has a long silence time at the beginning.</span></span> <span data-ttu-id="2255c-151">The service will stop the recognition after some number of seconds and returns `InitialSilenceTimeout`.</span><span class="sxs-lookup"><span data-stu-id="2255c-151">The service will stop the recognition after some number of seconds and returns `InitialSilenceTimeout`.</span></span>
- <span data-ttu-id="2255c-152">the audio uses unsupported codec format, which makes the audio data be treated as silence.</span><span class="sxs-lookup"><span data-stu-id="2255c-152">the audio uses unsupported codec format, which makes the audio data be treated as silence.</span></span>
