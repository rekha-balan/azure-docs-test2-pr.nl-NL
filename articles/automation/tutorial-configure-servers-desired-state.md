---
title: Configure servers to a desired state and manage drift with Azure Automation
description: Tutorial - Manage server configurations with Azure Automation State Configuration
services: automation
ms.service: automation
ms.component: dsc
author: DCtheGeek
ms.author: dacoulte
manager: carmonm
ms.topic: conceptual
ms.date: 08/08/2018
ms.openlocfilehash: 3b4ecc7596af52312785ea7acaad18a7af8a5087
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967712"
---
# <a name="configure-servers-to-a-desired-state-and-manage-drift"></a><span data-ttu-id="200c2-103">Configure servers to a desired state and manage drift</span><span class="sxs-lookup"><span data-stu-id="200c2-103">Configure servers to a desired state and manage drift</span></span>

<span data-ttu-id="200c2-104">Azure Automation State Configuration allows you to specify configurations for your servers and ensure that those servers are in the specified state over time.</span><span class="sxs-lookup"><span data-stu-id="200c2-104">Azure Automation State Configuration allows you to specify configurations for your servers and ensure that those servers are in the specified state over time.</span></span>

> [!div class="checklist"]
> - <span data-ttu-id="200c2-105">Onboard a VM to be managed by Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="200c2-105">Onboard a VM to be managed by Azure Automation DSC</span></span>
> - <span data-ttu-id="200c2-106">Upload a configuration to Azure Automation</span><span class="sxs-lookup"><span data-stu-id="200c2-106">Upload a configuration to Azure Automation</span></span>
> - <span data-ttu-id="200c2-107">Compile a configuration into a node configuration</span><span class="sxs-lookup"><span data-stu-id="200c2-107">Compile a configuration into a node configuration</span></span>
> - <span data-ttu-id="200c2-108">Assign a node configuration to a managed node</span><span class="sxs-lookup"><span data-stu-id="200c2-108">Assign a node configuration to a managed node</span></span>
> - <span data-ttu-id="200c2-109">Check the compliance status of a managed node</span><span class="sxs-lookup"><span data-stu-id="200c2-109">Check the compliance status of a managed node</span></span>

## <a name="prerequisites"></a><span data-ttu-id="200c2-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="200c2-110">Prerequisites</span></span>

<span data-ttu-id="200c2-111">To complete this tutorial, you will need:</span><span class="sxs-lookup"><span data-stu-id="200c2-111">To complete this tutorial, you will need:</span></span>

- <span data-ttu-id="200c2-112">An Azure Automation account.</span><span class="sxs-lookup"><span data-stu-id="200c2-112">An Azure Automation account.</span></span> <span data-ttu-id="200c2-113">For instructions on creating an Azure Automation Run As account, see [Azure Run As Account](automation-sec-configure-azure-runas-account.md).</span><span class="sxs-lookup"><span data-stu-id="200c2-113">For instructions on creating an Azure Automation Run As account, see [Azure Run As Account](automation-sec-configure-azure-runas-account.md).</span></span>
- <span data-ttu-id="200c2-114">An Azure Resource Manager VM (not Classic) running Windows Server 2008 R2 or later.</span><span class="sxs-lookup"><span data-stu-id="200c2-114">An Azure Resource Manager VM (not Classic) running Windows Server 2008 R2 or later.</span></span> <span data-ttu-id="200c2-115">For instructions on creating a VM, see [Create your first Windows virtual machine in the Azure portal](../virtual-machines/virtual-machines-windows-hero-tutorial.md)</span><span class="sxs-lookup"><span data-stu-id="200c2-115">For instructions on creating a VM, see [Create your first Windows virtual machine in the Azure portal](../virtual-machines/virtual-machines-windows-hero-tutorial.md)</span></span>
- <span data-ttu-id="200c2-116">Azure PowerShell module version 3.6 or later.</span><span class="sxs-lookup"><span data-stu-id="200c2-116">Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="200c2-117">Run `Get-Module -ListAvailable AzureRM` to find the version.</span><span class="sxs-lookup"><span data-stu-id="200c2-117">Run `Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="200c2-118">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="200c2-118">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>
- <span data-ttu-id="200c2-119">Familiarity with Desired State Configuration (DSC).</span><span class="sxs-lookup"><span data-stu-id="200c2-119">Familiarity with Desired State Configuration (DSC).</span></span> <span data-ttu-id="200c2-120">For information about DSC, see [Windows PowerShell Desired State Configuration Overview](https://docs.microsoft.com/powershell/dsc/overview)</span><span class="sxs-lookup"><span data-stu-id="200c2-120">For information about DSC, see [Windows PowerShell Desired State Configuration Overview](https://docs.microsoft.com/powershell/dsc/overview)</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="200c2-121">Log in to Azure</span><span class="sxs-lookup"><span data-stu-id="200c2-121">Log in to Azure</span></span>

<span data-ttu-id="200c2-122">Log in to your Azure subscription with the `Connect-AzureRmAccount` command and follow the on-screen directions.</span><span class="sxs-lookup"><span data-stu-id="200c2-122">Log in to your Azure subscription with the `Connect-AzureRmAccount` command and follow the on-screen directions.</span></span>

```powershell
Connect-AzureRmAccount
```

## <a name="create-and-upload-a-configuration-to-azure-automation"></a><span data-ttu-id="200c2-123">Create and upload a configuration to Azure Automation</span><span class="sxs-lookup"><span data-stu-id="200c2-123">Create and upload a configuration to Azure Automation</span></span>

<span data-ttu-id="200c2-124">For this tutorial, we will use a simple DSC configuration that ensures that IIS is installed on the VM.</span><span class="sxs-lookup"><span data-stu-id="200c2-124">For this tutorial, we will use a simple DSC configuration that ensures that IIS is installed on the VM.</span></span>

<span data-ttu-id="200c2-125">For information about DSC configurations, see [DSC configurations](/powershell/dsc/configurations).</span><span class="sxs-lookup"><span data-stu-id="200c2-125">For information about DSC configurations, see [DSC configurations](/powershell/dsc/configurations).</span></span>

<span data-ttu-id="200c2-126">In a text editor, type the following and save it locally as `TestConfig.ps1`.</span><span class="sxs-lookup"><span data-stu-id="200c2-126">In a text editor, type the following and save it locally as `TestConfig.ps1`.</span></span>

```powershell
configuration TestConfig {
   Node WebServer {
      WindowsFeature IIS {
         Ensure               = 'Present'
         Name                 = 'Web-Server'
         IncludeAllSubFeature = $true
      }
   }
}
```

<span data-ttu-id="200c2-127">Call the `Import-AzureRmAutomationDscConfiguration` cmdlet to upload the configuration into your Automation account:</span><span class="sxs-lookup"><span data-stu-id="200c2-127">Call the `Import-AzureRmAutomationDscConfiguration` cmdlet to upload the configuration into your Automation account:</span></span>

```powershell
 Import-AzureRmAutomationDscConfiguration -SourcePath 'C:\DscConfigs\TestConfig.ps1' -ResourceGroupName 'MyResourceGroup' -AutomationAccountName 'myAutomationAccount' -Published
```

## <a name="compile-a-configuration-into-a-node-configuration"></a><span data-ttu-id="200c2-128">Compile a configuration into a node configuration</span><span class="sxs-lookup"><span data-stu-id="200c2-128">Compile a configuration into a node configuration</span></span>

<span data-ttu-id="200c2-129">A DSC configuration must be compiled into a node configuration before it can be assigned to a node.</span><span class="sxs-lookup"><span data-stu-id="200c2-129">A DSC configuration must be compiled into a node configuration before it can be assigned to a node.</span></span>

<span data-ttu-id="200c2-130">For information about compiling configurations, see [DSC configurations](/powershell/dsc/configurations).</span><span class="sxs-lookup"><span data-stu-id="200c2-130">For information about compiling configurations, see [DSC configurations](/powershell/dsc/configurations).</span></span>

<span data-ttu-id="200c2-131">Call the `Start-AzureRmAutomationDscCompilationJob` cmdlet to compile the `TestConfig` configuration into a node configuration:</span><span class="sxs-lookup"><span data-stu-id="200c2-131">Call the `Start-AzureRmAutomationDscCompilationJob` cmdlet to compile the `TestConfig` configuration into a node configuration:</span></span>

```powershell
Start-AzureRmAutomationDscCompilationJob -ConfigurationName 'TestConfig' -ResourceGroupName 'MyResourceGroup' -AutomationAccountName 'myAutomationAccount'
```

<span data-ttu-id="200c2-132">This creates a node configuration named `TestConfig.WebServer` in your Automation account.</span><span class="sxs-lookup"><span data-stu-id="200c2-132">This creates a node configuration named `TestConfig.WebServer` in your Automation account.</span></span>

## <a name="register-a-vm-to-be-managed-by-state-configuration"></a><span data-ttu-id="200c2-133">Register a VM to be managed by State Configuration</span><span class="sxs-lookup"><span data-stu-id="200c2-133">Register a VM to be managed by State Configuration</span></span>

<span data-ttu-id="200c2-134">You can use Azure Automation State Configuration to manage Azure VMs (both Classic and Resource Manager), on-premises VMs, Linux machines, AWS VMs, and on-premises physical machines.</span><span class="sxs-lookup"><span data-stu-id="200c2-134">You can use Azure Automation State Configuration to manage Azure VMs (both Classic and Resource Manager), on-premises VMs, Linux machines, AWS VMs, and on-premises physical machines.</span></span> <span data-ttu-id="200c2-135">In this topic, we cover how to register only Azure Resource Manager VMs.</span><span class="sxs-lookup"><span data-stu-id="200c2-135">In this topic, we cover how to register only Azure Resource Manager VMs.</span></span> <span data-ttu-id="200c2-136">For information about registering other types of machines, see [Onboarding machines for management by Azure Automation State Configuration](automation-dsc-onboarding.md).</span><span class="sxs-lookup"><span data-stu-id="200c2-136">For information about registering other types of machines, see [Onboarding machines for management by Azure Automation State Configuration](automation-dsc-onboarding.md).</span></span>

<span data-ttu-id="200c2-137">Call the `Register-AzureRmAutomationDscNode` cmdlet to register your VM with Azure Automation State Configuration.</span><span class="sxs-lookup"><span data-stu-id="200c2-137">Call the `Register-AzureRmAutomationDscNode` cmdlet to register your VM with Azure Automation State Configuration.</span></span>

```powershell
Register-AzureRmAutomationDscNode -ResourceGroupName 'MyResourceGroup' -AutomationAccountName 'myAutomationAccount' -AzureVMName 'DscVm'
```

<span data-ttu-id="200c2-138">This registers the specified VM as a managed node in State Configuration.</span><span class="sxs-lookup"><span data-stu-id="200c2-138">This registers the specified VM as a managed node in State Configuration.</span></span>

### <a name="specify-configuration-mode-settings"></a><span data-ttu-id="200c2-139">Specify configuration mode settings</span><span class="sxs-lookup"><span data-stu-id="200c2-139">Specify configuration mode settings</span></span>

<span data-ttu-id="200c2-140">When you register a VM as a managed node, you can also specify properties of the configuration.</span><span class="sxs-lookup"><span data-stu-id="200c2-140">When you register a VM as a managed node, you can also specify properties of the configuration.</span></span> <span data-ttu-id="200c2-141">For example, you can specify that the state of the machine is to be applied only once (DSC does not attempt to apply the configuration after the initial check) by specifying `ApplyOnly` as the value of the **ConfigurationMode** property:</span><span class="sxs-lookup"><span data-stu-id="200c2-141">For example, you can specify that the state of the machine is to be applied only once (DSC does not attempt to apply the configuration after the initial check) by specifying `ApplyOnly` as the value of the **ConfigurationMode** property:</span></span>

```powershell
Register-AzureRmAutomationDscNode -ResourceGroupName 'MyResourceGroup' -AutomationAccountName 'myAutomationAccount' -AzureVMName 'DscVm' -ConfigurationMode 'ApplyOnly'
```

<span data-ttu-id="200c2-142">You can also specify how often DSC checks the configuration state by using the **ConfigurationModeFrequencyMins** property:</span><span class="sxs-lookup"><span data-stu-id="200c2-142">You can also specify how often DSC checks the configuration state by using the **ConfigurationModeFrequencyMins** property:</span></span>

```powershell
# Run a DSC check every 60 minutes
Register-AzureRmAutomationDscNode -ResourceGroupName 'MyResourceGroup' -AutomationAccountName 'myAutomationAccount' -AzureVMName 'DscVm' -ConfigurationModeFrequencyMins 60
```

<span data-ttu-id="200c2-143">For more information about setting configuration properties for a managed node, see [Register-AzureRmAutomationDscNode](/powershell/module/azurerm.automation/register-azurermautomationdscnode).</span><span class="sxs-lookup"><span data-stu-id="200c2-143">For more information about setting configuration properties for a managed node, see [Register-AzureRmAutomationDscNode](/powershell/module/azurerm.automation/register-azurermautomationdscnode).</span></span>

<span data-ttu-id="200c2-144">For more information about DSC configuration settings, see [Configuring the Local Configuration Manager](/powershell/dsc/metaconfig).</span><span class="sxs-lookup"><span data-stu-id="200c2-144">For more information about DSC configuration settings, see [Configuring the Local Configuration Manager](/powershell/dsc/metaconfig).</span></span>

## <a name="assign-a-node-configuration-to-a-managed-node"></a><span data-ttu-id="200c2-145">Assign a node configuration to a managed node</span><span class="sxs-lookup"><span data-stu-id="200c2-145">Assign a node configuration to a managed node</span></span>

<span data-ttu-id="200c2-146">Now we can assign the compiled node configuration to the VM we want to configure.</span><span class="sxs-lookup"><span data-stu-id="200c2-146">Now we can assign the compiled node configuration to the VM we want to configure.</span></span>

```powershell
# Get the ID of the DSC node
$node = Get-AzureRmAutomationDscNode -ResourceGroupName 'MyResourceGroup' -AutomationAccountName 'myAutomationAccount' -Name 'DscVm'

# Assign the node configuration to the DSC node
Set-AzureRmAutomationDscNode -ResourceGroupName 'MyResourceGroup' -AutomationAccountName 'myAutomationAccount' -NodeConfigurationName 'TestConfig.WebServer' -Id $node.Id
```

<span data-ttu-id="200c2-147">This assigns the node configuration named `TestConfig.WebServer` to the registered DSC node named `DscVm`.</span><span class="sxs-lookup"><span data-stu-id="200c2-147">This assigns the node configuration named `TestConfig.WebServer` to the registered DSC node named `DscVm`.</span></span>
<span data-ttu-id="200c2-148">By default, the DSC node is checked for compliance with the node configuration every 30 minutes.</span><span class="sxs-lookup"><span data-stu-id="200c2-148">By default, the DSC node is checked for compliance with the node configuration every 30 minutes.</span></span>
<span data-ttu-id="200c2-149">For information about how to change the compliance check interval, see [Configuring the Local Configuration Manager](/PowerShell/DSC/metaConfig).</span><span class="sxs-lookup"><span data-stu-id="200c2-149">For information about how to change the compliance check interval, see [Configuring the Local Configuration Manager](/PowerShell/DSC/metaConfig).</span></span>

## <a name="check-the-compliance-status-of-a-managed-node"></a><span data-ttu-id="200c2-150">Check the compliance status of a managed node</span><span class="sxs-lookup"><span data-stu-id="200c2-150">Check the compliance status of a managed node</span></span>

<span data-ttu-id="200c2-151">You can get reports on the compliance status of a managed node by calling the `Get-AzureRmAutomationDscNodeReport` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="200c2-151">You can get reports on the compliance status of a managed node by calling the `Get-AzureRmAutomationDscNodeReport` cmdlet:</span></span>

```powershell
# Get the ID of the DSC node
$node = Get-AzureRmAutomationDscNode -ResourceGroupName 'MyResourceGroup' -AutomationAccountName 'myAutomationAccount' -Name 'DscVm'

# Get an array of status reports for the DSC node
$reports = Get-AzureRmAutomationDscNodeReport -ResourceGroupName 'MyResourceGroup' -AutomationAccountName 'myAutomationAccount' -Id $node.Id

# Display the most recent report
$reports[0]
```

## <a name="next-steps"></a><span data-ttu-id="200c2-152">Next steps</span><span class="sxs-lookup"><span data-stu-id="200c2-152">Next steps</span></span>

- <span data-ttu-id="200c2-153">To get started, see [Getting started with Azure Automation State Configuration](automation-dsc-getting-started.md)</span><span class="sxs-lookup"><span data-stu-id="200c2-153">To get started, see [Getting started with Azure Automation State Configuration](automation-dsc-getting-started.md)</span></span>
- <span data-ttu-id="200c2-154">To learn how to onboard nodes, see [Onboarding machines for management by Azure Automation State Configuration](automation-dsc-onboarding.md)</span><span class="sxs-lookup"><span data-stu-id="200c2-154">To learn how to onboard nodes, see [Onboarding machines for management by Azure Automation State Configuration](automation-dsc-onboarding.md)</span></span>
- <span data-ttu-id="200c2-155">To learn about compiling DSC configurations so that you can assign them to target nodes, see [Compiling configurations in Azure Automation State Configuration](automation-dsc-compile.md)</span><span class="sxs-lookup"><span data-stu-id="200c2-155">To learn about compiling DSC configurations so that you can assign them to target nodes, see [Compiling configurations in Azure Automation State Configuration](automation-dsc-compile.md)</span></span>
- <span data-ttu-id="200c2-156">For PowerShell cmdlet reference, see [Azure Automation State Configuration cmdlets](/powershell/module/azurerm.automation/#automation)</span><span class="sxs-lookup"><span data-stu-id="200c2-156">For PowerShell cmdlet reference, see [Azure Automation State Configuration cmdlets](/powershell/module/azurerm.automation/#automation)</span></span>
- <span data-ttu-id="200c2-157">For pricing information, see [Azure Automation State Configuration pricing](https://azure.microsoft.com/pricing/details/automation/)</span><span class="sxs-lookup"><span data-stu-id="200c2-157">For pricing information, see [Azure Automation State Configuration pricing](https://azure.microsoft.com/pricing/details/automation/)</span></span>
- <span data-ttu-id="200c2-158">To see an example of using Azure Automation State Configuration in a continuous deployment pipeline, see [Continuous Deployment Using Azure Automation State Configuration and Chocolatey](automation-dsc-cd-chocolatey.md)</span><span class="sxs-lookup"><span data-stu-id="200c2-158">To see an example of using Azure Automation State Configuration in a continuous deployment pipeline, see [Continuous Deployment Using Azure Automation State Configuration and Chocolatey](automation-dsc-cd-chocolatey.md)</span></span>