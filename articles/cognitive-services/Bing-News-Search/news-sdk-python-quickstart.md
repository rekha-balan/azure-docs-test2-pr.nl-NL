---
title: News Search SDK Python quickstart | Microsoft Docs
description: Setup for News Search SDK console application.
titleSuffix: Azure News Search SDK Python quickstart
services: cognitive-services
author: mikedodaro
manager: rosh
ms.service: cognitive-services
ms.component: bing-news-search
ms.topic: article
ms.date: 02/14/2018
ms.author: v-gedod
ms.openlocfilehash: 6d212d1477ecf583a038e33e72aab3d60f6aa050
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856665"
---
# <a name="news-search-sdk-python-quickstart"></a><span data-ttu-id="bdd35-103">News Search SDK Python quickstart</span><span class="sxs-lookup"><span data-stu-id="bdd35-103">News Search SDK Python quickstart</span></span>

<span data-ttu-id="bdd35-104">The News Search SDK contains the functionality of the REST API for web queries and parsing results.</span><span class="sxs-lookup"><span data-stu-id="bdd35-104">The News Search SDK contains the functionality of the REST API for web queries and parsing results.</span></span> 

<span data-ttu-id="bdd35-105">The [source code for Python Bing News Search SDK samples](https://github.com/Azure-Samples/cognitive-services-python-sdk-samples/blob/master/samples/search/news_search_samples.py) is available on Git Hub.</span><span class="sxs-lookup"><span data-stu-id="bdd35-105">The [source code for Python Bing News Search SDK samples](https://github.com/Azure-Samples/cognitive-services-python-sdk-samples/blob/master/samples/search/news_search_samples.py) is available on Git Hub.</span></span>

## <a name="application-dependencies"></a><span data-ttu-id="bdd35-106">Application dependencies</span><span class="sxs-lookup"><span data-stu-id="bdd35-106">Application dependencies</span></span>
<span data-ttu-id="bdd35-107">If you don't already have it, install Python.</span><span class="sxs-lookup"><span data-stu-id="bdd35-107">If you don't already have it, install Python.</span></span> <span data-ttu-id="bdd35-108">The SDK is compatible with Python 2.7, 3.3, 3.4, 3.5, and 3.6.</span><span class="sxs-lookup"><span data-stu-id="bdd35-108">The SDK is compatible with Python 2.7, 3.3, 3.4, 3.5, and 3.6.</span></span>

<span data-ttu-id="bdd35-109">The general recommendation for Python development is to use a [virtual environment](https://docs.python.org/3/tutorial/venv.html).</span><span class="sxs-lookup"><span data-stu-id="bdd35-109">The general recommendation for Python development is to use a [virtual environment](https://docs.python.org/3/tutorial/venv.html).</span></span> <span data-ttu-id="bdd35-110">Install and initialize the virtual environment with the [venv module](https://pypi.python.org/pypi/virtualenv).</span><span class="sxs-lookup"><span data-stu-id="bdd35-110">Install and initialize the virtual environment with the [venv module](https://pypi.python.org/pypi/virtualenv).</span></span> <span data-ttu-id="bdd35-111">You must install virtualenv for Python 2.7.</span><span class="sxs-lookup"><span data-stu-id="bdd35-111">You must install virtualenv for Python 2.7.</span></span>
```
python -m venv mytestenv
```
<span data-ttu-id="bdd35-112">Install Bing News Search SDK dependencies:</span><span class="sxs-lookup"><span data-stu-id="bdd35-112">Install Bing News Search SDK dependencies:</span></span>
```
cd mytestenv
python -m pip install azure-cognitiveservices-search-newssearch
```
## <a name="news-search-client"></a><span data-ttu-id="bdd35-113">News Search client</span><span class="sxs-lookup"><span data-stu-id="bdd35-113">News Search client</span></span>
<span data-ttu-id="bdd35-114">Get a [Cognitive Services access key](https://azure.microsoft.com/try/cognitive-services/) under *Search*.</span><span class="sxs-lookup"><span data-stu-id="bdd35-114">Get a [Cognitive Services access key](https://azure.microsoft.com/try/cognitive-services/) under *Search*.</span></span> <span data-ttu-id="bdd35-115">Add imports:</span><span class="sxs-lookup"><span data-stu-id="bdd35-115">Add imports:</span></span>
```
from azure.cognitiveservices.search.newssearch import NewsSearchAPI
from msrest.authentication import CognitiveServicesCredentials

subscription_key = "YOUR-SUBSCRIPTION-KEY"
```
<span data-ttu-id="bdd35-116">Create an instance of `CognitiveServicesCredentials`.</span><span class="sxs-lookup"><span data-stu-id="bdd35-116">Create an instance of `CognitiveServicesCredentials`.</span></span> <span data-ttu-id="bdd35-117">Instantiate the client:</span><span class="sxs-lookup"><span data-stu-id="bdd35-117">Instantiate the client:</span></span>
```
client = NewsSearchAPI(CognitiveServicesCredentials(subscription_key))
```
<span data-ttu-id="bdd35-118">Search for results, and print the first webpage result:</span><span class="sxs-lookup"><span data-stu-id="bdd35-118">Search for results, and print the first webpage result:</span></span>
```
news_result = client.news.search(query="Quantum Computing", market="en-us", count=10)
print("Search news for query \"Quantum Computing\" with market and count")

if news_result.value:
    first_news_result = news_result.value[0]
    print("Total estimated matches value: {}".format(news_result.total_estimated_matches))
    print("News result count: {}".format(len(news_result.value)))
    print("First news name: {}".format(first_news_result.name))
    print("First news url: {}".format(first_news_result.url))
    print("First news description: {}".format(first_news_result.description))
    print("First published time: {}".format(first_news_result.date_published))
    print("First news provider: {}".format(first_news_result.provider[0].name))
else:
    print("Didn't see any news result data..")

```
<span data-ttu-id="bdd35-119">Search with filters for most recent news about "Artificial Intelligence" with `freshness` and `sortBy` parameters.</span><span class="sxs-lookup"><span data-stu-id="bdd35-119">Search with filters for most recent news about "Artificial Intelligence" with `freshness` and `sortBy` parameters.</span></span> <span data-ttu-id="bdd35-120">Verify number of results, and print out `totalEstimatedMatches`, `name`, `url`, `description`, `published time`, and `name of provider` of the first news item result.</span><span class="sxs-lookup"><span data-stu-id="bdd35-120">Verify number of results, and print out `totalEstimatedMatches`, `name`, `url`, `description`, `published time`, and `name of provider` of the first news item result.</span></span>
```
def news_search_with_filtering(subscription_key):

    client = NewsSearchAPI(CognitiveServicesCredentials(subscription_key))

    try:
        news_result = client.news.search(
            query="Artificial Intelligence",
            market="en-us",
            freshness="Week",
            sort_by="Date"
        )
        print("\r\nSearch most recent news for query \"Artificial Intelligence\" with freshness and sortBy")

        if news_result.value:
            first_news_result = news_result.value[0]
            print("News result count: {}".format(len(news_result.value)))
            print("First news name: {}".format(first_news_result.name))
            print("First news url: {}".format(first_news_result.url))
            print("First news description: {}".format(first_news_result.description))
            print("First published time: {}".format(first_news_result.date_published))
            print("First news provider: {}".format(first_news_result.provider[0].name))
        else:
            print("Didn't see any news result data..")

    except Exception as err:
        print("Encountered exception. {}".format(err))

```
<span data-ttu-id="bdd35-121">Search category news for movie and TV entertainment with safe search.</span><span class="sxs-lookup"><span data-stu-id="bdd35-121">Search category news for movie and TV entertainment with safe search.</span></span> <span data-ttu-id="bdd35-122">Verify number of results, and print out `category`, `name`, `url`, `description`, `published time`, and `name of provider` of the first news item result.</span><span class="sxs-lookup"><span data-stu-id="bdd35-122">Verify number of results, and print out `category`, `name`, `url`, `description`, `published time`, and `name of provider` of the first news item result.</span></span>
```
def news_category(subscription_key):

    client = NewsSearchAPI(CognitiveServicesCredentials(subscription_key))

    try:
        news_result = client.news.category(
            category="Entertainment_MovieAndTV",
            market="en-us",
            safe_search="strict"
        )
        print("\r\nSearch category news for movie and TV entertainment with safe search")

        if news_result.value:
            first_news_result = news_result.value[0]
            print("News result count: {}".format(len(news_result.value)))
            print("First news category: {}".format(first_news_result.category))
            print("First news name: {}".format(first_news_result.name))
            print("First news url: {}".format(first_news_result.url))
            print("First news description: {}".format(first_news_result.description))
            print("First published time: {}".format(first_news_result.date_published))
            print("First news provider: {}".format(first_news_result.provider[0].name))
        else:
            print("Didn't see any news result data..")

    except Exception as err:
        print("Encountered exception. {}".format(err))


```
<span data-ttu-id="bdd35-123">Search news trending topics in Bing.</span><span class="sxs-lookup"><span data-stu-id="bdd35-123">Search news trending topics in Bing.</span></span>  <span data-ttu-id="bdd35-124">Verify number of results, and print out `name`, `text of query`, `webSearchUrl`, `newsSearchUrl`, and `image Url` of the first news result.</span><span class="sxs-lookup"><span data-stu-id="bdd35-124">Verify number of results, and print out `name`, `text of query`, `webSearchUrl`, `newsSearchUrl`, and `image Url` of the first news result.</span></span>
```
def news_trending(subscription_key):

    client = NewsSearchAPI(CognitiveServicesCredentials(subscription_key))

    try:
        trending_topics = client.news.trending(market="en-us")
        print("\r\nSearch news trending topics in Bing")

        if trending_topics.value:
            first_topic = trending_topics.value[0]
            print("News result count: {}".format(len(trending_topics.value)))
            print("First topic name: {}".format(first_topic.name))
            print("First topic query: {}".format(first_topic.query.text))
            print("First topic image url: {}".format(first_topic.image.url))
            print("First topic webSearchUrl: {}".format(first_topic.web_search_url))
            print("First topic newsSearchUrl: {}".format(first_topic.news_search_url))
        else:
            print("Didn't see any topics result data..")

    except Exception as err:
        print("Encountered exception. {}".format(err))

```

## <a name="next-steps"></a><span data-ttu-id="bdd35-125">Next steps</span><span class="sxs-lookup"><span data-stu-id="bdd35-125">Next steps</span></span>

[<span data-ttu-id="bdd35-126">Cognitive Services Python SDK samples</span><span class="sxs-lookup"><span data-stu-id="bdd35-126">Cognitive Services Python SDK samples</span></span>](https://github.com/Azure-Samples/cognitive-services-python-sdk-samples)


