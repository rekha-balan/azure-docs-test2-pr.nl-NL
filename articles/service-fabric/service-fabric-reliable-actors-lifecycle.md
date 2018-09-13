---
title: Overview of actor-based Azure microservices lifecycle | Microsoft Docs
description: Explains Service Fabric Reliable Actor lifecycle, garbage collection, and manually deleting actors and their state
services: service-fabric
documentationcenter: .net
author: amanbha
manager: timlt
editor: vturecek
ms.assetid: b91384cc-804c-49d6-a6cb-f3f3d7d65a8e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/02/2017
ms.author: amanbha
ms.openlocfilehash: 957af8178efb4b7dbef7a6743e4aa4e3a1fd47b3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554006"
---
# <a name="actor-lifecycle-automatic-garbage-collection-and-manual-delete"></a><span data-ttu-id="40d93-103">Actor lifecycle, automatic garbage collection, and manual delete</span><span class="sxs-lookup"><span data-stu-id="40d93-103">Actor lifecycle, automatic garbage collection, and manual delete</span></span>
<span data-ttu-id="40d93-104">An actor is activated the first time a call is made to any of its methods.</span><span class="sxs-lookup"><span data-stu-id="40d93-104">An actor is activated the first time a call is made to any of its methods.</span></span> <span data-ttu-id="40d93-105">An actor is deactivated (garbage collected by the Actors runtime) if it is not used for a configurable period of time.</span><span class="sxs-lookup"><span data-stu-id="40d93-105">An actor is deactivated (garbage collected by the Actors runtime) if it is not used for a configurable period of time.</span></span> <span data-ttu-id="40d93-106">An actor and its state can also be deleted manually at any time.</span><span class="sxs-lookup"><span data-stu-id="40d93-106">An actor and its state can also be deleted manually at any time.</span></span>

## <a name="actor-activation"></a><span data-ttu-id="40d93-107">Actor activation</span><span class="sxs-lookup"><span data-stu-id="40d93-107">Actor activation</span></span>
<span data-ttu-id="40d93-108">When an actor is activated, the following occurs:</span><span class="sxs-lookup"><span data-stu-id="40d93-108">When an actor is activated, the following occurs:</span></span>

* <span data-ttu-id="40d93-109">When a call comes for an actor and one is not already active, a new actor is created.</span><span class="sxs-lookup"><span data-stu-id="40d93-109">When a call comes for an actor and one is not already active, a new actor is created.</span></span>
* <span data-ttu-id="40d93-110">The actor's state is loaded if it's maintaining state.</span><span class="sxs-lookup"><span data-stu-id="40d93-110">The actor's state is loaded if it's maintaining state.</span></span>
* <span data-ttu-id="40d93-111">The `OnActivateAsync` (C#) or `onActivateAsync` (Java) method (which can be overridden in the actor implementation) is called.</span><span class="sxs-lookup"><span data-stu-id="40d93-111">The `OnActivateAsync` (C#) or `onActivateAsync` (Java) method (which can be overridden in the actor implementation) is called.</span></span>
* <span data-ttu-id="40d93-112">The actor is now considered active.</span><span class="sxs-lookup"><span data-stu-id="40d93-112">The actor is now considered active.</span></span>

## <a name="actor-deactivation"></a><span data-ttu-id="40d93-113">Actor deactivation</span><span class="sxs-lookup"><span data-stu-id="40d93-113">Actor deactivation</span></span>
<span data-ttu-id="40d93-114">When an actor is deactivated, the following occurs:</span><span class="sxs-lookup"><span data-stu-id="40d93-114">When an actor is deactivated, the following occurs:</span></span>

* <span data-ttu-id="40d93-115">When an actor is not used for some period of time, it is removed from the Active Actors table.</span><span class="sxs-lookup"><span data-stu-id="40d93-115">When an actor is not used for some period of time, it is removed from the Active Actors table.</span></span>
* <span data-ttu-id="40d93-116">The `OnDeactivateAsync` (C#) or `onDeactivateAsync` (Java) method (which can be overridden in the actor implementation) is called.</span><span class="sxs-lookup"><span data-stu-id="40d93-116">The `OnDeactivateAsync` (C#) or `onDeactivateAsync` (Java) method (which can be overridden in the actor implementation) is called.</span></span> <span data-ttu-id="40d93-117">This clears all the timers for the actor.</span><span class="sxs-lookup"><span data-stu-id="40d93-117">This clears all the timers for the actor.</span></span> <span data-ttu-id="40d93-118">Actor operations like state changes should not be called from this method.</span><span class="sxs-lookup"><span data-stu-id="40d93-118">Actor operations like state changes should not be called from this method.</span></span>

> [!TIP]
> <span data-ttu-id="40d93-119">The Fabric Actors runtime emits some [events related to actor activation and deactivation](service-fabric-reliable-actors-diagnostics.md#list-of-events-and-performance-counters).</span><span class="sxs-lookup"><span data-stu-id="40d93-119">The Fabric Actors runtime emits some [events related to actor activation and deactivation](service-fabric-reliable-actors-diagnostics.md#list-of-events-and-performance-counters).</span></span> <span data-ttu-id="40d93-120">They are useful in diagnostics and performance monitoring.</span><span class="sxs-lookup"><span data-stu-id="40d93-120">They are useful in diagnostics and performance monitoring.</span></span>
>
>

### <a name="actor-garbage-collection"></a><span data-ttu-id="40d93-121">Actor garbage collection</span><span class="sxs-lookup"><span data-stu-id="40d93-121">Actor garbage collection</span></span>
<span data-ttu-id="40d93-122">When an actor is deactivated, references to the actor object are released and it can be garbage collected normally by the common language runtime (CLR) or java virtual machine (JVM) garbage collector.</span><span class="sxs-lookup"><span data-stu-id="40d93-122">When an actor is deactivated, references to the actor object are released and it can be garbage collected normally by the common language runtime (CLR) or java virtual machine (JVM) garbage collector.</span></span> <span data-ttu-id="40d93-123">Garbage collection only cleans up the actor object; it does **not** remove state stored in the actor's State Manager.</span><span class="sxs-lookup"><span data-stu-id="40d93-123">Garbage collection only cleans up the actor object; it does **not** remove state stored in the actor's State Manager.</span></span> <span data-ttu-id="40d93-124">The next time the actor is activated, a new actor object is created and its state is restored.</span><span class="sxs-lookup"><span data-stu-id="40d93-124">The next time the actor is activated, a new actor object is created and its state is restored.</span></span>

<span data-ttu-id="40d93-125">What counts as “being used” for the purpose of deactivation and garbage collection?</span><span class="sxs-lookup"><span data-stu-id="40d93-125">What counts as “being used” for the purpose of deactivation and garbage collection?</span></span>

* <span data-ttu-id="40d93-126">Receiving a call</span><span class="sxs-lookup"><span data-stu-id="40d93-126">Receiving a call</span></span>
* <span data-ttu-id="40d93-127">`IRemindable.ReceiveReminderAsync` method being invoked (applicable only if the actor uses reminders)</span><span class="sxs-lookup"><span data-stu-id="40d93-127">`IRemindable.ReceiveReminderAsync` method being invoked (applicable only if the actor uses reminders)</span></span>

> [!NOTE]
> <span data-ttu-id="40d93-128">if the actor uses timers and its timer callback is invoked, it does **not** count as "being used".</span><span class="sxs-lookup"><span data-stu-id="40d93-128">if the actor uses timers and its timer callback is invoked, it does **not** count as "being used".</span></span>
>
>

<span data-ttu-id="40d93-129">Before we go into the details of deactivation, it is important to define the following terms:</span><span class="sxs-lookup"><span data-stu-id="40d93-129">Before we go into the details of deactivation, it is important to define the following terms:</span></span>

* <span data-ttu-id="40d93-130">*Scan interval*.</span><span class="sxs-lookup"><span data-stu-id="40d93-130">*Scan interval*.</span></span> <span data-ttu-id="40d93-131">This is the interval at which the Actors runtime scans its Active Actors table for actors that can be deactivated and garbage collected.</span><span class="sxs-lookup"><span data-stu-id="40d93-131">This is the interval at which the Actors runtime scans its Active Actors table for actors that can be deactivated and garbage collected.</span></span> <span data-ttu-id="40d93-132">The default value for this is 1 minute.</span><span class="sxs-lookup"><span data-stu-id="40d93-132">The default value for this is 1 minute.</span></span>
* <span data-ttu-id="40d93-133">*Idle timeout*.</span><span class="sxs-lookup"><span data-stu-id="40d93-133">*Idle timeout*.</span></span> <span data-ttu-id="40d93-134">This is the amount of time that an actor needs to remain unused (idle) before it can be deactivated and garbage collected.</span><span class="sxs-lookup"><span data-stu-id="40d93-134">This is the amount of time that an actor needs to remain unused (idle) before it can be deactivated and garbage collected.</span></span> <span data-ttu-id="40d93-135">The default value for this is 60 minutes.</span><span class="sxs-lookup"><span data-stu-id="40d93-135">The default value for this is 60 minutes.</span></span>

<span data-ttu-id="40d93-136">Typically, you do not need to change these defaults.</span><span class="sxs-lookup"><span data-stu-id="40d93-136">Typically, you do not need to change these defaults.</span></span> <span data-ttu-id="40d93-137">However, if necessary, these intervals can be changed through `ActorServiceSettings` when registering your [Actor Service](service-fabric-reliable-actors-platform.md):</span><span class="sxs-lookup"><span data-stu-id="40d93-137">However, if necessary, these intervals can be changed through `ActorServiceSettings` when registering your [Actor Service](service-fabric-reliable-actors-platform.md):</span></span>

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        ActorRuntime.RegisterActorAsync<MyActor>((context, actorType) =>
                new ActorService(context, actorType,
                    settings:
                        new ActorServiceSettings()
                        {
                            ActorGarbageCollectionSettings =
                                new ActorGarbageCollectionSettings(10, 2)
                        }))
            .GetAwaiter()
            .GetResult();
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
    }
}
```
<span data-ttu-id="40d93-138">For each active actor, the actor runtime keeps track of the amount of time that it has been idle (i.e. not used).</span><span class="sxs-lookup"><span data-stu-id="40d93-138">For each active actor, the actor runtime keeps track of the amount of time that it has been idle (i.e. not used).</span></span> <span data-ttu-id="40d93-139">The actor runtime checks each of the actors every `ScanIntervalInSeconds` to see if it can be garbage collected and collects it if it has been idle for `IdleTimeoutInSeconds`.</span><span class="sxs-lookup"><span data-stu-id="40d93-139">The actor runtime checks each of the actors every `ScanIntervalInSeconds` to see if it can be garbage collected and collects it if it has been idle for `IdleTimeoutInSeconds`.</span></span>

<span data-ttu-id="40d93-140">Anytime an actor is used, its idle time is reset to 0.</span><span class="sxs-lookup"><span data-stu-id="40d93-140">Anytime an actor is used, its idle time is reset to 0.</span></span> <span data-ttu-id="40d93-141">After this, the actor can be garbage collected only if it again remains idle for `IdleTimeoutInSeconds`.</span><span class="sxs-lookup"><span data-stu-id="40d93-141">After this, the actor can be garbage collected only if it again remains idle for `IdleTimeoutInSeconds`.</span></span> <span data-ttu-id="40d93-142">Recall that an actor is considered to have been used if either an actor interface method or an actor reminder callback is executed.</span><span class="sxs-lookup"><span data-stu-id="40d93-142">Recall that an actor is considered to have been used if either an actor interface method or an actor reminder callback is executed.</span></span> <span data-ttu-id="40d93-143">An actor is **not** considered to have been used if its timer callback is executed.</span><span class="sxs-lookup"><span data-stu-id="40d93-143">An actor is **not** considered to have been used if its timer callback is executed.</span></span>

<span data-ttu-id="40d93-144">The following diagram shows the lifecycle of a single actor to illustrate these concepts.</span><span class="sxs-lookup"><span data-stu-id="40d93-144">The following diagram shows the lifecycle of a single actor to illustrate these concepts.</span></span>

![Example of idle time][1]

<span data-ttu-id="40d93-146">The example shows the impact of actor method calls, reminders, and timers on the lifetime of this actor.</span><span class="sxs-lookup"><span data-stu-id="40d93-146">The example shows the impact of actor method calls, reminders, and timers on the lifetime of this actor.</span></span> <span data-ttu-id="40d93-147">The following points about the example are worth mentioning:</span><span class="sxs-lookup"><span data-stu-id="40d93-147">The following points about the example are worth mentioning:</span></span>

* <span data-ttu-id="40d93-148">ScanInterval and IdleTimeout are set to 5 and 10 respectively.</span><span class="sxs-lookup"><span data-stu-id="40d93-148">ScanInterval and IdleTimeout are set to 5 and 10 respectively.</span></span> <span data-ttu-id="40d93-149">(Units do not matter here, since our purpose is only to illustrate the concept.)</span><span class="sxs-lookup"><span data-stu-id="40d93-149">(Units do not matter here, since our purpose is only to illustrate the concept.)</span></span>
* <span data-ttu-id="40d93-150">The scan for actors to be garbage collected happens at T=0,5,10,15,20,25, as defined by the scan interval of 5.</span><span class="sxs-lookup"><span data-stu-id="40d93-150">The scan for actors to be garbage collected happens at T=0,5,10,15,20,25, as defined by the scan interval of 5.</span></span>
* <span data-ttu-id="40d93-151">A periodic timer fires at T=4,8,12,16,20,24, and its callback executes.</span><span class="sxs-lookup"><span data-stu-id="40d93-151">A periodic timer fires at T=4,8,12,16,20,24, and its callback executes.</span></span> <span data-ttu-id="40d93-152">It does not impact the idle time of the actor.</span><span class="sxs-lookup"><span data-stu-id="40d93-152">It does not impact the idle time of the actor.</span></span>
* <span data-ttu-id="40d93-153">An actor method call at T=7 resets the idle time to 0 and delays the garbage collection of the actor.</span><span class="sxs-lookup"><span data-stu-id="40d93-153">An actor method call at T=7 resets the idle time to 0 and delays the garbage collection of the actor.</span></span>
* <span data-ttu-id="40d93-154">An actor reminder callback executes at T=14 and further delays the garbage collection of the actor.</span><span class="sxs-lookup"><span data-stu-id="40d93-154">An actor reminder callback executes at T=14 and further delays the garbage collection of the actor.</span></span>
* <span data-ttu-id="40d93-155">During the garbage collection scan at T=25, the actor's idle time finally exceeds the idle timeout of 10, and the actor is garbage collected.</span><span class="sxs-lookup"><span data-stu-id="40d93-155">During the garbage collection scan at T=25, the actor's idle time finally exceeds the idle timeout of 10, and the actor is garbage collected.</span></span>

<span data-ttu-id="40d93-156">An actor will never be garbage collected while it is executing one of its methods, no matter how much time is spent in executing that method.</span><span class="sxs-lookup"><span data-stu-id="40d93-156">An actor will never be garbage collected while it is executing one of its methods, no matter how much time is spent in executing that method.</span></span> <span data-ttu-id="40d93-157">As mentioned earlier, the execution of actor interface methods and reminder callbacks prevents garbage collection by resetting the actor's idle time to 0.</span><span class="sxs-lookup"><span data-stu-id="40d93-157">As mentioned earlier, the execution of actor interface methods and reminder callbacks prevents garbage collection by resetting the actor's idle time to 0.</span></span> <span data-ttu-id="40d93-158">The execution of timer callbacks does not reset the idle time to 0.</span><span class="sxs-lookup"><span data-stu-id="40d93-158">The execution of timer callbacks does not reset the idle time to 0.</span></span> <span data-ttu-id="40d93-159">However, the garbage collection of the actor is deferred until the timer callback has completed execution.</span><span class="sxs-lookup"><span data-stu-id="40d93-159">However, the garbage collection of the actor is deferred until the timer callback has completed execution.</span></span>

## <a name="deleting-actors-and-their-state"></a><span data-ttu-id="40d93-160">Deleting actors and their state</span><span class="sxs-lookup"><span data-stu-id="40d93-160">Deleting actors and their state</span></span>
<span data-ttu-id="40d93-161">Garbage collection of deactivated actors only cleans up the actor object, but it does not remove data that is stored in an actor's State Manager.</span><span class="sxs-lookup"><span data-stu-id="40d93-161">Garbage collection of deactivated actors only cleans up the actor object, but it does not remove data that is stored in an actor's State Manager.</span></span> <span data-ttu-id="40d93-162">When an actor is re-activated, its data is again made available to it through the State Manager.</span><span class="sxs-lookup"><span data-stu-id="40d93-162">When an actor is re-activated, its data is again made available to it through the State Manager.</span></span> <span data-ttu-id="40d93-163">In cases where actors store data in State Manager and are deactivated but never re-activated, it may be necessary to clean up their data.</span><span class="sxs-lookup"><span data-stu-id="40d93-163">In cases where actors store data in State Manager and are deactivated but never re-activated, it may be necessary to clean up their data.</span></span>

<span data-ttu-id="40d93-164">The [Actor Service](service-fabric-reliable-actors-platform.md) provides a function for deleting actors from a remote caller:</span><span class="sxs-lookup"><span data-stu-id="40d93-164">The [Actor Service](service-fabric-reliable-actors-platform.md) provides a function for deleting actors from a remote caller:</span></span>

```csharp
ActorId actorToDelete = new ActorId(id);

IActorService myActorServiceProxy = ActorServiceProxy.Create(
    new Uri("fabric:/MyApp/MyService"), actorToDelete);

await myActorServiceProxy.DeleteActorAsync(actorToDelete, cancellationToken)
```
```Java
ActorId actorToDelete = new ActorId(id);

ActorService myActorServiceProxy = ActorServiceProxy.create(
    new Uri("fabric:/MyApp/MyService"), actorToDelete);

myActorServiceProxy.deleteActorAsync(actorToDelete);
```

<span data-ttu-id="40d93-165">Deleting an actor has the following effects depending on whether or not the actor is currently active:</span><span class="sxs-lookup"><span data-stu-id="40d93-165">Deleting an actor has the following effects depending on whether or not the actor is currently active:</span></span>

* <span data-ttu-id="40d93-166">**Active Actor**</span><span class="sxs-lookup"><span data-stu-id="40d93-166">**Active Actor**</span></span>
  * <span data-ttu-id="40d93-167">Actor is removed from active actors list and is deactivated.</span><span class="sxs-lookup"><span data-stu-id="40d93-167">Actor is removed from active actors list and is deactivated.</span></span>
  * <span data-ttu-id="40d93-168">Its state is deleted permanently.</span><span class="sxs-lookup"><span data-stu-id="40d93-168">Its state is deleted permanently.</span></span>
* <span data-ttu-id="40d93-169">**Inactive Actor**</span><span class="sxs-lookup"><span data-stu-id="40d93-169">**Inactive Actor**</span></span>
  * <span data-ttu-id="40d93-170">Its state is deleted permanently.</span><span class="sxs-lookup"><span data-stu-id="40d93-170">Its state is deleted permanently.</span></span>

<span data-ttu-id="40d93-171">Note that an actor cannot call delete on itself from one of its actor methods because the actor cannot be deleted while executing within an actor call context, in which the runtime has obtained a lock around the actor call to enforce single-threaded access.</span><span class="sxs-lookup"><span data-stu-id="40d93-171">Note that an actor cannot call delete on itself from one of its actor methods because the actor cannot be deleted while executing within an actor call context, in which the runtime has obtained a lock around the actor call to enforce single-threaded access.</span></span>

## <a name="next-steps"></a><span data-ttu-id="40d93-172">Next steps</span><span class="sxs-lookup"><span data-stu-id="40d93-172">Next steps</span></span>
* [<span data-ttu-id="40d93-173">Actor timers and reminders</span><span class="sxs-lookup"><span data-stu-id="40d93-173">Actor timers and reminders</span></span>](service-fabric-reliable-actors-timers-reminders.md)
* [<span data-ttu-id="40d93-174">Actor events</span><span class="sxs-lookup"><span data-stu-id="40d93-174">Actor events</span></span>](service-fabric-reliable-actors-events.md)
* [<span data-ttu-id="40d93-175">Actor reentrancy</span><span class="sxs-lookup"><span data-stu-id="40d93-175">Actor reentrancy</span></span>](service-fabric-reliable-actors-reentrancy.md)
* [<span data-ttu-id="40d93-176">Actor diagnostics and performance monitoring</span><span class="sxs-lookup"><span data-stu-id="40d93-176">Actor diagnostics and performance monitoring</span></span>](service-fabric-reliable-actors-diagnostics.md)
* [<span data-ttu-id="40d93-177">Actor API reference documentation</span><span class="sxs-lookup"><span data-stu-id="40d93-177">Actor API reference documentation</span></span>](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [<span data-ttu-id="40d93-178">C# Sample code</span><span class="sxs-lookup"><span data-stu-id="40d93-178">C# Sample code</span></span>](https://github.com/Azure/servicefabric-samples)
* [<span data-ttu-id="40d93-179">Java Sample code</span><span class="sxs-lookup"><span data-stu-id="40d93-179">Java Sample code</span></span>](http://github.com/Azure-Samples/service-fabric-java-getting-started)

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-reliable-actors-lifecycle/garbage-collection.png

