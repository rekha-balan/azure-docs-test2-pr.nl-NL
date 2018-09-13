---
title: Reentrancy in actor-based Azure microservices | Microsoft Docs
description: Introduction to reentrancy for Service Fabric Reliable Actors
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: amanbha
ms.assetid: be23464a-0eea-4eca-ae5a-2e1b650d365e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/10/2017
ms.author: vturecek
ms.openlocfilehash: 8fddc4fb46f2b71133053ac06961cae2cb533e6d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44669107"
---
# <a name="reliable-actors-reentrancy"></a><span data-ttu-id="4e5b3-103">Reliable Actors reentrancy</span><span class="sxs-lookup"><span data-stu-id="4e5b3-103">Reliable Actors reentrancy</span></span>
<span data-ttu-id="4e5b3-104">The Reliable Actors runtime, by default, allows logical call context-based reentrancy.</span><span class="sxs-lookup"><span data-stu-id="4e5b3-104">The Reliable Actors runtime, by default, allows logical call context-based reentrancy.</span></span> <span data-ttu-id="4e5b3-105">This allows for actors to be reentrant if they are in the same call context chain.</span><span class="sxs-lookup"><span data-stu-id="4e5b3-105">This allows for actors to be reentrant if they are in the same call context chain.</span></span> <span data-ttu-id="4e5b3-106">For example, Actor A sends a message to Actor B, who sends a message to Actor C. As part of the message processing, if Actor C calls Actor A, the message is reentrant, so it will be allowed.</span><span class="sxs-lookup"><span data-stu-id="4e5b3-106">For example, Actor A sends a message to Actor B, who sends a message to Actor C. As part of the message processing, if Actor C calls Actor A, the message is reentrant, so it will be allowed.</span></span> <span data-ttu-id="4e5b3-107">Any other messages that are part of a different call context will be blocked on Actor A until it finishes processing.</span><span class="sxs-lookup"><span data-stu-id="4e5b3-107">Any other messages that are part of a different call context will be blocked on Actor A until it finishes processing.</span></span>

<span data-ttu-id="4e5b3-108">There are two options available for actor reentrancy defined in the `ActorReentrancyMode` enum:</span><span class="sxs-lookup"><span data-stu-id="4e5b3-108">There are two options available for actor reentrancy defined in the `ActorReentrancyMode` enum:</span></span>

* <span data-ttu-id="4e5b3-109">`LogicalCallContext` (default behavior)</span><span class="sxs-lookup"><span data-stu-id="4e5b3-109">`LogicalCallContext` (default behavior)</span></span>
* <span data-ttu-id="4e5b3-110">`Disallowed` - disables reentrancy</span><span class="sxs-lookup"><span data-stu-id="4e5b3-110">`Disallowed` - disables reentrancy</span></span>

```csharp
public enum ActorReentrancyMode
{
    LogicalCallContext = 1,
    Disallowed = 2
}
```
```Java
public enum ActorReentrancyMode
{
    LogicalCallContext(1),
    Disallowed(2)
}
```
<span data-ttu-id="4e5b3-111">Reentrancy can be configured in an `ActorService`'s settings during registration.</span><span class="sxs-lookup"><span data-stu-id="4e5b3-111">Reentrancy can be configured in an `ActorService`'s settings during registration.</span></span> <span data-ttu-id="4e5b3-112">The setting applies to all actor instances created in the actor service.</span><span class="sxs-lookup"><span data-stu-id="4e5b3-112">The setting applies to all actor instances created in the actor service.</span></span>

<span data-ttu-id="4e5b3-113">The following example shows an actor service that sets the reentrancy mode to `ActorReentrancyMode.Disallowed`.</span><span class="sxs-lookup"><span data-stu-id="4e5b3-113">The following example shows an actor service that sets the reentrancy mode to `ActorReentrancyMode.Disallowed`.</span></span> <span data-ttu-id="4e5b3-114">In this case, if an actor sends a reentrant message to another actor, an exception of type `FabricException` will be thrown.</span><span class="sxs-lookup"><span data-stu-id="4e5b3-114">In this case, if an actor sends a reentrant message to another actor, an exception of type `FabricException` will be thrown.</span></span>

```csharp
static class Program
{
    static void Main()
    {
        try
        {
            ActorRuntime.RegisterActorAsync<Actor1>(
                (context, actorType) => new ActorService(
                    context,
                    actorType, () => new Actor1(),
                    settings: new ActorServiceSettings()
                    {
                        ActorConcurrencySettings = new ActorConcurrencySettings()
                        {
                            ReentrancyMode = ActorReentrancyMode.Disallowed
                        }
                    }))
                .GetAwaiter().GetResult();

            Thread.Sleep(Timeout.Infinite);
        }
        catch (Exception e)
        {
            ActorEventSource.Current.ActorHostInitializationFailed(e.ToString());
            throw;
        }
    }
}
```
```Java
static class Program
{
    static void Main()
    {
        try
        {
            ActorConcurrencySettings actorConcurrencySettings = new ActorConcurrencySettings();
            actorConcurrencySettings.setReentrancyMode(ActorReentrancyMode.Disallowed);

            ActorServiceSettings actorServiceSettings = new ActorServiceSettings();
            actorServiceSettings.setActorConcurrencySettings(actorConcurrencySettings);

            ActorRuntime.registerActorAsync(
                Actor1.getClass(),
                (context, actorType) -> new FabricActorService(
                    context,
                    actorType, () -> new Actor1(),
                    null,
                    stateProvider,
                    actorServiceSettings, timeout);

            Thread.sleep(Long.MAX_VALUE);
        }
        catch (Exception e)
        {
            throw e;
        }
    }
}
```


## <a name="next-steps"></a><span data-ttu-id="4e5b3-115">Next steps</span><span class="sxs-lookup"><span data-stu-id="4e5b3-115">Next steps</span></span>
* [<span data-ttu-id="4e5b3-116">Actor diagnostics and performance monitoring</span><span class="sxs-lookup"><span data-stu-id="4e5b3-116">Actor diagnostics and performance monitoring</span></span>](service-fabric-reliable-actors-diagnostics.md)
* [<span data-ttu-id="4e5b3-117">Actor API reference documentation</span><span class="sxs-lookup"><span data-stu-id="4e5b3-117">Actor API reference documentation</span></span>](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [<span data-ttu-id="4e5b3-118">C# Sample code</span><span class="sxs-lookup"><span data-stu-id="4e5b3-118">C# Sample code</span></span>](https://github.com/Azure/servicefabric-samples)
* [<span data-ttu-id="4e5b3-119">Java Sample code</span><span class="sxs-lookup"><span data-stu-id="4e5b3-119">Java Sample code</span></span>](http://github.com/Azure-Samples/service-fabric-java-getting-started)
