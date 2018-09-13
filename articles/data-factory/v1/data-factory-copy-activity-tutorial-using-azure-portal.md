---
title: 'Tutorial: Create an Azure Data Factory pipeline to copy data (Azure portal) | Microsoft Docs'
description: In this tutorial, you use Azure portal to create an Azure Data Factory pipeline with a Copy Activity to copy data from an Azure blob storage to an Azure SQL database.
services: data-factory
documentationcenter: ''
author: linda33wj
manager: ''
editor: ''
ms.assetid: d9317652-0170-4fd3-b9b2-37711272162b
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 01/22/2018
ms.author: jingwang
robots: noindex
ms.openlocfilehash: 1373882fa64ac334b92dc772fc04d4b40260cc25
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855888"
---
# <a name="tutorial-use-azure-portal-to-create-a-data-factory-pipeline-to-copy-data"></a><span data-ttu-id="f5ad9-103">Tutorial: Use Azure portal to create a Data Factory pipeline to copy data</span><span class="sxs-lookup"><span data-stu-id="f5ad9-103">Tutorial: Use Azure portal to create a Data Factory pipeline to copy data</span></span> 
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

> [!NOTE]
> This article applies to version 1 of Data Factory. If you are using the current version of the Data Factory service, see [copy activity tutorial](../quickstart-create-data-factory-dot-net.md). 

<span data-ttu-id="f5ad9-114">In this article, you learn how to use [Azure portal](https://portal.azure.com) to create a data factory with a pipeline that copies data from an Azure blob storage to an Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-114">In this article, you learn how to use [Azure portal](https://portal.azure.com) to create a data factory with a pipeline that copies data from an Azure blob storage to an Azure SQL database.</span></span> <span data-ttu-id="f5ad9-115">If you are new to Azure Data Factory, read through the [Introduction to Azure Data Factory](data-factory-introduction.md) article before doing this tutorial.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-115">If you are new to Azure Data Factory, read through the [Introduction to Azure Data Factory](data-factory-introduction.md) article before doing this tutorial.</span></span>   

<span data-ttu-id="f5ad9-116">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-116">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="f5ad9-117">The copy activity copies data from a supported data store to a supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-117">The copy activity copies data from a supported data store to a supported sink data store.</span></span> <span data-ttu-id="f5ad9-118">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="f5ad9-118">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="f5ad9-119">The activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-119">The activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="f5ad9-120">For more information about the Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="f5ad9-120">For more information about the Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="f5ad9-121">A pipeline can have more than one activity.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-121">A pipeline can have more than one activity.</span></span> <span data-ttu-id="f5ad9-122">And, you can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-122">And, you can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="f5ad9-123">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="f5ad9-123">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span> 

> [!NOTE] 
> The data pipeline in this tutorial copies data from a source data store to a destination data store. For a tutorial on how to transform data using Azure Data Factory, see [Tutorial: Build a pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).

## <a name="prerequisites"></a><span data-ttu-id="f5ad9-126">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f5ad9-126">Prerequisites</span></span>
<span data-ttu-id="f5ad9-127">Complete prerequisites listed in the [tutorial prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) article before performing this tutorial.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-127">Complete prerequisites listed in the [tutorial prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) article before performing this tutorial.</span></span>

## <a name="steps"></a><span data-ttu-id="f5ad9-128">Steps</span><span class="sxs-lookup"><span data-stu-id="f5ad9-128">Steps</span></span>
<span data-ttu-id="f5ad9-129">Here are the steps you perform as part of this tutorial:</span><span class="sxs-lookup"><span data-stu-id="f5ad9-129">Here are the steps you perform as part of this tutorial:</span></span>

1. <span data-ttu-id="f5ad9-130">Create an Azure **data factory**.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-130">Create an Azure **data factory**.</span></span> <span data-ttu-id="f5ad9-131">In this step, you create a data factory named ADFTutorialDataFactory.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-131">In this step, you create a data factory named ADFTutorialDataFactory.</span></span> 
2. <span data-ttu-id="f5ad9-132">Create **linked services** in the data factory.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-132">Create **linked services** in the data factory.</span></span> <span data-ttu-id="f5ad9-133">In this step, you create two linked services of types: Azure Storage and Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-133">In this step, you create two linked services of types: Azure Storage and Azure SQL Database.</span></span> 
    
    <span data-ttu-id="f5ad9-134">The AzureStorageLinkedService links your Azure storage account to the data factory.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-134">The AzureStorageLinkedService links your Azure storage account to the data factory.</span></span> <span data-ttu-id="f5ad9-135">You created a container and uploaded data to this storage account as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="f5ad9-135">You created a container and uploaded data to this storage account as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

    <span data-ttu-id="f5ad9-136">AzureSqlLinkedService links your Azure SQL database to the data factory.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-136">AzureSqlLinkedService links your Azure SQL database to the data factory.</span></span> <span data-ttu-id="f5ad9-137">The data that is copied from the blob storage is stored in this database.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-137">The data that is copied from the blob storage is stored in this database.</span></span> <span data-ttu-id="f5ad9-138">You created a SQL table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="f5ad9-138">You created a SQL table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   
3. <span data-ttu-id="f5ad9-139">Create input and output **datasets** in the data factory.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-139">Create input and output **datasets** in the data factory.</span></span>  
    
    <span data-ttu-id="f5ad9-140">The Azure storage linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-140">The Azure storage linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure storage account.</span></span> <span data-ttu-id="f5ad9-141">And, the input blob dataset specifies the container and the folder that contains the input data.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-141">And, the input blob dataset specifies the container and the folder that contains the input data.</span></span>  

    <span data-ttu-id="f5ad9-142">Similarly, the Azure SQL Database linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-142">Similarly, the Azure SQL Database linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure SQL database.</span></span> <span data-ttu-id="f5ad9-143">And, the output SQL table dataset specifies the table in the database to which the data from the blob storage is copied.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-143">And, the output SQL table dataset specifies the table in the database to which the data from the blob storage is copied.</span></span>
4. <span data-ttu-id="f5ad9-144">Create a **pipeline** in the data factory.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-144">Create a **pipeline** in the data factory.</span></span> <span data-ttu-id="f5ad9-145">In this step, you create a pipeline with a copy activity.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-145">In this step, you create a pipeline with a copy activity.</span></span>   
    
    <span data-ttu-id="f5ad9-146">The copy activity copies data from a blob in the Azure blob storage to a table in the Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-146">The copy activity copies data from a blob in the Azure blob storage to a table in the Azure SQL database.</span></span> <span data-ttu-id="f5ad9-147">You can use a copy activity in a pipeline to copy data from any supported source to any supported destination.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-147">You can use a copy activity in a pipeline to copy data from any supported source to any supported destination.</span></span> <span data-ttu-id="f5ad9-148">For a list of supported data stores, see [data movement activities](data-factory-data-movement-activities.md#supported-data-stores-and-formats) article.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-148">For a list of supported data stores, see [data movement activities](data-factory-data-movement-activities.md#supported-data-stores-and-formats) article.</span></span> 
5. <span data-ttu-id="f5ad9-149">Monitor the pipeline.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-149">Monitor the pipeline.</span></span> <span data-ttu-id="f5ad9-150">In this step, you **monitor** the slices of input and output datasets by using Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-150">In this step, you **monitor** the slices of input and output datasets by using Azure portal.</span></span> 

## <a name="create-data-factory"></a><span data-ttu-id="f5ad9-151">Create data factory</span><span class="sxs-lookup"><span data-stu-id="f5ad9-151">Create data factory</span></span>
> [!IMPORTANT]
> Complete [prerequisites for the tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) if you haven't already done so.   

<span data-ttu-id="f5ad9-153">A data factory can have one or more pipelines.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-153">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="f5ad9-154">A pipeline can have one or more activities in it.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-154">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="f5ad9-155">For example, a Copy Activity to copy data from a source to a destination data store and a HDInsight Hive activity to run a Hive script to transform input data to product output data.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-155">For example, a Copy Activity to copy data from a source to a destination data store and a HDInsight Hive activity to run a Hive script to transform input data to product output data.</span></span> <span data-ttu-id="f5ad9-156">Let's start with creating the data factory in this step.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-156">Let's start with creating the data factory in this step.</span></span>

1. <span data-ttu-id="f5ad9-157">After logging in to the [Azure portal](https://portal.azure.com/), click **Create a resource** on the left menu, click **Data + Analytics**, and click **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-157">After logging in to the [Azure portal](https://portal.azure.com/), click **Create a resource** on the left menu, click **Data + Analytics**, and click **Data Factory**.</span></span> 
   
   ![New->DataFactory](./media/data-factory-copy-activity-tutorial-using-azure-portal/NewDataFactoryMenu.png)    
2. <span data-ttu-id="f5ad9-159">In the **New data factory** blade:</span><span class="sxs-lookup"><span data-stu-id="f5ad9-159">In the **New data factory** blade:</span></span>
   
   1. <span data-ttu-id="f5ad9-160">Enter **ADFTutorialDataFactory** for the **name**.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-160">Enter **ADFTutorialDataFactory** for the **name**.</span></span> 
      
         ![New data factory blade](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-new-data-factory.png)
      
       <span data-ttu-id="f5ad9-162">The name of the Azure data factory must be **globally unique**.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-162">The name of the Azure data factory must be **globally unique**.</span></span> <span data-ttu-id="f5ad9-163">If you receive the following error, change the name of the data factory (for example, yournameADFTutorialDataFactory) and try creating again.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-163">If you receive the following error, change the name of the data factory (for example, yournameADFTutorialDataFactory) and try creating again.</span></span> <span data-ttu-id="f5ad9-164">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-164">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
      
           Data factory name “ADFTutorialDataFactory” is not available  
      
       ![Data Factory name not available](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-data-factory-not-available.png)
   2. <span data-ttu-id="f5ad9-166">Select your Azure **subscription** in which you want to create the data factory.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-166">Select your Azure **subscription** in which you want to create the data factory.</span></span> 
   3. <span data-ttu-id="f5ad9-167">For the **Resource Group**, do one of the following steps:</span><span class="sxs-lookup"><span data-stu-id="f5ad9-167">For the **Resource Group**, do one of the following steps:</span></span>
      
      - <span data-ttu-id="f5ad9-168">Select **Use existing**, and select an existing resource group from the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-168">Select **Use existing**, and select an existing resource group from the drop-down list.</span></span> 
      - <span data-ttu-id="f5ad9-169">Select **Create new**, and enter the name of a resource group.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-169">Select **Create new**, and enter the name of a resource group.</span></span>   
         
          <span data-ttu-id="f5ad9-170">Some of the steps in this tutorial assume that you use the name: **ADFTutorialResourceGroup** for the resource group.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-170">Some of the steps in this tutorial assume that you use the name: **ADFTutorialResourceGroup** for the resource group.</span></span> <span data-ttu-id="f5ad9-171">To learn about resource groups, see [Using resource groups to manage your Azure resources](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f5ad9-171">To learn about resource groups, see [Using resource groups to manage your Azure resources](../../azure-resource-manager/resource-group-overview.md).</span></span>  
   4. <span data-ttu-id="f5ad9-172">Select the **location** for the data factory.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-172">Select the **location** for the data factory.</span></span> <span data-ttu-id="f5ad9-173">Only regions supported by the Data Factory service are shown in the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-173">Only regions supported by the Data Factory service are shown in the drop-down list.</span></span>
   5. <span data-ttu-id="f5ad9-174">Select **Pin to dashboard**.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-174">Select **Pin to dashboard**.</span></span>     
   6. <span data-ttu-id="f5ad9-175">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-175">Click **Create**.</span></span>
      
      > [!IMPORTANT]
      > To create Data Factory instances, you must be a member of the [Data Factory Contributor](../../role-based-access-control/built-in-roles.md#data-factory-contributor) role at the subscription/resource group level.
      > 
      > The name of the data factory may be registered as a DNS name in the future and hence become publically visible.                
      > 
      > 
3. <span data-ttu-id="f5ad9-178">On the dashboard, you see the following tile with status: **Deploying data factory**.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-178">On the dashboard, you see the following tile with status: **Deploying data factory**.</span></span> 

    ![deploying data factory tile](media/data-factory-copy-activity-tutorial-using-azure-portal/deploying-data-factory.png)
4. <span data-ttu-id="f5ad9-180">After the creation is complete, you see the **Data Factory** blade as shown in the image.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-180">After the creation is complete, you see the **Data Factory** blade as shown in the image.</span></span>
   
   ![Data factory home page](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-data-factory-home-page.png)

## <a name="create-linked-services"></a><span data-ttu-id="f5ad9-182">Create linked services</span><span class="sxs-lookup"><span data-stu-id="f5ad9-182">Create linked services</span></span>
<span data-ttu-id="f5ad9-183">You create linked services in a data factory to link your data stores and compute services to the data factory.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-183">You create linked services in a data factory to link your data stores and compute services to the data factory.</span></span> <span data-ttu-id="f5ad9-184">In this tutorial, you don't use any compute service such as Azure HDInsight or Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-184">In this tutorial, you don't use any compute service such as Azure HDInsight or Azure Data Lake Analytics.</span></span> <span data-ttu-id="f5ad9-185">You use two data stores of type Azure Storage (source) and Azure SQL Database (destination).</span><span class="sxs-lookup"><span data-stu-id="f5ad9-185">You use two data stores of type Azure Storage (source) and Azure SQL Database (destination).</span></span> 

<span data-ttu-id="f5ad9-186">Therefore, you create two linked services named AzureStorageLinkedService and AzureSqlLinkedService of types: AzureStorage and AzureSqlDatabase.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-186">Therefore, you create two linked services named AzureStorageLinkedService and AzureSqlLinkedService of types: AzureStorage and AzureSqlDatabase.</span></span>  

<span data-ttu-id="f5ad9-187">The AzureStorageLinkedService links your Azure storage account to the data factory.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-187">The AzureStorageLinkedService links your Azure storage account to the data factory.</span></span> <span data-ttu-id="f5ad9-188">This storage account is the one in which you created a container and uploaded the data as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="f5ad9-188">This storage account is the one in which you created a container and uploaded the data as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

<span data-ttu-id="f5ad9-189">AzureSqlLinkedService links your Azure SQL database to the data factory.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-189">AzureSqlLinkedService links your Azure SQL database to the data factory.</span></span> <span data-ttu-id="f5ad9-190">The data that is copied from the blob storage is stored in this database.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-190">The data that is copied from the blob storage is stored in this database.</span></span> <span data-ttu-id="f5ad9-191">You created the emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="f5ad9-191">You created the emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>  

### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="f5ad9-192">Create Azure Storage linked service</span><span class="sxs-lookup"><span data-stu-id="f5ad9-192">Create Azure Storage linked service</span></span>
<span data-ttu-id="f5ad9-193">In this step, you link your Azure storage account to your data factory.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-193">In this step, you link your Azure storage account to your data factory.</span></span> <span data-ttu-id="f5ad9-194">You specify the name and key of your Azure storage account in this section.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-194">You specify the name and key of your Azure storage account in this section.</span></span>  

1. <span data-ttu-id="f5ad9-195">In the **Data Factory** blade, click **Author and deploy** tile.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-195">In the **Data Factory** blade, click **Author and deploy** tile.</span></span>
   
   ![Author and Deploy Tile](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-author-deploy-tile.png) 
2. <span data-ttu-id="f5ad9-197">You see the **Data Factory Editor** as shown in the following image:</span><span class="sxs-lookup"><span data-stu-id="f5ad9-197">You see the **Data Factory Editor** as shown in the following image:</span></span> 

    ![Data Factory Editor](./media/data-factory-copy-activity-tutorial-using-azure-portal/data-factory-editor.png)
3. <span data-ttu-id="f5ad9-199">In the editor, click **New data store** button on the toolbar and select **Azure storage** from the drop-down menu.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-199">In the editor, click **New data store** button on the toolbar and select **Azure storage** from the drop-down menu.</span></span> <span data-ttu-id="f5ad9-200">You should see the JSON template for creating an Azure storage linked service in the right pane.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-200">You should see the JSON template for creating an Azure storage linked service in the right pane.</span></span> 
   
    ![Editor New data store button](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-editor-newdatastore-button.png)    
3. <span data-ttu-id="f5ad9-202">Replace `<accountname>` and `<accountkey>` with the account name and account key values for your Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-202">Replace `<accountname>` and `<accountkey>` with the account name and account key values for your Azure storage account.</span></span> 
   
    ![Editor Blob Storage JSON](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-editor-blob-storage-json.png)    
4. <span data-ttu-id="f5ad9-204">Click **Deploy** on the toolbar.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-204">Click **Deploy** on the toolbar.</span></span> <span data-ttu-id="f5ad9-205">You should see the deployed **AzureStorageLinkedService** in the tree view now.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-205">You should see the deployed **AzureStorageLinkedService** in the tree view now.</span></span> 
   
    ![Editor Blob Storage Deploy](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-editor-blob-storage-deploy.png)

    <span data-ttu-id="f5ad9-207">For more information about JSON properties in the linked service definition, see [Azure Blob Storage connector](data-factory-azure-blob-connector.md#linked-service-properties) article.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-207">For more information about JSON properties in the linked service definition, see [Azure Blob Storage connector](data-factory-azure-blob-connector.md#linked-service-properties) article.</span></span>

### <a name="create-a-linked-service-for-the-azure-sql-database"></a><span data-ttu-id="f5ad9-208">Create a linked service for the Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="f5ad9-208">Create a linked service for the Azure SQL Database</span></span>
<span data-ttu-id="f5ad9-209">In this step, you link your Azure SQL database to your data factory.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-209">In this step, you link your Azure SQL database to your data factory.</span></span> <span data-ttu-id="f5ad9-210">You specify the Azure SQL server name, database name, user name, and user password in this section.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-210">You specify the Azure SQL server name, database name, user name, and user password in this section.</span></span> 

1. <span data-ttu-id="f5ad9-211">In the **Data Factory Editor**, click **New data store** button on the toolbar and select **Azure SQL Database** from the drop-down menu.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-211">In the **Data Factory Editor**, click **New data store** button on the toolbar and select **Azure SQL Database** from the drop-down menu.</span></span> <span data-ttu-id="f5ad9-212">You should see the JSON template for creating the Azure SQL linked service in the right pane.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-212">You should see the JSON template for creating the Azure SQL linked service in the right pane.</span></span>
2. <span data-ttu-id="f5ad9-213">Replace `<servername>`, `<databasename>`, `<username>@<servername>`, and `<password>` with names of your Azure SQL server, database, user account, and password.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-213">Replace `<servername>`, `<databasename>`, `<username>@<servername>`, and `<password>` with names of your Azure SQL server, database, user account, and password.</span></span> 
3. <span data-ttu-id="f5ad9-214">Click **Deploy** on the toolbar to create and deploy the **AzureSqlLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-214">Click **Deploy** on the toolbar to create and deploy the **AzureSqlLinkedService**.</span></span>
4. <span data-ttu-id="f5ad9-215">Confirm that you see **AzureSqlLinkedService** in the tree view under **Linked services**.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-215">Confirm that you see **AzureSqlLinkedService** in the tree view under **Linked services**.</span></span>  

    <span data-ttu-id="f5ad9-216">For more information about these JSON properties, see [Azure SQL Database connector](data-factory-azure-sql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="f5ad9-216">For more information about these JSON properties, see [Azure SQL Database connector](data-factory-azure-sql-connector.md#linked-service-properties).</span></span>

## <a name="create-datasets"></a><span data-ttu-id="f5ad9-217">Create datasets</span><span class="sxs-lookup"><span data-stu-id="f5ad9-217">Create datasets</span></span>
<span data-ttu-id="f5ad9-218">In the previous step, you created linked services to link your Azure Storage account and Azure SQL database to your data factory.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-218">In the previous step, you created linked services to link your Azure Storage account and Azure SQL database to your data factory.</span></span> <span data-ttu-id="f5ad9-219">In this step, you define two datasets named InputDataset and OutputDataset that represent input and output data that is stored in the data stores referred by AzureStorageLinkedService and AzureSqlLinkedService respectively.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-219">In this step, you define two datasets named InputDataset and OutputDataset that represent input and output data that is stored in the data stores referred by AzureStorageLinkedService and AzureSqlLinkedService respectively.</span></span>

<span data-ttu-id="f5ad9-220">The Azure storage linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-220">The Azure storage linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure storage account.</span></span> <span data-ttu-id="f5ad9-221">And, the input blob dataset (InputDataset) specifies the container and the folder that contains the input data.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-221">And, the input blob dataset (InputDataset) specifies the container and the folder that contains the input data.</span></span>  

<span data-ttu-id="f5ad9-222">Similarly, the Azure SQL Database linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-222">Similarly, the Azure SQL Database linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure SQL database.</span></span> <span data-ttu-id="f5ad9-223">And, the output SQL table dataset (OututDataset) specifies the table in the database to which the data from the blob storage is copied.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-223">And, the output SQL table dataset (OututDataset) specifies the table in the database to which the data from the blob storage is copied.</span></span> 

### <a name="create-input-dataset"></a><span data-ttu-id="f5ad9-224">Create input dataset</span><span class="sxs-lookup"><span data-stu-id="f5ad9-224">Create input dataset</span></span>
<span data-ttu-id="f5ad9-225">In this step, you create a dataset named InputDataset that points to a blob file (emp.txt) in the root folder of a blob container (adftutorial) in the Azure Storage represented by the AzureStorageLinkedService linked service.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-225">In this step, you create a dataset named InputDataset that points to a blob file (emp.txt) in the root folder of a blob container (adftutorial) in the Azure Storage represented by the AzureStorageLinkedService linked service.</span></span> <span data-ttu-id="f5ad9-226">If you don't specify a value for the fileName (or skip it), data from all blobs in the input folder are copied to the destination.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-226">If you don't specify a value for the fileName (or skip it), data from all blobs in the input folder are copied to the destination.</span></span> <span data-ttu-id="f5ad9-227">In this tutorial, you specify a value for the fileName.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-227">In this tutorial, you specify a value for the fileName.</span></span> 

1. <span data-ttu-id="f5ad9-228">In the **Editor** for the Data Factory, click **... More**, click **New dataset**, and click **Azure Blob storage** from the drop-down menu.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-228">In the **Editor** for the Data Factory, click **... More**, click **New dataset**, and click **Azure Blob storage** from the drop-down menu.</span></span> 
   
    ![New dataset menu](./media/data-factory-copy-activity-tutorial-using-azure-portal/new-dataset-menu.png)
2. <span data-ttu-id="f5ad9-230">Replace JSON in the right pane with the following JSON snippet:</span><span class="sxs-lookup"><span data-stu-id="f5ad9-230">Replace JSON in the right pane with the following JSON snippet:</span></span> 
   
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

    <span data-ttu-id="f5ad9-231">The following table provides descriptions for the JSON properties used in the snippet:</span><span class="sxs-lookup"><span data-stu-id="f5ad9-231">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

    | <span data-ttu-id="f5ad9-232">Property</span><span class="sxs-lookup"><span data-stu-id="f5ad9-232">Property</span></span> | <span data-ttu-id="f5ad9-233">Description</span><span class="sxs-lookup"><span data-stu-id="f5ad9-233">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="f5ad9-234">type</span><span class="sxs-lookup"><span data-stu-id="f5ad9-234">type</span></span> | <span data-ttu-id="f5ad9-235">The type property is set to **AzureBlob** because data resides in an Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-235">The type property is set to **AzureBlob** because data resides in an Azure blob storage.</span></span> |
    | <span data-ttu-id="f5ad9-236">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="f5ad9-236">linkedServiceName</span></span> | <span data-ttu-id="f5ad9-237">Refers to the **AzureStorageLinkedService** that you created earlier.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-237">Refers to the **AzureStorageLinkedService** that you created earlier.</span></span> |
    | <span data-ttu-id="f5ad9-238">folderPath</span><span class="sxs-lookup"><span data-stu-id="f5ad9-238">folderPath</span></span> | <span data-ttu-id="f5ad9-239">Specifies the blob **container** and the **folder** that contains input blobs.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-239">Specifies the blob **container** and the **folder** that contains input blobs.</span></span> <span data-ttu-id="f5ad9-240">In this tutorial, adftutorial is the blob container and folder is the root folder.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-240">In this tutorial, adftutorial is the blob container and folder is the root folder.</span></span> | 
    | <span data-ttu-id="f5ad9-241">fileName</span><span class="sxs-lookup"><span data-stu-id="f5ad9-241">fileName</span></span> | <span data-ttu-id="f5ad9-242">This property is optional.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-242">This property is optional.</span></span> <span data-ttu-id="f5ad9-243">If you omit this property, all files from the folderPath are picked.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-243">If you omit this property, all files from the folderPath are picked.</span></span> <span data-ttu-id="f5ad9-244">In this tutorial, **emp.txt** is specified for the fileName, so only that file is picked up for processing.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-244">In this tutorial, **emp.txt** is specified for the fileName, so only that file is picked up for processing.</span></span> |
    | <span data-ttu-id="f5ad9-245">format -> type</span><span class="sxs-lookup"><span data-stu-id="f5ad9-245">format -> type</span></span> |<span data-ttu-id="f5ad9-246">The input file is in the text format, so we use **TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-246">The input file is in the text format, so we use **TextFormat**.</span></span> |
    | <span data-ttu-id="f5ad9-247">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="f5ad9-247">columnDelimiter</span></span> | <span data-ttu-id="f5ad9-248">The columns in the input file are delimited by **comma character (`,`)**.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-248">The columns in the input file are delimited by **comma character (`,`)**.</span></span> |
    | <span data-ttu-id="f5ad9-249">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="f5ad9-249">frequency/interval</span></span> | <span data-ttu-id="f5ad9-250">The frequency is set to **Hour** and interval is  set to **1**, which means that the input slices are available **hourly**.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-250">The frequency is set to **Hour** and interval is  set to **1**, which means that the input slices are available **hourly**.</span></span> <span data-ttu-id="f5ad9-251">In other words, the Data Factory service looks for input data every hour in the root folder of blob container (**adftutorial**) you specified.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-251">In other words, the Data Factory service looks for input data every hour in the root folder of blob container (**adftutorial**) you specified.</span></span> <span data-ttu-id="f5ad9-252">It looks for the data within the pipeline start and end times, not before or after these times.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-252">It looks for the data within the pipeline start and end times, not before or after these times.</span></span>  |
    | <span data-ttu-id="f5ad9-253">external</span><span class="sxs-lookup"><span data-stu-id="f5ad9-253">external</span></span> | <span data-ttu-id="f5ad9-254">This property is set to **true** if the data is not generated by this pipeline.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-254">This property is set to **true** if the data is not generated by this pipeline.</span></span> <span data-ttu-id="f5ad9-255">The input data in this tutorial is in the emp.txt file, which is not generated by this pipeline, so we set this property to true.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-255">The input data in this tutorial is in the emp.txt file, which is not generated by this pipeline, so we set this property to true.</span></span> |

    <span data-ttu-id="f5ad9-256">For more information about these JSON properties, see [Azure Blob connector article](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="f5ad9-256">For more information about these JSON properties, see [Azure Blob connector article](data-factory-azure-blob-connector.md#dataset-properties).</span></span>      
3. <span data-ttu-id="f5ad9-257">Click **Deploy** on the toolbar to create and deploy the **InputDataset** dataset.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-257">Click **Deploy** on the toolbar to create and deploy the **InputDataset** dataset.</span></span> <span data-ttu-id="f5ad9-258">Confirm that you see the **InputDataset** in the tree view.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-258">Confirm that you see the **InputDataset** in the tree view.</span></span>

### <a name="create-output-dataset"></a><span data-ttu-id="f5ad9-259">Create output dataset</span><span class="sxs-lookup"><span data-stu-id="f5ad9-259">Create output dataset</span></span>
<span data-ttu-id="f5ad9-260">The Azure SQL Database linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-260">The Azure SQL Database linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure SQL database.</span></span> <span data-ttu-id="f5ad9-261">The output SQL table dataset (OututDataset) you create in this step specifies the table in the database to which the data from the blob storage is copied.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-261">The output SQL table dataset (OututDataset) you create in this step specifies the table in the database to which the data from the blob storage is copied.</span></span>

1. <span data-ttu-id="f5ad9-262">In the **Editor** for the Data Factory, click **... More**, click **New dataset**, and click **Azure SQL** from the drop-down menu.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-262">In the **Editor** for the Data Factory, click **... More**, click **New dataset**, and click **Azure SQL** from the drop-down menu.</span></span> 
2. <span data-ttu-id="f5ad9-263">Replace JSON in the right pane with the following JSON snippet:</span><span class="sxs-lookup"><span data-stu-id="f5ad9-263">Replace JSON in the right pane with the following JSON snippet:</span></span>

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

    <span data-ttu-id="f5ad9-264">The following table provides descriptions for the JSON properties used in the snippet:</span><span class="sxs-lookup"><span data-stu-id="f5ad9-264">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

    | <span data-ttu-id="f5ad9-265">Property</span><span class="sxs-lookup"><span data-stu-id="f5ad9-265">Property</span></span> | <span data-ttu-id="f5ad9-266">Description</span><span class="sxs-lookup"><span data-stu-id="f5ad9-266">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="f5ad9-267">type</span><span class="sxs-lookup"><span data-stu-id="f5ad9-267">type</span></span> | <span data-ttu-id="f5ad9-268">The type property is set to **AzureSqlTable** because data is copied to a table in an Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-268">The type property is set to **AzureSqlTable** because data is copied to a table in an Azure SQL database.</span></span> |
    | <span data-ttu-id="f5ad9-269">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="f5ad9-269">linkedServiceName</span></span> | <span data-ttu-id="f5ad9-270">Refers to the **AzureSqlLinkedService** that you created earlier.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-270">Refers to the **AzureSqlLinkedService** that you created earlier.</span></span> |
    | <span data-ttu-id="f5ad9-271">tableName</span><span class="sxs-lookup"><span data-stu-id="f5ad9-271">tableName</span></span> | <span data-ttu-id="f5ad9-272">Specified the **table** to which the data is copied.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-272">Specified the **table** to which the data is copied.</span></span> | 
    | <span data-ttu-id="f5ad9-273">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="f5ad9-273">frequency/interval</span></span> | <span data-ttu-id="f5ad9-274">The frequency is set to **Hour** and interval is **1**, which means that the output slices are produced **hourly** between the pipeline start and end times, not before or after these times.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-274">The frequency is set to **Hour** and interval is **1**, which means that the output slices are produced **hourly** between the pipeline start and end times, not before or after these times.</span></span>  |

    <span data-ttu-id="f5ad9-275">There are three columns – **ID**, **FirstName**, and **LastName** – in the emp table in the database.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-275">There are three columns – **ID**, **FirstName**, and **LastName** – in the emp table in the database.</span></span> <span data-ttu-id="f5ad9-276">ID is an identity column, so you need to specify only **FirstName** and **LastName** here.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-276">ID is an identity column, so you need to specify only **FirstName** and **LastName** here.</span></span>

    <span data-ttu-id="f5ad9-277">For more information about these JSON properties, see [Azure SQL connector article](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="f5ad9-277">For more information about these JSON properties, see [Azure SQL connector article](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
3. <span data-ttu-id="f5ad9-278">Click **Deploy** on the toolbar to create and deploy the **OutputDataset** dataset.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-278">Click **Deploy** on the toolbar to create and deploy the **OutputDataset** dataset.</span></span> <span data-ttu-id="f5ad9-279">Confirm that you see the **OutputDataset** in the tree view under **Datasets**.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-279">Confirm that you see the **OutputDataset** in the tree view under **Datasets**.</span></span> 

## <a name="create-pipeline"></a><span data-ttu-id="f5ad9-280">Create pipeline</span><span class="sxs-lookup"><span data-stu-id="f5ad9-280">Create pipeline</span></span>
<span data-ttu-id="f5ad9-281">In this step, you create a pipeline with a **copy activity** that uses **InputDataset** as an input and **OutputDataset** as an output.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-281">In this step, you create a pipeline with a **copy activity** that uses **InputDataset** as an input and **OutputDataset** as an output.</span></span>

<span data-ttu-id="f5ad9-282">Currently, output dataset is what drives the schedule.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-282">Currently, output dataset is what drives the schedule.</span></span> <span data-ttu-id="f5ad9-283">In this tutorial, output dataset is configured to produce a slice once an hour.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-283">In this tutorial, output dataset is configured to produce a slice once an hour.</span></span> <span data-ttu-id="f5ad9-284">The pipeline has a start time and end time that are one day apart, which is 24 hours.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-284">The pipeline has a start time and end time that are one day apart, which is 24 hours.</span></span> <span data-ttu-id="f5ad9-285">Therefore, 24 slices of output dataset are produced by the pipeline.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-285">Therefore, 24 slices of output dataset are produced by the pipeline.</span></span> 

1. <span data-ttu-id="f5ad9-286">In the **Editor** for the Data Factory, click **... More**, and click **New pipeline**.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-286">In the **Editor** for the Data Factory, click **... More**, and click **New pipeline**.</span></span> <span data-ttu-id="f5ad9-287">Alternatively, you can right-click **Pipelines** in the tree view and click **New pipeline**.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-287">Alternatively, you can right-click **Pipelines** in the tree view and click **New pipeline**.</span></span>
2. <span data-ttu-id="f5ad9-288">Replace JSON in the right pane with the following JSON snippet:</span><span class="sxs-lookup"><span data-stu-id="f5ad9-288">Replace JSON in the right pane with the following JSON snippet:</span></span> 

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
              "retry": 0,
              "timeout": "01:00:00"
            }
          }
        ],
        "start": "2017-05-11T00:00:00Z",
        "end": "2017-05-12T00:00:00Z"
      }
    } 
    ```   
    
    <span data-ttu-id="f5ad9-289">Note the following points:</span><span class="sxs-lookup"><span data-stu-id="f5ad9-289">Note the following points:</span></span>
   
    - <span data-ttu-id="f5ad9-290">In the activities section, there is only one activity whose **type** is set to **Copy**.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-290">In the activities section, there is only one activity whose **type** is set to **Copy**.</span></span> <span data-ttu-id="f5ad9-291">For more information about the copy activity, see [data movement activities](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="f5ad9-291">For more information about the copy activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="f5ad9-292">In Data Factory solutions, you can also use [data transformation activities](data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="f5ad9-292">In Data Factory solutions, you can also use [data transformation activities](data-factory-data-transformation-activities.md).</span></span>
    - <span data-ttu-id="f5ad9-293">Input for the activity is set to **InputDataset** and output for the activity is set to **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-293">Input for the activity is set to **InputDataset** and output for the activity is set to **OutputDataset**.</span></span> 
    - <span data-ttu-id="f5ad9-294">In the **typeProperties** section, **BlobSource** is specified as the source type and **SqlSink** is specified as the sink type.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-294">In the **typeProperties** section, **BlobSource** is specified as the source type and **SqlSink** is specified as the sink type.</span></span> <span data-ttu-id="f5ad9-295">For a complete list of data stores supported by the copy activity as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="f5ad9-295">For a complete list of data stores supported by the copy activity as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="f5ad9-296">To learn how to use a specific supported data store as a source/sink, click the link in the table.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-296">To learn how to use a specific supported data store as a source/sink, click the link in the table.</span></span>
    - <span data-ttu-id="f5ad9-297">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="f5ad9-297">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="f5ad9-298">For example: 2016-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-298">For example: 2016-10-14T16:32:41Z.</span></span> <span data-ttu-id="f5ad9-299">The **end** time is optional, but we use it in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-299">The **end** time is optional, but we use it in this tutorial.</span></span> <span data-ttu-id="f5ad9-300">If you do not specify value for the **end** property, it is calculated as "**start + 48 hours**".</span><span class="sxs-lookup"><span data-stu-id="f5ad9-300">If you do not specify value for the **end** property, it is calculated as "**start + 48 hours**".</span></span> <span data-ttu-id="f5ad9-301">To run the pipeline indefinitely, specify **9999-09-09** as the value for the **end** property.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-301">To run the pipeline indefinitely, specify **9999-09-09** as the value for the **end** property.</span></span>
     
    <span data-ttu-id="f5ad9-302">In the preceding example, there are 24 data slices as each data slice is produced hourly.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-302">In the preceding example, there are 24 data slices as each data slice is produced hourly.</span></span>

    <span data-ttu-id="f5ad9-303">For descriptions of JSON properties in a pipeline definition, see [create pipelines](data-factory-create-pipelines.md) article.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-303">For descriptions of JSON properties in a pipeline definition, see [create pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="f5ad9-304">For descriptions of JSON properties in a copy activity definition, see [data movement activities](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="f5ad9-304">For descriptions of JSON properties in a copy activity definition, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="f5ad9-305">For descriptions of JSON properties supported by BlobSource, see [Azure Blob connector article](data-factory-azure-blob-connector.md).</span><span class="sxs-lookup"><span data-stu-id="f5ad9-305">For descriptions of JSON properties supported by BlobSource, see [Azure Blob connector article](data-factory-azure-blob-connector.md).</span></span> <span data-ttu-id="f5ad9-306">For descriptions of JSON properties supported by SqlSink, see [Azure SQL Database connector article](data-factory-azure-sql-connector.md).</span><span class="sxs-lookup"><span data-stu-id="f5ad9-306">For descriptions of JSON properties supported by SqlSink, see [Azure SQL Database connector article](data-factory-azure-sql-connector.md).</span></span>
3. <span data-ttu-id="f5ad9-307">Click **Deploy** on the toolbar to create and deploy the **ADFTutorialPipeline**.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-307">Click **Deploy** on the toolbar to create and deploy the **ADFTutorialPipeline**.</span></span> <span data-ttu-id="f5ad9-308">Confirm that you see the pipeline in the tree view.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-308">Confirm that you see the pipeline in the tree view.</span></span> 
4. <span data-ttu-id="f5ad9-309">Now, close the **Editor** blade by clicking **X**. Click **X** again to see the **Data Factory** home page for the **ADFTutorialDataFactory**.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-309">Now, close the **Editor** blade by clicking **X**. Click **X** again to see the **Data Factory** home page for the **ADFTutorialDataFactory**.</span></span>

<span data-ttu-id="f5ad9-310">**Congratulations!**</span><span class="sxs-lookup"><span data-stu-id="f5ad9-310">**Congratulations!**</span></span> <span data-ttu-id="f5ad9-311">You have successfully created an Azure data factory with a pipeline to copy data from an Azure blob storage to an Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-311">You have successfully created an Azure data factory with a pipeline to copy data from an Azure blob storage to an Azure SQL database.</span></span> 


## <a name="monitor-pipeline"></a><span data-ttu-id="f5ad9-312">Monitor pipeline</span><span class="sxs-lookup"><span data-stu-id="f5ad9-312">Monitor pipeline</span></span>
<span data-ttu-id="f5ad9-313">In this step, you use the Azure portal to monitor what’s going on in an Azure data factory.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-313">In this step, you use the Azure portal to monitor what’s going on in an Azure data factory.</span></span>    

### <a name="monitor-pipeline-using-monitor--manage-app"></a><span data-ttu-id="f5ad9-314">Monitor pipeline using Monitor & Manage App</span><span class="sxs-lookup"><span data-stu-id="f5ad9-314">Monitor pipeline using Monitor & Manage App</span></span>
<span data-ttu-id="f5ad9-315">The following steps show you how to monitor pipelines in your data factory by using the Monitor & Manage application:</span><span class="sxs-lookup"><span data-stu-id="f5ad9-315">The following steps show you how to monitor pipelines in your data factory by using the Monitor & Manage application:</span></span> 

1. <span data-ttu-id="f5ad9-316">Click **Monitor & Manage** tile on the home page for your data factory.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-316">Click **Monitor & Manage** tile on the home page for your data factory.</span></span>
   
    ![Monitor & Manage tile](./media/data-factory-copy-activity-tutorial-using-azure-portal/monitor-manage-tile.png) 
2. <span data-ttu-id="f5ad9-318">You should see **Monitor & Manage application** in a separate tab.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-318">You should see **Monitor & Manage application** in a separate tab.</span></span> 

    > [!NOTE]
    > If you see that the web browser is stuck at "Authorizing...", do one of the following: clear the **Block third-party cookies and site data** check box (or) create an exception for **login.microsoftonline.com**, and then try to open the app again.

    ![Monitor & Manage App](./media/data-factory-copy-activity-tutorial-using-azure-portal/monitor-and-manage-app.png)
3. <span data-ttu-id="f5ad9-321">Change the **Start time** and **End time** to include start (2017-05-11) and end times (2017-05-12) of your pipeline, and click **Apply**.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-321">Change the **Start time** and **End time** to include start (2017-05-11) and end times (2017-05-12) of your pipeline, and click **Apply**.</span></span>       
3. <span data-ttu-id="f5ad9-322">You see the **activity windows** associated with each hour between pipeline start and end times in the list in the middle pane.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-322">You see the **activity windows** associated with each hour between pipeline start and end times in the list in the middle pane.</span></span> 
4. <span data-ttu-id="f5ad9-323">To see details about an activity window, select the activity window in the **Activity Windows** list.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-323">To see details about an activity window, select the activity window in the **Activity Windows** list.</span></span> 
    <span data-ttu-id="f5ad9-324">![Activity window details](./media/data-factory-copy-activity-tutorial-using-azure-portal/activity-window-details.png)</span><span class="sxs-lookup"><span data-stu-id="f5ad9-324">![Activity window details](./media/data-factory-copy-activity-tutorial-using-azure-portal/activity-window-details.png)</span></span>

    <span data-ttu-id="f5ad9-325">In Activity Window Explorer on the right, you see that the slices up to the current UTC time (8:12 PM) are all processed (in green color).</span><span class="sxs-lookup"><span data-stu-id="f5ad9-325">In Activity Window Explorer on the right, you see that the slices up to the current UTC time (8:12 PM) are all processed (in green color).</span></span> <span data-ttu-id="f5ad9-326">The 8-9 PM, 9 - 10 PM, 10 - 11 PM, 11 PM - 12 AM slices are not processed yet.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-326">The 8-9 PM, 9 - 10 PM, 10 - 11 PM, 11 PM - 12 AM slices are not processed yet.</span></span>

    <span data-ttu-id="f5ad9-327">The **Attempts** section in the right pane provides information about the activity run for the data slice.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-327">The **Attempts** section in the right pane provides information about the activity run for the data slice.</span></span> <span data-ttu-id="f5ad9-328">If there was an error, it provides details about the error.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-328">If there was an error, it provides details about the error.</span></span> <span data-ttu-id="f5ad9-329">For example, if the input folder or container does not exist and the slice processing fails, you see an error message stating that the container or folder does not exist.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-329">For example, if the input folder or container does not exist and the slice processing fails, you see an error message stating that the container or folder does not exist.</span></span>

    ![Activity run attempts](./media/data-factory-copy-activity-tutorial-using-azure-portal/activity-run-attempts.png) 
4. <span data-ttu-id="f5ad9-331">Launch **SQL Server Management Studio**, connect to the Azure SQL Database, and verify that the rows are inserted in to the **emp** table in the database.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-331">Launch **SQL Server Management Studio**, connect to the Azure SQL Database, and verify that the rows are inserted in to the **emp** table in the database.</span></span>
    
    ![sql query results](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-sql-query-results.png)

<span data-ttu-id="f5ad9-333">For detailed information about using this application, see [Monitor and manage Azure Data Factory pipelines using Monitoring and Management App](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="f5ad9-333">For detailed information about using this application, see [Monitor and manage Azure Data Factory pipelines using Monitoring and Management App](data-factory-monitor-manage-app.md).</span></span>

### <a name="monitor-pipeline-using-diagram-view"></a><span data-ttu-id="f5ad9-334">Monitor pipeline using Diagram View</span><span class="sxs-lookup"><span data-stu-id="f5ad9-334">Monitor pipeline using Diagram View</span></span>
<span data-ttu-id="f5ad9-335">You can also monitor data pipelines by using the diagram view.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-335">You can also monitor data pipelines by using the diagram view.</span></span>  

1. <span data-ttu-id="f5ad9-336">In the **Data Factory** blade, click **Diagram**.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-336">In the **Data Factory** blade, click **Diagram**.</span></span>
   
    ![Data Factory Blade - Diagram Tile](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-datafactoryblade-diagramtile.png)
2. <span data-ttu-id="f5ad9-338">You should see the diagram similar to the following image:</span><span class="sxs-lookup"><span data-stu-id="f5ad9-338">You should see the diagram similar to the following image:</span></span> 
   
    ![Diagram view](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-diagram-blade.png)  
5. <span data-ttu-id="f5ad9-340">In the diagram view, double-click **InputDataset** to see slices for the dataset.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-340">In the diagram view, double-click **InputDataset** to see slices for the dataset.</span></span>  
   
    ![Datasets with InputDataset selected](./media/data-factory-copy-activity-tutorial-using-azure-portal/DataSetsWithInputDatasetFromBlobSelected.png)   
5. <span data-ttu-id="f5ad9-342">Click **See more** link to see all the data slices.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-342">Click **See more** link to see all the data slices.</span></span> <span data-ttu-id="f5ad9-343">You see 24 hourly slices between pipeline start and end times.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-343">You see 24 hourly slices between pipeline start and end times.</span></span> 
   
    ![All input data slices](./media/data-factory-copy-activity-tutorial-using-azure-portal/all-input-slices.png)  
   
    <span data-ttu-id="f5ad9-345">Notice that all the data slices up to the current UTC time are **Ready** because the **emp.txt** file exists all the time in the blob container: **adftutorial\input**.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-345">Notice that all the data slices up to the current UTC time are **Ready** because the **emp.txt** file exists all the time in the blob container: **adftutorial\input**.</span></span> <span data-ttu-id="f5ad9-346">The slices for the future times are not in ready state yet.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-346">The slices for the future times are not in ready state yet.</span></span> <span data-ttu-id="f5ad9-347">Confirm that no slices show up in the **Recently failed slices** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-347">Confirm that no slices show up in the **Recently failed slices** section at the bottom.</span></span>
6. <span data-ttu-id="f5ad9-348">Close the blades until you see the diagram view (or) scroll left to see the diagram view.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-348">Close the blades until you see the diagram view (or) scroll left to see the diagram view.</span></span> <span data-ttu-id="f5ad9-349">Then, double-click **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-349">Then, double-click **OutputDataset**.</span></span> 
8. <span data-ttu-id="f5ad9-350">Click **See more** link on the **Table** blade for **OutputDataset** to see all the slices.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-350">Click **See more** link on the **Table** blade for **OutputDataset** to see all the slices.</span></span>

    ![data slices blade](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-dataslices-blade.png) 
9. <span data-ttu-id="f5ad9-352">Notice that all the slices up to the current UTC time move from **pending execution** state => **In progress** ==> **Ready** state.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-352">Notice that all the slices up to the current UTC time move from **pending execution** state => **In progress** ==> **Ready** state.</span></span> <span data-ttu-id="f5ad9-353">The slices from the past (before current time) are processed from latest to oldest by default.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-353">The slices from the past (before current time) are processed from latest to oldest by default.</span></span> <span data-ttu-id="f5ad9-354">For example, if the current time is 8:12 PM UTC, the slice for 7 PM - 8 PM is processed ahead of the 6 PM - 7 PM slice.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-354">For example, if the current time is 8:12 PM UTC, the slice for 7 PM - 8 PM is processed ahead of the 6 PM - 7 PM slice.</span></span> <span data-ttu-id="f5ad9-355">The 8 PM - 9 PM slice is processed at the end of the time interval by default, that is after 9 PM.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-355">The 8 PM - 9 PM slice is processed at the end of the time interval by default, that is after 9 PM.</span></span>  
10. <span data-ttu-id="f5ad9-356">Click any data slice from the list and you should see the **Data slice** blade.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-356">Click any data slice from the list and you should see the **Data slice** blade.</span></span> <span data-ttu-id="f5ad9-357">A piece of data associated with an activity window is called a slice.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-357">A piece of data associated with an activity window is called a slice.</span></span> <span data-ttu-id="f5ad9-358">A slice can be one file or multiple files.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-358">A slice can be one file or multiple files.</span></span>  
    
     ![data slice blade](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-dataslice-blade.png)
    
     <span data-ttu-id="f5ad9-360">If the slice is not in the **Ready** state, you can see the upstream slices that are not Ready and are blocking the current slice from executing in the **Upstream slices that are not ready** list.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-360">If the slice is not in the **Ready** state, you can see the upstream slices that are not Ready and are blocking the current slice from executing in the **Upstream slices that are not ready** list.</span></span>
11. <span data-ttu-id="f5ad9-361">In the **DATA SLICE** blade, you should see all activity runs in the list at the bottom.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-361">In the **DATA SLICE** blade, you should see all activity runs in the list at the bottom.</span></span> <span data-ttu-id="f5ad9-362">Click an **activity run** to see the **Activity run details** blade.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-362">Click an **activity run** to see the **Activity run details** blade.</span></span> 
    
    ![Activity Run Details](./media/data-factory-copy-activity-tutorial-using-azure-portal/ActivityRunDetails.png)

    <span data-ttu-id="f5ad9-364">In this blade, you see how long the copy operation took, what throughput is, how many bytes of data were read and written, run start time, run end time etc.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-364">In this blade, you see how long the copy operation took, what throughput is, how many bytes of data were read and written, run start time, run end time etc.</span></span>  
12. <span data-ttu-id="f5ad9-365">Click **X** to close all the blades until you get back to the home blade for the **ADFTutorialDataFactory**.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-365">Click **X** to close all the blades until you get back to the home blade for the **ADFTutorialDataFactory**.</span></span>
13. <span data-ttu-id="f5ad9-366">(optional) click the **Datasets** tile or **Pipelines** tile to get the blades you have seen the preceding steps.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-366">(optional) click the **Datasets** tile or **Pipelines** tile to get the blades you have seen the preceding steps.</span></span> 
14. <span data-ttu-id="f5ad9-367">Launch **SQL Server Management Studio**, connect to the Azure SQL Database, and verify that the rows are inserted in to the **emp** table in the database.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-367">Launch **SQL Server Management Studio**, connect to the Azure SQL Database, and verify that the rows are inserted in to the **emp** table in the database.</span></span>
    
    ![sql query results](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-sql-query-results.png)


## <a name="summary"></a><span data-ttu-id="f5ad9-369">Summary</span><span class="sxs-lookup"><span data-stu-id="f5ad9-369">Summary</span></span>
<span data-ttu-id="f5ad9-370">In this tutorial, you created an Azure data factory to copy data from an Azure blob to an Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-370">In this tutorial, you created an Azure data factory to copy data from an Azure blob to an Azure SQL database.</span></span> <span data-ttu-id="f5ad9-371">You used the Azure portal to create the data factory, linked services, datasets, and a pipeline.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-371">You used the Azure portal to create the data factory, linked services, datasets, and a pipeline.</span></span> <span data-ttu-id="f5ad9-372">Here are the high-level steps you performed in this tutorial:</span><span class="sxs-lookup"><span data-stu-id="f5ad9-372">Here are the high-level steps you performed in this tutorial:</span></span>  

1. <span data-ttu-id="f5ad9-373">Created an Azure **data factory**.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-373">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="f5ad9-374">Created **linked services**:</span><span class="sxs-lookup"><span data-stu-id="f5ad9-374">Created **linked services**:</span></span>
   1. <span data-ttu-id="f5ad9-375">An **Azure Storage** linked service to link your Azure Storage account that holds input data.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-375">An **Azure Storage** linked service to link your Azure Storage account that holds input data.</span></span>     
   2. <span data-ttu-id="f5ad9-376">An **Azure SQL** linked service to link your Azure SQL database that holds the output data.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-376">An **Azure SQL** linked service to link your Azure SQL database that holds the output data.</span></span> 
3. <span data-ttu-id="f5ad9-377">Created **datasets** that describe input data and output data for pipelines.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-377">Created **datasets** that describe input data and output data for pipelines.</span></span>
4. <span data-ttu-id="f5ad9-378">Created a **pipeline** with a **Copy Activity** with **BlobSource** as source and **SqlSink** as sink.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-378">Created a **pipeline** with a **Copy Activity** with **BlobSource** as source and **SqlSink** as sink.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="f5ad9-379">Next steps</span><span class="sxs-lookup"><span data-stu-id="f5ad9-379">Next steps</span></span>
<span data-ttu-id="f5ad9-380">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-380">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="f5ad9-381">The following table provides a list of data stores supported as sources and destinations by the copy activity:</span><span class="sxs-lookup"><span data-stu-id="f5ad9-381">The following table provides a list of data stores supported as sources and destinations by the copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="f5ad9-382">To learn about how to copy data to/from a data store, click the link for the data store in the table.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-382">To learn about how to copy data to/from a data store, click the link for the data store in the table.</span></span>