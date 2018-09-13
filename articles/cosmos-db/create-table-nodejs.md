---
title: 'Quickstart: Table API with Node.js - Azure Cosmos DB | Microsoft Docs'
description: This quickstart shows how to use the Azure Cosmos DB Table API to create an application with the Azure portal and Node.js
services: cosmos-db
author: SnehaGunda
manager: kfile
ms.service: cosmos-db
ms.component: cosmosdb-table
ms.custom: quick start connect, mvc
ms.devlang: nodejs
ms.topic: quickstart
ms.date: 04/10/2018
ms.author: sngun
ms.openlocfilehash: d8d1ae9e95f76ff9e03dc5a54b6f00ffac8f2b39
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44858006"
---
# <a name="quickstart-build-a-table-api-app-with-nodejs-and-azure-cosmos-db"></a><span data-ttu-id="8e7b4-103">Quickstart: Build a Table API app with Node.js and Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="8e7b4-103">Quickstart: Build a Table API app with Node.js and Azure Cosmos DB</span></span>

> [!div class="op_single_selector"]
> * [.NET](create-table-dotnet.md)
> * [Java](create-table-java.md)
> * [Node.js](create-table-nodejs.md)
> * [Python](create-table-python.md)
> 

<span data-ttu-id="8e7b4-108">This quickstart shows how to use Node.js and the Azure Cosmos DB [Table API](table-introduction.md) to build an app by cloning an example from GitHub.</span><span class="sxs-lookup"><span data-stu-id="8e7b4-108">This quickstart shows how to use Node.js and the Azure Cosmos DB [Table API](table-introduction.md) to build an app by cloning an example from GitHub.</span></span> <span data-ttu-id="8e7b4-109">This quickstart also shows you how to create an Azure Cosmos DB account and how to use Data Explorer to create tables and entities in the web-based Azure portal.</span><span class="sxs-lookup"><span data-stu-id="8e7b4-109">This quickstart also shows you how to create an Azure Cosmos DB account and how to use Data Explorer to create tables and entities in the web-based Azure portal.</span></span>

<span data-ttu-id="8e7b4-110">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span><span class="sxs-lookup"><span data-stu-id="8e7b4-110">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="8e7b4-111">You can quickly create and query document, key/value, wide-column, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="8e7b4-111">You can quickly create and query document, key/value, wide-column, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="8e7b4-112">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="8e7b4-112">Prerequisites</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]
[!INCLUDE [cosmos-db-emulator-docdb-api](../../includes/cosmos-db-emulator-docdb-api.md)]

<span data-ttu-id="8e7b4-113">In addition:</span><span class="sxs-lookup"><span data-stu-id="8e7b4-113">In addition:</span></span>

* <span data-ttu-id="8e7b4-114">[Node.js](https://nodejs.org/en/) version v0.10.29 or higher</span><span class="sxs-lookup"><span data-stu-id="8e7b4-114">[Node.js](https://nodejs.org/en/) version v0.10.29 or higher</span></span>
* [<span data-ttu-id="8e7b4-115">Git</span><span class="sxs-lookup"><span data-stu-id="8e7b4-115">Git</span></span>](http://git-scm.com/)

## <a name="create-a-database-account"></a><span data-ttu-id="8e7b4-116">Create a database account</span><span class="sxs-lookup"><span data-stu-id="8e7b4-116">Create a database account</span></span>

> [!IMPORTANT] 
> You need to create a new Table API account to work with the generally available Table API SDKs. Table API accounts created during preview are not supported by the generally available SDKs.
>

[!INCLUDE [cosmos-db-create-dbaccount-table](../../includes/cosmos-db-create-dbaccount-table.md)]

## <a name="add-a-table"></a><span data-ttu-id="8e7b4-119">Add a table</span><span class="sxs-lookup"><span data-stu-id="8e7b4-119">Add a table</span></span>

[!INCLUDE [cosmos-db-create-table](../../includes/cosmos-db-create-table.md)]

## <a name="add-sample-data"></a><span data-ttu-id="8e7b4-120">Add sample data</span><span class="sxs-lookup"><span data-stu-id="8e7b4-120">Add sample data</span></span>

[!INCLUDE [cosmos-db-create-table-add-sample-data](../../includes/cosmos-db-create-table-add-sample-data.md)]

## <a name="clone-the-sample-application"></a><span data-ttu-id="8e7b4-121">Clone the sample application</span><span class="sxs-lookup"><span data-stu-id="8e7b4-121">Clone the sample application</span></span>

<span data-ttu-id="8e7b4-122">Now let's clone a Table app from github, set the connection string, and run it.</span><span class="sxs-lookup"><span data-stu-id="8e7b4-122">Now let's clone a Table app from github, set the connection string, and run it.</span></span> <span data-ttu-id="8e7b4-123">You'll see how easy it is to work with data programmatically.</span><span class="sxs-lookup"><span data-stu-id="8e7b4-123">You'll see how easy it is to work with data programmatically.</span></span> 

1. <span data-ttu-id="8e7b4-124">Open a command prompt, create a new folder named git-samples, then close the command prompt.</span><span class="sxs-lookup"><span data-stu-id="8e7b4-124">Open a command prompt, create a new folder named git-samples, then close the command prompt.</span></span>

    ```bash
    md "C:\git-samples"
    ```

2. <span data-ttu-id="8e7b4-125">Open a git terminal window, such as git bash, and use the `cd` command to change to the new folder to install the sample app.</span><span class="sxs-lookup"><span data-stu-id="8e7b4-125">Open a git terminal window, such as git bash, and use the `cd` command to change to the new folder to install the sample app.</span></span>

    ```bash
    cd "C:\git-samples"
    ```

3. <span data-ttu-id="8e7b4-126">Run the following command to clone the sample repository.</span><span class="sxs-lookup"><span data-stu-id="8e7b4-126">Run the following command to clone the sample repository.</span></span> <span data-ttu-id="8e7b4-127">This command creates a copy of the sample app on your computer.</span><span class="sxs-lookup"><span data-stu-id="8e7b4-127">This command creates a copy of the sample app on your computer.</span></span>

    ```bash
    git clone https://github.com/Azure-Samples/storage-table-node-getting-started.git
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="8e7b4-128">Update your connection string</span><span class="sxs-lookup"><span data-stu-id="8e7b4-128">Update your connection string</span></span>

<span data-ttu-id="8e7b4-129">Now go back to the Azure portal to get your connection string information and copy it into the app.</span><span class="sxs-lookup"><span data-stu-id="8e7b4-129">Now go back to the Azure portal to get your connection string information and copy it into the app.</span></span> <span data-ttu-id="8e7b4-130">This enables your app to communicate with your hosted database.</span><span class="sxs-lookup"><span data-stu-id="8e7b4-130">This enables your app to communicate with your hosted database.</span></span> 

1. <span data-ttu-id="8e7b4-131">In the [Azure portal](http://portal.azure.com/), click **Connection String**.</span><span class="sxs-lookup"><span data-stu-id="8e7b4-131">In the [Azure portal](http://portal.azure.com/), click **Connection String**.</span></span> 

    ![View and copy the required connection string information from the in the Connection String pane](./media/create-table-nodejs/connection-string.png)

2. <span data-ttu-id="8e7b4-133">Copy the PRIMARY CONNECTION STRING using the copy button on the right-side.</span><span class="sxs-lookup"><span data-stu-id="8e7b4-133">Copy the PRIMARY CONNECTION STRING using the copy button on the right-side.</span></span>

3. <span data-ttu-id="8e7b4-134">Open the app.config file, and paste the value into the connectionString on line three.</span><span class="sxs-lookup"><span data-stu-id="8e7b4-134">Open the app.config file, and paste the value into the connectionString on line three.</span></span> 

    > [!IMPORTANT]
    > If your Endpoint uses documents.azure.com, that means you have a preview account, and you need to create a [new Table API account](#create-a-database-account) to work with the generally available Table API SDK.
    >

3. <span data-ttu-id="8e7b4-136">Save the app.config file.</span><span class="sxs-lookup"><span data-stu-id="8e7b4-136">Save the app.config file.</span></span>

<span data-ttu-id="8e7b4-137">You've now updated your app with all the info it needs to communicate with Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="8e7b4-137">You've now updated your app with all the info it needs to communicate with Azure Cosmos DB.</span></span> 

## <a name="run-the-app"></a><span data-ttu-id="8e7b4-138">Run the app</span><span class="sxs-lookup"><span data-stu-id="8e7b4-138">Run the app</span></span>

1. <span data-ttu-id="8e7b4-139">In the git terminal window, `cd` to the storage-table-java-getting-started folder.</span><span class="sxs-lookup"><span data-stu-id="8e7b4-139">In the git terminal window, `cd` to the storage-table-java-getting-started folder.</span></span>

    ```
    cd "C:\git-samples\storage-table-node-getting-started"
    ```

2. <span data-ttu-id="8e7b4-140">Run the following command to install the [azure], [node-uuid], [nconf] and [async] modules locally as well as to save an entry for them to the package.json file</span><span class="sxs-lookup"><span data-stu-id="8e7b4-140">Run the following command to install the [azure], [node-uuid], [nconf] and [async] modules locally as well as to save an entry for them to the package.json file</span></span>

   ```
   npm install azure-storage node-uuid async nconf --save
   ```

2. <span data-ttu-id="8e7b4-141">In the git terminal window, run the following commands to run start the Node application.</span><span class="sxs-lookup"><span data-stu-id="8e7b4-141">In the git terminal window, run the following commands to run start the Node application.</span></span>

    ```
    node ./tableSample.js 
    ```

    <span data-ttu-id="8e7b4-142">The console window displays the table data being added to the new table database in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="8e7b4-142">The console window displays the table data being added to the new table database in Azure Cosmos DB.</span></span>

    <span data-ttu-id="8e7b4-143">You can now go back to Data Explorer and see query, modify, and work with this new data.</span><span class="sxs-lookup"><span data-stu-id="8e7b4-143">You can now go back to Data Explorer and see query, modify, and work with this new data.</span></span> 

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="8e7b4-144">Review SLAs in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="8e7b4-144">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="8e7b4-145">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="8e7b4-145">Clean up resources</span></span>

[!INCLUDE [cosmosdb-delete-resource-group](../../includes/cosmos-db-delete-resource-group.md)]

## <a name="next-steps"></a><span data-ttu-id="8e7b4-146">Next steps</span><span class="sxs-lookup"><span data-stu-id="8e7b4-146">Next steps</span></span>

<span data-ttu-id="8e7b4-147">In this quickstart, you've learned how to create an Azure Cosmos DB account, create a table using the Data Explorer, and run an app.</span><span class="sxs-lookup"><span data-stu-id="8e7b4-147">In this quickstart, you've learned how to create an Azure Cosmos DB account, create a table using the Data Explorer, and run an app.</span></span>  <span data-ttu-id="8e7b4-148">Now you can query your data using the Table API.</span><span class="sxs-lookup"><span data-stu-id="8e7b4-148">Now you can query your data using the Table API.</span></span>  

> [!div class="nextstepaction"]
> [Import table data to the Table API](table-import.md)
