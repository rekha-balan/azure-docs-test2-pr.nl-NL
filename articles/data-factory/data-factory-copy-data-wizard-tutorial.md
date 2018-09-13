---
title: 'Tutorial: Create a pipeline using Copy Wizard | Microsoft Docs'
description: In this tutorial, you create an Azure Data Factory pipeline with a Copy Activity by using the Copy Wizard supported by Data Factory
services: data-factory
documentationcenter: ''
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: b87afb8e-53b7-4e1b-905b-0343dd096198
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 02/02/2017
ms.author: spelluru
ms.openlocfilehash: 14959796c11063dd33bac6ec10ec724af0af3702
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554560"
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-data-factory-copy-wizard"></a><span data-ttu-id="0d4da-103">Tutorial: Create a pipeline with Copy Activity using Data Factory Copy Wizard</span><span class="sxs-lookup"><span data-stu-id="0d4da-103">Tutorial: Create a pipeline with Copy Activity using Data Factory Copy Wizard</span></span>
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

<span data-ttu-id="0d4da-112">The Azure Data Factory **Copy Wizard** allows you to easily and quickly create a pipeline that implements the data ingestion/movement scenario.</span><span class="sxs-lookup"><span data-stu-id="0d4da-112">The Azure Data Factory **Copy Wizard** allows you to easily and quickly create a pipeline that implements the data ingestion/movement scenario.</span></span> <span data-ttu-id="0d4da-113">Therefore, we recommend that you use the wizard as a first step to create a sample pipeline for data movement scenario.</span><span class="sxs-lookup"><span data-stu-id="0d4da-113">Therefore, we recommend that you use the wizard as a first step to create a sample pipeline for data movement scenario.</span></span> <span data-ttu-id="0d4da-114">This tutorial shows you how to create an Azure data factory, launch the Copy Wizard, go through a series of steps to provide details about your data ingestion/movement scenario.</span><span class="sxs-lookup"><span data-stu-id="0d4da-114">This tutorial shows you how to create an Azure data factory, launch the Copy Wizard, go through a series of steps to provide details about your data ingestion/movement scenario.</span></span> <span data-ttu-id="0d4da-115">When you finish steps in the wizard, the wizard automatically creates a pipeline with a Copy Activity to copy data from an Azure blob storage to an Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="0d4da-115">When you finish steps in the wizard, the wizard automatically creates a pipeline with a Copy Activity to copy data from an Azure blob storage to an Azure SQL database.</span></span> <span data-ttu-id="0d4da-116">See [Data Movement Activities](data-factory-data-movement-activities.md) article for details about the Copy Activity.</span><span class="sxs-lookup"><span data-stu-id="0d4da-116">See [Data Movement Activities](data-factory-data-movement-activities.md) article for details about the Copy Activity.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="0d4da-117">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="0d4da-117">Prerequisites</span></span>
- <span data-ttu-id="0d4da-118">Go through [Tutorial Overview and Pre-requisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) to get an overview of the tutorial and complete the **prerequisite** steps.</span><span class="sxs-lookup"><span data-stu-id="0d4da-118">Go through [Tutorial Overview and Pre-requisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) to get an overview of the tutorial and complete the **prerequisite** steps.</span></span>


## <a name="create-data-factory"></a><span data-ttu-id="0d4da-119">Create data factory</span><span class="sxs-lookup"><span data-stu-id="0d4da-119">Create data factory</span></span>
<span data-ttu-id="0d4da-120">In this step, you use the Azure portal to create an Azure data factory named **ADFTutorialDataFactory**.</span><span class="sxs-lookup"><span data-stu-id="0d4da-120">In this step, you use the Azure portal to create an Azure data factory named **ADFTutorialDataFactory**.</span></span>

1. <span data-ttu-id="0d4da-121">After logging in to the [Azure portal](https://portal.azure.com), click **+ NEW** from the top-left corner, click **Intelligence + analytics**, and click **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="0d4da-121">After logging in to the [Azure portal](https://portal.azure.com), click **+ NEW** from the top-left corner, click **Intelligence + analytics**, and click **Data Factory**.</span></span> 
   
   ![New->DataFactory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-data-wizard-tutorial/new-data-factory-menu.png)
2. <span data-ttu-id="0d4da-123">In the **New data factory** blade:</span><span class="sxs-lookup"><span data-stu-id="0d4da-123">In the **New data factory** blade:</span></span>
   
   1. <span data-ttu-id="0d4da-124">Enter **ADFTutorialDataFactory** for the **name**.</span><span class="sxs-lookup"><span data-stu-id="0d4da-124">Enter **ADFTutorialDataFactory** for the **name**.</span></span>
       <span data-ttu-id="0d4da-125">The name of the Azure data factory must be globally unique.</span><span class="sxs-lookup"><span data-stu-id="0d4da-125">The name of the Azure data factory must be globally unique.</span></span> <span data-ttu-id="0d4da-126">If you receive the error: **Data factory name “ADFTutorialDataFactory” is not available**, change the name of the data factory (for example, yournameADFTutorialDataFactory) and try creating again.</span><span class="sxs-lookup"><span data-stu-id="0d4da-126">If you receive the error: **Data factory name “ADFTutorialDataFactory” is not available**, change the name of the data factory (for example, yournameADFTutorialDataFactory) and try creating again.</span></span> <span data-ttu-id="0d4da-127">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span><span class="sxs-lookup"><span data-stu-id="0d4da-127">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>  
      
       ![Data Factory name not available](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-data-wizard-tutorial/getstarted-data-factory-not-available.png)
      
      > [!NOTE]
      > The name of the data factory may be registered as a DNS name in the future and hence become publically visible.
      > 
      > 
   2. <span data-ttu-id="0d4da-130">Select your Azure **subscription**.</span><span class="sxs-lookup"><span data-stu-id="0d4da-130">Select your Azure **subscription**.</span></span>
   3. <span data-ttu-id="0d4da-131">For Resource Group, do one of the following steps:</span><span class="sxs-lookup"><span data-stu-id="0d4da-131">For Resource Group, do one of the following steps:</span></span> 
      
      - <span data-ttu-id="0d4da-132">Select **Use existing** to select an existing resource group.</span><span class="sxs-lookup"><span data-stu-id="0d4da-132">Select **Use existing** to select an existing resource group.</span></span>
      - <span data-ttu-id="0d4da-133">Select **Create new** to enter a name for a resource group.</span><span class="sxs-lookup"><span data-stu-id="0d4da-133">Select **Create new** to enter a name for a resource group.</span></span>
         
          <span data-ttu-id="0d4da-134">Some of the steps in this tutorial assume that you use the name: **ADFTutorialResourceGroup** for the resource group.</span><span class="sxs-lookup"><span data-stu-id="0d4da-134">Some of the steps in this tutorial assume that you use the name: **ADFTutorialResourceGroup** for the resource group.</span></span> <span data-ttu-id="0d4da-135">To learn about resource groups, see [Using resource groups to manage your Azure resources](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0d4da-135">To learn about resource groups, see [Using resource groups to manage your Azure resources](../azure-resource-manager/resource-group-overview.md).</span></span>
   4. <span data-ttu-id="0d4da-136">Select a **location** for the data factory.</span><span class="sxs-lookup"><span data-stu-id="0d4da-136">Select a **location** for the data factory.</span></span>
   5. <span data-ttu-id="0d4da-137">Select **Pin to dashboard** check box at the bottom of the blade.</span><span class="sxs-lookup"><span data-stu-id="0d4da-137">Select **Pin to dashboard** check box at the bottom of the blade.</span></span>  
   6. <span data-ttu-id="0d4da-138">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="0d4da-138">Click **Create**.</span></span>
      
       ![New data factory blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-data-wizard-tutorial/new-data-factory-blade.png)            
3. <span data-ttu-id="0d4da-140">After the creation is complete, you see the **Data Factory** blade as shown in the following image:</span><span class="sxs-lookup"><span data-stu-id="0d4da-140">After the creation is complete, you see the **Data Factory** blade as shown in the following image:</span></span>
   
   ![Data factory home page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-data-wizard-tutorial/getstarted-data-factory-home-page.png)

## <a name="launch-copy-wizard"></a><span data-ttu-id="0d4da-142">Launch Copy Wizard</span><span class="sxs-lookup"><span data-stu-id="0d4da-142">Launch Copy Wizard</span></span>
1. <span data-ttu-id="0d4da-143">On the Data Factory home page, click the **Copy data** tile to launch **Copy Wizard**.</span><span class="sxs-lookup"><span data-stu-id="0d4da-143">On the Data Factory home page, click the **Copy data** tile to launch **Copy Wizard**.</span></span> 
   
   > [!NOTE]
   > If you see that the web browser is stuck at "Authorizing...", disable/uncheck **Block third party cookies and site data** setting (or) keep it enabled and create an exception for **login.microsoftonline.com** and then try launching the wizard again.
   > 
   > 
2. <span data-ttu-id="0d4da-145">In the **Properties** page:</span><span class="sxs-lookup"><span data-stu-id="0d4da-145">In the **Properties** page:</span></span>
   
   1. <span data-ttu-id="0d4da-146">Enter **CopyFromBlobToAzureSql** for **Task name**</span><span class="sxs-lookup"><span data-stu-id="0d4da-146">Enter **CopyFromBlobToAzureSql** for **Task name**</span></span>
   2. <span data-ttu-id="0d4da-147">Enter **description** (optional).</span><span class="sxs-lookup"><span data-stu-id="0d4da-147">Enter **description** (optional).</span></span>
   3. <span data-ttu-id="0d4da-148">Change the **Start date time** and the **End date time** so that the end date is set to today and start date to five days before the current day.</span><span class="sxs-lookup"><span data-stu-id="0d4da-148">Change the **Start date time** and the **End date time** so that the end date is set to today and start date to five days before the current day.</span></span>  
   4. <span data-ttu-id="0d4da-149">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="0d4da-149">Click **Next**.</span></span>  
      
      ![Copy Tool - Properties page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-data-wizard-tutorial/copy-tool-properties-page.png) 
3. <span data-ttu-id="0d4da-151">On the **Source data store** page, click **Azure Blob Storage** tile.</span><span class="sxs-lookup"><span data-stu-id="0d4da-151">On the **Source data store** page, click **Azure Blob Storage** tile.</span></span> <span data-ttu-id="0d4da-152">You use this page to specify the source data store for the copy task.</span><span class="sxs-lookup"><span data-stu-id="0d4da-152">You use this page to specify the source data store for the copy task.</span></span> <span data-ttu-id="0d4da-153">You can use an existing data store linked service (or) specify a new data store.</span><span class="sxs-lookup"><span data-stu-id="0d4da-153">You can use an existing data store linked service (or) specify a new data store.</span></span> <span data-ttu-id="0d4da-154">To use an existing linked service, you would click **FROM EXISTING LINKED SERVICES** and select the right linked service.</span><span class="sxs-lookup"><span data-stu-id="0d4da-154">To use an existing linked service, you would click **FROM EXISTING LINKED SERVICES** and select the right linked service.</span></span> 
   
    ![Copy Tool - Source data store page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-data-wizard-tutorial/copy-tool-source-data-store-page.png)
4. <span data-ttu-id="0d4da-156">On the **Specify the Azure Blob storage account** page:</span><span class="sxs-lookup"><span data-stu-id="0d4da-156">On the **Specify the Azure Blob storage account** page:</span></span>
   
   1. <span data-ttu-id="0d4da-157">Enter **AzureStorageLinkedService** for **Linked service name**.</span><span class="sxs-lookup"><span data-stu-id="0d4da-157">Enter **AzureStorageLinkedService** for **Linked service name**.</span></span>
   2. <span data-ttu-id="0d4da-158">Confirm that **From Azure subscriptions** option is selected for **Account selection method**.</span><span class="sxs-lookup"><span data-stu-id="0d4da-158">Confirm that **From Azure subscriptions** option is selected for **Account selection method**.</span></span>
   3. <span data-ttu-id="0d4da-159">Select your Azure **subscription**.</span><span class="sxs-lookup"><span data-stu-id="0d4da-159">Select your Azure **subscription**.</span></span>  
   4. <span data-ttu-id="0d4da-160">Select an **Azure storage account** from the list of Azure storage accounts available in the selected subscription.</span><span class="sxs-lookup"><span data-stu-id="0d4da-160">Select an **Azure storage account** from the list of Azure storage accounts available in the selected subscription.</span></span> <span data-ttu-id="0d4da-161">You can also choose to enter storage account settings manually by selecting **Enter manually** option for the **Account selection method**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="0d4da-161">You can also choose to enter storage account settings manually by selecting **Enter manually** option for the **Account selection method**, and then click **Next**.</span></span> 
      
      ![Copy Tool - Specify the Azure Blob storage account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-data-wizard-tutorial/copy-tool-specify-azure-blob-storage-account.png)
5. <span data-ttu-id="0d4da-163">On **Choose the input file or folder** page:</span><span class="sxs-lookup"><span data-stu-id="0d4da-163">On **Choose the input file or folder** page:</span></span>
   
   1. <span data-ttu-id="0d4da-164">Navigate to the **adftutorial** folder.</span><span class="sxs-lookup"><span data-stu-id="0d4da-164">Navigate to the **adftutorial** folder.</span></span>
   2. <span data-ttu-id="0d4da-165">Select **emp.txt**, and click **Choose**</span><span class="sxs-lookup"><span data-stu-id="0d4da-165">Select **emp.txt**, and click **Choose**</span></span>
   3. <span data-ttu-id="0d4da-166">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="0d4da-166">Click **Next**.</span></span> 
      
      ![Copy Tool - Choose the input file or folder](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-data-wizard-tutorial/copy-tool-choose-input-file-or-folder.png)
6. <span data-ttu-id="0d4da-168">On the **Choose the input file or folder** page, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="0d4da-168">On the **Choose the input file or folder** page, click **Next**.</span></span> <span data-ttu-id="0d4da-169">Do not select **Binary copy**.</span><span class="sxs-lookup"><span data-stu-id="0d4da-169">Do not select **Binary copy**.</span></span> 
   
    ![Copy Tool - Choose the input file or folder](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-data-wizard-tutorial/chose-input-file-folder.png) 
7. <span data-ttu-id="0d4da-171">On the **File format settings** page, you see the delimiters and the schema that is auto-detected by the wizard by parsing the file.</span><span class="sxs-lookup"><span data-stu-id="0d4da-171">On the **File format settings** page, you see the delimiters and the schema that is auto-detected by the wizard by parsing the file.</span></span> <span data-ttu-id="0d4da-172">You can also enter the delimiters manually for the copy wizard to stop auto-detecting or to override.</span><span class="sxs-lookup"><span data-stu-id="0d4da-172">You can also enter the delimiters manually for the copy wizard to stop auto-detecting or to override.</span></span> <span data-ttu-id="0d4da-173">Click **Next** after you review the delimiters and preview data.</span><span class="sxs-lookup"><span data-stu-id="0d4da-173">Click **Next** after you review the delimiters and preview data.</span></span> 
   
    ![Copy Tool - File format settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-data-wizard-tutorial/copy-tool-file-format-settings.png)  
8. <span data-ttu-id="0d4da-175">On the Destination data store page, select **Azure SQL Database**, and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="0d4da-175">On the Destination data store page, select **Azure SQL Database**, and click **Next**.</span></span>
   
    ![Copy Tool - Choose destination store](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-data-wizard-tutorial/choose-destination-store.png)
9. <span data-ttu-id="0d4da-177">On **Specify the Azure SQL database** page:</span><span class="sxs-lookup"><span data-stu-id="0d4da-177">On **Specify the Azure SQL database** page:</span></span>
   
   1. <span data-ttu-id="0d4da-178">Enter **AzureSqlLinkedService** for the **Connection name** field.</span><span class="sxs-lookup"><span data-stu-id="0d4da-178">Enter **AzureSqlLinkedService** for the **Connection name** field.</span></span>
   2. <span data-ttu-id="0d4da-179">Confirm that **From Azure subscriptions** option is selected for **Server / database selection method**.</span><span class="sxs-lookup"><span data-stu-id="0d4da-179">Confirm that **From Azure subscriptions** option is selected for **Server / database selection method**.</span></span>
   3. <span data-ttu-id="0d4da-180">Select your Azure **subscription**.</span><span class="sxs-lookup"><span data-stu-id="0d4da-180">Select your Azure **subscription**.</span></span>  
   4. <span data-ttu-id="0d4da-181">Select **Server name** and **Database**.</span><span class="sxs-lookup"><span data-stu-id="0d4da-181">Select **Server name** and **Database**.</span></span>
   5. <span data-ttu-id="0d4da-182">Enter **User name** and **Password**.</span><span class="sxs-lookup"><span data-stu-id="0d4da-182">Enter **User name** and **Password**.</span></span>
   6. <span data-ttu-id="0d4da-183">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="0d4da-183">Click **Next**.</span></span>  
      
      ![Copy Tool - specify Azure SQL database](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-data-wizard-tutorial/specify-azure-sql-database.png)
10. <span data-ttu-id="0d4da-185">On the **Table mapping** page, select **emp** for the **Destination** field from the drop-down list, click **down arrow** (optional) to see the schema and to preview the data.</span><span class="sxs-lookup"><span data-stu-id="0d4da-185">On the **Table mapping** page, select **emp** for the **Destination** field from the drop-down list, click **down arrow** (optional) to see the schema and to preview the data.</span></span>
    
     ![Copy Tool - Table mapping](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-data-wizard-tutorial/copy-tool-table-mapping-page.png) 
11. <span data-ttu-id="0d4da-187">On the **Schema mapping** page, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="0d4da-187">On the **Schema mapping** page, click **Next**.</span></span>
    
    ![Copy Tool - schema mapping](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-data-wizard-tutorial/schema-mapping-page.png)
12. <span data-ttu-id="0d4da-189">On the **Performance settings** page, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="0d4da-189">On the **Performance settings** page, click **Next**.</span></span> 
    
    ![Copy Tool - performance settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-data-wizard-tutorial/performance-settings.png)
13. <span data-ttu-id="0d4da-191">Review information in the **Summary** page, and click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="0d4da-191">Review information in the **Summary** page, and click **Finish**.</span></span> <span data-ttu-id="0d4da-192">The wizard creates two linked services, two datasets (input and output), and one pipeline in the data factory (from where you launched the Copy Wizard).</span><span class="sxs-lookup"><span data-stu-id="0d4da-192">The wizard creates two linked services, two datasets (input and output), and one pipeline in the data factory (from where you launched the Copy Wizard).</span></span> 
    
    ![Copy Tool - performance settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-data-wizard-tutorial/summary-page.png)

## <a name="launch-monitor-and-manage-application"></a><span data-ttu-id="0d4da-194">Launch Monitor and Manage application</span><span class="sxs-lookup"><span data-stu-id="0d4da-194">Launch Monitor and Manage application</span></span>
1. <span data-ttu-id="0d4da-195">On the **Deployment** page, click the link: `Click here to monitor copy pipeline`.</span><span class="sxs-lookup"><span data-stu-id="0d4da-195">On the **Deployment** page, click the link: `Click here to monitor copy pipeline`.</span></span>
   
   ![Copy Tool - Deployment succeeded](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-data-wizard-tutorial/copy-tool-deployment-succeeded.png)  
2. <span data-ttu-id="0d4da-197">Use instructions from [Monitor and manage pipeline using Monitoring App](data-factory-monitor-manage-app.md) to learn about how to monitor the pipeline you created.</span><span class="sxs-lookup"><span data-stu-id="0d4da-197">Use instructions from [Monitor and manage pipeline using Monitoring App](data-factory-monitor-manage-app.md) to learn about how to monitor the pipeline you created.</span></span> <span data-ttu-id="0d4da-198">Click **Refresh** icon in the **ACTIVITY WINDOWS** list to see the slice.</span><span class="sxs-lookup"><span data-stu-id="0d4da-198">Click **Refresh** icon in the **ACTIVITY WINDOWS** list to see the slice.</span></span> 
   
   ![Monitoring App](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-data-wizard-tutorial/monitoring-app.png) 
   
   
   <span data-ttu-id="0d4da-200">Click **Refresh** button in the **ACTIVITY WINDOWS** list at the bottom to see the latest status.</span><span class="sxs-lookup"><span data-stu-id="0d4da-200">Click **Refresh** button in the **ACTIVITY WINDOWS** list at the bottom to see the latest status.</span></span> <span data-ttu-id="0d4da-201">It is not automatically refreshed.</span><span class="sxs-lookup"><span data-stu-id="0d4da-201">It is not automatically refreshed.</span></span> 

> [!NOTE]
> The data pipeline in this tutorial copies data from a source data store to a destination data store. It does not transform input data to produce output data. For a tutorial on how to transform data using Azure Data Factory, see [Tutorial: Build your first pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).
> 
> You can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity. See [Scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md) for detailed information.

## <a name="see-also"></a><span data-ttu-id="0d4da-207">See Also</span><span class="sxs-lookup"><span data-stu-id="0d4da-207">See Also</span></span>
| <span data-ttu-id="0d4da-208">Topic</span><span class="sxs-lookup"><span data-stu-id="0d4da-208">Topic</span></span> | <span data-ttu-id="0d4da-209">Description</span><span class="sxs-lookup"><span data-stu-id="0d4da-209">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="0d4da-210">Pipelines</span><span class="sxs-lookup"><span data-stu-id="0d4da-210">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="0d4da-211">This article helps you understand pipelines and activities in Azure Data Factory and how to use them to construct end-to-end data-driven workflows for your scenario or business.</span><span class="sxs-lookup"><span data-stu-id="0d4da-211">This article helps you understand pipelines and activities in Azure Data Factory and how to use them to construct end-to-end data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="0d4da-212">Datasets</span><span class="sxs-lookup"><span data-stu-id="0d4da-212">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="0d4da-213">This article helps you understand datasets in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="0d4da-213">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="0d4da-214">Scheduling and execution</span><span class="sxs-lookup"><span data-stu-id="0d4da-214">Scheduling and execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="0d4da-215">This article explains the scheduling and execution aspects of Azure Data Factory application model.</span><span class="sxs-lookup"><span data-stu-id="0d4da-215">This article explains the scheduling and execution aspects of Azure Data Factory application model.</span></span> |



















