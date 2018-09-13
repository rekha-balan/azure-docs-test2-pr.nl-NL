---
title: Reliable Services communication overview | Microsoft Docs
description: Overview of the Reliable Services communication model, including opening listeners on services, resolving endpoints, and communicating between services.
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: BharatNarasimman
ms.assetid: 36217988-420e-409d-b0a4-e0e875b6eac8
ms.service: service-fabric
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 04/07/2017
ms.author: vturecek
ms.openlocfilehash: b841c23f07dd711b6e6bc97bc28e616eb0e06536
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552243"
---
# <a name="how-to-use-the-reliable-services-communication-apis"></a><span data-ttu-id="b72f1-103">How to use the Reliable Services communication APIs</span><span class="sxs-lookup"><span data-stu-id="b72f1-103">How to use the Reliable Services communication APIs</span></span>
<span data-ttu-id="b72f1-104">Azure Service Fabric as a platform is completely agnostic about communication between services.</span><span class="sxs-lookup"><span data-stu-id="b72f1-104">Azure Service Fabric as a platform is completely agnostic about communication between services.</span></span> <span data-ttu-id="b72f1-105">All protocols and stacks are acceptable, from UDP to HTTP.</span><span class="sxs-lookup"><span data-stu-id="b72f1-105">All protocols and stacks are acceptable, from UDP to HTTP.</span></span> <span data-ttu-id="b72f1-106">It's up to the service developer to choose how services should communicate.</span><span class="sxs-lookup"><span data-stu-id="b72f1-106">It's up to the service developer to choose how services should communicate.</span></span> <span data-ttu-id="b72f1-107">The Reliable Services application framework provides built-in communication stacks as well as APIs that you can use to build your custom communication components.</span><span class="sxs-lookup"><span data-stu-id="b72f1-107">The Reliable Services application framework provides built-in communication stacks as well as APIs that you can use to build your custom communication components.</span></span>

## <a name="set-up-service-communication"></a><span data-ttu-id="b72f1-108">Set up service communication</span><span class="sxs-lookup"><span data-stu-id="b72f1-108">Set up service communication</span></span>
<span data-ttu-id="b72f1-109">The Reliable Services API uses a simple interface for service communication.</span><span class="sxs-lookup"><span data-stu-id="b72f1-109">The Reliable Services API uses a simple interface for service communication.</span></span> <span data-ttu-id="b72f1-110">To open an endpoint for your service, simply implement this interface:</span><span class="sxs-lookup"><span data-stu-id="b72f1-110">To open an endpoint for your service, simply implement this interface:</span></span>

```csharp

public interface ICommunicationListener
{
    Task<string> OpenAsync(CancellationToken cancellationToken);

    Task CloseAsync(CancellationToken cancellationToken);

    void Abort();
}

```

```java
public interface CommunicationListener {
    CompletableFuture<String> openAsync(CancellationToken cancellationToken);

    CompletableFuture<?> closeAsync(CancellationToken cancellationToken);

    void abort();
}
```

<span data-ttu-id="b72f1-111">You can then add your communication listener implementation by returning it in a service-based class method override.</span><span class="sxs-lookup"><span data-stu-id="b72f1-111">You can then add your communication listener implementation by returning it in a service-based class method override.</span></span>

<span data-ttu-id="b72f1-112">For stateless services:</span><span class="sxs-lookup"><span data-stu-id="b72f1-112">For stateless services:</span></span>

```csharp
class MyStatelessService : StatelessService
{
    protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
    {
        ...
    }
    ...
}
```
```java
public class MyStatelessService extends StatelessService {

    @Override
    protected List<ServiceInstanceListener> createServiceInstanceListeners() {
        ...
    }
    ...
}
```

<span data-ttu-id="b72f1-113">For stateful services:</span><span class="sxs-lookup"><span data-stu-id="b72f1-113">For stateful services:</span></span>

> [!NOTE]
> <span data-ttu-id="b72f1-114">Stateful reliable services are not supported in Java yet.</span><span class="sxs-lookup"><span data-stu-id="b72f1-114">Stateful reliable services are not supported in Java yet.</span></span>
>
>

```csharp
class MyStatefulService : StatefulService
{
    protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
    {
        ...
    }
    ...
}
```

<span data-ttu-id="b72f1-115">In both cases, you return a collection of listeners.</span><span class="sxs-lookup"><span data-stu-id="b72f1-115">In both cases, you return a collection of listeners.</span></span> <span data-ttu-id="b72f1-116">This allows your service to listen on multiple endpoints, potentially using different protocols, by using multiple listeners.</span><span class="sxs-lookup"><span data-stu-id="b72f1-116">This allows your service to listen on multiple endpoints, potentially using different protocols, by using multiple listeners.</span></span> <span data-ttu-id="b72f1-117">For example, you may have an HTTP listener and a separate WebSocket listener.</span><span class="sxs-lookup"><span data-stu-id="b72f1-117">For example, you may have an HTTP listener and a separate WebSocket listener.</span></span> <span data-ttu-id="b72f1-118">Each listener gets a name, and the resulting collection of *name : address* pairs are represented as a JSON object when a client requests the listening addresses for a service instance or a partition.</span><span class="sxs-lookup"><span data-stu-id="b72f1-118">Each listener gets a name, and the resulting collection of *name : address* pairs are represented as a JSON object when a client requests the listening addresses for a service instance or a partition.</span></span>

<span data-ttu-id="b72f1-119">In a stateless service, the override returns a collection of ServiceInstanceListeners.</span><span class="sxs-lookup"><span data-stu-id="b72f1-119">In a stateless service, the override returns a collection of ServiceInstanceListeners.</span></span> <span data-ttu-id="b72f1-120">A `ServiceInstanceListener` contains a function to create an `ICommunicationListener(C#) / CommunicationListener(Java)` and gives it a name.</span><span class="sxs-lookup"><span data-stu-id="b72f1-120">A `ServiceInstanceListener` contains a function to create an `ICommunicationListener(C#) / CommunicationListener(Java)` and gives it a name.</span></span> <span data-ttu-id="b72f1-121">For stateful services, the override returns a collection of ServiceReplicaListeners.</span><span class="sxs-lookup"><span data-stu-id="b72f1-121">For stateful services, the override returns a collection of ServiceReplicaListeners.</span></span> <span data-ttu-id="b72f1-122">This is slightly different from its stateless counterpart, because a `ServiceReplicaListener` has an option to open an `ICommunicationListener` on secondary replicas.</span><span class="sxs-lookup"><span data-stu-id="b72f1-122">This is slightly different from its stateless counterpart, because a `ServiceReplicaListener` has an option to open an `ICommunicationListener` on secondary replicas.</span></span> <span data-ttu-id="b72f1-123">Not only can you use multiple communication listeners in a service, but you can also specify which listeners accept requests on secondary replicas and which ones listen only on primary replicas.</span><span class="sxs-lookup"><span data-stu-id="b72f1-123">Not only can you use multiple communication listeners in a service, but you can also specify which listeners accept requests on secondary replicas and which ones listen only on primary replicas.</span></span>

<span data-ttu-id="b72f1-124">For example, you can have a ServiceRemotingListener that takes RPC calls only on primary replicas, and a second, custom listener that takes read requests on secondary replicas over HTTP:</span><span class="sxs-lookup"><span data-stu-id="b72f1-124">For example, you can have a ServiceRemotingListener that takes RPC calls only on primary replicas, and a second, custom listener that takes read requests on secondary replicas over HTTP:</span></span>

```csharp
protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
{
    return new[]
    {
        new ServiceReplicaListener(context =>
            new MyCustomHttpListener(context),
            "HTTPReadonlyEndpoint",
            true),

        new ServiceReplicaListener(context =>
            this.CreateServiceRemotingListener(context),
            "rpcPrimaryEndpoint",
            false)
    };
}
```

> [!NOTE]
> <span data-ttu-id="b72f1-125">When creating multiple listeners for a service, each listener **must** be given a unique name.</span><span class="sxs-lookup"><span data-stu-id="b72f1-125">When creating multiple listeners for a service, each listener **must** be given a unique name.</span></span>
>
>

<span data-ttu-id="b72f1-126">Finally, describe the endpoints that are required for the service in the [service manifest](service-fabric-application-model.md) under the section on endpoints.</span><span class="sxs-lookup"><span data-stu-id="b72f1-126">Finally, describe the endpoints that are required for the service in the [service manifest](service-fabric-application-model.md) under the section on endpoints.</span></span>

```xml
<Resources>
    <Endpoints>
      <Endpoint Name="WebServiceEndpoint" Protocol="http" Port="80" />
      <Endpoint Name="OtherServiceEndpoint" Protocol="tcp" Port="8505" />
    <Endpoints>
</Resources>

```

<span data-ttu-id="b72f1-127">The communication listener can access the endpoint resources allocated to it from the `CodePackageActivationContext` in the `ServiceContext`.</span><span class="sxs-lookup"><span data-stu-id="b72f1-127">The communication listener can access the endpoint resources allocated to it from the `CodePackageActivationContext` in the `ServiceContext`.</span></span> <span data-ttu-id="b72f1-128">The listener can then start listening for requests when it is opened.</span><span class="sxs-lookup"><span data-stu-id="b72f1-128">The listener can then start listening for requests when it is opened.</span></span>

```csharp
var codePackageActivationContext = serviceContext.CodePackageActivationContext;
var port = codePackageActivationContext.GetEndpoint("ServiceEndpoint").Port;

```
```java
CodePackageActivationContext codePackageActivationContext = serviceContext.getCodePackageActivationContext();
int port = codePackageActivationContext.getEndpoint("ServiceEndpoint").getPort();

```

> [!NOTE]
> <span data-ttu-id="b72f1-129">Endpoint resources are common to the entire service package, and they are allocated by Service Fabric when the service package is activated.</span><span class="sxs-lookup"><span data-stu-id="b72f1-129">Endpoint resources are common to the entire service package, and they are allocated by Service Fabric when the service package is activated.</span></span> <span data-ttu-id="b72f1-130">Multiple service replicas hosted in the same ServiceHost may share the same port.</span><span class="sxs-lookup"><span data-stu-id="b72f1-130">Multiple service replicas hosted in the same ServiceHost may share the same port.</span></span> <span data-ttu-id="b72f1-131">This means that the communication listener should support port sharing.</span><span class="sxs-lookup"><span data-stu-id="b72f1-131">This means that the communication listener should support port sharing.</span></span> <span data-ttu-id="b72f1-132">The recommended way of doing this is for the communication listener to use the partition ID and replica/instance ID when it generates the listen address.</span><span class="sxs-lookup"><span data-stu-id="b72f1-132">The recommended way of doing this is for the communication listener to use the partition ID and replica/instance ID when it generates the listen address.</span></span>
>
>

### <a name="service-address-registration"></a><span data-ttu-id="b72f1-133">Service address registration</span><span class="sxs-lookup"><span data-stu-id="b72f1-133">Service address registration</span></span>
<span data-ttu-id="b72f1-134">A system service called the *Naming Service* runs on Service Fabric clusters.</span><span class="sxs-lookup"><span data-stu-id="b72f1-134">A system service called the *Naming Service* runs on Service Fabric clusters.</span></span> <span data-ttu-id="b72f1-135">The Naming Service is a registrar for services and their addresses that each instance or replica of the service is listening on.</span><span class="sxs-lookup"><span data-stu-id="b72f1-135">The Naming Service is a registrar for services and their addresses that each instance or replica of the service is listening on.</span></span> <span data-ttu-id="b72f1-136">When the `OpenAsync(C#) / openAsync(Java)` method of an `ICommunicationListener(C#) / CommunicationListener(Java)` completes, its return value gets registered in the Naming Service.</span><span class="sxs-lookup"><span data-stu-id="b72f1-136">When the `OpenAsync(C#) / openAsync(Java)` method of an `ICommunicationListener(C#) / CommunicationListener(Java)` completes, its return value gets registered in the Naming Service.</span></span> <span data-ttu-id="b72f1-137">This return value that gets published in the Naming Service is a string whose value can be anything at all.</span><span class="sxs-lookup"><span data-stu-id="b72f1-137">This return value that gets published in the Naming Service is a string whose value can be anything at all.</span></span> <span data-ttu-id="b72f1-138">This string value is what clients see when they ask for an address for the service from the Naming Service.</span><span class="sxs-lookup"><span data-stu-id="b72f1-138">This string value is what clients see when they ask for an address for the service from the Naming Service.</span></span>

```csharp
public Task<string> OpenAsync(CancellationToken cancellationToken)
{
    EndpointResourceDescription serviceEndpoint = serviceContext.CodePackageActivationContext.GetEndpoint("ServiceEndpoint");
    int port = serviceEndpoint.Port;

    this.listeningAddress = string.Format(
                CultureInfo.InvariantCulture,
                "http://+:{0}/",
                port);

    this.publishAddress = this.listeningAddress.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);

    this.webApp = WebApp.Start(this.listeningAddress, appBuilder => this.startup.Invoke(appBuilder));

    // the string returned here will be published in the Naming Service.
    return Task.FromResult(this.publishAddress);
}
```
```java
public CompletableFuture<String> openAsync(CancellationToken cancellationToken)
{
    EndpointResourceDescription serviceEndpoint = serviceContext.getCodePackageActivationContext.getEndpoint("ServiceEndpoint");
    int port = serviceEndpoint.getPort();

    this.publishAddress = String.format("http://%s:%d/", FabricRuntime.getNodeContext().getIpAddressOrFQDN(), port);

    this.webApp = new WebApp(port);
    this.webApp.start();

    /* the string returned here will be published in the Naming Service.
     */
    return CompletableFuture.completedFuture(this.publishAddress);
}
```

<span data-ttu-id="b72f1-139">Service Fabric provides APIs that allow clients and other services to then ask for this address by service name.</span><span class="sxs-lookup"><span data-stu-id="b72f1-139">Service Fabric provides APIs that allow clients and other services to then ask for this address by service name.</span></span> <span data-ttu-id="b72f1-140">This is important because the service address is not static.</span><span class="sxs-lookup"><span data-stu-id="b72f1-140">This is important because the service address is not static.</span></span> <span data-ttu-id="b72f1-141">Services are moved around in the cluster for resource balancing and availability purposes.</span><span class="sxs-lookup"><span data-stu-id="b72f1-141">Services are moved around in the cluster for resource balancing and availability purposes.</span></span> <span data-ttu-id="b72f1-142">This is the mechanism that allow clients to resolve the listening address for a service.</span><span class="sxs-lookup"><span data-stu-id="b72f1-142">This is the mechanism that allow clients to resolve the listening address for a service.</span></span>

> [!NOTE]
> <span data-ttu-id="b72f1-143">For a complete walk-through of how to write a communication listener, see [Service Fabric Web API services with OWIN self-hosting](service-fabric-reliable-services-communication-webapi.md) for C#, whereas for Java you can write your own HTTP server implementation, see EchoServer application example at https://github.com/Azure-Samples/service-fabric-java-getting-started.</span><span class="sxs-lookup"><span data-stu-id="b72f1-143">For a complete walk-through of how to write a communication listener, see [Service Fabric Web API services with OWIN self-hosting](service-fabric-reliable-services-communication-webapi.md) for C#, whereas for Java you can write your own HTTP server implementation, see EchoServer application example at https://github.com/Azure-Samples/service-fabric-java-getting-started.</span></span>
>
>

## <a name="communicating-with-a-service"></a><span data-ttu-id="b72f1-144">Communicating with a service</span><span class="sxs-lookup"><span data-stu-id="b72f1-144">Communicating with a service</span></span>
<span data-ttu-id="b72f1-145">The Reliable Services API provides the following libraries to write clients that communicate with services.</span><span class="sxs-lookup"><span data-stu-id="b72f1-145">The Reliable Services API provides the following libraries to write clients that communicate with services.</span></span>

### <a name="service-endpoint-resolution"></a><span data-ttu-id="b72f1-146">Service endpoint resolution</span><span class="sxs-lookup"><span data-stu-id="b72f1-146">Service endpoint resolution</span></span>
<span data-ttu-id="b72f1-147">The first step to communication with a service is to resolve an endpoint address of the partition or instance of the service you want to talk to.</span><span class="sxs-lookup"><span data-stu-id="b72f1-147">The first step to communication with a service is to resolve an endpoint address of the partition or instance of the service you want to talk to.</span></span> <span data-ttu-id="b72f1-148">The `ServicePartitionResolver(C#) / FabricServicePartitionResolver(Java)` utility class is a basic primitive that helps clients determine the endpoint of a service at runtime.</span><span class="sxs-lookup"><span data-stu-id="b72f1-148">The `ServicePartitionResolver(C#) / FabricServicePartitionResolver(Java)` utility class is a basic primitive that helps clients determine the endpoint of a service at runtime.</span></span> <span data-ttu-id="b72f1-149">In Service Fabric terminology, the process of determining the endpoint of a service is referred to as the *service endpoint resolution*.</span><span class="sxs-lookup"><span data-stu-id="b72f1-149">In Service Fabric terminology, the process of determining the endpoint of a service is referred to as the *service endpoint resolution*.</span></span>

<span data-ttu-id="b72f1-150">To connect to services within a cluster, ServicePartitionResolver can be created using default settings.</span><span class="sxs-lookup"><span data-stu-id="b72f1-150">To connect to services within a cluster, ServicePartitionResolver can be created using default settings.</span></span> <span data-ttu-id="b72f1-151">This is the recommended usage for most situations:</span><span class="sxs-lookup"><span data-stu-id="b72f1-151">This is the recommended usage for most situations:</span></span>

```csharp
ServicePartitionResolver resolver = ServicePartitionResolver.GetDefault();
```
```java
FabricServicePartitionResolver resolver = FabricServicePartitionResolver.getDefault();
```

<span data-ttu-id="b72f1-152">To connect to services in a different cluster, a ServicePartitionResolver can be created with a set of cluster gateway endpoints.</span><span class="sxs-lookup"><span data-stu-id="b72f1-152">To connect to services in a different cluster, a ServicePartitionResolver can be created with a set of cluster gateway endpoints.</span></span> <span data-ttu-id="b72f1-153">Note that gateway endpoints are just different endpoints for connecting to the same cluster.</span><span class="sxs-lookup"><span data-stu-id="b72f1-153">Note that gateway endpoints are just different endpoints for connecting to the same cluster.</span></span> <span data-ttu-id="b72f1-154">For example:</span><span class="sxs-lookup"><span data-stu-id="b72f1-154">For example:</span></span>

```csharp
ServicePartitionResolver resolver = new  ServicePartitionResolver("mycluster.cloudapp.azure.com:19000", "mycluster.cloudapp.azure.com:19001");
```
```java
FabricServicePartitionResolver resolver = new  FabricServicePartitionResolver("mycluster.cloudapp.azure.com:19000", "mycluster.cloudapp.azure.com:19001");
```

<span data-ttu-id="b72f1-155">Alternatively, `ServicePartitionResolver` can be given a function for creating a `FabricClient` to use internally:</span><span class="sxs-lookup"><span data-stu-id="b72f1-155">Alternatively, `ServicePartitionResolver` can be given a function for creating a `FabricClient` to use internally:</span></span>

```csharp
public delegate FabricClient CreateFabricClientDelegate();
```
```java
public FabricServicePartitionResolver(CreateFabricClient createFabricClient) {
...
}

public interface CreateFabricClient {
    public FabricClient getFabricClient();
}
```

<span data-ttu-id="b72f1-156">`FabricClient` is the object that is used to communicate with the Service Fabric cluster for various management operations on the cluster.</span><span class="sxs-lookup"><span data-stu-id="b72f1-156">`FabricClient` is the object that is used to communicate with the Service Fabric cluster for various management operations on the cluster.</span></span> <span data-ttu-id="b72f1-157">This is useful when you want more control over how a service partition resolver interacts with your cluster.</span><span class="sxs-lookup"><span data-stu-id="b72f1-157">This is useful when you want more control over how a service partition resolver interacts with your cluster.</span></span> <span data-ttu-id="b72f1-158">`FabricClient` performs caching internally and is generally expensive to create, so it is important to reuse `FabricClient` instances as much as possible.</span><span class="sxs-lookup"><span data-stu-id="b72f1-158">`FabricClient` performs caching internally and is generally expensive to create, so it is important to reuse `FabricClient` instances as much as possible.</span></span>

```csharp
ServicePartitionResolver resolver = new  ServicePartitionResolver(() => CreateMyFabricClient());
```
```java
FabricServicePartitionResolver resolver = new  FabricServicePartitionResolver(() -> new CreateFabricClientImpl());
```

<span data-ttu-id="b72f1-159">A resolve method is then used to retrieve the address of a service or a service partition for partitioned services.</span><span class="sxs-lookup"><span data-stu-id="b72f1-159">A resolve method is then used to retrieve the address of a service or a service partition for partitioned services.</span></span>

```csharp
ServicePartitionResolver resolver = ServicePartitionResolver.GetDefault();

ResolvedServicePartition partition =
    await resolver.ResolveAsync(new Uri("fabric:/MyApp/MyService"), new ServicePartitionKey(), cancellationToken);
```
```java
FabricServicePartitionResolver resolver = FabricServicePartitionResolver.getDefault();

CompletableFuture<ResolvedServicePartition> partition =
    resolver.resolveAsync(new URI("fabric:/MyApp/MyService"), new ServicePartitionKey());
```

<span data-ttu-id="b72f1-160">A service address can be resolved easily using a ServicePartitionResolver, but more work is required to ensure the resolved address can be used correctly.</span><span class="sxs-lookup"><span data-stu-id="b72f1-160">A service address can be resolved easily using a ServicePartitionResolver, but more work is required to ensure the resolved address can be used correctly.</span></span> <span data-ttu-id="b72f1-161">Your client needs to detect whether the connection attempt failed because of a transient error and can be retried (e.g., service moved or is temporarily unavailable), or a permanent error (e.g., service was deleted or the requested resource no longer exists).</span><span class="sxs-lookup"><span data-stu-id="b72f1-161">Your client needs to detect whether the connection attempt failed because of a transient error and can be retried (e.g., service moved or is temporarily unavailable), or a permanent error (e.g., service was deleted or the requested resource no longer exists).</span></span> <span data-ttu-id="b72f1-162">Service instances or replicas can move around from node to node at any time for multiple reasons.</span><span class="sxs-lookup"><span data-stu-id="b72f1-162">Service instances or replicas can move around from node to node at any time for multiple reasons.</span></span> <span data-ttu-id="b72f1-163">The service address resolved through ServicePartitionResolver may be stale by the time your client code attempts to connect.</span><span class="sxs-lookup"><span data-stu-id="b72f1-163">The service address resolved through ServicePartitionResolver may be stale by the time your client code attempts to connect.</span></span> <span data-ttu-id="b72f1-164">In that case again the client needs to re-resolve the address.</span><span class="sxs-lookup"><span data-stu-id="b72f1-164">In that case again the client needs to re-resolve the address.</span></span> <span data-ttu-id="b72f1-165">Providing the previous `ResolvedServicePartition` indicates that the resolver needs to try again rather than simply retrieve a cached address.</span><span class="sxs-lookup"><span data-stu-id="b72f1-165">Providing the previous `ResolvedServicePartition` indicates that the resolver needs to try again rather than simply retrieve a cached address.</span></span>

<span data-ttu-id="b72f1-166">Typically, the client code need not work with the ServicePartitionResolver directly.</span><span class="sxs-lookup"><span data-stu-id="b72f1-166">Typically, the client code need not work with the ServicePartitionResolver directly.</span></span> <span data-ttu-id="b72f1-167">It is created and passed on to communication client factories in the Reliable Services API.</span><span class="sxs-lookup"><span data-stu-id="b72f1-167">It is created and passed on to communication client factories in the Reliable Services API.</span></span> <span data-ttu-id="b72f1-168">The factories use the resolver internally to generate a client object that can be used to communicate with services.</span><span class="sxs-lookup"><span data-stu-id="b72f1-168">The factories use the resolver internally to generate a client object that can be used to communicate with services.</span></span>

### <a name="communication-clients-and-factories"></a><span data-ttu-id="b72f1-169">Communication clients and factories</span><span class="sxs-lookup"><span data-stu-id="b72f1-169">Communication clients and factories</span></span>
<span data-ttu-id="b72f1-170">The communication factory library implements a typical fault-handling retry pattern that makes retrying connections to resolved service endpoints easier.</span><span class="sxs-lookup"><span data-stu-id="b72f1-170">The communication factory library implements a typical fault-handling retry pattern that makes retrying connections to resolved service endpoints easier.</span></span> <span data-ttu-id="b72f1-171">The factory library provides the retry mechanism while you provide the error handlers.</span><span class="sxs-lookup"><span data-stu-id="b72f1-171">The factory library provides the retry mechanism while you provide the error handlers.</span></span>

<span data-ttu-id="b72f1-172">`ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)` defines the base interface implemented by a communication client factory that produces clients that can talk to a Service Fabric service.</span><span class="sxs-lookup"><span data-stu-id="b72f1-172">`ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)` defines the base interface implemented by a communication client factory that produces clients that can talk to a Service Fabric service.</span></span> <span data-ttu-id="b72f1-173">The implementation of the CommunicationClientFactory depends on the communication stack used by the Service Fabric service where the client wants to communicate.</span><span class="sxs-lookup"><span data-stu-id="b72f1-173">The implementation of the CommunicationClientFactory depends on the communication stack used by the Service Fabric service where the client wants to communicate.</span></span> <span data-ttu-id="b72f1-174">The Reliable Services API provides a `CommunicationClientFactoryBase<TCommunicationClient>`.</span><span class="sxs-lookup"><span data-stu-id="b72f1-174">The Reliable Services API provides a `CommunicationClientFactoryBase<TCommunicationClient>`.</span></span> <span data-ttu-id="b72f1-175">This provides a base implementation of the CommunicationClientFactory interface and performs tasks that are common to all the communication stacks.</span><span class="sxs-lookup"><span data-stu-id="b72f1-175">This provides a base implementation of the CommunicationClientFactory interface and performs tasks that are common to all the communication stacks.</span></span> <span data-ttu-id="b72f1-176">(These tasks include using a ServicePartitionResolver to determine the service endpoint).</span><span class="sxs-lookup"><span data-stu-id="b72f1-176">(These tasks include using a ServicePartitionResolver to determine the service endpoint).</span></span> <span data-ttu-id="b72f1-177">Clients usually implement the abstract CommunicationClientFactoryBase class to handle logic that is specific to the communication stack.</span><span class="sxs-lookup"><span data-stu-id="b72f1-177">Clients usually implement the abstract CommunicationClientFactoryBase class to handle logic that is specific to the communication stack.</span></span>

<span data-ttu-id="b72f1-178">The communication client just receives an address and uses it to connect to a service.</span><span class="sxs-lookup"><span data-stu-id="b72f1-178">The communication client just receives an address and uses it to connect to a service.</span></span> <span data-ttu-id="b72f1-179">The client can use whatever protocol it wants.</span><span class="sxs-lookup"><span data-stu-id="b72f1-179">The client can use whatever protocol it wants.</span></span>

```csharp
class MyCommunicationClient : ICommunicationClient
{
    public ResolvedServiceEndpoint Endpoint { get; set; }

    public string ListenerName { get; set; }

    public ResolvedServicePartition ResolvedServicePartition { get; set; }
}
```
```java
public class MyCommunicationClient implements CommunicationClient {

    private ResolvedServicePartition resolvedServicePartition;
    private String listenerName;
    private ResolvedServiceEndpoint endPoint;

    /*
     * Getters and Setters
     */
}
```

<span data-ttu-id="b72f1-180">The client factory is primarily responsible for creating communication clients.</span><span class="sxs-lookup"><span data-stu-id="b72f1-180">The client factory is primarily responsible for creating communication clients.</span></span> <span data-ttu-id="b72f1-181">For clients that don't maintain a persistent connection, such as an HTTP client, the factory only needs to create and return the client.</span><span class="sxs-lookup"><span data-stu-id="b72f1-181">For clients that don't maintain a persistent connection, such as an HTTP client, the factory only needs to create and return the client.</span></span> <span data-ttu-id="b72f1-182">Other protocols that maintain a persistent connection, such as some binary protocols, should also be validated by the factory to determine whether the connection needs to be re-created.</span><span class="sxs-lookup"><span data-stu-id="b72f1-182">Other protocols that maintain a persistent connection, such as some binary protocols, should also be validated by the factory to determine whether the connection needs to be re-created.</span></span>  

```csharp
public class MyCommunicationClientFactory : CommunicationClientFactoryBase<MyCommunicationClient>
{
    protected override void AbortClient(MyCommunicationClient client)
    {
    }

    protected override Task<MyCommunicationClient> CreateClientAsync(string endpoint, CancellationToken cancellationToken)
    {
    }

    protected override bool ValidateClient(MyCommunicationClient clientChannel)
    {
    }

    protected override bool ValidateClient(string endpoint, MyCommunicationClient client)
    {
    }
}
```
```java
public class MyCommunicationClientFactory extends CommunicationClientFactoryBase<MyCommunicationClient> {

    @Override
    protected boolean validateClient(MyCommunicationClient clientChannel) {
    }

    @Override
    protected boolean validateClient(String endpoint, MyCommunicationClient client) {
    }

    @Override
    protected CompletableFuture<MyCommunicationClient> createClientAsync(String endpoint) {
    }

    @Override
    protected void abortClient(MyCommunicationClient client) {
    }
}
```

<span data-ttu-id="b72f1-183">Finally, an exception handler is responsible for determining what action to take when an exception occurs.</span><span class="sxs-lookup"><span data-stu-id="b72f1-183">Finally, an exception handler is responsible for determining what action to take when an exception occurs.</span></span> <span data-ttu-id="b72f1-184">Exceptions are categorized into **retryable** and **non retryable**.</span><span class="sxs-lookup"><span data-stu-id="b72f1-184">Exceptions are categorized into **retryable** and **non retryable**.</span></span>

* <span data-ttu-id="b72f1-185">**Non retryable** exceptions simply get rethrown back to the caller.</span><span class="sxs-lookup"><span data-stu-id="b72f1-185">**Non retryable** exceptions simply get rethrown back to the caller.</span></span>
* <span data-ttu-id="b72f1-186">**retryable** exceptions are further categorized into **transient** and **non-transient**.</span><span class="sxs-lookup"><span data-stu-id="b72f1-186">**retryable** exceptions are further categorized into **transient** and **non-transient**.</span></span>
  * <span data-ttu-id="b72f1-187">**Transient** exceptions are those that can simply be retried without re-resolving the service endpoint address.</span><span class="sxs-lookup"><span data-stu-id="b72f1-187">**Transient** exceptions are those that can simply be retried without re-resolving the service endpoint address.</span></span> <span data-ttu-id="b72f1-188">These will include transient network problems or service error responses other than those that indicate the service endpoint address does not exist.</span><span class="sxs-lookup"><span data-stu-id="b72f1-188">These will include transient network problems or service error responses other than those that indicate the service endpoint address does not exist.</span></span>
  * <span data-ttu-id="b72f1-189">**Non-transient** exceptions are those that require the service endpoint address to be re-resolved.</span><span class="sxs-lookup"><span data-stu-id="b72f1-189">**Non-transient** exceptions are those that require the service endpoint address to be re-resolved.</span></span> <span data-ttu-id="b72f1-190">These include exceptions that indicate the service endpoint could not be reached, indicating the service has moved to a different node.</span><span class="sxs-lookup"><span data-stu-id="b72f1-190">These include exceptions that indicate the service endpoint could not be reached, indicating the service has moved to a different node.</span></span>

<span data-ttu-id="b72f1-191">The `TryHandleException` makes a decision about a given exception.</span><span class="sxs-lookup"><span data-stu-id="b72f1-191">The `TryHandleException` makes a decision about a given exception.</span></span> <span data-ttu-id="b72f1-192">If it **does not know** what decisions to make about an exception, it should return **false**.</span><span class="sxs-lookup"><span data-stu-id="b72f1-192">If it **does not know** what decisions to make about an exception, it should return **false**.</span></span> <span data-ttu-id="b72f1-193">If it **does know** what decision to make, it should set the result accordingly and return **true**.</span><span class="sxs-lookup"><span data-stu-id="b72f1-193">If it **does know** what decision to make, it should set the result accordingly and return **true**.</span></span>

```csharp
class MyExceptionHandler : IExceptionHandler
{
    public bool TryHandleException(ExceptionInformation exceptionInformation, OperationRetrySettings retrySettings, out ExceptionHandlingResult result)
    {
        // if exceptionInformation.Exception is known and is transient (can be retried without re-resolving)
        result = new ExceptionHandlingRetryResult(exceptionInformation.Exception, true, retrySettings, retrySettings.DefaultMaxRetryCount);
        return true;


        // if exceptionInformation.Exception is known and is not transient (indicates a new service endpoint address must be resolved)
        result = new ExceptionHandlingRetryResult(exceptionInformation.Exception, false, retrySettings, retrySettings.DefaultMaxRetryCount);
        return true;

        // if exceptionInformation.Exception is unknown (let the next IExceptionHandler attempt to handle it)
        result = null;
        return false;
    }
}
```
```java
public class MyExceptionHandler implements ExceptionHandler {

    @Override
    public ExceptionHandlingResult handleException(ExceptionInformation exceptionInformation, OperationRetrySettings retrySettings) {        

        /* if exceptionInformation.getException() is known and is transient (can be retried without re-resolving)
         */
        result = new ExceptionHandlingRetryResult(exceptionInformation.getException(), true, retrySettings, retrySettings.getDefaultMaxRetryCount());
        return true;


        /* if exceptionInformation.getException() is known and is not transient (indicates a new service endpoint address must be resolved)
         */
        result = new ExceptionHandlingRetryResult(exceptionInformation.getException(), false, retrySettings, retrySettings.getDefaultMaxRetryCount());
        return true;

        /* if exceptionInformation.getException() is unknown (let the next ExceptionHandler attempt to handle it)
         */
        result = null;
        return false;

    }
}
```
### <a name="putting-it-all-together"></a><span data-ttu-id="b72f1-194">Putting it all together</span><span class="sxs-lookup"><span data-stu-id="b72f1-194">Putting it all together</span></span>
<span data-ttu-id="b72f1-195">With an `ICommunicationClient(C#) / CommunicationClient(Java)`, `ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)`, and `IExceptionHandler(C#) / ExceptionHandler(Java)` built around a communication protocol, a `ServicePartitionClient(C#) / FabricServicePartitionClient(Java)` wraps it all together and provides the fault-handling and service partition address resolution loop around these components.</span><span class="sxs-lookup"><span data-stu-id="b72f1-195">With an `ICommunicationClient(C#) / CommunicationClient(Java)`, `ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)`, and `IExceptionHandler(C#) / ExceptionHandler(Java)` built around a communication protocol, a `ServicePartitionClient(C#) / FabricServicePartitionClient(Java)` wraps it all together and provides the fault-handling and service partition address resolution loop around these components.</span></span>

```csharp
private MyCommunicationClientFactory myCommunicationClientFactory;
private Uri myServiceUri;

var myServicePartitionClient = new ServicePartitionClient<MyCommunicationClient>(
    this.myCommunicationClientFactory,
    this.myServiceUri,
    myPartitionKey);

var result = await myServicePartitionClient.InvokeWithRetryAsync(async (client) =>
   {
      // Communicate with the service using the client.
   },
   CancellationToken.None);

```
```java
private MyCommunicationClientFactory myCommunicationClientFactory;
private URI myServiceUri;

FabricServicePartitionClient myServicePartitionClient = new FabricServicePartitionClient<MyCommunicationClient>(
    this.myCommunicationClientFactory,
    this.myServiceUri,
    myPartitionKey);

CompletableFuture<?> result = myServicePartitionClient.invokeWithRetryAsync(client -> {
      /* Communicate with the service using the client.
       */
   });

```

## <a name="next-steps"></a><span data-ttu-id="b72f1-196">Next steps</span><span class="sxs-lookup"><span data-stu-id="b72f1-196">Next steps</span></span>
* <span data-ttu-id="b72f1-197">See an example of HTTP communication between services in a [C# sample project on GitHUb](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount) or [Java sample project on GitHUb](https://github.com/Azure-Samples/service-fabric-java-getting-started/tree/master/Services/WatchDog).</span><span class="sxs-lookup"><span data-stu-id="b72f1-197">See an example of HTTP communication between services in a [C# sample project on GitHUb](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount) or [Java sample project on GitHUb](https://github.com/Azure-Samples/service-fabric-java-getting-started/tree/master/Services/WatchDog).</span></span>
* [<span data-ttu-id="b72f1-198">Remote procedure calls with Reliable Services remoting</span><span class="sxs-lookup"><span data-stu-id="b72f1-198">Remote procedure calls with Reliable Services remoting</span></span>](service-fabric-reliable-services-communication-remoting.md)
* [<span data-ttu-id="b72f1-199">Web API that uses OWIN in Reliable Services</span><span class="sxs-lookup"><span data-stu-id="b72f1-199">Web API that uses OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="b72f1-200">WCF communication by using Reliable Services</span><span class="sxs-lookup"><span data-stu-id="b72f1-200">WCF communication by using Reliable Services</span></span>](service-fabric-reliable-services-communication-wcf.md)
