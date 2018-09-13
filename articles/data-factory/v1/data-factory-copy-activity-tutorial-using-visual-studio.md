---
title: 'Tutorial: Create a pipeline with Copy Activity using Visual Studio | Microsoft Docs'
description: In this tutorial, you create an Azure Data Factory pipeline with a Copy Activity by using Visual Studio.
services: data-factory
documentationcenter: ''
author: linda33wj
manager: craigg
ms.assetid: 1751185b-ce0a-4ab2-a9c3-e37b4d149ca3
ms.service: data-factory
ms.workload: data-services
ms.custom: vs-azure
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 01/22/2018
ms.author: jingwang
robots: noindex
ms.openlocfilehash: 1152074f6dd45d9169f507aedf01541332d6f8f2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864877"
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-visual-studio"></a><span data-ttu-id="2772e-103">Tutorial: Create a pipeline with Copy Activity using Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2772e-103">Tutorial: Create a pipeline with Copy Activity using Visual Studio</span></span>
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

> [!NOTE]
> This article applies to version 1 of Data Factory. If you are using the current version of the Data Factory service, see [copy activity tutorial](../quickstart-create-data-factory-dot-net.md). 

<span data-ttu-id="2772e-114">In this article, you learn how to use the Microsoft Visual Studio to create a data factory with a pipeline that copies data from an Azure blob storage to an Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="2772e-114">In this article, you learn how to use the Microsoft Visual Studio to create a data factory with a pipeline that copies data from an Azure blob storage to an Azure SQL database.</span></span> <span data-ttu-id="2772e-115">If you are new to Azure Data Factory, read through the [Introduction to Azure Data Factory](data-factory-introduction.md) article before doing this tutorial.</span><span class="sxs-lookup"><span data-stu-id="2772e-115">If you are new to Azure Data Factory, read through the [Introduction to Azure Data Factory](data-factory-introduction.md) article before doing this tutorial.</span></span>   

<span data-ttu-id="2772e-116">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span><span class="sxs-lookup"><span data-stu-id="2772e-116">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="2772e-117">The copy activity copies data from a supported data store to a supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="2772e-117">The copy activity copies data from a supported data store to a supported sink data store.</span></span> <span data-ttu-id="2772e-118">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="2772e-118">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="2772e-119">The activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span><span class="sxs-lookup"><span data-stu-id="2772e-119">The activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="2772e-120">For more information about the Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="2772e-120">For more information about the Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="2772e-121">A pipeline can have more than one activity.</span><span class="sxs-lookup"><span data-stu-id="2772e-121">A pipeline can have more than one activity.</span></span> <span data-ttu-id="2772e-122">And, you can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span><span class="sxs-lookup"><span data-stu-id="2772e-122">And, you can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="2772e-123">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="2772e-123">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>

> [!NOTE] 
> The data pipeline in this tutorial copies data from a source data store to a destination data store. For a tutorial on how to transform data using Azure Data Factory, see [Tutorial: Build a pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).

## <a name="prerequisites"></a><span data-ttu-id="2772e-126">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="2772e-126">Prerequisites</span></span>
1. <span data-ttu-id="2772e-127">Read through [Tutorial Overview](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) article and complete the **prerequisite** steps.</span><span class="sxs-lookup"><span data-stu-id="2772e-127">Read through [Tutorial Overview](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) article and complete the **prerequisite** steps.</span></span>       
2. <span data-ttu-id="2772e-128">To create Data Factory instances, you must be a member of the [Data Factory Contributor](../../role-based-access-control/built-in-roles.md#data-factory-contributor) role at the subscription/resource group level.</span><span class="sxs-lookup"><span data-stu-id="2772e-128">To create Data Factory instances, you must be a member of the [Data Factory Contributor](../../role-based-access-control/built-in-roles.md#data-factory-contributor) role at the subscription/resource group level.</span></span>
3. <span data-ttu-id="2772e-129">You must have the following installed on your computer:</span><span class="sxs-lookup"><span data-stu-id="2772e-129">You must have the following installed on your computer:</span></span> 
   * <span data-ttu-id="2772e-130">Visual Studio 2013 or Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="2772e-130">Visual Studio 2013 or Visual Studio 2015</span></span>
   * <span data-ttu-id="2772e-131">Download Azure SDK for Visual Studio 2013 or Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="2772e-131">Download Azure SDK for Visual Studio 2013 or Visual Studio 2015.</span></span> <span data-ttu-id="2772e-132">Navigate to [Azure Download Page](https://azure.microsoft.com/downloads/) and click **VS 2013** or **VS 2015** in the **.NET** section.</span><span class="sxs-lookup"><span data-stu-id="2772e-132">Navigate to [Azure Download Page](https://azure.microsoft.com/downloads/) and click **VS 2013** or **VS 2015** in the **.NET** section.</span></span>
   * <span data-ttu-id="2772e-133">Download the latest Azure Data Factory plugin for Visual Studio: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) or [VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005).</span><span class="sxs-lookup"><span data-stu-id="2772e-133">Download the latest Azure Data Factory plugin for Visual Studio: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) or [VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005).</span></span> <span data-ttu-id="2772e-134">You can also update the plugin by doing the following steps: On the menu, click **Tools** -> **Extensions and Updates** -> **Online** -> **Visual Studio Gallery** -> **Microsoft Azure Data Factory Tools for Visual Studio** -> **Update**.</span><span class="sxs-lookup"><span data-stu-id="2772e-134">You can also update the plugin by doing the following steps: On the menu, click **Tools** -> **Extensions and Updates** -> **Online** -> **Visual Studio Gallery** -> **Microsoft Azure Data Factory Tools for Visual Studio** -> **Update**.</span></span>

## <a name="steps"></a><span data-ttu-id="2772e-135">Steps</span><span class="sxs-lookup"><span data-stu-id="2772e-135">Steps</span></span>
<span data-ttu-id="2772e-136">Here are the steps you perform as part of this tutorial:</span><span class="sxs-lookup"><span data-stu-id="2772e-136">Here are the steps you perform as part of this tutorial:</span></span>

1. <span data-ttu-id="2772e-137">Create **linked services** in the data factory.</span><span class="sxs-lookup"><span data-stu-id="2772e-137">Create **linked services** in the data factory.</span></span> <span data-ttu-id="2772e-138">In this step, you create two linked services of types: Azure Storage and Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="2772e-138">In this step, you create two linked services of types: Azure Storage and Azure SQL Database.</span></span> 
    
    <span data-ttu-id="2772e-139">The AzureStorageLinkedService links your Azure storage account to the data factory.</span><span class="sxs-lookup"><span data-stu-id="2772e-139">The AzureStorageLinkedService links your Azure storage account to the data factory.</span></span> <span data-ttu-id="2772e-140">You created a container and uploaded data to this storage account as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="2772e-140">You created a container and uploaded data to this storage account as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

    <span data-ttu-id="2772e-141">AzureSqlLinkedService links your Azure SQL database to the data factory.</span><span class="sxs-lookup"><span data-stu-id="2772e-141">AzureSqlLinkedService links your Azure SQL database to the data factory.</span></span> <span data-ttu-id="2772e-142">The data that is copied from the blob storage is stored in this database.</span><span class="sxs-lookup"><span data-stu-id="2772e-142">The data that is copied from the blob storage is stored in this database.</span></span> <span data-ttu-id="2772e-143">You created a SQL table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="2772e-143">You created a SQL table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>     
2. <span data-ttu-id="2772e-144">Create input and output **datasets** in the data factory.</span><span class="sxs-lookup"><span data-stu-id="2772e-144">Create input and output **datasets** in the data factory.</span></span>  
    
    <span data-ttu-id="2772e-145">The Azure storage linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="2772e-145">The Azure storage linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure storage account.</span></span> <span data-ttu-id="2772e-146">And, the input blob dataset specifies the container and the folder that contains the input data.</span><span class="sxs-lookup"><span data-stu-id="2772e-146">And, the input blob dataset specifies the container and the folder that contains the input data.</span></span>  

    <span data-ttu-id="2772e-147">Similarly, the Azure SQL Database linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="2772e-147">Similarly, the Azure SQL Database linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure SQL database.</span></span> <span data-ttu-id="2772e-148">And, the output SQL table dataset specifies the table in the database to which the data from the blob storage is copied.</span><span class="sxs-lookup"><span data-stu-id="2772e-148">And, the output SQL table dataset specifies the table in the database to which the data from the blob storage is copied.</span></span>
3. <span data-ttu-id="2772e-149">Create a **pipeline** in the data factory.</span><span class="sxs-lookup"><span data-stu-id="2772e-149">Create a **pipeline** in the data factory.</span></span> <span data-ttu-id="2772e-150">In this step, you create a pipeline with a copy activity.</span><span class="sxs-lookup"><span data-stu-id="2772e-150">In this step, you create a pipeline with a copy activity.</span></span>   
    
    <span data-ttu-id="2772e-151">The copy activity copies data from a blob in the Azure blob storage to a table in the Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="2772e-151">The copy activity copies data from a blob in the Azure blob storage to a table in the Azure SQL database.</span></span> <span data-ttu-id="2772e-152">You can use a copy activity in a pipeline to copy data from any supported source to any supported destination.</span><span class="sxs-lookup"><span data-stu-id="2772e-152">You can use a copy activity in a pipeline to copy data from any supported source to any supported destination.</span></span> <span data-ttu-id="2772e-153">For a list of supported data stores, see [data movement activities](data-factory-data-movement-activities.md#supported-data-stores-and-formats) article.</span><span class="sxs-lookup"><span data-stu-id="2772e-153">For a list of supported data stores, see [data movement activities](data-factory-data-movement-activities.md#supported-data-stores-and-formats) article.</span></span> 
4. <span data-ttu-id="2772e-154">Create an Azure **data factory** when deploying Data Factory entities (linked services, datasets/tables, and pipelines).</span><span class="sxs-lookup"><span data-stu-id="2772e-154">Create an Azure **data factory** when deploying Data Factory entities (linked services, datasets/tables, and pipelines).</span></span> 

## <a name="create-visual-studio-project"></a><span data-ttu-id="2772e-155">Create Visual Studio project</span><span class="sxs-lookup"><span data-stu-id="2772e-155">Create Visual Studio project</span></span>
1. <span data-ttu-id="2772e-156">Launch **Visual Studio 2015**.</span><span class="sxs-lookup"><span data-stu-id="2772e-156">Launch **Visual Studio 2015**.</span></span> <span data-ttu-id="2772e-157">Click **File**, point to **New**, and click **Project**.</span><span class="sxs-lookup"><span data-stu-id="2772e-157">Click **File**, point to **New**, and click **Project**.</span></span> <span data-ttu-id="2772e-158">You should see the **New Project** dialog box.</span><span class="sxs-lookup"><span data-stu-id="2772e-158">You should see the **New Project** dialog box.</span></span>  
2. <span data-ttu-id="2772e-159">In the **New Project** dialog, select the **DataFactory** template, and click **Empty Data Factory Project**.</span><span class="sxs-lookup"><span data-stu-id="2772e-159">In the **New Project** dialog, select the **DataFactory** template, and click **Empty Data Factory Project**.</span></span>  
   
    ![New project dialog box](./media/data-factory-copy-activity-tutorial-using-visual-studio/new-project-dialog.png)
3. <span data-ttu-id="2772e-161">Specify the name of the project, location for the solution, and name of the solution, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="2772e-161">Specify the name of the project, location for the solution, and name of the solution, and then click **OK**.</span></span>
   
    ![Solution Explorer](./media/data-factory-copy-activity-tutorial-using-visual-studio/solution-explorer.png)    

## <a name="create-linked-services"></a><span data-ttu-id="2772e-163">Create linked services</span><span class="sxs-lookup"><span data-stu-id="2772e-163">Create linked services</span></span>
<span data-ttu-id="2772e-164">You create linked services in a data factory to link your data stores and compute services to the data factory.</span><span class="sxs-lookup"><span data-stu-id="2772e-164">You create linked services in a data factory to link your data stores and compute services to the data factory.</span></span> <span data-ttu-id="2772e-165">In this tutorial, you don't use any compute service such as Azure HDInsight or Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="2772e-165">In this tutorial, you don't use any compute service such as Azure HDInsight or Azure Data Lake Analytics.</span></span> <span data-ttu-id="2772e-166">You use two data stores of type Azure Storage (source) and Azure SQL Database (destination).</span><span class="sxs-lookup"><span data-stu-id="2772e-166">You use two data stores of type Azure Storage (source) and Azure SQL Database (destination).</span></span> 

<span data-ttu-id="2772e-167">Therefore, you create two linked services of types: AzureStorage and AzureSqlDatabase.</span><span class="sxs-lookup"><span data-stu-id="2772e-167">Therefore, you create two linked services of types: AzureStorage and AzureSqlDatabase.</span></span>  

<span data-ttu-id="2772e-168">The Azure Storage linked service links your Azure storage account to the data factory.</span><span class="sxs-lookup"><span data-stu-id="2772e-168">The Azure Storage linked service links your Azure storage account to the data factory.</span></span> <span data-ttu-id="2772e-169">This storage account is the one in which you created a container and uploaded the data as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="2772e-169">This storage account is the one in which you created a container and uploaded the data as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

<span data-ttu-id="2772e-170">Azure SQL linked service links your Azure SQL database to the data factory.</span><span class="sxs-lookup"><span data-stu-id="2772e-170">Azure SQL linked service links your Azure SQL database to the data factory.</span></span> <span data-ttu-id="2772e-171">The data that is copied from the blob storage is stored in this database.</span><span class="sxs-lookup"><span data-stu-id="2772e-171">The data that is copied from the blob storage is stored in this database.</span></span> <span data-ttu-id="2772e-172">You created the emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="2772e-172">You created the emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

<span data-ttu-id="2772e-173">Linked services link data stores or compute services to an Azure data factory.</span><span class="sxs-lookup"><span data-stu-id="2772e-173">Linked services link data stores or compute services to an Azure data factory.</span></span> <span data-ttu-id="2772e-174">See [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) for all the sources and sinks supported by the Copy Activity.</span><span class="sxs-lookup"><span data-stu-id="2772e-174">See [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) for all the sources and sinks supported by the Copy Activity.</span></span> <span data-ttu-id="2772e-175">See [compute linked services](data-factory-compute-linked-services.md) for the list of compute services supported by Data Factory.</span><span class="sxs-lookup"><span data-stu-id="2772e-175">See [compute linked services](data-factory-compute-linked-services.md) for the list of compute services supported by Data Factory.</span></span> <span data-ttu-id="2772e-176">In this tutorial, you do not use any compute service.</span><span class="sxs-lookup"><span data-stu-id="2772e-176">In this tutorial, you do not use any compute service.</span></span> 

### <a name="create-the-azure-storage-linked-service"></a><span data-ttu-id="2772e-177">Create the Azure Storage linked service</span><span class="sxs-lookup"><span data-stu-id="2772e-177">Create the Azure Storage linked service</span></span>
1. <span data-ttu-id="2772e-178">In **Solution Explorer**, right-click **Linked Services**, point to **Add**, and click **New Item**.</span><span class="sxs-lookup"><span data-stu-id="2772e-178">In **Solution Explorer**, right-click **Linked Services**, point to **Add**, and click **New Item**.</span></span>      
2. <span data-ttu-id="2772e-179">In the **Add New Item** dialog box, select **Azure Storage Linked Service** from the list, and click **Add**.</span><span class="sxs-lookup"><span data-stu-id="2772e-179">In the **Add New Item** dialog box, select **Azure Storage Linked Service** from the list, and click **Add**.</span></span> 
   
    ![New Linked Service](./media/data-factory-copy-activity-tutorial-using-visual-studio/new-linked-service-dialog.png)
3. <span data-ttu-id="2772e-181">Replace `<accountname>` and `<accountkey>`\* with the name of your Azure storage account and its key.</span><span class="sxs-lookup"><span data-stu-id="2772e-181">Replace `<accountname>` and `<accountkey>`\* with the name of your Azure storage account and its key.</span></span> 
   
    ![Azure Storage Linked Service](./media/data-factory-copy-activity-tutorial-using-visual-studio/azure-storage-linked-service.png)
4. <span data-ttu-id="2772e-183">Save the **AzureStorageLinkedService1.json** file.</span><span class="sxs-lookup"><span data-stu-id="2772e-183">Save the **AzureStorageLinkedService1.json** file.</span></span>

    <span data-ttu-id="2772e-184">For more information about JSON properties in the linked service definition, see [Azure Blob Storage connector](data-factory-azure-blob-connector.md#linked-service-properties) article.</span><span class="sxs-lookup"><span data-stu-id="2772e-184">For more information about JSON properties in the linked service definition, see [Azure Blob Storage connector](data-factory-azure-blob-connector.md#linked-service-properties) article.</span></span>

### <a name="create-the-azure-sql-linked-service"></a><span data-ttu-id="2772e-185">Create the Azure SQL linked service</span><span class="sxs-lookup"><span data-stu-id="2772e-185">Create the Azure SQL linked service</span></span>
1. <span data-ttu-id="2772e-186">Right-click on **Linked Services** node in the **Solution Explorer** again, point to **Add**, and click **New Item**.</span><span class="sxs-lookup"><span data-stu-id="2772e-186">Right-click on **Linked Services** node in the **Solution Explorer** again, point to **Add**, and click **New Item**.</span></span> 
2. <span data-ttu-id="2772e-187">This time, select **Azure SQL Linked Service**, and click **Add**.</span><span class="sxs-lookup"><span data-stu-id="2772e-187">This time, select **Azure SQL Linked Service**, and click **Add**.</span></span> 
3. <span data-ttu-id="2772e-188">In the **AzureSqlLinkedService1.json file**, replace `<servername>`, `<databasename>`, `<username@servername>`, and `<password>` with names of your Azure SQL server, database, user account, and password.</span><span class="sxs-lookup"><span data-stu-id="2772e-188">In the **AzureSqlLinkedService1.json file**, replace `<servername>`, `<databasename>`, `<username@servername>`, and `<password>` with names of your Azure SQL server, database, user account, and password.</span></span>    
4. <span data-ttu-id="2772e-189">Save the **AzureSqlLinkedService1.json** file.</span><span class="sxs-lookup"><span data-stu-id="2772e-189">Save the **AzureSqlLinkedService1.json** file.</span></span> 
    
    <span data-ttu-id="2772e-190">For more information about these JSON properties, see [Azure SQL Database connector](data-factory-azure-sql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="2772e-190">For more information about these JSON properties, see [Azure SQL Database connector](data-factory-azure-sql-connector.md#linked-service-properties).</span></span>


## <a name="create-datasets"></a><span data-ttu-id="2772e-191">Create datasets</span><span class="sxs-lookup"><span data-stu-id="2772e-191">Create datasets</span></span>
<span data-ttu-id="2772e-192">In the previous step, you created linked services to link your Azure Storage account and Azure SQL database to your data factory.</span><span class="sxs-lookup"><span data-stu-id="2772e-192">In the previous step, you created linked services to link your Azure Storage account and Azure SQL database to your data factory.</span></span> <span data-ttu-id="2772e-193">In this step, you define two datasets named InputDataset and OutputDataset that represent input and output data that is stored in the data stores referred by AzureStorageLinkedService1 and AzureSqlLinkedService1 respectively.</span><span class="sxs-lookup"><span data-stu-id="2772e-193">In this step, you define two datasets named InputDataset and OutputDataset that represent input and output data that is stored in the data stores referred by AzureStorageLinkedService1 and AzureSqlLinkedService1 respectively.</span></span>

<span data-ttu-id="2772e-194">The Azure storage linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="2772e-194">The Azure storage linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure storage account.</span></span> <span data-ttu-id="2772e-195">And, the input blob dataset (InputDataset) specifies the container and the folder that contains the input data.</span><span class="sxs-lookup"><span data-stu-id="2772e-195">And, the input blob dataset (InputDataset) specifies the container and the folder that contains the input data.</span></span>  

<span data-ttu-id="2772e-196">Similarly, the Azure SQL Database linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="2772e-196">Similarly, the Azure SQL Database linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure SQL database.</span></span> <span data-ttu-id="2772e-197">And, the output SQL table dataset (OututDataset) specifies the table in the database to which the data from the blob storage is copied.</span><span class="sxs-lookup"><span data-stu-id="2772e-197">And, the output SQL table dataset (OututDataset) specifies the table in the database to which the data from the blob storage is copied.</span></span> 

### <a name="create-input-dataset"></a><span data-ttu-id="2772e-198">Create input dataset</span><span class="sxs-lookup"><span data-stu-id="2772e-198">Create input dataset</span></span>
<span data-ttu-id="2772e-199">In this step, you create a dataset named InputDataset that points to a blob file (emp.txt) in the root folder of a blob container (adftutorial) in the Azure Storage represented by the AzureStorageLinkedService1 linked service.</span><span class="sxs-lookup"><span data-stu-id="2772e-199">In this step, you create a dataset named InputDataset that points to a blob file (emp.txt) in the root folder of a blob container (adftutorial) in the Azure Storage represented by the AzureStorageLinkedService1 linked service.</span></span> <span data-ttu-id="2772e-200">If you don't specify a value for the fileName (or skip it), data from all blobs in the input folder are copied to the destination.</span><span class="sxs-lookup"><span data-stu-id="2772e-200">If you don't specify a value for the fileName (or skip it), data from all blobs in the input folder are copied to the destination.</span></span> <span data-ttu-id="2772e-201">In this tutorial, you specify a value for the fileName.</span><span class="sxs-lookup"><span data-stu-id="2772e-201">In this tutorial, you specify a value for the fileName.</span></span> 

<span data-ttu-id="2772e-202">Here, you use the term "tables" rather than "datasets".</span><span class="sxs-lookup"><span data-stu-id="2772e-202">Here, you use the term "tables" rather than "datasets".</span></span> <span data-ttu-id="2772e-203">A table is a rectangular dataset and is the only type of dataset supported right now.</span><span class="sxs-lookup"><span data-stu-id="2772e-203">A table is a rectangular dataset and is the only type of dataset supported right now.</span></span> 

1. <span data-ttu-id="2772e-204">Right-click **Tables** in the **Solution Explorer**, point to **Add**, and click **New Item**.</span><span class="sxs-lookup"><span data-stu-id="2772e-204">Right-click **Tables** in the **Solution Explorer**, point to **Add**, and click **New Item**.</span></span>
2. <span data-ttu-id="2772e-205">In the **Add New Item** dialog box, select **Azure Blob**, and click **Add**.</span><span class="sxs-lookup"><span data-stu-id="2772e-205">In the **Add New Item** dialog box, select **Azure Blob**, and click **Add**.</span></span>   
3. <span data-ttu-id="2772e-206">Replace the JSON text with the following text and save the **AzureBlobLocation1.json** file.</span><span class="sxs-lookup"><span data-stu-id="2772e-206">Replace the JSON text with the following text and save the **AzureBlobLocation1.json** file.</span></span> 

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
    <span data-ttu-id="2772e-207">The following table provides descriptions for the JSON properties used in the snippet:</span><span class="sxs-lookup"><span data-stu-id="2772e-207">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

    | <span data-ttu-id="2772e-208">Property</span><span class="sxs-lookup"><span data-stu-id="2772e-208">Property</span></span> | <span data-ttu-id="2772e-209">Description</span><span class="sxs-lookup"><span data-stu-id="2772e-209">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="2772e-210">type</span><span class="sxs-lookup"><span data-stu-id="2772e-210">type</span></span> | <span data-ttu-id="2772e-211">The type property is set to **AzureBlob** because data resides in an Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="2772e-211">The type property is set to **AzureBlob** because data resides in an Azure blob storage.</span></span> |
    | <span data-ttu-id="2772e-212">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="2772e-212">linkedServiceName</span></span> | <span data-ttu-id="2772e-213">Refers to the **AzureStorageLinkedService** that you created earlier.</span><span class="sxs-lookup"><span data-stu-id="2772e-213">Refers to the **AzureStorageLinkedService** that you created earlier.</span></span> |
    | <span data-ttu-id="2772e-214">folderPath</span><span class="sxs-lookup"><span data-stu-id="2772e-214">folderPath</span></span> | <span data-ttu-id="2772e-215">Specifies the blob **container** and the **folder** that contains input blobs.</span><span class="sxs-lookup"><span data-stu-id="2772e-215">Specifies the blob **container** and the **folder** that contains input blobs.</span></span> <span data-ttu-id="2772e-216">In this tutorial, adftutorial is the blob container and folder is the root folder.</span><span class="sxs-lookup"><span data-stu-id="2772e-216">In this tutorial, adftutorial is the blob container and folder is the root folder.</span></span> | 
    | <span data-ttu-id="2772e-217">fileName</span><span class="sxs-lookup"><span data-stu-id="2772e-217">fileName</span></span> | <span data-ttu-id="2772e-218">This property is optional.</span><span class="sxs-lookup"><span data-stu-id="2772e-218">This property is optional.</span></span> <span data-ttu-id="2772e-219">If you omit this property, all files from the folderPath are picked.</span><span class="sxs-lookup"><span data-stu-id="2772e-219">If you omit this property, all files from the folderPath are picked.</span></span> <span data-ttu-id="2772e-220">In this tutorial, **emp.txt** is specified for the fileName, so only that file is picked up for processing.</span><span class="sxs-lookup"><span data-stu-id="2772e-220">In this tutorial, **emp.txt** is specified for the fileName, so only that file is picked up for processing.</span></span> |
    | <span data-ttu-id="2772e-221">format -> type</span><span class="sxs-lookup"><span data-stu-id="2772e-221">format -> type</span></span> |<span data-ttu-id="2772e-222">The input file is in the text format, so we use **TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="2772e-222">The input file is in the text format, so we use **TextFormat**.</span></span> |
    | <span data-ttu-id="2772e-223">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="2772e-223">columnDelimiter</span></span> | <span data-ttu-id="2772e-224">The columns in the input file are delimited by **comma character (`,`)**.</span><span class="sxs-lookup"><span data-stu-id="2772e-224">The columns in the input file are delimited by **comma character (`,`)**.</span></span> |
    | <span data-ttu-id="2772e-225">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="2772e-225">frequency/interval</span></span> | <span data-ttu-id="2772e-226">The frequency is set to **Hour** and interval is  set to **1**, which means that the input slices are available **hourly**.</span><span class="sxs-lookup"><span data-stu-id="2772e-226">The frequency is set to **Hour** and interval is  set to **1**, which means that the input slices are available **hourly**.</span></span> <span data-ttu-id="2772e-227">In other words, the Data Factory service looks for input data every hour in the root folder of blob container (**adftutorial**) you specified.</span><span class="sxs-lookup"><span data-stu-id="2772e-227">In other words, the Data Factory service looks for input data every hour in the root folder of blob container (**adftutorial**) you specified.</span></span> <span data-ttu-id="2772e-228">It looks for the data within the pipeline start and end times, not before or after these times.</span><span class="sxs-lookup"><span data-stu-id="2772e-228">It looks for the data within the pipeline start and end times, not before or after these times.</span></span>  |
    | <span data-ttu-id="2772e-229">external</span><span class="sxs-lookup"><span data-stu-id="2772e-229">external</span></span> | <span data-ttu-id="2772e-230">This property is set to **true** if the data is not generated by this pipeline.</span><span class="sxs-lookup"><span data-stu-id="2772e-230">This property is set to **true** if the data is not generated by this pipeline.</span></span> <span data-ttu-id="2772e-231">The input data in this tutorial is in the emp.txt file, which is not generated by this pipeline, so we set this property to true.</span><span class="sxs-lookup"><span data-stu-id="2772e-231">The input data in this tutorial is in the emp.txt file, which is not generated by this pipeline, so we set this property to true.</span></span> |

    <span data-ttu-id="2772e-232">For more information about these JSON properties, see [Azure Blob connector article](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="2772e-232">For more information about these JSON properties, see [Azure Blob connector article](data-factory-azure-blob-connector.md#dataset-properties).</span></span>   

### <a name="create-output-dataset"></a><span data-ttu-id="2772e-233">Create output dataset</span><span class="sxs-lookup"><span data-stu-id="2772e-233">Create output dataset</span></span>
<span data-ttu-id="2772e-234">In this step, you create an output dataset named **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="2772e-234">In this step, you create an output dataset named **OutputDataset**.</span></span> <span data-ttu-id="2772e-235">This dataset points to a SQL table in the Azure SQL database represented by **AzureSqlLinkedService1**.</span><span class="sxs-lookup"><span data-stu-id="2772e-235">This dataset points to a SQL table in the Azure SQL database represented by **AzureSqlLinkedService1**.</span></span> 

1. <span data-ttu-id="2772e-236">Right-click **Tables** in the **Solution Explorer** again, point to **Add**, and click **New Item**.</span><span class="sxs-lookup"><span data-stu-id="2772e-236">Right-click **Tables** in the **Solution Explorer** again, point to **Add**, and click **New Item**.</span></span>
2. <span data-ttu-id="2772e-237">In the **Add New Item** dialog box, select **Azure SQL**, and click **Add**.</span><span class="sxs-lookup"><span data-stu-id="2772e-237">In the **Add New Item** dialog box, select **Azure SQL**, and click **Add**.</span></span> 
3. <span data-ttu-id="2772e-238">Replace the JSON text with the following JSON and save the **AzureSqlTableLocation1.json** file.</span><span class="sxs-lookup"><span data-stu-id="2772e-238">Replace the JSON text with the following JSON and save the **AzureSqlTableLocation1.json** file.</span></span>

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
    <span data-ttu-id="2772e-239">The following table provides descriptions for the JSON properties used in the snippet:</span><span class="sxs-lookup"><span data-stu-id="2772e-239">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

    | <span data-ttu-id="2772e-240">Property</span><span class="sxs-lookup"><span data-stu-id="2772e-240">Property</span></span> | <span data-ttu-id="2772e-241">Description</span><span class="sxs-lookup"><span data-stu-id="2772e-241">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="2772e-242">type</span><span class="sxs-lookup"><span data-stu-id="2772e-242">type</span></span> | <span data-ttu-id="2772e-243">The type property is set to **AzureSqlTable** because data is copied to a table in an Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="2772e-243">The type property is set to **AzureSqlTable** because data is copied to a table in an Azure SQL database.</span></span> |
    | <span data-ttu-id="2772e-244">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="2772e-244">linkedServiceName</span></span> | <span data-ttu-id="2772e-245">Refers to the **AzureSqlLinkedService** that you created earlier.</span><span class="sxs-lookup"><span data-stu-id="2772e-245">Refers to the **AzureSqlLinkedService** that you created earlier.</span></span> |
    | <span data-ttu-id="2772e-246">tableName</span><span class="sxs-lookup"><span data-stu-id="2772e-246">tableName</span></span> | <span data-ttu-id="2772e-247">Specified the **table** to which the data is copied.</span><span class="sxs-lookup"><span data-stu-id="2772e-247">Specified the **table** to which the data is copied.</span></span> | 
    | <span data-ttu-id="2772e-248">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="2772e-248">frequency/interval</span></span> | <span data-ttu-id="2772e-249">The frequency is set to **Hour** and interval is **1**, which means that the output slices are produced **hourly** between the pipeline start and end times, not before or after these times.</span><span class="sxs-lookup"><span data-stu-id="2772e-249">The frequency is set to **Hour** and interval is **1**, which means that the output slices are produced **hourly** between the pipeline start and end times, not before or after these times.</span></span>  |

    <span data-ttu-id="2772e-250">There are three columns – **ID**, **FirstName**, and **LastName** – in the emp table in the database.</span><span class="sxs-lookup"><span data-stu-id="2772e-250">There are three columns – **ID**, **FirstName**, and **LastName** – in the emp table in the database.</span></span> <span data-ttu-id="2772e-251">ID is an identity column, so you need to specify only **FirstName** and **LastName** here.</span><span class="sxs-lookup"><span data-stu-id="2772e-251">ID is an identity column, so you need to specify only **FirstName** and **LastName** here.</span></span>

    <span data-ttu-id="2772e-252">For more information about these JSON properties, see [Azure SQL connector article](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="2772e-252">For more information about these JSON properties, see [Azure SQL connector article](data-factory-azure-sql-connector.md#dataset-properties).</span></span>

## <a name="create-pipeline"></a><span data-ttu-id="2772e-253">Create pipeline</span><span class="sxs-lookup"><span data-stu-id="2772e-253">Create pipeline</span></span>
<span data-ttu-id="2772e-254">In this step, you create a pipeline with a **copy activity** that uses **InputDataset** as an input and **OutputDataset** as an output.</span><span class="sxs-lookup"><span data-stu-id="2772e-254">In this step, you create a pipeline with a **copy activity** that uses **InputDataset** as an input and **OutputDataset** as an output.</span></span>

<span data-ttu-id="2772e-255">Currently, output dataset is what drives the schedule.</span><span class="sxs-lookup"><span data-stu-id="2772e-255">Currently, output dataset is what drives the schedule.</span></span> <span data-ttu-id="2772e-256">In this tutorial, output dataset is configured to produce a slice once an hour.</span><span class="sxs-lookup"><span data-stu-id="2772e-256">In this tutorial, output dataset is configured to produce a slice once an hour.</span></span> <span data-ttu-id="2772e-257">The pipeline has a start time and end time that are one day apart, which is 24 hours.</span><span class="sxs-lookup"><span data-stu-id="2772e-257">The pipeline has a start time and end time that are one day apart, which is 24 hours.</span></span> <span data-ttu-id="2772e-258">Therefore, 24 slices of output dataset are produced by the pipeline.</span><span class="sxs-lookup"><span data-stu-id="2772e-258">Therefore, 24 slices of output dataset are produced by the pipeline.</span></span> 

1. <span data-ttu-id="2772e-259">Right-click **Pipelines** in the **Solution Explorer**, point to **Add**, and click **New Item**.</span><span class="sxs-lookup"><span data-stu-id="2772e-259">Right-click **Pipelines** in the **Solution Explorer**, point to **Add**, and click **New Item**.</span></span>  
2. <span data-ttu-id="2772e-260">Select **Copy Data Pipeline** in the **Add New Item** dialog box and click **Add**.</span><span class="sxs-lookup"><span data-stu-id="2772e-260">Select **Copy Data Pipeline** in the **Add New Item** dialog box and click **Add**.</span></span> 
3. <span data-ttu-id="2772e-261">Replace the JSON with the following JSON and save the **CopyActivity1.json** file.</span><span class="sxs-lookup"><span data-stu-id="2772e-261">Replace the JSON with the following JSON and save the **CopyActivity1.json** file.</span></span>

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
       "start": "2017-05-11T00:00:00Z",
       "end": "2017-05-12T00:00:00Z",
       "isPaused": false
     }
    }
    ```   
    - <span data-ttu-id="2772e-262">In the activities section, there is only one activity whose **type** is set to **Copy**.</span><span class="sxs-lookup"><span data-stu-id="2772e-262">In the activities section, there is only one activity whose **type** is set to **Copy**.</span></span> <span data-ttu-id="2772e-263">For more information about the copy activity, see [data movement activities](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="2772e-263">For more information about the copy activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="2772e-264">In Data Factory solutions, you can also use [data transformation activities](data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="2772e-264">In Data Factory solutions, you can also use [data transformation activities](data-factory-data-transformation-activities.md).</span></span>
    - <span data-ttu-id="2772e-265">Input for the activity is set to **InputDataset** and output for the activity is set to **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="2772e-265">Input for the activity is set to **InputDataset** and output for the activity is set to **OutputDataset**.</span></span> 
    - <span data-ttu-id="2772e-266">In the **typeProperties** section, **BlobSource** is specified as the source type and **SqlSink** is specified as the sink type.</span><span class="sxs-lookup"><span data-stu-id="2772e-266">In the **typeProperties** section, **BlobSource** is specified as the source type and **SqlSink** is specified as the sink type.</span></span> <span data-ttu-id="2772e-267">For a complete list of data stores supported by the copy activity as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="2772e-267">For a complete list of data stores supported by the copy activity as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="2772e-268">To learn how to use a specific supported data store as a source/sink, click the link in the table.</span><span class="sxs-lookup"><span data-stu-id="2772e-268">To learn how to use a specific supported data store as a source/sink, click the link in the table.</span></span>  
     
    <span data-ttu-id="2772e-269">Replace the value of the **start** property with the current day and **end** value with the next day.</span><span class="sxs-lookup"><span data-stu-id="2772e-269">Replace the value of the **start** property with the current day and **end** value with the next day.</span></span> <span data-ttu-id="2772e-270">You can specify only the date part and skip the time part of the date time.</span><span class="sxs-lookup"><span data-stu-id="2772e-270">You can specify only the date part and skip the time part of the date time.</span></span> <span data-ttu-id="2772e-271">For example, "2016-02-03", which is equivalent to "2016-02-03T00:00:00Z"</span><span class="sxs-lookup"><span data-stu-id="2772e-271">For example, "2016-02-03", which is equivalent to "2016-02-03T00:00:00Z"</span></span>
     
    <span data-ttu-id="2772e-272">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="2772e-272">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="2772e-273">For example: 2016-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="2772e-273">For example: 2016-10-14T16:32:41Z.</span></span> <span data-ttu-id="2772e-274">The **end** time is optional, but we use it in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="2772e-274">The **end** time is optional, but we use it in this tutorial.</span></span> 
     
    <span data-ttu-id="2772e-275">If you do not specify value for the **end** property, it is calculated as "**start + 48 hours**".</span><span class="sxs-lookup"><span data-stu-id="2772e-275">If you do not specify value for the **end** property, it is calculated as "**start + 48 hours**".</span></span> <span data-ttu-id="2772e-276">To run the pipeline indefinitely, specify **9999-09-09** as the value for the **end** property.</span><span class="sxs-lookup"><span data-stu-id="2772e-276">To run the pipeline indefinitely, specify **9999-09-09** as the value for the **end** property.</span></span>
     
    <span data-ttu-id="2772e-277">In the preceding example, there are 24 data slices as each data slice is produced hourly.</span><span class="sxs-lookup"><span data-stu-id="2772e-277">In the preceding example, there are 24 data slices as each data slice is produced hourly.</span></span>

    <span data-ttu-id="2772e-278">For descriptions of JSON properties in a pipeline definition, see [create pipelines](data-factory-create-pipelines.md) article.</span><span class="sxs-lookup"><span data-stu-id="2772e-278">For descriptions of JSON properties in a pipeline definition, see [create pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="2772e-279">For descriptions of JSON properties in a copy activity definition, see [data movement activities](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="2772e-279">For descriptions of JSON properties in a copy activity definition, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="2772e-280">For descriptions of JSON properties supported by BlobSource, see [Azure Blob connector article](data-factory-azure-blob-connector.md).</span><span class="sxs-lookup"><span data-stu-id="2772e-280">For descriptions of JSON properties supported by BlobSource, see [Azure Blob connector article](data-factory-azure-blob-connector.md).</span></span> <span data-ttu-id="2772e-281">For descriptions of JSON properties supported by SqlSink, see [Azure SQL Database connector article](data-factory-azure-sql-connector.md).</span><span class="sxs-lookup"><span data-stu-id="2772e-281">For descriptions of JSON properties supported by SqlSink, see [Azure SQL Database connector article](data-factory-azure-sql-connector.md).</span></span>

## <a name="publishdeploy-data-factory-entities"></a><span data-ttu-id="2772e-282">Publish/deploy Data Factory entities</span><span class="sxs-lookup"><span data-stu-id="2772e-282">Publish/deploy Data Factory entities</span></span>
<span data-ttu-id="2772e-283">In this step, you publish Data Factory entities (linked services, datasets, and pipeline) you created earlier.</span><span class="sxs-lookup"><span data-stu-id="2772e-283">In this step, you publish Data Factory entities (linked services, datasets, and pipeline) you created earlier.</span></span> <span data-ttu-id="2772e-284">You also specify the name of the new data factory to be created to hold these entities.</span><span class="sxs-lookup"><span data-stu-id="2772e-284">You also specify the name of the new data factory to be created to hold these entities.</span></span>  

1. <span data-ttu-id="2772e-285">Right-click project in the Solution Explorer, and click **Publish**.</span><span class="sxs-lookup"><span data-stu-id="2772e-285">Right-click project in the Solution Explorer, and click **Publish**.</span></span> 
2. <span data-ttu-id="2772e-286">If you see **Sign in to your Microsoft account** dialog box, enter your credentials for the account that has Azure subscription, and click **sign in**.</span><span class="sxs-lookup"><span data-stu-id="2772e-286">If you see **Sign in to your Microsoft account** dialog box, enter your credentials for the account that has Azure subscription, and click **sign in**.</span></span>
3. <span data-ttu-id="2772e-287">You should see the following dialog box:</span><span class="sxs-lookup"><span data-stu-id="2772e-287">You should see the following dialog box:</span></span>
   
   ![Publish dialog box](./media/data-factory-copy-activity-tutorial-using-visual-studio/publish.png)
4. <span data-ttu-id="2772e-289">In the Configure data factory page, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="2772e-289">In the Configure data factory page, do the following steps:</span></span> 
   
   1. <span data-ttu-id="2772e-290">select **Create New Data Factory** option.</span><span class="sxs-lookup"><span data-stu-id="2772e-290">select **Create New Data Factory** option.</span></span>
   2. <span data-ttu-id="2772e-291">Enter **VSTutorialFactory** for **Name**.</span><span class="sxs-lookup"><span data-stu-id="2772e-291">Enter **VSTutorialFactory** for **Name**.</span></span>  
      
      > [!IMPORTANT]
      > The name of the Azure data factory must be globally unique. If you receive an error about the name of data factory when publishing, change the name of the data factory (for example, yournameVSTutorialFactory) and try publishing again. See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.        
      > 
      > 
   3. <span data-ttu-id="2772e-295">Select your Azure subscription for the **Subscription** field.</span><span class="sxs-lookup"><span data-stu-id="2772e-295">Select your Azure subscription for the **Subscription** field.</span></span>
      
      > [!IMPORTANT]
      > If you do not see any subscription, ensure that you logged in using an account that is an admin or co-admin of the subscription.  
      > 
      > 
   4. <span data-ttu-id="2772e-297">Select the **resource group** for the data factory to be created.</span><span class="sxs-lookup"><span data-stu-id="2772e-297">Select the **resource group** for the data factory to be created.</span></span> 
   5. <span data-ttu-id="2772e-298">Select the **region** for the data factory.</span><span class="sxs-lookup"><span data-stu-id="2772e-298">Select the **region** for the data factory.</span></span> <span data-ttu-id="2772e-299">Only regions supported by the Data Factory service are shown in the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="2772e-299">Only regions supported by the Data Factory service are shown in the drop-down list.</span></span>
   6. <span data-ttu-id="2772e-300">Click **Next** to switch to the **Publish Items** page.</span><span class="sxs-lookup"><span data-stu-id="2772e-300">Click **Next** to switch to the **Publish Items** page.</span></span>
      
       ![Configure data factory page](media/data-factory-copy-activity-tutorial-using-visual-studio/configure-data-factory-page.png)   
5. <span data-ttu-id="2772e-302">In the **Publish Items** page, ensure that all the Data Factories entities are selected, and click **Next** to switch to the **Summary** page.</span><span class="sxs-lookup"><span data-stu-id="2772e-302">In the **Publish Items** page, ensure that all the Data Factories entities are selected, and click **Next** to switch to the **Summary** page.</span></span>
   
   ![Publish items page](media/data-factory-copy-activity-tutorial-using-visual-studio/publish-items-page.png)     
6. <span data-ttu-id="2772e-304">Review the summary and click **Next** to start the deployment process and view the **Deployment Status**.</span><span class="sxs-lookup"><span data-stu-id="2772e-304">Review the summary and click **Next** to start the deployment process and view the **Deployment Status**.</span></span>
   
   ![Publish summary page](media/data-factory-copy-activity-tutorial-using-visual-studio/publish-summary-page.png)
7. <span data-ttu-id="2772e-306">In the **Deployment Status** page, you should see the status of the deployment process.</span><span class="sxs-lookup"><span data-stu-id="2772e-306">In the **Deployment Status** page, you should see the status of the deployment process.</span></span> <span data-ttu-id="2772e-307">Click Finish after the deployment is done.</span><span class="sxs-lookup"><span data-stu-id="2772e-307">Click Finish after the deployment is done.</span></span>
 
   ![Deployment status page](media/data-factory-copy-activity-tutorial-using-visual-studio/deployment-status.png)

<span data-ttu-id="2772e-309">Note the following points:</span><span class="sxs-lookup"><span data-stu-id="2772e-309">Note the following points:</span></span> 

* <span data-ttu-id="2772e-310">If you receive the error: "This subscription is not registered to use namespace Microsoft.DataFactory", do one of the following and try publishing again:</span><span class="sxs-lookup"><span data-stu-id="2772e-310">If you receive the error: "This subscription is not registered to use namespace Microsoft.DataFactory", do one of the following and try publishing again:</span></span> 
  
  * <span data-ttu-id="2772e-311">In Azure PowerShell, run the following command to register the Data Factory provider.</span><span class="sxs-lookup"><span data-stu-id="2772e-311">In Azure PowerShell, run the following command to register the Data Factory provider.</span></span> 

    ```PowerShell    
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```
    <span data-ttu-id="2772e-312">You can run the following command to confirm that the Data Factory provider is registered.</span><span class="sxs-lookup"><span data-stu-id="2772e-312">You can run the following command to confirm that the Data Factory provider is registered.</span></span> 
    
    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="2772e-313">Login using the Azure subscription into the [Azure portal](https://portal.azure.com) and navigate to a Data Factory blade (or) create a data factory in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="2772e-313">Login using the Azure subscription into the [Azure portal](https://portal.azure.com) and navigate to a Data Factory blade (or) create a data factory in the Azure portal.</span></span> <span data-ttu-id="2772e-314">This action automatically registers the provider for you.</span><span class="sxs-lookup"><span data-stu-id="2772e-314">This action automatically registers the provider for you.</span></span>
* <span data-ttu-id="2772e-315">The name of the data factory may be registered as a DNS name in the future and hence become publically visible.</span><span class="sxs-lookup"><span data-stu-id="2772e-315">The name of the data factory may be registered as a DNS name in the future and hence become publically visible.</span></span>

> [!IMPORTANT]
> To create Data Factory instances, you need to be a admin/co-admin of the Azure subscription

## <a name="monitor-pipeline"></a><span data-ttu-id="2772e-317">Monitor pipeline</span><span class="sxs-lookup"><span data-stu-id="2772e-317">Monitor pipeline</span></span>
<span data-ttu-id="2772e-318">Navigate to the home page for your data factory:</span><span class="sxs-lookup"><span data-stu-id="2772e-318">Navigate to the home page for your data factory:</span></span>

1. <span data-ttu-id="2772e-319">Log in to [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2772e-319">Log in to [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="2772e-320">Click **More services** on the left menu, and click **Data factories**.</span><span class="sxs-lookup"><span data-stu-id="2772e-320">Click **More services** on the left menu, and click **Data factories**.</span></span>

    ![Browse data factories](media/data-factory-copy-activity-tutorial-using-visual-studio/browse-data-factories.png)
3. <span data-ttu-id="2772e-322">Start typing the name of your data factory.</span><span class="sxs-lookup"><span data-stu-id="2772e-322">Start typing the name of your data factory.</span></span>

    ![Name of data factory](media/data-factory-copy-activity-tutorial-using-visual-studio/enter-data-factory-name.png) 
4. <span data-ttu-id="2772e-324">Click your data factory in the results list to see the home page for your data factory.</span><span class="sxs-lookup"><span data-stu-id="2772e-324">Click your data factory in the results list to see the home page for your data factory.</span></span>

    ![Data factory home page](media/data-factory-copy-activity-tutorial-using-visual-studio/data-factory-home-page.png)
5. <span data-ttu-id="2772e-326">Follow instructions from [Monitor datasets and pipeline](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline) to monitor the pipeline and datasets you have created in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="2772e-326">Follow instructions from [Monitor datasets and pipeline](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline) to monitor the pipeline and datasets you have created in this tutorial.</span></span> <span data-ttu-id="2772e-327">Currently, Visual Studio does not support monitoring Data Factory pipelines.</span><span class="sxs-lookup"><span data-stu-id="2772e-327">Currently, Visual Studio does not support monitoring Data Factory pipelines.</span></span> 

## <a name="summary"></a><span data-ttu-id="2772e-328">Summary</span><span class="sxs-lookup"><span data-stu-id="2772e-328">Summary</span></span>
<span data-ttu-id="2772e-329">In this tutorial, you created an Azure data factory to copy data from an Azure blob to an Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="2772e-329">In this tutorial, you created an Azure data factory to copy data from an Azure blob to an Azure SQL database.</span></span> <span data-ttu-id="2772e-330">You used Visual Studio to create the data factory, linked services, datasets, and a pipeline.</span><span class="sxs-lookup"><span data-stu-id="2772e-330">You used Visual Studio to create the data factory, linked services, datasets, and a pipeline.</span></span> <span data-ttu-id="2772e-331">Here are the high-level steps you performed in this tutorial:</span><span class="sxs-lookup"><span data-stu-id="2772e-331">Here are the high-level steps you performed in this tutorial:</span></span>  

1. <span data-ttu-id="2772e-332">Created an Azure **data factory**.</span><span class="sxs-lookup"><span data-stu-id="2772e-332">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="2772e-333">Created **linked services**:</span><span class="sxs-lookup"><span data-stu-id="2772e-333">Created **linked services**:</span></span>
   1. <span data-ttu-id="2772e-334">An **Azure Storage** linked service to link your Azure Storage account that holds input data.</span><span class="sxs-lookup"><span data-stu-id="2772e-334">An **Azure Storage** linked service to link your Azure Storage account that holds input data.</span></span>     
   2. <span data-ttu-id="2772e-335">An **Azure SQL** linked service to link your Azure SQL database that holds the output data.</span><span class="sxs-lookup"><span data-stu-id="2772e-335">An **Azure SQL** linked service to link your Azure SQL database that holds the output data.</span></span> 
3. <span data-ttu-id="2772e-336">Created **datasets**, which describe input data and output data for pipelines.</span><span class="sxs-lookup"><span data-stu-id="2772e-336">Created **datasets**, which describe input data and output data for pipelines.</span></span>
4. <span data-ttu-id="2772e-337">Created a **pipeline** with a **Copy Activity** with **BlobSource** as source and **SqlSink** as sink.</span><span class="sxs-lookup"><span data-stu-id="2772e-337">Created a **pipeline** with a **Copy Activity** with **BlobSource** as source and **SqlSink** as sink.</span></span> 

<span data-ttu-id="2772e-338">To see how to use a HDInsight Hive Activity to transform data by using Azure HDInsight cluster, see [ Tutorial: Build your first pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="2772e-338">To see how to use a HDInsight Hive Activity to transform data by using Azure HDInsight cluster, see [ Tutorial: Build your first pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

<span data-ttu-id="2772e-339">You can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span><span class="sxs-lookup"><span data-stu-id="2772e-339">You can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="2772e-340">See [Scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md) for detailed information.</span><span class="sxs-lookup"><span data-stu-id="2772e-340">See [Scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md) for detailed information.</span></span> 

## <a name="view-all-data-factories-in-server-explorer"></a><span data-ttu-id="2772e-341">View all data factories in Server Explorer</span><span class="sxs-lookup"><span data-stu-id="2772e-341">View all data factories in Server Explorer</span></span>
<span data-ttu-id="2772e-342">This section describes how to use the Server Explorer in Visual Studio to view all the data factories in your Azure subscription and create a Visual Studio project based on an existing data factory.</span><span class="sxs-lookup"><span data-stu-id="2772e-342">This section describes how to use the Server Explorer in Visual Studio to view all the data factories in your Azure subscription and create a Visual Studio project based on an existing data factory.</span></span> 

1. <span data-ttu-id="2772e-343">In **Visual Studio**, click **View** on the menu, and click **Server Explorer**.</span><span class="sxs-lookup"><span data-stu-id="2772e-343">In **Visual Studio**, click **View** on the menu, and click **Server Explorer**.</span></span>
2. <span data-ttu-id="2772e-344">In the Server Explorer window, expand **Azure** and expand **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="2772e-344">In the Server Explorer window, expand **Azure** and expand **Data Factory**.</span></span> <span data-ttu-id="2772e-345">If you see **Sign in to Visual Studio**, enter the **account** associated with your Azure subscription and click **Continue**.</span><span class="sxs-lookup"><span data-stu-id="2772e-345">If you see **Sign in to Visual Studio**, enter the **account** associated with your Azure subscription and click **Continue**.</span></span> <span data-ttu-id="2772e-346">Enter **password**, and click **Sign in**.</span><span class="sxs-lookup"><span data-stu-id="2772e-346">Enter **password**, and click **Sign in**.</span></span> <span data-ttu-id="2772e-347">Visual Studio tries to get information about all Azure data factories in your subscription.</span><span class="sxs-lookup"><span data-stu-id="2772e-347">Visual Studio tries to get information about all Azure data factories in your subscription.</span></span> <span data-ttu-id="2772e-348">You see the status of this operation in the **Data Factory Task List** window.</span><span class="sxs-lookup"><span data-stu-id="2772e-348">You see the status of this operation in the **Data Factory Task List** window.</span></span>

    ![Server Explorer](./media/data-factory-copy-activity-tutorial-using-visual-studio/server-explorer.png)

## <a name="create-a-visual-studio-project-for-an-existing-data-factory"></a><span data-ttu-id="2772e-350">Create a Visual Studio project for an existing data factory</span><span class="sxs-lookup"><span data-stu-id="2772e-350">Create a Visual Studio project for an existing data factory</span></span>

- <span data-ttu-id="2772e-351">Right-click a data factory in Server Explorer, and select **Export Data Factory to New Project** to create a Visual Studio project based on an existing data factory.</span><span class="sxs-lookup"><span data-stu-id="2772e-351">Right-click a data factory in Server Explorer, and select **Export Data Factory to New Project** to create a Visual Studio project based on an existing data factory.</span></span>

    ![Export data factory to a VS project](./media/data-factory-copy-activity-tutorial-using-visual-studio/export-data-factory-menu.png)  

## <a name="update-data-factory-tools-for-visual-studio"></a><span data-ttu-id="2772e-353">Update Data Factory tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2772e-353">Update Data Factory tools for Visual Studio</span></span>
<span data-ttu-id="2772e-354">To update Azure Data Factory tools for Visual Studio, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="2772e-354">To update Azure Data Factory tools for Visual Studio, do the following steps:</span></span>

1. <span data-ttu-id="2772e-355">Click **Tools** on the menu and select **Extensions and Updates**.</span><span class="sxs-lookup"><span data-stu-id="2772e-355">Click **Tools** on the menu and select **Extensions and Updates**.</span></span> 
2. <span data-ttu-id="2772e-356">Select **Updates** in the left pane and then select **Visual Studio Gallery**.</span><span class="sxs-lookup"><span data-stu-id="2772e-356">Select **Updates** in the left pane and then select **Visual Studio Gallery**.</span></span>
3. <span data-ttu-id="2772e-357">Select **Azure Data Factory tools for Visual Studio** and click **Update**.</span><span class="sxs-lookup"><span data-stu-id="2772e-357">Select **Azure Data Factory tools for Visual Studio** and click **Update**.</span></span> <span data-ttu-id="2772e-358">If you do not see this entry, you already have the latest version of the tools.</span><span class="sxs-lookup"><span data-stu-id="2772e-358">If you do not see this entry, you already have the latest version of the tools.</span></span> 

## <a name="use-configuration-files"></a><span data-ttu-id="2772e-359">Use configuration files</span><span class="sxs-lookup"><span data-stu-id="2772e-359">Use configuration files</span></span>
<span data-ttu-id="2772e-360">You can use configuration files in Visual Studio to configure properties for linked services/tables/pipelines differently for each environment.</span><span class="sxs-lookup"><span data-stu-id="2772e-360">You can use configuration files in Visual Studio to configure properties for linked services/tables/pipelines differently for each environment.</span></span>

<span data-ttu-id="2772e-361">Consider the following JSON definition for an Azure Storage linked service.</span><span class="sxs-lookup"><span data-stu-id="2772e-361">Consider the following JSON definition for an Azure Storage linked service.</span></span> <span data-ttu-id="2772e-362">To specify **connectionString** with different values for accountname and accountkey based on the environment (Dev/Test/Production) to which you are deploying Data Factory entities.</span><span class="sxs-lookup"><span data-stu-id="2772e-362">To specify **connectionString** with different values for accountname and accountkey based on the environment (Dev/Test/Production) to which you are deploying Data Factory entities.</span></span> <span data-ttu-id="2772e-363">You can achieve this behavior by using separate configuration file for each environment.</span><span class="sxs-lookup"><span data-stu-id="2772e-363">You can achieve this behavior by using separate configuration file for each environment.</span></span>

```json
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "description": "",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
        }
    }
}
```

### <a name="add-a-configuration-file"></a><span data-ttu-id="2772e-364">Add a configuration file</span><span class="sxs-lookup"><span data-stu-id="2772e-364">Add a configuration file</span></span>
<span data-ttu-id="2772e-365">Add a configuration file for each environment by performing the following steps:</span><span class="sxs-lookup"><span data-stu-id="2772e-365">Add a configuration file for each environment by performing the following steps:</span></span>   

1. <span data-ttu-id="2772e-366">Right-click the Data Factory project in your Visual Studio solution, point to **Add**, and click **New item**.</span><span class="sxs-lookup"><span data-stu-id="2772e-366">Right-click the Data Factory project in your Visual Studio solution, point to **Add**, and click **New item**.</span></span>
2. <span data-ttu-id="2772e-367">Select **Config** from the list of installed templates on the left, select **Configuration File**, enter a **name** for the configuration file, and click **Add**.</span><span class="sxs-lookup"><span data-stu-id="2772e-367">Select **Config** from the list of installed templates on the left, select **Configuration File**, enter a **name** for the configuration file, and click **Add**.</span></span>

    ![Add configuration file](./media/data-factory-build-your-first-pipeline-using-vs/add-config-file.png)
3. <span data-ttu-id="2772e-369">Add configuration parameters and their values in the following format:</span><span class="sxs-lookup"><span data-stu-id="2772e-369">Add configuration parameters and their values in the following format:</span></span>

    ```json
    {
        "$schema": "http://datafactories.schema.management.azure.com/vsschemas/V1/Microsoft.DataFactory.Config.json",
        "AzureStorageLinkedService1": [
            {
                "name": "$.properties.typeProperties.connectionString",
                "value": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
            }
        ],
        "AzureSqlLinkedService1": [
            {
                "name": "$.properties.typeProperties.connectionString",
                "value":  "Server=tcp:<Azure SQL server name>.database.windows.net,1433;Database=<Azure SQL datbase>;User ID=<Username>;Password=<Password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
            }
        ]
    }
    ```

    <span data-ttu-id="2772e-370">This example configures connectionString property of an Azure Storage linked service and an Azure SQL linked service.</span><span class="sxs-lookup"><span data-stu-id="2772e-370">This example configures connectionString property of an Azure Storage linked service and an Azure SQL linked service.</span></span> <span data-ttu-id="2772e-371">Notice that the syntax for specifying name is [JsonPath](http://goessner.net/articles/JsonPath/).</span><span class="sxs-lookup"><span data-stu-id="2772e-371">Notice that the syntax for specifying name is [JsonPath](http://goessner.net/articles/JsonPath/).</span></span>   

    <span data-ttu-id="2772e-372">If JSON has a property that has an array of values as shown in the following code:</span><span class="sxs-lookup"><span data-stu-id="2772e-372">If JSON has a property that has an array of values as shown in the following code:</span></span>  

    ```json
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
    ```

    <span data-ttu-id="2772e-373">Configure properties as shown in the following configuration file (use zero-based indexing):</span><span class="sxs-lookup"><span data-stu-id="2772e-373">Configure properties as shown in the following configuration file (use zero-based indexing):</span></span>

    ```json
    {
        "name": "$.properties.structure[0].name",
        "value": "FirstName"
    }
    {
        "name": "$.properties.structure[0].type",
        "value": "String"
    }
    {
        "name": "$.properties.structure[1].name",
        "value": "LastName"
    }
    {
        "name": "$.properties.structure[1].type",
        "value": "String"
    }
    ```

### <a name="property-names-with-spaces"></a><span data-ttu-id="2772e-374">Property names with spaces</span><span class="sxs-lookup"><span data-stu-id="2772e-374">Property names with spaces</span></span>
<span data-ttu-id="2772e-375">If a property name has spaces in it, use square brackets as shown in the following example (Database server name):</span><span class="sxs-lookup"><span data-stu-id="2772e-375">If a property name has spaces in it, use square brackets as shown in the following example (Database server name):</span></span>

```json
 {
     "name": "$.properties.activities[1].typeProperties.webServiceParameters.['Database server name']",
     "value": "MyAsqlServer.database.windows.net"
 }
```

### <a name="deploy-solution-using-a-configuration"></a><span data-ttu-id="2772e-376">Deploy solution using a configuration</span><span class="sxs-lookup"><span data-stu-id="2772e-376">Deploy solution using a configuration</span></span>
<span data-ttu-id="2772e-377">When you are publishing Azure Data Factory entities in VS, you can specify the configuration that you want to use for that publishing operation.</span><span class="sxs-lookup"><span data-stu-id="2772e-377">When you are publishing Azure Data Factory entities in VS, you can specify the configuration that you want to use for that publishing operation.</span></span>

<span data-ttu-id="2772e-378">To publish entities in an Azure Data Factory project using configuration file:</span><span class="sxs-lookup"><span data-stu-id="2772e-378">To publish entities in an Azure Data Factory project using configuration file:</span></span>   

1. <span data-ttu-id="2772e-379">Right-click Data Factory project and click **Publish** to see the **Publish Items** dialog box.</span><span class="sxs-lookup"><span data-stu-id="2772e-379">Right-click Data Factory project and click **Publish** to see the **Publish Items** dialog box.</span></span>
2. <span data-ttu-id="2772e-380">Select an existing data factory or specify values for creating a data factory on the **Configure data factory** page, and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="2772e-380">Select an existing data factory or specify values for creating a data factory on the **Configure data factory** page, and click **Next**.</span></span>   
3. <span data-ttu-id="2772e-381">On the **Publish Items** page: you see a drop-down list with available configurations for the **Select Deployment Config** field.</span><span class="sxs-lookup"><span data-stu-id="2772e-381">On the **Publish Items** page: you see a drop-down list with available configurations for the **Select Deployment Config** field.</span></span>

    ![Select config file](./media/data-factory-build-your-first-pipeline-using-vs/select-config-file.png)
4. <span data-ttu-id="2772e-383">Select the **configuration file** that you would like to use and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="2772e-383">Select the **configuration file** that you would like to use and click **Next**.</span></span>
5. <span data-ttu-id="2772e-384">Confirm that you see the name of JSON file in the **Summary** page and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="2772e-384">Confirm that you see the name of JSON file in the **Summary** page and click **Next**.</span></span>
6. <span data-ttu-id="2772e-385">Click **Finish** after the deployment operation is finished.</span><span class="sxs-lookup"><span data-stu-id="2772e-385">Click **Finish** after the deployment operation is finished.</span></span>

<span data-ttu-id="2772e-386">When you deploy, the values from the configuration file are used to set values for properties in the JSON files before the entities are deployed to Azure Data Factory service.</span><span class="sxs-lookup"><span data-stu-id="2772e-386">When you deploy, the values from the configuration file are used to set values for properties in the JSON files before the entities are deployed to Azure Data Factory service.</span></span>   

## <a name="use-azure-key-vault"></a><span data-ttu-id="2772e-387">Use Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="2772e-387">Use Azure Key Vault</span></span>
<span data-ttu-id="2772e-388">It is not advisable and often against security policy to commit sensitive data such as connection strings to the code repository.</span><span class="sxs-lookup"><span data-stu-id="2772e-388">It is not advisable and often against security policy to commit sensitive data such as connection strings to the code repository.</span></span> <span data-ttu-id="2772e-389">See [ADF Secure Publish](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFSecurePublish) sample on GitHub to learn about storing sensitive information in Azure Key Vault and using it while publishing Data Factory entities.</span><span class="sxs-lookup"><span data-stu-id="2772e-389">See [ADF Secure Publish](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFSecurePublish) sample on GitHub to learn about storing sensitive information in Azure Key Vault and using it while publishing Data Factory entities.</span></span> <span data-ttu-id="2772e-390">The Secure Publish extension for Visual Studio allows the secrets to be stored in Key Vault and only references to them are specified in linked services/ deployment configurations.</span><span class="sxs-lookup"><span data-stu-id="2772e-390">The Secure Publish extension for Visual Studio allows the secrets to be stored in Key Vault and only references to them are specified in linked services/ deployment configurations.</span></span> <span data-ttu-id="2772e-391">These references are resolved when you publish Data Factory entities to Azure.</span><span class="sxs-lookup"><span data-stu-id="2772e-391">These references are resolved when you publish Data Factory entities to Azure.</span></span> <span data-ttu-id="2772e-392">These files can then be committed to source repository without exposing any secrets.</span><span class="sxs-lookup"><span data-stu-id="2772e-392">These files can then be committed to source repository without exposing any secrets.</span></span>


## <a name="next-steps"></a><span data-ttu-id="2772e-393">Next steps</span><span class="sxs-lookup"><span data-stu-id="2772e-393">Next steps</span></span>
<span data-ttu-id="2772e-394">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span><span class="sxs-lookup"><span data-stu-id="2772e-394">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="2772e-395">The following table provides a list of data stores supported as sources and destinations by the copy activity:</span><span class="sxs-lookup"><span data-stu-id="2772e-395">The following table provides a list of data stores supported as sources and destinations by the copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="2772e-396">To learn about how to copy data to/from a data store, click the link for the data store in the table.</span><span class="sxs-lookup"><span data-stu-id="2772e-396">To learn about how to copy data to/from a data store, click the link for the data store in the table.</span></span>