---
title: Call the Text Analytics API (Microsoft Cognitive Services on Azure) | Microsoft Docs
description: Learn how to call the Text Analytics REST API.
services: cognitive-services
author: ashmaka
manager: cgronlun
ms.service: cognitive-services
ms.technology: text-analytics
ms.topic: get-started-article
ms.date: 05/02/2018
ms.author: ashmaka
ms.openlocfilehash: abdcb080baf60442232d6c86bd8ae35d80ae35af
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868468"
---
# <a name="how-to-call-the-text-analytics-rest-api"></a><span data-ttu-id="6434d-103">How to call the Text Analytics REST API</span><span class="sxs-lookup"><span data-stu-id="6434d-103">How to call the Text Analytics REST API</span></span>

<span data-ttu-id="6434d-104">Calls to the **Text Analytics API** are HTTP POST/GET calls, which you can formulate in any language.</span><span class="sxs-lookup"><span data-stu-id="6434d-104">Calls to the **Text Analytics API** are HTTP POST/GET calls, which you can formulate in any language.</span></span> <span data-ttu-id="6434d-105">In this article, we use REST and [Postman](https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop) to demonstrate key concepts.</span><span class="sxs-lookup"><span data-stu-id="6434d-105">In this article, we use REST and [Postman](https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop) to demonstrate key concepts.</span></span>

<span data-ttu-id="6434d-106">Each request must include your access key and an HTTP endpoint.</span><span class="sxs-lookup"><span data-stu-id="6434d-106">Each request must include your access key and an HTTP endpoint.</span></span> <span data-ttu-id="6434d-107">The endpoint specifies the region you chose during sign up, the service URL, and a resource used on the request: `sentiment`, `keyphrases`, `languages`, and `entities`.</span><span class="sxs-lookup"><span data-stu-id="6434d-107">The endpoint specifies the region you chose during sign up, the service URL, and a resource used on the request: `sentiment`, `keyphrases`, `languages`, and `entities`.</span></span> 

<span data-ttu-id="6434d-108">Recall that Text Analytics is stateless so there are no data assets to manage.</span><span class="sxs-lookup"><span data-stu-id="6434d-108">Recall that Text Analytics is stateless so there are no data assets to manage.</span></span> <span data-ttu-id="6434d-109">Your text is uploaded, analyzed upon receipt, and results are returned immediately to the calling application.</span><span class="sxs-lookup"><span data-stu-id="6434d-109">Your text is uploaded, analyzed upon receipt, and results are returned immediately to the calling application.</span></span>

> [!Tip]
> <span data-ttu-id="6434d-110">For one-off calls to see how the API works, you can send POST requests from the built-in **API testing console**, available on any [API doc page](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/56f30ceeeda5650db055a3c6).</span><span class="sxs-lookup"><span data-stu-id="6434d-110">For one-off calls to see how the API works, you can send POST requests from the built-in **API testing console**, available on any [API doc page](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/56f30ceeeda5650db055a3c6).</span></span> <span data-ttu-id="6434d-111">There is no setup, and the only requirements are to paste an access key and the JSON documents into the request.</span><span class="sxs-lookup"><span data-stu-id="6434d-111">There is no setup, and the only requirements are to paste an access key and the JSON documents into the request.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="6434d-112">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="6434d-112">Prerequisites</span></span>

<span data-ttu-id="6434d-113">You must have a [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) with **Text Analytics API**.</span><span class="sxs-lookup"><span data-stu-id="6434d-113">You must have a [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) with **Text Analytics API**.</span></span> 

<span data-ttu-id="6434d-114">You must have the [endpoint and access key](text-analytics-how-to-access-key.md) that is generated for you when you sign up for Cognitive Services.</span><span class="sxs-lookup"><span data-stu-id="6434d-114">You must have the [endpoint and access key](text-analytics-how-to-access-key.md) that is generated for you when you sign up for Cognitive Services.</span></span> 

<a name="json-schema"></a>

## <a name="json-schema-definition"></a><span data-ttu-id="6434d-115">JSON schema definition</span><span class="sxs-lookup"><span data-stu-id="6434d-115">JSON schema definition</span></span>

<span data-ttu-id="6434d-116">Input must be JSON in raw unstructured text.</span><span class="sxs-lookup"><span data-stu-id="6434d-116">Input must be JSON in raw unstructured text.</span></span> <span data-ttu-id="6434d-117">XML is not supported.</span><span class="sxs-lookup"><span data-stu-id="6434d-117">XML is not supported.</span></span> <span data-ttu-id="6434d-118">The schema is simple, consisting of the elements described in the following list.</span><span class="sxs-lookup"><span data-stu-id="6434d-118">The schema is simple, consisting of the elements described in the following list.</span></span> 

<span data-ttu-id="6434d-119">You can currently submit the same documents for all Text Analytics operations: sentiment, key phrase, language detection, and entity linking.</span><span class="sxs-lookup"><span data-stu-id="6434d-119">You can currently submit the same documents for all Text Analytics operations: sentiment, key phrase, language detection, and entity linking.</span></span> <span data-ttu-id="6434d-120">(The schema is likely to vary for each analysis in the future.)</span><span class="sxs-lookup"><span data-stu-id="6434d-120">(The schema is likely to vary for each analysis in the future.)</span></span>

| <span data-ttu-id="6434d-121">Element</span><span class="sxs-lookup"><span data-stu-id="6434d-121">Element</span></span> | <span data-ttu-id="6434d-122">Valid values</span><span class="sxs-lookup"><span data-stu-id="6434d-122">Valid values</span></span> | <span data-ttu-id="6434d-123">Required?</span><span class="sxs-lookup"><span data-stu-id="6434d-123">Required?</span></span> | <span data-ttu-id="6434d-124">Usage</span><span class="sxs-lookup"><span data-stu-id="6434d-124">Usage</span></span> |
|---------|--------------|-----------|-------|
|`id` |<span data-ttu-id="6434d-125">The data type is string, but in practice document IDs tend to be integers.</span><span class="sxs-lookup"><span data-stu-id="6434d-125">The data type is string, but in practice document IDs tend to be integers.</span></span> | <span data-ttu-id="6434d-126">Required</span><span class="sxs-lookup"><span data-stu-id="6434d-126">Required</span></span> | <span data-ttu-id="6434d-127">The system uses the IDs you provide to structure the output.</span><span class="sxs-lookup"><span data-stu-id="6434d-127">The system uses the IDs you provide to structure the output.</span></span> <span data-ttu-id="6434d-128">Language codes, key phrases, and sentiment scores are generated for each ID in the request.</span><span class="sxs-lookup"><span data-stu-id="6434d-128">Language codes, key phrases, and sentiment scores are generated for each ID in the request.</span></span>|
|`text` | <span data-ttu-id="6434d-129">Unstructured raw text, up to 5,000 characters.</span><span class="sxs-lookup"><span data-stu-id="6434d-129">Unstructured raw text, up to 5,000 characters.</span></span> | <span data-ttu-id="6434d-130">Required</span><span class="sxs-lookup"><span data-stu-id="6434d-130">Required</span></span> | <span data-ttu-id="6434d-131">For language detection, text can be expressed in any language.</span><span class="sxs-lookup"><span data-stu-id="6434d-131">For language detection, text can be expressed in any language.</span></span> <span data-ttu-id="6434d-132">For sentiment analysis, key phrase extraction and entity identification, the text must be in a [supported language](../text-analytics-supported-languages.md).</span><span class="sxs-lookup"><span data-stu-id="6434d-132">For sentiment analysis, key phrase extraction and entity identification, the text must be in a [supported language](../text-analytics-supported-languages.md).</span></span> |
|`language` | <span data-ttu-id="6434d-133">2-character [ISO 639-1](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) code for a [supported language](../text-analytics-supported-languages.md)</span><span class="sxs-lookup"><span data-stu-id="6434d-133">2-character [ISO 639-1](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) code for a [supported language](../text-analytics-supported-languages.md)</span></span> | <span data-ttu-id="6434d-134">Varies</span><span class="sxs-lookup"><span data-stu-id="6434d-134">Varies</span></span> | <span data-ttu-id="6434d-135">Required for sentiment analysis, key phrase extraction, and entity linking; optional for language detection.</span><span class="sxs-lookup"><span data-stu-id="6434d-135">Required for sentiment analysis, key phrase extraction, and entity linking; optional for language detection.</span></span> <span data-ttu-id="6434d-136">There is no error if you exclude it, but the analysis is weakened without it.</span><span class="sxs-lookup"><span data-stu-id="6434d-136">There is no error if you exclude it, but the analysis is weakened without it.</span></span> <span data-ttu-id="6434d-137">The language code should correspond to the `text` you provide.</span><span class="sxs-lookup"><span data-stu-id="6434d-137">The language code should correspond to the `text` you provide.</span></span> |

<span data-ttu-id="6434d-138">For more information about limits, see [Text Analytics Overview > Data limits](../overview.md#data-limits).</span><span class="sxs-lookup"><span data-stu-id="6434d-138">For more information about limits, see [Text Analytics Overview > Data limits](../overview.md#data-limits).</span></span> 

## <a name="set-up-a-request-in-postman"></a><span data-ttu-id="6434d-139">Set up a request in Postman</span><span class="sxs-lookup"><span data-stu-id="6434d-139">Set up a request in Postman</span></span>

<span data-ttu-id="6434d-140">The service accepts request up to 1 MB in size.</span><span class="sxs-lookup"><span data-stu-id="6434d-140">The service accepts request up to 1 MB in size.</span></span> <span data-ttu-id="6434d-141">If you are using Postman (or another Web API test tool), set up the endpoint to include the resource you want to use, and provide the access key in a request header.</span><span class="sxs-lookup"><span data-stu-id="6434d-141">If you are using Postman (or another Web API test tool), set up the endpoint to include the resource you want to use, and provide the access key in a request header.</span></span> <span data-ttu-id="6434d-142">Each operation requires that you append the appropriate resource to the endpoint.</span><span class="sxs-lookup"><span data-stu-id="6434d-142">Each operation requires that you append the appropriate resource to the endpoint.</span></span> 

1. <span data-ttu-id="6434d-143">In Postman:</span><span class="sxs-lookup"><span data-stu-id="6434d-143">In Postman:</span></span>

   + <span data-ttu-id="6434d-144">Choose **Post** as the request type.</span><span class="sxs-lookup"><span data-stu-id="6434d-144">Choose **Post** as the request type.</span></span>
   + <span data-ttu-id="6434d-145">Paste in the endpoint you copied from the portal page.</span><span class="sxs-lookup"><span data-stu-id="6434d-145">Paste in the endpoint you copied from the portal page.</span></span>
   + <span data-ttu-id="6434d-146">Append a resource.</span><span class="sxs-lookup"><span data-stu-id="6434d-146">Append a resource.</span></span>

  <span data-ttu-id="6434d-147">Resource endpoints are as follows (your region may vary):</span><span class="sxs-lookup"><span data-stu-id="6434d-147">Resource endpoints are as follows (your region may vary):</span></span>

   + `https://westus.api.cognitive.microsoft.com/text/analytics/v2.0/sentiment`
   + `https://westus.api.cognitive.microsoft.com/text/analytics/v2.0/keyPhrases`
   + `https://westus.api.cognitive.microsoft.com/text/analytics/v2.0/languages`
   + `https://westus.api.cognitive.microsoft.com/text/analytics/v2.0/entities`

2. <span data-ttu-id="6434d-148">Set the three request headers:</span><span class="sxs-lookup"><span data-stu-id="6434d-148">Set the three request headers:</span></span>

   + <span data-ttu-id="6434d-149">`Ocp-Apim-Subscription-Key`: your access key, obtained from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="6434d-149">`Ocp-Apim-Subscription-Key`: your access key, obtained from Azure portal.</span></span>
   + <span data-ttu-id="6434d-150">`Content-Type`: application/json.</span><span class="sxs-lookup"><span data-stu-id="6434d-150">`Content-Type`: application/json.</span></span>
   + <span data-ttu-id="6434d-151">`Accept`: application/json.</span><span class="sxs-lookup"><span data-stu-id="6434d-151">`Accept`: application/json.</span></span>

  <span data-ttu-id="6434d-152">Your request should look similar to the following screenshot, assuming a **/keyPhrases** resource.</span><span class="sxs-lookup"><span data-stu-id="6434d-152">Your request should look similar to the following screenshot, assuming a **/keyPhrases** resource.</span></span>

   ![Request screenshot with endpoint and headers](../media/postman-request-keyphrase-1.png)

4. <span data-ttu-id="6434d-154">Click **Body** and choose **raw** for the format.</span><span class="sxs-lookup"><span data-stu-id="6434d-154">Click **Body** and choose **raw** for the format.</span></span>

   ![Request screenshot with body settings](../media/postman-request-body-raw.png)

5. <span data-ttu-id="6434d-156">Paste in some JSON documents in a format that is valid for the intended analysis.</span><span class="sxs-lookup"><span data-stu-id="6434d-156">Paste in some JSON documents in a format that is valid for the intended analysis.</span></span> <span data-ttu-id="6434d-157">For more information about a particular analysis, see the topics below:</span><span class="sxs-lookup"><span data-stu-id="6434d-157">For more information about a particular analysis, see the topics below:</span></span>

  + [<span data-ttu-id="6434d-158">Language detection</span><span class="sxs-lookup"><span data-stu-id="6434d-158">Language detection</span></span>](text-analytics-how-to-language-detection.md)  
  + [<span data-ttu-id="6434d-159">Key phrase extraction</span><span class="sxs-lookup"><span data-stu-id="6434d-159">Key phrase extraction</span></span>](text-analytics-how-to-keyword-extraction.md)  
  + [<span data-ttu-id="6434d-160">Sentiment analysis</span><span class="sxs-lookup"><span data-stu-id="6434d-160">Sentiment analysis</span></span>](text-analytics-how-to-sentiment-analysis.md)  
  + [<span data-ttu-id="6434d-161">Entity linking</span><span class="sxs-lookup"><span data-stu-id="6434d-161">Entity linking</span></span>](text-analytics-how-to-entity-linking.md)  


6. <span data-ttu-id="6434d-162">Click **Send** to submit the request.</span><span class="sxs-lookup"><span data-stu-id="6434d-162">Click **Send** to submit the request.</span></span> <span data-ttu-id="6434d-163">You can submit up to 100 requests per minute.</span><span class="sxs-lookup"><span data-stu-id="6434d-163">You can submit up to 100 requests per minute.</span></span> 

  <span data-ttu-id="6434d-164">In Postman, the response is displayed in the next window down, as a single JSON document, with an item for each document ID provided in the request.</span><span class="sxs-lookup"><span data-stu-id="6434d-164">In Postman, the response is displayed in the next window down, as a single JSON document, with an item for each document ID provided in the request.</span></span>

## <a name="see-also"></a><span data-ttu-id="6434d-165">See also</span><span class="sxs-lookup"><span data-stu-id="6434d-165">See also</span></span> 

 [<span data-ttu-id="6434d-166">Text Analytics Overview</span><span class="sxs-lookup"><span data-stu-id="6434d-166">Text Analytics Overview</span></span>](../overview.md)  
 [<span data-ttu-id="6434d-167">Frequently asked questions (FAQ)</span><span class="sxs-lookup"><span data-stu-id="6434d-167">Frequently asked questions (FAQ)</span></span>](../text-analytics-resource-faq.md)

## <a name="next-steps"></a><span data-ttu-id="6434d-168">Next steps</span><span class="sxs-lookup"><span data-stu-id="6434d-168">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6434d-169">Detect language</span><span class="sxs-lookup"><span data-stu-id="6434d-169">Detect language</span></span>](text-analytics-how-to-language-detection.md)
