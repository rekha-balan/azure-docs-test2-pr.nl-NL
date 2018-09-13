---
title: Service remoting in Azure Service Fabric | Microsoft Docs
description: Service Fabric remoting allows clients and services to communicate with services by using a remote procedure call.
services: service-fabric
documentationcenter: java
author: PavanKunapareddyMSFT
manager: timlt
ms.assetid: ''
ms.service: service-fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 03/09/2017
ms.author: pakunapa
ms.openlocfilehash: 11e300b3b1d0433bd4790332593ada2d3eede883
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555384"
---
# <a name="service-remoting-with-reliable-services"></a><span data-ttu-id="39271-103">Service remoting with Reliable Services</span><span class="sxs-lookup"><span data-stu-id="39271-103">Service remoting with Reliable Services</span></span>
> [!div class="op_single_selector"]
> * [C# on Windows](service-fabric-reliable-services-communication-remoting.md)
> * [Java on Linux](service-fabric-reliable-services-communication-remoting-java.md)
>
>

<span data-ttu-id="39271-106">The Reliable Services framework provides a remoting mechanism to quickly and easily set up remote procedure call for services.</span><span class="sxs-lookup"><span data-stu-id="39271-106">The Reliable Services framework provides a remoting mechanism to quickly and easily set up remote procedure call for services.</span></span>

## <a name="set-up-remoting-on-a-service"></a><span data-ttu-id="39271-107">Set up remoting on a service</span><span class="sxs-lookup"><span data-stu-id="39271-107">Set up remoting on a service</span></span>
<span data-ttu-id="39271-108">Setting up remoting for a service is done in two simple steps:</span><span class="sxs-lookup"><span data-stu-id="39271-108">Setting up remoting for a service is done in two simple steps:</span></span>

1. <span data-ttu-id="39271-109">Create an interface for your service to implement.</span><span class="sxs-lookup"><span data-stu-id="39271-109">Create an interface for your service to implement.</span></span> <span data-ttu-id="39271-110">This interface defines the methods that are available for a remote procedure call on your service.</span><span class="sxs-lookup"><span data-stu-id="39271-110">This interface defines the methods that are available for a remote procedure call on your service.</span></span> <span data-ttu-id="39271-111">The methods must be task-returning asynchronous methods.</span><span class="sxs-lookup"><span data-stu-id="39271-111">The methods must be task-returning asynchronous methods.</span></span> <span data-ttu-id="39271-112">The interface must implement `microsoft.serviceFabric.services.remoting.Service` to signal that the service has a remoting interface.</span><span class="sxs-lookup"><span data-stu-id="39271-112">The interface must implement `microsoft.serviceFabric.services.remoting.Service` to signal that the service has a remoting interface.</span></span>
2. <span data-ttu-id="39271-113">Use a remoting listener in your service.</span><span class="sxs-lookup"><span data-stu-id="39271-113">Use a remoting listener in your service.</span></span> <span data-ttu-id="39271-114">This is an `CommunicationListener` implementation that provides remoting capabilities.</span><span class="sxs-lookup"><span data-stu-id="39271-114">This is an `CommunicationListener` implementation that provides remoting capabilities.</span></span> <span data-ttu-id="39271-115">`FabricTransportServiceRemotingListener` can be used to create a remoting listener using the default remoting transport protocol.</span><span class="sxs-lookup"><span data-stu-id="39271-115">`FabricTransportServiceRemotingListener` can be used to create a remoting listener using the default remoting transport protocol.</span></span>

<span data-ttu-id="39271-116">For example, the following stateless service exposes a single method to get "Hello World" over a remote procedure call.</span><span class="sxs-lookup"><span data-stu-id="39271-116">For example, the following stateless service exposes a single method to get "Hello World" over a remote procedure call.</span></span>

```java
import java.util.ArrayList;
import java.util.concurrent.CompletableFuture;
import java.util.List;
import microsoft.servicefabric.services.communication.runtime.ServiceInstanceListener;
import microsoft.servicefabric.services.remoting.Service;
import microsoft.servicefabric.services.runtime.StatelessService;

public interface MyService extends Service {
    CompletableFuture<String> helloWorldAsync();
}

class MyServiceImpl extends StatelessService implements MyService {
    public MyServiceImpl(StatelessServiceContext context) {
       super(context);
    }

    public CompletableFuture<String> helloWorldAsync() {
        return CompletableFuture.completedFuture("Hello!");
    }

    @Override
    protected List<ServiceInstanceListener> createServiceInstanceListeners() {
        ArrayList<ServiceInstanceListener> listeners = new ArrayList<>();
        listeners.add(new ServiceInstanceListener((context) -> {
            return new FabricTransportServiceRemotingListener(context,this);
        }));
        return listeners;
    }
}
```

> [!NOTE]
> The arguments and the return types in the service interface can be any simple, complex, or custom types, but they must be serializable.
>
>

## <a name="call-remote-service-methods"></a><span data-ttu-id="39271-118">Call remote service methods</span><span class="sxs-lookup"><span data-stu-id="39271-118">Call remote service methods</span></span>
<span data-ttu-id="39271-119">Calling methods on a service by using the remoting stack is done by using a local proxy to the service through the `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` class.</span><span class="sxs-lookup"><span data-stu-id="39271-119">Calling methods on a service by using the remoting stack is done by using a local proxy to the service through the `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` class.</span></span> <span data-ttu-id="39271-120">The `ServiceProxyBase` method creates a local proxy by using the same interface that the service implements.</span><span class="sxs-lookup"><span data-stu-id="39271-120">The `ServiceProxyBase` method creates a local proxy by using the same interface that the service implements.</span></span> <span data-ttu-id="39271-121">With that proxy, you can simply call methods on the interface remotely.</span><span class="sxs-lookup"><span data-stu-id="39271-121">With that proxy, you can simply call methods on the interface remotely.</span></span>

```java

MyService helloWorldClient = ServiceProxyBase.create(MyService.class, new URI("fabric:/MyApplication/MyHelloWorldService"));

CompletableFuture<String> message = helloWorldClient.helloWorldAsync();

```

<span data-ttu-id="39271-122">The remoting framework propagates exceptions thrown at the service to the client.</span><span class="sxs-lookup"><span data-stu-id="39271-122">The remoting framework propagates exceptions thrown at the service to the client.</span></span> <span data-ttu-id="39271-123">So exception-handling logic at the client by using `ServiceProxyBase` can directly handle exceptions that the service throws.</span><span class="sxs-lookup"><span data-stu-id="39271-123">So exception-handling logic at the client by using `ServiceProxyBase` can directly handle exceptions that the service throws.</span></span>

## <a name="next-steps"></a><span data-ttu-id="39271-124">Next steps</span><span class="sxs-lookup"><span data-stu-id="39271-124">Next steps</span></span>
* [<span data-ttu-id="39271-125">Securing communication for Reliable Services</span><span class="sxs-lookup"><span data-stu-id="39271-125">Securing communication for Reliable Services</span></span>](service-fabric-reliable-services-secure-communication.md)
