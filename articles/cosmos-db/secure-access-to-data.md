---
title: Learn how to secure access to data in Azure Cosmos DB | Microsoft Docs
description: Learn about access control concepts in Azure Cosmos DB, including master keys, read-only keys, users, and permissions.
services: cosmos-db
author: rafats
manager: kfile
ms.service: cosmos-db
ms.devlang: na
ms.topic: conceptual
ms.date: 08/19/2018
ms.author: rafats
ms.openlocfilehash: cfd1160d1592c03eea94e3c4d04fdc5754eca671
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966476"
---
# <a name="securing-access-to-azure-cosmos-db-data"></a><span data-ttu-id="ffb8b-103">Securing access to Azure Cosmos DB data</span><span class="sxs-lookup"><span data-stu-id="ffb8b-103">Securing access to Azure Cosmos DB data</span></span>
<span data-ttu-id="ffb8b-104">This article provides an overview of securing access to data stored in [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="ffb8b-104">This article provides an overview of securing access to data stored in [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span></span>

<span data-ttu-id="ffb8b-105">Azure Cosmos DB uses two types of keys to authenticate users and provide access to its data and resources.</span><span class="sxs-lookup"><span data-stu-id="ffb8b-105">Azure Cosmos DB uses two types of keys to authenticate users and provide access to its data and resources.</span></span> 

|<span data-ttu-id="ffb8b-106">Key type</span><span class="sxs-lookup"><span data-stu-id="ffb8b-106">Key type</span></span>|<span data-ttu-id="ffb8b-107">Resources</span><span class="sxs-lookup"><span data-stu-id="ffb8b-107">Resources</span></span>|
|---|---|
|[<span data-ttu-id="ffb8b-108">Master keys</span><span class="sxs-lookup"><span data-stu-id="ffb8b-108">Master keys</span></span>](#master-keys) |<span data-ttu-id="ffb8b-109">Used for administrative resources: database accounts, databases, users, and permissions</span><span class="sxs-lookup"><span data-stu-id="ffb8b-109">Used for administrative resources: database accounts, databases, users, and permissions</span></span>|
|[<span data-ttu-id="ffb8b-110">Resource tokens</span><span class="sxs-lookup"><span data-stu-id="ffb8b-110">Resource tokens</span></span>](#resource-tokens)|<span data-ttu-id="ffb8b-111">Used for application resources: containers, documents, attachments, stored procedures, triggers, and UDFs</span><span class="sxs-lookup"><span data-stu-id="ffb8b-111">Used for application resources: containers, documents, attachments, stored procedures, triggers, and UDFs</span></span>|

<a id="master-keys"></a>

## <a name="master-keys"></a><span data-ttu-id="ffb8b-112">Master keys</span><span class="sxs-lookup"><span data-stu-id="ffb8b-112">Master keys</span></span> 

<span data-ttu-id="ffb8b-113">Master keys provide access to the all the administrative resources for the database account.</span><span class="sxs-lookup"><span data-stu-id="ffb8b-113">Master keys provide access to the all the administrative resources for the database account.</span></span> <span data-ttu-id="ffb8b-114">Master keys:</span><span class="sxs-lookup"><span data-stu-id="ffb8b-114">Master keys:</span></span>  
- <span data-ttu-id="ffb8b-115">Provide access to accounts, databases, users, and permissions.</span><span class="sxs-lookup"><span data-stu-id="ffb8b-115">Provide access to accounts, databases, users, and permissions.</span></span> 
- <span data-ttu-id="ffb8b-116">Cannot be used to provide granular access to containers and documents.</span><span class="sxs-lookup"><span data-stu-id="ffb8b-116">Cannot be used to provide granular access to containers and documents.</span></span>
- <span data-ttu-id="ffb8b-117">Are created during the creation of an account.</span><span class="sxs-lookup"><span data-stu-id="ffb8b-117">Are created during the creation of an account.</span></span>
- <span data-ttu-id="ffb8b-118">Can be regenerated at any time.</span><span class="sxs-lookup"><span data-stu-id="ffb8b-118">Can be regenerated at any time.</span></span>

<span data-ttu-id="ffb8b-119">Each account consists of two Master keys: a primary key and secondary key.</span><span class="sxs-lookup"><span data-stu-id="ffb8b-119">Each account consists of two Master keys: a primary key and secondary key.</span></span> <span data-ttu-id="ffb8b-120">The purpose of dual keys is so that you can regenerate, or roll keys, providing continuous access to your account and data.</span><span class="sxs-lookup"><span data-stu-id="ffb8b-120">The purpose of dual keys is so that you can regenerate, or roll keys, providing continuous access to your account and data.</span></span> 

<span data-ttu-id="ffb8b-121">In addition to the two master keys for the Cosmos DB account, there are two read-only keys.</span><span class="sxs-lookup"><span data-stu-id="ffb8b-121">In addition to the two master keys for the Cosmos DB account, there are two read-only keys.</span></span> <span data-ttu-id="ffb8b-122">These read-only keys only allow read operations on the account.</span><span class="sxs-lookup"><span data-stu-id="ffb8b-122">These read-only keys only allow read operations on the account.</span></span> <span data-ttu-id="ffb8b-123">Read-only keys do not provide access to read permissions resources.</span><span class="sxs-lookup"><span data-stu-id="ffb8b-123">Read-only keys do not provide access to read permissions resources.</span></span>

<span data-ttu-id="ffb8b-124">Primary, secondary, read only, and read-write master keys can be retrieved and regenerated using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="ffb8b-124">Primary, secondary, read only, and read-write master keys can be retrieved and regenerated using the Azure portal.</span></span> <span data-ttu-id="ffb8b-125">For instructions, see [View, copy, and regenerate access keys](manage-account.md#keys).</span><span class="sxs-lookup"><span data-stu-id="ffb8b-125">For instructions, see [View, copy, and regenerate access keys](manage-account.md#keys).</span></span>

![Access control (IAM) in the Azure portal - demonstrating NoSQL database security](./media/secure-access-to-data/nosql-database-security-master-key-portal.png)

<span data-ttu-id="ffb8b-127">The process of rotating your master key is simple.</span><span class="sxs-lookup"><span data-stu-id="ffb8b-127">The process of rotating your master key is simple.</span></span> <span data-ttu-id="ffb8b-128">Navigate to the Azure portal to retrieve your secondary key, then replace your primary key with your secondary key in your application, then rotate the primary key in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="ffb8b-128">Navigate to the Azure portal to retrieve your secondary key, then replace your primary key with your secondary key in your application, then rotate the primary key in the Azure portal.</span></span>

![Master key rotation in the Azure portal - demonstrating NoSQL database security](./media/secure-access-to-data/nosql-database-security-master-key-rotate-workflow.png)

### <a name="code-sample-to-use-a-master-key"></a><span data-ttu-id="ffb8b-130">Code sample to use a master key</span><span class="sxs-lookup"><span data-stu-id="ffb8b-130">Code sample to use a master key</span></span>

<span data-ttu-id="ffb8b-131">The following code sample illustrates how to use a Cosmos DB account endpoint and master key to instantiate a DocumentClient and create a database.</span><span class="sxs-lookup"><span data-stu-id="ffb8b-131">The following code sample illustrates how to use a Cosmos DB account endpoint and master key to instantiate a DocumentClient and create a database.</span></span> 

```csharp
//Read the Azure Cosmos DB endpointUrl and authorization keys from config.
//These values are available from the Azure portal on the Azure Cosmos DB account blade under "Keys".
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

## <a name="resource-tokens"></a><span data-ttu-id="ffb8b-132">Resource tokens</span><span class="sxs-lookup"><span data-stu-id="ffb8b-132">Resource tokens</span></span>

<span data-ttu-id="ffb8b-133">Resource tokens provide access to the application resources within a database.</span><span class="sxs-lookup"><span data-stu-id="ffb8b-133">Resource tokens provide access to the application resources within a database.</span></span> <span data-ttu-id="ffb8b-134">Resource tokens:</span><span class="sxs-lookup"><span data-stu-id="ffb8b-134">Resource tokens:</span></span>
- <span data-ttu-id="ffb8b-135">Provide access to specific containers, partition keys, documents, attachments, stored procedures, triggers, and UDFs.</span><span class="sxs-lookup"><span data-stu-id="ffb8b-135">Provide access to specific containers, partition keys, documents, attachments, stored procedures, triggers, and UDFs.</span></span>
- <span data-ttu-id="ffb8b-136">Are created when a [user](#users) is granted [permissions](#permissions) to a specific resource.</span><span class="sxs-lookup"><span data-stu-id="ffb8b-136">Are created when a [user](#users) is granted [permissions](#permissions) to a specific resource.</span></span>
- <span data-ttu-id="ffb8b-137">Are recreated when a permission resource is acted upon on by POST, GET, or PUT call.</span><span class="sxs-lookup"><span data-stu-id="ffb8b-137">Are recreated when a permission resource is acted upon on by POST, GET, or PUT call.</span></span>
- <span data-ttu-id="ffb8b-138">Use a hash resource token specifically constructed for the user, resource, and permission.</span><span class="sxs-lookup"><span data-stu-id="ffb8b-138">Use a hash resource token specifically constructed for the user, resource, and permission.</span></span>
- <span data-ttu-id="ffb8b-139">Are time bound with a customizable validity period.</span><span class="sxs-lookup"><span data-stu-id="ffb8b-139">Are time bound with a customizable validity period.</span></span> <span data-ttu-id="ffb8b-140">The default valid timespan is one hour.</span><span class="sxs-lookup"><span data-stu-id="ffb8b-140">The default valid timespan is one hour.</span></span> <span data-ttu-id="ffb8b-141">Token lifetime, however, may be explicitly specified, up to a maximum of five hours.</span><span class="sxs-lookup"><span data-stu-id="ffb8b-141">Token lifetime, however, may be explicitly specified, up to a maximum of five hours.</span></span>
- <span data-ttu-id="ffb8b-142">Provide a safe alternative to giving out the master key.</span><span class="sxs-lookup"><span data-stu-id="ffb8b-142">Provide a safe alternative to giving out the master key.</span></span> 
- <span data-ttu-id="ffb8b-143">Enable clients to read, write, and delete resources in the Cosmos DB account according to the permissions they've been granted.</span><span class="sxs-lookup"><span data-stu-id="ffb8b-143">Enable clients to read, write, and delete resources in the Cosmos DB account according to the permissions they've been granted.</span></span>

<span data-ttu-id="ffb8b-144">You can use a resource token (by creating Cosmos DB users and permissions) when you want to provide access to resources in your Cosmos DB account to a client that cannot be trusted with the master key.</span><span class="sxs-lookup"><span data-stu-id="ffb8b-144">You can use a resource token (by creating Cosmos DB users and permissions) when you want to provide access to resources in your Cosmos DB account to a client that cannot be trusted with the master key.</span></span>  

<span data-ttu-id="ffb8b-145">Cosmos DB resource tokens provide a safe alternative that enables clients to read, write, and delete resources in your Cosmos DB account according to the permissions you've granted, and without need for either a master or read only key.</span><span class="sxs-lookup"><span data-stu-id="ffb8b-145">Cosmos DB resource tokens provide a safe alternative that enables clients to read, write, and delete resources in your Cosmos DB account according to the permissions you've granted, and without need for either a master or read only key.</span></span>

<span data-ttu-id="ffb8b-146">Here is a typical design pattern whereby resource tokens may be requested, generated, and delivered to clients:</span><span class="sxs-lookup"><span data-stu-id="ffb8b-146">Here is a typical design pattern whereby resource tokens may be requested, generated, and delivered to clients:</span></span>

1. <span data-ttu-id="ffb8b-147">A mid-tier service is set up to serve a mobile application to share user photos.</span><span class="sxs-lookup"><span data-stu-id="ffb8b-147">A mid-tier service is set up to serve a mobile application to share user photos.</span></span> 
2. <span data-ttu-id="ffb8b-148">The mid-tier service possesses the master key of the Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="ffb8b-148">The mid-tier service possesses the master key of the Cosmos DB account.</span></span>
3. <span data-ttu-id="ffb8b-149">The photo app is installed on end-user mobile devices.</span><span class="sxs-lookup"><span data-stu-id="ffb8b-149">The photo app is installed on end-user mobile devices.</span></span> 
4. <span data-ttu-id="ffb8b-150">On login, the photo app establishes the identity of the user with the mid-tier service.</span><span class="sxs-lookup"><span data-stu-id="ffb8b-150">On login, the photo app establishes the identity of the user with the mid-tier service.</span></span> <span data-ttu-id="ffb8b-151">This mechanism of identity establishment is purely up to the application.</span><span class="sxs-lookup"><span data-stu-id="ffb8b-151">This mechanism of identity establishment is purely up to the application.</span></span>
5. <span data-ttu-id="ffb8b-152">Once the identity is established, the mid-tier service requests permissions based on the identity.</span><span class="sxs-lookup"><span data-stu-id="ffb8b-152">Once the identity is established, the mid-tier service requests permissions based on the identity.</span></span>
6. <span data-ttu-id="ffb8b-153">The mid-tier service sends a resource token back to the phone app.</span><span class="sxs-lookup"><span data-stu-id="ffb8b-153">The mid-tier service sends a resource token back to the phone app.</span></span>
7. <span data-ttu-id="ffb8b-154">The phone app can continue to use the resource token to directly access Cosmos DB resources with the permissions defined by the resource token and for the interval allowed by the resource token.</span><span class="sxs-lookup"><span data-stu-id="ffb8b-154">The phone app can continue to use the resource token to directly access Cosmos DB resources with the permissions defined by the resource token and for the interval allowed by the resource token.</span></span> 
8. <span data-ttu-id="ffb8b-155">When the resource token expires, subsequent requests receive a 401 unauthorized exception.</span><span class="sxs-lookup"><span data-stu-id="ffb8b-155">When the resource token expires, subsequent requests receive a 401 unauthorized exception.</span></span>  <span data-ttu-id="ffb8b-156">At this point, the phone app re-establishes the identity and requests a new resource token.</span><span class="sxs-lookup"><span data-stu-id="ffb8b-156">At this point, the phone app re-establishes the identity and requests a new resource token.</span></span>

    ![Azure Cosmos DB resource tokens workflow](./media/secure-access-to-data/resourcekeyworkflow.png)

<span data-ttu-id="ffb8b-158">Resource token generation and management is handled by the native Cosmos DB client libraries; however, if you use REST you must construct the request/authentication headers.</span><span class="sxs-lookup"><span data-stu-id="ffb8b-158">Resource token generation and management is handled by the native Cosmos DB client libraries; however, if you use REST you must construct the request/authentication headers.</span></span> <span data-ttu-id="ffb8b-159">For more information on creating authentication headers for REST, see [Access Control on Cosmos DB Resources](https://docs.microsoft.com/rest/api/cosmos-db/access-control-on-cosmosdb-resources) or the [source code for our SDKs](https://github.com/Azure/azure-documentdb-node/blob/master/source/lib/auth.js).</span><span class="sxs-lookup"><span data-stu-id="ffb8b-159">For more information on creating authentication headers for REST, see [Access Control on Cosmos DB Resources](https://docs.microsoft.com/rest/api/cosmos-db/access-control-on-cosmosdb-resources) or the [source code for our SDKs](https://github.com/Azure/azure-documentdb-node/blob/master/source/lib/auth.js).</span></span>

<span data-ttu-id="ffb8b-160">For an example of a middle tier service used to generate or broker resource tokens, see the [ResourceTokenBroker app](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker/Controllers).</span><span class="sxs-lookup"><span data-stu-id="ffb8b-160">For an example of a middle tier service used to generate or broker resource tokens, see the [ResourceTokenBroker app](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker/Controllers).</span></span>

<a id="users"></a>

## <a name="users"></a><span data-ttu-id="ffb8b-161">Users</span><span class="sxs-lookup"><span data-stu-id="ffb8b-161">Users</span></span>
<span data-ttu-id="ffb8b-162">Cosmos DB users are associated with a Cosmos DB database.</span><span class="sxs-lookup"><span data-stu-id="ffb8b-162">Cosmos DB users are associated with a Cosmos DB database.</span></span>  <span data-ttu-id="ffb8b-163">Each database can contain zero or more Cosmos DB users.</span><span class="sxs-lookup"><span data-stu-id="ffb8b-163">Each database can contain zero or more Cosmos DB users.</span></span>  <span data-ttu-id="ffb8b-164">The following code sample shows how to create a Cosmos DB user resource.</span><span class="sxs-lookup"><span data-stu-id="ffb8b-164">The following code sample shows how to create a Cosmos DB user resource.</span></span>

```csharp
//Create a user.
User docUser = new User
{
    Id = "mobileuser"
};

docUser = await client.CreateUserAsync(UriFactory.CreateDatabaseUri("db"), docUser);
```

> [!NOTE]
> <span data-ttu-id="ffb8b-165">Each Cosmos DB user has a PermissionsLink property that can be used to retrieve the list of [permissions](#permissions) associated with the user.</span><span class="sxs-lookup"><span data-stu-id="ffb8b-165">Each Cosmos DB user has a PermissionsLink property that can be used to retrieve the list of [permissions](#permissions) associated with the user.</span></span>
> 
> 

<a id="permissions"></a>

## <a name="permissions"></a><span data-ttu-id="ffb8b-166">Permissions</span><span class="sxs-lookup"><span data-stu-id="ffb8b-166">Permissions</span></span>
<span data-ttu-id="ffb8b-167">A Cosmos DB permission resource is associated with a Cosmos DB user.</span><span class="sxs-lookup"><span data-stu-id="ffb8b-167">A Cosmos DB permission resource is associated with a Cosmos DB user.</span></span>  <span data-ttu-id="ffb8b-168">Each user may contain zero or more Cosmos DB permissions.</span><span class="sxs-lookup"><span data-stu-id="ffb8b-168">Each user may contain zero or more Cosmos DB permissions.</span></span>  <span data-ttu-id="ffb8b-169">A permission resource provides access to a security token that the user needs when trying to access a specific application resource.</span><span class="sxs-lookup"><span data-stu-id="ffb8b-169">A permission resource provides access to a security token that the user needs when trying to access a specific application resource.</span></span>
<span data-ttu-id="ffb8b-170">There are two available access levels that may be provided by a permission resource:</span><span class="sxs-lookup"><span data-stu-id="ffb8b-170">There are two available access levels that may be provided by a permission resource:</span></span>

* <span data-ttu-id="ffb8b-171">All: The user has full permission on the resource.</span><span class="sxs-lookup"><span data-stu-id="ffb8b-171">All: The user has full permission on the resource.</span></span>
* <span data-ttu-id="ffb8b-172">Read: The user can only read the contents of the resource but cannot perform write, update, or delete operations on the resource.</span><span class="sxs-lookup"><span data-stu-id="ffb8b-172">Read: The user can only read the contents of the resource but cannot perform write, update, or delete operations on the resource.</span></span>

> [!NOTE]
> <span data-ttu-id="ffb8b-173">In order to run Cosmos DB stored procedures the user must have the All permission on the container in which the stored procedure will be run.</span><span class="sxs-lookup"><span data-stu-id="ffb8b-173">In order to run Cosmos DB stored procedures the user must have the All permission on the container in which the stored procedure will be run.</span></span>
> 
> 

### <a name="code-sample-to-create-permission"></a><span data-ttu-id="ffb8b-174">Code sample to create permission</span><span class="sxs-lookup"><span data-stu-id="ffb8b-174">Code sample to create permission</span></span>

<span data-ttu-id="ffb8b-175">The following code sample shows how to create a permission resource, read the resource token of the permission resource, and associate the permissions with the [user](#users) created above.</span><span class="sxs-lookup"><span data-stu-id="ffb8b-175">The following code sample shows how to create a permission resource, read the resource token of the permission resource, and associate the permissions with the [user](#users) created above.</span></span>

```csharp
// Create a permission.
Permission docPermission = new Permission
{
    PermissionMode = PermissionMode.Read,
    ResourceLink = UriFactory.CreateDocumentCollectionUri("db", "collection"),
    Id = "readperm"
};
  
docPermission = await client.CreatePermissionAsync(UriFactory.CreateUserUri("db", "user"), docPermission);
Console.WriteLine(docPermission.Id + " has token of: " + docPermission.Token);
```

<span data-ttu-id="ffb8b-176">If you have specified a partition key for your collection, then the permission for collection, document, and attachment resources must also include the ResourcePartitionKey in addition to the ResourceLink.</span><span class="sxs-lookup"><span data-stu-id="ffb8b-176">If you have specified a partition key for your collection, then the permission for collection, document, and attachment resources must also include the ResourcePartitionKey in addition to the ResourceLink.</span></span>

### <a name="code-sample-to-read-permissions-for-user"></a><span data-ttu-id="ffb8b-177">Code sample to read permissions for user</span><span class="sxs-lookup"><span data-stu-id="ffb8b-177">Code sample to read permissions for user</span></span>

<span data-ttu-id="ffb8b-178">To easily obtain all permission resources associated with a particular user, Cosmos DB makes available a permission feed for each user object.</span><span class="sxs-lookup"><span data-stu-id="ffb8b-178">To easily obtain all permission resources associated with a particular user, Cosmos DB makes available a permission feed for each user object.</span></span>  <span data-ttu-id="ffb8b-179">The following code snippet shows how to retrieve the permission associated with the user created above, construct a permission list, and instantiate a new DocumentClient on behalf of the user.</span><span class="sxs-lookup"><span data-stu-id="ffb8b-179">The following code snippet shows how to retrieve the permission associated with the user created above, construct a permission list, and instantiate a new DocumentClient on behalf of the user.</span></span>

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

## <a name="add-users-and-assign-roles"></a><span data-ttu-id="ffb8b-180">Add users and assign roles</span><span class="sxs-lookup"><span data-stu-id="ffb8b-180">Add users and assign roles</span></span>

<span data-ttu-id="ffb8b-181">To add Azure Cosmos DB account reader access to your user account, have a subscription owner perform the following steps in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="ffb8b-181">To add Azure Cosmos DB account reader access to your user account, have a subscription owner perform the following steps in the Azure portal.</span></span>

1. <span data-ttu-id="ffb8b-182">Open the Azure portal, and select your Azure Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="ffb8b-182">Open the Azure portal, and select your Azure Cosmos DB account.</span></span>
2. <span data-ttu-id="ffb8b-183">Click the **Access control (IAM)** tab, and then click  **+ Add**.</span><span class="sxs-lookup"><span data-stu-id="ffb8b-183">Click the **Access control (IAM)** tab, and then click  **+ Add**.</span></span>
3. <span data-ttu-id="ffb8b-184">In the **Add permissions** pane, in the **Role** box, select **Cosmos DB Account Reader Role**.</span><span class="sxs-lookup"><span data-stu-id="ffb8b-184">In the **Add permissions** pane, in the **Role** box, select **Cosmos DB Account Reader Role**.</span></span>
4. <span data-ttu-id="ffb8b-185">In the **Assign access to box**, select **Azure AD user, group, or application**.</span><span class="sxs-lookup"><span data-stu-id="ffb8b-185">In the **Assign access to box**, select **Azure AD user, group, or application**.</span></span>
5. <span data-ttu-id="ffb8b-186">Select the user, group, or application in your directory to which you wish to grant access.</span><span class="sxs-lookup"><span data-stu-id="ffb8b-186">Select the user, group, or application in your directory to which you wish to grant access.</span></span>  <span data-ttu-id="ffb8b-187">You can search the directory by display name, email address, or object identifiers.</span><span class="sxs-lookup"><span data-stu-id="ffb8b-187">You can search the directory by display name, email address, or object identifiers.</span></span>
    <span data-ttu-id="ffb8b-188">The selected user, group, or application appears in the selected members list.</span><span class="sxs-lookup"><span data-stu-id="ffb8b-188">The selected user, group, or application appears in the selected members list.</span></span>
6. <span data-ttu-id="ffb8b-189">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="ffb8b-189">Click **Save**.</span></span>

<span data-ttu-id="ffb8b-190">The entity can now read Azure Cosmos DB resources.</span><span class="sxs-lookup"><span data-stu-id="ffb8b-190">The entity can now read Azure Cosmos DB resources.</span></span>

## <a name="delete-or-export-user-data"></a><span data-ttu-id="ffb8b-191">Delete or export user data</span><span class="sxs-lookup"><span data-stu-id="ffb8b-191">Delete or export user data</span></span>
<span data-ttu-id="ffb8b-192">Azure Cosmos DB enables you to search, select, modify and delete any personal data located in database or collections.</span><span class="sxs-lookup"><span data-stu-id="ffb8b-192">Azure Cosmos DB enables you to search, select, modify and delete any personal data located in database or collections.</span></span> <span data-ttu-id="ffb8b-193">Azure Cosmos DB provides APIs to find and delete personal data however, it’s your responsibility to use the APIs and define logic required to erase the personal data.</span><span class="sxs-lookup"><span data-stu-id="ffb8b-193">Azure Cosmos DB provides APIs to find and delete personal data however, it’s your responsibility to use the APIs and define logic required to erase the personal data.</span></span> <span data-ttu-id="ffb8b-194">Each multi-model API (SQL API, MongoDB API, Gremlin API, Cassandra API, Table API) provides different language SDKs that contain methods to search and delete personal data.</span><span class="sxs-lookup"><span data-stu-id="ffb8b-194">Each multi-model API (SQL API, MongoDB API, Gremlin API, Cassandra API, Table API) provides different language SDKs that contain methods to search and delete personal data.</span></span> <span data-ttu-id="ffb8b-195">You can also enable the [time to live (TTL)](time-to-live.md) feature to delete data automatically after a specified period, without incurring any additional cost.</span><span class="sxs-lookup"><span data-stu-id="ffb8b-195">You can also enable the [time to live (TTL)](time-to-live.md) feature to delete data automatically after a specified period, without incurring any additional cost.</span></span>

[!INCLUDE [GDPR-related guidance](../../includes/gdpr-dsr-and-stp-note.md)]

## <a name="next-steps"></a><span data-ttu-id="ffb8b-196">Next steps</span><span class="sxs-lookup"><span data-stu-id="ffb8b-196">Next steps</span></span>
* <span data-ttu-id="ffb8b-197">To learn more about Cosmos DB database security, see [Cosmos DB: Database security](database-security.md).</span><span class="sxs-lookup"><span data-stu-id="ffb8b-197">To learn more about Cosmos DB database security, see [Cosmos DB: Database security](database-security.md).</span></span>
* <span data-ttu-id="ffb8b-198">To learn about managing master and read-only keys, see [How to manage an Azure Cosmos DB account](manage-account.md#keys).</span><span class="sxs-lookup"><span data-stu-id="ffb8b-198">To learn about managing master and read-only keys, see [How to manage an Azure Cosmos DB account](manage-account.md#keys).</span></span>
* <span data-ttu-id="ffb8b-199">To learn how to construct Azure Cosmos DB authorization tokens, see [Access Control on Azure Cosmos DB Resources](https://docs.microsoft.com/rest/api/cosmos-db/access-control-on-cosmosdb-resources).</span><span class="sxs-lookup"><span data-stu-id="ffb8b-199">To learn how to construct Azure Cosmos DB authorization tokens, see [Access Control on Azure Cosmos DB Resources](https://docs.microsoft.com/rest/api/cosmos-db/access-control-on-cosmosdb-resources).</span></span>
