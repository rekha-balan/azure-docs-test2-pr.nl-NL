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
ms.topic: conceptual
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/02/2017
ms.author: vturecek
ms.openlocfilehash: acbbb8f37a47185a5bac582723a08d6161a979bd
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44831129"
---
# <a name="reliable-actors-state-management"></a><span data-ttu-id="49aa3-103">Reliable Actors state management</span><span class="sxs-lookup"><span data-stu-id="49aa3-103">Reliable Actors state management</span></span>
<span data-ttu-id="49aa3-104">Reliable Actors are single-threaded objects that can encapsulate both logic and state.</span><span class="sxs-lookup"><span data-stu-id="49aa3-104">Reliable Actors are single-threaded objects that can encapsulate both logic and state.</span></span> <span data-ttu-id="49aa3-105">Because actors run on Reliable Services, they can maintain state reliably by using the same persistence and replication mechanisms.</span><span class="sxs-lookup"><span data-stu-id="49aa3-105">Because actors run on Reliable Services, they can maintain state reliably by using the same persistence and replication mechanisms.</span></span> <span data-ttu-id="49aa3-106">This way, actors don't lose their state after failures, upon reactivation after garbage collection, or when they are moved around between nodes in a cluster due to resource balancing or upgrades.</span><span class="sxs-lookup"><span data-stu-id="49aa3-106">This way, actors don't lose their state after failures, upon reactivation after garbage collection, or when they are moved around between nodes in a cluster due to resource balancing or upgrades.</span></span>

## <a name="state-persistence-and-replication"></a><span data-ttu-id="49aa3-107">State persistence and replication</span><span class="sxs-lookup"><span data-stu-id="49aa3-107">State persistence and replication</span></span>
<span data-ttu-id="49aa3-108">All Reliable Actors are considered *stateful* because each actor instance maps to a unique ID.</span><span class="sxs-lookup"><span data-stu-id="49aa3-108">All Reliable Actors are considered *stateful* because each actor instance maps to a unique ID.</span></span> <span data-ttu-id="49aa3-109">This means that repeated calls to the same actor ID are routed to the same actor instance.</span><span class="sxs-lookup"><span data-stu-id="49aa3-109">This means that repeated calls to the same actor ID are routed to the same actor instance.</span></span> <span data-ttu-id="49aa3-110">In a stateless system, by contrast, client calls are not guaranteed to be routed to the same server every time.</span><span class="sxs-lookup"><span data-stu-id="49aa3-110">In a stateless system, by contrast, client calls are not guaranteed to be routed to the same server every time.</span></span> <span data-ttu-id="49aa3-111">For this reason, actor services are always stateful services.</span><span class="sxs-lookup"><span data-stu-id="49aa3-111">For this reason, actor services are always stateful services.</span></span>

<span data-ttu-id="49aa3-112">Even though actors are considered stateful, that does not mean they must store state reliably.</span><span class="sxs-lookup"><span data-stu-id="49aa3-112">Even though actors are considered stateful, that does not mean they must store state reliably.</span></span> <span data-ttu-id="49aa3-113">Actors can choose the level of state persistence and replication based on their data storage requirements:</span><span class="sxs-lookup"><span data-stu-id="49aa3-113">Actors can choose the level of state persistence and replication based on their data storage requirements:</span></span>

* <span data-ttu-id="49aa3-114">**Persisted state**: State is persisted to disk and is replicated to three or more replicas.</span><span class="sxs-lookup"><span data-stu-id="49aa3-114">**Persisted state**: State is persisted to disk and is replicated to three or more replicas.</span></span> <span data-ttu-id="49aa3-115">Persisted state is the most durable state storage option, where state can persist through complete cluster outage.</span><span class="sxs-lookup"><span data-stu-id="49aa3-115">Persisted state is the most durable state storage option, where state can persist through complete cluster outage.</span></span>
* <span data-ttu-id="49aa3-116">**Volatile state**: State is replicated to three or more replicas and only kept in memory.</span><span class="sxs-lookup"><span data-stu-id="49aa3-116">**Volatile state**: State is replicated to three or more replicas and only kept in memory.</span></span> <span data-ttu-id="49aa3-117">Volatile state provides resilience against node failure and actor failure, and during upgrades and resource balancing.</span><span class="sxs-lookup"><span data-stu-id="49aa3-117">Volatile state provides resilience against node failure and actor failure, and during upgrades and resource balancing.</span></span> <span data-ttu-id="49aa3-118">However, state is not persisted to disk.</span><span class="sxs-lookup"><span data-stu-id="49aa3-118">However, state is not persisted to disk.</span></span> <span data-ttu-id="49aa3-119">So if all replicas are lost at once, the state is lost as well.</span><span class="sxs-lookup"><span data-stu-id="49aa3-119">So if all replicas are lost at once, the state is lost as well.</span></span>
* <span data-ttu-id="49aa3-120">**No persisted state**: State is not replicated or written to disk, only use for actors that don't need to maintain state reliably.</span><span class="sxs-lookup"><span data-stu-id="49aa3-120">**No persisted state**: State is not replicated or written to disk, only use for actors that don't need to maintain state reliably.</span></span>

<span data-ttu-id="49aa3-121">Each level of persistence is simply a different *state provider* and *replication* configuration of your service.</span><span class="sxs-lookup"><span data-stu-id="49aa3-121">Each level of persistence is simply a different *state provider* and *replication* configuration of your service.</span></span> <span data-ttu-id="49aa3-122">Whether or not state is written to disk depends on the state provider--the component in a reliable service that stores state.</span><span class="sxs-lookup"><span data-stu-id="49aa3-122">Whether or not state is written to disk depends on the state provider--the component in a reliable service that stores state.</span></span> <span data-ttu-id="49aa3-123">Replication depends on how many replicas a service is deployed with.</span><span class="sxs-lookup"><span data-stu-id="49aa3-123">Replication depends on how many replicas a service is deployed with.</span></span> <span data-ttu-id="49aa3-124">As with Reliable Services, both the state provider and replica count can easily be set manually.</span><span class="sxs-lookup"><span data-stu-id="49aa3-124">As with Reliable Services, both the state provider and replica count can easily be set manually.</span></span> <span data-ttu-id="49aa3-125">The actor framework provides an attribute that, when used on an actor, automatically selects a default state provider and automatically generates settings for replica count to achieve one of these three persistence settings.</span><span class="sxs-lookup"><span data-stu-id="49aa3-125">The actor framework provides an attribute that, when used on an actor, automatically selects a default state provider and automatically generates settings for replica count to achieve one of these three persistence settings.</span></span> <span data-ttu-id="49aa3-126">The StatePersistence attribute is not inherited by derived class, each Actor type must provide its StatePersistence level.</span><span class="sxs-lookup"><span data-stu-id="49aa3-126">The StatePersistence attribute is not inherited by derived class, each Actor type must provide its StatePersistence level.</span></span>

### <a name="persisted-state"></a><span data-ttu-id="49aa3-127">Persisted state</span><span class="sxs-lookup"><span data-stu-id="49aa3-127">Persisted state</span></span>
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
<span data-ttu-id="49aa3-128">This setting uses a state provider that stores data on disk and automatically sets the service replica count to 3.</span><span class="sxs-lookup"><span data-stu-id="49aa3-128">This setting uses a state provider that stores data on disk and automatically sets the service replica count to 3.</span></span>

### <a name="volatile-state"></a><span data-ttu-id="49aa3-129">Volatile state</span><span class="sxs-lookup"><span data-stu-id="49aa3-129">Volatile state</span></span>
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
<span data-ttu-id="49aa3-130">This setting uses an in-memory-only state provider and sets the replica count to 3.</span><span class="sxs-lookup"><span data-stu-id="49aa3-130">This setting uses an in-memory-only state provider and sets the replica count to 3.</span></span>

### <a name="no-persisted-state"></a><span data-ttu-id="49aa3-131">No persisted state</span><span class="sxs-lookup"><span data-stu-id="49aa3-131">No persisted state</span></span>
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
<span data-ttu-id="49aa3-132">This setting uses an in-memory-only state provider and sets the replica count to 1.</span><span class="sxs-lookup"><span data-stu-id="49aa3-132">This setting uses an in-memory-only state provider and sets the replica count to 1.</span></span>

### <a name="defaults-and-generated-settings"></a><span data-ttu-id="49aa3-133">Defaults and generated settings</span><span class="sxs-lookup"><span data-stu-id="49aa3-133">Defaults and generated settings</span></span>
<span data-ttu-id="49aa3-134">When you're using the `StatePersistence` attribute, a state provider is automatically selected for you at runtime when the actor service starts.</span><span class="sxs-lookup"><span data-stu-id="49aa3-134">When you're using the `StatePersistence` attribute, a state provider is automatically selected for you at runtime when the actor service starts.</span></span> <span data-ttu-id="49aa3-135">The replica count, however, is set at compile time by the Visual Studio actor build tools.</span><span class="sxs-lookup"><span data-stu-id="49aa3-135">The replica count, however, is set at compile time by the Visual Studio actor build tools.</span></span> <span data-ttu-id="49aa3-136">The build tools automatically generate a *default service* for the actor service in ApplicationManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="49aa3-136">The build tools automatically generate a *default service* for the actor service in ApplicationManifest.xml.</span></span> <span data-ttu-id="49aa3-137">Parameters are created for **min replica set size** and **target replica set size**.</span><span class="sxs-lookup"><span data-stu-id="49aa3-137">Parameters are created for **min replica set size** and **target replica set size**.</span></span>

<span data-ttu-id="49aa3-138">You can change these parameters manually.</span><span class="sxs-lookup"><span data-stu-id="49aa3-138">You can change these parameters manually.</span></span> <span data-ttu-id="49aa3-139">But each time the `StatePersistence` attribute is changed, the parameters are set to the default replica set size values for the selected `StatePersistence` attribute, overriding any previous values.</span><span class="sxs-lookup"><span data-stu-id="49aa3-139">But each time the `StatePersistence` attribute is changed, the parameters are set to the default replica set size values for the selected `StatePersistence` attribute, overriding any previous values.</span></span> <span data-ttu-id="49aa3-140">In other words, the values that you set in ServiceManifest.xml are *only* overridden at build time when you change the `StatePersistence` attribute value.</span><span class="sxs-lookup"><span data-stu-id="49aa3-140">In other words, the values that you set in ServiceManifest.xml are *only* overridden at build time when you change the `StatePersistence` attribute value.</span></span>

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

## <a name="state-manager"></a><span data-ttu-id="49aa3-141">State manager</span><span class="sxs-lookup"><span data-stu-id="49aa3-141">State manager</span></span>
<span data-ttu-id="49aa3-142">Every actor instance has its own state manager: a dictionary-like data structure that reliably stores key/value pairs.</span><span class="sxs-lookup"><span data-stu-id="49aa3-142">Every actor instance has its own state manager: a dictionary-like data structure that reliably stores key/value pairs.</span></span> <span data-ttu-id="49aa3-143">The state manager is a wrapper around a state provider.</span><span class="sxs-lookup"><span data-stu-id="49aa3-143">The state manager is a wrapper around a state provider.</span></span> <span data-ttu-id="49aa3-144">You can use it to store data regardless of which persistence setting is used.</span><span class="sxs-lookup"><span data-stu-id="49aa3-144">You can use it to store data regardless of which persistence setting is used.</span></span> <span data-ttu-id="49aa3-145">It does not provide any guarantees that a running actor service can be changed from a volatile (in-memory-only) state setting to a persisted state setting through a rolling upgrade while preserving data.</span><span class="sxs-lookup"><span data-stu-id="49aa3-145">It does not provide any guarantees that a running actor service can be changed from a volatile (in-memory-only) state setting to a persisted state setting through a rolling upgrade while preserving data.</span></span> <span data-ttu-id="49aa3-146">However, it is possible to change replica count for a running service.</span><span class="sxs-lookup"><span data-stu-id="49aa3-146">However, it is possible to change replica count for a running service.</span></span>

<span data-ttu-id="49aa3-147">State manager keys must be strings.</span><span class="sxs-lookup"><span data-stu-id="49aa3-147">State manager keys must be strings.</span></span> <span data-ttu-id="49aa3-148">Values are generic and can be any type, including custom types.</span><span class="sxs-lookup"><span data-stu-id="49aa3-148">Values are generic and can be any type, including custom types.</span></span> <span data-ttu-id="49aa3-149">Values stored in the state manager must be data contract serializable because they might be transmitted over the network to other nodes during replication and might be written to disk, depending on an actor's state persistence setting.</span><span class="sxs-lookup"><span data-stu-id="49aa3-149">Values stored in the state manager must be data contract serializable because they might be transmitted over the network to other nodes during replication and might be written to disk, depending on an actor's state persistence setting.</span></span>

<span data-ttu-id="49aa3-150">The state manager exposes common dictionary methods for managing state, similar to those found in Reliable Dictionary.</span><span class="sxs-lookup"><span data-stu-id="49aa3-150">The state manager exposes common dictionary methods for managing state, similar to those found in Reliable Dictionary.</span></span>

<span data-ttu-id="49aa3-151">For examples of managing actor state, read [Access, save, and remove Reliable Actors state](service-fabric-reliable-actors-access-save-remove-state.md).</span><span class="sxs-lookup"><span data-stu-id="49aa3-151">For examples of managing actor state, read [Access, save, and remove Reliable Actors state](service-fabric-reliable-actors-access-save-remove-state.md).</span></span>

## <a name="best-practices"></a><span data-ttu-id="49aa3-152">Best practices</span><span class="sxs-lookup"><span data-stu-id="49aa3-152">Best practices</span></span>
<span data-ttu-id="49aa3-153">Here are some suggested practices and troubleshooting tips for managing your actor state.</span><span class="sxs-lookup"><span data-stu-id="49aa3-153">Here are some suggested practices and troubleshooting tips for managing your actor state.</span></span>

### <a name="make-the-actor-state-as-granular-as-possible"></a><span data-ttu-id="49aa3-154">Make the actor state as granular as possible</span><span class="sxs-lookup"><span data-stu-id="49aa3-154">Make the actor state as granular as possible</span></span>
<span data-ttu-id="49aa3-155">This is critical for performance and resource usage of your application.</span><span class="sxs-lookup"><span data-stu-id="49aa3-155">This is critical for performance and resource usage of your application.</span></span> <span data-ttu-id="49aa3-156">Whenever there is any write/update to the "named state" of an actor, the whole value corresponding to that "named state" is serialized and sent over the network to the secondary replicas.</span><span class="sxs-lookup"><span data-stu-id="49aa3-156">Whenever there is any write/update to the "named state" of an actor, the whole value corresponding to that "named state" is serialized and sent over the network to the secondary replicas.</span></span>  <span data-ttu-id="49aa3-157">The secondaries write it to local disk and reply back to the primary replica.</span><span class="sxs-lookup"><span data-stu-id="49aa3-157">The secondaries write it to local disk and reply back to the primary replica.</span></span> <span data-ttu-id="49aa3-158">When the primary receives acknowledgements from a quorum of secondary replicas, it writes the state to its local disk.</span><span class="sxs-lookup"><span data-stu-id="49aa3-158">When the primary receives acknowledgements from a quorum of secondary replicas, it writes the state to its local disk.</span></span> <span data-ttu-id="49aa3-159">For example, suppose the value is a class which has 20 members and a size of 1 MB.</span><span class="sxs-lookup"><span data-stu-id="49aa3-159">For example, suppose the value is a class which has 20 members and a size of 1 MB.</span></span> <span data-ttu-id="49aa3-160">Even if you only modified one of the class members which is of size 1 KB, you end up paying the cost of serialization and network and disk writes for the full 1 MB.</span><span class="sxs-lookup"><span data-stu-id="49aa3-160">Even if you only modified one of the class members which is of size 1 KB, you end up paying the cost of serialization and network and disk writes for the full 1 MB.</span></span> <span data-ttu-id="49aa3-161">Similarly, if the value is a collection (such as a list, array, or dictionary), you pay the cost for the complete collection even if you modify one of it's members.</span><span class="sxs-lookup"><span data-stu-id="49aa3-161">Similarly, if the value is a collection (such as a list, array, or dictionary), you pay the cost for the complete collection even if you modify one of it's members.</span></span> <span data-ttu-id="49aa3-162">The StateManager interface of the actor class is like a dictionary.</span><span class="sxs-lookup"><span data-stu-id="49aa3-162">The StateManager interface of the actor class is like a dictionary.</span></span> <span data-ttu-id="49aa3-163">You should always model the data structure representing actor state on top of this dictionary.</span><span class="sxs-lookup"><span data-stu-id="49aa3-163">You should always model the data structure representing actor state on top of this dictionary.</span></span>
 
### <a name="correctly-manage-the-actors-life-cycle"></a><span data-ttu-id="49aa3-164">Correctly manage the actor's life-cycle</span><span class="sxs-lookup"><span data-stu-id="49aa3-164">Correctly manage the actor's life-cycle</span></span>
<span data-ttu-id="49aa3-165">You should have clear policy about managing the size of state in each partition of an actor service.</span><span class="sxs-lookup"><span data-stu-id="49aa3-165">You should have clear policy about managing the size of state in each partition of an actor service.</span></span> <span data-ttu-id="49aa3-166">Your actor service should have a fixed number of actors and reuse them a much as possible.</span><span class="sxs-lookup"><span data-stu-id="49aa3-166">Your actor service should have a fixed number of actors and reuse them a much as possible.</span></span> <span data-ttu-id="49aa3-167">If you continuously create new actors, you must delete them once they are done with their work.</span><span class="sxs-lookup"><span data-stu-id="49aa3-167">If you continuously create new actors, you must delete them once they are done with their work.</span></span> <span data-ttu-id="49aa3-168">The actor framework stores some metadata about each actor that exists.</span><span class="sxs-lookup"><span data-stu-id="49aa3-168">The actor framework stores some metadata about each actor that exists.</span></span> <span data-ttu-id="49aa3-169">Deleting all the state of an actor does not remove metadata about that actor.</span><span class="sxs-lookup"><span data-stu-id="49aa3-169">Deleting all the state of an actor does not remove metadata about that actor.</span></span> <span data-ttu-id="49aa3-170">You must delete the actor (see [deleting actors and their state](service-fabric-reliable-actors-lifecycle.md#manually-deleting-actors-and-their-state)) to remove all the information about it stored in the system.</span><span class="sxs-lookup"><span data-stu-id="49aa3-170">You must delete the actor (see [deleting actors and their state](service-fabric-reliable-actors-lifecycle.md#manually-deleting-actors-and-their-state)) to remove all the information about it stored in the system.</span></span> <span data-ttu-id="49aa3-171">As an extra check, you should query the actor service (see [enumerating actors](service-fabric-reliable-actors-platform.md)) once in a while to make sure the number actors are within the expected range.</span><span class="sxs-lookup"><span data-stu-id="49aa3-171">As an extra check, you should query the actor service (see [enumerating actors](service-fabric-reliable-actors-platform.md)) once in a while to make sure the number actors are within the expected range.</span></span>
 
<span data-ttu-id="49aa3-172">If you ever see that database file size of an Actor Service is increasing beyond the expected size, make sure that you are following the preceding guidelines.</span><span class="sxs-lookup"><span data-stu-id="49aa3-172">If you ever see that database file size of an Actor Service is increasing beyond the expected size, make sure that you are following the preceding guidelines.</span></span> <span data-ttu-id="49aa3-173">If you are following these guidelines and are still database file size issues, you should [open a support ticket](service-fabric-support.md) with the product team to get help.</span><span class="sxs-lookup"><span data-stu-id="49aa3-173">If you are following these guidelines and are still database file size issues, you should [open a support ticket](service-fabric-support.md) with the product team to get help.</span></span>

## <a name="next-steps"></a><span data-ttu-id="49aa3-174">Next steps</span><span class="sxs-lookup"><span data-stu-id="49aa3-174">Next steps</span></span>

<span data-ttu-id="49aa3-175">State that's stored in Reliable Actors must be serialized before its written to disk and replicated for high availability.</span><span class="sxs-lookup"><span data-stu-id="49aa3-175">State that's stored in Reliable Actors must be serialized before its written to disk and replicated for high availability.</span></span> <span data-ttu-id="49aa3-176">Learn more about [Actor type serialization](service-fabric-reliable-actors-notes-on-actor-type-serialization.md).</span><span class="sxs-lookup"><span data-stu-id="49aa3-176">Learn more about [Actor type serialization](service-fabric-reliable-actors-notes-on-actor-type-serialization.md).</span></span>

<span data-ttu-id="49aa3-177">Next, learn more about [Actor diagnostics and performance monitoring](service-fabric-reliable-actors-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="49aa3-177">Next, learn more about [Actor diagnostics and performance monitoring](service-fabric-reliable-actors-diagnostics.md).</span></span>
