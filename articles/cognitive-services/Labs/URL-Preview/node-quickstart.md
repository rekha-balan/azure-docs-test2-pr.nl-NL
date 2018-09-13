---
title: Node.js quickstart for Project URL Preview - Microsoft Cognitive Services | Microsoft Docs
description: Get started using the URL Preview in Microsoft Cognitive Services on Azure.
services: cognitive-services
author: mikedodaro
ms.service: cognitive-services
ms.technology: project-url-preview
ms.topic: article
ms.date: 03/16/2018
ms.author: rosh, v-gedod
ms.openlocfilehash: 195033d2740b11873baae095cec028dc8d19ce49
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866794"
---
# <a name="url-preview-node-quickstart"></a><span data-ttu-id="07003-103">URL Preview Node quickstart</span><span class="sxs-lookup"><span data-stu-id="07003-103">URL Preview Node quickstart</span></span>

<span data-ttu-id="07003-104">The following Node example creates a Url Preview for the SwiftKey Web site: https://swiftkey.com/en.</span><span class="sxs-lookup"><span data-stu-id="07003-104">The following Node example creates a Url Preview for the SwiftKey Web site: https://swiftkey.com/en.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="07003-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="07003-105">Prerequisites</span></span>

<span data-ttu-id="07003-106">Get an access key for the free trial [Cognitive Services Labs](https://aka.ms/answersearchsubscription)</span><span class="sxs-lookup"><span data-stu-id="07003-106">Get an access key for the free trial [Cognitive Services Labs](https://aka.ms/answersearchsubscription)</span></span>

## <a name="code-scenario"></a><span data-ttu-id="07003-107">Code scenario</span><span class="sxs-lookup"><span data-stu-id="07003-107">Code scenario</span></span> 

<span data-ttu-id="07003-108">The following code gets URL Preview data.</span><span class="sxs-lookup"><span data-stu-id="07003-108">The following code gets URL Preview data.</span></span>
<span data-ttu-id="07003-109">It is implemented in the following steps:</span><span class="sxs-lookup"><span data-stu-id="07003-109">It is implemented in the following steps:</span></span>
1. <span data-ttu-id="07003-110">Declare variables to specify the endpoint by host and path.</span><span class="sxs-lookup"><span data-stu-id="07003-110">Declare variables to specify the endpoint by host and path.</span></span>
2. <span data-ttu-id="07003-111">Specify the query URL to preview, and add the query parameter.</span><span class="sxs-lookup"><span data-stu-id="07003-111">Specify the query URL to preview, and add the query parameter.</span></span>  
3. <span data-ttu-id="07003-112">Create a handler function for the response.</span><span class="sxs-lookup"><span data-stu-id="07003-112">Create a handler function for the response.</span></span>
4. <span data-ttu-id="07003-113">Define the Search function that creates the request and adds the *Ocp-Apim-Subscription-Key* header.</span><span class="sxs-lookup"><span data-stu-id="07003-113">Define the Search function that creates the request and adds the *Ocp-Apim-Subscription-Key* header.</span></span>
5. <span data-ttu-id="07003-114">Run the Search function.</span><span class="sxs-lookup"><span data-stu-id="07003-114">Run the Search function.</span></span> 

<span data-ttu-id="07003-115">The complete code for this demo follows:</span><span class="sxs-lookup"><span data-stu-id="07003-115">The complete code for this demo follows:</span></span>

````
'use strict';

let https = require('https');

// Replace the subscriptionKey string value with your valid subscription key.
let subscriptionKey = 'YOUR-ACCESS-KEY'; 
let host = 'api.labs.cognitive.microsoft.com';
let path = '/urlpreview/v7.0/search';

let mkt = 'en-US';
let q = 'https://swiftkey.com/';

let params = '?q=' + encodeURI(q);

let response_handler = function (response) {
    let body = '';
    response.on('data', function (d) {
        body += d;
    });
    response.on('end', function () {
        let body_ = JSON.parse(body);
        let body__ = JSON.stringify(body_, null, '  ');
        console.log(body__);
    });
    response.on('error', function (e) {
        console.log('Error: ' + e.message);
    });
};

let Search = function () {
    let request_params = {
        method: 'GET',
        hostname: host,
        path: path + params,
        headers: {
            'Ocp-Apim-Subscription-Key': subscriptionKey,
        }
    };

    let req = https.request(request_params, response_handler);
    req.end();
}

Search();

````

## <a name="next-steps"></a><span data-ttu-id="07003-116">Next steps</span><span class="sxs-lookup"><span data-stu-id="07003-116">Next steps</span></span>
- [<span data-ttu-id="07003-117">C# example code</span><span class="sxs-lookup"><span data-stu-id="07003-117">C# example code</span></span>](csharp.md)
- [<span data-ttu-id="07003-118">Java quickstart</span><span class="sxs-lookup"><span data-stu-id="07003-118">Java quickstart</span></span>](java-quickstart.md)
- [<span data-ttu-id="07003-119">JavaScript quickstart</span><span class="sxs-lookup"><span data-stu-id="07003-119">JavaScript quickstart</span></span>](javascript.md)
- [<span data-ttu-id="07003-120">Python quickstart</span><span class="sxs-lookup"><span data-stu-id="07003-120">Python quickstart</span></span>](python-quickstart.md)