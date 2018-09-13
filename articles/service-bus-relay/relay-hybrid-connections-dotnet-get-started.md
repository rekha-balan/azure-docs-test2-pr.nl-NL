---
title: Get started with Azure Relay Hybrid Connections in .NET | Microsoft Docs
description: How to write a C# console application for Hybrid Connections
services: service-bus-relay
documentationcenter: .net
author: jtaubensee
manager: timlt
editor: ''
ms.assetid: d1386900-b942-4abf-acfc-38d2ef826253
ms.service: service-bus-relay
ms.devlang: tbd
ms.topic: get-started-article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 03/27/2017
ms.author: jotaub;sethm
ms.openlocfilehash: 25c0ba271885021efe701eed271cdab0132c4f9a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661355"
---
# <a name="get-started-with-relay-hybrid-connections"></a><span data-ttu-id="21f85-103">Get started with Relay Hybrid Connections</span><span class="sxs-lookup"><span data-stu-id="21f85-103">Get started with Relay Hybrid Connections</span></span>
[!INCLUDE [relay-selector-hybrid-connections](../../includes/relay-selector-hybrid-connections.md)]

<span data-ttu-id="21f85-104">This tutorial provides an introduction to [Azure Relay Hybrid Connections](relay-what-is-it.md#hybrid-connections), and shows how to create a client application that sends messages to a corresponding listener application.</span><span class="sxs-lookup"><span data-stu-id="21f85-104">This tutorial provides an introduction to [Azure Relay Hybrid Connections](relay-what-is-it.md#hybrid-connections), and shows how to create a client application that sends messages to a corresponding listener application.</span></span> 

## <a name="what-will-be-accomplished"></a><span data-ttu-id="21f85-105">What will be accomplished</span><span class="sxs-lookup"><span data-stu-id="21f85-105">What will be accomplished</span></span>
<span data-ttu-id="21f85-106">Because Hybrid Connections requires both a client and a server component, the tutorial creates two console applications.</span><span class="sxs-lookup"><span data-stu-id="21f85-106">Because Hybrid Connections requires both a client and a server component, the tutorial creates two console applications.</span></span> <span data-ttu-id="21f85-107">The steps are:</span><span class="sxs-lookup"><span data-stu-id="21f85-107">The steps are:</span></span>

1. <span data-ttu-id="21f85-108">Create a Relay namespace, using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="21f85-108">Create a Relay namespace, using the Azure portal.</span></span>
2. <span data-ttu-id="21f85-109">Create a Hybrid Connection, using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="21f85-109">Create a Hybrid Connection, using the Azure portal.</span></span>
3. <span data-ttu-id="21f85-110">Write a server (listener) console application to receive messages.</span><span class="sxs-lookup"><span data-stu-id="21f85-110">Write a server (listener) console application to receive messages.</span></span>
4. <span data-ttu-id="21f85-111">Write a client (sender) console application to send messages.</span><span class="sxs-lookup"><span data-stu-id="21f85-111">Write a client (sender) console application to send messages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="21f85-112">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="21f85-112">Prerequisites</span></span>
1. <span data-ttu-id="21f85-113">[Visual Studio 2015 or higher](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="21f85-113">[Visual Studio 2015 or higher](http://www.visualstudio.com).</span></span> <span data-ttu-id="21f85-114">The examples in this tutorial use Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="21f85-114">The examples in this tutorial use Visual Studio 2015.</span></span>
2. <span data-ttu-id="21f85-115">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="21f85-115">An Azure subscription.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-the-azure-portal"></a><span data-ttu-id="21f85-116">1. Create a namespace using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="21f85-116">1. Create a namespace using the Azure portal</span></span>
<span data-ttu-id="21f85-117">If you have already created a Relay namespace, jump to the [Create a Hybrid Connection using the Azure portal](#2-create-a-hybrid-connection-using-the-azure-portal) section.</span><span class="sxs-lookup"><span data-stu-id="21f85-117">If you have already created a Relay namespace, jump to the [Create a Hybrid Connection using the Azure portal](#2-create-a-hybrid-connection-using-the-azure-portal) section.</span></span>

[!INCLUDE [relay-create-namespace-portal](../../includes/relay-create-namespace-portal.md)]

## <a name="2-create-a-hybrid-connection-using-the-azure-portal"></a><span data-ttu-id="21f85-118">2. Create a Hybrid Connection using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="21f85-118">2. Create a Hybrid Connection using the Azure portal</span></span>
<span data-ttu-id="21f85-119">If you have already created a Hybrid Connection, jump to the [Create a server application](#3-create-a-server-application-listener) section.</span><span class="sxs-lookup"><span data-stu-id="21f85-119">If you have already created a Hybrid Connection, jump to the [Create a server application](#3-create-a-server-application-listener) section.</span></span>

[!INCLUDE [relay-create-hybrid-connection-portal](../../includes/relay-create-hybrid-connection-portal.md)]

## <a name="3-create-a-server-application-listener"></a><span data-ttu-id="21f85-120">3. Create a server application (listener)</span><span class="sxs-lookup"><span data-stu-id="21f85-120">3. Create a server application (listener)</span></span>
<span data-ttu-id="21f85-121">To listen and receive messages from the Relay, we will write a C# console application using Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="21f85-121">To listen and receive messages from the Relay, we will write a C# console application using Visual Studio.</span></span>

[!INCLUDE [relay-hybrid-connections-dotnet-get-started-server](../../includes/relay-hybrid-connections-dotnet-get-started-server.md)]

## <a name="4-create-a-client-application-sender"></a><span data-ttu-id="21f85-122">4. Create a client application (sender)</span><span class="sxs-lookup"><span data-stu-id="21f85-122">4. Create a client application (sender)</span></span>
<span data-ttu-id="21f85-123">To send messages to the Relay, we will write a C# console application using Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="21f85-123">To send messages to the Relay, we will write a C# console application using Visual Studio.</span></span>

[!INCLUDE [relay-hybrid-connections-dotnet-get-started-client](../../includes/relay-hybrid-connections-dotnet-get-started-client.md)]

## <a name="5-run-the-applications"></a><span data-ttu-id="21f85-124">5. Run the applications</span><span class="sxs-lookup"><span data-stu-id="21f85-124">5. Run the applications</span></span>
1. <span data-ttu-id="21f85-125">Run the server application.</span><span class="sxs-lookup"><span data-stu-id="21f85-125">Run the server application.</span></span>
2. <span data-ttu-id="21f85-126">Run the client application and enter some text.</span><span class="sxs-lookup"><span data-stu-id="21f85-126">Run the client application and enter some text.</span></span>
3. <span data-ttu-id="21f85-127">Ensure that the server application console outputs the text that was entered in the client application.</span><span class="sxs-lookup"><span data-stu-id="21f85-127">Ensure that the server application console outputs the text that was entered in the client application.</span></span>

![running-applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-bus-relay/media/relay-hybrid-connections-dotnet-get-started/running-applications.png)

<span data-ttu-id="21f85-129">Congratulations, you have created an end-to-end Hybrid Connections application.</span><span class="sxs-lookup"><span data-stu-id="21f85-129">Congratulations, you have created an end-to-end Hybrid Connections application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="21f85-130">Next steps:</span><span class="sxs-lookup"><span data-stu-id="21f85-130">Next steps:</span></span>
* [<span data-ttu-id="21f85-131">Relay FAQ</span><span class="sxs-lookup"><span data-stu-id="21f85-131">Relay FAQ</span></span>](relay-faq.md)
* [<span data-ttu-id="21f85-132">Create a namespace</span><span class="sxs-lookup"><span data-stu-id="21f85-132">Create a namespace</span></span>](relay-create-namespace-portal.md)
* [<span data-ttu-id="21f85-133">Get started with Node</span><span class="sxs-lookup"><span data-stu-id="21f85-133">Get started with Node</span></span>](relay-hybrid-connections-node-get-started.md)


