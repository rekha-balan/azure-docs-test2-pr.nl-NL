---
title: 'Quickstart: Table API with .NET - Azure Cosmos DB | Microsoft Docs'
description: This quickstart shows how to use the Azure Cosmos DB Table API to create an application with the Azure portal and .NET
services: cosmos-db
author: SnehaGunda
manager: kfile
ms.service: cosmos-db
ms.component: cosmosdb-table
ms.custom: quickstart connect, mvc
ms.devlang: dotnet
ms.topic: quickstart
ms.date: 08/17/2018
ms.author: sngun
ms.openlocfilehash: 9cda2c165d7d00ebb92907d54217a30d62df6c18
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871398"
---
# <a name="quickstart-build-a-table-api-app-with-net-and-azure-cosmos-db"></a><span data-ttu-id="59bbc-103">Quickstart: Build a Table API app with .NET and Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="59bbc-103">Quickstart: Build a Table API app with .NET and Azure Cosmos DB</span></span> 

> [!div class="op_single_selector"]
> * [.NET](create-table-dotnet.md)
> * [Java](create-table-java.md)
> * [Node.js](create-table-nodejs.md)
> * [Python](create-table-python.md)
>  

<span data-ttu-id="59bbc-108">This quickstart shows how to use .NET and the Azure Cosmos DB [Table API](table-introduction.md) to build an app by cloning an example from GitHub.</span><span class="sxs-lookup"><span data-stu-id="59bbc-108">This quickstart shows how to use .NET and the Azure Cosmos DB [Table API](table-introduction.md) to build an app by cloning an example from GitHub.</span></span> <span data-ttu-id="59bbc-109">This quickstart also shows you how to create an Azure Cosmos DB account and how to use Data Explorer to create tables and entities in the web-based Azure portal.</span><span class="sxs-lookup"><span data-stu-id="59bbc-109">This quickstart also shows you how to create an Azure Cosmos DB account and how to use Data Explorer to create tables and entities in the web-based Azure portal.</span></span>

<span data-ttu-id="59bbc-110">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span><span class="sxs-lookup"><span data-stu-id="59bbc-110">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="59bbc-111">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="59bbc-111">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="59bbc-112">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="59bbc-112">Prerequisites</span></span>

<span data-ttu-id="59bbc-113">If you don’t already have Visual Studio 2017 installed, you can download and use the **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="59bbc-113">If you don’t already have Visual Studio 2017 installed, you can download and use the **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="59bbc-114">Make sure that you enable **Azure development** during the Visual Studio setup.</span><span class="sxs-lookup"><span data-stu-id="59bbc-114">Make sure that you enable **Azure development** during the Visual Studio setup.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="59bbc-115">Create a database account</span><span class="sxs-lookup"><span data-stu-id="59bbc-115">Create a database account</span></span>

> [!IMPORTANT] 
> You must create a new Table API account to work with the generally available Table API SDKs. Table API accounts created during preview are not supported by the generally available SDKs.
>

[!INCLUDE [cosmos-db-create-dbaccount-table](../../includes/cosmos-db-create-dbaccount-table.md)]

## <a name="add-a-table"></a><span data-ttu-id="59bbc-118">Add a table</span><span class="sxs-lookup"><span data-stu-id="59bbc-118">Add a table</span></span>

[!INCLUDE [cosmos-db-create-table](../../includes/cosmos-db-create-table.md)]

## <a name="add-sample-data"></a><span data-ttu-id="59bbc-119">Add sample data</span><span class="sxs-lookup"><span data-stu-id="59bbc-119">Add sample data</span></span>

[!INCLUDE [cosmos-db-create-table-add-sample-data](../../includes/cosmos-db-create-table-add-sample-data.md)]

## <a name="clone-the-sample-application"></a><span data-ttu-id="59bbc-120">Clone the sample application</span><span class="sxs-lookup"><span data-stu-id="59bbc-120">Clone the sample application</span></span>

<span data-ttu-id="59bbc-121">Now let's clone a Table app from GitHub, set the connection string, and run it.</span><span class="sxs-lookup"><span data-stu-id="59bbc-121">Now let's clone a Table app from GitHub, set the connection string, and run it.</span></span> <span data-ttu-id="59bbc-122">You'll see how easy it is to work with data programmatically.</span><span class="sxs-lookup"><span data-stu-id="59bbc-122">You'll see how easy it is to work with data programmatically.</span></span> 

1. <span data-ttu-id="59bbc-123">Open a command prompt, create a new folder named git-samples, then close the command prompt.</span><span class="sxs-lookup"><span data-stu-id="59bbc-123">Open a command prompt, create a new folder named git-samples, then close the command prompt.</span></span>

    ```bash
    md "C:\git-samples"
    ```

2. <span data-ttu-id="59bbc-124">Open a git terminal window, such as git bash, and use the `cd` command to change to the new folder to install the sample app.</span><span class="sxs-lookup"><span data-stu-id="59bbc-124">Open a git terminal window, such as git bash, and use the `cd` command to change to the new folder to install the sample app.</span></span>

    ```bash
    cd "C:\git-samples"
    ```

3. <span data-ttu-id="59bbc-125">Run the following command to clone the sample repository.</span><span class="sxs-lookup"><span data-stu-id="59bbc-125">Run the following command to clone the sample repository.</span></span> <span data-ttu-id="59bbc-126">This command creates a copy of the sample app on your computer.</span><span class="sxs-lookup"><span data-stu-id="59bbc-126">This command creates a copy of the sample app on your computer.</span></span>

    ```bash
    git clone https://github.com/Azure-Samples/storage-table-dotnet-getting-started.git
    ```
## <a name="open-the-sample-application-in-visual-studio"></a><span data-ttu-id="59bbc-127">Open the sample application in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="59bbc-127">Open the sample application in Visual Studio</span></span>

1. <span data-ttu-id="59bbc-128">In Visual Studio, from the **File** menu, choose **Open**, then choose **Project/Solution**.</span><span class="sxs-lookup"><span data-stu-id="59bbc-128">In Visual Studio, from the **File** menu, choose **Open**, then choose **Project/Solution**.</span></span> 

   ![Open the solution](media/create-table-dotnet/azure-cosmosdb-open-solution.png) 

2. <span data-ttu-id="59bbc-130">Navigate to the folder where you cloned the sample application, and open the TableStorage.sln file.</span><span class="sxs-lookup"><span data-stu-id="59bbc-130">Navigate to the folder where you cloned the sample application, and open the TableStorage.sln file.</span></span>

   ![Open the cloned application](media/create-table-dotnet/azure-cosmos-db-open-clone.png) 

## <a name="update-your-connection-string"></a><span data-ttu-id="59bbc-132">Update your connection string</span><span class="sxs-lookup"><span data-stu-id="59bbc-132">Update your connection string</span></span>

<span data-ttu-id="59bbc-133">Now go back to the Azure portal to get your connection string information and copy it into the app.</span><span class="sxs-lookup"><span data-stu-id="59bbc-133">Now go back to the Azure portal to get your connection string information and copy it into the app.</span></span> <span data-ttu-id="59bbc-134">This enables your app to communicate with your hosted database.</span><span class="sxs-lookup"><span data-stu-id="59bbc-134">This enables your app to communicate with your hosted database.</span></span> 

1. <span data-ttu-id="59bbc-135">In the [Azure portal](http://portal.azure.com/), click **Connection String**.</span><span class="sxs-lookup"><span data-stu-id="59bbc-135">In the [Azure portal](http://portal.azure.com/), click **Connection String**.</span></span> 

    <span data-ttu-id="59bbc-136">Use the copy button on the right side of the window to copy the **PRIMARY CONNECTION STRING**.</span><span class="sxs-lookup"><span data-stu-id="59bbc-136">Use the copy button on the right side of the window to copy the **PRIMARY CONNECTION STRING**.</span></span>

    ![View and copy the PRIMARY CONNECTION STRING in the Connection String pane](./media/create-table-dotnet/connection-string.png)

2. <span data-ttu-id="59bbc-138">In Visual Studio, open the App.config file.</span><span class="sxs-lookup"><span data-stu-id="59bbc-138">In Visual Studio, open the App.config file.</span></span> 

3. <span data-ttu-id="59bbc-139">Uncomment the StorageConnectionString on line 8 and comment out the StorageConnectionString on line 7, because this tutorial does not use the Azure SDK Storage Emulator.</span><span class="sxs-lookup"><span data-stu-id="59bbc-139">Uncomment the StorageConnectionString on line 8 and comment out the StorageConnectionString on line 7, because this tutorial does not use the Azure SDK Storage Emulator.</span></span> <span data-ttu-id="59bbc-140">Lines 7 and 8 should now look like this:</span><span class="sxs-lookup"><span data-stu-id="59bbc-140">Lines 7 and 8 should now look like this:</span></span>

    ```
    <!--key="StorageConnectionString" value="UseDevelopmentStorage=true;" />-->
    <add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=[AccountName];AccountKey=[AccountKey]" />
    ```

4. <span data-ttu-id="59bbc-141">Paste the **PRIMARY CONNECTION STRING** from the portal into the StorageConnectionString value on line 8.</span><span class="sxs-lookup"><span data-stu-id="59bbc-141">Paste the **PRIMARY CONNECTION STRING** from the portal into the StorageConnectionString value on line 8.</span></span> <span data-ttu-id="59bbc-142">Paste the string inside the quotes.</span><span class="sxs-lookup"><span data-stu-id="59bbc-142">Paste the string inside the quotes.</span></span> 

    > [!IMPORTANT]
    > If your Endpoint uses documents.azure.com, that means you have a preview account, and you must create a [new Table API account](#create-a-database-account) to work with the generally available Table API SDK. 
    > 

    <span data-ttu-id="59bbc-144">Line 8 should now appear similar to:</span><span class="sxs-lookup"><span data-stu-id="59bbc-144">Line 8 should now appear similar to:</span></span>

    ```
    <add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<account-key>;TableEndpoint=https://<account name>.table.cosmosdb.azure.com;" />
    ```

5. <span data-ttu-id="59bbc-145">Press CTRL+S to save the App.config file.</span><span class="sxs-lookup"><span data-stu-id="59bbc-145">Press CTRL+S to save the App.config file.</span></span>

<span data-ttu-id="59bbc-146">You've now updated your app with all the info it needs to communicate with Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="59bbc-146">You've now updated your app with all the info it needs to communicate with Azure Cosmos DB.</span></span> 

## <a name="build-and-deploy-the-app"></a><span data-ttu-id="59bbc-147">Build and deploy the app</span><span class="sxs-lookup"><span data-stu-id="59bbc-147">Build and deploy the app</span></span>

1. <span data-ttu-id="59bbc-148">In Visual Studio, right-click on the **TableStorage** project in **Solution Explorer** and then click **Manage NuGet Packages**.</span><span class="sxs-lookup"><span data-stu-id="59bbc-148">In Visual Studio, right-click on the **TableStorage** project in **Solution Explorer** and then click **Manage NuGet Packages**.</span></span> 

   ![Manage NuGet Packages](media/create-table-dotnet/azure-cosmosdb-manage-nuget.png)
2. <span data-ttu-id="59bbc-150">In the NuGet **Browse** box, type *Microsoft.Azure.CosmosDB.Table*.</span><span class="sxs-lookup"><span data-stu-id="59bbc-150">In the NuGet **Browse** box, type *Microsoft.Azure.CosmosDB.Table*.</span></span> <span data-ttu-id="59bbc-151">This will find the Cosmos DB Table API client library.</span><span class="sxs-lookup"><span data-stu-id="59bbc-151">This will find the Cosmos DB Table API client library.</span></span> <span data-ttu-id="59bbc-152">Note that this library is currently available for .NET Standard only, it's not yet available for .NET Core.</span><span class="sxs-lookup"><span data-stu-id="59bbc-152">Note that this library is currently available for .NET Standard only, it's not yet available for .NET Core.</span></span>
   
   ![NuGet Browse tab](media/create-table-dotnet/azure-cosmosdb-nuget-browse.png)

3. <span data-ttu-id="59bbc-154">Click **Install** to install the **Microsoft.Azure.CosmosDB.Table** library.</span><span class="sxs-lookup"><span data-stu-id="59bbc-154">Click **Install** to install the **Microsoft.Azure.CosmosDB.Table** library.</span></span> <span data-ttu-id="59bbc-155">This installs the Azure Cosmos DB Table API package and all dependencies.</span><span class="sxs-lookup"><span data-stu-id="59bbc-155">This installs the Azure Cosmos DB Table API package and all dependencies.</span></span>

    ![Click Install](media/create-table-dotnet/azure-cosmosdb-nuget-install.png)

4. <span data-ttu-id="59bbc-157">Open BasicSamples.cs.</span><span class="sxs-lookup"><span data-stu-id="59bbc-157">Open BasicSamples.cs.</span></span> <span data-ttu-id="59bbc-158">Right-click on line 52, select **Breakpoint**, then select **Insert Breakpoint**.</span><span class="sxs-lookup"><span data-stu-id="59bbc-158">Right-click on line 52, select **Breakpoint**, then select **Insert Breakpoint**.</span></span> <span data-ttu-id="59bbc-159">Insert another breakpoint on line 55.</span><span class="sxs-lookup"><span data-stu-id="59bbc-159">Insert another breakpoint on line 55.</span></span>

   ![Add a breakpoint](media/create-table-dotnet/azure-cosmosdb-breakpoint.png) 

5. <span data-ttu-id="59bbc-161">Press F5 to run the application.</span><span class="sxs-lookup"><span data-stu-id="59bbc-161">Press F5 to run the application.</span></span>

    <span data-ttu-id="59bbc-162">The console window displays the name of the new table database (in this case, demo91ab4) in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="59bbc-162">The console window displays the name of the new table database (in this case, demo91ab4) in Azure Cosmos DB.</span></span> 
    
    ![Console output](media/create-table-dotnet/azure-cosmosdb-console.png)

    <span data-ttu-id="59bbc-164">If you get an error about dependencies, see [Troubleshooting](table-sdk-dotnet.md#troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="59bbc-164">If you get an error about dependencies, see [Troubleshooting](table-sdk-dotnet.md#troubleshooting).</span></span>

    <span data-ttu-id="59bbc-165">When you hit the first breakpoint, go back to Data Explorer in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="59bbc-165">When you hit the first breakpoint, go back to Data Explorer in the Azure portal.</span></span> <span data-ttu-id="59bbc-166">Click the **Refresh** button, expand the demo\* table, and click **Entities**.</span><span class="sxs-lookup"><span data-stu-id="59bbc-166">Click the **Refresh** button, expand the demo\* table, and click **Entities**.</span></span> <span data-ttu-id="59bbc-167">The **Entities** tab on the right shows the new entity that was added for Walter Harp.</span><span class="sxs-lookup"><span data-stu-id="59bbc-167">The **Entities** tab on the right shows the new entity that was added for Walter Harp.</span></span> <span data-ttu-id="59bbc-168">Note that the phone number for the new entity is 425-555-0101.</span><span class="sxs-lookup"><span data-stu-id="59bbc-168">Note that the phone number for the new entity is 425-555-0101.</span></span>

    ![New entity](media/create-table-dotnet/azure-cosmosdb-entity.png)
    
6. <span data-ttu-id="59bbc-170">Close the **Entities** tab in Data Explorer.</span><span class="sxs-lookup"><span data-stu-id="59bbc-170">Close the **Entities** tab in Data Explorer.</span></span>
    
7. <span data-ttu-id="59bbc-171">Press F5 to run the app to the next breakpoint.</span><span class="sxs-lookup"><span data-stu-id="59bbc-171">Press F5 to run the app to the next breakpoint.</span></span> 

    <span data-ttu-id="59bbc-172">When you hit the breakpoint, switch back to the Azure portal, click **Entities** again to open the **Entities** tab, and note that the phone number has been updated to 425-555-0105.</span><span class="sxs-lookup"><span data-stu-id="59bbc-172">When you hit the breakpoint, switch back to the Azure portal, click **Entities** again to open the **Entities** tab, and note that the phone number has been updated to 425-555-0105.</span></span>

8. <span data-ttu-id="59bbc-173">Press F5 to run the app.</span><span class="sxs-lookup"><span data-stu-id="59bbc-173">Press F5 to run the app.</span></span> 
 
   <span data-ttu-id="59bbc-174">The app adds entities for use in an advanced sample app that the Table API currently does not support.</span><span class="sxs-lookup"><span data-stu-id="59bbc-174">The app adds entities for use in an advanced sample app that the Table API currently does not support.</span></span> <span data-ttu-id="59bbc-175">The app then deletes the table created by the sample app.</span><span class="sxs-lookup"><span data-stu-id="59bbc-175">The app then deletes the table created by the sample app.</span></span>

9. <span data-ttu-id="59bbc-176">In the console window, press Enter to end the execution of the app.</span><span class="sxs-lookup"><span data-stu-id="59bbc-176">In the console window, press Enter to end the execution of the app.</span></span> 
  

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="59bbc-177">Review SLAs in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="59bbc-177">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="59bbc-178">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="59bbc-178">Clean up resources</span></span>

[!INCLUDE [cosmosdb-delete-resource-group](../../includes/cosmos-db-delete-resource-group.md)]

## <a name="next-steps"></a><span data-ttu-id="59bbc-179">Next steps</span><span class="sxs-lookup"><span data-stu-id="59bbc-179">Next steps</span></span>

<span data-ttu-id="59bbc-180">In this quickstart, you've learned how to create an Azure Cosmos DB account, create a table using the Data Explorer, and run an app.</span><span class="sxs-lookup"><span data-stu-id="59bbc-180">In this quickstart, you've learned how to create an Azure Cosmos DB account, create a table using the Data Explorer, and run an app.</span></span>  <span data-ttu-id="59bbc-181">Now you can query your data using the Table API.</span><span class="sxs-lookup"><span data-stu-id="59bbc-181">Now you can query your data using the Table API.</span></span>  

> [!div class="nextstepaction"]
> [Import table data to the Table API](table-import.md)

