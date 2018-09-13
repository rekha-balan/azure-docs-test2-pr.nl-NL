---
title: Custom events for Azure Event Grid with the Azure portal | Microsoft Docs
description: Use Azure Event Grid and PowerShell to publish a topic, and subscribe to that event.
services: event-grid
keywords: ''
author: tfitzmac
ms.author: tomfitz
ms.date: 07/05/2018
ms.topic: quickstart
ms.service: event-grid
ms.openlocfilehash: ec85a866279412232aa23fad8f975d1642525772
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856293"
---
# <a name="create-and-route-custom-events-with-the-azure-portal-and-event-grid"></a><span data-ttu-id="9a81a-103">Create and route custom events with the Azure portal and Event Grid</span><span class="sxs-lookup"><span data-stu-id="9a81a-103">Create and route custom events with the Azure portal and Event Grid</span></span>

<span data-ttu-id="9a81a-104">Azure Event Grid is an eventing service for the cloud.</span><span class="sxs-lookup"><span data-stu-id="9a81a-104">Azure Event Grid is an eventing service for the cloud.</span></span> <span data-ttu-id="9a81a-105">In this article, you use the Azure portal to create a custom topic, subscribe to the topic, and trigger the event to view the result.</span><span class="sxs-lookup"><span data-stu-id="9a81a-105">In this article, you use the Azure portal to create a custom topic, subscribe to the topic, and trigger the event to view the result.</span></span> <span data-ttu-id="9a81a-106">You send the event to an Azure Function that logs the event data.</span><span class="sxs-lookup"><span data-stu-id="9a81a-106">You send the event to an Azure Function that logs the event data.</span></span> <span data-ttu-id="9a81a-107">When you're finished, you see that the event data has been sent to an endpoint and logged.</span><span class="sxs-lookup"><span data-stu-id="9a81a-107">When you're finished, you see that the event data has been sent to an endpoint and logged.</span></span>

[!INCLUDE [quickstarts-free-trial-note.md](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [event-grid-register-provider-portal.md](../../includes/event-grid-register-provider-portal.md)]

## <a name="create-a-custom-topic"></a><span data-ttu-id="9a81a-108">Create a custom topic</span><span class="sxs-lookup"><span data-stu-id="9a81a-108">Create a custom topic</span></span>

<span data-ttu-id="9a81a-109">An event grid topic provides a user-defined endpoint that you post your events to.</span><span class="sxs-lookup"><span data-stu-id="9a81a-109">An event grid topic provides a user-defined endpoint that you post your events to.</span></span> 

1. <span data-ttu-id="9a81a-110">Log in to [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="9a81a-110">Log in to [Azure portal](https://portal.azure.com/).</span></span>

1. <span data-ttu-id="9a81a-111">To create a custom topic, select **Create a resource**.</span><span class="sxs-lookup"><span data-stu-id="9a81a-111">To create a custom topic, select **Create a resource**.</span></span> 

   ![Create a resource](./media/custom-event-quickstart-portal/create-resource.png)

1. <span data-ttu-id="9a81a-113">Search for *Event Grid Topic* and select it from the available options.</span><span class="sxs-lookup"><span data-stu-id="9a81a-113">Search for *Event Grid Topic* and select it from the available options.</span></span>

   ![Search event grid topic](./media/custom-event-quickstart-portal/search-event-grid.png)

1. <span data-ttu-id="9a81a-115">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="9a81a-115">Select **Create**.</span></span>

   ![Start steps](./media/custom-event-quickstart-portal/select-create.png)

1. <span data-ttu-id="9a81a-117">Provide a unique name for the custom topic.</span><span class="sxs-lookup"><span data-stu-id="9a81a-117">Provide a unique name for the custom topic.</span></span> <span data-ttu-id="9a81a-118">The topic name must be unique because it is represented by a DNS entry.</span><span class="sxs-lookup"><span data-stu-id="9a81a-118">The topic name must be unique because it is represented by a DNS entry.</span></span> <span data-ttu-id="9a81a-119">Do not use the name shown in the image.</span><span class="sxs-lookup"><span data-stu-id="9a81a-119">Do not use the name shown in the image.</span></span> <span data-ttu-id="9a81a-120">Instead, create your own name.</span><span class="sxs-lookup"><span data-stu-id="9a81a-120">Instead, create your own name.</span></span> <span data-ttu-id="9a81a-121">Provide a name for the resource group.</span><span class="sxs-lookup"><span data-stu-id="9a81a-121">Provide a name for the resource group.</span></span> <span data-ttu-id="9a81a-122">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="9a81a-122">Select **Create**.</span></span>

   ![Provide event grid topic values](./media/custom-event-quickstart-portal/create-custom-topic.png)

1. <span data-ttu-id="9a81a-124">After the custom topic has been created, you see the successful notification.</span><span class="sxs-lookup"><span data-stu-id="9a81a-124">After the custom topic has been created, you see the successful notification.</span></span>

   ![See succeed notification](./media/custom-event-quickstart-portal/success-notification.png)

   <span data-ttu-id="9a81a-126">If the deployment didn't succeed, find out what caused the error.</span><span class="sxs-lookup"><span data-stu-id="9a81a-126">If the deployment didn't succeed, find out what caused the error.</span></span> <span data-ttu-id="9a81a-127">Select **Deployment failed**.</span><span class="sxs-lookup"><span data-stu-id="9a81a-127">Select **Deployment failed**.</span></span>

   ![Select deployment failed](./media/custom-event-quickstart-portal/select-failed.png)

   <span data-ttu-id="9a81a-129">Select the error message.</span><span class="sxs-lookup"><span data-stu-id="9a81a-129">Select the error message.</span></span>

   ![Select deployment failed](./media/custom-event-quickstart-portal/failed-details.png)

   <span data-ttu-id="9a81a-131">The following image shows a deployment that failed because the name for the custom topic is already in use.</span><span class="sxs-lookup"><span data-stu-id="9a81a-131">The following image shows a deployment that failed because the name for the custom topic is already in use.</span></span> <span data-ttu-id="9a81a-132">If you see this error, retry the deployment with a different name.</span><span class="sxs-lookup"><span data-stu-id="9a81a-132">If you see this error, retry the deployment with a different name.</span></span>

   ![Name conflict](./media/custom-event-quickstart-portal/name-conflict.png)

## <a name="create-an-azure-function"></a><span data-ttu-id="9a81a-134">Create an Azure Function</span><span class="sxs-lookup"><span data-stu-id="9a81a-134">Create an Azure Function</span></span>

<span data-ttu-id="9a81a-135">Before subscribing to the topic, let's create the endpoint for the event message.</span><span class="sxs-lookup"><span data-stu-id="9a81a-135">Before subscribing to the topic, let's create the endpoint for the event message.</span></span> <span data-ttu-id="9a81a-136">In this article, you use Azure Functions to create a function app for the endpoint.</span><span class="sxs-lookup"><span data-stu-id="9a81a-136">In this article, you use Azure Functions to create a function app for the endpoint.</span></span>

1. <span data-ttu-id="9a81a-137">To create a function, select **Create a resource**.</span><span class="sxs-lookup"><span data-stu-id="9a81a-137">To create a function, select **Create a resource**.</span></span>

   ![Create a resource](./media/custom-event-quickstart-portal/create-resource-small.png)

1. <span data-ttu-id="9a81a-139">Select **Compute** and **Function App**.</span><span class="sxs-lookup"><span data-stu-id="9a81a-139">Select **Compute** and **Function App**.</span></span>

   ![Create function](./media/custom-event-quickstart-portal/create-function.png)

1. <span data-ttu-id="9a81a-141">Provide a unique name for the Azure Function.</span><span class="sxs-lookup"><span data-stu-id="9a81a-141">Provide a unique name for the Azure Function.</span></span> <span data-ttu-id="9a81a-142">Do not use the name shown in the image.</span><span class="sxs-lookup"><span data-stu-id="9a81a-142">Do not use the name shown in the image.</span></span> <span data-ttu-id="9a81a-143">Select the resource group you created in this article.</span><span class="sxs-lookup"><span data-stu-id="9a81a-143">Select the resource group you created in this article.</span></span> <span data-ttu-id="9a81a-144">For hosting plan, use **Consumption Plan**.</span><span class="sxs-lookup"><span data-stu-id="9a81a-144">For hosting plan, use **Consumption Plan**.</span></span> <span data-ttu-id="9a81a-145">Use the suggested new storage account.</span><span class="sxs-lookup"><span data-stu-id="9a81a-145">Use the suggested new storage account.</span></span> <span data-ttu-id="9a81a-146">You can turn off Application Insights.</span><span class="sxs-lookup"><span data-stu-id="9a81a-146">You can turn off Application Insights.</span></span> <span data-ttu-id="9a81a-147">After providing the values, select **Create**.</span><span class="sxs-lookup"><span data-stu-id="9a81a-147">After providing the values, select **Create**.</span></span>

   ![Provide function values](./media/custom-event-quickstart-portal/provide-function-values.png)

1. <span data-ttu-id="9a81a-149">When the deployment finishes, select **Go to resource**.</span><span class="sxs-lookup"><span data-stu-id="9a81a-149">When the deployment finishes, select **Go to resource**.</span></span>

   ![Go to resource](./media/custom-event-quickstart-portal/go-to-resource.png)

1. <span data-ttu-id="9a81a-151">Next to **Functions**, select **+**.</span><span class="sxs-lookup"><span data-stu-id="9a81a-151">Next to **Functions**, select **+**.</span></span>

   ![Add function](./media/custom-event-quickstart-portal/add-function.png)

1. <span data-ttu-id="9a81a-153">From the available options, select **Custom function**.</span><span class="sxs-lookup"><span data-stu-id="9a81a-153">From the available options, select **Custom function**.</span></span>

   ![Custom function](./media/custom-event-quickstart-portal/select-custom-function.png)

1. <span data-ttu-id="9a81a-155">Scroll down until you find **Event Grid trigger**.</span><span class="sxs-lookup"><span data-stu-id="9a81a-155">Scroll down until you find **Event Grid trigger**.</span></span> <span data-ttu-id="9a81a-156">Select **C#**.</span><span class="sxs-lookup"><span data-stu-id="9a81a-156">Select **C#**.</span></span>

   ![Select event grid trigger](./media/custom-event-quickstart-portal/select-event-grid-trigger.png)

1. <span data-ttu-id="9a81a-158">Accept the default values, and select **Create**.</span><span class="sxs-lookup"><span data-stu-id="9a81a-158">Accept the default values, and select **Create**.</span></span>

   ![New function](./media/custom-event-quickstart-portal/new-function.png)

<span data-ttu-id="9a81a-160">Your function is now ready to receive events.</span><span class="sxs-lookup"><span data-stu-id="9a81a-160">Your function is now ready to receive events.</span></span>

## <a name="subscribe-to-a-topic"></a><span data-ttu-id="9a81a-161">Subscribe to a topic</span><span class="sxs-lookup"><span data-stu-id="9a81a-161">Subscribe to a topic</span></span>

<span data-ttu-id="9a81a-162">You subscribe to a topic to tell Event Grid which events you want to track, and where to send the events.</span><span class="sxs-lookup"><span data-stu-id="9a81a-162">You subscribe to a topic to tell Event Grid which events you want to track, and where to send the events.</span></span>

1. <span data-ttu-id="9a81a-163">In your Azure function, select **Add Event Grid Subscription**.</span><span class="sxs-lookup"><span data-stu-id="9a81a-163">In your Azure function, select **Add Event Grid Subscription**.</span></span>

   ![Add event grid subscription](./media/custom-event-quickstart-portal/add-event-grid-subscription.png)

1. <span data-ttu-id="9a81a-165">Provide values for the subscription.</span><span class="sxs-lookup"><span data-stu-id="9a81a-165">Provide values for the subscription.</span></span> <span data-ttu-id="9a81a-166">Select **Event Grid Topics** for the topic type.</span><span class="sxs-lookup"><span data-stu-id="9a81a-166">Select **Event Grid Topics** for the topic type.</span></span> <span data-ttu-id="9a81a-167">For subscription and resource group, select the subscription and resource group where you created your custom topic.</span><span class="sxs-lookup"><span data-stu-id="9a81a-167">For subscription and resource group, select the subscription and resource group where you created your custom topic.</span></span> <span data-ttu-id="9a81a-168">For instance, select the name of your custom topic.</span><span class="sxs-lookup"><span data-stu-id="9a81a-168">For instance, select the name of your custom topic.</span></span> <span data-ttu-id="9a81a-169">The subscriber endpoint is prepopulated with the URL for the function.</span><span class="sxs-lookup"><span data-stu-id="9a81a-169">The subscriber endpoint is prepopulated with the URL for the function.</span></span>

   ![Provide subscription values](./media/custom-event-quickstart-portal/provide-subscription-values.png)

1. <span data-ttu-id="9a81a-171">Before triggering the event, open the logs for the function so you can see the event data when it is sent.</span><span class="sxs-lookup"><span data-stu-id="9a81a-171">Before triggering the event, open the logs for the function so you can see the event data when it is sent.</span></span> <span data-ttu-id="9a81a-172">At the bottom of your Azure function, select **Logs**.</span><span class="sxs-lookup"><span data-stu-id="9a81a-172">At the bottom of your Azure function, select **Logs**.</span></span>

   ![Select logs](./media/custom-event-quickstart-portal/select-logs.png)

<span data-ttu-id="9a81a-174">Now, let's trigger an event to see how Event Grid distributes the message to your endpoint.</span><span class="sxs-lookup"><span data-stu-id="9a81a-174">Now, let's trigger an event to see how Event Grid distributes the message to your endpoint.</span></span> <span data-ttu-id="9a81a-175">To simplify this article, use Cloud Shell to send sample event data to the custom topic.</span><span class="sxs-lookup"><span data-stu-id="9a81a-175">To simplify this article, use Cloud Shell to send sample event data to the custom topic.</span></span> <span data-ttu-id="9a81a-176">Typically, an application or Azure service would send the event data.</span><span class="sxs-lookup"><span data-stu-id="9a81a-176">Typically, an application or Azure service would send the event data.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="send-an-event-to-your-topic"></a><span data-ttu-id="9a81a-177">Send an event to your topic</span><span class="sxs-lookup"><span data-stu-id="9a81a-177">Send an event to your topic</span></span>

<span data-ttu-id="9a81a-178">Use either Azure CLI or PowerShell to send a test event to your custom topic.</span><span class="sxs-lookup"><span data-stu-id="9a81a-178">Use either Azure CLI or PowerShell to send a test event to your custom topic.</span></span>

<span data-ttu-id="9a81a-179">The first example uses Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="9a81a-179">The first example uses Azure CLI.</span></span> <span data-ttu-id="9a81a-180">It gets the URL and key for the topic, and sample event data.</span><span class="sxs-lookup"><span data-stu-id="9a81a-180">It gets the URL and key for the topic, and sample event data.</span></span> <span data-ttu-id="9a81a-181">Use your topic name for `<topic_name>`.</span><span class="sxs-lookup"><span data-stu-id="9a81a-181">Use your topic name for `<topic_name>`.</span></span> <span data-ttu-id="9a81a-182">To see the full event, use `echo "$body"`.</span><span class="sxs-lookup"><span data-stu-id="9a81a-182">To see the full event, use `echo "$body"`.</span></span> <span data-ttu-id="9a81a-183">The `data` element of the JSON is the payload of your event.</span><span class="sxs-lookup"><span data-stu-id="9a81a-183">The `data` element of the JSON is the payload of your event.</span></span> <span data-ttu-id="9a81a-184">Any well-formed JSON can go in this field.</span><span class="sxs-lookup"><span data-stu-id="9a81a-184">Any well-formed JSON can go in this field.</span></span> <span data-ttu-id="9a81a-185">You can also use the subject field for advanced routing and filtering.</span><span class="sxs-lookup"><span data-stu-id="9a81a-185">You can also use the subject field for advanced routing and filtering.</span></span> <span data-ttu-id="9a81a-186">CURL is a utility that sends HTTP requests.</span><span class="sxs-lookup"><span data-stu-id="9a81a-186">CURL is a utility that sends HTTP requests.</span></span>

```azurecli-interactive
endpoint=$(az eventgrid topic show --name <topic_name> -g myResourceGroup --query "endpoint" --output tsv)
key=$(az eventgrid topic key list --name <topic_name> -g myResourceGroup --query "key1" --output tsv)

body=$(eval echo "'$(curl https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/event-grid/customevent.json)'")

curl -X POST -H "aeg-sas-key: $key" -d "$body" $endpoint
```

<span data-ttu-id="9a81a-187">The second example uses PowerShell to perform similar steps.</span><span class="sxs-lookup"><span data-stu-id="9a81a-187">The second example uses PowerShell to perform similar steps.</span></span>

```azurepowershell-interactive
$endpoint = (Get-AzureRmEventGridTopic -ResourceGroupName gridResourceGroup -Name <topic-name>).Endpoint
$keys = Get-AzureRmEventGridTopicKey -ResourceGroupName gridResourceGroup -Name <topic-name>

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

Invoke-WebRequest -Uri $endpoint -Method POST -Body $body -Headers @{"aeg-sas-key" = $keys.Key1}
```

<span data-ttu-id="9a81a-188">You've triggered the event, and Event Grid sent the message to the endpoint you configured when subscribing.</span><span class="sxs-lookup"><span data-stu-id="9a81a-188">You've triggered the event, and Event Grid sent the message to the endpoint you configured when subscribing.</span></span> <span data-ttu-id="9a81a-189">Look at the logs to see the event data.</span><span class="sxs-lookup"><span data-stu-id="9a81a-189">Look at the logs to see the event data.</span></span>

![View logs](./media/custom-event-quickstart-portal/view-log-entry.png)

## <a name="clean-up-resources"></a><span data-ttu-id="9a81a-191">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="9a81a-191">Clean up resources</span></span>

<span data-ttu-id="9a81a-192">If you plan to continue working with this event, don't clean up the resources created in this article.</span><span class="sxs-lookup"><span data-stu-id="9a81a-192">If you plan to continue working with this event, don't clean up the resources created in this article.</span></span> <span data-ttu-id="9a81a-193">Otherwise, delete the resources you created in this article.</span><span class="sxs-lookup"><span data-stu-id="9a81a-193">Otherwise, delete the resources you created in this article.</span></span>

<span data-ttu-id="9a81a-194">Select the resource group, and select **Delete resource group**.</span><span class="sxs-lookup"><span data-stu-id="9a81a-194">Select the resource group, and select **Delete resource group**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9a81a-195">Next steps</span><span class="sxs-lookup"><span data-stu-id="9a81a-195">Next steps</span></span>

<span data-ttu-id="9a81a-196">Now that you know how to create custom topics and event subscriptions, learn more about what Event Grid can help you do:</span><span class="sxs-lookup"><span data-stu-id="9a81a-196">Now that you know how to create custom topics and event subscriptions, learn more about what Event Grid can help you do:</span></span>

- [<span data-ttu-id="9a81a-197">About Event Grid</span><span class="sxs-lookup"><span data-stu-id="9a81a-197">About Event Grid</span></span>](overview.md)
- [<span data-ttu-id="9a81a-198">Route Blob storage events to a custom web endpoint</span><span class="sxs-lookup"><span data-stu-id="9a81a-198">Route Blob storage events to a custom web endpoint</span></span>](../storage/blobs/storage-blob-event-quickstart.md?toc=%2fazure%2fevent-grid%2ftoc.json)
- [<span data-ttu-id="9a81a-199">Monitor virtual machine changes with Azure Event Grid and Logic Apps</span><span class="sxs-lookup"><span data-stu-id="9a81a-199">Monitor virtual machine changes with Azure Event Grid and Logic Apps</span></span>](monitor-virtual-machine-changes-event-grid-logic-app.md)
- [<span data-ttu-id="9a81a-200">Stream big data into a data warehouse</span><span class="sxs-lookup"><span data-stu-id="9a81a-200">Stream big data into a data warehouse</span></span>](event-grid-event-hubs-integration.md)
