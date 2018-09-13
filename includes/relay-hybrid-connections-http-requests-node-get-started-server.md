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
ms.openlocfilehash: d0fd3e88bdb25fdfd430924ef6b7f571d070b733
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855740"
---
### <a name="create-a-nodejs-application"></a><span data-ttu-id="6b1a9-103">Create a Node.js application</span><span class="sxs-lookup"><span data-stu-id="6b1a9-103">Create a Node.js application</span></span>

<span data-ttu-id="6b1a9-104">Create a new JavaScript file called `listener.js`.</span><span class="sxs-lookup"><span data-stu-id="6b1a9-104">Create a new JavaScript file called `listener.js`.</span></span>

### <a name="add-the-relay-npm-package"></a><span data-ttu-id="6b1a9-105">Add the Relay NPM package</span><span class="sxs-lookup"><span data-stu-id="6b1a9-105">Add the Relay NPM package</span></span>

<span data-ttu-id="6b1a9-106">Run `npm install hyco-https` from a Node command prompt in your project folder.</span><span class="sxs-lookup"><span data-stu-id="6b1a9-106">Run `npm install hyco-https` from a Node command prompt in your project folder.</span></span>

### <a name="write-some-code-to-handle-requests"></a><span data-ttu-id="6b1a9-107">Write some code to handle requests</span><span class="sxs-lookup"><span data-stu-id="6b1a9-107">Write some code to handle requests</span></span>

1. <span data-ttu-id="6b1a9-108">Add the following constant to the top of the `listener.js` file.</span><span class="sxs-lookup"><span data-stu-id="6b1a9-108">Add the following constant to the top of the `listener.js` file.</span></span>

    ```js
    const https = require('hyco-https');
    ```
2. <span data-ttu-id="6b1a9-109">Add the following constants to the `listener.js` file for the hybrid connection details.</span><span class="sxs-lookup"><span data-stu-id="6b1a9-109">Add the following constants to the `listener.js` file for the hybrid connection details.</span></span> <span data-ttu-id="6b1a9-110">Replace the placeholders in brackets with the values you obtained when you created the hybrid connection.</span><span class="sxs-lookup"><span data-stu-id="6b1a9-110">Replace the placeholders in brackets with the values you obtained when you created the hybrid connection.</span></span>

   1. <span data-ttu-id="6b1a9-111">`const ns` - The Relay namespace.</span><span class="sxs-lookup"><span data-stu-id="6b1a9-111">`const ns` - The Relay namespace.</span></span> <span data-ttu-id="6b1a9-112">Be sure to use the fully qualified namespace name; for example, `{namespace}.servicebus.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="6b1a9-112">Be sure to use the fully qualified namespace name; for example, `{namespace}.servicebus.windows.net`.</span></span>
   2. <span data-ttu-id="6b1a9-113">`const path` - The name of the hybrid connection.</span><span class="sxs-lookup"><span data-stu-id="6b1a9-113">`const path` - The name of the hybrid connection.</span></span>
   3. <span data-ttu-id="6b1a9-114">`const keyrule` - The name of the SAS key.</span><span class="sxs-lookup"><span data-stu-id="6b1a9-114">`const keyrule` - The name of the SAS key.</span></span>
   4. <span data-ttu-id="6b1a9-115">`const key` - The SAS key value.</span><span class="sxs-lookup"><span data-stu-id="6b1a9-115">`const key` - The SAS key value.</span></span>

3. <span data-ttu-id="6b1a9-116">Add the following code to the `listener.js` file.</span><span class="sxs-lookup"><span data-stu-id="6b1a9-116">Add the following code to the `listener.js` file.</span></span> <span data-ttu-id="6b1a9-117">:</span><span class="sxs-lookup"><span data-stu-id="6b1a9-117">:</span></span>

    <span data-ttu-id="6b1a9-118">You will notice that the code is not much different from any simple HTTP server  example you can find in Node.js beginner tutorials, which the exception of  using the `createRelayedServer` instead of the typical `createServer` function.</span><span class="sxs-lookup"><span data-stu-id="6b1a9-118">You will notice that the code is not much different from any simple HTTP server  example you can find in Node.js beginner tutorials, which the exception of  using the `createRelayedServer` instead of the typical `createServer` function.</span></span>

    ```js
    var uri = https.createRelayListenUri(ns, path);
    var server = https.createRelayedServer(
        {
            server : uri,
            token : () => https.createRelayToken(uri, keyrule, key)
        },
        (req, res) => {
            console.log('request accepted: ' + req.method + ' on ' + req.url);
            res.setHeader('Content-Type', 'text/html');
            res.end('<html><head><title>Hey!</title></head><body>Relayed Node.js Server!</body></html>');
        });

    server.listen( (err) => {
            if (err) {
              return console.log('something bad happened', err)
            }
            console.log(`server is listening on ${port}`)
          });

    server.on('error', (err) => {
        console.log('error: ' + err);
    });
    ```
    <span data-ttu-id="6b1a9-119">Here is what your listener.js file should look like:</span><span class="sxs-lookup"><span data-stu-id="6b1a9-119">Here is what your listener.js file should look like:</span></span>
   
    ```js
    const https = require('hyco-https');
   
    const ns = "{RelayNamespace}";
    const path = "{HybridConnectionName}";
    const keyrule = "{SASKeyName}";
    const key = "{SASKeyValue}";
   
    var uri = https.createRelayListenUri(ns, path);
    var server = https.createRelayedServer(
        {
            server : uri,
            token : () => https.createRelayToken(uri, keyrule, key)
        },
        (req, res) => {
            console.log('request accepted: ' + req.method + ' on ' + req.url);
            res.setHeader('Content-Type', 'text/html');
            res.end('<html><head><title>Hey!</title></head><body>Relayed Node.js Server!</body></html>');
        });

    server.listen( (err) => {
            if (err) {
              return console.log('something bad happened', err)
            }
            console.log(`server is listening on ${port}`)
          });

    server.on('error', (err) => {
        console.log('error: ' + err);
    });
    ```

