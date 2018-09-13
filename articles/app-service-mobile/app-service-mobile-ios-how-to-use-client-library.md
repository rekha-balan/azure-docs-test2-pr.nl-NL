---
title: How to Use iOS SDK for Azure Mobile Apps
description: How to Use iOS SDK for Azure Mobile Apps
services: app-service\mobile
documentationcenter: ios
author: conceptdev
editor: ''
ms.assetid: 4e8e45df-c36a-4a60-9ad4-393ec10b7eb9
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 10/01/2016
ms.author: crdun
ms.openlocfilehash: 0de561b177a1474b0ce4f0f203803e8265db5e7a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44812252"
---
# <a name="how-to-use-ios-client-library-for-azure-mobile-apps"></a><span data-ttu-id="91528-103">How to Use iOS Client Library for Azure Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="91528-103">How to Use iOS Client Library for Azure Mobile Apps</span></span>

[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

<span data-ttu-id="91528-104">This guide teaches you to perform common scenarios using the latest [Azure Mobile Apps iOS SDK][1].</span><span class="sxs-lookup"><span data-stu-id="91528-104">This guide teaches you to perform common scenarios using the latest [Azure Mobile Apps iOS SDK][1].</span></span> <span data-ttu-id="91528-105">If you are new to Azure Mobile Apps, first complete [Azure Mobile Apps Quick Start] to create a backend, create a table, and download a pre-built iOS Xcode project.</span><span class="sxs-lookup"><span data-stu-id="91528-105">If you are new to Azure Mobile Apps, first complete [Azure Mobile Apps Quick Start] to create a backend, create a table, and download a pre-built iOS Xcode project.</span></span> <span data-ttu-id="91528-106">In this guide, we focus on the client-side iOS SDK.</span><span class="sxs-lookup"><span data-stu-id="91528-106">In this guide, we focus on the client-side iOS SDK.</span></span> <span data-ttu-id="91528-107">To learn more about the server-side SDK for the backend, see the Server SDK HOWTOs.</span><span class="sxs-lookup"><span data-stu-id="91528-107">To learn more about the server-side SDK for the backend, see the Server SDK HOWTOs.</span></span>

## <a name="reference-documentation"></a><span data-ttu-id="91528-108">Reference documentation</span><span class="sxs-lookup"><span data-stu-id="91528-108">Reference documentation</span></span>

<span data-ttu-id="91528-109">The reference documentation for the iOS client SDK is located here: [Azure Mobile Apps iOS Client Reference][2].</span><span class="sxs-lookup"><span data-stu-id="91528-109">The reference documentation for the iOS client SDK is located here: [Azure Mobile Apps iOS Client Reference][2].</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="91528-110">Supported Platforms</span><span class="sxs-lookup"><span data-stu-id="91528-110">Supported Platforms</span></span>

<span data-ttu-id="91528-111">The iOS SDK supports Objective-C projects, Swift 2.2 projects, and Swift 2.3 projects for iOS versions 8.0 or later.</span><span class="sxs-lookup"><span data-stu-id="91528-111">The iOS SDK supports Objective-C projects, Swift 2.2 projects, and Swift 2.3 projects for iOS versions 8.0 or later.</span></span>

<span data-ttu-id="91528-112">The "server-flow" authentication uses a WebView for the presented UI.</span><span class="sxs-lookup"><span data-stu-id="91528-112">The "server-flow" authentication uses a WebView for the presented UI.</span></span>  <span data-ttu-id="91528-113">If the device is not able to present a WebView UI, then another method of authentication is required that is outside the scope of the product.</span><span class="sxs-lookup"><span data-stu-id="91528-113">If the device is not able to present a WebView UI, then another method of authentication is required that is outside the scope of the product.</span></span>  
<span data-ttu-id="91528-114">This SDK is thus not suitable for Watch-type or similarly restricted devices.</span><span class="sxs-lookup"><span data-stu-id="91528-114">This SDK is thus not suitable for Watch-type or similarly restricted devices.</span></span>

## <a name="Setup"></a><span data-ttu-id="91528-115">Setup and Prerequisites</span><span class="sxs-lookup"><span data-stu-id="91528-115">Setup and Prerequisites</span></span>

<span data-ttu-id="91528-116">This guide assumes that you have created a backend with a table.</span><span class="sxs-lookup"><span data-stu-id="91528-116">This guide assumes that you have created a backend with a table.</span></span> <span data-ttu-id="91528-117">This guide assumes that the table has the same schema as the tables in those tutorials.</span><span class="sxs-lookup"><span data-stu-id="91528-117">This guide assumes that the table has the same schema as the tables in those tutorials.</span></span> <span data-ttu-id="91528-118">This guide also assumes that in your code, you reference `MicrosoftAzureMobile.framework` and import `MicrosoftAzureMobile/MicrosoftAzureMobile.h`.</span><span class="sxs-lookup"><span data-stu-id="91528-118">This guide also assumes that in your code, you reference `MicrosoftAzureMobile.framework` and import `MicrosoftAzureMobile/MicrosoftAzureMobile.h`.</span></span>

## <a name="create-client"></a><span data-ttu-id="91528-119">How to: Create Client</span><span class="sxs-lookup"><span data-stu-id="91528-119">How to: Create Client</span></span>

<span data-ttu-id="91528-120">To access an Azure Mobile Apps backend in your project, create an `MSClient`.</span><span class="sxs-lookup"><span data-stu-id="91528-120">To access an Azure Mobile Apps backend in your project, create an `MSClient`.</span></span> <span data-ttu-id="91528-121">Replace `AppUrl` with the app URL.</span><span class="sxs-lookup"><span data-stu-id="91528-121">Replace `AppUrl` with the app URL.</span></span> <span data-ttu-id="91528-122">You may leave `gatewayURLString` and `applicationKey` empty.</span><span class="sxs-lookup"><span data-stu-id="91528-122">You may leave `gatewayURLString` and `applicationKey` empty.</span></span> <span data-ttu-id="91528-123">If you set up a gateway for authentication, populate `gatewayURLString` with the gateway URL.</span><span class="sxs-lookup"><span data-stu-id="91528-123">If you set up a gateway for authentication, populate `gatewayURLString` with the gateway URL.</span></span>

<span data-ttu-id="91528-124">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="91528-124">**Objective-C**:</span></span>

```objc
MSClient *client = [MSClient clientWithApplicationURLString:@"AppUrl"];
```

<span data-ttu-id="91528-125">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="91528-125">**Swift**:</span></span>

```swift
let client = MSClient(applicationURLString: "AppUrl")
```

## <a name="table-reference"></a><span data-ttu-id="91528-126">How to: Create Table Reference</span><span class="sxs-lookup"><span data-stu-id="91528-126">How to: Create Table Reference</span></span>

<span data-ttu-id="91528-127">To access or update data, create a reference to the backend table.</span><span class="sxs-lookup"><span data-stu-id="91528-127">To access or update data, create a reference to the backend table.</span></span> <span data-ttu-id="91528-128">Replace `TodoItem` with the name of your table</span><span class="sxs-lookup"><span data-stu-id="91528-128">Replace `TodoItem` with the name of your table</span></span>

<span data-ttu-id="91528-129">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="91528-129">**Objective-C**:</span></span>

```objc
MSTable *table = [client tableWithName:@"TodoItem"];
```

<span data-ttu-id="91528-130">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="91528-130">**Swift**:</span></span>

```swift
let table = client.tableWithName("TodoItem")
```

## <a name="querying"></a><span data-ttu-id="91528-131">How to: Query Data</span><span class="sxs-lookup"><span data-stu-id="91528-131">How to: Query Data</span></span>

<span data-ttu-id="91528-132">To create a database query, query the `MSTable` object.</span><span class="sxs-lookup"><span data-stu-id="91528-132">To create a database query, query the `MSTable` object.</span></span> <span data-ttu-id="91528-133">The following query gets all the items in `TodoItem` and logs the text of each item.</span><span class="sxs-lookup"><span data-stu-id="91528-133">The following query gets all the items in `TodoItem` and logs the text of each item.</span></span>

<span data-ttu-id="91528-134">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="91528-134">**Objective-C**:</span></span>

```objc
[table readWithCompletion:^(MSQueryResult *result, NSError *error) {
        if(error) { // error is nil if no error occured
                NSLog(@"ERROR %@", error);
        } else {
                for(NSDictionary *item in result.items) { // items is NSArray of records that match query
                        NSLog(@"Todo Item: %@", [item objectForKey:@"text"]);
                }
        }
}];
```

<span data-ttu-id="91528-135">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="91528-135">**Swift**:</span></span>

```swift
table.readWithCompletion { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let items = result?.items {
        for item in items {
            print("Todo Item: ", item["text"])
        }
    }
}
```

## <a name="filtering"></a><span data-ttu-id="91528-136">How to: Filter Returned Data</span><span class="sxs-lookup"><span data-stu-id="91528-136">How to: Filter Returned Data</span></span>

<span data-ttu-id="91528-137">To filter results, there are many available options.</span><span class="sxs-lookup"><span data-stu-id="91528-137">To filter results, there are many available options.</span></span>

<span data-ttu-id="91528-138">To filter using a predicate, use an `NSPredicate` and `readWithPredicate`.</span><span class="sxs-lookup"><span data-stu-id="91528-138">To filter using a predicate, use an `NSPredicate` and `readWithPredicate`.</span></span> <span data-ttu-id="91528-139">The following filters returned data to find only incomplete Todo items.</span><span class="sxs-lookup"><span data-stu-id="91528-139">The following filters returned data to find only incomplete Todo items.</span></span>

<span data-ttu-id="91528-140">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="91528-140">**Objective-C**:</span></span>

```objc
// Create a predicate that finds items where complete is false
NSPredicate * predicate = [NSPredicate predicateWithFormat:@"complete == NO"];
// Query the TodoItem table
[table readWithPredicate:predicate completion:^(MSQueryResult *result, NSError *error) {
        if(error) {
                NSLog(@"ERROR %@", error);
        } else {
                for(NSDictionary *item in result.items) {
                        NSLog(@"Todo Item: %@", [item objectForKey:@"text"]);
                }
        }
}];
```

<span data-ttu-id="91528-141">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="91528-141">**Swift**:</span></span>

```swift
// Create a predicate that finds items where complete is false
let predicate =  NSPredicate(format: "complete == NO")
// Query the TodoItem table
table.readWithPredicate(predicate) { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let items = result?.items {
        for item in items {
            print("Todo Item: ", item["text"])
        }
    }
}
```

## <a name="query-object"></a><span data-ttu-id="91528-142">How to: Use MSQuery</span><span class="sxs-lookup"><span data-stu-id="91528-142">How to: Use MSQuery</span></span>

<span data-ttu-id="91528-143">To perform a complex query (including sorting and paging), create an `MSQuery` object, directly or by using a predicate:</span><span class="sxs-lookup"><span data-stu-id="91528-143">To perform a complex query (including sorting and paging), create an `MSQuery` object, directly or by using a predicate:</span></span>

<span data-ttu-id="91528-144">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="91528-144">**Objective-C**:</span></span>

```objc
MSQuery *query = [table query];
MSQuery *query = [table queryWithPredicate: [NSPredicate predicateWithFormat:@"complete == NO"]];
```

<span data-ttu-id="91528-145">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="91528-145">**Swift**:</span></span>

```swift
let query = table.query()
let query = table.queryWithPredicate(NSPredicate(format: "complete == NO"))
```

<span data-ttu-id="91528-146">`MSQuery` lets you control several query behaviors.</span><span class="sxs-lookup"><span data-stu-id="91528-146">`MSQuery` lets you control several query behaviors.</span></span>

* <span data-ttu-id="91528-147">Specify order of results</span><span class="sxs-lookup"><span data-stu-id="91528-147">Specify order of results</span></span>
* <span data-ttu-id="91528-148">Limit which fields to return</span><span class="sxs-lookup"><span data-stu-id="91528-148">Limit which fields to return</span></span>
* <span data-ttu-id="91528-149">Limit how many records to return</span><span class="sxs-lookup"><span data-stu-id="91528-149">Limit how many records to return</span></span>
* <span data-ttu-id="91528-150">Specify total count in response</span><span class="sxs-lookup"><span data-stu-id="91528-150">Specify total count in response</span></span>
* <span data-ttu-id="91528-151">Specify custom query string parameters in request</span><span class="sxs-lookup"><span data-stu-id="91528-151">Specify custom query string parameters in request</span></span>
* <span data-ttu-id="91528-152">Apply additional functions</span><span class="sxs-lookup"><span data-stu-id="91528-152">Apply additional functions</span></span>

<span data-ttu-id="91528-153">Execute an `MSQuery` query by calling `readWithCompletion` on the object.</span><span class="sxs-lookup"><span data-stu-id="91528-153">Execute an `MSQuery` query by calling `readWithCompletion` on the object.</span></span>

## <a name="sorting"></a><span data-ttu-id="91528-154">How to: Sort Data with MSQuery</span><span class="sxs-lookup"><span data-stu-id="91528-154">How to: Sort Data with MSQuery</span></span>

<span data-ttu-id="91528-155">To sort results, let's look at an example.</span><span class="sxs-lookup"><span data-stu-id="91528-155">To sort results, let's look at an example.</span></span> <span data-ttu-id="91528-156">To sort by field 'text' ascending, then by 'complete' descending, invoke `MSQuery` like so:</span><span class="sxs-lookup"><span data-stu-id="91528-156">To sort by field 'text' ascending, then by 'complete' descending, invoke `MSQuery` like so:</span></span>

<span data-ttu-id="91528-157">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="91528-157">**Objective-C**:</span></span>

```objc
[query orderByAscending:@"text"];
[query orderByDescending:@"complete"];
[query readWithCompletion:^(MSQueryResult *result, NSError *error) {
        if(error) {
                NSLog(@"ERROR %@", error);
        } else {
                for(NSDictionary *item in result.items) {
                        NSLog(@"Todo Item: %@", [item objectForKey:@"text"]);
                }
        }
}];
```

<span data-ttu-id="91528-158">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="91528-158">**Swift**:</span></span>

```swift
query.orderByAscending("text")
query.orderByDescending("complete")
query.readWithCompletion { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let items = result?.items {
        for item in items {
            print("Todo Item: ", item["text"])
        }
    }
}
```

## <a name="selecting"></a><span data-ttu-id="91528-159"><a name="parameters"></a>How to: Limit Fields and Expand Query String Parameters with MSQuery</span><span class="sxs-lookup"><span data-stu-id="91528-159"><a name="parameters"></a>How to: Limit Fields and Expand Query String Parameters with MSQuery</span></span>

<span data-ttu-id="91528-160">To limit fields to be returned in a query, specify the names of the fields in the **selectFields** property.</span><span class="sxs-lookup"><span data-stu-id="91528-160">To limit fields to be returned in a query, specify the names of the fields in the **selectFields** property.</span></span> <span data-ttu-id="91528-161">This example returns only the text and completed fields:</span><span class="sxs-lookup"><span data-stu-id="91528-161">This example returns only the text and completed fields:</span></span>

<span data-ttu-id="91528-162">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="91528-162">**Objective-C**:</span></span>

```objc
query.selectFields = @[@"text", @"complete"];
```

<span data-ttu-id="91528-163">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="91528-163">**Swift**:</span></span>

```swift
query.selectFields = ["text", "complete"]
```

<span data-ttu-id="91528-164">To include additional query string parameters in the server request (for example, because a custom server-side script uses them), populate `query.parameters` like so:</span><span class="sxs-lookup"><span data-stu-id="91528-164">To include additional query string parameters in the server request (for example, because a custom server-side script uses them), populate `query.parameters` like so:</span></span>

<span data-ttu-id="91528-165">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="91528-165">**Objective-C**:</span></span>

```objc
query.parameters = @{
    @"myKey1" : @"value1",
    @"myKey2" : @"value2",
};
```

<span data-ttu-id="91528-166">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="91528-166">**Swift**:</span></span>

```swift
query.parameters = ["myKey1": "value1", "myKey2": "value2"]
```

## <a name="paging"></a><span data-ttu-id="91528-167">How to: Configure Page Size</span><span class="sxs-lookup"><span data-stu-id="91528-167">How to: Configure Page Size</span></span>

<span data-ttu-id="91528-168">With Azure Mobile Apps, the page size controls the number of records that are pulled at a time from the backend tables.</span><span class="sxs-lookup"><span data-stu-id="91528-168">With Azure Mobile Apps, the page size controls the number of records that are pulled at a time from the backend tables.</span></span> <span data-ttu-id="91528-169">A call to `pull` data would then batch up data, based on this page size, until there are no more records to pull.</span><span class="sxs-lookup"><span data-stu-id="91528-169">A call to `pull` data would then batch up data, based on this page size, until there are no more records to pull.</span></span>

<span data-ttu-id="91528-170">It's possible to configure a page size using **MSPullSettings** as shown below.</span><span class="sxs-lookup"><span data-stu-id="91528-170">It's possible to configure a page size using **MSPullSettings** as shown below.</span></span> <span data-ttu-id="91528-171">The default page size is 50, and the example below changes it to 3.</span><span class="sxs-lookup"><span data-stu-id="91528-171">The default page size is 50, and the example below changes it to 3.</span></span>

<span data-ttu-id="91528-172">You could configure a different page size for performance reasons.</span><span class="sxs-lookup"><span data-stu-id="91528-172">You could configure a different page size for performance reasons.</span></span> <span data-ttu-id="91528-173">If you have a large number of small data records, a high page size reduces the number of server round-trips.</span><span class="sxs-lookup"><span data-stu-id="91528-173">If you have a large number of small data records, a high page size reduces the number of server round-trips.</span></span>

<span data-ttu-id="91528-174">This setting controls only the page size on the client side.</span><span class="sxs-lookup"><span data-stu-id="91528-174">This setting controls only the page size on the client side.</span></span> <span data-ttu-id="91528-175">If the client asks for a larger page size than the Mobile Apps backend supports, the page size is capped at the maximum the backend is configured to support.</span><span class="sxs-lookup"><span data-stu-id="91528-175">If the client asks for a larger page size than the Mobile Apps backend supports, the page size is capped at the maximum the backend is configured to support.</span></span>

<span data-ttu-id="91528-176">This setting is also the *number* of data records, not the *byte size*.</span><span class="sxs-lookup"><span data-stu-id="91528-176">This setting is also the *number* of data records, not the *byte size*.</span></span>

<span data-ttu-id="91528-177">If you increase the client page size, you should also increase the page size on the server.</span><span class="sxs-lookup"><span data-stu-id="91528-177">If you increase the client page size, you should also increase the page size on the server.</span></span> <span data-ttu-id="91528-178">See ["How to: Adjust the table paging size"](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for the steps to do this.</span><span class="sxs-lookup"><span data-stu-id="91528-178">See ["How to: Adjust the table paging size"](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for the steps to do this.</span></span>

<span data-ttu-id="91528-179">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="91528-179">**Objective-C**:</span></span>

```objc
  MSPullSettings *pullSettings = [[MSPullSettings alloc] initWithPageSize:3];
  [table  pullWithQuery:query queryId:@nil settings:pullSettings
                        completion:^(NSError * _Nullable error) {
                               if(error) {
                    NSLog(@"ERROR %@", error);
                }
                           }];
```

<span data-ttu-id="91528-180">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="91528-180">**Swift**:</span></span>

```swift
let pullSettings = MSPullSettings(pageSize: 3)
table.pullWithQuery(query, queryId:nil, settings: pullSettings) { (error) in
    if let err = error {
        print("ERROR ", err)
    }
}
```

## <a name="inserting"></a><span data-ttu-id="91528-181">How to: Insert Data</span><span class="sxs-lookup"><span data-stu-id="91528-181">How to: Insert Data</span></span>

<span data-ttu-id="91528-182">To insert a new table row, create a `NSDictionary` and invoke `table insert`.</span><span class="sxs-lookup"><span data-stu-id="91528-182">To insert a new table row, create a `NSDictionary` and invoke `table insert`.</span></span> <span data-ttu-id="91528-183">If [Dynamic Schema] is enabled, the Azure App Service mobile backend automatically generates new columns based on the `NSDictionary`.</span><span class="sxs-lookup"><span data-stu-id="91528-183">If [Dynamic Schema] is enabled, the Azure App Service mobile backend automatically generates new columns based on the `NSDictionary`.</span></span>

<span data-ttu-id="91528-184">If `id` is not provided, the backend automatically generates a new unique ID.</span><span class="sxs-lookup"><span data-stu-id="91528-184">If `id` is not provided, the backend automatically generates a new unique ID.</span></span> <span data-ttu-id="91528-185">Provide your own `id` to use email addresses, usernames, or your own custom values as ID.</span><span class="sxs-lookup"><span data-stu-id="91528-185">Provide your own `id` to use email addresses, usernames, or your own custom values as ID.</span></span> <span data-ttu-id="91528-186">Providing your own ID may ease joins and business-oriented database logic.</span><span class="sxs-lookup"><span data-stu-id="91528-186">Providing your own ID may ease joins and business-oriented database logic.</span></span>

<span data-ttu-id="91528-187">The `result` contains the new item that was inserted.</span><span class="sxs-lookup"><span data-stu-id="91528-187">The `result` contains the new item that was inserted.</span></span> <span data-ttu-id="91528-188">Depending on your server logic, it may have additional or modified data compared to what was passed to the server.</span><span class="sxs-lookup"><span data-stu-id="91528-188">Depending on your server logic, it may have additional or modified data compared to what was passed to the server.</span></span>

<span data-ttu-id="91528-189">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="91528-189">**Objective-C**:</span></span>

```objc
NSDictionary *newItem = @{@"id": @"custom-id", @"text": @"my new item", @"complete" : @NO};
[table insert:newItem completion:^(NSDictionary *result, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item: %@", [result objectForKey:@"text"]);
    }
}];
```

<span data-ttu-id="91528-190">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="91528-190">**Swift**:</span></span>

```swift
let newItem = ["id": "custom-id", "text": "my new item", "complete": false]
table.insert(newItem) { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let item = result {
        print("Todo Item: ", item["text"])
    }
}
```

## <a name="modifying"></a><span data-ttu-id="91528-191">How to: Modify Data</span><span class="sxs-lookup"><span data-stu-id="91528-191">How to: Modify Data</span></span>

<span data-ttu-id="91528-192">To update an existing row, modify an item and call `update`:</span><span class="sxs-lookup"><span data-stu-id="91528-192">To update an existing row, modify an item and call `update`:</span></span>

<span data-ttu-id="91528-193">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="91528-193">**Objective-C**:</span></span>

```objc
NSMutableDictionary *newItem = [oldItem mutableCopy]; // oldItem is NSDictionary
[newItem setValue:@"Updated text" forKey:@"text"];
[table update:newItem completion:^(NSDictionary *result, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item: %@", [result objectForKey:@"text"]);
    }
}];
```

<span data-ttu-id="91528-194">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="91528-194">**Swift**:</span></span>

```swift
if let newItem = oldItem.mutableCopy() as? NSMutableDictionary {
    newItem["text"] = "Updated text"
    table2.update(newItem as [NSObject: AnyObject], completion: { (result, error) -> Void in
        if let err = error {
            print("ERROR ", err)
        } else if let item = result {
            print("Todo Item: ", item["text"])
        }
    })
}
```

<span data-ttu-id="91528-195">Alternatively, supply the row ID and the updated field:</span><span class="sxs-lookup"><span data-stu-id="91528-195">Alternatively, supply the row ID and the updated field:</span></span>

<span data-ttu-id="91528-196">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="91528-196">**Objective-C**:</span></span>

```objc
[table update:@{@"id":@"custom-id", @"text":"my EDITED item"} completion:^(NSDictionary *result, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item: %@", [result objectForKey:@"text"]);
    }
}];
```

<span data-ttu-id="91528-197">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="91528-197">**Swift**:</span></span>

```swift
table.update(["id": "custom-id", "text": "my EDITED item"]) { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let item = result {
        print("Todo Item: ", item["text"])
    }
}
```

<span data-ttu-id="91528-198">At minimum, the `id` attribute must be set when making updates.</span><span class="sxs-lookup"><span data-stu-id="91528-198">At minimum, the `id` attribute must be set when making updates.</span></span>

## <a name="deleting"></a><span data-ttu-id="91528-199">How to: Delete Data</span><span class="sxs-lookup"><span data-stu-id="91528-199">How to: Delete Data</span></span>

<span data-ttu-id="91528-200">To delete an item, invoke `delete` with the item:</span><span class="sxs-lookup"><span data-stu-id="91528-200">To delete an item, invoke `delete` with the item:</span></span>

<span data-ttu-id="91528-201">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="91528-201">**Objective-C**:</span></span>

```objc
[table delete:item completion:^(id itemId, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item ID: %@", itemId);
    }
}];
```

<span data-ttu-id="91528-202">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="91528-202">**Swift**:</span></span>

```swift
table.delete(newItem as [NSObject: AnyObject]) { (itemId, error) in
    if let err = error {
        print("ERROR ", err)
    } else {
        print("Todo Item ID: ", itemId)
    }
}
```

<span data-ttu-id="91528-203">Alternatively, delete by providing a row ID:</span><span class="sxs-lookup"><span data-stu-id="91528-203">Alternatively, delete by providing a row ID:</span></span>

<span data-ttu-id="91528-204">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="91528-204">**Objective-C**:</span></span>

```objc
[table deleteWithId:@"37BBF396-11F0-4B39-85C8-B319C729AF6D" completion:^(id itemId, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item ID: %@", itemId);
    }
}];
```

<span data-ttu-id="91528-205">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="91528-205">**Swift**:</span></span>

```swift
table.deleteWithId("37BBF396-11F0-4B39-85C8-B319C729AF6D") { (itemId, error) in
    if let err = error {
        print("ERROR ", err)
    } else {
        print("Todo Item ID: ", itemId)
    }
}
```

<span data-ttu-id="91528-206">At minimum, the `id` attribute must be set when making deletes.</span><span class="sxs-lookup"><span data-stu-id="91528-206">At minimum, the `id` attribute must be set when making deletes.</span></span>

## <a name="customapi"></a><span data-ttu-id="91528-207">How to: Call Custom API</span><span class="sxs-lookup"><span data-stu-id="91528-207">How to: Call Custom API</span></span>

<span data-ttu-id="91528-208">With a custom API, you can expose any backend functionality.</span><span class="sxs-lookup"><span data-stu-id="91528-208">With a custom API, you can expose any backend functionality.</span></span> <span data-ttu-id="91528-209">It doesn't have to map to a table operation.</span><span class="sxs-lookup"><span data-stu-id="91528-209">It doesn't have to map to a table operation.</span></span> <span data-ttu-id="91528-210">Not only do you gain more control over messaging, you can even read/set headers and change the response body format.</span><span class="sxs-lookup"><span data-stu-id="91528-210">Not only do you gain more control over messaging, you can even read/set headers and change the response body format.</span></span> <span data-ttu-id="91528-211">To learn how to create a custom API on the backend, read [Custom APIs](app-service-mobile-node-backend-how-to-use-server-sdk.md#work-easy-apis)</span><span class="sxs-lookup"><span data-stu-id="91528-211">To learn how to create a custom API on the backend, read [Custom APIs](app-service-mobile-node-backend-how-to-use-server-sdk.md#work-easy-apis)</span></span>

<span data-ttu-id="91528-212">To call a custom API, call `MSClient.invokeAPI`.</span><span class="sxs-lookup"><span data-stu-id="91528-212">To call a custom API, call `MSClient.invokeAPI`.</span></span> <span data-ttu-id="91528-213">The request and response content are treated as JSON.</span><span class="sxs-lookup"><span data-stu-id="91528-213">The request and response content are treated as JSON.</span></span> <span data-ttu-id="91528-214">To use other media types, [use the other overload of `invokeAPI`][5].</span><span class="sxs-lookup"><span data-stu-id="91528-214">To use other media types, [use the other overload of `invokeAPI`][5].</span></span>  <span data-ttu-id="91528-215">To make a `GET` request instead of a `POST` request, set parameter `HTTPMethod` to `"GET"` and parameter `body` to `nil` (since GET requests do not have message bodies.) If your custom API supports other HTTP verbs, change `HTTPMethod` appropriately.</span><span class="sxs-lookup"><span data-stu-id="91528-215">To make a `GET` request instead of a `POST` request, set parameter `HTTPMethod` to `"GET"` and parameter `body` to `nil` (since GET requests do not have message bodies.) If your custom API supports other HTTP verbs, change `HTTPMethod` appropriately.</span></span>

<span data-ttu-id="91528-216">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="91528-216">**Objective-C**:</span></span>

```objc
[self.client invokeAPI:@"sendEmail"
                  body:@{ @"contents": @"Hello world!" }
            HTTPMethod:@"POST"
            parameters:@{ @"to": @"bill@contoso.com", @"subject" : @"Hi!" }
               headers:nil
            completion: ^(NSData *result, NSHTTPURLResponse *response, NSError *error) {
                if(error) {
                    NSLog(@"ERROR %@", error);
                } else {
                    // Do something with result
                }
            }];
```

<span data-ttu-id="91528-217">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="91528-217">**Swift**:</span></span>

```swift
client.invokeAPI("sendEmail",
            body: [ "contents": "Hello World" ],
            HTTPMethod: "POST",
            parameters: [ "to": "bill@contoso.com", "subject" : "Hi!" ],
            headers: nil)
            {
                (result, response, error) -> Void in
                if let err = error {
                    print("ERROR ", err)
                } else if let res = result {
                          // Do something with result
                }
        }
```

## <a name="templates"></a><span data-ttu-id="91528-218">How to: Register push templates to send cross-platform notifications</span><span class="sxs-lookup"><span data-stu-id="91528-218">How to: Register push templates to send cross-platform notifications</span></span>

<span data-ttu-id="91528-219">To register templates, pass templates with your **client.push registerDeviceToken** method in your client app.</span><span class="sxs-lookup"><span data-stu-id="91528-219">To register templates, pass templates with your **client.push registerDeviceToken** method in your client app.</span></span>

<span data-ttu-id="91528-220">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="91528-220">**Objective-C**:</span></span>

```objc
[client.push registerDeviceToken:deviceToken template:iOSTemplate completion:^(NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    }
}];
```

<span data-ttu-id="91528-221">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="91528-221">**Swift**:</span></span>

```swift
client.push?.registerDeviceToken(NSData(), template: iOSTemplate, completion: { (error) in
    if let err = error {
        print("ERROR ", err)
    }
})
```

<span data-ttu-id="91528-222">Your templates are of type NSDictionary and can contain multiple templates in the following format:</span><span class="sxs-lookup"><span data-stu-id="91528-222">Your templates are of type NSDictionary and can contain multiple templates in the following format:</span></span>

<span data-ttu-id="91528-223">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="91528-223">**Objective-C**:</span></span>

```objc
NSDictionary *iOSTemplate = @{ @"templateName": @{ @"body": @{ @"aps": @{ @"alert": @"$(message)" } } } };
```

<span data-ttu-id="91528-224">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="91528-224">**Swift**:</span></span>

```swift
let iOSTemplate = ["templateName": ["body": ["aps": ["alert": "$(message)"]]]]
```

<span data-ttu-id="91528-225">All tags are stripped from the request for security.</span><span class="sxs-lookup"><span data-stu-id="91528-225">All tags are stripped from the request for security.</span></span>  <span data-ttu-id="91528-226">To add tags to installations or templates within installations, see [Work with the .NET backend server SDK for Azure Mobile Apps][4].</span><span class="sxs-lookup"><span data-stu-id="91528-226">To add tags to installations or templates within installations, see [Work with the .NET backend server SDK for Azure Mobile Apps][4].</span></span>  <span data-ttu-id="91528-227">To send notifications using these registered templates, work with [Notification Hubs APIs][3].</span><span class="sxs-lookup"><span data-stu-id="91528-227">To send notifications using these registered templates, work with [Notification Hubs APIs][3].</span></span>

## <a name="errors"></a><span data-ttu-id="91528-228">How to: Handle Errors</span><span class="sxs-lookup"><span data-stu-id="91528-228">How to: Handle Errors</span></span>

<span data-ttu-id="91528-229">When you call an Azure App Service mobile backend, the completion block contains an `NSError` parameter.</span><span class="sxs-lookup"><span data-stu-id="91528-229">When you call an Azure App Service mobile backend, the completion block contains an `NSError` parameter.</span></span> <span data-ttu-id="91528-230">When an error occurs, this parameter is non-nil.</span><span class="sxs-lookup"><span data-stu-id="91528-230">When an error occurs, this parameter is non-nil.</span></span> <span data-ttu-id="91528-231">In your code, you should check this parameter and handle the error as needed, as demonstrated in the preceding code snippets.</span><span class="sxs-lookup"><span data-stu-id="91528-231">In your code, you should check this parameter and handle the error as needed, as demonstrated in the preceding code snippets.</span></span>

<span data-ttu-id="91528-232">The file [`<WindowsAzureMobileServices/MSError.h>`][6] defines the constants `MSErrorResponseKey`, `MSErrorRequestKey`, and `MSErrorServerItemKey`.</span><span class="sxs-lookup"><span data-stu-id="91528-232">The file [`<WindowsAzureMobileServices/MSError.h>`][6] defines the constants `MSErrorResponseKey`, `MSErrorRequestKey`, and `MSErrorServerItemKey`.</span></span> <span data-ttu-id="91528-233">To get more data related to the error:</span><span class="sxs-lookup"><span data-stu-id="91528-233">To get more data related to the error:</span></span>

<span data-ttu-id="91528-234">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="91528-234">**Objective-C**:</span></span>

```objc
NSDictionary *serverItem = [error.userInfo objectForKey:MSErrorServerItemKey];
```

<span data-ttu-id="91528-235">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="91528-235">**Swift**:</span></span>

```swift
let serverItem = error.userInfo[MSErrorServerItemKey]
```

<span data-ttu-id="91528-236">In addition, the file defines constants for each error code:</span><span class="sxs-lookup"><span data-stu-id="91528-236">In addition, the file defines constants for each error code:</span></span>

<span data-ttu-id="91528-237">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="91528-237">**Objective-C**:</span></span>

```objc
if (error.code == MSErrorPreconditionFailed) {
```

<span data-ttu-id="91528-238">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="91528-238">**Swift**:</span></span>

```swift
if (error.code == MSErrorPreconditionFailed) {
```

## <a name="adal"></a><span data-ttu-id="91528-239">How to: Authenticate users with the Active Directory Authentication Library</span><span class="sxs-lookup"><span data-stu-id="91528-239">How to: Authenticate users with the Active Directory Authentication Library</span></span>

<span data-ttu-id="91528-240">You can use the Active Directory Authentication Library (ADAL) to sign users into your application using Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="91528-240">You can use the Active Directory Authentication Library (ADAL) to sign users into your application using Azure Active Directory.</span></span> <span data-ttu-id="91528-241">Client flow authentication using an identity provider SDK is preferable to using the `loginWithProvider:completion:` method.</span><span class="sxs-lookup"><span data-stu-id="91528-241">Client flow authentication using an identity provider SDK is preferable to using the `loginWithProvider:completion:` method.</span></span>  <span data-ttu-id="91528-242">Client flow authentication provides a more native UX feel and allows for additional customization.</span><span class="sxs-lookup"><span data-stu-id="91528-242">Client flow authentication provides a more native UX feel and allows for additional customization.</span></span>

1. <span data-ttu-id="91528-243">Configure your mobile app backend for AAD sign-in by following the [How to configure App Service for Active Directory login][7] tutorial.</span><span class="sxs-lookup"><span data-stu-id="91528-243">Configure your mobile app backend for AAD sign-in by following the [How to configure App Service for Active Directory login][7] tutorial.</span></span> <span data-ttu-id="91528-244">Make sure to complete the optional step of registering a native client application.</span><span class="sxs-lookup"><span data-stu-id="91528-244">Make sure to complete the optional step of registering a native client application.</span></span> <span data-ttu-id="91528-245">For iOS, we recommend that the redirect URI is of the form `<app-scheme>://<bundle-id>`.</span><span class="sxs-lookup"><span data-stu-id="91528-245">For iOS, we recommend that the redirect URI is of the form `<app-scheme>://<bundle-id>`.</span></span> <span data-ttu-id="91528-246">For more information, see the [ADAL iOS quickstart][8].</span><span class="sxs-lookup"><span data-stu-id="91528-246">For more information, see the [ADAL iOS quickstart][8].</span></span>
2. <span data-ttu-id="91528-247">Install ADAL using Cocoapods.</span><span class="sxs-lookup"><span data-stu-id="91528-247">Install ADAL using Cocoapods.</span></span> <span data-ttu-id="91528-248">Edit your Podfile to include the following definition, replacing **YOUR-PROJECT** with the name of your Xcode project:</span><span class="sxs-lookup"><span data-stu-id="91528-248">Edit your Podfile to include the following definition, replacing **YOUR-PROJECT** with the name of your Xcode project:</span></span>

        source 'https://github.com/CocoaPods/Specs.git'
        link_with ['YOUR-PROJECT']
        xcodeproj 'YOUR-PROJECT'

   <span data-ttu-id="91528-249">and the Pod:</span><span class="sxs-lookup"><span data-stu-id="91528-249">and the Pod:</span></span>

        pod 'ADALiOS'

3. <span data-ttu-id="91528-250">Using the Terminal, run `pod install` from the directory containing your project, and then open the generated Xcode workspace (not the project).</span><span class="sxs-lookup"><span data-stu-id="91528-250">Using the Terminal, run `pod install` from the directory containing your project, and then open the generated Xcode workspace (not the project).</span></span>
4. <span data-ttu-id="91528-251">Add the following code to your application, according to the language you are using.</span><span class="sxs-lookup"><span data-stu-id="91528-251">Add the following code to your application, according to the language you are using.</span></span> <span data-ttu-id="91528-252">In each, make these replacements:</span><span class="sxs-lookup"><span data-stu-id="91528-252">In each, make these replacements:</span></span>

   * <span data-ttu-id="91528-253">Replace **INSERT-AUTHORITY-HERE** with the name of the tenant in which you provisioned your application.</span><span class="sxs-lookup"><span data-stu-id="91528-253">Replace **INSERT-AUTHORITY-HERE** with the name of the tenant in which you provisioned your application.</span></span> <span data-ttu-id="91528-254">The format should be https://login.microsoftonline.com/contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="91528-254">The format should be https://login.microsoftonline.com/contoso.onmicrosoft.com.</span></span> <span data-ttu-id="91528-255">This value can be copied from the Domain tab in your Azure Active Directory in the [Azure portal].</span><span class="sxs-lookup"><span data-stu-id="91528-255">This value can be copied from the Domain tab in your Azure Active Directory in the [Azure portal].</span></span>
   * <span data-ttu-id="91528-256">Replace **INSERT-RESOURCE-ID-HERE** with the client ID for your mobile app backend.</span><span class="sxs-lookup"><span data-stu-id="91528-256">Replace **INSERT-RESOURCE-ID-HERE** with the client ID for your mobile app backend.</span></span> <span data-ttu-id="91528-257">You can obtain the client ID from the **Advanced** tab under **Azure Active Directory Settings** in the portal.</span><span class="sxs-lookup"><span data-stu-id="91528-257">You can obtain the client ID from the **Advanced** tab under **Azure Active Directory Settings** in the portal.</span></span>
   * <span data-ttu-id="91528-258">Replace **INSERT-CLIENT-ID-HERE** with the client ID you copied from the native client application.</span><span class="sxs-lookup"><span data-stu-id="91528-258">Replace **INSERT-CLIENT-ID-HERE** with the client ID you copied from the native client application.</span></span>
   * <span data-ttu-id="91528-259">Replace **INSERT-REDIRECT-URI-HERE** with your site's */.auth/login/done* endpoint, using the HTTPS scheme.</span><span class="sxs-lookup"><span data-stu-id="91528-259">Replace **INSERT-REDIRECT-URI-HERE** with your site's */.auth/login/done* endpoint, using the HTTPS scheme.</span></span> <span data-ttu-id="91528-260">This value should be similar to *https://contoso.azurewebsites.net/.auth/login/done*.</span><span class="sxs-lookup"><span data-stu-id="91528-260">This value should be similar to *https://contoso.azurewebsites.net/.auth/login/done*.</span></span>

<span data-ttu-id="91528-261">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="91528-261">**Objective-C**:</span></span>

```objc
#import <ADALiOS/ADAuthenticationContext.h>
#import <ADALiOS/ADAuthenticationSettings.h>
// ...
- (void) authenticate:(UIViewController*) parent
            completion:(void (^) (MSUser*, NSError*))completionBlock;
{
    NSString *authority = @"INSERT-AUTHORITY-HERE";
    NSString *resourceId = @"INSERT-RESOURCE-ID-HERE";
    NSString *clientId = @"INSERT-CLIENT-ID-HERE";
    NSURL *redirectUri = [[NSURL alloc]initWithString:@"INSERT-REDIRECT-URI-HERE"];
    ADAuthenticationError *error;
    ADAuthenticationContext *authContext = [ADAuthenticationContext authenticationContextWithAuthority:authority error:&error];
    authContext.parentController = parent;
    [ADAuthenticationSettings sharedInstance].enableFullScreen = YES;
    [authContext acquireTokenWithResource:resourceId
                                    clientId:clientId
                                redirectUri:redirectUri
                            completionBlock:^(ADAuthenticationResult *result) {
                                if (result.status != AD_SUCCEEDED)
                                {
                                    completionBlock(nil, result.error);;
                                }
                                else
                                {
                                    NSDictionary *payload = @{
                                                            @"access_token" : result.tokenCacheStoreItem.accessToken
                                                            };
                                    [client loginWithProvider:@"aad" token:payload completion:completionBlock];
                                }
                            }];
}
```

<span data-ttu-id="91528-262">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="91528-262">**Swift**:</span></span>

```swift
// add the following imports to your bridging header:
//        #import <ADALiOS/ADAuthenticationContext.h>
//        #import <ADALiOS/ADAuthenticationSettings.h>

func authenticate(parent: UIViewController, completion: (MSUser?, NSError?) -> Void) {
    let authority = "INSERT-AUTHORITY-HERE"
    let resourceId = "INSERT-RESOURCE-ID-HERE"
    let clientId = "INSERT-CLIENT-ID-HERE"
    let redirectUri = NSURL(string: "INSERT-REDIRECT-URI-HERE")
    var error: AutoreleasingUnsafeMutablePointer<ADAuthenticationError?> = nil
    let authContext = ADAuthenticationContext(authority: authority, error: error)
    authContext.parentController = parent
    ADAuthenticationSettings.sharedInstance().enableFullScreen = true
    authContext.acquireTokenWithResource(resourceId, clientId: clientId, redirectUri: redirectUri) { (result) in
            if result.status != AD_SUCCEEDED {
                completion(nil, result.error)
            }
            else {
                let payload: [String: String] = ["access_token": result.tokenCacheStoreItem.accessToken]
                client.loginWithProvider("aad", token: payload, completion: completion)
            }
        }
}
```

## <a name="facebook-sdk"></a><span data-ttu-id="91528-263">How to: Authenticate users with the Facebook SDK for iOS</span><span class="sxs-lookup"><span data-stu-id="91528-263">How to: Authenticate users with the Facebook SDK for iOS</span></span>

<span data-ttu-id="91528-264">You can use the Facebook SDK for iOS to sign users into your application using Facebook.</span><span class="sxs-lookup"><span data-stu-id="91528-264">You can use the Facebook SDK for iOS to sign users into your application using Facebook.</span></span>  <span data-ttu-id="91528-265">Using a client flow authentication is preferable to using the `loginWithProvider:completion:` method.</span><span class="sxs-lookup"><span data-stu-id="91528-265">Using a client flow authentication is preferable to using the `loginWithProvider:completion:` method.</span></span>  <span data-ttu-id="91528-266">The client flow authentication provides a more native UX feel and allows for additional customization.</span><span class="sxs-lookup"><span data-stu-id="91528-266">The client flow authentication provides a more native UX feel and allows for additional customization.</span></span>

1. <span data-ttu-id="91528-267">Configure your mobile app backend for Facebook sign-in by following the [How to configure App Service for Facebook login][9] tutorial.</span><span class="sxs-lookup"><span data-stu-id="91528-267">Configure your mobile app backend for Facebook sign-in by following the [How to configure App Service for Facebook login][9] tutorial.</span></span>
2. <span data-ttu-id="91528-268">Install the Facebook SDK for iOS by following the [Facebook SDK for iOS - Getting Started][10] documentation.</span><span class="sxs-lookup"><span data-stu-id="91528-268">Install the Facebook SDK for iOS by following the [Facebook SDK for iOS - Getting Started][10] documentation.</span></span> <span data-ttu-id="91528-269">Instead of creating an app, you can add the iOS platform to your existing registration.</span><span class="sxs-lookup"><span data-stu-id="91528-269">Instead of creating an app, you can add the iOS platform to your existing registration.</span></span>
3. <span data-ttu-id="91528-270">Facebook's documentation includes some Objective-C code in the App Delegate.</span><span class="sxs-lookup"><span data-stu-id="91528-270">Facebook's documentation includes some Objective-C code in the App Delegate.</span></span> <span data-ttu-id="91528-271">If you are using **Swift**, you can use the following translations for AppDelegate.swift:</span><span class="sxs-lookup"><span data-stu-id="91528-271">If you are using **Swift**, you can use the following translations for AppDelegate.swift:</span></span>

    ```swift
    // Add the following import to your bridging header:
    //        #import <FBSDKCoreKit/FBSDKCoreKit.h>

    func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject : AnyObject]?) -> Bool {
        FBSDKApplicationDelegate.sharedInstance().application(application, didFinishLaunchingWithOptions: launchOptions)
        // Add any custom logic here.
        return true
    }

    func application(application: UIApplication, openURL url: NSURL, sourceApplication: String?, annotation: AnyObject?) -> Bool {
        let handled = FBSDKApplicationDelegate.sharedInstance().application(application, openURL: url, sourceApplication: sourceApplication, annotation: annotation)
        // Add any custom logic here.
        return handled
    }
    ```
4. <span data-ttu-id="91528-272">In addition to adding `FBSDKCoreKit.framework` to your project, also add a reference to `FBSDKLoginKit.framework` in the same way.</span><span class="sxs-lookup"><span data-stu-id="91528-272">In addition to adding `FBSDKCoreKit.framework` to your project, also add a reference to `FBSDKLoginKit.framework` in the same way.</span></span>
5. <span data-ttu-id="91528-273">Add the following code to your application, according to the language you are using.</span><span class="sxs-lookup"><span data-stu-id="91528-273">Add the following code to your application, according to the language you are using.</span></span>

    <span data-ttu-id="91528-274">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="91528-274">**Objective-C**:</span></span>

    ```objc
    #import <FBSDKLoginKit/FBSDKLoginKit.h>
    #import <FBSDKCoreKit/FBSDKAccessToken.h>
    // ...
    - (void) authenticate:(UIViewController*) parent
                completion:(void (^) (MSUser*, NSError*)) completionBlock;
    {
        FBSDKLoginManager *loginManager = [[FBSDKLoginManager alloc] init];
        [loginManager
            logInWithReadPermissions: @[@"public_profile"]
            fromViewController:parent
            handler:^(FBSDKLoginManagerLoginResult *result, NSError *error) {
                if (error) {
                    completionBlock(nil, error);
                } else if (result.isCancelled) {
                    completionBlock(nil, error);
                } else {
                    NSDictionary *payload = @{
                                            @"access_token":result.token.tokenString
                                            };
                    [client loginWithProvider:@"facebook" token:payload completion:completionBlock];
                }
            }];
    }
    ```

    <span data-ttu-id="91528-275">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="91528-275">**Swift**:</span></span>

    ```swift
    // Add the following imports to your bridging header:
    //        #import <FBSDKLoginKit/FBSDKLoginKit.h>
    //        #import <FBSDKCoreKit/FBSDKAccessToken.h>

    func authenticate(parent: UIViewController, completion: (MSUser?, NSError?) -> Void) {
        let loginManager = FBSDKLoginManager()
        loginManager.logInWithReadPermissions(["public_profile"], fromViewController: parent) { (result, error) in
            if (error != nil) {
                completion(nil, error)
            }
            else if result.isCancelled {
                completion(nil, error)
            }
            else {
                let payload: [String: String] = ["access_token": result.token.tokenString]
                client.loginWithProvider("facebook", token: payload, completion: completion)
            }
        }
    }
    ```

## <a name="twitter-fabric"></a><span data-ttu-id="91528-276">How to: Authenticate users with Twitter Fabric for iOS</span><span class="sxs-lookup"><span data-stu-id="91528-276">How to: Authenticate users with Twitter Fabric for iOS</span></span>

<span data-ttu-id="91528-277">You can use Fabric for iOS to sign users into your application using Twitter.</span><span class="sxs-lookup"><span data-stu-id="91528-277">You can use Fabric for iOS to sign users into your application using Twitter.</span></span> <span data-ttu-id="91528-278">Client Flow authentication is preferable to using the `loginWithProvider:completion:` method, as it provides a more native UX feel and allows for additional customization.</span><span class="sxs-lookup"><span data-stu-id="91528-278">Client Flow authentication is preferable to using the `loginWithProvider:completion:` method, as it provides a more native UX feel and allows for additional customization.</span></span>

1. <span data-ttu-id="91528-279">Configure your mobile app backend for Twitter sign-in by following the [How to configure App Service for Twitter login](../app-service/app-service-mobile-how-to-configure-twitter-authentication.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="91528-279">Configure your mobile app backend for Twitter sign-in by following the [How to configure App Service for Twitter login](../app-service/app-service-mobile-how-to-configure-twitter-authentication.md) tutorial.</span></span>
2. <span data-ttu-id="91528-280">Add Fabric to your project by following the [Fabric for iOS - Getting Started] documentation and setting up TwitterKit.</span><span class="sxs-lookup"><span data-stu-id="91528-280">Add Fabric to your project by following the [Fabric for iOS - Getting Started] documentation and setting up TwitterKit.</span></span>

   > [!NOTE]
   > <span data-ttu-id="91528-281">By default, Fabric creates a Twitter application for you.</span><span class="sxs-lookup"><span data-stu-id="91528-281">By default, Fabric creates a Twitter application for you.</span></span> <span data-ttu-id="91528-282">You can avoid creating an application by registering the Consumer Key and Consumer Secret you created earlier using the following code snippets.</span><span class="sxs-lookup"><span data-stu-id="91528-282">You can avoid creating an application by registering the Consumer Key and Consumer Secret you created earlier using the following code snippets.</span></span>    <span data-ttu-id="91528-283">Alternatively, you can replace the Consumer Key and Consumer Secret values that you provide to App Service with the values you see in the [Fabric Dashboard].</span><span class="sxs-lookup"><span data-stu-id="91528-283">Alternatively, you can replace the Consumer Key and Consumer Secret values that you provide to App Service with the values you see in the [Fabric Dashboard].</span></span> <span data-ttu-id="91528-284">If you choose this option, be sure to set the callback URL to a placeholder value, such as `https://<yoursitename>.azurewebsites.net/.auth/login/twitter/callback`.</span><span class="sxs-lookup"><span data-stu-id="91528-284">If you choose this option, be sure to set the callback URL to a placeholder value, such as `https://<yoursitename>.azurewebsites.net/.auth/login/twitter/callback`.</span></span>

    <span data-ttu-id="91528-285">If you choose to use the secrets you created earlier, add the following code to your App Delegate:</span><span class="sxs-lookup"><span data-stu-id="91528-285">If you choose to use the secrets you created earlier, add the following code to your App Delegate:</span></span>

    <span data-ttu-id="91528-286">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="91528-286">**Objective-C**:</span></span>

    ```objc
    #import <Fabric/Fabric.h>
    #import <TwitterKit/TwitterKit.h>
    // ...
    - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
    {
        [[Twitter sharedInstance] startWithConsumerKey:@"your_key" consumerSecret:@"your_secret"];
        [Fabric with:@[[Twitter class]]];
        // Add any custom logic here.
        return YES;
    }
    ```

    <span data-ttu-id="91528-287">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="91528-287">**Swift**:</span></span>

    ```swift
    import Fabric
    import TwitterKit
    // ...
    func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject : AnyObject]?) -> Bool {
        Twitter.sharedInstance().startWithConsumerKey("your_key", consumerSecret: "your_secret")
        Fabric.with([Twitter.self])
        // Add any custom logic here.
        return true
    }
    ```

3. <span data-ttu-id="91528-288">Add the following code to your application, according to the language you are using.</span><span class="sxs-lookup"><span data-stu-id="91528-288">Add the following code to your application, according to the language you are using.</span></span>

    <span data-ttu-id="91528-289">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="91528-289">**Objective-C**:</span></span>

    ```objc
    #import <TwitterKit/TwitterKit.h>
    // ...
    - (void)authenticate:(UIViewController*)parent completion:(void (^) (MSUser*, NSError*))completionBlock
    {
        [[Twitter sharedInstance] logInWithCompletion:^(TWTRSession *session, NSError *error) {
            if (session) {
                NSDictionary *payload = @{
                                            @"access_token":session.authToken,
                                            @"access_token_secret":session.authTokenSecret
                                        };
                [client loginWithProvider:@"twitter" token:payload completion:completionBlock];
            } else {
                completionBlock(nil, error);
            }
        }];
    }
    ```

    <span data-ttu-id="91528-290">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="91528-290">**Swift**:</span></span>

    ```swift
    import TwitterKit
    // ...
    func authenticate(parent: UIViewController, completion: (MSUser?, NSError?) -> Void) {
        let client = self.table!.client
        Twitter.sharedInstance().logInWithCompletion { session, error in
            if (session != nil) {
                let payload: [String: String] = ["access_token": session!.authToken, "access_token_secret": session!.authTokenSecret]
                client.loginWithProvider("twitter", token: payload, completion: completion)
            } else {
                completion(nil, error)
            }
        }
    }
    ```

## <a name="google-sdk"></a><span data-ttu-id="91528-291">How to: Authenticate users with the Google Sign-In SDK for iOS</span><span class="sxs-lookup"><span data-stu-id="91528-291">How to: Authenticate users with the Google Sign-In SDK for iOS</span></span>

<span data-ttu-id="91528-292">You can use the Google Sign-In SDK for iOS to sign users into your application using a Google account.</span><span class="sxs-lookup"><span data-stu-id="91528-292">You can use the Google Sign-In SDK for iOS to sign users into your application using a Google account.</span></span>  <span data-ttu-id="91528-293">Google recently announced changes to their OAuth security policies.</span><span class="sxs-lookup"><span data-stu-id="91528-293">Google recently announced changes to their OAuth security policies.</span></span>  <span data-ttu-id="91528-294">These policy changes will require the use of the Google SDK in the future.</span><span class="sxs-lookup"><span data-stu-id="91528-294">These policy changes will require the use of the Google SDK in the future.</span></span>

1. <span data-ttu-id="91528-295">Configure your mobile app backend for Google sign-in by following the [How to configure App Service for Google login](../app-service/app-service-mobile-how-to-configure-google-authentication.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="91528-295">Configure your mobile app backend for Google sign-in by following the [How to configure App Service for Google login](../app-service/app-service-mobile-how-to-configure-google-authentication.md) tutorial.</span></span>
2. <span data-ttu-id="91528-296">Install the Google SDK for iOS by following the [Google Sign-In for iOS - Start integrating](https://developers.google.com/identity/sign-in/ios/start-integrating) documentation.</span><span class="sxs-lookup"><span data-stu-id="91528-296">Install the Google SDK for iOS by following the [Google Sign-In for iOS - Start integrating](https://developers.google.com/identity/sign-in/ios/start-integrating) documentation.</span></span> <span data-ttu-id="91528-297">You may skip the "Authenticate with a Backend Server" section.</span><span class="sxs-lookup"><span data-stu-id="91528-297">You may skip the "Authenticate with a Backend Server" section.</span></span>
3. <span data-ttu-id="91528-298">Add the following to your delegate's `signIn:didSignInForUser:withError:` method, according to the language you are using.</span><span class="sxs-lookup"><span data-stu-id="91528-298">Add the following to your delegate's `signIn:didSignInForUser:withError:` method, according to the language you are using.</span></span>

    <span data-ttu-id="91528-299">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="91528-299">**Objective-C**:</span></span>
    ```objc
    NSDictionary *payload = @{
                                @"id_token":user.authentication.idToken,
                                @"authorization_code":user.serverAuthCode
                                };

    [client loginWithProvider:@"google" token:payload completion:^(MSUser *user, NSError *error) {
        // ...
    }];
    ```

    <span data-ttu-id="91528-300">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="91528-300">**Swift**:</span></span>

    ```swift
    let payload: [String: String] = ["id_token": user.authentication.idToken, "authorization_code": user.serverAuthCode]
    client.loginWithProvider("google", token: payload) { (user, error) in
        // ...
    }
    ```

4. <span data-ttu-id="91528-301">Make sure you also add the following to `application:didFinishLaunchingWithOptions:` in your app delegate, replacing "SERVER_CLIENT_ID" with the same ID that you used to configure App Service in step 1.</span><span class="sxs-lookup"><span data-stu-id="91528-301">Make sure you also add the following to `application:didFinishLaunchingWithOptions:` in your app delegate, replacing "SERVER_CLIENT_ID" with the same ID that you used to configure App Service in step 1.</span></span>

    <span data-ttu-id="91528-302">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="91528-302">**Objective-C**:</span></span>

    ```objc
    [GIDSignIn sharedInstance].serverClientID = @"SERVER_CLIENT_ID";
    ```

     <span data-ttu-id="91528-303">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="91528-303">**Swift**:</span></span>

    ```swift
    GIDSignIn.sharedInstance().serverClientID = "SERVER_CLIENT_ID"
    ```

5. <span data-ttu-id="91528-304">Add the following code to your application in a UIViewController that implements the `GIDSignInUIDelegate` protocol, according to the language you are using.</span><span class="sxs-lookup"><span data-stu-id="91528-304">Add the following code to your application in a UIViewController that implements the `GIDSignInUIDelegate` protocol, according to the language you are using.</span></span>  <span data-ttu-id="91528-305">You are signed out before being signed in again, and although you don't need to enter your credentials again, you see a consent dialog.</span><span class="sxs-lookup"><span data-stu-id="91528-305">You are signed out before being signed in again, and although you don't need to enter your credentials again, you see a consent dialog.</span></span>  <span data-ttu-id="91528-306">Only call this method when the session token has expired.</span><span class="sxs-lookup"><span data-stu-id="91528-306">Only call this method when the session token has expired.</span></span>

   <span data-ttu-id="91528-307">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="91528-307">**Objective-C**:</span></span>

    ```objc
    #import <Google/SignIn.h>
    // ...
    - (void)authenticate
    {
            [GIDSignIn sharedInstance].uiDelegate = self;
            [[GIDSignIn sharedInstance] signOut];
            [[GIDSignIn sharedInstance] signIn];
    }
    ```

   <span data-ttu-id="91528-308">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="91528-308">**Swift**:</span></span>

    ```swift
    // ...
    func authenticate() {
        GIDSignIn.sharedInstance().uiDelegate = self
        GIDSignIn.sharedInstance().signOut()
        GIDSignIn.sharedInstance().signIn()
    }
    ```

<!-- Anchors. -->

[What is Mobile Services]: #what-is
[Concepts]: #concepts
[Setup and Prerequisites]: #Setup
[How to: Create the Mobile Services client]: #create-client
[How to: Create a table reference]: #table-reference
[How to: Query data from a mobile service]: #querying
[Filter returned data]: #filtering
[Sort returned data]: #sorting
[Return data in pages]: #paging
[Select specific columns]: #selecting
[How to: Bind data to the user interface]: #binding
[How to: Insert data into a mobile service]: #inserting
[How to: Modify data in a mobile service]: #modifying
[How to: Authenticate users]: #authentication
[Cache authentication tokens]: #caching-tokens
[How to: Upload images and large files]: #blobs
[How to: Handle errors]: #errors
[How to: Design unit tests]: #unit-testing
[How to: Customize the client]: #customizing
[Customize request headers]: #custom-headers
[Customize data type serialization]: #custom-serialization
[Next Steps]: #next-steps
[How to: Use MSQuery]: #query-object

<!-- Images. -->

<!-- URLs. -->
[Azure Mobile Apps Quick Start]: app-service-mobile-ios-get-started.md

[Add Mobile Services to Existing App]: /develop/mobile/tutorials/get-started-data
[Get started with Mobile Services]: /develop/mobile/tutorials/get-started-ios
[Validate and modify data in Mobile Services by using server scripts]: /develop/mobile/tutorials/validate-modify-and-augment-data-ios
[Mobile Services SDK]: https://go.microsoft.com/fwLink/p/?LinkID=266533
[Authentication]: /develop/mobile/tutorials/get-started-with-users-ios
[iOS SDK]: https://developer.apple.com/xcode
[Azure portal]: https://portal.azure.com/
[Handling Expired Tokens]: http://go.microsoft.com/fwlink/p/?LinkId=301955
[Live Connect SDK]: http://go.microsoft.com/fwlink/p/?LinkId=301960
[Permissions]: http://msdn.microsoft.com/library/windowsazure/jj193161.aspx
[Service-side Authorization]: mobile-services-javascript-backend-service-side-authorization.md
[Use scripts to authorize users]: /develop/mobile/tutorials/authorize-users-in-scripts-ios
[Dynamic Schema]: http://go.microsoft.com/fwlink/p/?LinkId=296271
[How to: access custom parameters]: /develop/mobile/how-to-guides/work-with-server-scripts#access-headers
[Create a table]: http://msdn.microsoft.com/library/windowsazure/jj193162.aspx
[NSDictionary object]: http://go.microsoft.com/fwlink/p/?LinkId=301965
[ASCII control codes C0 and C1]: http://en.wikipedia.org/wiki/Data_link_escape_character#C1_set
[CLI to manage Mobile Services tables]: /cli/azure/get-started-with-az-cli2
[Conflict-Handler]: mobile-services-ios-handling-conflicts-offline-data.md#add-conflict-handling

[Fabric Dashboard]: https://www.fabric.io/home
[Fabric for iOS - Getting Started]: https://docs.fabric.io/ios/fabric/getting-started.html
[1]: https://github.com/Azure/azure-mobile-apps-ios-client/blob/master/README.md#ios-client-sdk
[2]: http://azure.github.io/azure-mobile-apps-ios-client/
[3]: https://msdn.microsoft.com/library/azure/dn495101.aspx
[4]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#tags
[5]: http://azure.github.io/azure-mobile-services/iOS/v3/Classes/MSClient.html#//api/name/invokeAPI:data:HTTPMethod:parameters:headers:completion:
[6]: https://github.com/Azure/azure-mobile-services/blob/master/sdk/iOS/src/MSError.h
[7]: ../app-service/app-service-mobile-how-to-configure-active-directory-authentication.md
[8]:../active-directory/develop/quickstart-v1-ios.md
[9]: ../app-service/app-service-mobile-how-to-configure-facebook-authentication.md
[10]: https://developers.facebook.com/docs/ios/getting-started
