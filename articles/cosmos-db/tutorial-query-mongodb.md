---
title: 'Azure Cosmos DB: How to query using the MongoDB API? | Microsoft Docs'
description: Learn to query with the MongoDB API for Azure Cosmos DB
services: cosmos-db
author: SnehaGunda
manager: kfile
ms.service: cosmos-db
ms.component: cosmosdb-mongo
ms.devlang: na
ms.topic: tutorial
ms.date: 03/29/2018
ms.author: sngun
ms.custom: mvc
ms.openlocfilehash: efb59a73b3c9b0ab06fae2e7b4fe5b97d85249eb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968755"
---
# <a name="tutorial-query-azure-cosmos-db-by-using-the-mongodb-api"></a><span data-ttu-id="4237a-104">Tutorial: Query Azure Cosmos DB by using the MongoDB API</span><span class="sxs-lookup"><span data-stu-id="4237a-104">Tutorial: Query Azure Cosmos DB by using the MongoDB API</span></span>

<span data-ttu-id="4237a-105">The Azure Cosmos DB [API for MongoDB](mongodb-introduction.md) supports [MongoDB shell queries](https://docs.mongodb.com/manual/tutorial/query-documents/).</span><span class="sxs-lookup"><span data-stu-id="4237a-105">The Azure Cosmos DB [API for MongoDB](mongodb-introduction.md) supports [MongoDB shell queries](https://docs.mongodb.com/manual/tutorial/query-documents/).</span></span> 

<span data-ttu-id="4237a-106">This article covers the following tasks:</span><span class="sxs-lookup"><span data-stu-id="4237a-106">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="4237a-107">Querying data with MongoDB</span><span class="sxs-lookup"><span data-stu-id="4237a-107">Querying data with MongoDB</span></span>

<span data-ttu-id="4237a-108">You can get started by using the examples in this document and watch the [Query Azure Cosmos DB with MongoDB shell](https://azure.microsoft.com/resources/videos/query-azure-cosmos-db-data-by-using-the-mongodb-shell/) video .</span><span class="sxs-lookup"><span data-stu-id="4237a-108">You can get started by using the examples in this document and watch the [Query Azure Cosmos DB with MongoDB shell](https://azure.microsoft.com/resources/videos/query-azure-cosmos-db-data-by-using-the-mongodb-shell/) video .</span></span>

## <a name="sample-document"></a><span data-ttu-id="4237a-109">Sample document</span><span class="sxs-lookup"><span data-stu-id="4237a-109">Sample document</span></span>

<span data-ttu-id="4237a-110">The queries in this article use the following sample document.</span><span class="sxs-lookup"><span data-stu-id="4237a-110">The queries in this article use the following sample document.</span></span>

```json
{
  "id": "WakefieldFamily",
  "parents": [
      { "familyName": "Wakefield", "givenName": "Robin" },
      { "familyName": "Miller", "givenName": "Ben" }
  ],
  "children": [
      {
        "familyName": "Merriam", 
        "givenName": "Jesse", 
        "gender": "female", "grade": 1,
        "pets": [
            { "givenName": "Goofy" },
            { "givenName": "Shadow" }
        ]
      },
      { 
        "familyName": "Miller", 
         "givenName": "Lisa", 
         "gender": "female", 
         "grade": 8 }
  ],
  "address": { "state": "NY", "county": "Manhattan", "city": "NY" },
  "creationDate": 1431620462,
  "isRegistered": false
}
```
## <a id="examplequery1"></a> <span data-ttu-id="4237a-111">Example query 1</span><span class="sxs-lookup"><span data-stu-id="4237a-111">Example query 1</span></span> 

<span data-ttu-id="4237a-112">Given the sample family document above, the following query returns the documents where the id field matches `WakefieldFamily`.</span><span class="sxs-lookup"><span data-stu-id="4237a-112">Given the sample family document above, the following query returns the documents where the id field matches `WakefieldFamily`.</span></span>

<span data-ttu-id="4237a-113">**Query**</span><span class="sxs-lookup"><span data-stu-id="4237a-113">**Query**</span></span>
    
    db.families.find({ id: "WakefieldFamily"})

<span data-ttu-id="4237a-114">**Results**</span><span class="sxs-lookup"><span data-stu-id="4237a-114">**Results**</span></span>

    {
    "_id": "ObjectId(\"58f65e1198f3a12c7090e68c\")",
    "id": "WakefieldFamily",
    "parents": [
      {
        "familyName": "Wakefield",
        "givenName": "Robin"
      },
      {
        "familyName": "Miller",
        "givenName": "Ben"
      }
    ],
    "children": [
      {
        "familyName": "Merriam",
        "givenName": "Jesse",
        "gender": "female",
        "grade": 1,
        "pets": [
          { "givenName": "Goofy" },
          { "givenName": "Shadow" }
        ]
      },
      {
        "familyName": "Miller",
        "givenName": "Lisa",
        "gender": "female",
        "grade": 8
      }
    ],
    "address": {
      "state": "NY",
      "county": "Manhattan",
      "city": "NY"
    },
    "creationDate": 1431620462,
    "isRegistered": false
    }

## <a id="examplequery2"></a><span data-ttu-id="4237a-115">Example query 2</span><span class="sxs-lookup"><span data-stu-id="4237a-115">Example query 2</span></span> 

<span data-ttu-id="4237a-116">The next query returns all the children in the family.</span><span class="sxs-lookup"><span data-stu-id="4237a-116">The next query returns all the children in the family.</span></span> 

<span data-ttu-id="4237a-117">**Query**</span><span class="sxs-lookup"><span data-stu-id="4237a-117">**Query**</span></span>
    
    db.families.find( { id: "WakefieldFamily" }, { children: true } )

<span data-ttu-id="4237a-118">**Results**</span><span class="sxs-lookup"><span data-stu-id="4237a-118">**Results**</span></span>

    {
    "_id": "ObjectId("58f65e1198f3a12c7090e68c")",
    "children": [
      {
        "familyName": "Merriam",
        "givenName": "Jesse",
        "gender": "female",
        "grade": 1,
        "pets": [
          { "givenName": "Goofy" },
          { "givenName": "Shadow" }
        ]
      },
      {
        "familyName": "Miller",
        "givenName": "Lisa",
        "gender": "female",
        "grade": 8
      }
    ]
    }


## <a id="examplequery3"></a><span data-ttu-id="4237a-119">Example query 3</span><span class="sxs-lookup"><span data-stu-id="4237a-119">Example query 3</span></span> 

<span data-ttu-id="4237a-120">The next query returns all the families that are registered.</span><span class="sxs-lookup"><span data-stu-id="4237a-120">The next query returns all the families that are registered.</span></span> 

<span data-ttu-id="4237a-121">**Query**</span><span class="sxs-lookup"><span data-stu-id="4237a-121">**Query**</span></span>
    
    db.families.find( { "isRegistered" : true })
<span data-ttu-id="4237a-122">**Results** No document will be returned.</span><span class="sxs-lookup"><span data-stu-id="4237a-122">**Results** No document will be returned.</span></span> 

## <a id="examplequery4"></a><span data-ttu-id="4237a-123">Example query 4</span><span class="sxs-lookup"><span data-stu-id="4237a-123">Example query 4</span></span>

<span data-ttu-id="4237a-124">The next query returns all the families that are not registered.</span><span class="sxs-lookup"><span data-stu-id="4237a-124">The next query returns all the families that are not registered.</span></span> 

<span data-ttu-id="4237a-125">**Query**</span><span class="sxs-lookup"><span data-stu-id="4237a-125">**Query**</span></span>
    
    db.families.find( { "isRegistered" : false })
<span data-ttu-id="4237a-126">**Results**</span><span class="sxs-lookup"><span data-stu-id="4237a-126">**Results**</span></span>

     {
    "_id": ObjectId("58f65e1198f3a12c7090e68c"),
    "id": "WakefieldFamily",
    "parents": [{
        "familyName": "Wakefield",
        "givenName": "Robin"
    }, {
        "familyName": "Miller",
        "givenName": "Ben"
    }],
    "children": [{
        "familyName": "Merriam",
        "givenName": "Jesse",
        "gender": "female",
        "grade": 1,
        "pets": [{
            "givenName": "Goofy"
        }, {
            "givenName": "Shadow"
        }]
    }, {
        "familyName": "Miller",
        "givenName": "Lisa",
        "gender": "female",
        "grade": 8
    }],
    "address": {
        "state": "NY",
        "county": "Manhattan",
        "city": "NY"
    },
    "creationDate": 1431620462,
    "isRegistered": false
<span data-ttu-id="4237a-127">}</span><span class="sxs-lookup"><span data-stu-id="4237a-127">}</span></span>

## <a id="examplequery5"></a><span data-ttu-id="4237a-128">Example query 5</span><span class="sxs-lookup"><span data-stu-id="4237a-128">Example query 5</span></span>

<span data-ttu-id="4237a-129">The next query returns all the families that are not registered and state is NY.</span><span class="sxs-lookup"><span data-stu-id="4237a-129">The next query returns all the families that are not registered and state is NY.</span></span> 

<span data-ttu-id="4237a-130">**Query**</span><span class="sxs-lookup"><span data-stu-id="4237a-130">**Query**</span></span>
    
     db.families.find( { "isRegistered" : false, "address.state" : "NY" })

<span data-ttu-id="4237a-131">**Results**</span><span class="sxs-lookup"><span data-stu-id="4237a-131">**Results**</span></span>

     {
    "_id": ObjectId("58f65e1198f3a12c7090e68c"),
    "id": "WakefieldFamily",
    "parents": [{
        "familyName": "Wakefield",
        "givenName": "Robin"
    }, {
        "familyName": "Miller",
        "givenName": "Ben"
    }],
    "children": [{
        "familyName": "Merriam",
        "givenName": "Jesse",
        "gender": "female",
        "grade": 1,
        "pets": [{
            "givenName": "Goofy"
        }, {
            "givenName": "Shadow"
        }]
    }, {
        "familyName": "Miller",
        "givenName": "Lisa",
        "gender": "female",
        "grade": 8
    }],
    "address": {
        "state": "NY",
        "county": "Manhattan",
        "city": "NY"
    },
    "creationDate": 1431620462,
    "isRegistered": false
<span data-ttu-id="4237a-132">}</span><span class="sxs-lookup"><span data-stu-id="4237a-132">}</span></span>


## <a id="examplequery6"></a><span data-ttu-id="4237a-133">Example query 6</span><span class="sxs-lookup"><span data-stu-id="4237a-133">Example query 6</span></span>

<span data-ttu-id="4237a-134">The next query returns all the families where children grades are 8.</span><span class="sxs-lookup"><span data-stu-id="4237a-134">The next query returns all the families where children grades are 8.</span></span>

<span data-ttu-id="4237a-135">**Query**</span><span class="sxs-lookup"><span data-stu-id="4237a-135">**Query**</span></span>
  
     db.families.find( { children : { $elemMatch: { grade : 8 }} } )

<span data-ttu-id="4237a-136">**Results**</span><span class="sxs-lookup"><span data-stu-id="4237a-136">**Results**</span></span>

     {
    "_id": ObjectId("58f65e1198f3a12c7090e68c"),
    "id": "WakefieldFamily",
    "parents": [{
        "familyName": "Wakefield",
        "givenName": "Robin"
    }, {
        "familyName": "Miller",
        "givenName": "Ben"
    }],
    "children": [{
        "familyName": "Merriam",
        "givenName": "Jesse",
        "gender": "female",
        "grade": 1,
        "pets": [{
            "givenName": "Goofy"
        }, {
            "givenName": "Shadow"
        }]
    }, {
        "familyName": "Miller",
        "givenName": "Lisa",
        "gender": "female",
        "grade": 8
    }],
    "address": {
        "state": "NY",
        "county": "Manhattan",
        "city": "NY"
    },
    "creationDate": 1431620462,
    "isRegistered": false
<span data-ttu-id="4237a-137">}</span><span class="sxs-lookup"><span data-stu-id="4237a-137">}</span></span>

## <a id="examplequery7"></a><span data-ttu-id="4237a-138">Example query 7</span><span class="sxs-lookup"><span data-stu-id="4237a-138">Example query 7</span></span>

<span data-ttu-id="4237a-139">The next query returns all the families where size of children array is 3.</span><span class="sxs-lookup"><span data-stu-id="4237a-139">The next query returns all the families where size of children array is 3.</span></span>

<span data-ttu-id="4237a-140">**Query**</span><span class="sxs-lookup"><span data-stu-id="4237a-140">**Query**</span></span>
  
      db.Family.find( {children: { $size:3} } )

<span data-ttu-id="4237a-141">**Results**</span><span class="sxs-lookup"><span data-stu-id="4237a-141">**Results**</span></span>

<span data-ttu-id="4237a-142">No results will be returned as there are no families with more than two children.</span><span class="sxs-lookup"><span data-stu-id="4237a-142">No results will be returned as there are no families with more than two children.</span></span> <span data-ttu-id="4237a-143">Only when parameter is 2 this query will succeed and return the full document.</span><span class="sxs-lookup"><span data-stu-id="4237a-143">Only when parameter is 2 this query will succeed and return the full document.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4237a-144">Next steps</span><span class="sxs-lookup"><span data-stu-id="4237a-144">Next steps</span></span>

<span data-ttu-id="4237a-145">In this tutorial, you've done the following:</span><span class="sxs-lookup"><span data-stu-id="4237a-145">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4237a-146">Learned how to query using MongoDB</span><span class="sxs-lookup"><span data-stu-id="4237a-146">Learned how to query using MongoDB</span></span> 

<span data-ttu-id="4237a-147">You can now proceed to the next tutorial to learn how to distribute your data globally.</span><span class="sxs-lookup"><span data-stu-id="4237a-147">You can now proceed to the next tutorial to learn how to distribute your data globally.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4237a-148">Distribute your data globally</span><span class="sxs-lookup"><span data-stu-id="4237a-148">Distribute your data globally</span></span>](tutorial-global-distribution-sql-api.md)

