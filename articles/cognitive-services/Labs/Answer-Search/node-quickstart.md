---
title: Node quickstart for Microsoft Cognitive Services, Project Answer Search | Microsoft Docs
description: Get started using Project Answer Search, Microsoft Cognitive Services on Azure.
services: cognitive-services
author: mikedodaro
ms.service: cognitive-services
ms.technology: project-answer-search
ms.topic: article
ms.date: 04/13/2018
ms.author: rosh, v-gedod
ms.openlocfilehash: 36b2709d39230aae7929164ba4c9306f57043b43
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867213"
---
# <a name="project-answer-search-node-quickstart"></a><span data-ttu-id="7f72e-103">Project Answer Search Node quickstart</span><span class="sxs-lookup"><span data-stu-id="7f72e-103">Project Answer Search Node quickstart</span></span>

<span data-ttu-id="7f72e-104">The following Node example creates a query for information about Yosemite National Park.</span><span class="sxs-lookup"><span data-stu-id="7f72e-104">The following Node example creates a query for information about Yosemite National Park.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7f72e-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="7f72e-105">Prerequisites</span></span>

<span data-ttu-id="7f72e-106">Get an access key for the free trial [Cognitive Services Labs](https://aka.ms/answersearchsubscription)</span><span class="sxs-lookup"><span data-stu-id="7f72e-106">Get an access key for the free trial [Cognitive Services Labs](https://aka.ms/answersearchsubscription)</span></span>

<span data-ttu-id="7f72e-107">This example uses Node v8.9.4</span><span class="sxs-lookup"><span data-stu-id="7f72e-107">This example uses Node v8.9.4</span></span>

## <a name="code-scenario"></a><span data-ttu-id="7f72e-108">Code scenario</span><span class="sxs-lookup"><span data-stu-id="7f72e-108">Code scenario</span></span> 

<span data-ttu-id="7f72e-109">The following code gets answers.</span><span class="sxs-lookup"><span data-stu-id="7f72e-109">The following code gets answers.</span></span>
<span data-ttu-id="7f72e-110">It is implemented in the following steps:</span><span class="sxs-lookup"><span data-stu-id="7f72e-110">It is implemented in the following steps:</span></span>
1. <span data-ttu-id="7f72e-111">Declare variables to specify the endpoint by host and path.</span><span class="sxs-lookup"><span data-stu-id="7f72e-111">Declare variables to specify the endpoint by host and path.</span></span>
2. <span data-ttu-id="7f72e-112">Specify the query URL to preview, and add the query parameter.</span><span class="sxs-lookup"><span data-stu-id="7f72e-112">Specify the query URL to preview, and add the query parameter.</span></span>  
3. <span data-ttu-id="7f72e-113">Create a handler function for the response.</span><span class="sxs-lookup"><span data-stu-id="7f72e-113">Create a handler function for the response.</span></span>
4. <span data-ttu-id="7f72e-114">Define the Search function that creates the request and adds the *Ocp-Apim-Subscription-Key* header.</span><span class="sxs-lookup"><span data-stu-id="7f72e-114">Define the Search function that creates the request and adds the *Ocp-Apim-Subscription-Key* header.</span></span>
5. <span data-ttu-id="7f72e-115">Run the Search function.</span><span class="sxs-lookup"><span data-stu-id="7f72e-115">Run the Search function.</span></span> 

<span data-ttu-id="7f72e-116">The complete code for this demo follows:</span><span class="sxs-lookup"><span data-stu-id="7f72e-116">The complete code for this demo follows:</span></span>

````
'use strict';

let https = require('https');

// Replace the subscriptionKey string value with your valid subscription key.
let subscriptionKey = 'YOUR-SUBSCRIPTION-KEY'; 

let host = 'api.labs.cognitive.microsoft.com';
let path = '/answerSearch/v7.0/search';

let mkt = 'en-us';
let q = 'Yosemite National Park';

let params = '?q=' + encodeURI(q) + '&mkt=en-us';

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

## <a name="next-steps"></a><span data-ttu-id="7f72e-117">Next steps</span><span class="sxs-lookup"><span data-stu-id="7f72e-117">Next steps</span></span>
- [<span data-ttu-id="7f72e-118">C# example code</span><span class="sxs-lookup"><span data-stu-id="7f72e-118">C# example code</span></span>](c-sharp-quickstart.md)
- [<span data-ttu-id="7f72e-119">Java quickstart</span><span class="sxs-lookup"><span data-stu-id="7f72e-119">Java quickstart</span></span>](java-quickstart.md)
- [<span data-ttu-id="7f72e-120">Python quickstart</span><span class="sxs-lookup"><span data-stu-id="7f72e-120">Python quickstart</span></span>](python-quickstart.md)