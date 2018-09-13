---
title: AudioInputStream concepts
description: An overview of the capabilities of the AudioInputStream API.
titleSuffix: Microsoft Cognitive Services
services: cognitive-services
author: fmegen
ms.service: cognitive-services
ms.component: speech-service
ms.topic: article
ms.date: 06/07/2018
ms.author: fmegen
ms.openlocfilehash: b3e12fbc616c8d67b557102c6094467e119a23f1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871182"
---
# <a name="about-the-audio-input-stream-api"></a><span data-ttu-id="55c51-103">About the audio input stream API</span><span class="sxs-lookup"><span data-stu-id="55c51-103">About the audio input stream API</span></span>

<span data-ttu-id="55c51-104">The **Audio Input Stream** API provides a way to stream audio streams into the recognizers instead of using either the microphone or the input file APIs.</span><span class="sxs-lookup"><span data-stu-id="55c51-104">The **Audio Input Stream** API provides a way to stream audio streams into the recognizers instead of using either the microphone or the input file APIs.</span></span>

## <a name="api-overview"></a><span data-ttu-id="55c51-105">API overview</span><span class="sxs-lookup"><span data-stu-id="55c51-105">API overview</span></span>

<span data-ttu-id="55c51-106">The API uses two components, the `AudioInputStream` (the raw audio data) and the `AudioInputStreamFormat`.</span><span class="sxs-lookup"><span data-stu-id="55c51-106">The API uses two components, the `AudioInputStream` (the raw audio data) and the `AudioInputStreamFormat`.</span></span>

<span data-ttu-id="55c51-107">The `AudioInputStreamFormat` defines the format of the audio data.</span><span class="sxs-lookup"><span data-stu-id="55c51-107">The `AudioInputStreamFormat` defines the format of the audio data.</span></span> <span data-ttu-id="55c51-108">It can be compared to the standard `WAVEFORMAT` structure for wave files on Windows.</span><span class="sxs-lookup"><span data-stu-id="55c51-108">It can be compared to the standard `WAVEFORMAT` structure for wave files on Windows.</span></span>

  - `FormatTag`

    <span data-ttu-id="55c51-109">The format of the audio.</span><span class="sxs-lookup"><span data-stu-id="55c51-109">The format of the audio.</span></span> <span data-ttu-id="55c51-110">The Speech SDK currently only supports `format 1` (PCM - little-endian).</span><span class="sxs-lookup"><span data-stu-id="55c51-110">The Speech SDK currently only supports `format 1` (PCM - little-endian).</span></span>

  - `Channels`

    <span data-ttu-id="55c51-111">The number of channels.</span><span class="sxs-lookup"><span data-stu-id="55c51-111">The number of channels.</span></span> <span data-ttu-id="55c51-112">The current speech service supports only one channel (mono) audio material.</span><span class="sxs-lookup"><span data-stu-id="55c51-112">The current speech service supports only one channel (mono) audio material.</span></span>

  - `SamplesPerSec`

    <span data-ttu-id="55c51-113">The sample rate.</span><span class="sxs-lookup"><span data-stu-id="55c51-113">The sample rate.</span></span> <span data-ttu-id="55c51-114">A typical microphone recording has 16000 samples per second.</span><span class="sxs-lookup"><span data-stu-id="55c51-114">A typical microphone recording has 16000 samples per second.</span></span>

  - `AvgBytesPerSec`

    <span data-ttu-id="55c51-115">Average bytes per second, calculated as `SamplesPerSec * Channels * ceil(BitsPerSample, 8)`.</span><span class="sxs-lookup"><span data-stu-id="55c51-115">Average bytes per second, calculated as `SamplesPerSec * Channels * ceil(BitsPerSample, 8)`.</span></span> <span data-ttu-id="55c51-116">Average bytes per second can be different for audio streams that use variable bitrates.</span><span class="sxs-lookup"><span data-stu-id="55c51-116">Average bytes per second can be different for audio streams that use variable bitrates.</span></span>

  - `BlockAlign`

    <span data-ttu-id="55c51-117">The size of a single frame, calculated as `Channels * ceil(wBitsPerSample, 8)`.</span><span class="sxs-lookup"><span data-stu-id="55c51-117">The size of a single frame, calculated as `Channels * ceil(wBitsPerSample, 8)`.</span></span> <span data-ttu-id="55c51-118">Due to padding, the actual value might be higher than this value.</span><span class="sxs-lookup"><span data-stu-id="55c51-118">Due to padding, the actual value might be higher than this value.</span></span>

  - `BitsPerSample`

    <span data-ttu-id="55c51-119">The bits per sample.</span><span class="sxs-lookup"><span data-stu-id="55c51-119">The bits per sample.</span></span> <span data-ttu-id="55c51-120">A typical audio stream uses 16 bits per sample (CD quality).</span><span class="sxs-lookup"><span data-stu-id="55c51-120">A typical audio stream uses 16 bits per sample (CD quality).</span></span>

<span data-ttu-id="55c51-121">The `AudioInputStream` base class will be overridden by your custom stream adapter.</span><span class="sxs-lookup"><span data-stu-id="55c51-121">The `AudioInputStream` base class will be overridden by your custom stream adapter.</span></span> <span data-ttu-id="55c51-122">This adapter has to implement these functions:</span><span class="sxs-lookup"><span data-stu-id="55c51-122">This adapter has to implement these functions:</span></span>

   - `GetFormat()`

     <span data-ttu-id="55c51-123">This function is called to get the format of the audio stream.</span><span class="sxs-lookup"><span data-stu-id="55c51-123">This function is called to get the format of the audio stream.</span></span> <span data-ttu-id="55c51-124">It gets a pointer to the AudioInputStreamFormat buffer.</span><span class="sxs-lookup"><span data-stu-id="55c51-124">It gets a pointer to the AudioInputStreamFormat buffer.</span></span>

   - `Read()`

     <span data-ttu-id="55c51-125">This function is called to get data from the audio stream.</span><span class="sxs-lookup"><span data-stu-id="55c51-125">This function is called to get data from the audio stream.</span></span> <span data-ttu-id="55c51-126">One parameter is a pointer to the buffer to copy the audio data into.</span><span class="sxs-lookup"><span data-stu-id="55c51-126">One parameter is a pointer to the buffer to copy the audio data into.</span></span> <span data-ttu-id="55c51-127">The second parameter is the size of the buffer.</span><span class="sxs-lookup"><span data-stu-id="55c51-127">The second parameter is the size of the buffer.</span></span> <span data-ttu-id="55c51-128">The function returns the number of bytes copied to the buffer.</span><span class="sxs-lookup"><span data-stu-id="55c51-128">The function returns the number of bytes copied to the buffer.</span></span> <span data-ttu-id="55c51-129">A return value of `0` indicates the end of the stream.</span><span class="sxs-lookup"><span data-stu-id="55c51-129">A return value of `0` indicates the end of the stream.</span></span>

   - `Close()`

     <span data-ttu-id="55c51-130">This function is called to close the audio stream.</span><span class="sxs-lookup"><span data-stu-id="55c51-130">This function is called to close the audio stream.</span></span>

## <a name="usage-examples"></a><span data-ttu-id="55c51-131">Usage examples</span><span class="sxs-lookup"><span data-stu-id="55c51-131">Usage examples</span></span>

<span data-ttu-id="55c51-132">In general, the following steps are involved when using audio input streams:</span><span class="sxs-lookup"><span data-stu-id="55c51-132">In general, the following steps are involved when using audio input streams:</span></span>

  - <span data-ttu-id="55c51-133">Identify the format of the audio stream.</span><span class="sxs-lookup"><span data-stu-id="55c51-133">Identify the format of the audio stream.</span></span> <span data-ttu-id="55c51-134">The format must be supported by the SDK and the speech service.</span><span class="sxs-lookup"><span data-stu-id="55c51-134">The format must be supported by the SDK and the speech service.</span></span> <span data-ttu-id="55c51-135">Currently the following configuration is supported:</span><span class="sxs-lookup"><span data-stu-id="55c51-135">Currently the following configuration is supported:</span></span>

    <span data-ttu-id="55c51-136">One audio format tag (PCM), one channel, 16000 samples per second, 32000 bytes per second, two block align (16 bit including padding for a sample), 16 bits per sample</span><span class="sxs-lookup"><span data-stu-id="55c51-136">One audio format tag (PCM), one channel, 16000 samples per second, 32000 bytes per second, two block align (16 bit including padding for a sample), 16 bits per sample</span></span>

  - <span data-ttu-id="55c51-137">Make sure your code can provide the RAW audio data as to the specs identified above.</span><span class="sxs-lookup"><span data-stu-id="55c51-137">Make sure your code can provide the RAW audio data as to the specs identified above.</span></span> <span data-ttu-id="55c51-138">If your audio source data doesn't match the supported formats, the audio must be transcoded into the required format.</span><span class="sxs-lookup"><span data-stu-id="55c51-138">If your audio source data doesn't match the supported formats, the audio must be transcoded into the required format.</span></span>

  - <span data-ttu-id="55c51-139">Derive your custom audio input stream class from `AudioInputStream`.</span><span class="sxs-lookup"><span data-stu-id="55c51-139">Derive your custom audio input stream class from `AudioInputStream`.</span></span> <span data-ttu-id="55c51-140">Implement the `GetFormat()`, `Read()`, and `Close()` operation.</span><span class="sxs-lookup"><span data-stu-id="55c51-140">Implement the `GetFormat()`, `Read()`, and `Close()` operation.</span></span> <span data-ttu-id="55c51-141">The exact function signature is language-dependent, but the code will look similar to this code sample::</span><span class="sxs-lookup"><span data-stu-id="55c51-141">The exact function signature is language-dependent, but the code will look similar to this code sample::</span></span>

    ```
     public class ContosoAudioStream : AudioInputStream {
        ContosoConfig config;

        public ContosoAudioStream(const ContosoConfig& config) {
            this.config = config;
        }

        public void GetFormat(AudioInputStreamFormat& format) {
            // returns format data to the caller.
            // e.g. format.FormatTag = config.XXX;
            // ...
        }

        public size_t Read(byte *buffer, size_t size) {
            // returns audio data to the caller.
            // e.g. return read(config.YYY, buffer, size);
        }

        public void Close() {
            // close and cleanup resources.
        }
     };
    ```

  - <span data-ttu-id="55c51-142">Use your audio input stream:</span><span class="sxs-lookup"><span data-stu-id="55c51-142">Use your audio input stream:</span></span>

    ```
    var contosoStream = new ContosoAudioStream(contosoConfig);

    var factory = SpeechFactory.FromSubscription(...);
    var recognizer = CreateSpeechRecognizerWithStream(contosoStream);

    // run stream through recognizer
    var result = await recognizer.RecognizeAsync();

    var text = result.GetText();

    // In some languages you need to delete the stream explicitly.
    // delete contosoStream;
    ```

  - <span data-ttu-id="55c51-143">In some languages, the `contosoStream` must be deleted explicitly after the recognition is complete.</span><span class="sxs-lookup"><span data-stu-id="55c51-143">In some languages, the `contosoStream` must be deleted explicitly after the recognition is complete.</span></span> <span data-ttu-id="55c51-144">You can't release the AudioStream before the complete input is read.</span><span class="sxs-lookup"><span data-stu-id="55c51-144">You can't release the AudioStream before the complete input is read.</span></span> <span data-ttu-id="55c51-145">In a scenario using `StopContinuousRecognitionAsync` and `StopContinuousRecognitionAsync` it requires a concept illustrated in this sample:</span><span class="sxs-lookup"><span data-stu-id="55c51-145">In a scenario using `StopContinuousRecognitionAsync` and `StopContinuousRecognitionAsync` it requires a concept illustrated in this sample:</span></span>

    ```
    var contosoStream = new ContosoAudioStream(contosoConfig);

    var factory = SpeechFactory.FromSubscription(...);
    var recognizer = CreateSpeechRecognizerWithStream(contosoStream);

    // run stream through recognizer
    await recognizer.StartContinuousRecognitionAsync();

    // ERROR: do not delete the contosoStream before ending recognition!
    // delete contosoStream;

    await recognizer.StopContinuousRecognitionAsync();

    // OK: Safe to delete the contosoStream.
    // delete contosoStream;
    ```

## <a name="next-steps"></a><span data-ttu-id="55c51-146">Next steps</span><span class="sxs-lookup"><span data-stu-id="55c51-146">Next steps</span></span>

* [<span data-ttu-id="55c51-147">Get your Speech trial subscription</span><span class="sxs-lookup"><span data-stu-id="55c51-147">Get your Speech trial subscription</span></span>](https://azure.microsoft.com/try/cognitive-services/)
* [<span data-ttu-id="55c51-148">See how to recognize speech in C#</span><span class="sxs-lookup"><span data-stu-id="55c51-148">See how to recognize speech in C#</span></span>](quickstart-csharp-dotnet-windows.md)
