---
title: 'Quick start guide: Machine Learning Text Analytics APIs | Microsoft Docs'
description: Azure Machine Learning Text Analytics - Quick Start Guide
services: cognitive-services
documentationcenter: ''
author: onewth
manager: jhubbard
editor: cgronlun
ms.assetid: e8b9e98c-40e7-4425-ae16-d1eaa7d2f837
ms.service: cognitive-services
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/04/2016
ms.author: onewth
ms.openlocfilehash: 4ee0f0300deba730f724479a971fa5396f86143a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555043"
---
# <a name="getting-started-with-the-text-analytics-apis-to-detect-sentiment-key-phrases-topics-and-language"></a><span data-ttu-id="2af19-103">Getting started with the Text Analytics APIs to detect sentiment, key phrases, topics and language</span><span class="sxs-lookup"><span data-stu-id="2af19-103">Getting started with the Text Analytics APIs to detect sentiment, key phrases, topics and language</span></span>
<a name="HOLTop"></a>

<span data-ttu-id="2af19-104">This document describes how to onboard your service or application to use the [Text Analytics APIs](//go.microsoft.com/fwlink/?LinkID=759711).</span><span class="sxs-lookup"><span data-stu-id="2af19-104">This document describes how to onboard your service or application to use the [Text Analytics APIs](//go.microsoft.com/fwlink/?LinkID=759711).</span></span>
<span data-ttu-id="2af19-105">You can use these APIs to detect sentiment, key phrases, topics and language from your text.</span><span class="sxs-lookup"><span data-stu-id="2af19-105">You can use these APIs to detect sentiment, key phrases, topics and language from your text.</span></span> [<span data-ttu-id="2af19-106">Click here to see an interactive demo of the experience.</span><span class="sxs-lookup"><span data-stu-id="2af19-106">Click here to see an interactive demo of the experience.</span></span>](//go.microsoft.com/fwlink/?LinkID=759712)

<span data-ttu-id="2af19-107">Please refer to the [API definitions](//go.microsoft.com/fwlink/?LinkID=759346) for technical documentation for the APIs.</span><span class="sxs-lookup"><span data-stu-id="2af19-107">Please refer to the [API definitions](//go.microsoft.com/fwlink/?LinkID=759346) for technical documentation for the APIs.</span></span>

<span data-ttu-id="2af19-108">This guide is for version 2 of the APIs.</span><span class="sxs-lookup"><span data-stu-id="2af19-108">This guide is for version 2 of the APIs.</span></span> <span data-ttu-id="2af19-109">For details on version 1 of the APIs, [refer to this document](../machine-learning/machine-learning-apps-text-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="2af19-109">For details on version 1 of the APIs, [refer to this document](../machine-learning/machine-learning-apps-text-analytics.md).</span></span>

<span data-ttu-id="2af19-110">By the end of this tutorial, you will be able to programatically detect:</span><span class="sxs-lookup"><span data-stu-id="2af19-110">By the end of this tutorial, you will be able to programatically detect:</span></span>

* <span data-ttu-id="2af19-111">**Sentiment** - Is text positive or negative?</span><span class="sxs-lookup"><span data-stu-id="2af19-111">**Sentiment** - Is text positive or negative?</span></span>
* <span data-ttu-id="2af19-112">**Key phrases** - What are people discussing in a single article?</span><span class="sxs-lookup"><span data-stu-id="2af19-112">**Key phrases** - What are people discussing in a single article?</span></span>
* <span data-ttu-id="2af19-113">**Topics** - What are people discussing across many articles?</span><span class="sxs-lookup"><span data-stu-id="2af19-113">**Topics** - What are people discussing across many articles?</span></span>
* <span data-ttu-id="2af19-114">**Languages** - What language is text written in?</span><span class="sxs-lookup"><span data-stu-id="2af19-114">**Languages** - What language is text written in?</span></span>

<span data-ttu-id="2af19-115">Note that this API charges 1 transaction per document submitted.</span><span class="sxs-lookup"><span data-stu-id="2af19-115">Note that this API charges 1 transaction per document submitted.</span></span> <span data-ttu-id="2af19-116">As an example, if you request sentiment for 1000 documents in a single call, 1000 transactions will be deducted.</span><span class="sxs-lookup"><span data-stu-id="2af19-116">As an example, if you request sentiment for 1000 documents in a single call, 1000 transactions will be deducted.</span></span>

<a name="Overview"></a>

## <a name="general-overview"></a><span data-ttu-id="2af19-117">General overview</span><span class="sxs-lookup"><span data-stu-id="2af19-117">General overview</span></span>
<span data-ttu-id="2af19-118">This document is a step-by-step guide.</span><span class="sxs-lookup"><span data-stu-id="2af19-118">This document is a step-by-step guide.</span></span> <span data-ttu-id="2af19-119">Our objective is to walk you through the steps necessary to train a model, and to point you to resources that will allow you to put it in production.</span><span class="sxs-lookup"><span data-stu-id="2af19-119">Our objective is to walk you through the steps necessary to train a model, and to point you to resources that will allow you to put it in production.</span></span> <span data-ttu-id="2af19-120">This exercise will take about 30 minutes.</span><span class="sxs-lookup"><span data-stu-id="2af19-120">This exercise will take about 30 minutes.</span></span>

<span data-ttu-id="2af19-121">For these tasks, you will need an editor and call the RESTful endpoints in your language of choice.</span><span class="sxs-lookup"><span data-stu-id="2af19-121">For these tasks, you will need an editor and call the RESTful endpoints in your language of choice.</span></span>

<span data-ttu-id="2af19-122">Let's get started!</span><span class="sxs-lookup"><span data-stu-id="2af19-122">Let's get started!</span></span>

## <a name="task-1---signing-up-for-the-text-analytics-apis"></a><span data-ttu-id="2af19-123">Task 1 - Signing up for the Text Analytics APIs</span><span class="sxs-lookup"><span data-stu-id="2af19-123">Task 1 - Signing up for the Text Analytics APIs</span></span>
<span data-ttu-id="2af19-124">In this task, you will sign up for the text analytics service.</span><span class="sxs-lookup"><span data-stu-id="2af19-124">In this task, you will sign up for the text analytics service.</span></span>

1. <span data-ttu-id="2af19-125">Navigate to **Cognitive Services** in the [Azure Portal](//go.microsoft.com/fwlink/?LinkId=761108) and ensure **Text Analytics** is selected as the 'API type'.</span><span class="sxs-lookup"><span data-stu-id="2af19-125">Navigate to **Cognitive Services** in the [Azure Portal](//go.microsoft.com/fwlink/?LinkId=761108) and ensure **Text Analytics** is selected as the 'API type'.</span></span>
2. <span data-ttu-id="2af19-126">Select a plan.</span><span class="sxs-lookup"><span data-stu-id="2af19-126">Select a plan.</span></span> <span data-ttu-id="2af19-127">You may select the **free tier for 5,000 transactions/month**.</span><span class="sxs-lookup"><span data-stu-id="2af19-127">You may select the **free tier for 5,000 transactions/month**.</span></span> <span data-ttu-id="2af19-128">As is a free plan, you will not be charged for using the service.</span><span class="sxs-lookup"><span data-stu-id="2af19-128">As is a free plan, you will not be charged for using the service.</span></span> <span data-ttu-id="2af19-129">You will need to login to your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="2af19-129">You will need to login to your Azure subscription.</span></span> 
3. <span data-ttu-id="2af19-130">Complete the other fields and create your account.</span><span class="sxs-lookup"><span data-stu-id="2af19-130">Complete the other fields and create your account.</span></span>
4. <span data-ttu-id="2af19-131">After you sign up for Text Analytics, find your **API Key**.</span><span class="sxs-lookup"><span data-stu-id="2af19-131">After you sign up for Text Analytics, find your **API Key**.</span></span> <span data-ttu-id="2af19-132">Copy the primary key, as you will need it when using the API services.</span><span class="sxs-lookup"><span data-stu-id="2af19-132">Copy the primary key, as you will need it when using the API services.</span></span>

## <a name="task-2---detect-sentiment-key-phrases-and-languages"></a><span data-ttu-id="2af19-133">Task 2 - Detect sentiment, key phrases and languages</span><span class="sxs-lookup"><span data-stu-id="2af19-133">Task 2 - Detect sentiment, key phrases and languages</span></span>
<span data-ttu-id="2af19-134">It's easy to detect sentiment, key phrases and languages in your text.</span><span class="sxs-lookup"><span data-stu-id="2af19-134">It's easy to detect sentiment, key phrases and languages in your text.</span></span> <span data-ttu-id="2af19-135">You will programatically get the same results as the [demo experience](//go.microsoft.com/fwlink/?LinkID=759712) returns.</span><span class="sxs-lookup"><span data-stu-id="2af19-135">You will programatically get the same results as the [demo experience](//go.microsoft.com/fwlink/?LinkID=759712) returns.</span></span>

> [!TIP]
> <span data-ttu-id="2af19-136">For sentiment analysis, we recommend that you split text into sentences.</span><span class="sxs-lookup"><span data-stu-id="2af19-136">For sentiment analysis, we recommend that you split text into sentences.</span></span> <span data-ttu-id="2af19-137">This generally leads to a higher precision in sentiment predictions.</span><span class="sxs-lookup"><span data-stu-id="2af19-137">This generally leads to a higher precision in sentiment predictions.</span></span>
> 
> 

<span data-ttu-id="2af19-138">Note that the supported languages are as follows:</span><span class="sxs-lookup"><span data-stu-id="2af19-138">Note that the supported languages are as follows:</span></span>

| <span data-ttu-id="2af19-139">Feature</span><span class="sxs-lookup"><span data-stu-id="2af19-139">Feature</span></span> | <span data-ttu-id="2af19-140">Supported language codes</span><span class="sxs-lookup"><span data-stu-id="2af19-140">Supported language codes</span></span> |
|:--- |:--- |
| <span data-ttu-id="2af19-141">Sentiment</span><span class="sxs-lookup"><span data-stu-id="2af19-141">Sentiment</span></span> |<span data-ttu-id="2af19-142">`en` (English), `es` (Spanish), `fr` (French), `pt` (Portuguese)</span><span class="sxs-lookup"><span data-stu-id="2af19-142">`en` (English), `es` (Spanish), `fr` (French), `pt` (Portuguese)</span></span> |
| <span data-ttu-id="2af19-143">Key phrases</span><span class="sxs-lookup"><span data-stu-id="2af19-143">Key phrases</span></span> |<span data-ttu-id="2af19-144">`en` (English), `es` (Spanish), `de` (German), `ja` (Japanese)</span><span class="sxs-lookup"><span data-stu-id="2af19-144">`en` (English), `es` (Spanish), `de` (German), `ja` (Japanese)</span></span> |

1. <span data-ttu-id="2af19-145">You will need to set the headers to the following.</span><span class="sxs-lookup"><span data-stu-id="2af19-145">You will need to set the headers to the following.</span></span> <span data-ttu-id="2af19-146">Note that JSON is currently the only accepted input format for the APIs.</span><span class="sxs-lookup"><span data-stu-id="2af19-146">Note that JSON is currently the only accepted input format for the APIs.</span></span> <span data-ttu-id="2af19-147">XML is not supported.</span><span class="sxs-lookup"><span data-stu-id="2af19-147">XML is not supported.</span></span>
   
        Ocp-Apim-Subscription-Key: <your API key>
        Content-Type: application/json
        Accept: application/json
2. <span data-ttu-id="2af19-148">Next, format your input rows in JSON.</span><span class="sxs-lookup"><span data-stu-id="2af19-148">Next, format your input rows in JSON.</span></span> <span data-ttu-id="2af19-149">For sentiment, key phrases and language, the format is the same.</span><span class="sxs-lookup"><span data-stu-id="2af19-149">For sentiment, key phrases and language, the format is the same.</span></span> <span data-ttu-id="2af19-150">Note that each ID should be unique and will be the ID returned by the system.</span><span class="sxs-lookup"><span data-stu-id="2af19-150">Note that each ID should be unique and will be the ID returned by the system.</span></span> <span data-ttu-id="2af19-151">The maximum size of a single document that can be submitted is 10KB, and the total maximum size of submitted input is 1MB.</span><span class="sxs-lookup"><span data-stu-id="2af19-151">The maximum size of a single document that can be submitted is 10KB, and the total maximum size of submitted input is 1MB.</span></span> <span data-ttu-id="2af19-152">No more than 1,000 documents may be submitted in one call.</span><span class="sxs-lookup"><span data-stu-id="2af19-152">No more than 1,000 documents may be submitted in one call.</span></span> <span data-ttu-id="2af19-153">Rate limiting exists at a rate of 100 calls per minute - we therefore recommend that you submit large quantities of documents in a single call.</span><span class="sxs-lookup"><span data-stu-id="2af19-153">Rate limiting exists at a rate of 100 calls per minute - we therefore recommend that you submit large quantities of documents in a single call.</span></span> <span data-ttu-id="2af19-154">Language is an optional parameter that should be specified if analyzing non-English text.</span><span class="sxs-lookup"><span data-stu-id="2af19-154">Language is an optional parameter that should be specified if analyzing non-English text.</span></span> <span data-ttu-id="2af19-155">An example of input is shown below, where the optional parameter `language` for sentiment analysis or key phrase extraction is included:</span><span class="sxs-lookup"><span data-stu-id="2af19-155">An example of input is shown below, where the optional parameter `language` for sentiment analysis or key phrase extraction is included:</span></span>
   
        {
            "documents": [
                {
                    "language": "en",
                    "id": "1",
                    "text": "First document"
                },
                ...
                {
                    "language": "en",
                    "id": "100",
                    "text": "Final document"
                }
            ]
        }
3. <span data-ttu-id="2af19-156">Make a **POST** call to the system with the input for sentiment, key phrases and language.</span><span class="sxs-lookup"><span data-stu-id="2af19-156">Make a **POST** call to the system with the input for sentiment, key phrases and language.</span></span> <span data-ttu-id="2af19-157">The URLs will look as follows:</span><span class="sxs-lookup"><span data-stu-id="2af19-157">The URLs will look as follows:</span></span>
   
        POST https://westus.api.cognitive.microsoft.com/text/analytics/v2.0/sentiment
        POST https://westus.api.cognitive.microsoft.com/text/analytics/v2.0/keyPhrases
        POST https://westus.api.cognitive.microsoft.com/text/analytics/v2.0/languages
4. <span data-ttu-id="2af19-158">This call will return a JSON formatted response with the IDs and detected properties.</span><span class="sxs-lookup"><span data-stu-id="2af19-158">This call will return a JSON formatted response with the IDs and detected properties.</span></span> <span data-ttu-id="2af19-159">An example of the output for sentiment is shown below (with error details excluded).</span><span class="sxs-lookup"><span data-stu-id="2af19-159">An example of the output for sentiment is shown below (with error details excluded).</span></span> <span data-ttu-id="2af19-160">In the case of sentiment, a score between 0 and 1 will be returned for each document:</span><span class="sxs-lookup"><span data-stu-id="2af19-160">In the case of sentiment, a score between 0 and 1 will be returned for each document:</span></span>
   
        // Sentiment response
        {
              "documents": [
                {
                    "id": "1",
                    "score": "0.934"
                },
                ...
                {
                    "id": "100",
                    "score": "0.002"
                },
            ]
        }
   
        // Key phrases response
        {
              "documents": [
                {
                    "id": "1",
                    "keyPhrases": ["key phrase 1", ..., "key phrase n"]
                },
                ...
                {
                    "id": "100",
                    "keyPhrases": ["key phrase 1", ..., "key phrase n"]
                },
            ]
        }
   
        // Languages response
        {
              "documents": [
                {
                    "id": "1",
                    "detectedLanguages": [
                        {
                            "name": "English",
                            "iso6391Name": "en",
                            "score": "1"
                        }
                    ]
                },
                ...
                {
                    "id": "100",
                    "detectedLanguages": [
                        {
                            "name": "French",
                            "iso6391Name": "fr",
                            "score": "0.985"
                        }
                    ]
                }
            ]
        }

## <a name="task-3---detect-topics-in-a-corpus-of-text"></a><span data-ttu-id="2af19-161">Task 3 - Detect topics in a corpus of text</span><span class="sxs-lookup"><span data-stu-id="2af19-161">Task 3 - Detect topics in a corpus of text</span></span>
<span data-ttu-id="2af19-162">This is a newly released API which returns the top detected topics for a list of submitted text records.</span><span class="sxs-lookup"><span data-stu-id="2af19-162">This is a newly released API which returns the top detected topics for a list of submitted text records.</span></span> <span data-ttu-id="2af19-163">A topic is identified with a key phrase, which can be one or more related words.</span><span class="sxs-lookup"><span data-stu-id="2af19-163">A topic is identified with a key phrase, which can be one or more related words.</span></span> <span data-ttu-id="2af19-164">The API is designed to work well for short, human written text such as reviews and user feedback.</span><span class="sxs-lookup"><span data-stu-id="2af19-164">The API is designed to work well for short, human written text such as reviews and user feedback.</span></span>

<span data-ttu-id="2af19-165">This API requires **a minimum of 100 text records** to be submitted, but is designed to detect topics across hundreds to thousands of records.</span><span class="sxs-lookup"><span data-stu-id="2af19-165">This API requires **a minimum of 100 text records** to be submitted, but is designed to detect topics across hundreds to thousands of records.</span></span> <span data-ttu-id="2af19-166">Any non-English records or records with less than 3 words will be discarded and therefore will not be assigned to topics.</span><span class="sxs-lookup"><span data-stu-id="2af19-166">Any non-English records or records with less than 3 words will be discarded and therefore will not be assigned to topics.</span></span> <span data-ttu-id="2af19-167">For topic detection, the maximum size of a single document that can be submitted is 30KB, and the total maximum size of submitted input is 30MB.</span><span class="sxs-lookup"><span data-stu-id="2af19-167">For topic detection, the maximum size of a single document that can be submitted is 30KB, and the total maximum size of submitted input is 30MB.</span></span> <span data-ttu-id="2af19-168">Topic detection is rate limited to 5 submissions every 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="2af19-168">Topic detection is rate limited to 5 submissions every 5 minutes.</span></span>

<span data-ttu-id="2af19-169">There are two additional **optional** input parameters that can help to improve the quality of results:</span><span class="sxs-lookup"><span data-stu-id="2af19-169">There are two additional **optional** input parameters that can help to improve the quality of results:</span></span>

* <span data-ttu-id="2af19-170">**Stop words.**</span><span class="sxs-lookup"><span data-stu-id="2af19-170">**Stop words.**</span></span>  <span data-ttu-id="2af19-171">These words and their close forms (e.g. plurals) will be excluded from the entire topic detection pipeline.</span><span class="sxs-lookup"><span data-stu-id="2af19-171">These words and their close forms (e.g. plurals) will be excluded from the entire topic detection pipeline.</span></span> <span data-ttu-id="2af19-172">Use this for common words (for example, “issue”, “error” and “user” may be appropriate choices for customer complaints about software).</span><span class="sxs-lookup"><span data-stu-id="2af19-172">Use this for common words (for example, “issue”, “error” and “user” may be appropriate choices for customer complaints about software).</span></span> <span data-ttu-id="2af19-173">Each string should be a single word.</span><span class="sxs-lookup"><span data-stu-id="2af19-173">Each string should be a single word.</span></span>
* <span data-ttu-id="2af19-174">**Stop phrases** - These phrases will be excluded from the list of returned topics.</span><span class="sxs-lookup"><span data-stu-id="2af19-174">**Stop phrases** - These phrases will be excluded from the list of returned topics.</span></span> <span data-ttu-id="2af19-175">Use this to exclude generic topics that you don’t want to see in the results.</span><span class="sxs-lookup"><span data-stu-id="2af19-175">Use this to exclude generic topics that you don’t want to see in the results.</span></span> <span data-ttu-id="2af19-176">For example, “Microsoft” and “Azure” would be appropriate choices for topics to exclude.</span><span class="sxs-lookup"><span data-stu-id="2af19-176">For example, “Microsoft” and “Azure” would be appropriate choices for topics to exclude.</span></span> <span data-ttu-id="2af19-177">Strings can contain multiple words.</span><span class="sxs-lookup"><span data-stu-id="2af19-177">Strings can contain multiple words.</span></span>

<span data-ttu-id="2af19-178">Follow these steps to detect topics in your text.</span><span class="sxs-lookup"><span data-stu-id="2af19-178">Follow these steps to detect topics in your text.</span></span>

1. <span data-ttu-id="2af19-179">Format the input in JSON.</span><span class="sxs-lookup"><span data-stu-id="2af19-179">Format the input in JSON.</span></span> <span data-ttu-id="2af19-180">This time, you can define stop words and stop phrases.</span><span class="sxs-lookup"><span data-stu-id="2af19-180">This time, you can define stop words and stop phrases.</span></span>
   
        {
            "documents": [
                {
                    "id": "1",
                    "text": "First document"
                },
                ...
                {
                    "id": "100",
                    "text": "Final document"
                }
            ],
            "stopWords": [
                "issue", "error", "user"
            ],
            "stopPhrases": [
                "Microsoft", "Azure"
            ]
        }
2. <span data-ttu-id="2af19-181">Using the same headers as defined in Task 2, make a **POST** call to the topics endpoint:</span><span class="sxs-lookup"><span data-stu-id="2af19-181">Using the same headers as defined in Task 2, make a **POST** call to the topics endpoint:</span></span>
   
        POST https://westus.api.cognitive.microsoft.com/text/analytics/v2.0/topics
3. <span data-ttu-id="2af19-182">This will return an `operation-location` as the header in the response, where the value is the URL to query for the resulting topics:</span><span class="sxs-lookup"><span data-stu-id="2af19-182">This will return an `operation-location` as the header in the response, where the value is the URL to query for the resulting topics:</span></span>
   
        'operation-location': 'https://westus.api.cognitive.microsoft.com/text/analytics/v2.0/operations/<operationId>'
4. <span data-ttu-id="2af19-183">Query the returned `operation-location` periodically with a **GET** request.</span><span class="sxs-lookup"><span data-stu-id="2af19-183">Query the returned `operation-location` periodically with a **GET** request.</span></span> <span data-ttu-id="2af19-184">Once per minute is recommended.</span><span class="sxs-lookup"><span data-stu-id="2af19-184">Once per minute is recommended.</span></span>
   
        GET https://westus.api.cognitive.microsoft.com/text/analytics/v2.0/operations/<operationId>
5. <span data-ttu-id="2af19-185">The endpoint will return a response including `{"status": "notstarted"}` before processing, `{"status": "running"}` while processing and `{"status": "succeeded"}` with the output once completed.</span><span class="sxs-lookup"><span data-stu-id="2af19-185">The endpoint will return a response including `{"status": "notstarted"}` before processing, `{"status": "running"}` while processing and `{"status": "succeeded"}` with the output once completed.</span></span> <span data-ttu-id="2af19-186">You can then consume the output which will be in the following format (note details like error format and dates have been excluded from this example):</span><span class="sxs-lookup"><span data-stu-id="2af19-186">You can then consume the output which will be in the following format (note details like error format and dates have been excluded from this example):</span></span>
   
        {
            "status": "succeeded",
            "operationProcessingResult": {
                  "topics": [
                    {
                        "id": "8b89dd7e-de2b-4a48-94c0-8e7844265196"
                        "score": "5"
                        "keyPhrase": "first topic name"
                    },
                    ...
                    {
                        "id": "359ed9cb-f793-4168-9cde-cd63d24e0d6d"
                        "score": "3"
                        "keyPhrase": "final topic name"
                    }
                ],
                  "topicAssignments": [
                    {
                        "topicId": "8b89dd7e-de2b-4a48-94c0-8e7844265196",
                        "documentId": "1",
                        "distance": "0.354"
                    },
                    ...
                    {
                        "topicId": "359ed9cb-f793-4168-9cde-cd63d24e0d6d",
                        "documentId": "55",
                        "distance": "0.758"
                    },            
                ]
            }
        }

<span data-ttu-id="2af19-187">Note that the successful response for topics from the `operations` endpoint will have the following schema:</span><span class="sxs-lookup"><span data-stu-id="2af19-187">Note that the successful response for topics from the `operations` endpoint will have the following schema:</span></span>

    {
            "topics" : [{
                "id" : "string",
                "score" : "number",
                "keyPhrase" : "string"
            }],
            "topicAssignments" : [{
                "documentId" : "string",
                "topicId" : "string",
                "distance" : "number"
            }],
            "errors" : [{
                "id" : "string",
                "message" : "string"
            }]
        }

<span data-ttu-id="2af19-188">Explanations for each part of this response are as follows:</span><span class="sxs-lookup"><span data-stu-id="2af19-188">Explanations for each part of this response are as follows:</span></span>

<span data-ttu-id="2af19-189">**topics**</span><span class="sxs-lookup"><span data-stu-id="2af19-189">**topics**</span></span>

| <span data-ttu-id="2af19-190">Key</span><span class="sxs-lookup"><span data-stu-id="2af19-190">Key</span></span> | <span data-ttu-id="2af19-191">Description</span><span class="sxs-lookup"><span data-stu-id="2af19-191">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="2af19-192">id</span><span class="sxs-lookup"><span data-stu-id="2af19-192">id</span></span> |<span data-ttu-id="2af19-193">A unique identifier for each topic.</span><span class="sxs-lookup"><span data-stu-id="2af19-193">A unique identifier for each topic.</span></span> |
| <span data-ttu-id="2af19-194">score</span><span class="sxs-lookup"><span data-stu-id="2af19-194">score</span></span> |<span data-ttu-id="2af19-195">Count of documents assigned to topic.</span><span class="sxs-lookup"><span data-stu-id="2af19-195">Count of documents assigned to topic.</span></span> |
| <span data-ttu-id="2af19-196">keyPhrase</span><span class="sxs-lookup"><span data-stu-id="2af19-196">keyPhrase</span></span> |<span data-ttu-id="2af19-197">A summarizing word or phrase for the topic.</span><span class="sxs-lookup"><span data-stu-id="2af19-197">A summarizing word or phrase for the topic.</span></span> |

<span data-ttu-id="2af19-198">**topicAssignments**</span><span class="sxs-lookup"><span data-stu-id="2af19-198">**topicAssignments**</span></span>

| <span data-ttu-id="2af19-199">Key</span><span class="sxs-lookup"><span data-stu-id="2af19-199">Key</span></span> | <span data-ttu-id="2af19-200">Description</span><span class="sxs-lookup"><span data-stu-id="2af19-200">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="2af19-201">documentId</span><span class="sxs-lookup"><span data-stu-id="2af19-201">documentId</span></span> |<span data-ttu-id="2af19-202">Identifier for the document.</span><span class="sxs-lookup"><span data-stu-id="2af19-202">Identifier for the document.</span></span> <span data-ttu-id="2af19-203">Equates to the ID included in the input.</span><span class="sxs-lookup"><span data-stu-id="2af19-203">Equates to the ID included in the input.</span></span> |
| <span data-ttu-id="2af19-204">topicId</span><span class="sxs-lookup"><span data-stu-id="2af19-204">topicId</span></span> |<span data-ttu-id="2af19-205">The topic ID which the document has been assigned to.</span><span class="sxs-lookup"><span data-stu-id="2af19-205">The topic ID which the document has been assigned to.</span></span> |
| <span data-ttu-id="2af19-206">distance</span><span class="sxs-lookup"><span data-stu-id="2af19-206">distance</span></span> |<span data-ttu-id="2af19-207">Document-to-topic affiliation score between 0 and 1.</span><span class="sxs-lookup"><span data-stu-id="2af19-207">Document-to-topic affiliation score between 0 and 1.</span></span> <span data-ttu-id="2af19-208">The lower a distance score the stronger the topic affiliation is.</span><span class="sxs-lookup"><span data-stu-id="2af19-208">The lower a distance score the stronger the topic affiliation is.</span></span> |

<span data-ttu-id="2af19-209">**errors**</span><span class="sxs-lookup"><span data-stu-id="2af19-209">**errors**</span></span>

| <span data-ttu-id="2af19-210">Key</span><span class="sxs-lookup"><span data-stu-id="2af19-210">Key</span></span> | <span data-ttu-id="2af19-211">Description</span><span class="sxs-lookup"><span data-stu-id="2af19-211">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="2af19-212">id</span><span class="sxs-lookup"><span data-stu-id="2af19-212">id</span></span> |<span data-ttu-id="2af19-213">Input document unique identifier the error refers to.</span><span class="sxs-lookup"><span data-stu-id="2af19-213">Input document unique identifier the error refers to.</span></span> |
| <span data-ttu-id="2af19-214">message</span><span class="sxs-lookup"><span data-stu-id="2af19-214">message</span></span> |<span data-ttu-id="2af19-215">Error message.</span><span class="sxs-lookup"><span data-stu-id="2af19-215">Error message.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="2af19-216">Next steps</span><span class="sxs-lookup"><span data-stu-id="2af19-216">Next steps</span></span>
<span data-ttu-id="2af19-217">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="2af19-217">Congratulations!</span></span> <span data-ttu-id="2af19-218">You have now completed using text analytics on your data.</span><span class="sxs-lookup"><span data-stu-id="2af19-218">You have now completed using text analytics on your data.</span></span> <span data-ttu-id="2af19-219">You may now wish to look into using a tool such as [Power BI](//powerbi.microsoft.com) to visualize your data, as well as automating your insights to give you a real-time view of your text data.</span><span class="sxs-lookup"><span data-stu-id="2af19-219">You may now wish to look into using a tool such as [Power BI](//powerbi.microsoft.com) to visualize your data, as well as automating your insights to give you a real-time view of your text data.</span></span>

<span data-ttu-id="2af19-220">To see how Text Analytics capabilities, such as sentiment, can be used as part of a bot, see the [Emotional Bot](http://docs.botframework.com/en-us/bot-intelligence/language/#example-emotional-bot) example on the Bot Framework site.</span><span class="sxs-lookup"><span data-stu-id="2af19-220">To see how Text Analytics capabilities, such as sentiment, can be used as part of a bot, see the [Emotional Bot](http://docs.botframework.com/en-us/bot-intelligence/language/#example-emotional-bot) example on the Bot Framework site.</span></span>

