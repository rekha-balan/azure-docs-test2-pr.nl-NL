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
# <a name="get-started-with-relay-hybrid-connections"></a><span data-ttu-id="ab429-103">Get started with Relay Hybrid Connections</span><span class="sxs-lookup"><span data-stu-id="ab429-103">Get started with Relay Hybrid Connections</span></span>
[!INCLUDE [relay-selector-hybrid-connections](../../includes/relay-selector-hybrid-connections.md)]

## <a name="what-will-be-accomplished"></a><span data-ttu-id="ab429-104">What will be accomplished</span><span class="sxs-lookup"><span data-stu-id="ab429-104">What will be accomplished</span></span>
<span data-ttu-id="ab429-105">Since Hybrid Connections requires both a client and a server component, we will create two console applications in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="ab429-105">Since Hybrid Connections requires both a client and a server component, we will create two console applications in this tutorial.</span></span> <span data-ttu-id="ab429-106">Here are the steps:</span><span class="sxs-lookup"><span data-stu-id="ab429-106">Here are the steps:</span></span>

1. <span data-ttu-id="ab429-107">Create a Relay namespace, using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="ab429-107">Create a Relay namespace, using the Azure portal.</span></span>
2. <span data-ttu-id="ab429-108">Create a Hybrid Connection, using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="ab429-108">Create a Hybrid Connection, using the Azure portal.</span></span>
3. <span data-ttu-id="ab429-109">Write a server console application to receive messages.</span><span class="sxs-lookup"><span data-stu-id="ab429-109">Write a server console application to receive messages.</span></span>
4. <span data-ttu-id="ab429-110">Write a client console application to send messages.</span><span class="sxs-lookup"><span data-stu-id="ab429-110">Write a client console application to send messages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ab429-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="ab429-111">Prerequisites</span></span>
1. <span data-ttu-id="ab429-112">[Node.js](https://nodejs.org/en/) (This sample uses Node 7.0).</span><span class="sxs-lookup"><span data-stu-id="ab429-112">[Node.js](https://nodejs.org/en/) (This sample uses Node 7.0).</span></span>
2. <span data-ttu-id="ab429-113">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="ab429-113">An Azure subscription.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-the-azure-portal"></a><span data-ttu-id="ab429-114">1. Create a namespace using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="ab429-114">1. Create a namespace using the Azure portal</span></span>
<span data-ttu-id="ab429-115">If you already have a Relay namespace created, jump to the [Create a Hybrid Connection using the Azure portal](#2-create-a-hybrid-connection-using-the-azure-portal) section.</span><span class="sxs-lookup"><span data-stu-id="ab429-115">If you already have a Relay namespace created, jump to the [Create a Hybrid Connection using the Azure portal](#2-create-a-hybrid-connection-using-the-azure-portal) section.</span></span>

[!INCLUDE [relay-create-namespace-portal](../../includes/relay-create-namespace-portal.md)]

## <a name="2-create-a-hybrid-connection-using-the-azure-portal"></a><span data-ttu-id="ab429-116">2. Create a Hybrid Connection using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="ab429-116">2. Create a Hybrid Connection using the Azure portal</span></span>
<span data-ttu-id="ab429-117">If you already have a Hybrid Connection created, jump to the [Create a server application](#3-create-a-server-application-listener) section.</span><span class="sxs-lookup"><span data-stu-id="ab429-117">If you already have a Hybrid Connection created, jump to the [Create a server application](#3-create-a-server-application-listener) section.</span></span>

[!INCLUDE [relay-create-hybrid-connection-portal](../../includes/relay-create-hybrid-connection-portal.md)]

## <a name="3-create-a-server-application-listener"></a><span data-ttu-id="ab429-118">3. Create a server application (listener)</span><span class="sxs-lookup"><span data-stu-id="ab429-118">3. Create a server application (listener)</span></span>
<span data-ttu-id="ab429-119">To listen and receive messages from the Relay, we will write a Node.js console application.</span><span class="sxs-lookup"><span data-stu-id="ab429-119">To listen and receive messages from the Relay, we will write a Node.js console application.</span></span>

[!INCLUDE [relay-hybrid-connections-dotnet-get-started-server](../../includes/relay-hybrid-connections-node-get-started-server.md)]

## <a name="4-create-a-client-application-sender"></a><span data-ttu-id="ab429-120">4. Create a client application (sender)</span><span class="sxs-lookup"><span data-stu-id="ab429-120">4. Create a client application (sender)</span></span>
<span data-ttu-id="ab429-121">To send messages to the Relay, we will write a Node.js console application.</span><span class="sxs-lookup"><span data-stu-id="ab429-121">To send messages to the Relay, we will write a Node.js console application.</span></span>

[!INCLUDE [relay-hybrid-connections-dotnet-get-started-client](../../includes/relay-hybrid-connections-node-get-started-client.md)]

## <a name="5-run-the-applications"></a><span data-ttu-id="ab429-122">5. Run the applications</span><span class="sxs-lookup"><span data-stu-id="ab429-122">5. Run the applications</span></span>
1. <span data-ttu-id="ab429-123">Run the server application.</span><span class="sxs-lookup"><span data-stu-id="ab429-123">Run the server application.</span></span>
2. <span data-ttu-id="ab429-124">Run the client application and enter some text.</span><span class="sxs-lookup"><span data-stu-id="ab429-124">Run the client application and enter some text.</span></span>
3. <span data-ttu-id="ab429-125">Ensure that the server application console outputs the text that was entered in the client application.</span><span class="sxs-lookup"><span data-stu-id="ab429-125">Ensure that the server application console outputs the text that was entered in the client application.</span></span>

![running-applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-bus-relay/media/relay-hybrid-connections-node-get-started/running-applications.png)

<span data-ttu-id="ab429-127">Congratulations, you have created an end-to-end Hybrid Connections application.</span><span class="sxs-lookup"><span data-stu-id="ab429-127">Congratulations, you have created an end-to-end Hybrid Connections application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ab429-128">Next steps:</span><span class="sxs-lookup"><span data-stu-id="ab429-128">Next steps:</span></span>
* [<span data-ttu-id="ab429-129">Relay FAQ</span><span class="sxs-lookup"><span data-stu-id="ab429-129">Relay FAQ</span></span>](relay-faq.md)
* [<span data-ttu-id="ab429-130">Create a namespace</span><span class="sxs-lookup"><span data-stu-id="ab429-130">Create a namespace</span></span>](relay-create-namespace-portal.md)
* [<span data-ttu-id="ab429-131">Get started with .NET</span><span class="sxs-lookup"><span data-stu-id="ab429-131">Get started with .NET</span></span>](relay-hybrid-connections-dotnet-get-started.md)
* [<span data-ttu-id="ab429-132">Get started with Node</span><span class="sxs-lookup"><span data-stu-id="ab429-132">Get started with Node</span></span>](relay-hybrid-connections-node-get-started.md)


