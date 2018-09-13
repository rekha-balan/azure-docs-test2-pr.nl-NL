---
title: Visual search SDK Python Quickstart | Microsoft Docs
description: Setup for Visual search SDK Python console application.
titleSuffix: Azure Cognitive Services
services: cognitive-services
author: mikedodaro
manager: rosh
ms.service: cognitive-services
ms.component: bing-web-search
ms.topic: article
ms.date: 06/11/2018
ms.author: v-gedod
ms.openlocfilehash: f7a1f275f9059abdceaef577fb5ca722c9951366
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865690"
---
# <a name="visual-search-sdk-python-quickstart"></a><span data-ttu-id="cfc76-103">Visual Search SDK Python Quickstart</span><span class="sxs-lookup"><span data-stu-id="cfc76-103">Visual Search SDK Python Quickstart</span></span>

<span data-ttu-id="cfc76-104">The Bing Visual Search SDK uses the functionality of the REST API for web requests and parsing results.</span><span class="sxs-lookup"><span data-stu-id="cfc76-104">The Bing Visual Search SDK uses the functionality of the REST API for web requests and parsing results.</span></span>
<span data-ttu-id="cfc76-105">The [source code for Python Bing Visual Search SDK samples](https://github.com/Azure-Samples/cognitive-services-python-sdk-samples/blob/master/samples/search/visual_search_samples.py) is available on Git Hub.</span><span class="sxs-lookup"><span data-stu-id="cfc76-105">The [source code for Python Bing Visual Search SDK samples](https://github.com/Azure-Samples/cognitive-services-python-sdk-samples/blob/master/samples/search/visual_search_samples.py) is available on Git Hub.</span></span>

<span data-ttu-id="cfc76-106">Code scenarios are documented under the following headings:</span><span class="sxs-lookup"><span data-stu-id="cfc76-106">Code scenarios are documented under the following headings:</span></span>
* [<span data-ttu-id="cfc76-107">Visual Search Client</span><span class="sxs-lookup"><span data-stu-id="cfc76-107">Visual Search Client</span></span>](#client)
* [<span data-ttu-id="cfc76-108">Complete console application</span><span class="sxs-lookup"><span data-stu-id="cfc76-108">Complete console application</span></span>](#complete-console)
* [<span data-ttu-id="cfc76-109">Image binary post with cropArea</span><span class="sxs-lookup"><span data-stu-id="cfc76-109">Image binary post with cropArea</span></span>](#binary-crop)
* [<span data-ttu-id="cfc76-110">KnowledgeRequest parameter</span><span class="sxs-lookup"><span data-stu-id="cfc76-110">KnowledgeRequest parameter</span></span>](#knowledge-req)
* [<span data-ttu-id="cfc76-111">Tags, actions, and actionType</span><span class="sxs-lookup"><span data-stu-id="cfc76-111">Tags, actions, and actionType</span></span>](#tags-actions)

## <a name="application-dependencies"></a><span data-ttu-id="cfc76-112">Application dependencies</span><span class="sxs-lookup"><span data-stu-id="cfc76-112">Application dependencies</span></span>
* <span data-ttu-id="cfc76-113">A cognitive services API key is required to authenticate SDK calls.</span><span class="sxs-lookup"><span data-stu-id="cfc76-113">A cognitive services API key is required to authenticate SDK calls.</span></span> <span data-ttu-id="cfc76-114">Sign up for a [free trial key](https://azure.microsoft.com/try/cognitive-services/?api=search-api-v7).</span><span class="sxs-lookup"><span data-stu-id="cfc76-114">Sign up for a [free trial key](https://azure.microsoft.com/try/cognitive-services/?api=search-api-v7).</span></span> <span data-ttu-id="cfc76-115">The trial key is good for seven days with 1 call per second.</span><span class="sxs-lookup"><span data-stu-id="cfc76-115">The trial key is good for seven days with 1 call per second.</span></span> <span data-ttu-id="cfc76-116">For production scenario, [buy access key](https://portal.azure.com/#create/Microsoft.CognitiveServicesBingSearch-v7).</span><span class="sxs-lookup"><span data-stu-id="cfc76-116">For production scenario, [buy access key](https://portal.azure.com/#create/Microsoft.CognitiveServicesBingSearch-v7).</span></span> <span data-ttu-id="cfc76-117">See also [pricing information](https://azure.microsoft.com/pricing/details/cognitive-services/search-api/visual/).</span><span class="sxs-lookup"><span data-stu-id="cfc76-117">See also [pricing information](https://azure.microsoft.com/pricing/details/cognitive-services/search-api/visual/).</span></span>
* <span data-ttu-id="cfc76-118">If you don't already have it, install Python.</span><span class="sxs-lookup"><span data-stu-id="cfc76-118">If you don't already have it, install Python.</span></span> <span data-ttu-id="cfc76-119">The SDK is compatible with Python 2.7, 3.3, 3.4, 3.5 and 3.6.</span><span class="sxs-lookup"><span data-stu-id="cfc76-119">The SDK is compatible with Python 2.7, 3.3, 3.4, 3.5 and 3.6.</span></span>
* <span data-ttu-id="cfc76-120">The general recommendation for Python development is to use a [virtual environment](https://docs.python.org/3/tutorial/venv.html).</span><span class="sxs-lookup"><span data-stu-id="cfc76-120">The general recommendation for Python development is to use a [virtual environment](https://docs.python.org/3/tutorial/venv.html).</span></span> <span data-ttu-id="cfc76-121">Install and initialize the virtual environment with the [venv module](https://pypi.python.org/pypi/virtualenv).</span><span class="sxs-lookup"><span data-stu-id="cfc76-121">Install and initialize the virtual environment with the [venv module](https://pypi.python.org/pypi/virtualenv).</span></span> <span data-ttu-id="cfc76-122">Install virtualenv for Python 2.7.</span><span class="sxs-lookup"><span data-stu-id="cfc76-122">Install virtualenv for Python 2.7.</span></span>
```
python -m venv mytestenv
```
<span data-ttu-id="cfc76-123">Install Bing Visual Search SDK dependencies:</span><span class="sxs-lookup"><span data-stu-id="cfc76-123">Install Bing Visual Search SDK dependencies:</span></span>
```
cd mytestenv
python -m pip install azure-cognitiveservices-search-visualsearch
```

<a name="client"></a> 
## <a name="visual-search-client"></a><span data-ttu-id="cfc76-124">Visual Search client</span><span class="sxs-lookup"><span data-stu-id="cfc76-124">Visual Search client</span></span>
<span data-ttu-id="cfc76-125">To create an instance of the `VisualSearchAPI` client, import the following libraries:</span><span class="sxs-lookup"><span data-stu-id="cfc76-125">To create an instance of the `VisualSearchAPI` client, import the following libraries:</span></span>
```
import http.client, urllib.parse
import json
import os.path
from azure.cognitiveservices.search.visualsearch import VisualSearchAPI
from azure.cognitiveservices.search.visualsearch.models import (
    VisualSearchRequest,
    CropArea,
    ImageInfo,
    Filters,
    KnowledgeRequest,
)
```
<span data-ttu-id="cfc76-126">Replace the subscriptionKey string value with your valid subscription key.</span><span class="sxs-lookup"><span data-stu-id="cfc76-126">Replace the subscriptionKey string value with your valid subscription key.</span></span>
```
subscription_key = 'YOUR-VISUAL-SEARCH-ACCESS-KEY'
```
<span data-ttu-id="cfc76-127">Then, instantiate the client:</span><span class="sxs-lookup"><span data-stu-id="cfc76-127">Then, instantiate the client:</span></span>
```
var client = new WebSearchAPI(new ApiKeyServiceClientCredentials("YOUR-ACCESS-KEY"));
```
<span data-ttu-id="cfc76-128">Use the client to search images and parse results:</span><span class="sxs-lookup"><span data-stu-id="cfc76-128">Use the client to search images and parse results:</span></span>
```
PATH = 'C:\\Users\\USER\\azure-cognitive-samples\\mytestenv\\TestImages\\'
image_path = os.path.join(PATH, "image.jpg")

with open(image_path, "rb") as image_fd:

    # You need to pass the serialized form of the model
    knowledge_request = json.dumps(VisualSearchRequest().serialize())

    print("\r\nSearch visual search request with binary of dog image")
    result = client.images.visual_search(image=image_fd, knowledge_request=knowledge_request)
        
    if not result:
        print("No visual search result data.")

        # Visual Search results
    if result.image.image_insights_token:
        print("Uploaded image insights token: {}".format(result.image.image_insights_token))
    else:
        print("Couldn't find image insights token!")

    # List of tags
    if result.tags:
        first_tag = result.tags[0]
        print("Visual search tag count: {}".format(len(result.tags)))

        # List of actions in first tag
        if first_tag.actions:
            first_tag_action = first_tag.actions[0]
            print("First tag action count: {}".format(len(first_tag.actions)))
            print("First tag action type: {}".format(first_tag_action.action_type))
        else:
            print("Couldn't find tag actions!")
    else:
        print("Couldn't find image tags!")

```

<a name="complete-console"></a> 
## <a name="complete-console-application"></a><span data-ttu-id="cfc76-129">Complete console application</span><span class="sxs-lookup"><span data-stu-id="cfc76-129">Complete console application</span></span>

<span data-ttu-id="cfc76-130">The following console application executes the previously defined query and parses the results:</span><span class="sxs-lookup"><span data-stu-id="cfc76-130">The following console application executes the previously defined query and parses the results:</span></span>
```
import http.client, urllib.parse
import json
import os.path

# Replace the subscriptionKey string value with your valid subscription key.
subscription_key = 'YOUR-VISUAL-SEARCH-ACCESS-KEY'

PATH = 'C:\\Users\\v-gedod\\azure-cognitive-samples\\mytestenv\\TestImages\\'

from azure.cognitiveservices.search.visualsearch import VisualSearchAPI
from azure.cognitiveservices.search.visualsearch.models import (
    VisualSearchRequest,
    CropArea,
    ImageInfo,
    Filters,
    KnowledgeRequest,)

from msrest.authentication import CognitiveServicesCredentials

client = VisualSearchAPI(CognitiveServicesCredentials(subscription_key))

image_path = os.path.join(PATH, "image.jpg")

with open(image_path, "rb") as image_fd:

    # You need to pass the serialized form of the model
    knowledge_request = json.dumps(VisualSearchRequest().serialize())

    print("\r\nSearch visual search request with binary of dog image")
    result = client.images.visual_search(image=image_fd, knowledge_request=knowledge_request)
        
    if not result:
        print("No visual search result data.")

        # Visual Search results
    if result.image.image_insights_token:
        print("Uploaded image insights token: {}".format(result.image.image_insights_token))
    else:
        print("Couldn't find image insights token!")

    # List of tags
    if result.tags:
        first_tag = result.tags[0]
        print("Visual search tag count: {}".format(len(result.tags)))

        # List of actions in first tag
        if first_tag.actions:
            first_tag_action = first_tag.actions[0]
            print("First tag action count: {}".format(len(first_tag.actions)))
            print("First tag action type: {}".format(first_tag_action.action_type))
        else:
            print("Couldn't find tag actions!")
    else:
        print("Couldn't find image tags!")


# Uncomment these methods to include code under the following headings of this documentation.
#search_image_binary_with_crop_area(client, subscription_key, PATH)
#search_url_with_filters(client, subscription_key)
#search_insights_token_with_crop_area(client, subscription_key)

```

<span data-ttu-id="cfc76-131">The Bing search samples demonstrate various features of the SDK.</span><span class="sxs-lookup"><span data-stu-id="cfc76-131">The Bing search samples demonstrate various features of the SDK.</span></span>  <span data-ttu-id="cfc76-132">Add the following functions to the previously defined `VisualSrchSDK` class.</span><span class="sxs-lookup"><span data-stu-id="cfc76-132">Add the following functions to the previously defined `VisualSrchSDK` class.</span></span>

<a name="binary-crop"></a>
## <a name="image-binary-post-with-croparea"></a><span data-ttu-id="cfc76-133">Image binary post with cropArea</span><span class="sxs-lookup"><span data-stu-id="cfc76-133">Image binary post with cropArea</span></span>

<span data-ttu-id="cfc76-134">The following code sends an image binary in the body of the post request, along with a cropArea object.</span><span class="sxs-lookup"><span data-stu-id="cfc76-134">The following code sends an image binary in the body of the post request, along with a cropArea object.</span></span>  <span data-ttu-id="cfc76-135">Then it prints the imageInsightsToken, the number of tags, the number of actions, and the first actionType.</span><span class="sxs-lookup"><span data-stu-id="cfc76-135">Then it prints the imageInsightsToken, the number of tags, the number of actions, and the first actionType.</span></span>

```
def search_image_binary_with_crop_area(client, sub_key, file_path):

    #client = VisualSearchAPI(CognitiveServicesCredentials(sub_key))

    image_path = os.path.join(file_path, "image.jpg")
    with open(image_path, "rb") as image_fd:

        crop_area = CropArea(top=0.1,bottom=0.5,left=0.1,right=0.9)
        knowledge_request = VisualSearchRequest(image_info=ImageInfo(crop_area=crop_area))

        # You need to pass the serialized form of the model
        knowledge_request = json.dumps(knowledge_request.serialize())

        print("\r\nSearch visual search request with binary of dog image")
        result = client.images.visual_search(image=image_fd, knowledge_request=knowledge_request)

        if not result:
            print("No visual search result data.")
            return

        # Visual Search results
        if result.image.image_insights_token:
            print("Uploaded image insights token: {}".format(result.image.image_insights_token))
        else:
            print("Couldn't find image insights token!")

        # List of tags
        if result.tags:
            first_tag = result.tags[0]
            print("Visual search tag count: {}".format(len(result.tags)))

            # List of actions in first tag
            if first_tag.actions:
                first_tag_action = first_tag.actions[0]
                print("First tag action count: {}".format(len(first_tag.actions)))
                print("First tag action type: {}".format(first_tag_action.action_type))
            else:
                print("Couldn't find tag actions!")
        else:
            print("Couldn't find image tags!")


```
<a name="knowledge-req"></a>
## <a name="knowledgerequest-parameter"></a><span data-ttu-id="cfc76-136">KnowledgeRequest parameter</span><span class="sxs-lookup"><span data-stu-id="cfc76-136">KnowledgeRequest parameter</span></span>

<span data-ttu-id="cfc76-137">The following code sends an image url in the `knowledgeRequest` parameter, along with a \"site:www.bing.com\" filter.</span><span class="sxs-lookup"><span data-stu-id="cfc76-137">The following code sends an image url in the `knowledgeRequest` parameter, along with a \"site:www.bing.com\" filter.</span></span> <span data-ttu-id="cfc76-138">Then it prints the `imageInsightsToken`, the number of tags, the number of actions, and the first actionType.</span><span class="sxs-lookup"><span data-stu-id="cfc76-138">Then it prints the `imageInsightsToken`, the number of tags, the number of actions, and the first actionType.</span></span>
```
def search_url_with_filters(client_in, sub_key):

    client = client_in

    image_url = "https://images.unsplash.com/photo-1512546148165-e50d714a565a?w=600&q=80"
    filters = Filters(site="www.bing.com")

    knowledge_request = VisualSearchRequest(
        image_info=ImageInfo(url=image_url),
        knowledge_request=KnowledgeRequest(filters=filters)
    )

    # You need to pass the serialized form of the model
    knowledge_request = json.dumps(knowledge_request.serialize())

    print("\r\nSearch visual search request with url of dog image")
    result = client.images.visual_search(knowledge_request=knowledge_request)

    if not result:
        print("No visual search result data.")
        return

    # Visual Search results
    if result.image.image_insights_token:
        print("Uploaded image insights token: {}".format(result.image.image_insights_token))
    else:
        print("Couldn't find image insights token!")

    # List of tags
    if result.tags:
        first_tag = result.tags[0]
        print("Visual search tag count: {}".format(len(result.tags)))

        # List of actions in first tag
        if first_tag.actions:
            first_tag_action = first_tag.actions[0]
            print("First tag action count: {}".format(len(first_tag.actions)))
            print("First tag action type: {}".format(first_tag_action.action_type))
        else:
            print("Couldn't find tag actions!")
    else:
        print("Couldn't find image tags!")

```
<a name="tags-actions"></a>
## <a name="tags-actions-and-actiontype"></a><span data-ttu-id="cfc76-139">Tags, actions, and actionType</span><span class="sxs-lookup"><span data-stu-id="cfc76-139">Tags, actions, and actionType</span></span>

<span data-ttu-id="cfc76-140">The following code sends an image insights token in the knowledgeRequest parameter, along with a cropArea object.</span><span class="sxs-lookup"><span data-stu-id="cfc76-140">The following code sends an image insights token in the knowledgeRequest parameter, along with a cropArea object.</span></span> <span data-ttu-id="cfc76-141">Then it prints the imageInsightsToken, the number of tags, the number of actions, and the first actionType.</span><span class="sxs-lookup"><span data-stu-id="cfc76-141">Then it prints the imageInsightsToken, the number of tags, the number of actions, and the first actionType.</span></span>

```
    client = client_in

    image_insights_token = "bcid_113F29C079F18F385732D8046EC80145*ccid_oV/QcH95*mid_687689FAFA449B35BC11A1AE6CEAB6F9A9B53708*thid_R.113F29C079F18F385732D8046EC80145"
    crop_area = CropArea(top=0.1,bottom=0.5,left=0.1,right=0.9)

    knowledge_request = VisualSearchRequest(
        image_info=ImageInfo(
            image_insights_token=image_insights_token,
            crop_area=crop_area
        ),
    )

    # You need to pass the serialized form of the model
    knowledge_request = json.dumps(knowledge_request.serialize())

    print("\r\nSearch visual search request with URL of dog image")
    result = client.images.visual_search(knowledge_request=knowledge_request)

    if not result:
        print("No visual search result data.")
        return

    # Visual Search results
    if result.image.image_insights_token:
        print("Uploaded image insights token: {}".format(result.image.image_insights_token))
    else:
        print("Couldn't find image insights token!")

    # List of tags
    if result.tags:
        first_tag = result.tags[0]
        print("Visual search tag count: {}".format(len(result.tags)))

        # List of actions in first tag
        if first_tag.actions:
            first_tag_action = first_tag.actions[0]
            print("First tag action count: {}".format(len(first_tag.actions)))
            print("First tag action type: {}".format(first_tag_action.action_type))
        else:
            print("Couldn't find tag actions!")
    else:
        print("Couldn't find image tags!")
```

## <a name="next-steps"></a><span data-ttu-id="cfc76-142">Next steps</span><span class="sxs-lookup"><span data-stu-id="cfc76-142">Next steps</span></span>

<span data-ttu-id="cfc76-143">[Cognitive services .NET SDK samples](https://github.com/Azure-Samples/cognitive-services-dotnet-sdk-samples/tree/master/BingSearchv7).</span><span class="sxs-lookup"><span data-stu-id="cfc76-143">[Cognitive services .NET SDK samples](https://github.com/Azure-Samples/cognitive-services-dotnet-sdk-samples/tree/master/BingSearchv7).</span></span>