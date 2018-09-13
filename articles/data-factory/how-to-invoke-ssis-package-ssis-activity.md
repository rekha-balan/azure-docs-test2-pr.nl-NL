---
title: Run SSIS package with Execute SSIS Package Activity - Azure | Microsoft Docs
description: This article describes how to run a SQL Server Integration Services (SSIS) package in an Azure Data Factory pipeline by using the Execute SSIS Package Activity.
services: data-factory
documentationcenter: ''
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: ''
ms.devlang: powershell
ms.topic: conceptual
ms.date: 07/16/2018
author: swinarko
ms.author: sawinark
ms.reviewer: douglasl
manager: craigg
ms.openlocfilehash: 3a43c0cd13300918979ae03c7f6c703796b65dc9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867750"
---
# <a name="run-an-ssis-package-with-the-execute-ssis-package-activity-in-azure-data-factory"></a><span data-ttu-id="71e87-103">Run an SSIS package with the Execute SSIS Package Activity in Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="71e87-103">Run an SSIS package with the Execute SSIS Package Activity in Azure Data Factory</span></span>
<span data-ttu-id="71e87-104">This article describes how to run an SSIS package in an Azure Data Factory pipeline by using an Execute SSIS Package activity.</span><span class="sxs-lookup"><span data-stu-id="71e87-104">This article describes how to run an SSIS package in an Azure Data Factory pipeline by using an Execute SSIS Package activity.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="71e87-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="71e87-105">Prerequisites</span></span>

<span data-ttu-id="71e87-106">**Azure SQL Database**.</span><span class="sxs-lookup"><span data-stu-id="71e87-106">**Azure SQL Database**.</span></span> <span data-ttu-id="71e87-107">The walkthrough in this article uses an Azure SQL database that hosts the SSIS catalog.</span><span class="sxs-lookup"><span data-stu-id="71e87-107">The walkthrough in this article uses an Azure SQL database that hosts the SSIS catalog.</span></span> <span data-ttu-id="71e87-108">You can also use an Azure SQL Managed Instance (Preview).</span><span class="sxs-lookup"><span data-stu-id="71e87-108">You can also use an Azure SQL Managed Instance (Preview).</span></span>

## <a name="create-an-azure-ssis-integration-runtime"></a><span data-ttu-id="71e87-109">Create an Azure-SSIS integration runtime</span><span class="sxs-lookup"><span data-stu-id="71e87-109">Create an Azure-SSIS integration runtime</span></span>
<span data-ttu-id="71e87-110">Create an Azure-SSIS integration runtime if you don't have one by following the step-by-step instruction in the [Tutorial: Deploy SSIS packages](tutorial-create-azure-ssis-runtime-portal.md).</span><span class="sxs-lookup"><span data-stu-id="71e87-110">Create an Azure-SSIS integration runtime if you don't have one by following the step-by-step instruction in the [Tutorial: Deploy SSIS packages](tutorial-create-azure-ssis-runtime-portal.md).</span></span>

## <a name="run-a-package-in-the-azure-portal"></a><span data-ttu-id="71e87-111">Run a package in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="71e87-111">Run a package in the Azure portal</span></span>
<span data-ttu-id="71e87-112">In this section, you use Data Factory UI to create a Data Factory pipeline with an Execute SSIS Package activity that runs an SSIS package.</span><span class="sxs-lookup"><span data-stu-id="71e87-112">In this section, you use Data Factory UI to create a Data Factory pipeline with an Execute SSIS Package activity that runs an SSIS package.</span></span>

### <a name="create-a-data-factory"></a><span data-ttu-id="71e87-113">Create a data factory</span><span class="sxs-lookup"><span data-stu-id="71e87-113">Create a data factory</span></span>
<span data-ttu-id="71e87-114">First step is to create a data factory by using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="71e87-114">First step is to create a data factory by using the Azure portal.</span></span> 

1. <span data-ttu-id="71e87-115">Launch **Microsoft Edge** or **Google Chrome** web browser.</span><span class="sxs-lookup"><span data-stu-id="71e87-115">Launch **Microsoft Edge** or **Google Chrome** web browser.</span></span> <span data-ttu-id="71e87-116">Currently, Data Factory UI is supported only in Microsoft Edge and Google Chrome web browsers.</span><span class="sxs-lookup"><span data-stu-id="71e87-116">Currently, Data Factory UI is supported only in Microsoft Edge and Google Chrome web browsers.</span></span>
2. <span data-ttu-id="71e87-117">Navigate to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="71e87-117">Navigate to the [Azure portal](https://portal.azure.com).</span></span> 
3. <span data-ttu-id="71e87-118">Click **New** on the left menu, click **Data + Analytics**, and click **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="71e87-118">Click **New** on the left menu, click **Data + Analytics**, and click **Data Factory**.</span></span> 
   
   ![New->DataFactory](./media/how-to-invoke-ssis-package-stored-procedure-activity/new-azure-data-factory-menu.png)
2. <span data-ttu-id="71e87-120">In the **New data factory** page, enter **ADFTutorialDataFactory** for the **name**.</span><span class="sxs-lookup"><span data-stu-id="71e87-120">In the **New data factory** page, enter **ADFTutorialDataFactory** for the **name**.</span></span> 
      
     ![New data factory page](./media/how-to-invoke-ssis-package-stored-procedure-activity/new-azure-data-factory.png)
 
   <span data-ttu-id="71e87-122">The name of the Azure data factory must be **globally unique**.</span><span class="sxs-lookup"><span data-stu-id="71e87-122">The name of the Azure data factory must be **globally unique**.</span></span> <span data-ttu-id="71e87-123">If you see the following error for the name field, change the name of the data factory (for example, yournameADFTutorialDataFactory).</span><span class="sxs-lookup"><span data-stu-id="71e87-123">If you see the following error for the name field, change the name of the data factory (for example, yournameADFTutorialDataFactory).</span></span> <span data-ttu-id="71e87-124">See [Data Factory - Naming Rules](naming-rules.md) article for naming rules for Data Factory artifacts.</span><span class="sxs-lookup"><span data-stu-id="71e87-124">See [Data Factory - Naming Rules](naming-rules.md) article for naming rules for Data Factory artifacts.</span></span>
  
     ![Name not available - error](./media/how-to-invoke-ssis-package-stored-procedure-activity/name-not-available-error.png)
3. <span data-ttu-id="71e87-126">Select your Azure **subscription** in which you want to create the data factory.</span><span class="sxs-lookup"><span data-stu-id="71e87-126">Select your Azure **subscription** in which you want to create the data factory.</span></span> 
4. <span data-ttu-id="71e87-127">For the **Resource Group**, do one of the following steps:</span><span class="sxs-lookup"><span data-stu-id="71e87-127">For the **Resource Group**, do one of the following steps:</span></span>
     
      - <span data-ttu-id="71e87-128">Select **Use existing**, and select an existing resource group from the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="71e87-128">Select **Use existing**, and select an existing resource group from the drop-down list.</span></span> 
      - <span data-ttu-id="71e87-129">Select **Create new**, and enter the name of a resource group.</span><span class="sxs-lookup"><span data-stu-id="71e87-129">Select **Create new**, and enter the name of a resource group.</span></span>   
         
    <span data-ttu-id="71e87-130">To learn about resource groups, see [Using resource groups to manage your Azure resources](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="71e87-130">To learn about resource groups, see [Using resource groups to manage your Azure resources](../azure-resource-manager/resource-group-overview.md).</span></span>  
4. <span data-ttu-id="71e87-131">Select **V2** for the **version**.</span><span class="sxs-lookup"><span data-stu-id="71e87-131">Select **V2** for the **version**.</span></span>
5. <span data-ttu-id="71e87-132">Select the **location** for the data factory.</span><span class="sxs-lookup"><span data-stu-id="71e87-132">Select the **location** for the data factory.</span></span> <span data-ttu-id="71e87-133">Only locations that are supported by Data Factory are shown in the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="71e87-133">Only locations that are supported by Data Factory are shown in the drop-down list.</span></span> <span data-ttu-id="71e87-134">The data stores (Azure Storage, Azure SQL Database, etc.) and computes (HDInsight, etc.) used by data factory can be in other locations.</span><span class="sxs-lookup"><span data-stu-id="71e87-134">The data stores (Azure Storage, Azure SQL Database, etc.) and computes (HDInsight, etc.) used by data factory can be in other locations.</span></span>
6. <span data-ttu-id="71e87-135">Select **Pin to dashboard**.</span><span class="sxs-lookup"><span data-stu-id="71e87-135">Select **Pin to dashboard**.</span></span>     
7. <span data-ttu-id="71e87-136">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="71e87-136">Click **Create**.</span></span>
8. <span data-ttu-id="71e87-137">On the dashboard, you see the following tile with status: **Deploying data factory**.</span><span class="sxs-lookup"><span data-stu-id="71e87-137">On the dashboard, you see the following tile with status: **Deploying data factory**.</span></span> 

    ![deploying data factory tile](media//how-to-invoke-ssis-package-stored-procedure-activity/deploying-data-factory.png)
9. <span data-ttu-id="71e87-139">After the creation is complete, you see the **Data Factory** page as shown in the image.</span><span class="sxs-lookup"><span data-stu-id="71e87-139">After the creation is complete, you see the **Data Factory** page as shown in the image.</span></span>
   
    ![Data factory home page](./media/how-to-invoke-ssis-package-stored-procedure-activity/data-factory-home-page.png)
10. <span data-ttu-id="71e87-141">Click **Author & Monitor** tile to launch the Azure Data Factory user interface (UI) application in a separate tab.</span><span class="sxs-lookup"><span data-stu-id="71e87-141">Click **Author & Monitor** tile to launch the Azure Data Factory user interface (UI) application in a separate tab.</span></span> 

### <a name="create-a-pipeline-with-an-execute-ssis-package-activity"></a><span data-ttu-id="71e87-142">Create a pipeline with an Execute SSIS Package activity</span><span class="sxs-lookup"><span data-stu-id="71e87-142">Create a pipeline with an Execute SSIS Package activity</span></span>
<span data-ttu-id="71e87-143">In this step, you use the Data Factory UI to create a pipeline.</span><span class="sxs-lookup"><span data-stu-id="71e87-143">In this step, you use the Data Factory UI to create a pipeline.</span></span> <span data-ttu-id="71e87-144">You add an Execute SSIS Package activity to the pipeline and configure it to run the SSIS package.</span><span class="sxs-lookup"><span data-stu-id="71e87-144">You add an Execute SSIS Package activity to the pipeline and configure it to run the SSIS package.</span></span> 

1. <span data-ttu-id="71e87-145">In the get started page, click **Create pipeline**:</span><span class="sxs-lookup"><span data-stu-id="71e87-145">In the get started page, click **Create pipeline**:</span></span> 

    ![Get started page](./media/how-to-invoke-ssis-package-stored-procedure-activity/get-started-page.png)
2. <span data-ttu-id="71e87-147">In the **Activities** toolbox, expand **General**, and drag and drop the **Execute SSIS Package** activity to the pipeline designer surface.</span><span class="sxs-lookup"><span data-stu-id="71e87-147">In the **Activities** toolbox, expand **General**, and drag and drop the **Execute SSIS Package** activity to the pipeline designer surface.</span></span> 

   ![Drag the Execute SSIS Package activity to the designer surface](media/how-to-invoke-ssis-package-ssis-activity/ssis-activity-designer.png) 

3. <span data-ttu-id="71e87-149">On the **General** tab of properties for the Execute SSIS Package activity, provide a name and description for the activity.</span><span class="sxs-lookup"><span data-stu-id="71e87-149">On the **General** tab of properties for the Execute SSIS Package activity, provide a name and description for the activity.</span></span> <span data-ttu-id="71e87-150">Set optional timeout and retry values.</span><span class="sxs-lookup"><span data-stu-id="71e87-150">Set optional timeout and retry values.</span></span>

    ![Set properties on the General tab](media/how-to-invoke-ssis-package-ssis-activity/ssis-activity-general.png)

4. <span data-ttu-id="71e87-152">On the **Settings** tab of properties for the Execute SSIS Package activity, select the Azure-SSIS Integration Runtime associated with the `SSISDB` database where the package is deployed.</span><span class="sxs-lookup"><span data-stu-id="71e87-152">On the **Settings** tab of properties for the Execute SSIS Package activity, select the Azure-SSIS Integration Runtime associated with the `SSISDB` database where the package is deployed.</span></span> <span data-ttu-id="71e87-153">Provide the package path in the `SSISDB` database in the format `<folder name>/<project name>/<package name>.dtsx`.</span><span class="sxs-lookup"><span data-stu-id="71e87-153">Provide the package path in the `SSISDB` database in the format `<folder name>/<project name>/<package name>.dtsx`.</span></span> <span data-ttu-id="71e87-154">Optionally specify 32-bit execution and a predefined or custom logging level, and provide an environment path in the format `<folder name>/<environment name>`.</span><span class="sxs-lookup"><span data-stu-id="71e87-154">Optionally specify 32-bit execution and a predefined or custom logging level, and provide an environment path in the format `<folder name>/<environment name>`.</span></span>

    ![Set properties on the Settings tab](media/how-to-invoke-ssis-package-ssis-activity/ssis-activity-settings.png)

5. <span data-ttu-id="71e87-156">To validate the pipeline configuration, click **Validate** on the toolbar.</span><span class="sxs-lookup"><span data-stu-id="71e87-156">To validate the pipeline configuration, click **Validate** on the toolbar.</span></span> <span data-ttu-id="71e87-157">To close the **Pipeline Validation Report**, click **>>**.</span><span class="sxs-lookup"><span data-stu-id="71e87-157">To close the **Pipeline Validation Report**, click **>>**.</span></span>

6. <span data-ttu-id="71e87-158">Publish the pipeline to Data Factory by clicking **Publish All** button.</span><span class="sxs-lookup"><span data-stu-id="71e87-158">Publish the pipeline to Data Factory by clicking **Publish All** button.</span></span> 

### <a name="optionally-parameterize-the-activity"></a><span data-ttu-id="71e87-159">Optionally, parameterize the activity</span><span class="sxs-lookup"><span data-stu-id="71e87-159">Optionally, parameterize the activity</span></span>

<span data-ttu-id="71e87-160">Optionally, assign values, expressions, or functions, which can refer to Data Factory system variables, to your project or package parameters in JSON format by using the **View Source Code** button on the bottom of the Execute SSIS Package activity box, or the **Code** button on the top right-hand corner of the pipeline area.</span><span class="sxs-lookup"><span data-stu-id="71e87-160">Optionally, assign values, expressions, or functions, which can refer to Data Factory system variables, to your project or package parameters in JSON format by using the **View Source Code** button on the bottom of the Execute SSIS Package activity box, or the **Code** button on the top right-hand corner of the pipeline area.</span></span> <span data-ttu-id="71e87-161">For example, you can assign Data Factory pipeline parameters to your SSIS project or package parameters as shown in the following screenshots:</span><span class="sxs-lookup"><span data-stu-id="71e87-161">For example, you can assign Data Factory pipeline parameters to your SSIS project or package parameters as shown in the following screenshots:</span></span>

![Edit JSON script for Execute SSIS Package activity](media/how-to-invoke-ssis-package-ssis-activity/ssis-activity-parameters.png)

![Add parameters to the Execute SSIS Package activity](media/how-to-invoke-ssis-package-ssis-activity/ssis-activity-parameters2.png)

### <a name="run-the-pipeline"></a><span data-ttu-id="71e87-164">Run the pipeline</span><span class="sxs-lookup"><span data-stu-id="71e87-164">Run the pipeline</span></span>
<span data-ttu-id="71e87-165">In this section, you trigger a pipeline run and then monitor it.</span><span class="sxs-lookup"><span data-stu-id="71e87-165">In this section, you trigger a pipeline run and then monitor it.</span></span> 

1. <span data-ttu-id="71e87-166">To trigger a pipeline run, click **Trigger** on the toolbar, and click **Trigger now**.</span><span class="sxs-lookup"><span data-stu-id="71e87-166">To trigger a pipeline run, click **Trigger** on the toolbar, and click **Trigger now**.</span></span> 

    ![Trigger now](./media/how-to-invoke-ssis-package-ssis-activity/ssis-activity-trigger.png)

2. <span data-ttu-id="71e87-168">In the **Pipeline Run** window, select **Finish**.</span><span class="sxs-lookup"><span data-stu-id="71e87-168">In the **Pipeline Run** window, select **Finish**.</span></span> 

### <a name="monitor-the-pipeline"></a><span data-ttu-id="71e87-169">Monitor the pipeline</span><span class="sxs-lookup"><span data-stu-id="71e87-169">Monitor the pipeline</span></span>

1. <span data-ttu-id="71e87-170">Switch to the **Monitor** tab on the left.</span><span class="sxs-lookup"><span data-stu-id="71e87-170">Switch to the **Monitor** tab on the left.</span></span> <span data-ttu-id="71e87-171">You see the pipeline run and its status along with other information (such as Run Start time).</span><span class="sxs-lookup"><span data-stu-id="71e87-171">You see the pipeline run and its status along with other information (such as Run Start time).</span></span> <span data-ttu-id="71e87-172">To refresh the view, click **Refresh**.</span><span class="sxs-lookup"><span data-stu-id="71e87-172">To refresh the view, click **Refresh**.</span></span>

    ![Pipeline runs](./media/how-to-invoke-ssis-package-stored-procedure-activity/pipeline-runs.png)

2. <span data-ttu-id="71e87-174">Click **View Activity Runs** link in the **Actions** column.</span><span class="sxs-lookup"><span data-stu-id="71e87-174">Click **View Activity Runs** link in the **Actions** column.</span></span> <span data-ttu-id="71e87-175">You see only one activity run as the pipeline has only one activity (the Execute SSIS Package activity).</span><span class="sxs-lookup"><span data-stu-id="71e87-175">You see only one activity run as the pipeline has only one activity (the Execute SSIS Package activity).</span></span>

    ![Activity runs](./media/how-to-invoke-ssis-package-ssis-activity/ssis-activity-runs.png)

3. <span data-ttu-id="71e87-177">You can run the following **query** against the SSISDB database in your Azure SQL server to verify that the package executed.</span><span class="sxs-lookup"><span data-stu-id="71e87-177">You can run the following **query** against the SSISDB database in your Azure SQL server to verify that the package executed.</span></span> 

    ```sql
    select * from catalog.executions
    ```

    ![Verify package executions](./media/how-to-invoke-ssis-package-stored-procedure-activity/verify-package-executions.png)

4. <span data-ttu-id="71e87-179">You can also get the SSISDB execution ID from the output of the pipeline activity run, and use the ID to check more comprehensive execution logs and error messages in SSMS.</span><span class="sxs-lookup"><span data-stu-id="71e87-179">You can also get the SSISDB execution ID from the output of the pipeline activity run, and use the ID to check more comprehensive execution logs and error messages in SSMS.</span></span>

    ![Get the execution ID.](media/how-to-invoke-ssis-package-ssis-activity/get-execution-id.png)

### <a name="schedule-the-pipeline-with-a-trigger"></a><span data-ttu-id="71e87-181">Schedule the pipeline with a trigger</span><span class="sxs-lookup"><span data-stu-id="71e87-181">Schedule the pipeline with a trigger</span></span>

<span data-ttu-id="71e87-182">You can also create a scheduled trigger for your pipeline so that the pipeline runs on a schedule (hourly, daily, etc.).</span><span class="sxs-lookup"><span data-stu-id="71e87-182">You can also create a scheduled trigger for your pipeline so that the pipeline runs on a schedule (hourly, daily, etc.).</span></span> <span data-ttu-id="71e87-183">For an example, see [Create a data factory - Data Factory UI](quickstart-create-data-factory-portal.md#trigger-the-pipeline-on-a-schedule).</span><span class="sxs-lookup"><span data-stu-id="71e87-183">For an example, see [Create a data factory - Data Factory UI](quickstart-create-data-factory-portal.md#trigger-the-pipeline-on-a-schedule).</span></span>

## <a name="run-a-package-with-powershell"></a><span data-ttu-id="71e87-184">Run a package with PowerShell</span><span class="sxs-lookup"><span data-stu-id="71e87-184">Run a package with PowerShell</span></span>
<span data-ttu-id="71e87-185">In this section, you use Azure PowerShell to create a Data Factory pipeline with an Execute SSIS Package activity that runs an SSIS package.</span><span class="sxs-lookup"><span data-stu-id="71e87-185">In this section, you use Azure PowerShell to create a Data Factory pipeline with an Execute SSIS Package activity that runs an SSIS package.</span></span> 

<span data-ttu-id="71e87-186">Install the latest Azure PowerShell modules by following instructions in [How to install and configure Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="71e87-186">Install the latest Azure PowerShell modules by following instructions in [How to install and configure Azure PowerShell](/powershell/azure/install-azurerm-ps).</span></span> 

### <a name="create-a-data-factory"></a><span data-ttu-id="71e87-187">Create a data factory</span><span class="sxs-lookup"><span data-stu-id="71e87-187">Create a data factory</span></span>
<span data-ttu-id="71e87-188">You can either use the same data factory that has the Azure-SSIS IR or create a separate data factory.</span><span class="sxs-lookup"><span data-stu-id="71e87-188">You can either use the same data factory that has the Azure-SSIS IR or create a separate data factory.</span></span> <span data-ttu-id="71e87-189">The following procedure provides steps to create a data factory.</span><span class="sxs-lookup"><span data-stu-id="71e87-189">The following procedure provides steps to create a data factory.</span></span> <span data-ttu-id="71e87-190">You create a pipeline with an Execute SSIS Package activity in this data factory.</span><span class="sxs-lookup"><span data-stu-id="71e87-190">You create a pipeline with an Execute SSIS Package activity in this data factory.</span></span> <span data-ttu-id="71e87-191">The Execute SSIS Package activity runs your SSIS package.</span><span class="sxs-lookup"><span data-stu-id="71e87-191">The Execute SSIS Package activity runs your SSIS package.</span></span> 

1. <span data-ttu-id="71e87-192">Define a variable for the resource group name that you use in PowerShell commands later.</span><span class="sxs-lookup"><span data-stu-id="71e87-192">Define a variable for the resource group name that you use in PowerShell commands later.</span></span> <span data-ttu-id="71e87-193">Copy the following command text to PowerShell, specify a name for the [Azure resource group](../azure-resource-manager/resource-group-overview.md) in double quotes, and then run the command.</span><span class="sxs-lookup"><span data-stu-id="71e87-193">Copy the following command text to PowerShell, specify a name for the [Azure resource group](../azure-resource-manager/resource-group-overview.md) in double quotes, and then run the command.</span></span> <span data-ttu-id="71e87-194">For example: `"adfrg"`.</span><span class="sxs-lookup"><span data-stu-id="71e87-194">For example: `"adfrg"`.</span></span> 
   
     ```powershell
    $resourceGroupName = "ADFTutorialResourceGroup";
    ```

    <span data-ttu-id="71e87-195">If the resource group already exists, you may not want to overwrite it.</span><span class="sxs-lookup"><span data-stu-id="71e87-195">If the resource group already exists, you may not want to overwrite it.</span></span> <span data-ttu-id="71e87-196">Assign a different value to the `$ResourceGroupName` variable and run the command again</span><span class="sxs-lookup"><span data-stu-id="71e87-196">Assign a different value to the `$ResourceGroupName` variable and run the command again</span></span>
2. <span data-ttu-id="71e87-197">To create the Azure resource group, run the following command:</span><span class="sxs-lookup"><span data-stu-id="71e87-197">To create the Azure resource group, run the following command:</span></span> 

    ```powershell
    $ResGrp = New-AzureRmResourceGroup $resourceGroupName -location 'eastus'
    ``` 
    <span data-ttu-id="71e87-198">If the resource group already exists, you may not want to overwrite it.</span><span class="sxs-lookup"><span data-stu-id="71e87-198">If the resource group already exists, you may not want to overwrite it.</span></span> <span data-ttu-id="71e87-199">Assign a different value to the `$ResourceGroupName` variable and run the command again.</span><span class="sxs-lookup"><span data-stu-id="71e87-199">Assign a different value to the `$ResourceGroupName` variable and run the command again.</span></span> 
3. <span data-ttu-id="71e87-200">Define a variable for the data factory name.</span><span class="sxs-lookup"><span data-stu-id="71e87-200">Define a variable for the data factory name.</span></span> 

    > [!IMPORTANT]
    >  <span data-ttu-id="71e87-201">Update the data factory name to be globally unique.</span><span class="sxs-lookup"><span data-stu-id="71e87-201">Update the data factory name to be globally unique.</span></span> 

    ```powershell
    $DataFactoryName = "ADFTutorialFactory";
    ```

5. <span data-ttu-id="71e87-202">To create the data factory, run the following **Set-AzureRmDataFactoryV2** cmdlet, using the Location and ResourceGroupName property from the $ResGrp variable:</span><span class="sxs-lookup"><span data-stu-id="71e87-202">To create the data factory, run the following **Set-AzureRmDataFactoryV2** cmdlet, using the Location and ResourceGroupName property from the $ResGrp variable:</span></span> 
    
    ```powershell       
    $DataFactory = Set-AzureRmDataFactoryV2 -ResourceGroupName $ResGrp.ResourceGroupName `
                                            -Location $ResGrp.Location `
                                            -Name $dataFactoryName 
    ```

<span data-ttu-id="71e87-203">Note the following points:</span><span class="sxs-lookup"><span data-stu-id="71e87-203">Note the following points:</span></span>

* <span data-ttu-id="71e87-204">The name of the Azure data factory must be globally unique.</span><span class="sxs-lookup"><span data-stu-id="71e87-204">The name of the Azure data factory must be globally unique.</span></span> <span data-ttu-id="71e87-205">If you receive the following error, change the name and try again.</span><span class="sxs-lookup"><span data-stu-id="71e87-205">If you receive the following error, change the name and try again.</span></span>

    ```
    The specified Data Factory name 'ADFv2QuickStartDataFactory' is already in use. Data Factory names must be globally unique.
    ```
* <span data-ttu-id="71e87-206">To create Data Factory instances, the user account you use to log in to Azure must be a member of **contributor** or **owner** roles, or an **administrator** of the Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="71e87-206">To create Data Factory instances, the user account you use to log in to Azure must be a member of **contributor** or **owner** roles, or an **administrator** of the Azure subscription.</span></span>
* <span data-ttu-id="71e87-207">For a list of Azure regions in which Data Factory is currently available, select the regions that interest you on the following page, and then expand **Analytics** to locate **Data Factory**: [Products available by region](https://azure.microsoft.com/global-infrastructure/services/).</span><span class="sxs-lookup"><span data-stu-id="71e87-207">For a list of Azure regions in which Data Factory is currently available, select the regions that interest you on the following page, and then expand **Analytics** to locate **Data Factory**: [Products available by region](https://azure.microsoft.com/global-infrastructure/services/).</span></span> <span data-ttu-id="71e87-208">The data stores (Azure Storage, Azure SQL Database, etc.) and computes (HDInsight, etc.) used by data factory can be in other regions.</span><span class="sxs-lookup"><span data-stu-id="71e87-208">The data stores (Azure Storage, Azure SQL Database, etc.) and computes (HDInsight, etc.) used by data factory can be in other regions.</span></span>

### <a name="create-a-pipeline-with-an-execute-ssis-package-activity"></a><span data-ttu-id="71e87-209">Create a pipeline with an Execute SSIS Package activity</span><span class="sxs-lookup"><span data-stu-id="71e87-209">Create a pipeline with an Execute SSIS Package activity</span></span> 
<span data-ttu-id="71e87-210">In this step, you create a pipeline with an Execute SSIS Package activity.</span><span class="sxs-lookup"><span data-stu-id="71e87-210">In this step, you create a pipeline with an Execute SSIS Package activity.</span></span> <span data-ttu-id="71e87-211">The activity runs your SSIS package.</span><span class="sxs-lookup"><span data-stu-id="71e87-211">The activity runs your SSIS package.</span></span> 

1. <span data-ttu-id="71e87-212">Create a JSON file named **RunSSISPackagePipeline.json** in the **C:\ADF\RunSSISPackage** folder with content similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="71e87-212">Create a JSON file named **RunSSISPackagePipeline.json** in the **C:\ADF\RunSSISPackage** folder with content similar to the following example:</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="71e87-213">Replace object names, descriptions, and paths, property and parameter values, passwords, and other variable values before saving the file.</span><span class="sxs-lookup"><span data-stu-id="71e87-213">Replace object names, descriptions, and paths, property and parameter values, passwords, and other variable values before saving the file.</span></span> 

    ```json
    {
        "name": "RunSSISPackagePipeline",
        "properties": {
            "activities": [{
                "name": "mySSISActivity",
                "description": "My SSIS package/activity description",
                "type": "ExecuteSSISPackage",
                "typeProperties": {
                    "connectVia": {
                        "referenceName": "myAzureSSISIR",
                        "type": "IntegrationRuntimeReference"
                    },
                    "runtime": "x64",
                    "loggingLevel": "Basic",
                    "packageLocation": {
                        "packagePath": "FolderName/ProjectName/PackageName.dtsx"            
                    },
                    "environmentPath":   "FolderName/EnvironmentName",
                    "projectParameters": {
                        "project_param_1": {
                            "value": "123"
                        }
                    },
                    "packageParameters": {
                        "package_param_1": {
                            "value": "345"
                        }
                    },
                    "projectConnectionManagers": {
                        "MyAdonetCM": {
                            "userName": {
                                "value": "sa"
                            },
                            "passWord": {
                                "value": {
                                    "type": "SecureString",
                                    "value": "abc"
                                }
                            }
                        }
                    },
                    "packageConnectionManagers": {
                        "MyOledbCM": {
                            "userName": {
                                "value": "sa"
                            },
                            "passWord": {
                                "value": {
                                    "type": "SecureString",
                                    "value": "def"
                                }
                            }
                        }
                    },
                    "propertyOverrides": {
                        "\\PackageName.dtsx\\MaxConcurrentExecutables ": {
                            "value": 8,
                            "isSensitive": false
                        }
                    }
                },
                "policy": {
                    "timeout": "0.01:00:00",
                    "retry": 0,
                    "retryIntervalInSeconds": 30
                }
            }]
        }
    }
    ```

2.  <span data-ttu-id="71e87-214">In Azure PowerShell, switch to the `C:\ADF\RunSSISPackage` folder.</span><span class="sxs-lookup"><span data-stu-id="71e87-214">In Azure PowerShell, switch to the `C:\ADF\RunSSISPackage` folder.</span></span>

3. <span data-ttu-id="71e87-215">To create the pipeline **RunSSISPackagePipeline**, run the **Set-AzureRmDataFactoryV2Pipeline** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="71e87-215">To create the pipeline **RunSSISPackagePipeline**, run the **Set-AzureRmDataFactoryV2Pipeline** cmdlet.</span></span>

    ```powershell
    $DFPipeLine = Set-AzureRmDataFactoryV2Pipeline -DataFactoryName $DataFactory.DataFactoryName `
                                                   -ResourceGroupName $ResGrp.ResourceGroupName `
                                                   -Name "RunSSISPackagePipeline"
                                                   -DefinitionFile ".\RunSSISPackagePipeline.json"
    ```

    <span data-ttu-id="71e87-216">Here is the sample output:</span><span class="sxs-lookup"><span data-stu-id="71e87-216">Here is the sample output:</span></span>

    ```
    PipelineName      : Adfv2QuickStartPipeline
    ResourceGroupName : <resourceGroupName>
    DataFactoryName   : <dataFactoryName>
    Activities        : {CopyFromBlobToBlob}
    Parameters        : {[inputPath, Microsoft.Azure.Management.DataFactory.Models.ParameterSpecification], [outputPath, Microsoft.Azure.Management.DataFactory.Models.ParameterSpecification]}
    ```

### <a name="run-the-pipeline"></a><span data-ttu-id="71e87-217">Run the pipeline</span><span class="sxs-lookup"><span data-stu-id="71e87-217">Run the pipeline</span></span>
<span data-ttu-id="71e87-218">Use the **Invoke-AzureRmDataFactoryV2Pipeline** cmdlet to run the pipeline.</span><span class="sxs-lookup"><span data-stu-id="71e87-218">Use the **Invoke-AzureRmDataFactoryV2Pipeline** cmdlet to run the pipeline.</span></span> <span data-ttu-id="71e87-219">The cmdlet returns the pipeline run ID for future monitoring.</span><span class="sxs-lookup"><span data-stu-id="71e87-219">The cmdlet returns the pipeline run ID for future monitoring.</span></span>

```powershell
$RunId = Invoke-AzureRmDataFactoryV2Pipeline -DataFactoryName $DataFactory.DataFactoryName `
                                             -ResourceGroupName $ResGrp.ResourceGroupName `
                                             -PipelineName $DFPipeLine.Name
```

### <a name="monitor-the-pipeline"></a><span data-ttu-id="71e87-220">Monitor the pipeline</span><span class="sxs-lookup"><span data-stu-id="71e87-220">Monitor the pipeline</span></span>

<span data-ttu-id="71e87-221">Run the following PowerShell script to continuously check the pipeline run status until it finishes copying the data.</span><span class="sxs-lookup"><span data-stu-id="71e87-221">Run the following PowerShell script to continuously check the pipeline run status until it finishes copying the data.</span></span> <span data-ttu-id="71e87-222">Copy/paste the following script in the PowerShell window, and press ENTER.</span><span class="sxs-lookup"><span data-stu-id="71e87-222">Copy/paste the following script in the PowerShell window, and press ENTER.</span></span> 

```powershell
while ($True) {
    $Run = Get-AzureRmDataFactoryV2PipelineRun -ResourceGroupName $ResGrp.ResourceGroupName `
                                               -DataFactoryName $DataFactory.DataFactoryName `
                                               -PipelineRunId $RunId

    if ($Run) {
        if ($run.Status -ne 'InProgress') {
            Write-Output ("Pipeline run finished. The status is: " +  $Run.Status)
            $Run
            break
        }
        Write-Output  "Pipeline is running...status: InProgress"
    }

    Start-Sleep -Seconds 10
}   
```

<span data-ttu-id="71e87-223">You can also monitor the pipeline using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="71e87-223">You can also monitor the pipeline using the Azure portal.</span></span> <span data-ttu-id="71e87-224">For step-by-step instructions, see [Monitor the pipeline](quickstart-create-data-factory-resource-manager-template.md#monitor-the-pipeline).</span><span class="sxs-lookup"><span data-stu-id="71e87-224">For step-by-step instructions, see [Monitor the pipeline](quickstart-create-data-factory-resource-manager-template.md#monitor-the-pipeline).</span></span>

### <a name="schedule-the-pipeline-with-a-trigger"></a><span data-ttu-id="71e87-225">Schedule the pipeline with a trigger</span><span class="sxs-lookup"><span data-stu-id="71e87-225">Schedule the pipeline with a trigger</span></span>
<span data-ttu-id="71e87-226">In the previous step, you ran the pipeline on-demand.</span><span class="sxs-lookup"><span data-stu-id="71e87-226">In the previous step, you ran the pipeline on-demand.</span></span> <span data-ttu-id="71e87-227">You can also create a schedule trigger to run the pipeline on a schedule (hourly, daily, etc.).</span><span class="sxs-lookup"><span data-stu-id="71e87-227">You can also create a schedule trigger to run the pipeline on a schedule (hourly, daily, etc.).</span></span>

1. <span data-ttu-id="71e87-228">Create a JSON file named **MyTrigger.json** in **C:\ADF\RunSSISPackage** folder with the following content:</span><span class="sxs-lookup"><span data-stu-id="71e87-228">Create a JSON file named **MyTrigger.json** in **C:\ADF\RunSSISPackage** folder with the following content:</span></span> 

    ```json
    {
        "properties": {
            "name": "MyTrigger",
            "type": "ScheduleTrigger",
            "typeProperties": {
                "recurrence": {
                    "frequency": "Hour",
                    "interval": 1,
                    "startTime": "2017-12-07T00:00:00-08:00",
                    "endTime": "2017-12-08T00:00:00-08:00"
                }
            },
            "pipelines": [{
                    "pipelineReference": {
                        "type": "PipelineReference",
                        "referenceName": "RunSSISPackagePipeline"
                    },
                    "parameters": {}
                }
            ]
        }
    }    
    ```
2. <span data-ttu-id="71e87-229">In **Azure PowerShell**, switch to the **C:\ADF\RunSSISPackage** folder.</span><span class="sxs-lookup"><span data-stu-id="71e87-229">In **Azure PowerShell**, switch to the **C:\ADF\RunSSISPackage** folder.</span></span>
3. <span data-ttu-id="71e87-230">Run the **Set-AzureRmDataFactoryV2Trigger** cmdlet, which creates the trigger.</span><span class="sxs-lookup"><span data-stu-id="71e87-230">Run the **Set-AzureRmDataFactoryV2Trigger** cmdlet, which creates the trigger.</span></span> 

    ```powershell
    Set-AzureRmDataFactoryV2Trigger -ResourceGroupName $ResGrp.ResourceGroupName `
                                    -DataFactoryName $DataFactory.DataFactoryName `
                                    -Name "MyTrigger" -DefinitionFile ".\MyTrigger.json"
    ```
4. <span data-ttu-id="71e87-231">By default, the trigger is in stopped state.</span><span class="sxs-lookup"><span data-stu-id="71e87-231">By default, the trigger is in stopped state.</span></span> <span data-ttu-id="71e87-232">Start the trigger by running the **Start-AzureRmDataFactoryV2Trigger** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="71e87-232">Start the trigger by running the **Start-AzureRmDataFactoryV2Trigger** cmdlet.</span></span> 

    ```powershell
    Start-AzureRmDataFactoryV2Trigger -ResourceGroupName $ResGrp.ResourceGroupName `
                                      -DataFactoryName $DataFactory.DataFactoryName `
                                      -Name "MyTrigger" 
    ```
5. <span data-ttu-id="71e87-233">Confirm that the trigger is started by running the **Get-AzureRmDataFactoryV2Trigger** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="71e87-233">Confirm that the trigger is started by running the **Get-AzureRmDataFactoryV2Trigger** cmdlet.</span></span> 

    ```powershell
    Get-AzureRmDataFactoryV2Trigger -ResourceGroupName $ResourceGroupName `
                                    -DataFactoryName $DataFactoryName `
                                    -Name "MyTrigger"     
    ```    
6. <span data-ttu-id="71e87-234">Run the following command after the next hour.</span><span class="sxs-lookup"><span data-stu-id="71e87-234">Run the following command after the next hour.</span></span> <span data-ttu-id="71e87-235">For example, if the current time is 3:25 PM UTC, run the command at 4 PM UTC.</span><span class="sxs-lookup"><span data-stu-id="71e87-235">For example, if the current time is 3:25 PM UTC, run the command at 4 PM UTC.</span></span> 
    
    ```powershell
    Get-AzureRmDataFactoryV2TriggerRun -ResourceGroupName $ResourceGroupName `
                                       -DataFactoryName $DataFactoryName `
                                       -TriggerName "MyTrigger" `
                                       -TriggerRunStartedAfter "2017-12-06" `
                                       -TriggerRunStartedBefore "2017-12-09"
    ```

    <span data-ttu-id="71e87-236">You can run the following query against the SSISDB database in your Azure SQL server to verify that the package executed.</span><span class="sxs-lookup"><span data-stu-id="71e87-236">You can run the following query against the SSISDB database in your Azure SQL server to verify that the package executed.</span></span> 

    ```sql
    select * from catalog.executions
    ```

## <a name="next-steps"></a><span data-ttu-id="71e87-237">Next steps</span><span class="sxs-lookup"><span data-stu-id="71e87-237">Next steps</span></span>
<span data-ttu-id="71e87-238">See the following blog post:</span><span class="sxs-lookup"><span data-stu-id="71e87-238">See the following blog post:</span></span>
-   [<span data-ttu-id="71e87-239">Modernize and extend your ETL/ELT workflows with SSIS activities in ADF pipelines</span><span class="sxs-lookup"><span data-stu-id="71e87-239">Modernize and extend your ETL/ELT workflows with SSIS activities in ADF pipelines</span></span>](https://blogs.msdn.microsoft.com/ssis/2018/05/23/modernize-and-extend-your-etlelt-workflows-with-ssis-activities-in-adf-pipelines/)
