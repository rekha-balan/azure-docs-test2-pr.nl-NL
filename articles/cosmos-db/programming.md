---
title: Server-side JavaScript programming for Azure Cosmos DB | Microsoft Docs
description: Learn how to use Azure Cosmos DB to write stored procedures, database triggers, and user defined functions (UDFs) in JavaScript. Get database programing tips and more.
keywords: Database triggers, stored procedure, stored procedure, database program, sproc, azure, Microsoft azure
services: cosmos-db
author: aliuy
manager: kfile
ms.service: cosmos-db
ms.devlang: na
ms.topic: conceptual
ms.date: 03/26/2018
ms.author: andrl
ms.openlocfilehash: 3c18478fb2996178ee0b75870ce63dfc79ad4c4c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869280"
---
# <a name="azure-cosmos-db-server-side-programming-stored-procedures-database-triggers-and-udfs"></a><span data-ttu-id="f96df-105">Azure Cosmos DB server-side programming: Stored procedures, database triggers, and UDFs</span><span class="sxs-lookup"><span data-stu-id="f96df-105">Azure Cosmos DB server-side programming: Stored procedures, database triggers, and UDFs</span></span>

<span data-ttu-id="f96df-106">Learn how Azure Cosmos DB's language-integrated, transactional execution of JavaScript lets developers write **stored procedures**, **triggers**, and **user-defined functions (UDFs)** natively in an [ECMAScript 2015](http://www.ecma-international.org/ecma-262/6.0/) JavaScript.</span><span class="sxs-lookup"><span data-stu-id="f96df-106">Learn how Azure Cosmos DB's language-integrated, transactional execution of JavaScript lets developers write **stored procedures**, **triggers**, and **user-defined functions (UDFs)** natively in an [ECMAScript 2015](http://www.ecma-international.org/ecma-262/6.0/) JavaScript.</span></span> <span data-ttu-id="f96df-107">Javascript integration enables you to write program logic that can be shipped and executed directly within the database storage partitions.</span><span class="sxs-lookup"><span data-stu-id="f96df-107">Javascript integration enables you to write program logic that can be shipped and executed directly within the database storage partitions.</span></span> 

<span data-ttu-id="f96df-108">In this article you'll learn the answers to the following questions:</span><span class="sxs-lookup"><span data-stu-id="f96df-108">In this article you'll learn the answers to the following questions:</span></span>  

* <span data-ttu-id="f96df-109">How do I write a stored procedure, trigger, or UDF using JavaScript?</span><span class="sxs-lookup"><span data-stu-id="f96df-109">How do I write a stored procedure, trigger, or UDF using JavaScript?</span></span>
* <span data-ttu-id="f96df-110">How does Cosmos DB guarantee ACID?</span><span class="sxs-lookup"><span data-stu-id="f96df-110">How does Cosmos DB guarantee ACID?</span></span>
* <span data-ttu-id="f96df-111">How do transactions work in Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="f96df-111">How do transactions work in Cosmos DB?</span></span>
* <span data-ttu-id="f96df-112">What are pre-triggers and post-triggers and how do I write one?</span><span class="sxs-lookup"><span data-stu-id="f96df-112">What are pre-triggers and post-triggers and how do I write one?</span></span>
* <span data-ttu-id="f96df-113">How do I register and execute a stored procedure, trigger, or UDF in a RESTful manner by using HTTP?</span><span class="sxs-lookup"><span data-stu-id="f96df-113">How do I register and execute a stored procedure, trigger, or UDF in a RESTful manner by using HTTP?</span></span>
* <span data-ttu-id="f96df-114">What Cosmos DB SDKs are available to create and execute stored procedures, triggers, and UDFs?</span><span class="sxs-lookup"><span data-stu-id="f96df-114">What Cosmos DB SDKs are available to create and execute stored procedures, triggers, and UDFs?</span></span>

## <a name="introduction-to-stored-procedure-and-udf-programming"></a><span data-ttu-id="f96df-115">Introduction to Stored Procedure and UDF Programming</span><span class="sxs-lookup"><span data-stu-id="f96df-115">Introduction to Stored Procedure and UDF Programming</span></span>
<span data-ttu-id="f96df-116">This approach of *"JavaScript as a modern day T-SQL"* frees application developers from the complexities of type system mismatches and object-relational mapping technologies.</span><span class="sxs-lookup"><span data-stu-id="f96df-116">This approach of *"JavaScript as a modern day T-SQL"* frees application developers from the complexities of type system mismatches and object-relational mapping technologies.</span></span> <span data-ttu-id="f96df-117">It also has a number of intrinsic advantages that can be utilized to build rich applications:</span><span class="sxs-lookup"><span data-stu-id="f96df-117">It also has a number of intrinsic advantages that can be utilized to build rich applications:</span></span>  

* <span data-ttu-id="f96df-118">**Procedural Logic:** JavaScript as a high-level programming language, provides a rich and familiar interface to express business logic.</span><span class="sxs-lookup"><span data-stu-id="f96df-118">**Procedural Logic:** JavaScript as a high-level programming language, provides a rich and familiar interface to express business logic.</span></span> <span data-ttu-id="f96df-119">You can perform complex sequences of operations closer to the data.</span><span class="sxs-lookup"><span data-stu-id="f96df-119">You can perform complex sequences of operations closer to the data.</span></span>
* <span data-ttu-id="f96df-120">**Atomic Transactions:** Cosmos DB guarantees that database operations performed inside a single stored procedure or trigger are atomic.</span><span class="sxs-lookup"><span data-stu-id="f96df-120">**Atomic Transactions:** Cosmos DB guarantees that database operations performed inside a single stored procedure or trigger are atomic.</span></span> <span data-ttu-id="f96df-121">This atomic functionality lets an application combine related operations in a single batch so that either all of them succeed or none of them succeed.</span><span class="sxs-lookup"><span data-stu-id="f96df-121">This atomic functionality lets an application combine related operations in a single batch so that either all of them succeed or none of them succeed.</span></span> 
* <span data-ttu-id="f96df-122">**Performance:** The fact that JSON is intrinsically mapped to the Javascript language type system and is also the basic unit of storage in Cosmos DB allows for a number of optimizations like lazy materialization of JSON documents in the buffer pool and making them available on-demand to the executing code.</span><span class="sxs-lookup"><span data-stu-id="f96df-122">**Performance:** The fact that JSON is intrinsically mapped to the Javascript language type system and is also the basic unit of storage in Cosmos DB allows for a number of optimizations like lazy materialization of JSON documents in the buffer pool and making them available on-demand to the executing code.</span></span> <span data-ttu-id="f96df-123">There are more performance benefits associated with shipping business logic to the database:</span><span class="sxs-lookup"><span data-stu-id="f96df-123">There are more performance benefits associated with shipping business logic to the database:</span></span>
  
  * <span data-ttu-id="f96df-124">Batching – Developers can group operations like inserts and submit them in bulk.</span><span class="sxs-lookup"><span data-stu-id="f96df-124">Batching – Developers can group operations like inserts and submit them in bulk.</span></span> <span data-ttu-id="f96df-125">The network traffic latency cost and the store overhead to create separate transactions are reduced significantly.</span><span class="sxs-lookup"><span data-stu-id="f96df-125">The network traffic latency cost and the store overhead to create separate transactions are reduced significantly.</span></span> 
  * <span data-ttu-id="f96df-126">Pre-compilation – Cosmos DB precompiles stored procedures, triggers, and user-defined functions (UDFs) to avoid JavaScript compilation cost for each invocation.</span><span class="sxs-lookup"><span data-stu-id="f96df-126">Pre-compilation – Cosmos DB precompiles stored procedures, triggers, and user-defined functions (UDFs) to avoid JavaScript compilation cost for each invocation.</span></span> <span data-ttu-id="f96df-127">The overhead of building the byte code for the procedural logic is amortized to a minimal value.</span><span class="sxs-lookup"><span data-stu-id="f96df-127">The overhead of building the byte code for the procedural logic is amortized to a minimal value.</span></span>
  * <span data-ttu-id="f96df-128">Sequencing – Many operations need a side-effect ("trigger") that potentially involves doing one or many secondary store operations.</span><span class="sxs-lookup"><span data-stu-id="f96df-128">Sequencing – Many operations need a side-effect ("trigger") that potentially involves doing one or many secondary store operations.</span></span> <span data-ttu-id="f96df-129">Aside from atomicity, this is more performant when moved to the server.</span><span class="sxs-lookup"><span data-stu-id="f96df-129">Aside from atomicity, this is more performant when moved to the server.</span></span> 
* <span data-ttu-id="f96df-130">**Encapsulation:** Stored procedures can be used to group business logic in one place, which has two advantages:</span><span class="sxs-lookup"><span data-stu-id="f96df-130">**Encapsulation:** Stored procedures can be used to group business logic in one place, which has two advantages:</span></span>
  * <span data-ttu-id="f96df-131">It adds an abstraction layer on top of the raw data, which enables data architects to evolve their applications independently from the data.</span><span class="sxs-lookup"><span data-stu-id="f96df-131">It adds an abstraction layer on top of the raw data, which enables data architects to evolve their applications independently from the data.</span></span> <span data-ttu-id="f96df-132">This layer of abstraction is advantageous when the data is schema-less, due to the brittle assumptions that may need to be baked into the application if they have to deal with data directly.</span><span class="sxs-lookup"><span data-stu-id="f96df-132">This layer of abstraction is advantageous when the data is schema-less, due to the brittle assumptions that may need to be baked into the application if they have to deal with data directly.</span></span>  
  * <span data-ttu-id="f96df-133">This abstraction lets enterprises keep their data secure by streamlining the access from the scripts.</span><span class="sxs-lookup"><span data-stu-id="f96df-133">This abstraction lets enterprises keep their data secure by streamlining the access from the scripts.</span></span>  

<span data-ttu-id="f96df-134">The creation and execution of database triggers, stored procedures, and custom query operators is supported through the [Azure portal](https://portal.azure.com), the [REST API](/rest/api/cosmos-db/), [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio/releases), and [client SDKs](sql-api-sdk-dotnet.md) in many platforms including .NET, Node.js, and JavaScript.</span><span class="sxs-lookup"><span data-stu-id="f96df-134">The creation and execution of database triggers, stored procedures, and custom query operators is supported through the [Azure portal](https://portal.azure.com), the [REST API](/rest/api/cosmos-db/), [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio/releases), and [client SDKs](sql-api-sdk-dotnet.md) in many platforms including .NET, Node.js, and JavaScript.</span></span>

<span data-ttu-id="f96df-135">This tutorial uses the [Node.js SDK with Q Promises](http://azure.github.io/azure-documentdb-node-q/) to illustrate syntax and usage of stored procedures, triggers, and UDFs.</span><span class="sxs-lookup"><span data-stu-id="f96df-135">This tutorial uses the [Node.js SDK with Q Promises](http://azure.github.io/azure-documentdb-node-q/) to illustrate syntax and usage of stored procedures, triggers, and UDFs.</span></span>   

## <a name="stored-procedures"></a><span data-ttu-id="f96df-136">Stored procedures</span><span class="sxs-lookup"><span data-stu-id="f96df-136">Stored procedures</span></span>
### <a name="example-write-a-stored-procedure"></a><span data-ttu-id="f96df-137">Example: Write a stored procedure</span><span class="sxs-lookup"><span data-stu-id="f96df-137">Example: Write a stored procedure</span></span>
<span data-ttu-id="f96df-138">Let’s start with a simple stored procedure that returns a "Hello World" response.</span><span class="sxs-lookup"><span data-stu-id="f96df-138">Let’s start with a simple stored procedure that returns a "Hello World" response.</span></span>

```javascript
var helloWorldStoredProc = {
    id: "helloWorld",
    serverScript: function () {
        var context = getContext();
        var response = context.getResponse();

        response.setBody("Hello, World");
    }
}
```

<span data-ttu-id="f96df-139">Stored procedures are registered per collection, and can operate on any document and attachment present in that collection.</span><span class="sxs-lookup"><span data-stu-id="f96df-139">Stored procedures are registered per collection, and can operate on any document and attachment present in that collection.</span></span> <span data-ttu-id="f96df-140">The following snippet shows how to register the helloWorld stored procedure with a collection.</span><span class="sxs-lookup"><span data-stu-id="f96df-140">The following snippet shows how to register the helloWorld stored procedure with a collection.</span></span> 


```javascript
// register the stored procedure
var createdStoredProcedure;
client.createStoredProcedureAsync('dbs/testdb/colls/testColl', helloWorldStoredProc)
    .then(function (response) {
        createdStoredProcedure = response.resource;
        console.log("Successfully created stored procedure");
    }, function (error) {
        console.log("Error", error);
    });
```


<span data-ttu-id="f96df-141">Once the stored procedure is registered, you can execute it against the collection, and read the results back at the client.</span><span class="sxs-lookup"><span data-stu-id="f96df-141">Once the stored procedure is registered, you can execute it against the collection, and read the results back at the client.</span></span> 

```javascript
// execute the stored procedure
client.executeStoredProcedureAsync('dbs/testdb/colls/testColl/sprocs/helloWorld')
    .then(function (response) {
        console.log(response.result); // "Hello, World"
    }, function (err) {
        console.log("Error", error);
    });
```

<span data-ttu-id="f96df-142">The context object provides access to all operations that can be performed on Cosmos DB storage, as well as access to the request and response objects.</span><span class="sxs-lookup"><span data-stu-id="f96df-142">The context object provides access to all operations that can be performed on Cosmos DB storage, as well as access to the request and response objects.</span></span> <span data-ttu-id="f96df-143">In this case, you use the response object to set the body of the response that was sent back to the client.</span><span class="sxs-lookup"><span data-stu-id="f96df-143">In this case, you use the response object to set the body of the response that was sent back to the client.</span></span> <span data-ttu-id="f96df-144">For more information, see the [Azure Cosmos DB JavaScript server SDK documentation](https://azure.github.io/azure-cosmosdb-js-server/).</span><span class="sxs-lookup"><span data-stu-id="f96df-144">For more information, see the [Azure Cosmos DB JavaScript server SDK documentation](https://azure.github.io/azure-cosmosdb-js-server/).</span></span>  

<span data-ttu-id="f96df-145">Let us expand on this example and add more database-related functionality to the stored procedure.</span><span class="sxs-lookup"><span data-stu-id="f96df-145">Let us expand on this example and add more database-related functionality to the stored procedure.</span></span> <span data-ttu-id="f96df-146">Stored procedures can create, update, read, query, and delete documents and attachments inside the collection.</span><span class="sxs-lookup"><span data-stu-id="f96df-146">Stored procedures can create, update, read, query, and delete documents and attachments inside the collection.</span></span>    

### <a name="example-write-a-stored-procedure-to-create-a-document"></a><span data-ttu-id="f96df-147">Example: Write a stored procedure to create a document</span><span class="sxs-lookup"><span data-stu-id="f96df-147">Example: Write a stored procedure to create a document</span></span>
<span data-ttu-id="f96df-148">The next snippet shows how to use the context object to interact with Cosmos DB resources.</span><span class="sxs-lookup"><span data-stu-id="f96df-148">The next snippet shows how to use the context object to interact with Cosmos DB resources.</span></span>

```javascript
var createDocumentStoredProc = {
    id: "createMyDocument",
    serverScript: function createMyDocument(documentToCreate) {
        var context = getContext();
        var collection = context.getCollection();

        var accepted = collection.createDocument(collection.getSelfLink(),
              documentToCreate,
              function (err, documentCreated) {
                  if (err) throw new Error('Error' + err.message);
                  context.getResponse().setBody(documentCreated.id)
              });
        if (!accepted) return;
    }
}
```


<span data-ttu-id="f96df-149">This stored procedure takes as input documentToCreate, the body of a document to be created in the current collection.</span><span class="sxs-lookup"><span data-stu-id="f96df-149">This stored procedure takes as input documentToCreate, the body of a document to be created in the current collection.</span></span> <span data-ttu-id="f96df-150">All such operations are asynchronous and depend on JavaScript function callbacks.</span><span class="sxs-lookup"><span data-stu-id="f96df-150">All such operations are asynchronous and depend on JavaScript function callbacks.</span></span> <span data-ttu-id="f96df-151">The callback function has two parameters, one for the error object in case the operation fails, and one for the created object.</span><span class="sxs-lookup"><span data-stu-id="f96df-151">The callback function has two parameters, one for the error object in case the operation fails, and one for the created object.</span></span> <span data-ttu-id="f96df-152">Inside the callback, users can either handle the exception or throw an error.</span><span class="sxs-lookup"><span data-stu-id="f96df-152">Inside the callback, users can either handle the exception or throw an error.</span></span> <span data-ttu-id="f96df-153">In case a callback is not provided and there is an error, the Azure Cosmos DB runtime throws an error.</span><span class="sxs-lookup"><span data-stu-id="f96df-153">In case a callback is not provided and there is an error, the Azure Cosmos DB runtime throws an error.</span></span>   

<span data-ttu-id="f96df-154">In the example above, the callback throws an error if the operation failed.</span><span class="sxs-lookup"><span data-stu-id="f96df-154">In the example above, the callback throws an error if the operation failed.</span></span> <span data-ttu-id="f96df-155">Otherwise, it sets the ID of the created document as the body of the response to the client.</span><span class="sxs-lookup"><span data-stu-id="f96df-155">Otherwise, it sets the ID of the created document as the body of the response to the client.</span></span> <span data-ttu-id="f96df-156">Here is how this stored procedure is executed with input parameters.</span><span class="sxs-lookup"><span data-stu-id="f96df-156">Here is how this stored procedure is executed with input parameters.</span></span>

```javascript
// register the stored procedure
client.createStoredProcedureAsync('dbs/testdb/colls/testColl', createDocumentStoredProc)
    .then(function (response) {
        var createdStoredProcedure = response.resource;

        // run stored procedure to create a document
        var docToCreate = {
            id: "DocFromSproc",
            book: "The Hitchhiker’s Guide to the Galaxy",
            author: "Douglas Adams"
        };

        return client.executeStoredProcedureAsync('dbs/testdb/colls/testColl/sprocs/createMyDocument',
              docToCreate);
    }, function (error) {
        console.log("Error", error);
    })
.then(function (response) {
    console.log(response); // "DocFromSproc"
}, function (error) {
    console.log("Error", error);
});
```

<span data-ttu-id="f96df-157">This stored procedure can be modified to take an array of document bodies as input and create them all in the same stored procedure execution instead of multiple requests to create each of them individually.</span><span class="sxs-lookup"><span data-stu-id="f96df-157">This stored procedure can be modified to take an array of document bodies as input and create them all in the same stored procedure execution instead of multiple requests to create each of them individually.</span></span> <span data-ttu-id="f96df-158">This stored procedure can be used to implement an efficient bulk importer for Cosmos DB (discussed later in this tutorial).</span><span class="sxs-lookup"><span data-stu-id="f96df-158">This stored procedure can be used to implement an efficient bulk importer for Cosmos DB (discussed later in this tutorial).</span></span>   

<span data-ttu-id="f96df-159">The example described demonstrated how to use stored procedures.</span><span class="sxs-lookup"><span data-stu-id="f96df-159">The example described demonstrated how to use stored procedures.</span></span> <span data-ttu-id="f96df-160">Next you will learn about triggers and user-defined functions (UDFs) later in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="f96df-160">Next you will learn about triggers and user-defined functions (UDFs) later in the tutorial.</span></span>

### <a name="known-issues"></a><span data-ttu-id="f96df-161">Known issues</span><span class="sxs-lookup"><span data-stu-id="f96df-161">Known issues</span></span>

<span data-ttu-id="f96df-162">When defining a stored procedure by using Azure portal, input parameters are always sent as a string to the stored procedure.</span><span class="sxs-lookup"><span data-stu-id="f96df-162">When defining a stored procedure by using Azure portal, input parameters are always sent as a string to the stored procedure.</span></span> <span data-ttu-id="f96df-163">Even if you pass an array of strings as an input, the array is converted to string and sent to the stored procedure.</span><span class="sxs-lookup"><span data-stu-id="f96df-163">Even if you pass an array of strings as an input, the array is converted to string and sent to the stored procedure.</span></span> <span data-ttu-id="f96df-164">To workaround this issue, you can define a function within your stored procedure to parse the string as an array.</span><span class="sxs-lookup"><span data-stu-id="f96df-164">To workaround this issue, you can define a function within your stored procedure to parse the string as an array.</span></span> <span data-ttu-id="f96df-165">The following code is an example to parse the string as an array:</span><span class="sxs-lookup"><span data-stu-id="f96df-165">The following code is an example to parse the string as an array:</span></span> 

```javascript
function sample(arr) {
    if (typeof arr === "string") arr = JSON.parse(arr);
    
    arr.forEach(function(a) {
        // do something here
        console.log(a);
    });
}
```

## <a name="database-program-transactions"></a><span data-ttu-id="f96df-166">Database program transactions</span><span class="sxs-lookup"><span data-stu-id="f96df-166">Database program transactions</span></span>
<span data-ttu-id="f96df-167">Transaction in a typical database can be defined as a sequence of operations performed as a single logical unit of work.</span><span class="sxs-lookup"><span data-stu-id="f96df-167">Transaction in a typical database can be defined as a sequence of operations performed as a single logical unit of work.</span></span> <span data-ttu-id="f96df-168">Each transaction provides **ACID guarantees**.</span><span class="sxs-lookup"><span data-stu-id="f96df-168">Each transaction provides **ACID guarantees**.</span></span> <span data-ttu-id="f96df-169">ACID is a well-known acronym that stands for four properties -  Atomicity, Consistency, Isolation, and Durability.</span><span class="sxs-lookup"><span data-stu-id="f96df-169">ACID is a well-known acronym that stands for four properties -  Atomicity, Consistency, Isolation, and Durability.</span></span>  

<span data-ttu-id="f96df-170">Briefly, atomicity guarantees that all the work done inside a transaction is treated as a single unit where either all of it is committed or none.</span><span class="sxs-lookup"><span data-stu-id="f96df-170">Briefly, atomicity guarantees that all the work done inside a transaction is treated as a single unit where either all of it is committed or none.</span></span> <span data-ttu-id="f96df-171">Consistency makes sure that the data is always in a good internal state across transactions.</span><span class="sxs-lookup"><span data-stu-id="f96df-171">Consistency makes sure that the data is always in a good internal state across transactions.</span></span> <span data-ttu-id="f96df-172">Isolation guarantees that no two transactions interfere with each other – generally, most commercial systems provide multiple isolation levels that can be used based on the application needs.</span><span class="sxs-lookup"><span data-stu-id="f96df-172">Isolation guarantees that no two transactions interfere with each other – generally, most commercial systems provide multiple isolation levels that can be used based on the application needs.</span></span> <span data-ttu-id="f96df-173">Durability ensures that any change that’s committed in the database will always be present.</span><span class="sxs-lookup"><span data-stu-id="f96df-173">Durability ensures that any change that’s committed in the database will always be present.</span></span>   

<span data-ttu-id="f96df-174">In Cosmos DB, JavaScript is hosted in the same memory space as the database.</span><span class="sxs-lookup"><span data-stu-id="f96df-174">In Cosmos DB, JavaScript is hosted in the same memory space as the database.</span></span> <span data-ttu-id="f96df-175">Hence, requests made within stored procedures and triggers execute in the same scope of a database session.</span><span class="sxs-lookup"><span data-stu-id="f96df-175">Hence, requests made within stored procedures and triggers execute in the same scope of a database session.</span></span> <span data-ttu-id="f96df-176">This feature enables Cosmos DB to guarantee ACID for all operations that are part of a single stored procedure/trigger.</span><span class="sxs-lookup"><span data-stu-id="f96df-176">This feature enables Cosmos DB to guarantee ACID for all operations that are part of a single stored procedure/trigger.</span></span> <span data-ttu-id="f96df-177">Consider the following stored procedure definition:</span><span class="sxs-lookup"><span data-stu-id="f96df-177">Consider the following stored procedure definition:</span></span>

```javascript
// JavaScript source code
var exchangeItemsSproc = {
    id: "exchangeItems",
    serverScript: function (playerId1, playerId2) {
        var context = getContext();
        var collection = context.getCollection();
        var response = context.getResponse();

        var player1Document, player2Document;

        // query for players
        var filterQuery = 'SELECT * FROM Players p where p.id  = "' + playerId1 + '"';
        var accept = collection.queryDocuments(collection.getSelfLink(), filterQuery, {},
            function (err, documents, responseOptions) {
                if (err) throw new Error("Error" + err.message);

                if (documents.length != 1) throw "Unable to find both names";
                player1Document = documents[0];

                var filterQuery2 = 'SELECT * FROM Players p where p.id = "' + playerId2 + '"';
                var accept2 = collection.queryDocuments(collection.getSelfLink(), filterQuery2, {},
                    function (err2, documents2, responseOptions2) {
                        if (err2) throw new Error("Error" + err2.message);
                        if (documents2.length != 1) throw "Unable to find both names";
                        player2Document = documents2[0];
                        swapItems(player1Document, player2Document);
                        return;
                    });
                if (!accept2) throw "Unable to read player details, abort ";
            });

        if (!accept) throw "Unable to read player details, abort ";

        // swap the two players’ items
        function swapItems(player1, player2) {
            var player1ItemSave = player1.item;
            player1.item = player2.item;
            player2.item = player1ItemSave;

            var accept = collection.replaceDocument(player1._self, player1,
                function (err, docReplaced) {
                    if (err) throw "Unable to update player 1, abort ";

                    var accept2 = collection.replaceDocument(player2._self, player2,
                        function (err2, docReplaced2) {
                            if (err) throw "Unable to update player 2, abort"
                        });

                    if (!accept2) throw "Unable to update player 2, abort";
                });

            if (!accept) throw "Unable to update player 1, abort";
        }
    }
}

// register the stored procedure in Node.js client
client.createStoredProcedureAsync(collection._self, exchangeItemsSproc)
    .then(function (response) {
        var createdStoredProcedure = response.resource;
    }
);
```

<span data-ttu-id="f96df-178">This stored procedure uses transactions within a gaming app to trade items between two players in a single operation.</span><span class="sxs-lookup"><span data-stu-id="f96df-178">This stored procedure uses transactions within a gaming app to trade items between two players in a single operation.</span></span> <span data-ttu-id="f96df-179">The stored procedure attempts to read two documents each corresponding to the player IDs passed in as an argument.</span><span class="sxs-lookup"><span data-stu-id="f96df-179">The stored procedure attempts to read two documents each corresponding to the player IDs passed in as an argument.</span></span> <span data-ttu-id="f96df-180">If both player documents are found, then the stored procedure updates the documents by swapping their items.</span><span class="sxs-lookup"><span data-stu-id="f96df-180">If both player documents are found, then the stored procedure updates the documents by swapping their items.</span></span> <span data-ttu-id="f96df-181">If any errors are encountered along the way, it throws a JavaScript exception that implicitly aborts the transaction.</span><span class="sxs-lookup"><span data-stu-id="f96df-181">If any errors are encountered along the way, it throws a JavaScript exception that implicitly aborts the transaction.</span></span>

<span data-ttu-id="f96df-182">If the collection the stored procedure is registered against is a single-partition collection, then the transaction is scoped to all the documents within the collection.</span><span class="sxs-lookup"><span data-stu-id="f96df-182">If the collection the stored procedure is registered against is a single-partition collection, then the transaction is scoped to all the documents within the collection.</span></span> <span data-ttu-id="f96df-183">If the collection is partitioned, then stored procedures are executed in the transaction scope of a single partition key.</span><span class="sxs-lookup"><span data-stu-id="f96df-183">If the collection is partitioned, then stored procedures are executed in the transaction scope of a single partition key.</span></span> <span data-ttu-id="f96df-184">Each stored procedure execution must then include a partition key value corresponding to the scope the transaction must run under.</span><span class="sxs-lookup"><span data-stu-id="f96df-184">Each stored procedure execution must then include a partition key value corresponding to the scope the transaction must run under.</span></span> <span data-ttu-id="f96df-185">For more information, see [Azure Cosmos DB Partitioning](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="f96df-185">For more information, see [Azure Cosmos DB Partitioning](partition-data.md).</span></span>

### <a name="commit-and-rollback"></a><span data-ttu-id="f96df-186">Commit and rollback</span><span class="sxs-lookup"><span data-stu-id="f96df-186">Commit and rollback</span></span>
<span data-ttu-id="f96df-187">Transactions are deeply and natively integrated into Cosmos DB’s JavaScript programming model.</span><span class="sxs-lookup"><span data-stu-id="f96df-187">Transactions are deeply and natively integrated into Cosmos DB’s JavaScript programming model.</span></span> <span data-ttu-id="f96df-188">Inside a JavaScript function, all operations are automatically wrapped under a single transaction.</span><span class="sxs-lookup"><span data-stu-id="f96df-188">Inside a JavaScript function, all operations are automatically wrapped under a single transaction.</span></span> <span data-ttu-id="f96df-189">If the JavaScript completes without any exception, the operations to the database are committed.</span><span class="sxs-lookup"><span data-stu-id="f96df-189">If the JavaScript completes without any exception, the operations to the database are committed.</span></span> <span data-ttu-id="f96df-190">In effect, the "BEGIN TRANSACTION" and "COMMIT TRANSACTION" statements in relational databases are implicit in Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f96df-190">In effect, the "BEGIN TRANSACTION" and "COMMIT TRANSACTION" statements in relational databases are implicit in Cosmos DB.</span></span>  

<span data-ttu-id="f96df-191">If there is any exception that’s propagated from the script, Cosmos DB’s JavaScript runtime will roll back the whole transaction.</span><span class="sxs-lookup"><span data-stu-id="f96df-191">If there is any exception that’s propagated from the script, Cosmos DB’s JavaScript runtime will roll back the whole transaction.</span></span> <span data-ttu-id="f96df-192">As shown in the earlier example, throwing an exception is effectively equivalent to a "ROLLBACK TRANSACTION" in Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f96df-192">As shown in the earlier example, throwing an exception is effectively equivalent to a "ROLLBACK TRANSACTION" in Cosmos DB.</span></span>

### <a name="data-consistency"></a><span data-ttu-id="f96df-193">Data consistency</span><span class="sxs-lookup"><span data-stu-id="f96df-193">Data consistency</span></span>
<span data-ttu-id="f96df-194">Stored procedures and triggers are always executed on the primary replica of the Azure Cosmos DB container.</span><span class="sxs-lookup"><span data-stu-id="f96df-194">Stored procedures and triggers are always executed on the primary replica of the Azure Cosmos DB container.</span></span> <span data-ttu-id="f96df-195">This ensures that reads from inside stored procedures offer strong consistency.</span><span class="sxs-lookup"><span data-stu-id="f96df-195">This ensures that reads from inside stored procedures offer strong consistency.</span></span> <span data-ttu-id="f96df-196">Queries using user-defined functions can be executed on the primary or any secondary replica, but you ensure to meet the requested consistency level by choosing the appropriate replica.</span><span class="sxs-lookup"><span data-stu-id="f96df-196">Queries using user-defined functions can be executed on the primary or any secondary replica, but you ensure to meet the requested consistency level by choosing the appropriate replica.</span></span>

## <a name="bounded-execution"></a><span data-ttu-id="f96df-197">Bounded execution</span><span class="sxs-lookup"><span data-stu-id="f96df-197">Bounded execution</span></span>
<span data-ttu-id="f96df-198">All Cosmos DB operations must complete within the server specified request timeout duration.</span><span class="sxs-lookup"><span data-stu-id="f96df-198">All Cosmos DB operations must complete within the server specified request timeout duration.</span></span> <span data-ttu-id="f96df-199">This constraint also applies to JavaScript functions (stored procedures, triggers, and user-defined functions).</span><span class="sxs-lookup"><span data-stu-id="f96df-199">This constraint also applies to JavaScript functions (stored procedures, triggers, and user-defined functions).</span></span> <span data-ttu-id="f96df-200">If an operation does not complete with that time limit, the transaction is rolled back.</span><span class="sxs-lookup"><span data-stu-id="f96df-200">If an operation does not complete with that time limit, the transaction is rolled back.</span></span> <span data-ttu-id="f96df-201">JavaScript functions must finish within the time limit or implement a continuation-based model to batch/resume execution.</span><span class="sxs-lookup"><span data-stu-id="f96df-201">JavaScript functions must finish within the time limit or implement a continuation-based model to batch/resume execution.</span></span>  

<span data-ttu-id="f96df-202">In order to simplify development of stored procedures and triggers to handle time limits, all functions under the collection object (for create, read, replace, and delete of documents and attachments) return a Boolean value that represents whether that operation will complete.</span><span class="sxs-lookup"><span data-stu-id="f96df-202">In order to simplify development of stored procedures and triggers to handle time limits, all functions under the collection object (for create, read, replace, and delete of documents and attachments) return a Boolean value that represents whether that operation will complete.</span></span> <span data-ttu-id="f96df-203">If this value is false, it is an indication that the time limit is about to expire and that the procedure must wrap up execution.</span><span class="sxs-lookup"><span data-stu-id="f96df-203">If this value is false, it is an indication that the time limit is about to expire and that the procedure must wrap up execution.</span></span>  <span data-ttu-id="f96df-204">Operations queued prior to the first unaccepted store operation are guaranteed to complete if the stored procedure completes in time and does not queue any more requests.</span><span class="sxs-lookup"><span data-stu-id="f96df-204">Operations queued prior to the first unaccepted store operation are guaranteed to complete if the stored procedure completes in time and does not queue any more requests.</span></span>  

<span data-ttu-id="f96df-205">JavaScript functions are also bounded on resource consumption.</span><span class="sxs-lookup"><span data-stu-id="f96df-205">JavaScript functions are also bounded on resource consumption.</span></span> <span data-ttu-id="f96df-206">Cosmos DB reserves throughput per collection or for a set of containers.</span><span class="sxs-lookup"><span data-stu-id="f96df-206">Cosmos DB reserves throughput per collection or for a set of containers.</span></span> <span data-ttu-id="f96df-207">Throughput is expressed in terms of a normalized unit of CPU, memory and IO consumption called request units or RUs.</span><span class="sxs-lookup"><span data-stu-id="f96df-207">Throughput is expressed in terms of a normalized unit of CPU, memory and IO consumption called request units or RUs.</span></span> <span data-ttu-id="f96df-208">JavaScript functions can potentially use up a large number of RUs within a short time, and might get rate-limited if the collection’s limit is reached.</span><span class="sxs-lookup"><span data-stu-id="f96df-208">JavaScript functions can potentially use up a large number of RUs within a short time, and might get rate-limited if the collection’s limit is reached.</span></span> <span data-ttu-id="f96df-209">Resource-intensive stored procedures might also be quarantined to ensure availability of primitive database operations.</span><span class="sxs-lookup"><span data-stu-id="f96df-209">Resource-intensive stored procedures might also be quarantined to ensure availability of primitive database operations.</span></span>  

### <a name="example-bulk-importing-data-into-a-database-program"></a><span data-ttu-id="f96df-210">Example: Bulk importing data into a database program</span><span class="sxs-lookup"><span data-stu-id="f96df-210">Example: Bulk importing data into a database program</span></span>
<span data-ttu-id="f96df-211">Below is an example of a stored procedure that is written to bulk-import documents into a collection.</span><span class="sxs-lookup"><span data-stu-id="f96df-211">Below is an example of a stored procedure that is written to bulk-import documents into a collection.</span></span> <span data-ttu-id="f96df-212">Note how the stored procedure handles bounded execution by checking the Boolean return value from createDocument, and then uses the count of documents inserted in each invocation of the stored procedure to track and resume progress across batches.</span><span class="sxs-lookup"><span data-stu-id="f96df-212">Note how the stored procedure handles bounded execution by checking the Boolean return value from createDocument, and then uses the count of documents inserted in each invocation of the stored procedure to track and resume progress across batches.</span></span>

```javascript
function bulkImport(docs) {
    var collection = getContext().getCollection();
    var collectionLink = collection.getSelfLink();

    // The count of imported docs, also used as current doc index.
    var count = 0;

    // Validate input.
    if (!docs) throw new Error("The array is undefined or null.");

    var docsLength = docs.length;
    if (docsLength == 0) {
        getContext().getResponse().setBody(0);
    }

    // Call the create API to create a document.
    tryCreate(docs[count], callback);

    // Note that there are 2 exit conditions:
    // 1) The createDocument request was not accepted. 
    //    In this case the callback will not be called, we just call setBody and we are done.
    // 2) The callback was called docs.length times.
    //    In this case all documents were created and we don’t need to call tryCreate anymore. Just call setBody and we are done.
    function tryCreate(doc, callback) {
        var isAccepted = collection.createDocument(collectionLink, doc, callback);

        // If the request was accepted, callback will be called.
        // Otherwise report current count back to the client, 
        // which will call the script again with remaining set of docs.
        if (!isAccepted) getContext().getResponse().setBody(count);
    }

    // This is called when collection.createDocument is done in order to process the result.
    function callback(err, doc, options) {
        if (err) throw err;

        // One more document has been inserted, increment the count.
        count++;

        if (count >= docsLength) {
            // If we created all documents, we are done. Just set the response.
            getContext().getResponse().setBody(count);
        } else {
            // Create next document.
            tryCreate(docs[count], callback);
        }
    }
}
```

## <a id="trigger"></a> <span data-ttu-id="f96df-213">Database triggers</span><span class="sxs-lookup"><span data-stu-id="f96df-213">Database triggers</span></span>
### <a name="database-pre-triggers"></a><span data-ttu-id="f96df-214">Database pre-triggers</span><span class="sxs-lookup"><span data-stu-id="f96df-214">Database pre-triggers</span></span>
<span data-ttu-id="f96df-215">Cosmos DB provides triggers that are executed or triggered by an operation on a document.</span><span class="sxs-lookup"><span data-stu-id="f96df-215">Cosmos DB provides triggers that are executed or triggered by an operation on a document.</span></span> <span data-ttu-id="f96df-216">For example, you can specify a pre-trigger when you are creating a document – this pre-trigger will run before the document is created.</span><span class="sxs-lookup"><span data-stu-id="f96df-216">For example, you can specify a pre-trigger when you are creating a document – this pre-trigger will run before the document is created.</span></span> <span data-ttu-id="f96df-217">The following example shows how pre-triggers can be used to validate the properties of a document that is being created:</span><span class="sxs-lookup"><span data-stu-id="f96df-217">The following example shows how pre-triggers can be used to validate the properties of a document that is being created:</span></span>

```javascript
var validateDocumentContentsTrigger = {
    id: "validateDocumentContents",
    serverScript: function validate() {
        var context = getContext();
        var request = context.getRequest();

        // document to be created in the current operation
        var documentToCreate = request.getBody();

        // validate properties
        if (!("timestamp" in documentToCreate)) {
            var ts = new Date();
            documentToCreate["my timestamp"] = ts.getTime();
        }

        // update the document that will be created
        request.setBody(documentToCreate);
    },
    triggerType: TriggerType.Pre,
    triggerOperation: TriggerOperation.Create
}
```

<span data-ttu-id="f96df-218">And the corresponding Node.js client-side registration code for the trigger:</span><span class="sxs-lookup"><span data-stu-id="f96df-218">And the corresponding Node.js client-side registration code for the trigger:</span></span>

```javascript
// register pre-trigger
client.createTriggerAsync(collection.self, validateDocumentContentsTrigger)
    .then(function (response) {
        console.log("Created", response.resource);
        var docToCreate = {
            id: "DocWithTrigger",
            event: "Error",
            source: "Network outage"
        };

        // run trigger while creating above document 
        var options = { preTriggerInclude: "validateDocumentContents" };

        return client.createDocumentAsync(collection.self,
              docToCreate, options);
    }, function (error) {
        console.log("Error", error);
    })
.then(function (response) {
    console.log(response.resource); // document with timestamp property added
}, function (error) {
    console.log("Error", error);
});
```

<span data-ttu-id="f96df-219">Pre-triggers cannot have any input parameters.</span><span class="sxs-lookup"><span data-stu-id="f96df-219">Pre-triggers cannot have any input parameters.</span></span> <span data-ttu-id="f96df-220">The request object can be used to manipulate the request message associated with the operation.</span><span class="sxs-lookup"><span data-stu-id="f96df-220">The request object can be used to manipulate the request message associated with the operation.</span></span> <span data-ttu-id="f96df-221">Here, the pre-trigger is being run with the creation of a document, and the request message body contains the document to be created in JSON format.</span><span class="sxs-lookup"><span data-stu-id="f96df-221">Here, the pre-trigger is being run with the creation of a document, and the request message body contains the document to be created in JSON format.</span></span>   

<span data-ttu-id="f96df-222">When triggers are registered, users can specify the operations that it can run with.</span><span class="sxs-lookup"><span data-stu-id="f96df-222">When triggers are registered, users can specify the operations that it can run with.</span></span> <span data-ttu-id="f96df-223">This trigger was created with TriggerOperation.Create, which means using the trigger in a replace operation as shown in the following code is not permitted.</span><span class="sxs-lookup"><span data-stu-id="f96df-223">This trigger was created with TriggerOperation.Create, which means using the trigger in a replace operation as shown in the following code is not permitted.</span></span>

```javascript
var options = { preTriggerInclude: "validateDocumentContents" };

client.replaceDocumentAsync(docToReplace.self,
              newDocBody, options)
.then(function (response) {
    console.log(response.resource);
}, function (error) {
    console.log("Error", error);
});

// Fails, can’t use a create trigger in a replace operation
```
### <a name="database-post-triggers"></a><span data-ttu-id="f96df-224">Database post-triggers</span><span class="sxs-lookup"><span data-stu-id="f96df-224">Database post-triggers</span></span>
<span data-ttu-id="f96df-225">Post-triggers, like pre-triggers, are associated with an operation on a document and don’t take any input parameters.</span><span class="sxs-lookup"><span data-stu-id="f96df-225">Post-triggers, like pre-triggers, are associated with an operation on a document and don’t take any input parameters.</span></span> <span data-ttu-id="f96df-226">They run **after** the operation has completed, and have access to the response message that is sent to the client.</span><span class="sxs-lookup"><span data-stu-id="f96df-226">They run **after** the operation has completed, and have access to the response message that is sent to the client.</span></span>   

<span data-ttu-id="f96df-227">The following example shows post-triggers in action:</span><span class="sxs-lookup"><span data-stu-id="f96df-227">The following example shows post-triggers in action:</span></span>
```javascript
var updateMetadataTrigger = {
    id: "updateMetadata",
    serverScript: function updateMetadata() {
        var context = getContext();
        var collection = context.getCollection();
        var response = context.getResponse();

        // document that was created
        var createdDocument = response.getBody();

        // query for metadata document
        var filterQuery = 'SELECT * FROM root r WHERE r.id = "_metadata"';
        var accept = collection.queryDocuments(collection.getSelfLink(), filterQuery,
            updateMetadataCallback);
        if(!accept) throw "Unable to update metadata, abort";

        function updateMetadataCallback(err, documents, responseOptions) {
            if(err) throw new Error("Error" + err.message);
                     if(documents.length != 1) throw 'Unable to find metadata document';

                     var metadataDocument = documents[0];

                     // update metadata
                     metadataDocument.createdDocuments += 1;
                     metadataDocument.createdNames += " " + createdDocument.id;
                     var accept = collection.replaceDocument(metadataDocument._self,
                           metadataDocument, function(err, docReplaced) {
                                  if(err) throw "Unable to update metadata, abort";
                           });
                     if(!accept) throw "Unable to update metadata, abort";
                     return;                    
        }                                                                                            
    },
    triggerType: TriggerType.Post,
    triggerOperation: TriggerOperation.All
}

```
<span data-ttu-id="f96df-228">The trigger can be registered as shown in the following sample.</span><span class="sxs-lookup"><span data-stu-id="f96df-228">The trigger can be registered as shown in the following sample.</span></span>
```javascript
// register post-trigger
client.createTriggerAsync('dbs/testdb/colls/testColl', updateMetadataTrigger)
    .then(function(createdTrigger) { 
        var docToCreate = { 
            name: "artist_profile_1023",
            artist: "The Band",
            albums: ["Hellujah", "Rotators", "Spinning Top"]
        };

        // run trigger while creating above document 
        var options = { postTriggerInclude: "updateMetadata" };

        return client.createDocumentAsync(collection.self,
              docToCreate, options);
    }, function(error) {
        console.log("Error" , error);
    })
.then(function(response) {
    console.log(response.resource); 
}, function(error) {
    console.log("Error" , error);
});
```

<span data-ttu-id="f96df-229">This trigger queries for the metadata document and updates it with details about the newly created document.</span><span class="sxs-lookup"><span data-stu-id="f96df-229">This trigger queries for the metadata document and updates it with details about the newly created document.</span></span>  

<span data-ttu-id="f96df-230">One thing that is important to note is the **transactional** execution of triggers in Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f96df-230">One thing that is important to note is the **transactional** execution of triggers in Cosmos DB.</span></span> <span data-ttu-id="f96df-231">This post-trigger runs as part of the same transaction as the creation of the original document.</span><span class="sxs-lookup"><span data-stu-id="f96df-231">This post-trigger runs as part of the same transaction as the creation of the original document.</span></span> <span data-ttu-id="f96df-232">Therefore, if you throw an exception from the post-trigger (say if you are unable to update the metadata document), the whole transaction will fail and be rolled back.</span><span class="sxs-lookup"><span data-stu-id="f96df-232">Therefore, if you throw an exception from the post-trigger (say if you are unable to update the metadata document), the whole transaction will fail and be rolled back.</span></span> <span data-ttu-id="f96df-233">No document will be created, and an exception will be returned.</span><span class="sxs-lookup"><span data-stu-id="f96df-233">No document will be created, and an exception will be returned.</span></span>  

## <a id="udf"></a><span data-ttu-id="f96df-234">User-defined functions</span><span class="sxs-lookup"><span data-stu-id="f96df-234">User-defined functions</span></span>
<span data-ttu-id="f96df-235">User-defined functions (UDFs) are used to extend the Azure Cosmos DB SQL query language grammar and implement custom business logic.</span><span class="sxs-lookup"><span data-stu-id="f96df-235">User-defined functions (UDFs) are used to extend the Azure Cosmos DB SQL query language grammar and implement custom business logic.</span></span> <span data-ttu-id="f96df-236">They can only be called from inside queries.</span><span class="sxs-lookup"><span data-stu-id="f96df-236">They can only be called from inside queries.</span></span> <span data-ttu-id="f96df-237">They do not have access to the context object and are meant to be used as compute-only JavaScript.</span><span class="sxs-lookup"><span data-stu-id="f96df-237">They do not have access to the context object and are meant to be used as compute-only JavaScript.</span></span> <span data-ttu-id="f96df-238">Therefore, UDFs can be run on secondary replicas of the Cosmos DB service.</span><span class="sxs-lookup"><span data-stu-id="f96df-238">Therefore, UDFs can be run on secondary replicas of the Cosmos DB service.</span></span>  

<span data-ttu-id="f96df-239">The following sample creates a UDF to calculate income tax based on rates for various income brackets, and then uses it inside a query to find all people who paid more than $20,000 in taxes.</span><span class="sxs-lookup"><span data-stu-id="f96df-239">The following sample creates a UDF to calculate income tax based on rates for various income brackets, and then uses it inside a query to find all people who paid more than $20,000 in taxes.</span></span>

```javascript
var taxUdf = {
    id: "tax",
    serverScript: function tax(income) {

        if(income == undefined) 
            throw 'no input';

        if (income < 1000) 
            return income * 0.1;
        else if (income < 10000) 
            return income * 0.2;
        else
            return income * 0.4;
    }
}
```

<span data-ttu-id="f96df-240">The UDF can subsequently be used in queries like in the following sample:</span><span class="sxs-lookup"><span data-stu-id="f96df-240">The UDF can subsequently be used in queries like in the following sample:</span></span>

```javascript
// register UDF
client.createUserDefinedFunctionAsync('dbs/testdb/colls/testColl', taxUdf)
    .then(function(response) { 
        console.log("Created", response.resource);

        var query = 'SELECT * FROM TaxPayers t WHERE udf.tax(t.income) > 20000'; 
        return client.queryDocuments('dbs/testdb/colls/testColl',
               query).toArrayAsync();
    }, function(error) {
        console.log("Error" , error);
    })
.then(function(response) {
    var documents = response.feed;
    console.log(response.resource); 
}, function(error) {
    console.log("Error" , error);
});
```

## <a name="javascript-language-integrated-query-api"></a><span data-ttu-id="f96df-241">JavaScript language-integrated query API</span><span class="sxs-lookup"><span data-stu-id="f96df-241">JavaScript language-integrated query API</span></span>
<span data-ttu-id="f96df-242">In addition to issuing queries using Azure Cosmos DB's SQL grammar, the server-side SDK allows you to perform optimized queries using a fluent JavaScript interface without any knowledge of SQL.</span><span class="sxs-lookup"><span data-stu-id="f96df-242">In addition to issuing queries using Azure Cosmos DB's SQL grammar, the server-side SDK allows you to perform optimized queries using a fluent JavaScript interface without any knowledge of SQL.</span></span> <span data-ttu-id="f96df-243">The JavaScript query API allows you to programmatically build queries by passing predicate functions into chainable function calls, with a syntax familiar to ECMAScript5's Array built-ins and popular JavaScript libraries like Lodash.</span><span class="sxs-lookup"><span data-stu-id="f96df-243">The JavaScript query API allows you to programmatically build queries by passing predicate functions into chainable function calls, with a syntax familiar to ECMAScript5's Array built-ins and popular JavaScript libraries like Lodash.</span></span> <span data-ttu-id="f96df-244">Queries are parsed by the JavaScript runtime to be executed efficiently using Azure Cosmos DB’s indices.</span><span class="sxs-lookup"><span data-stu-id="f96df-244">Queries are parsed by the JavaScript runtime to be executed efficiently using Azure Cosmos DB’s indices.</span></span>

> [!NOTE]
> <span data-ttu-id="f96df-245">`__` (double-underscore) is an alias to `getContext().getCollection()`.</span><span class="sxs-lookup"><span data-stu-id="f96df-245">`__` (double-underscore) is an alias to `getContext().getCollection()`.</span></span>
> <br/>
> <span data-ttu-id="f96df-246">In other words, you can use `__` or `getContext().getCollection()` to access the JavaScript query API.</span><span class="sxs-lookup"><span data-stu-id="f96df-246">In other words, you can use `__` or `getContext().getCollection()` to access the JavaScript query API.</span></span>
> 
> 

<span data-ttu-id="f96df-247">Supported functions include:</span><span class="sxs-lookup"><span data-stu-id="f96df-247">Supported functions include:</span></span>

<ul>
<li><span data-ttu-id="f96df-248">
<b>chain() ... .value([callback] [, options])</b>
</span><span class="sxs-lookup"><span data-stu-id="f96df-248">
<b>chain() ... .value([callback] [, options])</b>
</span></span><ul>
<li>
<span data-ttu-id="f96df-249">Starts a chained call that must be terminated with value().</span><span class="sxs-lookup"><span data-stu-id="f96df-249">Starts a chained call that must be terminated with value().</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="f96df-250">
<b>filter(predicateFunction [, options] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="f96df-250">
<b>filter(predicateFunction [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="f96df-251">Filters the input using a predicate function that returns true/false in order to filter in/out input documents into the resulting set.</span><span class="sxs-lookup"><span data-stu-id="f96df-251">Filters the input using a predicate function that returns true/false in order to filter in/out input documents into the resulting set.</span></span> <span data-ttu-id="f96df-252">This function behaves similar to a WHERE clause in SQL.</span><span class="sxs-lookup"><span data-stu-id="f96df-252">This function behaves similar to a WHERE clause in SQL.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="f96df-253">
<b>map(transformationFunction [, options] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="f96df-253">
<b>map(transformationFunction [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="f96df-254">Applies a projection given a transformation function that maps each input item to a JavaScript object or value.</span><span class="sxs-lookup"><span data-stu-id="f96df-254">Applies a projection given a transformation function that maps each input item to a JavaScript object or value.</span></span> <span data-ttu-id="f96df-255">This function behaves similar to a SELECT clause in SQL.</span><span class="sxs-lookup"><span data-stu-id="f96df-255">This function behaves similar to a SELECT clause in SQL.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="f96df-256">
<b>pluck([propertyName] [, options] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="f96df-256">
<b>pluck([propertyName] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="f96df-257">This function is a shortcut for a map that extracts the value of a single property from each input item.</span><span class="sxs-lookup"><span data-stu-id="f96df-257">This function is a shortcut for a map that extracts the value of a single property from each input item.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="f96df-258">
<b>flatten([isShallow] [, options] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="f96df-258">
<b>flatten([isShallow] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="f96df-259">Combines and flattens arrays from each input item in to a single array.</span><span class="sxs-lookup"><span data-stu-id="f96df-259">Combines and flattens arrays from each input item in to a single array.</span></span> <span data-ttu-id="f96df-260">This function behaves similar to SelectMany in LINQ.</span><span class="sxs-lookup"><span data-stu-id="f96df-260">This function behaves similar to SelectMany in LINQ.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="f96df-261">
<b>sortBy([predicate] [, options] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="f96df-261">
<b>sortBy([predicate] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="f96df-262">Produce a new set of documents by sorting the documents in the input document stream in ascending order using the given predicate.</span><span class="sxs-lookup"><span data-stu-id="f96df-262">Produce a new set of documents by sorting the documents in the input document stream in ascending order using the given predicate.</span></span> <span data-ttu-id="f96df-263">This function behaves similar to an ORDER BY clause in SQL.</span><span class="sxs-lookup"><span data-stu-id="f96df-263">This function behaves similar to an ORDER BY clause in SQL.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="f96df-264">
<b>sortByDescending([predicate] [, options] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="f96df-264">
<b>sortByDescending([predicate] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="f96df-265">Produce a new set of documents by sorting the documents in the input document stream in descending order using the given predicate.</span><span class="sxs-lookup"><span data-stu-id="f96df-265">Produce a new set of documents by sorting the documents in the input document stream in descending order using the given predicate.</span></span> <span data-ttu-id="f96df-266">This function behaves similar to an ORDER BY x DESC clause in SQL.</span><span class="sxs-lookup"><span data-stu-id="f96df-266">This function behaves similar to an ORDER BY x DESC clause in SQL.</span></span>
</li>
</ul>
</li>
</ul>


<span data-ttu-id="f96df-267">When included inside predicate and/or selector functions, the following JavaScript constructs get automatically optimized to run directly on Azure Cosmos DB indices:</span><span class="sxs-lookup"><span data-stu-id="f96df-267">When included inside predicate and/or selector functions, the following JavaScript constructs get automatically optimized to run directly on Azure Cosmos DB indices:</span></span>

* <span data-ttu-id="f96df-268">Simple operators: = + - \* / % | ^ &amp; == != === !=== &lt; &gt; &lt;= &gt;= || &amp;&amp; &lt;&lt; &gt;&gt; &gt;&gt;&gt;!</span><span class="sxs-lookup"><span data-stu-id="f96df-268">Simple operators: = + - \* / % | ^ &amp; == != === !=== &lt; &gt; &lt;= &gt;= || &amp;&amp; &lt;&lt; &gt;&gt; &gt;&gt;&gt;!</span></span> ~
* <span data-ttu-id="f96df-269">Literals, including the object literal: {}</span><span class="sxs-lookup"><span data-stu-id="f96df-269">Literals, including the object literal: {}</span></span>
* <span data-ttu-id="f96df-270">var, return</span><span class="sxs-lookup"><span data-stu-id="f96df-270">var, return</span></span>

<span data-ttu-id="f96df-271">The following JavaScript constructs do not get optimized for Azure Cosmos DB indices:</span><span class="sxs-lookup"><span data-stu-id="f96df-271">The following JavaScript constructs do not get optimized for Azure Cosmos DB indices:</span></span>

* <span data-ttu-id="f96df-272">Control flow (for example, if, for, while)</span><span class="sxs-lookup"><span data-stu-id="f96df-272">Control flow (for example, if, for, while)</span></span>
* <span data-ttu-id="f96df-273">Function calls</span><span class="sxs-lookup"><span data-stu-id="f96df-273">Function calls</span></span>

<span data-ttu-id="f96df-274">For more information, see the [Server-Side JSDocs](https://azure.github.io/azure-cosmosdb-js-server/).</span><span class="sxs-lookup"><span data-stu-id="f96df-274">For more information, see the [Server-Side JSDocs](https://azure.github.io/azure-cosmosdb-js-server/).</span></span>

### <a name="example-write-a-stored-procedure-using-the-javascript-query-api"></a><span data-ttu-id="f96df-275">Example: Write a stored procedure using the JavaScript query API</span><span class="sxs-lookup"><span data-stu-id="f96df-275">Example: Write a stored procedure using the JavaScript query API</span></span>
<span data-ttu-id="f96df-276">The following code sample is an example of how the JavaScript Query API can be used in the context of a stored procedure.</span><span class="sxs-lookup"><span data-stu-id="f96df-276">The following code sample is an example of how the JavaScript Query API can be used in the context of a stored procedure.</span></span> <span data-ttu-id="f96df-277">The stored procedure inserts a document, given by an input parameter, and updates a metadata document, using the `__.filter()` method, with minSize, maxSize, and totalSize based upon the input document's size property.</span><span class="sxs-lookup"><span data-stu-id="f96df-277">The stored procedure inserts a document, given by an input parameter, and updates a metadata document, using the `__.filter()` method, with minSize, maxSize, and totalSize based upon the input document's size property.</span></span>

```javascript
/**
 * Insert actual doc and update metadata doc: minSize, maxSize, totalSize based on doc.size.
 */
function insertDocumentAndUpdateMetadata(doc) {
  // HTTP error codes sent to our callback funciton by DocDB server.
  var ErrorCode = {
    RETRY_WITH: 449,
  }

  var isAccepted = __.createDocument(__.getSelfLink(), doc, {}, function(err, doc, options) {
    if (err) throw err;

    // Check the doc (ignore docs with invalid/zero size and metaDoc itself) and call updateMetadata.
    if (!doc.isMetadata && doc.size > 0) {
      // Get the meta document. We keep it in the same collection. it's the only doc that has .isMetadata = true.
      var result = __.filter(function(x) {
        return x.isMetadata === true
      }, function(err, feed, options) {
        if (err) throw err;

        // We assume that metadata doc was pre-created and must exist when this script is called.
        if (!feed || !feed.length) throw new Error("Failed to find the metadata document.");

        // The metadata document.
        var metaDoc = feed[0];

        // Update metaDoc.minSize:
        // for 1st document use doc.Size, for all the rest see if it's less than last min.
        if (metaDoc.minSize == 0) metaDoc.minSize = doc.size;
        else metaDoc.minSize = Math.min(metaDoc.minSize, doc.size);

        // Update metaDoc.maxSize.
        metaDoc.maxSize = Math.max(metaDoc.maxSize, doc.size);

        // Update metaDoc.totalSize.
        metaDoc.totalSize += doc.size;

        // Update/replace the metadata document in the store.
        var isAccepted = __.replaceDocument(metaDoc._self, metaDoc, function(err) {
          if (err) throw err;
          // Note: in case concurrent updates causes conflict with ErrorCode.RETRY_WITH, we can't read the meta again 
          //       and update again because due to Snapshot isolation we will read same exact version (we are in same transaction).
          //       We have to take care of that on the client side.
        });
        if (!isAccepted) throw new Error("replaceDocument(metaDoc) returned false.");
      });
      if (!result.isAccepted) throw new Error("filter for metaDoc returned false.");
    }
  });
  if (!isAccepted) throw new Error("createDocument(actual doc) returned false.");
}
```

## <a name="sql-to-javascript-cheat-sheet"></a><span data-ttu-id="f96df-278">SQL to Javascript cheat sheet</span><span class="sxs-lookup"><span data-stu-id="f96df-278">SQL to Javascript cheat sheet</span></span>
<span data-ttu-id="f96df-279">The following table presents various SQL queries and the corresponding JavaScript queries.</span><span class="sxs-lookup"><span data-stu-id="f96df-279">The following table presents various SQL queries and the corresponding JavaScript queries.</span></span>

<span data-ttu-id="f96df-280">As with SQL queries, document property keys (for example, `doc.id`) are case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="f96df-280">As with SQL queries, document property keys (for example, `doc.id`) are case-sensitive.</span></span>

|<span data-ttu-id="f96df-281">SQL</span><span class="sxs-lookup"><span data-stu-id="f96df-281">SQL</span></span>| <span data-ttu-id="f96df-282">JavaScript Query API</span><span class="sxs-lookup"><span data-stu-id="f96df-282">JavaScript Query API</span></span>|<span data-ttu-id="f96df-283">Description below</span><span class="sxs-lookup"><span data-stu-id="f96df-283">Description below</span></span>|
|---|---|---|
|<span data-ttu-id="f96df-284">SELECT \*</span><span class="sxs-lookup"><span data-stu-id="f96df-284">SELECT \*</span></span><br><span data-ttu-id="f96df-285">FROM docs</span><span class="sxs-lookup"><span data-stu-id="f96df-285">FROM docs</span></span>| <span data-ttu-id="f96df-286">__.map(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="f96df-286">__.map(function(doc) {</span></span> <br><span data-ttu-id="f96df-287">&nbsp;&nbsp;&nbsp;&nbsp;return doc;</span><span class="sxs-lookup"><span data-stu-id="f96df-287">&nbsp;&nbsp;&nbsp;&nbsp;return doc;</span></span><br><span data-ttu-id="f96df-288">});</span><span class="sxs-lookup"><span data-stu-id="f96df-288">});</span></span>|<span data-ttu-id="f96df-289">1</span><span class="sxs-lookup"><span data-stu-id="f96df-289">1</span></span>|
|<span data-ttu-id="f96df-290">SELECT docs.id, docs.message AS msg, docs.actions</span><span class="sxs-lookup"><span data-stu-id="f96df-290">SELECT docs.id, docs.message AS msg, docs.actions</span></span> <br><span data-ttu-id="f96df-291">FROM docs</span><span class="sxs-lookup"><span data-stu-id="f96df-291">FROM docs</span></span>|<span data-ttu-id="f96df-292">__.map(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="f96df-292">__.map(function(doc) {</span></span><br><span data-ttu-id="f96df-293">&nbsp;&nbsp;&nbsp;&nbsp;return {</span><span class="sxs-lookup"><span data-stu-id="f96df-293">&nbsp;&nbsp;&nbsp;&nbsp;return {</span></span><br><span data-ttu-id="f96df-294">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id: doc.id,</span><span class="sxs-lookup"><span data-stu-id="f96df-294">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id: doc.id,</span></span><br><span data-ttu-id="f96df-295">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;msg: doc.message,</span><span class="sxs-lookup"><span data-stu-id="f96df-295">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;msg: doc.message,</span></span><br><span data-ttu-id="f96df-296">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;actions:doc.actions</span><span class="sxs-lookup"><span data-stu-id="f96df-296">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;actions:doc.actions</span></span><br><span data-ttu-id="f96df-297">&nbsp;&nbsp;&nbsp;&nbsp;};</span><span class="sxs-lookup"><span data-stu-id="f96df-297">&nbsp;&nbsp;&nbsp;&nbsp;};</span></span><br><span data-ttu-id="f96df-298">});</span><span class="sxs-lookup"><span data-stu-id="f96df-298">});</span></span>|<span data-ttu-id="f96df-299">2</span><span class="sxs-lookup"><span data-stu-id="f96df-299">2</span></span>|
|<span data-ttu-id="f96df-300">SELECT \*</span><span class="sxs-lookup"><span data-stu-id="f96df-300">SELECT \*</span></span><br><span data-ttu-id="f96df-301">FROM docs</span><span class="sxs-lookup"><span data-stu-id="f96df-301">FROM docs</span></span><br><span data-ttu-id="f96df-302">WHERE docs.id="X998_Y998"</span><span class="sxs-lookup"><span data-stu-id="f96df-302">WHERE docs.id="X998_Y998"</span></span>|<span data-ttu-id="f96df-303">__.filter(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="f96df-303">__.filter(function(doc) {</span></span><br><span data-ttu-id="f96df-304">&nbsp;&nbsp;&nbsp;&nbsp;return doc.id ==="X998_Y998";</span><span class="sxs-lookup"><span data-stu-id="f96df-304">&nbsp;&nbsp;&nbsp;&nbsp;return doc.id ==="X998_Y998";</span></span><br><span data-ttu-id="f96df-305">});</span><span class="sxs-lookup"><span data-stu-id="f96df-305">});</span></span>|<span data-ttu-id="f96df-306">3</span><span class="sxs-lookup"><span data-stu-id="f96df-306">3</span></span>|
|<span data-ttu-id="f96df-307">SELECT \*</span><span class="sxs-lookup"><span data-stu-id="f96df-307">SELECT \*</span></span><br><span data-ttu-id="f96df-308">FROM docs</span><span class="sxs-lookup"><span data-stu-id="f96df-308">FROM docs</span></span><br><span data-ttu-id="f96df-309">WHERE ARRAY_CONTAINS(docs.Tags, 123)</span><span class="sxs-lookup"><span data-stu-id="f96df-309">WHERE ARRAY_CONTAINS(docs.Tags, 123)</span></span>|<span data-ttu-id="f96df-310">__.filter(function(x) {</span><span class="sxs-lookup"><span data-stu-id="f96df-310">__.filter(function(x) {</span></span><br><span data-ttu-id="f96df-311">&nbsp;&nbsp;&nbsp;&nbsp;return x.Tags && x.Tags.indexOf(123) > -1;</span><span class="sxs-lookup"><span data-stu-id="f96df-311">&nbsp;&nbsp;&nbsp;&nbsp;return x.Tags && x.Tags.indexOf(123) > -1;</span></span><br><span data-ttu-id="f96df-312">});</span><span class="sxs-lookup"><span data-stu-id="f96df-312">});</span></span>|<span data-ttu-id="f96df-313">4</span><span class="sxs-lookup"><span data-stu-id="f96df-313">4</span></span>|
|<span data-ttu-id="f96df-314">SELECT docs.id, docs.message AS msg</span><span class="sxs-lookup"><span data-stu-id="f96df-314">SELECT docs.id, docs.message AS msg</span></span><br><span data-ttu-id="f96df-315">FROM docs</span><span class="sxs-lookup"><span data-stu-id="f96df-315">FROM docs</span></span><br><span data-ttu-id="f96df-316">WHERE docs.id="X998_Y998"</span><span class="sxs-lookup"><span data-stu-id="f96df-316">WHERE docs.id="X998_Y998"</span></span>|<span data-ttu-id="f96df-317">__.chain()</span><span class="sxs-lookup"><span data-stu-id="f96df-317">__.chain()</span></span><br><span data-ttu-id="f96df-318">&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="f96df-318">&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {</span></span><br><span data-ttu-id="f96df-319">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc.id ==="X998_Y998";</span><span class="sxs-lookup"><span data-stu-id="f96df-319">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc.id ==="X998_Y998";</span></span><br><span data-ttu-id="f96df-320">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="f96df-320">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="f96df-321">&nbsp;&nbsp;&nbsp;&nbsp;.map(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="f96df-321">&nbsp;&nbsp;&nbsp;&nbsp;.map(function(doc) {</span></span><br><span data-ttu-id="f96df-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return {</span><span class="sxs-lookup"><span data-stu-id="f96df-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return {</span></span><br><span data-ttu-id="f96df-323">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id: doc.id,</span><span class="sxs-lookup"><span data-stu-id="f96df-323">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id: doc.id,</span></span><br><span data-ttu-id="f96df-324">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;msg: doc.message</span><span class="sxs-lookup"><span data-stu-id="f96df-324">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;msg: doc.message</span></span><br><span data-ttu-id="f96df-325">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;};</span><span class="sxs-lookup"><span data-stu-id="f96df-325">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;};</span></span><br><span data-ttu-id="f96df-326">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="f96df-326">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="f96df-327">.value();</span><span class="sxs-lookup"><span data-stu-id="f96df-327">.value();</span></span>|<span data-ttu-id="f96df-328">5</span><span class="sxs-lookup"><span data-stu-id="f96df-328">5</span></span>|
|<span data-ttu-id="f96df-329">SELECT VALUE tag</span><span class="sxs-lookup"><span data-stu-id="f96df-329">SELECT VALUE tag</span></span><br><span data-ttu-id="f96df-330">FROM docs</span><span class="sxs-lookup"><span data-stu-id="f96df-330">FROM docs</span></span><br><span data-ttu-id="f96df-331">JOIN tag IN docs.Tags</span><span class="sxs-lookup"><span data-stu-id="f96df-331">JOIN tag IN docs.Tags</span></span><br><span data-ttu-id="f96df-332">ORDER BY docs._ts</span><span class="sxs-lookup"><span data-stu-id="f96df-332">ORDER BY docs._ts</span></span>|<span data-ttu-id="f96df-333">__.chain()</span><span class="sxs-lookup"><span data-stu-id="f96df-333">__.chain()</span></span><br><span data-ttu-id="f96df-334">&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="f96df-334">&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {</span></span><br><span data-ttu-id="f96df-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc.Tags && Array.isArray(doc.Tags);</span><span class="sxs-lookup"><span data-stu-id="f96df-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc.Tags && Array.isArray(doc.Tags);</span></span><br><span data-ttu-id="f96df-336">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="f96df-336">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="f96df-337">&nbsp;&nbsp;&nbsp;&nbsp;.sortBy(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="f96df-337">&nbsp;&nbsp;&nbsp;&nbsp;.sortBy(function(doc) {</span></span><br><span data-ttu-id="f96df-338">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc._ts;</span><span class="sxs-lookup"><span data-stu-id="f96df-338">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc._ts;</span></span><br><span data-ttu-id="f96df-339">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="f96df-339">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="f96df-340">&nbsp;&nbsp;&nbsp;&nbsp;.pluck("Tags")</span><span class="sxs-lookup"><span data-stu-id="f96df-340">&nbsp;&nbsp;&nbsp;&nbsp;.pluck("Tags")</span></span><br><span data-ttu-id="f96df-341">&nbsp;&nbsp;&nbsp;&nbsp;.flatten()</span><span class="sxs-lookup"><span data-stu-id="f96df-341">&nbsp;&nbsp;&nbsp;&nbsp;.flatten()</span></span><br><span data-ttu-id="f96df-342">&nbsp;&nbsp;&nbsp;&nbsp;.value()</span><span class="sxs-lookup"><span data-stu-id="f96df-342">&nbsp;&nbsp;&nbsp;&nbsp;.value()</span></span>|<span data-ttu-id="f96df-343">6</span><span class="sxs-lookup"><span data-stu-id="f96df-343">6</span></span>|

<span data-ttu-id="f96df-344">The following descriptions explain each query in the table above.</span><span class="sxs-lookup"><span data-stu-id="f96df-344">The following descriptions explain each query in the table above.</span></span>
1. <span data-ttu-id="f96df-345">Results in all documents (paginated with continuation token) as is.</span><span class="sxs-lookup"><span data-stu-id="f96df-345">Results in all documents (paginated with continuation token) as is.</span></span>
2. <span data-ttu-id="f96df-346">Projects the id, message (aliased to msg), and action from all documents.</span><span class="sxs-lookup"><span data-stu-id="f96df-346">Projects the id, message (aliased to msg), and action from all documents.</span></span>
3. <span data-ttu-id="f96df-347">Queries for documents with the predicate: id = "X998_Y998".</span><span class="sxs-lookup"><span data-stu-id="f96df-347">Queries for documents with the predicate: id = "X998_Y998".</span></span>
4. <span data-ttu-id="f96df-348">Queries for documents that have a Tags property and Tags is an array containing the value 123.</span><span class="sxs-lookup"><span data-stu-id="f96df-348">Queries for documents that have a Tags property and Tags is an array containing the value 123.</span></span>
5. <span data-ttu-id="f96df-349">Queries for documents with a predicate, id = "X998_Y998", and then projects the id and message (aliased to msg).</span><span class="sxs-lookup"><span data-stu-id="f96df-349">Queries for documents with a predicate, id = "X998_Y998", and then projects the id and message (aliased to msg).</span></span>
6. <span data-ttu-id="f96df-350">Filters for documents that have an array property, Tags, and sorts the resulting documents by the _ts timestamp system property, and then projects + flattens the Tags array.</span><span class="sxs-lookup"><span data-stu-id="f96df-350">Filters for documents that have an array property, Tags, and sorts the resulting documents by the _ts timestamp system property, and then projects + flattens the Tags array.</span></span>


## <a name="runtime-support"></a><span data-ttu-id="f96df-351">Runtime support</span><span class="sxs-lookup"><span data-stu-id="f96df-351">Runtime support</span></span>
<span data-ttu-id="f96df-352">The Azure Cosmos DB [JavaScript server side API](https://azure.github.io/azure-cosmosdb-js-server/) provides support for the most of the mainstream JavaScript language features as standardized by [ECMA-262](http://www.ecma-international.org/publications/standards/Ecma-262.htm).</span><span class="sxs-lookup"><span data-stu-id="f96df-352">The Azure Cosmos DB [JavaScript server side API](https://azure.github.io/azure-cosmosdb-js-server/) provides support for the most of the mainstream JavaScript language features as standardized by [ECMA-262](http://www.ecma-international.org/publications/standards/Ecma-262.htm).</span></span>

### <a name="security"></a><span data-ttu-id="f96df-353">Security</span><span class="sxs-lookup"><span data-stu-id="f96df-353">Security</span></span>
<span data-ttu-id="f96df-354">JavaScript stored procedures and triggers are sandboxed so that the effects of one script do not leak to the other without going through the snapshot transaction isolation at the database level.</span><span class="sxs-lookup"><span data-stu-id="f96df-354">JavaScript stored procedures and triggers are sandboxed so that the effects of one script do not leak to the other without going through the snapshot transaction isolation at the database level.</span></span> <span data-ttu-id="f96df-355">The runtime environments are pooled but cleaned of the context after each run.</span><span class="sxs-lookup"><span data-stu-id="f96df-355">The runtime environments are pooled but cleaned of the context after each run.</span></span> <span data-ttu-id="f96df-356">Hence they are guaranteed to be safe of any unintended side effects from each other.</span><span class="sxs-lookup"><span data-stu-id="f96df-356">Hence they are guaranteed to be safe of any unintended side effects from each other.</span></span>

### <a name="pre-compilation"></a><span data-ttu-id="f96df-357">Pre-compilation</span><span class="sxs-lookup"><span data-stu-id="f96df-357">Pre-compilation</span></span>
<span data-ttu-id="f96df-358">Stored procedures, triggers, and UDFs are implicitly precompiled to the byte code format in order to avoid compilation cost at the time of each script invocation.</span><span class="sxs-lookup"><span data-stu-id="f96df-358">Stored procedures, triggers, and UDFs are implicitly precompiled to the byte code format in order to avoid compilation cost at the time of each script invocation.</span></span> <span data-ttu-id="f96df-359">Pre-compilation ensures invocation of stored procedures is fast and have a low footprint.</span><span class="sxs-lookup"><span data-stu-id="f96df-359">Pre-compilation ensures invocation of stored procedures is fast and have a low footprint.</span></span>

## <a name="client-sdk-support"></a><span data-ttu-id="f96df-360">Client SDK support</span><span class="sxs-lookup"><span data-stu-id="f96df-360">Client SDK support</span></span>
<span data-ttu-id="f96df-361">In addition to the Azure Cosmos DB [Node.js](sql-api-sdk-node.md) API, Azure Cosmos DB has [.NET](sql-api-sdk-dotnet.md), [.NET Core](sql-api-sdk-dotnet-core.md), [Java](sql-api-sdk-java.md), [JavaScript](sql-api-sdk-node.md), and [Python SDKs](sql-api-sdk-python.md) for the SQL API as well.</span><span class="sxs-lookup"><span data-stu-id="f96df-361">In addition to the Azure Cosmos DB [Node.js](sql-api-sdk-node.md) API, Azure Cosmos DB has [.NET](sql-api-sdk-dotnet.md), [.NET Core](sql-api-sdk-dotnet-core.md), [Java](sql-api-sdk-java.md), [JavaScript](sql-api-sdk-node.md), and [Python SDKs](sql-api-sdk-python.md) for the SQL API as well.</span></span> <span data-ttu-id="f96df-362">Stored procedures, triggers, and UDFs can be created and executed using any of these SDKs as well.</span><span class="sxs-lookup"><span data-stu-id="f96df-362">Stored procedures, triggers, and UDFs can be created and executed using any of these SDKs as well.</span></span> <span data-ttu-id="f96df-363">The following example shows how to create and execute a stored procedure using the .NET client.</span><span class="sxs-lookup"><span data-stu-id="f96df-363">The following example shows how to create and execute a stored procedure using the .NET client.</span></span> <span data-ttu-id="f96df-364">Note how the .NET types are passed into the stored procedure as JSON and read back.</span><span class="sxs-lookup"><span data-stu-id="f96df-364">Note how the .NET types are passed into the stored procedure as JSON and read back.</span></span>

```javascript
var markAntiquesSproc = new StoredProcedure
{
    Id = "ValidateDocumentAge",
    Body = @"
            function(docToCreate, antiqueYear) {
                var collection = getContext().getCollection();    
                var response = getContext().getResponse();    

                if(docToCreate.Year != undefined && docToCreate.Year < antiqueYear){
                    docToCreate.antique = true;
                }

                collection.createDocument(collection.getSelfLink(), docToCreate, {}, 
                    function(err, docCreated, options) { 
                        if(err) throw new Error('Error while creating document: ' + err.message);                              
                        if(options.maxCollectionSizeInMb == 0) throw 'max collection size not found'; 
                        response.setBody(docCreated);
                });
         }"
};

// register stored procedure
StoredProcedure createdStoredProcedure = await client.CreateStoredProcedureAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"), markAntiquesSproc);
dynamic document = new Document() { Id = "Borges_112" };
document.Title = "Aleph";
document.Year = 1949;

// execute stored procedure
Document createdDocument = await client.ExecuteStoredProcedureAsync<Document>(UriFactory.CreateStoredProcedureUri("db", "coll", "ValidateDocumentAge"), document, 1920);
```

<span data-ttu-id="f96df-365">This sample shows how to use the [SQL .NET API](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) to create a pre-trigger and create a document with the trigger enabled.</span><span class="sxs-lookup"><span data-stu-id="f96df-365">This sample shows how to use the [SQL .NET API](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) to create a pre-trigger and create a document with the trigger enabled.</span></span> 

```javascript
Trigger preTrigger = new Trigger()
{
    Id = "CapitalizeName",
    Body = @"function() {
        var item = getContext().getRequest().getBody();
        item.id = item.id.toUpperCase();
        getContext().getRequest().setBody(item);
    }",
    TriggerOperation = TriggerOperation.Create,
    TriggerType = TriggerType.Pre
};

Document createdItem = await client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"), new Document { Id = "documentdb" },
    new RequestOptions
    {
        PreTriggerInclude = new List<string> { "CapitalizeName" },
    });
```

<span data-ttu-id="f96df-366">And the following example shows how to create a user-defined function (UDF) and use it in a [SQL query](sql-api-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="f96df-366">And the following example shows how to create a user-defined function (UDF) and use it in a [SQL query](sql-api-sql-query.md).</span></span>

```javascript
UserDefinedFunction function = new UserDefinedFunction()
{
    Id = "LOWER",
    Body = @"function(input) 
    {
        return input.toLowerCase();
    }"
};

foreach (Book book in client.CreateDocumentQuery(UriFactory.CreateDocumentCollectionUri("db", "coll"),
    "SELECT * FROM Books b WHERE udf.LOWER(b.Title) = 'war and peace'"))
{
    Console.WriteLine("Read {0} from query", book);
}
```

## <a name="rest-api"></a><span data-ttu-id="f96df-367">REST API</span><span class="sxs-lookup"><span data-stu-id="f96df-367">REST API</span></span>
<span data-ttu-id="f96df-368">All Azure Cosmos DB operations can be performed in a RESTful manner.</span><span class="sxs-lookup"><span data-stu-id="f96df-368">All Azure Cosmos DB operations can be performed in a RESTful manner.</span></span> <span data-ttu-id="f96df-369">Stored procedures, triggers, and user-defined functions can be registered under a collection by using HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="f96df-369">Stored procedures, triggers, and user-defined functions can be registered under a collection by using HTTP POST.</span></span> <span data-ttu-id="f96df-370">The following example shows how to register a stored procedure:</span><span class="sxs-lookup"><span data-stu-id="f96df-370">The following example shows how to register a stored procedure:</span></span>

    POST https://<url>/sprocs/ HTTP/1.1
    authorization: <<auth>>
    x-ms-date: Thu, 07 Aug 2014 03:43:10 GMT


    var x = {
      "name": "createAndAddProperty",
      "body": function (docToCreate, addedPropertyName, addedPropertyValue) {
                var collectionManager = getContext().getCollection();
                collectionManager.createDocument(
                    collectionManager.getSelfLink(),
                    docToCreate,
                    function(err, docCreated) {
                      if(err) throw new Error('Error:  ' + err.message);
                      docCreated[addedPropertyName] = addedPropertyValue;
                      getContext().getResponse().setBody(docCreated);
                    });
            }
    }


<span data-ttu-id="f96df-371">The stored procedure is registered by executing a POST request against the URI dbs/testdb/colls/testColl/sprocs with the body containing the stored procedure to create.</span><span class="sxs-lookup"><span data-stu-id="f96df-371">The stored procedure is registered by executing a POST request against the URI dbs/testdb/colls/testColl/sprocs with the body containing the stored procedure to create.</span></span> <span data-ttu-id="f96df-372">Triggers and UDFs can be registered similarly by issuing a POST against /triggers and /udfs respectively.</span><span class="sxs-lookup"><span data-stu-id="f96df-372">Triggers and UDFs can be registered similarly by issuing a POST against /triggers and /udfs respectively.</span></span>
<span data-ttu-id="f96df-373">This stored procedure can then be executed by issuing a POST request against its resource link:</span><span class="sxs-lookup"><span data-stu-id="f96df-373">This stored procedure can then be executed by issuing a POST request against its resource link:</span></span>

    POST https://<url>/sprocs/<sproc> HTTP/1.1
    authorization: <<auth>>
    x-ms-date: Thu, 07 Aug 2014 03:43:20 GMT


    [ { "name": "TestDocument", "book": "Autumn of the Patriarch"}, "Price", 200 ]


<span data-ttu-id="f96df-374">Here, the input to the stored procedure is passed in the request body.</span><span class="sxs-lookup"><span data-stu-id="f96df-374">Here, the input to the stored procedure is passed in the request body.</span></span> <span data-ttu-id="f96df-375">The input is passed as a JSON array of input parameters.</span><span class="sxs-lookup"><span data-stu-id="f96df-375">The input is passed as a JSON array of input parameters.</span></span> <span data-ttu-id="f96df-376">The stored procedure takes the first input as a document that is a response body.</span><span class="sxs-lookup"><span data-stu-id="f96df-376">The stored procedure takes the first input as a document that is a response body.</span></span> <span data-ttu-id="f96df-377">The response you receive is as follows:</span><span class="sxs-lookup"><span data-stu-id="f96df-377">The response you receive is as follows:</span></span>

    HTTP/1.1 200 OK

    { 
      name: 'TestDocument',
      book: 'Autumn of the Patriarch',
      id: 'V7tQANV3rAkDAAAAAAAAAA==',
      ts: 1407830727,
      self: 'dbs/V7tQAA==/colls/V7tQANV3rAk=/docs/V7tQANV3rAkDAAAAAAAAAA==/',
      etag: '6c006596-0000-0000-0000-53e9cac70000',
      attachments: 'attachments/',
      Price: 200
    }


<span data-ttu-id="f96df-378">Triggers, unlike stored procedures, cannot be executed directly.</span><span class="sxs-lookup"><span data-stu-id="f96df-378">Triggers, unlike stored procedures, cannot be executed directly.</span></span> <span data-ttu-id="f96df-379">Instead they are executed as part of an operation on a document.</span><span class="sxs-lookup"><span data-stu-id="f96df-379">Instead they are executed as part of an operation on a document.</span></span> <span data-ttu-id="f96df-380">You can specify the triggers to run with a request using HTTP headers.</span><span class="sxs-lookup"><span data-stu-id="f96df-380">You can specify the triggers to run with a request using HTTP headers.</span></span> <span data-ttu-id="f96df-381">The following code shows the request to create a document.</span><span class="sxs-lookup"><span data-stu-id="f96df-381">The following code shows the request to create a document.</span></span>

    POST https://<url>/docs/ HTTP/1.1
    authorization: <<auth>>
    x-ms-date: Thu, 07 Aug 2014 03:43:10 GMT
    x-ms-documentdb-pre-trigger-include: validateDocumentContents 
    x-ms-documentdb-post-trigger-include: bookCreationPostTrigger

    {
       "name": "newDocument",
       "title": "The Wizard of Oz",
       "author": "Frank Baum",
       "pages": 92
    }


<span data-ttu-id="f96df-382">Here the pre-trigger to be run with the request is specified in the x-ms-documentdb-pre-trigger-include header.</span><span class="sxs-lookup"><span data-stu-id="f96df-382">Here the pre-trigger to be run with the request is specified in the x-ms-documentdb-pre-trigger-include header.</span></span> <span data-ttu-id="f96df-383">Correspondingly, any post-triggers are given in the x-ms-documentdb-post-trigger-include header.</span><span class="sxs-lookup"><span data-stu-id="f96df-383">Correspondingly, any post-triggers are given in the x-ms-documentdb-post-trigger-include header.</span></span> <span data-ttu-id="f96df-384">Both pre- and post-triggers can be specified for a given request.</span><span class="sxs-lookup"><span data-stu-id="f96df-384">Both pre- and post-triggers can be specified for a given request.</span></span>

## <a name="sample-code"></a><span data-ttu-id="f96df-385">Sample code</span><span class="sxs-lookup"><span data-stu-id="f96df-385">Sample code</span></span>
<span data-ttu-id="f96df-386">You can find more server-side code examples (including [bulk-delete](https://github.com/Azure/azure-cosmosdb-js-server/blob/master/samples/stored-procedures/bulkDelete.js), and [update](https://github.com/Azure/azure-cosmosdb-js-server/blob/master/samples/stored-procedures/update.js)) in the [GitHub repository](https://github.com/Azure/azure-cosmosdb-js-server/tree/master/samples).</span><span class="sxs-lookup"><span data-stu-id="f96df-386">You can find more server-side code examples (including [bulk-delete](https://github.com/Azure/azure-cosmosdb-js-server/blob/master/samples/stored-procedures/bulkDelete.js), and [update](https://github.com/Azure/azure-cosmosdb-js-server/blob/master/samples/stored-procedures/update.js)) in the [GitHub repository](https://github.com/Azure/azure-cosmosdb-js-server/tree/master/samples).</span></span>

<span data-ttu-id="f96df-387">Want to share your awesome stored procedure? contribute to the repository and create a pull-request!</span><span class="sxs-lookup"><span data-stu-id="f96df-387">Want to share your awesome stored procedure? contribute to the repository and create a pull-request!</span></span> 

## <a name="next-steps"></a><span data-ttu-id="f96df-388">Next steps</span><span class="sxs-lookup"><span data-stu-id="f96df-388">Next steps</span></span>
<span data-ttu-id="f96df-389">Once you have one or more stored procedures, triggers, and user-defined functions created, you can load them and view them in the Azure portal using Data Explorer.</span><span class="sxs-lookup"><span data-stu-id="f96df-389">Once you have one or more stored procedures, triggers, and user-defined functions created, you can load them and view them in the Azure portal using Data Explorer.</span></span>

<span data-ttu-id="f96df-390">You may also find the following references and resources useful in your path to learn more about Azure Cosmos dB server-side programming:</span><span class="sxs-lookup"><span data-stu-id="f96df-390">You may also find the following references and resources useful in your path to learn more about Azure Cosmos dB server-side programming:</span></span>

* [<span data-ttu-id="f96df-391">Azure Cosmos DB SDKs</span><span class="sxs-lookup"><span data-stu-id="f96df-391">Azure Cosmos DB SDKs</span></span>](sql-api-sdk-dotnet.md)
* [<span data-ttu-id="f96df-392">DocumentDB Studio</span><span class="sxs-lookup"><span data-stu-id="f96df-392">DocumentDB Studio</span></span>](https://github.com/mingaliu/DocumentDBStudio/releases)
* [<span data-ttu-id="f96df-393">JSON</span><span class="sxs-lookup"><span data-stu-id="f96df-393">JSON</span></span>](http://www.json.org/) 
* [<span data-ttu-id="f96df-394">JavaScript ECMA-262</span><span class="sxs-lookup"><span data-stu-id="f96df-394">JavaScript ECMA-262</span></span>](http://www.ecma-international.org/publications/standards/Ecma-262.htm)
* [<span data-ttu-id="f96df-395">Secure and Portable Database Extensibility</span><span class="sxs-lookup"><span data-stu-id="f96df-395">Secure and Portable Database Extensibility</span></span>](http://dl.acm.org/citation.cfm?id=276339) 
* [<span data-ttu-id="f96df-396">Service Oriented Database Architecture</span><span class="sxs-lookup"><span data-stu-id="f96df-396">Service Oriented Database Architecture</span></span>](http://dl.acm.org/citation.cfm?id=1066267&coll=Portal&dl=GUIDE) 
* [<span data-ttu-id="f96df-397">Hosting the .NET Runtime in Microsoft SQL server</span><span class="sxs-lookup"><span data-stu-id="f96df-397">Hosting the .NET Runtime in Microsoft SQL server</span></span>](http://dl.acm.org/citation.cfm?id=1007669)
