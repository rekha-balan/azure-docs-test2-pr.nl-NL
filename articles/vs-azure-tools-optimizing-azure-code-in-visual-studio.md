---
title: Optimizing your Azure code in Visual Studio | Microsoft Docs
description: Learn about how Azure code optimization tools in Visual Studio help make your code more robust and better-performing.
services: visual-studio-online
documentationcenter: na
author: TomArcher
manager: douge
editor: ''
ms.assetid: ed48ee06-e2d2-4322-af22-07200fb16987
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: tarcher
ms.openlocfilehash: fe946e69faae5ddbdc19115730f7b6e8cf421e92
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551213"
---
# <a name="optimizing-your-azure-code"></a><span data-ttu-id="e86fc-103">Optimizing Your Azure Code</span><span class="sxs-lookup"><span data-stu-id="e86fc-103">Optimizing Your Azure Code</span></span>
<span data-ttu-id="e86fc-104">When you’re programming apps that use Microsoft Azure, there are some coding practices you should follow to help avoid problems with app scalability, behavior and performance in a cloud environment.</span><span class="sxs-lookup"><span data-stu-id="e86fc-104">When you’re programming apps that use Microsoft Azure, there are some coding practices you should follow to help avoid problems with app scalability, behavior and performance in a cloud environment.</span></span> <span data-ttu-id="e86fc-105">Microsoft provides an Azure Code Analysis tool that recognizes and identifies several of these commonly-encountered issues and helps you resolve them.</span><span class="sxs-lookup"><span data-stu-id="e86fc-105">Microsoft provides an Azure Code Analysis tool that recognizes and identifies several of these commonly-encountered issues and helps you resolve them.</span></span> <span data-ttu-id="e86fc-106">You can download the tool in Visual Studio via NuGet.</span><span class="sxs-lookup"><span data-stu-id="e86fc-106">You can download the tool in Visual Studio via NuGet.</span></span>

## <a name="azure-code-analysis-rules"></a><span data-ttu-id="e86fc-107">Azure Code Analysis rules</span><span class="sxs-lookup"><span data-stu-id="e86fc-107">Azure Code Analysis rules</span></span>
<span data-ttu-id="e86fc-108">The Azure Code Analysis tool uses the following rules to automatically flag your Azure code when it finds known performance-impacting issues.</span><span class="sxs-lookup"><span data-stu-id="e86fc-108">The Azure Code Analysis tool uses the following rules to automatically flag your Azure code when it finds known performance-impacting issues.</span></span> <span data-ttu-id="e86fc-109">Detected issues appear as a warnings or compiler errors.</span><span class="sxs-lookup"><span data-stu-id="e86fc-109">Detected issues appear as a warnings or compiler errors.</span></span> <span data-ttu-id="e86fc-110">Code fixes or suggestions to resolve the warning or error are often provided through a light bulb icon.</span><span class="sxs-lookup"><span data-stu-id="e86fc-110">Code fixes or suggestions to resolve the warning or error are often provided through a light bulb icon.</span></span>

## <a name="avoid-using-default-in-process-session-state-mode"></a><span data-ttu-id="e86fc-111">Avoid using default (in-process) session state mode</span><span class="sxs-lookup"><span data-stu-id="e86fc-111">Avoid using default (in-process) session state mode</span></span>
### <a name="id"></a><span data-ttu-id="e86fc-112">ID</span><span class="sxs-lookup"><span data-stu-id="e86fc-112">ID</span></span>
<span data-ttu-id="e86fc-113">AP0000</span><span class="sxs-lookup"><span data-stu-id="e86fc-113">AP0000</span></span>

### <a name="description"></a><span data-ttu-id="e86fc-114">Description</span><span class="sxs-lookup"><span data-stu-id="e86fc-114">Description</span></span>
<span data-ttu-id="e86fc-115">If you use the default (in-process) session state mode for cloud applications, you can lose session state.</span><span class="sxs-lookup"><span data-stu-id="e86fc-115">If you use the default (in-process) session state mode for cloud applications, you can lose session state.</span></span>

<span data-ttu-id="e86fc-116">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="e86fc-116">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="e86fc-117">Reason</span><span class="sxs-lookup"><span data-stu-id="e86fc-117">Reason</span></span>
<span data-ttu-id="e86fc-118">By default, the session state mode specified in the web.config file is in-process.</span><span class="sxs-lookup"><span data-stu-id="e86fc-118">By default, the session state mode specified in the web.config file is in-process.</span></span> <span data-ttu-id="e86fc-119">Also, if no entry specified in the configuration file, the Session State mode defaults to in-process.</span><span class="sxs-lookup"><span data-stu-id="e86fc-119">Also, if no entry specified in the configuration file, the Session State mode defaults to in-process.</span></span> <span data-ttu-id="e86fc-120">The in-process mode stores session state in memory on the web server.</span><span class="sxs-lookup"><span data-stu-id="e86fc-120">The in-process mode stores session state in memory on the web server.</span></span> <span data-ttu-id="e86fc-121">When an instance is restarted or a new instance is used for load balancing or failover support, the session state stored in memory on the web server isn’t saved.</span><span class="sxs-lookup"><span data-stu-id="e86fc-121">When an instance is restarted or a new instance is used for load balancing or failover support, the session state stored in memory on the web server isn’t saved.</span></span> <span data-ttu-id="e86fc-122">This situation prevents the application from being scalable on the cloud.</span><span class="sxs-lookup"><span data-stu-id="e86fc-122">This situation prevents the application from being scalable on the cloud.</span></span>

<span data-ttu-id="e86fc-123">ASP.NET session state supports several different storage options for session state data: InProc, StateServer, SQLServer, Custom, and Off.</span><span class="sxs-lookup"><span data-stu-id="e86fc-123">ASP.NET session state supports several different storage options for session state data: InProc, StateServer, SQLServer, Custom, and Off.</span></span> <span data-ttu-id="e86fc-124">It’s recommended that you use Custom mode to host data on an external Session State store, such as [Azure Session State provider for Redis](http://go.microsoft.com/fwlink/?LinkId=401521).</span><span class="sxs-lookup"><span data-stu-id="e86fc-124">It’s recommended that you use Custom mode to host data on an external Session State store, such as [Azure Session State provider for Redis](http://go.microsoft.com/fwlink/?LinkId=401521).</span></span>

### <a name="solution"></a><span data-ttu-id="e86fc-125">Solution</span><span class="sxs-lookup"><span data-stu-id="e86fc-125">Solution</span></span>
<span data-ttu-id="e86fc-126">One recommended solution is to store session state on a managed cache service.</span><span class="sxs-lookup"><span data-stu-id="e86fc-126">One recommended solution is to store session state on a managed cache service.</span></span> <span data-ttu-id="e86fc-127">Learn how to use [Azure Session State provider for Redis](http://go.microsoft.com/fwlink/?LinkId=401521) to store your session state.</span><span class="sxs-lookup"><span data-stu-id="e86fc-127">Learn how to use [Azure Session State provider for Redis](http://go.microsoft.com/fwlink/?LinkId=401521) to store your session state.</span></span> <span data-ttu-id="e86fc-128">You can also store session state in other places to ensure your application is scalable on the cloud.</span><span class="sxs-lookup"><span data-stu-id="e86fc-128">You can also store session state in other places to ensure your application is scalable on the cloud.</span></span> <span data-ttu-id="e86fc-129">To learn more about alternative solutions please read [Session State Modes](https://msdn.microsoft.com/library/ms178586).</span><span class="sxs-lookup"><span data-stu-id="e86fc-129">To learn more about alternative solutions please read [Session State Modes](https://msdn.microsoft.com/library/ms178586).</span></span>

## <a name="run-method-should-not-be-async"></a><span data-ttu-id="e86fc-130">Run method should not be async</span><span class="sxs-lookup"><span data-stu-id="e86fc-130">Run method should not be async</span></span>
### <a name="id"></a><span data-ttu-id="e86fc-131">ID</span><span class="sxs-lookup"><span data-stu-id="e86fc-131">ID</span></span>
<span data-ttu-id="e86fc-132">AP1000</span><span class="sxs-lookup"><span data-stu-id="e86fc-132">AP1000</span></span>

### <a name="description"></a><span data-ttu-id="e86fc-133">Description</span><span class="sxs-lookup"><span data-stu-id="e86fc-133">Description</span></span>
<span data-ttu-id="e86fc-134">Create asynchronous methods (such as [await](https://msdn.microsoft.com/library/hh156528.aspx)) outside of the [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method and then call the async methods from [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx).</span><span class="sxs-lookup"><span data-stu-id="e86fc-134">Create asynchronous methods (such as [await](https://msdn.microsoft.com/library/hh156528.aspx)) outside of the [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method and then call the async methods from [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx).</span></span> <span data-ttu-id="e86fc-135">Declaring the [[Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method as async causes the worker role to enter a restart loop.</span><span class="sxs-lookup"><span data-stu-id="e86fc-135">Declaring the [[Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method as async causes the worker role to enter a restart loop.</span></span>

<span data-ttu-id="e86fc-136">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="e86fc-136">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="e86fc-137">Reason</span><span class="sxs-lookup"><span data-stu-id="e86fc-137">Reason</span></span>
<span data-ttu-id="e86fc-138">Calling async methods inside the [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method causes the cloud service runtime to recycle the worker role.</span><span class="sxs-lookup"><span data-stu-id="e86fc-138">Calling async methods inside the [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method causes the cloud service runtime to recycle the worker role.</span></span> <span data-ttu-id="e86fc-139">When a worker role starts, all program execution takes place inside the [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method.</span><span class="sxs-lookup"><span data-stu-id="e86fc-139">When a worker role starts, all program execution takes place inside the [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method.</span></span> <span data-ttu-id="e86fc-140">Exiting the [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method causes the worker role to restart.</span><span class="sxs-lookup"><span data-stu-id="e86fc-140">Exiting the [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method causes the worker role to restart.</span></span> <span data-ttu-id="e86fc-141">When the worker role runtime hits the async method, it dispatches all operations after the async method and then returns.</span><span class="sxs-lookup"><span data-stu-id="e86fc-141">When the worker role runtime hits the async method, it dispatches all operations after the async method and then returns.</span></span> <span data-ttu-id="e86fc-142">This causes the worker role to exit from the [[[[Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method and restart.</span><span class="sxs-lookup"><span data-stu-id="e86fc-142">This causes the worker role to exit from the [[[[Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method and restart.</span></span> <span data-ttu-id="e86fc-143">In the next iteration of execution, the worker role hits the async method again and restarts, causing the worker role to recycle again as well.</span><span class="sxs-lookup"><span data-stu-id="e86fc-143">In the next iteration of execution, the worker role hits the async method again and restarts, causing the worker role to recycle again as well.</span></span>

### <a name="solution"></a><span data-ttu-id="e86fc-144">Solution</span><span class="sxs-lookup"><span data-stu-id="e86fc-144">Solution</span></span>
<span data-ttu-id="e86fc-145">Place all async operations outside of the [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method.</span><span class="sxs-lookup"><span data-stu-id="e86fc-145">Place all async operations outside of the [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method.</span></span> <span data-ttu-id="e86fc-146">Then, call the refactored async method from inside the [[Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method, such as RunAsync().wait.</span><span class="sxs-lookup"><span data-stu-id="e86fc-146">Then, call the refactored async method from inside the [[Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method, such as RunAsync().wait.</span></span> <span data-ttu-id="e86fc-147">The Azure Code Analysis tool can help you fix this issue.</span><span class="sxs-lookup"><span data-stu-id="e86fc-147">The Azure Code Analysis tool can help you fix this issue.</span></span>

<span data-ttu-id="e86fc-148">The following code snippet demonstrates the code fix for this issue:</span><span class="sxs-lookup"><span data-stu-id="e86fc-148">The following code snippet demonstrates the code fix for this issue:</span></span>

```
public override void Run()
{
    RunAsync().Wait();
}

public async Task RunAsync()
{
    //Asynchronous operations code logic
    // This is a sample worker implementation. Replace with your logic.

    Trace.TraceInformation("WorkerRole1 entry point called");

    HttpClient client = new HttpClient();

    Task<string> urlString = client.GetStringAsync("http://msdn.microsoft.com");

    while (true)
    {
        Thread.Sleep(10000);
        Trace.TraceInformation("Working");

        string stream = await urlString;
    }

}
```

## <a name="use-service-bus-shared-access-signature-authentication"></a><span data-ttu-id="e86fc-149">Use Service Bus Shared Access Signature authentication</span><span class="sxs-lookup"><span data-stu-id="e86fc-149">Use Service Bus Shared Access Signature authentication</span></span>
### <a name="id"></a><span data-ttu-id="e86fc-150">ID</span><span class="sxs-lookup"><span data-stu-id="e86fc-150">ID</span></span>
<span data-ttu-id="e86fc-151">AP2000</span><span class="sxs-lookup"><span data-stu-id="e86fc-151">AP2000</span></span>

### <a name="description"></a><span data-ttu-id="e86fc-152">Description</span><span class="sxs-lookup"><span data-stu-id="e86fc-152">Description</span></span>
<span data-ttu-id="e86fc-153">Use Shared Access Signature (SAS) for authentication.</span><span class="sxs-lookup"><span data-stu-id="e86fc-153">Use Shared Access Signature (SAS) for authentication.</span></span> <span data-ttu-id="e86fc-154">Access Control Service (ACS) is being deprecated for service bus authentication.</span><span class="sxs-lookup"><span data-stu-id="e86fc-154">Access Control Service (ACS) is being deprecated for service bus authentication.</span></span>

<span data-ttu-id="e86fc-155">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="e86fc-155">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="e86fc-156">Reason</span><span class="sxs-lookup"><span data-stu-id="e86fc-156">Reason</span></span>
<span data-ttu-id="e86fc-157">For enhanced security, Azure Active Directory is replacing ACS authentication with SAS authentication.</span><span class="sxs-lookup"><span data-stu-id="e86fc-157">For enhanced security, Azure Active Directory is replacing ACS authentication with SAS authentication.</span></span> <span data-ttu-id="e86fc-158">See [Azure Active Directory is the future of ACS](http://blogs.technet.com/b/ad/archive/2013/06/22/azure-active-directory-is-the-future-of-acs.aspx) for information on the transition plan.</span><span class="sxs-lookup"><span data-stu-id="e86fc-158">See [Azure Active Directory is the future of ACS](http://blogs.technet.com/b/ad/archive/2013/06/22/azure-active-directory-is-the-future-of-acs.aspx) for information on the transition plan.</span></span>

### <a name="solution"></a><span data-ttu-id="e86fc-159">Solution</span><span class="sxs-lookup"><span data-stu-id="e86fc-159">Solution</span></span>
<span data-ttu-id="e86fc-160">Use SAS authentication in your apps.</span><span class="sxs-lookup"><span data-stu-id="e86fc-160">Use SAS authentication in your apps.</span></span> <span data-ttu-id="e86fc-161">The following example shows how to use an existing SAS token to access a service bus namespace or entity.</span><span class="sxs-lookup"><span data-stu-id="e86fc-161">The following example shows how to use an existing SAS token to access a service bus namespace or entity.</span></span>

```
MessagingFactory listenMF = MessagingFactory.Create(endpoints, new StaticSASTokenProvider(subscriptionToken));
SubscriptionClient sc = listenMF.CreateSubscriptionClient(topicPath, subscriptionName);
BrokeredMessage receivedMessage = sc.Receive();
```

<span data-ttu-id="e86fc-162">See the following topics for more information.</span><span class="sxs-lookup"><span data-stu-id="e86fc-162">See the following topics for more information.</span></span>

* <span data-ttu-id="e86fc-163">For an overview, see [Shared Access Signature Authentication with Service Bus](https://msdn.microsoft.com/library/dn170477.aspx)</span><span class="sxs-lookup"><span data-stu-id="e86fc-163">For an overview, see [Shared Access Signature Authentication with Service Bus](https://msdn.microsoft.com/library/dn170477.aspx)</span></span>
* [<span data-ttu-id="e86fc-164">How to use Shared Access Signature Authentication with Service Bus</span><span class="sxs-lookup"><span data-stu-id="e86fc-164">How to use Shared Access Signature Authentication with Service Bus</span></span>](https://msdn.microsoft.com/library/dn205161.aspx)
* <span data-ttu-id="e86fc-165">For a sample project, see [Using Shared Access Signature (SAS) authentication with Service Bus Subscriptions](http://code.msdn.microsoft.com/windowsazure/Using-Shared-Access-e605b37c)</span><span class="sxs-lookup"><span data-stu-id="e86fc-165">For a sample project, see [Using Shared Access Signature (SAS) authentication with Service Bus Subscriptions](http://code.msdn.microsoft.com/windowsazure/Using-Shared-Access-e605b37c)</span></span>

## <a name="consider-using-onmessage-method-to-avoid-receive-loop"></a><span data-ttu-id="e86fc-166">Consider using OnMessage method to avoid "receive loop"</span><span class="sxs-lookup"><span data-stu-id="e86fc-166">Consider using OnMessage method to avoid "receive loop"</span></span>
### <a name="id"></a><span data-ttu-id="e86fc-167">ID</span><span class="sxs-lookup"><span data-stu-id="e86fc-167">ID</span></span>
<span data-ttu-id="e86fc-168">AP2002</span><span class="sxs-lookup"><span data-stu-id="e86fc-168">AP2002</span></span>

### <a name="description"></a><span data-ttu-id="e86fc-169">Description</span><span class="sxs-lookup"><span data-stu-id="e86fc-169">Description</span></span>
<span data-ttu-id="e86fc-170">To avoid going into a "receive loop," calling the **OnMessage** method is a better solution for receiving messages than calling the **Receive** method.</span><span class="sxs-lookup"><span data-stu-id="e86fc-170">To avoid going into a "receive loop," calling the **OnMessage** method is a better solution for receiving messages than calling the **Receive** method.</span></span> <span data-ttu-id="e86fc-171">However, if you must use the **Receive** method, and you specify a non-default server wait time, make sure the server wait time is more than one minute.</span><span class="sxs-lookup"><span data-stu-id="e86fc-171">However, if you must use the **Receive** method, and you specify a non-default server wait time, make sure the server wait time is more than one minute.</span></span>

<span data-ttu-id="e86fc-172">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="e86fc-172">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="e86fc-173">Reason</span><span class="sxs-lookup"><span data-stu-id="e86fc-173">Reason</span></span>
<span data-ttu-id="e86fc-174">When calling **OnMessage**, the client starts an internal message pump that constantly polls the queue or subscription.</span><span class="sxs-lookup"><span data-stu-id="e86fc-174">When calling **OnMessage**, the client starts an internal message pump that constantly polls the queue or subscription.</span></span> <span data-ttu-id="e86fc-175">This message pump contains an infinite loop that issues a call to receive messages.</span><span class="sxs-lookup"><span data-stu-id="e86fc-175">This message pump contains an infinite loop that issues a call to receive messages.</span></span> <span data-ttu-id="e86fc-176">If the call times out, it issues a new call.</span><span class="sxs-lookup"><span data-stu-id="e86fc-176">If the call times out, it issues a new call.</span></span> <span data-ttu-id="e86fc-177">The timeout interval is determined by the value of the [OperationTimeout](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactorysettings.operationtimeout.aspx) property of the [MessagingFactory](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactory.aspx)that’s being used.</span><span class="sxs-lookup"><span data-stu-id="e86fc-177">The timeout interval is determined by the value of the [OperationTimeout](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactorysettings.operationtimeout.aspx) property of the [MessagingFactory](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactory.aspx)that’s being used.</span></span>

<span data-ttu-id="e86fc-178">The advantage of using **OnMessage** compared to **Receive** is that users don’t have to manually poll for messages, handle exceptions, process multiple messages in parallel, and complete the messages.</span><span class="sxs-lookup"><span data-stu-id="e86fc-178">The advantage of using **OnMessage** compared to **Receive** is that users don’t have to manually poll for messages, handle exceptions, process multiple messages in parallel, and complete the messages.</span></span>

<span data-ttu-id="e86fc-179">If you call **Receive** without using its default value, be sure the *ServerWaitTime* value is more than one minute.</span><span class="sxs-lookup"><span data-stu-id="e86fc-179">If you call **Receive** without using its default value, be sure the *ServerWaitTime* value is more than one minute.</span></span> <span data-ttu-id="e86fc-180">Setting *ServerWaitTime* to more than one minute prevents the server from timing out before the message is fully received.</span><span class="sxs-lookup"><span data-stu-id="e86fc-180">Setting *ServerWaitTime* to more than one minute prevents the server from timing out before the message is fully received.</span></span>

### <a name="solution"></a><span data-ttu-id="e86fc-181">Solution</span><span class="sxs-lookup"><span data-stu-id="e86fc-181">Solution</span></span>
<span data-ttu-id="e86fc-182">Please see the following code examples for recommended usages.</span><span class="sxs-lookup"><span data-stu-id="e86fc-182">Please see the following code examples for recommended usages.</span></span> <span data-ttu-id="e86fc-183">For more details, see [QueueClient.OnMessage Method (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.onmessage.aspx)and [QueueClient.Receive Method (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.receive.aspx).</span><span class="sxs-lookup"><span data-stu-id="e86fc-183">For more details, see [QueueClient.OnMessage Method (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.onmessage.aspx)and [QueueClient.Receive Method (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.receive.aspx).</span></span>

<span data-ttu-id="e86fc-184">To improve the performance of the Azure messaging infrastructure, see the design pattern [Asynchronous Messaging Primer](https://msdn.microsoft.com/library/dn589781.aspx).</span><span class="sxs-lookup"><span data-stu-id="e86fc-184">To improve the performance of the Azure messaging infrastructure, see the design pattern [Asynchronous Messaging Primer](https://msdn.microsoft.com/library/dn589781.aspx).</span></span>

<span data-ttu-id="e86fc-185">The following is an example of using **OnMessage** to receive messages.</span><span class="sxs-lookup"><span data-stu-id="e86fc-185">The following is an example of using **OnMessage** to receive messages.</span></span>

```
void ReceiveMessages()
{
    // Initialize message pump options.
    OnMessageOptions options = new OnMessageOptions();
    options.AutoComplete = true; // Indicates if the message-pump should call complete on messages after the callback has completed processing.
    options.MaxConcurrentCalls = 1; // Indicates the maximum number of concurrent calls to the callback the pump should initiate.
    options.ExceptionReceived += LogErrors; // Enables you to get notified of any errors encountered by the message pump.

    // Start receiving messages.
    QueueClient client = QueueClient.Create("myQueue");
    client.OnMessage((receivedMessage) => // Initiates the message pump and callback is invoked for each message that is recieved, calling close on the client will stop the pump.
    {
        // Process the message.
    }, options);
    Console.WriteLine("Press any key to exit.");
    Console.ReadKey();
```

<span data-ttu-id="e86fc-186">The following is an example of using **Receive** with the default server wait time.</span><span class="sxs-lookup"><span data-stu-id="e86fc-186">The following is an example of using **Receive** with the default server wait time.</span></span>

```
string connectionString =  
CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");

QueueClient Client =  
    QueueClient.CreateFromConnectionString(connectionString, "TestQueue");

while (true)  
{   
   BrokeredMessage message = Client.Receive();
   if (message != null)
   {
      try  
      {
         Console.WriteLine("Body: " + message.GetBody<string>());
         Console.WriteLine("MessageID: " + message.MessageId);
         Console.WriteLine("Test Property: " +  
            message.Properties["TestProperty"]);

         // Remove message from queue
         message.Complete();
      }

      catch (Exception)
      {
         // Indicate a problem, unlock message in queue
         message.Abandon();
      }
   }
```

<span data-ttu-id="e86fc-187">The following is an example of using **Receive** with a non-default server wait time.</span><span class="sxs-lookup"><span data-stu-id="e86fc-187">The following is an example of using **Receive** with a non-default server wait time.</span></span>

```
while (true)  
{   
   BrokeredMessage message = Client.Receive(new TimeSpan(0,1,0));

   if (message != null)
   {
      try  
      {
         Console.WriteLine("Body: " + message.GetBody<string>());
         Console.WriteLine("MessageID: " + message.MessageId);
         Console.WriteLine("Test Property: " +  
            message.Properties["TestProperty"]);

         // Remove message from queue
         message.Complete();
      }

      catch (Exception)
      {
         // Indicate a problem, unlock message in queue
         message.Abandon();
      }
   }
}
```
## <a name="consider-using-asynchronous-service-bus-methods"></a><span data-ttu-id="e86fc-188">Consider using asynchronous Service Bus methods</span><span class="sxs-lookup"><span data-stu-id="e86fc-188">Consider using asynchronous Service Bus methods</span></span>
### <a name="id"></a><span data-ttu-id="e86fc-189">ID</span><span class="sxs-lookup"><span data-stu-id="e86fc-189">ID</span></span>
<span data-ttu-id="e86fc-190">AP2003</span><span class="sxs-lookup"><span data-stu-id="e86fc-190">AP2003</span></span>

### <a name="description"></a><span data-ttu-id="e86fc-191">Description</span><span class="sxs-lookup"><span data-stu-id="e86fc-191">Description</span></span>
<span data-ttu-id="e86fc-192">Use asynchronous Service Bus methods to improve performance with brokered messaging.</span><span class="sxs-lookup"><span data-stu-id="e86fc-192">Use asynchronous Service Bus methods to improve performance with brokered messaging.</span></span>

<span data-ttu-id="e86fc-193">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="e86fc-193">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="e86fc-194">Reason</span><span class="sxs-lookup"><span data-stu-id="e86fc-194">Reason</span></span>
<span data-ttu-id="e86fc-195">Using asynchronous methods enables application program concurrency because executing each call doesn’t block the main thread.</span><span class="sxs-lookup"><span data-stu-id="e86fc-195">Using asynchronous methods enables application program concurrency because executing each call doesn’t block the main thread.</span></span> <span data-ttu-id="e86fc-196">When using Service Bus messaging methods, performing an operation (send, receive, delete, etc.) takes time.</span><span class="sxs-lookup"><span data-stu-id="e86fc-196">When using Service Bus messaging methods, performing an operation (send, receive, delete, etc.) takes time.</span></span> <span data-ttu-id="e86fc-197">This time includes the processing of the operation by the Service Bus service in addition to the latency of the request and the reply.</span><span class="sxs-lookup"><span data-stu-id="e86fc-197">This time includes the processing of the operation by the Service Bus service in addition to the latency of the request and the reply.</span></span> <span data-ttu-id="e86fc-198">To increase the number of operations per time, operations must execute concurrently.</span><span class="sxs-lookup"><span data-stu-id="e86fc-198">To increase the number of operations per time, operations must execute concurrently.</span></span> <span data-ttu-id="e86fc-199">For more information please refer to [Best Practices for Performance Improvements Using Service Bus Brokered Messaging](https://msdn.microsoft.com/library/azure/hh528527.aspx).</span><span class="sxs-lookup"><span data-stu-id="e86fc-199">For more information please refer to [Best Practices for Performance Improvements Using Service Bus Brokered Messaging](https://msdn.microsoft.com/library/azure/hh528527.aspx).</span></span>

### <a name="solution"></a><span data-ttu-id="e86fc-200">Solution</span><span class="sxs-lookup"><span data-stu-id="e86fc-200">Solution</span></span>
<span data-ttu-id="e86fc-201">See [QueueClient Class (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.aspx) for information about how to use the recommended asynchronous method.</span><span class="sxs-lookup"><span data-stu-id="e86fc-201">See [QueueClient Class (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.aspx) for information about how to use the recommended asynchronous method.</span></span>

<span data-ttu-id="e86fc-202">To improve the performance of the Azure messaging infrastructure, see the design pattern [Asynchronous Messaging Primer](https://msdn.microsoft.com/library/dn589781.aspx).</span><span class="sxs-lookup"><span data-stu-id="e86fc-202">To improve the performance of the Azure messaging infrastructure, see the design pattern [Asynchronous Messaging Primer](https://msdn.microsoft.com/library/dn589781.aspx).</span></span>

## <a name="consider-partitioning-service-bus-queues-and-topics"></a><span data-ttu-id="e86fc-203">Consider partitioning Service Bus queues and topics</span><span class="sxs-lookup"><span data-stu-id="e86fc-203">Consider partitioning Service Bus queues and topics</span></span>
### <a name="id"></a><span data-ttu-id="e86fc-204">ID</span><span class="sxs-lookup"><span data-stu-id="e86fc-204">ID</span></span>
<span data-ttu-id="e86fc-205">AP2004</span><span class="sxs-lookup"><span data-stu-id="e86fc-205">AP2004</span></span>

### <a name="description"></a><span data-ttu-id="e86fc-206">Description</span><span class="sxs-lookup"><span data-stu-id="e86fc-206">Description</span></span>
<span data-ttu-id="e86fc-207">Partition Service Bus queues and topics for better performance with Service Bus messaging.</span><span class="sxs-lookup"><span data-stu-id="e86fc-207">Partition Service Bus queues and topics for better performance with Service Bus messaging.</span></span>

<span data-ttu-id="e86fc-208">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="e86fc-208">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="e86fc-209">Reason</span><span class="sxs-lookup"><span data-stu-id="e86fc-209">Reason</span></span>
<span data-ttu-id="e86fc-210">Partitioning Service Bus queues and topics increases performance throughput and service availability because the overall throughput of a partitioned queue or topic is no longer limited by the performance of a single message broker or messaging store.</span><span class="sxs-lookup"><span data-stu-id="e86fc-210">Partitioning Service Bus queues and topics increases performance throughput and service availability because the overall throughput of a partitioned queue or topic is no longer limited by the performance of a single message broker or messaging store.</span></span> <span data-ttu-id="e86fc-211">In addition, a temporary outage of a messaging store doesn’t make a partitioned queue or topic unavailable.</span><span class="sxs-lookup"><span data-stu-id="e86fc-211">In addition, a temporary outage of a messaging store doesn’t make a partitioned queue or topic unavailable.</span></span> <span data-ttu-id="e86fc-212">For more information, see [Partitioning Messaging Entities](https://msdn.microsoft.com/library/azure/dn520246.aspx).</span><span class="sxs-lookup"><span data-stu-id="e86fc-212">For more information, see [Partitioning Messaging Entities](https://msdn.microsoft.com/library/azure/dn520246.aspx).</span></span>

### <a name="solution"></a><span data-ttu-id="e86fc-213">Solution</span><span class="sxs-lookup"><span data-stu-id="e86fc-213">Solution</span></span>
<span data-ttu-id="e86fc-214">The following code snippet shows how to partition messaging entities.</span><span class="sxs-lookup"><span data-stu-id="e86fc-214">The following code snippet shows how to partition messaging entities.</span></span>

```
// Create partitioned topic.
NamespaceManager ns = NamespaceManager.CreateFromConnectionString(myConnectionString);
TopicDescription td = new TopicDescription(TopicName);
td.EnablePartitioning = true;
ns.CreateTopic(td);
```

<span data-ttu-id="e86fc-215">For more information, see [Partitioned Service Bus Queues and Topics | Microsoft Azure Blog](https://azure.microsoft.com/blog/2013/10/29/partitioned-service-bus-queues-and-topics/) and check out the [Microsoft Azure Service Bus Partitioned Queue](https://code.msdn.microsoft.com/windowsazure/Service-Bus-Partitioned-7dfd3f1f) sample.</span><span class="sxs-lookup"><span data-stu-id="e86fc-215">For more information, see [Partitioned Service Bus Queues and Topics | Microsoft Azure Blog](https://azure.microsoft.com/blog/2013/10/29/partitioned-service-bus-queues-and-topics/) and check out the [Microsoft Azure Service Bus Partitioned Queue](https://code.msdn.microsoft.com/windowsazure/Service-Bus-Partitioned-7dfd3f1f) sample.</span></span>

## <a name="do-not-set-sharedaccessstarttime"></a><span data-ttu-id="e86fc-216">Do not set SharedAccessStartTime</span><span class="sxs-lookup"><span data-stu-id="e86fc-216">Do not set SharedAccessStartTime</span></span>
### <a name="id"></a><span data-ttu-id="e86fc-217">ID</span><span class="sxs-lookup"><span data-stu-id="e86fc-217">ID</span></span>
<span data-ttu-id="e86fc-218">AP3001</span><span class="sxs-lookup"><span data-stu-id="e86fc-218">AP3001</span></span>

### <a name="description"></a><span data-ttu-id="e86fc-219">Description</span><span class="sxs-lookup"><span data-stu-id="e86fc-219">Description</span></span>
<span data-ttu-id="e86fc-220">You should avoid using SharedAccessStartTimeset to the current time to immediately start the Shared Access policy.</span><span class="sxs-lookup"><span data-stu-id="e86fc-220">You should avoid using SharedAccessStartTimeset to the current time to immediately start the Shared Access policy.</span></span> <span data-ttu-id="e86fc-221">You only need to set this property if you want to start the Shared Access policy at a later time.</span><span class="sxs-lookup"><span data-stu-id="e86fc-221">You only need to set this property if you want to start the Shared Access policy at a later time.</span></span>

<span data-ttu-id="e86fc-222">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="e86fc-222">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="e86fc-223">Reason</span><span class="sxs-lookup"><span data-stu-id="e86fc-223">Reason</span></span>
<span data-ttu-id="e86fc-224">Clock synchronization causes a slight time difference among datacenters.</span><span class="sxs-lookup"><span data-stu-id="e86fc-224">Clock synchronization causes a slight time difference among datacenters.</span></span> <span data-ttu-id="e86fc-225">For example, you would logically think setting the start time of a storage SAS policy as the current time by using DateTime.Now or a similar method will cause the SAS policy to take effect immediately.</span><span class="sxs-lookup"><span data-stu-id="e86fc-225">For example, you would logically think setting the start time of a storage SAS policy as the current time by using DateTime.Now or a similar method will cause the SAS policy to take effect immediately.</span></span> <span data-ttu-id="e86fc-226">However, the slight time differences between datacenters can cause problems with this since some datacenter times might be slightly later than the start time, while others ahead of it.</span><span class="sxs-lookup"><span data-stu-id="e86fc-226">However, the slight time differences between datacenters can cause problems with this since some datacenter times might be slightly later than the start time, while others ahead of it.</span></span> <span data-ttu-id="e86fc-227">As a result, the SAS policy can expire quickly (or even immediately) if the policy lifetime is set too short.</span><span class="sxs-lookup"><span data-stu-id="e86fc-227">As a result, the SAS policy can expire quickly (or even immediately) if the policy lifetime is set too short.</span></span>

<span data-ttu-id="e86fc-228">For more guidance on using Shared Access Signature on Azure storage, see [Introducing Table SAS (Shared Access Signature), Queue SAS and update to Blob SAS - Microsoft Azure Storage Team Blog - Site Home - MSDN Blogs](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx).</span><span class="sxs-lookup"><span data-stu-id="e86fc-228">For more guidance on using Shared Access Signature on Azure storage, see [Introducing Table SAS (Shared Access Signature), Queue SAS and update to Blob SAS - Microsoft Azure Storage Team Blog - Site Home - MSDN Blogs](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx).</span></span>

### <a name="solution"></a><span data-ttu-id="e86fc-229">Solution</span><span class="sxs-lookup"><span data-stu-id="e86fc-229">Solution</span></span>
<span data-ttu-id="e86fc-230">Remove the statement that sets the start time of the shared access policy.</span><span class="sxs-lookup"><span data-stu-id="e86fc-230">Remove the statement that sets the start time of the shared access policy.</span></span> <span data-ttu-id="e86fc-231">The Azure Code Analysis tool provides a fix for this issue.</span><span class="sxs-lookup"><span data-stu-id="e86fc-231">The Azure Code Analysis tool provides a fix for this issue.</span></span> <span data-ttu-id="e86fc-232">For more information on security management, please see the design pattern [Valet Key Pattern](https://msdn.microsoft.com/library/dn568102.aspx).</span><span class="sxs-lookup"><span data-stu-id="e86fc-232">For more information on security management, please see the design pattern [Valet Key Pattern](https://msdn.microsoft.com/library/dn568102.aspx).</span></span>

<span data-ttu-id="e86fc-233">The following code snippet demonstrates the code fix for this issue.</span><span class="sxs-lookup"><span data-stu-id="e86fc-233">The following code snippet demonstrates the code fix for this issue.</span></span>

```
// The shared access policy provides  
// read/write access to the container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // To ensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
   SharedAccessExpiryTime = DateTime.UtcNow.AddHours(10),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

## <a name="shared-access-policy-expiry-time-must-be-more-than-five-minutes"></a><span data-ttu-id="e86fc-234">Shared Access Policy expiry time must be more than five minutes</span><span class="sxs-lookup"><span data-stu-id="e86fc-234">Shared Access Policy expiry time must be more than five minutes</span></span>
### <a name="id"></a><span data-ttu-id="e86fc-235">ID</span><span class="sxs-lookup"><span data-stu-id="e86fc-235">ID</span></span>
<span data-ttu-id="e86fc-236">AP3002</span><span class="sxs-lookup"><span data-stu-id="e86fc-236">AP3002</span></span>

### <a name="description"></a><span data-ttu-id="e86fc-237">Description</span><span class="sxs-lookup"><span data-stu-id="e86fc-237">Description</span></span>
<span data-ttu-id="e86fc-238">There can be as much as a five minute difference in clocks among datacenters at different locations due to a condition known as "clock skew."</span><span class="sxs-lookup"><span data-stu-id="e86fc-238">There can be as much as a five minute difference in clocks among datacenters at different locations due to a condition known as "clock skew."</span></span> <span data-ttu-id="e86fc-239">To prevent the SAS policy token from expiring earlier than planned, set the expiry time to be more than five minutes.</span><span class="sxs-lookup"><span data-stu-id="e86fc-239">To prevent the SAS policy token from expiring earlier than planned, set the expiry time to be more than five minutes.</span></span>

<span data-ttu-id="e86fc-240">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="e86fc-240">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="e86fc-241">Reason</span><span class="sxs-lookup"><span data-stu-id="e86fc-241">Reason</span></span>
<span data-ttu-id="e86fc-242">Datacenters at different locations around the world synchronize by a clock signal.</span><span class="sxs-lookup"><span data-stu-id="e86fc-242">Datacenters at different locations around the world synchronize by a clock signal.</span></span> <span data-ttu-id="e86fc-243">Because it takes time for clock signal to travel to different locations, there can be a time variance between datacenters at different geographical locations although everything is supposedly synchronized.</span><span class="sxs-lookup"><span data-stu-id="e86fc-243">Because it takes time for clock signal to travel to different locations, there can be a time variance between datacenters at different geographical locations although everything is supposedly synchronized.</span></span> <span data-ttu-id="e86fc-244">This time difference can affect the Shared Access policy start time and expiration interval.</span><span class="sxs-lookup"><span data-stu-id="e86fc-244">This time difference can affect the Shared Access policy start time and expiration interval.</span></span> <span data-ttu-id="e86fc-245">Therefore, to ensure Shared Access policy takes effect immediately, don’t specify the start time.</span><span class="sxs-lookup"><span data-stu-id="e86fc-245">Therefore, to ensure Shared Access policy takes effect immediately, don’t specify the start time.</span></span> <span data-ttu-id="e86fc-246">In addition, make sure the expiration time is more than 5 minutes to prevent early timeout.</span><span class="sxs-lookup"><span data-stu-id="e86fc-246">In addition, make sure the expiration time is more than 5 minutes to prevent early timeout.</span></span>

<span data-ttu-id="e86fc-247">For more information about using Shared Access Signature on Azure storage, see [Introducing Table SAS (Shared Access Signature), Queue SAS and update to Blob SAS - Microsoft Azure Storage Team Blog - Site Home - MSDN Blogs](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx).</span><span class="sxs-lookup"><span data-stu-id="e86fc-247">For more information about using Shared Access Signature on Azure storage, see [Introducing Table SAS (Shared Access Signature), Queue SAS and update to Blob SAS - Microsoft Azure Storage Team Blog - Site Home - MSDN Blogs](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx).</span></span>

### <a name="solution"></a><span data-ttu-id="e86fc-248">Solution</span><span class="sxs-lookup"><span data-stu-id="e86fc-248">Solution</span></span>
<span data-ttu-id="e86fc-249">For more information on security management, see the design pattern [Valet Key Pattern](https://msdn.microsoft.com/library/dn568102.aspx).</span><span class="sxs-lookup"><span data-stu-id="e86fc-249">For more information on security management, see the design pattern [Valet Key Pattern](https://msdn.microsoft.com/library/dn568102.aspx).</span></span>

<span data-ttu-id="e86fc-250">The following is an example of not specifying a Shared Access policy start time.</span><span class="sxs-lookup"><span data-stu-id="e86fc-250">The following is an example of not specifying a Shared Access policy start time.</span></span>

```
// The shared access policy provides  
// read/write access to the container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // To ensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
   SharedAccessExpiryTime = DateTime.UtcNow.AddHours(10),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

<span data-ttu-id="e86fc-251">The following is an example of specifying a Shared Access policy start time with a policy expiration duration greater than five minutes.</span><span class="sxs-lookup"><span data-stu-id="e86fc-251">The following is an example of specifying a Shared Access policy start time with a policy expiration duration greater than five minutes.</span></span>

```
// The shared access policy provides  
// read/write access to the container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // To ensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
  SharedAccessStartTime = new DateTime(2014,1,20),   
 SharedAccessExpiryTime = new DateTime(2014, 1, 21),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

<span data-ttu-id="e86fc-252">For more information, see [Create and Use a Shared Access Signature](https://msdn.microsoft.com/library/azure/jj721951.aspx).</span><span class="sxs-lookup"><span data-stu-id="e86fc-252">For more information, see [Create and Use a Shared Access Signature](https://msdn.microsoft.com/library/azure/jj721951.aspx).</span></span>

## <a name="use-cloudconfigurationmanager"></a><span data-ttu-id="e86fc-253">Use CloudConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="e86fc-253">Use CloudConfigurationManager</span></span>
### <a name="id"></a><span data-ttu-id="e86fc-254">ID</span><span class="sxs-lookup"><span data-stu-id="e86fc-254">ID</span></span>
<span data-ttu-id="e86fc-255">AP4000</span><span class="sxs-lookup"><span data-stu-id="e86fc-255">AP4000</span></span>

### <a name="description"></a><span data-ttu-id="e86fc-256">Description</span><span class="sxs-lookup"><span data-stu-id="e86fc-256">Description</span></span>
<span data-ttu-id="e86fc-257">Using the [ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) class for projects such as Azure Website and Azure mobile services won't introduce runtime issues.</span><span class="sxs-lookup"><span data-stu-id="e86fc-257">Using the [ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) class for projects such as Azure Website and Azure mobile services won't introduce runtime issues.</span></span> <span data-ttu-id="e86fc-258">As a best practice, however, it's a good idea to use Cloud[ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) as a unified way of managing configurations for all Azure Cloud applications.</span><span class="sxs-lookup"><span data-stu-id="e86fc-258">As a best practice, however, it's a good idea to use Cloud[ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) as a unified way of managing configurations for all Azure Cloud applications.</span></span>

<span data-ttu-id="e86fc-259">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="e86fc-259">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="e86fc-260">Reason</span><span class="sxs-lookup"><span data-stu-id="e86fc-260">Reason</span></span>
<span data-ttu-id="e86fc-261">CloudConfigurationManager reads the configuration file appropriate to the application environment.</span><span class="sxs-lookup"><span data-stu-id="e86fc-261">CloudConfigurationManager reads the configuration file appropriate to the application environment.</span></span>

[<span data-ttu-id="e86fc-262">CloudConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="e86fc-262">CloudConfigurationManager</span></span>](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.cloudconfigurationmanager.aspx)

### <a name="solution"></a><span data-ttu-id="e86fc-263">Solution</span><span class="sxs-lookup"><span data-stu-id="e86fc-263">Solution</span></span>
<span data-ttu-id="e86fc-264">Refactor your code to use the [CloudConfigurationManager Class](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.cloudconfigurationmanager.aspx).</span><span class="sxs-lookup"><span data-stu-id="e86fc-264">Refactor your code to use the [CloudConfigurationManager Class](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.cloudconfigurationmanager.aspx).</span></span> <span data-ttu-id="e86fc-265">A code fix for this issue is provided by the Azure Code Analysis tool.</span><span class="sxs-lookup"><span data-stu-id="e86fc-265">A code fix for this issue is provided by the Azure Code Analysis tool.</span></span>

<span data-ttu-id="e86fc-266">The following code snippet demonstrates the code fix for this issue.</span><span class="sxs-lookup"><span data-stu-id="e86fc-266">The following code snippet demonstrates the code fix for this issue.</span></span> <span data-ttu-id="e86fc-267">Replace</span><span class="sxs-lookup"><span data-stu-id="e86fc-267">Replace</span></span>

`var settings = ConfigurationManager.AppSettings["mySettings"];`

<span data-ttu-id="e86fc-268">with</span><span class="sxs-lookup"><span data-stu-id="e86fc-268">with</span></span>

`var settings = CloudConfigurationManager.GetSetting("mySettings");`

<span data-ttu-id="e86fc-269">Here's an example of how to store the configuration setting in a App.config or Web.config file.</span><span class="sxs-lookup"><span data-stu-id="e86fc-269">Here's an example of how to store the configuration setting in a App.config or Web.config file.</span></span> <span data-ttu-id="e86fc-270">Add the settings to the appSettings section of the configuration file.</span><span class="sxs-lookup"><span data-stu-id="e86fc-270">Add the settings to the appSettings section of the configuration file.</span></span> <span data-ttu-id="e86fc-271">The following is the Web.config file for the previous code example.</span><span class="sxs-lookup"><span data-stu-id="e86fc-271">The following is the Web.config file for the previous code example.</span></span>

```
<appSettings>
    <add key="webpages:Version" value="3.0.0.0" />
    <add key="webpages:Enabled" value="false" />
    <add key="ClientValidationEnabled" value="true" />
    <add key="UnobtrusiveJavaScriptEnabled" value="true" />
    <add key="mySettings" value="[put_your_setting_here]"/>
  </appSettings>  
```

## <a name="avoid-using-hard-coded-connection-strings"></a><span data-ttu-id="e86fc-272">Avoid using hard-coded connection strings</span><span class="sxs-lookup"><span data-stu-id="e86fc-272">Avoid using hard-coded connection strings</span></span>
### <a name="id"></a><span data-ttu-id="e86fc-273">ID</span><span class="sxs-lookup"><span data-stu-id="e86fc-273">ID</span></span>
<span data-ttu-id="e86fc-274">AP4001</span><span class="sxs-lookup"><span data-stu-id="e86fc-274">AP4001</span></span>

### <a name="description"></a><span data-ttu-id="e86fc-275">Description</span><span class="sxs-lookup"><span data-stu-id="e86fc-275">Description</span></span>
<span data-ttu-id="e86fc-276">If you use hard-coded connection strings and you need to update them later, you’ll have to make changes to your source code and recompile the application.</span><span class="sxs-lookup"><span data-stu-id="e86fc-276">If you use hard-coded connection strings and you need to update them later, you’ll have to make changes to your source code and recompile the application.</span></span> <span data-ttu-id="e86fc-277">However, if you store your connection strings in a configuration file, you can change them later by simply updating the configuration file.</span><span class="sxs-lookup"><span data-stu-id="e86fc-277">However, if you store your connection strings in a configuration file, you can change them later by simply updating the configuration file.</span></span>

<span data-ttu-id="e86fc-278">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="e86fc-278">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="e86fc-279">Reason</span><span class="sxs-lookup"><span data-stu-id="e86fc-279">Reason</span></span>
<span data-ttu-id="e86fc-280">Hard-coding connection strings is a bad practice because it introduces problems when connection strings need to be changed quickly.</span><span class="sxs-lookup"><span data-stu-id="e86fc-280">Hard-coding connection strings is a bad practice because it introduces problems when connection strings need to be changed quickly.</span></span> <span data-ttu-id="e86fc-281">In addition, if the project needs to be checked in to source control, hard-coded connection strings introduce security vulnerabilities since the strings can be viewed in the source code.</span><span class="sxs-lookup"><span data-stu-id="e86fc-281">In addition, if the project needs to be checked in to source control, hard-coded connection strings introduce security vulnerabilities since the strings can be viewed in the source code.</span></span>

### <a name="solution"></a><span data-ttu-id="e86fc-282">Solution</span><span class="sxs-lookup"><span data-stu-id="e86fc-282">Solution</span></span>
<span data-ttu-id="e86fc-283">Store connection strings in the configuration files or Azure environments.</span><span class="sxs-lookup"><span data-stu-id="e86fc-283">Store connection strings in the configuration files or Azure environments.</span></span>

* <span data-ttu-id="e86fc-284">For standalone applications, use app.config to store connection string settings.</span><span class="sxs-lookup"><span data-stu-id="e86fc-284">For standalone applications, use app.config to store connection string settings.</span></span>
* <span data-ttu-id="e86fc-285">For IIS-hosted web applications, use web.config to store connection strings.</span><span class="sxs-lookup"><span data-stu-id="e86fc-285">For IIS-hosted web applications, use web.config to store connection strings.</span></span>
* <span data-ttu-id="e86fc-286">For ASP.NET vNext applications, use configuration.json to store connection strings.</span><span class="sxs-lookup"><span data-stu-id="e86fc-286">For ASP.NET vNext applications, use configuration.json to store connection strings.</span></span>

<span data-ttu-id="e86fc-287">For information on using configurations files such as web.config or app.config, see [ASP.NET Web Configuration Guidelines](https://msdn.microsoft.com/library/vstudio/ff400235\(v=vs.100\).aspx).</span><span class="sxs-lookup"><span data-stu-id="e86fc-287">For information on using configurations files such as web.config or app.config, see [ASP.NET Web Configuration Guidelines](https://msdn.microsoft.com/library/vstudio/ff400235\(v=vs.100\).aspx).</span></span> <span data-ttu-id="e86fc-288">For information on how Azure environment variables work, see [Azure Web Sites: How Application Strings and Connection Strings Work](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/).</span><span class="sxs-lookup"><span data-stu-id="e86fc-288">For information on how Azure environment variables work, see [Azure Web Sites: How Application Strings and Connection Strings Work](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/).</span></span> <span data-ttu-id="e86fc-289">For information on storing connection string in source control, see [avoid putting sensitive information such as connection strings in files that are stored in source code repository](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control).</span><span class="sxs-lookup"><span data-stu-id="e86fc-289">For information on storing connection string in source control, see [avoid putting sensitive information such as connection strings in files that are stored in source code repository](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control).</span></span>

## <a name="use-diagnostics-configuration-file"></a><span data-ttu-id="e86fc-290">Use diagnostics configuration file</span><span class="sxs-lookup"><span data-stu-id="e86fc-290">Use diagnostics configuration file</span></span>
### <a name="id"></a><span data-ttu-id="e86fc-291">ID</span><span class="sxs-lookup"><span data-stu-id="e86fc-291">ID</span></span>
<span data-ttu-id="e86fc-292">AP5000</span><span class="sxs-lookup"><span data-stu-id="e86fc-292">AP5000</span></span>

### <a name="description"></a><span data-ttu-id="e86fc-293">Description</span><span class="sxs-lookup"><span data-stu-id="e86fc-293">Description</span></span>
<span data-ttu-id="e86fc-294">Instead of configuring diagnostics settings in your code such as by using the Microsoft.WindowsAzure.Diagnostics programming API, you should configure diagnostics settings in the diagnostics.wadcfg file.</span><span class="sxs-lookup"><span data-stu-id="e86fc-294">Instead of configuring diagnostics settings in your code such as by using the Microsoft.WindowsAzure.Diagnostics programming API, you should configure diagnostics settings in the diagnostics.wadcfg file.</span></span> <span data-ttu-id="e86fc-295">(Or, diagnostics.wadcfgx if you use Azure SDK 2.5).</span><span class="sxs-lookup"><span data-stu-id="e86fc-295">(Or, diagnostics.wadcfgx if you use Azure SDK 2.5).</span></span> <span data-ttu-id="e86fc-296">By doing this, you can change diagnostics settings without having to recompile your code.</span><span class="sxs-lookup"><span data-stu-id="e86fc-296">By doing this, you can change diagnostics settings without having to recompile your code.</span></span>

<span data-ttu-id="e86fc-297">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="e86fc-297">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="e86fc-298">Reason</span><span class="sxs-lookup"><span data-stu-id="e86fc-298">Reason</span></span>
<span data-ttu-id="e86fc-299">Before Azure SDK 2.5 (which uses Azure diagnostics 1.3), Azure Diagnostics (WAD) could be configured by using several different methods: adding it to the configuration blob in storage, by using imperative code, declarative configuration, or the default configuration.</span><span class="sxs-lookup"><span data-stu-id="e86fc-299">Before Azure SDK 2.5 (which uses Azure diagnostics 1.3), Azure Diagnostics (WAD) could be configured by using several different methods: adding it to the configuration blob in storage, by using imperative code, declarative configuration, or the default configuration.</span></span> <span data-ttu-id="e86fc-300">However, the preferred way to configure diagnostics is to use an XML configuration file (diagnostics.wadcfg or diagnositcs.wadcfgx for SDK 2.5 and later) in the application project.</span><span class="sxs-lookup"><span data-stu-id="e86fc-300">However, the preferred way to configure diagnostics is to use an XML configuration file (diagnostics.wadcfg or diagnositcs.wadcfgx for SDK 2.5 and later) in the application project.</span></span> <span data-ttu-id="e86fc-301">In this approach, the diagnostics.wadcfg file completely defines the configuration and can be updated and redeployed at will.</span><span class="sxs-lookup"><span data-stu-id="e86fc-301">In this approach, the diagnostics.wadcfg file completely defines the configuration and can be updated and redeployed at will.</span></span> <span data-ttu-id="e86fc-302">Mixing the use of the diagnostics.wadcfg configuration file with the programmatic methods of setting configurations by using the [DiagnosticMonitor](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.diagnosticmonitor.aspx)or [RoleInstanceDiagnosticManager](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.management.roleinstancediagnosticmanager.aspx)classes can lead to confusion.</span><span class="sxs-lookup"><span data-stu-id="e86fc-302">Mixing the use of the diagnostics.wadcfg configuration file with the programmatic methods of setting configurations by using the [DiagnosticMonitor](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.diagnosticmonitor.aspx)or [RoleInstanceDiagnosticManager](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.management.roleinstancediagnosticmanager.aspx)classes can lead to confusion.</span></span> <span data-ttu-id="e86fc-303">See [Initialize or Change Azure Diagnostics Configuration](https://msdn.microsoft.com/library/azure/hh411537.aspx) for more information.</span><span class="sxs-lookup"><span data-stu-id="e86fc-303">See [Initialize or Change Azure Diagnostics Configuration](https://msdn.microsoft.com/library/azure/hh411537.aspx) for more information.</span></span>

<span data-ttu-id="e86fc-304">Beginning with WAD 1.3 (included with Azure SDK 2.5), it’s no longer possible to use code to configure diagnostics.</span><span class="sxs-lookup"><span data-stu-id="e86fc-304">Beginning with WAD 1.3 (included with Azure SDK 2.5), it’s no longer possible to use code to configure diagnostics.</span></span> <span data-ttu-id="e86fc-305">As a result, you can only provide the configuration when applying or updating the diagnostics extension.</span><span class="sxs-lookup"><span data-stu-id="e86fc-305">As a result, you can only provide the configuration when applying or updating the diagnostics extension.</span></span>

### <a name="solution"></a><span data-ttu-id="e86fc-306">Solution</span><span class="sxs-lookup"><span data-stu-id="e86fc-306">Solution</span></span>
<span data-ttu-id="e86fc-307">Use the diagnostics configuration designer to move diagnostic settings to the diagnostics configuration file (diagnositcs.wadcfg or diagnositcs.wadcfgx for SDK 2.5 and later).</span><span class="sxs-lookup"><span data-stu-id="e86fc-307">Use the diagnostics configuration designer to move diagnostic settings to the diagnostics configuration file (diagnositcs.wadcfg or diagnositcs.wadcfgx for SDK 2.5 and later).</span></span> <span data-ttu-id="e86fc-308">It’s also recommended that you install [Azure SDK 2.5](http://go.microsoft.com/fwlink/?LinkId=513188) and use the latest diagnostics feature.</span><span class="sxs-lookup"><span data-stu-id="e86fc-308">It’s also recommended that you install [Azure SDK 2.5](http://go.microsoft.com/fwlink/?LinkId=513188) and use the latest diagnostics feature.</span></span>

1. <span data-ttu-id="e86fc-309">On the shortcut menu for the role that you want to configure, choose Properties, and then choose the Configuration tab.</span><span class="sxs-lookup"><span data-stu-id="e86fc-309">On the shortcut menu for the role that you want to configure, choose Properties, and then choose the Configuration tab.</span></span>
2. <span data-ttu-id="e86fc-310">In the **Diagnostics** section, make sure that the **Enable Diagnostics** check box is selected.</span><span class="sxs-lookup"><span data-stu-id="e86fc-310">In the **Diagnostics** section, make sure that the **Enable Diagnostics** check box is selected.</span></span>
3. <span data-ttu-id="e86fc-311">Choose the **Configure** button.</span><span class="sxs-lookup"><span data-stu-id="e86fc-311">Choose the **Configure** button.</span></span>

   ![Accessing the Enable Diagnostics option](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-optimizing-azure-code-in-visual-studio/IC796660.png)

   <span data-ttu-id="e86fc-313">See [Configuring Diagnostics for Azure Cloud Services and Virtual Machines](vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) for more information.</span><span class="sxs-lookup"><span data-stu-id="e86fc-313">See [Configuring Diagnostics for Azure Cloud Services and Virtual Machines](vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) for more information.</span></span>

## <a name="avoid-declaring-dbcontext-objects-as-static"></a><span data-ttu-id="e86fc-314">Avoid declaring DbContext objects as static</span><span class="sxs-lookup"><span data-stu-id="e86fc-314">Avoid declaring DbContext objects as static</span></span>
### <a name="id"></a><span data-ttu-id="e86fc-315">ID</span><span class="sxs-lookup"><span data-stu-id="e86fc-315">ID</span></span>
<span data-ttu-id="e86fc-316">AP6000</span><span class="sxs-lookup"><span data-stu-id="e86fc-316">AP6000</span></span>

### <a name="description"></a><span data-ttu-id="e86fc-317">Description</span><span class="sxs-lookup"><span data-stu-id="e86fc-317">Description</span></span>
<span data-ttu-id="e86fc-318">To save memory, avoid declaring DBContext objects as static.</span><span class="sxs-lookup"><span data-stu-id="e86fc-318">To save memory, avoid declaring DBContext objects as static.</span></span>

<span data-ttu-id="e86fc-319">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="e86fc-319">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="e86fc-320">Reason</span><span class="sxs-lookup"><span data-stu-id="e86fc-320">Reason</span></span>
<span data-ttu-id="e86fc-321">DBContext objects hold the query results from each call.</span><span class="sxs-lookup"><span data-stu-id="e86fc-321">DBContext objects hold the query results from each call.</span></span> <span data-ttu-id="e86fc-322">Static DBContext objects are not disposed until the application domain is unloaded.</span><span class="sxs-lookup"><span data-stu-id="e86fc-322">Static DBContext objects are not disposed until the application domain is unloaded.</span></span> <span data-ttu-id="e86fc-323">Therefore, a static DBContext object can consume large amounts of memory.</span><span class="sxs-lookup"><span data-stu-id="e86fc-323">Therefore, a static DBContext object can consume large amounts of memory.</span></span>

### <a name="solution"></a><span data-ttu-id="e86fc-324">Solution</span><span class="sxs-lookup"><span data-stu-id="e86fc-324">Solution</span></span>
<span data-ttu-id="e86fc-325">Declare DBContext as a local variable or non-static instance field, use it for a task, and then let it be disposed of after use.</span><span class="sxs-lookup"><span data-stu-id="e86fc-325">Declare DBContext as a local variable or non-static instance field, use it for a task, and then let it be disposed of after use.</span></span>

<span data-ttu-id="e86fc-326">The following example MVC controller class shows how to use the DBContext object.</span><span class="sxs-lookup"><span data-stu-id="e86fc-326">The following example MVC controller class shows how to use the DBContext object.</span></span>

```
public class BlogsController : Controller
    {
        //BloggingContext is a subclass to DbContext        
        private BloggingContext db = new BloggingContext();
        // GET: Blogs
        public ActionResult Index()
        {
            //business logics…
            return View();
        }
        protected override void Dispose(bool disposing)
        {
            if (disposing)
            {
                db.Dispose();
            }
            base.Dispose(disposing);
        }
    }
```

## <a name="next-steps"></a><span data-ttu-id="e86fc-327">Next steps</span><span class="sxs-lookup"><span data-stu-id="e86fc-327">Next steps</span></span>
<span data-ttu-id="e86fc-328">To learn more about optimizing and troubleshooting Azure apps, see [Troubleshoot a web app in Azure App Service using Visual Studio](app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="e86fc-328">To learn more about optimizing and troubleshooting Azure apps, see [Troubleshoot a web app in Azure App Service using Visual Studio](app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span></span>

