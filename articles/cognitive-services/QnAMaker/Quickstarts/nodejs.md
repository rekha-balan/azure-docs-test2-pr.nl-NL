---
title: 'Quickstart: Node.js for QnA Maker API (V4)'
titleSuffix: Azure Cognitive Services
description: Get information and code samples to help you quickly get started using the Microsoft Translator Text API in Microsoft Cognitive Services on Azure.
services: cognitive-services
author: nitinme
manager: cgronlun
ms.service: cognitive-services
ms.technology: qna-maker
ms.topic: article
ms.date: 05/07/2018
ms.author: v-jaswel
ms.openlocfilehash: 1930315cae62081dae364d63e6b26ec26a69c654
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864731"
---
# <a name="quickstart-for-microsoft-qna-maker-api-with-nodejs"></a><span data-ttu-id="a75c4-103">Quickstart for Microsoft QnA Maker API with Node.js</span><span class="sxs-lookup"><span data-stu-id="a75c4-103">Quickstart for Microsoft QnA Maker API with Node.js</span></span> 
<a name="HOLTop"></a>

<span data-ttu-id="a75c4-104">This article shows you how to use the [Microsoft QnA Maker API](../Overview/overview.md) with Node.js to do the following.</span><span class="sxs-lookup"><span data-stu-id="a75c4-104">This article shows you how to use the [Microsoft QnA Maker API](../Overview/overview.md) with Node.js to do the following.</span></span>

- [<span data-ttu-id="a75c4-105">Create a new knowledge base.</span><span class="sxs-lookup"><span data-stu-id="a75c4-105">Create a new knowledge base.</span></span>](#Create)
- [<span data-ttu-id="a75c4-106">Update an existing knowledge base.</span><span class="sxs-lookup"><span data-stu-id="a75c4-106">Update an existing knowledge base.</span></span>](#Update)
- [<span data-ttu-id="a75c4-107">Get the status of a request to create or update a knowledge base.</span><span class="sxs-lookup"><span data-stu-id="a75c4-107">Get the status of a request to create or update a knowledge base.</span></span>](#Status)
- [<span data-ttu-id="a75c4-108">Publish an existing knowledge base.</span><span class="sxs-lookup"><span data-stu-id="a75c4-108">Publish an existing knowledge base.</span></span>](#Publish)
- [<span data-ttu-id="a75c4-109">Replace the contents of an existing knowledge base.</span><span class="sxs-lookup"><span data-stu-id="a75c4-109">Replace the contents of an existing knowledge base.</span></span>](#Replace)
- [<span data-ttu-id="a75c4-110">Download the contents of a knowledge base.</span><span class="sxs-lookup"><span data-stu-id="a75c4-110">Download the contents of a knowledge base.</span></span>](#GetQnA)
- [<span data-ttu-id="a75c4-111">Get answers to a question using a knowledge base.</span><span class="sxs-lookup"><span data-stu-id="a75c4-111">Get answers to a question using a knowledge base.</span></span>](#GetAnswers)
- [<span data-ttu-id="a75c4-112">Get information about a knowledge base.</span><span class="sxs-lookup"><span data-stu-id="a75c4-112">Get information about a knowledge base.</span></span>](#GetKB)
- [<span data-ttu-id="a75c4-113">Get information about all knowledge bases belonging to the specified user.</span><span class="sxs-lookup"><span data-stu-id="a75c4-113">Get information about all knowledge bases belonging to the specified user.</span></span>](#GetKBsByUser)
- [<span data-ttu-id="a75c4-114">Delete a knowledge base.</span><span class="sxs-lookup"><span data-stu-id="a75c4-114">Delete a knowledge base.</span></span>](#Delete)
- [<span data-ttu-id="a75c4-115">Get the current endpoint keys.</span><span class="sxs-lookup"><span data-stu-id="a75c4-115">Get the current endpoint keys.</span></span>](#GetKeys)
- [<span data-ttu-id="a75c4-116">Re-generate the current endpoint keys.</span><span class="sxs-lookup"><span data-stu-id="a75c4-116">Re-generate the current endpoint keys.</span></span>](#PutKeys)
- [<span data-ttu-id="a75c4-117">Get the current set of word alterations.</span><span class="sxs-lookup"><span data-stu-id="a75c4-117">Get the current set of word alterations.</span></span>](#GetAlterations)
- [<span data-ttu-id="a75c4-118">Replace the current set of word alterations.</span><span class="sxs-lookup"><span data-stu-id="a75c4-118">Replace the current set of word alterations.</span></span>](#PutAlterations)

## <a name="prerequisites"></a><span data-ttu-id="a75c4-119">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a75c4-119">Prerequisites</span></span>

<span data-ttu-id="a75c4-120">You will need [Node.js 6](https://nodejs.org/en/download/) to run this code.</span><span class="sxs-lookup"><span data-stu-id="a75c4-120">You will need [Node.js 6](https://nodejs.org/en/download/) to run this code.</span></span>

<span data-ttu-id="a75c4-121">You must have a [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) with **Microsoft QnA Maker API**.</span><span class="sxs-lookup"><span data-stu-id="a75c4-121">You must have a [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) with **Microsoft QnA Maker API**.</span></span> <span data-ttu-id="a75c4-122">You will need a paid subscription key from your [Azure dashboard](https://portal.azure.com/#create/Microsoft.CognitiveServices).</span><span class="sxs-lookup"><span data-stu-id="a75c4-122">You will need a paid subscription key from your [Azure dashboard](https://portal.azure.com/#create/Microsoft.CognitiveServices).</span></span>

<a name="Create"></a>

## <a name="create-knowledge-base"></a><span data-ttu-id="a75c4-123">Create knowledge base</span><span class="sxs-lookup"><span data-stu-id="a75c4-123">Create knowledge base</span></span>

<span data-ttu-id="a75c4-124">The following code creates a new knowledge base, using the [Create](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da75ff) method.</span><span class="sxs-lookup"><span data-stu-id="a75c4-124">The following code creates a new knowledge base, using the [Create](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da75ff) method.</span></span>

1. <span data-ttu-id="a75c4-125">Create a new Node.js project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="a75c4-125">Create a new Node.js project in your favorite IDE.</span></span>
2. <span data-ttu-id="a75c4-126">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="a75c4-126">Add the code provided below.</span></span>
3. <span data-ttu-id="a75c4-127">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="a75c4-127">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="a75c4-128">Run the program.</span><span class="sxs-lookup"><span data-stu-id="a75c4-128">Run the program.</span></span>

```nodejs
'use strict';

let fs = require ('fs');
let https = require ('https');

// **********************************************
// *** Update or verify the following values. ***
// **********************************************

// Replace this with a valid subscription key.
let subscriptionKey = 'ENTER KEY HERE';

let host = 'westus.api.cognitive.microsoft.com';
let service = '/qnamaker/v4.0';
let method = '/knowledgebases/create';

let pretty_print = function (s) {
    return JSON.stringify(JSON.parse(s), null, 4);
}

// callback is the function to call when we have the entire response.
let response_handler = function (callback, response) {
    let body = '';
    response.on ('data', function (d) {
        body += d;
    });
    response.on ('end', function () {
// Call the callback function with the status code, headers, and body of the response.
        callback ({ status : response.statusCode, headers : response.headers, body : body });
    });
    response.on ('error', function (e) {
        console.log ('Error: ' + e.message);
    });
};

// Get an HTTP response handler that calls the specified callback function when we have the entire response.
let get_response_handler = function (callback) {
// Return a function that takes an HTTP response, and is closed over the specified callback.
// This function signature is required by https.request, hence the need for the closure.
    return function (response) {
        response_handler (callback, response);
    }
}

// callback is the function to call when we have the entire response from the POST request.
let post = function (path, content, callback) {
    let request_params = {
        method : 'POST',
        hostname : host,
        path : path,
        headers : {
            'Content-Type' : 'application/json',
            'Content-Length' : content.length,
            'Ocp-Apim-Subscription-Key' : subscriptionKey,
        }
    };

// Pass the callback function to the response handler.
    let req = https.request (request_params, get_response_handler (callback));
    req.write (content);
    req.end ();
}

// callback is the function to call when we have the entire response from the GET request.
let get = function (path, callback) {
    let request_params = {
        method : 'GET',
        hostname : host,
        path : path,
        headers : {
            'Ocp-Apim-Subscription-Key' : subscriptionKey,
        }
    };

// Pass the callback function to the response handler.
    let req = https.request (request_params, get_response_handler (callback));
    req.end ();
}

// callback is the function to call when we have the response from the /knowledgebases/create POST method.
let create_kb = function (path, req, callback) {
    console.log ('Calling ' + host + path + '.');
// Send the POST request.
    post (path, req, function (response) {
// Extract the data we want from the POST response and pass it to the callback function.
        callback ({ operation : response.headers.location, response : response.body });
    });
}

// callback is the function to call when we have the response from the GET request to check the status.
let check_status = function (path, callback) {
    console.log ('Calling ' + host + path + '.');
// Send the GET request.
    get (path, function (response) {
// Extract the data we want from the GET response and pass it to the callback function.
        callback ({ wait : response.headers['retry-after'], response : response.body });
    });
}

let req = {
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
};

var path = service + method;
// Convert the request to a string.
let content = JSON.stringify(req);
create_kb (path, content, function (result) {
// Write out the response from the /knowledgebases/create method.
    console.log (pretty_print(result.response));
// Loop until the operation is complete.
    let loop = function () {
        path = service + result.operation;
// Check the status of the operation.
        check_status (path, function (status) {
// Write out the status.
            console.log (pretty_print(status.response));
// Convert the status into an object and get the value of the operationState field.
            var state = (JSON.parse(status.response)).operationState;
// If the operation isn't complete, wait and query again.
            if (state == 'Running' || state == 'NotStarted') {
                console.log ('Waiting ' + status.wait + ' seconds...');
                setTimeout(loop, status.wait * 1000);
            }
        });
    }
// Begin the loop.
    loop();
});
```

<span data-ttu-id="a75c4-129">**Create knowledge base response**</span><span class="sxs-lookup"><span data-stu-id="a75c4-129">**Create knowledge base response**</span></span>

<span data-ttu-id="a75c4-130">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="a75c4-130">A successful response is returned in JSON, as shown in the following example:</span></span> 

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

[<span data-ttu-id="a75c4-131">Back to top</span><span class="sxs-lookup"><span data-stu-id="a75c4-131">Back to top</span></span>](#HOLTop)

<a name="Update"></a>

## <a name="update-knowledge-base"></a><span data-ttu-id="a75c4-132">Update knowledge base</span><span class="sxs-lookup"><span data-stu-id="a75c4-132">Update knowledge base</span></span>

<span data-ttu-id="a75c4-133">The following code updates an existing knowledge base, using the [Update](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da7600) method.</span><span class="sxs-lookup"><span data-stu-id="a75c4-133">The following code updates an existing knowledge base, using the [Update](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da7600) method.</span></span>

1. <span data-ttu-id="a75c4-134">Create a new Node.js project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="a75c4-134">Create a new Node.js project in your favorite IDE.</span></span>
2. <span data-ttu-id="a75c4-135">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="a75c4-135">Add the code provided below.</span></span>
3. <span data-ttu-id="a75c4-136">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="a75c4-136">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="a75c4-137">Run the program.</span><span class="sxs-lookup"><span data-stu-id="a75c4-137">Run the program.</span></span>

```nodejs
'use strict';

let fs = require ('fs');
let https = require ('https');

// **********************************************
// *** Update or verify the following values. ***
// **********************************************

// Replace this with a valid subscription key.
let subscriptionKey = 'ENTER KEY HERE';

// NOTE: Replace this with a valid knowledge base ID.
let kb = 'ENTER ID HERE';

let host = 'westus.api.cognitive.microsoft.com';
let service = '/qnamaker/v4.0';
let method = '/knowledgebases/';

let pretty_print = function (s) {
    return JSON.stringify(JSON.parse(s), null, 4);
}

// callback is the function to call when we have the entire response.
let response_handler = function (callback, response) {
    let body = '';
    response.on ('data', function (d) {
        body += d;
    });
    response.on ('end', function () {
// Call the callback function with the status code, headers, and body of the response.
        callback ({ status : response.statusCode, headers : response.headers, body : body });
    });
    response.on ('error', function (e) {
        console.log ('Error: ' + e.message);
    });
};

// Get an HTTP response handler that calls the specified callback function when we have the entire response.
let get_response_handler = function (callback) {
// Return a function that takes an HTTP response, and is closed over the specified callback.
// This function signature is required by https.request, hence the need for the closure.
    return function (response) {
        response_handler (callback, response);
    }
}

// callback is the function to call when we have the entire response from the PATCH request.
let patch = function (path, content, callback) {
    let request_params = {
        method : 'PATCH',
        hostname : host,
        path : path,
        headers : {
            'Content-Type' : 'application/json',
            'Content-Length' : content.length,
            'Ocp-Apim-Subscription-Key' : subscriptionKey,
        }
    };

// Pass the callback function to the response handler.
    let req = https.request (request_params, get_response_handler (callback));
    req.write (content);
    req.end ();
}

// callback is the function to call when we have the entire response from the GET request.
let get = function (path, callback) {
    let request_params = {
        method : 'GET',
        hostname : host,
        path : path,
        headers : {
            'Ocp-Apim-Subscription-Key' : subscriptionKey,
        }
    };

// Pass the callback function to the response handler.
    let req = https.request (request_params, get_response_handler (callback));
    req.end ();
}

// callback is the function to call when we have the response from the /knowledgebases PATCH method.
let update_kb = function (path, req, callback) {
    console.log ('Calling ' + host + path + '.');
// Send the PATCH request.
    patch (path, req, function (response) {
// Extract the data we want from the PATCH response and pass it to the callback function.
        callback ({ operation : response.headers.location, response : response.body });
    });
}

// callback is the function to call when we have the response from the GET request to check the status.
let check_status = function (path, callback) {
    console.log ('Calling ' + host + path + '.');
// Send the GET request.
    get (path, function (response) {
// Extract the data we want from the GET response and pass it to the callback function.
        callback ({ wait : response.headers['retry-after'], response : response.body });
    });
}

let req = {
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
};

var path = service + method + kb;
// Convert the request to a string.
let content = JSON.stringify(req);
update_kb (path, content, function (result) {
    console.log (pretty_print(result.response));
// Loop until the operation is complete.
    let loop = function () {
        path = service + result.operation;
// Check the status of the operation.
        check_status (path, function (status) {
// Write out the status.
            console.log (pretty_print(status.response));
// Convert the status into an object and get the value of the operationState field.
            var state = (JSON.parse(status.response)).operationState;
// If the operation isn't complete, wait and query again.
            if (state == 'Running' || state == 'NotStarted') {
                console.log ('Waiting ' + status.wait + ' seconds...');
                setTimeout(loop, status.wait * 1000);
            }
        });
    }
// Begin the loop.
    loop();
});
```

<span data-ttu-id="a75c4-138">**Update knowledge base response**</span><span class="sxs-lookup"><span data-stu-id="a75c4-138">**Update knowledge base response**</span></span>

<span data-ttu-id="a75c4-139">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="a75c4-139">A successful response is returned in JSON, as shown in the following example:</span></span> 

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

[<span data-ttu-id="a75c4-140">Back to top</span><span class="sxs-lookup"><span data-stu-id="a75c4-140">Back to top</span></span>](#HOLTop)

<a name="Status"></a>

## <a name="get-request-status"></a><span data-ttu-id="a75c4-141">Get request status</span><span class="sxs-lookup"><span data-stu-id="a75c4-141">Get request status</span></span>

<span data-ttu-id="a75c4-142">You can call the [Operation](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/operations_getoperationdetails) method to check the status of a request to create or update a knowledge base.</span><span class="sxs-lookup"><span data-stu-id="a75c4-142">You can call the [Operation](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/operations_getoperationdetails) method to check the status of a request to create or update a knowledge base.</span></span> <span data-ttu-id="a75c4-143">To see how this method is used, please see the sample code for the [Create](#Create) or [Update](#Update) method.</span><span class="sxs-lookup"><span data-stu-id="a75c4-143">To see how this method is used, please see the sample code for the [Create](#Create) or [Update](#Update) method.</span></span>

[<span data-ttu-id="a75c4-144">Back to top</span><span class="sxs-lookup"><span data-stu-id="a75c4-144">Back to top</span></span>](#HOLTop)

<a name="Publish"></a>

## <a name="publish-knowledge-base"></a><span data-ttu-id="a75c4-145">Publish knowledge base</span><span class="sxs-lookup"><span data-stu-id="a75c4-145">Publish knowledge base</span></span>

<span data-ttu-id="a75c4-146">The following code publishes an existing knowledge base, using the [Publish](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da75fe) method.</span><span class="sxs-lookup"><span data-stu-id="a75c4-146">The following code publishes an existing knowledge base, using the [Publish](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da75fe) method.</span></span>

1. <span data-ttu-id="a75c4-147">Create a new Node.js project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="a75c4-147">Create a new Node.js project in your favorite IDE.</span></span>
2. <span data-ttu-id="a75c4-148">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="a75c4-148">Add the code provided below.</span></span>
3. <span data-ttu-id="a75c4-149">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="a75c4-149">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="a75c4-150">Run the program.</span><span class="sxs-lookup"><span data-stu-id="a75c4-150">Run the program.</span></span>

```nodejs
'use strict';

let fs = require ('fs');
let https = require ('https');

// **********************************************
// *** Update or verify the following values. ***
// **********************************************

// Replace this with a valid subscription key.
let subscriptionKey = 'ENTER KEY HERE';

// NOTE: Replace this with a valid knowledge base ID.
let kb = 'ENTER ID HERE';

let host = 'westus.api.cognitive.microsoft.com';
let service = '/qnamaker/v4.0';
let method = '/knowledgebases/';

let pretty_print = function (s) {
    return JSON.stringify(JSON.parse(s), null, 4);
}

// callback is the function to call when we have the entire response.
let response_handler = function (callback, response) {
    let body = '';
    response.on ('data', function (d) {
        body += d;
    });
    response.on ('end', function () {
// Call the callback function with the status code, headers, and body of the response.
        callback ({ status : response.statusCode, headers : response.headers, body : body });
    });
    response.on ('error', function (e) {
        console.log ('Error: ' + e.message);
    });
};

// Get an HTTP response handler that calls the specified callback function when we have the entire response.
let get_response_handler = function (callback) {
// Return a function that takes an HTTP response, and is closed over the specified callback.
// This function signature is required by https.request, hence the need for the closure.
    return function (response) {
        response_handler (callback, response);
    }
}

// callback is the function to call when we have the entire response from the POST request.
let post = function (path, content, callback) {
    let request_params = {
        method : 'POST',
        hostname : host,
        path : path,
        headers : {
            'Content-Type' : 'application/json',
            'Content-Length' : content.length,
            'Ocp-Apim-Subscription-Key' : subscriptionKey,
        }
    };

// Pass the callback function to the response handler.
    let req = https.request (request_params, get_response_handler (callback));
    req.write (content);
    req.end ();
}

// callback is the function to call when we have the response from the /knowledgebases POST method.
let publish_kb = function (path, req, callback) {
    console.log ('Calling ' + host + path + '.');
// Send the POST request.
    post (path, req, function (response) {
// Extract the data we want from the POST response and pass it to the callback function.
        if (response.status == '204') {
            let result = {'result':'Success'};
            callback (JSON.stringify(result));
        }
        else {
            callback (response.body);
        }
    });
}

var path = service + method + kb;
publish_kb (path, '', function (result) {
    console.log (pretty_print(result));
});
```

<span data-ttu-id="a75c4-151">**Publish knowledge base response**</span><span class="sxs-lookup"><span data-stu-id="a75c4-151">**Publish knowledge base response**</span></span>

<span data-ttu-id="a75c4-152">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="a75c4-152">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json
{
  "result": "Success."
}
```

[<span data-ttu-id="a75c4-153">Back to top</span><span class="sxs-lookup"><span data-stu-id="a75c4-153">Back to top</span></span>](#HOLTop)

<a name="Replace"></a>

## <a name="replace-knowledge-base"></a><span data-ttu-id="a75c4-154">Replace knowledge base</span><span class="sxs-lookup"><span data-stu-id="a75c4-154">Replace knowledge base</span></span>

<span data-ttu-id="a75c4-155">The following code replaces the contents of the specified knowledge base, using the [Replace](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/knowledgebases_publish) method.</span><span class="sxs-lookup"><span data-stu-id="a75c4-155">The following code replaces the contents of the specified knowledge base, using the [Replace](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/knowledgebases_publish) method.</span></span>

1. <span data-ttu-id="a75c4-156">Create a new Node.js project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="a75c4-156">Create a new Node.js project in your favorite IDE.</span></span>
2. <span data-ttu-id="a75c4-157">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="a75c4-157">Add the code provided below.</span></span>
3. <span data-ttu-id="a75c4-158">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="a75c4-158">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="a75c4-159">Run the program.</span><span class="sxs-lookup"><span data-stu-id="a75c4-159">Run the program.</span></span>

```nodejs
'use strict';

let fs = require ('fs');
let https = require ('https');

// **********************************************
// *** Update or verify the following values. ***
// **********************************************

// Replace this with a valid subscription key.
let subscriptionKey = 'ENTER KEY HERE';

// NOTE: Replace this with a valid knowledge base ID.
let kb = 'ENTER ID HERE';

let host = 'westus.api.cognitive.microsoft.com';
let service = '/qnamaker/v4.0';
let method = '/knowledgebases/';

let pretty_print = function (s) {
    return JSON.stringify(JSON.parse(s), null, 4);
}

// callback is the function to call when we have the entire response.
let response_handler = function (callback, response) {
    let body = '';
    response.on ('data', function (d) {
        body += d;
    });
    response.on ('end', function () {
// Call the callback function with the status code, headers, and body of the response.
        callback ({ status : response.statusCode, headers : response.headers, body : body });
    });
    response.on ('error', function (e) {
        console.log ('Error: ' + e.message);
    });
};

// Get an HTTP response handler that calls the specified callback function when we have the entire response.
let get_response_handler = function (callback) {
// Return a function that takes an HTTP response, and is closed over the specified callback.
// This function signature is required by https.request, hence the need for the closure.
    return function (response) {
        response_handler (callback, response);
    }
}

// callback is the function to call when we have the entire response from the PUT request.
let put = function (path, content, callback) {
    let request_params = {
        method : 'PUT',
        hostname : host,
        path : path,
        headers : {
            'Content-Type' : 'application/json',
            'Content-Length' : content.length,
            'Ocp-Apim-Subscription-Key' : subscriptionKey,
        }
    };

// Pass the callback function to the response handler.
    let req = https.request (request_params, get_response_handler (callback));
    req.write (content);
    req.end ();
}

// callback is the function to call when we have the response from the /knowledgebases PUT method.
let replace_kb = function (path, req, callback) {
    console.log ('Calling ' + host + path + '.');
// Send the PUT request.
    put (path, req, function (response) {
// Extract the data we want from the PUT response and pass it to the callback function.
        if (response.status == '204') {
            let result = {'result':'Success'};
            callback (JSON.stringify(result));
        }
        else {
            callback (response.body);
        }
    });
}

let req = {
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
};

var path = service + method + kb;
// Convert the request to a string.
let content = JSON.stringify(req);
replace_kb (path, content, function (result) {
    console.log (pretty_print(result));
});
```

<span data-ttu-id="a75c4-160">**Replace knowledge base response**</span><span class="sxs-lookup"><span data-stu-id="a75c4-160">**Replace knowledge base response**</span></span>

<span data-ttu-id="a75c4-161">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="a75c4-161">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json
{
    "result": "Success."
}
```

[<span data-ttu-id="a75c4-162">Back to top</span><span class="sxs-lookup"><span data-stu-id="a75c4-162">Back to top</span></span>](#HOLTop)

<a name="GetQnA"></a>

## <a name="download-the-contents-of-a-knowledge-base"></a><span data-ttu-id="a75c4-163">Download the contents of a knowledge base</span><span class="sxs-lookup"><span data-stu-id="a75c4-163">Download the contents of a knowledge base</span></span>

<span data-ttu-id="a75c4-164">The following code downloads the contents of the specified knowledge base, using the [Download knowledge base](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/knowledgebases_download) method.</span><span class="sxs-lookup"><span data-stu-id="a75c4-164">The following code downloads the contents of the specified knowledge base, using the [Download knowledge base](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/knowledgebases_download) method.</span></span>

1. <span data-ttu-id="a75c4-165">Create a new Node.js project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="a75c4-165">Create a new Node.js project in your favorite IDE.</span></span>
2. <span data-ttu-id="a75c4-166">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="a75c4-166">Add the code provided below.</span></span>
3. <span data-ttu-id="a75c4-167">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="a75c4-167">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="a75c4-168">Run the program.</span><span class="sxs-lookup"><span data-stu-id="a75c4-168">Run the program.</span></span>

```nodejs
'use strict';

let fs = require ('fs');
let https = require ('https');

// **********************************************
// *** Update or verify the following values. ***
// **********************************************

// Replace this with a valid subscription key.
let subscriptionKey = 'ENTER KEY HERE';

// NOTE: Replace this with a valid knowledge base ID.
let kb = 'ENTER ID HERE';

// NOTE: Replace this with "test" or "prod".
let env = "test";

let host = 'westus.api.cognitive.microsoft.com';
let service = '/qnamaker/v4.0';
let method = `/knowledgebases/${kb}/${env}/qna/`;

let pretty_print = function (s) {
    return JSON.stringify(JSON.parse(s), null, 4);
}

// callback is the function to call when we have the entire response.
let response_handler = function (callback, response) {
    let body = '';
    response.on ('data', function (d) {
        body += d;
    });
    response.on ('end', function () {
// Call the callback function with the status code, headers, and body of the response.
        callback ({ status : response.statusCode, headers : response.headers, body : body });
    });
    response.on ('error', function (e) {
        console.log ('Error: ' + e.message);
    });
};

// Get an HTTP response handler that calls the specified callback function when we have the entire response.
let get_response_handler = function (callback) {
// Return a function that takes an HTTP response, and is closed over the specified callback.
// This function signature is required by https.request, hence the need for the closure.
    return function (response) {
        response_handler (callback, response);
    }
}

// callback is the function to call when we have the entire response from the GET request.
let get = function (path, callback) {
    let request_params = {
        method : 'GET',
        hostname : host,
        path : path,
        headers : {
            'Ocp-Apim-Subscription-Key' : subscriptionKey,
        }
    };

// Pass the callback function to the response handler.
    let req = https.request (request_params, get_response_handler (callback));
    req.end ();
}

// callback is the function to call when we have the response from the /knowledgebases GET method.
let get_qna = function (path, callback) {
    console.log ('Calling ' + host + path + '.');
// Send the GET request.
    get (path, function (response) {
// Extract the data we want from the GET response and pass it to the callback function.
        callback ({ operation : response.headers.location, response : response.body });
    });
}

var path = service + method;
get_qna (path, function (result) {
    console.log (pretty_print(result.response));
});
```

<span data-ttu-id="a75c4-169">**Download knowledge base response**</span><span class="sxs-lookup"><span data-stu-id="a75c4-169">**Download knowledge base response**</span></span>

<span data-ttu-id="a75c4-170">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="a75c4-170">A successful response is returned in JSON, as shown in the following example:</span></span> 

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

[<span data-ttu-id="a75c4-171">Back to top</span><span class="sxs-lookup"><span data-stu-id="a75c4-171">Back to top</span></span>](#HOLTop)

<a name="GetAnswers"></a>

## <a name="get-answers-to-a-question-using-a-knowledge-base"></a><span data-ttu-id="a75c4-172">Get answers to a question using a knowledge base</span><span class="sxs-lookup"><span data-stu-id="a75c4-172">Get answers to a question using a knowledge base</span></span>

<span data-ttu-id="a75c4-173">The following code gets answers to a question using the specified knowledge base, using the **Generate answers** method.</span><span class="sxs-lookup"><span data-stu-id="a75c4-173">The following code gets answers to a question using the specified knowledge base, using the **Generate answers** method.</span></span>

1. <span data-ttu-id="a75c4-174">Create a new Node.js project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="a75c4-174">Create a new Node.js project in your favorite IDE.</span></span>
1. <span data-ttu-id="a75c4-175">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="a75c4-175">Add the code provided below.</span></span>
1. <span data-ttu-id="a75c4-176">Replace the `host` value with the Website name for your QnA Maker subscription.</span><span class="sxs-lookup"><span data-stu-id="a75c4-176">Replace the `host` value with the Website name for your QnA Maker subscription.</span></span> <span data-ttu-id="a75c4-177">For more information see [Create a QnA Maker service](../How-To/set-up-qnamaker-service-azure.md).</span><span class="sxs-lookup"><span data-stu-id="a75c4-177">For more information see [Create a QnA Maker service](../How-To/set-up-qnamaker-service-azure.md).</span></span>
1. <span data-ttu-id="a75c4-178">Replace the `endpoint_key` value with a valid endpoint key for your subscription.</span><span class="sxs-lookup"><span data-stu-id="a75c4-178">Replace the `endpoint_key` value with a valid endpoint key for your subscription.</span></span> <span data-ttu-id="a75c4-179">Note this is not the same as your subscription key.</span><span class="sxs-lookup"><span data-stu-id="a75c4-179">Note this is not the same as your subscription key.</span></span> <span data-ttu-id="a75c4-180">You can get your endpoint keys using the [Get endpoint keys](#GetKeys) method.</span><span class="sxs-lookup"><span data-stu-id="a75c4-180">You can get your endpoint keys using the [Get endpoint keys](#GetKeys) method.</span></span>
1. <span data-ttu-id="a75c4-181">Replace the `kb` value with the ID of the knowledge base you want to query for answers.</span><span class="sxs-lookup"><span data-stu-id="a75c4-181">Replace the `kb` value with the ID of the knowledge base you want to query for answers.</span></span> <span data-ttu-id="a75c4-182">Note this knowledge base must already have been published using the [Publish](#Publish) method.</span><span class="sxs-lookup"><span data-stu-id="a75c4-182">Note this knowledge base must already have been published using the [Publish](#Publish) method.</span></span>
1. <span data-ttu-id="a75c4-183">Run the program.</span><span class="sxs-lookup"><span data-stu-id="a75c4-183">Run the program.</span></span>

```nodejs
'use strict';

let fs = require ('fs');
let https = require ('https');

// **********************************************
// *** Update or verify the following values. ***
// **********************************************

// NOTE: Replace this with a valid host name.
let host = "ENTER HOST HERE";

// NOTE: Replace this with a valid endpoint key.
// This is not your subscription key.
// To get your endpoint keys, call the GET /endpointkeys method.
let endpoint_key = "ENTER KEY HERE";

// NOTE: Replace this with a valid knowledge base ID.
// Make sure you have published the knowledge base with the
// POST /knowledgebases/{knowledge base ID} method.
let kb = "ENTER KB ID HERE";

let method = "/qnamaker/knowledgebases/" + kb + "/generateAnswer";

let question = {
    'question': 'Is the QnA Maker Service free?',
    'top': 3
};

let pretty_print = function (s) {
    return JSON.stringify(JSON.parse(s), null, 4);
}

// callback is the function to call when we have the entire response.
let response_handler = function (callback, response) {
    let body = '';
    response.on ('data', function (d) {
        body += d;
    });
    response.on ('end', function () {
// Call the callback function with the status code, headers, and body of the response.
        callback ({ status : response.statusCode, headers : response.headers, body : body });
    });
    response.on ('error', function (e) {
        console.log ('Error: ' + e.message);
    });
};

// Get an HTTP response handler that calls the specified callback function when we have the entire response.
let get_response_handler = function (callback) {
// Return a function that takes an HTTP response, and is closed over the specified callback.
// This function signature is required by https.request, hence the need for the closure.
    return function (response) {
        response_handler (callback, response);
    }
}

// callback is the function to call when we have the entire response from the POST request.
let post = function (path, content, callback) {
    let request_params = {
        method : 'POST',
        hostname : host,
        path : path,
        headers : {
            'Content-Type' : 'application/json',
            'Content-Length' : content.length,
            'Authorization' : 'EndpointKey ' + endpoint_key,
        }
    };

// Pass the callback function to the response handler.
    let req = https.request (request_params, get_response_handler (callback));
    req.write (content);
    req.end ();
}

// callback is the function to call when we have the response from the /knowledgebases POST method.
let get_answers = function (path, req, callback) {
    console.log ('Calling ' + host + path + '.');
// Send the POST request.
    post (path, req, function (response) {
        callback (response.body);
    });
}

// Convert the request to a string.
let content = JSON.stringify(question);
get_answers (method, content, function (result) {
// Write out the response from the /knowledgebases/create method.
    console.log (pretty_print(result));
});
```

<span data-ttu-id="a75c4-184">**Get answers response**</span><span class="sxs-lookup"><span data-stu-id="a75c4-184">**Get answers response**</span></span>

<span data-ttu-id="a75c4-185">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="a75c4-185">A successful response is returned in JSON, as shown in the following example:</span></span> 

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

[<span data-ttu-id="a75c4-186">Back to top</span><span class="sxs-lookup"><span data-stu-id="a75c4-186">Back to top</span></span>](#HOLTop)

<a name="GetKB"></a>

## <a name="get-information-about-a-knowledge-base"></a><span data-ttu-id="a75c4-187">Get information about a knowledge base</span><span class="sxs-lookup"><span data-stu-id="a75c4-187">Get information about a knowledge base</span></span>

<span data-ttu-id="a75c4-188">The following code gets information about the specified knowledge base, using the [Get knowledge base details](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/knowledgebases_getknowledgebasedetails) method.</span><span class="sxs-lookup"><span data-stu-id="a75c4-188">The following code gets information about the specified knowledge base, using the [Get knowledge base details](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/knowledgebases_getknowledgebasedetails) method.</span></span>

1. <span data-ttu-id="a75c4-189">Create a new Node.js project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="a75c4-189">Create a new Node.js project in your favorite IDE.</span></span>
2. <span data-ttu-id="a75c4-190">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="a75c4-190">Add the code provided below.</span></span>
3. <span data-ttu-id="a75c4-191">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="a75c4-191">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="a75c4-192">Run the program.</span><span class="sxs-lookup"><span data-stu-id="a75c4-192">Run the program.</span></span>

```nodejs
'use strict';

let fs = require ('fs');
let https = require ('https');

// **********************************************
// *** Update or verify the following values. ***
// **********************************************

// Replace this with a valid subscription key.
let subscriptionKey = 'ENTER KEY HERE';

// NOTE: Replace this with a valid knowledge base ID.
let kb = 'ENTER ID HERE';

let host = 'westus.api.cognitive.microsoft.com';
let service = '/qnamaker/v4.0';
let method = '/knowledgebases/';

let pretty_print = function (s) {
    return JSON.stringify(JSON.parse(s), null, 4);
}

// callback is the function to call when we have the entire response.
let response_handler = function (callback, response) {
    let body = '';
    response.on ('data', function (d) {
        body += d;
    });
    response.on ('end', function () {
// Call the callback function with the status code, headers, and body of the response.
        callback ({ status : response.statusCode, headers : response.headers, body : body });
    });
    response.on ('error', function (e) {
        console.log ('Error: ' + e.message);
    });
};

// Get an HTTP response handler that calls the specified callback function when we have the entire response.
let get_response_handler = function (callback) {
// Return a function that takes an HTTP response, and is closed over the specified callback.
// This function signature is required by https.request, hence the need for the closure.
    return function (response) {
        response_handler (callback, response);
    }
}

// callback is the function to call when we have the entire response from the GET request.
let get = function (path, callback) {
    let request_params = {
        method : 'GET',
        hostname : host,
        path : path,
        headers : {
            'Ocp-Apim-Subscription-Key' : subscriptionKey,
        }
    };

// Pass the callback function to the response handler.
    let req = https.request (request_params, get_response_handler (callback));
    req.end ();
}

// callback is the function to call when we have the response from the /knowledgebases GET method.
let get_kb = function (path, callback) {
    console.log ('Calling ' + host + path + '.');
// Send the GET request.
    get (path, function (response) {
// Extract the data we want from the GET response and pass it to the callback function.
        callback ({ operation : response.headers.location, response : response.body });
    });
}

var path = service + method + kb;
get_kb (path, function (result) {
    console.log (pretty_print(result.response));
});
```

<span data-ttu-id="a75c4-193">**Get knowledge base details response**</span><span class="sxs-lookup"><span data-stu-id="a75c4-193">**Get knowledge base details response**</span></span>

<span data-ttu-id="a75c4-194">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="a75c4-194">A successful response is returned in JSON, as shown in the following example:</span></span> 

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

[<span data-ttu-id="a75c4-195">Back to top</span><span class="sxs-lookup"><span data-stu-id="a75c4-195">Back to top</span></span>](#HOLTop)

<a name="GetKBsByUser"></a>

## <a name="get-all-knowledge-bases-for-a-user"></a><span data-ttu-id="a75c4-196">Get all knowledge bases for a user</span><span class="sxs-lookup"><span data-stu-id="a75c4-196">Get all knowledge bases for a user</span></span>

<span data-ttu-id="a75c4-197">The following code gets information about all knowledge bases for a specified user, using the [Get knowledge bases for user](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/knowledgebases_getknowledgebasesforuser) method.</span><span class="sxs-lookup"><span data-stu-id="a75c4-197">The following code gets information about all knowledge bases for a specified user, using the [Get knowledge bases for user](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/knowledgebases_getknowledgebasesforuser) method.</span></span>

1. <span data-ttu-id="a75c4-198">Create a new Node.js project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="a75c4-198">Create a new Node.js project in your favorite IDE.</span></span>
2. <span data-ttu-id="a75c4-199">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="a75c4-199">Add the code provided below.</span></span>
3. <span data-ttu-id="a75c4-200">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="a75c4-200">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="a75c4-201">Run the program.</span><span class="sxs-lookup"><span data-stu-id="a75c4-201">Run the program.</span></span>

```nodejs
'use strict';

let fs = require ('fs');
let https = require ('https');

// **********************************************
// *** Update or verify the following values. ***
// **********************************************

// Replace this with a valid subscription key.
let subscriptionKey = 'ENTER KEY HERE';

let host = 'westus.api.cognitive.microsoft.com';
let service = '/qnamaker/v4.0';
let method = '/knowledgebases/';

let pretty_print = function (s) {
    return JSON.stringify(JSON.parse(s), null, 4);
}

// callback is the function to call when we have the entire response.
let response_handler = function (callback, response) {
    let body = '';
    response.on ('data', function (d) {
        body += d;
    });
    response.on ('end', function () {
// Call the callback function with the status code, headers, and body of the response.
        callback ({ status : response.statusCode, headers : response.headers, body : body });
    });
    response.on ('error', function (e) {
        console.log ('Error: ' + e.message);
    });
};

// Get an HTTP response handler that calls the specified callback function when we have the entire response.
let get_response_handler = function (callback) {
// Return a function that takes an HTTP response, and is closed over the specified callback.
// This function signature is required by https.request, hence the need for the closure.
    return function (response) {
        response_handler (callback, response);
    }
}

// callback is the function to call when we have the entire response from the GET request.
let get = function (path, callback) {
    let request_params = {
        method : 'GET',
        hostname : host,
        path : path,
        headers : {
            'Ocp-Apim-Subscription-Key' : subscriptionKey,
        }
    };

// Pass the callback function to the response handler.
    let req = https.request (request_params, get_response_handler (callback));
    req.end ();
}

// callback is the function to call when we have the response from the /knowledgebases GET method.
let get_kbs = function (path, callback) {
    console.log ('Calling ' + host + path + '.');
// Send the GET request.
    get (path, function (response) {
// Extract the data we want from the GET response and pass it to the callback function.
        callback ({ operation : response.headers.location, response : response.body });
    });
}

var path = service + method;
get_kbs (path, function (result) {
    console.log (pretty_print(result.response));
});
```

<span data-ttu-id="a75c4-202">**Get knowledge bases for user response**</span><span class="sxs-lookup"><span data-stu-id="a75c4-202">**Get knowledge bases for user response**</span></span>

<span data-ttu-id="a75c4-203">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="a75c4-203">A successful response is returned in JSON, as shown in the following example:</span></span> 

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

[<span data-ttu-id="a75c4-204">Back to top</span><span class="sxs-lookup"><span data-stu-id="a75c4-204">Back to top</span></span>](#HOLTop)

<a name="Delete"></a>

## <a name="delete-a-knowledge-base"></a><span data-ttu-id="a75c4-205">Delete a knowledge base</span><span class="sxs-lookup"><span data-stu-id="a75c4-205">Delete a knowledge base</span></span>

<span data-ttu-id="a75c4-206">The following code deletes the specified knowledge base, using the [Delete knowledge base](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/knowledgebases_delete) method.</span><span class="sxs-lookup"><span data-stu-id="a75c4-206">The following code deletes the specified knowledge base, using the [Delete knowledge base](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/knowledgebases_delete) method.</span></span>

1. <span data-ttu-id="a75c4-207">Create a new Node.js project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="a75c4-207">Create a new Node.js project in your favorite IDE.</span></span>
2. <span data-ttu-id="a75c4-208">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="a75c4-208">Add the code provided below.</span></span>
3. <span data-ttu-id="a75c4-209">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="a75c4-209">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="a75c4-210">Run the program.</span><span class="sxs-lookup"><span data-stu-id="a75c4-210">Run the program.</span></span>

```nodejs
'use strict';

let fs = require ('fs');
let https = require ('https');

// **********************************************
// *** Update or verify the following values. ***
// **********************************************

// Replace this with a valid subscription key.
let subscriptionKey = 'ENTER KEY HERE';

// NOTE: Replace this with a valid knowledge base ID.
let kb = 'ENTER ID HERE';

let host = 'westus.api.cognitive.microsoft.com';
let service = '/qnamaker/v4.0';
let method = '/knowledgebases/';

let pretty_print = function (s) {
    return JSON.stringify(JSON.parse(s), null, 4);
}

// callback is the function to call when we have the entire response.
let response_handler = function (callback, response) {
    let body = '';
    response.on ('data', function (d) {
        body += d;
    });
    response.on ('end', function () {
// Call the callback function with the status code, headers, and body of the response.
        callback ({ status : response.statusCode, headers : response.headers, body : body });
    });
    response.on ('error', function (e) {
        console.log ('Error: ' + e.message);
    });
};

// Get an HTTP response handler that calls the specified callback function when we have the entire response.
let get_response_handler = function (callback) {
// Return a function that takes an HTTP response, and is closed over the specified callback.
// This function signature is required by https.request, hence the need for the closure.
    return function (response) {
        response_handler (callback, response);
    }
}

// callback is the function to call when we have the entire response from the DELETE request.
let http_delete = function (path, content, callback) {
    let request_params = {
        method : 'DELETE',
        hostname : host,
        path : path,
        headers : {
            'Content-Type' : 'application/json',
            'Content-Length' : content.length,
            'Ocp-Apim-Subscription-Key' : subscriptionKey,
        }
    };

// Pass the callback function to the response handler.
    let req = https.request (request_params, get_response_handler (callback));
    req.write (content);
    req.end ();
}

// callback is the function to call when we have the response from the /knowledgebases DELETE method.
let delete_kb = function (path, req, callback) {
    console.log ('Calling ' + host + path + '.');
// Send the DELETE request.
    http_delete (path, req, function (response) {
// Extract the data we want from the DELETE response and pass it to the callback function.
        if (response.status == '204') {
            let result = {'result':'Success'};
            callback (JSON.stringify(result));
        }
        else {
            callback (response.body);
        }
    });
}

var path = service + method + kb;
delete_kb (path, '', function (result) {
    console.log (pretty_print(result));
});
```

<span data-ttu-id="a75c4-211">**Delete knowledge base response**</span><span class="sxs-lookup"><span data-stu-id="a75c4-211">**Delete knowledge base response**</span></span>

<span data-ttu-id="a75c4-212">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="a75c4-212">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json
{
  "result": "Success."
}
```

[<span data-ttu-id="a75c4-213">Back to top</span><span class="sxs-lookup"><span data-stu-id="a75c4-213">Back to top</span></span>](#HOLTop)

<a name="GetKeys"></a>

## <a name="get-endpoint-keys"></a><span data-ttu-id="a75c4-214">Get endpoint keys</span><span class="sxs-lookup"><span data-stu-id="a75c4-214">Get endpoint keys</span></span>

<span data-ttu-id="a75c4-215">The following code gets the current endpoint keys, using the [Get endpoint keys](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/endpointkeys_getendpointkeys) method.</span><span class="sxs-lookup"><span data-stu-id="a75c4-215">The following code gets the current endpoint keys, using the [Get endpoint keys](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/endpointkeys_getendpointkeys) method.</span></span>

1. <span data-ttu-id="a75c4-216">Create a new Node.js project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="a75c4-216">Create a new Node.js project in your favorite IDE.</span></span>
2. <span data-ttu-id="a75c4-217">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="a75c4-217">Add the code provided below.</span></span>
3. <span data-ttu-id="a75c4-218">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="a75c4-218">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="a75c4-219">Run the program.</span><span class="sxs-lookup"><span data-stu-id="a75c4-219">Run the program.</span></span>

```nodejs
'use strict';

let fs = require ('fs');
let https = require ('https');

// **********************************************
// *** Update or verify the following values. ***
// **********************************************

// Replace this with a valid subscription key.
let subscriptionKey = 'ENTER KEY HERE';

let host = 'westus.api.cognitive.microsoft.com';
let service = '/qnamaker/v4.0';
let method = '/endpointkeys/';

let pretty_print = function (s) {
    return JSON.stringify(JSON.parse(s), null, 4);
}

// callback is the function to call when we have the entire response.
let response_handler = function (callback, response) {
    let body = '';
    response.on ('data', function (d) {
        body += d;
    });
    response.on ('end', function () {
// Call the callback function with the status code, headers, and body of the response.
        callback ({ status : response.statusCode, headers : response.headers, body : body });
    });
    response.on ('error', function (e) {
        console.log ('Error: ' + e.message);
    });
};

// Get an HTTP response handler that calls the specified callback function when we have the entire response.
let get_response_handler = function (callback) {
// Return a function that takes an HTTP response, and is closed over the specified callback.
// This function signature is required by https.request, hence the need for the closure.
    return function (response) {
        response_handler (callback, response);
    }
}

// callback is the function to call when we have the entire response from the GET request.
let get = function (path, callback) {
    let request_params = {
        method : 'GET',
        hostname : host,
        path : path,
        headers : {
            'Ocp-Apim-Subscription-Key' : subscriptionKey,
        }
    };

// Pass the callback function to the response handler.
    let req = https.request (request_params, get_response_handler (callback));
    req.end ();
}

// callback is the function to call when we have the response from the /knowledgebases GET method.
let get_keys = function (path, callback) {
    console.log ('Calling ' + host + path + '.');
// Send the GET request.
    get (path, function (response) {
// Extract the data we want from the GET response and pass it to the callback function.
        callback ({ operation : response.headers.location, response : response.body });
    });
}

var path = service + method;
get_keys (path, function (result) {
    console.log (pretty_print(result.response));
});
```

<span data-ttu-id="a75c4-220">**Get endpoint keys response**</span><span class="sxs-lookup"><span data-stu-id="a75c4-220">**Get endpoint keys response**</span></span>

<span data-ttu-id="a75c4-221">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="a75c4-221">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json
{
  "primaryEndpointKey": "ac110bdc-34b7-4b1c-b9cd-b05f9a6001f3",
  "secondaryEndpointKey": "1b4ed14e-614f-444a-9f3d-9347f45a9206"
}
```

[<span data-ttu-id="a75c4-222">Back to top</span><span class="sxs-lookup"><span data-stu-id="a75c4-222">Back to top</span></span>](#HOLTop)

<a name="PutKeys"></a>

## <a name="refresh-endpoint-keys"></a><span data-ttu-id="a75c4-223">Refresh endpoint keys</span><span class="sxs-lookup"><span data-stu-id="a75c4-223">Refresh endpoint keys</span></span>

<span data-ttu-id="a75c4-224">The following code regenerates the current endpoint keys, using the [Refresh endpoint keys](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/endpointkeys_refreshendpointkeys) method.</span><span class="sxs-lookup"><span data-stu-id="a75c4-224">The following code regenerates the current endpoint keys, using the [Refresh endpoint keys](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/endpointkeys_refreshendpointkeys) method.</span></span>

1. <span data-ttu-id="a75c4-225">Create a new Node.js project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="a75c4-225">Create a new Node.js project in your favorite IDE.</span></span>
2. <span data-ttu-id="a75c4-226">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="a75c4-226">Add the code provided below.</span></span>
3. <span data-ttu-id="a75c4-227">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="a75c4-227">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="a75c4-228">Run the program.</span><span class="sxs-lookup"><span data-stu-id="a75c4-228">Run the program.</span></span>

```nodejs
'use strict';

let fs = require ('fs');
let https = require ('https');

// **********************************************
// *** Update or verify the following values. ***
// **********************************************

// Replace this with a valid subscription key.
let subscriptionKey = 'ENTER KEY HERE';

// NOTE: Replace this with "PrimaryKey" or "SecondaryKey."
let key_type = "PrimaryKey";

let host = 'westus.api.cognitive.microsoft.com';
let service = '/qnamaker/v4.0';
let method = '/endpointkeys/';

let pretty_print = function (s) {
    return JSON.stringify(JSON.parse(s), null, 4);
}

// callback is the function to call when we have the entire response.
let response_handler = function (callback, response) {
    let body = '';
    response.on ('data', function (d) {
        body += d;
    });
    response.on ('end', function () {
// Call the callback function with the status code, headers, and body of the response.
        callback ({ status : response.statusCode, headers : response.headers, body : body });
    });
    response.on ('error', function (e) {
        console.log ('Error: ' + e.message);
    });
};

// Get an HTTP response handler that calls the specified callback function when we have the entire response.
let get_response_handler = function (callback) {
// Return a function that takes an HTTP response, and is closed over the specified callback.
// This function signature is required by https.request, hence the need for the closure.
    return function (response) {
        response_handler (callback, response);
    }
}

// callback is the function to call when we have the entire response from the PATCH request.
let patch = function (path, content, callback) {
    let request_params = {
        method : 'PATCH',
        hostname : host,
        path : path,
        headers : {
            'Content-Type' : 'application/json',
            'Content-Length' : content.length,
            'Ocp-Apim-Subscription-Key' : subscriptionKey,
        }
    };

// Pass the callback function to the response handler.
    let req = https.request (request_params, get_response_handler (callback));
    req.write (content);
    req.end ();
}

// callback is the function to call when we have the response from the /knowledgebases PATCH method.
let refresh_keys = function (path, req, callback) {
    console.log ('Calling ' + host + path + '.');
// Send the PATCH request.
    patch (path, req, function (response) {
// Extract the data we want from the PATCH response and pass it to the callback function.
        if (response.status == '204') {
            let result = {'result':'Success'};
            callback (JSON.stringify(result));
        }
        else {
            callback (response.body);
        }
    });
}

let req = {
  'wordAlterations': [
    {
      'alterations': [
        'botframework',
        'bot frame work'
      ]
    }
  ]
};

var path = service + method + key_type;
// Convert the request to a string.
let content = JSON.stringify(req);
refresh_keys (path, content, function (result) {
    console.log (pretty_print(result));
});
```

<span data-ttu-id="a75c4-229">**Refresh endpoint keys response**</span><span class="sxs-lookup"><span data-stu-id="a75c4-229">**Refresh endpoint keys response**</span></span>

<span data-ttu-id="a75c4-230">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="a75c4-230">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json
{
  "primaryEndpointKey": "ac110bdc-34b7-4b1c-b9cd-b05f9a6001f3",
  "secondaryEndpointKey": "1b4ed14e-614f-444a-9f3d-9347f45a9206"
}
```

[<span data-ttu-id="a75c4-231">Back to top</span><span class="sxs-lookup"><span data-stu-id="a75c4-231">Back to top</span></span>](#HOLTop)

<a name="GetAlterations"></a>

## <a name="get-word-alterations"></a><span data-ttu-id="a75c4-232">Get word alterations</span><span class="sxs-lookup"><span data-stu-id="a75c4-232">Get word alterations</span></span>

<span data-ttu-id="a75c4-233">The following code gets the current word alterations, using the [Download alterations](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da75fc) method.</span><span class="sxs-lookup"><span data-stu-id="a75c4-233">The following code gets the current word alterations, using the [Download alterations](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da75fc) method.</span></span>

1. <span data-ttu-id="a75c4-234">Create a new Node.js project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="a75c4-234">Create a new Node.js project in your favorite IDE.</span></span>
2. <span data-ttu-id="a75c4-235">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="a75c4-235">Add the code provided below.</span></span>
3. <span data-ttu-id="a75c4-236">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="a75c4-236">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="a75c4-237">Run the program.</span><span class="sxs-lookup"><span data-stu-id="a75c4-237">Run the program.</span></span>

```nodejs
'use strict';

let fs = require ('fs');
let https = require ('https');

// **********************************************
// *** Update or verify the following values. ***
// **********************************************

// Replace this with a valid subscription key.
let subscriptionKey = 'ENTER KEY HERE';

let host = 'westus.api.cognitive.microsoft.com';
let service = '/qnamaker/v4.0';
let method = '/alterations/';

let pretty_print = function (s) {
    return JSON.stringify(JSON.parse(s), null, 4);
}

// callback is the function to call when we have the entire response.
let response_handler = function (callback, response) {
    let body = '';
    response.on ('data', function (d) {
        body += d;
    });
    response.on ('end', function () {
// Call the callback function with the status code, headers, and body of the response.
        callback ({ status : response.statusCode, headers : response.headers, body : body });
    });
    response.on ('error', function (e) {
        console.log ('Error: ' + e.message);
    });
};

// Get an HTTP response handler that calls the specified callback function when we have the entire response.
let get_response_handler = function (callback) {
// Return a function that takes an HTTP response, and is closed over the specified callback.
// This function signature is required by https.request, hence the need for the closure.
    return function (response) {
        response_handler (callback, response);
    }
}

// callback is the function to call when we have the entire response from the GET request.
let get = function (path, callback) {
    let request_params = {
        method : 'GET',
        hostname : host,
        path : path,
        headers : {
            'Ocp-Apim-Subscription-Key' : subscriptionKey,
        }
    };

// Pass the callback function to the response handler.
    let req = https.request (request_params, get_response_handler (callback));
    req.end ();
}

// callback is the function to call when we have the response from the /knowledgebases GET method.
let get_alterations = function (path, callback) {
    console.log ('Calling ' + host + path + '.');
// Send the GET request.
    get (path, function (response) {
// Extract the data we want from the GET response and pass it to the callback function.
        callback ({ operation : response.headers.location, response : response.body });
    });
}

var path = service + method;
get_alterations (path, function (result) {
    console.log (pretty_print(result.response));
});
```

<span data-ttu-id="a75c4-238">**Get word alterations response**</span><span class="sxs-lookup"><span data-stu-id="a75c4-238">**Get word alterations response**</span></span>

<span data-ttu-id="a75c4-239">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="a75c4-239">A successful response is returned in JSON, as shown in the following example:</span></span> 

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

[<span data-ttu-id="a75c4-240">Back to top</span><span class="sxs-lookup"><span data-stu-id="a75c4-240">Back to top</span></span>](#HOLTop)

<a name="PutAlterations"></a>

## <a name="replace-word-alterations"></a><span data-ttu-id="a75c4-241">Replace word alterations</span><span class="sxs-lookup"><span data-stu-id="a75c4-241">Replace word alterations</span></span>

<span data-ttu-id="a75c4-242">The following code replaces the current word alterations, using the [Replace alterations](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da75fd) method.</span><span class="sxs-lookup"><span data-stu-id="a75c4-242">The following code replaces the current word alterations, using the [Replace alterations](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da75fd) method.</span></span>

1. <span data-ttu-id="a75c4-243">Create a new Node.js project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="a75c4-243">Create a new Node.js project in your favorite IDE.</span></span>
2. <span data-ttu-id="a75c4-244">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="a75c4-244">Add the code provided below.</span></span>
3. <span data-ttu-id="a75c4-245">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="a75c4-245">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="a75c4-246">Run the program.</span><span class="sxs-lookup"><span data-stu-id="a75c4-246">Run the program.</span></span>

```nodejs
'use strict';

let fs = require ('fs');
let https = require ('https');

// **********************************************
// *** Update or verify the following values. ***
// **********************************************

// Replace this with a valid subscription key.
let subscriptionKey = 'ENTER KEY HERE';

let host = 'westus.api.cognitive.microsoft.com';
let service = '/qnamaker/v4.0';
let method = '/alterations/';

let pretty_print = function (s) {
    return JSON.stringify(JSON.parse(s), null, 4);
}

// callback is the function to call when we have the entire response.
let response_handler = function (callback, response) {
    let body = '';
    response.on ('data', function (d) {
        body += d;
    });
    response.on ('end', function () {
// Call the callback function with the status code, headers, and body of the response.
        callback ({ status : response.statusCode, headers : response.headers, body : body });
    });
    response.on ('error', function (e) {
        console.log ('Error: ' + e.message);
    });
};

// Get an HTTP response handler that calls the specified callback function when we have the entire response.
let get_response_handler = function (callback) {
// Return a function that takes an HTTP response, and is closed over the specified callback.
// This function signature is required by https.request, hence the need for the closure.
    return function (response) {
        response_handler (callback, response);
    }
}

// callback is the function to call when we have the entire response from the PUT request.
let put = function (path, content, callback) {
    let request_params = {
        method : 'PUT',
        hostname : host,
        path : path,
        headers : {
            'Content-Type' : 'application/json',
            'Content-Length' : content.length,
            'Ocp-Apim-Subscription-Key' : subscriptionKey,
        }
    };

// Pass the callback function to the response handler.
    let req = https.request (request_params, get_response_handler (callback));
    req.write (content);
    req.end ();
}

// callback is the function to call when we have the response from the /knowledgebases PUT method.
let put_alterations = function (path, req, callback) {
    console.log ('Calling ' + host + path + '.');
// Send the PUT request.
    put (path, req, function (response) {
// Extract the data we want from the PUT response and pass it to the callback function.
        if (response.status == '204') {
            let result = {'result':'Success'};
            callback (JSON.stringify(result));
        }
        else {
            callback (response.body);
        }
    });
}

let req = {
  'wordAlterations': [
    {
      'alterations': [
        'botframework',
        'bot frame work'
      ]
    }
  ]
};

var path = service + method;
// Convert the request to a string.
let content = JSON.stringify(req);
put_alterations (path, content, function (result) {
    console.log (pretty_print(result));
});
```

<span data-ttu-id="a75c4-247">**Replace word alterations response**</span><span class="sxs-lookup"><span data-stu-id="a75c4-247">**Replace word alterations response**</span></span>

<span data-ttu-id="a75c4-248">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="a75c4-248">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json
{
  "result": "Success."
}
```

[<span data-ttu-id="a75c4-249">Back to top</span><span class="sxs-lookup"><span data-stu-id="a75c4-249">Back to top</span></span>](#HOLTop)

## <a name="next-steps"></a><span data-ttu-id="a75c4-250">Next steps</span><span class="sxs-lookup"><span data-stu-id="a75c4-250">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a75c4-251">QnA Maker (V4) REST API Reference</span><span class="sxs-lookup"><span data-stu-id="a75c4-251">QnA Maker (V4) REST API Reference</span></span>](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da75ff)

## <a name="see-also"></a><span data-ttu-id="a75c4-252">See also</span><span class="sxs-lookup"><span data-stu-id="a75c4-252">See also</span></span> 

[<span data-ttu-id="a75c4-253">QnA Maker overview</span><span class="sxs-lookup"><span data-stu-id="a75c4-253">QnA Maker overview</span></span>](../Overview/overview.md)
