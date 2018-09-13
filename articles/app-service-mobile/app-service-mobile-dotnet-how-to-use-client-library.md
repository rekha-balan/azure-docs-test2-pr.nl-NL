---
title: Working with the App Service Mobile Apps managed client library (Windows | Microsoft Docs
description: Learn how to use a .NET client for Azure App Service Mobile Apps with Windows and Xamarin apps.
services: app-service\mobile
documentationcenter: ''
author: adrianhall
manager: adrianha
editor: ''
ms.assetid: 0280785c-e027-4e0d-aaf2-6f155e5a6197
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 01/04/2017
ms.author: adrianha
ms.openlocfilehash: a1c53059b51680ef126f0d5ea636adff65dd28dd
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549416"
---
# <a name="how-to-use-the-managed-client-for-azure-mobile-apps"></a><span data-ttu-id="3df5c-103">How to use the managed client for Azure Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="3df5c-103">How to use the managed client for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

## <a name="overview"></a><span data-ttu-id="3df5c-104">Overview</span><span class="sxs-lookup"><span data-stu-id="3df5c-104">Overview</span></span>
<span data-ttu-id="3df5c-105">This guide shows you how to perform common scenarios using the managed client library for Azure App Service Mobile Apps for Windows and Xamarin apps.</span><span class="sxs-lookup"><span data-stu-id="3df5c-105">This guide shows you how to perform common scenarios using the managed client library for Azure App Service Mobile Apps for Windows and Xamarin apps.</span></span> <span data-ttu-id="3df5c-106">If you are new to Mobile Apps, you should consider first completing the [Azure Mobile Apps quickstart][1] tutorial.</span><span class="sxs-lookup"><span data-stu-id="3df5c-106">If you are new to Mobile Apps, you should consider first completing the [Azure Mobile Apps quickstart][1] tutorial.</span></span> <span data-ttu-id="3df5c-107">In this guide, we focus on the client-side managed SDK.</span><span class="sxs-lookup"><span data-stu-id="3df5c-107">In this guide, we focus on the client-side managed SDK.</span></span> <span data-ttu-id="3df5c-108">To learn more about the server-side SDKs for Mobile Apps, see the documentation for the [.NET Server SDK][2] or the [Node.js Server SDK][3].</span><span class="sxs-lookup"><span data-stu-id="3df5c-108">To learn more about the server-side SDKs for Mobile Apps, see the documentation for the [.NET Server SDK][2] or the [Node.js Server SDK][3].</span></span>

## <a name="reference-documentation"></a><span data-ttu-id="3df5c-109">Reference documentation</span><span class="sxs-lookup"><span data-stu-id="3df5c-109">Reference documentation</span></span>
<span data-ttu-id="3df5c-110">The reference documentation for the client SDK is located here: [Azure Mobile Apps .NET client reference][4].</span><span class="sxs-lookup"><span data-stu-id="3df5c-110">The reference documentation for the client SDK is located here: [Azure Mobile Apps .NET client reference][4].</span></span>
<span data-ttu-id="3df5c-111">You can also find several client samples in the [Azure-Samples GitHub repository][5].</span><span class="sxs-lookup"><span data-stu-id="3df5c-111">You can also find several client samples in the [Azure-Samples GitHub repository][5].</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="3df5c-112">Supported Platforms</span><span class="sxs-lookup"><span data-stu-id="3df5c-112">Supported Platforms</span></span>
<span data-ttu-id="3df5c-113">The .NET Platform supports the following platforms:</span><span class="sxs-lookup"><span data-stu-id="3df5c-113">The .NET Platform supports the following platforms:</span></span>

* <span data-ttu-id="3df5c-114">Xamarin Android releases for API 19 through 24 (KitKat through Nougat)</span><span class="sxs-lookup"><span data-stu-id="3df5c-114">Xamarin Android releases for API 19 through 24 (KitKat through Nougat)</span></span>
* <span data-ttu-id="3df5c-115">Xamarin iOS releases for iOS versions 8.0 and later</span><span class="sxs-lookup"><span data-stu-id="3df5c-115">Xamarin iOS releases for iOS versions 8.0 and later</span></span>
* <span data-ttu-id="3df5c-116">Universal Windows Platform</span><span class="sxs-lookup"><span data-stu-id="3df5c-116">Universal Windows Platform</span></span>
* <span data-ttu-id="3df5c-117">Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="3df5c-117">Windows Phone 8.1</span></span>
* <span data-ttu-id="3df5c-118">Windows Phone 8.0 except for Silverlight applications</span><span class="sxs-lookup"><span data-stu-id="3df5c-118">Windows Phone 8.0 except for Silverlight applications</span></span>

<span data-ttu-id="3df5c-119">The "server-flow" authentication uses a WebView for the presented UI.</span><span class="sxs-lookup"><span data-stu-id="3df5c-119">The "server-flow" authentication uses a WebView for the presented UI.</span></span>  <span data-ttu-id="3df5c-120">If the device is not able to present a WebView UI, then other methods of authentication are needed.</span><span class="sxs-lookup"><span data-stu-id="3df5c-120">If the device is not able to present a WebView UI, then other methods of authentication are needed.</span></span>  <span data-ttu-id="3df5c-121">This SDK is thus not suitable for Watch-type or similarly restricted devices.</span><span class="sxs-lookup"><span data-stu-id="3df5c-121">This SDK is thus not suitable for Watch-type or similarly restricted devices.</span></span>

## <a name="setup"></a><span data-ttu-id="3df5c-122">Setup and Prerequisites</span><span class="sxs-lookup"><span data-stu-id="3df5c-122">Setup and Prerequisites</span></span>
<span data-ttu-id="3df5c-123">We assume that you have already created and published your Mobile App backend project, which includes at least one table.</span><span class="sxs-lookup"><span data-stu-id="3df5c-123">We assume that you have already created and published your Mobile App backend project, which includes at least one table.</span></span>  <span data-ttu-id="3df5c-124">In the code used in this topic, the table is named `TodoItem` and it has the following columns: `Id`, `Text`, and `Complete`.</span><span class="sxs-lookup"><span data-stu-id="3df5c-124">In the code used in this topic, the table is named `TodoItem` and it has the following columns: `Id`, `Text`, and `Complete`.</span></span> <span data-ttu-id="3df5c-125">This table is the same table created when you complete the [Azure Mobile Apps quickstart][1].</span><span class="sxs-lookup"><span data-stu-id="3df5c-125">This table is the same table created when you complete the [Azure Mobile Apps quickstart][1].</span></span>

<span data-ttu-id="3df5c-126">The corresponding typed client-side type in C# is the following class:</span><span class="sxs-lookup"><span data-stu-id="3df5c-126">The corresponding typed client-side type in C# is the following class:</span></span>

```
public class TodoItem
{
    public string Id { get; set; }

    [JsonProperty(PropertyName = "text")]
    public string Text { get; set; }

    [JsonProperty(PropertyName = "complete")]
    public bool Complete { get; set; }
}
```

<span data-ttu-id="3df5c-127">The [JsonPropertyAttribute][6] is used to define the *PropertyName* mapping between the client field and the table field.</span><span class="sxs-lookup"><span data-stu-id="3df5c-127">The [JsonPropertyAttribute][6] is used to define the *PropertyName* mapping between the client field and the table field.</span></span>

<span data-ttu-id="3df5c-128">To learn how to create tables in your Mobile Apps backend, see the [.NET Server SDK topic][7] or the [Node.js Server SDK topic][8].</span><span class="sxs-lookup"><span data-stu-id="3df5c-128">To learn how to create tables in your Mobile Apps backend, see the [.NET Server SDK topic][7] or the [Node.js Server SDK topic][8].</span></span> <span data-ttu-id="3df5c-129">If you created your Mobile App backend in the Azure portal using the QuickStart, you can also use the **Easy tables** setting in the [Azure portal].</span><span class="sxs-lookup"><span data-stu-id="3df5c-129">If you created your Mobile App backend in the Azure portal using the QuickStart, you can also use the **Easy tables** setting in the [Azure portal].</span></span>

### <a name="how-to-install-the-managed-client-sdk-package"></a><span data-ttu-id="3df5c-130">How to: Install the managed client SDK package</span><span class="sxs-lookup"><span data-stu-id="3df5c-130">How to: Install the managed client SDK package</span></span>
<span data-ttu-id="3df5c-131">Use one of the following methods to install the managed client SDK package for Mobile Apps from [NuGet][9]:</span><span class="sxs-lookup"><span data-stu-id="3df5c-131">Use one of the following methods to install the managed client SDK package for Mobile Apps from [NuGet][9]:</span></span>

* <span data-ttu-id="3df5c-132">**Visual Studio** Right-click your project, click **Manage NuGet Packages**, search for the `Microsoft.Azure.Mobile.Client` package, then click **Install**.</span><span class="sxs-lookup"><span data-stu-id="3df5c-132">**Visual Studio** Right-click your project, click **Manage NuGet Packages**, search for the `Microsoft.Azure.Mobile.Client` package, then click **Install**.</span></span>
* <span data-ttu-id="3df5c-133">**Xamarin Studio** Right-click your project, click **Add** > **Add NuGet Packages**, search for the `Microsoft.Azure.Mobile.Client `package, and then click **Add Package**.</span><span class="sxs-lookup"><span data-stu-id="3df5c-133">**Xamarin Studio** Right-click your project, click **Add** > **Add NuGet Packages**, search for the `Microsoft.Azure.Mobile.Client `package, and then click **Add Package**.</span></span>

<span data-ttu-id="3df5c-134">In your main activity file, remember to add the following **using** statement:</span><span class="sxs-lookup"><span data-stu-id="3df5c-134">In your main activity file, remember to add the following **using** statement:</span></span>

```
using Microsoft.WindowsAzure.MobileServices;
```

### <a name="symbolsource"></a><span data-ttu-id="3df5c-135">How to: Work with debug symbols in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3df5c-135">How to: Work with debug symbols in Visual Studio</span></span>
<span data-ttu-id="3df5c-136">The symbols for the Microsoft.Azure.Mobile namespace are available on [SymbolSource][10].</span><span class="sxs-lookup"><span data-stu-id="3df5c-136">The symbols for the Microsoft.Azure.Mobile namespace are available on [SymbolSource][10].</span></span>  <span data-ttu-id="3df5c-137">Refer to the [SymbolSource instructions][11] to integrate SymbolSource with Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3df5c-137">Refer to the [SymbolSource instructions][11] to integrate SymbolSource with Visual Studio.</span></span>

## <a name="create-client"></a><span data-ttu-id="3df5c-138">Create the Mobile Apps client</span><span class="sxs-lookup"><span data-stu-id="3df5c-138">Create the Mobile Apps client</span></span>
<span data-ttu-id="3df5c-139">The following code creates the [MobileServiceClient][12] object that is used to access your Mobile App backend.</span><span class="sxs-lookup"><span data-stu-id="3df5c-139">The following code creates the [MobileServiceClient][12] object that is used to access your Mobile App backend.</span></span>

```
var client = new MobileServiceClient("MOBILE_APP_URL");
```

<span data-ttu-id="3df5c-140">In the preceding code, replace `MOBILE_APP_URL` with the URL of the Mobile App backend, which is found in the blade for your Mobile App backend in the [Azure portal].</span><span class="sxs-lookup"><span data-stu-id="3df5c-140">In the preceding code, replace `MOBILE_APP_URL` with the URL of the Mobile App backend, which is found in the blade for your Mobile App backend in the [Azure portal].</span></span> <span data-ttu-id="3df5c-141">The MobileServiceClient object should be a singleton.</span><span class="sxs-lookup"><span data-stu-id="3df5c-141">The MobileServiceClient object should be a singleton.</span></span>

## <a name="work-with-tables"></a><span data-ttu-id="3df5c-142">Work with Tables</span><span class="sxs-lookup"><span data-stu-id="3df5c-142">Work with Tables</span></span>
<span data-ttu-id="3df5c-143">The following section details how to search and retrieve records and modify the data within the table.</span><span class="sxs-lookup"><span data-stu-id="3df5c-143">The following section details how to search and retrieve records and modify the data within the table.</span></span>  <span data-ttu-id="3df5c-144">The following topics are covered:</span><span class="sxs-lookup"><span data-stu-id="3df5c-144">The following topics are covered:</span></span>

* [<span data-ttu-id="3df5c-145">Create a table reference</span><span class="sxs-lookup"><span data-stu-id="3df5c-145">Create a table reference</span></span>](#instantiating)
* [<span data-ttu-id="3df5c-146">Query data</span><span class="sxs-lookup"><span data-stu-id="3df5c-146">Query data</span></span>](#querying)
* [<span data-ttu-id="3df5c-147">Filter returned data</span><span class="sxs-lookup"><span data-stu-id="3df5c-147">Filter returned data</span></span>](#filtering)
* [<span data-ttu-id="3df5c-148">Sort returned data</span><span class="sxs-lookup"><span data-stu-id="3df5c-148">Sort returned data</span></span>](#sorting)
* [<span data-ttu-id="3df5c-149">Return data in pages</span><span class="sxs-lookup"><span data-stu-id="3df5c-149">Return data in pages</span></span>](#paging)
* [<span data-ttu-id="3df5c-150">Select specific columns</span><span class="sxs-lookup"><span data-stu-id="3df5c-150">Select specific columns</span></span>](#selecting)
* [<span data-ttu-id="3df5c-151">Look up a record by Id</span><span class="sxs-lookup"><span data-stu-id="3df5c-151">Look up a record by Id</span></span>](#lookingup)
* [<span data-ttu-id="3df5c-152">Dealing with untyped queries</span><span class="sxs-lookup"><span data-stu-id="3df5c-152">Dealing with untyped queries</span></span>](#untypedqueries)
* [<span data-ttu-id="3df5c-153">Inserting data</span><span class="sxs-lookup"><span data-stu-id="3df5c-153">Inserting data</span></span>](#inserting)
* [<span data-ttu-id="3df5c-154">Updating data</span><span class="sxs-lookup"><span data-stu-id="3df5c-154">Updating data</span></span>](#updating)
* [<span data-ttu-id="3df5c-155">Deleting data</span><span class="sxs-lookup"><span data-stu-id="3df5c-155">Deleting data</span></span>](#deleting)
* [<span data-ttu-id="3df5c-156">Conflict Resolution and Optimistic Concurrency</span><span class="sxs-lookup"><span data-stu-id="3df5c-156">Conflict Resolution and Optimistic Concurrency</span></span>](#optimisticconcurrency)
* [<span data-ttu-id="3df5c-157">Binding to a Windows User Interface</span><span class="sxs-lookup"><span data-stu-id="3df5c-157">Binding to a Windows User Interface</span></span>](#binding)
* [<span data-ttu-id="3df5c-158">Changing the Page Size</span><span class="sxs-lookup"><span data-stu-id="3df5c-158">Changing the Page Size</span></span>](#pagesize)

### <a name="instantiating"></a><span data-ttu-id="3df5c-159">How to: Create a table reference</span><span class="sxs-lookup"><span data-stu-id="3df5c-159">How to: Create a table reference</span></span>
<span data-ttu-id="3df5c-160">All the code that accesses or modifies data in a backend table calls functions on the `MobileServiceTable` object.</span><span class="sxs-lookup"><span data-stu-id="3df5c-160">All the code that accesses or modifies data in a backend table calls functions on the `MobileServiceTable` object.</span></span> <span data-ttu-id="3df5c-161">Obtain a reference to the table by calling the [GetTable] method, as follows:</span><span class="sxs-lookup"><span data-stu-id="3df5c-161">Obtain a reference to the table by calling the [GetTable] method, as follows:</span></span>

```
IMobileServiceTable<TodoItem> todoTable = client.GetTable<TodoItem>();
```

<span data-ttu-id="3df5c-162">The returned object uses the typed serialization model.</span><span class="sxs-lookup"><span data-stu-id="3df5c-162">The returned object uses the typed serialization model.</span></span> <span data-ttu-id="3df5c-163">An untyped serialization model is also supported.</span><span class="sxs-lookup"><span data-stu-id="3df5c-163">An untyped serialization model is also supported.</span></span> <span data-ttu-id="3df5c-164">The following example [creates a reference to an untyped table]:</span><span class="sxs-lookup"><span data-stu-id="3df5c-164">The following example [creates a reference to an untyped table]:</span></span>

```
// Get an untyped table reference
IMobileServiceTable untypedTodoTable = client.GetTable("TodoItem");
```

<span data-ttu-id="3df5c-165">In untyped queries, you must specify the underlying OData query string.</span><span class="sxs-lookup"><span data-stu-id="3df5c-165">In untyped queries, you must specify the underlying OData query string.</span></span>

### <a name="querying"></a><span data-ttu-id="3df5c-166">How to: Query data from your Mobile App</span><span class="sxs-lookup"><span data-stu-id="3df5c-166">How to: Query data from your Mobile App</span></span>
<span data-ttu-id="3df5c-167">This section describes how to issue queries to the Mobile App backend, which includes the following functionality:</span><span class="sxs-lookup"><span data-stu-id="3df5c-167">This section describes how to issue queries to the Mobile App backend, which includes the following functionality:</span></span>

* [<span data-ttu-id="3df5c-168">Filter returned data</span><span class="sxs-lookup"><span data-stu-id="3df5c-168">Filter returned data</span></span>](#filtering)
* [<span data-ttu-id="3df5c-169">Sort returned data</span><span class="sxs-lookup"><span data-stu-id="3df5c-169">Sort returned data</span></span>](#sorting)
* [<span data-ttu-id="3df5c-170">Return data in pages</span><span class="sxs-lookup"><span data-stu-id="3df5c-170">Return data in pages</span></span>](#paging)
* [<span data-ttu-id="3df5c-171">Select specific columns</span><span class="sxs-lookup"><span data-stu-id="3df5c-171">Select specific columns</span></span>](#selecting)
* [<span data-ttu-id="3df5c-172">Look up data by ID</span><span class="sxs-lookup"><span data-stu-id="3df5c-172">Look up data by ID</span></span>](#lookingup)

> [!NOTE]
> <span data-ttu-id="3df5c-173">A server-driven page size is enforced to prevent all rows from being returned.</span><span class="sxs-lookup"><span data-stu-id="3df5c-173">A server-driven page size is enforced to prevent all rows from being returned.</span></span>  <span data-ttu-id="3df5c-174">Paging keeps default requests for large data sets from negatively impacting the service.</span><span class="sxs-lookup"><span data-stu-id="3df5c-174">Paging keeps default requests for large data sets from negatively impacting the service.</span></span>  <span data-ttu-id="3df5c-175">To return more than 50 rows, use the `Skip` and `Take` method, as described in [Return data in pages](#paging).</span><span class="sxs-lookup"><span data-stu-id="3df5c-175">To return more than 50 rows, use the `Skip` and `Take` method, as described in [Return data in pages](#paging).</span></span>

### <a name="filtering"></a><span data-ttu-id="3df5c-176">How to: Filter returned data</span><span class="sxs-lookup"><span data-stu-id="3df5c-176">How to: Filter returned data</span></span>
<span data-ttu-id="3df5c-177">The following code illustrates how to filter data by including a `Where` clause in a query.</span><span class="sxs-lookup"><span data-stu-id="3df5c-177">The following code illustrates how to filter data by including a `Where` clause in a query.</span></span> <span data-ttu-id="3df5c-178">It returns all items from `todoTable` whose `Complete` property is equal to `false`.</span><span class="sxs-lookup"><span data-stu-id="3df5c-178">It returns all items from `todoTable` whose `Complete` property is equal to `false`.</span></span> <span data-ttu-id="3df5c-179">The [Where] function applies a row filtering predicate to the query against the table.</span><span class="sxs-lookup"><span data-stu-id="3df5c-179">The [Where] function applies a row filtering predicate to the query against the table.</span></span>

```
// This query filters out completed TodoItems and items without a timestamp.
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false)
    .ToListAsync();
```

<span data-ttu-id="3df5c-180">You can view the URI of the request sent to the backend by using message inspection software, such as browser developer tools or [Fiddler].</span><span class="sxs-lookup"><span data-stu-id="3df5c-180">You can view the URI of the request sent to the backend by using message inspection software, such as browser developer tools or [Fiddler].</span></span> <span data-ttu-id="3df5c-181">If you look at the request URI, notice that the query string is modified:</span><span class="sxs-lookup"><span data-stu-id="3df5c-181">If you look at the request URI, notice that the query string is modified:</span></span>

```
GET /tables/todoitem?$filter=(complete+eq+false) HTTP/1.1
```

<span data-ttu-id="3df5c-182">This OData request is translated into an SQL query by the Server SDK:</span><span class="sxs-lookup"><span data-stu-id="3df5c-182">This OData request is translated into an SQL query by the Server SDK:</span></span>

```
SELECT *
    FROM TodoItem
    WHERE ISNULL(complete, 0) = 0
```

<span data-ttu-id="3df5c-183">The function that is passed to the `Where` method can have an arbitrary number of conditions.</span><span class="sxs-lookup"><span data-stu-id="3df5c-183">The function that is passed to the `Where` method can have an arbitrary number of conditions.</span></span>

```
// This query filters out completed TodoItems where Text isn't null
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false && todoItem.Text != null)
    .ToListAsync();
```

<span data-ttu-id="3df5c-184">This example would be translated into an SQL query by the Server SDK:</span><span class="sxs-lookup"><span data-stu-id="3df5c-184">This example would be translated into an SQL query by the Server SDK:</span></span>

```
SELECT *
    FROM TodoItem
    WHERE ISNULL(complete, 0) = 0
          AND ISNULL(text, 0) = 0
```

<span data-ttu-id="3df5c-185">This query can also be split into multiple clauses:</span><span class="sxs-lookup"><span data-stu-id="3df5c-185">This query can also be split into multiple clauses:</span></span>

```
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false)
    .Where(todoItem => todoItem.Text != null)
    .ToListAsync();
```

<span data-ttu-id="3df5c-186">The two methods are equivalent and may be used interchangeably.</span><span class="sxs-lookup"><span data-stu-id="3df5c-186">The two methods are equivalent and may be used interchangeably.</span></span>  <span data-ttu-id="3df5c-187">The former option&mdash;of concatenating multiple predicates in one query&mdash;is more compact and recommended.</span><span class="sxs-lookup"><span data-stu-id="3df5c-187">The former option&mdash;of concatenating multiple predicates in one query&mdash;is more compact and recommended.</span></span>

<span data-ttu-id="3df5c-188">The `Where` clause supports operations that be translated into the OData subset.</span><span class="sxs-lookup"><span data-stu-id="3df5c-188">The `Where` clause supports operations that be translated into the OData subset.</span></span> <span data-ttu-id="3df5c-189">Operations include:</span><span class="sxs-lookup"><span data-stu-id="3df5c-189">Operations include:</span></span>

* <span data-ttu-id="3df5c-190">Relational operators (==, !=, <, <=, >, >=),</span><span class="sxs-lookup"><span data-stu-id="3df5c-190">Relational operators (==, !=, <, <=, >, >=),</span></span>
* <span data-ttu-id="3df5c-191">Arithmetic operators (+, -, /, \*, %),</span><span class="sxs-lookup"><span data-stu-id="3df5c-191">Arithmetic operators (+, -, /, \*, %),</span></span>
* <span data-ttu-id="3df5c-192">Number precision (Math.Floor, Math.Ceiling),</span><span class="sxs-lookup"><span data-stu-id="3df5c-192">Number precision (Math.Floor, Math.Ceiling),</span></span>
* <span data-ttu-id="3df5c-193">String functions (Length, Substring, Replace, IndexOf, StartsWith, EndsWith),</span><span class="sxs-lookup"><span data-stu-id="3df5c-193">String functions (Length, Substring, Replace, IndexOf, StartsWith, EndsWith),</span></span>
* <span data-ttu-id="3df5c-194">Date properties (Year, Month, Day, Hour, Minute, Second),</span><span class="sxs-lookup"><span data-stu-id="3df5c-194">Date properties (Year, Month, Day, Hour, Minute, Second),</span></span>
* <span data-ttu-id="3df5c-195">Access properties of an object, and</span><span class="sxs-lookup"><span data-stu-id="3df5c-195">Access properties of an object, and</span></span>
* <span data-ttu-id="3df5c-196">Expressions combining any of these operations.</span><span class="sxs-lookup"><span data-stu-id="3df5c-196">Expressions combining any of these operations.</span></span>

<span data-ttu-id="3df5c-197">When considering what the Server SDK supports, you can consider the [OData v3 Documentation].</span><span class="sxs-lookup"><span data-stu-id="3df5c-197">When considering what the Server SDK supports, you can consider the [OData v3 Documentation].</span></span>

### <a name="sorting"></a><span data-ttu-id="3df5c-198">How to: Sort returned data</span><span class="sxs-lookup"><span data-stu-id="3df5c-198">How to: Sort returned data</span></span>
<span data-ttu-id="3df5c-199">The following code illustrates how to sort data by including an [OrderBy] or [OrderByDescending] function in the query.</span><span class="sxs-lookup"><span data-stu-id="3df5c-199">The following code illustrates how to sort data by including an [OrderBy] or [OrderByDescending] function in the query.</span></span> <span data-ttu-id="3df5c-200">It returns items from `todoTable` sorted ascending by the `Text` field.</span><span class="sxs-lookup"><span data-stu-id="3df5c-200">It returns items from `todoTable` sorted ascending by the `Text` field.</span></span>

```
// Sort items in ascending order by Text field
MobileServiceTableQuery<TodoItem> query = todoTable
                .OrderBy(todoItem => todoItem.Text)
List<TodoItem> items = await query.ToListAsync();

// Sort items in descending order by Text field
MobileServiceTableQuery<TodoItem> query = todoTable
                .OrderByDescending(todoItem => todoItem.Text)
List<TodoItem> items = await query.ToListAsync();
```

### <a name="paging"></a><span data-ttu-id="3df5c-201">How to: Return data in pages</span><span class="sxs-lookup"><span data-stu-id="3df5c-201">How to: Return data in pages</span></span>
<span data-ttu-id="3df5c-202">By default, the backend returns only the first 50 rows.</span><span class="sxs-lookup"><span data-stu-id="3df5c-202">By default, the backend returns only the first 50 rows.</span></span> <span data-ttu-id="3df5c-203">You can increase the number of returned rows by calling the [Take] method.</span><span class="sxs-lookup"><span data-stu-id="3df5c-203">You can increase the number of returned rows by calling the [Take] method.</span></span> <span data-ttu-id="3df5c-204">Use `Take` along with the [Skip] method to request a specific "page" of the total dataset returned by the query.</span><span class="sxs-lookup"><span data-stu-id="3df5c-204">Use `Take` along with the [Skip] method to request a specific "page" of the total dataset returned by the query.</span></span> <span data-ttu-id="3df5c-205">The following query, when executed, returns the top three items in the table.</span><span class="sxs-lookup"><span data-stu-id="3df5c-205">The following query, when executed, returns the top three items in the table.</span></span>

```
// Define a filtered query that returns the top 3 items.
MobileServiceTableQuery<TodoItem> query = todoTable.Take(3);
List<TodoItem> items = await query.ToListAsync();
```

<span data-ttu-id="3df5c-206">The following revised query skips the first three results and returns the next three results.</span><span class="sxs-lookup"><span data-stu-id="3df5c-206">The following revised query skips the first three results and returns the next three results.</span></span> <span data-ttu-id="3df5c-207">This query produces the second "page" of data, where the page size is three items.</span><span class="sxs-lookup"><span data-stu-id="3df5c-207">This query produces the second "page" of data, where the page size is three items.</span></span>

```
// Define a filtered query that skips the top 3 items and returns the next 3 items.
MobileServiceTableQuery<TodoItem> query = todoTable.Skip(3).Take(3);
List<TodoItem> items = await query.ToListAsync();
```

<span data-ttu-id="3df5c-208">The [IncludeTotalCount] method requests the total count for *all* the records that would have been returned, ignoring any paging/limit clause specified:</span><span class="sxs-lookup"><span data-stu-id="3df5c-208">The [IncludeTotalCount] method requests the total count for *all* the records that would have been returned, ignoring any paging/limit clause specified:</span></span>

```
query = query.IncludeTotalCount();
```

<span data-ttu-id="3df5c-209">In a real world app, you can use queries similar to the preceding example with a pager control or comparable UI to navigate between pages.</span><span class="sxs-lookup"><span data-stu-id="3df5c-209">In a real world app, you can use queries similar to the preceding example with a pager control or comparable UI to navigate between pages.</span></span>

> [!NOTE]
> <span data-ttu-id="3df5c-210">To override the 50-row limit in a Mobile App backend, you must also apply the [EnableQueryAttribute] to the public GET method and specify the paging behavior.</span><span class="sxs-lookup"><span data-stu-id="3df5c-210">To override the 50-row limit in a Mobile App backend, you must also apply the [EnableQueryAttribute] to the public GET method and specify the paging behavior.</span></span> <span data-ttu-id="3df5c-211">When applied to the method, the following sets the maximum returned rows to 1000:</span><span class="sxs-lookup"><span data-stu-id="3df5c-211">When applied to the method, the following sets the maximum returned rows to 1000:</span></span>
>
> `[EnableQuery(MaxTop=1000)]`


### <a name="selecting"></a><span data-ttu-id="3df5c-212">How to: Select specific columns</span><span class="sxs-lookup"><span data-stu-id="3df5c-212">How to: Select specific columns</span></span>
<span data-ttu-id="3df5c-213">You can specify which set of properties to include in the results by adding a [Select] clause to your query.</span><span class="sxs-lookup"><span data-stu-id="3df5c-213">You can specify which set of properties to include in the results by adding a [Select] clause to your query.</span></span> <span data-ttu-id="3df5c-214">For example, the following code shows how to select just one field and also how to select and format multiple fields:</span><span class="sxs-lookup"><span data-stu-id="3df5c-214">For example, the following code shows how to select just one field and also how to select and format multiple fields:</span></span>

```
// Select one field -- just the Text
MobileServiceTableQuery<TodoItem> query = todoTable
                .Select(todoItem => todoItem.Text);
List<string> items = await query.ToListAsync();

// Select multiple fields -- both Complete and Text info
MobileServiceTableQuery<TodoItem> query = todoTable
                .Select(todoItem => string.Format("{0} -- {1}",
                    todoItem.Text.PadRight(30), todoItem.Complete ?
                    "Now complete!" : "Incomplete!"));
List<string> items = await query.ToListAsync();
```

<span data-ttu-id="3df5c-215">All the functions described so far are additive, so we can keep chaining them.</span><span class="sxs-lookup"><span data-stu-id="3df5c-215">All the functions described so far are additive, so we can keep chaining them.</span></span> <span data-ttu-id="3df5c-216">Each chained call affects more of the query.</span><span class="sxs-lookup"><span data-stu-id="3df5c-216">Each chained call affects more of the query.</span></span> <span data-ttu-id="3df5c-217">One more example:</span><span class="sxs-lookup"><span data-stu-id="3df5c-217">One more example:</span></span>

```
MobileServiceTableQuery<TodoItem> query = todoTable
                .Where(todoItem => todoItem.Complete == false)
                .Select(todoItem => todoItem.Text)
                .Skip(3).
                .Take(3);
List<string> items = await query.ToListAsync();
```

### <a name="lookingup"></a><span data-ttu-id="3df5c-218">How to: Look up data by ID</span><span class="sxs-lookup"><span data-stu-id="3df5c-218">How to: Look up data by ID</span></span>
<span data-ttu-id="3df5c-219">The [LookupAsync] function can be used to look up objects from the database with a particular ID.</span><span class="sxs-lookup"><span data-stu-id="3df5c-219">The [LookupAsync] function can be used to look up objects from the database with a particular ID.</span></span>

```
// This query filters out the item with the ID of 37BBF396-11F0-4B39-85C8-B319C729AF6D
TodoItem item = await todoTable.LookupAsync("37BBF396-11F0-4B39-85C8-B319C729AF6D");
```

### <a name="untypedqueries"></a><span data-ttu-id="3df5c-220">How to: Execute untyped queries</span><span class="sxs-lookup"><span data-stu-id="3df5c-220">How to: Execute untyped queries</span></span>
<span data-ttu-id="3df5c-221">When executing a query using an untyped table object, you must explicitly specify the OData query string by calling [ReadAsync], as in the following example:</span><span class="sxs-lookup"><span data-stu-id="3df5c-221">When executing a query using an untyped table object, you must explicitly specify the OData query string by calling [ReadAsync], as in the following example:</span></span>

```
// Lookup untyped data using OData
JToken untypedItems = await untypedTodoTable.ReadAsync("$filter=complete eq 0&$orderby=text");
```

<span data-ttu-id="3df5c-222">You get back JSON values that you can use like a property bag.</span><span class="sxs-lookup"><span data-stu-id="3df5c-222">You get back JSON values that you can use like a property bag.</span></span> <span data-ttu-id="3df5c-223">For more information on JToken and Newtonsoft Json.NET, see the [Json.NET] site.</span><span class="sxs-lookup"><span data-stu-id="3df5c-223">For more information on JToken and Newtonsoft Json.NET, see the [Json.NET] site.</span></span>

### <a name="inserting"></a><span data-ttu-id="3df5c-224">How to: Insert data into a Mobile App backend</span><span class="sxs-lookup"><span data-stu-id="3df5c-224">How to: Insert data into a Mobile App backend</span></span>
<span data-ttu-id="3df5c-225">All client types must contain a member named **Id**, which is by default a string.</span><span class="sxs-lookup"><span data-stu-id="3df5c-225">All client types must contain a member named **Id**, which is by default a string.</span></span> <span data-ttu-id="3df5c-226">This **Id** is required to perform CRUD operations and for offline sync. The following code illustrates how to use the [InsertAsync] method to insert new rows into a table.</span><span class="sxs-lookup"><span data-stu-id="3df5c-226">This **Id** is required to perform CRUD operations and for offline sync. The following code illustrates how to use the [InsertAsync] method to insert new rows into a table.</span></span> <span data-ttu-id="3df5c-227">The parameter contains the data to be inserted as a .NET object.</span><span class="sxs-lookup"><span data-stu-id="3df5c-227">The parameter contains the data to be inserted as a .NET object.</span></span>

```
await todoTable.InsertAsync(todoItem);
```

<span data-ttu-id="3df5c-228">If a unique custom ID value is not included in the `todoItem` during an insert, a GUID is generated by the server.</span><span class="sxs-lookup"><span data-stu-id="3df5c-228">If a unique custom ID value is not included in the `todoItem` during an insert, a GUID is generated by the server.</span></span>
<span data-ttu-id="3df5c-229">You can retrieve the generated Id by inspecting the object after the call returns.</span><span class="sxs-lookup"><span data-stu-id="3df5c-229">You can retrieve the generated Id by inspecting the object after the call returns.</span></span>

<span data-ttu-id="3df5c-230">To insert untyped data, you may take advantage of Json.NET:</span><span class="sxs-lookup"><span data-stu-id="3df5c-230">To insert untyped data, you may take advantage of Json.NET:</span></span>

```
JObject jo = new JObject();
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.InsertAsync(jo);
```

<span data-ttu-id="3df5c-231">Here is an example using an email address as a unique string id:</span><span class="sxs-lookup"><span data-stu-id="3df5c-231">Here is an example using an email address as a unique string id:</span></span>

```
JObject jo = new JObject();
jo.Add("id", "myemail@emaildomain.com");
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.InsertAsync(jo);
```

### <a name="working-with-id-values"></a><span data-ttu-id="3df5c-232">Working with ID values</span><span class="sxs-lookup"><span data-stu-id="3df5c-232">Working with ID values</span></span>
<span data-ttu-id="3df5c-233">Mobile Apps supports unique custom string values for the table's **id** column.</span><span class="sxs-lookup"><span data-stu-id="3df5c-233">Mobile Apps supports unique custom string values for the table's **id** column.</span></span> <span data-ttu-id="3df5c-234">A string value allows applications to use custom values such as email addresses or user names for the ID.</span><span class="sxs-lookup"><span data-stu-id="3df5c-234">A string value allows applications to use custom values such as email addresses or user names for the ID.</span></span>  <span data-ttu-id="3df5c-235">String IDs provide you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="3df5c-235">String IDs provide you with the following benefits:</span></span>

* <span data-ttu-id="3df5c-236">IDs are generated without making a round trip to the database.</span><span class="sxs-lookup"><span data-stu-id="3df5c-236">IDs are generated without making a round trip to the database.</span></span>
* <span data-ttu-id="3df5c-237">Records are easier to merge from different tables or databases.</span><span class="sxs-lookup"><span data-stu-id="3df5c-237">Records are easier to merge from different tables or databases.</span></span>
* <span data-ttu-id="3df5c-238">IDs values can integrate better with an application's logic.</span><span class="sxs-lookup"><span data-stu-id="3df5c-238">IDs values can integrate better with an application's logic.</span></span>

<span data-ttu-id="3df5c-239">When a string ID value is not set on an inserted record, the Mobile App backend generates a unique value for the ID.</span><span class="sxs-lookup"><span data-stu-id="3df5c-239">When a string ID value is not set on an inserted record, the Mobile App backend generates a unique value for the ID.</span></span> <span data-ttu-id="3df5c-240">You can use the [Guid.NewGuid] method to generate your own ID values, either on the client or in the backend.</span><span class="sxs-lookup"><span data-stu-id="3df5c-240">You can use the [Guid.NewGuid] method to generate your own ID values, either on the client or in the backend.</span></span>

```
JObject jo = new JObject();
jo.Add("id", Guid.NewGuid().ToString("N"));
```

### <a name="modifying"></a><span data-ttu-id="3df5c-241">How to: Modify data in a Mobile App backend</span><span class="sxs-lookup"><span data-stu-id="3df5c-241">How to: Modify data in a Mobile App backend</span></span>
<span data-ttu-id="3df5c-242">The following code illustrates how to use the [UpdateAsync] method to update an existing record with the same ID with new information.</span><span class="sxs-lookup"><span data-stu-id="3df5c-242">The following code illustrates how to use the [UpdateAsync] method to update an existing record with the same ID with new information.</span></span> <span data-ttu-id="3df5c-243">The parameter contains the data to be updated as a .NET object.</span><span class="sxs-lookup"><span data-stu-id="3df5c-243">The parameter contains the data to be updated as a .NET object.</span></span>

```
await todoTable.UpdateAsync(todoItem);
```

<span data-ttu-id="3df5c-244">To update untyped data, you may take advantage of [Json.NET] as follows:</span><span class="sxs-lookup"><span data-stu-id="3df5c-244">To update untyped data, you may take advantage of [Json.NET] as follows:</span></span>

```
JObject jo = new JObject();
jo.Add("id", "37BBF396-11F0-4B39-85C8-B319C729AF6D");
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.UpdateAsync(jo);
```

<span data-ttu-id="3df5c-245">An `id` field must be specified when making an update.</span><span class="sxs-lookup"><span data-stu-id="3df5c-245">An `id` field must be specified when making an update.</span></span> <span data-ttu-id="3df5c-246">The backend uses the `id` field to identify which row to update.</span><span class="sxs-lookup"><span data-stu-id="3df5c-246">The backend uses the `id` field to identify which row to update.</span></span> <span data-ttu-id="3df5c-247">The `id` field can be obtained from the result of the `InsertAsync` call.</span><span class="sxs-lookup"><span data-stu-id="3df5c-247">The `id` field can be obtained from the result of the `InsertAsync` call.</span></span> <span data-ttu-id="3df5c-248">An `ArgumentException` is raised if you try to update an item without providing the `id` value.</span><span class="sxs-lookup"><span data-stu-id="3df5c-248">An `ArgumentException` is raised if you try to update an item without providing the `id` value.</span></span>

### <a name="deleting"></a><span data-ttu-id="3df5c-249">How to: Delete data in a Mobile App backend</span><span class="sxs-lookup"><span data-stu-id="3df5c-249">How to: Delete data in a Mobile App backend</span></span>
<span data-ttu-id="3df5c-250">The following code illustrates how to use the [DeleteAsync] method to delete an existing instance.</span><span class="sxs-lookup"><span data-stu-id="3df5c-250">The following code illustrates how to use the [DeleteAsync] method to delete an existing instance.</span></span> <span data-ttu-id="3df5c-251">The instance is identified by the `id` field set on the `todoItem`.</span><span class="sxs-lookup"><span data-stu-id="3df5c-251">The instance is identified by the `id` field set on the `todoItem`.</span></span>

```
await todoTable.DeleteAsync(todoItem);
```

<span data-ttu-id="3df5c-252">To delete untyped data, you may take advantage of Json.NET as follows:</span><span class="sxs-lookup"><span data-stu-id="3df5c-252">To delete untyped data, you may take advantage of Json.NET as follows:</span></span>

```
JObject jo = new JObject();
jo.Add("id", "37BBF396-11F0-4B39-85C8-B319C729AF6D");
await table.DeleteAsync(jo);
```

<span data-ttu-id="3df5c-253">When you make a delete request, an ID must be specified.</span><span class="sxs-lookup"><span data-stu-id="3df5c-253">When you make a delete request, an ID must be specified.</span></span> <span data-ttu-id="3df5c-254">Other properties are not passed to the service or are ignored at the service.</span><span class="sxs-lookup"><span data-stu-id="3df5c-254">Other properties are not passed to the service or are ignored at the service.</span></span> <span data-ttu-id="3df5c-255">The result of a `DeleteAsync` call is usually `null`.</span><span class="sxs-lookup"><span data-stu-id="3df5c-255">The result of a `DeleteAsync` call is usually `null`.</span></span> <span data-ttu-id="3df5c-256">The ID to pass in can be obtained from the result of the `InsertAsync` call.</span><span class="sxs-lookup"><span data-stu-id="3df5c-256">The ID to pass in can be obtained from the result of the `InsertAsync` call.</span></span> <span data-ttu-id="3df5c-257">A `MobileServiceInvalidOperationException` is thrown when you try to delete an item without specifying the `id` field.</span><span class="sxs-lookup"><span data-stu-id="3df5c-257">A `MobileServiceInvalidOperationException` is thrown when you try to delete an item without specifying the `id` field.</span></span>

### <a name="optimisticconcurrency"></a><span data-ttu-id="3df5c-258">How to: Use Optimistic Concurrency for conflict resolution</span><span class="sxs-lookup"><span data-stu-id="3df5c-258">How to: Use Optimistic Concurrency for conflict resolution</span></span>
<span data-ttu-id="3df5c-259">Two or more clients may write changes to the same item at the same time.</span><span class="sxs-lookup"><span data-stu-id="3df5c-259">Two or more clients may write changes to the same item at the same time.</span></span> <span data-ttu-id="3df5c-260">Without conflict detection, the last write would overwrite any previous updates.</span><span class="sxs-lookup"><span data-stu-id="3df5c-260">Without conflict detection, the last write would overwrite any previous updates.</span></span> <span data-ttu-id="3df5c-261">**Optimistic concurrency control** assumes that each transaction can commit and therefore does not use any resource locking.</span><span class="sxs-lookup"><span data-stu-id="3df5c-261">**Optimistic concurrency control** assumes that each transaction can commit and therefore does not use any resource locking.</span></span>  <span data-ttu-id="3df5c-262">Before committing a transaction, optimistic concurrency control verifies that no other transaction has modified the data.</span><span class="sxs-lookup"><span data-stu-id="3df5c-262">Before committing a transaction, optimistic concurrency control verifies that no other transaction has modified the data.</span></span> <span data-ttu-id="3df5c-263">If the data has been modified, the committing transaction is rolled back.</span><span class="sxs-lookup"><span data-stu-id="3df5c-263">If the data has been modified, the committing transaction is rolled back.</span></span>

<span data-ttu-id="3df5c-264">Mobile Apps supports optimistic concurrency control by tracking changes to each item using the `version` system property column that is defined for each table in your Mobile App backend.</span><span class="sxs-lookup"><span data-stu-id="3df5c-264">Mobile Apps supports optimistic concurrency control by tracking changes to each item using the `version` system property column that is defined for each table in your Mobile App backend.</span></span> <span data-ttu-id="3df5c-265">Each time a record is updated, Mobile Apps sets the `version` property for that record to a new value.</span><span class="sxs-lookup"><span data-stu-id="3df5c-265">Each time a record is updated, Mobile Apps sets the `version` property for that record to a new value.</span></span> <span data-ttu-id="3df5c-266">During each update request, the `version` property of the record included with the request is compared to the same property for the record on the server.</span><span class="sxs-lookup"><span data-stu-id="3df5c-266">During each update request, the `version` property of the record included with the request is compared to the same property for the record on the server.</span></span> <span data-ttu-id="3df5c-267">If the version passed with the request does not match the backend, then the client library raises a `MobileServicePreconditionFailedException<T>` exception.</span><span class="sxs-lookup"><span data-stu-id="3df5c-267">If the version passed with the request does not match the backend, then the client library raises a `MobileServicePreconditionFailedException<T>` exception.</span></span> <span data-ttu-id="3df5c-268">The type included with the exception is the record from the backend containing the servers version of the record.</span><span class="sxs-lookup"><span data-stu-id="3df5c-268">The type included with the exception is the record from the backend containing the servers version of the record.</span></span> <span data-ttu-id="3df5c-269">The application can then use this information to decide whether to execute the update request again with the correct `version` value from the backend to commit changes.</span><span class="sxs-lookup"><span data-stu-id="3df5c-269">The application can then use this information to decide whether to execute the update request again with the correct `version` value from the backend to commit changes.</span></span>

<span data-ttu-id="3df5c-270">Define a column on the table class for the `version` system property to enable optimistic concurrency.</span><span class="sxs-lookup"><span data-stu-id="3df5c-270">Define a column on the table class for the `version` system property to enable optimistic concurrency.</span></span> <span data-ttu-id="3df5c-271">For example:</span><span class="sxs-lookup"><span data-stu-id="3df5c-271">For example:</span></span>

```
public class TodoItem
{
    public string Id { get; set; }

    [JsonProperty(PropertyName = "text")]
    public string Text { get; set; }

    [JsonProperty(PropertyName = "complete")]
    public bool Complete { get; set; }

    // *** Enable Optimistic Concurrency *** //
    [JsonProperty(PropertyName = "version")]
    public string Version { set; get; }
}
```

<span data-ttu-id="3df5c-272">Applications using untyped tables enable optimistic concurrency by setting the `Version` flag on the `SystemProperties` of the table as follows.</span><span class="sxs-lookup"><span data-stu-id="3df5c-272">Applications using untyped tables enable optimistic concurrency by setting the `Version` flag on the `SystemProperties` of the table as follows.</span></span>

```
//Enable optimistic concurrency by retrieving version
todoTable.SystemProperties |= MobileServiceSystemProperties.Version;
```

<span data-ttu-id="3df5c-273">In addition to enabling optimistic concurrency, you must also catch the `MobileServicePreconditionFailedException<T>` exception in your code when calling [UpdateAsync].</span><span class="sxs-lookup"><span data-stu-id="3df5c-273">In addition to enabling optimistic concurrency, you must also catch the `MobileServicePreconditionFailedException<T>` exception in your code when calling [UpdateAsync].</span></span>  <span data-ttu-id="3df5c-274">Resolve the conflict by applying the correct `version` to the updated record and call [UpdateAsync] with the resolved record.</span><span class="sxs-lookup"><span data-stu-id="3df5c-274">Resolve the conflict by applying the correct `version` to the updated record and call [UpdateAsync] with the resolved record.</span></span> <span data-ttu-id="3df5c-275">The following code shows how to resolve a write conflict once detected:</span><span class="sxs-lookup"><span data-stu-id="3df5c-275">The following code shows how to resolve a write conflict once detected:</span></span>

```
private async void UpdateToDoItem(TodoItem item)
{
    MobileServicePreconditionFailedException<TodoItem> exception = null;

    try
    {
        //update at the remote table
        await todoTable.UpdateAsync(item);
    }
    catch (MobileServicePreconditionFailedException<TodoItem> writeException)
    {
        exception = writeException;
    }

    if (exception != null)
    {
        // Conflict detected, the item has changed since the last query
        // Resolve the conflict between the local and server item
        await ResolveConflict(item, exception.Item);
    }
}


private async Task ResolveConflict(TodoItem localItem, TodoItem serverItem)
{
    //Ask user to choose the resoltion between versions
    MessageDialog msgDialog = new MessageDialog(
        String.Format("Server Text: \"{0}\" \nLocal Text: \"{1}\"\n",
        serverItem.Text, localItem.Text),
        "CONFLICT DETECTED - Select a resolution:");

    UICommand localBtn = new UICommand("Commit Local Text");
    UICommand ServerBtn = new UICommand("Leave Server Text");
    msgDialog.Commands.Add(localBtn);
    msgDialog.Commands.Add(ServerBtn);

    localBtn.Invoked = async (IUICommand command) =>
    {
        // To resolve the conflict, update the version of the item being committed. Otherwise, you will keep
        // catching a MobileServicePreConditionFailedException.
        localItem.Version = serverItem.Version;

        // Updating recursively here just in case another change happened while the user was making a decision
        UpdateToDoItem(localItem);
    };

    ServerBtn.Invoked = async (IUICommand command) =>
    {
        RefreshTodoItems();
    };

    await msgDialog.ShowAsync();
}
```

<span data-ttu-id="3df5c-276">For more information, see the [Offline Data Sync in Azure Mobile Apps] topic.</span><span class="sxs-lookup"><span data-stu-id="3df5c-276">For more information, see the [Offline Data Sync in Azure Mobile Apps] topic.</span></span>

### <a name="binding"></a><span data-ttu-id="3df5c-277">How to: Bind Mobile Apps data to a Windows user interface</span><span class="sxs-lookup"><span data-stu-id="3df5c-277">How to: Bind Mobile Apps data to a Windows user interface</span></span>
<span data-ttu-id="3df5c-278">This section shows how to display returned data objects using UI elements in a Windows app.</span><span class="sxs-lookup"><span data-stu-id="3df5c-278">This section shows how to display returned data objects using UI elements in a Windows app.</span></span>  <span data-ttu-id="3df5c-279">The following example code binds to the source of the list with a query for incomplete items.</span><span class="sxs-lookup"><span data-stu-id="3df5c-279">The following example code binds to the source of the list with a query for incomplete items.</span></span> <span data-ttu-id="3df5c-280">The [MobileServiceCollection] creates a Mobile Apps-aware binding collection.</span><span class="sxs-lookup"><span data-stu-id="3df5c-280">The [MobileServiceCollection] creates a Mobile Apps-aware binding collection.</span></span>

```
// This query filters out completed TodoItems.
MobileServiceCollection<TodoItem, TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false)
    .ToCollectionAsync();

// itemsControl is an IEnumerable that could be bound to a UI list control
IEnumerable itemsControl  = items;

// Bind this to a ListBox
ListBox lb = new ListBox();
lb.ItemsSource = items;
```

<span data-ttu-id="3df5c-281">Some controls in the managed runtime support an interface called [ISupportIncrementalLoading].</span><span class="sxs-lookup"><span data-stu-id="3df5c-281">Some controls in the managed runtime support an interface called [ISupportIncrementalLoading].</span></span> <span data-ttu-id="3df5c-282">This interface allows controls to request extra data when the user scrolls.</span><span class="sxs-lookup"><span data-stu-id="3df5c-282">This interface allows controls to request extra data when the user scrolls.</span></span> <span data-ttu-id="3df5c-283">There is built-in support for this interface for universal Windows apps via [MobileServiceIncrementalLoadingCollection], which automatically handles the calls from the controls.</span><span class="sxs-lookup"><span data-stu-id="3df5c-283">There is built-in support for this interface for universal Windows apps via [MobileServiceIncrementalLoadingCollection], which automatically handles the calls from the controls.</span></span> <span data-ttu-id="3df5c-284">Use `MobileServiceIncrementalLoadingCollection` in Windows apps as follows:</span><span class="sxs-lookup"><span data-stu-id="3df5c-284">Use `MobileServiceIncrementalLoadingCollection` in Windows apps as follows:</span></span>

```
MobileServiceIncrementalLoadingCollection<TodoItem,TodoItem> items;
items = todoTable.Where(todoItem => todoItem.Complete == false).ToIncrementalLoadingCollection();

ListBox lb = new ListBox();
lb.ItemsSource = items;
```

<span data-ttu-id="3df5c-285">To use the new collection on Windows Phone 8 and "Silverlight" apps, use the `ToCollection` extension methods on `IMobileServiceTableQuery<T>` and `IMobileServiceTable<T>`.</span><span class="sxs-lookup"><span data-stu-id="3df5c-285">To use the new collection on Windows Phone 8 and "Silverlight" apps, use the `ToCollection` extension methods on `IMobileServiceTableQuery<T>` and `IMobileServiceTable<T>`.</span></span> <span data-ttu-id="3df5c-286">To load data, call `LoadMoreItemsAsync()`.</span><span class="sxs-lookup"><span data-stu-id="3df5c-286">To load data, call `LoadMoreItemsAsync()`.</span></span>

```
MobileServiceCollection<TodoItem, TodoItem> items = todoTable.Where(todoItem => todoItem.Complete==false).ToCollection();
await items.LoadMoreItemsAsync();
```

<span data-ttu-id="3df5c-287">When you use the collection created by calling `ToCollectionAsync` or `ToCollection`, you get a collection that can be bound to UI controls.</span><span class="sxs-lookup"><span data-stu-id="3df5c-287">When you use the collection created by calling `ToCollectionAsync` or `ToCollection`, you get a collection that can be bound to UI controls.</span></span>  <span data-ttu-id="3df5c-288">This collection is paging-aware.</span><span class="sxs-lookup"><span data-stu-id="3df5c-288">This collection is paging-aware.</span></span>  <span data-ttu-id="3df5c-289">Since the collection is loading data from the network, loading sometimes fails.</span><span class="sxs-lookup"><span data-stu-id="3df5c-289">Since the collection is loading data from the network, loading sometimes fails.</span></span> <span data-ttu-id="3df5c-290">To handle such failures, override the `OnException` method on `MobileServiceIncrementalLoadingCollection` to handle exceptions resulting from calls to `LoadMoreItemsAsync`.</span><span class="sxs-lookup"><span data-stu-id="3df5c-290">To handle such failures, override the `OnException` method on `MobileServiceIncrementalLoadingCollection` to handle exceptions resulting from calls to `LoadMoreItemsAsync`.</span></span>

<span data-ttu-id="3df5c-291">Consider if your table has many fields but you only want to display some of them in your control.</span><span class="sxs-lookup"><span data-stu-id="3df5c-291">Consider if your table has many fields but you only want to display some of them in your control.</span></span> <span data-ttu-id="3df5c-292">You may use the guidance in the preceding section "[Select specific columns](#selecting)" to select specific columns to display in the UI.</span><span class="sxs-lookup"><span data-stu-id="3df5c-292">You may use the guidance in the preceding section "[Select specific columns](#selecting)" to select specific columns to display in the UI.</span></span>

### <a name="pagesize"></a><span data-ttu-id="3df5c-293">Change the Page size</span><span class="sxs-lookup"><span data-stu-id="3df5c-293">Change the Page size</span></span>
<span data-ttu-id="3df5c-294">Azure Mobile Apps returns a maximum of 50 items per request by default.</span><span class="sxs-lookup"><span data-stu-id="3df5c-294">Azure Mobile Apps returns a maximum of 50 items per request by default.</span></span>  <span data-ttu-id="3df5c-295">You can change the paging size by increasing the maximum page size on both the client and server.</span><span class="sxs-lookup"><span data-stu-id="3df5c-295">You can change the paging size by increasing the maximum page size on both the client and server.</span></span>  <span data-ttu-id="3df5c-296">To increase the requested page size, specify `PullOptions` when using `PullAsync()`:</span><span class="sxs-lookup"><span data-stu-id="3df5c-296">To increase the requested page size, specify `PullOptions` when using `PullAsync()`:</span></span>

```
PullOptions pullOptions = new PullOptions
    {
        MaxPageSize = 100
    };
```

<span data-ttu-id="3df5c-297">Assuming you have made the `PageSize` equal to or greater than 100 within the server, a request returns up to 100 items.</span><span class="sxs-lookup"><span data-stu-id="3df5c-297">Assuming you have made the `PageSize` equal to or greater than 100 within the server, a request returns up to 100 items.</span></span>

## <a name="#offlinesync"></a><span data-ttu-id="3df5c-298">Work with Offline Tables</span><span class="sxs-lookup"><span data-stu-id="3df5c-298">Work with Offline Tables</span></span>
<span data-ttu-id="3df5c-299">Offline tables use a local SQLite store to store data for use when offline.</span><span class="sxs-lookup"><span data-stu-id="3df5c-299">Offline tables use a local SQLite store to store data for use when offline.</span></span>  <span data-ttu-id="3df5c-300">All table operations are done against the local SQLite store instead of the remote server store.</span><span class="sxs-lookup"><span data-stu-id="3df5c-300">All table operations are done against the local SQLite store instead of the remote server store.</span></span>  <span data-ttu-id="3df5c-301">To create an offline table, first prepare your project:</span><span class="sxs-lookup"><span data-stu-id="3df5c-301">To create an offline table, first prepare your project:</span></span>

1. <span data-ttu-id="3df5c-302">In Visual Studio, right-click the solution > **Manage NuGet Packages for Solution...**, then search for and install the **Microsoft.Azure.Mobile.Client.SQLiteStore** NuGet package for all projects in the solution.</span><span class="sxs-lookup"><span data-stu-id="3df5c-302">In Visual Studio, right-click the solution > **Manage NuGet Packages for Solution...**, then search for and install the **Microsoft.Azure.Mobile.Client.SQLiteStore** NuGet package for all projects in the solution.</span></span>
2. <span data-ttu-id="3df5c-303">(Optional) To support Windows devices, install one of the following SQLite runtime packages:</span><span class="sxs-lookup"><span data-stu-id="3df5c-303">(Optional) To support Windows devices, install one of the following SQLite runtime packages:</span></span>

   * <span data-ttu-id="3df5c-304">**Windows 8.1 Runtime:** Install [SQLite for Windows 8.1][3].</span><span class="sxs-lookup"><span data-stu-id="3df5c-304">**Windows 8.1 Runtime:** Install [SQLite for Windows 8.1][3].</span></span>
   * <span data-ttu-id="3df5c-305">**Windows Phone 8.1:** Install [SQLite for Windows Phone 8.1][4].</span><span class="sxs-lookup"><span data-stu-id="3df5c-305">**Windows Phone 8.1:** Install [SQLite for Windows Phone 8.1][4].</span></span>
   * <span data-ttu-id="3df5c-306">**Universal Windows Platform** Install [SQLite for the Universal Windows][5].</span><span class="sxs-lookup"><span data-stu-id="3df5c-306">**Universal Windows Platform** Install [SQLite for the Universal Windows][5].</span></span>
3. <span data-ttu-id="3df5c-307">(Optional).</span><span class="sxs-lookup"><span data-stu-id="3df5c-307">(Optional).</span></span> <span data-ttu-id="3df5c-308">For Windows devices, click **References** > **Add Reference...**, expand the **Windows** folder > **Extensions**, then enable the appropriate **SQLite for Windows** SDK along with the **Visual C++ 2013 Runtime for Windows** SDK.</span><span class="sxs-lookup"><span data-stu-id="3df5c-308">For Windows devices, click **References** > **Add Reference...**, expand the **Windows** folder > **Extensions**, then enable the appropriate **SQLite for Windows** SDK along with the **Visual C++ 2013 Runtime for Windows** SDK.</span></span>
    <span data-ttu-id="3df5c-309">The SQLite SDK names vary slightly with each Windows platform.</span><span class="sxs-lookup"><span data-stu-id="3df5c-309">The SQLite SDK names vary slightly with each Windows platform.</span></span>

<span data-ttu-id="3df5c-310">Before a table reference can be created, the local store must be prepared:</span><span class="sxs-lookup"><span data-stu-id="3df5c-310">Before a table reference can be created, the local store must be prepared:</span></span>

```
var store = new MobileServiceSQLiteStore(Constants.OfflineDbPath);
store.DefineTable<TodoItem>();

//Initializes the SyncContext using the default IMobileServiceSyncHandler.
await this.client.SyncContext.InitializeAsync(store);
```

<span data-ttu-id="3df5c-311">Store initialization is normally done immediately after the client is created.</span><span class="sxs-lookup"><span data-stu-id="3df5c-311">Store initialization is normally done immediately after the client is created.</span></span>  <span data-ttu-id="3df5c-312">The **OfflineDbPath** should be a filename suitable for use on all platforms that you support.</span><span class="sxs-lookup"><span data-stu-id="3df5c-312">The **OfflineDbPath** should be a filename suitable for use on all platforms that you support.</span></span>  <span data-ttu-id="3df5c-313">If the path is a fully qualified path (that is, it starts with a slash), then that path is used.</span><span class="sxs-lookup"><span data-stu-id="3df5c-313">If the path is a fully qualified path (that is, it starts with a slash), then that path is used.</span></span>  <span data-ttu-id="3df5c-314">If the path is not fully qualified, the file is placed in a platform-specific location.</span><span class="sxs-lookup"><span data-stu-id="3df5c-314">If the path is not fully qualified, the file is placed in a platform-specific location.</span></span>

* <span data-ttu-id="3df5c-315">For iOS and Android devices, the default path is the "Personal Files" folder.</span><span class="sxs-lookup"><span data-stu-id="3df5c-315">For iOS and Android devices, the default path is the "Personal Files" folder.</span></span>
* <span data-ttu-id="3df5c-316">For Windows devices, the default path is the application-specific "AppData" folder.</span><span class="sxs-lookup"><span data-stu-id="3df5c-316">For Windows devices, the default path is the application-specific "AppData" folder.</span></span>

<span data-ttu-id="3df5c-317">A table reference can be obtained using the `GetSyncTable<>` method:</span><span class="sxs-lookup"><span data-stu-id="3df5c-317">A table reference can be obtained using the `GetSyncTable<>` method:</span></span>

```
var table = client.GetSyncTable<TodoItem>();
```

<span data-ttu-id="3df5c-318">You do not need to authenticate to use an offline table.</span><span class="sxs-lookup"><span data-stu-id="3df5c-318">You do not need to authenticate to use an offline table.</span></span>  <span data-ttu-id="3df5c-319">You only need to authenticate when you are communicating with the backend service.</span><span class="sxs-lookup"><span data-stu-id="3df5c-319">You only need to authenticate when you are communicating with the backend service.</span></span>

### <a name="syncoffline"></a><span data-ttu-id="3df5c-320">Syncing an Offline Table</span><span class="sxs-lookup"><span data-stu-id="3df5c-320">Syncing an Offline Table</span></span>
<span data-ttu-id="3df5c-321">Offline tables are not synchronized with the backend by default.</span><span class="sxs-lookup"><span data-stu-id="3df5c-321">Offline tables are not synchronized with the backend by default.</span></span>  <span data-ttu-id="3df5c-322">Synchronization is split into two pieces.</span><span class="sxs-lookup"><span data-stu-id="3df5c-322">Synchronization is split into two pieces.</span></span>  <span data-ttu-id="3df5c-323">You can push changes separately from downloading new items.</span><span class="sxs-lookup"><span data-stu-id="3df5c-323">You can push changes separately from downloading new items.</span></span>  <span data-ttu-id="3df5c-324">Here is a typical sync method:</span><span class="sxs-lookup"><span data-stu-id="3df5c-324">Here is a typical sync method:</span></span>

```
public async Task SyncAsync()
{
    ReadOnlyCollection<MobileServiceTableOperationError> syncErrors = null;

    try
    {
        await this.client.SyncContext.PushAsync();

        await this.todoTable.PullAsync(
            //The first parameter is a query name that is used internally by the client SDK to implement incremental sync.
            //Use a different query name for each unique query in your program
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

    // Simple error/conflict handling. A real application would handle the various errors like network conditions,
    // server conflicts and others via the IMobileServiceSyncHandler.
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

            Debug.WriteLine(@"Error executing sync operation. Item: {0} ({1}). Operation discarded.", error.TableName, error.Item["id"]);
        }
    }
}
```

<span data-ttu-id="3df5c-325">If the first argument to `PullAsync` is null, then incremental sync is not used.</span><span class="sxs-lookup"><span data-stu-id="3df5c-325">If the first argument to `PullAsync` is null, then incremental sync is not used.</span></span>  <span data-ttu-id="3df5c-326">Each sync operation retrieves all records.</span><span class="sxs-lookup"><span data-stu-id="3df5c-326">Each sync operation retrieves all records.</span></span>

<span data-ttu-id="3df5c-327">The SDK performs an implicit `PushAsync()` before pulling records.</span><span class="sxs-lookup"><span data-stu-id="3df5c-327">The SDK performs an implicit `PushAsync()` before pulling records.</span></span>

<span data-ttu-id="3df5c-328">Conflict handling happens on a `PullAsync()` method.</span><span class="sxs-lookup"><span data-stu-id="3df5c-328">Conflict handling happens on a `PullAsync()` method.</span></span>  <span data-ttu-id="3df5c-329">You can deal with conflicts in the same way as online tables.</span><span class="sxs-lookup"><span data-stu-id="3df5c-329">You can deal with conflicts in the same way as online tables.</span></span>  <span data-ttu-id="3df5c-330">The conflict is produced when `PullAsync()` is called instead of during the insert, update, or delete.</span><span class="sxs-lookup"><span data-stu-id="3df5c-330">The conflict is produced when `PullAsync()` is called instead of during the insert, update, or delete.</span></span> <span data-ttu-id="3df5c-331">If multiple conflicts happen, they are bundled into a single MobileServicePushFailedException.</span><span class="sxs-lookup"><span data-stu-id="3df5c-331">If multiple conflicts happen, they are bundled into a single MobileServicePushFailedException.</span></span>  <span data-ttu-id="3df5c-332">Handle each failure separately.</span><span class="sxs-lookup"><span data-stu-id="3df5c-332">Handle each failure separately.</span></span>

## <a name="#customapi"></a><span data-ttu-id="3df5c-333">Work with a custom API</span><span class="sxs-lookup"><span data-stu-id="3df5c-333">Work with a custom API</span></span>
<span data-ttu-id="3df5c-334">A custom API enables you to define custom endpoints that expose server functionality that does not map to an insert, update, delete, or read operation.</span><span class="sxs-lookup"><span data-stu-id="3df5c-334">A custom API enables you to define custom endpoints that expose server functionality that does not map to an insert, update, delete, or read operation.</span></span> <span data-ttu-id="3df5c-335">By using a custom API, you can have more control over messaging, including reading and setting HTTP message headers and defining a message body format other than JSON.</span><span class="sxs-lookup"><span data-stu-id="3df5c-335">By using a custom API, you can have more control over messaging, including reading and setting HTTP message headers and defining a message body format other than JSON.</span></span>

<span data-ttu-id="3df5c-336">You call a custom API by calling one of the [InvokeApiAsync] methods on the client.</span><span class="sxs-lookup"><span data-stu-id="3df5c-336">You call a custom API by calling one of the [InvokeApiAsync] methods on the client.</span></span> <span data-ttu-id="3df5c-337">For example, the following line of code sends a POST request to the **completeAll** API on the backend:</span><span class="sxs-lookup"><span data-stu-id="3df5c-337">For example, the following line of code sends a POST request to the **completeAll** API on the backend:</span></span>

```
var result = await client.InvokeApiAsync<MarkAllResult>("completeAll", System.Net.Http.HttpMethod.Post, null);
```

<span data-ttu-id="3df5c-338">This form is a typed method call and requires that the **MarkAllResult** return type is defined.</span><span class="sxs-lookup"><span data-stu-id="3df5c-338">This form is a typed method call and requires that the **MarkAllResult** return type is defined.</span></span> <span data-ttu-id="3df5c-339">Both typed and untyped methods are supported.</span><span class="sxs-lookup"><span data-stu-id="3df5c-339">Both typed and untyped methods are supported.</span></span>

<span data-ttu-id="3df5c-340">The InvokeApiAsync() method prepends '/api/' to the API that you wish to call unless the API starts with a '/'.</span><span class="sxs-lookup"><span data-stu-id="3df5c-340">The InvokeApiAsync() method prepends '/api/' to the API that you wish to call unless the API starts with a '/'.</span></span>
<span data-ttu-id="3df5c-341">For example:</span><span class="sxs-lookup"><span data-stu-id="3df5c-341">For example:</span></span>

* <span data-ttu-id="3df5c-342">`InvokeApiAsync("completeAll",...)` calls /api/completeAll on the backend</span><span class="sxs-lookup"><span data-stu-id="3df5c-342">`InvokeApiAsync("completeAll",...)` calls /api/completeAll on the backend</span></span>
* <span data-ttu-id="3df5c-343">`InvokeApiAsync("/.auth/me",...)` calls /.auth/me on the backend</span><span class="sxs-lookup"><span data-stu-id="3df5c-343">`InvokeApiAsync("/.auth/me",...)` calls /.auth/me on the backend</span></span>

<span data-ttu-id="3df5c-344">You can use InvokeApiAsync to call any WebAPI, including those WebAPIs that are not defined with Azure Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="3df5c-344">You can use InvokeApiAsync to call any WebAPI, including those WebAPIs that are not defined with Azure Mobile Apps.</span></span>  <span data-ttu-id="3df5c-345">When you use InvokeApiAsync(), the appropriate headers, including authentication headers, are sent with the request.</span><span class="sxs-lookup"><span data-stu-id="3df5c-345">When you use InvokeApiAsync(), the appropriate headers, including authentication headers, are sent with the request.</span></span>

## <a name="authentication"></a><span data-ttu-id="3df5c-346">Authenticate users</span><span class="sxs-lookup"><span data-stu-id="3df5c-346">Authenticate users</span></span>
<span data-ttu-id="3df5c-347">Mobile Apps supports authenticating and authorizing app users using various external identity providers: Facebook, Google, Microsoft Account, Twitter, and Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3df5c-347">Mobile Apps supports authenticating and authorizing app users using various external identity providers: Facebook, Google, Microsoft Account, Twitter, and Azure Active Directory.</span></span> <span data-ttu-id="3df5c-348">You can set permissions on tables to restrict access for specific operations to only authenticated users.</span><span class="sxs-lookup"><span data-stu-id="3df5c-348">You can set permissions on tables to restrict access for specific operations to only authenticated users.</span></span> <span data-ttu-id="3df5c-349">You can also use the identity of authenticated users to implement authorization rules in server scripts.</span><span class="sxs-lookup"><span data-stu-id="3df5c-349">You can also use the identity of authenticated users to implement authorization rules in server scripts.</span></span> <span data-ttu-id="3df5c-350">For more information, see the tutorial [Add authentication to your app].</span><span class="sxs-lookup"><span data-stu-id="3df5c-350">For more information, see the tutorial [Add authentication to your app].</span></span>

<span data-ttu-id="3df5c-351">Two authentication flows are supported: *client-managed* and *server-managed* flow.</span><span class="sxs-lookup"><span data-stu-id="3df5c-351">Two authentication flows are supported: *client-managed* and *server-managed* flow.</span></span> <span data-ttu-id="3df5c-352">The server-managed flow provides the simplest authentication experience, as it relies on the provider's web authentication interface.</span><span class="sxs-lookup"><span data-stu-id="3df5c-352">The server-managed flow provides the simplest authentication experience, as it relies on the provider's web authentication interface.</span></span> <span data-ttu-id="3df5c-353">The client-managed flow allows for deeper integration with device-specific capabilities as it relies on provider-specific device-specific SDKs.</span><span class="sxs-lookup"><span data-stu-id="3df5c-353">The client-managed flow allows for deeper integration with device-specific capabilities as it relies on provider-specific device-specific SDKs.</span></span>

> [!NOTE]
> <span data-ttu-id="3df5c-354">We recommend using a client-managed flow in your production apps.</span><span class="sxs-lookup"><span data-stu-id="3df5c-354">We recommend using a client-managed flow in your production apps.</span></span>

<span data-ttu-id="3df5c-355">To set up authentication, you must register your app with one or more identity providers.</span><span class="sxs-lookup"><span data-stu-id="3df5c-355">To set up authentication, you must register your app with one or more identity providers.</span></span>  <span data-ttu-id="3df5c-356">The identity provider generates a client ID and a client secret for your app.</span><span class="sxs-lookup"><span data-stu-id="3df5c-356">The identity provider generates a client ID and a client secret for your app.</span></span>  <span data-ttu-id="3df5c-357">These values are then set in your backend to enable Azure App Service authentication/authorization.</span><span class="sxs-lookup"><span data-stu-id="3df5c-357">These values are then set in your backend to enable Azure App Service authentication/authorization.</span></span>  <span data-ttu-id="3df5c-358">For more information, follow the detailed instructions in the tutorial [Add authentication to your app].</span><span class="sxs-lookup"><span data-stu-id="3df5c-358">For more information, follow the detailed instructions in the tutorial [Add authentication to your app].</span></span>

<span data-ttu-id="3df5c-359">The following topics are covered in this section:</span><span class="sxs-lookup"><span data-stu-id="3df5c-359">The following topics are covered in this section:</span></span>

* [<span data-ttu-id="3df5c-360">Client-managed authentication</span><span class="sxs-lookup"><span data-stu-id="3df5c-360">Client-managed authentication</span></span>](#clientflow)
* [<span data-ttu-id="3df5c-361">Server-managed authentication</span><span class="sxs-lookup"><span data-stu-id="3df5c-361">Server-managed authentication</span></span>](#serverflow)
* [<span data-ttu-id="3df5c-362">Caching the authentication token</span><span class="sxs-lookup"><span data-stu-id="3df5c-362">Caching the authentication token</span></span>](#caching)

### <a name="clientflow"></a><span data-ttu-id="3df5c-363">Client-managed authentication</span><span class="sxs-lookup"><span data-stu-id="3df5c-363">Client-managed authentication</span></span>
<span data-ttu-id="3df5c-364">Your app can independently contact the identity provider and then provide the returned token during login with your backend.</span><span class="sxs-lookup"><span data-stu-id="3df5c-364">Your app can independently contact the identity provider and then provide the returned token during login with your backend.</span></span> <span data-ttu-id="3df5c-365">This client flow enables you to provide a single sign-on experience for users or to retrieve additional user data from the identity provider.</span><span class="sxs-lookup"><span data-stu-id="3df5c-365">This client flow enables you to provide a single sign-on experience for users or to retrieve additional user data from the identity provider.</span></span> <span data-ttu-id="3df5c-366">Client flow authentication is preferred to using a server flow as the identity provider SDK provides a more native UX feel and allows for additional customization.</span><span class="sxs-lookup"><span data-stu-id="3df5c-366">Client flow authentication is preferred to using a server flow as the identity provider SDK provides a more native UX feel and allows for additional customization.</span></span>

<span data-ttu-id="3df5c-367">Examples are provided for the following client-flow authentication patterns:</span><span class="sxs-lookup"><span data-stu-id="3df5c-367">Examples are provided for the following client-flow authentication patterns:</span></span>

* [<span data-ttu-id="3df5c-368">Active Directory Authentication Library</span><span class="sxs-lookup"><span data-stu-id="3df5c-368">Active Directory Authentication Library</span></span>](#adal)
* [<span data-ttu-id="3df5c-369">Facebook or Google</span><span class="sxs-lookup"><span data-stu-id="3df5c-369">Facebook or Google</span></span>](#client-facebook)
* [<span data-ttu-id="3df5c-370">Live SDK</span><span class="sxs-lookup"><span data-stu-id="3df5c-370">Live SDK</span></span>](#client-livesdk)

#### <a name="adal"></a><span data-ttu-id="3df5c-371">Authenticate users with the Active Directory Authentication Library</span><span class="sxs-lookup"><span data-stu-id="3df5c-371">Authenticate users with the Active Directory Authentication Library</span></span>
<span data-ttu-id="3df5c-372">You can use the Active Directory Authentication Library (ADAL) to initiate user authentication from the client using Azure Active Directory authentication.</span><span class="sxs-lookup"><span data-stu-id="3df5c-372">You can use the Active Directory Authentication Library (ADAL) to initiate user authentication from the client using Azure Active Directory authentication.</span></span>

1. <span data-ttu-id="3df5c-373">Configure your mobile app backend for AAD sign-on by following the [How to configure App Service for Active Directory login] tutorial.</span><span class="sxs-lookup"><span data-stu-id="3df5c-373">Configure your mobile app backend for AAD sign-on by following the [How to configure App Service for Active Directory login] tutorial.</span></span> <span data-ttu-id="3df5c-374">Make sure to complete the optional step of registering a native client application.</span><span class="sxs-lookup"><span data-stu-id="3df5c-374">Make sure to complete the optional step of registering a native client application.</span></span>
2. <span data-ttu-id="3df5c-375">In Visual Studio or Xamarin Studio, open your project and add a reference to the `Microsoft.IdentityModel.CLients.ActiveDirectory` NuGet package.</span><span class="sxs-lookup"><span data-stu-id="3df5c-375">In Visual Studio or Xamarin Studio, open your project and add a reference to the `Microsoft.IdentityModel.CLients.ActiveDirectory` NuGet package.</span></span> <span data-ttu-id="3df5c-376">When searching, include pre-release versions.</span><span class="sxs-lookup"><span data-stu-id="3df5c-376">When searching, include pre-release versions.</span></span>
3. <span data-ttu-id="3df5c-377">Add the following code to your application, according to the platform you are using.</span><span class="sxs-lookup"><span data-stu-id="3df5c-377">Add the following code to your application, according to the platform you are using.</span></span> <span data-ttu-id="3df5c-378">In each, make the following replacements:</span><span class="sxs-lookup"><span data-stu-id="3df5c-378">In each, make the following replacements:</span></span>

   * <span data-ttu-id="3df5c-379">Replace **INSERT-AUTHORITY-HERE** with the name of the tenant in which you provisioned your application.</span><span class="sxs-lookup"><span data-stu-id="3df5c-379">Replace **INSERT-AUTHORITY-HERE** with the name of the tenant in which you provisioned your application.</span></span> <span data-ttu-id="3df5c-380">The format should be https://login.windows.net/contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="3df5c-380">The format should be https://login.windows.net/contoso.onmicrosoft.com.</span></span> <span data-ttu-id="3df5c-381">This value can be copied from the Domain tab in your Azure Active Directory in the [Azure classic portal].</span><span class="sxs-lookup"><span data-stu-id="3df5c-381">This value can be copied from the Domain tab in your Azure Active Directory in the [Azure classic portal].</span></span>
   * <span data-ttu-id="3df5c-382">Replace **INSERT-RESOURCE-ID-HERE** with the client ID for your mobile app backend.</span><span class="sxs-lookup"><span data-stu-id="3df5c-382">Replace **INSERT-RESOURCE-ID-HERE** with the client ID for your mobile app backend.</span></span> <span data-ttu-id="3df5c-383">You can obtain the client ID from the **Advanced** tab under **Azure Active Directory Settings** in the portal.</span><span class="sxs-lookup"><span data-stu-id="3df5c-383">You can obtain the client ID from the **Advanced** tab under **Azure Active Directory Settings** in the portal.</span></span>
   * <span data-ttu-id="3df5c-384">Replace **INSERT-CLIENT-ID-HERE** with the client ID you copied from the native client application.</span><span class="sxs-lookup"><span data-stu-id="3df5c-384">Replace **INSERT-CLIENT-ID-HERE** with the client ID you copied from the native client application.</span></span>
   * <span data-ttu-id="3df5c-385">Replace **INSERT-REDIRECT-URI-HERE** with your site's */.auth/login/done* endpoint, using the HTTPS scheme.</span><span class="sxs-lookup"><span data-stu-id="3df5c-385">Replace **INSERT-REDIRECT-URI-HERE** with your site's */.auth/login/done* endpoint, using the HTTPS scheme.</span></span> <span data-ttu-id="3df5c-386">This value should be similar to *https://contoso.azurewebsites.net/.auth/login/done*.</span><span class="sxs-lookup"><span data-stu-id="3df5c-386">This value should be similar to *https://contoso.azurewebsites.net/.auth/login/done*.</span></span>

     <span data-ttu-id="3df5c-387">The code needed for each platform follows:</span><span class="sxs-lookup"><span data-stu-id="3df5c-387">The code needed for each platform follows:</span></span>

     <span data-ttu-id="3df5c-388">**Windows:**</span><span class="sxs-lookup"><span data-stu-id="3df5c-388">**Windows:**</span></span>

    ```
    private MobileServiceUser user;
    private async Task AuthenticateAsync()
    {

        string authority = "INSERT-AUTHORITY-HERE";
        string resourceId = "INSERT-RESOURCE-ID-HERE";
        string clientId = "INSERT-CLIENT-ID-HERE";
        string redirectUri = "INSERT-REDIRECT-URI-HERE";
        while (user == null)
        {
            string message;
            try
            {
                AuthenticationContext ac = new AuthenticationContext(authority);
                AuthenticationResult ar = await ac.AcquireTokenAsync(resourceId, clientId,
                    new Uri(redirectUri), new PlatformParameters(PromptBehavior.Auto, false) );
                JObject payload = new JObject();
                payload["access_token"] = ar.AccessToken;
                user = await App.MobileService.LoginAsync(
                    MobileServiceAuthenticationProvider.WindowsAzureActiveDirectory, payload);
                message = string.Format("You are now logged in - {0}", user.UserId);
            }
            catch (InvalidOperationException)
            {
                message = "You must log in. Login Required";
            }
            var dialog = new MessageDialog(message);
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
        }
    }
    ```

     <span data-ttu-id="3df5c-389">**Xamarin.iOS**</span><span class="sxs-lookup"><span data-stu-id="3df5c-389">**Xamarin.iOS**</span></span>

    ```
    private MobileServiceUser user;
    private async Task AuthenticateAsync(UIViewController view)
    {

        string authority = "INSERT-AUTHORITY-HERE";
        string resourceId = "INSERT-RESOURCE-ID-HERE";
        string clientId = "INSERT-CLIENT-ID-HERE";
        string redirectUri = "INSERT-REDIRECT-URI-HERE";
        try
        {
            AuthenticationContext ac = new AuthenticationContext(authority);
            AuthenticationResult ar = await ac.AcquireTokenAsync(resourceId, clientId,
                new Uri(redirectUri), new PlatformParameters(view));
            JObject payload = new JObject();
            payload["access_token"] = ar.AccessToken;
            user = await client.LoginAsync(
                MobileServiceAuthenticationProvider.WindowsAzureActiveDirectory, payload);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine(@"ERROR - AUTHENTICATION FAILED {0}", ex.Message);
        }
    }
    ```

     <span data-ttu-id="3df5c-390">**Xamarin.Android**</span><span class="sxs-lookup"><span data-stu-id="3df5c-390">**Xamarin.Android**</span></span>

    ```
    private MobileServiceUser user;
    private async Task AuthenticateAsync()
    {

        string authority = "INSERT-AUTHORITY-HERE";
        string resourceId = "INSERT-RESOURCE-ID-HERE";
        string clientId = "INSERT-CLIENT-ID-HERE";
        string redirectUri = "INSERT-REDIRECT-URI-HERE";
        try
        {
            AuthenticationContext ac = new AuthenticationContext(authority);
            AuthenticationResult ar = await ac.AcquireTokenAsync(resourceId, clientId,
                new Uri(redirectUri), new PlatformParameters(this));
            JObject payload = new JObject();
            payload["access_token"] = ar.AccessToken;
            user = await client.LoginAsync(
                MobileServiceAuthenticationProvider.WindowsAzureActiveDirectory, payload);
        }
        catch (Exception ex)
        {
            AlertDialog.Builder builder = new AlertDialog.Builder(this);
            builder.SetMessage(ex.Message);
            builder.SetTitle("You must log in. Login Required");
            builder.Create().Show();
        }
    }
    protected override void OnActivityResult(int requestCode, Result resultCode, Intent data)
    {

        base.OnActivityResult(requestCode, resultCode, data);
        AuthenticationAgentContinuationHelper.SetAuthenticationAgentContinuationEventArgs(requestCode, resultCode, data);
    }
    ```

#### <a name="client-facebook"></a><span data-ttu-id="3df5c-391">Single Sign-On using a token from Facebook or Google</span><span class="sxs-lookup"><span data-stu-id="3df5c-391">Single Sign-On using a token from Facebook or Google</span></span>
<span data-ttu-id="3df5c-392">You can use the client flow as shown in this snippet for Facebook or Google.</span><span class="sxs-lookup"><span data-stu-id="3df5c-392">You can use the client flow as shown in this snippet for Facebook or Google.</span></span>

```
var token = new JObject();
// Replace access_token_value with actual value of your access token obtained
// using the Facebook or Google SDK.
token.Add("access_token", "access_token_value");

private MobileServiceUser user;
private async Task AuthenticateAsync()
{
    while (user == null)
    {
        string message;
        try
        {
            // Change MobileServiceAuthenticationProvider.Facebook
            // to MobileServiceAuthenticationProvider.Google if using Google auth.
            user = await client.LoginAsync(MobileServiceAuthenticationProvider.Facebook, token);
            message = string.Format("You are now logged in - {0}", user.UserId);
        }
        catch (InvalidOperationException)
        {
            message = "You must log in. Login Required";
        }

        var dialog = new MessageDialog(message);
        dialog.Commands.Add(new UICommand("OK"));
        await dialog.ShowAsync();
    }
}
```

#### <a name="client-livesdk"></a><span data-ttu-id="3df5c-393">Single Sign On using Microsoft Account with the Live SDK</span><span class="sxs-lookup"><span data-stu-id="3df5c-393">Single Sign On using Microsoft Account with the Live SDK</span></span>
<span data-ttu-id="3df5c-394">To authenticate users, you must register your app at the Microsoft account Developer Center.</span><span class="sxs-lookup"><span data-stu-id="3df5c-394">To authenticate users, you must register your app at the Microsoft account Developer Center.</span></span> <span data-ttu-id="3df5c-395">Configure the registration details on your Mobile App backend.</span><span class="sxs-lookup"><span data-stu-id="3df5c-395">Configure the registration details on your Mobile App backend.</span></span> <span data-ttu-id="3df5c-396">To create a Microsoft account registration and connect it to your Mobile App backend, complete the steps in [Register your app to use a Microsoft account login].</span><span class="sxs-lookup"><span data-stu-id="3df5c-396">To create a Microsoft account registration and connect it to your Mobile App backend, complete the steps in [Register your app to use a Microsoft account login].</span></span> <span data-ttu-id="3df5c-397">If you have both Windows Store and Windows Phone 8/Silverlight versions of your app, register the Windows Store version first.</span><span class="sxs-lookup"><span data-stu-id="3df5c-397">If you have both Windows Store and Windows Phone 8/Silverlight versions of your app, register the Windows Store version first.</span></span>

<span data-ttu-id="3df5c-398">The following code authenticates using Live SDK and uses the returned token to sign in to your Mobile App backend.</span><span class="sxs-lookup"><span data-stu-id="3df5c-398">The following code authenticates using Live SDK and uses the returned token to sign in to your Mobile App backend.</span></span>

```
private LiveConnectSession session;
    //private static string clientId = "<microsoft-account-client-id>";
private async System.Threading.Tasks.Task AuthenticateAsync()
{

    // Get the URL the Mobile App backend.
    var serviceUrl = App.MobileService.ApplicationUri.AbsoluteUri;

    // Create the authentication client for Windows Store using the service URL.
    LiveAuthClient liveIdClient = new LiveAuthClient(serviceUrl);
    //// Create the authentication client for Windows Phone using the client ID of the registration.
    //LiveAuthClient liveIdClient = new LiveAuthClient(clientId);

    while (session == null)
    {
        // Request the authentication token from the Live authentication service.
        // The wl.basic scope should always be requested.  Other scopes can be added
        LiveLoginResult result = await liveIdClient.LoginAsync(new string[] { "wl.basic" });
        if (result.Status == LiveConnectSessionStatus.Connected)
        {
            session = result.Session;

            // Get information about the logged-in user.
            LiveConnectClient client = new LiveConnectClient(session);
            LiveOperationResult meResult = await client.GetAsync("me");

            // Use the Microsoft account auth token to sign in to App Service.
            MobileServiceUser loginResult = await App.MobileService
                .LoginWithMicrosoftAccountAsync(result.Session.AuthenticationToken);

            // Display a personalized sign-in greeting.
            string title = string.Format("Welcome {0}!", meResult.Result["first_name"]);
            var message = string.Format("You are now logged in - {0}", loginResult.UserId);
            var dialog = new MessageDialog(message, title);
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
        }
        else
        {
            session = null;
            var dialog = new MessageDialog("You must log in.", "Login Required");
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
        }
    }
}
```

<span data-ttu-id="3df5c-399">For more information, see the [Windows Live SDK] documentation.</span><span class="sxs-lookup"><span data-stu-id="3df5c-399">For more information, see the [Windows Live SDK] documentation.</span></span>

### <a name="serverflow"></a><span data-ttu-id="3df5c-400">Server-managed authentication</span><span class="sxs-lookup"><span data-stu-id="3df5c-400">Server-managed authentication</span></span>
<span data-ttu-id="3df5c-401">Once you have registered your identity provider, call the [LoginAsync] method on the [MobileServiceClient] with the [MobileServiceAuthenticationProvider] value of your provider.</span><span class="sxs-lookup"><span data-stu-id="3df5c-401">Once you have registered your identity provider, call the [LoginAsync] method on the [MobileServiceClient] with the [MobileServiceAuthenticationProvider] value of your provider.</span></span> <span data-ttu-id="3df5c-402">For example, the following code initiates a server flow sign-in by using Facebook.</span><span class="sxs-lookup"><span data-stu-id="3df5c-402">For example, the following code initiates a server flow sign-in by using Facebook.</span></span>

```
private MobileServiceUser user;
private async System.Threading.Tasks.Task Authenticate()
{
    while (user == null)
    {
        string message;
        try
        {
            user = await client
                .LoginAsync(MobileServiceAuthenticationProvider.Facebook);
            message =
                string.Format("You are now logged in - {0}", user.UserId);
        }
        catch (InvalidOperationException)
        {
            message = "You must log in. Login Required";
        }

        var dialog = new MessageDialog(message);
        dialog.Commands.Add(new UICommand("OK"));
        await dialog.ShowAsync();
    }
}
```

<span data-ttu-id="3df5c-403">If you are using an identity provider other than Facebook, change the value of [MobileServiceAuthenticationProvider] to the value for your provider.</span><span class="sxs-lookup"><span data-stu-id="3df5c-403">If you are using an identity provider other than Facebook, change the value of [MobileServiceAuthenticationProvider] to the value for your provider.</span></span>

<span data-ttu-id="3df5c-404">In a server flow, Azure App Service manages the OAuth authentication flow by displaying the sign-in page of the selected provider.</span><span class="sxs-lookup"><span data-stu-id="3df5c-404">In a server flow, Azure App Service manages the OAuth authentication flow by displaying the sign-in page of the selected provider.</span></span>  <span data-ttu-id="3df5c-405">Once the identity provider returns, Azure App Service generates an App Service authentication token.</span><span class="sxs-lookup"><span data-stu-id="3df5c-405">Once the identity provider returns, Azure App Service generates an App Service authentication token.</span></span> <span data-ttu-id="3df5c-406">The [LoginAsync] method returns a [MobileServiceUser], which provides both the [UserId] of the authenticated user and the [MobileServiceAuthenticationToken], as a JSON web token (JWT).</span><span class="sxs-lookup"><span data-stu-id="3df5c-406">The [LoginAsync] method returns a [MobileServiceUser], which provides both the [UserId] of the authenticated user and the [MobileServiceAuthenticationToken], as a JSON web token (JWT).</span></span> <span data-ttu-id="3df5c-407">This token can be cached and reused until it expires.</span><span class="sxs-lookup"><span data-stu-id="3df5c-407">This token can be cached and reused until it expires.</span></span> <span data-ttu-id="3df5c-408">For more information, see [Caching the authentication token](#caching).</span><span class="sxs-lookup"><span data-stu-id="3df5c-408">For more information, see [Caching the authentication token](#caching).</span></span>

### <a name="caching"></a><span data-ttu-id="3df5c-409">Caching the authentication token</span><span class="sxs-lookup"><span data-stu-id="3df5c-409">Caching the authentication token</span></span>
<span data-ttu-id="3df5c-410">In some cases, the call to the login method can be avoided after the first successful authentication by storing the authentication token from the provider.</span><span class="sxs-lookup"><span data-stu-id="3df5c-410">In some cases, the call to the login method can be avoided after the first successful authentication by storing the authentication token from the provider.</span></span>  <span data-ttu-id="3df5c-411">Windows Store and UWP apps can use [PasswordVault] to cache the current authentication token after a successful sign-in, as follows:</span><span class="sxs-lookup"><span data-stu-id="3df5c-411">Windows Store and UWP apps can use [PasswordVault] to cache the current authentication token after a successful sign-in, as follows:</span></span>

```
await client.LoginAsync(MobileServiceAuthenticationProvider.Facebook);

PasswordVault vault = new PasswordVault();
vault.Add(new PasswordCredential("Facebook", client.currentUser.UserId,
    client.currentUser.MobileServiceAuthenticationToken));
```

<span data-ttu-id="3df5c-412">The UserId value is stored as the UserName of the credential and the token is the stored as the Password.</span><span class="sxs-lookup"><span data-stu-id="3df5c-412">The UserId value is stored as the UserName of the credential and the token is the stored as the Password.</span></span> <span data-ttu-id="3df5c-413">On subsequent start-ups, you can check the **PasswordVault** for cached credentials.</span><span class="sxs-lookup"><span data-stu-id="3df5c-413">On subsequent start-ups, you can check the **PasswordVault** for cached credentials.</span></span> <span data-ttu-id="3df5c-414">The following example uses cached credentials when they are found, and otherwise attempts to authenticate again with the backend:</span><span class="sxs-lookup"><span data-stu-id="3df5c-414">The following example uses cached credentials when they are found, and otherwise attempts to authenticate again with the backend:</span></span>

```
// Try to retrieve stored credentials.
var creds = vault.FindAllByResource("Facebook").FirstOrDefault();
if (creds != null)
{
    // Create the current user from the stored credentials.
    client.currentUser = new MobileServiceUser(creds.UserName);
    client.currentUser.MobileServiceAuthenticationToken =
        vault.Retrieve("Facebook", creds.UserName).Password;
}
else
{
    // Regular login flow and cache the token as shown above.
}
```

<span data-ttu-id="3df5c-415">When you sign out a user, you must also remove the stored credential, as follows:</span><span class="sxs-lookup"><span data-stu-id="3df5c-415">When you sign out a user, you must also remove the stored credential, as follows:</span></span>

```
client.Logout();
vault.Remove(vault.Retrieve("Facebook", client.currentUser.UserId));
```

<span data-ttu-id="3df5c-416">Xamarin    apps use the [Xamarin.Auth] APIs to securely store credentials in an **Account** object.</span><span class="sxs-lookup"><span data-stu-id="3df5c-416">Xamarin    apps use the [Xamarin.Auth] APIs to securely store credentials in an **Account** object.</span></span> <span data-ttu-id="3df5c-417">For an example of using these APIs, see the [AuthStore.cs] code file in the [ContosoMoments photo sharing sample](https://github.com/azure-appservice-samples/ContosoMoments).</span><span class="sxs-lookup"><span data-stu-id="3df5c-417">For an example of using these APIs, see the [AuthStore.cs] code file in the [ContosoMoments photo sharing sample](https://github.com/azure-appservice-samples/ContosoMoments).</span></span>

<span data-ttu-id="3df5c-418">When you use client-managed authentication, you can also cache the access token obtained from your provider such as Facebook or Twitter.</span><span class="sxs-lookup"><span data-stu-id="3df5c-418">When you use client-managed authentication, you can also cache the access token obtained from your provider such as Facebook or Twitter.</span></span> <span data-ttu-id="3df5c-419">This token can be supplied to request a new authentication token from the backend, as follows:</span><span class="sxs-lookup"><span data-stu-id="3df5c-419">This token can be supplied to request a new authentication token from the backend, as follows:</span></span>

```
var token = new JObject();
// Replace <your_access_token_value> with actual value of your access token
token.Add("access_token", "<your_access_token_value>");

// Authenticate using the access token.
await client.LoginAsync(MobileServiceAuthenticationProvider.Facebook, token);
```

## <a name="pushnotifications"></a><span data-ttu-id="3df5c-420">Push Notifications</span><span class="sxs-lookup"><span data-stu-id="3df5c-420">Push Notifications</span></span>
<span data-ttu-id="3df5c-421">The following topics cover Push Notifications:</span><span class="sxs-lookup"><span data-stu-id="3df5c-421">The following topics cover Push Notifications:</span></span>

* [<span data-ttu-id="3df5c-422">Register for Push Notifications</span><span class="sxs-lookup"><span data-stu-id="3df5c-422">Register for Push Notifications</span></span>](#register-for-push)
* [<span data-ttu-id="3df5c-423">Obtain a Windows Store package SID</span><span class="sxs-lookup"><span data-stu-id="3df5c-423">Obtain a Windows Store package SID</span></span>](#package-sid)
* [<span data-ttu-id="3df5c-424">Register with Cross-platform templates</span><span class="sxs-lookup"><span data-stu-id="3df5c-424">Register with Cross-platform templates</span></span>](#register-xplat)

### <a name="register-for-push"></a><span data-ttu-id="3df5c-425">How to: Register for Push Notifications</span><span class="sxs-lookup"><span data-stu-id="3df5c-425">How to: Register for Push Notifications</span></span>
<span data-ttu-id="3df5c-426">The Mobile Apps client enables you to register for push notifications with Azure Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="3df5c-426">The Mobile Apps client enables you to register for push notifications with Azure Notification Hubs.</span></span> <span data-ttu-id="3df5c-427">When registering, you obtain a handle that you obtain from the platform-specific Push Notification Service (PNS).</span><span class="sxs-lookup"><span data-stu-id="3df5c-427">When registering, you obtain a handle that you obtain from the platform-specific Push Notification Service (PNS).</span></span> <span data-ttu-id="3df5c-428">You then provide this value along with any tags when you create the registration.</span><span class="sxs-lookup"><span data-stu-id="3df5c-428">You then provide this value along with any tags when you create the registration.</span></span> <span data-ttu-id="3df5c-429">The following code registers your Windows app for push notifications with the Windows Notification Service (WNS):</span><span class="sxs-lookup"><span data-stu-id="3df5c-429">The following code registers your Windows app for push notifications with the Windows Notification Service (WNS):</span></span>

```
private async void InitNotificationsAsync()
{
    // Request a push notification channel.
    var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    // Register for notifications using the new channel.
    await MobileService.GetPush().RegisterNativeAsync(channel.Uri, null);
}
```

<span data-ttu-id="3df5c-430">If you are pushing to WNS, then you MUST [obtain a Windows Store package SID](#package-sid).</span><span class="sxs-lookup"><span data-stu-id="3df5c-430">If you are pushing to WNS, then you MUST [obtain a Windows Store package SID](#package-sid).</span></span>  <span data-ttu-id="3df5c-431">For more information on Windows apps, including how to register for template registrations, see [Add push notifications to your app].</span><span class="sxs-lookup"><span data-stu-id="3df5c-431">For more information on Windows apps, including how to register for template registrations, see [Add push notifications to your app].</span></span>

<span data-ttu-id="3df5c-432">Requesting tags from the client is not supported.</span><span class="sxs-lookup"><span data-stu-id="3df5c-432">Requesting tags from the client is not supported.</span></span>  <span data-ttu-id="3df5c-433">Tag Requests are silently dropped from registration.</span><span class="sxs-lookup"><span data-stu-id="3df5c-433">Tag Requests are silently dropped from registration.</span></span>
<span data-ttu-id="3df5c-434">If you wish to register your device with tags, create a Custom API that uses the Notification Hubs API to perform the registration on your behalf.</span><span class="sxs-lookup"><span data-stu-id="3df5c-434">If you wish to register your device with tags, create a Custom API that uses the Notification Hubs API to perform the registration on your behalf.</span></span>  <span data-ttu-id="3df5c-435">[Call the Custom API](#customapi) instead of the `RegisterNativeAsync()` method.</span><span class="sxs-lookup"><span data-stu-id="3df5c-435">[Call the Custom API](#customapi) instead of the `RegisterNativeAsync()` method.</span></span>

### <a name="package-sid"></a><span data-ttu-id="3df5c-436">How to: Obtain a Windows Store package SID</span><span class="sxs-lookup"><span data-stu-id="3df5c-436">How to: Obtain a Windows Store package SID</span></span>
<span data-ttu-id="3df5c-437">A package SID is needed for enabling push notifications in Windows Store apps.</span><span class="sxs-lookup"><span data-stu-id="3df5c-437">A package SID is needed for enabling push notifications in Windows Store apps.</span></span>  <span data-ttu-id="3df5c-438">To receive a package SID, register your application with the Windows Store.</span><span class="sxs-lookup"><span data-stu-id="3df5c-438">To receive a package SID, register your application with the Windows Store.</span></span>

<span data-ttu-id="3df5c-439">To obtain this value:</span><span class="sxs-lookup"><span data-stu-id="3df5c-439">To obtain this value:</span></span>

1. <span data-ttu-id="3df5c-440">In Visual Studio Solution Explorer, right-click the Windows Store app project, click **Store** > **Associate App with the Store...**.</span><span class="sxs-lookup"><span data-stu-id="3df5c-440">In Visual Studio Solution Explorer, right-click the Windows Store app project, click **Store** > **Associate App with the Store...**.</span></span>
2. <span data-ttu-id="3df5c-441">In the wizard, click **Next**, sign in with your Microsoft account, type a name for your app in **Reserve a new app name**, then click **Reserve**.</span><span class="sxs-lookup"><span data-stu-id="3df5c-441">In the wizard, click **Next**, sign in with your Microsoft account, type a name for your app in **Reserve a new app name**, then click **Reserve**.</span></span>
3. <span data-ttu-id="3df5c-442">After the app registration is successfully created, select the app name, click **Next**, and then click **Associate**.</span><span class="sxs-lookup"><span data-stu-id="3df5c-442">After the app registration is successfully created, select the app name, click **Next**, and then click **Associate**.</span></span>
4. <span data-ttu-id="3df5c-443">Log in to the [Windows Dev Center] using your Microsoft Account.</span><span class="sxs-lookup"><span data-stu-id="3df5c-443">Log in to the [Windows Dev Center] using your Microsoft Account.</span></span> <span data-ttu-id="3df5c-444">Under **My apps**, click the app registration you created.</span><span class="sxs-lookup"><span data-stu-id="3df5c-444">Under **My apps**, click the app registration you created.</span></span>
5. <span data-ttu-id="3df5c-445">Click **App management** > **App identity**, and then scroll down to find your **Package SID**.</span><span class="sxs-lookup"><span data-stu-id="3df5c-445">Click **App management** > **App identity**, and then scroll down to find your **Package SID**.</span></span>

<span data-ttu-id="3df5c-446">Many uses of the package SID treat it as a URI, in which case you need to use *ms-app://* as the scheme.</span><span class="sxs-lookup"><span data-stu-id="3df5c-446">Many uses of the package SID treat it as a URI, in which case you need to use *ms-app://* as the scheme.</span></span> <span data-ttu-id="3df5c-447">Make note of the version of your package SID formed by concatenating this value as a prefix.</span><span class="sxs-lookup"><span data-stu-id="3df5c-447">Make note of the version of your package SID formed by concatenating this value as a prefix.</span></span>

<span data-ttu-id="3df5c-448">Xamarin apps require some additional code to be able to register an app running on the iOS or Android platforms.</span><span class="sxs-lookup"><span data-stu-id="3df5c-448">Xamarin apps require some additional code to be able to register an app running on the iOS or Android platforms.</span></span> <span data-ttu-id="3df5c-449">For more information, see the topic for your platform:</span><span class="sxs-lookup"><span data-stu-id="3df5c-449">For more information, see the topic for your platform:</span></span>

* [<span data-ttu-id="3df5c-450">Xamarin.Android</span><span class="sxs-lookup"><span data-stu-id="3df5c-450">Xamarin.Android</span></span>](app-service-mobile-xamarin-android-get-started-push.md#add-push)
* [<span data-ttu-id="3df5c-451">Xamarin.iOS</span><span class="sxs-lookup"><span data-stu-id="3df5c-451">Xamarin.iOS</span></span>](app-service-mobile-xamarin-ios-get-started-push.md#add-push-notifications-to-your-app)

### <a name="register-xplat"></a><span data-ttu-id="3df5c-452">How to: Register push templates to send cross-platform notifications</span><span class="sxs-lookup"><span data-stu-id="3df5c-452">How to: Register push templates to send cross-platform notifications</span></span>
<span data-ttu-id="3df5c-453">To register templates, use the `RegisterAsync()` method with the templates, as follows:</span><span class="sxs-lookup"><span data-stu-id="3df5c-453">To register templates, use the `RegisterAsync()` method with the templates, as follows:</span></span>

```
JObject templates = myTemplates();
MobileService.GetPush().RegisterAsync(channel.Uri, templates);
```

<span data-ttu-id="3df5c-454">Your templates should be `JObject` types and can contain multiple templates in the following JSON format:</span><span class="sxs-lookup"><span data-stu-id="3df5c-454">Your templates should be `JObject` types and can contain multiple templates in the following JSON format:</span></span>

```
public JObject myTemplates()
{
    // single template for Windows Notification Service toast
    var template = "<toast><visual><binding template=\"ToastText01\"><text id=\"1\">$(message)</text></binding></visual></toast>";

    var templates = new JObject
    {
        ["generic-message"] = new JObject
        {
            ["body"] = template,
            ["headers"] = new JObject
            {
                ["X-WNS-Type"] = "wns/toast"
            },
            ["tags"] = new JArray()
        },
        ["more-templates"] = new JObject {...}
    };
    return templates;
}
```

<span data-ttu-id="3df5c-455">The method **RegisterAsync()** also accepts Secondary Tiles:</span><span class="sxs-lookup"><span data-stu-id="3df5c-455">The method **RegisterAsync()** also accepts Secondary Tiles:</span></span>

```
MobileService.GetPush().RegisterAsync(string channelUri, JObject templates, JObject secondaryTiles);
```

<span data-ttu-id="3df5c-456">All tags are stripped away during registration for security.</span><span class="sxs-lookup"><span data-stu-id="3df5c-456">All tags are stripped away during registration for security.</span></span> <span data-ttu-id="3df5c-457">To add tags to installations or templates within installations, see [Work with the .NET backend server SDK for Azure Mobile Apps].</span><span class="sxs-lookup"><span data-stu-id="3df5c-457">To add tags to installations or templates within installations, see [Work with the .NET backend server SDK for Azure Mobile Apps].</span></span>

<span data-ttu-id="3df5c-458">To send notifications utilizing these registered templates, refer to the [Notification Hubs APIs].</span><span class="sxs-lookup"><span data-stu-id="3df5c-458">To send notifications utilizing these registered templates, refer to the [Notification Hubs APIs].</span></span>

## <a name="misc"></a><span data-ttu-id="3df5c-459">Miscellaneous Topics</span><span class="sxs-lookup"><span data-stu-id="3df5c-459">Miscellaneous Topics</span></span>
### <a name="errors"></a><span data-ttu-id="3df5c-460">How to: Handle errors</span><span class="sxs-lookup"><span data-stu-id="3df5c-460">How to: Handle errors</span></span>
<span data-ttu-id="3df5c-461">When an error occurs in the backend, the client SDK raises a `MobileServiceInvalidOperationException`.</span><span class="sxs-lookup"><span data-stu-id="3df5c-461">When an error occurs in the backend, the client SDK raises a `MobileServiceInvalidOperationException`.</span></span>  <span data-ttu-id="3df5c-462">The following example shows how to handle an exception that is returned by the backend:</span><span class="sxs-lookup"><span data-stu-id="3df5c-462">The following example shows how to handle an exception that is returned by the backend:</span></span>

```
private async void InsertTodoItem(TodoItem todoItem)
{
    // This code inserts a new TodoItem into the database. When the operation completes
    // and App Service has assigned an Id, the item is added to the CollectionView
    try
    {
        await todoTable.InsertAsync(todoItem);
        items.Add(todoItem);
    }
    catch (MobileServiceInvalidOperationException e)
    {
        // Handle error
    }
}
```

<span data-ttu-id="3df5c-463">Another example of dealing with error conditions can be found in the [Mobile Apps Files Sample].</span><span class="sxs-lookup"><span data-stu-id="3df5c-463">Another example of dealing with error conditions can be found in the [Mobile Apps Files Sample].</span></span> <span data-ttu-id="3df5c-464">The [LoggingHandler] example provides a logging delegate handler to log the requests being made to the backend.</span><span class="sxs-lookup"><span data-stu-id="3df5c-464">The [LoggingHandler] example provides a logging delegate handler to log the requests being made to the backend.</span></span>

### <a name="headers"></a><span data-ttu-id="3df5c-465">How to: Customize request headers</span><span class="sxs-lookup"><span data-stu-id="3df5c-465">How to: Customize request headers</span></span>
<span data-ttu-id="3df5c-466">To support your specific app scenario, you might need to customize communication with the Mobile App backend.</span><span class="sxs-lookup"><span data-stu-id="3df5c-466">To support your specific app scenario, you might need to customize communication with the Mobile App backend.</span></span> <span data-ttu-id="3df5c-467">For example, you may want to add a custom header to every outgoing request or even change responses status codes.</span><span class="sxs-lookup"><span data-stu-id="3df5c-467">For example, you may want to add a custom header to every outgoing request or even change responses status codes.</span></span> <span data-ttu-id="3df5c-468">You can use a custom [DelegatingHandler], as in the following example:</span><span class="sxs-lookup"><span data-stu-id="3df5c-468">You can use a custom [DelegatingHandler], as in the following example:</span></span>

```
public async Task CallClientWithHandler()
{
    MobileServiceClient client = new MobileServiceClient("AppUrl", new MyHandler());
    IMobileServiceTable<TodoItem> todoTable = client.GetTable<TodoItem>();
    var newItem = new TodoItem { Text = "Hello world", Complete = false };
    await todoTable.InsertAsync(newItem);
}

public class MyHandler : DelegatingHandler
{
    protected override async Task<HttpResponseMessage>
        SendAsync(HttpRequestMessage request, CancellationToken cancellationToken)
    {
        // Change the request-side here based on the HttpRequestMessage
        request.Headers.Add("x-my-header", "my value");

        // Do the request
        var response = await base.SendAsync(request, cancellationToken);

        // Change the response-side here based on the HttpResponseMessage

        // Return the modified response
        return response;
    }
}
```


<!-- Anchors. -->


<!-- Images. -->

<!-- URLs. -->
[1]: app-service-mobile-windows-store-dotnet-get-started.md
[2]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[3]: app-service-mobile-node-backend-how-to-use-server-sdk.md
[4]: https://msdn.microsoft.com/en-us/library/azure/mt419521(v=azure.10).aspx
[5]: https://github.com/Azure-Samples
[6]: http://www.newtonsoft.com/json/help/html/Properties_T_Newtonsoft_Json_JsonPropertyAttribute.htm
[7]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#define-table-controller
[8]: app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations
[9]: https://www.nuget.org/packages/Microsoft.Azure.Mobile.Client/
[10]: http://www.symbolsource.org/
[11]: http://www.symbolsource.org/Public/Wiki/Using
[12]: https://msdn.microsoft.com/en-us/library/azure/microsoft.windowsazure.mobileservices.mobileserviceclient(v=azure.10).aspx

[Add authentication to your app]: app-service-mobile-windows-store-dotnet-get-started-users.md
[Offline Data Sync in Azure Mobile Apps]: app-service-mobile-offline-data-sync.md
[Add push notifications to your app]: app-service-mobile-windows-store-dotnet-get-started-push.md
[Register your app to use a Microsoft account login]: app-service-mobile-how-to-configure-microsoft-authentication.md
[How to configure App Service for Active Directory login]: app-service-mobile-how-to-configure-active-directory-authentication.md

<!-- Microsoft URLs. -->
[MobileServiceCollection]: https://msdn.microsoft.com/en-us/library/azure/dn250636(v=azure.10).aspx
[MobileServiceIncrementalLoadingCollection]: https://msdn.microsoft.com/en-us/library/azure/dn268408(v=azure.10).aspx
[MobileServiceAuthenticationProvider]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceauthenticationprovider(v=azure.10).aspx
[MobileServiceUser]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser(v=azure.10).aspx
[MobileServiceAuthenticationToken]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser.mobileserviceauthenticationtoken(v=azure.10).aspx
[GetTable]: https://msdn.microsoft.com/en-us/library/azure/jj554275(v=azure.10).aspx
[creates a reference to an untyped table]: https://msdn.microsoft.com/en-us/library/azure/jj554278(v=azure.10).aspx
[DeleteAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296407(v=azure.10).aspx
[IncludeTotalCount]: https://msdn.microsoft.com/en-us/library/azure/dn250560(v=azure.10).aspx
[InsertAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296400(v=azure.10).aspx
[InvokeApiAsync]: https://msdn.microsoft.com/en-us/library/azure/dn268343(v=azure.10).aspx
[LoginAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296411(v=azure.10).aspx
[LookupAsync]: https://msdn.microsoft.com/en-us/library/azure/jj871654(v=azure.10).aspx
[OrderBy]: https://msdn.microsoft.com/en-us/library/azure/dn250572(v=azure.10).aspx
[OrderByDescending]: https://msdn.microsoft.com/en-us/library/azure/dn250568(v=azure.10).aspx
[ReadAsync]: https://msdn.microsoft.com/en-us/library/azure/mt691741(v=azure.10).aspx
[Take]: https://msdn.microsoft.com/en-us/library/azure/dn250574(v=azure.10).aspx
[Select]: https://msdn.microsoft.com/en-us/library/azure/dn250569(v=azure.10).aspx
[Skip]: https://msdn.microsoft.com/en-us/library/azure/dn250573(v=azure.10).aspx
[UpdateAsync]: https://msdn.microsoft.com/en-us/library/azure/dn250536.(v=azure.10)aspx
[UserID]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser.userid(v=azure.10).aspx
[Where]: https://msdn.microsoft.com/en-us/library/azure/dn250579(v=azure.10).aspx
[Azure portal]: https://portal.azure.com/
[Azure classic portal]: https://manage.windowsazure.com/
[EnableQueryAttribute]: https://msdn.microsoft.com/library/system.web.http.odata.enablequeryattribute.aspx
[Guid.NewGuid]: https://msdn.microsoft.com/en-us/library/system.guid.newguid(v=vs.110).aspx
[ISupportIncrementalLoading]: http://msdn.microsoft.com/library/windows/apps/Hh701916.aspx
[Windows Dev Center]: https://dev.windows.com/en-us/overview
[DelegatingHandler]: https://msdn.microsoft.com/library/system.net.http.delegatinghandler(v=vs.110).aspx
[Windows Live SDK]: https://msdn.microsoft.com/en-us/library/bb404787.aspx
[PasswordVault]: http://msdn.microsoft.com/library/windows/apps/windows.security.credentials.passwordvault.aspx
[ProtectedData]: http://msdn.microsoft.com/library/system.security.cryptography.protecteddata%28VS.95%29.aspx
[Notification Hubs APIs]: https://msdn.microsoft.com/library/azure/dn495101.aspx
[Mobile Apps Files Sample]: https://github.com/Azure-Samples/app-service-mobile-dotnet-todo-list-files
[LoggingHandler]: https://github.com/Azure-Samples/app-service-mobile-dotnet-todo-list-files/blob/master/src/client/MobileAppsFilesSample/Helpers/LoggingHandler.cs#L63

<!-- External URLs -->
[OData v3 Documentation]: http://www.odata.org/documentation/odata-version-3-0/
[Fiddler]: http://www.telerik.com/fiddler
[Json.NET]: http://www.newtonsoft.com/json
[Xamarin.Auth]: https://components.xamarin.com/view/xamarin.auth/
[AuthStore.cs]: https://github.com/azure-appservice-samples/ContosoMoments
[ContosoMoments photo sharing sample]: https://github.com/azure-appservice-samples/ContosoMoments
