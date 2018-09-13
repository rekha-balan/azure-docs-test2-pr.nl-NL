---
title: Get started with the Microsoft Speech Recognition API by using REST | Microsoft Docs
description: Use REST to access the Speech Recognition API in Microsoft Cognitive Services to convert spoken audio to text.
services: cognitive-services
author: zhouwangzw
manager: wolfma
ms.service: cognitive-services
ms.component: bing-speech
ms.topic: article
ms.date: 09/15/2017
ms.author: zhouwang
ms.openlocfilehash: 53785cdfd75c23910802f2be20e6305817b3b097
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856735"
---
# <a name="get-started-with-speech-recognition-by-using-the-rest-api"></a><span data-ttu-id="52908-103">Get started with speech recognition by using the REST API</span><span class="sxs-lookup"><span data-stu-id="52908-103">Get started with speech recognition by using the REST API</span></span>

<span data-ttu-id="52908-104">With cloud-based Speech Service, you can develop applications by using the REST API to convert spoken audio to text.</span><span class="sxs-lookup"><span data-stu-id="52908-104">With cloud-based Speech Service, you can develop applications by using the REST API to convert spoken audio to text.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="52908-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="52908-105">Prerequisites</span></span>

### <a name="subscribe-to-the-speech-api-and-get-a-free-trial-subscription-key"></a><span data-ttu-id="52908-106">Subscribe to the Speech API, and get a free trial subscription key</span><span class="sxs-lookup"><span data-stu-id="52908-106">Subscribe to the Speech API, and get a free trial subscription key</span></span>

<span data-ttu-id="52908-107">The Speech API is part of Cognitive Services (previously Project Oxford).</span><span class="sxs-lookup"><span data-stu-id="52908-107">The Speech API is part of Cognitive Services (previously Project Oxford).</span></span> <span data-ttu-id="52908-108">You can get free trial subscription keys from the [Cognitive Services subscription](https://azure.microsoft.com/try/cognitive-services/) page.</span><span class="sxs-lookup"><span data-stu-id="52908-108">You can get free trial subscription keys from the [Cognitive Services subscription](https://azure.microsoft.com/try/cognitive-services/) page.</span></span> <span data-ttu-id="52908-109">After you select the Speech API, select **Get API Key** to get the key.</span><span class="sxs-lookup"><span data-stu-id="52908-109">After you select the Speech API, select **Get API Key** to get the key.</span></span> <span data-ttu-id="52908-110">It returns a primary and secondary key.</span><span class="sxs-lookup"><span data-stu-id="52908-110">It returns a primary and secondary key.</span></span> <span data-ttu-id="52908-111">Both keys are tied to the same quota, so you can use either key.</span><span class="sxs-lookup"><span data-stu-id="52908-111">Both keys are tied to the same quota, so you can use either key.</span></span>

> [!IMPORTANT]
>* <span data-ttu-id="52908-112">Get a subscription key.</span><span class="sxs-lookup"><span data-stu-id="52908-112">Get a subscription key.</span></span> <span data-ttu-id="52908-113">Before you can access the REST API, you must have a [subscription key](https://azure.microsoft.com/try/cognitive-services/).</span><span class="sxs-lookup"><span data-stu-id="52908-113">Before you can access the REST API, you must have a [subscription key](https://azure.microsoft.com/try/cognitive-services/).</span></span>
>
>* <span data-ttu-id="52908-114">Use your subscription key.</span><span class="sxs-lookup"><span data-stu-id="52908-114">Use your subscription key.</span></span> <span data-ttu-id="52908-115">In the following REST samples, replace YOUR_SUBSCRIPTION_KEY with your own subscription key.</span><span class="sxs-lookup"><span data-stu-id="52908-115">In the following REST samples, replace YOUR_SUBSCRIPTION_KEY with your own subscription key.</span></span> 
>
>* <span data-ttu-id="52908-116">Refer to the [authentication](../how-to/how-to-authentication.md) page for how to get a subscription key.</span><span class="sxs-lookup"><span data-stu-id="52908-116">Refer to the [authentication](../how-to/how-to-authentication.md) page for how to get a subscription key.</span></span>

### <a name="prerecorded-audio-file"></a><span data-ttu-id="52908-117">Prerecorded audio file</span><span class="sxs-lookup"><span data-stu-id="52908-117">Prerecorded audio file</span></span>

<span data-ttu-id="52908-118">In this example, we use a recorded audio file to illustrate how to use the REST API.</span><span class="sxs-lookup"><span data-stu-id="52908-118">In this example, we use a recorded audio file to illustrate how to use the REST API.</span></span> <span data-ttu-id="52908-119">Record an audio file of yourself saying a short phrase.</span><span class="sxs-lookup"><span data-stu-id="52908-119">Record an audio file of yourself saying a short phrase.</span></span> <span data-ttu-id="52908-120">For example, say "What is the weather like today?"</span><span class="sxs-lookup"><span data-stu-id="52908-120">For example, say "What is the weather like today?"</span></span> <span data-ttu-id="52908-121">or "Find funny movies to watch."</span><span class="sxs-lookup"><span data-stu-id="52908-121">or "Find funny movies to watch."</span></span> <span data-ttu-id="52908-122">The speech recognition API also supports external microphone input.</span><span class="sxs-lookup"><span data-stu-id="52908-122">The speech recognition API also supports external microphone input.</span></span>

> [!NOTE]
> <span data-ttu-id="52908-123">The example requires that audio is recorded as a WAV file with **PCM single channel (mono), 16 KHz**.</span><span class="sxs-lookup"><span data-stu-id="52908-123">The example requires that audio is recorded as a WAV file with **PCM single channel (mono), 16 KHz**.</span></span>

## <a name="build-a-recognition-request-and-send-it-to-the-speech-recognition-service"></a><span data-ttu-id="52908-124">Build a recognition request, and send it to the speech recognition service</span><span class="sxs-lookup"><span data-stu-id="52908-124">Build a recognition request, and send it to the speech recognition service</span></span>

<span data-ttu-id="52908-125">The next step for speech recognition is to send a POST request to the Speech HTTP endpoints with the proper request header and body.</span><span class="sxs-lookup"><span data-stu-id="52908-125">The next step for speech recognition is to send a POST request to the Speech HTTP endpoints with the proper request header and body.</span></span>

### <a name="service-uri"></a><span data-ttu-id="52908-126">Service URI</span><span class="sxs-lookup"><span data-stu-id="52908-126">Service URI</span></span>

<span data-ttu-id="52908-127">The speech recognition service URI is defined based on [recognition modes](../concepts.md#recognition-modes) and [recognition languages](../concepts.md#recognition-languages):</span><span class="sxs-lookup"><span data-stu-id="52908-127">The speech recognition service URI is defined based on [recognition modes](../concepts.md#recognition-modes) and [recognition languages](../concepts.md#recognition-languages):</span></span>

```HTTP
https://speech.platform.bing.com/speech/recognition/<RECOGNITION_MODE>/cognitiveservices/v1?language=<LANGUAGE_TAG>&format=<OUTPUT_FORMAT>
```

<span data-ttu-id="52908-128">`<RECOGNITION_MODE>` specifies the recognition mode and must be one of the following values: `interactive`, `conversation`, or `dictation`.</span><span class="sxs-lookup"><span data-stu-id="52908-128">`<RECOGNITION_MODE>` specifies the recognition mode and must be one of the following values: `interactive`, `conversation`, or `dictation`.</span></span> <span data-ttu-id="52908-129">It's a required resource path in the URI.</span><span class="sxs-lookup"><span data-stu-id="52908-129">It's a required resource path in the URI.</span></span> <span data-ttu-id="52908-130">For more information, see [Recognition modes](../concepts.md#recognition-modes).</span><span class="sxs-lookup"><span data-stu-id="52908-130">For more information, see [Recognition modes](../concepts.md#recognition-modes).</span></span>

<span data-ttu-id="52908-131">`<LANGUAGE_TAG>` is a required parameter in the query string.</span><span class="sxs-lookup"><span data-stu-id="52908-131">`<LANGUAGE_TAG>` is a required parameter in the query string.</span></span> <span data-ttu-id="52908-132">It defines the target language for audio conversion: for example, `en-US` for English (United States).</span><span class="sxs-lookup"><span data-stu-id="52908-132">It defines the target language for audio conversion: for example, `en-US` for English (United States).</span></span> <span data-ttu-id="52908-133">For more information, see [Recognition languages](../concepts.md#recognition-languages).</span><span class="sxs-lookup"><span data-stu-id="52908-133">For more information, see [Recognition languages](../concepts.md#recognition-languages).</span></span>

<span data-ttu-id="52908-134">`<OUTPUT_FORMAT>` is an optional parameter in the query string.</span><span class="sxs-lookup"><span data-stu-id="52908-134">`<OUTPUT_FORMAT>` is an optional parameter in the query string.</span></span> <span data-ttu-id="52908-135">Its allowed values are `simple` and `detailed`.</span><span class="sxs-lookup"><span data-stu-id="52908-135">Its allowed values are `simple` and `detailed`.</span></span> <span data-ttu-id="52908-136">By default, the service returns results in `simple` format.</span><span class="sxs-lookup"><span data-stu-id="52908-136">By default, the service returns results in `simple` format.</span></span> <span data-ttu-id="52908-137">For more information, see [Output format](../concepts.md#output-format).</span><span class="sxs-lookup"><span data-stu-id="52908-137">For more information, see [Output format](../concepts.md#output-format).</span></span>

<span data-ttu-id="52908-138">Some examples of service URIs are listed in the following table.</span><span class="sxs-lookup"><span data-stu-id="52908-138">Some examples of service URIs are listed in the following table.</span></span>

| <span data-ttu-id="52908-139">Recognition mode</span><span class="sxs-lookup"><span data-stu-id="52908-139">Recognition mode</span></span>  | <span data-ttu-id="52908-140">Language</span><span class="sxs-lookup"><span data-stu-id="52908-140">Language</span></span> | <span data-ttu-id="52908-141">Output format</span><span class="sxs-lookup"><span data-stu-id="52908-141">Output format</span></span> | <span data-ttu-id="52908-142">Service URI</span><span class="sxs-lookup"><span data-stu-id="52908-142">Service URI</span></span> |
|---|---|---|---|
| `interactive` | <span data-ttu-id="52908-143">pt-BR</span><span class="sxs-lookup"><span data-stu-id="52908-143">pt-BR</span></span> | <span data-ttu-id="52908-144">Default</span><span class="sxs-lookup"><span data-stu-id="52908-144">Default</span></span> | https://speech.platform.bing.com/speech/recognition/interactive/cognitiveservices/v1?language=pt-BR |
| `conversation` | <span data-ttu-id="52908-145">en-US</span><span class="sxs-lookup"><span data-stu-id="52908-145">en-US</span></span> | <span data-ttu-id="52908-146">Detailed</span><span class="sxs-lookup"><span data-stu-id="52908-146">Detailed</span></span> |https://speech.platform.bing.com/speech/recognition/conversation/cognitiveservices/v1?language=en-US&format=detailed |
| `dictation` | <span data-ttu-id="52908-147">fr-FR</span><span class="sxs-lookup"><span data-stu-id="52908-147">fr-FR</span></span> | <span data-ttu-id="52908-148">Simple</span><span class="sxs-lookup"><span data-stu-id="52908-148">Simple</span></span> | https://speech.platform.bing.com/speech/recognition/dictation/cognitiveservices/v1?language=fr-FR&format=simple |

> [!NOTE]
> <span data-ttu-id="52908-149">The service URI is needed only when your application uses REST APIs to call the speech recognition service.</span><span class="sxs-lookup"><span data-stu-id="52908-149">The service URI is needed only when your application uses REST APIs to call the speech recognition service.</span></span> <span data-ttu-id="52908-150">If you use one of the [client libraries](GetStartedClientLibraries.md), you usually don't need to know which URI is used.</span><span class="sxs-lookup"><span data-stu-id="52908-150">If you use one of the [client libraries](GetStartedClientLibraries.md), you usually don't need to know which URI is used.</span></span> <span data-ttu-id="52908-151">The client libraries might use different service URIs, which are applicable only for a specific client library.</span><span class="sxs-lookup"><span data-stu-id="52908-151">The client libraries might use different service URIs, which are applicable only for a specific client library.</span></span> <span data-ttu-id="52908-152">For more information, see the client library of your choice.</span><span class="sxs-lookup"><span data-stu-id="52908-152">For more information, see the client library of your choice.</span></span>

### <a name="request-headers"></a><span data-ttu-id="52908-153">Request headers</span><span class="sxs-lookup"><span data-stu-id="52908-153">Request headers</span></span>

<span data-ttu-id="52908-154">The following fields must be set in the request header:</span><span class="sxs-lookup"><span data-stu-id="52908-154">The following fields must be set in the request header:</span></span>

- <span data-ttu-id="52908-155">`Ocp-Apim-Subscription-Key`: Each time that you call the service, you must pass your subscription key in the `Ocp-Apim-Subscription-Key` header.</span><span class="sxs-lookup"><span data-stu-id="52908-155">`Ocp-Apim-Subscription-Key`: Each time that you call the service, you must pass your subscription key in the `Ocp-Apim-Subscription-Key` header.</span></span> <span data-ttu-id="52908-156">Speech Service also supports passing authorization tokens instead of subscription keys.</span><span class="sxs-lookup"><span data-stu-id="52908-156">Speech Service also supports passing authorization tokens instead of subscription keys.</span></span> <span data-ttu-id="52908-157">For more information, see [Authentication](../How-to/how-to-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="52908-157">For more information, see [Authentication](../How-to/how-to-authentication.md).</span></span>
- <span data-ttu-id="52908-158">`Content-type`: The `Content-type` field describes the format and codec of the audio stream.</span><span class="sxs-lookup"><span data-stu-id="52908-158">`Content-type`: The `Content-type` field describes the format and codec of the audio stream.</span></span> <span data-ttu-id="52908-159">Currently, only WAV file and PCM Mono 16000 encoding is supported.</span><span class="sxs-lookup"><span data-stu-id="52908-159">Currently, only WAV file and PCM Mono 16000 encoding is supported.</span></span> <span data-ttu-id="52908-160">The Content-type value for this format is `audio/wav; codec=audio/pcm; samplerate=16000`.</span><span class="sxs-lookup"><span data-stu-id="52908-160">The Content-type value for this format is `audio/wav; codec=audio/pcm; samplerate=16000`.</span></span>

<span data-ttu-id="52908-161">The `Transfer-Encoding` field is optional.</span><span class="sxs-lookup"><span data-stu-id="52908-161">The `Transfer-Encoding` field is optional.</span></span> <span data-ttu-id="52908-162">If you set this field to `chunked`, you can chop the audio into small chunks.</span><span class="sxs-lookup"><span data-stu-id="52908-162">If you set this field to `chunked`, you can chop the audio into small chunks.</span></span> <span data-ttu-id="52908-163">For more information, see [Chunked transfer](../How-to/how-to-chunked-transfer.md).</span><span class="sxs-lookup"><span data-stu-id="52908-163">For more information, see [Chunked transfer](../How-to/how-to-chunked-transfer.md).</span></span>

<span data-ttu-id="52908-164">The following is a sample request header:</span><span class="sxs-lookup"><span data-stu-id="52908-164">The following is a sample request header:</span></span>

```HTTP
POST https://speech.platform.bing.com/speech/recognition/interactive/cognitiveservices/v1?language=en-US&format=detailed HTTP/1.1
Accept: application/json;text/xml
Content-Type: audio/wav; codec=audio/pcm; samplerate=16000
Ocp-Apim-Subscription-Key: YOUR_SUBSCRIPTION_KEY
Host: speech.platform.bing.com
Transfer-Encoding: chunked
Expect: 100-continue
```

### <a name="send-a-request-to-the-service"></a><span data-ttu-id="52908-165">Send a request to the service</span><span class="sxs-lookup"><span data-stu-id="52908-165">Send a request to the service</span></span>

<span data-ttu-id="52908-166">The following example shows how to send a speech recognition request to Speech REST endpoints.</span><span class="sxs-lookup"><span data-stu-id="52908-166">The following example shows how to send a speech recognition request to Speech REST endpoints.</span></span> <span data-ttu-id="52908-167">It uses the `interactive` recognition mode.</span><span class="sxs-lookup"><span data-stu-id="52908-167">It uses the `interactive` recognition mode.</span></span>

> [!NOTE]
> <span data-ttu-id="52908-168">Replace `YOUR_AUDIO_FILE` with the path to your prerecorded audio file.</span><span class="sxs-lookup"><span data-stu-id="52908-168">Replace `YOUR_AUDIO_FILE` with the path to your prerecorded audio file.</span></span> <span data-ttu-id="52908-169">Replace `YOUR_SUBSCRIPTION_KEY` with your own subscription key.</span><span class="sxs-lookup"><span data-stu-id="52908-169">Replace `YOUR_SUBSCRIPTION_KEY` with your own subscription key.</span></span>

# <a name="powershelltabpowershell"></a>[<span data-ttu-id="52908-170">PowerShell</span><span class="sxs-lookup"><span data-stu-id="52908-170">PowerShell</span></span>](#tab/Powershell)

```Powershell

$SpeechServiceURI =
'https://speech.platform.bing.com/speech/recognition/interactive/cognitiveservices/v1?language=en-us&format=detailed'

# $OAuthToken is the authorization token returned by the token service.
$RecoRequestHeader = @{
  'Ocp-Apim-Subscription-Key' = 'YOUR_SUBSCRIPTION_KEY';
  'Transfer-Encoding' = 'chunked';
  'Content-type' = 'audio/wav; codec=audio/pcm; samplerate=16000'
}

# Read audio into byte array
$audioBytes = [System.IO.File]::ReadAllBytes("YOUR_AUDIO_FILE")

$RecoResponse = Invoke-RestMethod -Method POST -Uri $SpeechServiceURI -Headers $RecoRequestHeader -Body $audioBytes

# Show the result
$RecoResponse

```

# <a name="curltabcurl"></a>[<span data-ttu-id="52908-171">curl</span><span class="sxs-lookup"><span data-stu-id="52908-171">curl</span></span>](#tab/curl)

<span data-ttu-id="52908-172">The example uses curl on Linux with bash.</span><span class="sxs-lookup"><span data-stu-id="52908-172">The example uses curl on Linux with bash.</span></span> <span data-ttu-id="52908-173">If it's not available on your platform, you might need to install curl.</span><span class="sxs-lookup"><span data-stu-id="52908-173">If it's not available on your platform, you might need to install curl.</span></span> <span data-ttu-id="52908-174">The example also works on Cygwin on Windows, Git Bash, zsh, and other shells.</span><span class="sxs-lookup"><span data-stu-id="52908-174">The example also works on Cygwin on Windows, Git Bash, zsh, and other shells.</span></span>

> [!NOTE]
> <span data-ttu-id="52908-175">Keep the `@` before the audio file name when replacing `YOUR_AUDIO_FILE` with the path to your prerecorded audio file, as it indicates that the value of `--data-binary` is a file name instead of data.</span><span class="sxs-lookup"><span data-stu-id="52908-175">Keep the `@` before the audio file name when replacing `YOUR_AUDIO_FILE` with the path to your prerecorded audio file, as it indicates that the value of `--data-binary` is a file name instead of data.</span></span>

```
curl -v -X POST "https://speech.platform.bing.com/speech/recognition/interactive/cognitiveservices/v1?language=en-us&format=detailed" -H "Transfer-Encoding: chunked" -H "Ocp-Apim-Subscription-Key: YOUR_SUBSCRIPTION_KEY" -H "Content-type: audio/wav; codec=audio/pcm; samplerate=16000" --data-binary @YOUR_AUDIO_FILE
```

# <a name="ctabcsharp"></a>[<span data-ttu-id="52908-176">C#</span><span class="sxs-lookup"><span data-stu-id="52908-176">C#</span></span>](#tab/CSharp)

```cs
HttpWebRequest request = null;
request = (HttpWebRequest)HttpWebRequest.Create(requestUri);
request.SendChunked = true;
request.Accept = @"application/json;text/xml";
request.Method = "POST";
request.ProtocolVersion = HttpVersion.Version11;
request.ContentType = @"audio/wav; codec=audio/pcm; samplerate=16000";
request.Headers["Ocp-Apim-Subscription-Key"] = "YOUR_SUBSCRIPTION_KEY";

// Send an audio file by 1024 byte chunks
using (FileStream fs = new FileStream(YOUR_AUDIO_FILE, FileMode.Open, FileAccess.Read))
{

    /*
    * Open a request stream and write 1024 byte chunks in the stream one at a time.
    */
    byte[] buffer = null;
    int bytesRead = 0;
    using (Stream requestStream = request.GetRequestStream())
    {
        /*
        * Read 1024 raw bytes from the input audio file.
        */
        buffer = new Byte[checked((uint)Math.Min(1024, (int)fs.Length))];
        while ((bytesRead = fs.Read(buffer, 0, buffer.Length)) != 0)
        {
            requestStream.Write(buffer, 0, bytesRead);
        }

        // Flush
        requestStream.Flush();
    }
}
```

---

## <a name="process-the-speech-recognition-response"></a><span data-ttu-id="52908-177">Process the speech recognition response</span><span class="sxs-lookup"><span data-stu-id="52908-177">Process the speech recognition response</span></span>

<span data-ttu-id="52908-178">After processing the request, Speech Service returns the results in a response as JSON format.</span><span class="sxs-lookup"><span data-stu-id="52908-178">After processing the request, Speech Service returns the results in a response as JSON format.</span></span>

> [!NOTE]
> <span data-ttu-id="52908-179">If the previous code returns an error, see [Troubleshooting](../troubleshooting.md) to locate the possible cause.</span><span class="sxs-lookup"><span data-stu-id="52908-179">If the previous code returns an error, see [Troubleshooting](../troubleshooting.md) to locate the possible cause.</span></span>

<span data-ttu-id="52908-180">The following code snippet shows an example of how you can read the response from the stream.</span><span class="sxs-lookup"><span data-stu-id="52908-180">The following code snippet shows an example of how you can read the response from the stream.</span></span>

# <a name="powershelltabpowershell"></a>[<span data-ttu-id="52908-181">PowerShell</span><span class="sxs-lookup"><span data-stu-id="52908-181">PowerShell</span></span>](#tab/Powershell)

```Powershell
# show the response in JSON format
ConvertTo-Json $RecoResponse
```

# <a name="curltabcurl"></a>[<span data-ttu-id="52908-182">curl</span><span class="sxs-lookup"><span data-stu-id="52908-182">curl</span></span>](#tab/curl)

<span data-ttu-id="52908-183">In this example, curl directly returns the response message in a string.</span><span class="sxs-lookup"><span data-stu-id="52908-183">In this example, curl directly returns the response message in a string.</span></span> <span data-ttu-id="52908-184">If you want to show it in JSON format, you can use additional tools, for example, jq.</span><span class="sxs-lookup"><span data-stu-id="52908-184">If you want to show it in JSON format, you can use additional tools, for example, jq.</span></span>

```
curl -X POST "https://speech.platform.bing.com/speech/recognition/interactive/cognitiveservices/v1?language=en-us&format=detailed" -H "Transfer-Encoding: chunked" -H "Ocp-Apim-Subscription-Key: YOUR_SUBSCRIPTION_KEY" -H "Content-type: audio/wav; codec=audio/pcm; samplerate=16000" --data-binary @YOUR_AUDIO_FILE | jq
```

# <a name="ctabcsharp"></a>[<span data-ttu-id="52908-185">C#</span><span class="sxs-lookup"><span data-stu-id="52908-185">C#</span></span>](#tab/CSharp)

```cs
/*
* Get the response from the service.
*/
Console.WriteLine("Response:");
using (WebResponse response = request.GetResponse())
{
    Console.WriteLine(((HttpWebResponse)response).StatusCode);

    using (StreamReader sr = new StreamReader(response.GetResponseStream()))
    {
        responseString = sr.ReadToEnd();
    }

    Console.WriteLine(responseString);
    Console.ReadLine();
}
```

---

<span data-ttu-id="52908-186">The following sample is a JSON response:</span><span class="sxs-lookup"><span data-stu-id="52908-186">The following sample is a JSON response:</span></span>

```json
OK
{
  "RecognitionStatus": "Success",
  "Offset": 22500000,
  "Duration": 21000000,
  "NBest": [{
    "Confidence": 0.941552162,
    "Lexical": "find a funny movie to watch",
    "ITN": "find a funny movie to watch",
    "MaskedITN": "find a funny movie to watch",
    "Display": "Find a funny movie to watch."
  }]
}
```

## <a name="limitations"></a><span data-ttu-id="52908-187">Limitations</span><span class="sxs-lookup"><span data-stu-id="52908-187">Limitations</span></span>

<span data-ttu-id="52908-188">The REST API has some limitations:</span><span class="sxs-lookup"><span data-stu-id="52908-188">The REST API has some limitations:</span></span>

- <span data-ttu-id="52908-189">It supports audio stream only up to 15 seconds.</span><span class="sxs-lookup"><span data-stu-id="52908-189">It supports audio stream only up to 15 seconds.</span></span>
- <span data-ttu-id="52908-190">It doesn't support intermediate results during recognition.</span><span class="sxs-lookup"><span data-stu-id="52908-190">It doesn't support intermediate results during recognition.</span></span> <span data-ttu-id="52908-191">Users receive only the final recognition result.</span><span class="sxs-lookup"><span data-stu-id="52908-191">Users receive only the final recognition result.</span></span>

<span data-ttu-id="52908-192">To remove these limitations, use Speech [client libraries](GetStartedClientLibraries.md).</span><span class="sxs-lookup"><span data-stu-id="52908-192">To remove these limitations, use Speech [client libraries](GetStartedClientLibraries.md).</span></span> <span data-ttu-id="52908-193">Or you can work directly with the [Speech WebSocket protocol](../API-Reference-REST/websocketprotocol.md).</span><span class="sxs-lookup"><span data-stu-id="52908-193">Or you can work directly with the [Speech WebSocket protocol](../API-Reference-REST/websocketprotocol.md).</span></span>

## <a name="whats-next"></a><span data-ttu-id="52908-194">What's next</span><span class="sxs-lookup"><span data-stu-id="52908-194">What's next</span></span>

- <span data-ttu-id="52908-195">To see how to use the REST API in C#, Java, etc., see these [sample applications](../samples.md).</span><span class="sxs-lookup"><span data-stu-id="52908-195">To see how to use the REST API in C#, Java, etc., see these [sample applications](../samples.md).</span></span>
- <span data-ttu-id="52908-196">To locate and fix errors, see [Troubleshooting](../troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="52908-196">To locate and fix errors, see [Troubleshooting](../troubleshooting.md).</span></span>
- <span data-ttu-id="52908-197">To use more advanced features, see how to get started by using Speech [client libraries](GetStartedClientLibraries.md).</span><span class="sxs-lookup"><span data-stu-id="52908-197">To use more advanced features, see how to get started by using Speech [client libraries](GetStartedClientLibraries.md).</span></span>

### <a name="license"></a><span data-ttu-id="52908-198">License</span><span class="sxs-lookup"><span data-stu-id="52908-198">License</span></span>

<span data-ttu-id="52908-199">All Cognitive Services SDKs and samples are licensed with the MIT License.</span><span class="sxs-lookup"><span data-stu-id="52908-199">All Cognitive Services SDKs and samples are licensed with the MIT License.</span></span> <span data-ttu-id="52908-200">For more information, see [License](https://github.com/Microsoft/Cognitive-Speech-STT-JavaScript/blob/master/LICENSE.md).</span><span class="sxs-lookup"><span data-stu-id="52908-200">For more information, see [License](https://github.com/Microsoft/Cognitive-Speech-STT-JavaScript/blob/master/LICENSE.md).</span></span>
