---
title: Upload and index your videos with Azure Video Indexer | Microsoft Docs
description: This topic demonstrates how to use APIs to upload and index your videos with Azure Video Indexer
services: cognitive services
documentationcenter: ''
author: juliako
manager: erikre
ms.service: cognitive-services
ms.topic: article
ms.date: 08/17/2018
ms.author: juliako
ms.openlocfilehash: ac9d3f8fd10a3b65a2af2999b8c7ade7965de912
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868855"
---
# <a name="upload-and-index-your-videos"></a><span data-ttu-id="ace95-103">Upload and index your videos</span><span class="sxs-lookup"><span data-stu-id="ace95-103">Upload and index your videos</span></span>  

<span data-ttu-id="ace95-104">This article shows how to upload a video with Azure Video Indexer.</span><span class="sxs-lookup"><span data-stu-id="ace95-104">This article shows how to upload a video with Azure Video Indexer.</span></span> <span data-ttu-id="ace95-105">The Video Indexer API provides two uploading options:</span><span class="sxs-lookup"><span data-stu-id="ace95-105">The Video Indexer API provides two uploading options:</span></span> 

* <span data-ttu-id="ace95-106">upload your video from a URL (preferred),</span><span class="sxs-lookup"><span data-stu-id="ace95-106">upload your video from a URL (preferred),</span></span>
* <span data-ttu-id="ace95-107">send the video file as a byte array in the request body.</span><span class="sxs-lookup"><span data-stu-id="ace95-107">send the video file as a byte array in the request body.</span></span>

<span data-ttu-id="ace95-108">The article shows how to use the [Upload video](https://api-portal.videoindexer.ai/docs/services/operations/operations/Upload-video?) API to upload and index your videos based on a URL.</span><span class="sxs-lookup"><span data-stu-id="ace95-108">The article shows how to use the [Upload video](https://api-portal.videoindexer.ai/docs/services/operations/operations/Upload-video?) API to upload and index your videos based on a URL.</span></span> <span data-ttu-id="ace95-109">The code sample in the article includes the commented out code that shows how to upload the byte array.</span><span class="sxs-lookup"><span data-stu-id="ace95-109">The code sample in the article includes the commented out code that shows how to upload the byte array.</span></span>  

<span data-ttu-id="ace95-110">The article also discusses some of the parameters that you can set on the API to change the process and output of the API.</span><span class="sxs-lookup"><span data-stu-id="ace95-110">The article also discusses some of the parameters that you can set on the API to change the process and output of the API.</span></span>

> [!Note]
> <span data-ttu-id="ace95-111">When creating a Video Indexer account, you can choose a free trial account (where you get a certain number of free indexing minutes) or a paid option (where you are not limited by the quota).</span><span class="sxs-lookup"><span data-stu-id="ace95-111">When creating a Video Indexer account, you can choose a free trial account (where you get a certain number of free indexing minutes) or a paid option (where you are not limited by the quota).</span></span> <br/><span data-ttu-id="ace95-112">With free trial, Video Indexer provides up to 600 minutes of free indexing to website users and up to 2400 minutes of free indexing to API users.</span><span class="sxs-lookup"><span data-stu-id="ace95-112">With free trial, Video Indexer provides up to 600 minutes of free indexing to website users and up to 2400 minutes of free indexing to API users.</span></span> <span data-ttu-id="ace95-113">With paid option, you create a Video Indexer account that is [connected to your Azure subscription and a Azure Media Services account](connect-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="ace95-113">With paid option, you create a Video Indexer account that is [connected to your Azure subscription and a Azure Media Services account](connect-to-azure.md).</span></span> <span data-ttu-id="ace95-114">You pay for minutes indexed as well as the Media Account related charges.</span><span class="sxs-lookup"><span data-stu-id="ace95-114">You pay for minutes indexed as well as the Media Account related charges.</span></span> 

## <a name="uploading-considerations"></a><span data-ttu-id="ace95-115">Uploading considerations</span><span class="sxs-lookup"><span data-stu-id="ace95-115">Uploading considerations</span></span>
    
- <span data-ttu-id="ace95-116">When uploading your video based on the URL (preferred) the endpoint must be secured with TLS 1.2 (or higher)</span><span class="sxs-lookup"><span data-stu-id="ace95-116">When uploading your video based on the URL (preferred) the endpoint must be secured with TLS 1.2 (or higher)</span></span>
- <span data-ttu-id="ace95-117">The byte array option is limited to 4GB and times out after 30 min</span><span class="sxs-lookup"><span data-stu-id="ace95-117">The byte array option is limited to 4GB and times out after 30 min</span></span>
- <span data-ttu-id="ace95-118">The URL provided in the `videoURL` param needs to be encoded</span><span class="sxs-lookup"><span data-stu-id="ace95-118">The URL provided in the `videoURL` param needs to be encoded</span></span>

## <a name="configurations-and-params"></a><span data-ttu-id="ace95-119">Configurations and params</span><span class="sxs-lookup"><span data-stu-id="ace95-119">Configurations and params</span></span>

<span data-ttu-id="ace95-120">This section describes some of the optional parameters and when you would want to set them.</span><span class="sxs-lookup"><span data-stu-id="ace95-120">This section describes some of the optional parameters and when you would want to set them.</span></span>

### <a name="externalid"></a><span data-ttu-id="ace95-121">externalID</span><span class="sxs-lookup"><span data-stu-id="ace95-121">externalID</span></span> 

<span data-ttu-id="ace95-122">This parameter enables you to specify an ID that will be associated with the video.</span><span class="sxs-lookup"><span data-stu-id="ace95-122">This parameter enables you to specify an ID that will be associated with the video.</span></span> <span data-ttu-id="ace95-123">The ID can be applied to external "Video Content Management" (VCM) system integration.</span><span class="sxs-lookup"><span data-stu-id="ace95-123">The ID can be applied to external "Video Content Management" (VCM) system integration.</span></span> <span data-ttu-id="ace95-124">The videos that are located in the Video Indexer portal can be searched using the specified external ID.</span><span class="sxs-lookup"><span data-stu-id="ace95-124">The videos that are located in the Video Indexer portal can be searched using the specified external ID.</span></span>

### <a name="indexingpreset"></a><span data-ttu-id="ace95-125">indexingPreset</span><span class="sxs-lookup"><span data-stu-id="ace95-125">indexingPreset</span></span>

<span data-ttu-id="ace95-126">Use this parameter if raw or external recordings contain background noise.</span><span class="sxs-lookup"><span data-stu-id="ace95-126">Use this parameter if raw or external recordings contain background noise.</span></span> <span data-ttu-id="ace95-127">This parameter is used to configure the indexing process.</span><span class="sxs-lookup"><span data-stu-id="ace95-127">This parameter is used to configure the indexing process.</span></span> <span data-ttu-id="ace95-128">You can specify the following values:</span><span class="sxs-lookup"><span data-stu-id="ace95-128">You can specify the following values:</span></span>

- <span data-ttu-id="ace95-129">`Default` – Index and extract insights using both audio and video</span><span class="sxs-lookup"><span data-stu-id="ace95-129">`Default` – Index and extract insights using both audio and video</span></span>
- <span data-ttu-id="ace95-130">`AudioOnly` – Index and extract insights using audio only (ignoring video)</span><span class="sxs-lookup"><span data-stu-id="ace95-130">`AudioOnly` – Index and extract insights using audio only (ignoring video)</span></span>
- <span data-ttu-id="ace95-131">`DefaultWithNoiseReduction` – Index and extract insights from both audio and video, while applying noise reduction algorithms on audio stream</span><span class="sxs-lookup"><span data-stu-id="ace95-131">`DefaultWithNoiseReduction` – Index and extract insights from both audio and video, while applying noise reduction algorithms on audio stream</span></span>

<span data-ttu-id="ace95-132">Price depends on the selected indexing option.</span><span class="sxs-lookup"><span data-stu-id="ace95-132">Price depends on the selected indexing option.</span></span>  

### <a name="callbackurl"></a><span data-ttu-id="ace95-133">callbackUrl</span><span class="sxs-lookup"><span data-stu-id="ace95-133">callbackUrl</span></span>

<span data-ttu-id="ace95-134">A POST URL to notify when indexing is completed.</span><span class="sxs-lookup"><span data-stu-id="ace95-134">A POST URL to notify when indexing is completed.</span></span> <span data-ttu-id="ace95-135">Video Indexer adds two query string parameters to it: id and state.</span><span class="sxs-lookup"><span data-stu-id="ace95-135">Video Indexer adds two query string parameters to it: id and state.</span></span> <span data-ttu-id="ace95-136">For example, if the callback url is 'https://test.com/notifyme?projectName=MyProject', the notification will be sent with additional parameters to 'https://test.com/notifyme?projectName=MyProject&id=1234abcd&state=Processed'.</span><span class="sxs-lookup"><span data-stu-id="ace95-136">For example, if the callback url is 'https://test.com/notifyme?projectName=MyProject', the notification will be sent with additional parameters to 'https://test.com/notifyme?projectName=MyProject&id=1234abcd&state=Processed'.</span></span>

<span data-ttu-id="ace95-137">You can also add more parameters to the URL before POSTing the call to Video Indexer and these parameters will be included in the callback.</span><span class="sxs-lookup"><span data-stu-id="ace95-137">You can also add more parameters to the URL before POSTing the call to Video Indexer and these parameters will be included in the callback.</span></span> <span data-ttu-id="ace95-138">Later, in your code you can parse the query string and get back all of the specified parameters in the query string (data that you had originally appended to the URL plus the Video Indexer supplied info.) The URL needs to be encoded.</span><span class="sxs-lookup"><span data-stu-id="ace95-138">Later, in your code you can parse the query string and get back all of the specified parameters in the query string (data that you had originally appended to the URL plus the Video Indexer supplied info.) The URL needs to be encoded.</span></span>

### <a name="streamingpreset"></a><span data-ttu-id="ace95-139">streamingPreset</span><span class="sxs-lookup"><span data-stu-id="ace95-139">streamingPreset</span></span>

<span data-ttu-id="ace95-140">Once your video has been uploaded, Video Indexer, optionally encodes the video.</span><span class="sxs-lookup"><span data-stu-id="ace95-140">Once your video has been uploaded, Video Indexer, optionally encodes the video.</span></span> <span data-ttu-id="ace95-141">Then, proceeds to indexing, and analyzing the video.</span><span class="sxs-lookup"><span data-stu-id="ace95-141">Then, proceeds to indexing, and analyzing the video.</span></span> <span data-ttu-id="ace95-142">When Video Indexer is done analyzing, you will get a notification with the video ID.</span><span class="sxs-lookup"><span data-stu-id="ace95-142">When Video Indexer is done analyzing, you will get a notification with the video ID.</span></span>  

<span data-ttu-id="ace95-143">When using the [Upload video](https://api-portal.videoindexer.ai/docs/services/operations/operations/Upload-video?) or [Re-Index Video](https://api-portal.videoindexer.ai/docs/services/operations/operations/Re-index-video?) API, one of the optional parameters is `streamingPreset`.</span><span class="sxs-lookup"><span data-stu-id="ace95-143">When using the [Upload video](https://api-portal.videoindexer.ai/docs/services/operations/operations/Upload-video?) or [Re-Index Video](https://api-portal.videoindexer.ai/docs/services/operations/operations/Re-index-video?) API, one of the optional parameters is `streamingPreset`.</span></span> <span data-ttu-id="ace95-144">If you set `streamingPreset` to `Default`, `SingleBitrate`, or `AdaptiveBitrate`, the encoding process is triggered.</span><span class="sxs-lookup"><span data-stu-id="ace95-144">If you set `streamingPreset` to `Default`, `SingleBitrate`, or `AdaptiveBitrate`, the encoding process is triggered.</span></span> <span data-ttu-id="ace95-145">Once the indexing and encoding jobs are done, the video is published so you can also stream your video.</span><span class="sxs-lookup"><span data-stu-id="ace95-145">Once the indexing and encoding jobs are done, the video is published so you can also stream your video.</span></span> <span data-ttu-id="ace95-146">The Streaming Endpoint from which you want to stream the video must be in the **Running** state.</span><span class="sxs-lookup"><span data-stu-id="ace95-146">The Streaming Endpoint from which you want to stream the video must be in the **Running** state.</span></span>

<span data-ttu-id="ace95-147">In order to run the indexing and encoding jobs, the [Azure Media Services account connected to your Video Indexer account](connect-to-azure.md), requires Reserved Units.</span><span class="sxs-lookup"><span data-stu-id="ace95-147">In order to run the indexing and encoding jobs, the [Azure Media Services account connected to your Video Indexer account](connect-to-azure.md), requires Reserved Units.</span></span> <span data-ttu-id="ace95-148">For more information, see [Scaling Media Processing](https://docs.microsoft.com/azure/media-services/previous/media-services-scale-media-processing-overview).</span><span class="sxs-lookup"><span data-stu-id="ace95-148">For more information, see [Scaling Media Processing](https://docs.microsoft.com/azure/media-services/previous/media-services-scale-media-processing-overview).</span></span> <span data-ttu-id="ace95-149">Since these are compute intensive jobs, S3 unit type is highly recommended.</span><span class="sxs-lookup"><span data-stu-id="ace95-149">Since these are compute intensive jobs, S3 unit type is highly recommended.</span></span> <span data-ttu-id="ace95-150">The number of RUs defines the max number of jobs that can run in parallel.</span><span class="sxs-lookup"><span data-stu-id="ace95-150">The number of RUs defines the max number of jobs that can run in parallel.</span></span> <span data-ttu-id="ace95-151">The baseline recommendation is 10 S3 RUs.</span><span class="sxs-lookup"><span data-stu-id="ace95-151">The baseline recommendation is 10 S3 RUs.</span></span> 

<span data-ttu-id="ace95-152">If you only want to index your video but not encode it, set `streamingPreset`to `NoStreaming`.</span><span class="sxs-lookup"><span data-stu-id="ace95-152">If you only want to index your video but not encode it, set `streamingPreset`to `NoStreaming`.</span></span>

### <a name="videourl"></a><span data-ttu-id="ace95-153">videoUrl</span><span class="sxs-lookup"><span data-stu-id="ace95-153">videoUrl</span></span>

<span data-ttu-id="ace95-154">A URL of the video/audio file to be indexed.</span><span class="sxs-lookup"><span data-stu-id="ace95-154">A URL of the video/audio file to be indexed.</span></span> <span data-ttu-id="ace95-155">The URL must point at a media file (HTML pages are not supported).</span><span class="sxs-lookup"><span data-stu-id="ace95-155">The URL must point at a media file (HTML pages are not supported).</span></span> <span data-ttu-id="ace95-156">The file can be protected by an access token provided as part of the URI and the endpoint serving the file must be secured with TLS 1.2 or higher.</span><span class="sxs-lookup"><span data-stu-id="ace95-156">The file can be protected by an access token provided as part of the URI and the endpoint serving the file must be secured with TLS 1.2 or higher.</span></span> <span data-ttu-id="ace95-157">The URL needs to be encoded.</span><span class="sxs-lookup"><span data-stu-id="ace95-157">The URL needs to be encoded.</span></span> 

<span data-ttu-id="ace95-158">If the `videoUrl` is not specified, the Video Indexer expects you to pass the file as a multipart/form body content.</span><span class="sxs-lookup"><span data-stu-id="ace95-158">If the `videoUrl` is not specified, the Video Indexer expects you to pass the file as a multipart/form body content.</span></span>

## <a name="code-sample"></a><span data-ttu-id="ace95-159">Code sample</span><span class="sxs-lookup"><span data-stu-id="ace95-159">Code sample</span></span>

<span data-ttu-id="ace95-160">The following C# code snippet demonstrates the usage of all the Video Indexer APIs together.</span><span class="sxs-lookup"><span data-stu-id="ace95-160">The following C# code snippet demonstrates the usage of all the Video Indexer APIs together.</span></span>

```csharp
public async Task Sample()
{
    var apiUrl = "https://api.videoindexer.ai";
    var location = "westus2";
    var apiKey = "...";

    System.Net.ServicePointManager.SecurityProtocol =
        System.Net.ServicePointManager.SecurityProtocol | System.Net.SecurityProtocolType.Tls12;

    // create the http client
    var handler = new HttpClientHandler();
    handler.AllowAutoRedirect = false;
    var client = new HttpClient(handler);
    client.DefaultRequestHeaders.Add("Ocp-Apim-Subscription-Key", apiKey);

    // obtain account information and access token
    string queryParams = CreateQueryString(
        new Dictionary<string, string>()
        {
            {"generateAccessTokens", "true"},
            {"allowEdit", "true"},
        });
    HttpResponseMessage result = await client.GetAsync($"{apiUrl}/auth/trial/Accounts?{queryParams}");
    var json = await result.Content.ReadAsStringAsync();
    var accounts = JsonConvert.DeserializeObject<AccountContractSlim[]>(json);
    // take the relevant account, here we simply take the first
    var accountInfo = accounts.First();

    // we will use the access token from here on, no need for the apim key
    client.DefaultRequestHeaders.Remove("Ocp-Apim-Subscription-Key");

    // upload a video
    var content = new MultipartFormDataContent();
    Debug.WriteLine("Uploading...");
    // get the video from URL
    var videoUrl = "VIDEO_URL"; // replace with the video URL

    // as an alternative to specifying video URL, you can upload a file.
    // remove the videoUrl parameter from the query params below and add the following lines:
    //FileStream video =File.OpenRead(Globals.VIDEOFILE_PATH);
    //byte[] buffer =newbyte[video.Length];
    //video.Read(buffer, 0, buffer.Length);
    //content.Add(newByteArrayContent(buffer));

    queryParams = CreateQueryString(
        new Dictionary<string, string>()
        {
            {"accessToken", accountInfo.AccessToken},
            {"name", "video_name"},
            {"description", "video_description"},
            {"privacy", "private"},
            {"partition", "partition"},
            {"videoUrl", videoUrl},
        });
    var uploadRequestResult = await client.PostAsync($"{apiUrl}/{accountInfo.Location}/Accounts/{accountInfo.Id}/Videos?{queryParams}", content);
    var uploadResult = await uploadRequestResult.Content.ReadAsStringAsync();

    // get the video id from the upload result
    string videoId = JsonConvert.DeserializeObject<dynamic>(uploadResult)["id"];
    Debug.WriteLine("Uploaded");
    Debug.WriteLine("Video ID:");
    Debug.WriteLine(videoId);

    // wait for the video index to finish
    while (true)
    {
        await Task.Delay(10000);

        queryParams = CreateQueryString(
            new Dictionary<string, string>()
            {
                {"accessToken", accountInfo.AccessToken},
                {"language", "English"},
            });

        var videoGetIndexRequestResult = await client.GetAsync($"{apiUrl}/{accountInfo.Location}/Accounts/{accountInfo.Id}/Videos/{videoId}/Index?{queryParams}");
        var videoGetIndexResult = await videoGetIndexRequestResult.Content.ReadAsStringAsync();

        string processingState = JsonConvert.DeserializeObject<dynamic>(videoGetIndexResult)["state"];

        Debug.WriteLine("");
        Debug.WriteLine("State:");
        Debug.WriteLine(processingState);

        // job is finished
        if (processingState != "Uploaded" && processingState != "Processing")
        {
            Debug.WriteLine("");
            Debug.WriteLine("Full JSON:");
            Debug.WriteLine(videoGetIndexResult);
            break;
        }
    }

    // search for the video
    queryParams = CreateQueryString(
        new Dictionary<string, string>()
        {
            {"accessToken", accountInfo.AccessToken},
            {"id", videoId},
        });

    var searchRequestResult = await client.GetAsync($"{apiUrl}/{accountInfo.Location}/Accounts/{accountInfo.Id}/Videos/Search?{queryParams}");
    var searchResult = await searchRequestResult.Content.ReadAsStringAsync();
    Debug.WriteLine("");
    Debug.WriteLine("Search:");
    Debug.WriteLine(searchResult);

    // Generate video access token (used for get widget calls)
    client.DefaultRequestHeaders.Add("Ocp-Apim-Subscription-Key", apiKey);
    var videoTokenRequestResult = await client.GetAsync($"{apiUrl}/auth/{accountInfo.Location}/Accounts/{accountInfo.Id}/Videos/{videoId}/AccessToken?allowEdit=true");
    var videoAccessToken = (await videoTokenRequestResult.Content.ReadAsStringAsync()).Replace("\"", "");
    client.DefaultRequestHeaders.Remove("Ocp-Apim-Subscription-Key");

    // get insights widget url
    queryParams = CreateQueryString(
        new Dictionary<string, string>()
        {
            {"accessToken", videoAccessToken},
            {"widgetType", "Keywords"},
            {"allowEdit", "true"},
        });
    var insightsWidgetRequestResult = await client.GetAsync($"{apiUrl}/{accountInfo.Location}/Accounts/{accountInfo.Id}/Videos/{videoId}/InsightsWidget?{queryParams}");
    var insightsWidgetLink = insightsWidgetRequestResult.Headers.Location;
    Debug.WriteLine("Insights Widget url:");
    Debug.WriteLine(insightsWidgetLink);

    // get player widget url
    queryParams = CreateQueryString(
        new Dictionary<string, string>()
        {
            {"accessToken", videoAccessToken},
        });
    var playerWidgetRequestResult = await client.GetAsync($"{apiUrl}/{accountInfo.Location}/Accounts/{accountInfo.Id}/Videos/{videoId}/PlayerWidget?{queryParams}");
    var playerWidgetLink = playerWidgetRequestResult.Headers.Location;
    Debug.WriteLine("");
    Debug.WriteLine("Player Widget url:");
    Debug.WriteLine(playerWidgetLink);
}

private string CreateQueryString(IDictionary<string, string> parameters)
{
    var queryParameters = HttpUtility.ParseQueryString(string.Empty);
    foreach (var parameter in parameters)
    {
        queryParameters[parameter.Key] = parameter.Value;
    }

    return queryParameters.ToString();
}

public class AccountContractSlim
{
    public Guid Id { get; set; }
    public string Name { get; set; }
    public string Location { get; set; }
    public string AccountType { get; set; }
    public string Url { get; set; }
    public string AccessToken { get; set; }
}
```



## <a name="next-steps"></a><span data-ttu-id="ace95-161">Next steps</span><span class="sxs-lookup"><span data-stu-id="ace95-161">Next steps</span></span>

[<span data-ttu-id="ace95-162">Examine the Azure Video Indexer output produced by v2 API</span><span class="sxs-lookup"><span data-stu-id="ace95-162">Examine the Azure Video Indexer output produced by v2 API</span></span>](video-indexer-output-json-v2.md)
