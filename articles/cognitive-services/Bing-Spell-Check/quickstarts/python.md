---
title: Python Quickstart for Bing Spell Check API - Azure Cognitive Services | Microsoft Docs
description: Get information and code samples to help you quickly get started using the Bing Spell Check API in Microsoft Cognitive Services on Azure.
services: cognitive-services
documentationcenter: ''
author: v-jaswel
ms.service: cognitive-services
ms.component: bing-spell-check
ms.topic: quickstart
ms.date: 09/14/2017
ms.author: v-jaswel
ms.openlocfilehash: b7b2414a496a87cdd349a6faedf50f0771df4268
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868950"
---
# <a name="quickstart-for-bing-spell-check-api-with-python"></a><span data-ttu-id="35ed4-103">Quickstart for Bing Spell Check API with Python</span><span class="sxs-lookup"><span data-stu-id="35ed4-103">Quickstart for Bing Spell Check API with Python</span></span> 
<a name="HOLTop"></a>

<span data-ttu-id="35ed4-104">This article shows you how to use the [Bing Spell Check API](https://azure.microsoft.com/services/cognitive-services/spell-check/) with Python.</span><span class="sxs-lookup"><span data-stu-id="35ed4-104">This article shows you how to use the [Bing Spell Check API](https://azure.microsoft.com/services/cognitive-services/spell-check/) with Python.</span></span> <span data-ttu-id="35ed4-105">The Spell Check API returns a list of words it does not recognize along with suggested replacements.</span><span class="sxs-lookup"><span data-stu-id="35ed4-105">The Spell Check API returns a list of words it does not recognize along with suggested replacements.</span></span> <span data-ttu-id="35ed4-106">Typically, you would submit text to this API and then either make the suggested replacements in the text or show them to the user of your application so they can decide whether to make the replacements.</span><span class="sxs-lookup"><span data-stu-id="35ed4-106">Typically, you would submit text to this API and then either make the suggested replacements in the text or show them to the user of your application so they can decide whether to make the replacements.</span></span> <span data-ttu-id="35ed4-107">This article shows how to send a request that contains the text "Hollo, wrld!"</span><span class="sxs-lookup"><span data-stu-id="35ed4-107">This article shows how to send a request that contains the text "Hollo, wrld!"</span></span> <span data-ttu-id="35ed4-108">The suggested replacements are "Hello" and "world."</span><span class="sxs-lookup"><span data-stu-id="35ed4-108">The suggested replacements are "Hello" and "world."</span></span>

## <a name="prerequisites"></a><span data-ttu-id="35ed4-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="35ed4-109">Prerequisites</span></span>

<span data-ttu-id="35ed4-110">You will need [Python 3.x](https://www.python.org/downloads/) to run this code.</span><span class="sxs-lookup"><span data-stu-id="35ed4-110">You will need [Python 3.x](https://www.python.org/downloads/) to run this code.</span></span>

<span data-ttu-id="35ed4-111">You must have a [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) with **Bing Spell Check API v7**.</span><span class="sxs-lookup"><span data-stu-id="35ed4-111">You must have a [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) with **Bing Spell Check API v7**.</span></span> <span data-ttu-id="35ed4-112">The [free trial](https://azure.microsoft.com/try/cognitive-services/#lang) is sufficient for this quickstart.</span><span class="sxs-lookup"><span data-stu-id="35ed4-112">The [free trial](https://azure.microsoft.com/try/cognitive-services/#lang) is sufficient for this quickstart.</span></span> <span data-ttu-id="35ed4-113">You need the access key provided when you activate your free trial, or you may use a paid subscription key from your Azure dashboard.</span><span class="sxs-lookup"><span data-stu-id="35ed4-113">You need the access key provided when you activate your free trial, or you may use a paid subscription key from your Azure dashboard.</span></span>

## <a name="get-spell-check-results"></a><span data-ttu-id="35ed4-114">Get Spell Check results</span><span class="sxs-lookup"><span data-stu-id="35ed4-114">Get Spell Check results</span></span>

1. <span data-ttu-id="35ed4-115">Create a new Python project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="35ed4-115">Create a new Python project in your favorite IDE.</span></span>
2. <span data-ttu-id="35ed4-116">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="35ed4-116">Add the code provided below.</span></span>
3. <span data-ttu-id="35ed4-117">Replace the `subscriptionKey` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="35ed4-117">Replace the `subscriptionKey` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="35ed4-118">Run the program.</span><span class="sxs-lookup"><span data-stu-id="35ed4-118">Run the program.</span></span>

```python
import http.client, urllib.parse, json

text = 'Hollo, wrld!'

data = {'text': text}

# NOTE: Replace this example key with a valid subscription key.
key = 'ENTER KEY HERE'

host = 'api.cognitive.microsoft.com'
path = '/bing/v7.0/spellcheck?'
params = 'mkt=en-us&mode=proof'

headers = {'Ocp-Apim-Subscription-Key': key,
'Content-Type': 'application/x-www-form-urlencoded'}

# The headers in the following example 
# are optional but should be considered as required:
#
# X-MSEdge-ClientIP: 999.999.999.999  
# X-Search-Location: lat: +90.0000000000000;long: 00.0000000000000;re:100.000000000000
# X-MSEdge-ClientID: <Client ID from Previous Response Goes Here>

conn = http.client.HTTPSConnection(host)
body = urllib.parse.urlencode (data)
conn.request ("POST", path + params, body, headers)
response = conn.getresponse ()
output = json.dumps(json.loads(response.read()), indent=4)
print (output)
```

<span data-ttu-id="35ed4-119">**Response**</span><span class="sxs-lookup"><span data-stu-id="35ed4-119">**Response**</span></span>

<span data-ttu-id="35ed4-120">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="35ed4-120">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json
{
   "_type": "SpellCheck",
   "flaggedTokens": [
      {
         "offset": 0,
         "token": "Hollo",
         "type": "UnknownToken",
         "suggestions": [
            {
               "suggestion": "Hello",
               "score": 0.9115257530801
            },
            {
               "suggestion": "Hollow",
               "score": 0.858039839213461
            },
            {
               "suggestion": "Hallo",
               "score": 0.597385084464481
            }
         ]
      },
      {
         "offset": 7,
         "token": "wrld",
         "type": "UnknownToken",
         "suggestions": [
            {
               "suggestion": "world",
               "score": 0.9115257530801
            }
         ]
      }
   ]
}
```

## <a name="next-steps"></a><span data-ttu-id="35ed4-121">Next steps</span><span class="sxs-lookup"><span data-stu-id="35ed4-121">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="35ed4-122">Bing Spell Check tutorial</span><span class="sxs-lookup"><span data-stu-id="35ed4-122">Bing Spell Check tutorial</span></span>](../tutorials/spellcheck.md)

## <a name="see-also"></a><span data-ttu-id="35ed4-123">See also</span><span class="sxs-lookup"><span data-stu-id="35ed4-123">See also</span></span>

- [<span data-ttu-id="35ed4-124">Bing Spell Check overview</span><span class="sxs-lookup"><span data-stu-id="35ed4-124">Bing Spell Check overview</span></span>](../proof-text.md)
- [<span data-ttu-id="35ed4-125">Bing Spell Check API v7 Reference</span><span class="sxs-lookup"><span data-stu-id="35ed4-125">Bing Spell Check API v7 Reference</span></span>](https://docs.microsoft.com/rest/api/cognitiveservices/bing-spell-check-api-v7-reference)
