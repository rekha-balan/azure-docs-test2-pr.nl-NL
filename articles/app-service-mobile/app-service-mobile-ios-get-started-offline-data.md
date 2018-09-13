---
title: Enable offline syncing with iOS mobile apps | Microsoft Docs
description: Learn how to use Azure App Service mobile apps to cache and sync offline data in iOS applications.
documentationcenter: ios
author: conceptdev
manager: crdun
editor: ''
services: app-service\mobile
ms.assetid: eb5b9520-0f39-4a09-940a-dadb6d940db8
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 10/01/2016
ms.author: crdun
ms.openlocfilehash: 2f415f1886c654f3bdd880cdccaadc7aa3e69892
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44798153"
---
# <a name="enable-offline-syncing-with-ios-mobile-apps"></a><span data-ttu-id="48b62-103">Enable offline syncing with iOS mobile apps</span><span class="sxs-lookup"><span data-stu-id="48b62-103">Enable offline syncing with iOS mobile apps</span></span>
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a><span data-ttu-id="48b62-104">Overview</span><span class="sxs-lookup"><span data-stu-id="48b62-104">Overview</span></span>
<span data-ttu-id="48b62-105">This tutorial covers offline syncing with the Mobile Apps feature of Azure App Service for iOS.</span><span class="sxs-lookup"><span data-stu-id="48b62-105">This tutorial covers offline syncing with the Mobile Apps feature of Azure App Service for iOS.</span></span> <span data-ttu-id="48b62-106">With offline syncing end-users can interact with a mobile app to view, add, or modify data, even when they have no network connection.</span><span class="sxs-lookup"><span data-stu-id="48b62-106">With offline syncing end-users can interact with a mobile app to view, add, or modify data, even when they have no network connection.</span></span> <span data-ttu-id="48b62-107">Changes are stored in a local database.</span><span class="sxs-lookup"><span data-stu-id="48b62-107">Changes are stored in a local database.</span></span> <span data-ttu-id="48b62-108">After the device is back online, the changes are synced with the remote back end.</span><span class="sxs-lookup"><span data-stu-id="48b62-108">After the device is back online, the changes are synced with the remote back end.</span></span>

<span data-ttu-id="48b62-109">If this is your first experience with Mobile Apps, you should first complete the tutorial [Create an iOS App].</span><span class="sxs-lookup"><span data-stu-id="48b62-109">If this is your first experience with Mobile Apps, you should first complete the tutorial [Create an iOS App].</span></span> <span data-ttu-id="48b62-110">If you do not use the downloaded quick-start server project, you must add the data-access extension packages to your project.</span><span class="sxs-lookup"><span data-stu-id="48b62-110">If you do not use the downloaded quick-start server project, you must add the data-access extension packages to your project.</span></span> <span data-ttu-id="48b62-111">For more information about server extension packages, see [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="48b62-111">For more information about server extension packages, see [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

<span data-ttu-id="48b62-112">To learn more about the offline sync feature, see [Offline Data Sync in Mobile Apps].</span><span class="sxs-lookup"><span data-stu-id="48b62-112">To learn more about the offline sync feature, see [Offline Data Sync in Mobile Apps].</span></span>

## <a name="review-sync"></a><span data-ttu-id="48b62-113">Review the client sync code</span><span class="sxs-lookup"><span data-stu-id="48b62-113">Review the client sync code</span></span>
<span data-ttu-id="48b62-114">The client project that you downloaded for the [Create an iOS App] tutorial already contains code that supports offline synchronization using a local Core Data-based database.</span><span class="sxs-lookup"><span data-stu-id="48b62-114">The client project that you downloaded for the [Create an iOS App] tutorial already contains code that supports offline synchronization using a local Core Data-based database.</span></span> <span data-ttu-id="48b62-115">This section summarizes what is already included in the tutorial code.</span><span class="sxs-lookup"><span data-stu-id="48b62-115">This section summarizes what is already included in the tutorial code.</span></span> <span data-ttu-id="48b62-116">For a conceptual overview of the feature, see [Offline Data Sync in Mobile Apps].</span><span class="sxs-lookup"><span data-stu-id="48b62-116">For a conceptual overview of the feature, see [Offline Data Sync in Mobile Apps].</span></span>

<span data-ttu-id="48b62-117">Using the offline data-sync feature of Mobile Apps, end-users can interact with a local database even when the network is inaccessible.</span><span class="sxs-lookup"><span data-stu-id="48b62-117">Using the offline data-sync feature of Mobile Apps, end-users can interact with a local database even when the network is inaccessible.</span></span> <span data-ttu-id="48b62-118">To use these features in your app, you initialize the sync context of `MSClient` and reference a local store.</span><span class="sxs-lookup"><span data-stu-id="48b62-118">To use these features in your app, you initialize the sync context of `MSClient` and reference a local store.</span></span> <span data-ttu-id="48b62-119">Then you reference your table through the **MSSyncTable** interface.</span><span class="sxs-lookup"><span data-stu-id="48b62-119">Then you reference your table through the **MSSyncTable** interface.</span></span>

<span data-ttu-id="48b62-120">In **QSTodoService.m** (Objective-C) or **ToDoTableViewController.swift** (Swift), notice that the type of the member **syncTable** is **MSSyncTable**.</span><span class="sxs-lookup"><span data-stu-id="48b62-120">In **QSTodoService.m** (Objective-C) or **ToDoTableViewController.swift** (Swift), notice that the type of the member **syncTable** is **MSSyncTable**.</span></span> <span data-ttu-id="48b62-121">Offline sync uses this sync table interface instead of **MSTable**.</span><span class="sxs-lookup"><span data-stu-id="48b62-121">Offline sync uses this sync table interface instead of **MSTable**.</span></span> <span data-ttu-id="48b62-122">When a sync table is used, all operations go to the local store and are synchronized only with the remote back end with explicit push and pull operations.</span><span class="sxs-lookup"><span data-stu-id="48b62-122">When a sync table is used, all operations go to the local store and are synchronized only with the remote back end with explicit push and pull operations.</span></span>

 <span data-ttu-id="48b62-123">To get a reference to a sync table, use the **syncTableWithName** method on `MSClient`.</span><span class="sxs-lookup"><span data-stu-id="48b62-123">To get a reference to a sync table, use the **syncTableWithName** method on `MSClient`.</span></span> <span data-ttu-id="48b62-124">To remove offline sync functionality, use **tableWithName** instead.</span><span class="sxs-lookup"><span data-stu-id="48b62-124">To remove offline sync functionality, use **tableWithName** instead.</span></span>

<span data-ttu-id="48b62-125">Before any table operations can be performed, the local store must be initialized.</span><span class="sxs-lookup"><span data-stu-id="48b62-125">Before any table operations can be performed, the local store must be initialized.</span></span> <span data-ttu-id="48b62-126">Here is the relevant code:</span><span class="sxs-lookup"><span data-stu-id="48b62-126">Here is the relevant code:</span></span>

* <span data-ttu-id="48b62-127">**Objective-C**.</span><span class="sxs-lookup"><span data-stu-id="48b62-127">**Objective-C**.</span></span> <span data-ttu-id="48b62-128">In the **QSTodoService.init** method:</span><span class="sxs-lookup"><span data-stu-id="48b62-128">In the **QSTodoService.init** method:</span></span>

   ```objc
   MSCoreDataStore *store = [[MSCoreDataStore alloc] initWithManagedObjectContext:context];
   self.client.syncContext = [[MSSyncContext alloc] initWithDelegate:nil dataSource:store callback:nil];
   ```    
* <span data-ttu-id="48b62-129">**Swift**.</span><span class="sxs-lookup"><span data-stu-id="48b62-129">**Swift**.</span></span> <span data-ttu-id="48b62-130">In the **ToDoTableViewController.viewDidLoad** method:</span><span class="sxs-lookup"><span data-stu-id="48b62-130">In the **ToDoTableViewController.viewDidLoad** method:</span></span>

   ```swift
   let client = MSClient(applicationURLString: "http:// ...") // URI of the Mobile App
   let managedObjectContext = (UIApplication.sharedApplication().delegate as! AppDelegate).managedObjectContext!
   self.store = MSCoreDataStore(managedObjectContext: managedObjectContext)
   client.syncContext = MSSyncContext(delegate: nil, dataSource: self.store, callback: nil)
   ```
   <span data-ttu-id="48b62-131">This method creates a local store by using the `MSCoreDataStore` interface, which the Mobile Apps SDK provides.</span><span class="sxs-lookup"><span data-stu-id="48b62-131">This method creates a local store by using the `MSCoreDataStore` interface, which the Mobile Apps SDK provides.</span></span> <span data-ttu-id="48b62-132">Alternatively, you can provide a different local store by implementing the `MSSyncContextDataSource` protocol.</span><span class="sxs-lookup"><span data-stu-id="48b62-132">Alternatively, you can provide a different local store by implementing the `MSSyncContextDataSource` protocol.</span></span> <span data-ttu-id="48b62-133">Also, the first parameter of **MSSyncContext** is used to specify a conflict handler.</span><span class="sxs-lookup"><span data-stu-id="48b62-133">Also, the first parameter of **MSSyncContext** is used to specify a conflict handler.</span></span> <span data-ttu-id="48b62-134">Because we have passed `nil`, we get the default conflict handler, which fails on any conflict.</span><span class="sxs-lookup"><span data-stu-id="48b62-134">Because we have passed `nil`, we get the default conflict handler, which fails on any conflict.</span></span>

<span data-ttu-id="48b62-135">Now, let's perform the actual sync operation, and get data from the remote back end:</span><span class="sxs-lookup"><span data-stu-id="48b62-135">Now, let's perform the actual sync operation, and get data from the remote back end:</span></span>

* <span data-ttu-id="48b62-136">**Objective-C**.</span><span class="sxs-lookup"><span data-stu-id="48b62-136">**Objective-C**.</span></span> <span data-ttu-id="48b62-137">`syncData` first pushes new changes and then calls **pullData** to get data from the remote back end.</span><span class="sxs-lookup"><span data-stu-id="48b62-137">`syncData` first pushes new changes and then calls **pullData** to get data from the remote back end.</span></span> <span data-ttu-id="48b62-138">In turn, the **pullData** method gets new data that matches a query:</span><span class="sxs-lookup"><span data-stu-id="48b62-138">In turn, the **pullData** method gets new data that matches a query:</span></span>

   ```objc
   -(void)syncData:(QSCompletionBlock)completion
   {
       // Push all changes in the sync context, and then pull new data.
       [self.client.syncContext pushWithCompletion:^(NSError *error) {
           [self logErrorIfNotNil:error];
           [self pullData:completion];
       }];
   }

   -(void)pullData:(QSCompletionBlock)completion
   {
       MSQuery *query = [self.syncTable query];

       // Pulls data from the remote server into the local table.
       // We're pulling all items and filtering in the view.
       // Query ID is used for incremental sync.
       [self.syncTable pullWithQuery:query queryId:@"allTodoItems" completion:^(NSError *error) {
           [self logErrorIfNotNil:error];

           // Lets the caller know that we have finished.
           if (completion != nil) {
               dispatch_async(dispatch_get_main_queue(), completion);
           }
       }];
   }
   ```
* <span data-ttu-id="48b62-139">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="48b62-139">**Swift**:</span></span>
   ```swift
   func onRefresh(sender: UIRefreshControl!) {
      UIApplication.sharedApplication().networkActivityIndicatorVisible = true

      self.table!.pullWithQuery(self.table?.query(), queryId: "AllRecords") {
          (error) -> Void in

          UIApplication.sharedApplication().networkActivityIndicatorVisible = false

          if error != nil {
              // A real application would handle various errors like network conditions,
              // server conflicts, etc via the MSSyncContextDelegate
              print("Error: \(error!.description)")

              // We will discard our changes and keep the server's copy for simplicity
              if let opErrors = error!.userInfo[MSErrorPushResultKey] as? Array<MSTableOperationError> {
                  for opError in opErrors {
                      print("Attempted operation to item \(opError.itemId)")
                      if (opError.operation == .Insert || opError.operation == .Delete) {
                          print("Insert/Delete, failed discarding changes")
                          opError.cancelOperationAndDiscardItemWithCompletion(nil)
                      } else {
                          print("Update failed, reverting to server's copy")
                          opError.cancelOperationAndUpdateItem(opError.serverItem!, completion: nil)
                      }
                  }
              }
          }
          self.refreshControl?.endRefreshing()
      }
   }
   ```

<span data-ttu-id="48b62-140">In the Objective-C version, in `syncData`, we first call **pushWithCompletion** on the sync context.</span><span class="sxs-lookup"><span data-stu-id="48b62-140">In the Objective-C version, in `syncData`, we first call **pushWithCompletion** on the sync context.</span></span> <span data-ttu-id="48b62-141">This method is a member of `MSSyncContext` (and not the sync table itself) because it pushes changes across all tables.</span><span class="sxs-lookup"><span data-stu-id="48b62-141">This method is a member of `MSSyncContext` (and not the sync table itself) because it pushes changes across all tables.</span></span> <span data-ttu-id="48b62-142">Only records that have been modified in some way locally (through CUD operations) are sent to the server.</span><span class="sxs-lookup"><span data-stu-id="48b62-142">Only records that have been modified in some way locally (through CUD operations) are sent to the server.</span></span> <span data-ttu-id="48b62-143">Then the helper **pullData** is called, which calls **MSSyncTable.pullWithQuery** to retrieve remote data and store it in the local database.</span><span class="sxs-lookup"><span data-stu-id="48b62-143">Then the helper **pullData** is called, which calls **MSSyncTable.pullWithQuery** to retrieve remote data and store it in the local database.</span></span>

<span data-ttu-id="48b62-144">In the Swift version, because the push operation was not strictly necessary, there is no call to **pushWithCompletion**.</span><span class="sxs-lookup"><span data-stu-id="48b62-144">In the Swift version, because the push operation was not strictly necessary, there is no call to **pushWithCompletion**.</span></span> <span data-ttu-id="48b62-145">If there are any changes pending in the sync context for the table that is doing a push operation, pull always issues a push first.</span><span class="sxs-lookup"><span data-stu-id="48b62-145">If there are any changes pending in the sync context for the table that is doing a push operation, pull always issues a push first.</span></span> <span data-ttu-id="48b62-146">However, if you have more than one sync table, it is best to explicitly call push to ensure that everything is consistent across related tables.</span><span class="sxs-lookup"><span data-stu-id="48b62-146">However, if you have more than one sync table, it is best to explicitly call push to ensure that everything is consistent across related tables.</span></span>

<span data-ttu-id="48b62-147">In both the Objective-C and Swift versions, you can use the **pullWithQuery** method to specify a query to filter the records you want to retrieve.</span><span class="sxs-lookup"><span data-stu-id="48b62-147">In both the Objective-C and Swift versions, you can use the **pullWithQuery** method to specify a query to filter the records you want to retrieve.</span></span> <span data-ttu-id="48b62-148">In this example, the query retrieves all records in the remote `TodoItem` table.</span><span class="sxs-lookup"><span data-stu-id="48b62-148">In this example, the query retrieves all records in the remote `TodoItem` table.</span></span>

<span data-ttu-id="48b62-149">The second parameter of **pullWithQuery** is a query ID that is used for *incremental sync*. Incremental sync retrieves only records that were modified since the last sync, using the record's `UpdatedAt` time stamp (called `updatedAt` in the local store.) The query ID should be a descriptive string that is unique for each logical query in your app.</span><span class="sxs-lookup"><span data-stu-id="48b62-149">The second parameter of **pullWithQuery** is a query ID that is used for *incremental sync*. Incremental sync retrieves only records that were modified since the last sync, using the record's `UpdatedAt` time stamp (called `updatedAt` in the local store.) The query ID should be a descriptive string that is unique for each logical query in your app.</span></span> <span data-ttu-id="48b62-150">To opt out of incremental sync, pass `nil` as the query ID.</span><span class="sxs-lookup"><span data-stu-id="48b62-150">To opt out of incremental sync, pass `nil` as the query ID.</span></span> <span data-ttu-id="48b62-151">This approach can be potentially inefficient, because it retrieves all records on each pull operation.</span><span class="sxs-lookup"><span data-stu-id="48b62-151">This approach can be potentially inefficient, because it retrieves all records on each pull operation.</span></span>

<span data-ttu-id="48b62-152">The Objective-C app syncs when you modify or add data, when a user performs the refresh gesture, and on launch.</span><span class="sxs-lookup"><span data-stu-id="48b62-152">The Objective-C app syncs when you modify or add data, when a user performs the refresh gesture, and on launch.</span></span>

<span data-ttu-id="48b62-153">The Swift app syncs when the user performs the refresh gesture and on launch.</span><span class="sxs-lookup"><span data-stu-id="48b62-153">The Swift app syncs when the user performs the refresh gesture and on launch.</span></span>

<span data-ttu-id="48b62-154">Because the app syncs whenever data is modified (Objective-C) or whenever the app starts (Objective-C and Swift), the app assumes that the user is online.</span><span class="sxs-lookup"><span data-stu-id="48b62-154">Because the app syncs whenever data is modified (Objective-C) or whenever the app starts (Objective-C and Swift), the app assumes that the user is online.</span></span> <span data-ttu-id="48b62-155">In a later section, you will update the app so that users can edit even when they are offline.</span><span class="sxs-lookup"><span data-stu-id="48b62-155">In a later section, you will update the app so that users can edit even when they are offline.</span></span>

## <a name="review-core-data"></a><span data-ttu-id="48b62-156">Review the Core Data model</span><span class="sxs-lookup"><span data-stu-id="48b62-156">Review the Core Data model</span></span>
<span data-ttu-id="48b62-157">When you use the Core Data offline store, you must define particular tables and fields in your data model.</span><span class="sxs-lookup"><span data-stu-id="48b62-157">When you use the Core Data offline store, you must define particular tables and fields in your data model.</span></span> <span data-ttu-id="48b62-158">The sample app already includes a data model with the right format.</span><span class="sxs-lookup"><span data-stu-id="48b62-158">The sample app already includes a data model with the right format.</span></span> <span data-ttu-id="48b62-159">In this section, we walk through these tables to show how they are used.</span><span class="sxs-lookup"><span data-stu-id="48b62-159">In this section, we walk through these tables to show how they are used.</span></span>

<span data-ttu-id="48b62-160">Open **QSDataModel.xcdatamodeld**.</span><span class="sxs-lookup"><span data-stu-id="48b62-160">Open **QSDataModel.xcdatamodeld**.</span></span> <span data-ttu-id="48b62-161">Four tables are defined--three that are used by the SDK and one that's used for the to-do items themselves:</span><span class="sxs-lookup"><span data-stu-id="48b62-161">Four tables are defined--three that are used by the SDK and one that's used for the to-do items themselves:</span></span>
  * <span data-ttu-id="48b62-162">MS_TableOperations: Tracks the items that need to be synchronized with the server.</span><span class="sxs-lookup"><span data-stu-id="48b62-162">MS_TableOperations: Tracks the items that need to be synchronized with the server.</span></span>
  * <span data-ttu-id="48b62-163">MS_TableOperationErrors: Tracks any errors that happen during offline synchronization.</span><span class="sxs-lookup"><span data-stu-id="48b62-163">MS_TableOperationErrors: Tracks any errors that happen during offline synchronization.</span></span>
  * <span data-ttu-id="48b62-164">MS_TableConfig: Tracks the last updated time for the last sync operation for all pull operations.</span><span class="sxs-lookup"><span data-stu-id="48b62-164">MS_TableConfig: Tracks the last updated time for the last sync operation for all pull operations.</span></span>
  * <span data-ttu-id="48b62-165">TodoItem: Stores the to-do items.</span><span class="sxs-lookup"><span data-stu-id="48b62-165">TodoItem: Stores the to-do items.</span></span> <span data-ttu-id="48b62-166">The system columns **createdAt**, **updatedAt**, and **version** are optional system properties.</span><span class="sxs-lookup"><span data-stu-id="48b62-166">The system columns **createdAt**, **updatedAt**, and **version** are optional system properties.</span></span>

> [!NOTE]
> <span data-ttu-id="48b62-167">The Mobile Apps SDK reserves column names that begin with "**\`\`**".</span><span class="sxs-lookup"><span data-stu-id="48b62-167">The Mobile Apps SDK reserves column names that begin with "**\`\`**".</span></span> <span data-ttu-id="48b62-168">Do not use this prefix with anything other than system columns.</span><span class="sxs-lookup"><span data-stu-id="48b62-168">Do not use this prefix with anything other than system columns.</span></span> <span data-ttu-id="48b62-169">Otherwise, your column names are modified when you use the remote back end.</span><span class="sxs-lookup"><span data-stu-id="48b62-169">Otherwise, your column names are modified when you use the remote back end.</span></span>
>
>

<span data-ttu-id="48b62-170">When you use the offline sync feature, define the three system tables and the data table.</span><span class="sxs-lookup"><span data-stu-id="48b62-170">When you use the offline sync feature, define the three system tables and the data table.</span></span>

### <a name="system-tables"></a><span data-ttu-id="48b62-171">System tables</span><span class="sxs-lookup"><span data-stu-id="48b62-171">System tables</span></span>

<span data-ttu-id="48b62-172">**MS_TableOperations**</span><span class="sxs-lookup"><span data-stu-id="48b62-172">**MS_TableOperations**</span></span>  

![MS_TableOperations table attributes][defining-core-data-tableoperations-entity]

| <span data-ttu-id="48b62-174">Attribute</span><span class="sxs-lookup"><span data-stu-id="48b62-174">Attribute</span></span> | <span data-ttu-id="48b62-175">Type</span><span class="sxs-lookup"><span data-stu-id="48b62-175">Type</span></span> |
| --- | --- |
| <span data-ttu-id="48b62-176">id</span><span class="sxs-lookup"><span data-stu-id="48b62-176">id</span></span> | <span data-ttu-id="48b62-177">Integer 64</span><span class="sxs-lookup"><span data-stu-id="48b62-177">Integer 64</span></span> |
| <span data-ttu-id="48b62-178">itemId</span><span class="sxs-lookup"><span data-stu-id="48b62-178">itemId</span></span> | <span data-ttu-id="48b62-179">String</span><span class="sxs-lookup"><span data-stu-id="48b62-179">String</span></span> |
| <span data-ttu-id="48b62-180">properties</span><span class="sxs-lookup"><span data-stu-id="48b62-180">properties</span></span> | <span data-ttu-id="48b62-181">Binary Data</span><span class="sxs-lookup"><span data-stu-id="48b62-181">Binary Data</span></span> |
| <span data-ttu-id="48b62-182">table</span><span class="sxs-lookup"><span data-stu-id="48b62-182">table</span></span> | <span data-ttu-id="48b62-183">String</span><span class="sxs-lookup"><span data-stu-id="48b62-183">String</span></span> |
| <span data-ttu-id="48b62-184">tableKind</span><span class="sxs-lookup"><span data-stu-id="48b62-184">tableKind</span></span> | <span data-ttu-id="48b62-185">Integer 16</span><span class="sxs-lookup"><span data-stu-id="48b62-185">Integer 16</span></span> |


<span data-ttu-id="48b62-186">**MS_TableOperationErrors**</span><span class="sxs-lookup"><span data-stu-id="48b62-186">**MS_TableOperationErrors**</span></span>

 ![MS_TableOperationErrors table attributes][defining-core-data-tableoperationerrors-entity]

| <span data-ttu-id="48b62-188">Attribute</span><span class="sxs-lookup"><span data-stu-id="48b62-188">Attribute</span></span> | <span data-ttu-id="48b62-189">Type</span><span class="sxs-lookup"><span data-stu-id="48b62-189">Type</span></span> |
| --- | --- |
| <span data-ttu-id="48b62-190">id</span><span class="sxs-lookup"><span data-stu-id="48b62-190">id</span></span> |<span data-ttu-id="48b62-191">String</span><span class="sxs-lookup"><span data-stu-id="48b62-191">String</span></span> |
| <span data-ttu-id="48b62-192">operationId</span><span class="sxs-lookup"><span data-stu-id="48b62-192">operationId</span></span> |<span data-ttu-id="48b62-193">Integer 64</span><span class="sxs-lookup"><span data-stu-id="48b62-193">Integer 64</span></span> |
| <span data-ttu-id="48b62-194">properties</span><span class="sxs-lookup"><span data-stu-id="48b62-194">properties</span></span> |<span data-ttu-id="48b62-195">Binary Data</span><span class="sxs-lookup"><span data-stu-id="48b62-195">Binary Data</span></span> |
| <span data-ttu-id="48b62-196">tableKind</span><span class="sxs-lookup"><span data-stu-id="48b62-196">tableKind</span></span> |<span data-ttu-id="48b62-197">Integer 16</span><span class="sxs-lookup"><span data-stu-id="48b62-197">Integer 16</span></span> |

 <span data-ttu-id="48b62-198">**MS_TableConfig**</span><span class="sxs-lookup"><span data-stu-id="48b62-198">**MS_TableConfig**</span></span>

 ![][defining-core-data-tableconfig-entity]

| <span data-ttu-id="48b62-199">Attribute</span><span class="sxs-lookup"><span data-stu-id="48b62-199">Attribute</span></span> | <span data-ttu-id="48b62-200">Type</span><span class="sxs-lookup"><span data-stu-id="48b62-200">Type</span></span> |
| --- | --- |
| <span data-ttu-id="48b62-201">id</span><span class="sxs-lookup"><span data-stu-id="48b62-201">id</span></span> |<span data-ttu-id="48b62-202">String</span><span class="sxs-lookup"><span data-stu-id="48b62-202">String</span></span> |
| <span data-ttu-id="48b62-203">key</span><span class="sxs-lookup"><span data-stu-id="48b62-203">key</span></span> |<span data-ttu-id="48b62-204">String</span><span class="sxs-lookup"><span data-stu-id="48b62-204">String</span></span> |
| <span data-ttu-id="48b62-205">keyType</span><span class="sxs-lookup"><span data-stu-id="48b62-205">keyType</span></span> |<span data-ttu-id="48b62-206">Integer 64</span><span class="sxs-lookup"><span data-stu-id="48b62-206">Integer 64</span></span> |
| <span data-ttu-id="48b62-207">table</span><span class="sxs-lookup"><span data-stu-id="48b62-207">table</span></span> |<span data-ttu-id="48b62-208">String</span><span class="sxs-lookup"><span data-stu-id="48b62-208">String</span></span> |
| <span data-ttu-id="48b62-209">value</span><span class="sxs-lookup"><span data-stu-id="48b62-209">value</span></span> |<span data-ttu-id="48b62-210">String</span><span class="sxs-lookup"><span data-stu-id="48b62-210">String</span></span> |

### <a name="data-table"></a><span data-ttu-id="48b62-211">Data table</span><span class="sxs-lookup"><span data-stu-id="48b62-211">Data table</span></span>

<span data-ttu-id="48b62-212">**TodoItem**</span><span class="sxs-lookup"><span data-stu-id="48b62-212">**TodoItem**</span></span>

| <span data-ttu-id="48b62-213">Attribute</span><span class="sxs-lookup"><span data-stu-id="48b62-213">Attribute</span></span> | <span data-ttu-id="48b62-214">Type</span><span class="sxs-lookup"><span data-stu-id="48b62-214">Type</span></span> | <span data-ttu-id="48b62-215">Note</span><span class="sxs-lookup"><span data-stu-id="48b62-215">Note</span></span> |
| --- | --- | --- |
| <span data-ttu-id="48b62-216">id</span><span class="sxs-lookup"><span data-stu-id="48b62-216">id</span></span> | <span data-ttu-id="48b62-217">String, marked required</span><span class="sxs-lookup"><span data-stu-id="48b62-217">String, marked required</span></span> |<span data-ttu-id="48b62-218">Primary key in remote store</span><span class="sxs-lookup"><span data-stu-id="48b62-218">Primary key in remote store</span></span> |
| <span data-ttu-id="48b62-219">complete</span><span class="sxs-lookup"><span data-stu-id="48b62-219">complete</span></span> | <span data-ttu-id="48b62-220">Boolean</span><span class="sxs-lookup"><span data-stu-id="48b62-220">Boolean</span></span> | <span data-ttu-id="48b62-221">To-do item field</span><span class="sxs-lookup"><span data-stu-id="48b62-221">To-do item field</span></span> |
| <span data-ttu-id="48b62-222">text</span><span class="sxs-lookup"><span data-stu-id="48b62-222">text</span></span> |<span data-ttu-id="48b62-223">String</span><span class="sxs-lookup"><span data-stu-id="48b62-223">String</span></span> |<span data-ttu-id="48b62-224">To-do item field</span><span class="sxs-lookup"><span data-stu-id="48b62-224">To-do item field</span></span> |
| <span data-ttu-id="48b62-225">createdAt</span><span class="sxs-lookup"><span data-stu-id="48b62-225">createdAt</span></span> | <span data-ttu-id="48b62-226">Date</span><span class="sxs-lookup"><span data-stu-id="48b62-226">Date</span></span> | <span data-ttu-id="48b62-227">(optional) Maps to **createdAt** system property</span><span class="sxs-lookup"><span data-stu-id="48b62-227">(optional) Maps to **createdAt** system property</span></span> |
| <span data-ttu-id="48b62-228">updatedAt</span><span class="sxs-lookup"><span data-stu-id="48b62-228">updatedAt</span></span> | <span data-ttu-id="48b62-229">Date</span><span class="sxs-lookup"><span data-stu-id="48b62-229">Date</span></span> | <span data-ttu-id="48b62-230">(optional) Maps to **updatedAt** system property</span><span class="sxs-lookup"><span data-stu-id="48b62-230">(optional) Maps to **updatedAt** system property</span></span> |
| <span data-ttu-id="48b62-231">version</span><span class="sxs-lookup"><span data-stu-id="48b62-231">version</span></span> | <span data-ttu-id="48b62-232">String</span><span class="sxs-lookup"><span data-stu-id="48b62-232">String</span></span> | <span data-ttu-id="48b62-233">(optional) Used to detect conflicts, maps to version</span><span class="sxs-lookup"><span data-stu-id="48b62-233">(optional) Used to detect conflicts, maps to version</span></span> |

## <a name="setup-sync"></a><span data-ttu-id="48b62-234">Change the sync behavior of the app</span><span class="sxs-lookup"><span data-stu-id="48b62-234">Change the sync behavior of the app</span></span>
<span data-ttu-id="48b62-235">In this section, you modify the app so that it does not sync on app start or when you insert and update items.</span><span class="sxs-lookup"><span data-stu-id="48b62-235">In this section, you modify the app so that it does not sync on app start or when you insert and update items.</span></span> <span data-ttu-id="48b62-236">It syncs only when the refresh gesture button is performed.</span><span class="sxs-lookup"><span data-stu-id="48b62-236">It syncs only when the refresh gesture button is performed.</span></span>

<span data-ttu-id="48b62-237">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="48b62-237">**Objective-C**:</span></span>

1. <span data-ttu-id="48b62-238">In **QSTodoListViewController.m**, change the **viewDidLoad** method to remove the call to `[self refresh]` at the end of the method.</span><span class="sxs-lookup"><span data-stu-id="48b62-238">In **QSTodoListViewController.m**, change the **viewDidLoad** method to remove the call to `[self refresh]` at the end of the method.</span></span> <span data-ttu-id="48b62-239">Now the data is not synced with the server on app start.</span><span class="sxs-lookup"><span data-stu-id="48b62-239">Now the data is not synced with the server on app start.</span></span> <span data-ttu-id="48b62-240">Instead, it's synced with the contents of the local store.</span><span class="sxs-lookup"><span data-stu-id="48b62-240">Instead, it's synced with the contents of the local store.</span></span>
2. <span data-ttu-id="48b62-241">In **QSTodoService.m**, modify the definition of `addItem` so that it doesn't sync after the item is inserted.</span><span class="sxs-lookup"><span data-stu-id="48b62-241">In **QSTodoService.m**, modify the definition of `addItem` so that it doesn't sync after the item is inserted.</span></span> <span data-ttu-id="48b62-242">Remove the `self syncData` block and replace it with the following:</span><span class="sxs-lookup"><span data-stu-id="48b62-242">Remove the `self syncData` block and replace it with the following:</span></span>

   ```objc
   if (completion != nil) {
       dispatch_async(dispatch_get_main_queue(), completion);
   }
   ```
3. <span data-ttu-id="48b62-243">Modify the definition of `completeItem` as mentioned previously.</span><span class="sxs-lookup"><span data-stu-id="48b62-243">Modify the definition of `completeItem` as mentioned previously.</span></span> <span data-ttu-id="48b62-244">Remove the block for `self syncData` and replace it with the following:</span><span class="sxs-lookup"><span data-stu-id="48b62-244">Remove the block for `self syncData` and replace it with the following:</span></span>
   ```objc
   if (completion != nil) {
       dispatch_async(dispatch_get_main_queue(), completion);
   }
   ```

<span data-ttu-id="48b62-245">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="48b62-245">**Swift**:</span></span>

<span data-ttu-id="48b62-246">In `viewDidLoad`, in **ToDoTableViewController.swift**, comment out the two lines shown here, to stop syncing on app start.</span><span class="sxs-lookup"><span data-stu-id="48b62-246">In `viewDidLoad`, in **ToDoTableViewController.swift**, comment out the two lines shown here, to stop syncing on app start.</span></span> <span data-ttu-id="48b62-247">At the time of this writing, the Swift Todo app does not update the service when someone adds or completes an item.</span><span class="sxs-lookup"><span data-stu-id="48b62-247">At the time of this writing, the Swift Todo app does not update the service when someone adds or completes an item.</span></span> <span data-ttu-id="48b62-248">It updates the service only on app start.</span><span class="sxs-lookup"><span data-stu-id="48b62-248">It updates the service only on app start.</span></span>

   ```swift
  self.refreshControl?.beginRefreshing()
  self.onRefresh(self.refreshControl)
```

## <a name="test-app"></a><span data-ttu-id="48b62-249">Test the app</span><span class="sxs-lookup"><span data-stu-id="48b62-249">Test the app</span></span>
<span data-ttu-id="48b62-250">In this section, you connect to an invalid URL to simulate an offline scenario.</span><span class="sxs-lookup"><span data-stu-id="48b62-250">In this section, you connect to an invalid URL to simulate an offline scenario.</span></span> <span data-ttu-id="48b62-251">When you add data items, they're held in the local Core Data store, but they're not synced with the mobile-app back end.</span><span class="sxs-lookup"><span data-stu-id="48b62-251">When you add data items, they're held in the local Core Data store, but they're not synced with the mobile-app back end.</span></span>

1. <span data-ttu-id="48b62-252">Change the mobile-app URL in **QSTodoService.m** to an invalid URL, and run the app again:</span><span class="sxs-lookup"><span data-stu-id="48b62-252">Change the mobile-app URL in **QSTodoService.m** to an invalid URL, and run the app again:</span></span>

   <span data-ttu-id="48b62-253">**Objective-C**.</span><span class="sxs-lookup"><span data-stu-id="48b62-253">**Objective-C**.</span></span> <span data-ttu-id="48b62-254">In QSTodoService.m:</span><span class="sxs-lookup"><span data-stu-id="48b62-254">In QSTodoService.m:</span></span>
   ```objc
   self.client = [MSClient clientWithApplicationURLString:@"https://sitename.azurewebsites.net.fail"];
   ```
   <span data-ttu-id="48b62-255">**Swift**.</span><span class="sxs-lookup"><span data-stu-id="48b62-255">**Swift**.</span></span> <span data-ttu-id="48b62-256">In ToDoTableViewController.swift:</span><span class="sxs-lookup"><span data-stu-id="48b62-256">In ToDoTableViewController.swift:</span></span>
   ```swift
   let client = MSClient(applicationURLString: "https://sitename.azurewebsites.net.fail")
   ```
2. <span data-ttu-id="48b62-257">Add some to-do items.</span><span class="sxs-lookup"><span data-stu-id="48b62-257">Add some to-do items.</span></span> <span data-ttu-id="48b62-258">Quit the simulator (or forcibly close the app), and then restart it.</span><span class="sxs-lookup"><span data-stu-id="48b62-258">Quit the simulator (or forcibly close the app), and then restart it.</span></span> <span data-ttu-id="48b62-259">Verify that your changes persist.</span><span class="sxs-lookup"><span data-stu-id="48b62-259">Verify that your changes persist.</span></span>

3. <span data-ttu-id="48b62-260">View the contents of the remote **TodoItem** table:</span><span class="sxs-lookup"><span data-stu-id="48b62-260">View the contents of the remote **TodoItem** table:</span></span>
   * <span data-ttu-id="48b62-261">For a Node.js back end, go to the [Azure portal](https://portal.azure.com/) and, in your mobile-app back end, click **Easy Tables** > **TodoItem**.</span><span class="sxs-lookup"><span data-stu-id="48b62-261">For a Node.js back end, go to the [Azure portal](https://portal.azure.com/) and, in your mobile-app back end, click **Easy Tables** > **TodoItem**.</span></span>  
   * <span data-ttu-id="48b62-262">For a .NET back end, use either a SQL tool, such as SQL Server Management Studio, or a REST client, such as Fiddler or Postman.</span><span class="sxs-lookup"><span data-stu-id="48b62-262">For a .NET back end, use either a SQL tool, such as SQL Server Management Studio, or a REST client, such as Fiddler or Postman.</span></span>  

4. <span data-ttu-id="48b62-263">Verify that the new items have *not* been synced with the server.</span><span class="sxs-lookup"><span data-stu-id="48b62-263">Verify that the new items have *not* been synced with the server.</span></span>

5. <span data-ttu-id="48b62-264">Change the URL back to the correct one in **QSTodoService.m**, and rerun the app.</span><span class="sxs-lookup"><span data-stu-id="48b62-264">Change the URL back to the correct one in **QSTodoService.m**, and rerun the app.</span></span>

6. <span data-ttu-id="48b62-265">Perform the refresh gesture by pulling down the list of items.</span><span class="sxs-lookup"><span data-stu-id="48b62-265">Perform the refresh gesture by pulling down the list of items.</span></span>  
<span data-ttu-id="48b62-266">A progress spinner is displayed.</span><span class="sxs-lookup"><span data-stu-id="48b62-266">A progress spinner is displayed.</span></span>

7. <span data-ttu-id="48b62-267">View the **TodoItem** data again.</span><span class="sxs-lookup"><span data-stu-id="48b62-267">View the **TodoItem** data again.</span></span> <span data-ttu-id="48b62-268">The new and changed to-do items should now be displayed.</span><span class="sxs-lookup"><span data-stu-id="48b62-268">The new and changed to-do items should now be displayed.</span></span>

## <a name="summary"></a><span data-ttu-id="48b62-269">Summary</span><span class="sxs-lookup"><span data-stu-id="48b62-269">Summary</span></span>
<span data-ttu-id="48b62-270">To support the offline sync feature, we used the `MSSyncTable` interface and initialized `MSClient.syncContext` with a local store.</span><span class="sxs-lookup"><span data-stu-id="48b62-270">To support the offline sync feature, we used the `MSSyncTable` interface and initialized `MSClient.syncContext` with a local store.</span></span> <span data-ttu-id="48b62-271">In this case, the local store was a Core Data-based database.</span><span class="sxs-lookup"><span data-stu-id="48b62-271">In this case, the local store was a Core Data-based database.</span></span>

<span data-ttu-id="48b62-272">When you use a Core Data local store, you must define several tables with the [correct system properties](#review-core-data).</span><span class="sxs-lookup"><span data-stu-id="48b62-272">When you use a Core Data local store, you must define several tables with the [correct system properties](#review-core-data).</span></span>

<span data-ttu-id="48b62-273">The normal create, read, update, and delete (CRUD) operations for mobile apps work as if the app is still connected, but all the operations occur against the local store.</span><span class="sxs-lookup"><span data-stu-id="48b62-273">The normal create, read, update, and delete (CRUD) operations for mobile apps work as if the app is still connected, but all the operations occur against the local store.</span></span>

<span data-ttu-id="48b62-274">When we synchronized the local store with the server, we used the **MSSyncTable.pullWithQuery** method.</span><span class="sxs-lookup"><span data-stu-id="48b62-274">When we synchronized the local store with the server, we used the **MSSyncTable.pullWithQuery** method.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="48b62-275">Additional resources</span><span class="sxs-lookup"><span data-stu-id="48b62-275">Additional resources</span></span>
* <span data-ttu-id="48b62-276">[Offline Data Sync in Mobile Apps]</span><span class="sxs-lookup"><span data-stu-id="48b62-276">[Offline Data Sync in Mobile Apps]</span></span>
* <span data-ttu-id="48b62-277">[Cloud Cover: Offline Sync in Azure Mobile Services] \(The video is about Mobile Services, but Mobile Apps offline sync works in a similar way.\)</span><span class="sxs-lookup"><span data-stu-id="48b62-277">[Cloud Cover: Offline Sync in Azure Mobile Services] \(The video is about Mobile Services, but Mobile Apps offline sync works in a similar way.\)</span></span>

<!-- URLs. -->


[Create an iOS App]: app-service-mobile-ios-get-started.md
[Offline Data Sync in Mobile Apps]: app-service-mobile-offline-data-sync.md

[defining-core-data-tableoperationerrors-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableoperationerrors-entity.png
[defining-core-data-tableoperations-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableoperations-entity.png
[defining-core-data-tableconfig-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableconfig-entity.png
[defining-core-data-todoitem-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-todoitem-entity.png

[Cloud Cover: Offline Sync in Azure Mobile Services]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri
[Azure Friday: Offline-enabled apps in Azure Mobile Services]: http://azure.microsoft.com/documentation/videos/azure-mobile-services-offline-enabled-apps-with-donna-malayeri/
