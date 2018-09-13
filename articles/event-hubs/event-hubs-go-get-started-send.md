---
title: Send events to Azure Event Hubs using Go | Microsoft Docs
description: Get started sending events to Event Hubs using Go
services: event-hubs
author: ShubhaVijayasarathy
manager: kamalb
ms.service: event-hubs
ms.workload: core
ms.topic: article
ms.date: 07/23/2018
ms.author: shvija
ms.openlocfilehash: 40b3aa82c3e9e8ab9a30362c0a41998877655725
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855880"
---
# <a name="send-events-to-event-hubs-using-go"></a><span data-ttu-id="c4c80-103">Send events to Event Hubs using Go</span><span class="sxs-lookup"><span data-stu-id="c4c80-103">Send events to Event Hubs using Go</span></span>

<span data-ttu-id="c4c80-104">Azure Event Hubs is a highly scalable event management system that can handle millions of events per second, enabling applications to process and analyze massive amounts of data produced by connected devices and other systems.</span><span class="sxs-lookup"><span data-stu-id="c4c80-104">Azure Event Hubs is a highly scalable event management system that can handle millions of events per second, enabling applications to process and analyze massive amounts of data produced by connected devices and other systems.</span></span> <span data-ttu-id="c4c80-105">Once collected into an event hub, you can receive and handle events using in-process handlers or by forwarding to other analytics systems.</span><span class="sxs-lookup"><span data-stu-id="c4c80-105">Once collected into an event hub, you can receive and handle events using in-process handlers or by forwarding to other analytics systems.</span></span>

<span data-ttu-id="c4c80-106">To learn more about Event Hubs, see the [Event Hubs overview][Event Hubs overview].</span><span class="sxs-lookup"><span data-stu-id="c4c80-106">To learn more about Event Hubs, see the [Event Hubs overview][Event Hubs overview].</span></span>

<span data-ttu-id="c4c80-107">This tutorial describes how to send events to an event hub from an application written in Go.</span><span class="sxs-lookup"><span data-stu-id="c4c80-107">This tutorial describes how to send events to an event hub from an application written in Go.</span></span> <span data-ttu-id="c4c80-108">To receive events, use the **Go eph** (Event Processor Host) package as described in [the corresponding Receive article](event-hubs-go-get-started-receive-eph.md).</span><span class="sxs-lookup"><span data-stu-id="c4c80-108">To receive events, use the **Go eph** (Event Processor Host) package as described in [the corresponding Receive article](event-hubs-go-get-started-receive-eph.md).</span></span>

<span data-ttu-id="c4c80-109">Code in this tutorial is taken from [these GitHub samples](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/eventhubs), which you can examine to see the full working application, including import statements and variable declarations.</span><span class="sxs-lookup"><span data-stu-id="c4c80-109">Code in this tutorial is taken from [these GitHub samples](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/eventhubs), which you can examine to see the full working application, including import statements and variable declarations.</span></span>

<span data-ttu-id="c4c80-110">Other examples are available [in the Event Hubs package repo](https://github.com/Azure/azure-event-hubs-go/tree/master/_examples).</span><span class="sxs-lookup"><span data-stu-id="c4c80-110">Other examples are available [in the Event Hubs package repo](https://github.com/Azure/azure-event-hubs-go/tree/master/_examples).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c4c80-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="c4c80-111">Prerequisites</span></span>

<span data-ttu-id="c4c80-112">To complete this tutorial, you need the following prerequisites:</span><span class="sxs-lookup"><span data-stu-id="c4c80-112">To complete this tutorial, you need the following prerequisites:</span></span>

* <span data-ttu-id="c4c80-113">Go installed locally.</span><span class="sxs-lookup"><span data-stu-id="c4c80-113">Go installed locally.</span></span> <span data-ttu-id="c4c80-114">Follow [these instructions](https://golang.org/doc/install) if necessary.</span><span class="sxs-lookup"><span data-stu-id="c4c80-114">Follow [these instructions](https://golang.org/doc/install) if necessary.</span></span>
* <span data-ttu-id="c4c80-115">An active Azure account.</span><span class="sxs-lookup"><span data-stu-id="c4c80-115">An active Azure account.</span></span> <span data-ttu-id="c4c80-116">If you don't have an Azure subscription, create a [free account][] before you begin.</span><span class="sxs-lookup"><span data-stu-id="c4c80-116">If you don't have an Azure subscription, create a [free account][] before you begin.</span></span>
* <span data-ttu-id="c4c80-117">An existing Event Hubs namespace and event hub.</span><span class="sxs-lookup"><span data-stu-id="c4c80-117">An existing Event Hubs namespace and event hub.</span></span> <span data-ttu-id="c4c80-118">You can create these entities by following the instructions in [this article](event-hubs-create.md).</span><span class="sxs-lookup"><span data-stu-id="c4c80-118">You can create these entities by following the instructions in [this article](event-hubs-create.md).</span></span>

## <a name="install-go-package"></a><span data-ttu-id="c4c80-119">Install Go package</span><span class="sxs-lookup"><span data-stu-id="c4c80-119">Install Go package</span></span>

<span data-ttu-id="c4c80-120">Get the Go package for Event Hubs with `go get` or `dep`.</span><span class="sxs-lookup"><span data-stu-id="c4c80-120">Get the Go package for Event Hubs with `go get` or `dep`.</span></span> <span data-ttu-id="c4c80-121">For example:</span><span class="sxs-lookup"><span data-stu-id="c4c80-121">For example:</span></span>

```bash
go get -u github.com/Azure/azure-event-hubs-go
go get -u github.com/Azure/azure-amqp-common-go/...

# or

dep ensure -add github.com/Azure/azure-event-hubs-go
dep ensure -add github.com/Azure/azure-amqp-common-go
```

## <a name="import-packages-in-your-code-file"></a><span data-ttu-id="c4c80-122">Import packages in your code file</span><span class="sxs-lookup"><span data-stu-id="c4c80-122">Import packages in your code file</span></span>

<span data-ttu-id="c4c80-123">To import the Go packages, use the following code example:</span><span class="sxs-lookup"><span data-stu-id="c4c80-123">To import the Go packages, use the following code example:</span></span>

```go
import (
    aad "github.com/Azure/azure-amqp-common-go/aad"
    eventhubs "github.com/Azure/azure-event-hubs-go"
)
```

## <a name="create-service-principal"></a><span data-ttu-id="c4c80-124">Create service principal</span><span class="sxs-lookup"><span data-stu-id="c4c80-124">Create service principal</span></span>

<span data-ttu-id="c4c80-125">Create a new service principal by following the instructions in [Create an Azure service principal with Azure CLI 2.0](/cli/azure/create-an-azure-service-principal-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="c4c80-125">Create a new service principal by following the instructions in [Create an Azure service principal with Azure CLI 2.0](/cli/azure/create-an-azure-service-principal-azure-cli).</span></span> <span data-ttu-id="c4c80-126">Save the provided credentials in your environment with the following names.</span><span class="sxs-lookup"><span data-stu-id="c4c80-126">Save the provided credentials in your environment with the following names.</span></span> <span data-ttu-id="c4c80-127">Both the Azure SDK for Go and the Event Hubs packages are preconfigured to look for these variable names:</span><span class="sxs-lookup"><span data-stu-id="c4c80-127">Both the Azure SDK for Go and the Event Hubs packages are preconfigured to look for these variable names:</span></span>

```bash
export AZURE_CLIENT_ID=
export AZURE_CLIENT_SECRET=
export AZURE_TENANT_ID=
export AZURE_SUBSCRIPTION_ID= 
```

<span data-ttu-id="c4c80-128">Now, create an authorization provider for your Event Hubs client that uses these credentials:</span><span class="sxs-lookup"><span data-stu-id="c4c80-128">Now, create an authorization provider for your Event Hubs client that uses these credentials:</span></span>

```go
tokenProvider, err := aad.NewJWTProvider(aad.JWTProviderWithEnvironmentVars())
if err != nil {
    log.Fatalf("failed to configure AAD JWT provider: %s\n", err)
}
```

## <a name="create-event-hubs-client"></a><span data-ttu-id="c4c80-129">Create Event Hubs client</span><span class="sxs-lookup"><span data-stu-id="c4c80-129">Create Event Hubs client</span></span>

<span data-ttu-id="c4c80-130">The following code creates an Event Hubs client:</span><span class="sxs-lookup"><span data-stu-id="c4c80-130">The following code creates an Event Hubs client:</span></span>

```go
hub, err := eventhubs.NewHub("namespaceName", "hubName", tokenProvider)
ctx := context.WithTimeout(context.Background(), 10 * time.Second)
defer hub.Close(ctx)
if err != nil {
    log.Fatalf("failed to get hub %s\n", err)
}
```

## <a name="send-messages"></a><span data-ttu-id="c4c80-131">Send messages</span><span class="sxs-lookup"><span data-stu-id="c4c80-131">Send messages</span></span>

<span data-ttu-id="c4c80-132">In the following snippet, use (1) to send messages interactively from a terminal, or (2) to send messages within your program:</span><span class="sxs-lookup"><span data-stu-id="c4c80-132">In the following snippet, use (1) to send messages interactively from a terminal, or (2) to send messages within your program:</span></span>

```go
// 1. send messages at the terminal
ctx = context.Background()
reader := bufio.NewReader(os.Stdin)
for {
    fmt.Printf("Input a message to send: ")
    text, _ := reader.ReadString('\n')
    hub.Send(ctx, eventhubs.NewEventFromString(text))
}

// 2. send messages within program
ctx = context.Background()
hub.Send(ctx, eventhubs.NewEventFromString("hello Azure!")
```

## <a name="extras"></a><span data-ttu-id="c4c80-133">Extras</span><span class="sxs-lookup"><span data-stu-id="c4c80-133">Extras</span></span>

<span data-ttu-id="c4c80-134">Get the IDs of the partitions in your event hub:</span><span class="sxs-lookup"><span data-stu-id="c4c80-134">Get the IDs of the partitions in your event hub:</span></span>

```go
info, err := hub.GetRuntimeInformation(ctx)
if err != nil {
    log.Fatalf("failed to get runtime info: %s\n", err)
}
log.Printf("got partition IDs: %s\n, info.PartitionIDs)
```

## <a name="next-steps"></a><span data-ttu-id="c4c80-135">Next steps</span><span class="sxs-lookup"><span data-stu-id="c4c80-135">Next steps</span></span>

<span data-ttu-id="c4c80-136">Visit the following pages to learn more about Event Hubs:</span><span class="sxs-lookup"><span data-stu-id="c4c80-136">Visit the following pages to learn more about Event Hubs:</span></span>

* [<span data-ttu-id="c4c80-137">Receive events using EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="c4c80-137">Receive events using EventProcessorHost</span></span>](event-hubs-go-get-started-receive-eph.md)
* <span data-ttu-id="c4c80-138">[Event Hubs overview][Event Hubs overview]</span><span class="sxs-lookup"><span data-stu-id="c4c80-138">[Event Hubs overview][Event Hubs overview]</span></span>
* [<span data-ttu-id="c4c80-139">Create an event hub</span><span class="sxs-lookup"><span data-stu-id="c4c80-139">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="c4c80-140">Event Hubs FAQ</span><span class="sxs-lookup"><span data-stu-id="c4c80-140">Event Hubs FAQ</span></span>](event-hubs-faq.md)

<!-- Links -->
[Event Hubs overview]: event-hubs-about.md
[free account]: https://azure.microsoft.com/free/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio
