---
title: Use the Azure portal to create a data factory pipeline | Microsoft Docs
description: This tutorial provides step-by-step instructions for using the Azure portal to create a data factory with a pipeline. The pipeline uses the copy activity to copy data from Azure Blob storage to a SQL database.
services: data-factory
documentationcenter: ''
author: linda33wj
manager: craigg
ms.reviewer: douglasl
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 06/21/2018
ms.author: jingwang
ms.openlocfilehash: f7d6f34c75069f91e06d58c960249d040b2bda8a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857623"
---
# <a name="copy-data-from-azure-blob-storage-to-a-sql-database-by-using-azure-data-factory"></a><span data-ttu-id="f33d3-104">Copy data from Azure Blob storage to a SQL database by using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="f33d3-104">Copy data from Azure Blob storage to a SQL database by using Azure Data Factory</span></span>
<span data-ttu-id="f33d3-105">In this tutorial, you create a data factory by using the Azure Data Factory user interface (UI).</span><span class="sxs-lookup"><span data-stu-id="f33d3-105">In this tutorial, you create a data factory by using the Azure Data Factory user interface (UI).</span></span> <span data-ttu-id="f33d3-106">The pipeline in this data factory copies data from Azure Blob storage to a SQL database.</span><span class="sxs-lookup"><span data-stu-id="f33d3-106">The pipeline in this data factory copies data from Azure Blob storage to a SQL database.</span></span> <span data-ttu-id="f33d3-107">The configuration pattern in this tutorial applies to copying from a file-based data store to a relational data store.</span><span class="sxs-lookup"><span data-stu-id="f33d3-107">The configuration pattern in this tutorial applies to copying from a file-based data store to a relational data store.</span></span> <span data-ttu-id="f33d3-108">For a list of data stores supported as sources and sinks, see the [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="f33d3-108">For a list of data stores supported as sources and sinks, see the [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span></span>

> [!NOTE]
> - <span data-ttu-id="f33d3-109">If you're new to Data Factory, see [Introduction to Azure Data Factory](introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f33d3-109">If you're new to Data Factory, see [Introduction to Azure Data Factory](introduction.md).</span></span>

<span data-ttu-id="f33d3-110">In this tutorial, you perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="f33d3-110">In this tutorial, you perform the following steps:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f33d3-111">Create a data factory.</span><span class="sxs-lookup"><span data-stu-id="f33d3-111">Create a data factory.</span></span>
> * <span data-ttu-id="f33d3-112">Create a pipeline with a copy activity.</span><span class="sxs-lookup"><span data-stu-id="f33d3-112">Create a pipeline with a copy activity.</span></span>
> * <span data-ttu-id="f33d3-113">Test run the pipeline.</span><span class="sxs-lookup"><span data-stu-id="f33d3-113">Test run the pipeline.</span></span>
> * <span data-ttu-id="f33d3-114">Trigger the pipeline manually.</span><span class="sxs-lookup"><span data-stu-id="f33d3-114">Trigger the pipeline manually.</span></span>
> * <span data-ttu-id="f33d3-115">Trigger the pipeline on a schedule.</span><span class="sxs-lookup"><span data-stu-id="f33d3-115">Trigger the pipeline on a schedule.</span></span>
> * <span data-ttu-id="f33d3-116">Monitor the pipeline and activity runs.</span><span class="sxs-lookup"><span data-stu-id="f33d3-116">Monitor the pipeline and activity runs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f33d3-117">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f33d3-117">Prerequisites</span></span>
* <span data-ttu-id="f33d3-118">**Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="f33d3-118">**Azure subscription**.</span></span> <span data-ttu-id="f33d3-119">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span><span class="sxs-lookup"><span data-stu-id="f33d3-119">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>
* <span data-ttu-id="f33d3-120">**Azure storage account**.</span><span class="sxs-lookup"><span data-stu-id="f33d3-120">**Azure storage account**.</span></span> <span data-ttu-id="f33d3-121">You use Blob storage as a *source* data store.</span><span class="sxs-lookup"><span data-stu-id="f33d3-121">You use Blob storage as a *source* data store.</span></span> <span data-ttu-id="f33d3-122">If you don't have a storage account, see [Create an Azure storage account](../storage/common/storage-quickstart-create-account.md) for steps to create one.</span><span class="sxs-lookup"><span data-stu-id="f33d3-122">If you don't have a storage account, see [Create an Azure storage account](../storage/common/storage-quickstart-create-account.md) for steps to create one.</span></span>
* <span data-ttu-id="f33d3-123">**Azure SQL Database**.</span><span class="sxs-lookup"><span data-stu-id="f33d3-123">**Azure SQL Database**.</span></span> <span data-ttu-id="f33d3-124">You use the database as a *sink* data store.</span><span class="sxs-lookup"><span data-stu-id="f33d3-124">You use the database as a *sink* data store.</span></span> <span data-ttu-id="f33d3-125">If you don't have a SQL database, see [Create a SQL database](../sql-database/sql-database-get-started-portal.md) for steps to create one.</span><span class="sxs-lookup"><span data-stu-id="f33d3-125">If you don't have a SQL database, see [Create a SQL database](../sql-database/sql-database-get-started-portal.md) for steps to create one.</span></span>

### <a name="create-a-blob-and-a-sql-table"></a><span data-ttu-id="f33d3-126">Create a blob and a SQL table</span><span class="sxs-lookup"><span data-stu-id="f33d3-126">Create a blob and a SQL table</span></span>

<span data-ttu-id="f33d3-127">Now, prepare your Blob storage and SQL database for the tutorial by performing the following steps.</span><span class="sxs-lookup"><span data-stu-id="f33d3-127">Now, prepare your Blob storage and SQL database for the tutorial by performing the following steps.</span></span>

#### <a name="create-a-source-blob"></a><span data-ttu-id="f33d3-128">Create a source blob</span><span class="sxs-lookup"><span data-stu-id="f33d3-128">Create a source blob</span></span>

1. <span data-ttu-id="f33d3-129">Launch Notepad.</span><span class="sxs-lookup"><span data-stu-id="f33d3-129">Launch Notepad.</span></span> <span data-ttu-id="f33d3-130">Copy the following text, and save it as an **emp.txt** file on your disk:</span><span class="sxs-lookup"><span data-stu-id="f33d3-130">Copy the following text, and save it as an **emp.txt** file on your disk:</span></span>

    ```
    John,Doe
    Jane,Doe
    ```

1. <span data-ttu-id="f33d3-131">Create a container named **adftutorial** in your Blob storage.</span><span class="sxs-lookup"><span data-stu-id="f33d3-131">Create a container named **adftutorial** in your Blob storage.</span></span> <span data-ttu-id="f33d3-132">Create a folder named **input** in this container.</span><span class="sxs-lookup"><span data-stu-id="f33d3-132">Create a folder named **input** in this container.</span></span> <span data-ttu-id="f33d3-133">Then, upload the **emp.txt** file to the **input** folder.</span><span class="sxs-lookup"><span data-stu-id="f33d3-133">Then, upload the **emp.txt** file to the **input** folder.</span></span> <span data-ttu-id="f33d3-134">Use the Azure portal or tools such as [Azure Storage Explorer](http://storageexplorer.com/) to do these tasks.</span><span class="sxs-lookup"><span data-stu-id="f33d3-134">Use the Azure portal or tools such as [Azure Storage Explorer](http://storageexplorer.com/) to do these tasks.</span></span>

#### <a name="create-a-sink-sql-table"></a><span data-ttu-id="f33d3-135">Create a sink SQL table</span><span class="sxs-lookup"><span data-stu-id="f33d3-135">Create a sink SQL table</span></span>

1. <span data-ttu-id="f33d3-136">Use the following SQL script to create the **dbo.emp** table in your SQL database:</span><span class="sxs-lookup"><span data-stu-id="f33d3-136">Use the following SQL script to create the **dbo.emp** table in your SQL database:</span></span>

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

1. <span data-ttu-id="f33d3-137">Allow Azure services to access SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f33d3-137">Allow Azure services to access SQL Server.</span></span> <span data-ttu-id="f33d3-138">Ensure that **Allow access to Azure services** is turned **ON** for your SQL Server so that Data Factory can write data to your SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f33d3-138">Ensure that **Allow access to Azure services** is turned **ON** for your SQL Server so that Data Factory can write data to your SQL Server.</span></span> <span data-ttu-id="f33d3-139">To verify and turn on this setting, take the following steps:</span><span class="sxs-lookup"><span data-stu-id="f33d3-139">To verify and turn on this setting, take the following steps:</span></span>

    <span data-ttu-id="f33d3-140">a.</span><span class="sxs-lookup"><span data-stu-id="f33d3-140">a.</span></span> <span data-ttu-id="f33d3-141">On the left, select **More services** > **SQL servers**.</span><span class="sxs-lookup"><span data-stu-id="f33d3-141">On the left, select **More services** > **SQL servers**.</span></span>

    <span data-ttu-id="f33d3-142">b.</span><span class="sxs-lookup"><span data-stu-id="f33d3-142">b.</span></span> <span data-ttu-id="f33d3-143">Select your server, and under **SETTINGS** select **Firewall**.</span><span class="sxs-lookup"><span data-stu-id="f33d3-143">Select your server, and under **SETTINGS** select **Firewall**.</span></span>

    <span data-ttu-id="f33d3-144">c.</span><span class="sxs-lookup"><span data-stu-id="f33d3-144">c.</span></span> <span data-ttu-id="f33d3-145">On the **Firewall settings** page, select **ON** for **Allow access to Azure services**.</span><span class="sxs-lookup"><span data-stu-id="f33d3-145">On the **Firewall settings** page, select **ON** for **Allow access to Azure services**.</span></span>

## <a name="create-a-data-factory"></a><span data-ttu-id="f33d3-146">Create a data factory</span><span class="sxs-lookup"><span data-stu-id="f33d3-146">Create a data factory</span></span>
<span data-ttu-id="f33d3-147">In this step, you create a data factory and start the Data Factory UI to create a pipeline in the data factory.</span><span class="sxs-lookup"><span data-stu-id="f33d3-147">In this step, you create a data factory and start the Data Factory UI to create a pipeline in the data factory.</span></span> 

1. <span data-ttu-id="f33d3-148">Open the **Microsoft Edge** or **Google Chrome** web browser.</span><span class="sxs-lookup"><span data-stu-id="f33d3-148">Open the **Microsoft Edge** or **Google Chrome** web browser.</span></span> <span data-ttu-id="f33d3-149">Currently, Data Factory UI is supported only in Microsoft Edge and Google Chrome web browsers.</span><span class="sxs-lookup"><span data-stu-id="f33d3-149">Currently, Data Factory UI is supported only in Microsoft Edge and Google Chrome web browsers.</span></span>
1. <span data-ttu-id="f33d3-150">On the left menu, select **New** > **Data + Analytics** > **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="f33d3-150">On the left menu, select **New** > **Data + Analytics** > **Data Factory**.</span></span> 
  
   ![New data factory creation](./media/tutorial-copy-data-portal/new-azure-data-factory-menu.png)
1. <span data-ttu-id="f33d3-152">On the **New data factory** page, under **Name**, enter **ADFTutorialDataFactory**.</span><span class="sxs-lookup"><span data-stu-id="f33d3-152">On the **New data factory** page, under **Name**, enter **ADFTutorialDataFactory**.</span></span> 
      
     ![New data factory](./media/tutorial-copy-data-portal/new-azure-data-factory.png)
 
   <span data-ttu-id="f33d3-154">The name of the Azure data factory must be *globally unique*.</span><span class="sxs-lookup"><span data-stu-id="f33d3-154">The name of the Azure data factory must be *globally unique*.</span></span> <span data-ttu-id="f33d3-155">If you see the following error message for the name field, change the name of the data factory (for example, yournameADFTutorialDataFactory).</span><span class="sxs-lookup"><span data-stu-id="f33d3-155">If you see the following error message for the name field, change the name of the data factory (for example, yournameADFTutorialDataFactory).</span></span> <span data-ttu-id="f33d3-156">For naming rules for Data Factory artifacts, see [Data Factory naming rules](naming-rules.md).</span><span class="sxs-lookup"><span data-stu-id="f33d3-156">For naming rules for Data Factory artifacts, see [Data Factory naming rules](naming-rules.md).</span></span>
  
   ![Error message](./media/tutorial-copy-data-portal/name-not-available-error.png)
1. <span data-ttu-id="f33d3-158">Select the Azure **subscription** in which you want to create the data factory.</span><span class="sxs-lookup"><span data-stu-id="f33d3-158">Select the Azure **subscription** in which you want to create the data factory.</span></span> 
1. <span data-ttu-id="f33d3-159">For **Resource Group**, take one of the following steps:</span><span class="sxs-lookup"><span data-stu-id="f33d3-159">For **Resource Group**, take one of the following steps:</span></span>
     
    <span data-ttu-id="f33d3-160">a.</span><span class="sxs-lookup"><span data-stu-id="f33d3-160">a.</span></span> <span data-ttu-id="f33d3-161">Select **Use existing**, and select an existing resource group from the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="f33d3-161">Select **Use existing**, and select an existing resource group from the drop-down list.</span></span>

    <span data-ttu-id="f33d3-162">b.</span><span class="sxs-lookup"><span data-stu-id="f33d3-162">b.</span></span> <span data-ttu-id="f33d3-163">Select **Create new**, and enter the name of a resource group.</span><span class="sxs-lookup"><span data-stu-id="f33d3-163">Select **Create new**, and enter the name of a resource group.</span></span> 
         
    <span data-ttu-id="f33d3-164">To learn about resource groups, see [Use resource groups to manage your Azure resources](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f33d3-164">To learn about resource groups, see [Use resource groups to manage your Azure resources](../azure-resource-manager/resource-group-overview.md).</span></span> 
1. <span data-ttu-id="f33d3-165">Under **Version**, select **V2**.</span><span class="sxs-lookup"><span data-stu-id="f33d3-165">Under **Version**, select **V2**.</span></span>
1. <span data-ttu-id="f33d3-166">Under **Location**, select a location for the data factory.</span><span class="sxs-lookup"><span data-stu-id="f33d3-166">Under **Location**, select a location for the data factory.</span></span> <span data-ttu-id="f33d3-167">Only locations that are supported are displayed in the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="f33d3-167">Only locations that are supported are displayed in the drop-down list.</span></span> <span data-ttu-id="f33d3-168">The data stores (for example, Azure Storage and SQL Database) and computes (for example, Azure HDInsight) used by the data factory can be in other regions.</span><span class="sxs-lookup"><span data-stu-id="f33d3-168">The data stores (for example, Azure Storage and SQL Database) and computes (for example, Azure HDInsight) used by the data factory can be in other regions.</span></span>
1. <span data-ttu-id="f33d3-169">Select **Pin to dashboard**.</span><span class="sxs-lookup"><span data-stu-id="f33d3-169">Select **Pin to dashboard**.</span></span> 
1. <span data-ttu-id="f33d3-170">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="f33d3-170">Select **Create**.</span></span> 
1. <span data-ttu-id="f33d3-171">On the dashboard, you see the following tile with the status **Deploying Data Factory**:</span><span class="sxs-lookup"><span data-stu-id="f33d3-171">On the dashboard, you see the following tile with the status **Deploying Data Factory**:</span></span> 

    ![Deploying data factory tile](media/tutorial-copy-data-portal/deploying-data-factory.png)
1. <span data-ttu-id="f33d3-173">After the creation is finished, you see the **Data factory** page as shown in the image.</span><span class="sxs-lookup"><span data-stu-id="f33d3-173">After the creation is finished, you see the **Data factory** page as shown in the image.</span></span>
   
    ![Data factory home page](./media/tutorial-copy-data-portal/data-factory-home-page.png)
1. <span data-ttu-id="f33d3-175">Select **Author & Monitor** to launch the Data Factory UI in a separate tab.</span><span class="sxs-lookup"><span data-stu-id="f33d3-175">Select **Author & Monitor** to launch the Data Factory UI in a separate tab.</span></span>

## <a name="create-a-pipeline"></a><span data-ttu-id="f33d3-176">Create a pipeline</span><span class="sxs-lookup"><span data-stu-id="f33d3-176">Create a pipeline</span></span>
<span data-ttu-id="f33d3-177">In this step, you create a pipeline with a copy activity in the data factory.</span><span class="sxs-lookup"><span data-stu-id="f33d3-177">In this step, you create a pipeline with a copy activity in the data factory.</span></span> <span data-ttu-id="f33d3-178">The copy activity copies data from Blob storage to SQL Database.</span><span class="sxs-lookup"><span data-stu-id="f33d3-178">The copy activity copies data from Blob storage to SQL Database.</span></span> <span data-ttu-id="f33d3-179">In the [Quickstart tutorial](quickstart-create-data-factory-portal.md), you created a pipeline by following these steps:</span><span class="sxs-lookup"><span data-stu-id="f33d3-179">In the [Quickstart tutorial](quickstart-create-data-factory-portal.md), you created a pipeline by following these steps:</span></span>

1. <span data-ttu-id="f33d3-180">Create the linked service.</span><span class="sxs-lookup"><span data-stu-id="f33d3-180">Create the linked service.</span></span> 
1. <span data-ttu-id="f33d3-181">Create input and output datasets.</span><span class="sxs-lookup"><span data-stu-id="f33d3-181">Create input and output datasets.</span></span>
1. <span data-ttu-id="f33d3-182">Create a pipeline.</span><span class="sxs-lookup"><span data-stu-id="f33d3-182">Create a pipeline.</span></span>

<span data-ttu-id="f33d3-183">In this tutorial, you start with creating the pipeline.</span><span class="sxs-lookup"><span data-stu-id="f33d3-183">In this tutorial, you start with creating the pipeline.</span></span> <span data-ttu-id="f33d3-184">Then you create linked services and datasets when you need them to configure the pipeline.</span><span class="sxs-lookup"><span data-stu-id="f33d3-184">Then you create linked services and datasets when you need them to configure the pipeline.</span></span> 

1. <span data-ttu-id="f33d3-185">On the **Let's get started** page, select **Create pipeline**.</span><span class="sxs-lookup"><span data-stu-id="f33d3-185">On the **Let's get started** page, select **Create pipeline**.</span></span> 

   ![Create pipeline](./media/tutorial-copy-data-portal/create-pipeline-tile.png)
1. <span data-ttu-id="f33d3-187">In the **General** tab for the pipeline, enter **CopyPipeline** for **Name** of the pipeline.</span><span class="sxs-lookup"><span data-stu-id="f33d3-187">In the **General** tab for the pipeline, enter **CopyPipeline** for **Name** of the pipeline.</span></span>

1. <span data-ttu-id="f33d3-188">In the **Activities** tool box, expand the **Data Flow** category, and drag and drop the **Copy** activity from the tool box to the pipeline designer surface.</span><span class="sxs-lookup"><span data-stu-id="f33d3-188">In the **Activities** tool box, expand the **Data Flow** category, and drag and drop the **Copy** activity from the tool box to the pipeline designer surface.</span></span> <span data-ttu-id="f33d3-189">Specify **CopyFromBlobToSql** for **Name**.</span><span class="sxs-lookup"><span data-stu-id="f33d3-189">Specify **CopyFromBlobToSql** for **Name**.</span></span>

    ![Copy activity](./media/tutorial-copy-data-portal/drag-drop-copy-activity.png)

### <a name="configure-source"></a><span data-ttu-id="f33d3-191">Configure source</span><span class="sxs-lookup"><span data-stu-id="f33d3-191">Configure source</span></span>

1. <span data-ttu-id="f33d3-192">Go to the **Source** tab. Select **+ New** to create a source dataset.</span><span class="sxs-lookup"><span data-stu-id="f33d3-192">Go to the **Source** tab. Select **+ New** to create a source dataset.</span></span> 

1. <span data-ttu-id="f33d3-193">In the **New Dataset** window, select **Azure Blob Storage**, and then select **Finish**.</span><span class="sxs-lookup"><span data-stu-id="f33d3-193">In the **New Dataset** window, select **Azure Blob Storage**, and then select **Finish**.</span></span> <span data-ttu-id="f33d3-194">The source data is in Blob storage, so you select **Azure Blob Storage** for the source dataset.</span><span class="sxs-lookup"><span data-stu-id="f33d3-194">The source data is in Blob storage, so you select **Azure Blob Storage** for the source dataset.</span></span> 

    ![Storage selection](./media/tutorial-copy-data-portal/select-azure-blob-dataset.png)

1. <span data-ttu-id="f33d3-196">You see a new tab opened for blob dataset.</span><span class="sxs-lookup"><span data-stu-id="f33d3-196">You see a new tab opened for blob dataset.</span></span> <span data-ttu-id="f33d3-197">On the **General** tab at the bottom of the **Properties** window, enter **SourceBlobDataset** for **Name**.</span><span class="sxs-lookup"><span data-stu-id="f33d3-197">On the **General** tab at the bottom of the **Properties** window, enter **SourceBlobDataset** for **Name**.</span></span>

    ![Dataset name](./media/tutorial-copy-data-portal/dataset-name.png)

1. <span data-ttu-id="f33d3-199">Go to the **Connection** tab of the **Properties** window.</span><span class="sxs-lookup"><span data-stu-id="f33d3-199">Go to the **Connection** tab of the **Properties** window.</span></span> <span data-ttu-id="f33d3-200">Next to the **Linked service** text box, select **+ New**.</span><span class="sxs-lookup"><span data-stu-id="f33d3-200">Next to the **Linked service** text box, select **+ New**.</span></span> 

    ![New linked service button](./media/tutorial-copy-data-portal/source-dataset-new-linked-service-button.png)

1. <span data-ttu-id="f33d3-202">In the **New Linked Service** window, enter **AzureStorageLinkedService** as name, select your storage account from the **Storage account name** list, then select **Save** to deploy the linked service.</span><span class="sxs-lookup"><span data-stu-id="f33d3-202">In the **New Linked Service** window, enter **AzureStorageLinkedService** as name, select your storage account from the **Storage account name** list, then select **Save** to deploy the linked service.</span></span>

    ![New linked service](./media/tutorial-copy-data-portal/new-azure-storage-linked-service.png)

1. <span data-ttu-id="f33d3-204">After the linked service is created, you are back in the dataset settings.</span><span class="sxs-lookup"><span data-stu-id="f33d3-204">After the linked service is created, you are back in the dataset settings.</span></span> <span data-ttu-id="f33d3-205">Next to **File path**, select **Browse**.</span><span class="sxs-lookup"><span data-stu-id="f33d3-205">Next to **File path**, select **Browse**.</span></span>

    ![Browse button for file path](./media/tutorial-copy-data-portal/file-browse-button.png)

1. <span data-ttu-id="f33d3-207">Navigate to the **adftutorial/input** folder, select the **emp.txt** file, and then select **Finish**.</span><span class="sxs-lookup"><span data-stu-id="f33d3-207">Navigate to the **adftutorial/input** folder, select the **emp.txt** file, and then select **Finish**.</span></span> 

    ![Select input file](./media/tutorial-copy-data-portal/select-input-file.png)

1. <span data-ttu-id="f33d3-209">Confirm that **File format** is set to **Text format** and that **Column delimiter** is set to **Comma (`,`)**.</span><span class="sxs-lookup"><span data-stu-id="f33d3-209">Confirm that **File format** is set to **Text format** and that **Column delimiter** is set to **Comma (`,`)**.</span></span> <span data-ttu-id="f33d3-210">If the source file uses different row and column delimiters, you can select **Detect Text Format** for **File format**.</span><span class="sxs-lookup"><span data-stu-id="f33d3-210">If the source file uses different row and column delimiters, you can select **Detect Text Format** for **File format**.</span></span> <span data-ttu-id="f33d3-211">The Copy Data tool detects the file format and delimiters automatically for you.</span><span class="sxs-lookup"><span data-stu-id="f33d3-211">The Copy Data tool detects the file format and delimiters automatically for you.</span></span> <span data-ttu-id="f33d3-212">You can still override these values.</span><span class="sxs-lookup"><span data-stu-id="f33d3-212">You can still override these values.</span></span> <span data-ttu-id="f33d3-213">To preview data on this page, select **Preview data**.</span><span class="sxs-lookup"><span data-stu-id="f33d3-213">To preview data on this page, select **Preview data**.</span></span>

    ![Detect text format](./media/tutorial-copy-data-portal/detect-text-format.png)

1. <span data-ttu-id="f33d3-215">Go to the **Schema** tab of the **Properties** window, and select **Import Schema**.</span><span class="sxs-lookup"><span data-stu-id="f33d3-215">Go to the **Schema** tab of the **Properties** window, and select **Import Schema**.</span></span> <span data-ttu-id="f33d3-216">Notice that the application detected two columns in the source file.</span><span class="sxs-lookup"><span data-stu-id="f33d3-216">Notice that the application detected two columns in the source file.</span></span> <span data-ttu-id="f33d3-217">You import the schema here so that you can map columns from the source data store to the sink data store.</span><span class="sxs-lookup"><span data-stu-id="f33d3-217">You import the schema here so that you can map columns from the source data store to the sink data store.</span></span> <span data-ttu-id="f33d3-218">If you don't need to map columns, you can skip this step.</span><span class="sxs-lookup"><span data-stu-id="f33d3-218">If you don't need to map columns, you can skip this step.</span></span> <span data-ttu-id="f33d3-219">For this tutorial, import the schema.</span><span class="sxs-lookup"><span data-stu-id="f33d3-219">For this tutorial, import the schema.</span></span>

    ![Detect source schema](./media/tutorial-copy-data-portal/detect-source-schema.png)  

1. <span data-ttu-id="f33d3-221">Now, go back to the pipeline -> **Source** tab, confirm that **SourceBlobDataset** is selected.</span><span class="sxs-lookup"><span data-stu-id="f33d3-221">Now, go back to the pipeline -> **Source** tab, confirm that **SourceBlobDataset** is selected.</span></span> <span data-ttu-id="f33d3-222">To preview data on this page, select **Preview data**.</span><span class="sxs-lookup"><span data-stu-id="f33d3-222">To preview data on this page, select **Preview data**.</span></span> 
    
    ![Source dataset](./media/tutorial-copy-data-portal/source-dataset-selected.png)

### <a name="configure-sink"></a><span data-ttu-id="f33d3-224">Configure sink</span><span class="sxs-lookup"><span data-stu-id="f33d3-224">Configure sink</span></span>

1. <span data-ttu-id="f33d3-225">Go to the **Sink** tab, and select **+ New** to create a sink dataset.</span><span class="sxs-lookup"><span data-stu-id="f33d3-225">Go to the **Sink** tab, and select **+ New** to create a sink dataset.</span></span> 

    ![Sink dataset](./media/tutorial-copy-data-portal/new-sink-dataset-button.png)
1. <span data-ttu-id="f33d3-227">In the **New Dataset** window, input "SQL" in the searchbox to filter the connectors, then select **Azure SQL Database**, and then select **Finish**.</span><span class="sxs-lookup"><span data-stu-id="f33d3-227">In the **New Dataset** window, input "SQL" in the searchbox to filter the connectors, then select **Azure SQL Database**, and then select **Finish**.</span></span> <span data-ttu-id="f33d3-228">In this tutorial, you copy data to a SQL database.</span><span class="sxs-lookup"><span data-stu-id="f33d3-228">In this tutorial, you copy data to a SQL database.</span></span> 

    ![SQL database selection](./media/tutorial-copy-data-portal/select-azure-sql-dataset.png)
1. <span data-ttu-id="f33d3-230">On the **General** tab of the **Properties** window, in **Name**, enter **OutputSqlDataset**.</span><span class="sxs-lookup"><span data-stu-id="f33d3-230">On the **General** tab of the **Properties** window, in **Name**, enter **OutputSqlDataset**.</span></span> 
    
    ![Output dataset name](./media/tutorial-copy-data-portal/output-dataset-name.png)
1. <span data-ttu-id="f33d3-232">Go to the **Connection** tab, and next to **Linked service**, select **+ New**.</span><span class="sxs-lookup"><span data-stu-id="f33d3-232">Go to the **Connection** tab, and next to **Linked service**, select **+ New**.</span></span> <span data-ttu-id="f33d3-233">A dataset must be associated with a linked service.</span><span class="sxs-lookup"><span data-stu-id="f33d3-233">A dataset must be associated with a linked service.</span></span> <span data-ttu-id="f33d3-234">The linked service has the connection string that Data Factory uses to connect to the SQL database at runtime.</span><span class="sxs-lookup"><span data-stu-id="f33d3-234">The linked service has the connection string that Data Factory uses to connect to the SQL database at runtime.</span></span> <span data-ttu-id="f33d3-235">The dataset specifies the container, folder, and the file (optional) to which the data is copied.</span><span class="sxs-lookup"><span data-stu-id="f33d3-235">The dataset specifies the container, folder, and the file (optional) to which the data is copied.</span></span> 
    
    ![Linked service](./media/tutorial-copy-data-portal/new-azure-sql-database-linked-service-button.png)       
1. <span data-ttu-id="f33d3-237">In the **New Linked Service** window, take the following steps:</span><span class="sxs-lookup"><span data-stu-id="f33d3-237">In the **New Linked Service** window, take the following steps:</span></span> 

    <span data-ttu-id="f33d3-238">a.</span><span class="sxs-lookup"><span data-stu-id="f33d3-238">a.</span></span> <span data-ttu-id="f33d3-239">Under **Name**, enter **AzureSqlDatabaseLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="f33d3-239">Under **Name**, enter **AzureSqlDatabaseLinkedService**.</span></span>

    <span data-ttu-id="f33d3-240">b.</span><span class="sxs-lookup"><span data-stu-id="f33d3-240">b.</span></span> <span data-ttu-id="f33d3-241">Under **Server name**, select your SQL Server instance.</span><span class="sxs-lookup"><span data-stu-id="f33d3-241">Under **Server name**, select your SQL Server instance.</span></span>

    <span data-ttu-id="f33d3-242">c.</span><span class="sxs-lookup"><span data-stu-id="f33d3-242">c.</span></span> <span data-ttu-id="f33d3-243">Under **Database name**, select your SQL database.</span><span class="sxs-lookup"><span data-stu-id="f33d3-243">Under **Database name**, select your SQL database.</span></span>

    <span data-ttu-id="f33d3-244">d.</span><span class="sxs-lookup"><span data-stu-id="f33d3-244">d.</span></span> <span data-ttu-id="f33d3-245">Under **User name**, enter the name of the user.</span><span class="sxs-lookup"><span data-stu-id="f33d3-245">Under **User name**, enter the name of the user.</span></span>

    <span data-ttu-id="f33d3-246">e.</span><span class="sxs-lookup"><span data-stu-id="f33d3-246">e.</span></span> <span data-ttu-id="f33d3-247">Under **Password**, enter the password for the user.</span><span class="sxs-lookup"><span data-stu-id="f33d3-247">Under **Password**, enter the password for the user.</span></span>

    <span data-ttu-id="f33d3-248">f.</span><span class="sxs-lookup"><span data-stu-id="f33d3-248">f.</span></span> <span data-ttu-id="f33d3-249">Select **Test connection** to test the connection.</span><span class="sxs-lookup"><span data-stu-id="f33d3-249">Select **Test connection** to test the connection.</span></span>

    <span data-ttu-id="f33d3-250">g.</span><span class="sxs-lookup"><span data-stu-id="f33d3-250">g.</span></span> <span data-ttu-id="f33d3-251">Select **Save** to save the linked service.</span><span class="sxs-lookup"><span data-stu-id="f33d3-251">Select **Save** to save the linked service.</span></span> 
    
    ![Save new linked service](./media/tutorial-copy-data-portal/new-azure-sql-linked-service-window.png)

1. <span data-ttu-id="f33d3-253">In **Table**, select **[dbo].[emp]**.</span><span class="sxs-lookup"><span data-stu-id="f33d3-253">In **Table**, select **[dbo].[emp]**.</span></span> 

    ![Table](./media/tutorial-copy-data-portal/select-emp-table.png)
1. <span data-ttu-id="f33d3-255">Go to the **Schema** tab, and select **Import Schema**.</span><span class="sxs-lookup"><span data-stu-id="f33d3-255">Go to the **Schema** tab, and select **Import Schema**.</span></span> 

    ![Select import schema](./media/tutorial-copy-data-portal/import-destination-schema.png)
1. <span data-ttu-id="f33d3-257">Select the **ID** column, and then select **Delete**.</span><span class="sxs-lookup"><span data-stu-id="f33d3-257">Select the **ID** column, and then select **Delete**.</span></span> <span data-ttu-id="f33d3-258">The **ID** column is an identity column in the SQL database, so the copy activity doesn't need to insert data into this column.</span><span class="sxs-lookup"><span data-stu-id="f33d3-258">The **ID** column is an identity column in the SQL database, so the copy activity doesn't need to insert data into this column.</span></span>

    ![Delete ID column](./media/tutorial-copy-data-portal/delete-id-column.png)
1. <span data-ttu-id="f33d3-260">Go to the tab with the pipeline, and in **Sink Dataset**, confirm that **OutputSqlDataset** is selected.</span><span class="sxs-lookup"><span data-stu-id="f33d3-260">Go to the tab with the pipeline, and in **Sink Dataset**, confirm that **OutputSqlDataset** is selected.</span></span>

    ![Pipeline tab](./media/tutorial-copy-data-portal/pipeline-tab-2.png)        

### <a name="confugure-mapping"></a><span data-ttu-id="f33d3-262">Confugure mapping</span><span class="sxs-lookup"><span data-stu-id="f33d3-262">Confugure mapping</span></span>

<span data-ttu-id="f33d3-263">Go to the **Mapping** tab at the bottom of the **Properties** window, and select **Import Schemas**.</span><span class="sxs-lookup"><span data-stu-id="f33d3-263">Go to the **Mapping** tab at the bottom of the **Properties** window, and select **Import Schemas**.</span></span> <span data-ttu-id="f33d3-264">Notice that the first and second columns in the source file are mapped to **FirstName** and **LastName** in the SQL database.</span><span class="sxs-lookup"><span data-stu-id="f33d3-264">Notice that the first and second columns in the source file are mapped to **FirstName** and **LastName** in the SQL database.</span></span>

![Map schemas](./media/tutorial-copy-data-portal/map-schemas.png)

## <a name="validate-the-pipeline"></a><span data-ttu-id="f33d3-266">Validate the pipeline</span><span class="sxs-lookup"><span data-stu-id="f33d3-266">Validate the pipeline</span></span>
<span data-ttu-id="f33d3-267">To validate the pipeline, select **Validate** from the tool bar.</span><span class="sxs-lookup"><span data-stu-id="f33d3-267">To validate the pipeline, select **Validate** from the tool bar.</span></span>
 
<span data-ttu-id="f33d3-268">You can see the JSON code associated with the pipeline by clicking **Code** on the upper-right.</span><span class="sxs-lookup"><span data-stu-id="f33d3-268">You can see the JSON code associated with the pipeline by clicking **Code** on the upper-right.</span></span>

## <a name="debug-and-publish-the-pipeline"></a><span data-ttu-id="f33d3-269">Debug and publish the pipeline</span><span class="sxs-lookup"><span data-stu-id="f33d3-269">Debug and publish the pipeline</span></span>
<span data-ttu-id="f33d3-270">You can debug a pipeline before you publish artifacts (linked services, datasets, and pipeline) to Data Factory or your own Azure Repos Git repository.</span><span class="sxs-lookup"><span data-stu-id="f33d3-270">You can debug a pipeline before you publish artifacts (linked services, datasets, and pipeline) to Data Factory or your own Azure Repos Git repository.</span></span> 

1. <span data-ttu-id="f33d3-271">To debug the pipeline, select **Debug** on the toolbar.</span><span class="sxs-lookup"><span data-stu-id="f33d3-271">To debug the pipeline, select **Debug** on the toolbar.</span></span> <span data-ttu-id="f33d3-272">You see the status of the pipeline run in the **Output** tab at the bottom of the window.</span><span class="sxs-lookup"><span data-stu-id="f33d3-272">You see the status of the pipeline run in the **Output** tab at the bottom of the window.</span></span> 

1. <span data-ttu-id="f33d3-273">Once the pipeline can run successfually, in the top toolbar, select **Publish All**.</span><span class="sxs-lookup"><span data-stu-id="f33d3-273">Once the pipeline can run successfually, in the top toolbar, select **Publish All**.</span></span> <span data-ttu-id="f33d3-274">This action publishes entities (datasets, and pipelines) you created to Data Factory.</span><span class="sxs-lookup"><span data-stu-id="f33d3-274">This action publishes entities (datasets, and pipelines) you created to Data Factory.</span></span>

    ![Publish](./media/tutorial-copy-data-portal/publish-button.png)

1. <span data-ttu-id="f33d3-276">Wait until you see the **Successfully published** message.</span><span class="sxs-lookup"><span data-stu-id="f33d3-276">Wait until you see the **Successfully published** message.</span></span> <span data-ttu-id="f33d3-277">To see notification messages, click the **Show Notifications**  on the top-right (bell button).</span><span class="sxs-lookup"><span data-stu-id="f33d3-277">To see notification messages, click the **Show Notifications**  on the top-right (bell button).</span></span> 

## <a name="trigger-the-pipeline-manually"></a><span data-ttu-id="f33d3-278">Trigger the pipeline manually</span><span class="sxs-lookup"><span data-stu-id="f33d3-278">Trigger the pipeline manually</span></span>
<span data-ttu-id="f33d3-279">In this step, you manually trigger the pipeline you published in the previous step.</span><span class="sxs-lookup"><span data-stu-id="f33d3-279">In this step, you manually trigger the pipeline you published in the previous step.</span></span> 

1. <span data-ttu-id="f33d3-280">Select **Trigger** on the toolbar, and then select **Trigger Now**.</span><span class="sxs-lookup"><span data-stu-id="f33d3-280">Select **Trigger** on the toolbar, and then select **Trigger Now**.</span></span> <span data-ttu-id="f33d3-281">On the **Pipeline Run** page, select **Finish**.</span><span class="sxs-lookup"><span data-stu-id="f33d3-281">On the **Pipeline Run** page, select **Finish**.</span></span>  

1. <span data-ttu-id="f33d3-282">Go to the **Monitor** tab on the left.</span><span class="sxs-lookup"><span data-stu-id="f33d3-282">Go to the **Monitor** tab on the left.</span></span> <span data-ttu-id="f33d3-283">You see a pipeline run that is triggered by a manual trigger.</span><span class="sxs-lookup"><span data-stu-id="f33d3-283">You see a pipeline run that is triggered by a manual trigger.</span></span> <span data-ttu-id="f33d3-284">You can use links in the **Actions** column to view activity details and to rerun the pipeline.</span><span class="sxs-lookup"><span data-stu-id="f33d3-284">You can use links in the **Actions** column to view activity details and to rerun the pipeline.</span></span>

    ![Monitor pipeline runs](./media/tutorial-copy-data-portal/monitor-pipeline.png)
1. <span data-ttu-id="f33d3-286">To see activity runs associated with the pipeline run, select the **View Activity Runs** link in the **Actions** column.</span><span class="sxs-lookup"><span data-stu-id="f33d3-286">To see activity runs associated with the pipeline run, select the **View Activity Runs** link in the **Actions** column.</span></span> <span data-ttu-id="f33d3-287">In this example, there is only one activity, so you see only one entry in the list.</span><span class="sxs-lookup"><span data-stu-id="f33d3-287">In this example, there is only one activity, so you see only one entry in the list.</span></span> <span data-ttu-id="f33d3-288">For details about the copy operation, select the **Details** link (eyeglasses icon) in the **Actions** column.</span><span class="sxs-lookup"><span data-stu-id="f33d3-288">For details about the copy operation, select the **Details** link (eyeglasses icon) in the **Actions** column.</span></span> <span data-ttu-id="f33d3-289">Select **Pipelines** at the top to go back to the **Pipeline Runs** view.</span><span class="sxs-lookup"><span data-stu-id="f33d3-289">Select **Pipelines** at the top to go back to the **Pipeline Runs** view.</span></span> <span data-ttu-id="f33d3-290">To refresh the view, select **Refresh**.</span><span class="sxs-lookup"><span data-stu-id="f33d3-290">To refresh the view, select **Refresh**.</span></span>

    ![Monitor activity runs](./media/tutorial-copy-data-portal/view-activity-runs.png)
1. <span data-ttu-id="f33d3-292">Verify that two more rows are added to the **emp** table in the SQL database.</span><span class="sxs-lookup"><span data-stu-id="f33d3-292">Verify that two more rows are added to the **emp** table in the SQL database.</span></span> 

## <a name="trigger-the-pipeline-on-a-schedule"></a><span data-ttu-id="f33d3-293">Trigger the pipeline on a schedule</span><span class="sxs-lookup"><span data-stu-id="f33d3-293">Trigger the pipeline on a schedule</span></span>
<span data-ttu-id="f33d3-294">In this schedule, you create a schedule trigger for the pipeline.</span><span class="sxs-lookup"><span data-stu-id="f33d3-294">In this schedule, you create a schedule trigger for the pipeline.</span></span> <span data-ttu-id="f33d3-295">The trigger runs the pipeline on the specified schedule, such as hourly or daily.</span><span class="sxs-lookup"><span data-stu-id="f33d3-295">The trigger runs the pipeline on the specified schedule, such as hourly or daily.</span></span> <span data-ttu-id="f33d3-296">In this example, you set the trigger to run every minute until the specified end datetime.</span><span class="sxs-lookup"><span data-stu-id="f33d3-296">In this example, you set the trigger to run every minute until the specified end datetime.</span></span> 

1. <span data-ttu-id="f33d3-297">Go to the **Author** tab on the left above the monitor tab.</span><span class="sxs-lookup"><span data-stu-id="f33d3-297">Go to the **Author** tab on the left above the monitor tab.</span></span> 

1. <span data-ttu-id="f33d3-298">Go to your pipeline, click **Trigger** on the tool bar, and select **New/Edit**.</span><span class="sxs-lookup"><span data-stu-id="f33d3-298">Go to your pipeline, click **Trigger** on the tool bar, and select **New/Edit**.</span></span> 

1. <span data-ttu-id="f33d3-299">In the **Add Triggers** window, select **Choose trigger**, and then select **+ New**.</span><span class="sxs-lookup"><span data-stu-id="f33d3-299">In the **Add Triggers** window, select **Choose trigger**, and then select **+ New**.</span></span> 

    ![New button](./media/tutorial-copy-data-portal/add-trigger-new-button.png)
1. <span data-ttu-id="f33d3-301">In the **New Trigger** window, take the following steps:</span><span class="sxs-lookup"><span data-stu-id="f33d3-301">In the **New Trigger** window, take the following steps:</span></span> 

    <span data-ttu-id="f33d3-302">a.</span><span class="sxs-lookup"><span data-stu-id="f33d3-302">a.</span></span> <span data-ttu-id="f33d3-303">Under **Name**, enter **RunEveryMinute**.</span><span class="sxs-lookup"><span data-stu-id="f33d3-303">Under **Name**, enter **RunEveryMinute**.</span></span>

    <span data-ttu-id="f33d3-304">b.</span><span class="sxs-lookup"><span data-stu-id="f33d3-304">b.</span></span> <span data-ttu-id="f33d3-305">Under **End**, select **On Date**.</span><span class="sxs-lookup"><span data-stu-id="f33d3-305">Under **End**, select **On Date**.</span></span>

    <span data-ttu-id="f33d3-306">c.</span><span class="sxs-lookup"><span data-stu-id="f33d3-306">c.</span></span> <span data-ttu-id="f33d3-307">Under **End On**, select the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="f33d3-307">Under **End On**, select the drop-down list.</span></span>

    <span data-ttu-id="f33d3-308">d.</span><span class="sxs-lookup"><span data-stu-id="f33d3-308">d.</span></span> <span data-ttu-id="f33d3-309">Select the **current day** option.</span><span class="sxs-lookup"><span data-stu-id="f33d3-309">Select the **current day** option.</span></span> <span data-ttu-id="f33d3-310">By default, the end day is set to the next day.</span><span class="sxs-lookup"><span data-stu-id="f33d3-310">By default, the end day is set to the next day.</span></span>

    <span data-ttu-id="f33d3-311">e.</span><span class="sxs-lookup"><span data-stu-id="f33d3-311">e.</span></span> <span data-ttu-id="f33d3-312">Update the **minutes** part to be a few minutes past the current datetime.</span><span class="sxs-lookup"><span data-stu-id="f33d3-312">Update the **minutes** part to be a few minutes past the current datetime.</span></span> <span data-ttu-id="f33d3-313">The trigger is activated only after you publish the changes.</span><span class="sxs-lookup"><span data-stu-id="f33d3-313">The trigger is activated only after you publish the changes.</span></span> <span data-ttu-id="f33d3-314">If you set it to only a couple of minutes apart and you don't publish it by then, you don't see a trigger run.</span><span class="sxs-lookup"><span data-stu-id="f33d3-314">If you set it to only a couple of minutes apart and you don't publish it by then, you don't see a trigger run.</span></span>

    <span data-ttu-id="f33d3-315">f.</span><span class="sxs-lookup"><span data-stu-id="f33d3-315">f.</span></span> <span data-ttu-id="f33d3-316">Select **Apply**.</span><span class="sxs-lookup"><span data-stu-id="f33d3-316">Select **Apply**.</span></span> 

    ![Trigger properties](./media/tutorial-copy-data-portal/set-trigger-properties.png)

    <span data-ttu-id="f33d3-318">g.</span><span class="sxs-lookup"><span data-stu-id="f33d3-318">g.</span></span> <span data-ttu-id="f33d3-319">Select the **Activated** option.</span><span class="sxs-lookup"><span data-stu-id="f33d3-319">Select the **Activated** option.</span></span> <span data-ttu-id="f33d3-320">You can deactivate it and activate it later by using this check box.</span><span class="sxs-lookup"><span data-stu-id="f33d3-320">You can deactivate it and activate it later by using this check box.</span></span>

    <span data-ttu-id="f33d3-321">h.</span><span class="sxs-lookup"><span data-stu-id="f33d3-321">h.</span></span> <span data-ttu-id="f33d3-322">Select **Next**.</span><span class="sxs-lookup"><span data-stu-id="f33d3-322">Select **Next**.</span></span>

    ![Activated button](./media/tutorial-copy-data-portal/trigger-activiated-next.png)

    > [!IMPORTANT]
    > <span data-ttu-id="f33d3-324">A cost is associated with each pipeline run, so set the end date appropriately.</span><span class="sxs-lookup"><span data-stu-id="f33d3-324">A cost is associated with each pipeline run, so set the end date appropriately.</span></span> 
1. <span data-ttu-id="f33d3-325">On the **Trigger Run Parameters** page, review the warning, and then select **Finish**.</span><span class="sxs-lookup"><span data-stu-id="f33d3-325">On the **Trigger Run Parameters** page, review the warning, and then select **Finish**.</span></span> <span data-ttu-id="f33d3-326">The pipeline in this example doesn't take any parameters.</span><span class="sxs-lookup"><span data-stu-id="f33d3-326">The pipeline in this example doesn't take any parameters.</span></span> 

    ![Trigger run parameters](./media/tutorial-copy-data-portal/trigger-pipeline-parameters.png)

1. <span data-ttu-id="f33d3-328">Click **Publish All** to publish the change.</span><span class="sxs-lookup"><span data-stu-id="f33d3-328">Click **Publish All** to publish the change.</span></span> 

1. <span data-ttu-id="f33d3-329">Go to the **Monitor** tab on the left to see the triggered pipeline runs.</span><span class="sxs-lookup"><span data-stu-id="f33d3-329">Go to the **Monitor** tab on the left to see the triggered pipeline runs.</span></span> 

    ![Triggered pipeline runs](./media/tutorial-copy-data-portal/triggered-pipeline-runs.png)    
1. <span data-ttu-id="f33d3-331">To switch from the **Pipeline Runs** view to the **Trigger Runs** view, select **Pipeline Runs** and then select **Trigger Runs**.</span><span class="sxs-lookup"><span data-stu-id="f33d3-331">To switch from the **Pipeline Runs** view to the **Trigger Runs** view, select **Pipeline Runs** and then select **Trigger Runs**.</span></span>
    
    ![Trigger runs](./media/tutorial-copy-data-portal/trigger-runs-menu.png)
1. <span data-ttu-id="f33d3-333">You see the trigger runs in a list.</span><span class="sxs-lookup"><span data-stu-id="f33d3-333">You see the trigger runs in a list.</span></span> 

    ![Trigger runs list](./media/tutorial-copy-data-portal/trigger-runs-list.png)
1. <span data-ttu-id="f33d3-335">Verify that two rows per minute (for each pipeline run) are inserted into the **emp** table until the specified end time.</span><span class="sxs-lookup"><span data-stu-id="f33d3-335">Verify that two rows per minute (for each pipeline run) are inserted into the **emp** table until the specified end time.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="f33d3-336">Next steps</span><span class="sxs-lookup"><span data-stu-id="f33d3-336">Next steps</span></span>
<span data-ttu-id="f33d3-337">The pipeline in this sample copies data from one location to another location in Blob storage.</span><span class="sxs-lookup"><span data-stu-id="f33d3-337">The pipeline in this sample copies data from one location to another location in Blob storage.</span></span> <span data-ttu-id="f33d3-338">You learned how to:</span><span class="sxs-lookup"><span data-stu-id="f33d3-338">You learned how to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="f33d3-339">Create a data factory.</span><span class="sxs-lookup"><span data-stu-id="f33d3-339">Create a data factory.</span></span>
> * <span data-ttu-id="f33d3-340">Create a pipeline with a copy activity.</span><span class="sxs-lookup"><span data-stu-id="f33d3-340">Create a pipeline with a copy activity.</span></span>
> * <span data-ttu-id="f33d3-341">Test run the pipeline.</span><span class="sxs-lookup"><span data-stu-id="f33d3-341">Test run the pipeline.</span></span>
> * <span data-ttu-id="f33d3-342">Trigger the pipeline manually.</span><span class="sxs-lookup"><span data-stu-id="f33d3-342">Trigger the pipeline manually.</span></span>
> * <span data-ttu-id="f33d3-343">Trigger the pipeline on a schedule.</span><span class="sxs-lookup"><span data-stu-id="f33d3-343">Trigger the pipeline on a schedule.</span></span>
> * <span data-ttu-id="f33d3-344">Monitor the pipeline and activity runs.</span><span class="sxs-lookup"><span data-stu-id="f33d3-344">Monitor the pipeline and activity runs.</span></span>


<span data-ttu-id="f33d3-345">Advance to the following tutorial to learn how to copy data from on-premises to the cloud:</span><span class="sxs-lookup"><span data-stu-id="f33d3-345">Advance to the following tutorial to learn how to copy data from on-premises to the cloud:</span></span> 

> [!div class="nextstepaction"]
>[<span data-ttu-id="f33d3-346">Copy data from on-premises to the cloud</span><span class="sxs-lookup"><span data-stu-id="f33d3-346">Copy data from on-premises to the cloud</span></span>](tutorial-hybrid-copy-portal.md)
