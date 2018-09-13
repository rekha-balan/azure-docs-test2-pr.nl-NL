---
title: 'Tutorial: Create a pipeline to move data by using Azure PowerShell | Microsoft Docs'
description: In this tutorial, you create an Azure Data Factory pipeline with Copy Activity by using Azure PowerShell.
services: data-factory
documentationcenter: ''
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 71087349-9365-4e95-9847-170658216ed8
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/11/2017
ms.author: spelluru
ms.openlocfilehash: 4a11eeff91ab2d39f4456df1e943739f830c08c7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44548717"
---
# <a name="tutorial-create-a-data-factory-pipeline-that-moves-data-by-using-azure-powershell"></a><span data-ttu-id="79f4e-103">Tutorial: Create a Data Factory pipeline that moves data by using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="79f4e-103">Tutorial: Create a Data Factory pipeline that moves data by using Azure PowerShell</span></span>
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

<span data-ttu-id="79f4e-112">In this tutorial, you create and monitor an instance of Azure Data Factory by using Azure PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="79f4e-112">In this tutorial, you create and monitor an instance of Azure Data Factory by using Azure PowerShell cmdlets.</span></span> <span data-ttu-id="79f4e-113">The pipeline in the data factory you create in this tutorial uses a copy activity to copy data from an Azure blob to an Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="79f4e-113">The pipeline in the data factory you create in this tutorial uses a copy activity to copy data from an Azure blob to an Azure SQL database.</span></span>

<span data-ttu-id="79f4e-114">The Copy Activity feature performs the data movement in Data Factory.</span><span class="sxs-lookup"><span data-stu-id="79f4e-114">The Copy Activity feature performs the data movement in Data Factory.</span></span> <span data-ttu-id="79f4e-115">The activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span><span class="sxs-lookup"><span data-stu-id="79f4e-115">The activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="79f4e-116">See [Data Movement Activities](data-factory-data-movement-activities.md) for details about Copy Activity.</span><span class="sxs-lookup"><span data-stu-id="79f4e-116">See [Data Movement Activities](data-factory-data-movement-activities.md) for details about Copy Activity.</span></span>   

> [!NOTE]
> This article does not cover all the Data Factory cmdlets. See [Data Factory Cmdlet Reference](/powershell/resourcemanager/azurerm.datafactories/v2.5.0/azurerm.datafactories) for comprehensive documentation on these cmdlets.
>
> The data pipeline in this tutorial copies data from a source data store to a destination data store. It does not transform input data to produce output data. For a tutorial on how to transform data using Azure Data Factory, see [Tutorial: Build a pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).

## <a name="prerequisites"></a><span data-ttu-id="79f4e-122">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="79f4e-122">Prerequisites</span></span>
- <span data-ttu-id="79f4e-123">Go through [Tutorial Overview and Pre-requisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) to get an overview of the tutorial and complete the **prerequisite** steps.</span><span class="sxs-lookup"><span data-stu-id="79f4e-123">Go through [Tutorial Overview and Pre-requisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) to get an overview of the tutorial and complete the **prerequisite** steps.</span></span>
- <span data-ttu-id="79f4e-124">Install Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="79f4e-124">Install Azure PowerShell.</span></span> <span data-ttu-id="79f4e-125">Follow the instructions in [How to install and configure Azure PowerShell](../powershell-install-configure.md).</span><span class="sxs-lookup"><span data-stu-id="79f4e-125">Follow the instructions in [How to install and configure Azure PowerShell](../powershell-install-configure.md).</span></span>

## <a name="in-this-tutorial"></a><span data-ttu-id="79f4e-126">In this tutorial</span><span class="sxs-lookup"><span data-stu-id="79f4e-126">In this tutorial</span></span>
<span data-ttu-id="79f4e-127">The following table lists the steps you perform as part of the tutorial.</span><span class="sxs-lookup"><span data-stu-id="79f4e-127">The following table lists the steps you perform as part of the tutorial.</span></span>

| <span data-ttu-id="79f4e-128">Step</span><span class="sxs-lookup"><span data-stu-id="79f4e-128">Step</span></span> | <span data-ttu-id="79f4e-129">Description</span><span class="sxs-lookup"><span data-stu-id="79f4e-129">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="79f4e-130">Create an Azure data factory</span><span class="sxs-lookup"><span data-stu-id="79f4e-130">Create an Azure data factory</span></span>](#create-data-factory) |<span data-ttu-id="79f4e-131">In this step, you create an Azure data factory named **ADFTutorialDataFactoryPSH**.</span><span class="sxs-lookup"><span data-stu-id="79f4e-131">In this step, you create an Azure data factory named **ADFTutorialDataFactoryPSH**.</span></span> |
| [<span data-ttu-id="79f4e-132">Create linked services</span><span class="sxs-lookup"><span data-stu-id="79f4e-132">Create linked services</span></span>](#create-linked-services) |<span data-ttu-id="79f4e-133">In this step, you create two linked services: **StorageLinkedService** and **AzureSqlLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="79f4e-133">In this step, you create two linked services: **StorageLinkedService** and **AzureSqlLinkedService**.</span></span> <span data-ttu-id="79f4e-134">The StorageLinkedService links an Azure Storage service and AzureSqlLinkedService links an Azure SQL database to the ADFTutorialDataFactoryPSH.</span><span class="sxs-lookup"><span data-stu-id="79f4e-134">The StorageLinkedService links an Azure Storage service and AzureSqlLinkedService links an Azure SQL database to the ADFTutorialDataFactoryPSH.</span></span> |
| [<span data-ttu-id="79f4e-135">Create input and output datasets</span><span class="sxs-lookup"><span data-stu-id="79f4e-135">Create input and output datasets</span></span>](#create-datasets) |<span data-ttu-id="79f4e-136">In this step, you define two datasets (EmpTableFromBlob and EmpSQLTable).</span><span class="sxs-lookup"><span data-stu-id="79f4e-136">In this step, you define two datasets (EmpTableFromBlob and EmpSQLTable).</span></span> <span data-ttu-id="79f4e-137">These datasets are used as input and output tables for **Copy Activity** in the ADFTutorialPipeline that you create in the next step.</span><span class="sxs-lookup"><span data-stu-id="79f4e-137">These datasets are used as input and output tables for **Copy Activity** in the ADFTutorialPipeline that you create in the next step.</span></span> |
| [<span data-ttu-id="79f4e-138">Create and run a pipeline</span><span class="sxs-lookup"><span data-stu-id="79f4e-138">Create and run a pipeline</span></span>](#create-pipeline) |<span data-ttu-id="79f4e-139">In this step, you create a pipeline named **ADFTutorialPipeline** in the data factory ADFTutorialDataFactoryPSH.</span><span class="sxs-lookup"><span data-stu-id="79f4e-139">In this step, you create a pipeline named **ADFTutorialPipeline** in the data factory ADFTutorialDataFactoryPSH.</span></span> <span data-ttu-id="79f4e-140">The pipeline uses Copy Activity to copy data from an Azure blob to an output Azure database table.</span><span class="sxs-lookup"><span data-stu-id="79f4e-140">The pipeline uses Copy Activity to copy data from an Azure blob to an output Azure database table.</span></span> |
| [<span data-ttu-id="79f4e-141">Monitor datasets and pipeline</span><span class="sxs-lookup"><span data-stu-id="79f4e-141">Monitor datasets and pipeline</span></span>](#monitor-pipeline) |<span data-ttu-id="79f4e-142">In this step, you monitor the datasets and the pipeline by using Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="79f4e-142">In this step, you monitor the datasets and the pipeline by using Azure PowerShell.</span></span> |

## <a name="create-a-data-factory"></a><span data-ttu-id="79f4e-143">Create a data factory</span><span class="sxs-lookup"><span data-stu-id="79f4e-143">Create a data factory</span></span>
<span data-ttu-id="79f4e-144">In this step, you use Azure PowerShell to create an Azure data factory named **ADFTutorialDataFactoryPSH**.</span><span class="sxs-lookup"><span data-stu-id="79f4e-144">In this step, you use Azure PowerShell to create an Azure data factory named **ADFTutorialDataFactoryPSH**.</span></span>

1. <span data-ttu-id="79f4e-145">Launch **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="79f4e-145">Launch **PowerShell**.</span></span> <span data-ttu-id="79f4e-146">Keep Azure PowerShell open until the end of this tutorial.</span><span class="sxs-lookup"><span data-stu-id="79f4e-146">Keep Azure PowerShell open until the end of this tutorial.</span></span> <span data-ttu-id="79f4e-147">If you close and reopen, you need to run the commands again.</span><span class="sxs-lookup"><span data-stu-id="79f4e-147">If you close and reopen, you need to run the commands again.</span></span>

    <span data-ttu-id="79f4e-148">Run the following command, and enter the user name and password that you use to sign in to the Azure portal:</span><span class="sxs-lookup"><span data-stu-id="79f4e-148">Run the following command, and enter the user name and password that you use to sign in to the Azure portal:</span></span>

    ```PowerShell
    Login-AzureRmAccount
    ```   
   
    <span data-ttu-id="79f4e-149">Run the following command to view all the subscriptions for this account:</span><span class="sxs-lookup"><span data-stu-id="79f4e-149">Run the following command to view all the subscriptions for this account:</span></span>

    ```PowerShell
    Get-AzureRmSubscription
    ```

    <span data-ttu-id="79f4e-150">Run the following command to select the subscription that you want to work with.</span><span class="sxs-lookup"><span data-stu-id="79f4e-150">Run the following command to select the subscription that you want to work with.</span></span> <span data-ttu-id="79f4e-151">Replace **&lt;NameOfAzureSubscription**&gt; with the name of your Azure subscription:</span><span class="sxs-lookup"><span data-stu-id="79f4e-151">Replace **&lt;NameOfAzureSubscription**&gt; with the name of your Azure subscription:</span></span>

    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```
2. <span data-ttu-id="79f4e-152">Create an Azure resource group named **ADFTutorialResourceGroup** by running the following command:</span><span class="sxs-lookup"><span data-stu-id="79f4e-152">Create an Azure resource group named **ADFTutorialResourceGroup** by running the following command:</span></span>

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```
    
    <span data-ttu-id="79f4e-153">Some of the steps in this tutorial assume that you use the resource group named **ADFTutorialResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="79f4e-153">Some of the steps in this tutorial assume that you use the resource group named **ADFTutorialResourceGroup**.</span></span> <span data-ttu-id="79f4e-154">If you use a different resource group, you need to use it in place of ADFTutorialResourceGroup in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="79f4e-154">If you use a different resource group, you need to use it in place of ADFTutorialResourceGroup in this tutorial.</span></span>
3. <span data-ttu-id="79f4e-155">Run the **New-AzureRmDataFactory** cmdlet to create a data factory named **ADFTutorialDataFactoryPSH**:</span><span class="sxs-lookup"><span data-stu-id="79f4e-155">Run the **New-AzureRmDataFactory** cmdlet to create a data factory named **ADFTutorialDataFactoryPSH**:</span></span>  

    ```PowerShell
    New-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name ADFTutorialDataFactoryPSH –Location "West US"
    ```
<span data-ttu-id="79f4e-156">Note the following points:</span><span class="sxs-lookup"><span data-stu-id="79f4e-156">Note the following points:</span></span>

* <span data-ttu-id="79f4e-157">The name of the Azure data factory must be globally unique.</span><span class="sxs-lookup"><span data-stu-id="79f4e-157">The name of the Azure data factory must be globally unique.</span></span> <span data-ttu-id="79f4e-158">If you receive the following error, change the name (for example, yournameADFTutorialDataFactoryPSH).</span><span class="sxs-lookup"><span data-stu-id="79f4e-158">If you receive the following error, change the name (for example, yournameADFTutorialDataFactoryPSH).</span></span> <span data-ttu-id="79f4e-159">Use this name in place of ADFTutorialFactoryPSH while performing steps in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="79f4e-159">Use this name in place of ADFTutorialFactoryPSH while performing steps in this tutorial.</span></span> <span data-ttu-id="79f4e-160">See [Data Factory - Naming Rules](data-factory-naming-rules.md) for Data Factory artifacts.</span><span class="sxs-lookup"><span data-stu-id="79f4e-160">See [Data Factory - Naming Rules](data-factory-naming-rules.md) for Data Factory artifacts.</span></span>

    ```
    Data factory name “ADFTutorialDataFactoryPSH” is not available
    ```
* <span data-ttu-id="79f4e-161">To create Data Factory instances, you need to be a contributor or administrator of the Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="79f4e-161">To create Data Factory instances, you need to be a contributor or administrator of the Azure subscription.</span></span>
* <span data-ttu-id="79f4e-162">The name of the data factory may be registered as a DNS name in the future, and hence become publicly visible.</span><span class="sxs-lookup"><span data-stu-id="79f4e-162">The name of the data factory may be registered as a DNS name in the future, and hence become publicly visible.</span></span>
* <span data-ttu-id="79f4e-163">You may receive the following error: "**This subscription is not registered to use namespace Microsoft.DataFactory.**"</span><span class="sxs-lookup"><span data-stu-id="79f4e-163">You may receive the following error: "**This subscription is not registered to use namespace Microsoft.DataFactory.**"</span></span> <span data-ttu-id="79f4e-164">Do one of the following, and try publishing again:</span><span class="sxs-lookup"><span data-stu-id="79f4e-164">Do one of the following, and try publishing again:</span></span>

  * <span data-ttu-id="79f4e-165">In Azure PowerShell, run the following command to register the Data Factory provider:</span><span class="sxs-lookup"><span data-stu-id="79f4e-165">In Azure PowerShell, run the following command to register the Data Factory provider:</span></span>

    ```PowerShell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```

    <span data-ttu-id="79f4e-166">Run the following command to confirm that the Data Factory provider is registered:</span><span class="sxs-lookup"><span data-stu-id="79f4e-166">Run the following command to confirm that the Data Factory provider is registered:</span></span>

    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="79f4e-167">Sign in by using the Azure subscription to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="79f4e-167">Sign in by using the Azure subscription to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="79f4e-168">Go to a Data Factory blade, or create a data factory in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="79f4e-168">Go to a Data Factory blade, or create a data factory in the Azure portal.</span></span> <span data-ttu-id="79f4e-169">This action automatically registers the provider for you.</span><span class="sxs-lookup"><span data-stu-id="79f4e-169">This action automatically registers the provider for you.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="79f4e-170">Create linked services</span><span class="sxs-lookup"><span data-stu-id="79f4e-170">Create linked services</span></span>
<span data-ttu-id="79f4e-171">Linked services link data stores or compute services to an Azure data factory.</span><span class="sxs-lookup"><span data-stu-id="79f4e-171">Linked services link data stores or compute services to an Azure data factory.</span></span> <span data-ttu-id="79f4e-172">A data store can be an Azure Storage service, Azure SQL Database, or an on-premises SQL Server database that contains input data or stores output data for a Data Factory pipeline.</span><span class="sxs-lookup"><span data-stu-id="79f4e-172">A data store can be an Azure Storage service, Azure SQL Database, or an on-premises SQL Server database that contains input data or stores output data for a Data Factory pipeline.</span></span> <span data-ttu-id="79f4e-173">A compute service is the service that processes input data and produces output data.</span><span class="sxs-lookup"><span data-stu-id="79f4e-173">A compute service is the service that processes input data and produces output data.</span></span>

<span data-ttu-id="79f4e-174">In this step, you create two linked services: **StorageLinkedService** and **AzureSqlLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="79f4e-174">In this step, you create two linked services: **StorageLinkedService** and **AzureSqlLinkedService**.</span></span> <span data-ttu-id="79f4e-175">StorageLinkedService links an Azure storage account, and AzureSqlLinkedService links an Azure SQL database, to the data factory **ADFTutorialDataFactoryPSH**.</span><span class="sxs-lookup"><span data-stu-id="79f4e-175">StorageLinkedService links an Azure storage account, and AzureSqlLinkedService links an Azure SQL database, to the data factory **ADFTutorialDataFactoryPSH**.</span></span> <span data-ttu-id="79f4e-176">You create a pipeline later in this tutorial that copies data from a blob container in StorageLinkedService to a SQL table in AzureSqlLinkedService.</span><span class="sxs-lookup"><span data-stu-id="79f4e-176">You create a pipeline later in this tutorial that copies data from a blob container in StorageLinkedService to a SQL table in AzureSqlLinkedService.</span></span>

### <a name="create-a-linked-service-for-an-azure-storage-account"></a><span data-ttu-id="79f4e-177">Create a linked service for an Azure storage account</span><span class="sxs-lookup"><span data-stu-id="79f4e-177">Create a linked service for an Azure storage account</span></span>
1. <span data-ttu-id="79f4e-178">Create a JSON file named **StorageLinkedService.json** in the **C:\ADFGetStartedPSH** folder, with the following content.</span><span class="sxs-lookup"><span data-stu-id="79f4e-178">Create a JSON file named **StorageLinkedService.json** in the **C:\ADFGetStartedPSH** folder, with the following content.</span></span> <span data-ttu-id="79f4e-179">(Create the folder ADFGetStartedPSH if it does not already exist.)</span><span class="sxs-lookup"><span data-stu-id="79f4e-179">(Create the folder ADFGetStartedPSH if it does not already exist.)</span></span>

    ```json
    {
        "name": "StorageLinkedService",
        "properties": {
            "type": "AzureStorage",
            "typeProperties": {
                "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
            }
        }
     }
    ```
   <span data-ttu-id="79f4e-180">Replace **accountname** and **accountkey** with name and key of your Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="79f4e-180">Replace **accountname** and **accountkey** with name and key of your Azure storage account.</span></span>
2. <span data-ttu-id="79f4e-181">In **Azure PowerShell**, switch to the **ADFGetStartedPSH** folder.</span><span class="sxs-lookup"><span data-stu-id="79f4e-181">In **Azure PowerShell**, switch to the **ADFGetStartedPSH** folder.</span></span>
3. <span data-ttu-id="79f4e-182">You can use the **New-AzureRmDataFactoryLinkedService** cmdlet to create a linked service.</span><span class="sxs-lookup"><span data-stu-id="79f4e-182">You can use the **New-AzureRmDataFactoryLinkedService** cmdlet to create a linked service.</span></span> <span data-ttu-id="79f4e-183">This cmdlet, and other Data Factory cmdlets you use in this tutorial, requires you to pass values for the **ResourceGroupName** and **DataFactoryName** parameters.</span><span class="sxs-lookup"><span data-stu-id="79f4e-183">This cmdlet, and other Data Factory cmdlets you use in this tutorial, requires you to pass values for the **ResourceGroupName** and **DataFactoryName** parameters.</span></span> <span data-ttu-id="79f4e-184">Alternatively, you can use **Get-AzureRmDataFactory** to get a DataFactory object, and pass the object without typing ResourceGroupName and DataFactoryName each time you run a cmdlet.</span><span class="sxs-lookup"><span data-stu-id="79f4e-184">Alternatively, you can use **Get-AzureRmDataFactory** to get a DataFactory object, and pass the object without typing ResourceGroupName and DataFactoryName each time you run a cmdlet.</span></span> <span data-ttu-id="79f4e-185">Run the following command to assign the output of the **Get-AzureRmDataFactory** cmdlet to a variable: **$df**:</span><span class="sxs-lookup"><span data-stu-id="79f4e-185">Run the following command to assign the output of the **Get-AzureRmDataFactory** cmdlet to a variable: **$df**:</span></span>

    ```PowerShell   
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name ADFTutorialDataFactoryPSH
    ```

4. <span data-ttu-id="79f4e-186">Now, run the **New-AzureRmDataFactoryLinkedService** cmdlet to create the linked service: **StorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="79f4e-186">Now, run the **New-AzureRmDataFactoryLinkedService** cmdlet to create the linked service: **StorageLinkedService**.</span></span>

    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\StorageLinkedService.json
    ```

    <span data-ttu-id="79f4e-187">If you hadn't run the **Get-AzureRmDataFactory** cmdlet and assigned the output to **$df** variable, you would have to specify values for the ResourceGroupName and DataFactoryName parameters as follows.</span><span class="sxs-lookup"><span data-stu-id="79f4e-187">If you hadn't run the **Get-AzureRmDataFactory** cmdlet and assigned the output to **$df** variable, you would have to specify values for the ResourceGroupName and DataFactoryName parameters as follows.</span></span>   

    ```PowerShell
    New-AzureRmDataFactoryLinkedService -ResourceGroupName ADFTutorialResourceGroup -DataFactoryName ADFTutorialDataFactoryPSH -File .\StorageLinkedService.json
    ```

<span data-ttu-id="79f4e-188">If you close Azure PowerShell in the middle of the tutorial, you have run the Get-AzureRmDataFactory cmdlet the next time you launch Azure PowerShell to complete the tutorial.</span><span class="sxs-lookup"><span data-stu-id="79f4e-188">If you close Azure PowerShell in the middle of the tutorial, you have run the Get-AzureRmDataFactory cmdlet the next time you launch Azure PowerShell to complete the tutorial.</span></span>

### <a name="create-a-linked-service-for-an-azure-sql-database"></a><span data-ttu-id="79f4e-189">Create a linked service for an Azure SQL database</span><span class="sxs-lookup"><span data-stu-id="79f4e-189">Create a linked service for an Azure SQL database</span></span>
1. <span data-ttu-id="79f4e-190">Create a JSON file named AzureSqlLinkedService.json, with the following content:</span><span class="sxs-lookup"><span data-stu-id="79f4e-190">Create a JSON file named AzureSqlLinkedService.json, with the following content:</span></span>

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
   <span data-ttu-id="79f4e-191">Replace **servername**, **databasename**, **username@servername**, and **password** with names of your Azure SQL server, database, user account, and password.</span><span class="sxs-lookup"><span data-stu-id="79f4e-191">Replace **servername**, **databasename**, **username@servername**, and **password** with names of your Azure SQL server, database, user account, and password.</span></span>
2. <span data-ttu-id="79f4e-192">Run the following command to create a linked service:</span><span class="sxs-lookup"><span data-stu-id="79f4e-192">Run the following command to create a linked service:</span></span>

    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\AzureSqlLinkedService.json
    ```

   <span data-ttu-id="79f4e-193">Confirm that the **Allow access to Azure services** setting is turned on for your SQL database server.</span><span class="sxs-lookup"><span data-stu-id="79f4e-193">Confirm that the **Allow access to Azure services** setting is turned on for your SQL database server.</span></span> <span data-ttu-id="79f4e-194">To verify and turn it on, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="79f4e-194">To verify and turn it on, do the following steps:</span></span>

   1. <span data-ttu-id="79f4e-195">Click the **BROWSE** hub on the left, and click **SQL servers**.</span><span class="sxs-lookup"><span data-stu-id="79f4e-195">Click the **BROWSE** hub on the left, and click **SQL servers**.</span></span>
   2. <span data-ttu-id="79f4e-196">Select your server, and click **SETTINGS** on the **SQL SERVER** blade.</span><span class="sxs-lookup"><span data-stu-id="79f4e-196">Select your server, and click **SETTINGS** on the **SQL SERVER** blade.</span></span>
   3. <span data-ttu-id="79f4e-197">In the **SETTINGS** blade, click **Firewall**.</span><span class="sxs-lookup"><span data-stu-id="79f4e-197">In the **SETTINGS** blade, click **Firewall**.</span></span>
   4. <span data-ttu-id="79f4e-198">In the **Firewall settings** blade, click **ON** for **Allow access to Azure services**.</span><span class="sxs-lookup"><span data-stu-id="79f4e-198">In the **Firewall settings** blade, click **ON** for **Allow access to Azure services**.</span></span>
   5. <span data-ttu-id="79f4e-199">Click the **ACTIVE** hub on the left to switch to the **Data Factory** blade you were on.</span><span class="sxs-lookup"><span data-stu-id="79f4e-199">Click the **ACTIVE** hub on the left to switch to the **Data Factory** blade you were on.</span></span>

## <a name="create-datasets"></a><span data-ttu-id="79f4e-200">Create datasets</span><span class="sxs-lookup"><span data-stu-id="79f4e-200">Create datasets</span></span>
<span data-ttu-id="79f4e-201">In the previous step, you created services to link an Azure storage account and Azure SQL database to the data factory.</span><span class="sxs-lookup"><span data-stu-id="79f4e-201">In the previous step, you created services to link an Azure storage account and Azure SQL database to the data factory.</span></span> <span data-ttu-id="79f4e-202">In this step, you create datasets that represent the input and output data for Copy Activity in the pipeline you create in the next step.</span><span class="sxs-lookup"><span data-stu-id="79f4e-202">In this step, you create datasets that represent the input and output data for Copy Activity in the pipeline you create in the next step.</span></span>

<span data-ttu-id="79f4e-203">A table is a rectangular dataset.</span><span class="sxs-lookup"><span data-stu-id="79f4e-203">A table is a rectangular dataset.</span></span> <span data-ttu-id="79f4e-204">Currently, it is the only type of dataset that is supported.</span><span class="sxs-lookup"><span data-stu-id="79f4e-204">Currently, it is the only type of dataset that is supported.</span></span> <span data-ttu-id="79f4e-205">The input table in this tutorial refers to a blob container in Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="79f4e-205">The input table in this tutorial refers to a blob container in Azure Storage.</span></span> <span data-ttu-id="79f4e-206">The output table refers to a SQL table in the Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="79f4e-206">The output table refers to a SQL table in the Azure SQL database.</span></span>  

### <a name="prepare-azure-blob-storage-and-azure-sql-database-for-the-tutorial"></a><span data-ttu-id="79f4e-207">Prepare Azure Blob storage and Azure SQL Database for the tutorial</span><span class="sxs-lookup"><span data-stu-id="79f4e-207">Prepare Azure Blob storage and Azure SQL Database for the tutorial</span></span>
<span data-ttu-id="79f4e-208">Skip this step if you have gone through the tutorial from [Copy data from Blob storage to SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="79f4e-208">Skip this step if you have gone through the tutorial from [Copy data from Blob storage to SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

<span data-ttu-id="79f4e-209">Perform the following steps to prepare the Blob storage and SQL Database for this tutorial.</span><span class="sxs-lookup"><span data-stu-id="79f4e-209">Perform the following steps to prepare the Blob storage and SQL Database for this tutorial.</span></span>

1. <span data-ttu-id="79f4e-210">Create a blob container, named **adftutorial**, in Blob storage that **StorageLinkedService** points to.</span><span class="sxs-lookup"><span data-stu-id="79f4e-210">Create a blob container, named **adftutorial**, in Blob storage that **StorageLinkedService** points to.</span></span>
2. <span data-ttu-id="79f4e-211">Create and upload a text file, named **emp.txt**, as a blob to the **adftutorial** container.</span><span class="sxs-lookup"><span data-stu-id="79f4e-211">Create and upload a text file, named **emp.txt**, as a blob to the **adftutorial** container.</span></span>
3. <span data-ttu-id="79f4e-212">Create a table, named **emp**, in the SQL database that **AzureSqlLinkedService** points to.</span><span class="sxs-lookup"><span data-stu-id="79f4e-212">Create a table, named **emp**, in the SQL database that **AzureSqlLinkedService** points to.</span></span>

4. <span data-ttu-id="79f4e-213">Launch Notepad.</span><span class="sxs-lookup"><span data-stu-id="79f4e-213">Launch Notepad.</span></span> <span data-ttu-id="79f4e-214">Copy the following text and save it as **emp.txt** to **C:\ADFGetStartedPSH** folder on your hard drive.</span><span class="sxs-lookup"><span data-stu-id="79f4e-214">Copy the following text and save it as **emp.txt** to **C:\ADFGetStartedPSH** folder on your hard drive.</span></span>

    ```
    John, Doe
    Jane, Doe
    ```
5. <span data-ttu-id="79f4e-215">Use tools such as [Azure Storage Explorer](https://azurestorageexplorer.codeplex.com/) to create the **adftutorial** container, and to upload the **emp.txt** file to the container.</span><span class="sxs-lookup"><span data-stu-id="79f4e-215">Use tools such as [Azure Storage Explorer](https://azurestorageexplorer.codeplex.com/) to create the **adftutorial** container, and to upload the **emp.txt** file to the container.</span></span>

    ![Azure Storage Explorer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-activity-tutorial-using-powershell/getstarted-storage-explorer.png)
6. <span data-ttu-id="79f4e-217">Use the following SQL script to create the **emp** table in your SQL database.</span><span class="sxs-lookup"><span data-stu-id="79f4e-217">Use the following SQL script to create the **emp** table in your SQL database.</span></span>  

    ```sql
    CREATE TABLE dbo.emp
    (
        ID int IDENTITY(1,1) NOT NULL,
        FirstName varchar(50),
        LastName varchar(50),
    )
    GO

    CREATE CLUSTERED INDEX IX_emp_ID ON dbo.emp (ID);
    ```

    <span data-ttu-id="79f4e-218">If you have SQL Server 2014 installed on your computer, follow instructions from [Step 2: Connect to SQL Database of the Managing Azure SQL Database using SQL Server Management Studio](../sql-database/sql-database-manage-azure-ssms.md) to connect to your SQL database server and run the SQL script.</span><span class="sxs-lookup"><span data-stu-id="79f4e-218">If you have SQL Server 2014 installed on your computer, follow instructions from [Step 2: Connect to SQL Database of the Managing Azure SQL Database using SQL Server Management Studio](../sql-database/sql-database-manage-azure-ssms.md) to connect to your SQL database server and run the SQL script.</span></span>

    <span data-ttu-id="79f4e-219">If your client is not allowed to access the SQL database server, you need to set up the firewall for your SQL database server to allow access from your machine (IP Address).</span><span class="sxs-lookup"><span data-stu-id="79f4e-219">If your client is not allowed to access the SQL database server, you need to set up the firewall for your SQL database server to allow access from your machine (IP Address).</span></span> <span data-ttu-id="79f4e-220">For the steps, see [this article](../sql-database/sql-database-configure-firewall-settings.md).</span><span class="sxs-lookup"><span data-stu-id="79f4e-220">For the steps, see [this article](../sql-database/sql-database-configure-firewall-settings.md).</span></span>

### <a name="create-an-input-dataset"></a><span data-ttu-id="79f4e-221">Create an input dataset</span><span class="sxs-lookup"><span data-stu-id="79f4e-221">Create an input dataset</span></span>
<span data-ttu-id="79f4e-222">A table is a rectangular dataset, and has a schema.</span><span class="sxs-lookup"><span data-stu-id="79f4e-222">A table is a rectangular dataset, and has a schema.</span></span> <span data-ttu-id="79f4e-223">In this step, you create a table, named **EmpBlobTable**.</span><span class="sxs-lookup"><span data-stu-id="79f4e-223">In this step, you create a table, named **EmpBlobTable**.</span></span> <span data-ttu-id="79f4e-224">This table points to a blob container in Azure Storage represented by the **StorageLinkedService** linked service.</span><span class="sxs-lookup"><span data-stu-id="79f4e-224">This table points to a blob container in Azure Storage represented by the **StorageLinkedService** linked service.</span></span> <span data-ttu-id="79f4e-225">This blob container (adftutorial) contains the input data in the file **emp.txt**.</span><span class="sxs-lookup"><span data-stu-id="79f4e-225">This blob container (adftutorial) contains the input data in the file **emp.txt**.</span></span>

1. <span data-ttu-id="79f4e-226">Create a JSON file named **EmpBlobTable.json** in the **C:\ADFGetStartedPSH** folder, with the following content:</span><span class="sxs-lookup"><span data-stu-id="79f4e-226">Create a JSON file named **EmpBlobTable.json** in the **C:\ADFGetStartedPSH** folder, with the following content:</span></span>

    ```json
    {
        "name": "EmpTableFromBlob",
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
            "linkedServiceName": "StorageLinkedService",
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

   <span data-ttu-id="79f4e-227">Note the following points:</span><span class="sxs-lookup"><span data-stu-id="79f4e-227">Note the following points:</span></span>

   * <span data-ttu-id="79f4e-228">Dataset **type** is set to **AzureBlob**.</span><span class="sxs-lookup"><span data-stu-id="79f4e-228">Dataset **type** is set to **AzureBlob**.</span></span>
   * <span data-ttu-id="79f4e-229">**linkedServiceName** is set to **StorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="79f4e-229">**linkedServiceName** is set to **StorageLinkedService**.</span></span>
   * <span data-ttu-id="79f4e-230">**folderPath** is set to the **adftutorial** container.</span><span class="sxs-lookup"><span data-stu-id="79f4e-230">**folderPath** is set to the **adftutorial** container.</span></span>
   * <span data-ttu-id="79f4e-231">**fileName** is set to **emp.txt**.</span><span class="sxs-lookup"><span data-stu-id="79f4e-231">**fileName** is set to **emp.txt**.</span></span> <span data-ttu-id="79f4e-232">If you do not specify the name of the blob, data from all blobs in the container is considered as input data.</span><span class="sxs-lookup"><span data-stu-id="79f4e-232">If you do not specify the name of the blob, data from all blobs in the container is considered as input data.</span></span>  
   * <span data-ttu-id="79f4e-233">Format **type** is set to **TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="79f4e-233">Format **type** is set to **TextFormat**.</span></span>
   * <span data-ttu-id="79f4e-234">There are two fields in the text file, **FirstName** and **LastName**, separated by a comma character (columnDelimiter).</span><span class="sxs-lookup"><span data-stu-id="79f4e-234">There are two fields in the text file, **FirstName** and **LastName**, separated by a comma character (columnDelimiter).</span></span>    
   * <span data-ttu-id="79f4e-235">**availability** is set to **hourly** (frequency is set to hour, and interval is set to 1).</span><span class="sxs-lookup"><span data-stu-id="79f4e-235">**availability** is set to **hourly** (frequency is set to hour, and interval is set to 1).</span></span> <span data-ttu-id="79f4e-236">Therefore, Data Factory looks for input data hourly in the root folder in the blob container (adftutorial).</span><span class="sxs-lookup"><span data-stu-id="79f4e-236">Therefore, Data Factory looks for input data hourly in the root folder in the blob container (adftutorial).</span></span>

   <span data-ttu-id="79f4e-237">If you don't specify a **fileName** for an **input table**, all files and blobs from the input folder (folderPath) are considered as inputs.</span><span class="sxs-lookup"><span data-stu-id="79f4e-237">If you don't specify a **fileName** for an **input table**, all files and blobs from the input folder (folderPath) are considered as inputs.</span></span> <span data-ttu-id="79f4e-238">If you specify a fileName in the JSON, only the specified file or blob is considered as an input.</span><span class="sxs-lookup"><span data-stu-id="79f4e-238">If you specify a fileName in the JSON, only the specified file or blob is considered as an input.</span></span>

   <span data-ttu-id="79f4e-239">If you do not specify a **fileName** for an **output table**, the generated files in the **folderPath** are named in the following format: Data.<Guid\>.txt (example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.).</span><span class="sxs-lookup"><span data-stu-id="79f4e-239">If you do not specify a **fileName** for an **output table**, the generated files in the **folderPath** are named in the following format: Data.<Guid\>.txt (example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.).</span></span>

   <span data-ttu-id="79f4e-240">To set **folderPath** and **fileName** dynamically based on the **SliceStart** time, use the **partitionedBy** property.</span><span class="sxs-lookup"><span data-stu-id="79f4e-240">To set **folderPath** and **fileName** dynamically based on the **SliceStart** time, use the **partitionedBy** property.</span></span> <span data-ttu-id="79f4e-241">In the following example, folderPath uses Year, Month, and Day from the SliceStart (start time of the slice being processed) and fileName uses Hour from the SliceStart.</span><span class="sxs-lookup"><span data-stu-id="79f4e-241">In the following example, folderPath uses Year, Month, and Day from the SliceStart (start time of the slice being processed) and fileName uses Hour from the SliceStart.</span></span> <span data-ttu-id="79f4e-242">For example, if a slice is being produced for 2016-10-20T08:00:00, the folderName is set to wikidatagateway/wikisampledataout/2016/10/20 and the fileName is set to 08.csv.</span><span class="sxs-lookup"><span data-stu-id="79f4e-242">For example, if a slice is being produced for 2016-10-20T08:00:00, the folderName is set to wikidatagateway/wikisampledataout/2016/10/20 and the fileName is set to 08.csv.</span></span>

    ```json
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

   <span data-ttu-id="79f4e-243">For details about JSON properties, see the [JSON Scripting Reference](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="79f4e-243">For details about JSON properties, see the [JSON Scripting Reference](data-factory-data-movement-activities.md).</span></span>
2. <span data-ttu-id="79f4e-244">Run the following command to create the Data Factory dataset.</span><span class="sxs-lookup"><span data-stu-id="79f4e-244">Run the following command to create the Data Factory dataset.</span></span>

    ```PowerShell  
    New-AzureRmDataFactoryDataset $df -File .\EmpBlobTable.json
    ```

### <a name="create-an-output-dataset"></a><span data-ttu-id="79f4e-245">Create an output dataset</span><span class="sxs-lookup"><span data-stu-id="79f4e-245">Create an output dataset</span></span>
<span data-ttu-id="79f4e-246">In this step, you create an output dataset named **EmpSQLTable**.</span><span class="sxs-lookup"><span data-stu-id="79f4e-246">In this step, you create an output dataset named **EmpSQLTable**.</span></span> <span data-ttu-id="79f4e-247">This dataset points to a SQL table (emp) in the Azure SQL database represented by **AzureSqlLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="79f4e-247">This dataset points to a SQL table (emp) in the Azure SQL database represented by **AzureSqlLinkedService**.</span></span> <span data-ttu-id="79f4e-248">The pipeline copies data from the input blob to the **emp** table.</span><span class="sxs-lookup"><span data-stu-id="79f4e-248">The pipeline copies data from the input blob to the **emp** table.</span></span>

1. <span data-ttu-id="79f4e-249">Create a JSON file named **EmpSQLTable.json** in the **C:\ADFGetStartedPSH** folder with the following content:</span><span class="sxs-lookup"><span data-stu-id="79f4e-249">Create a JSON file named **EmpSQLTable.json** in the **C:\ADFGetStartedPSH** folder with the following content:</span></span>

    ```json
    {
        "name": "EmpSQLTable",
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

   <span data-ttu-id="79f4e-250">Note the following points:</span><span class="sxs-lookup"><span data-stu-id="79f4e-250">Note the following points:</span></span>

   * <span data-ttu-id="79f4e-251">Dataset **type** is set to **AzureSqlTable**.</span><span class="sxs-lookup"><span data-stu-id="79f4e-251">Dataset **type** is set to **AzureSqlTable**.</span></span>
   * <span data-ttu-id="79f4e-252">**linkedServiceName** is set to **AzureSqlLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="79f4e-252">**linkedServiceName** is set to **AzureSqlLinkedService**.</span></span>
   * <span data-ttu-id="79f4e-253">**tablename** is set to **emp**.</span><span class="sxs-lookup"><span data-stu-id="79f4e-253">**tablename** is set to **emp**.</span></span>
   * <span data-ttu-id="79f4e-254">There are three columns, **ID**, **FirstName**, and **LastName**, in the emp table in the database.</span><span class="sxs-lookup"><span data-stu-id="79f4e-254">There are three columns, **ID**, **FirstName**, and **LastName**, in the emp table in the database.</span></span> <span data-ttu-id="79f4e-255">ID is an identity column, so you need to specify only **FirstName** and **LastName** here.</span><span class="sxs-lookup"><span data-stu-id="79f4e-255">ID is an identity column, so you need to specify only **FirstName** and **LastName** here.</span></span>
   * <span data-ttu-id="79f4e-256">**availability** is set to **hourly** (frequency set to hour and interval set to 1).</span><span class="sxs-lookup"><span data-stu-id="79f4e-256">**availability** is set to **hourly** (frequency set to hour and interval set to 1).</span></span> <span data-ttu-id="79f4e-257">The Data Factory service generates an output data slice every hour in the **emp** table in the Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="79f4e-257">The Data Factory service generates an output data slice every hour in the **emp** table in the Azure SQL database.</span></span>
2. <span data-ttu-id="79f4e-258">Run the following command to create the data factory dataset.</span><span class="sxs-lookup"><span data-stu-id="79f4e-258">Run the following command to create the data factory dataset.</span></span>

    ```PowerShell   
    New-AzureRmDataFactoryDataset $df -File .\EmpSQLTable.json
    ```

## <a name="create-a-pipeline"></a><span data-ttu-id="79f4e-259">Create a pipeline</span><span class="sxs-lookup"><span data-stu-id="79f4e-259">Create a pipeline</span></span>
<span data-ttu-id="79f4e-260">In this step, you create a pipeline with **Copy Activity**.</span><span class="sxs-lookup"><span data-stu-id="79f4e-260">In this step, you create a pipeline with **Copy Activity**.</span></span> <span data-ttu-id="79f4e-261">The pipeline uses **EmpTableFromBlob** as input, and **EmpSQLTable** as output.</span><span class="sxs-lookup"><span data-stu-id="79f4e-261">The pipeline uses **EmpTableFromBlob** as input, and **EmpSQLTable** as output.</span></span>

1. <span data-ttu-id="79f4e-262">Create a JSON file named **ADFTutorialPipeline.json** in the **C:\ADFGetStartedPSH** folder, with the following content:</span><span class="sxs-lookup"><span data-stu-id="79f4e-262">Create a JSON file named **ADFTutorialPipeline.json** in the **C:\ADFGetStartedPSH** folder, with the following content:</span></span>

    ```json
    {
        "name": "ADFTutorialPipeline",
        "properties": {
            "description": "Copy data from a blob to Azure SQL table",
            "activities": [
                {
                    "name": "CopyFromBlobToSQL",
                    "description": "Push Regional Effectiveness Campaign data to Azure SQL database",
                    "type": "Copy",
                    "inputs": [{ "name": "EmpTableFromBlob" }],
                    "outputs": [{ "name": "EmpSQLTable" }],
                    "typeProperties": {
                        "source": {
                            "type": "BlobSource"
                        },
                        "sink": {
                            "type": "SqlSink"
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
            "start": "2016-08-09T00:00:00Z",
            "end": "2016-08-10T00:00:00Z",
            "isPaused": false
        }
     }
    ```
   <span data-ttu-id="79f4e-263">Note the following points:</span><span class="sxs-lookup"><span data-stu-id="79f4e-263">Note the following points:</span></span>

   * <span data-ttu-id="79f4e-264">In the activities section, there is only one activity whose **type** is set to **Copy**.</span><span class="sxs-lookup"><span data-stu-id="79f4e-264">In the activities section, there is only one activity whose **type** is set to **Copy**.</span></span>
   * <span data-ttu-id="79f4e-265">Input for the activity is set to **EmpTableFromBlob**, and output for the activity is set to **EmpSQLTable**.</span><span class="sxs-lookup"><span data-stu-id="79f4e-265">Input for the activity is set to **EmpTableFromBlob**, and output for the activity is set to **EmpSQLTable**.</span></span>
   * <span data-ttu-id="79f4e-266">In the **transformation** section, **BlobSource** is specified as the source type, and **SqlSink** is specified as the sink type.</span><span class="sxs-lookup"><span data-stu-id="79f4e-266">In the **transformation** section, **BlobSource** is specified as the source type, and **SqlSink** is specified as the sink type.</span></span>

   <span data-ttu-id="79f4e-267">Replace the value of the **start** property with the current day, and that of the **end** property with the next day.</span><span class="sxs-lookup"><span data-stu-id="79f4e-267">Replace the value of the **start** property with the current day, and that of the **end** property with the next day.</span></span> <span data-ttu-id="79f4e-268">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="79f4e-268">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="79f4e-269">For example: 2016-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="79f4e-269">For example: 2016-10-14T16:32:41Z.</span></span> <span data-ttu-id="79f4e-270">The **end** time is used in this tutorial, but it is optional.</span><span class="sxs-lookup"><span data-stu-id="79f4e-270">The **end** time is used in this tutorial, but it is optional.</span></span>

   <span data-ttu-id="79f4e-271">If you do not specify value for the **end** property, it is calculated as "**start + 48 hours**".</span><span class="sxs-lookup"><span data-stu-id="79f4e-271">If you do not specify value for the **end** property, it is calculated as "**start + 48 hours**".</span></span> <span data-ttu-id="79f4e-272">To run the pipeline indefinitely, specify **9/9/9999** as the value for the **end** property.</span><span class="sxs-lookup"><span data-stu-id="79f4e-272">To run the pipeline indefinitely, specify **9/9/9999** as the value for the **end** property.</span></span>

   <span data-ttu-id="79f4e-273">In the example, there are 24 data slices, as each data slice is produced hourly.</span><span class="sxs-lookup"><span data-stu-id="79f4e-273">In the example, there are 24 data slices, as each data slice is produced hourly.</span></span>

   <span data-ttu-id="79f4e-274">For more information about JSON properties, see the [JSON Scripting Reference](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="79f4e-274">For more information about JSON properties, see the [JSON Scripting Reference](data-factory-data-movement-activities.md).</span></span>
2. <span data-ttu-id="79f4e-275">Run the following command to create the data factory table.</span><span class="sxs-lookup"><span data-stu-id="79f4e-275">Run the following command to create the data factory table.</span></span>

    ```PowerShell   
    New-AzureRmDataFactoryPipeline $df -File .\ADFTutorialPipeline.json
    ```

<span data-ttu-id="79f4e-276">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="79f4e-276">Congratulations!</span></span> <span data-ttu-id="79f4e-277">You have successfully created an Azure data factory, linked services, tables, and a pipeline.</span><span class="sxs-lookup"><span data-stu-id="79f4e-277">You have successfully created an Azure data factory, linked services, tables, and a pipeline.</span></span> <span data-ttu-id="79f4e-278">You have also scheduled the pipeline.</span><span class="sxs-lookup"><span data-stu-id="79f4e-278">You have also scheduled the pipeline.</span></span>

## <a name="monitor-the-pipeline"></a><span data-ttu-id="79f4e-279">Monitor the pipeline</span><span class="sxs-lookup"><span data-stu-id="79f4e-279">Monitor the pipeline</span></span>
<span data-ttu-id="79f4e-280">In this step, you use Azure PowerShell to monitor what’s going on in an Azure data factory.</span><span class="sxs-lookup"><span data-stu-id="79f4e-280">In this step, you use Azure PowerShell to monitor what’s going on in an Azure data factory.</span></span>

1. <span data-ttu-id="79f4e-281">Run **Get-AzureRmDataFactory**, and assign the output to a variable $df.</span><span class="sxs-lookup"><span data-stu-id="79f4e-281">Run **Get-AzureRmDataFactory**, and assign the output to a variable $df.</span></span>

    ```PowerShell  
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name ADFTutorialDataFactoryPSH
    ```

2. <span data-ttu-id="79f4e-282">Run **Get-AzureRmDataFactorySlice** to get details about all slices of the **EmpSQLTable**, which is the output table of the pipeline.</span><span class="sxs-lookup"><span data-stu-id="79f4e-282">Run **Get-AzureRmDataFactorySlice** to get details about all slices of the **EmpSQLTable**, which is the output table of the pipeline.</span></span>  

    ```PowerShell   
    Get-AzureRmDataFactorySlice $df -DatasetName EmpSQLTable -StartDateTime 2016-08-09T00:00:00
    ```

   <span data-ttu-id="79f4e-283">Replace the year, month, and date part of the **StartDateTime** parameter with the current year, month, and date.</span><span class="sxs-lookup"><span data-stu-id="79f4e-283">Replace the year, month, and date part of the **StartDateTime** parameter with the current year, month, and date.</span></span> <span data-ttu-id="79f4e-284">This setting should match the **Start** value in the pipeline JSON.</span><span class="sxs-lookup"><span data-stu-id="79f4e-284">This setting should match the **Start** value in the pipeline JSON.</span></span>

   <span data-ttu-id="79f4e-285">You should see 24 slices, one for each hour from 12 AM of the current day to 12 AM of the next day.</span><span class="sxs-lookup"><span data-stu-id="79f4e-285">You should see 24 slices, one for each hour from 12 AM of the current day to 12 AM of the next day.</span></span>

   <span data-ttu-id="79f4e-286">**Sample output:**</span><span class="sxs-lookup"><span data-stu-id="79f4e-286">**Sample output:**</span></span>

    ``` 
     ResourceGroupName : ADFTutorialResourceGroup
     DataFactoryName   : ADFTutorialDataFactoryPSH
     TableName         : EmpSQLTable
     Start             : 8/9/2016 12:00:00 AM
     End               : 8/9/2016 1:00:00 AM
     RetryCount        : 0
     Status            : Waiting
     LatencyStatus     :
     LongRetryCount    : 0
    ```
3. <span data-ttu-id="79f4e-287">Run **Get-AzureRmDataFactoryRun** to get the details of activity runs for a **specific** slice.</span><span class="sxs-lookup"><span data-stu-id="79f4e-287">Run **Get-AzureRmDataFactoryRun** to get the details of activity runs for a **specific** slice.</span></span> <span data-ttu-id="79f4e-288">Change the value of the **StartDateTime** parameter to match the **Start** time of the slice from the output.</span><span class="sxs-lookup"><span data-stu-id="79f4e-288">Change the value of the **StartDateTime** parameter to match the **Start** time of the slice from the output.</span></span> <span data-ttu-id="79f4e-289">The value of the **StartDateTime** must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="79f4e-289">The value of the **StartDateTime** must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span>

    ```PowerShell  
    Get-AzureRmDataFactoryRun $df -DatasetName EmpSQLTable -StartDateTime 2016-08-09T00:00:00
    ```

   <span data-ttu-id="79f4e-290">You should see output similar to the following sample:</span><span class="sxs-lookup"><span data-stu-id="79f4e-290">You should see output similar to the following sample:</span></span>

    ```  
    Id                  : 3404c187-c889-4f88-933b-2a2f5cd84e90_635614488000000000_635614524000000000_EmpSQLTable
    ResourceGroupName   : ADFTutorialResourceGroup
    DataFactoryName     : ADFTutorialDataFactoryPSH
    TableName           : EmpSQLTable
    ProcessingStartTime : 8/9/2016 11:03:28 PM
    ProcessingEndTime   : 8/9/2016 11:04:36 PM
    PercentComplete     : 100
    DataSliceStart      : 8/9/2016 10:00:00 PM
    DataSliceEnd        : 8/9/2016 11:00:00 PM
    Status              : Succeeded
    Timestamp           : 8/9/2016 11:03:28 PM
    RetryAttempt        : 0
    Properties          : {}
    ErrorMessage        :
    ActivityName        : CopyFromBlobToSQL
    PipelineName        : ADFTutorialPipeline
    Type                : Copy
    ```

<span data-ttu-id="79f4e-291">For comprehensive documentation on Data Factory cmdlets, see the [Data Factory Cmdlet Reference][cmdlet-reference].</span><span class="sxs-lookup"><span data-stu-id="79f4e-291">For comprehensive documentation on Data Factory cmdlets, see the [Data Factory Cmdlet Reference][cmdlet-reference].</span></span>

## <a name="summary"></a><span data-ttu-id="79f4e-292">Summary</span><span class="sxs-lookup"><span data-stu-id="79f4e-292">Summary</span></span>
<span data-ttu-id="79f4e-293">In this tutorial, you created an Azure data factory to copy data from an Azure blob to an Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="79f4e-293">In this tutorial, you created an Azure data factory to copy data from an Azure blob to an Azure SQL database.</span></span> <span data-ttu-id="79f4e-294">You used PowerShell to create the data factory, linked services, datasets, and a pipeline.</span><span class="sxs-lookup"><span data-stu-id="79f4e-294">You used PowerShell to create the data factory, linked services, datasets, and a pipeline.</span></span> <span data-ttu-id="79f4e-295">Here are the high-level steps you performed in this tutorial:</span><span class="sxs-lookup"><span data-stu-id="79f4e-295">Here are the high-level steps you performed in this tutorial:</span></span>  

1. <span data-ttu-id="79f4e-296">Created an Azure **data factory**.</span><span class="sxs-lookup"><span data-stu-id="79f4e-296">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="79f4e-297">Created **linked services**:</span><span class="sxs-lookup"><span data-stu-id="79f4e-297">Created **linked services**:</span></span>

   <span data-ttu-id="79f4e-298">a.</span><span class="sxs-lookup"><span data-stu-id="79f4e-298">a.</span></span> <span data-ttu-id="79f4e-299">An **Azure Storage** linked service to link your Azure storage account that holds input data.</span><span class="sxs-lookup"><span data-stu-id="79f4e-299">An **Azure Storage** linked service to link your Azure storage account that holds input data.</span></span>     
   <span data-ttu-id="79f4e-300">b.</span><span class="sxs-lookup"><span data-stu-id="79f4e-300">b.</span></span> <span data-ttu-id="79f4e-301">An **Azure SQL** linked service to link your SQL database that holds the output data.</span><span class="sxs-lookup"><span data-stu-id="79f4e-301">An **Azure SQL** linked service to link your SQL database that holds the output data.</span></span>
3. <span data-ttu-id="79f4e-302">Created **datasets** that describe input data and output data for pipelines.</span><span class="sxs-lookup"><span data-stu-id="79f4e-302">Created **datasets** that describe input data and output data for pipelines.</span></span>
4. <span data-ttu-id="79f4e-303">Created a **pipeline** with **Copy Activity**, with **BlobSource** as the source and **SqlSink** as the sink.</span><span class="sxs-lookup"><span data-stu-id="79f4e-303">Created a **pipeline** with **Copy Activity**, with **BlobSource** as the source and **SqlSink** as the sink.</span></span>

## <a name="see-also"></a><span data-ttu-id="79f4e-304">See also</span><span class="sxs-lookup"><span data-stu-id="79f4e-304">See also</span></span>
| <span data-ttu-id="79f4e-305">Topic</span><span class="sxs-lookup"><span data-stu-id="79f4e-305">Topic</span></span> | <span data-ttu-id="79f4e-306">Description</span><span class="sxs-lookup"><span data-stu-id="79f4e-306">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="79f4e-307">Data Factory Cmdlet Reference</span><span class="sxs-lookup"><span data-stu-id="79f4e-307">Data Factory Cmdlet Reference</span></span>](/powershell/resourcemanager/azurerm.datafactories/v2.5.0/azurerm.datafactories) | <span data-ttu-id="79f4e-308">This section provides information about all the Data Factory cmdlets</span><span class="sxs-lookup"><span data-stu-id="79f4e-308">This section provides information about all the Data Factory cmdlets</span></span> |
| [<span data-ttu-id="79f4e-309">Pipelines</span><span class="sxs-lookup"><span data-stu-id="79f4e-309">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="79f4e-310">This article helps you understand pipelines and activities in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="79f4e-310">This article helps you understand pipelines and activities in Azure Data Factory.</span></span> |
| [<span data-ttu-id="79f4e-311">datasets</span><span class="sxs-lookup"><span data-stu-id="79f4e-311">datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="79f4e-312">This article helps you understand datasets in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="79f4e-312">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="79f4e-313">Scheduling and execution</span><span class="sxs-lookup"><span data-stu-id="79f4e-313">Scheduling and execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="79f4e-314">This article explains the scheduling and execution aspects of the Azure Data Factory application model.</span><span class="sxs-lookup"><span data-stu-id="79f4e-314">This article explains the scheduling and execution aspects of the Azure Data Factory application model.</span></span> |

[use-custom-activities]: data-factory-use-custom-activities.md
[troubleshoot]: data-factory-troubleshoot.md
[developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908

[cmdlet-reference]: https://msdn.microsoft.com/library/azure/dn820234.aspx
[old-cmdlet-reference]: https://msdn.microsoft.com/library/azure/dn820234(v=azure.98).aspx
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[azure-portal]: http://portal.azure.com
[download-azure-powershell]: ../powershell-install-configure.md
[data-factory-introduction]: data-factory-introduction.md

[image-data-factory-get-started-storage-explorer]: ./https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-activity-tutorial-using-powershell/getstarted-storage-explorer.png

[sql-management-studio]: ../sql-database/sql-database-manage-azure-ssms.md


