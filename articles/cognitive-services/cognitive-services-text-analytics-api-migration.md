---
title: Upgrading to Version 2 of the Text Analytics API | Microsoft Docs
description: Azure Machine Learning Text Analytics - Upgrade to Version 2
services: cognitive-services
documentationcenter: ''
author: onewth
manager: jhubbard
editor: cgronlun
ms.assetid: bbf86f80-f677-42f3-8c17-118b16a23c34
ms.service: cognitive-services
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/04/2016
ms.author: onewth
ms.openlocfilehash: 9b28666e384402935ae342788afff6b6e8c7eab8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549977"
---
# <a name="upgrading-to-version-2-of-the-text-analytics-api"></a><span data-ttu-id="b8f02-103">Upgrading to Version 2 of the Text Analytics API</span><span class="sxs-lookup"><span data-stu-id="b8f02-103">Upgrading to Version 2 of the Text Analytics API</span></span>
<span data-ttu-id="b8f02-104">This guide will take you through the process of upgrading your code from using the [first version of the API](../machine-learning/machine-learning-apps-text-analytics.md) to using the second version.</span><span class="sxs-lookup"><span data-stu-id="b8f02-104">This guide will take you through the process of upgrading your code from using the [first version of the API](../machine-learning/machine-learning-apps-text-analytics.md) to using the second version.</span></span> 

<span data-ttu-id="b8f02-105">If you have not used the API and would like to learn more, you can **[learn more about the API here](//go.microsoft.com/fwlink/?LinkID=759711)** or **[follow the Quick Start Guide](//go.microsoft.com/fwlink/?LinkID=760860)**.</span><span class="sxs-lookup"><span data-stu-id="b8f02-105">If you have not used the API and would like to learn more, you can **[learn more about the API here](//go.microsoft.com/fwlink/?LinkID=759711)** or **[follow the Quick Start Guide](//go.microsoft.com/fwlink/?LinkID=760860)**.</span></span> <span data-ttu-id="b8f02-106">For technical reference, refer to the **[API Definition](//go.microsoft.com/fwlink/?LinkID=759346)**.</span><span class="sxs-lookup"><span data-stu-id="b8f02-106">For technical reference, refer to the **[API Definition](//go.microsoft.com/fwlink/?LinkID=759346)**.</span></span>

### <a name="part-1-get-a-new-key"></a><span data-ttu-id="b8f02-107">Part 1.</span><span class="sxs-lookup"><span data-stu-id="b8f02-107">Part 1.</span></span> <span data-ttu-id="b8f02-108">Get a new key</span><span class="sxs-lookup"><span data-stu-id="b8f02-108">Get a new key</span></span>
<span data-ttu-id="b8f02-109">First, you will need to get a new API key from the **Azure Portal**:</span><span class="sxs-lookup"><span data-stu-id="b8f02-109">First, you will need to get a new API key from the **Azure Portal**:</span></span>

1. <span data-ttu-id="b8f02-110">Navigate to the Text Analytics service through the [Cortana Intelligence Gallery](//gallery.cortanaintelligence.com/MachineLearningAPI/Text-Analytics-2).</span><span class="sxs-lookup"><span data-stu-id="b8f02-110">Navigate to the Text Analytics service through the [Cortana Intelligence Gallery](//gallery.cortanaintelligence.com/MachineLearningAPI/Text-Analytics-2).</span></span> <span data-ttu-id="b8f02-111">Here, you will also find links to the documentation and code samples.</span><span class="sxs-lookup"><span data-stu-id="b8f02-111">Here, you will also find links to the documentation and code samples.</span></span>
2. <span data-ttu-id="b8f02-112">Click **Sign Up**.</span><span class="sxs-lookup"><span data-stu-id="b8f02-112">Click **Sign Up**.</span></span> <span data-ttu-id="b8f02-113">This link will take you to the Azure management portal, where you can sign up for the service.</span><span class="sxs-lookup"><span data-stu-id="b8f02-113">This link will take you to the Azure management portal, where you can sign up for the service.</span></span>
3. <span data-ttu-id="b8f02-114">Select a plan.</span><span class="sxs-lookup"><span data-stu-id="b8f02-114">Select a plan.</span></span> <span data-ttu-id="b8f02-115">You may select the **free tier for 5,000 transactions/month**.</span><span class="sxs-lookup"><span data-stu-id="b8f02-115">You may select the **free tier for 5,000 transactions/month**.</span></span> <span data-ttu-id="b8f02-116">As is a free plan, you will not be charged for using the service.</span><span class="sxs-lookup"><span data-stu-id="b8f02-116">As is a free plan, you will not be charged for using the service.</span></span> <span data-ttu-id="b8f02-117">You will need to login to your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="b8f02-117">You will need to login to your Azure subscription.</span></span> 
4. <span data-ttu-id="b8f02-118">After you sign up for Text Analytics, you'll be given an **API Key**.</span><span class="sxs-lookup"><span data-stu-id="b8f02-118">After you sign up for Text Analytics, you'll be given an **API Key**.</span></span> <span data-ttu-id="b8f02-119">Copy this key, as you'll need it when using the API services.</span><span class="sxs-lookup"><span data-stu-id="b8f02-119">Copy this key, as you'll need it when using the API services.</span></span>

### <a name="part-2-update-the-headers"></a><span data-ttu-id="b8f02-120">Part 2.</span><span class="sxs-lookup"><span data-stu-id="b8f02-120">Part 2.</span></span> <span data-ttu-id="b8f02-121">Update the headers</span><span class="sxs-lookup"><span data-stu-id="b8f02-121">Update the headers</span></span>
<span data-ttu-id="b8f02-122">Update the submitted header values as shown below.</span><span class="sxs-lookup"><span data-stu-id="b8f02-122">Update the submitted header values as shown below.</span></span> <span data-ttu-id="b8f02-123">Note that the account key is no longer encoded.</span><span class="sxs-lookup"><span data-stu-id="b8f02-123">Note that the account key is no longer encoded.</span></span>

<span data-ttu-id="b8f02-124">**Version 1**</span><span class="sxs-lookup"><span data-stu-id="b8f02-124">**Version 1**</span></span>

    Authorization: Basic base64encode(<your Data Market account key>)
    Accept: application/json

<span data-ttu-id="b8f02-125">**Version 2**</span><span class="sxs-lookup"><span data-stu-id="b8f02-125">**Version 2**</span></span>

    Content-Type: application/json
    Accept: application/json
    Ocp-Apim-Subscription-Key: <your Azure Portal account key>


### <a name="part-3-update-the-base-url"></a><span data-ttu-id="b8f02-126">Part 3.</span><span class="sxs-lookup"><span data-stu-id="b8f02-126">Part 3.</span></span> <span data-ttu-id="b8f02-127">Update the base URL</span><span class="sxs-lookup"><span data-stu-id="b8f02-127">Update the base URL</span></span>
<span data-ttu-id="b8f02-128">**Version 1**</span><span class="sxs-lookup"><span data-stu-id="b8f02-128">**Version 1**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/

<span data-ttu-id="b8f02-129">**Version 2**</span><span class="sxs-lookup"><span data-stu-id="b8f02-129">**Version 2**</span></span>

    https://westus.api.cognitive.microsoft.com/text/analytics/v2.0/

### <a name="part-4a-update-the-formats-for-sentiment-key-phrases-and-languages"></a><span data-ttu-id="b8f02-130">Part 4a.</span><span class="sxs-lookup"><span data-stu-id="b8f02-130">Part 4a.</span></span> <span data-ttu-id="b8f02-131">Update the formats for sentiment, key phrases and languages</span><span class="sxs-lookup"><span data-stu-id="b8f02-131">Update the formats for sentiment, key phrases and languages</span></span>
#### <a name="endpoints"></a><span data-ttu-id="b8f02-132">Endpoints</span><span class="sxs-lookup"><span data-stu-id="b8f02-132">Endpoints</span></span>
<span data-ttu-id="b8f02-133">GET endpoints have now been deprecated, so all input should be submitted as a POST request.</span><span class="sxs-lookup"><span data-stu-id="b8f02-133">GET endpoints have now been deprecated, so all input should be submitted as a POST request.</span></span> <span data-ttu-id="b8f02-134">Update the endpoints to the ones shown below.</span><span class="sxs-lookup"><span data-stu-id="b8f02-134">Update the endpoints to the ones shown below.</span></span>

|  | <span data-ttu-id="b8f02-135">Version 1 single endpoint</span><span class="sxs-lookup"><span data-stu-id="b8f02-135">Version 1 single endpoint</span></span> | <span data-ttu-id="b8f02-136">Version 1 batch endpoint</span><span class="sxs-lookup"><span data-stu-id="b8f02-136">Version 1 batch endpoint</span></span> | <span data-ttu-id="b8f02-137">Version 2 endpoint</span><span class="sxs-lookup"><span data-stu-id="b8f02-137">Version 2 endpoint</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b8f02-138">Call type</span><span class="sxs-lookup"><span data-stu-id="b8f02-138">Call type</span></span> |<span data-ttu-id="b8f02-139">GET</span><span class="sxs-lookup"><span data-stu-id="b8f02-139">GET</span></span> |<span data-ttu-id="b8f02-140">POST</span><span class="sxs-lookup"><span data-stu-id="b8f02-140">POST</span></span> |<span data-ttu-id="b8f02-141">POST</span><span class="sxs-lookup"><span data-stu-id="b8f02-141">POST</span></span> |
| <span data-ttu-id="b8f02-142">Sentiment</span><span class="sxs-lookup"><span data-stu-id="b8f02-142">Sentiment</span></span> |```GetSentiment``` |```GetSentimentBatch``` |```sentiment``` |
| <span data-ttu-id="b8f02-143">Key phrases</span><span class="sxs-lookup"><span data-stu-id="b8f02-143">Key phrases</span></span> |```GetKeyPhrases``` |```GetKeyPhrasesBatch``` |```keyPhrases``` |
| <span data-ttu-id="b8f02-144">Languages</span><span class="sxs-lookup"><span data-stu-id="b8f02-144">Languages</span></span> |```GetLanguage``` |```GetLanguageBatch``` |```languages``` |

#### <a name="input-formats"></a><span data-ttu-id="b8f02-145">Input formats</span><span class="sxs-lookup"><span data-stu-id="b8f02-145">Input formats</span></span>
<span data-ttu-id="b8f02-146">Note that only POST format is now accepted, so you should reformat any input which previously used the single document endpoints accordingly.</span><span class="sxs-lookup"><span data-stu-id="b8f02-146">Note that only POST format is now accepted, so you should reformat any input which previously used the single document endpoints accordingly.</span></span> <span data-ttu-id="b8f02-147">Inputs are not case sensitive.</span><span class="sxs-lookup"><span data-stu-id="b8f02-147">Inputs are not case sensitive.</span></span>

<span data-ttu-id="b8f02-148">**Version 1 (batch)**</span><span class="sxs-lookup"><span data-stu-id="b8f02-148">**Version 1 (batch)**</span></span>

    {
      "Inputs": [
        {
          "Id": "string",
          "Text": "string"
        }
      ]
    }

<span data-ttu-id="b8f02-149">**Version 2**</span><span class="sxs-lookup"><span data-stu-id="b8f02-149">**Version 2**</span></span>

    {
      "documents": [
        {
          "id": "string",
          "text": "string"
        }
      ]
    }

#### <a name="output-from-sentiment"></a><span data-ttu-id="b8f02-150">Output from sentiment</span><span class="sxs-lookup"><span data-stu-id="b8f02-150">Output from sentiment</span></span>
<span data-ttu-id="b8f02-151">**Version 1**</span><span class="sxs-lookup"><span data-stu-id="b8f02-151">**Version 1**</span></span>

    {
      "SentimentBatch":[{
        "Id":"string",
        "Score":"double"
      }],
      "Errors" : [{
        "Id":"string",
        "Message":"string"
      }]
    }

<span data-ttu-id="b8f02-152">**Version 2**</span><span class="sxs-lookup"><span data-stu-id="b8f02-152">**Version 2**</span></span>

    {
      "documents":[{
        "id":"string",
        "score":"double"
      }],
      "errors" : [{
        "id":"string",
        "message":"string"
      }]
    }

#### <a name="output-from-key-phrases"></a><span data-ttu-id="b8f02-153">Output from key phrases</span><span class="sxs-lookup"><span data-stu-id="b8f02-153">Output from key phrases</span></span>
<span data-ttu-id="b8f02-154">**Version 1**</span><span class="sxs-lookup"><span data-stu-id="b8f02-154">**Version 1**</span></span>

    {
      "KeyPhrasesBatch":[{
        "Id":"string",
        "KeyPhrases":["string"]
      }],
      "Errors" : [{
        "Id":"string",
        "Message":"string"
      }]
    }

<span data-ttu-id="b8f02-155">**Version 2**</span><span class="sxs-lookup"><span data-stu-id="b8f02-155">**Version 2**</span></span>

    {
      "documents":[{
        "id":"string",
        "keyPhrases":["string"]
      }],
      "errors" : [{
        "id":"string",
        "message":"string"
      }]
    }

#### <a name="output-from-languages"></a><span data-ttu-id="b8f02-156">Output from languages</span><span class="sxs-lookup"><span data-stu-id="b8f02-156">Output from languages</span></span>
<span data-ttu-id="b8f02-157">**Version 1**</span><span class="sxs-lookup"><span data-stu-id="b8f02-157">**Version 1**</span></span>

    {
      "LanguageBatch":[{
        "id":"string",
        "detectedLanguages": [{
          "Score":"double"
          "Name":"string",
          "Iso6391Name":"string"
        }]
      }],
      "Errors" : [{
        "Id":"string",
        "Message":"string"
      }]
    }

<span data-ttu-id="b8f02-158">**Version 2**</span><span class="sxs-lookup"><span data-stu-id="b8f02-158">**Version 2**</span></span>

    {
      "documents":[{
        "id":"string",
        "detectedLanguages": [{
          "score":"double"
          "name":"string",
          "iso6391Name":"string"
        }]
      }],
      "errors" : [{
        "id":"string",
        "message":"string"
      }]
    }


### <a name="part-4b-update-the-formats-for-topics"></a><span data-ttu-id="b8f02-159">Part 4b.</span><span class="sxs-lookup"><span data-stu-id="b8f02-159">Part 4b.</span></span> <span data-ttu-id="b8f02-160">Update the formats for topics</span><span class="sxs-lookup"><span data-stu-id="b8f02-160">Update the formats for topics</span></span>
#### <a name="endpoints"></a><span data-ttu-id="b8f02-161">Endpoints</span><span class="sxs-lookup"><span data-stu-id="b8f02-161">Endpoints</span></span>
|  | <span data-ttu-id="b8f02-162">Version 1 endpoint</span><span class="sxs-lookup"><span data-stu-id="b8f02-162">Version 1 endpoint</span></span> | <span data-ttu-id="b8f02-163">Version 2 endpoint</span><span class="sxs-lookup"><span data-stu-id="b8f02-163">Version 2 endpoint</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b8f02-164">Submit for topic detection (POST)</span><span class="sxs-lookup"><span data-stu-id="b8f02-164">Submit for topic detection (POST)</span></span> |```StartTopicDetection``` |```topics``` |
| <span data-ttu-id="b8f02-165">Fetch topic results (GET)</span><span class="sxs-lookup"><span data-stu-id="b8f02-165">Fetch topic results (GET)</span></span> |```GetTopicDetectionResult?JobId=<jobId>``` |```operations/<operationId>``` |

#### <a name="input-formats"></a><span data-ttu-id="b8f02-166">Input formats</span><span class="sxs-lookup"><span data-stu-id="b8f02-166">Input formats</span></span>
<span data-ttu-id="b8f02-167">**Version 1**</span><span class="sxs-lookup"><span data-stu-id="b8f02-167">**Version 1**</span></span>

    {
      "StopWords": [
        "string"
      ],
      "StopPhrases": [
        "string"
      ], 
      "Inputs": [
        {
          "Id": "string",
          "Text": "string"
        }
      ]
    }

<span data-ttu-id="b8f02-168">**Version 2**</span><span class="sxs-lookup"><span data-stu-id="b8f02-168">**Version 2**</span></span>

    {
      "stopWords": [
        "string"
      ],
      "stopPhrases": [
        "string"
      ],
      "documents": [
        {
          "id": "string",
          "text": "string"
        }
      ]
    }

#### <a name="submission-results"></a><span data-ttu-id="b8f02-169">Submission results</span><span class="sxs-lookup"><span data-stu-id="b8f02-169">Submission results</span></span>
<span data-ttu-id="b8f02-170">**Version 1 (POST)**</span><span class="sxs-lookup"><span data-stu-id="b8f02-170">**Version 1 (POST)**</span></span>

<span data-ttu-id="b8f02-171">Previously, when the job finished, you would receive the following JSON output, where the jobId would be appended to a URL to fetch the output.</span><span class="sxs-lookup"><span data-stu-id="b8f02-171">Previously, when the job finished, you would receive the following JSON output, where the jobId would be appended to a URL to fetch the output.</span></span>

    {
        "odata.metadata":"<url>",
        "JobId":"<JobId>"
    }

<span data-ttu-id="b8f02-172">**Version 2 (POST)**</span><span class="sxs-lookup"><span data-stu-id="b8f02-172">**Version 2 (POST)**</span></span>

<span data-ttu-id="b8f02-173">The response will now include a header value as follows, where `operation-location` is used as the endpoint to poll for the results:</span><span class="sxs-lookup"><span data-stu-id="b8f02-173">The response will now include a header value as follows, where `operation-location` is used as the endpoint to poll for the results:</span></span>

    'operation-location': 'https://westus.api.cognitive.microsoft.com/text/analytics/v2.0/operations/<operationId>'

#### <a name="operation-results"></a><span data-ttu-id="b8f02-174">Operation results</span><span class="sxs-lookup"><span data-stu-id="b8f02-174">Operation results</span></span>
<span data-ttu-id="b8f02-175">**Version 1 (GET)**</span><span class="sxs-lookup"><span data-stu-id="b8f02-175">**Version 1 (GET)**</span></span>

    {
      "TopicInfo" : [{
        "TopicId" : "string"
        "Score" : "double"
        "KeyPhrase" : "string"
      }],
      "TopicAssignment" : [{
        "Id" : "string",
        "TopicId" : "string",
        "Distance" : "double"
      }],
      "Errors" : [{
        "Id":"string",
        "Message":"string"
      }]
    }

<span data-ttu-id="b8f02-176">**Version 2 (GET)**</span><span class="sxs-lookup"><span data-stu-id="b8f02-176">**Version 2 (GET)**</span></span>

<span data-ttu-id="b8f02-177">As before, **periodically poll the output** (the suggested period is every minute) until the output is returned.</span><span class="sxs-lookup"><span data-stu-id="b8f02-177">As before, **periodically poll the output** (the suggested period is every minute) until the output is returned.</span></span> 

<span data-ttu-id="b8f02-178">When the topics API has finished, a status reading `succeeded` will be returned.</span><span class="sxs-lookup"><span data-stu-id="b8f02-178">When the topics API has finished, a status reading `succeeded` will be returned.</span></span> <span data-ttu-id="b8f02-179">This will then include the output results in the format shown below:</span><span class="sxs-lookup"><span data-stu-id="b8f02-179">This will then include the output results in the format shown below:</span></span>

    {
        "status": "succeeded",
        "createdDateTime": "string",
        "operationType": "topics",
        "processingResult": {
            "topics" : [{
            "id" : "string"
            "score" : "double"
            "keyPhrase" : "string"
          }],
          "topicAssignments" : [{
            "topicId" : "string",
            "documentId" : "string",
            "distance" : "double"
          }],
          "errors" : [{
              "id":"string",
              "message":"string"
          }]
        }
    }

### <a name="part-5-test-it"></a><span data-ttu-id="b8f02-180">Part 5.</span><span class="sxs-lookup"><span data-stu-id="b8f02-180">Part 5.</span></span> <span data-ttu-id="b8f02-181">Test it!</span><span class="sxs-lookup"><span data-stu-id="b8f02-181">Test it!</span></span>
<span data-ttu-id="b8f02-182">You should now be good to go!</span><span class="sxs-lookup"><span data-stu-id="b8f02-182">You should now be good to go!</span></span> <span data-ttu-id="b8f02-183">Test your code with a small sample to ensure that you can successfully process your data.</span><span class="sxs-lookup"><span data-stu-id="b8f02-183">Test your code with a small sample to ensure that you can successfully process your data.</span></span>

