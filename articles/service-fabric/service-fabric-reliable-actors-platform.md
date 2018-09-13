---
title: Reliable Actors on Service Fabric | Microsoft Docs
description: Describes how Reliable Actors are layered on Reliable Services and use the features of the Service Fabric platform.
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: amanbha
ms.assetid: 45839a7f-0536-46f1-ae2b-8ba3556407fb
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/07/2017
ms.author: vturecek
ms.openlocfilehash: eabd42cb1c08ca2157c680fe6e5aa2aa72da033e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553208"
---
# <a name="how-reliable-actors-use-the-service-fabric-platform"></a><span data-ttu-id="826cc-103">How Reliable Actors use the Service Fabric platform</span><span class="sxs-lookup"><span data-stu-id="826cc-103">How Reliable Actors use the Service Fabric platform</span></span>
<span data-ttu-id="826cc-104">This article explains how Reliable Actors work on the Azure Service Fabric platform.</span><span class="sxs-lookup"><span data-stu-id="826cc-104">This article explains how Reliable Actors work on the Azure Service Fabric platform.</span></span> <span data-ttu-id="826cc-105">Reliable Actors run in a framework that is hosted in an implementation of a stateful reliable service called the *actor service*.</span><span class="sxs-lookup"><span data-stu-id="826cc-105">Reliable Actors run in a framework that is hosted in an implementation of a stateful reliable service called the *actor service*.</span></span> <span data-ttu-id="826cc-106">The actor service contains all the components necessary to manage the lifecycle and message dispatching for your actors:</span><span class="sxs-lookup"><span data-stu-id="826cc-106">The actor service contains all the components necessary to manage the lifecycle and message dispatching for your actors:</span></span>

* <span data-ttu-id="826cc-107">The Actor Runtime manages lifecycle, garbage collection, and enforces single-threaded access.</span><span class="sxs-lookup"><span data-stu-id="826cc-107">The Actor Runtime manages lifecycle, garbage collection, and enforces single-threaded access.</span></span>
* <span data-ttu-id="826cc-108">An actor service remoting listener accepts remote access calls to actors and sends them to a dispatcher to route to the appropriate actor instance.</span><span class="sxs-lookup"><span data-stu-id="826cc-108">An actor service remoting listener accepts remote access calls to actors and sends them to a dispatcher to route to the appropriate actor instance.</span></span>
* <span data-ttu-id="826cc-109">The Actor State Provider wraps state providers (such as the Reliable Collections state provider) and provides an adapter for actor state management.</span><span class="sxs-lookup"><span data-stu-id="826cc-109">The Actor State Provider wraps state providers (such as the Reliable Collections state provider) and provides an adapter for actor state management.</span></span>

<span data-ttu-id="826cc-110">These components together form the Reliable Actor framework.</span><span class="sxs-lookup"><span data-stu-id="826cc-110">These components together form the Reliable Actor framework.</span></span>

## <a name="service-layering"></a><span data-ttu-id="826cc-111">Service layering</span><span class="sxs-lookup"><span data-stu-id="826cc-111">Service layering</span></span>
<span data-ttu-id="826cc-112">Because the actor service itself is a reliable service, all the [application model](service-fabric-application-model.md), lifecycle, [packaging](service-fabric-package-apps.md), [deployment](service-fabric-deploy-remove-applications.md), upgrade, and scaling concepts of Reliable Services apply the same way to actor services.</span><span class="sxs-lookup"><span data-stu-id="826cc-112">Because the actor service itself is a reliable service, all the [application model](service-fabric-application-model.md), lifecycle, [packaging](service-fabric-package-apps.md), [deployment](service-fabric-deploy-remove-applications.md), upgrade, and scaling concepts of Reliable Services apply the same way to actor services.</span></span> 

![Actor service layering][1]

<span data-ttu-id="826cc-114">The preceding diagram shows the relationship between the Service Fabric application frameworks and user code.</span><span class="sxs-lookup"><span data-stu-id="826cc-114">The preceding diagram shows the relationship between the Service Fabric application frameworks and user code.</span></span> <span data-ttu-id="826cc-115">Blue elements represent the Reliable Services application framework, orange represents the Reliable Actor framework, and green represents user code.</span><span class="sxs-lookup"><span data-stu-id="826cc-115">Blue elements represent the Reliable Services application framework, orange represents the Reliable Actor framework, and green represents user code.</span></span>

<span data-ttu-id="826cc-116">In Reliable Services, your service inherits the `StatefulService` class.</span><span class="sxs-lookup"><span data-stu-id="826cc-116">In Reliable Services, your service inherits the `StatefulService` class.</span></span> <span data-ttu-id="826cc-117">This class is itself derived from `StatefulServiceBase` (or `StatelessService` for stateless services).</span><span class="sxs-lookup"><span data-stu-id="826cc-117">This class is itself derived from `StatefulServiceBase` (or `StatelessService` for stateless services).</span></span> <span data-ttu-id="826cc-118">In Reliable Actors, you use the actor service.</span><span class="sxs-lookup"><span data-stu-id="826cc-118">In Reliable Actors, you use the actor service.</span></span> <span data-ttu-id="826cc-119">The actor service is a different implementation of the `StatefulServiceBase` class that implements the actor pattern where your actors run.</span><span class="sxs-lookup"><span data-stu-id="826cc-119">The actor service is a different implementation of the `StatefulServiceBase` class that implements the actor pattern where your actors run.</span></span> <span data-ttu-id="826cc-120">Because the actor service itself is just an implementation of `StatefulServiceBase`, you can write your own service that derives from `ActorService` and implement service-level features the same way you would when inheriting `StatefulService`, such as:</span><span class="sxs-lookup"><span data-stu-id="826cc-120">Because the actor service itself is just an implementation of `StatefulServiceBase`, you can write your own service that derives from `ActorService` and implement service-level features the same way you would when inheriting `StatefulService`, such as:</span></span>

* <span data-ttu-id="826cc-121">Service backup and restore.</span><span class="sxs-lookup"><span data-stu-id="826cc-121">Service backup and restore.</span></span>
* <span data-ttu-id="826cc-122">Shared functionality for all actors, for example, a circuit breaker.</span><span class="sxs-lookup"><span data-stu-id="826cc-122">Shared functionality for all actors, for example, a circuit breaker.</span></span>
* <span data-ttu-id="826cc-123">Remote procedure calls on the actor service itself and on each individual actor.</span><span class="sxs-lookup"><span data-stu-id="826cc-123">Remote procedure calls on the actor service itself and on each individual actor.</span></span>

> [!NOTE]
> <span data-ttu-id="826cc-124">Stateful services are not currently supported in Java/Linux.</span><span class="sxs-lookup"><span data-stu-id="826cc-124">Stateful services are not currently supported in Java/Linux.</span></span>

### <a name="using-the-actor-service"></a><span data-ttu-id="826cc-125">Using the actor service</span><span class="sxs-lookup"><span data-stu-id="826cc-125">Using the actor service</span></span>
<span data-ttu-id="826cc-126">Actor instances have access to the actor service in which they are running.</span><span class="sxs-lookup"><span data-stu-id="826cc-126">Actor instances have access to the actor service in which they are running.</span></span> <span data-ttu-id="826cc-127">Through the actor service, actor instances can programmatically obtain the service context.</span><span class="sxs-lookup"><span data-stu-id="826cc-127">Through the actor service, actor instances can programmatically obtain the service context.</span></span> <span data-ttu-id="826cc-128">The service context has the partition ID, service name, application name, and other Service Fabric platform-specific information:</span><span class="sxs-lookup"><span data-stu-id="826cc-128">The service context has the partition ID, service name, application name, and other Service Fabric platform-specific information:</span></span>

```csharp
Task MyActorMethod()
{
    Guid partitionId = this.ActorService.Context.PartitionId;
    string serviceTypeName = this.ActorService.Context.ServiceTypeName;
    Uri serviceInstanceName = this.ActorService.Context.ServiceName;
    string applicationInstanceName = this.ActorService.Context.CodePackageActivationContext.ApplicationName;
}
```
```Java
CompletableFuture<?> MyActorMethod()
{
    UUID partitionId = this.getActorService().getServiceContext().getPartitionId();
    String serviceTypeName = this.getActorService().getServiceContext().getServiceTypeName();
    URI serviceInstanceName = this.getActorService().getServiceContext().getServiceName();
    String applicationInstanceName = this.getActorService().getServiceContext().getCodePackageActivationContext().getApplicationName();
}
```


<span data-ttu-id="826cc-129">Like all Reliable Services, the actor service must be registered with a service type in the Service Fabric runtime.</span><span class="sxs-lookup"><span data-stu-id="826cc-129">Like all Reliable Services, the actor service must be registered with a service type in the Service Fabric runtime.</span></span> <span data-ttu-id="826cc-130">For the actor service to run your actor instances, your actor type must also be registered with the actor service.</span><span class="sxs-lookup"><span data-stu-id="826cc-130">For the actor service to run your actor instances, your actor type must also be registered with the actor service.</span></span> <span data-ttu-id="826cc-131">The `ActorRuntime` registration method performs this work for actors.</span><span class="sxs-lookup"><span data-stu-id="826cc-131">The `ActorRuntime` registration method performs this work for actors.</span></span> <span data-ttu-id="826cc-132">In the simplest case, you can just register your actor type, and the actor service with default settings will implicitly be used:</span><span class="sxs-lookup"><span data-stu-id="826cc-132">In the simplest case, you can just register your actor type, and the actor service with default settings will implicitly be used:</span></span>

```csharp
static class Program
{
    private static void Main()
    {
        ActorRuntime.RegisterActorAsync<MyActor>().GetAwaiter().GetResult();

        Thread.Sleep(Timeout.Infinite);
    }
}
```

<span data-ttu-id="826cc-133">Alternatively, you can use a lambda provided by the registration method to construct the actor service yourself.</span><span class="sxs-lookup"><span data-stu-id="826cc-133">Alternatively, you can use a lambda provided by the registration method to construct the actor service yourself.</span></span> <span data-ttu-id="826cc-134">You can then configure the actor service and explicitly construct your actor instances, where you can inject dependencies to your actor through its constructor:</span><span class="sxs-lookup"><span data-stu-id="826cc-134">You can then configure the actor service and explicitly construct your actor instances, where you can inject dependencies to your actor through its constructor:</span></span>

```csharp
static class Program
{
    private static void Main()
    {
        ActorRuntime.RegisterActorAsync<MyActor>(
            (context, actorType) => new ActorService(context, actorType, () => new MyActor()))
            .GetAwaiter().GetResult();

        Thread.Sleep(Timeout.Infinite);
    }
}
```
```Java
static class Program
{
    private static void Main()
    {
      ActorRuntime.registerActorAsync(
              MyActor.class,
              (context, actorTypeInfo) -> new FabricActorService(context, actorTypeInfo),
              timeout);

        Thread.sleep(Long.MAX_VALUE);
    }
}
```

### <a name="actor-service-methods"></a><span data-ttu-id="826cc-135">Actor service methods</span><span class="sxs-lookup"><span data-stu-id="826cc-135">Actor service methods</span></span>
<span data-ttu-id="826cc-136">The Actor service implements `IActorService` (C#) or `ActorService` (Java), which in turn implements `IService` (C#) or `Service` (Java).</span><span class="sxs-lookup"><span data-stu-id="826cc-136">The Actor service implements `IActorService` (C#) or `ActorService` (Java), which in turn implements `IService` (C#) or `Service` (Java).</span></span> <span data-ttu-id="826cc-137">This is the interface used by Reliable Services remoting, which allows remote procedure calls on service methods.</span><span class="sxs-lookup"><span data-stu-id="826cc-137">This is the interface used by Reliable Services remoting, which allows remote procedure calls on service methods.</span></span> <span data-ttu-id="826cc-138">It contains service-level methods that can be called remotely via service remoting.</span><span class="sxs-lookup"><span data-stu-id="826cc-138">It contains service-level methods that can be called remotely via service remoting.</span></span>

#### <a name="enumerating-actors"></a><span data-ttu-id="826cc-139">Enumerating actors</span><span class="sxs-lookup"><span data-stu-id="826cc-139">Enumerating actors</span></span>
<span data-ttu-id="826cc-140">The actor service allows a client to enumerate metadata about the actors that the service is hosting.</span><span class="sxs-lookup"><span data-stu-id="826cc-140">The actor service allows a client to enumerate metadata about the actors that the service is hosting.</span></span> <span data-ttu-id="826cc-141">Because the actor service is a partitioned stateful service, enumeration is performed per partition.</span><span class="sxs-lookup"><span data-stu-id="826cc-141">Because the actor service is a partitioned stateful service, enumeration is performed per partition.</span></span> <span data-ttu-id="826cc-142">Because each partition might contain many actors, the enumeration is returned as a set of paged results.</span><span class="sxs-lookup"><span data-stu-id="826cc-142">Because each partition might contain many actors, the enumeration is returned as a set of paged results.</span></span> <span data-ttu-id="826cc-143">The pages are looped over until all pages are read.</span><span class="sxs-lookup"><span data-stu-id="826cc-143">The pages are looped over until all pages are read.</span></span> <span data-ttu-id="826cc-144">The following example shows how to create a list of all active actors in one partition of an actor service:</span><span class="sxs-lookup"><span data-stu-id="826cc-144">The following example shows how to create a list of all active actors in one partition of an actor service:</span></span>

```csharp
IActorService actorServiceProxy = ActorServiceProxy.Create(
    new Uri("fabric:/MyApp/MyService"), partitionKey);

ContinuationToken continuationToken = null;
List<ActorInformation> activeActors = new List<ActorInformation>();

do
{
    PagedResult<ActorInformation> page = await actorServiceProxy.GetActorsAsync(continuationToken, cancellationToken);

    activeActors.AddRange(page.Items.Where(x => x.IsActive));

    continuationToken = page.ContinuationToken;
}
while (continuationToken != null);
```

```Java
ActorService actorServiceProxy = ActorServiceProxy.create(
    new URI("fabric:/MyApp/MyService"), partitionKey);

ContinuationToken continuationToken = null;
List<ActorInformation> activeActors = new ArrayList<ActorInformation>();

do
{
    PagedResult<ActorInformation> page = actorServiceProxy.getActorsAsync(continuationToken);

    while(ActorInformation x: page.getItems())
    {
         if(x.isActive()){
              activeActors.add(x);
         }
    }

    continuationToken = page.getContinuationToken();
}
while (continuationToken != null);
```

#### <a name="deleting-actors"></a><span data-ttu-id="826cc-145">Deleting actors</span><span class="sxs-lookup"><span data-stu-id="826cc-145">Deleting actors</span></span>
<span data-ttu-id="826cc-146">The actor service also provides a function for deleting actors:</span><span class="sxs-lookup"><span data-stu-id="826cc-146">The actor service also provides a function for deleting actors:</span></span>

```csharp
ActorId actorToDelete = new ActorId(id);

IActorService myActorServiceProxy = ActorServiceProxy.Create(
    new Uri("fabric:/MyApp/MyService"), actorToDelete);

await myActorServiceProxy.DeleteActorAsync(actorToDelete, cancellationToken)
```
```Java
ActorId actorToDelete = new ActorId(id);

ActorService myActorServiceProxy = ActorServiceProxy.create(
    new URI("fabric:/MyApp/MyService"), actorToDelete);

myActorServiceProxy.deleteActorAsync(actorToDelete);
```

<span data-ttu-id="826cc-147">For more information on deleting actors and their state, see the [actor lifecycle documentation](service-fabric-reliable-actors-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="826cc-147">For more information on deleting actors and their state, see the [actor lifecycle documentation](service-fabric-reliable-actors-lifecycle.md).</span></span>

### <a name="custom-actor-service"></a><span data-ttu-id="826cc-148">Custom actor service</span><span class="sxs-lookup"><span data-stu-id="826cc-148">Custom actor service</span></span>
<span data-ttu-id="826cc-149">By using the actor registration lambda, you can register your own custom actor service that derives from `ActorService` (C#) and `FabricActorService` (Java).</span><span class="sxs-lookup"><span data-stu-id="826cc-149">By using the actor registration lambda, you can register your own custom actor service that derives from `ActorService` (C#) and `FabricActorService` (Java).</span></span> <span data-ttu-id="826cc-150">In this custom actor service, you can implement your own service-level functionality by writing a service class that inherits `ActorService` (C#) or `FabricActorService` (Java).</span><span class="sxs-lookup"><span data-stu-id="826cc-150">In this custom actor service, you can implement your own service-level functionality by writing a service class that inherits `ActorService` (C#) or `FabricActorService` (Java).</span></span> <span data-ttu-id="826cc-151">A custom actor service inherits all the actor runtime functionality from `ActorService` (C#) or `FabricActorService` (Java) and can be used to implement your own service methods.</span><span class="sxs-lookup"><span data-stu-id="826cc-151">A custom actor service inherits all the actor runtime functionality from `ActorService` (C#) or `FabricActorService` (Java) and can be used to implement your own service methods.</span></span>

```csharp
class MyActorService : ActorService
{
    public MyActorService(StatefulServiceContext context, ActorTypeInformation typeInfo, Func<ActorBase> newActor)
        : base(context, typeInfo, newActor)
    { }
}
```
```Java
class MyActorService extends FabricActorService
{
    public MyActorService(StatefulServiceContext context, ActorTypeInformation typeInfo, BiFunction<FabricActorService, ActorId, ActorBase> newActor)
    {
         super(context, typeInfo, newActor);
    }
}
```

```csharp
static class Program
{
    private static void Main()
    {
        ActorRuntime.RegisterActorAsync<MyActor>(
            (context, actorType) => new MyActorService(context, actorType, () => new MyActor()))
            .GetAwaiter().GetResult();

        Thread.Sleep(Timeout.Infinite);
    }
}
```
```Java
public class Program
{
    public static void main(String[] args)
    {
        ActorRuntime.registerActorAsync(
                MyActor.class,
                (context, actorTypeInfo) -> new FabricActorService(context, actorTypeInfo),
                timeout);
        Thread.sleep(Long.MAX_VALUE);
    }
}
```

#### <a name="implementing-actor-backup-and-restore"></a><span data-ttu-id="826cc-152">Implementing actor backup and restore</span><span class="sxs-lookup"><span data-stu-id="826cc-152">Implementing actor backup and restore</span></span>
 <span data-ttu-id="826cc-153">In the following example, the custom actor service exposes a method to back up actor data by taking advantage of the remoting listener already present in `ActorService`:</span><span class="sxs-lookup"><span data-stu-id="826cc-153">In the following example, the custom actor service exposes a method to back up actor data by taking advantage of the remoting listener already present in `ActorService`:</span></span>

```csharp
public interface IMyActorService : IService
{
    Task BackupActorsAsync();
}

class MyActorService : ActorService, IMyActorService
{
    public MyActorService(StatefulServiceContext context, ActorTypeInformation typeInfo, Func<ActorBase> newActor)
        : base(context, typeInfo, newActor)
    { }

    public Task BackupActorsAsync()
    {
        return this.BackupAsync(new BackupDescription(PerformBackupAsync));
    }

    private async Task<bool> PerformBackupAsync(BackupInfo backupInfo, CancellationToken cancellationToken)
    {
        try
        {
           // store the contents of backupInfo.Directory
           return true;
        }
        finally
        {
           Directory.Delete(backupInfo.Directory, recursive: true);
        }
    }
}
```
```Java
public interface MyActorService extends Service
{
    CompletableFuture<?> backupActorsAsync();
}

class MyActorServiceImpl extends ActorService implements MyActorService
{
    public MyActorService(StatefulServiceContext context, ActorTypeInformation typeInfo, Func<FabricActorService, ActorId, ActorBase> newActor)
    {
       super(context, typeInfo, newActor);
    }

    public CompletableFuture backupActorsAsync()
    {
        return this.backupAsync(new BackupDescription((backupInfo, cancellationToken) -> performBackupAsync(backupInfo, cancellationToken)));
    }

    private CompletableFuture<Boolean> performBackupAsync(BackupInfo backupInfo, CancellationToken cancellationToken)
    {
        try
        {
           // store the contents of backupInfo.Directory
           return true;
        }
        finally
        {
           deleteDirectory(backupInfo.Directory)
        }
    }

    void deleteDirectory(File file) {
        File[] contents = file.listFiles();
        if (contents != null) {
            for (File f : contents) {
               deleteDirectory(f);
             }
        }
        file.delete();
    }
}
```


<span data-ttu-id="826cc-154">In this example, `IMyActorService` is a remoting contract that implements `IService` (C#) and `Service` (Java), and is then implemented by `MyActorService`.</span><span class="sxs-lookup"><span data-stu-id="826cc-154">In this example, `IMyActorService` is a remoting contract that implements `IService` (C#) and `Service` (Java), and is then implemented by `MyActorService`.</span></span> <span data-ttu-id="826cc-155">By adding this remoting contract, methods on `IMyActorService` are now also available to a client by creating a remoting proxy via `ActorServiceProxy`:</span><span class="sxs-lookup"><span data-stu-id="826cc-155">By adding this remoting contract, methods on `IMyActorService` are now also available to a client by creating a remoting proxy via `ActorServiceProxy`:</span></span>

```csharp
IMyActorService myActorServiceProxy = ActorServiceProxy.Create<IMyActorService>(
    new Uri("fabric:/MyApp/MyService"), ActorId.CreateRandom());

await myActorServiceProxy.BackupActorsAsync();
```
```Java
MyActorService myActorServiceProxy = ActorServiceProxy.create(MyActorService.class,
    new URI("fabric:/MyApp/MyService"), actorId);

myActorServiceProxy.backupActorsAsync();
```

## <a name="application-model"></a><span data-ttu-id="826cc-156">Application model</span><span class="sxs-lookup"><span data-stu-id="826cc-156">Application model</span></span>
<span data-ttu-id="826cc-157">Actor services are Reliable Services, so the application model is the same.</span><span class="sxs-lookup"><span data-stu-id="826cc-157">Actor services are Reliable Services, so the application model is the same.</span></span> <span data-ttu-id="826cc-158">However, the actor framework build tools generate some of the application model files for you.</span><span class="sxs-lookup"><span data-stu-id="826cc-158">However, the actor framework build tools generate some of the application model files for you.</span></span>

### <a name="service-manifest"></a><span data-ttu-id="826cc-159">Service manifest</span><span class="sxs-lookup"><span data-stu-id="826cc-159">Service manifest</span></span>
<span data-ttu-id="826cc-160">The actor framework build tools automatically generate the contents of your actor service's ServiceManifest.xml file.</span><span class="sxs-lookup"><span data-stu-id="826cc-160">The actor framework build tools automatically generate the contents of your actor service's ServiceManifest.xml file.</span></span> <span data-ttu-id="826cc-161">This file includes:</span><span class="sxs-lookup"><span data-stu-id="826cc-161">This file includes:</span></span>

* <span data-ttu-id="826cc-162">Actor service type.</span><span class="sxs-lookup"><span data-stu-id="826cc-162">Actor service type.</span></span> <span data-ttu-id="826cc-163">The type name is generated based on your actor's project name.</span><span class="sxs-lookup"><span data-stu-id="826cc-163">The type name is generated based on your actor's project name.</span></span> <span data-ttu-id="826cc-164">Based on the persistence attribute on your actor, the HasPersistedState flag is also set accordingly.</span><span class="sxs-lookup"><span data-stu-id="826cc-164">Based on the persistence attribute on your actor, the HasPersistedState flag is also set accordingly.</span></span>
* <span data-ttu-id="826cc-165">Code package.</span><span class="sxs-lookup"><span data-stu-id="826cc-165">Code package.</span></span>
* <span data-ttu-id="826cc-166">Config package.</span><span class="sxs-lookup"><span data-stu-id="826cc-166">Config package.</span></span>
* <span data-ttu-id="826cc-167">Resources and endpoints.</span><span class="sxs-lookup"><span data-stu-id="826cc-167">Resources and endpoints.</span></span>

### <a name="application-manifest"></a><span data-ttu-id="826cc-168">Application manifest</span><span class="sxs-lookup"><span data-stu-id="826cc-168">Application manifest</span></span>
<span data-ttu-id="826cc-169">The actor framework build tools automatically create a default service definition for your actor service.</span><span class="sxs-lookup"><span data-stu-id="826cc-169">The actor framework build tools automatically create a default service definition for your actor service.</span></span> <span data-ttu-id="826cc-170">The build tools populate the default service properties:</span><span class="sxs-lookup"><span data-stu-id="826cc-170">The build tools populate the default service properties:</span></span>

* <span data-ttu-id="826cc-171">Replica set count is determined by the persistence attribute on your actor.</span><span class="sxs-lookup"><span data-stu-id="826cc-171">Replica set count is determined by the persistence attribute on your actor.</span></span> <span data-ttu-id="826cc-172">Each time the persistence attribute on your actor is changed, the replica set count in the default service definition is reset accordingly.</span><span class="sxs-lookup"><span data-stu-id="826cc-172">Each time the persistence attribute on your actor is changed, the replica set count in the default service definition is reset accordingly.</span></span>
* <span data-ttu-id="826cc-173">Partition scheme and range are set to Uniform Int64 with the full Int64 key range.</span><span class="sxs-lookup"><span data-stu-id="826cc-173">Partition scheme and range are set to Uniform Int64 with the full Int64 key range.</span></span>

## <a name="service-fabric-partition-concepts-for-actors"></a><span data-ttu-id="826cc-174">Service Fabric partition concepts for actors</span><span class="sxs-lookup"><span data-stu-id="826cc-174">Service Fabric partition concepts for actors</span></span>
<span data-ttu-id="826cc-175">Actor services are partitioned stateful services.</span><span class="sxs-lookup"><span data-stu-id="826cc-175">Actor services are partitioned stateful services.</span></span> <span data-ttu-id="826cc-176">Each partition of an actor service contains a set of actors.</span><span class="sxs-lookup"><span data-stu-id="826cc-176">Each partition of an actor service contains a set of actors.</span></span> <span data-ttu-id="826cc-177">Service partitions are automatically distributed over multiple nodes in Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="826cc-177">Service partitions are automatically distributed over multiple nodes in Service Fabric.</span></span> <span data-ttu-id="826cc-178">Actor instances are distributed as a result.</span><span class="sxs-lookup"><span data-stu-id="826cc-178">Actor instances are distributed as a result.</span></span>

![Actor partitioning and distribution][5]

<span data-ttu-id="826cc-180">Reliable Services can be created with different partition schemes and partition key ranges.</span><span class="sxs-lookup"><span data-stu-id="826cc-180">Reliable Services can be created with different partition schemes and partition key ranges.</span></span> <span data-ttu-id="826cc-181">The actor service uses the Int64 partitioning scheme with the full Int64 key range to map actors to partitions.</span><span class="sxs-lookup"><span data-stu-id="826cc-181">The actor service uses the Int64 partitioning scheme with the full Int64 key range to map actors to partitions.</span></span>

### <a name="actor-id"></a><span data-ttu-id="826cc-182">Actor ID</span><span class="sxs-lookup"><span data-stu-id="826cc-182">Actor ID</span></span>
<span data-ttu-id="826cc-183">Each actor that's created in the service has a unique ID associated with it, represented by the `ActorId` class.</span><span class="sxs-lookup"><span data-stu-id="826cc-183">Each actor that's created in the service has a unique ID associated with it, represented by the `ActorId` class.</span></span> <span data-ttu-id="826cc-184">`ActorId` is an opaque ID value that can be used for uniform distribution of actors across the service partitions by generating random IDs:</span><span class="sxs-lookup"><span data-stu-id="826cc-184">`ActorId` is an opaque ID value that can be used for uniform distribution of actors across the service partitions by generating random IDs:</span></span>

```csharp
ActorProxy.Create<IMyActor>(ActorId.CreateRandom());
```
```Java
ActorProxyBase.create<MyActor>(MyActor.class, ActorId.newId());
```


<span data-ttu-id="826cc-185">Every `ActorId` is hashed to an Int64.</span><span class="sxs-lookup"><span data-stu-id="826cc-185">Every `ActorId` is hashed to an Int64.</span></span> <span data-ttu-id="826cc-186">This is why the actor service must use an Int64 partitioning scheme with the full Int64 key range.</span><span class="sxs-lookup"><span data-stu-id="826cc-186">This is why the actor service must use an Int64 partitioning scheme with the full Int64 key range.</span></span> <span data-ttu-id="826cc-187">However, custom ID values can be used for an `ActorID`, including GUIDs/UUIDs, strings, and Int64s.</span><span class="sxs-lookup"><span data-stu-id="826cc-187">However, custom ID values can be used for an `ActorID`, including GUIDs/UUIDs, strings, and Int64s.</span></span>

```csharp
ActorProxy.Create<IMyActor>(new ActorId(Guid.NewGuid()));
ActorProxy.Create<IMyActor>(new ActorId("myActorId"));
ActorProxy.Create<IMyActor>(new ActorId(1234));
```
```Java
ActorProxyBase.create(MyActor.class, new ActorId(UUID.randomUUID()));
ActorProxyBase.create(MyActor.class, new ActorId("myActorId"));
ActorProxyBase.create(MyActor.class, new ActorId(1234));
```

<span data-ttu-id="826cc-188">When you're using GUIDs/UUIDs and strings, the values are hashed to an Int64.</span><span class="sxs-lookup"><span data-stu-id="826cc-188">When you're using GUIDs/UUIDs and strings, the values are hashed to an Int64.</span></span> <span data-ttu-id="826cc-189">However, when you're explicitly providing an Int64 to an `ActorId`, the Int64 will map directly to a partition without further hashing.</span><span class="sxs-lookup"><span data-stu-id="826cc-189">However, when you're explicitly providing an Int64 to an `ActorId`, the Int64 will map directly to a partition without further hashing.</span></span> <span data-ttu-id="826cc-190">You can use this technique to control which partition the actors are placed in.</span><span class="sxs-lookup"><span data-stu-id="826cc-190">You can use this technique to control which partition the actors are placed in.</span></span>

## <a name="next-steps"></a><span data-ttu-id="826cc-191">Next steps</span><span class="sxs-lookup"><span data-stu-id="826cc-191">Next steps</span></span>
* [<span data-ttu-id="826cc-192">Actor state management</span><span class="sxs-lookup"><span data-stu-id="826cc-192">Actor state management</span></span>](service-fabric-reliable-actors-state-management.md)
* [<span data-ttu-id="826cc-193">Actor lifecycle and garbage collection</span><span class="sxs-lookup"><span data-stu-id="826cc-193">Actor lifecycle and garbage collection</span></span>](service-fabric-reliable-actors-lifecycle.md)
* [<span data-ttu-id="826cc-194">Actors API reference documentation</span><span class="sxs-lookup"><span data-stu-id="826cc-194">Actors API reference documentation</span></span>](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [<span data-ttu-id="826cc-195">.NET sample code</span><span class="sxs-lookup"><span data-stu-id="826cc-195">.NET sample code</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="826cc-196">Java sample code</span><span class="sxs-lookup"><span data-stu-id="826cc-196">Java sample code</span></span>](http://github.com/Azure-Samples/service-fabric-java-getting-started)

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-reliable-actors-platform/actor-service.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-reliable-actors-platform/app-deployment-scripts.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-reliable-actors-platform/actor-partition-info.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-reliable-actors-platform/actor-replica-role.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-reliable-actors-introduction/distribution.png





