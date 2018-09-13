---
title: 'Tutorial: Create a pipeline to move data by using Azure PowerShell | Microsoft Docs'
description: In this tutorial, you create an Azure Data Factory pipeline with Copy Activity by using Azure PowerShell.
services: data-factory
documentationcenter: ''
author: linda33wj
manager: ''
editor: ''
ms.assetid: 71087349-9365-4e95-9847-170658216ed8
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 01/22/2018
ms.author: jingwang
robots: noindex
ms.openlocfilehash: bfe1d022364455f6c3e22872358b6e18b0806e6a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871674"
---
# <a name="tutorial-create-a-data-factory-pipeline-that-moves-data-by-using-azure-powershell"></a><span data-ttu-id="7ef6e-103">Tutorial: Create a Data Factory pipeline that moves data by using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="7ef6e-103">Tutorial: Create a Data Factory pipeline that moves data by using Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [Overview and prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [Copy Wizard](data-factory-copy-data-wizard-tutorial.md)
> * [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)
> * [Azure Resource Manager template](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [REST API](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [.NET API](data-factory-copy-activity-tutorial-using-dotnet-api.md)

> [!NOTE]
> This article applies to version 1 of Data Factory. If you are using the current version of the Data Factory service, see [copy activity tutorial](../quickstart-create-data-factory-powershell.md). 

<span data-ttu-id="7ef6e-114">In this article, you learn how to use PowerShell to create a data factory with a pipeline that copies data from an Azure blob storage to an Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-114">In this article, you learn how to use PowerShell to create a data factory with a pipeline that copies data from an Azure blob storage to an Azure SQL database.</span></span> <span data-ttu-id="7ef6e-115">If you are new to Azure Data Factory, read through the [Introduction to Azure Data Factory](data-factory-introduction.md) article before doing this tutorial.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-115">If you are new to Azure Data Factory, read through the [Introduction to Azure Data Factory](data-factory-introduction.md) article before doing this tutorial.</span></span>   

<span data-ttu-id="7ef6e-116">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-116">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="7ef6e-117">The copy activity copies data from a supported data store to a supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-117">The copy activity copies data from a supported data store to a supported sink data store.</span></span> <span data-ttu-id="7ef6e-118">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="7ef6e-118">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="7ef6e-119">The activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-119">The activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="7ef6e-120">For more information about the Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="7ef6e-120">For more information about the Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="7ef6e-121">A pipeline can have more than one activity.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-121">A pipeline can have more than one activity.</span></span> <span data-ttu-id="7ef6e-122">And, you can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-122">And, you can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="7ef6e-123">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="7ef6e-123">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>

> [!NOTE]
> This article does not cover all the Data Factory cmdlets. See [Data Factory Cmdlet Reference](/powershell/module/azurerm.datafactories) for comprehensive documentation on these cmdlets.
> 
> The data pipeline in this tutorial copies data from a source data store to a destination data store. For a tutorial on how to transform data using Azure Data Factory, see [Tutorial: Build a pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).

## <a name="prerequisites"></a><span data-ttu-id="7ef6e-128">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="7ef6e-128">Prerequisites</span></span>
- <span data-ttu-id="7ef6e-129">Complete prerequisites listed in the [tutorial prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) article.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-129">Complete prerequisites listed in the [tutorial prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) article.</span></span>
- <span data-ttu-id="7ef6e-130">Install **Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-130">Install **Azure PowerShell**.</span></span> <span data-ttu-id="7ef6e-131">Follow the instructions in [How to install and configure Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="7ef6e-131">Follow the instructions in [How to install and configure Azure PowerShell](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="steps"></a><span data-ttu-id="7ef6e-132">Steps</span><span class="sxs-lookup"><span data-stu-id="7ef6e-132">Steps</span></span>
<span data-ttu-id="7ef6e-133">Here are the steps you perform as part of this tutorial:</span><span class="sxs-lookup"><span data-stu-id="7ef6e-133">Here are the steps you perform as part of this tutorial:</span></span>

1. <span data-ttu-id="7ef6e-134">Create an Azure **data factory**.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-134">Create an Azure **data factory**.</span></span> <span data-ttu-id="7ef6e-135">In this step, you create a data factory named ADFTutorialDataFactoryPSH.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-135">In this step, you create a data factory named ADFTutorialDataFactoryPSH.</span></span> 
1. <span data-ttu-id="7ef6e-136">Create **linked services** in the data factory.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-136">Create **linked services** in the data factory.</span></span> <span data-ttu-id="7ef6e-137">In this step, you create two linked services of types: Azure Storage and Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-137">In this step, you create two linked services of types: Azure Storage and Azure SQL Database.</span></span> 
    
    <span data-ttu-id="7ef6e-138">The AzureStorageLinkedService links your Azure storage account to the data factory.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-138">The AzureStorageLinkedService links your Azure storage account to the data factory.</span></span> <span data-ttu-id="7ef6e-139">You created a container and uploaded data to this storage account as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="7ef6e-139">You created a container and uploaded data to this storage account as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

    <span data-ttu-id="7ef6e-140">AzureSqlLinkedService links your Azure SQL database to the data factory.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-140">AzureSqlLinkedService links your Azure SQL database to the data factory.</span></span> <span data-ttu-id="7ef6e-141">The data that is copied from the blob storage is stored in this database.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-141">The data that is copied from the blob storage is stored in this database.</span></span> <span data-ttu-id="7ef6e-142">You created a SQL table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="7ef6e-142">You created a SQL table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   
1. <span data-ttu-id="7ef6e-143">Create input and output **datasets** in the data factory.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-143">Create input and output **datasets** in the data factory.</span></span>  
    
    <span data-ttu-id="7ef6e-144">The Azure storage linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-144">The Azure storage linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure storage account.</span></span> <span data-ttu-id="7ef6e-145">And, the input blob dataset specifies the container and the folder that contains the input data.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-145">And, the input blob dataset specifies the container and the folder that contains the input data.</span></span>  

    <span data-ttu-id="7ef6e-146">Similarly, the Azure SQL Database linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-146">Similarly, the Azure SQL Database linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure SQL database.</span></span> <span data-ttu-id="7ef6e-147">And, the output SQL table dataset specifies the table in the database to which the data from the blob storage is copied.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-147">And, the output SQL table dataset specifies the table in the database to which the data from the blob storage is copied.</span></span>
1. <span data-ttu-id="7ef6e-148">Create a **pipeline** in the data factory.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-148">Create a **pipeline** in the data factory.</span></span> <span data-ttu-id="7ef6e-149">In this step, you create a pipeline with a copy activity.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-149">In this step, you create a pipeline with a copy activity.</span></span>   
    
    <span data-ttu-id="7ef6e-150">The copy activity copies data from a blob in the Azure blob storage to a table in the Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-150">The copy activity copies data from a blob in the Azure blob storage to a table in the Azure SQL database.</span></span> <span data-ttu-id="7ef6e-151">You can use a copy activity in a pipeline to copy data from any supported source to any supported destination.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-151">You can use a copy activity in a pipeline to copy data from any supported source to any supported destination.</span></span> <span data-ttu-id="7ef6e-152">For a list of supported data stores, see [data movement activities](data-factory-data-movement-activities.md#supported-data-stores-and-formats) article.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-152">For a list of supported data stores, see [data movement activities](data-factory-data-movement-activities.md#supported-data-stores-and-formats) article.</span></span> 
1. <span data-ttu-id="7ef6e-153">Monitor the pipeline.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-153">Monitor the pipeline.</span></span> <span data-ttu-id="7ef6e-154">In this step, you **monitor** the slices of input and output datasets by using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-154">In this step, you **monitor** the slices of input and output datasets by using PowerShell.</span></span>

## <a name="create-a-data-factory"></a><span data-ttu-id="7ef6e-155">Create a data factory</span><span class="sxs-lookup"><span data-stu-id="7ef6e-155">Create a data factory</span></span>
> [!IMPORTANT]
> Complete [prerequisites for the tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) if you haven't already done so.   

<span data-ttu-id="7ef6e-157">A data factory can have one or more pipelines.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-157">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="7ef6e-158">A pipeline can have one or more activities in it.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-158">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="7ef6e-159">For example, a Copy Activity to copy data from a source to a destination data store and a HDInsight Hive activity to run a Hive script to transform input data to product output data.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-159">For example, a Copy Activity to copy data from a source to a destination data store and a HDInsight Hive activity to run a Hive script to transform input data to product output data.</span></span> <span data-ttu-id="7ef6e-160">Let's start with creating the data factory in this step.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-160">Let's start with creating the data factory in this step.</span></span>

1. <span data-ttu-id="7ef6e-161">Launch **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-161">Launch **PowerShell**.</span></span> <span data-ttu-id="7ef6e-162">Keep Azure PowerShell open until the end of this tutorial.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-162">Keep Azure PowerShell open until the end of this tutorial.</span></span> <span data-ttu-id="7ef6e-163">If you close and reopen, you need to run the commands again.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-163">If you close and reopen, you need to run the commands again.</span></span>

    <span data-ttu-id="7ef6e-164">Run the following command, and enter the user name and password that you use to sign in to the Azure portal:</span><span class="sxs-lookup"><span data-stu-id="7ef6e-164">Run the following command, and enter the user name and password that you use to sign in to the Azure portal:</span></span>

    ```PowerShell
    Connect-AzureRmAccount
    ```   
   
    <span data-ttu-id="7ef6e-165">Run the following command to view all the subscriptions for this account:</span><span class="sxs-lookup"><span data-stu-id="7ef6e-165">Run the following command to view all the subscriptions for this account:</span></span>

    ```PowerShell
    Get-AzureRmSubscription
    ```

    <span data-ttu-id="7ef6e-166">Run the following command to select the subscription that you want to work with.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-166">Run the following command to select the subscription that you want to work with.</span></span> <span data-ttu-id="7ef6e-167">Replace **&lt;NameOfAzureSubscription**&gt; with the name of your Azure subscription:</span><span class="sxs-lookup"><span data-stu-id="7ef6e-167">Replace **&lt;NameOfAzureSubscription**&gt; with the name of your Azure subscription:</span></span>

    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```
1. <span data-ttu-id="7ef6e-168">Create an Azure resource group named **ADFTutorialResourceGroup** by running the following command:</span><span class="sxs-lookup"><span data-stu-id="7ef6e-168">Create an Azure resource group named **ADFTutorialResourceGroup** by running the following command:</span></span>

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```
    
    <span data-ttu-id="7ef6e-169">Some of the steps in this tutorial assume that you use the resource group named **ADFTutorialResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-169">Some of the steps in this tutorial assume that you use the resource group named **ADFTutorialResourceGroup**.</span></span> <span data-ttu-id="7ef6e-170">If you use a different resource group, you need to use it in place of ADFTutorialResourceGroup in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-170">If you use a different resource group, you need to use it in place of ADFTutorialResourceGroup in this tutorial.</span></span>
1. <span data-ttu-id="7ef6e-171">Run the **New-AzureRmDataFactory** cmdlet to create a data factory named **ADFTutorialDataFactoryPSH**:</span><span class="sxs-lookup"><span data-stu-id="7ef6e-171">Run the **New-AzureRmDataFactory** cmdlet to create a data factory named **ADFTutorialDataFactoryPSH**:</span></span>  

    ```PowerShell
    $df=New-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name ADFTutorialDataFactoryPSH –Location "West US"
    ```
    <span data-ttu-id="7ef6e-172">This name may already have been taken.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-172">This name may already have been taken.</span></span> <span data-ttu-id="7ef6e-173">Therefore, make the name of the data factory unique by adding a prefix or suffix (for example: ADFTutorialDataFactoryPSH05152017) and run the command again.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-173">Therefore, make the name of the data factory unique by adding a prefix or suffix (for example: ADFTutorialDataFactoryPSH05152017) and run the command again.</span></span>  

<span data-ttu-id="7ef6e-174">Note the following points:</span><span class="sxs-lookup"><span data-stu-id="7ef6e-174">Note the following points:</span></span>

* <span data-ttu-id="7ef6e-175">The name of the Azure data factory must be globally unique.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-175">The name of the Azure data factory must be globally unique.</span></span> <span data-ttu-id="7ef6e-176">If you receive the following error, change the name (for example, yournameADFTutorialDataFactoryPSH).</span><span class="sxs-lookup"><span data-stu-id="7ef6e-176">If you receive the following error, change the name (for example, yournameADFTutorialDataFactoryPSH).</span></span> <span data-ttu-id="7ef6e-177">Use this name in place of ADFTutorialFactoryPSH while performing steps in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-177">Use this name in place of ADFTutorialFactoryPSH while performing steps in this tutorial.</span></span> <span data-ttu-id="7ef6e-178">See [Data Factory - Naming Rules](data-factory-naming-rules.md) for Data Factory artifacts.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-178">See [Data Factory - Naming Rules](data-factory-naming-rules.md) for Data Factory artifacts.</span></span>

    ```
    Data factory name “ADFTutorialDataFactoryPSH” is not available
    ```
* <span data-ttu-id="7ef6e-179">To create Data Factory instances, you must be a contributor or administrator of the Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-179">To create Data Factory instances, you must be a contributor or administrator of the Azure subscription.</span></span>
* <span data-ttu-id="7ef6e-180">The name of the data factory may be registered as a DNS name in the future, and hence become publicly visible.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-180">The name of the data factory may be registered as a DNS name in the future, and hence become publicly visible.</span></span>
* <span data-ttu-id="7ef6e-181">You may receive the following error: "**This subscription is not registered to use namespace Microsoft.DataFactory.**"</span><span class="sxs-lookup"><span data-stu-id="7ef6e-181">You may receive the following error: "**This subscription is not registered to use namespace Microsoft.DataFactory.**"</span></span> <span data-ttu-id="7ef6e-182">Do one of the following, and try publishing again:</span><span class="sxs-lookup"><span data-stu-id="7ef6e-182">Do one of the following, and try publishing again:</span></span>

  * <span data-ttu-id="7ef6e-183">In Azure PowerShell, run the following command to register the Data Factory provider:</span><span class="sxs-lookup"><span data-stu-id="7ef6e-183">In Azure PowerShell, run the following command to register the Data Factory provider:</span></span>

    ```PowerShell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```

    <span data-ttu-id="7ef6e-184">Run the following command to confirm that the Data Factory provider is registered:</span><span class="sxs-lookup"><span data-stu-id="7ef6e-184">Run the following command to confirm that the Data Factory provider is registered:</span></span>

    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="7ef6e-185">Sign in by using the Azure subscription to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7ef6e-185">Sign in by using the Azure subscription to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="7ef6e-186">Go to a Data Factory blade, or create a data factory in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-186">Go to a Data Factory blade, or create a data factory in the Azure portal.</span></span> <span data-ttu-id="7ef6e-187">This action automatically registers the provider for you.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-187">This action automatically registers the provider for you.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="7ef6e-188">Create linked services</span><span class="sxs-lookup"><span data-stu-id="7ef6e-188">Create linked services</span></span>
<span data-ttu-id="7ef6e-189">You create linked services in a data factory to link your data stores and compute services to the data factory.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-189">You create linked services in a data factory to link your data stores and compute services to the data factory.</span></span> <span data-ttu-id="7ef6e-190">In this tutorial, you don't use any compute service such as Azure HDInsight or Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-190">In this tutorial, you don't use any compute service such as Azure HDInsight or Azure Data Lake Analytics.</span></span> <span data-ttu-id="7ef6e-191">You use two data stores of type Azure Storage (source) and Azure SQL Database (destination).</span><span class="sxs-lookup"><span data-stu-id="7ef6e-191">You use two data stores of type Azure Storage (source) and Azure SQL Database (destination).</span></span> 

<span data-ttu-id="7ef6e-192">Therefore, you create two linked services named AzureStorageLinkedService and AzureSqlLinkedService of types: AzureStorage and AzureSqlDatabase.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-192">Therefore, you create two linked services named AzureStorageLinkedService and AzureSqlLinkedService of types: AzureStorage and AzureSqlDatabase.</span></span>  

<span data-ttu-id="7ef6e-193">The AzureStorageLinkedService links your Azure storage account to the data factory.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-193">The AzureStorageLinkedService links your Azure storage account to the data factory.</span></span> <span data-ttu-id="7ef6e-194">This storage account is the one in which you created a container and uploaded the data as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="7ef6e-194">This storage account is the one in which you created a container and uploaded the data as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

<span data-ttu-id="7ef6e-195">AzureSqlLinkedService links your Azure SQL database to the data factory.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-195">AzureSqlLinkedService links your Azure SQL database to the data factory.</span></span> <span data-ttu-id="7ef6e-196">The data that is copied from the blob storage is stored in this database.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-196">The data that is copied from the blob storage is stored in this database.</span></span> <span data-ttu-id="7ef6e-197">You created the emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="7ef6e-197">You created the emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> 

### <a name="create-a-linked-service-for-an-azure-storage-account"></a><span data-ttu-id="7ef6e-198">Create a linked service for an Azure storage account</span><span class="sxs-lookup"><span data-stu-id="7ef6e-198">Create a linked service for an Azure storage account</span></span>
<span data-ttu-id="7ef6e-199">In this step, you link your Azure storage account to your data factory.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-199">In this step, you link your Azure storage account to your data factory.</span></span>

1. <span data-ttu-id="7ef6e-200">Create a JSON file named **AzureStorageLinkedService.json** in **C:\ADFGetStartedPSH** folder with the following content: (Create the folder ADFGetStartedPSH if it does not already exist.)</span><span class="sxs-lookup"><span data-stu-id="7ef6e-200">Create a JSON file named **AzureStorageLinkedService.json** in **C:\ADFGetStartedPSH** folder with the following content: (Create the folder ADFGetStartedPSH if it does not already exist.)</span></span>

    > [!IMPORTANT]
    > Replace &lt;accountname&gt; and &lt;accountkey&gt; with name and key of your Azure storage account before saving the file. 

    ```json
    {
        "name": "AzureStorageLinkedService",
        "properties": {
            "type": "AzureStorage",
            "typeProperties": {
                "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
            }
        }
     }
    ``` 
1. <span data-ttu-id="7ef6e-202">In **Azure PowerShell**, switch to the **ADFGetStartedPSH** folder.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-202">In **Azure PowerShell**, switch to the **ADFGetStartedPSH** folder.</span></span>
1. <span data-ttu-id="7ef6e-203">Run the **New-AzureRmDataFactoryLinkedService** cmdlet to create the linked service: **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-203">Run the **New-AzureRmDataFactoryLinkedService** cmdlet to create the linked service: **AzureStorageLinkedService**.</span></span> <span data-ttu-id="7ef6e-204">This cmdlet, and other Data Factory cmdlets you use in this tutorial requires you to pass values for the **ResourceGroupName** and **DataFactoryName** parameters.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-204">This cmdlet, and other Data Factory cmdlets you use in this tutorial requires you to pass values for the **ResourceGroupName** and **DataFactoryName** parameters.</span></span> <span data-ttu-id="7ef6e-205">Alternatively, you can pass the DataFactory object returned by the New-AzureRmDataFactory cmdlet without typing ResourceGroupName and DataFactoryName each time you run a cmdlet.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-205">Alternatively, you can pass the DataFactory object returned by the New-AzureRmDataFactory cmdlet without typing ResourceGroupName and DataFactoryName each time you run a cmdlet.</span></span> 

    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\AzureStorageLinkedService.json
    ```
    <span data-ttu-id="7ef6e-206">Here is the sample output:</span><span class="sxs-lookup"><span data-stu-id="7ef6e-206">Here is the sample output:</span></span>

    ```
    LinkedServiceName : AzureStorageLinkedService
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Properties        : Microsoft.Azure.Management.DataFactories.Models.LinkedServiceProperties
    ProvisioningState : Succeeded
    ``` 

    <span data-ttu-id="7ef6e-207">Other way of creating this linked service is to specify resource group name and data factory name instead of specifying the DataFactory object.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-207">Other way of creating this linked service is to specify resource group name and data factory name instead of specifying the DataFactory object.</span></span>  

    ```PowerShell
    New-AzureRmDataFactoryLinkedService -ResourceGroupName ADFTutorialResourceGroup -DataFactoryName <Name of your data factory> -File .\AzureStorageLinkedService.json
    ```

### <a name="create-a-linked-service-for-an-azure-sql-database"></a><span data-ttu-id="7ef6e-208">Create a linked service for an Azure SQL database</span><span class="sxs-lookup"><span data-stu-id="7ef6e-208">Create a linked service for an Azure SQL database</span></span>
<span data-ttu-id="7ef6e-209">In this step, you link your Azure SQL database to your data factory.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-209">In this step, you link your Azure SQL database to your data factory.</span></span>

1. <span data-ttu-id="7ef6e-210">Create a JSON file named AzureSqlLinkedService.json in C:\ADFGetStartedPSH folder with the following content:</span><span class="sxs-lookup"><span data-stu-id="7ef6e-210">Create a JSON file named AzureSqlLinkedService.json in C:\ADFGetStartedPSH folder with the following content:</span></span>

    > [!IMPORTANT]
    > Replace &lt;servername&gt;, &lt;databasename&gt;, &lt;username@servername&gt;, and &lt;password&gt; with names of your Azure SQL server, database, user account, and password.
    
    ```json
    {
        "name": "AzureSqlLinkedService",
        "properties": {
            "type": "AzureSqlDatabase",
            "typeProperties": {
                "connectionString": "Server=tcp:<server>.database.windows.net,1433;Database=<databasename>;User ID=<user>@<server>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
            }
        }
     }
    ```
1. <span data-ttu-id="7ef6e-212">Run the following command to create a linked service:</span><span class="sxs-lookup"><span data-stu-id="7ef6e-212">Run the following command to create a linked service:</span></span>

    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\AzureSqlLinkedService.json
    ```
    
    <span data-ttu-id="7ef6e-213">Here is the sample output:</span><span class="sxs-lookup"><span data-stu-id="7ef6e-213">Here is the sample output:</span></span>

    ```
    LinkedServiceName : AzureSqlLinkedService
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Properties        : Microsoft.Azure.Management.DataFactories.Models.LinkedServiceProperties
    ProvisioningState : Succeeded
    ```

   <span data-ttu-id="7ef6e-214">Confirm that **Allow access to Azure services** setting is turned on for your SQL database server.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-214">Confirm that **Allow access to Azure services** setting is turned on for your SQL database server.</span></span> <span data-ttu-id="7ef6e-215">To verify and turn it on, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="7ef6e-215">To verify and turn it on, do the following steps:</span></span>

    1. <span data-ttu-id="7ef6e-216">Log in to the [Azure portal](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="7ef6e-216">Log in to the [Azure portal](https://portal.azure.com)</span></span>
    1. <span data-ttu-id="7ef6e-217">Click **More services >** on the left, and click **SQL servers** in the **DATABASES** category.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-217">Click **More services >** on the left, and click **SQL servers** in the **DATABASES** category.</span></span>
    1. <span data-ttu-id="7ef6e-218">Select your server in the list of SQL servers.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-218">Select your server in the list of SQL servers.</span></span>
    1. <span data-ttu-id="7ef6e-219">On the SQL server blade, click **Show firewall settings** link.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-219">On the SQL server blade, click **Show firewall settings** link.</span></span>
    1. <span data-ttu-id="7ef6e-220">In the **Firewall settings** blade, click **ON** for **Allow access to Azure services**.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-220">In the **Firewall settings** blade, click **ON** for **Allow access to Azure services**.</span></span>
    1. <span data-ttu-id="7ef6e-221">Click **Save** on the toolbar.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-221">Click **Save** on the toolbar.</span></span> 

## <a name="create-datasets"></a><span data-ttu-id="7ef6e-222">Create datasets</span><span class="sxs-lookup"><span data-stu-id="7ef6e-222">Create datasets</span></span>
<span data-ttu-id="7ef6e-223">In the previous step, you created linked services to link your Azure Storage account and Azure SQL database to your data factory.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-223">In the previous step, you created linked services to link your Azure Storage account and Azure SQL database to your data factory.</span></span> <span data-ttu-id="7ef6e-224">In this step, you define two datasets named InputDataset and OutputDataset that represent input and output data that is stored in the data stores referred by AzureStorageLinkedService and AzureSqlLinkedService respectively.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-224">In this step, you define two datasets named InputDataset and OutputDataset that represent input and output data that is stored in the data stores referred by AzureStorageLinkedService and AzureSqlLinkedService respectively.</span></span>

<span data-ttu-id="7ef6e-225">The Azure storage linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-225">The Azure storage linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure storage account.</span></span> <span data-ttu-id="7ef6e-226">And, the input blob dataset (InputDataset) specifies the container and the folder that contains the input data.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-226">And, the input blob dataset (InputDataset) specifies the container and the folder that contains the input data.</span></span>  

<span data-ttu-id="7ef6e-227">Similarly, the Azure SQL Database linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-227">Similarly, the Azure SQL Database linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure SQL database.</span></span> <span data-ttu-id="7ef6e-228">And, the output SQL table dataset (OututDataset) specifies the table in the database to which the data from the blob storage is copied.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-228">And, the output SQL table dataset (OututDataset) specifies the table in the database to which the data from the blob storage is copied.</span></span> 

### <a name="create-an-input-dataset"></a><span data-ttu-id="7ef6e-229">Create an input dataset</span><span class="sxs-lookup"><span data-stu-id="7ef6e-229">Create an input dataset</span></span>
<span data-ttu-id="7ef6e-230">In this step, you create a dataset named InputDataset that points to a blob file (emp.txt) in the root folder of a blob container (adftutorial) in the Azure Storage represented by the AzureStorageLinkedService linked service.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-230">In this step, you create a dataset named InputDataset that points to a blob file (emp.txt) in the root folder of a blob container (adftutorial) in the Azure Storage represented by the AzureStorageLinkedService linked service.</span></span> <span data-ttu-id="7ef6e-231">If you don't specify a value for the fileName (or skip it), data from all blobs in the input folder are copied to the destination.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-231">If you don't specify a value for the fileName (or skip it), data from all blobs in the input folder are copied to the destination.</span></span> <span data-ttu-id="7ef6e-232">In this tutorial, you specify a value for the fileName.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-232">In this tutorial, you specify a value for the fileName.</span></span>  

1. <span data-ttu-id="7ef6e-233">Create a JSON file named **InputDataset.json** in the **C:\ADFGetStartedPSH** folder, with the following content:</span><span class="sxs-lookup"><span data-stu-id="7ef6e-233">Create a JSON file named **InputDataset.json** in the **C:\ADFGetStartedPSH** folder, with the following content:</span></span>

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
                "fileName": "emp.txt",
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

    <span data-ttu-id="7ef6e-234">The following table provides descriptions for the JSON properties used in the snippet:</span><span class="sxs-lookup"><span data-stu-id="7ef6e-234">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

    | <span data-ttu-id="7ef6e-235">Property</span><span class="sxs-lookup"><span data-stu-id="7ef6e-235">Property</span></span> | <span data-ttu-id="7ef6e-236">Description</span><span class="sxs-lookup"><span data-stu-id="7ef6e-236">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="7ef6e-237">type</span><span class="sxs-lookup"><span data-stu-id="7ef6e-237">type</span></span> | <span data-ttu-id="7ef6e-238">The type property is set to **AzureBlob** because data resides in an Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-238">The type property is set to **AzureBlob** because data resides in an Azure blob storage.</span></span> |
    | <span data-ttu-id="7ef6e-239">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="7ef6e-239">linkedServiceName</span></span> | <span data-ttu-id="7ef6e-240">Refers to the **AzureStorageLinkedService** that you created earlier.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-240">Refers to the **AzureStorageLinkedService** that you created earlier.</span></span> |
    | <span data-ttu-id="7ef6e-241">folderPath</span><span class="sxs-lookup"><span data-stu-id="7ef6e-241">folderPath</span></span> | <span data-ttu-id="7ef6e-242">Specifies the blob **container** and the **folder** that contains input blobs.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-242">Specifies the blob **container** and the **folder** that contains input blobs.</span></span> <span data-ttu-id="7ef6e-243">In this tutorial, adftutorial is the blob container and folder is the root folder.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-243">In this tutorial, adftutorial is the blob container and folder is the root folder.</span></span> | 
    | <span data-ttu-id="7ef6e-244">fileName</span><span class="sxs-lookup"><span data-stu-id="7ef6e-244">fileName</span></span> | <span data-ttu-id="7ef6e-245">This property is optional.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-245">This property is optional.</span></span> <span data-ttu-id="7ef6e-246">If you omit this property, all files from the folderPath are picked.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-246">If you omit this property, all files from the folderPath are picked.</span></span> <span data-ttu-id="7ef6e-247">In this tutorial, **emp.txt** is specified for the fileName, so only that file is picked up for processing.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-247">In this tutorial, **emp.txt** is specified for the fileName, so only that file is picked up for processing.</span></span> |
    | <span data-ttu-id="7ef6e-248">format -> type</span><span class="sxs-lookup"><span data-stu-id="7ef6e-248">format -> type</span></span> |<span data-ttu-id="7ef6e-249">The input file is in the text format, so we use **TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-249">The input file is in the text format, so we use **TextFormat**.</span></span> |
    | <span data-ttu-id="7ef6e-250">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="7ef6e-250">columnDelimiter</span></span> | <span data-ttu-id="7ef6e-251">The columns in the input file are delimited by **comma character (`,`)**.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-251">The columns in the input file are delimited by **comma character (`,`)**.</span></span> |
    | <span data-ttu-id="7ef6e-252">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="7ef6e-252">frequency/interval</span></span> | <span data-ttu-id="7ef6e-253">The frequency is set to **Hour** and interval is  set to **1**, which means that the input slices are available **hourly**.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-253">The frequency is set to **Hour** and interval is  set to **1**, which means that the input slices are available **hourly**.</span></span> <span data-ttu-id="7ef6e-254">In other words, the Data Factory service looks for input data every hour in the root folder of blob container (**adftutorial**) you specified.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-254">In other words, the Data Factory service looks for input data every hour in the root folder of blob container (**adftutorial**) you specified.</span></span> <span data-ttu-id="7ef6e-255">It looks for the data within the pipeline start and end times, not before or after these times.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-255">It looks for the data within the pipeline start and end times, not before or after these times.</span></span>  |
    | <span data-ttu-id="7ef6e-256">external</span><span class="sxs-lookup"><span data-stu-id="7ef6e-256">external</span></span> | <span data-ttu-id="7ef6e-257">This property is set to **true** if the data is not generated by this pipeline.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-257">This property is set to **true** if the data is not generated by this pipeline.</span></span> <span data-ttu-id="7ef6e-258">The input data in this tutorial is in the emp.txt file, which is not generated by this pipeline, so we set this property to true.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-258">The input data in this tutorial is in the emp.txt file, which is not generated by this pipeline, so we set this property to true.</span></span> |

    <span data-ttu-id="7ef6e-259">For more information about these JSON properties, see [Azure Blob connector article](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="7ef6e-259">For more information about these JSON properties, see [Azure Blob connector article](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
1. <span data-ttu-id="7ef6e-260">Run the following command to create the Data Factory dataset.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-260">Run the following command to create the Data Factory dataset.</span></span>

    ```PowerShell  
    New-AzureRmDataFactoryDataset $df -File .\InputDataset.json
    ```
    <span data-ttu-id="7ef6e-261">Here is the sample output:</span><span class="sxs-lookup"><span data-stu-id="7ef6e-261">Here is the sample output:</span></span>

    ```
    DatasetName       : InputDataset
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Availability      : Microsoft.Azure.Management.DataFactories.Common.Models.Availability
    Location          : Microsoft.Azure.Management.DataFactories.Models.AzureBlobDataset
    Policy            : Microsoft.Azure.Management.DataFactories.Common.Models.Policy
    Structure         : {FirstName, LastName}
    Properties        : Microsoft.Azure.Management.DataFactories.Models.DatasetProperties
    ProvisioningState : Succeeded
    ```

### <a name="create-an-output-dataset"></a><span data-ttu-id="7ef6e-262">Create an output dataset</span><span class="sxs-lookup"><span data-stu-id="7ef6e-262">Create an output dataset</span></span>
<span data-ttu-id="7ef6e-263">In this part of the step, you create an output dataset named **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-263">In this part of the step, you create an output dataset named **OutputDataset**.</span></span> <span data-ttu-id="7ef6e-264">This dataset points to a SQL table in the Azure SQL database represented by **AzureSqlLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-264">This dataset points to a SQL table in the Azure SQL database represented by **AzureSqlLinkedService**.</span></span> 

1. <span data-ttu-id="7ef6e-265">Create a JSON file named **OutputDataset.json** in the **C:\ADFGetStartedPSH** folder with the following content:</span><span class="sxs-lookup"><span data-stu-id="7ef6e-265">Create a JSON file named **OutputDataset.json** in the **C:\ADFGetStartedPSH** folder with the following content:</span></span>

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

    <span data-ttu-id="7ef6e-266">The following table provides descriptions for the JSON properties used in the snippet:</span><span class="sxs-lookup"><span data-stu-id="7ef6e-266">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

    | <span data-ttu-id="7ef6e-267">Property</span><span class="sxs-lookup"><span data-stu-id="7ef6e-267">Property</span></span> | <span data-ttu-id="7ef6e-268">Description</span><span class="sxs-lookup"><span data-stu-id="7ef6e-268">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="7ef6e-269">type</span><span class="sxs-lookup"><span data-stu-id="7ef6e-269">type</span></span> | <span data-ttu-id="7ef6e-270">The type property is set to **AzureSqlTable** because data is copied to a table in an Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-270">The type property is set to **AzureSqlTable** because data is copied to a table in an Azure SQL database.</span></span> |
    | <span data-ttu-id="7ef6e-271">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="7ef6e-271">linkedServiceName</span></span> | <span data-ttu-id="7ef6e-272">Refers to the **AzureSqlLinkedService** that you created earlier.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-272">Refers to the **AzureSqlLinkedService** that you created earlier.</span></span> |
    | <span data-ttu-id="7ef6e-273">tableName</span><span class="sxs-lookup"><span data-stu-id="7ef6e-273">tableName</span></span> | <span data-ttu-id="7ef6e-274">Specified the **table** to which the data is copied.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-274">Specified the **table** to which the data is copied.</span></span> | 
    | <span data-ttu-id="7ef6e-275">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="7ef6e-275">frequency/interval</span></span> | <span data-ttu-id="7ef6e-276">The frequency is set to **Hour** and interval is **1**, which means that the output slices are produced **hourly** between the pipeline start and end times, not before or after these times.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-276">The frequency is set to **Hour** and interval is **1**, which means that the output slices are produced **hourly** between the pipeline start and end times, not before or after these times.</span></span>  |

    <span data-ttu-id="7ef6e-277">There are three columns – **ID**, **FirstName**, and **LastName** – in the emp table in the database.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-277">There are three columns – **ID**, **FirstName**, and **LastName** – in the emp table in the database.</span></span> <span data-ttu-id="7ef6e-278">ID is an identity column, so you need to specify only **FirstName** and **LastName** here.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-278">ID is an identity column, so you need to specify only **FirstName** and **LastName** here.</span></span>

    <span data-ttu-id="7ef6e-279">For more information about these JSON properties, see [Azure SQL connector article](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="7ef6e-279">For more information about these JSON properties, see [Azure SQL connector article](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
1. <span data-ttu-id="7ef6e-280">Run the following command to create the data factory dataset.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-280">Run the following command to create the data factory dataset.</span></span>

    ```PowerShell   
    New-AzureRmDataFactoryDataset $df -File .\OutputDataset.json
    ```

    <span data-ttu-id="7ef6e-281">Here is the sample output:</span><span class="sxs-lookup"><span data-stu-id="7ef6e-281">Here is the sample output:</span></span>

    ```
    DatasetName       : OutputDataset
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Availability      : Microsoft.Azure.Management.DataFactories.Common.Models.Availability
    Location          : Microsoft.Azure.Management.DataFactories.Models.AzureSqlTableDataset
    Policy            :
    Structure         : {FirstName, LastName}
    Properties        : Microsoft.Azure.Management.DataFactories.Models.DatasetProperties
    ProvisioningState : Succeeded
    ```

## <a name="create-a-pipeline"></a><span data-ttu-id="7ef6e-282">Create a pipeline</span><span class="sxs-lookup"><span data-stu-id="7ef6e-282">Create a pipeline</span></span>
<span data-ttu-id="7ef6e-283">In this step, you create a pipeline with a **copy activity** that uses **InputDataset** as an input and **OutputDataset** as an output.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-283">In this step, you create a pipeline with a **copy activity** that uses **InputDataset** as an input and **OutputDataset** as an output.</span></span>

<span data-ttu-id="7ef6e-284">Currently, output dataset is what drives the schedule.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-284">Currently, output dataset is what drives the schedule.</span></span> <span data-ttu-id="7ef6e-285">In this tutorial, output dataset is configured to produce a slice once an hour.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-285">In this tutorial, output dataset is configured to produce a slice once an hour.</span></span> <span data-ttu-id="7ef6e-286">The pipeline has a start time and end time that are one day apart, which is 24 hours.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-286">The pipeline has a start time and end time that are one day apart, which is 24 hours.</span></span> <span data-ttu-id="7ef6e-287">Therefore, 24 slices of output dataset are produced by the pipeline.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-287">Therefore, 24 slices of output dataset are produced by the pipeline.</span></span> 


1. <span data-ttu-id="7ef6e-288">Create a JSON file named **ADFTutorialPipeline.json** in the **C:\ADFGetStartedPSH** folder, with the following content:</span><span class="sxs-lookup"><span data-stu-id="7ef6e-288">Create a JSON file named **ADFTutorialPipeline.json** in the **C:\ADFGetStartedPSH** folder, with the following content:</span></span>

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
    <span data-ttu-id="7ef6e-289">Note the following points:</span><span class="sxs-lookup"><span data-stu-id="7ef6e-289">Note the following points:</span></span>
   
    - <span data-ttu-id="7ef6e-290">In the activities section, there is only one activity whose **type** is set to **Copy**.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-290">In the activities section, there is only one activity whose **type** is set to **Copy**.</span></span> <span data-ttu-id="7ef6e-291">For more information about the copy activity, see [data movement activities](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="7ef6e-291">For more information about the copy activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="7ef6e-292">In Data Factory solutions, you can also use [data transformation activities](data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="7ef6e-292">In Data Factory solutions, you can also use [data transformation activities](data-factory-data-transformation-activities.md).</span></span>
    - <span data-ttu-id="7ef6e-293">Input for the activity is set to **InputDataset** and output for the activity is set to **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-293">Input for the activity is set to **InputDataset** and output for the activity is set to **OutputDataset**.</span></span> 
    - <span data-ttu-id="7ef6e-294">In the **typeProperties** section, **BlobSource** is specified as the source type and **SqlSink** is specified as the sink type.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-294">In the **typeProperties** section, **BlobSource** is specified as the source type and **SqlSink** is specified as the sink type.</span></span> <span data-ttu-id="7ef6e-295">For a complete list of data stores supported by the copy activity as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="7ef6e-295">For a complete list of data stores supported by the copy activity as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="7ef6e-296">To learn how to use a specific supported data store as a source/sink, click the link in the table.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-296">To learn how to use a specific supported data store as a source/sink, click the link in the table.</span></span>  
     
    <span data-ttu-id="7ef6e-297">Replace the value of the **start** property with the current day and **end** value with the next day.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-297">Replace the value of the **start** property with the current day and **end** value with the next day.</span></span> <span data-ttu-id="7ef6e-298">You can specify only the date part and skip the time part of the date time.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-298">You can specify only the date part and skip the time part of the date time.</span></span> <span data-ttu-id="7ef6e-299">For example, "2016-02-03", which is equivalent to "2016-02-03T00:00:00Z"</span><span class="sxs-lookup"><span data-stu-id="7ef6e-299">For example, "2016-02-03", which is equivalent to "2016-02-03T00:00:00Z"</span></span>
     
    <span data-ttu-id="7ef6e-300">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="7ef6e-300">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="7ef6e-301">For example: 2016-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-301">For example: 2016-10-14T16:32:41Z.</span></span> <span data-ttu-id="7ef6e-302">The **end** time is optional, but we use it in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-302">The **end** time is optional, but we use it in this tutorial.</span></span> 
     
    <span data-ttu-id="7ef6e-303">If you do not specify value for the **end** property, it is calculated as "**start + 48 hours**".</span><span class="sxs-lookup"><span data-stu-id="7ef6e-303">If you do not specify value for the **end** property, it is calculated as "**start + 48 hours**".</span></span> <span data-ttu-id="7ef6e-304">To run the pipeline indefinitely, specify **9999-09-09** as the value for the **end** property.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-304">To run the pipeline indefinitely, specify **9999-09-09** as the value for the **end** property.</span></span>
     
    <span data-ttu-id="7ef6e-305">In the preceding example, there are 24 data slices as each data slice is produced hourly.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-305">In the preceding example, there are 24 data slices as each data slice is produced hourly.</span></span>

    <span data-ttu-id="7ef6e-306">For descriptions of JSON properties in a pipeline definition, see [create pipelines](data-factory-create-pipelines.md) article.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-306">For descriptions of JSON properties in a pipeline definition, see [create pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="7ef6e-307">For descriptions of JSON properties in a copy activity definition, see [data movement activities](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="7ef6e-307">For descriptions of JSON properties in a copy activity definition, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="7ef6e-308">For descriptions of JSON properties supported by BlobSource, see [Azure Blob connector article](data-factory-azure-blob-connector.md).</span><span class="sxs-lookup"><span data-stu-id="7ef6e-308">For descriptions of JSON properties supported by BlobSource, see [Azure Blob connector article](data-factory-azure-blob-connector.md).</span></span> <span data-ttu-id="7ef6e-309">For descriptions of JSON properties supported by SqlSink, see [Azure SQL Database connector article](data-factory-azure-sql-connector.md).</span><span class="sxs-lookup"><span data-stu-id="7ef6e-309">For descriptions of JSON properties supported by SqlSink, see [Azure SQL Database connector article](data-factory-azure-sql-connector.md).</span></span>
1. <span data-ttu-id="7ef6e-310">Run the following command to create the data factory table.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-310">Run the following command to create the data factory table.</span></span>

    ```PowerShell   
    New-AzureRmDataFactoryPipeline $df -File .\ADFTutorialPipeline.json
    ```

    <span data-ttu-id="7ef6e-311">Here is the sample output:</span><span class="sxs-lookup"><span data-stu-id="7ef6e-311">Here is the sample output:</span></span> 

    ```
    PipelineName      : ADFTutorialPipeline
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Properties        : Microsoft.Azure.Management.DataFactories.Models.PipelinePropertie
    ProvisioningState : Succeeded
    ```

<span data-ttu-id="7ef6e-312">**Congratulations!**</span><span class="sxs-lookup"><span data-stu-id="7ef6e-312">**Congratulations!**</span></span> <span data-ttu-id="7ef6e-313">You have successfully created an Azure data factory with a pipeline to copy data from an Azure blob storage to an Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-313">You have successfully created an Azure data factory with a pipeline to copy data from an Azure blob storage to an Azure SQL database.</span></span> 

## <a name="monitor-the-pipeline"></a><span data-ttu-id="7ef6e-314">Monitor the pipeline</span><span class="sxs-lookup"><span data-stu-id="7ef6e-314">Monitor the pipeline</span></span>
<span data-ttu-id="7ef6e-315">In this step, you use Azure PowerShell to monitor what’s going on in an Azure data factory.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-315">In this step, you use Azure PowerShell to monitor what’s going on in an Azure data factory.</span></span>

1. <span data-ttu-id="7ef6e-316">Replace &lt;DataFactoryName&gt; with the name of your data factory and run **Get-AzureRmDataFactory**, and assign the output to a variable $df.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-316">Replace &lt;DataFactoryName&gt; with the name of your data factory and run **Get-AzureRmDataFactory**, and assign the output to a variable $df.</span></span>

    ```PowerShell  
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name <DataFactoryName>
    ```

    <span data-ttu-id="7ef6e-317">For example:</span><span class="sxs-lookup"><span data-stu-id="7ef6e-317">For example:</span></span>
    ```PowerShell
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name ADFTutorialDataFactoryPSH0516
    ```
    
    <span data-ttu-id="7ef6e-318">Then, run print the contents of $df to see the following output:</span><span class="sxs-lookup"><span data-stu-id="7ef6e-318">Then, run print the contents of $df to see the following output:</span></span> 
    
    ```
    PS C:\ADFGetStartedPSH> $df
    
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    DataFactoryId     : 6f194b34-03b3-49ab-8f03-9f8a7b9d3e30
    ResourceGroupName : ADFTutorialResourceGroup
    Location          : West US
    Tags              : {}
    Properties        : Microsoft.Azure.Management.DataFactories.Models.DataFactoryProperties
    ProvisioningState : Succeeded
    ```
1. <span data-ttu-id="7ef6e-319">Run **Get-AzureRmDataFactorySlice** to get details about all slices of the **OutputDataset**, which is the output dataset of the pipeline.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-319">Run **Get-AzureRmDataFactorySlice** to get details about all slices of the **OutputDataset**, which is the output dataset of the pipeline.</span></span>  

    ```PowerShell   
    Get-AzureRmDataFactorySlice $df -DatasetName OutputDataset -StartDateTime 2017-05-11T00:00:00Z
    ```

   <span data-ttu-id="7ef6e-320">This setting should match the **Start** value in the pipeline JSON.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-320">This setting should match the **Start** value in the pipeline JSON.</span></span> <span data-ttu-id="7ef6e-321">You should see 24 slices, one for each hour from 12 AM of the current day to 12 AM of the next day.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-321">You should see 24 slices, one for each hour from 12 AM of the current day to 12 AM of the next day.</span></span>

   <span data-ttu-id="7ef6e-322">Here are three sample slices from the output:</span><span class="sxs-lookup"><span data-stu-id="7ef6e-322">Here are three sample slices from the output:</span></span> 

    ``` 
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    DatasetName       : OutputDataset
    Start             : 5/11/2017 11:00:00 PM
    End               : 5/12/2017 12:00:00 AM
    RetryCount        : 0
    State             : Ready
    SubState          :
    LatencyStatus     :
    LongRetryCount    : 0

    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    DatasetName       : OutputDataset
    Start             : 5/11/2017 9:00:00 PM
    End               : 5/11/2017 10:00:00 PM
    RetryCount        : 0
    State             : InProgress
    SubState          :
    LatencyStatus     :
    LongRetryCount    : 0   

    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    DatasetName       : OutputDataset
    Start             : 5/11/2017 8:00:00 PM
    End               : 5/11/2017 9:00:00 PM
    RetryCount        : 0
    State             : Waiting
    SubState          : ConcurrencyLimit
    LatencyStatus     :
    LongRetryCount    : 0
    ```
1. <span data-ttu-id="7ef6e-323">Run **Get-AzureRmDataFactoryRun** to get the details of activity runs for a **specific** slice.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-323">Run **Get-AzureRmDataFactoryRun** to get the details of activity runs for a **specific** slice.</span></span> <span data-ttu-id="7ef6e-324">Copy the date-time value from the output of the previous command to specify the value for the StartDateTime parameter.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-324">Copy the date-time value from the output of the previous command to specify the value for the StartDateTime parameter.</span></span> 

    ```PowerShell  
    Get-AzureRmDataFactoryRun $df -DatasetName OutputDataset -StartDateTime "5/11/2017 09:00:00 PM"
    ```

   <span data-ttu-id="7ef6e-325">Here is the sample output:</span><span class="sxs-lookup"><span data-stu-id="7ef6e-325">Here is the sample output:</span></span> 

    ```
    Id                  : c0ddbd75-d0c7-4816-a775-704bbd7c7eab_636301332000000000_636301368000000000_OutputDataset
    ResourceGroupName   : ADFTutorialResourceGroup
    DataFactoryName     : ADFTutorialDataFactoryPSH0516
    DatasetName         : OutputDataset
    ProcessingStartTime : 5/16/2017 8:00:33 PM
    ProcessingEndTime   : 5/16/2017 8:01:36 PM
    PercentComplete     : 100
    DataSliceStart      : 5/11/2017 9:00:00 PM
    DataSliceEnd        : 5/11/2017 10:00:00 PM
    Status              : Succeeded
    Timestamp           : 5/16/2017 8:00:33 PM
    RetryAttempt        : 0
    Properties          : {}
    ErrorMessage        :
    ActivityName        : CopyFromBlobToSQL
    PipelineName        : ADFTutorialPipeline
    Type                : Copy  
    ```

<span data-ttu-id="7ef6e-326">For comprehensive documentation on Data Factory cmdlets, see [Data Factory Cmdlet Reference](/powershell/module/azurerm.datafactories).</span><span class="sxs-lookup"><span data-stu-id="7ef6e-326">For comprehensive documentation on Data Factory cmdlets, see [Data Factory Cmdlet Reference](/powershell/module/azurerm.datafactories).</span></span>

## <a name="summary"></a><span data-ttu-id="7ef6e-327">Summary</span><span class="sxs-lookup"><span data-stu-id="7ef6e-327">Summary</span></span>
<span data-ttu-id="7ef6e-328">In this tutorial, you created an Azure data factory to copy data from an Azure blob to an Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-328">In this tutorial, you created an Azure data factory to copy data from an Azure blob to an Azure SQL database.</span></span> <span data-ttu-id="7ef6e-329">You used PowerShell to create the data factory, linked services, datasets, and a pipeline.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-329">You used PowerShell to create the data factory, linked services, datasets, and a pipeline.</span></span> <span data-ttu-id="7ef6e-330">Here are the high-level steps you performed in this tutorial:</span><span class="sxs-lookup"><span data-stu-id="7ef6e-330">Here are the high-level steps you performed in this tutorial:</span></span>  

1. <span data-ttu-id="7ef6e-331">Created an Azure **data factory**.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-331">Created an Azure **data factory**.</span></span>
1. <span data-ttu-id="7ef6e-332">Created **linked services**:</span><span class="sxs-lookup"><span data-stu-id="7ef6e-332">Created **linked services**:</span></span>

   <span data-ttu-id="7ef6e-333">a.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-333">a.</span></span> <span data-ttu-id="7ef6e-334">An **Azure Storage** linked service to link your Azure storage account that holds input data.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-334">An **Azure Storage** linked service to link your Azure storage account that holds input data.</span></span>     
   <span data-ttu-id="7ef6e-335">b.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-335">b.</span></span> <span data-ttu-id="7ef6e-336">An **Azure SQL** linked service to link your SQL database that holds the output data.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-336">An **Azure SQL** linked service to link your SQL database that holds the output data.</span></span>
1. <span data-ttu-id="7ef6e-337">Created **datasets** that describe input data and output data for pipelines.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-337">Created **datasets** that describe input data and output data for pipelines.</span></span>
1. <span data-ttu-id="7ef6e-338">Created a **pipeline** with **Copy Activity**, with **BlobSource** as the source and **SqlSink** as the sink.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-338">Created a **pipeline** with **Copy Activity**, with **BlobSource** as the source and **SqlSink** as the sink.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7ef6e-339">Next steps</span><span class="sxs-lookup"><span data-stu-id="7ef6e-339">Next steps</span></span>
<span data-ttu-id="7ef6e-340">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-340">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="7ef6e-341">The following table provides a list of data stores supported as sources and destinations by the copy activity:</span><span class="sxs-lookup"><span data-stu-id="7ef6e-341">The following table provides a list of data stores supported as sources and destinations by the copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="7ef6e-342">To learn about how to copy data to/from a data store, click the link for the data store in the table.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-342">To learn about how to copy data to/from a data store, click the link for the data store in the table.</span></span> 

