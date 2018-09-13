---
title: Custom events for Azure Event Grid with CLI | Microsoft Docs
description: Use Azure Event Grid and Azure CLI to publish a topic, and subscribe to that event.
services: event-grid
keywords: ''
author: tfitzmac
ms.author: tomfitz
ms.date: 08/23/2018
ms.topic: quickstart
ms.service: event-grid
ms.openlocfilehash: 5d980e480c6a730ad66dfaee56459c8bb36605e8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968915"
---
# <a name="create-and-route-custom-events-with-azure-cli-and-event-grid"></a><span data-ttu-id="d1a06-103">Create and route custom events with Azure CLI and Event Grid</span><span class="sxs-lookup"><span data-stu-id="d1a06-103">Create and route custom events with Azure CLI and Event Grid</span></span>

<span data-ttu-id="d1a06-104">Azure Event Grid is an eventing service for the cloud.</span><span class="sxs-lookup"><span data-stu-id="d1a06-104">Azure Event Grid is an eventing service for the cloud.</span></span> <span data-ttu-id="d1a06-105">In this article, you use the Azure CLI to create a custom topic, subscribe to the topic, and trigger the event to view the result.</span><span class="sxs-lookup"><span data-stu-id="d1a06-105">In this article, you use the Azure CLI to create a custom topic, subscribe to the topic, and trigger the event to view the result.</span></span> <span data-ttu-id="d1a06-106">Typically, you send events to an endpoint that processes the event data and takes actions.</span><span class="sxs-lookup"><span data-stu-id="d1a06-106">Typically, you send events to an endpoint that processes the event data and takes actions.</span></span> <span data-ttu-id="d1a06-107">However, to simplify this article, you send the events to a web app that collects and displays the messages.</span><span class="sxs-lookup"><span data-stu-id="d1a06-107">However, to simplify this article, you send the events to a web app that collects and displays the messages.</span></span>

<span data-ttu-id="d1a06-108">When you're finished, you see that the event data has been sent to the web app.</span><span class="sxs-lookup"><span data-stu-id="d1a06-108">When you're finished, you see that the event data has been sent to the web app.</span></span>

![View results](./media/custom-event-quickstart/view-result.png)

[!INCLUDE [quickstarts-free-trial-note.md](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="d1a06-110">If you choose to install and use the CLI locally, this article requires that you are running the latest version of Azure CLI (2.0.24 or later).</span><span class="sxs-lookup"><span data-stu-id="d1a06-110">If you choose to install and use the CLI locally, this article requires that you are running the latest version of Azure CLI (2.0.24 or later).</span></span> <span data-ttu-id="d1a06-111">To find the version, run `az --version`.</span><span class="sxs-lookup"><span data-stu-id="d1a06-111">To find the version, run `az --version`.</span></span> <span data-ttu-id="d1a06-112">If you need to install or upgrade, see [Install Azure CLI](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="d1a06-112">If you need to install or upgrade, see [Install Azure CLI](/cli/azure/install-azure-cli).</span></span>

<span data-ttu-id="d1a06-113">If you aren't using Cloud Shell, you must first sign in using `az login`.</span><span class="sxs-lookup"><span data-stu-id="d1a06-113">If you aren't using Cloud Shell, you must first sign in using `az login`.</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="d1a06-114">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="d1a06-114">Create a resource group</span></span>

<span data-ttu-id="d1a06-115">Event Grid topics are Azure resources, and must be placed in an Azure resource group.</span><span class="sxs-lookup"><span data-stu-id="d1a06-115">Event Grid topics are Azure resources, and must be placed in an Azure resource group.</span></span> <span data-ttu-id="d1a06-116">The resource group is a logical collection into which Azure resources are deployed and managed.</span><span class="sxs-lookup"><span data-stu-id="d1a06-116">The resource group is a logical collection into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="d1a06-117">Create a resource group with the [az group create](/cli/azure/group#az-group-create) command.</span><span class="sxs-lookup"><span data-stu-id="d1a06-117">Create a resource group with the [az group create](/cli/azure/group#az-group-create) command.</span></span> 

<span data-ttu-id="d1a06-118">The following example creates a resource group named *gridResourceGroup* in the *westus2* location.</span><span class="sxs-lookup"><span data-stu-id="d1a06-118">The following example creates a resource group named *gridResourceGroup* in the *westus2* location.</span></span>

```azurecli-interactive
az group create --name gridResourceGroup --location westus2
```

[!INCLUDE [event-grid-register-provider-cli.md](../../includes/event-grid-register-provider-cli.md)]

## <a name="create-a-custom-topic"></a><span data-ttu-id="d1a06-119">Create a custom topic</span><span class="sxs-lookup"><span data-stu-id="d1a06-119">Create a custom topic</span></span>

<span data-ttu-id="d1a06-120">An event grid topic provides a user-defined endpoint that you post your events to.</span><span class="sxs-lookup"><span data-stu-id="d1a06-120">An event grid topic provides a user-defined endpoint that you post your events to.</span></span> <span data-ttu-id="d1a06-121">The following example creates the custom topic in your resource group.</span><span class="sxs-lookup"><span data-stu-id="d1a06-121">The following example creates the custom topic in your resource group.</span></span> <span data-ttu-id="d1a06-122">Replace `<your-topic-name>` with a unique name for your topic.</span><span class="sxs-lookup"><span data-stu-id="d1a06-122">Replace `<your-topic-name>` with a unique name for your topic.</span></span> <span data-ttu-id="d1a06-123">The topic name must be unique because it's part of the DNS entry.</span><span class="sxs-lookup"><span data-stu-id="d1a06-123">The topic name must be unique because it's part of the DNS entry.</span></span>

```azurecli-interactive
topicname=<your-topic-name>

az eventgrid topic create --name $topicname -l westus2 -g gridResourceGroup
```

## <a name="create-a-message-endpoint"></a><span data-ttu-id="d1a06-124">Create a message endpoint</span><span class="sxs-lookup"><span data-stu-id="d1a06-124">Create a message endpoint</span></span>

<span data-ttu-id="d1a06-125">Before subscribing to the topic, let's create the endpoint for the event message.</span><span class="sxs-lookup"><span data-stu-id="d1a06-125">Before subscribing to the topic, let's create the endpoint for the event message.</span></span> <span data-ttu-id="d1a06-126">Typically, the endpoint takes actions based on the event data.</span><span class="sxs-lookup"><span data-stu-id="d1a06-126">Typically, the endpoint takes actions based on the event data.</span></span> <span data-ttu-id="d1a06-127">To simplify this quickstart, you deploy a [pre-built web app](https://github.com/Azure-Samples/azure-event-grid-viewer) that displays the event messages.</span><span class="sxs-lookup"><span data-stu-id="d1a06-127">To simplify this quickstart, you deploy a [pre-built web app](https://github.com/Azure-Samples/azure-event-grid-viewer) that displays the event messages.</span></span> <span data-ttu-id="d1a06-128">The deployed solution includes an App Service plan, an App Service web app, and source code from GitHub.</span><span class="sxs-lookup"><span data-stu-id="d1a06-128">The deployed solution includes an App Service plan, an App Service web app, and source code from GitHub.</span></span>

<span data-ttu-id="d1a06-129">Replace `<your-site-name>` with a unique name for your web app.</span><span class="sxs-lookup"><span data-stu-id="d1a06-129">Replace `<your-site-name>` with a unique name for your web app.</span></span> <span data-ttu-id="d1a06-130">The web app name must be unique because it's part of the DNS entry.</span><span class="sxs-lookup"><span data-stu-id="d1a06-130">The web app name must be unique because it's part of the DNS entry.</span></span>

```azurecli-interactive
sitename=<your-site-name>

az group deployment create \
  --resource-group gridResourceGroup \
  --template-uri "https://raw.githubusercontent.com/Azure-Samples/azure-event-grid-viewer/master/azuredeploy.json" \
  --parameters siteName=$sitename hostingPlanName=viewerhost
```

<span data-ttu-id="d1a06-131">The deployment may take a few minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="d1a06-131">The deployment may take a few minutes to complete.</span></span> <span data-ttu-id="d1a06-132">After the deployment has succeeded, view your web app to make sure it's running.</span><span class="sxs-lookup"><span data-stu-id="d1a06-132">After the deployment has succeeded, view your web app to make sure it's running.</span></span> <span data-ttu-id="d1a06-133">In a web browser, navigate to: `https://<your-site-name>.azurewebsites.net`</span><span class="sxs-lookup"><span data-stu-id="d1a06-133">In a web browser, navigate to: `https://<your-site-name>.azurewebsites.net`</span></span>

<span data-ttu-id="d1a06-134">You should see the site with no messages currently displayed.</span><span class="sxs-lookup"><span data-stu-id="d1a06-134">You should see the site with no messages currently displayed.</span></span>

## <a name="subscribe-to-a-topic"></a><span data-ttu-id="d1a06-135">Subscribe to a topic</span><span class="sxs-lookup"><span data-stu-id="d1a06-135">Subscribe to a topic</span></span>

<span data-ttu-id="d1a06-136">You subscribe to a topic to tell Event Grid which events you want to track and where to send those events.</span><span class="sxs-lookup"><span data-stu-id="d1a06-136">You subscribe to a topic to tell Event Grid which events you want to track and where to send those events.</span></span> <span data-ttu-id="d1a06-137">The following example subscribes to the topic you created, and passes the URL from your web app as the endpoint for event notification.</span><span class="sxs-lookup"><span data-stu-id="d1a06-137">The following example subscribes to the topic you created, and passes the URL from your web app as the endpoint for event notification.</span></span>

<span data-ttu-id="d1a06-138">The endpoint for your web app must include the suffix `/api/updates/`.</span><span class="sxs-lookup"><span data-stu-id="d1a06-138">The endpoint for your web app must include the suffix `/api/updates/`.</span></span>

```azurecli-interactive
endpoint=https://$sitename.azurewebsites.net/api/updates

az eventgrid event-subscription create \
  -g gridResourceGroup \
  --topic-name $topicname \
  --name demoViewerSub \
  --endpoint $endpoint
```

<span data-ttu-id="d1a06-139">View your web app again, and notice that a subscription validation event has been sent to it.</span><span class="sxs-lookup"><span data-stu-id="d1a06-139">View your web app again, and notice that a subscription validation event has been sent to it.</span></span> <span data-ttu-id="d1a06-140">Select the eye icon to expand the event data.</span><span class="sxs-lookup"><span data-stu-id="d1a06-140">Select the eye icon to expand the event data.</span></span> <span data-ttu-id="d1a06-141">Event Grid sends the validation event so the endpoint can verify that it wants to receive event data.</span><span class="sxs-lookup"><span data-stu-id="d1a06-141">Event Grid sends the validation event so the endpoint can verify that it wants to receive event data.</span></span> <span data-ttu-id="d1a06-142">The web app includes code to validate the subscription.</span><span class="sxs-lookup"><span data-stu-id="d1a06-142">The web app includes code to validate the subscription.</span></span>

![View subscription event](./media/custom-event-quickstart/view-subscription-event.png)

## <a name="send-an-event-to-your-topic"></a><span data-ttu-id="d1a06-144">Send an event to your topic</span><span class="sxs-lookup"><span data-stu-id="d1a06-144">Send an event to your topic</span></span>

<span data-ttu-id="d1a06-145">Let's trigger an event to see how Event Grid distributes the message to your endpoint.</span><span class="sxs-lookup"><span data-stu-id="d1a06-145">Let's trigger an event to see how Event Grid distributes the message to your endpoint.</span></span> <span data-ttu-id="d1a06-146">First, let's get the URL and key for the custom topic.</span><span class="sxs-lookup"><span data-stu-id="d1a06-146">First, let's get the URL and key for the custom topic.</span></span>

```azurecli-interactive
endpoint=$(az eventgrid topic show --name $topicname -g gridResourceGroup --query "endpoint" --output tsv)
key=$(az eventgrid topic key list --name $topicname -g gridResourceGroup --query "key1" --output tsv)
```

<span data-ttu-id="d1a06-147">To simplify this article, you use sample event data to send to the topic.</span><span class="sxs-lookup"><span data-stu-id="d1a06-147">To simplify this article, you use sample event data to send to the topic.</span></span> <span data-ttu-id="d1a06-148">Typically, an application or Azure service would send the event data.</span><span class="sxs-lookup"><span data-stu-id="d1a06-148">Typically, an application or Azure service would send the event data.</span></span> <span data-ttu-id="d1a06-149">The following example gets the event data:</span><span class="sxs-lookup"><span data-stu-id="d1a06-149">The following example gets the event data:</span></span>

```azurecli-interactive
body=$(eval echo "'$(curl https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/event-grid/customevent.json)'")
```

<span data-ttu-id="d1a06-150">To see the full event, use `echo "$body"`.</span><span class="sxs-lookup"><span data-stu-id="d1a06-150">To see the full event, use `echo "$body"`.</span></span> <span data-ttu-id="d1a06-151">The `data` element of the JSON is the payload of your event.</span><span class="sxs-lookup"><span data-stu-id="d1a06-151">The `data` element of the JSON is the payload of your event.</span></span> <span data-ttu-id="d1a06-152">Any well-formed JSON can go in this field.</span><span class="sxs-lookup"><span data-stu-id="d1a06-152">Any well-formed JSON can go in this field.</span></span> <span data-ttu-id="d1a06-153">You can also use the subject field for advanced routing and filtering.</span><span class="sxs-lookup"><span data-stu-id="d1a06-153">You can also use the subject field for advanced routing and filtering.</span></span>

<span data-ttu-id="d1a06-154">CURL is a utility that sends HTTP requests.</span><span class="sxs-lookup"><span data-stu-id="d1a06-154">CURL is a utility that sends HTTP requests.</span></span> <span data-ttu-id="d1a06-155">In this article, use CURL to send the event to the topic.</span><span class="sxs-lookup"><span data-stu-id="d1a06-155">In this article, use CURL to send the event to the topic.</span></span> 

```azurecli-interactive
curl -X POST -H "aeg-sas-key: $key" -d "$body" $endpoint
```

<span data-ttu-id="d1a06-156">You've triggered the event, and Event Grid sent the message to the endpoint you configured when subscribing.</span><span class="sxs-lookup"><span data-stu-id="d1a06-156">You've triggered the event, and Event Grid sent the message to the endpoint you configured when subscribing.</span></span> <span data-ttu-id="d1a06-157">View your web app to see the event you just sent.</span><span class="sxs-lookup"><span data-stu-id="d1a06-157">View your web app to see the event you just sent.</span></span>

```json
[{
  "id": "1807",
  "eventType": "recordInserted",
  "subject": "myapp/vehicles/motorcycles",
  "eventTime": "2017-08-10T21:03:07+00:00",
  "data": {
    "make": "Ducati",
    "model": "Monster"
  },
  "dataVersion": "1.0",
  "metadataVersion": "1",
  "topic": "/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.EventGrid/topics/{topic}"
}]
```

## <a name="clean-up-resources"></a><span data-ttu-id="d1a06-158">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="d1a06-158">Clean up resources</span></span>
<span data-ttu-id="d1a06-159">If you plan to continue working with this event or the event viewer app, don't clean up the resources created in this article.</span><span class="sxs-lookup"><span data-stu-id="d1a06-159">If you plan to continue working with this event or the event viewer app, don't clean up the resources created in this article.</span></span> <span data-ttu-id="d1a06-160">Otherwise, use the following command to delete the resources you created in this article.</span><span class="sxs-lookup"><span data-stu-id="d1a06-160">Otherwise, use the following command to delete the resources you created in this article.</span></span>

```azurecli-interactive
az group delete --name gridResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="d1a06-161">Next steps</span><span class="sxs-lookup"><span data-stu-id="d1a06-161">Next steps</span></span>

<span data-ttu-id="d1a06-162">Now that you know how to create topics and event subscriptions, learn more about what Event Grid can help you do:</span><span class="sxs-lookup"><span data-stu-id="d1a06-162">Now that you know how to create topics and event subscriptions, learn more about what Event Grid can help you do:</span></span>

- [<span data-ttu-id="d1a06-163">About Event Grid</span><span class="sxs-lookup"><span data-stu-id="d1a06-163">About Event Grid</span></span>](overview.md)
- [<span data-ttu-id="d1a06-164">Route Blob storage events to a custom web endpoint</span><span class="sxs-lookup"><span data-stu-id="d1a06-164">Route Blob storage events to a custom web endpoint</span></span>](../storage/blobs/storage-blob-event-quickstart.md?toc=%2fazure%2fevent-grid%2ftoc.json)
- [<span data-ttu-id="d1a06-165">Monitor virtual machine changes with Azure Event Grid and Logic Apps</span><span class="sxs-lookup"><span data-stu-id="d1a06-165">Monitor virtual machine changes with Azure Event Grid and Logic Apps</span></span>](monitor-virtual-machine-changes-event-grid-logic-app.md)
- [<span data-ttu-id="d1a06-166">Stream big data into a data warehouse</span><span class="sxs-lookup"><span data-stu-id="d1a06-166">Stream big data into a data warehouse</span></span>](event-grid-event-hubs-integration.md)
