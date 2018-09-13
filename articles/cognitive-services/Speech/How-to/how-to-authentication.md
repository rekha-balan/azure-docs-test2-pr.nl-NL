---
title: Authenticate to Microsoft Speech Service | Microsoft Docs
description: Request authentication to use the Microsoft Speech API
services: cognitive-services
author: zhouwangzw
manager: wolfma
ms.service: cognitive-services
ms.component: bing-speech
ms.topic: article
ms.date: 09/15/2017
ms.author: zhouwang
ms.openlocfilehash: e36168cf3ff938af44f1028c2d26fd475d60b148
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965512"
---
# <a name="authenticate-to-the-speech-api"></a><span data-ttu-id="559d4-103">Authenticate to the Speech API</span><span class="sxs-lookup"><span data-stu-id="559d4-103">Authenticate to the Speech API</span></span>

<span data-ttu-id="559d4-104">Speech Service supports authentication by using:</span><span class="sxs-lookup"><span data-stu-id="559d4-104">Speech Service supports authentication by using:</span></span>

- <span data-ttu-id="559d4-105">A subscription key.</span><span class="sxs-lookup"><span data-stu-id="559d4-105">A subscription key.</span></span>
- <span data-ttu-id="559d4-106">An authorization token.</span><span class="sxs-lookup"><span data-stu-id="559d4-106">An authorization token.</span></span>

## <a name="use-a-subscription-key"></a><span data-ttu-id="559d4-107">Use a subscription key</span><span class="sxs-lookup"><span data-stu-id="559d4-107">Use a subscription key</span></span>

<span data-ttu-id="559d4-108">To use Speech Service, you must first subscribe to the Speech API that's part of Cognitive Services (previously Project Oxford).</span><span class="sxs-lookup"><span data-stu-id="559d4-108">To use Speech Service, you must first subscribe to the Speech API that's part of Cognitive Services (previously Project Oxford).</span></span> <span data-ttu-id="559d4-109">You can get free trial subscription keys from the [Cognitive Services subscription](https://azure.microsoft.com/try/cognitive-services/) page.</span><span class="sxs-lookup"><span data-stu-id="559d4-109">You can get free trial subscription keys from the [Cognitive Services subscription](https://azure.microsoft.com/try/cognitive-services/) page.</span></span> <span data-ttu-id="559d4-110">After you select the Speech API, select **Get API Key** to get the key.</span><span class="sxs-lookup"><span data-stu-id="559d4-110">After you select the Speech API, select **Get API Key** to get the key.</span></span> <span data-ttu-id="559d4-111">It returns a primary and secondary key.</span><span class="sxs-lookup"><span data-stu-id="559d4-111">It returns a primary and secondary key.</span></span> <span data-ttu-id="559d4-112">Both keys are tied to the same quota, so you can use either key.</span><span class="sxs-lookup"><span data-stu-id="559d4-112">Both keys are tied to the same quota, so you can use either key.</span></span>

<span data-ttu-id="559d4-113">For long-term use or an increased quota, sign up for an [Azure account](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="559d4-113">For long-term use or an increased quota, sign up for an [Azure account](https://azure.microsoft.com/free/).</span></span>

<span data-ttu-id="559d4-114">To use the Speech REST API, you need to pass the subscription key in the `Ocp-Apim-Subscription-Key` field in the request header.</span><span class="sxs-lookup"><span data-stu-id="559d4-114">To use the Speech REST API, you need to pass the subscription key in the `Ocp-Apim-Subscription-Key` field in the request header.</span></span>

<span data-ttu-id="559d4-115">Name</span><span class="sxs-lookup"><span data-stu-id="559d4-115">Name</span></span>| <span data-ttu-id="559d4-116">Format</span><span class="sxs-lookup"><span data-stu-id="559d4-116">Format</span></span>| <span data-ttu-id="559d4-117">Description</span><span class="sxs-lookup"><span data-stu-id="559d4-117">Description</span></span>
----|-------|------------
<span data-ttu-id="559d4-118">Ocp-Apim-Subscription-Key</span><span class="sxs-lookup"><span data-stu-id="559d4-118">Ocp-Apim-Subscription-Key</span></span> | <span data-ttu-id="559d4-119">ASCII</span><span class="sxs-lookup"><span data-stu-id="559d4-119">ASCII</span></span> | <span data-ttu-id="559d4-120">YOUR_SUBSCRIPTION_KEY</span><span class="sxs-lookup"><span data-stu-id="559d4-120">YOUR_SUBSCRIPTION_KEY</span></span>

<span data-ttu-id="559d4-121">The following is an example of a request header:</span><span class="sxs-lookup"><span data-stu-id="559d4-121">The following is an example of a request header:</span></span>

```HTTP
POST https://speech.platform.bing.com/speech/recognition/interactive/cognitiveservices/v1?language=en-US&format=detailed HTTP/1.1
Accept: application/json;text/xml
Content-Type: audio/wav; codec=audio/pcm; samplerate=16000
Ocp-Apim-Subscription-Key: YOUR_SUBSCRIPTION_KEY
Host: speech.platform.bing.com
Transfer-Encoding: chunked
Expect: 100-continue
```

> [!IMPORTANT]
> <span data-ttu-id="559d4-122">If you use [client libraries](../GetStarted/GetStartedClientLibraries.md) in your application, verify that you can get the authorization token with your subscription key, as described in the following section.</span><span class="sxs-lookup"><span data-stu-id="559d4-122">If you use [client libraries](../GetStarted/GetStartedClientLibraries.md) in your application, verify that you can get the authorization token with your subscription key, as described in the following section.</span></span> <span data-ttu-id="559d4-123">The client libraries use the subscription key to get an authorization token and then use the token for authentication.</span><span class="sxs-lookup"><span data-stu-id="559d4-123">The client libraries use the subscription key to get an authorization token and then use the token for authentication.</span></span>

## <a name="use-an-authorization-token"></a><span data-ttu-id="559d4-124">Use an authorization token</span><span class="sxs-lookup"><span data-stu-id="559d4-124">Use an authorization token</span></span>

<span data-ttu-id="559d4-125">Alternatively, you can use an authorization token for authentication as proof of authentication/authorization.</span><span class="sxs-lookup"><span data-stu-id="559d4-125">Alternatively, you can use an authorization token for authentication as proof of authentication/authorization.</span></span> <span data-ttu-id="559d4-126">To get this token, you must first obtain a subscription key from the Speech API, as described in the [preceding section](#use-a-subscription-key).</span><span class="sxs-lookup"><span data-stu-id="559d4-126">To get this token, you must first obtain a subscription key from the Speech API, as described in the [preceding section](#use-a-subscription-key).</span></span>

### <a name="get-an-authorization-token"></a><span data-ttu-id="559d4-127">Get an authorization token</span><span class="sxs-lookup"><span data-stu-id="559d4-127">Get an authorization token</span></span>

<span data-ttu-id="559d4-128">After you have a valid subscription key, send a POST request to the token service of Cognitive Services.</span><span class="sxs-lookup"><span data-stu-id="559d4-128">After you have a valid subscription key, send a POST request to the token service of Cognitive Services.</span></span> <span data-ttu-id="559d4-129">In the response, you receive the authorization token as a JSON Web Token (JWT).</span><span class="sxs-lookup"><span data-stu-id="559d4-129">In the response, you receive the authorization token as a JSON Web Token (JWT).</span></span>

> [!NOTE]
> <span data-ttu-id="559d4-130">The token has an expiration of 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="559d4-130">The token has an expiration of 10 minutes.</span></span> <span data-ttu-id="559d4-131">To renew the token, see the following section.</span><span class="sxs-lookup"><span data-stu-id="559d4-131">To renew the token, see the following section.</span></span>

<span data-ttu-id="559d4-132">The token service URI is located here:</span><span class="sxs-lookup"><span data-stu-id="559d4-132">The token service URI is located here:</span></span>

```
https://api.cognitive.microsoft.com/sts/v1.0/issueToken
```

<span data-ttu-id="559d4-133">The following code sample shows how to get an access token.</span><span class="sxs-lookup"><span data-stu-id="559d4-133">The following code sample shows how to get an access token.</span></span> <span data-ttu-id="559d4-134">Replace `YOUR_SUBSCRIPTION_KEY` with your own subscription key:</span><span class="sxs-lookup"><span data-stu-id="559d4-134">Replace `YOUR_SUBSCRIPTION_KEY` with your own subscription key:</span></span>

# <a name="powershelltabpowershell"></a>[<span data-ttu-id="559d4-135">PowerShell</span><span class="sxs-lookup"><span data-stu-id="559d4-135">PowerShell</span></span>](#tab/Powershell)

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

# <a name="curltabcurl"></a>[<span data-ttu-id="559d4-136">curl</span><span class="sxs-lookup"><span data-stu-id="559d4-136">curl</span></span>](#tab/curl)

<span data-ttu-id="559d4-137">The example uses curl on Linux with bash.</span><span class="sxs-lookup"><span data-stu-id="559d4-137">The example uses curl on Linux with bash.</span></span> <span data-ttu-id="559d4-138">If it's not available on your platform, you might need to install curl.</span><span class="sxs-lookup"><span data-stu-id="559d4-138">If it's not available on your platform, you might need to install curl.</span></span> <span data-ttu-id="559d4-139">The example also works on Cygwin on Windows, Git Bash, zsh, and other shells.</span><span class="sxs-lookup"><span data-stu-id="559d4-139">The example also works on Cygwin on Windows, Git Bash, zsh, and other shells.</span></span>

```
curl -v -X POST "https://api.cognitive.microsoft.com/sts/v1.0/issueToken" -H "Content-type: application/x-www-form-urlencoded" -H "Content-Length: 0" -H "Ocp-Apim-Subscription-Key: YOUR_SUBSCRIPTION_KEY"
```

# <a name="ctabcsharp"></a>[<span data-ttu-id="559d4-140">C#</span><span class="sxs-lookup"><span data-stu-id="559d4-140">C#</span></span>](#tab/CSharp)

```cs
    /*
     * This class demonstrates how to get a valid access token.
     */
    public class Authentication
    {
        public static readonly string FetchTokenUri = "https://api.cognitive.microsoft.com/sts/v1.0";
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
                uriBuilder.Path += "/issueToken";

                var result = await client.PostAsync(uriBuilder.Uri.AbsoluteUri, null);
                Console.WriteLine("Token Uri: {0}", uriBuilder.Uri.AbsoluteUri);
                return await result.Content.ReadAsStringAsync();
            }
        }
    }
```

---

<span data-ttu-id="559d4-141">The following is a sample POST request:</span><span class="sxs-lookup"><span data-stu-id="559d4-141">The following is a sample POST request:</span></span>

```HTTP
POST https://api.cognitive.microsoft.com/sts/v1.0/issueToken HTTP/1.1
Ocp-Apim-Subscription-Key: YOUR_SUBSCRIPTION_KEY
Host: api.cognitive.microsoft.com
Content-type: application/x-www-form-urlencoded
Content-Length: 0
Connection: Keep-Alive
```

<span data-ttu-id="559d4-142">If you cannot get an authorization token from the token service, check whether your subscription key is still valid.</span><span class="sxs-lookup"><span data-stu-id="559d4-142">If you cannot get an authorization token from the token service, check whether your subscription key is still valid.</span></span> <span data-ttu-id="559d4-143">If you are using a free trial key, go to the [Cognitive Services subscription](https://azure.microsoft.com/try/cognitive-services/) page, click on "Log in" to login using the account that you used for applying the free trial key, and check whether the subscription key is expired or exceeds the quota.</span><span class="sxs-lookup"><span data-stu-id="559d4-143">If you are using a free trial key, go to the [Cognitive Services subscription](https://azure.microsoft.com/try/cognitive-services/) page, click on "Log in" to login using the account that you used for applying the free trial key, and check whether the subscription key is expired or exceeds the quota.</span></span>

### <a name="use-an-authorization-token-in-a-request"></a><span data-ttu-id="559d4-144">Use an authorization token in a request</span><span class="sxs-lookup"><span data-stu-id="559d4-144">Use an authorization token in a request</span></span>

<span data-ttu-id="559d4-145">Each time you call the Speech API, you need to pass the authorization token in the `Authorization` header.</span><span class="sxs-lookup"><span data-stu-id="559d4-145">Each time you call the Speech API, you need to pass the authorization token in the `Authorization` header.</span></span> <span data-ttu-id="559d4-146">The `Authorization` header must contain a JWT access token.</span><span class="sxs-lookup"><span data-stu-id="559d4-146">The `Authorization` header must contain a JWT access token.</span></span>

<span data-ttu-id="559d4-147">The following example shows how to use an authorization token when you call the Speech REST API.</span><span class="sxs-lookup"><span data-stu-id="559d4-147">The following example shows how to use an authorization token when you call the Speech REST API.</span></span>

> [!NOTE]
> <span data-ttu-id="559d4-148">Replace `YOUR_AUDIO_FILE` with the path to your prerecorded audio file.</span><span class="sxs-lookup"><span data-stu-id="559d4-148">Replace `YOUR_AUDIO_FILE` with the path to your prerecorded audio file.</span></span> <span data-ttu-id="559d4-149">Replace `YOUR_ACCESS_TOKEN` with the authorization token you got in the previous step [Get an authorization token](#get-an-authorization-token).</span><span class="sxs-lookup"><span data-stu-id="559d4-149">Replace `YOUR_ACCESS_TOKEN` with the authorization token you got in the previous step [Get an authorization token](#get-an-authorization-token).</span></span>

# <a name="powershelltabpowershell"></a>[<span data-ttu-id="559d4-150">PowerShell</span><span class="sxs-lookup"><span data-stu-id="559d4-150">PowerShell</span></span>](#tab/Powershell)

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

# <a name="curltabcurl"></a>[<span data-ttu-id="559d4-151">curl</span><span class="sxs-lookup"><span data-stu-id="559d4-151">curl</span></span>](#tab/curl)

```
curl -v -X POST "https://speech.platform.bing.com/speech/recognition/interactive/cognitiveservices/v1?language=en-us&format=detailed" -H "Transfer-Encoding: chunked" -H "Authorization: Bearer YOUR_ACCESS_TOKEN" -H "Content-type: audio/wav; codec=audio/pcm; samplerate=16000" --data-binary @YOUR_AUDIO_FILE
```

# <a name="ctabcsharp"></a>[<span data-ttu-id="559d4-152">C#</span><span class="sxs-lookup"><span data-stu-id="559d4-152">C#</span></span>](#tab/CSharp)

```cs
HttpWebRequest request = null;
request = (HttpWebRequest)HttpWebRequest.Create(requestUri);
request.SendChunked = true;
request.Accept = @"application/json;text/xml";
request.Method = "POST";
request.ProtocolVersion = HttpVersion.Version11;
request.Host = @"speech.platform.bing.com";
request.ContentType = @"audio/wav; codec=audio/pcm; samplerate=16000";
request.Headers["Authorization"] = "Bearer " + token;

// Send an audio file by 1024 byte chunks
using (fs = new FileStream(audioFile, FileMode.Open, FileAccess.Read))
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

### <a name="renew-an-authorization-token"></a><span data-ttu-id="559d4-153">Renew an authorization token</span><span class="sxs-lookup"><span data-stu-id="559d4-153">Renew an authorization token</span></span>

<span data-ttu-id="559d4-154">The authorization token expires after a certain time period (currently 10 minutes).</span><span class="sxs-lookup"><span data-stu-id="559d4-154">The authorization token expires after a certain time period (currently 10 minutes).</span></span> <span data-ttu-id="559d4-155">You need to renew the authorization token before it expires.</span><span class="sxs-lookup"><span data-stu-id="559d4-155">You need to renew the authorization token before it expires.</span></span>

<span data-ttu-id="559d4-156">The following code is an example implementation in C# of how to renew the authorization token:</span><span class="sxs-lookup"><span data-stu-id="559d4-156">The following code is an example implementation in C# of how to renew the authorization token:</span></span>

```cs
    /*
     * This class demonstrates how to get a valid O-auth token.
     */
    public class Authentication
    {
        public static readonly string FetchTokenUri = "https://api.cognitive.microsoft.com/sts/v1.0";
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
                uriBuilder.Path += "/issueToken";

                var result = await client.PostAsync(uriBuilder.Uri.AbsoluteUri, null);
                Console.WriteLine("Token Uri: {0}", uriBuilder.Uri.AbsoluteUri);
                return await result.Content.ReadAsStringAsync();
            }
        }
    }
```
