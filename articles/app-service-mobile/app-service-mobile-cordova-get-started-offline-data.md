---
title: Enable offline sync for your Azure Mobile App (Cordova) | Microsoft Docs
description: Learn how to use App Service Mobile App to cache and sync offline data in your Cordova application
documentationcenter: cordova
author: adrianhall
manager: adrianha
editor: ''
services: app-service\mobile
ms.assetid: 1a3f685d-f79d-4f8b-ae11-ff96e79e9de9
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-cordova-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 10/30/2016
ms.author: adrianha
ms.openlocfilehash: 15ef3d9d105798ad4839c759c878bf017d4bac01
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553691"
---
# <a name="enable-offline-sync-for-your-cordova-mobile-app"></a><span data-ttu-id="465b7-103">Enable offline sync for your Cordova mobile app</span><span class="sxs-lookup"><span data-stu-id="465b7-103">Enable offline sync for your Cordova mobile app</span></span>
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

<span data-ttu-id="465b7-104">This tutorial introduces the offline sync feature of Azure Mobile Apps for Cordova.</span><span class="sxs-lookup"><span data-stu-id="465b7-104">This tutorial introduces the offline sync feature of Azure Mobile Apps for Cordova.</span></span> <span data-ttu-id="465b7-105">Offline sync allows end users to interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span><span class="sxs-lookup"><span data-stu-id="465b7-105">Offline sync allows end users to interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span> <span data-ttu-id="465b7-106">Changes are stored in a local database.</span><span class="sxs-lookup"><span data-stu-id="465b7-106">Changes are stored in a local database.</span></span>  <span data-ttu-id="465b7-107">Once the device is back online, these changes are synced with the remote service.</span><span class="sxs-lookup"><span data-stu-id="465b7-107">Once the device is back online, these changes are synced with the remote service.</span></span>

<span data-ttu-id="465b7-108">This tutorial is based on the Cordova quickstart solution for Mobile Apps that you create when you complete the tutorial [Apache Cordova quick start].</span><span class="sxs-lookup"><span data-stu-id="465b7-108">This tutorial is based on the Cordova quickstart solution for Mobile Apps that you create when you complete the tutorial [Apache Cordova quick start].</span></span> <span data-ttu-id="465b7-109">In this tutorial, you update the quickstart solution to add offline features of Azure Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="465b7-109">In this tutorial, you update the quickstart solution to add offline features of Azure Mobile Apps.</span></span>  <span data-ttu-id="465b7-110">We also highlight the offline-specific code in the app.</span><span class="sxs-lookup"><span data-stu-id="465b7-110">We also highlight the offline-specific code in the app.</span></span>

<span data-ttu-id="465b7-111">To learn more about the offline sync feature, see the topic [Offline Data Sync in Azure Mobile Apps].</span><span class="sxs-lookup"><span data-stu-id="465b7-111">To learn more about the offline sync feature, see the topic [Offline Data Sync in Azure Mobile Apps].</span></span> <span data-ttu-id="465b7-112">For details of API usage, see the [API documentation](https://azure.github.io/azure-mobile-apps-js-client).</span><span class="sxs-lookup"><span data-stu-id="465b7-112">For details of API usage, see the [API documentation](https://azure.github.io/azure-mobile-apps-js-client).</span></span>

## <a name="add-offline-sync-to-the-quickstart-solution"></a><span data-ttu-id="465b7-113">Add offline sync to the quickstart solution</span><span class="sxs-lookup"><span data-stu-id="465b7-113">Add offline sync to the quickstart solution</span></span>
<span data-ttu-id="465b7-114">The offline sync code must be added to the app.</span><span class="sxs-lookup"><span data-stu-id="465b7-114">The offline sync code must be added to the app.</span></span> <span data-ttu-id="465b7-115">Offline sync requires the cordova-sqlite-storage plugin, which automatically gets added to your app when the Azure Mobile Apps plugin is included in the project.</span><span class="sxs-lookup"><span data-stu-id="465b7-115">Offline sync requires the cordova-sqlite-storage plugin, which automatically gets added to your app when the Azure Mobile Apps plugin is included in the project.</span></span> <span data-ttu-id="465b7-116">The Quickstart project includes both of these plugins.</span><span class="sxs-lookup"><span data-stu-id="465b7-116">The Quickstart project includes both of these plugins.</span></span>

1. <span data-ttu-id="465b7-117">In Visual Studio's Solution Explorer, open index.js and replace the following code</span><span class="sxs-lookup"><span data-stu-id="465b7-117">In Visual Studio's Solution Explorer, open index.js and replace the following code</span></span>

        var client,            // Connection to the Azure Mobile App backend
           todoItemTable;      // Reference to a table endpoint on backend

    <span data-ttu-id="465b7-118">with this code:</span><span class="sxs-lookup"><span data-stu-id="465b7-118">with this code:</span></span>

        var client,            // Connection to the Azure Mobile App backend
           todoItemTable,      // Reference to a table endpoint on backend
           syncContext;        // Reference to offline data sync context

2. <span data-ttu-id="465b7-119">Next, replace the following code:</span><span class="sxs-lookup"><span data-stu-id="465b7-119">Next, replace the following code:</span></span>

        client = new WindowsAzure.MobileServiceClient('http://yourmobileapp.azurewebsites.net');

    <span data-ttu-id="465b7-120">with this code:</span><span class="sxs-lookup"><span data-stu-id="465b7-120">with this code:</span></span>

        client = new WindowsAzure.MobileServiceClient('http://yourmobileapp.azurewebsites.net');
        var store = new WindowsAzure.MobileServiceSqliteStore('store.db');

        store.defineTable({
          name: 'todoitem',
          columnDefinitions: {
              id: 'string',
              text: 'string',
              complete: 'boolean',
              version: 'string'
          }
        });

        // Get the sync context from the client
        syncContext = client.getSyncContext();

    <span data-ttu-id="465b7-121">The preceding code additions initialize the local store and define a local table that matches the column values used in your Azure back end.</span><span class="sxs-lookup"><span data-stu-id="465b7-121">The preceding code additions initialize the local store and define a local table that matches the column values used in your Azure back end.</span></span> <span data-ttu-id="465b7-122">(You don't need to include all column values in this code.)  The `version` field is maintained by the mobile backend and is used for conflict resolution.</span><span class="sxs-lookup"><span data-stu-id="465b7-122">(You don't need to include all column values in this code.)  The `version` field is maintained by the mobile backend and is used for conflict resolution.</span></span>

    <span data-ttu-id="465b7-123">You get a reference to the sync context by calling **getSyncContext**.</span><span class="sxs-lookup"><span data-stu-id="465b7-123">You get a reference to the sync context by calling **getSyncContext**.</span></span> <span data-ttu-id="465b7-124">The sync context helps preserve table relationships by tracking and pushing changes in all tables a client app has modified when `.push()` is called.</span><span class="sxs-lookup"><span data-stu-id="465b7-124">The sync context helps preserve table relationships by tracking and pushing changes in all tables a client app has modified when `.push()` is called.</span></span>

3. <span data-ttu-id="465b7-125">Update the application URL to your Mobile App application URL.</span><span class="sxs-lookup"><span data-stu-id="465b7-125">Update the application URL to your Mobile App application URL.</span></span>

4. <span data-ttu-id="465b7-126">Next, replace this code:</span><span class="sxs-lookup"><span data-stu-id="465b7-126">Next, replace this code:</span></span>

        todoItemTable = client.getTable('todoitem'); // todoitem is the table name

    <span data-ttu-id="465b7-127">with this code:</span><span class="sxs-lookup"><span data-stu-id="465b7-127">with this code:</span></span>

        // Initialize the sync context with the store
        syncContext.initialize(store).then(function () {

        // Get the local table reference.
        todoItemTable = client.getSyncTable('todoitem');

        syncContext.pushHandler = {
            onConflict: function (pushError) {
                // Handle the conflict.
                console.log("Sync conflict! " + pushError.getError().message);
                // Update failed, revert to server's copy.
                pushError.cancelAndDiscard();
              },
              onError: function (pushError) {
                  // Handle the error
                  // In the simulated offline state, you get "Sync error! Unexpected connection failure."
                  console.log("Sync error! " + pushError.getError().message);
              }
        };

        // Call a function to perform the actual sync
        syncBackend();

        // Refresh the todoItems
        refreshDisplay();

        // Wire up the UI Event Handler for the Add Item
        $('#add-item').submit(addItemHandler);
        $('#refresh').on('click', refreshDisplay);

    <span data-ttu-id="465b7-128">The preceding code initializes the sync context and then calls getSyncTable (instead of getTable) to get a reference to the local table.</span><span class="sxs-lookup"><span data-stu-id="465b7-128">The preceding code initializes the sync context and then calls getSyncTable (instead of getTable) to get a reference to the local table.</span></span>

    <span data-ttu-id="465b7-129">This code uses the local database for all create, read, update, and delete (CRUD) table operations.</span><span class="sxs-lookup"><span data-stu-id="465b7-129">This code uses the local database for all create, read, update, and delete (CRUD) table operations.</span></span>

    <span data-ttu-id="465b7-130">This sample performs simple error handling on sync conflicts.</span><span class="sxs-lookup"><span data-stu-id="465b7-130">This sample performs simple error handling on sync conflicts.</span></span> <span data-ttu-id="465b7-131">A real application would handle the various errors like network conditions, server conflicts, and others.</span><span class="sxs-lookup"><span data-stu-id="465b7-131">A real application would handle the various errors like network conditions, server conflicts, and others.</span></span> <span data-ttu-id="465b7-132">For code examples, see the [offline sync sample].</span><span class="sxs-lookup"><span data-stu-id="465b7-132">For code examples, see the [offline sync sample].</span></span>

5. <span data-ttu-id="465b7-133">Next, add this function to perform the actual sync.</span><span class="sxs-lookup"><span data-stu-id="465b7-133">Next, add this function to perform the actual sync.</span></span>

        function syncBackend() {

          // Sync local store to Azure table when app loads, or when login complete.
          syncContext.push().then(function () {
              // Push completed

          });

          // Pull items from the Azure table after syncing to Azure.
          syncContext.pull(new WindowsAzure.Query('todoitem'));
        }

    <span data-ttu-id="465b7-134">You decide when to push changes to the Mobile App backend by calling **syncContext.push()**.</span><span class="sxs-lookup"><span data-stu-id="465b7-134">You decide when to push changes to the Mobile App backend by calling **syncContext.push()**.</span></span> <span data-ttu-id="465b7-135">For example, you could call **syncBackend** in a button event handler tied to a sync button.</span><span class="sxs-lookup"><span data-stu-id="465b7-135">For example, you could call **syncBackend** in a button event handler tied to a sync button.</span></span>

## <a name="offline-sync-considerations"></a><span data-ttu-id="465b7-136">Offline sync considerations</span><span class="sxs-lookup"><span data-stu-id="465b7-136">Offline sync considerations</span></span>

<span data-ttu-id="465b7-137">In the sample, the **push** method of **syncContext** is only called on app startup in the callback function for login.</span><span class="sxs-lookup"><span data-stu-id="465b7-137">In the sample, the **push** method of **syncContext** is only called on app startup in the callback function for login.</span></span>  <span data-ttu-id="465b7-138">In a real-world application, you could also make this sync functionality triggered manually or when the network state changes.</span><span class="sxs-lookup"><span data-stu-id="465b7-138">In a real-world application, you could also make this sync functionality triggered manually or when the network state changes.</span></span>

<span data-ttu-id="465b7-139">When a pull is executed against a table that has pending local updates tracked by the context, that pull operation automatically triggers a push.</span><span class="sxs-lookup"><span data-stu-id="465b7-139">When a pull is executed against a table that has pending local updates tracked by the context, that pull operation automatically triggers a push.</span></span> <span data-ttu-id="465b7-140">When refreshing, adding, and completing items in this sample, you can omit the explicit **push** call, since it may be redundant.</span><span class="sxs-lookup"><span data-stu-id="465b7-140">When refreshing, adding, and completing items in this sample, you can omit the explicit **push** call, since it may be redundant.</span></span>

<span data-ttu-id="465b7-141">In the provided code, all records in the remote todoItem table are queried, but it is also possible to filter records by passing a query id and query to **push**.</span><span class="sxs-lookup"><span data-stu-id="465b7-141">In the provided code, all records in the remote todoItem table are queried, but it is also possible to filter records by passing a query id and query to **push**.</span></span> <span data-ttu-id="465b7-142">For more information, see the section *Incremental Sync* in [Offline Data Sync in Azure Mobile Apps].</span><span class="sxs-lookup"><span data-stu-id="465b7-142">For more information, see the section *Incremental Sync* in [Offline Data Sync in Azure Mobile Apps].</span></span>

## <a name="optional-disable-authentication"></a><span data-ttu-id="465b7-143">(Optional) Disable authentication</span><span class="sxs-lookup"><span data-stu-id="465b7-143">(Optional) Disable authentication</span></span>

<span data-ttu-id="465b7-144">If you don't want to set up authentication before testing offline sync, comment out the callback function for login, but leave the code inside the callback function uncommented.</span><span class="sxs-lookup"><span data-stu-id="465b7-144">If you don't want to set up authentication before testing offline sync, comment out the callback function for login, but leave the code inside the callback function uncommented.</span></span>  <span data-ttu-id="465b7-145">After commenting out the login lines, the code follows:</span><span class="sxs-lookup"><span data-stu-id="465b7-145">After commenting out the login lines, the code follows:</span></span>

      // Login to the service.
      // client.login('twitter')
      //    .then(function () {
        syncContext.initialize(store).then(function () {
          // Leave the rest of the code in this callback function  uncommented.
                ...
        });
      // }, handleError);

<span data-ttu-id="465b7-146">Now, the app syncs with the Azure backend when you run the app.</span><span class="sxs-lookup"><span data-stu-id="465b7-146">Now, the app syncs with the Azure backend when you run the app.</span></span>

## <a name="run-the-client-app"></a><span data-ttu-id="465b7-147">Run the client app</span><span class="sxs-lookup"><span data-stu-id="465b7-147">Run the client app</span></span>
<span data-ttu-id="465b7-148">With offline sync now enabled, you can run the client application at least once on each platform to populate the local store database.</span><span class="sxs-lookup"><span data-stu-id="465b7-148">With offline sync now enabled, you can run the client application at least once on each platform to populate the local store database.</span></span> <span data-ttu-id="465b7-149">Later, simulate an offline scenario and modify the data in the local store while the app is offline.</span><span class="sxs-lookup"><span data-stu-id="465b7-149">Later, simulate an offline scenario and modify the data in the local store while the app is offline.</span></span>

## <a name="optional-test-the-sync-behavior"></a><span data-ttu-id="465b7-150">(Optional) Test the sync behavior</span><span class="sxs-lookup"><span data-stu-id="465b7-150">(Optional) Test the sync behavior</span></span>
<span data-ttu-id="465b7-151">In this section, you modify the client project to simulate an offline scenario by using an invalid application URL for your backend.</span><span class="sxs-lookup"><span data-stu-id="465b7-151">In this section, you modify the client project to simulate an offline scenario by using an invalid application URL for your backend.</span></span> <span data-ttu-id="465b7-152">When you add or change data items, these changes are held in the local store, but are not synced to the backend data store until the connection is re-established.</span><span class="sxs-lookup"><span data-stu-id="465b7-152">When you add or change data items, these changes are held in the local store, but are not synced to the backend data store until the connection is re-established.</span></span>

1. <span data-ttu-id="465b7-153">In the Solution Explorer, open the index.js project file and change the application URL to point to  an invalid URL, like the following code:</span><span class="sxs-lookup"><span data-stu-id="465b7-153">In the Solution Explorer, open the index.js project file and change the application URL to point to  an invalid URL, like the following code:</span></span>

        client = new WindowsAzure.MobileServiceClient('http://yourmobileapp.azurewebsites.net-fail');

2. <span data-ttu-id="465b7-154">In index.html, update the CSP `<meta>` element with the same invalid URL.</span><span class="sxs-lookup"><span data-stu-id="465b7-154">In index.html, update the CSP `<meta>` element with the same invalid URL.</span></span>

        <meta http-equiv="Content-Security-Policy" content="default-src 'self' data: gap: http://yourmobileapp.azurewebsites.net-fail; style-src 'self'; media-src *">

3. <span data-ttu-id="465b7-155">Build and run the client app and notice that an exception is logged in the console when the app attempts to sync with the backend after login.</span><span class="sxs-lookup"><span data-stu-id="465b7-155">Build and run the client app and notice that an exception is logged in the console when the app attempts to sync with the backend after login.</span></span> <span data-ttu-id="465b7-156">Any new items you add exist only in the local store until they are pushed to the mobile backend.</span><span class="sxs-lookup"><span data-stu-id="465b7-156">Any new items you add exist only in the local store until they are pushed to the mobile backend.</span></span> <span data-ttu-id="465b7-157">The client app behaves as if it is connected to the backend.</span><span class="sxs-lookup"><span data-stu-id="465b7-157">The client app behaves as if it is connected to the backend.</span></span>

4. <span data-ttu-id="465b7-158">Close the app and restart it to verify that the new items you created are persisted to the local store.</span><span class="sxs-lookup"><span data-stu-id="465b7-158">Close the app and restart it to verify that the new items you created are persisted to the local store.</span></span>

5. <span data-ttu-id="465b7-159">(Optional) Use Visual Studio to view your Azure SQL Database table to see that the data in the backend database has not changed.</span><span class="sxs-lookup"><span data-stu-id="465b7-159">(Optional) Use Visual Studio to view your Azure SQL Database table to see that the data in the backend database has not changed.</span></span>

    <span data-ttu-id="465b7-160">In Visual Studio, open **Server Explorer**.</span><span class="sxs-lookup"><span data-stu-id="465b7-160">In Visual Studio, open **Server Explorer**.</span></span> <span data-ttu-id="465b7-161">Navigate to your database in **Azure**->**SQL Databases**.</span><span class="sxs-lookup"><span data-stu-id="465b7-161">Navigate to your database in **Azure**->**SQL Databases**.</span></span> <span data-ttu-id="465b7-162">Right-click your database and select **Open in SQL Server Object Explorer**.</span><span class="sxs-lookup"><span data-stu-id="465b7-162">Right-click your database and select **Open in SQL Server Object Explorer**.</span></span> <span data-ttu-id="465b7-163">Now you can browse to your SQL database table and its contents.</span><span class="sxs-lookup"><span data-stu-id="465b7-163">Now you can browse to your SQL database table and its contents.</span></span>

## <a name="optional-test-the-reconnection-to-your-mobile-backend"></a><span data-ttu-id="465b7-164">(Optional) Test the reconnection to your mobile backend</span><span class="sxs-lookup"><span data-stu-id="465b7-164">(Optional) Test the reconnection to your mobile backend</span></span>

<span data-ttu-id="465b7-165">In this section, you reconnect the app to the mobile backend, which simulates the app coming back to an online state.</span><span class="sxs-lookup"><span data-stu-id="465b7-165">In this section, you reconnect the app to the mobile backend, which simulates the app coming back to an online state.</span></span> <span data-ttu-id="465b7-166">When you log in, data is synced to your mobile backend.</span><span class="sxs-lookup"><span data-stu-id="465b7-166">When you log in, data is synced to your mobile backend.</span></span>

1. <span data-ttu-id="465b7-167">Reopen index.js and restore the application URL.</span><span class="sxs-lookup"><span data-stu-id="465b7-167">Reopen index.js and restore the application URL.</span></span>
2. <span data-ttu-id="465b7-168">Reopen index.html and correct the application URL in the CSP `<meta>` element.</span><span class="sxs-lookup"><span data-stu-id="465b7-168">Reopen index.html and correct the application URL in the CSP `<meta>` element.</span></span>
3. <span data-ttu-id="465b7-169">Rebuild and run the client app.</span><span class="sxs-lookup"><span data-stu-id="465b7-169">Rebuild and run the client app.</span></span> <span data-ttu-id="465b7-170">The app attempts to sync with the mobile app backend after login.</span><span class="sxs-lookup"><span data-stu-id="465b7-170">The app attempts to sync with the mobile app backend after login.</span></span> <span data-ttu-id="465b7-171">Verify that no exceptions are logged in the debug console.</span><span class="sxs-lookup"><span data-stu-id="465b7-171">Verify that no exceptions are logged in the debug console.</span></span>
4. <span data-ttu-id="465b7-172">(Optional) View the updated data using either SQL Server Object Explorer or a REST tool like Fiddler.</span><span class="sxs-lookup"><span data-stu-id="465b7-172">(Optional) View the updated data using either SQL Server Object Explorer or a REST tool like Fiddler.</span></span> <span data-ttu-id="465b7-173">Notice the data has been synchronized between the backend database and the local store.</span><span class="sxs-lookup"><span data-stu-id="465b7-173">Notice the data has been synchronized between the backend database and the local store.</span></span>

    <span data-ttu-id="465b7-174">Notice the data has been synchronized between the database and the local store and contains the items you added while your app was disconnected.</span><span class="sxs-lookup"><span data-stu-id="465b7-174">Notice the data has been synchronized between the database and the local store and contains the items you added while your app was disconnected.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="465b7-175">Additional resources</span><span class="sxs-lookup"><span data-stu-id="465b7-175">Additional resources</span></span>
* <span data-ttu-id="465b7-176">[Offline Data Sync in Azure Mobile Apps]</span><span class="sxs-lookup"><span data-stu-id="465b7-176">[Offline Data Sync in Azure Mobile Apps]</span></span>
* <span data-ttu-id="465b7-177">[Visual Studio Tools for Apache Cordova]</span><span class="sxs-lookup"><span data-stu-id="465b7-177">[Visual Studio Tools for Apache Cordova]</span></span>

## <a name="next-steps"></a><span data-ttu-id="465b7-178">Next steps</span><span class="sxs-lookup"><span data-stu-id="465b7-178">Next steps</span></span>
* <span data-ttu-id="465b7-179">Review more advanced offline sync features such as conflict resolution in the [offline sync sample]</span><span class="sxs-lookup"><span data-stu-id="465b7-179">Review more advanced offline sync features such as conflict resolution in the [offline sync sample]</span></span>
* <span data-ttu-id="465b7-180">Review the offline sync API reference in the [API documentation](https://azure.github.io/azure-mobile-apps-js-client).</span><span class="sxs-lookup"><span data-stu-id="465b7-180">Review the offline sync API reference in the [API documentation](https://azure.github.io/azure-mobile-apps-js-client).</span></span>

<!-- ##Summary -->

<!-- Images -->

<!-- URLs. -->
[Apache Cordova quick start]: app-service-mobile-cordova-get-started.md
[offline sync sample]: https://github.com/Azure-Samples/app-service-mobile-cordova-client-conflict-handling
[Offline Data Sync in Azure Mobile Apps]: app-service-mobile-offline-data-sync.md
[Cloud Cover: Offline Sync in Azure Mobile Services]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri
[Adding Authentication]: app-service-mobile-cordova-get-started-users.md
[authentication]: app-service-mobile-cordova-get-started-users.md
[Work with the .NET backend server SDK for Azure Mobile Apps]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Visual Studio Community 2015]: http://www.visualstudio.com/
[Visual Studio Tools for Apache Cordova]: https://www.visualstudio.com/en-us/features/cordova-vs.aspx
[Apache Cordova SDK]: app-service-mobile-cordova-how-to-use-client-library.md
[ASP.NET Server SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Node.js Server SDK]: app-service-mobile-node-backend-how-to-use-server-sdk.md
