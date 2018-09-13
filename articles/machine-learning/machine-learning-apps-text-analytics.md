---
title: 'Machine Learning APIs: Text Analytics | Microsoft Docs'
description: Microsoft's Machine Learning Text Analytics APIs can be used to analyze unstructured text for sentiment analysis, key phrase extraction, language detection and topic detection.
services: machine-learning
documentationcenter: ''
author: onewth
manager: jhubbard
editor: cgronlun
ms.assetid: 5b60694e-5521-4e4d-bf6a-1a92fdf94b65
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: onewth
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: ../cognitive-services/cognitive-services-text-analytics-quick-start
ms.openlocfilehash: b22a206cffea3ba551680e77e4e56d3d8553bdd3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550312"
---
# <a name="machine-learning-apis-text-analytics-for-sentiment-key-phrase-extraction-language-detection-and-topic-detection"></a><span data-ttu-id="f8a26-103">Machine Learning APIs: Text Analytics for Sentiment, Key Phrase Extraction, Language Detection and Topic Detection</span><span class="sxs-lookup"><span data-stu-id="f8a26-103">Machine Learning APIs: Text Analytics for Sentiment, Key Phrase Extraction, Language Detection and Topic Detection</span></span>
> [!NOTE]
> <span data-ttu-id="f8a26-104">This guide is for version 1 of the API.</span><span class="sxs-lookup"><span data-stu-id="f8a26-104">This guide is for version 1 of the API.</span></span> <span data-ttu-id="f8a26-105">For version 2, [**refer to this document**](../cognitive-services/cognitive-services-text-analytics-quick-start.md).</span><span class="sxs-lookup"><span data-stu-id="f8a26-105">For version 2, [**refer to this document**](../cognitive-services/cognitive-services-text-analytics-quick-start.md).</span></span> <span data-ttu-id="f8a26-106">Version 2 is now the preferred version of this API.</span><span class="sxs-lookup"><span data-stu-id="f8a26-106">Version 2 is now the preferred version of this API.</span></span>
> 
> 

## <a name="overview"></a><span data-ttu-id="f8a26-107">Overview</span><span class="sxs-lookup"><span data-stu-id="f8a26-107">Overview</span></span>
<span data-ttu-id="f8a26-108">The Text Analytics API is a suite of text analytics [web services](https://datamarket.azure.com/dataset/amla/text-analytics) built with Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="f8a26-108">The Text Analytics API is a suite of text analytics [web services](https://datamarket.azure.com/dataset/amla/text-analytics) built with Azure Machine Learning.</span></span> <span data-ttu-id="f8a26-109">The API can be used to analyze unstructured text for tasks such as sentiment analysis, key phrase extraction, language detection and topic detection.</span><span class="sxs-lookup"><span data-stu-id="f8a26-109">The API can be used to analyze unstructured text for tasks such as sentiment analysis, key phrase extraction, language detection and topic detection.</span></span> <span data-ttu-id="f8a26-110">No training data is needed to use this API: just bring your text data.</span><span class="sxs-lookup"><span data-stu-id="f8a26-110">No training data is needed to use this API: just bring your text data.</span></span> <span data-ttu-id="f8a26-111">This API uses advanced natural language processing techniques to deliver best in class predictions.</span><span class="sxs-lookup"><span data-stu-id="f8a26-111">This API uses advanced natural language processing techniques to deliver best in class predictions.</span></span>

<span data-ttu-id="f8a26-112">You can see text analytics in action on our [demo site](https://text-analytics-demo.azurewebsites.net/), where you will also find [samples](https://text-analytics-demo.azurewebsites.net/Home/SampleCode) on how to implement text analytics in C# and Python.</span><span class="sxs-lookup"><span data-stu-id="f8a26-112">You can see text analytics in action on our [demo site](https://text-analytics-demo.azurewebsites.net/), where you will also find [samples](https://text-analytics-demo.azurewebsites.net/Home/SampleCode) on how to implement text analytics in C# and Python.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

- - -
## <a name="sentiment-analysis"></a><span data-ttu-id="f8a26-113">Sentiment analysis</span><span class="sxs-lookup"><span data-stu-id="f8a26-113">Sentiment analysis</span></span>
<span data-ttu-id="f8a26-114">The API returns a numeric score between 0 & 1.</span><span class="sxs-lookup"><span data-stu-id="f8a26-114">The API returns a numeric score between 0 & 1.</span></span> <span data-ttu-id="f8a26-115">Scores close to 1 indicate positive sentiment, while scores close to 0 indicate negative sentiment.</span><span class="sxs-lookup"><span data-stu-id="f8a26-115">Scores close to 1 indicate positive sentiment, while scores close to 0 indicate negative sentiment.</span></span> <span data-ttu-id="f8a26-116">Sentiment score is generated using classification techniques.</span><span class="sxs-lookup"><span data-stu-id="f8a26-116">Sentiment score is generated using classification techniques.</span></span> <span data-ttu-id="f8a26-117">The input features to the classifier include n-grams, features generated from part-of-speech tags, and word embeddings.</span><span class="sxs-lookup"><span data-stu-id="f8a26-117">The input features to the classifier include n-grams, features generated from part-of-speech tags, and word embeddings.</span></span> <span data-ttu-id="f8a26-118">Currently, English is the only supported language.</span><span class="sxs-lookup"><span data-stu-id="f8a26-118">Currently, English is the only supported language.</span></span>

## <a name="key-phrase-extraction"></a><span data-ttu-id="f8a26-119">Key phrase extraction</span><span class="sxs-lookup"><span data-stu-id="f8a26-119">Key phrase extraction</span></span>
<span data-ttu-id="f8a26-120">The API returns a list of strings denoting the key talking points in the input text.</span><span class="sxs-lookup"><span data-stu-id="f8a26-120">The API returns a list of strings denoting the key talking points in the input text.</span></span> <span data-ttu-id="f8a26-121">We employ techniques from Microsoft Office's sophisticated Natural Language Processing toolkit.</span><span class="sxs-lookup"><span data-stu-id="f8a26-121">We employ techniques from Microsoft Office's sophisticated Natural Language Processing toolkit.</span></span> <span data-ttu-id="f8a26-122">Currently, English is the only supported language.</span><span class="sxs-lookup"><span data-stu-id="f8a26-122">Currently, English is the only supported language.</span></span>

## <a name="language-detection"></a><span data-ttu-id="f8a26-123">Language detection</span><span class="sxs-lookup"><span data-stu-id="f8a26-123">Language detection</span></span>
<span data-ttu-id="f8a26-124">The API returns the detected language and a numeric score between 0 & 1.</span><span class="sxs-lookup"><span data-stu-id="f8a26-124">The API returns the detected language and a numeric score between 0 & 1.</span></span> <span data-ttu-id="f8a26-125">Scores close to 1 indicate 100% certainty that the identified language is true.</span><span class="sxs-lookup"><span data-stu-id="f8a26-125">Scores close to 1 indicate 100% certainty that the identified language is true.</span></span> <span data-ttu-id="f8a26-126">A total of 120 languages are supported.</span><span class="sxs-lookup"><span data-stu-id="f8a26-126">A total of 120 languages are supported.</span></span>

## <a name="topic-detection"></a><span data-ttu-id="f8a26-127">Topic detection</span><span class="sxs-lookup"><span data-stu-id="f8a26-127">Topic detection</span></span>
<span data-ttu-id="f8a26-128">This is a newly released API which returns the top detected topics for a list of submitted text records.</span><span class="sxs-lookup"><span data-stu-id="f8a26-128">This is a newly released API which returns the top detected topics for a list of submitted text records.</span></span> <span data-ttu-id="f8a26-129">A topic is identified with a key phrase, which can be one or more related words.</span><span class="sxs-lookup"><span data-stu-id="f8a26-129">A topic is identified with a key phrase, which can be one or more related words.</span></span> <span data-ttu-id="f8a26-130">This API requires a minimum of 100 text records to be submitted, but is designed to detect topics across hundreds to thousands of records.</span><span class="sxs-lookup"><span data-stu-id="f8a26-130">This API requires a minimum of 100 text records to be submitted, but is designed to detect topics across hundreds to thousands of records.</span></span> <span data-ttu-id="f8a26-131">Note that this API charges 1 transaction per text record submitted.</span><span class="sxs-lookup"><span data-stu-id="f8a26-131">Note that this API charges 1 transaction per text record submitted.</span></span> <span data-ttu-id="f8a26-132">The API is designed to work well for short, human written text such as reviews and user feedback.</span><span class="sxs-lookup"><span data-stu-id="f8a26-132">The API is designed to work well for short, human written text such as reviews and user feedback.</span></span>

- - -
## <a name="api-definition"></a><span data-ttu-id="f8a26-133">API Definition</span><span class="sxs-lookup"><span data-stu-id="f8a26-133">API Definition</span></span>
### <a name="headers"></a><span data-ttu-id="f8a26-134">Headers</span><span class="sxs-lookup"><span data-stu-id="f8a26-134">Headers</span></span>
<span data-ttu-id="f8a26-135">Ensure that you include the correct headers in your request, which should be as follows:</span><span class="sxs-lookup"><span data-stu-id="f8a26-135">Ensure that you include the correct headers in your request, which should be as follows:</span></span>

    Authorization: Basic <creds>
    Accept: application/json

    Where <creds> = ConvertToBase64(“AccountKey:” + yourActualAccountKey);  

<span data-ttu-id="f8a26-136">You can find your account key from your account in the [Azure Data Market](https://datamarket.azure.com/account/keys).</span><span class="sxs-lookup"><span data-stu-id="f8a26-136">You can find your account key from your account in the [Azure Data Market](https://datamarket.azure.com/account/keys).</span></span> <span data-ttu-id="f8a26-137">Note that currently only JSON is accepted for input and output formats.</span><span class="sxs-lookup"><span data-stu-id="f8a26-137">Note that currently only JSON is accepted for input and output formats.</span></span> <span data-ttu-id="f8a26-138">XML is not supported.</span><span class="sxs-lookup"><span data-stu-id="f8a26-138">XML is not supported.</span></span>

- - -
## <a name="single-response-apis"></a><span data-ttu-id="f8a26-139">Single Response APIs</span><span class="sxs-lookup"><span data-stu-id="f8a26-139">Single Response APIs</span></span>
### <a name="getsentiment"></a><span data-ttu-id="f8a26-140">GetSentiment</span><span class="sxs-lookup"><span data-stu-id="f8a26-140">GetSentiment</span></span>
<span data-ttu-id="f8a26-141">**URL**</span><span class="sxs-lookup"><span data-stu-id="f8a26-141">**URL**</span></span>    

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentiment

<span data-ttu-id="f8a26-142">**Example request**</span><span class="sxs-lookup"><span data-stu-id="f8a26-142">**Example request**</span></span>

<span data-ttu-id="f8a26-143">In the call below, we are requesting sentiment analysis for the phrase "Hello World":</span><span class="sxs-lookup"><span data-stu-id="f8a26-143">In the call below, we are requesting sentiment analysis for the phrase "Hello World":</span></span>

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentiment?Text=hello+world

<span data-ttu-id="f8a26-144">This will return a response as follows:</span><span class="sxs-lookup"><span data-stu-id="f8a26-144">This will return a response as follows:</span></span>

    {
      "odata.metadata":"https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/$metadata",
        "Score":1.0
    }

- - -
### <a name="getkeyphrases"></a><span data-ttu-id="f8a26-145">GetKeyPhrases</span><span class="sxs-lookup"><span data-stu-id="f8a26-145">GetKeyPhrases</span></span>
<span data-ttu-id="f8a26-146">**URL**</span><span class="sxs-lookup"><span data-stu-id="f8a26-146">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrases

<span data-ttu-id="f8a26-147">**Example request**</span><span class="sxs-lookup"><span data-stu-id="f8a26-147">**Example request**</span></span>

<span data-ttu-id="f8a26-148">In the call below, we are requesting the key phrases found in the text "It was a wonderful hotel to stay at, with unique decor and friendly staff":</span><span class="sxs-lookup"><span data-stu-id="f8a26-148">In the call below, we are requesting the key phrases found in the text "It was a wonderful hotel to stay at, with unique decor and friendly staff":</span></span>

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrases?
    Text=It+was+a+wonderful+hotel+to+stay+at,+with+unique+decor+and+friendly+staff

<span data-ttu-id="f8a26-149">This will return a response as follows:</span><span class="sxs-lookup"><span data-stu-id="f8a26-149">This will return a response as follows:</span></span>

    {
      "odata.metadata":"https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/$metadata",
      "KeyPhrases":[
        "wonderful hotel",
        "unique decor",
        "friendly staff"
      ]
    }

- - -
### <a name="getlanguage"></a><span data-ttu-id="f8a26-150">GetLanguage</span><span class="sxs-lookup"><span data-stu-id="f8a26-150">GetLanguage</span></span>
<span data-ttu-id="f8a26-151">**URL**</span><span class="sxs-lookup"><span data-stu-id="f8a26-151">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguage

<span data-ttu-id="f8a26-152">**Example request**</span><span class="sxs-lookup"><span data-stu-id="f8a26-152">**Example request**</span></span>

<span data-ttu-id="f8a26-153">In the GET call below, we are requesting for the sentiment for the key phrases in the text *Hello World*</span><span class="sxs-lookup"><span data-stu-id="f8a26-153">In the GET call below, we are requesting for the sentiment for the key phrases in the text *Hello World*</span></span>

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguages?
    Text=Hello+World

<span data-ttu-id="f8a26-154">This will return a response as follows:</span><span class="sxs-lookup"><span data-stu-id="f8a26-154">This will return a response as follows:</span></span>

    {
      "UnknownLanguage": false,
      "DetectedLanguages": [{
        "Name": "English",
        "Iso6391Name": "en",
        "Score": 1.0
      }]
    }

<span data-ttu-id="f8a26-155">**Optional parameters**</span><span class="sxs-lookup"><span data-stu-id="f8a26-155">**Optional parameters**</span></span>

<span data-ttu-id="f8a26-156">`NumberOfLanguagesToDetect` is an optional parameter.</span><span class="sxs-lookup"><span data-stu-id="f8a26-156">`NumberOfLanguagesToDetect` is an optional parameter.</span></span> <span data-ttu-id="f8a26-157">The default is 1.</span><span class="sxs-lookup"><span data-stu-id="f8a26-157">The default is 1.</span></span>

- - -
## <a name="batch-apis"></a><span data-ttu-id="f8a26-158">Batch APIs</span><span class="sxs-lookup"><span data-stu-id="f8a26-158">Batch APIs</span></span>
<span data-ttu-id="f8a26-159">The Text Analytics service allows you to do sentiment and key-phrase extractions in batch mode.</span><span class="sxs-lookup"><span data-stu-id="f8a26-159">The Text Analytics service allows you to do sentiment and key-phrase extractions in batch mode.</span></span> <span data-ttu-id="f8a26-160">Note that each of the records scored counts as one transaction.</span><span class="sxs-lookup"><span data-stu-id="f8a26-160">Note that each of the records scored counts as one transaction.</span></span> <span data-ttu-id="f8a26-161">As an example, if you request sentiment for 1000 records in a single call, 1000 transactions will be deducted.</span><span class="sxs-lookup"><span data-stu-id="f8a26-161">As an example, if you request sentiment for 1000 records in a single call, 1000 transactions will be deducted.</span></span>

<span data-ttu-id="f8a26-162">Note that the IDs entered into the system are the IDs returned by the system.</span><span class="sxs-lookup"><span data-stu-id="f8a26-162">Note that the IDs entered into the system are the IDs returned by the system.</span></span> <span data-ttu-id="f8a26-163">The web service does not check that these IDs are unique.</span><span class="sxs-lookup"><span data-stu-id="f8a26-163">The web service does not check that these IDs are unique.</span></span> <span data-ttu-id="f8a26-164">It is the responsibility of the caller to verify uniqueness.</span><span class="sxs-lookup"><span data-stu-id="f8a26-164">It is the responsibility of the caller to verify uniqueness.</span></span> 

### <a name="getsentimentbatch"></a><span data-ttu-id="f8a26-165">GetSentimentBatch</span><span class="sxs-lookup"><span data-stu-id="f8a26-165">GetSentimentBatch</span></span>
<span data-ttu-id="f8a26-166">**URL**</span><span class="sxs-lookup"><span data-stu-id="f8a26-166">**URL**</span></span>    

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentimentBatch

<span data-ttu-id="f8a26-167">**Example request**</span><span class="sxs-lookup"><span data-stu-id="f8a26-167">**Example request**</span></span>

<span data-ttu-id="f8a26-168">In the POST call below, we are requesting for the sentiments of the phrases "Hello World", "Hello Foo World" and "Hello My World" in the body of the request:</span><span class="sxs-lookup"><span data-stu-id="f8a26-168">In the POST call below, we are requesting for the sentiments of the phrases "Hello World", "Hello Foo World" and "Hello My World" in the body of the request:</span></span>

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentimentBatch 

<span data-ttu-id="f8a26-169">Request body:</span><span class="sxs-lookup"><span data-stu-id="f8a26-169">Request body:</span></span>

    {"Inputs":
    [
        {"Id":"1","Text":"hello world"},
        {"Id":"2","Text":"hello foo world"},
        {"Id":"3","Text":"hello my world"},
    ]}

<span data-ttu-id="f8a26-170">In the response below, you get the list of scores associated with your text Ids:</span><span class="sxs-lookup"><span data-stu-id="f8a26-170">In the response below, you get the list of scores associated with your text Ids:</span></span>

    {
      "odata.metadata":"<url>", 
      "SentimentBatch":
      [
        {"Score":0.9549767,"Id":"1"},
        {"Score":0.7767222,"Id":"2"},
        {"Score":0.8988889,"Id":"3"}
      ],  
      "Errors":[]
    }


- - -
### <a name="getkeyphrasesbatch"></a><span data-ttu-id="f8a26-171">GetKeyPhrasesBatch</span><span class="sxs-lookup"><span data-stu-id="f8a26-171">GetKeyPhrasesBatch</span></span>
<span data-ttu-id="f8a26-172">**URL**</span><span class="sxs-lookup"><span data-stu-id="f8a26-172">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrasesBatch

<span data-ttu-id="f8a26-173">**Example request**</span><span class="sxs-lookup"><span data-stu-id="f8a26-173">**Example request**</span></span>

<span data-ttu-id="f8a26-174">In this example, we are requesting for the list of sentiments for the key phrases in the following texts:</span><span class="sxs-lookup"><span data-stu-id="f8a26-174">In this example, we are requesting for the list of sentiments for the key phrases in the following texts:</span></span> 

* <span data-ttu-id="f8a26-175">"It was a wonderful hotel to stay at, with unique decor and friendly staff"</span><span class="sxs-lookup"><span data-stu-id="f8a26-175">"It was a wonderful hotel to stay at, with unique decor and friendly staff"</span></span>
* <span data-ttu-id="f8a26-176">"It was an amazing build conference, with very interesting talks"</span><span class="sxs-lookup"><span data-stu-id="f8a26-176">"It was an amazing build conference, with very interesting talks"</span></span>
* <span data-ttu-id="f8a26-177">"The traffic was terrible, I spent three hours going to the airport"</span><span class="sxs-lookup"><span data-stu-id="f8a26-177">"The traffic was terrible, I spent three hours going to the airport"</span></span>

<span data-ttu-id="f8a26-178">This request is made as a POST call to the endpoint:</span><span class="sxs-lookup"><span data-stu-id="f8a26-178">This request is made as a POST call to the endpoint:</span></span>

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrasesBatch

<span data-ttu-id="f8a26-179">Request body:</span><span class="sxs-lookup"><span data-stu-id="f8a26-179">Request body:</span></span>

    {"Inputs":
    [
        {"Id":"1","Text":"It was a wonderful hotel to stay at, with unique decor and friendly staff"},
        {"Id":"2","Text":"It was an amazing build conference, with very interesting talks"},
        {"Id":"3","Text":"The traffic was terrible, I spent three hours going to the airport"}
    ]}

<span data-ttu-id="f8a26-180">In the response below, you get the list of key phrases associated with your text Ids:</span><span class="sxs-lookup"><span data-stu-id="f8a26-180">In the response below, you get the list of key phrases associated with your text Ids:</span></span>

    { "odata.metadata":"<url>",
         "KeyPhrasesBatch":
        [
           {"KeyPhrases":["unique decor","friendly staff","wonderful hotel"],"Id":"1"},
           {"KeyPhrases":["amazing build conference","interesting talks"],"Id":"2"},
           {"KeyPhrases":["hours","traffic","airport"],"Id":"3" }
        ],
        "Errors":[]
    }

- - -
### <a name="getlanguagebatch"></a><span data-ttu-id="f8a26-181">GetLanguageBatch</span><span class="sxs-lookup"><span data-stu-id="f8a26-181">GetLanguageBatch</span></span>

<span data-ttu-id="f8a26-182">In the POST call below, we are requesting language detection for two text inputs:</span><span class="sxs-lookup"><span data-stu-id="f8a26-182">In the POST call below, we are requesting language detection for two text inputs:</span></span>

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguageBatch

<span data-ttu-id="f8a26-183">Request body:</span><span class="sxs-lookup"><span data-stu-id="f8a26-183">Request body:</span></span>

    {
      "Inputs": [
        {"Text": "hello world", "Id": "1"},
        {"Text": "c'est la vie", "Id": "2"}
      ]
    }

<span data-ttu-id="f8a26-184">This returns the following response, where English is detected in the first input and French in the second input:</span><span class="sxs-lookup"><span data-stu-id="f8a26-184">This returns the following response, where English is detected in the first input and French in the second input:</span></span>

    {
       "LanguageBatch": [{
         "Id": "1",
         "DetectedLanguages": [{
            "Name": "English",
            "Iso6391Name": "en",
            "Score": 1.0
         }],
         "UnknownLanguage": false
       },
       {
         "Id": "2",
         "DetectedLanguages": [{
            "Name": "French",
            "Iso6391Name": "fr",
            "Score": 1.0
         }],
         "UnknownLanguage": false
       }],
       "Errors": []
    }

- - -
## <a name="topic-detection-apis"></a><span data-ttu-id="f8a26-185">Topic Detection APIs</span><span class="sxs-lookup"><span data-stu-id="f8a26-185">Topic Detection APIs</span></span>
<span data-ttu-id="f8a26-186">This is a newly released API which returns the top detected topics for a list of submitted text records.</span><span class="sxs-lookup"><span data-stu-id="f8a26-186">This is a newly released API which returns the top detected topics for a list of submitted text records.</span></span> <span data-ttu-id="f8a26-187">A topic is identified with a key phrase, which can be one or more related words.</span><span class="sxs-lookup"><span data-stu-id="f8a26-187">A topic is identified with a key phrase, which can be one or more related words.</span></span> <span data-ttu-id="f8a26-188">Note that this API charges 1 transaction per text record submitted.</span><span class="sxs-lookup"><span data-stu-id="f8a26-188">Note that this API charges 1 transaction per text record submitted.</span></span>

<span data-ttu-id="f8a26-189">This API requires a minimum of 100 text records to be submitted, but is designed to detect topics across hundreds to thousands of records.</span><span class="sxs-lookup"><span data-stu-id="f8a26-189">This API requires a minimum of 100 text records to be submitted, but is designed to detect topics across hundreds to thousands of records.</span></span>

### <a name="topics--submit-job"></a><span data-ttu-id="f8a26-190">Topics – Submit job</span><span class="sxs-lookup"><span data-stu-id="f8a26-190">Topics – Submit job</span></span>
<span data-ttu-id="f8a26-191">**URL**</span><span class="sxs-lookup"><span data-stu-id="f8a26-191">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/StartTopicDetection

<span data-ttu-id="f8a26-192">**Example request**</span><span class="sxs-lookup"><span data-stu-id="f8a26-192">**Example request**</span></span>

<span data-ttu-id="f8a26-193">In the POST call below, we are requesting topics for a set of 100 articles, where the first and last input articles are shown, and two StopPhrases are included.</span><span class="sxs-lookup"><span data-stu-id="f8a26-193">In the POST call below, we are requesting topics for a set of 100 articles, where the first and last input articles are shown, and two StopPhrases are included.</span></span>

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/StartTopicDetection HTTP/1.1

<span data-ttu-id="f8a26-194">Request body:</span><span class="sxs-lookup"><span data-stu-id="f8a26-194">Request body:</span></span>

    {"Inputs":[
        {"Id":"1","Text":"I loved the food at this restaurant"},
        ...,
        {"Id":"100","Text":"I hated the decor"}
    ],
    "StopPhrases":[
        "restaurant", “visitor"
    ]}

<span data-ttu-id="f8a26-195">In the response below, you get the JobId for the submitted job:</span><span class="sxs-lookup"><span data-stu-id="f8a26-195">In the response below, you get the JobId for the submitted job:</span></span>

    {
        "odata.metadata":"<url>",
        "JobId":"<JobId>"
    }

<span data-ttu-id="f8a26-196">A list of single word or multiple word phrases which should not be returned as topics.</span><span class="sxs-lookup"><span data-stu-id="f8a26-196">A list of single word or multiple word phrases which should not be returned as topics.</span></span> <span data-ttu-id="f8a26-197">Can be used to filter out very generic topics.</span><span class="sxs-lookup"><span data-stu-id="f8a26-197">Can be used to filter out very generic topics.</span></span> <span data-ttu-id="f8a26-198">For example, in a dataset about hotel reviews, "hotel" and "hostel" may be sensible stop phrases.</span><span class="sxs-lookup"><span data-stu-id="f8a26-198">For example, in a dataset about hotel reviews, "hotel" and "hostel" may be sensible stop phrases.</span></span>  

### <a name="topics--poll-for-job-results"></a><span data-ttu-id="f8a26-199">Topics – Poll for job results</span><span class="sxs-lookup"><span data-stu-id="f8a26-199">Topics – Poll for job results</span></span>
<span data-ttu-id="f8a26-200">**URL**</span><span class="sxs-lookup"><span data-stu-id="f8a26-200">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetTopicDetectionResult

<span data-ttu-id="f8a26-201">**Example request**</span><span class="sxs-lookup"><span data-stu-id="f8a26-201">**Example request**</span></span>

<span data-ttu-id="f8a26-202">Pass the JobId returned from the ‘Submit job’ step to fetch the results.</span><span class="sxs-lookup"><span data-stu-id="f8a26-202">Pass the JobId returned from the ‘Submit job’ step to fetch the results.</span></span> <span data-ttu-id="f8a26-203">We recommend that you call this endpoint every minute until Status=’Complete’ in the response.</span><span class="sxs-lookup"><span data-stu-id="f8a26-203">We recommend that you call this endpoint every minute until Status=’Complete’ in the response.</span></span> <span data-ttu-id="f8a26-204">It will take around 10 mins for a job to complete, or longer for jobs with many thousands of records.</span><span class="sxs-lookup"><span data-stu-id="f8a26-204">It will take around 10 mins for a job to complete, or longer for jobs with many thousands of records.</span></span>

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetTopicDetectionResult?JobId=<JobId>


<span data-ttu-id="f8a26-205">While it is processing, the response will be as follows:</span><span class="sxs-lookup"><span data-stu-id="f8a26-205">While it is processing, the response will be as follows:</span></span>

    {
        "odata.metadata":"<url>",
        "Status":"Running",
         "TopicInfo":[],
        "TopicAssignment":[],
        "Errors":[]
    }


<span data-ttu-id="f8a26-206">The API returns output in JSON format in the following format:</span><span class="sxs-lookup"><span data-stu-id="f8a26-206">The API returns output in JSON format in the following format:</span></span>

    {
        "odata.metadata":"<url>",
        "Status":"Finished",
        "TopicInfo":[
        {
            "TopicId":"ed00480e-f0a0-41b3-8fe4-07c1593f4afd",
            "Score":8.0,
            "KeyPhrase":"food"
        },
        ...
        {
            "TopicId":"a5ca3f1a-fdb1-4f02-8f1b-89f2f626d692",
            "Score":6.0,
            "KeyPhrase":"decor"
            }
          ],
        "TopicAssignment":[
        {
            "Id":"1",
            "TopicId":"ed00480e-f0a0-41b3-8fe4-07c1593f4afd",
            "Distance":0.7809
        },
        ...
        {
            "Id":"100",
            "TopicId":"a5ca3f1a-fdb1-4f02-8f1b-89f2f626d692",
            "Distance":0.8034
        }
        ],
        "Errors":[]


<span data-ttu-id="f8a26-207">The properties for each part of the response are as follows:</span><span class="sxs-lookup"><span data-stu-id="f8a26-207">The properties for each part of the response are as follows:</span></span>

<span data-ttu-id="f8a26-208">**TopicInfo properties**</span><span class="sxs-lookup"><span data-stu-id="f8a26-208">**TopicInfo properties**</span></span>

| <span data-ttu-id="f8a26-209">Key</span><span class="sxs-lookup"><span data-stu-id="f8a26-209">Key</span></span> | <span data-ttu-id="f8a26-210">Description</span><span class="sxs-lookup"><span data-stu-id="f8a26-210">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="f8a26-211">TopicId</span><span class="sxs-lookup"><span data-stu-id="f8a26-211">TopicId</span></span> |<span data-ttu-id="f8a26-212">A unique identifier for each topic.</span><span class="sxs-lookup"><span data-stu-id="f8a26-212">A unique identifier for each topic.</span></span> |
| <span data-ttu-id="f8a26-213">Score</span><span class="sxs-lookup"><span data-stu-id="f8a26-213">Score</span></span> |<span data-ttu-id="f8a26-214">Count of records assigned to topic.</span><span class="sxs-lookup"><span data-stu-id="f8a26-214">Count of records assigned to topic.</span></span> |
| <span data-ttu-id="f8a26-215">KeyPhrase</span><span class="sxs-lookup"><span data-stu-id="f8a26-215">KeyPhrase</span></span> |<span data-ttu-id="f8a26-216">A summarizing word or phrase for the topic.</span><span class="sxs-lookup"><span data-stu-id="f8a26-216">A summarizing word or phrase for the topic.</span></span> <span data-ttu-id="f8a26-217">Can be 1 or multiple words.</span><span class="sxs-lookup"><span data-stu-id="f8a26-217">Can be 1 or multiple words.</span></span> |

<span data-ttu-id="f8a26-218">**TopicAssignment properties**</span><span class="sxs-lookup"><span data-stu-id="f8a26-218">**TopicAssignment properties**</span></span>

| <span data-ttu-id="f8a26-219">Key</span><span class="sxs-lookup"><span data-stu-id="f8a26-219">Key</span></span> | <span data-ttu-id="f8a26-220">Description</span><span class="sxs-lookup"><span data-stu-id="f8a26-220">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="f8a26-221">Id</span><span class="sxs-lookup"><span data-stu-id="f8a26-221">Id</span></span> |<span data-ttu-id="f8a26-222">Identifier for the record.</span><span class="sxs-lookup"><span data-stu-id="f8a26-222">Identifier for the record.</span></span> <span data-ttu-id="f8a26-223">Equates to the ID included in the input.</span><span class="sxs-lookup"><span data-stu-id="f8a26-223">Equates to the ID included in the input.</span></span> |
| <span data-ttu-id="f8a26-224">TopicId</span><span class="sxs-lookup"><span data-stu-id="f8a26-224">TopicId</span></span> |<span data-ttu-id="f8a26-225">The topic ID which the record has been assigned to.</span><span class="sxs-lookup"><span data-stu-id="f8a26-225">The topic ID which the record has been assigned to.</span></span> |
| <span data-ttu-id="f8a26-226">Distance</span><span class="sxs-lookup"><span data-stu-id="f8a26-226">Distance</span></span> |<span data-ttu-id="f8a26-227">Confidence that the record belongs to the topic.</span><span class="sxs-lookup"><span data-stu-id="f8a26-227">Confidence that the record belongs to the topic.</span></span> <span data-ttu-id="f8a26-228">Distance closer to zero indicates higher confidence.</span><span class="sxs-lookup"><span data-stu-id="f8a26-228">Distance closer to zero indicates higher confidence.</span></span> |

