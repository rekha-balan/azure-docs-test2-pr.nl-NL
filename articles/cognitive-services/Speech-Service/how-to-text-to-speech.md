---
title: Use Text to Speech using Speech services
description: Learn how to use Text to Speech in the Speech service.
titleSuffix: Microsoft Cognitive Services
services: cognitive-services
author: v-jerkin
ms.service: cognitive-services
ms.component: speech-service
ms.topic: article
ms.date: 05/07/2018
ms.author: v-jerkin
ms.openlocfilehash: 9b0484503cf655c153d57b39135745b8ba906203
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869177"
---
# <a name="use-text-to-speech-in-speech-service"></a><span data-ttu-id="cd647-103">Use "Text to Speech" in Speech service</span><span class="sxs-lookup"><span data-stu-id="cd647-103">Use "Text to Speech" in Speech service</span></span>

<span data-ttu-id="cd647-104">The Speech service provides Text to Speech functionality through a straightforward HTTP request.</span><span class="sxs-lookup"><span data-stu-id="cd647-104">The Speech service provides Text to Speech functionality through a straightforward HTTP request.</span></span> <span data-ttu-id="cd647-105">You POST the text to be spoken to the appropriate endpoint, and the service returns an audio file (`.wav`) containing synthesized speech.</span><span class="sxs-lookup"><span data-stu-id="cd647-105">You POST the text to be spoken to the appropriate endpoint, and the service returns an audio file (`.wav`) containing synthesized speech.</span></span> <span data-ttu-id="cd647-106">Your application can then use this audio as it likes.</span><span class="sxs-lookup"><span data-stu-id="cd647-106">Your application can then use this audio as it likes.</span></span>

<span data-ttu-id="cd647-107">The body of the POST request for Text to Speech may be plain text (ASCII or UTF8) or an [SSML](speech-synthesis-markup.md) document.</span><span class="sxs-lookup"><span data-stu-id="cd647-107">The body of the POST request for Text to Speech may be plain text (ASCII or UTF8) or an [SSML](speech-synthesis-markup.md) document.</span></span> <span data-ttu-id="cd647-108">Plain-text requests are spoken with a default voice.</span><span class="sxs-lookup"><span data-stu-id="cd647-108">Plain-text requests are spoken with a default voice.</span></span> <span data-ttu-id="cd647-109">In most cases, you want to use an SSML body.</span><span class="sxs-lookup"><span data-stu-id="cd647-109">In most cases, you want to use an SSML body.</span></span> <span data-ttu-id="cd647-110">The HTTP request must include an [authorization](https://docs.microsoft.com/azure/cognitive-services/speech-service/rest-apis#authentication) token.</span><span class="sxs-lookup"><span data-stu-id="cd647-110">The HTTP request must include an [authorization](https://docs.microsoft.com/azure/cognitive-services/speech-service/rest-apis#authentication) token.</span></span> 

<span data-ttu-id="cd647-111">The regional Text to Speech endpoints are shown here.</span><span class="sxs-lookup"><span data-stu-id="cd647-111">The regional Text to Speech endpoints are shown here.</span></span> <span data-ttu-id="cd647-112">Use the one appropriate to your subscription.</span><span class="sxs-lookup"><span data-stu-id="cd647-112">Use the one appropriate to your subscription.</span></span>

[!INCLUDE [](../../../includes/cognitive-services-speech-service-endpoints-text-to-speech.md)]

## <a name="specify-a-voice"></a><span data-ttu-id="cd647-113">Specify a voice</span><span class="sxs-lookup"><span data-stu-id="cd647-113">Specify a voice</span></span>

<span data-ttu-id="cd647-114">To specify a voice, use the `<voice>` [SSML](speech-synthesis-markup.md) tag.</span><span class="sxs-lookup"><span data-stu-id="cd647-114">To specify a voice, use the `<voice>` [SSML](speech-synthesis-markup.md) tag.</span></span> <span data-ttu-id="cd647-115">For example:</span><span class="sxs-lookup"><span data-stu-id="cd647-115">For example:</span></span>

```xml
<speak version='1.0' xmlns="http://www.w3.org/2001/10/synthesis" xml:lang='en-US'>
  <voice  name='Microsoft Server Speech Text to Speech Voice (en-US, JessaRUS)'>
    Hello, world!
  </voice>
</speak>
```

<span data-ttu-id="cd647-116">See [Text to Speech voices](supported-languages.md#text-to-speech) for a list of the available voices and their names.</span><span class="sxs-lookup"><span data-stu-id="cd647-116">See [Text to Speech voices](supported-languages.md#text-to-speech) for a list of the available voices and their names.</span></span>

## <a name="make-a-request"></a><span data-ttu-id="cd647-117">Make a request</span><span class="sxs-lookup"><span data-stu-id="cd647-117">Make a request</span></span>

<span data-ttu-id="cd647-118">A Text to Speech HTTP request is made in POST mode with the text to be spoken in the body of the request.</span><span class="sxs-lookup"><span data-stu-id="cd647-118">A Text to Speech HTTP request is made in POST mode with the text to be spoken in the body of the request.</span></span> <span data-ttu-id="cd647-119">The maximum length of the HTTP request body is 1024 characters.</span><span class="sxs-lookup"><span data-stu-id="cd647-119">The maximum length of the HTTP request body is 1024 characters.</span></span> <span data-ttu-id="cd647-120">The request must have the following headers:</span><span class="sxs-lookup"><span data-stu-id="cd647-120">The request must have the following headers:</span></span> 

<span data-ttu-id="cd647-121">Header</span><span class="sxs-lookup"><span data-stu-id="cd647-121">Header</span></span>|<span data-ttu-id="cd647-122">Values</span><span class="sxs-lookup"><span data-stu-id="cd647-122">Values</span></span>|<span data-ttu-id="cd647-123">Comments</span><span class="sxs-lookup"><span data-stu-id="cd647-123">Comments</span></span>
-|-|-
|`Content-Type` | `application/ssml+xml` | <span data-ttu-id="cd647-124">The input text format.</span><span class="sxs-lookup"><span data-stu-id="cd647-124">The input text format.</span></span>
|`X-Microsoft-OutputFormat`|     `raw-16khz-16bit-mono-pcm`<br>`audio-16khz-16kbps-mono-siren`<br>`riff-16khz-16kbps-mono-siren`<br>`riff-16khz-16bit-mono-pcm`<br>`audio-16khz-128kbitrate-mono-mp3`<br>`audio-16khz-64kbitrate-mono-mp3`<br>`audio-16khz-32kbitrate-mono-mp3`<br>`raw-24khz-16bit-mono-pcm`<br>`riff-24khz-16bit-mono-pcm`<br>`audio-24khz-160kbitrate-mono-mp3`<br>`audio-24khz-96kbitrate-mono-mp3`<br>`audio-24khz-48kbitrate-mono-mp3` | <span data-ttu-id="cd647-125">The output audio format.</span><span class="sxs-lookup"><span data-stu-id="cd647-125">The output audio format.</span></span>
|`User-Agent`   |<span data-ttu-id="cd647-126">Application name</span><span class="sxs-lookup"><span data-stu-id="cd647-126">Application name</span></span> | <span data-ttu-id="cd647-127">The application name is required and must be fewer than 255 characters.</span><span class="sxs-lookup"><span data-stu-id="cd647-127">The application name is required and must be fewer than 255 characters.</span></span>
| `Authorization`   | <span data-ttu-id="cd647-128">Authorization token obtained by presenting your subscription key to the token service.</span><span class="sxs-lookup"><span data-stu-id="cd647-128">Authorization token obtained by presenting your subscription key to the token service.</span></span> <span data-ttu-id="cd647-129">Each token is valid for ten minutes.</span><span class="sxs-lookup"><span data-stu-id="cd647-129">Each token is valid for ten minutes.</span></span> <span data-ttu-id="cd647-130">See [REST APIs: Authentication](rest-apis.md#authentication).</span><span class="sxs-lookup"><span data-stu-id="cd647-130">See [REST APIs: Authentication](rest-apis.md#authentication).</span></span>

> [!NOTE]
> <span data-ttu-id="cd647-131">If your selected voice and output format have different bit rates, the audio is resampled as necessary.</span><span class="sxs-lookup"><span data-stu-id="cd647-131">If your selected voice and output format have different bit rates, the audio is resampled as necessary.</span></span> <span data-ttu-id="cd647-132">24khz voices do not support `audio-16khz-16kbps-mono-siren` and `riff-16khz-16kbps-mono-siren` output formats.</span><span class="sxs-lookup"><span data-stu-id="cd647-132">24khz voices do not support `audio-16khz-16kbps-mono-siren` and `riff-16khz-16kbps-mono-siren` output formats.</span></span> 

<span data-ttu-id="cd647-133">A sample request is shown below.</span><span class="sxs-lookup"><span data-stu-id="cd647-133">A sample request is shown below.</span></span>

```xml
POST /cognitiveservices/v1
HTTP/1.1
Host: westus.tts.speech.microsoft.com
X-Microsoft-OutputFormat: riff-24khz-16bit-mono-pcm
Content-Type: application/ssml+xml
User-Agent: Test TTS application
Authorization: (authorization token)

<speak version='1.0' xmlns="http://www.w3.org/2001/10/synthesis" xml:lang='en-US'>
<voice  name='Microsoft Server Speech Text to Speech Voice (en-US, JessaRUS)'>
    Hello, world!
</voice> </speak>
```

<span data-ttu-id="cd647-134">The response body with a status of 200 contains audio in the specified output format.</span><span class="sxs-lookup"><span data-stu-id="cd647-134">The response body with a status of 200 contains audio in the specified output format.</span></span>

```
HTTP/1.1 200 OK
Content-Length: XXX
Content-Type: audio/x-wav

Response audio payload
```

<span data-ttu-id="cd647-135">If an error occurs, the status codes below are used.</span><span class="sxs-lookup"><span data-stu-id="cd647-135">If an error occurs, the status codes below are used.</span></span> <span data-ttu-id="cd647-136">The response body for the error also contains a description of the problem.</span><span class="sxs-lookup"><span data-stu-id="cd647-136">The response body for the error also contains a description of the problem.</span></span>

|<span data-ttu-id="cd647-137">Code</span><span class="sxs-lookup"><span data-stu-id="cd647-137">Code</span></span>|<span data-ttu-id="cd647-138">Description</span><span class="sxs-lookup"><span data-stu-id="cd647-138">Description</span></span>|<span data-ttu-id="cd647-139">Problem</span><span class="sxs-lookup"><span data-stu-id="cd647-139">Problem</span></span>|
|-|-|-|
<span data-ttu-id="cd647-140">400</span><span class="sxs-lookup"><span data-stu-id="cd647-140">400</span></span> |<span data-ttu-id="cd647-141">Bad Request</span><span class="sxs-lookup"><span data-stu-id="cd647-141">Bad Request</span></span> |<span data-ttu-id="cd647-142">A required parameter is missing, empty, or null.</span><span class="sxs-lookup"><span data-stu-id="cd647-142">A required parameter is missing, empty, or null.</span></span> <span data-ttu-id="cd647-143">Or, the value passed to either a required or optional parameter is invalid.</span><span class="sxs-lookup"><span data-stu-id="cd647-143">Or, the value passed to either a required or optional parameter is invalid.</span></span> <span data-ttu-id="cd647-144">A common issue is a header that is too long.</span><span class="sxs-lookup"><span data-stu-id="cd647-144">A common issue is a header that is too long.</span></span>
<span data-ttu-id="cd647-145">401</span><span class="sxs-lookup"><span data-stu-id="cd647-145">401</span></span>|<span data-ttu-id="cd647-146">Unauthorized</span><span class="sxs-lookup"><span data-stu-id="cd647-146">Unauthorized</span></span> |<span data-ttu-id="cd647-147">The request is not authorized.</span><span class="sxs-lookup"><span data-stu-id="cd647-147">The request is not authorized.</span></span> <span data-ttu-id="cd647-148">Check to make sure your subscription key or token is valid.</span><span class="sxs-lookup"><span data-stu-id="cd647-148">Check to make sure your subscription key or token is valid.</span></span>
<span data-ttu-id="cd647-149">413</span><span class="sxs-lookup"><span data-stu-id="cd647-149">413</span></span>|<span data-ttu-id="cd647-150">Request Entity Too Large</span><span class="sxs-lookup"><span data-stu-id="cd647-150">Request Entity Too Large</span></span>|<span data-ttu-id="cd647-151">The SSML input is longer than 1024 characters.</span><span class="sxs-lookup"><span data-stu-id="cd647-151">The SSML input is longer than 1024 characters.</span></span>
|<span data-ttu-id="cd647-152">502</span><span class="sxs-lookup"><span data-stu-id="cd647-152">502</span></span>|<span data-ttu-id="cd647-153">Bad Gateway</span><span class="sxs-lookup"><span data-stu-id="cd647-153">Bad Gateway</span></span>    | <span data-ttu-id="cd647-154">Network or server-side issue.</span><span class="sxs-lookup"><span data-stu-id="cd647-154">Network or server-side issue.</span></span> <span data-ttu-id="cd647-155">May also indicate invalid headers.</span><span class="sxs-lookup"><span data-stu-id="cd647-155">May also indicate invalid headers.</span></span>

<span data-ttu-id="cd647-156">For more information on the Text to Speech REST API, see [REST APIs](rest-apis.md#text-to-speech).</span><span class="sxs-lookup"><span data-stu-id="cd647-156">For more information on the Text to Speech REST API, see [REST APIs](rest-apis.md#text-to-speech).</span></span>

## <a name="next-steps"></a><span data-ttu-id="cd647-157">Next steps</span><span class="sxs-lookup"><span data-stu-id="cd647-157">Next steps</span></span>

- [<span data-ttu-id="cd647-158">Get your Speech trial subscription</span><span class="sxs-lookup"><span data-stu-id="cd647-158">Get your Speech trial subscription</span></span>](https://azure.microsoft.com/try/cognitive-services/)
- [<span data-ttu-id="cd647-159">Recognize speech in C++</span><span class="sxs-lookup"><span data-stu-id="cd647-159">Recognize speech in C++</span></span>](quickstart-cpp-windows.md)
- [<span data-ttu-id="cd647-160">Recognize speech in C#</span><span class="sxs-lookup"><span data-stu-id="cd647-160">Recognize speech in C#</span></span>](quickstart-csharp-dotnet-windows.md)
- [<span data-ttu-id="cd647-161">Recognize speech in Java</span><span class="sxs-lookup"><span data-stu-id="cd647-161">Recognize speech in Java</span></span>](quickstart-java-android.md)
