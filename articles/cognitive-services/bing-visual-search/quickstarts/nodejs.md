---
title: JavaScript Quickstart for Bing Visual Search API | Microsoft Docs
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
ms.openlocfilehash: 60b1dc9b8ea9eda258e9776b8967df38c97d964e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864942"
---
# <a name="your-first-bing-visual-search-query-in-javascript"></a><span data-ttu-id="cbf4e-103">Your first Bing Visual Search query in JavaScript</span><span class="sxs-lookup"><span data-stu-id="cbf4e-103">Your first Bing Visual Search query in JavaScript</span></span>

<span data-ttu-id="cbf4e-104">Bing Visual Search API returns information about an image that you provide.</span><span class="sxs-lookup"><span data-stu-id="cbf4e-104">Bing Visual Search API returns information about an image that you provide.</span></span> <span data-ttu-id="cbf4e-105">You can provide the image by using the URL of the image, an insights token, or by uploading an image.</span><span class="sxs-lookup"><span data-stu-id="cbf4e-105">You can provide the image by using the URL of the image, an insights token, or by uploading an image.</span></span> <span data-ttu-id="cbf4e-106">For information about these options, see [What is Bing Visual Search API?](../overview.md)</span><span class="sxs-lookup"><span data-stu-id="cbf4e-106">For information about these options, see [What is Bing Visual Search API?](../overview.md)</span></span> <span data-ttu-id="cbf4e-107">This article demonstrates uploading an image.</span><span class="sxs-lookup"><span data-stu-id="cbf4e-107">This article demonstrates uploading an image.</span></span> <span data-ttu-id="cbf4e-108">Uploading an image could be useful in mobile scenarios where you take a picture of a well-known landmark and get back information about it.</span><span class="sxs-lookup"><span data-stu-id="cbf4e-108">Uploading an image could be useful in mobile scenarios where you take a picture of a well-known landmark and get back information about it.</span></span> <span data-ttu-id="cbf4e-109">For example, the insights could include trivia about the landmark.</span><span class="sxs-lookup"><span data-stu-id="cbf4e-109">For example, the insights could include trivia about the landmark.</span></span> 

<span data-ttu-id="cbf4e-110">If you upload a local image, the following shows the form data you must include in the body of the POST.</span><span class="sxs-lookup"><span data-stu-id="cbf4e-110">If you upload a local image, the following shows the form data you must include in the body of the POST.</span></span> <span data-ttu-id="cbf4e-111">The form data must include the Content-Disposition header.</span><span class="sxs-lookup"><span data-stu-id="cbf4e-111">The form data must include the Content-Disposition header.</span></span> <span data-ttu-id="cbf4e-112">Its `name` parameter must be set to "image" and the `filename` parameter may be set to any string.</span><span class="sxs-lookup"><span data-stu-id="cbf4e-112">Its `name` parameter must be set to "image" and the `filename` parameter may be set to any string.</span></span> <span data-ttu-id="cbf4e-113">The contents of the form is the binary of the image.</span><span class="sxs-lookup"><span data-stu-id="cbf4e-113">The contents of the form is the binary of the image.</span></span> <span data-ttu-id="cbf4e-114">The maximum image size you may upload is 1 MB.</span><span class="sxs-lookup"><span data-stu-id="cbf4e-114">The maximum image size you may upload is 1 MB.</span></span> 

```
--boundary_1234-abcd
Content-Disposition: form-data; name="image"; filename="myimagefile.jpg"

ÿØÿà JFIF ÖÆ68g-¤CWŸþ29ÌÄøÖ‘º«™æ±èuZiÀ)"óÓß°Î= ØJ9á+*G¦...

--boundary_1234-abcd--
```

<span data-ttu-id="cbf4e-115">This article includes a simple console application that sends a Bing Visual Search API request and displays the JSON search results.</span><span class="sxs-lookup"><span data-stu-id="cbf4e-115">This article includes a simple console application that sends a Bing Visual Search API request and displays the JSON search results.</span></span> <span data-ttu-id="cbf4e-116">While this application is written in JavaScript, the API is a RESTful Web service compatible with any programming language that can make HTTP requests and parse JSON.</span><span class="sxs-lookup"><span data-stu-id="cbf4e-116">While this application is written in JavaScript, the API is a RESTful Web service compatible with any programming language that can make HTTP requests and parse JSON.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="cbf4e-117">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="cbf4e-117">Prerequisites</span></span>

<span data-ttu-id="cbf4e-118">You need [Node.js 6](https://nodejs.org/en/download/) to run this code.</span><span class="sxs-lookup"><span data-stu-id="cbf4e-118">You need [Node.js 6](https://nodejs.org/en/download/) to run this code.</span></span>

<span data-ttu-id="cbf4e-119">For this quickstart, you may use a [free trial](https://azure.microsoft.com/try/cognitive-services/?api=bing-web-search-api) subscription key or a paid subscription key.</span><span class="sxs-lookup"><span data-stu-id="cbf4e-119">For this quickstart, you may use a [free trial](https://azure.microsoft.com/try/cognitive-services/?api=bing-web-search-api) subscription key or a paid subscription key.</span></span>

## <a name="running-the-application"></a><span data-ttu-id="cbf4e-120">Running the application</span><span class="sxs-lookup"><span data-stu-id="cbf4e-120">Running the application</span></span>

<span data-ttu-id="cbf4e-121">The following shows how to send the message using FormData in Node.js.</span><span class="sxs-lookup"><span data-stu-id="cbf4e-121">The following shows how to send the message using FormData in Node.js.</span></span>

<span data-ttu-id="cbf4e-122">To run this application, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="cbf4e-122">To run this application, follow these steps:</span></span>

1. <span data-ttu-id="cbf4e-123">Create a folder for your project (or use your favorite IDE or editor).</span><span class="sxs-lookup"><span data-stu-id="cbf4e-123">Create a folder for your project (or use your favorite IDE or editor).</span></span>
2. <span data-ttu-id="cbf4e-124">From a command prompt or terminal, navigate to the folder you just created.</span><span class="sxs-lookup"><span data-stu-id="cbf4e-124">From a command prompt or terminal, navigate to the folder you just created.</span></span>
3. <span data-ttu-id="cbf4e-125">Install the request modules:</span><span class="sxs-lookup"><span data-stu-id="cbf4e-125">Install the request modules:</span></span>  
  ```  
  npm install request  
  ```  
3. <span data-ttu-id="cbf4e-126">Install the form-data modules:</span><span class="sxs-lookup"><span data-stu-id="cbf4e-126">Install the form-data modules:</span></span>  
  ```  
  npm install form-data  
  ```  
4. <span data-ttu-id="cbf4e-127">Create a file named GetVisualInsights.js and add the following code to it.</span><span class="sxs-lookup"><span data-stu-id="cbf4e-127">Create a file named GetVisualInsights.js and add the following code to it.</span></span>
5. <span data-ttu-id="cbf4e-128">Replace the `subscriptionKey` value with your subscription key.</span><span class="sxs-lookup"><span data-stu-id="cbf4e-128">Replace the `subscriptionKey` value with your subscription key.</span></span>
6. <span data-ttu-id="cbf4e-129">Replace the `imagePath` value with the path of the image to upload.</span><span class="sxs-lookup"><span data-stu-id="cbf4e-129">Replace the `imagePath` value with the path of the image to upload.</span></span>
7. <span data-ttu-id="cbf4e-130">Run the program.</span><span class="sxs-lookup"><span data-stu-id="cbf4e-130">Run the program.</span></span>  
  ```
  node GetVisualInsights.js
  ```

```javascript
var request = require('request');
var FormData = require('form-data');
var fs = require('fs');

var baseUri = 'https://api.cognitive.microsoft.com/bing/v7.0/images/visualsearch';
var subscriptionKey = '<yoursubscriptionkeygoeshere>';
var imagePath = "<pathtoyourimagegoeshere>";

var form = new FormData();
form.append("image", fs.createReadStream(imagePath));

form.getLength(function(err, length){
  if (err) {
    return requestCallback(err);
  }

  var r = request.post(baseUri, requestCallback);
  r._form = form; 
  r.setHeader('Ocp-Apim-Subscription-Key', subscriptionKey);
});

function requestCallback(err, res, body) {
    console.log(JSON.stringify(JSON.parse(body), null, '  '))
}
```


## <a name="next-steps"></a><span data-ttu-id="cbf4e-131">Next steps</span><span class="sxs-lookup"><span data-stu-id="cbf4e-131">Next steps</span></span>

[<span data-ttu-id="cbf4e-132">Get insights about an image using an insights token</span><span class="sxs-lookup"><span data-stu-id="cbf4e-132">Get insights about an image using an insights token</span></span>](../use-insights-token.md)  
<span data-ttu-id="cbf4e-133">[Bing Visual Search image upload tutorial](../tutorial-visual-search-image-upload.md)
[Bing Visual Search single-page app tutorial](../tutorial-bing-visual-search-single-page-app.md)</span><span class="sxs-lookup"><span data-stu-id="cbf4e-133">[Bing Visual Search image upload tutorial](../tutorial-visual-search-image-upload.md)
[Bing Visual Search single-page app tutorial](../tutorial-bing-visual-search-single-page-app.md)</span></span>  
[<span data-ttu-id="cbf4e-134">Bing Visual Search overview</span><span class="sxs-lookup"><span data-stu-id="cbf4e-134">Bing Visual Search overview</span></span>](../overview.md)  
[<span data-ttu-id="cbf4e-135">Try it</span><span class="sxs-lookup"><span data-stu-id="cbf4e-135">Try it</span></span>](https://aka.ms/bingvisualsearchtryforfree)  
[<span data-ttu-id="cbf4e-136">Get a free trial access key</span><span class="sxs-lookup"><span data-stu-id="cbf4e-136">Get a free trial access key</span></span>](https://azure.microsoft.com/try/cognitive-services/?api=bing-visual-search-api)  
[<span data-ttu-id="cbf4e-137">Bing Visual Search API reference</span><span class="sxs-lookup"><span data-stu-id="cbf4e-137">Bing Visual Search API reference</span></span>](https://aka.ms/bingvisualsearchreferencedoc)
