---
title: 'Quickstart: Node.js Publish Knowledge Base - Qna Maker'
titleSuffix: Azure Cognitive Services
description: How to publish a knowledge base in Node.js for QnA Maker.
services: cognitive-services
author: nitinme
manager: cgronlun
ms.service: cognitive-services
ms.technology: qna-maker
ms.topic: quickstart
ms.date: 06/18/2018
ms.author: nolachar
ms.openlocfilehash: 868c63481fe7190db56567bfcfde78f498a45dff
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865988"
---
# <a name="publish-a-knowledge-base-in-nodejs"></a><span data-ttu-id="993b0-103">Publish a knowledge base in Node.js</span><span class="sxs-lookup"><span data-stu-id="993b0-103">Publish a knowledge base in Node.js</span></span>

<span data-ttu-id="993b0-104">The following code publishes an existing knowledge base, using the [Publish](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da75fe) method.</span><span class="sxs-lookup"><span data-stu-id="993b0-104">The following code publishes an existing knowledge base, using the [Publish](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da75fe) method.</span></span>

<span data-ttu-id="993b0-105">If you don't have a knowledge base yet, you can create a sample one to use for this quickstart: [Create a new knowledge base](create-new-kb-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="993b0-105">If you don't have a knowledge base yet, you can create a sample one to use for this quickstart: [Create a new knowledge base](create-new-kb-nodejs.md).</span></span>

1. <span data-ttu-id="993b0-106">Create a new Node project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="993b0-106">Create a new Node project in your favorite IDE.</span></span>
1. <span data-ttu-id="993b0-107">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="993b0-107">Add the code provided below.</span></span>
1. <span data-ttu-id="993b0-108">Replace the `subscriptionKey` value with a valid subscription key.</span><span class="sxs-lookup"><span data-stu-id="993b0-108">Replace the `subscriptionKey` value with a valid subscription key.</span></span>
1. <span data-ttu-id="993b0-109">Replace the `kb` value with a valid knowledge base ID.</span><span class="sxs-lookup"><span data-stu-id="993b0-109">Replace the `kb` value with a valid knowledge base ID.</span></span> <span data-ttu-id="993b0-110">Find this value by going to one of your [QnA Maker knowledge bases](https://www.qnamaker.ai/Home/MyServices).</span><span class="sxs-lookup"><span data-stu-id="993b0-110">Find this value by going to one of your [QnA Maker knowledge bases](https://www.qnamaker.ai/Home/MyServices).</span></span> <span data-ttu-id="993b0-111">Select the knowledge base you want to publish.</span><span class="sxs-lookup"><span data-stu-id="993b0-111">Select the knowledge base you want to publish.</span></span> <span data-ttu-id="993b0-112">Once on that page, find the 'kdid=' in the URL as shown below.</span><span class="sxs-lookup"><span data-stu-id="993b0-112">Once on that page, find the 'kdid=' in the URL as shown below.</span></span> <span data-ttu-id="993b0-113">Use its value for your code sample.</span><span class="sxs-lookup"><span data-stu-id="993b0-113">Use its value for your code sample.</span></span>

    ![QnA Maker knowledge base ID](../media/qnamaker-quickstart-kb/qna-maker-id.png)
1. <span data-ttu-id="993b0-115">Run the program.</span><span class="sxs-lookup"><span data-stu-id="993b0-115">Run the program.</span></span>

``` Node.js
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

## <a name="understand-what-qna-maker-returns"></a><span data-ttu-id="993b0-116">Understand what QnA Maker returns</span><span class="sxs-lookup"><span data-stu-id="993b0-116">Understand what QnA Maker returns</span></span>

<span data-ttu-id="993b0-117">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="993b0-117">A successful response is returned in JSON, as shown in the following example:</span></span>

```json
{
  "result": "Success."
}
```

## <a name="next-steps"></a><span data-ttu-id="993b0-118">Next steps</span><span class="sxs-lookup"><span data-stu-id="993b0-118">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="993b0-119">QnA Maker (V4) REST API Reference</span><span class="sxs-lookup"><span data-stu-id="993b0-119">QnA Maker (V4) REST API Reference</span></span>](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da75ff)