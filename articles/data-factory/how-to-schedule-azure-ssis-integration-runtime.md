---
title: How to schedule the Azure SSIS integration runtime | Microsoft Docs
description: This article describes how to schedule starting and stopping of an Azure SSIS integration runtime by using Azure Automation and Data Factory.
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
ms.openlocfilehash: f83715d2a382db271686210d9df285c255c09216
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869788"
---
# <a name="how-to-start-and-stop-the-azure-ssis-integration-runtime-on-a-schedule"></a><span data-ttu-id="d2dd9-103">How to start and stop the Azure SSIS integration runtime on a schedule</span><span class="sxs-lookup"><span data-stu-id="d2dd9-103">How to start and stop the Azure SSIS integration runtime on a schedule</span></span>
<span data-ttu-id="d2dd9-104">This article describes how to schedule starting and stopping of an Azure SSIS integration runtime (IR) by using Azure Automation and Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-104">This article describes how to schedule starting and stopping of an Azure SSIS integration runtime (IR) by using Azure Automation and Azure Data Factory.</span></span> <span data-ttu-id="d2dd9-105">Running an Azure SSIS (SQL Server Integration Services) integration runtime (IR) has a cost associated with it.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-105">Running an Azure SSIS (SQL Server Integration Services) integration runtime (IR) has a cost associated with it.</span></span> <span data-ttu-id="d2dd9-106">Therefore, you typically want to run the IR only when you need to run SSIS packages in Azure, and stop the IR when you don't need it.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-106">Therefore, you typically want to run the IR only when you need to run SSIS packages in Azure, and stop the IR when you don't need it.</span></span> <span data-ttu-id="d2dd9-107">You can use the Data Factory UI or Azure PowerShell to [manually start or stop an Azure SSIS IR](manage-azure-ssis-integration-runtime.md)).</span><span class="sxs-lookup"><span data-stu-id="d2dd9-107">You can use the Data Factory UI or Azure PowerShell to [manually start or stop an Azure SSIS IR](manage-azure-ssis-integration-runtime.md)).</span></span>

<span data-ttu-id="d2dd9-108">For example, you can create Web activities with webhooks to an Azure Automation PowerShell runbook and chain an Execute SSIS Package activity between them.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-108">For example, you can create Web activities with webhooks to an Azure Automation PowerShell runbook and chain an Execute SSIS Package activity between them.</span></span> <span data-ttu-id="d2dd9-109">The Web activities can start and stop your Azure-SSIS IR just in time before and after your package runs.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-109">The Web activities can start and stop your Azure-SSIS IR just in time before and after your package runs.</span></span> <span data-ttu-id="d2dd9-110">For more info about the Execute SSIS Package activity, see [Run an SSIS package using the SSIS Activity in Azure Data Factory](how-to-invoke-ssis-package-ssis-activity.md).</span><span class="sxs-lookup"><span data-stu-id="d2dd9-110">For more info about the Execute SSIS Package activity, see [Run an SSIS package using the SSIS Activity in Azure Data Factory](how-to-invoke-ssis-package-ssis-activity.md).</span></span>

## <a name="overview-of-the-steps"></a><span data-ttu-id="d2dd9-111">Overview of the steps</span><span class="sxs-lookup"><span data-stu-id="d2dd9-111">Overview of the steps</span></span>

<span data-ttu-id="d2dd9-112">Here are the high-level steps described in this article:</span><span class="sxs-lookup"><span data-stu-id="d2dd9-112">Here are the high-level steps described in this article:</span></span>

1. <span data-ttu-id="d2dd9-113">**Create and test an Azure Automation runbook.**</span><span class="sxs-lookup"><span data-stu-id="d2dd9-113">**Create and test an Azure Automation runbook.**</span></span> <span data-ttu-id="d2dd9-114">In this step, you create a PowerShell runbook with the script that starts or stops an Azure SSIS IR.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-114">In this step, you create a PowerShell runbook with the script that starts or stops an Azure SSIS IR.</span></span> <span data-ttu-id="d2dd9-115">Then, you test the runbook in both START and STOP scenarios and confirm that IR starts or stops.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-115">Then, you test the runbook in both START and STOP scenarios and confirm that IR starts or stops.</span></span> 
2. <span data-ttu-id="d2dd9-116">**Create two schedules for the runbook.**</span><span class="sxs-lookup"><span data-stu-id="d2dd9-116">**Create two schedules for the runbook.**</span></span> <span data-ttu-id="d2dd9-117">For the first schedule, you configure the runbook with START as the operation.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-117">For the first schedule, you configure the runbook with START as the operation.</span></span> <span data-ttu-id="d2dd9-118">For the second schedule, configure the runbook with STOP as the operation.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-118">For the second schedule, configure the runbook with STOP as the operation.</span></span> <span data-ttu-id="d2dd9-119">For both the schedules, you specify the cadence at which the runbook is run.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-119">For both the schedules, you specify the cadence at which the runbook is run.</span></span> <span data-ttu-id="d2dd9-120">For example, you may want to schedule the first one to run at 8 AM every day and the second one to run at 11 PM everyday.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-120">For example, you may want to schedule the first one to run at 8 AM every day and the second one to run at 11 PM everyday.</span></span> <span data-ttu-id="d2dd9-121">When the first runbook runs, it starts the Azure SSIS IR.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-121">When the first runbook runs, it starts the Azure SSIS IR.</span></span> <span data-ttu-id="d2dd9-122">When the second runbook runs, it stops the Azure SSIS IR.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-122">When the second runbook runs, it stops the Azure SSIS IR.</span></span> 
3. <span data-ttu-id="d2dd9-123">**Create two webhooks for the runbook**, one for the START operation and the other for the STOP operation.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-123">**Create two webhooks for the runbook**, one for the START operation and the other for the STOP operation.</span></span> <span data-ttu-id="d2dd9-124">You use the URLs of these webhooks when configuring web activities in a Data Factory pipeline.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-124">You use the URLs of these webhooks when configuring web activities in a Data Factory pipeline.</span></span> 
4. <span data-ttu-id="d2dd9-125">**Create a Data Factory pipeline**.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-125">**Create a Data Factory pipeline**.</span></span> <span data-ttu-id="d2dd9-126">The pipeline you create consists of three activities.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-126">The pipeline you create consists of three activities.</span></span> <span data-ttu-id="d2dd9-127">The first **Web** activity invokes the first webhook to start the Azure SSIS IR.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-127">The first **Web** activity invokes the first webhook to start the Azure SSIS IR.</span></span> <span data-ttu-id="d2dd9-128">The **Stored Procedure** activity runs a SQL script that runs the SSIS package.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-128">The **Stored Procedure** activity runs a SQL script that runs the SSIS package.</span></span> <span data-ttu-id="d2dd9-129">The second **Web** activity stops the Azure SSIS IR.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-129">The second **Web** activity stops the Azure SSIS IR.</span></span> <span data-ttu-id="d2dd9-130">For more information about invoking an SSIS package from a Data Factory pipeline by using the Stored Procedure activity, see [Invoke an SSIS package](how-to-invoke-ssis-package-stored-procedure-activity.md).</span><span class="sxs-lookup"><span data-stu-id="d2dd9-130">For more information about invoking an SSIS package from a Data Factory pipeline by using the Stored Procedure activity, see [Invoke an SSIS package](how-to-invoke-ssis-package-stored-procedure-activity.md).</span></span> <span data-ttu-id="d2dd9-131">Then, you create a schedule trigger to schedule the pipeline to run at the cadence you specify.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-131">Then, you create a schedule trigger to schedule the pipeline to run at the cadence you specify.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d2dd9-132">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d2dd9-132">Prerequisites</span></span>
<span data-ttu-id="d2dd9-133">If you haven't provisioned an Azure SSIS integration runtime already, provision it by following instructions in the [tutorial](tutorial-create-azure-ssis-runtime-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d2dd9-133">If you haven't provisioned an Azure SSIS integration runtime already, provision it by following instructions in the [tutorial](tutorial-create-azure-ssis-runtime-portal.md).</span></span> 

## <a name="create-and-test-an-azure-automation-runbook"></a><span data-ttu-id="d2dd9-134">Create and test an Azure Automation runbook</span><span class="sxs-lookup"><span data-stu-id="d2dd9-134">Create and test an Azure Automation runbook</span></span>
<span data-ttu-id="d2dd9-135">In this section, you perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d2dd9-135">In this section, you perform the following steps:</span></span> 

1. <span data-ttu-id="d2dd9-136">Create an Azure Automation account.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-136">Create an Azure Automation account.</span></span>
2. <span data-ttu-id="d2dd9-137">Create a PowerShell runbook in the Azure Automation account.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-137">Create a PowerShell runbook in the Azure Automation account.</span></span> <span data-ttu-id="d2dd9-138">The PowerShell script associated with the runbook either starts or stops an Azure SSIS IR based on the command you specify for the OPERATION parameter.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-138">The PowerShell script associated with the runbook either starts or stops an Azure SSIS IR based on the command you specify for the OPERATION parameter.</span></span> 
3. <span data-ttu-id="d2dd9-139">Test the runbook in both start and stop scenarios to confirm that it works.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-139">Test the runbook in both start and stop scenarios to confirm that it works.</span></span> 

### <a name="create-an-azure-automation-account"></a><span data-ttu-id="d2dd9-140">Create an Azure Automation account</span><span class="sxs-lookup"><span data-stu-id="d2dd9-140">Create an Azure Automation account</span></span>
<span data-ttu-id="d2dd9-141">If you don't have an Azure Automation account, create one by following the instructions in this step.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-141">If you don't have an Azure Automation account, create one by following the instructions in this step.</span></span> <span data-ttu-id="d2dd9-142">For detailed steps, see [Create an Azure Automation account](../automation/automation-quickstart-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="d2dd9-142">For detailed steps, see [Create an Azure Automation account](../automation/automation-quickstart-create-account.md).</span></span> <span data-ttu-id="d2dd9-143">As part of this step, you create an **Azure Run As** account (a service principal in your Azure Active Directory), and add it to the **Contributor** role of your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-143">As part of this step, you create an **Azure Run As** account (a service principal in your Azure Active Directory), and add it to the **Contributor** role of your Azure subscription.</span></span> <span data-ttu-id="d2dd9-144">Ensure that it's same as the subscription that contains the data factory that has the Azure SSIS IR.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-144">Ensure that it's same as the subscription that contains the data factory that has the Azure SSIS IR.</span></span> <span data-ttu-id="d2dd9-145">Azure Automation uses this account to authenticate to Azure Resource Manager and operate on your resources.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-145">Azure Automation uses this account to authenticate to Azure Resource Manager and operate on your resources.</span></span> 

1. <span data-ttu-id="d2dd9-146">Launch **Microsoft Edge** or **Google Chrome** web browser.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-146">Launch **Microsoft Edge** or **Google Chrome** web browser.</span></span> <span data-ttu-id="d2dd9-147">Currently, Data Factory UI is supported only in Microsoft Edge and Google Chrome web browsers.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-147">Currently, Data Factory UI is supported only in Microsoft Edge and Google Chrome web browsers.</span></span>
2. <span data-ttu-id="d2dd9-148">Log in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="d2dd9-148">Log in to the [Azure portal](https://portal.azure.com/).</span></span>    
3. <span data-ttu-id="d2dd9-149">Select **New** on the left menu, select **Monitoring + Management**, and select **Automation**.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-149">Select **New** on the left menu, select **Monitoring + Management**, and select **Automation**.</span></span> 

    ![New -> Monitoring + Management -> Automation](./media/how-to-schedule-azure-ssis-integration-runtime/new-automation.png)
2. <span data-ttu-id="d2dd9-151">In the **Add Automation Account** window, take the following steps:</span><span class="sxs-lookup"><span data-stu-id="d2dd9-151">In the **Add Automation Account** window, take the following steps:</span></span> 

    1. <span data-ttu-id="d2dd9-152">Specify a **name** for the automation account.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-152">Specify a **name** for the automation account.</span></span> 
    2. <span data-ttu-id="d2dd9-153">Select the **subscription** that has the data factory with Azure SSIS IR.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-153">Select the **subscription** that has the data factory with Azure SSIS IR.</span></span> 
    3. <span data-ttu-id="d2dd9-154">For **Resource group**, select **Create new** to create a new resource group, or select **Use existing** to select an existing resource group.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-154">For **Resource group**, select **Create new** to create a new resource group, or select **Use existing** to select an existing resource group.</span></span> 
    4. <span data-ttu-id="d2dd9-155">Select a **location** for the automation account.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-155">Select a **location** for the automation account.</span></span> 
    5. <span data-ttu-id="d2dd9-156">Confirm that **Create Run As account** is set to **Yes**.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-156">Confirm that **Create Run As account** is set to **Yes**.</span></span> <span data-ttu-id="d2dd9-157">A service principal is created in your Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-157">A service principal is created in your Azure Active Directory.</span></span> <span data-ttu-id="d2dd9-158">It's added to the **Contributor** role of your Azure subscription</span><span class="sxs-lookup"><span data-stu-id="d2dd9-158">It's added to the **Contributor** role of your Azure subscription</span></span>
    6. <span data-ttu-id="d2dd9-159">Select **Pin to dashboard** so that you see it on the dashboard of the portal.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-159">Select **Pin to dashboard** so that you see it on the dashboard of the portal.</span></span> 
    7. <span data-ttu-id="d2dd9-160">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-160">Select **Create**.</span></span> 

        ![New -> Monitoring + Management -> Automation](./media/how-to-schedule-azure-ssis-integration-runtime/add-automation-account-window.png)
3. <span data-ttu-id="d2dd9-162">You see the **deployment status** on the dashboard and in the notifications.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-162">You see the **deployment status** on the dashboard and in the notifications.</span></span> 
    
    ![Deploying automation](./media/how-to-schedule-azure-ssis-integration-runtime/deploying-automation.png) 
4. <span data-ttu-id="d2dd9-164">You see the home page for the automation account after it's created successfully.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-164">You see the home page for the automation account after it's created successfully.</span></span> 

    ![Automation home page](./media/how-to-schedule-azure-ssis-integration-runtime/automation-home-page.png)

### <a name="import-data-factory-modules"></a><span data-ttu-id="d2dd9-166">Import Data Factory modules</span><span class="sxs-lookup"><span data-stu-id="d2dd9-166">Import Data Factory modules</span></span>

1. <span data-ttu-id="d2dd9-167">Select **Modules** in the **SHARED RESOURCES** section on the left menu, and verify whether you have **AzureRM.Profile** and **AzureRM.DataFactoryV2** in the list of modules.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-167">Select **Modules** in the **SHARED RESOURCES** section on the left menu, and verify whether you have **AzureRM.Profile** and **AzureRM.DataFactoryV2** in the list of modules.</span></span>

    ![Verify the required modules](media/how-to-schedule-azure-ssis-integration-runtime/automation-fix-image1.png)

2.  <span data-ttu-id="d2dd9-169">Go to the PowerShell Gallery for the [AzureRM.DataFactoryV2 module](https://www.powershellgallery.com/packages/AzureRM.DataFactoryV2/), select **Deploy to Azure Automation**, select your Automation account, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-169">Go to the PowerShell Gallery for the [AzureRM.DataFactoryV2 module](https://www.powershellgallery.com/packages/AzureRM.DataFactoryV2/), select **Deploy to Azure Automation**, select your Automation account, and then select **OK**.</span></span> <span data-ttu-id="d2dd9-170">Go back to view **Modules** in the **SHARED RESOURCES** section on the left menu, and wait until you see the **STATUS** of the **AzureRM.DataFactoryV2** module change to **Available**.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-170">Go back to view **Modules** in the **SHARED RESOURCES** section on the left menu, and wait until you see the **STATUS** of the **AzureRM.DataFactoryV2** module change to **Available**.</span></span>

    ![Verify the Data Factory module](media/how-to-schedule-azure-ssis-integration-runtime/automation-fix-image2.png)

3.  <span data-ttu-id="d2dd9-172">Go to the PowerShell Gallery for the [AzureRM.Profile module](https://www.powershellgallery.com/packages/AzureRM.profile/), click on **Deploy to Azure Automation**, select your Automation account, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-172">Go to the PowerShell Gallery for the [AzureRM.Profile module](https://www.powershellgallery.com/packages/AzureRM.profile/), click on **Deploy to Azure Automation**, select your Automation account, and then select **OK**.</span></span> <span data-ttu-id="d2dd9-173">Go back to view **Modules** in the **SHARED RESOURCES** section on the left menu, and wait until you see the **STATUS** of the **AzureRM.Profile** module change to **Available**.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-173">Go back to view **Modules** in the **SHARED RESOURCES** section on the left menu, and wait until you see the **STATUS** of the **AzureRM.Profile** module change to **Available**.</span></span>

    ![Verify the Profile module](media/how-to-schedule-azure-ssis-integration-runtime/automation-fix-image3.png)

### <a name="create-a-powershell-runbook"></a><span data-ttu-id="d2dd9-175">Create a PowerShell runbook</span><span class="sxs-lookup"><span data-stu-id="d2dd9-175">Create a PowerShell runbook</span></span>
<span data-ttu-id="d2dd9-176">The following procedure provides steps for creating a PowerShell runbook.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-176">The following procedure provides steps for creating a PowerShell runbook.</span></span> <span data-ttu-id="d2dd9-177">The script associated with the runbook either starts/stops an Azure SSIS IR based on the command you specify for the **OPERATION** parameter.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-177">The script associated with the runbook either starts/stops an Azure SSIS IR based on the command you specify for the **OPERATION** parameter.</span></span> <span data-ttu-id="d2dd9-178">This section does not provide all the details for creating a runbook.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-178">This section does not provide all the details for creating a runbook.</span></span> <span data-ttu-id="d2dd9-179">For more information, see [Create a runbook](../automation/automation-quickstart-create-runbook.md) article.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-179">For more information, see [Create a runbook](../automation/automation-quickstart-create-runbook.md) article.</span></span>

1. <span data-ttu-id="d2dd9-180">Switch to the **Runbooks** tab, and select **+ Add a runbook** from the toolbar.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-180">Switch to the **Runbooks** tab, and select **+ Add a runbook** from the toolbar.</span></span> 

    ![Add a runbook button](./media/how-to-schedule-azure-ssis-integration-runtime/runbooks-window.png)
2. <span data-ttu-id="d2dd9-182">Select **Create a new runbook**, and perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d2dd9-182">Select **Create a new runbook**, and perform the following steps:</span></span> 

    1. <span data-ttu-id="d2dd9-183">For **Name**, type **StartStopAzureSsisRuntime**.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-183">For **Name**, type **StartStopAzureSsisRuntime**.</span></span>
    2. <span data-ttu-id="d2dd9-184">For **Runbook type**, select **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-184">For **Runbook type**, select **PowerShell**.</span></span>
    3. <span data-ttu-id="d2dd9-185">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-185">Select **Create**.</span></span>
    
        ![Add a runbook button](./media/how-to-schedule-azure-ssis-integration-runtime/add-runbook-window.png)
3. <span data-ttu-id="d2dd9-187">Copy/paste the following script to the runbook script window.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-187">Copy/paste the following script to the runbook script window.</span></span> <span data-ttu-id="d2dd9-188">Save and then publish the runbook by using the **Save** and **Publish** buttons on the toolbar.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-188">Save and then publish the runbook by using the **Save** and **Publish** buttons on the toolbar.</span></span> 

    ```powershell
    Param
    (
          [Parameter (Mandatory= $true)]
          [String] $ResourceGroupName,
    
          [Parameter (Mandatory= $true)]
          [String] $DataFactoryName,
    
          [Parameter (Mandatory= $true)]
          [String] $AzureSSISName,
    
          [Parameter (Mandatory= $true)]
          [String] $Operation
    )
    
    $connectionName = "AzureRunAsConnection"
    try
    {
        # Get the connection "AzureRunAsConnection "
        $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         
    
        "Logging in to Azure..."
        Connect-AzureRmAccount `
            -ServicePrincipal `
            -TenantId $servicePrincipalConnection.TenantId `
            -ApplicationId $servicePrincipalConnection.ApplicationId `
            -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint 
    }
    catch {
        if (!$servicePrincipalConnection)
        {
            $ErrorMessage = "Connection $connectionName not found."
            throw $ErrorMessage
        } else{
            Write-Error -Message $_.Exception
            throw $_.Exception
        }
    }
    
    if($Operation -eq "START" -or $operation -eq "start")
    {
        "##### Starting #####"
        Start-AzureRmDataFactoryV2IntegrationRuntime -ResourceGroupName $ResourceGroupName -DataFactoryName $DataFactoryName -Name $AzureSSISName -Force
    }
    elseif($Operation -eq "STOP" -or $operation -eq "stop")
    {
        "##### Stopping #####"
        Stop-AzureRmDataFactoryV2IntegrationRuntime -DataFactoryName $DataFactoryName -Name $AzureSSISName -ResourceGroupName $ResourceGroupName -Force
    }  
    "##### Completed #####"    
    ```

    ![Edit PowerShell runbook](./media/how-to-schedule-azure-ssis-integration-runtime/edit-powershell-runbook.png)
5. <span data-ttu-id="d2dd9-190">Test the runbook by selecting **Start** button on the toolbar.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-190">Test the runbook by selecting **Start** button on the toolbar.</span></span> 

    ![Start runbook button](./media/how-to-schedule-azure-ssis-integration-runtime/start-runbook-button.png)
6. <span data-ttu-id="d2dd9-192">In the **Start Runbook** window, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d2dd9-192">In the **Start Runbook** window, perform the following steps:</span></span> 

    1. <span data-ttu-id="d2dd9-193">For **RESOURCE GROUP NAME**, enter the name of the resource group with the data factory that has the Azure SSIS IR.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-193">For **RESOURCE GROUP NAME**, enter the name of the resource group with the data factory that has the Azure SSIS IR.</span></span> 
    2. <span data-ttu-id="d2dd9-194">For **DATA FACTORY NAME**, enter the name of the data factory that has the Azure SSIS IR.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-194">For **DATA FACTORY NAME**, enter the name of the data factory that has the Azure SSIS IR.</span></span> 
    3. <span data-ttu-id="d2dd9-195">For **AZURESSISNAME**, enter the name of the Azure SSIS IR.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-195">For **AZURESSISNAME**, enter the name of the Azure SSIS IR.</span></span> 
    4. <span data-ttu-id="d2dd9-196">For **OPERATION**, enter **START**.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-196">For **OPERATION**, enter **START**.</span></span> 
    5. <span data-ttu-id="d2dd9-197">Select **OK**.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-197">Select **OK**.</span></span>  

        ![Start runbook window](./media/how-to-schedule-azure-ssis-integration-runtime/start-runbook-window.png)
7. <span data-ttu-id="d2dd9-199">In the job window, select **Output** tile.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-199">In the job window, select **Output** tile.</span></span> <span data-ttu-id="d2dd9-200">In the output window of the job, wait until you see the message **##### Completed #####** after you see **##### Starting #####**.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-200">In the output window of the job, wait until you see the message **##### Completed #####** after you see **##### Starting #####**.</span></span> <span data-ttu-id="d2dd9-201">Starting an Azure SSIS IR takes approximately 20 minutes.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-201">Starting an Azure SSIS IR takes approximately 20 minutes.</span></span> <span data-ttu-id="d2dd9-202">Close the **Job** window, and get back to the **Runbook** window.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-202">Close the **Job** window, and get back to the **Runbook** window.</span></span>

    ![Azure SSIS IR - started](./media/how-to-schedule-azure-ssis-integration-runtime/start-completed.png)
8.  <span data-ttu-id="d2dd9-204">Repeat the previous two steps, but by using **STOP** as the value for the **OPERATION**.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-204">Repeat the previous two steps, but by using **STOP** as the value for the **OPERATION**.</span></span> <span data-ttu-id="d2dd9-205">Start the runbook again by selecting the **Start** button on the toolbar.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-205">Start the runbook again by selecting the **Start** button on the toolbar.</span></span> <span data-ttu-id="d2dd9-206">Specify the resource group name, data factory name, and Azure SSIS IR name.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-206">Specify the resource group name, data factory name, and Azure SSIS IR name.</span></span> <span data-ttu-id="d2dd9-207">For **OPERATION**, enter **STOP**.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-207">For **OPERATION**, enter **STOP**.</span></span> 

    <span data-ttu-id="d2dd9-208">In the output window of the job, wait until you see message **##### Completed #####** after you see **##### Stopping #####**.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-208">In the output window of the job, wait until you see message **##### Completed #####** after you see **##### Stopping #####**.</span></span> <span data-ttu-id="d2dd9-209">Stopping an Azure SSIS IR does not take as long as starting the Azure SSIS IR.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-209">Stopping an Azure SSIS IR does not take as long as starting the Azure SSIS IR.</span></span> <span data-ttu-id="d2dd9-210">Close the **Job** window, and get back to the **Runbook** window.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-210">Close the **Job** window, and get back to the **Runbook** window.</span></span>

## <a name="create-schedules-for-the-runbook-to-startstop-the-azure-ssis-ir"></a><span data-ttu-id="d2dd9-211">Create schedules for the runbook to start/stop the Azure SSIS IR</span><span class="sxs-lookup"><span data-stu-id="d2dd9-211">Create schedules for the runbook to start/stop the Azure SSIS IR</span></span>
<span data-ttu-id="d2dd9-212">In the previous section, you created an Azure Automation runbook that can either start or stop an Azure SSIS IR.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-212">In the previous section, you created an Azure Automation runbook that can either start or stop an Azure SSIS IR.</span></span> <span data-ttu-id="d2dd9-213">In this section, you create two schedules for the runbook.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-213">In this section, you create two schedules for the runbook.</span></span> <span data-ttu-id="d2dd9-214">When configuring the first schedule, you specify START for the OPERATION parameter.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-214">When configuring the first schedule, you specify START for the OPERATION parameter.</span></span> <span data-ttu-id="d2dd9-215">Similarly, when configuring the second schedule, you specify STOP for the OPERATION.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-215">Similarly, when configuring the second schedule, you specify STOP for the OPERATION.</span></span> <span data-ttu-id="d2dd9-216">For detailed steps for creating schedules, see [Create a schedule](../automation/automation-schedules.md#creating-a-schedule).</span><span class="sxs-lookup"><span data-stu-id="d2dd9-216">For detailed steps for creating schedules, see [Create a schedule](../automation/automation-schedules.md#creating-a-schedule).</span></span>

1. <span data-ttu-id="d2dd9-217">In the **Runbook** window, select **Schedules**, and select **+ Add a schedule** on the toolbar.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-217">In the **Runbook** window, select **Schedules**, and select **+ Add a schedule** on the toolbar.</span></span> 

    ![Azure SSIS IR - started](./media/how-to-schedule-azure-ssis-integration-runtime/add-schedules-button.png)
2. <span data-ttu-id="d2dd9-219">In the **Schedule Runbook** window, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d2dd9-219">In the **Schedule Runbook** window, perform the following steps:</span></span> 

    1. <span data-ttu-id="d2dd9-220">Select **Link a schedule to your runbook**.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-220">Select **Link a schedule to your runbook**.</span></span> 
    2. <span data-ttu-id="d2dd9-221">Select **Create a new schedule**.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-221">Select **Create a new schedule**.</span></span>
    3. <span data-ttu-id="d2dd9-222">In the **New Schedule** window, type **Start IR daily** for **Name**.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-222">In the **New Schedule** window, type **Start IR daily** for **Name**.</span></span> 
    4. <span data-ttu-id="d2dd9-223">In the **Starts section**, for the time, specify a time a few minutes past the current time.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-223">In the **Starts section**, for the time, specify a time a few minutes past the current time.</span></span> 
    5. <span data-ttu-id="d2dd9-224">For **Recurrence**, select **Recurring**.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-224">For **Recurrence**, select **Recurring**.</span></span> 
    6. <span data-ttu-id="d2dd9-225">In the **Recur every** section, select **Day**.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-225">In the **Recur every** section, select **Day**.</span></span> 
    7. <span data-ttu-id="d2dd9-226">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-226">Select **Create**.</span></span> 

        ![Schedule for Azure SSIS IR start](./media/how-to-schedule-azure-ssis-integration-runtime/new-schedule-start.png)
3. <span data-ttu-id="d2dd9-228">Switch to the **Parameters and run settings** tab. Specify the resource group name, data factory name, and Azure SSIS IR name.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-228">Switch to the **Parameters and run settings** tab. Specify the resource group name, data factory name, and Azure SSIS IR name.</span></span> <span data-ttu-id="d2dd9-229">For **OPERATION**, enter **START**.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-229">For **OPERATION**, enter **START**.</span></span> <span data-ttu-id="d2dd9-230">Select **OK**.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-230">Select **OK**.</span></span> <span data-ttu-id="d2dd9-231">Select **OK** again to see the schedule on the **Schedules** page of the runbook.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-231">Select **OK** again to see the schedule on the **Schedules** page of the runbook.</span></span> 

    ![Schedule for staring the Azure SSIS IR](./media/how-to-schedule-azure-ssis-integration-runtime/start-schedule.png)
4. <span data-ttu-id="d2dd9-233">Repeat the previous two steps to create a schedule named **Stop IR daily**.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-233">Repeat the previous two steps to create a schedule named **Stop IR daily**.</span></span> <span data-ttu-id="d2dd9-234">This time, specify time at least 30 minutes after the time you specified for the **Start IR daily** schedule.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-234">This time, specify time at least 30 minutes after the time you specified for the **Start IR daily** schedule.</span></span> <span data-ttu-id="d2dd9-235">For **OPERATION**, specify **STOP**.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-235">For **OPERATION**, specify **STOP**.</span></span> 
5. <span data-ttu-id="d2dd9-236">In the **Runbook** window, select **Jobs** on the left menu.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-236">In the **Runbook** window, select **Jobs** on the left menu.</span></span> <span data-ttu-id="d2dd9-237">You should see the jobs created by the schedules at the specified times and their statuses.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-237">You should see the jobs created by the schedules at the specified times and their statuses.</span></span> <span data-ttu-id="d2dd9-238">You can see details about the job such as its output similar to what you have seen when you tested the runbook.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-238">You can see details about the job such as its output similar to what you have seen when you tested the runbook.</span></span> 

    ![Schedule for staring the Azure SSIS IR](./media/how-to-schedule-azure-ssis-integration-runtime/schedule-jobs.png)
6. <span data-ttu-id="d2dd9-240">After you are done testing, disable the schedules by editing them and selecting **NO** for **Enabled**.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-240">After you are done testing, disable the schedules by editing them and selecting **NO** for **Enabled**.</span></span> <span data-ttu-id="d2dd9-241">Select **Schedules** in the left menu, select the **Start IR daily/Stop IR daily**, and select **No** for **Enabled**.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-241">Select **Schedules** in the left menu, select the **Start IR daily/Stop IR daily**, and select **No** for **Enabled**.</span></span> 

## <a name="create-webhooks-to-start-and-stop-the-azure-ssis-ir"></a><span data-ttu-id="d2dd9-242">Create webhooks to start and stop the Azure SSIS IR</span><span class="sxs-lookup"><span data-stu-id="d2dd9-242">Create webhooks to start and stop the Azure SSIS IR</span></span>
<span data-ttu-id="d2dd9-243">Follow instructions in [Create a webhook](../automation/automation-webhooks.md#creating-a-webhook) to create two webhooks for the runbook.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-243">Follow instructions in [Create a webhook](../automation/automation-webhooks.md#creating-a-webhook) to create two webhooks for the runbook.</span></span> <span data-ttu-id="d2dd9-244">For the first one, specify START as the OPERATION, and for the second one, specify STOP as the OPERATION.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-244">For the first one, specify START as the OPERATION, and for the second one, specify STOP as the OPERATION.</span></span> <span data-ttu-id="d2dd9-245">Save the URLs for both the webhooks somewhere (like a text file or a OneNote notebook).</span><span class="sxs-lookup"><span data-stu-id="d2dd9-245">Save the URLs for both the webhooks somewhere (like a text file or a OneNote notebook).</span></span> <span data-ttu-id="d2dd9-246">You use these URLs when configuring Web activities in the Data Factory pipeline.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-246">You use these URLs when configuring Web activities in the Data Factory pipeline.</span></span> <span data-ttu-id="d2dd9-247">The following image shown an example of creating a webhook that starts the Azure SSIS IR:</span><span class="sxs-lookup"><span data-stu-id="d2dd9-247">The following image shown an example of creating a webhook that starts the Azure SSIS IR:</span></span>

1. <span data-ttu-id="d2dd9-248">In the **Runbook** window, select **Webhooks** from the left menu, and select **+ Add Webhook** on the toolbar.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-248">In the **Runbook** window, select **Webhooks** from the left menu, and select **+ Add Webhook** on the toolbar.</span></span> 

    ![Webhooks -> Add Webhook](./media/how-to-schedule-azure-ssis-integration-runtime/add-web-hook-menu.png)
2. <span data-ttu-id="d2dd9-250">In the **Add Webhook** window, select **Create new webhook**, and do the following actions:</span><span class="sxs-lookup"><span data-stu-id="d2dd9-250">In the **Add Webhook** window, select **Create new webhook**, and do the following actions:</span></span> 

    1. <span data-ttu-id="d2dd9-251">For **Name**, enter **StartAzureSsisIR**.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-251">For **Name**, enter **StartAzureSsisIR**.</span></span> 
    2. <span data-ttu-id="d2dd9-252">Confirm that **Enabled** is set to **Yes**.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-252">Confirm that **Enabled** is set to **Yes**.</span></span> 
    3. <span data-ttu-id="d2dd9-253">Copy the **URL** and save it somewhere.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-253">Copy the **URL** and save it somewhere.</span></span> <span data-ttu-id="d2dd9-254">This step is important.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-254">This step is important.</span></span> <span data-ttu-id="d2dd9-255">You do not see the URL later.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-255">You do not see the URL later.</span></span> 
    4. <span data-ttu-id="d2dd9-256">Select **OK**.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-256">Select **OK**.</span></span> 

        ![New Webhook window](./media/how-to-schedule-azure-ssis-integration-runtime/new-web-hook-window.png)
3. <span data-ttu-id="d2dd9-258">Switch to the **Parameters and run settings** tab. Specify the resource group name, the data factory name, and the Azure SSIS IR name.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-258">Switch to the **Parameters and run settings** tab. Specify the resource group name, the data factory name, and the Azure SSIS IR name.</span></span> <span data-ttu-id="d2dd9-259">For **OPERATION**, enter **START**.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-259">For **OPERATION**, enter **START**.</span></span> <span data-ttu-id="d2dd9-260">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-260">Click **OK**.</span></span> <span data-ttu-id="d2dd9-261">Then, click **Create**.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-261">Then, click **Create**.</span></span> 

    ![Webhook - parameters and run settings](./media/how-to-schedule-azure-ssis-integration-runtime/webhook-parameters.png)
4. <span data-ttu-id="d2dd9-263">Repeat the previous three steps to create another webhook named **StopAzureSsisIR**.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-263">Repeat the previous three steps to create another webhook named **StopAzureSsisIR**.</span></span> <span data-ttu-id="d2dd9-264">Don't forget to copy the URL.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-264">Don't forget to copy the URL.</span></span> <span data-ttu-id="d2dd9-265">When specifying the parameters and run settings, enter **STOP** for **OPERATION**.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-265">When specifying the parameters and run settings, enter **STOP** for **OPERATION**.</span></span> 

<span data-ttu-id="d2dd9-266">You should have two URLs, one for the **StartAzureSsisIR** webhook and the other for the **StopAzureSsisIR** webhook.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-266">You should have two URLs, one for the **StartAzureSsisIR** webhook and the other for the **StopAzureSsisIR** webhook.</span></span> <span data-ttu-id="d2dd9-267">You can send an HTTP POST request to these URLs to start/stop your Azure SSIS IR.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-267">You can send an HTTP POST request to these URLs to start/stop your Azure SSIS IR.</span></span> 

## <a name="create-and-schedule-a-data-factory-pipeline-that-startsstops-the-ir"></a><span data-ttu-id="d2dd9-268">Create and schedule a Data Factory pipeline that starts/stops the IR</span><span class="sxs-lookup"><span data-stu-id="d2dd9-268">Create and schedule a Data Factory pipeline that starts/stops the IR</span></span>
<span data-ttu-id="d2dd9-269">This section shows how to use a Web activity to invoke the webhooks you created in the previous section.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-269">This section shows how to use a Web activity to invoke the webhooks you created in the previous section.</span></span>

<span data-ttu-id="d2dd9-270">The pipeline you create consists of three activities.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-270">The pipeline you create consists of three activities.</span></span> 

1. <span data-ttu-id="d2dd9-271">The first **Web** activity invokes the first webhook to start the Azure SSIS IR.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-271">The first **Web** activity invokes the first webhook to start the Azure SSIS IR.</span></span> 
2. <span data-ttu-id="d2dd9-272">The **Execute SSIS Package** activity or the **Stored Procedure** activity runs the SSIS package.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-272">The **Execute SSIS Package** activity or the **Stored Procedure** activity runs the SSIS package.</span></span>
3. <span data-ttu-id="d2dd9-273">The second **Web** activity invokes the webhook to stop the Azure SSIS IR.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-273">The second **Web** activity invokes the webhook to stop the Azure SSIS IR.</span></span> 

<span data-ttu-id="d2dd9-274">After you create and test the pipeline, you create a schedule trigger and associate with the pipeline.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-274">After you create and test the pipeline, you create a schedule trigger and associate with the pipeline.</span></span> <span data-ttu-id="d2dd9-275">The schedule trigger defines a schedule for the pipeline.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-275">The schedule trigger defines a schedule for the pipeline.</span></span> <span data-ttu-id="d2dd9-276">Suppose, you create a trigger that is scheduled to run daily at 11 PM.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-276">Suppose, you create a trigger that is scheduled to run daily at 11 PM.</span></span> <span data-ttu-id="d2dd9-277">The trigger runs the pipeline at 11 PM every day.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-277">The trigger runs the pipeline at 11 PM every day.</span></span> <span data-ttu-id="d2dd9-278">The pipeline starts the Azure SSIS IR, executes the SSIS package, and then stops the Azure SSIS IR.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-278">The pipeline starts the Azure SSIS IR, executes the SSIS package, and then stops the Azure SSIS IR.</span></span> 

### <a name="create-a-data-factory"></a><span data-ttu-id="d2dd9-279">Create a data factory</span><span class="sxs-lookup"><span data-stu-id="d2dd9-279">Create a data factory</span></span>

1. <span data-ttu-id="d2dd9-280">Log in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="d2dd9-280">Log in to the [Azure portal](https://portal.azure.com/).</span></span>    
2. <span data-ttu-id="d2dd9-281">Click **New** on the left menu, click **Data + Analytics**, and click **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-281">Click **New** on the left menu, click **Data + Analytics**, and click **Data Factory**.</span></span> 
   
   ![New->DataFactory](./media/tutorial-create-azure-ssis-runtime-portal/new-data-factory-menu.png)
3. <span data-ttu-id="d2dd9-283">In the **New data factory** page, enter **MyAzureSsisDataFactory** for the **name**.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-283">In the **New data factory** page, enter **MyAzureSsisDataFactory** for the **name**.</span></span> 
      
     ![New data factory page](./media/tutorial-create-azure-ssis-runtime-portal/new-azure-data-factory.png)
 
   <span data-ttu-id="d2dd9-285">The name of the Azure data factory must be **globally unique**.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-285">The name of the Azure data factory must be **globally unique**.</span></span> <span data-ttu-id="d2dd9-286">If you receive the following error, change the name of the data factory (for example, yournameMyAzureSsisDataFactory) and try creating again.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-286">If you receive the following error, change the name of the data factory (for example, yournameMyAzureSsisDataFactory) and try creating again.</span></span> <span data-ttu-id="d2dd9-287">See [Data Factory - Naming Rules](naming-rules.md) article for naming rules for Data Factory artifacts.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-287">See [Data Factory - Naming Rules](naming-rules.md) article for naming rules for Data Factory artifacts.</span></span>
  
       `Data factory name �MyAzureSsisDataFactory� is not available`
3. <span data-ttu-id="d2dd9-288">Select your Azure **subscription** in which you want to create the data factory.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-288">Select your Azure **subscription** in which you want to create the data factory.</span></span> 
4. <span data-ttu-id="d2dd9-289">For the **Resource Group**, do one of the following steps:</span><span class="sxs-lookup"><span data-stu-id="d2dd9-289">For the **Resource Group**, do one of the following steps:</span></span>
     
      - <span data-ttu-id="d2dd9-290">Select **Use existing**, and select an existing resource group from the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-290">Select **Use existing**, and select an existing resource group from the drop-down list.</span></span> 
      - <span data-ttu-id="d2dd9-291">Select **Create new**, and enter the name of a resource group.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-291">Select **Create new**, and enter the name of a resource group.</span></span>   
         
      <span data-ttu-id="d2dd9-292">To learn about resource groups, see [Using resource groups to manage your Azure resources](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d2dd9-292">To learn about resource groups, see [Using resource groups to manage your Azure resources](../azure-resource-manager/resource-group-overview.md).</span></span>  
4. <span data-ttu-id="d2dd9-293">Select **V2** for the **version**.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-293">Select **V2** for the **version**.</span></span>
5. <span data-ttu-id="d2dd9-294">Select the **location** for the data factory.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-294">Select the **location** for the data factory.</span></span> <span data-ttu-id="d2dd9-295">Only locations that are supported for creation of data factories are shown in the list.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-295">Only locations that are supported for creation of data factories are shown in the list.</span></span>
6. <span data-ttu-id="d2dd9-296">Select **Pin to dashboard**.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-296">Select **Pin to dashboard**.</span></span>     
7. <span data-ttu-id="d2dd9-297">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-297">Click **Create**.</span></span>
8. <span data-ttu-id="d2dd9-298">On the dashboard, you see the following tile with status: **Deploying data factory**.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-298">On the dashboard, you see the following tile with status: **Deploying data factory**.</span></span> 

    ![deploying data factory tile](media/tutorial-create-azure-ssis-runtime-portal/deploying-data-factory.png)
9. <span data-ttu-id="d2dd9-300">After the creation is complete, you see the **Data Factory** page as shown in the image.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-300">After the creation is complete, you see the **Data Factory** page as shown in the image.</span></span>
   
   ![Data factory home page](./media/tutorial-create-azure-ssis-runtime-portal/data-factory-home-page.png)
10. <span data-ttu-id="d2dd9-302">Click **Author & Monitor** to launch the Data Factory User Interface (UI) in a separate tab.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-302">Click **Author & Monitor** to launch the Data Factory User Interface (UI) in a separate tab.</span></span>

### <a name="create-a-pipeline"></a><span data-ttu-id="d2dd9-303">Create a pipeline</span><span class="sxs-lookup"><span data-stu-id="d2dd9-303">Create a pipeline</span></span>

1. <span data-ttu-id="d2dd9-304">In the **Get started** page, select **Create pipeline**.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-304">In the **Get started** page, select **Create pipeline**.</span></span> 

   ![Get started page](./media/how-to-schedule-azure-ssis-integration-runtime/get-started-page.png)
2. <span data-ttu-id="d2dd9-306">In the **Activities** toolbox, expand **General**, drag-drop the **Web** activity onto the pipeline designer surface.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-306">In the **Activities** toolbox, expand **General**, drag-drop the **Web** activity onto the pipeline designer surface.</span></span> <span data-ttu-id="d2dd9-307">In the **General** tab of the **Properties** window, change the name of the activity to **StartIR**.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-307">In the **General** tab of the **Properties** window, change the name of the activity to **StartIR**.</span></span>

   ![First Web activity - general tab](./media/how-to-schedule-azure-ssis-integration-runtime/first-web-activity-general-tab.png)
3. <span data-ttu-id="d2dd9-309">Switch to the **Settings** tab in the **Properties** window, and do the following actions:</span><span class="sxs-lookup"><span data-stu-id="d2dd9-309">Switch to the **Settings** tab in the **Properties** window, and do the following actions:</span></span> 

    1. <span data-ttu-id="d2dd9-310">For **URL**, paste the URL for the webhook that starts the Azure SSIS IR.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-310">For **URL**, paste the URL for the webhook that starts the Azure SSIS IR.</span></span> 
    2. <span data-ttu-id="d2dd9-311">For **Method**, select **POST**.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-311">For **Method**, select **POST**.</span></span> 
    3. <span data-ttu-id="d2dd9-312">For **Body**, enter `{"message":"hello world"}`.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-312">For **Body**, enter `{"message":"hello world"}`.</span></span> 
   
        ![First Web activity - settings tab](./media/how-to-schedule-azure-ssis-integration-runtime/first-web-activity-settnigs-tab.png)

4. <span data-ttu-id="d2dd9-314">Drag and drop the Execute SSIS Package activity or the Stored Procedure activity from the **General** section of the **Activities** toolbox.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-314">Drag and drop the Execute SSIS Package activity or the Stored Procedure activity from the **General** section of the **Activities** toolbox.</span></span> <span data-ttu-id="d2dd9-315">Set the name of the activity to **RunSSISPackage**.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-315">Set the name of the activity to **RunSSISPackage**.</span></span> 

5. <span data-ttu-id="d2dd9-316">If you select the Execute SSIS Package activity, follow the instructions in [Run an SSIS package using the SSIS activity in Azure Data Factory](how-to-invoke-ssis-package-ssis-activity.md) to complete the activity creation.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-316">If you select the Execute SSIS Package activity, follow the instructions in [Run an SSIS package using the SSIS activity in Azure Data Factory](how-to-invoke-ssis-package-ssis-activity.md) to complete the activity creation.</span></span>  <span data-ttu-id="d2dd9-317">Make sure that you specify a sufficient number of retry attempts that are frequent enough to wait for the availability of the Azure-SSIS IR, since it takes up to 30 minutes to start.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-317">Make sure that you specify a sufficient number of retry attempts that are frequent enough to wait for the availability of the Azure-SSIS IR, since it takes up to 30 minutes to start.</span></span> 

    ![Retry settings](media/how-to-schedule-azure-ssis-integration-runtime/retry-settings.png)

6. <span data-ttu-id="d2dd9-319">If you select the Stored Procedure activity, follow the instructions in [Invoke an SSIS package using stored procedure activity in Azure Data Factory](how-to-invoke-ssis-package-stored-procedure-activity.md) to complete the activity creation.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-319">If you select the Stored Procedure activity, follow the instructions in [Invoke an SSIS package using stored procedure activity in Azure Data Factory](how-to-invoke-ssis-package-stored-procedure-activity.md) to complete the activity creation.</span></span> <span data-ttu-id="d2dd9-320">Make sure that you insert a Transact-SQL script that waits for the availability of the Azure-SSIS IR, since it takes up to 30 minutes to start.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-320">Make sure that you insert a Transact-SQL script that waits for the availability of the Azure-SSIS IR, since it takes up to 30 minutes to start.</span></span>
    ```sql
    DECLARE @return_value int, @exe_id bigint, @err_msg nvarchar(150)

    -- Wait until Azure-SSIS IR is started
    WHILE NOT EXISTS (SELECT * FROM [SSISDB].[catalog].[worker_agents] WHERE IsEnabled = 1 AND LastOnlineTime > DATEADD(MINUTE, -10, SYSDATETIMEOFFSET()))
    BEGIN
        WAITFOR DELAY '00:00:01';
    END

    EXEC @return_value = [SSISDB].[catalog].[create_execution] @folder_name=N'YourFolder',
        @project_name=N'YourProject', @package_name=N'YourPackage',
        @use32bitruntime=0, @runincluster=1, @useanyworker=1,
        @execution_id=@exe_id OUTPUT 

    EXEC [SSISDB].[catalog].[set_execution_parameter_value] @exe_id, @object_type=50, @parameter_name=N'SYNCHRONIZED', @parameter_value=1

    EXEC [SSISDB].[catalog].[start_execution] @execution_id = @exe_id, @retry_count = 0

    -- Raise an error for unsuccessful package execution, check package execution status = created (1)/running (2)/canceled (3)/
    -- failed (4)/pending (5)/ended unexpectedly (6)/succeeded (7)/stopping (8)/completed (9) 
    IF (SELECT [status] FROM [SSISDB].[catalog].[executions] WHERE execution_id = @exe_id) <> 7 
    BEGIN
        SET @err_msg=N'Your package execution did not succeed for execution ID: '+ CAST(@execution_id as nvarchar(20))
        RAISERROR(@err_msg, 15, 1)
    END
    ```

7. <span data-ttu-id="d2dd9-321">Connect the **Web** activity to the **Execute SSIS Package** or the **Stored Procedure** activity.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-321">Connect the **Web** activity to the **Execute SSIS Package** or the **Stored Procedure** activity.</span></span> 

    ![Connect Web and Stored Procedure activities](./media/how-to-schedule-azure-ssis-integration-runtime/connect-web-sproc.png)

8. <span data-ttu-id="d2dd9-323">Drag and drop another **Web** activity to the right of the **Execute SSIS Package** activity or the **Stored Procedure** activity.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-323">Drag and drop another **Web** activity to the right of the **Execute SSIS Package** activity or the **Stored Procedure** activity.</span></span> <span data-ttu-id="d2dd9-324">Set the name of the activity to **StopIR**.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-324">Set the name of the activity to **StopIR**.</span></span> 
9. <span data-ttu-id="d2dd9-325">Switch to the **Settings** tab in the **Properties** window, and do the following actions:</span><span class="sxs-lookup"><span data-stu-id="d2dd9-325">Switch to the **Settings** tab in the **Properties** window, and do the following actions:</span></span> 

    1. <span data-ttu-id="d2dd9-326">For **URL**, paste the URL for the webhook that stops the Azure SSIS IR.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-326">For **URL**, paste the URL for the webhook that stops the Azure SSIS IR.</span></span> 
    2. <span data-ttu-id="d2dd9-327">For **Method**, select **POST**.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-327">For **Method**, select **POST**.</span></span> 
    3. <span data-ttu-id="d2dd9-328">For **Body**, enter `{"message":"hello world"}`.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-328">For **Body**, enter `{"message":"hello world"}`.</span></span>  
10. <span data-ttu-id="d2dd9-329">Connect the **Execute SSIS Package** activity or the **Stored Procedure** activity to the last **Web** activity.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-329">Connect the **Execute SSIS Package** activity or the **Stored Procedure** activity to the last **Web** activity.</span></span>

    ![Full pipeline](./media/how-to-schedule-azure-ssis-integration-runtime/full-pipeline.png)
11. <span data-ttu-id="d2dd9-331">Validate the pipeline settings by clicking **Validate** on the toolbar.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-331">Validate the pipeline settings by clicking **Validate** on the toolbar.</span></span> <span data-ttu-id="d2dd9-332">Close the **Pipeline Validation Report** by clicking **>>** button.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-332">Close the **Pipeline Validation Report** by clicking **>>** button.</span></span> 

    ![Validate pipeline](./media/how-to-schedule-azure-ssis-integration-runtime/validate-pipeline.png)

### <a name="test-run-the-pipeline"></a><span data-ttu-id="d2dd9-334">Test run the pipeline</span><span class="sxs-lookup"><span data-stu-id="d2dd9-334">Test run the pipeline</span></span>

1. <span data-ttu-id="d2dd9-335">Select **Test Run** on the toolbar for the pipeline.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-335">Select **Test Run** on the toolbar for the pipeline.</span></span> <span data-ttu-id="d2dd9-336">You see the output in the **Output** window in the bottom pane.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-336">You see the output in the **Output** window in the bottom pane.</span></span> 

    ![Test Run](./media/how-to-schedule-azure-ssis-integration-runtime/test-run-output.png)
2. <span data-ttu-id="d2dd9-338">In the **Runbook** page of your Azure Automation account, you can verify that the jobs ran to start and stop the Azure SSIS IR.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-338">In the **Runbook** page of your Azure Automation account, you can verify that the jobs ran to start and stop the Azure SSIS IR.</span></span> 

    ![Runbook jobs](./media/how-to-schedule-azure-ssis-integration-runtime/runbook-jobs.png)
3. <span data-ttu-id="d2dd9-340">Launch SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-340">Launch SQL Server Management Studio.</span></span> <span data-ttu-id="d2dd9-341">In the **Connect to Server** window, do the following actions:</span><span class="sxs-lookup"><span data-stu-id="d2dd9-341">In the **Connect to Server** window, do the following actions:</span></span> 

    1. <span data-ttu-id="d2dd9-342">For **Server name**, specify **&lt;your Azure SQL database&gt;.database.windows.net**.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-342">For **Server name**, specify **&lt;your Azure SQL database&gt;.database.windows.net**.</span></span>
    2. <span data-ttu-id="d2dd9-343">Select **Options >>**.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-343">Select **Options >>**.</span></span>
    3. <span data-ttu-id="d2dd9-344">For **Connect to database**, select **SSISDB**.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-344">For **Connect to database**, select **SSISDB**.</span></span>
    4. <span data-ttu-id="d2dd9-345">Select **Connect**.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-345">Select **Connect**.</span></span> 
    5. <span data-ttu-id="d2dd9-346">Expand **Integration Services Catalogs** -> **SSISDB** -> Your folder -> **Projects** -> Your SSIS project -> **Packages**.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-346">Expand **Integration Services Catalogs** -> **SSISDB** -> Your folder -> **Projects** -> Your SSIS project -> **Packages**.</span></span> 
    6. <span data-ttu-id="d2dd9-347">Right-click your SSIS package, and select **Reports** -> **Standard Reports** -> **All Executions**.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-347">Right-click your SSIS package, and select **Reports** -> **Standard Reports** -> **All Executions**.</span></span> 
    7. <span data-ttu-id="d2dd9-348">Verify that the SSIS package ran.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-348">Verify that the SSIS package ran.</span></span> 

        ![Verify SSIS package run](./media/how-to-schedule-azure-ssis-integration-runtime/verfiy-ssis-package-run.png)

### <a name="schedule-the-pipeline"></a><span data-ttu-id="d2dd9-350">Schedule the pipeline</span><span class="sxs-lookup"><span data-stu-id="d2dd9-350">Schedule the pipeline</span></span> 
<span data-ttu-id="d2dd9-351">Now that the pipeline works as you expected, you can create a trigger to run this pipeline at a specified cadence.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-351">Now that the pipeline works as you expected, you can create a trigger to run this pipeline at a specified cadence.</span></span> <span data-ttu-id="d2dd9-352">For details about associating a schedule trigger with a pipeline, see [Trigger the pipeline on a schedule](quickstart-create-data-factory-portal.md#trigger-the-pipeline-on-a-schedule).</span><span class="sxs-lookup"><span data-stu-id="d2dd9-352">For details about associating a schedule trigger with a pipeline, see [Trigger the pipeline on a schedule](quickstart-create-data-factory-portal.md#trigger-the-pipeline-on-a-schedule).</span></span>

1. <span data-ttu-id="d2dd9-353">On the toolbar for the pipeline, select **Trigger**, and select **New/Edit**.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-353">On the toolbar for the pipeline, select **Trigger**, and select **New/Edit**.</span></span> 

    ![Trigger -> New/Edit](./media/how-to-schedule-azure-ssis-integration-runtime/trigger-new-menu.png)
2. <span data-ttu-id="d2dd9-355">In the **Add Triggers** window, select **+ New**.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-355">In the **Add Triggers** window, select **+ New**.</span></span>

    ![Add Triggers - New](./media/how-to-schedule-azure-ssis-integration-runtime/add-triggers-new.png)
3. <span data-ttu-id="d2dd9-357">In the **New Trigger**, do the following actions:</span><span class="sxs-lookup"><span data-stu-id="d2dd9-357">In the **New Trigger**, do the following actions:</span></span> 

    1. <span data-ttu-id="d2dd9-358">For **Name**, specify a name for the trigger.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-358">For **Name**, specify a name for the trigger.</span></span> <span data-ttu-id="d2dd9-359">In the following example, **Run daily** is the name of the trigger.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-359">In the following example, **Run daily** is the name of the trigger.</span></span> 
    2. <span data-ttu-id="d2dd9-360">For **Type**, select **Schedule**.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-360">For **Type**, select **Schedule**.</span></span> 
    3. <span data-ttu-id="d2dd9-361">For **Start Date**, select a start date and time.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-361">For **Start Date**, select a start date and time.</span></span> 
    4. <span data-ttu-id="d2dd9-362">For **Recurrence**, specify the cadence for the trigger.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-362">For **Recurrence**, specify the cadence for the trigger.</span></span> <span data-ttu-id="d2dd9-363">In the following example, it's daily once.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-363">In the following example, it's daily once.</span></span> 
    5. <span data-ttu-id="d2dd9-364">For **End**, you can specify the date and time by selecting the **On Date** option.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-364">For **End**, you can specify the date and time by selecting the **On Date** option.</span></span> 
    6. <span data-ttu-id="d2dd9-365">Select **Activated**.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-365">Select **Activated**.</span></span> <span data-ttu-id="d2dd9-366">The trigger is activated immediately after you publish the solution to Data Factory.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-366">The trigger is activated immediately after you publish the solution to Data Factory.</span></span> 
    7. <span data-ttu-id="d2dd9-367">Select **Next**.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-367">Select **Next**.</span></span>

        ![Trigger -> New/Edit](./media/how-to-schedule-azure-ssis-integration-runtime/new-trigger-window.png)
4. <span data-ttu-id="d2dd9-369">In the **Trigger Run Parameters** page, review the warning, and select **Finish**.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-369">In the **Trigger Run Parameters** page, review the warning, and select **Finish**.</span></span> 
5. <span data-ttu-id="d2dd9-370">Publish the solution to Data Factory by selecting **Publish All** in the left pane.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-370">Publish the solution to Data Factory by selecting **Publish All** in the left pane.</span></span> 

    ![Publish All](./media/how-to-schedule-azure-ssis-integration-runtime/publish-all.png)

### <a name="monitor-the-pipeline-and-trigger-in-the-azure-portal"></a><span data-ttu-id="d2dd9-372">Monitor the pipeline and trigger in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="d2dd9-372">Monitor the pipeline and trigger in the Azure portal</span></span>

1. <span data-ttu-id="d2dd9-373">To monitor trigger runs and pipeline runs, use the **Monitor** tab on the left.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-373">To monitor trigger runs and pipeline runs, use the **Monitor** tab on the left.</span></span> <span data-ttu-id="d2dd9-374">For detailed steps, see [Monitor the pipeline](quickstart-create-data-factory-portal.md#monitor-the-pipeline).</span><span class="sxs-lookup"><span data-stu-id="d2dd9-374">For detailed steps, see [Monitor the pipeline](quickstart-create-data-factory-portal.md#monitor-the-pipeline).</span></span>

    ![Pipeline runs](./media/how-to-schedule-azure-ssis-integration-runtime/pipeline-runs.png)
2. <span data-ttu-id="d2dd9-376">To view the activity runs associated with a pipeline run, select the first link (**View Activity Runs**) in the **Actions** column.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-376">To view the activity runs associated with a pipeline run, select the first link (**View Activity Runs**) in the **Actions** column.</span></span> <span data-ttu-id="d2dd9-377">You see the three activity runs associated with each activity in the pipeline (first Web activity, Stored Procedure activity, and the second Web activity).</span><span class="sxs-lookup"><span data-stu-id="d2dd9-377">You see the three activity runs associated with each activity in the pipeline (first Web activity, Stored Procedure activity, and the second Web activity).</span></span> <span data-ttu-id="d2dd9-378">To switch back to view the pipeline runs, select **Pipelines** link at the top.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-378">To switch back to view the pipeline runs, select **Pipelines** link at the top.</span></span>

    ![Activity runs](./media/how-to-schedule-azure-ssis-integration-runtime/activity-runs.png)
3. <span data-ttu-id="d2dd9-380">You can also view trigger runs by selecting **Trigger runs** from the drop-down list that's next to the **Pipeline Runs** at the top.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-380">You can also view trigger runs by selecting **Trigger runs** from the drop-down list that's next to the **Pipeline Runs** at the top.</span></span> 

    ![Trigger runs](./media/how-to-schedule-azure-ssis-integration-runtime/trigger-runs.png)

### <a name="monitor-the-pipeline-and-trigger-with-powershell"></a><span data-ttu-id="d2dd9-382">Monitor the pipeline and trigger with PowerShell</span><span class="sxs-lookup"><span data-stu-id="d2dd9-382">Monitor the pipeline and trigger with PowerShell</span></span>

<span data-ttu-id="d2dd9-383">Use scripts like the following examples to monitor the pipeline and the trigger.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-383">Use scripts like the following examples to monitor the pipeline and the trigger.</span></span>

1. <span data-ttu-id="d2dd9-384">Get the status of a pipeline run.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-384">Get the status of a pipeline run.</span></span>

  ```powershell
  Get-AzureRmDataFactoryV2PipelineRun -ResourceGroupName $ResourceGroupName -DataFactoryName $DataFactoryName -PipelineRunId $myPipelineRun
  ```

2. <span data-ttu-id="d2dd9-385">Get info about the trigger.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-385">Get info about the trigger.</span></span>

  ```powershell
  Get-AzureRmDataFactoryV2Trigger -ResourceGroupName $ResourceGroupName -DataFactoryName $DataFactoryName -Name  "myTrigger"
  ```

3. <span data-ttu-id="d2dd9-386">Get the status of a trigger run.</span><span class="sxs-lookup"><span data-stu-id="d2dd9-386">Get the status of a trigger run.</span></span>

  ```powershell
  Get-AzureRmDataFactoryV2TriggerRun -ResourceGroupName $ResourceGroupName -DataFactoryName $DataFactoryName -TriggerName "myTrigger" -TriggerRunStartedAfter "2018-07-15" -TriggerRunStartedBefore "2018-07-16"
  ```

## <a name="next-steps"></a><span data-ttu-id="d2dd9-387">Next steps</span><span class="sxs-lookup"><span data-stu-id="d2dd9-387">Next steps</span></span>
<span data-ttu-id="d2dd9-388">See the following blog post:</span><span class="sxs-lookup"><span data-stu-id="d2dd9-388">See the following blog post:</span></span>
-   [<span data-ttu-id="d2dd9-389">Modernize and extend your ETL/ELT workflows with SSIS activities in ADF pipelines</span><span class="sxs-lookup"><span data-stu-id="d2dd9-389">Modernize and extend your ETL/ELT workflows with SSIS activities in ADF pipelines</span></span>](https://blogs.msdn.microsoft.com/ssis/2018/05/23/modernize-and-extend-your-etlelt-workflows-with-ssis-activities-in-adf-pipelines/)

<span data-ttu-id="d2dd9-390">See the following articles from SSIS documentation:</span><span class="sxs-lookup"><span data-stu-id="d2dd9-390">See the following articles from SSIS documentation:</span></span> 

- [<span data-ttu-id="d2dd9-391">Deploy, run, and monitor an SSIS package on Azure</span><span class="sxs-lookup"><span data-stu-id="d2dd9-391">Deploy, run, and monitor an SSIS package on Azure</span></span>](/sql/integration-services/lift-shift/ssis-azure-deploy-run-monitor-tutorial)   
- [<span data-ttu-id="d2dd9-392">Connect to SSIS catalog on Azure</span><span class="sxs-lookup"><span data-stu-id="d2dd9-392">Connect to SSIS catalog on Azure</span></span>](/sql/integration-services/lift-shift/ssis-azure-connect-to-catalog-database)
- [<span data-ttu-id="d2dd9-393">Schedule package execution on Azure</span><span class="sxs-lookup"><span data-stu-id="d2dd9-393">Schedule package execution on Azure</span></span>](/sql/integration-services/lift-shift/ssis-azure-schedule-packages)
- [<span data-ttu-id="d2dd9-394">Connect to on-premises data sources with Windows authentication</span><span class="sxs-lookup"><span data-stu-id="d2dd9-394">Connect to on-premises data sources with Windows authentication</span></span>](/sql/integration-services/lift-shift/ssis-azure-connect-with-windows-auth)
