---
title: Copy data by using the Azure Copy Data tool | Microsoft Docs
description: Create an Azure data factory and then use the Copy Data tool to copy data from one location in Azure Blob storage to another location.
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
ms.openlocfilehash: d314c04a40155fccc99660bacdb9f646ce77b22f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866467"
---
# <a name="use-the-copy-data-tool-to-copy-data"></a><span data-ttu-id="f8394-103">Use the Copy Data tool to copy data</span><span class="sxs-lookup"><span data-stu-id="f8394-103">Use the Copy Data tool to copy data</span></span> 
> [!div class="op_single_selector" title1="Select the version of Data Factory service that you are using:"]
> * [Version 1](v1/data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [Current version](quickstart-create-data-factory-copy-data-tool.md)

<span data-ttu-id="f8394-106">In this quickstart, you use the Azure portal to create a data factory.</span><span class="sxs-lookup"><span data-stu-id="f8394-106">In this quickstart, you use the Azure portal to create a data factory.</span></span> <span data-ttu-id="f8394-107">Then, you use the Copy Data tool to create a pipeline that copies data from a folder in Azure Blob storage to another folder.</span><span class="sxs-lookup"><span data-stu-id="f8394-107">Then, you use the Copy Data tool to create a pipeline that copies data from a folder in Azure Blob storage to another folder.</span></span> 

> [!NOTE]
> If you are new to Azure Data Factory, see [Introduction to Azure Data Factory](data-factory-introduction.md) before doing this quickstart. 

[!INCLUDE [data-factory-quickstart-prerequisites](../../includes/data-factory-quickstart-prerequisites.md)] 

## <a name="create-a-data-factory"></a><span data-ttu-id="f8394-109">Create a data factory</span><span class="sxs-lookup"><span data-stu-id="f8394-109">Create a data factory</span></span>

1. <span data-ttu-id="f8394-110">Select **New** on the left menu, select **Data + Analytics**, and then select **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="f8394-110">Select **New** on the left menu, select **Data + Analytics**, and then select **Data Factory**.</span></span> 
   
   ![Data Factory selection in the "New" pane](./media/quickstart-create-data-factory-copy-data-tool/new-azure-data-factory-menu.png)
1. <span data-ttu-id="f8394-112">On the **New data factory** page, enter **ADFTutorialDataFactory** for **Name**.</span><span class="sxs-lookup"><span data-stu-id="f8394-112">On the **New data factory** page, enter **ADFTutorialDataFactory** for **Name**.</span></span> 
      
   !["New data factory" page](./media/quickstart-create-data-factory-copy-data-tool/new-azure-data-factory.png)
 
   <span data-ttu-id="f8394-114">The name of the Azure data factory must be *globally unique*.</span><span class="sxs-lookup"><span data-stu-id="f8394-114">The name of the Azure data factory must be *globally unique*.</span></span> <span data-ttu-id="f8394-115">If you see the following error, change the name of the data factory (for example, **&lt;yourname&gt;ADFTutorialDataFactory**) and try creating again.</span><span class="sxs-lookup"><span data-stu-id="f8394-115">If you see the following error, change the name of the data factory (for example, **&lt;yourname&gt;ADFTutorialDataFactory**) and try creating again.</span></span> <span data-ttu-id="f8394-116">For naming rules for Data Factory artifacts, see the [Data Factory - naming rules](naming-rules.md) article.</span><span class="sxs-lookup"><span data-stu-id="f8394-116">For naming rules for Data Factory artifacts, see the [Data Factory - naming rules](naming-rules.md) article.</span></span>
  
   ![Error when a name is not available](./media/quickstart-create-data-factory-portal/name-not-available-error.png)
1. <span data-ttu-id="f8394-118">For **Subscription**, select your Azure subscription in which you want to create the data factory.</span><span class="sxs-lookup"><span data-stu-id="f8394-118">For **Subscription**, select your Azure subscription in which you want to create the data factory.</span></span> 
1. <span data-ttu-id="f8394-119">For **Resource Group**, use one of the following steps:</span><span class="sxs-lookup"><span data-stu-id="f8394-119">For **Resource Group**, use one of the following steps:</span></span>
     
   - <span data-ttu-id="f8394-120">Select **Use existing**, and select an existing resource group from the list.</span><span class="sxs-lookup"><span data-stu-id="f8394-120">Select **Use existing**, and select an existing resource group from the list.</span></span> 
   - <span data-ttu-id="f8394-121">Select **Create new**, and enter the name of a resource group.</span><span class="sxs-lookup"><span data-stu-id="f8394-121">Select **Create new**, and enter the name of a resource group.</span></span>   
         
   <span data-ttu-id="f8394-122">To learn about resource groups, see [Using resource groups to manage your Azure resources](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f8394-122">To learn about resource groups, see [Using resource groups to manage your Azure resources](../azure-resource-manager/resource-group-overview.md).</span></span>  
1. <span data-ttu-id="f8394-123">For **Version**, select **V2**.</span><span class="sxs-lookup"><span data-stu-id="f8394-123">For **Version**, select **V2**.</span></span>
1. <span data-ttu-id="f8394-124">For **Location**, select the location for the data factory.</span><span class="sxs-lookup"><span data-stu-id="f8394-124">For **Location**, select the location for the data factory.</span></span> 

   <span data-ttu-id="f8394-125">The list shows only supported locations.</span><span class="sxs-lookup"><span data-stu-id="f8394-125">The list shows only supported locations.</span></span> <span data-ttu-id="f8394-126">The data stores (like Azure Storage and Azure SQL Database) and computes (like Azure HDInsight) that Data Factory uses can be in other locations/regions.</span><span class="sxs-lookup"><span data-stu-id="f8394-126">The data stores (like Azure Storage and Azure SQL Database) and computes (like Azure HDInsight) that Data Factory uses can be in other locations/regions.</span></span>

1. <span data-ttu-id="f8394-127">Select **Pin to dashboard**.</span><span class="sxs-lookup"><span data-stu-id="f8394-127">Select **Pin to dashboard**.</span></span>     
1. <span data-ttu-id="f8394-128">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="f8394-128">Select **Create**.</span></span>
1. <span data-ttu-id="f8394-129">On the dashboard, you see the following tile with the status **Deploying Data Factory**:</span><span class="sxs-lookup"><span data-stu-id="f8394-129">On the dashboard, you see the following tile with the status **Deploying Data Factory**:</span></span> 

    !["Deploying Data Factory" tile](media/quickstart-create-data-factory-copy-data-tool/deploying-data-factory.png)
1. <span data-ttu-id="f8394-131">After the creation is complete, you see the **Data Factory** page.</span><span class="sxs-lookup"><span data-stu-id="f8394-131">After the creation is complete, you see the **Data Factory** page.</span></span> <span data-ttu-id="f8394-132">Select the **Author & Monitor** tile to start the Azure Data Factory user interface (UI) application on a separate tab.</span><span class="sxs-lookup"><span data-stu-id="f8394-132">Select the **Author & Monitor** tile to start the Azure Data Factory user interface (UI) application on a separate tab.</span></span>
   
   ![Home page for the data factory, with the "Author & Monitor" tile](./media/quickstart-create-data-factory-copy-data-tool/data-factory-home-page.png)

## <a name="start-the-copy-data-tool"></a><span data-ttu-id="f8394-134">Start the Copy Data tool</span><span class="sxs-lookup"><span data-stu-id="f8394-134">Start the Copy Data tool</span></span>

1. <span data-ttu-id="f8394-135">On the **Let's get started** page, select the **Copy Data** tile to start the Copy Data tool.</span><span class="sxs-lookup"><span data-stu-id="f8394-135">On the **Let's get started** page, select the **Copy Data** tile to start the Copy Data tool.</span></span> 

   !["Copy Data" tile](./media/quickstart-create-data-factory-copy-data-tool/copy-data-tool-tile.png)

1. <span data-ttu-id="f8394-137">On the **Properties** page of the Copy Data tool, you can specify a name for the pipeline and its description, then select **Next**.</span><span class="sxs-lookup"><span data-stu-id="f8394-137">On the **Properties** page of the Copy Data tool, you can specify a name for the pipeline and its description, then select **Next**.</span></span> 

   !["Properties" page](./media/quickstart-create-data-factory-copy-data-tool/copy-data-tool-properties-page.png)
1. <span data-ttu-id="f8394-139">On the **Source data store** page, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="f8394-139">On the **Source data store** page, complete the following steps:</span></span>

    <span data-ttu-id="f8394-140">a.</span><span class="sxs-lookup"><span data-stu-id="f8394-140">a.</span></span> <span data-ttu-id="f8394-141">Click **+ Create new connection** to add a connection.</span><span class="sxs-lookup"><span data-stu-id="f8394-141">Click **+ Create new connection** to add a connection.</span></span>

    !["Source data store" page](./media/quickstart-create-data-factory-copy-data-tool/new-source-linked-service.png)

    <span data-ttu-id="f8394-143">b.</span><span class="sxs-lookup"><span data-stu-id="f8394-143">b.</span></span> <span data-ttu-id="f8394-144">Select **Azure Blob Storage** from the gallery, and then select **Next**.</span><span class="sxs-lookup"><span data-stu-id="f8394-144">Select **Azure Blob Storage** from the gallery, and then select **Next**.</span></span>

    ![Select blob storage from gallery](./media/quickstart-create-data-factory-copy-data-tool/select-blob-source.png)

    <span data-ttu-id="f8394-146">c.</span><span class="sxs-lookup"><span data-stu-id="f8394-146">c.</span></span> <span data-ttu-id="f8394-147">On the **Specify the Azure Blob storage account** page, select your storage account from the **Storage account name** list, and then select **Finish**.</span><span class="sxs-lookup"><span data-stu-id="f8394-147">On the **Specify the Azure Blob storage account** page, select your storage account from the **Storage account name** list, and then select **Finish**.</span></span> 

   ![Configure the Azure Blob storage account](./media/quickstart-create-data-factory-copy-data-tool/configure-blob-storage.png)

   <span data-ttu-id="f8394-149">d.</span><span class="sxs-lookup"><span data-stu-id="f8394-149">d.</span></span> <span data-ttu-id="f8394-150">Select the newly created linked service as source, then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="f8394-150">Select the newly created linked service as source, then click **Next**.</span></span>

   ![Select source linked service](./media/quickstart-create-data-factory-copy-data-tool/select-source-linked-service.png)


1. <span data-ttu-id="f8394-152">On the **Choose the input file or folder** page, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="f8394-152">On the **Choose the input file or folder** page, complete the following steps:</span></span>

   <span data-ttu-id="f8394-153">a.</span><span class="sxs-lookup"><span data-stu-id="f8394-153">a.</span></span> <span data-ttu-id="f8394-154">Click **Browse** to navigate to the **adftutorial/input** folder, select the **emp.txt** file, then click **Choose**.</span><span class="sxs-lookup"><span data-stu-id="f8394-154">Click **Browse** to navigate to the **adftutorial/input** folder, select the **emp.txt** file, then click **Choose**.</span></span> 

   !["Choose the input file or folder" page](./media/quickstart-create-data-factory-copy-data-tool/configure-source-path.png)

   <span data-ttu-id="f8394-156">d.</span><span class="sxs-lookup"><span data-stu-id="f8394-156">d.</span></span> <span data-ttu-id="f8394-157">Check the **Binary copy** option to copy file as-is, then select **Next**.</span><span class="sxs-lookup"><span data-stu-id="f8394-157">Check the **Binary copy** option to copy file as-is, then select **Next**.</span></span> 

   !["Choose the input file or folder" page](./media/quickstart-create-data-factory-copy-data-tool/select-binary-copy.png)


1. <span data-ttu-id="f8394-159">On the **Destination data store** page, select the **Azure Blob Storage** linked service you just created, and then select **Next**.</span><span class="sxs-lookup"><span data-stu-id="f8394-159">On the **Destination data store** page, select the **Azure Blob Storage** linked service you just created, and then select **Next**.</span></span> 

   !["Destination data store" page](./media/quickstart-create-data-factory-copy-data-tool/select-sink-linked-service.png)

1. <span data-ttu-id="f8394-161">On the **Choose the output file or folder** page, enter **adftutorial/output** for the folder path, then select **Next**.</span><span class="sxs-lookup"><span data-stu-id="f8394-161">On the **Choose the output file or folder** page, enter **adftutorial/output** for the folder path, then select **Next**.</span></span> 

   !["Choose the output file or folder" page](./media/quickstart-create-data-factory-copy-data-tool/configure-sink-path.png) 

1. <span data-ttu-id="f8394-163">On the **Settings** page, select **Next** to use the default configurations.</span><span class="sxs-lookup"><span data-stu-id="f8394-163">On the **Settings** page, select **Next** to use the default configurations.</span></span> 

1. <span data-ttu-id="f8394-164">On the **Summary** page, review all settings, and select **Next**.</span><span class="sxs-lookup"><span data-stu-id="f8394-164">On the **Summary** page, review all settings, and select **Next**.</span></span> 

    !["Summary" page](./media/quickstart-create-data-factory-copy-data-tool/summary-page.png)

1. <span data-ttu-id="f8394-166">On the **Deployment complete** page, select **Monitor** to monitor the pipeline that you created.</span><span class="sxs-lookup"><span data-stu-id="f8394-166">On the **Deployment complete** page, select **Monitor** to monitor the pipeline that you created.</span></span> 

    !["Deployment complete" page](./media/quickstart-create-data-factory-copy-data-tool/deployment-page.png)

1. <span data-ttu-id="f8394-168">The application switches to the **Monitor** tab. You see the status of the pipeline on this tab. Select **Refresh** to refresh the list.</span><span class="sxs-lookup"><span data-stu-id="f8394-168">The application switches to the **Monitor** tab. You see the status of the pipeline on this tab. Select **Refresh** to refresh the list.</span></span> 
    
    ![Monitor pipeline run](./media/quickstart-create-data-factory-copy-data-tool/pipeline-monitoring.png)

1. <span data-ttu-id="f8394-170">Select the **View Activity Runs** link in the **Actions** column.</span><span class="sxs-lookup"><span data-stu-id="f8394-170">Select the **View Activity Runs** link in the **Actions** column.</span></span> <span data-ttu-id="f8394-171">The pipeline has only one activity of type **Copy**.</span><span class="sxs-lookup"><span data-stu-id="f8394-171">The pipeline has only one activity of type **Copy**.</span></span> 

    ![Monitor activity run](./media/quickstart-create-data-factory-copy-data-tool/activity-monitoring.png)
    
1. <span data-ttu-id="f8394-173">To view details about the copy operation, select the **Details** (eyeglasses image) link in the **Actions** column.</span><span class="sxs-lookup"><span data-stu-id="f8394-173">To view details about the copy operation, select the **Details** (eyeglasses image) link in the **Actions** column.</span></span> <span data-ttu-id="f8394-174">For details about the properties, see [Copy Activity overview](copy-activity-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f8394-174">For details about the properties, see [Copy Activity overview](copy-activity-overview.md).</span></span>

    ![Copy operation details](./media/quickstart-create-data-factory-copy-data-tool/activity-execution-details.png)

1. <span data-ttu-id="f8394-176">Verify that the **emp.txt** file is created in the **output** folder of the **adftutorial** container.</span><span class="sxs-lookup"><span data-stu-id="f8394-176">Verify that the **emp.txt** file is created in the **output** folder of the **adftutorial** container.</span></span> <span data-ttu-id="f8394-177">If the output folder does not exist, the Data Factory service automatically creates it.</span><span class="sxs-lookup"><span data-stu-id="f8394-177">If the output folder does not exist, the Data Factory service automatically creates it.</span></span> 

1. <span data-ttu-id="f8394-178">Switch to the **Author** tab above the **Monitor** tab on the left panel so that you can edit linked services, datasets, and pipelines.</span><span class="sxs-lookup"><span data-stu-id="f8394-178">Switch to the **Author** tab above the **Monitor** tab on the left panel so that you can edit linked services, datasets, and pipelines.</span></span> <span data-ttu-id="f8394-179">To learn about editing them in the Data Factory UI, see [Create a data factory by using the Azure portal](quickstart-create-data-factory-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f8394-179">To learn about editing them in the Data Factory UI, see [Create a data factory by using the Azure portal](quickstart-create-data-factory-portal.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f8394-180">Next steps</span><span class="sxs-lookup"><span data-stu-id="f8394-180">Next steps</span></span>
<span data-ttu-id="f8394-181">The pipeline in this sample copies data from one location to another location in Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="f8394-181">The pipeline in this sample copies data from one location to another location in Azure Blob storage.</span></span> <span data-ttu-id="f8394-182">To learn about using Data Factory in more scenarios, go through the [tutorials](tutorial-copy-data-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f8394-182">To learn about using Data Factory in more scenarios, go through the [tutorials](tutorial-copy-data-portal.md).</span></span> 