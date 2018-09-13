---
title: Get started with Azure Relay Hybrid Connections in Node | Microsoft Docs
description: How to write a Node console application for Hybrid Connections
services: service-bus-relay
documentationcenter: node
author: jtaubensee
manager: timlt
editor: ''
ms.assetid: e44e4867-3cf3-46be-8f8a-7671e2013bc4
ms.service: service-bus-relay
ms.devlang: tbd
ms.topic: get-started-article
ms.tgt_pltfrm: node
ms.workload: na
ms.date: 02/13/2017
ms.author: jotaub;sethm
ms.openlocfilehash: ebeed8fafdf0d77d7a8dea15fbcfadd02074738e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540671"
---
# <a name="get-started-with-relay-hybrid-connections"></a>Get started with Relay Hybrid Connections
[!INCLUDE [relay-selector-hybrid-connections](../../includes/relay-selector-hybrid-connections.md)]

## <a name="what-will-be-accomplished"></a>What will be accomplished
Since Hybrid Connections requires both a client and a server component, we will create two console applications in this tutorial. Here are the steps:

1. Create a Relay namespace, using the Azure portal.
2. Create a Hybrid Connection, using the Azure portal.
3. Write a server console application to receive messages.
4. Write a client console application to send messages.

## <a name="prerequisites"></a>Prerequisites
1. [Node.js](https://nodejs.org/en/) (This sample uses Node 7.0).
2. An Azure subscription.

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-the-azure-portal"></a>1. Create a namespace using the Azure portal
If you already have a Relay namespace created, jump to the [Create a Hybrid Connection using the Azure portal](#2-create-a-hybrid-connection-using-the-azure-portal) section.

[!INCLUDE [relay-create-namespace-portal](../../includes/relay-create-namespace-portal.md)]

## <a name="2-create-a-hybrid-connection-using-the-azure-portal"></a>2. Create a Hybrid Connection using the Azure portal
If you already have a Hybrid Connection created, jump to the [Create a server application](#3-create-a-server-application-listener) section.

[!INCLUDE [relay-create-hybrid-connection-portal](../../includes/relay-create-hybrid-connection-portal.md)]

## <a name="3-create-a-server-application-listener"></a>3. Create a server application (listener)
To listen and receive messages from the Relay, we will write a Node.js console application.

[!INCLUDE [relay-hybrid-connections-dotnet-get-started-server](../../includes/relay-hybrid-connections-node-get-started-server.md)]

## <a name="4-create-a-client-application-sender"></a>4. Create a client application (sender)
To send messages to the Relay, we will write a Node.js console application.

[!INCLUDE [relay-hybrid-connections-dotnet-get-started-client](../../includes/relay-hybrid-connections-node-get-started-client.md)]

## <a name="5-run-the-applications"></a>5. Run the applications
1. Run the server application.
2. Run the client application and enter some text.
3. Ensure that the server application console outputs the text that was entered in the client application.

![running-applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-bus-relay/media/relay-hybrid-connections-node-get-started/running-applications.png)

Congratulations, you have created an end-to-end Hybrid Connections application.

## <a name="next-steps"></a>Next steps:
* [Relay FAQ](relay-faq.md)
* [Create a namespace](relay-create-namespace-portal.md)
* [Get started with .NET](relay-hybrid-connections-dotnet-get-started.md)
* [Get started with Node](relay-hybrid-connections-node-get-started.md)


