---
title: Node.js tutorial for the SQL API for Azure Cosmos DB | Microsoft Docs
description: A Node.js tutorial that creates a Cosmos DB with the SQL API.
keywords: node.js tutorial, node database
services: cosmos-db
author: SnehaGunda
manager: kfile
editor: monicar
ms.service: cosmos-db
ms.component: cosmosdb-sql
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 08/14/2017
ms.author: sngun
ms.openlocfilehash: 16225e666df59da654e993c4d0618a97288471ac
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865012"
---
# <a name="nodejs-tutorial-use-the-sql-api-in-azure-cosmos-db-to-create-a-nodejs-console-application"></a><span data-ttu-id="aa710-104">Node.js tutorial: Use the SQL API in Azure Cosmos DB to create a Node.js console application</span><span class="sxs-lookup"><span data-stu-id="aa710-104">Node.js tutorial: Use the SQL API in Azure Cosmos DB to create a Node.js console application</span></span>

> [!div class="op_single_selector"]
> * [.NET](sql-api-get-started.md)
> * [.NET Core](sql-api-dotnetcore-get-started.md)
> * [Java](sql-api-java-get-started.md)
> * [Async Java](sql-api-async-java-get-started.md)
> * [Node.js](sql-api-nodejs-get-started.md)
> * [Node.js- v2](sql-api-nodejs-get-started-preview.md) 
> 


<span data-ttu-id="aa710-111">Welcome to the Node.js tutorial for the Azure Cosmos DB Node.js SDK!</span><span class="sxs-lookup"><span data-stu-id="aa710-111">Welcome to the Node.js tutorial for the Azure Cosmos DB Node.js SDK!</span></span> <span data-ttu-id="aa710-112">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources.</span><span class="sxs-lookup"><span data-stu-id="aa710-112">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources.</span></span>

<span data-ttu-id="aa710-113">We'll cover:</span><span class="sxs-lookup"><span data-stu-id="aa710-113">We'll cover:</span></span>

* <span data-ttu-id="aa710-114">Creating and connecting to an Azure Cosmos DB account</span><span class="sxs-lookup"><span data-stu-id="aa710-114">Creating and connecting to an Azure Cosmos DB account</span></span>
* <span data-ttu-id="aa710-115">Setting up your application</span><span class="sxs-lookup"><span data-stu-id="aa710-115">Setting up your application</span></span>
* <span data-ttu-id="aa710-116">Creating a node database</span><span class="sxs-lookup"><span data-stu-id="aa710-116">Creating a node database</span></span>
* <span data-ttu-id="aa710-117">Creating a collection</span><span class="sxs-lookup"><span data-stu-id="aa710-117">Creating a collection</span></span>
* <span data-ttu-id="aa710-118">Creating JSON documents</span><span class="sxs-lookup"><span data-stu-id="aa710-118">Creating JSON documents</span></span>
* <span data-ttu-id="aa710-119">Querying the collection</span><span class="sxs-lookup"><span data-stu-id="aa710-119">Querying the collection</span></span>
* <span data-ttu-id="aa710-120">Replacing a document</span><span class="sxs-lookup"><span data-stu-id="aa710-120">Replacing a document</span></span>
* <span data-ttu-id="aa710-121">Deleting a document</span><span class="sxs-lookup"><span data-stu-id="aa710-121">Deleting a document</span></span>
* <span data-ttu-id="aa710-122">Deleting the node database</span><span class="sxs-lookup"><span data-stu-id="aa710-122">Deleting the node database</span></span>

<span data-ttu-id="aa710-123">Don't have time?</span><span class="sxs-lookup"><span data-stu-id="aa710-123">Don't have time?</span></span> <span data-ttu-id="aa710-124">Don't worry!</span><span class="sxs-lookup"><span data-stu-id="aa710-124">Don't worry!</span></span> <span data-ttu-id="aa710-125">The complete solution is available on [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started).</span><span class="sxs-lookup"><span data-stu-id="aa710-125">The complete solution is available on [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started).</span></span> <span data-ttu-id="aa710-126">See [Get the complete solution](#GetSolution) for quick instructions.</span><span class="sxs-lookup"><span data-stu-id="aa710-126">See [Get the complete solution](#GetSolution) for quick instructions.</span></span>

<span data-ttu-id="aa710-127">After you've completed the Node.js tutorial, please use the voting buttons at the top and bottom of this page to give us feedback.</span><span class="sxs-lookup"><span data-stu-id="aa710-127">After you've completed the Node.js tutorial, please use the voting buttons at the top and bottom of this page to give us feedback.</span></span> <span data-ttu-id="aa710-128">If you'd like us to contact you directly, feel free to include your email address in your comments.</span><span class="sxs-lookup"><span data-stu-id="aa710-128">If you'd like us to contact you directly, feel free to include your email address in your comments.</span></span>

<span data-ttu-id="aa710-129">Now let's get started!</span><span class="sxs-lookup"><span data-stu-id="aa710-129">Now let's get started!</span></span>

## <a name="prerequisites-for-the-nodejs-tutorial"></a><span data-ttu-id="aa710-130">Prerequisites for the Node.js tutorial</span><span class="sxs-lookup"><span data-stu-id="aa710-130">Prerequisites for the Node.js tutorial</span></span>

<span data-ttu-id="aa710-131">Please make sure you have the following:</span><span class="sxs-lookup"><span data-stu-id="aa710-131">Please make sure you have the following:</span></span>

* <span data-ttu-id="aa710-132">An active Azure account.</span><span class="sxs-lookup"><span data-stu-id="aa710-132">An active Azure account.</span></span> <span data-ttu-id="aa710-133">If you don't have one, you can sign up for a [Free Azure Trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="aa710-133">If you don't have one, you can sign up for a [Free Azure Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

  [!INCLUDE [cosmos-db-emulator-docdb-api](../../includes/cosmos-db-emulator-docdb-api.md)]

* <span data-ttu-id="aa710-134">[Node.js](https://nodejs.org/) version v0.10.29 or higher.</span><span class="sxs-lookup"><span data-stu-id="aa710-134">[Node.js](https://nodejs.org/) version v0.10.29 or higher.</span></span>

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="aa710-135">Step 1: Create an Azure Cosmos DB account</span><span class="sxs-lookup"><span data-stu-id="aa710-135">Step 1: Create an Azure Cosmos DB account</span></span>

<span data-ttu-id="aa710-136">Let's create an Azure Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="aa710-136">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="aa710-137">If you already have an account you want to use, you can skip ahead to [Set up your Node.js application](#SetupNode).</span><span class="sxs-lookup"><span data-stu-id="aa710-137">If you already have an account you want to use, you can skip ahead to [Set up your Node.js application](#SetupNode).</span></span> <span data-ttu-id="aa710-138">If you are using the Azure Cosmos DB Emulator, please follow the steps at [Azure Cosmos DB Emulator](local-emulator.md) to setup the emulator and skip ahead to [Set up your Node.js application](#SetupNode).</span><span class="sxs-lookup"><span data-stu-id="aa710-138">If you are using the Azure Cosmos DB Emulator, please follow the steps at [Azure Cosmos DB Emulator](local-emulator.md) to setup the emulator and skip ahead to [Set up your Node.js application](#SetupNode).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a id="SetupNode"></a><span data-ttu-id="aa710-139">Step 2: Set up your Node.js application</span><span class="sxs-lookup"><span data-stu-id="aa710-139">Step 2: Set up your Node.js application</span></span>

1. <span data-ttu-id="aa710-140">Open your favorite terminal.</span><span class="sxs-lookup"><span data-stu-id="aa710-140">Open your favorite terminal.</span></span>
2. <span data-ttu-id="aa710-141">Locate the folder or directory where you'd like to save your Node.js application.</span><span class="sxs-lookup"><span data-stu-id="aa710-141">Locate the folder or directory where you'd like to save your Node.js application.</span></span>
3. <span data-ttu-id="aa710-142">Create two empty JavaScript files with the following commands:</span><span class="sxs-lookup"><span data-stu-id="aa710-142">Create two empty JavaScript files with the following commands:</span></span>
   * <span data-ttu-id="aa710-143">Windows:</span><span class="sxs-lookup"><span data-stu-id="aa710-143">Windows:</span></span>
     * ```fsutil file createnew app.js 0```
     * ```fsutil file createnew config.js 0```
   * <span data-ttu-id="aa710-144">Linux/OS X:</span><span class="sxs-lookup"><span data-stu-id="aa710-144">Linux/OS X:</span></span>
     * ```touch app.js```
     * ```touch config.js```
4. <span data-ttu-id="aa710-145">Install the documentdb module via npm.</span><span class="sxs-lookup"><span data-stu-id="aa710-145">Install the documentdb module via npm.</span></span> <span data-ttu-id="aa710-146">Use the following command:</span><span class="sxs-lookup"><span data-stu-id="aa710-146">Use the following command:</span></span>
   * ```npm install documentdb --save```

<span data-ttu-id="aa710-147">Great!</span><span class="sxs-lookup"><span data-stu-id="aa710-147">Great!</span></span> <span data-ttu-id="aa710-148">Now that you've finished setting up, let's start writing some code.</span><span class="sxs-lookup"><span data-stu-id="aa710-148">Now that you've finished setting up, let's start writing some code.</span></span>

## <a id="Config"></a><span data-ttu-id="aa710-149">Step 3: Set your app's configurations</span><span class="sxs-lookup"><span data-stu-id="aa710-149">Step 3: Set your app's configurations</span></span>

<span data-ttu-id="aa710-150">Open ```config.js``` in your favorite text editor.</span><span class="sxs-lookup"><span data-stu-id="aa710-150">Open ```config.js``` in your favorite text editor.</span></span>

<span data-ttu-id="aa710-151">Then, copy and paste the code snippet below and set properties ```config.endpoint``` and ```config.primaryKey``` to your Azure Cosmos DB endpoint uri and primary key.</span><span class="sxs-lookup"><span data-stu-id="aa710-151">Then, copy and paste the code snippet below and set properties ```config.endpoint``` and ```config.primaryKey``` to your Azure Cosmos DB endpoint uri and primary key.</span></span> <span data-ttu-id="aa710-152">Both these configurations can be found in the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="aa710-152">Both these configurations can be found in the [Azure portal](https://portal.azure.com).</span></span>

![Node.js tutorial - Screen shot of the Azure portal, showing an Azure Cosmos DB account, with the ACTIVE hub highlighted, the KEYS button highlighted on the Azure Cosmos DB account blade, and the URI, PRIMARY KEY and SECONDARY KEY values highlighted on the Keys blade - Node database][keys]

    // ADD THIS PART TO YOUR CODE
    var config = {}

    config.endpoint = "~your Azure Cosmos DB endpoint uri here~";
    config.primaryKey = "~your primary key here~";

<span data-ttu-id="aa710-154">Copy and paste the ```database id```, ```collection id```, and ```JSON documents``` to your ```config``` object below where you set your ```config.endpoint``` and ```config.primaryKey``` properties.</span><span class="sxs-lookup"><span data-stu-id="aa710-154">Copy and paste the ```database id```, ```collection id```, and ```JSON documents``` to your ```config``` object below where you set your ```config.endpoint``` and ```config.primaryKey``` properties.</span></span> <span data-ttu-id="aa710-155">If you already have data you'd like to store in your database, you can use Azure Cosmos DB's [Data Migration tool](import-data.md) rather than adding the document definitions.</span><span class="sxs-lookup"><span data-stu-id="aa710-155">If you already have data you'd like to store in your database, you can use Azure Cosmos DB's [Data Migration tool](import-data.md) rather than adding the document definitions.</span></span>

    config.endpoint = "~your Azure Cosmos DB endpoint uri here~";
    config.primaryKey = "~your primary key here~";

    // ADD THIS PART TO YOUR CODE
    config.database = {
        "id": "FamilyDB"
    };

    config.collection = {
        "id": "FamilyColl"
    };

    config.documents = {
        "Andersen": {
            "id": "Anderson.1",
            "lastName": "Andersen",
            "parents": [{
                "firstName": "Thomas"
            }, {
                    "firstName": "Mary Kay"
                }],
            "children": [{
                "firstName": "Henriette Thaulow",
                "gender": "female",
                "grade": 5,
                "pets": [{
                    "givenName": "Fluffy"
                }]
            }],
            "address": {
                "state": "WA",
                "county": "King",
                "city": "Seattle"
            }
        },
        "Wakefield": {
            "id": "Wakefield.7",
            "parents": [{
                "familyName": "Wakefield",
                "firstName": "Robin"
            }, {
                    "familyName": "Miller",
                    "firstName": "Ben"
                }],
            "children": [{
                "familyName": "Merriam",
                "firstName": "Jesse",
                "gender": "female",
                "grade": 8,
                "pets": [{
                    "givenName": "Goofy"
                }, {
                        "givenName": "Shadow"
                    }]
            }, {
                    "familyName": "Miller",
                    "firstName": "Lisa",
                    "gender": "female",
                    "grade": 1
                }],
            "address": {
                "state": "NY",
                "county": "Manhattan",
                "city": "NY"
            },
            "isRegistered": false
        }
    };

<span data-ttu-id="aa710-156">The database, collection, and document definitions will act as your Azure Cosmos DB ```database id```, ```collection id```, and documents' data.</span><span class="sxs-lookup"><span data-stu-id="aa710-156">The database, collection, and document definitions will act as your Azure Cosmos DB ```database id```, ```collection id```, and documents' data.</span></span>

<span data-ttu-id="aa710-157">Finally, export your ```config``` object, so that you can reference it within the ```app.js``` file.</span><span class="sxs-lookup"><span data-stu-id="aa710-157">Finally, export your ```config``` object, so that you can reference it within the ```app.js``` file.</span></span>

            },
            "isRegistered": false
        }
    };

    // ADD THIS PART TO YOUR CODE
    module.exports = config;

## <a id="Connect"></a> <span data-ttu-id="aa710-158">Step 4: Connect to an Azure Cosmos DB account</span><span class="sxs-lookup"><span data-stu-id="aa710-158">Step 4: Connect to an Azure Cosmos DB account</span></span>

<span data-ttu-id="aa710-159">Open your empty ```app.js``` file in the text editor.</span><span class="sxs-lookup"><span data-stu-id="aa710-159">Open your empty ```app.js``` file in the text editor.</span></span> <span data-ttu-id="aa710-160">Copy and paste the code below to import the ```documentdb``` module and your newly created ```config``` module.</span><span class="sxs-lookup"><span data-stu-id="aa710-160">Copy and paste the code below to import the ```documentdb``` module and your newly created ```config``` module.</span></span>

    // ADD THIS PART TO YOUR CODE
    "use strict";

    var documentClient = require("documentdb").DocumentClient;
    const uriFactory = require('documentdb').UriFactory;
    var config = require("./config");

<span data-ttu-id="aa710-161">Copy and paste the code to use the previously saved ```config.endpoint``` and ```config.primaryKey``` to create a new DocumentClient.</span><span class="sxs-lookup"><span data-stu-id="aa710-161">Copy and paste the code to use the previously saved ```config.endpoint``` and ```config.primaryKey``` to create a new DocumentClient.</span></span>

    var config = require("./config");

    // ADD THIS PART TO YOUR CODE
    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });

<span data-ttu-id="aa710-162">Now that you have the code to initialize the Azure Cosmos DB client, let's take a look at working with Azure Cosmos DB resources.</span><span class="sxs-lookup"><span data-stu-id="aa710-162">Now that you have the code to initialize the Azure Cosmos DB client, let's take a look at working with Azure Cosmos DB resources.</span></span>

## <a name="step-5-create-a-node-database"></a><span data-ttu-id="aa710-163">Step 5: Create a Node database</span><span class="sxs-lookup"><span data-stu-id="aa710-163">Step 5: Create a Node database</span></span>

<span data-ttu-id="aa710-164">Copy and paste the code below to set the HTTP status for Not Found, the database id, and the collection id. These ids are how the Azure Cosmos DB client will find the right database and collection.</span><span class="sxs-lookup"><span data-stu-id="aa710-164">Copy and paste the code below to set the HTTP status for Not Found, the database id, and the collection id. These ids are how the Azure Cosmos DB client will find the right database and collection.</span></span>

    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });

    // ADD THIS PART TO YOUR CODE
    var HttpStatusCodes = { NOTFOUND: 404 };
    var databaseId = config.database.id;
    var collectionId = config.collection.id;

<span data-ttu-id="aa710-165">A [database](sql-api-resources.md#databases) can be created by using the [createDatabase](/javascript/api/documentdb/documentclient) function of the **DocumentClient** class.</span><span class="sxs-lookup"><span data-stu-id="aa710-165">A [database](sql-api-resources.md#databases) can be created by using the [createDatabase](/javascript/api/documentdb/documentclient) function of the **DocumentClient** class.</span></span> <span data-ttu-id="aa710-166">A database is the logical container of document storage partitioned across collections.</span><span class="sxs-lookup"><span data-stu-id="aa710-166">A database is the logical container of document storage partitioned across collections.</span></span>

<span data-ttu-id="aa710-167">Copy and paste the **getDatabase** function for creating your new database in the app.js file with the ```databaseId``` specified from the ```config``` object.</span><span class="sxs-lookup"><span data-stu-id="aa710-167">Copy and paste the **getDatabase** function for creating your new database in the app.js file with the ```databaseId``` specified from the ```config``` object.</span></span> <span data-ttu-id="aa710-168">The function will check if the database with the same ```FamilyRegistry``` id does not already exist.</span><span class="sxs-lookup"><span data-stu-id="aa710-168">The function will check if the database with the same ```FamilyRegistry``` id does not already exist.</span></span> <span data-ttu-id="aa710-169">If it does exist, we'll return that database instead of creating a new one.</span><span class="sxs-lookup"><span data-stu-id="aa710-169">If it does exist, we'll return that database instead of creating a new one.</span></span>

    // ADD THIS PART TO YOUR CODE
    function getDatabase() {
        console.log(`Getting database:\n${databaseId}\n`);
        let databaseUrl = uriFactory.createDatabaseUri(databaseId);
        return new Promise((resolve, reject) => {
            client.readDatabase(databaseUrl, (err, result) => {
                if (err) {
                    if (err.code == HttpStatusCodes.NOTFOUND) {
                        client.createDatabase({ id: databaseId }, (err, created) => {
                            if (err) reject(err)
                            else resolve(created);
                        });
                    } else {
                        reject(err);
                    }
                } else {
                    resolve(result);
                }
            });
        });
    };

<span data-ttu-id="aa710-170">Copy and paste the code below where you set the **getDatabase** function to add the helper function **exit** that will print the exit message and the call to **getDatabase** function.</span><span class="sxs-lookup"><span data-stu-id="aa710-170">Copy and paste the code below where you set the **getDatabase** function to add the helper function **exit** that will print the exit message and the call to **getDatabase** function.</span></span>

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART TO YOUR CODE
    function exit(message) {
        console.log(message);
        console.log('Press any key to exit');
        process.stdin.setRawMode(true);
        process.stdin.resume();
        process.stdin.on('data', process.exit.bind(process, 0));
    };

    getDatabase()
    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="aa710-171">In your terminal, locate your ```app.js``` file and run the command: ```node app.js```</span><span class="sxs-lookup"><span data-stu-id="aa710-171">In your terminal, locate your ```app.js``` file and run the command: ```node app.js```</span></span>

<span data-ttu-id="aa710-172">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="aa710-172">Congratulations!</span></span> <span data-ttu-id="aa710-173">You have successfully created an Azure Cosmos DB database.</span><span class="sxs-lookup"><span data-stu-id="aa710-173">You have successfully created an Azure Cosmos DB database.</span></span>

## <a id="CreateColl"></a><span data-ttu-id="aa710-174">Step 6: Create a collection</span><span class="sxs-lookup"><span data-stu-id="aa710-174">Step 6: Create a collection</span></span>

> [!WARNING]
> **createCollection** will create a new collection, which has pricing implications. For more details, please visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).

<span data-ttu-id="aa710-177">A [collection](sql-api-resources.md#collections) can be created by using the [createCollection](/javascript/api/documentdb/documentclient) function of the **DocumentClient** class.</span><span class="sxs-lookup"><span data-stu-id="aa710-177">A [collection](sql-api-resources.md#collections) can be created by using the [createCollection](/javascript/api/documentdb/documentclient) function of the **DocumentClient** class.</span></span> <span data-ttu-id="aa710-178">A collection is a container of JSON documents and associated JavaScript application logic.</span><span class="sxs-lookup"><span data-stu-id="aa710-178">A collection is a container of JSON documents and associated JavaScript application logic.</span></span>

<span data-ttu-id="aa710-179">Copy and paste the **getCollection** function underneath the **getDatabase** function in the app.js file to create your new collection with the ```collectionId``` specified from the ```config``` object.</span><span class="sxs-lookup"><span data-stu-id="aa710-179">Copy and paste the **getCollection** function underneath the **getDatabase** function in the app.js file to create your new collection with the ```collectionId``` specified from the ```config``` object.</span></span> <span data-ttu-id="aa710-180">Again, we'll check to make sure a collection with the same ```FamilyCollection``` id does not already exist.</span><span class="sxs-lookup"><span data-stu-id="aa710-180">Again, we'll check to make sure a collection with the same ```FamilyCollection``` id does not already exist.</span></span> <span data-ttu-id="aa710-181">If it does exist, we'll return that collection instead of creating a new one.</span><span class="sxs-lookup"><span data-stu-id="aa710-181">If it does exist, we'll return that collection instead of creating a new one.</span></span>

                } else {
                    resolve(result);
                }
            });
        });
    };

    // ADD THIS PART TO YOUR CODE
    function getCollection() {
        console.log(`Getting collection:\n${collectionId}\n`);
        let collectionUrl = uriFactory.createDocumentCollectionUri(databaseId, collectionId);
        return new Promise((resolve, reject) => {
            client.readCollection(collectionUrl, (err, result) => {
                if (err) {
                    if (err.code == HttpStatusCodes.NOTFOUND) {
                        let databaseUrl = uriFactory.createDatabaseUri(databaseId);
                        client.createCollection(databaseUrl, { id: collectionId }, { offerThroughput: 400 }, (err, created) => {
                            if (err) reject(err)
                            else resolve(created);
                        });
                    } else {
                        reject(err);
                    }
                } else {
                    resolve(result);
                }
            });
        });
    };

<span data-ttu-id="aa710-182">Copy and paste the code below the call to **getDatabase** to execute the **getCollection** function.</span><span class="sxs-lookup"><span data-stu-id="aa710-182">Copy and paste the code below the call to **getDatabase** to execute the **getCollection** function.</span></span>

    getDatabase()

    // ADD THIS PART TO YOUR CODE
    .then(() => getCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="aa710-183">In your terminal, locate your ```app.js``` file and run the command: ```node app.js```</span><span class="sxs-lookup"><span data-stu-id="aa710-183">In your terminal, locate your ```app.js``` file and run the command: ```node app.js```</span></span>

<span data-ttu-id="aa710-184">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="aa710-184">Congratulations!</span></span> <span data-ttu-id="aa710-185">You have successfully created an Azure Cosmos DB collection.</span><span class="sxs-lookup"><span data-stu-id="aa710-185">You have successfully created an Azure Cosmos DB collection.</span></span>

## <a id="CreateDoc"></a><span data-ttu-id="aa710-186">Step 7: Create a document</span><span class="sxs-lookup"><span data-stu-id="aa710-186">Step 7: Create a document</span></span>

<span data-ttu-id="aa710-187">A [document](sql-api-resources.md#documents) can be created by using the [createDocument](/javascript/api/documentdb/documentclient) function of the **DocumentClient** class.</span><span class="sxs-lookup"><span data-stu-id="aa710-187">A [document](sql-api-resources.md#documents) can be created by using the [createDocument](/javascript/api/documentdb/documentclient) function of the **DocumentClient** class.</span></span> <span data-ttu-id="aa710-188">Documents are user defined (arbitrary) JSON content.</span><span class="sxs-lookup"><span data-stu-id="aa710-188">Documents are user defined (arbitrary) JSON content.</span></span> <span data-ttu-id="aa710-189">You can now insert a document into Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="aa710-189">You can now insert a document into Azure Cosmos DB.</span></span>

<span data-ttu-id="aa710-190">Copy and paste the **getFamilyDocument** function underneath the **getCollection** function for creating the documents containing the JSON data saved in the ```config``` object.</span><span class="sxs-lookup"><span data-stu-id="aa710-190">Copy and paste the **getFamilyDocument** function underneath the **getCollection** function for creating the documents containing the JSON data saved in the ```config``` object.</span></span> <span data-ttu-id="aa710-191">Again, we'll check to make sure a document with the same id does not already exist.</span><span class="sxs-lookup"><span data-stu-id="aa710-191">Again, we'll check to make sure a document with the same id does not already exist.</span></span>

                } else {
                    resolve(result);
                }
            });
        });
    };

    // ADD THIS PART TO YOUR CODE
    function getFamilyDocument(document) {
        console.log(`Getting document:\n${document.id}\n`);
        let documentUrl = uriFactory.createDocumentUri(databaseId, collectionId, document.id);
        return new Promise((resolve, reject) => {
            client.readDocument(documentUrl, (err, result) => {
                if (err) {
                    if (err.code == HttpStatusCodes.NOTFOUND) {
                        let collectionUrl = uriFactory.createDocumentCollectionUri(databaseId, collectionId);
                        client.createDocument(collectionUrl, document, (err, created) => {
                            if (err) reject(err)
                            else resolve(created);
                        });
                    } else {
                        reject(err);
                    }
                } else {
                    resolve(result);
                }
            });
        });
    };

<span data-ttu-id="aa710-192">Copy and paste the code below the call to **getCollection** to execute the **getFamilyDocument** function.</span><span class="sxs-lookup"><span data-stu-id="aa710-192">Copy and paste the code below the call to **getCollection** to execute the **getFamilyDocument** function.</span></span>

    getDatabase()
    .then(() => getCollection())

    // ADD THIS PART TO YOUR CODE
    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="aa710-193">In your terminal, locate your ```app.js``` file and run the command: ```node app.js```</span><span class="sxs-lookup"><span data-stu-id="aa710-193">In your terminal, locate your ```app.js``` file and run the command: ```node app.js```</span></span>

<span data-ttu-id="aa710-194">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="aa710-194">Congratulations!</span></span> <span data-ttu-id="aa710-195">You have successfully created an Azure Cosmos DB document.</span><span class="sxs-lookup"><span data-stu-id="aa710-195">You have successfully created an Azure Cosmos DB document.</span></span>

![Node.js tutorial - Diagram illustrating the hierarchical relationship between the account, the database, the collection, and the documents - Node database](./media/sql-api-nodejs-get-started/node-js-tutorial-cosmos-db-account.png)

## <a id="Query"></a><span data-ttu-id="aa710-197">Step 8: Query Azure Cosmos DB resources</span><span class="sxs-lookup"><span data-stu-id="aa710-197">Step 8: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="aa710-198">Azure Cosmos DB supports [rich queries](sql-api-sql-query.md) against JSON documents stored in each collection.</span><span class="sxs-lookup"><span data-stu-id="aa710-198">Azure Cosmos DB supports [rich queries](sql-api-sql-query.md) against JSON documents stored in each collection.</span></span> <span data-ttu-id="aa710-199">The following sample code shows a query that you can run against the documents in your collection.</span><span class="sxs-lookup"><span data-stu-id="aa710-199">The following sample code shows a query that you can run against the documents in your collection.</span></span>

<span data-ttu-id="aa710-200">Copy and paste the **queryCollection** function underneath the **getFamilyDocument** function in the app.js file.</span><span class="sxs-lookup"><span data-stu-id="aa710-200">Copy and paste the **queryCollection** function underneath the **getFamilyDocument** function in the app.js file.</span></span> <span data-ttu-id="aa710-201">Azure Cosmos DB supports SQL-like queries as shown below.</span><span class="sxs-lookup"><span data-stu-id="aa710-201">Azure Cosmos DB supports SQL-like queries as shown below.</span></span> <span data-ttu-id="aa710-202">For more information on building complex queries, check out the [Query Playground](https://www.documentdb.com/sql/demo) and the [query documentation](sql-api-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="aa710-202">For more information on building complex queries, check out the [Query Playground](https://www.documentdb.com/sql/demo) and the [query documentation](sql-api-sql-query.md).</span></span>

                } else {
                    resolve(result);
                }
            });
        });
    };

    // ADD THIS PART TO YOUR CODE
    function queryCollection() {
        console.log(`Querying collection through index:\n${collectionId}`);
        let collectionUrl = uriFactory.createDocumentCollectionUri(databaseId, collectionId);
        return new Promise((resolve, reject) => {
            client.queryDocuments(
                collectionUrl,
                'SELECT VALUE r.children FROM root r WHERE r.lastName = "Andersen"'
            ).toArray((err, results) => {
                if (err) reject(err)
                else {
                    for (var queryResult of results) {
                        let resultString = JSON.stringify(queryResult);
                        console.log(`\tQuery returned ${resultString}`);
                    }
                    console.log();
                    resolve(results);
                }
            });
        });
    };

<span data-ttu-id="aa710-203">The following diagram illustrates how the Azure Cosmos DB SQL query syntax is called against the collection you created.</span><span class="sxs-lookup"><span data-stu-id="aa710-203">The following diagram illustrates how the Azure Cosmos DB SQL query syntax is called against the collection you created.</span></span>

![Node.js tutorial - Diagram illustrating the scope and meaning of the query - Node database](./media/sql-api-nodejs-get-started/node-js-tutorial-collection-documents.png)

<span data-ttu-id="aa710-205">The [FROM](sql-api-sql-query.md#FromClause) keyword is optional in the query because Azure Cosmos DB queries are already scoped to a single collection.</span><span class="sxs-lookup"><span data-stu-id="aa710-205">The [FROM](sql-api-sql-query.md#FromClause) keyword is optional in the query because Azure Cosmos DB queries are already scoped to a single collection.</span></span> <span data-ttu-id="aa710-206">Therefore, "FROM Families f" can be swapped with "FROM root r", or any other variable name you choose.</span><span class="sxs-lookup"><span data-stu-id="aa710-206">Therefore, "FROM Families f" can be swapped with "FROM root r", or any other variable name you choose.</span></span> <span data-ttu-id="aa710-207">Azure Cosmos DB will infer that Families, root, or the variable name you chose, reference the current collection by default.</span><span class="sxs-lookup"><span data-stu-id="aa710-207">Azure Cosmos DB will infer that Families, root, or the variable name you chose, reference the current collection by default.</span></span>

<span data-ttu-id="aa710-208">Copy and paste the code below the call to **getFamilyDocument** to execute the **queryCollection** function.</span><span class="sxs-lookup"><span data-stu-id="aa710-208">Copy and paste the code below the call to **getFamilyDocument** to execute the **queryCollection** function.</span></span>

    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))

    // ADD THIS PART TO YOUR CODE
    .then(() => queryCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="aa710-209">In your terminal, locate your ```app.js``` file and run the command: ```node app.js```</span><span class="sxs-lookup"><span data-stu-id="aa710-209">In your terminal, locate your ```app.js``` file and run the command: ```node app.js```</span></span>

<span data-ttu-id="aa710-210">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="aa710-210">Congratulations!</span></span> <span data-ttu-id="aa710-211">You have successfully queried Azure Cosmos DB documents.</span><span class="sxs-lookup"><span data-stu-id="aa710-211">You have successfully queried Azure Cosmos DB documents.</span></span>

## <a id="ReplaceDocument"></a><span data-ttu-id="aa710-212">Step 9: Replace a document</span><span class="sxs-lookup"><span data-stu-id="aa710-212">Step 9: Replace a document</span></span>
<span data-ttu-id="aa710-213">Azure Cosmos DB supports replacing JSON documents.</span><span class="sxs-lookup"><span data-stu-id="aa710-213">Azure Cosmos DB supports replacing JSON documents.</span></span>

<span data-ttu-id="aa710-214">Copy and paste the **replaceFamilyDocument** function underneath the **queryCollection** function in the app.js file.</span><span class="sxs-lookup"><span data-stu-id="aa710-214">Copy and paste the **replaceFamilyDocument** function underneath the **queryCollection** function in the app.js file.</span></span>

                    }
                    console.log();
                    resolve(result);
                }
            });
        });
    };

    // ADD THIS PART TO YOUR CODE
    function replaceFamilyDocument(document) {
        console.log(`Replacing document:\n${document.id}\n`);
        let documentUrl = uriFactory.createDocumentUri(databaseId, collectionId, document.id);
        document.children[0].grade = 6;
        return new Promise((resolve, reject) => {
            client.replaceDocument(documentUrl, document, (err, result) => {
                if (err) reject(err);
                else {
                    resolve(result);
                }
            });
        });
    };

<span data-ttu-id="aa710-215">Copy and paste the code below the call to **queryCollection** to execute the **replaceDocument** function.</span><span class="sxs-lookup"><span data-stu-id="aa710-215">Copy and paste the code below the call to **queryCollection** to execute the **replaceDocument** function.</span></span> <span data-ttu-id="aa710-216">Also, add the code to call **queryCollection** again to verify that the document had successfully changed.</span><span class="sxs-lookup"><span data-stu-id="aa710-216">Also, add the code to call **queryCollection** again to verify that the document had successfully changed.</span></span>

    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))
    .then(() => queryCollection())

    // ADD THIS PART TO YOUR CODE
    .then(() => replaceFamilyDocument(config.documents.Andersen))
    .then(() => queryCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="aa710-217">In your terminal, locate your ```app.js``` file and run the command: ```node app.js```</span><span class="sxs-lookup"><span data-stu-id="aa710-217">In your terminal, locate your ```app.js``` file and run the command: ```node app.js```</span></span>

<span data-ttu-id="aa710-218">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="aa710-218">Congratulations!</span></span> <span data-ttu-id="aa710-219">You have successfully replaced an Azure Cosmos DB document.</span><span class="sxs-lookup"><span data-stu-id="aa710-219">You have successfully replaced an Azure Cosmos DB document.</span></span>

## <a id="DeleteDocument"></a><span data-ttu-id="aa710-220">Step 10: Delete a document</span><span class="sxs-lookup"><span data-stu-id="aa710-220">Step 10: Delete a document</span></span>

<span data-ttu-id="aa710-221">Azure Cosmos DB supports deleting JSON documents.</span><span class="sxs-lookup"><span data-stu-id="aa710-221">Azure Cosmos DB supports deleting JSON documents.</span></span>

<span data-ttu-id="aa710-222">Copy and paste the **deleteFamilyDocument** function underneath the **replaceFamilyDocument** function.</span><span class="sxs-lookup"><span data-stu-id="aa710-222">Copy and paste the **deleteFamilyDocument** function underneath the **replaceFamilyDocument** function.</span></span>

                else {
                    resolve(result);
                }
            });
        });
    };

    // ADD THIS PART TO YOUR CODE
    function deleteFamilyDocument(document) {
        console.log(`Deleting document:\n${document.id}\n`);
        let documentUrl = uriFactory.createDocumentUri(databaseId, collectionId, document.id);
        return new Promise((resolve, reject) => {
            client.deleteDocument(documentUrl, (err, result) => {
                if (err) reject(err);
                else {
                    resolve(result);
                }
            });
        });
    };

<span data-ttu-id="aa710-223">Copy and paste the code below the call to the second **queryCollection** to execute the **deleteDocument** function.</span><span class="sxs-lookup"><span data-stu-id="aa710-223">Copy and paste the code below the call to the second **queryCollection** to execute the **deleteDocument** function.</span></span>

    .then(() => queryCollection())
    .then(() => replaceFamilyDocument(config.documents.Andersen))
    .then(() => queryCollection())

    // ADD THIS PART TO YOUR CODE
    .then(() => deleteFamilyDocument(config.documents.Andersen))
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="aa710-224">In your terminal, locate your ```app.js``` file and run the command: ```node app.js```</span><span class="sxs-lookup"><span data-stu-id="aa710-224">In your terminal, locate your ```app.js``` file and run the command: ```node app.js```</span></span>

<span data-ttu-id="aa710-225">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="aa710-225">Congratulations!</span></span> <span data-ttu-id="aa710-226">You have successfully deleted an Azure Cosmos DB document.</span><span class="sxs-lookup"><span data-stu-id="aa710-226">You have successfully deleted an Azure Cosmos DB document.</span></span>

## <a id="DeleteDatabase"></a><span data-ttu-id="aa710-227">Step 11: Delete the Node database</span><span class="sxs-lookup"><span data-stu-id="aa710-227">Step 11: Delete the Node database</span></span>

<span data-ttu-id="aa710-228">Deleting the created database will remove the database and all children resources (collections, documents, etc.).</span><span class="sxs-lookup"><span data-stu-id="aa710-228">Deleting the created database will remove the database and all children resources (collections, documents, etc.).</span></span>

<span data-ttu-id="aa710-229">Copy and paste the **cleanup** function underneath the **deleteFamilyDocument** function to remove the database and all the children resources.</span><span class="sxs-lookup"><span data-stu-id="aa710-229">Copy and paste the **cleanup** function underneath the **deleteFamilyDocument** function to remove the database and all the children resources.</span></span>

                else {
                    resolve(result);
                }
            });
        });
    };

    // ADD THIS PART TO YOUR CODE
    function cleanup() {
        console.log(`Cleaning up by deleting database ${databaseId}`);
        let databaseUrl = uriFactory.createDatabaseUri(databaseId);
        return new Promise((resolve, reject) => {
            client.deleteDatabase(databaseUrl, (err) => {
                if (err) reject(err)
                else resolve(null);
            });
        });
    };

<span data-ttu-id="aa710-230">Copy and paste the code below the call to **deleteFamilyDocument** to execute the **cleanup** function.</span><span class="sxs-lookup"><span data-stu-id="aa710-230">Copy and paste the code below the call to **deleteFamilyDocument** to execute the **cleanup** function.</span></span>

    .then(() => deleteFamilyDocument(config.documents.Andersen))

    // ADD THIS PART TO YOUR CODE
    .then(() => cleanup())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

## <a id="Run"></a><span data-ttu-id="aa710-231">Step 12: Run your Node.js application all together!</span><span class="sxs-lookup"><span data-stu-id="aa710-231">Step 12: Run your Node.js application all together!</span></span>

<span data-ttu-id="aa710-232">Altogether, the sequence for calling your functions should look like this:</span><span class="sxs-lookup"><span data-stu-id="aa710-232">Altogether, the sequence for calling your functions should look like this:</span></span>

    getDatabase()
    .then(() => getCollection())
    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))
    .then(() => queryCollection())
    .then(() => replaceFamilyDocument(config.documents.Andersen))
    .then(() => queryCollection())
    .then(() => deleteFamilyDocument(config.documents.Andersen))
    .then(() => cleanup())
    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="aa710-233">In your terminal, locate your ```app.js``` file and run the command: ```node app.js```</span><span class="sxs-lookup"><span data-stu-id="aa710-233">In your terminal, locate your ```app.js``` file and run the command: ```node app.js```</span></span>

<span data-ttu-id="aa710-234">You should see the output of your get started app.</span><span class="sxs-lookup"><span data-stu-id="aa710-234">You should see the output of your get started app.</span></span> <span data-ttu-id="aa710-235">The output should match the example text below.</span><span class="sxs-lookup"><span data-stu-id="aa710-235">The output should match the example text below.</span></span>

    Getting database:
    FamilyDB

    Getting collection:
    FamilyColl

    Getting document:
    Anderson.1

    Getting document:
    Wakefield.7

    Querying collection through index:
    FamilyColl
        Query returned [{"firstName":"Henriette Thaulow","gender":"female","grade":5,"pets":[{"givenName":"Fluffy"}]}]

    Replacing document:
    Anderson.1

    Querying collection through index:
    FamilyColl
        Query returned [{"firstName":"Henriette Thaulow","gender":"female","grade":6,"pets":[{"givenName":"Fluffy"}]}]

    Deleting document:
    Anderson.1

    Cleaning up by deleting database FamilyDB
    Completed successfully
    Press any key to exit

<span data-ttu-id="aa710-236">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="aa710-236">Congratulations!</span></span> <span data-ttu-id="aa710-237">You've created you've completed the Node.js tutorial and have your first Azure Cosmos DB console application!</span><span class="sxs-lookup"><span data-stu-id="aa710-237">You've created you've completed the Node.js tutorial and have your first Azure Cosmos DB console application!</span></span>

## <a id="GetSolution"></a><span data-ttu-id="aa710-238">Get the complete Node.js tutorial solution</span><span class="sxs-lookup"><span data-stu-id="aa710-238">Get the complete Node.js tutorial solution</span></span>

<span data-ttu-id="aa710-239">If you didn't have time to complete the steps in this tutorial, or just want to download the code, you can get it from [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started).</span><span class="sxs-lookup"><span data-stu-id="aa710-239">If you didn't have time to complete the steps in this tutorial, or just want to download the code, you can get it from [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started).</span></span>

<span data-ttu-id="aa710-240">To run the GetStarted solution that contains all the samples in this article, you will need the following:</span><span class="sxs-lookup"><span data-stu-id="aa710-240">To run the GetStarted solution that contains all the samples in this article, you will need the following:</span></span>

* <span data-ttu-id="aa710-241">[Azure Cosmos DB account][create-account].</span><span class="sxs-lookup"><span data-stu-id="aa710-241">[Azure Cosmos DB account][create-account].</span></span>
* <span data-ttu-id="aa710-242">The [GetStarted](https://github.com/Azure-Samples/documentdb-node-getting-started) solution available on GitHub.</span><span class="sxs-lookup"><span data-stu-id="aa710-242">The [GetStarted](https://github.com/Azure-Samples/documentdb-node-getting-started) solution available on GitHub.</span></span>

<span data-ttu-id="aa710-243">Install the **documentdb** module via npm.</span><span class="sxs-lookup"><span data-stu-id="aa710-243">Install the **documentdb** module via npm.</span></span> <span data-ttu-id="aa710-244">Use the following command:</span><span class="sxs-lookup"><span data-stu-id="aa710-244">Use the following command:</span></span>

* ```npm install documentdb --save```

<span data-ttu-id="aa710-245">Next, in the ```config.js``` file, update the config.endpoint and config.primaryKey values as described in [Step 3: Set your app's configurations](#Config).</span><span class="sxs-lookup"><span data-stu-id="aa710-245">Next, in the ```config.js``` file, update the config.endpoint and config.primaryKey values as described in [Step 3: Set your app's configurations](#Config).</span></span> 

<span data-ttu-id="aa710-246">Then in your terminal, locate your ```app.js``` file and run the command: ```node app.js```.</span><span class="sxs-lookup"><span data-stu-id="aa710-246">Then in your terminal, locate your ```app.js``` file and run the command: ```node app.js```.</span></span>

<span data-ttu-id="aa710-247">That's it, build it and you're on your way!</span><span class="sxs-lookup"><span data-stu-id="aa710-247">That's it, build it and you're on your way!</span></span> 

## <a name="next-steps"></a><span data-ttu-id="aa710-248">Next steps</span><span class="sxs-lookup"><span data-stu-id="aa710-248">Next steps</span></span>
* <span data-ttu-id="aa710-249">Want a more complex Node.js sample?</span><span class="sxs-lookup"><span data-stu-id="aa710-249">Want a more complex Node.js sample?</span></span> <span data-ttu-id="aa710-250">See [Build a Node.js web application using Azure Cosmos DB](sql-api-nodejs-application.md).</span><span class="sxs-lookup"><span data-stu-id="aa710-250">See [Build a Node.js web application using Azure Cosmos DB](sql-api-nodejs-application.md).</span></span>
* <span data-ttu-id="aa710-251">Learn how to [monitor an Azure Cosmos DB account](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="aa710-251">Learn how to [monitor an Azure Cosmos DB account](monitor-accounts.md).</span></span>
* <span data-ttu-id="aa710-252">Run queries against our sample dataset in the [Query Playground](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="aa710-252">Run queries against our sample dataset in the [Query Playground](https://www.documentdb.com/sql/demo).</span></span>

[create-account]: create-sql-api-dotnet.md#create-account
[keys]: media/sql-api-nodejs-get-started/node-js-tutorial-keys.png
