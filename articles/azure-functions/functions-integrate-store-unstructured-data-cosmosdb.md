---
title: Store unstructured data using Azure Cosmos DB and Functions | Microsoft Docs
description: Store unstructured data using Azure Functions and Cosmos DB
services: functions
documentationcenter: functions
author: ggailey777
manager: jeconnoc
keywords: azure functions, functions, event processing, Cosmos DB, dynamic compute, serverless architecture
ms.assetid: ''
ms.service: azure-functions
ms.devlang: csharp
ms.topic: quickstart
ms.date: 09/19/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: ddd9a3186e86b1b5bd24c0c99f5fcb18c456119a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868098"
---
# <a name="store-unstructured-data-using-azure-functions-and-azure-cosmos-db"></a><span data-ttu-id="b79a4-104">Store unstructured data using Azure Functions and Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="b79a4-104">Store unstructured data using Azure Functions and Azure Cosmos DB</span></span>

<span data-ttu-id="b79a4-105">[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) is a great way to store unstructured and JSON data.</span><span class="sxs-lookup"><span data-stu-id="b79a4-105">[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) is a great way to store unstructured and JSON data.</span></span> <span data-ttu-id="b79a4-106">Combined with Azure Functions, Cosmos DB makes storing data quick and easy with much less code than required for storing data in a relational database.</span><span class="sxs-lookup"><span data-stu-id="b79a4-106">Combined with Azure Functions, Cosmos DB makes storing data quick and easy with much less code than required for storing data in a relational database.</span></span>

> [!NOTE]
> <span data-ttu-id="b79a4-107">At this time, the Azure Cosmos DB trigger, input bindings, and output bindings work with SQL API and Graph API accounts only.</span><span class="sxs-lookup"><span data-stu-id="b79a4-107">At this time, the Azure Cosmos DB trigger, input bindings, and output bindings work with SQL API and Graph API accounts only.</span></span>

<span data-ttu-id="b79a4-108">In Azure Functions, input and output bindings provide a declarative way to connect to external service data from your function.</span><span class="sxs-lookup"><span data-stu-id="b79a4-108">In Azure Functions, input and output bindings provide a declarative way to connect to external service data from your function.</span></span> <span data-ttu-id="b79a4-109">In this topic, learn how to update an existing C# function to add an output binding that stores unstructured data in a Cosmos DB document.</span><span class="sxs-lookup"><span data-stu-id="b79a4-109">In this topic, learn how to update an existing C# function to add an output binding that stores unstructured data in a Cosmos DB document.</span></span> 

![Cosmos DB](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-cosmosdb.png)

## <a name="prerequisites"></a><span data-ttu-id="b79a4-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b79a4-111">Prerequisites</span></span>

<span data-ttu-id="b79a4-112">To complete this tutorial:</span><span class="sxs-lookup"><span data-stu-id="b79a4-112">To complete this tutorial:</span></span>

[!INCLUDE [Previous quickstart note](../../includes/functions-quickstart-previous-topics.md)]

## <a name="add-an-output-binding"></a><span data-ttu-id="b79a4-113">Add an output binding</span><span class="sxs-lookup"><span data-stu-id="b79a4-113">Add an output binding</span></span>

1. <span data-ttu-id="b79a4-114">Expand both your function app and your function.</span><span class="sxs-lookup"><span data-stu-id="b79a4-114">Expand both your function app and your function.</span></span>

1. <span data-ttu-id="b79a4-115">Select **Integrate** and **+ New Output**, which is at the top right of the page.</span><span class="sxs-lookup"><span data-stu-id="b79a4-115">Select **Integrate** and **+ New Output**, which is at the top right of the page.</span></span> <span data-ttu-id="b79a4-116">Choose **Azure Cosmos DB**, and click **Select**.</span><span class="sxs-lookup"><span data-stu-id="b79a4-116">Choose **Azure Cosmos DB**, and click **Select**.</span></span>

    ![Add a Cosmos DB output binding](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-integrate-tab-add-new-output-binding.png)

3. <span data-ttu-id="b79a4-118">Use the **Azure Cosmos DB output** settings as specified in the table:</span><span class="sxs-lookup"><span data-stu-id="b79a4-118">Use the **Azure Cosmos DB output** settings as specified in the table:</span></span> 

    ![Configure Cosmos DB output binding](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-integrate-tab-configure-cosmosdb-binding.png)

    | <span data-ttu-id="b79a4-120">Setting</span><span class="sxs-lookup"><span data-stu-id="b79a4-120">Setting</span></span>      | <span data-ttu-id="b79a4-121">Suggested value</span><span class="sxs-lookup"><span data-stu-id="b79a4-121">Suggested value</span></span>  | <span data-ttu-id="b79a4-122">Description</span><span class="sxs-lookup"><span data-stu-id="b79a4-122">Description</span></span>                                |
    | ------------ | ---------------- | ------------------------------------------ |
    | <span data-ttu-id="b79a4-123">**Document parameter name**</span><span class="sxs-lookup"><span data-stu-id="b79a4-123">**Document parameter name**</span></span> | <span data-ttu-id="b79a4-124">taskDocument</span><span class="sxs-lookup"><span data-stu-id="b79a4-124">taskDocument</span></span> | <span data-ttu-id="b79a4-125">Name that refers to the Cosmos DB object in code.</span><span class="sxs-lookup"><span data-stu-id="b79a4-125">Name that refers to the Cosmos DB object in code.</span></span> |
    | <span data-ttu-id="b79a4-126">**Database name**</span><span class="sxs-lookup"><span data-stu-id="b79a4-126">**Database name**</span></span> | <span data-ttu-id="b79a4-127">taskDatabase</span><span class="sxs-lookup"><span data-stu-id="b79a4-127">taskDatabase</span></span> | <span data-ttu-id="b79a4-128">Name of database to save documents.</span><span class="sxs-lookup"><span data-stu-id="b79a4-128">Name of database to save documents.</span></span> |
    | <span data-ttu-id="b79a4-129">**Collection name**</span><span class="sxs-lookup"><span data-stu-id="b79a4-129">**Collection name**</span></span> | <span data-ttu-id="b79a4-130">TaskCollection</span><span class="sxs-lookup"><span data-stu-id="b79a4-130">TaskCollection</span></span> | <span data-ttu-id="b79a4-131">Name of the database collection.</span><span class="sxs-lookup"><span data-stu-id="b79a4-131">Name of the database collection.</span></span> |
    | <span data-ttu-id="b79a4-132">**If true, creates the Cosmos DB database and collection**</span><span class="sxs-lookup"><span data-stu-id="b79a4-132">**If true, creates the Cosmos DB database and collection**</span></span> | <span data-ttu-id="b79a4-133">Checked</span><span class="sxs-lookup"><span data-stu-id="b79a4-133">Checked</span></span> | <span data-ttu-id="b79a4-134">The collection doesn't already exist, so create it.</span><span class="sxs-lookup"><span data-stu-id="b79a4-134">The collection doesn't already exist, so create it.</span></span> |

4. <span data-ttu-id="b79a4-135">Select **New** next to the **Azure Cosmos DB document connection** label, and select **+ Create new**.</span><span class="sxs-lookup"><span data-stu-id="b79a4-135">Select **New** next to the **Azure Cosmos DB document connection** label, and select **+ Create new**.</span></span> 

5. <span data-ttu-id="b79a4-136">Use the **New account** settings as specified in the table:</span><span class="sxs-lookup"><span data-stu-id="b79a4-136">Use the **New account** settings as specified in the table:</span></span> 

    ![Configure Cosmos DB connection](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-create-CosmosDB.png)

    | <span data-ttu-id="b79a4-138">Setting</span><span class="sxs-lookup"><span data-stu-id="b79a4-138">Setting</span></span>      | <span data-ttu-id="b79a4-139">Suggested value</span><span class="sxs-lookup"><span data-stu-id="b79a4-139">Suggested value</span></span>  | <span data-ttu-id="b79a4-140">Description</span><span class="sxs-lookup"><span data-stu-id="b79a4-140">Description</span></span>                                |
    | ------------ | ---------------- | ------------------------------------------ |
    | <span data-ttu-id="b79a4-141">**ID**</span><span class="sxs-lookup"><span data-stu-id="b79a4-141">**ID**</span></span> | <span data-ttu-id="b79a4-142">Name of database</span><span class="sxs-lookup"><span data-stu-id="b79a4-142">Name of database</span></span> | <span data-ttu-id="b79a4-143">Unique ID for the Azure Cosmos DB database</span><span class="sxs-lookup"><span data-stu-id="b79a4-143">Unique ID for the Azure Cosmos DB database</span></span>  |
    | <span data-ttu-id="b79a4-144">**API**</span><span class="sxs-lookup"><span data-stu-id="b79a4-144">**API**</span></span> | <span data-ttu-id="b79a4-145">SQL</span><span class="sxs-lookup"><span data-stu-id="b79a4-145">SQL</span></span> | <span data-ttu-id="b79a4-146">Select the SQL API.</span><span class="sxs-lookup"><span data-stu-id="b79a4-146">Select the SQL API.</span></span> <span data-ttu-id="b79a4-147">At this time, the Azure Cosmos DB trigger, input bindings, and output bindings work with SQL API and Graph API accounts only.</span><span class="sxs-lookup"><span data-stu-id="b79a4-147">At this time, the Azure Cosmos DB trigger, input bindings, and output bindings work with SQL API and Graph API accounts only.</span></span> |
    | <span data-ttu-id="b79a4-148">**Subscription**</span><span class="sxs-lookup"><span data-stu-id="b79a4-148">**Subscription**</span></span> | <span data-ttu-id="b79a4-149">Azure Subscription</span><span class="sxs-lookup"><span data-stu-id="b79a4-149">Azure Subscription</span></span> | <span data-ttu-id="b79a4-150">Azure Subscription</span><span class="sxs-lookup"><span data-stu-id="b79a4-150">Azure Subscription</span></span>  |
    | <span data-ttu-id="b79a4-151">**Resource Group**</span><span class="sxs-lookup"><span data-stu-id="b79a4-151">**Resource Group**</span></span> | <span data-ttu-id="b79a4-152">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="b79a4-152">myResourceGroup</span></span> |  <span data-ttu-id="b79a4-153">Use the existing resource group that contains your function app.</span><span class="sxs-lookup"><span data-stu-id="b79a4-153">Use the existing resource group that contains your function app.</span></span> |
    | <span data-ttu-id="b79a4-154">**Location**</span><span class="sxs-lookup"><span data-stu-id="b79a4-154">**Location**</span></span>  | <span data-ttu-id="b79a4-155">WestEurope</span><span class="sxs-lookup"><span data-stu-id="b79a4-155">WestEurope</span></span> | <span data-ttu-id="b79a4-156">Select a location near to either your function app or to other apps that use the stored documents.</span><span class="sxs-lookup"><span data-stu-id="b79a4-156">Select a location near to either your function app or to other apps that use the stored documents.</span></span>  |

6. <span data-ttu-id="b79a4-157">Click **OK** to create the database.</span><span class="sxs-lookup"><span data-stu-id="b79a4-157">Click **OK** to create the database.</span></span> <span data-ttu-id="b79a4-158">It may take a few minutes to create the database.</span><span class="sxs-lookup"><span data-stu-id="b79a4-158">It may take a few minutes to create the database.</span></span> <span data-ttu-id="b79a4-159">After the database is created, the database connection string is stored as a function app setting.</span><span class="sxs-lookup"><span data-stu-id="b79a4-159">After the database is created, the database connection string is stored as a function app setting.</span></span> <span data-ttu-id="b79a4-160">The name of this app setting is inserted in **Azure Cosmos DB account connection**.</span><span class="sxs-lookup"><span data-stu-id="b79a4-160">The name of this app setting is inserted in **Azure Cosmos DB account connection**.</span></span> 
 
8. <span data-ttu-id="b79a4-161">After the connection string is set, select **Save** to create the binding.</span><span class="sxs-lookup"><span data-stu-id="b79a4-161">After the connection string is set, select **Save** to create the binding.</span></span>

## <a name="update-the-function-code"></a><span data-ttu-id="b79a4-162">Update the function code</span><span class="sxs-lookup"><span data-stu-id="b79a4-162">Update the function code</span></span>

<span data-ttu-id="b79a4-163">Replace the existing C# function code with the following code:</span><span class="sxs-lookup"><span data-stu-id="b79a4-163">Replace the existing C# function code with the following code:</span></span>

```csharp
using System.Net;

public static HttpResponseMessage Run(HttpRequestMessage req, out object taskDocument, TraceWriter log)
{
    string name = req.GetQueryNameValuePairs()
        .FirstOrDefault(q => string.Compare(q.Key, "name", true) == 0)
        .Value;

    string task = req.GetQueryNameValuePairs()
        .FirstOrDefault(q => string.Compare(q.Key, "task", true) == 0)
        .Value;

    string duedate = req.GetQueryNameValuePairs()
        .FirstOrDefault(q => string.Compare(q.Key, "duedate", true) == 0)
        .Value;

    taskDocument = new {
        name = name,
        duedate = duedate.ToString(),
        task = task
    };

    if (name != "" && task != "") {
        return req.CreateResponse(HttpStatusCode.OK);
    }
    else {
        return req.CreateResponse(HttpStatusCode.BadRequest);
    }
}

```
<span data-ttu-id="b79a4-164">This code sample reads the HTTP Request query strings and assigns them to fields in the `taskDocument` object.</span><span class="sxs-lookup"><span data-stu-id="b79a4-164">This code sample reads the HTTP Request query strings and assigns them to fields in the `taskDocument` object.</span></span> <span data-ttu-id="b79a4-165">The `taskDocument` binding sends the object data from this binding parameter to be stored in the bound document database.</span><span class="sxs-lookup"><span data-stu-id="b79a4-165">The `taskDocument` binding sends the object data from this binding parameter to be stored in the bound document database.</span></span> <span data-ttu-id="b79a4-166">The database is created the first time the function runs.</span><span class="sxs-lookup"><span data-stu-id="b79a4-166">The database is created the first time the function runs.</span></span>

## <a name="test-the-function-and-database"></a><span data-ttu-id="b79a4-167">Test the function and database</span><span class="sxs-lookup"><span data-stu-id="b79a4-167">Test the function and database</span></span>

1. <span data-ttu-id="b79a4-168">Expand the right window and select **Test**.</span><span class="sxs-lookup"><span data-stu-id="b79a4-168">Expand the right window and select **Test**.</span></span> <span data-ttu-id="b79a4-169">Under **Query**, click **+ Add parameter** and add the following parameters to the query string:</span><span class="sxs-lookup"><span data-stu-id="b79a4-169">Under **Query**, click **+ Add parameter** and add the following parameters to the query string:</span></span>

    + `name`
    + `task`
    + `duedate`

2. <span data-ttu-id="b79a4-170">Click **Run** and verify that a 200 status is returned.</span><span class="sxs-lookup"><span data-stu-id="b79a4-170">Click **Run** and verify that a 200 status is returned.</span></span>

    ![Configure Cosmos DB output binding](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-test-function.png)

1. <span data-ttu-id="b79a4-172">On the left side of the Azure portal, expand the icon bar, type `cosmos` in the search field, and select **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="b79a4-172">On the left side of the Azure portal, expand the icon bar, type `cosmos` in the search field, and select **Azure Cosmos DB**.</span></span>

    ![Search for the Cosmos DB service](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-search-cosmos-db.png)

2. <span data-ttu-id="b79a4-174">Choose your Azure Cosmos DB account, then select the **Data Explorer**.</span><span class="sxs-lookup"><span data-stu-id="b79a4-174">Choose your Azure Cosmos DB account, then select the **Data Explorer**.</span></span> 

3. <span data-ttu-id="b79a4-175">Expand the **Collections** nodes, select the new document, and confirm that the document contains your query string values, along with some additional metadata.</span><span class="sxs-lookup"><span data-stu-id="b79a4-175">Expand the **Collections** nodes, select the new document, and confirm that the document contains your query string values, along with some additional metadata.</span></span> 

    ![Verify Cosmos DB entry](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-verify-cosmosdb-output.png)

<span data-ttu-id="b79a4-177">You have successfully added a binding to your HTTP trigger that stores unstructured data in a Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b79a4-177">You have successfully added a binding to your HTTP trigger that stores unstructured data in a Azure Cosmos DB.</span></span>

[!INCLUDE [Clean-up section](../../includes/clean-up-section-portal.md)]

## <a name="next-steps"></a><span data-ttu-id="b79a4-178">Next steps</span><span class="sxs-lookup"><span data-stu-id="b79a4-178">Next steps</span></span>

[!INCLUDE [functions-quickstart-next-steps](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="b79a4-179">For more information about binding to a Cosmos DB database, see [Azure Functions Cosmos DB bindings](functions-bindings-cosmosdb.md).</span><span class="sxs-lookup"><span data-stu-id="b79a4-179">For more information about binding to a Cosmos DB database, see [Azure Functions Cosmos DB bindings](functions-bindings-cosmosdb.md).</span></span>
