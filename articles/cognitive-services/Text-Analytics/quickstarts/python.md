---
title: 'Quickstart: Using Python to call the Text Analytics API | Microsoft Docs'
titleSuffix: Azure Cognitive Services
description: Get information and code samples to help you quickly get started using the Text Analytics API in Microsoft Cognitive Services on Azure.
services: cognitive-services
author: ashmaka
ms.service: cognitive-services
ms.component: text-analytics
ms.topic: article
ms.date: 05/02/2018
ms.author: ashmaka
ms.openlocfilehash: 8e570aac2c2d89a8147d179c4b0f9155497c5188
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869344"
---
# <a name="quickstart-using-python-to-call-the-text-analytics-cognitive-service"></a><span data-ttu-id="4df82-103">Quickstart: Using Python to call the Text Analytics Cognitive Service</span><span class="sxs-lookup"><span data-stu-id="4df82-103">Quickstart: Using Python to call the Text Analytics Cognitive Service</span></span>
<a name="HOLTop"></a>

<span data-ttu-id="4df82-104">This walkthrough shows you how to [detect language](#Detect), [analyze sentiment](#SentimentAnalysis), and [extract key phrases](#KeyPhraseExtraction) using the [Text Analytics APIs](//go.microsoft.com/fwlink/?LinkID=759711) with Python.</span><span class="sxs-lookup"><span data-stu-id="4df82-104">This walkthrough shows you how to [detect language](#Detect), [analyze sentiment](#SentimentAnalysis), and [extract key phrases](#KeyPhraseExtraction) using the [Text Analytics APIs](//go.microsoft.com/fwlink/?LinkID=759711) with Python.</span></span>

<span data-ttu-id="4df82-105">You can run this example as a Jupyter notebook on [MyBinder](https://mybinder.org) by clicking on the launch Binder badge:</span><span class="sxs-lookup"><span data-stu-id="4df82-105">You can run this example as a Jupyter notebook on [MyBinder](https://mybinder.org) by clicking on the launch Binder badge:</span></span> 

<span data-ttu-id="4df82-106">[![Binder](https://mybinder.org/badge.svg)](https://mybinder.org/v2/gh/Microsoft/cognitive-services-notebooks/master?filepath=TextAnalytics.ipynb)</span><span class="sxs-lookup"><span data-stu-id="4df82-106">[![Binder](https://mybinder.org/badge.svg)](https://mybinder.org/v2/gh/Microsoft/cognitive-services-notebooks/master?filepath=TextAnalytics.ipynb)</span></span>

<span data-ttu-id="4df82-107">Refer to the [API definitions](//go.microsoft.com/fwlink/?LinkID=759346) for technical documentation for the APIs.</span><span class="sxs-lookup"><span data-stu-id="4df82-107">Refer to the [API definitions](//go.microsoft.com/fwlink/?LinkID=759346) for technical documentation for the APIs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4df82-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="4df82-108">Prerequisites</span></span>

<span data-ttu-id="4df82-109">You must have a [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) with **Text Analytics API**.</span><span class="sxs-lookup"><span data-stu-id="4df82-109">You must have a [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) with **Text Analytics API**.</span></span> <span data-ttu-id="4df82-110">You can use the **free tier for 5,000 transactions/month** to complete this walkthrough.</span><span class="sxs-lookup"><span data-stu-id="4df82-110">You can use the **free tier for 5,000 transactions/month** to complete this walkthrough.</span></span>

<span data-ttu-id="4df82-111">You must also have the [endpoint and access key](../How-tos/text-analytics-how-to-access-key.md) that was generated for you during sign-up.</span><span class="sxs-lookup"><span data-stu-id="4df82-111">You must also have the [endpoint and access key](../How-tos/text-analytics-how-to-access-key.md) that was generated for you during sign-up.</span></span> 

<span data-ttu-id="4df82-112">To continue with this walkthrough, replace `subscription_key` with a valid subscription key that you obtained earlier.</span><span class="sxs-lookup"><span data-stu-id="4df82-112">To continue with this walkthrough, replace `subscription_key` with a valid subscription key that you obtained earlier.</span></span>


```python
subscription_key = None
assert subscription_key
```

<span data-ttu-id="4df82-113">Next, verify that the region in `text_analytics_base_url` corresponds to the one you used when setting up the service.</span><span class="sxs-lookup"><span data-stu-id="4df82-113">Next, verify that the region in `text_analytics_base_url` corresponds to the one you used when setting up the service.</span></span> <span data-ttu-id="4df82-114">If you are using a free trial key, you do not need to change anything.</span><span class="sxs-lookup"><span data-stu-id="4df82-114">If you are using a free trial key, you do not need to change anything.</span></span>


```python
text_analytics_base_url = "https://westcentralus.api.cognitive.microsoft.com/text/analytics/v2.0/"
```

<a name="Detect"></a>

## <a name="detect-languages"></a><span data-ttu-id="4df82-115">Detect languages</span><span class="sxs-lookup"><span data-stu-id="4df82-115">Detect languages</span></span>

<span data-ttu-id="4df82-116">The Language Detection API detects the language of a text document, using the [Detect Language method](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/56f30ceeeda5650db055a3c7).</span><span class="sxs-lookup"><span data-stu-id="4df82-116">The Language Detection API detects the language of a text document, using the [Detect Language method](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/56f30ceeeda5650db055a3c7).</span></span> <span data-ttu-id="4df82-117">The service endpoint of the language detection API for your region is available via the following URL:</span><span class="sxs-lookup"><span data-stu-id="4df82-117">The service endpoint of the language detection API for your region is available via the following URL:</span></span>


```python
language_api_url = text_analytics_base_url + "languages"
print(language_api_url)
```

    https://westcentralus.api.cognitive.microsoft.com/text/analytics/v2.0/languages


<span data-ttu-id="4df82-118">The payload to the API consists of a list of `documents`, each of which in turn contains an `id` and a `text` attribute.</span><span class="sxs-lookup"><span data-stu-id="4df82-118">The payload to the API consists of a list of `documents`, each of which in turn contains an `id` and a `text` attribute.</span></span> <span data-ttu-id="4df82-119">The `text` attribute stores the text to be analyzed.</span><span class="sxs-lookup"><span data-stu-id="4df82-119">The `text` attribute stores the text to be analyzed.</span></span> 

<span data-ttu-id="4df82-120">Replace the `documents` dictionary with any other text for language detection.</span><span class="sxs-lookup"><span data-stu-id="4df82-120">Replace the `documents` dictionary with any other text for language detection.</span></span> 


```python
documents = { 'documents': [
    { 'id': '1', 'text': 'This is a document written in English.' },
    { 'id': '2', 'text': 'Este es un document escrito en Español.' },
    { 'id': '3', 'text': '这是一个用中文写的文件' }
]}
```

<span data-ttu-id="4df82-121">The next few lines of code call out to the language detection API using the `requests` library in Python to determine the language in the documents.</span><span class="sxs-lookup"><span data-stu-id="4df82-121">The next few lines of code call out to the language detection API using the `requests` library in Python to determine the language in the documents.</span></span>


```python
import requests
from pprint import pprint
headers   = {"Ocp-Apim-Subscription-Key": subscription_key}
response  = requests.post(language_api_url, headers=headers, json=documents)
languages = response.json()
pprint(languages)
```

    {'documents': [{'detectedLanguages': [{'iso6391Name': 'en',
                                           'name': 'English',
                                           'score': 1.0}],
                    'id': '1'},
                   {'detectedLanguages': [{'iso6391Name': 'es',
                                           'name': 'Spanish',
                                           'score': 1.0}],
                    'id': '2'},
                   {'detectedLanguages': [{'iso6391Name': 'zh_chs',
                                           'name': 'Chinese_Simplified',
                                           'score': 1.0}],
                    'id': '3'}],
     'errors': []}


<span data-ttu-id="4df82-122">The following lines of code render the JSON data as an HTML table.</span><span class="sxs-lookup"><span data-stu-id="4df82-122">The following lines of code render the JSON data as an HTML table.</span></span>


```python
from IPython.display import HTML
table = []
for document in languages["documents"]:
    text  = next(filter(lambda d: d["id"] == document["id"], documents["documents"]))["text"]
    langs = ", ".join(["{0}({1})".format(lang["name"], lang["score"]) for lang in document["detectedLanguages"]])
    table.append("<tr><td>{0}</td><td>{1}</td>".format(text, langs))
HTML("<table><tr><th>Text</th><th>Detected languages(scores)</th></tr>{0}</table>".format("\n".join(table)))
```

<a name="SentimentAnalysis"></a>

## <a name="analyze-sentiment"></a><span data-ttu-id="4df82-123">Analyze sentiment</span><span class="sxs-lookup"><span data-stu-id="4df82-123">Analyze sentiment</span></span>

<span data-ttu-id="4df82-124">The Sentiment Analysis API detexts the sentiment of a set of text records, using the [Sentiment method](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/56f30ceeeda5650db055a3c9).</span><span class="sxs-lookup"><span data-stu-id="4df82-124">The Sentiment Analysis API detexts the sentiment of a set of text records, using the [Sentiment method](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/56f30ceeeda5650db055a3c9).</span></span> <span data-ttu-id="4df82-125">The following example scores two documents, one in English and another in Spanish.</span><span class="sxs-lookup"><span data-stu-id="4df82-125">The following example scores two documents, one in English and another in Spanish.</span></span>

<span data-ttu-id="4df82-126">The service endpoint for sentiment analysis is available for your region via the following URL:</span><span class="sxs-lookup"><span data-stu-id="4df82-126">The service endpoint for sentiment analysis is available for your region via the following URL:</span></span>


```python
sentiment_api_url = text_analytics_base_url + "sentiment"
print(sentiment_api_url)
```

    https://westcentralus.api.cognitive.microsoft.com/text/analytics/v2.0/sentiment


<span data-ttu-id="4df82-127">As with the language detection example, the service is provided with a dictionary with a `documents` key that consists of a list of documents.</span><span class="sxs-lookup"><span data-stu-id="4df82-127">As with the language detection example, the service is provided with a dictionary with a `documents` key that consists of a list of documents.</span></span> <span data-ttu-id="4df82-128">Each document is a tuple consisting of the `id`, the `text` to be analyzed and the `language` of the text.</span><span class="sxs-lookup"><span data-stu-id="4df82-128">Each document is a tuple consisting of the `id`, the `text` to be analyzed and the `language` of the text.</span></span> <span data-ttu-id="4df82-129">You can use the language detection API from the previous section to populate this field.</span><span class="sxs-lookup"><span data-stu-id="4df82-129">You can use the language detection API from the previous section to populate this field.</span></span> 


```python
documents = {'documents' : [
  {'id': '1', 'language': 'en', 'text': 'I had a wonderful experience! The rooms were wonderful and the staff was helpful.'},
  {'id': '2', 'language': 'en', 'text': 'I had a terrible time at the hotel. The staff was rude and the food was awful.'},  
  {'id': '3', 'language': 'es', 'text': 'Los caminos que llevan hasta Monte Rainier son espectaculares y hermosos.'},  
  {'id': '4', 'language': 'es', 'text': 'La carretera estaba atascada. Había mucho tráfico el día de ayer.'}
]}
```

<span data-ttu-id="4df82-130">The sentiment API can now be used to analyze the documents for their sentiments.</span><span class="sxs-lookup"><span data-stu-id="4df82-130">The sentiment API can now be used to analyze the documents for their sentiments.</span></span>


```python
headers   = {"Ocp-Apim-Subscription-Key": subscription_key}
response  = requests.post(sentiment_api_url, headers=headers, json=documents)
sentiments = response.json()
pprint(sentiments)
```

    {'documents': [{'id': '1', 'score': 0.7673527002334595},
                   {'id': '2', 'score': 0.18574094772338867},
                   {'id': '3', 'score': 0.5}],
     'errors': []}


<span data-ttu-id="4df82-131">The sentiment score for a document is between $0$ and $1$, with a higher score indicating a more positive sentiment.</span><span class="sxs-lookup"><span data-stu-id="4df82-131">The sentiment score for a document is between $0$ and $1$, with a higher score indicating a more positive sentiment.</span></span>

<a name="KeyPhraseExtraction"></a>

## <a name="extract-key-phrases"></a><span data-ttu-id="4df82-132">Extract key phrases</span><span class="sxs-lookup"><span data-stu-id="4df82-132">Extract key phrases</span></span>

<span data-ttu-id="4df82-133">The Key Phrase Extraction API extracts key-phrases from a text document, using the [Key Phrases method](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/56f30ceeeda5650db055a3c6).</span><span class="sxs-lookup"><span data-stu-id="4df82-133">The Key Phrase Extraction API extracts key-phrases from a text document, using the [Key Phrases method](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/56f30ceeeda5650db055a3c6).</span></span> <span data-ttu-id="4df82-134">This section of the walkthrough extracts key phrases for both English and Spanish documents.</span><span class="sxs-lookup"><span data-stu-id="4df82-134">This section of the walkthrough extracts key phrases for both English and Spanish documents.</span></span>

<span data-ttu-id="4df82-135">The service endpoint for the key-phrase extraction service is accessed via the following URL:</span><span class="sxs-lookup"><span data-stu-id="4df82-135">The service endpoint for the key-phrase extraction service is accessed via the following URL:</span></span>


```python
key_phrase_api_url = text_analytics_base_url + "keyPhrases"
print(key_phrase_api_url)
```

    https://westcentralus.api.cognitive.microsoft.com/text/analytics/v2.0/keyPhrases


<span data-ttu-id="4df82-136">The collection of documents is the same as what was used for sentiment analysis.</span><span class="sxs-lookup"><span data-stu-id="4df82-136">The collection of documents is the same as what was used for sentiment analysis.</span></span>


```python
documents = {'documents' : [
  {'id': '1', 'language': 'en', 'text': 'I had a wonderful experience! The rooms were wonderful and the staff was helpful.'},
  {'id': '2', 'language': 'en', 'text': 'I had a terrible time at the hotel. The staff was rude and the food was awful.'},  
  {'id': '3', 'language': 'es', 'text': 'Los caminos que llevan hasta Monte Rainier son espectaculares y hermosos.'},  
  {'id': '4', 'language': 'es', 'text': 'La carretera estaba atascada. Había mucho tráfico el día de ayer.'}
]}
headers   = {'Ocp-Apim-Subscription-Key': subscription_key}
response  = requests.post(key_phrase_api_url, headers=headers, json=documents)
key_phrases = response.json()
pprint(key_phrases)
```


    {'documents': [
        {'keyPhrases': ['wonderful experience', 'staff', 'rooms'], 'id': '1'},
        {'keyPhrases': ['food', 'terrible time', 'hotel', 'staff'], 'id': '2'},
        {'keyPhrases': ['Monte Rainier', 'caminos'], 'id': '3'},
        {'keyPhrases': ['carretera', 'tráfico', 'día'], 'id': '4'}],
     'errors': []
    }


<span data-ttu-id="4df82-137">The JSON object can once again be rendered as an HTML table using the following lines of code:</span><span class="sxs-lookup"><span data-stu-id="4df82-137">The JSON object can once again be rendered as an HTML table using the following lines of code:</span></span>


```python
from IPython.display import HTML
table = []
for document in key_phrases["documents"]:
    text    = next(filter(lambda d: d["id"] == document["id"], documents["documents"]))["text"]    
    phrases = ",".join(document["keyPhrases"])
    table.append("<tr><td>{0}</td><td>{1}</td>".format(text, phrases))
HTML("<table><tr><th>Text</th><th>Key phrases</th></tr>{0}</table>".format("\n".join(table)))
```

## <a name="identify-linked-entities"></a><span data-ttu-id="4df82-138">Identify linked entities</span><span class="sxs-lookup"><span data-stu-id="4df82-138">Identify linked entities</span></span>

<span data-ttu-id="4df82-139">The Entity Linking API identifies well-known entities in a text document, using the [Entity Linking method](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/5ac4251d5b4ccd1554da7634).</span><span class="sxs-lookup"><span data-stu-id="4df82-139">The Entity Linking API identifies well-known entities in a text document, using the [Entity Linking method](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/5ac4251d5b4ccd1554da7634).</span></span> <span data-ttu-id="4df82-140">The following example identifies entities for English documents.</span><span class="sxs-lookup"><span data-stu-id="4df82-140">The following example identifies entities for English documents.</span></span>

<span data-ttu-id="4df82-141">The service endpoint for the entity linking service is accessed via the following URL:</span><span class="sxs-lookup"><span data-stu-id="4df82-141">The service endpoint for the entity linking service is accessed via the following URL:</span></span>


```python
entity_linking_api_url = text_analytics_base_url + "entities"
print(entity_linking_api_url)
```

    https://westcentralus.api.cognitive.microsoft.com/text/analytics/v2.0/entities


<span data-ttu-id="4df82-142">The collection of documents is below:</span><span class="sxs-lookup"><span data-stu-id="4df82-142">The collection of documents is below:</span></span>


```python
documents = {'documents' : [
  {'id': '1', 'text': 'I really enjoy the new XBox One S. It has a clean look, it has 4K/HDR resolution and it is affordable.'},
  {'id': '2', 'text': 'The Seattle Seahawks won the Super Bowl in 2014.'}
]}
```

<span data-ttu-id="4df82-143">Now, the documents can be sent to the Text Analytics API to receive the response.</span><span class="sxs-lookup"><span data-stu-id="4df82-143">Now, the documents can be sent to the Text Analytics API to receive the response.</span></span>

```python
headers   = {"Ocp-Apim-Subscription-Key": subscription_key}
response  = requests.post(entity_linking_api_url, headers=headers, json=documents)
entities = response.json()
```
    {
        "documents": [
            {
                "id": "1",
                "entities": [
                    {
                        "name": "Xbox One",
                        "matches": [
                            {
                                "text": "XBox One",
                                "offset": 23,
                                "length": 8
                            }
                        ],
                        "wikipediaLanguage": "en",
                        "wikipediaId": "Xbox One",
                        "wikipediaUrl": "https://en.wikipedia.org/wiki/Xbox_One",
                        "bingId": "446bb4df-4999-4243-84c0-74e0f6c60e75"
                    },
                    {
                        "name": "Ultra-high-definition television",
                        "matches": [
                            {
                                "text": "4K",
                                "offset": 63,
                                "length": 2
                            }
                        ],
                        "wikipediaLanguage": "en",
                        "wikipediaId": "Ultra-high-definition television",
                        "wikipediaUrl": "https://en.wikipedia.org/wiki/Ultra-high-definition_television",
                        "bingId": "7ee02026-b6ec-878b-f4de-f0bc7b0ab8c4"
                    }
                ]
            },
            {
                "id": "2",
                "entities": [
                    {
                        "name": "2013 Seattle Seahawks season",
                        "matches": [
                            {
                                "text": "Seattle Seahawks",
                                "offset": 4,
                                "length": 16
                            }
                        ],
                        "wikipediaLanguage": "en",
                        "wikipediaId": "2013 Seattle Seahawks season",
                        "wikipediaUrl": "https://en.wikipedia.org/wiki/2013_Seattle_Seahawks_season",
                        "bingId": "eb637865-4722-4eca-be9e-0ac0c376d361"
                    }
                ]
            }
        ],
        "errors": []
    }

## <a name="next-steps"></a><span data-ttu-id="4df82-144">Next steps</span><span class="sxs-lookup"><span data-stu-id="4df82-144">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4df82-145">Text Analytics With Power BI</span><span class="sxs-lookup"><span data-stu-id="4df82-145">Text Analytics With Power BI</span></span>](../tutorials/tutorial-power-bi-key-phrases.md)

## <a name="see-also"></a><span data-ttu-id="4df82-146">See also</span><span class="sxs-lookup"><span data-stu-id="4df82-146">See also</span></span> 

 [<span data-ttu-id="4df82-147">Text Analytics overview</span><span class="sxs-lookup"><span data-stu-id="4df82-147">Text Analytics overview</span></span>](../overview.md)  
 [<span data-ttu-id="4df82-148">Frequently asked questions (FAQ)</span><span class="sxs-lookup"><span data-stu-id="4df82-148">Frequently asked questions (FAQ)</span></span>](../text-analytics-resource-faq.md)
