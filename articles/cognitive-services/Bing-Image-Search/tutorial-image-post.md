---
title: Bing Image Upload for Insights | Microsoft Docs
description: Console application that uses the Bing Image Search API to upload an image and get image insights.
services: cognitive-services
author: mikedodaro
manager: rosh
ms.service: cognitive-services
ms.component: bing-image-search
ms.topic: article
ms.date: 12/07/2017
ms.author: v-gedod
ms.openlocfilehash: f0bf32a9951527a072fffe464f6b5f50d0f237a2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966584"
---
# <a name="tutorial-bing-image-upload-for-insights"></a><span data-ttu-id="2e67d-103">Tutorial: Bing image upload for insights</span><span class="sxs-lookup"><span data-stu-id="2e67d-103">Tutorial: Bing image upload for insights</span></span>

<span data-ttu-id="2e67d-104">The Bing Image Search API provides a `POST` option to upload an image and search for information pertinent to the image.</span><span class="sxs-lookup"><span data-stu-id="2e67d-104">The Bing Image Search API provides a `POST` option to upload an image and search for information pertinent to the image.</span></span> <span data-ttu-id="2e67d-105">This C# console application uploads an image using the Image Search endpoint to get details about the image.</span><span class="sxs-lookup"><span data-stu-id="2e67d-105">This C# console application uploads an image using the Image Search endpoint to get details about the image.</span></span>
<span data-ttu-id="2e67d-106">The results, briefly, are JSON objects such as the following:</span><span class="sxs-lookup"><span data-stu-id="2e67d-106">The results, briefly, are JSON objects such as the following:</span></span>

![[JSON results]](media/cognitive-services-bing-images-api/jsonResult.jpg)

<span data-ttu-id="2e67d-108">This tutorial explains how to:</span><span class="sxs-lookup"><span data-stu-id="2e67d-108">This tutorial explains how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2e67d-109">Use the Image Search `/details` endpoint in a `POST` request</span><span class="sxs-lookup"><span data-stu-id="2e67d-109">Use the Image Search `/details` endpoint in a `POST` request</span></span>
> * <span data-ttu-id="2e67d-110">Specify headers for the request</span><span class="sxs-lookup"><span data-stu-id="2e67d-110">Specify headers for the request</span></span>
> * <span data-ttu-id="2e67d-111">Use URL parameters to specify results</span><span class="sxs-lookup"><span data-stu-id="2e67d-111">Use URL parameters to specify results</span></span>
> * <span data-ttu-id="2e67d-112">Upload the image data and send the `POST` request</span><span class="sxs-lookup"><span data-stu-id="2e67d-112">Upload the image data and send the `POST` request</span></span>
> * <span data-ttu-id="2e67d-113">Print the JSON results to the console</span><span class="sxs-lookup"><span data-stu-id="2e67d-113">Print the JSON results to the console</span></span>

## <a name="app-components"></a><span data-ttu-id="2e67d-114">App components</span><span class="sxs-lookup"><span data-stu-id="2e67d-114">App components</span></span>

<span data-ttu-id="2e67d-115">The tutorial application includes three parts:</span><span class="sxs-lookup"><span data-stu-id="2e67d-115">The tutorial application includes three parts:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2e67d-116">Endpoint configuration to specify the Bing Image Search endpoint and required headers</span><span class="sxs-lookup"><span data-stu-id="2e67d-116">Endpoint configuration to specify the Bing Image Search endpoint and required headers</span></span>
> * <span data-ttu-id="2e67d-117">Image file upload for `POST` request to the endpoint</span><span class="sxs-lookup"><span data-stu-id="2e67d-117">Image file upload for `POST` request to the endpoint</span></span>
> * <span data-ttu-id="2e67d-118">Parsing the JSON results that are the details returned from the `POST` request</span><span class="sxs-lookup"><span data-stu-id="2e67d-118">Parsing the JSON results that are the details returned from the `POST` request</span></span>

## <a name="scenario-overview"></a><span data-ttu-id="2e67d-119">Scenario overview</span><span class="sxs-lookup"><span data-stu-id="2e67d-119">Scenario overview</span></span>
<span data-ttu-id="2e67d-120">There are [three Image Search endpoints](https://docs.microsoft.com/azure/cognitive-services/bing-image-search/image-search-endpoint).</span><span class="sxs-lookup"><span data-stu-id="2e67d-120">There are [three Image Search endpoints](https://docs.microsoft.com/azure/cognitive-services/bing-image-search/image-search-endpoint).</span></span> <span data-ttu-id="2e67d-121">The `/details` endpoint can use a `POST` request with image data in the body of the request.</span><span class="sxs-lookup"><span data-stu-id="2e67d-121">The `/details` endpoint can use a `POST` request with image data in the body of the request.</span></span>
```
https://api.cognitive.microsoft.com/bing/v7.0/images/details
```
<span data-ttu-id="2e67d-122">The `modules` URL parameter following `/details?` specifies what kind of details the results contain:</span><span class="sxs-lookup"><span data-stu-id="2e67d-122">The `modules` URL parameter following `/details?` specifies what kind of details the results contain:</span></span>
* `modules=All`
* <span data-ttu-id="2e67d-123">`modules=RecognizedEntities` (people or places visible in the image)</span><span class="sxs-lookup"><span data-stu-id="2e67d-123">`modules=RecognizedEntities` (people or places visible in the image)</span></span>

<span data-ttu-id="2e67d-124">Specify `modules=All` in the `POST` request to get JSON text that includes the following list:</span><span class="sxs-lookup"><span data-stu-id="2e67d-124">Specify `modules=All` in the `POST` request to get JSON text that includes the following list:</span></span>
* <span data-ttu-id="2e67d-125">`bestRepresentativeQuery` - a Bing query that returns images similar to the uploaded image</span><span class="sxs-lookup"><span data-stu-id="2e67d-125">`bestRepresentativeQuery` - a Bing query that returns images similar to the uploaded image</span></span>
* <span data-ttu-id="2e67d-126">`detectedObjects` such as a bounding box or hot spots in the image</span><span class="sxs-lookup"><span data-stu-id="2e67d-126">`detectedObjects` such as a bounding box or hot spots in the image</span></span>
* <span data-ttu-id="2e67d-127">`image` metadata</span><span class="sxs-lookup"><span data-stu-id="2e67d-127">`image` metadata</span></span>
* <span data-ttu-id="2e67d-128">`imageInsightsToken` - token for a subsequent `GET` request that gets `RecognizedEntities` (people or places visible in the image)</span><span class="sxs-lookup"><span data-stu-id="2e67d-128">`imageInsightsToken` - token for a subsequent `GET` request that gets `RecognizedEntities` (people or places visible in the image)</span></span> 
* `imageTags`
* <span data-ttu-id="2e67d-129">`pagesIncluding` - Web pages that include the image</span><span class="sxs-lookup"><span data-stu-id="2e67d-129">`pagesIncluding` - Web pages that include the image</span></span>
* `relatedSearches`
* `visuallySimilarImages`

<span data-ttu-id="2e67d-130">Specify `modules=RecognizedEntities` in the `POST` request to get only the `imageInsightsToken`, which is used in a subsequent `GET` request.</span><span class="sxs-lookup"><span data-stu-id="2e67d-130">Specify `modules=RecognizedEntities` in the `POST` request to get only the `imageInsightsToken`, which is used in a subsequent `GET` request.</span></span> <span data-ttu-id="2e67d-131">It identifies people or places visible in the image.</span><span class="sxs-lookup"><span data-stu-id="2e67d-131">It identifies people or places visible in the image.</span></span>

## <a name="webclient-and-headers-for-the-post-request"></a><span data-ttu-id="2e67d-132">WebClient and headers for the POST request</span><span class="sxs-lookup"><span data-stu-id="2e67d-132">WebClient and headers for the POST request</span></span>
<span data-ttu-id="2e67d-133">Create a `WebClient` object, and set the headers.</span><span class="sxs-lookup"><span data-stu-id="2e67d-133">Create a `WebClient` object, and set the headers.</span></span> <span data-ttu-id="2e67d-134">All requests to the Bing Search API require an `Ocp-Apim-Subscription-Key`.</span><span class="sxs-lookup"><span data-stu-id="2e67d-134">All requests to the Bing Search API require an `Ocp-Apim-Subscription-Key`.</span></span> <span data-ttu-id="2e67d-135">A `POST` request to upload an image must also specify `ContentType: multipart/form-data`.</span><span class="sxs-lookup"><span data-stu-id="2e67d-135">A `POST` request to upload an image must also specify `ContentType: multipart/form-data`.</span></span>

```
            WebClient client = new WebClient();
            client.Headers["Ocp-Apim-Subscription-Key"] = accessKey;
            client.Headers["ContentType"] = "multipart/form-data"; 
```

## <a name="upload-the-image-and-get-results"></a><span data-ttu-id="2e67d-136">Upload the image and get results</span><span class="sxs-lookup"><span data-stu-id="2e67d-136">Upload the image and get results</span></span>

<span data-ttu-id="2e67d-137">The `WebClient` class includes the `UpLoadFile` method that formats data for the `POST` request.</span><span class="sxs-lookup"><span data-stu-id="2e67d-137">The `WebClient` class includes the `UpLoadFile` method that formats data for the `POST` request.</span></span> <span data-ttu-id="2e67d-138">It formats the `RequestStream` and calls `HttpWebRequest`, avoiding a lot of complexity.</span><span class="sxs-lookup"><span data-stu-id="2e67d-138">It formats the `RequestStream` and calls `HttpWebRequest`, avoiding a lot of complexity.</span></span>
<span data-ttu-id="2e67d-139">Call `WebClient.UpLoadFile` with the `/details` endpoint and the image file to upload.</span><span class="sxs-lookup"><span data-stu-id="2e67d-139">Call `WebClient.UpLoadFile` with the `/details` endpoint and the image file to upload.</span></span> <span data-ttu-id="2e67d-140">The response is binary data that is easily converted to JSON.</span><span class="sxs-lookup"><span data-stu-id="2e67d-140">The response is binary data that is easily converted to JSON.</span></span> 

<span data-ttu-id="2e67d-141">Use the JSON text to initialize an instance of the `SearchResult` structure (see the [application source code](tutorial-image-post-source.md) for context).</span><span class="sxs-lookup"><span data-stu-id="2e67d-141">Use the JSON text to initialize an instance of the `SearchResult` structure (see the [application source code](tutorial-image-post-source.md) for context).</span></span>
```        
         const string uriBase = "https://api.cognitive.microsoft.com/bing/v7.0/images/details";

        // The image to upload. Replace with your file and path.
        const string imageFile = "ansel-adams-tetons-snake-river.jpg";
            
        byte[] resp = client.UploadFile(uriBase + "?modules=All", imageFile);
        var json = System.Text.Encoding.Default.GetString(resp);

        // Create result object for return
        var searchResult = new SearchResult()
        {
            jsonResult = json,
            relevantHeaders = new Dictionary<String, String>()
        };
```

## <a name="print-the-results"></a><span data-ttu-id="2e67d-142">Print the results</span><span class="sxs-lookup"><span data-stu-id="2e67d-142">Print the results</span></span>
<span data-ttu-id="2e67d-143">The rest of the code parses the JSON result and prints it to the console.</span><span class="sxs-lookup"><span data-stu-id="2e67d-143">The rest of the code parses the JSON result and prints it to the console.</span></span>

```
        /// <summary>
        /// Formats the given JSON string by adding line breaks and indents.
        /// </summary>
        /// <param name="json">The raw JSON string to format.</param>
        /// <returns>The formatted JSON string.</returns>
        static string JsonPrettyPrint(string json)
        {
            if (string.IsNullOrEmpty(json))
                return string.Empty;

            json = json.Replace(Environment.NewLine, "").Replace("\t", "");

            StringBuilder sb = new StringBuilder();
            bool quote = false;
            bool ignore = false;
            char last = ' ';
            int offset = 0;
            int indentLength = 2;

            foreach (char ch in json)
            {
                switch (ch)
                {
                    case '"':
                        if (!ignore) quote = !quote;
                        break;
                    case '\\':
                        if (quote && last != '\\') ignore = true;
                        break;
                }

                if (quote)
                {
                    sb.Append(ch);
                    if (last == '\\' && ignore) ignore = false;
                }
                else
                {
                    switch (ch)
                    {
                        case '{':
                        case '[':
                            sb.Append(ch);
                            sb.Append(Environment.NewLine);
                            sb.Append(new string(' ', ++offset * indentLength));
                            break;
                        case '}':
                        case ']':
                            sb.Append(Environment.NewLine);
                            sb.Append(new string(' ', --offset * indentLength));
                            sb.Append(ch);
                            break;
                        case ',':
                            sb.Append(ch);
                            sb.Append(Environment.NewLine);
                            sb.Append(new string(' ', offset * indentLength));
                            break;
                        case ':':
                            sb.Append(ch);
                            sb.Append(' ');
                            break;
                        default:
                            if (quote || ch != ' ') sb.Append(ch);
                            break;
                    }
                }
                last = ch;
            }

            return sb.ToString().Trim();
        }
```
## <a name="get-request-using-the-imageinsightstoken"></a><span data-ttu-id="2e67d-144">GET Request using the ImageInsightsToken</span><span class="sxs-lookup"><span data-stu-id="2e67d-144">GET Request using the ImageInsightsToken</span></span>
<span data-ttu-id="2e67d-145">To use the `ImageInsightsToken` returned with results of a `POST`, create a `GET` request like the following:</span><span class="sxs-lookup"><span data-stu-id="2e67d-145">To use the `ImageInsightsToken` returned with results of a `POST`, create a `GET` request like the following:</span></span>
```
https://api.cognitive.microsoft.com/bing/v7.0/images/details?InsightsToken="bcid_A2C4BB81AA2C9EF8E049C5933C546449*ccid_osS7gaos*mid_BF7CC4FC4A882A3C3D56E644685BFF7B8BACEAF2
```
<span data-ttu-id="2e67d-146">If there are identifiable people or places in the image, this request will return information about them.</span><span class="sxs-lookup"><span data-stu-id="2e67d-146">If there are identifiable people or places in the image, this request will return information about them.</span></span>
<span data-ttu-id="2e67d-147">The [Quickstarts](https://docs.microsoft.com/azure/cognitive-services/bing-image-search) contain numerous code examples.</span><span class="sxs-lookup"><span data-stu-id="2e67d-147">The [Quickstarts](https://docs.microsoft.com/azure/cognitive-services/bing-image-search) contain numerous code examples.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2e67d-148">Next steps</span><span class="sxs-lookup"><span data-stu-id="2e67d-148">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2e67d-149">Bing Image Search API reference</span><span class="sxs-lookup"><span data-stu-id="2e67d-149">Bing Image Search API reference</span></span>](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference)

