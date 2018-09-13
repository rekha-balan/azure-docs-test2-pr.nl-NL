---
title: Receive events from Azure Event Hubs using Go | Microsoft Docs
description: Get started receiving events from Event Hubs using Go
services: event-hubs
author: ShubhaVijayasarathy
manager: kamalb
ms.service: event-hubs
ms.workload: core
ms.topic: article
ms.date: 07/23/2018
ms.author: shvija
ms.openlocfilehash: eaea6adbaef7baf9bb1e617ba0a709cf14edf781
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870736"
---
# <a name="receive-events-from-event-hubs-using-go"></a><span data-ttu-id="8ecdd-103">Receive events from Event Hubs using Go</span><span class="sxs-lookup"><span data-stu-id="8ecdd-103">Receive events from Event Hubs using Go</span></span>

<span data-ttu-id="8ecdd-104">Azure Event Hubs is a highly scalable event management system that can handle millions of events per second, enabling applications to process and analyze massive amounts of data produced by connected devices and other systems.</span><span class="sxs-lookup"><span data-stu-id="8ecdd-104">Azure Event Hubs is a highly scalable event management system that can handle millions of events per second, enabling applications to process and analyze massive amounts of data produced by connected devices and other systems.</span></span> <span data-ttu-id="8ecdd-105">Once collected into an event hub, you can receive and handle events using in-process handlers or by forwarding to other analytics systems.</span><span class="sxs-lookup"><span data-stu-id="8ecdd-105">Once collected into an event hub, you can receive and handle events using in-process handlers or by forwarding to other analytics systems.</span></span>

<span data-ttu-id="8ecdd-106">To learn more about Event Hubs, see the [Event Hubs overview][Event Hubs overview].</span><span class="sxs-lookup"><span data-stu-id="8ecdd-106">To learn more about Event Hubs, see the [Event Hubs overview][Event Hubs overview].</span></span>

<span data-ttu-id="8ecdd-107">This tutorial describes how to receive events from an event hub in a Go application.</span><span class="sxs-lookup"><span data-stu-id="8ecdd-107">This tutorial describes how to receive events from an event hub in a Go application.</span></span> <span data-ttu-id="8ecdd-108">To learn how to send events see [the corresponding Send article](event-hubs-go-get-started-send.md).</span><span class="sxs-lookup"><span data-stu-id="8ecdd-108">To learn how to send events see [the corresponding Send article](event-hubs-go-get-started-send.md).</span></span>

<span data-ttu-id="8ecdd-109">Code in this tutorial is taken from [these GitHub samples](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/eventhubs), which you can examine to see the full working application including import statements and variable declarations.</span><span class="sxs-lookup"><span data-stu-id="8ecdd-109">Code in this tutorial is taken from [these GitHub samples](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/eventhubs), which you can examine to see the full working application including import statements and variable declarations.</span></span>

<span data-ttu-id="8ecdd-110">Other examples are available [in the Event Hubs package repo](https://github.com/Azure/azure-event-hubs-go/tree/master/_examples).</span><span class="sxs-lookup"><span data-stu-id="8ecdd-110">Other examples are available [in the Event Hubs package repo](https://github.com/Azure/azure-event-hubs-go/tree/master/_examples).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8ecdd-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="8ecdd-111">Prerequisites</span></span>

<span data-ttu-id="8ecdd-112">To complete this tutorial you'll need the following prerequisites:</span><span class="sxs-lookup"><span data-stu-id="8ecdd-112">To complete this tutorial you'll need the following prerequisites:</span></span>

* <span data-ttu-id="8ecdd-113">Go installed locally.</span><span class="sxs-lookup"><span data-stu-id="8ecdd-113">Go installed locally.</span></span> <span data-ttu-id="8ecdd-114">Follow [these instructions](https://golang.org/doc/install) if necessary.</span><span class="sxs-lookup"><span data-stu-id="8ecdd-114">Follow [these instructions](https://golang.org/doc/install) if necessary.</span></span>
* <span data-ttu-id="8ecdd-115">An active Azure account.</span><span class="sxs-lookup"><span data-stu-id="8ecdd-115">An active Azure account.</span></span> <span data-ttu-id="8ecdd-116">If you don't have an Azure subscription, create a [free account][] before you begin.</span><span class="sxs-lookup"><span data-stu-id="8ecdd-116">If you don't have an Azure subscription, create a [free account][] before you begin.</span></span>
* <span data-ttu-id="8ecdd-117">To receive messages, there must be messages in the target event hub.</span><span class="sxs-lookup"><span data-stu-id="8ecdd-117">To receive messages, there must be messages in the target event hub.</span></span> <span data-ttu-id="8ecdd-118">Learn how to send messages in the [send tutorial](event-hubs-go-get-started-send.md).</span><span class="sxs-lookup"><span data-stu-id="8ecdd-118">Learn how to send messages in the [send tutorial](event-hubs-go-get-started-send.md).</span></span>
* <span data-ttu-id="8ecdd-119">An existing event hub (see the following section).</span><span class="sxs-lookup"><span data-stu-id="8ecdd-119">An existing event hub (see the following section).</span></span>
* <span data-ttu-id="8ecdd-120">An existing storage account and container (see the section after the next section).</span><span class="sxs-lookup"><span data-stu-id="8ecdd-120">An existing storage account and container (see the section after the next section).</span></span>

### <a name="create-an-event-hub"></a><span data-ttu-id="8ecdd-121">Create an event hub</span><span class="sxs-lookup"><span data-stu-id="8ecdd-121">Create an event hub</span></span>

<span data-ttu-id="8ecdd-122">This tutorial starts with an existing Event Hubs namespace and event hub.</span><span class="sxs-lookup"><span data-stu-id="8ecdd-122">This tutorial starts with an existing Event Hubs namespace and event hub.</span></span> <span data-ttu-id="8ecdd-123">You can create these entities by following the instructions in [this article](event-hubs-create.md).</span><span class="sxs-lookup"><span data-stu-id="8ecdd-123">You can create these entities by following the instructions in [this article](event-hubs-create.md).</span></span>

### <a name="create-a-storage-account-and-container"></a><span data-ttu-id="8ecdd-124">Create a Storage account and container</span><span class="sxs-lookup"><span data-stu-id="8ecdd-124">Create a Storage account and container</span></span>

<span data-ttu-id="8ecdd-125">State such as leases on partitions and checkpoints in the event stream are shared between receivers using an Azure Storage container.</span><span class="sxs-lookup"><span data-stu-id="8ecdd-125">State such as leases on partitions and checkpoints in the event stream are shared between receivers using an Azure Storage container.</span></span> <span data-ttu-id="8ecdd-126">You can create a storage account and container with the Go SDK, but you can also create one by following the instructions in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="8ecdd-126">You can create a storage account and container with the Go SDK, but you can also create one by following the instructions in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

<span data-ttu-id="8ecdd-127">Samples for creating Storage artifacts with the Go SDK are available in the [Go samples repo](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/storage) and in the sample corresponding to this tutorial.</span><span class="sxs-lookup"><span data-stu-id="8ecdd-127">Samples for creating Storage artifacts with the Go SDK are available in the [Go samples repo](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/storage) and in the sample corresponding to this tutorial.</span></span>

## <a name="receive-messages"></a><span data-ttu-id="8ecdd-128">Receive messages</span><span class="sxs-lookup"><span data-stu-id="8ecdd-128">Receive messages</span></span>

<span data-ttu-id="8ecdd-129">To receive the messages, get the Go packages for Event Hubs with `go get` or `dep`:</span><span class="sxs-lookup"><span data-stu-id="8ecdd-129">To receive the messages, get the Go packages for Event Hubs with `go get` or `dep`:</span></span>

```bash
go get -u github.com/Azure/azure-event-hubs-go/...
go get -u github.com/Azure/azure-amqp-common-go/...
go get -u github.com/Azure/go-autorest/...

# or

dep ensure -add github.com/Azure/azure-event-hubs-go
dep ensure -add github.com/Azure/azure-amqp-common-go
dep ensure -add github.com/Azure/go-autorest
```

## <a name="import-packages-in-your-code-file"></a><span data-ttu-id="8ecdd-130">Import packages in your code file</span><span class="sxs-lookup"><span data-stu-id="8ecdd-130">Import packages in your code file</span></span>

<span data-ttu-id="8ecdd-131">To import the Go packages, use the following code example:</span><span class="sxs-lookup"><span data-stu-id="8ecdd-131">To import the Go packages, use the following code example:</span></span>

```go
import (
    aad "github.com/Azure/azure-amqp-common-go/aad"
    eventhubs "github.com/Azure/azure-event-hubs-go"
    eph "github.com/Azure/azure-event-hubs-go/eph"
    storageLeaser "github.com/Azure/azure-event-hubs-go/storage"
    azure "github.com/Azure/go-autorest/autorest/azure"
)
```

## <a name="create-service-principal"></a><span data-ttu-id="8ecdd-132">Create service principal</span><span class="sxs-lookup"><span data-stu-id="8ecdd-132">Create service principal</span></span>

<span data-ttu-id="8ecdd-133">Create a new service principal by following the instructions in [Create an Azure service principal with Azure CLI 2.0](/cli/azure/create-an-azure-service-principal-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="8ecdd-133">Create a new service principal by following the instructions in [Create an Azure service principal with Azure CLI 2.0](/cli/azure/create-an-azure-service-principal-azure-cli).</span></span> <span data-ttu-id="8ecdd-134">Save the provided credentials in your environment with the following names.</span><span class="sxs-lookup"><span data-stu-id="8ecdd-134">Save the provided credentials in your environment with the following names.</span></span> <span data-ttu-id="8ecdd-135">Both the Azure SDK for Go and the Event Hubs package are preconfigured to look for these variable names.</span><span class="sxs-lookup"><span data-stu-id="8ecdd-135">Both the Azure SDK for Go and the Event Hubs package are preconfigured to look for these variable names.</span></span>

```bash
export AZURE_CLIENT_ID=
export AZURE_CLIENT_SECRET=
export AZURE_TENANT_ID=
export AZURE_SUBSCRIPTION_ID= 
```

<span data-ttu-id="8ecdd-136">Next, create an authorization provider for your Event Hubs client that uses these credentials:</span><span class="sxs-lookup"><span data-stu-id="8ecdd-136">Next, create an authorization provider for your Event Hubs client that uses these credentials:</span></span>

```go
tokenProvider, err := aad.NewJWTProvider(aad.JWTProviderWithEnvironmentVars())
if err != nil {
    log.Fatalf("failed to configure AAD JWT provider: %s\n", err)
}
```

## <a name="get-metadata-struct"></a><span data-ttu-id="8ecdd-137">Get metadata struct</span><span class="sxs-lookup"><span data-stu-id="8ecdd-137">Get metadata struct</span></span>

<span data-ttu-id="8ecdd-138">Get a struct with metadata about your Azure environment using the Azure Go SDK.</span><span class="sxs-lookup"><span data-stu-id="8ecdd-138">Get a struct with metadata about your Azure environment using the Azure Go SDK.</span></span> <span data-ttu-id="8ecdd-139">Later operations use this struct to find correct endpoints.</span><span class="sxs-lookup"><span data-stu-id="8ecdd-139">Later operations use this struct to find correct endpoints.</span></span>

```go
azureEnv, err := azure.EnvironmentFromName("AzurePublicCloud")
if err != nil {
    log.Fatalf("could not get azure.Environment struct: %s\n", err)
}
```

## <a name="create-credential-helper"></a><span data-ttu-id="8ecdd-140">Create credential helper</span><span class="sxs-lookup"><span data-stu-id="8ecdd-140">Create credential helper</span></span> 

<span data-ttu-id="8ecdd-141">Create a credential helper that uses the previous Azure Active Directory (AAD) credentials to create a Shared Access Signature (SAS) credential for Storage.</span><span class="sxs-lookup"><span data-stu-id="8ecdd-141">Create a credential helper that uses the previous Azure Active Directory (AAD) credentials to create a Shared Access Signature (SAS) credential for Storage.</span></span> <span data-ttu-id="8ecdd-142">The last parameter tells this constructor to use the same environment variables as used previously:</span><span class="sxs-lookup"><span data-stu-id="8ecdd-142">The last parameter tells this constructor to use the same environment variables as used previously:</span></span>

```go
cred, err := storageLeaser.NewAADSASCredential(
    subscriptionID,
    resourceGroupName,
    storageAccountName,
    storageContainerName,
    storageLeaser.AADSASCredentialWithEnvironmentVars())
if err != nil {
    log.Fatalf("could not prepare a storage credential: %s\n", err)
}
```

## <a name="create-checkpointer-and-leaser"></a><span data-ttu-id="8ecdd-143">Create Checkpointer and Leaser</span><span class="sxs-lookup"><span data-stu-id="8ecdd-143">Create Checkpointer and Leaser</span></span> 

<span data-ttu-id="8ecdd-144">Create a **Leaser**, responsible for leasing a partition to a particular receiver, and a **Checkpointer**, responsible for writing checkpoints for the message stream so that other receivers can begin reading from the correct offset.</span><span class="sxs-lookup"><span data-stu-id="8ecdd-144">Create a **Leaser**, responsible for leasing a partition to a particular receiver, and a **Checkpointer**, responsible for writing checkpoints for the message stream so that other receivers can begin reading from the correct offset.</span></span>

<span data-ttu-id="8ecdd-145">Currently, a single **StorageLeaserCheckpointer** is available that uses the same Storage container to manage both leases and checkpoints.</span><span class="sxs-lookup"><span data-stu-id="8ecdd-145">Currently, a single **StorageLeaserCheckpointer** is available that uses the same Storage container to manage both leases and checkpoints.</span></span> <span data-ttu-id="8ecdd-146">In addition to the storage account and container names, the **StorageLeaserCheckpointer** needs the credential created in the previous step and the Azure environment struct to correctly access the container.</span><span class="sxs-lookup"><span data-stu-id="8ecdd-146">In addition to the storage account and container names, the **StorageLeaserCheckpointer** needs the credential created in the previous step and the Azure environment struct to correctly access the container.</span></span>

```go
leaserCheckpointer, err := storageLeaser.NewStorageLeaserCheckpointer(
    cred,
    storageAccountName,
    storageContainerName,
    azureEnv)
if err != nil {
    log.Fatalf("could not prepare a storage leaserCheckpointer: %s\n", err)
}
```

## <a name="construct-event-processor-host"></a><span data-ttu-id="8ecdd-147">Construct Event Processor Host</span><span class="sxs-lookup"><span data-stu-id="8ecdd-147">Construct Event Processor Host</span></span>

<span data-ttu-id="8ecdd-148">You now have the pieces needed to construct an EventProcessorHost, as follows.</span><span class="sxs-lookup"><span data-stu-id="8ecdd-148">You now have the pieces needed to construct an EventProcessorHost, as follows.</span></span> <span data-ttu-id="8ecdd-149">The same **StorageLeaserCheckpointer** is used as both a Leaser and Checkpointer, as described previously:</span><span class="sxs-lookup"><span data-stu-id="8ecdd-149">The same **StorageLeaserCheckpointer** is used as both a Leaser and Checkpointer, as described previously:</span></span>

```go
ctx := context.Background()
p, err := eph.New(
    ctx,
    nsName,
    hubName,
    tokenProvider,
    leaserCheckpointer,
    leaserCheckpointer)
if err != nil {
    log.Fatalf("failed to create EPH: %s\n", err)
}
defer p.Close(context.Background())
```

## <a name="create-handler"></a><span data-ttu-id="8ecdd-150">Create handler</span><span class="sxs-lookup"><span data-stu-id="8ecdd-150">Create handler</span></span> 

<span data-ttu-id="8ecdd-151">Now create a handler and register it with the Event Processor Host.</span><span class="sxs-lookup"><span data-stu-id="8ecdd-151">Now create a handler and register it with the Event Processor Host.</span></span> <span data-ttu-id="8ecdd-152">When the host is started, it applies this and any other specified handlers to incoming messages:</span><span class="sxs-lookup"><span data-stu-id="8ecdd-152">When the host is started, it applies this and any other specified handlers to incoming messages:</span></span>

```go
handler := func(ctx context.Context, event *eventhubs.Event) error {
    fmt.Printf("received: %s\n", string(event.Data))
    return nil
}

// register the handler with the EPH
_, err := p.RegisterHandler(ctx, handler)
if err != nil {
    log.Fatalf("failed to register handler: %s\n", err)
}
```

## <a name="receive-messages"></a><span data-ttu-id="8ecdd-153">Receive messages</span><span class="sxs-lookup"><span data-stu-id="8ecdd-153">Receive messages</span></span>

<span data-ttu-id="8ecdd-154">With everything set up, you can start the Event Processor Host with `Start(context)` to keep it permanently running, or with `StartNonBlocking(context)` to run only as long as messages are available.</span><span class="sxs-lookup"><span data-stu-id="8ecdd-154">With everything set up, you can start the Event Processor Host with `Start(context)` to keep it permanently running, or with `StartNonBlocking(context)` to run only as long as messages are available.</span></span>

<span data-ttu-id="8ecdd-155">This tutorial starts and runs as follows; see the GitHub sample for an example using `StartNonBlocking`:</span><span class="sxs-lookup"><span data-stu-id="8ecdd-155">This tutorial starts and runs as follows; see the GitHub sample for an example using `StartNonBlocking`:</span></span>

```go
ctx := context.Background()
err = p.Start()
if err != nil {
    log.Fatalf("failed to start EPH: %s\n", err)
}
```

## <a name="notes"></a><span data-ttu-id="8ecdd-156">Notes</span><span class="sxs-lookup"><span data-stu-id="8ecdd-156">Notes</span></span>

<span data-ttu-id="8ecdd-157">This tutorial uses a single instance of **EventProcessorHost**.</span><span class="sxs-lookup"><span data-stu-id="8ecdd-157">This tutorial uses a single instance of **EventProcessorHost**.</span></span> <span data-ttu-id="8ecdd-158">To increase throughput and reliability, you should run multiple instances of **EventProcessorHost** on different systems.</span><span class="sxs-lookup"><span data-stu-id="8ecdd-158">To increase throughput and reliability, you should run multiple instances of **EventProcessorHost** on different systems.</span></span> <span data-ttu-id="8ecdd-159">The Leaser system ensures that only one receiver is associated with, and receives messages from, a specified partition at a specified time.</span><span class="sxs-lookup"><span data-stu-id="8ecdd-159">The Leaser system ensures that only one receiver is associated with, and receives messages from, a specified partition at a specified time.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8ecdd-160">Next steps</span><span class="sxs-lookup"><span data-stu-id="8ecdd-160">Next steps</span></span>

<span data-ttu-id="8ecdd-161">Visit these pages to learn more about Event Hubs:</span><span class="sxs-lookup"><span data-stu-id="8ecdd-161">Visit these pages to learn more about Event Hubs:</span></span>

* [<span data-ttu-id="8ecdd-162">Send events with Go</span><span class="sxs-lookup"><span data-stu-id="8ecdd-162">Send events with Go</span></span>](event-hubs-go-get-started-send.md)
* [<span data-ttu-id="8ecdd-163">Event Hubs overview</span><span class="sxs-lookup"><span data-stu-id="8ecdd-163">Event Hubs overview</span></span>](event-hubs-about.md)
* [<span data-ttu-id="8ecdd-164">Create an Event Hub</span><span class="sxs-lookup"><span data-stu-id="8ecdd-164">Create an Event Hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="8ecdd-165">Event Hubs FAQ</span><span class="sxs-lookup"><span data-stu-id="8ecdd-165">Event Hubs FAQ</span></span>](event-hubs-faq.md)

<!-- Links -->
[Event Hubs overview]: event-hubs-about.md
[free account]: https://azure.microsoft.com/free/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio
