---
title: Azure Batch transcription API
description: Samples
services: cognitive-services
author: PanosPeriorellis
ms.service: cognitive-services
ms.technology: Speech to Text
ms.topic: article
ms.date: 04/26/2018
ms.author: panosper
ms.openlocfilehash: b6fb39ef5941157cfe0d18324deeb9d836d7ab09
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869008"
---
# <a name="batch-transcription"></a><span data-ttu-id="9c29a-103">Batch transcription</span><span class="sxs-lookup"><span data-stu-id="9c29a-103">Batch transcription</span></span>

<span data-ttu-id="9c29a-104">Batch transcription is ideal if you have large amounts of audio.</span><span class="sxs-lookup"><span data-stu-id="9c29a-104">Batch transcription is ideal if you have large amounts of audio.</span></span> <span data-ttu-id="9c29a-105">You can point to audio files and get back transcriptions in asynchronous mode.</span><span class="sxs-lookup"><span data-stu-id="9c29a-105">You can point to audio files and get back transcriptions in asynchronous mode.</span></span>

## <a name="batch-transcription-api"></a><span data-ttu-id="9c29a-106">Batch transcription API</span><span class="sxs-lookup"><span data-stu-id="9c29a-106">Batch transcription API</span></span>

<span data-ttu-id="9c29a-107">The Batch transcription API offers asynchronous speech to text transcription, along with additional features.</span><span class="sxs-lookup"><span data-stu-id="9c29a-107">The Batch transcription API offers asynchronous speech to text transcription, along with additional features.</span></span>

> [!NOTE]
> <span data-ttu-id="9c29a-108">The Batch transcription API is ideal for call centers, which typically accumulate thousands of hours of audio.</span><span class="sxs-lookup"><span data-stu-id="9c29a-108">The Batch transcription API is ideal for call centers, which typically accumulate thousands of hours of audio.</span></span> <span data-ttu-id="9c29a-109">The API is guided by a "fire and forget" philosophy, which makes it easy to transcribe large volume of audio recordings.</span><span class="sxs-lookup"><span data-stu-id="9c29a-109">The API is guided by a "fire and forget" philosophy, which makes it easy to transcribe large volume of audio recordings.</span></span>

### <a name="supported-formats"></a><span data-ttu-id="9c29a-110">Supported formats</span><span class="sxs-lookup"><span data-stu-id="9c29a-110">Supported formats</span></span>

<span data-ttu-id="9c29a-111">The Batch transcription API supports the following formats:</span><span class="sxs-lookup"><span data-stu-id="9c29a-111">The Batch transcription API supports the following formats:</span></span>

<span data-ttu-id="9c29a-112">Name</span><span class="sxs-lookup"><span data-stu-id="9c29a-112">Name</span></span>| <span data-ttu-id="9c29a-113">Channel</span><span class="sxs-lookup"><span data-stu-id="9c29a-113">Channel</span></span>  |
----|----------|
<span data-ttu-id="9c29a-114">mp3</span><span class="sxs-lookup"><span data-stu-id="9c29a-114">mp3</span></span> |   <span data-ttu-id="9c29a-115">Mono</span><span class="sxs-lookup"><span data-stu-id="9c29a-115">Mono</span></span>   |   
<span data-ttu-id="9c29a-116">mp3</span><span class="sxs-lookup"><span data-stu-id="9c29a-116">mp3</span></span> |  <span data-ttu-id="9c29a-117">Stereo</span><span class="sxs-lookup"><span data-stu-id="9c29a-117">Stereo</span></span>  | 
<span data-ttu-id="9c29a-118">wav</span><span class="sxs-lookup"><span data-stu-id="9c29a-118">wav</span></span> |   <span data-ttu-id="9c29a-119">Mono</span><span class="sxs-lookup"><span data-stu-id="9c29a-119">Mono</span></span>   |
<span data-ttu-id="9c29a-120">wav</span><span class="sxs-lookup"><span data-stu-id="9c29a-120">wav</span></span> |  <span data-ttu-id="9c29a-121">Stereo</span><span class="sxs-lookup"><span data-stu-id="9c29a-121">Stereo</span></span>  |

<span data-ttu-id="9c29a-122">For stereo audio streams, Batch transcription splits the left and right channel during the transcription.</span><span class="sxs-lookup"><span data-stu-id="9c29a-122">For stereo audio streams, Batch transcription splits the left and right channel during the transcription.</span></span> <span data-ttu-id="9c29a-123">The two JSON files with the result are each created from a single channel.</span><span class="sxs-lookup"><span data-stu-id="9c29a-123">The two JSON files with the result are each created from a single channel.</span></span> <span data-ttu-id="9c29a-124">The timestamps per utterance enable the developer to create an ordered final transcript.</span><span class="sxs-lookup"><span data-stu-id="9c29a-124">The timestamps per utterance enable the developer to create an ordered final transcript.</span></span> <span data-ttu-id="9c29a-125">The following JSON sample shows the output of a channel.</span><span class="sxs-lookup"><span data-stu-id="9c29a-125">The following JSON sample shows the output of a channel.</span></span>

```json
       {
        "recordingsUrl": "https://mystorage.blob.core.windows.net/cris-e2e-datasets/TranscriptionsDataset/small_sentence.wav?st=2018-04-19T15:56:00Z&se=2040-04-21T15:56:00Z&sp=rl&sv=2017-04-17&sr=b&sig=DtvXbMYquDWQ2OkhAenGuyZI%2BYgaa3cyvdQoHKIBGdQ%3D",
        "resultsUrls": {
            "channel_0": "https://mystorage.blob.core.windows.net/bestor-87a0286f-304c-4636-b6bd-b3a96166df28/TranscriptionData/24265e4c-e459-4384-b572-5e3e7795221f?sv=2017-04-17&sr=b&sig=IY2qd%2Fkgtz2PwRe2C88BphH4Hv%2F1VCb1UVJ33xsw%2BEY%3D&se=2018-04-23T14:48:24Z&sp=r"
        },
        "statusMessage": "None.",
        "id": "0bb95356-ff06-469d-acc7-81f9144a269a",
        "createdDateTime": "2018-04-20T14:11:57.167",
        "lastActionDateTime": "2018-04-20T14:12:54.643",
        "status": "Succeeded",
        "locale": "en-US"
    },
```

> [!NOTE]
> <span data-ttu-id="9c29a-126">The Batch transcription API is using a REST service for requesting transcriptions, their status, and associated results.</span><span class="sxs-lookup"><span data-stu-id="9c29a-126">The Batch transcription API is using a REST service for requesting transcriptions, their status, and associated results.</span></span> <span data-ttu-id="9c29a-127">You can use the API from any language.</span><span class="sxs-lookup"><span data-stu-id="9c29a-127">You can use the API from any language.</span></span> <span data-ttu-id="9c29a-128">The next section describes how it is used.</span><span class="sxs-lookup"><span data-stu-id="9c29a-128">The next section describes how it is used.</span></span>

## <a name="authorization-token"></a><span data-ttu-id="9c29a-129">Authorization token</span><span class="sxs-lookup"><span data-stu-id="9c29a-129">Authorization token</span></span>

<span data-ttu-id="9c29a-130">As with all features of the Unified Speech Service, you create a subscription key from the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9c29a-130">As with all features of the Unified Speech Service, you create a subscription key from the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="9c29a-131">In addition, you acquire an API key from the Speech portal:</span><span class="sxs-lookup"><span data-stu-id="9c29a-131">In addition, you acquire an API key from the Speech portal:</span></span> 

1. <span data-ttu-id="9c29a-132">Sign in to [Custom Speech](https://customspeech.ai).</span><span class="sxs-lookup"><span data-stu-id="9c29a-132">Sign in to [Custom Speech](https://customspeech.ai).</span></span>

2. <span data-ttu-id="9c29a-133">Select **Subscriptions**.</span><span class="sxs-lookup"><span data-stu-id="9c29a-133">Select **Subscriptions**.</span></span>

3. <span data-ttu-id="9c29a-134">Select **Generate API Key**.</span><span class="sxs-lookup"><span data-stu-id="9c29a-134">Select **Generate API Key**.</span></span>

    ![Screenshot of Custom Speech Subscriptions page](media/stt/Subscriptions.jpg)

4. <span data-ttu-id="9c29a-136">Copy and paste that key in the client code in the following sample.</span><span class="sxs-lookup"><span data-stu-id="9c29a-136">Copy and paste that key in the client code in the following sample.</span></span>

> [!NOTE]
> <span data-ttu-id="9c29a-137">If you plan to use a custom model, you will need the ID of that model too.</span><span class="sxs-lookup"><span data-stu-id="9c29a-137">If you plan to use a custom model, you will need the ID of that model too.</span></span> <span data-ttu-id="9c29a-138">Note that this is not the deployment or endpoint ID that you find on the Endpoint Details view.</span><span class="sxs-lookup"><span data-stu-id="9c29a-138">Note that this is not the deployment or endpoint ID that you find on the Endpoint Details view.</span></span> <span data-ttu-id="9c29a-139">It is the model ID that you can retrieve when you select the details of that model.</span><span class="sxs-lookup"><span data-stu-id="9c29a-139">It is the model ID that you can retrieve when you select the details of that model.</span></span>

## <a name="sample-code"></a><span data-ttu-id="9c29a-140">Sample code</span><span class="sxs-lookup"><span data-stu-id="9c29a-140">Sample code</span></span>

<span data-ttu-id="9c29a-141">Customize the following sample code with a subscription key and an API key.</span><span class="sxs-lookup"><span data-stu-id="9c29a-141">Customize the following sample code with a subscription key and an API key.</span></span> <span data-ttu-id="9c29a-142">This allows you to obtain a bearer token.</span><span class="sxs-lookup"><span data-stu-id="9c29a-142">This allows you to obtain a bearer token.</span></span>

```cs
    public static async Task<CrisClient> CreateApiV1ClientAsync(string username, string key, string hostName, int port)
        {
            var client = new HttpClient();
            client.Timeout = TimeSpan.FromMinutes(25);
            client.BaseAddress = new UriBuilder(Uri.UriSchemeHttps, hostName, port).Uri;

            var tokenProviderPath = "/oauth/ctoken";
            var clientToken = await CreateClientTokenAsync(client, hostName, port, tokenProviderPath, username, key).ConfigureAwait(false);
            client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("bearer", clientToken.AccessToken);

            return new CrisClient(client);
        }
```

<span data-ttu-id="9c29a-143">After you obtain the token, you must specify the SAS URI pointing to the audio file requiring transcription.</span><span class="sxs-lookup"><span data-stu-id="9c29a-143">After you obtain the token, you must specify the SAS URI pointing to the audio file requiring transcription.</span></span> <span data-ttu-id="9c29a-144">The rest of the code iterates through the status and displays results.</span><span class="sxs-lookup"><span data-stu-id="9c29a-144">The rest of the code iterates through the status and displays results.</span></span>

```cs
   static async Task TranscribeAsync()
        { 
            private const string SubscriptionKey = "<your Speech[Preview] subscription key>";
            private const string HostName = "cris.ai";
            private const int Port = 443;
    
            // Creating a Batch transcription API Client
            var client = CrisClient.CreateApiV2Client(SubscriptionKey, HostName, Port);
            
            var transcriptions = await client.GetTranscriptionAsync().ConfigureAwait(false);

            var transcriptionLocation = await client.PostTranscriptionAsync(Name, Description, Locale, new Uri(RecordingsBlobUri), new[] { AdaptedAcousticId, AdaptedLanguageId }).ConfigureAwait(false);

            // get the transcription Id from the location URI
            var createdTranscriptions = new List<Guid>();
            createdTranscriptions.Add(new Guid(transcriptionLocation.ToString().Split('/').LastOrDefault()))

            while (true)
            {
                // get all transcriptions for the user
                transcriptions = await client.GetTranscriptionAsync().ConfigureAwait(false);
                completed = 0; running = 0; notStarted = 0;

                // for each transcription in the list we check the status
                foreach (var transcription in transcriptions)
                {
                    switch(transcription.Status)
                    {
                        case "Failed":
                        case "Succeeded":

                            // we check to see if it was one of the transcriptions we created from this client.
                            if (!createdTranscriptions.Contains(transcription.Id))
                            {
                                // not creted form here, continue
                                continue;
                            }
                            
                            completed++;
                            
                            // if the transcription was successfull, check the results
                            if (transcription.Status == "Succeeded")
                            {
                                var resultsUri = transcription.ResultsUrls["channel_0"];
                                WebClient webClient = new WebClient();
                                var filename = Path.GetTempFileName();
                                webClient.DownloadFile(resultsUri, filename);
                                var results = File.ReadAllText(filename);
                                Console.WriteLine("Transcription succedded. Results: ");
                                Console.WriteLine(results);
                            }
                            break;
                        case "Running":
                            running++;
                            break;
                        case "NotStarted":
                            notStarted++;
                            break;
                    }
                }

                Console.WriteLine(string.Format("Transcriptions status: {0} completed, {1} running, {2} not started yet", completed, running, notStarted));

                await Task.Delay(TimeSpan.FromSeconds(5)).ConfigureAwait(false);
            }

            Console.WriteLine("Press any key...");
        }
```

> [!NOTE]
> <span data-ttu-id="9c29a-145">In the preceding code, the subscription key is from the Speech(Preview) resource that you create on the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="9c29a-145">In the preceding code, the subscription key is from the Speech(Preview) resource that you create on the Azure portal.</span></span> <span data-ttu-id="9c29a-146">Keys obtained from the Custom Speech Service resource do not work.</span><span class="sxs-lookup"><span data-stu-id="9c29a-146">Keys obtained from the Custom Speech Service resource do not work.</span></span>

<span data-ttu-id="9c29a-147">Notice the asynchronous setup for posting audio and receiving transcription status.</span><span class="sxs-lookup"><span data-stu-id="9c29a-147">Notice the asynchronous setup for posting audio and receiving transcription status.</span></span> <span data-ttu-id="9c29a-148">The client created is a .NET Http client.</span><span class="sxs-lookup"><span data-stu-id="9c29a-148">The client created is a .NET Http client.</span></span> <span data-ttu-id="9c29a-149">There is a `PostTranscriptions` method for sending the audio file details, and a `GetTranscriptions` method to receive the results.</span><span class="sxs-lookup"><span data-stu-id="9c29a-149">There is a `PostTranscriptions` method for sending the audio file details, and a `GetTranscriptions` method to receive the results.</span></span> <span data-ttu-id="9c29a-150">`PostTranscriptions` returns a handle, and  `GetTranscriptions` uses this handle to create a handle to obtain the transcription status.</span><span class="sxs-lookup"><span data-stu-id="9c29a-150">`PostTranscriptions` returns a handle, and  `GetTranscriptions` uses this handle to create a handle to obtain the transcription status.</span></span>

<span data-ttu-id="9c29a-151">The current sample code does not specify any custom models.</span><span class="sxs-lookup"><span data-stu-id="9c29a-151">The current sample code does not specify any custom models.</span></span> <span data-ttu-id="9c29a-152">The service uses the baseline models for transcribing the file or files.</span><span class="sxs-lookup"><span data-stu-id="9c29a-152">The service uses the baseline models for transcribing the file or files.</span></span> <span data-ttu-id="9c29a-153">To specify the models, you can pass on the same method the model IDs for the acoustic and the language model.</span><span class="sxs-lookup"><span data-stu-id="9c29a-153">To specify the models, you can pass on the same method the model IDs for the acoustic and the language model.</span></span> 

<span data-ttu-id="9c29a-154">If you don't want to use the baseline, you must pass model Ids for both acoustic and language models.</span><span class="sxs-lookup"><span data-stu-id="9c29a-154">If you don't want to use the baseline, you must pass model Ids for both acoustic and language models.</span></span>

> [!NOTE]
> <span data-ttu-id="9c29a-155">For baseline transcription, you don't have to declare the endpoints of the baseline models.</span><span class="sxs-lookup"><span data-stu-id="9c29a-155">For baseline transcription, you don't have to declare the endpoints of the baseline models.</span></span> <span data-ttu-id="9c29a-156">If you want to use custom models, you provide their endpoints IDs as the [Sample](https://github.com/PanosPeriorellis/Speech_Service-BatchTranscriptionAPI).</span><span class="sxs-lookup"><span data-stu-id="9c29a-156">If you want to use custom models, you provide their endpoints IDs as the [Sample](https://github.com/PanosPeriorellis/Speech_Service-BatchTranscriptionAPI).</span></span> <span data-ttu-id="9c29a-157">If you want to use an acoustic baseline with a baseline language model, you only have to declare the custom model's endpoint ID.</span><span class="sxs-lookup"><span data-stu-id="9c29a-157">If you want to use an acoustic baseline with a baseline language model, you only have to declare the custom model's endpoint ID.</span></span> <span data-ttu-id="9c29a-158">Microsoft detects the partner baseline model (be it acoustic or language), and uses that to fulfill the transcription request.</span><span class="sxs-lookup"><span data-stu-id="9c29a-158">Microsoft detects the partner baseline model (be it acoustic or language), and uses that to fulfill the transcription request.</span></span>

### <a name="supported-storage"></a><span data-ttu-id="9c29a-159">Supported storage</span><span class="sxs-lookup"><span data-stu-id="9c29a-159">Supported storage</span></span>

<span data-ttu-id="9c29a-160">Currently the only storage supported is Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="9c29a-160">Currently the only storage supported is Azure Blob storage.</span></span>

## <a name="downloading-the-sample"></a><span data-ttu-id="9c29a-161">Downloading the sample</span><span class="sxs-lookup"><span data-stu-id="9c29a-161">Downloading the sample</span></span>

<span data-ttu-id="9c29a-162">The sample shown here is on [GitHub](https://github.com/PanosPeriorellis/Speech_Service-BatchTranscriptionAPI).</span><span class="sxs-lookup"><span data-stu-id="9c29a-162">The sample shown here is on [GitHub](https://github.com/PanosPeriorellis/Speech_Service-BatchTranscriptionAPI).</span></span>

> [!NOTE]
> <span data-ttu-id="9c29a-163">Typically, an audio transcription requires a time span equal to the duration of the audio file, plus a 2-3 minute overhead.</span><span class="sxs-lookup"><span data-stu-id="9c29a-163">Typically, an audio transcription requires a time span equal to the duration of the audio file, plus a 2-3 minute overhead.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9c29a-164">Next steps</span><span class="sxs-lookup"><span data-stu-id="9c29a-164">Next steps</span></span>

* [<span data-ttu-id="9c29a-165">Get your Speech trial subscription</span><span class="sxs-lookup"><span data-stu-id="9c29a-165">Get your Speech trial subscription</span></span>](https://azure.microsoft.com/try/cognitive-services/)
