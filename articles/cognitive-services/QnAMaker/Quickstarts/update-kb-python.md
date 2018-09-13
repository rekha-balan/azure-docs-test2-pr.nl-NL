---
title: Update Knowledge Base, Python Quickstart - Azure Cognitive Services | Microsoft Docs
description: How to update a knowledge base in Python for QnA Maker.
services: cognitive-services
author: noellelacharite
manager: nolachar
ms.service: cognitive-services
ms.technology: qna-maker
ms.topic: quickstart
ms.date: 06/18/2018
ms.author: nolachar
ms.openlocfilehash: 79b2af150558aa5da8e060e1b5117b91ffd34387
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855961"
---
# <a name="update-a-knowledge-base-in-python"></a><span data-ttu-id="69889-103">Update a knowledge base in Python</span><span class="sxs-lookup"><span data-stu-id="69889-103">Update a knowledge base in Python</span></span>

<span data-ttu-id="69889-104">The following code updates an existing knowledge base, using the [Update](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da7600) method.</span><span class="sxs-lookup"><span data-stu-id="69889-104">The following code updates an existing knowledge base, using the [Update](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da7600) method.</span></span>

<span data-ttu-id="69889-105">If you don't have a knowledge base yet, you can create a sample one to use for this quickstart: [Create a new knowledge base](create-new-kb-python.md).</span><span class="sxs-lookup"><span data-stu-id="69889-105">If you don't have a knowledge base yet, you can create a sample one to use for this quickstart: [Create a new knowledge base](create-new-kb-python.md).</span></span>

1. <span data-ttu-id="69889-106">Create a new Python project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="69889-106">Create a new Python project in your favorite IDE.</span></span>
1. <span data-ttu-id="69889-107">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="69889-107">Add the code provided below.</span></span>
1. <span data-ttu-id="69889-108">Replace the `subscriptionKey` value with a valid subscription key.</span><span class="sxs-lookup"><span data-stu-id="69889-108">Replace the `subscriptionKey` value with a valid subscription key.</span></span>
1. <span data-ttu-id="69889-109">Replace the `kb` value with a valid knowledge base ID.</span><span class="sxs-lookup"><span data-stu-id="69889-109">Replace the `kb` value with a valid knowledge base ID.</span></span> <span data-ttu-id="69889-110">Find this value by going to one of your [QnA Maker knowledge bases](https://www.qnamaker.ai/Home/MyServices).</span><span class="sxs-lookup"><span data-stu-id="69889-110">Find this value by going to one of your [QnA Maker knowledge bases](https://www.qnamaker.ai/Home/MyServices).</span></span> <span data-ttu-id="69889-111">Select the knowledge base you want to update.</span><span class="sxs-lookup"><span data-stu-id="69889-111">Select the knowledge base you want to update.</span></span> <span data-ttu-id="69889-112">Once on that page, find the 'kdid=' in the URL as shown below.</span><span class="sxs-lookup"><span data-stu-id="69889-112">Once on that page, find the 'kdid=' in the URL as shown below.</span></span> <span data-ttu-id="69889-113">Use its value for your code sample.</span><span class="sxs-lookup"><span data-stu-id="69889-113">Use its value for your code sample.</span></span>

    ![QnA Maker knowledge base ID](../media/qnamaker-quickstart-kb/qna-maker-id.png)

1. <span data-ttu-id="69889-115">Run the program.</span><span class="sxs-lookup"><span data-stu-id="69889-115">Run the program.</span></span>

```python
# -*- coding: utf-8 -*-

import http.client, urllib.parse, json, time

# **********************************************
# *** Update or verify the following values. ***
# **********************************************

# Replace this with a valid subscription key.
subscriptionKey = 'ADD KEY HERE'

# Replace this with a valid knowledge base ID.
kb = 'ADD ID HERE';

# Represents the various elements used to create HTTP request path
# for QnA Maker operations.
host = 'westus.api.cognitive.microsoft.com'
service = '/qnamaker/v4.0'
method = '/knowledgebases/'

'''
Formats and indents JSON for display.
:param content: The JSON to format and indent.
:type: string
:return: Formatted and indented JSON.
:rtype: string
'''
def pretty_print(content):
    # Note: We convert content to and from an object so we can pretty-print it.
    return json.dumps(json.loads(content), indent=4)

'''
Sends a PATCH HTTP request.
:param path: The URL path of your request.
:param content: The contents of your PATCH request.
:type: string
:return: URL with status of PATCH request in updating the kb, actual response.
:rtype: string, string
'''
def update_kb(path, content):
    print('Calling ' + host + path + '.')
    headers = {
        'Ocp-Apim-Subscription-Key': subscriptionKey,
        'Content-Type': 'application/json',
        'Content-Length': len (content)
    }
    conn = http.client.HTTPSConnection(host)
    conn.request ("PATCH", path, content, headers)
    response = conn.getresponse ()
    return response.getheader('Location'), response.read ()

'''
Gets the status of the specified QnA Maker operation.
:param path: The URL of the request.
:type: string
:return: Header from retrying of the request (if retry is needed), response of the retry.
:rtype: string, string
'''
def check_status (path):
    print('Calling ' + host + path + '.')
    headers = {'Ocp-Apim-Subscription-Key': subscriptionKey}
    conn = http.client.HTTPSConnection(host)
    conn.request("GET", path, None, headers)
    response = conn.getresponse ()
    # If the operation is not finished, /operations returns an HTTP header named
    # 'Retry-After' with the number of seconds to wait before querying the operation again.
    return response.getheader('Retry-After'), response.read ()

'''
Dictionary that holds the knowledge base.
Modifications to the knowledge base are made here, using 'update', 'delete' and so on.
'''
req = {
    'add': {
        'qnaList': [
            {
              'id': 1,
              'answer': 'You can change the default message if you use the QnAMakerDialog. '
                      + 'See this for details:  https://docs.botframework.com/en-us'
                      + '/azure-bot-service/templates/qnamaker/#navtitle',
              'source': 'Custom Editorial',
              'questions': [
                  'How can I change the default message from QnA Maker?'
              ],
              'metadata': []
            }
        ],
        'urls': []
    },
    'update' : {
        'name' : 'New KB Name'
    },
    'delete': {
        'ids': [
            0
        ]
    }
}

# Builds the path URL.
path = service + method + kb
# Convert the request to a string.
content = json.dumps(req)
# Retrieve the operation ID to check status, and JSON result.
operation, result = update_kb(path, content)
# Print request response in JSON with presentable formatting.
print(pretty_print(result))

'''
Iteratively gets the operation state, updating the knowledge base.
Once state is no longer "Running" or "NotStarted", the loop ends.
'''
done = False
while False == done:
    path = service + operation
    # Gets the status of the operation.
    wait, status = check_status(path)
    # Print status checks in JSON with presentable formatting
    print(pretty_print(status))

    # Convert the JSON response into an object and get the value of the operationState field.
    state = json.loads(status)['operationState']
    # If the operation isn't finished, wait and query again.
    if state == 'Running' or state == 'NotStarted':
        print('Waiting ' + wait + ' seconds...')
        time.sleep (int(wait))
    else:
        done = True # request has been processed, if successful, knowledge base is updated
```

## <a name="understand-what-qna-maker-returns"></a><span data-ttu-id="69889-116">Understand what QnA Maker returns</span><span class="sxs-lookup"><span data-stu-id="69889-116">Understand what QnA Maker returns</span></span>

<span data-ttu-id="69889-117">A successful response is returned in JSON, as shown in the following example.</span><span class="sxs-lookup"><span data-stu-id="69889-117">A successful response is returned in JSON, as shown in the following example.</span></span> <span data-ttu-id="69889-118">Your results may differ slightly.</span><span class="sxs-lookup"><span data-stu-id="69889-118">Your results may differ slightly.</span></span> <span data-ttu-id="69889-119">If the final call returns a "Succeeded" state... your knowledge base was updated successfully.</span><span class="sxs-lookup"><span data-stu-id="69889-119">If the final call returns a "Succeeded" state... your knowledge base was updated successfully.</span></span> <span data-ttu-id="69889-120">To troubleshoot, refer to the [Update Knowledgebase](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da7600) response codes of the QnA Maker API.</span><span class="sxs-lookup"><span data-stu-id="69889-120">To troubleshoot, refer to the [Update Knowledgebase](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da7600) response codes of the QnA Maker API.</span></span>

```json
{
  "operationState": "NotStarted",
  "createdTimestamp": "2018-04-13T01:49:48Z",
  "lastActionTimestamp": "2018-04-13T01:49:48Z",
  "userId": "2280ef5917rt4ebfa1aae41fb1cebb4a",
  "operationId": "5156f64e-e31d-4638-ad7c-a2bdd7f41658"
}
...
{
  "operationState": "Succeeded",
  "createdTimestamp": "2018-04-13T01:49:48Z",
  "lastActionTimestamp": "2018-04-13T01:49:50Z",
  "resourceLocation": "/knowledgebases/140a46f3-b248-4f1b-9349-614bfd6e5563",
  "userId": "2280ef5917rt4ebfa1aae41fb1cebb4a",
  "operationId": "5156f64e-e31d-4638-ad7c-a2bdd7f41658"
}
Press any key to continue.
```

<span data-ttu-id="69889-121">Once your knowledge base is updated, you can view it on your QnA Maker Portal, [My knowledge bases](https://www.qnamaker.ai/Home/MyServices) page.</span><span class="sxs-lookup"><span data-stu-id="69889-121">Once your knowledge base is updated, you can view it on your QnA Maker Portal, [My knowledge bases](https://www.qnamaker.ai/Home/MyServices) page.</span></span> <span data-ttu-id="69889-122">Notice that a new QnA pair has been added and the name of your database is now 'New KB Name'.</span><span class="sxs-lookup"><span data-stu-id="69889-122">Notice that a new QnA pair has been added and the name of your database is now 'New KB Name'.</span></span>

<span data-ttu-id="69889-123">To modify other elements of your knowledge base, refer to the QnA Maker [JSON schema](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da7600) and modify the `req` string.</span><span class="sxs-lookup"><span data-stu-id="69889-123">To modify other elements of your knowledge base, refer to the QnA Maker [JSON schema](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da7600) and modify the `req` string.</span></span>

## <a name="next-steps"></a><span data-ttu-id="69889-124">Next steps</span><span class="sxs-lookup"><span data-stu-id="69889-124">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="69889-125">QnA Maker (V4) REST API Reference</span><span class="sxs-lookup"><span data-stu-id="69889-125">QnA Maker (V4) REST API Reference</span></span>](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da75ff)