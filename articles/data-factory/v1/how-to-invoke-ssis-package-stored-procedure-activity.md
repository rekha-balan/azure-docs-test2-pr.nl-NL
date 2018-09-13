---
title: Invoke SSIS package using Azure Data Factory - Stored Procedure Activity | Microsoft Docs
description: This article describes how to invoke a SQL Server Integration Services (SSIS) package from an Azure Data Factory pipeline using the Stored Procedure Activity.
services: data-factory
documentationcenter: ''
author: linda33wj
manager: craigg
ms.reviewer: douglasl
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: ''
ms.devlang: powershell
ms.topic: conceptual
ms.date: 01/19/2018
ms.author: jingwang
ms.openlocfilehash: bf91b1cb1e764c1350cead0c5dfb109b73e9dad3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867749"
---
# <a name="invoke-an-ssis-package-using-stored-procedure-activity-in-azure-data-factory"></a><span data-ttu-id="43b2a-103">Invoke an SSIS package using stored procedure activity in Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="43b2a-103">Invoke an SSIS package using stored procedure activity in Azure Data Factory</span></span>
<span data-ttu-id="43b2a-104">This article describes how to invoke an SSIS package from an Azure Data Factory pipeline by using a stored procedure activity.</span><span class="sxs-lookup"><span data-stu-id="43b2a-104">This article describes how to invoke an SSIS package from an Azure Data Factory pipeline by using a stored procedure activity.</span></span> 

> [!NOTE]
> <span data-ttu-id="43b2a-105">This article applies to version 1 of Data Factory.</span><span class="sxs-lookup"><span data-stu-id="43b2a-105">This article applies to version 1 of Data Factory.</span></span> <span data-ttu-id="43b2a-106">If you are using the current version of the Data Factory service, see [Invoke SSIS packages using stored procedure activity in](../how-to-invoke-ssis-package-stored-procedure-activity.md).</span><span class="sxs-lookup"><span data-stu-id="43b2a-106">If you are using the current version of the Data Factory service, see [Invoke SSIS packages using stored procedure activity in](../how-to-invoke-ssis-package-stored-procedure-activity.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="43b2a-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="43b2a-107">Prerequisites</span></span>

### <a name="azure-sql-database"></a><span data-ttu-id="43b2a-108">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="43b2a-108">Azure SQL Database</span></span> 
<span data-ttu-id="43b2a-109">The walkthrough in this article uses an Azure SQL database that hosts the SSIS catalog.</span><span class="sxs-lookup"><span data-stu-id="43b2a-109">The walkthrough in this article uses an Azure SQL database that hosts the SSIS catalog.</span></span> <span data-ttu-id="43b2a-110">You can also use an Azure SQL Database Managed Instance (Preview).</span><span class="sxs-lookup"><span data-stu-id="43b2a-110">You can also use an Azure SQL Database Managed Instance (Preview).</span></span>

### <a name="create-an-azure-ssis-integration-runtime"></a><span data-ttu-id="43b2a-111">Create an Azure-SSIS integration runtime</span><span class="sxs-lookup"><span data-stu-id="43b2a-111">Create an Azure-SSIS integration runtime</span></span>
<span data-ttu-id="43b2a-112">Create an Azure-SSIS integration runtime if you don't have one by following the step-by-step instruction in the [Tutorial: Deploy SSIS packages](../tutorial-create-azure-ssis-runtime-portal.md).</span><span class="sxs-lookup"><span data-stu-id="43b2a-112">Create an Azure-SSIS integration runtime if you don't have one by following the step-by-step instruction in the [Tutorial: Deploy SSIS packages](../tutorial-create-azure-ssis-runtime-portal.md).</span></span> <span data-ttu-id="43b2a-113">You cannot use Data Factory version 1 to create an Azure-SSIS integration runtime.</span><span class="sxs-lookup"><span data-stu-id="43b2a-113">You cannot use Data Factory version 1 to create an Azure-SSIS integration runtime.</span></span> 

## <a name="azure-portal"></a><span data-ttu-id="43b2a-114">Azure portal</span><span class="sxs-lookup"><span data-stu-id="43b2a-114">Azure portal</span></span>
<span data-ttu-id="43b2a-115">In this section you use the Azure portal to create a Data Factory pipeline with a stored procedure activity that invokes an SSIS package.</span><span class="sxs-lookup"><span data-stu-id="43b2a-115">In this section you use the Azure portal to create a Data Factory pipeline with a stored procedure activity that invokes an SSIS package.</span></span>

### <a name="create-a-data-factory"></a><span data-ttu-id="43b2a-116">Create a data factory</span><span class="sxs-lookup"><span data-stu-id="43b2a-116">Create a data factory</span></span>
<span data-ttu-id="43b2a-117">First step is to create a data factory by using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="43b2a-117">First step is to create a data factory by using the Azure portal.</span></span> 

1. <span data-ttu-id="43b2a-118">Navigate to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="43b2a-118">Navigate to the [Azure portal](https://portal.azure.com).</span></span> 
2. <span data-ttu-id="43b2a-119">Click **New** on the left menu, click **Data + Analytics**, and click **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="43b2a-119">Click **New** on the left menu, click **Data + Analytics**, and click **Data Factory**.</span></span> 
   
   ![New->DataFactory](./media/how-to-invoke-ssis-package-stored-procedure-activity/new-azure-data-factory-menu.png)
2. <span data-ttu-id="43b2a-121">In the **New data factory** page, enter **ADFTutorialDataFactory** for the **name**.</span><span class="sxs-lookup"><span data-stu-id="43b2a-121">In the **New data factory** page, enter **ADFTutorialDataFactory** for the **name**.</span></span> 
      
     ![New data factory page](./media/how-to-invoke-ssis-package-stored-procedure-activity/new-azure-data-factory.png)
 
   <span data-ttu-id="43b2a-123">The name of the Azure data factory must be **globally unique**.</span><span class="sxs-lookup"><span data-stu-id="43b2a-123">The name of the Azure data factory must be **globally unique**.</span></span> <span data-ttu-id="43b2a-124">If you see the following error for the name field, change the name of the data factory (for example, yournameADFTutorialDataFactory).</span><span class="sxs-lookup"><span data-stu-id="43b2a-124">If you see the following error for the name field, change the name of the data factory (for example, yournameADFTutorialDataFactory).</span></span> <span data-ttu-id="43b2a-125">See [Data Factory - Naming Rules](data-factory-naming-rules.md) article for naming rules for Data Factory artifacts.</span><span class="sxs-lookup"><span data-stu-id="43b2a-125">See [Data Factory - Naming Rules](data-factory-naming-rules.md) article for naming rules for Data Factory artifacts.</span></span>

    `Data factory name ADFTutorialDataFactory is not available`
3. <span data-ttu-id="43b2a-126">Select your Azure **subscription** in which you want to create the data factory.</span><span class="sxs-lookup"><span data-stu-id="43b2a-126">Select your Azure **subscription** in which you want to create the data factory.</span></span> 
4. <span data-ttu-id="43b2a-127">For the **Resource Group**, do one of the following steps:</span><span class="sxs-lookup"><span data-stu-id="43b2a-127">For the **Resource Group**, do one of the following steps:</span></span>
     
      - <span data-ttu-id="43b2a-128">Select **Use existing**, and select an existing resource group from the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="43b2a-128">Select **Use existing**, and select an existing resource group from the drop-down list.</span></span> 
      - <span data-ttu-id="43b2a-129">Select **Create new**, and enter the name of a resource group.</span><span class="sxs-lookup"><span data-stu-id="43b2a-129">Select **Create new**, and enter the name of a resource group.</span></span>   
         
    <span data-ttu-id="43b2a-130">To learn about resource groups, see [Using resource groups to manage your Azure resources](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="43b2a-130">To learn about resource groups, see [Using resource groups to manage your Azure resources](../../azure-resource-manager/resource-group-overview.md).</span></span>  
4. <span data-ttu-id="43b2a-131">Select **V1** for the **version**.</span><span class="sxs-lookup"><span data-stu-id="43b2a-131">Select **V1** for the **version**.</span></span>
5. <span data-ttu-id="43b2a-132">Select the **location** for the data factory.</span><span class="sxs-lookup"><span data-stu-id="43b2a-132">Select the **location** for the data factory.</span></span> <span data-ttu-id="43b2a-133">Only locations that are supported by Data Factory are shown in the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="43b2a-133">Only locations that are supported by Data Factory are shown in the drop-down list.</span></span> <span data-ttu-id="43b2a-134">The data stores (Azure Storage, Azure SQL Database, etc.) and computes (HDInsight, etc.) used by data factory can be in other locations.</span><span class="sxs-lookup"><span data-stu-id="43b2a-134">The data stores (Azure Storage, Azure SQL Database, etc.) and computes (HDInsight, etc.) used by data factory can be in other locations.</span></span>
6. <span data-ttu-id="43b2a-135">Select **Pin to dashboard**.</span><span class="sxs-lookup"><span data-stu-id="43b2a-135">Select **Pin to dashboard**.</span></span>     
7. <span data-ttu-id="43b2a-136">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="43b2a-136">Click **Create**.</span></span>
8. <span data-ttu-id="43b2a-137">On the dashboard, you see the following tile with status: **Deploying data factory**.</span><span class="sxs-lookup"><span data-stu-id="43b2a-137">On the dashboard, you see the following tile with status: **Deploying data factory**.</span></span> 

    ![deploying data factory tile](media//how-to-invoke-ssis-package-stored-procedure-activity/deploying-data-factory.png)
9. <span data-ttu-id="43b2a-139">After the creation is complete, you see the **Data Factory** page as shown in the image.</span><span class="sxs-lookup"><span data-stu-id="43b2a-139">After the creation is complete, you see the **Data Factory** page as shown in the image.</span></span>
   
    ![Data factory home page](./media/how-to-invoke-ssis-package-stored-procedure-activity/data-factory-home-page.png)
10. <span data-ttu-id="43b2a-141">Click **Author and deploy** tile to launch the Data Factory Editor.</span><span class="sxs-lookup"><span data-stu-id="43b2a-141">Click **Author and deploy** tile to launch the Data Factory Editor.</span></span>

    ![Data Factory Editor](./media/how-to-invoke-ssis-package-stored-procedure-activity/data-factory-editor.png)

### <a name="create-an-azure-sql-database-linked-service"></a><span data-ttu-id="43b2a-143">Create an Azure SQL Database linked service</span><span class="sxs-lookup"><span data-stu-id="43b2a-143">Create an Azure SQL Database linked service</span></span>
<span data-ttu-id="43b2a-144">Create a linked service to link your Azure SQL database that hosts the SSIS catalog to your data factory.</span><span class="sxs-lookup"><span data-stu-id="43b2a-144">Create a linked service to link your Azure SQL database that hosts the SSIS catalog to your data factory.</span></span> <span data-ttu-id="43b2a-145">Data Factory uses information in this linked service to connect to SSISDB database, and executes a stored procedure to run an SSIS package.</span><span class="sxs-lookup"><span data-stu-id="43b2a-145">Data Factory uses information in this linked service to connect to SSISDB database, and executes a stored procedure to run an SSIS package.</span></span> 

1. <span data-ttu-id="43b2a-146">In the Data Factory Editor, click **New data store** on the menu, and click **Azure SQL Database**.</span><span class="sxs-lookup"><span data-stu-id="43b2a-146">In the Data Factory Editor, click **New data store** on the menu, and click **Azure SQL Database**.</span></span> 

    ![New data store -> Azure SQL Database](./media/how-to-invoke-ssis-package-stored-procedure-activity/new-azure-sql-database-linked-service-menu.png)
2. <span data-ttu-id="43b2a-148">In the right pane, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="43b2a-148">In the right pane, do the following steps:</span></span>

    1. <span data-ttu-id="43b2a-149">Replace `<servername>` with the name of your Azure SQL server.</span><span class="sxs-lookup"><span data-stu-id="43b2a-149">Replace `<servername>` with the name of your Azure SQL server.</span></span> 
    2. <span data-ttu-id="43b2a-150">Replace `<databasename>` with **SSISDB** (name of the SSIS Catalog database).</span><span class="sxs-lookup"><span data-stu-id="43b2a-150">Replace `<databasename>` with **SSISDB** (name of the SSIS Catalog database).</span></span> 
    3. <span data-ttu-id="43b2a-151">Replace `<username@servername>` with the name of the user who has access to the Azure SQL server.</span><span class="sxs-lookup"><span data-stu-id="43b2a-151">Replace `<username@servername>` with the name of the user who has access to the Azure SQL server.</span></span> 
    4. <span data-ttu-id="43b2a-152">Replace `<password>` with the password for the user.</span><span class="sxs-lookup"><span data-stu-id="43b2a-152">Replace `<password>` with the password for the user.</span></span> 
    5. <span data-ttu-id="43b2a-153">Deploy the linked service by clicking the **Deploy** button on the toolbar.</span><span class="sxs-lookup"><span data-stu-id="43b2a-153">Deploy the linked service by clicking the **Deploy** button on the toolbar.</span></span> 

        ![Azure SQL Database linked service](./media/how-to-invoke-ssis-package-stored-procedure-activity/azure-sql-database-linked-service-definition.png)

### <a name="create-a-dummy-dataset-for-output"></a><span data-ttu-id="43b2a-155">Create a dummy dataset for output</span><span class="sxs-lookup"><span data-stu-id="43b2a-155">Create a dummy dataset for output</span></span>
<span data-ttu-id="43b2a-156">This output dataset is a dummy dataset that drives the schedule of the pipeline.</span><span class="sxs-lookup"><span data-stu-id="43b2a-156">This output dataset is a dummy dataset that drives the schedule of the pipeline.</span></span> <span data-ttu-id="43b2a-157">Notice that the frequency is set to Hour and interval is set to 1.</span><span class="sxs-lookup"><span data-stu-id="43b2a-157">Notice that the frequency is set to Hour and interval is set to 1.</span></span> <span data-ttu-id="43b2a-158">Therefore, the pipeline runs once an hour within the pipeline start and end times.</span><span class="sxs-lookup"><span data-stu-id="43b2a-158">Therefore, the pipeline runs once an hour within the pipeline start and end times.</span></span> 

1. <span data-ttu-id="43b2a-159">In the left pane of the Data Factory Editor, click **... More** -> **New dataset** -> **Azure SQL**.</span><span class="sxs-lookup"><span data-stu-id="43b2a-159">In the left pane of the Data Factory Editor, click **... More** -> **New dataset** -> **Azure SQL**.</span></span>

    ![More -> New dataset](./media/how-to-invoke-ssis-package-stored-procedure-activity/new-dataset-menu.png)
2. <span data-ttu-id="43b2a-161">Copy the following JSON snippet into the JSON editor in the right pane.</span><span class="sxs-lookup"><span data-stu-id="43b2a-161">Copy the following JSON snippet into the JSON editor in the right pane.</span></span> 
    
    ```json
    {
        "name": "sprocsampleout",
        "properties": {
            "type": "AzureSqlTable",
            "linkedServiceName": "AzureSqlLinkedService",
            "typeProperties": { },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            }
        }
    }
    ```
3. <span data-ttu-id="43b2a-162">Click **Deploy** on the toolbar.</span><span class="sxs-lookup"><span data-stu-id="43b2a-162">Click **Deploy** on the toolbar.</span></span> <span data-ttu-id="43b2a-163">This action deploys the dataset to the Azure Data Factory service.</span><span class="sxs-lookup"><span data-stu-id="43b2a-163">This action deploys the dataset to the Azure Data Factory service.</span></span> 

### <a name="create-a-pipeline-with-stored-procedure-activity"></a><span data-ttu-id="43b2a-164">Create a pipeline with stored procedure activity</span><span class="sxs-lookup"><span data-stu-id="43b2a-164">Create a pipeline with stored procedure activity</span></span> 
<span data-ttu-id="43b2a-165">In this step, you create a pipeline with a stored procedure activity.</span><span class="sxs-lookup"><span data-stu-id="43b2a-165">In this step, you create a pipeline with a stored procedure activity.</span></span> <span data-ttu-id="43b2a-166">The activity invokes the sp_executesql stored procedure to run your SSIS package.</span><span class="sxs-lookup"><span data-stu-id="43b2a-166">The activity invokes the sp_executesql stored procedure to run your SSIS package.</span></span> 

1. <span data-ttu-id="43b2a-167">In the left pane, click **... More**, and click **New pipeline**.</span><span class="sxs-lookup"><span data-stu-id="43b2a-167">In the left pane, click **... More**, and click **New pipeline**.</span></span>
2. <span data-ttu-id="43b2a-168">Copy the following JSON snippet into the JSON editor:</span><span class="sxs-lookup"><span data-stu-id="43b2a-168">Copy the following JSON snippet into the JSON editor:</span></span> 

    > [!IMPORTANT]
    > <span data-ttu-id="43b2a-169">Replace &lt;folder name&gt;, &lt;project name&gt;, &lt;package name&gt; with names of folder, project, and package in the SSIS catalog before saving the file.</span><span class="sxs-lookup"><span data-stu-id="43b2a-169">Replace &lt;folder name&gt;, &lt;project name&gt;, &lt;package name&gt; with names of folder, project, and package in the SSIS catalog before saving the file.</span></span>

    ```json
    {
        "name": "MyPipeline",
        "properties": {
            "activities": [{
                "name": "SprocActivitySample",
                "type": "SqlServerStoredProcedure",
                "typeProperties": {
                    "storedProcedureName": "sp_executesql",
                    "storedProcedureParameters": {
                        "stmt": "DECLARE @return_value INT, @exe_id BIGINT, @err_msg NVARCHAR(150)    EXEC @return_value=[SSISDB].[catalog].[create_execution] @folder_name=N'<folder name>', @project_name=N'<project name>', @package_name=N'<package name>', @use32bitruntime=0, @runinscaleout=1, @useanyworker=1, @execution_id=@exe_id OUTPUT    EXEC [SSISDB].[catalog].[set_execution_parameter_value] @exe_id, @object_type=50, @parameter_name=N'SYNCHRONIZED', @parameter_value=1    EXEC [SSISDB].[catalog].[start_execution] @execution_id=@exe_id, @retry_count=0    IF(SELECT [status] FROM [SSISDB].[catalog].[executions] WHERE execution_id=@exe_id)<>7 BEGIN SET @err_msg=N'Your package execution did not succeed for execution ID: ' + CAST(@exe_id AS NVARCHAR(20)) RAISERROR(@err_msg,15,1) END"
                    }
                },
                "outputs": [{
                    "name": "sprocsampleout"
                }],
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                }
            }],
            "start": "2018-01-19T00:00:00Z",
            "end": "2018-01-19T05:00:00Z",
            "isPaused": false
        }
    }    
    ```
3. <span data-ttu-id="43b2a-170">Click **Deploy** on the toolbar.</span><span class="sxs-lookup"><span data-stu-id="43b2a-170">Click **Deploy** on the toolbar.</span></span> <span data-ttu-id="43b2a-171">This action deploys the pipeline to the Azure Data Factory service.</span><span class="sxs-lookup"><span data-stu-id="43b2a-171">This action deploys the pipeline to the Azure Data Factory service.</span></span> 

### <a name="monitor-the-pipeline-run"></a><span data-ttu-id="43b2a-172">Monitor the pipeline run</span><span class="sxs-lookup"><span data-stu-id="43b2a-172">Monitor the pipeline run</span></span>
<span data-ttu-id="43b2a-173">The schedule on the output dataset is defined as hourly.</span><span class="sxs-lookup"><span data-stu-id="43b2a-173">The schedule on the output dataset is defined as hourly.</span></span> <span data-ttu-id="43b2a-174">The pipeline end time is five hours from the start time.</span><span class="sxs-lookup"><span data-stu-id="43b2a-174">The pipeline end time is five hours from the start time.</span></span> <span data-ttu-id="43b2a-175">Therefore, you see five pipeline runs.</span><span class="sxs-lookup"><span data-stu-id="43b2a-175">Therefore, you see five pipeline runs.</span></span> 

1. <span data-ttu-id="43b2a-176">Close the editor windows so that you see the home page for the data factory.</span><span class="sxs-lookup"><span data-stu-id="43b2a-176">Close the editor windows so that you see the home page for the data factory.</span></span> <span data-ttu-id="43b2a-177">Click **Monitor & Manage** tile.</span><span class="sxs-lookup"><span data-stu-id="43b2a-177">Click **Monitor & Manage** tile.</span></span> 

    ![Diagram tile](./media/how-to-invoke-ssis-package-stored-procedure-activity/monitor-manage-tile.png)
2. <span data-ttu-id="43b2a-179">Update the **Start time** and **End time** to **01/18/2018 08:30 AM** and **01/20/2018 08:30 AM**, and click **Apply**.</span><span class="sxs-lookup"><span data-stu-id="43b2a-179">Update the **Start time** and **End time** to **01/18/2018 08:30 AM** and **01/20/2018 08:30 AM**, and click **Apply**.</span></span> <span data-ttu-id="43b2a-180">You should see the **activity windows** associated with the pipeline run.</span><span class="sxs-lookup"><span data-stu-id="43b2a-180">You should see the **activity windows** associated with the pipeline run.</span></span> 

    ![Activity windows](./media/how-to-invoke-ssis-package-stored-procedure-activity/activity-windows.png)

<span data-ttu-id="43b2a-182">For more information about monitoring pipelines, see [Monitor and manage Azure Data Factory pipelines by using the Monitoring and Management App](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="43b2a-182">For more information about monitoring pipelines, see [Monitor and manage Azure Data Factory pipelines by using the Monitoring and Management App](data-factory-monitor-manage-app.md).</span></span>

## <a name="azure-powershell"></a><span data-ttu-id="43b2a-183">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="43b2a-183">Azure PowerShell</span></span>
<span data-ttu-id="43b2a-184">In this section you use Azure PowerShell to create a Data Factory pipeline with a stored procedure activity that invokes an SSIS package.</span><span class="sxs-lookup"><span data-stu-id="43b2a-184">In this section you use Azure PowerShell to create a Data Factory pipeline with a stored procedure activity that invokes an SSIS package.</span></span>

<span data-ttu-id="43b2a-185">Install the latest Azure PowerShell modules by following instructions in [How to install and configure Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="43b2a-185">Install the latest Azure PowerShell modules by following instructions in [How to install and configure Azure PowerShell](/powershell/azure/install-azurerm-ps).</span></span>

### <a name="create-a-data-factory"></a><span data-ttu-id="43b2a-186">Create a data factory</span><span class="sxs-lookup"><span data-stu-id="43b2a-186">Create a data factory</span></span>
<span data-ttu-id="43b2a-187">The following procedure provides steps to create a data factory.</span><span class="sxs-lookup"><span data-stu-id="43b2a-187">The following procedure provides steps to create a data factory.</span></span> <span data-ttu-id="43b2a-188">You create a pipeline with a stored procedure activity in this data factory.</span><span class="sxs-lookup"><span data-stu-id="43b2a-188">You create a pipeline with a stored procedure activity in this data factory.</span></span> <span data-ttu-id="43b2a-189">The stored procedure activity executes a stored procedure in the SSISDB database to run your SSIS package.</span><span class="sxs-lookup"><span data-stu-id="43b2a-189">The stored procedure activity executes a stored procedure in the SSISDB database to run your SSIS package.</span></span>

1. <span data-ttu-id="43b2a-190">Define a variable for the resource group name that you use in PowerShell commands later.</span><span class="sxs-lookup"><span data-stu-id="43b2a-190">Define a variable for the resource group name that you use in PowerShell commands later.</span></span> <span data-ttu-id="43b2a-191">Copy the following command text to PowerShell, specify a name for the [Azure resource group](../../azure-resource-manager/resource-group-overview.md) in double quotes, and then run the command.</span><span class="sxs-lookup"><span data-stu-id="43b2a-191">Copy the following command text to PowerShell, specify a name for the [Azure resource group](../../azure-resource-manager/resource-group-overview.md) in double quotes, and then run the command.</span></span> <span data-ttu-id="43b2a-192">For example: `"adfrg"`.</span><span class="sxs-lookup"><span data-stu-id="43b2a-192">For example: `"adfrg"`.</span></span> 
   
     ```powershell
    $resourceGroupName = "ADFTutorialResourceGroup";
    ```

    <span data-ttu-id="43b2a-193">If the resource group already exists, you may not want to overwrite it.</span><span class="sxs-lookup"><span data-stu-id="43b2a-193">If the resource group already exists, you may not want to overwrite it.</span></span> <span data-ttu-id="43b2a-194">Assign a different value to the `$ResourceGroupName` variable and run the command again</span><span class="sxs-lookup"><span data-stu-id="43b2a-194">Assign a different value to the `$ResourceGroupName` variable and run the command again</span></span>
2. <span data-ttu-id="43b2a-195">To create the Azure resource group, run the following command:</span><span class="sxs-lookup"><span data-stu-id="43b2a-195">To create the Azure resource group, run the following command:</span></span> 

    ```powershell
    $ResGrp = New-AzureRmResourceGroup $resourceGroupName -location 'eastus'
    ``` 
    <span data-ttu-id="43b2a-196">If the resource group already exists, you may not want to overwrite it.</span><span class="sxs-lookup"><span data-stu-id="43b2a-196">If the resource group already exists, you may not want to overwrite it.</span></span> <span data-ttu-id="43b2a-197">Assign a different value to the `$ResourceGroupName` variable and run the command again.</span><span class="sxs-lookup"><span data-stu-id="43b2a-197">Assign a different value to the `$ResourceGroupName` variable and run the command again.</span></span> 
3. <span data-ttu-id="43b2a-198">Define a variable for the data factory name.</span><span class="sxs-lookup"><span data-stu-id="43b2a-198">Define a variable for the data factory name.</span></span> 

    > [!IMPORTANT]
    >  <span data-ttu-id="43b2a-199">Update the data factory name to be globally unique.</span><span class="sxs-lookup"><span data-stu-id="43b2a-199">Update the data factory name to be globally unique.</span></span> 

    ```powershell
    $DataFactoryName = "ADFTutorialFactory";
    ```

5. <span data-ttu-id="43b2a-200">To create the data factory, run the following **New-AzureRmDataFactory** cmdlet, using the Location and ResourceGroupName property from the $ResGrp variable:</span><span class="sxs-lookup"><span data-stu-id="43b2a-200">To create the data factory, run the following **New-AzureRmDataFactory** cmdlet, using the Location and ResourceGroupName property from the $ResGrp variable:</span></span> 
    
    ```powershell       
    $df = New-AzureRmDataFactory -ResourceGroupName $ResourceGroupName -Name $dataFactoryName -Location "East US"
    ```

<span data-ttu-id="43b2a-201">Note the following points:</span><span class="sxs-lookup"><span data-stu-id="43b2a-201">Note the following points:</span></span>

* <span data-ttu-id="43b2a-202">The name of the Azure data factory must be globally unique.</span><span class="sxs-lookup"><span data-stu-id="43b2a-202">The name of the Azure data factory must be globally unique.</span></span> <span data-ttu-id="43b2a-203">If you receive the following error, change the name and try again.</span><span class="sxs-lookup"><span data-stu-id="43b2a-203">If you receive the following error, change the name and try again.</span></span>

    ```
    The specified Data Factory name 'ADFTutorialFactory' is already in use. Data Factory names must be globally unique.
    ```
* <span data-ttu-id="43b2a-204">To create Data Factory instances, the user account you use to log in to Azure must be a member of **contributor** or **owner** roles, or an **administrator** of the Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="43b2a-204">To create Data Factory instances, the user account you use to log in to Azure must be a member of **contributor** or **owner** roles, or an **administrator** of the Azure subscription.</span></span>

### <a name="create-an-azure-sql-database-linked-service"></a><span data-ttu-id="43b2a-205">Create an Azure SQL Database linked service</span><span class="sxs-lookup"><span data-stu-id="43b2a-205">Create an Azure SQL Database linked service</span></span>
<span data-ttu-id="43b2a-206">Create a linked service to link your Azure SQL database that hosts the SSIS catalog to your data factory.</span><span class="sxs-lookup"><span data-stu-id="43b2a-206">Create a linked service to link your Azure SQL database that hosts the SSIS catalog to your data factory.</span></span> <span data-ttu-id="43b2a-207">Data Factory uses information in this linked service to connect to SSISDB database, and executes a stored procedure to run an SSIS package.</span><span class="sxs-lookup"><span data-stu-id="43b2a-207">Data Factory uses information in this linked service to connect to SSISDB database, and executes a stored procedure to run an SSIS package.</span></span> 

1. <span data-ttu-id="43b2a-208">Create a JSON file named **AzureSqlDatabaseLinkedService.json** in **C:\ADF\RunSSISPackage** folder with the following content:</span><span class="sxs-lookup"><span data-stu-id="43b2a-208">Create a JSON file named **AzureSqlDatabaseLinkedService.json** in **C:\ADF\RunSSISPackage** folder with the following content:</span></span> 

    > [!IMPORTANT]
    > <span data-ttu-id="43b2a-209">Replace &lt;servername&gt;, &lt;username&gt;@&lt;servername&gt; and &lt;password&gt; with values of your Azure SQL Database before saving the file.</span><span class="sxs-lookup"><span data-stu-id="43b2a-209">Replace &lt;servername&gt;, &lt;username&gt;@&lt;servername&gt; and &lt;password&gt; with values of your Azure SQL Database before saving the file.</span></span>

    ```json
    {
        "name": "AzureSqlDatabaseLinkedService",
        "properties": {
            "type": "AzureSqlDatabase",
            "typeProperties": {
                "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=SSISDB;User ID=<username>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
            }
        }
        }
    ```
2. <span data-ttu-id="43b2a-210">In **Azure PowerShell**, switch to the **C:\ADF\RunSSISPackage** folder.</span><span class="sxs-lookup"><span data-stu-id="43b2a-210">In **Azure PowerShell**, switch to the **C:\ADF\RunSSISPackage** folder.</span></span>
3. <span data-ttu-id="43b2a-211">Run the **New-AzureRmDataFactoryLinkedService** cmdlet to create the linked service: **AzureSqlDatabaseLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="43b2a-211">Run the **New-AzureRmDataFactoryLinkedService** cmdlet to create the linked service: **AzureSqlDatabaseLinkedService**.</span></span> 

    ```powershell
    New-AzureRmDataFactoryLinkedService $df -File ".\AzureSqlDatabaseLinkedService.json"
    ```

### <a name="create-an-output-dataset"></a><span data-ttu-id="43b2a-212">Create an output dataset</span><span class="sxs-lookup"><span data-stu-id="43b2a-212">Create an output dataset</span></span>
<span data-ttu-id="43b2a-213">This output dataset is a dummy dataset that drives the schedule of the pipeline.</span><span class="sxs-lookup"><span data-stu-id="43b2a-213">This output dataset is a dummy dataset that drives the schedule of the pipeline.</span></span> <span data-ttu-id="43b2a-214">Notice that the frequency is set to Hour and interval is set to 1.</span><span class="sxs-lookup"><span data-stu-id="43b2a-214">Notice that the frequency is set to Hour and interval is set to 1.</span></span> <span data-ttu-id="43b2a-215">Therefore, the pipeline runs once an hour within the pipeline start and end times.</span><span class="sxs-lookup"><span data-stu-id="43b2a-215">Therefore, the pipeline runs once an hour within the pipeline start and end times.</span></span> 

1. <span data-ttu-id="43b2a-216">Create an OuputDataset.json file with the following content:</span><span class="sxs-lookup"><span data-stu-id="43b2a-216">Create an OuputDataset.json file with the following content:</span></span> 
    
    ```json
    {
        "name": "sprocsampleout",
        "properties": {
            "type": "AzureSqlTable",
            "linkedServiceName": "AzureSqlLinkedService",
            "typeProperties": { },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            }
        }
    }
    ```
2. <span data-ttu-id="43b2a-217">Run the **New-AzureRmDataFactoryDataset** cmdlet to create a dataset.</span><span class="sxs-lookup"><span data-stu-id="43b2a-217">Run the **New-AzureRmDataFactoryDataset** cmdlet to create a dataset.</span></span> 

    ```powershell
    New-AzureRmDataFactoryDataset $df -File ".\OutputDataset.json"
    ```

### <a name="create-a-pipeline-with-stored-procedure-activity"></a><span data-ttu-id="43b2a-218">Create a pipeline with stored procedure activity</span><span class="sxs-lookup"><span data-stu-id="43b2a-218">Create a pipeline with stored procedure activity</span></span> 
<span data-ttu-id="43b2a-219">In this step, you create a pipeline with a stored procedure activity.</span><span class="sxs-lookup"><span data-stu-id="43b2a-219">In this step, you create a pipeline with a stored procedure activity.</span></span> <span data-ttu-id="43b2a-220">The activity invokes the sp_executesql stored procedure to run your SSIS package.</span><span class="sxs-lookup"><span data-stu-id="43b2a-220">The activity invokes the sp_executesql stored procedure to run your SSIS package.</span></span> 

1. <span data-ttu-id="43b2a-221">Create a JSON file named **MyPipeline.json** in the **C:\ADF\RunSSISPackage** folder with the following content:</span><span class="sxs-lookup"><span data-stu-id="43b2a-221">Create a JSON file named **MyPipeline.json** in the **C:\ADF\RunSSISPackage** folder with the following content:</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="43b2a-222">Replace &lt;folder name&gt;, &lt;project name&gt;, &lt;package name&gt; with names of folder, project, and package in the SSIS catalog before saving the file.</span><span class="sxs-lookup"><span data-stu-id="43b2a-222">Replace &lt;folder name&gt;, &lt;project name&gt;, &lt;package name&gt; with names of folder, project, and package in the SSIS catalog before saving the file.</span></span>

    ```json
    {
        "name": "MyPipeline",
        "properties": {
            "activities": [{
                "name": "SprocActivitySample",
                "type": "SqlServerStoredProcedure",
                "typeProperties": {
                    "storedProcedureName": "sp_executesql",
                    "storedProcedureParameters": {
                        "stmt": "DECLARE @return_value INT, @exe_id BIGINT, @err_msg NVARCHAR(150)    EXEC @return_value=[SSISDB].[catalog].[create_execution] @folder_name=N'<folder name>', @project_name=N'<project name>', @package_name=N'<package name>', @use32bitruntime=0, @runinscaleout=1, @useanyworker=1, @execution_id=@exe_id OUTPUT    EXEC [SSISDB].[catalog].[set_execution_parameter_value] @exe_id, @object_type=50, @parameter_name=N'SYNCHRONIZED', @parameter_value=1    EXEC [SSISDB].[catalog].[start_execution] @execution_id=@exe_id, @retry_count=0    IF(SELECT [status] FROM [SSISDB].[catalog].[executions] WHERE execution_id=@exe_id)<>7 BEGIN SET @err_msg=N'Your package execution did not succeed for execution ID: ' + CAST(@exe_id AS NVARCHAR(20)) RAISERROR(@err_msg,15,1) END"
                    }
                },
                "outputs": [{
                    "name": "sprocsampleout"
                }],
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                }
            }],
            "start": "2017-10-01T00:00:00Z",
            "end": "2017-10-01T05:00:00Z",
            "isPaused": false
        }
    }    
    ```

2. <span data-ttu-id="43b2a-223">To create the pipeline: **RunSSISPackagePipeline**, run the **New-AzureRmDataFactoryPipeline** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="43b2a-223">To create the pipeline: **RunSSISPackagePipeline**, run the **New-AzureRmDataFactoryPipeline** cmdlet.</span></span>

    ```powershell
    $DFPipeLine = New-AzureRmDataFactoryPipeline -DataFactoryName $DataFactory.DataFactoryName -ResourceGroupName $ResGrp.ResourceGroupName -Name "RunSSISPackagePipeline" -DefinitionFile ".\RunSSISPackagePipeline.json"
    ```

### <a name="monitor-the-pipeline-run"></a><span data-ttu-id="43b2a-224">Monitor the pipeline run</span><span class="sxs-lookup"><span data-stu-id="43b2a-224">Monitor the pipeline run</span></span>

2. <span data-ttu-id="43b2a-225">Run **Get-AzureRmDataFactorySlice** to get details about all slices of the output dataset\*\*, which is the output table of the pipeline.</span><span class="sxs-lookup"><span data-stu-id="43b2a-225">Run **Get-AzureRmDataFactorySlice** to get details about all slices of the output dataset\*\*, which is the output table of the pipeline.</span></span>

    ```PowerShell
    Get-AzureRmDataFactorySlice $df -DatasetName sprocsampleout -StartDateTime 2017-10-01T00:00:00Z
    ```
    <span data-ttu-id="43b2a-226">Notice that the StartDateTime you specify here is the same start time specified in the pipeline JSON.</span><span class="sxs-lookup"><span data-stu-id="43b2a-226">Notice that the StartDateTime you specify here is the same start time specified in the pipeline JSON.</span></span> 
3. <span data-ttu-id="43b2a-227">Run **Get-AzureRmDataFactoryRun** to get the details of activity runs for a specific slice.</span><span class="sxs-lookup"><span data-stu-id="43b2a-227">Run **Get-AzureRmDataFactoryRun** to get the details of activity runs for a specific slice.</span></span>

    ```PowerShell
    Get-AzureRmDataFactoryRun $df -DatasetName sprocsampleout -StartDateTime 2017-10-01T00:00:00Z
    ```

    <span data-ttu-id="43b2a-228">You can keep running this cmdlet until you see the slice in **Ready** state or **Failed** state.</span><span class="sxs-lookup"><span data-stu-id="43b2a-228">You can keep running this cmdlet until you see the slice in **Ready** state or **Failed** state.</span></span> 

    <span data-ttu-id="43b2a-229">You can run the following query against the SSISDB database in your Azure SQL server to verify that the package executed.</span><span class="sxs-lookup"><span data-stu-id="43b2a-229">You can run the following query against the SSISDB database in your Azure SQL server to verify that the package executed.</span></span> 

    ```sql
    select * from catalog.executions
    ```

## <a name="next-steps"></a><span data-ttu-id="43b2a-230">Next steps</span><span class="sxs-lookup"><span data-stu-id="43b2a-230">Next steps</span></span>
<span data-ttu-id="43b2a-231">For details about the stored procedure activity, see the [Stored Procedure activity](data-factory-stored-proc-activity.md) article.</span><span class="sxs-lookup"><span data-stu-id="43b2a-231">For details about the stored procedure activity, see the [Stored Procedure activity](data-factory-stored-proc-activity.md) article.</span></span>

