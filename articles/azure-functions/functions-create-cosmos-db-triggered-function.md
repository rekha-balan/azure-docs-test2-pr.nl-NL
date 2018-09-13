---
title: Create a function triggered by Azure Cosmos DB | Microsoft Docs
description: Use Azure Functions to create a serverless function that is invoked when data is added to a database in Azure Cosmos DB.
services: azure-functions
documentationcenter: na
author: ggailey777
manager: jeconnoc
ms.assetid: bc497d71-75e7-47b1-babd-a060a664adca
ms.service: azure-functions; cosmos-db
ms.devlang: multiple
ms.topic: quickstart
ms.date: 03/27/2018
ms.author: glenga
ms.custom: cc996988-fb4f-47
ms.openlocfilehash: 5ae81824c2f35dd2ad26d64f3a343fecc549d805
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865695"
---
# <a name="create-a-function-triggered-by-azure-cosmos-db"></a><span data-ttu-id="26fd6-103">Create a function triggered by Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="26fd6-103">Create a function triggered by Azure Cosmos DB</span></span>

<span data-ttu-id="26fd6-104">Learn how to create a function triggered when data is added to or changed in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="26fd6-104">Learn how to create a function triggered when data is added to or changed in Azure Cosmos DB.</span></span> <span data-ttu-id="26fd6-105">To learn more about Azure Cosmos DB, see [Azure Cosmos DB: Serverless database computing using Azure Functions](..\cosmos-db\serverless-computing-database.md).</span><span class="sxs-lookup"><span data-stu-id="26fd6-105">To learn more about Azure Cosmos DB, see [Azure Cosmos DB: Serverless database computing using Azure Functions](..\cosmos-db\serverless-computing-database.md).</span></span>

![View message in the logs.](./media/functions-create-cosmos-db-triggered-function/quickstart-completed.png)

## <a name="prerequisites"></a><span data-ttu-id="26fd6-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="26fd6-107">Prerequisites</span></span>

<span data-ttu-id="26fd6-108">To complete this tutorial:</span><span class="sxs-lookup"><span data-stu-id="26fd6-108">To complete this tutorial:</span></span>

+ <span data-ttu-id="26fd6-109">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="26fd6-109">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

> [!NOTE]
> [!INCLUDE [SQL API support only](../../includes/functions-cosmosdb-sqlapi-note.md)]

## <a name="create-an-azure-function-app"></a><span data-ttu-id="26fd6-110">Create an Azure Function app</span><span class="sxs-lookup"><span data-stu-id="26fd6-110">Create an Azure Function app</span></span>

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

<span data-ttu-id="26fd6-111">Next, you create a function in the new function app.</span><span class="sxs-lookup"><span data-stu-id="26fd6-111">Next, you create a function in the new function app.</span></span>

<a name="create-function"></a>

## <a name="create-azure-cosmos-db-trigger"></a><span data-ttu-id="26fd6-112">Create Azure Cosmos DB trigger</span><span class="sxs-lookup"><span data-stu-id="26fd6-112">Create Azure Cosmos DB trigger</span></span>

1. <span data-ttu-id="26fd6-113">Expand your function app and click the **+** button next to **Functions**.</span><span class="sxs-lookup"><span data-stu-id="26fd6-113">Expand your function app and click the **+** button next to **Functions**.</span></span> <span data-ttu-id="26fd6-114">If this is the first function in your function app, select **Custom function**.</span><span class="sxs-lookup"><span data-stu-id="26fd6-114">If this is the first function in your function app, select **Custom function**.</span></span> <span data-ttu-id="26fd6-115">This displays the complete set of function templates.</span><span class="sxs-lookup"><span data-stu-id="26fd6-115">This displays the complete set of function templates.</span></span>

    ![Functions quickstart page in the Azure portal](./media/functions-create-cosmos-db-triggered-function/add-first-function.png)

2. <span data-ttu-id="26fd6-117">In the search field, type `cosmos` and then choose your desired language for the Azure Cosmos DB trigger template.</span><span class="sxs-lookup"><span data-stu-id="26fd6-117">In the search field, type `cosmos` and then choose your desired language for the Azure Cosmos DB trigger template.</span></span>

    ![Choose the Azure Cosmos DB trigger](./media/functions-create-cosmos-db-triggered-function/select-cosmos-db-trigger-portal.png)

3. <span data-ttu-id="26fd6-119">Configure the new trigger with the settings as specified in the table below the image.</span><span class="sxs-lookup"><span data-stu-id="26fd6-119">Configure the new trigger with the settings as specified in the table below the image.</span></span>

    ![Create the Azure Cosmos DB triggered function](./media/functions-create-cosmos-db-triggered-function/functions-cosmosdb-trigger-settings.png)
    
    | <span data-ttu-id="26fd6-121">Setting</span><span class="sxs-lookup"><span data-stu-id="26fd6-121">Setting</span></span>      | <span data-ttu-id="26fd6-122">Suggested value</span><span class="sxs-lookup"><span data-stu-id="26fd6-122">Suggested value</span></span>  | <span data-ttu-id="26fd6-123">Description</span><span class="sxs-lookup"><span data-stu-id="26fd6-123">Description</span></span>                                |
    | ------------ | ---------------- | ------------------------------------------ |
    | <span data-ttu-id="26fd6-124">**Name**</span><span class="sxs-lookup"><span data-stu-id="26fd6-124">**Name**</span></span> | <span data-ttu-id="26fd6-125">Default</span><span class="sxs-lookup"><span data-stu-id="26fd6-125">Default</span></span> | <span data-ttu-id="26fd6-126">Use the default function name suggested by the template.</span><span class="sxs-lookup"><span data-stu-id="26fd6-126">Use the default function name suggested by the template.</span></span> |
    | <span data-ttu-id="26fd6-127">**Collection name**</span><span class="sxs-lookup"><span data-stu-id="26fd6-127">**Collection name**</span></span> | <span data-ttu-id="26fd6-128">Items</span><span class="sxs-lookup"><span data-stu-id="26fd6-128">Items</span></span> | <span data-ttu-id="26fd6-129">Name of collection to be monitored.</span><span class="sxs-lookup"><span data-stu-id="26fd6-129">Name of collection to be monitored.</span></span> |
    | <span data-ttu-id="26fd6-130">**Create lease collection if it doesn't exist**</span><span class="sxs-lookup"><span data-stu-id="26fd6-130">**Create lease collection if it doesn't exist**</span></span> | <span data-ttu-id="26fd6-131">Checked</span><span class="sxs-lookup"><span data-stu-id="26fd6-131">Checked</span></span> | <span data-ttu-id="26fd6-132">The collection doesn't already exist, so create it.</span><span class="sxs-lookup"><span data-stu-id="26fd6-132">The collection doesn't already exist, so create it.</span></span> |
    | <span data-ttu-id="26fd6-133">**Database name**</span><span class="sxs-lookup"><span data-stu-id="26fd6-133">**Database name**</span></span> | <span data-ttu-id="26fd6-134">Tasks</span><span class="sxs-lookup"><span data-stu-id="26fd6-134">Tasks</span></span> | <span data-ttu-id="26fd6-135">Name of database with the collection to be monitored.</span><span class="sxs-lookup"><span data-stu-id="26fd6-135">Name of database with the collection to be monitored.</span></span> |

4. <span data-ttu-id="26fd6-136">Select **New** next to the **Azure Cosmos DB account connection** label, and choose an existing Cosmos DB account or **+ Create new**.</span><span class="sxs-lookup"><span data-stu-id="26fd6-136">Select **New** next to the **Azure Cosmos DB account connection** label, and choose an existing Cosmos DB account or **+ Create new**.</span></span> 
 
    ![Configure Azure Cosmos DB connection](./media/functions-create-cosmos-db-triggered-function/functions-create-CosmosDB.png)

6. <span data-ttu-id="26fd6-138">When creating a new Cosmos DB account, use the **New account** settings as specified in the table.</span><span class="sxs-lookup"><span data-stu-id="26fd6-138">When creating a new Cosmos DB account, use the **New account** settings as specified in the table.</span></span>

    | <span data-ttu-id="26fd6-139">Setting</span><span class="sxs-lookup"><span data-stu-id="26fd6-139">Setting</span></span>      | <span data-ttu-id="26fd6-140">Suggested value</span><span class="sxs-lookup"><span data-stu-id="26fd6-140">Suggested value</span></span>  | <span data-ttu-id="26fd6-141">Description</span><span class="sxs-lookup"><span data-stu-id="26fd6-141">Description</span></span>                                |
    | ------------ | ---------------- | ------------------------------------------ |
    | <span data-ttu-id="26fd6-142">**ID**</span><span class="sxs-lookup"><span data-stu-id="26fd6-142">**ID**</span></span> | <span data-ttu-id="26fd6-143">Name of database</span><span class="sxs-lookup"><span data-stu-id="26fd6-143">Name of database</span></span> | <span data-ttu-id="26fd6-144">Unique ID for the Azure Cosmos DB database</span><span class="sxs-lookup"><span data-stu-id="26fd6-144">Unique ID for the Azure Cosmos DB database</span></span>  |
    | <span data-ttu-id="26fd6-145">**API**</span><span class="sxs-lookup"><span data-stu-id="26fd6-145">**API**</span></span> | <span data-ttu-id="26fd6-146">SQL</span><span class="sxs-lookup"><span data-stu-id="26fd6-146">SQL</span></span> | <span data-ttu-id="26fd6-147">This topic uses the SQL API.</span><span class="sxs-lookup"><span data-stu-id="26fd6-147">This topic uses the SQL API.</span></span>  |
    | <span data-ttu-id="26fd6-148">**Subscription**</span><span class="sxs-lookup"><span data-stu-id="26fd6-148">**Subscription**</span></span> | <span data-ttu-id="26fd6-149">Azure Subscription</span><span class="sxs-lookup"><span data-stu-id="26fd6-149">Azure Subscription</span></span> | <span data-ttu-id="26fd6-150">The subscription under which this new Cosmos DB account is created.</span><span class="sxs-lookup"><span data-stu-id="26fd6-150">The subscription under which this new Cosmos DB account is created.</span></span>  |
    | <span data-ttu-id="26fd6-151">**Resource Group**</span><span class="sxs-lookup"><span data-stu-id="26fd6-151">**Resource Group**</span></span> | <span data-ttu-id="26fd6-152">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="26fd6-152">myResourceGroup</span></span> |  <span data-ttu-id="26fd6-153">Use the existing resource group that contains your function app.</span><span class="sxs-lookup"><span data-stu-id="26fd6-153">Use the existing resource group that contains your function app.</span></span> |
    | <span data-ttu-id="26fd6-154">**Location**</span><span class="sxs-lookup"><span data-stu-id="26fd6-154">**Location**</span></span>  | <span data-ttu-id="26fd6-155">WestEurope</span><span class="sxs-lookup"><span data-stu-id="26fd6-155">WestEurope</span></span> | <span data-ttu-id="26fd6-156">Select a location near to either your function app or to other apps that use the stored documents.</span><span class="sxs-lookup"><span data-stu-id="26fd6-156">Select a location near to either your function app or to other apps that use the stored documents.</span></span>  |

6. <span data-ttu-id="26fd6-157">Click **OK** to create the database.</span><span class="sxs-lookup"><span data-stu-id="26fd6-157">Click **OK** to create the database.</span></span> <span data-ttu-id="26fd6-158">It may take a few minutes to create the database.</span><span class="sxs-lookup"><span data-stu-id="26fd6-158">It may take a few minutes to create the database.</span></span> <span data-ttu-id="26fd6-159">After the database is created, the database connection string is stored as a function app setting.</span><span class="sxs-lookup"><span data-stu-id="26fd6-159">After the database is created, the database connection string is stored as a function app setting.</span></span> <span data-ttu-id="26fd6-160">The name of this app setting is inserted in **Azure Cosmos DB account connection**.</span><span class="sxs-lookup"><span data-stu-id="26fd6-160">The name of this app setting is inserted in **Azure Cosmos DB account connection**.</span></span> 

7. <span data-ttu-id="26fd6-161">Click **Create** to create your Azure Cosmos DB triggered function.</span><span class="sxs-lookup"><span data-stu-id="26fd6-161">Click **Create** to create your Azure Cosmos DB triggered function.</span></span> <span data-ttu-id="26fd6-162">After the function is created, the template-based function code is displayed.</span><span class="sxs-lookup"><span data-stu-id="26fd6-162">After the function is created, the template-based function code is displayed.</span></span>  

    ![Cosmos DB function template in C#](./media/functions-create-cosmos-db-triggered-function/function-cosmosdb-template.png)

    <span data-ttu-id="26fd6-164">This function template writes the number of documents and the first document ID to the logs.</span><span class="sxs-lookup"><span data-stu-id="26fd6-164">This function template writes the number of documents and the first document ID to the logs.</span></span> 

<span data-ttu-id="26fd6-165">Next, you connect to your Azure Cosmos DB account and create the **Tasks** collection in the database.</span><span class="sxs-lookup"><span data-stu-id="26fd6-165">Next, you connect to your Azure Cosmos DB account and create the **Tasks** collection in the database.</span></span> 

## <a name="create-the-items-collection"></a><span data-ttu-id="26fd6-166">Create the Items collection</span><span class="sxs-lookup"><span data-stu-id="26fd6-166">Create the Items collection</span></span>

1. <span data-ttu-id="26fd6-167">Open a second instance of the [Azure portal](https://portal.azure.com) in a new tab in the browser.</span><span class="sxs-lookup"><span data-stu-id="26fd6-167">Open a second instance of the [Azure portal](https://portal.azure.com) in a new tab in the browser.</span></span> 

2. <span data-ttu-id="26fd6-168">On the left side of the portal, expand the icon bar, type `cosmos` in the search field, and select **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="26fd6-168">On the left side of the portal, expand the icon bar, type `cosmos` in the search field, and select **Azure Cosmos DB**.</span></span>

    ![Search for the Azure Cosmos DB service](./media/functions-create-cosmos-db-triggered-function/functions-search-cosmos-db.png)

2. <span data-ttu-id="26fd6-170">Choose your Azure Cosmos DB account, then select the **Data Explorer**.</span><span class="sxs-lookup"><span data-stu-id="26fd6-170">Choose your Azure Cosmos DB account, then select the **Data Explorer**.</span></span> 
 
3. <span data-ttu-id="26fd6-171">In **Collections**, choose **taskDatabase** and select **New Collection**.</span><span class="sxs-lookup"><span data-stu-id="26fd6-171">In **Collections**, choose **taskDatabase** and select **New Collection**.</span></span>

    ![Create a collection](./media/functions-create-cosmos-db-triggered-function/cosmosdb-create-collection.png)

4. <span data-ttu-id="26fd6-173">In **Add Collection**, use the settings shown in the table below the image.</span><span class="sxs-lookup"><span data-stu-id="26fd6-173">In **Add Collection**, use the settings shown in the table below the image.</span></span> 
 
    ![Define the taskCollection](./media/functions-create-cosmos-db-triggered-function/cosmosdb-create-collection2.png)
 
    | <span data-ttu-id="26fd6-175">Setting</span><span class="sxs-lookup"><span data-stu-id="26fd6-175">Setting</span></span>|<span data-ttu-id="26fd6-176">Suggested value</span><span class="sxs-lookup"><span data-stu-id="26fd6-176">Suggested value</span></span>|<span data-ttu-id="26fd6-177">Description</span><span class="sxs-lookup"><span data-stu-id="26fd6-177">Description</span></span> |
    | ---|---|--- |
    | <span data-ttu-id="26fd6-178">**Database ID**</span><span class="sxs-lookup"><span data-stu-id="26fd6-178">**Database ID**</span></span> | <span data-ttu-id="26fd6-179">Tasks</span><span class="sxs-lookup"><span data-stu-id="26fd6-179">Tasks</span></span> |<span data-ttu-id="26fd6-180">The name for your new database.</span><span class="sxs-lookup"><span data-stu-id="26fd6-180">The name for your new database.</span></span> <span data-ttu-id="26fd6-181">This must match the name defined in your function binding.</span><span class="sxs-lookup"><span data-stu-id="26fd6-181">This must match the name defined in your function binding.</span></span> |
    | <span data-ttu-id="26fd6-182">**Collection ID**</span><span class="sxs-lookup"><span data-stu-id="26fd6-182">**Collection ID**</span></span> | <span data-ttu-id="26fd6-183">Items</span><span class="sxs-lookup"><span data-stu-id="26fd6-183">Items</span></span> | <span data-ttu-id="26fd6-184">The name for the new collection.</span><span class="sxs-lookup"><span data-stu-id="26fd6-184">The name for the new collection.</span></span> <span data-ttu-id="26fd6-185">This must match the name defined in your function binding.</span><span class="sxs-lookup"><span data-stu-id="26fd6-185">This must match the name defined in your function binding.</span></span>  |
    | <span data-ttu-id="26fd6-186">**Storage capacity**</span><span class="sxs-lookup"><span data-stu-id="26fd6-186">**Storage capacity**</span></span> | <span data-ttu-id="26fd6-187">Fixed (10 GB)</span><span class="sxs-lookup"><span data-stu-id="26fd6-187">Fixed (10 GB)</span></span>|<span data-ttu-id="26fd6-188">Use the default value.</span><span class="sxs-lookup"><span data-stu-id="26fd6-188">Use the default value.</span></span> <span data-ttu-id="26fd6-189">This value is the storage capacity of the database.</span><span class="sxs-lookup"><span data-stu-id="26fd6-189">This value is the storage capacity of the database.</span></span> |
    | <span data-ttu-id="26fd6-190">**Throughput**</span><span class="sxs-lookup"><span data-stu-id="26fd6-190">**Throughput**</span></span> |<span data-ttu-id="26fd6-191">400 RU</span><span class="sxs-lookup"><span data-stu-id="26fd6-191">400 RU</span></span>| <span data-ttu-id="26fd6-192">Use the default value.</span><span class="sxs-lookup"><span data-stu-id="26fd6-192">Use the default value.</span></span> <span data-ttu-id="26fd6-193">If you want to reduce latency, you can scale up the throughput later.</span><span class="sxs-lookup"><span data-stu-id="26fd6-193">If you want to reduce latency, you can scale up the throughput later.</span></span> |
    | <span data-ttu-id="26fd6-194">**[Partition key](../cosmos-db/partition-data.md#best-practices-when-choosing-a-partition-key)**</span><span class="sxs-lookup"><span data-stu-id="26fd6-194">**[Partition key](../cosmos-db/partition-data.md#best-practices-when-choosing-a-partition-key)**</span></span> | <span data-ttu-id="26fd6-195">/category</span><span class="sxs-lookup"><span data-stu-id="26fd6-195">/category</span></span>|<span data-ttu-id="26fd6-196">A partition key that distributes data evenly to each partition.</span><span class="sxs-lookup"><span data-stu-id="26fd6-196">A partition key that distributes data evenly to each partition.</span></span> <span data-ttu-id="26fd6-197">Selecting the correct partition key is important in creating a performant collection.</span><span class="sxs-lookup"><span data-stu-id="26fd6-197">Selecting the correct partition key is important in creating a performant collection.</span></span> | 

1. <span data-ttu-id="26fd6-198">Click **OK** to create the **Tasks** collection.</span><span class="sxs-lookup"><span data-stu-id="26fd6-198">Click **OK** to create the **Tasks** collection.</span></span> <span data-ttu-id="26fd6-199">It may take a short time for the collection to get created.</span><span class="sxs-lookup"><span data-stu-id="26fd6-199">It may take a short time for the collection to get created.</span></span>

<span data-ttu-id="26fd6-200">After the collection specified in the function binding exists, you can test the function by adding documents to this new collection.</span><span class="sxs-lookup"><span data-stu-id="26fd6-200">After the collection specified in the function binding exists, you can test the function by adding documents to this new collection.</span></span>

## <a name="test-the-function"></a><span data-ttu-id="26fd6-201">Test the function</span><span class="sxs-lookup"><span data-stu-id="26fd6-201">Test the function</span></span>

1. <span data-ttu-id="26fd6-202">Expand the new **taskCollection** collection in Data Explorer, choose **Documents**, then select **New Document**.</span><span class="sxs-lookup"><span data-stu-id="26fd6-202">Expand the new **taskCollection** collection in Data Explorer, choose **Documents**, then select **New Document**.</span></span>

    ![Create a document in taskCollection](./media/functions-create-cosmos-db-triggered-function/create-document-in-collection.png)

2. <span data-ttu-id="26fd6-204">Replace the contents of the new document with the following content, then choose **Save**.</span><span class="sxs-lookup"><span data-stu-id="26fd6-204">Replace the contents of the new document with the following content, then choose **Save**.</span></span>

        {
            "id": "task1",
            "category": "general",
            "description": "some task"
        }

1. <span data-ttu-id="26fd6-205">Switch to the first browser tab that contains your function in the portal.</span><span class="sxs-lookup"><span data-stu-id="26fd6-205">Switch to the first browser tab that contains your function in the portal.</span></span> <span data-ttu-id="26fd6-206">Expand the function logs and verify that the new document has triggered the function.</span><span class="sxs-lookup"><span data-stu-id="26fd6-206">Expand the function logs and verify that the new document has triggered the function.</span></span> <span data-ttu-id="26fd6-207">See that the `task1` document ID value is written to the logs.</span><span class="sxs-lookup"><span data-stu-id="26fd6-207">See that the `task1` document ID value is written to the logs.</span></span> 

    ![View message in the logs.](./media/functions-create-cosmos-db-triggered-function/functions-cosmosdb-trigger-view-logs.png)

4. <span data-ttu-id="26fd6-209">(Optional) Go back to your document, make a change, and click **Update**.</span><span class="sxs-lookup"><span data-stu-id="26fd6-209">(Optional) Go back to your document, make a change, and click **Update**.</span></span> <span data-ttu-id="26fd6-210">Then, go back to the function logs and verify that the update has also triggered the function.</span><span class="sxs-lookup"><span data-stu-id="26fd6-210">Then, go back to the function logs and verify that the update has also triggered the function.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="26fd6-211">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="26fd6-211">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="26fd6-212">Next steps</span><span class="sxs-lookup"><span data-stu-id="26fd6-212">Next steps</span></span>

<span data-ttu-id="26fd6-213">You have created a function that runs when a document is added or modified in your Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="26fd6-213">You have created a function that runs when a document is added or modified in your Azure Cosmos DB.</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="26fd6-214">For more information about Azure Cosmos DB triggers, see [Azure Cosmos DB bindings for Azure Functions](functions-bindings-cosmosdb.md).</span><span class="sxs-lookup"><span data-stu-id="26fd6-214">For more information about Azure Cosmos DB triggers, see [Azure Cosmos DB bindings for Azure Functions](functions-bindings-cosmosdb.md).</span></span>
