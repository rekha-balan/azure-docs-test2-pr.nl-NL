---
title: Overview of the Azure Relay Node APIs | Microsoft Docs
description: Relay Node API overview
services: service-bus-relay
documentationcenter: na
author: jtaubensee
manager: timlt
editor: ''
ms.assetid: b7d6e822-7c32-4cb5-a4b8-df7d009bdc85
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/23/2017
ms.author: jotaub
ms.openlocfilehash: 74e020992f5d841d9692dee2cb0bea97a9f27f8e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552258"
---
# <a name="relay-hybrid-connections-hyco-ws-node-api-overview"></a><span data-ttu-id="657a8-103">Relay Hybrid Connections hyco-ws Node API overview</span><span class="sxs-lookup"><span data-stu-id="657a8-103">Relay Hybrid Connections hyco-ws Node API overview</span></span>

## <a name="overview"></a><span data-ttu-id="657a8-104">Overview</span><span class="sxs-lookup"><span data-stu-id="657a8-104">Overview</span></span>

<span data-ttu-id="657a8-105">The [`hyco-ws`](https://www.npmjs.com/package/hyco-ws) Node package for Azure Relay Hybrid Connections is built on and extends the ['ws'](https://www.npmjs.com/package/ws) NPM package.</span><span class="sxs-lookup"><span data-stu-id="657a8-105">The [`hyco-ws`](https://www.npmjs.com/package/hyco-ws) Node package for Azure Relay Hybrid Connections is built on and extends the ['ws'](https://www.npmjs.com/package/ws) NPM package.</span></span> <span data-ttu-id="657a8-106">This package re-exports all exports of that base package and adds new exports that enable integration with the Azure Relay service Hybrid Connections feature.</span><span class="sxs-lookup"><span data-stu-id="657a8-106">This package re-exports all exports of that base package and adds new exports that enable integration with the Azure Relay service Hybrid Connections feature.</span></span> 

<span data-ttu-id="657a8-107">Existing applications that `require('ws')` can use this package with `require('hyco-ws')` instead, which also enables hybrid scenarios in which an application can listen for WebSocket connections locally from "inside the firewall" and via Hybrid Connections, all at the same time.</span><span class="sxs-lookup"><span data-stu-id="657a8-107">Existing applications that `require('ws')` can use this package with `require('hyco-ws')` instead, which also enables hybrid scenarios in which an application can listen for WebSocket connections locally from "inside the firewall" and via Hybrid Connections, all at the same time.</span></span>
  
## <a name="documentation"></a><span data-ttu-id="657a8-108">Documentation</span><span class="sxs-lookup"><span data-stu-id="657a8-108">Documentation</span></span>

<span data-ttu-id="657a8-109">The APIs are [documented in the main 'ws' package](https://github.com/websockets/ws/blob/master/doc/ws.md).</span><span class="sxs-lookup"><span data-stu-id="657a8-109">The APIs are [documented in the main 'ws' package](https://github.com/websockets/ws/blob/master/doc/ws.md).</span></span> <span data-ttu-id="657a8-110">This document describes how this package differs from that baseline.</span><span class="sxs-lookup"><span data-stu-id="657a8-110">This document describes how this package differs from that baseline.</span></span> 

<span data-ttu-id="657a8-111">The key differences between the base package and this 'hyco-ws' is that it adds a new server class, exported via `require('hyco-ws').RelayedServer`, and a few helper methods.</span><span class="sxs-lookup"><span data-stu-id="657a8-111">The key differences between the base package and this 'hyco-ws' is that it adds a new server class, exported via `require('hyco-ws').RelayedServer`, and a few helper methods.</span></span>

### <a name="package-helper-methods"></a><span data-ttu-id="657a8-112">Package Helper methods</span><span class="sxs-lookup"><span data-stu-id="657a8-112">Package Helper methods</span></span>

<span data-ttu-id="657a8-113">There are several utility methods available on the package export that you can reference as follows:</span><span class="sxs-lookup"><span data-stu-id="657a8-113">There are several utility methods available on the package export that you can reference as follows:</span></span>

``` JavaScript
const WebSocket = require('hyco-ws');

var listenUri = WebSocket.createRelayListenUri('namespace.servicebus.windows.net', 'path');
listenUri = WebSocket.appendRelayToken(listenUri, 'ruleName', '...key...')
...

```

<span data-ttu-id="657a8-114">The helper methods are for use with this package, but can also be used by a Node server for enabling web or device clients to create listeners or senders.</span><span class="sxs-lookup"><span data-stu-id="657a8-114">The helper methods are for use with this package, but can also be used by a Node server for enabling web or device clients to create listeners or senders.</span></span> <span data-ttu-id="657a8-115">The server uses these methods by passing them URIs that embed short-lived tokens.</span><span class="sxs-lookup"><span data-stu-id="657a8-115">The server uses these methods by passing them URIs that embed short-lived tokens.</span></span> <span data-ttu-id="657a8-116">These URIs can also be used with common WebSocket stacks that do not support setting HTTP headers for the WebSocket handshake.</span><span class="sxs-lookup"><span data-stu-id="657a8-116">These URIs can also be used with common WebSocket stacks that do not support setting HTTP headers for the WebSocket handshake.</span></span> <span data-ttu-id="657a8-117">Embedding authorization tokens into the URI is supported primarily for those library-external usage scenarios.</span><span class="sxs-lookup"><span data-stu-id="657a8-117">Embedding authorization tokens into the URI is supported primarily for those library-external usage scenarios.</span></span> 

#### <a name="createrelaylistenuri"></a><span data-ttu-id="657a8-118">createRelayListenUri</span><span class="sxs-lookup"><span data-stu-id="657a8-118">createRelayListenUri</span></span>
``` JavaScript
var uri = createRelayListenUri([namespaceName], [path], [[token]], [[id]])
```

<span data-ttu-id="657a8-119">Creates a valid Azure Relay Hybrid Connection listener URI for the given namespace and path.</span><span class="sxs-lookup"><span data-stu-id="657a8-119">Creates a valid Azure Relay Hybrid Connection listener URI for the given namespace and path.</span></span> <span data-ttu-id="657a8-120">This URI can then be used with the relay version of the WebSocketServer class.</span><span class="sxs-lookup"><span data-stu-id="657a8-120">This URI can then be used with the relay version of the WebSocketServer class.</span></span>

- <span data-ttu-id="657a8-121">**namespaceName** (required) - the domain-qualified name of the Azure Relay namespace to use</span><span class="sxs-lookup"><span data-stu-id="657a8-121">**namespaceName** (required) - the domain-qualified name of the Azure Relay namespace to use</span></span>
- <span data-ttu-id="657a8-122">**path** (required) - the name of an existing Azure Relay Hybrid Connection in that namespace</span><span class="sxs-lookup"><span data-stu-id="657a8-122">**path** (required) - the name of an existing Azure Relay Hybrid Connection in that namespace</span></span>
- <span data-ttu-id="657a8-123">**token** (optional) - a previously-issued Relay access token that is embedded in                        the listener URI (see the following example)</span><span class="sxs-lookup"><span data-stu-id="657a8-123">**token** (optional) - a previously-issued Relay access token that is embedded in                        the listener URI (see the following example)</span></span>
- <span data-ttu-id="657a8-124">**id** (optional) - a tracking identifier that enables end-to-end diagnostics tracking of requests</span><span class="sxs-lookup"><span data-stu-id="657a8-124">**id** (optional) - a tracking identifier that enables end-to-end diagnostics tracking of requests</span></span>

<span data-ttu-id="657a8-125">The **token** value is optional and should only be used when it is not possible to send HTTP headers along with the WebSocket handshake, as is the case with the W3C WebSocket stack.</span><span class="sxs-lookup"><span data-stu-id="657a8-125">The **token** value is optional and should only be used when it is not possible to send HTTP headers along with the WebSocket handshake, as is the case with the W3C WebSocket stack.</span></span>                  


#### <a name="createrelaysenduri"></a><span data-ttu-id="657a8-126">createRelaySendUri</span><span class="sxs-lookup"><span data-stu-id="657a8-126">createRelaySendUri</span></span> 
``` JavaScript
var uri = createRelaySendUri([namespaceName], [path], [[token]], [[id]])
```

<span data-ttu-id="657a8-127">Creates a valid Azure Relay Hybrid Connection send URI for the given namespace and path.</span><span class="sxs-lookup"><span data-stu-id="657a8-127">Creates a valid Azure Relay Hybrid Connection send URI for the given namespace and path.</span></span> <span data-ttu-id="657a8-128">This URI can be used with any WebSocket client.</span><span class="sxs-lookup"><span data-stu-id="657a8-128">This URI can be used with any WebSocket client.</span></span>

- <span data-ttu-id="657a8-129">**namespaceName** (required) - the domain-qualified name of the Azure Relay namespace to use</span><span class="sxs-lookup"><span data-stu-id="657a8-129">**namespaceName** (required) - the domain-qualified name of the Azure Relay namespace to use</span></span>
- <span data-ttu-id="657a8-130">**path** (required) - the name of an existing Azure Relay Hybrid Connection in that namespace</span><span class="sxs-lookup"><span data-stu-id="657a8-130">**path** (required) - the name of an existing Azure Relay Hybrid Connection in that namespace</span></span>
- <span data-ttu-id="657a8-131">**token** (optional) - a previously-issued Relay access token that is embedded in                        the send URI (see the following example)</span><span class="sxs-lookup"><span data-stu-id="657a8-131">**token** (optional) - a previously-issued Relay access token that is embedded in                        the send URI (see the following example)</span></span>
- <span data-ttu-id="657a8-132">**id** (optional) - a tracking identifier that enables end-to-end diagnostics tracking of requests</span><span class="sxs-lookup"><span data-stu-id="657a8-132">**id** (optional) - a tracking identifier that enables end-to-end diagnostics tracking of requests</span></span>

<span data-ttu-id="657a8-133">The **token** value is optional and should only be used when it is not possible to send HTTP headers along with the WebSocket handshake, as is the case with the W3C WebSocket stack.</span><span class="sxs-lookup"><span data-stu-id="657a8-133">The **token** value is optional and should only be used when it is not possible to send HTTP headers along with the WebSocket handshake, as is the case with the W3C WebSocket stack.</span></span>                   


#### <a name="createrelaytoken"></a><span data-ttu-id="657a8-134">createRelayToken</span><span class="sxs-lookup"><span data-stu-id="657a8-134">createRelayToken</span></span> 
``` JavaScript
var token = createRelayToken([uri], [ruleName], [key], [[expirationSeconds]])
```

<span data-ttu-id="657a8-135">Creates an Azure Relay Shared Access Signature (SAS) token for the given target URI, SAS rule, and SAS rule key that is valid for the given number of seconds or for an hour from the current instant if the expiry argunent is omitted.</span><span class="sxs-lookup"><span data-stu-id="657a8-135">Creates an Azure Relay Shared Access Signature (SAS) token for the given target URI, SAS rule, and SAS rule key that is valid for the given number of seconds or for an hour from the current instant if the expiry argunent is omitted.</span></span>

- <span data-ttu-id="657a8-136">**uri** (required) - the URI for which the token is to be issued.</span><span class="sxs-lookup"><span data-stu-id="657a8-136">**uri** (required) - the URI for which the token is to be issued.</span></span> <span data-ttu-id="657a8-137">The URI is normalized to use the HTTP scheme, and query string information will be stripped.</span><span class="sxs-lookup"><span data-stu-id="657a8-137">The URI is normalized to use the HTTP scheme, and query string information will be stripped.</span></span>
- <span data-ttu-id="657a8-138">**ruleName** (required) - SAS rule name for either the entity represented by the given URI, or                           for the namespace represented by the URI host portion.</span><span class="sxs-lookup"><span data-stu-id="657a8-138">**ruleName** (required) - SAS rule name for either the entity represented by the given URI, or                           for the namespace represented by the URI host portion.</span></span>
- <span data-ttu-id="657a8-139">**key** (required) - valid key for the SAS rule.</span><span class="sxs-lookup"><span data-stu-id="657a8-139">**key** (required) - valid key for the SAS rule.</span></span> 
- <span data-ttu-id="657a8-140">**expirationSeconds** (optional) - the number of seconds until the generated token should expire.</span><span class="sxs-lookup"><span data-stu-id="657a8-140">**expirationSeconds** (optional) - the number of seconds until the generated token should expire.</span></span> 
                            <span data-ttu-id="657a8-141">The default is 1 hour (3600) if not specified.</span><span class="sxs-lookup"><span data-stu-id="657a8-141">The default is 1 hour (3600) if not specified.</span></span>

<span data-ttu-id="657a8-142">The issued token confers the rights associated with the specified SAS rule for the given duration.</span><span class="sxs-lookup"><span data-stu-id="657a8-142">The issued token confers the rights associated with the specified SAS rule for the given duration.</span></span>

#### <a name="appendrelaytoken"></a><span data-ttu-id="657a8-143">appendRelayToken</span><span class="sxs-lookup"><span data-stu-id="657a8-143">appendRelayToken</span></span>
``` JavaScript
var uri = appendRelayToken([uri], [ruleName], [key], [[expirationSeconds]])
```

<span data-ttu-id="657a8-144">This method is functionally equivalent to the **createRelayToken** method documented previously, but returns the token correctly appended to the input URI.</span><span class="sxs-lookup"><span data-stu-id="657a8-144">This method is functionally equivalent to the **createRelayToken** method documented previously, but returns the token correctly appended to the input URI.</span></span>

### <a name="class-wsrelayedserver"></a><span data-ttu-id="657a8-145">Class ws.RelayedServer</span><span class="sxs-lookup"><span data-stu-id="657a8-145">Class ws.RelayedServer</span></span>

<span data-ttu-id="657a8-146">The `hycows.RelayedServer` class is an alternative to the `ws.Server` class that does not listen on the local network, but delegates listening to the Azure Relay service.</span><span class="sxs-lookup"><span data-stu-id="657a8-146">The `hycows.RelayedServer` class is an alternative to the `ws.Server` class that does not listen on the local network, but delegates listening to the Azure Relay service.</span></span>

<span data-ttu-id="657a8-147">The two classes are mostly contract compatible, meaning that an existing application using the `ws.Server` class can be changed to use the relayed version quite easily.</span><span class="sxs-lookup"><span data-stu-id="657a8-147">The two classes are mostly contract compatible, meaning that an existing application using the `ws.Server` class can be changed to use the relayed version quite easily.</span></span> <span data-ttu-id="657a8-148">The main differences are in the constructor and in the available options.</span><span class="sxs-lookup"><span data-stu-id="657a8-148">The main differences are in the constructor and in the available options.</span></span>

#### <a name="constructor"></a><span data-ttu-id="657a8-149">Constructor</span><span class="sxs-lookup"><span data-stu-id="657a8-149">Constructor</span></span>  

``` JavaScript 
var ws = require('hyco-ws');
var server = ws.RelayedServer;

var wss = new server(
    {
        server : ws.createRelayListenUri(ns, path),
        token: function() { return ws.createRelayToken('http://' + ns, keyrule, key); }
    });
```

<span data-ttu-id="657a8-150">The `RelayedServer` constructor supports a different set of arguments than the `Server`, because it is neither a standalone listener nor embeddable into an existing HTTP listener framework.</span><span class="sxs-lookup"><span data-stu-id="657a8-150">The `RelayedServer` constructor supports a different set of arguments than the `Server`, because it is neither a standalone listener nor embeddable into an existing HTTP listener framework.</span></span> <span data-ttu-id="657a8-151">There are also fewer options available since the WebSocket management is largely delegated to the Relay service.</span><span class="sxs-lookup"><span data-stu-id="657a8-151">There are also fewer options available since the WebSocket management is largely delegated to the Relay service.</span></span>

<span data-ttu-id="657a8-152">Constructor arguments:</span><span class="sxs-lookup"><span data-stu-id="657a8-152">Constructor arguments:</span></span>

- <span data-ttu-id="657a8-153">**server** (required) - the fully qualified URI for a Hybrid Connection name on which to listen, usually                         constructed with the WebSocket.createRelayListenUri() helper method.</span><span class="sxs-lookup"><span data-stu-id="657a8-153">**server** (required) - the fully qualified URI for a Hybrid Connection name on which to listen, usually                         constructed with the WebSocket.createRelayListenUri() helper method.</span></span>
- <span data-ttu-id="657a8-154">**token** (required) - this argument holds either a previously issued token string or a callback function that can be called to obtain such a token string.</span><span class="sxs-lookup"><span data-stu-id="657a8-154">**token** (required) - this argument holds either a previously issued token string or a callback function that can be called to obtain such a token string.</span></span> <span data-ttu-id="657a8-155">The callback option is preferred, as it enables token renewal.</span><span class="sxs-lookup"><span data-stu-id="657a8-155">The callback option is preferred, as it enables token renewal.</span></span>

#### <a name="events"></a><span data-ttu-id="657a8-156">Events</span><span class="sxs-lookup"><span data-stu-id="657a8-156">Events</span></span>

<span data-ttu-id="657a8-157">`RelayedServer` instances emit three events that enable you to handle incoming requests, establish connections, and detect error conditions.</span><span class="sxs-lookup"><span data-stu-id="657a8-157">`RelayedServer` instances emit three events that enable you to handle incoming requests, establish connections, and detect error conditions.</span></span> <span data-ttu-id="657a8-158">You must subscribe to the 'connect' event to handle messages.</span><span class="sxs-lookup"><span data-stu-id="657a8-158">You must subscribe to the 'connect' event to handle messages.</span></span> 

##### <a name="headers"></a><span data-ttu-id="657a8-159">headers</span><span class="sxs-lookup"><span data-stu-id="657a8-159">headers</span></span>
``` JavaScript 
function(headers)
```

<span data-ttu-id="657a8-160">The 'headers' event is raised just before an incoming connection is accepted, enabling modification of the headers to send to the client.</span><span class="sxs-lookup"><span data-stu-id="657a8-160">The 'headers' event is raised just before an incoming connection is accepted, enabling modification of the headers to send to the client.</span></span> 

##### <a name="connection"></a><span data-ttu-id="657a8-161">connection</span><span class="sxs-lookup"><span data-stu-id="657a8-161">connection</span></span>
``` JavaScript
function(socket)
```

<span data-ttu-id="657a8-162">Emitted when a new WebSocket connection is accepted.</span><span class="sxs-lookup"><span data-stu-id="657a8-162">Emitted when a new WebSocket connection is accepted.</span></span> <span data-ttu-id="657a8-163">The object is of type `ws.WebSocket`, same as with the base package.</span><span class="sxs-lookup"><span data-stu-id="657a8-163">The object is of type `ws.WebSocket`, same as with the base package.</span></span>


##### <a name="error"></a><span data-ttu-id="657a8-164">error</span><span class="sxs-lookup"><span data-stu-id="657a8-164">error</span></span>
``` JavaScript
function(error)
```

<span data-ttu-id="657a8-165">If the underlying server emits an error, it is forwarded here.</span><span class="sxs-lookup"><span data-stu-id="657a8-165">If the underlying server emits an error, it is forwarded here.</span></span>  

#### <a name="helpers"></a><span data-ttu-id="657a8-166">Helpers</span><span class="sxs-lookup"><span data-stu-id="657a8-166">Helpers</span></span>

<span data-ttu-id="657a8-167">To simplify starting a relayed server and immediately subscribing to incoming connections, the package exposes a simple helper function, which is also used in the samples, as follows:</span><span class="sxs-lookup"><span data-stu-id="657a8-167">To simplify starting a relayed server and immediately subscribing to incoming connections, the package exposes a simple helper function, which is also used in the samples, as follows:</span></span>

##### <a name="createrelayedlistener"></a><span data-ttu-id="657a8-168">createRelayedListener</span><span class="sxs-lookup"><span data-stu-id="657a8-168">createRelayedListener</span></span>

``` JavaScript
    var WebSocket = require('hyco-ws');

    var wss = WebSocket.createRelayedServer(
        {
            server : WebSocket.createRelayListenUri(ns, path),
            token: function() { return WebSocket.createRelayToken('http://' + ns, keyrule, key); }
        }, 
        function (ws) {
            console.log('connection accepted');
            ws.onmessage = function (event) {
                console.log(JSON.parse(event.data));
            };
            ws.on('close', function () {
                console.log('connection closed');
            });       
    });
``` 

<span data-ttu-id="657a8-169">var server = createRelayedServer([options], [connectCallback] )</span><span class="sxs-lookup"><span data-stu-id="657a8-169">var server = createRelayedServer([options], [connectCallback] )</span></span>

<span data-ttu-id="657a8-170">This method calls the constructor to create a new instance of the RelayedServer and then subscribes the provided callback to the 'connection' event.</span><span class="sxs-lookup"><span data-stu-id="657a8-170">This method calls the constructor to create a new instance of the RelayedServer and then subscribes the provided callback to the 'connection' event.</span></span>
 
##### <a name="relayedconnect"></a><span data-ttu-id="657a8-171">relayedConnect</span><span class="sxs-lookup"><span data-stu-id="657a8-171">relayedConnect</span></span>

<span data-ttu-id="657a8-172">Simply mirroring the `createRelayedServer` helper in function, `relayedConnect` creates a client connection and subscribes to the 'open' event on the resulting socket.</span><span class="sxs-lookup"><span data-stu-id="657a8-172">Simply mirroring the `createRelayedServer` helper in function, `relayedConnect` creates a client connection and subscribes to the 'open' event on the resulting socket.</span></span>

``` JavaScript
    var uri = WebSocket.createRelaySendUri(ns, path);
    WebSocket.relayedConnect(
        uri,
        WebSocket.createRelayToken(uri, keyrule, key),
        function (socket) {
            ...
        }
    );
```

## <a name="next-steps"></a><span data-ttu-id="657a8-173">Next steps</span><span class="sxs-lookup"><span data-stu-id="657a8-173">Next steps</span></span>
<span data-ttu-id="657a8-174">To learn more about Azure Relay, visit these links:</span><span class="sxs-lookup"><span data-stu-id="657a8-174">To learn more about Azure Relay, visit these links:</span></span>
* [<span data-ttu-id="657a8-175">What is Azure Relay?</span><span class="sxs-lookup"><span data-stu-id="657a8-175">What is Azure Relay?</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="657a8-176">Available Relay APIs</span><span class="sxs-lookup"><span data-stu-id="657a8-176">Available Relay APIs</span></span>](relay-api-overview.md)
