---
title: Get started with the Microsoft Speech Recognition API by using the C# service library | Microsoft Docs
description: Use the Microsoft speech recognition service library to convert spoken language to text.
services: cognitive-services
author: zhouwangzw
manager: wolfma
ms.service: cognitive-services
ms.component: bing-speech
ms.topic: article
ms.date: 09/17/2017
ms.author: zhouwang
ms.openlocfilehash: 0320f41658a7ac4d6bf9e88ed998c853b665d485
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44783541"
---
# <a name="get-started-with-the-speech-recognition-service-library-in-c35-for-net-windows"></a><span data-ttu-id="a78ef-103">Get started with the speech recognition service library in C&#35; for .NET Windows</span><span class="sxs-lookup"><span data-stu-id="a78ef-103">Get started with the speech recognition service library in C&#35; for .NET Windows</span></span>

<span data-ttu-id="a78ef-104">The service library is for developers who have their own cloud service and want to call Speech Service from their service.</span><span class="sxs-lookup"><span data-stu-id="a78ef-104">The service library is for developers who have their own cloud service and want to call Speech Service from their service.</span></span> <span data-ttu-id="a78ef-105">If you want to call the speech recognition service from device-bound apps, do not use this SDK.</span><span class="sxs-lookup"><span data-stu-id="a78ef-105">If you want to call the speech recognition service from device-bound apps, do not use this SDK.</span></span> <span data-ttu-id="a78ef-106">(Use other client libraries or REST APIs for that.)</span><span class="sxs-lookup"><span data-stu-id="a78ef-106">(Use other client libraries or REST APIs for that.)</span></span>

<span data-ttu-id="a78ef-107">To use the C# service library, install the [NuGet package Microsoft.Bing.Speech](https://www.nuget.org/packages/Microsoft.Bing.Speech/).</span><span class="sxs-lookup"><span data-stu-id="a78ef-107">To use the C# service library, install the [NuGet package Microsoft.Bing.Speech](https://www.nuget.org/packages/Microsoft.Bing.Speech/).</span></span> <span data-ttu-id="a78ef-108">For the library API reference, see the [Microsoft Speech C# service library](https://cdn.rawgit.com/Microsoft/Cognitive-Speech-STT-ServiceLibrary/master/docs/index.html).</span><span class="sxs-lookup"><span data-stu-id="a78ef-108">For the library API reference, see the [Microsoft Speech C# service library](https://cdn.rawgit.com/Microsoft/Cognitive-Speech-STT-ServiceLibrary/master/docs/index.html).</span></span>

<span data-ttu-id="a78ef-109">The following sections describe how to install, build, and run the C# sample application by using the C# service library.</span><span class="sxs-lookup"><span data-stu-id="a78ef-109">The following sections describe how to install, build, and run the C# sample application by using the C# service library.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a78ef-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a78ef-110">Prerequisites</span></span>

### <a name="platform-requirements"></a><span data-ttu-id="a78ef-111">Platform requirements</span><span class="sxs-lookup"><span data-stu-id="a78ef-111">Platform requirements</span></span>

<span data-ttu-id="a78ef-112">The following example was developed for Windows 8+ and .NET 4.5+ Framework by using [Visual Studio 2015, Community Edition](https://www.visualstudio.com/products/visual-studio-community-vs).</span><span class="sxs-lookup"><span data-stu-id="a78ef-112">The following example was developed for Windows 8+ and .NET 4.5+ Framework by using [Visual Studio 2015, Community Edition](https://www.visualstudio.com/products/visual-studio-community-vs).</span></span>

### <a name="get-the-sample-application"></a><span data-ttu-id="a78ef-113">Get the sample application</span><span class="sxs-lookup"><span data-stu-id="a78ef-113">Get the sample application</span></span>

<span data-ttu-id="a78ef-114">Clone the sample from the [Speech C# service library sample](https://github.com/Microsoft/Cognitive-Speech-STT-ServiceLibrary) repository.</span><span class="sxs-lookup"><span data-stu-id="a78ef-114">Clone the sample from the [Speech C# service library sample](https://github.com/Microsoft/Cognitive-Speech-STT-ServiceLibrary) repository.</span></span>

### <a name="subscribe-to-the-speech-recognition-api-and-get-a-free-trial-subscription-key"></a><span data-ttu-id="a78ef-115">Subscribe to the Speech Recognition API, and get a free trial subscription key</span><span class="sxs-lookup"><span data-stu-id="a78ef-115">Subscribe to the Speech Recognition API, and get a free trial subscription key</span></span>

<span data-ttu-id="a78ef-116">The Speech API is part of Cognitive Services (previously Project Oxford).</span><span class="sxs-lookup"><span data-stu-id="a78ef-116">The Speech API is part of Cognitive Services (previously Project Oxford).</span></span> <span data-ttu-id="a78ef-117">You can get free trial subscription keys from the [Cognitive Services subscription](https://azure.microsoft.com/try/cognitive-services/) page.</span><span class="sxs-lookup"><span data-stu-id="a78ef-117">You can get free trial subscription keys from the [Cognitive Services subscription](https://azure.microsoft.com/try/cognitive-services/) page.</span></span> <span data-ttu-id="a78ef-118">After you select the Speech API, select **Get API Key** to get the key.</span><span class="sxs-lookup"><span data-stu-id="a78ef-118">After you select the Speech API, select **Get API Key** to get the key.</span></span> <span data-ttu-id="a78ef-119">It returns a primary and secondary key.</span><span class="sxs-lookup"><span data-stu-id="a78ef-119">It returns a primary and secondary key.</span></span> <span data-ttu-id="a78ef-120">Both keys are tied to the same quota, so you can use either key.</span><span class="sxs-lookup"><span data-stu-id="a78ef-120">Both keys are tied to the same quota, so you can use either key.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="a78ef-121">Get a subscription key.</span><span class="sxs-lookup"><span data-stu-id="a78ef-121">Get a subscription key.</span></span> <span data-ttu-id="a78ef-122">Before you can use the Speech client libraries, you must have a [subscription key](https://azure.microsoft.com/try/cognitive-services/).</span><span class="sxs-lookup"><span data-stu-id="a78ef-122">Before you can use the Speech client libraries, you must have a [subscription key](https://azure.microsoft.com/try/cognitive-services/).</span></span>
>
> * <span data-ttu-id="a78ef-123">Use your subscription key.</span><span class="sxs-lookup"><span data-stu-id="a78ef-123">Use your subscription key.</span></span> <span data-ttu-id="a78ef-124">With the provided C# service library sample application, you need to provide your subscription key as one of the command-line parameters.</span><span class="sxs-lookup"><span data-stu-id="a78ef-124">With the provided C# service library sample application, you need to provide your subscription key as one of the command-line parameters.</span></span> <span data-ttu-id="a78ef-125">For more information, see [Run the sample application](#step-3-run-the-sample-application).</span><span class="sxs-lookup"><span data-stu-id="a78ef-125">For more information, see [Run the sample application](#step-3-run-the-sample-application).</span></span>

## <a name="step-1-install-the-sample-application"></a><span data-ttu-id="a78ef-126">Step 1: Install the sample application</span><span class="sxs-lookup"><span data-stu-id="a78ef-126">Step 1: Install the sample application</span></span>

1. <span data-ttu-id="a78ef-127">Start Visual Studio 2015, and select **File** > **Open** > **Project/Solution**.</span><span class="sxs-lookup"><span data-stu-id="a78ef-127">Start Visual Studio 2015, and select **File** > **Open** > **Project/Solution**.</span></span>

2. <span data-ttu-id="a78ef-128">Double-click to open the Visual Studio 2015 Solution (.sln) file named SpeechClient.sln.</span><span class="sxs-lookup"><span data-stu-id="a78ef-128">Double-click to open the Visual Studio 2015 Solution (.sln) file named SpeechClient.sln.</span></span> <span data-ttu-id="a78ef-129">The solution opens in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a78ef-129">The solution opens in Visual Studio.</span></span>

## <a name="step-2-build-the-sample-application"></a><span data-ttu-id="a78ef-130">Step 2: Build the sample application</span><span class="sxs-lookup"><span data-stu-id="a78ef-130">Step 2: Build the sample application</span></span>

<span data-ttu-id="a78ef-131">Press Ctrl+Shift+B, or select **Build** on the ribbon menu.</span><span class="sxs-lookup"><span data-stu-id="a78ef-131">Press Ctrl+Shift+B, or select **Build** on the ribbon menu.</span></span> <span data-ttu-id="a78ef-132">Then select **Build Solution**.</span><span class="sxs-lookup"><span data-stu-id="a78ef-132">Then select **Build Solution**.</span></span>

## <a name="step-3-run-the-sample-application"></a><span data-ttu-id="a78ef-133">Step 3: Run the sample application</span><span class="sxs-lookup"><span data-stu-id="a78ef-133">Step 3: Run the sample application</span></span>

1. <span data-ttu-id="a78ef-134">After the build is finished, press F5 or select **Start** on the ribbon menu to run the example.</span><span class="sxs-lookup"><span data-stu-id="a78ef-134">After the build is finished, press F5 or select **Start** on the ribbon menu to run the example.</span></span>

2. <span data-ttu-id="a78ef-135">Open the output directory for the sample, for example, SpeechClientSample\bin\Debug.</span><span class="sxs-lookup"><span data-stu-id="a78ef-135">Open the output directory for the sample, for example, SpeechClientSample\bin\Debug.</span></span> <span data-ttu-id="a78ef-136">Press Shift+Right-click, and select **Open command window here**.</span><span class="sxs-lookup"><span data-stu-id="a78ef-136">Press Shift+Right-click, and select **Open command window here**.</span></span>

3. <span data-ttu-id="a78ef-137">Run `SpeechClientSample.exe` with the following arguments:</span><span class="sxs-lookup"><span data-stu-id="a78ef-137">Run `SpeechClientSample.exe` with the following arguments:</span></span>

   * <span data-ttu-id="a78ef-138">Arg[0]: Specify an input audio WAV file.</span><span class="sxs-lookup"><span data-stu-id="a78ef-138">Arg[0]: Specify an input audio WAV file.</span></span>
   * <span data-ttu-id="a78ef-139">Arg[1]: Specify the audio locale.</span><span class="sxs-lookup"><span data-stu-id="a78ef-139">Arg[1]: Specify the audio locale.</span></span>
   * <span data-ttu-id="a78ef-140">Arg[2]: Specify the recognition modes: *Short* for the `ShortPhrase` mode and *Long* for the `LongDictation` mode.</span><span class="sxs-lookup"><span data-stu-id="a78ef-140">Arg[2]: Specify the recognition modes: *Short* for the `ShortPhrase` mode and *Long* for the `LongDictation` mode.</span></span>
   * <span data-ttu-id="a78ef-141">Arg[3]: Specify the subscription key to access the speech recognition service.</span><span class="sxs-lookup"><span data-stu-id="a78ef-141">Arg[3]: Specify the subscription key to access the speech recognition service.</span></span>

## <a name="samples-explained"></a><span data-ttu-id="a78ef-142">Samples explained</span><span class="sxs-lookup"><span data-stu-id="a78ef-142">Samples explained</span></span>

### <a name="recognition-modes"></a><span data-ttu-id="a78ef-143">Recognition modes</span><span class="sxs-lookup"><span data-stu-id="a78ef-143">Recognition modes</span></span>

* <span data-ttu-id="a78ef-144">`ShortPhrase` mode: An utterance up to 15 seconds long.</span><span class="sxs-lookup"><span data-stu-id="a78ef-144">`ShortPhrase` mode: An utterance up to 15 seconds long.</span></span> <span data-ttu-id="a78ef-145">As data is sent to the server, the client receives multiple partial results and one final best result.</span><span class="sxs-lookup"><span data-stu-id="a78ef-145">As data is sent to the server, the client receives multiple partial results and one final best result.</span></span>
* <span data-ttu-id="a78ef-146">`LongDictation` mode: An utterance up to 10 minutes long.</span><span class="sxs-lookup"><span data-stu-id="a78ef-146">`LongDictation` mode: An utterance up to 10 minutes long.</span></span> <span data-ttu-id="a78ef-147">As data is sent to the server, the client receives multiple partial results and multiple final results, based on where the server indicates sentence pauses.</span><span class="sxs-lookup"><span data-stu-id="a78ef-147">As data is sent to the server, the client receives multiple partial results and multiple final results, based on where the server indicates sentence pauses.</span></span>

### <a name="supported-audio-formats"></a><span data-ttu-id="a78ef-148">Supported audio formats</span><span class="sxs-lookup"><span data-stu-id="a78ef-148">Supported audio formats</span></span>

<span data-ttu-id="a78ef-149">The Speech API supports audio/WAV by using the following codecs:</span><span class="sxs-lookup"><span data-stu-id="a78ef-149">The Speech API supports audio/WAV by using the following codecs:</span></span>

* <span data-ttu-id="a78ef-150">PCM single channel</span><span class="sxs-lookup"><span data-stu-id="a78ef-150">PCM single channel</span></span>
* <span data-ttu-id="a78ef-151">Siren</span><span class="sxs-lookup"><span data-stu-id="a78ef-151">Siren</span></span>
* <span data-ttu-id="a78ef-152">SirenSR</span><span class="sxs-lookup"><span data-stu-id="a78ef-152">SirenSR</span></span>

### <a name="preferences"></a><span data-ttu-id="a78ef-153">Preferences</span><span class="sxs-lookup"><span data-stu-id="a78ef-153">Preferences</span></span>

<span data-ttu-id="a78ef-154">To create a SpeechClient, you need to first create a Preferences object.</span><span class="sxs-lookup"><span data-stu-id="a78ef-154">To create a SpeechClient, you need to first create a Preferences object.</span></span> <span data-ttu-id="a78ef-155">The Preferences object is a set of parameters that configures the behavior of the speech service.</span><span class="sxs-lookup"><span data-stu-id="a78ef-155">The Preferences object is a set of parameters that configures the behavior of the speech service.</span></span> <span data-ttu-id="a78ef-156">It consists of the following fields:</span><span class="sxs-lookup"><span data-stu-id="a78ef-156">It consists of the following fields:</span></span>

* <span data-ttu-id="a78ef-157">`SpeechLanguage`: The locale of the audio sent to the speech service.</span><span class="sxs-lookup"><span data-stu-id="a78ef-157">`SpeechLanguage`: The locale of the audio sent to the speech service.</span></span>
* <span data-ttu-id="a78ef-158">`ServiceUri`: The endpoint used to call the speech service.</span><span class="sxs-lookup"><span data-stu-id="a78ef-158">`ServiceUri`: The endpoint used to call the speech service.</span></span>
* <span data-ttu-id="a78ef-159">`AuthorizationProvider`: An IAuthorizationProvider implementation used to fetch tokens in order to access the speech service.</span><span class="sxs-lookup"><span data-stu-id="a78ef-159">`AuthorizationProvider`: An IAuthorizationProvider implementation used to fetch tokens in order to access the speech service.</span></span> <span data-ttu-id="a78ef-160">Although the sample provides a Cognitive Services authorization provider, we highly recommend that you create your own implementation to handle token caching.</span><span class="sxs-lookup"><span data-stu-id="a78ef-160">Although the sample provides a Cognitive Services authorization provider, we highly recommend that you create your own implementation to handle token caching.</span></span>
* <span data-ttu-id="a78ef-161">`EnableAudioBuffering`: An advanced option.</span><span class="sxs-lookup"><span data-stu-id="a78ef-161">`EnableAudioBuffering`: An advanced option.</span></span> <span data-ttu-id="a78ef-162">See [Connection management](#connection-management).</span><span class="sxs-lookup"><span data-stu-id="a78ef-162">See [Connection management](#connection-management).</span></span>

### <a name="speech-input"></a><span data-ttu-id="a78ef-163">Speech input</span><span class="sxs-lookup"><span data-stu-id="a78ef-163">Speech input</span></span>

<span data-ttu-id="a78ef-164">The SpeechInput object consists of two fields:</span><span class="sxs-lookup"><span data-stu-id="a78ef-164">The SpeechInput object consists of two fields:</span></span>

* <span data-ttu-id="a78ef-165">**Audio**: A stream implementation of your choice from which the SDK pulls audio.</span><span class="sxs-lookup"><span data-stu-id="a78ef-165">**Audio**: A stream implementation of your choice from which the SDK pulls audio.</span></span> <span data-ttu-id="a78ef-166">It can be any [stream](https://msdn.microsoft.com/library/system.io.stream(v=vs.110).aspx) that supports reading.</span><span class="sxs-lookup"><span data-stu-id="a78ef-166">It can be any [stream](https://msdn.microsoft.com/library/system.io.stream(v=vs.110).aspx) that supports reading.</span></span>
   > [!NOTE]
   > <span data-ttu-id="a78ef-167">The SDK detects the end of the stream when the stream returns **0** in read.</span><span class="sxs-lookup"><span data-stu-id="a78ef-167">The SDK detects the end of the stream when the stream returns **0** in read.</span></span>

* <span data-ttu-id="a78ef-168">**RequestMetadata**: Metadata about the speech request.</span><span class="sxs-lookup"><span data-stu-id="a78ef-168">**RequestMetadata**: Metadata about the speech request.</span></span> <span data-ttu-id="a78ef-169">For more information, see the [reference](https://cdn.rawgit.com/Microsoft/Cognitive-Speech-STT-ServiceLibrary/master/docs/index.html).</span><span class="sxs-lookup"><span data-stu-id="a78ef-169">For more information, see the [reference](https://cdn.rawgit.com/Microsoft/Cognitive-Speech-STT-ServiceLibrary/master/docs/index.html).</span></span>

### <a name="speech-request"></a><span data-ttu-id="a78ef-170">Speech request</span><span class="sxs-lookup"><span data-stu-id="a78ef-170">Speech request</span></span>

<span data-ttu-id="a78ef-171">After you have instantiated a SpeechClient and SpeechInput objects, use RecognizeAsync to make a request to Speech Service.</span><span class="sxs-lookup"><span data-stu-id="a78ef-171">After you have instantiated a SpeechClient and SpeechInput objects, use RecognizeAsync to make a request to Speech Service.</span></span>

```cs
    var task = speechClient.RecognizeAsync(speechInput);
```

<span data-ttu-id="a78ef-172">After the request finishes, the task returned by RecognizeAsync finishes.</span><span class="sxs-lookup"><span data-stu-id="a78ef-172">After the request finishes, the task returned by RecognizeAsync finishes.</span></span> <span data-ttu-id="a78ef-173">The last RecognitionResult is the end of the recognition.</span><span class="sxs-lookup"><span data-stu-id="a78ef-173">The last RecognitionResult is the end of the recognition.</span></span> <span data-ttu-id="a78ef-174">The task can fail if the service or the SDK fails unexpectedly.</span><span class="sxs-lookup"><span data-stu-id="a78ef-174">The task can fail if the service or the SDK fails unexpectedly.</span></span>

### <a name="speech-recognition-events"></a><span data-ttu-id="a78ef-175">Speech recognition events</span><span class="sxs-lookup"><span data-stu-id="a78ef-175">Speech recognition events</span></span>

#### <a name="partial-results-event"></a><span data-ttu-id="a78ef-176">Partial results event</span><span class="sxs-lookup"><span data-stu-id="a78ef-176">Partial results event</span></span>

<span data-ttu-id="a78ef-177">This event gets called every time Speech Service predicts what you might be saying, even before you finish speaking (if you use `MicrophoneRecognitionClient`) or finish sending data (if you use `DataRecognitionClient`).</span><span class="sxs-lookup"><span data-stu-id="a78ef-177">This event gets called every time Speech Service predicts what you might be saying, even before you finish speaking (if you use `MicrophoneRecognitionClient`) or finish sending data (if you use `DataRecognitionClient`).</span></span> <span data-ttu-id="a78ef-178">You can subscribe to the event by using `SpeechClient.SubscribeToPartialResult()`.</span><span class="sxs-lookup"><span data-stu-id="a78ef-178">You can subscribe to the event by using `SpeechClient.SubscribeToPartialResult()`.</span></span> <span data-ttu-id="a78ef-179">Or you can use the generic events subscription method `SpeechClient.SubscribeTo<RecognitionPartialResult>()`.</span><span class="sxs-lookup"><span data-stu-id="a78ef-179">Or you can use the generic events subscription method `SpeechClient.SubscribeTo<RecognitionPartialResult>()`.</span></span>

<span data-ttu-id="a78ef-180">**Return format**</span><span class="sxs-lookup"><span data-stu-id="a78ef-180">**Return format**</span></span> | <span data-ttu-id="a78ef-181">Description</span><span class="sxs-lookup"><span data-stu-id="a78ef-181">Description</span></span> |
------|------
<span data-ttu-id="a78ef-182">**LexicalForm**</span><span class="sxs-lookup"><span data-stu-id="a78ef-182">**LexicalForm**</span></span> | <span data-ttu-id="a78ef-183">This form is optimal for use by applications that need raw, unprocessed speech recognition results.</span><span class="sxs-lookup"><span data-stu-id="a78ef-183">This form is optimal for use by applications that need raw, unprocessed speech recognition results.</span></span>
<span data-ttu-id="a78ef-184">**DisplayText**</span><span class="sxs-lookup"><span data-stu-id="a78ef-184">**DisplayText**</span></span> | <span data-ttu-id="a78ef-185">The recognized phrase with inverse text normalization, capitalization, punctuation, and profanity masking applied.</span><span class="sxs-lookup"><span data-stu-id="a78ef-185">The recognized phrase with inverse text normalization, capitalization, punctuation, and profanity masking applied.</span></span> <span data-ttu-id="a78ef-186">Profanity is masked with asterisks after the initial character, for example, "d\*\*\*."</span><span class="sxs-lookup"><span data-stu-id="a78ef-186">Profanity is masked with asterisks after the initial character, for example, "d\*\*\*."</span></span> <span data-ttu-id="a78ef-187">This form is optimal for use by applications that display the speech recognition results to a user.</span><span class="sxs-lookup"><span data-stu-id="a78ef-187">This form is optimal for use by applications that display the speech recognition results to a user.</span></span>
<span data-ttu-id="a78ef-188">**Confidence**</span><span class="sxs-lookup"><span data-stu-id="a78ef-188">**Confidence**</span></span> | <span data-ttu-id="a78ef-189">The level of confidence the recognized phrase represents for the associated audio as defined by the speech recognition server.</span><span class="sxs-lookup"><span data-stu-id="a78ef-189">The level of confidence the recognized phrase represents for the associated audio as defined by the speech recognition server.</span></span>
<span data-ttu-id="a78ef-190">**MediaTime**</span><span class="sxs-lookup"><span data-stu-id="a78ef-190">**MediaTime**</span></span> | <span data-ttu-id="a78ef-191">The current time relative to the start of the audio stream (in 100-nanosecond units of time).</span><span class="sxs-lookup"><span data-stu-id="a78ef-191">The current time relative to the start of the audio stream (in 100-nanosecond units of time).</span></span>
<span data-ttu-id="a78ef-192">**MediaDuration**</span><span class="sxs-lookup"><span data-stu-id="a78ef-192">**MediaDuration**</span></span> | <span data-ttu-id="a78ef-193">The current phrase duration/length relative to the audio segment (in 100-nanosecond units of time).</span><span class="sxs-lookup"><span data-stu-id="a78ef-193">The current phrase duration/length relative to the audio segment (in 100-nanosecond units of time).</span></span>

#### <a name="result-event"></a><span data-ttu-id="a78ef-194">Result event</span><span class="sxs-lookup"><span data-stu-id="a78ef-194">Result event</span></span>
<span data-ttu-id="a78ef-195">When you finish speaking (in `ShortPhrase` mode), this event is called.</span><span class="sxs-lookup"><span data-stu-id="a78ef-195">When you finish speaking (in `ShortPhrase` mode), this event is called.</span></span> <span data-ttu-id="a78ef-196">You're provided with n-best choices for the result.</span><span class="sxs-lookup"><span data-stu-id="a78ef-196">You're provided with n-best choices for the result.</span></span> <span data-ttu-id="a78ef-197">In `LongDictation` mode, the event can be called multiple times, based on where the server indicates sentence pauses.</span><span class="sxs-lookup"><span data-stu-id="a78ef-197">In `LongDictation` mode, the event can be called multiple times, based on where the server indicates sentence pauses.</span></span> <span data-ttu-id="a78ef-198">You can subscribe to the event by using `SpeechClient.SubscribeToRecognitionResult()`.</span><span class="sxs-lookup"><span data-stu-id="a78ef-198">You can subscribe to the event by using `SpeechClient.SubscribeToRecognitionResult()`.</span></span> <span data-ttu-id="a78ef-199">Or you can use the generic events subscription method `SpeechClient.SubscribeTo<RecognitionResult>()`.</span><span class="sxs-lookup"><span data-stu-id="a78ef-199">Or you can use the generic events subscription method `SpeechClient.SubscribeTo<RecognitionResult>()`.</span></span>

<span data-ttu-id="a78ef-200">**Return format**</span><span class="sxs-lookup"><span data-stu-id="a78ef-200">**Return format**</span></span> | <span data-ttu-id="a78ef-201">Description</span><span class="sxs-lookup"><span data-stu-id="a78ef-201">Description</span></span> |
------|------|
<span data-ttu-id="a78ef-202">**RecognitionStatus**</span><span class="sxs-lookup"><span data-stu-id="a78ef-202">**RecognitionStatus**</span></span> | <span data-ttu-id="a78ef-203">The status on how the recognition was produced.</span><span class="sxs-lookup"><span data-stu-id="a78ef-203">The status on how the recognition was produced.</span></span> <span data-ttu-id="a78ef-204">For example, was it produced as a result of successful recognition or as a result of canceling the connection, etc.</span><span class="sxs-lookup"><span data-stu-id="a78ef-204">For example, was it produced as a result of successful recognition or as a result of canceling the connection, etc.</span></span>
<span data-ttu-id="a78ef-205">**Phrases**</span><span class="sxs-lookup"><span data-stu-id="a78ef-205">**Phrases**</span></span> | <span data-ttu-id="a78ef-206">The set of n-best recognized phrases with the recognition confidence.</span><span class="sxs-lookup"><span data-stu-id="a78ef-206">The set of n-best recognized phrases with the recognition confidence.</span></span>

<span data-ttu-id="a78ef-207">For more information on recognition results, see [Output format](../Concepts.md#output-format).</span><span class="sxs-lookup"><span data-stu-id="a78ef-207">For more information on recognition results, see [Output format](../Concepts.md#output-format).</span></span>

### <a name="speech-recognition-response"></a><span data-ttu-id="a78ef-208">Speech recognition response</span><span class="sxs-lookup"><span data-stu-id="a78ef-208">Speech recognition response</span></span>

<span data-ttu-id="a78ef-209">Speech response example:</span><span class="sxs-lookup"><span data-stu-id="a78ef-209">Speech response example:</span></span>
```
--- Partial result received by OnPartialResult  
---what  
--- Partial result received by OnPartialResult  
--what's  
--- Partial result received by OnPartialResult  
---what's the web  
--- Partial result received by OnPartialResult   
---what's the weather like  
---***** Phrase Recognition Status = [Success]   
***What's the weather like? (Confidence:High)  
What's the weather like? (Confidence:High) 
```

## <a name="connection-management"></a><span data-ttu-id="a78ef-210">Connection management</span><span class="sxs-lookup"><span data-stu-id="a78ef-210">Connection management</span></span>

<span data-ttu-id="a78ef-211">The API utilizes a single WebSocket connection per request.</span><span class="sxs-lookup"><span data-stu-id="a78ef-211">The API utilizes a single WebSocket connection per request.</span></span> <span data-ttu-id="a78ef-212">For optimal user experience, the SDK attempts to reconnect to Speech Service and start the recognition from the last RecognitionResult that it received.</span><span class="sxs-lookup"><span data-stu-id="a78ef-212">For optimal user experience, the SDK attempts to reconnect to Speech Service and start the recognition from the last RecognitionResult that it received.</span></span> <span data-ttu-id="a78ef-213">For example, if the audio request is two minutes long, the SDK received a RecognitionEvent at the one-minute mark, and a network failure occurred after five seconds, the SDK starts a new connection that starts from the one-minute mark.</span><span class="sxs-lookup"><span data-stu-id="a78ef-213">For example, if the audio request is two minutes long, the SDK received a RecognitionEvent at the one-minute mark, and a network failure occurred after five seconds, the SDK starts a new connection that starts from the one-minute mark.</span></span>

>[!NOTE]
><span data-ttu-id="a78ef-214">The SDK doesn't seek back to the one-minute mark because the stream might not support seeking.</span><span class="sxs-lookup"><span data-stu-id="a78ef-214">The SDK doesn't seek back to the one-minute mark because the stream might not support seeking.</span></span> <span data-ttu-id="a78ef-215">Instead, the SDK keeps an internal buffer that it uses to buffer the audio and clears the buffer as it receives RecognitionResult events.</span><span class="sxs-lookup"><span data-stu-id="a78ef-215">Instead, the SDK keeps an internal buffer that it uses to buffer the audio and clears the buffer as it receives RecognitionResult events.</span></span>

## <a name="buffering-behavior"></a><span data-ttu-id="a78ef-216">Buffering behavior</span><span class="sxs-lookup"><span data-stu-id="a78ef-216">Buffering behavior</span></span>

<span data-ttu-id="a78ef-217">By default, the SDK buffers audio so that it can recover when a network interrupt occurs.</span><span class="sxs-lookup"><span data-stu-id="a78ef-217">By default, the SDK buffers audio so that it can recover when a network interrupt occurs.</span></span> <span data-ttu-id="a78ef-218">In a scenario where it's preferable to discard the audio lost during the network disconnect and restart the connection, it's best to disable audio buffering by setting `EnableAudioBuffering` in the Preferences object to `false`.</span><span class="sxs-lookup"><span data-stu-id="a78ef-218">In a scenario where it's preferable to discard the audio lost during the network disconnect and restart the connection, it's best to disable audio buffering by setting `EnableAudioBuffering` in the Preferences object to `false`.</span></span>

## <a name="related-topics"></a><span data-ttu-id="a78ef-219">Related topics</span><span class="sxs-lookup"><span data-stu-id="a78ef-219">Related topics</span></span>

[<span data-ttu-id="a78ef-220">Microsoft Speech C# service library reference</span><span class="sxs-lookup"><span data-stu-id="a78ef-220">Microsoft Speech C# service library reference</span></span>](https://cdn.rawgit.com/Microsoft/Cognitive-Speech-STT-ServiceLibrary/master/docs/index.html)
