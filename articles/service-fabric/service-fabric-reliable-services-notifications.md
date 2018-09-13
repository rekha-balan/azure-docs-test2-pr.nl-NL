---
title: Reliable Services notifications | Microsoft Docs
description: Conceptual documentation for Service Fabric Reliable Services notifications
services: service-fabric
documentationcenter: .net
author: mcoskun
manager: timlt
editor: masnider,vturecek
ms.assetid: cdc918dd-5e81-49c8-a03d-7ddcd12a9a76
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 6/29/2017
ms.author: mcoskun
ms.openlocfilehash: 9f37b9a7e877437f91e209ad8607b8568ac9ed72
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44808163"
---
# <a name="reliable-services-notifications"></a><span data-ttu-id="3f551-103">Reliable Services notifications</span><span class="sxs-lookup"><span data-stu-id="3f551-103">Reliable Services notifications</span></span>
<span data-ttu-id="3f551-104">Notifications allow clients to track the changes that are being made to an object that they're interested in.</span><span class="sxs-lookup"><span data-stu-id="3f551-104">Notifications allow clients to track the changes that are being made to an object that they're interested in.</span></span> <span data-ttu-id="3f551-105">Two types of objects support notifications: *Reliable State Manager* and *Reliable Dictionary*.</span><span class="sxs-lookup"><span data-stu-id="3f551-105">Two types of objects support notifications: *Reliable State Manager* and *Reliable Dictionary*.</span></span>

<span data-ttu-id="3f551-106">Common reasons for using notifications are:</span><span class="sxs-lookup"><span data-stu-id="3f551-106">Common reasons for using notifications are:</span></span>

* <span data-ttu-id="3f551-107">Building materialized views, such as secondary indexes or aggregated filtered views of the replica's state.</span><span class="sxs-lookup"><span data-stu-id="3f551-107">Building materialized views, such as secondary indexes or aggregated filtered views of the replica's state.</span></span> <span data-ttu-id="3f551-108">An example is a sorted index of all keys in Reliable Dictionary.</span><span class="sxs-lookup"><span data-stu-id="3f551-108">An example is a sorted index of all keys in Reliable Dictionary.</span></span>
* <span data-ttu-id="3f551-109">Sending monitoring data, such as the number of users added in the last hour.</span><span class="sxs-lookup"><span data-stu-id="3f551-109">Sending monitoring data, such as the number of users added in the last hour.</span></span>

<span data-ttu-id="3f551-110">Notifications are fired as part of applying operations.</span><span class="sxs-lookup"><span data-stu-id="3f551-110">Notifications are fired as part of applying operations.</span></span> <span data-ttu-id="3f551-111">Because of that, notifications should be handled as fast as possible, and synchronous events shouldn't include any expensive operations.</span><span class="sxs-lookup"><span data-stu-id="3f551-111">Because of that, notifications should be handled as fast as possible, and synchronous events shouldn't include any expensive operations.</span></span>

## <a name="reliable-state-manager-notifications"></a><span data-ttu-id="3f551-112">Reliable State Manager notifications</span><span class="sxs-lookup"><span data-stu-id="3f551-112">Reliable State Manager notifications</span></span>
<span data-ttu-id="3f551-113">Reliable State Manager provides notifications for the following events:</span><span class="sxs-lookup"><span data-stu-id="3f551-113">Reliable State Manager provides notifications for the following events:</span></span>

* <span data-ttu-id="3f551-114">Transaction</span><span class="sxs-lookup"><span data-stu-id="3f551-114">Transaction</span></span>
  * <span data-ttu-id="3f551-115">Commit</span><span class="sxs-lookup"><span data-stu-id="3f551-115">Commit</span></span>
* <span data-ttu-id="3f551-116">State manager</span><span class="sxs-lookup"><span data-stu-id="3f551-116">State manager</span></span>
  * <span data-ttu-id="3f551-117">Rebuild</span><span class="sxs-lookup"><span data-stu-id="3f551-117">Rebuild</span></span>
  * <span data-ttu-id="3f551-118">Addition of a reliable state</span><span class="sxs-lookup"><span data-stu-id="3f551-118">Addition of a reliable state</span></span>
  * <span data-ttu-id="3f551-119">Removal of a reliable state</span><span class="sxs-lookup"><span data-stu-id="3f551-119">Removal of a reliable state</span></span>

<span data-ttu-id="3f551-120">Reliable State Manager tracks the current inflight transactions.</span><span class="sxs-lookup"><span data-stu-id="3f551-120">Reliable State Manager tracks the current inflight transactions.</span></span> <span data-ttu-id="3f551-121">The only change in transaction state that causes a notification to be fired is a transaction being committed.</span><span class="sxs-lookup"><span data-stu-id="3f551-121">The only change in transaction state that causes a notification to be fired is a transaction being committed.</span></span>

<span data-ttu-id="3f551-122">Reliable State Manager maintains a collection of reliable states like Reliable Dictionary and Reliable Queue.</span><span class="sxs-lookup"><span data-stu-id="3f551-122">Reliable State Manager maintains a collection of reliable states like Reliable Dictionary and Reliable Queue.</span></span> <span data-ttu-id="3f551-123">Reliable State Manager fires notifications when this collection changes: a reliable state is added or removed, or the entire collection is rebuilt.</span><span class="sxs-lookup"><span data-stu-id="3f551-123">Reliable State Manager fires notifications when this collection changes: a reliable state is added or removed, or the entire collection is rebuilt.</span></span>
<span data-ttu-id="3f551-124">The Reliable State Manager collection is rebuilt in three cases:</span><span class="sxs-lookup"><span data-stu-id="3f551-124">The Reliable State Manager collection is rebuilt in three cases:</span></span>

* <span data-ttu-id="3f551-125">Recovery: When a replica starts, it recovers its previous state from the disk.</span><span class="sxs-lookup"><span data-stu-id="3f551-125">Recovery: When a replica starts, it recovers its previous state from the disk.</span></span> <span data-ttu-id="3f551-126">At the end of recovery, it uses **NotifyStateManagerChangedEventArgs** to fire an event that contains the set of recovered reliable states.</span><span class="sxs-lookup"><span data-stu-id="3f551-126">At the end of recovery, it uses **NotifyStateManagerChangedEventArgs** to fire an event that contains the set of recovered reliable states.</span></span>
* <span data-ttu-id="3f551-127">Full copy: Before a replica can join the configuration set, it has to be built.</span><span class="sxs-lookup"><span data-stu-id="3f551-127">Full copy: Before a replica can join the configuration set, it has to be built.</span></span> <span data-ttu-id="3f551-128">Sometimes, this requires a full copy of Reliable State Manager's state from the primary replica to be applied to the idle secondary replica.</span><span class="sxs-lookup"><span data-stu-id="3f551-128">Sometimes, this requires a full copy of Reliable State Manager's state from the primary replica to be applied to the idle secondary replica.</span></span> <span data-ttu-id="3f551-129">Reliable State Manager on the secondary replica uses **NotifyStateManagerChangedEventArgs** to fire an event that contains the set of reliable states that it acquired from the primary replica.</span><span class="sxs-lookup"><span data-stu-id="3f551-129">Reliable State Manager on the secondary replica uses **NotifyStateManagerChangedEventArgs** to fire an event that contains the set of reliable states that it acquired from the primary replica.</span></span>
* <span data-ttu-id="3f551-130">Restore: In disaster recovery scenarios, the replica's state can be restored from a backup via **RestoreAsync**.</span><span class="sxs-lookup"><span data-stu-id="3f551-130">Restore: In disaster recovery scenarios, the replica's state can be restored from a backup via **RestoreAsync**.</span></span> <span data-ttu-id="3f551-131">In such cases, Reliable State Manager on the primary replica uses **NotifyStateManagerChangedEventArgs** to fire an event that contains the set of reliable states that it restored from the backup.</span><span class="sxs-lookup"><span data-stu-id="3f551-131">In such cases, Reliable State Manager on the primary replica uses **NotifyStateManagerChangedEventArgs** to fire an event that contains the set of reliable states that it restored from the backup.</span></span>

<span data-ttu-id="3f551-132">To register for transaction notifications and/or state manager notifications, you need to register with the **TransactionChanged** or **StateManagerChanged** events on Reliable State Manager.</span><span class="sxs-lookup"><span data-stu-id="3f551-132">To register for transaction notifications and/or state manager notifications, you need to register with the **TransactionChanged** or **StateManagerChanged** events on Reliable State Manager.</span></span> <span data-ttu-id="3f551-133">A common place to register with these event handlers is the constructor of your stateful service.</span><span class="sxs-lookup"><span data-stu-id="3f551-133">A common place to register with these event handlers is the constructor of your stateful service.</span></span> <span data-ttu-id="3f551-134">When you register on the constructor, you won't miss any notification that's caused by a change during the lifetime of **IReliableStateManager**.</span><span class="sxs-lookup"><span data-stu-id="3f551-134">When you register on the constructor, you won't miss any notification that's caused by a change during the lifetime of **IReliableStateManager**.</span></span>

```csharp
public MyService(StatefulServiceContext context)
    : base(MyService.EndpointName, context, CreateReliableStateManager(context))
{
    this.StateManager.TransactionChanged += this.OnTransactionChangedHandler;
    this.StateManager.StateManagerChanged += this.OnStateManagerChangedHandler;
}
```

<span data-ttu-id="3f551-135">The **TransactionChanged** event handler uses **NotifyTransactionChangedEventArgs** to provide details about the event.</span><span class="sxs-lookup"><span data-stu-id="3f551-135">The **TransactionChanged** event handler uses **NotifyTransactionChangedEventArgs** to provide details about the event.</span></span> <span data-ttu-id="3f551-136">It contains the action property (for example, **NotifyTransactionChangedAction.Commit**) that specifies the type of change.</span><span class="sxs-lookup"><span data-stu-id="3f551-136">It contains the action property (for example, **NotifyTransactionChangedAction.Commit**) that specifies the type of change.</span></span> <span data-ttu-id="3f551-137">It also contains the transaction property that provides a reference to the transaction that changed.</span><span class="sxs-lookup"><span data-stu-id="3f551-137">It also contains the transaction property that provides a reference to the transaction that changed.</span></span>

> [!NOTE]
> <span data-ttu-id="3f551-138">Today, **TransactionChanged** events are raised only if the transaction is committed.</span><span class="sxs-lookup"><span data-stu-id="3f551-138">Today, **TransactionChanged** events are raised only if the transaction is committed.</span></span> <span data-ttu-id="3f551-139">The action is then equal to **NotifyTransactionChangedAction.Commit**.</span><span class="sxs-lookup"><span data-stu-id="3f551-139">The action is then equal to **NotifyTransactionChangedAction.Commit**.</span></span> <span data-ttu-id="3f551-140">But in the future, events might be raised for other types of transaction state changes.</span><span class="sxs-lookup"><span data-stu-id="3f551-140">But in the future, events might be raised for other types of transaction state changes.</span></span> <span data-ttu-id="3f551-141">We recommend checking the action and processing the event only if it's one that you expect.</span><span class="sxs-lookup"><span data-stu-id="3f551-141">We recommend checking the action and processing the event only if it's one that you expect.</span></span>
> 
> 

<span data-ttu-id="3f551-142">Following is an example **TransactionChanged** event handler.</span><span class="sxs-lookup"><span data-stu-id="3f551-142">Following is an example **TransactionChanged** event handler.</span></span>

```csharp
private void OnTransactionChangedHandler(object sender, NotifyTransactionChangedEventArgs e)
{
    if (e.Action == NotifyTransactionChangedAction.Commit)
    {
        this.lastCommitLsn = e.Transaction.CommitSequenceNumber;
        this.lastTransactionId = e.Transaction.TransactionId;

        this.lastCommittedTransactionList.Add(e.Transaction.TransactionId);
    }
}
```

<span data-ttu-id="3f551-143">The **StateManagerChanged** event handler uses **NotifyStateManagerChangedEventArgs** to provide details about the event.</span><span class="sxs-lookup"><span data-stu-id="3f551-143">The **StateManagerChanged** event handler uses **NotifyStateManagerChangedEventArgs** to provide details about the event.</span></span>
<span data-ttu-id="3f551-144">**NotifyStateManagerChangedEventArgs** has two subclasses: **NotifyStateManagerRebuildEventArgs** and **NotifyStateManagerSingleEntityChangedEventArgs**.</span><span class="sxs-lookup"><span data-stu-id="3f551-144">**NotifyStateManagerChangedEventArgs** has two subclasses: **NotifyStateManagerRebuildEventArgs** and **NotifyStateManagerSingleEntityChangedEventArgs**.</span></span>
<span data-ttu-id="3f551-145">You use the action property in **NotifyStateManagerChangedEventArgs** to cast **NotifyStateManagerChangedEventArgs** to the correct subclass:</span><span class="sxs-lookup"><span data-stu-id="3f551-145">You use the action property in **NotifyStateManagerChangedEventArgs** to cast **NotifyStateManagerChangedEventArgs** to the correct subclass:</span></span>

* <span data-ttu-id="3f551-146">**NotifyStateManagerChangedAction.Rebuild**: **NotifyStateManagerRebuildEventArgs**</span><span class="sxs-lookup"><span data-stu-id="3f551-146">**NotifyStateManagerChangedAction.Rebuild**: **NotifyStateManagerRebuildEventArgs**</span></span>
* <span data-ttu-id="3f551-147">**NotifyStateManagerChangedAction.Add** and **NotifyStateManagerChangedAction.Remove**: **NotifyStateManagerSingleEntityChangedEventArgs**</span><span class="sxs-lookup"><span data-stu-id="3f551-147">**NotifyStateManagerChangedAction.Add** and **NotifyStateManagerChangedAction.Remove**: **NotifyStateManagerSingleEntityChangedEventArgs**</span></span>

<span data-ttu-id="3f551-148">Following is an example **StateManagerChanged** notification handler.</span><span class="sxs-lookup"><span data-stu-id="3f551-148">Following is an example **StateManagerChanged** notification handler.</span></span>

```csharp
public void OnStateManagerChangedHandler(object sender, NotifyStateManagerChangedEventArgs e)
{
    if (e.Action == NotifyStateManagerChangedAction.Rebuild)
    {
        this.ProcessStataManagerRebuildNotification(e);

        return;
    }

    this.ProcessStateManagerSingleEntityNotification(e);
}
```

## <a name="reliable-dictionary-notifications"></a><span data-ttu-id="3f551-149">Reliable Dictionary notifications</span><span class="sxs-lookup"><span data-stu-id="3f551-149">Reliable Dictionary notifications</span></span>
<span data-ttu-id="3f551-150">Reliable Dictionary provides notifications for the following events:</span><span class="sxs-lookup"><span data-stu-id="3f551-150">Reliable Dictionary provides notifications for the following events:</span></span>

* <span data-ttu-id="3f551-151">Rebuild: Called when **ReliableDictionary** has recovered its state from a recovered or copied local state or backup.</span><span class="sxs-lookup"><span data-stu-id="3f551-151">Rebuild: Called when **ReliableDictionary** has recovered its state from a recovered or copied local state or backup.</span></span>
* <span data-ttu-id="3f551-152">Clear: Called when the state of **ReliableDictionary** has been cleared through the **ClearAsync** method.</span><span class="sxs-lookup"><span data-stu-id="3f551-152">Clear: Called when the state of **ReliableDictionary** has been cleared through the **ClearAsync** method.</span></span>
* <span data-ttu-id="3f551-153">Add: Called when an item has been added to **ReliableDictionary**.</span><span class="sxs-lookup"><span data-stu-id="3f551-153">Add: Called when an item has been added to **ReliableDictionary**.</span></span>
* <span data-ttu-id="3f551-154">Update: Called when an item in **IReliableDictionary** has been updated.</span><span class="sxs-lookup"><span data-stu-id="3f551-154">Update: Called when an item in **IReliableDictionary** has been updated.</span></span>
* <span data-ttu-id="3f551-155">Remove: Called when an item in **IReliableDictionary** has been deleted.</span><span class="sxs-lookup"><span data-stu-id="3f551-155">Remove: Called when an item in **IReliableDictionary** has been deleted.</span></span>

<span data-ttu-id="3f551-156">To get Reliable Dictionary notifications, you need to register with the **DictionaryChanged** event handler on **IReliableDictionary**.</span><span class="sxs-lookup"><span data-stu-id="3f551-156">To get Reliable Dictionary notifications, you need to register with the **DictionaryChanged** event handler on **IReliableDictionary**.</span></span> <span data-ttu-id="3f551-157">A common place to register with these event handlers is in the **ReliableStateManager.StateManagerChanged** add notification.</span><span class="sxs-lookup"><span data-stu-id="3f551-157">A common place to register with these event handlers is in the **ReliableStateManager.StateManagerChanged** add notification.</span></span>
<span data-ttu-id="3f551-158">Registering when **IReliableDictionary** is added to **IReliableStateManager** ensures that you won't miss any notifications.</span><span class="sxs-lookup"><span data-stu-id="3f551-158">Registering when **IReliableDictionary** is added to **IReliableStateManager** ensures that you won't miss any notifications.</span></span>

```csharp
private void ProcessStateManagerSingleEntityNotification(NotifyStateManagerChangedEventArgs e)
{
    var operation = e as NotifyStateManagerSingleEntityChangedEventArgs;

    if (operation.Action == NotifyStateManagerChangedAction.Add)
    {
        if (operation.ReliableState is IReliableDictionary<TKey, TValue>)
        {
            var dictionary = (IReliableDictionary<TKey, TValue>)operation.ReliableState;
            dictionary.RebuildNotificationAsyncCallback = this.OnDictionaryRebuildNotificationHandlerAsync;
            dictionary.DictionaryChanged += this.OnDictionaryChangedHandler;
        }
    }
}
```

> [!NOTE]
> <span data-ttu-id="3f551-159">**ProcessStateManagerSingleEntityNotification** is the sample method that the preceding **OnStateManagerChangedHandler** example calls.</span><span class="sxs-lookup"><span data-stu-id="3f551-159">**ProcessStateManagerSingleEntityNotification** is the sample method that the preceding **OnStateManagerChangedHandler** example calls.</span></span>
> 
> 

<span data-ttu-id="3f551-160">The preceding code sets the **IReliableNotificationAsyncCallback** interface, along with **DictionaryChanged**.</span><span class="sxs-lookup"><span data-stu-id="3f551-160">The preceding code sets the **IReliableNotificationAsyncCallback** interface, along with **DictionaryChanged**.</span></span> <span data-ttu-id="3f551-161">Because **NotifyDictionaryRebuildEventArgs** contains an **IAsyncEnumerable** interface--which needs to be enumerated asynchronously--rebuild notifications are fired through **RebuildNotificationAsyncCallback** instead of **OnDictionaryChangedHandler**.</span><span class="sxs-lookup"><span data-stu-id="3f551-161">Because **NotifyDictionaryRebuildEventArgs** contains an **IAsyncEnumerable** interface--which needs to be enumerated asynchronously--rebuild notifications are fired through **RebuildNotificationAsyncCallback** instead of **OnDictionaryChangedHandler**.</span></span>

```csharp
public async Task OnDictionaryRebuildNotificationHandlerAsync(
    IReliableDictionary<TKey, TValue> origin,
    NotifyDictionaryRebuildEventArgs<TKey, TValue> rebuildNotification)
{
    this.secondaryIndex.Clear();

    var enumerator = e.State.GetAsyncEnumerator();
    while (await enumerator.MoveNextAsync(CancellationToken.None))
    {
        this.secondaryIndex.Add(enumerator.Current.Key, enumerator.Current.Value);
    }
}
```

> [!NOTE]
> <span data-ttu-id="3f551-162">In the preceding code, as part of processing the rebuild notification, first the maintained aggregated state is cleared.</span><span class="sxs-lookup"><span data-stu-id="3f551-162">In the preceding code, as part of processing the rebuild notification, first the maintained aggregated state is cleared.</span></span> <span data-ttu-id="3f551-163">Because the reliable collection is being rebuilt with a new state, all previous notifications are irrelevant.</span><span class="sxs-lookup"><span data-stu-id="3f551-163">Because the reliable collection is being rebuilt with a new state, all previous notifications are irrelevant.</span></span>
> 
> 

<span data-ttu-id="3f551-164">The **DictionaryChanged** event handler uses **NotifyDictionaryChangedEventArgs** to provide details about the event.</span><span class="sxs-lookup"><span data-stu-id="3f551-164">The **DictionaryChanged** event handler uses **NotifyDictionaryChangedEventArgs** to provide details about the event.</span></span>
<span data-ttu-id="3f551-165">**NotifyDictionaryChangedEventArgs** has five subclasses.</span><span class="sxs-lookup"><span data-stu-id="3f551-165">**NotifyDictionaryChangedEventArgs** has five subclasses.</span></span> <span data-ttu-id="3f551-166">Use the action property in **NotifyDictionaryChangedEventArgs** to cast **NotifyDictionaryChangedEventArgs** to the correct subclass:</span><span class="sxs-lookup"><span data-stu-id="3f551-166">Use the action property in **NotifyDictionaryChangedEventArgs** to cast **NotifyDictionaryChangedEventArgs** to the correct subclass:</span></span>

* <span data-ttu-id="3f551-167">**NotifyDictionaryChangedAction.Rebuild**: **NotifyDictionaryRebuildEventArgs**</span><span class="sxs-lookup"><span data-stu-id="3f551-167">**NotifyDictionaryChangedAction.Rebuild**: **NotifyDictionaryRebuildEventArgs**</span></span>
* <span data-ttu-id="3f551-168">**NotifyDictionaryChangedAction.Clear**: **NotifyDictionaryClearEventArgs**</span><span class="sxs-lookup"><span data-stu-id="3f551-168">**NotifyDictionaryChangedAction.Clear**: **NotifyDictionaryClearEventArgs**</span></span>
* <span data-ttu-id="3f551-169">**NotifyDictionaryChangedAction.Add** and **NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemAddedEventArgs**</span><span class="sxs-lookup"><span data-stu-id="3f551-169">**NotifyDictionaryChangedAction.Add** and **NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemAddedEventArgs**</span></span>
* <span data-ttu-id="3f551-170">**NotifyDictionaryChangedAction.Update**: **NotifyDictionaryItemUpdatedEventArgs**</span><span class="sxs-lookup"><span data-stu-id="3f551-170">**NotifyDictionaryChangedAction.Update**: **NotifyDictionaryItemUpdatedEventArgs**</span></span>
* <span data-ttu-id="3f551-171">**NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemRemovedEventArgs**</span><span class="sxs-lookup"><span data-stu-id="3f551-171">**NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemRemovedEventArgs**</span></span>

```csharp
public void OnDictionaryChangedHandler(object sender, NotifyDictionaryChangedEventArgs<TKey, TValue> e)
{
    switch (e.Action)
    {
        case NotifyDictionaryChangedAction.Clear:
            var clearEvent = e as NotifyDictionaryClearEventArgs<TKey, TValue>;
            this.ProcessClearNotification(clearEvent);
            return;

        case NotifyDictionaryChangedAction.Add:
            var addEvent = e as NotifyDictionaryItemAddedEventArgs<TKey, TValue>;
            this.ProcessAddNotification(addEvent);
            return;

        case NotifyDictionaryChangedAction.Update:
            var updateEvent = e as NotifyDictionaryItemUpdatedEventArgs<TKey, TValue>;
            this.ProcessUpdateNotification(updateEvent);
            return;

        case NotifyDictionaryChangedAction.Remove:
            var deleteEvent = e as NotifyDictionaryItemRemovedEventArgs<TKey, TValue>;
            this.ProcessRemoveNotification(deleteEvent);
            return;

        default:
            break;
    }
}
```

## <a name="recommendations"></a><span data-ttu-id="3f551-172">Recommendations</span><span class="sxs-lookup"><span data-stu-id="3f551-172">Recommendations</span></span>
* <span data-ttu-id="3f551-173">*Do* complete notification events as fast as possible.</span><span class="sxs-lookup"><span data-stu-id="3f551-173">*Do* complete notification events as fast as possible.</span></span>
* <span data-ttu-id="3f551-174">*Do not* execute any expensive operations (for example, I/O operations) as part of synchronous events.</span><span class="sxs-lookup"><span data-stu-id="3f551-174">*Do not* execute any expensive operations (for example, I/O operations) as part of synchronous events.</span></span>
* <span data-ttu-id="3f551-175">*Do* check the action type before you process the event.</span><span class="sxs-lookup"><span data-stu-id="3f551-175">*Do* check the action type before you process the event.</span></span> <span data-ttu-id="3f551-176">New action types might be added in the future.</span><span class="sxs-lookup"><span data-stu-id="3f551-176">New action types might be added in the future.</span></span>

<span data-ttu-id="3f551-177">Here are some things to keep in mind:</span><span class="sxs-lookup"><span data-stu-id="3f551-177">Here are some things to keep in mind:</span></span>

* <span data-ttu-id="3f551-178">Notifications are fired as part of the execution of an operation.</span><span class="sxs-lookup"><span data-stu-id="3f551-178">Notifications are fired as part of the execution of an operation.</span></span> <span data-ttu-id="3f551-179">For example, a restore notification is fired as the last step of a restore operation.</span><span class="sxs-lookup"><span data-stu-id="3f551-179">For example, a restore notification is fired as the last step of a restore operation.</span></span> <span data-ttu-id="3f551-180">A restore will not finish until the notification event is processed.</span><span class="sxs-lookup"><span data-stu-id="3f551-180">A restore will not finish until the notification event is processed.</span></span>
* <span data-ttu-id="3f551-181">Because notifications are fired as part of the applying operations, clients see only notifications for locally committed operations.</span><span class="sxs-lookup"><span data-stu-id="3f551-181">Because notifications are fired as part of the applying operations, clients see only notifications for locally committed operations.</span></span> <span data-ttu-id="3f551-182">And because operations are guaranteed only to be locally committed (in other words, logged), they might or might not be undone in the future.</span><span class="sxs-lookup"><span data-stu-id="3f551-182">And because operations are guaranteed only to be locally committed (in other words, logged), they might or might not be undone in the future.</span></span>
* <span data-ttu-id="3f551-183">On the redo path, a single notification is fired for each applied operation.</span><span class="sxs-lookup"><span data-stu-id="3f551-183">On the redo path, a single notification is fired for each applied operation.</span></span> <span data-ttu-id="3f551-184">This means that if transaction T1 includes Create(X), Delete(X), and Create(X), you'll get one notification for the creation of X, one for the deletion, and one for the creation again, in that order.</span><span class="sxs-lookup"><span data-stu-id="3f551-184">This means that if transaction T1 includes Create(X), Delete(X), and Create(X), you'll get one notification for the creation of X, one for the deletion, and one for the creation again, in that order.</span></span>
* <span data-ttu-id="3f551-185">For transactions that contain multiple operations, operations are applied in the order in which they were received on the primary replica from the user.</span><span class="sxs-lookup"><span data-stu-id="3f551-185">For transactions that contain multiple operations, operations are applied in the order in which they were received on the primary replica from the user.</span></span>
* <span data-ttu-id="3f551-186">As part of processing false progress, some operations might be undone.</span><span class="sxs-lookup"><span data-stu-id="3f551-186">As part of processing false progress, some operations might be undone.</span></span> <span data-ttu-id="3f551-187">Notifications are raised for such undo operations, rolling the state of the replica back to a stable point.</span><span class="sxs-lookup"><span data-stu-id="3f551-187">Notifications are raised for such undo operations, rolling the state of the replica back to a stable point.</span></span> <span data-ttu-id="3f551-188">One important difference of undo notifications is that events that have duplicate keys are aggregated.</span><span class="sxs-lookup"><span data-stu-id="3f551-188">One important difference of undo notifications is that events that have duplicate keys are aggregated.</span></span> <span data-ttu-id="3f551-189">For example, if transaction T1 is being undone, you'll see a single notification to Delete(X).</span><span class="sxs-lookup"><span data-stu-id="3f551-189">For example, if transaction T1 is being undone, you'll see a single notification to Delete(X).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3f551-190">Next steps</span><span class="sxs-lookup"><span data-stu-id="3f551-190">Next steps</span></span>
* [<span data-ttu-id="3f551-191">Reliable Collections</span><span class="sxs-lookup"><span data-stu-id="3f551-191">Reliable Collections</span></span>](service-fabric-work-with-reliable-collections.md)
* [<span data-ttu-id="3f551-192">Reliable Services quick start</span><span class="sxs-lookup"><span data-stu-id="3f551-192">Reliable Services quick start</span></span>](service-fabric-reliable-services-quick-start.md)
* [<span data-ttu-id="3f551-193">Reliable Services backup and restore (disaster recovery)</span><span class="sxs-lookup"><span data-stu-id="3f551-193">Reliable Services backup and restore (disaster recovery)</span></span>](service-fabric-reliable-services-backup-restore.md)
* [<span data-ttu-id="3f551-194">Developer reference for Reliable Collections</span><span class="sxs-lookup"><span data-stu-id="3f551-194">Developer reference for Reliable Collections</span></span>](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)

