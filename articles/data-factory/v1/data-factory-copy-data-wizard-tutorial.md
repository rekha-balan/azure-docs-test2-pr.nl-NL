---
title: 'Tutorial: Create a pipeline using Copy Wizard | Microsoft Docs'
description: In this tutorial, you create an Azure Data Factory pipeline with a Copy Activity by using the Copy Wizard supported by Data Factory
services: data-factory
documentationcenter: ''
author: linda33wj
manager: craigg
ms.assetid: b87afb8e-53b7-4e1b-905b-0343dd096198
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 01/22/2018
ms.author: jingwang
robots: noindex
ms.openlocfilehash: 85cea4bea0b1cff65464a2ad692e500efdc50c10
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856438"
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-data-factory-copy-wizard"></a><span data-ttu-id="2dd38-103">Tutorial: Create a pipeline with Copy Activity using Data Factory Copy Wizard</span><span class="sxs-lookup"><span data-stu-id="2dd38-103">Tutorial: Create a pipeline with Copy Activity using Data Factory Copy Wizard</span></span>
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
> This article applies to version 1 of Data Factory. If you are using the current version of the Data Factory service, see [copy activity tutorial](../quickstart-create-data-factory-dot-net.md). 


<span data-ttu-id="2dd38-114">This tutorial shows you how to use the **Copy Wizard** to copy data from an Azure blob storage to an Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="2dd38-114">This tutorial shows you how to use the **Copy Wizard** to copy data from an Azure blob storage to an Azure SQL database.</span></span> 

<span data-ttu-id="2dd38-115">The Azure Data Factory **Copy Wizard** allows you to quickly create a data pipeline that copies data from a supported source data store to a supported destination data store.</span><span class="sxs-lookup"><span data-stu-id="2dd38-115">The Azure Data Factory **Copy Wizard** allows you to quickly create a data pipeline that copies data from a supported source data store to a supported destination data store.</span></span> <span data-ttu-id="2dd38-116">Therefore, we recommend that you use the wizard as a first step to create a sample pipeline for your data movement scenario.</span><span class="sxs-lookup"><span data-stu-id="2dd38-116">Therefore, we recommend that you use the wizard as a first step to create a sample pipeline for your data movement scenario.</span></span> <span data-ttu-id="2dd38-117">For a list of data stores supported as sources and as destinations, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="2dd38-117">For a list of data stores supported as sources and as destinations, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span>  

<span data-ttu-id="2dd38-118">This tutorial shows you how to create an Azure data factory, launch the Copy Wizard, go through a series of steps to provide details about your data ingestion/movement scenario.</span><span class="sxs-lookup"><span data-stu-id="2dd38-118">This tutorial shows you how to create an Azure data factory, launch the Copy Wizard, go through a series of steps to provide details about your data ingestion/movement scenario.</span></span> <span data-ttu-id="2dd38-119">When you finish steps in the wizard, the wizard automatically creates a pipeline with a Copy Activity to copy data from an Azure blob storage to an Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="2dd38-119">When you finish steps in the wizard, the wizard automatically creates a pipeline with a Copy Activity to copy data from an Azure blob storage to an Azure SQL database.</span></span> <span data-ttu-id="2dd38-120">For more information about Copy Activity, see [data movement activities](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="2dd38-120">For more information about Copy Activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2dd38-121">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="2dd38-121">Prerequisites</span></span>
<span data-ttu-id="2dd38-122">Complete prerequisites listed in the [Tutorial Overview](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) article before performing this tutorial.</span><span class="sxs-lookup"><span data-stu-id="2dd38-122">Complete prerequisites listed in the [Tutorial Overview](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) article before performing this tutorial.</span></span>

## <a name="create-data-factory"></a><span data-ttu-id="2dd38-123">Create data factory</span><span class="sxs-lookup"><span data-stu-id="2dd38-123">Create data factory</span></span>
<span data-ttu-id="2dd38-124">In this step, you use the Azure portal to create an Azure data factory named **ADFTutorialDataFactory**.</span><span class="sxs-lookup"><span data-stu-id="2dd38-124">In this step, you use the Azure portal to create an Azure data factory named **ADFTutorialDataFactory**.</span></span>

1. <span data-ttu-id="2dd38-125">Log in to [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2dd38-125">Log in to [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="2dd38-126">Click **Create a resource** from the top-left corner, click **Data + analytics**, and click **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="2dd38-126">Click **Create a resource** from the top-left corner, click **Data + analytics**, and click **Data Factory**.</span></span> 
   
   ![New->DataFactory](./media/data-factory-copy-data-wizard-tutorial/new-data-factory-menu.png)
2. <span data-ttu-id="2dd38-128">In the **New data factory** blade:</span><span class="sxs-lookup"><span data-stu-id="2dd38-128">In the **New data factory** blade:</span></span>
   
   1. <span data-ttu-id="2dd38-129">Enter **ADFTutorialDataFactory** for the **name**.</span><span class="sxs-lookup"><span data-stu-id="2dd38-129">Enter **ADFTutorialDataFactory** for the **name**.</span></span>
       <span data-ttu-id="2dd38-130">The name of the Azure data factory must be globally unique.</span><span class="sxs-lookup"><span data-stu-id="2dd38-130">The name of the Azure data factory must be globally unique.</span></span> <span data-ttu-id="2dd38-131">If you receive the error: `Data factory name “ADFTutorialDataFactory” is not available`, change the name of the data factory (for example, yournameADFTutorialDataFactoryYYYYMMDD) and try creating again.</span><span class="sxs-lookup"><span data-stu-id="2dd38-131">If you receive the error: `Data factory name “ADFTutorialDataFactory” is not available`, change the name of the data factory (for example, yournameADFTutorialDataFactoryYYYYMMDD) and try creating again.</span></span> <span data-ttu-id="2dd38-132">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span><span class="sxs-lookup"><span data-stu-id="2dd38-132">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>  
      
       ![Data Factory name not available](./media/data-factory-copy-data-wizard-tutorial/getstarted-data-factory-not-available.png)    
   2. <span data-ttu-id="2dd38-134">Select your Azure **subscription**.</span><span class="sxs-lookup"><span data-stu-id="2dd38-134">Select your Azure **subscription**.</span></span>
   3. <span data-ttu-id="2dd38-135">For Resource Group, do one of the following steps:</span><span class="sxs-lookup"><span data-stu-id="2dd38-135">For Resource Group, do one of the following steps:</span></span> 
      
      - <span data-ttu-id="2dd38-136">Select **Use existing** to select an existing resource group.</span><span class="sxs-lookup"><span data-stu-id="2dd38-136">Select **Use existing** to select an existing resource group.</span></span>
      - <span data-ttu-id="2dd38-137">Select **Create new** to enter a name for a resource group.</span><span class="sxs-lookup"><span data-stu-id="2dd38-137">Select **Create new** to enter a name for a resource group.</span></span>
          
        <span data-ttu-id="2dd38-138">Some of the steps in this tutorial assume that you use the name: **ADFTutorialResourceGroup** for the resource group.</span><span class="sxs-lookup"><span data-stu-id="2dd38-138">Some of the steps in this tutorial assume that you use the name: **ADFTutorialResourceGroup** for the resource group.</span></span> <span data-ttu-id="2dd38-139">To learn about resource groups, see [Using resource groups to manage your Azure resources](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2dd38-139">To learn about resource groups, see [Using resource groups to manage your Azure resources](../../azure-resource-manager/resource-group-overview.md).</span></span>
   4. <span data-ttu-id="2dd38-140">Select a **location** for the data factory.</span><span class="sxs-lookup"><span data-stu-id="2dd38-140">Select a **location** for the data factory.</span></span>
   5. <span data-ttu-id="2dd38-141">Select **Pin to dashboard** check box at the bottom of the blade.</span><span class="sxs-lookup"><span data-stu-id="2dd38-141">Select **Pin to dashboard** check box at the bottom of the blade.</span></span>  
   6. <span data-ttu-id="2dd38-142">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="2dd38-142">Click **Create**.</span></span>
      
       ![New data factory blade](media/data-factory-copy-data-wizard-tutorial/new-data-factory-blade.png)            
3. <span data-ttu-id="2dd38-144">After the creation is complete, you see the **Data Factory** blade as shown in the following image:</span><span class="sxs-lookup"><span data-stu-id="2dd38-144">After the creation is complete, you see the **Data Factory** blade as shown in the following image:</span></span>
   
   ![Data factory home page](./media/data-factory-copy-data-wizard-tutorial/getstarted-data-factory-home-page.png)

## <a name="launch-copy-wizard"></a><span data-ttu-id="2dd38-146">Launch Copy Wizard</span><span class="sxs-lookup"><span data-stu-id="2dd38-146">Launch Copy Wizard</span></span>
1. <span data-ttu-id="2dd38-147">On the Data Factory blade, click **Copy data** to launch the **Copy Wizard**.</span><span class="sxs-lookup"><span data-stu-id="2dd38-147">On the Data Factory blade, click **Copy data** to launch the **Copy Wizard**.</span></span> 
   
   > [!NOTE]
   > If you see that the web browser is stuck at "Authorizing...", disable/uncheck **Block third-party cookies and site data** setting in the browser settings (or) keep it enabled and create an exception for **login.microsoftonline.com** and then try launching the wizard again.
2. <span data-ttu-id="2dd38-149">In the **Properties** page:</span><span class="sxs-lookup"><span data-stu-id="2dd38-149">In the **Properties** page:</span></span>
   
   1. <span data-ttu-id="2dd38-150">Enter **CopyFromBlobToAzureSql** for **Task name**</span><span class="sxs-lookup"><span data-stu-id="2dd38-150">Enter **CopyFromBlobToAzureSql** for **Task name**</span></span>
   2. <span data-ttu-id="2dd38-151">Enter **description** (optional).</span><span class="sxs-lookup"><span data-stu-id="2dd38-151">Enter **description** (optional).</span></span>
   3. <span data-ttu-id="2dd38-152">Change the **Start date time** and the **End date time** so that the end date is set to today and start date to five days earlier.</span><span class="sxs-lookup"><span data-stu-id="2dd38-152">Change the **Start date time** and the **End date time** so that the end date is set to today and start date to five days earlier.</span></span>  
   4. <span data-ttu-id="2dd38-153">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="2dd38-153">Click **Next**.</span></span>  
      
      ![Copy Tool - Properties page](./media/data-factory-copy-data-wizard-tutorial/copy-tool-properties-page.png) 
3. <span data-ttu-id="2dd38-155">On the **Source data store** page, click **Azure Blob Storage** tile.</span><span class="sxs-lookup"><span data-stu-id="2dd38-155">On the **Source data store** page, click **Azure Blob Storage** tile.</span></span> <span data-ttu-id="2dd38-156">You use this page to specify the source data store for the copy task.</span><span class="sxs-lookup"><span data-stu-id="2dd38-156">You use this page to specify the source data store for the copy task.</span></span> 
   
    ![Copy Tool - Source data store page](./media/data-factory-copy-data-wizard-tutorial/copy-tool-source-data-store-page.png)
4. <span data-ttu-id="2dd38-158">On the **Specify the Azure Blob storage account** page:</span><span class="sxs-lookup"><span data-stu-id="2dd38-158">On the **Specify the Azure Blob storage account** page:</span></span>
   
   1. <span data-ttu-id="2dd38-159">Enter **AzureStorageLinkedService** for **Linked service name**.</span><span class="sxs-lookup"><span data-stu-id="2dd38-159">Enter **AzureStorageLinkedService** for **Linked service name**.</span></span>
   2. <span data-ttu-id="2dd38-160">Confirm that **From Azure subscriptions** option is selected for **Account selection method**.</span><span class="sxs-lookup"><span data-stu-id="2dd38-160">Confirm that **From Azure subscriptions** option is selected for **Account selection method**.</span></span>
   3. <span data-ttu-id="2dd38-161">Select your Azure **subscription**.</span><span class="sxs-lookup"><span data-stu-id="2dd38-161">Select your Azure **subscription**.</span></span>  
   4. <span data-ttu-id="2dd38-162">Select an **Azure storage account** from the list of Azure storage accounts available in the selected subscription.</span><span class="sxs-lookup"><span data-stu-id="2dd38-162">Select an **Azure storage account** from the list of Azure storage accounts available in the selected subscription.</span></span> <span data-ttu-id="2dd38-163">You can also choose to enter storage account settings manually by selecting **Enter manually** option for the **Account selection method**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="2dd38-163">You can also choose to enter storage account settings manually by selecting **Enter manually** option for the **Account selection method**, and then click **Next**.</span></span> 
      
      ![Copy Tool - Specify the Azure Blob storage account](./media/data-factory-copy-data-wizard-tutorial/copy-tool-specify-azure-blob-storage-account.png)
5. <span data-ttu-id="2dd38-165">On **Choose the input file or folder** page:</span><span class="sxs-lookup"><span data-stu-id="2dd38-165">On **Choose the input file or folder** page:</span></span>
   
   1. <span data-ttu-id="2dd38-166">Double-click **adftutorial** (folder).</span><span class="sxs-lookup"><span data-stu-id="2dd38-166">Double-click **adftutorial** (folder).</span></span>
   2. <span data-ttu-id="2dd38-167">Select **emp.txt**, and click **Choose**</span><span class="sxs-lookup"><span data-stu-id="2dd38-167">Select **emp.txt**, and click **Choose**</span></span>
      
      ![Copy Tool - Choose the input file or folder](./media/data-factory-copy-data-wizard-tutorial/copy-tool-choose-input-file-or-folder.png)
6. <span data-ttu-id="2dd38-169">On the **Choose the input file or folder** page, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="2dd38-169">On the **Choose the input file or folder** page, click **Next**.</span></span> <span data-ttu-id="2dd38-170">Do not select **Binary copy**.</span><span class="sxs-lookup"><span data-stu-id="2dd38-170">Do not select **Binary copy**.</span></span> 
   
    ![Copy Tool - Choose the input file or folder](./media/data-factory-copy-data-wizard-tutorial/chose-input-file-folder.png) 
7. <span data-ttu-id="2dd38-172">On the **File format settings** page, you see the delimiters and the schema that is auto-detected by the wizard by parsing the file.</span><span class="sxs-lookup"><span data-stu-id="2dd38-172">On the **File format settings** page, you see the delimiters and the schema that is auto-detected by the wizard by parsing the file.</span></span> <span data-ttu-id="2dd38-173">You can also enter the delimiters manually for the copy wizard to stop auto-detecting or to override.</span><span class="sxs-lookup"><span data-stu-id="2dd38-173">You can also enter the delimiters manually for the copy wizard to stop auto-detecting or to override.</span></span> <span data-ttu-id="2dd38-174">Click **Next** after you review the delimiters and preview data.</span><span class="sxs-lookup"><span data-stu-id="2dd38-174">Click **Next** after you review the delimiters and preview data.</span></span> 
   
    ![Copy Tool - File format settings](./media/data-factory-copy-data-wizard-tutorial/copy-tool-file-format-settings.png)  
8. <span data-ttu-id="2dd38-176">On the Destination data store page, select **Azure SQL Database**, and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="2dd38-176">On the Destination data store page, select **Azure SQL Database**, and click **Next**.</span></span>
   
    ![Copy Tool - Choose destination store](./media/data-factory-copy-data-wizard-tutorial/choose-destination-store.png)
9. <span data-ttu-id="2dd38-178">On **Specify the Azure SQL database** page:</span><span class="sxs-lookup"><span data-stu-id="2dd38-178">On **Specify the Azure SQL database** page:</span></span>
   
   1. <span data-ttu-id="2dd38-179">Enter **AzureSqlLinkedService** for the **Connection name** field.</span><span class="sxs-lookup"><span data-stu-id="2dd38-179">Enter **AzureSqlLinkedService** for the **Connection name** field.</span></span>
   2. <span data-ttu-id="2dd38-180">Confirm that **From Azure subscriptions** option is selected for **Server / database selection method**.</span><span class="sxs-lookup"><span data-stu-id="2dd38-180">Confirm that **From Azure subscriptions** option is selected for **Server / database selection method**.</span></span>
   3. <span data-ttu-id="2dd38-181">Select your Azure **subscription**.</span><span class="sxs-lookup"><span data-stu-id="2dd38-181">Select your Azure **subscription**.</span></span>  
   4. <span data-ttu-id="2dd38-182">Select **Server name** and **Database**.</span><span class="sxs-lookup"><span data-stu-id="2dd38-182">Select **Server name** and **Database**.</span></span>
   5. <span data-ttu-id="2dd38-183">Enter **User name** and **Password**.</span><span class="sxs-lookup"><span data-stu-id="2dd38-183">Enter **User name** and **Password**.</span></span>
   6. <span data-ttu-id="2dd38-184">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="2dd38-184">Click **Next**.</span></span>  
      
      ![Copy Tool - specify Azure SQL database](./media/data-factory-copy-data-wizard-tutorial/specify-azure-sql-database.png)
10. <span data-ttu-id="2dd38-186">On the **Table mapping** page, select **emp** for the **Destination** field from the drop-down list, click **down arrow** (optional) to see the schema and to preview the data.</span><span class="sxs-lookup"><span data-stu-id="2dd38-186">On the **Table mapping** page, select **emp** for the **Destination** field from the drop-down list, click **down arrow** (optional) to see the schema and to preview the data.</span></span>
    
     ![Copy Tool - Table mapping](./media/data-factory-copy-data-wizard-tutorial/copy-tool-table-mapping-page.png) 
11. <span data-ttu-id="2dd38-188">On the **Schema mapping** page, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="2dd38-188">On the **Schema mapping** page, click **Next**.</span></span>
    
    ![Copy Tool - schema mapping](./media/data-factory-copy-data-wizard-tutorial/schema-mapping-page.png)
12. <span data-ttu-id="2dd38-190">On the **Performance settings** page, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="2dd38-190">On the **Performance settings** page, click **Next**.</span></span> 
    
    ![Copy Tool - performance settings](./media/data-factory-copy-data-wizard-tutorial/performance-settings.png)
13. <span data-ttu-id="2dd38-192">Review information in the **Summary** page, and click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="2dd38-192">Review information in the **Summary** page, and click **Finish**.</span></span> <span data-ttu-id="2dd38-193">The wizard creates two linked services, two datasets (input and output), and one pipeline in the data factory (from where you launched the Copy Wizard).</span><span class="sxs-lookup"><span data-stu-id="2dd38-193">The wizard creates two linked services, two datasets (input and output), and one pipeline in the data factory (from where you launched the Copy Wizard).</span></span> 
    
    ![Copy Tool - performance settings](./media/data-factory-copy-data-wizard-tutorial/summary-page.png)

## <a name="launch-monitor-and-manage-application"></a><span data-ttu-id="2dd38-195">Launch Monitor and Manage application</span><span class="sxs-lookup"><span data-stu-id="2dd38-195">Launch Monitor and Manage application</span></span>
1. <span data-ttu-id="2dd38-196">On the **Deployment** page, click the link: `Click here to monitor copy pipeline`.</span><span class="sxs-lookup"><span data-stu-id="2dd38-196">On the **Deployment** page, click the link: `Click here to monitor copy pipeline`.</span></span>
   
   ![Copy Tool - Deployment succeeded](./media/data-factory-copy-data-wizard-tutorial/copy-tool-deployment-succeeded.png)  
2. <span data-ttu-id="2dd38-198">The monitoring application is launched in a separate tab in your web browser.</span><span class="sxs-lookup"><span data-stu-id="2dd38-198">The monitoring application is launched in a separate tab in your web browser.</span></span>   
   
   ![Monitoring App](./media/data-factory-copy-data-wizard-tutorial/monitoring-app.png)   
3. <span data-ttu-id="2dd38-200">To see the latest status of hourly slices, click **Refresh** button in the **ACTIVITY WINDOWS** list at the bottom.</span><span class="sxs-lookup"><span data-stu-id="2dd38-200">To see the latest status of hourly slices, click **Refresh** button in the **ACTIVITY WINDOWS** list at the bottom.</span></span> <span data-ttu-id="2dd38-201">You see five activity windows for five days between start and end times for the pipeline.</span><span class="sxs-lookup"><span data-stu-id="2dd38-201">You see five activity windows for five days between start and end times for the pipeline.</span></span> <span data-ttu-id="2dd38-202">The list is not automatically refreshed, so you may need to click Refresh a couple of times before you see all the activity windows in the Ready state.</span><span class="sxs-lookup"><span data-stu-id="2dd38-202">The list is not automatically refreshed, so you may need to click Refresh a couple of times before you see all the activity windows in the Ready state.</span></span> 
4. <span data-ttu-id="2dd38-203">Select an activity window in the list.</span><span class="sxs-lookup"><span data-stu-id="2dd38-203">Select an activity window in the list.</span></span> <span data-ttu-id="2dd38-204">See the details about it in the **Activity Window Explorer** on the right.</span><span class="sxs-lookup"><span data-stu-id="2dd38-204">See the details about it in the **Activity Window Explorer** on the right.</span></span>

    ![Activity window details](media/data-factory-copy-data-wizard-tutorial/activity-window-details.png)    

    <span data-ttu-id="2dd38-206">Notice that the dates 11, 12, 13, 14, and 15 are in green color, which means that the daily output slices for these dates have already been produced.</span><span class="sxs-lookup"><span data-stu-id="2dd38-206">Notice that the dates 11, 12, 13, 14, and 15 are in green color, which means that the daily output slices for these dates have already been produced.</span></span> <span data-ttu-id="2dd38-207">You also see this color coding on the pipeline and the output dataset in the diagram view.</span><span class="sxs-lookup"><span data-stu-id="2dd38-207">You also see this color coding on the pipeline and the output dataset in the diagram view.</span></span> <span data-ttu-id="2dd38-208">In the previous step, notice that two slices have already been produced, one slice is currently being processed, and the other two are waiting to be processed (based on the color coding).</span><span class="sxs-lookup"><span data-stu-id="2dd38-208">In the previous step, notice that two slices have already been produced, one slice is currently being processed, and the other two are waiting to be processed (based on the color coding).</span></span> 

    <span data-ttu-id="2dd38-209">For more information on using this application, see [Monitor and manage pipeline using Monitoring App](data-factory-monitor-manage-app.md) article.</span><span class="sxs-lookup"><span data-stu-id="2dd38-209">For more information on using this application, see [Monitor and manage pipeline using Monitoring App](data-factory-monitor-manage-app.md) article.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2dd38-210">Next steps</span><span class="sxs-lookup"><span data-stu-id="2dd38-210">Next steps</span></span>
<span data-ttu-id="2dd38-211">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span><span class="sxs-lookup"><span data-stu-id="2dd38-211">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="2dd38-212">The following table provides a list of data stores supported as sources and destinations by the copy activity:</span><span class="sxs-lookup"><span data-stu-id="2dd38-212">The following table provides a list of data stores supported as sources and destinations by the copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="2dd38-213">For details about fields/properties that you see in the copy wizard for a data store, click the link for the data store in the table.</span><span class="sxs-lookup"><span data-stu-id="2dd38-213">For details about fields/properties that you see in the copy wizard for a data store, click the link for the data store in the table.</span></span> 