---
title: Editing textual runbooks in Azure Automation
description: This article provides different procedures for working with PowerShell and PowerShell Workflow runbooks in Azure Automation using the textual editor.
services: automation
ms.service: automation
ms.component: process-automation
author: georgewallace
ms.author: gwallace
ms.date: 08/01/2018
ms.topic: conceptual
manager: carmonm
ms.openlocfilehash: b17fc82d6e9cbda6ffa94ac2ee5c97835b089a7e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44825916"
---
# <a name="editing-textual-runbooks-in-azure-automation"></a><span data-ttu-id="7b52c-103">Editing textual runbooks in Azure Automation</span><span class="sxs-lookup"><span data-stu-id="7b52c-103">Editing textual runbooks in Azure Automation</span></span>

<span data-ttu-id="7b52c-104">The textual editor in Azure Automation can be used to edit [PowerShell runbooks](automation-runbook-types.md#powershell-runbooks) and [PowerShell Workflow runbooks](automation-runbook-types.md#powershell-workflow-runbooks).</span><span class="sxs-lookup"><span data-stu-id="7b52c-104">The textual editor in Azure Automation can be used to edit [PowerShell runbooks](automation-runbook-types.md#powershell-runbooks) and [PowerShell Workflow runbooks](automation-runbook-types.md#powershell-workflow-runbooks).</span></span> <span data-ttu-id="7b52c-105">This has the typical features of other code editors such as intellisense and color coding  with additional special features to assist you in accessing resources common to runbooks.</span><span class="sxs-lookup"><span data-stu-id="7b52c-105">This has the typical features of other code editors such as intellisense and color coding  with additional special features to assist you in accessing resources common to runbooks.</span></span> <span data-ttu-id="7b52c-106">This article provides detailed steps for performing different functions with this editor.</span><span class="sxs-lookup"><span data-stu-id="7b52c-106">This article provides detailed steps for performing different functions with this editor.</span></span>

<span data-ttu-id="7b52c-107">The textual editor includes a feature to insert code for cmdlets, assets, and child runbooks into a runbook.</span><span class="sxs-lookup"><span data-stu-id="7b52c-107">The textual editor includes a feature to insert code for cmdlets, assets, and child runbooks into a runbook.</span></span> <span data-ttu-id="7b52c-108">Rather than typing in the code yourself, you can select from a list of available resources and have the appropriate code inserted into the runbook.</span><span class="sxs-lookup"><span data-stu-id="7b52c-108">Rather than typing in the code yourself, you can select from a list of available resources and have the appropriate code inserted into the runbook.</span></span>

<span data-ttu-id="7b52c-109">Each runbook in Azure Automation has two versions, Draft and Published.</span><span class="sxs-lookup"><span data-stu-id="7b52c-109">Each runbook in Azure Automation has two versions, Draft and Published.</span></span> <span data-ttu-id="7b52c-110">You edit the Draft version of the runbook and then publish it so it can be executed.</span><span class="sxs-lookup"><span data-stu-id="7b52c-110">You edit the Draft version of the runbook and then publish it so it can be executed.</span></span> <span data-ttu-id="7b52c-111">The Published version cannot be edited.</span><span class="sxs-lookup"><span data-stu-id="7b52c-111">The Published version cannot be edited.</span></span> <span data-ttu-id="7b52c-112">See [Publishing a runbook](automation-creating-importing-runbook.md#publishing-a-runbook) for more information.</span><span class="sxs-lookup"><span data-stu-id="7b52c-112">See [Publishing a runbook](automation-creating-importing-runbook.md#publishing-a-runbook) for more information.</span></span>

<span data-ttu-id="7b52c-113">To work with [Graphical Runbooks](automation-runbook-types.md#graphical-runbooks), see [Graphical authoring in Azure Automation](automation-graphical-authoring-intro.md).</span><span class="sxs-lookup"><span data-stu-id="7b52c-113">To work with [Graphical Runbooks](automation-runbook-types.md#graphical-runbooks), see [Graphical authoring in Azure Automation](automation-graphical-authoring-intro.md).</span></span>

## <a name="to-edit-a-runbook-with-the-azure-portal"></a><span data-ttu-id="7b52c-114">To edit a runbook with the Azure portal</span><span class="sxs-lookup"><span data-stu-id="7b52c-114">To edit a runbook with the Azure portal</span></span>

<span data-ttu-id="7b52c-115">Use the following procedure to open a runbook for editing in the textual editor.</span><span class="sxs-lookup"><span data-stu-id="7b52c-115">Use the following procedure to open a runbook for editing in the textual editor.</span></span>

1. <span data-ttu-id="7b52c-116">In the Azure portal, select your automation account.</span><span class="sxs-lookup"><span data-stu-id="7b52c-116">In the Azure portal, select your automation account.</span></span>
2. <span data-ttu-id="7b52c-117">Under **PROCESS AUTOMATION**, select **Runbooks** to open the list of runbooks.</span><span class="sxs-lookup"><span data-stu-id="7b52c-117">Under **PROCESS AUTOMATION**, select **Runbooks** to open the list of runbooks.</span></span>
3. <span data-ttu-id="7b52c-118">Select the runbook you want to edit and then click the **Edit** button.</span><span class="sxs-lookup"><span data-stu-id="7b52c-118">Select the runbook you want to edit and then click the **Edit** button.</span></span>
4. <span data-ttu-id="7b52c-119">Perform the required editing.</span><span class="sxs-lookup"><span data-stu-id="7b52c-119">Perform the required editing.</span></span>
5. <span data-ttu-id="7b52c-120">Click **Save** when your edits are complete.</span><span class="sxs-lookup"><span data-stu-id="7b52c-120">Click **Save** when your edits are complete.</span></span>
6. <span data-ttu-id="7b52c-121">Click **Publish** if you want the latest draft version of the runbook to be published.</span><span class="sxs-lookup"><span data-stu-id="7b52c-121">Click **Publish** if you want the latest draft version of the runbook to be published.</span></span>

### <a name="to-insert-a-cmdlet-into-a-runbook"></a><span data-ttu-id="7b52c-122">To insert a cmdlet into a runbook</span><span class="sxs-lookup"><span data-stu-id="7b52c-122">To insert a cmdlet into a runbook</span></span>

1. <span data-ttu-id="7b52c-123">In the Canvas of the textual editor, position the cursor where you want to place the cmdlet.</span><span class="sxs-lookup"><span data-stu-id="7b52c-123">In the Canvas of the textual editor, position the cursor where you want to place the cmdlet.</span></span>
2. <span data-ttu-id="7b52c-124">Expand the **Cmdlets** node in the Library control.</span><span class="sxs-lookup"><span data-stu-id="7b52c-124">Expand the **Cmdlets** node in the Library control.</span></span>
3. <span data-ttu-id="7b52c-125">Expand the module containing the cmdlet you want to use.</span><span class="sxs-lookup"><span data-stu-id="7b52c-125">Expand the module containing the cmdlet you want to use.</span></span>
4. <span data-ttu-id="7b52c-126">Right click the cmdlet to insert and select **Add to canvas**.</span><span class="sxs-lookup"><span data-stu-id="7b52c-126">Right click the cmdlet to insert and select **Add to canvas**.</span></span> <span data-ttu-id="7b52c-127">If the cmdlet has more than one parameter set, then the default set will be added.</span><span class="sxs-lookup"><span data-stu-id="7b52c-127">If the cmdlet has more than one parameter set, then the default set will be added.</span></span> <span data-ttu-id="7b52c-128">You can also expand the cmdlet to select a different parameter set.</span><span class="sxs-lookup"><span data-stu-id="7b52c-128">You can also expand the cmdlet to select a different parameter set.</span></span>
5. <span data-ttu-id="7b52c-129">The code for the cmdlet is inserted with its entire list of parameters.</span><span class="sxs-lookup"><span data-stu-id="7b52c-129">The code for the cmdlet is inserted with its entire list of parameters.</span></span>
6. <span data-ttu-id="7b52c-130">Provide an appropriate value in place of the data type surrounded by braces <> for any required parameters.</span><span class="sxs-lookup"><span data-stu-id="7b52c-130">Provide an appropriate value in place of the data type surrounded by braces <> for any required parameters.</span></span> <span data-ttu-id="7b52c-131">Remove any parameters you don't need.</span><span class="sxs-lookup"><span data-stu-id="7b52c-131">Remove any parameters you don't need.</span></span>

### <a name="to-insert-code-for-a-child-runbook-into-a-runbook"></a><span data-ttu-id="7b52c-132">To insert code for a child runbook into a runbook</span><span class="sxs-lookup"><span data-stu-id="7b52c-132">To insert code for a child runbook into a runbook</span></span>

1. <span data-ttu-id="7b52c-133">In the Canvas of the textual editor, position the cursor where you want to place the code for the [child runbook](automation-child-runbooks.md).</span><span class="sxs-lookup"><span data-stu-id="7b52c-133">In the Canvas of the textual editor, position the cursor where you want to place the code for the [child runbook](automation-child-runbooks.md).</span></span>
2. <span data-ttu-id="7b52c-134">Expand the **Runbooks** node in the Library control.</span><span class="sxs-lookup"><span data-stu-id="7b52c-134">Expand the **Runbooks** node in the Library control.</span></span>
3. <span data-ttu-id="7b52c-135">Right click the runbook to insert and select **Add to canvas**.</span><span class="sxs-lookup"><span data-stu-id="7b52c-135">Right click the runbook to insert and select **Add to canvas**.</span></span>
4. <span data-ttu-id="7b52c-136">The code for the child runbook is inserted with any placeholders for any runbook parameters.</span><span class="sxs-lookup"><span data-stu-id="7b52c-136">The code for the child runbook is inserted with any placeholders for any runbook parameters.</span></span>
5. <span data-ttu-id="7b52c-137">Replace the placeholders with appropriate values for each parameter.</span><span class="sxs-lookup"><span data-stu-id="7b52c-137">Replace the placeholders with appropriate values for each parameter.</span></span>

### <a name="to-insert-an-asset-into-a-runbook"></a><span data-ttu-id="7b52c-138">To insert an asset into a runbook</span><span class="sxs-lookup"><span data-stu-id="7b52c-138">To insert an asset into a runbook</span></span>

1. <span data-ttu-id="7b52c-139">In the Canvas of the textual editor, position the cursor where you want to place the code for the child runbook.</span><span class="sxs-lookup"><span data-stu-id="7b52c-139">In the Canvas of the textual editor, position the cursor where you want to place the code for the child runbook.</span></span>
2. <span data-ttu-id="7b52c-140">Expand the **Assets** node in the Library control.</span><span class="sxs-lookup"><span data-stu-id="7b52c-140">Expand the **Assets** node in the Library control.</span></span>
3. <span data-ttu-id="7b52c-141">Expand the node for the type of asset you want.</span><span class="sxs-lookup"><span data-stu-id="7b52c-141">Expand the node for the type of asset you want.</span></span>
4. <span data-ttu-id="7b52c-142">Right click the asset to insert and select **Add to canvas**.</span><span class="sxs-lookup"><span data-stu-id="7b52c-142">Right click the asset to insert and select **Add to canvas**.</span></span> <span data-ttu-id="7b52c-143">For [variable assets](automation-variables.md), select either **Add "Get Variable" to canvas** or **Add "Set Variable" to canvas** depending on whether you want to get or set the variable.</span><span class="sxs-lookup"><span data-stu-id="7b52c-143">For [variable assets](automation-variables.md), select either **Add "Get Variable" to canvas** or **Add "Set Variable" to canvas** depending on whether you want to get or set the variable.</span></span>
5. <span data-ttu-id="7b52c-144">The code for the asset is inserted into the runbook.</span><span class="sxs-lookup"><span data-stu-id="7b52c-144">The code for the asset is inserted into the runbook.</span></span>

## <a name="to-edit-an-azure-automation-runbook-using-windows-powershell"></a><span data-ttu-id="7b52c-145">To edit an Azure Automation runbook using Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="7b52c-145">To edit an Azure Automation runbook using Windows PowerShell</span></span>

<span data-ttu-id="7b52c-146">To edit a runbook with Windows PowerShell, you use the editor of your choice and save it to a .ps1 file.</span><span class="sxs-lookup"><span data-stu-id="7b52c-146">To edit a runbook with Windows PowerShell, you use the editor of your choice and save it to a .ps1 file.</span></span> <span data-ttu-id="7b52c-147">You can use the [Export-AzureRmAutomationRunbook](/powershell/module/AzureRM.Automation/Export-AzureRmAutomationRunbook) cmdlet to retrieve the contents of the runbook and then [Import-AzureRmAutomationRunbook](/powershell/module/AzureRM.Automation/import-azurermautomationrunbook) cmdlet to replace the existing draft runbook with the modified one.</span><span class="sxs-lookup"><span data-stu-id="7b52c-147">You can use the [Export-AzureRmAutomationRunbook](/powershell/module/AzureRM.Automation/Export-AzureRmAutomationRunbook) cmdlet to retrieve the contents of the runbook and then [Import-AzureRmAutomationRunbook](/powershell/module/AzureRM.Automation/import-azurermautomationrunbook) cmdlet to replace the existing draft runbook with the modified one.</span></span>

### <a name="to-retrieve-the-contents-of-a-runbook-using-windows-powershell"></a><span data-ttu-id="7b52c-148">To Retrieve the Contents of a Runbook Using Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="7b52c-148">To Retrieve the Contents of a Runbook Using Windows PowerShell</span></span>

<span data-ttu-id="7b52c-149">The following sample commands show how to retrieve the script for a runbook and save it to a script file.</span><span class="sxs-lookup"><span data-stu-id="7b52c-149">The following sample commands show how to retrieve the script for a runbook and save it to a script file.</span></span> <span data-ttu-id="7b52c-150">In this example, the Draft version is retrieved.</span><span class="sxs-lookup"><span data-stu-id="7b52c-150">In this example, the Draft version is retrieved.</span></span> <span data-ttu-id="7b52c-151">It is also possible to retrieve the Published version of the runbook although this version cannot be changed.</span><span class="sxs-lookup"><span data-stu-id="7b52c-151">It is also possible to retrieve the Published version of the runbook although this version cannot be changed.</span></span>

```powershell-interactive
$resourceGroupName = "MyResourceGroup"
$automationAccountName = "MyAutomatonAccount"
$runbookName = "Hello-World"
$scriptFolder = "c:\runbooks"

Export-AzureRmAutomationRunbook -Name $runbookName -AutomationAccountName $automationAccountName -ResourceGroupName $resourceGroupName -OutputFolder $scriptFolder -Slot Draft
```

### <a name="to-change-the-contents-of-a-runbook-using-windows-powershell"></a><span data-ttu-id="7b52c-152">To Change the Contents of a Runbook Using Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="7b52c-152">To Change the Contents of a Runbook Using Windows PowerShell</span></span>

<span data-ttu-id="7b52c-153">The following sample commands show how to replace the existing contents of a runbook with the contents of a script file.</span><span class="sxs-lookup"><span data-stu-id="7b52c-153">The following sample commands show how to replace the existing contents of a runbook with the contents of a script file.</span></span> <span data-ttu-id="7b52c-154">Note that this is the same sample procedure as in [To import a runbook from a script file with Windows PowerShell](automation-creating-importing-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="7b52c-154">Note that this is the same sample procedure as in [To import a runbook from a script file with Windows PowerShell](automation-creating-importing-runbook.md).</span></span>

```powershell-interactive
$resourceGroupName = "MyResourceGroup"
$automationAccountName = "MyAutomatonAccount"
$runbookName = "Hello-World"
$scriptFolder = "c:\runbooks"

Import-AzureRmAutomationRunbook -Path "$scriptfolder\Hello-World.ps1" -Name $runbookName -Type PowerShell -AutomationAccountName $automationAccountName -ResourceGroupName $resourceGroupName -Force
Publish-AzureRmAutomationRunbook -Name $runbookName -AutomationAccountName $automationAccountName -ResourceGroupName $resourceGroupName
```

## <a name="related-articles"></a><span data-ttu-id="7b52c-155">Related articles</span><span class="sxs-lookup"><span data-stu-id="7b52c-155">Related articles</span></span>

* [<span data-ttu-id="7b52c-156">Creating or importing a runbook in Azure Automation</span><span class="sxs-lookup"><span data-stu-id="7b52c-156">Creating or importing a runbook in Azure Automation</span></span>](automation-creating-importing-runbook.md)
* [<span data-ttu-id="7b52c-157">Learning PowerShell workflow</span><span class="sxs-lookup"><span data-stu-id="7b52c-157">Learning PowerShell workflow</span></span>](automation-powershell-workflow.md)
* [<span data-ttu-id="7b52c-158">Graphical authoring in Azure Automation</span><span class="sxs-lookup"><span data-stu-id="7b52c-158">Graphical authoring in Azure Automation</span></span>](automation-graphical-authoring-intro.md)
* [<span data-ttu-id="7b52c-159">Certificates</span><span class="sxs-lookup"><span data-stu-id="7b52c-159">Certificates</span></span>](automation-certificates.md)
* [<span data-ttu-id="7b52c-160">Connections</span><span class="sxs-lookup"><span data-stu-id="7b52c-160">Connections</span></span>](automation-connections.md)
* [<span data-ttu-id="7b52c-161">Credentials</span><span class="sxs-lookup"><span data-stu-id="7b52c-161">Credentials</span></span>](automation-credentials.md)
* [<span data-ttu-id="7b52c-162">Schedules</span><span class="sxs-lookup"><span data-stu-id="7b52c-162">Schedules</span></span>](automation-schedules.md)
* [<span data-ttu-id="7b52c-163">Variables</span><span class="sxs-lookup"><span data-stu-id="7b52c-163">Variables</span></span>](automation-variables.md)
