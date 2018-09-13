---
title: Enable offline sync for your Azure Mobile App (Android)
description: Learn how to use App Service Mobile Apps to cache and sync offline data in your Android application
documentationcenter: android
author: ysxu
manager: adrianha
services: app-service\mobile
ms.assetid: 32a8a079-9b3c-4faf-8588-ccff02097224
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 10/01/2016
ms.author: yuaxu
ms.openlocfilehash: 6135c042010147270e06740038afe80efc738f2d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661803"
---
# <a name="enable-offline-sync-for-your-android-mobile-app"></a><span data-ttu-id="122ed-103">Enable offline sync for your Android mobile app</span><span class="sxs-lookup"><span data-stu-id="122ed-103">Enable offline sync for your Android mobile app</span></span>
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a><span data-ttu-id="122ed-104">Overview</span><span class="sxs-lookup"><span data-stu-id="122ed-104">Overview</span></span>
<span data-ttu-id="122ed-105">This tutorial covers the offline sync feature of Azure Mobile Apps for Android.</span><span class="sxs-lookup"><span data-stu-id="122ed-105">This tutorial covers the offline sync feature of Azure Mobile Apps for Android.</span></span> <span data-ttu-id="122ed-106">Offline sync allows end users to interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span><span class="sxs-lookup"><span data-stu-id="122ed-106">Offline sync allows end users to interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span> <span data-ttu-id="122ed-107">Changes are stored in a local database.</span><span class="sxs-lookup"><span data-stu-id="122ed-107">Changes are stored in a local database.</span></span> <span data-ttu-id="122ed-108">Once the device is back online, these changes are synced with the remote backend.</span><span class="sxs-lookup"><span data-stu-id="122ed-108">Once the device is back online, these changes are synced with the remote backend.</span></span>

<span data-ttu-id="122ed-109">If this is your first experience with Azure Mobile Apps, you should first complete the tutorial [Create an Android App].</span><span class="sxs-lookup"><span data-stu-id="122ed-109">If this is your first experience with Azure Mobile Apps, you should first complete the tutorial [Create an Android App].</span></span> <span data-ttu-id="122ed-110">If you do not use the downloaded quick start server project, you must add the data access extension packages to your project.</span><span class="sxs-lookup"><span data-stu-id="122ed-110">If you do not use the downloaded quick start server project, you must add the data access extension packages to your project.</span></span> <span data-ttu-id="122ed-111">For more information about server extension packages, see [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="122ed-111">For more information about server extension packages, see [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

<span data-ttu-id="122ed-112">To learn more about the offline sync feature, see the topic [Offline Data Sync in Azure Mobile Apps].</span><span class="sxs-lookup"><span data-stu-id="122ed-112">To learn more about the offline sync feature, see the topic [Offline Data Sync in Azure Mobile Apps].</span></span>

## <a name="update-the-app-to-support-offline-sync"></a><span data-ttu-id="122ed-113">Update the app to support offline sync</span><span class="sxs-lookup"><span data-stu-id="122ed-113">Update the app to support offline sync</span></span>
<span data-ttu-id="122ed-114">With offline sync, you read to and write from a *sync table* (using the *IMobileServiceSyncTable* interface), which is part of a **SQLite** database on your device.</span><span class="sxs-lookup"><span data-stu-id="122ed-114">With offline sync, you read to and write from a *sync table* (using the *IMobileServiceSyncTable* interface), which is part of a **SQLite** database on your device.</span></span>

<span data-ttu-id="122ed-115">To push and pull changes between the device and Azure Mobile Services, you use a *synchronization context* (*MobileServiceClient.SyncContext*), which you initialize with the local database to store data locally.</span><span class="sxs-lookup"><span data-stu-id="122ed-115">To push and pull changes between the device and Azure Mobile Services, you use a *synchronization context* (*MobileServiceClient.SyncContext*), which you initialize with the local database to store data locally.</span></span>

1. <span data-ttu-id="122ed-116">In `TodoActivity.java`, comment out the existing definition of `mToDoTable` and uncomment the sync table version:</span><span class="sxs-lookup"><span data-stu-id="122ed-116">In `TodoActivity.java`, comment out the existing definition of `mToDoTable` and uncomment the sync table version:</span></span>
   
        private MobileServiceSyncTable<ToDoItem> mToDoTable;
2. <span data-ttu-id="122ed-117">In the `onCreate` method, comment out the existing initialization of `mToDoTable` and uncomment this definition:</span><span class="sxs-lookup"><span data-stu-id="122ed-117">In the `onCreate` method, comment out the existing initialization of `mToDoTable` and uncomment this definition:</span></span>
   
        mToDoTable = mClient.getSyncTable("ToDoItem", ToDoItem.class);
3. <span data-ttu-id="122ed-118">In `refreshItemsFromTable` comment out the definition of `results` and uncomment this definition:</span><span class="sxs-lookup"><span data-stu-id="122ed-118">In `refreshItemsFromTable` comment out the definition of `results` and uncomment this definition:</span></span>
   
        // Offline Sync
        final List<ToDoItem> results = refreshItemsFromMobileServiceTableSyncTable();
4. <span data-ttu-id="122ed-119">Comment out the definition of `refreshItemsFromMobileServiceTable`.</span><span class="sxs-lookup"><span data-stu-id="122ed-119">Comment out the definition of `refreshItemsFromMobileServiceTable`.</span></span>
5. <span data-ttu-id="122ed-120">Uncomment the definition of `refreshItemsFromMobileServiceTableSyncTable`:</span><span class="sxs-lookup"><span data-stu-id="122ed-120">Uncomment the definition of `refreshItemsFromMobileServiceTableSyncTable`:</span></span>
   
        private List<ToDoItem> refreshItemsFromMobileServiceTableSyncTable() throws ExecutionException, InterruptedException {
            //sync the data
            sync().get();
            Query query = QueryOperations.field("complete").
                    eq(val(false));
            return mToDoTable.read(query).get();
        }
6. <span data-ttu-id="122ed-121">Uncomment the definition of `sync`:</span><span class="sxs-lookup"><span data-stu-id="122ed-121">Uncomment the definition of `sync`:</span></span>
   
        private AsyncTask<Void, Void, Void> sync() {
            AsyncTask<Void, Void, Void> task = new AsyncTask<Void, Void, Void>(){
                @Override
                protected Void doInBackground(Void... params) {
                    try {
                        MobileServiceSyncContext syncContext = mClient.getSyncContext();
                        syncContext.push().get();
                        mToDoTable.pull(null).get();
                    } catch (final Exception e) {
                        createAndShowDialogFromTask(e, "Error");
                    }
                    return null;
                }
            };
            return runAsyncTask(task);
        }

## <a name="test-the-app"></a><span data-ttu-id="122ed-122">Test the app</span><span class="sxs-lookup"><span data-stu-id="122ed-122">Test the app</span></span>
<span data-ttu-id="122ed-123">In this section, you test the behavior with WiFi on, and then turn off WiFi to create an offline scenario.</span><span class="sxs-lookup"><span data-stu-id="122ed-123">In this section, you test the behavior with WiFi on, and then turn off WiFi to create an offline scenario.</span></span>

<span data-ttu-id="122ed-124">When you add data items, they are held in the local SQLite store, but not synced to the mobile service until you press the **Refresh** button.</span><span class="sxs-lookup"><span data-stu-id="122ed-124">When you add data items, they are held in the local SQLite store, but not synced to the mobile service until you press the **Refresh** button.</span></span> <span data-ttu-id="122ed-125">Other apps may have different requirements regarding when data needs to be synchronized, but for demo purposes this tutorial has the user explicitly request it.</span><span class="sxs-lookup"><span data-stu-id="122ed-125">Other apps may have different requirements regarding when data needs to be synchronized, but for demo purposes this tutorial has the user explicitly request it.</span></span>

<span data-ttu-id="122ed-126">When you press that button, a new background task starts.</span><span class="sxs-lookup"><span data-stu-id="122ed-126">When you press that button, a new background task starts.</span></span> <span data-ttu-id="122ed-127">It first pushes all changes made to the local store using synchronization context, then pulls all changed data from Azure to the local table.</span><span class="sxs-lookup"><span data-stu-id="122ed-127">It first pushes all changes made to the local store using synchronization context, then pulls all changed data from Azure to the local table.</span></span>

### <a name="offline-testing"></a><span data-ttu-id="122ed-128">Offline testing</span><span class="sxs-lookup"><span data-stu-id="122ed-128">Offline testing</span></span>
1. <span data-ttu-id="122ed-129">Place the device or simulator in *Airplane Mode*.</span><span class="sxs-lookup"><span data-stu-id="122ed-129">Place the device or simulator in *Airplane Mode*.</span></span> <span data-ttu-id="122ed-130">This creates an offline scenario.</span><span class="sxs-lookup"><span data-stu-id="122ed-130">This creates an offline scenario.</span></span>
2. <span data-ttu-id="122ed-131">Add some *ToDo* items, or mark some items as complete.</span><span class="sxs-lookup"><span data-stu-id="122ed-131">Add some *ToDo* items, or mark some items as complete.</span></span> <span data-ttu-id="122ed-132">Quit the device or simulator (or forcibly close the app) and restart.</span><span class="sxs-lookup"><span data-stu-id="122ed-132">Quit the device or simulator (or forcibly close the app) and restart.</span></span> <span data-ttu-id="122ed-133">Verify that your changes have been persisted on the device because they are held in the local SQLite store.</span><span class="sxs-lookup"><span data-stu-id="122ed-133">Verify that your changes have been persisted on the device because they are held in the local SQLite store.</span></span>
3. <span data-ttu-id="122ed-134">View the contents of the Azure *TodoItem* table either with a SQL tool such as *SQL Server Management Studio*, or a REST client such as *Fiddler* or *Postman*.</span><span class="sxs-lookup"><span data-stu-id="122ed-134">View the contents of the Azure *TodoItem* table either with a SQL tool such as *SQL Server Management Studio*, or a REST client such as *Fiddler* or *Postman*.</span></span> <span data-ttu-id="122ed-135">Verify that the new items have *not* been synced to the server</span><span class="sxs-lookup"><span data-stu-id="122ed-135">Verify that the new items have *not* been synced to the server</span></span>
   
       + <span data-ttu-id="122ed-136">For a Node.js backend, go to the [Azure portal](https://portal.azure.com/), and in your Mobile App backend click **Easy Tables** > **TodoItem** to view the contents of the `TodoItem` table.</span><span class="sxs-lookup"><span data-stu-id="122ed-136">For a Node.js backend, go to the [Azure portal](https://portal.azure.com/), and in your Mobile App backend click **Easy Tables** > **TodoItem** to view the contents of the `TodoItem` table.</span></span>
       + <span data-ttu-id="122ed-137">For a .NET backend, view the table contents either with a SQL tool such as *SQL Server Management Studio*, or a REST client such as *Fiddler* or *Postman*.</span><span class="sxs-lookup"><span data-stu-id="122ed-137">For a .NET backend, view the table contents either with a SQL tool such as *SQL Server Management Studio*, or a REST client such as *Fiddler* or *Postman*.</span></span>
4. <span data-ttu-id="122ed-138">Turn on WiFi in the device or simulator.</span><span class="sxs-lookup"><span data-stu-id="122ed-138">Turn on WiFi in the device or simulator.</span></span> <span data-ttu-id="122ed-139">Next, press the **Refresh** button.</span><span class="sxs-lookup"><span data-stu-id="122ed-139">Next, press the **Refresh** button.</span></span>
5. <span data-ttu-id="122ed-140">View the TodoItem data again in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="122ed-140">View the TodoItem data again in the Azure portal.</span></span> <span data-ttu-id="122ed-141">The new and changed TodoItems should now appear.</span><span class="sxs-lookup"><span data-stu-id="122ed-141">The new and changed TodoItems should now appear.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="122ed-142">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="122ed-142">Additional Resources</span></span>
* <span data-ttu-id="122ed-143">[Offline Data Sync in Azure Mobile Apps]</span><span class="sxs-lookup"><span data-stu-id="122ed-143">[Offline Data Sync in Azure Mobile Apps]</span></span>
* <span data-ttu-id="122ed-144">[Cloud Cover: Offline Sync in Azure Mobile Services] \(note: the video is on Mobile Services, but offline sync works in a similar way in Azure Mobile Apps\)</span><span class="sxs-lookup"><span data-stu-id="122ed-144">[Cloud Cover: Offline Sync in Azure Mobile Services] \(note: the video is on Mobile Services, but offline sync works in a similar way in Azure Mobile Apps\)</span></span>

<!-- URLs. -->

[Offline Data Sync in Azure Mobile Apps]: app-service-mobile-offline-data-sync.md

[Create an Android App]: app-service-mobile-android-get-started.md

[Cloud Cover: Offline Sync in Azure Mobile Services]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri
[Azure Friday: Offline-enabled apps in Azure Mobile Services]: http://azure.microsoft.com/documentation/videos/azure-mobile-services-offline-enabled-apps-with-donna-malayeri/

