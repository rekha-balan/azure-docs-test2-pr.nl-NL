---
title: include file
description: include file
services: service-bus-relay
author: clemensv
ms.service: service-bus-relay
ms.topic: include
ms.date: 05/02/2018
ms.author: clemensv
ms.custom: include file
ms.openlocfilehash: 04cb694f556d1b53344c0fd95947a258170c4f88
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855697"
---
### <a name="create-a-nodejs-application"></a><span data-ttu-id="217ba-103">Create a Node.js application</span><span class="sxs-lookup"><span data-stu-id="217ba-103">Create a Node.js application</span></span>

<span data-ttu-id="217ba-104">If you have disabled the "Requires Client Authorization" option when creating the Relay, you can send requests to the Hybrid Connections URL with any browser.</span><span class="sxs-lookup"><span data-stu-id="217ba-104">If you have disabled the "Requires Client Authorization" option when creating the Relay, you can send requests to the Hybrid Connections URL with any browser.</span></span> <span data-ttu-id="217ba-105">For accessing protected endpoints, you need to create and pass a token in the `ServiceBusAuthorization` header, which is shown here.</span><span class="sxs-lookup"><span data-stu-id="217ba-105">For accessing protected endpoints, you need to create and pass a token in the `ServiceBusAuthorization` header, which is shown here.</span></span>

<span data-ttu-id="217ba-106">To start, create a new JavaScript file called `sender.js`.</span><span class="sxs-lookup"><span data-stu-id="217ba-106">To start, create a new JavaScript file called `sender.js`.</span></span>

### <a name="add-the-relay-npm-package"></a><span data-ttu-id="217ba-107">Add the Relay NPM package</span><span class="sxs-lookup"><span data-stu-id="217ba-107">Add the Relay NPM package</span></span>

<span data-ttu-id="217ba-108">Run `npm install hyco-https` from a Node command prompt in your project folder.</span><span class="sxs-lookup"><span data-stu-id="217ba-108">Run `npm install hyco-https` from a Node command prompt in your project folder.</span></span> <span data-ttu-id="217ba-109">This package also imports the regular `https` package.</span><span class="sxs-lookup"><span data-stu-id="217ba-109">This package also imports the regular `https` package.</span></span> <span data-ttu-id="217ba-110">For the client-side, the key difference is that the package provides functions to construct Relay URIs and tokens.</span><span class="sxs-lookup"><span data-stu-id="217ba-110">For the client-side, the key difference is that the package provides functions to construct Relay URIs and tokens.</span></span>

### <a name="write-some-code-to-send-messages"></a><span data-ttu-id="217ba-111">Write some code to send messages</span><span class="sxs-lookup"><span data-stu-id="217ba-111">Write some code to send messages</span></span>

1. <span data-ttu-id="217ba-112">Add the following `constants` to the top of the `sender.js` file.</span><span class="sxs-lookup"><span data-stu-id="217ba-112">Add the following `constants` to the top of the `sender.js` file.</span></span>
   
    ```js
    const https = require('hyco-https');
    ```

2. <span data-ttu-id="217ba-113">Add the following constants to the `sender.js` file for the hybrid connection details.</span><span class="sxs-lookup"><span data-stu-id="217ba-113">Add the following constants to the `sender.js` file for the hybrid connection details.</span></span> <span data-ttu-id="217ba-114">Replace the placeholders in brackets with the values you obtained when you created the hybrid connection.</span><span class="sxs-lookup"><span data-stu-id="217ba-114">Replace the placeholders in brackets with the values you obtained when you created the hybrid connection.</span></span>
   
   1. <span data-ttu-id="217ba-115">`const ns` - The Relay namespace.</span><span class="sxs-lookup"><span data-stu-id="217ba-115">`const ns` - The Relay namespace.</span></span> <span data-ttu-id="217ba-116">Be sure to use the fully qualified namespace name; for example, `{namespace}.servicebus.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="217ba-116">Be sure to use the fully qualified namespace name; for example, `{namespace}.servicebus.windows.net`.</span></span>
   2. <span data-ttu-id="217ba-117">`const path` - The name of the hybrid connection.</span><span class="sxs-lookup"><span data-stu-id="217ba-117">`const path` - The name of the hybrid connection.</span></span>
   3. <span data-ttu-id="217ba-118">`const keyrule` - The name of the SAS key.</span><span class="sxs-lookup"><span data-stu-id="217ba-118">`const keyrule` - The name of the SAS key.</span></span>
   4. <span data-ttu-id="217ba-119">`const key` - The SAS key value.</span><span class="sxs-lookup"><span data-stu-id="217ba-119">`const key` - The SAS key value.</span></span>

3. <span data-ttu-id="217ba-120">Add the following code to the `sender.js` file.</span><span class="sxs-lookup"><span data-stu-id="217ba-120">Add the following code to the `sender.js` file.</span></span> <span data-ttu-id="217ba-121">You will notice that the code does not differ significantly from the regular use of the Node.js HTTPS client; it just adds the authorization header.</span><span class="sxs-lookup"><span data-stu-id="217ba-121">You will notice that the code does not differ significantly from the regular use of the Node.js HTTPS client; it just adds the authorization header.</span></span>
   
    ```js
   https.get({
        hostname : ns,
        path : (!path || path.length == 0 || path[0] !== '/'?'/':'') + path,
        port : 443,
        headers : {
            'ServiceBusAuthorization' : 
                https.createRelayToken(https.createRelayHttpsUri(ns, path), keyrule, key)
        }
    }, (res) => {
        let error;
        if (res.statusCode !== 200) {
            console.error('Request Failed.\n Status Code: ${statusCode}');
            res.resume();
        } 
        else {
            res.setEncoding('utf8');
            res.on('data', (chunk) => {
                console.log(`BODY: ${chunk}`);
            });
            res.on('end', () => {
                console.log('No more data in response.');
            });
        };
    }).on('error', (e) => {
        console.error(`Got error: ${e.message}`);
    });
    ```
    <span data-ttu-id="217ba-122">Here is what your sender.js file should look like:</span><span class="sxs-lookup"><span data-stu-id="217ba-122">Here is what your sender.js file should look like:</span></span>
   
    ```js
    const https = require('hyco-https');
       
    const ns = "{RelayNamespace}";
    const path = "{HybridConnectionName}";
    const keyrule = "{SASKeyName}";
    const key = "{SASKeyValue}";
   
    https.get({
        hostname : ns,
        path : (!path || path.length == 0 || path[0] !== '/'?'/':'') + path,
        port : 443,
        headers : {
            'ServiceBusAuthorization' : 
                https.createRelayToken(https.createRelayHttpsUri(ns, path), keyrule, key)
        }
    }, (res) => {
        let error;
        if (res.statusCode !== 200) {
            console.error('Request Failed.\n Status Code: ${statusCode}');
            res.resume();
        } 
        else {
            res.setEncoding('utf8');
            res.on('data', (chunk) => {
                console.log(`BODY: ${chunk}`);
            });
            res.on('end', () => {
                console.log('No more data in response.');
            });
        };
    }).on('error', (e) => {
        console.error(`Got error: ${e.message}`);
    });
    ```

