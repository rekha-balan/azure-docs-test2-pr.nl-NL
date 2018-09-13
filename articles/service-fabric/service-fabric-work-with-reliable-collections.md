---
title: Working with Reliable Collections | Microsoft Docs
description: Learn the best practices for working with Reliable Collections.
services: service-fabric
documentationcenter: .net
author: rajak
manager: timlt
editor: ''
ms.assetid: 39e0cd6b-32c4-4b97-bbcf-33dad93dcad1
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/19/2017
ms.author: rajak
ms.openlocfilehash: f53f13e4fb83b1cd370ec673e86e5311cd93055f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660897"
---
# <a name="working-with-reliable-collections"></a><span data-ttu-id="1732e-103">Working with Reliable Collections</span><span class="sxs-lookup"><span data-stu-id="1732e-103">Working with Reliable Collections</span></span>
<span data-ttu-id="1732e-104">Service Fabric offers a stateful programming model available to .NET developers via Reliable Collections.</span><span class="sxs-lookup"><span data-stu-id="1732e-104">Service Fabric offers a stateful programming model available to .NET developers via Reliable Collections.</span></span> <span data-ttu-id="1732e-105">Specifically, Service Fabric provides reliable dictionary and reliable queue classes.</span><span class="sxs-lookup"><span data-stu-id="1732e-105">Specifically, Service Fabric provides reliable dictionary and reliable queue classes.</span></span> <span data-ttu-id="1732e-106">When you use these classes, your state is partitioned (for scalability), replicated (for availability), and transacted within a partition (for ACID semantics).</span><span class="sxs-lookup"><span data-stu-id="1732e-106">When you use these classes, your state is partitioned (for scalability), replicated (for availability), and transacted within a partition (for ACID semantics).</span></span> <span data-ttu-id="1732e-107">Let’s look at a typical usage of a reliable dictionary object and see what its actually doing.</span><span class="sxs-lookup"><span data-stu-id="1732e-107">Let’s look at a typical usage of a reliable dictionary object and see what its actually doing.</span></span>

```csharp

///retry:

try {
   // Create a new Transaction object for this partition
   using (ITransaction tx = base.StateManager.CreateTransaction()) {
      // AddAsync takes key's write lock; if >4 secs, TimeoutException
      // Key & value put in temp dictionary (read your own writes),
      // serialized, redo/undo record is logged & sent to
      // secondary replicas
      await m_dic.AddAsync(tx, key, value, cancellationToken);

      // CommitAsync sends Commit record to log & secondary replicas
      // After quorum responds, all locks released
      await tx.CommitAsync();
   }
   // If CommitAsync not called, Dispose sends Abort
   // record to log & all locks released
}
catch (TimeoutException) {
   await Task.Delay(100, cancellationToken); goto retry;
}
```

<span data-ttu-id="1732e-108">All operations on reliable dictionary objects (except for ClearAsync which is not undoable), require an ITransaction object.</span><span class="sxs-lookup"><span data-stu-id="1732e-108">All operations on reliable dictionary objects (except for ClearAsync which is not undoable), require an ITransaction object.</span></span> <span data-ttu-id="1732e-109">This object has associated with it any and all changes you’re attempting to make to any reliable dictionary and/or reliable queue objects within a single partition.</span><span class="sxs-lookup"><span data-stu-id="1732e-109">This object has associated with it any and all changes you’re attempting to make to any reliable dictionary and/or reliable queue objects within a single partition.</span></span> <span data-ttu-id="1732e-110">You acquire an ITransaction object by calling the partition’s StateManager’s CreateTransaction method.</span><span class="sxs-lookup"><span data-stu-id="1732e-110">You acquire an ITransaction object by calling the partition’s StateManager’s CreateTransaction method.</span></span>

<span data-ttu-id="1732e-111">In the code above, the ITransaction object is passed to a reliable dictionary’s AddAsync method.</span><span class="sxs-lookup"><span data-stu-id="1732e-111">In the code above, the ITransaction object is passed to a reliable dictionary’s AddAsync method.</span></span> <span data-ttu-id="1732e-112">Internally, dictionary methods that accepts a key take a reader/writer lock associated with the key.</span><span class="sxs-lookup"><span data-stu-id="1732e-112">Internally, dictionary methods that accepts a key take a reader/writer lock associated with the key.</span></span> <span data-ttu-id="1732e-113">If the method modifies the key’s value, the method takes a write lock on the key and if the method only reads from the key’s value, then a read lock is taken on the key.</span><span class="sxs-lookup"><span data-stu-id="1732e-113">If the method modifies the key’s value, the method takes a write lock on the key and if the method only reads from the key’s value, then a read lock is taken on the key.</span></span> <span data-ttu-id="1732e-114">Since AddAsync modifies the key’s value to the new, passed-in value, the key’s write lock is taken.</span><span class="sxs-lookup"><span data-stu-id="1732e-114">Since AddAsync modifies the key’s value to the new, passed-in value, the key’s write lock is taken.</span></span> <span data-ttu-id="1732e-115">So, if 2 (or more) threads attempt to add values with the same key at the same time, one thread will acquire the write lock and the other threads will block.</span><span class="sxs-lookup"><span data-stu-id="1732e-115">So, if 2 (or more) threads attempt to add values with the same key at the same time, one thread will acquire the write lock and the other threads will block.</span></span> <span data-ttu-id="1732e-116">By default, methods block for up to 4 seconds to acquire the lock; after 4 seconds, the methods throw a TimeoutException.</span><span class="sxs-lookup"><span data-stu-id="1732e-116">By default, methods block for up to 4 seconds to acquire the lock; after 4 seconds, the methods throw a TimeoutException.</span></span> <span data-ttu-id="1732e-117">Method overloads exist allowing you to pass an explicit timeout value if you’d prefer.</span><span class="sxs-lookup"><span data-stu-id="1732e-117">Method overloads exist allowing you to pass an explicit timeout value if you’d prefer.</span></span>

<span data-ttu-id="1732e-118">Usually, you write your code to react to a TimeoutException by catching it and retrying the entire operation (as shown in the code above).</span><span class="sxs-lookup"><span data-stu-id="1732e-118">Usually, you write your code to react to a TimeoutException by catching it and retrying the entire operation (as shown in the code above).</span></span> <span data-ttu-id="1732e-119">In my simple code, I’m just calling Task.Delay passing 100 milliseconds each time.</span><span class="sxs-lookup"><span data-stu-id="1732e-119">In my simple code, I’m just calling Task.Delay passing 100 milliseconds each time.</span></span> <span data-ttu-id="1732e-120">But, in reality, you might be better off using some kind of exponential back-off delay instead.</span><span class="sxs-lookup"><span data-stu-id="1732e-120">But, in reality, you might be better off using some kind of exponential back-off delay instead.</span></span>

<span data-ttu-id="1732e-121">Once the lock is acquired, AddAsync adds the key and value object references to an internal temporary dictionary associated with the ITransaction object.</span><span class="sxs-lookup"><span data-stu-id="1732e-121">Once the lock is acquired, AddAsync adds the key and value object references to an internal temporary dictionary associated with the ITransaction object.</span></span> <span data-ttu-id="1732e-122">This is done to provide you with read-your-own-writes semantics.</span><span class="sxs-lookup"><span data-stu-id="1732e-122">This is done to provide you with read-your-own-writes semantics.</span></span> <span data-ttu-id="1732e-123">That is, after you call AddAsync, a later call to TryGetValueAsync (using the same ITransaction object) will return the value even if you have not yet committed the transaction.</span><span class="sxs-lookup"><span data-stu-id="1732e-123">That is, after you call AddAsync, a later call to TryGetValueAsync (using the same ITransaction object) will return the value even if you have not yet committed the transaction.</span></span> <span data-ttu-id="1732e-124">Next, AddAsync serializes your key and value objects to byte arrays and appends these byte arrays to a log file on the local node.</span><span class="sxs-lookup"><span data-stu-id="1732e-124">Next, AddAsync serializes your key and value objects to byte arrays and appends these byte arrays to a log file on the local node.</span></span> <span data-ttu-id="1732e-125">Finally, AddAsync sends the byte arrays to all the secondary replicas so they have the same key/value information.</span><span class="sxs-lookup"><span data-stu-id="1732e-125">Finally, AddAsync sends the byte arrays to all the secondary replicas so they have the same key/value information.</span></span> <span data-ttu-id="1732e-126">Even though the key/value information has been written to a log file, the information is not considered part of the dictionary until the transaction that they are associated with has been committed.</span><span class="sxs-lookup"><span data-stu-id="1732e-126">Even though the key/value information has been written to a log file, the information is not considered part of the dictionary until the transaction that they are associated with has been committed.</span></span>

<span data-ttu-id="1732e-127">In the code above, the call to CommitAsync commits all of the transaction’s operations.</span><span class="sxs-lookup"><span data-stu-id="1732e-127">In the code above, the call to CommitAsync commits all of the transaction’s operations.</span></span> <span data-ttu-id="1732e-128">Specifically, it appends commit information to the log file on the local node and also sends the commit record to all the secondary replicas.</span><span class="sxs-lookup"><span data-stu-id="1732e-128">Specifically, it appends commit information to the log file on the local node and also sends the commit record to all the secondary replicas.</span></span> <span data-ttu-id="1732e-129">Once a quorum (majority) of the replicas has replied, all data changes are considered permanent and any locks associated with keys that were manipulated via the ITransaction object are released so other threads/transactions can manipulate the same keys and their values.</span><span class="sxs-lookup"><span data-stu-id="1732e-129">Once a quorum (majority) of the replicas has replied, all data changes are considered permanent and any locks associated with keys that were manipulated via the ITransaction object are released so other threads/transactions can manipulate the same keys and their values.</span></span>

<span data-ttu-id="1732e-130">If CommitAsync is not called (usually due to an exception being thrown), then the ITransaction object gets disposed.</span><span class="sxs-lookup"><span data-stu-id="1732e-130">If CommitAsync is not called (usually due to an exception being thrown), then the ITransaction object gets disposed.</span></span> <span data-ttu-id="1732e-131">When disposing an uncommitted ITransaction object, Service Fabric appends abort information to the local node’s log file and nothing needs to be sent to any of the secondary replicas.</span><span class="sxs-lookup"><span data-stu-id="1732e-131">When disposing an uncommitted ITransaction object, Service Fabric appends abort information to the local node’s log file and nothing needs to be sent to any of the secondary replicas.</span></span> <span data-ttu-id="1732e-132">And then, any locks associated with keys that were manipulated via the transaction are released.</span><span class="sxs-lookup"><span data-stu-id="1732e-132">And then, any locks associated with keys that were manipulated via the transaction are released.</span></span>

## <a name="common-pitfalls-and-how-to-avoid-them"></a><span data-ttu-id="1732e-133">Common pitfalls and how to avoid them</span><span class="sxs-lookup"><span data-stu-id="1732e-133">Common pitfalls and how to avoid them</span></span>
<span data-ttu-id="1732e-134">Now that you understand how the reliable collections work internally, let’s take a look at some common misuses of them.</span><span class="sxs-lookup"><span data-stu-id="1732e-134">Now that you understand how the reliable collections work internally, let’s take a look at some common misuses of them.</span></span> <span data-ttu-id="1732e-135">See the code below:</span><span class="sxs-lookup"><span data-stu-id="1732e-135">See the code below:</span></span>

```csharp
using (ITransaction tx = StateManager.CreateTransaction()) {
   // AddAsync serializes the name/user, logs the bytes,
   // & sends the bytes to the secondary replicas.
   await m_dic.AddAsync(tx, name, user);

   // The line below updates the property’s value in memory only; the
   // new value is NOT serialized, logged, & sent to secondary replicas.
   user.LastLogin = DateTime.UtcNow;  // Corruption!

   await tx.CommitAsync();
}
```

<span data-ttu-id="1732e-136">When working with a regular .NET dictionary, you can add a key/value to the dictionary and then change the value of a property (such as LastLogin).</span><span class="sxs-lookup"><span data-stu-id="1732e-136">When working with a regular .NET dictionary, you can add a key/value to the dictionary and then change the value of a property (such as LastLogin).</span></span> <span data-ttu-id="1732e-137">However, this code will not work correctly with a reliable dictionary.</span><span class="sxs-lookup"><span data-stu-id="1732e-137">However, this code will not work correctly with a reliable dictionary.</span></span> <span data-ttu-id="1732e-138">Remember from the earlier discussion, the call to AddAsync serializes the key/value objects to byte arrays and then saves the arrays to a local file and also sends them to the secondary replicas.</span><span class="sxs-lookup"><span data-stu-id="1732e-138">Remember from the earlier discussion, the call to AddAsync serializes the key/value objects to byte arrays and then saves the arrays to a local file and also sends them to the secondary replicas.</span></span> <span data-ttu-id="1732e-139">If you later change a property, this changes the property’s value in memory only; it does not impact the local file or the data sent to the replicas.</span><span class="sxs-lookup"><span data-stu-id="1732e-139">If you later change a property, this changes the property’s value in memory only; it does not impact the local file or the data sent to the replicas.</span></span> <span data-ttu-id="1732e-140">If the process crashes, what’s in memory is thrown away.</span><span class="sxs-lookup"><span data-stu-id="1732e-140">If the process crashes, what’s in memory is thrown away.</span></span> <span data-ttu-id="1732e-141">When a new process starts or if another replica becomes primary, then the old property value is what is available.</span><span class="sxs-lookup"><span data-stu-id="1732e-141">When a new process starts or if another replica becomes primary, then the old property value is what is available.</span></span>

<span data-ttu-id="1732e-142">I cannot stress enough how easy it is to make the kind of mistake shown above.</span><span class="sxs-lookup"><span data-stu-id="1732e-142">I cannot stress enough how easy it is to make the kind of mistake shown above.</span></span> <span data-ttu-id="1732e-143">And, you will only learn about the mistake if/when the process goes down.</span><span class="sxs-lookup"><span data-stu-id="1732e-143">And, you will only learn about the mistake if/when the process goes down.</span></span> <span data-ttu-id="1732e-144">The correct way to write the code is simply to reverse the two lines:</span><span class="sxs-lookup"><span data-stu-id="1732e-144">The correct way to write the code is simply to reverse the two lines:</span></span>


```csharp

using (ITransaction tx = StateManager.CreateTransaction()) {
   user.LastLogin = DateTime.UtcNow;  // Do this BEFORE calling AddAsync
   await m_dic.AddAsync(tx, name, user);
   await tx.CommitAsync();
}
```

<span data-ttu-id="1732e-145">Here is another example showing a common mistake:</span><span class="sxs-lookup"><span data-stu-id="1732e-145">Here is another example showing a common mistake:</span></span>

```csharp

using (ITransaction tx = StateManager.CreateTransaction()) {
   // Use the user’s name to look up their data
   ConditionalValue<User> user =
      await m_dic.TryGetValueAsync(tx, name);

   // The user exists in the dictionary, update one of their properties.
   if (user.HasValue) {
      // The line below updates the property’s value in memory only; the
      // new value is NOT serialized, logged, & sent to secondary replicas.
      user.Value.LastLogin = DateTime.UtcNow; // Corruption!
      await tx.CommitAsync();
   }
}
```

<span data-ttu-id="1732e-146">Again, with regular .NET dictionaries, the code above works fine and is a common pattern: the developer uses a key to look up a value.</span><span class="sxs-lookup"><span data-stu-id="1732e-146">Again, with regular .NET dictionaries, the code above works fine and is a common pattern: the developer uses a key to look up a value.</span></span> <span data-ttu-id="1732e-147">If the value exists, the developer changes a property’s value.</span><span class="sxs-lookup"><span data-stu-id="1732e-147">If the value exists, the developer changes a property’s value.</span></span> <span data-ttu-id="1732e-148">However, with reliable collections, this code exhibits the same problem as already discussed: **you MUST not modify an object once you have given it to a reliable collection.**</span><span class="sxs-lookup"><span data-stu-id="1732e-148">However, with reliable collections, this code exhibits the same problem as already discussed: **you MUST not modify an object once you have given it to a reliable collection.**</span></span>

<span data-ttu-id="1732e-149">The correct way to update a value in a reliable collection, is to get a reference to the existing value and consider the object referred to by this reference immutable.</span><span class="sxs-lookup"><span data-stu-id="1732e-149">The correct way to update a value in a reliable collection, is to get a reference to the existing value and consider the object referred to by this reference immutable.</span></span> <span data-ttu-id="1732e-150">Then, create a new object which is an exact copy of the original object.</span><span class="sxs-lookup"><span data-stu-id="1732e-150">Then, create a new object which is an exact copy of the original object.</span></span> <span data-ttu-id="1732e-151">Now, you can modify the state of this new object and write the new object into the collection so that it gets serialized to byte arrays, appended to the local file and sent to the replicas.</span><span class="sxs-lookup"><span data-stu-id="1732e-151">Now, you can modify the state of this new object and write the new object into the collection so that it gets serialized to byte arrays, appended to the local file and sent to the replicas.</span></span> <span data-ttu-id="1732e-152">After committing the change(s), the in-memory objects, the local file, and all the replicas have the same exact state.</span><span class="sxs-lookup"><span data-stu-id="1732e-152">After committing the change(s), the in-memory objects, the local file, and all the replicas have the same exact state.</span></span> <span data-ttu-id="1732e-153">All is good!</span><span class="sxs-lookup"><span data-stu-id="1732e-153">All is good!</span></span>

<span data-ttu-id="1732e-154">The code below shows the correct way to update a value in a reliable collection:</span><span class="sxs-lookup"><span data-stu-id="1732e-154">The code below shows the correct way to update a value in a reliable collection:</span></span>

```csharp

using (ITransaction tx = StateManager.CreateTransaction()) {
   // Use the user’s name to look up their data
   ConditionalValue<User> currentUser =
      await m_dic.TryGetValueAsync(tx, name);

   // The user exists in the dictionary, update one of their properties.
   if (currentUser.HasValue) {
      // Create new user object with the same state as the current user object.
      // NOTE: This must be a deep copy; not a shallow copy. Specifically, only
      // immutable state can be shared by currentUser & updatedUser object graphs.
      User updatedUser = new User(currentUser);

      // In the new object, modify any properties you desire
      updatedUser.LastLogin = DateTime.UtcNow;

      // Update the key’s value to the updateUser info
      await m_dic.SetValue(tx, name, updatedUser);

      await tx.CommitAsync();
   }
}
```

## <a name="define-immutable-data-types-to-prevent-programmer-error"></a><span data-ttu-id="1732e-155">Define immutable data types to prevent programmer error</span><span class="sxs-lookup"><span data-stu-id="1732e-155">Define immutable data types to prevent programmer error</span></span>
<span data-ttu-id="1732e-156">Ideally, we’d like the compiler to report errors when you accidentally produce code that mutates state of an object that you are supposed to consider immutable.</span><span class="sxs-lookup"><span data-stu-id="1732e-156">Ideally, we’d like the compiler to report errors when you accidentally produce code that mutates state of an object that you are supposed to consider immutable.</span></span> <span data-ttu-id="1732e-157">But, the C# compiler does not have the ability to do this.</span><span class="sxs-lookup"><span data-stu-id="1732e-157">But, the C# compiler does not have the ability to do this.</span></span> <span data-ttu-id="1732e-158">So, to avoid potential programmer bugs, we highly recommend that you define the types you use with reliable collections to be immutable types.</span><span class="sxs-lookup"><span data-stu-id="1732e-158">So, to avoid potential programmer bugs, we highly recommend that you define the types you use with reliable collections to be immutable types.</span></span> <span data-ttu-id="1732e-159">Specifically, this means that you stick to core value types (such as numbers [Int32, UInt64, etc.], DateTime, Guid, TimeSpan, and the like).</span><span class="sxs-lookup"><span data-stu-id="1732e-159">Specifically, this means that you stick to core value types (such as numbers [Int32, UInt64, etc.], DateTime, Guid, TimeSpan, and the like).</span></span> <span data-ttu-id="1732e-160">And, of course, you can also use String.</span><span class="sxs-lookup"><span data-stu-id="1732e-160">And, of course, you can also use String.</span></span> <span data-ttu-id="1732e-161">It is best to avoid collection properties as serializing and deserializing them can frequently can hurt performance.</span><span class="sxs-lookup"><span data-stu-id="1732e-161">It is best to avoid collection properties as serializing and deserializing them can frequently can hurt performance.</span></span> <span data-ttu-id="1732e-162">However, if you want to use collection properties, we highly recommend the use of .NET’s immutable collections library ([System.Collections.Immutable](https://www.nuget.org/packages/System.Collections.Immutable/)).</span><span class="sxs-lookup"><span data-stu-id="1732e-162">However, if you want to use collection properties, we highly recommend the use of .NET’s immutable collections library ([System.Collections.Immutable](https://www.nuget.org/packages/System.Collections.Immutable/)).</span></span> <span data-ttu-id="1732e-163">This library is available for download from http://nuget.org. We also recommend sealing your classes and making fields read-only whenever possible.</span><span class="sxs-lookup"><span data-stu-id="1732e-163">This library is available for download from http://nuget.org. We also recommend sealing your classes and making fields read-only whenever possible.</span></span>

<span data-ttu-id="1732e-164">The UserInfo type below demonstrates how to define an immutable type taking advantage of aforementioned recommendations.</span><span class="sxs-lookup"><span data-stu-id="1732e-164">The UserInfo type below demonstrates how to define an immutable type taking advantage of aforementioned recommendations.</span></span>

```csharp

[DataContract]
// If you don’t seal, you must ensure that any derived classes are also immutable
public sealed class UserInfo {
   private static readonly IEnumerable<ItemId> NoBids = ImmutableList<ItemId>.Empty;

   public UserInfo(String email, IEnumerable<ItemId> itemsBidding = null) {
      Email = email;
      ItemsBidding = (itemsBidding == null) ? NoBids : itemsBidding.ToImmutableList();
   }

   [OnDeserialized]
   private void OnDeserialized(StreamingContext context) {
      // Convert the deserialized collection to an immutable collection
      ItemsBidding = ItemsBidding.ToImmutableList();
   }

   [DataMember]
   public readonly String Email;

   // Ideally, this would be a readonly field but it can't be because OnDeserialized
   // has to set it. So instead, the getter is public and the setter is private.
   [DataMember]
   public IEnumerable<ItemId> ItemsBidding { get; private set; }

   // Since each UserInfo object is immutable, we add a new ItemId to the ItemsBidding
   // collection by creating a new immutable UserInfo object with the added ItemId.
   public UserInfo AddItemBidding(ItemId itemId) {
      return new UserInfo(Email, ((ImmutableList<ItemId>)ItemsBidding).Add(itemId));
   }
}
```

<span data-ttu-id="1732e-165">The ItemId type is also an immutable type as shown here:</span><span class="sxs-lookup"><span data-stu-id="1732e-165">The ItemId type is also an immutable type as shown here:</span></span>

```csharp

[DataContract]
public struct ItemId {

   [DataMember] public readonly String Seller;
   [DataMember] public readonly String ItemName;
   public ItemId(String seller, String itemName) {
      Seller = seller;
      ItemName = itemName;
   }
}
```

## <a name="schema-versioning-upgrades"></a><span data-ttu-id="1732e-166">Schema versioning (upgrades)</span><span class="sxs-lookup"><span data-stu-id="1732e-166">Schema versioning (upgrades)</span></span>
<span data-ttu-id="1732e-167">Internally, Reliable Collections serialize your objects using .NET’s DataContractSerializer.</span><span class="sxs-lookup"><span data-stu-id="1732e-167">Internally, Reliable Collections serialize your objects using .NET’s DataContractSerializer.</span></span> <span data-ttu-id="1732e-168">The serialized objects are persisted to the primary replica’s local disk and are also transmitted to the secondary replicas.</span><span class="sxs-lookup"><span data-stu-id="1732e-168">The serialized objects are persisted to the primary replica’s local disk and are also transmitted to the secondary replicas.</span></span> <span data-ttu-id="1732e-169">As your service matures, it’s likely you’ll want to change the kind of data (schema) your service requires.</span><span class="sxs-lookup"><span data-stu-id="1732e-169">As your service matures, it’s likely you’ll want to change the kind of data (schema) your service requires.</span></span> <span data-ttu-id="1732e-170">You must approach versioning of your data with great care.</span><span class="sxs-lookup"><span data-stu-id="1732e-170">You must approach versioning of your data with great care.</span></span> <span data-ttu-id="1732e-171">First and foremost, you must always be able to deserialize old data.</span><span class="sxs-lookup"><span data-stu-id="1732e-171">First and foremost, you must always be able to deserialize old data.</span></span> <span data-ttu-id="1732e-172">Specifically, this means your deserialization code must be infinitely backward compatible: Version 333 of your service code must be able to operate on data placed in a reliable collection by version 1 of your service code 5 years ago.</span><span class="sxs-lookup"><span data-stu-id="1732e-172">Specifically, this means your deserialization code must be infinitely backward compatible: Version 333 of your service code must be able to operate on data placed in a reliable collection by version 1 of your service code 5 years ago.</span></span>

<span data-ttu-id="1732e-173">Furthermore, service code is upgraded one upgrade domain at a time.</span><span class="sxs-lookup"><span data-stu-id="1732e-173">Furthermore, service code is upgraded one upgrade domain at a time.</span></span> <span data-ttu-id="1732e-174">So, during an upgrade, you have two different versions of your service code running simultaneously.</span><span class="sxs-lookup"><span data-stu-id="1732e-174">So, during an upgrade, you have two different versions of your service code running simultaneously.</span></span> <span data-ttu-id="1732e-175">You must avoid having the new version of your service code use the new schema as old versions of your service code might not be able to handle the new schema.</span><span class="sxs-lookup"><span data-stu-id="1732e-175">You must avoid having the new version of your service code use the new schema as old versions of your service code might not be able to handle the new schema.</span></span> <span data-ttu-id="1732e-176">When possible, you should design each version of your service to be forward compatible by 1 version.</span><span class="sxs-lookup"><span data-stu-id="1732e-176">When possible, you should design each version of your service to be forward compatible by 1 version.</span></span> <span data-ttu-id="1732e-177">Specifically, this means that V1 of your service code should be able to simply ignore any schema elements it does not explicitly handle.</span><span class="sxs-lookup"><span data-stu-id="1732e-177">Specifically, this means that V1 of your service code should be able to simply ignore any schema elements it does not explicitly handle.</span></span> <span data-ttu-id="1732e-178">However, it must be able to save any data it doesn’t explicitly know about and simply write it back out when updating a dictionary key or value.</span><span class="sxs-lookup"><span data-stu-id="1732e-178">However, it must be able to save any data it doesn’t explicitly know about and simply write it back out when updating a dictionary key or value.</span></span>

> [!WARNING]
> <span data-ttu-id="1732e-179">While you can modify the schema of a key, you must ensure that your key’s hash code and equals algorithms are stable.</span><span class="sxs-lookup"><span data-stu-id="1732e-179">While you can modify the schema of a key, you must ensure that your key’s hash code and equals algorithms are stable.</span></span> <span data-ttu-id="1732e-180">If you change how either of these algorithms operate, you will not be able to look up the key within the reliable dictionary ever again.</span><span class="sxs-lookup"><span data-stu-id="1732e-180">If you change how either of these algorithms operate, you will not be able to look up the key within the reliable dictionary ever again.</span></span>
>
>

<span data-ttu-id="1732e-181">Alternatively, you can perform what is typically referred to as a 2-phase upgrade.</span><span class="sxs-lookup"><span data-stu-id="1732e-181">Alternatively, you can perform what is typically referred to as a 2-phase upgrade.</span></span> <span data-ttu-id="1732e-182">With a 2-phase upgrade, you upgrade your service from V1 to V2: V2 contains the code that knows how to deal with the new schema change but this code doesn’t execute.</span><span class="sxs-lookup"><span data-stu-id="1732e-182">With a 2-phase upgrade, you upgrade your service from V1 to V2: V2 contains the code that knows how to deal with the new schema change but this code doesn’t execute.</span></span> <span data-ttu-id="1732e-183">When the V2 code reads V1 data, it operates on it and writes V1 data.</span><span class="sxs-lookup"><span data-stu-id="1732e-183">When the V2 code reads V1 data, it operates on it and writes V1 data.</span></span> <span data-ttu-id="1732e-184">Then, after the upgrade is complete across all upgrade domains, you can somehow signal to the running V2 instances that the upgrade is complete.</span><span class="sxs-lookup"><span data-stu-id="1732e-184">Then, after the upgrade is complete across all upgrade domains, you can somehow signal to the running V2 instances that the upgrade is complete.</span></span> <span data-ttu-id="1732e-185">(One way to signal this is to roll out a configuration upgrade; this is what makes this a 2-phase upgrade.) Now, the V2 instances can read V1 data, convert it to V2 data, operate on it, and write it out as V2 data.</span><span class="sxs-lookup"><span data-stu-id="1732e-185">(One way to signal this is to roll out a configuration upgrade; this is what makes this a 2-phase upgrade.) Now, the V2 instances can read V1 data, convert it to V2 data, operate on it, and write it out as V2 data.</span></span> <span data-ttu-id="1732e-186">When other instances read V2 data, they do not need to convert it, they just operate on it, and write out V2 data.</span><span class="sxs-lookup"><span data-stu-id="1732e-186">When other instances read V2 data, they do not need to convert it, they just operate on it, and write out V2 data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1732e-187">Next Steps</span><span class="sxs-lookup"><span data-stu-id="1732e-187">Next Steps</span></span>
<span data-ttu-id="1732e-188">To learn about creating forward compatible data contracts, see [Forward-Compatible Data Contracts](https://msdn.microsoft.com/library/ms731083.aspx).</span><span class="sxs-lookup"><span data-stu-id="1732e-188">To learn about creating forward compatible data contracts, see [Forward-Compatible Data Contracts](https://msdn.microsoft.com/library/ms731083.aspx).</span></span>

<span data-ttu-id="1732e-189">To learn best practices on versioning data contracts, see [Data Contract Versioning](https://msdn.microsoft.com/library/ms731138.aspx).</span><span class="sxs-lookup"><span data-stu-id="1732e-189">To learn best practices on versioning data contracts, see [Data Contract Versioning](https://msdn.microsoft.com/library/ms731138.aspx).</span></span>

<span data-ttu-id="1732e-190">To learn how to implement version tolerant data contracts, see [Version-Tolerant Serialization Callbacks](https://msdn.microsoft.com/library/ms733734.aspx).</span><span class="sxs-lookup"><span data-stu-id="1732e-190">To learn how to implement version tolerant data contracts, see [Version-Tolerant Serialization Callbacks](https://msdn.microsoft.com/library/ms733734.aspx).</span></span>

<span data-ttu-id="1732e-191">To learn how to provide a data structure that can interoperate across multiple versions, see [IExtensibleDataObject](https://msdn.microsoft.com/library/system.runtime.serialization.iextensibledataobject.aspx).</span><span class="sxs-lookup"><span data-stu-id="1732e-191">To learn how to provide a data structure that can interoperate across multiple versions, see [IExtensibleDataObject](https://msdn.microsoft.com/library/system.runtime.serialization.iextensibledataobject.aspx).</span></span>
