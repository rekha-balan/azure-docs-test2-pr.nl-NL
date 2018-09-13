---
title: Copy on-premises data by using the Azure Copy Data tool | Microsoft Docs
description: Create an Azure data factory and then use the Copy Data tool to copy data from an on-premises SQL Server database to Azure Blob storage.
services: data-factory
documentationcenter: ''
author: linda33wj
manager: craigg
ms.reviewer: douglasl
ms.service: data-factory
ms.workload: data-services
ms.topic: tutorial
ms.date: 01/04/2018
ms.author: jingwang
ms.openlocfilehash: a6c17fc897dae765f9789840262cb001d598b731
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857298"
---
# <a name="copy-data-from-an-on-premises-sql-server-database-to-azure-blob-storage-by-using-the-copy-data-tool"></a><span data-ttu-id="b1d0d-103">Copy data from an on-premises SQL Server database to Azure Blob storage by using the Copy Data tool</span><span class="sxs-lookup"><span data-stu-id="b1d0d-103">Copy data from an on-premises SQL Server database to Azure Blob storage by using the Copy Data tool</span></span>
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Version 1](v1/data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [Current version](tutorial-hybrid-copy-data-tool.md)

<span data-ttu-id="b1d0d-106">In this tutorial, you use the Azure portal to create a data factory.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-106">In this tutorial, you use the Azure portal to create a data factory.</span></span> <span data-ttu-id="b1d0d-107">Then, you use the Copy Data tool to create a pipeline that copies data from an on-premises SQL Server database to Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-107">Then, you use the Copy Data tool to create a pipeline that copies data from an on-premises SQL Server database to Azure Blob storage.</span></span>

> [!NOTE]
> - If you're new to Azure Data Factory, see [Introduction to Data Factory](introduction.md).
In this tutorial, you perform the following steps:

> [!div class="checklist"]
> * <span data-ttu-id="b1d0d-110">Create a data factory.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-110">Create a data factory.</span></span>
> * <span data-ttu-id="b1d0d-111">Use the Copy Data tool to create a pipeline.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-111">Use the Copy Data tool to create a pipeline.</span></span>
> * <span data-ttu-id="b1d0d-112">Monitor the pipeline and activity runs.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-112">Monitor the pipeline and activity runs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b1d0d-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b1d0d-113">Prerequisites</span></span>
### <a name="azure-subscription"></a><span data-ttu-id="b1d0d-114">Azure subscription</span><span class="sxs-lookup"><span data-stu-id="b1d0d-114">Azure subscription</span></span>
<span data-ttu-id="b1d0d-115">Before you begin, if you don't already have an Azure subscription, [create a free account](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="b1d0d-115">Before you begin, if you don't already have an Azure subscription, [create a free account](https://azure.microsoft.com/free/).</span></span>

### <a name="azure-roles"></a><span data-ttu-id="b1d0d-116">Azure roles</span><span class="sxs-lookup"><span data-stu-id="b1d0d-116">Azure roles</span></span>
<span data-ttu-id="b1d0d-117">To create data factory instances, the user account you use to log in to Azure must be assigned a *Contributor* or *Owner* role or must be an *administrator* of the Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-117">To create data factory instances, the user account you use to log in to Azure must be assigned a *Contributor* or *Owner* role or must be an *administrator* of the Azure subscription.</span></span> 

<span data-ttu-id="b1d0d-118">To view the permissions you have in the subscription, go to the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-118">To view the permissions you have in the subscription, go to the Azure portal.</span></span> <span data-ttu-id="b1d0d-119">Select your user name in the upper-right corner, and then select **Permissions**.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-119">Select your user name in the upper-right corner, and then select **Permissions**.</span></span> <span data-ttu-id="b1d0d-120">If you have access to multiple subscriptions, select the appropriate subscription.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-120">If you have access to multiple subscriptions, select the appropriate subscription.</span></span> <span data-ttu-id="b1d0d-121">For sample instructions on how to add a user to a role, see [Manage access using RBAC and the Azure portal](../role-based-access-control/role-assignments-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b1d0d-121">For sample instructions on how to add a user to a role, see [Manage access using RBAC and the Azure portal](../role-based-access-control/role-assignments-portal.md).</span></span>

### <a name="sql-server-2014-2016-and-2017"></a><span data-ttu-id="b1d0d-122">SQL Server 2014, 2016, and 2017</span><span class="sxs-lookup"><span data-stu-id="b1d0d-122">SQL Server 2014, 2016, and 2017</span></span>
<span data-ttu-id="b1d0d-123">In this tutorial, you use an on-premises SQL Server database as a *source* data store.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-123">In this tutorial, you use an on-premises SQL Server database as a *source* data store.</span></span> <span data-ttu-id="b1d0d-124">The pipeline in the data factory you create in this tutorial copies data from this on-premises SQL Server database (source) to Blob storage (sink).</span><span class="sxs-lookup"><span data-stu-id="b1d0d-124">The pipeline in the data factory you create in this tutorial copies data from this on-premises SQL Server database (source) to Blob storage (sink).</span></span> <span data-ttu-id="b1d0d-125">You then create a table named **emp** in your SQL Server database and insert a couple of sample entries into the table.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-125">You then create a table named **emp** in your SQL Server database and insert a couple of sample entries into the table.</span></span> 

1. <span data-ttu-id="b1d0d-126">Start SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-126">Start SQL Server Management Studio.</span></span> <span data-ttu-id="b1d0d-127">If it's not already installed on your machine, go to [Download SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span><span class="sxs-lookup"><span data-stu-id="b1d0d-127">If it's not already installed on your machine, go to [Download SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span></span> 

1. <span data-ttu-id="b1d0d-128">Connect to your SQL Server instance by using your credentials.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-128">Connect to your SQL Server instance by using your credentials.</span></span> 

1. <span data-ttu-id="b1d0d-129">Create a sample database.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-129">Create a sample database.</span></span> <span data-ttu-id="b1d0d-130">In the tree view, right-click **Databases**, and then select **New Database**.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-130">In the tree view, right-click **Databases**, and then select **New Database**.</span></span> 

1. <span data-ttu-id="b1d0d-131">In the **New Database** window, enter a name for the database, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-131">In the **New Database** window, enter a name for the database, and then select **OK**.</span></span> 

1. <span data-ttu-id="b1d0d-132">To create the **emp** table and insert some sample data into it, run the following query script against the database.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-132">To create the **emp** table and insert some sample data into it, run the following query script against the database.</span></span> <span data-ttu-id="b1d0d-133">In the tree view, right-click the database that you created, and then select **New Query**.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-133">In the tree view, right-click the database that you created, and then select **New Query**.</span></span>

    ```sql
    CREATE TABLE dbo.emp
    (
        ID int IDENTITY(1,1) NOT NULL,
        FirstName varchar(50),
        LastName varchar(50)
    )
    GO
    
    INSERT INTO emp (FirstName, LastName) VALUES ('John', 'Doe')
    INSERT INTO emp (FirstName, LastName) VALUES ('Jane', 'Doe')
    GO
    ```

### <a name="azure-storage-account"></a><span data-ttu-id="b1d0d-134">Azure storage account</span><span class="sxs-lookup"><span data-stu-id="b1d0d-134">Azure storage account</span></span>
<span data-ttu-id="b1d0d-135">In this tutorial, you use a general-purpose Azure storage account (specifically, Blob storage) as a destination/sink data store.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-135">In this tutorial, you use a general-purpose Azure storage account (specifically, Blob storage) as a destination/sink data store.</span></span> <span data-ttu-id="b1d0d-136">If you don't have a general-purpose storage account, see [Create a storage account](../storage/common/storage-quickstart-create-account.md) for instructions to create one.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-136">If you don't have a general-purpose storage account, see [Create a storage account](../storage/common/storage-quickstart-create-account.md) for instructions to create one.</span></span> <span data-ttu-id="b1d0d-137">The pipeline in the data factory you that create in this tutorial copies data from the on-premises SQL Server database (source) to this Blob storage (sink).</span><span class="sxs-lookup"><span data-stu-id="b1d0d-137">The pipeline in the data factory you that create in this tutorial copies data from the on-premises SQL Server database (source) to this Blob storage (sink).</span></span> 

#### <a name="get-the-storage-account-name-and-account-key"></a><span data-ttu-id="b1d0d-138">Get the storage account name and account key</span><span class="sxs-lookup"><span data-stu-id="b1d0d-138">Get the storage account name and account key</span></span>
<span data-ttu-id="b1d0d-139">You use the name and key of your storage account in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-139">You use the name and key of your storage account in this tutorial.</span></span> <span data-ttu-id="b1d0d-140">To get the name and key of your storage account, take the following steps:</span><span class="sxs-lookup"><span data-stu-id="b1d0d-140">To get the name and key of your storage account, take the following steps:</span></span> 

1. <span data-ttu-id="b1d0d-141">Sign in to the [Azure portal](https://portal.azure.com) with your Azure user name and password.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-141">Sign in to the [Azure portal](https://portal.azure.com) with your Azure user name and password.</span></span> 

1. <span data-ttu-id="b1d0d-142">In the left pane, select **More services**.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-142">In the left pane, select **More services**.</span></span> <span data-ttu-id="b1d0d-143">Filter by using the **Storage** keyword, and then select **Storage accounts**.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-143">Filter by using the **Storage** keyword, and then select **Storage accounts**.</span></span>

    ![Storage account search](media/tutorial-hybrid-copy-powershell/search-storage-account.png)

1. <span data-ttu-id="b1d0d-145">In the list of storage accounts, filter for your storage account, if needed.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-145">In the list of storage accounts, filter for your storage account, if needed.</span></span> <span data-ttu-id="b1d0d-146">Then select your storage account.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-146">Then select your storage account.</span></span> 

1. <span data-ttu-id="b1d0d-147">In the **Storage account** window, select **Access keys**.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-147">In the **Storage account** window, select **Access keys**.</span></span>

    ![Access keys](media/tutorial-hybrid-copy-powershell/storage-account-name-key.png)

1. <span data-ttu-id="b1d0d-149">In the **Storage account name** and **key1** boxes, copy the values, and then paste them into Notepad or another editor for later use in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-149">In the **Storage account name** and **key1** boxes, copy the values, and then paste them into Notepad or another editor for later use in the tutorial.</span></span> 

#### <a name="create-the-adftutorial-container"></a><span data-ttu-id="b1d0d-150">Create the adftutorial container</span><span class="sxs-lookup"><span data-stu-id="b1d0d-150">Create the adftutorial container</span></span> 
<span data-ttu-id="b1d0d-151">In this section, you create a blob container named **adftutorial** in your Blob storage.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-151">In this section, you create a blob container named **adftutorial** in your Blob storage.</span></span> 

1. <span data-ttu-id="b1d0d-152">In the **Storage account** window, switch to **Overview**, and then select **Blobs**.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-152">In the **Storage account** window, switch to **Overview**, and then select **Blobs**.</span></span> 

    ![Select Blobs option](media/tutorial-hybrid-copy-powershell/select-blobs.png)

1. <span data-ttu-id="b1d0d-154">In the **Blob service** window, select **Container**.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-154">In the **Blob service** window, select **Container**.</span></span> 

    ![Container button](media/tutorial-hybrid-copy-powershell/add-container-button.png)

1. <span data-ttu-id="b1d0d-156">In the **New container** window, in the **Name** box, enter **adftutorial**, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-156">In the **New container** window, in the **Name** box, enter **adftutorial**, and then select **OK**.</span></span> 

    ![New container](media/tutorial-hybrid-copy-powershell/new-container-dialog.png)

1. <span data-ttu-id="b1d0d-158">In the list of containers, select **adftutorial**.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-158">In the list of containers, select **adftutorial**.</span></span>

    ![Container selection](media/tutorial-hybrid-copy-powershell/seelct-adftutorial-container.png)

1. <span data-ttu-id="b1d0d-160">Keep the **Container** window for **adftutorial** open.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-160">Keep the **Container** window for **adftutorial** open.</span></span> <span data-ttu-id="b1d0d-161">You use it verify the output at the end of the tutorial.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-161">You use it verify the output at the end of the tutorial.</span></span> <span data-ttu-id="b1d0d-162">Data Factory automatically creates the output folder in this container, so you don't need to create one.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-162">Data Factory automatically creates the output folder in this container, so you don't need to create one.</span></span>

    ![Container window](media/tutorial-hybrid-copy-powershell/container-page.png)


## <a name="create-a-data-factory"></a><span data-ttu-id="b1d0d-164">Create a data factory</span><span class="sxs-lookup"><span data-stu-id="b1d0d-164">Create a data factory</span></span>

1. <span data-ttu-id="b1d0d-165">On the menu on the left, select **New** > **Data + Analytics** > **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-165">On the menu on the left, select **New** > **Data + Analytics** > **Data Factory**.</span></span> 
  
   ![New data factory creation](./media/tutorial-hybrid-copy-data-tool/new-azure-data-factory-menu.png)
1. <span data-ttu-id="b1d0d-167">On the **New data factory** page, under **Name**, enter **ADFTutorialDataFactory**.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-167">On the **New data factory** page, under **Name**, enter **ADFTutorialDataFactory**.</span></span> 
   
     ![New data factory](./media/tutorial-hybrid-copy-data-tool/new-azure-data-factory.png)

   <span data-ttu-id="b1d0d-169">The name of the data factory must be *globally unique*.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-169">The name of the data factory must be *globally unique*.</span></span> <span data-ttu-id="b1d0d-170">If you see the following error message for the name field, change the name of the data factory (for example, yournameADFTutorialDataFactory).</span><span class="sxs-lookup"><span data-stu-id="b1d0d-170">If you see the following error message for the name field, change the name of the data factory (for example, yournameADFTutorialDataFactory).</span></span> <span data-ttu-id="b1d0d-171">For naming rules for Data Factory artifacts, see [Data Factory naming rules](naming-rules.md).</span><span class="sxs-lookup"><span data-stu-id="b1d0d-171">For naming rules for Data Factory artifacts, see [Data Factory naming rules](naming-rules.md).</span></span>

   ![New data factory name](./media/tutorial-hybrid-copy-data-tool/name-not-available-error.png)
1. <span data-ttu-id="b1d0d-173">Select the Azure **subscription** in which you want to create the data factory.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-173">Select the Azure **subscription** in which you want to create the data factory.</span></span> 
1. <span data-ttu-id="b1d0d-174">For **Resource Group**, take one of the following steps:</span><span class="sxs-lookup"><span data-stu-id="b1d0d-174">For **Resource Group**, take one of the following steps:</span></span>
  
      - <span data-ttu-id="b1d0d-175">Select **Use existing**, and select an existing resource group from the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-175">Select **Use existing**, and select an existing resource group from the drop-down list.</span></span>

      - <span data-ttu-id="b1d0d-176">Select **Create new**, and enter the name of a resource group.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-176">Select **Create new**, and enter the name of a resource group.</span></span> 
        
      <span data-ttu-id="b1d0d-177">To learn about resource groups, see [Use resource groups to manage your Azure resources](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b1d0d-177">To learn about resource groups, see [Use resource groups to manage your Azure resources](../azure-resource-manager/resource-group-overview.md).</span></span>
1. <span data-ttu-id="b1d0d-178">Under **Version**, select \*\*V2 \*\*.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-178">Under **Version**, select \*\*V2 \*\*.</span></span>
1. <span data-ttu-id="b1d0d-179">Under **Location**, select the location for the data factory.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-179">Under **Location**, select the location for the data factory.</span></span> <span data-ttu-id="b1d0d-180">Only locations that are supported are displayed in the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-180">Only locations that are supported are displayed in the drop-down list.</span></span> <span data-ttu-id="b1d0d-181">The data stores (for example, Azure Storage and SQL Database) and computes (for example, Azure HDInsight) used by Data Factory can be in other locations/regions.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-181">The data stores (for example, Azure Storage and SQL Database) and computes (for example, Azure HDInsight) used by Data Factory can be in other locations/regions.</span></span>
1. <span data-ttu-id="b1d0d-182">Select **Pin to dashboard**.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-182">Select **Pin to dashboard**.</span></span> 
1. <span data-ttu-id="b1d0d-183">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-183">Select **Create**.</span></span>
1. <span data-ttu-id="b1d0d-184">On the dashboard, you see the following tile with the status **Deploying Data Factory**:</span><span class="sxs-lookup"><span data-stu-id="b1d0d-184">On the dashboard, you see the following tile with the status **Deploying Data Factory**:</span></span>

    ![Deploying data factory tile](media/tutorial-hybrid-copy-data-tool/deploying-data-factory.png)
1. <span data-ttu-id="b1d0d-186">After the creation is finished, you see the **Data Factory** page as shown in the image.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-186">After the creation is finished, you see the **Data Factory** page as shown in the image.</span></span>
  
    ![Data factory home page](./media/tutorial-hybrid-copy-data-tool/data-factory-home-page.png)
1. <span data-ttu-id="b1d0d-188">Select **Author & Monitor** to launch the Data Factory user interface in a separate tab.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-188">Select **Author & Monitor** to launch the Data Factory user interface in a separate tab.</span></span> 

## <a name="use-the-copy-data-tool-to-create-a-pipeline"></a><span data-ttu-id="b1d0d-189">Use the Copy Data tool to create a pipeline</span><span class="sxs-lookup"><span data-stu-id="b1d0d-189">Use the Copy Data tool to create a pipeline</span></span>

1. <span data-ttu-id="b1d0d-190">On the **Let's get started** page, select **Copy Data** to launch the Copy Data tool.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-190">On the **Let's get started** page, select **Copy Data** to launch the Copy Data tool.</span></span> 

   ![Copy Data tool tile](./media/tutorial-hybrid-copy-data-tool/copy-data-tool-tile.png)

1. <span data-ttu-id="b1d0d-192">On the **Properties** page of the Copy Data tool, under **Task name**, enter **CopyFromOnPremSqlToAzureBlobPipeline**.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-192">On the **Properties** page of the Copy Data tool, under **Task name**, enter **CopyFromOnPremSqlToAzureBlobPipeline**.</span></span> <span data-ttu-id="b1d0d-193">Then select **Next**.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-193">Then select **Next**.</span></span> <span data-ttu-id="b1d0d-194">The Copy Data tool creates a pipeline with the name you specify for this field.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-194">The Copy Data tool creates a pipeline with the name you specify for this field.</span></span> 

   ![Task name](./media/tutorial-hybrid-copy-data-tool/properties-page.png)

1. <span data-ttu-id="b1d0d-196">On the **Source data store** page, click on **Create new connection**.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-196">On the **Source data store** page, click on **Create new connection**.</span></span> 

   ![Create new linked service](./media/tutorial-hybrid-copy-data-tool/create-new-source-data-store.png)

1. <span data-ttu-id="b1d0d-198">Under **New Linked Service**, search for **SQL Server**, and then select **Next**.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-198">Under **New Linked Service**, search for **SQL Server**, and then select **Next**.</span></span> 

   ![SQL Server selection](./media/tutorial-hybrid-copy-data-tool/select-source-data-store.png)

1. <span data-ttu-id="b1d0d-200">Under New Linked Service (SQL Server) \*\*Name\*\*\*\*, enter **SqlServerLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-200">Under New Linked Service (SQL Server) \*\*Name\*\*\*\*, enter **SqlServerLinkedService**.</span></span> <span data-ttu-id="b1d0d-201">Select **+New** under **Connect via integration runtime**.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-201">Select **+New** under **Connect via integration runtime**.</span></span> <span data-ttu-id="b1d0d-202">You must create a self-hosted integration runtime, download it to your machine, and register it with Data Factory.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-202">You must create a self-hosted integration runtime, download it to your machine, and register it with Data Factory.</span></span> <span data-ttu-id="b1d0d-203">The self-hosted integration runtime copies data between your on-premises environment and the cloud.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-203">The self-hosted integration runtime copies data between your on-premises environment and the cloud.</span></span>

   ![Create self-hosted integration runtime](./media/tutorial-hybrid-copy-data-tool/create-integration-runtime-link.png)

1. <span data-ttu-id="b1d0d-205">In the **Integration Runtime Setup** dialog box, Select **Private Network**.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-205">In the **Integration Runtime Setup** dialog box, Select **Private Network**.</span></span> <span data-ttu-id="b1d0d-206">Then select **Next**.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-206">Then select **Next**.</span></span> 

   ![](./media/tutorial-hybrid-copy-data-tool/create-integration-runtime-dialog0.png)

1. <span data-ttu-id="b1d0d-207">In the **Integration Runtime Setup** dialog box under **Name**, enter **TutorialIntegrationRuntime**.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-207">In the **Integration Runtime Setup** dialog box under **Name**, enter **TutorialIntegrationRuntime**.</span></span> <span data-ttu-id="b1d0d-208">Then select **Next**.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-208">Then select **Next**.</span></span> 

   ![Integration runtime name](./media/tutorial-hybrid-copy-data-tool/create-integration-runtime-dialog.png)

1. <span data-ttu-id="b1d0d-210">Select **Click here to launch the express setup for this computer**.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-210">Select **Click here to launch the express setup for this computer**.</span></span> <span data-ttu-id="b1d0d-211">This action installs the integration runtime on your machine and registers it with Data Factory.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-211">This action installs the integration runtime on your machine and registers it with Data Factory.</span></span> <span data-ttu-id="b1d0d-212">Alternatively, you can use the manual setup option to download the installation file, run it, and use the key to register the integration runtime.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-212">Alternatively, you can use the manual setup option to download the installation file, run it, and use the key to register the integration runtime.</span></span> 

    ![lLaunch express setup on this computer link](./media/tutorial-hybrid-copy-data-tool/launch-express-setup-link.png)

1. <span data-ttu-id="b1d0d-214">Run the downloaded application.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-214">Run the downloaded application.</span></span> <span data-ttu-id="b1d0d-215">You see the status of the express setup in the window.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-215">You see the status of the express setup in the window.</span></span> 

    ![Express setup status](./media/tutorial-hybrid-copy-data-tool/express-setup-status.png)

1. <span data-ttu-id="b1d0d-217">Confirm that **TutorialIntegrationRuntime** is selected for the **Integration Runtime** field.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-217">Confirm that **TutorialIntegrationRuntime** is selected for the **Integration Runtime** field.</span></span>

    ![Integration runtime selected](./media/tutorial-hybrid-copy-data-tool/integration-runtime-selected.png)

1. <span data-ttu-id="b1d0d-219">In **Specify the on-premises SQL Server database**, take the following steps:</span><span class="sxs-lookup"><span data-stu-id="b1d0d-219">In **Specify the on-premises SQL Server database**, take the following steps:</span></span> 

      <span data-ttu-id="b1d0d-220">a.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-220">a.</span></span> <span data-ttu-id="b1d0d-221">Under **Name**, enter **SqlServerLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-221">Under **Name**, enter **SqlServerLinkedService**.</span></span>

      <span data-ttu-id="b1d0d-222">b.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-222">b.</span></span> <span data-ttu-id="b1d0d-223">Under **Server name**, enter the name of your on-premises SQL Server instance.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-223">Under **Server name**, enter the name of your on-premises SQL Server instance.</span></span>

      <span data-ttu-id="b1d0d-224">c.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-224">c.</span></span> <span data-ttu-id="b1d0d-225">Under **Database name**, enter the name of your on-premises database.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-225">Under **Database name**, enter the name of your on-premises database.</span></span>

      <span data-ttu-id="b1d0d-226">d.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-226">d.</span></span> <span data-ttu-id="b1d0d-227">Under **Authentication type**, select appropriate authentication.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-227">Under **Authentication type**, select appropriate authentication.</span></span>

      <span data-ttu-id="b1d0d-228">e.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-228">e.</span></span> <span data-ttu-id="b1d0d-229">Under **User name**, enter the name of user with access to on-premises SQL Server.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-229">Under **User name**, enter the name of user with access to on-premises SQL Server.</span></span>

      <span data-ttu-id="b1d0d-230">f.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-230">f.</span></span> <span data-ttu-id="b1d0d-231">Enter the **password** for the user.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-231">Enter the **password** for the user.</span></span> <span data-ttu-id="b1d0d-232">Select **Finish**.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-232">Select **Finish**.</span></span> 

1. <span data-ttu-id="b1d0d-233">Select **Next**.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-233">Select **Next**.</span></span>

     ![](./media/tutorial-hybrid-copy-data-tool/select-source-linked-service.png)

1. <span data-ttu-id="b1d0d-234">On the **Select tables from which to copy the data or use a custom query** page, select the **[dbo].[emp]** table in the list, and select **Next**.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-234">On the **Select tables from which to copy the data or use a custom query** page, select the **[dbo].[emp]** table in the list, and select **Next**.</span></span> <span data-ttu-id="b1d0d-235">You can select any other table based on your database.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-235">You can select any other table based on your database.</span></span>

     ![The Product table selection](./media/tutorial-hybrid-copy-data-tool/select-emp-table.png)

1. <span data-ttu-id="b1d0d-237">On the **Destination data store** page, select **Create new connection**</span><span class="sxs-lookup"><span data-stu-id="b1d0d-237">On the **Destination data store** page, select **Create new connection**</span></span>

     <span data-ttu-id="b1d0d-238">//image create-new-sink-connection.png</span><span class="sxs-lookup"><span data-stu-id="b1d0d-238">//image create-new-sink-connection.png</span></span>

     ![Create Destination linked service](./media/tutorial-hybrid-copy-data-tool/create-new-sink-connection.png)

1. <span data-ttu-id="b1d0d-240">In **New Linked Service**, Search and Select **Azure Blob**, then **Continue**.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-240">In **New Linked Service**, Search and Select **Azure Blob**, then **Continue**.</span></span> 

     ![Blob storage selection](./media/tutorial-hybrid-copy-data-tool/select-destination-data-store.png)

1. <span data-ttu-id="b1d0d-242">On the **New Linked Service (Azure Blob Storage)** dialog, take the following steps:</span><span class="sxs-lookup"><span data-stu-id="b1d0d-242">On the **New Linked Service (Azure Blob Storage)** dialog, take the following steps:</span></span> 

     <span data-ttu-id="b1d0d-243">a.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-243">a.</span></span> <span data-ttu-id="b1d0d-244">Under \*\*Name\*\*\*\*, enter **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-244">Under \*\*Name\*\*\*\*, enter **AzureStorageLinkedService**.</span></span>

     <span data-ttu-id="b1d0d-245">b.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-245">b.</span></span> <span data-ttu-id="b1d0d-246">Under **Connect via integration runtime**, select **TutorialIntegrationRuntime**</span><span class="sxs-lookup"><span data-stu-id="b1d0d-246">Under **Connect via integration runtime**, select **TutorialIntegrationRuntime**</span></span>

     <span data-ttu-id="b1d0d-247">c.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-247">c.</span></span> <span data-ttu-id="b1d0d-248">Under **Storage account name**, select your storage account from the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-248">Under **Storage account name**, select your storage account from the drop-down list.</span></span> 

     <span data-ttu-id="b1d0d-249">d.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-249">d.</span></span> <span data-ttu-id="b1d0d-250">Select **Next**.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-250">Select **Next**.</span></span>

     ![Specify the storage account](./media/tutorial-hybrid-copy-data-tool/specify-azure-blob-storage-account.png)

1. <span data-ttu-id="b1d0d-252">In **Destination data store** dialog, select **Next**.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-252">In **Destination data store** dialog, select **Next**.</span></span> <span data-ttu-id="b1d0d-253">In **Connection properties**, select **Azure storage service** as **Azure Blob Storage**.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-253">In **Connection properties**, select **Azure storage service** as **Azure Blob Storage**.</span></span> <span data-ttu-id="b1d0d-254">Select **Next**.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-254">Select **Next**.</span></span> 

     ![connection properties](./media/tutorial-hybrid-copy-data-tool/select-connection-properties.png)

1. <span data-ttu-id="b1d0d-256">In the **Choose the output file or folder** dialog, under **Folder path**, enter **adftutorial/fromonprem**.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-256">In the **Choose the output file or folder** dialog, under **Folder path**, enter **adftutorial/fromonprem**.</span></span> <span data-ttu-id="b1d0d-257">You created the **adftutorial** container as part of the prerequisites.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-257">You created the **adftutorial** container as part of the prerequisites.</span></span> <span data-ttu-id="b1d0d-258">If the output folder doesn't exist (in this case **fromonprem**), Data Factory automatically creates it.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-258">If the output folder doesn't exist (in this case **fromonprem**), Data Factory automatically creates it.</span></span> <span data-ttu-id="b1d0d-259">You also can use the **Browse** button to browse the blob storage and its containers/folders.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-259">You also can use the **Browse** button to browse the blob storage and its containers/folders.</span></span> <span data-ttu-id="b1d0d-260">If you do not specify any value under **File name**, by default the name from the source would be used (in this case **dbo.emp**).</span><span class="sxs-lookup"><span data-stu-id="b1d0d-260">If you do not specify any value under **File name**, by default the name from the source would be used (in this case **dbo.emp**).</span></span>
           
     ![Choose the output file or folder](./media/tutorial-hybrid-copy-data-tool/choose-output-file-folder.png)

1. <span data-ttu-id="b1d0d-262">On the **File format settings** dialog, select **Next**.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-262">On the **File format settings** dialog, select **Next**.</span></span> 

     ![File format settings page](./media/tutorial-hybrid-copy-data-tool/file-format-settings-page.png)

1. <span data-ttu-id="b1d0d-264">On the **Settings** dialog, select **Next**.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-264">On the **Settings** dialog, select **Next**.</span></span> 

     ![Settings page](./media/tutorial-hybrid-copy-data-tool/settings-page.png)

1. <span data-ttu-id="b1d0d-266">On the **Summary** dialog, review values for all the settings, and select **Next**.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-266">On the **Summary** dialog, review values for all the settings, and select **Next**.</span></span> 

     ![Summary page](./media/tutorial-hybrid-copy-data-tool/summary-page.png)

1. <span data-ttu-id="b1d0d-268">On the **Deployment** page, select **Monitor** to monitor the pipeline or task you created.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-268">On the **Deployment** page, select **Monitor** to monitor the pipeline or task you created.</span></span>

     ![Deployment page](./media/tutorial-hybrid-copy-data-tool/deployment-page.png)

1. <span data-ttu-id="b1d0d-270">On the **Monitor** tab, you can view the status of the pipeline you created.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-270">On the **Monitor** tab, you can view the status of the pipeline you created.</span></span> <span data-ttu-id="b1d0d-271">You can use the links in the **Action** column to view activity runs associated with the pipeline run and to rerun the pipeline.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-271">You can use the links in the **Action** column to view activity runs associated with the pipeline run and to rerun the pipeline.</span></span> 

     ![Monitor pipeline runs](./media/tutorial-hybrid-copy-data-tool/monitor-pipeline-runs.png)

1. <span data-ttu-id="b1d0d-273">Select the **View Activity Runs** link in the **Actions** column to see activity runs associated with the pipeline run.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-273">Select the **View Activity Runs** link in the **Actions** column to see activity runs associated with the pipeline run.</span></span> <span data-ttu-id="b1d0d-274">To see details about the copy operation, select the **Details** link (eyeglasses icon) in the **Actions** column.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-274">To see details about the copy operation, select the **Details** link (eyeglasses icon) in the **Actions** column.</span></span> <span data-ttu-id="b1d0d-275">To switch back to the **Pipeline Runs** view, select **Pipelines** at the top.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-275">To switch back to the **Pipeline Runs** view, select **Pipelines** at the top.</span></span>

     ![Monitor activity runs](./media/tutorial-hybrid-copy-data-tool/monitor-activity-runs.png)

1. <span data-ttu-id="b1d0d-277">Confirm that you see the output file in the **fromonprem** folder of the **adftutorial** container.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-277">Confirm that you see the output file in the **fromonprem** folder of the **adftutorial** container.</span></span> 

     ![Output blob](./media/tutorial-hybrid-copy-data-tool/output-blob.png)

1. <span data-ttu-id="b1d0d-279">Select the **Edit** tab on the left to switch to the editor mode.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-279">Select the **Edit** tab on the left to switch to the editor mode.</span></span> <span data-ttu-id="b1d0d-280">You can update the linked services, datasets, and pipelines created by the tool by using the editor.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-280">You can update the linked services, datasets, and pipelines created by the tool by using the editor.</span></span> <span data-ttu-id="b1d0d-281">Select **Code** to view the JSON code associated with the entity opened in the editor.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-281">Select **Code** to view the JSON code associated with the entity opened in the editor.</span></span> <span data-ttu-id="b1d0d-282">For details on how to edit these entities in the Data Factory UI, see [the Azure portal version of this tutorial](tutorial-copy-data-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b1d0d-282">For details on how to edit these entities in the Data Factory UI, see [the Azure portal version of this tutorial](tutorial-copy-data-portal.md).</span></span>

     ![Edit tab](./media/tutorial-hybrid-copy-data-tool/edit-tab.png)


## <a name="next-steps"></a><span data-ttu-id="b1d0d-284">Next steps</span><span class="sxs-lookup"><span data-stu-id="b1d0d-284">Next steps</span></span>
<span data-ttu-id="b1d0d-285">The pipeline in this sample copies data from an on-premises SQL Server database to Blob storage.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-285">The pipeline in this sample copies data from an on-premises SQL Server database to Blob storage.</span></span> <span data-ttu-id="b1d0d-286">You learned how to:</span><span class="sxs-lookup"><span data-stu-id="b1d0d-286">You learned how to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="b1d0d-287">Create a data factory.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-287">Create a data factory.</span></span>
> * <span data-ttu-id="b1d0d-288">Use the Copy Data tool to create a pipeline.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-288">Use the Copy Data tool to create a pipeline.</span></span>
> * <span data-ttu-id="b1d0d-289">Monitor the pipeline and activity runs.</span><span class="sxs-lookup"><span data-stu-id="b1d0d-289">Monitor the pipeline and activity runs.</span></span>

<span data-ttu-id="b1d0d-290">For a list of data stores that are supported by Data Factory, see [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="b1d0d-290">For a list of data stores that are supported by Data Factory, see [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span></span>

<span data-ttu-id="b1d0d-291">To learn about how to copy data in bulk from a source to a destination, advance to the following tutorial:</span><span class="sxs-lookup"><span data-stu-id="b1d0d-291">To learn about how to copy data in bulk from a source to a destination, advance to the following tutorial:</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="b1d0d-292">Copy data in bulk</span><span class="sxs-lookup"><span data-stu-id="b1d0d-292">Copy data in bulk</span></span>](tutorial-bulk-copy-portal.md)
