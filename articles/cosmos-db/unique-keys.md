---
title: Unique keys in Azure Cosmos DB | Microsoft Docs
description: Learn how to use unique keys in your Azure Cosmos DB database.
services: cosmos-db
keywords: unique key constraint, violation of unique key constraint
author: rafats
manager: kfile
editor: monicar
ms.service: cosmos-db
ms.devlang: na
ms.topic: conceptual
ms.date: 08/08/2018
ms.author: rafats
ms.openlocfilehash: 5811cb1e08ed5d02038da2a4460ae4b63580833b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867875"
---
# <a name="unique-keys-in-azure-cosmos-db"></a><span data-ttu-id="cd289-104">Unique keys in Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="cd289-104">Unique keys in Azure Cosmos DB</span></span>

<span data-ttu-id="cd289-105">Unique keys provide developers with the ability to add a layer of data integrity to their database.</span><span class="sxs-lookup"><span data-stu-id="cd289-105">Unique keys provide developers with the ability to add a layer of data integrity to their database.</span></span> <span data-ttu-id="cd289-106">By creating a unique key policy when a container is created, you ensure the uniqueness of one or more values per [partition key](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="cd289-106">By creating a unique key policy when a container is created, you ensure the uniqueness of one or more values per [partition key](partition-data.md).</span></span> <span data-ttu-id="cd289-107">Once a container has been created with a unique key policy, it prevents the creation of any new or updated items with values that duplicate values specified by the unique key constraint.</span><span class="sxs-lookup"><span data-stu-id="cd289-107">Once a container has been created with a unique key policy, it prevents the creation of any new or updated items with values that duplicate values specified by the unique key constraint.</span></span>   

> [!NOTE]
> <span data-ttu-id="cd289-108">Unique keys are supported by the latest versions of the [.NET](sql-api-sdk-dotnet.md) and [.NET Core](sql-api-sdk-dotnet-core.md) SQL SDKs, and the [MongoDB API](mongodb-feature-support.md#unique-indexes).</span><span class="sxs-lookup"><span data-stu-id="cd289-108">Unique keys are supported by the latest versions of the [.NET](sql-api-sdk-dotnet.md) and [.NET Core](sql-api-sdk-dotnet-core.md) SQL SDKs, and the [MongoDB API](mongodb-feature-support.md#unique-indexes).</span></span> <span data-ttu-id="cd289-109">The Table API and Gremlin API do not support unique keys at this time.</span><span class="sxs-lookup"><span data-stu-id="cd289-109">The Table API and Gremlin API do not support unique keys at this time.</span></span> 
> 
>

## <a name="use-case"></a><span data-ttu-id="cd289-110">Use case</span><span class="sxs-lookup"><span data-stu-id="cd289-110">Use case</span></span>

<span data-ttu-id="cd289-111">As an example, let's look at how a user database associated with a [social application](use-cases.md#web-and-mobile-applications) could benefit from having a unique key policy on email addresses.</span><span class="sxs-lookup"><span data-stu-id="cd289-111">As an example, let's look at how a user database associated with a [social application](use-cases.md#web-and-mobile-applications) could benefit from having a unique key policy on email addresses.</span></span> <span data-ttu-id="cd289-112">By making the user's email address a unique key, you ensure each record has a unique email address, and no new records can be created with duplicate email addresses.</span><span class="sxs-lookup"><span data-stu-id="cd289-112">By making the user's email address a unique key, you ensure each record has a unique email address, and no new records can be created with duplicate email addresses.</span></span> 

<span data-ttu-id="cd289-113">If you did want users to be able to create multiple records with the same email address, but not the same first name, last name, and email address, you could add other paths to the unique key policy.</span><span class="sxs-lookup"><span data-stu-id="cd289-113">If you did want users to be able to create multiple records with the same email address, but not the same first name, last name, and email address, you could add other paths to the unique key policy.</span></span> <span data-ttu-id="cd289-114">So instead of creating a unique key based on an email address, you can create a unique key that's a combination of the first name, last name, and email.</span><span class="sxs-lookup"><span data-stu-id="cd289-114">So instead of creating a unique key based on an email address, you can create a unique key that's a combination of the first name, last name, and email.</span></span> <span data-ttu-id="cd289-115">In this case, each unique combination of the three paths is allowed, so the database could contain items that have the following path values.</span><span class="sxs-lookup"><span data-stu-id="cd289-115">In this case, each unique combination of the three paths is allowed, so the database could contain items that have the following path values.</span></span> <span data-ttu-id="cd289-116">Each of these records would pass the unique key policy.</span><span class="sxs-lookup"><span data-stu-id="cd289-116">Each of these records would pass the unique key policy.</span></span>  

<span data-ttu-id="cd289-117">**Allowed values for unique key of firstName, lastName, and email**</span><span class="sxs-lookup"><span data-stu-id="cd289-117">**Allowed values for unique key of firstName, lastName, and email**</span></span>

|<span data-ttu-id="cd289-118">First name</span><span class="sxs-lookup"><span data-stu-id="cd289-118">First name</span></span>|<span data-ttu-id="cd289-119">Last name</span><span class="sxs-lookup"><span data-stu-id="cd289-119">Last name</span></span>|<span data-ttu-id="cd289-120">Email address</span><span class="sxs-lookup"><span data-stu-id="cd289-120">Email address</span></span>|
|---|---|---|
|<span data-ttu-id="cd289-121">Gaby</span><span class="sxs-lookup"><span data-stu-id="cd289-121">Gaby</span></span>|<span data-ttu-id="cd289-122">Duperre</span><span class="sxs-lookup"><span data-stu-id="cd289-122">Duperre</span></span>|gaby@contoso.com |
|<span data-ttu-id="cd289-123">Gaby</span><span class="sxs-lookup"><span data-stu-id="cd289-123">Gaby</span></span>|<span data-ttu-id="cd289-124">Duperre</span><span class="sxs-lookup"><span data-stu-id="cd289-124">Duperre</span></span>|gaby@fabrikam.com|
|<span data-ttu-id="cd289-125">Ivan</span><span class="sxs-lookup"><span data-stu-id="cd289-125">Ivan</span></span>|<span data-ttu-id="cd289-126">Duperre</span><span class="sxs-lookup"><span data-stu-id="cd289-126">Duperre</span></span>|gaby@fabrikam.com|
|    |<span data-ttu-id="cd289-127">Duperre</span><span class="sxs-lookup"><span data-stu-id="cd289-127">Duperre</span></span>|gaby@fabrikam.com|
|    |       |gaby@fabraikam.com|

<span data-ttu-id="cd289-128">If you attempted to insert another record with any of the combinations listed in the table above, you would receive an error indicating that the unique key constraint was not met.</span><span class="sxs-lookup"><span data-stu-id="cd289-128">If you attempted to insert another record with any of the combinations listed in the table above, you would receive an error indicating that the unique key constraint was not met.</span></span> <span data-ttu-id="cd289-129">The error Azure Cosmos DB returned is "Resource with specified id or name already exists."</span><span class="sxs-lookup"><span data-stu-id="cd289-129">The error Azure Cosmos DB returned is "Resource with specified id or name already exists."</span></span> <span data-ttu-id="cd289-130">or "Resource with specified id, name, or unique index already exists."</span><span class="sxs-lookup"><span data-stu-id="cd289-130">or "Resource with specified id, name, or unique index already exists."</span></span> 

## <a name="using-unique-keys"></a><span data-ttu-id="cd289-131">Using unique keys</span><span class="sxs-lookup"><span data-stu-id="cd289-131">Using unique keys</span></span>

<span data-ttu-id="cd289-132">Unique keys must be defined when the container is created, and the unique key is scoped to the partition key.</span><span class="sxs-lookup"><span data-stu-id="cd289-132">Unique keys must be defined when the container is created, and the unique key is scoped to the partition key.</span></span> <span data-ttu-id="cd289-133">To build on the earlier example, if you partition based on zip code, you could have the records from the table duplicated in each partition.</span><span class="sxs-lookup"><span data-stu-id="cd289-133">To build on the earlier example, if you partition based on zip code, you could have the records from the table duplicated in each partition.</span></span>

<span data-ttu-id="cd289-134">You cannot update existing container to use unique keys.</span><span class="sxs-lookup"><span data-stu-id="cd289-134">You cannot update existing container to use unique keys.</span></span>

<span data-ttu-id="cd289-135">Once a container is created with a unique key policy, the policy cannot be changed unless you recreate the container.</span><span class="sxs-lookup"><span data-stu-id="cd289-135">Once a container is created with a unique key policy, the policy cannot be changed unless you recreate the container.</span></span> <span data-ttu-id="cd289-136">If you have existing data that you'd like to implement unique keys on, create the new container, and then use the appropriate data migration tool to move the data to the new container.</span><span class="sxs-lookup"><span data-stu-id="cd289-136">If you have existing data that you'd like to implement unique keys on, create the new container, and then use the appropriate data migration tool to move the data to the new container.</span></span> <span data-ttu-id="cd289-137">For SQL containers, use the [Data Migration Tool](import-data.md).</span><span class="sxs-lookup"><span data-stu-id="cd289-137">For SQL containers, use the [Data Migration Tool](import-data.md).</span></span> <span data-ttu-id="cd289-138">For MongoDB containers, use [mongoimport.exe or mongorestore.exe](mongodb-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="cd289-138">For MongoDB containers, use [mongoimport.exe or mongorestore.exe](mongodb-migrate.md).</span></span>

<span data-ttu-id="cd289-139">A maximum of 16 path values (for example /firstName, /lastName, /address/zipCode, etc.) can be included in each unique key.</span><span class="sxs-lookup"><span data-stu-id="cd289-139">A maximum of 16 path values (for example /firstName, /lastName, /address/zipCode, etc.) can be included in each unique key.</span></span> 

<span data-ttu-id="cd289-140">Each unique key policy can have a maximum of 10 unique key constraints or combinations and the combined paths for all unique index properties should not exceed 60 characters.</span><span class="sxs-lookup"><span data-stu-id="cd289-140">Each unique key policy can have a maximum of 10 unique key constraints or combinations and the combined paths for all unique index properties should not exceed 60 characters.</span></span> <span data-ttu-id="cd289-141">So the earlier example that uses first name, last name, and email address is just one constraint, and it uses three of the 16 possible paths available.</span><span class="sxs-lookup"><span data-stu-id="cd289-141">So the earlier example that uses first name, last name, and email address is just one constraint, and it uses three of the 16 possible paths available.</span></span> 

<span data-ttu-id="cd289-142">Request unit charges for creating, updating, and deleting an item are slightly higher when there is a unique key policy on the container.</span><span class="sxs-lookup"><span data-stu-id="cd289-142">Request unit charges for creating, updating, and deleting an item are slightly higher when there is a unique key policy on the container.</span></span> 

<span data-ttu-id="cd289-143">Sparse unique keys are not supported.</span><span class="sxs-lookup"><span data-stu-id="cd289-143">Sparse unique keys are not supported.</span></span> <span data-ttu-id="cd289-144">If values for some unique paths are missing, they are treated as a special null value, which takes part in the uniqueness constraint.</span><span class="sxs-lookup"><span data-stu-id="cd289-144">If values for some unique paths are missing, they are treated as a special null value, which takes part in the uniqueness constraint.</span></span>

## <a name="sql-api-sample"></a><span data-ttu-id="cd289-145">SQL API sample</span><span class="sxs-lookup"><span data-stu-id="cd289-145">SQL API sample</span></span>

<span data-ttu-id="cd289-146">The following code sample shows how to create a new SQL container with two unique key constraints.</span><span class="sxs-lookup"><span data-stu-id="cd289-146">The following code sample shows how to create a new SQL container with two unique key constraints.</span></span> <span data-ttu-id="cd289-147">The first constraint is the firstName, lastName, email constraint described in the earlier example.</span><span class="sxs-lookup"><span data-stu-id="cd289-147">The first constraint is the firstName, lastName, email constraint described in the earlier example.</span></span> <span data-ttu-id="cd289-148">The second constraint is the users address/zipCode.</span><span class="sxs-lookup"><span data-stu-id="cd289-148">The second constraint is the users address/zipCode.</span></span> <span data-ttu-id="cd289-149">A sample JSON file that uses the paths in this unique key policy follows the code example.</span><span class="sxs-lookup"><span data-stu-id="cd289-149">A sample JSON file that uses the paths in this unique key policy follows the code example.</span></span> 

```csharp
// Create a collection with two separate UniqueKeys, one compound key for /firstName, /lastName,
// and /email, and another for /address/zipCode.
private static async Task CreateCollectionIfNotExistsAsync(string dataBase, string collection)
{
    try
    {
        await client.ReadDocumentCollectionAsync(UriFactory.CreateDocumentCollectionUri(dataBase, collection));
    }
    catch (DocumentClientException e)
    {
        if (e.StatusCode == System.Net.HttpStatusCode.NotFound)
        {
            DocumentCollection myCollection = new DocumentCollection();
            myCollection.Id = collection;
            myCollection.PartitionKey.Paths.Add("/pk");
            myCollection.UniqueKeyPolicy = new UniqueKeyPolicy
            {
                UniqueKeys =
                new Collection<UniqueKey>
                {
                    new UniqueKey { Paths = new Collection<string> { "/firstName" , "/lastName" , "/email" }}
                    new UniqueKey { Paths = new Collection<string> { "/address/zipcode" } },
          }
            };
            await client.CreateDocumentCollectionAsync(
                UriFactory.CreateDatabaseUri(dataBase),
                myCollection,
                new RequestOptions { OfferThroughput = 2500 });
        }
        else
        {
            throw;
        }
    }
```

<span data-ttu-id="cd289-150">Sample JSON document.</span><span class="sxs-lookup"><span data-stu-id="cd289-150">Sample JSON document.</span></span>

```json
{
    "id": "1",
    "pk": "1234",
    "firstName": "Gaby",
    "lastName": "Duperre",
    "email": "gaby@contoso.com",
    "address": 
        {            
            "line1": "100 Some Street",
            "line2": "Unit 1",
            "city": "Seattle",
            "state": "WA",
            "zipcode": 98012
        }
    
}
```
> [!NOTE]
> <span data-ttu-id="cd289-151">Please note unique key name is case sensitive.</span><span class="sxs-lookup"><span data-stu-id="cd289-151">Please note unique key name is case sensitive.</span></span> <span data-ttu-id="cd289-152">As shown in above example, unique name is set for /address/zipcode.</span><span class="sxs-lookup"><span data-stu-id="cd289-152">As shown in above example, unique name is set for /address/zipcode.</span></span> <span data-ttu-id="cd289-153">If your data will have ZipCode, then it will insert "null" in  unique key as zipcode is not equal to ZipCode.</span><span class="sxs-lookup"><span data-stu-id="cd289-153">If your data will have ZipCode, then it will insert "null" in  unique key as zipcode is not equal to ZipCode.</span></span> <span data-ttu-id="cd289-154">And because of this case sensitivity all other records with ZipCode will not be able to be inserted as duplicate "null" will violate unique key constraint.</span><span class="sxs-lookup"><span data-stu-id="cd289-154">And because of this case sensitivity all other records with ZipCode will not be able to be inserted as duplicate "null" will violate unique key constraint.</span></span>

## <a name="mongodb-api-sample"></a><span data-ttu-id="cd289-155">MongoDB API sample</span><span class="sxs-lookup"><span data-stu-id="cd289-155">MongoDB API sample</span></span>

<span data-ttu-id="cd289-156">The following command sample shows how to create a unique index on the firstName, lastName, and email fields of the users collection for the MongoDB API.</span><span class="sxs-lookup"><span data-stu-id="cd289-156">The following command sample shows how to create a unique index on the firstName, lastName, and email fields of the users collection for the MongoDB API.</span></span> <span data-ttu-id="cd289-157">This ensures the uniqueness for a combination of all three fields across all documents in the collection.</span><span class="sxs-lookup"><span data-stu-id="cd289-157">This ensures the uniqueness for a combination of all three fields across all documents in the collection.</span></span> <span data-ttu-id="cd289-158">For MongoDB API collections, the unique index is created after the collection is created, but before populating the collection.</span><span class="sxs-lookup"><span data-stu-id="cd289-158">For MongoDB API collections, the unique index is created after the collection is created, but before populating the collection.</span></span>

> [!NOTE]
> <span data-ttu-id="cd289-159">The unique key format for MongoDB API accounts is different from that of SQL API accounts, where you don’t have to specify the backslash (/) character before the field name.</span><span class="sxs-lookup"><span data-stu-id="cd289-159">The unique key format for MongoDB API accounts is different from that of SQL API accounts, where you don’t have to specify the backslash (/) character before the field name.</span></span> 

```
db.users.createIndex( { firstName: 1, lastName: 1, email: 1 }, { unique: true } )
```
## <a name="configure-unique-keys-by-using-azure-portal"></a><span data-ttu-id="cd289-160">Configure unique keys by using Azure Portal</span><span class="sxs-lookup"><span data-stu-id="cd289-160">Configure unique keys by using Azure Portal</span></span>

<span data-ttu-id="cd289-161">In the sections above you'll find code samples that will show how you can define unique key constraints when a collection is created using the SQL API or MongoDB API.</span><span class="sxs-lookup"><span data-stu-id="cd289-161">In the sections above you'll find code samples that will show how you can define unique key constraints when a collection is created using the SQL API or MongoDB API.</span></span> <span data-ttu-id="cd289-162">But it's also possible to define unique keys when you create a collection via the web UI in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="cd289-162">But it's also possible to define unique keys when you create a collection via the web UI in the Azure portal.</span></span> 

- <span data-ttu-id="cd289-163">Navigate to the **Data Explorer** in your Cosmos DB account</span><span class="sxs-lookup"><span data-stu-id="cd289-163">Navigate to the **Data Explorer** in your Cosmos DB account</span></span>
- <span data-ttu-id="cd289-164">Click **New Collection**</span><span class="sxs-lookup"><span data-stu-id="cd289-164">Click **New Collection**</span></span>
- <span data-ttu-id="cd289-165">In the section Unique keys,\*\* you can add the desired unique key constraints by clicking **Add unique key**</span><span class="sxs-lookup"><span data-stu-id="cd289-165">In the section Unique keys,\*\* you can add the desired unique key constraints by clicking **Add unique key**</span></span>

![Define Unique Keys in the Data Explorer](./media/unique-keys/unique-keys-azure-portal.png)

- <span data-ttu-id="cd289-167">If you'd like to create a unique key constraint on the lastName path, you add `/lastName`.</span><span class="sxs-lookup"><span data-stu-id="cd289-167">If you'd like to create a unique key constraint on the lastName path, you add `/lastName`.</span></span>
- <span data-ttu-id="cd289-168">If you'd like to create a unique key constraint for the lastName firstName combination, you add `/lastName,/firstName`</span><span class="sxs-lookup"><span data-stu-id="cd289-168">If you'd like to create a unique key constraint for the lastName firstName combination, you add `/lastName,/firstName`</span></span>

<span data-ttu-id="cd289-169">When done click **OK** to create the collection.</span><span class="sxs-lookup"><span data-stu-id="cd289-169">When done click **OK** to create the collection.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cd289-170">Next steps</span><span class="sxs-lookup"><span data-stu-id="cd289-170">Next steps</span></span>

<span data-ttu-id="cd289-171">In this article, you learned how to create unique keys for items in a database.</span><span class="sxs-lookup"><span data-stu-id="cd289-171">In this article, you learned how to create unique keys for items in a database.</span></span> <span data-ttu-id="cd289-172">If you are creating a container for the first time, review [Partitioning data in Azure Cosmos DB](partition-data.md) as unique keys and partition keys rely on each other.</span><span class="sxs-lookup"><span data-stu-id="cd289-172">If you are creating a container for the first time, review [Partitioning data in Azure Cosmos DB](partition-data.md) as unique keys and partition keys rely on each other.</span></span> 


