---
title: Variable assets in Azure Automation
description: Variable assets are values that are available to all runbooks and DSC configurations in Azure Automation.  This article explains the details of variables and how to work with them in both textual and graphical authoring.
services: automation
ms.service: automation
ms.component: shared-capabilities
author: georgewallace
ms.author: gwallace
ms.date: 03/16/2018
ms.topic: conceptual
manager: carmonm
ms.openlocfilehash: ea6aae349bfbec0d1b6538010df42e7a0fb22d8e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44827658"
---
# <a name="variable-assets-in-azure-automation"></a><span data-ttu-id="48c2c-104">Variable assets in Azure Automation</span><span class="sxs-lookup"><span data-stu-id="48c2c-104">Variable assets in Azure Automation</span></span>

<span data-ttu-id="48c2c-105">Variable assets are values that are available to all runbooks and DSC configurations in your automation account.</span><span class="sxs-lookup"><span data-stu-id="48c2c-105">Variable assets are values that are available to all runbooks and DSC configurations in your automation account.</span></span> <span data-ttu-id="48c2c-106">They can be created, modified, and retrieved from the Azure portal, Windows PowerShell, and from within a runbook or DSC configuration.</span><span class="sxs-lookup"><span data-stu-id="48c2c-106">They can be created, modified, and retrieved from the Azure portal, Windows PowerShell, and from within a runbook or DSC configuration.</span></span> <span data-ttu-id="48c2c-107">Automation variables are useful for the following scenarios:</span><span class="sxs-lookup"><span data-stu-id="48c2c-107">Automation variables are useful for the following scenarios:</span></span>

- <span data-ttu-id="48c2c-108">Share a value between multiple runbooks or DSC configurations.</span><span class="sxs-lookup"><span data-stu-id="48c2c-108">Share a value between multiple runbooks or DSC configurations.</span></span>

- <span data-ttu-id="48c2c-109">Share a value between multiple jobs from the same runbook or DSC configuration.</span><span class="sxs-lookup"><span data-stu-id="48c2c-109">Share a value between multiple jobs from the same runbook or DSC configuration.</span></span>

- <span data-ttu-id="48c2c-110">Manage a value from the portal or from the Windows PowerShell command line that is used by runbooks or DSC configurations, such as a set of common configuration items like specific list of VM names, a specific resource group,  an AD domain name, etc.</span><span class="sxs-lookup"><span data-stu-id="48c2c-110">Manage a value from the portal or from the Windows PowerShell command line that is used by runbooks or DSC configurations, such as a set of common configuration items like specific list of VM names, a specific resource group,  an AD domain name, etc.</span></span>  

<span data-ttu-id="48c2c-111">Automation variables are persisted so that they continue to be available even if the runbook or DSC configuration fails.</span><span class="sxs-lookup"><span data-stu-id="48c2c-111">Automation variables are persisted so that they continue to be available even if the runbook or DSC configuration fails.</span></span> <span data-ttu-id="48c2c-112">This also allows a value to be set by one runbook that is then used by another, or is used by the same runbook or DSC configuration the next time that it is run.</span><span class="sxs-lookup"><span data-stu-id="48c2c-112">This also allows a value to be set by one runbook that is then used by another, or is used by the same runbook or DSC configuration the next time that it is run.</span></span>

<span data-ttu-id="48c2c-113">When a variable is created, you can specify that it is stored encrypted.</span><span class="sxs-lookup"><span data-stu-id="48c2c-113">When a variable is created, you can specify that it is stored encrypted.</span></span> <span data-ttu-id="48c2c-114">When a variable is encrypted, it is stored securely in Azure Automation, and its value cannot be retrieved from the [Get-AzureRmAutomationVariable](/powershell/module/AzureRM.Automation/Get-AzureRmAutomationVariable) cmdlet that ships as part of the Azure PowerShell module.</span><span class="sxs-lookup"><span data-stu-id="48c2c-114">When a variable is encrypted, it is stored securely in Azure Automation, and its value cannot be retrieved from the [Get-AzureRmAutomationVariable](/powershell/module/AzureRM.Automation/Get-AzureRmAutomationVariable) cmdlet that ships as part of the Azure PowerShell module.</span></span> <span data-ttu-id="48c2c-115">The only way that an encrypted value can be retrieved is from the **Get-AutomationVariable** activity in a runbook or DSC configuration.</span><span class="sxs-lookup"><span data-stu-id="48c2c-115">The only way that an encrypted value can be retrieved is from the **Get-AutomationVariable** activity in a runbook or DSC configuration.</span></span>

>[!NOTE]
><span data-ttu-id="48c2c-116">Secure assets in Azure Automation include credentials, certificates, connections, and encrypted variables.</span><span class="sxs-lookup"><span data-stu-id="48c2c-116">Secure assets in Azure Automation include credentials, certificates, connections, and encrypted variables.</span></span> <span data-ttu-id="48c2c-117">These assets are encrypted and stored in Azure Automation using a unique key that is generated for each automation account.</span><span class="sxs-lookup"><span data-stu-id="48c2c-117">These assets are encrypted and stored in Azure Automation using a unique key that is generated for each automation account.</span></span> <span data-ttu-id="48c2c-118">This key is stored in Key Vault.</span><span class="sxs-lookup"><span data-stu-id="48c2c-118">This key is stored in Key Vault.</span></span> <span data-ttu-id="48c2c-119">Before storing a secure asset, the key is loaded from Key Vault and then used to encrypt the asset.</span><span class="sxs-lookup"><span data-stu-id="48c2c-119">Before storing a secure asset, the key is loaded from Key Vault and then used to encrypt the asset.</span></span>

## <a name="variable-types"></a><span data-ttu-id="48c2c-120">Variable types</span><span class="sxs-lookup"><span data-stu-id="48c2c-120">Variable types</span></span>

<span data-ttu-id="48c2c-121">When you create a variable with the Azure portal, you must specify a data type from the drop-down list so the portal can display the appropriate control for entering the variable value.</span><span class="sxs-lookup"><span data-stu-id="48c2c-121">When you create a variable with the Azure portal, you must specify a data type from the drop-down list so the portal can display the appropriate control for entering the variable value.</span></span> <span data-ttu-id="48c2c-122">The variable is not restricted to this data type, but you must set the variable using Windows PowerShell if you want to specify a value of a different type.</span><span class="sxs-lookup"><span data-stu-id="48c2c-122">The variable is not restricted to this data type, but you must set the variable using Windows PowerShell if you want to specify a value of a different type.</span></span> <span data-ttu-id="48c2c-123">If you specify **Not defined**, then the value of the variable is set to **$null**, and you must set the value with the [Set-AzureRMAutomationVariable](/powershell/module/AzureRM.Automation/Set-AzureRmAutomationVariable) cmdlet or **Set-AutomationVariable** activity.</span><span class="sxs-lookup"><span data-stu-id="48c2c-123">If you specify **Not defined**, then the value of the variable is set to **$null**, and you must set the value with the [Set-AzureRMAutomationVariable](/powershell/module/AzureRM.Automation/Set-AzureRmAutomationVariable) cmdlet or **Set-AutomationVariable** activity.</span></span> <span data-ttu-id="48c2c-124">You cannot create or change the value for a complex variable type in the portal, but you can provide a value of any type using Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="48c2c-124">You cannot create or change the value for a complex variable type in the portal, but you can provide a value of any type using Windows PowerShell.</span></span> <span data-ttu-id="48c2c-125">Complex types are returned as a [PSCustomObject](/dotnet/api/system.management.automation.pscustomobject).</span><span class="sxs-lookup"><span data-stu-id="48c2c-125">Complex types are returned as a [PSCustomObject](/dotnet/api/system.management.automation.pscustomobject).</span></span>

<span data-ttu-id="48c2c-126">You can store multiple values to a single variable by creating an array or hashtable and saving it to the variable.</span><span class="sxs-lookup"><span data-stu-id="48c2c-126">You can store multiple values to a single variable by creating an array or hashtable and saving it to the variable.</span></span>

<span data-ttu-id="48c2c-127">The following are a list of variable types available in Automation:</span><span class="sxs-lookup"><span data-stu-id="48c2c-127">The following are a list of variable types available in Automation:</span></span>

* <span data-ttu-id="48c2c-128">String</span><span class="sxs-lookup"><span data-stu-id="48c2c-128">String</span></span>
* <span data-ttu-id="48c2c-129">Integer</span><span class="sxs-lookup"><span data-stu-id="48c2c-129">Integer</span></span>
* <span data-ttu-id="48c2c-130">DateTime</span><span class="sxs-lookup"><span data-stu-id="48c2c-130">DateTime</span></span>
* <span data-ttu-id="48c2c-131">Boolean</span><span class="sxs-lookup"><span data-stu-id="48c2c-131">Boolean</span></span>
* <span data-ttu-id="48c2c-132">Null</span><span class="sxs-lookup"><span data-stu-id="48c2c-132">Null</span></span>

## <a name="azurerm-powershell-cmdlets"></a><span data-ttu-id="48c2c-133">AzureRM PowerShell cmdlets</span><span class="sxs-lookup"><span data-stu-id="48c2c-133">AzureRM PowerShell cmdlets</span></span>
<span data-ttu-id="48c2c-134">For AzureRM, the cmdlets in the following table are used to create and manage automation credential assets with Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="48c2c-134">For AzureRM, the cmdlets in the following table are used to create and manage automation credential assets with Windows PowerShell.</span></span> <span data-ttu-id="48c2c-135">They ship as part of the [AzureRM.Automation module](/powershell/azure/overview) which is available for use in Automation runbooks and DSC configurations.</span><span class="sxs-lookup"><span data-stu-id="48c2c-135">They ship as part of the [AzureRM.Automation module](/powershell/azure/overview) which is available for use in Automation runbooks and DSC configurations.</span></span>

| <span data-ttu-id="48c2c-136">Cmdlets</span><span class="sxs-lookup"><span data-stu-id="48c2c-136">Cmdlets</span></span> | <span data-ttu-id="48c2c-137">Description</span><span class="sxs-lookup"><span data-stu-id="48c2c-137">Description</span></span> |
|:---|:---|
|[<span data-ttu-id="48c2c-138">Get-AzureRmAutomationVariable</span><span class="sxs-lookup"><span data-stu-id="48c2c-138">Get-AzureRmAutomationVariable</span></span>](/powershell/module/AzureRM.Automation/Get-AzureRmAutomationVariable)|<span data-ttu-id="48c2c-139">Retrieves the value of an existing variable.</span><span class="sxs-lookup"><span data-stu-id="48c2c-139">Retrieves the value of an existing variable.</span></span>|
|[<span data-ttu-id="48c2c-140">New-AzureRmAutomationVariable</span><span class="sxs-lookup"><span data-stu-id="48c2c-140">New-AzureRmAutomationVariable</span></span>](/powershell/module/AzureRM.Automation/New-AzureRmAutomationVariable)|<span data-ttu-id="48c2c-141">Creates a new variable and sets its value.</span><span class="sxs-lookup"><span data-stu-id="48c2c-141">Creates a new variable and sets its value.</span></span>|
|[<span data-ttu-id="48c2c-142">Remove-AzureRmAutomationVariable</span><span class="sxs-lookup"><span data-stu-id="48c2c-142">Remove-AzureRmAutomationVariable</span></span>](/powershell/module/AzureRM.Automation/Remove-AzureRmAutomationVariable)|<span data-ttu-id="48c2c-143">Removes an existing variable.</span><span class="sxs-lookup"><span data-stu-id="48c2c-143">Removes an existing variable.</span></span>|
|[<span data-ttu-id="48c2c-144">Set-AzureRmAutomationVariable</span><span class="sxs-lookup"><span data-stu-id="48c2c-144">Set-AzureRmAutomationVariable</span></span>](/powershell/module/AzureRM.Automation/Set-AzureRmAutomationVariable)|<span data-ttu-id="48c2c-145">Sets the value for an existing variable.</span><span class="sxs-lookup"><span data-stu-id="48c2c-145">Sets the value for an existing variable.</span></span>|

## <a name="activities"></a><span data-ttu-id="48c2c-146">Activities</span><span class="sxs-lookup"><span data-stu-id="48c2c-146">Activities</span></span>
<span data-ttu-id="48c2c-147">The activities in the following table are used to access credentials in a runbook and DSC configurations.</span><span class="sxs-lookup"><span data-stu-id="48c2c-147">The activities in the following table are used to access credentials in a runbook and DSC configurations.</span></span>

| <span data-ttu-id="48c2c-148">Activities</span><span class="sxs-lookup"><span data-stu-id="48c2c-148">Activities</span></span> | <span data-ttu-id="48c2c-149">Description</span><span class="sxs-lookup"><span data-stu-id="48c2c-149">Description</span></span> |
|:---|:---|
|<span data-ttu-id="48c2c-150">Get-AutomationVariable</span><span class="sxs-lookup"><span data-stu-id="48c2c-150">Get-AutomationVariable</span></span>|<span data-ttu-id="48c2c-151">Retrieves the value of an existing variable.</span><span class="sxs-lookup"><span data-stu-id="48c2c-151">Retrieves the value of an existing variable.</span></span>|
|<span data-ttu-id="48c2c-152">Set-AutomationVariable</span><span class="sxs-lookup"><span data-stu-id="48c2c-152">Set-AutomationVariable</span></span>|<span data-ttu-id="48c2c-153">Sets the value for an existing variable.</span><span class="sxs-lookup"><span data-stu-id="48c2c-153">Sets the value for an existing variable.</span></span>|

> [!NOTE] 
> <span data-ttu-id="48c2c-154">You should avoid using variables in the –Name parameter of **Get-AutomationVariable**  in a runbook or DSC configuration since this can complicate discovering dependencies between runbooks or DSC configuration, and Automation variables at design time.</span><span class="sxs-lookup"><span data-stu-id="48c2c-154">You should avoid using variables in the –Name parameter of **Get-AutomationVariable**  in a runbook or DSC configuration since this can complicate discovering dependencies between runbooks or DSC configuration, and Automation variables at design time.</span></span>

<span data-ttu-id="48c2c-155">The functions in the following table are used to access and retrieve variables in a Python2 runbook.</span><span class="sxs-lookup"><span data-stu-id="48c2c-155">The functions in the following table are used to access and retrieve variables in a Python2 runbook.</span></span> 

|<span data-ttu-id="48c2c-156">Python2 Functions</span><span class="sxs-lookup"><span data-stu-id="48c2c-156">Python2 Functions</span></span>|<span data-ttu-id="48c2c-157">Description</span><span class="sxs-lookup"><span data-stu-id="48c2c-157">Description</span></span>|
|:---|:---|
|<span data-ttu-id="48c2c-158">automationassets.get_automation_variable</span><span class="sxs-lookup"><span data-stu-id="48c2c-158">automationassets.get_automation_variable</span></span>|<span data-ttu-id="48c2c-159">Retrieves the value of an existing variable.</span><span class="sxs-lookup"><span data-stu-id="48c2c-159">Retrieves the value of an existing variable.</span></span> |
|<span data-ttu-id="48c2c-160">automationassets.set_automation_variable</span><span class="sxs-lookup"><span data-stu-id="48c2c-160">automationassets.set_automation_variable</span></span>|<span data-ttu-id="48c2c-161">Sets the value for an existing variable.</span><span class="sxs-lookup"><span data-stu-id="48c2c-161">Sets the value for an existing variable.</span></span> |

> [!NOTE] 
> <span data-ttu-id="48c2c-162">You must import the "automationassets" module at the top of your Python runbook in order to access the asset functions.</span><span class="sxs-lookup"><span data-stu-id="48c2c-162">You must import the "automationassets" module at the top of your Python runbook in order to access the asset functions.</span></span>

## <a name="creating-a-new-automation-variable"></a><span data-ttu-id="48c2c-163">Creating a new Automation variable</span><span class="sxs-lookup"><span data-stu-id="48c2c-163">Creating a new Automation variable</span></span>

### <a name="to-create-a-new-variable-with-the-azure-portal"></a><span data-ttu-id="48c2c-164">To create a new variable with the Azure portal</span><span class="sxs-lookup"><span data-stu-id="48c2c-164">To create a new variable with the Azure portal</span></span>

1. <span data-ttu-id="48c2c-165">From your Automation account, click the **Assets** tile and then on the **Assets** blade, select **Variables**.</span><span class="sxs-lookup"><span data-stu-id="48c2c-165">From your Automation account, click the **Assets** tile and then on the **Assets** blade, select **Variables**.</span></span>
2. <span data-ttu-id="48c2c-166">On the **Variables** tile, select **Add a variable**.</span><span class="sxs-lookup"><span data-stu-id="48c2c-166">On the **Variables** tile, select **Add a variable**.</span></span>
3. <span data-ttu-id="48c2c-167">Complete the options on the **New Variable** blade and click **Create** save the new variable.</span><span class="sxs-lookup"><span data-stu-id="48c2c-167">Complete the options on the **New Variable** blade and click **Create** save the new variable.</span></span>

### <a name="to-create-a-new-variable-with-windows-powershell"></a><span data-ttu-id="48c2c-168">To create a new variable with Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="48c2c-168">To create a new variable with Windows PowerShell</span></span>

<span data-ttu-id="48c2c-169">The [New-AzureRmAutomationVariable](/powershell/module/AzureRM.Automation/New-AzureRmAutomationVariable) cmdlet creates a new variable and sets its initial value.</span><span class="sxs-lookup"><span data-stu-id="48c2c-169">The [New-AzureRmAutomationVariable](/powershell/module/AzureRM.Automation/New-AzureRmAutomationVariable) cmdlet creates a new variable and sets its initial value.</span></span> <span data-ttu-id="48c2c-170">You can retrieve the value using [Get-AzureRmAutomationVariable](/powershell/module/AzureRM.Automation/Get-AzureRmAutomationVariable).</span><span class="sxs-lookup"><span data-stu-id="48c2c-170">You can retrieve the value using [Get-AzureRmAutomationVariable](/powershell/module/AzureRM.Automation/Get-AzureRmAutomationVariable).</span></span> <span data-ttu-id="48c2c-171">If the value is a simple type, then that same type is returned.</span><span class="sxs-lookup"><span data-stu-id="48c2c-171">If the value is a simple type, then that same type is returned.</span></span> <span data-ttu-id="48c2c-172">If it’s a complex type, then a **PSCustomObject** is returned.</span><span class="sxs-lookup"><span data-stu-id="48c2c-172">If it’s a complex type, then a **PSCustomObject** is returned.</span></span>

<span data-ttu-id="48c2c-173">The following sample commands show how to create a variable of type string and then return its value.</span><span class="sxs-lookup"><span data-stu-id="48c2c-173">The following sample commands show how to create a variable of type string and then return its value.</span></span>

    New-AzureRmAutomationVariable -ResourceGroupName "ResourceGroup01" 
    –AutomationAccountName "MyAutomationAccount" –Name 'MyStringVariable' `
    –Encrypted $false –Value 'My String'
    $string = (Get-AzureRmAutomationVariable -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name 'MyStringVariable').Value

<span data-ttu-id="48c2c-174">The following sample commands show how to create a variable with a complex type and then return its properties.</span><span class="sxs-lookup"><span data-stu-id="48c2c-174">The following sample commands show how to create a variable with a complex type and then return its properties.</span></span> <span data-ttu-id="48c2c-175">In this case, a virtual machine object from **Get-AzureRmVm** is used.</span><span class="sxs-lookup"><span data-stu-id="48c2c-175">In this case, a virtual machine object from **Get-AzureRmVm** is used.</span></span>

    $vm = Get-AzureRmVm -ResourceGroupName "ResourceGroup01" –Name "VM01"
    New-AzureRmAutomationVariable –AutomationAccountName "MyAutomationAccount" –Name "MyComplexVariable" –Encrypted $false –Value $vm
    
    $vmValue = (Get-AzureRmAutomationVariable -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name "MyComplexVariable").Value
    $vmName = $vmValue.Name
    $vmIpAddress = $vmValue.IpAddress



## <a name="using-a-variable-in-a-runbook-or-dsc-configuration"></a><span data-ttu-id="48c2c-176">Using a variable in a runbook or DSC configuration</span><span class="sxs-lookup"><span data-stu-id="48c2c-176">Using a variable in a runbook or DSC configuration</span></span>

<span data-ttu-id="48c2c-177">Use the **Set-AutomationVariable** activity to set the value of an Automation variable in a PowerShell runbook or DSC configuration, and the **Get-AutomationVariable** to retrieve it.</span><span class="sxs-lookup"><span data-stu-id="48c2c-177">Use the **Set-AutomationVariable** activity to set the value of an Automation variable in a PowerShell runbook or DSC configuration, and the **Get-AutomationVariable** to retrieve it.</span></span> <span data-ttu-id="48c2c-178">You shouldn't use the **Set-AzureRMAutomationVariable** or  **Get-AzureRMAutomationVariable** cmdlets in a runbook or DSC configuration since they are less efficient than the workflow activities.</span><span class="sxs-lookup"><span data-stu-id="48c2c-178">You shouldn't use the **Set-AzureRMAutomationVariable** or  **Get-AzureRMAutomationVariable** cmdlets in a runbook or DSC configuration since they are less efficient than the workflow activities.</span></span> <span data-ttu-id="48c2c-179">You also cannot retrieve the value of secure variables with **Get-AzureRMAutomationVariable**.</span><span class="sxs-lookup"><span data-stu-id="48c2c-179">You also cannot retrieve the value of secure variables with **Get-AzureRMAutomationVariable**.</span></span> <span data-ttu-id="48c2c-180">The only way to create a new variable from within a runbook or DSC configuration is to use the [New-AzureRMAutomationVariable](/powershell/module/AzureRM.Automation/New-AzureRmAutomationVariable)  cmdlet.</span><span class="sxs-lookup"><span data-stu-id="48c2c-180">The only way to create a new variable from within a runbook or DSC configuration is to use the [New-AzureRMAutomationVariable](/powershell/module/AzureRM.Automation/New-AzureRmAutomationVariable)  cmdlet.</span></span>


### <a name="textual-runbook-samples"></a><span data-ttu-id="48c2c-181">Textual runbook samples</span><span class="sxs-lookup"><span data-stu-id="48c2c-181">Textual runbook samples</span></span>

#### <a name="setting-and-retrieving-a-simple-value-from-a-variable"></a><span data-ttu-id="48c2c-182">Setting and retrieving a simple value from a variable</span><span class="sxs-lookup"><span data-stu-id="48c2c-182">Setting and retrieving a simple value from a variable</span></span>

<span data-ttu-id="48c2c-183">The following sample commands show how to set and retrieve a variable in a textual runbook.</span><span class="sxs-lookup"><span data-stu-id="48c2c-183">The following sample commands show how to set and retrieve a variable in a textual runbook.</span></span> <span data-ttu-id="48c2c-184">In this sample, it is assumed that variables of type integer named *NumberOfIterations* and *NumberOfRunnings* and a variable of type string named *SampleMessage* have already been created.</span><span class="sxs-lookup"><span data-stu-id="48c2c-184">In this sample, it is assumed that variables of type integer named *NumberOfIterations* and *NumberOfRunnings* and a variable of type string named *SampleMessage* have already been created.</span></span>

    $NumberOfIterations = Get-AzureRmAutomationVariable -ResourceGroupName "ResourceGroup01" –AutomationAccountName "MyAutomationAccount" -Name 'NumberOfIterations'
    $NumberOfRunnings = Get-AzureRmAutomationVariable -ResourceGroupName "ResourceGroup01" –AutomationAccountName "MyAutomationAccount" -Name 'NumberOfRunnings'
    $SampleMessage = Get-AutomationVariable -Name 'SampleMessage'
    
    Write-Output "Runbook has been run $NumberOfRunnings times."
    
    for ($i = 1; $i -le $NumberOfIterations; $i++) {
       Write-Output "$i`: $SampleMessage"
    }
    Set-AzureRmAutomationVariable -ResourceGroupName "ResourceGroup01" –AutomationAccountName "MyAutomationAccount" –Name NumberOfRunnings –Value ($NumberOfRunnings += 1)

#### <a name="setting-and-retrieving-a-complex-object-in-a-variable"></a><span data-ttu-id="48c2c-185">Setting and retrieving a complex object in a variable</span><span class="sxs-lookup"><span data-stu-id="48c2c-185">Setting and retrieving a complex object in a variable</span></span>

<span data-ttu-id="48c2c-186">The following sample code shows how to update a variable with a complex value in a textual runbook.</span><span class="sxs-lookup"><span data-stu-id="48c2c-186">The following sample code shows how to update a variable with a complex value in a textual runbook.</span></span> <span data-ttu-id="48c2c-187">In this sample, an Azure virtual machine is retrieved with **Get-AzureVM** and saved to an existing Automation variable.</span><span class="sxs-lookup"><span data-stu-id="48c2c-187">In this sample, an Azure virtual machine is retrieved with **Get-AzureVM** and saved to an existing Automation variable.</span></span>  <span data-ttu-id="48c2c-188">As explained in [Variable types](#variable-types), this is stored as a PSCustomObject.</span><span class="sxs-lookup"><span data-stu-id="48c2c-188">As explained in [Variable types](#variable-types), this is stored as a PSCustomObject.</span></span>

    $vm = Get-AzureVM -ServiceName "MyVM" -Name "MyVM"
    Set-AutomationVariable -Name "MyComplexVariable" -Value $vm

<span data-ttu-id="48c2c-189">In the following code, the value is retrieved from the variable and used to start the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="48c2c-189">In the following code, the value is retrieved from the variable and used to start the virtual machine.</span></span>

    $vmObject = Get-AutomationVariable -Name "MyComplexVariable"
    if ($vmObject.PowerState -eq 'Stopped') {
       Start-AzureVM -ServiceName $vmObject.ServiceName -Name $vmObject.Name
    }


#### <a name="setting-and-retrieving-a-collection-in-a-variable"></a><span data-ttu-id="48c2c-190">Setting and retrieving a collection in a variable</span><span class="sxs-lookup"><span data-stu-id="48c2c-190">Setting and retrieving a collection in a variable</span></span>

<span data-ttu-id="48c2c-191">The following sample code shows how to use a variable with a collection of complex values in a textual runbook.</span><span class="sxs-lookup"><span data-stu-id="48c2c-191">The following sample code shows how to use a variable with a collection of complex values in a textual runbook.</span></span> <span data-ttu-id="48c2c-192">In this sample, multiple Azure virtual machines are retrieved with **Get-AzureVM** and saved to an existing Automation variable.</span><span class="sxs-lookup"><span data-stu-id="48c2c-192">In this sample, multiple Azure virtual machines are retrieved with **Get-AzureVM** and saved to an existing Automation variable.</span></span> <span data-ttu-id="48c2c-193">As explained in [Variable types](#variable-types), this is stored as a collection of PSCustomObjects.</span><span class="sxs-lookup"><span data-stu-id="48c2c-193">As explained in [Variable types](#variable-types), this is stored as a collection of PSCustomObjects.</span></span>

    $vms = Get-AzureVM | Where -FilterScript {$_.Name -match "my"}     
    Set-AutomationVariable -Name 'MyComplexVariable' -Value $vms

<span data-ttu-id="48c2c-194">In the following code, the collection is retrieved from the variable and used to start each virtual machine.</span><span class="sxs-lookup"><span data-stu-id="48c2c-194">In the following code, the collection is retrieved from the variable and used to start each virtual machine.</span></span>

    $vmValues = Get-AutomationVariable -Name "MyComplexVariable"
    ForEach ($vmValue in $vmValues)
    {
       if ($vmValue.PowerState -eq 'Stopped') {
          Start-AzureVM -ServiceName $vmValue.ServiceName -Name $vmValue.Name
       }
    }
    
#### <a name="setting-and-retrieving-a-variable-in-python2"></a><span data-ttu-id="48c2c-195">Setting and retrieving a variable in Python2</span><span class="sxs-lookup"><span data-stu-id="48c2c-195">Setting and retrieving a variable in Python2</span></span>
<span data-ttu-id="48c2c-196">The following sample code shows how to use a variable, set a variable, and handle an exception for a non-existent variable in a Python2 runbook.</span><span class="sxs-lookup"><span data-stu-id="48c2c-196">The following sample code shows how to use a variable, set a variable, and handle an exception for a non-existent variable in a Python2 runbook.</span></span>

    import automationassets
    from automationassets import AutomationAssetNotFound

    # get a variable
    value = automationassets.get_automation_variable("test-variable")
    print value

    # set a variable (value can be int/bool/string)
    automationassets.set_automation_variable("test-variable", True)
    automationassets.set_automation_variable("test-variable", 4)
    automationassets.set_automation_variable("test-variable", "test-string")

    # handle a non-existent variable exception
    try:
        value = automationassets.get_automation_variable("non-existing variable")
    except AutomationAssetNotFound:
        print "variable not found"


### <a name="graphical-runbook-samples"></a><span data-ttu-id="48c2c-197">Graphical runbook samples</span><span class="sxs-lookup"><span data-stu-id="48c2c-197">Graphical runbook samples</span></span>

<span data-ttu-id="48c2c-198">In a graphical runbook, you add the **Get-AutomationVariable** or **Set-AutomationVariable** by right-clicking on the variable in the Library pane of the graphical editor and selecting the activity you want.</span><span class="sxs-lookup"><span data-stu-id="48c2c-198">In a graphical runbook, you add the **Get-AutomationVariable** or **Set-AutomationVariable** by right-clicking on the variable in the Library pane of the graphical editor and selecting the activity you want.</span></span>

![Add variable to canvas](media/automation-variables/runbook-variable-add-canvas.png)

#### <a name="setting-values-in-a-variable"></a><span data-ttu-id="48c2c-200">Setting values in a variable</span><span class="sxs-lookup"><span data-stu-id="48c2c-200">Setting values in a variable</span></span>
<span data-ttu-id="48c2c-201">The following image shows sample activities to update a variable with a simple value in a graphical runbook.</span><span class="sxs-lookup"><span data-stu-id="48c2c-201">The following image shows sample activities to update a variable with a simple value in a graphical runbook.</span></span> <span data-ttu-id="48c2c-202">In this sample, a single Azure virtual machine is retrieved with **Get-AzureRmVM** and the computer name is saved to an existing Automation variable with a type of String.</span><span class="sxs-lookup"><span data-stu-id="48c2c-202">In this sample, a single Azure virtual machine is retrieved with **Get-AzureRmVM** and the computer name is saved to an existing Automation variable with a type of String.</span></span> <span data-ttu-id="48c2c-203">It doesn't matter whether the [link is a pipeline or sequence](automation-graphical-authoring-intro.md#links-and-workflow) since you only expect a single object in the output.</span><span class="sxs-lookup"><span data-stu-id="48c2c-203">It doesn't matter whether the [link is a pipeline or sequence](automation-graphical-authoring-intro.md#links-and-workflow) since you only expect a single object in the output.</span></span>

![Set simple variable](media/automation-variables/runbook-set-simple-variable.png)

## <a name="next-steps"></a><span data-ttu-id="48c2c-205">Next Steps</span><span class="sxs-lookup"><span data-stu-id="48c2c-205">Next Steps</span></span>

* <span data-ttu-id="48c2c-206">To learn more about connecting activities together in graphical authoring, see [Links in graphical authoring](automation-graphical-authoring-intro.md#links-and-workflow)</span><span class="sxs-lookup"><span data-stu-id="48c2c-206">To learn more about connecting activities together in graphical authoring, see [Links in graphical authoring](automation-graphical-authoring-intro.md#links-and-workflow)</span></span>
* <span data-ttu-id="48c2c-207">To get started with Graphical runbooks, see [My first graphical runbook](automation-first-runbook-graphical.md)</span><span class="sxs-lookup"><span data-stu-id="48c2c-207">To get started with Graphical runbooks, see [My first graphical runbook](automation-first-runbook-graphical.md)</span></span> 
