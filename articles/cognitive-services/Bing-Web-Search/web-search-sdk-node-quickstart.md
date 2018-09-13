---
title: 'Quickstart: Use the Bing Web Search SDK for Node.js'
description: Learn to use the Bing Web Search SDK for Node.js.
services: cognitive-services
author: erhopf
manager: cgronlun
ms.service: cognitive-services
ms.component: bing-web-search
ms.topic: quickstart
ms.date: 08/16/2018
ms.author: erhopf
ms.openlocfilehash: 7c3003ab4ba40a9d0212e7c94b6dd3bfbc8f0ca2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869013"
---
# <a name="quickstart-use-the-bing-web-search-sdk-for-nodejs"></a>Quickstart: Use the Bing Web Search SDK for Node.js

The Bing Web Search SDK makes it easy to integrate Bing Web Search into your Node.js application. In this quickstart, you'll learn how to instantiate a client, send a request, and print the response.

Want to see the code right now? The [Bing Web Search SDK for Node.js samples](https://github.com/Azure-Samples/cognitive-services-node-sdk-samples) are available on GitHub.

[!INCLUDE [bing-web-search-quickstart-signup](../../../includes/bing-web-search-quickstart-signup.md)]

## <a name="prerequisites"></a>Prerequisites

Here are a few things that you'll need before running this quickstart:

* [Node.js 6](https://nodejs.org/en/download/) or later
* A subscription key  

## <a name="set-up-your-development-environment"></a>Set up your development environment

Let's start by setting up the development environment for our Node.js project.

1. Create a new directory for your project:

    ```console
    mkdir YOUR_PROJECT
    ```

2. Create a new package file:

    ```console
    cd YOUR_PROJECT
    npm init
    ```

3. Now, let's install some azure modules and add them to the `package.json`:

    ```console
    npm install --save azure-cognitiveservices-websearch
    npm install --save ms-rest-azure
    ```

## <a name="create-a-project-and-declare-required-modules"></a>Create a project and declare required modules

In the same directory as your `package.json`, create a new Node.js project using your favorite IDE or editor. For example: `sample.js`.

Next, copy this code into your project. It loads the modules installed in the previous section.

```javascript
const CognitiveServicesCredentials = require('ms-rest-azure').CognitiveServicesCredentials;
const WebSearchAPIClient = require('azure-cognitiveservices-websearch');
```

## <a name="instantiate-the-client"></a>Instantiate the client

This code instantiates a client and using the `azure-cognitiveservices-websearch` module. Make sure that you enter a valid subscription key for your Azure account before continuing.

```javascript
let credentials = new CognitiveServicesCredentials('YOUR-ACCESS-KEY');
let webSearchApiClient = new WebSearchAPIClient(credentials);
```

## <a name="make-a-request-and-print-the-results"></a>Make a request and print the results

Use the client to send a search query to Bing Web Search. If the response includes results for any of the items in the `properties` array, the `result.value` is printed to console.

```javascript
webSearchApiClient.web.search('seahawks').then((result) => {
    let properties = ["images", "webPages", "news", "videos"];
    for (let i = 0; i < properties.length; i++) {
        if (result[properties[i]]) {
            console.log(result[properties[i]].value);
        } else {
            console.log(`No ${properties[i]} data`);
        }
    }
}).catch((err) => {
    throw err;
})
```

## <a name="run-the-program"></a>Run the program

The final step is to run your program!

## <a name="clean-up-resources"></a>Clean up resources

When you're done with this project, make sure to remove your subscription key from the program's code.

## <a name="next-steps"></a>Next steps

> [!div class="nextstepaction"]
> [Cognitive Services Node.js SDK samples](https://github.com/Azure-Samples/cognitive-services-node-sdk-samples)

## <a name="see-also"></a>See also

* [Azure Node SDK reference](https://docs.microsoft.com/javascript/api/azure-cognitiveservices-websearch/)
