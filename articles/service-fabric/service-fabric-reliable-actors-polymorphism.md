---
title: Polymorphism in the Reliable Actors framework | Microsoft Docs
description: Build hierarchies of .NET interfaces and types in the Reliable Actors framework to reuse functionality and API definitions.
services: service-fabric
documentationcenter: .net
author: seanmck
manager: timlt
editor: vturecek
ms.assetid: ef0eeff6-32b7-410d-ac69-87cba8b8fd46
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/28/2017
ms.author: seanmck
ms.openlocfilehash: b399f4f4e6381ac2652ab8c06f1a0aea4b8bcfca
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556019"
---
# <a name="polymorphism-in-the-reliable-actors-framework"></a><span data-ttu-id="0c119-103">Polymorphism in the Reliable Actors framework</span><span class="sxs-lookup"><span data-stu-id="0c119-103">Polymorphism in the Reliable Actors framework</span></span>
<span data-ttu-id="0c119-104">The Reliable Actors framework allows you to build actors using many of the same techniques that you would use in object-oriented design.</span><span class="sxs-lookup"><span data-stu-id="0c119-104">The Reliable Actors framework allows you to build actors using many of the same techniques that you would use in object-oriented design.</span></span> <span data-ttu-id="0c119-105">One of those techniques is polymorphism, which allows types and interfaces to inherit from more generalized parents.</span><span class="sxs-lookup"><span data-stu-id="0c119-105">One of those techniques is polymorphism, which allows types and interfaces to inherit from more generalized parents.</span></span> <span data-ttu-id="0c119-106">Inheritance in the Reliable Actors framework generally follows the .NET model with a few additional constraints.</span><span class="sxs-lookup"><span data-stu-id="0c119-106">Inheritance in the Reliable Actors framework generally follows the .NET model with a few additional constraints.</span></span> <span data-ttu-id="0c119-107">In case of Java/Linux, it follows the Java model.</span><span class="sxs-lookup"><span data-stu-id="0c119-107">In case of Java/Linux, it follows the Java model.</span></span>

## <a name="interfaces"></a><span data-ttu-id="0c119-108">Interfaces</span><span class="sxs-lookup"><span data-stu-id="0c119-108">Interfaces</span></span>
<span data-ttu-id="0c119-109">The Reliable Actors framework requires you to define at least one interface to be implemented by your actor type.</span><span class="sxs-lookup"><span data-stu-id="0c119-109">The Reliable Actors framework requires you to define at least one interface to be implemented by your actor type.</span></span> <span data-ttu-id="0c119-110">This interface is used to generate a proxy class that can be used by clients to communicate with your actors.</span><span class="sxs-lookup"><span data-stu-id="0c119-110">This interface is used to generate a proxy class that can be used by clients to communicate with your actors.</span></span> <span data-ttu-id="0c119-111">Interfaces can inherit from other interfaces as long as every interface that is implemented by an actor type and all of its parents ultimately derive from IActor(C#) or Actor(Java) .</span><span class="sxs-lookup"><span data-stu-id="0c119-111">Interfaces can inherit from other interfaces as long as every interface that is implemented by an actor type and all of its parents ultimately derive from IActor(C#) or Actor(Java) .</span></span> <span data-ttu-id="0c119-112">IActor(C#) and Actor(Java) are the platform-defined base interfaces for actors in the frameworks .NET and Java respectively.</span><span class="sxs-lookup"><span data-stu-id="0c119-112">IActor(C#) and Actor(Java) are the platform-defined base interfaces for actors in the frameworks .NET and Java respectively.</span></span> <span data-ttu-id="0c119-113">Thus, the classic polymorphism example using shapes might look something like this:</span><span class="sxs-lookup"><span data-stu-id="0c119-113">Thus, the classic polymorphism example using shapes might look something like this:</span></span>

![Interface hierarchy for shape actors][shapes-interface-hierarchy]

## <a name="types"></a><span data-ttu-id="0c119-115">Types</span><span class="sxs-lookup"><span data-stu-id="0c119-115">Types</span></span>
<span data-ttu-id="0c119-116">You can also create a hierarchy of actor types, which are derived from the base Actor class that is provided by the platform.</span><span class="sxs-lookup"><span data-stu-id="0c119-116">You can also create a hierarchy of actor types, which are derived from the base Actor class that is provided by the platform.</span></span> <span data-ttu-id="0c119-117">In the case of shapes, you might have a base `Shape`(C#) or `ShapeImpl`(Java) type:</span><span class="sxs-lookup"><span data-stu-id="0c119-117">In the case of shapes, you might have a base `Shape`(C#) or `ShapeImpl`(Java) type:</span></span>

```csharp
public abstract class Shape : Actor, IShape
{
    public abstract Task<int> GetVerticeCount();

    public abstract Task<double> GetAreaAsync();
}
```
```Java
public abstract class ShapeImpl extends FabricActor implements Shape
{
    public abstract CompletableFuture<int> getVerticeCount();

    public abstract CompletableFuture<double> getAreaAsync();
}
```

<span data-ttu-id="0c119-118">Subtypes of `Shape`(C#) or `ShapeImpl`(Java) can override methods from the base.</span><span class="sxs-lookup"><span data-stu-id="0c119-118">Subtypes of `Shape`(C#) or `ShapeImpl`(Java) can override methods from the base.</span></span>

```csharp
[ActorService(Name = "Circle")]
[StatePersistence(StatePersistence.Persisted)]
public class Circle : Shape, ICircle
{
    public override Task<int> GetVerticeCount()
    {
        return Task.FromResult(0);
    }

    public override async Task<double> GetAreaAsync()
    {
        CircleState state = await this.StateManager.GetStateAsync<CircleState>("circle");

        return Math.PI *
            state.Radius *
            state.Radius;
    }
}
```
```Java
@ActorServiceAttribute(name = "Circle")
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
public class Circle extends ShapeImpl implements Circle
{
    @Override
    public CompletableFuture<Integer> getVerticeCount()
    {
        return CompletableFuture.completedFuture(0);
    }

    @Override
    public CompletableFuture<Double> getAreaAsync()
    {
        return (this.stateManager().getStateAsync<CircleState>("circle").thenApply(state->{
          return Math.PI * state.radius * state.radius;
        }));
    }
}
```

<span data-ttu-id="0c119-119">Note the `ActorService` attribute on the actor type.</span><span class="sxs-lookup"><span data-stu-id="0c119-119">Note the `ActorService` attribute on the actor type.</span></span> <span data-ttu-id="0c119-120">This attribute tells the Reliable Actor framework that it should automatically create a service for hosting actors of this type.</span><span class="sxs-lookup"><span data-stu-id="0c119-120">This attribute tells the Reliable Actor framework that it should automatically create a service for hosting actors of this type.</span></span> <span data-ttu-id="0c119-121">In some cases, you may wish to create a base type that is solely intended for sharing functionality with subtypes and will never be used to instantiate concrete actors.</span><span class="sxs-lookup"><span data-stu-id="0c119-121">In some cases, you may wish to create a base type that is solely intended for sharing functionality with subtypes and will never be used to instantiate concrete actors.</span></span> <span data-ttu-id="0c119-122">In those cases, you should use the `abstract` keyword to indicate that you will never create an actor based on that type.</span><span class="sxs-lookup"><span data-stu-id="0c119-122">In those cases, you should use the `abstract` keyword to indicate that you will never create an actor based on that type.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0c119-123">Next steps</span><span class="sxs-lookup"><span data-stu-id="0c119-123">Next steps</span></span>
* <span data-ttu-id="0c119-124">See [how the Reliable Actors framework leverages the Service Fabric platform](service-fabric-reliable-actors-platform.md) to provide reliability, scalability, and consistent state.</span><span class="sxs-lookup"><span data-stu-id="0c119-124">See [how the Reliable Actors framework leverages the Service Fabric platform](service-fabric-reliable-actors-platform.md) to provide reliability, scalability, and consistent state.</span></span>
* <span data-ttu-id="0c119-125">Learn about the [actor lifecycle](service-fabric-reliable-actors-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="0c119-125">Learn about the [actor lifecycle](service-fabric-reliable-actors-lifecycle.md).</span></span>

<!-- Image references -->

[shapes-interface-hierarchy]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-reliable-actors-polymorphism/Shapes-Interface-Hierarchy.png
