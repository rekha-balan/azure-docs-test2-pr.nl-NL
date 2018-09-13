---
title: Bing Speech Recognition REST API in Microsoft Cognitive Services | Microsoft Docs
description: Use the Bing Speech Recognition REST API in contexts that need cloud-based speech recognition capabilities.
services: cognitive-services
author: priyaravi20
manager: yanbo
ms.service: cognitive-services
ms.technology: speech
ms.topic: article
ms.date: 02/28/2017
ms.author: prrajan
ms.openlocfilehash: 17ced64476fe1abd7fe9754206495006f662d1e7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549923"
---
# <a name="bing-speech-recognition-api"></a><span data-ttu-id="e918c-103">Bing Speech Recognition API</span><span class="sxs-lookup"><span data-stu-id="e918c-103">Bing Speech Recognition API</span></span>

## <span data-ttu-id="e918c-104"><a name="Introduction">Introduction</a></span><span class="sxs-lookup"><span data-stu-id="e918c-104"><a name="Introduction">Introduction</a></span></span>
<span data-ttu-id="e918c-105">This documentation describes the Bing Speech Recognition REST API that exposes an HTTP interface which enables developers to transcribe voice queries.</span><span class="sxs-lookup"><span data-stu-id="e918c-105">This documentation describes the Bing Speech Recognition REST API that exposes an HTTP interface which enables developers to transcribe voice queries.</span></span> <span data-ttu-id="e918c-106">The Bing Speech Recognition API may be used in many different contexts that need cloud-based speech recognition capabilities.</span><span class="sxs-lookup"><span data-stu-id="e918c-106">The Bing Speech Recognition API may be used in many different contexts that need cloud-based speech recognition capabilities.</span></span> 

## <span data-ttu-id="e918c-107"><a name="VoiceRecReq">Speech Recognition Request</a></span><span class="sxs-lookup"><span data-stu-id="e918c-107"><a name="VoiceRecReq">Speech Recognition Request</a></span></span>
### <span data-ttu-id="e918c-108"><a name="Authorize">Authenticate the API call</a></span><span class="sxs-lookup"><span data-stu-id="e918c-108"><a name="Authorize">Authenticate the API call</a></span></span>

<span data-ttu-id="e918c-109">Every request requires a JSON Web Token (JWT) access token.</span><span class="sxs-lookup"><span data-stu-id="e918c-109">Every request requires a JSON Web Token (JWT) access token.</span></span> <span data-ttu-id="e918c-110">The JWT access token is passed through in the Speech request header.</span><span class="sxs-lookup"><span data-stu-id="e918c-110">The JWT access token is passed through in the Speech request header.</span></span> <span data-ttu-id="e918c-111">The token has an expiry time of 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="e918c-111">The token has an expiry time of 10 minutes.</span></span> <span data-ttu-id="e918c-112">See [Get Started for Free](https://www.microsoft.com/cognitive-services/en-US/sign-up?ReturnUrl=/cognitive-services/en-us/subscriptions?productId=%2fproducts%2fBing.Speech.Preview) for information about subscribing and obtaining API keys used to retrieve valid JWT access tokens.</span><span class="sxs-lookup"><span data-stu-id="e918c-112">See [Get Started for Free](https://www.microsoft.com/cognitive-services/en-US/sign-up?ReturnUrl=/cognitive-services/en-us/subscriptions?productId=%2fproducts%2fBing.Speech.Preview) for information about subscribing and obtaining API keys used to retrieve valid JWT access tokens.</span></span>

<span data-ttu-id="e918c-113">The API key is passed to the token service, for example:</span><span class="sxs-lookup"><span data-stu-id="e918c-113">The API key is passed to the token service, for example:</span></span>

```
POST https://api.cognitive.microsoft.com/sts/v1.0/issueToken
Content-Length: 0
```

<span data-ttu-id="e918c-114">The required header for token access is:</span><span class="sxs-lookup"><span data-stu-id="e918c-114">The required header for token access is:</span></span>

<span data-ttu-id="e918c-115">Name</span><span class="sxs-lookup"><span data-stu-id="e918c-115">Name</span></span>    | <span data-ttu-id="e918c-116">Format</span><span class="sxs-lookup"><span data-stu-id="e918c-116">Format</span></span>    | <span data-ttu-id="e918c-117">Description, Example and Use</span><span class="sxs-lookup"><span data-stu-id="e918c-117">Description, Example and Use</span></span>
---------|---------|--------
<span data-ttu-id="e918c-118">Ocp-Apim-Subscription-Key</span><span class="sxs-lookup"><span data-stu-id="e918c-118">Ocp-Apim-Subscription-Key</span></span> | <span data-ttu-id="e918c-119">ASCII</span><span class="sxs-lookup"><span data-stu-id="e918c-119">ASCII</span></span>   | <span data-ttu-id="e918c-120">Your subscription key.</span><span class="sxs-lookup"><span data-stu-id="e918c-120">Your subscription key.</span></span>

<span data-ttu-id="e918c-121">The token service returns the JWT access token as text/plain.</span><span class="sxs-lookup"><span data-stu-id="e918c-121">The token service returns the JWT access token as text/plain.</span></span> <span data-ttu-id="e918c-122">Then the JWT is passed as a Base64 access_token to the Speech endpoint as an Authorization header prefixed with the string Bearer, for example:</span><span class="sxs-lookup"><span data-stu-id="e918c-122">Then the JWT is passed as a Base64 access_token to the Speech endpoint as an Authorization header prefixed with the string Bearer, for example:</span></span>

`Authorization: Bearer [Base64 access_token]`

### <span data-ttu-id="e918c-123"><a name="SpeechService">Access the Speech Service Endpoint</a></span><span class="sxs-lookup"><span data-stu-id="e918c-123"><a name="SpeechService">Access the Speech Service Endpoint</a></span></span>

<span data-ttu-id="e918c-124">Clients must use the following endpoint to access the service and build voice enabled applications:</span><span class="sxs-lookup"><span data-stu-id="e918c-124">Clients must use the following endpoint to access the service and build voice enabled applications:</span></span> 

 `https://speech.platform.bing.com/recognize`

>[!NOTE]
><span data-ttu-id="e918c-125">Until you have acquired an `access token` with your subscription key as described above this link will generate a 403 Response Error.</span><span class="sxs-lookup"><span data-stu-id="e918c-125">Until you have acquired an `access token` with your subscription key as described above this link will generate a 403 Response Error.</span></span>

<span data-ttu-id="e918c-126">The API uses HTTP POST to upload audio.</span><span class="sxs-lookup"><span data-stu-id="e918c-126">The API uses HTTP POST to upload audio.</span></span> <span data-ttu-id="e918c-127">The API supports [chunked transfer encoding](https://en.wikipedia.org/wiki/Chunked_transfer_encoding) for efficient audio streaming.</span><span class="sxs-lookup"><span data-stu-id="e918c-127">The API supports [chunked transfer encoding](https://en.wikipedia.org/wiki/Chunked_transfer_encoding) for efficient audio streaming.</span></span> <span data-ttu-id="e918c-128">For live transcription scenarios, it is recommended you use chunked transfer encoding to stream the audio to the service while the user is speaking.</span><span class="sxs-lookup"><span data-stu-id="e918c-128">For live transcription scenarios, it is recommended you use chunked transfer encoding to stream the audio to the service while the user is speaking.</span></span> <span data-ttu-id="e918c-129">Other implementations result in higher user-perceived latency.</span><span class="sxs-lookup"><span data-stu-id="e918c-129">Other implementations result in higher user-perceived latency.</span></span> 

<span data-ttu-id="e918c-130">Your application must indicate the end of the audio to determine start and end of speech, which in turn is used by the service to determine the start and end of the request.</span><span class="sxs-lookup"><span data-stu-id="e918c-130">Your application must indicate the end of the audio to determine start and end of speech, which in turn is used by the service to determine the start and end of the request.</span></span> <span data-ttu-id="e918c-131">You may not upload more than 10 seconds of audio in any one request and the total request duration cannot exceed 14 seconds.</span><span class="sxs-lookup"><span data-stu-id="e918c-131">You may not upload more than 10 seconds of audio in any one request and the total request duration cannot exceed 14 seconds.</span></span> 

### <span data-ttu-id="e918c-132"><a name="InputParam">Input Parameters</a></span><span class="sxs-lookup"><span data-stu-id="e918c-132"><a name="InputParam">Input Parameters</a></span></span>

<span data-ttu-id="e918c-133">Inputs to the Bing Speech Recognition API are expressed as HTTP query parameters.</span><span class="sxs-lookup"><span data-stu-id="e918c-133">Inputs to the Bing Speech Recognition API are expressed as HTTP query parameters.</span></span> <span data-ttu-id="e918c-134">Parameters in the POST body are treated as audio content.</span><span class="sxs-lookup"><span data-stu-id="e918c-134">Parameters in the POST body are treated as audio content.</span></span> <span data-ttu-id="e918c-135">Unsafe characters should be escaped following the W3C URL spec ([http://www.w3.org/Addressing/URL/url-spec.txt](http://www.w3.org/Addressing/URL/url-spec.txt)).</span><span class="sxs-lookup"><span data-stu-id="e918c-135">Unsafe characters should be escaped following the W3C URL spec ([http://www.w3.org/Addressing/URL/url-spec.txt](http://www.w3.org/Addressing/URL/url-spec.txt)).</span></span> <span data-ttu-id="e918c-136">A request with more than one instance of any parameter will result in an error response (HTTP 400).</span><span class="sxs-lookup"><span data-stu-id="e918c-136">A request with more than one instance of any parameter will result in an error response (HTTP 400).</span></span> 

<span data-ttu-id="e918c-137">Following is a complete list of required and optional input parameters.</span><span class="sxs-lookup"><span data-stu-id="e918c-137">Following is a complete list of required and optional input parameters.</span></span>

#### <span data-ttu-id="e918c-138"><a name="ReqParam">Required Parameters</a></span><span class="sxs-lookup"><span data-stu-id="e918c-138"><a name="ReqParam">Required Parameters</a></span></span>

<span data-ttu-id="e918c-139">Name</span><span class="sxs-lookup"><span data-stu-id="e918c-139">Name</span></span>  |<span data-ttu-id="e918c-140">Format</span><span class="sxs-lookup"><span data-stu-id="e918c-140">Format</span></span>  |<span data-ttu-id="e918c-141">Description, example and use</span><span class="sxs-lookup"><span data-stu-id="e918c-141">Description, example and use</span></span>  
---------|---------|---------
<span data-ttu-id="e918c-142">Version</span><span class="sxs-lookup"><span data-stu-id="e918c-142">Version</span></span>     |  <span data-ttu-id="e918c-143">Digits and "."</span><span class="sxs-lookup"><span data-stu-id="e918c-143">Digits and "."</span></span>       |    <span data-ttu-id="e918c-144">The API version being used by the client.</span><span class="sxs-lookup"><span data-stu-id="e918c-144">The API version being used by the client.</span></span> <span data-ttu-id="e918c-145">The required value is 3.0.</span><span class="sxs-lookup"><span data-stu-id="e918c-145">The required value is 3.0.</span></span>   <span data-ttu-id="e918c-146">**Example:** version=3.0</span><span class="sxs-lookup"><span data-stu-id="e918c-146">**Example:** version=3.0</span></span>   
<span data-ttu-id="e918c-147">requestid</span><span class="sxs-lookup"><span data-stu-id="e918c-147">requestid</span></span>     |    <span data-ttu-id="e918c-148">GUID</span><span class="sxs-lookup"><span data-stu-id="e918c-148">GUID</span></span>     |        <span data-ttu-id="e918c-149">A globally unique identifier generated by the client for this request.</span><span class="sxs-lookup"><span data-stu-id="e918c-149">A globally unique identifier generated by the client for this request.</span></span> <span data-ttu-id="e918c-150">**Example:** requestid=b2c95ede-97eb-4c88-81e4-80f32d6aee54</span><span class="sxs-lookup"><span data-stu-id="e918c-150">**Example:** requestid=b2c95ede-97eb-4c88-81e4-80f32d6aee54</span></span>
<span data-ttu-id="e918c-151">appID</span><span class="sxs-lookup"><span data-stu-id="e918c-151">appID</span></span>     |   <span data-ttu-id="e918c-152">GUID</span><span class="sxs-lookup"><span data-stu-id="e918c-152">GUID</span></span>      |   <span data-ttu-id="e918c-153">A globally unique identifier used for this application.</span><span class="sxs-lookup"><span data-stu-id="e918c-153">A globally unique identifier used for this application.</span></span> <span data-ttu-id="e918c-154">Always use appID = D4D52672-91D7-4C74-8AD8-42B1D98141A5.</span><span class="sxs-lookup"><span data-stu-id="e918c-154">Always use appID = D4D52672-91D7-4C74-8AD8-42B1D98141A5.</span></span> <span data-ttu-id="e918c-155">Do not generate a new GUID as it will be unsupported.</span><span class="sxs-lookup"><span data-stu-id="e918c-155">Do not generate a new GUID as it will be unsupported.</span></span>     
<span data-ttu-id="e918c-156">format</span><span class="sxs-lookup"><span data-stu-id="e918c-156">format</span></span>     |  <span data-ttu-id="e918c-157">UTF-8</span><span class="sxs-lookup"><span data-stu-id="e918c-157">UTF-8</span></span>       |      <span data-ttu-id="e918c-158">Specifies the desired format of the returned data.</span><span class="sxs-lookup"><span data-stu-id="e918c-158">Specifies the desired format of the returned data.</span></span> <span data-ttu-id="e918c-159">The required value is JSON.</span><span class="sxs-lookup"><span data-stu-id="e918c-159">The required value is JSON.</span></span> <span data-ttu-id="e918c-160">**Example:** format=json.</span><span class="sxs-lookup"><span data-stu-id="e918c-160">**Example:** format=json.</span></span> 
<span data-ttu-id="e918c-161">locale</span><span class="sxs-lookup"><span data-stu-id="e918c-161">locale</span></span>     |    <span data-ttu-id="e918c-162">UTF-8 (IETF Language Tag)</span><span class="sxs-lookup"><span data-stu-id="e918c-162">UTF-8 (IETF Language Tag)</span></span>     |    <span data-ttu-id="e918c-163">Language code of the audio content in IETF RFC 5646.</span><span class="sxs-lookup"><span data-stu-id="e918c-163">Language code of the audio content in IETF RFC 5646.</span></span> <span data-ttu-id="e918c-164">Case does not matter.</span><span class="sxs-lookup"><span data-stu-id="e918c-164">Case does not matter.</span></span> <span data-ttu-id="e918c-165">**Example:** locale=en-US.</span><span class="sxs-lookup"><span data-stu-id="e918c-165">**Example:** locale=en-US.</span></span> 
<span data-ttu-id="e918c-166">device.os</span><span class="sxs-lookup"><span data-stu-id="e918c-166">device.os</span></span>    |     <span data-ttu-id="e918c-167">UTF-8</span><span class="sxs-lookup"><span data-stu-id="e918c-167">UTF-8</span></span>    |     <span data-ttu-id="e918c-168">Operating system the client is running on.</span><span class="sxs-lookup"><span data-stu-id="e918c-168">Operating system the client is running on.</span></span> <span data-ttu-id="e918c-169">This is an open field but we encourage clients to use it consistently across devices and applications.</span><span class="sxs-lookup"><span data-stu-id="e918c-169">This is an open field but we encourage clients to use it consistently across devices and applications.</span></span> <span data-ttu-id="e918c-170">Suggested values: Windows OS, Windows Phone OS, XBOX, Android, iPhone OS.</span><span class="sxs-lookup"><span data-stu-id="e918c-170">Suggested values: Windows OS, Windows Phone OS, XBOX, Android, iPhone OS.</span></span> <span data-ttu-id="e918c-171">**Example:** device.os=Windows Phone OS.</span><span class="sxs-lookup"><span data-stu-id="e918c-171">**Example:** device.os=Windows Phone OS.</span></span>
<span data-ttu-id="e918c-172">scenarios</span><span class="sxs-lookup"><span data-stu-id="e918c-172">scenarios</span></span>     |    <span data-ttu-id="e918c-173">UTF-8</span><span class="sxs-lookup"><span data-stu-id="e918c-173">UTF-8</span></span>     |    <span data-ttu-id="e918c-174">The context for performing a recognition.</span><span class="sxs-lookup"><span data-stu-id="e918c-174">The context for performing a recognition.</span></span> <span data-ttu-id="e918c-175">The supported values are: ulm, websearch.</span><span class="sxs-lookup"><span data-stu-id="e918c-175">The supported values are: ulm, websearch.</span></span> <span data-ttu-id="e918c-176">**Example:** scenarios=ulm.</span><span class="sxs-lookup"><span data-stu-id="e918c-176">**Example:** scenarios=ulm.</span></span>     
<span data-ttu-id="e918c-177">instanceid</span><span class="sxs-lookup"><span data-stu-id="e918c-177">instanceid</span></span>      |    <span data-ttu-id="e918c-178">GUID</span><span class="sxs-lookup"><span data-stu-id="e918c-178">GUID</span></span>     |      <span data-ttu-id="e918c-179">A globally unique device identifier of the device making the request.</span><span class="sxs-lookup"><span data-stu-id="e918c-179">A globally unique device identifier of the device making the request.</span></span> <span data-ttu-id="e918c-180">**Example:** instanceid=b2c95ede-97eb-4c88-81e4-80f32d6aee54</span><span class="sxs-lookup"><span data-stu-id="e918c-180">**Example:** instanceid=b2c95ede-97eb-4c88-81e4-80f32d6aee54</span></span>
  
#### <span data-ttu-id="e918c-181"><a name="OptParam">Optional Parameters</a></span><span class="sxs-lookup"><span data-stu-id="e918c-181"><a name="OptParam">Optional Parameters</a></span></span>

>[!NOTE]
><span data-ttu-id="e918c-182">The values below are used either for performing the request or to manage the service operationally.</span><span class="sxs-lookup"><span data-stu-id="e918c-182">The values below are used either for performing the request or to manage the service operationally.</span></span> 

<span data-ttu-id="e918c-183">Name</span><span class="sxs-lookup"><span data-stu-id="e918c-183">Name</span></span>  |<span data-ttu-id="e918c-184">Format</span><span class="sxs-lookup"><span data-stu-id="e918c-184">Format</span></span>  |<span data-ttu-id="e918c-185">Description and example</span><span class="sxs-lookup"><span data-stu-id="e918c-185">Description and example</span></span>  
---------|---------|---------
<span data-ttu-id="e918c-186">maxnbest</span><span class="sxs-lookup"><span data-stu-id="e918c-186">maxnbest</span></span>     |     <span data-ttu-id="e918c-187">Integer</span><span class="sxs-lookup"><span data-stu-id="e918c-187">Integer</span></span>    |       <span data-ttu-id="e918c-188">Maximum number of results the voice application API should return.</span><span class="sxs-lookup"><span data-stu-id="e918c-188">Maximum number of results the voice application API should return.</span></span> <span data-ttu-id="e918c-189">The default is 1.</span><span class="sxs-lookup"><span data-stu-id="e918c-189">The default is 1.</span></span> <span data-ttu-id="e918c-190">The maximum is 5.</span><span class="sxs-lookup"><span data-stu-id="e918c-190">The maximum is 5.</span></span> <span data-ttu-id="e918c-191">**Example:** maxnbest=3</span><span class="sxs-lookup"><span data-stu-id="e918c-191">**Example:** maxnbest=3</span></span>   
<span data-ttu-id="e918c-192">result.profanitymarkup</span><span class="sxs-lookup"><span data-stu-id="e918c-192">result.profanitymarkup</span></span>     |     <span data-ttu-id="e918c-193">0/1</span><span class="sxs-lookup"><span data-stu-id="e918c-193">0/1</span></span>    |      <span data-ttu-id="e918c-194">Scan the result text for words included in an offensive word list.</span><span class="sxs-lookup"><span data-stu-id="e918c-194">Scan the result text for words included in an offensive word list.</span></span> <span data-ttu-id="e918c-195">If found, the word will be delimited by bad word tag.</span><span class="sxs-lookup"><span data-stu-id="e918c-195">If found, the word will be delimited by bad word tag.</span></span> <span data-ttu-id="e918c-196">**Example:** result.profanity=1 (0 means off, 1 means on, default is 1.)</span><span class="sxs-lookup"><span data-stu-id="e918c-196">**Example:** result.profanity=1 (0 means off, 1 means on, default is 1.)</span></span>

### <a name="a-namesampleimplementationrest-api-implementation-sample"></a><span data-ttu-id="e918c-197"><a name="SampleImplementation">REST API Implementation Sample</span><span class="sxs-lookup"><span data-stu-id="e918c-197"><a name="SampleImplementation">REST API Implementation Sample</span></span>

<span data-ttu-id="e918c-198">A working code sample of REST API implementation can be found [here](https://oxfordportal.blob.core.windows.net/speech/doc/recognition/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="e918c-198">A working code sample of REST API implementation can be found [here](https://oxfordportal.blob.core.windows.net/speech/doc/recognition/Program.cs).</span></span> 

###  <span data-ttu-id="e918c-199"><a name="SampleVoiceRR">Example Speech Recognition Request</a></span><span class="sxs-lookup"><span data-stu-id="e918c-199"><a name="SampleVoiceRR">Example Speech Recognition Request</a></span></span>

<span data-ttu-id="e918c-200">The following is an example of a request where the audio is supplied as part of a recognition request:</span><span class="sxs-lookup"><span data-stu-id="e918c-200">The following is an example of a request where the audio is supplied as part of a recognition request:</span></span> 
   
```
POST /recognize?scenarios=catsearch&appid=f84e364c-ec34-4773-a783-73707bd9a585&locale=en-US&device.os=wp7&version=3.0&format=xml&requestid=1d4b6030-9099-11e0-91e4-0800200c9a66&instanceid=1d4b6030-9099-11e0-91e4-0800200c9a66 HTTP/1.1
Host: speech.platform.bing.com
Content-Type: audio/wav; samplerate=16000
Authorization: Bearer [Base64 access_token]

(audio data)
```
### <span data-ttu-id="e918c-201"><a name="Codecs">Supported Codecs</a></span><span class="sxs-lookup"><span data-stu-id="e918c-201"><a name="Codecs">Supported Codecs</a></span></span>
<span data-ttu-id="e918c-202">The Speech Recognition API supports audio/wav using the following codecs:</span><span class="sxs-lookup"><span data-stu-id="e918c-202">The Speech Recognition API supports audio/wav using the following codecs:</span></span> 
* <span data-ttu-id="e918c-203">PCM single channel</span><span class="sxs-lookup"><span data-stu-id="e918c-203">PCM single channel</span></span>
* <span data-ttu-id="e918c-204">Siren</span><span class="sxs-lookup"><span data-stu-id="e918c-204">Siren</span></span>
* <span data-ttu-id="e918c-205">SirenSR</span><span class="sxs-lookup"><span data-stu-id="e918c-205">SirenSR</span></span>

## <span data-ttu-id="e918c-206"><a name="VoiceRecResponse">Speech Recognition Responses</a></span><span class="sxs-lookup"><span data-stu-id="e918c-206"><a name="VoiceRecResponse">Speech Recognition Responses</a></span></span>
<span data-ttu-id="e918c-207">The API response is returned in JSON format.</span><span class="sxs-lookup"><span data-stu-id="e918c-207">The API response is returned in JSON format.</span></span> <span data-ttu-id="e918c-208">The value of the “name” tag has the post-inverse text normalization result.</span><span class="sxs-lookup"><span data-stu-id="e918c-208">The value of the “name” tag has the post-inverse text normalization result.</span></span> <span data-ttu-id="e918c-209">The value of the “lexical” tag has the pre-inverse text normalization result.</span><span class="sxs-lookup"><span data-stu-id="e918c-209">The value of the “lexical” tag has the pre-inverse text normalization result.</span></span> 

### <span data-ttu-id="e918c-210"><a name="NormalResponse">Normal response</a></span><span class="sxs-lookup"><span data-stu-id="e918c-210"><a name="NormalResponse">Normal response</a></span></span>

#### <span data-ttu-id="e918c-211"><a name="Schema1">Schema 1</a></span><span class="sxs-lookup"><span data-stu-id="e918c-211"><a name="Schema1">Schema 1</a></span></span>
<span data-ttu-id="e918c-212">Schema Legend:</span><span class="sxs-lookup"><span data-stu-id="e918c-212">Schema Legend:</span></span> 

* <span data-ttu-id="e918c-213">< ... >  means optional</span><span class="sxs-lookup"><span data-stu-id="e918c-213">< ... >  means optional</span></span>
* <span data-ttu-id="e918c-214">"[ ]" represents a json array</span><span class="sxs-lookup"><span data-stu-id="e918c-214">"[ ]" represents a json array</span></span>
* <span data-ttu-id="e918c-215">"{ }" represents a json object</span><span class="sxs-lookup"><span data-stu-id="e918c-215">"{ }" represents a json object</span></span>  
* <span data-ttu-id="e918c-216">"\*" indicates that the object can be defined multiple times</span><span class="sxs-lookup"><span data-stu-id="e918c-216">"\*" indicates that the object can be defined multiple times</span></span>

  
```
JSON-text: version header <results> // result must be always and only present when status = "success" 
version: string // The API version "3.0" — the value the client passed and consequently the API version that serviced the request. 
header: {status scenario <name> <lexical> properties} // name and lexical are always and only present in the case of "status" = “success”
     status: "success"/ "error"/ "false reco"// 'false reco' is returned only for 2.0 responses when NOSPEECH OR FALSERECO is 1. This is done to maintain backward compatibility. 
     scenario: string // the scenario this recognition result came from. 
     name: string // formatted recognition result. Profane terms are surrounded with <profanity> tags. 
     lexical: string // text of what was spoken. Profane terms are surrounded with <profanity> tags.
     properties: {requestid <NOSPEECH> <FALSERECO> <HIGHCONF> <ERROR>} 
           requestid: string // this is a uuid identifying the requestid to be sent with the associated logs. It should be used as the "server.requestid" parameter value in the subsequent logging API request. 
           NOSPEECH: 1 // set when no speech was detected on the sent audio. 
           FALSERECO: 1 // set when no matches were found for the sent audio. 
           HIGHCONF: 1 // set when the header result is determined to be of high-confidence. 
           MIDCONF: 1 // set when the header result is determined to be of medium-confidence.
           LOWCONF: 1 // set when the header result is determined to be of low-confidence. 
           ERROR: 1 // set when there was an error generating a response. 
results: [{scenario name lexical confidence pronunciation tokens}*] // n-best list of results ordered by confidence. 
     scenario: string // the scenario this recognition result came from. 
     name: string // formatted recognition result. Profane terms are surrounded with <profanity> tags. 
     lexical: string // text of what was spoken. Profane terms are surrounded with <profanity> tags. 
     properties: {<HIGHCONF>} 
           HIGHCONF: 1 // set when the header result is determined to be of high-confidence. 
           MIDCONF: 1 // set when the header result is determined to be of medium-confidence. 
           LOWCONF: 1 // set when the header result is determined to be of low-confidence. 

```
  
#### <span data-ttu-id="e918c-217"><a name="Schema2">Schema 2</a></span><span class="sxs-lookup"><span data-stu-id="e918c-217"><a name="Schema2">Schema 2</a></span></span>

* <span data-ttu-id="e918c-218">**speechbox-root:**</span><span class="sxs-lookup"><span data-stu-id="e918c-218">**speechbox-root:**</span></span>  
  * <span data-ttu-id="e918c-219">**child tags:** version, header, results</span><span class="sxs-lookup"><span data-stu-id="e918c-219">**child tags:** version, header, results</span></span> 
  * <span data-ttu-id="e918c-220">**value:** none</span><span class="sxs-lookup"><span data-stu-id="e918c-220">**value:** none</span></span> 
  * <span data-ttu-id="e918c-221">**attributes:** none</span><span class="sxs-lookup"><span data-stu-id="e918c-221">**attributes:** none</span></span> 

* <span data-ttu-id="e918c-222">**version:**</span><span class="sxs-lookup"><span data-stu-id="e918c-222">**version:**</span></span> 
  * <span data-ttu-id="e918c-223">**child tags:** none</span><span class="sxs-lookup"><span data-stu-id="e918c-223">**child tags:** none</span></span> 
  * <span data-ttu-id="e918c-224">**value:** string, the API version "3.0"</span><span class="sxs-lookup"><span data-stu-id="e918c-224">**value:** string, the API version "3.0"</span></span> 
  * <span data-ttu-id="e918c-225">**attributes:** none</span><span class="sxs-lookup"><span data-stu-id="e918c-225">**attributes:** none</span></span> 

* <span data-ttu-id="e918c-226">**header:**</span><span class="sxs-lookup"><span data-stu-id="e918c-226">**header:**</span></span>  
  * <span data-ttu-id="e918c-227">**tags:** status, name, lexical, properties</span><span class="sxs-lookup"><span data-stu-id="e918c-227">**tags:** status, name, lexical, properties</span></span> 
  * <span data-ttu-id="e918c-228">**value:** none</span><span class="sxs-lookup"><span data-stu-id="e918c-228">**value:** none</span></span> 
  * <span data-ttu-id="e918c-229">**attributes:** none</span><span class="sxs-lookup"><span data-stu-id="e918c-229">**attributes:** none</span></span> 

* <span data-ttu-id="e918c-230">**status:**</span><span class="sxs-lookup"><span data-stu-id="e918c-230">**status:**</span></span>  
  * <span data-ttu-id="e918c-231">**child tags:** none</span><span class="sxs-lookup"><span data-stu-id="e918c-231">**child tags:** none</span></span> 
  * <span data-ttu-id="e918c-232">**value:** string, "success" or "error"</span><span class="sxs-lookup"><span data-stu-id="e918c-232">**value:** string, "success" or "error"</span></span> 
  * <span data-ttu-id="e918c-233">**attributes:** none</span><span class="sxs-lookup"><span data-stu-id="e918c-233">**attributes:** none</span></span> 

* <span data-ttu-id="e918c-234">**scenario:**</span><span class="sxs-lookup"><span data-stu-id="e918c-234">**scenario:**</span></span>  
  * <span data-ttu-id="e918c-235">**child tags:** none</span><span class="sxs-lookup"><span data-stu-id="e918c-235">**child tags:** none</span></span> 
  * <span data-ttu-id="e918c-236">**value:** string, the scenario parameter value</span><span class="sxs-lookup"><span data-stu-id="e918c-236">**value:** string, the scenario parameter value</span></span> 
  * <span data-ttu-id="e918c-237">**attributes:** none</span><span class="sxs-lookup"><span data-stu-id="e918c-237">**attributes:** none</span></span> 

* <span data-ttu-id="e918c-238">**name:**</span><span class="sxs-lookup"><span data-stu-id="e918c-238">**name:**</span></span>  
  * <span data-ttu-id="e918c-239">**child tags:** none</span><span class="sxs-lookup"><span data-stu-id="e918c-239">**child tags:** none</span></span> 
  * <span data-ttu-id="e918c-240">**value:** string, formatted recognition result</span><span class="sxs-lookup"><span data-stu-id="e918c-240">**value:** string, formatted recognition result</span></span> 
  * <span data-ttu-id="e918c-241">**attributes:** none</span><span class="sxs-lookup"><span data-stu-id="e918c-241">**attributes:** none</span></span> 

* <span data-ttu-id="e918c-242">**lexical:**</span><span class="sxs-lookup"><span data-stu-id="e918c-242">**lexical:**</span></span>  
  * <span data-ttu-id="e918c-243">**child tags:** none</span><span class="sxs-lookup"><span data-stu-id="e918c-243">**child tags:** none</span></span> 
  * <span data-ttu-id="e918c-244">**value:** string, text of what was spoken</span><span class="sxs-lookup"><span data-stu-id="e918c-244">**value:** string, text of what was spoken</span></span> 
  * <span data-ttu-id="e918c-245">**attributes:** none</span><span class="sxs-lookup"><span data-stu-id="e918c-245">**attributes:** none</span></span> 

* <span data-ttu-id="e918c-246">**properties:**</span><span class="sxs-lookup"><span data-stu-id="e918c-246">**properties:**</span></span>  
  * <span data-ttu-id="e918c-247">**child tags:** property</span><span class="sxs-lookup"><span data-stu-id="e918c-247">**child tags:** property</span></span> 
  * <span data-ttu-id="e918c-248">**value: none**</span><span class="sxs-lookup"><span data-stu-id="e918c-248">**value: none**</span></span> 
  * <span data-ttu-id="e918c-249">**attributes:** none</span><span class="sxs-lookup"><span data-stu-id="e918c-249">**attributes:** none</span></span> 

* <span data-ttu-id="e918c-250">**property:**</span><span class="sxs-lookup"><span data-stu-id="e918c-250">**property:**</span></span>  
  * <span data-ttu-id="e918c-251">**child tags:** none</span><span class="sxs-lookup"><span data-stu-id="e918c-251">**child tags:** none</span></span> 
  * <span data-ttu-id="e918c-252">**value:** string, the property value</span><span class="sxs-lookup"><span data-stu-id="e918c-252">**value:** string, the property value</span></span> 
  * <span data-ttu-id="e918c-253">**attributes:** { name: the property name }</span><span class="sxs-lookup"><span data-stu-id="e918c-253">**attributes:** { name: the property name }</span></span> 
  * <span data-ttu-id="e918c-254">**other information:**  Properties based in the header have the following valid names: requestid, NOSPEECH, FALSERECO.</span><span class="sxs-lookup"><span data-stu-id="e918c-254">**other information:**  Properties based in the header have the following valid names: requestid, NOSPEECH, FALSERECO.</span></span> <span data-ttu-id="e918c-255">Properties based in the result portion consist of only HIGHCONF.</span><span class="sxs-lookup"><span data-stu-id="e918c-255">Properties based in the result portion consist of only HIGHCONF.</span></span>
  * <span data-ttu-id="e918c-256">**valid property values:**  requestid: a valid GUID string NOSPEECH: “1” to indicate a no speech false recognition FALSERECO: “1” to indicate that there were no interpretations HIGHCONF: “1” to indicate high confidence (currently above .5 threshold) MIDCONF: “1” to indicate medium-confidence LOWCONF: “1” to indicate low-confidence</span><span class="sxs-lookup"><span data-stu-id="e918c-256">**valid property values:**  requestid: a valid GUID string NOSPEECH: “1” to indicate a no speech false recognition FALSERECO: “1” to indicate that there were no interpretations HIGHCONF: “1” to indicate high confidence (currently above .5 threshold) MIDCONF: “1” to indicate medium-confidence LOWCONF: “1” to indicate low-confidence</span></span>
* <span data-ttu-id="e918c-257">**results:**</span><span class="sxs-lookup"><span data-stu-id="e918c-257">**results:**</span></span>  
  * <span data-ttu-id="e918c-258">**child tags:** result</span><span class="sxs-lookup"><span data-stu-id="e918c-258">**child tags:** result</span></span> 
  * <span data-ttu-id="e918c-259">**value:** none</span><span class="sxs-lookup"><span data-stu-id="e918c-259">**value:** none</span></span> 
  * <span data-ttu-id="e918c-260">**attributes:** none</span><span class="sxs-lookup"><span data-stu-id="e918c-260">**attributes:** none</span></span> 

* <span data-ttu-id="e918c-261">**result:**</span><span class="sxs-lookup"><span data-stu-id="e918c-261">**result:**</span></span>  
  * <span data-ttu-id="e918c-262">**child tags:** name, lexical, confidence, tokens</span><span class="sxs-lookup"><span data-stu-id="e918c-262">**child tags:** name, lexical, confidence, tokens</span></span> 
  * <span data-ttu-id="e918c-263">**value:** none</span><span class="sxs-lookup"><span data-stu-id="e918c-263">**value:** none</span></span> 
  * <span data-ttu-id="e918c-264">**attributes:** none</span><span class="sxs-lookup"><span data-stu-id="e918c-264">**attributes:** none</span></span> 

* <span data-ttu-id="e918c-265">**confidence:**</span><span class="sxs-lookup"><span data-stu-id="e918c-265">**confidence:**</span></span> 
  * <span data-ttu-id="e918c-266">**child tags:** none</span><span class="sxs-lookup"><span data-stu-id="e918c-266">**child tags:** none</span></span> 
  * <span data-ttu-id="e918c-267">**value:** float, indicates result confidence</span><span class="sxs-lookup"><span data-stu-id="e918c-267">**value:** float, indicates result confidence</span></span> 
  * <span data-ttu-id="e918c-268">**attributes:** none</span><span class="sxs-lookup"><span data-stu-id="e918c-268">**attributes:** none</span></span> 

* <span data-ttu-id="e918c-269">**tokens:**</span><span class="sxs-lookup"><span data-stu-id="e918c-269">**tokens:**</span></span>  
  * <span data-ttu-id="e918c-270">**child tags:** token</span><span class="sxs-lookup"><span data-stu-id="e918c-270">**child tags:** token</span></span> 
  * <span data-ttu-id="e918c-271">**value:** none</span><span class="sxs-lookup"><span data-stu-id="e918c-271">**value:** none</span></span> 
  * <span data-ttu-id="e918c-272">**attributes:** none</span><span class="sxs-lookup"><span data-stu-id="e918c-272">**attributes:** none</span></span> 

* <span data-ttu-id="e918c-273">**token:**</span><span class="sxs-lookup"><span data-stu-id="e918c-273">**token:**</span></span>  
  * <span data-ttu-id="e918c-274">**child tags:** name, lexical, pronunciation</span><span class="sxs-lookup"><span data-stu-id="e918c-274">**child tags:** name, lexical, pronunciation</span></span> 
  * <span data-ttu-id="e918c-275">**value:** none</span><span class="sxs-lookup"><span data-stu-id="e918c-275">**value:** none</span></span> 
  * <span data-ttu-id="e918c-276">**attributes:** none</span><span class="sxs-lookup"><span data-stu-id="e918c-276">**attributes:** none</span></span> 

* <span data-ttu-id="e918c-277">**pronunciation:**</span><span class="sxs-lookup"><span data-stu-id="e918c-277">**pronunciation:**</span></span>  
  * <span data-ttu-id="e918c-278">**child tags:** none</span><span class="sxs-lookup"><span data-stu-id="e918c-278">**child tags:** none</span></span> 
  * <span data-ttu-id="e918c-279">**value:** string, the IPA pronunciation of this token</span><span class="sxs-lookup"><span data-stu-id="e918c-279">**value:** string, the IPA pronunciation of this token</span></span> 
  * <span data-ttu-id="e918c-280">**attributes:** none</span><span class="sxs-lookup"><span data-stu-id="e918c-280">**attributes:** none</span></span> 

#### <span data-ttu-id="e918c-281"><a name="SuccessfulRecResponse">Successful Recognition Response</a></span><span class="sxs-lookup"><span data-stu-id="e918c-281"><a name="SuccessfulRecResponse">Successful Recognition Response</a></span></span>

<span data-ttu-id="e918c-282">Example JSON response for a successful voice search.</span><span class="sxs-lookup"><span data-stu-id="e918c-282">Example JSON response for a successful voice search.</span></span> <span data-ttu-id="e918c-283">The comments and formatting of the JSON below is for example reasons only.</span><span class="sxs-lookup"><span data-stu-id="e918c-283">The comments and formatting of the JSON below is for example reasons only.</span></span> <span data-ttu-id="e918c-284">The real result will omit indentations, spaces, smart quotes, comments, etc.</span><span class="sxs-lookup"><span data-stu-id="e918c-284">The real result will omit indentations, spaces, smart quotes, comments, etc.</span></span> 

```
HTTP/1.1 200 OK
Content-Length: XXX
Content-Type: application/json; charset=UTF-8
{
 
  "version":"3.0", 
  "header":{
    "status":"success",
    "scenario":"websearch",
    "name":"Mc Dermant Autos",
    “lexical”:”mac dermant autos”,
    "properties":{
      "requestid":"ABDDD97E-171F-4B75-A491-A977027B0BC3"
    },
  "results":[{
    # Formatted result
    "name":"Mc Dermant Autos",
    # The text of what was spoken
    “lexical”:”mac dermant autos”,
    # Words that make up the result; a word can include a space if there
    # isn’t supposed to be a pause between words when speaking them
    "tokens":[{ 
      # The text in the grammar that matched what was spoken for this token
      "token":"mc dermant", 
      # The text of what was spoken for this token
      “lexical”:”mac dermant”,
      # The IPA pronunciation of this token (I made up M AC DIR MANT; 
      # refer to a real IPA spec for the text of an actual pronunciation)
      “pronunciation”:”M AC DIR MANT”,
    },
    {
      "token":"autos",
      “lexical”:”autos”,
      “pronunciation”:”OW TOS”,
    }],
    “properties”:{
      “HIGHCONF”:”1”
    },
  }],
  }
}

```

```
</speechbox-root>
```
#### <span data-ttu-id="e918c-285"><a name="RecFailure">Recognition Failure</a></span><span class="sxs-lookup"><span data-stu-id="e918c-285"><a name="RecFailure">Recognition Failure</a></span></span>

<span data-ttu-id="e918c-286">Example JSON response for a voice search query where the user’s speech could not be recognized.</span><span class="sxs-lookup"><span data-stu-id="e918c-286">Example JSON response for a voice search query where the user’s speech could not be recognized.</span></span> 


```
HTTP/1.1 200 OK
Content-Length: XXX
Content-Type: application/json; charset=UTF-8

{
   "version":"3.0",
   "results":[{}],
   “header”:{
     "status":"error",
     "scenario":"websearch",
     "properties":{
"requestid":"ABDDD97E-171F-4B75-A491-A977027B0BC3",
       "FALSERECO":"1"
     }
   }
}

```

### <span data-ttu-id="e918c-287"><a name="ErrorResponse">Error Responses</a></span><span class="sxs-lookup"><span data-stu-id="e918c-287"><a name="ErrorResponse">Error Responses</a></span></span>

* <span data-ttu-id="e918c-288">**Http/400 BadRequest:** Will be returned if a required parameter is missing, empty or null, or if the value passed to either a required or optional parameter is invalid.</span><span class="sxs-lookup"><span data-stu-id="e918c-288">**Http/400 BadRequest:** Will be returned if a required parameter is missing, empty or null, or if the value passed to either a required or optional parameter is invalid.</span></span> <span data-ttu-id="e918c-289">The “Invalid” response includes passing a string value that is longer than the allowed length.</span><span class="sxs-lookup"><span data-stu-id="e918c-289">The “Invalid” response includes passing a string value that is longer than the allowed length.</span></span> <span data-ttu-id="e918c-290">A brief description of the problematic parameter will be included.</span><span class="sxs-lookup"><span data-stu-id="e918c-290">A brief description of the problematic parameter will be included.</span></span> 

* <span data-ttu-id="e918c-291">**Http/401 Unauthorized:** Will be returned if the request is not authorized.</span><span class="sxs-lookup"><span data-stu-id="e918c-291">**Http/401 Unauthorized:** Will be returned if the request is not authorized.</span></span> 

* <span data-ttu-id="e918c-292">**Http/502 BadGateway:** Will be returned when the service was unable to perform the recognition.</span><span class="sxs-lookup"><span data-stu-id="e918c-292">**Http/502 BadGateway:** Will be returned when the service was unable to perform the recognition.</span></span> 

* <span data-ttu-id="e918c-293">**Http/403 Forbidden:** Will be returned when there are issues with your authentication or quota.</span><span class="sxs-lookup"><span data-stu-id="e918c-293">**Http/403 Forbidden:** Will be returned when there are issues with your authentication or quota.</span></span>

<span data-ttu-id="e918c-294">Example response for a voice search request submitted with a bad parameter.</span><span class="sxs-lookup"><span data-stu-id="e918c-294">Example response for a voice search request submitted with a bad parameter.</span></span> <span data-ttu-id="e918c-295">This is the error response format regardless of what format the user has requested.</span><span class="sxs-lookup"><span data-stu-id="e918c-295">This is the error response format regardless of what format the user has requested.</span></span> 

```
HTTP/1.0 400 Bad Request
Content-Length: XXX
Content-Type: text/plain; charset=UTF-8

Invalid lat parameter specified       
```

## <span data-ttu-id="e918c-296"><a name="TrouNSupport">Troubleshooting and Support</a></span><span class="sxs-lookup"><span data-stu-id="e918c-296"><a name="TrouNSupport">Troubleshooting and Support</a></span></span>
<span data-ttu-id="e918c-297">Post all questions and issues to the [Bing Speech Service](https://social.msdn.microsoft.com/Forums/en-US/home?forum=SpeechService) MSDN Forum, with complete detail, such as:</span><span class="sxs-lookup"><span data-stu-id="e918c-297">Post all questions and issues to the [Bing Speech Service](https://social.msdn.microsoft.com/Forums/en-US/home?forum=SpeechService) MSDN Forum, with complete detail, such as:</span></span> 
* <span data-ttu-id="e918c-298">An example of the full request string (minus the raw audio data).</span><span class="sxs-lookup"><span data-stu-id="e918c-298">An example of the full request string (minus the raw audio data).</span></span>
* <span data-ttu-id="e918c-299">If applicable, the full output of a failed request, which includes log IDs.</span><span class="sxs-lookup"><span data-stu-id="e918c-299">If applicable, the full output of a failed request, which includes log IDs.</span></span>
* <span data-ttu-id="e918c-300">The percentage of requests that are failing.</span><span class="sxs-lookup"><span data-stu-id="e918c-300">The percentage of requests that are failing.</span></span>


