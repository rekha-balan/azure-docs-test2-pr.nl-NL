---
title: Speech service REST APIs
description: Reference for REST APIs for the Speech service.
services: cognitive-services
author: v-jerkin
ms.service: cognitive-services
ms.technology: speech
ms.topic: article
ms.date: 05/09/2018
ms.author: v-jerkin
ms.openlocfilehash: 64dce26303c0e700da54d371af5cb275b1613d70
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969478"
---
# <a name="speech-service-rest-apis"></a><span data-ttu-id="d7741-103">Speech service REST APIs</span><span class="sxs-lookup"><span data-stu-id="d7741-103">Speech service REST APIs</span></span>

<span data-ttu-id="d7741-104">The REST APIs of the unified Speech service are similar to the APIs provided by the [Speech API](https://docs.microsoft.com/azure/cognitive-services/Speech) (formerly known as the Bing Speech Service).</span><span class="sxs-lookup"><span data-stu-id="d7741-104">The REST APIs of the unified Speech service are similar to the APIs provided by the [Speech API](https://docs.microsoft.com/azure/cognitive-services/Speech) (formerly known as the Bing Speech Service).</span></span> <span data-ttu-id="d7741-105">The endpoints differ from the endpoints used by the previous Speech service.</span><span class="sxs-lookup"><span data-stu-id="d7741-105">The endpoints differ from the endpoints used by the previous Speech service.</span></span>

## <a name="speech-to-text"></a><span data-ttu-id="d7741-106">Speech to Text</span><span class="sxs-lookup"><span data-stu-id="d7741-106">Speech to Text</span></span>

<span data-ttu-id="d7741-107">In the Speech to Text API, only the endpoints used differ from the previous Speech service Speech Recognition API.</span><span class="sxs-lookup"><span data-stu-id="d7741-107">In the Speech to Text API, only the endpoints used differ from the previous Speech service Speech Recognition API.</span></span> <span data-ttu-id="d7741-108">The new endpoints are shown in the table below.</span><span class="sxs-lookup"><span data-stu-id="d7741-108">The new endpoints are shown in the table below.</span></span> <span data-ttu-id="d7741-109">Use the one that matches your subscription region.</span><span class="sxs-lookup"><span data-stu-id="d7741-109">Use the one that matches your subscription region.</span></span>

[!INCLUDE [](../../../includes/cognitive-services-speech-service-endpoints-speech-to-text.md)]

<span data-ttu-id="d7741-110">The Speech to Text API is otherwise similar to the [REST API](https://docs.microsoft.com/azure/cognitive-services/speech/getstarted/getstartedrest) for the previous Speech API.</span><span class="sxs-lookup"><span data-stu-id="d7741-110">The Speech to Text API is otherwise similar to the [REST API](https://docs.microsoft.com/azure/cognitive-services/speech/getstarted/getstartedrest) for the previous Speech API.</span></span>

<span data-ttu-id="d7741-111">The Speech to Text REST API supports only short utterances.</span><span class="sxs-lookup"><span data-stu-id="d7741-111">The Speech to Text REST API supports only short utterances.</span></span> <span data-ttu-id="d7741-112">Requests may contain up to 10 seconds of audio and last a maximum of 14 seconds overall.</span><span class="sxs-lookup"><span data-stu-id="d7741-112">Requests may contain up to 10 seconds of audio and last a maximum of 14 seconds overall.</span></span> <span data-ttu-id="d7741-113">The REST API only returns final results, not partial or interim results.</span><span class="sxs-lookup"><span data-stu-id="d7741-113">The REST API only returns final results, not partial or interim results.</span></span>

> [!NOTE]
> <span data-ttu-id="d7741-114">If you customized the acoustic model or language model, or pronunciation, use your custom endpoint instead.</span><span class="sxs-lookup"><span data-stu-id="d7741-114">If you customized the acoustic model or language model, or pronunciation, use your custom endpoint instead.</span></span>

## <a name="text-to-speech"></a><span data-ttu-id="d7741-115">Text to Speech</span><span class="sxs-lookup"><span data-stu-id="d7741-115">Text to Speech</span></span>

<span data-ttu-id="d7741-116">The new Text to Speech API supports 24-KHz audio output.</span><span class="sxs-lookup"><span data-stu-id="d7741-116">The new Text to Speech API supports 24-KHz audio output.</span></span> <span data-ttu-id="d7741-117">The `X-Microsoft-OutputFormat` header may now contain the following values.</span><span class="sxs-lookup"><span data-stu-id="d7741-117">The `X-Microsoft-OutputFormat` header may now contain the following values.</span></span>

|||
|-|-|
`raw-16khz-16bit-mono-pcm`         | `audio-16khz-16kbps-mono-siren`
`riff-16khz-16kbps-mono-siren`     | `riff-16khz-16bit-mono-pcm`
`audio-16khz-128kbitrate-mono-mp3` | `audio-16khz-64kbitrate-mono-mp3`
`audio-16khz-32kbitrate-mono-mp3`  | `raw-24khz-16bit-mono-pcm`
`riff-24khz-16bit-mono-pcm`        | `audio-24khz-160kbitrate-mono-mp3`
`audio-24khz-96kbitrate-mono-mp3`  | `audio-24khz-48kbitrate-mono-mp3`

<span data-ttu-id="d7741-118">The Speech service now provides two 24-KHz voices:</span><span class="sxs-lookup"><span data-stu-id="d7741-118">The Speech service now provides two 24-KHz voices:</span></span>

<span data-ttu-id="d7741-119">Locale</span><span class="sxs-lookup"><span data-stu-id="d7741-119">Locale</span></span> | <span data-ttu-id="d7741-120">Language</span><span class="sxs-lookup"><span data-stu-id="d7741-120">Language</span></span>   | <span data-ttu-id="d7741-121">Gender</span><span class="sxs-lookup"><span data-stu-id="d7741-121">Gender</span></span> | <span data-ttu-id="d7741-122">Service name mapping</span><span class="sxs-lookup"><span data-stu-id="d7741-122">Service name mapping</span></span>
-------|------------|--------|------------
<span data-ttu-id="d7741-123">en-US</span><span class="sxs-lookup"><span data-stu-id="d7741-123">en-US</span></span>  | <span data-ttu-id="d7741-124">US English</span><span class="sxs-lookup"><span data-stu-id="d7741-124">US English</span></span> | <span data-ttu-id="d7741-125">Female</span><span class="sxs-lookup"><span data-stu-id="d7741-125">Female</span></span> | <span data-ttu-id="d7741-126">"Microsoft Server Speech Text to Speech Voice (en-US, Jessa24kRUS)"</span><span class="sxs-lookup"><span data-stu-id="d7741-126">"Microsoft Server Speech Text to Speech Voice (en-US, Jessa24kRUS)"</span></span> 
<span data-ttu-id="d7741-127">en-US</span><span class="sxs-lookup"><span data-stu-id="d7741-127">en-US</span></span>  | <span data-ttu-id="d7741-128">US English</span><span class="sxs-lookup"><span data-stu-id="d7741-128">US English</span></span> | <span data-ttu-id="d7741-129">Male</span><span class="sxs-lookup"><span data-stu-id="d7741-129">Male</span></span>   | <span data-ttu-id="d7741-130">"Microsoft Server Speech Text to Speech Voice (en-US, Guy24kRUS)"</span><span class="sxs-lookup"><span data-stu-id="d7741-130">"Microsoft Server Speech Text to Speech Voice (en-US, Guy24kRUS)"</span></span>

<span data-ttu-id="d7741-131">The following are the REST endpoints for the unified Speech service Text to Speech API.</span><span class="sxs-lookup"><span data-stu-id="d7741-131">The following are the REST endpoints for the unified Speech service Text to Speech API.</span></span> <span data-ttu-id="d7741-132">Use the endpoint that matches your subscription region.</span><span class="sxs-lookup"><span data-stu-id="d7741-132">Use the endpoint that matches your subscription region.</span></span>

[!INCLUDE [](../../../includes/cognitive-services-speech-service-endpoints-text-to-speech.md)]

<span data-ttu-id="d7741-133">Keep these differences in mind as you refer to the [REST API documentation](https://docs.microsoft.com/azure/cognitive-services/speech/api-reference-rest/bingvoiceoutput) for the previous Speech API.</span><span class="sxs-lookup"><span data-stu-id="d7741-133">Keep these differences in mind as you refer to the [REST API documentation](https://docs.microsoft.com/azure/cognitive-services/speech/api-reference-rest/bingvoiceoutput) for the previous Speech API.</span></span>

## <a name="authentication"></a><span data-ttu-id="d7741-134">Authentication</span><span class="sxs-lookup"><span data-stu-id="d7741-134">Authentication</span></span>

<span data-ttu-id="d7741-135">Sending a request to the Speech service's REST API requires an access token.</span><span class="sxs-lookup"><span data-stu-id="d7741-135">Sending a request to the Speech service's REST API requires an access token.</span></span> <span data-ttu-id="d7741-136">You obtain a token by providing your subscription key to a regional Speech service `issueToken` endpoint, shown in the table below.</span><span class="sxs-lookup"><span data-stu-id="d7741-136">You obtain a token by providing your subscription key to a regional Speech service `issueToken` endpoint, shown in the table below.</span></span> <span data-ttu-id="d7741-137">Use the endpoint that matches your subscription region.</span><span class="sxs-lookup"><span data-stu-id="d7741-137">Use the endpoint that matches your subscription region.</span></span>

[!INCLUDE [](../../../includes/cognitive-services-speech-service-endpoints-token-service.md)]

<span data-ttu-id="d7741-138">Each access token is valid for 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="d7741-138">Each access token is valid for 10 minutes.</span></span> <span data-ttu-id="d7741-139">You may obtain a new token at any time—including, if you like, just before every Speech REST API request.</span><span class="sxs-lookup"><span data-stu-id="d7741-139">You may obtain a new token at any time—including, if you like, just before every Speech REST API request.</span></span> <span data-ttu-id="d7741-140">To minimize network traffic and latency, however, we recommend using the same token for nine minutes.</span><span class="sxs-lookup"><span data-stu-id="d7741-140">To minimize network traffic and latency, however, we recommend using the same token for nine minutes.</span></span>

<span data-ttu-id="d7741-141">The following sections show how to get a token and how to use it in a request.</span><span class="sxs-lookup"><span data-stu-id="d7741-141">The following sections show how to get a token and how to use it in a request.</span></span>

### <a name="getting-a-token-http"></a><span data-ttu-id="d7741-142">Getting a token: HTTP</span><span class="sxs-lookup"><span data-stu-id="d7741-142">Getting a token: HTTP</span></span>

<span data-ttu-id="d7741-143">Below is a sample HTTP request for obtaining a token.</span><span class="sxs-lookup"><span data-stu-id="d7741-143">Below is a sample HTTP request for obtaining a token.</span></span> <span data-ttu-id="d7741-144">Replace `YOUR_SUBSCRIPTION_KEY` with your Speech service subscription key.</span><span class="sxs-lookup"><span data-stu-id="d7741-144">Replace `YOUR_SUBSCRIPTION_KEY` with your Speech service subscription key.</span></span> <span data-ttu-id="d7741-145">If your subscription is not in the West US region, replace the `Host` header with your region's hostname.</span><span class="sxs-lookup"><span data-stu-id="d7741-145">If your subscription is not in the West US region, replace the `Host` header with your region's hostname.</span></span>

```
POST /sts/v1.0/issueToken HTTP/1.1
Ocp-Apim-Subscription-Key: YOUR_SUBSCRIPTION_KEY
Host: westus.api.cognitive.microsoft.com
Content-type: application/x-www-form-urlencoded
Content-Length: 0
```

<span data-ttu-id="d7741-146">The body of the response to this request is the access token in Java Web Token (JWT) format.</span><span class="sxs-lookup"><span data-stu-id="d7741-146">The body of the response to this request is the access token in Java Web Token (JWT) format.</span></span>

### <a name="getting-a-token-powershell"></a><span data-ttu-id="d7741-147">Getting a token: PowerShell</span><span class="sxs-lookup"><span data-stu-id="d7741-147">Getting a token: PowerShell</span></span>

<span data-ttu-id="d7741-148">The Windows PowerShell script below illustrates how to obtain an access token.</span><span class="sxs-lookup"><span data-stu-id="d7741-148">The Windows PowerShell script below illustrates how to obtain an access token.</span></span> <span data-ttu-id="d7741-149">Replace `YOUR_SUBSCRIPTION_KEY` with your Speech service subscription key.</span><span class="sxs-lookup"><span data-stu-id="d7741-149">Replace `YOUR_SUBSCRIPTION_KEY` with your Speech service subscription key.</span></span> <span data-ttu-id="d7741-150">If your subscription is not in the West US region, change the hostname of the given URI accordingly.</span><span class="sxs-lookup"><span data-stu-id="d7741-150">If your subscription is not in the West US region, change the hostname of the given URI accordingly.</span></span>

```Powershell
$FetchTokenHeader = @{
  'Content-type'='application/x-www-form-urlencoded';
  'Content-Length'= '0';
  'Ocp-Apim-Subscription-Key' = 'YOUR_SUBSCRIPTION_KEY'
}

$OAuthToken = Invoke-RestMethod -Method POST -Uri https://westus.api.cognitive.microsoft.com/sts/v1.0/issueToken
 -Headers $FetchTokenHeader

# show the token received
$OAuthToken

```

### <a name="getting-a-token-curl"></a><span data-ttu-id="d7741-151">Getting a token: cURL</span><span class="sxs-lookup"><span data-stu-id="d7741-151">Getting a token: cURL</span></span>

<span data-ttu-id="d7741-152">cURL is a command-line tool available in Linux (and in the Windows Subsystem for Linux).</span><span class="sxs-lookup"><span data-stu-id="d7741-152">cURL is a command-line tool available in Linux (and in the Windows Subsystem for Linux).</span></span> <span data-ttu-id="d7741-153">The cURL command below illustrates how to obtain an access token.</span><span class="sxs-lookup"><span data-stu-id="d7741-153">The cURL command below illustrates how to obtain an access token.</span></span> <span data-ttu-id="d7741-154">Replace `YOUR_SUBSCRIPTION_KEY` with your Speech service subscription key.</span><span class="sxs-lookup"><span data-stu-id="d7741-154">Replace `YOUR_SUBSCRIPTION_KEY` with your Speech service subscription key.</span></span> <span data-ttu-id="d7741-155">If your subscription is not in the West US region, change the hostname of the given URI accordingly.</span><span class="sxs-lookup"><span data-stu-id="d7741-155">If your subscription is not in the West US region, change the hostname of the given URI accordingly.</span></span>

> [!NOTE]
> <span data-ttu-id="d7741-156">The command is shown on multiple lines for readability, but should entered on a single line at a shell prompt.</span><span class="sxs-lookup"><span data-stu-id="d7741-156">The command is shown on multiple lines for readability, but should entered on a single line at a shell prompt.</span></span>

```
curl -v -X POST 
 "https://westus.api.cognitive.microsoft.com/sts/v1.0/issueToken" 
 -H "Content-type: application/x-www-form-urlencoded" 
 -H "Content-Length: 0" 
 -H "Ocp-Apim-Subscription-Key: YOUR_SUBSCRIPTION_KEY"
```

### <a name="getting-a-token-c"></a><span data-ttu-id="d7741-157">Getting a token: C#</span><span class="sxs-lookup"><span data-stu-id="d7741-157">Getting a token: C#</span></span>

<span data-ttu-id="d7741-158">The C# class below illustrates how to obtain an access token.</span><span class="sxs-lookup"><span data-stu-id="d7741-158">The C# class below illustrates how to obtain an access token.</span></span> <span data-ttu-id="d7741-159">Pass your Speech service subscription key when instantiating the class.</span><span class="sxs-lookup"><span data-stu-id="d7741-159">Pass your Speech service subscription key when instantiating the class.</span></span> <span data-ttu-id="d7741-160">If your subscription is not in the West US region, change the hostname of `FetchTokenUri` appropriately.</span><span class="sxs-lookup"><span data-stu-id="d7741-160">If your subscription is not in the West US region, change the hostname of `FetchTokenUri` appropriately.</span></span>

```cs
    /*
     * This class demonstrates how to get a valid access token.
     */
    public class Authentication
    {
        public static readonly string FetchTokenUri =
            "https://westus.api.cognitive.microsoft.com/sts/v1.0/issueToken";
        private string subscriptionKey;
        private string token;

        public Authentication(string subscriptionKey)
        {
            this.subscriptionKey = subscriptionKey;
            this.token = FetchTokenAsync(FetchTokenUri, subscriptionKey).Result;
        }

        public string GetAccessToken()
        {
            return this.token;
        }

        private async Task<string> FetchTokenAsync(string fetchUri, string subscriptionKey)
        {
            using (var client = new HttpClient())
            {
                client.DefaultRequestHeaders.Add("Ocp-Apim-Subscription-Key", subscriptionKey);
                UriBuilder uriBuilder = new UriBuilder(fetchUri);

                var result = await client.PostAsync(uriBuilder.Uri.AbsoluteUri, null);
                Console.WriteLine("Token Uri: {0}", uriBuilder.Uri.AbsoluteUri);
                return await result.Content.ReadAsStringAsync();
            }
        }
    }
```

### <a name="using-a-token"></a><span data-ttu-id="d7741-161">Using a token</span><span class="sxs-lookup"><span data-stu-id="d7741-161">Using a token</span></span>

<span data-ttu-id="d7741-162">To use a token in a REST API request, provide it in the `Authorization` header, following the word `Bearer`.</span><span class="sxs-lookup"><span data-stu-id="d7741-162">To use a token in a REST API request, provide it in the `Authorization` header, following the word `Bearer`.</span></span> <span data-ttu-id="d7741-163">Here, for example, is a sample Text to Speech REST request containing a token.</span><span class="sxs-lookup"><span data-stu-id="d7741-163">Here, for example, is a sample Text to Speech REST request containing a token.</span></span> <span data-ttu-id="d7741-164">Substitute your actual token for `YOUR_ACCESS_TOKEN` and use the correct hostname in the `Host` header.</span><span class="sxs-lookup"><span data-stu-id="d7741-164">Substitute your actual token for `YOUR_ACCESS_TOKEN` and use the correct hostname in the `Host` header.</span></span>

```xml
POST /cognitiveservices/v1 HTTP/1.1
Authorization: Bearer YOUR_ACCESS_TOKEN
Host: westus.tts.speech.microsoft.com
Content-type: application/ssml+xml
Content-Length: 199
Connection: Keep-Alive

<speak version='1.0' xmlns="http://www.w3.org/2001/10/synthesis" xml:lang='en-US'>
<voice name='Microsoft Server Speech Text to Speech Voice (en-US, Jessa24kRUS)'>
    Hello, world!
</voice></speak>
```

### <a name="renewing-authorization"></a><span data-ttu-id="d7741-165">Renewing authorization</span><span class="sxs-lookup"><span data-stu-id="d7741-165">Renewing authorization</span></span>

<span data-ttu-id="d7741-166">The authorization token expires after 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="d7741-166">The authorization token expires after 10 minutes.</span></span> <span data-ttu-id="d7741-167">Renew your authorization by obtaining a new token before it expires—for example, after nine minutes.</span><span class="sxs-lookup"><span data-stu-id="d7741-167">Renew your authorization by obtaining a new token before it expires—for example, after nine minutes.</span></span> 

<span data-ttu-id="d7741-168">The following C# code is a drop-in replacement for the class presented earlier.</span><span class="sxs-lookup"><span data-stu-id="d7741-168">The following C# code is a drop-in replacement for the class presented earlier.</span></span> <span data-ttu-id="d7741-169">The `Authentication` class automatically obtains a new access token every nine minutes using a timer.</span><span class="sxs-lookup"><span data-stu-id="d7741-169">The `Authentication` class automatically obtains a new access token every nine minutes using a timer.</span></span> <span data-ttu-id="d7741-170">This approach ensures that a valid token is always available while your program is running.</span><span class="sxs-lookup"><span data-stu-id="d7741-170">This approach ensures that a valid token is always available while your program is running.</span></span>

> [!NOTE]
> <span data-ttu-id="d7741-171">Instead of using a timer, you could store a timestamp of when the current token was obtained, then request a new one only if the current token is close to expiring.</span><span class="sxs-lookup"><span data-stu-id="d7741-171">Instead of using a timer, you could store a timestamp of when the current token was obtained, then request a new one only if the current token is close to expiring.</span></span> <span data-ttu-id="d7741-172">This approach avoids requesting new tokens unnecessarily and may be more suitable for programs that make infrequent Speech requests.</span><span class="sxs-lookup"><span data-stu-id="d7741-172">This approach avoids requesting new tokens unnecessarily and may be more suitable for programs that make infrequent Speech requests.</span></span>

<span data-ttu-id="d7741-173">As before, make sure the `FetchTokenUri` value matches your subscription region.</span><span class="sxs-lookup"><span data-stu-id="d7741-173">As before, make sure the `FetchTokenUri` value matches your subscription region.</span></span> <span data-ttu-id="d7741-174">Pass your subscription key when instantiating the class.</span><span class="sxs-lookup"><span data-stu-id="d7741-174">Pass your subscription key when instantiating the class.</span></span>

```cs
    /*
     * This class demonstrates how to maintain a valid access token.
     */
    public class Authentication
    {
        public static readonly string FetchTokenUri = 
            "https://westus.api.cognitive.microsoft.com/sts/v1.0/issueToken";
        private string subscriptionKey;
        private string token;
        private Timer accessTokenRenewer;

        //Access token expires every 10 minutes. Renew it every 9 minutes.
        private const int RefreshTokenDuration = 9;

        public Authentication(string subscriptionKey)
        {
            this.subscriptionKey = subscriptionKey;
            this.token = FetchToken(FetchTokenUri, subscriptionKey).Result;

            // renew the token on set duration.
            accessTokenRenewer = new Timer(new TimerCallback(OnTokenExpiredCallback),
                                           this,
                                           TimeSpan.FromMinutes(RefreshTokenDuration),
                                           TimeSpan.FromMilliseconds(-1));
        }

        public string GetAccessToken()
        {
            return this.token;
        }

        private void RenewAccessToken()
        {
            this.token = FetchToken(FetchTokenUri, this.subscriptionKey).Result;
            Console.WriteLine("Renewed token.");
        }

        private void OnTokenExpiredCallback(object stateInfo)
        {
            try
            {
                RenewAccessToken();
            }
            catch (Exception ex)
            {
                Console.WriteLine(string.Format("Failed renewing access token. Details: {0}", ex.Message));
            }
            finally
            {
                try
                {
                    accessTokenRenewer.Change(TimeSpan.FromMinutes(RefreshTokenDuration), TimeSpan.FromMilliseconds(-1));
                }
                catch (Exception ex)
                {
                    Console.WriteLine(string.Format("Failed to reschedule the timer to renew access token. Details: {0}", ex.Message));
                }
            }
        }

        private async Task<string> FetchToken(string fetchUri, string subscriptionKey)
        {
            using (var client = new HttpClient())
            {
                client.DefaultRequestHeaders.Add("Ocp-Apim-Subscription-Key", subscriptionKey);
                UriBuilder uriBuilder = new UriBuilder(fetchUri);

                var result = await client.PostAsync(uriBuilder.Uri.AbsoluteUri, null);
                Console.WriteLine("Token Uri: {0}", uriBuilder.Uri.AbsoluteUri);
                return await result.Content.ReadAsStringAsync();
            }
        }
    }
```

## <a name="next-steps"></a><span data-ttu-id="d7741-175">Next steps</span><span class="sxs-lookup"><span data-stu-id="d7741-175">Next steps</span></span>

- [<span data-ttu-id="d7741-176">Get your Speech trial subscription</span><span class="sxs-lookup"><span data-stu-id="d7741-176">Get your Speech trial subscription</span></span>](https://azure.microsoft.com/try/cognitive-services/)
- [<span data-ttu-id="d7741-177">Customize acoustic models</span><span class="sxs-lookup"><span data-stu-id="d7741-177">Customize acoustic models</span></span>](how-to-customize-acoustic-models.md)
- [<span data-ttu-id="d7741-178">Customize language models</span><span class="sxs-lookup"><span data-stu-id="d7741-178">Customize language models</span></span>](how-to-customize-language-model.md)

