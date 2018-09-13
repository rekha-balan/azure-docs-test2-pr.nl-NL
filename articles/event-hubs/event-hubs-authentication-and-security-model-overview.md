---
title: Overview of Azure Event Hubs authentication and security model | Microsoft Docs
description: Event Hubs authentication and security model overview.
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: ''
ms.assetid: 93841e30-0c5c-4719-9dc1-57a4814342e7
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/29/2017
ms.author: sethm;clemensv
ms.openlocfilehash: 31bf24034558582eb138251207580e8f7fd7ddaf
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551292"
---
# <a name="event-hubs-authentication-and-security-model-overview"></a><span data-ttu-id="7fd9b-103">Event Hubs authentication and security model overview</span><span class="sxs-lookup"><span data-stu-id="7fd9b-103">Event Hubs authentication and security model overview</span></span>
<span data-ttu-id="7fd9b-104">The Azure Event Hubs security model meets the following requirements:</span><span class="sxs-lookup"><span data-stu-id="7fd9b-104">The Azure Event Hubs security model meets the following requirements:</span></span>

* <span data-ttu-id="7fd9b-105">Only clients that present valid credentials can send data to an event hub.</span><span class="sxs-lookup"><span data-stu-id="7fd9b-105">Only clients that present valid credentials can send data to an event hub.</span></span>
* <span data-ttu-id="7fd9b-106">A client cannot impersonate another client.</span><span class="sxs-lookup"><span data-stu-id="7fd9b-106">A client cannot impersonate another client.</span></span>
* <span data-ttu-id="7fd9b-107">A rogue client can be blocked from sending data to an event hub.</span><span class="sxs-lookup"><span data-stu-id="7fd9b-107">A rogue client can be blocked from sending data to an event hub.</span></span>

## <a name="client-authentication"></a><span data-ttu-id="7fd9b-108">Client authentication</span><span class="sxs-lookup"><span data-stu-id="7fd9b-108">Client authentication</span></span>
<span data-ttu-id="7fd9b-109">The Event Hubs security model is based on a combination of [Shared Access Signature (SAS)](../service-bus-messaging/service-bus-sas.md) tokens and *event publishers*.</span><span class="sxs-lookup"><span data-stu-id="7fd9b-109">The Event Hubs security model is based on a combination of [Shared Access Signature (SAS)](../service-bus-messaging/service-bus-sas.md) tokens and *event publishers*.</span></span> <span data-ttu-id="7fd9b-110">An event publisher defines a virtual endpoint for an event hub.</span><span class="sxs-lookup"><span data-stu-id="7fd9b-110">An event publisher defines a virtual endpoint for an event hub.</span></span> <span data-ttu-id="7fd9b-111">The publisher can only be used to send messages to an event hub.</span><span class="sxs-lookup"><span data-stu-id="7fd9b-111">The publisher can only be used to send messages to an event hub.</span></span> <span data-ttu-id="7fd9b-112">It is not possible to receive messages from a publisher.</span><span class="sxs-lookup"><span data-stu-id="7fd9b-112">It is not possible to receive messages from a publisher.</span></span>

<span data-ttu-id="7fd9b-113">Typically, an event hub employs one publisher per client.</span><span class="sxs-lookup"><span data-stu-id="7fd9b-113">Typically, an event hub employs one publisher per client.</span></span> <span data-ttu-id="7fd9b-114">All messages that are sent to any of the publishers of an event hub are enqueued within that event hub.</span><span class="sxs-lookup"><span data-stu-id="7fd9b-114">All messages that are sent to any of the publishers of an event hub are enqueued within that event hub.</span></span> <span data-ttu-id="7fd9b-115">Publishers enable fine-grained access control and throttling.</span><span class="sxs-lookup"><span data-stu-id="7fd9b-115">Publishers enable fine-grained access control and throttling.</span></span>

<span data-ttu-id="7fd9b-116">Each Event Hubs client is assigned a unique token, which is uploaded to the client.</span><span class="sxs-lookup"><span data-stu-id="7fd9b-116">Each Event Hubs client is assigned a unique token, which is uploaded to the client.</span></span> <span data-ttu-id="7fd9b-117">The tokens are produced such that each unique token grants access to a different unique publisher.</span><span class="sxs-lookup"><span data-stu-id="7fd9b-117">The tokens are produced such that each unique token grants access to a different unique publisher.</span></span> <span data-ttu-id="7fd9b-118">A client that possesses a token can only send to one publisher, but no other publisher.</span><span class="sxs-lookup"><span data-stu-id="7fd9b-118">A client that possesses a token can only send to one publisher, but no other publisher.</span></span> <span data-ttu-id="7fd9b-119">If multiple clients share the same token, then each of them shares a publisher.</span><span class="sxs-lookup"><span data-stu-id="7fd9b-119">If multiple clients share the same token, then each of them shares a publisher.</span></span>

<span data-ttu-id="7fd9b-120">Although not recommended, it is possible to equip devices with tokens that grant direct access to an event hub.</span><span class="sxs-lookup"><span data-stu-id="7fd9b-120">Although not recommended, it is possible to equip devices with tokens that grant direct access to an event hub.</span></span> <span data-ttu-id="7fd9b-121">Any device that holds this token can send messages directly into that event hub.</span><span class="sxs-lookup"><span data-stu-id="7fd9b-121">Any device that holds this token can send messages directly into that event hub.</span></span> <span data-ttu-id="7fd9b-122">Such a device will not be subject to throttling.</span><span class="sxs-lookup"><span data-stu-id="7fd9b-122">Such a device will not be subject to throttling.</span></span> <span data-ttu-id="7fd9b-123">Furthermore, the device cannot be blacklisted from sending to that event hub.</span><span class="sxs-lookup"><span data-stu-id="7fd9b-123">Furthermore, the device cannot be blacklisted from sending to that event hub.</span></span>

<span data-ttu-id="7fd9b-124">All tokens are signed with a SAS key.</span><span class="sxs-lookup"><span data-stu-id="7fd9b-124">All tokens are signed with a SAS key.</span></span> <span data-ttu-id="7fd9b-125">Typically, all tokens are signed with the same key.</span><span class="sxs-lookup"><span data-stu-id="7fd9b-125">Typically, all tokens are signed with the same key.</span></span> <span data-ttu-id="7fd9b-126">Clients are not aware of the key; this prevents other clients from manufacturing tokens.</span><span class="sxs-lookup"><span data-stu-id="7fd9b-126">Clients are not aware of the key; this prevents other clients from manufacturing tokens.</span></span>

### <a name="create-the-sas-key"></a><span data-ttu-id="7fd9b-127">Create the SAS key</span><span class="sxs-lookup"><span data-stu-id="7fd9b-127">Create the SAS key</span></span>
<span data-ttu-id="7fd9b-128">When creating an Azure Event Hubs namespace, the service generates a 256-bit SAS key named **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="7fd9b-128">When creating an Azure Event Hubs namespace, the service generates a 256-bit SAS key named **RootManageSharedAccessKey**.</span></span> <span data-ttu-id="7fd9b-129">This key grants send, listen, and manage rights to the namespace.</span><span class="sxs-lookup"><span data-stu-id="7fd9b-129">This key grants send, listen, and manage rights to the namespace.</span></span> <span data-ttu-id="7fd9b-130">You can create additional keys.</span><span class="sxs-lookup"><span data-stu-id="7fd9b-130">You can create additional keys.</span></span> <span data-ttu-id="7fd9b-131">It is recommended that you produce a key that grants send permissions to the specific event hub.</span><span class="sxs-lookup"><span data-stu-id="7fd9b-131">It is recommended that you produce a key that grants send permissions to the specific event hub.</span></span> <span data-ttu-id="7fd9b-132">For the remainder of this topic, it is assumed that you named this key **EventHubSendKey**.</span><span class="sxs-lookup"><span data-stu-id="7fd9b-132">For the remainder of this topic, it is assumed that you named this key **EventHubSendKey**.</span></span>

<span data-ttu-id="7fd9b-133">The following example creates a send-only key when creating the event hub:</span><span class="sxs-lookup"><span data-stu-id="7fd9b-133">The following example creates a send-only key when creating the event hub:</span></span>

```csharp
// Create namespace manager.
string serviceNamespace = "YOUR_NAMESPACE";
string namespaceManageKeyName = "RootManageSharedAccessKey";
string namespaceManageKey = "YOUR_ROOT_MANAGE_SHARED_ACCESS_KEY";
Uri uri = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, string.Empty);
TokenProvider td = TokenProvider.CreateSharedAccessSignatureTokenProvider(namespaceManageKeyName, namespaceManageKey);
NamespaceManager nm = new NamespaceManager(namespaceUri, namespaceManageTokenProvider);

// Create event hub with a SAS rule that enables sending to that event hub
EventHubDescription ed = new EventHubDescription("MY_EVENT_HUB") { PartitionCount = 32 };
string eventHubSendKeyName = "EventHubSendKey";
string eventHubSendKey = SharedAccessAuthorizationRule.GenerateRandomKey();
SharedAccessAuthorizationRule eventHubSendRule = new SharedAccessAuthorizationRule(eventHubSendKeyName, eventHubSendKey, new[] { AccessRights.Send });
ed.Authorization.Add(eventHubSendRule); 
nm.CreateEventHub(ed);
```

### <a name="generate-tokens"></a><span data-ttu-id="7fd9b-134">Generate tokens</span><span class="sxs-lookup"><span data-stu-id="7fd9b-134">Generate tokens</span></span>
<span data-ttu-id="7fd9b-135">You can generate tokens using the SAS key.</span><span class="sxs-lookup"><span data-stu-id="7fd9b-135">You can generate tokens using the SAS key.</span></span> <span data-ttu-id="7fd9b-136">You must produce only one token per client.</span><span class="sxs-lookup"><span data-stu-id="7fd9b-136">You must produce only one token per client.</span></span> <span data-ttu-id="7fd9b-137">Tokens can then be produced using the following method.</span><span class="sxs-lookup"><span data-stu-id="7fd9b-137">Tokens can then be produced using the following method.</span></span> <span data-ttu-id="7fd9b-138">All tokens are generated using the **EventHubSendKey** key.</span><span class="sxs-lookup"><span data-stu-id="7fd9b-138">All tokens are generated using the **EventHubSendKey** key.</span></span> <span data-ttu-id="7fd9b-139">Each token is assigned a unique URI.</span><span class="sxs-lookup"><span data-stu-id="7fd9b-139">Each token is assigned a unique URI.</span></span>

```csharp
public static string SharedAccessSignatureTokenProvider.GetSharedAccessSignature(string keyName, string sharedAccessKey, string resource, TimeSpan tokenTimeToLive)
```

<span data-ttu-id="7fd9b-140">When calling this method, the URI should be specified as `//<NAMESPACE>.servicebus.windows.net/<EVENT_HUB_NAME>/publishers/<PUBLISHER_NAME>`.</span><span class="sxs-lookup"><span data-stu-id="7fd9b-140">When calling this method, the URI should be specified as `//<NAMESPACE>.servicebus.windows.net/<EVENT_HUB_NAME>/publishers/<PUBLISHER_NAME>`.</span></span> <span data-ttu-id="7fd9b-141">For all tokens, the URI is identical, with the exception of `PUBLISHER_NAME`, which should be different for each token.</span><span class="sxs-lookup"><span data-stu-id="7fd9b-141">For all tokens, the URI is identical, with the exception of `PUBLISHER_NAME`, which should be different for each token.</span></span> <span data-ttu-id="7fd9b-142">Ideally, `PUBLISHER_NAME` represents the ID of the client that receives that token.</span><span class="sxs-lookup"><span data-stu-id="7fd9b-142">Ideally, `PUBLISHER_NAME` represents the ID of the client that receives that token.</span></span>

<span data-ttu-id="7fd9b-143">This method generates a token with the following structure:</span><span class="sxs-lookup"><span data-stu-id="7fd9b-143">This method generates a token with the following structure:</span></span>

```csharp
SharedAccessSignature sr={URI}&sig={HMAC_SHA256_SIGNATURE}&se={EXPIRATION_TIME}&skn={KEY_NAME}
```

<span data-ttu-id="7fd9b-144">The token expiration time is specified in seconds from Jan 1, 1970.</span><span class="sxs-lookup"><span data-stu-id="7fd9b-144">The token expiration time is specified in seconds from Jan 1, 1970.</span></span> <span data-ttu-id="7fd9b-145">The following is an example of a token:</span><span class="sxs-lookup"><span data-stu-id="7fd9b-145">The following is an example of a token:</span></span>

```csharp
SharedAccessSignature sr=contoso&sig=nPzdNN%2Gli0ifrfJwaK4mkK0RqAB%2byJUlt%2bGFmBHG77A%3d&se=1403130337&skn=RootManageSharedAccessKey
```

<span data-ttu-id="7fd9b-146">Typically, the tokens have a lifespan that resembles or exceeds the lifespan of the client.</span><span class="sxs-lookup"><span data-stu-id="7fd9b-146">Typically, the tokens have a lifespan that resembles or exceeds the lifespan of the client.</span></span> <span data-ttu-id="7fd9b-147">If the client has the capability to obtain a new token, tokens with a shorter lifespan can be used.</span><span class="sxs-lookup"><span data-stu-id="7fd9b-147">If the client has the capability to obtain a new token, tokens with a shorter lifespan can be used.</span></span>

### <a name="sending-data"></a><span data-ttu-id="7fd9b-148">Sending data</span><span class="sxs-lookup"><span data-stu-id="7fd9b-148">Sending data</span></span>
<span data-ttu-id="7fd9b-149">Once the tokens have been created, each client is provisioned with its own unique token.</span><span class="sxs-lookup"><span data-stu-id="7fd9b-149">Once the tokens have been created, each client is provisioned with its own unique token.</span></span>

<span data-ttu-id="7fd9b-150">When the client sends data into an event hub, it tags its token with the send request.</span><span class="sxs-lookup"><span data-stu-id="7fd9b-150">When the client sends data into an event hub, it tags its token with the send request.</span></span> <span data-ttu-id="7fd9b-151">To prevent an attacker from eavesdropping and stealing the token, the communication between the client and the event hub must occur over an encrypted channel.</span><span class="sxs-lookup"><span data-stu-id="7fd9b-151">To prevent an attacker from eavesdropping and stealing the token, the communication between the client and the event hub must occur over an encrypted channel.</span></span>

### <a name="blacklisting-clients"></a><span data-ttu-id="7fd9b-152">Blacklisting clients</span><span class="sxs-lookup"><span data-stu-id="7fd9b-152">Blacklisting clients</span></span>
<span data-ttu-id="7fd9b-153">If a token is stolen by an attacker, the attacker can impersonate the client whose token has been stolen.</span><span class="sxs-lookup"><span data-stu-id="7fd9b-153">If a token is stolen by an attacker, the attacker can impersonate the client whose token has been stolen.</span></span> <span data-ttu-id="7fd9b-154">Blacklisting a client renders that client unusable until it receives a new token that uses a different publisher.</span><span class="sxs-lookup"><span data-stu-id="7fd9b-154">Blacklisting a client renders that client unusable until it receives a new token that uses a different publisher.</span></span>

## <a name="authentication-of-back-end-applications"></a><span data-ttu-id="7fd9b-155">Authentication of back-end applications</span><span class="sxs-lookup"><span data-stu-id="7fd9b-155">Authentication of back-end applications</span></span>

<span data-ttu-id="7fd9b-156">To authenticate back-end applications that consume the data generated by Event Hubs clients, Event Hubs employs a security model that is similar to the model that is used for Service Bus topics.</span><span class="sxs-lookup"><span data-stu-id="7fd9b-156">To authenticate back-end applications that consume the data generated by Event Hubs clients, Event Hubs employs a security model that is similar to the model that is used for Service Bus topics.</span></span> <span data-ttu-id="7fd9b-157">An Event Hubs consumer group is equivalent to a subscription to a Service Bus topic.</span><span class="sxs-lookup"><span data-stu-id="7fd9b-157">An Event Hubs consumer group is equivalent to a subscription to a Service Bus topic.</span></span> <span data-ttu-id="7fd9b-158">A client can create a consumer group if the request to create the consumer group is accompanied by a token that grants manage privileges for the event hub,or for the namespace to which the event hub belongs.</span><span class="sxs-lookup"><span data-stu-id="7fd9b-158">A client can create a consumer group if the request to create the consumer group is accompanied by a token that grants manage privileges for the event hub,or for the namespace to which the event hub belongs.</span></span> <span data-ttu-id="7fd9b-159">A client is allowed to consume data from a consumer group if the receive request is accompanied by a token that grants receive rights on that consumer group, the event hub, or the namespace to which the event hub belongs.</span><span class="sxs-lookup"><span data-stu-id="7fd9b-159">A client is allowed to consume data from a consumer group if the receive request is accompanied by a token that grants receive rights on that consumer group, the event hub, or the namespace to which the event hub belongs.</span></span>


<span data-ttu-id="7fd9b-160">The current version of Service Bus does not support SAS rules for individual subscriptions.</span><span class="sxs-lookup"><span data-stu-id="7fd9b-160">The current version of Service Bus does not support SAS rules for individual subscriptions.</span></span> <span data-ttu-id="7fd9b-161">The same holds true for Event Hubs consumer groups.</span><span class="sxs-lookup"><span data-stu-id="7fd9b-161">The same holds true for Event Hubs consumer groups.</span></span> <span data-ttu-id="7fd9b-162">SAS support will be added for both features in the future.</span><span class="sxs-lookup"><span data-stu-id="7fd9b-162">SAS support will be added for both features in the future.</span></span>

<span data-ttu-id="7fd9b-163">In the absence of SAS authentication for individual consumer groups, you can use SAS keys to secure all consumer groups with a common key.</span><span class="sxs-lookup"><span data-stu-id="7fd9b-163">In the absence of SAS authentication for individual consumer groups, you can use SAS keys to secure all consumer groups with a common key.</span></span> <span data-ttu-id="7fd9b-164">This approach enables an application to consume data from any of the consumer groups of an event hub.</span><span class="sxs-lookup"><span data-stu-id="7fd9b-164">This approach enables an application to consume data from any of the consumer groups of an event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7fd9b-165">Next steps</span><span class="sxs-lookup"><span data-stu-id="7fd9b-165">Next steps</span></span>
<span data-ttu-id="7fd9b-166">To learn more about Event Hubs, visit the following topics:</span><span class="sxs-lookup"><span data-stu-id="7fd9b-166">To learn more about Event Hubs, visit the following topics:</span></span>

* <span data-ttu-id="7fd9b-167">[Event Hubs overview]</span><span class="sxs-lookup"><span data-stu-id="7fd9b-167">[Event Hubs overview]</span></span>
* <span data-ttu-id="7fd9b-168">[Overview of Shared Access Signatures]</span><span class="sxs-lookup"><span data-stu-id="7fd9b-168">[Overview of Shared Access Signatures]</span></span>
* <span data-ttu-id="7fd9b-169">[Sample applications that use Event Hubs]</span><span class="sxs-lookup"><span data-stu-id="7fd9b-169">[Sample applications that use Event Hubs]</span></span>

[Event Hubs overview]: event-hubs-what-is-event-hubs.md
[Sample applications that use Event Hubs]: https://github.com/Azure/azure-event-hubs/tree/master/samples
[Overview of Shared Access Signatures]: ../service-bus-messaging/service-bus-sas.md

