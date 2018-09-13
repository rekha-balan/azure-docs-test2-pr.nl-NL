---
title: Enable offline sync for your Azure Mobile App (Xamarin Android)
description: Learn how to use App Service Mobile App to cache and sync offline data in your Xamarin Android application
documentationcenter: xamarin
author: adrianhall
manager: adrianha
editor: ''
services: app-service\mobile
ms.assetid: 91d59e4b-abaa-41f4-80cf-ee7933b32568
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: adrianha
ms.openlocfilehash: d2716581f247d8b1522297ea34b6488b128611e2
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554357"
---
# <a name="enable-offline-sync-for-your-xamarinandroid-mobile-app"></a><span data-ttu-id="085ec-103">Enable offline sync for your Xamarin.Android mobile app</span><span class="sxs-lookup"><span data-stu-id="085ec-103">Enable offline sync for your Xamarin.Android mobile app</span></span>
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a><span data-ttu-id="085ec-104">Overview</span><span class="sxs-lookup"><span data-stu-id="085ec-104">Overview</span></span>
<span data-ttu-id="085ec-105">This tutorial introduces the offline sync feature of Azure Mobile Apps for Xamarin.Android.</span><span class="sxs-lookup"><span data-stu-id="085ec-105">This tutorial introduces the offline sync feature of Azure Mobile Apps for Xamarin.Android.</span></span> <span data-ttu-id="085ec-106">Offline sync allows end users to interact with a mobile app--viewing, adding, or modifying data--even when there is no network connection.</span><span class="sxs-lookup"><span data-stu-id="085ec-106">Offline sync allows end users to interact with a mobile app--viewing, adding, or modifying data--even when there is no network connection.</span></span> <span data-ttu-id="085ec-107">Changes are stored in a local database.</span><span class="sxs-lookup"><span data-stu-id="085ec-107">Changes are stored in a local database.</span></span>
<span data-ttu-id="085ec-108">Once the device is back online, these changes are synced with the remote service.</span><span class="sxs-lookup"><span data-stu-id="085ec-108">Once the device is back online, these changes are synced with the remote service.</span></span>

<span data-ttu-id="085ec-109">In this tutorial, you update the client project from the tutorial [Create a Xamarin Android app] to support the offline features of Azure Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="085ec-109">In this tutorial, you update the client project from the tutorial [Create a Xamarin Android app] to support the offline features of Azure Mobile Apps.</span></span> <span data-ttu-id="085ec-110">If you do not use the downloaded quick start server project, you must add the data access extension packages to your project.</span><span class="sxs-lookup"><span data-stu-id="085ec-110">If you do not use the downloaded quick start server project, you must add the data access extension packages to your project.</span></span> <span data-ttu-id="085ec-111">For more information about server extension packages, see [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="085ec-111">For more information about server extension packages, see [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

<span data-ttu-id="085ec-112">To learn more about the offline sync feature, see the topic [Offline Data Sync in Azure Mobile Apps].</span><span class="sxs-lookup"><span data-stu-id="085ec-112">To learn more about the offline sync feature, see the topic [Offline Data Sync in Azure Mobile Apps].</span></span>

## <a name="update-the-client-app-to-support-offline-features"></a><span data-ttu-id="085ec-113">Update the client app to support offline features</span><span class="sxs-lookup"><span data-stu-id="085ec-113">Update the client app to support offline features</span></span>
<span data-ttu-id="085ec-114">Azure Mobile App offline features allow you to interact with a local database when you are in an offline scenario.</span><span class="sxs-lookup"><span data-stu-id="085ec-114">Azure Mobile App offline features allow you to interact with a local database when you are in an offline scenario.</span></span> <span data-ttu-id="085ec-115">To use these features in your app, you initialize a [SyncContext] to a local store.</span><span class="sxs-lookup"><span data-stu-id="085ec-115">To use these features in your app, you initialize a [SyncContext] to a local store.</span></span> <span data-ttu-id="085ec-116">Then reference your table through the [IMobileServiceSyncTable][IMobileServiceSyncTable] interface.</span><span class="sxs-lookup"><span data-stu-id="085ec-116">Then reference your table through the [IMobileServiceSyncTable][IMobileServiceSyncTable] interface.</span></span> <span data-ttu-id="085ec-117">SQLite is used as the local store on the device.</span><span class="sxs-lookup"><span data-stu-id="085ec-117">SQLite is used as the local store on the device.</span></span>

1. <span data-ttu-id="085ec-118">In Visual Studio, open the NuGet package manager in the project that you completed in the [Create a Xamarin Android app] tutorial.</span><span class="sxs-lookup"><span data-stu-id="085ec-118">In Visual Studio, open the NuGet package manager in the project that you completed in the [Create a Xamarin Android app] tutorial.</span></span>  <span data-ttu-id="085ec-119">Search for and install the **Microsoft.Azure.Mobile.Client.SQLiteStore** NuGet package.</span><span class="sxs-lookup"><span data-stu-id="085ec-119">Search for and install the **Microsoft.Azure.Mobile.Client.SQLiteStore** NuGet package.</span></span>
2. <span data-ttu-id="085ec-120">Open the ToDoActivity.cs file and uncomment the `#define OFFLINE_SYNC_ENABLED` definition.</span><span class="sxs-lookup"><span data-stu-id="085ec-120">Open the ToDoActivity.cs file and uncomment the `#define OFFLINE_SYNC_ENABLED` definition.</span></span>
3. <span data-ttu-id="085ec-121">In Visual Studio, press the **F5** key to rebuild and run the client app.</span><span class="sxs-lookup"><span data-stu-id="085ec-121">In Visual Studio, press the **F5** key to rebuild and run the client app.</span></span> <span data-ttu-id="085ec-122">The app works the same as it did before you enabled offline sync. However, the local database is now populated with data that can be used in an offline scenario.</span><span class="sxs-lookup"><span data-stu-id="085ec-122">The app works the same as it did before you enabled offline sync. However, the local database is now populated with data that can be used in an offline scenario.</span></span>

## <a name="update-sync"></a><span data-ttu-id="085ec-123">Update the app to disconnect from the backend</span><span class="sxs-lookup"><span data-stu-id="085ec-123">Update the app to disconnect from the backend</span></span>
<span data-ttu-id="085ec-124">In this section, you break the connection to your Mobile App backend to simulate an offline situation.</span><span class="sxs-lookup"><span data-stu-id="085ec-124">In this section, you break the connection to your Mobile App backend to simulate an offline situation.</span></span> <span data-ttu-id="085ec-125">When you add data items, your exception handler tells you that the app is in offline mode.</span><span class="sxs-lookup"><span data-stu-id="085ec-125">When you add data items, your exception handler tells you that the app is in offline mode.</span></span> <span data-ttu-id="085ec-126">In this state, new items added in the local store and are synced to the mobile app backend when a push is executed in a connected state.</span><span class="sxs-lookup"><span data-stu-id="085ec-126">In this state, new items added in the local store and are synced to the mobile app backend when a push is executed in a connected state.</span></span>

1. <span data-ttu-id="085ec-127">Edit ToDoActivity.cs in the shared project.</span><span class="sxs-lookup"><span data-stu-id="085ec-127">Edit ToDoActivity.cs in the shared project.</span></span> <span data-ttu-id="085ec-128">Change the **applicationURL** to point to an invalid URL:</span><span class="sxs-lookup"><span data-stu-id="085ec-128">Change the **applicationURL** to point to an invalid URL:</span></span>
   
         const string applicationURL = @"https://your-service.azurewebsites.fail";
   
    <span data-ttu-id="085ec-129">You can also demonstrate offline behavior by disabling wifi and cellular networks on the device or using airplane mode.</span><span class="sxs-lookup"><span data-stu-id="085ec-129">You can also demonstrate offline behavior by disabling wifi and cellular networks on the device or using airplane mode.</span></span>
2. <span data-ttu-id="085ec-130">Press **F5** to build and run the app.</span><span class="sxs-lookup"><span data-stu-id="085ec-130">Press **F5** to build and run the app.</span></span> <span data-ttu-id="085ec-131">Notice your sync failed on refresh when the app launched.</span><span class="sxs-lookup"><span data-stu-id="085ec-131">Notice your sync failed on refresh when the app launched.</span></span>
3. <span data-ttu-id="085ec-132">Enter new items and notice that push fails with a [CancelledByNetworkError] status each time you click **Save**.</span><span class="sxs-lookup"><span data-stu-id="085ec-132">Enter new items and notice that push fails with a [CancelledByNetworkError] status each time you click **Save**.</span></span> <span data-ttu-id="085ec-133">However, the new todo items exist in the local store until they can be pushed to the mobile app backend.</span><span class="sxs-lookup"><span data-stu-id="085ec-133">However, the new todo items exist in the local store until they can be pushed to the mobile app backend.</span></span>  <span data-ttu-id="085ec-134">In a production app, if you suppress these exceptions the client app behaves as if it's still connected to the mobile app backend.</span><span class="sxs-lookup"><span data-stu-id="085ec-134">In a production app, if you suppress these exceptions the client app behaves as if it's still connected to the mobile app backend.</span></span>
4. <span data-ttu-id="085ec-135">Close the app and restart it to verify that the new items you created are persisted to the local store.</span><span class="sxs-lookup"><span data-stu-id="085ec-135">Close the app and restart it to verify that the new items you created are persisted to the local store.</span></span>
5. <span data-ttu-id="085ec-136">(Optional) In Visual Studio, open **Server Explorer**.</span><span class="sxs-lookup"><span data-stu-id="085ec-136">(Optional) In Visual Studio, open **Server Explorer**.</span></span> <span data-ttu-id="085ec-137">Navigate to your database in **Azure**->**SQL Databases**.</span><span class="sxs-lookup"><span data-stu-id="085ec-137">Navigate to your database in **Azure**->**SQL Databases**.</span></span> <span data-ttu-id="085ec-138">Right-click your database and select **Open in SQL Server Object Explorer**.</span><span class="sxs-lookup"><span data-stu-id="085ec-138">Right-click your database and select **Open in SQL Server Object Explorer**.</span></span> <span data-ttu-id="085ec-139">Now you can browse to your SQL database table and its contents.</span><span class="sxs-lookup"><span data-stu-id="085ec-139">Now you can browse to your SQL database table and its contents.</span></span> <span data-ttu-id="085ec-140">Verify that the data in the backend database has not changed.</span><span class="sxs-lookup"><span data-stu-id="085ec-140">Verify that the data in the backend database has not changed.</span></span>
6. <span data-ttu-id="085ec-141">(Optional) Use a REST tool such as Fiddler or Postman to query your mobile backend, using a GET query in the form `https://<your-mobile-app-backend-name>.azurewebsites.net/tables/TodoItem`.</span><span class="sxs-lookup"><span data-stu-id="085ec-141">(Optional) Use a REST tool such as Fiddler or Postman to query your mobile backend, using a GET query in the form `https://<your-mobile-app-backend-name>.azurewebsites.net/tables/TodoItem`.</span></span>

## <a name="update-online-app"></a><span data-ttu-id="085ec-142">Update the app to reconnect your Mobile App backend</span><span class="sxs-lookup"><span data-stu-id="085ec-142">Update the app to reconnect your Mobile App backend</span></span>
<span data-ttu-id="085ec-143">In this section, reconnect the app to the mobile app backend.</span><span class="sxs-lookup"><span data-stu-id="085ec-143">In this section, reconnect the app to the mobile app backend.</span></span> <span data-ttu-id="085ec-144">When you first run the application, the `OnCreate` event handler calls `OnRefreshItemsSelected`.</span><span class="sxs-lookup"><span data-stu-id="085ec-144">When you first run the application, the `OnCreate` event handler calls `OnRefreshItemsSelected`.</span></span> <span data-ttu-id="085ec-145">This method calls `SyncAsync` to sync your local store with the backend database.</span><span class="sxs-lookup"><span data-stu-id="085ec-145">This method calls `SyncAsync` to sync your local store with the backend database.</span></span>

1. <span data-ttu-id="085ec-146">Open ToDoActivity.cs in the shared project, and revert your change of the **applicationURL** property.</span><span class="sxs-lookup"><span data-stu-id="085ec-146">Open ToDoActivity.cs in the shared project, and revert your change of the **applicationURL** property.</span></span>
2. <span data-ttu-id="085ec-147">Press the **F5** key to rebuild and run the app.</span><span class="sxs-lookup"><span data-stu-id="085ec-147">Press the **F5** key to rebuild and run the app.</span></span> <span data-ttu-id="085ec-148">The app syncs your local changes with the Azure Mobile App backend using push and pull operations when the `OnRefreshItemsSelected` method executes.</span><span class="sxs-lookup"><span data-stu-id="085ec-148">The app syncs your local changes with the Azure Mobile App backend using push and pull operations when the `OnRefreshItemsSelected` method executes.</span></span>
3. <span data-ttu-id="085ec-149">(Optional) View the updated data using either SQL Server Object Explorer or a REST tool like Fiddler.</span><span class="sxs-lookup"><span data-stu-id="085ec-149">(Optional) View the updated data using either SQL Server Object Explorer or a REST tool like Fiddler.</span></span> <span data-ttu-id="085ec-150">Notice the data has been synchronized between the Azure Mobile App backend database and the local store.</span><span class="sxs-lookup"><span data-stu-id="085ec-150">Notice the data has been synchronized between the Azure Mobile App backend database and the local store.</span></span>
4. <span data-ttu-id="085ec-151">In the app, click the check box beside a few items to complete them in the local store.</span><span class="sxs-lookup"><span data-stu-id="085ec-151">In the app, click the check box beside a few items to complete them in the local store.</span></span>
   
   <span data-ttu-id="085ec-152">`CheckItem` calls `SyncAsync` to sync each completed item with the Mobile App backend.</span><span class="sxs-lookup"><span data-stu-id="085ec-152">`CheckItem` calls `SyncAsync` to sync each completed item with the Mobile App backend.</span></span> <span data-ttu-id="085ec-153">`SyncAsync` calls both push and pull.</span><span class="sxs-lookup"><span data-stu-id="085ec-153">`SyncAsync` calls both push and pull.</span></span> <span data-ttu-id="085ec-154">**Whenever you execute a pull against a table that the client has made changes to, a push is always executed automatically**.</span><span class="sxs-lookup"><span data-stu-id="085ec-154">**Whenever you execute a pull against a table that the client has made changes to, a push is always executed automatically**.</span></span> <span data-ttu-id="085ec-155">This ensures all tables in the local store along with relationships remain consistent.</span><span class="sxs-lookup"><span data-stu-id="085ec-155">This ensures all tables in the local store along with relationships remain consistent.</span></span> <span data-ttu-id="085ec-156">This behavior may result in an unexpected push.</span><span class="sxs-lookup"><span data-stu-id="085ec-156">This behavior may result in an unexpected push.</span></span> <span data-ttu-id="085ec-157">For more information on this behavior, see [Offline Data Sync in Azure Mobile Apps].</span><span class="sxs-lookup"><span data-stu-id="085ec-157">For more information on this behavior, see [Offline Data Sync in Azure Mobile Apps].</span></span>

## <a name="review-the-client-sync-code"></a><span data-ttu-id="085ec-158">Review the client sync code</span><span class="sxs-lookup"><span data-stu-id="085ec-158">Review the client sync code</span></span>
<span data-ttu-id="085ec-159">The Xamarin client project that you downloaded when you completed the tutorial [Create a Xamarin Android app] already contains code supporting offline synchronization using a local SQLite database.</span><span class="sxs-lookup"><span data-stu-id="085ec-159">The Xamarin client project that you downloaded when you completed the tutorial [Create a Xamarin Android app] already contains code supporting offline synchronization using a local SQLite database.</span></span> <span data-ttu-id="085ec-160">Here is a brief overview of what is already included in the tutorial code.</span><span class="sxs-lookup"><span data-stu-id="085ec-160">Here is a brief overview of what is already included in the tutorial code.</span></span> <span data-ttu-id="085ec-161">For a conceptual overview of the feature, see [Offline Data Sync in Azure Mobile Apps].</span><span class="sxs-lookup"><span data-stu-id="085ec-161">For a conceptual overview of the feature, see [Offline Data Sync in Azure Mobile Apps].</span></span>

* <span data-ttu-id="085ec-162">Before any table operations can be performed, the local store must be initialized.</span><span class="sxs-lookup"><span data-stu-id="085ec-162">Before any table operations can be performed, the local store must be initialized.</span></span> <span data-ttu-id="085ec-163">The local store database is initialized when `ToDoActivity.OnCreate()` executes `ToDoActivity.InitLocalStoreAsync()`.</span><span class="sxs-lookup"><span data-stu-id="085ec-163">The local store database is initialized when `ToDoActivity.OnCreate()` executes `ToDoActivity.InitLocalStoreAsync()`.</span></span> <span data-ttu-id="085ec-164">This method creates a local SQLite database using the `MobileServiceSQLiteStore` class provided by the Azure Mobile Apps client SDK.</span><span class="sxs-lookup"><span data-stu-id="085ec-164">This method creates a local SQLite database using the `MobileServiceSQLiteStore` class provided by the Azure Mobile Apps client SDK.</span></span>
  
    <span data-ttu-id="085ec-165">The `DefineTable` method creates a table in the local store that matches the fields in the provided type, `ToDoItem` in this case.</span><span class="sxs-lookup"><span data-stu-id="085ec-165">The `DefineTable` method creates a table in the local store that matches the fields in the provided type, `ToDoItem` in this case.</span></span> <span data-ttu-id="085ec-166">The type doesn't have to include all the columns that are in the remote database.</span><span class="sxs-lookup"><span data-stu-id="085ec-166">The type doesn't have to include all the columns that are in the remote database.</span></span> <span data-ttu-id="085ec-167">It is possible to store just a subset of columns.</span><span class="sxs-lookup"><span data-stu-id="085ec-167">It is possible to store just a subset of columns.</span></span>
  
        // ToDoActivity.cs
        private async Task InitLocalStoreAsync()
        {
            // new code to initialize the SQLite store
            string path = Path.Combine(System.Environment
                .GetFolderPath(System.Environment.SpecialFolder.Personal), localDbFilename);
  
            if (!File.Exists(path))
            {
                File.Create(path).Dispose();
            }
  
            var store = new MobileServiceSQLiteStore(path);
            store.DefineTable<ToDoItem>();
  
            // Uses the default conflict handler, which fails on conflict
            // To use a different conflict handler, pass a parameter to InitializeAsync.
            // For more details, see http://go.microsoft.com/fwlink/?LinkId=521416.
            await client.SyncContext.InitializeAsync(store);
        }
* <span data-ttu-id="085ec-168">The `toDoTable` member of `ToDoActivity` is of the `IMobileServiceSyncTable` type instead of `IMobileServiceTable`.</span><span class="sxs-lookup"><span data-stu-id="085ec-168">The `toDoTable` member of `ToDoActivity` is of the `IMobileServiceSyncTable` type instead of `IMobileServiceTable`.</span></span> <span data-ttu-id="085ec-169">The IMobileServiceSyncTable directs all create, read, update, and delete (CRUD) table operations to the local store database.</span><span class="sxs-lookup"><span data-stu-id="085ec-169">The IMobileServiceSyncTable directs all create, read, update, and delete (CRUD) table operations to the local store database.</span></span>
  
    <span data-ttu-id="085ec-170">You decide when changes are pushed to the Azure Mobile App backend by calling `IMobileServiceSyncContext.PushAsync()`.</span><span class="sxs-lookup"><span data-stu-id="085ec-170">You decide when changes are pushed to the Azure Mobile App backend by calling `IMobileServiceSyncContext.PushAsync()`.</span></span> <span data-ttu-id="085ec-171">The sync context helps preserve table relationships by tracking and pushing changes in all tables a client app has modified when `PushAsync` is called.</span><span class="sxs-lookup"><span data-stu-id="085ec-171">The sync context helps preserve table relationships by tracking and pushing changes in all tables a client app has modified when `PushAsync` is called.</span></span>
  
    <span data-ttu-id="085ec-172">The provided code calls `ToDoActivity.SyncAsync()` to sync whenever the todoitem list is refreshed or a todoitem is added or completed.</span><span class="sxs-lookup"><span data-stu-id="085ec-172">The provided code calls `ToDoActivity.SyncAsync()` to sync whenever the todoitem list is refreshed or a todoitem is added or completed.</span></span> <span data-ttu-id="085ec-173">The code syncs after every local change.</span><span class="sxs-lookup"><span data-stu-id="085ec-173">The code syncs after every local change.</span></span>
  
    <span data-ttu-id="085ec-174">In the provided code, all records in the remote `TodoItem` table are queried, but it is also possible to filter records by passing a query id and query to `PushAsync`.</span><span class="sxs-lookup"><span data-stu-id="085ec-174">In the provided code, all records in the remote `TodoItem` table are queried, but it is also possible to filter records by passing a query id and query to `PushAsync`.</span></span> <span data-ttu-id="085ec-175">For more information, see the section *Incremental Sync* in [Offline Data Sync in Azure Mobile Apps].</span><span class="sxs-lookup"><span data-stu-id="085ec-175">For more information, see the section *Incremental Sync* in [Offline Data Sync in Azure Mobile Apps].</span></span>
  
        // ToDoActivity.cs
        private async Task SyncAsync()
        {
            try {
                await client.SyncContext.PushAsync();
                await toDoTable.PullAsync("allTodoItems", toDoTable.CreateQuery()); // query ID is used for incremental sync
            } catch (Java.Net.MalformedURLException) {
                CreateAndShowDialog (new Exception ("There was an error creating the Mobile Service. Verify the URL"), "Error");
            } catch (Exception e) {
                CreateAndShowDialog (e, "Error");
            }
        }

## <a name="additional-resources"></a><span data-ttu-id="085ec-176">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="085ec-176">Additional Resources</span></span>
* <span data-ttu-id="085ec-177">[Offline Data Sync in Azure Mobile Apps]</span><span class="sxs-lookup"><span data-stu-id="085ec-177">[Offline Data Sync in Azure Mobile Apps]</span></span>
* <span data-ttu-id="085ec-178">[Azure Mobile Apps .NET SDK HOWTO][8]</span><span class="sxs-lookup"><span data-stu-id="085ec-178">[Azure Mobile Apps .NET SDK HOWTO][8]</span></span>

<!-- URLs. -->
[Create a Xamarin Android app]: ../app-service-mobile-xamarin-android-get-started.md
[Offline Data Sync in Azure Mobile Apps]: ../app-service-mobile-offline-data-sync.md

<!-- Images -->

<!-- URLs. -->
[Create a Xamarin Android app]: app-service-mobile-xamarin-android-get-started.md
[Offline Data Sync in Azure Mobile Apps]: app-service-mobile-offline-data-sync.md
[Xamarin Studio]: http://xamarin.com/download
[Xamarin extension]: http://xamarin.com/visual-studio
[SyncContext]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.mobileserviceclient.synccontext(v=azure.10).aspx
[8]: app-service-mobile-dotnet-how-to-use-client-library.md
