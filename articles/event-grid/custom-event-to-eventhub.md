---
title: Send custom events for Azure Event Grid to Event Hubs | Microsoft Docs
description: Use Azure Event Grid and Azure CLI to publish a topic, and subscribe to that event. An event hub is used for the endpoint.
services: event-grid
keywords: ''
author: tfitzmac
ms.author: tomfitz
ms.date: 07/05/2018
ms.topic: quickstart
ms.service: event-grid
ms.openlocfilehash: b5be37ede208ba14fbfe8270bff317a782bf655a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869643"
---
# <a name="route-custom-events-to-azure-event-hubs-with-azure-cli-and-event-grid"></a><span data-ttu-id="690d0-104">Route custom events to Azure Event Hubs with Azure CLI and Event Grid</span><span class="sxs-lookup"><span data-stu-id="690d0-104">Route custom events to Azure Event Hubs with Azure CLI and Event Grid</span></span>

<span data-ttu-id="690d0-105">Azure Event Grid is an eventing service for the cloud.</span><span class="sxs-lookup"><span data-stu-id="690d0-105">Azure Event Grid is an eventing service for the cloud.</span></span> <span data-ttu-id="690d0-106">Azure Event Hubs is one of the supported event handlers.</span><span class="sxs-lookup"><span data-stu-id="690d0-106">Azure Event Hubs is one of the supported event handlers.</span></span> <span data-ttu-id="690d0-107">In this article, you use the Azure CLI to create a custom topic, subscribe to the topic, and trigger the event to view the result.</span><span class="sxs-lookup"><span data-stu-id="690d0-107">In this article, you use the Azure CLI to create a custom topic, subscribe to the topic, and trigger the event to view the result.</span></span> <span data-ttu-id="690d0-108">You send the events to an event hub.</span><span class="sxs-lookup"><span data-stu-id="690d0-108">You send the events to an event hub.</span></span>

[!INCLUDE [quickstarts-free-trial-note.md](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-resource-group"></a><span data-ttu-id="690d0-109">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="690d0-109">Create a resource group</span></span>

<span data-ttu-id="690d0-110">Event Grid topics are Azure resources, and must be placed in an Azure resource group.</span><span class="sxs-lookup"><span data-stu-id="690d0-110">Event Grid topics are Azure resources, and must be placed in an Azure resource group.</span></span> <span data-ttu-id="690d0-111">The resource group is a logical collection into which Azure resources are deployed and managed.</span><span class="sxs-lookup"><span data-stu-id="690d0-111">The resource group is a logical collection into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="690d0-112">Create a resource group with the [az group create](/cli/azure/group#az-group-create) command.</span><span class="sxs-lookup"><span data-stu-id="690d0-112">Create a resource group with the [az group create](/cli/azure/group#az-group-create) command.</span></span> 

<span data-ttu-id="690d0-113">The following example creates a resource group named *gridResourceGroup* in the *westus2* location.</span><span class="sxs-lookup"><span data-stu-id="690d0-113">The following example creates a resource group named *gridResourceGroup* in the *westus2* location.</span></span>

```azurecli-interactive
az group create --name gridResourceGroup --location westus2
```

[!INCLUDE [event-grid-register-provider-cli.md](../../includes/event-grid-register-provider-cli.md)]

## <a name="create-a-custom-topic"></a><span data-ttu-id="690d0-114">Create a Custom Topic</span><span class="sxs-lookup"><span data-stu-id="690d0-114">Create a Custom Topic</span></span>

<span data-ttu-id="690d0-115">An event grid topic provides a user-defined endpoint that you post your events to.</span><span class="sxs-lookup"><span data-stu-id="690d0-115">An event grid topic provides a user-defined endpoint that you post your events to.</span></span> <span data-ttu-id="690d0-116">The following example creates the custom topic in your resource group.</span><span class="sxs-lookup"><span data-stu-id="690d0-116">The following example creates the custom topic in your resource group.</span></span> <span data-ttu-id="690d0-117">Replace `<your-topic-name>` with a unique name for your topic.</span><span class="sxs-lookup"><span data-stu-id="690d0-117">Replace `<your-topic-name>` with a unique name for your topic.</span></span> <span data-ttu-id="690d0-118">The topic name must be unique because it's represented by a DNS entry.</span><span class="sxs-lookup"><span data-stu-id="690d0-118">The topic name must be unique because it's represented by a DNS entry.</span></span>

```azurecli-interactive
topicname=<your-topic-name>
az eventgrid topic create --name $topicname -l westus2 -g gridResourceGroup
```

## <a name="create-event-hub"></a><span data-ttu-id="690d0-119">Create event hub</span><span class="sxs-lookup"><span data-stu-id="690d0-119">Create event hub</span></span>

<span data-ttu-id="690d0-120">Before subscribing to the topic, let's create the endpoint for the event message.</span><span class="sxs-lookup"><span data-stu-id="690d0-120">Before subscribing to the topic, let's create the endpoint for the event message.</span></span> <span data-ttu-id="690d0-121">You create an event hub for collecting the events.</span><span class="sxs-lookup"><span data-stu-id="690d0-121">You create an event hub for collecting the events.</span></span>

```azurecli-interactive
namespace=<unique-namespace-name>
hubname=demohub

az eventhubs namespace create --name $namespace --resource-group gridResourceGroup
az eventhubs eventhub create --name $hubname --namespace-name $namespace --resource-group gridResourceGroup
```

## <a name="subscribe-to-a-topic"></a><span data-ttu-id="690d0-122">Subscribe to a topic</span><span class="sxs-lookup"><span data-stu-id="690d0-122">Subscribe to a topic</span></span>

<span data-ttu-id="690d0-123">You subscribe to a topic to tell Event Grid which events you want to track. The following example subscribes to the topic you created, and passes the resource ID of the event hub for the endpoint.</span><span class="sxs-lookup"><span data-stu-id="690d0-123">You subscribe to a topic to tell Event Grid which events you want to track. The following example subscribes to the topic you created, and passes the resource ID of the event hub for the endpoint.</span></span> <span data-ttu-id="690d0-124">The endpoint is in the format:</span><span class="sxs-lookup"><span data-stu-id="690d0-124">The endpoint is in the format:</span></span>

`/subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.EventHub/namespaces/<namespace-name>/eventhubs/<hub-name>`

<span data-ttu-id="690d0-125">The following script gets the resource ID for the event hub, and subscribes to an event grid topic.</span><span class="sxs-lookup"><span data-stu-id="690d0-125">The following script gets the resource ID for the event hub, and subscribes to an event grid topic.</span></span> <span data-ttu-id="690d0-126">It sets the endpoint type to `eventhub` and uses the event hub ID for the endpoint.</span><span class="sxs-lookup"><span data-stu-id="690d0-126">It sets the endpoint type to `eventhub` and uses the event hub ID for the endpoint.</span></span>

```azurecli-interactive
hubid=$(az eventhubs eventhub show --name $hubname --namespace-name $namespace --resource-group gridResourceGroup --query id --output tsv)

az eventgrid event-subscription create \
  --topic-name $topicname \
  -g gridResourceGroup \
  --name subtoeventhub \
  --endpoint-type eventhub \
  --endpoint $hubid
```

## <a name="send-an-event-to-your-topic"></a><span data-ttu-id="690d0-127">Send an event to your topic</span><span class="sxs-lookup"><span data-stu-id="690d0-127">Send an event to your topic</span></span>

<span data-ttu-id="690d0-128">Let's trigger an event to see how Event Grid distributes the message to your endpoint.</span><span class="sxs-lookup"><span data-stu-id="690d0-128">Let's trigger an event to see how Event Grid distributes the message to your endpoint.</span></span> <span data-ttu-id="690d0-129">First, let's get the URL and key for the custom topic.</span><span class="sxs-lookup"><span data-stu-id="690d0-129">First, let's get the URL and key for the custom topic.</span></span>

```azurecli-interactive
endpoint=$(az eventgrid topic show --name $topicname -g gridResourceGroup --query "endpoint" --output tsv)
key=$(az eventgrid topic key list --name $topicname -g gridResourceGroup --query "key1" --output tsv)
```

<span data-ttu-id="690d0-130">To simplify this article, you use sample event data to send to the topic.</span><span class="sxs-lookup"><span data-stu-id="690d0-130">To simplify this article, you use sample event data to send to the topic.</span></span> <span data-ttu-id="690d0-131">Typically, an application or Azure service would send the event data.</span><span class="sxs-lookup"><span data-stu-id="690d0-131">Typically, an application or Azure service would send the event data.</span></span> <span data-ttu-id="690d0-132">CURL is a utility that sends HTTP requests.</span><span class="sxs-lookup"><span data-stu-id="690d0-132">CURL is a utility that sends HTTP requests.</span></span> <span data-ttu-id="690d0-133">In this article, use CURL to send the event to the topic.</span><span class="sxs-lookup"><span data-stu-id="690d0-133">In this article, use CURL to send the event to the topic.</span></span>  <span data-ttu-id="690d0-134">The following example sends three events to the event grid topic:</span><span class="sxs-lookup"><span data-stu-id="690d0-134">The following example sends three events to the event grid topic:</span></span>

```azurecli-interactive
for i in 1 2 3
do
   body=$(eval echo "'$(curl https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/event-grid/customevent.json)'")
   curl -X POST -H "aeg-sas-key: $key" -d "$body" $endpoint
done
```

<span data-ttu-id="690d0-135">Navigate to the event hub in the portal, and notice that Event Grid sent those three events to the event hub.</span><span class="sxs-lookup"><span data-stu-id="690d0-135">Navigate to the event hub in the portal, and notice that Event Grid sent those three events to the event hub.</span></span>

![Show messages](./media/custom-event-to-eventhub/show-result.png)

<span data-ttu-id="690d0-137">Typically, you create an application that retrieves the events from the event hub.</span><span class="sxs-lookup"><span data-stu-id="690d0-137">Typically, you create an application that retrieves the events from the event hub.</span></span> <span data-ttu-id="690d0-138">To create an application that gets messages from an event hub, see:</span><span class="sxs-lookup"><span data-stu-id="690d0-138">To create an application that gets messages from an event hub, see:</span></span>

* [<span data-ttu-id="690d0-139">Get started receiving messages with the Event Processor Host in .NET Standard</span><span class="sxs-lookup"><span data-stu-id="690d0-139">Get started receiving messages with the Event Processor Host in .NET Standard</span></span>](../event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph.md)
* [<span data-ttu-id="690d0-140">Receive events from Azure Event Hubs using Java</span><span class="sxs-lookup"><span data-stu-id="690d0-140">Receive events from Azure Event Hubs using Java</span></span>](../event-hubs/event-hubs-java-get-started-receive-eph.md)
* [<span data-ttu-id="690d0-141">Receive events from Event Hubs using Apache Storm</span><span class="sxs-lookup"><span data-stu-id="690d0-141">Receive events from Event Hubs using Apache Storm</span></span>](../event-hubs/event-hubs-storm-getstarted-receive.md)

## <a name="clean-up-resources"></a><span data-ttu-id="690d0-142">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="690d0-142">Clean up resources</span></span>
<span data-ttu-id="690d0-143">If you plan to continue working with this event, don't clean up the resources created in this article.</span><span class="sxs-lookup"><span data-stu-id="690d0-143">If you plan to continue working with this event, don't clean up the resources created in this article.</span></span> <span data-ttu-id="690d0-144">Otherwise, use the following command to delete the resources you created in this article.</span><span class="sxs-lookup"><span data-stu-id="690d0-144">Otherwise, use the following command to delete the resources you created in this article.</span></span>

```azurecli-interactive
az group delete --name gridResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="690d0-145">Next steps</span><span class="sxs-lookup"><span data-stu-id="690d0-145">Next steps</span></span>

<span data-ttu-id="690d0-146">Now that you know how to create topics and event subscriptions, learn more about what Event Grid can help you do:</span><span class="sxs-lookup"><span data-stu-id="690d0-146">Now that you know how to create topics and event subscriptions, learn more about what Event Grid can help you do:</span></span>

- [<span data-ttu-id="690d0-147">About Event Grid</span><span class="sxs-lookup"><span data-stu-id="690d0-147">About Event Grid</span></span>](overview.md)
- [<span data-ttu-id="690d0-148">Route Blob storage events to a custom web endpoint</span><span class="sxs-lookup"><span data-stu-id="690d0-148">Route Blob storage events to a custom web endpoint</span></span>](../storage/blobs/storage-blob-event-quickstart.md?toc=%2fazure%2fevent-grid%2ftoc.json)
- [<span data-ttu-id="690d0-149">Monitor virtual machine changes with Azure Event Grid and Logic Apps</span><span class="sxs-lookup"><span data-stu-id="690d0-149">Monitor virtual machine changes with Azure Event Grid and Logic Apps</span></span>](monitor-virtual-machine-changes-event-grid-logic-app.md)
- [<span data-ttu-id="690d0-150">Stream big data into a data warehouse</span><span class="sxs-lookup"><span data-stu-id="690d0-150">Stream big data into a data warehouse</span></span>](event-grid-event-hubs-integration.md)
