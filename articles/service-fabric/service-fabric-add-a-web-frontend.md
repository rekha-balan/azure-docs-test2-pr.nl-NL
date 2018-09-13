---
title: Create a web front end for your application using ASP.NET Core | Microsoft Docs
description: Expose your Service Fabric application to the web by using an ASP.NET Core Web API project and inter-service communication via ServiceProxy.
services: service-fabric
documentationcenter: .net
author: seanmck
manager: timlt
editor: ''
ms.assetid: 96176149-69bb-4b06-a72e-ebbfea84454b
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/30/2017
ms.author: seanmck
ms.openlocfilehash: a9cce2902babb3bf05380804addc3c99f633ab9f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551458"
---
# <a name="build-a-web-service-front-end-for-your-application-using-aspnet-core"></a><span data-ttu-id="10cde-103">Build a web service front end for your application using ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="10cde-103">Build a web service front end for your application using ASP.NET Core</span></span>
<span data-ttu-id="10cde-104">By default, Azure Service Fabric services do not provide a public interface to the web.</span><span class="sxs-lookup"><span data-stu-id="10cde-104">By default, Azure Service Fabric services do not provide a public interface to the web.</span></span> <span data-ttu-id="10cde-105">To expose your application's functionality to HTTP clients, you will need to create a web project to act as an entry point and then communicate from there to your individual services.</span><span class="sxs-lookup"><span data-stu-id="10cde-105">To expose your application's functionality to HTTP clients, you will need to create a web project to act as an entry point and then communicate from there to your individual services.</span></span>

<span data-ttu-id="10cde-106">In this tutorial, we will pick up where we left off in the [Creating your first application in Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md) tutorial and add a web service in front of the stateful counter service.</span><span class="sxs-lookup"><span data-stu-id="10cde-106">In this tutorial, we will pick up where we left off in the [Creating your first application in Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md) tutorial and add a web service in front of the stateful counter service.</span></span> <span data-ttu-id="10cde-107">If you have not already done so, you should go back and step through that tutorial first.</span><span class="sxs-lookup"><span data-stu-id="10cde-107">If you have not already done so, you should go back and step through that tutorial first.</span></span>

## <a name="add-an-aspnet-core-service-to-your-application"></a><span data-ttu-id="10cde-108">Add an ASP.NET Core service to your application</span><span class="sxs-lookup"><span data-stu-id="10cde-108">Add an ASP.NET Core service to your application</span></span>
<span data-ttu-id="10cde-109">ASP.NET Core is a lightweight, cross-platform web development framework that you can use to create modern web UI and web APIs.</span><span class="sxs-lookup"><span data-stu-id="10cde-109">ASP.NET Core is a lightweight, cross-platform web development framework that you can use to create modern web UI and web APIs.</span></span> <span data-ttu-id="10cde-110">Let's add an ASP.NET Web API project to our existing application.</span><span class="sxs-lookup"><span data-stu-id="10cde-110">Let's add an ASP.NET Web API project to our existing application.</span></span>

> [!NOTE]
> <span data-ttu-id="10cde-111">This tutorial is based on the [ASP.NET Core tools for Visual Studio 2017](https://docs.microsoft.com/aspnet/core/tutorials/first-mvc-app/start-mvc).</span><span class="sxs-lookup"><span data-stu-id="10cde-111">This tutorial is based on the [ASP.NET Core tools for Visual Studio 2017](https://docs.microsoft.com/aspnet/core/tutorials/first-mvc-app/start-mvc).</span></span> <span data-ttu-id="10cde-112">The .NET Core tools for Visual Studio 2015 are no longer being updated.</span><span class="sxs-lookup"><span data-stu-id="10cde-112">The .NET Core tools for Visual Studio 2015 are no longer being updated.</span></span>


1. <span data-ttu-id="10cde-113">In Solution Explorer, right-click **Services** within the application project and choose **Add > New Service Fabric Service**.</span><span class="sxs-lookup"><span data-stu-id="10cde-113">In Solution Explorer, right-click **Services** within the application project and choose **Add > New Service Fabric Service**.</span></span>
   
    ![Adding a new service to an existing application][vs-add-new-service]
2. <span data-ttu-id="10cde-115">On the **Create a Service** page, choose **ASP.NET Core** and give it a name.</span><span class="sxs-lookup"><span data-stu-id="10cde-115">On the **Create a Service** page, choose **ASP.NET Core** and give it a name.</span></span>
   
    ![Choosing ASP.NET web service in the new service dialog][vs-new-service-dialog]

3. <span data-ttu-id="10cde-117">The next page provides a set of ASP.NET Core project templates.</span><span class="sxs-lookup"><span data-stu-id="10cde-117">The next page provides a set of ASP.NET Core project templates.</span></span> <span data-ttu-id="10cde-118">Note that these are the same choices that you would see if you created an ASP.NET Core project outside of a Service Fabric application, with a small amount of additional code to register the service with the Service Fabric runtime.</span><span class="sxs-lookup"><span data-stu-id="10cde-118">Note that these are the same choices that you would see if you created an ASP.NET Core project outside of a Service Fabric application, with a small amount of additional code to register the service with the Service Fabric runtime.</span></span> <span data-ttu-id="10cde-119">For this tutorial, we will choose **Web API**.</span><span class="sxs-lookup"><span data-stu-id="10cde-119">For this tutorial, we will choose **Web API**.</span></span> <span data-ttu-id="10cde-120">However, you can apply the same concepts to building a full web application.</span><span class="sxs-lookup"><span data-stu-id="10cde-120">However, you can apply the same concepts to building a full web application.</span></span>
   
    ![Choosing ASP.NET project type][vs-new-aspnet-project-dialog]
   
    <span data-ttu-id="10cde-122">Once your Web API project is created, you will have two services in your application.</span><span class="sxs-lookup"><span data-stu-id="10cde-122">Once your Web API project is created, you will have two services in your application.</span></span> <span data-ttu-id="10cde-123">As you continue to build your application, you will add more services in exactly the same way.</span><span class="sxs-lookup"><span data-stu-id="10cde-123">As you continue to build your application, you will add more services in exactly the same way.</span></span> <span data-ttu-id="10cde-124">Each can be independently versioned and upgraded.</span><span class="sxs-lookup"><span data-stu-id="10cde-124">Each can be independently versioned and upgraded.</span></span>

> [!TIP]
> <span data-ttu-id="10cde-125">To learn more about building ASP.NET Core services, see the [ASP.NET Core Documentation](https://docs.microsoft.com/aspnet/core/).</span><span class="sxs-lookup"><span data-stu-id="10cde-125">To learn more about building ASP.NET Core services, see the [ASP.NET Core Documentation](https://docs.microsoft.com/aspnet/core/).</span></span>
> 

## <a name="run-the-application"></a><span data-ttu-id="10cde-126">Run the application</span><span class="sxs-lookup"><span data-stu-id="10cde-126">Run the application</span></span>
<span data-ttu-id="10cde-127">To get a sense of what we've done, let's deploy the new application and take a look at the default behavior that the ASP.NET Core Web API template provides.</span><span class="sxs-lookup"><span data-stu-id="10cde-127">To get a sense of what we've done, let's deploy the new application and take a look at the default behavior that the ASP.NET Core Web API template provides.</span></span>

1. <span data-ttu-id="10cde-128">Press F5 in Visual Studio to debug the app.</span><span class="sxs-lookup"><span data-stu-id="10cde-128">Press F5 in Visual Studio to debug the app.</span></span>
2. <span data-ttu-id="10cde-129">When deployment is complete, Visual Studio will launch the browser to the root of the ASP.NET Web API service, which by default is listening on port 8966.</span><span class="sxs-lookup"><span data-stu-id="10cde-129">When deployment is complete, Visual Studio will launch the browser to the root of the ASP.NET Web API service, which by default is listening on port 8966.</span></span> <span data-ttu-id="10cde-130">The ASP.NET Core Web API template doesn't provide default behavior for the root, so you will get an error in the browser.</span><span class="sxs-lookup"><span data-stu-id="10cde-130">The ASP.NET Core Web API template doesn't provide default behavior for the root, so you will get an error in the browser.</span></span>
3. <span data-ttu-id="10cde-131">Add `/api/values` to the location in the browser.</span><span class="sxs-lookup"><span data-stu-id="10cde-131">Add `/api/values` to the location in the browser.</span></span> <span data-ttu-id="10cde-132">This will invoke the `Get` method on the ValuesController in the Web API template.</span><span class="sxs-lookup"><span data-stu-id="10cde-132">This will invoke the `Get` method on the ValuesController in the Web API template.</span></span> <span data-ttu-id="10cde-133">It will return the default response that is provided by the template--a JSON array that contains two strings:</span><span class="sxs-lookup"><span data-stu-id="10cde-133">It will return the default response that is provided by the template--a JSON array that contains two strings:</span></span>
   
    ![Default values returned from ASP.NET Core Web API template][browser-aspnet-template-values]
   
    <span data-ttu-id="10cde-135">By the end of the tutorial, we will have replaced these default values with the most recent counter value from our stateful service.</span><span class="sxs-lookup"><span data-stu-id="10cde-135">By the end of the tutorial, we will have replaced these default values with the most recent counter value from our stateful service.</span></span>

## <a name="connect-the-services"></a><span data-ttu-id="10cde-136">Connect the services</span><span class="sxs-lookup"><span data-stu-id="10cde-136">Connect the services</span></span>
<span data-ttu-id="10cde-137">Service Fabric provides complete flexibility in how you communicate with reliable services.</span><span class="sxs-lookup"><span data-stu-id="10cde-137">Service Fabric provides complete flexibility in how you communicate with reliable services.</span></span> <span data-ttu-id="10cde-138">Within a single application, you might have services that are accessible via TCP, other services that are accessible via an HTTP REST API, and still other services that are accessible via web sockets.</span><span class="sxs-lookup"><span data-stu-id="10cde-138">Within a single application, you might have services that are accessible via TCP, other services that are accessible via an HTTP REST API, and still other services that are accessible via web sockets.</span></span> <span data-ttu-id="10cde-139">For background on the options available and the tradeoffs involved, see [Communicating with services](service-fabric-connect-and-communicate-with-services.md).</span><span class="sxs-lookup"><span data-stu-id="10cde-139">For background on the options available and the tradeoffs involved, see [Communicating with services](service-fabric-connect-and-communicate-with-services.md).</span></span> <span data-ttu-id="10cde-140">In this tutorial, we will follow one of the simpler approaches and use the `ServiceProxy`/`ServiceRemotingListener` classes that are provided in the SDK.</span><span class="sxs-lookup"><span data-stu-id="10cde-140">In this tutorial, we will follow one of the simpler approaches and use the `ServiceProxy`/`ServiceRemotingListener` classes that are provided in the SDK.</span></span>

<span data-ttu-id="10cde-141">In the `ServiceProxy` approach (modeled on remote procedure calls or RPCs), you define an interface to act as the public contract for the service.</span><span class="sxs-lookup"><span data-stu-id="10cde-141">In the `ServiceProxy` approach (modeled on remote procedure calls or RPCs), you define an interface to act as the public contract for the service.</span></span> <span data-ttu-id="10cde-142">Then, you use that interface to generate a proxy class for interacting with the service.</span><span class="sxs-lookup"><span data-stu-id="10cde-142">Then, you use that interface to generate a proxy class for interacting with the service.</span></span>

### <a name="create-the-interface"></a><span data-ttu-id="10cde-143">Create the interface</span><span class="sxs-lookup"><span data-stu-id="10cde-143">Create the interface</span></span>
<span data-ttu-id="10cde-144">We will start by creating the interface to act as the contract between the stateful service and its clients, including the ASP.NET Core project.</span><span class="sxs-lookup"><span data-stu-id="10cde-144">We will start by creating the interface to act as the contract between the stateful service and its clients, including the ASP.NET Core project.</span></span>

1. <span data-ttu-id="10cde-145">In Solution Explorer, right-click your solution and choose **Add** > **New Project**.</span><span class="sxs-lookup"><span data-stu-id="10cde-145">In Solution Explorer, right-click your solution and choose **Add** > **New Project**.</span></span>
2. <span data-ttu-id="10cde-146">Choose the **Visual C#** entry in the left navigation pane and then select the **Class Library** template.</span><span class="sxs-lookup"><span data-stu-id="10cde-146">Choose the **Visual C#** entry in the left navigation pane and then select the **Class Library** template.</span></span> <span data-ttu-id="10cde-147">Ensure that the .NET Framework version is set to **4.5.2**.</span><span class="sxs-lookup"><span data-stu-id="10cde-147">Ensure that the .NET Framework version is set to **4.5.2**.</span></span>
   
    ![Creating an interface project for your stateful service][vs-add-class-library-project]

3. <span data-ttu-id="10cde-149">In order for an interface to be usable by `ServiceProxy`, it must derive from the IService interface.</span><span class="sxs-lookup"><span data-stu-id="10cde-149">In order for an interface to be usable by `ServiceProxy`, it must derive from the IService interface.</span></span> <span data-ttu-id="10cde-150">This interface is included in one of the Service Fabric NuGet packages.</span><span class="sxs-lookup"><span data-stu-id="10cde-150">This interface is included in one of the Service Fabric NuGet packages.</span></span> <span data-ttu-id="10cde-151">To add the package, right-click your new class library project and choose **Manage NuGet Packages**.</span><span class="sxs-lookup"><span data-stu-id="10cde-151">To add the package, right-click your new class library project and choose **Manage NuGet Packages**.</span></span>
4. <span data-ttu-id="10cde-152">Search for the **Microsoft.ServiceFabric.Services** package and install it.</span><span class="sxs-lookup"><span data-stu-id="10cde-152">Search for the **Microsoft.ServiceFabric.Services** package and install it.</span></span>
   
    ![Adding the Services NuGet package][vs-services-nuget-package]

5. <span data-ttu-id="10cde-154">In the class library, create an interface with a single method, `GetCountAsync`, and extend the interface from IService.</span><span class="sxs-lookup"><span data-stu-id="10cde-154">In the class library, create an interface with a single method, `GetCountAsync`, and extend the interface from IService.</span></span>
   
    ```c#
    namespace MyStatefulService.Interface
    {
        using Microsoft.ServiceFabric.Services.Remoting;
   
        public interface ICounter: IService
        {
            Task<long> GetCountAsync();
        }
    }
    ```

### <a name="implement-the-interface-in-your-stateful-service"></a><span data-ttu-id="10cde-155">Implement the interface in your stateful service</span><span class="sxs-lookup"><span data-stu-id="10cde-155">Implement the interface in your stateful service</span></span>
<span data-ttu-id="10cde-156">Now that we have defined the interface, we need to implement it in the stateful service.</span><span class="sxs-lookup"><span data-stu-id="10cde-156">Now that we have defined the interface, we need to implement it in the stateful service.</span></span>

1. <span data-ttu-id="10cde-157">In your stateful service, add a reference to the class library project that contains the interface.</span><span class="sxs-lookup"><span data-stu-id="10cde-157">In your stateful service, add a reference to the class library project that contains the interface.</span></span>
   
    ![Adding a reference to the class library project in the stateful service][vs-add-class-library-reference]
2. <span data-ttu-id="10cde-159">Locate the class that inherits from `StatefulService`, such as `MyStatefulService`, and extend it to implement the `ICounter` interface.</span><span class="sxs-lookup"><span data-stu-id="10cde-159">Locate the class that inherits from `StatefulService`, such as `MyStatefulService`, and extend it to implement the `ICounter` interface.</span></span>
   
    ```c#
    using MyStatefulService.Interface;
   
    ...
   
    public class MyStatefulService : StatefulService, ICounter
    {        
          // ...
    }
    ```
3. <span data-ttu-id="10cde-160">Now implement the single method that is defined in the `ICounter` interface, `GetCountAsync`.</span><span class="sxs-lookup"><span data-stu-id="10cde-160">Now implement the single method that is defined in the `ICounter` interface, `GetCountAsync`.</span></span>
   
    ```c#
    public async Task<long> GetCountAsync()
    {
      var myDictionary =
        await this.StateManager.GetOrAddAsync<IReliableDictionary<string, long>>("myDictionary");
   
        using (var tx = this.StateManager.CreateTransaction())
        {          
            var result = await myDictionary.TryGetValueAsync(tx, "Counter");
            return result.HasValue ? result.Value : 0;
        }
    }
    ```

### <a name="expose-the-stateful-service-using-a-service-remoting-listener"></a><span data-ttu-id="10cde-161">Expose the stateful service using a service remoting listener</span><span class="sxs-lookup"><span data-stu-id="10cde-161">Expose the stateful service using a service remoting listener</span></span>
<span data-ttu-id="10cde-162">With the `ICounter` interface implemented, the final step in enabling the stateful service to be callable from other services is to open a communication channel.</span><span class="sxs-lookup"><span data-stu-id="10cde-162">With the `ICounter` interface implemented, the final step in enabling the stateful service to be callable from other services is to open a communication channel.</span></span> <span data-ttu-id="10cde-163">For stateful services, Service Fabric provides an overridable method called `CreateServiceReplicaListeners`.</span><span class="sxs-lookup"><span data-stu-id="10cde-163">For stateful services, Service Fabric provides an overridable method called `CreateServiceReplicaListeners`.</span></span> <span data-ttu-id="10cde-164">With this method, you can specify one or more communication listeners, based on the type of communication that you want to enable to your service.</span><span class="sxs-lookup"><span data-stu-id="10cde-164">With this method, you can specify one or more communication listeners, based on the type of communication that you want to enable to your service.</span></span>

> [!NOTE]
> <span data-ttu-id="10cde-165">The equivalent method for opening a communication channel to stateless services is called `CreateServiceInstanceListeners`.</span><span class="sxs-lookup"><span data-stu-id="10cde-165">The equivalent method for opening a communication channel to stateless services is called `CreateServiceInstanceListeners`.</span></span>
> 
> 

<span data-ttu-id="10cde-166">In this case, we will replace the existing `CreateServiceReplicaListeners` method and provide an instance of `ServiceRemotingListener`, which creates an RPC endpoint that is callable from clients through `ServiceProxy`.</span><span class="sxs-lookup"><span data-stu-id="10cde-166">In this case, we will replace the existing `CreateServiceReplicaListeners` method and provide an instance of `ServiceRemotingListener`, which creates an RPC endpoint that is callable from clients through `ServiceProxy`.</span></span>  

```c#
using Microsoft.ServiceFabric.Services.Remoting.Runtime;

...

protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
{
    return new List<ServiceReplicaListener>()
    {
        new ServiceReplicaListener(
            (context) =>
                this.CreateServiceRemotingListener(context))
    };
}
```


### <a name="use-the-serviceproxy-class-to-interact-with-the-service"></a><span data-ttu-id="10cde-167">Use the ServiceProxy class to interact with the service</span><span class="sxs-lookup"><span data-stu-id="10cde-167">Use the ServiceProxy class to interact with the service</span></span>
<span data-ttu-id="10cde-168">Our stateful service is now ready to receive traffic from other services.</span><span class="sxs-lookup"><span data-stu-id="10cde-168">Our stateful service is now ready to receive traffic from other services.</span></span> <span data-ttu-id="10cde-169">So all that remains is adding the code to communicate with it from the ASP.NET web service.</span><span class="sxs-lookup"><span data-stu-id="10cde-169">So all that remains is adding the code to communicate with it from the ASP.NET web service.</span></span>

1. <span data-ttu-id="10cde-170">In your ASP.NET project, add a reference to the class library that contains the `ICounter` interface.</span><span class="sxs-lookup"><span data-stu-id="10cde-170">In your ASP.NET project, add a reference to the class library that contains the `ICounter` interface.</span></span>

2. <span data-ttu-id="10cde-171">Add the Microsoft.ServiceFabric.Services package to the ASP.NET project, just as you did for the class library project earlier.</span><span class="sxs-lookup"><span data-stu-id="10cde-171">Add the Microsoft.ServiceFabric.Services package to the ASP.NET project, just as you did for the class library project earlier.</span></span> <span data-ttu-id="10cde-172">This will provide the `ServiceProxy` class.</span><span class="sxs-lookup"><span data-stu-id="10cde-172">This will provide the `ServiceProxy` class.</span></span>

4. <span data-ttu-id="10cde-173">In the **Controllers** folder, open the `ValuesController` class.</span><span class="sxs-lookup"><span data-stu-id="10cde-173">In the **Controllers** folder, open the `ValuesController` class.</span></span> <span data-ttu-id="10cde-174">Note that the `Get` method currently just returns a hard-coded string array of "value1" and "value2"--which matches what we saw earlier in the browser.</span><span class="sxs-lookup"><span data-stu-id="10cde-174">Note that the `Get` method currently just returns a hard-coded string array of "value1" and "value2"--which matches what we saw earlier in the browser.</span></span> <span data-ttu-id="10cde-175">Replace this implementation with the following code:</span><span class="sxs-lookup"><span data-stu-id="10cde-175">Replace this implementation with the following code:</span></span>
   
    ```c#
    using MyStatefulService.Interface;
    using Microsoft.ServiceFabric.Services.Remoting.Client;
   
    ...
   
    public async Task<IEnumerable<string>> Get()
    {
        ICounter counter =
            ServiceProxy.Create<ICounter>(new Uri("fabric:/MyApplication/MyStatefulService"), new ServicePartitionKey(0));
   
        long count = await counter.GetCountAsync();
   
        return new string[] { count.ToString() };
    }
    ```
   
    <span data-ttu-id="10cde-176">The first line of code is the key one.</span><span class="sxs-lookup"><span data-stu-id="10cde-176">The first line of code is the key one.</span></span> <span data-ttu-id="10cde-177">To create the ICounter proxy to the stateful service, you need to provide two pieces of information: a partition ID and the name of the service.</span><span class="sxs-lookup"><span data-stu-id="10cde-177">To create the ICounter proxy to the stateful service, you need to provide two pieces of information: a partition ID and the name of the service.</span></span>
   
    <span data-ttu-id="10cde-178">You can use partitioning to scale stateful services by breaking up their state into different buckets, based on a key that you define, such as a customer ID or postal code.</span><span class="sxs-lookup"><span data-stu-id="10cde-178">You can use partitioning to scale stateful services by breaking up their state into different buckets, based on a key that you define, such as a customer ID or postal code.</span></span> <span data-ttu-id="10cde-179">In our trivial application, the stateful service only has one partition, so the key doesn't matter.</span><span class="sxs-lookup"><span data-stu-id="10cde-179">In our trivial application, the stateful service only has one partition, so the key doesn't matter.</span></span> <span data-ttu-id="10cde-180">Any key that you provide will lead to the same partition.</span><span class="sxs-lookup"><span data-stu-id="10cde-180">Any key that you provide will lead to the same partition.</span></span> <span data-ttu-id="10cde-181">To learn more about partitioning services, see [How to partition Service Fabric Reliable Services](service-fabric-concepts-partitioning.md).</span><span class="sxs-lookup"><span data-stu-id="10cde-181">To learn more about partitioning services, see [How to partition Service Fabric Reliable Services](service-fabric-concepts-partitioning.md).</span></span>
   
    <span data-ttu-id="10cde-182">The service name is a URI of the form fabric:/&lt;application_name&gt;/&lt;service_name&gt;.</span><span class="sxs-lookup"><span data-stu-id="10cde-182">The service name is a URI of the form fabric:/&lt;application_name&gt;/&lt;service_name&gt;.</span></span>
   
    <span data-ttu-id="10cde-183">With these two pieces of information, Service Fabric can uniquely identify the machine that requests should be sent to.</span><span class="sxs-lookup"><span data-stu-id="10cde-183">With these two pieces of information, Service Fabric can uniquely identify the machine that requests should be sent to.</span></span> <span data-ttu-id="10cde-184">The `ServiceProxy` class also seamlessly handles the case where the machine that hosts the stateful service partition fails and another machine must be promoted to take its place.</span><span class="sxs-lookup"><span data-stu-id="10cde-184">The `ServiceProxy` class also seamlessly handles the case where the machine that hosts the stateful service partition fails and another machine must be promoted to take its place.</span></span> <span data-ttu-id="10cde-185">This abstraction makes writing the client code to deal with other services significantly simpler.</span><span class="sxs-lookup"><span data-stu-id="10cde-185">This abstraction makes writing the client code to deal with other services significantly simpler.</span></span>
   
    <span data-ttu-id="10cde-186">Once we have the proxy, we simply invoke the `GetCountAsync` method and return its result.</span><span class="sxs-lookup"><span data-stu-id="10cde-186">Once we have the proxy, we simply invoke the `GetCountAsync` method and return its result.</span></span>

5. <span data-ttu-id="10cde-187">Press F5 again to run the modified application.</span><span class="sxs-lookup"><span data-stu-id="10cde-187">Press F5 again to run the modified application.</span></span> <span data-ttu-id="10cde-188">As before, Visual Studio will automatically launch the browser to the root of the web project.</span><span class="sxs-lookup"><span data-stu-id="10cde-188">As before, Visual Studio will automatically launch the browser to the root of the web project.</span></span> <span data-ttu-id="10cde-189">Add the "api/values" path, and you should see the current counter value returned.</span><span class="sxs-lookup"><span data-stu-id="10cde-189">Add the "api/values" path, and you should see the current counter value returned.</span></span>
   
    ![The stateful counter value displayed in the browser][browser-aspnet-counter-value]
   
    <span data-ttu-id="10cde-191">Refresh the browser periodically to see the counter value update.</span><span class="sxs-lookup"><span data-stu-id="10cde-191">Refresh the browser periodically to see the counter value update.</span></span>

## <a name="kestrel-and-weblistener"></a><span data-ttu-id="10cde-192">Kestrel and WebListener</span><span class="sxs-lookup"><span data-stu-id="10cde-192">Kestrel and WebListener</span></span>

<span data-ttu-id="10cde-193">The default ASP.NET Core web server, known as Kestrel, is [not currently supported for handling direct internet traffic](https://docs.asp.net/en/latest/fundamentals/servers.html#kestrel).</span><span class="sxs-lookup"><span data-stu-id="10cde-193">The default ASP.NET Core web server, known as Kestrel, is [not currently supported for handling direct internet traffic](https://docs.asp.net/en/latest/fundamentals/servers.html#kestrel).</span></span> <span data-ttu-id="10cde-194">As a result, the ASP.NET templates for Service Fabric use [WebListener](https://docs.microsoft.com/aspnet/core/fundamentals/servers/weblistener) by default.</span><span class="sxs-lookup"><span data-stu-id="10cde-194">As a result, the ASP.NET templates for Service Fabric use [WebListener](https://docs.microsoft.com/aspnet/core/fundamentals/servers/weblistener) by default.</span></span> 

<span data-ttu-id="10cde-195">If you will not be serving direct internet traffic and would prefer to use Kestrel as your web server, you can change it in your service listener configuration.</span><span class="sxs-lookup"><span data-stu-id="10cde-195">If you will not be serving direct internet traffic and would prefer to use Kestrel as your web server, you can change it in your service listener configuration.</span></span> <span data-ttu-id="10cde-196">Simply replace `return new WebHostBuilder().UseWebListener()` with `return new WebHostBuilder().UseKestrel()`.</span><span class="sxs-lookup"><span data-stu-id="10cde-196">Simply replace `return new WebHostBuilder().UseWebListener()` with `return new WebHostBuilder().UseKestrel()`.</span></span> <span data-ttu-id="10cde-197">All other configurations on the web host can remain the same.</span><span class="sxs-lookup"><span data-stu-id="10cde-197">All other configurations on the web host can remain the same.</span></span>
 

## <a name="what-about-actors"></a><span data-ttu-id="10cde-198">What about actors?</span><span class="sxs-lookup"><span data-stu-id="10cde-198">What about actors?</span></span>
<span data-ttu-id="10cde-199">This tutorial focused on adding a web front end that communicated with a stateful service.</span><span class="sxs-lookup"><span data-stu-id="10cde-199">This tutorial focused on adding a web front end that communicated with a stateful service.</span></span> <span data-ttu-id="10cde-200">However, you can follow a very similar model to talk to actors.</span><span class="sxs-lookup"><span data-stu-id="10cde-200">However, you can follow a very similar model to talk to actors.</span></span> <span data-ttu-id="10cde-201">In fact, it is somewhat simpler.</span><span class="sxs-lookup"><span data-stu-id="10cde-201">In fact, it is somewhat simpler.</span></span>

<span data-ttu-id="10cde-202">When you create an actor project, Visual Studio automatically generates an interface project for you.</span><span class="sxs-lookup"><span data-stu-id="10cde-202">When you create an actor project, Visual Studio automatically generates an interface project for you.</span></span> <span data-ttu-id="10cde-203">You can use that interface to generate an actor proxy in the web project to communicate with the actor.</span><span class="sxs-lookup"><span data-stu-id="10cde-203">You can use that interface to generate an actor proxy in the web project to communicate with the actor.</span></span> <span data-ttu-id="10cde-204">The communication channel is provided automatically.</span><span class="sxs-lookup"><span data-stu-id="10cde-204">The communication channel is provided automatically.</span></span> <span data-ttu-id="10cde-205">So you do not need to do anything that is equivalent to establishing a `ServiceRemotingListener` like you did for the stateful service in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="10cde-205">So you do not need to do anything that is equivalent to establishing a `ServiceRemotingListener` like you did for the stateful service in this tutorial.</span></span>

## <a name="how-web-services-work-on-your-local-cluster"></a><span data-ttu-id="10cde-206">How web services work on your local cluster</span><span class="sxs-lookup"><span data-stu-id="10cde-206">How web services work on your local cluster</span></span>
<span data-ttu-id="10cde-207">In general, you can deploy exactly the same Service Fabric application to a multi-machine cluster that you deployed on your local cluster and be highly confident that it will work as you expect.</span><span class="sxs-lookup"><span data-stu-id="10cde-207">In general, you can deploy exactly the same Service Fabric application to a multi-machine cluster that you deployed on your local cluster and be highly confident that it will work as you expect.</span></span> <span data-ttu-id="10cde-208">This is because your local cluster is simply a five-node configuration that is collapsed to a single machine.</span><span class="sxs-lookup"><span data-stu-id="10cde-208">This is because your local cluster is simply a five-node configuration that is collapsed to a single machine.</span></span>

<span data-ttu-id="10cde-209">When it comes to web services, however, there is one key nuance.</span><span class="sxs-lookup"><span data-stu-id="10cde-209">When it comes to web services, however, there is one key nuance.</span></span> <span data-ttu-id="10cde-210">When your cluster sits behind a load balancer, as it does in Azure, you must ensure that your web services are deployed on every machine since the load balancer will simply round-robin traffic across the machines.</span><span class="sxs-lookup"><span data-stu-id="10cde-210">When your cluster sits behind a load balancer, as it does in Azure, you must ensure that your web services are deployed on every machine since the load balancer will simply round-robin traffic across the machines.</span></span> <span data-ttu-id="10cde-211">You can do this by setting the `InstanceCount` for the service to the special value of "-1".</span><span class="sxs-lookup"><span data-stu-id="10cde-211">You can do this by setting the `InstanceCount` for the service to the special value of "-1".</span></span>

<span data-ttu-id="10cde-212">By contrast, when you run a web service locally, you need to ensure that only one instance of the service is running.</span><span class="sxs-lookup"><span data-stu-id="10cde-212">By contrast, when you run a web service locally, you need to ensure that only one instance of the service is running.</span></span> <span data-ttu-id="10cde-213">Otherwise, you will run into conflicts from multiple processes that are listening on the same path and port.</span><span class="sxs-lookup"><span data-stu-id="10cde-213">Otherwise, you will run into conflicts from multiple processes that are listening on the same path and port.</span></span> <span data-ttu-id="10cde-214">As a result, the web service instance count should be set to "1" for local deployments.</span><span class="sxs-lookup"><span data-stu-id="10cde-214">As a result, the web service instance count should be set to "1" for local deployments.</span></span>

<span data-ttu-id="10cde-215">To learn how to configure different values for different environment, see [Managing application parameters for multiple environments](service-fabric-manage-multiple-environment-app-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="10cde-215">To learn how to configure different values for different environment, see [Managing application parameters for multiple environments](service-fabric-manage-multiple-environment-app-configuration.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="10cde-216">Next steps</span><span class="sxs-lookup"><span data-stu-id="10cde-216">Next steps</span></span>
* [<span data-ttu-id="10cde-217">Create a cluster in Azure for deploying your application to the cloud</span><span class="sxs-lookup"><span data-stu-id="10cde-217">Create a cluster in Azure for deploying your application to the cloud</span></span>](service-fabric-cluster-creation-via-portal.md)
* [<span data-ttu-id="10cde-218">Learn more about communicating with services</span><span class="sxs-lookup"><span data-stu-id="10cde-218">Learn more about communicating with services</span></span>](service-fabric-connect-and-communicate-with-services.md)
* [<span data-ttu-id="10cde-219">Learn more about partitioning stateful services</span><span class="sxs-lookup"><span data-stu-id="10cde-219">Learn more about partitioning stateful services</span></span>](service-fabric-concepts-partitioning.md)

<!-- Image References -->

[vs-add-new-service]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-add-a-web-frontend/vs-add-new-service.png
[vs-new-service-dialog]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-add-a-web-frontend/vs-new-service-dialog.png
[vs-new-aspnet-project-dialog]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-add-a-web-frontend/vs-new-aspnet-project-dialog.png
[browser-aspnet-template-values]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-add-a-web-frontend/browser-aspnet-template-values.png
[vs-add-class-library-project]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-add-a-web-frontend/vs-add-class-library-project.png
[vs-add-class-library-reference]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-add-a-web-frontend/vs-add-class-library-reference.png
[vs-services-nuget-package]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-add-a-web-frontend/vs-services-nuget-package.png
[browser-aspnet-counter-value]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-add-a-web-frontend/browser-aspnet-counter-value.png
[vs-create-platform]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-add-a-web-frontend/vs-create-platform.png


<!-- external links -->
[dotnetcore-install]: https://www.microsoft.com/net/core#windows









