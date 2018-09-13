---
title: Creating or importing a runbook in Azure Automation
description: This article describes how to create a new runbook in Azure Automation or import one from a file.
services: automation
ms.service: automation
ms.component: process-automation
author: georgewallace
ms.author: gwallace
ms.date: 08/06/2018
ms.topic: conceptual
manager: carmonm
ms.openlocfilehash: 2ccf9036d3701c710c6d3258f81390ed355c246c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44783853"
---
# <a name="creating-or-importing-a-runbook-in-azure-automation"></a><span data-ttu-id="adf0d-103">Creating or importing a runbook in Azure Automation</span><span class="sxs-lookup"><span data-stu-id="adf0d-103">Creating or importing a runbook in Azure Automation</span></span>

<span data-ttu-id="adf0d-104">You can add a runbook to Azure Automation by either [creating a new one](#creating-a-new-runbook) or by importing an existing runbook from a file or from the [Runbook Gallery](automation-runbook-gallery.md).</span><span class="sxs-lookup"><span data-stu-id="adf0d-104">You can add a runbook to Azure Automation by either [creating a new one](#creating-a-new-runbook) or by importing an existing runbook from a file or from the [Runbook Gallery](automation-runbook-gallery.md).</span></span> <span data-ttu-id="adf0d-105">This article provides information on creating and importing runbooks from a file.</span><span class="sxs-lookup"><span data-stu-id="adf0d-105">This article provides information on creating and importing runbooks from a file.</span></span>  <span data-ttu-id="adf0d-106">You can get all of the details on accessing community runbooks and modules in [Runbook and module galleries for Azure Automation](automation-runbook-gallery.md).</span><span class="sxs-lookup"><span data-stu-id="adf0d-106">You can get all of the details on accessing community runbooks and modules in [Runbook and module galleries for Azure Automation](automation-runbook-gallery.md).</span></span>

## <a name="creating-a-new-runbook"></a><span data-ttu-id="adf0d-107">Creating a new runbook</span><span class="sxs-lookup"><span data-stu-id="adf0d-107">Creating a new runbook</span></span>

<span data-ttu-id="adf0d-108">You can create a new runbook in Azure Automation using one of the Azure portals or Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="adf0d-108">You can create a new runbook in Azure Automation using one of the Azure portals or Windows PowerShell.</span></span> <span data-ttu-id="adf0d-109">Once the runbook has been created, you can edit it using information in [Learning PowerShell Workflow](automation-powershell-workflow.md) and [Graphical authoring in Azure Automation](automation-graphical-authoring-intro.md).</span><span class="sxs-lookup"><span data-stu-id="adf0d-109">Once the runbook has been created, you can edit it using information in [Learning PowerShell Workflow](automation-powershell-workflow.md) and [Graphical authoring in Azure Automation](automation-graphical-authoring-intro.md).</span></span>

### <a name="to-create-a-new-azure-automation-runbook-with-the-azure-portal"></a><span data-ttu-id="adf0d-110">To create a new Azure Automation runbook with the Azure portal</span><span class="sxs-lookup"><span data-stu-id="adf0d-110">To create a new Azure Automation runbook with the Azure portal</span></span>

1. <span data-ttu-id="adf0d-111">In the Azure portal, open your Automation account.</span><span class="sxs-lookup"><span data-stu-id="adf0d-111">In the Azure portal, open your Automation account.</span></span>
1. <span data-ttu-id="adf0d-112">From the Hub, select **Runbooks** to open the list of runbooks.</span><span class="sxs-lookup"><span data-stu-id="adf0d-112">From the Hub, select **Runbooks** to open the list of runbooks.</span></span>
1. <span data-ttu-id="adf0d-113">Click on the **Add a runbook** button and then **Create a new runbook**.</span><span class="sxs-lookup"><span data-stu-id="adf0d-113">Click on the **Add a runbook** button and then **Create a new runbook**.</span></span>
1. <span data-ttu-id="adf0d-114">Type a **Name** for the runbook and select its [Type](automation-runbook-types.md).</span><span class="sxs-lookup"><span data-stu-id="adf0d-114">Type a **Name** for the runbook and select its [Type](automation-runbook-types.md).</span></span> <span data-ttu-id="adf0d-115">The runbook name must start with a letter and can have letters, numbers, underscores, and dashes.</span><span class="sxs-lookup"><span data-stu-id="adf0d-115">The runbook name must start with a letter and can have letters, numbers, underscores, and dashes.</span></span>
1. <span data-ttu-id="adf0d-116">Click **Create** to create the runbook and open the editor.</span><span class="sxs-lookup"><span data-stu-id="adf0d-116">Click **Create** to create the runbook and open the editor.</span></span>

### <a name="to-create-a-new-azure-automation-runbook-with-windows-powershell"></a><span data-ttu-id="adf0d-117">To create a new Azure Automation runbook with Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="adf0d-117">To create a new Azure Automation runbook with Windows PowerShell</span></span>
<span data-ttu-id="adf0d-118">You can use the [New-AzureRmAutomationRunbook](https://docs.microsoft.com/powershell/module/azurerm.automation/new-azurermautomationrunbook) cmdlet to create an empty [PowerShell Workflow runbook](automation-runbook-types.md#powershell-workflow-runbooks).</span><span class="sxs-lookup"><span data-stu-id="adf0d-118">You can use the [New-AzureRmAutomationRunbook](https://docs.microsoft.com/powershell/module/azurerm.automation/new-azurermautomationrunbook) cmdlet to create an empty [PowerShell Workflow runbook](automation-runbook-types.md#powershell-workflow-runbooks).</span></span> <span data-ttu-id="adf0d-119">The **Type** parameter should also be included to specify one of the four runbook types.</span><span class="sxs-lookup"><span data-stu-id="adf0d-119">The **Type** parameter should also be included to specify one of the four runbook types.</span></span>

<span data-ttu-id="adf0d-120">The following sample commands show how to create a new empty runbook.</span><span class="sxs-lookup"><span data-stu-id="adf0d-120">The following sample commands show how to create a new empty runbook.</span></span>

```azurepowershell-interactive
New-AzureRmAutomationRunbook -AutomationAccountName MyAccount `
-Name NewRunbook -ResourceGroupName MyResourceGroup -Type PowerShell
```

## <a name="importing-a-runbook-from-a-file-into-azure-automation"></a><span data-ttu-id="adf0d-121">Importing a runbook from a file into Azure Automation</span><span class="sxs-lookup"><span data-stu-id="adf0d-121">Importing a runbook from a file into Azure Automation</span></span>

<span data-ttu-id="adf0d-122">You can create a new runbook in Azure Automation by importing a PowerShell script or PowerShell Workflow (.ps1 extension), an exported graphical runbook (.graphrunbook), or a Python 2 script (.py extension).</span><span class="sxs-lookup"><span data-stu-id="adf0d-122">You can create a new runbook in Azure Automation by importing a PowerShell script or PowerShell Workflow (.ps1 extension), an exported graphical runbook (.graphrunbook), or a Python 2 script (.py extension).</span></span>  <span data-ttu-id="adf0d-123">You must specify the [type of runbook](automation-runbook-types.md) that is created during import, taking into account the following considerations.</span><span class="sxs-lookup"><span data-stu-id="adf0d-123">You must specify the [type of runbook](automation-runbook-types.md) that is created during import, taking into account the following considerations.</span></span>

* <span data-ttu-id="adf0d-124">A .graphrunbook file may only be imported into a new [graphical runbook](automation-runbook-types.md#graphical-runbooks), and graphical runbooks can only be created from a .graphrunbook file.</span><span class="sxs-lookup"><span data-stu-id="adf0d-124">A .graphrunbook file may only be imported into a new [graphical runbook](automation-runbook-types.md#graphical-runbooks), and graphical runbooks can only be created from a .graphrunbook file.</span></span>
* <span data-ttu-id="adf0d-125">A .ps1 file containing a PowerShell Workflow can only be imported into a [PowerShell Workflow runbook](automation-runbook-types.md#powershell-workflow-runbooks).</span><span class="sxs-lookup"><span data-stu-id="adf0d-125">A .ps1 file containing a PowerShell Workflow can only be imported into a [PowerShell Workflow runbook](automation-runbook-types.md#powershell-workflow-runbooks).</span></span>  <span data-ttu-id="adf0d-126">If the file contains multiple PowerShell Workflows, then the import will fail.</span><span class="sxs-lookup"><span data-stu-id="adf0d-126">If the file contains multiple PowerShell Workflows, then the import will fail.</span></span> <span data-ttu-id="adf0d-127">You must save each workflow to its own file and import each separately.</span><span class="sxs-lookup"><span data-stu-id="adf0d-127">You must save each workflow to its own file and import each separately.</span></span>
* <span data-ttu-id="adf0d-128">A .ps1 file that does not contain a workflow can be imported into either a [PowerShell runbook](automation-runbook-types.md#powershell-runbooks) or a [PowerShell Workflow runbook](automation-runbook-types.md#powershell-workflow-runbooks).</span><span class="sxs-lookup"><span data-stu-id="adf0d-128">A .ps1 file that does not contain a workflow can be imported into either a [PowerShell runbook](automation-runbook-types.md#powershell-runbooks) or a [PowerShell Workflow runbook](automation-runbook-types.md#powershell-workflow-runbooks).</span></span>  <span data-ttu-id="adf0d-129">If it is imported into a PowerShell Workflow runbook, then it is converted to a workflow, and comments are included in the runbook specifying the changes that were made.</span><span class="sxs-lookup"><span data-stu-id="adf0d-129">If it is imported into a PowerShell Workflow runbook, then it is converted to a workflow, and comments are included in the runbook specifying the changes that were made.</span></span>

### <a name="to-import-a-runbook-from-a-file-with-the-azure-portal"></a><span data-ttu-id="adf0d-130">To import a runbook from a file with the Azure portal</span><span class="sxs-lookup"><span data-stu-id="adf0d-130">To import a runbook from a file with the Azure portal</span></span>

<span data-ttu-id="adf0d-131">You can use the following procedure to import a script file into Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="adf0d-131">You can use the following procedure to import a script file into Azure Automation.</span></span>  

> [!NOTE]
> <span data-ttu-id="adf0d-132">Note that you can only import a .ps1 file into a PowerShell Workflow runbook using the portal.</span><span class="sxs-lookup"><span data-stu-id="adf0d-132">Note that you can only import a .ps1 file into a PowerShell Workflow runbook using the portal.</span></span>

1. <span data-ttu-id="adf0d-133">In the Azure portal, open your Automation account.</span><span class="sxs-lookup"><span data-stu-id="adf0d-133">In the Azure portal, open your Automation account.</span></span>
2. <span data-ttu-id="adf0d-134">From the Hub, select **Runbooks** to open the list of runbooks.</span><span class="sxs-lookup"><span data-stu-id="adf0d-134">From the Hub, select **Runbooks** to open the list of runbooks.</span></span>
3. <span data-ttu-id="adf0d-135">Click on the **Add a runbook** button and then **Import**.</span><span class="sxs-lookup"><span data-stu-id="adf0d-135">Click on the **Add a runbook** button and then **Import**.</span></span>
4. <span data-ttu-id="adf0d-136">Click **Runbook file** to select the file to import</span><span class="sxs-lookup"><span data-stu-id="adf0d-136">Click **Runbook file** to select the file to import</span></span>
5. <span data-ttu-id="adf0d-137">If the **Name** field is enabled, then you have the option to change it.</span><span class="sxs-lookup"><span data-stu-id="adf0d-137">If the **Name** field is enabled, then you have the option to change it.</span></span>  <span data-ttu-id="adf0d-138">The runbook name must start with a letter and can have letters, numbers, underscores, and dashes.</span><span class="sxs-lookup"><span data-stu-id="adf0d-138">The runbook name must start with a letter and can have letters, numbers, underscores, and dashes.</span></span>
6. <span data-ttu-id="adf0d-139">The [runbook type](automation-runbook-types.md) is automatically selected, but you can change the type after taking the applicable restrictions into account.</span><span class="sxs-lookup"><span data-stu-id="adf0d-139">The [runbook type](automation-runbook-types.md) is automatically selected, but you can change the type after taking the applicable restrictions into account.</span></span> 
7. <span data-ttu-id="adf0d-140">The new runbook appears in the list of runbooks for the Automation Account.</span><span class="sxs-lookup"><span data-stu-id="adf0d-140">The new runbook appears in the list of runbooks for the Automation Account.</span></span>
8. <span data-ttu-id="adf0d-141">You must [publish the runbook](#publishing-a-runbook) before you can run it.</span><span class="sxs-lookup"><span data-stu-id="adf0d-141">You must [publish the runbook](#publishing-a-runbook) before you can run it.</span></span>

> [!NOTE]
> <span data-ttu-id="adf0d-142">After you import a graphical runbook or a graphical PowerShell workflow runbook, you have the option to convert to the other type if wanted.</span><span class="sxs-lookup"><span data-stu-id="adf0d-142">After you import a graphical runbook or a graphical PowerShell workflow runbook, you have the option to convert to the other type if wanted.</span></span> <span data-ttu-id="adf0d-143">You can’t convert to a textual runbook.</span><span class="sxs-lookup"><span data-stu-id="adf0d-143">You can’t convert to a textual runbook.</span></span>
>  
> 

### <a name="to-import-a-runbook-from-a-script-file-with-windows-powershell"></a><span data-ttu-id="adf0d-144">To import a runbook from a script file with Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="adf0d-144">To import a runbook from a script file with Windows PowerShell</span></span>
<span data-ttu-id="adf0d-145">You can use the [Import-AzureRMAutomationRunbook](https://docs.microsoft.com/powershell/module/azurerm.automation/import-azurermautomationrunbook) cmdlet to import a script file as a draft PowerShell Workflow runbook.</span><span class="sxs-lookup"><span data-stu-id="adf0d-145">You can use the [Import-AzureRMAutomationRunbook](https://docs.microsoft.com/powershell/module/azurerm.automation/import-azurermautomationrunbook) cmdlet to import a script file as a draft PowerShell Workflow runbook.</span></span> <span data-ttu-id="adf0d-146">If the runbook already exists, the import fails unless you use the *-Force* parameter.</span><span class="sxs-lookup"><span data-stu-id="adf0d-146">If the runbook already exists, the import fails unless you use the *-Force* parameter.</span></span> 

<span data-ttu-id="adf0d-147">The following sample commands show how to import a script file into a runbook.</span><span class="sxs-lookup"><span data-stu-id="adf0d-147">The following sample commands show how to import a script file into a runbook.</span></span>

```azurepowershell-interactive
$automationAccountName =  "AutomationAccount"
$runbookName = "Sample_TestRunbook"
$scriptPath = "C:\Runbooks\Sample_TestRunbook.ps1"
$RGName = "ResourceGroup"

Import-AzureRMAutomationRunbook -Name $runbookName -Path $scriptPath `
-ResourceGroupName $RGName -AutomationAccountName $automationAccountName `
-Type PowerShellWorkflow
```

## <a name="publishing-a-runbook"></a><span data-ttu-id="adf0d-148">Publishing a runbook</span><span class="sxs-lookup"><span data-stu-id="adf0d-148">Publishing a runbook</span></span>

<span data-ttu-id="adf0d-149">When you create or import a new runbook, you must publish it before you can run it.</span><span class="sxs-lookup"><span data-stu-id="adf0d-149">When you create or import a new runbook, you must publish it before you can run it.</span></span>  <span data-ttu-id="adf0d-150">Each runbook in Automation has a Draft and a Published version.</span><span class="sxs-lookup"><span data-stu-id="adf0d-150">Each runbook in Automation has a Draft and a Published version.</span></span> <span data-ttu-id="adf0d-151">Only the Published version is available to be run, and only the Draft version can be edited.</span><span class="sxs-lookup"><span data-stu-id="adf0d-151">Only the Published version is available to be run, and only the Draft version can be edited.</span></span> <span data-ttu-id="adf0d-152">The Published version is unaffected by any changes to the Draft version.</span><span class="sxs-lookup"><span data-stu-id="adf0d-152">The Published version is unaffected by any changes to the Draft version.</span></span> <span data-ttu-id="adf0d-153">When the Draft version should be made available, then you publish it, which overwrites the Published version with the Draft version.</span><span class="sxs-lookup"><span data-stu-id="adf0d-153">When the Draft version should be made available, then you publish it, which overwrites the Published version with the Draft version.</span></span>

## <a name="to-publish-a-runbook-using-the-azure-portal"></a><span data-ttu-id="adf0d-154">To publish a runbook using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="adf0d-154">To publish a runbook using the Azure portal</span></span>

1. <span data-ttu-id="adf0d-155">Open the runbook in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="adf0d-155">Open the runbook in the Azure portal.</span></span>
1. <span data-ttu-id="adf0d-156">Click the **Edit** button.</span><span class="sxs-lookup"><span data-stu-id="adf0d-156">Click the **Edit** button.</span></span>
1. <span data-ttu-id="adf0d-157">Click the **Publish** button and then **Yes** to the verification message.</span><span class="sxs-lookup"><span data-stu-id="adf0d-157">Click the **Publish** button and then **Yes** to the verification message.</span></span>

## <a name="to-publish-a-runbook-using-windows-powershell"></a><span data-ttu-id="adf0d-158">To publish a runbook using Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="adf0d-158">To publish a runbook using Windows PowerShell</span></span>
<span data-ttu-id="adf0d-159">You can use the [Publish-AzureRmAutomationRunbook](https://docs.microsoft.com/powershell/module/azurerm.automation/publish-azurermautomationrunbook) cmdlet to publish a runbook with Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="adf0d-159">You can use the [Publish-AzureRmAutomationRunbook](https://docs.microsoft.com/powershell/module/azurerm.automation/publish-azurermautomationrunbook) cmdlet to publish a runbook with Windows PowerShell.</span></span> <span data-ttu-id="adf0d-160">The following sample commands show how to publish a sample runbook.</span><span class="sxs-lookup"><span data-stu-id="adf0d-160">The following sample commands show how to publish a sample runbook.</span></span>

```azurepowershell-interactive
$automationAccountName =  "AutomationAccount"
$runbookName = "Sample_TestRunbook"
$RGName = "ResourceGroup"

Publish-AzureRmAutomationRunbook -AutomationAccountName $automationAccountName `
-Name $runbookName -ResourceGroupName $RGName
```

## <a name="next-steps"></a><span data-ttu-id="adf0d-161">Next Steps</span><span class="sxs-lookup"><span data-stu-id="adf0d-161">Next Steps</span></span>

* <span data-ttu-id="adf0d-162">To learn about how you can benefit from the Runbook and PowerShell Module Gallery, see  [Runbook and module galleries for Azure Automation](automation-runbook-gallery.md)</span><span class="sxs-lookup"><span data-stu-id="adf0d-162">To learn about how you can benefit from the Runbook and PowerShell Module Gallery, see  [Runbook and module galleries for Azure Automation](automation-runbook-gallery.md)</span></span>
* <span data-ttu-id="adf0d-163">To learn more about editing PowerShell and PowerShell Workflow runbooks with a textual editor, see [Editing textual runbooks in Azure Automation](automation-edit-textual-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="adf0d-163">To learn more about editing PowerShell and PowerShell Workflow runbooks with a textual editor, see [Editing textual runbooks in Azure Automation](automation-edit-textual-runbook.md)</span></span>
* <span data-ttu-id="adf0d-164">To learn more about Graphical runbook authoring, see [Graphical authoring in Azure Automation](automation-graphical-authoring-intro.md)</span><span class="sxs-lookup"><span data-stu-id="adf0d-164">To learn more about Graphical runbook authoring, see [Graphical authoring in Azure Automation](automation-graphical-authoring-intro.md)</span></span>