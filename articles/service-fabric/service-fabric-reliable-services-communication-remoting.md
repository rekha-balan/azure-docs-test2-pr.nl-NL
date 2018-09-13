---
title: Service remoting in Azure Service Fabric | Microsoft Docs
description: Service Fabric remoting allows clients and services to communicate with services by using a remote procedure call.
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: BharatNarasimman
ms.assetid: abfaf430-fea0-4974-afba-cfc9f9f2354b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 02/10/2017
ms.author: vturecek
ms.openlocfilehash: d76093b18851a7010b16b66eaa5db858bf1f9f86
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549373"
---
# <a name="service-remoting-with-reliable-services"></a><span data-ttu-id="2137f-103">Service remoting with Reliable Services</span><span class="sxs-lookup"><span data-stu-id="2137f-103">Service remoting with Reliable Services</span></span>
> [!div class="op_single_selector"]
> * [C# on Windows](service-fabric-reliable-services-communication-remoting.md)
> * [Java on Linux](service-fabric-reliable-services-communication-remoting-java.md)
>
>

<span data-ttu-id="2137f-106">For services that are not tied to a particular communication protocol or stack, such as WebAPI, Windows Communication Foundation (WCF), or others, the Reliable Services framework provides a remoting mechanism to quickly and easily set up remote procedure call for services.</span><span class="sxs-lookup"><span data-stu-id="2137f-106">For services that are not tied to a particular communication protocol or stack, such as WebAPI, Windows Communication Foundation (WCF), or others, the Reliable Services framework provides a remoting mechanism to quickly and easily set up remote procedure call for services.</span></span>

## <a name="set-up-remoting-on-a-service"></a><span data-ttu-id="2137f-107">Set up remoting on a service</span><span class="sxs-lookup"><span data-stu-id="2137f-107">Set up remoting on a service</span></span>
<span data-ttu-id="2137f-108">Setting up remoting for a service is done in two simple steps:</span><span class="sxs-lookup"><span data-stu-id="2137f-108">Setting up remoting for a service is done in two simple steps:</span></span>

1. <span data-ttu-id="2137f-109">Create an interface for your service to implement.</span><span class="sxs-lookup"><span data-stu-id="2137f-109">Create an interface for your service to implement.</span></span> <span data-ttu-id="2137f-110">This interface defines the methods that are available for a remote procedure call on your service.</span><span class="sxs-lookup"><span data-stu-id="2137f-110">This interface defines the methods that are available for a remote procedure call on your service.</span></span> <span data-ttu-id="2137f-111">The methods must be task-returning asynchronous methods.</span><span class="sxs-lookup"><span data-stu-id="2137f-111">The methods must be task-returning asynchronous methods.</span></span> <span data-ttu-id="2137f-112">The interface must implement `Microsoft.ServiceFabric.Services.Remoting.IService` to signal that the service has a remoting interface.</span><span class="sxs-lookup"><span data-stu-id="2137f-112">The interface must implement `Microsoft.ServiceFabric.Services.Remoting.IService` to signal that the service has a remoting interface.</span></span>
2. <span data-ttu-id="2137f-113">Use a remoting listener in your service.</span><span class="sxs-lookup"><span data-stu-id="2137f-113">Use a remoting listener in your service.</span></span> <span data-ttu-id="2137f-114">This is an `ICommunicationListener` implementation that provides remoting capabilities.</span><span class="sxs-lookup"><span data-stu-id="2137f-114">This is an `ICommunicationListener` implementation that provides remoting capabilities.</span></span> <span data-ttu-id="2137f-115">The `Microsoft.ServiceFabric.Services.Remoting.Runtime` namespace contains an extension method, `CreateServiceRemotingListener` for both stateless and stateful services that can be used to create a remoting listener using the default remoting transport protocol.</span><span class="sxs-lookup"><span data-stu-id="2137f-115">The `Microsoft.ServiceFabric.Services.Remoting.Runtime` namespace contains an extension method, `CreateServiceRemotingListener` for both stateless and stateful services that can be used to create a remoting listener using the default remoting transport protocol.</span></span>

<span data-ttu-id="2137f-116">For example, the following stateless service exposes a single method to get "Hello World" over a remote procedure call.</span><span class="sxs-lookup"><span data-stu-id="2137f-116">For example, the following stateless service exposes a single method to get "Hello World" over a remote procedure call.</span></span>

```csharp
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Microsoft.ServiceFabric.Services.Remoting;
using Microsoft.ServiceFabric.Services.Remoting.Runtime;
using Microsoft.ServiceFabric.Services.Runtime;

public interface IMyService : IService
{
    Task<string> HelloWorldAsync();
}

class MyService : StatelessService, IMyService
{
    public MyService(StatelessServiceContext context)
        : base (context)
    {
    }

    public Task HelloWorldAsync()
    {
        return Task.FromResult("Hello!");
    }

    protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
    {
        return new[] { new ServiceInstanceListener(context =>
            this.CreateServiceRemotingListener(context)) };
    }
}
```
> [!NOTE]
> The arguments and the return types in the service interface can be any simple, complex, or custom types, but they must be serializable by the .NET [DataContractSerializer](https://msdn.microsoft.com/library/ms731923.aspx).
>
>

## <a name="call-remote-service-methods"></a><span data-ttu-id="2137f-118">Call remote service methods</span><span class="sxs-lookup"><span data-stu-id="2137f-118">Call remote service methods</span></span>
<span data-ttu-id="2137f-119">Calling methods on a service by using the remoting stack is done by using a local proxy to the service through the `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` class.</span><span class="sxs-lookup"><span data-stu-id="2137f-119">Calling methods on a service by using the remoting stack is done by using a local proxy to the service through the `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` class.</span></span> <span data-ttu-id="2137f-120">The `ServiceProxy` method creates a local proxy by using the same interface that the service implements.</span><span class="sxs-lookup"><span data-stu-id="2137f-120">The `ServiceProxy` method creates a local proxy by using the same interface that the service implements.</span></span> <span data-ttu-id="2137f-121">With that proxy, you can simply call methods on the interface remotely.</span><span class="sxs-lookup"><span data-stu-id="2137f-121">With that proxy, you can simply call methods on the interface remotely.</span></span>

```csharp

IMyService helloWorldClient = ServiceProxy.Create<IMyService>(new Uri("fabric:/MyApplication/MyHelloWorldService"));

string message = await helloWorldClient.HelloWorldAsync();

```

<span data-ttu-id="2137f-122">The remoting framework propagates exceptions thrown at the service to the client.</span><span class="sxs-lookup"><span data-stu-id="2137f-122">The remoting framework propagates exceptions thrown at the service to the client.</span></span> <span data-ttu-id="2137f-123">So exception-handling logic at the client by using `ServiceProxy` can directly handle exceptions that the service throws.</span><span class="sxs-lookup"><span data-stu-id="2137f-123">So exception-handling logic at the client by using `ServiceProxy` can directly handle exceptions that the service throws.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2137f-124">Next steps</span><span class="sxs-lookup"><span data-stu-id="2137f-124">Next steps</span></span>
* [<span data-ttu-id="2137f-125">Web API with OWIN in Reliable Services</span><span class="sxs-lookup"><span data-stu-id="2137f-125">Web API with OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="2137f-126">WCF communication with Reliable Services</span><span class="sxs-lookup"><span data-stu-id="2137f-126">WCF communication with Reliable Services</span></span>](service-fabric-reliable-services-communication-wcf.md)
* [<span data-ttu-id="2137f-127">Securing communication for Reliable Services</span><span class="sxs-lookup"><span data-stu-id="2137f-127">Securing communication for Reliable Services</span></span>](service-fabric-reliable-services-secure-communication.md)
