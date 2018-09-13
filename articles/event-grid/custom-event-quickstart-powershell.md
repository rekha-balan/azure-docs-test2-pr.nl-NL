---
title: Custom events for Azure Event Grid with PowerShell | Microsoft Docs
description: Use Azure Event Grid and PowerShell to publish a topic, and subscribe to that event.
services: event-grid
keywords: ''
author: tfitzmac
ms.author: tomfitz
ms.date: 08/23/2018
ms.topic: quickstart
ms.service: event-grid
ms.openlocfilehash: 13620fbd6393c747285574cf16b519b9b6a1f324
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869282"
---
# <a name="create-and-route-custom-events-with-azure-powershell-and-event-grid"></a><span data-ttu-id="a2771-103">Create and route custom events with Azure PowerShell and Event Grid</span><span class="sxs-lookup"><span data-stu-id="a2771-103">Create and route custom events with Azure PowerShell and Event Grid</span></span>

<span data-ttu-id="a2771-104">Azure Event Grid is an eventing service for the cloud.</span><span class="sxs-lookup"><span data-stu-id="a2771-104">Azure Event Grid is an eventing service for the cloud.</span></span> <span data-ttu-id="a2771-105">In this article, you use the Azure PowerShell to create a custom topic, subscribe to the topic, and trigger the event to view the result.</span><span class="sxs-lookup"><span data-stu-id="a2771-105">In this article, you use the Azure PowerShell to create a custom topic, subscribe to the topic, and trigger the event to view the result.</span></span> <span data-ttu-id="a2771-106">Typically, you send events to an endpoint that processes the event data and takes actions.</span><span class="sxs-lookup"><span data-stu-id="a2771-106">Typically, you send events to an endpoint that processes the event data and takes actions.</span></span> <span data-ttu-id="a2771-107">However, to simplify this article, you send the events to a web app that collects and displays the messages.</span><span class="sxs-lookup"><span data-stu-id="a2771-107">However, to simplify this article, you send the events to a web app that collects and displays the messages.</span></span>

<span data-ttu-id="a2771-108">When you're finished, you see that the event data has been sent to the web app.</span><span class="sxs-lookup"><span data-stu-id="a2771-108">When you're finished, you see that the event data has been sent to the web app.</span></span>

![View results](./media/custom-event-quickstart-powershell/view-result.png)

[!INCLUDE [quickstarts-free-trial-note.md](../../includes/quickstarts-free-trial-note.md)]

<span data-ttu-id="a2771-110">This article requires that you are running the latest version of Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a2771-110">This article requires that you are running the latest version of Azure PowerShell.</span></span> <span data-ttu-id="a2771-111">If you need to install or upgrade, see [Install and configure Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="a2771-111">If you need to install or upgrade, see [Install and configure Azure PowerShell](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="a2771-112">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="a2771-112">Create a resource group</span></span>

<span data-ttu-id="a2771-113">Event Grid topics are Azure resources, and must be placed in an Azure resource group.</span><span class="sxs-lookup"><span data-stu-id="a2771-113">Event Grid topics are Azure resources, and must be placed in an Azure resource group.</span></span> <span data-ttu-id="a2771-114">The resource group is a logical collection into which Azure resources are deployed and managed.</span><span class="sxs-lookup"><span data-stu-id="a2771-114">The resource group is a logical collection into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="a2771-115">Create a resource group with the [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) command.</span><span class="sxs-lookup"><span data-stu-id="a2771-115">Create a resource group with the [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) command.</span></span>

<span data-ttu-id="a2771-116">The following example creates a resource group named *gridResourceGroup* in the *westus2* location.</span><span class="sxs-lookup"><span data-stu-id="a2771-116">The following example creates a resource group named *gridResourceGroup* in the *westus2* location.</span></span>

```powershell-interactive
New-AzureRmResourceGroup -Name gridResourceGroup -Location westus2
```

[!INCLUDE [event-grid-register-provider-powershell.md](../../includes/event-grid-register-provider-powershell.md)]

## <a name="create-a-custom-topic"></a><span data-ttu-id="a2771-117">Create a custom topic</span><span class="sxs-lookup"><span data-stu-id="a2771-117">Create a custom topic</span></span>

<span data-ttu-id="a2771-118">An event grid topic provides a user-defined endpoint that you post your events to.</span><span class="sxs-lookup"><span data-stu-id="a2771-118">An event grid topic provides a user-defined endpoint that you post your events to.</span></span> <span data-ttu-id="a2771-119">The following example creates the custom topic in your resource group.</span><span class="sxs-lookup"><span data-stu-id="a2771-119">The following example creates the custom topic in your resource group.</span></span> <span data-ttu-id="a2771-120">Replace `<your-topic-name>` with a unique name for your topic.</span><span class="sxs-lookup"><span data-stu-id="a2771-120">Replace `<your-topic-name>` with a unique name for your topic.</span></span> <span data-ttu-id="a2771-121">The topic name must be unique because it's part of the DNS entry.</span><span class="sxs-lookup"><span data-stu-id="a2771-121">The topic name must be unique because it's part of the DNS entry.</span></span>

```powershell-interactive
$topicname="<your-topic-name>"

New-AzureRmEventGridTopic -ResourceGroupName gridResourceGroup -Location westus2 -Name $topicname
```

## <a name="create-a-message-endpoint"></a><span data-ttu-id="a2771-122">Create a message endpoint</span><span class="sxs-lookup"><span data-stu-id="a2771-122">Create a message endpoint</span></span>

<span data-ttu-id="a2771-123">Before subscribing to the topic, let's create the endpoint for the event message.</span><span class="sxs-lookup"><span data-stu-id="a2771-123">Before subscribing to the topic, let's create the endpoint for the event message.</span></span> <span data-ttu-id="a2771-124">Typically, the endpoint takes actions based on the event data.</span><span class="sxs-lookup"><span data-stu-id="a2771-124">Typically, the endpoint takes actions based on the event data.</span></span> <span data-ttu-id="a2771-125">To simplify this quickstart, you deploy a [pre-built web app](https://github.com/Azure-Samples/azure-event-grid-viewer) that displays the event messages.</span><span class="sxs-lookup"><span data-stu-id="a2771-125">To simplify this quickstart, you deploy a [pre-built web app](https://github.com/Azure-Samples/azure-event-grid-viewer) that displays the event messages.</span></span> <span data-ttu-id="a2771-126">The deployed solution includes an App Service plan, an App Service web app, and source code from GitHub.</span><span class="sxs-lookup"><span data-stu-id="a2771-126">The deployed solution includes an App Service plan, an App Service web app, and source code from GitHub.</span></span>

<span data-ttu-id="a2771-127">Replace `<your-site-name>` with a unique name for your web app.</span><span class="sxs-lookup"><span data-stu-id="a2771-127">Replace `<your-site-name>` with a unique name for your web app.</span></span> <span data-ttu-id="a2771-128">The web app name must be unique because it's part of the DNS entry.</span><span class="sxs-lookup"><span data-stu-id="a2771-128">The web app name must be unique because it's part of the DNS entry.</span></span>

```powershell-interactive
$sitename="<your-site-name>"

New-AzureRmResourceGroupDeployment `
  -ResourceGroupName gridResourceGroup `
  -TemplateUri "https://raw.githubusercontent.com/Azure-Samples/azure-event-grid-viewer/master/azuredeploy.json" `
  -siteName $sitename `
  -hostingPlanName viewerhost
```

<span data-ttu-id="a2771-129">The deployment may take a few minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="a2771-129">The deployment may take a few minutes to complete.</span></span> <span data-ttu-id="a2771-130">After the deployment has succeeded, view your web app to make sure it's running.</span><span class="sxs-lookup"><span data-stu-id="a2771-130">After the deployment has succeeded, view your web app to make sure it's running.</span></span> <span data-ttu-id="a2771-131">In a web browser, navigate to: `https://<your-site-name>.azurewebsites.net`</span><span class="sxs-lookup"><span data-stu-id="a2771-131">In a web browser, navigate to: `https://<your-site-name>.azurewebsites.net`</span></span>

<span data-ttu-id="a2771-132">You should see the site with no messages currently displayed.</span><span class="sxs-lookup"><span data-stu-id="a2771-132">You should see the site with no messages currently displayed.</span></span>

## <a name="subscribe-to-a-topic"></a><span data-ttu-id="a2771-133">Subscribe to a topic</span><span class="sxs-lookup"><span data-stu-id="a2771-133">Subscribe to a topic</span></span>

<span data-ttu-id="a2771-134">You subscribe to a topic to tell Event Grid which events you want to track and where to send those events.</span><span class="sxs-lookup"><span data-stu-id="a2771-134">You subscribe to a topic to tell Event Grid which events you want to track and where to send those events.</span></span> <span data-ttu-id="a2771-135">The following example subscribes to the topic you created, and passes the URL from your web app as the endpoint for event notification.</span><span class="sxs-lookup"><span data-stu-id="a2771-135">The following example subscribes to the topic you created, and passes the URL from your web app as the endpoint for event notification.</span></span>

<span data-ttu-id="a2771-136">The endpoint for your web app must include the suffix `/api/updates/`.</span><span class="sxs-lookup"><span data-stu-id="a2771-136">The endpoint for your web app must include the suffix `/api/updates/`.</span></span>

```powershell-interactive
$endpoint="https://$sitename.azurewebsites.net/api/updates"

New-AzureRmEventGridSubscription `
  -EventSubscriptionName demoViewerSub `
  -Endpoint $endpoint `
  -ResourceGroupName gridResourceGroup `
  -TopicName $topicname
```

<span data-ttu-id="a2771-137">View your web app again, and notice that a subscription validation event has been sent to it.</span><span class="sxs-lookup"><span data-stu-id="a2771-137">View your web app again, and notice that a subscription validation event has been sent to it.</span></span> <span data-ttu-id="a2771-138">Select the eye icon to expand the event data.</span><span class="sxs-lookup"><span data-stu-id="a2771-138">Select the eye icon to expand the event data.</span></span> <span data-ttu-id="a2771-139">Event Grid sends the validation event so the endpoint can verify that it wants to receive event data.</span><span class="sxs-lookup"><span data-stu-id="a2771-139">Event Grid sends the validation event so the endpoint can verify that it wants to receive event data.</span></span> <span data-ttu-id="a2771-140">The web app includes code to validate the subscription.</span><span class="sxs-lookup"><span data-stu-id="a2771-140">The web app includes code to validate the subscription.</span></span>

![View subscription event](./media/custom-event-quickstart-powershell/view-subscription-event.png)

## <a name="send-an-event-to-your-topic"></a><span data-ttu-id="a2771-142">Send an event to your topic</span><span class="sxs-lookup"><span data-stu-id="a2771-142">Send an event to your topic</span></span>

<span data-ttu-id="a2771-143">Let's trigger an event to see how Event Grid distributes the message to your endpoint.</span><span class="sxs-lookup"><span data-stu-id="a2771-143">Let's trigger an event to see how Event Grid distributes the message to your endpoint.</span></span> <span data-ttu-id="a2771-144">First, let's get the URL and key for the topic.</span><span class="sxs-lookup"><span data-stu-id="a2771-144">First, let's get the URL and key for the topic.</span></span>

```powershell-interactive
$endpoint = (Get-AzureRmEventGridTopic -ResourceGroupName gridResourceGroup -Name $topicname).Endpoint
$keys = Get-AzureRmEventGridTopicKey -ResourceGroupName gridResourceGroup -Name $topicname
```

<span data-ttu-id="a2771-145">To simplify this article, let's set up sample event data to send to the custom topic.</span><span class="sxs-lookup"><span data-stu-id="a2771-145">To simplify this article, let's set up sample event data to send to the custom topic.</span></span> <span data-ttu-id="a2771-146">Typically, an application or Azure service would send the event data.</span><span class="sxs-lookup"><span data-stu-id="a2771-146">Typically, an application or Azure service would send the event data.</span></span> <span data-ttu-id="a2771-147">The following example uses Hashtable to construct the event's data `htbody` and then coverts it to well-formed JSON payload object `$body`:</span><span class="sxs-lookup"><span data-stu-id="a2771-147">The following example uses Hashtable to construct the event's data `htbody` and then coverts it to well-formed JSON payload object `$body`:</span></span>

```powershell-interactive
$eventID = Get-Random 99999

#Date format should be SortableDateTimePattern (ISO 8601)
$eventDate = Get-Date -Format s

#Construct body using Hashtable
$htbody = @{
    id= $eventID
    eventType="recordInserted"
    subject="myapp/vehicles/motorcycles"
    eventTime= $eventDate   
    data= @{
        make="Ducati"
        model="Monster"
    }
    dataVersion="1.0"
}

#Use ConvertTo-Json to convert event body from Hashtable to JSON Object
#Append square brackets to the converted JSON payload since they are expected in the event's JSON payload syntax
$body = "["+(ConvertTo-Json $htbody)+"]"
```

<span data-ttu-id="a2771-148">If you view `$body`, you see the full event.</span><span class="sxs-lookup"><span data-stu-id="a2771-148">If you view `$body`, you see the full event.</span></span> <span data-ttu-id="a2771-149">The `data` element of the JSON is the payload of your event.</span><span class="sxs-lookup"><span data-stu-id="a2771-149">The `data` element of the JSON is the payload of your event.</span></span> <span data-ttu-id="a2771-150">Any well-formed JSON can go in this field.</span><span class="sxs-lookup"><span data-stu-id="a2771-150">Any well-formed JSON can go in this field.</span></span> <span data-ttu-id="a2771-151">You can also use the subject field for advanced routing and filtering.</span><span class="sxs-lookup"><span data-stu-id="a2771-151">You can also use the subject field for advanced routing and filtering.</span></span>

<span data-ttu-id="a2771-152">Now, send the event to your topic.</span><span class="sxs-lookup"><span data-stu-id="a2771-152">Now, send the event to your topic.</span></span>

```powershell-interactive
Invoke-WebRequest -Uri $endpoint -Method POST -Body $body -Headers @{"aeg-sas-key" = $keys.Key1}
```

<span data-ttu-id="a2771-153">You've triggered the event, and Event Grid sent the message to the endpoint you configured when subscribing.</span><span class="sxs-lookup"><span data-stu-id="a2771-153">You've triggered the event, and Event Grid sent the message to the endpoint you configured when subscribing.</span></span> <span data-ttu-id="a2771-154">View your web app to see the event you just sent.</span><span class="sxs-lookup"><span data-stu-id="a2771-154">View your web app to see the event you just sent.</span></span>

```json
[{
  "id": "1807",
  "eventType": "recordInserted",
  "subject": "myapp/vehicles/motorcycles",
  "eventTime": "2018-01-25T15:58:13",
  "data": {
    "make": "Ducati",
    "model": "Monster"
  },
  "dataVersion": "1.0",
  "metadataVersion": "1",
  "topic": "/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.EventGrid/topics/{topic}"
}]
```

## <a name="clean-up-resources"></a><span data-ttu-id="a2771-155">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="a2771-155">Clean up resources</span></span>

<span data-ttu-id="a2771-156">If you plan to continue working with this event or the event viewer app, don't clean up the resources created in this article.</span><span class="sxs-lookup"><span data-stu-id="a2771-156">If you plan to continue working with this event or the event viewer app, don't clean up the resources created in this article.</span></span> <span data-ttu-id="a2771-157">Otherwise, use the following command to delete the resources you created in this article.</span><span class="sxs-lookup"><span data-stu-id="a2771-157">Otherwise, use the following command to delete the resources you created in this article.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name gridResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="a2771-158">Next steps</span><span class="sxs-lookup"><span data-stu-id="a2771-158">Next steps</span></span>

<span data-ttu-id="a2771-159">Now that you know how to create topics and event subscriptions, learn more about what Event Grid can help you do:</span><span class="sxs-lookup"><span data-stu-id="a2771-159">Now that you know how to create topics and event subscriptions, learn more about what Event Grid can help you do:</span></span>

- [<span data-ttu-id="a2771-160">About Event Grid</span><span class="sxs-lookup"><span data-stu-id="a2771-160">About Event Grid</span></span>](overview.md)
- [<span data-ttu-id="a2771-161">Route Blob storage events to a custom web endpoint</span><span class="sxs-lookup"><span data-stu-id="a2771-161">Route Blob storage events to a custom web endpoint</span></span>](../storage/blobs/storage-blob-event-quickstart.md?toc=%2fazure%2fevent-grid%2ftoc.json)
- [<span data-ttu-id="a2771-162">Monitor virtual machine changes with Azure Event Grid and Logic Apps</span><span class="sxs-lookup"><span data-stu-id="a2771-162">Monitor virtual machine changes with Azure Event Grid and Logic Apps</span></span>](monitor-virtual-machine-changes-event-grid-logic-app.md)
- [<span data-ttu-id="a2771-163">Stream big data into a data warehouse</span><span class="sxs-lookup"><span data-stu-id="a2771-163">Stream big data into a data warehouse</span></span>](event-grid-event-hubs-integration.md)
