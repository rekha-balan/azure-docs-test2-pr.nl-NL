---
title: Enable offline sync for your Azure Mobile App (Xamarin.Forms) | Microsoft Docs
description: Learn how to use App Service Mobile App to cache and sync offline data in your Xamarin.Forms application
documentationcenter: xamarin
author: adrianhall
manager: yochayk
editor: ''
services: app-service\mobile
ms.assetid: acf0f874-3ea5-4410-bd22-b0e72140f3b5
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 10/04/2016
ms.author: adrianha
ms.openlocfilehash: 62610da9598077ffd17b97e9427149310c639a1a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551773"
---
# <a name="enable-offline-sync-for-your-xamarinforms-mobile-app"></a><span data-ttu-id="20471-103">Enable offline sync for your Xamarin.Forms mobile app</span><span class="sxs-lookup"><span data-stu-id="20471-103">Enable offline sync for your Xamarin.Forms mobile app</span></span>
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a><span data-ttu-id="20471-104">Overview</span><span class="sxs-lookup"><span data-stu-id="20471-104">Overview</span></span>
<span data-ttu-id="20471-105">This tutorial introduces the offline sync feature of Azure Mobile Apps for Xamarin.Forms.</span><span class="sxs-lookup"><span data-stu-id="20471-105">This tutorial introduces the offline sync feature of Azure Mobile Apps for Xamarin.Forms.</span></span> <span data-ttu-id="20471-106">Offline sync allows end users to interact with a mobile app--viewing, adding, or modifying data--even when there is no network connection.</span><span class="sxs-lookup"><span data-stu-id="20471-106">Offline sync allows end users to interact with a mobile app--viewing, adding, or modifying data--even when there is no network connection.</span></span> <span data-ttu-id="20471-107">Changes are stored in a local database.</span><span class="sxs-lookup"><span data-stu-id="20471-107">Changes are stored in a local database.</span></span> <span data-ttu-id="20471-108">Once the device is back online, these changes are synced with the remote service.</span><span class="sxs-lookup"><span data-stu-id="20471-108">Once the device is back online, these changes are synced with the remote service.</span></span>

<span data-ttu-id="20471-109">This tutorial is based on the Xamarin.Forms quickstart solution for Mobile Apps that you create when you complete the tutorial [Create a Xamarin iOS app].</span><span class="sxs-lookup"><span data-stu-id="20471-109">This tutorial is based on the Xamarin.Forms quickstart solution for Mobile Apps that you create when you complete the tutorial [Create a Xamarin iOS app].</span></span> <span data-ttu-id="20471-110">The quickstart solution for Xamarin.Forms contains the code to support offline sync, which just needs to be enabled.</span><span class="sxs-lookup"><span data-stu-id="20471-110">The quickstart solution for Xamarin.Forms contains the code to support offline sync, which just needs to be enabled.</span></span> <span data-ttu-id="20471-111">In this tutorial, you update the quickstart solution to turn on the offline features of Azure Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="20471-111">In this tutorial, you update the quickstart solution to turn on the offline features of Azure Mobile Apps.</span></span> <span data-ttu-id="20471-112">We also highlight the offline-specific code in the app.</span><span class="sxs-lookup"><span data-stu-id="20471-112">We also highlight the offline-specific code in the app.</span></span> <span data-ttu-id="20471-113">If you do not use the downloaded quickstart solution, you must add the data access extension packages to your project.</span><span class="sxs-lookup"><span data-stu-id="20471-113">If you do not use the downloaded quickstart solution, you must add the data access extension packages to your project.</span></span> <span data-ttu-id="20471-114">For more information about server extension packages, see [Work with the .NET backend server SDK for Azure Mobile Apps][1].</span><span class="sxs-lookup"><span data-stu-id="20471-114">For more information about server extension packages, see [Work with the .NET backend server SDK for Azure Mobile Apps][1].</span></span>

<span data-ttu-id="20471-115">To learn more about the offline sync feature, see the topic [Offline Data Sync in Azure Mobile Apps][2].</span><span class="sxs-lookup"><span data-stu-id="20471-115">To learn more about the offline sync feature, see the topic [Offline Data Sync in Azure Mobile Apps][2].</span></span>

## <a name="enable-offline-sync-functionality-in-the-quickstart-solution"></a><span data-ttu-id="20471-116">Enable offline sync functionality in the quickstart solution</span><span class="sxs-lookup"><span data-stu-id="20471-116">Enable offline sync functionality in the quickstart solution</span></span>
<span data-ttu-id="20471-117">The offline sync code is included in the project by using C# preprocessor directives.</span><span class="sxs-lookup"><span data-stu-id="20471-117">The offline sync code is included in the project by using C# preprocessor directives.</span></span> <span data-ttu-id="20471-118">When the **OFFLINE\_SYNC\_ENABLED** symbol is defined, these code paths are included in the build.</span><span class="sxs-lookup"><span data-stu-id="20471-118">When the **OFFLINE\_SYNC\_ENABLED** symbol is defined, these code paths are included in the build.</span></span> <span data-ttu-id="20471-119">For Windows apps, you must also install the SQLite platform.</span><span class="sxs-lookup"><span data-stu-id="20471-119">For Windows apps, you must also install the SQLite platform.</span></span>

1. <span data-ttu-id="20471-120">In Visual Studio, right-click the solution > **Manage NuGet Packages for Solution...**, then search for and install the **Microsoft.Azure.Mobile.Client.SQLiteStore** NuGet package for all projects in the solution.</span><span class="sxs-lookup"><span data-stu-id="20471-120">In Visual Studio, right-click the solution > **Manage NuGet Packages for Solution...**, then search for and install the **Microsoft.Azure.Mobile.Client.SQLiteStore** NuGet package for all projects in the solution.</span></span>
2. <span data-ttu-id="20471-121">In the Solution Explorer, open the TodoItemManager.cs file from the project with **Portable** in the name, which is Portable Class Library project, then uncomment the following preprocessor directive:</span><span class="sxs-lookup"><span data-stu-id="20471-121">In the Solution Explorer, open the TodoItemManager.cs file from the project with **Portable** in the name, which is Portable Class Library project, then uncomment the following preprocessor directive:</span></span>
   
        #define OFFLINE_SYNC_ENABLED
3. <span data-ttu-id="20471-122">(Optional) To support Windows devices, install one of the following SQLite runtime packages:</span><span class="sxs-lookup"><span data-stu-id="20471-122">(Optional) To support Windows devices, install one of the following SQLite runtime packages:</span></span>
   
   * <span data-ttu-id="20471-123">**Windows 8.1 Runtime:** Install [SQLite for Windows 8.1][3].</span><span class="sxs-lookup"><span data-stu-id="20471-123">**Windows 8.1 Runtime:** Install [SQLite for Windows 8.1][3].</span></span>
   * <span data-ttu-id="20471-124">**Windows Phone 8.1:** Install [SQLite for Windows Phone 8.1][4].</span><span class="sxs-lookup"><span data-stu-id="20471-124">**Windows Phone 8.1:** Install [SQLite for Windows Phone 8.1][4].</span></span>
   * <span data-ttu-id="20471-125">**Universal Windows Platform** Install [SQLite for the Universal Windows Universal][5].</span><span class="sxs-lookup"><span data-stu-id="20471-125">**Universal Windows Platform** Install [SQLite for the Universal Windows Universal][5].</span></span>
     
     <span data-ttu-id="20471-126">Although the quickstart does not contain a Universal Windows project, the Universal Windows platform is supported with Xamarin Forms.</span><span class="sxs-lookup"><span data-stu-id="20471-126">Although the quickstart does not contain a Universal Windows project, the Universal Windows platform is supported with Xamarin Forms.</span></span>
4. <span data-ttu-id="20471-127">(Optional) In each Windows app project, right-click **References** > **Add Reference...**, expand the **Windows** folder > **Extensions**.</span><span class="sxs-lookup"><span data-stu-id="20471-127">(Optional) In each Windows app project, right-click **References** > **Add Reference...**, expand the **Windows** folder > **Extensions**.</span></span>
    <span data-ttu-id="20471-128">Enable the appropriate **SQLite for Windows** SDK along with the **Visual C++ 2013 Runtime for Windows** SDK.</span><span class="sxs-lookup"><span data-stu-id="20471-128">Enable the appropriate **SQLite for Windows** SDK along with the **Visual C++ 2013 Runtime for Windows** SDK.</span></span>
    <span data-ttu-id="20471-129">The SQLite SDK names vary slightly with each Windows platform.</span><span class="sxs-lookup"><span data-stu-id="20471-129">The SQLite SDK names vary slightly with each Windows platform.</span></span>

## <a name="review-the-client-sync-code"></a><span data-ttu-id="20471-130">Review the client sync code</span><span class="sxs-lookup"><span data-stu-id="20471-130">Review the client sync code</span></span>
<span data-ttu-id="20471-131">Here is a brief overview of what is already included in the tutorial code inside the `#if OFFLINE_SYNC_ENABLED` directives.</span><span class="sxs-lookup"><span data-stu-id="20471-131">Here is a brief overview of what is already included in the tutorial code inside the `#if OFFLINE_SYNC_ENABLED` directives.</span></span> <span data-ttu-id="20471-132">The offline sync functionality is in the TodoItemManager.cs project file in the Portable Class Library project.</span><span class="sxs-lookup"><span data-stu-id="20471-132">The offline sync functionality is in the TodoItemManager.cs project file in the Portable Class Library project.</span></span> <span data-ttu-id="20471-133">For a conceptual overview of the feature, see [Offline Data Sync in Azure Mobile Apps][2].</span><span class="sxs-lookup"><span data-stu-id="20471-133">For a conceptual overview of the feature, see [Offline Data Sync in Azure Mobile Apps][2].</span></span>

* <span data-ttu-id="20471-134">Before any table operations can be performed, the local store must be initialized.</span><span class="sxs-lookup"><span data-stu-id="20471-134">Before any table operations can be performed, the local store must be initialized.</span></span> <span data-ttu-id="20471-135">The local store database is initialized in the **TodoItemManager** class constructor by using the following code:</span><span class="sxs-lookup"><span data-stu-id="20471-135">The local store database is initialized in the **TodoItemManager** class constructor by using the following code:</span></span>
  
        var store = new MobileServiceSQLiteStore(OfflineDbPath);
        store.DefineTable<TodoItem>();
  
        //Initializes the SyncContext using the default IMobileServiceSyncHandler.
        this.client.SyncContext.InitializeAsync(store);
  
        this.todoTable = client.GetSyncTable<TodoItem>();
  
    <span data-ttu-id="20471-136">This code creates a new local SQLite database using the **MobileServiceSQLiteStore** class.</span><span class="sxs-lookup"><span data-stu-id="20471-136">This code creates a new local SQLite database using the **MobileServiceSQLiteStore** class.</span></span>
  
    <span data-ttu-id="20471-137">The **DefineTable** method creates a table in the local store that matches the fields in the provided type.</span><span class="sxs-lookup"><span data-stu-id="20471-137">The **DefineTable** method creates a table in the local store that matches the fields in the provided type.</span></span>  <span data-ttu-id="20471-138">The type doesn't have to include all the columns that are in the remote database.</span><span class="sxs-lookup"><span data-stu-id="20471-138">The type doesn't have to include all the columns that are in the remote database.</span></span> <span data-ttu-id="20471-139">It is possible to store a subset of columns.</span><span class="sxs-lookup"><span data-stu-id="20471-139">It is possible to store a subset of columns.</span></span>
* <span data-ttu-id="20471-140">The **todoTable** field in **TodoItemManager** is an **IMobileServiceSyncTable** type instead of **IMobileServiceTable**.</span><span class="sxs-lookup"><span data-stu-id="20471-140">The **todoTable** field in **TodoItemManager** is an **IMobileServiceSyncTable** type instead of **IMobileServiceTable**.</span></span> <span data-ttu-id="20471-141">This class uses the local database for all create, read, update, and delete (CRUD) table operations.</span><span class="sxs-lookup"><span data-stu-id="20471-141">This class uses the local database for all create, read, update, and delete (CRUD) table operations.</span></span> <span data-ttu-id="20471-142">You decide when those changes are pushed to the Mobile App backend by calling **PushAsync** on the **IMobileServiceSyncContext**.</span><span class="sxs-lookup"><span data-stu-id="20471-142">You decide when those changes are pushed to the Mobile App backend by calling **PushAsync** on the **IMobileServiceSyncContext**.</span></span> <span data-ttu-id="20471-143">The sync context helps preserve table relationships by tracking and pushing changes in all tables a client app has modified when **PushAsync** is called.</span><span class="sxs-lookup"><span data-stu-id="20471-143">The sync context helps preserve table relationships by tracking and pushing changes in all tables a client app has modified when **PushAsync** is called.</span></span>
  
    <span data-ttu-id="20471-144">The following **SyncAsync** method is called to sync with the Mobile App backend:</span><span class="sxs-lookup"><span data-stu-id="20471-144">The following **SyncAsync** method is called to sync with the Mobile App backend:</span></span>
  
        public async Task SyncAsync()
        {
            ReadOnlyCollection<MobileServiceTableOperationError> syncErrors = null;
  
            try
            {
                await this.client.SyncContext.PushAsync();
  
                await this.todoTable.PullAsync(
                    "allTodoItems",
                    this.todoTable.CreateQuery());
            }
            catch (MobileServicePushFailedException exc)
            {
                if (exc.PushResult != null)
                {
                    syncErrors = exc.PushResult.Errors;
                }
            }
  
            // Simple error/conflict handling.
            if (syncErrors != null)
            {
                foreach (var error in syncErrors)
                {
                    if (error.OperationKind == MobileServiceTableOperationKind.Update && error.Result != null)
                    {
                        //Update failed, reverting to server's copy.
                        await error.CancelAndUpdateItemAsync(error.Result);
                    }
                    else
                    {
                        // Discard local change.
                        await error.CancelAndDiscardItemAsync();
                    }
  
                    Debug.WriteLine(@"Error executing sync operation. Item: {0} ({1}). Operation discarded.",
                        error.TableName, error.Item["id"]);
                }
            }
        }
  
    <span data-ttu-id="20471-145">This sample uses simple error handling with the default sync handler.</span><span class="sxs-lookup"><span data-stu-id="20471-145">This sample uses simple error handling with the default sync handler.</span></span> <span data-ttu-id="20471-146">A real application would handle the various errors like network conditions and server conflicts by using a custom **IMobileServiceSyncHandler** implementation.</span><span class="sxs-lookup"><span data-stu-id="20471-146">A real application would handle the various errors like network conditions and server conflicts by using a custom **IMobileServiceSyncHandler** implementation.</span></span>

## <a name="offline-sync-considerations"></a><span data-ttu-id="20471-147">Offline sync considerations</span><span class="sxs-lookup"><span data-stu-id="20471-147">Offline sync considerations</span></span>
<span data-ttu-id="20471-148">In the sample, the **SyncAsync** method is only called on start-up and when a sync is requested.</span><span class="sxs-lookup"><span data-stu-id="20471-148">In the sample, the **SyncAsync** method is only called on start-up and when a sync is requested.</span></span>  <span data-ttu-id="20471-149">To initiate a sync in an Android or iOS app, pull down on the items list; for Windows, use the **Sync** button.</span><span class="sxs-lookup"><span data-stu-id="20471-149">To initiate a sync in an Android or iOS app, pull down on the items list; for Windows, use the **Sync** button.</span></span> <span data-ttu-id="20471-150">In a real-world application, you could also make the sync trigger when the network state changes.</span><span class="sxs-lookup"><span data-stu-id="20471-150">In a real-world application, you could also make the sync trigger when the network state changes.</span></span>

<span data-ttu-id="20471-151">When a pull is executed against a table that has pending local updates tracked by the context, that pull operation automatically triggers a preceding context push.</span><span class="sxs-lookup"><span data-stu-id="20471-151">When a pull is executed against a table that has pending local updates tracked by the context, that pull operation automatically triggers a preceding context push.</span></span> <span data-ttu-id="20471-152">When refreshing, adding, and completing items in this sample, you can omit the explicit **PushAsync** call.</span><span class="sxs-lookup"><span data-stu-id="20471-152">When refreshing, adding, and completing items in this sample, you can omit the explicit **PushAsync** call.</span></span>

<span data-ttu-id="20471-153">In the provided code, all records in the remote TodoItem table are queried, but it is also possible to filter records by passing a query id and query to **PushAsync**.</span><span class="sxs-lookup"><span data-stu-id="20471-153">In the provided code, all records in the remote TodoItem table are queried, but it is also possible to filter records by passing a query id and query to **PushAsync**.</span></span> <span data-ttu-id="20471-154">For more information, see the section *Incremental Sync* in [Offline Data Sync in Azure Mobile Apps][2].</span><span class="sxs-lookup"><span data-stu-id="20471-154">For more information, see the section *Incremental Sync* in [Offline Data Sync in Azure Mobile Apps][2].</span></span>

## <a name="run-the-client-app"></a><span data-ttu-id="20471-155">Run the client app</span><span class="sxs-lookup"><span data-stu-id="20471-155">Run the client app</span></span>
<span data-ttu-id="20471-156">With offline sync now enabled, run the client application at least once on each platform to populate the local store database.</span><span class="sxs-lookup"><span data-stu-id="20471-156">With offline sync now enabled, run the client application at least once on each platform to populate the local store database.</span></span> <span data-ttu-id="20471-157">Later, simulate an offline scenario and modify the data in the local store while the app is offline.</span><span class="sxs-lookup"><span data-stu-id="20471-157">Later, simulate an offline scenario and modify the data in the local store while the app is offline.</span></span>

## <a name="update-the-sync-behavior-of-the-client-app"></a><span data-ttu-id="20471-158">Update the sync behavior of the client app</span><span class="sxs-lookup"><span data-stu-id="20471-158">Update the sync behavior of the client app</span></span>
<span data-ttu-id="20471-159">In this section, modify the client project to simulate an offline scenario by using an invalid application URL for your backend.</span><span class="sxs-lookup"><span data-stu-id="20471-159">In this section, modify the client project to simulate an offline scenario by using an invalid application URL for your backend.</span></span> <span data-ttu-id="20471-160">Alternatively, you can turn off network connections by moving your device to "Airplane mode."</span><span class="sxs-lookup"><span data-stu-id="20471-160">Alternatively, you can turn off network connections by moving your device to "Airplane mode."</span></span>  <span data-ttu-id="20471-161">When you add or change data items, these changes are held in the local store, but not synced to the backend data store until the connection is re-established.</span><span class="sxs-lookup"><span data-stu-id="20471-161">When you add or change data items, these changes are held in the local store, but not synced to the backend data store until the connection is re-established.</span></span>

1. <span data-ttu-id="20471-162">In the Solution Explorer, open the Constants.cs project file from the **Portable** project and change the value of `ApplicationURL` to point to an invalid URL:</span><span class="sxs-lookup"><span data-stu-id="20471-162">In the Solution Explorer, open the Constants.cs project file from the **Portable** project and change the value of `ApplicationURL` to point to an invalid URL:</span></span>
   
        public static string ApplicationURL = @"https://your-service.azurewebsites.net/";
2. <span data-ttu-id="20471-163">Open the TodoItemManager.cs file from the **Portable** project, then add a **catch** for the base **Exception** class to the **try...catch** block in **SyncAsync**.</span><span class="sxs-lookup"><span data-stu-id="20471-163">Open the TodoItemManager.cs file from the **Portable** project, then add a **catch** for the base **Exception** class to the **try...catch** block in **SyncAsync**.</span></span> <span data-ttu-id="20471-164">This **catch** block writes the exception message to the console, as follows:</span><span class="sxs-lookup"><span data-stu-id="20471-164">This **catch** block writes the exception message to the console, as follows:</span></span>
   
            catch (Exception ex)
            {
                Console.Error.WriteLine(@"Exception: {0}", ex.Message);
            }
3. <span data-ttu-id="20471-165">Build and run the client app.</span><span class="sxs-lookup"><span data-stu-id="20471-165">Build and run the client app.</span></span>  <span data-ttu-id="20471-166">Add some new items.</span><span class="sxs-lookup"><span data-stu-id="20471-166">Add some new items.</span></span> <span data-ttu-id="20471-167">Notice that an exception is logged in the console for each attempt to sync with the backend.</span><span class="sxs-lookup"><span data-stu-id="20471-167">Notice that an exception is logged in the console for each attempt to sync with the backend.</span></span> <span data-ttu-id="20471-168">These new items exist only in the local store until they can be pushed to the mobile backend.</span><span class="sxs-lookup"><span data-stu-id="20471-168">These new items exist only in the local store until they can be pushed to the mobile backend.</span></span> <span data-ttu-id="20471-169">The client app behaves as if it is connected to the backend, supporting all create, read, update, delete (CRUD) operations.</span><span class="sxs-lookup"><span data-stu-id="20471-169">The client app behaves as if it is connected to the backend, supporting all create, read, update, delete (CRUD) operations.</span></span>
4. <span data-ttu-id="20471-170">Close the app and restart it to verify that the new items you created are persisted to the local store.</span><span class="sxs-lookup"><span data-stu-id="20471-170">Close the app and restart it to verify that the new items you created are persisted to the local store.</span></span>
5. <span data-ttu-id="20471-171">(Optional) Use Visual Studio to view your Azure SQL Database table to see that the data in the backend database has not changed.</span><span class="sxs-lookup"><span data-stu-id="20471-171">(Optional) Use Visual Studio to view your Azure SQL Database table to see that the data in the backend database has not changed.</span></span>
   
    <span data-ttu-id="20471-172">In Visual Studio, open **Server Explorer**.</span><span class="sxs-lookup"><span data-stu-id="20471-172">In Visual Studio, open **Server Explorer**.</span></span> <span data-ttu-id="20471-173">Navigate to your database in **Azure**->**SQL Databases**.</span><span class="sxs-lookup"><span data-stu-id="20471-173">Navigate to your database in **Azure**->**SQL Databases**.</span></span> <span data-ttu-id="20471-174">Right-click your database and select **Open in SQL Server Object Explorer**.</span><span class="sxs-lookup"><span data-stu-id="20471-174">Right-click your database and select **Open in SQL Server Object Explorer**.</span></span> <span data-ttu-id="20471-175">Now you can browse to your SQL database table and its contents.</span><span class="sxs-lookup"><span data-stu-id="20471-175">Now you can browse to your SQL database table and its contents.</span></span>

## <a name="update-the-client-app-to-reconnect-your-mobile-backend"></a><span data-ttu-id="20471-176">Update the client app to reconnect your mobile backend</span><span class="sxs-lookup"><span data-stu-id="20471-176">Update the client app to reconnect your mobile backend</span></span>
<span data-ttu-id="20471-177">In this section, reconnect the app to the mobile backend, which simulates the app coming back to an online state.</span><span class="sxs-lookup"><span data-stu-id="20471-177">In this section, reconnect the app to the mobile backend, which simulates the app coming back to an online state.</span></span> <span data-ttu-id="20471-178">When you perform the refresh gesture, data is synced to your mobile backend.</span><span class="sxs-lookup"><span data-stu-id="20471-178">When you perform the refresh gesture, data is synced to your mobile backend.</span></span>

1. <span data-ttu-id="20471-179">Reopen Constants.cs.</span><span class="sxs-lookup"><span data-stu-id="20471-179">Reopen Constants.cs.</span></span> <span data-ttu-id="20471-180">Correct the `applicationURL` to point to the correct URL.</span><span class="sxs-lookup"><span data-stu-id="20471-180">Correct the `applicationURL` to point to the correct URL.</span></span>
2. <span data-ttu-id="20471-181">Rebuild and run the client app.</span><span class="sxs-lookup"><span data-stu-id="20471-181">Rebuild and run the client app.</span></span> <span data-ttu-id="20471-182">The app attempts to sync with the mobile app backend after launching.</span><span class="sxs-lookup"><span data-stu-id="20471-182">The app attempts to sync with the mobile app backend after launching.</span></span> <span data-ttu-id="20471-183">Verify that no exceptions are logged in the debug console.</span><span class="sxs-lookup"><span data-stu-id="20471-183">Verify that no exceptions are logged in the debug console.</span></span>
3. <span data-ttu-id="20471-184">(Optional) View the updated data using either SQL Server Object Explorer or a REST tool like Fiddler or [Postman][6].</span><span class="sxs-lookup"><span data-stu-id="20471-184">(Optional) View the updated data using either SQL Server Object Explorer or a REST tool like Fiddler or [Postman][6].</span></span> <span data-ttu-id="20471-185">Notice the data has been synchronized between the backend database and the local store.</span><span class="sxs-lookup"><span data-stu-id="20471-185">Notice the data has been synchronized between the backend database and the local store.</span></span>
   
    <span data-ttu-id="20471-186">Notice the data has been synchronized between the database and the local store and contains the items you added while your app was disconnected.</span><span class="sxs-lookup"><span data-stu-id="20471-186">Notice the data has been synchronized between the database and the local store and contains the items you added while your app was disconnected.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="20471-187">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="20471-187">Additional Resources</span></span>
* <span data-ttu-id="20471-188">[Offline Data Sync in Azure Mobile Apps][2]</span><span class="sxs-lookup"><span data-stu-id="20471-188">[Offline Data Sync in Azure Mobile Apps][2]</span></span>
* <span data-ttu-id="20471-189">[Azure Mobile Apps .NET SDK HOWTO][8]</span><span class="sxs-lookup"><span data-stu-id="20471-189">[Azure Mobile Apps .NET SDK HOWTO][8]</span></span>

<!-- URLs. -->
[1]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[2]: app-service-mobile-offline-data-sync.md
[3]: http://go.microsoft.com/fwlink/p/?LinkID=716919
[4]: http://go.microsoft.com/fwlink/p/?LinkID=716920
[5]: http://sqlite.org/2016/sqlite-uwp-3120200.vsix
[6]: https://www.getpostman.com/
[7]: http://www.telerik.com/fiddler
[8]: app-service-mobile-dotnet-how-to-use-client-library.md
