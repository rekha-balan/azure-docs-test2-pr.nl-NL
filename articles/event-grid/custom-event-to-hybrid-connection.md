---
title: Send custom events for Azure Event Grid to hybrid connection | Microsoft Docs
description: Use Azure Event Grid and Azure CLI to publish a topic, and subscribe to that event. A hybrid connection is used for the endpoint.
services: event-grid
keywords: ''
author: tfitzmac
ms.author: tomfitz
ms.date: 06/29/2018
ms.topic: tutorial
ms.service: event-grid
ms.openlocfilehash: 544f5210adbea6791f9224a1e2be0743ce9995d5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865495"
---
# <a name="route-custom-events-to-azure-relay-hybrid-connections-with-azure-cli-and-event-grid"></a><span data-ttu-id="24721-104">Route custom events to Azure Relay Hybrid Connections with Azure CLI and Event Grid</span><span class="sxs-lookup"><span data-stu-id="24721-104">Route custom events to Azure Relay Hybrid Connections with Azure CLI and Event Grid</span></span>

<span data-ttu-id="24721-105">Azure Event Grid is an eventing service for the cloud.</span><span class="sxs-lookup"><span data-stu-id="24721-105">Azure Event Grid is an eventing service for the cloud.</span></span> <span data-ttu-id="24721-106">Azure Relay Hybrid Connections is one of the supported event handlers.</span><span class="sxs-lookup"><span data-stu-id="24721-106">Azure Relay Hybrid Connections is one of the supported event handlers.</span></span> <span data-ttu-id="24721-107">You use hybrid connections as the event handler when you need to process events from applications that don't have a public endpoint.</span><span class="sxs-lookup"><span data-stu-id="24721-107">You use hybrid connections as the event handler when you need to process events from applications that don't have a public endpoint.</span></span> <span data-ttu-id="24721-108">These applications might be within your corporate enterprise network.</span><span class="sxs-lookup"><span data-stu-id="24721-108">These applications might be within your corporate enterprise network.</span></span> <span data-ttu-id="24721-109">In this article, you use the Azure CLI to create a custom topic, subscribe to the topic, and trigger the event to view the result.</span><span class="sxs-lookup"><span data-stu-id="24721-109">In this article, you use the Azure CLI to create a custom topic, subscribe to the topic, and trigger the event to view the result.</span></span> <span data-ttu-id="24721-110">You send the events to the hybrid connection.</span><span class="sxs-lookup"><span data-stu-id="24721-110">You send the events to the hybrid connection.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="24721-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="24721-111">Prerequisites</span></span>

<span data-ttu-id="24721-112">This article assumes you already have a hybrid connection and a listener application.</span><span class="sxs-lookup"><span data-stu-id="24721-112">This article assumes you already have a hybrid connection and a listener application.</span></span> <span data-ttu-id="24721-113">To get started with hybrid connections, see [Get started with Relay Hybrid Connections - .NET](../service-bus-relay/relay-hybrid-connections-dotnet-get-started.md) or [Get started with Relay Hybrid Connections - Node](../service-bus-relay/relay-hybrid-connections-node-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="24721-113">To get started with hybrid connections, see [Get started with Relay Hybrid Connections - .NET](../service-bus-relay/relay-hybrid-connections-dotnet-get-started.md) or [Get started with Relay Hybrid Connections - Node](../service-bus-relay/relay-hybrid-connections-node-get-started.md).</span></span>

[!INCLUDE [event-grid-preview-feature-note.md](../../includes/event-grid-preview-feature-note.md)]

## <a name="create-a-resource-group"></a><span data-ttu-id="24721-114">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="24721-114">Create a resource group</span></span>

<span data-ttu-id="24721-115">Event Grid topics are Azure resources, and must be placed in an Azure resource group.</span><span class="sxs-lookup"><span data-stu-id="24721-115">Event Grid topics are Azure resources, and must be placed in an Azure resource group.</span></span> <span data-ttu-id="24721-116">The resource group is a logical collection into which Azure resources are deployed and managed.</span><span class="sxs-lookup"><span data-stu-id="24721-116">The resource group is a logical collection into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="24721-117">Create a resource group with the [az group create](/cli/azure/group#az-group-create) command.</span><span class="sxs-lookup"><span data-stu-id="24721-117">Create a resource group with the [az group create](/cli/azure/group#az-group-create) command.</span></span> 

<span data-ttu-id="24721-118">The following example creates a resource group named *gridResourceGroup* in the *westus2* location.</span><span class="sxs-lookup"><span data-stu-id="24721-118">The following example creates a resource group named *gridResourceGroup* in the *westus2* location.</span></span>

```azurecli-interactive
az group create --name gridResourceGroup --location westus2
```

## <a name="create-a-custom-topic"></a><span data-ttu-id="24721-119">Create a custom topic</span><span class="sxs-lookup"><span data-stu-id="24721-119">Create a custom topic</span></span>

<span data-ttu-id="24721-120">An event grid topic provides a user-defined endpoint that you post your events to.</span><span class="sxs-lookup"><span data-stu-id="24721-120">An event grid topic provides a user-defined endpoint that you post your events to.</span></span> <span data-ttu-id="24721-121">The following example creates the custom topic in your resource group.</span><span class="sxs-lookup"><span data-stu-id="24721-121">The following example creates the custom topic in your resource group.</span></span> <span data-ttu-id="24721-122">Replace `<topic_name>` with a unique name for your topic.</span><span class="sxs-lookup"><span data-stu-id="24721-122">Replace `<topic_name>` with a unique name for your topic.</span></span> <span data-ttu-id="24721-123">The topic name must be unique because it's represented by a DNS entry.</span><span class="sxs-lookup"><span data-stu-id="24721-123">The topic name must be unique because it's represented by a DNS entry.</span></span>

```azurecli-interactive
# if you have not already installed the extension, do it now.
# This extension is required for preview features.
az extension add --name eventgrid

az eventgrid topic create --name <topic_name> -l westus2 -g gridResourceGroup
```

## <a name="subscribe-to-a-topic"></a><span data-ttu-id="24721-124">Subscribe to a topic</span><span class="sxs-lookup"><span data-stu-id="24721-124">Subscribe to a topic</span></span>

<span data-ttu-id="24721-125">You subscribe to a topic to tell Event Grid which events you want to track. The following example subscribes to the topic you created, and passes the resource ID of the hybrid connection for the endpoint.</span><span class="sxs-lookup"><span data-stu-id="24721-125">You subscribe to a topic to tell Event Grid which events you want to track. The following example subscribes to the topic you created, and passes the resource ID of the hybrid connection for the endpoint.</span></span> <span data-ttu-id="24721-126">The hybrid connection ID is in the format:</span><span class="sxs-lookup"><span data-stu-id="24721-126">The hybrid connection ID is in the format:</span></span>

`/subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Relay/namespaces/<relay-namespace>/hybridConnections/<hybrid-connection-name>`

<span data-ttu-id="24721-127">The following script gets the resource ID of the relay namespace.</span><span class="sxs-lookup"><span data-stu-id="24721-127">The following script gets the resource ID of the relay namespace.</span></span> <span data-ttu-id="24721-128">It constructs the ID for the hybrid connection, and subscribes to an event grid topic.</span><span class="sxs-lookup"><span data-stu-id="24721-128">It constructs the ID for the hybrid connection, and subscribes to an event grid topic.</span></span> <span data-ttu-id="24721-129">The script sets the endpoint type to `hybridconnection` and uses the hybrid connection ID for the endpoint.</span><span class="sxs-lookup"><span data-stu-id="24721-129">The script sets the endpoint type to `hybridconnection` and uses the hybrid connection ID for the endpoint.</span></span>

```azurecli-interactive
relayname=<namespace-name>
relayrg=<resource-group-for-relay>
hybridname=<hybrid-name>

relayid=$(az resource show --name $relayname --resource-group $relayrg --resource-type Microsoft.Relay/namespaces --query id --output tsv)
hybridid="$relayid/hybridConnections/$hybridname"

az eventgrid event-subscription create \
  --topic-name <topic_name> \
  -g gridResourceGroup \
  --name <event_subscription_name> \
  --endpoint-type hybridconnection \
  --endpoint $hybridid
```

## <a name="create-application-to-process-events"></a><span data-ttu-id="24721-130">Create application to process events</span><span class="sxs-lookup"><span data-stu-id="24721-130">Create application to process events</span></span>

<span data-ttu-id="24721-131">You need an application that can retrieve events from the hybrid connection.</span><span class="sxs-lookup"><span data-stu-id="24721-131">You need an application that can retrieve events from the hybrid connection.</span></span> <span data-ttu-id="24721-132">The [Microsoft Azure Event Grid Hybrid Connection Consumer sample for C#](https://github.com/Azure-Samples/event-grid-dotnet-hybridconnection-destination) performs that operation.</span><span class="sxs-lookup"><span data-stu-id="24721-132">The [Microsoft Azure Event Grid Hybrid Connection Consumer sample for C#](https://github.com/Azure-Samples/event-grid-dotnet-hybridconnection-destination) performs that operation.</span></span> <span data-ttu-id="24721-133">You've already finished the prerequisite steps.</span><span class="sxs-lookup"><span data-stu-id="24721-133">You've already finished the prerequisite steps.</span></span>

1. <span data-ttu-id="24721-134">Make sure you have Visual Studio 2017 Version 15.5 or later.</span><span class="sxs-lookup"><span data-stu-id="24721-134">Make sure you have Visual Studio 2017 Version 15.5 or later.</span></span>

1. <span data-ttu-id="24721-135">Clone the repository to your local machine.</span><span class="sxs-lookup"><span data-stu-id="24721-135">Clone the repository to your local machine.</span></span>

1. <span data-ttu-id="24721-136">Load HybridConnectionConsumer project in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="24721-136">Load HybridConnectionConsumer project in Visual Studio.</span></span>

1. <span data-ttu-id="24721-137">In Program.cs, replace `<relayConnectionString>` and `<hybridConnectionName>` with the relay connection string and hybrid connection name that you created.</span><span class="sxs-lookup"><span data-stu-id="24721-137">In Program.cs, replace `<relayConnectionString>` and `<hybridConnectionName>` with the relay connection string and hybrid connection name that you created.</span></span>

1. <span data-ttu-id="24721-138">Compile and run the application from Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="24721-138">Compile and run the application from Visual Studio.</span></span>

## <a name="send-an-event-to-your-topic"></a><span data-ttu-id="24721-139">Send an event to your topic</span><span class="sxs-lookup"><span data-stu-id="24721-139">Send an event to your topic</span></span>

<span data-ttu-id="24721-140">Let's trigger an event to see how Event Grid distributes the message to your endpoint.</span><span class="sxs-lookup"><span data-stu-id="24721-140">Let's trigger an event to see how Event Grid distributes the message to your endpoint.</span></span> <span data-ttu-id="24721-141">This article shows how to use Azure CLI to trigger the event.</span><span class="sxs-lookup"><span data-stu-id="24721-141">This article shows how to use Azure CLI to trigger the event.</span></span> <span data-ttu-id="24721-142">Alternatively, you can use [Event Grid publisher application](https://github.com/Azure-Samples/event-grid-dotnet-publish-consume-events/tree/master/EventGridPublisher).</span><span class="sxs-lookup"><span data-stu-id="24721-142">Alternatively, you can use [Event Grid publisher application](https://github.com/Azure-Samples/event-grid-dotnet-publish-consume-events/tree/master/EventGridPublisher).</span></span>

<span data-ttu-id="24721-143">First, let's get the URL and key for the custom topic.</span><span class="sxs-lookup"><span data-stu-id="24721-143">First, let's get the URL and key for the custom topic.</span></span> <span data-ttu-id="24721-144">Again, use your topic name for `<topic_name>`.</span><span class="sxs-lookup"><span data-stu-id="24721-144">Again, use your topic name for `<topic_name>`.</span></span>

```azurecli-interactive
endpoint=$(az eventgrid topic show --name <topic_name> -g gridResourceGroup --query "endpoint" --output tsv)
key=$(az eventgrid topic key list --name <topic_name> -g gridResourceGroup --query "key1" --output tsv)
```

<span data-ttu-id="24721-145">To simplify this article, you use sample event data to send to the topic.</span><span class="sxs-lookup"><span data-stu-id="24721-145">To simplify this article, you use sample event data to send to the topic.</span></span> <span data-ttu-id="24721-146">Typically, an application or Azure service would send the event data.</span><span class="sxs-lookup"><span data-stu-id="24721-146">Typically, an application or Azure service would send the event data.</span></span> <span data-ttu-id="24721-147">CURL is a utility that sends HTTP requests.</span><span class="sxs-lookup"><span data-stu-id="24721-147">CURL is a utility that sends HTTP requests.</span></span> <span data-ttu-id="24721-148">In this article, use CURL to send the event to the topic.</span><span class="sxs-lookup"><span data-stu-id="24721-148">In this article, use CURL to send the event to the topic.</span></span>  <span data-ttu-id="24721-149">The following example sends three events to the event grid topic:</span><span class="sxs-lookup"><span data-stu-id="24721-149">The following example sends three events to the event grid topic:</span></span>

```azurecli-interactive
body=$(eval echo "'$(curl https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/event-grid/customevent.json)'")
curl -X POST -H "aeg-sas-key: $key" -d "$body" $endpoint
```

<span data-ttu-id="24721-150">Your listener application should receive the event message.</span><span class="sxs-lookup"><span data-stu-id="24721-150">Your listener application should receive the event message.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="24721-151">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="24721-151">Clean up resources</span></span>
<span data-ttu-id="24721-152">If you plan to continue working with this event, don't clean up the resources created in this article.</span><span class="sxs-lookup"><span data-stu-id="24721-152">If you plan to continue working with this event, don't clean up the resources created in this article.</span></span> <span data-ttu-id="24721-153">Otherwise, use the following command to delete the resources you created in this article.</span><span class="sxs-lookup"><span data-stu-id="24721-153">Otherwise, use the following command to delete the resources you created in this article.</span></span>

```azurecli-interactive
az group delete --name gridResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="24721-154">Next steps</span><span class="sxs-lookup"><span data-stu-id="24721-154">Next steps</span></span>

<span data-ttu-id="24721-155">Now that you know how to create topics and event subscriptions, learn more about what Event Grid can help you do:</span><span class="sxs-lookup"><span data-stu-id="24721-155">Now that you know how to create topics and event subscriptions, learn more about what Event Grid can help you do:</span></span>

- [<span data-ttu-id="24721-156">About Event Grid</span><span class="sxs-lookup"><span data-stu-id="24721-156">About Event Grid</span></span>](overview.md)
- [<span data-ttu-id="24721-157">Route Blob storage events to a custom web endpoint</span><span class="sxs-lookup"><span data-stu-id="24721-157">Route Blob storage events to a custom web endpoint</span></span>](../storage/blobs/storage-blob-event-quickstart.md?toc=%2fazure%2fevent-grid%2ftoc.json)
- [<span data-ttu-id="24721-158">Monitor virtual machine changes with Azure Event Grid and Logic Apps</span><span class="sxs-lookup"><span data-stu-id="24721-158">Monitor virtual machine changes with Azure Event Grid and Logic Apps</span></span>](monitor-virtual-machine-changes-event-grid-logic-app.md)
- [<span data-ttu-id="24721-159">Stream big data into a data warehouse</span><span class="sxs-lookup"><span data-stu-id="24721-159">Stream big data into a data warehouse</span></span>](event-grid-event-hubs-integration.md)
