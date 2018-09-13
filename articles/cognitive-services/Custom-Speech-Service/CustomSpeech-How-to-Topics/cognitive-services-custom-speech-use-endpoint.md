---
title: Use a custom speech endpoint with Custom Speech Service on Azure | Microsoft Docs
description: Learn how to use a custom speech-to-text endpoint with the Custom Speech Service in Cognitive Services.
services: cognitive-services
author: PanosPeriorellis
manager: onano
ms.service: cognitive-services
ms.component: custom-speech
ms.topic: article
ms.date: 02/08/2017
ms.author: panosper
ms.openlocfilehash: d28065d7962ee660cafd4b3321abdd6a8f94abcb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966817"
---
# <a name="use-a-custom-speech-to-text-endpoint"></a><span data-ttu-id="82479-103">Use a custom speech-to-text endpoint</span><span class="sxs-lookup"><span data-stu-id="82479-103">Use a custom speech-to-text endpoint</span></span>
<span data-ttu-id="82479-104">You can send requests to an Azure Custom Speech Service speech-to-text endpoint, in a similar way as you can to the default Cognitive Services speech endpoint.</span><span class="sxs-lookup"><span data-stu-id="82479-104">You can send requests to an Azure Custom Speech Service speech-to-text endpoint, in a similar way as you can to the default Cognitive Services speech endpoint.</span></span> <span data-ttu-id="82479-105">These endpoints are functionally identical to the default endpoints of the Speech API.</span><span class="sxs-lookup"><span data-stu-id="82479-105">These endpoints are functionally identical to the default endpoints of the Speech API.</span></span> <span data-ttu-id="82479-106">Thus, the same functionality that's available via the client library or the REST API for the Speech API is also available for your custom endpoint.</span><span class="sxs-lookup"><span data-stu-id="82479-106">Thus, the same functionality that's available via the client library or the REST API for the Speech API is also available for your custom endpoint.</span></span>

<span data-ttu-id="82479-107">The endpoints you create by using this service can process different numbers of concurrent requests.</span><span class="sxs-lookup"><span data-stu-id="82479-107">The endpoints you create by using this service can process different numbers of concurrent requests.</span></span> <span data-ttu-id="82479-108">The volume depends on the pricing tier associated with your subscription.</span><span class="sxs-lookup"><span data-stu-id="82479-108">The volume depends on the pricing tier associated with your subscription.</span></span> <span data-ttu-id="82479-109">If too many requests are received, an error occurs.</span><span class="sxs-lookup"><span data-stu-id="82479-109">If too many requests are received, an error occurs.</span></span> <span data-ttu-id="82479-110">The free tier has a monthly limit of requests.</span><span class="sxs-lookup"><span data-stu-id="82479-110">The free tier has a monthly limit of requests.</span></span>

<span data-ttu-id="82479-111">The service assumes that data is transmitted in real time.</span><span class="sxs-lookup"><span data-stu-id="82479-111">The service assumes that data is transmitted in real time.</span></span> <span data-ttu-id="82479-112">If it's sent faster, the request is considered running until its audio duration in real time has passed.</span><span class="sxs-lookup"><span data-stu-id="82479-112">If it's sent faster, the request is considered running until its audio duration in real time has passed.</span></span>

> [!NOTE]
> <span data-ttu-id="82479-113">We do support the [new web sockets](https://docs.microsoft.com/azure/cognitive-services/speech/api-reference-rest/websocketprotocol) yet.</span><span class="sxs-lookup"><span data-stu-id="82479-113">We do support the [new web sockets](https://docs.microsoft.com/azure/cognitive-services/speech/api-reference-rest/websocketprotocol) yet.</span></span> <span data-ttu-id="82479-114">If you plan to use web sockets with your custom speech endpoint, follow the instructions here.</span><span class="sxs-lookup"><span data-stu-id="82479-114">If you plan to use web sockets with your custom speech endpoint, follow the instructions here.</span></span>
>
> <span data-ttu-id="82479-115">The new [REST API](https://docs.microsoft.com/azure/cognitive-services/speech/getstarted/getstartedrest) support is coming soon.</span><span class="sxs-lookup"><span data-stu-id="82479-115">The new [REST API](https://docs.microsoft.com/azure/cognitive-services/speech/getstarted/getstartedrest) support is coming soon.</span></span> <span data-ttu-id="82479-116">If you plan to call your custom speech endpoint via HTTP, follow the instructions here.</span><span class="sxs-lookup"><span data-stu-id="82479-116">If you plan to call your custom speech endpoint via HTTP, follow the instructions here.</span></span>
>

## <a name="send-requests-by-using-the-speech-client-library"></a><span data-ttu-id="82479-117">Send requests by using the speech client library</span><span class="sxs-lookup"><span data-stu-id="82479-117">Send requests by using the speech client library</span></span>

<span data-ttu-id="82479-118">To send requests to your custom endpoint by using the speech client library, start the recognition client.</span><span class="sxs-lookup"><span data-stu-id="82479-118">To send requests to your custom endpoint by using the speech client library, start the recognition client.</span></span> <span data-ttu-id="82479-119">Use the Client Speech SDK from [NuGet](http://nuget.org/).</span><span class="sxs-lookup"><span data-stu-id="82479-119">Use the Client Speech SDK from [NuGet](http://nuget.org/).</span></span> <span data-ttu-id="82479-120">Search for *speech recognition*, and select the speech recognition package from Microsoft for your platform.</span><span class="sxs-lookup"><span data-stu-id="82479-120">Search for *speech recognition*, and select the speech recognition package from Microsoft for your platform.</span></span> <span data-ttu-id="82479-121">Some sample code can be found on [GitHub](https://github.com/Microsoft/Cognitive-Speech-STT-Windows).</span><span class="sxs-lookup"><span data-stu-id="82479-121">Some sample code can be found on [GitHub](https://github.com/Microsoft/Cognitive-Speech-STT-Windows).</span></span> <span data-ttu-id="82479-122">The Client Speech SDK provides a factory class **SpeechRecognitionServiceFactory**, which offers the following methods:</span><span class="sxs-lookup"><span data-stu-id="82479-122">The Client Speech SDK provides a factory class **SpeechRecognitionServiceFactory**, which offers the following methods:</span></span>

  *   <span data-ttu-id="82479-123">```CreateDataClient(...)```: A data recognition client.</span><span class="sxs-lookup"><span data-stu-id="82479-123">```CreateDataClient(...)```: A data recognition client.</span></span>
  *   <span data-ttu-id="82479-124">```CreateDataClientWithIntent(...)```: A data recognition client with intent.</span><span class="sxs-lookup"><span data-stu-id="82479-124">```CreateDataClientWithIntent(...)```: A data recognition client with intent.</span></span>
  *   <span data-ttu-id="82479-125">```CreateMicrophoneClient(...)```: A microphone recognition client.</span><span class="sxs-lookup"><span data-stu-id="82479-125">```CreateMicrophoneClient(...)```: A microphone recognition client.</span></span>
  *   <span data-ttu-id="82479-126">```CreateMicrophoneClientWithIntent(...)```: A microphone recognition client with intent.</span><span class="sxs-lookup"><span data-stu-id="82479-126">```CreateMicrophoneClientWithIntent(...)```: A microphone recognition client with intent.</span></span>

<span data-ttu-id="82479-127">For detailed documentation, see the [Bing Speech API](https://docs.microsoft.com/azure/cognitive-services/speech/home).</span><span class="sxs-lookup"><span data-stu-id="82479-127">For detailed documentation, see the [Bing Speech API](https://docs.microsoft.com/azure/cognitive-services/speech/home).</span></span> <span data-ttu-id="82479-128">The Custom Speech Service endpoints support the same SDK.</span><span class="sxs-lookup"><span data-stu-id="82479-128">The Custom Speech Service endpoints support the same SDK.</span></span>

<span data-ttu-id="82479-129">The data recognition client is appropriate for speech recognition from data, such as a file or other audio source.</span><span class="sxs-lookup"><span data-stu-id="82479-129">The data recognition client is appropriate for speech recognition from data, such as a file or other audio source.</span></span> <span data-ttu-id="82479-130">The microphone recognition client is appropriate for speech recognition from the microphone.</span><span class="sxs-lookup"><span data-stu-id="82479-130">The microphone recognition client is appropriate for speech recognition from the microphone.</span></span> <span data-ttu-id="82479-131">The use of intent in either client can return structured intent results from the [Language Understanding Intelligent Service](https://www.luis.ai/) (LUIS), if you've built a LUIS application for your scenario.</span><span class="sxs-lookup"><span data-stu-id="82479-131">The use of intent in either client can return structured intent results from the [Language Understanding Intelligent Service](https://www.luis.ai/) (LUIS), if you've built a LUIS application for your scenario.</span></span>

<span data-ttu-id="82479-132">All four types of clients can be instantiated in two ways.</span><span class="sxs-lookup"><span data-stu-id="82479-132">All four types of clients can be instantiated in two ways.</span></span> <span data-ttu-id="82479-133">The first way uses the standard Cognitive Services Speech API.</span><span class="sxs-lookup"><span data-stu-id="82479-133">The first way uses the standard Cognitive Services Speech API.</span></span> <span data-ttu-id="82479-134">The second way allows you to specify a URL that corresponds to your custom endpoint created with the Custom Speech Service.</span><span class="sxs-lookup"><span data-stu-id="82479-134">The second way allows you to specify a URL that corresponds to your custom endpoint created with the Custom Speech Service.</span></span>

<span data-ttu-id="82479-135">For example, you can create a **DataRecognitionClient** that sends requests to a custom endpoint by using the following method:</span><span class="sxs-lookup"><span data-stu-id="82479-135">For example, you can create a **DataRecognitionClient** that sends requests to a custom endpoint by using the following method:</span></span>

```csharp
public static DataRecognitionClient CreateDataClient(SpeeechRecognitionMode speechRecognitionMode, string language, string primaryOrSecondaryKey, **string url**);
```

<span data-ttu-id="82479-136">The **your_subscriptionId** and **endpointURL** refer to the subscription key and the web sockets URL, respectively, on the **Deployment Information** page.</span><span class="sxs-lookup"><span data-stu-id="82479-136">The **your_subscriptionId** and **endpointURL** refer to the subscription key and the web sockets URL, respectively, on the **Deployment Information** page.</span></span>

<span data-ttu-id="82479-137">The **AuthenticationUri** is used to receive a token from the authentication service.</span><span class="sxs-lookup"><span data-stu-id="82479-137">The **AuthenticationUri** is used to receive a token from the authentication service.</span></span> <span data-ttu-id="82479-138">This URI must be set separately, as shown in the following sample code.</span><span class="sxs-lookup"><span data-stu-id="82479-138">This URI must be set separately, as shown in the following sample code.</span></span>

<span data-ttu-id="82479-139">This sample code shows how to use the client SDK:</span><span class="sxs-lookup"><span data-stu-id="82479-139">This sample code shows how to use the client SDK:</span></span>

```csharp
var dataClient = SpeechRecognitionServiceFactory.CreateDataClient(
  SpeechRecognitionMode.LongDictation,
  "en-us",
  "your_subscriptionId",
  "your_subscriptionId",
  "endpointURL");
// set the authorization Uri
dataClient.AuthenticationUri = "https://westus.api.cognitive.microsoft.com/sts/v1.0/issueToken";
```

> [!NOTE]
> <span data-ttu-id="82479-140">When you use **Create** methods in the SDK, you must provide the subscription ID twice because of overloading of the **Create** methods.</span><span class="sxs-lookup"><span data-stu-id="82479-140">When you use **Create** methods in the SDK, you must provide the subscription ID twice because of overloading of the **Create** methods.</span></span>
>

<span data-ttu-id="82479-141">The Custom Speech Service uses two different URLs for short-form and long-form recognition.</span><span class="sxs-lookup"><span data-stu-id="82479-141">The Custom Speech Service uses two different URLs for short-form and long-form recognition.</span></span> <span data-ttu-id="82479-142">Both are listed on the **Deployments** page.</span><span class="sxs-lookup"><span data-stu-id="82479-142">Both are listed on the **Deployments** page.</span></span> <span data-ttu-id="82479-143">Use the correct endpoint URL for the specific form you want to use.</span><span class="sxs-lookup"><span data-stu-id="82479-143">Use the correct endpoint URL for the specific form you want to use.</span></span>

<span data-ttu-id="82479-144">For more information about invoking the various recognition clients with your custom endpoint, see the [SpeechRecognitionServiceFactory](https://www.microsoft.com/cognitive-services/Speech-api/documentation/GetStarted/GetStartedCSharpDesktop) class.</span><span class="sxs-lookup"><span data-stu-id="82479-144">For more information about invoking the various recognition clients with your custom endpoint, see the [SpeechRecognitionServiceFactory](https://www.microsoft.com/cognitive-services/Speech-api/documentation/GetStarted/GetStartedCSharpDesktop) class.</span></span> <span data-ttu-id="82479-145">The documentation on this page refers to acoustic model adaptation, but it applies to all endpoints created by using the Custom Speech Service.</span><span class="sxs-lookup"><span data-stu-id="82479-145">The documentation on this page refers to acoustic model adaptation, but it applies to all endpoints created by using the Custom Speech Service.</span></span>

## <a name="send-requests-by-using-the-speech-protocol"></a><span data-ttu-id="82479-146">Send requests by using the Speech Protocol</span><span class="sxs-lookup"><span data-stu-id="82479-146">Send requests by using the Speech Protocol</span></span>

<span data-ttu-id="82479-147">The endpoints shown for the [Speech Protocol](https://docs.microsoft.com/azure/cognitive-services/speech/api-reference-rest/websocketprotocol) are endpoints for the Open Source Web Socket Speech Protocol.</span><span class="sxs-lookup"><span data-stu-id="82479-147">The endpoints shown for the [Speech Protocol](https://docs.microsoft.com/azure/cognitive-services/speech/api-reference-rest/websocketprotocol) are endpoints for the Open Source Web Socket Speech Protocol.</span></span>

<span data-ttu-id="82479-148">Currently, the only official client implementation is for [JavaScript](https://github.com/Azure-Samples/SpeechToText-WebSockets-Javascript).</span><span class="sxs-lookup"><span data-stu-id="82479-148">Currently, the only official client implementation is for [JavaScript](https://github.com/Azure-Samples/SpeechToText-WebSockets-Javascript).</span></span> <span data-ttu-id="82479-149">If you want to start with the sample provided there, make the following changes to the code and build the sample again:</span><span class="sxs-lookup"><span data-stu-id="82479-149">If you want to start with the sample provided there, make the following changes to the code and build the sample again:</span></span>

1. <span data-ttu-id="82479-150">In _src\sdk\speech.browser\SpeechConnectionFactory.ts_, replace the host name "wss://speech.platform.bing.com" with the host name shown on the details page of your deployment.</span><span class="sxs-lookup"><span data-stu-id="82479-150">In _src\sdk\speech.browser\SpeechConnectionFactory.ts_, replace the host name "wss://speech.platform.bing.com" with the host name shown on the details page of your deployment.</span></span> <span data-ttu-id="82479-151">Do not insert the full URI here but just the *wss* protocol scheme and the host name.</span><span class="sxs-lookup"><span data-stu-id="82479-151">Do not insert the full URI here but just the *wss* protocol scheme and the host name.</span></span> <span data-ttu-id="82479-152">For example:</span><span class="sxs-lookup"><span data-stu-id="82479-152">For example:</span></span>

    ```JavaScript
    private get Host(): string {
        return Storage.Local.GetOrAdd("Host", "wss://<your_key_goes_here>.api.cris.ai");
    }
    ```

2. <span data-ttu-id="82479-153">Set the _recognitionMode_ parameter in _samples\browser\Samples.html_ according to your requirements:</span><span class="sxs-lookup"><span data-stu-id="82479-153">Set the _recognitionMode_ parameter in _samples\browser\Samples.html_ according to your requirements:</span></span>
    * <span data-ttu-id="82479-154">_RecognitionMode.Interactive_ supports requests up to 15 seconds.</span><span class="sxs-lookup"><span data-stu-id="82479-154">_RecognitionMode.Interactive_ supports requests up to 15 seconds.</span></span>
    * <span data-ttu-id="82479-155">_RecognitionMode.Conversation_ and _RecognitionMode.Dictation_ (both are equivalent in Custom Speech Service) support requests up to 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="82479-155">_RecognitionMode.Conversation_ and _RecognitionMode.Dictation_ (both are equivalent in Custom Speech Service) support requests up to 10 minutes.</span></span>

3. <span data-ttu-id="82479-156">Build the sample by using "gulp build" before you use it.</span><span class="sxs-lookup"><span data-stu-id="82479-156">Build the sample by using "gulp build" before you use it.</span></span>

> [!NOTE]
> <span data-ttu-id="82479-157">Ensure that you use the correct URI for this protocol.</span><span class="sxs-lookup"><span data-stu-id="82479-157">Ensure that you use the correct URI for this protocol.</span></span> <span data-ttu-id="82479-158">The required scheme is *wss* (not *http* as in the client protocol).</span><span class="sxs-lookup"><span data-stu-id="82479-158">The required scheme is *wss* (not *http* as in the client protocol).</span></span> 

<span data-ttu-id="82479-159">For more information, see the [Bing Speech API](https://docs.microsoft.com/azure/cognitive-services/speech/getstarted/getstartedclientlibraries) documentation.</span><span class="sxs-lookup"><span data-stu-id="82479-159">For more information, see the [Bing Speech API](https://docs.microsoft.com/azure/cognitive-services/speech/getstarted/getstartedclientlibraries) documentation.</span></span>

## <a name="send-requests-by-using-http"></a><span data-ttu-id="82479-160">Send requests by using HTTP</span><span class="sxs-lookup"><span data-stu-id="82479-160">Send requests by using HTTP</span></span>

<span data-ttu-id="82479-161">Sending a request to your custom endpoint by using an HTTP post is similar to sending a request by HTTP to the Cognitive Services Bing Speech API.</span><span class="sxs-lookup"><span data-stu-id="82479-161">Sending a request to your custom endpoint by using an HTTP post is similar to sending a request by HTTP to the Cognitive Services Bing Speech API.</span></span> <span data-ttu-id="82479-162">Modify the URL to reflect the address of your custom deployment.</span><span class="sxs-lookup"><span data-stu-id="82479-162">Modify the URL to reflect the address of your custom deployment.</span></span>

<span data-ttu-id="82479-163">There are some restrictions on requests sent via HTTP for both the Cognitive Services Speech endpoint and the custom endpoints created with this service.</span><span class="sxs-lookup"><span data-stu-id="82479-163">There are some restrictions on requests sent via HTTP for both the Cognitive Services Speech endpoint and the custom endpoints created with this service.</span></span> <span data-ttu-id="82479-164">The HTTP request can't return partial results during the recognition process.</span><span class="sxs-lookup"><span data-stu-id="82479-164">The HTTP request can't return partial results during the recognition process.</span></span> <span data-ttu-id="82479-165">Additionally, the duration of the requests is limited to 10 seconds for the audio content, and 14 seconds overall.</span><span class="sxs-lookup"><span data-stu-id="82479-165">Additionally, the duration of the requests is limited to 10 seconds for the audio content, and 14 seconds overall.</span></span>

<span data-ttu-id="82479-166">To create a post request, follow the same process you use for the Cognitive Services Speech API.</span><span class="sxs-lookup"><span data-stu-id="82479-166">To create a post request, follow the same process you use for the Cognitive Services Speech API.</span></span>

1. <span data-ttu-id="82479-167">Obtain an access token by using your subscription ID.</span><span class="sxs-lookup"><span data-stu-id="82479-167">Obtain an access token by using your subscription ID.</span></span> <span data-ttu-id="82479-168">This token is required to access the recognition endpoint.</span><span class="sxs-lookup"><span data-stu-id="82479-168">This token is required to access the recognition endpoint.</span></span> <span data-ttu-id="82479-169">It can be reused for 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="82479-169">It can be reused for 10 minutes.</span></span>

    ```
    curl -X POST --header "Ocp-Apim-Subscription-Key:<subscriptionId>" --data "" "https://westus.api.cognitive.microsoft.com/sts/v1.0/issueToken"
    ```
      <span data-ttu-id="82479-170">The **subscriptionId** should be set to the subscription ID you use for this deployment.</span><span class="sxs-lookup"><span data-stu-id="82479-170">The **subscriptionId** should be set to the subscription ID you use for this deployment.</span></span> <span data-ttu-id="82479-171">The response is the plain token you need for the next request.</span><span class="sxs-lookup"><span data-stu-id="82479-171">The response is the plain token you need for the next request.</span></span>

2. <span data-ttu-id="82479-172">Post audio to the endpoint by using POST again.</span><span class="sxs-lookup"><span data-stu-id="82479-172">Post audio to the endpoint by using POST again.</span></span>

    ```
    curl -X POST --data-binary @example.wav -H "Authorization: Bearer <token>" -H "Content-Type: application/octet-stream" "<https_endpoint>"
    ```

    <span data-ttu-id="82479-173">The **token** is the access token you received with the previous call.</span><span class="sxs-lookup"><span data-stu-id="82479-173">The **token** is the access token you received with the previous call.</span></span> <span data-ttu-id="82479-174">The **https_endpoint** is the full address of your custom speech-to-text endpoint, shown on the **Deployment Information** page.</span><span class="sxs-lookup"><span data-stu-id="82479-174">The **https_endpoint** is the full address of your custom speech-to-text endpoint, shown on the **Deployment Information** page.</span></span>

<span data-ttu-id="82479-175">For more information about HTTP post parameters and the response format, see the [Microsoft Cognitive Services Bing Speech HTTP API](https://www.microsoft.com/cognitive-services/speech-api/documentation/API-Reference-REST/BingVoiceRecognition#SampleImplementation).</span><span class="sxs-lookup"><span data-stu-id="82479-175">For more information about HTTP post parameters and the response format, see the [Microsoft Cognitive Services Bing Speech HTTP API](https://www.microsoft.com/cognitive-services/speech-api/documentation/API-Reference-REST/BingVoiceRecognition#SampleImplementation).</span></span>

## <a name="send-requests-by-using-the-service-library"></a><span data-ttu-id="82479-176">Send requests by using the Service Library</span><span class="sxs-lookup"><span data-stu-id="82479-176">Send requests by using the Service Library</span></span>
<span data-ttu-id="82479-177">The Service Library enables your service to make use of the Microsoft Speech transcription cloud to convert spoken language to text in real-time, so that your client app can send audio and receive partial recognition results back simultaneously and asynchronously.</span><span class="sxs-lookup"><span data-stu-id="82479-177">The Service Library enables your service to make use of the Microsoft Speech transcription cloud to convert spoken language to text in real-time, so that your client app can send audio and receive partial recognition results back simultaneously and asynchronously.</span></span> <span data-ttu-id="82479-178">Detail of the Service SDK can be found [here](https://docs.microsoft.com/azure/cognitive-services/speech/getstarted/getstartedcsharpservicelibrary)</span><span class="sxs-lookup"><span data-stu-id="82479-178">Detail of the Service SDK can be found [here](https://docs.microsoft.com/azure/cognitive-services/speech/getstarted/getstartedcsharpservicelibrary)</span></span>

> [!NOTE]
> <span data-ttu-id="82479-179">When using the Service Library you have to change the URI of the authorization provider in the implementation of **IAuthorizationProvider** to https://westus.api.cognitive.microsoft.com/sts/v1.0/issueToken.</span><span class="sxs-lookup"><span data-stu-id="82479-179">When using the Service Library you have to change the URI of the authorization provider in the implementation of **IAuthorizationProvider** to https://westus.api.cognitive.microsoft.com/sts/v1.0/issueToken.</span></span>

## <a name="next-steps"></a><span data-ttu-id="82479-180">Next steps</span><span class="sxs-lookup"><span data-stu-id="82479-180">Next steps</span></span>
* <span data-ttu-id="82479-181">Improve accuracy with your [custom acoustic model](cognitive-services-custom-speech-create-acoustic-model.md).</span><span class="sxs-lookup"><span data-stu-id="82479-181">Improve accuracy with your [custom acoustic model](cognitive-services-custom-speech-create-acoustic-model.md).</span></span>
* <span data-ttu-id="82479-182">Improve accuracy with a [custom language model](cognitive-services-custom-speech-create-language-model.md).</span><span class="sxs-lookup"><span data-stu-id="82479-182">Improve accuracy with a [custom language model](cognitive-services-custom-speech-create-language-model.md).</span></span>
