---
title: Create an Azure data factory using the Azure Data Factory UI | Microsoft Docs
description: Create a data factory with a pipeline that copies data from one location in Azure Blob storage to another location.
services: data-factory
documentationcenter: ''
author: linda33wj
manager: craigg
ms.reviewer: douglasl
ms.service: data-factory
ms.workload: data-services
ms.topic: quickstart
ms.date: 06/20/2018
ms.author: jingwang
ms.openlocfilehash: 0638aaa9165bcf760dabca330f6ee396807e4597
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866901"
---
# <a name="create-a-data-factory-by-using-the-azure-data-factory-ui"></a><span data-ttu-id="aee61-103">Create a data factory by using the Azure Data Factory UI</span><span class="sxs-lookup"><span data-stu-id="aee61-103">Create a data factory by using the Azure Data Factory UI</span></span>
> [!div class="op_single_selector" title1="Select the version of Data Factory service that you are using:"]
> * [Version 1](v1/data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [Current version](quickstart-create-data-factory-portal.md)

<span data-ttu-id="aee61-106">This quickstart describes how to use the Azure Data Factory UI to create and monitor a data factory.</span><span class="sxs-lookup"><span data-stu-id="aee61-106">This quickstart describes how to use the Azure Data Factory UI to create and monitor a data factory.</span></span> <span data-ttu-id="aee61-107">The pipeline that you create in this data factory *copies* data from one folder to another folder in Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="aee61-107">The pipeline that you create in this data factory *copies* data from one folder to another folder in Azure Blob storage.</span></span> <span data-ttu-id="aee61-108">For a tutorial on how to *transform* data by using Azure Data Factory, see [Tutorial: Transform data by using Spark](tutorial-transform-data-spark-portal.md).</span><span class="sxs-lookup"><span data-stu-id="aee61-108">For a tutorial on how to *transform* data by using Azure Data Factory, see [Tutorial: Transform data by using Spark](tutorial-transform-data-spark-portal.md).</span></span> 

> [!NOTE]
> If you are new to Azure Data Factory, see [Introduction to Azure Data Factory](data-factory-introduction.md) before doing this quickstart. 

[!INCLUDE [data-factory-quickstart-prerequisites](../../includes/data-factory-quickstart-prerequisites.md)] 

### <a name="video"></a><span data-ttu-id="aee61-110">Video</span><span class="sxs-lookup"><span data-stu-id="aee61-110">Video</span></span> 
<span data-ttu-id="aee61-111">Watching this video helps you understand the Data Factory UI:</span><span class="sxs-lookup"><span data-stu-id="aee61-111">Watching this video helps you understand the Data Factory UI:</span></span> 
>[!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Visually-build-pipelines-for-Azure-Data-Factory-v2/Player]

## <a name="create-a-data-factory"></a><span data-ttu-id="aee61-112">Create a data factory</span><span class="sxs-lookup"><span data-stu-id="aee61-112">Create a data factory</span></span>

1. <span data-ttu-id="aee61-113">Launch **Microsoft Edge** or **Google Chrome** web browser.</span><span class="sxs-lookup"><span data-stu-id="aee61-113">Launch **Microsoft Edge** or **Google Chrome** web browser.</span></span> <span data-ttu-id="aee61-114">Currently, Data Factory UI is supported only in Microsoft Edge and Google Chrome web browsers.</span><span class="sxs-lookup"><span data-stu-id="aee61-114">Currently, Data Factory UI is supported only in Microsoft Edge and Google Chrome web browsers.</span></span>
1. <span data-ttu-id="aee61-115">Go to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="aee61-115">Go to the [Azure portal](https://portal.azure.com).</span></span> 
1. <span data-ttu-id="aee61-116">Select **New** on the left menu, select **Data + Analytics**, and then select **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="aee61-116">Select **New** on the left menu, select **Data + Analytics**, and then select **Data Factory**.</span></span> 
   
   ![Data Factory selection in the "New" pane](./media/quickstart-create-data-factory-portal/new-azure-data-factory-menu.png)
1. <span data-ttu-id="aee61-118">On the **New data factory** page, enter **ADFTutorialDataFactory** for **Name**.</span><span class="sxs-lookup"><span data-stu-id="aee61-118">On the **New data factory** page, enter **ADFTutorialDataFactory** for **Name**.</span></span> 
      
   !["New data factory" page](./media/quickstart-create-data-factory-portal/new-azure-data-factory.png)
 
   <span data-ttu-id="aee61-120">The name of the Azure data factory must be *globally unique*.</span><span class="sxs-lookup"><span data-stu-id="aee61-120">The name of the Azure data factory must be *globally unique*.</span></span> <span data-ttu-id="aee61-121">If you see the following error, change the name of the data factory (for example, **&lt;yourname&gt;ADFTutorialDataFactory**) and try creating again.</span><span class="sxs-lookup"><span data-stu-id="aee61-121">If you see the following error, change the name of the data factory (for example, **&lt;yourname&gt;ADFTutorialDataFactory**) and try creating again.</span></span> <span data-ttu-id="aee61-122">For naming rules for Data Factory artifacts, see the [Data Factory - naming rules](naming-rules.md) article.</span><span class="sxs-lookup"><span data-stu-id="aee61-122">For naming rules for Data Factory artifacts, see the [Data Factory - naming rules](naming-rules.md) article.</span></span>
  
   ![Error when a name is not available](./media/quickstart-create-data-factory-portal/name-not-available-error.png)
1. <span data-ttu-id="aee61-124">For **Subscription**, select your Azure subscription in which you want to create the data factory.</span><span class="sxs-lookup"><span data-stu-id="aee61-124">For **Subscription**, select your Azure subscription in which you want to create the data factory.</span></span> 
1. <span data-ttu-id="aee61-125">For **Resource Group**, use one of the following steps:</span><span class="sxs-lookup"><span data-stu-id="aee61-125">For **Resource Group**, use one of the following steps:</span></span>
     
   - <span data-ttu-id="aee61-126">Select **Use existing**, and select an existing resource group from the list.</span><span class="sxs-lookup"><span data-stu-id="aee61-126">Select **Use existing**, and select an existing resource group from the list.</span></span> 
   - <span data-ttu-id="aee61-127">Select **Create new**, and enter the name of a resource group.</span><span class="sxs-lookup"><span data-stu-id="aee61-127">Select **Create new**, and enter the name of a resource group.</span></span>   
         
   <span data-ttu-id="aee61-128">To learn about resource groups, see [Using resource groups to manage your Azure resources](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="aee61-128">To learn about resource groups, see [Using resource groups to manage your Azure resources](../azure-resource-manager/resource-group-overview.md).</span></span>  
1. <span data-ttu-id="aee61-129">For **Version**, select **V2**.</span><span class="sxs-lookup"><span data-stu-id="aee61-129">For **Version**, select **V2**.</span></span>
1. <span data-ttu-id="aee61-130">For **Location**, select the location for the data factory.</span><span class="sxs-lookup"><span data-stu-id="aee61-130">For **Location**, select the location for the data factory.</span></span>

   <span data-ttu-id="aee61-131">The list shows only locations that Data Factory supports.</span><span class="sxs-lookup"><span data-stu-id="aee61-131">The list shows only locations that Data Factory supports.</span></span> <span data-ttu-id="aee61-132">The data stores (like Azure Storage and Azure SQL Database) and computes (like Azure HDInsight) that Data Factory uses can be in other locations.</span><span class="sxs-lookup"><span data-stu-id="aee61-132">The data stores (like Azure Storage and Azure SQL Database) and computes (like Azure HDInsight) that Data Factory uses can be in other locations.</span></span>
1. <span data-ttu-id="aee61-133">Select **Pin to dashboard**.</span><span class="sxs-lookup"><span data-stu-id="aee61-133">Select **Pin to dashboard**.</span></span>     
1. <span data-ttu-id="aee61-134">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="aee61-134">Select **Create**.</span></span>
1. <span data-ttu-id="aee61-135">On the dashboard, you see the following tile with the status **Deploying Data Factory**:</span><span class="sxs-lookup"><span data-stu-id="aee61-135">On the dashboard, you see the following tile with the status **Deploying Data Factory**:</span></span> 

   !["Deploying Data Factory" tile](media//quickstart-create-data-factory-portal/deploying-data-factory.png)
1. <span data-ttu-id="aee61-137">After the creation is complete, you see the **Data Factory** page.</span><span class="sxs-lookup"><span data-stu-id="aee61-137">After the creation is complete, you see the **Data Factory** page.</span></span> <span data-ttu-id="aee61-138">Select the **Author & Monitor** tile to start the Azure Data Factory user interface (UI) application on a separate tab.</span><span class="sxs-lookup"><span data-stu-id="aee61-138">Select the **Author & Monitor** tile to start the Azure Data Factory user interface (UI) application on a separate tab.</span></span>
   
   ![Home page for the data factory, with the "Author & Monitor" tile](./media/quickstart-create-data-factory-portal/data-factory-home-page.png)
1. <span data-ttu-id="aee61-140">On the **Let's get started** page, switch to the **Author** tab in the left panel.</span><span class="sxs-lookup"><span data-stu-id="aee61-140">On the **Let's get started** page, switch to the **Author** tab in the left panel.</span></span> 

    !["Let's get started" page](./media/quickstart-create-data-factory-portal/get-started-page.png)

## <a name="create-a-linked-service"></a><span data-ttu-id="aee61-142">Create a linked service</span><span class="sxs-lookup"><span data-stu-id="aee61-142">Create a linked service</span></span>
<span data-ttu-id="aee61-143">In this procedure, you create a linked service to link your Azure storage account to the data factory.</span><span class="sxs-lookup"><span data-stu-id="aee61-143">In this procedure, you create a linked service to link your Azure storage account to the data factory.</span></span> <span data-ttu-id="aee61-144">The linked service has the connection information that the Data Factory service uses at runtime to connect to it.</span><span class="sxs-lookup"><span data-stu-id="aee61-144">The linked service has the connection information that the Data Factory service uses at runtime to connect to it.</span></span>

1. <span data-ttu-id="aee61-145">Select **Connections**, and then select the **New** button on the toolbar.</span><span class="sxs-lookup"><span data-stu-id="aee61-145">Select **Connections**, and then select the **New** button on the toolbar.</span></span> 

   ![Buttons for creating a new connection](./media/quickstart-create-data-factory-portal/new-connection-button.png)    
1. <span data-ttu-id="aee61-147">On the **New Linked Service** page, select **Azure Blob Storage**, and then select **Continue**.</span><span class="sxs-lookup"><span data-stu-id="aee61-147">On the **New Linked Service** page, select **Azure Blob Storage**, and then select **Continue**.</span></span> 

   ![Selecting the "Azure Blob Storage" tile](./media/quickstart-create-data-factory-portal/select-azure-blob-linked-service.png)
1. <span data-ttu-id="aee61-149">Complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="aee61-149">Complete the following steps:</span></span> 

   <span data-ttu-id="aee61-150">a.</span><span class="sxs-lookup"><span data-stu-id="aee61-150">a.</span></span> <span data-ttu-id="aee61-151">For **Name**, enter **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="aee61-151">For **Name**, enter **AzureStorageLinkedService**.</span></span>

   <span data-ttu-id="aee61-152">b.</span><span class="sxs-lookup"><span data-stu-id="aee61-152">b.</span></span> <span data-ttu-id="aee61-153">For **Storage account name**, select the name of your Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="aee61-153">For **Storage account name**, select the name of your Azure storage account.</span></span>

   <span data-ttu-id="aee61-154">c.</span><span class="sxs-lookup"><span data-stu-id="aee61-154">c.</span></span> <span data-ttu-id="aee61-155">Select **Test connection** to confirm that the Data Factory service can connect to the storage account.</span><span class="sxs-lookup"><span data-stu-id="aee61-155">Select **Test connection** to confirm that the Data Factory service can connect to the storage account.</span></span> 

   <span data-ttu-id="aee61-156">d.</span><span class="sxs-lookup"><span data-stu-id="aee61-156">d.</span></span> <span data-ttu-id="aee61-157">Select **Save** to save the linked service.</span><span class="sxs-lookup"><span data-stu-id="aee61-157">Select **Save** to save the linked service.</span></span> 

   ![Azure Storage linked service settings](./media/quickstart-create-data-factory-portal/azure-storage-linked-service.png) 

## <a name="create-datasets"></a><span data-ttu-id="aee61-159">Create datasets</span><span class="sxs-lookup"><span data-stu-id="aee61-159">Create datasets</span></span>
<span data-ttu-id="aee61-160">In this procedure, you create two datasets: **InputDataset** and **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="aee61-160">In this procedure, you create two datasets: **InputDataset** and **OutputDataset**.</span></span> <span data-ttu-id="aee61-161">These datasets are of type **AzureBlob**.</span><span class="sxs-lookup"><span data-stu-id="aee61-161">These datasets are of type **AzureBlob**.</span></span> <span data-ttu-id="aee61-162">They refer to the Azure Storage linked service that you created in the previous section.</span><span class="sxs-lookup"><span data-stu-id="aee61-162">They refer to the Azure Storage linked service that you created in the previous section.</span></span> 

<span data-ttu-id="aee61-163">The input dataset represents the source data in the input folder.</span><span class="sxs-lookup"><span data-stu-id="aee61-163">The input dataset represents the source data in the input folder.</span></span> <span data-ttu-id="aee61-164">In the input dataset definition, you specify the blob container (**adftutorial**), the folder (**input**), and the file (**emp.txt**) that contain the source data.</span><span class="sxs-lookup"><span data-stu-id="aee61-164">In the input dataset definition, you specify the blob container (**adftutorial**), the folder (**input**), and the file (**emp.txt**) that contain the source data.</span></span> 

<span data-ttu-id="aee61-165">The output dataset represents the data that's copied to the destination.</span><span class="sxs-lookup"><span data-stu-id="aee61-165">The output dataset represents the data that's copied to the destination.</span></span> <span data-ttu-id="aee61-166">In the output dataset definition, you specify the blob container (**adftutorial**), the folder (**output**), and the file to which the data is copied.</span><span class="sxs-lookup"><span data-stu-id="aee61-166">In the output dataset definition, you specify the blob container (**adftutorial**), the folder (**output**), and the file to which the data is copied.</span></span> <span data-ttu-id="aee61-167">Each run of a pipeline has a unique ID associated with it.</span><span class="sxs-lookup"><span data-stu-id="aee61-167">Each run of a pipeline has a unique ID associated with it.</span></span> <span data-ttu-id="aee61-168">You can access this ID by using the system variable **RunId**.</span><span class="sxs-lookup"><span data-stu-id="aee61-168">You can access this ID by using the system variable **RunId**.</span></span> <span data-ttu-id="aee61-169">The name of the output file is dynamically evaluated based on the run ID of the pipeline.</span><span class="sxs-lookup"><span data-stu-id="aee61-169">The name of the output file is dynamically evaluated based on the run ID of the pipeline.</span></span>   

<span data-ttu-id="aee61-170">In the linked service settings, you specified the Azure storage account that contains the source data.</span><span class="sxs-lookup"><span data-stu-id="aee61-170">In the linked service settings, you specified the Azure storage account that contains the source data.</span></span> <span data-ttu-id="aee61-171">In the source dataset settings, you specify where exactly the source data resides (blob container, folder, and file).</span><span class="sxs-lookup"><span data-stu-id="aee61-171">In the source dataset settings, you specify where exactly the source data resides (blob container, folder, and file).</span></span> <span data-ttu-id="aee61-172">In the sink dataset settings, you specify where the data is copied to (blob container, folder, and file).</span><span class="sxs-lookup"><span data-stu-id="aee61-172">In the sink dataset settings, you specify where the data is copied to (blob container, folder, and file).</span></span> 
 
1. <span data-ttu-id="aee61-173">Select the **+** (plus) button, and then select **Dataset**.</span><span class="sxs-lookup"><span data-stu-id="aee61-173">Select the **+** (plus) button, and then select **Dataset**.</span></span>

   ![Menu for creating a dataset](./media/quickstart-create-data-factory-portal/new-dataset-menu.png)
1. <span data-ttu-id="aee61-175">On the **New Dataset** page, select **Azure Blob Storage**, and then select **Finish**.</span><span class="sxs-lookup"><span data-stu-id="aee61-175">On the **New Dataset** page, select **Azure Blob Storage**, and then select **Finish**.</span></span> 

   ![Selecting "Azure Blob Storage"](./media/quickstart-create-data-factory-portal/select-azure-blob-dataset.png)
1. <span data-ttu-id="aee61-177">In the **General** tab for the dataset, enter **InputDataset** for **Name**.</span><span class="sxs-lookup"><span data-stu-id="aee61-177">In the **General** tab for the dataset, enter **InputDataset** for **Name**.</span></span> 

1. <span data-ttu-id="aee61-178">Switch to the **Connection** tab and complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="aee61-178">Switch to the **Connection** tab and complete the following steps:</span></span> 

    <span data-ttu-id="aee61-179">a.</span><span class="sxs-lookup"><span data-stu-id="aee61-179">a.</span></span> <span data-ttu-id="aee61-180">For **Linked service**, select **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="aee61-180">For **Linked service**, select **AzureStorageLinkedService**.</span></span>

    <span data-ttu-id="aee61-181">b.</span><span class="sxs-lookup"><span data-stu-id="aee61-181">b.</span></span> <span data-ttu-id="aee61-182">For **File path**, select the **Browse** button.</span><span class="sxs-lookup"><span data-stu-id="aee61-182">For **File path**, select the **Browse** button.</span></span>

    <span data-ttu-id="aee61-183">!["Connection" tab and "Browse" button](./media/quickstart-create-data-factory-portal/file-path-browse-button.png) c.</span><span class="sxs-lookup"><span data-stu-id="aee61-183">!["Connection" tab and "Browse" button](./media/quickstart-create-data-factory-portal/file-path-browse-button.png) c.</span></span> <span data-ttu-id="aee61-184">In the **Choose a file or folder** window, browse to the **input** folder in the **adftutorial** container, select the **emp.txt** file, and then select **Finish**.</span><span class="sxs-lookup"><span data-stu-id="aee61-184">In the **Choose a file or folder** window, browse to the **input** folder in the **adftutorial** container, select the **emp.txt** file, and then select **Finish**.</span></span>

    ![Browse for the input file](./media/quickstart-create-data-factory-portal/choose-file-folder.png)
    
   <span data-ttu-id="aee61-186">d.</span><span class="sxs-lookup"><span data-stu-id="aee61-186">d.</span></span> <span data-ttu-id="aee61-187">(optional) Select **Preview data** to preview the data in the emp.txt file.</span><span class="sxs-lookup"><span data-stu-id="aee61-187">(optional) Select **Preview data** to preview the data in the emp.txt file.</span></span>     
1. <span data-ttu-id="aee61-188">Repeat the steps to create the output dataset:</span><span class="sxs-lookup"><span data-stu-id="aee61-188">Repeat the steps to create the output dataset:</span></span>  

   <span data-ttu-id="aee61-189">a.</span><span class="sxs-lookup"><span data-stu-id="aee61-189">a.</span></span> <span data-ttu-id="aee61-190">Select the **+** (plus) button, and then select **Dataset**.</span><span class="sxs-lookup"><span data-stu-id="aee61-190">Select the **+** (plus) button, and then select **Dataset**.</span></span>

   <span data-ttu-id="aee61-191">b.</span><span class="sxs-lookup"><span data-stu-id="aee61-191">b.</span></span> <span data-ttu-id="aee61-192">On the **New Dataset** page, select **Azure Blob Storage**, and then select **Finish**.</span><span class="sxs-lookup"><span data-stu-id="aee61-192">On the **New Dataset** page, select **Azure Blob Storage**, and then select **Finish**.</span></span>

   <span data-ttu-id="aee61-193">c.</span><span class="sxs-lookup"><span data-stu-id="aee61-193">c.</span></span> <span data-ttu-id="aee61-194">In **General** table, specify **OutputDataset** for the name.</span><span class="sxs-lookup"><span data-stu-id="aee61-194">In **General** table, specify **OutputDataset** for the name.</span></span>

   <span data-ttu-id="aee61-195">d.</span><span class="sxs-lookup"><span data-stu-id="aee61-195">d.</span></span> <span data-ttu-id="aee61-196">In **Connection** tab, select **AzureStorageLinkedService** as linked service, and enter **adftutorial/output** for the folder.</span><span class="sxs-lookup"><span data-stu-id="aee61-196">In **Connection** tab, select **AzureStorageLinkedService** as linked service, and enter **adftutorial/output** for the folder.</span></span> <span data-ttu-id="aee61-197">If the **output** folder does not exist, the copy activity creates it at runtime.</span><span class="sxs-lookup"><span data-stu-id="aee61-197">If the **output** folder does not exist, the copy activity creates it at runtime.</span></span>

## <a name="create-a-pipeline"></a><span data-ttu-id="aee61-198">Create a pipeline</span><span class="sxs-lookup"><span data-stu-id="aee61-198">Create a pipeline</span></span> 
<span data-ttu-id="aee61-199">In this procedure, you create and validate a pipeline with a copy activity that uses the input and output datasets.</span><span class="sxs-lookup"><span data-stu-id="aee61-199">In this procedure, you create and validate a pipeline with a copy activity that uses the input and output datasets.</span></span> <span data-ttu-id="aee61-200">The copy activity copies data from the file you specified in the input dataset settings to the file you specified in the output dataset settings.</span><span class="sxs-lookup"><span data-stu-id="aee61-200">The copy activity copies data from the file you specified in the input dataset settings to the file you specified in the output dataset settings.</span></span> <span data-ttu-id="aee61-201">If the input dataset specifies only a folder (not the file name), the copy activity copies all the files in the source folder to the destination.</span><span class="sxs-lookup"><span data-stu-id="aee61-201">If the input dataset specifies only a folder (not the file name), the copy activity copies all the files in the source folder to the destination.</span></span> 

1. <span data-ttu-id="aee61-202">Select the **+** (plus) button, and then select **Pipeline**.</span><span class="sxs-lookup"><span data-stu-id="aee61-202">Select the **+** (plus) button, and then select **Pipeline**.</span></span> 

   ![Menu for creating a new pipeline](./media/quickstart-create-data-factory-portal/new-pipeline-menu.png)
1. <span data-ttu-id="aee61-204">In the **General** tab, specify **CopyPipeline** for **Name**.</span><span class="sxs-lookup"><span data-stu-id="aee61-204">In the **General** tab, specify **CopyPipeline** for **Name**.</span></span> 

1. <span data-ttu-id="aee61-205">In the **Activities** toolbox, expand **Data Flow**.</span><span class="sxs-lookup"><span data-stu-id="aee61-205">In the **Activities** toolbox, expand **Data Flow**.</span></span> <span data-ttu-id="aee61-206">Drag the **Copy** activity from the **Activities** toolbox to the pipeline designer surface.</span><span class="sxs-lookup"><span data-stu-id="aee61-206">Drag the **Copy** activity from the **Activities** toolbox to the pipeline designer surface.</span></span> <span data-ttu-id="aee61-207">You can also search for activities in the **Activities** toolbox.</span><span class="sxs-lookup"><span data-stu-id="aee61-207">You can also search for activities in the **Activities** toolbox.</span></span> <span data-ttu-id="aee61-208">Specify **CopyFromBlobToBlob** for **Name**.</span><span class="sxs-lookup"><span data-stu-id="aee61-208">Specify **CopyFromBlobToBlob** for **Name**.</span></span>

   ![Copy activity general settings](./media/quickstart-create-data-factory-portal/copy-activity-general-settings.png)
1. <span data-ttu-id="aee61-210">Switch to the **Source** tab in the copy activity settings, and select **InputDataset** for **Source Dataset**.</span><span class="sxs-lookup"><span data-stu-id="aee61-210">Switch to the **Source** tab in the copy activity settings, and select **InputDataset** for **Source Dataset**.</span></span>

1. <span data-ttu-id="aee61-211">Switch to the **Sink** tab in the copy activity settings, and select **OutputDataset** for **Sink Dataset**.</span><span class="sxs-lookup"><span data-stu-id="aee61-211">Switch to the **Sink** tab in the copy activity settings, and select **OutputDataset** for **Sink Dataset**.</span></span>

1. <span data-ttu-id="aee61-212">Click **Validate** on the pipeline toolbar above the canvas to validate the pipeline settings.</span><span class="sxs-lookup"><span data-stu-id="aee61-212">Click **Validate** on the pipeline toolbar above the canvas to validate the pipeline settings.</span></span> <span data-ttu-id="aee61-213">Confirm that the pipeline has been successfully validated.</span><span class="sxs-lookup"><span data-stu-id="aee61-213">Confirm that the pipeline has been successfully validated.</span></span> <span data-ttu-id="aee61-214">To close the validation output, select the **>>** (right arrow) button.</span><span class="sxs-lookup"><span data-stu-id="aee61-214">To close the validation output, select the **>>** (right arrow) button.</span></span> 

## <a name="debug-the-pipeline"></a><span data-ttu-id="aee61-215">Debug the pipeline</span><span class="sxs-lookup"><span data-stu-id="aee61-215">Debug the pipeline</span></span>
<span data-ttu-id="aee61-216">In this step, you debug the pipeline before deploying it to Data Factory.</span><span class="sxs-lookup"><span data-stu-id="aee61-216">In this step, you debug the pipeline before deploying it to Data Factory.</span></span> 

1. <span data-ttu-id="aee61-217">On the pipeline toolbar above the canvas, click **Debug** to trigger a test run.</span><span class="sxs-lookup"><span data-stu-id="aee61-217">On the pipeline toolbar above the canvas, click **Debug** to trigger a test run.</span></span> 
    
1. <span data-ttu-id="aee61-218">Confirm that you see the status of the pipeline run on the **Output** tab of the pipeline settings at the bottom.</span><span class="sxs-lookup"><span data-stu-id="aee61-218">Confirm that you see the status of the pipeline run on the **Output** tab of the pipeline settings at the bottom.</span></span> 

1. <span data-ttu-id="aee61-219">Confirm that you see an output file in the **output** folder of the **adftutorial** container.</span><span class="sxs-lookup"><span data-stu-id="aee61-219">Confirm that you see an output file in the **output** folder of the **adftutorial** container.</span></span> <span data-ttu-id="aee61-220">If the output folder does not exist, the Data Factory service automatically creates it.</span><span class="sxs-lookup"><span data-stu-id="aee61-220">If the output folder does not exist, the Data Factory service automatically creates it.</span></span> 

## <a name="trigger-the-pipeline-manually"></a><span data-ttu-id="aee61-221">Trigger the pipeline manually</span><span class="sxs-lookup"><span data-stu-id="aee61-221">Trigger the pipeline manually</span></span>
<span data-ttu-id="aee61-222">In this procedure, you deploy entities (linked services, datasets, pipelines) to Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="aee61-222">In this procedure, you deploy entities (linked services, datasets, pipelines) to Azure Data Factory.</span></span> <span data-ttu-id="aee61-223">Then, you manually trigger a pipeline run.</span><span class="sxs-lookup"><span data-stu-id="aee61-223">Then, you manually trigger a pipeline run.</span></span> 

1. <span data-ttu-id="aee61-224">Before you trigger a pipeline, you must publish entities to Data Factory.</span><span class="sxs-lookup"><span data-stu-id="aee61-224">Before you trigger a pipeline, you must publish entities to Data Factory.</span></span> <span data-ttu-id="aee61-225">To publish, select **Publish All** on the top.</span><span class="sxs-lookup"><span data-stu-id="aee61-225">To publish, select **Publish All** on the top.</span></span> 

   ![Publish button](./media/quickstart-create-data-factory-portal/publish-button.png)
1. <span data-ttu-id="aee61-227">To trigger the pipeline manually, select **Trigger** on the pipeline toolbar, and then select **Trigger Now**.</span><span class="sxs-lookup"><span data-stu-id="aee61-227">To trigger the pipeline manually, select **Trigger** on the pipeline toolbar, and then select **Trigger Now**.</span></span> 

## <a name="monitor-the-pipeline"></a><span data-ttu-id="aee61-228">Monitor the pipeline</span><span class="sxs-lookup"><span data-stu-id="aee61-228">Monitor the pipeline</span></span>

1. <span data-ttu-id="aee61-229">Switch to the **Monitor** tab on the left.</span><span class="sxs-lookup"><span data-stu-id="aee61-229">Switch to the **Monitor** tab on the left.</span></span> <span data-ttu-id="aee61-230">Use the **Refresh** button to refresh the list.</span><span class="sxs-lookup"><span data-stu-id="aee61-230">Use the **Refresh** button to refresh the list.</span></span>

   ![Tab for monitoring pipeline runs, with "Refresh" button](./media/quickstart-create-data-factory-portal/monitor-trigger-now-pipeline.png)
1. <span data-ttu-id="aee61-232">Select the **View Activity Runs** link under **Actions**.</span><span class="sxs-lookup"><span data-stu-id="aee61-232">Select the **View Activity Runs** link under **Actions**.</span></span> <span data-ttu-id="aee61-233">You see the status of the copy activity run on this page.</span><span class="sxs-lookup"><span data-stu-id="aee61-233">You see the status of the copy activity run on this page.</span></span> 

   ![Pipeline activity runs](./media/quickstart-create-data-factory-portal/pipeline-activity-runs.png)
1. <span data-ttu-id="aee61-235">To view details about the copy operation, select the **Details** (eyeglasses image) link in the **Actions** column.</span><span class="sxs-lookup"><span data-stu-id="aee61-235">To view details about the copy operation, select the **Details** (eyeglasses image) link in the **Actions** column.</span></span> <span data-ttu-id="aee61-236">For details about the properties, see [Copy Activity overview](copy-activity-overview.md).</span><span class="sxs-lookup"><span data-stu-id="aee61-236">For details about the properties, see [Copy Activity overview](copy-activity-overview.md).</span></span> 

   ![Copy operation details](./media/quickstart-create-data-factory-portal/copy-operation-details.png)
1. <span data-ttu-id="aee61-238">Confirm that you see a new file in the **output** folder.</span><span class="sxs-lookup"><span data-stu-id="aee61-238">Confirm that you see a new file in the **output** folder.</span></span> 
1. <span data-ttu-id="aee61-239">You can switch back to the **Pipeline Runs** view from the **Activity Runs** view by selecting the **Pipelines** link.</span><span class="sxs-lookup"><span data-stu-id="aee61-239">You can switch back to the **Pipeline Runs** view from the **Activity Runs** view by selecting the **Pipelines** link.</span></span> 

## <a name="trigger-the-pipeline-on-a-schedule"></a><span data-ttu-id="aee61-240">Trigger the pipeline on a schedule</span><span class="sxs-lookup"><span data-stu-id="aee61-240">Trigger the pipeline on a schedule</span></span>
<span data-ttu-id="aee61-241">This procedure is optional in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="aee61-241">This procedure is optional in this tutorial.</span></span> <span data-ttu-id="aee61-242">You can create a *scheduler trigger* to schedule the pipeline to run periodically (hourly, daily, and so on).</span><span class="sxs-lookup"><span data-stu-id="aee61-242">You can create a *scheduler trigger* to schedule the pipeline to run periodically (hourly, daily, and so on).</span></span> <span data-ttu-id="aee61-243">In this procedure, you create a trigger to run every minute until the end date and time that you specify.</span><span class="sxs-lookup"><span data-stu-id="aee61-243">In this procedure, you create a trigger to run every minute until the end date and time that you specify.</span></span> 

1. <span data-ttu-id="aee61-244">Switch to the **Author** tab.</span><span class="sxs-lookup"><span data-stu-id="aee61-244">Switch to the **Author** tab.</span></span> 

1. <span data-ttu-id="aee61-245">Go to your pipeline, select **Trigger** on the pipeline toolbar, and then select **New/Edit**.</span><span class="sxs-lookup"><span data-stu-id="aee61-245">Go to your pipeline, select **Trigger** on the pipeline toolbar, and then select **New/Edit**.</span></span> 

1. <span data-ttu-id="aee61-246">On the **Add Triggers** page, select **Choose trigger**, and then select **New**.</span><span class="sxs-lookup"><span data-stu-id="aee61-246">On the **Add Triggers** page, select **Choose trigger**, and then select **New**.</span></span> 

1. <span data-ttu-id="aee61-247">On the **New Trigger** page, under **End**, select **On Date**, specify an end time a few minutes after the current time, and then select **Apply**.</span><span class="sxs-lookup"><span data-stu-id="aee61-247">On the **New Trigger** page, under **End**, select **On Date**, specify an end time a few minutes after the current time, and then select **Apply**.</span></span> 

   <span data-ttu-id="aee61-248">A cost is associated with each pipeline run, so specify the end time only minutes apart from the start time.</span><span class="sxs-lookup"><span data-stu-id="aee61-248">A cost is associated with each pipeline run, so specify the end time only minutes apart from the start time.</span></span> <span data-ttu-id="aee61-249">Ensure that it's the same day.</span><span class="sxs-lookup"><span data-stu-id="aee61-249">Ensure that it's the same day.</span></span> <span data-ttu-id="aee61-250">However, ensure that there is enough time for the pipeline to run between the publish time and the end time.</span><span class="sxs-lookup"><span data-stu-id="aee61-250">However, ensure that there is enough time for the pipeline to run between the publish time and the end time.</span></span> <span data-ttu-id="aee61-251">The trigger comes into effect only after you publish the solution to Data Factory, not when you save the trigger in the UI.</span><span class="sxs-lookup"><span data-stu-id="aee61-251">The trigger comes into effect only after you publish the solution to Data Factory, not when you save the trigger in the UI.</span></span> 

   ![Trigger settings](./media/quickstart-create-data-factory-portal/trigger-settings.png)
1. <span data-ttu-id="aee61-253">On the **New Trigger** page, select the **Activated** check box, and then select **Next**.</span><span class="sxs-lookup"><span data-stu-id="aee61-253">On the **New Trigger** page, select the **Activated** check box, and then select **Next**.</span></span> 

   !["Activated" check box and "Next" button](./media/quickstart-create-data-factory-portal/trigger-settings-next.png)
1. <span data-ttu-id="aee61-255">Review the warning message, and select **Finish**.</span><span class="sxs-lookup"><span data-stu-id="aee61-255">Review the warning message, and select **Finish**.</span></span>

   ![Warning and "Finish" button](./media/quickstart-create-data-factory-portal/new-trigger-finish.png)
1. <span data-ttu-id="aee61-257">Select **Publish All** to publish changes to Data Factory.</span><span class="sxs-lookup"><span data-stu-id="aee61-257">Select **Publish All** to publish changes to Data Factory.</span></span> 

1. <span data-ttu-id="aee61-258">Switch to the **Monitor** tab on the left.</span><span class="sxs-lookup"><span data-stu-id="aee61-258">Switch to the **Monitor** tab on the left.</span></span> <span data-ttu-id="aee61-259">Select **Refresh** to refresh the list.</span><span class="sxs-lookup"><span data-stu-id="aee61-259">Select **Refresh** to refresh the list.</span></span> <span data-ttu-id="aee61-260">You see that the pipeline runs once every minute from the publish time to the end time.</span><span class="sxs-lookup"><span data-stu-id="aee61-260">You see that the pipeline runs once every minute from the publish time to the end time.</span></span> 

   <span data-ttu-id="aee61-261">Notice the values in the **Triggered By** column.</span><span class="sxs-lookup"><span data-stu-id="aee61-261">Notice the values in the **Triggered By** column.</span></span> <span data-ttu-id="aee61-262">The manual trigger run was from the step (**Trigger Now**) that you did earlier.</span><span class="sxs-lookup"><span data-stu-id="aee61-262">The manual trigger run was from the step (**Trigger Now**) that you did earlier.</span></span> 

   ![List of triggered runs](./media/quickstart-create-data-factory-portal/monitor-triggered-runs.png)
1. <span data-ttu-id="aee61-264">Select the down arrow next to **Pipeline Runs** to switch to the **Trigger Runs** view.</span><span class="sxs-lookup"><span data-stu-id="aee61-264">Select the down arrow next to **Pipeline Runs** to switch to the **Trigger Runs** view.</span></span> 

   ![Switch to "Trigger Runs" view](./media/quickstart-create-data-factory-portal/monitor-trigger-runs.png)    
1. <span data-ttu-id="aee61-266">Confirm that an output file is created for every pipeline run until the specified end date and time in the **output** folder.</span><span class="sxs-lookup"><span data-stu-id="aee61-266">Confirm that an output file is created for every pipeline run until the specified end date and time in the **output** folder.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="aee61-267">Next steps</span><span class="sxs-lookup"><span data-stu-id="aee61-267">Next steps</span></span>
<span data-ttu-id="aee61-268">The pipeline in this sample copies data from one location to another location in Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="aee61-268">The pipeline in this sample copies data from one location to another location in Azure Blob storage.</span></span> <span data-ttu-id="aee61-269">To learn about using Data Factory in more scenarios, go through the [tutorials](tutorial-copy-data-portal.md).</span><span class="sxs-lookup"><span data-stu-id="aee61-269">To learn about using Data Factory in more scenarios, go through the [tutorials](tutorial-copy-data-portal.md).</span></span> 