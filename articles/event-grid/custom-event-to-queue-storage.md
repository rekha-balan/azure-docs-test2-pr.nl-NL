---
title: Send custom events for Azure Event Grid to storage queue | Microsoft Docs
description: Use Azure Event Grid and Azure CLI to publish a topic, and subscribe to that event. A storage queue is used for the endpoint.
services: event-grid
keywords: ''
author: tfitzmac
ms.author: tomfitz
ms.date: 07/05/2018
ms.topic: quickstart
ms.service: event-grid
ms.openlocfilehash: d550812f9cb23fd17d3c73c851a306190be293fa
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868329"
---
# <a name="route-custom-events-to-azure-queue-storage-with-azure-cli-and-event-grid"></a><span data-ttu-id="c5c4c-104">Route custom events to Azure Queue storage with Azure CLI and Event Grid</span><span class="sxs-lookup"><span data-stu-id="c5c4c-104">Route custom events to Azure Queue storage with Azure CLI and Event Grid</span></span>

<span data-ttu-id="c5c4c-105">Azure Event Grid is an eventing service for the cloud.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-105">Azure Event Grid is an eventing service for the cloud.</span></span> <span data-ttu-id="c5c4c-106">Azure Queue storage is one of the supported event handlers.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-106">Azure Queue storage is one of the supported event handlers.</span></span> <span data-ttu-id="c5c4c-107">In this article, you use the Azure CLI to create a custom topic, subscribe to the topic, and trigger the event to view the result.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-107">In this article, you use the Azure CLI to create a custom topic, subscribe to the topic, and trigger the event to view the result.</span></span> <span data-ttu-id="c5c4c-108">You send the events to the Queue storage.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-108">You send the events to the Queue storage.</span></span>

[!INCLUDE [quickstarts-free-trial-note.md](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [event-grid-preview-feature-note.md](../../includes/event-grid-preview-feature-note.md)]

## <a name="create-a-resource-group"></a><span data-ttu-id="c5c4c-109">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="c5c4c-109">Create a resource group</span></span>

<span data-ttu-id="c5c4c-110">Event Grid topics are Azure resources, and must be placed in an Azure resource group.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-110">Event Grid topics are Azure resources, and must be placed in an Azure resource group.</span></span> <span data-ttu-id="c5c4c-111">The resource group is a logical collection into which Azure resources are deployed and managed.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-111">The resource group is a logical collection into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="c5c4c-112">Create a resource group with the [az group create](/cli/azure/group#az-group-create) command.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-112">Create a resource group with the [az group create](/cli/azure/group#az-group-create) command.</span></span> 

<span data-ttu-id="c5c4c-113">The following example creates a resource group named *gridResourceGroup* in the *westus2* location.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-113">The following example creates a resource group named *gridResourceGroup* in the *westus2* location.</span></span>

```azurecli-interactive
az group create --name gridResourceGroup --location westus2
```

[!INCLUDE [event-grid-register-provider-cli.md](../../includes/event-grid-register-provider-cli.md)]

## <a name="create-a-custom-topic"></a><span data-ttu-id="c5c4c-114">Create a custom topic</span><span class="sxs-lookup"><span data-stu-id="c5c4c-114">Create a custom topic</span></span>

<span data-ttu-id="c5c4c-115">An event grid topic provides a user-defined endpoint that you post your events to.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-115">An event grid topic provides a user-defined endpoint that you post your events to.</span></span> <span data-ttu-id="c5c4c-116">The following example creates the custom topic in your resource group.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-116">The following example creates the custom topic in your resource group.</span></span> <span data-ttu-id="c5c4c-117">Replace `<topic_name>` with a unique name for your topic.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-117">Replace `<topic_name>` with a unique name for your topic.</span></span> <span data-ttu-id="c5c4c-118">The topic name must be unique because it is represented by a DNS entry.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-118">The topic name must be unique because it is represented by a DNS entry.</span></span>

```azurecli-interactive
# if you have not already installed the extension, do it now.
# This extension is required for preview features.
az extension add --name eventgrid

az eventgrid topic create --name <topic_name> -l westus2 -g gridResourceGroup
```

## <a name="create-queue-storage"></a><span data-ttu-id="c5c4c-119">Create Queue storage</span><span class="sxs-lookup"><span data-stu-id="c5c4c-119">Create Queue storage</span></span>

<span data-ttu-id="c5c4c-120">Before subscribing to the topic, let's create the endpoint for the event message.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-120">Before subscribing to the topic, let's create the endpoint for the event message.</span></span> <span data-ttu-id="c5c4c-121">You create a Queue storage for collecting the events.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-121">You create a Queue storage for collecting the events.</span></span>

```azurecli-interactive
storagename="<unique-storage-name>"
queuename="eventqueue"

az storage account create -n $storagename -g gridResourceGroup -l westus2 --sku Standard_LRS
az storage queue create --name $queuename --account-name $storagename
```

## <a name="subscribe-to-a-topic"></a><span data-ttu-id="c5c4c-122">Subscribe to a topic</span><span class="sxs-lookup"><span data-stu-id="c5c4c-122">Subscribe to a topic</span></span>

<span data-ttu-id="c5c4c-123">You subscribe to a topic to tell Event Grid which events you want to track. The following example subscribes to the topic you created, and passes the resource ID of the Queue storage for the endpoint.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-123">You subscribe to a topic to tell Event Grid which events you want to track. The following example subscribes to the topic you created, and passes the resource ID of the Queue storage for the endpoint.</span></span> <span data-ttu-id="c5c4c-124">With Azure CLI, you pass the Queue storage ID as the endpoint.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-124">With Azure CLI, you pass the Queue storage ID as the endpoint.</span></span> <span data-ttu-id="c5c4c-125">The endpoint is in the format:</span><span class="sxs-lookup"><span data-stu-id="c5c4c-125">The endpoint is in the format:</span></span>

`/subscriptions/<subscription-id>/resourcegroups/<resource-group-name>/providers/Microsoft.Storage/storageAccounts/<storage-name>/queueservices/default/queues/<queue-name>`

<span data-ttu-id="c5c4c-126">The following script gets the resource ID of the storage account for the queue.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-126">The following script gets the resource ID of the storage account for the queue.</span></span> <span data-ttu-id="c5c4c-127">It constructs the ID for the queue storage, and subscribes to an event grid topic.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-127">It constructs the ID for the queue storage, and subscribes to an event grid topic.</span></span> <span data-ttu-id="c5c4c-128">It sets the endpoint type to `storagequeue` and uses the queue ID for the endpoint.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-128">It sets the endpoint type to `storagequeue` and uses the queue ID for the endpoint.</span></span>

```azurecli-interactive
storageid=$(az storage account show --name $storagename --resource-group gridResourceGroup --query id --output tsv)
queueid="$storageid/queueservices/default/queues/$queuename"

az eventgrid event-subscription create \
  --topic-name <topic_name> \
  -g gridResourceGroup \
  --name <event_subscription_name> \
  --endpoint-type storagequeue \
  --endpoint $queueid
```

<span data-ttu-id="c5c4c-129">If you use the REST API to create the subscription, you pass the ID of the storage account and the name of the queue as a separate parameter.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-129">If you use the REST API to create the subscription, you pass the ID of the storage account and the name of the queue as a separate parameter.</span></span>

```json
"destination": {
  "endpointType": "storagequeue",
  "properties": {
    "queueName":"eventqueue",
    "resourceId": "/subscriptions/<subscription-id>/resourcegroups/<resource-group-name>/providers/Microsoft.Storage/storageAccounts/<storage-name>"
  }
  ...
```

## <a name="send-an-event-to-your-topic"></a><span data-ttu-id="c5c4c-130">Send an event to your topic</span><span class="sxs-lookup"><span data-stu-id="c5c4c-130">Send an event to your topic</span></span>

<span data-ttu-id="c5c4c-131">Let's trigger an event to see how Event Grid distributes the message to your endpoint.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-131">Let's trigger an event to see how Event Grid distributes the message to your endpoint.</span></span> <span data-ttu-id="c5c4c-132">First, let's get the URL and key for the custom topic.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-132">First, let's get the URL and key for the custom topic.</span></span> <span data-ttu-id="c5c4c-133">Again, use your topic name for `<topic_name>`.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-133">Again, use your topic name for `<topic_name>`.</span></span>

```azurecli-interactive
endpoint=$(az eventgrid topic show --name <topic_name> -g gridResourceGroup --query "endpoint" --output tsv)
key=$(az eventgrid topic key list --name <topic_name> -g gridResourceGroup --query "key1" --output tsv)
```

<span data-ttu-id="c5c4c-134">To simplify this article, you use sample event data to send to the topic.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-134">To simplify this article, you use sample event data to send to the topic.</span></span> <span data-ttu-id="c5c4c-135">Typically, an application or Azure service would send the event data.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-135">Typically, an application or Azure service would send the event data.</span></span> <span data-ttu-id="c5c4c-136">CURL is a utility that sends HTTP requests.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-136">CURL is a utility that sends HTTP requests.</span></span> <span data-ttu-id="c5c4c-137">In this article, use CURL to send the event to the topic.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-137">In this article, use CURL to send the event to the topic.</span></span>  <span data-ttu-id="c5c4c-138">The following example sends three events to the event grid topic:</span><span class="sxs-lookup"><span data-stu-id="c5c4c-138">The following example sends three events to the event grid topic:</span></span>

```azurecli-interactive
for i in 1 2 3
do
   body=$(eval echo "'$(curl https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/event-grid/customevent.json)'")
   curl -X POST -H "aeg-sas-key: $key" -d "$body" $endpoint
done
```

<span data-ttu-id="c5c4c-139">Navigate to the Queue storage in the portal, and notice that Event Grid sent those three events to the queue.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-139">Navigate to the Queue storage in the portal, and notice that Event Grid sent those three events to the queue.</span></span>

![Show messages](./media/custom-event-to-queue-storage/messages.png)


## <a name="clean-up-resources"></a><span data-ttu-id="c5c4c-141">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="c5c4c-141">Clean up resources</span></span>
<span data-ttu-id="c5c4c-142">If you plan to continue working with this event, don't clean up the resources created in this article.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-142">If you plan to continue working with this event, don't clean up the resources created in this article.</span></span> <span data-ttu-id="c5c4c-143">Otherwise, use the following command to delete the resources you created in this article.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-143">Otherwise, use the following command to delete the resources you created in this article.</span></span>

```azurecli-interactive
az group delete --name gridResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="c5c4c-144">Next steps</span><span class="sxs-lookup"><span data-stu-id="c5c4c-144">Next steps</span></span>

<span data-ttu-id="c5c4c-145">Now that you know how to create topics and event subscriptions, learn more about what Event Grid can help you do:</span><span class="sxs-lookup"><span data-stu-id="c5c4c-145">Now that you know how to create topics and event subscriptions, learn more about what Event Grid can help you do:</span></span>

- [<span data-ttu-id="c5c4c-146">About Event Grid</span><span class="sxs-lookup"><span data-stu-id="c5c4c-146">About Event Grid</span></span>](overview.md)
- [<span data-ttu-id="c5c4c-147">Route Blob storage events to a custom web endpoint</span><span class="sxs-lookup"><span data-stu-id="c5c4c-147">Route Blob storage events to a custom web endpoint</span></span>](../storage/blobs/storage-blob-event-quickstart.md?toc=%2fazure%2fevent-grid%2ftoc.json)
- [<span data-ttu-id="c5c4c-148">Monitor virtual machine changes with Azure Event Grid and Logic Apps</span><span class="sxs-lookup"><span data-stu-id="c5c4c-148">Monitor virtual machine changes with Azure Event Grid and Logic Apps</span></span>](monitor-virtual-machine-changes-event-grid-logic-app.md)
- [<span data-ttu-id="c5c4c-149">Stream big data into a data warehouse</span><span class="sxs-lookup"><span data-stu-id="c5c4c-149">Stream big data into a data warehouse</span></span>](event-grid-event-hubs-integration.md)
