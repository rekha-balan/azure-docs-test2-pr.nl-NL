---
title: Route Azure Media Services events to a custom web endpoint  | Microsoft Docs
description: Use Azure Event Grid to subscribe to Media Services job state change event.
services: media-services
documentationcenter: ''
author: Juliako
manager: cfowler
editor: ''
ms.service: media-services
ms.workload: ''
ms.topic: article
ms.date: 03/19/2018
ms.author: juliako
ms.openlocfilehash: e9df0cd24ef890765b78c25a073d671889be10a7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867906"
---
# <a name="route-azure-media-services-events-to-a-custom-web-endpoint-using-cli"></a><span data-ttu-id="4f74d-103">Route Azure Media Services events to a custom web endpoint using CLI</span><span class="sxs-lookup"><span data-stu-id="4f74d-103">Route Azure Media Services events to a custom web endpoint using CLI</span></span>

<span data-ttu-id="4f74d-104">Azure Event Grid is an eventing service for the cloud.</span><span class="sxs-lookup"><span data-stu-id="4f74d-104">Azure Event Grid is an eventing service for the cloud.</span></span> <span data-ttu-id="4f74d-105">In this article, you use the Azure CLI to subscribe to Azure Media Services job state change events, and trigger the event to view the result.</span><span class="sxs-lookup"><span data-stu-id="4f74d-105">In this article, you use the Azure CLI to subscribe to Azure Media Services job state change events, and trigger the event to view the result.</span></span> 

<span data-ttu-id="4f74d-106">Typically, you send events to an endpoint that responds to the event, such as a webhook or Azure Function.</span><span class="sxs-lookup"><span data-stu-id="4f74d-106">Typically, you send events to an endpoint that responds to the event, such as a webhook or Azure Function.</span></span> <span data-ttu-id="4f74d-107">This tutorial, shows how to create and set a webhook.</span><span class="sxs-lookup"><span data-stu-id="4f74d-107">This tutorial, shows how to create and set a webhook.</span></span>

<span data-ttu-id="4f74d-108">When you complete the steps described in this article, you see that the event data has been sent to an endpoint.</span><span class="sxs-lookup"><span data-stu-id="4f74d-108">When you complete the steps described in this article, you see that the event data has been sent to an endpoint.</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="4f74d-109">Log in to Azure</span><span class="sxs-lookup"><span data-stu-id="4f74d-109">Log in to Azure</span></span>

<span data-ttu-id="4f74d-110">Log in to the [Azure portal](http://portal.azure.com) and launch **CloudShell** to execute CLI commands, as shown in the next steps.</span><span class="sxs-lookup"><span data-stu-id="4f74d-110">Log in to the [Azure portal](http://portal.azure.com) and launch **CloudShell** to execute CLI commands, as shown in the next steps.</span></span>

[!INCLUDE [cloud-shell-powershell.md](../../../includes/cloud-shell-powershell.md)]

<span data-ttu-id="4f74d-111">If you choose to install and use the CLI locally, this article requires the Azure CLI version 2.0 or later.</span><span class="sxs-lookup"><span data-stu-id="4f74d-111">If you choose to install and use the CLI locally, this article requires the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="4f74d-112">Run `az --version` to find the version you have.</span><span class="sxs-lookup"><span data-stu-id="4f74d-112">Run `az --version` to find the version you have.</span></span> <span data-ttu-id="4f74d-113">If you need to install or upgrade, see [Install the Azure CLI](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="4f74d-113">If you need to install or upgrade, see [Install the Azure CLI](/cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [media-services-cli-create-v3-account-include](../../../includes/media-services-cli-create-v3-account-include.md)]

<span data-ttu-id="4f74d-114">Make sure to remember the values that you used for the Media Services account name, storage name, and resource name.</span><span class="sxs-lookup"><span data-stu-id="4f74d-114">Make sure to remember the values that you used for the Media Services account name, storage name, and resource name.</span></span>

## <a name="enable-event-grid-resource-provider"></a><span data-ttu-id="4f74d-115">Enable Event Grid resource provider</span><span class="sxs-lookup"><span data-stu-id="4f74d-115">Enable Event Grid resource provider</span></span>

<span data-ttu-id="4f74d-116">First thing you need to do is make sure that you have Event Grid resource provider enabled on your subscription.</span><span class="sxs-lookup"><span data-stu-id="4f74d-116">First thing you need to do is make sure that you have Event Grid resource provider enabled on your subscription.</span></span> 

<span data-ttu-id="4f74d-117">In the **Azure** portal do the following:</span><span class="sxs-lookup"><span data-stu-id="4f74d-117">In the **Azure** portal do the following:</span></span>

1. <span data-ttu-id="4f74d-118">Go to Subscriptions.</span><span class="sxs-lookup"><span data-stu-id="4f74d-118">Go to Subscriptions.</span></span>
2. <span data-ttu-id="4f74d-119">Select your subscription.</span><span class="sxs-lookup"><span data-stu-id="4f74d-119">Select your subscription.</span></span>
3. <span data-ttu-id="4f74d-120">Under Settings, select Resource Providers.</span><span class="sxs-lookup"><span data-stu-id="4f74d-120">Under Settings, select Resource Providers.</span></span>
4. <span data-ttu-id="4f74d-121">Search for "EventGrid".</span><span class="sxs-lookup"><span data-stu-id="4f74d-121">Search for "EventGrid".</span></span>
5. <span data-ttu-id="4f74d-122">Make sure Event Grid is registered.</span><span class="sxs-lookup"><span data-stu-id="4f74d-122">Make sure Event Grid is registered.</span></span> <span data-ttu-id="4f74d-123">If not, press the **Register** button.</span><span class="sxs-lookup"><span data-stu-id="4f74d-123">If not, press the **Register** button.</span></span>  

## <a name="create-a-generic-azure-function-webhook"></a><span data-ttu-id="4f74d-124">Create a generic Azure Function webhook</span><span class="sxs-lookup"><span data-stu-id="4f74d-124">Create a generic Azure Function webhook</span></span> 

### <a name="create-a-message-endpoint"></a><span data-ttu-id="4f74d-125">Create a message endpoint</span><span class="sxs-lookup"><span data-stu-id="4f74d-125">Create a message endpoint</span></span>

<span data-ttu-id="4f74d-126">Before subscribing to the Event Grid's article, create an endpoint that collects the messages so you can view them.</span><span class="sxs-lookup"><span data-stu-id="4f74d-126">Before subscribing to the Event Grid's article, create an endpoint that collects the messages so you can view them.</span></span>

<span data-ttu-id="4f74d-127">Create a function triggered by a generic webhook as described in the [generic webhook](https://docs.microsoft.com/azure/azure-functions/functions-create-generic-webhook-triggered-function) article.</span><span class="sxs-lookup"><span data-stu-id="4f74d-127">Create a function triggered by a generic webhook as described in the [generic webhook](https://docs.microsoft.com/azure/azure-functions/functions-create-generic-webhook-triggered-function) article.</span></span> <span data-ttu-id="4f74d-128">In this tutorial, the **C#** code is used.</span><span class="sxs-lookup"><span data-stu-id="4f74d-128">In this tutorial, the **C#** code is used.</span></span>

<span data-ttu-id="4f74d-129">Once the webhook is created, copy the URL by clicking on the *Get function URL* link at the top of the **Azure** portal window.</span><span class="sxs-lookup"><span data-stu-id="4f74d-129">Once the webhook is created, copy the URL by clicking on the *Get function URL* link at the top of the **Azure** portal window.</span></span> <span data-ttu-id="4f74d-130">You do not need the last part of the URL (*&clientID=default*).</span><span class="sxs-lookup"><span data-stu-id="4f74d-130">You do not need the last part of the URL (*&clientID=default*).</span></span>

![Create a webhook](./media/job-state-events-cli-how-to/generic_webhook_files.png)

### <a name="validate-the-webhook"></a><span data-ttu-id="4f74d-132">Validate the webhook</span><span class="sxs-lookup"><span data-stu-id="4f74d-132">Validate the webhook</span></span>

<span data-ttu-id="4f74d-133">When you register your own webhook endpoint with Event Grid, it sends you a POST request with a simple validation code to prove endpoint ownership.</span><span class="sxs-lookup"><span data-stu-id="4f74d-133">When you register your own webhook endpoint with Event Grid, it sends you a POST request with a simple validation code to prove endpoint ownership.</span></span> <span data-ttu-id="4f74d-134">Your app needs to respond by echoing back the validation code.</span><span class="sxs-lookup"><span data-stu-id="4f74d-134">Your app needs to respond by echoing back the validation code.</span></span> <span data-ttu-id="4f74d-135">Event Grid doesn't deliver events to webHook endpoints that haven't passed the validation.</span><span class="sxs-lookup"><span data-stu-id="4f74d-135">Event Grid doesn't deliver events to webHook endpoints that haven't passed the validation.</span></span> <span data-ttu-id="4f74d-136">For more information, see [Event Grid security and authentication](https://docs.microsoft.com/azure/event-grid/security-authentication).</span><span class="sxs-lookup"><span data-stu-id="4f74d-136">For more information, see [Event Grid security and authentication](https://docs.microsoft.com/azure/event-grid/security-authentication).</span></span> <span data-ttu-id="4f74d-137">This section defines two parts that must be defined for the validation to pass.</span><span class="sxs-lookup"><span data-stu-id="4f74d-137">This section defines two parts that must be defined for the validation to pass.</span></span>

#### <a name="update-the-source-code"></a><span data-ttu-id="4f74d-138">Update the source code</span><span class="sxs-lookup"><span data-stu-id="4f74d-138">Update the source code</span></span>

<span data-ttu-id="4f74d-139">After you created your webhook, the **run.csx** file appears in the browser.</span><span class="sxs-lookup"><span data-stu-id="4f74d-139">After you created your webhook, the **run.csx** file appears in the browser.</span></span> <span data-ttu-id="4f74d-140">Replace the default code with the following code.</span><span class="sxs-lookup"><span data-stu-id="4f74d-140">Replace the default code with the following code.</span></span> 

```csharp
#r "Newtonsoft.Json"

using System;
using System.Net;
using Newtonsoft.Json;

public static async Task<object> Run(HttpRequestMessage req, TraceWriter log)
{
    log.Info($"Webhook was triggered!");

    string jsonContent = await req.Content.ReadAsStringAsync();
    string eventGridValidation = 
        req.Headers.FirstOrDefault( x => x.Key == "Aeg-Event-Type" ).Value?.FirstOrDefault();

    dynamic eventData = JsonConvert.DeserializeObject(jsonContent);

    log.Info($"event: {eventData}");

    if (eventGridValidation != String.Empty)
    {
        if (eventData[0].data.validationCode !=String.Empty && eventData[0].eventType == "Microsoft.EventGrid.SubscriptionValidationEvent")
        {
            return req.CreateResponse(HttpStatusCode.OK, new 
            {
                validationResponse = eventData[0].data.validationCode
            });
        }
    }
    
    log.Info(jsonContent);

    return req.CreateResponse(HttpStatusCode.OK);
}
```

#### <a name="update-test-request-body"></a><span data-ttu-id="4f74d-141">Update test request body</span><span class="sxs-lookup"><span data-stu-id="4f74d-141">Update test request body</span></span>

<span data-ttu-id="4f74d-142">On the right of the **Azure** portal window you see two tabs: **View files** and **Test**.</span><span class="sxs-lookup"><span data-stu-id="4f74d-142">On the right of the **Azure** portal window you see two tabs: **View files** and **Test**.</span></span> <span data-ttu-id="4f74d-143">Select the **Test** tab. In the **Request body**, paste the following json.</span><span class="sxs-lookup"><span data-stu-id="4f74d-143">Select the **Test** tab. In the **Request body**, paste the following json.</span></span> <span data-ttu-id="4f74d-144">You can paste it as is, no need to change any values.</span><span class="sxs-lookup"><span data-stu-id="4f74d-144">You can paste it as is, no need to change any values.</span></span>

```json
[{
  "id": "2d1781af-3a4c-4d7c-bd0c-e34b19da4e66",
  "topic": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
  "subject": "",
  "data": {
    "validationCode": "512d38b6-c7b8-40c8-89fe-f46f9e9622b6"
  },
  "eventType": "Microsoft.EventGrid.SubscriptionValidationEvent",
  "eventTime": "2017-08-06T22:09:30.740323Z"
}
]
```

<span data-ttu-id="4f74d-145">Press **Save and run** at the top of the window.</span><span class="sxs-lookup"><span data-stu-id="4f74d-145">Press **Save and run** at the top of the window.</span></span>

![Request body](./media/job-state-events-cli-how-to/generic_webhook_test.png)

## <a name="register-for-the-event-grid-subscription"></a><span data-ttu-id="4f74d-147">Register for the Event Grid subscription</span><span class="sxs-lookup"><span data-stu-id="4f74d-147">Register for the Event Grid subscription</span></span> 

<span data-ttu-id="4f74d-148">You subscribe to an article to tell Event Grid which events you want to track. The following example subscribes to the Media Services account you created, and passes the URL from  Azure Function webhook you created as the endpoint for event notification.</span><span class="sxs-lookup"><span data-stu-id="4f74d-148">You subscribe to an article to tell Event Grid which events you want to track. The following example subscribes to the Media Services account you created, and passes the URL from  Azure Function webhook you created as the endpoint for event notification.</span></span> 

<span data-ttu-id="4f74d-149">Replace `<event_subscription_name>` with a unique name for your event subscription.</span><span class="sxs-lookup"><span data-stu-id="4f74d-149">Replace `<event_subscription_name>` with a unique name for your event subscription.</span></span> <span data-ttu-id="4f74d-150">For `<resource_group_name>` and `<ams_account_name>`, use the values you created earlier.</span><span class="sxs-lookup"><span data-stu-id="4f74d-150">For `<resource_group_name>` and `<ams_account_name>`, use the values you created earlier.</span></span>  <span data-ttu-id="4f74d-151">For the `<endpoint_URL>` paste your endpoint URL.</span><span class="sxs-lookup"><span data-stu-id="4f74d-151">For the `<endpoint_URL>` paste your endpoint URL.</span></span> <span data-ttu-id="4f74d-152">Remove *&clientID=default* from the URL.</span><span class="sxs-lookup"><span data-stu-id="4f74d-152">Remove *&clientID=default* from the URL.</span></span> <span data-ttu-id="4f74d-153">By specifying an endpoint when subscribing, Event Grid handles the routing of events to that endpoint.</span><span class="sxs-lookup"><span data-stu-id="4f74d-153">By specifying an endpoint when subscribing, Event Grid handles the routing of events to that endpoint.</span></span> 

```cli
amsResourceId=$(az ams account show --name <ams_account_name> --resource-group <resource_group_name> --query id --output tsv)

az eventgrid event-subscription create \
  --resource-id $amsResourceId \
  --name <event_subscription_name> \
  --endpoint <endpoint_URL>
```

<span data-ttu-id="4f74d-154">The Media Services account resource id value looks similar to this:</span><span class="sxs-lookup"><span data-stu-id="4f74d-154">The Media Services account resource id value looks similar to this:</span></span>

<span data-ttu-id="4f74d-155">/subscriptions/81212121-2f4f-4b5d-a3dc-ba0015515f7b/resourceGroups/amsResourceGroup/providers/Microsoft.Media/mediaservices/amstestaccount</span><span class="sxs-lookup"><span data-stu-id="4f74d-155">/subscriptions/81212121-2f4f-4b5d-a3dc-ba0015515f7b/resourceGroups/amsResourceGroup/providers/Microsoft.Media/mediaservices/amstestaccount</span></span>

## <a name="test-the-events"></a><span data-ttu-id="4f74d-156">Test the events</span><span class="sxs-lookup"><span data-stu-id="4f74d-156">Test the events</span></span>

<span data-ttu-id="4f74d-157">Run an encoding job.</span><span class="sxs-lookup"><span data-stu-id="4f74d-157">Run an encoding job.</span></span> <span data-ttu-id="4f74d-158">For example, as described in the [Stream video files](stream-files-dotnet-quickstart.md) quickstart.</span><span class="sxs-lookup"><span data-stu-id="4f74d-158">For example, as described in the [Stream video files](stream-files-dotnet-quickstart.md) quickstart.</span></span>

<span data-ttu-id="4f74d-159">You have triggered the event, and Event Grid sent the message to the endpoint you configured when subscribing.</span><span class="sxs-lookup"><span data-stu-id="4f74d-159">You have triggered the event, and Event Grid sent the message to the endpoint you configured when subscribing.</span></span> <span data-ttu-id="4f74d-160">Browse to the webhook you created earlier.</span><span class="sxs-lookup"><span data-stu-id="4f74d-160">Browse to the webhook you created earlier.</span></span> <span data-ttu-id="4f74d-161">Click **Monitor** and **Refresh**.</span><span class="sxs-lookup"><span data-stu-id="4f74d-161">Click **Monitor** and **Refresh**.</span></span> <span data-ttu-id="4f74d-162">You see the job's state changes events: "Queued", "Scheduled", "Processing", "Finished", "Error", "Canceled", "Canceling".</span><span class="sxs-lookup"><span data-stu-id="4f74d-162">You see the job's state changes events: "Queued", "Scheduled", "Processing", "Finished", "Error", "Canceled", "Canceling".</span></span>  <span data-ttu-id="4f74d-163">For more information, see [Media Services event schemas](media-services-event-schemas.md).</span><span class="sxs-lookup"><span data-stu-id="4f74d-163">For more information, see [Media Services event schemas](media-services-event-schemas.md).</span></span>

<span data-ttu-id="4f74d-164">For example:</span><span class="sxs-lookup"><span data-stu-id="4f74d-164">For example:</span></span>

```json
[{
  "topic": "/subscriptions/<subscription id>/resourceGroups/amsResourceGroup/providers/Microsoft.Media/mediaservices/amsaccount",
  "subject": "transforms/VideoAnalyzerTransform/jobs/<job id>",
  "eventType": "Microsoft.Media.JobStateChange",
  "eventTime": "2018-04-20T21:17:26.2534881",
  "id": "<id>",
  "data": {
    "previousState": "Scheduled",
    "state": "Processing"
  },
  "dataVersion": "1.0",
  "metadataVersion": "1"
}]
```

![Test events](./media/job-state-events-cli-how-to/test_events.png)

## <a name="clean-up-resources"></a><span data-ttu-id="4f74d-166">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="4f74d-166">Clean up resources</span></span>

<span data-ttu-id="4f74d-167">If you plan to continue working with this storage account and event subscription, do not clean up the resources created in this article.</span><span class="sxs-lookup"><span data-stu-id="4f74d-167">If you plan to continue working with this storage account and event subscription, do not clean up the resources created in this article.</span></span> <span data-ttu-id="4f74d-168">If you do not plan to continue, use the following command to delete the resources you created in this article.</span><span class="sxs-lookup"><span data-stu-id="4f74d-168">If you do not plan to continue, use the following command to delete the resources you created in this article.</span></span>

<span data-ttu-id="4f74d-169">Replace `<resource_group_name>` with the resource group you created above.</span><span class="sxs-lookup"><span data-stu-id="4f74d-169">Replace `<resource_group_name>` with the resource group you created above.</span></span>

```azurecli-interactive
az group delete --name <resource_group_name>
```

## <a name="next-steps"></a><span data-ttu-id="4f74d-170">Next steps</span><span class="sxs-lookup"><span data-stu-id="4f74d-170">Next steps</span></span>

[<span data-ttu-id="4f74d-171">Reacting to events</span><span class="sxs-lookup"><span data-stu-id="4f74d-171">Reacting to events</span></span>](reacting-to-media-services-events.md)

## <a name="see-also"></a><span data-ttu-id="4f74d-172">See also</span><span class="sxs-lookup"><span data-stu-id="4f74d-172">See also</span></span>

[<span data-ttu-id="4f74d-173">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="4f74d-173">Azure CLI</span></span>](https://docs.microsoft.com/en-us/cli/azure/ams?view=azure-cli-latest)
