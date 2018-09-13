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
# <a name="url-preview-node-quickstart"></a>URL Preview Node quickstart

The following Node example creates a Url Preview for the SwiftKey Web site: https://swiftkey.com/en.

## <a name="prerequisites"></a>Prerequisites

Get an access key for the free trial [Cognitive Services Labs](https://aka.ms/answersearchsubscription)

## <a name="code-scenario"></a>Code scenario 

The following code gets URL Preview data.
It is implemented in the following steps:
1. Declare variables to specify the endpoint by host and path.
2. Specify the query URL to preview, and add the query parameter.  
3. Create a handler function for the response.
4. Define the Search function that creates the request and adds the *Ocp-Apim-Subscription-Key* header.
5. Run the Search function. 

The complete code for this demo follows:

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

## <a name="next-steps"></a>Next steps
- [C# example code](csharp.md)
- [Java quickstart](java-quickstart.md)
- [JavaScript quickstart](javascript.md)
- [Python quickstart](python-quickstart.md)