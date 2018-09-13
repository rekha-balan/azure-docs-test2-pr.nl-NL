---
title: NoSQL Node.js tutorial for DocumentDB | Microsoft Docs
description: A NoSQL Node.js tutorial that creates a NoSQL database and console application using the DocumentDB Node.js SDK. DocumentDB is a NoSQL database for JSON.
keywords: node.js tutorial, node database
services: documentdb
documentationcenter: node.js
author: AndrewHoh
manager: jhubbard
editor: monicar
ms.assetid: 14d52110-1dce-4ac0-9dd9-f936afccd550
ms.service: documentdb
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: node
ms.topic: hero-article
ms.date: 12/25/2016
ms.author: anhoh
ms.openlocfilehash: 6eb0606f7ce93d8a31d3fdc127a40357d64fd5f6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564519"
---
# <a name="nosql-nodejs-tutorial-documentdb-nodejs-console-application"></a><span data-ttu-id="8854f-105">NoSQL Node.js tutorial: DocumentDB Node.js console application</span><span class="sxs-lookup"><span data-stu-id="8854f-105">NoSQL Node.js tutorial: DocumentDB Node.js console application</span></span>
> [!div class="op_single_selector"]
> * [.NET](documentdb-get-started.md)
> * [.NET Core](documentdb-dotnetcore-get-started.md)
> * [Node.js for MongoDB](documentdb-mongodb-samples.md)
> * [Node.js](documentdb-nodejs-get-started.md)
> * [Java](documentdb-java-get-started.md)
> * [C++](documentdb-cpp-get-started.md)
>  
> 

<span data-ttu-id="8854f-112">Welcome to the Node.js tutorial for the Azure DocumentDB Node.js SDK!</span><span class="sxs-lookup"><span data-stu-id="8854f-112">Welcome to the Node.js tutorial for the Azure DocumentDB Node.js SDK!</span></span> <span data-ttu-id="8854f-113">After following this tutorial, you'll have a console application that creates and queries DocumentDB resources.</span><span class="sxs-lookup"><span data-stu-id="8854f-113">After following this tutorial, you'll have a console application that creates and queries DocumentDB resources.</span></span>

<span data-ttu-id="8854f-114">We'll cover:</span><span class="sxs-lookup"><span data-stu-id="8854f-114">We'll cover:</span></span>

* <span data-ttu-id="8854f-115">Creating and connecting to a DocumentDB account</span><span class="sxs-lookup"><span data-stu-id="8854f-115">Creating and connecting to a DocumentDB account</span></span>
* <span data-ttu-id="8854f-116">Setting up your application</span><span class="sxs-lookup"><span data-stu-id="8854f-116">Setting up your application</span></span>
* <span data-ttu-id="8854f-117">Creating a node database</span><span class="sxs-lookup"><span data-stu-id="8854f-117">Creating a node database</span></span>
* <span data-ttu-id="8854f-118">Creating a collection</span><span class="sxs-lookup"><span data-stu-id="8854f-118">Creating a collection</span></span>
* <span data-ttu-id="8854f-119">Creating JSON documents</span><span class="sxs-lookup"><span data-stu-id="8854f-119">Creating JSON documents</span></span>
* <span data-ttu-id="8854f-120">Querying the collection</span><span class="sxs-lookup"><span data-stu-id="8854f-120">Querying the collection</span></span>
* <span data-ttu-id="8854f-121">Replacing a document</span><span class="sxs-lookup"><span data-stu-id="8854f-121">Replacing a document</span></span>
* <span data-ttu-id="8854f-122">Deleting a document</span><span class="sxs-lookup"><span data-stu-id="8854f-122">Deleting a document</span></span>
* <span data-ttu-id="8854f-123">Deleting the node database</span><span class="sxs-lookup"><span data-stu-id="8854f-123">Deleting the node database</span></span>

<span data-ttu-id="8854f-124">Don't have time?</span><span class="sxs-lookup"><span data-stu-id="8854f-124">Don't have time?</span></span> <span data-ttu-id="8854f-125">Don't worry!</span><span class="sxs-lookup"><span data-stu-id="8854f-125">Don't worry!</span></span> <span data-ttu-id="8854f-126">The complete solution is available on [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started).</span><span class="sxs-lookup"><span data-stu-id="8854f-126">The complete solution is available on [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started).</span></span> <span data-ttu-id="8854f-127">See [Get the complete solution](#GetSolution) for quick instructions.</span><span class="sxs-lookup"><span data-stu-id="8854f-127">See [Get the complete solution](#GetSolution) for quick instructions.</span></span>

<span data-ttu-id="8854f-128">After you've completed the Node.js tutorial, please use the voting buttons at the top and bottom of this page to give us feedback.</span><span class="sxs-lookup"><span data-stu-id="8854f-128">After you've completed the Node.js tutorial, please use the voting buttons at the top and bottom of this page to give us feedback.</span></span> <span data-ttu-id="8854f-129">If you'd like us to contact you directly, feel free to include your email address in your comments.</span><span class="sxs-lookup"><span data-stu-id="8854f-129">If you'd like us to contact you directly, feel free to include your email address in your comments.</span></span>

<span data-ttu-id="8854f-130">Now let's get started!</span><span class="sxs-lookup"><span data-stu-id="8854f-130">Now let's get started!</span></span>

## <a name="prerequisites-for-the-nodejs-tutorial"></a><span data-ttu-id="8854f-131">Prerequisites for the Node.js tutorial</span><span class="sxs-lookup"><span data-stu-id="8854f-131">Prerequisites for the Node.js tutorial</span></span>
<span data-ttu-id="8854f-132">Please make sure you have the following:</span><span class="sxs-lookup"><span data-stu-id="8854f-132">Please make sure you have the following:</span></span>

* <span data-ttu-id="8854f-133">An active Azure account.</span><span class="sxs-lookup"><span data-stu-id="8854f-133">An active Azure account.</span></span> <span data-ttu-id="8854f-134">If you don't have one, you can sign up for a [Free Azure Trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8854f-134">If you don't have one, you can sign up for a [Free Azure Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
    * <span data-ttu-id="8854f-135">Alternatively, you can use the [Azure DocumentDB Emulator](documentdb-nosql-local-emulator.md) for this tutorial.</span><span class="sxs-lookup"><span data-stu-id="8854f-135">Alternatively, you can use the [Azure DocumentDB Emulator](documentdb-nosql-local-emulator.md) for this tutorial.</span></span>
* <span data-ttu-id="8854f-136">[Node.js](https://nodejs.org/) version v0.10.29 or higher.</span><span class="sxs-lookup"><span data-stu-id="8854f-136">[Node.js](https://nodejs.org/) version v0.10.29 or higher.</span></span>

## <a name="step-1-create-a-documentdb-account"></a><span data-ttu-id="8854f-137">Step 1: Create a DocumentDB account</span><span class="sxs-lookup"><span data-stu-id="8854f-137">Step 1: Create a DocumentDB account</span></span>
<span data-ttu-id="8854f-138">Let's create a DocumentDB account.</span><span class="sxs-lookup"><span data-stu-id="8854f-138">Let's create a DocumentDB account.</span></span> <span data-ttu-id="8854f-139">If you already have an account you want to use, you can skip ahead to [Setup your Node.js application](#SetupNode).</span><span class="sxs-lookup"><span data-stu-id="8854f-139">If you already have an account you want to use, you can skip ahead to [Setup your Node.js application](#SetupNode).</span></span> <span data-ttu-id="8854f-140">If you are using the DocumentDB Emulator, please follow the steps at [Azure DocumentDB Emulator](documentdb-nosql-local-emulator.md) to setup the emulator and skip ahead to [Setup your Node.js application](#SetupNode).</span><span class="sxs-lookup"><span data-stu-id="8854f-140">If you are using the DocumentDB Emulator, please follow the steps at [Azure DocumentDB Emulator](documentdb-nosql-local-emulator.md) to setup the emulator and skip ahead to [Setup your Node.js application](#SetupNode).</span></span>

[!INCLUDE [documentdb-create-dbaccount](../../includes/documentdb-create-dbaccount.md)]

## <a id="SetupNode"></a><span data-ttu-id="8854f-141">Step 2: Setup your Node.js application</span><span class="sxs-lookup"><span data-stu-id="8854f-141">Step 2: Setup your Node.js application</span></span>
1. <span data-ttu-id="8854f-142">Open your favorite terminal.</span><span class="sxs-lookup"><span data-stu-id="8854f-142">Open your favorite terminal.</span></span>
2. <span data-ttu-id="8854f-143">Locate the folder or directory where you'd like to save your Node.js application.</span><span class="sxs-lookup"><span data-stu-id="8854f-143">Locate the folder or directory where you'd like to save your Node.js application.</span></span>
3. <span data-ttu-id="8854f-144">Create two empty JavaScript files with the following commands:</span><span class="sxs-lookup"><span data-stu-id="8854f-144">Create two empty JavaScript files with the following commands:</span></span>
   * <span data-ttu-id="8854f-145">Windows:</span><span class="sxs-lookup"><span data-stu-id="8854f-145">Windows:</span></span>
     * ```fsutil file createnew app.js 0```
     * ```fsutil file createnew config.js 0```
   * <span data-ttu-id="8854f-146">Linux/OS X:</span><span class="sxs-lookup"><span data-stu-id="8854f-146">Linux/OS X:</span></span>
     * ```touch app.js```
     * ```touch config.js```
4. <span data-ttu-id="8854f-147">Install the documentdb module via npm.</span><span class="sxs-lookup"><span data-stu-id="8854f-147">Install the documentdb module via npm.</span></span> <span data-ttu-id="8854f-148">Use the following command:</span><span class="sxs-lookup"><span data-stu-id="8854f-148">Use the following command:</span></span>
   * ```npm install documentdb --save```

<span data-ttu-id="8854f-149">Great!</span><span class="sxs-lookup"><span data-stu-id="8854f-149">Great!</span></span> <span data-ttu-id="8854f-150">Now that you've finished setting up, let's start writing some code.</span><span class="sxs-lookup"><span data-stu-id="8854f-150">Now that you've finished setting up, let's start writing some code.</span></span>

## <a id="Config"></a><span data-ttu-id="8854f-151">Step 3: Set your app's configurations</span><span class="sxs-lookup"><span data-stu-id="8854f-151">Step 3: Set your app's configurations</span></span>
<span data-ttu-id="8854f-152">Open ```config.js``` in your favorite text editor.</span><span class="sxs-lookup"><span data-stu-id="8854f-152">Open ```config.js``` in your favorite text editor.</span></span>

<span data-ttu-id="8854f-153">Then, copy and paste the code snippet below and set properties ```config.endpoint``` and ```config.primaryKey``` to your DocumentDB endpoint uri and primary key.</span><span class="sxs-lookup"><span data-stu-id="8854f-153">Then, copy and paste the code snippet below and set properties ```config.endpoint``` and ```config.primaryKey``` to your DocumentDB endpoint uri and primary key.</span></span> <span data-ttu-id="8854f-154">Both these configurations can be found in the [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8854f-154">Both these configurations can be found in the [Azure Portal](https://portal.azure.com).</span></span>

![Node.js tutorial - Screen shot of the Azure Portal, showing a DocumentDB account, with the ACTIVE hub highlighted, the KEYS button highlighted on the DocumentDB account blade, and the URI, PRIMARY KEY and SECONDARY KEY values highlighted on the Keys blade - Node database][keys]

    // ADD THIS PART TO YOUR CODE
    var config = {}

    config.endpoint = "~your DocumentDB endpoint uri here~";
    config.primaryKey = "~your primary key here~";

<span data-ttu-id="8854f-156">Copy and paste the ```database id```, ```collection id```, and ```JSON documents``` to your ```config``` object below where you set your ```config.endpoint``` and ```config.authKey``` properties.</span><span class="sxs-lookup"><span data-stu-id="8854f-156">Copy and paste the ```database id```, ```collection id```, and ```JSON documents``` to your ```config``` object below where you set your ```config.endpoint``` and ```config.authKey``` properties.</span></span> <span data-ttu-id="8854f-157">If you already have data you'd like to store in your database, you can use DocumentDB's [Data Migration tool](documentdb-import-data.md) rather than adding the document definitions.</span><span class="sxs-lookup"><span data-stu-id="8854f-157">If you already have data you'd like to store in your database, you can use DocumentDB's [Data Migration tool](documentdb-import-data.md) rather than adding the document definitions.</span></span>

    config.endpoint = "~your DocumentDB endpoint uri here~";
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


<span data-ttu-id="8854f-158">The database, collection, and document definitions will act as your DocumentDB ```database id```, ```collection id```, and documents' data.</span><span class="sxs-lookup"><span data-stu-id="8854f-158">The database, collection, and document definitions will act as your DocumentDB ```database id```, ```collection id```, and documents' data.</span></span>

<span data-ttu-id="8854f-159">Finally, export your ```config``` object, so that you can reference it within the ```app.js``` file.</span><span class="sxs-lookup"><span data-stu-id="8854f-159">Finally, export your ```config``` object, so that you can reference it within the ```app.js``` file.</span></span>

            },
            "isRegistered": false
        }
    };

    // ADD THIS PART TO YOUR CODE
    module.exports = config;

## <a id="Connect"></a> <span data-ttu-id="8854f-160">Step 4: Connect to a DocumentDB account</span><span class="sxs-lookup"><span data-stu-id="8854f-160">Step 4: Connect to a DocumentDB account</span></span>
<span data-ttu-id="8854f-161">Open your empty ```app.js``` file in the text editor.</span><span class="sxs-lookup"><span data-stu-id="8854f-161">Open your empty ```app.js``` file in the text editor.</span></span> <span data-ttu-id="8854f-162">Copy and paste the code below to import the ```documentdb``` module and your newly created ```config``` module.</span><span class="sxs-lookup"><span data-stu-id="8854f-162">Copy and paste the code below to import the ```documentdb``` module and your newly created ```config``` module.</span></span>

    // ADD THIS PART TO YOUR CODE
    "use strict";

    var documentClient = require("documentdb").DocumentClient;
    var config = require("./config");
    var url = require('url');

<span data-ttu-id="8854f-163">Copy and paste the code to use the previously saved ```config.endpoint``` and ```config.primaryKey``` to create a new DocumentClient.</span><span class="sxs-lookup"><span data-stu-id="8854f-163">Copy and paste the code to use the previously saved ```config.endpoint``` and ```config.primaryKey``` to create a new DocumentClient.</span></span>

    var config = require("./config");
    var url = require('url');

    // ADD THIS PART TO YOUR CODE
    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });

<span data-ttu-id="8854f-164">Now that you have the code to initialize the documentdb client, let's take a look at working with DocumentDB resources.</span><span class="sxs-lookup"><span data-stu-id="8854f-164">Now that you have the code to initialize the documentdb client, let's take a look at working with DocumentDB resources.</span></span>

## <a name="step-5-create-a-node-database"></a><span data-ttu-id="8854f-165">Step 5: Create a Node database</span><span class="sxs-lookup"><span data-stu-id="8854f-165">Step 5: Create a Node database</span></span>
<span data-ttu-id="8854f-166">Copy and paste the code below to set the HTTP status for Not Found, the database url, and the collection url.</span><span class="sxs-lookup"><span data-stu-id="8854f-166">Copy and paste the code below to set the HTTP status for Not Found, the database url, and the collection url.</span></span> <span data-ttu-id="8854f-167">These urls are how the DocumentDB client will find the right database and collection.</span><span class="sxs-lookup"><span data-stu-id="8854f-167">These urls are how the DocumentDB client will find the right database and collection.</span></span>

    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });

    // ADD THIS PART TO YOUR CODE
    var HttpStatusCodes = { NOTFOUND: 404 };
    var databaseUrl = `dbs/${config.database.id}`;
    var collectionUrl = `${databaseUrl}/colls/${config.collection.id}`;

<span data-ttu-id="8854f-168">A [database](documentdb-resources.md#databases) can be created by using the [createDatabase](https://azure.github.io/azure-documentdb-node/DocumentClient.html) function of the **DocumentClient** class.</span><span class="sxs-lookup"><span data-stu-id="8854f-168">A [database](documentdb-resources.md#databases) can be created by using the [createDatabase](https://azure.github.io/azure-documentdb-node/DocumentClient.html) function of the **DocumentClient** class.</span></span> <span data-ttu-id="8854f-169">A database is the logical container of document storage partitioned across collections.</span><span class="sxs-lookup"><span data-stu-id="8854f-169">A database is the logical container of document storage partitioned across collections.</span></span>

<span data-ttu-id="8854f-170">Copy and paste the **getDatabase** function for creating your new database in the app.js file with the ```id``` specified in the ```config``` object.</span><span class="sxs-lookup"><span data-stu-id="8854f-170">Copy and paste the **getDatabase** function for creating your new database in the app.js file with the ```id``` specified in the ```config``` object.</span></span> <span data-ttu-id="8854f-171">The function will check if the database with the same ```FamilyRegistry``` id does not already exist.</span><span class="sxs-lookup"><span data-stu-id="8854f-171">The function will check if the database with the same ```FamilyRegistry``` id does not already exist.</span></span> <span data-ttu-id="8854f-172">If it does exist, we'll return that database instead of creating a new one.</span><span class="sxs-lookup"><span data-stu-id="8854f-172">If it does exist, we'll return that database instead of creating a new one.</span></span>

    var collectionUrl = `${databaseUrl}/colls/${config.collection.id}`;

    // ADD THIS PART TO YOUR CODE
    function getDatabase() {
        console.log(`Getting database:\n${config.database.id}\n`);

        return new Promise((resolve, reject) => {
            client.readDatabase(databaseUrl, (err, result) => {
                if (err) {
                    if (err.code == HttpStatusCodes.NOTFOUND) {
                        client.createDatabase(config.database, (err, created) => {
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
    }

<span data-ttu-id="8854f-173">Copy and paste the code below where you set the **getDatabase** function to add the helper function **exit** that will print the exit message and the call to **getDatabase** function.</span><span class="sxs-lookup"><span data-stu-id="8854f-173">Copy and paste the code below where you set the **getDatabase** function to add the helper function **exit** that will print the exit message and the call to **getDatabase** function.</span></span>

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
    }

    getDatabase()
    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="8854f-174">In your terminal, locate your ```app.js``` file and run the command: ```node app.js```</span><span class="sxs-lookup"><span data-stu-id="8854f-174">In your terminal, locate your ```app.js``` file and run the command: ```node app.js```</span></span>

<span data-ttu-id="8854f-175">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="8854f-175">Congratulations!</span></span> <span data-ttu-id="8854f-176">You have successfully created a DocumentDB database.</span><span class="sxs-lookup"><span data-stu-id="8854f-176">You have successfully created a DocumentDB database.</span></span>

## <a id="CreateColl"></a><span data-ttu-id="8854f-177">Step 6: Create a collection</span><span class="sxs-lookup"><span data-stu-id="8854f-177">Step 6: Create a collection</span></span>
> [!WARNING]
> **CreateDocumentCollectionAsync** will create a new collection, which has pricing implications. For more details, please visit our [pricing page](https://azure.microsoft.com/pricing/details/documentdb/).
> 
> 

<span data-ttu-id="8854f-180">A [collection](documentdb-resources.md#collections) can be created by using the [createCollection](https://azure.github.io/azure-documentdb-node/DocumentClient.html) function of the **DocumentClient** class.</span><span class="sxs-lookup"><span data-stu-id="8854f-180">A [collection](documentdb-resources.md#collections) can be created by using the [createCollection](https://azure.github.io/azure-documentdb-node/DocumentClient.html) function of the **DocumentClient** class.</span></span> <span data-ttu-id="8854f-181">A collection is a container of JSON documents and associated JavaScript application logic.</span><span class="sxs-lookup"><span data-stu-id="8854f-181">A collection is a container of JSON documents and associated JavaScript application logic.</span></span>

<span data-ttu-id="8854f-182">Copy and paste the **getCollection** function underneath the **getDatabase** function in the app.js file to create your new collection with the ```id``` specified in the ```config``` object.</span><span class="sxs-lookup"><span data-stu-id="8854f-182">Copy and paste the **getCollection** function underneath the **getDatabase** function in the app.js file to create your new collection with the ```id``` specified in the ```config``` object.</span></span> <span data-ttu-id="8854f-183">Again, we'll check to make sure a collection with the same ```FamilyCollection``` id does not already exist.</span><span class="sxs-lookup"><span data-stu-id="8854f-183">Again, we'll check to make sure a collection with the same ```FamilyCollection``` id does not already exist.</span></span> <span data-ttu-id="8854f-184">If it does exist, we'll return that collection instead of creating a new one.</span><span class="sxs-lookup"><span data-stu-id="8854f-184">If it does exist, we'll return that collection instead of creating a new one.</span></span>

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART TO YOUR CODE
    function getCollection() {
        console.log(`Getting collection:\n${config.collection.id}\n`);

        return new Promise((resolve, reject) => {
            client.readCollection(collectionUrl, (err, result) => {
                if (err) {
                    if (err.code == HttpStatusCodes.NOTFOUND) {
                        client.createCollection(databaseUrl, config.collection, { offerThroughput: 400 }, (err, created) => {
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
    }

<span data-ttu-id="8854f-185">Copy and paste the code below the call to **getDatabase** to execute the **getCollection** function.</span><span class="sxs-lookup"><span data-stu-id="8854f-185">Copy and paste the code below the call to **getDatabase** to execute the **getCollection** function.</span></span>

    getDatabase()

    // ADD THIS PART TO YOUR CODE
    .then(() => getCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="8854f-186">In your terminal, locate your ```app.js``` file and run the command: ```node app.js```</span><span class="sxs-lookup"><span data-stu-id="8854f-186">In your terminal, locate your ```app.js``` file and run the command: ```node app.js```</span></span>

<span data-ttu-id="8854f-187">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="8854f-187">Congratulations!</span></span> <span data-ttu-id="8854f-188">You have successfully created a DocumentDB collection.</span><span class="sxs-lookup"><span data-stu-id="8854f-188">You have successfully created a DocumentDB collection.</span></span>

## <a id="CreateDoc"></a><span data-ttu-id="8854f-189">Step 7: Create a document</span><span class="sxs-lookup"><span data-stu-id="8854f-189">Step 7: Create a document</span></span>
<span data-ttu-id="8854f-190">A [document](documentdb-resources.md#documents) can be created by using the [createDocument](https://azure.github.io/azure-documentdb-node/DocumentClient.html) function of the **DocumentClient** class.</span><span class="sxs-lookup"><span data-stu-id="8854f-190">A [document](documentdb-resources.md#documents) can be created by using the [createDocument](https://azure.github.io/azure-documentdb-node/DocumentClient.html) function of the **DocumentClient** class.</span></span> <span data-ttu-id="8854f-191">Documents are user defined (arbitrary) JSON content.</span><span class="sxs-lookup"><span data-stu-id="8854f-191">Documents are user defined (arbitrary) JSON content.</span></span> <span data-ttu-id="8854f-192">You can now insert a document into DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="8854f-192">You can now insert a document into DocumentDB.</span></span>

<span data-ttu-id="8854f-193">Copy and paste the **getFamilyDocument** function underneath the **getCollection** function for creating the documents containing the JSON data saved in the ```config``` object.</span><span class="sxs-lookup"><span data-stu-id="8854f-193">Copy and paste the **getFamilyDocument** function underneath the **getCollection** function for creating the documents containing the JSON data saved in the ```config``` object.</span></span> <span data-ttu-id="8854f-194">Again, we'll check to make sure a document with the same id does not already exist.</span><span class="sxs-lookup"><span data-stu-id="8854f-194">Again, we'll check to make sure a document with the same id does not already exist.</span></span>

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART TO YOUR CODE
    function getFamilyDocument(document) {
        let documentUrl = `${collectionUrl}/docs/${document.id}`;
        console.log(`Getting document:\n${document.id}\n`);

        return new Promise((resolve, reject) => {
            client.readDocument(documentUrl, { partitionKey: document.district }, (err, result) => {
                if (err) {
                    if (err.code == HttpStatusCodes.NOTFOUND) {
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

<span data-ttu-id="8854f-195">Copy and paste the code below the call to **getCollection** to execute the **getFamilyDocument** function.</span><span class="sxs-lookup"><span data-stu-id="8854f-195">Copy and paste the code below the call to **getCollection** to execute the **getFamilyDocument** function.</span></span>

    getDatabase()
    .then(() => getCollection())

    // ADD THIS PART TO YOUR CODE
    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="8854f-196">In your terminal, locate your ```app.js``` file and run the command: ```node app.js```</span><span class="sxs-lookup"><span data-stu-id="8854f-196">In your terminal, locate your ```app.js``` file and run the command: ```node app.js```</span></span>

<span data-ttu-id="8854f-197">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="8854f-197">Congratulations!</span></span> <span data-ttu-id="8854f-198">You have successfully created a DocumentDB documents.</span><span class="sxs-lookup"><span data-stu-id="8854f-198">You have successfully created a DocumentDB documents.</span></span>

![Node.js tutorial - Diagram illustrating the hierarchical relationship between the account, the database, the collection, and the documents - Node database](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-nodejs-get-started/node-js-tutorial-account-database.png)

## <a id="Query"></a><span data-ttu-id="8854f-200">Step 8: Query DocumentDB resources</span><span class="sxs-lookup"><span data-stu-id="8854f-200">Step 8: Query DocumentDB resources</span></span>
<span data-ttu-id="8854f-201">DocumentDB supports [rich queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span><span class="sxs-lookup"><span data-stu-id="8854f-201">DocumentDB supports [rich queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span> <span data-ttu-id="8854f-202">The following sample code shows a query that you can run against the documents in your collection.</span><span class="sxs-lookup"><span data-stu-id="8854f-202">The following sample code shows a query that you can run against the documents in your collection.</span></span>

<span data-ttu-id="8854f-203">Copy and paste the **queryCollection** function underneath the **getFamilyDocument** function in the app.js file.</span><span class="sxs-lookup"><span data-stu-id="8854f-203">Copy and paste the **queryCollection** function underneath the **getFamilyDocument** function in the app.js file.</span></span> <span data-ttu-id="8854f-204">DocumentDB supports SQL-like queries as shown below.</span><span class="sxs-lookup"><span data-stu-id="8854f-204">DocumentDB supports SQL-like queries as shown below.</span></span> <span data-ttu-id="8854f-205">For more information on building complex queries, check out the [Query Playground](https://www.documentdb.com/sql/demo) and the [query documentation](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="8854f-205">For more information on building complex queries, check out the [Query Playground](https://www.documentdb.com/sql/demo) and the [query documentation](documentdb-sql-query.md).</span></span>

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART TO YOUR CODE
    function queryCollection() {
        console.log(`Querying collection through index:\n${config.collection.id}`);

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


<span data-ttu-id="8854f-206">The following diagram illustrates how the DocumentDB SQL query syntax is called against the collection you created.</span><span class="sxs-lookup"><span data-stu-id="8854f-206">The following diagram illustrates how the DocumentDB SQL query syntax is called against the collection you created.</span></span>

![Node.js tutorial - Diagram illustrating the scope and meaning of the query - Node database](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-nodejs-get-started/node-js-tutorial-collection-documents.png)

<span data-ttu-id="8854f-208">The [FROM](documentdb-sql-query.md#FromClause) keyword is optional in the query because DocumentDB queries are already scoped to a single collection.</span><span class="sxs-lookup"><span data-stu-id="8854f-208">The [FROM](documentdb-sql-query.md#FromClause) keyword is optional in the query because DocumentDB queries are already scoped to a single collection.</span></span> <span data-ttu-id="8854f-209">Therefore, "FROM Families f" can be swapped with "FROM root r", or any other variable name you choose.</span><span class="sxs-lookup"><span data-stu-id="8854f-209">Therefore, "FROM Families f" can be swapped with "FROM root r", or any other variable name you choose.</span></span> <span data-ttu-id="8854f-210">DocumentDB will infer that Families, root, or the variable name you chose, reference the current collection by default.</span><span class="sxs-lookup"><span data-stu-id="8854f-210">DocumentDB will infer that Families, root, or the variable name you chose, reference the current collection by default.</span></span>

<span data-ttu-id="8854f-211">Copy and paste the code below the call to **getFamilyDocument** to execute the **queryCollection** function.</span><span class="sxs-lookup"><span data-stu-id="8854f-211">Copy and paste the code below the call to **getFamilyDocument** to execute the **queryCollection** function.</span></span>

    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))

    // ADD THIS PART TO YOUR CODE
    .then(() => queryCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="8854f-212">In your terminal, locate your ```app.js``` file and run the command: ```node app.js```</span><span class="sxs-lookup"><span data-stu-id="8854f-212">In your terminal, locate your ```app.js``` file and run the command: ```node app.js```</span></span>

<span data-ttu-id="8854f-213">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="8854f-213">Congratulations!</span></span> <span data-ttu-id="8854f-214">You have successfully queried DocumentDB documents.</span><span class="sxs-lookup"><span data-stu-id="8854f-214">You have successfully queried DocumentDB documents.</span></span>

## <a id="ReplaceDocument"></a><span data-ttu-id="8854f-215">Step 9: Replace a document</span><span class="sxs-lookup"><span data-stu-id="8854f-215">Step 9: Replace a document</span></span>
<span data-ttu-id="8854f-216">DocumentDB supports replacing JSON documents.</span><span class="sxs-lookup"><span data-stu-id="8854f-216">DocumentDB supports replacing JSON documents.</span></span>

<span data-ttu-id="8854f-217">Copy and paste the **replaceFamilyDocument** function underneath the **queryCollection** function in the app.js file.</span><span class="sxs-lookup"><span data-stu-id="8854f-217">Copy and paste the **replaceFamilyDocument** function underneath the **queryCollection** function in the app.js file.</span></span>

                    }
                    console.log();
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART TO YOUR CODE
    function replaceFamilyDocument(document) {
        let documentUrl = `${collectionUrl}/docs/${document.id}`;
        console.log(`Replacing document:\n${document.id}\n`);
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

<span data-ttu-id="8854f-218">Copy and paste the code below the call to **queryCollection** to execute the **replaceDocument** function.</span><span class="sxs-lookup"><span data-stu-id="8854f-218">Copy and paste the code below the call to **queryCollection** to execute the **replaceDocument** function.</span></span> <span data-ttu-id="8854f-219">Also, add the code to call **queryCollection** again to verify that the document had successfully changed.</span><span class="sxs-lookup"><span data-stu-id="8854f-219">Also, add the code to call **queryCollection** again to verify that the document had successfully changed.</span></span>

    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))
    .then(() => queryCollection())

    // ADD THIS PART TO YOUR CODE
    .then(() => replaceFamilyDocument(config.documents.Andersen))
    .then(() => queryCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="8854f-220">In your terminal, locate your ```app.js``` file and run the command: ```node app.js```</span><span class="sxs-lookup"><span data-stu-id="8854f-220">In your terminal, locate your ```app.js``` file and run the command: ```node app.js```</span></span>

<span data-ttu-id="8854f-221">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="8854f-221">Congratulations!</span></span> <span data-ttu-id="8854f-222">You have successfully replaced a DocumentDB document.</span><span class="sxs-lookup"><span data-stu-id="8854f-222">You have successfully replaced a DocumentDB document.</span></span>

## <a id="DeleteDocument"></a><span data-ttu-id="8854f-223">Step 10: Delete a document</span><span class="sxs-lookup"><span data-stu-id="8854f-223">Step 10: Delete a document</span></span>
<span data-ttu-id="8854f-224">DocumentDB supports deleting JSON documents.</span><span class="sxs-lookup"><span data-stu-id="8854f-224">DocumentDB supports deleting JSON documents.</span></span>

<span data-ttu-id="8854f-225">Copy and paste the **deleteFamilyDocument** function underneath the **replaceFamilyDocument** function.</span><span class="sxs-lookup"><span data-stu-id="8854f-225">Copy and paste the **deleteFamilyDocument** function underneath the **replaceFamilyDocument** function.</span></span>

                else {
                    resolve(result);
                }
            });
        });
    };

    // ADD THIS PART TO YOUR CODE
    function deleteFamilyDocument(document) {
        let documentUrl = `${collectionUrl}/docs/${document.id}`;
        console.log(`Deleting document:\n${document.id}\n`);

        return new Promise((resolve, reject) => {
            client.deleteDocument(documentUrl, (err, result) => {
                if (err) reject(err);
                else {
                    resolve(result);
                }
            });
        });
    };

<span data-ttu-id="8854f-226">Copy and paste the code below the call to the second **queryCollection** to execute the **deleteDocument** function.</span><span class="sxs-lookup"><span data-stu-id="8854f-226">Copy and paste the code below the call to the second **queryCollection** to execute the **deleteDocument** function.</span></span>

    .then(() => queryCollection())
    .then(() => replaceFamilyDocument(config.documents.Andersen))
    .then(() => queryCollection())

    // ADD THIS PART TO YOUR CODE
    .then(() => deleteFamilyDocument(config.documents.Andersen))
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="8854f-227">In your terminal, locate your ```app.js``` file and run the command: ```node app.js```</span><span class="sxs-lookup"><span data-stu-id="8854f-227">In your terminal, locate your ```app.js``` file and run the command: ```node app.js```</span></span>

<span data-ttu-id="8854f-228">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="8854f-228">Congratulations!</span></span> <span data-ttu-id="8854f-229">You have successfully deleted a DocumentDB document.</span><span class="sxs-lookup"><span data-stu-id="8854f-229">You have successfully deleted a DocumentDB document.</span></span>

## <a id="DeleteDatabase"></a><span data-ttu-id="8854f-230">Step 11: Delete the Node database</span><span class="sxs-lookup"><span data-stu-id="8854f-230">Step 11: Delete the Node database</span></span>
<span data-ttu-id="8854f-231">Deleting the created database will remove the database and all children resources (collections, documents, etc.).</span><span class="sxs-lookup"><span data-stu-id="8854f-231">Deleting the created database will remove the database and all children resources (collections, documents, etc.).</span></span>

<span data-ttu-id="8854f-232">Copy and paste the **cleanup** function underneath the **deleteFamilyDocument** function to remove the database and all the children resources.</span><span class="sxs-lookup"><span data-stu-id="8854f-232">Copy and paste the **cleanup** function underneath the **deleteFamilyDocument** function to remove the database and all the children resources.</span></span>

                else {
                    resolve(result);
                }
            });
        });
    };

    // ADD THIS PART TO YOUR CODE
    function cleanup() {
        console.log(`Cleaning up by deleting database ${config.database.id}`);

        return new Promise((resolve, reject) => {
            client.deleteDatabase(databaseUrl, (err) => {
                if (err) reject(err)
                else resolve(null);
            });
        });
    }

<span data-ttu-id="8854f-233">Copy and paste the code below the call to **deleteFamilyDocument** to execute the **cleanup** function.</span><span class="sxs-lookup"><span data-stu-id="8854f-233">Copy and paste the code below the call to **deleteFamilyDocument** to execute the **cleanup** function.</span></span>

    .then(() => deleteFamilyDocument(config.documents.Andersen))

    // ADD THIS PART TO YOUR CODE
    .then(() => cleanup())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

## <a id="Run"></a><span data-ttu-id="8854f-234">Step 12: Run your Node.js application all together!</span><span class="sxs-lookup"><span data-stu-id="8854f-234">Step 12: Run your Node.js application all together!</span></span>
<span data-ttu-id="8854f-235">Altogether, the sequence for calling your functions should look like this:</span><span class="sxs-lookup"><span data-stu-id="8854f-235">Altogether, the sequence for calling your functions should look like this:</span></span>

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

<span data-ttu-id="8854f-236">In your terminal, locate your ```app.js``` file and run the command: ```node app.js```</span><span class="sxs-lookup"><span data-stu-id="8854f-236">In your terminal, locate your ```app.js``` file and run the command: ```node app.js```</span></span>

<span data-ttu-id="8854f-237">You should see the output of your get started app.</span><span class="sxs-lookup"><span data-stu-id="8854f-237">You should see the output of your get started app.</span></span> <span data-ttu-id="8854f-238">The output should match the example text below.</span><span class="sxs-lookup"><span data-stu-id="8854f-238">The output should match the example text below.</span></span>

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

<span data-ttu-id="8854f-239">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="8854f-239">Congratulations!</span></span> <span data-ttu-id="8854f-240">You've created you've completed the Node.js tutorial and have your first DocumentDB console application!</span><span class="sxs-lookup"><span data-stu-id="8854f-240">You've created you've completed the Node.js tutorial and have your first DocumentDB console application!</span></span>

## <a id="GetSolution"></a><span data-ttu-id="8854f-241">Get the complete Node.js tutorial solution</span><span class="sxs-lookup"><span data-stu-id="8854f-241">Get the complete Node.js tutorial solution</span></span>
<span data-ttu-id="8854f-242">If you didn't have time to complete the steps in this tutorial, or just want to download the code, you can get it from [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started).</span><span class="sxs-lookup"><span data-stu-id="8854f-242">If you didn't have time to complete the steps in this tutorial, or just want to download the code, you can get it from [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started).</span></span>

<span data-ttu-id="8854f-243">To run the GetStarted solution that contains all the samples in this article, you will need the following:</span><span class="sxs-lookup"><span data-stu-id="8854f-243">To run the GetStarted solution that contains all the samples in this article, you will need the following:</span></span>

* <span data-ttu-id="8854f-244">[DocumentDB account][documentdb-create-account].</span><span class="sxs-lookup"><span data-stu-id="8854f-244">[DocumentDB account][documentdb-create-account].</span></span>
* <span data-ttu-id="8854f-245">The [GetStarted](https://github.com/Azure-Samples/documentdb-node-getting-started) solution available on GitHub.</span><span class="sxs-lookup"><span data-stu-id="8854f-245">The [GetStarted](https://github.com/Azure-Samples/documentdb-node-getting-started) solution available on GitHub.</span></span>

<span data-ttu-id="8854f-246">Install the **documentdb** module via npm.</span><span class="sxs-lookup"><span data-stu-id="8854f-246">Install the **documentdb** module via npm.</span></span> <span data-ttu-id="8854f-247">Use the following command:</span><span class="sxs-lookup"><span data-stu-id="8854f-247">Use the following command:</span></span>

* ```npm install documentdb --save```

<span data-ttu-id="8854f-248">Next, in the ```config.js``` file, update the config.endpoint and config.authKey values as described in [Step 3: Set your app's configurations](#Config).</span><span class="sxs-lookup"><span data-stu-id="8854f-248">Next, in the ```config.js``` file, update the config.endpoint and config.authKey values as described in [Step 3: Set your app's configurations](#Config).</span></span> 

<span data-ttu-id="8854f-249">Then in your terminal, locate your ```app.js``` file and run the command: ```node app.js```.</span><span class="sxs-lookup"><span data-stu-id="8854f-249">Then in your terminal, locate your ```app.js``` file and run the command: ```node app.js```.</span></span>

<span data-ttu-id="8854f-250">That's it, build it and you're on your way!</span><span class="sxs-lookup"><span data-stu-id="8854f-250">That's it, build it and you're on your way!</span></span> 

## <a name="next-steps"></a><span data-ttu-id="8854f-251">Next steps</span><span class="sxs-lookup"><span data-stu-id="8854f-251">Next steps</span></span>
* <span data-ttu-id="8854f-252">Want a more complex Node.js sample?</span><span class="sxs-lookup"><span data-stu-id="8854f-252">Want a more complex Node.js sample?</span></span> <span data-ttu-id="8854f-253">See [Build a Node.js web application using DocumentDB](documentdb-nodejs-application.md).</span><span class="sxs-lookup"><span data-stu-id="8854f-253">See [Build a Node.js web application using DocumentDB](documentdb-nodejs-application.md).</span></span>
* <span data-ttu-id="8854f-254">Learn how to [monitor a DocumentDB account](documentdb-monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="8854f-254">Learn how to [monitor a DocumentDB account](documentdb-monitor-accounts.md).</span></span>
* <span data-ttu-id="8854f-255">Run queries against our sample dataset in the [Query Playground](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="8854f-255">Run queries against our sample dataset in the [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="8854f-256">Learn more about the programming model in the Develop section of the [DocumentDB documentation page](https://azure.microsoft.com/documentation/services/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="8854f-256">Learn more about the programming model in the Develop section of the [DocumentDB documentation page](https://azure.microsoft.com/documentation/services/documentdb/).</span></span>

[documentdb-create-account]: documentdb-create-account.md
[keys]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-nodejs-get-started/node-js-tutorial-keys.png



