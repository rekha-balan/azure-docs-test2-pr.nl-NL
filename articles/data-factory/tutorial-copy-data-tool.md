---
title: Copy data by using the Azure Copy Data tool | Microsoft Docs
description: Create an Azure data factory and then use the Copy Data tool to copy data from Azure Blob storage to a SQL database.
services: data-factory
documentationcenter: ''
author: linda33wj
manager: craigg
ms.reviewer: douglasl
ms.service: data-factory
ms.workload: data-services
ms.topic: tutorial
ms.date: 06/21/2018
ms.author: jingwang
ms.openlocfilehash: 1be4769a8a07ac5d4a968ed5aa15ed2e0a2b6db2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864375"
---
# <a name="copy-data-from-azure-blob-storage-to-a-sql-database-by-using-the-copy-data-tool"></a><span data-ttu-id="aeacb-103">Copy data from Azure Blob storage to a SQL database by using the Copy Data tool</span><span class="sxs-lookup"><span data-stu-id="aeacb-103">Copy data from Azure Blob storage to a SQL database by using the Copy Data tool</span></span>
> [!div class="op_single_selector" title1="Select the version of the Data Factory service that you're using:"]
> * [Version 1](v1/data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [Current version](tutorial-copy-data-tool.md)

<span data-ttu-id="aeacb-106">In this tutorial, you use the Azure portal to create a data factory.</span><span class="sxs-lookup"><span data-stu-id="aeacb-106">In this tutorial, you use the Azure portal to create a data factory.</span></span> <span data-ttu-id="aeacb-107">Then, you use the Copy Data tool to create a pipeline that copies data from Azure Blob storage to a SQL database.</span><span class="sxs-lookup"><span data-stu-id="aeacb-107">Then, you use the Copy Data tool to create a pipeline that copies data from Azure Blob storage to a SQL database.</span></span> 

> [!NOTE]
> If you're new to Azure Data Factory, see [Introduction to Azure Data Factory](introduction.md).

<span data-ttu-id="aeacb-109">In this tutorial, you perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="aeacb-109">In this tutorial, you perform the following steps:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="aeacb-110">Create a data factory.</span><span class="sxs-lookup"><span data-stu-id="aeacb-110">Create a data factory.</span></span>
> * <span data-ttu-id="aeacb-111">Use the Copy Data tool to create a pipeline.</span><span class="sxs-lookup"><span data-stu-id="aeacb-111">Use the Copy Data tool to create a pipeline.</span></span>
> * <span data-ttu-id="aeacb-112">Monitor the pipeline and activity runs.</span><span class="sxs-lookup"><span data-stu-id="aeacb-112">Monitor the pipeline and activity runs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aeacb-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="aeacb-113">Prerequisites</span></span>

* <span data-ttu-id="aeacb-114">**Azure subscription**: If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/) before you begin.</span><span class="sxs-lookup"><span data-stu-id="aeacb-114">**Azure subscription**: If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/) before you begin.</span></span>
* <span data-ttu-id="aeacb-115">**Azure storage account**: Use Blob storage as the _source_ data store.</span><span class="sxs-lookup"><span data-stu-id="aeacb-115">**Azure storage account**: Use Blob storage as the _source_ data store.</span></span> <span data-ttu-id="aeacb-116">If you don't have an Azure storage account, see the instructions in [Create a storage account](../storage/common/storage-quickstart-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="aeacb-116">If you don't have an Azure storage account, see the instructions in [Create a storage account](../storage/common/storage-quickstart-create-account.md).</span></span>
* <span data-ttu-id="aeacb-117">**Azure SQL Database**: Use a SQL database as the _sink_ data store.</span><span class="sxs-lookup"><span data-stu-id="aeacb-117">**Azure SQL Database**: Use a SQL database as the _sink_ data store.</span></span> <span data-ttu-id="aeacb-118">If you don't have a SQL database, see the instructions in [Create a SQL database](../sql-database/sql-database-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="aeacb-118">If you don't have a SQL database, see the instructions in [Create a SQL database](../sql-database/sql-database-get-started-portal.md).</span></span>

### <a name="create-a-blob-and-a-sql-table"></a><span data-ttu-id="aeacb-119">Create a blob and a SQL table</span><span class="sxs-lookup"><span data-stu-id="aeacb-119">Create a blob and a SQL table</span></span>

<span data-ttu-id="aeacb-120">Prepare your Blob storage and your SQL database for the tutorial by performing these steps.</span><span class="sxs-lookup"><span data-stu-id="aeacb-120">Prepare your Blob storage and your SQL database for the tutorial by performing these steps.</span></span>

#### <a name="create-a-source-blob"></a><span data-ttu-id="aeacb-121">Create a source blob</span><span class="sxs-lookup"><span data-stu-id="aeacb-121">Create a source blob</span></span>

1. <span data-ttu-id="aeacb-122">Launch **Notepad**.</span><span class="sxs-lookup"><span data-stu-id="aeacb-122">Launch **Notepad**.</span></span> <span data-ttu-id="aeacb-123">Copy the following text and save it in a file named **inputEmp.txt** on your disk:</span><span class="sxs-lookup"><span data-stu-id="aeacb-123">Copy the following text and save it in a file named **inputEmp.txt** on your disk:</span></span>

    ```
    John|Doe
    Jane|Doe
    ```

1. <span data-ttu-id="aeacb-124">Create a container named **adfv2tutorial** and upload the inputEmp.txt file to the container.</span><span class="sxs-lookup"><span data-stu-id="aeacb-124">Create a container named **adfv2tutorial** and upload the inputEmp.txt file to the container.</span></span> <span data-ttu-id="aeacb-125">You can use various tools to perform these tasks, such as [Azure Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="aeacb-125">You can use various tools to perform these tasks, such as [Azure Storage Explorer](http://storageexplorer.com/).</span></span>

#### <a name="create-a-sink-sql-table"></a><span data-ttu-id="aeacb-126">Create a sink SQL table</span><span class="sxs-lookup"><span data-stu-id="aeacb-126">Create a sink SQL table</span></span>

1. <span data-ttu-id="aeacb-127">Use the following SQL script to create a table named **dbo.emp** in your SQL database:</span><span class="sxs-lookup"><span data-stu-id="aeacb-127">Use the following SQL script to create a table named **dbo.emp** in your SQL database:</span></span>

    ```sql
    CREATE TABLE dbo.emp
    (
        ID int IDENTITY(1,1) NOT NULL,
        FirstName varchar(50),
        LastName varchar(50)
    )
    GO

    CREATE CLUSTERED INDEX IX_emp_ID ON dbo.emp (ID);
    ```

1. <span data-ttu-id="aeacb-128">Allow Azure services to access SQL Server.</span><span class="sxs-lookup"><span data-stu-id="aeacb-128">Allow Azure services to access SQL Server.</span></span> <span data-ttu-id="aeacb-129">Verify that the setting **Allow access to Azure services** is enabled for your server that's running SQL Server.</span><span class="sxs-lookup"><span data-stu-id="aeacb-129">Verify that the setting **Allow access to Azure services** is enabled for your server that's running SQL Server.</span></span> <span data-ttu-id="aeacb-130">This setting lets Data Factory write data to your SQL server instance.</span><span class="sxs-lookup"><span data-stu-id="aeacb-130">This setting lets Data Factory write data to your SQL server instance.</span></span> <span data-ttu-id="aeacb-131">To verify and turn on this setting, take the following steps:</span><span class="sxs-lookup"><span data-stu-id="aeacb-131">To verify and turn on this setting, take the following steps:</span></span>

    <span data-ttu-id="aeacb-132">a.</span><span class="sxs-lookup"><span data-stu-id="aeacb-132">a.</span></span> <span data-ttu-id="aeacb-133">On the left, select **More services**, and then select **SQL servers**.</span><span class="sxs-lookup"><span data-stu-id="aeacb-133">On the left, select **More services**, and then select **SQL servers**.</span></span>

    <span data-ttu-id="aeacb-134">b.</span><span class="sxs-lookup"><span data-stu-id="aeacb-134">b.</span></span> <span data-ttu-id="aeacb-135">Select your server, and then select **SETTINGS** > **Firewall**.</span><span class="sxs-lookup"><span data-stu-id="aeacb-135">Select your server, and then select **SETTINGS** > **Firewall**.</span></span>

    <span data-ttu-id="aeacb-136">c.</span><span class="sxs-lookup"><span data-stu-id="aeacb-136">c.</span></span> <span data-ttu-id="aeacb-137">On the **Firewall settings** page, set the **Allow access to Azure services** option to **ON**.</span><span class="sxs-lookup"><span data-stu-id="aeacb-137">On the **Firewall settings** page, set the **Allow access to Azure services** option to **ON**.</span></span>

## <a name="create-a-data-factory"></a><span data-ttu-id="aeacb-138">Create a data factory</span><span class="sxs-lookup"><span data-stu-id="aeacb-138">Create a data factory</span></span>

1. <span data-ttu-id="aeacb-139">On the left menu, select **+ New** > **Data + Analytics** > **Data Factory**:</span><span class="sxs-lookup"><span data-stu-id="aeacb-139">On the left menu, select **+ New** > **Data + Analytics** > **Data Factory**:</span></span> 
   
   ![New data factory creation](./media/tutorial-copy-data-tool/new-azure-data-factory-menu.png)
1. <span data-ttu-id="aeacb-141">On the **New data factory** page, under **Name**, enter **ADFTutorialDataFactory**.</span><span class="sxs-lookup"><span data-stu-id="aeacb-141">On the **New data factory** page, under **Name**, enter **ADFTutorialDataFactory**.</span></span> 
      
     ![New data factory](./media/tutorial-copy-data-tool/new-azure-data-factory.png)
 
   <span data-ttu-id="aeacb-143">The name for your data factory must be _globally unique_.</span><span class="sxs-lookup"><span data-stu-id="aeacb-143">The name for your data factory must be _globally unique_.</span></span> <span data-ttu-id="aeacb-144">You might receive the following error message:</span><span class="sxs-lookup"><span data-stu-id="aeacb-144">You might receive the following error message:</span></span>
   
   ![New data factory error message](./media/tutorial-copy-data-tool/name-not-available-error.png)

   <span data-ttu-id="aeacb-146">If you receive an error message about the name value, enter a different name for the data factory.</span><span class="sxs-lookup"><span data-stu-id="aeacb-146">If you receive an error message about the name value, enter a different name for the data factory.</span></span> <span data-ttu-id="aeacb-147">For example, use the name _**yourname**_**ADFTutorialDataFactory**.</span><span class="sxs-lookup"><span data-stu-id="aeacb-147">For example, use the name _**yourname**_**ADFTutorialDataFactory**.</span></span> <span data-ttu-id="aeacb-148">For the naming rules for Data Factory artifacts, see [Data Factory naming rules](naming-rules.md).</span><span class="sxs-lookup"><span data-stu-id="aeacb-148">For the naming rules for Data Factory artifacts, see [Data Factory naming rules](naming-rules.md).</span></span>
1. <span data-ttu-id="aeacb-149">Select the Azure **subscription** in which to create the new data factory.</span><span class="sxs-lookup"><span data-stu-id="aeacb-149">Select the Azure **subscription** in which to create the new data factory.</span></span> 
1. <span data-ttu-id="aeacb-150">For **Resource Group**, take one of the following steps:</span><span class="sxs-lookup"><span data-stu-id="aeacb-150">For **Resource Group**, take one of the following steps:</span></span>
     
    <span data-ttu-id="aeacb-151">a.</span><span class="sxs-lookup"><span data-stu-id="aeacb-151">a.</span></span> <span data-ttu-id="aeacb-152">Select **Use existing**, and select an existing resource group from the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="aeacb-152">Select **Use existing**, and select an existing resource group from the drop-down list.</span></span>

    <span data-ttu-id="aeacb-153">b.</span><span class="sxs-lookup"><span data-stu-id="aeacb-153">b.</span></span> <span data-ttu-id="aeacb-154">Select **Create new**, and enter the name of a resource group.</span><span class="sxs-lookup"><span data-stu-id="aeacb-154">Select **Create new**, and enter the name of a resource group.</span></span> 
         
    <span data-ttu-id="aeacb-155">To learn about resource groups, see [Use resource groups to manage your Azure resources](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="aeacb-155">To learn about resource groups, see [Use resource groups to manage your Azure resources](../azure-resource-manager/resource-group-overview.md).</span></span>

1. <span data-ttu-id="aeacb-156">Under **version**, select **V2** for the version.</span><span class="sxs-lookup"><span data-stu-id="aeacb-156">Under **version**, select **V2** for the version.</span></span>
1. <span data-ttu-id="aeacb-157">Under **location**, select the location for the data factory.</span><span class="sxs-lookup"><span data-stu-id="aeacb-157">Under **location**, select the location for the data factory.</span></span> <span data-ttu-id="aeacb-158">Only supported locations are displayed in the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="aeacb-158">Only supported locations are displayed in the drop-down list.</span></span> <span data-ttu-id="aeacb-159">The data stores (for example, Azure Storage and SQL Database) and computes (for example, Azure HDInsight) that are used by your data factory can be in other locations and regions.</span><span class="sxs-lookup"><span data-stu-id="aeacb-159">The data stores (for example, Azure Storage and SQL Database) and computes (for example, Azure HDInsight) that are used by your data factory can be in other locations and regions.</span></span>
1. <span data-ttu-id="aeacb-160">Select **Pin to dashboard**.</span><span class="sxs-lookup"><span data-stu-id="aeacb-160">Select **Pin to dashboard**.</span></span> 
1. <span data-ttu-id="aeacb-161">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="aeacb-161">Select **Create**.</span></span>
1. <span data-ttu-id="aeacb-162">On the dashboard, the **Deploying Data Factory** tile shows the process status.</span><span class="sxs-lookup"><span data-stu-id="aeacb-162">On the dashboard, the **Deploying Data Factory** tile shows the process status.</span></span>

    ![Deploying data factory tile](media/tutorial-copy-data-tool/deploying-data-factory.png)
1. <span data-ttu-id="aeacb-164">After creation is finished, the **Data Factory** home page is displayed.</span><span class="sxs-lookup"><span data-stu-id="aeacb-164">After creation is finished, the **Data Factory** home page is displayed.</span></span>
   
    ![Data factory home page](./media/tutorial-copy-data-tool/data-factory-home-page.png)
1. <span data-ttu-id="aeacb-166">To launch the Azure Data Factory user interface (UI) in a separate tab, select the **Author & Monitor** tile.</span><span class="sxs-lookup"><span data-stu-id="aeacb-166">To launch the Azure Data Factory user interface (UI) in a separate tab, select the **Author & Monitor** tile.</span></span> 

## <a name="use-the-copy-data-tool-to-create-a-pipeline"></a><span data-ttu-id="aeacb-167">Use the Copy Data tool to create a pipeline</span><span class="sxs-lookup"><span data-stu-id="aeacb-167">Use the Copy Data tool to create a pipeline</span></span>

1. <span data-ttu-id="aeacb-168">On the **Let's get started** page, select the **Copy Data** tile to launch the Copy Data tool.</span><span class="sxs-lookup"><span data-stu-id="aeacb-168">On the **Let's get started** page, select the **Copy Data** tile to launch the Copy Data tool.</span></span> 

   ![Copy Data tool tile](./media/tutorial-copy-data-tool/copy-data-tool-tile.png)
1. <span data-ttu-id="aeacb-170">On the **Properties** page, under **Task name**, enter **CopyFromBlobToSqlPipeline**.</span><span class="sxs-lookup"><span data-stu-id="aeacb-170">On the **Properties** page, under **Task name**, enter **CopyFromBlobToSqlPipeline**.</span></span> <span data-ttu-id="aeacb-171">Then select **Next**.</span><span class="sxs-lookup"><span data-stu-id="aeacb-171">Then select **Next**.</span></span> <span data-ttu-id="aeacb-172">The Data Factory UI creates a pipeline with the specified task name.</span><span class="sxs-lookup"><span data-stu-id="aeacb-172">The Data Factory UI creates a pipeline with the specified task name.</span></span> 

    ![Properties page](./media/tutorial-copy-data-tool/copy-data-tool-properties-page.png)
1. <span data-ttu-id="aeacb-174">On the **Source data store** page, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="aeacb-174">On the **Source data store** page, complete the following steps:</span></span>

    <span data-ttu-id="aeacb-175">a.</span><span class="sxs-lookup"><span data-stu-id="aeacb-175">a.</span></span> <span data-ttu-id="aeacb-176">Click **+ Create new connection** to add a connection</span><span class="sxs-lookup"><span data-stu-id="aeacb-176">Click **+ Create new connection** to add a connection</span></span>

    ![New source linked service](./media/tutorial-copy-data-tool/new-source-linked-service.png)

    <span data-ttu-id="aeacb-178">b.</span><span class="sxs-lookup"><span data-stu-id="aeacb-178">b.</span></span> <span data-ttu-id="aeacb-179">Select **Azure Blob Storage** from the gallery, and then select **Next**.</span><span class="sxs-lookup"><span data-stu-id="aeacb-179">Select **Azure Blob Storage** from the gallery, and then select **Next**.</span></span>

    ![Select blob source](./media/tutorial-copy-data-tool/select-blob-source.png)

    <span data-ttu-id="aeacb-181">c.</span><span class="sxs-lookup"><span data-stu-id="aeacb-181">c.</span></span> <span data-ttu-id="aeacb-182">On the **New Linked Service** page, select your storage account from the **Storage account name** list, and then select **Finish**.</span><span class="sxs-lookup"><span data-stu-id="aeacb-182">On the **New Linked Service** page, select your storage account from the **Storage account name** list, and then select **Finish**.</span></span>

    ![Configure azure storage](./media/tutorial-copy-data-tool/configure-azure-storage.png)

    <span data-ttu-id="aeacb-184">d.</span><span class="sxs-lookup"><span data-stu-id="aeacb-184">d.</span></span> <span data-ttu-id="aeacb-185">Select the newly created linked service as source, then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="aeacb-185">Select the newly created linked service as source, then click **Next**.</span></span>

    ![Select source linked service](./media/tutorial-copy-data-tool/select-source-linked-service.png)

1. <span data-ttu-id="aeacb-187">On the **Choose the input file or folder** page, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="aeacb-187">On the **Choose the input file or folder** page, complete the following steps:</span></span>
    
    <span data-ttu-id="aeacb-188">a.</span><span class="sxs-lookup"><span data-stu-id="aeacb-188">a.</span></span> <span data-ttu-id="aeacb-189">Click **Browse** to navigate to the **adfv2tutorial/input** folder, select the **inputEmp.txt** file, then click **Choose**.</span><span class="sxs-lookup"><span data-stu-id="aeacb-189">Click **Browse** to navigate to the **adfv2tutorial/input** folder, select the **inputEmp.txt** file, then click **Choose**.</span></span>

    ![Choose the input file or folder](./media/tutorial-copy-data-tool/specify-source-path.png)

    <span data-ttu-id="aeacb-191">b.</span><span class="sxs-lookup"><span data-stu-id="aeacb-191">b.</span></span> <span data-ttu-id="aeacb-192">Click **Next** to move to next step.</span><span class="sxs-lookup"><span data-stu-id="aeacb-192">Click **Next** to move to next step.</span></span>

1. <span data-ttu-id="aeacb-193">On the **File format settings** page, notice that the tool automatically detects the column and row delimiters.</span><span class="sxs-lookup"><span data-stu-id="aeacb-193">On the **File format settings** page, notice that the tool automatically detects the column and row delimiters.</span></span> <span data-ttu-id="aeacb-194">Select **Next**.</span><span class="sxs-lookup"><span data-stu-id="aeacb-194">Select **Next**.</span></span> <span data-ttu-id="aeacb-195">You also can preview data and view the schema of the input data on this page.</span><span class="sxs-lookup"><span data-stu-id="aeacb-195">You also can preview data and view the schema of the input data on this page.</span></span> 

    ![File format settings](./media/tutorial-copy-data-tool/file-format-settings-page.png)
1. <span data-ttu-id="aeacb-197">On the **Destination data store** page, completes the following steps:</span><span class="sxs-lookup"><span data-stu-id="aeacb-197">On the **Destination data store** page, completes the following steps:</span></span>

    <span data-ttu-id="aeacb-198">a.</span><span class="sxs-lookup"><span data-stu-id="aeacb-198">a.</span></span> <span data-ttu-id="aeacb-199">Click **+ Create new connection** to add a connection</span><span class="sxs-lookup"><span data-stu-id="aeacb-199">Click **+ Create new connection** to add a connection</span></span>

    ![New sink linked service](./media/tutorial-copy-data-tool/new-sink-linked-service.png)

    <span data-ttu-id="aeacb-201">b.</span><span class="sxs-lookup"><span data-stu-id="aeacb-201">b.</span></span> <span data-ttu-id="aeacb-202">Select **Azure Blob Storage** from the gallery, and then select **Next**.</span><span class="sxs-lookup"><span data-stu-id="aeacb-202">Select **Azure Blob Storage** from the gallery, and then select **Next**.</span></span>

    ![Select Azure SQL DB](./media/tutorial-copy-data-tool/select-azure-sql-db.png)

    <span data-ttu-id="aeacb-204">c.</span><span class="sxs-lookup"><span data-stu-id="aeacb-204">c.</span></span> <span data-ttu-id="aeacb-205">On the **New Linked Service** page, select your server name and DB name from the dropdown list, and specify the username and password, then select **Finish**.</span><span class="sxs-lookup"><span data-stu-id="aeacb-205">On the **New Linked Service** page, select your server name and DB name from the dropdown list, and specify the username and password, then select **Finish**.</span></span>    

    ![Configure Azure SQL DB](./media/tutorial-copy-data-tool/config-azure-sql-db.png)

    <span data-ttu-id="aeacb-207">d.</span><span class="sxs-lookup"><span data-stu-id="aeacb-207">d.</span></span> <span data-ttu-id="aeacb-208">Select the newly created linked service as sink, then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="aeacb-208">Select the newly created linked service as sink, then click **Next**.</span></span>

    ![Select sink linked service](./media/tutorial-copy-data-tool/select-sink-linked-service.png)

1. <span data-ttu-id="aeacb-210">On the **Table mapping** page, select the **[dbo].[emp]** table, and then select **Next**.</span><span class="sxs-lookup"><span data-stu-id="aeacb-210">On the **Table mapping** page, select the **[dbo].[emp]** table, and then select **Next**.</span></span> 

    ![Table mapping](./media/tutorial-copy-data-tool/table-mapping.png)
1. <span data-ttu-id="aeacb-212">On the **Schema mapping** page, notice that the first and second columns in the input file are mapped to the **FirstName** and **LastName** columns of the **emp** table.</span><span class="sxs-lookup"><span data-stu-id="aeacb-212">On the **Schema mapping** page, notice that the first and second columns in the input file are mapped to the **FirstName** and **LastName** columns of the **emp** table.</span></span> <span data-ttu-id="aeacb-213">Select **Next**.</span><span class="sxs-lookup"><span data-stu-id="aeacb-213">Select **Next**.</span></span>

    ![Schema mapping page](./media/tutorial-copy-data-tool/schema-mapping.png)
1. <span data-ttu-id="aeacb-215">On the **Settings** page, select **Next**.</span><span class="sxs-lookup"><span data-stu-id="aeacb-215">On the **Settings** page, select **Next**.</span></span> 
1. <span data-ttu-id="aeacb-216">On the **Summary** page, review the settings, and then select **Next**.</span><span class="sxs-lookup"><span data-stu-id="aeacb-216">On the **Summary** page, review the settings, and then select **Next**.</span></span>

    ![Summary page](./media/tutorial-copy-data-tool/summary-page.png)
1. <span data-ttu-id="aeacb-218">On the **Deployment page**, select **Monitor** to monitor the pipeline (task).</span><span class="sxs-lookup"><span data-stu-id="aeacb-218">On the **Deployment page**, select **Monitor** to monitor the pipeline (task).</span></span>

    ![Deployment page](./media/tutorial-copy-data-tool/deployment-page.png)
1. <span data-ttu-id="aeacb-220">Notice that the **Monitor** tab on the left is automatically selected.</span><span class="sxs-lookup"><span data-stu-id="aeacb-220">Notice that the **Monitor** tab on the left is automatically selected.</span></span> <span data-ttu-id="aeacb-221">The **Actions** column includes links to view activity run details and to rerun the pipeline.</span><span class="sxs-lookup"><span data-stu-id="aeacb-221">The **Actions** column includes links to view activity run details and to rerun the pipeline.</span></span> <span data-ttu-id="aeacb-222">Select **Refresh** to refresh the list.</span><span class="sxs-lookup"><span data-stu-id="aeacb-222">Select **Refresh** to refresh the list.</span></span> 

    ![Monitor pipeline runs](./media/tutorial-copy-data-tool/pipeline-monitoring.png)
1. <span data-ttu-id="aeacb-224">To view the activity runs that are associated with the pipeline run, select the **View Activity Runs** link in the **Actions** column.</span><span class="sxs-lookup"><span data-stu-id="aeacb-224">To view the activity runs that are associated with the pipeline run, select the **View Activity Runs** link in the **Actions** column.</span></span> <span data-ttu-id="aeacb-225">For details about the copy operation, select the **Details** link (eyeglasses icon) in the **Actions** column.</span><span class="sxs-lookup"><span data-stu-id="aeacb-225">For details about the copy operation, select the **Details** link (eyeglasses icon) in the **Actions** column.</span></span> <span data-ttu-id="aeacb-226">To go back to the **Pipeline Runs** view, select the **Pipelines** link at the top.</span><span class="sxs-lookup"><span data-stu-id="aeacb-226">To go back to the **Pipeline Runs** view, select the **Pipelines** link at the top.</span></span> <span data-ttu-id="aeacb-227">To refresh the view, select **Refresh**.</span><span class="sxs-lookup"><span data-stu-id="aeacb-227">To refresh the view, select **Refresh**.</span></span> 

    ![Monitor activity runs](./media/tutorial-copy-data-tool/activity-monitoring.png)

    ![Copy activity details](./media/tutorial-copy-data-tool/copy-execution-details.png)

1. <span data-ttu-id="aeacb-230">Verify that the data is inserted into the **emp** table in your SQL database.</span><span class="sxs-lookup"><span data-stu-id="aeacb-230">Verify that the data is inserted into the **emp** table in your SQL database.</span></span>

    ![Verify SQL output](./media/tutorial-copy-data-tool/verify-sql-output.png)

1. <span data-ttu-id="aeacb-232">Select the **Author** tab on the left to switch to the editor mode.</span><span class="sxs-lookup"><span data-stu-id="aeacb-232">Select the **Author** tab on the left to switch to the editor mode.</span></span> <span data-ttu-id="aeacb-233">You can update the linked services, datasets, and pipelines that were created via the tool by using the editor.</span><span class="sxs-lookup"><span data-stu-id="aeacb-233">You can update the linked services, datasets, and pipelines that were created via the tool by using the editor.</span></span> <span data-ttu-id="aeacb-234">For details on editing these entities in the Data Factory UI, see [the Azure portal version of this tutorial](tutorial-copy-data-portal.md).</span><span class="sxs-lookup"><span data-stu-id="aeacb-234">For details on editing these entities in the Data Factory UI, see [the Azure portal version of this tutorial](tutorial-copy-data-portal.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="aeacb-235">Next steps</span><span class="sxs-lookup"><span data-stu-id="aeacb-235">Next steps</span></span>
<span data-ttu-id="aeacb-236">The pipeline in this sample copies data from Blob storage to a SQL database.</span><span class="sxs-lookup"><span data-stu-id="aeacb-236">The pipeline in this sample copies data from Blob storage to a SQL database.</span></span> <span data-ttu-id="aeacb-237">You learned how to:</span><span class="sxs-lookup"><span data-stu-id="aeacb-237">You learned how to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="aeacb-238">Create a data factory.</span><span class="sxs-lookup"><span data-stu-id="aeacb-238">Create a data factory.</span></span>
> * <span data-ttu-id="aeacb-239">Use the Copy Data tool to create a pipeline.</span><span class="sxs-lookup"><span data-stu-id="aeacb-239">Use the Copy Data tool to create a pipeline.</span></span>
> * <span data-ttu-id="aeacb-240">Monitor the pipeline and activity runs.</span><span class="sxs-lookup"><span data-stu-id="aeacb-240">Monitor the pipeline and activity runs.</span></span>

<span data-ttu-id="aeacb-241">Advance to the following tutorial to learn how to copy data from on-premises to the cloud:</span><span class="sxs-lookup"><span data-stu-id="aeacb-241">Advance to the following tutorial to learn how to copy data from on-premises to the cloud:</span></span> 

> [!div class="nextstepaction"]
>[<span data-ttu-id="aeacb-242">Copy data from on-premises to the cloud</span><span class="sxs-lookup"><span data-stu-id="aeacb-242">Copy data from on-premises to the cloud</span></span>](tutorial-hybrid-copy-data-tool.md)
