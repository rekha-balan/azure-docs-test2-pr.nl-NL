---
title: Reliable Actors timers and reminders | Microsoft Docs
description: Introduction to timers and reminders for Service Fabric Reliable Actors.
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: amanbha
ms.assetid: 00c48716-569e-4a64-bd6c-25234c85ff4f
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/10/2017
ms.author: vturecek
ms.openlocfilehash: 0798a2d91df01faf240d95bffc52af1c29055b71
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661943"
---
# <a name="actor-timers-and-reminders"></a><span data-ttu-id="cc4ab-103">Actor timers and reminders</span><span class="sxs-lookup"><span data-stu-id="cc4ab-103">Actor timers and reminders</span></span>
<span data-ttu-id="cc4ab-104">Actors can schedule periodic work on themselves by registering either timers or reminders.</span><span class="sxs-lookup"><span data-stu-id="cc4ab-104">Actors can schedule periodic work on themselves by registering either timers or reminders.</span></span> <span data-ttu-id="cc4ab-105">This article shows how to use timers and reminders and explains the differences between them.</span><span class="sxs-lookup"><span data-stu-id="cc4ab-105">This article shows how to use timers and reminders and explains the differences between them.</span></span>

## <a name="actor-timers"></a><span data-ttu-id="cc4ab-106">Actor timers</span><span class="sxs-lookup"><span data-stu-id="cc4ab-106">Actor timers</span></span>
<span data-ttu-id="cc4ab-107">Actor timers provide a simple wrapper around a .NET or Java timer to ensure that the callback methods respect the turn-based concurrency guarantees that the Actors runtime provides.</span><span class="sxs-lookup"><span data-stu-id="cc4ab-107">Actor timers provide a simple wrapper around a .NET or Java timer to ensure that the callback methods respect the turn-based concurrency guarantees that the Actors runtime provides.</span></span>

<span data-ttu-id="cc4ab-108">Actors can use the `RegisterTimer`(C#) or `registerTimer`(Java)  and `UnregisterTimer`(C#) or `unregisterTimer`(Java) methods on their base class to register and unregister their timers.</span><span class="sxs-lookup"><span data-stu-id="cc4ab-108">Actors can use the `RegisterTimer`(C#) or `registerTimer`(Java)  and `UnregisterTimer`(C#) or `unregisterTimer`(Java) methods on their base class to register and unregister their timers.</span></span> <span data-ttu-id="cc4ab-109">The example below shows the use of timer APIs.</span><span class="sxs-lookup"><span data-stu-id="cc4ab-109">The example below shows the use of timer APIs.</span></span> <span data-ttu-id="cc4ab-110">The APIs are very similar to the .NET timer or Java timer.</span><span class="sxs-lookup"><span data-stu-id="cc4ab-110">The APIs are very similar to the .NET timer or Java timer.</span></span> <span data-ttu-id="cc4ab-111">In this example, when the timer is due, the Actors runtime will call the `MoveObject`(C#) or `moveObject`(Java) method.</span><span class="sxs-lookup"><span data-stu-id="cc4ab-111">In this example, when the timer is due, the Actors runtime will call the `MoveObject`(C#) or `moveObject`(Java) method.</span></span> <span data-ttu-id="cc4ab-112">The method is guaranteed to respect the turn-based concurrency.</span><span class="sxs-lookup"><span data-stu-id="cc4ab-112">The method is guaranteed to respect the turn-based concurrency.</span></span> <span data-ttu-id="cc4ab-113">This means that no other actor methods or timer/reminder callbacks will be in progress until this callback completes execution.</span><span class="sxs-lookup"><span data-stu-id="cc4ab-113">This means that no other actor methods or timer/reminder callbacks will be in progress until this callback completes execution.</span></span>

```csharp
class VisualObjectActor : Actor, IVisualObject
{
    private IActorTimer _updateTimer;

    public VisualObjectActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    protected override Task OnActivateAsync()
    {
        ...

        _updateTimer = RegisterTimer(
            MoveObject,                     // Callback method
            null,                           // Parameter to pass to the callback method
            TimeSpan.FromMilliseconds(15),  // Amount of time to delay before the callback is invoked
            TimeSpan.FromMilliseconds(15)); // Time interval between invocations of the callback method

        return base.OnActivateAsync();
    }

    protected override Task OnDeactivateAsync()
    {
        if (_updateTimer != null)
        {
            UnregisterTimer(_updateTimer);
        }

        return base.OnDeactivateAsync();
    }

    private Task MoveObject(object state)
    {
        ...
        return Task.FromResult(true);
    }
}
```
```Java
public class VisualObjectActorImpl extends FabricActor implements VisualObjectActor
{
    private ActorTimer updateTimer;

    public VisualObjectActorImpl(FabricActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    @Override
    protected CompletableFuture onActivateAsync()
    {
        ...

        return this.stateManager()
                .getOrAddStateAsync(
                        stateName,
                        VisualObject.createRandom(
                                this.getId().toString(),
                                new Random(this.getId().toString().hashCode())))
                .thenApply((r) -> {
                    this.registerTimer(
                            (o) -> this.moveObject(o),                        // Callback method
                            "moveObject",
                            null,                                             // Parameter to pass to the callback method
                            Duration.ofMillis(10),                            // Amount of time to delay before the callback is invoked
                            Duration.ofMillis(timerIntervalInMilliSeconds));  // Time interval between invocations of the callback method
                    return null;
                });
    }

    @Override
    protected CompletableFuture onDeactivateAsync()
    {
        if (updateTimer != null)
        {
            unregisterTimer(updateTimer);
        }

        return super.onDeactivateAsync();
    }

    private CompletableFuture moveObject(Object state)
    {
        ...
        return this.stateManager().getStateAsync(this.stateName).thenCompose(v -> {
            VisualObject v1 = (VisualObject)v;
            v1.move();
            return (CompletableFuture<?>)this.stateManager().setStateAsync(stateName, v1).
                    thenApply(r -> {
                      ...
                      return null;});
        });
    }
}
```

<span data-ttu-id="cc4ab-114">The next period of the timer starts after the callback completes execution.</span><span class="sxs-lookup"><span data-stu-id="cc4ab-114">The next period of the timer starts after the callback completes execution.</span></span> <span data-ttu-id="cc4ab-115">This implies that the timer is stopped while the callback is executing and is started when the callback finishes.</span><span class="sxs-lookup"><span data-stu-id="cc4ab-115">This implies that the timer is stopped while the callback is executing and is started when the callback finishes.</span></span>

<span data-ttu-id="cc4ab-116">The Actors runtime saves changes made to the actor's State Manager when the callback finishes.</span><span class="sxs-lookup"><span data-stu-id="cc4ab-116">The Actors runtime saves changes made to the actor's State Manager when the callback finishes.</span></span> <span data-ttu-id="cc4ab-117">If an error occurs in saving the state, that actor object will be deactivated and a new instance will be activated.</span><span class="sxs-lookup"><span data-stu-id="cc4ab-117">If an error occurs in saving the state, that actor object will be deactivated and a new instance will be activated.</span></span>

<span data-ttu-id="cc4ab-118">All timers are stopped when the actor is deactivated as part of garbage collection.</span><span class="sxs-lookup"><span data-stu-id="cc4ab-118">All timers are stopped when the actor is deactivated as part of garbage collection.</span></span> <span data-ttu-id="cc4ab-119">No timer callbacks are invoked after that.</span><span class="sxs-lookup"><span data-stu-id="cc4ab-119">No timer callbacks are invoked after that.</span></span> <span data-ttu-id="cc4ab-120">Also, the Actors runtime does not retain any information about the timers that were running before deactivation.</span><span class="sxs-lookup"><span data-stu-id="cc4ab-120">Also, the Actors runtime does not retain any information about the timers that were running before deactivation.</span></span> <span data-ttu-id="cc4ab-121">It is up to the actor to register any timers that it needs when it is reactivated in the future.</span><span class="sxs-lookup"><span data-stu-id="cc4ab-121">It is up to the actor to register any timers that it needs when it is reactivated in the future.</span></span> <span data-ttu-id="cc4ab-122">For more information, see the section on [actor garbage collection](service-fabric-reliable-actors-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="cc4ab-122">For more information, see the section on [actor garbage collection](service-fabric-reliable-actors-lifecycle.md).</span></span>

## <a name="actor-reminders"></a><span data-ttu-id="cc4ab-123">Actor reminders</span><span class="sxs-lookup"><span data-stu-id="cc4ab-123">Actor reminders</span></span>
<span data-ttu-id="cc4ab-124">Reminders are a mechanism to trigger persistent callbacks on an actor at specified times.</span><span class="sxs-lookup"><span data-stu-id="cc4ab-124">Reminders are a mechanism to trigger persistent callbacks on an actor at specified times.</span></span> <span data-ttu-id="cc4ab-125">Their functionality is similar to timers.</span><span class="sxs-lookup"><span data-stu-id="cc4ab-125">Their functionality is similar to timers.</span></span> <span data-ttu-id="cc4ab-126">But unlike timers, reminders are triggered under all circumstances until the actor explicitly unregisters them or the actor is explicitly deleted.</span><span class="sxs-lookup"><span data-stu-id="cc4ab-126">But unlike timers, reminders are triggered under all circumstances until the actor explicitly unregisters them or the actor is explicitly deleted.</span></span> <span data-ttu-id="cc4ab-127">Specifically, reminders are triggered across actor deactivations and failovers because the Actors runtime persists information about the actor's reminders.</span><span class="sxs-lookup"><span data-stu-id="cc4ab-127">Specifically, reminders are triggered across actor deactivations and failovers because the Actors runtime persists information about the actor's reminders.</span></span>

<span data-ttu-id="cc4ab-128">To register a reminder, an actor calls the `RegisterReminderAsync` method provided on the base class, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="cc4ab-128">To register a reminder, an actor calls the `RegisterReminderAsync` method provided on the base class, as shown in the following example:</span></span>

```csharp
protected override async Task OnActivateAsync()
{
    string reminderName = "Pay cell phone bill";
    int amountInDollars = 100;

    IActorReminder reminderRegistration = await this.RegisterReminderAsync(
        reminderName,
        BitConverter.GetBytes(amountInDollars),
        TimeSpan.FromDays(3),
        TimeSpan.FromDays(1));
}
```

```Java
@Override
protected CompletableFuture onActivateAsync()
{
    String reminderName = "Pay cell phone bill";
    int amountInDollars = 100;

    ActorReminder reminderRegistration = this.registerReminderAsync(
            reminderName,
            state,
            dueTime,    //The amount of time to delay before firing the reminder
            period);    //The time interval between firing of reminders
}
```

<span data-ttu-id="cc4ab-129">In this example, `"Pay cell phone bill"` is the reminder name.</span><span class="sxs-lookup"><span data-stu-id="cc4ab-129">In this example, `"Pay cell phone bill"` is the reminder name.</span></span> <span data-ttu-id="cc4ab-130">This is a string that the actor uses to uniquely identify a reminder.</span><span class="sxs-lookup"><span data-stu-id="cc4ab-130">This is a string that the actor uses to uniquely identify a reminder.</span></span> <span data-ttu-id="cc4ab-131">`BitConverter.GetBytes(amountInDollars)`(C#) is the context that is associated with the reminder.</span><span class="sxs-lookup"><span data-stu-id="cc4ab-131">`BitConverter.GetBytes(amountInDollars)`(C#) is the context that is associated with the reminder.</span></span> <span data-ttu-id="cc4ab-132">It will be passed back to the actor as an argument to the reminder callback, i.e. `IRemindable.ReceiveReminderAsync`(C#) or `Remindable.receiveReminderAsync`(Java).</span><span class="sxs-lookup"><span data-stu-id="cc4ab-132">It will be passed back to the actor as an argument to the reminder callback, i.e. `IRemindable.ReceiveReminderAsync`(C#) or `Remindable.receiveReminderAsync`(Java).</span></span>

<span data-ttu-id="cc4ab-133">Actors that use reminders must implement the `IRemindable` interface, as shown in the example below.</span><span class="sxs-lookup"><span data-stu-id="cc4ab-133">Actors that use reminders must implement the `IRemindable` interface, as shown in the example below.</span></span>

```csharp
public class ToDoListActor : Actor, IToDoListActor, IRemindable
{
    public ToDoListActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task ReceiveReminderAsync(string reminderName, byte[] context, TimeSpan dueTime, TimeSpan period)
    {
        if (reminderName.Equals("Pay cell phone bill"))
        {
            int amountToPay = BitConverter.ToInt32(context, 0);
            System.Console.WriteLine("Please pay your cell phone bill of ${0}!", amountToPay);
        }
        return Task.FromResult(true);
    }
}
```
```Java
public class ToDoListActorImpl extends FabricActor implements ToDoListActor, Remindable
{
    public ToDoListActor(FabricActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture receiveReminderAsync(String reminderName, byte[] context, Duration dueTime, Duration period)
    {
        if (reminderName.equals("Pay cell phone bill"))
        {
            int amountToPay = ByteBuffer.wrap(context).getInt();
            System.out.println("Please pay your cell phone bill of " + amountToPay);
        }
        return CompletableFuture.completedFuture(true);
    }

```

<span data-ttu-id="cc4ab-134">When a reminder is triggered, the Reliable Actors runtime will invoke the  `ReceiveReminderAsync`(C#) or `receiveReminderAsync`(Java) method on the Actor.</span><span class="sxs-lookup"><span data-stu-id="cc4ab-134">When a reminder is triggered, the Reliable Actors runtime will invoke the  `ReceiveReminderAsync`(C#) or `receiveReminderAsync`(Java) method on the Actor.</span></span> <span data-ttu-id="cc4ab-135">An actor can register multiple reminders, and the `ReceiveReminderAsync`(C#) or `receiveReminderAsync`(Java) method is invoked when any of those reminders is triggered.</span><span class="sxs-lookup"><span data-stu-id="cc4ab-135">An actor can register multiple reminders, and the `ReceiveReminderAsync`(C#) or `receiveReminderAsync`(Java) method is invoked when any of those reminders is triggered.</span></span> <span data-ttu-id="cc4ab-136">The actor can use the reminder name that is passed in to the `ReceiveReminderAsync`(C#) or `receiveReminderAsync`(Java) method to figure out which reminder was triggered.</span><span class="sxs-lookup"><span data-stu-id="cc4ab-136">The actor can use the reminder name that is passed in to the `ReceiveReminderAsync`(C#) or `receiveReminderAsync`(Java) method to figure out which reminder was triggered.</span></span>

<span data-ttu-id="cc4ab-137">The Actors runtime saves the actor's state when the `ReceiveReminderAsync`(C#) or `receiveReminderAsync`(Java) call finishes.</span><span class="sxs-lookup"><span data-stu-id="cc4ab-137">The Actors runtime saves the actor's state when the `ReceiveReminderAsync`(C#) or `receiveReminderAsync`(Java) call finishes.</span></span> <span data-ttu-id="cc4ab-138">If an error occurs in saving the state, that actor object will be deactivated and a new instance will be activated.</span><span class="sxs-lookup"><span data-stu-id="cc4ab-138">If an error occurs in saving the state, that actor object will be deactivated and a new instance will be activated.</span></span>

<span data-ttu-id="cc4ab-139">To unregister a reminder, an actor calls the `UnregisterReminderAsync`(C#) or `unregisterReminderAsync`(Java) method, as shown in the examples below.</span><span class="sxs-lookup"><span data-stu-id="cc4ab-139">To unregister a reminder, an actor calls the `UnregisterReminderAsync`(C#) or `unregisterReminderAsync`(Java) method, as shown in the examples below.</span></span>

```csharp
IActorReminder reminder = GetReminder("Pay cell phone bill");
Task reminderUnregistration = UnregisterReminderAsync(reminder);
```
```Java
ActorReminder reminder = getReminder("Pay cell phone bill");
CompletableFuture reminderUnregistration = unregisterReminderAsync(reminder);
```

<span data-ttu-id="cc4ab-140">As shown above, the `UnregisterReminderAsync`(C#) or `unregisterReminderAsync`(Java) method accepts an `IActorReminder`(C#) or `ActorReminder`(Java) interface.</span><span class="sxs-lookup"><span data-stu-id="cc4ab-140">As shown above, the `UnregisterReminderAsync`(C#) or `unregisterReminderAsync`(Java) method accepts an `IActorReminder`(C#) or `ActorReminder`(Java) interface.</span></span> <span data-ttu-id="cc4ab-141">The actor base class supports a `GetReminder`(C#) or `getReminder`(Java) method that can be used to retrieve the `IActorReminder`(C#) or `ActorReminder`(Java) interface by passing in the reminder name.</span><span class="sxs-lookup"><span data-stu-id="cc4ab-141">The actor base class supports a `GetReminder`(C#) or `getReminder`(Java) method that can be used to retrieve the `IActorReminder`(C#) or `ActorReminder`(Java) interface by passing in the reminder name.</span></span> <span data-ttu-id="cc4ab-142">This is convenient because the actor does not need to persist the `IActorReminder`(C#) or `ActorReminder`(Java) interface that was returned from the `RegisterReminder`(C#) or `registerReminder`(Java) method call.</span><span class="sxs-lookup"><span data-stu-id="cc4ab-142">This is convenient because the actor does not need to persist the `IActorReminder`(C#) or `ActorReminder`(Java) interface that was returned from the `RegisterReminder`(C#) or `registerReminder`(Java) method call.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cc4ab-143">Next Steps</span><span class="sxs-lookup"><span data-stu-id="cc4ab-143">Next Steps</span></span>
* [<span data-ttu-id="cc4ab-144">Actor events</span><span class="sxs-lookup"><span data-stu-id="cc4ab-144">Actor events</span></span>](service-fabric-reliable-actors-events.md)
* [<span data-ttu-id="cc4ab-145">Actor reentrancy</span><span class="sxs-lookup"><span data-stu-id="cc4ab-145">Actor reentrancy</span></span>](service-fabric-reliable-actors-reentrancy.md)
* [<span data-ttu-id="cc4ab-146">Actor diagnostics and performance monitoring</span><span class="sxs-lookup"><span data-stu-id="cc4ab-146">Actor diagnostics and performance monitoring</span></span>](service-fabric-reliable-actors-diagnostics.md)
* [<span data-ttu-id="cc4ab-147">Actor API reference documentation</span><span class="sxs-lookup"><span data-stu-id="cc4ab-147">Actor API reference documentation</span></span>](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [<span data-ttu-id="cc4ab-148">C# Sample code</span><span class="sxs-lookup"><span data-stu-id="cc4ab-148">C# Sample code</span></span>](https://github.com/Azure/servicefabric-samples)
* [<span data-ttu-id="cc4ab-149">Java Sample code</span><span class="sxs-lookup"><span data-stu-id="cc4ab-149">Java Sample code</span></span>](http://github.com/Azure-Samples/service-fabric-java-getting-started)
