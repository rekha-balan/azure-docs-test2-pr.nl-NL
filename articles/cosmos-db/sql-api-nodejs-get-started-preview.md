---
title: Node.js tutorial for the SQL API for Azure Cosmos DB | Microsoft Docs
description: A Node.js tutorial that demonstrates how to connect to and query Azure Cosmos DB using the SQL API
keywords: node.js tutorial, node database
services: cosmos-db
author: deborahc
manager: kfile
editor: monicar
ms.service: cosmos-db
ms.component: cosmosdb-sql
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 07/30/2018
ms.author: dech
ms.openlocfilehash: 1657dc016198ea19832b146a1642511346f777dc
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966985"
---
# <a name="nodejs-tutorial-create-a-nodejs-console-application-with-azure-cosmos-db-sql-api-and-javascript-sdk-20-preview"></a><span data-ttu-id="9c591-104">Node.js tutorial: Create a Node.js console application with Azure Cosmos DB SQL API and JavaScript SDK 2.0 (preview)</span><span class="sxs-lookup"><span data-stu-id="9c591-104">Node.js tutorial: Create a Node.js console application with Azure Cosmos DB SQL API and JavaScript SDK 2.0 (preview)</span></span>

> [!div class="op_single_selector"]
> * [.NET](sql-api-get-started.md)
> * [.NET Core](sql-api-dotnetcore-get-started.md)
> * [Java](sql-api-java-get-started.md)
> * [Async Java](sql-api-async-java-get-started.md)
> * [Node.js](sql-api-nodejs-get-started.md)
> * [Node.js- v2](sql-api-nodejs-get-started-preview.md) 
> 


<span data-ttu-id="9c591-111">Welcome to the Node.js tutorial for the Azure Cosmos DB JavaScript SDK!</span><span class="sxs-lookup"><span data-stu-id="9c591-111">Welcome to the Node.js tutorial for the Azure Cosmos DB JavaScript SDK!</span></span> <span data-ttu-id="9c591-112">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources.</span><span class="sxs-lookup"><span data-stu-id="9c591-112">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources.</span></span>

<span data-ttu-id="9c591-113">We'll cover:</span><span class="sxs-lookup"><span data-stu-id="9c591-113">We'll cover:</span></span>

* <span data-ttu-id="9c591-114">Creating and connecting to an Azure Cosmos DB account</span><span class="sxs-lookup"><span data-stu-id="9c591-114">Creating and connecting to an Azure Cosmos DB account</span></span>
* <span data-ttu-id="9c591-115">Setting up your application</span><span class="sxs-lookup"><span data-stu-id="9c591-115">Setting up your application</span></span>
* <span data-ttu-id="9c591-116">Creating a database</span><span class="sxs-lookup"><span data-stu-id="9c591-116">Creating a database</span></span>
* <span data-ttu-id="9c591-117">Creating a container</span><span class="sxs-lookup"><span data-stu-id="9c591-117">Creating a container</span></span>
* <span data-ttu-id="9c591-118">Adding JSON items to the container</span><span class="sxs-lookup"><span data-stu-id="9c591-118">Adding JSON items to the container</span></span>
* <span data-ttu-id="9c591-119">Querying the container</span><span class="sxs-lookup"><span data-stu-id="9c591-119">Querying the container</span></span>
* <span data-ttu-id="9c591-120">Replacing an item</span><span class="sxs-lookup"><span data-stu-id="9c591-120">Replacing an item</span></span>
* <span data-ttu-id="9c591-121">Deleting an item</span><span class="sxs-lookup"><span data-stu-id="9c591-121">Deleting an item</span></span>
* <span data-ttu-id="9c591-122">Deleting the database</span><span class="sxs-lookup"><span data-stu-id="9c591-122">Deleting the database</span></span>

<span data-ttu-id="9c591-123">Don't have time?</span><span class="sxs-lookup"><span data-stu-id="9c591-123">Don't have time?</span></span> <span data-ttu-id="9c591-124">Don't worry!</span><span class="sxs-lookup"><span data-stu-id="9c591-124">Don't worry!</span></span> <span data-ttu-id="9c591-125">The complete solution is available on [GitHub](https://github.com/Azure-Samples/azure-cosmos-db-sql-api-nodejs-getting-started ).</span><span class="sxs-lookup"><span data-stu-id="9c591-125">The complete solution is available on [GitHub](https://github.com/Azure-Samples/azure-cosmos-db-sql-api-nodejs-getting-started ).</span></span> <span data-ttu-id="9c591-126">See [Get the complete solution](#GetSolution) for quick instructions.</span><span class="sxs-lookup"><span data-stu-id="9c591-126">See [Get the complete solution](#GetSolution) for quick instructions.</span></span>

<span data-ttu-id="9c591-127">After you've completed the Node.js tutorial, please use the voting buttons at the top and bottom of this page to give us feedback.</span><span class="sxs-lookup"><span data-stu-id="9c591-127">After you've completed the Node.js tutorial, please use the voting buttons at the top and bottom of this page to give us feedback.</span></span> <span data-ttu-id="9c591-128">If you'd like us to contact you directly, feel free to include your email address in your comments.</span><span class="sxs-lookup"><span data-stu-id="9c591-128">If you'd like us to contact you directly, feel free to include your email address in your comments.</span></span>

<span data-ttu-id="9c591-129">Now let's get started!</span><span class="sxs-lookup"><span data-stu-id="9c591-129">Now let's get started!</span></span>

## <a name="prerequisites-for-the-nodejs-tutorial"></a><span data-ttu-id="9c591-130">Prerequisites for the Node.js tutorial</span><span class="sxs-lookup"><span data-stu-id="9c591-130">Prerequisites for the Node.js tutorial</span></span>

<span data-ttu-id="9c591-131">Make sure you have the following:</span><span class="sxs-lookup"><span data-stu-id="9c591-131">Make sure you have the following:</span></span>

* <span data-ttu-id="9c591-132">An active Azure account.</span><span class="sxs-lookup"><span data-stu-id="9c591-132">An active Azure account.</span></span> <span data-ttu-id="9c591-133">If you don't have one, you can sign up for a [Free Azure Trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9c591-133">If you don't have one, you can sign up for a [Free Azure Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

  [!INCLUDE [cosmos-db-emulator-docdb-api](../../includes/cosmos-db-emulator-docdb-api.md)]

* <span data-ttu-id="9c591-134">[Node.js](https://nodejs.org/) version v6.0.0 or higher.</span><span class="sxs-lookup"><span data-stu-id="9c591-134">[Node.js](https://nodejs.org/) version v6.0.0 or higher.</span></span>

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="9c591-135">Step 1: Create an Azure Cosmos DB account</span><span class="sxs-lookup"><span data-stu-id="9c591-135">Step 1: Create an Azure Cosmos DB account</span></span>

<span data-ttu-id="9c591-136">Let's create an Azure Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="9c591-136">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="9c591-137">If you already have an account you want to use, you can skip ahead to [Set up your Node.js application](#SetupNode).</span><span class="sxs-lookup"><span data-stu-id="9c591-137">If you already have an account you want to use, you can skip ahead to [Set up your Node.js application](#SetupNode).</span></span> <span data-ttu-id="9c591-138">If you are using the Azure Cosmos DB Emulator, follow the steps at [Azure Cosmos DB Emulator](local-emulator.md) to set up the emulator and skip ahead to [Set up your Node.js application](#SetupNode).</span><span class="sxs-lookup"><span data-stu-id="9c591-138">If you are using the Azure Cosmos DB Emulator, follow the steps at [Azure Cosmos DB Emulator](local-emulator.md) to set up the emulator and skip ahead to [Set up your Node.js application](#SetupNode).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a id="SetupNode"></a><span data-ttu-id="9c591-139">Step 2: Set up your Node.js application</span><span class="sxs-lookup"><span data-stu-id="9c591-139">Step 2: Set up your Node.js application</span></span>

1. <span data-ttu-id="9c591-140">Open your favorite terminal.</span><span class="sxs-lookup"><span data-stu-id="9c591-140">Open your favorite terminal.</span></span>
2. <span data-ttu-id="9c591-141">Locate the folder or directory where you'd like to save your Node.js application.</span><span class="sxs-lookup"><span data-stu-id="9c591-141">Locate the folder or directory where you'd like to save your Node.js application.</span></span>
3. <span data-ttu-id="9c591-142">Create two empty JavaScript files with the following commands:</span><span class="sxs-lookup"><span data-stu-id="9c591-142">Create two empty JavaScript files with the following commands:</span></span>
   * <span data-ttu-id="9c591-143">Windows:</span><span class="sxs-lookup"><span data-stu-id="9c591-143">Windows:</span></span>
     * ```fsutil file createnew app.js 0```
     * ```fsutil file createnew config.js 0```
   * <span data-ttu-id="9c591-144">Linux/OS X:</span><span class="sxs-lookup"><span data-stu-id="9c591-144">Linux/OS X:</span></span>
     * ```touch app.js```
     * ```touch config.js```
4. <span data-ttu-id="9c591-145">Install the documentdb module via npm.</span><span class="sxs-lookup"><span data-stu-id="9c591-145">Install the documentdb module via npm.</span></span> <span data-ttu-id="9c591-146">Use the following command:</span><span class="sxs-lookup"><span data-stu-id="9c591-146">Use the following command:</span></span>
   * ```npm install @azure/cosmos --save```

<span data-ttu-id="9c591-147">Great!</span><span class="sxs-lookup"><span data-stu-id="9c591-147">Great!</span></span> <span data-ttu-id="9c591-148">Now that you've finished setting up, let's start writing some code.</span><span class="sxs-lookup"><span data-stu-id="9c591-148">Now that you've finished setting up, let's start writing some code.</span></span>

## <a id="Config"></a><span data-ttu-id="9c591-149">Step 3: Set your app's configurations</span><span class="sxs-lookup"><span data-stu-id="9c591-149">Step 3: Set your app's configurations</span></span>

<span data-ttu-id="9c591-150">Open ```config.js``` in your favorite text editor.</span><span class="sxs-lookup"><span data-stu-id="9c591-150">Open ```config.js``` in your favorite text editor.</span></span>

<span data-ttu-id="9c591-151">Then, copy and paste the code snippet below and set properties ```config.endpoint``` and ```config.primaryKey``` to your Azure Cosmos DB endpoint URI and primary key.</span><span class="sxs-lookup"><span data-stu-id="9c591-151">Then, copy and paste the code snippet below and set properties ```config.endpoint``` and ```config.primaryKey``` to your Azure Cosmos DB endpoint URI and primary key.</span></span> <span data-ttu-id="9c591-152">Both these configurations can be found in the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9c591-152">Both these configurations can be found in the [Azure portal](https://portal.azure.com).</span></span>

![Node.js tutorial - Screen shot of the Azure portal, showing an Azure Cosmos DB account, with the ACTIVE hub highlighted, the KEYS button highlighted on the Azure Cosmos DB account blade, and the URI, PRIMARY KEY and SECONDARY KEY values highlighted on the Keys blade - Node database][keys]

```nodejs
// ADD THIS PART TO YOUR CODE
var config = {}

config.endpoint = "~your Azure Cosmos DB endpoint uri here~";
config.primaryKey = "~your primary key here~";
``` 

<span data-ttu-id="9c591-154">Copy and paste the ```database```, ```container```, and ```items``` data to your ```config``` object below where you set your ```config.endpoint``` and ```config.primaryKey``` properties.</span><span class="sxs-lookup"><span data-stu-id="9c591-154">Copy and paste the ```database```, ```container```, and ```items``` data to your ```config``` object below where you set your ```config.endpoint``` and ```config.primaryKey``` properties.</span></span> <span data-ttu-id="9c591-155">If you already have data you'd like to store in your database, you can use Azure Cosmos DB's [Data Migration tool](import-data.md) rather than defining the data here.</span><span class="sxs-lookup"><span data-stu-id="9c591-155">If you already have data you'd like to store in your database, you can use Azure Cosmos DB's [Data Migration tool](import-data.md) rather than defining the data here.</span></span>

```nodejs
var config = {}

config.endpoint = "~your Azure Cosmos DB account endpoint uri here~";
config.primaryKey = "~your primary key here~";

config.database = {
    "id": "FamilyDatabase"
};

config.container = {
    "id": "FamilyContainer"
};

config.items = {
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
```
<span data-ttu-id="9c591-156">Note, if you are familiar with the previous version of the JavaScript SDK, you may be used to seeing the terms 'collection' and 'document.'</span><span class="sxs-lookup"><span data-stu-id="9c591-156">Note, if you are familiar with the previous version of the JavaScript SDK, you may be used to seeing the terms 'collection' and 'document.'</span></span> <span data-ttu-id="9c591-157">Because Azure Cosmos DB supports [multiple API models](https://docs.microsoft.com/azure/cosmos-db/introduction#key-capabilities), version 2.0+ of the JavaScript SDK uses the generic terms 'container' and 'item.'</span><span class="sxs-lookup"><span data-stu-id="9c591-157">Because Azure Cosmos DB supports [multiple API models](https://docs.microsoft.com/azure/cosmos-db/introduction#key-capabilities), version 2.0+ of the JavaScript SDK uses the generic terms 'container' and 'item.'</span></span> <span data-ttu-id="9c591-158">A container can be a collection, graph, or table.</span><span class="sxs-lookup"><span data-stu-id="9c591-158">A container can be a collection, graph, or table.</span></span> <span data-ttu-id="9c591-159">An item can be a document, edge/vertex, or row, and is the content inside a container.</span><span class="sxs-lookup"><span data-stu-id="9c591-159">An item can be a document, edge/vertex, or row, and is the content inside a container.</span></span> 

<span data-ttu-id="9c591-160">Finally, export your ```config``` object, so that you can reference it within the ```app.js``` file.</span><span class="sxs-lookup"><span data-stu-id="9c591-160">Finally, export your ```config``` object, so that you can reference it within the ```app.js``` file.</span></span>
```nodejs
        },
        "isRegistered": false
    }
};

// ADD THIS PART TO YOUR CODE
module.exports = config;
```
## <a id="Connect"></a> <span data-ttu-id="9c591-161">Step 4: Connect to an Azure Cosmos DB account</span><span class="sxs-lookup"><span data-stu-id="9c591-161">Step 4: Connect to an Azure Cosmos DB account</span></span>

<span data-ttu-id="9c591-162">Open your empty ```app.js``` file in the text editor.</span><span class="sxs-lookup"><span data-stu-id="9c591-162">Open your empty ```app.js``` file in the text editor.</span></span> <span data-ttu-id="9c591-163">Copy and paste the code below to import the ```@azure/cosmos``` module and your newly created ```config``` module.</span><span class="sxs-lookup"><span data-stu-id="9c591-163">Copy and paste the code below to import the ```@azure/cosmos``` module and your newly created ```config``` module.</span></span>

```nodejs
// ADD THIS PART TO YOUR CODE
const CosmosClient = require('@azure/cosmos').CosmosClient;

const config = require('./config');
const url = require('url');
```

<span data-ttu-id="9c591-164">Copy and paste the code to use the previously saved ```config.endpoint``` and ```config.primaryKey``` to create a new CosmosClient.</span><span class="sxs-lookup"><span data-stu-id="9c591-164">Copy and paste the code to use the previously saved ```config.endpoint``` and ```config.primaryKey``` to create a new CosmosClient.</span></span>

```nodejs
const url = require('url');

// ADD THIS PART TO YOUR CODE
const endpoint = config.endpoint;
const masterKey = config.primaryKey;

const client = new CosmosClient({ endpoint: endpoint, auth: { masterKey: masterKey } });
```

<span data-ttu-id="9c591-165">Now that you have the code to initialize the Azure Cosmos DB client, let's take a look at how to work with Azure Cosmos DB resources.</span><span class="sxs-lookup"><span data-stu-id="9c591-165">Now that you have the code to initialize the Azure Cosmos DB client, let's take a look at how to work with Azure Cosmos DB resources.</span></span>

## <a name="step-5-create-a-database"></a><span data-ttu-id="9c591-166">Step 5: Create a database</span><span class="sxs-lookup"><span data-stu-id="9c591-166">Step 5: Create a database</span></span>

<span data-ttu-id="9c591-167">Copy and paste the code below to set the HTTP status for Not Found, the database id, and the container id. These ids are how the Azure Cosmos DB client will find the right database and container.</span><span class="sxs-lookup"><span data-stu-id="9c591-167">Copy and paste the code below to set the HTTP status for Not Found, the database id, and the container id. These ids are how the Azure Cosmos DB client will find the right database and container.</span></span>

```nodejs
const client = new CosmosClient({ endpoint: endpoint, auth: { masterKey: masterKey } });

// ADD THIS PART TO YOUR CODE
const HttpStatusCodes = { NOTFOUND: 404 };

const databaseId = config.database.id;
const containerId = config.container.id;
```

<span data-ttu-id="9c591-168">A [database](sql-api-resources.md#databases) can be created by using either the [createIfNotExists](/javascript/api/%40azure/cosmos/databases) or [create](/javascript/api/%40azure/cosmos/databases) function of the **Databases** class.</span><span class="sxs-lookup"><span data-stu-id="9c591-168">A [database](sql-api-resources.md#databases) can be created by using either the [createIfNotExists](/javascript/api/%40azure/cosmos/databases) or [create](/javascript/api/%40azure/cosmos/databases) function of the **Databases** class.</span></span> <span data-ttu-id="9c591-169">A database is the logical container of items partitioned across containers.</span><span class="sxs-lookup"><span data-stu-id="9c591-169">A database is the logical container of items partitioned across containers.</span></span> 

<span data-ttu-id="9c591-170">Copy and paste the **createDatabase** and **readDatabase** functions into the app.js file underneath the definition of ```databaseId``` and ```containerId```.</span><span class="sxs-lookup"><span data-stu-id="9c591-170">Copy and paste the **createDatabase** and **readDatabase** functions into the app.js file underneath the definition of ```databaseId``` and ```containerId```.</span></span> <span data-ttu-id="9c591-171">The **createDatabase** function will create a new database with id ```FamilyDatabase```, specified from the ```config``` object if it does not already exist.</span><span class="sxs-lookup"><span data-stu-id="9c591-171">The **createDatabase** function will create a new database with id ```FamilyDatabase```, specified from the ```config``` object if it does not already exist.</span></span> <span data-ttu-id="9c591-172">The **readDatabase** function will read the database's definition to ensure that the database exists.</span><span class="sxs-lookup"><span data-stu-id="9c591-172">The **readDatabase** function will read the database's definition to ensure that the database exists.</span></span>

```nodejs
/**
 * Create the database if it does not exist
 */
async function createDatabase() {
    const { database } = await client.databases.createIfNotExists({ id: databaseId });
    console.log(`Created database:\n${database.id}\n`);
}

/**
 * Read the database definition
 */
async function readDatabase() {
    const { body: databaseDefinition } = await client.database(databaseId).read();
    console.log(`Reading database:\n${databaseDefinition.id}\n`);
}
```

<span data-ttu-id="9c591-173">Copy and paste the code below where you set the **createDatabase** and **readDatabase** functions to add the helper function **exit** that will print the exit message.</span><span class="sxs-lookup"><span data-stu-id="9c591-173">Copy and paste the code below where you set the **createDatabase** and **readDatabase** functions to add the helper function **exit** that will print the exit message.</span></span> 

```nodejs
// ADD THIS PART TO YOUR CODE
function exit(message) {
    console.log(message);
    console.log('Press any key to exit');
    process.stdin.setRawMode(true);
    process.stdin.resume();
    process.stdin.on('data', process.exit.bind(process, 0));
};
```
<span data-ttu-id="9c591-174">Copy and paste the code below where you set the **exit** function to call the **createDatabase** and **readDatabase** functions.</span><span class="sxs-lookup"><span data-stu-id="9c591-174">Copy and paste the code below where you set the **exit** function to call the **createDatabase** and **readDatabase** functions.</span></span>

```nodejs
createDatabase()
    .then(() => readDatabase())
    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error \${JSON.stringify(error)}`) });
```

<span data-ttu-id="9c591-175">At this point, your code in ```app.js``` should now look like this:</span><span class="sxs-lookup"><span data-stu-id="9c591-175">At this point, your code in ```app.js``` should now look like this:</span></span>

```nodejs
const CosmosClient = require('@azure/cosmos').CosmosClient;

const config = require('./config');
const url = require('url');

const endpoint = config.endpoint;
const masterKey = config.primaryKey;

const client = new CosmosClient({ endpoint: endpoint, auth: { masterKey: masterKey } });

const HttpStatusCodes = { NOTFOUND: 404 };

const databaseId = config.database.id;
const containerId = config.container.id;


/**
 * Create the database if it does not exist
 */
async function createDatabase() {
    const { database } = await client.databases.createIfNotExists({ id: databaseId });
    console.log(`Created database:\n${database.id}\n`);
}

/**
 * Read the database definition
 */
async function readDatabase() {
    const { body: databaseDefinition } = await client.database(databaseId).read();
    console.log(`Reading database:\n${databaseDefinition.id}\n`);
}

/**
 * Exit the app with a prompt
 * @param {message} message - The message to display
 */
function exit(message) {
    console.log(message);
    console.log('Press any key to exit');
    process.stdin.setRawMode(true);
    process.stdin.resume();
    process.stdin.on('data', process.exit.bind(process, 0));
}

createDatabase()
    .then(() => readDatabase())
    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });
```

<span data-ttu-id="9c591-176">In your terminal, locate your ```app.js``` file and run the command:</span><span class="sxs-lookup"><span data-stu-id="9c591-176">In your terminal, locate your ```app.js``` file and run the command:</span></span> 
```bash 
node app.js
```

<span data-ttu-id="9c591-177">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="9c591-177">Congratulations!</span></span> <span data-ttu-id="9c591-178">You have successfully created an Azure Cosmos DB database.</span><span class="sxs-lookup"><span data-stu-id="9c591-178">You have successfully created an Azure Cosmos DB database.</span></span>

## <a id="CreateContainer"></a><span data-ttu-id="9c591-179">Step 6: Create a container</span><span class="sxs-lookup"><span data-stu-id="9c591-179">Step 6: Create a container</span></span>

> [!WARNING]
> Calling the function **createContainer** will create a new container, which has pricing implications. For more details, visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).

<span data-ttu-id="9c591-182">A container can be created by using either the [createIfNotExists](/javascript/api/%40azure/cosmos/containers) or [create](/javascript/api/%40azure/cosmos/containers) function from the **Containers** class.</span><span class="sxs-lookup"><span data-stu-id="9c591-182">A container can be created by using either the [createIfNotExists](/javascript/api/%40azure/cosmos/containers) or [create](/javascript/api/%40azure/cosmos/containers) function from the **Containers** class.</span></span> 

<span data-ttu-id="9c591-183">A container consists of items (which in the case of the SQL API are JSON documents) and associated JavaScript application logic.</span><span class="sxs-lookup"><span data-stu-id="9c591-183">A container consists of items (which in the case of the SQL API are JSON documents) and associated JavaScript application logic.</span></span>

<span data-ttu-id="9c591-184">Copy and paste the **createContainer**  and **readContainer** function underneath the **readDatabase** function in the app.js file.</span><span class="sxs-lookup"><span data-stu-id="9c591-184">Copy and paste the **createContainer**  and **readContainer** function underneath the **readDatabase** function in the app.js file.</span></span> <span data-ttu-id="9c591-185">The **createContainer** function will create a new container with the ```containerId``` specified from the ```config``` object if it does not already exist.</span><span class="sxs-lookup"><span data-stu-id="9c591-185">The **createContainer** function will create a new container with the ```containerId``` specified from the ```config``` object if it does not already exist.</span></span> <span data-ttu-id="9c591-186">The **readContainer** function will read the container definition to verify the container exists.</span><span class="sxs-lookup"><span data-stu-id="9c591-186">The **readContainer** function will read the container definition to verify the container exists.</span></span>

```nodejs
/**
 * Create the container if it does not exist
 */
async function createContainer() {
    const { container } = await client.database(databaseId).containers.createIfNotExists({ id: containerId });
    console.log(`Created container:\n${config.container.id}\n`);
}

/**
 * Read the container definition
 */
async function readContainer() {
    const { body: containerDefinition } = await client.database(databaseId).container(containerId).read();
    console.log(`Reading container:\n${containerDefinition.id}\n`);
}
```

<span data-ttu-id="9c591-187">Copy and paste the code underneath the call to **readDatabase** to execute the **createContainer** and **readContainer** functions.</span><span class="sxs-lookup"><span data-stu-id="9c591-187">Copy and paste the code underneath the call to **readDatabase** to execute the **createContainer** and **readContainer** functions.</span></span>
```nodejs
createDatabase()
    .then(() => readDatabase())

    // ADD THIS PART TO YOUR CODE
    .then(() => createContainer())
    .then(() => readContainer())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });
```

<span data-ttu-id="9c591-188">At this point, your code in ```app.js``` should now look like this:</span><span class="sxs-lookup"><span data-stu-id="9c591-188">At this point, your code in ```app.js``` should now look like this:</span></span>

```nodejs
const CosmosClient = require('@azure/cosmos').CosmosClient;

const config = require('./config');
const url = require('url');

const endpoint = config.endpoint;
const masterKey = config.primaryKey;

const client = new CosmosClient({ endpoint: endpoint, auth: { masterKey: masterKey } });

const HttpStatusCodes = { NOTFOUND: 404 };

const databaseId = config.database.id;
const containerId = config.container.id;

/**
 * Create the database if it does not exist
 */
async function createDatabase() {
    const { database } = await client.databases.createIfNotExists({ id: databaseId });
    console.log(`Created database:\n${database.id}\n`);
}

/**
 * Read the database definition
 */
async function readDatabase() {
    const { body: databaseDefinition } = await client.database(databaseId).read();
    console.log(`Reading database:\n${databaseDefinition.id}\n`);
}

/**
 * Create the container if it does not exist
 */
async function createContainer() {
    const { container } = await client.database(databaseId).containers.createIfNotExists({ id: containerId });
    console.log(`Created container:\n${config.container.id}\n`);
}

/**
 * Read the container definition
 */
async function readContainer() {
    const { body: containerDefinition } = await client.database(databaseId).container(containerId).read();
    console.log(`Reading container:\n${containerDefinition.id}\n`);
}

/**
 * Exit the app with a prompt
 * @param {message} message - The message to display
 */
function exit(message) {
    console.log(message);
    console.log('Press any key to exit');
    process.stdin.setRawMode(true);
    process.stdin.resume();
    process.stdin.on('data', process.exit.bind(process, 0));
}

createDatabase()
    .then(() => readDatabase())
    .then(() => createContainer())
    .then(() => readContainer())
    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });
```

<span data-ttu-id="9c591-189">In your terminal, locate your ```app.js``` file and run the command:</span><span class="sxs-lookup"><span data-stu-id="9c591-189">In your terminal, locate your ```app.js``` file and run the command:</span></span> 

```bash 
node app.js
```

<span data-ttu-id="9c591-190">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="9c591-190">Congratulations!</span></span> <span data-ttu-id="9c591-191">You have successfully created an Azure Cosmos DB container.</span><span class="sxs-lookup"><span data-stu-id="9c591-191">You have successfully created an Azure Cosmos DB container.</span></span>

## <a id="CreateItem"></a><span data-ttu-id="9c591-192">Step 7: Create an item</span><span class="sxs-lookup"><span data-stu-id="9c591-192">Step 7: Create an item</span></span>

<span data-ttu-id="9c591-193">An item can be created by using the [create](/javascript/api/%40azure/cosmos/items) function of the **Items** class.</span><span class="sxs-lookup"><span data-stu-id="9c591-193">An item can be created by using the [create](/javascript/api/%40azure/cosmos/items) function of the **Items** class.</span></span> <span data-ttu-id="9c591-194">When using the SQL API, items are projected as documents, which are user-defined (arbitrary) JSON content.</span><span class="sxs-lookup"><span data-stu-id="9c591-194">When using the SQL API, items are projected as documents, which are user-defined (arbitrary) JSON content.</span></span> <span data-ttu-id="9c591-195">You can now insert an item into Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="9c591-195">You can now insert an item into Azure Cosmos DB.</span></span>

<span data-ttu-id="9c591-196">Copy and paste the **createFamilyItem** function underneath the **readContainer** function.</span><span class="sxs-lookup"><span data-stu-id="9c591-196">Copy and paste the **createFamilyItem** function underneath the **readContainer** function.</span></span> <span data-ttu-id="9c591-197">The **createFamilyItem** function creates the items containing the JSON data saved in the ```config``` object.</span><span class="sxs-lookup"><span data-stu-id="9c591-197">The **createFamilyItem** function creates the items containing the JSON data saved in the ```config``` object.</span></span> <span data-ttu-id="9c591-198">We'll check to make sure an item with the same id does not already exist before creating it.</span><span class="sxs-lookup"><span data-stu-id="9c591-198">We'll check to make sure an item with the same id does not already exist before creating it.</span></span>

```nodejs
/**
 * Create family item if it does not exist
 */
async function createFamilyItem(itemBody) {
    try {
        // read the item to see if it exists
        const { item } = await client.database(databaseId).container(containerId).item(itemBody.id).read();
        console.log(`Item with family id ${itemBody.id} already exists\n`);
    }
    catch (error) {
        // create the family item if it does not exist
        if (error.code === HttpStatusCodes.NOTFOUND) {
            const { item } = await client.database(databaseId).container(containerId).items.create(itemBody);
            console.log(`Created family item with id:\n${itemBody.id}\n`);
        } else {
            throw error;
        }
    }
};
```

<span data-ttu-id="9c591-199">Copy and paste the code below the call to **readContainer** to execute the **createFamilyItem** function.</span><span class="sxs-lookup"><span data-stu-id="9c591-199">Copy and paste the code below the call to **readContainer** to execute the **createFamilyItem** function.</span></span>
```nodejs
createDatabase()
    .then(() => readDatabase())
    .then(() => createContainer())
    .then(() => readContainer())

    // ADD THIS PART TO YOUR CODE
    .then(() => createFamilyItem(config.items.Andersen))
    .then(() => createFamilyItem(config.items.Wakefield))
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });
```

<span data-ttu-id="9c591-200">In your terminal, locate your ```app.js``` file and run the command:</span><span class="sxs-lookup"><span data-stu-id="9c591-200">In your terminal, locate your ```app.js``` file and run the command:</span></span> 

```bash 
node app.js
```

<span data-ttu-id="9c591-201">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="9c591-201">Congratulations!</span></span> <span data-ttu-id="9c591-202">You have successfully created an Azure Cosmos DB item.</span><span class="sxs-lookup"><span data-stu-id="9c591-202">You have successfully created an Azure Cosmos DB item.</span></span>


## <a id="Query"></a><span data-ttu-id="9c591-203">Step 8: Query Azure Cosmos DB resources</span><span class="sxs-lookup"><span data-stu-id="9c591-203">Step 8: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="9c591-204">Azure Cosmos DB supports [rich queries](sql-api-sql-query.md) against JSON documents stored in each container.</span><span class="sxs-lookup"><span data-stu-id="9c591-204">Azure Cosmos DB supports [rich queries](sql-api-sql-query.md) against JSON documents stored in each container.</span></span> <span data-ttu-id="9c591-205">The following sample code shows a query that you can run against the documents in your container.</span><span class="sxs-lookup"><span data-stu-id="9c591-205">The following sample code shows a query that you can run against the documents in your container.</span></span>

<span data-ttu-id="9c591-206">Copy and paste the **queryContainer** function below the **createFamilyItem** function in the app.js file.</span><span class="sxs-lookup"><span data-stu-id="9c591-206">Copy and paste the **queryContainer** function below the **createFamilyItem** function in the app.js file.</span></span> <span data-ttu-id="9c591-207">Azure Cosmos DB supports SQL-like queries as shown below.</span><span class="sxs-lookup"><span data-stu-id="9c591-207">Azure Cosmos DB supports SQL-like queries as shown below.</span></span> <span data-ttu-id="9c591-208">For more information on building complex queries, check out the [Query Playground](https://www.documentdb.com/sql/demo) and the [query documentation](sql-api-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="9c591-208">For more information on building complex queries, check out the [Query Playground](https://www.documentdb.com/sql/demo) and the [query documentation](sql-api-sql-query.md).</span></span>

```nodejs
/**
 * Query the container using SQL
 */
async function queryContainer() {
    console.log(`Querying container:\n${config.container.id}`);

    // query to return all children in a family
    const querySpec = {
        query: "SELECT VALUE r.children FROM root r WHERE r.lastName = @lastName",
        parameters: [
            {
                name: "@lastName",
                value: "Andersen"
            }
        ]
    };

    const { result: results } = await client.database(databaseId).container(containerId).items.query(querySpec).toArray();
    for (var queryResult of results) {
        let resultString = JSON.stringify(queryResult);
        console.log(`\tQuery returned ${resultString}\n`);
    }
};
```

<span data-ttu-id="9c591-209">Copy and paste the code below the calls to **createFamilyItem** to execute the **queryContainer** function.</span><span class="sxs-lookup"><span data-stu-id="9c591-209">Copy and paste the code below the calls to **createFamilyItem** to execute the **queryContainer** function.</span></span>

```nodejs
createDatabase()
    .then(() => readDatabase())
    .then(() => createContainer())
    .then(() => readContainer())
    .then(() => createFamilyItem(config.items.Andersen))
    .then(() => createFamilyItem(config.items.Wakefield))

    // ADD THIS PART TO YOUR CODE
    .then(() => queryContainer())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });
```

<span data-ttu-id="9c591-210">In your terminal, locate your ```app.js``` file and run the command:</span><span class="sxs-lookup"><span data-stu-id="9c591-210">In your terminal, locate your ```app.js``` file and run the command:</span></span>

```bash 
node app.js
```

<span data-ttu-id="9c591-211">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="9c591-211">Congratulations!</span></span> <span data-ttu-id="9c591-212">You have successfully queried your Azure Cosmos DB items.</span><span class="sxs-lookup"><span data-stu-id="9c591-212">You have successfully queried your Azure Cosmos DB items.</span></span>

## <a id="ReplaceItem"></a><span data-ttu-id="9c591-213">Step 9: Replace an item</span><span class="sxs-lookup"><span data-stu-id="9c591-213">Step 9: Replace an item</span></span>
<span data-ttu-id="9c591-214">Azure Cosmos DB supports replacing the content of items.</span><span class="sxs-lookup"><span data-stu-id="9c591-214">Azure Cosmos DB supports replacing the content of items.</span></span>

<span data-ttu-id="9c591-215">Copy and paste the **replaceFamilyItem** function below the **queryContainer** function in the app.js file.</span><span class="sxs-lookup"><span data-stu-id="9c591-215">Copy and paste the **replaceFamilyItem** function below the **queryContainer** function in the app.js file.</span></span> <span data-ttu-id="9c591-216">Note we've changed the property 'grade' of a child to 6 from the previous value of 5.</span><span class="sxs-lookup"><span data-stu-id="9c591-216">Note we've changed the property 'grade' of a child to 6 from the previous value of 5.</span></span>

```nodejs
// ADD THIS PART TO YOUR CODE
/**
 * Replace the item by ID.
 */
async function replaceFamilyItem(itemBody) {
    console.log(`Replacing item:\n${itemBody.id}\n`);
    // Change property 'grade'
    itemBody.children[0].grade = 6;
    const { item } = await client.database(databaseId).container(containerId).item(itemBody.id).replace(itemBody);
};
```
<span data-ttu-id="9c591-217">Copy and paste the code below the call to **queryContainer** to execute the **replaceFamilyItem** function.</span><span class="sxs-lookup"><span data-stu-id="9c591-217">Copy and paste the code below the call to **queryContainer** to execute the **replaceFamilyItem** function.</span></span> <span data-ttu-id="9c591-218">Also, add the code to call **queryContainer** again to verify that item has successfully changed.</span><span class="sxs-lookup"><span data-stu-id="9c591-218">Also, add the code to call **queryContainer** again to verify that item has successfully changed.</span></span>

```nodejs
createDatabase()
    .then(() => readDatabase())
    .then(() => createContainer())
    .then(() => readContainer())
    .then(() => createFamilyItem(config.items.Andersen))
    .then(() => createFamilyItem(config.items.Wakefield))
    .then(() => queryContainer())

    // ADD THIS PART TO YOUR CODE
    .then(() => replaceFamilyItem(config.items.Andersen))
    .then(() => queryContainer())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });
```
<span data-ttu-id="9c591-219">In your terminal, locate your ```app.js``` file and run the command:</span><span class="sxs-lookup"><span data-stu-id="9c591-219">In your terminal, locate your ```app.js``` file and run the command:</span></span>

```bash 
node app.js
```

<span data-ttu-id="9c591-220">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="9c591-220">Congratulations!</span></span> <span data-ttu-id="9c591-221">You have successfully replaced an Azure Cosmos DB item.</span><span class="sxs-lookup"><span data-stu-id="9c591-221">You have successfully replaced an Azure Cosmos DB item.</span></span>

## <a id="DeleteItem"></a><span data-ttu-id="9c591-222">Step 10: Delete an item</span><span class="sxs-lookup"><span data-stu-id="9c591-222">Step 10: Delete an item</span></span>

<span data-ttu-id="9c591-223">Azure Cosmos DB supports deleting JSON items.</span><span class="sxs-lookup"><span data-stu-id="9c591-223">Azure Cosmos DB supports deleting JSON items.</span></span>

<span data-ttu-id="9c591-224">Copy and paste the **deleteFamilyItem** function underneath the **replaceFamilyItem** function.</span><span class="sxs-lookup"><span data-stu-id="9c591-224">Copy and paste the **deleteFamilyItem** function underneath the **replaceFamilyItem** function.</span></span>

```nodejs
/**
 * Delete the item by ID.
 */
async function deleteFamilyItem(itemBody) {
    await client.database(databaseId).container(containerId).item(itemBody.id).delete(itemBody);
    console.log(`Deleted item:\n${itemBody.id}\n`);
};
```

<span data-ttu-id="9c591-225">Copy and paste the code below the call to the second **queryContainer** to execute the **deleteFamilyItem** function.</span><span class="sxs-lookup"><span data-stu-id="9c591-225">Copy and paste the code below the call to the second **queryContainer** to execute the **deleteFamilyItem** function.</span></span>

```nodejs
createDatabase()
    .then(() => readDatabase())
    .then(() => createContainer())
    .then(() => readContainer())
    .then(() => createFamilyItem(config.items.Andersen))
    .then(() => createFamilyItem(config.items.Wakefield))
    .then(() => queryContainer
    ())
    .then(() => replaceFamilyItem(config.items.Andersen))
    .then(() => queryContainer())

    // ADD THIS PART TO YOUR CODE
    .then(() => deleteFamilyItem(config.items.Andersen))
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });
```

<span data-ttu-id="9c591-226">In your terminal, locate your ```app.js``` file and run the command:</span><span class="sxs-lookup"><span data-stu-id="9c591-226">In your terminal, locate your ```app.js``` file and run the command:</span></span> 

```bash 
node app.js
```

<span data-ttu-id="9c591-227">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="9c591-227">Congratulations!</span></span> <span data-ttu-id="9c591-228">You have successfully deleted an Azure Cosmos DB item.</span><span class="sxs-lookup"><span data-stu-id="9c591-228">You have successfully deleted an Azure Cosmos DB item.</span></span>

## <a id="DeleteDatabase"></a><span data-ttu-id="9c591-229">Step 11: Delete the database</span><span class="sxs-lookup"><span data-stu-id="9c591-229">Step 11: Delete the database</span></span>

<span data-ttu-id="9c591-230">Deleting the created database will remove the database and all children resources (containers, items, etc.).</span><span class="sxs-lookup"><span data-stu-id="9c591-230">Deleting the created database will remove the database and all children resources (containers, items, etc.).</span></span>

<span data-ttu-id="9c591-231">Copy and paste the **cleanup** function underneath the **deleteFamilyItem** function to remove the database and all its children resources.</span><span class="sxs-lookup"><span data-stu-id="9c591-231">Copy and paste the **cleanup** function underneath the **deleteFamilyItem** function to remove the database and all its children resources.</span></span>

```nodejs
/**
 * Cleanup the database and container on completion
 */
async function cleanup() {
    await client.database(databaseId).delete();
}
```

<span data-ttu-id="9c591-232">Copy and paste the code below the call to **deleteFamilyItem** to execute the **cleanup** function.</span><span class="sxs-lookup"><span data-stu-id="9c591-232">Copy and paste the code below the call to **deleteFamilyItem** to execute the **cleanup** function.</span></span>

```nodejs
createDatabase()
    .then(() => readDatabase())
    .then(() => createContainer())
    .then(() => readContainer())
    .then(() => createFamilyItem(config.items.Andersen))
    .then(() => createFamilyItem(config.items.Wakefield))
    .then(() => queryContainer())
    .then(() => replaceFamilyItem(config.items.Andersen))
    .then(() => queryContainer())
    .then(() => deleteFamilyItem(config.items.Andersen))

    // ADD THIS PART TO YOUR CODE
    .then(() => cleanup())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });
```

## <a id="Run"></a><span data-ttu-id="9c591-233">Step 12: Run your Node.js application all together!</span><span class="sxs-lookup"><span data-stu-id="9c591-233">Step 12: Run your Node.js application all together!</span></span>

<span data-ttu-id="9c591-234">Altogether, your code should look like this:</span><span class="sxs-lookup"><span data-stu-id="9c591-234">Altogether, your code should look like this:</span></span>
```nodejs
const CosmosClient = require('@azure/cosmos').CosmosClient;

const config = require('./config');
const url = require('url');

const endpoint = config.endpoint;
const masterKey = config.primaryKey;

const HttpStatusCodes = { NOTFOUND: 404 };

const databaseId = config.database.id;
const containerId = config.container.id;

const client = new CosmosClient({ endpoint: endpoint, auth: { masterKey: masterKey } });

/**
 * Create the database if it does not exist
 */
async function createDatabase() {
    const { database } = await client.databases.createIfNotExists({ id: databaseId });
    console.log(`Created database:\n${database.id}\n`);
}

/**
 * Read the database definition
 */
async function readDatabase() {
    const { body: databaseDefinition } = await client.database(databaseId).read();
    console.log(`Reading database:\n${databaseDefinition.id}\n`);
}

/**
 * Create the container if it does not exist
 */
async function createContainer() {
    const { container } = await client.database(databaseId).containers.createIfNotExists({ id: containerId });
    console.log(`Created container:\n${config.container.id}\n`);
}

/**
 * Read the container definition
 */
async function readContainer() {
    const { body: containerDefinition } = await client.database(databaseId).container(containerId).read();
    console.log(`Reading container:\n${containerDefinition.id}\n`);
}

/**
 * Create family item if it does not exist
 */
async function createFamilyItem(itemBody) {
    try {
        // read the item to see if it exists
        const { item } = await client.database(databaseId).container(containerId).item(itemBody.id).read();
        console.log(`Item with family id ${itemBody.id} already exists\n`);
    }
    catch (error) {
        // create the family item if it does not exist
        if (error.code === HttpStatusCodes.NOTFOUND) {
            const { item } = await client.database(databaseId).container(containerId).items.create(itemBody);
            console.log(`Created family item with id:\n${itemBody.id}\n`);
        } else {
            throw error;
        }
    }
};

/**
 * Query the container using SQL
 */
async function queryContainer() {
    console.log(`Querying container:\n${config.container.id}`);

    // query to return all children in a family
    const querySpec = {
        query: "SELECT VALUE r.children FROM root r WHERE r.lastName = @lastName",
        parameters: [
            {
                name: "@lastName",
                value: "Andersen"
            }
        ]
    };

    const { result: results } = await client.database(databaseId).container(containerId).items.query(querySpec).toArray();
    for (var queryResult of results) {
        let resultString = JSON.stringify(queryResult);
        console.log(`\tQuery returned ${resultString}\n`);
    }
};

/**
 * Replace the item by ID.
 */
async function replaceFamilyItem(itemBody) {
    console.log(`Replacing item:\n${itemBody.id}\n`);
    // Change property 'grade'
    itemBody.children[0].grade = 6;
    const { item } = await client.database(databaseId).container(containerId).item(itemBody.id).replace(itemBody);
};

/**
 * Delete the item by ID.
 */
async function deleteFamilyItem(itemBody) {
    await client.database(databaseId).container(containerId).item(itemBody.id).delete(itemBody);
    console.log(`Deleted item:\n${itemBody.id}\n`);
};

/**
 * Cleanup the database and container on completion
 */
async function cleanup() {
    await client.database(databaseId).delete();
}

/**
 * Exit the app with a prompt
 * @param {message} message - The message to display
 */
function exit(message) {
    console.log(message);
    console.log('Press any key to exit');
    process.stdin.setRawMode(true);
    process.stdin.resume();
    process.stdin.on('data', process.exit.bind(process, 0));
}

createDatabase()
    .then(() => readDatabase())
    .then(() => createContainer())
    .then(() => readContainer())
    .then(() => createFamilyItem(config.items.Andersen))
    .then(() => createFamilyItem(config.items.Wakefield))
    .then(() => queryContainer())
    .then(() => replaceFamilyItem(config.items.Andersen))
    .then(() => queryContainer())
    .then(() => deleteFamilyItem(config.items.Andersen))
    .then(() => cleanup())
    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });
```

<span data-ttu-id="9c591-235">In your terminal, locate your ```app.js``` file and run the command:</span><span class="sxs-lookup"><span data-stu-id="9c591-235">In your terminal, locate your ```app.js``` file and run the command:</span></span> 

```bash 
node app.js
```

<span data-ttu-id="9c591-236">You should see the output of your get started app.</span><span class="sxs-lookup"><span data-stu-id="9c591-236">You should see the output of your get started app.</span></span> <span data-ttu-id="9c591-237">The output should match the example text below.</span><span class="sxs-lookup"><span data-stu-id="9c591-237">The output should match the example text below.</span></span>

    Created database:
    FamilyDatabase

    Reading database:
    FamilyDatabase

    Created container:
    FamilyContainer

    Reading container:
    FamilyContainer

    Created family item with id:
    Anderson.1

    Created family item with id:
    Wakefield.7

    Querying container:
    FamilyContainer
            Query returned [{"firstName":"Henriette Thaulow","gender":"female","grade":5,"pets":[{"givenName":"Fluffy"}]}]

    Replacing item:
    Anderson.1

    Querying container:
    FamilyContainer
            Query returned [{"firstName":"Henriette Thaulow","gender":"female","grade":6,"pets":[{"givenName":"Fluffy"}]}]

    Deleted item:
    Anderson.1

    Completed successfully
    Press any key to exit

<span data-ttu-id="9c591-238">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="9c591-238">Congratulations!</span></span> <span data-ttu-id="9c591-239">You've completed the Node.js tutorial and have your first Azure Cosmos DB console application!</span><span class="sxs-lookup"><span data-stu-id="9c591-239">You've completed the Node.js tutorial and have your first Azure Cosmos DB console application!</span></span>

## <a id="GetSolution"></a><span data-ttu-id="9c591-240">Get the complete Node.js tutorial solution</span><span class="sxs-lookup"><span data-stu-id="9c591-240">Get the complete Node.js tutorial solution</span></span>

<span data-ttu-id="9c591-241">If you didn't have time to complete the steps in this tutorial, or just want to download the code, you can get it from [GitHub](https://github.com/Azure-Samples/azure-cosmos-db-sql-api-nodejs-getting-started ).</span><span class="sxs-lookup"><span data-stu-id="9c591-241">If you didn't have time to complete the steps in this tutorial, or just want to download the code, you can get it from [GitHub](https://github.com/Azure-Samples/azure-cosmos-db-sql-api-nodejs-getting-started ).</span></span>

<span data-ttu-id="9c591-242">To run the getting started solution that contains all the code in this article, you will need the following:</span><span class="sxs-lookup"><span data-stu-id="9c591-242">To run the getting started solution that contains all the code in this article, you will need the following:</span></span>

* <span data-ttu-id="9c591-243">An [Azure Cosmos DB account][create-account].</span><span class="sxs-lookup"><span data-stu-id="9c591-243">An [Azure Cosmos DB account][create-account].</span></span>
* <span data-ttu-id="9c591-244">The [Getting Started](https://github.com/Azure-Samples/azure-cosmos-db-sql-api-nodejs-getting-started) solution available on GitHub.</span><span class="sxs-lookup"><span data-stu-id="9c591-244">The [Getting Started](https://github.com/Azure-Samples/azure-cosmos-db-sql-api-nodejs-getting-started) solution available on GitHub.</span></span>

<span data-ttu-id="9c591-245">Install the **@azure/cosmos** module via npm.</span><span class="sxs-lookup"><span data-stu-id="9c591-245">Install the **@azure/cosmos** module via npm.</span></span> <span data-ttu-id="9c591-246">Use the following command:</span><span class="sxs-lookup"><span data-stu-id="9c591-246">Use the following command:</span></span>

* ```npm install @azure/cosmos --save```

<span data-ttu-id="9c591-247">Next, in the ```config.js``` file, update the config.endpoint and config.primaryKey values as described in [Step 3: Set your app's configurations](#Config).</span><span class="sxs-lookup"><span data-stu-id="9c591-247">Next, in the ```config.js``` file, update the config.endpoint and config.primaryKey values as described in [Step 3: Set your app's configurations](#Config).</span></span> 

<span data-ttu-id="9c591-248">Then in your terminal, locate your ```app.js``` file and run the command:</span><span class="sxs-lookup"><span data-stu-id="9c591-248">Then in your terminal, locate your ```app.js``` file and run the command:</span></span> 

```bash 
node app.js
```

<span data-ttu-id="9c591-249">That's it, and you're on your way!</span><span class="sxs-lookup"><span data-stu-id="9c591-249">That's it, and you're on your way!</span></span> 

## <a name="next-steps"></a><span data-ttu-id="9c591-250">Next steps</span><span class="sxs-lookup"><span data-stu-id="9c591-250">Next steps</span></span>
* <span data-ttu-id="9c591-251">Want a more complex Node.js sample?</span><span class="sxs-lookup"><span data-stu-id="9c591-251">Want a more complex Node.js sample?</span></span> <span data-ttu-id="9c591-252">See [Build a Node.js web application using Azure Cosmos DB](sql-api-nodejs-application-preview.md).</span><span class="sxs-lookup"><span data-stu-id="9c591-252">See [Build a Node.js web application using Azure Cosmos DB](sql-api-nodejs-application-preview.md).</span></span>
* <span data-ttu-id="9c591-253">Learn how to [monitor an Azure Cosmos DB account](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="9c591-253">Learn how to [monitor an Azure Cosmos DB account](monitor-accounts.md).</span></span>
* <span data-ttu-id="9c591-254">Run queries against our sample dataset in the [Query Playground](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="9c591-254">Run queries against our sample dataset in the [Query Playground](https://www.documentdb.com/sql/demo).</span></span>

[create-account]: create-sql-api-dotnet.md#create-account
[keys]: media/sql-api-nodejs-get-started/node-js-tutorial-keys.png