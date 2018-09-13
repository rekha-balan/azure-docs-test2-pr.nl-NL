---
title: App Service API app triggers | Microsoft Docs
description: How to implement triggers in an API App in Azure App Service
services: logic-apps
documentationcenter: .net
author: guangyang
manager: erikre
editor: jimbe
ms.assetid: 493c3703-786d-4434-9dca-8f77744b2f5d
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 08/25/2016
ms.author: rachelap
ms.openlocfilehash: 4344d7030cdfc786c7bd35c25408fb96d7266fc2
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662095"
---
# <a name="azure-app-service-api-app-triggers"></a><span data-ttu-id="e9fd2-103">Azure App Service API app triggers</span><span class="sxs-lookup"><span data-stu-id="e9fd2-103">Azure App Service API app triggers</span></span>
> [!NOTE]
> <span data-ttu-id="e9fd2-104">This version of the article applies to API apps 2014-12-01-preview schema version.</span><span class="sxs-lookup"><span data-stu-id="e9fd2-104">This version of the article applies to API apps 2014-12-01-preview schema version.</span></span>
>
>

## <a name="overview"></a><span data-ttu-id="e9fd2-105">Overview</span><span class="sxs-lookup"><span data-stu-id="e9fd2-105">Overview</span></span>
<span data-ttu-id="e9fd2-106">This article explains how to implement API app triggers and consume them from a Logic app.</span><span class="sxs-lookup"><span data-stu-id="e9fd2-106">This article explains how to implement API app triggers and consume them from a Logic app.</span></span>

<span data-ttu-id="e9fd2-107">All of the code snippets in this topic are copied from the [FileWatcher API App code sample](http://go.microsoft.com/fwlink/?LinkId=534802).</span><span class="sxs-lookup"><span data-stu-id="e9fd2-107">All of the code snippets in this topic are copied from the [FileWatcher API App code sample](http://go.microsoft.com/fwlink/?LinkId=534802).</span></span>

<span data-ttu-id="e9fd2-108">Note that you'll need to download the following nuget package for the code in this article to build and run: [http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/](http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/).</span><span class="sxs-lookup"><span data-stu-id="e9fd2-108">Note that you'll need to download the following nuget package for the code in this article to build and run: [http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/](http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/).</span></span>

## <a name="what-are-api-app-triggers"></a><span data-ttu-id="e9fd2-109">What are API app triggers?</span><span class="sxs-lookup"><span data-stu-id="e9fd2-109">What are API app triggers?</span></span>
<span data-ttu-id="e9fd2-110">It's a common scenario for an API app to fire an event so that clients of the API app can take the appropriate action in response to the event.</span><span class="sxs-lookup"><span data-stu-id="e9fd2-110">It's a common scenario for an API app to fire an event so that clients of the API app can take the appropriate action in response to the event.</span></span> <span data-ttu-id="e9fd2-111">The REST API based mechanism that supports this scenario is called an API app trigger.</span><span class="sxs-lookup"><span data-stu-id="e9fd2-111">The REST API based mechanism that supports this scenario is called an API app trigger.</span></span>

<span data-ttu-id="e9fd2-112">For example, let's say your client code is using the [Twitter Connector API app](../connectors/connectors-create-api-twitter.md) and your code needs to perform an action based on new tweets that contain specific words.</span><span class="sxs-lookup"><span data-stu-id="e9fd2-112">For example, let's say your client code is using the [Twitter Connector API app](../connectors/connectors-create-api-twitter.md) and your code needs to perform an action based on new tweets that contain specific words.</span></span> <span data-ttu-id="e9fd2-113">In this case, you might set up a poll or push trigger to facilitate this need.</span><span class="sxs-lookup"><span data-stu-id="e9fd2-113">In this case, you might set up a poll or push trigger to facilitate this need.</span></span>

## <a name="poll-trigger-versus-push-trigger"></a><span data-ttu-id="e9fd2-114">Poll trigger versus push trigger</span><span class="sxs-lookup"><span data-stu-id="e9fd2-114">Poll trigger versus push trigger</span></span>
<span data-ttu-id="e9fd2-115">Currently, two types of triggers are supported:</span><span class="sxs-lookup"><span data-stu-id="e9fd2-115">Currently, two types of triggers are supported:</span></span>

* <span data-ttu-id="e9fd2-116">Poll trigger - Client polls the API app for notification of an event having been fired</span><span class="sxs-lookup"><span data-stu-id="e9fd2-116">Poll trigger - Client polls the API app for notification of an event having been fired</span></span>
* <span data-ttu-id="e9fd2-117">Push trigger - Client is notified by the API app when an event fires</span><span class="sxs-lookup"><span data-stu-id="e9fd2-117">Push trigger - Client is notified by the API app when an event fires</span></span>

### <a name="poll-trigger"></a><span data-ttu-id="e9fd2-118">Poll trigger</span><span class="sxs-lookup"><span data-stu-id="e9fd2-118">Poll trigger</span></span>
<span data-ttu-id="e9fd2-119">A poll trigger is implemented as a regular REST API and expects its clients (such as a Logic app) to poll it in order to get notification.</span><span class="sxs-lookup"><span data-stu-id="e9fd2-119">A poll trigger is implemented as a regular REST API and expects its clients (such as a Logic app) to poll it in order to get notification.</span></span> <span data-ttu-id="e9fd2-120">While the client may maintain state, the poll trigger itself is stateless.</span><span class="sxs-lookup"><span data-stu-id="e9fd2-120">While the client may maintain state, the poll trigger itself is stateless.</span></span>

<span data-ttu-id="e9fd2-121">The following information regarding the request and response packets illustrate some key aspects of the poll trigger contract:</span><span class="sxs-lookup"><span data-stu-id="e9fd2-121">The following information regarding the request and response packets illustrate some key aspects of the poll trigger contract:</span></span>

* <span data-ttu-id="e9fd2-122">Request</span><span class="sxs-lookup"><span data-stu-id="e9fd2-122">Request</span></span>
  * <span data-ttu-id="e9fd2-123">HTTP method: GET</span><span class="sxs-lookup"><span data-stu-id="e9fd2-123">HTTP method: GET</span></span>
  * <span data-ttu-id="e9fd2-124">Parameters</span><span class="sxs-lookup"><span data-stu-id="e9fd2-124">Parameters</span></span>
    * <span data-ttu-id="e9fd2-125">triggerState - This optional parameter allows clients to specify their state so that the poll trigger can properly decide whether to return notification or not based on the specified state.</span><span class="sxs-lookup"><span data-stu-id="e9fd2-125">triggerState - This optional parameter allows clients to specify their state so that the poll trigger can properly decide whether to return notification or not based on the specified state.</span></span>
    * <span data-ttu-id="e9fd2-126">API-specific parameters</span><span class="sxs-lookup"><span data-stu-id="e9fd2-126">API-specific parameters</span></span>
* <span data-ttu-id="e9fd2-127">Response</span><span class="sxs-lookup"><span data-stu-id="e9fd2-127">Response</span></span>
  * <span data-ttu-id="e9fd2-128">Status code **200** - Request is valid and there is a notification from the trigger.</span><span class="sxs-lookup"><span data-stu-id="e9fd2-128">Status code **200** - Request is valid and there is a notification from the trigger.</span></span> <span data-ttu-id="e9fd2-129">The content of the notification will be the response body.</span><span class="sxs-lookup"><span data-stu-id="e9fd2-129">The content of the notification will be the response body.</span></span> <span data-ttu-id="e9fd2-130">A "Retry-After" header in the response indicates that additional notification data must be retrieved with a subsequent request call.</span><span class="sxs-lookup"><span data-stu-id="e9fd2-130">A "Retry-After" header in the response indicates that additional notification data must be retrieved with a subsequent request call.</span></span>
  * <span data-ttu-id="e9fd2-131">Status code **202** - Request is valid, but there is no new notification from the trigger.</span><span class="sxs-lookup"><span data-stu-id="e9fd2-131">Status code **202** - Request is valid, but there is no new notification from the trigger.</span></span>
  * <span data-ttu-id="e9fd2-132">Status code **4xx** - Request is not valid.</span><span class="sxs-lookup"><span data-stu-id="e9fd2-132">Status code **4xx** - Request is not valid.</span></span> <span data-ttu-id="e9fd2-133">The client should not retry the request.</span><span class="sxs-lookup"><span data-stu-id="e9fd2-133">The client should not retry the request.</span></span>
  * <span data-ttu-id="e9fd2-134">Status code **5xx** - Request has resulted in an internal server error and/or temporary issue.</span><span class="sxs-lookup"><span data-stu-id="e9fd2-134">Status code **5xx** - Request has resulted in an internal server error and/or temporary issue.</span></span> <span data-ttu-id="e9fd2-135">The client should retry the request.</span><span class="sxs-lookup"><span data-stu-id="e9fd2-135">The client should retry the request.</span></span>

<span data-ttu-id="e9fd2-136">The following code snippet is an example of how to implement a poll trigger.</span><span class="sxs-lookup"><span data-stu-id="e9fd2-136">The following code snippet is an example of how to implement a poll trigger.</span></span>

    // Implement a poll trigger.
    [HttpGet]
    [Route("api/files/poll/TouchedFiles")]
    public HttpResponseMessage TouchedFilesPollTrigger(
        // triggerState is a UTC timestamp
        string triggerState,
        // Additional parameters
        string searchPattern = "*")
    {
        // Check to see whether there is any file touched after the timestamp.
        var lastTriggerTimeUtc = DateTime.Parse(triggerState).ToUniversalTime();
        var touchedFiles = Directory.EnumerateFiles(rootPath, searchPattern, SearchOption.AllDirectories)
            .Select(f => FileInfoWrapper.FromFileInfo(new FileInfo(f)))
            .Where(fi => fi.LastAccessTimeUtc > lastTriggerTimeUtc);

        // If there are files touched after the timestamp, return their information.
        if (touchedFiles != null && touchedFiles.Count() != 0)
        {
            // Extension method provided by the AppService service SDK.
            return this.Request.EventTriggered(new { files = touchedFiles });
        }
        // If there are no files touched after the timestamp, tell the caller to poll again after 1 mintue.
        else
        {
            // Extension method provided by the AppService service SDK.
            return this.Request.EventWaitPoll(new TimeSpan(0, 1, 0));
        }
    }

<span data-ttu-id="e9fd2-137">To test this poll trigger, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="e9fd2-137">To test this poll trigger, follow these steps:</span></span>

1. <span data-ttu-id="e9fd2-138">Deploy the API App with an authentication setting of **public anonymous**.</span><span class="sxs-lookup"><span data-stu-id="e9fd2-138">Deploy the API App with an authentication setting of **public anonymous**.</span></span>
2. <span data-ttu-id="e9fd2-139">Call the **touch** operation to touch a file.</span><span class="sxs-lookup"><span data-stu-id="e9fd2-139">Call the **touch** operation to touch a file.</span></span> <span data-ttu-id="e9fd2-140">The following image shows a sample request via Postman.</span><span class="sxs-lookup"><span data-stu-id="e9fd2-140">The following image shows a sample request via Postman.</span></span>
   <span data-ttu-id="e9fd2-141">![Call Touch Operation via Postman](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="e9fd2-141">![Call Touch Operation via Postman](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span></span>
3. <span data-ttu-id="e9fd2-142">Call the poll trigger with the **triggerState** parameter set to a time stamp prior to Step #2.</span><span class="sxs-lookup"><span data-stu-id="e9fd2-142">Call the poll trigger with the **triggerState** parameter set to a time stamp prior to Step #2.</span></span> <span data-ttu-id="e9fd2-143">The following image shows the sample request via Postman.</span><span class="sxs-lookup"><span data-stu-id="e9fd2-143">The following image shows the sample request via Postman.</span></span>
   <span data-ttu-id="e9fd2-144">![Call Poll Trigger via Postman](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-dotnet-triggers/callpolltriggerfrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="e9fd2-144">![Call Poll Trigger via Postman](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-dotnet-triggers/callpolltriggerfrompostman.PNG)</span></span>

### <a name="push-trigger"></a><span data-ttu-id="e9fd2-145">Push trigger</span><span class="sxs-lookup"><span data-stu-id="e9fd2-145">Push trigger</span></span>
<span data-ttu-id="e9fd2-146">A push trigger is implemented as a regular REST API that pushes notifications to clients who have registered to be notified when specific events fire.</span><span class="sxs-lookup"><span data-stu-id="e9fd2-146">A push trigger is implemented as a regular REST API that pushes notifications to clients who have registered to be notified when specific events fire.</span></span>

<span data-ttu-id="e9fd2-147">The following information regarding the request and response packets illustrate some key aspects of the push trigger contract.</span><span class="sxs-lookup"><span data-stu-id="e9fd2-147">The following information regarding the request and response packets illustrate some key aspects of the push trigger contract.</span></span>

* <span data-ttu-id="e9fd2-148">Request</span><span class="sxs-lookup"><span data-stu-id="e9fd2-148">Request</span></span>
  * <span data-ttu-id="e9fd2-149">HTTP method: PUT</span><span class="sxs-lookup"><span data-stu-id="e9fd2-149">HTTP method: PUT</span></span>
  * <span data-ttu-id="e9fd2-150">Parameters</span><span class="sxs-lookup"><span data-stu-id="e9fd2-150">Parameters</span></span>
    * <span data-ttu-id="e9fd2-151">triggerId: required - Opaque string (such as a GUID) that represents the registration of a push trigger.</span><span class="sxs-lookup"><span data-stu-id="e9fd2-151">triggerId: required - Opaque string (such as a GUID) that represents the registration of a push trigger.</span></span>
    * <span data-ttu-id="e9fd2-152">callbackUrl: required - URL of the callback to invoke when the event fires.</span><span class="sxs-lookup"><span data-stu-id="e9fd2-152">callbackUrl: required - URL of the callback to invoke when the event fires.</span></span> <span data-ttu-id="e9fd2-153">The invocation is a simple POST HTTP call.</span><span class="sxs-lookup"><span data-stu-id="e9fd2-153">The invocation is a simple POST HTTP call.</span></span>
    * <span data-ttu-id="e9fd2-154">API-specific parameters</span><span class="sxs-lookup"><span data-stu-id="e9fd2-154">API-specific parameters</span></span>
* <span data-ttu-id="e9fd2-155">Response</span><span class="sxs-lookup"><span data-stu-id="e9fd2-155">Response</span></span>
  * <span data-ttu-id="e9fd2-156">Status code **200** - Request to register client successful.</span><span class="sxs-lookup"><span data-stu-id="e9fd2-156">Status code **200** - Request to register client successful.</span></span>
  * <span data-ttu-id="e9fd2-157">Status code **4xx** - Request is not valid.</span><span class="sxs-lookup"><span data-stu-id="e9fd2-157">Status code **4xx** - Request is not valid.</span></span> <span data-ttu-id="e9fd2-158">The client should not retry the request.</span><span class="sxs-lookup"><span data-stu-id="e9fd2-158">The client should not retry the request.</span></span>
  * <span data-ttu-id="e9fd2-159">Status code **5xx** - Request has resulted in an internal server error and/or temporary issue.</span><span class="sxs-lookup"><span data-stu-id="e9fd2-159">Status code **5xx** - Request has resulted in an internal server error and/or temporary issue.</span></span> <span data-ttu-id="e9fd2-160">The client should retry the request.</span><span class="sxs-lookup"><span data-stu-id="e9fd2-160">The client should retry the request.</span></span>
* <span data-ttu-id="e9fd2-161">Callback</span><span class="sxs-lookup"><span data-stu-id="e9fd2-161">Callback</span></span>
  * <span data-ttu-id="e9fd2-162">HTTP method: POST</span><span class="sxs-lookup"><span data-stu-id="e9fd2-162">HTTP method: POST</span></span>
  * <span data-ttu-id="e9fd2-163">Request body: Notification content.</span><span class="sxs-lookup"><span data-stu-id="e9fd2-163">Request body: Notification content.</span></span>

<span data-ttu-id="e9fd2-164">The following code snippet is an example of how to implement a push trigger:</span><span class="sxs-lookup"><span data-stu-id="e9fd2-164">The following code snippet is an example of how to implement a push trigger:</span></span>

    // Implement a push trigger.
    [HttpPut]
    [Route("api/files/push/TouchedFiles/{triggerId}")]
    public HttpResponseMessage TouchedFilesPushTrigger(
        // triggerId is an opaque string.
        string triggerId,
        // A helper class provided by the AppService service SDK.
        // Here it defines the input of the push trigger is a string and the output to the callback is a FileInfoWrapper object.
        [FromBody]TriggerInput<string, FileInfoWrapper> triggerInput)
    {
        // Register the trigger to some trigger store.
        triggerStore.RegisterTrigger(triggerId, rootPath, triggerInput);

        // Extension method provided by the AppService service SDK indicating the registration is completed.
        return this.Request.PushTriggerRegistered(triggerInput.GetCallback());
    }

    // A simple in-memory trigger store.
    public class InMemoryTriggerStore
    {
        private static InMemoryTriggerStore instance;

        private IDictionary<string, FileSystemWatcher> _store;

        private InMemoryTriggerStore()
        {
            _store = new Dictionary<string, FileSystemWatcher>();
        }

        public static InMemoryTriggerStore Instance
        {
            get
            {
                if (instance == null)
                {
                    instance = new InMemoryTriggerStore();
                }
                return instance;
            }
        }

        // Register a push trigger.
        public void RegisterTrigger(string triggerId, string rootPath,
            TriggerInput<string, FileInfoWrapper> triggerInput)
        {
            // Use FileSystemWatcher to listen to file change event.
            var filter = string.IsNullOrEmpty(triggerInput.inputs) ? "*" : triggerInput.inputs;
            var watcher = new FileSystemWatcher(rootPath, filter);
            watcher.IncludeSubdirectories = true;
            watcher.EnableRaisingEvents = true;
            watcher.NotifyFilter = NotifyFilters.LastAccess;

            // When some file is changed, fire the push trigger.
            watcher.Changed +=
                (sender, e) => watcher_Changed(sender, e,
                    Runtime.FromAppSettings(),
                    triggerInput.GetCallback());

            // Assoicate the FileSystemWatcher object with the triggerId.
            _store[triggerId] = watcher;

        }

        // Fire the assoicated push trigger when some file is changed.
        void watcher_Changed(object sender, FileSystemEventArgs e,
            // AppService runtime object needed to invoke the callback.
            Runtime runtime,
            // The callback to invoke.
            ClientTriggerCallback<FileInfoWrapper> callback)
        {
            // Helper method provided by AppService service SDK to invoke a push trigger callback.
            callback.InvokeAsync(runtime, FileInfoWrapper.FromFileInfo(new FileInfo(e.FullPath)));
        }
    }

<span data-ttu-id="e9fd2-165">To test this poll trigger, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="e9fd2-165">To test this poll trigger, follow these steps:</span></span>

1. <span data-ttu-id="e9fd2-166">Deploy the API App with an authentication setting of **public anonymous**.</span><span class="sxs-lookup"><span data-stu-id="e9fd2-166">Deploy the API App with an authentication setting of **public anonymous**.</span></span>
2. <span data-ttu-id="e9fd2-167">Browse to [http://requestb.in/](http://requestb.in/) to create a RequestBin which will serve as your callback URL.</span><span class="sxs-lookup"><span data-stu-id="e9fd2-167">Browse to [http://requestb.in/](http://requestb.in/) to create a RequestBin which will serve as your callback URL.</span></span>
3. <span data-ttu-id="e9fd2-168">Call the push trigger with a GUID as **triggerId** and the RequestBin URL as **callbackUrl**.</span><span class="sxs-lookup"><span data-stu-id="e9fd2-168">Call the push trigger with a GUID as **triggerId** and the RequestBin URL as **callbackUrl**.</span></span>
   <span data-ttu-id="e9fd2-169">![Call Push Trigger via Postman](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-dotnet-triggers/callpushtriggerfrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="e9fd2-169">![Call Push Trigger via Postman](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-dotnet-triggers/callpushtriggerfrompostman.PNG)</span></span>
4. <span data-ttu-id="e9fd2-170">Call the **touch** operation to touch a file.</span><span class="sxs-lookup"><span data-stu-id="e9fd2-170">Call the **touch** operation to touch a file.</span></span> <span data-ttu-id="e9fd2-171">The following image shows a sample request via Postman.</span><span class="sxs-lookup"><span data-stu-id="e9fd2-171">The following image shows a sample request via Postman.</span></span>
   <span data-ttu-id="e9fd2-172">![Call Touch Operation via Postman](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="e9fd2-172">![Call Touch Operation via Postman](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span></span>
5. <span data-ttu-id="e9fd2-173">Check the RequestBin to confirm that the push trigger callback is invoked with property output.</span><span class="sxs-lookup"><span data-stu-id="e9fd2-173">Check the RequestBin to confirm that the push trigger callback is invoked with property output.</span></span>
   <span data-ttu-id="e9fd2-174">![Call Poll Trigger via Postman](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-dotnet-triggers/pushtriggercallbackinrequestbin.PNG)</span><span class="sxs-lookup"><span data-stu-id="e9fd2-174">![Call Poll Trigger via Postman](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-dotnet-triggers/pushtriggercallbackinrequestbin.PNG)</span></span>

### <a name="describe-triggers-in-api-definition"></a><span data-ttu-id="e9fd2-175">Describe triggers in API definition</span><span class="sxs-lookup"><span data-stu-id="e9fd2-175">Describe triggers in API definition</span></span>
<span data-ttu-id="e9fd2-176">After implementing the triggers and deploying your API app to Azure, navigate to the **API Definition** blade in the Azure preview portal and you'll see that triggers are automatically recognized in the UI, which is driven by the Swagger 2.0 API definition of the API app.</span><span class="sxs-lookup"><span data-stu-id="e9fd2-176">After implementing the triggers and deploying your API app to Azure, navigate to the **API Definition** blade in the Azure preview portal and you'll see that triggers are automatically recognized in the UI, which is driven by the Swagger 2.0 API definition of the API app.</span></span>

![API Definition Blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-dotnet-triggers/apidefinitionblade.PNG)

<span data-ttu-id="e9fd2-178">If you click the **Download Swagger** button and open the JSON file, you'll see results similar to the following:</span><span class="sxs-lookup"><span data-stu-id="e9fd2-178">If you click the **Download Swagger** button and open the JSON file, you'll see results similar to the following:</span></span>

    "/api/files/poll/TouchedFiles": {
      "get": {
        "operationId": "Files_TouchedFilesPollTrigger",
        ...
        "x-ms-scheduler-trigger": "poll"
      }
    },
    "/api/files/push/TouchedFiles/{triggerId}": {
      "put": {
        "operationId": "Files_TouchedFilesPushTrigger",
        ...
        "x-ms-scheduler-trigger": "push"
      }
    }

<span data-ttu-id="e9fd2-179">The extension property **x-ms-schedular-trigger** is how triggers are described in API definition, and is automatically added by the API app gateway when you request the API definition via the gateway if the request to one of the following criteria.</span><span class="sxs-lookup"><span data-stu-id="e9fd2-179">The extension property **x-ms-schedular-trigger** is how triggers are described in API definition, and is automatically added by the API app gateway when you request the API definition via the gateway if the request to one of the following criteria.</span></span> <span data-ttu-id="e9fd2-180">(You can also add this property manually.)</span><span class="sxs-lookup"><span data-stu-id="e9fd2-180">(You can also add this property manually.)</span></span>

* <span data-ttu-id="e9fd2-181">Poll trigger</span><span class="sxs-lookup"><span data-stu-id="e9fd2-181">Poll trigger</span></span>
  * <span data-ttu-id="e9fd2-182">If the HTTP method is **GET**.</span><span class="sxs-lookup"><span data-stu-id="e9fd2-182">If the HTTP method is **GET**.</span></span>
  * <span data-ttu-id="e9fd2-183">If the **operationId** property contains the string **trigger**.</span><span class="sxs-lookup"><span data-stu-id="e9fd2-183">If the **operationId** property contains the string **trigger**.</span></span>
  * <span data-ttu-id="e9fd2-184">If the **parameters** property includes a parameter with a **name** property set to **triggerState**.</span><span class="sxs-lookup"><span data-stu-id="e9fd2-184">If the **parameters** property includes a parameter with a **name** property set to **triggerState**.</span></span>
* <span data-ttu-id="e9fd2-185">Push trigger</span><span class="sxs-lookup"><span data-stu-id="e9fd2-185">Push trigger</span></span>
  * <span data-ttu-id="e9fd2-186">If the HTTP method is **PUT**.</span><span class="sxs-lookup"><span data-stu-id="e9fd2-186">If the HTTP method is **PUT**.</span></span>
  * <span data-ttu-id="e9fd2-187">If the **operationId** property contains the string **trigger**.</span><span class="sxs-lookup"><span data-stu-id="e9fd2-187">If the **operationId** property contains the string **trigger**.</span></span>
  * <span data-ttu-id="e9fd2-188">If the **parameters** property includes a parameter with a **name** property set to **triggerId**.</span><span class="sxs-lookup"><span data-stu-id="e9fd2-188">If the **parameters** property includes a parameter with a **name** property set to **triggerId**.</span></span>

## <a name="use-api-app-triggers-in-logic-apps"></a><span data-ttu-id="e9fd2-189">Use API app triggers in Logic apps</span><span class="sxs-lookup"><span data-stu-id="e9fd2-189">Use API app triggers in Logic apps</span></span>
### <a name="list-and-configure-api-app-triggers-in-the-logic-apps-designer"></a><span data-ttu-id="e9fd2-190">List and configure API app triggers in the Logic apps designer</span><span class="sxs-lookup"><span data-stu-id="e9fd2-190">List and configure API app triggers in the Logic apps designer</span></span>
<span data-ttu-id="e9fd2-191">If you create a Logic app in the same resource group as the API app, you will be able to add it to the designer canvas simply by clicking it.</span><span class="sxs-lookup"><span data-stu-id="e9fd2-191">If you create a Logic app in the same resource group as the API app, you will be able to add it to the designer canvas simply by clicking it.</span></span> <span data-ttu-id="e9fd2-192">The following images illustrate this:</span><span class="sxs-lookup"><span data-stu-id="e9fd2-192">The following images illustrate this:</span></span>

![Triggers in Logic App Designer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-dotnet-triggers/triggersinlogicappdesigner.PNG)

![Configure Poll Trigger in Logic App Designer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-dotnet-triggers/configurepolltriggerinlogicappdesigner.PNG)

![Configure Push Trigger in Logic App Designer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-dotnet-triggers/configurepushtriggerinlogicappdesigner.PNG)

## <a name="optimize-api-app-triggers-for-logic-apps"></a><span data-ttu-id="e9fd2-196">Optimize API app triggers for Logic apps</span><span class="sxs-lookup"><span data-stu-id="e9fd2-196">Optimize API app triggers for Logic apps</span></span>
<span data-ttu-id="e9fd2-197">After you add triggers to an API app, there are a few things you can do to improve the experience when using the API app in a Logic app.</span><span class="sxs-lookup"><span data-stu-id="e9fd2-197">After you add triggers to an API app, there are a few things you can do to improve the experience when using the API app in a Logic app.</span></span>

<span data-ttu-id="e9fd2-198">For instance, the **triggerState** parameter for poll triggers should be set to the following expression in the Logic app.</span><span class="sxs-lookup"><span data-stu-id="e9fd2-198">For instance, the **triggerState** parameter for poll triggers should be set to the following expression in the Logic app.</span></span> <span data-ttu-id="e9fd2-199">This expression should evaluate the last invocation of the trigger from the Logic app, and return that value.</span><span class="sxs-lookup"><span data-stu-id="e9fd2-199">This expression should evaluate the last invocation of the trigger from the Logic app, and return that value.</span></span>  

    @coalesce(triggers()?.outputs?.body?['triggerState'], '')

<span data-ttu-id="e9fd2-200">NOTE: For an explanation of the functions used in the expression above, refer to the documentation on [Logic App Workflow Definition Language](https://msdn.microsoft.com/library/azure/dn948512.aspx).</span><span class="sxs-lookup"><span data-stu-id="e9fd2-200">NOTE: For an explanation of the functions used in the expression above, refer to the documentation on [Logic App Workflow Definition Language](https://msdn.microsoft.com/library/azure/dn948512.aspx).</span></span>

<span data-ttu-id="e9fd2-201">Logic app users would need to provide the expression above for the **triggerState** parameter while using the trigger.</span><span class="sxs-lookup"><span data-stu-id="e9fd2-201">Logic app users would need to provide the expression above for the **triggerState** parameter while using the trigger.</span></span> <span data-ttu-id="e9fd2-202">It is possible to have this value preset by the Logic app designer through the extension property **x-ms-scheduler-recommendation**.</span><span class="sxs-lookup"><span data-stu-id="e9fd2-202">It is possible to have this value preset by the Logic app designer through the extension property **x-ms-scheduler-recommendation**.</span></span>  <span data-ttu-id="e9fd2-203">The **x-ms-visibility** extension property can be set to a value of *internal* so that the parameter itself is not shown on the designer.</span><span class="sxs-lookup"><span data-stu-id="e9fd2-203">The **x-ms-visibility** extension property can be set to a value of *internal* so that the parameter itself is not shown on the designer.</span></span>  <span data-ttu-id="e9fd2-204">The following snippet illustrates that.</span><span class="sxs-lookup"><span data-stu-id="e9fd2-204">The following snippet illustrates that.</span></span>

    "/api/Messages/poll": {
      "get": {
        "operationId": "Messages_NewMessageTrigger",
        "parameters": [
          {
            "name": "triggerState",
            "in": "query",
            "required": true,
            "x-ms-visibility": "internal",
            "x-ms-scheduler-recommendation": "@coalesce(triggers()?.outputs?.body?['triggerState'], '')",
            "type": "string"
          }
        ]
        ...
        "x-ms-scheduler-trigger": "poll"
      }
    }

<span data-ttu-id="e9fd2-205">For push triggers, the **triggerId** parameter must uniquely identify the Logic app.</span><span class="sxs-lookup"><span data-stu-id="e9fd2-205">For push triggers, the **triggerId** parameter must uniquely identify the Logic app.</span></span> <span data-ttu-id="e9fd2-206">A recommended best practice is to set this property to the name of the workflow by using the following expression:</span><span class="sxs-lookup"><span data-stu-id="e9fd2-206">A recommended best practice is to set this property to the name of the workflow by using the following expression:</span></span>

    @workflow().name

<span data-ttu-id="e9fd2-207">Using the **x-ms-scheduler-recommendation** and **x-ms-visibility** extension properties in its API definiton, the API app can convey to the Logic app designer to automatically set this expression for the user.</span><span class="sxs-lookup"><span data-stu-id="e9fd2-207">Using the **x-ms-scheduler-recommendation** and **x-ms-visibility** extension properties in its API definiton, the API app can convey to the Logic app designer to automatically set this expression for the user.</span></span>

        "parameters":[  
          {  
            "name":"triggerId",
            "in":"path",
            "required":true,
            "x-ms-visibility":"internal",
            "x-ms-scheduler-recommendation":"@workflow().name",
            "type":"string"
          },


### <a name="add-extension-properties-in-api-defintion"></a><span data-ttu-id="e9fd2-208">Add extension properties in API defintion</span><span class="sxs-lookup"><span data-stu-id="e9fd2-208">Add extension properties in API defintion</span></span>
<span data-ttu-id="e9fd2-209">Additional metadata information - such as the extension properties **x-ms-scheduler-recommendation** and **x-ms-visibility** - can be added in the API defintion in one of two ways: static or dynamic.</span><span class="sxs-lookup"><span data-stu-id="e9fd2-209">Additional metadata information - such as the extension properties **x-ms-scheduler-recommendation** and **x-ms-visibility** - can be added in the API defintion in one of two ways: static or dynamic.</span></span>

<span data-ttu-id="e9fd2-210">For static metadata, you can directly edit the */metadata/apiDefinition.swagger.json* file in your project and add the properties manually.</span><span class="sxs-lookup"><span data-stu-id="e9fd2-210">For static metadata, you can directly edit the */metadata/apiDefinition.swagger.json* file in your project and add the properties manually.</span></span>

<span data-ttu-id="e9fd2-211">For API apps using dynamic metadata, you can edit the SwaggerConfig.cs file to add an operation filter which can add these extensions.</span><span class="sxs-lookup"><span data-stu-id="e9fd2-211">For API apps using dynamic metadata, you can edit the SwaggerConfig.cs file to add an operation filter which can add these extensions.</span></span>

    GlobalConfiguration.Configuration
        .EnableSwagger(c =>
            {
                ...
                c.OperationFilter<TriggerStateFilter>();
                ...
            }


<span data-ttu-id="e9fd2-212">The following is an example of how this class can be implemented to facilitate the dynamic metadata scenario.</span><span class="sxs-lookup"><span data-stu-id="e9fd2-212">The following is an example of how this class can be implemented to facilitate the dynamic metadata scenario.</span></span>

    // Add extension properties on the triggerState parameter
    public class TriggerStateFilter : IOperationFilter
    {

        public void Apply(Operation operation, SchemaRegistry schemaRegistry, System.Web.Http.Description.ApiDescription apiDescription)
        {
            if (operation.operationId.IndexOf("Trigger", StringComparison.InvariantCultureIgnoreCase) >= 0)
            {
                // this is a possible trigger
                var triggerStateParam = operation.parameters.FirstOrDefault(x => x.name.Equals("triggerState"));
                if (triggerStateParam != null)
                {
                    if (triggerStateParam.vendorExtensions == null)
                    {
                        triggerStateParam.vendorExtensions = new Dictionary<string, object>();
                    }

                    // add 2 vendor extensions
                    // x-ms-visibility: set to 'internal' to signify this is an internal field
                    // x-ms-scheduler-recommendation: set to a value that logic app can use
                    triggerStateParam.vendorExtensions.Add("x-ms-visibility", "internal");
                    triggerStateParam.vendorExtensions.Add("x-ms-scheduler-recommendation",
                                                           "@coalesce(triggers()?.outputs?.body?['triggerState'], '')");
                }
            }
        }
    }









