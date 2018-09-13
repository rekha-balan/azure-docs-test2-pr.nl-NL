---
title: Compiling configurations in Azure Automation DSC | Microsoft Docs
description: This article describes how to compile Desired State Configuration (DSC) configurations for Azure Automation.
services: automation
documentationcenter: na
author: eslesar
manager: carmonm
ms.assetid: 49f20b31-4fa5-4712-b1c7-8f4409f1aecc
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: na
ms.date: 02/07/2017
ms.author: magoedte; eslesar
ms.openlocfilehash: 89d33ab3ad62c8ce5ca8e856450f2b4be71da010
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555373"
---
# <a name="compiling-configurations-in-azure-automation-dsc"></a><span data-ttu-id="8bd1f-103">Compiling configurations in Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="8bd1f-103">Compiling configurations in Azure Automation DSC</span></span>

<span data-ttu-id="8bd1f-104">You can compile Desired State Configuration (DSC) configurations in two ways with Azure Automation: in the Azure portal, and with Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8bd1f-104">You can compile Desired State Configuration (DSC) configurations in two ways with Azure Automation: in the Azure portal, and with Windows PowerShell.</span></span> <span data-ttu-id="8bd1f-105">The following table will help you determine when to use which method based on the characteristics of each:</span><span class="sxs-lookup"><span data-stu-id="8bd1f-105">The following table will help you determine when to use which method based on the characteristics of each:</span></span>

### <a name="azure-portal"></a><span data-ttu-id="8bd1f-106">Azure portal</span><span class="sxs-lookup"><span data-stu-id="8bd1f-106">Azure portal</span></span>

* <span data-ttu-id="8bd1f-107">Simplest method with interactive user interface</span><span class="sxs-lookup"><span data-stu-id="8bd1f-107">Simplest method with interactive user interface</span></span>
* <span data-ttu-id="8bd1f-108">Form to provide simple parameter values</span><span class="sxs-lookup"><span data-stu-id="8bd1f-108">Form to provide simple parameter values</span></span>
* <span data-ttu-id="8bd1f-109">Easily track job state</span><span class="sxs-lookup"><span data-stu-id="8bd1f-109">Easily track job state</span></span>
* <span data-ttu-id="8bd1f-110">Access authenticated with Azure logon</span><span class="sxs-lookup"><span data-stu-id="8bd1f-110">Access authenticated with Azure logon</span></span>

### <a name="windows-powershell"></a><span data-ttu-id="8bd1f-111">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="8bd1f-111">Windows PowerShell</span></span>

* <span data-ttu-id="8bd1f-112">Call from command line with Windows PowerShell cmdlets</span><span class="sxs-lookup"><span data-stu-id="8bd1f-112">Call from command line with Windows PowerShell cmdlets</span></span>
* <span data-ttu-id="8bd1f-113">Can be included in automated solution with multiple steps</span><span class="sxs-lookup"><span data-stu-id="8bd1f-113">Can be included in automated solution with multiple steps</span></span>
* <span data-ttu-id="8bd1f-114">Provide simple and complex parameter values</span><span class="sxs-lookup"><span data-stu-id="8bd1f-114">Provide simple and complex parameter values</span></span>
* <span data-ttu-id="8bd1f-115">Track job state</span><span class="sxs-lookup"><span data-stu-id="8bd1f-115">Track job state</span></span>
* <span data-ttu-id="8bd1f-116">Client required to support PowerShell cmdlets</span><span class="sxs-lookup"><span data-stu-id="8bd1f-116">Client required to support PowerShell cmdlets</span></span>
* <span data-ttu-id="8bd1f-117">Pass ConfigurationData</span><span class="sxs-lookup"><span data-stu-id="8bd1f-117">Pass ConfigurationData</span></span>
* <span data-ttu-id="8bd1f-118">Compile configurations that use credentials</span><span class="sxs-lookup"><span data-stu-id="8bd1f-118">Compile configurations that use credentials</span></span>

<span data-ttu-id="8bd1f-119">Once you have decided on a compilation method, you can follow the respective procedures below to start compiling.</span><span class="sxs-lookup"><span data-stu-id="8bd1f-119">Once you have decided on a compilation method, you can follow the respective procedures below to start compiling.</span></span>

## <a name="compiling-a-dsc-configuration-with-the-azure-portal"></a><span data-ttu-id="8bd1f-120">Compiling a DSC Configuration with the Azure portal</span><span class="sxs-lookup"><span data-stu-id="8bd1f-120">Compiling a DSC Configuration with the Azure portal</span></span>

1. <span data-ttu-id="8bd1f-121">From your Automation account, click **DSC Configurations**.</span><span class="sxs-lookup"><span data-stu-id="8bd1f-121">From your Automation account, click **DSC Configurations**.</span></span>
2. <span data-ttu-id="8bd1f-122">Click a configuration to open its blade.</span><span class="sxs-lookup"><span data-stu-id="8bd1f-122">Click a configuration to open its blade.</span></span>
3. <span data-ttu-id="8bd1f-123">Click **Compile**.</span><span class="sxs-lookup"><span data-stu-id="8bd1f-123">Click **Compile**.</span></span>
4. <span data-ttu-id="8bd1f-124">If the configuration has no parameters, you will be prompted to confirm whether you want to compile it.</span><span class="sxs-lookup"><span data-stu-id="8bd1f-124">If the configuration has no parameters, you will be prompted to confirm whether you want to compile it.</span></span> <span data-ttu-id="8bd1f-125">If the configuration has parameters, the **Compile Configuration** blade will open so you can provide parameter values.</span><span class="sxs-lookup"><span data-stu-id="8bd1f-125">If the configuration has parameters, the **Compile Configuration** blade will open so you can provide parameter values.</span></span> <span data-ttu-id="8bd1f-126">See the [**Basic Parameters**](#basic-parameters) section below for further details on parameters.</span><span class="sxs-lookup"><span data-stu-id="8bd1f-126">See the [**Basic Parameters**](#basic-parameters) section below for further details on parameters.</span></span>
5. <span data-ttu-id="8bd1f-127">The **Compilation Job** blade is opened so that you can track the compilation job's status, and the node configurations (MOF configuration documents) it caused to be placed on the Azure Automation DSC Pull Server.</span><span class="sxs-lookup"><span data-stu-id="8bd1f-127">The **Compilation Job** blade is opened so that you can track the compilation job's status, and the node configurations (MOF configuration documents) it caused to be placed on the Azure Automation DSC Pull Server.</span></span>

## <a name="compiling-a-dsc-configuration-with-windows-powershell"></a><span data-ttu-id="8bd1f-128">Compiling a DSC Configuration with Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="8bd1f-128">Compiling a DSC Configuration with Windows PowerShell</span></span>

<span data-ttu-id="8bd1f-129">You can use [`Start-AzureRmAutomationDscCompilationJob`](https://msdn.microsoft.com/library/mt244118.aspx) to start compiling with Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8bd1f-129">You can use [`Start-AzureRmAutomationDscCompilationJob`](https://msdn.microsoft.com/library/mt244118.aspx) to start compiling with Windows PowerShell.</span></span> <span data-ttu-id="8bd1f-130">The following sample code starts compilation of a DSC configuration called **SampleConfig**.</span><span class="sxs-lookup"><span data-stu-id="8bd1f-130">The following sample code starts compilation of a DSC configuration called **SampleConfig**.</span></span>

```powershell
Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "SampleConfig"
```

<span data-ttu-id="8bd1f-131">`Start-AzureRmAutomationDscCompilationJob` returns a compilation job object that you can use to track its status.</span><span class="sxs-lookup"><span data-stu-id="8bd1f-131">`Start-AzureRmAutomationDscCompilationJob` returns a compilation job object that you can use to track its status.</span></span> <span data-ttu-id="8bd1f-132">You can then use this compilation job object with [`Get-AzureRmAutomationDscCompilationJob`](https://msdn.microsoft.com/library/mt244120.aspx) to determine the status of the compilation job, and [`Get-AzureRmAutomationDscCompilationJobOutput`](https://msdn.microsoft.com/library/mt244103.aspx) to view its streams (output).</span><span class="sxs-lookup"><span data-stu-id="8bd1f-132">You can then use this compilation job object with [`Get-AzureRmAutomationDscCompilationJob`](https://msdn.microsoft.com/library/mt244120.aspx) to determine the status of the compilation job, and [`Get-AzureRmAutomationDscCompilationJobOutput`](https://msdn.microsoft.com/library/mt244103.aspx) to view its streams (output).</span></span> <span data-ttu-id="8bd1f-133">The following sample code starts compilation of the **SampleConfig** configuration, waits until it has completed, and then displays its streams.</span><span class="sxs-lookup"><span data-stu-id="8bd1f-133">The following sample code starts compilation of the **SampleConfig** configuration, waits until it has completed, and then displays its streams.</span></span>

```powershell
$CompilationJob = Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "SampleConfig"

while($CompilationJob.EndTime –eq $null -and $CompilationJob.Exception –eq $null)
{
    $CompilationJob = $CompilationJob | Get-AzureRmAutomationDscCompilationJob
    Start-Sleep -Seconds 3
}

$CompilationJob | Get-AzureRmAutomationDscCompilationJobOutput –Stream Any
```

## <a name="basic-parameters"></a><span data-ttu-id="8bd1f-134">Basic Parameters</span><span class="sxs-lookup"><span data-stu-id="8bd1f-134">Basic Parameters</span></span>
<span data-ttu-id="8bd1f-135">Parameter declaration in DSC configurations, including parameter types and properties, works the same as in Azure Automation runbooks.</span><span class="sxs-lookup"><span data-stu-id="8bd1f-135">Parameter declaration in DSC configurations, including parameter types and properties, works the same as in Azure Automation runbooks.</span></span> <span data-ttu-id="8bd1f-136">See [Starting a runbook in Azure Automation](automation-starting-a-runbook.md) to learn more about runbook parameters.</span><span class="sxs-lookup"><span data-stu-id="8bd1f-136">See [Starting a runbook in Azure Automation](automation-starting-a-runbook.md) to learn more about runbook parameters.</span></span>

<span data-ttu-id="8bd1f-137">The following example uses two parameters called **FeatureName** and **IsPresent**, to determine the values of properties in the **ParametersExample.sample** node configuration, generated during compilation.</span><span class="sxs-lookup"><span data-stu-id="8bd1f-137">The following example uses two parameters called **FeatureName** and **IsPresent**, to determine the values of properties in the **ParametersExample.sample** node configuration, generated during compilation.</span></span>

```powershell
Configuration ParametersExample
{
    param(
        [Parameter(Mandatory=$true)]

        [string] $FeatureName,

        [Parameter(Mandatory=$true)]
        [boolean] $IsPresent
    )

    $EnsureString = "Present"
    if($IsPresent -eq $false)
    {
        $EnsureString = "Absent"
    }

    Node "sample"
    {
        WindowsFeature ($FeatureName + "Feature")
        {
            Ensure = $EnsureString
            Name = $FeatureName
        }
    }
}
```

<span data-ttu-id="8bd1f-138">You can compile DSC Configurations that use basic parameters in the Azure Automation DSC portal, or with Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="8bd1f-138">You can compile DSC Configurations that use basic parameters in the Azure Automation DSC portal, or with Azure PowerShell:</span></span>

### <a name="portal"></a><span data-ttu-id="8bd1f-139">Portal</span><span class="sxs-lookup"><span data-stu-id="8bd1f-139">Portal</span></span>

<span data-ttu-id="8bd1f-140">In the portal, you can enter parameter values after clicking **Compile**.</span><span class="sxs-lookup"><span data-stu-id="8bd1f-140">In the portal, you can enter parameter values after clicking **Compile**.</span></span>

![alt text](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-dsc-compile/DSC_compiling_1.png)

### <a name="powershell"></a><span data-ttu-id="8bd1f-142">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8bd1f-142">PowerShell</span></span>

<span data-ttu-id="8bd1f-143">PowerShell requires parameters in a [hashtable](http://technet.microsoft.com/library/hh847780.aspx) where the key matches the parameter name, and the value equals the parameter value.</span><span class="sxs-lookup"><span data-stu-id="8bd1f-143">PowerShell requires parameters in a [hashtable](http://technet.microsoft.com/library/hh847780.aspx) where the key matches the parameter name, and the value equals the parameter value.</span></span>

```powershell
$Parameters = @{
    "FeatureName" = "Web-Server"
    "IsPresent" = $False
}

Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "ParametersExample" -Parameters $Parameters
```

<span data-ttu-id="8bd1f-144">For information about passing PSCredentials as parameters, see <a href="#credential-assets">**Credential Assets**</a> below.</span><span class="sxs-lookup"><span data-stu-id="8bd1f-144">For information about passing PSCredentials as parameters, see <a href="#credential-assets">**Credential Assets**</a> below.</span></span>

## <a name="configurationdata"></a><span data-ttu-id="8bd1f-145">ConfigurationData</span><span class="sxs-lookup"><span data-stu-id="8bd1f-145">ConfigurationData</span></span>
<span data-ttu-id="8bd1f-146">**ConfigurationData** allows you to separate structural configuration from any environment specific configuration while using PowerShell DSC.</span><span class="sxs-lookup"><span data-stu-id="8bd1f-146">**ConfigurationData** allows you to separate structural configuration from any environment specific configuration while using PowerShell DSC.</span></span> <span data-ttu-id="8bd1f-147">See [Separating "What" from "Where" in PowerShell DSC](http://blogs.msdn.com/b/powershell/archive/2014/01/09/continuous-deployment-using-dsc-with-minimal-change.aspx) to learn more about **ConfigurationData**.</span><span class="sxs-lookup"><span data-stu-id="8bd1f-147">See [Separating "What" from "Where" in PowerShell DSC](http://blogs.msdn.com/b/powershell/archive/2014/01/09/continuous-deployment-using-dsc-with-minimal-change.aspx) to learn more about **ConfigurationData**.</span></span>

> [!NOTE]
> <span data-ttu-id="8bd1f-148">You can use **ConfigurationData** when compiling in Azure Automation DSC using Azure PowerShell, but not in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="8bd1f-148">You can use **ConfigurationData** when compiling in Azure Automation DSC using Azure PowerShell, but not in the Azure portal.</span></span>

<span data-ttu-id="8bd1f-149">The following example DSC configuration uses **ConfigurationData** via the **$ConfigurationData** and **$AllNodes** keywords.</span><span class="sxs-lookup"><span data-stu-id="8bd1f-149">The following example DSC configuration uses **ConfigurationData** via the **$ConfigurationData** and **$AllNodes** keywords.</span></span> <span data-ttu-id="8bd1f-150">You'll also need the [**xWebAdministration** module](https://www.powershellgallery.com/packages/xWebAdministration/) for this example:</span><span class="sxs-lookup"><span data-stu-id="8bd1f-150">You'll also need the [**xWebAdministration** module](https://www.powershellgallery.com/packages/xWebAdministration/) for this example:</span></span>

```powershell
Configuration ConfigurationDataSample
{
    Import-DscResource -ModuleName xWebAdministration -Name MSFT_xWebsite

    Write-Verbose $ConfigurationData.NonNodeData.SomeMessage

    Node $AllNodes.Where{$_.Role -eq "WebServer"}.NodeName
    {
        xWebsite Site
        {
            Name = $Node.SiteName
            PhysicalPath = $Node.SiteContents
            Ensure   = "Present"
        }
    }
}
```

<span data-ttu-id="8bd1f-151">You can compile the DSC configuration above with PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8bd1f-151">You can compile the DSC configuration above with PowerShell.</span></span> <span data-ttu-id="8bd1f-152">The below PowerShell adds two node configurations to the Azure Automation DSC Pull Server: **ConfigurationDataSample.MyVM1** and **ConfigurationDataSample.MyVM3**:</span><span class="sxs-lookup"><span data-stu-id="8bd1f-152">The below PowerShell adds two node configurations to the Azure Automation DSC Pull Server: **ConfigurationDataSample.MyVM1** and **ConfigurationDataSample.MyVM3**:</span></span>

```powershell
$ConfigData = @{
    AllNodes = @(
        @{
            NodeName = "MyVM1"
            Role = "WebServer"
        },
        @{
            NodeName = "MyVM2"
            Role = "SQLServer"
        },
        @{
            NodeName = "MyVM3"
            Role = "WebServer"
        }
    )

    NonNodeData = @{
        SomeMessage = "I love Azure Automation DSC!"
    }
}

Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "ConfigurationDataSample" -ConfigurationData $ConfigData
```

## <a name="assets"></a><span data-ttu-id="8bd1f-153">Assets</span><span class="sxs-lookup"><span data-stu-id="8bd1f-153">Assets</span></span>

<span data-ttu-id="8bd1f-154">Asset references are the same in Azure Automation DSC configurations and runbooks.</span><span class="sxs-lookup"><span data-stu-id="8bd1f-154">Asset references are the same in Azure Automation DSC configurations and runbooks.</span></span> <span data-ttu-id="8bd1f-155">See the following for more information:</span><span class="sxs-lookup"><span data-stu-id="8bd1f-155">See the following for more information:</span></span>

* [<span data-ttu-id="8bd1f-156">Certificates</span><span class="sxs-lookup"><span data-stu-id="8bd1f-156">Certificates</span></span>](automation-certificates.md)
* [<span data-ttu-id="8bd1f-157">Connections</span><span class="sxs-lookup"><span data-stu-id="8bd1f-157">Connections</span></span>](automation-connections.md)
* [<span data-ttu-id="8bd1f-158">Credentials</span><span class="sxs-lookup"><span data-stu-id="8bd1f-158">Credentials</span></span>](automation-credentials.md)
* [<span data-ttu-id="8bd1f-159">Variables</span><span class="sxs-lookup"><span data-stu-id="8bd1f-159">Variables</span></span>](automation-variables.md)

### <a name="credential-assets"></a><span data-ttu-id="8bd1f-160">Credential Assets</span><span class="sxs-lookup"><span data-stu-id="8bd1f-160">Credential Assets</span></span>

<span data-ttu-id="8bd1f-161">While DSC configurations in Azure Automation can reference credential assets using **Get-AzureRmAutomationCredential**, credential assets can also be passed in via parameters, if desired.</span><span class="sxs-lookup"><span data-stu-id="8bd1f-161">While DSC configurations in Azure Automation can reference credential assets using **Get-AzureRmAutomationCredential**, credential assets can also be passed in via parameters, if desired.</span></span> <span data-ttu-id="8bd1f-162">If a configuration takes a parameter of **PSCredential** type, then you need to pass the string name of an Azure Automation credential asset as that parameter’s value, rather than a PSCredential object.</span><span class="sxs-lookup"><span data-stu-id="8bd1f-162">If a configuration takes a parameter of **PSCredential** type, then you need to pass the string name of an Azure Automation credential asset as that parameter’s value, rather than a PSCredential object.</span></span> <span data-ttu-id="8bd1f-163">Behind the scenes, the Azure Automation credential asset with that name will be retrieved and passed to the configuration.</span><span class="sxs-lookup"><span data-stu-id="8bd1f-163">Behind the scenes, the Azure Automation credential asset with that name will be retrieved and passed to the configuration.</span></span>

<span data-ttu-id="8bd1f-164">Keeping credentials secure in node configurations (MOF configuration documents) requires encrypting the credentials in the node configuration MOF file.</span><span class="sxs-lookup"><span data-stu-id="8bd1f-164">Keeping credentials secure in node configurations (MOF configuration documents) requires encrypting the credentials in the node configuration MOF file.</span></span> <span data-ttu-id="8bd1f-165">Azure Automation takes this one step further and encrypts the entire MOF file.</span><span class="sxs-lookup"><span data-stu-id="8bd1f-165">Azure Automation takes this one step further and encrypts the entire MOF file.</span></span> <span data-ttu-id="8bd1f-166">However, currently you must tell PowerShell DSC it is okay for credentials to be outputted in plain text during node configuration MOF generation, because PowerShell DSC doesn’t know that Azure Automation will be encrypting the entire MOF file after its generation via a compilation job.</span><span class="sxs-lookup"><span data-stu-id="8bd1f-166">However, currently you must tell PowerShell DSC it is okay for credentials to be outputted in plain text during node configuration MOF generation, because PowerShell DSC doesn’t know that Azure Automation will be encrypting the entire MOF file after its generation via a compilation job.</span></span>

<span data-ttu-id="8bd1f-167">You can tell PowerShell DSC that it is okay for credentials to be outputted in plain text in the generated node configuration MOFs using [**ConfigurationData**](#configurationdata).</span><span class="sxs-lookup"><span data-stu-id="8bd1f-167">You can tell PowerShell DSC that it is okay for credentials to be outputted in plain text in the generated node configuration MOFs using [**ConfigurationData**](#configurationdata).</span></span> <span data-ttu-id="8bd1f-168">You should pass `PSDscAllowPlainTextPassword = $true` via **ConfigurationData** for each node block’s name that appears in the DSC configuration and uses credentials.</span><span class="sxs-lookup"><span data-stu-id="8bd1f-168">You should pass `PSDscAllowPlainTextPassword = $true` via **ConfigurationData** for each node block’s name that appears in the DSC configuration and uses credentials.</span></span>

<span data-ttu-id="8bd1f-169">The following example shows a DSC configuration that uses an Automation credential asset.</span><span class="sxs-lookup"><span data-stu-id="8bd1f-169">The following example shows a DSC configuration that uses an Automation credential asset.</span></span>

```powershell
Configuration CredentialSample
{
    $Cred = Get-AzureRmAutomationCredential -ResourceGroupName "ResourceGroup01" -AutomationAccountName "AutomationAcct" -Name "SomeCredentialAsset"

    Node $AllNodes.NodeName
    {
        File ExampleFile
        {
            SourcePath = "\\Server\share\path\file.ext"
            DestinationPath = "C:\destinationPath"
            Credential = $Cred
        }
    }
}
```

<span data-ttu-id="8bd1f-170">You can compile the DSC configuration above with PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8bd1f-170">You can compile the DSC configuration above with PowerShell.</span></span> <span data-ttu-id="8bd1f-171">The below PowerShell adds two node configurations to the Azure Automation DSC Pull Server:  **CredentialSample.MyVM1** and **CredentialSample.MyVM2**.</span><span class="sxs-lookup"><span data-stu-id="8bd1f-171">The below PowerShell adds two node configurations to the Azure Automation DSC Pull Server:  **CredentialSample.MyVM1** and **CredentialSample.MyVM2**.</span></span>

```powershell
$ConfigData = @{
    AllNodes = @(
        @{
            NodeName = "*"
            PSDscAllowPlainTextPassword = $True
        },
        @{
            NodeName = "MyVM1"
        },
        @{
            NodeName = "MyVM2"
        }
    )
}

Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "CredentialSample" -ConfigurationData $ConfigData
```

## <a name="importing-node-configurations"></a><span data-ttu-id="8bd1f-172">Importing node configurations</span><span class="sxs-lookup"><span data-stu-id="8bd1f-172">Importing node configurations</span></span>

<span data-ttu-id="8bd1f-173">You can also import node configuratons (MOFs) that you have compiled outside of Azure.</span><span class="sxs-lookup"><span data-stu-id="8bd1f-173">You can also import node configuratons (MOFs) that you have compiled outside of Azure.</span></span> <span data-ttu-id="8bd1f-174">One advantage of this is that node confiturations can be signed.</span><span class="sxs-lookup"><span data-stu-id="8bd1f-174">One advantage of this is that node confiturations can be signed.</span></span>
<span data-ttu-id="8bd1f-175">A signed node configuration is verified locally on a managed node by the DSC agent, ensuring that the configuration being applied to the node comes from an authorized source.</span><span class="sxs-lookup"><span data-stu-id="8bd1f-175">A signed node configuration is verified locally on a managed node by the DSC agent, ensuring that the configuration being applied to the node comes from an authorized source.</span></span>

> [!NOTE]
> <span data-ttu-id="8bd1f-176">You can use import signed configurations into your Azure Automation account, but Azure Automation does not currently support compiling signed configurations.</span><span class="sxs-lookup"><span data-stu-id="8bd1f-176">You can use import signed configurations into your Azure Automation account, but Azure Automation does not currently support compiling signed configurations.</span></span>

> [!NOTE]
> <span data-ttu-id="8bd1f-177">A node configuration file must be no larger than 1 MB to allow it to be imported into Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="8bd1f-177">A node configuration file must be no larger than 1 MB to allow it to be imported into Azure Automation.</span></span>

<span data-ttu-id="8bd1f-178">You can learn how to sign node configurations at https://msdn.microsoft.com/en-us/powershell/wmf/5.1/dsc-improvements#how-to-sign-configuration-and-module.</span><span class="sxs-lookup"><span data-stu-id="8bd1f-178">You can learn how to sign node configurations at https://msdn.microsoft.com/en-us/powershell/wmf/5.1/dsc-improvements#how-to-sign-configuration-and-module.</span></span>

### <a name="importing-a-node-configuration-in-the-azure-portal"></a><span data-ttu-id="8bd1f-179">Importing a node configuration in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="8bd1f-179">Importing a node configuration in the Azure portal</span></span>

1. <span data-ttu-id="8bd1f-180">From your Automation account, click **DSC node configurations**.</span><span class="sxs-lookup"><span data-stu-id="8bd1f-180">From your Automation account, click **DSC node configurations**.</span></span>

    ![DSC node configurations](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-dsc-compile/node-config.png)
2. <span data-ttu-id="8bd1f-182">In the **DSC node configurations** blade, click **Add a NodeConfiguration**.</span><span class="sxs-lookup"><span data-stu-id="8bd1f-182">In the **DSC node configurations** blade, click **Add a NodeConfiguration**.</span></span>
3. <span data-ttu-id="8bd1f-183">In the **Import** blade, click the folder icon next to the **Node Configuration File** textbox to browse for a node configuration file (MOF) on your local computer.</span><span class="sxs-lookup"><span data-stu-id="8bd1f-183">In the **Import** blade, click the folder icon next to the **Node Configuration File** textbox to browse for a node configuration file (MOF) on your local computer.</span></span>

    ![Browse for local file](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-dsc-compile/import-browse.png)
4. <span data-ttu-id="8bd1f-185">Enter a name in the **Configuration Name** textbox.</span><span class="sxs-lookup"><span data-stu-id="8bd1f-185">Enter a name in the **Configuration Name** textbox.</span></span> <span data-ttu-id="8bd1f-186">This name must match the name of the configuration from which the node configuration was compiled.</span><span class="sxs-lookup"><span data-stu-id="8bd1f-186">This name must match the name of the configuration from which the node configuration was compiled.</span></span>
5. <span data-ttu-id="8bd1f-187">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="8bd1f-187">Click **OK**.</span></span>

### <a name="importing-a-node-configuration-with-powershell"></a><span data-ttu-id="8bd1f-188">Importing a node configuration with PowerShell</span><span class="sxs-lookup"><span data-stu-id="8bd1f-188">Importing a node configuration with PowerShell</span></span>

<span data-ttu-id="8bd1f-189">You can use the [Import-AzureRmAutomationDscNodeConfiguration](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.automation/v1.0.12/import-azurermautomationdscnodeconfiguration) cmdlet to import a node configuration into your automation account.</span><span class="sxs-lookup"><span data-stu-id="8bd1f-189">You can use the [Import-AzureRmAutomationDscNodeConfiguration](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.automation/v1.0.12/import-azurermautomationdscnodeconfiguration) cmdlet to import a node configuration into your automation account.</span></span>

```powershell
Import-AzureRmAutomationDscNodeConfiguration -AutomationAccountName "MyAutomationAccount" -ResourceGroupName "MyResourceGroup" -ConfigurationName "MyNodeConfiguration" -Path "C:\MyConfigurations\TestVM1.mof"
```






