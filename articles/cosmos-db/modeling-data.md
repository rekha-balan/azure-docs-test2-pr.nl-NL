---
title: Modeling document data for a NoSQL database | Microsoft Docs
description: Learn about modeling data for NoSQL databases
keywords: modeling data
services: cosmos-db
author: aliuy
manager: kfile
ms.service: cosmos-db
ms.devlang: na
ms.topic: conceptual
ms.date: 05/29/2016
ms.author: andrl
ms.openlocfilehash: 452ea278df57956821bd6166b0b36fd406c3139d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968534"
---
# <a name="modeling-document-data-for-nosql-databases"></a><span data-ttu-id="c7d38-104">Modeling document data for NoSQL databases</span><span class="sxs-lookup"><span data-stu-id="c7d38-104">Modeling document data for NoSQL databases</span></span>
<span data-ttu-id="c7d38-105">While schema-free databases, like Azure Cosmos DB, make it super easy to embrace changes to your data model you should still spend some time thinking about your data.</span><span class="sxs-lookup"><span data-stu-id="c7d38-105">While schema-free databases, like Azure Cosmos DB, make it super easy to embrace changes to your data model you should still spend some time thinking about your data.</span></span> 

<span data-ttu-id="c7d38-106">How is data going to be stored?</span><span class="sxs-lookup"><span data-stu-id="c7d38-106">How is data going to be stored?</span></span> <span data-ttu-id="c7d38-107">How is your application going to retrieve and query data?</span><span class="sxs-lookup"><span data-stu-id="c7d38-107">How is your application going to retrieve and query data?</span></span> <span data-ttu-id="c7d38-108">Is your application read heavy, or write heavy?</span><span class="sxs-lookup"><span data-stu-id="c7d38-108">Is your application read heavy, or write heavy?</span></span> 

<span data-ttu-id="c7d38-109">After reading this article, you will be able to answer the following questions:</span><span class="sxs-lookup"><span data-stu-id="c7d38-109">After reading this article, you will be able to answer the following questions:</span></span>

* <span data-ttu-id="c7d38-110">How should I think about a document in a document database?</span><span class="sxs-lookup"><span data-stu-id="c7d38-110">How should I think about a document in a document database?</span></span>
* <span data-ttu-id="c7d38-111">What is data modeling and why should I care?</span><span class="sxs-lookup"><span data-stu-id="c7d38-111">What is data modeling and why should I care?</span></span> 
* <span data-ttu-id="c7d38-112">How is modeling data in a document database different to a relational database?</span><span class="sxs-lookup"><span data-stu-id="c7d38-112">How is modeling data in a document database different to a relational database?</span></span>
* <span data-ttu-id="c7d38-113">How do I express data relationships in a non-relational database?</span><span class="sxs-lookup"><span data-stu-id="c7d38-113">How do I express data relationships in a non-relational database?</span></span>
* <span data-ttu-id="c7d38-114">When do I embed data and when do I link to data?</span><span class="sxs-lookup"><span data-stu-id="c7d38-114">When do I embed data and when do I link to data?</span></span>

## <a name="embedding-data"></a><span data-ttu-id="c7d38-115">Embedding data</span><span class="sxs-lookup"><span data-stu-id="c7d38-115">Embedding data</span></span>
<span data-ttu-id="c7d38-116">When you start modeling data in a document store, such as Azure Cosmos DB, try to treat your entities as **self-contained documents** represented in JSON.</span><span class="sxs-lookup"><span data-stu-id="c7d38-116">When you start modeling data in a document store, such as Azure Cosmos DB, try to treat your entities as **self-contained documents** represented in JSON.</span></span>

<span data-ttu-id="c7d38-117">Before we dive in too much further, let us take a few steps back and have a look at how we might model something in a relational database, a subject many of us are already familiar with.</span><span class="sxs-lookup"><span data-stu-id="c7d38-117">Before we dive in too much further, let us take a few steps back and have a look at how we might model something in a relational database, a subject many of us are already familiar with.</span></span> <span data-ttu-id="c7d38-118">The following example shows how a person might be stored in a relational database.</span><span class="sxs-lookup"><span data-stu-id="c7d38-118">The following example shows how a person might be stored in a relational database.</span></span> 

![Relational database model](./media/sql-api-modeling-data/relational-data-model.png)

<span data-ttu-id="c7d38-120">When working with relational databases, we've been taught for years to normalize, normalize, normalize.</span><span class="sxs-lookup"><span data-stu-id="c7d38-120">When working with relational databases, we've been taught for years to normalize, normalize, normalize.</span></span>

<span data-ttu-id="c7d38-121">Normalizing your data typically involves taking an entity, such as a person, and breaking it down in to discrete pieces of data.</span><span class="sxs-lookup"><span data-stu-id="c7d38-121">Normalizing your data typically involves taking an entity, such as a person, and breaking it down in to discrete pieces of data.</span></span> <span data-ttu-id="c7d38-122">In the example above, a person can have multiple contact detail records as well as multiple address records.</span><span class="sxs-lookup"><span data-stu-id="c7d38-122">In the example above, a person can have multiple contact detail records as well as multiple address records.</span></span> <span data-ttu-id="c7d38-123">We even go one step further and break down contact details by further extracting common fields like a type.</span><span class="sxs-lookup"><span data-stu-id="c7d38-123">We even go one step further and break down contact details by further extracting common fields like a type.</span></span> <span data-ttu-id="c7d38-124">Same for address, each record here has a type like *Home* or *Business*</span><span class="sxs-lookup"><span data-stu-id="c7d38-124">Same for address, each record here has a type like *Home* or *Business*</span></span> 

<span data-ttu-id="c7d38-125">The guiding premise when normalizing data is to **avoid storing redundant data** on each record and rather refer to data.</span><span class="sxs-lookup"><span data-stu-id="c7d38-125">The guiding premise when normalizing data is to **avoid storing redundant data** on each record and rather refer to data.</span></span> <span data-ttu-id="c7d38-126">In this example, to read a person, with all their contact details and addresses, you need to use JOINS to effectively aggregate your data at run time.</span><span class="sxs-lookup"><span data-stu-id="c7d38-126">In this example, to read a person, with all their contact details and addresses, you need to use JOINS to effectively aggregate your data at run time.</span></span>

    SELECT p.FirstName, p.LastName, a.City, cd.Detail
    FROM Person p
    JOIN ContactDetail cd ON cd.PersonId = p.Id
    JOIN ContactDetailType on cdt ON cdt.Id = cd.TypeId
    JOIN Address a ON a.PersonId = p.Id

<span data-ttu-id="c7d38-127">Updating a single person with their contact details and addresses requires write operations across many individual tables.</span><span class="sxs-lookup"><span data-stu-id="c7d38-127">Updating a single person with their contact details and addresses requires write operations across many individual tables.</span></span> 

<span data-ttu-id="c7d38-128">Now let's take a look at how we would model the same data as a self-contained entity in a document database.</span><span class="sxs-lookup"><span data-stu-id="c7d38-128">Now let's take a look at how we would model the same data as a self-contained entity in a document database.</span></span>

    {
        "id": "1",
        "firstName": "Thomas",
        "lastName": "Andersen",
        "addresses": [
            {            
                "line1": "100 Some Street",
                "line2": "Unit 1",
                "city": "Seattle",
                "state": "WA",
                "zip": 98012
            }
        ],
        "contactDetails": [
            {"email": "thomas@andersen.com"},
            {"phone": "+1 555 555-5555", "extension": 5555}
        ] 
    }

<span data-ttu-id="c7d38-129">Using the approach above we have now **denormalized** the person record where we **embedded** all the information relating to this person, such as their contact details and addresses, in to a single JSON document.</span><span class="sxs-lookup"><span data-stu-id="c7d38-129">Using the approach above we have now **denormalized** the person record where we **embedded** all the information relating to this person, such as their contact details and addresses, in to a single JSON document.</span></span>
<span data-ttu-id="c7d38-130">In addition, because we're not confined to a fixed schema we have the flexibility to do things like having contact details of different shapes entirely.</span><span class="sxs-lookup"><span data-stu-id="c7d38-130">In addition, because we're not confined to a fixed schema we have the flexibility to do things like having contact details of different shapes entirely.</span></span> 

<span data-ttu-id="c7d38-131">Retrieving a complete person record from the database is now a single read operation against a single collection and for a single document.</span><span class="sxs-lookup"><span data-stu-id="c7d38-131">Retrieving a complete person record from the database is now a single read operation against a single collection and for a single document.</span></span> <span data-ttu-id="c7d38-132">Updating a person record, with their contact details and addresses, is also a single write operation against a single document.</span><span class="sxs-lookup"><span data-stu-id="c7d38-132">Updating a person record, with their contact details and addresses, is also a single write operation against a single document.</span></span>

<span data-ttu-id="c7d38-133">By denormalizing data, your application may need to issue fewer queries and updates to complete common operations.</span><span class="sxs-lookup"><span data-stu-id="c7d38-133">By denormalizing data, your application may need to issue fewer queries and updates to complete common operations.</span></span> 

### <a name="when-to-embed"></a><span data-ttu-id="c7d38-134">When to embed</span><span class="sxs-lookup"><span data-stu-id="c7d38-134">When to embed</span></span>
<span data-ttu-id="c7d38-135">In general, use embedded data models when:</span><span class="sxs-lookup"><span data-stu-id="c7d38-135">In general, use embedded data models when:</span></span>

* <span data-ttu-id="c7d38-136">There are **contains** relationships between entities.</span><span class="sxs-lookup"><span data-stu-id="c7d38-136">There are **contains** relationships between entities.</span></span>
* <span data-ttu-id="c7d38-137">There are **one-to-few** relationships between entities.</span><span class="sxs-lookup"><span data-stu-id="c7d38-137">There are **one-to-few** relationships between entities.</span></span>
* <span data-ttu-id="c7d38-138">There is embedded data that **changes infrequently**.</span><span class="sxs-lookup"><span data-stu-id="c7d38-138">There is embedded data that **changes infrequently**.</span></span>
* <span data-ttu-id="c7d38-139">There is embedded data won't grow **without bound**.</span><span class="sxs-lookup"><span data-stu-id="c7d38-139">There is embedded data won't grow **without bound**.</span></span>
* <span data-ttu-id="c7d38-140">There is embedded data that is **integral** to data in a document.</span><span class="sxs-lookup"><span data-stu-id="c7d38-140">There is embedded data that is **integral** to data in a document.</span></span>

> [!NOTE]
> <span data-ttu-id="c7d38-141">Typically denormalized data models provide better **read** performance.</span><span class="sxs-lookup"><span data-stu-id="c7d38-141">Typically denormalized data models provide better **read** performance.</span></span>
> 
> 

### <a name="when-not-to-embed"></a><span data-ttu-id="c7d38-142">When not to embed</span><span class="sxs-lookup"><span data-stu-id="c7d38-142">When not to embed</span></span>
<span data-ttu-id="c7d38-143">While the rule of thumb in a document database is to denormalize everything and embed all data in to a single document, this can lead to some situations that should be avoided.</span><span class="sxs-lookup"><span data-stu-id="c7d38-143">While the rule of thumb in a document database is to denormalize everything and embed all data in to a single document, this can lead to some situations that should be avoided.</span></span>

<span data-ttu-id="c7d38-144">Take this JSON snippet.</span><span class="sxs-lookup"><span data-stu-id="c7d38-144">Take this JSON snippet.</span></span>

    {
        "id": "1",
        "name": "What's new in the coolest Cloud",
        "summary": "A blog post by someone real famous",
        "comments": [
            {"id": 1, "author": "anon", "comment": "something useful, I'm sure"},
            {"id": 2, "author": "bob", "comment": "wisdom from the interwebs"},
            …
            {"id": 100001, "author": "jane", "comment": "and on we go ..."},
            …
            {"id": 1000000001, "author": "angry", "comment": "blah angry blah angry"},
            …
            {"id": ∞ + 1, "author": "bored", "comment": "oh man, will this ever end?"},
        ]
    }

<span data-ttu-id="c7d38-145">This might be what a post entity with embedded comments would look like if we were modeling a typical blog, or CMS, system.</span><span class="sxs-lookup"><span data-stu-id="c7d38-145">This might be what a post entity with embedded comments would look like if we were modeling a typical blog, or CMS, system.</span></span> <span data-ttu-id="c7d38-146">The problem with this example is that the comments array is **unbounded**, meaning that there is no (practical) limit to the number of comments any single post can have.</span><span class="sxs-lookup"><span data-stu-id="c7d38-146">The problem with this example is that the comments array is **unbounded**, meaning that there is no (practical) limit to the number of comments any single post can have.</span></span> <span data-ttu-id="c7d38-147">This will become a problem as the size of the document could grow significantly.</span><span class="sxs-lookup"><span data-stu-id="c7d38-147">This will become a problem as the size of the document could grow significantly.</span></span>

<span data-ttu-id="c7d38-148">As the size of the document grows the ability to transmit the data over the wire as well as reading and updating the document, at scale, will be impacted.</span><span class="sxs-lookup"><span data-stu-id="c7d38-148">As the size of the document grows the ability to transmit the data over the wire as well as reading and updating the document, at scale, will be impacted.</span></span>

<span data-ttu-id="c7d38-149">In this case it would be better to consider the following model.</span><span class="sxs-lookup"><span data-stu-id="c7d38-149">In this case it would be better to consider the following model.</span></span>

    Post document:
    {
        "id": "1",
        "name": "What's new in the coolest Cloud",
        "summary": "A blog post by someone real famous",
        "recentComments": [
            {"id": 1, "author": "anon", "comment": "something useful, I'm sure"},
            {"id": 2, "author": "bob", "comment": "wisdom from the interwebs"},
            {"id": 3, "author": "jane", "comment": "....."}
        ]
    }

    Comment documents:
    {
        "postId": "1"
        "comments": [
            {"id": 4, "author": "anon", "comment": "more goodness"},
            {"id": 5, "author": "bob", "comment": "tails from the field"},
            ...
            {"id": 99, "author": "angry", "comment": "blah angry blah angry"}
        ]
    },
    {
        "postId": "1"
        "comments": [
            {"id": 100, "author": "anon", "comment": "yet more"},
            ...
            {"id": 199, "author": "bored", "comment": "will this ever end?"}
        ]
    }

<span data-ttu-id="c7d38-150">This model has the three most recent comments embedded on the post itself, which is an array with a fixed bound this time.</span><span class="sxs-lookup"><span data-stu-id="c7d38-150">This model has the three most recent comments embedded on the post itself, which is an array with a fixed bound this time.</span></span> <span data-ttu-id="c7d38-151">The other comments are grouped in to batches of 100 comments and stored in separate documents.</span><span class="sxs-lookup"><span data-stu-id="c7d38-151">The other comments are grouped in to batches of 100 comments and stored in separate documents.</span></span> <span data-ttu-id="c7d38-152">The size of the batch was chosen as 100 because our fictitious application allows the user to load 100 comments at a time.</span><span class="sxs-lookup"><span data-stu-id="c7d38-152">The size of the batch was chosen as 100 because our fictitious application allows the user to load 100 comments at a time.</span></span>  

<span data-ttu-id="c7d38-153">Another case where embedding data is not a good idea is when the embedded data is used often across documents and will change frequently.</span><span class="sxs-lookup"><span data-stu-id="c7d38-153">Another case where embedding data is not a good idea is when the embedded data is used often across documents and will change frequently.</span></span> 

<span data-ttu-id="c7d38-154">Take this JSON snippet.</span><span class="sxs-lookup"><span data-stu-id="c7d38-154">Take this JSON snippet.</span></span>

    {
        "id": "1",
        "firstName": "Thomas",
        "lastName": "Andersen",
        "holdings": [
            {
                "numberHeld": 100,
                "stock": { "symbol": "zaza", "open": 1, "high": 2, "low": 0.5 }
            },
            {
                "numberHeld": 50,
                "stock": { "symbol": "xcxc", "open": 89, "high": 93.24, "low": 88.87 }
            }
        ]
    }

<span data-ttu-id="c7d38-155">This could represent a person's stock portfolio.</span><span class="sxs-lookup"><span data-stu-id="c7d38-155">This could represent a person's stock portfolio.</span></span> <span data-ttu-id="c7d38-156">We have chosen to embed the stock information in to each portfolio document.</span><span class="sxs-lookup"><span data-stu-id="c7d38-156">We have chosen to embed the stock information in to each portfolio document.</span></span> <span data-ttu-id="c7d38-157">In an environment where related data is changing frequently, like a stock trading application, embedding data that changes frequently is going to mean that you are constantly updating each portfolio document every time a stock is traded.</span><span class="sxs-lookup"><span data-stu-id="c7d38-157">In an environment where related data is changing frequently, like a stock trading application, embedding data that changes frequently is going to mean that you are constantly updating each portfolio document every time a stock is traded.</span></span>

<span data-ttu-id="c7d38-158">Stock *zaza* may be traded many hundreds of times in a single day and thousands of users could have *zaza* on their portfolio.</span><span class="sxs-lookup"><span data-stu-id="c7d38-158">Stock *zaza* may be traded many hundreds of times in a single day and thousands of users could have *zaza* on their portfolio.</span></span> <span data-ttu-id="c7d38-159">With a data model like the above we would have to update many thousands of portfolio documents many times every day leading to a system that won't scale very well.</span><span class="sxs-lookup"><span data-stu-id="c7d38-159">With a data model like the above we would have to update many thousands of portfolio documents many times every day leading to a system that won't scale very well.</span></span> 

## <a id="Refer"></a><span data-ttu-id="c7d38-160">Referencing data</span><span class="sxs-lookup"><span data-stu-id="c7d38-160">Referencing data</span></span>
<span data-ttu-id="c7d38-161">So, embedding data works nicely for many cases but it is clear that there are scenarios when denormalizing your data will cause more problems than it is worth.</span><span class="sxs-lookup"><span data-stu-id="c7d38-161">So, embedding data works nicely for many cases but it is clear that there are scenarios when denormalizing your data will cause more problems than it is worth.</span></span> <span data-ttu-id="c7d38-162">So what do we do now?</span><span class="sxs-lookup"><span data-stu-id="c7d38-162">So what do we do now?</span></span> 

<span data-ttu-id="c7d38-163">Relational databases are not the only place where you can create relationships between entities.</span><span class="sxs-lookup"><span data-stu-id="c7d38-163">Relational databases are not the only place where you can create relationships between entities.</span></span> <span data-ttu-id="c7d38-164">In a document database you can have information in one document that actually relates to data in other documents.</span><span class="sxs-lookup"><span data-stu-id="c7d38-164">In a document database you can have information in one document that actually relates to data in other documents.</span></span> <span data-ttu-id="c7d38-165">Now, I am not advocating for even one minute that we build systems that would be better suited to a relational database in Azure Cosmos DB, or any other document database, but simple relationships are fine and can be very useful.</span><span class="sxs-lookup"><span data-stu-id="c7d38-165">Now, I am not advocating for even one minute that we build systems that would be better suited to a relational database in Azure Cosmos DB, or any other document database, but simple relationships are fine and can be very useful.</span></span> 

<span data-ttu-id="c7d38-166">In the JSON below we chose to use the example of a stock portfolio from earlier but this time we refer to the stock item on the portfolio instead of embedding it.</span><span class="sxs-lookup"><span data-stu-id="c7d38-166">In the JSON below we chose to use the example of a stock portfolio from earlier but this time we refer to the stock item on the portfolio instead of embedding it.</span></span> <span data-ttu-id="c7d38-167">This way, when the stock item changes frequently throughout the day the only document that needs to be updated is the single stock document.</span><span class="sxs-lookup"><span data-stu-id="c7d38-167">This way, when the stock item changes frequently throughout the day the only document that needs to be updated is the single stock document.</span></span> 

    Person document:
    {
        "id": "1",
        "firstName": "Thomas",
        "lastName": "Andersen",
        "holdings": [
            { "numberHeld":  100, "stockId": 1},
            { "numberHeld":  50, "stockId": 2}
        ]
    }

    Stock documents:
    {
        "id": "1",
        "symbol": "zaza",
        "open": 1,
        "high": 2,
        "low": 0.5,
        "vol": 11970000,
        "mkt-cap": 42000000,
        "pe": 5.89
    },
    {
        "id": "2",
        "symbol": "xcxc",
        "open": 89,
        "high": 93.24,
        "low": 88.87,
        "vol": 2970200,
        "mkt-cap": 1005000,
        "pe": 75.82
    }


<span data-ttu-id="c7d38-168">An immediate downside to this approach though is if your application is required to show information about each stock that is held when displaying a person's portfolio; in this case you would need to make multiple trips to the database to load the information for each stock document.</span><span class="sxs-lookup"><span data-stu-id="c7d38-168">An immediate downside to this approach though is if your application is required to show information about each stock that is held when displaying a person's portfolio; in this case you would need to make multiple trips to the database to load the information for each stock document.</span></span> <span data-ttu-id="c7d38-169">Here we've made a decision to improve the efficiency of write operations, which happen frequently throughout the day, but in turn compromised on the read operations that potentially have less impact on the performance of this particular system.</span><span class="sxs-lookup"><span data-stu-id="c7d38-169">Here we've made a decision to improve the efficiency of write operations, which happen frequently throughout the day, but in turn compromised on the read operations that potentially have less impact on the performance of this particular system.</span></span>

> [!NOTE]
> <span data-ttu-id="c7d38-170">Normalized data models **can require more round trips** to the server.</span><span class="sxs-lookup"><span data-stu-id="c7d38-170">Normalized data models **can require more round trips** to the server.</span></span>
> 
> 

### <a name="what-about-foreign-keys"></a><span data-ttu-id="c7d38-171">What about foreign keys?</span><span class="sxs-lookup"><span data-stu-id="c7d38-171">What about foreign keys?</span></span>
<span data-ttu-id="c7d38-172">Because there is currently no concept of a constraint, foreign-key or otherwise, any inter-document relationships that you have in documents are effectively "weak links" and will not be verified by the database itself.</span><span class="sxs-lookup"><span data-stu-id="c7d38-172">Because there is currently no concept of a constraint, foreign-key or otherwise, any inter-document relationships that you have in documents are effectively "weak links" and will not be verified by the database itself.</span></span> <span data-ttu-id="c7d38-173">If you want to ensure that the data a document is referring to actually exists, then you need to do this in your application, or through the use of server-side triggers or stored procedures on Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c7d38-173">If you want to ensure that the data a document is referring to actually exists, then you need to do this in your application, or through the use of server-side triggers or stored procedures on Azure Cosmos DB.</span></span>

### <a name="when-to-reference"></a><span data-ttu-id="c7d38-174">When to reference</span><span class="sxs-lookup"><span data-stu-id="c7d38-174">When to reference</span></span>
<span data-ttu-id="c7d38-175">In general, use normalized data models when:</span><span class="sxs-lookup"><span data-stu-id="c7d38-175">In general, use normalized data models when:</span></span>

* <span data-ttu-id="c7d38-176">Representing **one-to-many** relationships.</span><span class="sxs-lookup"><span data-stu-id="c7d38-176">Representing **one-to-many** relationships.</span></span>
* <span data-ttu-id="c7d38-177">Representing **many-to-many** relationships.</span><span class="sxs-lookup"><span data-stu-id="c7d38-177">Representing **many-to-many** relationships.</span></span>
* <span data-ttu-id="c7d38-178">Related data **changes frequently**.</span><span class="sxs-lookup"><span data-stu-id="c7d38-178">Related data **changes frequently**.</span></span>
* <span data-ttu-id="c7d38-179">Referenced data could be **unbounded**.</span><span class="sxs-lookup"><span data-stu-id="c7d38-179">Referenced data could be **unbounded**.</span></span>

> [!NOTE]
> <span data-ttu-id="c7d38-180">Typically normalizing provides better **write** performance.</span><span class="sxs-lookup"><span data-stu-id="c7d38-180">Typically normalizing provides better **write** performance.</span></span>
> 
> 

### <a name="where-do-i-put-the-relationship"></a><span data-ttu-id="c7d38-181">Where do I put the relationship?</span><span class="sxs-lookup"><span data-stu-id="c7d38-181">Where do I put the relationship?</span></span>
<span data-ttu-id="c7d38-182">The growth of the relationship will help determine in which document to store the reference.</span><span class="sxs-lookup"><span data-stu-id="c7d38-182">The growth of the relationship will help determine in which document to store the reference.</span></span>

<span data-ttu-id="c7d38-183">If we look at the JSON below that models publishers and books.</span><span class="sxs-lookup"><span data-stu-id="c7d38-183">If we look at the JSON below that models publishers and books.</span></span>

    Publisher document:
    {
        "id": "mspress",
        "name": "Microsoft Press",
        "books": [ 1, 2, 3, ..., 100, ..., 1000]
    }

    Book documents:
    {"id": "1", "name": "Azure Cosmos DB 101" }
    {"id": "2", "name": "Azure Cosmos DB for RDBMS Users" }
    {"id": "3", "name": "Taking over the world one JSON doc at a time" }
    ...
    {"id": "100", "name": "Learn about Azure Cosmos DB" }
    ...
    {"id": "1000", "name": "Deep Dive in to Azure Cosmos DB" }

<span data-ttu-id="c7d38-184">If the number of the books per publisher is small with limited growth, then storing the book reference inside the publisher document may be useful.</span><span class="sxs-lookup"><span data-stu-id="c7d38-184">If the number of the books per publisher is small with limited growth, then storing the book reference inside the publisher document may be useful.</span></span> <span data-ttu-id="c7d38-185">However, if the number of books per publisher is unbounded, then this data model would lead to mutable, growing arrays, as in the example publisher document above.</span><span class="sxs-lookup"><span data-stu-id="c7d38-185">However, if the number of books per publisher is unbounded, then this data model would lead to mutable, growing arrays, as in the example publisher document above.</span></span> 

<span data-ttu-id="c7d38-186">Switching things around a bit would result in a model that still represents the same data but now avoids these large mutable collections.</span><span class="sxs-lookup"><span data-stu-id="c7d38-186">Switching things around a bit would result in a model that still represents the same data but now avoids these large mutable collections.</span></span>

    Publisher document: 
    {
        "id": "mspress",
        "name": "Microsoft Press"
    }

    Book documents: 
    {"id": "1","name": "Azure Cosmos DB 101", "pub-id": "mspress"}
    {"id": "2","name": "Azure Cosmos DB for RDBMS Users", "pub-id": "mspress"}
    {"id": "3","name": "Taking over the world one JSON doc at a time"}
    ...
    {"id": "100","name": "Learn about Azure Cosmos DB", "pub-id": "mspress"}
    ...
    {"id": "1000","name": "Deep Dive in to Azure Cosmos DB", "pub-id": "mspress"}

<span data-ttu-id="c7d38-187">In the above example, we have dropped the unbounded collection on the publisher document.</span><span class="sxs-lookup"><span data-stu-id="c7d38-187">In the above example, we have dropped the unbounded collection on the publisher document.</span></span> <span data-ttu-id="c7d38-188">Instead we just have a reference to the publisher on each book document.</span><span class="sxs-lookup"><span data-stu-id="c7d38-188">Instead we just have a reference to the publisher on each book document.</span></span>

### <a name="how-do-i-model-manymany-relationships"></a><span data-ttu-id="c7d38-189">How do I model many:many relationships?</span><span class="sxs-lookup"><span data-stu-id="c7d38-189">How do I model many:many relationships?</span></span>
<span data-ttu-id="c7d38-190">In a relational database *many:many* relationships are often modeled with join tables, which just join records from other tables together.</span><span class="sxs-lookup"><span data-stu-id="c7d38-190">In a relational database *many:many* relationships are often modeled with join tables, which just join records from other tables together.</span></span> 

![Join tables](./media/sql-api-modeling-data/join-table.png)

<span data-ttu-id="c7d38-192">You might be tempted to replicate the same thing using documents and produce a data model that looks similar to the following.</span><span class="sxs-lookup"><span data-stu-id="c7d38-192">You might be tempted to replicate the same thing using documents and produce a data model that looks similar to the following.</span></span>

    Author documents: 
    {"id": "a1", "name": "Thomas Andersen" }
    {"id": "a2", "name": "William Wakefield" }

    Book documents:
    {"id": "b1", "name": "Azure Cosmos DB 101" }
    {"id": "b2", "name": "Azure Cosmos DB for RDBMS Users" }
    {"id": "b3", "name": "Taking over the world one JSON doc at a time" }
    {"id": "b4", "name": "Learn about Azure Cosmos DB" }
    {"id": "b5", "name": "Deep Dive in to Azure Cosmos DB" }

    Joining documents: 
    {"authorId": "a1", "bookId": "b1" }
    {"authorId": "a2", "bookId": "b1" }
    {"authorId": "a1", "bookId": "b2" }
    {"authorId": "a1", "bookId": "b3" }

<span data-ttu-id="c7d38-193">This would work.</span><span class="sxs-lookup"><span data-stu-id="c7d38-193">This would work.</span></span> <span data-ttu-id="c7d38-194">However, loading either an author with their books, or loading a book with its author, would always require at least two additional queries against the database.</span><span class="sxs-lookup"><span data-stu-id="c7d38-194">However, loading either an author with their books, or loading a book with its author, would always require at least two additional queries against the database.</span></span> <span data-ttu-id="c7d38-195">One query to the joining document and then another query to fetch the actual document being joined.</span><span class="sxs-lookup"><span data-stu-id="c7d38-195">One query to the joining document and then another query to fetch the actual document being joined.</span></span> 

<span data-ttu-id="c7d38-196">If all this join table is doing is gluing together two pieces of data, then why not drop it completely?</span><span class="sxs-lookup"><span data-stu-id="c7d38-196">If all this join table is doing is gluing together two pieces of data, then why not drop it completely?</span></span>
<span data-ttu-id="c7d38-197">Consider the following.</span><span class="sxs-lookup"><span data-stu-id="c7d38-197">Consider the following.</span></span>

    Author documents:
    {"id": "a1", "name": "Thomas Andersen", "books": ["b1, "b2", "b3"]}
    {"id": "a2", "name": "William Wakefield", "books": ["b1", "b4"]}

    Book documents: 
    {"id": "b1", "name": "Azure Cosmos DB 101", "authors": ["a1", "a2"]}
    {"id": "b2", "name": "Azure Cosmos DB for RDBMS Users", "authors": ["a1"]}
    {"id": "b3", "name": "Learn about Azure Cosmos DB", "authors": ["a1"]}
    {"id": "b4", "name": "Deep Dive in to Azure Cosmos DB", "authors": ["a2"]}

<span data-ttu-id="c7d38-198">Now, if I had an author, I immediately know which books they have written, and conversely if I had a book document loaded I would know the ids of the author(s).</span><span class="sxs-lookup"><span data-stu-id="c7d38-198">Now, if I had an author, I immediately know which books they have written, and conversely if I had a book document loaded I would know the ids of the author(s).</span></span> <span data-ttu-id="c7d38-199">This saves that intermediary query against the join table reducing the number of server round trips your application has to make.</span><span class="sxs-lookup"><span data-stu-id="c7d38-199">This saves that intermediary query against the join table reducing the number of server round trips your application has to make.</span></span> 

## <a id="WrapUp"></a><span data-ttu-id="c7d38-200">Hybrid data models</span><span class="sxs-lookup"><span data-stu-id="c7d38-200">Hybrid data models</span></span>
<span data-ttu-id="c7d38-201">We've now looked embedding (or denormalizing) and referencing (or normalizing) data, each have their upsides and each have compromises as we have seen.</span><span class="sxs-lookup"><span data-stu-id="c7d38-201">We've now looked embedding (or denormalizing) and referencing (or normalizing) data, each have their upsides and each have compromises as we have seen.</span></span> 

<span data-ttu-id="c7d38-202">It doesn't always have to be either or, don't be scared to mix things up a little.</span><span class="sxs-lookup"><span data-stu-id="c7d38-202">It doesn't always have to be either or, don't be scared to mix things up a little.</span></span> 

<span data-ttu-id="c7d38-203">Based on your application's specific usage patterns and workloads there may be cases where mixing embedded and referenced data makes sense and could lead to simpler application logic with fewer server round trips while still maintaining a good level of performance.</span><span class="sxs-lookup"><span data-stu-id="c7d38-203">Based on your application's specific usage patterns and workloads there may be cases where mixing embedded and referenced data makes sense and could lead to simpler application logic with fewer server round trips while still maintaining a good level of performance.</span></span>

<span data-ttu-id="c7d38-204">Consider the following JSON.</span><span class="sxs-lookup"><span data-stu-id="c7d38-204">Consider the following JSON.</span></span> 

    Author documents: 
    {
        "id": "a1",
        "firstName": "Thomas",
        "lastName": "Andersen",        
        "countOfBooks": 3,
         "books": ["b1", "b2", "b3"],
        "images": [
            {"thumbnail": "http://....png"}
            {"profile": "http://....png"}
            {"large": "http://....png"}
        ]
    },
    {
        "id": "a2",
        "firstName": "William",
        "lastName": "Wakefield",
        "countOfBooks": 1,
        "books": ["b1"],
        "images": [
            {"thumbnail": "http://....png"}
        ]
    }

    Book documents:
    {
        "id": "b1",
        "name": "Azure Cosmos DB 101",
        "authors": [
            {"id": "a1", "name": "Thomas Andersen", "thumbnailUrl": "http://....png"},
            {"id": "a2", "name": "William Wakefield", "thumbnailUrl": "http://....png"}
        ]
    },
    {
        "id": "b2",
        "name": "Azure Cosmos DB for RDBMS Users",
        "authors": [
            {"id": "a1", "name": "Thomas Andersen", "thumbnailUrl": "http://....png"},
        ]
    }

<span data-ttu-id="c7d38-205">Here we've (mostly) followed the embedded model, where data from other entities are embedded in the top-level document, but other data is referenced.</span><span class="sxs-lookup"><span data-stu-id="c7d38-205">Here we've (mostly) followed the embedded model, where data from other entities are embedded in the top-level document, but other data is referenced.</span></span> 

<span data-ttu-id="c7d38-206">If you look at the book document, we can see a few interesting fields when we look at the array of authors.</span><span class="sxs-lookup"><span data-stu-id="c7d38-206">If you look at the book document, we can see a few interesting fields when we look at the array of authors.</span></span> <span data-ttu-id="c7d38-207">There is an *id* field which is the field we use to refer back to an author document, standard practice in a normalized model, but then we also have *name* and *thumbnailUrl*.</span><span class="sxs-lookup"><span data-stu-id="c7d38-207">There is an *id* field which is the field we use to refer back to an author document, standard practice in a normalized model, but then we also have *name* and *thumbnailUrl*.</span></span> <span data-ttu-id="c7d38-208">We could've just stuck with *id* and left the application to get any additional information it needed from the respective author document using the "link", but because our application displays the author's name and a thumbnail picture with every book displayed we can save a round trip to the server per book in a list by denormalizing **some** data from the author.</span><span class="sxs-lookup"><span data-stu-id="c7d38-208">We could've just stuck with *id* and left the application to get any additional information it needed from the respective author document using the "link", but because our application displays the author's name and a thumbnail picture with every book displayed we can save a round trip to the server per book in a list by denormalizing **some** data from the author.</span></span>

<span data-ttu-id="c7d38-209">Sure, if the author's name changed or they wanted to update their photo we'd have to go an update every book they ever published but for our application, based on the assumption that authors don't change their names very often, this is an acceptable design decision.</span><span class="sxs-lookup"><span data-stu-id="c7d38-209">Sure, if the author's name changed or they wanted to update their photo we'd have to go an update every book they ever published but for our application, based on the assumption that authors don't change their names very often, this is an acceptable design decision.</span></span>  

<span data-ttu-id="c7d38-210">In the example there are **pre-calculated aggregates** values to save expensive processing on a read operation.</span><span class="sxs-lookup"><span data-stu-id="c7d38-210">In the example there are **pre-calculated aggregates** values to save expensive processing on a read operation.</span></span> <span data-ttu-id="c7d38-211">In the example, some of the data embedded in the author document is data that is calculated at run-time.</span><span class="sxs-lookup"><span data-stu-id="c7d38-211">In the example, some of the data embedded in the author document is data that is calculated at run-time.</span></span> <span data-ttu-id="c7d38-212">Every time a new book is published, a book document is created **and** the countOfBooks field is set to a calculated value based on the number of book documents that exist for a particular author.</span><span class="sxs-lookup"><span data-stu-id="c7d38-212">Every time a new book is published, a book document is created **and** the countOfBooks field is set to a calculated value based on the number of book documents that exist for a particular author.</span></span> <span data-ttu-id="c7d38-213">This optimization would be good in read heavy systems where we can afford to do computations on writes in order to optimize reads.</span><span class="sxs-lookup"><span data-stu-id="c7d38-213">This optimization would be good in read heavy systems where we can afford to do computations on writes in order to optimize reads.</span></span>

<span data-ttu-id="c7d38-214">The ability to have a model with pre-calculated fields is made possible because Azure Cosmos DB supports **multi-document transactions**.</span><span class="sxs-lookup"><span data-stu-id="c7d38-214">The ability to have a model with pre-calculated fields is made possible because Azure Cosmos DB supports **multi-document transactions**.</span></span> <span data-ttu-id="c7d38-215">Many NoSQL stores cannot do transactions across documents and therefore advocate design decisions, such as "always embed everything", due to this limitation.</span><span class="sxs-lookup"><span data-stu-id="c7d38-215">Many NoSQL stores cannot do transactions across documents and therefore advocate design decisions, such as "always embed everything", due to this limitation.</span></span> <span data-ttu-id="c7d38-216">With Azure Cosmos DB, you can use server-side triggers, or stored procedures, that insert books and update authors all within an ACID transaction.</span><span class="sxs-lookup"><span data-stu-id="c7d38-216">With Azure Cosmos DB, you can use server-side triggers, or stored procedures, that insert books and update authors all within an ACID transaction.</span></span> <span data-ttu-id="c7d38-217">Now you don't **have** to embed everything in to one document just to be sure that your data remains consistent.</span><span class="sxs-lookup"><span data-stu-id="c7d38-217">Now you don't **have** to embed everything in to one document just to be sure that your data remains consistent.</span></span>

## <a name="NextSteps"></a><span data-ttu-id="c7d38-218">Next steps</span><span class="sxs-lookup"><span data-stu-id="c7d38-218">Next steps</span></span>
<span data-ttu-id="c7d38-219">The biggest takeaways from this article is to understand that data modeling in a schema-free world is just as important as ever.</span><span class="sxs-lookup"><span data-stu-id="c7d38-219">The biggest takeaways from this article is to understand that data modeling in a schema-free world is just as important as ever.</span></span> 

<span data-ttu-id="c7d38-220">Just as there is no single way to represent a piece of data on a screen, there is no single way to model your data.</span><span class="sxs-lookup"><span data-stu-id="c7d38-220">Just as there is no single way to represent a piece of data on a screen, there is no single way to model your data.</span></span> <span data-ttu-id="c7d38-221">You need to understand your application and how it will produce, consume, and process the data.</span><span class="sxs-lookup"><span data-stu-id="c7d38-221">You need to understand your application and how it will produce, consume, and process the data.</span></span> <span data-ttu-id="c7d38-222">Then, by applying some of the guidelines presented here you can set about creating a model that addresses the immediate needs of your application.</span><span class="sxs-lookup"><span data-stu-id="c7d38-222">Then, by applying some of the guidelines presented here you can set about creating a model that addresses the immediate needs of your application.</span></span> <span data-ttu-id="c7d38-223">When your applications need to change, you can leverage the flexibility of a schema-free database to embrace that change and evolve your data model easily.</span><span class="sxs-lookup"><span data-stu-id="c7d38-223">When your applications need to change, you can leverage the flexibility of a schema-free database to embrace that change and evolve your data model easily.</span></span> 

<span data-ttu-id="c7d38-224">To learn more about Azure Cosmos DB, refer to the service's [documentation](https://azure.microsoft.com/documentation/services/cosmos-db/) page.</span><span class="sxs-lookup"><span data-stu-id="c7d38-224">To learn more about Azure Cosmos DB, refer to the service's [documentation](https://azure.microsoft.com/documentation/services/cosmos-db/) page.</span></span> 

<span data-ttu-id="c7d38-225">To understand how to shard your data across multiple partitions, refer to [Partitioning Data in Azure Cosmos DB](sql-api-partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="c7d38-225">To understand how to shard your data across multiple partitions, refer to [Partitioning Data in Azure Cosmos DB](sql-api-partition-data.md).</span></span> 
