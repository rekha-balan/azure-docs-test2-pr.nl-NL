---
title: 'Quickstart: Python Publish Knowledge Base - Qna Maker'
titleSuffix: Azure Cognitive Services
description: How to publish a knowledge base in Python for QnA Maker.
services: cognitive-services
author: nitinme
manager: cgronlun
ms.service: cognitive-services
ms.technology: qna-maker
ms.topic: quickstart
ms.date: 06/18/2018
ms.author: nolachar
ms.openlocfilehash: f6c35a6444635aed88c5b1b841a129710cbd37b3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869720"
---
# <a name="publish-a-knowledge-base-in-python"></a><span data-ttu-id="d8652-103">Publish a knowledge base in Python</span><span class="sxs-lookup"><span data-stu-id="d8652-103">Publish a knowledge base in Python</span></span>

<span data-ttu-id="d8652-104">The following code publishes an existing knowledge base, using the [Publish](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da75fe) method.</span><span class="sxs-lookup"><span data-stu-id="d8652-104">The following code publishes an existing knowledge base, using the [Publish](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da75fe) method.</span></span>

1. <span data-ttu-id="d8652-105">Create a new Python project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="d8652-105">Create a new Python project in your favorite IDE.</span></span>
2. <span data-ttu-id="d8652-106">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="d8652-106">Add the code provided below.</span></span>
3. <span data-ttu-id="d8652-107">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="d8652-107">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="d8652-108">Run the program.</span><span class="sxs-lookup"><span data-stu-id="d8652-108">Run the program.</span></span>

```python
# -*- coding: utf-8 -*-

import http.client, urllib.parse, json, time

# **********************************************
# *** Update or verify the following values. ***
# **********************************************

# Replace this with a valid subscription key.
subscriptionKey = 'ENTER KEY HERE'

# Replace this with a valid knowledge base ID.
kb = 'ENTER ID HERE';

host = 'westus.api.cognitive.microsoft.com'
service = '/qnamaker/v4.0'
method = '/knowledgebases/'

def pretty_print (content):
# Note: We convert content to and from an object so we can pretty-print it.
    return json.dumps(json.loads(content), indent=4)

def publish_kb (path, content):
    print ('Calling ' + host + path + '.')
    headers = {
        'Ocp-Apim-Subscription-Key': subscriptionKey,
        'Content-Type': 'application/json',
        'Content-Length': len (content)
    }
    conn = http.client.HTTPSConnection(host)
    conn.request ("POST", path, content, headers)
    response = conn.getresponse ()

    if response.status == 204:
        return json.dumps({'result' : 'Success.'})
    else:
        return response.read ()

path = service + method + kb
result = publish_kb (path, '')
print (pretty_print(result))
```

## <a name="the-publish-a-knowledge-base-response"></a><span data-ttu-id="d8652-109">The publish a knowledge base response</span><span class="sxs-lookup"><span data-stu-id="d8652-109">The publish a knowledge base response</span></span>

<span data-ttu-id="d8652-110">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="d8652-110">A successful response is returned in JSON, as shown in the following example:</span></span>

```json
{
  "result": "Success."
}
```

## <a name="next-steps"></a><span data-ttu-id="d8652-111">Next steps</span><span class="sxs-lookup"><span data-stu-id="d8652-111">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d8652-112">QnA Maker (V4) REST API Reference</span><span class="sxs-lookup"><span data-stu-id="d8652-112">QnA Maker (V4) REST API Reference</span></span>](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da75ff)

[<span data-ttu-id="d8652-113">QnA Maker overview</span><span class="sxs-lookup"><span data-stu-id="d8652-113">QnA Maker overview</span></span>](../Overview/overview.md)