---
title: Reliable Actors notes on actor type serialization | Microsoft Docs
description: Discusses basic requirements for defining serializable classes that can be used to define Service Fabric Reliable Actors states and interfaces
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: ''
ms.assetid: 6e50e4dc-969a-4a1c-b36c-b292d964c7e3
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/10/2017
ms.author: vturecek
ms.openlocfilehash: 1a27c94f5a64ec33f1ac5357d8968814537d0664
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556353"
---
# <a name="notes-on-service-fabric-reliable-actors-type-serialization"></a><span data-ttu-id="85371-103">Notes on Service Fabric Reliable Actors type serialization</span><span class="sxs-lookup"><span data-stu-id="85371-103">Notes on Service Fabric Reliable Actors type serialization</span></span>
<span data-ttu-id="85371-104">The arguments of all methods, result types of the tasks returned by each method in an actor interface, and objects stored in an actor's state manager must be [data contract serializable](https://msdn.microsoft.com/library/ms731923.aspx).</span><span class="sxs-lookup"><span data-stu-id="85371-104">The arguments of all methods, result types of the tasks returned by each method in an actor interface, and objects stored in an actor's state manager must be [data contract serializable](https://msdn.microsoft.com/library/ms731923.aspx).</span></span> <span data-ttu-id="85371-105">This also applies to the arguments of the methods defined in [actor event interfaces](service-fabric-reliable-actors-events.md).</span><span class="sxs-lookup"><span data-stu-id="85371-105">This also applies to the arguments of the methods defined in [actor event interfaces](service-fabric-reliable-actors-events.md).</span></span> <span data-ttu-id="85371-106">(Actor event interface methods always return void.)</span><span class="sxs-lookup"><span data-stu-id="85371-106">(Actor event interface methods always return void.)</span></span>

## <a name="custom-data-types"></a><span data-ttu-id="85371-107">Custom data types</span><span class="sxs-lookup"><span data-stu-id="85371-107">Custom data types</span></span>
<span data-ttu-id="85371-108">In this example, the following actor interface defines a method that returns a custom data type called `VoicemailBox`:</span><span class="sxs-lookup"><span data-stu-id="85371-108">In this example, the following actor interface defines a method that returns a custom data type called `VoicemailBox`:</span></span>

```csharp
public interface IVoiceMailBoxActor : IActor
{
    Task<VoicemailBox> GetMailBoxAsync();
}
```

```Java
public interface VoiceMailBoxActor extends Actor
{
    CompletableFuture<VoicemailBox> getMailBoxAsync();
}
```

<span data-ttu-id="85371-109">The interface is implemented by an actor that uses the state manager to store a `VoicemailBox` object:</span><span class="sxs-lookup"><span data-stu-id="85371-109">The interface is implemented by an actor that uses the state manager to store a `VoicemailBox` object:</span></span>

```csharp
[StatePersistence(StatePersistence.Persisted)]
public class VoiceMailBoxActor : Actor, IVoicemailBoxActor
{
    public VoiceMailBoxActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task<VoicemailBox> GetMailboxAsync()
    {
        return this.StateManager.GetStateAsync<VoicemailBox>("Mailbox");
    }
}

```

```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
public class VoiceMailBoxActorImpl extends FabricActor implements VoicemailBoxActor
{
    public VoiceMailBoxActorImpl(ActorService actorService, ActorId actorId)
    {
         super(actorService, actorId);
    }

    public CompletableFuture<VoicemailBox> getMailBoxAsync()
    {
         return this.stateManager().getStateAsync("Mailbox");
    }
}

```

<span data-ttu-id="85371-110">In this example, the `VoicemailBox` object is serialized when:</span><span class="sxs-lookup"><span data-stu-id="85371-110">In this example, the `VoicemailBox` object is serialized when:</span></span>

* <span data-ttu-id="85371-111">The object is transmitted between an actor instance and a caller.</span><span class="sxs-lookup"><span data-stu-id="85371-111">The object is transmitted between an actor instance and a caller.</span></span>
* <span data-ttu-id="85371-112">The object is saved in the state manager where it is persisted to disk and replicated to other nodes.</span><span class="sxs-lookup"><span data-stu-id="85371-112">The object is saved in the state manager where it is persisted to disk and replicated to other nodes.</span></span>

<span data-ttu-id="85371-113">The Reliable Actor framework uses DataContract serialization.</span><span class="sxs-lookup"><span data-stu-id="85371-113">The Reliable Actor framework uses DataContract serialization.</span></span> <span data-ttu-id="85371-114">Therefore, the custom data objects and their members must be annotated with the **DataContract** and **DataMember** attributes, respectively.</span><span class="sxs-lookup"><span data-stu-id="85371-114">Therefore, the custom data objects and their members must be annotated with the **DataContract** and **DataMember** attributes, respectively.</span></span>

```csharp
[DataContract]
public class Voicemail
{
    [DataMember]
    public Guid Id { get; set; }

    [DataMember]
    public string Message { get; set; }

    [DataMember]
    public DateTime ReceivedAt { get; set; }
}
```
```Java
public class Voicemail implements Serializable
{
    private static final long serialVersionUID = 42L;

    private UUID id;                    //getUUID() and setUUID()

    private String message;             //getMessage() and setMessage()

    private GregorianCalendar receivedAt; //getReceivedAt() and setReceivedAt()
}
```


```csharp
[DataContract]
public class VoicemailBox
{
    public VoicemailBox()
    {
        this.MessageList = new List<Voicemail>();
    }

    [DataMember]
    public List<Voicemail> MessageList { get; set; }

    [DataMember]
    public string Greeting { get; set; }
}
```
```Java
public class VoicemailBox implements Serializable
{
    static final long serialVersionUID = 42L;
    
    public VoicemailBox()
    {
        this.messageList = new ArrayList<Voicemail>();
    }

    private List<Voicemail> messageList;   //getMessageList() and setMessageList()

    private String greeting;               //getGreeting() and setGreeting()
}
```


## <a name="next-steps"></a><span data-ttu-id="85371-115">Next steps</span><span class="sxs-lookup"><span data-stu-id="85371-115">Next steps</span></span>
* [<span data-ttu-id="85371-116">Actor lifecycle and garbage collection</span><span class="sxs-lookup"><span data-stu-id="85371-116">Actor lifecycle and garbage collection</span></span>](service-fabric-reliable-actors-lifecycle.md)
* [<span data-ttu-id="85371-117">Actor timers and reminders</span><span class="sxs-lookup"><span data-stu-id="85371-117">Actor timers and reminders</span></span>](service-fabric-reliable-actors-timers-reminders.md)
* [<span data-ttu-id="85371-118">Actor events</span><span class="sxs-lookup"><span data-stu-id="85371-118">Actor events</span></span>](service-fabric-reliable-actors-events.md)
* [<span data-ttu-id="85371-119">Actor reentrancy</span><span class="sxs-lookup"><span data-stu-id="85371-119">Actor reentrancy</span></span>](service-fabric-reliable-actors-reentrancy.md)
* [<span data-ttu-id="85371-120">Actor polymorphism and object-oriented design patterns</span><span class="sxs-lookup"><span data-stu-id="85371-120">Actor polymorphism and object-oriented design patterns</span></span>](service-fabric-reliable-actors-polymorphism.md)
* [<span data-ttu-id="85371-121">Actor diagnostics and performance monitoring</span><span class="sxs-lookup"><span data-stu-id="85371-121">Actor diagnostics and performance monitoring</span></span>](service-fabric-reliable-actors-diagnostics.md)
