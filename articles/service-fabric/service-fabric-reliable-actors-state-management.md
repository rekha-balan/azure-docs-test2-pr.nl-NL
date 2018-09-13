---
title: Reliable Actors state management | Microsoft Docs
description: Describes how Reliable Actors state is managed, persisted, and replicated for high availability.
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: ''
ms.assetid: 37cf466a-5293-44c0-a4e0-037e5d292214
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/10/2017
ms.author: vturecek
ms.openlocfilehash: b6b2bc36f6fcdfa7a6f478608d6d698a56039a10
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551118"
---
# <a name="reliable-actors-state-management"></a><span data-ttu-id="29353-103">Reliable Actors state management</span><span class="sxs-lookup"><span data-stu-id="29353-103">Reliable Actors state management</span></span>
<span data-ttu-id="29353-104">Reliable Actors are single-threaded objects that can encapsulate both logic and state.</span><span class="sxs-lookup"><span data-stu-id="29353-104">Reliable Actors are single-threaded objects that can encapsulate both logic and state.</span></span> <span data-ttu-id="29353-105">Because actors run on Reliable Services, they can maintain state reliably by using the same persistence and replication mechanisms that Reliable Services uses.</span><span class="sxs-lookup"><span data-stu-id="29353-105">Because actors run on Reliable Services, they can maintain state reliably by using the same persistence and replication mechanisms that Reliable Services uses.</span></span> <span data-ttu-id="29353-106">This way, actors don't lose their state after failures, upon reactivation after garbage collection, or when they are moved around between nodes in a cluster due to resource balancing or upgrades.</span><span class="sxs-lookup"><span data-stu-id="29353-106">This way, actors don't lose their state after failures, upon reactivation after garbage collection, or when they are moved around between nodes in a cluster due to resource balancing or upgrades.</span></span>

## <a name="state-persistence-and-replication"></a><span data-ttu-id="29353-107">State persistence and replication</span><span class="sxs-lookup"><span data-stu-id="29353-107">State persistence and replication</span></span>
<span data-ttu-id="29353-108">All Reliable Actors are considered *stateful* because each actor instance maps to a unique ID.</span><span class="sxs-lookup"><span data-stu-id="29353-108">All Reliable Actors are considered *stateful* because each actor instance maps to a unique ID.</span></span> <span data-ttu-id="29353-109">This means that repeated calls to the same actor ID are routed to the same actor instance.</span><span class="sxs-lookup"><span data-stu-id="29353-109">This means that repeated calls to the same actor ID are routed to the same actor instance.</span></span> <span data-ttu-id="29353-110">In a stateless system, by contrast, client calls are not guaranteed to be routed to the same server every time.</span><span class="sxs-lookup"><span data-stu-id="29353-110">In a stateless system, by contrast, client calls are not guaranteed to be routed to the same server every time.</span></span> <span data-ttu-id="29353-111">For this reason, actor services are always stateful services.</span><span class="sxs-lookup"><span data-stu-id="29353-111">For this reason, actor services are always stateful services.</span></span>

<span data-ttu-id="29353-112">Even though actors are considered stateful, that does not mean they must store state reliably.</span><span class="sxs-lookup"><span data-stu-id="29353-112">Even though actors are considered stateful, that does not mean they must store state reliably.</span></span> <span data-ttu-id="29353-113">Actors can choose the level of state persistence and replication based on their data storage requirements:</span><span class="sxs-lookup"><span data-stu-id="29353-113">Actors can choose the level of state persistence and replication based on their data storage requirements:</span></span>

* <span data-ttu-id="29353-114">**Persisted state**: State is persisted to disk and is replicated to 3 or more replicas.</span><span class="sxs-lookup"><span data-stu-id="29353-114">**Persisted state**: State is persisted to disk and is replicated to 3 or more replicas.</span></span> <span data-ttu-id="29353-115">This is the most durable state storage option, where state can persist through complete cluster outage.</span><span class="sxs-lookup"><span data-stu-id="29353-115">This is the most durable state storage option, where state can persist through complete cluster outage.</span></span>
* <span data-ttu-id="29353-116">**Volatile state**: State is replicated to 3 or more replicas and only kept in memory.</span><span class="sxs-lookup"><span data-stu-id="29353-116">**Volatile state**: State is replicated to 3 or more replicas and only kept in memory.</span></span> <span data-ttu-id="29353-117">This provides resilience against node failure and actor failure, and during upgrades and resource balancing.</span><span class="sxs-lookup"><span data-stu-id="29353-117">This provides resilience against node failure and actor failure, and during upgrades and resource balancing.</span></span> <span data-ttu-id="29353-118">However, state is not persisted to disk.</span><span class="sxs-lookup"><span data-stu-id="29353-118">However, state is not persisted to disk.</span></span> <span data-ttu-id="29353-119">So if all replicas are lost at once, the state is lost as well.</span><span class="sxs-lookup"><span data-stu-id="29353-119">So if all replicas are lost at once, the state is lost as well.</span></span>
* <span data-ttu-id="29353-120">**No persisted state**: State is not replicated or written to disk.</span><span class="sxs-lookup"><span data-stu-id="29353-120">**No persisted state**: State is not replicated or written to disk.</span></span> <span data-ttu-id="29353-121">This level is for actors that simply don't need to maintain state reliably.</span><span class="sxs-lookup"><span data-stu-id="29353-121">This level is for actors that simply don't need to maintain state reliably.</span></span>

<span data-ttu-id="29353-122">Each level of persistence is simply a different *state provider* and *replication* configuration of your service.</span><span class="sxs-lookup"><span data-stu-id="29353-122">Each level of persistence is simply a different *state provider* and *replication* configuration of your service.</span></span> <span data-ttu-id="29353-123">Whether or not state is written to disk depends on the state provider--the component in a reliable service that stores state.</span><span class="sxs-lookup"><span data-stu-id="29353-123">Whether or not state is written to disk depends on the state provider--the component in a reliable service that stores state.</span></span> <span data-ttu-id="29353-124">Replication depends on how many replicas a service is deployed with.</span><span class="sxs-lookup"><span data-stu-id="29353-124">Replication depends on how many replicas a service is deployed with.</span></span> <span data-ttu-id="29353-125">As with Reliable Services, both the state provider and replica count can easily be set manually.</span><span class="sxs-lookup"><span data-stu-id="29353-125">As with Reliable Services, both the state provider and replica count can easily be set manually.</span></span> <span data-ttu-id="29353-126">The actor framework provides an attribute that, when used on an actor, automatically selects a default state provider and automatically generates settings for replica count to achieve one of these three persistence settings.</span><span class="sxs-lookup"><span data-stu-id="29353-126">The actor framework provides an attribute that, when used on an actor, automatically selects a default state provider and automatically generates settings for replica count to achieve one of these three persistence settings.</span></span>

### <a name="persisted-state"></a><span data-ttu-id="29353-127">Persisted state</span><span class="sxs-lookup"><span data-stu-id="29353-127">Persisted state</span></span>
```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl  extends FabricActor implements MyActor
{
}
```  
<span data-ttu-id="29353-128">This setting uses a state provider that stores data on disk and automatically sets the service replica count to 3.</span><span class="sxs-lookup"><span data-stu-id="29353-128">This setting uses a state provider that stores data on disk and automatically sets the service replica count to 3.</span></span>

### <a name="volatile-state"></a><span data-ttu-id="29353-129">Volatile state</span><span class="sxs-lookup"><span data-stu-id="29353-129">Volatile state</span></span>
```csharp
[StatePersistence(StatePersistence.Volatile)]
class MyActor : Actor, IMyActor
{
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Volatile)
class MyActorImpl extends FabricActor implements MyActor
{
}
```
<span data-ttu-id="29353-130">This setting uses an in-memory-only state provider and sets the replica count to 3.</span><span class="sxs-lookup"><span data-stu-id="29353-130">This setting uses an in-memory-only state provider and sets the replica count to 3.</span></span>

### <a name="no-persisted-state"></a><span data-ttu-id="29353-131">No persisted state</span><span class="sxs-lookup"><span data-stu-id="29353-131">No persisted state</span></span>
```csharp
[StatePersistence(StatePersistence.None)]
class MyActor : Actor, IMyActor
{
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.None)
class MyActorImpl extends FabricActor implements MyActor
{
}
```
<span data-ttu-id="29353-132">This setting uses an in-memory-only state provider and sets the replica count to 1.</span><span class="sxs-lookup"><span data-stu-id="29353-132">This setting uses an in-memory-only state provider and sets the replica count to 1.</span></span>

### <a name="defaults-and-generated-settings"></a><span data-ttu-id="29353-133">Defaults and generated settings</span><span class="sxs-lookup"><span data-stu-id="29353-133">Defaults and generated settings</span></span>
<span data-ttu-id="29353-134">When you're using the `StatePersistence` attribute, a state provider is automatically selected for you at runtime when the actor service starts.</span><span class="sxs-lookup"><span data-stu-id="29353-134">When you're using the `StatePersistence` attribute, a state provider is automatically selected for you at runtime when the actor service starts.</span></span> <span data-ttu-id="29353-135">The replica count, however, is set at compile time by the Visual Studio actor build tools.</span><span class="sxs-lookup"><span data-stu-id="29353-135">The replica count, however, is set at compile time by the Visual Studio actor build tools.</span></span> <span data-ttu-id="29353-136">The build tools automatically generate a *default service* for the actor service in ApplicationManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="29353-136">The build tools automatically generate a *default service* for the actor service in ApplicationManifest.xml.</span></span> <span data-ttu-id="29353-137">Parameters are created for **min replica set size** and **target replica set size**.</span><span class="sxs-lookup"><span data-stu-id="29353-137">Parameters are created for **min replica set size** and **target replica set size**.</span></span> 

<span data-ttu-id="29353-138">You can change these parameters manually.</span><span class="sxs-lookup"><span data-stu-id="29353-138">You can change these parameters manually.</span></span> <span data-ttu-id="29353-139">But each time the `StatePersistence` attribute is changed, the parameters are set to the default replica set size values for the selected `StatePersistence` attribute, overriding any previous values.</span><span class="sxs-lookup"><span data-stu-id="29353-139">But each time the `StatePersistence` attribute is changed, the parameters are set to the default replica set size values for the selected `StatePersistence` attribute, overriding any previous values.</span></span> <span data-ttu-id="29353-140">In other words, the values that you set in ServiceManifest.xml are *only* overridden at build time when you change the `StatePersistence` attribute value.</span><span class="sxs-lookup"><span data-stu-id="29353-140">In other words, the values that you set in ServiceManifest.xml are *only* overridden at build time when you change the `StatePersistence` attribute value.</span></span>

```xml
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="Application12Type" ApplicationTypeVersion="1.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <Parameters>
      <Parameter Name="MyActorService_PartitionCount" DefaultValue="10" />
      <Parameter Name="MyActorService_MinReplicaSetSize" DefaultValue="3" />
      <Parameter Name="MyActorService_TargetReplicaSetSize" DefaultValue="3" />
   </Parameters>
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="MyActorPkg" ServiceManifestVersion="1.0.0" />
   </ServiceManifestImport>
   <DefaultServices>
      <Service Name="MyActorService" GeneratedIdRef="77d965dc-85fb-488c-bd06-c6c1fe29d593|Persisted">
         <StatefulService ServiceTypeName="MyActorServiceType" TargetReplicaSetSize="[MyActorService_TargetReplicaSetSize]" MinReplicaSetSize="[MyActorService_MinReplicaSetSize]">
            <UniformInt64Partition PartitionCount="[MyActorService_PartitionCount]" LowKey="-9223372036854775808" HighKey="9223372036854775807" />
         </StatefulService>
      </Service>
   </DefaultServices>
</ApplicationManifest>
```

## <a name="state-manager"></a><span data-ttu-id="29353-141">State manager</span><span class="sxs-lookup"><span data-stu-id="29353-141">State manager</span></span>
<span data-ttu-id="29353-142">Every actor instance has its own state manager: a dictionary-like data structure that reliably stores key/value pairs.</span><span class="sxs-lookup"><span data-stu-id="29353-142">Every actor instance has its own state manager: a dictionary-like data structure that reliably stores key/value pairs.</span></span> <span data-ttu-id="29353-143">The state manager is a wrapper around a state provider.</span><span class="sxs-lookup"><span data-stu-id="29353-143">The state manager is a wrapper around a state provider.</span></span> <span data-ttu-id="29353-144">You can use it to store data regardless of which persistence setting is used.</span><span class="sxs-lookup"><span data-stu-id="29353-144">You can use it to store data regardless of which persistence setting is used.</span></span> <span data-ttu-id="29353-145">It does not provide any guarantees that a running actor service can be changed from a volatile (in-memory-only) state setting to a persisted state setting through a rolling upgrade while preserving data.</span><span class="sxs-lookup"><span data-stu-id="29353-145">It does not provide any guarantees that a running actor service can be changed from a volatile (in-memory-only) state setting to a persisted state setting through a rolling upgrade while preserving data.</span></span> <span data-ttu-id="29353-146">However, it is possible to change replica count for a running service.</span><span class="sxs-lookup"><span data-stu-id="29353-146">However, it is possible to change replica count for a running service.</span></span>

<span data-ttu-id="29353-147">State manager keys must be strings.</span><span class="sxs-lookup"><span data-stu-id="29353-147">State manager keys must be strings.</span></span> <span data-ttu-id="29353-148">Values are generic and can be any type, including custom types.</span><span class="sxs-lookup"><span data-stu-id="29353-148">Values are generic and can be any type, including custom types.</span></span> <span data-ttu-id="29353-149">Values stored in the state manager must be data contract serializable because they might be transmitted over the network to other nodes during replication and might be written to disk, depending on an actor's state persistence setting.</span><span class="sxs-lookup"><span data-stu-id="29353-149">Values stored in the state manager must be data contract serializable because they might be transmitted over the network to other nodes during replication and might be written to disk, depending on an actor's state persistence setting.</span></span>

<span data-ttu-id="29353-150">The state manager exposes common dictionary methods for managing state, similar to those found in Reliable Dictionary.</span><span class="sxs-lookup"><span data-stu-id="29353-150">The state manager exposes common dictionary methods for managing state, similar to those found in Reliable Dictionary.</span></span>

### <a name="accessing-state"></a><span data-ttu-id="29353-151">Accessing state</span><span class="sxs-lookup"><span data-stu-id="29353-151">Accessing state</span></span>
<span data-ttu-id="29353-152">State can be accessed through the state manager by key.</span><span class="sxs-lookup"><span data-stu-id="29353-152">State can be accessed through the state manager by key.</span></span> <span data-ttu-id="29353-153">State manager methods are all asynchronous because they might require disk I/O when actors have persisted state.</span><span class="sxs-lookup"><span data-stu-id="29353-153">State manager methods are all asynchronous because they might require disk I/O when actors have persisted state.</span></span> <span data-ttu-id="29353-154">Upon first access, state objects are cached in memory.</span><span class="sxs-lookup"><span data-stu-id="29353-154">Upon first access, state objects are cached in memory.</span></span> <span data-ttu-id="29353-155">Repeat access operations access objects directly from memory and return synchronously without incurring disk I/O or asynchronous context-switching overhead.</span><span class="sxs-lookup"><span data-stu-id="29353-155">Repeat access operations access objects directly from memory and return synchronously without incurring disk I/O or asynchronous context-switching overhead.</span></span> <span data-ttu-id="29353-156">A state object is removed from the cache in the following cases:</span><span class="sxs-lookup"><span data-stu-id="29353-156">A state object is removed from the cache in the following cases:</span></span>

* <span data-ttu-id="29353-157">An actor method throws an unhandled exception after it retrieves an object from the state manager.</span><span class="sxs-lookup"><span data-stu-id="29353-157">An actor method throws an unhandled exception after it retrieves an object from the state manager.</span></span>
* <span data-ttu-id="29353-158">An actor is reactivated, either after being deactivated or after failure.</span><span class="sxs-lookup"><span data-stu-id="29353-158">An actor is reactivated, either after being deactivated or after failure.</span></span>
* <span data-ttu-id="29353-159">The state provider pages state to disk.</span><span class="sxs-lookup"><span data-stu-id="29353-159">The state provider pages state to disk.</span></span> <span data-ttu-id="29353-160">This behavior depends on the state provider implementation.</span><span class="sxs-lookup"><span data-stu-id="29353-160">This behavior depends on the state provider implementation.</span></span> <span data-ttu-id="29353-161">The default state provider for the `Persisted` setting has this behavior.</span><span class="sxs-lookup"><span data-stu-id="29353-161">The default state provider for the `Persisted` setting has this behavior.</span></span>

<span data-ttu-id="29353-162">You can retrieve state by using a standard *Get* operation that throws `KeyNotFoundException`(C#) or `NoSuchElementException`(Java) if an entry does not exist for the key:</span><span class="sxs-lookup"><span data-stu-id="29353-162">You can retrieve state by using a standard *Get* operation that throws `KeyNotFoundException`(C#) or `NoSuchElementException`(Java) if an entry does not exist for the key:</span></span>

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task<int> GetCountAsync()
    {
        return this.StateManager.GetStateAsync<int>("MyState");
    }
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture<Integer> getCountAsync()
    {
        return this.stateManager().getStateAsync("MyState");
    }
}
```

<span data-ttu-id="29353-163">You can also retrieve state by using a *TryGet* method that does not throw if an entry does not exist for a key:</span><span class="sxs-lookup"><span data-stu-id="29353-163">You can also retrieve state by using a *TryGet* method that does not throw if an entry does not exist for a key:</span></span>

```csharp
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public async Task<int> GetCountAsync()
    {
        ConditionalValue<int> result = await this.StateManager.TryGetStateAsync<int>("MyState");
        if (result.HasValue)
        {
            return result.Value;
        }

        return 0;
    }
}
```
```Java
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture<Integer> getCountAsync()
    {
        return this.stateManager().<Integer>tryGetStateAsync("MyState").thenApply(result -> {
            if (result.hasValue()) {
                return result.getValue();
            } else {
                return 0;
            });
    }
}
```

### <a name="saving-state"></a><span data-ttu-id="29353-164">Saving state</span><span class="sxs-lookup"><span data-stu-id="29353-164">Saving state</span></span>
<span data-ttu-id="29353-165">The state manager retrieval methods return a reference to an object in local memory.</span><span class="sxs-lookup"><span data-stu-id="29353-165">The state manager retrieval methods return a reference to an object in local memory.</span></span> <span data-ttu-id="29353-166">Modifying this object in local memory alone does not cause it to be saved durably.</span><span class="sxs-lookup"><span data-stu-id="29353-166">Modifying this object in local memory alone does not cause it to be saved durably.</span></span> <span data-ttu-id="29353-167">When an object is retrieved from the state manager and modified, it must be reinserted into the state manager to be saved durably.</span><span class="sxs-lookup"><span data-stu-id="29353-167">When an object is retrieved from the state manager and modified, it must be reinserted into the state manager to be saved durably.</span></span>

<span data-ttu-id="29353-168">You can insert state by using an unconditional *Set*, which is the equivalent of the `dictionary["key"] = value` syntax:</span><span class="sxs-lookup"><span data-stu-id="29353-168">You can insert state by using an unconditional *Set*, which is the equivalent of the `dictionary["key"] = value` syntax:</span></span>

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task SetCountAsync(int value)
    {
        return this.StateManager.SetStateAsync<int>("MyState", value);
    }
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture setCountAsync(int value)
    {
        return this.stateManager().setStateAsync("MyState", value);
    }
}
```

<span data-ttu-id="29353-169">You can add state by using an *Add* method.</span><span class="sxs-lookup"><span data-stu-id="29353-169">You can add state by using an *Add* method.</span></span> <span data-ttu-id="29353-170">This method throws `InvalidOperationException`(C#) or `IllegalStateException`(Java) when it tries to add a key that already exists.</span><span class="sxs-lookup"><span data-stu-id="29353-170">This method throws `InvalidOperationException`(C#) or `IllegalStateException`(Java) when it tries to add a key that already exists.</span></span>

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task AddCountAsync(int value)
    {
        return this.StateManager.AddStateAsync<int>("MyState", value);
    }
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture addCountAsync(int value)
    {
        return this.stateManager().addOrUpdateStateAsync("MyState", value, (key, old_value) -> old_value + value);
    }
}
```

<span data-ttu-id="29353-171">You can also add state by using a *TryAdd* method.</span><span class="sxs-lookup"><span data-stu-id="29353-171">You can also add state by using a *TryAdd* method.</span></span> <span data-ttu-id="29353-172">This method does not throw when it tries to add a key that already exists.</span><span class="sxs-lookup"><span data-stu-id="29353-172">This method does not throw when it tries to add a key that already exists.</span></span>

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public async Task AddCountAsync(int value)
    {
        bool result = await this.StateManager.TryAddStateAsync<int>("MyState", value);

        if (result)
        {
            // Added successfully!
        }
    }
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture addCountAsync(int value)
    {
        return this.stateManager().tryAddStateAsync("MyState", value).thenApply((result)->{
            if(result)
            {
                // Added successfully!
            }
        });
    }
}
```

<span data-ttu-id="29353-173">At the end of an actor method, the state manager automatically saves any values that have been added or modified by an insert or update operation.</span><span class="sxs-lookup"><span data-stu-id="29353-173">At the end of an actor method, the state manager automatically saves any values that have been added or modified by an insert or update operation.</span></span> <span data-ttu-id="29353-174">A "save" can include persisting to disk and replication, depending on the settings used.</span><span class="sxs-lookup"><span data-stu-id="29353-174">A "save" can include persisting to disk and replication, depending on the settings used.</span></span> <span data-ttu-id="29353-175">Values that have not been modified are not persisted or replicated.</span><span class="sxs-lookup"><span data-stu-id="29353-175">Values that have not been modified are not persisted or replicated.</span></span> <span data-ttu-id="29353-176">If no values have been modified, the save operation does nothing.</span><span class="sxs-lookup"><span data-stu-id="29353-176">If no values have been modified, the save operation does nothing.</span></span> <span data-ttu-id="29353-177">If saving fails, the modified state is discarded and the original state is reloaded.</span><span class="sxs-lookup"><span data-stu-id="29353-177">If saving fails, the modified state is discarded and the original state is reloaded.</span></span>

<span data-ttu-id="29353-178">You can also save state manually by calling the `SaveStateAsync` method on the actor base:</span><span class="sxs-lookup"><span data-stu-id="29353-178">You can also save state manually by calling the `SaveStateAsync` method on the actor base:</span></span>

```csharp
async Task IMyActor.SetCountAsync(int count)
{
    await this.StateManager.AddOrUpdateStateAsync("count", count, (key, value) => count > value ? count : value);

    await this.SaveStateAsync();
}
```
```Java
interface MyActor {
    CompletableFuture setCountAsync(int count)
    {
        this.stateManager().addOrUpdateStateAsync("count", count, (key, value) -> count > value ? count : value).thenApply();

        this.stateManager().saveStateAsync().thenApply();
    }
}
```

### <a name="removing-state"></a><span data-ttu-id="29353-179">Removing state</span><span class="sxs-lookup"><span data-stu-id="29353-179">Removing state</span></span>
<span data-ttu-id="29353-180">You can remove state permanently from an actor's state manager by calling the *Remove* method.</span><span class="sxs-lookup"><span data-stu-id="29353-180">You can remove state permanently from an actor's state manager by calling the *Remove* method.</span></span> <span data-ttu-id="29353-181">This method throws `KeyNotFoundException`(C#) or `NoSuchElementException`(Java) when it tries to remove a key that doesn't exist.</span><span class="sxs-lookup"><span data-stu-id="29353-181">This method throws `KeyNotFoundException`(C#) or `NoSuchElementException`(Java) when it tries to remove a key that doesn't exist.</span></span>

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task RemoveCountAsync()
    {
        return this.StateManager.RemoveStateAsync("MyState");
    }
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture removeCountAsync()
    {
        return this.stateManager().removeStateAsync("MyState");
    }
}
```

<span data-ttu-id="29353-182">You can also remove state permanently by using the *TryRemove* method.</span><span class="sxs-lookup"><span data-stu-id="29353-182">You can also remove state permanently by using the *TryRemove* method.</span></span> <span data-ttu-id="29353-183">This method does not throw when it tries to remove a key that does not exist.</span><span class="sxs-lookup"><span data-stu-id="29353-183">This method does not throw when it tries to remove a key that does not exist.</span></span>

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public async Task RemoveCountAsync()
    {
        bool result = await this.StateManager.TryRemoveStateAsync("MyState");

        if (result)
        {
            // State removed!
        }
    }
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture removeCountAsync()
    {
        return this.stateManager().tryRemoveStateAsync("MyState").thenApply((result)->{
            if(result)
            {
                // State removed!
            }
        });
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="29353-184">Next steps</span><span class="sxs-lookup"><span data-stu-id="29353-184">Next steps</span></span>
* [<span data-ttu-id="29353-185">Actor type serialization</span><span class="sxs-lookup"><span data-stu-id="29353-185">Actor type serialization</span></span>](service-fabric-reliable-actors-notes-on-actor-type-serialization.md)
* [<span data-ttu-id="29353-186">Actor polymorphism and object-oriented design patterns</span><span class="sxs-lookup"><span data-stu-id="29353-186">Actor polymorphism and object-oriented design patterns</span></span>](service-fabric-reliable-actors-polymorphism.md)
* [<span data-ttu-id="29353-187">Actor diagnostics and performance monitoring</span><span class="sxs-lookup"><span data-stu-id="29353-187">Actor diagnostics and performance monitoring</span></span>](service-fabric-reliable-actors-diagnostics.md)
* [<span data-ttu-id="29353-188">Actor API reference documentation</span><span class="sxs-lookup"><span data-stu-id="29353-188">Actor API reference documentation</span></span>](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [<span data-ttu-id="29353-189">C# sample code</span><span class="sxs-lookup"><span data-stu-id="29353-189">C# sample code</span></span>](https://github.com/Azure/servicefabric-samples)
* [<span data-ttu-id="29353-190">Java sample code</span><span class="sxs-lookup"><span data-stu-id="29353-190">Java sample code</span></span>](http://github.com/Azure-Samples/service-fabric-java-getting-started)
