---
title: Cognitive Services Speech SDK Documentation | Microsoft Docs
description: Release notes - what has changed in the most recent releases
titleSuffix: Microsoft Cognitive Services
services: cognitive-services
author: wolfma61
manager: onano
ms.service: cognitive-services
ms.component: speech-service
ms.topic: article
ms.date: 08/16/2018
ms.author: wolfma
ms.openlocfilehash: bbf3c5930de2ec6c709b6b527ae3eac107382420
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866259"
---
# <a name="release-notes"></a><span data-ttu-id="b84c3-103">Release notes</span><span class="sxs-lookup"><span data-stu-id="b84c3-103">Release notes</span></span>

## <a name="cognitive-services-speech-sdk-060-2018-august-release"></a><span data-ttu-id="b84c3-104">Cognitive Services Speech SDK 0.6.0: 2018-August release</span><span class="sxs-lookup"><span data-stu-id="b84c3-104">Cognitive Services Speech SDK 0.6.0: 2018-August release</span></span>

<span data-ttu-id="b84c3-105">**New features**</span><span class="sxs-lookup"><span data-stu-id="b84c3-105">**New features**</span></span>

* <span data-ttu-id="b84c3-106">UWP apps built with the Speech SDK can now pass the Windows App Certification Kit (WACK).</span><span class="sxs-lookup"><span data-stu-id="b84c3-106">UWP apps built with the Speech SDK can now pass the Windows App Certification Kit (WACK).</span></span>
  <span data-ttu-id="b84c3-107">Check out our [UWP quickstart](quickstart-csharp-uwp.md).</span><span class="sxs-lookup"><span data-stu-id="b84c3-107">Check out our [UWP quickstart](quickstart-csharp-uwp.md).</span></span>
* <span data-ttu-id="b84c3-108">Support for .NET Standard 2.0 on Linux (Ubuntu 16.04 x64).</span><span class="sxs-lookup"><span data-stu-id="b84c3-108">Support for .NET Standard 2.0 on Linux (Ubuntu 16.04 x64).</span></span>
* <span data-ttu-id="b84c3-109">Experimental: Support Java 8 on Windows (64-bit) and Linux (Ubuntu 16.04 x64).</span><span class="sxs-lookup"><span data-stu-id="b84c3-109">Experimental: Support Java 8 on Windows (64-bit) and Linux (Ubuntu 16.04 x64).</span></span>
  <span data-ttu-id="b84c3-110">Check out the [Java Run-Time Environment quickstart](quickstart-java-jre.md)</span><span class="sxs-lookup"><span data-stu-id="b84c3-110">Check out the [Java Run-Time Environment quickstart](quickstart-java-jre.md)</span></span>

<span data-ttu-id="b84c3-111">**Functional changes**</span><span class="sxs-lookup"><span data-stu-id="b84c3-111">**Functional changes**</span></span>

* <span data-ttu-id="b84c3-112">Exposing additional error detail information on connection errors.</span><span class="sxs-lookup"><span data-stu-id="b84c3-112">Exposing additional error detail information on connection errors.</span></span>

<span data-ttu-id="b84c3-113">**Breaking changes**</span><span class="sxs-lookup"><span data-stu-id="b84c3-113">**Breaking changes**</span></span>

* <span data-ttu-id="b84c3-114">On Java (Android), the `SpeechFactory.configureNativePlatformBindingWithDefaultCertificate` function no longer requires a path parameter.</span><span class="sxs-lookup"><span data-stu-id="b84c3-114">On Java (Android), the `SpeechFactory.configureNativePlatformBindingWithDefaultCertificate` function no longer requires a path parameter.</span></span> <span data-ttu-id="b84c3-115">The path is now automatically detected on all supported platforms.</span><span class="sxs-lookup"><span data-stu-id="b84c3-115">The path is now automatically detected on all supported platforms.</span></span>
* <span data-ttu-id="b84c3-116">The get-accessor of the property `EndpointUrl` in Java and C# was removed.</span><span class="sxs-lookup"><span data-stu-id="b84c3-116">The get-accessor of the property `EndpointUrl` in Java and C# was removed.</span></span>

<span data-ttu-id="b84c3-117">**Bug fixes**</span><span class="sxs-lookup"><span data-stu-id="b84c3-117">**Bug fixes**</span></span>

* <span data-ttu-id="b84c3-118">In Java, the audio synthesis result on the translation recognizer is now implemented.</span><span class="sxs-lookup"><span data-stu-id="b84c3-118">In Java, the audio synthesis result on the translation recognizer is now implemented.</span></span>
* <span data-ttu-id="b84c3-119">Fixed a bug, that could cause inactive threads and an increased number of open and unused sockets.</span><span class="sxs-lookup"><span data-stu-id="b84c3-119">Fixed a bug, that could cause inactive threads and an increased number of open and unused sockets.</span></span>
* <span data-ttu-id="b84c3-120">Fixed a problem, where a long running recognition could terminate in the middle the transmission.</span><span class="sxs-lookup"><span data-stu-id="b84c3-120">Fixed a problem, where a long running recognition could terminate in the middle the transmission.</span></span>
* <span data-ttu-id="b84c3-121">Fixed a race condition in recognizer shutdown.</span><span class="sxs-lookup"><span data-stu-id="b84c3-121">Fixed a race condition in recognizer shutdown.</span></span>

## <a name="cognitive-services-speech-sdk-050-2018-july-release"></a><span data-ttu-id="b84c3-122">Cognitive Services Speech SDK 0.5.0: 2018-July release</span><span class="sxs-lookup"><span data-stu-id="b84c3-122">Cognitive Services Speech SDK 0.5.0: 2018-July release</span></span>

<span data-ttu-id="b84c3-123">**New features**</span><span class="sxs-lookup"><span data-stu-id="b84c3-123">**New features**</span></span>

* <span data-ttu-id="b84c3-124">Support Android platform (API 23: Android 6.0 Marshmallow or higher).</span><span class="sxs-lookup"><span data-stu-id="b84c3-124">Support Android platform (API 23: Android 6.0 Marshmallow or higher).</span></span>
  <span data-ttu-id="b84c3-125">Check out the [Android quickstart](quickstart-java-android.md).</span><span class="sxs-lookup"><span data-stu-id="b84c3-125">Check out the [Android quickstart](quickstart-java-android.md).</span></span>
* <span data-ttu-id="b84c3-126">Support .NET Standard 2.0 on Windows.</span><span class="sxs-lookup"><span data-stu-id="b84c3-126">Support .NET Standard 2.0 on Windows.</span></span>
  <span data-ttu-id="b84c3-127">Check out the [.NET Core quickstart](quickstart-csharp-dotnetcore-windows.md).</span><span class="sxs-lookup"><span data-stu-id="b84c3-127">Check out the [.NET Core quickstart](quickstart-csharp-dotnetcore-windows.md).</span></span>
* <span data-ttu-id="b84c3-128">Experimental: Support UWP on Windows (version 1709 or later)</span><span class="sxs-lookup"><span data-stu-id="b84c3-128">Experimental: Support UWP on Windows (version 1709 or later)</span></span>
  * <span data-ttu-id="b84c3-129">Check out our [UWP quickstart](quickstart-csharp-uwp.md).</span><span class="sxs-lookup"><span data-stu-id="b84c3-129">Check out our [UWP quickstart](quickstart-csharp-uwp.md).</span></span>
  * <span data-ttu-id="b84c3-130">Note: UWP apps built with the Speech SDK do not yet pass the Windows App Certification Kit (WACK).</span><span class="sxs-lookup"><span data-stu-id="b84c3-130">Note: UWP apps built with the Speech SDK do not yet pass the Windows App Certification Kit (WACK).</span></span>
* <span data-ttu-id="b84c3-131">Support long running recognition with automatic reconnection.</span><span class="sxs-lookup"><span data-stu-id="b84c3-131">Support long running recognition with automatic reconnection.</span></span>

<span data-ttu-id="b84c3-132">**Functional changes**</span><span class="sxs-lookup"><span data-stu-id="b84c3-132">**Functional changes**</span></span>

* <span data-ttu-id="b84c3-133">`StartContinuousRecognitionAsync()` supports long running recognition</span><span class="sxs-lookup"><span data-stu-id="b84c3-133">`StartContinuousRecognitionAsync()` supports long running recognition</span></span>
* <span data-ttu-id="b84c3-134">The recognition result contains more fields: offset from the audio beginning and duration (both in ticks) of the recognized text, additional values representing recognition status, e.g., `InitialSilenceTimeout`, `InitialBabbleTimeout`.</span><span class="sxs-lookup"><span data-stu-id="b84c3-134">The recognition result contains more fields: offset from the audio beginning and duration (both in ticks) of the recognized text, additional values representing recognition status, e.g., `InitialSilenceTimeout`, `InitialBabbleTimeout`.</span></span>
* <span data-ttu-id="b84c3-135">Support AuthorizationToken for creating factory instances.</span><span class="sxs-lookup"><span data-stu-id="b84c3-135">Support AuthorizationToken for creating factory instances.</span></span>

<span data-ttu-id="b84c3-136">**Breaking changes**</span><span class="sxs-lookup"><span data-stu-id="b84c3-136">**Breaking changes**</span></span>

* <span data-ttu-id="b84c3-137">Recognition events: NoMatch event type is merged into the Error event.</span><span class="sxs-lookup"><span data-stu-id="b84c3-137">Recognition events: NoMatch event type is merged into the Error event.</span></span>
* <span data-ttu-id="b84c3-138">SpeechOutputFormat in C# is renamed to OutputFormat to keep aligned with C++.</span><span class="sxs-lookup"><span data-stu-id="b84c3-138">SpeechOutputFormat in C# is renamed to OutputFormat to keep aligned with C++.</span></span>
* <span data-ttu-id="b84c3-139">The return type of some methods of the `AudioInputStream` interface slightly changed:</span><span class="sxs-lookup"><span data-stu-id="b84c3-139">The return type of some methods of the `AudioInputStream` interface slightly changed:</span></span>
   * <span data-ttu-id="b84c3-140">In Java, the `read` method now returns `long` instead of `int`.</span><span class="sxs-lookup"><span data-stu-id="b84c3-140">In Java, the `read` method now returns `long` instead of `int`.</span></span>
   * <span data-ttu-id="b84c3-141">In C#, the `Read` method now returns `uint` instead of `int`.</span><span class="sxs-lookup"><span data-stu-id="b84c3-141">In C#, the `Read` method now returns `uint` instead of `int`.</span></span>
   * <span data-ttu-id="b84c3-142">In C++, the `Read` and `GetFormat` methods now return `size_t` instead of `int`.</span><span class="sxs-lookup"><span data-stu-id="b84c3-142">In C++, the `Read` and `GetFormat` methods now return `size_t` instead of `int`.</span></span>
* <span data-ttu-id="b84c3-143">C++: instances of audio input streams can now only be passed as a `shared_ptr`.</span><span class="sxs-lookup"><span data-stu-id="b84c3-143">C++: instances of audio input streams can now only be passed as a `shared_ptr`.</span></span>

<span data-ttu-id="b84c3-144">**Bug fixes**</span><span class="sxs-lookup"><span data-stu-id="b84c3-144">**Bug fixes**</span></span>

* <span data-ttu-id="b84c3-145">Fixed incorrect return values in result when `RecognizeAsync()` times out.</span><span class="sxs-lookup"><span data-stu-id="b84c3-145">Fixed incorrect return values in result when `RecognizeAsync()` times out.</span></span>
* <span data-ttu-id="b84c3-146">The dependency on media foundation libraries on Windows is removed.</span><span class="sxs-lookup"><span data-stu-id="b84c3-146">The dependency on media foundation libraries on Windows is removed.</span></span> <span data-ttu-id="b84c3-147">The SDK is now using Core Audio APIs.</span><span class="sxs-lookup"><span data-stu-id="b84c3-147">The SDK is now using Core Audio APIs.</span></span>
* <span data-ttu-id="b84c3-148">Documentation fix: added a [regions](regions.md) page to describe what are the supported regions.</span><span class="sxs-lookup"><span data-stu-id="b84c3-148">Documentation fix: added a [regions](regions.md) page to describe what are the supported regions.</span></span>

<span data-ttu-id="b84c3-149">**Known issues**</span><span class="sxs-lookup"><span data-stu-id="b84c3-149">**Known issues**</span></span>

* <span data-ttu-id="b84c3-150">The Speech SDK for Android does not report speech synthesis results for translation.</span><span class="sxs-lookup"><span data-stu-id="b84c3-150">The Speech SDK for Android does not report speech synthesis results for translation.</span></span>
  <span data-ttu-id="b84c3-151">This will be fixed in the next release.</span><span class="sxs-lookup"><span data-stu-id="b84c3-151">This will be fixed in the next release.</span></span>

## <a name="cognitive-services-speech-sdk-040-2018-june-release"></a><span data-ttu-id="b84c3-152">Cognitive Services Speech SDK 0.4.0: 2018-June release</span><span class="sxs-lookup"><span data-stu-id="b84c3-152">Cognitive Services Speech SDK 0.4.0: 2018-June release</span></span>

<span data-ttu-id="b84c3-153">**Functional changes**</span><span class="sxs-lookup"><span data-stu-id="b84c3-153">**Functional changes**</span></span>

- <span data-ttu-id="b84c3-154">AudioInputStream</span><span class="sxs-lookup"><span data-stu-id="b84c3-154">AudioInputStream</span></span>

  <span data-ttu-id="b84c3-155">A recognizer can now consume a stream as the audio source.</span><span class="sxs-lookup"><span data-stu-id="b84c3-155">A recognizer can now consume a stream as the audio source.</span></span> <span data-ttu-id="b84c3-156">For detailed information, see the related [how-to guide](how-to-use-audio-input-streams.md).</span><span class="sxs-lookup"><span data-stu-id="b84c3-156">For detailed information, see the related [how-to guide](how-to-use-audio-input-streams.md).</span></span>

- <span data-ttu-id="b84c3-157">Detailed output format</span><span class="sxs-lookup"><span data-stu-id="b84c3-157">Detailed output format</span></span>

  <span data-ttu-id="b84c3-158">While creating a `SpeechRecognizer`, you can request `Detailed` or `Simple` output format.</span><span class="sxs-lookup"><span data-stu-id="b84c3-158">While creating a `SpeechRecognizer`, you can request `Detailed` or `Simple` output format.</span></span> <span data-ttu-id="b84c3-159">The `DetailedSpeechRecognitionResult` contains a confidence score, recognized text, raw lexical form, normalized form, and normalized form with masked profanity.</span><span class="sxs-lookup"><span data-stu-id="b84c3-159">The `DetailedSpeechRecognitionResult` contains a confidence score, recognized text, raw lexical form, normalized form, and normalized form with masked profanity.</span></span>

<span data-ttu-id="b84c3-160">**Breaking change**</span><span class="sxs-lookup"><span data-stu-id="b84c3-160">**Breaking change**</span></span>

- <span data-ttu-id="b84c3-161">Change to `SpeechRecognitionResult.Text` from `SpeechRecognitionResult.RecognizedText` in C#.</span><span class="sxs-lookup"><span data-stu-id="b84c3-161">Change to `SpeechRecognitionResult.Text` from `SpeechRecognitionResult.RecognizedText` in C#.</span></span>

<span data-ttu-id="b84c3-162">**Bug fixes**</span><span class="sxs-lookup"><span data-stu-id="b84c3-162">**Bug fixes**</span></span>

- <span data-ttu-id="b84c3-163">Fix a possible callback issue in USP layer during shutdown.</span><span class="sxs-lookup"><span data-stu-id="b84c3-163">Fix a possible callback issue in USP layer during shutdown.</span></span>

- <span data-ttu-id="b84c3-164">If a recognizer consumed an audio input file, it was holding on to the file handle longer than necessary.</span><span class="sxs-lookup"><span data-stu-id="b84c3-164">If a recognizer consumed an audio input file, it was holding on to the file handle longer than necessary.</span></span>

- <span data-ttu-id="b84c3-165">Removed several deadlocks between message pump and recognizer.</span><span class="sxs-lookup"><span data-stu-id="b84c3-165">Removed several deadlocks between message pump and recognizer.</span></span>

- <span data-ttu-id="b84c3-166">Fire a `NoMatch` result when the response from service is timed out.</span><span class="sxs-lookup"><span data-stu-id="b84c3-166">Fire a `NoMatch` result when the response from service is timed out.</span></span>

- <span data-ttu-id="b84c3-167">The media foundation libraries on Windows are delay-loaded.</span><span class="sxs-lookup"><span data-stu-id="b84c3-167">The media foundation libraries on Windows are delay-loaded.</span></span> <span data-ttu-id="b84c3-168">This library is only required for microphone input.</span><span class="sxs-lookup"><span data-stu-id="b84c3-168">This library is only required for microphone input.</span></span>

- <span data-ttu-id="b84c3-169">The upload speed for audio data is limited to about twice the original audio speed.</span><span class="sxs-lookup"><span data-stu-id="b84c3-169">The upload speed for audio data is limited to about twice the original audio speed.</span></span>

- <span data-ttu-id="b84c3-170">On Windows, C# .NET assemblies are now strong-named.</span><span class="sxs-lookup"><span data-stu-id="b84c3-170">On Windows, C# .NET assemblies are now strong-named.</span></span>

- <span data-ttu-id="b84c3-171">Documentation fix: `Region` is required information to create a recognizer.</span><span class="sxs-lookup"><span data-stu-id="b84c3-171">Documentation fix: `Region` is required information to create a recognizer.</span></span>

<span data-ttu-id="b84c3-172">More samples have been added and are constantly being updated.</span><span class="sxs-lookup"><span data-stu-id="b84c3-172">More samples have been added and are constantly being updated.</span></span> <span data-ttu-id="b84c3-173">For the latest set of samples, see the [Speech SDK Sample GitHub repository](https://aka.ms/csspeech/samples).</span><span class="sxs-lookup"><span data-stu-id="b84c3-173">For the latest set of samples, see the [Speech SDK Sample GitHub repository](https://aka.ms/csspeech/samples).</span></span>

## <a name="cognitive-services-speech-sdk-0212733-2018-may-release"></a><span data-ttu-id="b84c3-174">Cognitive Services Speech SDK 0.2.12733: 2018-May release</span><span class="sxs-lookup"><span data-stu-id="b84c3-174">Cognitive Services Speech SDK 0.2.12733: 2018-May release</span></span>

<span data-ttu-id="b84c3-175">The first public preview release of the Cognitive Services Speech SDK.</span><span class="sxs-lookup"><span data-stu-id="b84c3-175">The first public preview release of the Cognitive Services Speech SDK.</span></span>
