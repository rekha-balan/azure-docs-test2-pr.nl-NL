---
title: Learn how to secure access to data in DocumentDB | Microsoft Docs
description: Learn about access control concepts in DocumentDB, including master keys, read-only keys, users, and permissions.
services: documentdb
author: mimig1
manager: jhubbard
editor: monicar
documentationcenter: ''
ms.assetid: 8641225d-e839-4ba6-a6fd-d6314ae3a51c
ms.service: documentdb
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: mimig
ms.openlocfilehash: dcbaf2a617e8ff773c305e516977c331e2672537
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553819"
---
# <a name="securing-access-to-documentdb-data"></a><span data-ttu-id="cccfa-103">Securing access to DocumentDB data</span><span class="sxs-lookup"><span data-stu-id="cccfa-103">Securing access to DocumentDB data</span></span>
<span data-ttu-id="cccfa-104">This article provides an overview of securing access to data stored in [Microsoft Azure DocumentDB](https://azure.microsoft.com/services/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="cccfa-104">This article provides an overview of securing access to data stored in [Microsoft Azure DocumentDB](https://azure.microsoft.com/services/documentdb/).</span></span>

<span data-ttu-id="cccfa-105">DocumentDB uses two types of keys to authenticate users and provide access to its data and resources.</span><span class="sxs-lookup"><span data-stu-id="cccfa-105">DocumentDB uses two types of keys to authenticate users and provide access to its data and resources.</span></span> 

|<span data-ttu-id="cccfa-106">Key type</span><span class="sxs-lookup"><span data-stu-id="cccfa-106">Key type</span></span>|<span data-ttu-id="cccfa-107">Resources</span><span class="sxs-lookup"><span data-stu-id="cccfa-107">Resources</span></span>|
|---|---|
|[<span data-ttu-id="cccfa-108">Master keys</span><span class="sxs-lookup"><span data-stu-id="cccfa-108">Master keys</span></span>](#master-keys) |<span data-ttu-id="cccfa-109">Used for administrative resources: database accounts, databases, users, and permissions</span><span class="sxs-lookup"><span data-stu-id="cccfa-109">Used for administrative resources: database accounts, databases, users, and permissions</span></span>|
|[<span data-ttu-id="cccfa-110">Resource tokens</span><span class="sxs-lookup"><span data-stu-id="cccfa-110">Resource tokens</span></span>](#resource-tokens)|<span data-ttu-id="cccfa-111">Used for application resources: collections, documents, attachments, stored procedures, triggers, and UDFs</span><span class="sxs-lookup"><span data-stu-id="cccfa-111">Used for application resources: collections, documents, attachments, stored procedures, triggers, and UDFs</span></span>|

<a id="master-keys"></a>

## <a name="master-keys"></a><span data-ttu-id="cccfa-112">Master keys</span><span class="sxs-lookup"><span data-stu-id="cccfa-112">Master keys</span></span> 

<span data-ttu-id="cccfa-113">Master keys provide access to the all the administrative resources for the database account.</span><span class="sxs-lookup"><span data-stu-id="cccfa-113">Master keys provide access to the all the administrative resources for the database account.</span></span> <span data-ttu-id="cccfa-114">Master keys:</span><span class="sxs-lookup"><span data-stu-id="cccfa-114">Master keys:</span></span>  
- <span data-ttu-id="cccfa-115">Provide access to accounts, databases, users, and permissions.</span><span class="sxs-lookup"><span data-stu-id="cccfa-115">Provide access to accounts, databases, users, and permissions.</span></span> 
- <span data-ttu-id="cccfa-116">Cannot be used to provide granular access to collections and documents.</span><span class="sxs-lookup"><span data-stu-id="cccfa-116">Cannot be used to provide granular access to collections and documents.</span></span>
- <span data-ttu-id="cccfa-117">Are created during the creation of an account.</span><span class="sxs-lookup"><span data-stu-id="cccfa-117">Are created during the creation of an account.</span></span>
- <span data-ttu-id="cccfa-118">Can be regenerated at any time.</span><span class="sxs-lookup"><span data-stu-id="cccfa-118">Can be regenerated at any time.</span></span>

<span data-ttu-id="cccfa-119">Each account consists of two Master keys: a primary key and secondary key.</span><span class="sxs-lookup"><span data-stu-id="cccfa-119">Each account consists of two Master keys: a primary key and secondary key.</span></span> <span data-ttu-id="cccfa-120">The purpose of dual keys is so that you can regenerate, or roll keys, providing continuous access to your account and data.</span><span class="sxs-lookup"><span data-stu-id="cccfa-120">The purpose of dual keys is so that you can regenerate, or roll keys, providing continuous access to your account and data.</span></span> 

<span data-ttu-id="cccfa-121">In addition to the two master keys for the DocumentDB account, there are two read-only keys.</span><span class="sxs-lookup"><span data-stu-id="cccfa-121">In addition to the two master keys for the DocumentDB account, there are two read-only keys.</span></span> <span data-ttu-id="cccfa-122">These read-only keys only allow read operations on the account.</span><span class="sxs-lookup"><span data-stu-id="cccfa-122">These read-only keys only allow read operations on the account.</span></span> <span data-ttu-id="cccfa-123">Read-only keys do not provide access to read permissions resources.</span><span class="sxs-lookup"><span data-stu-id="cccfa-123">Read-only keys do not provide access to read permissions resources.</span></span>

<span data-ttu-id="cccfa-124">Primary, secondary, read only, and read-write master keys can be retrieved and regenerated using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="cccfa-124">Primary, secondary, read only, and read-write master keys can be retrieved and regenerated using the Azure portal.</span></span> <span data-ttu-id="cccfa-125">For instructions, see [View, copy, and regenerate access keys](documentdb-manage-account.md#a-idkeysaview-copy-and-regenerate-access-keys).</span><span class="sxs-lookup"><span data-stu-id="cccfa-125">For instructions, see [View, copy, and regenerate access keys](documentdb-manage-account.md#a-idkeysaview-copy-and-regenerate-access-keys).</span></span>

![Access control (IAM) in the Azure portal - demonstrating NoSQL database security](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-secure-access-to-data/nosql-database-security-master-key-portal.png)

<span data-ttu-id="cccfa-127">The process of rotating your master key is simple.</span><span class="sxs-lookup"><span data-stu-id="cccfa-127">The process of rotating your master key is simple.</span></span> <span data-ttu-id="cccfa-128">Navigate to the Azure portal to retrieve your secondary key, then replace your primary key with your secondary key in your application, then rotate the primary key in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="cccfa-128">Navigate to the Azure portal to retrieve your secondary key, then replace your primary key with your secondary key in your application, then rotate the primary key in the Azure portal.</span></span>

![Master key rotation in the Azure portal - demonstrating NoSQL database security](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-secure-access-to-data/nosql-database-security-master-key-rotate-workflow.png)

### <a name="code-sample-to-use-a-master-key"></a><span data-ttu-id="cccfa-130">Code sample to use a master key</span><span class="sxs-lookup"><span data-stu-id="cccfa-130">Code sample to use a master key</span></span>

<span data-ttu-id="cccfa-131">The following code sample illustrates how to use a DocumentDB account endpoint and master key to instantiate a DocumentClient and create a database.</span><span class="sxs-lookup"><span data-stu-id="cccfa-131">The following code sample illustrates how to use a DocumentDB account endpoint and master key to instantiate a DocumentClient and create a database.</span></span> 

```csharp
//Read the DocumentDB endpointUrl and authorization keys from config.
//These values are available from the Azure portal on the NOSQL (DocumentDB) account blade under "Keys".
//NB > Keep these values in a safe and secure location. Together they provide Administrative access to your DocDB account.

private static readonly string endpointUrl = ConfigurationManager.AppSettings["EndPointUrl"];
private static readonly SecureString authorizationKey = ToSecureString(ConfigurationManager.AppSettings["AuthorizationKey"]);

client = new DocumentClient(new Uri(endpointUrl), authorizationKey);

// Create Database
Database database = await client.CreateDatabaseAsync(
    new Database
    {
        Id = databaseName
    });
```

<a id="resource-tokens"></a>

## <a name="resource-tokens"></a><span data-ttu-id="cccfa-132">Resource tokens</span><span class="sxs-lookup"><span data-stu-id="cccfa-132">Resource tokens</span></span>

<span data-ttu-id="cccfa-133">Resource tokens provide access to the application resources within a database.</span><span class="sxs-lookup"><span data-stu-id="cccfa-133">Resource tokens provide access to the application resources within a database.</span></span> <span data-ttu-id="cccfa-134">Resource tokens:</span><span class="sxs-lookup"><span data-stu-id="cccfa-134">Resource tokens:</span></span>
- <span data-ttu-id="cccfa-135">Provide access to specific collections, partition keys, documents, attachments, stored procedures, triggers, and UDFs.</span><span class="sxs-lookup"><span data-stu-id="cccfa-135">Provide access to specific collections, partition keys, documents, attachments, stored procedures, triggers, and UDFs.</span></span>
- <span data-ttu-id="cccfa-136">Are created when a [user](#users) is granted [permissions](#permissions) to a specific resource.</span><span class="sxs-lookup"><span data-stu-id="cccfa-136">Are created when a [user](#users) is granted [permissions](#permissions) to a specific resource.</span></span>
- <span data-ttu-id="cccfa-137">Are recreated when a permission resource is acted upon on by POST, GET, or PUT call.</span><span class="sxs-lookup"><span data-stu-id="cccfa-137">Are recreated when a permission resource is acted upon on by POST, GET, or PUT call.</span></span>
- <span data-ttu-id="cccfa-138">Use a hash resource token specifically constructed for the user, resource, and permission.</span><span class="sxs-lookup"><span data-stu-id="cccfa-138">Use a hash resource token specifically constructed for the user, resource, and permission.</span></span>
- <span data-ttu-id="cccfa-139">Are time bound with a customizable validity period.</span><span class="sxs-lookup"><span data-stu-id="cccfa-139">Are time bound with a customizable validity period.</span></span> <span data-ttu-id="cccfa-140">The devault valid timespan is one hour.</span><span class="sxs-lookup"><span data-stu-id="cccfa-140">The devault valid timespan is one hour.</span></span> <span data-ttu-id="cccfa-141">Token lifetime, however, may be explicitly specified, up to a maximum of five hours.</span><span class="sxs-lookup"><span data-stu-id="cccfa-141">Token lifetime, however, may be explicitly specified, up to a maximum of five hours.</span></span>
- <span data-ttu-id="cccfa-142">Provide a safe alternative to giving out the master key.</span><span class="sxs-lookup"><span data-stu-id="cccfa-142">Provide a safe alternative to giving out the master key.</span></span> 
- <span data-ttu-id="cccfa-143">Enable clients to read, write, and delete resources in the DocumentDB account according to the permissions they've been granted.</span><span class="sxs-lookup"><span data-stu-id="cccfa-143">Enable clients to read, write, and delete resources in the DocumentDB account according to the permissions they've been granted.</span></span>

<span data-ttu-id="cccfa-144">You can use a resource token (by creating DocumentDB users and permissions) when you want to provide access to resources in your DocumentDB account to a client that cannot be trusted with the master key.</span><span class="sxs-lookup"><span data-stu-id="cccfa-144">You can use a resource token (by creating DocumentDB users and permissions) when you want to provide access to resources in your DocumentDB account to a client that cannot be trusted with the master key.</span></span>  

<span data-ttu-id="cccfa-145">DocumentDB resource tokens provide a safe alternative that enables clients to read, write, and delete resources in your DocumentDB account according to the permissions you've granted, and without need for either a master or read only key.</span><span class="sxs-lookup"><span data-stu-id="cccfa-145">DocumentDB resource tokens provide a safe alternative that enables clients to read, write, and delete resources in your DocumentDB account according to the permissions you've granted, and without need for either a master or read only key.</span></span>

<span data-ttu-id="cccfa-146">Here is a typical design pattern whereby resource tokens may be requested, generated, and delivered to clients:</span><span class="sxs-lookup"><span data-stu-id="cccfa-146">Here is a typical design pattern whereby resource tokens may be requested, generated, and delivered to clients:</span></span>

1. <span data-ttu-id="cccfa-147">A mid-tier service is set up to serve a mobile application to share user photos.</span><span class="sxs-lookup"><span data-stu-id="cccfa-147">A mid-tier service is set up to serve a mobile application to share user photos.</span></span> 
2. <span data-ttu-id="cccfa-148">The mid-tier service possesses the master key of the DocumentDB account.</span><span class="sxs-lookup"><span data-stu-id="cccfa-148">The mid-tier service possesses the master key of the DocumentDB account.</span></span>
3. <span data-ttu-id="cccfa-149">The photo app is installed on end-user mobile devices.</span><span class="sxs-lookup"><span data-stu-id="cccfa-149">The photo app is installed on end-user mobile devices.</span></span> 
4. <span data-ttu-id="cccfa-150">On login, the photo app establishes the identity of the user with the mid-tier service.</span><span class="sxs-lookup"><span data-stu-id="cccfa-150">On login, the photo app establishes the identity of the user with the mid-tier service.</span></span> <span data-ttu-id="cccfa-151">This mechanism of identity establishment is purely up to the application.</span><span class="sxs-lookup"><span data-stu-id="cccfa-151">This mechanism of identity establishment is purely up to the application.</span></span>
5. <span data-ttu-id="cccfa-152">Once the identity is established, the mid-tier service requests permissions based on the identity.</span><span class="sxs-lookup"><span data-stu-id="cccfa-152">Once the identity is established, the mid-tier service requests permissions based on the identity.</span></span>
6. <span data-ttu-id="cccfa-153">The mid-tier service sends a resource token back to the phone app.</span><span class="sxs-lookup"><span data-stu-id="cccfa-153">The mid-tier service sends a resource token back to the phone app.</span></span>
7. <span data-ttu-id="cccfa-154">The phone app can continue to use the resource token to directly access DocumentDB resources with the permissions defined by the resource token and for the interval allowed by the resource token.</span><span class="sxs-lookup"><span data-stu-id="cccfa-154">The phone app can continue to use the resource token to directly access DocumentDB resources with the permissions defined by the resource token and for the interval allowed by the resource token.</span></span> 
8. <span data-ttu-id="cccfa-155">When the resource token expires, subsequent requests receive a 401 unauthorized exception.</span><span class="sxs-lookup"><span data-stu-id="cccfa-155">When the resource token expires, subsequent requests receive a 401 unauthorized exception.</span></span>  <span data-ttu-id="cccfa-156">At this point, the phone app re-establishes the identity and requests a new resource token.</span><span class="sxs-lookup"><span data-stu-id="cccfa-156">At this point, the phone app re-establishes the identity and requests a new resource token.</span></span>

    ![DocumentDB resource tokens workflow](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-secure-access-to-data/resourcekeyworkflow.png)

<span data-ttu-id="cccfa-158">Resource token generation and management is handled by the native DocumentDB client libraries; however, if you use REST you must construct the request/authentication headers.</span><span class="sxs-lookup"><span data-stu-id="cccfa-158">Resource token generation and management is handled by the native DocumentDB client libraries; however, if you use REST you must construct the request/authentication headers.</span></span> <span data-ttu-id="cccfa-159">For more information on creating authentication headers for REST, see [Access Control on DocumentDB Resources](https://docs.microsoft.com/en-us/rest/api/documentdb/access-control-on-documentdb-resources) or the [source code for our SDKs](https://github.com/Azure/azure-documentdb-node/blob/master/source/lib/auth.js).</span><span class="sxs-lookup"><span data-stu-id="cccfa-159">For more information on creating authentication headers for REST, see [Access Control on DocumentDB Resources](https://docs.microsoft.com/en-us/rest/api/documentdb/access-control-on-documentdb-resources) or the [source code for our SDKs](https://github.com/Azure/azure-documentdb-node/blob/master/source/lib/auth.js).</span></span>

<span data-ttu-id="cccfa-160">For an example of a middle tier service used to generate or broker resource tokens, see the [ResourceTokenBroker app](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker/Controllers).</span><span class="sxs-lookup"><span data-stu-id="cccfa-160">For an example of a middle tier service used to generate or broker resource tokens, see the [ResourceTokenBroker app](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker/Controllers).</span></span>

<a id="users"></a>

## <a name="users"></a><span data-ttu-id="cccfa-161">Users</span><span class="sxs-lookup"><span data-stu-id="cccfa-161">Users</span></span>
<span data-ttu-id="cccfa-162">DocumentDB users are associated with a DocumentDB database.</span><span class="sxs-lookup"><span data-stu-id="cccfa-162">DocumentDB users are associated with a DocumentDB database.</span></span>  <span data-ttu-id="cccfa-163">Each database can contain zero or more DocumentDB users.</span><span class="sxs-lookup"><span data-stu-id="cccfa-163">Each database can contain zero or more DocumentDB users.</span></span>  <span data-ttu-id="cccfa-164">The following code sample shows how to create a DocumentDB user resource.</span><span class="sxs-lookup"><span data-stu-id="cccfa-164">The following code sample shows how to create a DocumentDB user resource.</span></span>

```csharp
//Create a user.
User docUser = new User
{
    Id = "mobileuser"
};

docUser = await client.CreateUserAsync(UriFactory.CreateDatabaseUri("db"), docUser);
```

> [!NOTE]
> <span data-ttu-id="cccfa-165">Each DocumentDB user has a PermissionsLink property that can be used to retrieve the list of [permissions](#permissions) associated with the user.</span><span class="sxs-lookup"><span data-stu-id="cccfa-165">Each DocumentDB user has a PermissionsLink property that can be used to retrieve the list of [permissions](#permissions) associated with the user.</span></span>
> 
> 

<a id="permissions"></a>

## <a name="permissions"></a><span data-ttu-id="cccfa-166">Permissions</span><span class="sxs-lookup"><span data-stu-id="cccfa-166">Permissions</span></span>
<span data-ttu-id="cccfa-167">A DocumentDB permission resource is associated with a DocumentDB user.</span><span class="sxs-lookup"><span data-stu-id="cccfa-167">A DocumentDB permission resource is associated with a DocumentDB user.</span></span>  <span data-ttu-id="cccfa-168">Each user may contain zero or more DocumentDB permissions.</span><span class="sxs-lookup"><span data-stu-id="cccfa-168">Each user may contain zero or more DocumentDB permissions.</span></span>  <span data-ttu-id="cccfa-169">A permission resource provides access to a security token that the user needs when trying to access a specific application resource.</span><span class="sxs-lookup"><span data-stu-id="cccfa-169">A permission resource provides access to a security token that the user needs when trying to access a specific application resource.</span></span>
<span data-ttu-id="cccfa-170">There are two available access levels that may be provided by a permission resource:</span><span class="sxs-lookup"><span data-stu-id="cccfa-170">There are two available access levels that may be provided by a permission resource:</span></span>

* <span data-ttu-id="cccfa-171">All: The user has full permission on the resource.</span><span class="sxs-lookup"><span data-stu-id="cccfa-171">All: The user has full permission on the resource.</span></span>
* <span data-ttu-id="cccfa-172">Read: The user can only read the contents of the resource but cannot perform write, update, or delete operations on the resource.</span><span class="sxs-lookup"><span data-stu-id="cccfa-172">Read: The user can only read the contents of the resource but cannot perform write, update, or delete operations on the resource.</span></span>

> [!NOTE]
> <span data-ttu-id="cccfa-173">In order to run DocumentDB stored procedures the user must have the All permission on the collection in which the stored procedure will be run.</span><span class="sxs-lookup"><span data-stu-id="cccfa-173">In order to run DocumentDB stored procedures the user must have the All permission on the collection in which the stored procedure will be run.</span></span>
> 
> 

### <a name="code-sample-to-create-permission"></a><span data-ttu-id="cccfa-174">Code sample to create permission</span><span class="sxs-lookup"><span data-stu-id="cccfa-174">Code sample to create permission</span></span>

<span data-ttu-id="cccfa-175">The following code sample shows how to create a permission resource, read the resource token of the permission resource, and associate the permissions with the [user](#users) created above.</span><span class="sxs-lookup"><span data-stu-id="cccfa-175">The following code sample shows how to create a permission resource, read the resource token of the permission resource, and associate the permissions with the [user](#users) created above.</span></span>

```csharp
// Create a permission.
Permission docPermission = new Permission
{
    PermissionMode = PermissionMode.Read,
    ResourceLink = documentCollection.SelfLink,
    Id = "readperm"
};
  
docPermission = await client.CreatePermissionAsync(UriFactory.CreateUserUri("db", "user"), docPermission);
Console.WriteLine(docPermission.Id + " has token of: " + docPermission.Token);
```

<span data-ttu-id="cccfa-176">If you have specified a partition key for your collection, then the permission for collection, document, and attachment resources must also include the ResourcePartitionKey in addition to the ResourceLink.</span><span class="sxs-lookup"><span data-stu-id="cccfa-176">If you have specified a partition key for your collection, then the permission for collection, document, and attachment resources must also include the ResourcePartitionKey in addition to the ResourceLink.</span></span>

### <a name="code-sample-to-read-permissions-for-user"></a><span data-ttu-id="cccfa-177">Code sample to read permissions for user</span><span class="sxs-lookup"><span data-stu-id="cccfa-177">Code sample to read permissions for user</span></span>

<span data-ttu-id="cccfa-178">To easily obtain all permission resources associated with a particular user, DocumentDB makes available a permission feed for each user object.</span><span class="sxs-lookup"><span data-stu-id="cccfa-178">To easily obtain all permission resources associated with a particular user, DocumentDB makes available a permission feed for each user object.</span></span>  <span data-ttu-id="cccfa-179">The following code snippet shows how to retrieve the permission associated with the user created above, construct a permission list, and instantiate a new DocumentClient on behalf of the user.</span><span class="sxs-lookup"><span data-stu-id="cccfa-179">The following code snippet shows how to retrieve the permission associated with the user created above, construct a permission list, and instantiate a new DocumentClient on behalf of the user.</span></span>

```csharp
//Read a permission feed.
FeedResponse<Permission> permFeed = await client.ReadPermissionFeedAsync(
  UriFactory.CreateUserUri("db", "myUser"));
 List<Permission> permList = new List<Permission>();

foreach (Permission perm in permFeed)
{
    permList.Add(perm);
}

DocumentClient userClient = new DocumentClient(new Uri(endpointUrl), permList);
```

## <a name="next-steps"></a><span data-ttu-id="cccfa-180">Next steps</span><span class="sxs-lookup"><span data-stu-id="cccfa-180">Next steps</span></span>
* <span data-ttu-id="cccfa-181">To learn more about DocumentDB database security, see [DocumentDB: NoSQL database security](documentdb-nosql-database-security.md).</span><span class="sxs-lookup"><span data-stu-id="cccfa-181">To learn more about DocumentDB database security, see [DocumentDB: NoSQL database security](documentdb-nosql-database-security.md).</span></span>
* <span data-ttu-id="cccfa-182">To learn about managing master and read-only keys, see [How to manage a DocumentDB account](documentdb-manage-account.md#a-idkeysaview-copy-and-regenerate-access-keys).</span><span class="sxs-lookup"><span data-stu-id="cccfa-182">To learn about managing master and read-only keys, see [How to manage a DocumentDB account](documentdb-manage-account.md#a-idkeysaview-copy-and-regenerate-access-keys).</span></span>
* <span data-ttu-id="cccfa-183">To learn how to construct DocumentDB authorization tokens, see [Access Control on DocumentDB Resources](https://docs.microsoft.com/en-us/rest/api/documentdb/access-control-on-documentdb-resources).</span><span class="sxs-lookup"><span data-stu-id="cccfa-183">To learn how to construct DocumentDB authorization tokens, see [Access Control on DocumentDB Resources](https://docs.microsoft.com/en-us/rest/api/documentdb/access-control-on-documentdb-resources).</span></span>



