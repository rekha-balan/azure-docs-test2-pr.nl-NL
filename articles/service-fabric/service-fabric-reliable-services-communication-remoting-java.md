---
title: Service remoting using Java in Azure Service Fabric | Microsoft Docs
description: Service Fabric remoting allows clients and services to communicate with Java services by using a remote procedure call.
services: service-fabric
documentationcenter: java
author: PavanKunapareddyMSFT
manager: timlt
ms.assetid: ''
ms.service: service-fabric
ms.devlang: java
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 06/30/2017
ms.author: pakunapa
ms.openlocfilehash: 5135884352308eb31ef7a080078255f016bd6e10
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44826527"
---
# <a name="service-remoting-in-java-with-reliable-services"></a><span data-ttu-id="0a801-103">Service remoting in Java with Reliable Services</span><span class="sxs-lookup"><span data-stu-id="0a801-103">Service remoting in Java with Reliable Services</span></span>
> [!div class="op_single_selector"]
> * [C# on Windows](service-fabric-reliable-services-communication-remoting.md)
> * [Java on Linux](service-fabric-reliable-services-communication-remoting-java.md)
>
>

<span data-ttu-id="0a801-106">For services that aren't tied to a particular communication protocol or stack, such as WebAPI, Windows Communication Foundation (WCF), or others, the Reliable Services framework provides a remoting mechanism to quickly and easily set up remote procedure calls for services.</span><span class="sxs-lookup"><span data-stu-id="0a801-106">For services that aren't tied to a particular communication protocol or stack, such as WebAPI, Windows Communication Foundation (WCF), or others, the Reliable Services framework provides a remoting mechanism to quickly and easily set up remote procedure calls for services.</span></span>  <span data-ttu-id="0a801-107">This article discusses how to set up remote procedure calls for services written with Java.</span><span class="sxs-lookup"><span data-stu-id="0a801-107">This article discusses how to set up remote procedure calls for services written with Java.</span></span>

## <a name="set-up-remoting-on-a-service"></a><span data-ttu-id="0a801-108">Set up remoting on a service</span><span class="sxs-lookup"><span data-stu-id="0a801-108">Set up remoting on a service</span></span>
<span data-ttu-id="0a801-109">Setting up remoting for a service is done in two simple steps:</span><span class="sxs-lookup"><span data-stu-id="0a801-109">Setting up remoting for a service is done in two simple steps:</span></span>

1. <span data-ttu-id="0a801-110">Create an interface for your service to implement.</span><span class="sxs-lookup"><span data-stu-id="0a801-110">Create an interface for your service to implement.</span></span> <span data-ttu-id="0a801-111">This interface defines the methods that are available for a remote procedure call on your service.</span><span class="sxs-lookup"><span data-stu-id="0a801-111">This interface defines the methods that are available for a remote procedure call on your service.</span></span> <span data-ttu-id="0a801-112">The methods must be task-returning asynchronous methods.</span><span class="sxs-lookup"><span data-stu-id="0a801-112">The methods must be task-returning asynchronous methods.</span></span> <span data-ttu-id="0a801-113">The interface must implement `microsoft.serviceFabric.services.remoting.Service` to signal that the service has a remoting interface.</span><span class="sxs-lookup"><span data-stu-id="0a801-113">The interface must implement `microsoft.serviceFabric.services.remoting.Service` to signal that the service has a remoting interface.</span></span>
2. <span data-ttu-id="0a801-114">Use a remoting listener in your service.</span><span class="sxs-lookup"><span data-stu-id="0a801-114">Use a remoting listener in your service.</span></span> <span data-ttu-id="0a801-115">This is an `CommunicationListener` implementation that provides remoting capabilities.</span><span class="sxs-lookup"><span data-stu-id="0a801-115">This is an `CommunicationListener` implementation that provides remoting capabilities.</span></span> <span data-ttu-id="0a801-116">`FabricTransportServiceRemotingListener` can be used to create a remoting listener using the default remoting transport protocol.</span><span class="sxs-lookup"><span data-stu-id="0a801-116">`FabricTransportServiceRemotingListener` can be used to create a remoting listener using the default remoting transport protocol.</span></span>

<span data-ttu-id="0a801-117">For example, the following stateless service exposes a single method to get "Hello World" over a remote procedure call.</span><span class="sxs-lookup"><span data-stu-id="0a801-117">For example, the following stateless service exposes a single method to get "Hello World" over a remote procedure call.</span></span>

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

## <a name="call-remote-service-methods"></a><span data-ttu-id="0a801-119">Call remote service methods</span><span class="sxs-lookup"><span data-stu-id="0a801-119">Call remote service methods</span></span>
<span data-ttu-id="0a801-120">Calling methods on a service by using the remoting stack is done by using a local proxy to the service through the `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` class.</span><span class="sxs-lookup"><span data-stu-id="0a801-120">Calling methods on a service by using the remoting stack is done by using a local proxy to the service through the `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` class.</span></span> <span data-ttu-id="0a801-121">The `ServiceProxyBase` method creates a local proxy by using the same interface that the service implements.</span><span class="sxs-lookup"><span data-stu-id="0a801-121">The `ServiceProxyBase` method creates a local proxy by using the same interface that the service implements.</span></span> <span data-ttu-id="0a801-122">With that proxy, you can simply call methods on the interface remotely.</span><span class="sxs-lookup"><span data-stu-id="0a801-122">With that proxy, you can simply call methods on the interface remotely.</span></span>

```java

MyService helloWorldClient = ServiceProxyBase.create(MyService.class, new URI("fabric:/MyApplication/MyHelloWorldService"));

CompletableFuture<String> message = helloWorldClient.helloWorldAsync();

```

<span data-ttu-id="0a801-123">The remoting framework propagates exceptions thrown at the service to the client.</span><span class="sxs-lookup"><span data-stu-id="0a801-123">The remoting framework propagates exceptions thrown at the service to the client.</span></span> <span data-ttu-id="0a801-124">So exception-handling logic at the client by using `ServiceProxyBase` can directly handle exceptions that the service throws.</span><span class="sxs-lookup"><span data-stu-id="0a801-124">So exception-handling logic at the client by using `ServiceProxyBase` can directly handle exceptions that the service throws.</span></span>

## <a name="service-proxy-lifetime"></a><span data-ttu-id="0a801-125">Service Proxy Lifetime</span><span class="sxs-lookup"><span data-stu-id="0a801-125">Service Proxy Lifetime</span></span>
<span data-ttu-id="0a801-126">ServiceProxy creation is a lightweight operation, so you can create as many as you need.</span><span class="sxs-lookup"><span data-stu-id="0a801-126">ServiceProxy creation is a lightweight operation, so you can create as many as you need.</span></span> <span data-ttu-id="0a801-127">Service Proxy instances can be reused as long as they are needed.</span><span class="sxs-lookup"><span data-stu-id="0a801-127">Service Proxy instances can be reused as long as they are needed.</span></span> <span data-ttu-id="0a801-128">If a remote procedure call throws an Exception, you can still reuse the same proxy instance.</span><span class="sxs-lookup"><span data-stu-id="0a801-128">If a remote procedure call throws an Exception, you can still reuse the same proxy instance.</span></span> <span data-ttu-id="0a801-129">Each ServiceProxy contains a communication client used to send messages over the wire.</span><span class="sxs-lookup"><span data-stu-id="0a801-129">Each ServiceProxy contains a communication client used to send messages over the wire.</span></span> <span data-ttu-id="0a801-130">While invoking remote calls, internal checks are performed to determine if the communication client is valid.</span><span class="sxs-lookup"><span data-stu-id="0a801-130">While invoking remote calls, internal checks are performed to determine if the communication client is valid.</span></span> <span data-ttu-id="0a801-131">Based on the results of those checks, the communication client is recreated if needed.</span><span class="sxs-lookup"><span data-stu-id="0a801-131">Based on the results of those checks, the communication client is recreated if needed.</span></span> <span data-ttu-id="0a801-132">Therefore, if an exception occurs, you do not need to recreate `ServiceProxy`.</span><span class="sxs-lookup"><span data-stu-id="0a801-132">Therefore, if an exception occurs, you do not need to recreate `ServiceProxy`.</span></span>

### <a name="serviceproxyfactory-lifetime"></a><span data-ttu-id="0a801-133">ServiceProxyFactory Lifetime</span><span class="sxs-lookup"><span data-stu-id="0a801-133">ServiceProxyFactory Lifetime</span></span>
<span data-ttu-id="0a801-134">[FabricServiceProxyFactory](https://docs.microsoft.com/java/api/microsoft.servicefabric.services.remoting.client._fabric_service_proxy_factory) is a factory that creates proxy for different remoting interfaces.</span><span class="sxs-lookup"><span data-stu-id="0a801-134">[FabricServiceProxyFactory](https://docs.microsoft.com/java/api/microsoft.servicefabric.services.remoting.client._fabric_service_proxy_factory) is a factory that creates proxy for different remoting interfaces.</span></span> <span data-ttu-id="0a801-135">If you use API `ServiceProxyBase.create` for creating proxy, then framework creates a `FabricServiceProxyFactory`.</span><span class="sxs-lookup"><span data-stu-id="0a801-135">If you use API `ServiceProxyBase.create` for creating proxy, then framework creates a `FabricServiceProxyFactory`.</span></span>
<span data-ttu-id="0a801-136">It is useful to create one manually when you need to override [ServiceRemotingClientFactory](https://docs.microsoft.com/java/api/microsoft.servicefabric.services.remoting.client._service_remoting_client_factory) properties.</span><span class="sxs-lookup"><span data-stu-id="0a801-136">It is useful to create one manually when you need to override [ServiceRemotingClientFactory](https://docs.microsoft.com/java/api/microsoft.servicefabric.services.remoting.client._service_remoting_client_factory) properties.</span></span>
<span data-ttu-id="0a801-137">Factory is an expensive operation.</span><span class="sxs-lookup"><span data-stu-id="0a801-137">Factory is an expensive operation.</span></span> <span data-ttu-id="0a801-138">`FabricServiceProxyFactory` maintains cache of communication clients.</span><span class="sxs-lookup"><span data-stu-id="0a801-138">`FabricServiceProxyFactory` maintains cache of communication clients.</span></span>
<span data-ttu-id="0a801-139">Best practice is to cache `FabricServiceProxyFactory` for as long as possible.</span><span class="sxs-lookup"><span data-stu-id="0a801-139">Best practice is to cache `FabricServiceProxyFactory` for as long as possible.</span></span>

## <a name="remoting-exception-handling"></a><span data-ttu-id="0a801-140">Remoting Exception Handling</span><span class="sxs-lookup"><span data-stu-id="0a801-140">Remoting Exception Handling</span></span>
<span data-ttu-id="0a801-141">All the remote exception thrown by service API, are sent back to the client either as RuntimeException or FabricException.</span><span class="sxs-lookup"><span data-stu-id="0a801-141">All the remote exception thrown by service API, are sent back to the client either as RuntimeException or FabricException.</span></span>

<span data-ttu-id="0a801-142">ServiceProxy does handle all Failover Exception for the service partition it  is created for.</span><span class="sxs-lookup"><span data-stu-id="0a801-142">ServiceProxy does handle all Failover Exception for the service partition it  is created for.</span></span> <span data-ttu-id="0a801-143">It re-resolves the endpoints if there is Failover Exceptions(Non-Transient Exceptions) and retries the call with the correct endpoint.</span><span class="sxs-lookup"><span data-stu-id="0a801-143">It re-resolves the endpoints if there is Failover Exceptions(Non-Transient Exceptions) and retries the call with the correct endpoint.</span></span> <span data-ttu-id="0a801-144">Number of retries for failover Exception is indefinite.</span><span class="sxs-lookup"><span data-stu-id="0a801-144">Number of retries for failover Exception is indefinite.</span></span>
<span data-ttu-id="0a801-145">In case of TransientExceptions, it only retries the call.</span><span class="sxs-lookup"><span data-stu-id="0a801-145">In case of TransientExceptions, it only retries the call.</span></span>

<span data-ttu-id="0a801-146">Default retry parameters are provied by [OperationRetrySettings].</span><span class="sxs-lookup"><span data-stu-id="0a801-146">Default retry parameters are provied by [OperationRetrySettings].</span></span> <span data-ttu-id="0a801-147">(https://docs.microsoft.com/java/api/microsoft.servicefabric.services.communication.client._operation_retry_settings) You can configure these values by passing OperationRetrySettings object to ServiceProxyFactory constructor.</span><span class="sxs-lookup"><span data-stu-id="0a801-147">(https://docs.microsoft.com/java/api/microsoft.servicefabric.services.communication.client._operation_retry_settings) You can configure these values by passing OperationRetrySettings object to ServiceProxyFactory constructor.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0a801-148">Next steps</span><span class="sxs-lookup"><span data-stu-id="0a801-148">Next steps</span></span>
* [<span data-ttu-id="0a801-149">Securing communication for Reliable Services</span><span class="sxs-lookup"><span data-stu-id="0a801-149">Securing communication for Reliable Services</span></span>](service-fabric-reliable-services-secure-communication-java.md)
