---
title: Get started with Azure Relay Hybrid Connections Websockets in .NET | Microsoft Docs
description: Write a C# console application for Azure Relay Hybrid Connections Websockets.
services: service-bus-relay
documentationcenter: .net
author: spelluru
manager: timlt
editor: ''
ms.assetid: d1386900-b942-4abf-acfc-38d2ef826253
ms.service: service-bus-relay
ms.devlang: tbd
ms.topic: get-started-article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 12/15/2017
ms.author: spelluru
ms.openlocfilehash: 1ed401f6175d7ebea83a888898221d345791bc34
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44800168"
---
# <a name="get-started-with-relay-hybrid-connections-websockets-in-net"></a><span data-ttu-id="705a3-103">Get started with Relay Hybrid Connections Websockets in .NET</span><span class="sxs-lookup"><span data-stu-id="705a3-103">Get started with Relay Hybrid Connections Websockets in .NET</span></span>
[!INCLUDE [relay-selector-hybrid-connections](../../includes/relay-selector-hybrid-connections.md)]

<span data-ttu-id="705a3-104">This tutorial provides an introduction to [Azure Relay Hybrid Connections](relay-what-is-it.md#hybrid-connections).</span><span class="sxs-lookup"><span data-stu-id="705a3-104">This tutorial provides an introduction to [Azure Relay Hybrid Connections](relay-what-is-it.md#hybrid-connections).</span></span> <span data-ttu-id="705a3-105">Learn how to use Microsoft .NET to create a client application that sends messages to a corresponding listener application.</span><span class="sxs-lookup"><span data-stu-id="705a3-105">Learn how to use Microsoft .NET to create a client application that sends messages to a corresponding listener application.</span></span> 

## <a name="what-will-be-accomplished"></a><span data-ttu-id="705a3-106">What will be accomplished</span><span class="sxs-lookup"><span data-stu-id="705a3-106">What will be accomplished</span></span>
<span data-ttu-id="705a3-107">Hybrid Connections requires both a client component and a server component.</span><span class="sxs-lookup"><span data-stu-id="705a3-107">Hybrid Connections requires both a client component and a server component.</span></span> <span data-ttu-id="705a3-108">In this tutorial, you complete these steps to create two console applications:</span><span class="sxs-lookup"><span data-stu-id="705a3-108">In this tutorial, you complete these steps to create two console applications:</span></span>

1. <span data-ttu-id="705a3-109">Create a Relay namespace by using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="705a3-109">Create a Relay namespace by using the Azure portal.</span></span>
2. <span data-ttu-id="705a3-110">Create a hybrid connection in that namespace by using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="705a3-110">Create a hybrid connection in that namespace by using the Azure portal.</span></span>
3. <span data-ttu-id="705a3-111">Write a server (listener) console application to receive messages.</span><span class="sxs-lookup"><span data-stu-id="705a3-111">Write a server (listener) console application to receive messages.</span></span>
4. <span data-ttu-id="705a3-112">Write a client (sender) console application to send messages.</span><span class="sxs-lookup"><span data-stu-id="705a3-112">Write a client (sender) console application to send messages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="705a3-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="705a3-113">Prerequisites</span></span>

<span data-ttu-id="705a3-114">To complete this tutorial, you need the following prerequisites:</span><span class="sxs-lookup"><span data-stu-id="705a3-114">To complete this tutorial, you need the following prerequisites:</span></span>

* <span data-ttu-id="705a3-115">[Visual Studio 2015 or later](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="705a3-115">[Visual Studio 2015 or later](http://www.visualstudio.com).</span></span> <span data-ttu-id="705a3-116">The examples in this tutorial use Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="705a3-116">The examples in this tutorial use Visual Studio 2017.</span></span>
* <span data-ttu-id="705a3-117">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="705a3-117">An Azure subscription.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-by-using-the-azure-portal"></a><span data-ttu-id="705a3-118">1. Create a namespace by using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="705a3-118">1. Create a namespace by using the Azure portal</span></span>
<span data-ttu-id="705a3-119">If you have already created a Relay namespace, go to [Create a hybrid connection by using the Azure portal](#2-create-a-hybrid-connection-using-the-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="705a3-119">If you have already created a Relay namespace, go to [Create a hybrid connection by using the Azure portal](#2-create-a-hybrid-connection-using-the-azure-portal).</span></span>

[!INCLUDE [relay-create-namespace-portal](../../includes/relay-create-namespace-portal.md)]

## <a name="2-create-a-hybrid-connection-by-using-the-azure-portal"></a><span data-ttu-id="705a3-120">2. Create a hybrid connection by using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="705a3-120">2. Create a hybrid connection by using the Azure portal</span></span>
<span data-ttu-id="705a3-121">If you have already created a hybrid connection, go to [Create a server application](#3-create-a-server-application-listener).</span><span class="sxs-lookup"><span data-stu-id="705a3-121">If you have already created a hybrid connection, go to [Create a server application](#3-create-a-server-application-listener).</span></span>

[!INCLUDE [relay-create-hybrid-connection-portal](../../includes/relay-create-hybrid-connection-portal.md)]

## <a name="3-create-a-server-application-listener"></a><span data-ttu-id="705a3-122">3. Create a server application (listener)</span><span class="sxs-lookup"><span data-stu-id="705a3-122">3. Create a server application (listener)</span></span>
<span data-ttu-id="705a3-123">In Visual Studio, write a C# console application to listen for and receive messages from the relay.</span><span class="sxs-lookup"><span data-stu-id="705a3-123">In Visual Studio, write a C# console application to listen for and receive messages from the relay.</span></span>

[!INCLUDE [relay-hybrid-connections-dotnet-get-started-server](../../includes/relay-hybrid-connections-dotnet-get-started-server.md)]

## <a name="4-create-a-client-application-sender"></a><span data-ttu-id="705a3-124">4. Create a client application (sender)</span><span class="sxs-lookup"><span data-stu-id="705a3-124">4. Create a client application (sender)</span></span>
<span data-ttu-id="705a3-125">In Visual Studio, write a C# console application to send messages to the relay.</span><span class="sxs-lookup"><span data-stu-id="705a3-125">In Visual Studio, write a C# console application to send messages to the relay.</span></span>

[!INCLUDE [relay-hybrid-connections-dotnet-get-started-client](../../includes/relay-hybrid-connections-dotnet-get-started-client.md)]

## <a name="5-run-the-applications"></a><span data-ttu-id="705a3-126">5. Run the applications</span><span class="sxs-lookup"><span data-stu-id="705a3-126">5. Run the applications</span></span>
1. <span data-ttu-id="705a3-127">Run the server application.</span><span class="sxs-lookup"><span data-stu-id="705a3-127">Run the server application.</span></span>
2. <span data-ttu-id="705a3-128">Run the client application and enter some text.</span><span class="sxs-lookup"><span data-stu-id="705a3-128">Run the client application and enter some text.</span></span>
3. <span data-ttu-id="705a3-129">Ensure that the server application console displays the text that was entered in the client application.</span><span class="sxs-lookup"><span data-stu-id="705a3-129">Ensure that the server application console displays the text that was entered in the client application.</span></span>

![running-applications](./media/relay-hybrid-connections-dotnet-get-started/running-applications.png)

<span data-ttu-id="705a3-131">Congratulations, you have created an end-to-end Hybrid Connections application!</span><span class="sxs-lookup"><span data-stu-id="705a3-131">Congratulations, you have created an end-to-end Hybrid Connections application!</span></span>

## <a name="next-steps"></a><span data-ttu-id="705a3-132">Next steps</span><span class="sxs-lookup"><span data-stu-id="705a3-132">Next steps</span></span>

* [<span data-ttu-id="705a3-133">Relay FAQ</span><span class="sxs-lookup"><span data-stu-id="705a3-133">Relay FAQ</span></span>](relay-faq.md)
* [<span data-ttu-id="705a3-134">Create a namespace</span><span class="sxs-lookup"><span data-stu-id="705a3-134">Create a namespace</span></span>](relay-create-namespace-portal.md)
* [<span data-ttu-id="705a3-135">Get started with Node</span><span class="sxs-lookup"><span data-stu-id="705a3-135">Get started with Node</span></span>](relay-hybrid-connections-node-get-started.md)

