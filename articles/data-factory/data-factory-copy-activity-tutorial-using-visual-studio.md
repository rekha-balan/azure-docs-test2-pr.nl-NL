---
title: 'Tutorial: Create a pipeline with Copy Activity using Visual Studio | Microsoft Docs'
description: In this tutorial, you create an Azure Data Factory pipeline with a Copy Activity by using Visual Studio.
services: data-factory
documentationcenter: ''
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 1751185b-ce0a-4ab2-a9c3-e37b4d149ca3
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/11/2017
ms.author: spelluru
ms.openlocfilehash: 0195d68e0151fa5ac43056b10faffced71d2a1c8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555783"
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-visual-studio"></a><span data-ttu-id="262c3-103">Tutorial: Create a pipeline with Copy Activity using Visual Studio</span><span class="sxs-lookup"><span data-stu-id="262c3-103">Tutorial: Create a pipeline with Copy Activity using Visual Studio</span></span>
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

<span data-ttu-id="262c3-112">This tutorial shows you how to create and monitor an Azure data factory using the Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="262c3-112">This tutorial shows you how to create and monitor an Azure data factory using the Visual Studio.</span></span> <span data-ttu-id="262c3-113">The pipeline in the data factory uses a Copy Activity to copy data from Azure Blob Storage to Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="262c3-113">The pipeline in the data factory uses a Copy Activity to copy data from Azure Blob Storage to Azure SQL Database.</span></span>

> [!NOTE]
> The data pipeline in this tutorial copies data from a source data store to a destination data store. It does not transform input data to produce output data. For a tutorial on how to transform data using Azure Data Factory, see [Tutorial: Build your first pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).
> 
> You can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity. See [Scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md) for detailed information.

<span data-ttu-id="262c3-119">Here are the steps you perform as part of this tutorial:</span><span class="sxs-lookup"><span data-stu-id="262c3-119">Here are the steps you perform as part of this tutorial:</span></span>

1. <span data-ttu-id="262c3-120">Create two linked services: **AzureStorageLinkedService1** and **AzureSqlinkedService1**.</span><span class="sxs-lookup"><span data-stu-id="262c3-120">Create two linked services: **AzureStorageLinkedService1** and **AzureSqlinkedService1**.</span></span> 
   
    <span data-ttu-id="262c3-121">The AzureStorageLinkedService1 links an Azure storage and AzureSqlLinkedService1 links an Azure SQL database to the data factory: **ADFTutorialDataFactoryVS**.</span><span class="sxs-lookup"><span data-stu-id="262c3-121">The AzureStorageLinkedService1 links an Azure storage and AzureSqlLinkedService1 links an Azure SQL database to the data factory: **ADFTutorialDataFactoryVS**.</span></span> <span data-ttu-id="262c3-122">The input data for the pipeline resides in a blob container in the Azure blob storage and output data is stored in a table in the Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="262c3-122">The input data for the pipeline resides in a blob container in the Azure blob storage and output data is stored in a table in the Azure SQL database.</span></span> <span data-ttu-id="262c3-123">Therefore, you add these two data stores as linked services to the data factory.</span><span class="sxs-lookup"><span data-stu-id="262c3-123">Therefore, you add these two data stores as linked services to the data factory.</span></span>
2. <span data-ttu-id="262c3-124">Create two datasets: **InputDataset** and **OutputDataset**, which represent the input/output data that is stored in the data stores.</span><span class="sxs-lookup"><span data-stu-id="262c3-124">Create two datasets: **InputDataset** and **OutputDataset**, which represent the input/output data that is stored in the data stores.</span></span> 
   
    <span data-ttu-id="262c3-125">For the InputDataset, you specify the blob container that contains a blob with the source data.</span><span class="sxs-lookup"><span data-stu-id="262c3-125">For the InputDataset, you specify the blob container that contains a blob with the source data.</span></span> <span data-ttu-id="262c3-126">For the OutputDataset, you specify the SQL table that stores the output data.</span><span class="sxs-lookup"><span data-stu-id="262c3-126">For the OutputDataset, you specify the SQL table that stores the output data.</span></span> <span data-ttu-id="262c3-127">You also specify other properties such as structure, availability, and policy.</span><span class="sxs-lookup"><span data-stu-id="262c3-127">You also specify other properties such as structure, availability, and policy.</span></span>
3. <span data-ttu-id="262c3-128">Create a pipeline named **ADFTutorialPipeline** in the ADFTutorialDataFactoryVS.</span><span class="sxs-lookup"><span data-stu-id="262c3-128">Create a pipeline named **ADFTutorialPipeline** in the ADFTutorialDataFactoryVS.</span></span> 
   
    <span data-ttu-id="262c3-129">The pipeline has a **Copy Activity** that copies input data from the Azure blob to the output Azure SQL table.</span><span class="sxs-lookup"><span data-stu-id="262c3-129">The pipeline has a **Copy Activity** that copies input data from the Azure blob to the output Azure SQL table.</span></span> <span data-ttu-id="262c3-130">The Copy Activity performs the data movement in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="262c3-130">The Copy Activity performs the data movement in Azure Data Factory.</span></span> <span data-ttu-id="262c3-131">The activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span><span class="sxs-lookup"><span data-stu-id="262c3-131">The activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="262c3-132">See [Data Movement Activities](data-factory-data-movement-activities.md) article for details about the Copy Activity.</span><span class="sxs-lookup"><span data-stu-id="262c3-132">See [Data Movement Activities](data-factory-data-movement-activities.md) article for details about the Copy Activity.</span></span> 
4. <span data-ttu-id="262c3-133">Create a data factory named **VSTutorialFactory**.</span><span class="sxs-lookup"><span data-stu-id="262c3-133">Create a data factory named **VSTutorialFactory**.</span></span> <span data-ttu-id="262c3-134">Deploy the data factory and all Data Factory entities (linked services, tables, and the pipeline).</span><span class="sxs-lookup"><span data-stu-id="262c3-134">Deploy the data factory and all Data Factory entities (linked services, tables, and the pipeline).</span></span>    

## <a name="prerequisites"></a><span data-ttu-id="262c3-135">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="262c3-135">Prerequisites</span></span>
1. <span data-ttu-id="262c3-136">Read through [Tutorial Overview](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) article and complete the **prerequisite** steps.</span><span class="sxs-lookup"><span data-stu-id="262c3-136">Read through [Tutorial Overview](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) article and complete the **prerequisite** steps.</span></span> 
2. <span data-ttu-id="262c3-137">You must be an **administrator of the Azure subscription** to be able to publish Data Factory entities to Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="262c3-137">You must be an **administrator of the Azure subscription** to be able to publish Data Factory entities to Azure Data Factory.</span></span>  
3. <span data-ttu-id="262c3-138">You must have the following installed on your computer:</span><span class="sxs-lookup"><span data-stu-id="262c3-138">You must have the following installed on your computer:</span></span> 
   * <span data-ttu-id="262c3-139">Visual Studio 2013 or Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="262c3-139">Visual Studio 2013 or Visual Studio 2015</span></span>
   * <span data-ttu-id="262c3-140">Download Azure SDK for Visual Studio 2013 or Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="262c3-140">Download Azure SDK for Visual Studio 2013 or Visual Studio 2015.</span></span> <span data-ttu-id="262c3-141">Navigate to [Azure Download Page](https://azure.microsoft.com/downloads/) and click **VS 2013** or **VS 2015** in the **.NET** section.</span><span class="sxs-lookup"><span data-stu-id="262c3-141">Navigate to [Azure Download Page](https://azure.microsoft.com/downloads/) and click **VS 2013** or **VS 2015** in the **.NET** section.</span></span>
   * <span data-ttu-id="262c3-142">Download the latest Azure Data Factory plugin for Visual Studio: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) or [VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005).</span><span class="sxs-lookup"><span data-stu-id="262c3-142">Download the latest Azure Data Factory plugin for Visual Studio: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) or [VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005).</span></span> <span data-ttu-id="262c3-143">You can also update the plugin by doing the following steps: On the menu, click **Tools** -> **Extensions and Updates** -> **Online** -> **Visual Studio Gallery** -> **Microsoft Azure Data Factory Tools for Visual Studio** -> **Update**.</span><span class="sxs-lookup"><span data-stu-id="262c3-143">You can also update the plugin by doing the following steps: On the menu, click **Tools** -> **Extensions and Updates** -> **Online** -> **Visual Studio Gallery** -> **Microsoft Azure Data Factory Tools for Visual Studio** -> **Update**.</span></span>

## <a name="create-visual-studio-project"></a><span data-ttu-id="262c3-144">Create Visual Studio project</span><span class="sxs-lookup"><span data-stu-id="262c3-144">Create Visual Studio project</span></span>
1. <span data-ttu-id="262c3-145">Launch **Visual Studio 2013**.</span><span class="sxs-lookup"><span data-stu-id="262c3-145">Launch **Visual Studio 2013**.</span></span> <span data-ttu-id="262c3-146">Click **File**, point to **New**, and click **Project**.</span><span class="sxs-lookup"><span data-stu-id="262c3-146">Click **File**, point to **New**, and click **Project**.</span></span> <span data-ttu-id="262c3-147">You should see the **New Project** dialog box.</span><span class="sxs-lookup"><span data-stu-id="262c3-147">You should see the **New Project** dialog box.</span></span>  
2. <span data-ttu-id="262c3-148">In the **New Project** dialog, select the **DataFactory** template, and click **Empty Data Factory Project**.</span><span class="sxs-lookup"><span data-stu-id="262c3-148">In the **New Project** dialog, select the **DataFactory** template, and click **Empty Data Factory Project**.</span></span> <span data-ttu-id="262c3-149">If you don't see the DataFactory template, close Visual Studio, install Azure SDK for Visual Studio 2013, and reopen Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="262c3-149">If you don't see the DataFactory template, close Visual Studio, install Azure SDK for Visual Studio 2013, and reopen Visual Studio.</span></span>  
   
    ![New project dialog box](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-activity-tutorial-using-visual-studio/new-project-dialog.png)
3. <span data-ttu-id="262c3-151">Enter a **name** for the project, **location**, and a name for the **solution**, and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="262c3-151">Enter a **name** for the project, **location**, and a name for the **solution**, and click **OK**.</span></span>
   
    ![Solution Explorer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-activity-tutorial-using-visual-studio/solution-explorer.png)    

## <a name="create-linked-services"></a><span data-ttu-id="262c3-153">Create linked services</span><span class="sxs-lookup"><span data-stu-id="262c3-153">Create linked services</span></span>
<span data-ttu-id="262c3-154">Linked services link data stores or compute services to an Azure data factory.</span><span class="sxs-lookup"><span data-stu-id="262c3-154">Linked services link data stores or compute services to an Azure data factory.</span></span> <span data-ttu-id="262c3-155">See [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) for all the sources and sinks supported by the Copy Activity.</span><span class="sxs-lookup"><span data-stu-id="262c3-155">See [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) for all the sources and sinks supported by the Copy Activity.</span></span> <span data-ttu-id="262c3-156">See [compute linked services](data-factory-compute-linked-services.md) for the list of compute services supported by Data Factory.</span><span class="sxs-lookup"><span data-stu-id="262c3-156">See [compute linked services](data-factory-compute-linked-services.md) for the list of compute services supported by Data Factory.</span></span> <span data-ttu-id="262c3-157">In this tutorial, you do not use any compute service.</span><span class="sxs-lookup"><span data-stu-id="262c3-157">In this tutorial, you do not use any compute service.</span></span> 

<span data-ttu-id="262c3-158">In this step, you create two linked services: **AzureStorageLinkedService1** and **AzureSqlLinkedService1**.</span><span class="sxs-lookup"><span data-stu-id="262c3-158">In this step, you create two linked services: **AzureStorageLinkedService1** and **AzureSqlLinkedService1**.</span></span> <span data-ttu-id="262c3-159">AzureStorageLinkedService1 linked service links an Azure Storage Account and AzureSqlLinkedService links an Azure SQL database to the data factory: **ADFTutorialDataFactory**.</span><span class="sxs-lookup"><span data-stu-id="262c3-159">AzureStorageLinkedService1 linked service links an Azure Storage Account and AzureSqlLinkedService links an Azure SQL database to the data factory: **ADFTutorialDataFactory**.</span></span> 

### <a name="create-the-azure-storage-linked-service"></a><span data-ttu-id="262c3-160">Create the Azure Storage linked service</span><span class="sxs-lookup"><span data-stu-id="262c3-160">Create the Azure Storage linked service</span></span>
1. <span data-ttu-id="262c3-161">Right-click **Linked Services** in the solution explorer, point to **Add**, and click **New Item**.</span><span class="sxs-lookup"><span data-stu-id="262c3-161">Right-click **Linked Services** in the solution explorer, point to **Add**, and click **New Item**.</span></span>      
2. <span data-ttu-id="262c3-162">In the **Add New Item** dialog box, select **Azure Storage Linked Service** from the list, and click **Add**.</span><span class="sxs-lookup"><span data-stu-id="262c3-162">In the **Add New Item** dialog box, select **Azure Storage Linked Service** from the list, and click **Add**.</span></span> 
   
    ![New Linked Service](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-activity-tutorial-using-visual-studio/new-linked-service-dialog.png)
3. <span data-ttu-id="262c3-164">Replace `<accountname>` and `<accountkey>`\* with the name of your Azure storage account and its key.</span><span class="sxs-lookup"><span data-stu-id="262c3-164">Replace `<accountname>` and `<accountkey>`\* with the name of your Azure storage account and its key.</span></span> 
   
    ![Azure Storage Linked Service](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-activity-tutorial-using-visual-studio/azure-storage-linked-service.png)
4. <span data-ttu-id="262c3-166">Save the **AzureStorageLinkedService1.json** file.</span><span class="sxs-lookup"><span data-stu-id="262c3-166">Save the **AzureStorageLinkedService1.json** file.</span></span>

> See [Move data from/to Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties.
> 
> 

### <a name="create-the-azure-sql-linked-service"></a><span data-ttu-id="262c3-168">Create the Azure SQL linked service</span><span class="sxs-lookup"><span data-stu-id="262c3-168">Create the Azure SQL linked service</span></span>
1. <span data-ttu-id="262c3-169">Right-click on **Linked Services** node in the **Solution Explorer** again, point to **Add**, and click **New Item**.</span><span class="sxs-lookup"><span data-stu-id="262c3-169">Right-click on **Linked Services** node in the **Solution Explorer** again, point to **Add**, and click **New Item**.</span></span> 
2. <span data-ttu-id="262c3-170">This time, select **Azure SQL Linked Service**, and click **Add**.</span><span class="sxs-lookup"><span data-stu-id="262c3-170">This time, select **Azure SQL Linked Service**, and click **Add**.</span></span> 
3. <span data-ttu-id="262c3-171">In the **AzureSqlLinkedService1.json file**, replace `<servername>`, `<databasename>`, `<username@servername>`, and `<password>` with names of your Azure SQL server, database, user account, and password.</span><span class="sxs-lookup"><span data-stu-id="262c3-171">In the **AzureSqlLinkedService1.json file**, replace `<servername>`, `<databasename>`, `<username@servername>`, and `<password>` with names of your Azure SQL server, database, user account, and password.</span></span>    
4. <span data-ttu-id="262c3-172">Save the **AzureSqlLinkedService1.json** file.</span><span class="sxs-lookup"><span data-stu-id="262c3-172">Save the **AzureSqlLinkedService1.json** file.</span></span> 

> [!NOTE]
> See [Move data from/to Azure SQL Database](data-factory-azure-sql-connector.md#linked-service-properties) for details about JSON properties.
> 
> 

## <a name="create-datasets"></a><span data-ttu-id="262c3-174">Create datasets</span><span class="sxs-lookup"><span data-stu-id="262c3-174">Create datasets</span></span>
<span data-ttu-id="262c3-175">In the previous step, you created linked services **AzureStorageLinkedService1** and **AzureSqlLinkedService1** to link an Azure Storage account and Azure SQL database to the data factory: **ADFTutorialDataFactory**.</span><span class="sxs-lookup"><span data-stu-id="262c3-175">In the previous step, you created linked services **AzureStorageLinkedService1** and **AzureSqlLinkedService1** to link an Azure Storage account and Azure SQL database to the data factory: **ADFTutorialDataFactory**.</span></span> <span data-ttu-id="262c3-176">In this step, you define two datasets -- **InputDataset** and **OutputDataset** -- that represent the input/output data that is stored in the data stores referred by AzureStorageLinkedService1 and AzureSqlLinkedService1 respectively.</span><span class="sxs-lookup"><span data-stu-id="262c3-176">In this step, you define two datasets -- **InputDataset** and **OutputDataset** -- that represent the input/output data that is stored in the data stores referred by AzureStorageLinkedService1 and AzureSqlLinkedService1 respectively.</span></span> <span data-ttu-id="262c3-177">For InputDataset, you specify the blob container that contains a blob with the source data.</span><span class="sxs-lookup"><span data-stu-id="262c3-177">For InputDataset, you specify the blob container that contains a blob with the source data.</span></span> <span data-ttu-id="262c3-178">For OutputDataset, you specify the SQL table that stores the output data.</span><span class="sxs-lookup"><span data-stu-id="262c3-178">For OutputDataset, you specify the SQL table that stores the output data.</span></span>

### <a name="create-input-dataset"></a><span data-ttu-id="262c3-179">Create input dataset</span><span class="sxs-lookup"><span data-stu-id="262c3-179">Create input dataset</span></span>
<span data-ttu-id="262c3-180">In this step, you create a dataset named **InputDataset** that points to a blob container in the Azure Storage represented by the **AzureStorageLinkedService1** linked service.</span><span class="sxs-lookup"><span data-stu-id="262c3-180">In this step, you create a dataset named **InputDataset** that points to a blob container in the Azure Storage represented by the **AzureStorageLinkedService1** linked service.</span></span> <span data-ttu-id="262c3-181">A table is a rectangular dataset and is the only type of dataset supported right now.</span><span class="sxs-lookup"><span data-stu-id="262c3-181">A table is a rectangular dataset and is the only type of dataset supported right now.</span></span> 

1. <span data-ttu-id="262c3-182">Right-click **Tables** in the **Solution Explorer**, point to **Add**, and click **New Item**.</span><span class="sxs-lookup"><span data-stu-id="262c3-182">Right-click **Tables** in the **Solution Explorer**, point to **Add**, and click **New Item**.</span></span>
2. <span data-ttu-id="262c3-183">In the **Add New Item** dialog box, select **Azure Blob**, and click **Add**.</span><span class="sxs-lookup"><span data-stu-id="262c3-183">In the **Add New Item** dialog box, select **Azure Blob**, and click **Add**.</span></span>   
3. <span data-ttu-id="262c3-184">Replace the JSON text with the following text and save the **AzureBlobLocation1.json** file.</span><span class="sxs-lookup"><span data-stu-id="262c3-184">Replace the JSON text with the following text and save the **AzureBlobLocation1.json** file.</span></span> 

  ```json   
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
      "linkedServiceName": "AzureStorageLinkedService1",
      "typeProperties": {
        "folderPath": "adftutorial/",
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
    <span data-ttu-id="262c3-185">Note the following points:</span><span class="sxs-lookup"><span data-stu-id="262c3-185">Note the following points:</span></span> 
   
   * <span data-ttu-id="262c3-186">dataset **type** is set to **AzureBlob**.</span><span class="sxs-lookup"><span data-stu-id="262c3-186">dataset **type** is set to **AzureBlob**.</span></span>
   * <span data-ttu-id="262c3-187">**linkedServiceName** is set to **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="262c3-187">**linkedServiceName** is set to **AzureStorageLinkedService**.</span></span> <span data-ttu-id="262c3-188">You created this linked service in Step 2.</span><span class="sxs-lookup"><span data-stu-id="262c3-188">You created this linked service in Step 2.</span></span>
   * <span data-ttu-id="262c3-189">**folderPath** is set to the **adftutorial** container.</span><span class="sxs-lookup"><span data-stu-id="262c3-189">**folderPath** is set to the **adftutorial** container.</span></span> <span data-ttu-id="262c3-190">You can also specify the name of a blob within the folder using the **fileName** property.</span><span class="sxs-lookup"><span data-stu-id="262c3-190">You can also specify the name of a blob within the folder using the **fileName** property.</span></span> <span data-ttu-id="262c3-191">Since you are not specifying the name of the blob, data from all blobs in the container is considered as an input data.</span><span class="sxs-lookup"><span data-stu-id="262c3-191">Since you are not specifying the name of the blob, data from all blobs in the container is considered as an input data.</span></span>  
   * <span data-ttu-id="262c3-192">format **type** is set to **TextFormat**</span><span class="sxs-lookup"><span data-stu-id="262c3-192">format **type** is set to **TextFormat**</span></span>
   * <span data-ttu-id="262c3-193">There are two fields in the text file – **FirstName** and **LastName** – separated by a comma character (columnDelimiter)</span><span class="sxs-lookup"><span data-stu-id="262c3-193">There are two fields in the text file – **FirstName** and **LastName** – separated by a comma character (columnDelimiter)</span></span>    
   * <span data-ttu-id="262c3-194">The **availability** is set to **hourly** (frequency is set to hour and interval is set to 1).</span><span class="sxs-lookup"><span data-stu-id="262c3-194">The **availability** is set to **hourly** (frequency is set to hour and interval is set to 1).</span></span> <span data-ttu-id="262c3-195">Therefore, Data Factory looks for input data every hour in the root folder of blob container (adftutorial) you specified.</span><span class="sxs-lookup"><span data-stu-id="262c3-195">Therefore, Data Factory looks for input data every hour in the root folder of blob container (adftutorial) you specified.</span></span> 
   
   <span data-ttu-id="262c3-196">if you don't specify a **fileName** for an **input** dataset, all files/blobs from the input folder (folderPath) are considered as inputs.</span><span class="sxs-lookup"><span data-stu-id="262c3-196">if you don't specify a **fileName** for an **input** dataset, all files/blobs from the input folder (folderPath) are considered as inputs.</span></span> <span data-ttu-id="262c3-197">If you specify a fileName in the JSON, only the specified file/blob is considered asn input.</span><span class="sxs-lookup"><span data-stu-id="262c3-197">If you specify a fileName in the JSON, only the specified file/blob is considered asn input.</span></span>
   
   <span data-ttu-id="262c3-198">If you do not specify a **fileName** for an **output table**, the generated files in the **folderPath** are named in the following format: Data.&lt;Guid&gt;.txt (example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.).</span><span class="sxs-lookup"><span data-stu-id="262c3-198">If you do not specify a **fileName** for an **output table**, the generated files in the **folderPath** are named in the following format: Data.&lt;Guid&gt;.txt (example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.).</span></span>
   
   <span data-ttu-id="262c3-199">To set **folderPath** and **fileName** dynamically based on the **SliceStart** time, use the **partitionedBy** property.</span><span class="sxs-lookup"><span data-stu-id="262c3-199">To set **folderPath** and **fileName** dynamically based on the **SliceStart** time, use the **partitionedBy** property.</span></span> <span data-ttu-id="262c3-200">In the following example, folderPath uses Year, Month, and Day from the SliceStart (start time of the slice being processed) and fileName uses Hour from the SliceStart.</span><span class="sxs-lookup"><span data-stu-id="262c3-200">In the following example, folderPath uses Year, Month, and Day from the SliceStart (start time of the slice being processed) and fileName uses Hour from the SliceStart.</span></span> <span data-ttu-id="262c3-201">For example, if a slice is being produced for 2016-09-20T08:00:00, the folderName is set to wikidatagateway/wikisampledataout/2016/09/20 and the fileName is set to 08.csv.</span><span class="sxs-lookup"><span data-stu-id="262c3-201">For example, if a slice is being produced for 2016-09-20T08:00:00, the folderName is set to wikidatagateway/wikisampledataout/2016/09/20 and the fileName is set to 08.csv.</span></span> 
  
    ```json   
    "folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
    "fileName": "{Hour}.csv",
    "partitionedBy": 
    [
        { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
        { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } }, 
        { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } }, 
        { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } } 
    ```
            
> [!NOTE]
> See [Move data from/to Azure Blob](data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties.
> 
> 

### <a name="create-output-dataset"></a><span data-ttu-id="262c3-203">Create output dataset</span><span class="sxs-lookup"><span data-stu-id="262c3-203">Create output dataset</span></span>
<span data-ttu-id="262c3-204">In this step, you create an output dataset named **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="262c3-204">In this step, you create an output dataset named **OutputDataset**.</span></span> <span data-ttu-id="262c3-205">This dataset points to a SQL table in the Azure SQL database represented by **AzureSqlLinkedService1**.</span><span class="sxs-lookup"><span data-stu-id="262c3-205">This dataset points to a SQL table in the Azure SQL database represented by **AzureSqlLinkedService1**.</span></span> 

1. <span data-ttu-id="262c3-206">Right-click **Tables** in the **Solution Explorer** again, point to **Add**, and click **New Item**.</span><span class="sxs-lookup"><span data-stu-id="262c3-206">Right-click **Tables** in the **Solution Explorer** again, point to **Add**, and click **New Item**.</span></span>
2. <span data-ttu-id="262c3-207">In the **Add New Item** dialog box, select **Azure SQL**, and click **Add**.</span><span class="sxs-lookup"><span data-stu-id="262c3-207">In the **Add New Item** dialog box, select **Azure SQL**, and click **Add**.</span></span> 
3. <span data-ttu-id="262c3-208">Replace the JSON text with the following JSON and save the **AzureSqlTableLocation1.json** file.</span><span class="sxs-lookup"><span data-stu-id="262c3-208">Replace the JSON text with the following JSON and save the **AzureSqlTableLocation1.json** file.</span></span>

  ```json
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
       "linkedServiceName": "AzureSqlLinkedService1",
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
   
    <span data-ttu-id="262c3-209">Note the following points:</span><span class="sxs-lookup"><span data-stu-id="262c3-209">Note the following points:</span></span> 
   
   * <span data-ttu-id="262c3-210">dataset **type** is set to **AzureSQLTable**.</span><span class="sxs-lookup"><span data-stu-id="262c3-210">dataset **type** is set to **AzureSQLTable**.</span></span>
   * <span data-ttu-id="262c3-211">**linkedServiceName** is set to **AzureSqlLinkedService** (you created this linked service in Step 2).</span><span class="sxs-lookup"><span data-stu-id="262c3-211">**linkedServiceName** is set to **AzureSqlLinkedService** (you created this linked service in Step 2).</span></span>
   * <span data-ttu-id="262c3-212">**tablename** is set to **emp**.</span><span class="sxs-lookup"><span data-stu-id="262c3-212">**tablename** is set to **emp**.</span></span>
   * <span data-ttu-id="262c3-213">There are three columns – **ID**, **FirstName**, and **LastName** – in the emp table in the database.</span><span class="sxs-lookup"><span data-stu-id="262c3-213">There are three columns – **ID**, **FirstName**, and **LastName** – in the emp table in the database.</span></span> <span data-ttu-id="262c3-214">ID is an identity column, so you need to specify only **FirstName** and **LastName** here.</span><span class="sxs-lookup"><span data-stu-id="262c3-214">ID is an identity column, so you need to specify only **FirstName** and **LastName** here.</span></span>
   * <span data-ttu-id="262c3-215">The **availability** is set to **hourly** (frequency set to hour and interval set to 1).</span><span class="sxs-lookup"><span data-stu-id="262c3-215">The **availability** is set to **hourly** (frequency set to hour and interval set to 1).</span></span>  <span data-ttu-id="262c3-216">The Data Factory service generates an output data slice every hour in the **emp** table in the Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="262c3-216">The Data Factory service generates an output data slice every hour in the **emp** table in the Azure SQL database.</span></span>

> [!NOTE]
> See [Move data from/to Azure SQL Database](data-factory-azure-sql-connector.md#linked-service-properties) for details about JSON properties.
> 
> 

## <a name="create-pipeline"></a><span data-ttu-id="262c3-218">Create pipeline</span><span class="sxs-lookup"><span data-stu-id="262c3-218">Create pipeline</span></span>
<span data-ttu-id="262c3-219">You have created input/output linked services and tables so far.</span><span class="sxs-lookup"><span data-stu-id="262c3-219">You have created input/output linked services and tables so far.</span></span> <span data-ttu-id="262c3-220">Now, you create a pipeline with a **Copy Activity** to copy data from the Azure blob to Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="262c3-220">Now, you create a pipeline with a **Copy Activity** to copy data from the Azure blob to Azure SQL database.</span></span> 

1. <span data-ttu-id="262c3-221">Right-click **Pipelines** in the **Solution Explorer**, point to **Add**, and click **New Item**.</span><span class="sxs-lookup"><span data-stu-id="262c3-221">Right-click **Pipelines** in the **Solution Explorer**, point to **Add**, and click **New Item**.</span></span>  
2. <span data-ttu-id="262c3-222">Select **Copy Data Pipeline** in the **Add New Item** dialog box and click **Add**.</span><span class="sxs-lookup"><span data-stu-id="262c3-222">Select **Copy Data Pipeline** in the **Add New Item** dialog box and click **Add**.</span></span> 
3. <span data-ttu-id="262c3-223">Replace the JSON with the following JSON and save the **CopyActivity1.json** file.</span><span class="sxs-lookup"><span data-stu-id="262c3-223">Replace the JSON with the following JSON and save the **CopyActivity1.json** file.</span></span>

  ```json   
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
             "style": "StartOfInterval",
             "retry": 0,
             "timeout": "01:00:00"
           }
         }
       ],
       "start": "2015-07-12T00:00:00Z",
       "end": "2015-07-13T00:00:00Z",
       "isPaused": false
     }
    }
    ```   
   <span data-ttu-id="262c3-224">Note the following points:</span><span class="sxs-lookup"><span data-stu-id="262c3-224">Note the following points:</span></span>
   
   * <span data-ttu-id="262c3-225">In the activities section, there is only one activity whose **type** is set to **Copy**.</span><span class="sxs-lookup"><span data-stu-id="262c3-225">In the activities section, there is only one activity whose **type** is set to **Copy**.</span></span>
   * <span data-ttu-id="262c3-226">Input for the activity is set to **InputDataset** and output for the activity is set to **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="262c3-226">Input for the activity is set to **InputDataset** and output for the activity is set to **OutputDataset**.</span></span>
   * <span data-ttu-id="262c3-227">In the **typeProperties** section, **BlobSource** is specified as the source type and **SqlSink** is specified as the sink type.</span><span class="sxs-lookup"><span data-stu-id="262c3-227">In the **typeProperties** section, **BlobSource** is specified as the source type and **SqlSink** is specified as the sink type.</span></span>
   
   <span data-ttu-id="262c3-228">Replace the value of the **start** property with the current day and **end** value with the next day.</span><span class="sxs-lookup"><span data-stu-id="262c3-228">Replace the value of the **start** property with the current day and **end** value with the next day.</span></span> <span data-ttu-id="262c3-229">You can specify only the date part and skip the time part of the date time.</span><span class="sxs-lookup"><span data-stu-id="262c3-229">You can specify only the date part and skip the time part of the date time.</span></span> <span data-ttu-id="262c3-230">For example, "2016-02-03", which is equivalent to "2016-02-03T00:00:00Z"</span><span class="sxs-lookup"><span data-stu-id="262c3-230">For example, "2016-02-03", which is equivalent to "2016-02-03T00:00:00Z"</span></span>
   
   <span data-ttu-id="262c3-231">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="262c3-231">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="262c3-232">For example: 2016-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="262c3-232">For example: 2016-10-14T16:32:41Z.</span></span> <span data-ttu-id="262c3-233">The **end** time is optional, but we use it in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="262c3-233">The **end** time is optional, but we use it in this tutorial.</span></span> 
   
   <span data-ttu-id="262c3-234">If you do not specify value for the **end** property, it is calculated as **start + 48 hours**.</span><span class="sxs-lookup"><span data-stu-id="262c3-234">If you do not specify value for the **end** property, it is calculated as **start + 48 hours**.</span></span> <span data-ttu-id="262c3-235">To run the pipeline indefinitely, specify **9999-09-09** as the value for the **end** property.</span><span class="sxs-lookup"><span data-stu-id="262c3-235">To run the pipeline indefinitely, specify **9999-09-09** as the value for the **end** property.</span></span>
   
   <span data-ttu-id="262c3-236">In the preceding example, there are 24 data slices as each data slice is produced hourly.</span><span class="sxs-lookup"><span data-stu-id="262c3-236">In the preceding example, there are 24 data slices as each data slice is produced hourly.</span></span>

## <a name="publishdeploy-data-factory-entities"></a><span data-ttu-id="262c3-237">Publish/deploy Data Factory entities</span><span class="sxs-lookup"><span data-stu-id="262c3-237">Publish/deploy Data Factory entities</span></span>
<span data-ttu-id="262c3-238">In this step, you publish Data Factory entities (linked services, datasets, and pipeline) you created earlier.</span><span class="sxs-lookup"><span data-stu-id="262c3-238">In this step, you publish Data Factory entities (linked services, datasets, and pipeline) you created earlier.</span></span> <span data-ttu-id="262c3-239">You also specify the name of the new data factory to be created to hold these entities.</span><span class="sxs-lookup"><span data-stu-id="262c3-239">You also specify the name of the new data factory to be created to hold these entities.</span></span>  

1. <span data-ttu-id="262c3-240">Right-click project in the Solution Explorer, and click **Publish**.</span><span class="sxs-lookup"><span data-stu-id="262c3-240">Right-click project in the Solution Explorer, and click **Publish**.</span></span> 
2. <span data-ttu-id="262c3-241">If you see **Sign in to your Microsoft account** dialog box, enter your credentials for the account that has Azure subscription, and click **sign in**.</span><span class="sxs-lookup"><span data-stu-id="262c3-241">If you see **Sign in to your Microsoft account** dialog box, enter your credentials for the account that has Azure subscription, and click **sign in**.</span></span>
3. <span data-ttu-id="262c3-242">You should see the following dialog box:</span><span class="sxs-lookup"><span data-stu-id="262c3-242">You should see the following dialog box:</span></span>
   
   ![Publish dialog box](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-activity-tutorial-using-visual-studio/publish.png)
4. <span data-ttu-id="262c3-244">In the Configure data factory page, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="262c3-244">In the Configure data factory page, do the following steps:</span></span> 
   
   1. <span data-ttu-id="262c3-245">select **Create New Data Factory** option.</span><span class="sxs-lookup"><span data-stu-id="262c3-245">select **Create New Data Factory** option.</span></span>
   2. <span data-ttu-id="262c3-246">Enter **VSTutorialFactory** for **Name**.</span><span class="sxs-lookup"><span data-stu-id="262c3-246">Enter **VSTutorialFactory** for **Name**.</span></span>  
      
      > [!IMPORTANT]
      > The name of the Azure data factory must be globally unique. If you receive an error about the name of data factory when publishing, change the name of the data factory (for example, yournameVSTutorialFactory) and try publishing again. See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.        
      > 
      > 
   3. <span data-ttu-id="262c3-250">Select your Azure subscription for the **Subscription** field.</span><span class="sxs-lookup"><span data-stu-id="262c3-250">Select your Azure subscription for the **Subscription** field.</span></span>
      
      > [!IMPORTANT]
      > If you do not see any subscription, ensure that you logged in using an account that is an admin or co-admin of the subscription.  
      > 
      > 
   4. <span data-ttu-id="262c3-252">Select the **resource group** for the data factory to be created.</span><span class="sxs-lookup"><span data-stu-id="262c3-252">Select the **resource group** for the data factory to be created.</span></span> 
   5. <span data-ttu-id="262c3-253">Select the **region** for the data factory.</span><span class="sxs-lookup"><span data-stu-id="262c3-253">Select the **region** for the data factory.</span></span> <span data-ttu-id="262c3-254">Only regions supported by the Data Factory service are shown in the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="262c3-254">Only regions supported by the Data Factory service are shown in the drop-down list.</span></span>
   6. <span data-ttu-id="262c3-255">Click **Next** to switch to the **Publish Items** page.</span><span class="sxs-lookup"><span data-stu-id="262c3-255">Click **Next** to switch to the **Publish Items** page.</span></span>
      
       ![Configure data factory page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-activity-tutorial-using-visual-studio/configure-data-factory-page.png)   
5. <span data-ttu-id="262c3-257">In the **Publish Items** page, ensure that all the Data Factories entities are selected, and click **Next** to switch to the **Summary** page.</span><span class="sxs-lookup"><span data-stu-id="262c3-257">In the **Publish Items** page, ensure that all the Data Factories entities are selected, and click **Next** to switch to the **Summary** page.</span></span>
   
   ![Publish items page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-activity-tutorial-using-visual-studio/publish-items-page.png)     
6. <span data-ttu-id="262c3-259">Review the summary and click **Next** to start the deployment process and view the **Deployment Status**.</span><span class="sxs-lookup"><span data-stu-id="262c3-259">Review the summary and click **Next** to start the deployment process and view the **Deployment Status**.</span></span>
   
   ![Publish summary page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-activity-tutorial-using-visual-studio/publish-summary-page.png)
7. <span data-ttu-id="262c3-261">In the **Deployment Status** page, you should see the status of the deployment process.</span><span class="sxs-lookup"><span data-stu-id="262c3-261">In the **Deployment Status** page, you should see the status of the deployment process.</span></span> <span data-ttu-id="262c3-262">Click Finish after the deployment is done.</span><span class="sxs-lookup"><span data-stu-id="262c3-262">Click Finish after the deployment is done.</span></span>
 
   ![Deployment status page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-activity-tutorial-using-visual-studio/deployment-status.png)

<span data-ttu-id="262c3-264">Note the following points:</span><span class="sxs-lookup"><span data-stu-id="262c3-264">Note the following points:</span></span> 

* <span data-ttu-id="262c3-265">If you receive the error: "This subscription is not registered to use namespace Microsoft.DataFactory", do one of the following and try publishing again:</span><span class="sxs-lookup"><span data-stu-id="262c3-265">If you receive the error: "This subscription is not registered to use namespace Microsoft.DataFactory", do one of the following and try publishing again:</span></span> 
  
  * <span data-ttu-id="262c3-266">In Azure PowerShell, run the following command to register the Data Factory provider.</span><span class="sxs-lookup"><span data-stu-id="262c3-266">In Azure PowerShell, run the following command to register the Data Factory provider.</span></span> 

    ```PowerShell    
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```
    <span data-ttu-id="262c3-267">You can run the following command to confirm that the Data Factory provider is registered.</span><span class="sxs-lookup"><span data-stu-id="262c3-267">You can run the following command to confirm that the Data Factory provider is registered.</span></span> 
    
    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="262c3-268">Login using the Azure subscription into the [Azure portal](https://portal.azure.com) and navigate to a Data Factory blade (or) create a data factory in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="262c3-268">Login using the Azure subscription into the [Azure portal](https://portal.azure.com) and navigate to a Data Factory blade (or) create a data factory in the Azure portal.</span></span> <span data-ttu-id="262c3-269">This action automatically registers the provider for you.</span><span class="sxs-lookup"><span data-stu-id="262c3-269">This action automatically registers the provider for you.</span></span>
* <span data-ttu-id="262c3-270">The name of the data factory may be registered as a DNS name in the future and hence become publically visible.</span><span class="sxs-lookup"><span data-stu-id="262c3-270">The name of the data factory may be registered as a DNS name in the future and hence become publically visible.</span></span>

> [!IMPORTANT]
> To create Data Factory instances, you need to be a admin/co-admin of the Azure subscription
> 
> 

## <a name="summary"></a><span data-ttu-id="262c3-272">Summary</span><span class="sxs-lookup"><span data-stu-id="262c3-272">Summary</span></span>
<span data-ttu-id="262c3-273">In this tutorial, you created an Azure data factory to copy data from an Azure blob to an Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="262c3-273">In this tutorial, you created an Azure data factory to copy data from an Azure blob to an Azure SQL database.</span></span> <span data-ttu-id="262c3-274">You used Visual Studio to create the data factory, linked services, datasets, and a pipeline.</span><span class="sxs-lookup"><span data-stu-id="262c3-274">You used Visual Studio to create the data factory, linked services, datasets, and a pipeline.</span></span> <span data-ttu-id="262c3-275">Here are the high-level steps you performed in this tutorial:</span><span class="sxs-lookup"><span data-stu-id="262c3-275">Here are the high-level steps you performed in this tutorial:</span></span>  

1. <span data-ttu-id="262c3-276">Created an Azure **data factory**.</span><span class="sxs-lookup"><span data-stu-id="262c3-276">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="262c3-277">Created **linked services**:</span><span class="sxs-lookup"><span data-stu-id="262c3-277">Created **linked services**:</span></span>
   1. <span data-ttu-id="262c3-278">An **Azure Storage** linked service to link your Azure Storage account that holds input data.</span><span class="sxs-lookup"><span data-stu-id="262c3-278">An **Azure Storage** linked service to link your Azure Storage account that holds input data.</span></span>     
   2. <span data-ttu-id="262c3-279">An **Azure SQL** linked service to link your Azure SQL database that holds the output data.</span><span class="sxs-lookup"><span data-stu-id="262c3-279">An **Azure SQL** linked service to link your Azure SQL database that holds the output data.</span></span> 
3. <span data-ttu-id="262c3-280">Created **datasets**, which describe input data and output data for pipelines.</span><span class="sxs-lookup"><span data-stu-id="262c3-280">Created **datasets**, which describe input data and output data for pipelines.</span></span>
4. <span data-ttu-id="262c3-281">Created a **pipeline** with a **Copy Activity** with **BlobSource** as source and **SqlSink** as sink.</span><span class="sxs-lookup"><span data-stu-id="262c3-281">Created a **pipeline** with a **Copy Activity** with **BlobSource** as source and **SqlSink** as sink.</span></span> 

## <a name="use-server-explorer-to-view-data-factories"></a><span data-ttu-id="262c3-282">Use Server Explorer to view data factories</span><span class="sxs-lookup"><span data-stu-id="262c3-282">Use Server Explorer to view data factories</span></span>
1. <span data-ttu-id="262c3-283">In **Visual Studio**, click **View** on the menu, and click **Server Explorer**.</span><span class="sxs-lookup"><span data-stu-id="262c3-283">In **Visual Studio**, click **View** on the menu, and click **Server Explorer**.</span></span>
2. <span data-ttu-id="262c3-284">In the Server Explorer window, expand **Azure** and expand **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="262c3-284">In the Server Explorer window, expand **Azure** and expand **Data Factory**.</span></span> <span data-ttu-id="262c3-285">If you see **Sign in to Visual Studio**, enter the **account** associated with your Azure subscription and click **Continue**.</span><span class="sxs-lookup"><span data-stu-id="262c3-285">If you see **Sign in to Visual Studio**, enter the **account** associated with your Azure subscription and click **Continue**.</span></span> <span data-ttu-id="262c3-286">Enter **password**, and click **Sign in**.</span><span class="sxs-lookup"><span data-stu-id="262c3-286">Enter **password**, and click **Sign in**.</span></span> <span data-ttu-id="262c3-287">Visual Studio tries to get information about all Azure data factories in your subscription.</span><span class="sxs-lookup"><span data-stu-id="262c3-287">Visual Studio tries to get information about all Azure data factories in your subscription.</span></span> <span data-ttu-id="262c3-288">You see the status of this operation in the **Data Factory Task List** window.</span><span class="sxs-lookup"><span data-stu-id="262c3-288">You see the status of this operation in the **Data Factory Task List** window.</span></span>

    ![Server Explorer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-activity-tutorial-using-visual-studio/server-explorer.png)
3. <span data-ttu-id="262c3-290">You can right-click on a data factory, and select Export Data Factory to New Project to create a Visual Studio project based on an existing data factory.</span><span class="sxs-lookup"><span data-stu-id="262c3-290">You can right-click on a data factory, and select Export Data Factory to New Project to create a Visual Studio project based on an existing data factory.</span></span>

    ![Export data factory to a VS project](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-activity-tutorial-using-visual-studio/export-data-factory-menu.png)  

## <a name="update-data-factory-tools-for-visual-studio"></a><span data-ttu-id="262c3-292">Update Data Factory tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="262c3-292">Update Data Factory tools for Visual Studio</span></span>
<span data-ttu-id="262c3-293">To update Azure Data Factory tools for Visual Studio, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="262c3-293">To update Azure Data Factory tools for Visual Studio, do the following steps:</span></span>

1. <span data-ttu-id="262c3-294">Click **Tools** on the menu and select **Extensions and Updates**.</span><span class="sxs-lookup"><span data-stu-id="262c3-294">Click **Tools** on the menu and select **Extensions and Updates**.</span></span> 
2. <span data-ttu-id="262c3-295">Select **Updates** in the left pane and then select **Visual Studio Gallery**.</span><span class="sxs-lookup"><span data-stu-id="262c3-295">Select **Updates** in the left pane and then select **Visual Studio Gallery**.</span></span>
3. <span data-ttu-id="262c3-296">Select **Azure Data Factory tools for Visual Studio** and click **Update**.</span><span class="sxs-lookup"><span data-stu-id="262c3-296">Select **Azure Data Factory tools for Visual Studio** and click **Update**.</span></span> <span data-ttu-id="262c3-297">If you do not see this entry, you already have the latest version of the tools.</span><span class="sxs-lookup"><span data-stu-id="262c3-297">If you do not see this entry, you already have the latest version of the tools.</span></span> 

<span data-ttu-id="262c3-298">See [Monitor datasets and pipeline](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline) for instructions on how to use the Azure portal to monitor the pipeline and datasets you have created in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="262c3-298">See [Monitor datasets and pipeline](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline) for instructions on how to use the Azure portal to monitor the pipeline and datasets you have created in this tutorial.</span></span>

## <a name="see-also"></a><span data-ttu-id="262c3-299">See Also</span><span class="sxs-lookup"><span data-stu-id="262c3-299">See Also</span></span>
| <span data-ttu-id="262c3-300">Topic</span><span class="sxs-lookup"><span data-stu-id="262c3-300">Topic</span></span> | <span data-ttu-id="262c3-301">Description</span><span class="sxs-lookup"><span data-stu-id="262c3-301">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="262c3-302">Pipelines</span><span class="sxs-lookup"><span data-stu-id="262c3-302">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="262c3-303">This article helps you understand pipelines and activities in Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="262c3-303">This article helps you understand pipelines and activities in Azure Data Factory</span></span> |
| [<span data-ttu-id="262c3-304">Datasets</span><span class="sxs-lookup"><span data-stu-id="262c3-304">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="262c3-305">This article helps you understand datasets in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="262c3-305">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="262c3-306">Scheduling and execution</span><span class="sxs-lookup"><span data-stu-id="262c3-306">Scheduling and execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="262c3-307">This article explains the scheduling and execution aspects of Azure Data Factory application model.</span><span class="sxs-lookup"><span data-stu-id="262c3-307">This article explains the scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="262c3-308">Monitor and manage pipelines using Monitoring App</span><span class="sxs-lookup"><span data-stu-id="262c3-308">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="262c3-309">This article describes how to monitor, manage, and debug pipelines using the Monitoring & Management App.</span><span class="sxs-lookup"><span data-stu-id="262c3-309">This article describes how to monitor, manage, and debug pipelines using the Monitoring & Management App.</span></span> |












