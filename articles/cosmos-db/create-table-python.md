---
title: 'Quickstart: Table API with Python - Azure Cosmos DB | Microsoft Docs'
description: This quickstart shows how to use the Azure Cosmos DB Table API to create an application with the Azure portal and Python
services: cosmos-db
author: SnehaGunda
manager: kfile
ms.service: cosmos-db
ms.component: cosmosdb-table
ms.devlang: python
ms.topic: quickstart
ms.date: 04/10/2018
ms.author: sngun
ms.custom: mvc
ms.openlocfilehash: 614e22cbbb6a94d9b148b29474a5fc82c3f0fef4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868496"
---
# <a name="quickstart-build-a-table-api-app-with-python-and-azure-cosmos-db"></a><span data-ttu-id="923fa-103">Quickstart: Build a Table API app with Python and Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="923fa-103">Quickstart: Build a Table API app with Python and Azure Cosmos DB</span></span>

> [!div class="op_single_selector"]
> * [.NET](create-table-dotnet.md)
> * [Java](create-table-java.md)
> * [Node.js](create-table-nodejs.md)
> * [Python](create-table-python.md)
> 

<span data-ttu-id="923fa-108">This quickstart shows how to use Python and the Azure Cosmos DB [Table API](table-introduction.md) to build an app by cloning an example from GitHub.</span><span class="sxs-lookup"><span data-stu-id="923fa-108">This quickstart shows how to use Python and the Azure Cosmos DB [Table API](table-introduction.md) to build an app by cloning an example from GitHub.</span></span> <span data-ttu-id="923fa-109">This quickstart also shows you how to create an Azure Cosmos DB account and how to use Data Explorer to create tables and entities in the web-based Azure portal.</span><span class="sxs-lookup"><span data-stu-id="923fa-109">This quickstart also shows you how to create an Azure Cosmos DB account and how to use Data Explorer to create tables and entities in the web-based Azure portal.</span></span>

<span data-ttu-id="923fa-110">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span><span class="sxs-lookup"><span data-stu-id="923fa-110">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="923fa-111">You can quickly create and query document, key/value, wide-column, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="923fa-111">You can quickly create and query document, key/value, wide-column, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="923fa-112">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="923fa-112">Prerequisites</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]
[!INCLUDE [cosmos-db-emulator-docdb-api](../../includes/cosmos-db-emulator-docdb-api.md)]

<span data-ttu-id="923fa-113">In addition:</span><span class="sxs-lookup"><span data-stu-id="923fa-113">In addition:</span></span>

* <span data-ttu-id="923fa-114">If you don’t already have Visual Studio 2017 installed, you can download and use the **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="923fa-114">If you don’t already have Visual Studio 2017 installed, you can download and use the **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="923fa-115">Make sure that you select the **Azure development** and **Python development** workloads during the Visual Studio setup.</span><span class="sxs-lookup"><span data-stu-id="923fa-115">Make sure that you select the **Azure development** and **Python development** workloads during the Visual Studio setup.</span></span>
* <span data-ttu-id="923fa-116">Also select the Python 2 option in the **Python development** workload, or download Python 2.7 from [python.org](https://www.python.org/downloads/release/python-2712/).</span><span class="sxs-lookup"><span data-stu-id="923fa-116">Also select the Python 2 option in the **Python development** workload, or download Python 2.7 from [python.org](https://www.python.org/downloads/release/python-2712/).</span></span>

## <a name="create-a-database-account"></a><span data-ttu-id="923fa-117">Create a database account</span><span class="sxs-lookup"><span data-stu-id="923fa-117">Create a database account</span></span>

> [!IMPORTANT] 
> You need to create a new Table API account to work with the generally available Table API SDKs. Table API accounts created during preview are not supported by the generally available SDKs.
>

[!INCLUDE [cosmos-db-create-dbaccount-table](../../includes/cosmos-db-create-dbaccount-table.md)]

## <a name="add-a-table"></a><span data-ttu-id="923fa-120">Add a table</span><span class="sxs-lookup"><span data-stu-id="923fa-120">Add a table</span></span>

[!INCLUDE [cosmos-db-create-table](../../includes/cosmos-db-create-table.md)]

## <a name="add-sample-data"></a><span data-ttu-id="923fa-121">Add sample data</span><span class="sxs-lookup"><span data-stu-id="923fa-121">Add sample data</span></span>

[!INCLUDE [cosmos-db-create-table-add-sample-data](../../includes/cosmos-db-create-table-add-sample-data.md)]

## <a name="clone-the-sample-application"></a><span data-ttu-id="923fa-122">Clone the sample application</span><span class="sxs-lookup"><span data-stu-id="923fa-122">Clone the sample application</span></span>

<span data-ttu-id="923fa-123">Now let's clone a Table app from github, set the connection string, and run it.</span><span class="sxs-lookup"><span data-stu-id="923fa-123">Now let's clone a Table app from github, set the connection string, and run it.</span></span> <span data-ttu-id="923fa-124">You'll see how easy it is to work with data programmatically.</span><span class="sxs-lookup"><span data-stu-id="923fa-124">You'll see how easy it is to work with data programmatically.</span></span> 

1. <span data-ttu-id="923fa-125">Open a command prompt, create a new folder named git-samples, then close the command prompt.</span><span class="sxs-lookup"><span data-stu-id="923fa-125">Open a command prompt, create a new folder named git-samples, then close the command prompt.</span></span>

    ```bash
    md "C:\git-samples"
    ```

2. <span data-ttu-id="923fa-126">Open a git terminal window, such as git bash, and use the `cd` command to change to the new folder to install the sample app.</span><span class="sxs-lookup"><span data-stu-id="923fa-126">Open a git terminal window, such as git bash, and use the `cd` command to change to the new folder to install the sample app.</span></span>

    ```bash
    cd "C:\git-samples"
    ```

3. <span data-ttu-id="923fa-127">Run the following command to clone the sample repository.</span><span class="sxs-lookup"><span data-stu-id="923fa-127">Run the following command to clone the sample repository.</span></span> <span data-ttu-id="923fa-128">This command creates a copy of the sample app on your computer.</span><span class="sxs-lookup"><span data-stu-id="923fa-128">This command creates a copy of the sample app on your computer.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/storage-python-getting-started.git
    ```

3. <span data-ttu-id="923fa-129">Then open the solution file in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="923fa-129">Then open the solution file in Visual Studio.</span></span> 

## <a name="update-your-connection-string"></a><span data-ttu-id="923fa-130">Update your connection string</span><span class="sxs-lookup"><span data-stu-id="923fa-130">Update your connection string</span></span>

<span data-ttu-id="923fa-131">Now go back to the Azure portal to get your connection string information and copy it into the app.</span><span class="sxs-lookup"><span data-stu-id="923fa-131">Now go back to the Azure portal to get your connection string information and copy it into the app.</span></span> <span data-ttu-id="923fa-132">This enables your app to communicate with your hosted database.</span><span class="sxs-lookup"><span data-stu-id="923fa-132">This enables your app to communicate with your hosted database.</span></span> 

1. <span data-ttu-id="923fa-133">In the [Azure portal](http://portal.azure.com/), click **Connection String**.</span><span class="sxs-lookup"><span data-stu-id="923fa-133">In the [Azure portal](http://portal.azure.com/), click **Connection String**.</span></span> 

    ![View and copy the CONNECTION STRING in the Connection String pane](./media/create-table-python/connection-string.png)

2. <span data-ttu-id="923fa-135">Copy the ACCOUNT NAME using the button on the right side.</span><span class="sxs-lookup"><span data-stu-id="923fa-135">Copy the ACCOUNT NAME using the button on the right side.</span></span>

3. <span data-ttu-id="923fa-136">Open the config.py file, and paste the ACCOUNT NAME from the portal into the STORAGE_ACCOUNT_NAME value on line 19.</span><span class="sxs-lookup"><span data-stu-id="923fa-136">Open the config.py file, and paste the ACCOUNT NAME from the portal into the STORAGE_ACCOUNT_NAME value on line 19.</span></span>

4. <span data-ttu-id="923fa-137">Go back to the portal and copy the PRIMARY KEY.</span><span class="sxs-lookup"><span data-stu-id="923fa-137">Go back to the portal and copy the PRIMARY KEY.</span></span>

5. <span data-ttu-id="923fa-138">Paste the PRIMARY KEY from the portal into the STORAGE_ACCOUNT_KEY value on line 20.</span><span class="sxs-lookup"><span data-stu-id="923fa-138">Paste the PRIMARY KEY from the portal into the STORAGE_ACCOUNT_KEY value on line 20.</span></span>

3. <span data-ttu-id="923fa-139">Save the config.py file.</span><span class="sxs-lookup"><span data-stu-id="923fa-139">Save the config.py file.</span></span>

## <a name="run-the-app"></a><span data-ttu-id="923fa-140">Run the app</span><span class="sxs-lookup"><span data-stu-id="923fa-140">Run the app</span></span>

1. <span data-ttu-id="923fa-141">In Visual Studio, right-click on the project in **Solution Explorer**, select the current Python environment, then right click.</span><span class="sxs-lookup"><span data-stu-id="923fa-141">In Visual Studio, right-click on the project in **Solution Explorer**, select the current Python environment, then right click.</span></span>

2. <span data-ttu-id="923fa-142">Select Install Python Package, then type in **azure-storage-table**</span><span class="sxs-lookup"><span data-stu-id="923fa-142">Select Install Python Package, then type in **azure-storage-table**</span></span>

3. <span data-ttu-id="923fa-143">Run F5 to run the application.</span><span class="sxs-lookup"><span data-stu-id="923fa-143">Run F5 to run the application.</span></span> <span data-ttu-id="923fa-144">Your app displays in your browser.</span><span class="sxs-lookup"><span data-stu-id="923fa-144">Your app displays in your browser.</span></span> 

<span data-ttu-id="923fa-145">You can now go back to Data Explorer and see query, modify, and work with this new data.</span><span class="sxs-lookup"><span data-stu-id="923fa-145">You can now go back to Data Explorer and see query, modify, and work with this new data.</span></span> 

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="923fa-146">Review SLAs in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="923fa-146">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="923fa-147">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="923fa-147">Clean up resources</span></span>

[!INCLUDE [cosmosdb-delete-resource-group](../../includes/cosmos-db-delete-resource-group.md)]

## <a name="next-steps"></a><span data-ttu-id="923fa-148">Next steps</span><span class="sxs-lookup"><span data-stu-id="923fa-148">Next steps</span></span>

<span data-ttu-id="923fa-149">In this quickstart, you've learned how to create an Azure Cosmos DB account, create a table using the Data Explorer, and run an app.</span><span class="sxs-lookup"><span data-stu-id="923fa-149">In this quickstart, you've learned how to create an Azure Cosmos DB account, create a table using the Data Explorer, and run an app.</span></span>  <span data-ttu-id="923fa-150">Now you can query your data using the Table API.</span><span class="sxs-lookup"><span data-stu-id="923fa-150">Now you can query your data using the Table API.</span></span>  

> [!div class="nextstepaction"]
> [Import table data to the Table API](table-import.md)
