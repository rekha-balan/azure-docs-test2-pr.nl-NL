---
title: 'Azure Cosmos DB: Build an app with Python and the SQL API | Microsoft Docs'
description: Presents a Python code sample you can use to connect to and query the Azure Cosmos DB SQL API
services: cosmos-db
author: SnehaGunda
manager: kfile
ms.service: cosmos-db
ms.component: cosmosdb-sql
ms.custom: quick start connect, mvc, devcenter
ms.devlang: python
ms.topic: quickstart
ms.date: 04/13/2018
ms.author: sngun
ms.openlocfilehash: b9f1258ff6beebeef4acee0694b60863b785cda5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870140"
---
# <a name="azure-cosmos-db-build-a-sql-api-app-with-python-and-the-azure-portal"></a><span data-ttu-id="4ca79-103">Azure Cosmos DB: Build a SQL API app with Python and the Azure portal</span><span class="sxs-lookup"><span data-stu-id="4ca79-103">Azure Cosmos DB: Build a SQL API app with Python and the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [.NET](create-sql-api-dotnet.md)
> * [Java](create-sql-api-java.md)
> * [Node.js](create-sql-api-nodejs.md)
> * [Node.js- v2](create-sql-api-nodejs-preview.md)
> * [Python](create-sql-api-python.md)
> * [Xamarin](create-sql-api-xamarin-dotnet.md)
>  

<span data-ttu-id="4ca79-110">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span><span class="sxs-lookup"><span data-stu-id="4ca79-110">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="4ca79-111">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="4ca79-111">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="4ca79-112">This quick start demonstrates how to create an Azure Cosmos DB [SQL API](sql-api-introduction.md) account, document database, and collection using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="4ca79-112">This quick start demonstrates how to create an Azure Cosmos DB [SQL API](sql-api-introduction.md) account, document database, and collection using the Azure portal.</span></span> <span data-ttu-id="4ca79-113">You then build and run a console app built on the [SQL Python API](sql-api-sdk-python.md).</span><span class="sxs-lookup"><span data-stu-id="4ca79-113">You then build and run a console app built on the [SQL Python API](sql-api-sdk-python.md).</span></span>

<span data-ttu-id="4ca79-114">[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)] [!INCLUDE [cosmos-db-emulator-docdb-api](../../includes/cosmos-db-emulator-docdb-api.md)]</span><span class="sxs-lookup"><span data-stu-id="4ca79-114">[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)] [!INCLUDE [cosmos-db-emulator-docdb-api](../../includes/cosmos-db-emulator-docdb-api.md)]</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4ca79-115">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="4ca79-115">Prerequisites</span></span>

* <span data-ttu-id="4ca79-116">[Python 3.6](https://www.python.org/downloads/) with \<install location\>\Python36 and \<install location>\Python36\Scripts added to your PATH.</span><span class="sxs-lookup"><span data-stu-id="4ca79-116">[Python 3.6](https://www.python.org/downloads/) with \<install location\>\Python36 and \<install location>\Python36\Scripts added to your PATH.</span></span> 
* [<span data-ttu-id="4ca79-117">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="4ca79-117">Visual Studio Code</span></span>](https://code.visualstudio.com/)
* [<span data-ttu-id="4ca79-118">Python extention for Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="4ca79-118">Python extention for Visual Studio Code</span></span>](https://marketplace.visualstudio.com/items?itemName=ms-python.python#overview)

## <a name="create-a-database-account"></a><span data-ttu-id="4ca79-119">Create a database account</span><span class="sxs-lookup"><span data-stu-id="4ca79-119">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="4ca79-120">Add a collection</span><span class="sxs-lookup"><span data-stu-id="4ca79-120">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="add-sample-data"></a><span data-ttu-id="4ca79-121">Add sample data</span><span class="sxs-lookup"><span data-stu-id="4ca79-121">Add sample data</span></span>

[!INCLUDE [cosmos-db-create-sql-api-add-sample-data](../../includes/cosmos-db-create-sql-api-add-sample-data.md)]

## <a name="query-your-data"></a><span data-ttu-id="4ca79-122">Query your data</span><span class="sxs-lookup"><span data-stu-id="4ca79-122">Query your data</span></span>

[!INCLUDE [cosmos-db-create-sql-api-query-data](../../includes/cosmos-db-create-sql-api-query-data.md)]

## <a name="clone-the-sample-application"></a><span data-ttu-id="4ca79-123">Clone the sample application</span><span class="sxs-lookup"><span data-stu-id="4ca79-123">Clone the sample application</span></span>

<span data-ttu-id="4ca79-124">Now let's clone a SQL API app from github, set the connection string, and run it.</span><span class="sxs-lookup"><span data-stu-id="4ca79-124">Now let's clone a SQL API app from github, set the connection string, and run it.</span></span> <span data-ttu-id="4ca79-125">You see how easy it is to work with data programmatically.</span><span class="sxs-lookup"><span data-stu-id="4ca79-125">You see how easy it is to work with data programmatically.</span></span> 

1. <span data-ttu-id="4ca79-126">Open a command prompt, create a new folder named git-samples, then close the command prompt.</span><span class="sxs-lookup"><span data-stu-id="4ca79-126">Open a command prompt, create a new folder named git-samples, then close the command prompt.</span></span>

    ```bash
    md "C:\git-samples"
    ```

2. <span data-ttu-id="4ca79-127">Open a git terminal window, such as git bash, and use the `cd` command to change to the new folder to install the sample app.</span><span class="sxs-lookup"><span data-stu-id="4ca79-127">Open a git terminal window, such as git bash, and use the `cd` command to change to the new folder to install the sample app.</span></span>

    ```bash
    cd "C:\git-samples"
    ```

3. <span data-ttu-id="4ca79-128">Run the following command to clone the sample repository.</span><span class="sxs-lookup"><span data-stu-id="4ca79-128">Run the following command to clone the sample repository.</span></span> <span data-ttu-id="4ca79-129">This command creates a copy of the sample app on your computer.</span><span class="sxs-lookup"><span data-stu-id="4ca79-129">This command creates a copy of the sample app on your computer.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-documentdb-python-getting-started.git
    ```  
    
## <a name="review-the-code"></a><span data-ttu-id="4ca79-130">Review the code</span><span class="sxs-lookup"><span data-stu-id="4ca79-130">Review the code</span></span>

<span data-ttu-id="4ca79-131">This step is optional.</span><span class="sxs-lookup"><span data-stu-id="4ca79-131">This step is optional.</span></span> <span data-ttu-id="4ca79-132">If you're interested in learning how the database resources are created in the code, you can review the following snippets.</span><span class="sxs-lookup"><span data-stu-id="4ca79-132">If you're interested in learning how the database resources are created in the code, you can review the following snippets.</span></span> <span data-ttu-id="4ca79-133">Otherwise, you can skip ahead to [Update your connection string](#update-your-connection-string).</span><span class="sxs-lookup"><span data-stu-id="4ca79-133">Otherwise, you can skip ahead to [Update your connection string](#update-your-connection-string).</span></span> 

<span data-ttu-id="4ca79-134">The following snippets are all taken from the DocumentDBGetStarted.py file.</span><span class="sxs-lookup"><span data-stu-id="4ca79-134">The following snippets are all taken from the DocumentDBGetStarted.py file.</span></span>

* <span data-ttu-id="4ca79-135">The DocumentClient is initialized.</span><span class="sxs-lookup"><span data-stu-id="4ca79-135">The DocumentClient is initialized.</span></span>

    ```python
    # Initialize the Python client
    client = document_client.DocumentClient(config['ENDPOINT'], {'masterKey': config['MASTERKEY']})
    ```

* <span data-ttu-id="4ca79-136">A new database is created.</span><span class="sxs-lookup"><span data-stu-id="4ca79-136">A new database is created.</span></span>

    ```python
    # Create a database
    db = client.CreateDatabase({ 'id': config['SQL_DATABASE'] })
    ```

* <span data-ttu-id="4ca79-137">A new collection is created.</span><span class="sxs-lookup"><span data-stu-id="4ca79-137">A new collection is created.</span></span>

    ```python
    # Create collection options
    options = {
        'offerEnableRUPerMinuteThroughput': True,
        'offerVersion': "V2",
        'offerThroughput': 400
    }

    # Create a collection
    collection = client.CreateCollection(db['_self'], { 'id': config['SQL_COLLECTION'] }, options)
    ```

* <span data-ttu-id="4ca79-138">Some documents are created.</span><span class="sxs-lookup"><span data-stu-id="4ca79-138">Some documents are created.</span></span>

    ```python
    # Create some documents
    document1 = client.CreateDocument(collection['_self'],
        { 
            'id': 'server1',
            'Web Site': 0,
            'Cloud Service': 0,
            'Virtual Machine': 0,
            'name': 'some' 
        })
    ```

* <span data-ttu-id="4ca79-139">A query is performed using SQL</span><span class="sxs-lookup"><span data-stu-id="4ca79-139">A query is performed using SQL</span></span>

    ```python
    # Query them in SQL
    query = { 'query': 'SELECT * FROM server s' }    
            
    options = {} 
    options['enableCrossPartitionQuery'] = True
    options['maxItemCount'] = 2

    result_iterable = client.QueryDocuments(collection['_self'], query, options)
    results = list(result_iterable);

    print(results)
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="4ca79-140">Update your connection string</span><span class="sxs-lookup"><span data-stu-id="4ca79-140">Update your connection string</span></span>

<span data-ttu-id="4ca79-141">Now go back to the Azure portal to get your connection string information and copy it into the app.</span><span class="sxs-lookup"><span data-stu-id="4ca79-141">Now go back to the Azure portal to get your connection string information and copy it into the app.</span></span>

1. <span data-ttu-id="4ca79-142">In the [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in the left navigation click **Keys**.</span><span class="sxs-lookup"><span data-stu-id="4ca79-142">In the [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in the left navigation click **Keys**.</span></span> <span data-ttu-id="4ca79-143">You'll use the copy buttons on the right side of the screen to copy the **URI** and **Primary Key** into the DocumentDBGetStarted.py file in the next step.</span><span class="sxs-lookup"><span data-stu-id="4ca79-143">You'll use the copy buttons on the right side of the screen to copy the **URI** and **Primary Key** into the DocumentDBGetStarted.py file in the next step.</span></span>

    ![View and copy an access key in the Azure portal, Keys blade](./media/create-sql-api-dotnet/keys.png)

2. <span data-ttu-id="4ca79-145">Open the C:\git-samples\azure-cosmos-db-documentdb-python-getting-startedDocumentDBGetStarted.py file in Visual Studio code.</span><span class="sxs-lookup"><span data-stu-id="4ca79-145">Open the C:\git-samples\azure-cosmos-db-documentdb-python-getting-startedDocumentDBGetStarted.py file in Visual Studio code.</span></span> 

3. <span data-ttu-id="4ca79-146">Copy your **URI** value from the portal (using the copy button) and make it the value of the **endpoint** key in DocumentDBGetStarted.py.</span><span class="sxs-lookup"><span data-stu-id="4ca79-146">Copy your **URI** value from the portal (using the copy button) and make it the value of the **endpoint** key in DocumentDBGetStarted.py.</span></span> 

    `'ENDPOINT': 'https://FILLME.documents.azure.com',`

4. <span data-ttu-id="4ca79-147">Then copy your **PRIMARY KEY** value from the portal and make it the value of the **config.MASTERKEY** in DocumentDBGetStarted.py.</span><span class="sxs-lookup"><span data-stu-id="4ca79-147">Then copy your **PRIMARY KEY** value from the portal and make it the value of the **config.MASTERKEY** in DocumentDBGetStarted.py.</span></span> <span data-ttu-id="4ca79-148">You've now updated your app with all the info it needs to communicate with Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="4ca79-148">You've now updated your app with all the info it needs to communicate with Azure Cosmos DB.</span></span> 

    `'MASTERKEY': 'FILLME',`

5. <span data-ttu-id="4ca79-149">Save the DocumentDBGetStarted.py file.</span><span class="sxs-lookup"><span data-stu-id="4ca79-149">Save the DocumentDBGetStarted.py file.</span></span>
    
## <a name="run-the-app"></a><span data-ttu-id="4ca79-150">Run the app</span><span class="sxs-lookup"><span data-stu-id="4ca79-150">Run the app</span></span>

1. <span data-ttu-id="4ca79-151">In Visual Studio Code, select **View**>**Command Palette**.</span><span class="sxs-lookup"><span data-stu-id="4ca79-151">In Visual Studio Code, select **View**>**Command Palette**.</span></span> 

2. <span data-ttu-id="4ca79-152">At the prompt, enter  **Python: Select Interpreter** and then select the version of Python to use.</span><span class="sxs-lookup"><span data-stu-id="4ca79-152">At the prompt, enter  **Python: Select Interpreter** and then select the version of Python to use.</span></span>

    <span data-ttu-id="4ca79-153">The Footer in Visual Studio Code is updated to indicate the interpreter selected.</span><span class="sxs-lookup"><span data-stu-id="4ca79-153">The Footer in Visual Studio Code is updated to indicate the interpreter selected.</span></span> 

3. <span data-ttu-id="4ca79-154">Select **View** > **Integrated Terminal** to open the Visual Studio SCode integrated terminal.</span><span class="sxs-lookup"><span data-stu-id="4ca79-154">Select **View** > **Integrated Terminal** to open the Visual Studio SCode integrated terminal.</span></span>

4. <span data-ttu-id="4ca79-155">In the integrated terminal window, ensure you're in the run the azure-cosmos-db-documentdb-python-getting-started folder.</span><span class="sxs-lookup"><span data-stu-id="4ca79-155">In the integrated terminal window, ensure you're in the run the azure-cosmos-db-documentdb-python-getting-started folder.</span></span> <span data-ttu-id="4ca79-156">If not, run the following command to switch to the sample folder.</span><span class="sxs-lookup"><span data-stu-id="4ca79-156">If not, run the following command to switch to the sample folder.</span></span> 

    ```
    cd "C:\git-samples\azure-cosmos-db-documentdb-python-getting-started"`
    ```

5. <span data-ttu-id="4ca79-157">Run the following command to install the pydocumentdb package.</span><span class="sxs-lookup"><span data-stu-id="4ca79-157">Run the following command to install the pydocumentdb package.</span></span> 

    ```
    pip3 install pydocumentdb
    ```

    <span data-ttu-id="4ca79-158">If you get an error about access being denied when attempting to install pydocumentdb, you'll need to [run VS Code as an administrator](https://stackoverflow.com/questions/37700536/visual-studio-code-terminal-how-to-run-a-command-with-administrator-rights).</span><span class="sxs-lookup"><span data-stu-id="4ca79-158">If you get an error about access being denied when attempting to install pydocumentdb, you'll need to [run VS Code as an administrator](https://stackoverflow.com/questions/37700536/visual-studio-code-terminal-how-to-run-a-command-with-administrator-rights).</span></span>

6. <span data-ttu-id="4ca79-159">Run the following command to run the sample and create and store new documents in Azure Cosmos dB.</span><span class="sxs-lookup"><span data-stu-id="4ca79-159">Run the following command to run the sample and create and store new documents in Azure Cosmos dB.</span></span>

    ```
    python DocumentDBGetStarted.py
    ```

7. <span data-ttu-id="4ca79-160">To confirm the new documents were created and saved, in the Azure portal, select **Data Explorer**, expand **coll**, expand **Documents**, and then select the **server1** document.</span><span class="sxs-lookup"><span data-stu-id="4ca79-160">To confirm the new documents were created and saved, in the Azure portal, select **Data Explorer**, expand **coll**, expand **Documents**, and then select the **server1** document.</span></span> <span data-ttu-id="4ca79-161">The server1 document contents match the content returned in the integrated terminal window.</span><span class="sxs-lookup"><span data-stu-id="4ca79-161">The server1 document contents match the content returned in the integrated terminal window.</span></span> 

    ![View the new documents in the Azure portal](./media/create-sql-api-python/azure-cosmos-db-confirm-documents.png)

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="4ca79-163">Review SLAs in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="4ca79-163">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="4ca79-164">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="4ca79-164">Clean up resources</span></span>

[!INCLUDE [cosmosdb-delete-resource-group](../../includes/cosmos-db-delete-resource-group.md)]

## <a name="next-steps"></a><span data-ttu-id="4ca79-165">Next steps</span><span class="sxs-lookup"><span data-stu-id="4ca79-165">Next steps</span></span>

<span data-ttu-id="4ca79-166">In this quickstart, you've learned how to create an Azure Cosmos DB account, create a collection using the Data Explorer, and run an app.</span><span class="sxs-lookup"><span data-stu-id="4ca79-166">In this quickstart, you've learned how to create an Azure Cosmos DB account, create a collection using the Data Explorer, and run an app.</span></span> <span data-ttu-id="4ca79-167">You can now import additional data to your Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="4ca79-167">You can now import additional data to your Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [Import data into Azure Cosmos DB for the SQL API](import-data.md)


