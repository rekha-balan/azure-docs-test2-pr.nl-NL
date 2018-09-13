---
title: Reconfigure the Azure-SSIS integration runtime | Microsoft Docs
description: Learn how to reconfigure an Azure-SSIS integration runtime in Azure Data Factory after you have already provisioned it.
services: data-factory
documentationcenter: ''
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 01/22/2018
author: swinarko
ms.author: sawinark
ms.reviewer: douglasl
manager: craigg
ms.openlocfilehash: 248967f736fcd10cf398917d3cd1e2760537df7c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857794"
---
# <a name="reconfigure-the-azure-ssis-integration-runtime"></a><span data-ttu-id="9464c-103">Reconfigure the Azure-SSIS integration runtime</span><span class="sxs-lookup"><span data-stu-id="9464c-103">Reconfigure the Azure-SSIS integration runtime</span></span>
<span data-ttu-id="9464c-104">This article describes how to reconfigure an existing Azure-SSIS integration runtime.</span><span class="sxs-lookup"><span data-stu-id="9464c-104">This article describes how to reconfigure an existing Azure-SSIS integration runtime.</span></span> <span data-ttu-id="9464c-105">To create an Azure-SSIS integration runtime (IR) in Azure Data Factory, see [Create an Azure-SSIS integration runtime](create-azure-ssis-integration-runtime.md).</span><span class="sxs-lookup"><span data-stu-id="9464c-105">To create an Azure-SSIS integration runtime (IR) in Azure Data Factory, see [Create an Azure-SSIS integration runtime](create-azure-ssis-integration-runtime.md).</span></span>  

## <a name="data-factory-ui"></a><span data-ttu-id="9464c-106">Data Factory UI</span><span class="sxs-lookup"><span data-stu-id="9464c-106">Data Factory UI</span></span> 
<span data-ttu-id="9464c-107">You can use Data Factory UI to stop, edit/reconfigure, or delete an Azure-SSIS IR.</span><span class="sxs-lookup"><span data-stu-id="9464c-107">You can use Data Factory UI to stop, edit/reconfigure, or delete an Azure-SSIS IR.</span></span> 

1. <span data-ttu-id="9464c-108">In the **Data Factory UI**, switch to the **Edit** tab. To launch Data Factory UI, click **Author & Monitor** on the home page of your data factory.</span><span class="sxs-lookup"><span data-stu-id="9464c-108">In the **Data Factory UI**, switch to the **Edit** tab. To launch Data Factory UI, click **Author & Monitor** on the home page of your data factory.</span></span>
2. <span data-ttu-id="9464c-109">In the left pane, click **Connections**.</span><span class="sxs-lookup"><span data-stu-id="9464c-109">In the left pane, click **Connections**.</span></span>
3. <span data-ttu-id="9464c-110">In the right pane, switch to the **Integration Runtimes**.</span><span class="sxs-lookup"><span data-stu-id="9464c-110">In the right pane, switch to the **Integration Runtimes**.</span></span> 
4. <span data-ttu-id="9464c-111">You can use buttons in the Actions column to **stop**, **edit**, or **delete** the integration runtime.</span><span class="sxs-lookup"><span data-stu-id="9464c-111">You can use buttons in the Actions column to **stop**, **edit**, or **delete** the integration runtime.</span></span> <span data-ttu-id="9464c-112">The **Code** button in the **Actions** column lets you view the JSON definition associated with the integration runtime.</span><span class="sxs-lookup"><span data-stu-id="9464c-112">The **Code** button in the **Actions** column lets you view the JSON definition associated with the integration runtime.</span></span>  
    
    ![Actions for Azure SSIS IR](./media/manage-azure-ssis-integration-runtime/actions-for-azure-ssis-ir.png)

### <a name="to-reconfigure-an-azure-ssis-ir"></a><span data-ttu-id="9464c-114">To reconfigure an Azure-SSIS IR</span><span class="sxs-lookup"><span data-stu-id="9464c-114">To reconfigure an Azure-SSIS IR</span></span>
1. <span data-ttu-id="9464c-115">Stop the integration runtime by clicking **Stop** in the **Actions** column.</span><span class="sxs-lookup"><span data-stu-id="9464c-115">Stop the integration runtime by clicking **Stop** in the **Actions** column.</span></span> <span data-ttu-id="9464c-116">To refresh the list view, click **Refresh** on the toolbar.</span><span class="sxs-lookup"><span data-stu-id="9464c-116">To refresh the list view, click **Refresh** on the toolbar.</span></span> <span data-ttu-id="9464c-117">After the IR is stopped, you see that the first action lets you start the IR.</span><span class="sxs-lookup"><span data-stu-id="9464c-117">After the IR is stopped, you see that the first action lets you start the IR.</span></span> 

    ![Actions for Azure SSIS IR - after stopped](./media/manage-azure-ssis-integration-runtime/actions-after-ssis-ir-stopped.png)
2. <span data-ttu-id="9464c-119">Edit/reconfigure IR by clicking **Edit** button in the **Actions** column.</span><span class="sxs-lookup"><span data-stu-id="9464c-119">Edit/reconfigure IR by clicking **Edit** button in the **Actions** column.</span></span> <span data-ttu-id="9464c-120">In the **Integration Runtime Setup** window, change settings (for example, size of the node, number of nodes, or maximum parallel executions per node).</span><span class="sxs-lookup"><span data-stu-id="9464c-120">In the **Integration Runtime Setup** window, change settings (for example, size of the node, number of nodes, or maximum parallel executions per node).</span></span> 
3. <span data-ttu-id="9464c-121">To restart the IR, click **Start** button in the **Actions** column.</span><span class="sxs-lookup"><span data-stu-id="9464c-121">To restart the IR, click **Start** button in the **Actions** column.</span></span>     

## <a name="azure-powershell"></a><span data-ttu-id="9464c-122">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="9464c-122">Azure PowerShell</span></span>
<span data-ttu-id="9464c-123">After you provision and start an instance of Azure-SSIS integration runtime, you can reconfigure it by running a sequence of `Stop` - `Set` - `Start` PowerShell cmdlets consecutively.</span><span class="sxs-lookup"><span data-stu-id="9464c-123">After you provision and start an instance of Azure-SSIS integration runtime, you can reconfigure it by running a sequence of `Stop` - `Set` - `Start` PowerShell cmdlets consecutively.</span></span> <span data-ttu-id="9464c-124">For example, the following PowerShell script changes the number of nodes allocated for the Azure-SSIS integration runtime instance to five.</span><span class="sxs-lookup"><span data-stu-id="9464c-124">For example, the following PowerShell script changes the number of nodes allocated for the Azure-SSIS integration runtime instance to five.</span></span>

### <a name="reconfigure-an-azure-ssis-ir"></a><span data-ttu-id="9464c-125">Reconfigure an Azure-SSIS IR</span><span class="sxs-lookup"><span data-stu-id="9464c-125">Reconfigure an Azure-SSIS IR</span></span>

1. <span data-ttu-id="9464c-126">First, stop the Azure-SSIS integration runtime by using the [Stop-AzureRmDataFactoryV2IntegrationRuntime](/powershell/module/azurerm.datafactoryv2/stop-azurermdatafactoryv2integrationruntime?view=azurermps-4.4.1) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9464c-126">First, stop the Azure-SSIS integration runtime by using the [Stop-AzureRmDataFactoryV2IntegrationRuntime](/powershell/module/azurerm.datafactoryv2/stop-azurermdatafactoryv2integrationruntime?view=azurermps-4.4.1) cmdlet.</span></span> <span data-ttu-id="9464c-127">This command releases all of its nodes and stops billing.</span><span class="sxs-lookup"><span data-stu-id="9464c-127">This command releases all of its nodes and stops billing.</span></span>

    ```powershell
    Stop-AzureRmDataFactoryV2IntegrationRuntime -DataFactoryName $DataFactoryName -Name $AzureSSISName -ResourceGroupName $ResourceGroupName 
    ```
2. <span data-ttu-id="9464c-128">Next, reconfigure the Azure-SSIS IR by using the [Set-AzureRmDataFactoryV2IntegrationRuntime](/powershell/module/azurerm.datafactoryv2/set-azurermdatafactoryv2integrationruntime?view=azurermps-4.4.1) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9464c-128">Next, reconfigure the Azure-SSIS IR by using the [Set-AzureRmDataFactoryV2IntegrationRuntime](/powershell/module/azurerm.datafactoryv2/set-azurermdatafactoryv2integrationruntime?view=azurermps-4.4.1) cmdlet.</span></span> <span data-ttu-id="9464c-129">The following sample command scales out an Azure-SSIS integration runtime to five nodes.</span><span class="sxs-lookup"><span data-stu-id="9464c-129">The following sample command scales out an Azure-SSIS integration runtime to five nodes.</span></span>

    ```powershell
    Set-AzureRmDataFactoryV2IntegrationRuntime -DataFactoryName $DataFactoryName -Name $AzureSSISName -ResourceGroupName $ResourceGroupName -NodeCount 5
    ```  
3. <span data-ttu-id="9464c-130">Then, start the Azure-SSIS integration runtime by using the [Start-AzureRmDataFactoryV2IntegrationRuntime](/powershell/module/azurerm.datafactoryv2/start-azurermdatafactoryv2integrationruntime?view=azurermps-4.4.1) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9464c-130">Then, start the Azure-SSIS integration runtime by using the [Start-AzureRmDataFactoryV2IntegrationRuntime](/powershell/module/azurerm.datafactoryv2/start-azurermdatafactoryv2integrationruntime?view=azurermps-4.4.1) cmdlet.</span></span> <span data-ttu-id="9464c-131">This command allocates all of its nodes for running SSIS packages.</span><span class="sxs-lookup"><span data-stu-id="9464c-131">This command allocates all of its nodes for running SSIS packages.</span></span>   

    ```powershell
    Start-AzureRmDataFactoryV2IntegrationRuntime -DataFactoryName $DataFactoryName -Name $AzureSSISName -ResourceGroupName $ResourceGroupName
    ```

### <a name="delete-an-azure-ssis-ir"></a><span data-ttu-id="9464c-132">Delete an Azure-SSIS IR</span><span class="sxs-lookup"><span data-stu-id="9464c-132">Delete an Azure-SSIS IR</span></span>
1. <span data-ttu-id="9464c-133">First, list all existing Azure SSIS IRs under your data factory.</span><span class="sxs-lookup"><span data-stu-id="9464c-133">First, list all existing Azure SSIS IRs under your data factory.</span></span>

    ```powershell
    Get-AzureRmDataFactoryV2IntegrationRuntime -DataFactoryName $DataFactoryName -ResourceGroupName $ResourceGroupName -Status
    ```
2. <span data-ttu-id="9464c-134">Next, stop all existing Azure SSIS IRs in your data factory.</span><span class="sxs-lookup"><span data-stu-id="9464c-134">Next, stop all existing Azure SSIS IRs in your data factory.</span></span>

    ```powershell
    Stop-AzureRmDataFactoryV2IntegrationRuntime -DataFactoryName $DataFactoryName -Name $AzureSSISName -ResourceGroupName $ResourceGroupName -Force
    ```
3. <span data-ttu-id="9464c-135">Next, remove all existing Azure SSIS IRs in your data factory one by one.</span><span class="sxs-lookup"><span data-stu-id="9464c-135">Next, remove all existing Azure SSIS IRs in your data factory one by one.</span></span>

    ```powershell
    Remove-AzureRmDataFactoryV2IntegrationRuntime -DataFactoryName $DataFactoryName -Name $AzureSSISName -ResourceGroupName $ResourceGroupName -Force
    ```
4. <span data-ttu-id="9464c-136">Finally, remove your data factory.</span><span class="sxs-lookup"><span data-stu-id="9464c-136">Finally, remove your data factory.</span></span>

    ```powershell
    Remove-AzureRmDataFactoryV2 -Name $DataFactoryName -ResourceGroupName $ResourceGroupName -Force
    ```
5. <span data-ttu-id="9464c-137">If you had created a new resource group, remove the resource group.</span><span class="sxs-lookup"><span data-stu-id="9464c-137">If you had created a new resource group, remove the resource group.</span></span>

    ```powershell
    Remove-AzureRmResourceGroup -Name $ResourceGroupName -Force 
    ```

## <a name="next-steps"></a><span data-ttu-id="9464c-138">Next steps</span><span class="sxs-lookup"><span data-stu-id="9464c-138">Next steps</span></span>
<span data-ttu-id="9464c-139">For more information about Azure-SSIS runtime, see the following topics:</span><span class="sxs-lookup"><span data-stu-id="9464c-139">For more information about Azure-SSIS runtime, see the following topics:</span></span> 

- <span data-ttu-id="9464c-140">[Azure-SSIS Integration Runtime](concepts-integration-runtime.md#azure-ssis-integration-runtime).</span><span class="sxs-lookup"><span data-stu-id="9464c-140">[Azure-SSIS Integration Runtime](concepts-integration-runtime.md#azure-ssis-integration-runtime).</span></span> <span data-ttu-id="9464c-141">This article provides conceptual information about integration runtimes in general including the Azure-SSIS IR.</span><span class="sxs-lookup"><span data-stu-id="9464c-141">This article provides conceptual information about integration runtimes in general including the Azure-SSIS IR.</span></span> 
- <span data-ttu-id="9464c-142">[Tutorial: deploy SSIS packages to Azure](tutorial-create-azure-ssis-runtime-portal.md).</span><span class="sxs-lookup"><span data-stu-id="9464c-142">[Tutorial: deploy SSIS packages to Azure](tutorial-create-azure-ssis-runtime-portal.md).</span></span> <span data-ttu-id="9464c-143">This article provides step-by-step instructions to create an Azure-SSIS IR and uses an Azure SQL database to host the SSIS catalog.</span><span class="sxs-lookup"><span data-stu-id="9464c-143">This article provides step-by-step instructions to create an Azure-SSIS IR and uses an Azure SQL database to host the SSIS catalog.</span></span> 
- <span data-ttu-id="9464c-144">[How to: Create an Azure-SSIS integration runtime](create-azure-ssis-integration-runtime.md).</span><span class="sxs-lookup"><span data-stu-id="9464c-144">[How to: Create an Azure-SSIS integration runtime](create-azure-ssis-integration-runtime.md).</span></span> <span data-ttu-id="9464c-145">This article expands on the tutorial and provides instructions on using Azure SQL Managed Instance (Preview) and joining the IR to a virtual network.</span><span class="sxs-lookup"><span data-stu-id="9464c-145">This article expands on the tutorial and provides instructions on using Azure SQL Managed Instance (Preview) and joining the IR to a virtual network.</span></span> 
- <span data-ttu-id="9464c-146">[Join an Azure-SSIS IR to a virtual network](join-azure-ssis-integration-runtime-virtual-network.md).</span><span class="sxs-lookup"><span data-stu-id="9464c-146">[Join an Azure-SSIS IR to a virtual network](join-azure-ssis-integration-runtime-virtual-network.md).</span></span> <span data-ttu-id="9464c-147">This article provides conceptual information about joining an Azure-SSIS IR to an Azure virtual network.</span><span class="sxs-lookup"><span data-stu-id="9464c-147">This article provides conceptual information about joining an Azure-SSIS IR to an Azure virtual network.</span></span> <span data-ttu-id="9464c-148">It also provides steps to use Azure portal to configure virtual network so that Azure-SSIS IR can join the virtual network.</span><span class="sxs-lookup"><span data-stu-id="9464c-148">It also provides steps to use Azure portal to configure virtual network so that Azure-SSIS IR can join the virtual network.</span></span> 
- <span data-ttu-id="9464c-149">[Monitor an Azure-SSIS IR](monitor-integration-runtime.md#azure-ssis-integration-runtime).</span><span class="sxs-lookup"><span data-stu-id="9464c-149">[Monitor an Azure-SSIS IR](monitor-integration-runtime.md#azure-ssis-integration-runtime).</span></span> <span data-ttu-id="9464c-150">This article shows you how to retrieve information about an Azure-SSIS IR and descriptions of statuses in the returned information.</span><span class="sxs-lookup"><span data-stu-id="9464c-150">This article shows you how to retrieve information about an Azure-SSIS IR and descriptions of statuses in the returned information.</span></span> 
 
