---
title: Server-side JavaScript programming for Azure DocumentDB | Microsoft Docs
description: Learn how to use DocumentDB to write stored procedures, database triggers, and user defined functions (UDFs) in JavaScript. Get database programing tips and more.
keywords: Database triggers, stored procedure, stored procedure, database program, sproc, documentdb, azure, Microsoft azure
services: documentdb
documentationcenter: ''
author: aliuy
manager: jhubbard
editor: mimig
ms.assetid: 0fba7ebd-a4fc-4253-a786-97f1354fbf17
ms.service: documentdb
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/11/2016
ms.author: andrl
ms.openlocfilehash: d337114c123151f06a24e80b0208c6eafb1df487
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662038"
---
# <a name="documentdb-server-side-programming-stored-procedures-database-triggers-and-udfs"></a><span data-ttu-id="514cd-105">DocumentDB server-side programming: Stored procedures, database triggers, and UDFs</span><span class="sxs-lookup"><span data-stu-id="514cd-105">DocumentDB server-side programming: Stored procedures, database triggers, and UDFs</span></span>
<span data-ttu-id="514cd-106">Learn how Azure DocumentDB’s language integrated, transactional execution of JavaScript lets developers write **stored procedures**, **triggers** and **user defined functions (UDFs)** natively in JavaScript.</span><span class="sxs-lookup"><span data-stu-id="514cd-106">Learn how Azure DocumentDB’s language integrated, transactional execution of JavaScript lets developers write **stored procedures**, **triggers** and **user defined functions (UDFs)** natively in JavaScript.</span></span> <span data-ttu-id="514cd-107">This allows you to write database program application logic that can be shipped and executed directly on the database storage partitions</span><span class="sxs-lookup"><span data-stu-id="514cd-107">This allows you to write database program application logic that can be shipped and executed directly on the database storage partitions</span></span> 

<span data-ttu-id="514cd-108">We recommend getting started by watching the following video, where Andrew Liu provides a brief introduction to DocumentDB's server-side database programming model.</span><span class="sxs-lookup"><span data-stu-id="514cd-108">We recommend getting started by watching the following video, where Andrew Liu provides a brief introduction to DocumentDB's server-side database programming model.</span></span> 

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-Demo-A-Quick-Intro-to-Azure-DocumentDBs-Server-Side-Javascript/player]
> 
> 

<span data-ttu-id="514cd-109">Then, return to this article, where you'll learn the answers to the following questions:</span><span class="sxs-lookup"><span data-stu-id="514cd-109">Then, return to this article, where you'll learn the answers to the following questions:</span></span>  

* <span data-ttu-id="514cd-110">How do I write a a stored procedure, trigger, or UDF using JavaScript?</span><span class="sxs-lookup"><span data-stu-id="514cd-110">How do I write a a stored procedure, trigger, or UDF using JavaScript?</span></span>
* <span data-ttu-id="514cd-111">How does DocumentDB guarantee ACID?</span><span class="sxs-lookup"><span data-stu-id="514cd-111">How does DocumentDB guarantee ACID?</span></span>
* <span data-ttu-id="514cd-112">How do transactions work in DocumentDB?</span><span class="sxs-lookup"><span data-stu-id="514cd-112">How do transactions work in DocumentDB?</span></span>
* <span data-ttu-id="514cd-113">What are pre-triggers and post-triggers and how do I write one?</span><span class="sxs-lookup"><span data-stu-id="514cd-113">What are pre-triggers and post-triggers and how do I write one?</span></span>
* <span data-ttu-id="514cd-114">How do I register and execute a stored procedure, trigger, or UDF in a RESTful manner by using HTTP?</span><span class="sxs-lookup"><span data-stu-id="514cd-114">How do I register and execute a stored procedure, trigger, or UDF in a RESTful manner by using HTTP?</span></span>
* <span data-ttu-id="514cd-115">What DocumentDB SDKs are available to create and execute stored procedures, triggers, and UDFs?</span><span class="sxs-lookup"><span data-stu-id="514cd-115">What DocumentDB SDKs are available to create and execute stored procedures, triggers, and UDFs?</span></span>

## <a name="introduction-to-stored-procedure-and-udf-programming"></a><span data-ttu-id="514cd-116">Introduction to Stored Procedure and UDF Programming</span><span class="sxs-lookup"><span data-stu-id="514cd-116">Introduction to Stored Procedure and UDF Programming</span></span>
<span data-ttu-id="514cd-117">This approach of *“JavaScript as a modern day T-SQL”* frees application developers from the complexities of type system mismatches and object-relational mapping technologies.</span><span class="sxs-lookup"><span data-stu-id="514cd-117">This approach of *“JavaScript as a modern day T-SQL”* frees application developers from the complexities of type system mismatches and object-relational mapping technologies.</span></span> <span data-ttu-id="514cd-118">It also has a number of intrinsic advantages that can be utilized to build rich applications:</span><span class="sxs-lookup"><span data-stu-id="514cd-118">It also has a number of intrinsic advantages that can be utilized to build rich applications:</span></span>  

* <span data-ttu-id="514cd-119">**Procedural Logic:** JavaScript as a high level programming language, provides a rich and familiar interface to express business logic.</span><span class="sxs-lookup"><span data-stu-id="514cd-119">**Procedural Logic:** JavaScript as a high level programming language, provides a rich and familiar interface to express business logic.</span></span> <span data-ttu-id="514cd-120">You can perform complex sequences of operations closer to the data.</span><span class="sxs-lookup"><span data-stu-id="514cd-120">You can perform complex sequences of operations closer to the data.</span></span>
* <span data-ttu-id="514cd-121">**Atomic Transactions:** DocumentDB guarantees that database operations performed inside a single stored procedure or trigger are atomic.</span><span class="sxs-lookup"><span data-stu-id="514cd-121">**Atomic Transactions:** DocumentDB guarantees that database operations performed inside a single stored procedure or trigger are atomic.</span></span> <span data-ttu-id="514cd-122">This lets an application combine related operations in a single batch so that either all of them succeed or none of them succeed.</span><span class="sxs-lookup"><span data-stu-id="514cd-122">This lets an application combine related operations in a single batch so that either all of them succeed or none of them succeed.</span></span> 
* <span data-ttu-id="514cd-123">**Performance:** The fact that JSON is intrinsically mapped to the Javascript language type system and is also the basic unit of storage in DocumentDB allows for a number of optimizations like lazy materialization of JSON documents in the buffer pool and making them available on-demand to the executing code.</span><span class="sxs-lookup"><span data-stu-id="514cd-123">**Performance:** The fact that JSON is intrinsically mapped to the Javascript language type system and is also the basic unit of storage in DocumentDB allows for a number of optimizations like lazy materialization of JSON documents in the buffer pool and making them available on-demand to the executing code.</span></span> <span data-ttu-id="514cd-124">There are more performance benefits associated with shipping business logic to the database:</span><span class="sxs-lookup"><span data-stu-id="514cd-124">There are more performance benefits associated with shipping business logic to the database:</span></span>
  
  * <span data-ttu-id="514cd-125">Batching – Developers can group operations like inserts and submit them in bulk.</span><span class="sxs-lookup"><span data-stu-id="514cd-125">Batching – Developers can group operations like inserts and submit them in bulk.</span></span> <span data-ttu-id="514cd-126">The network traffic latency cost and the store overhead to create separate transactions are reduced significantly.</span><span class="sxs-lookup"><span data-stu-id="514cd-126">The network traffic latency cost and the store overhead to create separate transactions are reduced significantly.</span></span> 
  * <span data-ttu-id="514cd-127">Pre-compilation – DocumentDB precompiles stored procedures, triggers and user defined functions (UDFs) to avoid JavaScript compilation cost for each invocation.</span><span class="sxs-lookup"><span data-stu-id="514cd-127">Pre-compilation – DocumentDB precompiles stored procedures, triggers and user defined functions (UDFs) to avoid JavaScript compilation cost for each invocation.</span></span> <span data-ttu-id="514cd-128">The overhead of building the byte code for the procedural logic is amortized to a minimal value.</span><span class="sxs-lookup"><span data-stu-id="514cd-128">The overhead of building the byte code for the procedural logic is amortized to a minimal value.</span></span>
  * <span data-ttu-id="514cd-129">Sequencing – Many operations need a side-effect (“trigger”) that potentially involves doing one or many secondary store operations.</span><span class="sxs-lookup"><span data-stu-id="514cd-129">Sequencing – Many operations need a side-effect (“trigger”) that potentially involves doing one or many secondary store operations.</span></span> <span data-ttu-id="514cd-130">Aside from atomicity, this is more performant when moved to the server.</span><span class="sxs-lookup"><span data-stu-id="514cd-130">Aside from atomicity, this is more performant when moved to the server.</span></span> 
* <span data-ttu-id="514cd-131">**Encapsulation:** Stored procedures can be used to group business logic in one place.</span><span class="sxs-lookup"><span data-stu-id="514cd-131">**Encapsulation:** Stored procedures can be used to group business logic in one place.</span></span> <span data-ttu-id="514cd-132">This has two advantages:</span><span class="sxs-lookup"><span data-stu-id="514cd-132">This has two advantages:</span></span>
  * <span data-ttu-id="514cd-133">It adds an abstraction layer on top of the raw data, which enables data architects to evolve their applications independently from the data.</span><span class="sxs-lookup"><span data-stu-id="514cd-133">It adds an abstraction layer on top of the raw data, which enables data architects to evolve their applications independently from the data.</span></span> <span data-ttu-id="514cd-134">This is particularly advantageous when the data is schema-less, due to the brittle assumptions that may need to be baked into the application if they have to deal with data directly.</span><span class="sxs-lookup"><span data-stu-id="514cd-134">This is particularly advantageous when the data is schema-less, due to the brittle assumptions that may need to be baked into the application if they have to deal with data directly.</span></span>  
  * <span data-ttu-id="514cd-135">This abstraction lets enterprises keep their data secure by streamlining the access from the scripts.</span><span class="sxs-lookup"><span data-stu-id="514cd-135">This abstraction lets enterprises keep their data secure by streamlining the access from the scripts.</span></span>  

<span data-ttu-id="514cd-136">The creation and execution of database triggers, stored procedure and custom query operators is supported through the [REST API](https://msdn.microsoft.com/library/azure/dn781481.aspx), [DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio/releases), and [client SDKs](documentdb-sdk-dotnet.md) in many platforms including .NET, Node.js and JavaScript.</span><span class="sxs-lookup"><span data-stu-id="514cd-136">The creation and execution of database triggers, stored procedure and custom query operators is supported through the [REST API](https://msdn.microsoft.com/library/azure/dn781481.aspx), [DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio/releases), and [client SDKs](documentdb-sdk-dotnet.md) in many platforms including .NET, Node.js and JavaScript.</span></span>

<span data-ttu-id="514cd-137">This tutorial uses the [Node.js SDK with Q Promises](http://azure.github.io/azure-documentdb-node-q/) to illustrate syntax and usage of stored procedures, triggers, and UDFs.</span><span class="sxs-lookup"><span data-stu-id="514cd-137">This tutorial uses the [Node.js SDK with Q Promises](http://azure.github.io/azure-documentdb-node-q/) to illustrate syntax and usage of stored procedures, triggers, and UDFs.</span></span>   

## <a name="stored-procedures"></a><span data-ttu-id="514cd-138">Stored procedures</span><span class="sxs-lookup"><span data-stu-id="514cd-138">Stored procedures</span></span>
### <a name="example-write-a-simple-stored-procedure"></a><span data-ttu-id="514cd-139">Example: Write a simple stored procedure</span><span class="sxs-lookup"><span data-stu-id="514cd-139">Example: Write a simple stored procedure</span></span>
<span data-ttu-id="514cd-140">Let’s start with a simple stored procedure that returns a “Hello World” response.</span><span class="sxs-lookup"><span data-stu-id="514cd-140">Let’s start with a simple stored procedure that returns a “Hello World” response.</span></span>

    var helloWorldStoredProc = {
        id: "helloWorld",
        serverScript: function () {
            var context = getContext();
            var response = context.getResponse();

            response.setBody("Hello, World");
        }
    }


<span data-ttu-id="514cd-141">Stored procedures are registered per collection, and can operate on any document and attachment present in that collection.</span><span class="sxs-lookup"><span data-stu-id="514cd-141">Stored procedures are registered per collection, and can operate on any document and attachment present in that collection.</span></span> <span data-ttu-id="514cd-142">The following snippet shows how to register the helloWorld stored procedure with a collection.</span><span class="sxs-lookup"><span data-stu-id="514cd-142">The following snippet shows how to register the helloWorld stored procedure with a collection.</span></span> 

    // register the stored procedure
    var createdStoredProcedure;
    client.createStoredProcedureAsync('dbs/testdb/colls/testColl', helloWorldStoredProc)
        .then(function (response) {
            createdStoredProcedure = response.resource;
            console.log("Successfully created stored procedure");
        }, function (error) {
            console.log("Error", error);
        });


<span data-ttu-id="514cd-143">Once the stored procedure is registered, we can execute it against the collection, and read the results back at the client.</span><span class="sxs-lookup"><span data-stu-id="514cd-143">Once the stored procedure is registered, we can execute it against the collection, and read the results back at the client.</span></span> 

    // execute the stored procedure
    client.executeStoredProcedureAsync('dbs/testdb/colls/testColl/sprocs/helloWorld')
        .then(function (response) {
            console.log(response.result); // "Hello, World"
        }, function (err) {
            console.log("Error", error);
        });


<span data-ttu-id="514cd-144">The context object provides access to all operations that can be performed on DocumentDB storage, as well as access to the request and response objects.</span><span class="sxs-lookup"><span data-stu-id="514cd-144">The context object provides access to all operations that can be performed on DocumentDB storage, as well as access to the request and response objects.</span></span> <span data-ttu-id="514cd-145">In this case, we used the response object to set the body of the response that was sent back to the client.</span><span class="sxs-lookup"><span data-stu-id="514cd-145">In this case, we used the response object to set the body of the response that was sent back to the client.</span></span> <span data-ttu-id="514cd-146">For more details, refer to the [DocumentDB JavaScript server SDK documentation](http://azure.github.io/azure-documentdb-js-server/).</span><span class="sxs-lookup"><span data-stu-id="514cd-146">For more details, refer to the [DocumentDB JavaScript server SDK documentation](http://azure.github.io/azure-documentdb-js-server/).</span></span>  

<span data-ttu-id="514cd-147">Let us expand on this example and add more database related functionality to the stored procedure.</span><span class="sxs-lookup"><span data-stu-id="514cd-147">Let us expand on this example and add more database related functionality to the stored procedure.</span></span> <span data-ttu-id="514cd-148">Stored procedures can create, update, read, query and delete documents and attachments inside the collection.</span><span class="sxs-lookup"><span data-stu-id="514cd-148">Stored procedures can create, update, read, query and delete documents and attachments inside the collection.</span></span>    

### <a name="example-write-a-stored-procedure-to-create-a-document"></a><span data-ttu-id="514cd-149">Example: Write a stored procedure to create a document</span><span class="sxs-lookup"><span data-stu-id="514cd-149">Example: Write a stored procedure to create a document</span></span>
<span data-ttu-id="514cd-150">The next snippet shows how to use the context object to interact with DocumentDB resources.</span><span class="sxs-lookup"><span data-stu-id="514cd-150">The next snippet shows how to use the context object to interact with DocumentDB resources.</span></span>

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


<span data-ttu-id="514cd-151">This stored procedure takes as input documentToCreate, the body of a document to be created in the current collection.</span><span class="sxs-lookup"><span data-stu-id="514cd-151">This stored procedure takes as input documentToCreate, the body of a document to be created in the current collection.</span></span> <span data-ttu-id="514cd-152">All such operations are asynchronous and depend on JavaScript function callbacks.</span><span class="sxs-lookup"><span data-stu-id="514cd-152">All such operations are asynchronous and depend on JavaScript function callbacks.</span></span> <span data-ttu-id="514cd-153">The callback function has two parameters, one for the error object in case the operation fails, and one for the created object.</span><span class="sxs-lookup"><span data-stu-id="514cd-153">The callback function has two parameters, one for the error object in case the operation fails, and one for the created object.</span></span> <span data-ttu-id="514cd-154">Inside the callback, users can either handle the exception or throw an error.</span><span class="sxs-lookup"><span data-stu-id="514cd-154">Inside the callback, users can either handle the exception or throw an error.</span></span> <span data-ttu-id="514cd-155">In case a callback is not provided and there is an error, the DocumentDB runtime throws an error.</span><span class="sxs-lookup"><span data-stu-id="514cd-155">In case a callback is not provided and there is an error, the DocumentDB runtime throws an error.</span></span>   

<span data-ttu-id="514cd-156">In the example above, the callback throws an error if the operation failed.</span><span class="sxs-lookup"><span data-stu-id="514cd-156">In the example above, the callback throws an error if the operation failed.</span></span> <span data-ttu-id="514cd-157">Otherwise, it sets the id of the created document as the body of the response to the client.</span><span class="sxs-lookup"><span data-stu-id="514cd-157">Otherwise, it sets the id of the created document as the body of the response to the client.</span></span> <span data-ttu-id="514cd-158">Here is how this stored procedure is executed with input parameters.</span><span class="sxs-lookup"><span data-stu-id="514cd-158">Here is how this stored procedure is executed with input parameters.</span></span>

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


<span data-ttu-id="514cd-159">Note that this stored procedure can be modified to take an array of document bodies as input and create them all in the same stored procedure execution instead of multiple network requests to create each of them individually.</span><span class="sxs-lookup"><span data-stu-id="514cd-159">Note that this stored procedure can be modified to take an array of document bodies as input and create them all in the same stored procedure execution instead of multiple network requests to create each of them individually.</span></span> <span data-ttu-id="514cd-160">This can be used to implement an efficient bulk importer for DocumentDB (discussed later in this tutorial).</span><span class="sxs-lookup"><span data-stu-id="514cd-160">This can be used to implement an efficient bulk importer for DocumentDB (discussed later in this tutorial).</span></span>   

<span data-ttu-id="514cd-161">The example described demonstrated how to use stored procedures.</span><span class="sxs-lookup"><span data-stu-id="514cd-161">The example described demonstrated how to use stored procedures.</span></span> <span data-ttu-id="514cd-162">We will cover triggers and user defined functions (UDFs) later in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="514cd-162">We will cover triggers and user defined functions (UDFs) later in the tutorial.</span></span>

## <a name="database-program-transactions"></a><span data-ttu-id="514cd-163">Database program transactions</span><span class="sxs-lookup"><span data-stu-id="514cd-163">Database program transactions</span></span>
<span data-ttu-id="514cd-164">Transaction in a typical database can be defined as a sequence of operations performed as a single logical unit of work.</span><span class="sxs-lookup"><span data-stu-id="514cd-164">Transaction in a typical database can be defined as a sequence of operations performed as a single logical unit of work.</span></span> <span data-ttu-id="514cd-165">Each transaction provides **ACID guarantees**.</span><span class="sxs-lookup"><span data-stu-id="514cd-165">Each transaction provides **ACID guarantees**.</span></span> <span data-ttu-id="514cd-166">ACID is a well-known acronym that stands for four properties -  Atomicity, Consistency, Isolation and Durability.</span><span class="sxs-lookup"><span data-stu-id="514cd-166">ACID is a well-known acronym that stands for four properties -  Atomicity, Consistency, Isolation and Durability.</span></span>  

<span data-ttu-id="514cd-167">Briefly, atomicity guarantees that all the work done inside a transaction is treated as a single unit where either all of it is committed or none.</span><span class="sxs-lookup"><span data-stu-id="514cd-167">Briefly, atomicity guarantees that all the work done inside a transaction is treated as a single unit where either all of it is committed or none.</span></span> <span data-ttu-id="514cd-168">Consistency makes sure that the data is always in a good internal state across transactions.</span><span class="sxs-lookup"><span data-stu-id="514cd-168">Consistency makes sure that the data is always in a good internal state across transactions.</span></span> <span data-ttu-id="514cd-169">Isolation guarantees that no two transactions interfere with each other – generally, most commercial systems provide multiple isolation levels that can be used based on the application needs.</span><span class="sxs-lookup"><span data-stu-id="514cd-169">Isolation guarantees that no two transactions interfere with each other – generally, most commercial systems provide multiple isolation levels that can be used based on the application needs.</span></span> <span data-ttu-id="514cd-170">Durability ensures that any change that’s committed in the database will always be present.</span><span class="sxs-lookup"><span data-stu-id="514cd-170">Durability ensures that any change that’s committed in the database will always be present.</span></span>   

<span data-ttu-id="514cd-171">In DocumentDB, JavaScript is hosted in the same memory space as the database.</span><span class="sxs-lookup"><span data-stu-id="514cd-171">In DocumentDB, JavaScript is hosted in the same memory space as the database.</span></span> <span data-ttu-id="514cd-172">Hence, requests made within stored procedures and triggers execute in the same scope of a database session.</span><span class="sxs-lookup"><span data-stu-id="514cd-172">Hence, requests made within stored procedures and triggers execute in the same scope of a database session.</span></span> <span data-ttu-id="514cd-173">This enables DocumentDB to guarantee ACID for all operations that are part of a single stored procedure/trigger.</span><span class="sxs-lookup"><span data-stu-id="514cd-173">This enables DocumentDB to guarantee ACID for all operations that are part of a single stored procedure/trigger.</span></span> <span data-ttu-id="514cd-174">Consider the following stored procedure definition:</span><span class="sxs-lookup"><span data-stu-id="514cd-174">Consider the following stored procedure definition:</span></span>

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

<span data-ttu-id="514cd-175">This stored procedure uses transactions within a gaming app to trade items between two players in a single operation.</span><span class="sxs-lookup"><span data-stu-id="514cd-175">This stored procedure uses transactions within a gaming app to trade items between two players in a single operation.</span></span> <span data-ttu-id="514cd-176">The stored procedure attempts to read two documents each corresponding to the player IDs passed in as an argument.</span><span class="sxs-lookup"><span data-stu-id="514cd-176">The stored procedure attempts to read two documents each corresponding to the player IDs passed in as an argument.</span></span> <span data-ttu-id="514cd-177">If both player documents are found, then the stored procedure updates the documents by swapping their items.</span><span class="sxs-lookup"><span data-stu-id="514cd-177">If both player documents are found, then the stored procedure updates the documents by swapping their items.</span></span> <span data-ttu-id="514cd-178">If any errors are encountered along the way, it throws a JavaScript exception that implicitly aborts the transaction.</span><span class="sxs-lookup"><span data-stu-id="514cd-178">If any errors are encountered along the way, it throws a JavaScript exception that implicitly aborts the transaction.</span></span>

<span data-ttu-id="514cd-179">If the collection the stored procedure is registered against is a single-partition collection, then the transaction is scoped to all the docuemnts within the collection.</span><span class="sxs-lookup"><span data-stu-id="514cd-179">If the collection the stored procedure is registered against is a single-partition collection, then the transaction is scoped to all the docuemnts within the collection.</span></span> <span data-ttu-id="514cd-180">If the collection is partitioned, then stored procedures are executed in the transaction scope of a single partition key.</span><span class="sxs-lookup"><span data-stu-id="514cd-180">If the collection is partitioned, then stored procedures are executed in the transaction scope of a single partition key.</span></span> <span data-ttu-id="514cd-181">Each stored procedure execution must then include a partition key value corresponding to the scope the transaction must run under.</span><span class="sxs-lookup"><span data-stu-id="514cd-181">Each stored procedure execution must then include a partition key value corresponding to the scope the transaction must run under.</span></span> <span data-ttu-id="514cd-182">For more details, see [DocumentDB Partitioning](documentdb-partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="514cd-182">For more details, see [DocumentDB Partitioning](documentdb-partition-data.md).</span></span>

### <a name="commit-and-rollback"></a><span data-ttu-id="514cd-183">Commit and rollback</span><span class="sxs-lookup"><span data-stu-id="514cd-183">Commit and rollback</span></span>
<span data-ttu-id="514cd-184">Transactions are deeply and natively integrated into DocumentDB’s JavaScript programming model.</span><span class="sxs-lookup"><span data-stu-id="514cd-184">Transactions are deeply and natively integrated into DocumentDB’s JavaScript programming model.</span></span> <span data-ttu-id="514cd-185">Inside a JavaScript function, all operations are automatically wrapped under a single transaction.</span><span class="sxs-lookup"><span data-stu-id="514cd-185">Inside a JavaScript function, all operations are automatically wrapped under a single transaction.</span></span> <span data-ttu-id="514cd-186">If the JavaScript completes without any exception, the operations to the database are committed.</span><span class="sxs-lookup"><span data-stu-id="514cd-186">If the JavaScript completes without any exception, the operations to the database are committed.</span></span> <span data-ttu-id="514cd-187">In effect, the “BEGIN TRANSACTION” and “COMMIT TRANSACTION” statements in relational databases are implicit in DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="514cd-187">In effect, the “BEGIN TRANSACTION” and “COMMIT TRANSACTION” statements in relational databases are implicit in DocumentDB.</span></span>  

<span data-ttu-id="514cd-188">If there is any exception that’s propagated from the script, DocumentDB’s JavaScript runtime will roll back the whole transaction.</span><span class="sxs-lookup"><span data-stu-id="514cd-188">If there is any exception that’s propagated from the script, DocumentDB’s JavaScript runtime will roll back the whole transaction.</span></span> <span data-ttu-id="514cd-189">As shown in the earlier example, throwing an exception is effectively equivalent to a “ROLLBACK TRANSACTION” in DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="514cd-189">As shown in the earlier example, throwing an exception is effectively equivalent to a “ROLLBACK TRANSACTION” in DocumentDB.</span></span>

### <a name="data-consistency"></a><span data-ttu-id="514cd-190">Data consistency</span><span class="sxs-lookup"><span data-stu-id="514cd-190">Data consistency</span></span>
<span data-ttu-id="514cd-191">Stored procedures and triggers are always executed on the primary replica of the DocumentDB collection.</span><span class="sxs-lookup"><span data-stu-id="514cd-191">Stored procedures and triggers are always executed on the primary replica of the DocumentDB collection.</span></span> <span data-ttu-id="514cd-192">This ensures that reads from inside stored procedures offer strong consistency.</span><span class="sxs-lookup"><span data-stu-id="514cd-192">This ensures that reads from inside stored procedures offer strong consistency.</span></span> <span data-ttu-id="514cd-193">Queries using user defined functions can be executed on the primary or any secondary replica, but we ensure to meet the requested consistency level by choosing the appropriate replica.</span><span class="sxs-lookup"><span data-stu-id="514cd-193">Queries using user defined functions can be executed on the primary or any secondary replica, but we ensure to meet the requested consistency level by choosing the appropriate replica.</span></span>

## <a name="bounded-execution"></a><span data-ttu-id="514cd-194">Bounded execution</span><span class="sxs-lookup"><span data-stu-id="514cd-194">Bounded execution</span></span>
<span data-ttu-id="514cd-195">All DocumentDB operations must complete within the server specified request timeout duration.</span><span class="sxs-lookup"><span data-stu-id="514cd-195">All DocumentDB operations must complete within the server specified request timeout duration.</span></span> <span data-ttu-id="514cd-196">This constraint also applies to JavaScript functions (stored procedures, triggers and user-defined functions).</span><span class="sxs-lookup"><span data-stu-id="514cd-196">This constraint also applies to JavaScript functions (stored procedures, triggers and user-defined functions).</span></span> <span data-ttu-id="514cd-197">If an operation does not complete with that time limit, the transaction is rolled back.</span><span class="sxs-lookup"><span data-stu-id="514cd-197">If an operation does not complete with that time limit, the transaction is rolled back.</span></span> <span data-ttu-id="514cd-198">JavaScript functions must finish within the time limit or implement a continuation based model to batch/resume execution.</span><span class="sxs-lookup"><span data-stu-id="514cd-198">JavaScript functions must finish within the time limit or implement a continuation based model to batch/resume execution.</span></span>  

<span data-ttu-id="514cd-199">In order to simplify development of stored procedures and triggers to handle time limits, all functions under the collection object (for create, read, replace, and delete of documents and attachments) return a Boolean value that represents whether that operation will complete.</span><span class="sxs-lookup"><span data-stu-id="514cd-199">In order to simplify development of stored procedures and triggers to handle time limits, all functions under the collection object (for create, read, replace, and delete of documents and attachments) return a Boolean value that represents whether that operation will complete.</span></span> <span data-ttu-id="514cd-200">If this value is false, it is an indication that the time limit is about to expire and that the procedure must wrap up execution.</span><span class="sxs-lookup"><span data-stu-id="514cd-200">If this value is false, it is an indication that the time limit is about to expire and that the procedure must wrap up execution.</span></span>  <span data-ttu-id="514cd-201">Operations queued prior to the first unaccepted store operation are guaranteed to complete if the stored procedure completes in time and does not queue any more requests.</span><span class="sxs-lookup"><span data-stu-id="514cd-201">Operations queued prior to the first unaccepted store operation are guaranteed to complete if the stored procedure completes in time and does not queue any more requests.</span></span>  

<span data-ttu-id="514cd-202">JavaScript functions are also bounded on resource consumption.</span><span class="sxs-lookup"><span data-stu-id="514cd-202">JavaScript functions are also bounded on resource consumption.</span></span> <span data-ttu-id="514cd-203">DocumentDB reserves throughput per collection based on the provisioned size of a database account.</span><span class="sxs-lookup"><span data-stu-id="514cd-203">DocumentDB reserves throughput per collection based on the provisioned size of a database account.</span></span> <span data-ttu-id="514cd-204">Throughput is expressed in terms of a normalized unit of CPU, memory and IO consumption called request units or RUs.</span><span class="sxs-lookup"><span data-stu-id="514cd-204">Throughput is expressed in terms of a normalized unit of CPU, memory and IO consumption called request units or RUs.</span></span> <span data-ttu-id="514cd-205">JavaScript functions can potentially use up a large number of RUs within a short time, and might get rate-limited if the collection’s limit is reached.</span><span class="sxs-lookup"><span data-stu-id="514cd-205">JavaScript functions can potentially use up a large number of RUs within a short time, and might get rate-limited if the collection’s limit is reached.</span></span> <span data-ttu-id="514cd-206">Resource intensive stored procedures might also be quarantined to ensure availability of primitive database operations.</span><span class="sxs-lookup"><span data-stu-id="514cd-206">Resource intensive stored procedures might also be quarantined to ensure availability of primitive database operations.</span></span>  

### <a name="example-bulk-importing-data-into-a-database-program"></a><span data-ttu-id="514cd-207">Example: Bulk importing data into a database program</span><span class="sxs-lookup"><span data-stu-id="514cd-207">Example: Bulk importing data into a database program</span></span>
<span data-ttu-id="514cd-208">Below is an example of a stored procedure that is written to bulk-import documents into a collection.</span><span class="sxs-lookup"><span data-stu-id="514cd-208">Below is an example of a stored procedure that is written to bulk-import documents into a collection.</span></span> <span data-ttu-id="514cd-209">Note how the stored procedure handles bounded execution by checking the Boolean return value from createDocument, and then uses the count of documents inserted in each invocation of the stored procedure to track and resume progress across batches.</span><span class="sxs-lookup"><span data-stu-id="514cd-209">Note how the stored procedure handles bounded execution by checking the Boolean return value from createDocument, and then uses the count of documents inserted in each invocation of the stored procedure to track and resume progress across batches.</span></span>

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

## <a id="trigger"></a> <span data-ttu-id="514cd-210">Database triggers</span><span class="sxs-lookup"><span data-stu-id="514cd-210">Database triggers</span></span>
### <a name="database-pre-triggers"></a><span data-ttu-id="514cd-211">Database pre-triggers</span><span class="sxs-lookup"><span data-stu-id="514cd-211">Database pre-triggers</span></span>
<span data-ttu-id="514cd-212">DocumentDB provides triggers that are executed or triggered by an operation on a document.</span><span class="sxs-lookup"><span data-stu-id="514cd-212">DocumentDB provides triggers that are executed or triggered by an operation on a document.</span></span> <span data-ttu-id="514cd-213">For example, you can specify a pre-trigger when you are creating a document – this pre-trigger will run before the document is created.</span><span class="sxs-lookup"><span data-stu-id="514cd-213">For example, you can specify a pre-trigger when you are creating a document – this pre-trigger will run before the document is created.</span></span> <span data-ttu-id="514cd-214">The following is an example of how pre-triggers can be used to validate the properties of a document that is being created:</span><span class="sxs-lookup"><span data-stu-id="514cd-214">The following is an example of how pre-triggers can be used to validate the properties of a document that is being created:</span></span>

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


<span data-ttu-id="514cd-215">And the corresponding Node.js client-side registration code for the trigger:</span><span class="sxs-lookup"><span data-stu-id="514cd-215">And the corresponding Node.js client-side registration code for the trigger:</span></span>

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


<span data-ttu-id="514cd-216">Pre-triggers cannot have any input parameters.</span><span class="sxs-lookup"><span data-stu-id="514cd-216">Pre-triggers cannot have any input parameters.</span></span> <span data-ttu-id="514cd-217">The request object can be used to manipulate the request message associated with the operation.</span><span class="sxs-lookup"><span data-stu-id="514cd-217">The request object can be used to manipulate the request message associated with the operation.</span></span> <span data-ttu-id="514cd-218">Here, the pre-trigger is being run with the creation of a document, and the request message body contains the document to be created in JSON format.</span><span class="sxs-lookup"><span data-stu-id="514cd-218">Here, the pre-trigger is being run with the creation of a document, and the request message body contains the document to be created in JSON format.</span></span>   

<span data-ttu-id="514cd-219">When triggers are registered, users can specify the operations that it can run with.</span><span class="sxs-lookup"><span data-stu-id="514cd-219">When triggers are registered, users can specify the operations that it can run with.</span></span> <span data-ttu-id="514cd-220">This trigger was created with TriggerOperation.Create, which means the following is not permitted.</span><span class="sxs-lookup"><span data-stu-id="514cd-220">This trigger was created with TriggerOperation.Create, which means the following is not permitted.</span></span>

    var options = { preTriggerInclude: "validateDocumentContents" };

    client.replaceDocumentAsync(docToReplace.self,
                  newDocBody, options)
    .then(function (response) {
        console.log(response.resource);
    }, function (error) {
        console.log("Error", error);
    });

    // Fails, can’t use a create trigger in a replace operation

### <a name="database-post-triggers"></a><span data-ttu-id="514cd-221">Database post-triggers</span><span class="sxs-lookup"><span data-stu-id="514cd-221">Database post-triggers</span></span>
<span data-ttu-id="514cd-222">Post-triggers, like pre-triggers, are associated with an operation on a document and don’t take any input parameters.</span><span class="sxs-lookup"><span data-stu-id="514cd-222">Post-triggers, like pre-triggers, are associated with an operation on a document and don’t take any input parameters.</span></span> <span data-ttu-id="514cd-223">They run **after** the operation has completed, and have access to the response message that is sent to the client.</span><span class="sxs-lookup"><span data-stu-id="514cd-223">They run **after** the operation has completed, and have access to the response message that is sent to the client.</span></span>   

<span data-ttu-id="514cd-224">The following example shows post-triggers in action:</span><span class="sxs-lookup"><span data-stu-id="514cd-224">The following example shows post-triggers in action:</span></span>

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


<span data-ttu-id="514cd-225">The trigger can be registered as shown in the following sample.</span><span class="sxs-lookup"><span data-stu-id="514cd-225">The trigger can be registered as shown in the following sample.</span></span>

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


<span data-ttu-id="514cd-226">This trigger queries for the metadata document and updates it with details about the newly created document.</span><span class="sxs-lookup"><span data-stu-id="514cd-226">This trigger queries for the metadata document and updates it with details about the newly created document.</span></span>  

<span data-ttu-id="514cd-227">One thing that is important to note is the **transactional** execution of triggers in DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="514cd-227">One thing that is important to note is the **transactional** execution of triggers in DocumentDB.</span></span> <span data-ttu-id="514cd-228">This post-trigger runs as part of the same transaction as the creation of the original document.</span><span class="sxs-lookup"><span data-stu-id="514cd-228">This post-trigger runs as part of the same transaction as the creation of the original document.</span></span> <span data-ttu-id="514cd-229">Therefore, if we throw an exception from the post-trigger (say if we are unable to update the metadata document), the whole transaction will fail and be rolled back.</span><span class="sxs-lookup"><span data-stu-id="514cd-229">Therefore, if we throw an exception from the post-trigger (say if we are unable to update the metadata document), the whole transaction will fail and be rolled back.</span></span> <span data-ttu-id="514cd-230">No document will be created, and an exception will be returned.</span><span class="sxs-lookup"><span data-stu-id="514cd-230">No document will be created, and an exception will be returned.</span></span>  

## <a id="udf"></a><span data-ttu-id="514cd-231">User-defined functions</span><span class="sxs-lookup"><span data-stu-id="514cd-231">User-defined functions</span></span>
<span data-ttu-id="514cd-232">User-defined functions (UDFs) are used to extend the DocumentDB SQL query language grammar and implement custom business logic.</span><span class="sxs-lookup"><span data-stu-id="514cd-232">User-defined functions (UDFs) are used to extend the DocumentDB SQL query language grammar and implement custom business logic.</span></span> <span data-ttu-id="514cd-233">They can only be called from inside queries.</span><span class="sxs-lookup"><span data-stu-id="514cd-233">They can only be called from inside queries.</span></span> <span data-ttu-id="514cd-234">They do not have access to the context object and are meant to be used as compute-only JavaScript.</span><span class="sxs-lookup"><span data-stu-id="514cd-234">They do not have access to the context object and are meant to be used as compute-only JavaScript.</span></span> <span data-ttu-id="514cd-235">Therefore, UDFs can be run on secondary replicas of the DocumentDB service.</span><span class="sxs-lookup"><span data-stu-id="514cd-235">Therefore, UDFs can be run on secondary replicas of the DocumentDB service.</span></span>  

<span data-ttu-id="514cd-236">The following sample creates a UDF to calculate income tax based on rates for various income brackets, and then uses it inside a query to find all people who paid more than $20,000 in taxes.</span><span class="sxs-lookup"><span data-stu-id="514cd-236">The following sample creates a UDF to calculate income tax based on rates for various income brackets, and then uses it inside a query to find all people who paid more than $20,000 in taxes.</span></span>

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


<span data-ttu-id="514cd-237">The UDF can subsequently be used in queries like in the following sample:</span><span class="sxs-lookup"><span data-stu-id="514cd-237">The UDF can subsequently be used in queries like in the following sample:</span></span>

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

## <a name="javascript-language-integrated-query-api"></a><span data-ttu-id="514cd-238">JavaScript language-integrated query API</span><span class="sxs-lookup"><span data-stu-id="514cd-238">JavaScript language-integrated query API</span></span>
<span data-ttu-id="514cd-239">In addition to issuing queries using DocumentDB’s SQL grammar, the server-side SDK allows you to perform optimized queries using a fluent JavaScript interface without any knowledge of SQL.</span><span class="sxs-lookup"><span data-stu-id="514cd-239">In addition to issuing queries using DocumentDB’s SQL grammar, the server-side SDK allows you to perform optimized queries using a fluent JavaScript interface without any knowledge of SQL.</span></span> <span data-ttu-id="514cd-240">The JavaScript query API allows you to programmatically build queries by passing predicate functions into chainable function calls, with a syntax familiar to ECMAScript5's Array built-ins and popular JavaScript libraries like lodash.</span><span class="sxs-lookup"><span data-stu-id="514cd-240">The JavaScript query API allows you to programmatically build queries by passing predicate functions into chainable function calls, with a syntax familiar to ECMAScript5's Array built-ins and popular JavaScript libraries like lodash.</span></span> <span data-ttu-id="514cd-241">Queries are parsed by the JavaScript runtime to be executed efficiently using DocumentDB’s indices.</span><span class="sxs-lookup"><span data-stu-id="514cd-241">Queries are parsed by the JavaScript runtime to be executed efficiently using DocumentDB’s indices.</span></span>

> [!NOTE]
> <span data-ttu-id="514cd-242">`__` (double-underscore) is an alias to `getContext().getCollection()`.</span><span class="sxs-lookup"><span data-stu-id="514cd-242">`__` (double-underscore) is an alias to `getContext().getCollection()`.</span></span>
> <br/>
> <span data-ttu-id="514cd-243">In other words, you can use `__` or `getContext().getCollection()` to access the JavaScript query API.</span><span class="sxs-lookup"><span data-stu-id="514cd-243">In other words, you can use `__` or `getContext().getCollection()` to access the JavaScript query API.</span></span>
> 
> 

<span data-ttu-id="514cd-244">Supported functions include:</span><span class="sxs-lookup"><span data-stu-id="514cd-244">Supported functions include:</span></span>

<ul>
<li><span data-ttu-id="514cd-245">
<b>chain() ... .value([callback] [, options])</b>
</span><span class="sxs-lookup"><span data-stu-id="514cd-245">
<b>chain() ... .value([callback] [, options])</b>
</span></span><ul>
<li>
<span data-ttu-id="514cd-246">Starts a chained call which must be terminated with value().</span><span class="sxs-lookup"><span data-stu-id="514cd-246">Starts a chained call which must be terminated with value().</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="514cd-247">
<b>filter(predicateFunction [, options] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="514cd-247">
<b>filter(predicateFunction [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="514cd-248">Filters the input using a predicate function which returns true/false in order to filter in/out input documents into the resulting set.</span><span class="sxs-lookup"><span data-stu-id="514cd-248">Filters the input using a predicate function which returns true/false in order to filter in/out input documents into the resulting set.</span></span> <span data-ttu-id="514cd-249">This behaves similar to a WHERE clause in SQL.</span><span class="sxs-lookup"><span data-stu-id="514cd-249">This behaves similar to a WHERE clause in SQL.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="514cd-250">
<b>map(transformationFunction [, options] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="514cd-250">
<b>map(transformationFunction [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="514cd-251">Applies a projection given a transformation function which maps each input item to a JavaScript object or value.</span><span class="sxs-lookup"><span data-stu-id="514cd-251">Applies a projection given a transformation function which maps each input item to a JavaScript object or value.</span></span> <span data-ttu-id="514cd-252">This behaves similar to a SELECT clause in SQL.</span><span class="sxs-lookup"><span data-stu-id="514cd-252">This behaves similar to a SELECT clause in SQL.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="514cd-253">
<b>pluck([propertyName] [, options] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="514cd-253">
<b>pluck([propertyName] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="514cd-254">This is a shortcut for a map which extracts the value of a single property from each input item.</span><span class="sxs-lookup"><span data-stu-id="514cd-254">This is a shortcut for a map which extracts the value of a single property from each input item.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="514cd-255">
<b>flatten([isShallow] [, options] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="514cd-255">
<b>flatten([isShallow] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="514cd-256">Combines and flattens arrays from each input item in to a single array.</span><span class="sxs-lookup"><span data-stu-id="514cd-256">Combines and flattens arrays from each input item in to a single array.</span></span> <span data-ttu-id="514cd-257">This behaves similar to SelectMany in LINQ.</span><span class="sxs-lookup"><span data-stu-id="514cd-257">This behaves similar to SelectMany in LINQ.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="514cd-258">
<b>sortBy([predicate] [, options] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="514cd-258">
<b>sortBy([predicate] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="514cd-259">Produce a new set of documents by sorting the documents in the input document stream in ascending order using the given predicate.</span><span class="sxs-lookup"><span data-stu-id="514cd-259">Produce a new set of documents by sorting the documents in the input document stream in ascending order using the given predicate.</span></span> <span data-ttu-id="514cd-260">This behaves similar to a ORDER BY clause in SQL.</span><span class="sxs-lookup"><span data-stu-id="514cd-260">This behaves similar to a ORDER BY clause in SQL.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="514cd-261">
<b>sortByDescending([predicate] [, options] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="514cd-261">
<b>sortByDescending([predicate] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="514cd-262">Produce a new set of documents by sorting the documents in the input document stream in descending order using the given predicate.</span><span class="sxs-lookup"><span data-stu-id="514cd-262">Produce a new set of documents by sorting the documents in the input document stream in descending order using the given predicate.</span></span> <span data-ttu-id="514cd-263">This behaves similar to a ORDER BY x DESC clause in SQL.</span><span class="sxs-lookup"><span data-stu-id="514cd-263">This behaves similar to a ORDER BY x DESC clause in SQL.</span></span>
</li>
</ul>
</li>
</ul>


<span data-ttu-id="514cd-264">When included inside predicate and/or selector functions, the following JavaScript constructs get automatically optimized to run directly on DocumentDB indices:</span><span class="sxs-lookup"><span data-stu-id="514cd-264">When included inside predicate and/or selector functions, the following JavaScript constructs get automatically optimized to run directly on DocumentDB indices:</span></span>

* <span data-ttu-id="514cd-265">Simple operators: = + - \* / % | ^ &amp; == != === !=== &lt; &gt; &lt;= &gt;= || &amp;&amp; &lt;&lt; &gt;&gt; &gt;&gt;&gt;!</span><span class="sxs-lookup"><span data-stu-id="514cd-265">Simple operators: = + - \* / % | ^ &amp; == != === !=== &lt; &gt; &lt;= &gt;= || &amp;&amp; &lt;&lt; &gt;&gt; &gt;&gt;&gt;!</span></span> ~
* <span data-ttu-id="514cd-266">Literals, including the object literal: {}</span><span class="sxs-lookup"><span data-stu-id="514cd-266">Literals, including the object literal: {}</span></span>
* <span data-ttu-id="514cd-267">var, return</span><span class="sxs-lookup"><span data-stu-id="514cd-267">var, return</span></span>

<span data-ttu-id="514cd-268">The following JavaScript constructs do not get optimized for DocumentDB indices:</span><span class="sxs-lookup"><span data-stu-id="514cd-268">The following JavaScript constructs do not get optimized for DocumentDB indices:</span></span>

* <span data-ttu-id="514cd-269">Control flow (e.g. if, for, while)</span><span class="sxs-lookup"><span data-stu-id="514cd-269">Control flow (e.g. if, for, while)</span></span>
* <span data-ttu-id="514cd-270">Function calls</span><span class="sxs-lookup"><span data-stu-id="514cd-270">Function calls</span></span>

<span data-ttu-id="514cd-271">For more information, please see our [Server-Side JSDocs](http://azure.github.io/azure-documentdb-js-server/).</span><span class="sxs-lookup"><span data-stu-id="514cd-271">For more information, please see our [Server-Side JSDocs](http://azure.github.io/azure-documentdb-js-server/).</span></span>

### <a name="example-write-a-stored-procedure-using-the-javascript-query-api"></a><span data-ttu-id="514cd-272">Example: Write a stored procedure using the JavaScript query API</span><span class="sxs-lookup"><span data-stu-id="514cd-272">Example: Write a stored procedure using the JavaScript query API</span></span>
<span data-ttu-id="514cd-273">The following code sample is an example of how the JavaScript Query API can be used in the context of a stored procedure.</span><span class="sxs-lookup"><span data-stu-id="514cd-273">The following code sample is an example of how the JavaScript Query API can be used in the context of a stored procedure.</span></span> <span data-ttu-id="514cd-274">The stored procedure inserts a document, given by an input parameter, and updates a metadata document, using the `__.filter()` method, with minSize, maxSize, and totalSize based upon the input document's size property.</span><span class="sxs-lookup"><span data-stu-id="514cd-274">The stored procedure inserts a document, given by an input parameter, and updates a metadata document, using the `__.filter()` method, with minSize, maxSize, and totalSize based upon the input document's size property.</span></span>

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

## <a name="sql-to-javascript-cheat-sheet"></a><span data-ttu-id="514cd-275">SQL to Javascript cheat sheet</span><span class="sxs-lookup"><span data-stu-id="514cd-275">SQL to Javascript cheat sheet</span></span>
<span data-ttu-id="514cd-276">The following table presents various SQL queries and the corresponding JavaScript queries.</span><span class="sxs-lookup"><span data-stu-id="514cd-276">The following table presents various SQL queries and the corresponding JavaScript queries.</span></span>

<span data-ttu-id="514cd-277">As with SQL queries, document property keys (e.g. `doc.id`) are case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="514cd-277">As with SQL queries, document property keys (e.g. `doc.id`) are case-sensitive.</span></span>

|<span data-ttu-id="514cd-278">SQL</span><span class="sxs-lookup"><span data-stu-id="514cd-278">SQL</span></span>| <span data-ttu-id="514cd-279">JavaScript Query API</span><span class="sxs-lookup"><span data-stu-id="514cd-279">JavaScript Query API</span></span>|<span data-ttu-id="514cd-280">Description below</span><span class="sxs-lookup"><span data-stu-id="514cd-280">Description below</span></span>|
|---|---|---|
|<span data-ttu-id="514cd-281">SELECT \*</span><span class="sxs-lookup"><span data-stu-id="514cd-281">SELECT \*</span></span><br><span data-ttu-id="514cd-282">FROM docs</span><span class="sxs-lookup"><span data-stu-id="514cd-282">FROM docs</span></span>| <span data-ttu-id="514cd-283">__.map(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="514cd-283">__.map(function(doc) {</span></span> <br><span data-ttu-id="514cd-284">&nbsp;&nbsp;&nbsp;&nbsp;return doc;</span><span class="sxs-lookup"><span data-stu-id="514cd-284">&nbsp;&nbsp;&nbsp;&nbsp;return doc;</span></span><br><span data-ttu-id="514cd-285">});</span><span class="sxs-lookup"><span data-stu-id="514cd-285">});</span></span>|<span data-ttu-id="514cd-286">1</span><span class="sxs-lookup"><span data-stu-id="514cd-286">1</span></span>|
|<span data-ttu-id="514cd-287">SELECT docs.id, docs.message AS msg, docs.actions</span><span class="sxs-lookup"><span data-stu-id="514cd-287">SELECT docs.id, docs.message AS msg, docs.actions</span></span> <br><span data-ttu-id="514cd-288">FROM docs</span><span class="sxs-lookup"><span data-stu-id="514cd-288">FROM docs</span></span>|<span data-ttu-id="514cd-289">__.map(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="514cd-289">__.map(function(doc) {</span></span><br><span data-ttu-id="514cd-290">&nbsp;&nbsp;&nbsp;&nbsp;return {</span><span class="sxs-lookup"><span data-stu-id="514cd-290">&nbsp;&nbsp;&nbsp;&nbsp;return {</span></span><br><span data-ttu-id="514cd-291">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id: doc.id,</span><span class="sxs-lookup"><span data-stu-id="514cd-291">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id: doc.id,</span></span><br><span data-ttu-id="514cd-292">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;msg: doc.message,</span><span class="sxs-lookup"><span data-stu-id="514cd-292">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;msg: doc.message,</span></span><br><span data-ttu-id="514cd-293">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;actions:doc.actions</span><span class="sxs-lookup"><span data-stu-id="514cd-293">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;actions:doc.actions</span></span><br><span data-ttu-id="514cd-294">&nbsp;&nbsp;&nbsp;&nbsp;};</span><span class="sxs-lookup"><span data-stu-id="514cd-294">&nbsp;&nbsp;&nbsp;&nbsp;};</span></span><br><span data-ttu-id="514cd-295">});</span><span class="sxs-lookup"><span data-stu-id="514cd-295">});</span></span>|<span data-ttu-id="514cd-296">2</span><span class="sxs-lookup"><span data-stu-id="514cd-296">2</span></span>|
|<span data-ttu-id="514cd-297">SELECT \*</span><span class="sxs-lookup"><span data-stu-id="514cd-297">SELECT \*</span></span><br><span data-ttu-id="514cd-298">FROM docs</span><span class="sxs-lookup"><span data-stu-id="514cd-298">FROM docs</span></span><br><span data-ttu-id="514cd-299">WHERE docs.id="X998_Y998"</span><span class="sxs-lookup"><span data-stu-id="514cd-299">WHERE docs.id="X998_Y998"</span></span>|<span data-ttu-id="514cd-300">__.filter(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="514cd-300">__.filter(function(doc) {</span></span><br><span data-ttu-id="514cd-301">&nbsp;&nbsp;&nbsp;&nbsp;return doc.id ==="X998_Y998";</span><span class="sxs-lookup"><span data-stu-id="514cd-301">&nbsp;&nbsp;&nbsp;&nbsp;return doc.id ==="X998_Y998";</span></span><br><span data-ttu-id="514cd-302">});</span><span class="sxs-lookup"><span data-stu-id="514cd-302">});</span></span>|<span data-ttu-id="514cd-303">3</span><span class="sxs-lookup"><span data-stu-id="514cd-303">3</span></span>|
|<span data-ttu-id="514cd-304">SELECT \*</span><span class="sxs-lookup"><span data-stu-id="514cd-304">SELECT \*</span></span><br><span data-ttu-id="514cd-305">FROM docs</span><span class="sxs-lookup"><span data-stu-id="514cd-305">FROM docs</span></span><br><span data-ttu-id="514cd-306">WHERE ARRAY_CONTAINS(docs.Tags, 123)</span><span class="sxs-lookup"><span data-stu-id="514cd-306">WHERE ARRAY_CONTAINS(docs.Tags, 123)</span></span>|<span data-ttu-id="514cd-307">__.filter(function(x) {</span><span class="sxs-lookup"><span data-stu-id="514cd-307">__.filter(function(x) {</span></span><br><span data-ttu-id="514cd-308">&nbsp;&nbsp;&nbsp;&nbsp;return x.Tags && x.Tags.indexOf(123) > -1;</span><span class="sxs-lookup"><span data-stu-id="514cd-308">&nbsp;&nbsp;&nbsp;&nbsp;return x.Tags && x.Tags.indexOf(123) > -1;</span></span><br><span data-ttu-id="514cd-309">});</span><span class="sxs-lookup"><span data-stu-id="514cd-309">});</span></span>|<span data-ttu-id="514cd-310">4</span><span class="sxs-lookup"><span data-stu-id="514cd-310">4</span></span>|
|<span data-ttu-id="514cd-311">SELECT docs.id, docs.message AS msg</span><span class="sxs-lookup"><span data-stu-id="514cd-311">SELECT docs.id, docs.message AS msg</span></span><br><span data-ttu-id="514cd-312">FROM docs</span><span class="sxs-lookup"><span data-stu-id="514cd-312">FROM docs</span></span><br><span data-ttu-id="514cd-313">WHERE docs.id="X998_Y998"</span><span class="sxs-lookup"><span data-stu-id="514cd-313">WHERE docs.id="X998_Y998"</span></span>|<span data-ttu-id="514cd-314">__.chain()</span><span class="sxs-lookup"><span data-stu-id="514cd-314">__.chain()</span></span><br><span data-ttu-id="514cd-315">&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="514cd-315">&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {</span></span><br><span data-ttu-id="514cd-316">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc.id ==="X998_Y998";</span><span class="sxs-lookup"><span data-stu-id="514cd-316">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc.id ==="X998_Y998";</span></span><br><span data-ttu-id="514cd-317">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="514cd-317">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="514cd-318">&nbsp;&nbsp;&nbsp;&nbsp;.map(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="514cd-318">&nbsp;&nbsp;&nbsp;&nbsp;.map(function(doc) {</span></span><br><span data-ttu-id="514cd-319">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return {</span><span class="sxs-lookup"><span data-stu-id="514cd-319">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return {</span></span><br><span data-ttu-id="514cd-320">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id: doc.id,</span><span class="sxs-lookup"><span data-stu-id="514cd-320">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id: doc.id,</span></span><br><span data-ttu-id="514cd-321">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;msg: doc.message</span><span class="sxs-lookup"><span data-stu-id="514cd-321">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;msg: doc.message</span></span><br><span data-ttu-id="514cd-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;};</span><span class="sxs-lookup"><span data-stu-id="514cd-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;};</span></span><br><span data-ttu-id="514cd-323">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="514cd-323">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="514cd-324">.value();</span><span class="sxs-lookup"><span data-stu-id="514cd-324">.value();</span></span>|<span data-ttu-id="514cd-325">5</span><span class="sxs-lookup"><span data-stu-id="514cd-325">5</span></span>|
|<span data-ttu-id="514cd-326">SELECT VALUE tag</span><span class="sxs-lookup"><span data-stu-id="514cd-326">SELECT VALUE tag</span></span><br><span data-ttu-id="514cd-327">FROM docs</span><span class="sxs-lookup"><span data-stu-id="514cd-327">FROM docs</span></span><br><span data-ttu-id="514cd-328">JOIN tag IN docs.Tags</span><span class="sxs-lookup"><span data-stu-id="514cd-328">JOIN tag IN docs.Tags</span></span><br><span data-ttu-id="514cd-329">ORDER BY docs._ts</span><span class="sxs-lookup"><span data-stu-id="514cd-329">ORDER BY docs._ts</span></span>|<span data-ttu-id="514cd-330">__.chain()</span><span class="sxs-lookup"><span data-stu-id="514cd-330">__.chain()</span></span><br><span data-ttu-id="514cd-331">&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="514cd-331">&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {</span></span><br><span data-ttu-id="514cd-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc.Tags && Array.isArray(doc.Tags);</span><span class="sxs-lookup"><span data-stu-id="514cd-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc.Tags && Array.isArray(doc.Tags);</span></span><br><span data-ttu-id="514cd-333">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="514cd-333">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="514cd-334">&nbsp;&nbsp;&nbsp;&nbsp;.sortBy(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="514cd-334">&nbsp;&nbsp;&nbsp;&nbsp;.sortBy(function(doc) {</span></span><br><span data-ttu-id="514cd-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc._ts;</span><span class="sxs-lookup"><span data-stu-id="514cd-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc._ts;</span></span><br><span data-ttu-id="514cd-336">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="514cd-336">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="514cd-337">&nbsp;&nbsp;&nbsp;&nbsp;.pluck("Tags")</span><span class="sxs-lookup"><span data-stu-id="514cd-337">&nbsp;&nbsp;&nbsp;&nbsp;.pluck("Tags")</span></span><br><span data-ttu-id="514cd-338">&nbsp;&nbsp;&nbsp;&nbsp;.flatten()</span><span class="sxs-lookup"><span data-stu-id="514cd-338">&nbsp;&nbsp;&nbsp;&nbsp;.flatten()</span></span><br><span data-ttu-id="514cd-339">&nbsp;&nbsp;&nbsp;&nbsp;.value()</span><span class="sxs-lookup"><span data-stu-id="514cd-339">&nbsp;&nbsp;&nbsp;&nbsp;.value()</span></span>|<span data-ttu-id="514cd-340">6</span><span class="sxs-lookup"><span data-stu-id="514cd-340">6</span></span>|

<span data-ttu-id="514cd-341">The following descriptions explain each query in the table above.</span><span class="sxs-lookup"><span data-stu-id="514cd-341">The following descriptions explain each query in the table above.</span></span>
1. <span data-ttu-id="514cd-342">Results in all documents (paginated with continuation token) as is.</span><span class="sxs-lookup"><span data-stu-id="514cd-342">Results in all documents (paginated with continuation token) as is.</span></span>
2. <span data-ttu-id="514cd-343">Projects the id, message (aliased to msg), and action from all documents.</span><span class="sxs-lookup"><span data-stu-id="514cd-343">Projects the id, message (aliased to msg), and action from all documents.</span></span>
3. <span data-ttu-id="514cd-344">Queries for documents with the predicate: id = "X998_Y998".</span><span class="sxs-lookup"><span data-stu-id="514cd-344">Queries for documents with the predicate: id = "X998_Y998".</span></span>
4. <span data-ttu-id="514cd-345">Queries for documents that have a Tags property and Tags is an array containing the value 123.</span><span class="sxs-lookup"><span data-stu-id="514cd-345">Queries for documents that have a Tags property and Tags is an array containing the value 123.</span></span>
5. <span data-ttu-id="514cd-346">Queries for documents with a predicate, id = "X998_Y998", and then projects the id and message (aliased to msg).</span><span class="sxs-lookup"><span data-stu-id="514cd-346">Queries for documents with a predicate, id = "X998_Y998", and then projects the id and message (aliased to msg).</span></span>
6. <span data-ttu-id="514cd-347">Filters for documents which have an array property, Tags, and sorts the resulting documents by the _ts timestamp system property, and then projects + flattens the Tags array.</span><span class="sxs-lookup"><span data-stu-id="514cd-347">Filters for documents which have an array property, Tags, and sorts the resulting documents by the _ts timestamp system property, and then projects + flattens the Tags array.</span></span>


## <a name="runtime-support"></a><span data-ttu-id="514cd-348">Runtime support</span><span class="sxs-lookup"><span data-stu-id="514cd-348">Runtime support</span></span>
<span data-ttu-id="514cd-349">[DocumentDB JavaScript server side SDK](http://azure.github.io/azure-documentdb-js-server/) provides support for the most of the mainstream JavaScript language features as standardized by [ECMA-262](http://www.ecma-international.org/publications/standards/Ecma-262.htm).</span><span class="sxs-lookup"><span data-stu-id="514cd-349">[DocumentDB JavaScript server side SDK](http://azure.github.io/azure-documentdb-js-server/) provides support for the most of the mainstream JavaScript language features as standardized by [ECMA-262](http://www.ecma-international.org/publications/standards/Ecma-262.htm).</span></span>

### <a name="security"></a><span data-ttu-id="514cd-350">Security</span><span class="sxs-lookup"><span data-stu-id="514cd-350">Security</span></span>
<span data-ttu-id="514cd-351">JavaScript stored procedures and triggers are sandboxed so that the effects of one script do not leak to the other without going through the snapshot transaction isolation at the database level.</span><span class="sxs-lookup"><span data-stu-id="514cd-351">JavaScript stored procedures and triggers are sandboxed so that the effects of one script do not leak to the other without going through the snapshot transaction isolation at the database level.</span></span> <span data-ttu-id="514cd-352">The runtime environments are pooled but cleaned of the context after each run.</span><span class="sxs-lookup"><span data-stu-id="514cd-352">The runtime environments are pooled but cleaned of the context after each run.</span></span> <span data-ttu-id="514cd-353">Hence they are guaranteed to be safe of any unintended side effects from each other.</span><span class="sxs-lookup"><span data-stu-id="514cd-353">Hence they are guaranteed to be safe of any unintended side effects from each other.</span></span>

### <a name="pre-compilation"></a><span data-ttu-id="514cd-354">Pre-compilation</span><span class="sxs-lookup"><span data-stu-id="514cd-354">Pre-compilation</span></span>
<span data-ttu-id="514cd-355">Stored procedures, triggers and UDFs are implicitly precompiled to the byte code format in order to avoid compilation cost at the time of each script invocation.</span><span class="sxs-lookup"><span data-stu-id="514cd-355">Stored procedures, triggers and UDFs are implicitly precompiled to the byte code format in order to avoid compilation cost at the time of each script invocation.</span></span> <span data-ttu-id="514cd-356">This ensures invocations of stored procedures are fast and have a low footprint.</span><span class="sxs-lookup"><span data-stu-id="514cd-356">This ensures invocations of stored procedures are fast and have a low footprint.</span></span>

## <a name="client-sdk-support"></a><span data-ttu-id="514cd-357">Client SDK support</span><span class="sxs-lookup"><span data-stu-id="514cd-357">Client SDK support</span></span>
<span data-ttu-id="514cd-358">In addition to the [Node.js](documentdb-sdk-node.md) client, DocumentDB supports [.NET](documentdb-sdk-dotnet.md), [.NET Core](documentdb-sdk-dotnet-core.md), [Java](documentdb-sdk-java.md), [JavaScript](http://azure.github.io/azure-documentdb-js/), and [Python SDKs](documentdb-sdk-python.md).</span><span class="sxs-lookup"><span data-stu-id="514cd-358">In addition to the [Node.js](documentdb-sdk-node.md) client, DocumentDB supports [.NET](documentdb-sdk-dotnet.md), [.NET Core](documentdb-sdk-dotnet-core.md), [Java](documentdb-sdk-java.md), [JavaScript](http://azure.github.io/azure-documentdb-js/), and [Python SDKs](documentdb-sdk-python.md).</span></span> <span data-ttu-id="514cd-359">Stored procedures, triggers and UDFs can be created and executed using any of these SDKs as well.</span><span class="sxs-lookup"><span data-stu-id="514cd-359">Stored procedures, triggers and UDFs can be created and executed using any of these SDKs as well.</span></span> <span data-ttu-id="514cd-360">The following example shows how to create and execute a stored procedure using the .NET client.</span><span class="sxs-lookup"><span data-stu-id="514cd-360">The following example shows how to create and execute a stored procedure using the .NET client.</span></span> <span data-ttu-id="514cd-361">Note how the .NET types are passed into the stored procedure as JSON and read back.</span><span class="sxs-lookup"><span data-stu-id="514cd-361">Note how the .NET types are passed into the stored procedure as JSON and read back.</span></span>

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
    Document createdDocument = await client.ExecuteStoredProcedureAsync<Document>(UriFactory.CreateStoredProcedureUri("db", "coll", "sproc"), document, 1920);


<span data-ttu-id="514cd-362">This sample shows how to use the [.NET SDK](https://msdn.microsoft.com/library/azure/dn948556.aspx) to create a pre-trigger and create a document with the trigger enabled.</span><span class="sxs-lookup"><span data-stu-id="514cd-362">This sample shows how to use the [.NET SDK](https://msdn.microsoft.com/library/azure/dn948556.aspx) to create a pre-trigger and create a document with the trigger enabled.</span></span> 

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


<span data-ttu-id="514cd-363">And the following example shows how to create a user defined function (UDF) and use it in a [DocumentDB SQL query](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="514cd-363">And the following example shows how to create a user defined function (UDF) and use it in a [DocumentDB SQL query](documentdb-sql-query.md).</span></span>

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

## <a name="rest-api"></a><span data-ttu-id="514cd-364">REST API</span><span class="sxs-lookup"><span data-stu-id="514cd-364">REST API</span></span>
<span data-ttu-id="514cd-365">All DocumentDB operations can be performed in a RESTful manner.</span><span class="sxs-lookup"><span data-stu-id="514cd-365">All DocumentDB operations can be performed in a RESTful manner.</span></span> <span data-ttu-id="514cd-366">Stored procedures, triggers and user-defined functions can be registered under a collection by using HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="514cd-366">Stored procedures, triggers and user-defined functions can be registered under a collection by using HTTP POST.</span></span> <span data-ttu-id="514cd-367">The following is an example of how to register a stored procedure:</span><span class="sxs-lookup"><span data-stu-id="514cd-367">The following is an example of how to register a stored procedure:</span></span>

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


<span data-ttu-id="514cd-368">The stored procedure is registered by executing a POST request against the URI dbs/testdb/colls/testColl/sprocs with the body containing the stored procedure to create.</span><span class="sxs-lookup"><span data-stu-id="514cd-368">The stored procedure is registered by executing a POST request against the URI dbs/testdb/colls/testColl/sprocs with the body containing the stored procedure to create.</span></span> <span data-ttu-id="514cd-369">Triggers and UDFs can be registered similarly by issuing a POST against /triggers and /udfs respectively.</span><span class="sxs-lookup"><span data-stu-id="514cd-369">Triggers and UDFs can be registered similarly by issuing a POST against /triggers and /udfs respectively.</span></span>
<span data-ttu-id="514cd-370">This stored procedure can then be executed by issuing a POST request against its resource link:</span><span class="sxs-lookup"><span data-stu-id="514cd-370">This stored procedure can then be executed by issuing a POST request against its resource link:</span></span>

    POST https://<url>/sprocs/<sproc> HTTP/1.1
    authorization: <<auth>>
    x-ms-date: Thu, 07 Aug 2014 03:43:20 GMT


    [ { "name": "TestDocument", "book": "Autumn of the Patriarch"}, "Price", 200 ]


<span data-ttu-id="514cd-371">Here, the input to the stored procedure is passed in the request body.</span><span class="sxs-lookup"><span data-stu-id="514cd-371">Here, the input to the stored procedure is passed in the request body.</span></span> <span data-ttu-id="514cd-372">Note that the input is passed as a JSON array of input parameters.</span><span class="sxs-lookup"><span data-stu-id="514cd-372">Note that the input is passed as a JSON array of input parameters.</span></span> <span data-ttu-id="514cd-373">The stored procedure takes the first input as a document that is a response body.</span><span class="sxs-lookup"><span data-stu-id="514cd-373">The stored procedure takes the first input as a document that is a response body.</span></span> <span data-ttu-id="514cd-374">The response we receive is as follows:</span><span class="sxs-lookup"><span data-stu-id="514cd-374">The response we receive is as follows:</span></span>

    HTTP/1.1 200 OK

    { 
      name: 'TestDocument',
      book: ‘Autumn of the Patriarch’,
      id: ‘V7tQANV3rAkDAAAAAAAAAA==‘,
      ts: 1407830727,
      self: ‘dbs/V7tQAA==/colls/V7tQANV3rAk=/docs/V7tQANV3rAkDAAAAAAAAAA==/’,
      etag: ‘6c006596-0000-0000-0000-53e9cac70000’,
      attachments: ‘attachments/’,
      Price: 200
    }


<span data-ttu-id="514cd-375">Triggers, unlike stored procedures, cannot be executed directly.</span><span class="sxs-lookup"><span data-stu-id="514cd-375">Triggers, unlike stored procedures, cannot be executed directly.</span></span> <span data-ttu-id="514cd-376">Instead they are executed as part of an operation on a document.</span><span class="sxs-lookup"><span data-stu-id="514cd-376">Instead they are executed as part of an operation on a document.</span></span> <span data-ttu-id="514cd-377">We can specify the triggers to run with a request using HTTP headers.</span><span class="sxs-lookup"><span data-stu-id="514cd-377">We can specify the triggers to run with a request using HTTP headers.</span></span> <span data-ttu-id="514cd-378">The following is request to create a document.</span><span class="sxs-lookup"><span data-stu-id="514cd-378">The following is request to create a document.</span></span>

    POST https://<url>/docs/ HTTP/1.1
    authorization: <<auth>>
    x-ms-date: Thu, 07 Aug 2014 03:43:10 GMT
    x-ms-documentdb-pre-trigger-include: validateDocumentContents 
    x-ms-documentdb-post-trigger-include: bookCreationPostTrigger


    {
       "name": "newDocument",
       “title”: “The Wizard of Oz”,
       “author”: “Frank Baum”,
       “pages”: 92
    }


<span data-ttu-id="514cd-379">Here the pre-trigger to be run with the request is specified in the x-ms-documentdb-pre-trigger-include header.</span><span class="sxs-lookup"><span data-stu-id="514cd-379">Here the pre-trigger to be run with the request is specified in the x-ms-documentdb-pre-trigger-include header.</span></span> <span data-ttu-id="514cd-380">Correspondingly, any post-triggers are given in the x-ms-documentdb-post-trigger-include header.</span><span class="sxs-lookup"><span data-stu-id="514cd-380">Correspondingly, any post-triggers are given in the x-ms-documentdb-post-trigger-include header.</span></span> <span data-ttu-id="514cd-381">Note that both pre- and post-triggers can be specified for a given request.</span><span class="sxs-lookup"><span data-stu-id="514cd-381">Note that both pre- and post-triggers can be specified for a given request.</span></span>

## <a name="sample-code"></a><span data-ttu-id="514cd-382">Sample code</span><span class="sxs-lookup"><span data-stu-id="514cd-382">Sample code</span></span>
<span data-ttu-id="514cd-383">You can find more server-side code examples (including [bulk-delete](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/bulkDelete.js), and [update](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/update.js)) on our [GitHub repository](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples).</span><span class="sxs-lookup"><span data-stu-id="514cd-383">You can find more server-side code examples (including [bulk-delete](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/bulkDelete.js), and [update](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/update.js)) on our [GitHub repository](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples).</span></span>

<span data-ttu-id="514cd-384">Want to share your awesome stored procedure?</span><span class="sxs-lookup"><span data-stu-id="514cd-384">Want to share your awesome stored procedure?</span></span> <span data-ttu-id="514cd-385">Please, send us a pull-request!</span><span class="sxs-lookup"><span data-stu-id="514cd-385">Please, send us a pull-request!</span></span> 

## <a name="next-steps"></a><span data-ttu-id="514cd-386">Next steps</span><span class="sxs-lookup"><span data-stu-id="514cd-386">Next steps</span></span>
<span data-ttu-id="514cd-387">Once you have one or more stored procedures, triggers, and user-defined functions created, you can load them and view them in the Azure Portal using Script Explorer.</span><span class="sxs-lookup"><span data-stu-id="514cd-387">Once you have one or more stored procedures, triggers, and user-defined functions created, you can load them and view them in the Azure Portal using Script Explorer.</span></span> <span data-ttu-id="514cd-388">For more information, see [View stored procedures, triggers, and user-defined functions using the DocumentDB Script Explorer](documentdb-view-scripts.md).</span><span class="sxs-lookup"><span data-stu-id="514cd-388">For more information, see [View stored procedures, triggers, and user-defined functions using the DocumentDB Script Explorer](documentdb-view-scripts.md).</span></span>

<span data-ttu-id="514cd-389">You may also find the following references and resources useful in your path to learn more about DocumentDB server-side programming:</span><span class="sxs-lookup"><span data-stu-id="514cd-389">You may also find the following references and resources useful in your path to learn more about DocumentDB server-side programming:</span></span>

* [<span data-ttu-id="514cd-390">Azure DocumentDB SDKs</span><span class="sxs-lookup"><span data-stu-id="514cd-390">Azure DocumentDB SDKs</span></span>](https://msdn.microsoft.com/library/azure/dn781482.aspx)
* [<span data-ttu-id="514cd-391">DocumentDB Studio</span><span class="sxs-lookup"><span data-stu-id="514cd-391">DocumentDB Studio</span></span>](https://github.com/mingaliu/DocumentDBStudio/releases)
* [<span data-ttu-id="514cd-392">JSON</span><span class="sxs-lookup"><span data-stu-id="514cd-392">JSON</span></span>](http://www.json.org/) 
* [<span data-ttu-id="514cd-393">JavaScript ECMA-262</span><span class="sxs-lookup"><span data-stu-id="514cd-393">JavaScript ECMA-262</span></span>](http://www.ecma-international.org/publications/standards/Ecma-262.htm)
* [<span data-ttu-id="514cd-394">JavaScript – JSON type system</span><span class="sxs-lookup"><span data-stu-id="514cd-394">JavaScript – JSON type system</span></span>](http://www.json.org/js.html) 
* [<span data-ttu-id="514cd-395">Secure and Portable Database Extensibility</span><span class="sxs-lookup"><span data-stu-id="514cd-395">Secure and Portable Database Extensibility</span></span>](http://dl.acm.org/citation.cfm?id=276339) 
* [<span data-ttu-id="514cd-396">Service Oriented Database Architecture</span><span class="sxs-lookup"><span data-stu-id="514cd-396">Service Oriented Database Architecture</span></span>](http://dl.acm.org/citation.cfm?id=1066267&coll=Portal&dl=GUIDE) 
* [<span data-ttu-id="514cd-397">Hosting the .NET Runtime in Microsoft SQL server</span><span class="sxs-lookup"><span data-stu-id="514cd-397">Hosting the .NET Runtime in Microsoft SQL server</span></span>](http://dl.acm.org/citation.cfm?id=1007669)

