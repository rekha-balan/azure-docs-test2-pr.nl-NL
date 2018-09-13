---
title: 'Quickstart: Use the Bing Web Search SDK for Python'
description: Learn how to use the Bing Web Search SDK for Python.
services: cognitive-services
author: erhopf
manager: cgronlun
ms.service: cognitive-services
ms.component: bing-web-search
ms.topic: quickstart
ms.date: 08/16/2018
ms.author: erhopf
ms.openlocfilehash: ff8dc93693a5aec7b6efa3aefd05de8c90f517ed
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866885"
---
# <a name="quickstart-use-the-bing-web-search-sdk-for-python"></a><span data-ttu-id="ee774-103">Quickstart: Use the Bing Web Search SDK for Python</span><span class="sxs-lookup"><span data-stu-id="ee774-103">Quickstart: Use the Bing Web Search SDK for Python</span></span>

<span data-ttu-id="ee774-104">The Bing Web Search SDK makes it easy to integrate Bing Web Search into your Python application.</span><span class="sxs-lookup"><span data-stu-id="ee774-104">The Bing Web Search SDK makes it easy to integrate Bing Web Search into your Python application.</span></span> <span data-ttu-id="ee774-105">In this quickstart, you'll learn how to send a request, receive a JSON response, and filter and parse the results.</span><span class="sxs-lookup"><span data-stu-id="ee774-105">In this quickstart, you'll learn how to send a request, receive a JSON response, and filter and parse the results.</span></span>

<span data-ttu-id="ee774-106">Want to see the code right now?</span><span class="sxs-lookup"><span data-stu-id="ee774-106">Want to see the code right now?</span></span> <span data-ttu-id="ee774-107">The [Bing Web Search SDK for Python samples](https://github.com/Azure-Samples/cognitive-services-python-sdk-samples) are available on GitHub.</span><span class="sxs-lookup"><span data-stu-id="ee774-107">The [Bing Web Search SDK for Python samples](https://github.com/Azure-Samples/cognitive-services-python-sdk-samples) are available on GitHub.</span></span>

[!INCLUDE [bing-web-search-quickstart-signup](../../../includes/bing-web-search-quickstart-signup.md)]

## <a name="prerequisites"></a><span data-ttu-id="ee774-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="ee774-108">Prerequisites</span></span>

<span data-ttu-id="ee774-109">The Bing Web Search SDK is compatible with Python 2.7, 3.3, 3.4, 3.5, and 3.6.</span><span class="sxs-lookup"><span data-stu-id="ee774-109">The Bing Web Search SDK is compatible with Python 2.7, 3.3, 3.4, 3.5, and 3.6.</span></span> <span data-ttu-id="ee774-110">We recommend using a virtual environment for this quickstart.</span><span class="sxs-lookup"><span data-stu-id="ee774-110">We recommend using a virtual environment for this quickstart.</span></span>

* <span data-ttu-id="ee774-111">Python 2.7, 3.3, 3.4, 3.5 or 3.6</span><span class="sxs-lookup"><span data-stu-id="ee774-111">Python 2.7, 3.3, 3.4, 3.5 or 3.6</span></span>
* <span data-ttu-id="ee774-112">[virtualenv](https://docs.python.org/3/tutorial/venv.html) for Python 2.7</span><span class="sxs-lookup"><span data-stu-id="ee774-112">[virtualenv](https://docs.python.org/3/tutorial/venv.html) for Python 2.7</span></span>
* <span data-ttu-id="ee774-113">[venv](https://pypi.python.org/pypi/virtualenv) for Python 3.x</span><span class="sxs-lookup"><span data-stu-id="ee774-113">[venv](https://pypi.python.org/pypi/virtualenv) for Python 3.x</span></span>

## <a name="create-and-configure-your-virtual-environment"></a><span data-ttu-id="ee774-114">Create and configure your virtual environment</span><span class="sxs-lookup"><span data-stu-id="ee774-114">Create and configure your virtual environment</span></span>

<span data-ttu-id="ee774-115">The instructions to set up and configure a virtual environment are different for Python 2.x and Python 3.x.</span><span class="sxs-lookup"><span data-stu-id="ee774-115">The instructions to set up and configure a virtual environment are different for Python 2.x and Python 3.x.</span></span> <span data-ttu-id="ee774-116">Follow the steps below to create and initialize your virtual environment.</span><span class="sxs-lookup"><span data-stu-id="ee774-116">Follow the steps below to create and initialize your virtual environment.</span></span>

### <a name="python-2x"></a><span data-ttu-id="ee774-117">Python 2.x</span><span class="sxs-lookup"><span data-stu-id="ee774-117">Python 2.x</span></span>

<span data-ttu-id="ee774-118">Create a virtual environment with `virtualenv` for Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="ee774-118">Create a virtual environment with `virtualenv` for Python 2.7:</span></span>

```console
virtualenv mytestenv
```

<span data-ttu-id="ee774-119">Activate your environment:</span><span class="sxs-lookup"><span data-stu-id="ee774-119">Activate your environment:</span></span>

```console
cd mytestenv
source bin/activate
```

<span data-ttu-id="ee774-120">Install Bing Web Search SDK dependencies:</span><span class="sxs-lookup"><span data-stu-id="ee774-120">Install Bing Web Search SDK dependencies:</span></span>

```console
python -m pip install azure-cognitiveservices-search-websearch
```

### <a name="python-3x"></a><span data-ttu-id="ee774-121">Python 3.x</span><span class="sxs-lookup"><span data-stu-id="ee774-121">Python 3.x</span></span>

<span data-ttu-id="ee774-122">Create a virtual environment with `venv` for Python 3.x:</span><span class="sxs-lookup"><span data-stu-id="ee774-122">Create a virtual environment with `venv` for Python 3.x:</span></span>

```console
python -m venv mytestenv
```

<span data-ttu-id="ee774-123">Install Bing Web Search SDK dependencies:</span><span class="sxs-lookup"><span data-stu-id="ee774-123">Install Bing Web Search SDK dependencies:</span></span>

```console
cd mytestenv
python -m pip install azure-cognitiveservices-search-websearch
```

## <a name="create-a-client-and-print-your-first-results"></a><span data-ttu-id="ee774-124">Create a client and print your first results</span><span class="sxs-lookup"><span data-stu-id="ee774-124">Create a client and print your first results</span></span>

<span data-ttu-id="ee774-125">Now that you've set up your virtual environment and installed dependencies, let's create a client.</span><span class="sxs-lookup"><span data-stu-id="ee774-125">Now that you've set up your virtual environment and installed dependencies, let's create a client.</span></span> <span data-ttu-id="ee774-126">The client will handle requests to and responses from the Bing Web Search API.</span><span class="sxs-lookup"><span data-stu-id="ee774-126">The client will handle requests to and responses from the Bing Web Search API.</span></span>

<span data-ttu-id="ee774-127">If the response contains web pages, images, news, or videos, the first result for each is printed.</span><span class="sxs-lookup"><span data-stu-id="ee774-127">If the response contains web pages, images, news, or videos, the first result for each is printed.</span></span>

1. <span data-ttu-id="ee774-128">Create a new Python project using your favorite IDE or editor.</span><span class="sxs-lookup"><span data-stu-id="ee774-128">Create a new Python project using your favorite IDE or editor.</span></span>
2. <span data-ttu-id="ee774-129">Copy this sample code into your project:</span><span class="sxs-lookup"><span data-stu-id="ee774-129">Copy this sample code into your project:</span></span>  
    ```python
    # Import required modules.
    from azure.cognitiveservices.search.websearch import WebSearchAPI
    from azure.cognitiveservices.search.websearch.models import SafeSearch
    from msrest.authentication import CognitiveServicesCredentials

    # Replace with your subscription key.
    subscription_key = "YOUR_SUBSCRIPTION_KEY"

    # Instantiate the client.
    client = WebSearchAPI(CognitiveServicesCredentials(subscription_key))

    # Make a request. Replace Yosemite if you'd like.
    web_data = client.web.search(query="Yosemite")
    print("\r\nSearched for Query# \" Yosemite \"")

    '''
    Web pages
    If the search response contains web pages, the first result's name and url
    are printed.
    '''
    if hasattr(web_data.web_pages, 'value'):

        print("\r\nWebpage Results#{}".format(len(web_data.web_pages.value)))

        first_web_page = web_data.web_pages.value[0]
        print("First web page name: {} ".format(first_web_page.name))
        print("First web page URL: {} ".format(first_web_page.url))

    else:
        print("Didn't find any web pages...")

    '''
    Images
    If the search response contains images, the first result's name and url
    are printed.
    '''
    if hasattr(web_data.images, 'value'):

        print("\r\nImage Results#{}".format(len(web_data.images.value)))

        first_image = web_data.images.value[0]
        print("First Image name: {} ".format(first_image.name))
        print("First Image URL: {} ".format(first_image.url))

    else:
        print("Didn't find any images...")

    '''
    News
    If the search response contains news, the first result's name and url
    are printed.
    '''
    if hasattr(web_data.news, 'value'):

        print("\r\nNews Results#{}".format(len(web_data.news.value)))

        first_news = web_data.news.value[0]
        print("First News name: {} ".format(first_news.name))
        print("First News URL: {} ".format(first_news.url))

    else:
        print("Didn't find any news...")

    '''
    If the search response contains videos, the first result's name and url
    are printed.
    '''
    if hasattr(web_data.videos, 'value'):

        print("\r\nVideos Results#{}".format(len(web_data.videos.value)))

        first_video = web_data.videos.value[0]
        print("First Videos name: {} ".format(first_video.name))
        print("First Videos URL: {} ".format(first_video.url))

    else:
        print("Didn't find any videos...")
    ```
3. <span data-ttu-id="ee774-130">Replace `subscription_key` with a valid subscription key.</span><span class="sxs-lookup"><span data-stu-id="ee774-130">Replace `subscription_key` with a valid subscription key.</span></span>
4. <span data-ttu-id="ee774-131">Run the program.</span><span class="sxs-lookup"><span data-stu-id="ee774-131">Run the program.</span></span> <span data-ttu-id="ee774-132">For example: `python your_program.py`.</span><span class="sxs-lookup"><span data-stu-id="ee774-132">For example: `python your_program.py`.</span></span>

## <a name="define-functions-and-filter-results"></a><span data-ttu-id="ee774-133">Define functions and filter results</span><span class="sxs-lookup"><span data-stu-id="ee774-133">Define functions and filter results</span></span>

<span data-ttu-id="ee774-134">Now that you've made your first call to the Bing Web Search API, let's look at a few functions that highlight SDK functionality for refining queries and filtering results.</span><span class="sxs-lookup"><span data-stu-id="ee774-134">Now that you've made your first call to the Bing Web Search API, let's look at a few functions that highlight SDK functionality for refining queries and filtering results.</span></span> <span data-ttu-id="ee774-135">Each function can be added to your Python program that was created in the previous section.</span><span class="sxs-lookup"><span data-stu-id="ee774-135">Each function can be added to your Python program that was created in the previous section.</span></span>

### <a name="limit-the-number-of-results-returned-by-bing"></a><span data-ttu-id="ee774-136">Limit the number of results returned by Bing</span><span class="sxs-lookup"><span data-stu-id="ee774-136">Limit the number of results returned by Bing</span></span>

<span data-ttu-id="ee774-137">This sample uses the `count` and `offset` parameters to limit the number of results returned using the SDK's [`search` method](https://docs.microsoft.com/python/api/azure-cognitiveservices-search-websearch/azure.cognitiveservices.search.websearch.operations.weboperations?view=azure-python#search).</span><span class="sxs-lookup"><span data-stu-id="ee774-137">This sample uses the `count` and `offset` parameters to limit the number of results returned using the SDK's [`search` method](https://docs.microsoft.com/python/api/azure-cognitiveservices-search-websearch/azure.cognitiveservices.search.websearch.operations.weboperations?view=azure-python#search).</span></span> <span data-ttu-id="ee774-138">The `name` and `URL` for the first result are printed.</span><span class="sxs-lookup"><span data-stu-id="ee774-138">The `name` and `URL` for the first result are printed.</span></span>

1. <span data-ttu-id="ee774-139">Add this code to your Python project:</span><span class="sxs-lookup"><span data-stu-id="ee774-139">Add this code to your Python project:</span></span>
    ```python
    # Declare the function.
    def web_results_with_count_and_offset(subscription_key):
        client = WebSearchAPI(CognitiveServicesCredentials(subscription_key))

        try:
            '''
            Set the query, offset, and count using the SDK's search method. See:
            https://docs.microsoft.com/python/api/azure-cognitiveservices-search-websearch/azure.cognitiveservices.search.websearch.operations.weboperations?view=azure-python#search.
            '''
            web_data = client.web.search(query="Best restaurants in Seattle", offset=10, count=20)
            print("\r\nSearching for \"Best restaurants in Seattle\"")

            if web_data.web_pages.value:
                '''
                If web pages are available, print the # of responses, and the first and second
                web pages returned.
                '''
                print("Webpage Results#{}".format(len(web_data.web_pages.value)))

                first_web_page = web_data.web_pages.value[0]
                print("First web page name: {} ".format(first_web_page.name))
                print("First web page URL: {} ".format(first_web_page.url))

            else:
                print("Didn't find any web pages...")

        except Exception as err:
            print("Encountered exception. {}".format(err))
    ```
2. <span data-ttu-id="ee774-140">Run the program.</span><span class="sxs-lookup"><span data-stu-id="ee774-140">Run the program.</span></span>

### <a name="filter-for-news-and-freshness"></a><span data-ttu-id="ee774-141">Filter for news and freshness</span><span class="sxs-lookup"><span data-stu-id="ee774-141">Filter for news and freshness</span></span>

<span data-ttu-id="ee774-142">This sample uses the `response_filter` and `freshness` parameters to filter search results using the SDK's [`search` method](https://docs.microsoft.com//api/azure-cognitiveservices-search-websearch/azure.cognitiveservices.search.websearch.operations.weboperations?view=azure-python#search).</span><span class="sxs-lookup"><span data-stu-id="ee774-142">This sample uses the `response_filter` and `freshness` parameters to filter search results using the SDK's [`search` method](https://docs.microsoft.com//api/azure-cognitiveservices-search-websearch/azure.cognitiveservices.search.websearch.operations.weboperations?view=azure-python#search).</span></span> <span data-ttu-id="ee774-143">The search results returned are limited to news articles and pages that Bing has discovered within the last 24 hours.</span><span class="sxs-lookup"><span data-stu-id="ee774-143">The search results returned are limited to news articles and pages that Bing has discovered within the last 24 hours.</span></span> <span data-ttu-id="ee774-144">The `name` and `URL` for the first result are printed.</span><span class="sxs-lookup"><span data-stu-id="ee774-144">The `name` and `URL` for the first result are printed.</span></span>

1. <span data-ttu-id="ee774-145">Add this code to your Python project:</span><span class="sxs-lookup"><span data-stu-id="ee774-145">Add this code to your Python project:</span></span>
    ```python
    # Declare the function.
    def web_search_with_response_filter(subscription_key):
        client = WebSearchAPI(CognitiveServicesCredentials(subscription_key))
        try:
            '''
            Set the query, response_filter, and freshness using the SDK's search method. See:
            https://docs.microsoft.com/python/api/azure-cognitiveservices-search-websearch/azure.cognitiveservices.search.websearch.operations.weboperations?view=azure-python#search.
            '''
            web_data = client.web.search(query="xbox",
                response_filter=["News"],
                freshness="Day")
            print("\r\nSearching for \"xbox\" with the response filter set to \"News\" and freshness filter set to \"Day\".")

            '''
            If news articles are available, print the # of responses, and the first and second
            articles returned.
            '''
            if web_data.news.value:

                print("# of news results: {}".format(len(web_data.news.value)))

                first_web_page = web_data.news.value[0]
                print("First article name: {} ".format(first_web_page.name))
                print("First article URL: {} ".format(first_web_page.url))

                print("")

                second_web_page = web_data.news.value[1]
                print("\nSecond article name: {} ".format(second_web_page.name))
                print("Second article URL: {} ".format(second_web_page.url))

            else:
                print("Didn't find any news articles...")

        except Exception as err:
            print("Encountered exception. {}".format(err))

    # Call the function.
    web_search_with_response_filter(subscription_key)
    ```
2. <span data-ttu-id="ee774-146">Run the program.</span><span class="sxs-lookup"><span data-stu-id="ee774-146">Run the program.</span></span>

### <a name="use-safe-search-answer-count-and-the-promote-filter"></a><span data-ttu-id="ee774-147">Use safe search, answer count, and the promote filter</span><span class="sxs-lookup"><span data-stu-id="ee774-147">Use safe search, answer count, and the promote filter</span></span>

<span data-ttu-id="ee774-148">This sample uses the `answer_count`, `promote`, and `safe_search` parameters to filter search results using the SDK's [`search` method](https://docs.microsoft.com/python/api/azure-cognitiveservices-search-websearch/azure.cognitiveservices.search.websearch.operations.weboperations?view=azure-python#search).</span><span class="sxs-lookup"><span data-stu-id="ee774-148">This sample uses the `answer_count`, `promote`, and `safe_search` parameters to filter search results using the SDK's [`search` method](https://docs.microsoft.com/python/api/azure-cognitiveservices-search-websearch/azure.cognitiveservices.search.websearch.operations.weboperations?view=azure-python#search).</span></span> <span data-ttu-id="ee774-149">The `name` and `URL` for the first result are displayed.</span><span class="sxs-lookup"><span data-stu-id="ee774-149">The `name` and `URL` for the first result are displayed.</span></span>

1. <span data-ttu-id="ee774-150">Add this code to your Python project:</span><span class="sxs-lookup"><span data-stu-id="ee774-150">Add this code to your Python project:</span></span>
    ```python
    # Declare the function.
    def web_search_with_answer_count_promote_and_safe_search(subscription_key):

        client = WebSearchAPI(CognitiveServicesCredentials(subscription_key))

        try:
            '''
            Set the query, answer_count, promote, and safe_search parameters using the SDK's search method. See:
            https://docs.microsoft.com/python/api/azure-cognitiveservices-search-websearch/azure.cognitiveservices.search.websearch.operations.weboperations?view=azure-python#search.
            '''
            web_data = client.web.search(
                query="Niagara Falls",
                answer_count=2,
                promote=["videos"],
                safe_search=SafeSearch.strict  # or directly "Strict"
            )
            print("\r\nSearching for \"Niagara Falls\"")

            '''
            If results are available, print the # of responses, and the first result returned.
            '''
            if web_data.web_pages.value:

                print("Webpage Results#{}".format(len(web_data.web_pages.value)))

                first_web_page = web_data.web_pages.value[0]
                print("First web page name: {} ".format(first_web_page.name))
                print("First web page URL: {} ".format(first_web_page.url))

            else:
                print("Didn't see any Web data..")

        except Exception as err:
            print("Encountered exception. {}".format(err))
    ```
2. <span data-ttu-id="ee774-151">Run the program.</span><span class="sxs-lookup"><span data-stu-id="ee774-151">Run the program.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="ee774-152">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="ee774-152">Clean up resources</span></span>

<span data-ttu-id="ee774-153">When you're done with this project, make sure to remove your subscription key from the program's code and to deactivate your virtual environment.</span><span class="sxs-lookup"><span data-stu-id="ee774-153">When you're done with this project, make sure to remove your subscription key from the program's code and to deactivate your virtual environment.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ee774-154">Next steps</span><span class="sxs-lookup"><span data-stu-id="ee774-154">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ee774-155">Cognitive Services Python SDK samples</span><span class="sxs-lookup"><span data-stu-id="ee774-155">Cognitive Services Python SDK samples</span></span>](https://github.com/Azure-Samples/cognitive-services-python-sdk-samples)

## <a name="see-also"></a><span data-ttu-id="ee774-156">See also</span><span class="sxs-lookup"><span data-stu-id="ee774-156">See also</span></span>

* [<span data-ttu-id="ee774-157">Azure Python SDK reference</span><span class="sxs-lookup"><span data-stu-id="ee774-157">Azure Python SDK reference</span></span>](https://docs.microsoft.com/python/api/overview/azure/cognitiveservices/websearch)
