---
title: 'Tutorial: Create a pipeline with Copy Activity using Azure portal | Microsoft Docs'
description: In this tutorial, you create an Azure Data Factory pipeline with a Copy Activity by using the Data Factory Editor in the Azure portal.
services: data-factory
documentationcenter: ''
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: d9317652-0170-4fd3-b9b2-37711272162b
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/11/2017
ms.author: spelluru
ms.openlocfilehash: e4ce9363d862f71534899c429365de20c62f8b58
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564097"
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-azure-portal"></a><span data-ttu-id="e41cd-103">Tutorial: Create a pipeline with Copy Activity using Azure portal</span><span class="sxs-lookup"><span data-stu-id="e41cd-103">Tutorial: Create a pipeline with Copy Activity using Azure portal</span></span>
> [!div class="op_single_selector"]
> * [Overview and prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [Copy Wizard](data-factory-copy-data-wizard-tutorial.md)
> * [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)
> * [Azure Resource Manager template](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [REST API](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [.NET API](data-factory-copy-activity-tutorial-using-dotnet-api.md)
> 
> 

<span data-ttu-id="e41cd-112">This tutorial shows you how to create and monitor an Azure data factory using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="e41cd-112">This tutorial shows you how to create and monitor an Azure data factory using the Azure portal.</span></span> <span data-ttu-id="e41cd-113">The pipeline in the data factory uses a Copy Activity to copy data from Azure Blob Storage to Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="e41cd-113">The pipeline in the data factory uses a Copy Activity to copy data from Azure Blob Storage to Azure SQL Database.</span></span>

> [!NOTE]
> The data pipeline in this tutorial copies data from a source data store to a destination data store. It does not transform input data to produce output data. For a tutorial on how to transform data using Azure Data Factory, see [Tutorial: Build a pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).
> 
> You can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity. See [Scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md) for detailed information. 

<span data-ttu-id="e41cd-119">Here are the steps you perform as part of this tutorial:</span><span class="sxs-lookup"><span data-stu-id="e41cd-119">Here are the steps you perform as part of this tutorial:</span></span>

| <span data-ttu-id="e41cd-120">Step</span><span class="sxs-lookup"><span data-stu-id="e41cd-120">Step</span></span> | <span data-ttu-id="e41cd-121">Description</span><span class="sxs-lookup"><span data-stu-id="e41cd-121">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="e41cd-122">Create an Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="e41cd-122">Create an Azure Data Factory</span></span>](#create-data-factory) |<span data-ttu-id="e41cd-123">In this step, you create an Azure data factory named **ADFTutorialDataFactory**.</span><span class="sxs-lookup"><span data-stu-id="e41cd-123">In this step, you create an Azure data factory named **ADFTutorialDataFactory**.</span></span> |
| [<span data-ttu-id="e41cd-124">Create linked services</span><span class="sxs-lookup"><span data-stu-id="e41cd-124">Create linked services</span></span>](#create-linked-services) |<span data-ttu-id="e41cd-125">In this step, you create two linked services: **AzureStorageLinkedService** and **AzureSqlLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="e41cd-125">In this step, you create two linked services: **AzureStorageLinkedService** and **AzureSqlLinkedService**.</span></span> <br/><br/><span data-ttu-id="e41cd-126">The AzureStorageLinkedService links the Azure storage and AzureSqlLinkedService links the Azure SQL database to the ADFTutorialDataFactory.</span><span class="sxs-lookup"><span data-stu-id="e41cd-126">The AzureStorageLinkedService links the Azure storage and AzureSqlLinkedService links the Azure SQL database to the ADFTutorialDataFactory.</span></span> <span data-ttu-id="e41cd-127">The input data for the pipeline resides in a blob container in the Azure blob storage and output data be stored in a table in the Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="e41cd-127">The input data for the pipeline resides in a blob container in the Azure blob storage and output data be stored in a table in the Azure SQL database.</span></span> <span data-ttu-id="e41cd-128">Therefore, you add these two data stores as linked services to the data factory.</span><span class="sxs-lookup"><span data-stu-id="e41cd-128">Therefore, you add these two data stores as linked services to the data factory.</span></span> |
| [<span data-ttu-id="e41cd-129">Create input and output datasets</span><span class="sxs-lookup"><span data-stu-id="e41cd-129">Create input and output datasets</span></span>](#create-datasets) |<span data-ttu-id="e41cd-130">In the previous step, you created linked services that refer to data stores that contain input/output data.</span><span class="sxs-lookup"><span data-stu-id="e41cd-130">In the previous step, you created linked services that refer to data stores that contain input/output data.</span></span> <span data-ttu-id="e41cd-131">In this step, you define two datasets -- **InputDataset** and **OutputDataset** -- that represent the input/output data that is stored in the data stores.</span><span class="sxs-lookup"><span data-stu-id="e41cd-131">In this step, you define two datasets -- **InputDataset** and **OutputDataset** -- that represent the input/output data that is stored in the data stores.</span></span> <br/><br/><span data-ttu-id="e41cd-132">For the InputDataset, you specify the blob container that contains a blob with the source data and for the OutputDataset, you specify the SQL table that stores the output data.</span><span class="sxs-lookup"><span data-stu-id="e41cd-132">For the InputDataset, you specify the blob container that contains a blob with the source data and for the OutputDataset, you specify the SQL table that stores the output data.</span></span> <span data-ttu-id="e41cd-133">You also specify other properties such as structure, availability, and policy.</span><span class="sxs-lookup"><span data-stu-id="e41cd-133">You also specify other properties such as structure, availability, and policy.</span></span> |
| [<span data-ttu-id="e41cd-134">Create a pipeline</span><span class="sxs-lookup"><span data-stu-id="e41cd-134">Create a pipeline</span></span>](#create-pipeline) |<span data-ttu-id="e41cd-135">In this step, you create a pipeline named **ADFTutorialPipeline** in the ADFTutorialDataFactory.</span><span class="sxs-lookup"><span data-stu-id="e41cd-135">In this step, you create a pipeline named **ADFTutorialPipeline** in the ADFTutorialDataFactory.</span></span> <br/><br/><span data-ttu-id="e41cd-136">You add a **Copy Activity** to the pipeline that copies input data from the Azure blob to the output Azure SQL table.</span><span class="sxs-lookup"><span data-stu-id="e41cd-136">You add a **Copy Activity** to the pipeline that copies input data from the Azure blob to the output Azure SQL table.</span></span> <span data-ttu-id="e41cd-137">The Copy Activity performs the data movement in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="e41cd-137">The Copy Activity performs the data movement in Azure Data Factory.</span></span> <span data-ttu-id="e41cd-138">It is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span><span class="sxs-lookup"><span data-stu-id="e41cd-138">It is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="e41cd-139">See [Data Movement Activities](data-factory-data-movement-activities.md) article for details about the Copy Activity.</span><span class="sxs-lookup"><span data-stu-id="e41cd-139">See [Data Movement Activities](data-factory-data-movement-activities.md) article for details about the Copy Activity.</span></span> |
| [<span data-ttu-id="e41cd-140">Monitor pipeline</span><span class="sxs-lookup"><span data-stu-id="e41cd-140">Monitor pipeline</span></span>](#monitor-pipeline) |<span data-ttu-id="e41cd-141">In this step, you monitor slices of input and output tables by using Azure portal.</span><span class="sxs-lookup"><span data-stu-id="e41cd-141">In this step, you monitor slices of input and output tables by using Azure portal.</span></span> |

## <a name="prerequisites"></a><span data-ttu-id="e41cd-142">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e41cd-142">Prerequisites</span></span>
<span data-ttu-id="e41cd-143">Complete prerequisites listed in the [Tutorial Overview](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) article before performing this tutorial.</span><span class="sxs-lookup"><span data-stu-id="e41cd-143">Complete prerequisites listed in the [Tutorial Overview](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) article before performing this tutorial.</span></span>

## <a name="create-data-factory"></a><span data-ttu-id="e41cd-144">Create data factory</span><span class="sxs-lookup"><span data-stu-id="e41cd-144">Create data factory</span></span>
<span data-ttu-id="e41cd-145">In this step, you use the Azure portal to create an Azure data factory named **ADFTutorialDataFactory**.</span><span class="sxs-lookup"><span data-stu-id="e41cd-145">In this step, you use the Azure portal to create an Azure data factory named **ADFTutorialDataFactory**.</span></span>

1. <span data-ttu-id="e41cd-146">After logging in to the [Azure portal](https://portal.azure.com/), click **New**, select **Intelligence + Analytics**, and click **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="e41cd-146">After logging in to the [Azure portal](https://portal.azure.com/), click **New**, select **Intelligence + Analytics**, and click **Data Factory**.</span></span> 
   
   ![New->DataFactory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-activity-tutorial-using-azure-portal/NewDataFactoryMenu.png)    
2. <span data-ttu-id="e41cd-148">In the **New data factory** blade:</span><span class="sxs-lookup"><span data-stu-id="e41cd-148">In the **New data factory** blade:</span></span>
   
   1. <span data-ttu-id="e41cd-149">Enter **ADFTutorialDataFactory** for the **name**.</span><span class="sxs-lookup"><span data-stu-id="e41cd-149">Enter **ADFTutorialDataFactory** for the **name**.</span></span> 
      
         ![New data factory blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-new-data-factory.png)
      
       <span data-ttu-id="e41cd-151">The name of the Azure data factory must be **globally unique**.</span><span class="sxs-lookup"><span data-stu-id="e41cd-151">The name of the Azure data factory must be **globally unique**.</span></span> <span data-ttu-id="e41cd-152">If you receive the following error, change the name of the data factory (for example, yournameADFTutorialDataFactory) and try creating again.</span><span class="sxs-lookup"><span data-stu-id="e41cd-152">If you receive the following error, change the name of the data factory (for example, yournameADFTutorialDataFactory) and try creating again.</span></span> <span data-ttu-id="e41cd-153">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span><span class="sxs-lookup"><span data-stu-id="e41cd-153">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
      
           Data factory name “ADFTutorialDataFactory” is not available  
      
       ![Data Factory name not available](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-data-factory-not-available.png)
   2. <span data-ttu-id="e41cd-155">Select your Azure **subscription**.</span><span class="sxs-lookup"><span data-stu-id="e41cd-155">Select your Azure **subscription**.</span></span>
   3. <span data-ttu-id="e41cd-156">For the Resource Group, do one of the following steps:</span><span class="sxs-lookup"><span data-stu-id="e41cd-156">For the Resource Group, do one of the following steps:</span></span>
      
      - <span data-ttu-id="e41cd-157">Select **Use existing**, and select an existing resource group from the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="e41cd-157">Select **Use existing**, and select an existing resource group from the drop-down list.</span></span> 
      - <span data-ttu-id="e41cd-158">Select **Create new**, and enter the name of a resource group.</span><span class="sxs-lookup"><span data-stu-id="e41cd-158">Select **Create new**, and enter the name of a resource group.</span></span>   
         
          <span data-ttu-id="e41cd-159">Some of the steps in this tutorial assume that you use the name: **ADFTutorialResourceGroup** for the resource group.</span><span class="sxs-lookup"><span data-stu-id="e41cd-159">Some of the steps in this tutorial assume that you use the name: **ADFTutorialResourceGroup** for the resource group.</span></span> <span data-ttu-id="e41cd-160">To learn about resource groups, see [Using resource groups to manage your Azure resources](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e41cd-160">To learn about resource groups, see [Using resource groups to manage your Azure resources](../azure-resource-manager/resource-group-overview.md).</span></span>  
   4. <span data-ttu-id="e41cd-161">Select the **location** for the data factory.</span><span class="sxs-lookup"><span data-stu-id="e41cd-161">Select the **location** for the data factory.</span></span> <span data-ttu-id="e41cd-162">Only regions supported by the Data Factory service are shown in the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="e41cd-162">Only regions supported by the Data Factory service are shown in the drop-down list.</span></span>
   5. <span data-ttu-id="e41cd-163">Select **Pin to Startboard**.</span><span class="sxs-lookup"><span data-stu-id="e41cd-163">Select **Pin to Startboard**.</span></span>     
   6. <span data-ttu-id="e41cd-164">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="e41cd-164">Click **Create**.</span></span>
      
      > [!IMPORTANT]
      > To create Data Factory instances, you must be a member of the [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at the subscription/resource group level.
      > 
      > The name of the data factory may be registered as a DNS name in the future and hence become publically visible.                
      > 
      > 
3. <span data-ttu-id="e41cd-167">To see the status/notification messages, click the bell icon on the toolbar.</span><span class="sxs-lookup"><span data-stu-id="e41cd-167">To see the status/notification messages, click the bell icon on the toolbar.</span></span> 
   
   ![Notification messages](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-activity-tutorial-using-azure-portal/Notifications.png) 
4. <span data-ttu-id="e41cd-169">After the creation is complete, you see the **Data Factory** blade as shown in the image.</span><span class="sxs-lookup"><span data-stu-id="e41cd-169">After the creation is complete, you see the **Data Factory** blade as shown in the image.</span></span>
   
   ![Data factory home page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-data-factory-home-page.png)

## <a name="create-linked-services"></a><span data-ttu-id="e41cd-171">Create linked services</span><span class="sxs-lookup"><span data-stu-id="e41cd-171">Create linked services</span></span>
<span data-ttu-id="e41cd-172">Linked services link data stores or compute services to an Azure data factory.</span><span class="sxs-lookup"><span data-stu-id="e41cd-172">Linked services link data stores or compute services to an Azure data factory.</span></span> <span data-ttu-id="e41cd-173">See [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) for all the sources and sinks supported by the Copy Activity.</span><span class="sxs-lookup"><span data-stu-id="e41cd-173">See [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) for all the sources and sinks supported by the Copy Activity.</span></span> <span data-ttu-id="e41cd-174">See [compute linked services](data-factory-compute-linked-services.md) for the list of compute services supported by Data Factory.</span><span class="sxs-lookup"><span data-stu-id="e41cd-174">See [compute linked services](data-factory-compute-linked-services.md) for the list of compute services supported by Data Factory.</span></span> <span data-ttu-id="e41cd-175">In this tutorial, you do not use any compute service.</span><span class="sxs-lookup"><span data-stu-id="e41cd-175">In this tutorial, you do not use any compute service.</span></span> 

<span data-ttu-id="e41cd-176">In this step, you create two linked services: **AzureStorageLinkedService** and **AzureSqlLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="e41cd-176">In this step, you create two linked services: **AzureStorageLinkedService** and **AzureSqlLinkedService**.</span></span> <span data-ttu-id="e41cd-177">AzureStorageLinkedService linked service links an Azure Storage Account and AzureSqlLinkedService links an Azure SQL database to the **ADFTutorialDataFactory**.</span><span class="sxs-lookup"><span data-stu-id="e41cd-177">AzureStorageLinkedService linked service links an Azure Storage Account and AzureSqlLinkedService links an Azure SQL database to the **ADFTutorialDataFactory**.</span></span> <span data-ttu-id="e41cd-178">You create a pipeline later in this tutorial that copies data from a blob container in AzureStorageLinkedService to a SQL table in AzureSqlLinkedService.</span><span class="sxs-lookup"><span data-stu-id="e41cd-178">You create a pipeline later in this tutorial that copies data from a blob container in AzureStorageLinkedService to a SQL table in AzureSqlLinkedService.</span></span>

### <a name="create-a-linked-service-for-the-azure-storage-account"></a><span data-ttu-id="e41cd-179">Create a linked service for the Azure storage account</span><span class="sxs-lookup"><span data-stu-id="e41cd-179">Create a linked service for the Azure storage account</span></span>
1. <span data-ttu-id="e41cd-180">In the **Data Factory** blade, click **Author and deploy** tile to launch the **Editor** for the data factory.</span><span class="sxs-lookup"><span data-stu-id="e41cd-180">In the **Data Factory** blade, click **Author and deploy** tile to launch the **Editor** for the data factory.</span></span>
   
   ![Author and Deploy Tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-author-deploy-tile.png) 
2. <span data-ttu-id="e41cd-182">In the **Editor**, click **New data store** button on the toolbar and select **Azure storage** from the drop-down menu.</span><span class="sxs-lookup"><span data-stu-id="e41cd-182">In the **Editor**, click **New data store** button on the toolbar and select **Azure storage** from the drop-down menu.</span></span> <span data-ttu-id="e41cd-183">You should see the JSON template for creating an Azure storage linked service in the right pane.</span><span class="sxs-lookup"><span data-stu-id="e41cd-183">You should see the JSON template for creating an Azure storage linked service in the right pane.</span></span> 
   
    ![Editor New data store button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-editor-newdatastore-button.png)    
3. <span data-ttu-id="e41cd-185">Replace `<accountname>` and `<accountkey>` with the account name and account key values for your Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="e41cd-185">Replace `<accountname>` and `<accountkey>` with the account name and account key values for your Azure storage account.</span></span> 
   
    ![Editor Blob Storage JSON](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-editor-blob-storage-json.png)    
4. <span data-ttu-id="e41cd-187">Click **Deploy** on the toolbar.</span><span class="sxs-lookup"><span data-stu-id="e41cd-187">Click **Deploy** on the toolbar.</span></span> <span data-ttu-id="e41cd-188">You should see the deployed **AzureStorageLinkedService** in the tree view now.</span><span class="sxs-lookup"><span data-stu-id="e41cd-188">You should see the deployed **AzureStorageLinkedService** in the tree view now.</span></span> 
   
    ![Editor Blob Storage Deploy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-editor-blob-storage-deploy.png)

> [!NOTE]
> See [Move data from/to Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties.
> 
> 

### <a name="create-a-linked-service-for-the-azure-sql-database"></a><span data-ttu-id="e41cd-191">Create a linked service for the Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="e41cd-191">Create a linked service for the Azure SQL Database</span></span>
1. <span data-ttu-id="e41cd-192">In the **Data Factory Editor**, click **New data store** button on the toolbar and select **Azure SQL Database** from the drop-down menu.</span><span class="sxs-lookup"><span data-stu-id="e41cd-192">In the **Data Factory Editor**, click **New data store** button on the toolbar and select **Azure SQL Database** from the drop-down menu.</span></span> <span data-ttu-id="e41cd-193">You should see the JSON template for creating the Azure SQL linked service in the right pane.</span><span class="sxs-lookup"><span data-stu-id="e41cd-193">You should see the JSON template for creating the Azure SQL linked service in the right pane.</span></span>
2. <span data-ttu-id="e41cd-194">Replace `<servername>`, `<databasename>`, `<username>@<servername>`, and `<password>` with names of your Azure SQL server, database, user account, and password.</span><span class="sxs-lookup"><span data-stu-id="e41cd-194">Replace `<servername>`, `<databasename>`, `<username>@<servername>`, and `<password>` with names of your Azure SQL server, database, user account, and password.</span></span> 
3. <span data-ttu-id="e41cd-195">Click **Deploy** on the toolbar to create and deploy the **AzureSqlLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="e41cd-195">Click **Deploy** on the toolbar to create and deploy the **AzureSqlLinkedService**.</span></span>
4. <span data-ttu-id="e41cd-196">Confirm that you see **AzureSqlLinkedService** in the tree view.</span><span class="sxs-lookup"><span data-stu-id="e41cd-196">Confirm that you see **AzureSqlLinkedService** in the tree view.</span></span> 

> [!NOTE]
> See [Move data from/to Azure SQL Database](data-factory-azure-sql-connector.md#linked-service-properties) for details about JSON properties.
> 
> 

## <a name="create-datasets"></a><span data-ttu-id="e41cd-198">Create datasets</span><span class="sxs-lookup"><span data-stu-id="e41cd-198">Create datasets</span></span>
<span data-ttu-id="e41cd-199">In the previous step, you created linked services **AzureStorageLinkedService** and **AzureSqlLinkedService** to link an Azure Storage account and Azure SQL database to the data factory: **ADFTutorialDataFactory**.</span><span class="sxs-lookup"><span data-stu-id="e41cd-199">In the previous step, you created linked services **AzureStorageLinkedService** and **AzureSqlLinkedService** to link an Azure Storage account and Azure SQL database to the data factory: **ADFTutorialDataFactory**.</span></span> <span data-ttu-id="e41cd-200">In this step, you define two datasets -- **InputDataset** and **OutputDataset** -- that represent the input/output data that is stored in the data stores referred by AzureStorageLinkedService and AzureSqlLinkedService respectively.</span><span class="sxs-lookup"><span data-stu-id="e41cd-200">In this step, you define two datasets -- **InputDataset** and **OutputDataset** -- that represent the input/output data that is stored in the data stores referred by AzureStorageLinkedService and AzureSqlLinkedService respectively.</span></span> <span data-ttu-id="e41cd-201">For InputDataset, you specify the blob container that contains a blob with the source data and for OutputDataset, you specify the SQL table that stores the output data.</span><span class="sxs-lookup"><span data-stu-id="e41cd-201">For InputDataset, you specify the blob container that contains a blob with the source data and for OutputDataset, you specify the SQL table that stores the output data.</span></span> 

### <a name="create-input-dataset"></a><span data-ttu-id="e41cd-202">Create input dataset</span><span class="sxs-lookup"><span data-stu-id="e41cd-202">Create input dataset</span></span>
<span data-ttu-id="e41cd-203">In this step, you create a dataset named **InputDataset** that points to a blob container in the Azure Storage represented by the **AzureStorageLinkedService** linked service.</span><span class="sxs-lookup"><span data-stu-id="e41cd-203">In this step, you create a dataset named **InputDataset** that points to a blob container in the Azure Storage represented by the **AzureStorageLinkedService** linked service.</span></span>

1. <span data-ttu-id="e41cd-204">In the **Editor** for the Data Factory, click **... More**, click **New dataset**, and click **Azure Blob storage** from the drop-down menu.</span><span class="sxs-lookup"><span data-stu-id="e41cd-204">In the **Editor** for the Data Factory, click **... More**, click **New dataset**, and click **Azure Blob storage** from the drop-down menu.</span></span> 
   
    ![New dataset menu](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-activity-tutorial-using-azure-portal/new-dataset-menu.png)
2. <span data-ttu-id="e41cd-206">Replace JSON in the right pane with the following JSON snippet:</span><span class="sxs-lookup"><span data-stu-id="e41cd-206">Replace JSON in the right pane with the following JSON snippet:</span></span> 
   
    ```JSON
    {
      "name": "InputDataset",
      "properties": {
        "structure": [
          {
            "name": "FirstName",
            "type": "String"
          },
          {
            "name": "LastName",
            "type": "String"
          }
        ],
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
          "folderPath": "adftutorial/",
          "fileName": "emp.txt",
          "format": {
            "type": "TextFormat",
            "columnDelimiter": ","
          }
        },
        "external": true,
        "availability": {
          "frequency": "Hour",
          "interval": 1
        }
      }
    }
    ```   
    <span data-ttu-id="e41cd-207">Note the following points:</span><span class="sxs-lookup"><span data-stu-id="e41cd-207">Note the following points:</span></span> 
   
    - <span data-ttu-id="e41cd-208">dataset **type** is set to **AzureBlob**.</span><span class="sxs-lookup"><span data-stu-id="e41cd-208">dataset **type** is set to **AzureBlob**.</span></span>
    - <span data-ttu-id="e41cd-209">**linkedServiceName** is set to **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="e41cd-209">**linkedServiceName** is set to **AzureStorageLinkedService**.</span></span> <span data-ttu-id="e41cd-210">You created this linked service in Step 2.</span><span class="sxs-lookup"><span data-stu-id="e41cd-210">You created this linked service in Step 2.</span></span>
    - <span data-ttu-id="e41cd-211">**folderPath** is set to the **adftutorial** container.</span><span class="sxs-lookup"><span data-stu-id="e41cd-211">**folderPath** is set to the **adftutorial** container.</span></span> <span data-ttu-id="e41cd-212">You can also specify the name of a blob within the folder using the **fileName** property.</span><span class="sxs-lookup"><span data-stu-id="e41cd-212">You can also specify the name of a blob within the folder using the **fileName** property.</span></span> <span data-ttu-id="e41cd-213">Since you are not specifying the name of the blob, data from all blobs in the container is considered as an input data.</span><span class="sxs-lookup"><span data-stu-id="e41cd-213">Since you are not specifying the name of the blob, data from all blobs in the container is considered as an input data.</span></span>
    - <span data-ttu-id="e41cd-214">format **type** is set to **TextFormat**</span><span class="sxs-lookup"><span data-stu-id="e41cd-214">format **type** is set to **TextFormat**</span></span>
    - <span data-ttu-id="e41cd-215">There are two fields in the text file – **FirstName** and **LastName** separated by a comma character (**columnDelimiter**)</span><span class="sxs-lookup"><span data-stu-id="e41cd-215">There are two fields in the text file – **FirstName** and **LastName** separated by a comma character (**columnDelimiter**)</span></span>
    - <span data-ttu-id="e41cd-216">The **availability** is set to **hourly** (**frequency** is set to **hour** and **interval** is set to **1**).</span><span class="sxs-lookup"><span data-stu-id="e41cd-216">The **availability** is set to **hourly** (**frequency** is set to **hour** and **interval** is set to **1**).</span></span> <span data-ttu-id="e41cd-217">Therefore, Data Factory looks for input data every hour in the root folder of blob container (**adftutorial**) you specified.</span><span class="sxs-lookup"><span data-stu-id="e41cd-217">Therefore, Data Factory looks for input data every hour in the root folder of blob container (**adftutorial**) you specified.</span></span> 
     
     <span data-ttu-id="e41cd-218">if you don't specify a **fileName** for an **input** dataset, all files/blobs from the input folder (**folderPath**) are considered as inputs.</span><span class="sxs-lookup"><span data-stu-id="e41cd-218">if you don't specify a **fileName** for an **input** dataset, all files/blobs from the input folder (**folderPath**) are considered as inputs.</span></span> <span data-ttu-id="e41cd-219">If you specify a fileName in the JSON, only the specified file/blob is considered asn input.</span><span class="sxs-lookup"><span data-stu-id="e41cd-219">If you specify a fileName in the JSON, only the specified file/blob is considered asn input.</span></span>
     
     <span data-ttu-id="e41cd-220">If you do not specify a **fileName** for an **output table**, the generated files in the **folderPath** are named in the following format: Data.&lt;Guid&gt;.txt (example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.).</span><span class="sxs-lookup"><span data-stu-id="e41cd-220">If you do not specify a **fileName** for an **output table**, the generated files in the **folderPath** are named in the following format: Data.&lt;Guid&gt;.txt (example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.).</span></span>
     
     <span data-ttu-id="e41cd-221">To set **folderPath** and **fileName** dynamically based on the **SliceStart** time, use the **partitionedBy** property.</span><span class="sxs-lookup"><span data-stu-id="e41cd-221">To set **folderPath** and **fileName** dynamically based on the **SliceStart** time, use the **partitionedBy** property.</span></span> <span data-ttu-id="e41cd-222">In the following example, folderPath uses Year, Month, and Day from the SliceStart (start time of the slice being processed) and fileName uses Hour from the SliceStart.</span><span class="sxs-lookup"><span data-stu-id="e41cd-222">In the following example, folderPath uses Year, Month, and Day from the SliceStart (start time of the slice being processed) and fileName uses Hour from the SliceStart.</span></span> <span data-ttu-id="e41cd-223">For example, if a slice is being produced for 2016-09-20T08:00:00, the folderName is set to wikidatagateway/wikisampledataout/2016/09/20 and the fileName is set to 08.csv.</span><span class="sxs-lookup"><span data-stu-id="e41cd-223">For example, if a slice is being produced for 2016-09-20T08:00:00, the folderName is set to wikidatagateway/wikisampledataout/2016/09/20 and the fileName is set to 08.csv.</span></span> 

    ```JSON     
    "folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
    "fileName": "{Hour}.csv",
    "partitionedBy": 
    [
       { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
       { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } }, 
       { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } }, 
       { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } } 
    ],
    ```
3. <span data-ttu-id="e41cd-224">Click **Deploy** on the toolbar to create and deploy the **InputDataset** dataset.</span><span class="sxs-lookup"><span data-stu-id="e41cd-224">Click **Deploy** on the toolbar to create and deploy the **InputDataset** dataset.</span></span> <span data-ttu-id="e41cd-225">Confirm that you see the **InputDataset** in the tree view.</span><span class="sxs-lookup"><span data-stu-id="e41cd-225">Confirm that you see the **InputDataset** in the tree view.</span></span>

> [!NOTE]
> See [Move data from/to Azure Blob](data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties.
> 
> 

### <a name="create-output-dataset"></a><span data-ttu-id="e41cd-227">Create output dataset</span><span class="sxs-lookup"><span data-stu-id="e41cd-227">Create output dataset</span></span>
<span data-ttu-id="e41cd-228">In this part of the step, you create an output dataset named **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="e41cd-228">In this part of the step, you create an output dataset named **OutputDataset**.</span></span> <span data-ttu-id="e41cd-229">This dataset points to a SQL table in the Azure SQL database represented by **AzureSqlLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="e41cd-229">This dataset points to a SQL table in the Azure SQL database represented by **AzureSqlLinkedService**.</span></span> 

1. <span data-ttu-id="e41cd-230">In the **Editor** for the Data Factory, click **... More**, click **New dataset**, and click **Azure SQL** from the drop-down menu.</span><span class="sxs-lookup"><span data-stu-id="e41cd-230">In the **Editor** for the Data Factory, click **... More**, click **New dataset**, and click **Azure SQL** from the drop-down menu.</span></span> 
2. <span data-ttu-id="e41cd-231">Replace JSON in the right pane with the following JSON snippet:</span><span class="sxs-lookup"><span data-stu-id="e41cd-231">Replace JSON in the right pane with the following JSON snippet:</span></span>

    ```JSON   
    {
      "name": "OutputDataset",
      "properties": {
        "structure": [
          {
            "name": "FirstName",
            "type": "String"
          },
          {
            "name": "LastName",
            "type": "String"
          }
        ],
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
          "tableName": "emp"
        },
        "availability": {
          "frequency": "Hour",
          "interval": 1
        }
      }
    }
    ```     
    <span data-ttu-id="e41cd-232">Note the following points:</span><span class="sxs-lookup"><span data-stu-id="e41cd-232">Note the following points:</span></span> 
   
    - <span data-ttu-id="e41cd-233">dataset **type** is set to **AzureSQLTable**.</span><span class="sxs-lookup"><span data-stu-id="e41cd-233">dataset **type** is set to **AzureSQLTable**.</span></span>
    - <span data-ttu-id="e41cd-234">**linkedServiceName** is set to **AzureSqlLinkedService** (you created this linked service in Step 2).</span><span class="sxs-lookup"><span data-stu-id="e41cd-234">**linkedServiceName** is set to **AzureSqlLinkedService** (you created this linked service in Step 2).</span></span>
    - <span data-ttu-id="e41cd-235">**tablename** is set to **emp**.</span><span class="sxs-lookup"><span data-stu-id="e41cd-235">**tablename** is set to **emp**.</span></span>
    - <span data-ttu-id="e41cd-236">There are three columns – **ID**, **FirstName**, and **LastName** – in the emp table in the database.</span><span class="sxs-lookup"><span data-stu-id="e41cd-236">There are three columns – **ID**, **FirstName**, and **LastName** – in the emp table in the database.</span></span> <span data-ttu-id="e41cd-237">ID is an identity column, so you need to specify only **FirstName** and **LastName** here.</span><span class="sxs-lookup"><span data-stu-id="e41cd-237">ID is an identity column, so you need to specify only **FirstName** and **LastName** here.</span></span>
    - <span data-ttu-id="e41cd-238">The **availability** is set to **hourly** (**frequency** set to **hour** and **interval** set to **1**).</span><span class="sxs-lookup"><span data-stu-id="e41cd-238">The **availability** is set to **hourly** (**frequency** set to **hour** and **interval** set to **1**).</span></span>  <span data-ttu-id="e41cd-239">The Data Factory service generates an output data slice every hour in the **emp** table in the Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="e41cd-239">The Data Factory service generates an output data slice every hour in the **emp** table in the Azure SQL database.</span></span>
3. <span data-ttu-id="e41cd-240">Click **Deploy** on the toolbar to create and deploy the **OutputDataset** dataset.</span><span class="sxs-lookup"><span data-stu-id="e41cd-240">Click **Deploy** on the toolbar to create and deploy the **OutputDataset** dataset.</span></span> <span data-ttu-id="e41cd-241">Confirm that you see the **OutputDataset** in the tree view.</span><span class="sxs-lookup"><span data-stu-id="e41cd-241">Confirm that you see the **OutputDataset** in the tree view.</span></span> 

> [!NOTE]
> See [Move data from/to Azure SQL Database](data-factory-azure-sql-connector.md#linked-service-properties) for details about JSON properties.
> 
> 

## <a name="create-pipeline"></a><span data-ttu-id="e41cd-243">Create pipeline</span><span class="sxs-lookup"><span data-stu-id="e41cd-243">Create pipeline</span></span>
<span data-ttu-id="e41cd-244">In this step, you create a pipeline with a **Copy Activity** that uses **InputDataset** as input and **OutputDataset** as output.</span><span class="sxs-lookup"><span data-stu-id="e41cd-244">In this step, you create a pipeline with a **Copy Activity** that uses **InputDataset** as input and **OutputDataset** as output.</span></span>

1. <span data-ttu-id="e41cd-245">In the **Editor** for the Data Factory, click **... More**, and click **New pipeline**.</span><span class="sxs-lookup"><span data-stu-id="e41cd-245">In the **Editor** for the Data Factory, click **... More**, and click **New pipeline**.</span></span> <span data-ttu-id="e41cd-246">Alternatively, you can right-click **Pipelines** in the tree view and click **New pipeline**.</span><span class="sxs-lookup"><span data-stu-id="e41cd-246">Alternatively, you can right-click **Pipelines** in the tree view and click **New pipeline**.</span></span>
2. <span data-ttu-id="e41cd-247">Replace JSON in the right pane with the following JSON snippet:</span><span class="sxs-lookup"><span data-stu-id="e41cd-247">Replace JSON in the right pane with the following JSON snippet:</span></span> 

    ```JSON   
    {
      "name": "ADFTutorialPipeline",
      "properties": {
        "description": "Copy data from a blob to Azure SQL table",
        "activities": [
          {
            "name": "CopyFromBlobToSQL",
            "type": "Copy",
            "inputs": [
              {
                "name": "InputDataset"
              }
            ],
            "outputs": [
              {
                "name": "OutputDataset"
              }
            ],
            "typeProperties": {
              "source": {
                "type": "BlobSource"
              },
              "sink": {
                "type": "SqlSink",
                "writeBatchSize": 10000,
                "writeBatchTimeout": "60:00:00"
              }
            },
            "Policy": {
              "concurrency": 1,
              "executionPriorityOrder": "NewestFirst",
              "retry": 0,
              "timeout": "01:00:00"
            }
          }
        ],
        "start": "2016-07-12T00:00:00Z",
        "end": "2016-07-13T00:00:00Z"
      }
    } 
    ```   
    
    <span data-ttu-id="e41cd-248">Note the following points:</span><span class="sxs-lookup"><span data-stu-id="e41cd-248">Note the following points:</span></span>
   
    - <span data-ttu-id="e41cd-249">In the activities section, there is only one activity whose **type** is set to **Copy**.</span><span class="sxs-lookup"><span data-stu-id="e41cd-249">In the activities section, there is only one activity whose **type** is set to **Copy**.</span></span>
    - <span data-ttu-id="e41cd-250">Input for the activity is set to **InputDataset** and output for the activity is set to **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="e41cd-250">Input for the activity is set to **InputDataset** and output for the activity is set to **OutputDataset**.</span></span>
    - <span data-ttu-id="e41cd-251">In the **typeProperties** section, **BlobSource** is specified as the source type and **SqlSink** is specified as the sink type.</span><span class="sxs-lookup"><span data-stu-id="e41cd-251">In the **typeProperties** section, **BlobSource** is specified as the source type and **SqlSink** is specified as the sink type.</span></span>
     
    <span data-ttu-id="e41cd-252">Replace the value of the **start** property with the current day and **end** value with the next day.</span><span class="sxs-lookup"><span data-stu-id="e41cd-252">Replace the value of the **start** property with the current day and **end** value with the next day.</span></span> <span data-ttu-id="e41cd-253">You can specify only the date part and skip the time part of the date time.</span><span class="sxs-lookup"><span data-stu-id="e41cd-253">You can specify only the date part and skip the time part of the date time.</span></span> <span data-ttu-id="e41cd-254">For example, "2016-02-03", which is equivalent to "2016-02-03T00:00:00Z"</span><span class="sxs-lookup"><span data-stu-id="e41cd-254">For example, "2016-02-03", which is equivalent to "2016-02-03T00:00:00Z"</span></span>
     
    <span data-ttu-id="e41cd-255">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="e41cd-255">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="e41cd-256">For example: 2016-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="e41cd-256">For example: 2016-10-14T16:32:41Z.</span></span> <span data-ttu-id="e41cd-257">The **end** time is optional, but we use it in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="e41cd-257">The **end** time is optional, but we use it in this tutorial.</span></span> 
     
    <span data-ttu-id="e41cd-258">If you do not specify value for the **end** property, it is calculated as "**start + 48 hours**".</span><span class="sxs-lookup"><span data-stu-id="e41cd-258">If you do not specify value for the **end** property, it is calculated as "**start + 48 hours**".</span></span> <span data-ttu-id="e41cd-259">To run the pipeline indefinitely, specify **9999-09-09** as the value for the **end** property.</span><span class="sxs-lookup"><span data-stu-id="e41cd-259">To run the pipeline indefinitely, specify **9999-09-09** as the value for the **end** property.</span></span>
     
    <span data-ttu-id="e41cd-260">In the preceding example, there are 24 data slices as each data slice is produced hourly.</span><span class="sxs-lookup"><span data-stu-id="e41cd-260">In the preceding example, there are 24 data slices as each data slice is produced hourly.</span></span>
3. <span data-ttu-id="e41cd-261">Click **Deploy** on the toolbar to create and deploy the **ADFTutorialPipeline**.</span><span class="sxs-lookup"><span data-stu-id="e41cd-261">Click **Deploy** on the toolbar to create and deploy the **ADFTutorialPipeline**.</span></span> <span data-ttu-id="e41cd-262">Confirm that you see the pipeline in the tree view.</span><span class="sxs-lookup"><span data-stu-id="e41cd-262">Confirm that you see the pipeline in the tree view.</span></span> 
4. <span data-ttu-id="e41cd-263">Now, close the **Editor** blade by clicking **X**. Click **X** again to see the **Data Factory** home page for the **ADFTutorialDataFactory**.</span><span class="sxs-lookup"><span data-stu-id="e41cd-263">Now, close the **Editor** blade by clicking **X**. Click **X** again to see the **Data Factory** home page for the **ADFTutorialDataFactory**.</span></span>

<span data-ttu-id="e41cd-264">**Congratulations!**</span><span class="sxs-lookup"><span data-stu-id="e41cd-264">**Congratulations!**</span></span> <span data-ttu-id="e41cd-265">You have successfully created an Azure data factory, linked services, tables, and a pipeline and scheduled the pipeline.</span><span class="sxs-lookup"><span data-stu-id="e41cd-265">You have successfully created an Azure data factory, linked services, tables, and a pipeline and scheduled the pipeline.</span></span>   

### <a name="view-the-data-factory-in-a-diagram-view"></a><span data-ttu-id="e41cd-266">View the data factory in a Diagram View</span><span class="sxs-lookup"><span data-stu-id="e41cd-266">View the data factory in a Diagram View</span></span>
1. <span data-ttu-id="e41cd-267">In the **Data Factory** blade, click **Diagram**.</span><span class="sxs-lookup"><span data-stu-id="e41cd-267">In the **Data Factory** blade, click **Diagram**.</span></span>
   
    ![Data Factory Blade - Diagram Tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-datafactoryblade-diagramtile.png)
2. <span data-ttu-id="e41cd-269">You should see the diagram similar to the following image:</span><span class="sxs-lookup"><span data-stu-id="e41cd-269">You should see the diagram similar to the following image:</span></span> 
   
    ![Diagram view](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-diagram-blade.png)
   
    <span data-ttu-id="e41cd-271">You can zoom in, zoom out, zoom to 100%, zoom to fit, automatically position pipelines and tables, and show lineage information (highlights upstream and downstream items of selected items).</span><span class="sxs-lookup"><span data-stu-id="e41cd-271">You can zoom in, zoom out, zoom to 100%, zoom to fit, automatically position pipelines and tables, and show lineage information (highlights upstream and downstream items of selected items).</span></span>  <span data-ttu-id="e41cd-272">You can double-click an object (input/output table or pipeline) to see properties for it.</span><span class="sxs-lookup"><span data-stu-id="e41cd-272">You can double-click an object (input/output table or pipeline) to see properties for it.</span></span> 
3. <span data-ttu-id="e41cd-273">Right-click **ADFTutorialPipeline** in the Diagram View and click **Open pipeline**.</span><span class="sxs-lookup"><span data-stu-id="e41cd-273">Right-click **ADFTutorialPipeline** in the Diagram View and click **Open pipeline**.</span></span> 
   
    ![Open Pipeline](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-activity-tutorial-using-azure-portal/DiagramView-OpenPipeline.png)
4. <span data-ttu-id="e41cd-275">You should see the activities in the pipeline along with input and output datasets for the activities.</span><span class="sxs-lookup"><span data-stu-id="e41cd-275">You should see the activities in the pipeline along with input and output datasets for the activities.</span></span> <span data-ttu-id="e41cd-276">In this tutorial, you have only one activity in the pipeline (Copy Activity) with InputDataset as input dataset and OutputDataset as output dataset.</span><span class="sxs-lookup"><span data-stu-id="e41cd-276">In this tutorial, you have only one activity in the pipeline (Copy Activity) with InputDataset as input dataset and OutputDataset as output dataset.</span></span>   
   
    ![Opened pipeline view](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-activity-tutorial-using-azure-portal/DiagramView-OpenedPipeline.png)
5. <span data-ttu-id="e41cd-278">Click **Data factory** in the breadcrumb in the top-left corner to get back to the diagram view.</span><span class="sxs-lookup"><span data-stu-id="e41cd-278">Click **Data factory** in the breadcrumb in the top-left corner to get back to the diagram view.</span></span> <span data-ttu-id="e41cd-279">The diagram view displays all the pipelines.</span><span class="sxs-lookup"><span data-stu-id="e41cd-279">The diagram view displays all the pipelines.</span></span> <span data-ttu-id="e41cd-280">In this example, you have only created one pipeline.</span><span class="sxs-lookup"><span data-stu-id="e41cd-280">In this example, you have only created one pipeline.</span></span>   

## <a name="monitor-pipeline"></a><span data-ttu-id="e41cd-281">Monitor pipeline</span><span class="sxs-lookup"><span data-stu-id="e41cd-281">Monitor pipeline</span></span>
<span data-ttu-id="e41cd-282">In this step, you use the Azure portal to monitor what’s going on in an Azure data factory.</span><span class="sxs-lookup"><span data-stu-id="e41cd-282">In this step, you use the Azure portal to monitor what’s going on in an Azure data factory.</span></span> 

### <a name="monitor-pipeline-using-diagram-view"></a><span data-ttu-id="e41cd-283">Monitor pipeline using Diagram View</span><span class="sxs-lookup"><span data-stu-id="e41cd-283">Monitor pipeline using Diagram View</span></span>
1. <span data-ttu-id="e41cd-284">Click **X** to close the **Diagram** view to see the Data Factory home page for the data factory.</span><span class="sxs-lookup"><span data-stu-id="e41cd-284">Click **X** to close the **Diagram** view to see the Data Factory home page for the data factory.</span></span> <span data-ttu-id="e41cd-285">If you have closed the web browser, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="e41cd-285">If you have closed the web browser, do the following steps:</span></span> 
   1. <span data-ttu-id="e41cd-286">Navigate to [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="e41cd-286">Navigate to [Azure portal](https://portal.azure.com/).</span></span> 
   2. <span data-ttu-id="e41cd-287">Double-click **ADFTutorialDataFactory** on the **Startboard** (or) click **Data factories** on the left menu, and search for ADFTutorialDataFactory.</span><span class="sxs-lookup"><span data-stu-id="e41cd-287">Double-click **ADFTutorialDataFactory** on the **Startboard** (or) click **Data factories** on the left menu, and search for ADFTutorialDataFactory.</span></span> 
2. <span data-ttu-id="e41cd-288">You should see the count and names of tables and pipeline you created on this blade.</span><span class="sxs-lookup"><span data-stu-id="e41cd-288">You should see the count and names of tables and pipeline you created on this blade.</span></span>
   
    ![home page with names](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-datafactory-home-page-pipeline-tables.png)
3. <span data-ttu-id="e41cd-290">Now, click **Datasets** tile.</span><span class="sxs-lookup"><span data-stu-id="e41cd-290">Now, click **Datasets** tile.</span></span>
4. <span data-ttu-id="e41cd-291">In the **Datasets** blade, click **InputDataset**.</span><span class="sxs-lookup"><span data-stu-id="e41cd-291">In the **Datasets** blade, click **InputDataset**.</span></span> <span data-ttu-id="e41cd-292">This dataset is the input dataset for **ADFTutorialPipeline**.</span><span class="sxs-lookup"><span data-stu-id="e41cd-292">This dataset is the input dataset for **ADFTutorialPipeline**.</span></span>
   
    ![Datasets with InputDataset selected](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-activity-tutorial-using-azure-portal/DataSetsWithInputDatasetFromBlobSelected.png)   
5. <span data-ttu-id="e41cd-294">Click **... (ellipsis)** to see all the data slices.</span><span class="sxs-lookup"><span data-stu-id="e41cd-294">Click **... (ellipsis)** to see all the data slices.</span></span>
   
    ![All input data slices](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-activity-tutorial-using-azure-portal/all-input-slices.png)  
   
    <span data-ttu-id="e41cd-296">Notice that all the data slices up to the current time are **Ready** because the **emp.txt** file exists all the time in the blob container: **adftutorial\input**.</span><span class="sxs-lookup"><span data-stu-id="e41cd-296">Notice that all the data slices up to the current time are **Ready** because the **emp.txt** file exists all the time in the blob container: **adftutorial\input**.</span></span> <span data-ttu-id="e41cd-297">Confirm that no slices show up in the **Recently failed slices** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="e41cd-297">Confirm that no slices show up in the **Recently failed slices** section at the bottom.</span></span>
   
    <span data-ttu-id="e41cd-298">Both **Recently updated slices** and **Recently failed slices** lists are sorted by the **LAST UPDATE TIME**.</span><span class="sxs-lookup"><span data-stu-id="e41cd-298">Both **Recently updated slices** and **Recently failed slices** lists are sorted by the **LAST UPDATE TIME**.</span></span> 
   
    <span data-ttu-id="e41cd-299">Click **Filter** on the toolbar to filter the slices.</span><span class="sxs-lookup"><span data-stu-id="e41cd-299">Click **Filter** on the toolbar to filter the slices.</span></span>  
   
    ![Filter input slices](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-activity-tutorial-using-azure-portal/filter-input-slices.png)
6. <span data-ttu-id="e41cd-301">Close the blades until you see the **Datasets** blade.</span><span class="sxs-lookup"><span data-stu-id="e41cd-301">Close the blades until you see the **Datasets** blade.</span></span> <span data-ttu-id="e41cd-302">Click the **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="e41cd-302">Click the **OutputDataset**.</span></span> <span data-ttu-id="e41cd-303">This dataset is the output dataset for **ADFTutorialPipeline**.</span><span class="sxs-lookup"><span data-stu-id="e41cd-303">This dataset is the output dataset for **ADFTutorialPipeline**.</span></span>
   
    ![data sets blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-datasets-blade.png)
7. <span data-ttu-id="e41cd-305">You should see the **OutputDataset** blade as shown in the following image:</span><span class="sxs-lookup"><span data-stu-id="e41cd-305">You should see the **OutputDataset** blade as shown in the following image:</span></span>
   
    ![table blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-table-blade.png) 
8. <span data-ttu-id="e41cd-307">Notice that the data slices up to the current time have already been produced and they are **Ready**.</span><span class="sxs-lookup"><span data-stu-id="e41cd-307">Notice that the data slices up to the current time have already been produced and they are **Ready**.</span></span> <span data-ttu-id="e41cd-308">No slices show up in the **Problem slices** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="e41cd-308">No slices show up in the **Problem slices** section at the bottom.</span></span>
9. <span data-ttu-id="e41cd-309">Click **… (Ellipsis)** to see all the slices.</span><span class="sxs-lookup"><span data-stu-id="e41cd-309">Click **… (Ellipsis)** to see all the slices.</span></span>
   
    ![data slices blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-dataslices-blade.png)
10. <span data-ttu-id="e41cd-311">Click any data slice from the list and you should see the **Data slice** blade.</span><span class="sxs-lookup"><span data-stu-id="e41cd-311">Click any data slice from the list and you should see the **Data slice** blade.</span></span>
    
     ![data slice blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-dataslice-blade.png)
    
     <span data-ttu-id="e41cd-313">If the slice is not in the **Ready** state, you can see the upstream slices that are not Ready and are blocking the current slice from executing in the **Upstream slices that are not ready** list.</span><span class="sxs-lookup"><span data-stu-id="e41cd-313">If the slice is not in the **Ready** state, you can see the upstream slices that are not Ready and are blocking the current slice from executing in the **Upstream slices that are not ready** list.</span></span>
11. <span data-ttu-id="e41cd-314">In the **DATA SLICE** blade, you should see all activity runs in the list at the bottom.</span><span class="sxs-lookup"><span data-stu-id="e41cd-314">In the **DATA SLICE** blade, you should see all activity runs in the list at the bottom.</span></span> <span data-ttu-id="e41cd-315">Click an **activity run** to see the **Activity run details** blade.</span><span class="sxs-lookup"><span data-stu-id="e41cd-315">Click an **activity run** to see the **Activity run details** blade.</span></span> 
    
    ![Activity Run Details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-activity-tutorial-using-azure-portal/ActivityRunDetails.png)
12. <span data-ttu-id="e41cd-317">Click **X** to close all the blades until you get back to the home blade for the **ADFTutorialDataFactory**.</span><span class="sxs-lookup"><span data-stu-id="e41cd-317">Click **X** to close all the blades until you get back to the home blade for the **ADFTutorialDataFactory**.</span></span>
13. <span data-ttu-id="e41cd-318">(optional) Click **Pipelines** on the home page for **ADFTutorialDataFactory**, click **ADFTutorialPipeline** in the **Pipelines** blade, and drill through input tables (**Consumed**) or output tables (**Produced**).</span><span class="sxs-lookup"><span data-stu-id="e41cd-318">(optional) Click **Pipelines** on the home page for **ADFTutorialDataFactory**, click **ADFTutorialPipeline** in the **Pipelines** blade, and drill through input tables (**Consumed**) or output tables (**Produced**).</span></span>
14. <span data-ttu-id="e41cd-319">Launch **SQL Server Management Studio**, connect to the Azure SQL Database, and verify that the rows are inserted in to the **emp** table in the database.</span><span class="sxs-lookup"><span data-stu-id="e41cd-319">Launch **SQL Server Management Studio**, connect to the Azure SQL Database, and verify that the rows are inserted in to the **emp** table in the database.</span></span>
    
    ![sql query results](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-sql-query-results.png)

### <a name="monitor-pipeline-using-monitor--manage-app"></a><span data-ttu-id="e41cd-321">Monitor pipeline using Monitor & Manage App</span><span class="sxs-lookup"><span data-stu-id="e41cd-321">Monitor pipeline using Monitor & Manage App</span></span>
<span data-ttu-id="e41cd-322">You can also use Monitor & Manage application to monitor your pipelines.</span><span class="sxs-lookup"><span data-stu-id="e41cd-322">You can also use Monitor & Manage application to monitor your pipelines.</span></span> <span data-ttu-id="e41cd-323">For detailed information about using this application, see [Monitor and manage Azure Data Factory pipelines using Monitoring and Management App](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="e41cd-323">For detailed information about using this application, see [Monitor and manage Azure Data Factory pipelines using Monitoring and Management App](data-factory-monitor-manage-app.md).</span></span>

1. <span data-ttu-id="e41cd-324">Click **Monitor & Manage** tile on the home page for your data factory.</span><span class="sxs-lookup"><span data-stu-id="e41cd-324">Click **Monitor & Manage** tile on the home page for your data factory.</span></span>
   
    ![Monitor & Manage tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-activity-tutorial-using-azure-portal/monitor-manage-tile.png) 
2. <span data-ttu-id="e41cd-326">You should see **Monitor & Manage application**.</span><span class="sxs-lookup"><span data-stu-id="e41cd-326">You should see **Monitor & Manage application**.</span></span> <span data-ttu-id="e41cd-327">Change the **Start time** and **End time** to include start (2016-07-12) and end times (2016-07-13) of your pipeline, and click **Apply**.</span><span class="sxs-lookup"><span data-stu-id="e41cd-327">Change the **Start time** and **End time** to include start (2016-07-12) and end times (2016-07-13) of your pipeline, and click **Apply**.</span></span> 
   
    ![Monitor & Manage App](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-activity-tutorial-using-azure-portal/monitor-and-manage-app.png) 
3. <span data-ttu-id="e41cd-329">Select an activity window in the **Activity Windows** list to see details about it.</span><span class="sxs-lookup"><span data-stu-id="e41cd-329">Select an activity window in the **Activity Windows** list to see details about it.</span></span> 
    <span data-ttu-id="e41cd-330">![Activity window details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-activity-tutorial-using-azure-portal/activity-window-details.png)</span><span class="sxs-lookup"><span data-stu-id="e41cd-330">![Activity window details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-activity-tutorial-using-azure-portal/activity-window-details.png)</span></span>

## <a name="summary"></a><span data-ttu-id="e41cd-331">Summary</span><span class="sxs-lookup"><span data-stu-id="e41cd-331">Summary</span></span>
<span data-ttu-id="e41cd-332">In this tutorial, you created an Azure data factory to copy data from an Azure blob to an Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="e41cd-332">In this tutorial, you created an Azure data factory to copy data from an Azure blob to an Azure SQL database.</span></span> <span data-ttu-id="e41cd-333">You used the Azure portal to create the data factory, linked services, datasets, and a pipeline.</span><span class="sxs-lookup"><span data-stu-id="e41cd-333">You used the Azure portal to create the data factory, linked services, datasets, and a pipeline.</span></span> <span data-ttu-id="e41cd-334">Here are the high-level steps you performed in this tutorial:</span><span class="sxs-lookup"><span data-stu-id="e41cd-334">Here are the high-level steps you performed in this tutorial:</span></span>  

1. <span data-ttu-id="e41cd-335">Created an Azure **data factory**.</span><span class="sxs-lookup"><span data-stu-id="e41cd-335">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="e41cd-336">Created **linked services**:</span><span class="sxs-lookup"><span data-stu-id="e41cd-336">Created **linked services**:</span></span>
   1. <span data-ttu-id="e41cd-337">An **Azure Storage** linked service to link your Azure Storage account that holds input data.</span><span class="sxs-lookup"><span data-stu-id="e41cd-337">An **Azure Storage** linked service to link your Azure Storage account that holds input data.</span></span>     
   2. <span data-ttu-id="e41cd-338">An **Azure SQL** linked service to link your Azure SQL database that holds the output data.</span><span class="sxs-lookup"><span data-stu-id="e41cd-338">An **Azure SQL** linked service to link your Azure SQL database that holds the output data.</span></span> 
3. <span data-ttu-id="e41cd-339">Created **datasets** that describe input data and output data for pipelines.</span><span class="sxs-lookup"><span data-stu-id="e41cd-339">Created **datasets** that describe input data and output data for pipelines.</span></span>
4. <span data-ttu-id="e41cd-340">Created a **pipeline** with a **Copy Activity** with **BlobSource** as source and **SqlSink** as sink.</span><span class="sxs-lookup"><span data-stu-id="e41cd-340">Created a **pipeline** with a **Copy Activity** with **BlobSource** as source and **SqlSink** as sink.</span></span>  

## <a name="see-also"></a><span data-ttu-id="e41cd-341">See Also</span><span class="sxs-lookup"><span data-stu-id="e41cd-341">See Also</span></span>
| <span data-ttu-id="e41cd-342">Topic</span><span class="sxs-lookup"><span data-stu-id="e41cd-342">Topic</span></span> | <span data-ttu-id="e41cd-343">Description</span><span class="sxs-lookup"><span data-stu-id="e41cd-343">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="e41cd-344">Pipelines</span><span class="sxs-lookup"><span data-stu-id="e41cd-344">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="e41cd-345">This article helps you understand pipelines and activities in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="e41cd-345">This article helps you understand pipelines and activities in Azure Data Factory.</span></span> |
| [<span data-ttu-id="e41cd-346">Datasets</span><span class="sxs-lookup"><span data-stu-id="e41cd-346">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="e41cd-347">This article helps you understand datasets in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="e41cd-347">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="e41cd-348">Scheduling and execution</span><span class="sxs-lookup"><span data-stu-id="e41cd-348">Scheduling and execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="e41cd-349">This article explains the scheduling and execution aspects of Azure Data Factory application model.</span><span class="sxs-lookup"><span data-stu-id="e41cd-349">This article explains the scheduling and execution aspects of Azure Data Factory application model.</span></span> |



























