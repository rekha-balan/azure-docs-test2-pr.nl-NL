---
title: Events in actor-based Azure microservices| Microsoft Docs
description: Introduction to events for Service Fabric Reliable Actors.
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: ''
ms.assetid: aa01b0f7-8f88-403a-bfe1-5aba00312c24
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/02/2017
ms.author: amanbha
ms.openlocfilehash: eef9c1ab69153d3a2e4d8e7363108703819823a7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551136"
---
# <a name="actor-events"></a><span data-ttu-id="720e0-103">Actor events</span><span class="sxs-lookup"><span data-stu-id="720e0-103">Actor events</span></span>
<span data-ttu-id="720e0-104">Actor events provide a way to send best-effort notifications from the actor to the clients.</span><span class="sxs-lookup"><span data-stu-id="720e0-104">Actor events provide a way to send best-effort notifications from the actor to the clients.</span></span> <span data-ttu-id="720e0-105">Actor events are designed for actor-to-client communication and should not be used for actor-to-actor communication.</span><span class="sxs-lookup"><span data-stu-id="720e0-105">Actor events are designed for actor-to-client communication and should not be used for actor-to-actor communication.</span></span>

<span data-ttu-id="720e0-106">The following code snippets show how to use actor events in your application.</span><span class="sxs-lookup"><span data-stu-id="720e0-106">The following code snippets show how to use actor events in your application.</span></span>

<span data-ttu-id="720e0-107">Define an interface that describes the events published by the actor.</span><span class="sxs-lookup"><span data-stu-id="720e0-107">Define an interface that describes the events published by the actor.</span></span> <span data-ttu-id="720e0-108">This interface must be derived from the `IActorEvents` interface.</span><span class="sxs-lookup"><span data-stu-id="720e0-108">This interface must be derived from the `IActorEvents` interface.</span></span> <span data-ttu-id="720e0-109">The arguments of the methods must be [data contract serializable](service-fabric-reliable-actors-notes-on-actor-type-serialization.md).</span><span class="sxs-lookup"><span data-stu-id="720e0-109">The arguments of the methods must be [data contract serializable](service-fabric-reliable-actors-notes-on-actor-type-serialization.md).</span></span> <span data-ttu-id="720e0-110">The methods must return void, as event notifications are one way and best effort.</span><span class="sxs-lookup"><span data-stu-id="720e0-110">The methods must return void, as event notifications are one way and best effort.</span></span>

```csharp
public interface IGameEvents : IActorEvents
{
    void GameScoreUpdated(Guid gameId, string currentScore);
}
```
```Java
public interface GameEvents implements ActorEvents
{
    void gameScoreUpdated(UUID gameId, String currentScore);
}
```
<span data-ttu-id="720e0-111">Declare the events published by the actor in the actor interface.</span><span class="sxs-lookup"><span data-stu-id="720e0-111">Declare the events published by the actor in the actor interface.</span></span>

```csharp
public interface IGameActor : IActor, IActorEventPublisher<IGameEvents>
{
    Task UpdateGameStatus(GameStatus status);

    Task<string> GetGameScore();
}
```
```Java
public interface GameActor extends Actor, ActorEventPublisherE<GameEvents>
{
    CompletableFuture<?> updateGameStatus(GameStatus status);

    CompletableFuture<String> getGameScore();
}
```
<span data-ttu-id="720e0-112">On the client side, implement the event handler.</span><span class="sxs-lookup"><span data-stu-id="720e0-112">On the client side, implement the event handler.</span></span>

```csharp
class GameEventsHandler : IGameEvents
{
    public void GameScoreUpdated(Guid gameId, string currentScore)
    {
        Console.WriteLine(@"Updates: Game: {0}, Score: {1}", gameId, currentScore);
    }
}
```

```Java
class GameEventsHandler implements GameEvents {
    public void gameScoreUpdated(UUID gameId, String currentScore)
    {
        System.out.println("Updates: Game: "+gameId+" ,Score: "+currentScore);
    }
}
```

<span data-ttu-id="720e0-113">On the client, create a proxy to the actor that publishes the event and subscribe to its events.</span><span class="sxs-lookup"><span data-stu-id="720e0-113">On the client, create a proxy to the actor that publishes the event and subscribe to its events.</span></span>

```csharp
var proxy = ActorProxy.Create<IGameActor>(
                    new ActorId(Guid.Parse(arg)), ApplicationName);

await proxy.SubscribeAsync<IGameEvents>(new GameEventsHandler());
```

```Java
GameActor actorProxy = ActorProxyBase.create<GameActor>(GameActor.class, new ActorId(UUID.fromString(args)));

return ActorProxyEventUtility.subscribeAsync(actorProxy, new GameEventsHandler());
```

<span data-ttu-id="720e0-114">In the event of failovers, the actor may fail over to a different process or node.</span><span class="sxs-lookup"><span data-stu-id="720e0-114">In the event of failovers, the actor may fail over to a different process or node.</span></span> <span data-ttu-id="720e0-115">The actor proxy manages the active subscriptions and automatically re-subscribes them.</span><span class="sxs-lookup"><span data-stu-id="720e0-115">The actor proxy manages the active subscriptions and automatically re-subscribes them.</span></span> <span data-ttu-id="720e0-116">You can control the re-subscription interval through the `ActorProxyEventExtensions.SubscribeAsync<TEvent>` API.</span><span class="sxs-lookup"><span data-stu-id="720e0-116">You can control the re-subscription interval through the `ActorProxyEventExtensions.SubscribeAsync<TEvent>` API.</span></span> <span data-ttu-id="720e0-117">To unsubscribe, use the `ActorProxyEventExtensions.UnsubscribeAsync<TEvent>` API.</span><span class="sxs-lookup"><span data-stu-id="720e0-117">To unsubscribe, use the `ActorProxyEventExtensions.UnsubscribeAsync<TEvent>` API.</span></span>

<span data-ttu-id="720e0-118">On the actor, simply publish the events as they happen.</span><span class="sxs-lookup"><span data-stu-id="720e0-118">On the actor, simply publish the events as they happen.</span></span> <span data-ttu-id="720e0-119">If there are subscribers to the event, the Actors runtime will send them the notification.</span><span class="sxs-lookup"><span data-stu-id="720e0-119">If there are subscribers to the event, the Actors runtime will send them the notification.</span></span>

```csharp
var ev = GetEvent<IGameEvents>();
ev.GameScoreUpdated(Id.GetGuidId(), score);
```
```Java
GameEvents event = getEvent<GameEvents>(GameEvents.class);
event.gameScoreUpdated(Id.getUUIDId(), score);
```


## <a name="next-steps"></a><span data-ttu-id="720e0-120">Next steps</span><span class="sxs-lookup"><span data-stu-id="720e0-120">Next steps</span></span>
* [<span data-ttu-id="720e0-121">Actor reentrancy</span><span class="sxs-lookup"><span data-stu-id="720e0-121">Actor reentrancy</span></span>](service-fabric-reliable-actors-reentrancy.md)
* [<span data-ttu-id="720e0-122">Actor diagnostics and performance monitoring</span><span class="sxs-lookup"><span data-stu-id="720e0-122">Actor diagnostics and performance monitoring</span></span>](service-fabric-reliable-actors-diagnostics.md)
* [<span data-ttu-id="720e0-123">Actor API reference documentation</span><span class="sxs-lookup"><span data-stu-id="720e0-123">Actor API reference documentation</span></span>](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [<span data-ttu-id="720e0-124">C# Sample code</span><span class="sxs-lookup"><span data-stu-id="720e0-124">C# Sample code</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="720e0-125">C# .NET Core Sample code</span><span class="sxs-lookup"><span data-stu-id="720e0-125">C# .NET Core Sample code</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-core-getting-started)
* [<span data-ttu-id="720e0-126">Java Sample code</span><span class="sxs-lookup"><span data-stu-id="720e0-126">Java Sample code</span></span>](http://github.com/Azure-Samples/service-fabric-java-getting-started)
