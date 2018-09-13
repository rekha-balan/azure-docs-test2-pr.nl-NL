---
title: Python Quickstart for Bing Visual Search API | Microsoft Docs
titleSuffix: Bing Web Search APIs - Cognitive Services
description: Shows how to upload an image to Bing Visual Search API and get back insights about the image.
services: cognitive-services
author: swhite-msft
manager: rosh
ms.service: cognitive-services
ms.technology: bing-visual-search
ms.topic: article
ms.date: 5/16/2018
ms.author: scottwhi
ms.openlocfilehash: 96bd94e37c75d10726245fbcea7044d4ae2ed07e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866772"
---
# <a name="your-first-bing-visual-search-query-in-python"></a><span data-ttu-id="8c814-103">Your first Bing Visual Search query in Python</span><span class="sxs-lookup"><span data-stu-id="8c814-103">Your first Bing Visual Search query in Python</span></span>

<span data-ttu-id="8c814-104">Bing Visual Search API returns information about an image that you provide.</span><span class="sxs-lookup"><span data-stu-id="8c814-104">Bing Visual Search API returns information about an image that you provide.</span></span> <span data-ttu-id="8c814-105">You can provide the image by using the URL of the image, an insights token, or by uploading an image.</span><span class="sxs-lookup"><span data-stu-id="8c814-105">You can provide the image by using the URL of the image, an insights token, or by uploading an image.</span></span> <span data-ttu-id="8c814-106">For information about these options, see [What is Bing Visual Search API?](../overview.md)</span><span class="sxs-lookup"><span data-stu-id="8c814-106">For information about these options, see [What is Bing Visual Search API?](../overview.md)</span></span> <span data-ttu-id="8c814-107">This article demonstrates uploading an image.</span><span class="sxs-lookup"><span data-stu-id="8c814-107">This article demonstrates uploading an image.</span></span> <span data-ttu-id="8c814-108">Uploading an image could be useful in mobile scenarios where you take a picture of a well-known landmark and get back information about it.</span><span class="sxs-lookup"><span data-stu-id="8c814-108">Uploading an image could be useful in mobile scenarios where you take a picture of a well-known landmark and get back information about it.</span></span> <span data-ttu-id="8c814-109">For example, the insights could include trivia about the landmark.</span><span class="sxs-lookup"><span data-stu-id="8c814-109">For example, the insights could include trivia about the landmark.</span></span> 

<span data-ttu-id="8c814-110">If you upload a local image, the following shows the form data you must include in the body of the POST.</span><span class="sxs-lookup"><span data-stu-id="8c814-110">If you upload a local image, the following shows the form data you must include in the body of the POST.</span></span> <span data-ttu-id="8c814-111">The form data must include the Content-Disposition header.</span><span class="sxs-lookup"><span data-stu-id="8c814-111">The form data must include the Content-Disposition header.</span></span> <span data-ttu-id="8c814-112">Its `name` parameter must be set to "image" and the `filename` parameter may be set to any string.</span><span class="sxs-lookup"><span data-stu-id="8c814-112">Its `name` parameter must be set to "image" and the `filename` parameter may be set to any string.</span></span> <span data-ttu-id="8c814-113">The contents of the form is the binary of the image.</span><span class="sxs-lookup"><span data-stu-id="8c814-113">The contents of the form is the binary of the image.</span></span> <span data-ttu-id="8c814-114">The maximum image size you may upload is 1 MB.</span><span class="sxs-lookup"><span data-stu-id="8c814-114">The maximum image size you may upload is 1 MB.</span></span> 

```
--boundary_1234-abcd
Content-Disposition: form-data; name="image"; filename="myimagefile.jpg"

ÿØÿà JFIF ÖÆ68g-¤CWŸþ29ÌÄøÖ‘º«™æ±èuZiÀ)"óÓß°Î= ØJ9á+*G¦...

--boundary_1234-abcd--
```

<span data-ttu-id="8c814-115">This article includes a simple console application that sends a Bing Visual Search API request and displays the JSON search results.</span><span class="sxs-lookup"><span data-stu-id="8c814-115">This article includes a simple console application that sends a Bing Visual Search API request and displays the JSON search results.</span></span> <span data-ttu-id="8c814-116">While this application is written in Python, the API is a RESTful Web service compatible with any programming language that can make HTTP requests and parse JSON.</span><span class="sxs-lookup"><span data-stu-id="8c814-116">While this application is written in Python, the API is a RESTful Web service compatible with any programming language that can make HTTP requests and parse JSON.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="8c814-117">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="8c814-117">Prerequisites</span></span>

<span data-ttu-id="8c814-118">You need [Python 3](https://www.python.org/) to run this code.</span><span class="sxs-lookup"><span data-stu-id="8c814-118">You need [Python 3](https://www.python.org/) to run this code.</span></span>

<span data-ttu-id="8c814-119">For this quickstart, you may use a [free trial](https://azure.microsoft.com/try/cognitive-services/?api=bing-web-search-api) subscription key or a paid subscription key.</span><span class="sxs-lookup"><span data-stu-id="8c814-119">For this quickstart, you may use a [free trial](https://azure.microsoft.com/try/cognitive-services/?api=bing-web-search-api) subscription key or a paid subscription key.</span></span>

## <a name="running-the-walkthrough"></a><span data-ttu-id="8c814-120">Running the walkthrough</span><span class="sxs-lookup"><span data-stu-id="8c814-120">Running the walkthrough</span></span>

<span data-ttu-id="8c814-121">To run this application, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="8c814-121">To run this application, follow these steps:</span></span>

1. <span data-ttu-id="8c814-122">Create a new Python project in your favorite IDE or editor.</span><span class="sxs-lookup"><span data-stu-id="8c814-122">Create a new Python project in your favorite IDE or editor.</span></span>
2. <span data-ttu-id="8c814-123">Create a file named visualsearch.py and add the code shown in this quickstart.</span><span class="sxs-lookup"><span data-stu-id="8c814-123">Create a file named visualsearch.py and add the code shown in this quickstart.</span></span>
3. <span data-ttu-id="8c814-124">Replace the `SUBSCRIPTION_KEY` value with your subscription key.</span><span class="sxs-lookup"><span data-stu-id="8c814-124">Replace the `SUBSCRIPTION_KEY` value with your subscription key.</span></span>
3. <span data-ttu-id="8c814-125">Replace the `imagePath` value with the path of the image to upload.</span><span class="sxs-lookup"><span data-stu-id="8c814-125">Replace the `imagePath` value with the path of the image to upload.</span></span>
4. <span data-ttu-id="8c814-126">Run the program.</span><span class="sxs-lookup"><span data-stu-id="8c814-126">Run the program.</span></span>



<span data-ttu-id="8c814-127">The following shows how to send the message using multipart form data in Python.</span><span class="sxs-lookup"><span data-stu-id="8c814-127">The following shows how to send the message using multipart form data in Python.</span></span>

```python
"""Bing Visual Search upload image example"""

# Download and install Python at https://www.python.org/
# Run the following in a command console window
# pip3 install requests

import requests, json


BASE_URI = 'https://api.cognitive.microsoft.com/bing/v7.0/images/visualsearch'

SUBSCRIPTION_KEY = '<yoursubscriptionkeygoeshere>'

HEADERS = {'Ocp-Apim-Subscription-Key': SUBSCRIPTION_KEY}

imagePath = '<pathtoyourimagetouploadgoeshere>'

file = {'image' : ('myfile', open(imagePath, 'rb'))}

def main():
    
    try:
        response = requests.post(BASE_URI, headers=HEADERS, files=file)
        response.raise_for_status()
        print_json(response.json())

    except Exception as ex:
        raise ex


def print_json(obj):
    """Print the object as json"""
    print(json.dumps(obj, sort_keys=True, indent=2, separators=(',', ': ')))



# Main execution
if __name__ == '__main__':
    main()
```


## <a name="next-steps"></a><span data-ttu-id="8c814-128">Next steps</span><span class="sxs-lookup"><span data-stu-id="8c814-128">Next steps</span></span>

[<span data-ttu-id="8c814-129">Get insights about an image using an insights token</span><span class="sxs-lookup"><span data-stu-id="8c814-129">Get insights about an image using an insights token</span></span>](../use-insights-token.md)  
<span data-ttu-id="8c814-130">[Bing Visual Search image upload tutorial](../tutorial-visual-search-image-upload.md)
[Bing Visual Search single-page app tutorial](../tutorial-bing-visual-search-single-page-app.md)</span><span class="sxs-lookup"><span data-stu-id="8c814-130">[Bing Visual Search image upload tutorial](../tutorial-visual-search-image-upload.md)
[Bing Visual Search single-page app tutorial](../tutorial-bing-visual-search-single-page-app.md)</span></span>  
[<span data-ttu-id="8c814-131">Bing Visual Search overview</span><span class="sxs-lookup"><span data-stu-id="8c814-131">Bing Visual Search overview</span></span>](../overview.md)  
[<span data-ttu-id="8c814-132">Try it</span><span class="sxs-lookup"><span data-stu-id="8c814-132">Try it</span></span>](https://aka.ms/bingvisualsearchtryforfree)  
[<span data-ttu-id="8c814-133">Get a free trial access key</span><span class="sxs-lookup"><span data-stu-id="8c814-133">Get a free trial access key</span></span>](https://azure.microsoft.com/try/cognitive-services/?api=bing-visual-search-api)  
[<span data-ttu-id="8c814-134">Bing Visual Search API reference</span><span class="sxs-lookup"><span data-stu-id="8c814-134">Bing Visual Search API reference</span></span>](https://aka.ms/bingvisualsearchreferencedoc)
