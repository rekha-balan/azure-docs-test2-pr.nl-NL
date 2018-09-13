---
title: Python Quickstart for Microsoft QnA Maker API (V4) - Azure Cognitive Services | Microsoft Docs
description: Get information and code samples to help you quickly get started using the Microsoft Translator Text API in Microsoft Cognitive Services on Azure.
services: cognitive-services
documentationcenter: ''
author: v-jaswel
ms.service: cognitive-services
ms.technology: qna-maker
ms.topic: article
ms.date: 05/07/2018
ms.author: v-jaswel
ms.openlocfilehash: c0d02a0f586857f6dd303fc98407da71b2addb9b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857698"
---
# <a name="quickstart-for-microsoft-qna-maker-api-with-python"></a><span data-ttu-id="a1660-103">Quickstart for Microsoft QnA Maker API with Python</span><span class="sxs-lookup"><span data-stu-id="a1660-103">Quickstart for Microsoft QnA Maker API with Python</span></span> 
<a name="HOLTop"></a>

<span data-ttu-id="a1660-104">This article shows you how to use the [Microsoft QnA Maker API](../Overview/overview.md) with Python to do the following.</span><span class="sxs-lookup"><span data-stu-id="a1660-104">This article shows you how to use the [Microsoft QnA Maker API](../Overview/overview.md) with Python to do the following.</span></span>

- [<span data-ttu-id="a1660-105">Create a new knowledge base.</span><span class="sxs-lookup"><span data-stu-id="a1660-105">Create a new knowledge base.</span></span>](#Create)
- [<span data-ttu-id="a1660-106">Update an existing knowledge base.</span><span class="sxs-lookup"><span data-stu-id="a1660-106">Update an existing knowledge base.</span></span>](#Update)
- [<span data-ttu-id="a1660-107">Get the status of a request to create or update a knowledge base.</span><span class="sxs-lookup"><span data-stu-id="a1660-107">Get the status of a request to create or update a knowledge base.</span></span>](#Status)
- [<span data-ttu-id="a1660-108">Publish an existing knowledge base.</span><span class="sxs-lookup"><span data-stu-id="a1660-108">Publish an existing knowledge base.</span></span>](#Publish)
- [<span data-ttu-id="a1660-109">Replace the contents of an existing knowledge base.</span><span class="sxs-lookup"><span data-stu-id="a1660-109">Replace the contents of an existing knowledge base.</span></span>](#Replace)
- [<span data-ttu-id="a1660-110">Download the contents of a knowledge base.</span><span class="sxs-lookup"><span data-stu-id="a1660-110">Download the contents of a knowledge base.</span></span>](#GetQnA)
- [<span data-ttu-id="a1660-111">Get answers to a question using a knowledge base.</span><span class="sxs-lookup"><span data-stu-id="a1660-111">Get answers to a question using a knowledge base.</span></span>](#GetAnswers)
- [<span data-ttu-id="a1660-112">Get information about a knowledge base.</span><span class="sxs-lookup"><span data-stu-id="a1660-112">Get information about a knowledge base.</span></span>](#GetKB)
- [<span data-ttu-id="a1660-113">Get information about all knowledge bases belonging to the specified user.</span><span class="sxs-lookup"><span data-stu-id="a1660-113">Get information about all knowledge bases belonging to the specified user.</span></span>](#GetKBsByUser)
- [<span data-ttu-id="a1660-114">Delete a knowledge base.</span><span class="sxs-lookup"><span data-stu-id="a1660-114">Delete a knowledge base.</span></span>](#Delete)
- [<span data-ttu-id="a1660-115">Get the current endpoint keys.</span><span class="sxs-lookup"><span data-stu-id="a1660-115">Get the current endpoint keys.</span></span>](#GetKeys)
- [<span data-ttu-id="a1660-116">Re-generate the current endpoint keys.</span><span class="sxs-lookup"><span data-stu-id="a1660-116">Re-generate the current endpoint keys.</span></span>](#PutKeys)
- [<span data-ttu-id="a1660-117">Get the current set of word alterations.</span><span class="sxs-lookup"><span data-stu-id="a1660-117">Get the current set of word alterations.</span></span>](#GetAlterations)
- [<span data-ttu-id="a1660-118">Replace the current set of word alterations.</span><span class="sxs-lookup"><span data-stu-id="a1660-118">Replace the current set of word alterations.</span></span>](#PutAlterations)

## <a name="prerequisites"></a><span data-ttu-id="a1660-119">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a1660-119">Prerequisites</span></span>

<span data-ttu-id="a1660-120">You will need [Python 3.x](https://www.python.org/downloads/) to run this code.</span><span class="sxs-lookup"><span data-stu-id="a1660-120">You will need [Python 3.x](https://www.python.org/downloads/) to run this code.</span></span>

<span data-ttu-id="a1660-121">You must have a [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) with **Microsoft QnA Maker API**.</span><span class="sxs-lookup"><span data-stu-id="a1660-121">You must have a [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) with **Microsoft QnA Maker API**.</span></span> <span data-ttu-id="a1660-122">You will need a paid subscription key from your [Azure dashboard](https://portal.azure.com/#create/Microsoft.CognitiveServices).</span><span class="sxs-lookup"><span data-stu-id="a1660-122">You will need a paid subscription key from your [Azure dashboard](https://portal.azure.com/#create/Microsoft.CognitiveServices).</span></span>

<a name="Create"></a>

## <a name="create-knowledge-base"></a><span data-ttu-id="a1660-123">Create knowledge base</span><span class="sxs-lookup"><span data-stu-id="a1660-123">Create knowledge base</span></span>

<span data-ttu-id="a1660-124">The following code creates a new knowledge base, using the [Create](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da75ff) method.</span><span class="sxs-lookup"><span data-stu-id="a1660-124">The following code creates a new knowledge base, using the [Create](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da75ff) method.</span></span>

1. <span data-ttu-id="a1660-125">Create a new Python project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="a1660-125">Create a new Python project in your favorite IDE.</span></span>
2. <span data-ttu-id="a1660-126">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="a1660-126">Add the code provided below.</span></span>
3. <span data-ttu-id="a1660-127">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="a1660-127">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="a1660-128">Run the program.</span><span class="sxs-lookup"><span data-stu-id="a1660-128">Run the program.</span></span>

```python
# -*- coding: utf-8 -*-

import http.client, urllib.parse, json, time

# **********************************************
# *** Update or verify the following values. ***
# **********************************************

# Replace this with a valid subscription key.
subscriptionKey = 'ENTER KEY HERE'

host = 'westus.api.cognitive.microsoft.com'
service = '/qnamaker/v4.0'
method = '/knowledgebases/create'

def pretty_print (content):
# Note: We convert content to and from an object so we can pretty-print it.
    return json.dumps(json.loads(content), indent=4)

def create_kb (path, content):
    print ('Calling ' + host + path + '.')
    headers = {
        'Ocp-Apim-Subscription-Key': subscriptionKey,
        'Content-Type': 'application/json',
        'Content-Length': len (content)
    }
    conn = http.client.HTTPSConnection(host)
    conn.request ("POST", path, content, headers)
    response = conn.getresponse ()
# /knowledgebases/create returns an HTTP header named Location that contains a URL
# to check the status of the operation to create the knowledgebase.
    return response.getheader('Location'), response.read ()

def check_status (path):
    print ('Calling ' + host + path + '.')
    headers = {'Ocp-Apim-Subscription-Key': subscriptionKey}
    conn = http.client.HTTPSConnection(host)
    conn.request ("GET", path, None, headers)
    response = conn.getresponse ()
# If the operation is not finished, /operations returns an HTTP header named Retry-After
# that contains the number of seconds to wait before we query the operation again.
    return response.getheader('Retry-After'), response.read ()

req = {
  "name": "QnA Maker FAQ",
  "qnaList": [
    {
      "id": 0,
      "answer": "You can use our REST APIs to manage your Knowledge Base. See here for details: https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da7600",
      "source": "Custom Editorial",
      "questions": [
        "How do I programmatically update my Knowledge Base?"
      ],
      "metadata": [
        {
          "name": "category",
          "value": "api"
        }
      ]
    }
  ],
  "urls": [
    "https://docs.microsoft.com/en-in/azure/cognitive-services/qnamaker/faqs",
    "https://docs.microsoft.com/en-us/bot-framework/resources-bot-framework-faq"
  ],
  "files": []
}

path = service + method
# Convert the request to a string.
content = json.dumps(req)
operation, result = create_kb (path, content)
print (pretty_print(result))

done = False
while False == done:
    path = service + operation
    wait, status = check_status (path)
    print (pretty_print(status))

# Convert the JSON response into an object and get the value of the operationState field.
    state = json.loads(status)['operationState']
# If the operation isn't finished, wait and query again.
    if state == 'Running' or state == 'NotStarted':
        print ('Waiting ' + wait + ' seconds...')
        time.sleep (int(wait))
    else:
        done = True
```

<span data-ttu-id="a1660-129">**Create knowledge base response**</span><span class="sxs-lookup"><span data-stu-id="a1660-129">**Create knowledge base response**</span></span>

<span data-ttu-id="a1660-130">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="a1660-130">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json
{
  "operationState": "NotStarted",
  "createdTimestamp": "2018-04-13T01:52:30Z",
  "lastActionTimestamp": "2018-04-13T01:52:30Z",
  "userId": "2280ef5917bb4ebfa1aae41fb1cebb4a",
  "operationId": "e88b5b23-e9ab-47fe-87dd-3affc2fb10f3"
}
...
{
  "operationState": "Running",
  "createdTimestamp": "2018-04-13T01:52:30Z",
  "lastActionTimestamp": "2018-04-13T01:52:30Z",
  "userId": "2280ef5917bb4ebfa1aae41fb1cebb4a",
  "operationId": "e88b5b23-e9ab-47fe-87dd-3affc2fb10f3"
}
...
{
  "operationState": "Succeeded",
  "createdTimestamp": "2018-04-13T01:52:30Z",
  "lastActionTimestamp": "2018-04-13T01:52:46Z",
  "resourceLocation": "/knowledgebases/b0288f33-27b9-4258-a304-8b9f63427dad",
  "userId": "2280ef5917bb4ebfa1aae41fb1cebb4a",
  "operationId": "e88b5b23-e9ab-47fe-87dd-3affc2fb10f3"
}
```

[<span data-ttu-id="a1660-131">Back to top</span><span class="sxs-lookup"><span data-stu-id="a1660-131">Back to top</span></span>](#HOLTop)

<a name="Update"></a>

## <a name="update-knowledge-base"></a><span data-ttu-id="a1660-132">Update knowledge base</span><span class="sxs-lookup"><span data-stu-id="a1660-132">Update knowledge base</span></span>

<span data-ttu-id="a1660-133">The following code updates an existing knowledge base, using the [Update](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da7600) method.</span><span class="sxs-lookup"><span data-stu-id="a1660-133">The following code updates an existing knowledge base, using the [Update](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da7600) method.</span></span>

1. <span data-ttu-id="a1660-134">Create a new Python project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="a1660-134">Create a new Python project in your favorite IDE.</span></span>
2. <span data-ttu-id="a1660-135">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="a1660-135">Add the code provided below.</span></span>
3. <span data-ttu-id="a1660-136">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="a1660-136">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="a1660-137">Run the program.</span><span class="sxs-lookup"><span data-stu-id="a1660-137">Run the program.</span></span>

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

def update_kb (path, content):
    print ('Calling ' + host + path + '.')
    headers = {
        'Ocp-Apim-Subscription-Key': subscriptionKey,
        'Content-Type': 'application/json',
        'Content-Length': len (content)
    }
    conn = http.client.HTTPSConnection(host)
    conn.request ("PATCH", path, content, headers)
    response = conn.getresponse ()
# PATCH /knowledgebases returns an HTTP header named Location that contains a URL
# to check the status of the operation to create the knowledgebase.
    return response.getheader('Location'), response.read ()

def check_status (path):
    print ('Calling ' + host + path + '.')
    headers = {'Ocp-Apim-Subscription-Key': subscriptionKey}
    conn = http.client.HTTPSConnection(host)
    conn.request ("GET", path, None, headers)
    response = conn.getresponse ()
# If the operation is not finished, /operations returns an HTTP header named Retry-After
# that contains the number of seconds to wait before we query the operation again.
    return response.getheader('Retry-After'), response.read ()

req = {
  'add': {
    'qnaList': [
      {
        'id': 1,
        'answer': 'You can change the default message if you use the QnAMakerDialog. See this for details: https://docs.botframework.com/en-us/azure-bot-service/templates/qnamaker/#navtitle',
        'source': 'Custom Editorial',
        'questions': [
          'How can I change the default message from QnA Maker?'
        ],
        'metadata': []
      }
    ],
    'urls': [
      'https://docs.microsoft.com/en-us/azure/cognitive-services/Emotion/FAQ'
    ]
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

path = service + method + kb
# Convert the request to a string.
content = json.dumps(req)
operation, result = update_kb (path, content)
print (pretty_print(result))

done = False
while False == done:
    path = service + operation
    wait, status = check_status (path)
    print (pretty_print(status))

# Convert the JSON response into an object and get the value of the operationState field.
    state = json.loads(status)['operationState']
# If the operation isn't finished, wait and query again.
    if state == 'Running' or state == 'NotStarted':
        print ('Waiting ' + wait + ' seconds...')
        time.sleep (int(wait))
    else:
        done = True
```

<span data-ttu-id="a1660-138">**Update knowledge base response**</span><span class="sxs-lookup"><span data-stu-id="a1660-138">**Update knowledge base response**</span></span>

<span data-ttu-id="a1660-139">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="a1660-139">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json
{
  "operationState": "NotStarted",
  "createdTimestamp": "2018-04-13T01:49:48Z",
  "lastActionTimestamp": "2018-04-13T01:49:48Z",
  "userId": "2280ef5917bb4ebfa1aae41fb1cebb4a",
  "operationId": "5156f64e-e31d-4638-ad7c-a2bdd7f41658"
}
...
{
  "operationState": "Succeeded",
  "createdTimestamp": "2018-04-13T01:49:48Z",
  "lastActionTimestamp": "2018-04-13T01:49:50Z",
  "resourceLocation": "/knowledgebases/140a46f3-b248-4f1b-9349-614bfd6e5563",
  "userId": "2280ef5917bb4ebfa1aae41fb1cebb4a",
  "operationId": "5156f64e-e31d-4638-ad7c-a2bdd7f41658"
}
Press any key to continue.
```

[<span data-ttu-id="a1660-140">Back to top</span><span class="sxs-lookup"><span data-stu-id="a1660-140">Back to top</span></span>](#HOLTop)

<a name="Status"></a>

## <a name="get-request-status"></a><span data-ttu-id="a1660-141">Get request status</span><span class="sxs-lookup"><span data-stu-id="a1660-141">Get request status</span></span>

<span data-ttu-id="a1660-142">You can call the [Operation](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/operations_getoperationdetails) method to check the status of a request to create or update a knowledge base.</span><span class="sxs-lookup"><span data-stu-id="a1660-142">You can call the [Operation](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/operations_getoperationdetails) method to check the status of a request to create or update a knowledge base.</span></span> <span data-ttu-id="a1660-143">To see how this method is used, please see the sample code for the [Create](#Create) or [Update](#Update) method.</span><span class="sxs-lookup"><span data-stu-id="a1660-143">To see how this method is used, please see the sample code for the [Create](#Create) or [Update](#Update) method.</span></span>

[<span data-ttu-id="a1660-144">Back to top</span><span class="sxs-lookup"><span data-stu-id="a1660-144">Back to top</span></span>](#HOLTop)

<a name="Publish"></a>

## <a name="publish-knowledge-base"></a><span data-ttu-id="a1660-145">Publish knowledge base</span><span class="sxs-lookup"><span data-stu-id="a1660-145">Publish knowledge base</span></span>

<span data-ttu-id="a1660-146">The following code publishes an existing knowledge base, using the [Publish](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da75fe) method.</span><span class="sxs-lookup"><span data-stu-id="a1660-146">The following code publishes an existing knowledge base, using the [Publish](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da75fe) method.</span></span>

1. <span data-ttu-id="a1660-147">Create a new Python project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="a1660-147">Create a new Python project in your favorite IDE.</span></span>
2. <span data-ttu-id="a1660-148">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="a1660-148">Add the code provided below.</span></span>
3. <span data-ttu-id="a1660-149">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="a1660-149">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="a1660-150">Run the program.</span><span class="sxs-lookup"><span data-stu-id="a1660-150">Run the program.</span></span>

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

<span data-ttu-id="a1660-151">**Publish knowledge base response**</span><span class="sxs-lookup"><span data-stu-id="a1660-151">**Publish knowledge base response**</span></span>

<span data-ttu-id="a1660-152">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="a1660-152">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json
{
  "result": "Success."
}
```

[<span data-ttu-id="a1660-153">Back to top</span><span class="sxs-lookup"><span data-stu-id="a1660-153">Back to top</span></span>](#HOLTop)

<a name="Replace"></a>

## <a name="replace-knowledge-base"></a><span data-ttu-id="a1660-154">Replace knowledge base</span><span class="sxs-lookup"><span data-stu-id="a1660-154">Replace knowledge base</span></span>

<span data-ttu-id="a1660-155">The following code replaces the contents of the specified knowledge base, using the [Replace](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/knowledgebases_publish) method.</span><span class="sxs-lookup"><span data-stu-id="a1660-155">The following code replaces the contents of the specified knowledge base, using the [Replace](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/knowledgebases_publish) method.</span></span>

1. <span data-ttu-id="a1660-156">Create a new Python project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="a1660-156">Create a new Python project in your favorite IDE.</span></span>
2. <span data-ttu-id="a1660-157">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="a1660-157">Add the code provided below.</span></span>
3. <span data-ttu-id="a1660-158">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="a1660-158">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="a1660-159">Run the program.</span><span class="sxs-lookup"><span data-stu-id="a1660-159">Run the program.</span></span>

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

def replace_kb (path, content):
    print ('Calling ' + host + path + '.')
    headers = {
        'Ocp-Apim-Subscription-Key': subscriptionKey,
        'Content-Type': 'application/json',
        'Content-Length': len (content)
    }
    conn = http.client.HTTPSConnection(host)
    conn.request ("PUT", path, content, headers)
    response = conn.getresponse ()

    if response.status == 204:
        return json.dumps({'result' : 'Success.'})
    else:
        return response.read ()

req = {
  'qnaList': [
    {
      'id': 0,
      'answer': 'You can use our REST APIs to manage your Knowledge Base. See here for details: https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da7600',
      'source': 'Custom Editorial',
      'questions': [
        'How do I programmatically update my Knowledge Base?'
      ],
      'metadata': [
        {
          'name': 'category',
          'value': 'api'
        }
      ]
    }
  ]
}

path = service + method + kb
# Convert the request to a string.
content = json.dumps(req)
result = replace_kb (path, content)
print (pretty_print(result))
```

<span data-ttu-id="a1660-160">**Replace knowledge base response**</span><span class="sxs-lookup"><span data-stu-id="a1660-160">**Replace knowledge base response**</span></span>

<span data-ttu-id="a1660-161">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="a1660-161">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json
{
    "result": "Success."
}
```

[<span data-ttu-id="a1660-162">Back to top</span><span class="sxs-lookup"><span data-stu-id="a1660-162">Back to top</span></span>](#HOLTop)

<a name="GetQnA"></a>

## <a name="download-the-contents-of-a-knowledge-base"></a><span data-ttu-id="a1660-163">Download the contents of a knowledge base</span><span class="sxs-lookup"><span data-stu-id="a1660-163">Download the contents of a knowledge base</span></span>

<span data-ttu-id="a1660-164">The following code downloads the contents of the specified knowledge base, using the [Download knowledge base](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/knowledgebases_download) method.</span><span class="sxs-lookup"><span data-stu-id="a1660-164">The following code downloads the contents of the specified knowledge base, using the [Download knowledge base](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/knowledgebases_download) method.</span></span>

1. <span data-ttu-id="a1660-165">Create a new Python project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="a1660-165">Create a new Python project in your favorite IDE.</span></span>
2. <span data-ttu-id="a1660-166">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="a1660-166">Add the code provided below.</span></span>
3. <span data-ttu-id="a1660-167">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="a1660-167">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="a1660-168">Run the program.</span><span class="sxs-lookup"><span data-stu-id="a1660-168">Run the program.</span></span>

```python
# -*- coding: utf-8 -*-

import http.client, urllib.parse, json, time

# **********************************************
# *** Update or verify the following values. ***
# **********************************************

# Replace this with a valid subscription key.
subscriptionKey = 'ENTER KEY HERE'

# Replace this with a valid knowledge base ID.
kb = 'ENTER ID HERE'

# Replace this with "test" or "prod".
env = 'test';

host = 'westus.api.cognitive.microsoft.com'
service = '/qnamaker/v4.0'
method = '/knowledgebases/{0}/{1}/qna/'.format(kb, env);

def pretty_print (content):
# Note: We convert content to and from an object so we can pretty-print it.
    return json.dumps(json.loads(content), indent=4)

def get_qna (path):
    print ('Calling ' + host + path + '.')
    headers = {
        'Ocp-Apim-Subscription-Key': subscriptionKey,
    }
    conn = http.client.HTTPSConnection(host)
    conn.request ("GET", path, '', headers)
    response = conn.getresponse ()
    return response.read ()

path = service + method
result = get_qna (path)
print (pretty_print(result))
```

<span data-ttu-id="a1660-169">**Download knowledge base response**</span><span class="sxs-lookup"><span data-stu-id="a1660-169">**Download knowledge base response**</span></span>

<span data-ttu-id="a1660-170">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="a1660-170">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json
{
  "qnaDocuments": [
    {
      "id": 1,
      "answer": "You can use our REST APIs to manage your Knowledge Base. See here for details: https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da7600",
      "source": "Custom Editorial",
      "questions": [
        "How do I programmatically update my Knowledge Base?"
      ],
      "metadata": [
        {
          "name": "category",
          "value": "api"
        }
      ]
    },
    {
      "id": 2,
      "answer": "QnA Maker provides an FAQ data source that you can query from your bot or application. Although developers will find this useful, content owners will especially benefit from this tool. QnA Maker is a completely no-code way of managing the content that powers your bot or application.",
      "source": "https://docs.microsoft.com/en-in/azure/cognitive-services/qnamaker/faqs",
      "questions": [
        "Who is the target audience for the QnA Maker tool?"
      ],
      "metadata": []
    },
...
  ]
}
```

[<span data-ttu-id="a1660-171">Back to top</span><span class="sxs-lookup"><span data-stu-id="a1660-171">Back to top</span></span>](#HOLTop)

<a name="GetAnswers"></a>

## <a name="get-answers-to-a-question-using-a-knowledge-base"></a><span data-ttu-id="a1660-172">Get answers to a question using a knowledge base</span><span class="sxs-lookup"><span data-stu-id="a1660-172">Get answers to a question using a knowledge base</span></span>

<span data-ttu-id="a1660-173">The following code gets answers to a question using the specified knowledge base, using the **Generate answers** method.</span><span class="sxs-lookup"><span data-stu-id="a1660-173">The following code gets answers to a question using the specified knowledge base, using the **Generate answers** method.</span></span>

1. <span data-ttu-id="a1660-174">Create a new Python project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="a1660-174">Create a new Python project in your favorite IDE.</span></span>
1. <span data-ttu-id="a1660-175">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="a1660-175">Add the code provided below.</span></span>
1. <span data-ttu-id="a1660-176">Replace the `host` value with the Website name for your QnA Maker subscription.</span><span class="sxs-lookup"><span data-stu-id="a1660-176">Replace the `host` value with the Website name for your QnA Maker subscription.</span></span> <span data-ttu-id="a1660-177">For more information see [Create a QnA Maker service](../How-To/set-up-qnamaker-service-azure.md).</span><span class="sxs-lookup"><span data-stu-id="a1660-177">For more information see [Create a QnA Maker service](../How-To/set-up-qnamaker-service-azure.md).</span></span>
1. <span data-ttu-id="a1660-178">Replace the `endpoint_key` value with a valid endpoint key for your subscription.</span><span class="sxs-lookup"><span data-stu-id="a1660-178">Replace the `endpoint_key` value with a valid endpoint key for your subscription.</span></span> <span data-ttu-id="a1660-179">Note this is not the same as your subscription key.</span><span class="sxs-lookup"><span data-stu-id="a1660-179">Note this is not the same as your subscription key.</span></span> <span data-ttu-id="a1660-180">You can get your endpoint keys using the [Get endpoint keys](#GetKeys) method.</span><span class="sxs-lookup"><span data-stu-id="a1660-180">You can get your endpoint keys using the [Get endpoint keys](#GetKeys) method.</span></span>
1. <span data-ttu-id="a1660-181">Replace the `kb` value with the ID of the knowledge base you want to query for answers.</span><span class="sxs-lookup"><span data-stu-id="a1660-181">Replace the `kb` value with the ID of the knowledge base you want to query for answers.</span></span> <span data-ttu-id="a1660-182">Note this knowledge base must already have been published using the [Publish](#Publish) method.</span><span class="sxs-lookup"><span data-stu-id="a1660-182">Note this knowledge base must already have been published using the [Publish](#Publish) method.</span></span>
1. <span data-ttu-id="a1660-183">Run the program.</span><span class="sxs-lookup"><span data-stu-id="a1660-183">Run the program.</span></span>

```python
# -*- coding: utf-8 -*-

import http.client, urllib.parse, json, time

# **********************************************
# *** Update or verify the following values. ***
# **********************************************

# NOTE: Replace this with a valid host name.
host = "ENTER HOST HERE"

# NOTE: Replace this with a valid endpoint key.
# This is not your subscription key.
# To get your endpoint keys, call the GET /endpointkeys method.
endpoint_key = "ENTER KEY HERE"

# NOTE: Replace this with a valid knowledge base ID.
# Make sure you have published the knowledge base with the
# POST /knowledgebases/{knowledge base ID} method.
kb = "ENTER KB ID HERE"

method = "/qnamaker/knowledgebases/" + kb + "/generateAnswer"

question = {
    'question': 'Is the QnA Maker Service free?',
    'top': 3
}

def pretty_print (content):
# Note: We convert content to and from an object so we can pretty-print it.
    return json.dumps(json.loads(content), indent=4)

def get_answers (path, content):
    print ('Calling ' + host + path + '.')
    headers = {
        'Authorization': 'EndpointKey ' + endpoint_key,
        'Content-Type': 'application/json',
        'Content-Length': len (content)
    }
    conn = http.client.HTTPSConnection(host)
    conn.request ("POST", path, content, headers)
    response = conn.getresponse ()
    return response.read ()

# Convert the request to a string.
content = json.dumps(question)
result = get_answers (method, content)
print (pretty_print(result))
```

<span data-ttu-id="a1660-184">**Get answers response**</span><span class="sxs-lookup"><span data-stu-id="a1660-184">**Get answers response**</span></span>

<span data-ttu-id="a1660-185">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="a1660-185">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json
{
  "answers": [
    {
      "questions": [
        "Can I use BitLocker with the Volume Shadow Copy Service?"
      ],
      "answer": "Yes. However, shadow copies made prior to enabling BitLocker will be automatically deleted when BitLocker is enabled on software-encrypted drives. If you are using a hardware encrypted drive, the shadow copies are retained.",
      "score": 17.3,
      "id": 62,
      "source": "https://docs.microsoft.com/en-us/windows/security/information-protection/bitlocker/bitlocker-frequently-asked-questions",
      "metadata": []
    },
...
  ]
}
```

[<span data-ttu-id="a1660-186">Back to top</span><span class="sxs-lookup"><span data-stu-id="a1660-186">Back to top</span></span>](#HOLTop)

<a name="GetKB"></a>

## <a name="get-information-about-a-knowledge-base"></a><span data-ttu-id="a1660-187">Get information about a knowledge base</span><span class="sxs-lookup"><span data-stu-id="a1660-187">Get information about a knowledge base</span></span>

<span data-ttu-id="a1660-188">The following code gets information about the specified knowledge base, using the [Get knowledge base details](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/knowledgebases_getknowledgebasedetails) method.</span><span class="sxs-lookup"><span data-stu-id="a1660-188">The following code gets information about the specified knowledge base, using the [Get knowledge base details](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/knowledgebases_getknowledgebasedetails) method.</span></span>

1. <span data-ttu-id="a1660-189">Create a new Python project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="a1660-189">Create a new Python project in your favorite IDE.</span></span>
2. <span data-ttu-id="a1660-190">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="a1660-190">Add the code provided below.</span></span>
3. <span data-ttu-id="a1660-191">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="a1660-191">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="a1660-192">Run the program.</span><span class="sxs-lookup"><span data-stu-id="a1660-192">Run the program.</span></span>

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

def get_kb (path):
    print ('Calling ' + host + path + '.')
    headers = {
        'Ocp-Apim-Subscription-Key': subscriptionKey,
    }
    conn = http.client.HTTPSConnection(host)
    conn.request ("GET", path, '', headers)
    response = conn.getresponse ()
    return response.read ()

path = service + method + kb
result = get_kb (path)
print (pretty_print(result))
```

<span data-ttu-id="a1660-193">**Get knowledge base details response**</span><span class="sxs-lookup"><span data-stu-id="a1660-193">**Get knowledge base details response**</span></span>

<span data-ttu-id="a1660-194">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="a1660-194">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json
{
  "id": "140a46f3-b248-4f1b-9349-614bfd6e5563",
  "hostName": "https://qna-docs.azurewebsites.net",
  "lastAccessedTimestamp": "2018-04-12T22:58:01Z",
  "lastChangedTimestamp": "2018-04-12T22:58:01Z",
  "name": "QnA Maker FAQ",
  "userId": "2280ef5917bb4ebfa1aae41fb1cebb4a",
  "urls": [
    "https://docs.microsoft.com/en-in/azure/cognitive-services/qnamaker/faqs",
    "https://docs.microsoft.com/en-us/bot-framework/resources-bot-framework-faq"
  ],
  "sources": [
    "Custom Editorial"
  ]
}
```

[<span data-ttu-id="a1660-195">Back to top</span><span class="sxs-lookup"><span data-stu-id="a1660-195">Back to top</span></span>](#HOLTop)

<a name="GetKBsByUser"></a>

## <a name="get-all-knowledge-bases-for-a-user"></a><span data-ttu-id="a1660-196">Get all knowledge bases for a user</span><span class="sxs-lookup"><span data-stu-id="a1660-196">Get all knowledge bases for a user</span></span>

<span data-ttu-id="a1660-197">The following code gets information about all knowledge bases for a specified user, using the [Get knowledge bases for user](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/knowledgebases_getknowledgebasesforuser) method.</span><span class="sxs-lookup"><span data-stu-id="a1660-197">The following code gets information about all knowledge bases for a specified user, using the [Get knowledge bases for user](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/knowledgebases_getknowledgebasesforuser) method.</span></span>

1. <span data-ttu-id="a1660-198">Create a new Python project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="a1660-198">Create a new Python project in your favorite IDE.</span></span>
2. <span data-ttu-id="a1660-199">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="a1660-199">Add the code provided below.</span></span>
3. <span data-ttu-id="a1660-200">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="a1660-200">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="a1660-201">Run the program.</span><span class="sxs-lookup"><span data-stu-id="a1660-201">Run the program.</span></span>

```python
# -*- coding: utf-8 -*-

import http.client, urllib.parse, json, time

# **********************************************
# *** Update or verify the following values. ***
# **********************************************

# Replace this with a valid subscription key.
subscriptionKey = 'ENTER KEY HERE'

host = 'westus.api.cognitive.microsoft.com'
service = '/qnamaker/v4.0'
method = '/knowledgebases/'

def pretty_print (content):
# Note: We convert content to and from an object so we can pretty-print it.
    return json.dumps(json.loads(content), indent=4)

def get_kbs (path):
    print ('Calling ' + host + path + '.')
    headers = {
        'Ocp-Apim-Subscription-Key': subscriptionKey,
    }
    conn = http.client.HTTPSConnection(host)
    conn.request ("GET", path, '', headers)
    response = conn.getresponse ()
    return response.read ()

path = service + method
result = get_kbs (path)
print (pretty_print(result))
```

<span data-ttu-id="a1660-202">**Get knowledge bases for user response**</span><span class="sxs-lookup"><span data-stu-id="a1660-202">**Get knowledge bases for user response**</span></span>

<span data-ttu-id="a1660-203">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="a1660-203">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json
{
  "knowledgebases": [
    {
      "id": "081c32a7-bd05-4982-9d74-07ac736df0ac",
      "hostName": "https://qna-docs.azurewebsites.net",
      "lastAccessedTimestamp": "2018-04-12T11:51:58Z",
      "lastChangedTimestamp": "2018-04-12T11:51:58Z",
      "name": "QnA Maker FAQ",
      "userId": "2280ef5917bb4ebfa1aae41fb1cebb4a",
      "urls": [],
      "sources": []
    },
    {
      "id": "140a46f3-b248-4f1b-9349-614bfd6e5563",
      "hostName": "https://qna-docs.azurewebsites.net",
      "lastAccessedTimestamp": "2018-04-12T22:58:01Z",
      "lastChangedTimestamp": "2018-04-12T22:58:01Z",
      "name": "QnA Maker FAQ",
      "userId": "2280ef5917bb4ebfa1aae41fb1cebb4a",
      "urls": [
        "https://docs.microsoft.com/en-in/azure/cognitive-services/qnamaker/faqs",
        "https://docs.microsoft.com/en-us/bot-framework/resources-bot-framework-faq"
      ],
      "sources": [
        "Custom Editorial"
      ]
    },
...
  ]
}
Press any key to continue.
```

[<span data-ttu-id="a1660-204">Back to top</span><span class="sxs-lookup"><span data-stu-id="a1660-204">Back to top</span></span>](#HOLTop)

<a name="Delete"></a>

## <a name="delete-a-knowledge-base"></a><span data-ttu-id="a1660-205">Delete a knowledge base</span><span class="sxs-lookup"><span data-stu-id="a1660-205">Delete a knowledge base</span></span>

<span data-ttu-id="a1660-206">The following code deletes the specified knowledge base, using the [Delete knowledge base](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/knowledgebases_delete) method.</span><span class="sxs-lookup"><span data-stu-id="a1660-206">The following code deletes the specified knowledge base, using the [Delete knowledge base](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/knowledgebases_delete) method.</span></span>

1. <span data-ttu-id="a1660-207">Create a new Python project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="a1660-207">Create a new Python project in your favorite IDE.</span></span>
2. <span data-ttu-id="a1660-208">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="a1660-208">Add the code provided below.</span></span>
3. <span data-ttu-id="a1660-209">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="a1660-209">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="a1660-210">Run the program.</span><span class="sxs-lookup"><span data-stu-id="a1660-210">Run the program.</span></span>

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

def delete_kb (path, content):
    print ('Calling ' + host + path + '.')
    headers = {
        'Ocp-Apim-Subscription-Key': subscriptionKey,
        'Content-Type': 'application/json',
        'Content-Length': len (content)
    }
    conn = http.client.HTTPSConnection(host)
    conn.request ("DELETE", path, content, headers)
    response = conn.getresponse ()

    if response.status == 204:
        return json.dumps({'result' : 'Success.'})
    else:
        return response.read ()

path = service + method + kb
result = delete_kb (path, '')
print (pretty_print(result))
```

<span data-ttu-id="a1660-211">**Delete knowledge base response**</span><span class="sxs-lookup"><span data-stu-id="a1660-211">**Delete knowledge base response**</span></span>

<span data-ttu-id="a1660-212">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="a1660-212">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json
{
  "result": "Success."
}
```

[<span data-ttu-id="a1660-213">Back to top</span><span class="sxs-lookup"><span data-stu-id="a1660-213">Back to top</span></span>](#HOLTop)

<a name="GetKeys"></a>

## <a name="get-endpoint-keys"></a><span data-ttu-id="a1660-214">Get endpoint keys</span><span class="sxs-lookup"><span data-stu-id="a1660-214">Get endpoint keys</span></span>

<span data-ttu-id="a1660-215">The following code gets the current endpoint keys, using the [Get endpoint keys](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/endpointkeys_getendpointkeys) method.</span><span class="sxs-lookup"><span data-stu-id="a1660-215">The following code gets the current endpoint keys, using the [Get endpoint keys](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/endpointkeys_getendpointkeys) method.</span></span>

1. <span data-ttu-id="a1660-216">Create a new Python project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="a1660-216">Create a new Python project in your favorite IDE.</span></span>
2. <span data-ttu-id="a1660-217">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="a1660-217">Add the code provided below.</span></span>
3. <span data-ttu-id="a1660-218">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="a1660-218">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="a1660-219">Run the program.</span><span class="sxs-lookup"><span data-stu-id="a1660-219">Run the program.</span></span>

```python
# -*- coding: utf-8 -*-

import http.client, urllib.parse, json, time

# **********************************************
# *** Update or verify the following values. ***
# **********************************************

# Replace this with a valid subscription key.
subscriptionKey = 'ENTER KEY HERE'

host = 'westus.api.cognitive.microsoft.com'
service = '/qnamaker/v4.0'
method = '/endpointkeys/'

def pretty_print (content):
# Note: We convert content to and from an object so we can pretty-print it.
    return json.dumps(json.loads(content), indent=4)

def get_keys (path):
    print ('Calling ' + host + path + '.')
    headers = {
        'Ocp-Apim-Subscription-Key': subscriptionKey,
    }
    conn = http.client.HTTPSConnection(host)
    conn.request ("GET", path, '', headers)
    response = conn.getresponse ()
    return response.read ()

path = service + method
result = get_keys (path)
print (pretty_print(result))
```

<span data-ttu-id="a1660-220">**Get endpoint keys response**</span><span class="sxs-lookup"><span data-stu-id="a1660-220">**Get endpoint keys response**</span></span>

<span data-ttu-id="a1660-221">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="a1660-221">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json
{
  "primaryEndpointKey": "ac110bdc-34b7-4b1c-b9cd-b05f9a6001f3",
  "secondaryEndpointKey": "1b4ed14e-614f-444a-9f3d-9347f45a9206"
}
```

[<span data-ttu-id="a1660-222">Back to top</span><span class="sxs-lookup"><span data-stu-id="a1660-222">Back to top</span></span>](#HOLTop)

<a name="PutKeys"></a>

## <a name="refresh-endpoint-keys"></a><span data-ttu-id="a1660-223">Refresh endpoint keys</span><span class="sxs-lookup"><span data-stu-id="a1660-223">Refresh endpoint keys</span></span>

<span data-ttu-id="a1660-224">The following code regenerates the current endpoint keys, using the [Refresh endpoint keys](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/endpointkeys_refreshendpointkeys) method.</span><span class="sxs-lookup"><span data-stu-id="a1660-224">The following code regenerates the current endpoint keys, using the [Refresh endpoint keys](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/endpointkeys_refreshendpointkeys) method.</span></span>

1. <span data-ttu-id="a1660-225">Create a new Python project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="a1660-225">Create a new Python project in your favorite IDE.</span></span>
2. <span data-ttu-id="a1660-226">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="a1660-226">Add the code provided below.</span></span>
3. <span data-ttu-id="a1660-227">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="a1660-227">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="a1660-228">Run the program.</span><span class="sxs-lookup"><span data-stu-id="a1660-228">Run the program.</span></span>

```python
# -*- coding: utf-8 -*-

import http.client, urllib.parse, json, time

# **********************************************
# *** Update or verify the following values. ***
# **********************************************

# Replace this with a valid subscription key.
subscriptionKey = 'ENTER KEY HERE'

# Replace this with "PrimaryKey" or "SecondaryKey."
key_type = "PrimaryKey";

host = 'westus.api.cognitive.microsoft.com'
service = '/qnamaker/v4.0'
method = '/endpointkeys/'

def pretty_print (content):
# Note: We convert content to and from an object so we can pretty-print it.
    return json.dumps(json.loads(content), indent=4)

def refresh_keys (path, content):
    print ('Calling ' + host + path + '.')
    headers = {
        'Ocp-Apim-Subscription-Key': subscriptionKey,
        'Content-Type': 'application/json',
        'Content-Length': len (content)
    }
    conn = http.client.HTTPSConnection(host)
    conn.request ("PATCH", path, content, headers)
    response = conn.getresponse ()

    if response.status == 204:
        return json.dumps({'result' : 'Success.'})
    else:
        return response.read ()

path = service + method + key_type
result = refresh_keys (path, '')
print (pretty_print(result))
```

<span data-ttu-id="a1660-229">**Refresh endpoint keys response**</span><span class="sxs-lookup"><span data-stu-id="a1660-229">**Refresh endpoint keys response**</span></span>

<span data-ttu-id="a1660-230">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="a1660-230">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json
{
  "primaryEndpointKey": "ac110bdc-34b7-4b1c-b9cd-b05f9a6001f3",
  "secondaryEndpointKey": "1b4ed14e-614f-444a-9f3d-9347f45a9206"
}
```

[<span data-ttu-id="a1660-231">Back to top</span><span class="sxs-lookup"><span data-stu-id="a1660-231">Back to top</span></span>](#HOLTop)

<a name="GetAlterations"></a>

## <a name="get-word-alterations"></a><span data-ttu-id="a1660-232">Get word alterations</span><span class="sxs-lookup"><span data-stu-id="a1660-232">Get word alterations</span></span>

<span data-ttu-id="a1660-233">The following code gets the current word alterations, using the [Download alterations](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da75fc) method.</span><span class="sxs-lookup"><span data-stu-id="a1660-233">The following code gets the current word alterations, using the [Download alterations](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da75fc) method.</span></span>

1. <span data-ttu-id="a1660-234">Create a new Python project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="a1660-234">Create a new Python project in your favorite IDE.</span></span>
2. <span data-ttu-id="a1660-235">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="a1660-235">Add the code provided below.</span></span>
3. <span data-ttu-id="a1660-236">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="a1660-236">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="a1660-237">Run the program.</span><span class="sxs-lookup"><span data-stu-id="a1660-237">Run the program.</span></span>

```python
# -*- coding: utf-8 -*-

import http.client, urllib.parse, json, time

# **********************************************
# *** Update or verify the following values. ***
# **********************************************

# Replace this with a valid subscription key.
subscriptionKey = 'ENTER KEY HERE'

host = 'westus.api.cognitive.microsoft.com'
service = '/qnamaker/v4.0'
method = '/alterations/'

def pretty_print (content):
# Note: We convert content to and from an object so we can pretty-print it.
    return json.dumps(json.loads(content), indent=4)

def get_alterations (path):
    print ('Calling ' + host + path + '.')
    headers = {
        'Ocp-Apim-Subscription-Key': subscriptionKey,
    }
    conn = http.client.HTTPSConnection(host)
    conn.request ("GET", path, '', headers)
    response = conn.getresponse ()
    return response.read ()

path = service + method
result = get_alterations (path)
print (pretty_print(result))
```

<span data-ttu-id="a1660-238">**Get word alterations response**</span><span class="sxs-lookup"><span data-stu-id="a1660-238">**Get word alterations response**</span></span>

<span data-ttu-id="a1660-239">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="a1660-239">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json
{
  "wordAlterations": [
    {
      "alterations": [
        "botframework",
        "bot frame work"
      ]
    }
  ]
}
```

[<span data-ttu-id="a1660-240">Back to top</span><span class="sxs-lookup"><span data-stu-id="a1660-240">Back to top</span></span>](#HOLTop)

<a name="PutAlterations"></a>

## <a name="replace-word-alterations"></a><span data-ttu-id="a1660-241">Replace word alterations</span><span class="sxs-lookup"><span data-stu-id="a1660-241">Replace word alterations</span></span>

<span data-ttu-id="a1660-242">The following code replaces the current word alterations, using the [Replace alterations](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da75fd) method.</span><span class="sxs-lookup"><span data-stu-id="a1660-242">The following code replaces the current word alterations, using the [Replace alterations](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da75fd) method.</span></span>

1. <span data-ttu-id="a1660-243">Create a new Python project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="a1660-243">Create a new Python project in your favorite IDE.</span></span>
2. <span data-ttu-id="a1660-244">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="a1660-244">Add the code provided below.</span></span>
3. <span data-ttu-id="a1660-245">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="a1660-245">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="a1660-246">Run the program.</span><span class="sxs-lookup"><span data-stu-id="a1660-246">Run the program.</span></span>

```python
# -*- coding: utf-8 -*-

import http.client, urllib.parse, json, time

# **********************************************
# *** Update or verify the following values. ***
# **********************************************

# Replace this with a valid subscription key.
subscriptionKey = 'ENTER KEY HERE'

host = 'westus.api.cognitive.microsoft.com'
service = '/qnamaker/v4.0'
method = '/alterations/'

def pretty_print (content):
# Note: We convert content to and from an object so we can pretty-print it.
    return json.dumps(json.loads(content), indent=4)

def put_alterations (path, content):
    print ('Calling ' + host + path + '.')
    headers = {
        'Ocp-Apim-Subscription-Key': subscriptionKey,
        'Content-Type': 'application/json',
        'Content-Length': len (content)
    }
    conn = http.client.HTTPSConnection(host)
    conn.request ("PUT", path, content, headers)
    response = conn.getresponse ()

    if response.status == 204:
        return json.dumps({'result' : 'Success.'})
    else:
        return response.read ()

req = {
  'wordAlterations': [
    {
      'alterations': [
        'botframework',
        'bot frame work'
      ]
    }
  ]
}

path = service + method
# Convert the request to a string.
content = json.dumps(req)
result = put_alterations (path, content)
print (pretty_print(result))
```

<span data-ttu-id="a1660-247">**Replace word alterations response**</span><span class="sxs-lookup"><span data-stu-id="a1660-247">**Replace word alterations response**</span></span>

<span data-ttu-id="a1660-248">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="a1660-248">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json
{
  "result": "Success."
}
```

[<span data-ttu-id="a1660-249">Back to top</span><span class="sxs-lookup"><span data-stu-id="a1660-249">Back to top</span></span>](#HOLTop)

## <a name="next-steps"></a><span data-ttu-id="a1660-250">Next steps</span><span class="sxs-lookup"><span data-stu-id="a1660-250">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a1660-251">QnA Maker (V4) REST API Reference</span><span class="sxs-lookup"><span data-stu-id="a1660-251">QnA Maker (V4) REST API Reference</span></span>](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da75ff)

## <a name="see-also"></a><span data-ttu-id="a1660-252">See also</span><span class="sxs-lookup"><span data-stu-id="a1660-252">See also</span></span> 

[<span data-ttu-id="a1660-253">QnA Maker overview</span><span class="sxs-lookup"><span data-stu-id="a1660-253">QnA Maker overview</span></span>](../Overview/overview.md)
