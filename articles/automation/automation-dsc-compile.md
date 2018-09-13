---
title: Compiling configurations in Azure Automation State Configuration
description: This article describes how to compile Desired State Configuration (DSC) configurations for Azure Automation.
services: automation
ms.service: automation
ms.component: dsc
author: DCtheGeek
ms.author: dacoulte
ms.date: 09/10/2018
ms.topic: conceptual
manager: carmonm
ms.openlocfilehash: 6b45107fc4b98f51ba296cbca03701d20cf3ac50
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44809977"
---
# <a name="compiling-dsc-configurations-in-azure-automation-state-configuration"></a><span data-ttu-id="ed0d8-103">Compiling DSC configurations in Azure Automation State Configuration</span><span class="sxs-lookup"><span data-stu-id="ed0d8-103">Compiling DSC configurations in Azure Automation State Configuration</span></span>

<span data-ttu-id="ed0d8-104">You can compile Desired State Configuration (DSC) configurations in two ways with Azure Automation State Configuration: in the Azure portal and with Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ed0d8-104">You can compile Desired State Configuration (DSC) configurations in two ways with Azure Automation State Configuration: in the Azure portal and with Windows PowerShell.</span></span> <span data-ttu-id="ed0d8-105">The following table helps you determine when to use which method based on the characteristics of each:</span><span class="sxs-lookup"><span data-stu-id="ed0d8-105">The following table helps you determine when to use which method based on the characteristics of each:</span></span>

<span data-ttu-id="ed0d8-106">**Azure portal**</span><span class="sxs-lookup"><span data-stu-id="ed0d8-106">**Azure portal**</span></span>

- <span data-ttu-id="ed0d8-107">Simplest method with interactive user interface</span><span class="sxs-lookup"><span data-stu-id="ed0d8-107">Simplest method with interactive user interface</span></span>
- <span data-ttu-id="ed0d8-108">Form to provide simple parameter values</span><span class="sxs-lookup"><span data-stu-id="ed0d8-108">Form to provide simple parameter values</span></span>
- <span data-ttu-id="ed0d8-109">Easily track job state</span><span class="sxs-lookup"><span data-stu-id="ed0d8-109">Easily track job state</span></span>
- <span data-ttu-id="ed0d8-110">Access authenticated with Azure logon</span><span class="sxs-lookup"><span data-stu-id="ed0d8-110">Access authenticated with Azure logon</span></span>

<span data-ttu-id="ed0d8-111">**Windows PowerShell**</span><span class="sxs-lookup"><span data-stu-id="ed0d8-111">**Windows PowerShell**</span></span>

- <span data-ttu-id="ed0d8-112">Call from command line with Windows PowerShell cmdlets</span><span class="sxs-lookup"><span data-stu-id="ed0d8-112">Call from command line with Windows PowerShell cmdlets</span></span>
- <span data-ttu-id="ed0d8-113">Can be included in automated solution with multiple steps</span><span class="sxs-lookup"><span data-stu-id="ed0d8-113">Can be included in automated solution with multiple steps</span></span>
- <span data-ttu-id="ed0d8-114">Provide simple and complex parameter values</span><span class="sxs-lookup"><span data-stu-id="ed0d8-114">Provide simple and complex parameter values</span></span>
- <span data-ttu-id="ed0d8-115">Track job state</span><span class="sxs-lookup"><span data-stu-id="ed0d8-115">Track job state</span></span>
- <span data-ttu-id="ed0d8-116">Client required to support PowerShell cmdlets</span><span class="sxs-lookup"><span data-stu-id="ed0d8-116">Client required to support PowerShell cmdlets</span></span>
- <span data-ttu-id="ed0d8-117">Pass ConfigurationData</span><span class="sxs-lookup"><span data-stu-id="ed0d8-117">Pass ConfigurationData</span></span>
- <span data-ttu-id="ed0d8-118">Compile configurations that use credentials</span><span class="sxs-lookup"><span data-stu-id="ed0d8-118">Compile configurations that use credentials</span></span>

<span data-ttu-id="ed0d8-119">Once you have decided on a compilation method, use the following procedures to start compiling.</span><span class="sxs-lookup"><span data-stu-id="ed0d8-119">Once you have decided on a compilation method, use the following procedures to start compiling.</span></span>

## <a name="compiling-a-dsc-configuration-with-the-azure-portal"></a><span data-ttu-id="ed0d8-120">Compiling a DSC Configuration with the Azure portal</span><span class="sxs-lookup"><span data-stu-id="ed0d8-120">Compiling a DSC Configuration with the Azure portal</span></span>

1. <span data-ttu-id="ed0d8-121">From your Automation account, click **State configuration (DSC)**.</span><span class="sxs-lookup"><span data-stu-id="ed0d8-121">From your Automation account, click **State configuration (DSC)**.</span></span>
1. <span data-ttu-id="ed0d8-122">Click on the **Configurations** tab, then click on the configuration name to compile.</span><span class="sxs-lookup"><span data-stu-id="ed0d8-122">Click on the **Configurations** tab, then click on the configuration name to compile.</span></span>
1. <span data-ttu-id="ed0d8-123">Click **Compile**.</span><span class="sxs-lookup"><span data-stu-id="ed0d8-123">Click **Compile**.</span></span>
1. <span data-ttu-id="ed0d8-124">If the configuration has no parameters, you are prompted to confirm whether you want to compile it.</span><span class="sxs-lookup"><span data-stu-id="ed0d8-124">If the configuration has no parameters, you are prompted to confirm whether you want to compile it.</span></span> <span data-ttu-id="ed0d8-125">If the configuration has parameters, the **Compile Configuration** blade opens so you can provide parameter values.</span><span class="sxs-lookup"><span data-stu-id="ed0d8-125">If the configuration has parameters, the **Compile Configuration** blade opens so you can provide parameter values.</span></span> <span data-ttu-id="ed0d8-126">See the following [**Basic Parameters**](#basic-parameters) section for further details on parameters.</span><span class="sxs-lookup"><span data-stu-id="ed0d8-126">See the following [**Basic Parameters**](#basic-parameters) section for further details on parameters.</span></span>
1. <span data-ttu-id="ed0d8-127">The **Compilation Job** page is opened so that you can track the compilation job's status, and the node configurations (MOF configuration documents) it caused to be placed on the Azure Automation State Configuration Pull Server.</span><span class="sxs-lookup"><span data-stu-id="ed0d8-127">The **Compilation Job** page is opened so that you can track the compilation job's status, and the node configurations (MOF configuration documents) it caused to be placed on the Azure Automation State Configuration Pull Server.</span></span>

## <a name="compiling-a-dsc-configuration-with-windows-powershell"></a><span data-ttu-id="ed0d8-128">Compiling a DSC Configuration with Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="ed0d8-128">Compiling a DSC Configuration with Windows PowerShell</span></span>

<span data-ttu-id="ed0d8-129">You can use [`Start-AzureRmAutomationDscCompilationJob`](/powershell/module/azurerm.automation/start-azurermautomationdsccompilationjob) to start compiling with Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ed0d8-129">You can use [`Start-AzureRmAutomationDscCompilationJob`](/powershell/module/azurerm.automation/start-azurermautomationdsccompilationjob) to start compiling with Windows PowerShell.</span></span> <span data-ttu-id="ed0d8-130">The following sample code starts compilation of a DSC configuration called **SampleConfig**.</span><span class="sxs-lookup"><span data-stu-id="ed0d8-130">The following sample code starts compilation of a DSC configuration called **SampleConfig**.</span></span>

```powershell
Start-AzureRmAutomationDscCompilationJob -ResourceGroupName 'MyResourceGroup' -AutomationAccountName 'MyAutomationAccount' -ConfigurationName 'SampleConfig'
```

<span data-ttu-id="ed0d8-131">`Start-AzureRmAutomationDscCompilationJob` returns a compilation job object that you can use to track its status.</span><span class="sxs-lookup"><span data-stu-id="ed0d8-131">`Start-AzureRmAutomationDscCompilationJob` returns a compilation job object that you can use to track its status.</span></span> <span data-ttu-id="ed0d8-132">You can then use this compilation job object with [`Get-AzureRmAutomationDscCompilationJob`](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjob)</span><span class="sxs-lookup"><span data-stu-id="ed0d8-132">You can then use this compilation job object with [`Get-AzureRmAutomationDscCompilationJob`](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjob)</span></span>
<span data-ttu-id="ed0d8-133">to determine the status of the compilation job, and [`Get-AzureRmAutomationDscCompilationJobOutput`](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjoboutput)</span><span class="sxs-lookup"><span data-stu-id="ed0d8-133">to determine the status of the compilation job, and [`Get-AzureRmAutomationDscCompilationJobOutput`](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjoboutput)</span></span>
<span data-ttu-id="ed0d8-134">to view its streams (output).</span><span class="sxs-lookup"><span data-stu-id="ed0d8-134">to view its streams (output).</span></span> <span data-ttu-id="ed0d8-135">The following sample code starts compilation of the **SampleConfig** configuration, waits until it has completed, and then displays its streams.</span><span class="sxs-lookup"><span data-stu-id="ed0d8-135">The following sample code starts compilation of the **SampleConfig** configuration, waits until it has completed, and then displays its streams.</span></span>

```powershell
$CompilationJob = Start-AzureRmAutomationDscCompilationJob -ResourceGroupName 'MyResourceGroup' -AutomationAccountName 'MyAutomationAccount' -ConfigurationName 'SampleConfig'

while($CompilationJob.EndTime –eq $null -and $CompilationJob.Exception –eq $null)
{
    $CompilationJob = $CompilationJob | Get-AzureRmAutomationDscCompilationJob
    Start-Sleep -Seconds 3
}

$CompilationJob | Get-AzureRmAutomationDscCompilationJobOutput –Stream Any
```

## <a name="basic-parameters"></a><span data-ttu-id="ed0d8-136">Basic Parameters</span><span class="sxs-lookup"><span data-stu-id="ed0d8-136">Basic Parameters</span></span>

<span data-ttu-id="ed0d8-137">Parameter declaration in DSC configurations, including parameter types and properties, works the same as in Azure Automation runbooks.</span><span class="sxs-lookup"><span data-stu-id="ed0d8-137">Parameter declaration in DSC configurations, including parameter types and properties, works the same as in Azure Automation runbooks.</span></span> <span data-ttu-id="ed0d8-138">See [Starting a runbook in Azure Automation](automation-starting-a-runbook.md) to learn more about runbook parameters.</span><span class="sxs-lookup"><span data-stu-id="ed0d8-138">See [Starting a runbook in Azure Automation](automation-starting-a-runbook.md) to learn more about runbook parameters.</span></span>

<span data-ttu-id="ed0d8-139">The following example uses two parameters called **FeatureName** and **IsPresent**, to determine the values of properties in the **ParametersExample.sample** node configuration, generated during compilation.</span><span class="sxs-lookup"><span data-stu-id="ed0d8-139">The following example uses two parameters called **FeatureName** and **IsPresent**, to determine the values of properties in the **ParametersExample.sample** node configuration, generated during compilation.</span></span>

```powershell
Configuration ParametersExample
{
    param(
        [Parameter(Mandatory=$true)]
        [string] $FeatureName,

        [Parameter(Mandatory=$true)]
        [boolean] $IsPresent
    )

    $EnsureString = 'Present'
    if($IsPresent -eq $false)
    {
        $EnsureString = 'Absent'
    }

    Node 'sample'
    {
        WindowsFeature ($FeatureName + 'Feature')
        {
            Ensure = $EnsureString
            Name   = $FeatureName
        }
    }
}
```

<span data-ttu-id="ed0d8-140">You can compile DSC Configurations that use basic parameters in the Azure Automation State Configuration portal or with Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="ed0d8-140">You can compile DSC Configurations that use basic parameters in the Azure Automation State Configuration portal or with Azure PowerShell:</span></span>

### <a name="portal"></a><span data-ttu-id="ed0d8-141">Portal</span><span class="sxs-lookup"><span data-stu-id="ed0d8-141">Portal</span></span>

<span data-ttu-id="ed0d8-142">In the portal, you can enter parameter values after clicking **Compile**.</span><span class="sxs-lookup"><span data-stu-id="ed0d8-142">In the portal, you can enter parameter values after clicking **Compile**.</span></span>

![Configuration compile parameters](./media/automation-dsc-compile/DSC_compiling_1.png)

### <a name="powershell"></a><span data-ttu-id="ed0d8-144">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ed0d8-144">PowerShell</span></span>

<span data-ttu-id="ed0d8-145">PowerShell requires parameters in a [hashtable](/powershell/module/microsoft.powershell.core/about/about_hash_tables) where the key matches the parameter name, and the value equals the parameter value.</span><span class="sxs-lookup"><span data-stu-id="ed0d8-145">PowerShell requires parameters in a [hashtable](/powershell/module/microsoft.powershell.core/about/about_hash_tables) where the key matches the parameter name, and the value equals the parameter value.</span></span>

```powershell
$Parameters = @{
    'FeatureName' = 'Web-Server'
    'IsPresent' = $False
}

Start-AzureRmAutomationDscCompilationJob -ResourceGroupName 'MyResourceGroup' -AutomationAccountName 'MyAutomationAccount' -ConfigurationName 'ParametersExample' -Parameters $Parameters
```

<span data-ttu-id="ed0d8-146">For information about passing PSCredentials as parameters, see [Credential Assets](#credential-assets) below.</span><span class="sxs-lookup"><span data-stu-id="ed0d8-146">For information about passing PSCredentials as parameters, see [Credential Assets](#credential-assets) below.</span></span>

## <a name="composite-resources"></a><span data-ttu-id="ed0d8-147">Composite Resources</span><span class="sxs-lookup"><span data-stu-id="ed0d8-147">Composite Resources</span></span>

<span data-ttu-id="ed0d8-148">**Composite Resources** allow you to use DSC configurations as nested resources inside of a configuration.</span><span class="sxs-lookup"><span data-stu-id="ed0d8-148">**Composite Resources** allow you to use DSC configurations as nested resources inside of a configuration.</span></span> <span data-ttu-id="ed0d8-149">This enables you to apply multiple configurations to a single resource.</span><span class="sxs-lookup"><span data-stu-id="ed0d8-149">This enables you to apply multiple configurations to a single resource.</span></span> <span data-ttu-id="ed0d8-150">See [Composite resources: Using a DSC configuration as a resource](/powershell/dsc/authoringresourcecomposite) to learn more about **Composite Resources**.</span><span class="sxs-lookup"><span data-stu-id="ed0d8-150">See [Composite resources: Using a DSC configuration as a resource](/powershell/dsc/authoringresourcecomposite) to learn more about **Composite Resources**.</span></span>

> [!NOTE]
> <span data-ttu-id="ed0d8-151">In order for **Composite Resources** to compile correctly, you must first ensure that any DSC Resources that the composite relies on are first installed in the Azure Automation Account Modules repository or it doesn't import properly.</span><span class="sxs-lookup"><span data-stu-id="ed0d8-151">In order for **Composite Resources** to compile correctly, you must first ensure that any DSC Resources that the composite relies on are first installed in the Azure Automation Account Modules repository or it doesn't import properly.</span></span>

<span data-ttu-id="ed0d8-152">To add a DSC **Composite Resource**, you must add the resource module to an archive (\*.zip).</span><span class="sxs-lookup"><span data-stu-id="ed0d8-152">To add a DSC **Composite Resource**, you must add the resource module to an archive (\*.zip).</span></span> <span data-ttu-id="ed0d8-153">Go to the Modules repository on your Azure Automation Account.</span><span class="sxs-lookup"><span data-stu-id="ed0d8-153">Go to the Modules repository on your Azure Automation Account.</span></span> <span data-ttu-id="ed0d8-154">Then click on the 'Add a Module' button.</span><span class="sxs-lookup"><span data-stu-id="ed0d8-154">Then click on the 'Add a Module' button.</span></span>

![Add Module](./media/automation-dsc-compile/add_module.png)

<span data-ttu-id="ed0d8-156">Navigate to the directory where your archive is located.</span><span class="sxs-lookup"><span data-stu-id="ed0d8-156">Navigate to the directory where your archive is located.</span></span> <span data-ttu-id="ed0d8-157">Select the archive file, and click OK.</span><span class="sxs-lookup"><span data-stu-id="ed0d8-157">Select the archive file, and click OK.</span></span>

![Select Module](./media/automation-dsc-compile/select_dscresource.png)

<span data-ttu-id="ed0d8-159">You are taken back to the modules directory, where you can monitor the status of your **Composite Resource** while it unpacks and registers with Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="ed0d8-159">You are taken back to the modules directory, where you can monitor the status of your **Composite Resource** while it unpacks and registers with Azure Automation.</span></span>

![Import Composite Resource](./media/automation-dsc-compile/register_composite_resource.png)

<span data-ttu-id="ed0d8-161">Once the module is registered, you can then click on it to validate that the **Composite Resources** are now available to be used in a configuration.</span><span class="sxs-lookup"><span data-stu-id="ed0d8-161">Once the module is registered, you can then click on it to validate that the **Composite Resources** are now available to be used in a configuration.</span></span>

![Validate Composite Resource](./media/automation-dsc-compile/validate_composite_resource.png)

<span data-ttu-id="ed0d8-163">Then you can call the **Composite Resource** into your configuration like so:</span><span class="sxs-lookup"><span data-stu-id="ed0d8-163">Then you can call the **Composite Resource** into your configuration like so:</span></span>

```powershell
Node ($AllNodes.Where{$_.Role -eq 'WebServer'}).NodeName
{
    JoinDomain DomainJoin
    {
        DomainName = $DomainName
        Admincreds = $Admincreds
    }

    PSWAWebServer InstallPSWAWebServer
    {
        DependsOn = '[JoinDomain]DomainJoin'
    }
}
```

## <a name="configurationdata"></a><span data-ttu-id="ed0d8-164">ConfigurationData</span><span class="sxs-lookup"><span data-stu-id="ed0d8-164">ConfigurationData</span></span>

<span data-ttu-id="ed0d8-165">**ConfigurationData** allows you to separate structural configuration from any environment-specific configuration while using PowerShell DSC.</span><span class="sxs-lookup"><span data-stu-id="ed0d8-165">**ConfigurationData** allows you to separate structural configuration from any environment-specific configuration while using PowerShell DSC.</span></span> <span data-ttu-id="ed0d8-166">See [Separating "What" from "Where" in PowerShell DSC](http://blogs.msdn.com/b/powershell/archive/2014/01/09/continuous-deployment-using-dsc-with-minimal-change.aspx) to learn more about **ConfigurationData**.</span><span class="sxs-lookup"><span data-stu-id="ed0d8-166">See [Separating "What" from "Where" in PowerShell DSC](http://blogs.msdn.com/b/powershell/archive/2014/01/09/continuous-deployment-using-dsc-with-minimal-change.aspx) to learn more about **ConfigurationData**.</span></span>

> [!NOTE]
> <span data-ttu-id="ed0d8-167">You can use **ConfigurationData** when compiling in Azure Automation State Configuration using Azure PowerShell, but not in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="ed0d8-167">You can use **ConfigurationData** when compiling in Azure Automation State Configuration using Azure PowerShell, but not in the Azure portal.</span></span>

<span data-ttu-id="ed0d8-168">The following example DSC configuration uses **ConfigurationData** via the **$ConfigurationData** and **$AllNodes** keywords.</span><span class="sxs-lookup"><span data-stu-id="ed0d8-168">The following example DSC configuration uses **ConfigurationData** via the **$ConfigurationData** and **$AllNodes** keywords.</span></span> <span data-ttu-id="ed0d8-169">You also need the [**xWebAdministration** module](https://www.powershellgallery.com/packages/xWebAdministration/) for this example:</span><span class="sxs-lookup"><span data-stu-id="ed0d8-169">You also need the [**xWebAdministration** module](https://www.powershellgallery.com/packages/xWebAdministration/) for this example:</span></span>

```powershell
Configuration ConfigurationDataSample
{
    Import-DscResource -ModuleName xWebAdministration -Name MSFT_xWebsite

    Write-Verbose $ConfigurationData.NonNodeData.SomeMessage

    Node $AllNodes.Where{$_.Role -eq 'WebServer'}.NodeName
    {
        xWebsite Site
        {
            Name         = $Node.SiteName
            PhysicalPath = $Node.SiteContents
            Ensure       = 'Present'
        }
    }
}
```

<span data-ttu-id="ed0d8-170">You can compile the preceding DSC configuration with PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ed0d8-170">You can compile the preceding DSC configuration with PowerShell.</span></span> <span data-ttu-id="ed0d8-171">The following PowerShell adds two node configurations to the Azure Automation State Configuration Pull Server: **ConfigurationDataSample.MyVM1** and **ConfigurationDataSample.MyVM3**:</span><span class="sxs-lookup"><span data-stu-id="ed0d8-171">The following PowerShell adds two node configurations to the Azure Automation State Configuration Pull Server: **ConfigurationDataSample.MyVM1** and **ConfigurationDataSample.MyVM3**:</span></span>

```powershell
$ConfigData = @{
    AllNodes = @(
        @{
            NodeName = 'MyVM1'
            Role = 'WebServer'
        },
        @{
            NodeName = 'MyVM2'
            Role = 'SQLServer'
        },
        @{
            NodeName = 'MyVM3'
            Role = 'WebServer'
        }
    )

    NonNodeData = @{
        SomeMessage = 'I love Azure Automation State Configuration and DSC!'
    }
}

Start-AzureRmAutomationDscCompilationJob -ResourceGroupName 'MyResourceGroup' -AutomationAccountName 'MyAutomationAccount' -ConfigurationName 'ConfigurationDataSample' -ConfigurationData $ConfigData
```

## <a name="assets"></a><span data-ttu-id="ed0d8-172">Assets</span><span class="sxs-lookup"><span data-stu-id="ed0d8-172">Assets</span></span>

<span data-ttu-id="ed0d8-173">Asset references are the same in Azure Automation State Configuration and runbooks.</span><span class="sxs-lookup"><span data-stu-id="ed0d8-173">Asset references are the same in Azure Automation State Configuration and runbooks.</span></span> <span data-ttu-id="ed0d8-174">See the following for more information:</span><span class="sxs-lookup"><span data-stu-id="ed0d8-174">See the following for more information:</span></span>

- [<span data-ttu-id="ed0d8-175">Certificates</span><span class="sxs-lookup"><span data-stu-id="ed0d8-175">Certificates</span></span>](automation-certificates.md)
- [<span data-ttu-id="ed0d8-176">Connections</span><span class="sxs-lookup"><span data-stu-id="ed0d8-176">Connections</span></span>](automation-connections.md)
- [<span data-ttu-id="ed0d8-177">Credentials</span><span class="sxs-lookup"><span data-stu-id="ed0d8-177">Credentials</span></span>](automation-credentials.md)
- [<span data-ttu-id="ed0d8-178">Variables</span><span class="sxs-lookup"><span data-stu-id="ed0d8-178">Variables</span></span>](automation-variables.md)

### <a name="credential-assets"></a><span data-ttu-id="ed0d8-179">Credential Assets</span><span class="sxs-lookup"><span data-stu-id="ed0d8-179">Credential Assets</span></span>

<span data-ttu-id="ed0d8-180">DSC configurations in Azure Automation can reference Automation credential assets using the `Get-AutomationPSCredential` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ed0d8-180">DSC configurations in Azure Automation can reference Automation credential assets using the `Get-AutomationPSCredential` cmdlet.</span></span> <span data-ttu-id="ed0d8-181">If a configuration has a parameter that has a **PSCredential** type, then you can use the `Get-AutomationPSCredential` cmdlet by passing the string name of an Azure Automation credential asset to the cmdlet to retrieve the credential.</span><span class="sxs-lookup"><span data-stu-id="ed0d8-181">If a configuration has a parameter that has a **PSCredential** type, then you can use the `Get-AutomationPSCredential` cmdlet by passing the string name of an Azure Automation credential asset to the cmdlet to retrieve the credential.</span></span> <span data-ttu-id="ed0d8-182">You can then use that object for the parameter requiring the **PSCredential** object.</span><span class="sxs-lookup"><span data-stu-id="ed0d8-182">You can then use that object for the parameter requiring the **PSCredential** object.</span></span> <span data-ttu-id="ed0d8-183">Behind the scenes, the Azure Automation credential asset with that name is retrieved and passed to the configuration.</span><span class="sxs-lookup"><span data-stu-id="ed0d8-183">Behind the scenes, the Azure Automation credential asset with that name is retrieved and passed to the configuration.</span></span> <span data-ttu-id="ed0d8-184">The example below shows this in action.</span><span class="sxs-lookup"><span data-stu-id="ed0d8-184">The example below shows this in action.</span></span>

<span data-ttu-id="ed0d8-185">Keeping credentials secure in node configurations (MOF configuration documents) requires encrypting the credentials in the node configuration MOF file.</span><span class="sxs-lookup"><span data-stu-id="ed0d8-185">Keeping credentials secure in node configurations (MOF configuration documents) requires encrypting the credentials in the node configuration MOF file.</span></span> <span data-ttu-id="ed0d8-186">However, currently you must tell PowerShell DSC it is okay for credentials to be outputted in plain text during node configuration MOF generation, because PowerShell DSC doesn’t know that Azure Automation will be encrypting the entire MOF file after its generation via a compilation job.</span><span class="sxs-lookup"><span data-stu-id="ed0d8-186">However, currently you must tell PowerShell DSC it is okay for credentials to be outputted in plain text during node configuration MOF generation, because PowerShell DSC doesn’t know that Azure Automation will be encrypting the entire MOF file after its generation via a compilation job.</span></span>

<span data-ttu-id="ed0d8-187">You can tell PowerShell DSC that it is okay for credentials to be outputted in plain text in the generated node configuration MOFs using [**ConfigurationData**](#configurationdata).</span><span class="sxs-lookup"><span data-stu-id="ed0d8-187">You can tell PowerShell DSC that it is okay for credentials to be outputted in plain text in the generated node configuration MOFs using [**ConfigurationData**](#configurationdata).</span></span> <span data-ttu-id="ed0d8-188">You should pass `PSDscAllowPlainTextPassword = $true` via **ConfigurationData** for each node block’s name that appears in the DSC configuration and uses credentials.</span><span class="sxs-lookup"><span data-stu-id="ed0d8-188">You should pass `PSDscAllowPlainTextPassword = $true` via **ConfigurationData** for each node block’s name that appears in the DSC configuration and uses credentials.</span></span>

<span data-ttu-id="ed0d8-189">The following example shows a DSC configuration that uses an Automation credential asset.</span><span class="sxs-lookup"><span data-stu-id="ed0d8-189">The following example shows a DSC configuration that uses an Automation credential asset.</span></span>

```powershell
Configuration CredentialSample
{
    Import-DscResource -ModuleName PSDesiredStateConfiguration
    $Cred = Get-AutomationPSCredential 'SomeCredentialAsset'

    Node $AllNodes.NodeName
    {
        File ExampleFile
        {
            SourcePath      = '\\Server\share\path\file.ext'
            DestinationPath = 'C:\destinationPath'
            Credential      = $Cred
        }
    }
}
```

<span data-ttu-id="ed0d8-190">You can compile the preceding DSC configuration with PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ed0d8-190">You can compile the preceding DSC configuration with PowerShell.</span></span> <span data-ttu-id="ed0d8-191">The following PowerShell adds two node configurations to the Azure Automation State Configuration Pull Server: **CredentialSample.MyVM1** and **CredentialSample.MyVM2**.</span><span class="sxs-lookup"><span data-stu-id="ed0d8-191">The following PowerShell adds two node configurations to the Azure Automation State Configuration Pull Server: **CredentialSample.MyVM1** and **CredentialSample.MyVM2**.</span></span>

```powershell
$ConfigData = @{
    AllNodes = @(
        @{
            NodeName = '*'
            PSDscAllowPlainTextPassword = $True
        },
        @{
            NodeName = 'MyVM1'
        },
        @{
            NodeName = 'MyVM2'
        }
    )
}

Start-AzureRmAutomationDscCompilationJob -ResourceGroupName 'MyResourceGroup' -AutomationAccountName 'MyAutomationAccount' -ConfigurationName 'CredentialSample' -ConfigurationData $ConfigData
```

> [!NOTE]
> <span data-ttu-id="ed0d8-192">When compilation is complete you may receive an error stating: **The 'Microsoft.PowerShell.Management' module was not imported because the 'Microsoft.PowerShell.Management' snap-in was already imported.**</span><span class="sxs-lookup"><span data-stu-id="ed0d8-192">When compilation is complete you may receive an error stating: **The 'Microsoft.PowerShell.Management' module was not imported because the 'Microsoft.PowerShell.Management' snap-in was already imported.**</span></span> <span data-ttu-id="ed0d8-193">This warning can safely be ignored.</span><span class="sxs-lookup"><span data-stu-id="ed0d8-193">This warning can safely be ignored.</span></span>

## <a name="importing-node-configurations"></a><span data-ttu-id="ed0d8-194">Importing node configurations</span><span class="sxs-lookup"><span data-stu-id="ed0d8-194">Importing node configurations</span></span>

<span data-ttu-id="ed0d8-195">You can also import node configurations (MOFs) that have been compiled outside of Azure.</span><span class="sxs-lookup"><span data-stu-id="ed0d8-195">You can also import node configurations (MOFs) that have been compiled outside of Azure.</span></span> <span data-ttu-id="ed0d8-196">One advantage of this is that node configurations can be signed.</span><span class="sxs-lookup"><span data-stu-id="ed0d8-196">One advantage of this is that node configurations can be signed.</span></span> <span data-ttu-id="ed0d8-197">A signed node configuration is verified locally on a managed node by the DSC agent, ensuring that the configuration being applied to the node comes from an authorized source.</span><span class="sxs-lookup"><span data-stu-id="ed0d8-197">A signed node configuration is verified locally on a managed node by the DSC agent, ensuring that the configuration being applied to the node comes from an authorized source.</span></span>

> [!NOTE]
> <span data-ttu-id="ed0d8-198">You can use import signed configurations into your Azure Automation account, but Azure Automation does not currently support compiling signed configurations.</span><span class="sxs-lookup"><span data-stu-id="ed0d8-198">You can use import signed configurations into your Azure Automation account, but Azure Automation does not currently support compiling signed configurations.</span></span>

> [!NOTE]
> <span data-ttu-id="ed0d8-199">A node configuration file must be no larger than 1 MB to allow it to be imported into Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="ed0d8-199">A node configuration file must be no larger than 1 MB to allow it to be imported into Azure Automation.</span></span>

<span data-ttu-id="ed0d8-200">For more information about how to sign node configurations, see [Improvements in WMF 5.1 - How to sign configuration and module](/powershell/wmf/5.1/dsc-improvements#dsc-module-and-configuration-signing-validations).</span><span class="sxs-lookup"><span data-stu-id="ed0d8-200">For more information about how to sign node configurations, see [Improvements in WMF 5.1 - How to sign configuration and module](/powershell/wmf/5.1/dsc-improvements#dsc-module-and-configuration-signing-validations).</span></span>

### <a name="importing-a-node-configuration-in-the-azure-portal"></a><span data-ttu-id="ed0d8-201">Importing a node configuration in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="ed0d8-201">Importing a node configuration in the Azure portal</span></span>

1. <span data-ttu-id="ed0d8-202">From your Automation account, click **State configuration (DSC)** under **Configuration Management**.</span><span class="sxs-lookup"><span data-stu-id="ed0d8-202">From your Automation account, click **State configuration (DSC)** under **Configuration Management**.</span></span>
1. <span data-ttu-id="ed0d8-203">In the **State configuration (DSC)** page, click on the **Configurations** tab, then click **+ Add**.</span><span class="sxs-lookup"><span data-stu-id="ed0d8-203">In the **State configuration (DSC)** page, click on the **Configurations** tab, then click **+ Add**.</span></span>
1. <span data-ttu-id="ed0d8-204">In the **Import** page, click the folder icon next to the **Node Configuration File** textbox to browse for a node configuration file (MOF) on your local computer.</span><span class="sxs-lookup"><span data-stu-id="ed0d8-204">In the **Import** page, click the folder icon next to the **Node Configuration File** textbox to browse for a node configuration file (MOF) on your local computer.</span></span>

   ![Browse for local file](./media/automation-dsc-compile/import-browse.png)

1. <span data-ttu-id="ed0d8-206">Enter a name in the **Configuration Name** textbox.</span><span class="sxs-lookup"><span data-stu-id="ed0d8-206">Enter a name in the **Configuration Name** textbox.</span></span> <span data-ttu-id="ed0d8-207">This name must match the name of the configuration from which the node configuration was compiled.</span><span class="sxs-lookup"><span data-stu-id="ed0d8-207">This name must match the name of the configuration from which the node configuration was compiled.</span></span>
1. <span data-ttu-id="ed0d8-208">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="ed0d8-208">Click **OK**.</span></span>

### <a name="importing-a-node-configuration-with-powershell"></a><span data-ttu-id="ed0d8-209">Importing a node configuration with PowerShell</span><span class="sxs-lookup"><span data-stu-id="ed0d8-209">Importing a node configuration with PowerShell</span></span>

<span data-ttu-id="ed0d8-210">You can use the [Import-AzureRmAutomationDscNodeConfiguration](/powershell/module/azurerm.automation/import-azurermautomationdscnodeconfiguration) cmdlet to import a node configuration into your automation account.</span><span class="sxs-lookup"><span data-stu-id="ed0d8-210">You can use the [Import-AzureRmAutomationDscNodeConfiguration](/powershell/module/azurerm.automation/import-azurermautomationdscnodeconfiguration) cmdlet to import a node configuration into your automation account.</span></span>

```powershell
Import-AzureRmAutomationDscNodeConfiguration -AutomationAccountName 'MyAutomationAccount' -ResourceGroupName 'MyResourceGroup' -ConfigurationName 'MyNodeConfiguration' -Path 'C:\MyConfigurations\TestVM1.mof'
```

## <a name="next-steps"></a><span data-ttu-id="ed0d8-211">Next steps</span><span class="sxs-lookup"><span data-stu-id="ed0d8-211">Next steps</span></span>

- <span data-ttu-id="ed0d8-212">To get started, see [Getting started with Azure Automation State Configuration](automation-dsc-getting-started.md)</span><span class="sxs-lookup"><span data-stu-id="ed0d8-212">To get started, see [Getting started with Azure Automation State Configuration](automation-dsc-getting-started.md)</span></span>
- <span data-ttu-id="ed0d8-213">To learn about compiling DSC configurations so that you can assign them to target nodes, see [Compiling configurations in Azure Automation State Configuration](automation-dsc-compile.md)</span><span class="sxs-lookup"><span data-stu-id="ed0d8-213">To learn about compiling DSC configurations so that you can assign them to target nodes, see [Compiling configurations in Azure Automation State Configuration](automation-dsc-compile.md)</span></span>
- <span data-ttu-id="ed0d8-214">For PowerShell cmdlet reference, see [Azure Automation State Configuration cmdlets](/powershell/module/azurerm.automation/#automation)</span><span class="sxs-lookup"><span data-stu-id="ed0d8-214">For PowerShell cmdlet reference, see [Azure Automation State Configuration cmdlets](/powershell/module/azurerm.automation/#automation)</span></span>
- <span data-ttu-id="ed0d8-215">For pricing information, see [Azure Automation State Configuration pricing](https://azure.microsoft.com/pricing/details/automation/)</span><span class="sxs-lookup"><span data-stu-id="ed0d8-215">For pricing information, see [Azure Automation State Configuration pricing](https://azure.microsoft.com/pricing/details/automation/)</span></span>
- <span data-ttu-id="ed0d8-216">To see an example of using Azure Automation State Configuration in a continuous deployment pipeline, see [Continuous Deployment Using Azure Automation State Configuration and Chocolatey](automation-dsc-cd-chocolatey.md)</span><span class="sxs-lookup"><span data-stu-id="ed0d8-216">To see an example of using Azure Automation State Configuration in a continuous deployment pipeline, see [Continuous Deployment Using Azure Automation State Configuration and Chocolatey](automation-dsc-cd-chocolatey.md)</span></span>