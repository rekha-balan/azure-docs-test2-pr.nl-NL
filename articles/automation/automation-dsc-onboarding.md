---
title: Onboarding machines for management by Azure Automation DSC | Microsoft Docs
description: How to setup machines for management with Azure Automation DSC
services: automation
documentationcenter: dev-center-name
author: eslesar
manager: carmonm
ms.assetid: da13e1f5-2a1c-443b-8e3b-9f0d6f9e4810
ms.service: automation
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: TBD
ms.date: 12/13/2016
ms.author: eslesar
ms.openlocfilehash: 94441a6edeec776eb1551a0b640b6b3a5970cf34
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563734"
---
# <a name="onboarding-machines-for-management-by-azure-automation-dsc"></a><span data-ttu-id="e1401-103">Onboarding machines for management by Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="e1401-103">Onboarding machines for management by Azure Automation DSC</span></span>

## <a name="why-manage-machines-with-azure-automation-dsc"></a><span data-ttu-id="e1401-104">Why manage machines with Azure Automation DSC?</span><span class="sxs-lookup"><span data-stu-id="e1401-104">Why manage machines with Azure Automation DSC?</span></span>

<span data-ttu-id="e1401-105">Like [PowerShell Desired State Configuration](https://technet.microsoft.com/library/dn249912.aspx), Azure Automation Desired State Configuration is a simple, yet powerful, configuration management service for DSC nodes (physical and virtual machines) in any cloud or on-premises datacenter.</span><span class="sxs-lookup"><span data-stu-id="e1401-105">Like [PowerShell Desired State Configuration](https://technet.microsoft.com/library/dn249912.aspx), Azure Automation Desired State Configuration is a simple, yet powerful, configuration management service for DSC nodes (physical and virtual machines) in any cloud or on-premises datacenter.</span></span> <span data-ttu-id="e1401-106">It enables scalability across thousands of machines quickly and easily from a central, secure location.</span><span class="sxs-lookup"><span data-stu-id="e1401-106">It enables scalability across thousands of machines quickly and easily from a central, secure location.</span></span> <span data-ttu-id="e1401-107">You can easily onboard machines, assign them declarative configurations, and view reports showing each machine's compliance to the desired state you specified.</span><span class="sxs-lookup"><span data-stu-id="e1401-107">You can easily onboard machines, assign them declarative configurations, and view reports showing each machine's compliance to the desired state you specified.</span></span> <span data-ttu-id="e1401-108">The Azure Automation DSC management layer is to DSC what the Azure Automation management layer is to PowerShell scripting.</span><span class="sxs-lookup"><span data-stu-id="e1401-108">The Azure Automation DSC management layer is to DSC what the Azure Automation management layer is to PowerShell scripting.</span></span> <span data-ttu-id="e1401-109">In other words, in the same way that Azure Automation helps you manage PowerShell scripts, it also helps you manage DSC configurations.</span><span class="sxs-lookup"><span data-stu-id="e1401-109">In other words, in the same way that Azure Automation helps you manage PowerShell scripts, it also helps you manage DSC configurations.</span></span> <span data-ttu-id="e1401-110">To learn more about the benefits of using Azure Automation DSC, see [Azure Automation DSC overview](automation-dsc-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e1401-110">To learn more about the benefits of using Azure Automation DSC, see [Azure Automation DSC overview](automation-dsc-overview.md).</span></span>

<span data-ttu-id="e1401-111">Azure Automation DSC can be used to manage a variety of machines:</span><span class="sxs-lookup"><span data-stu-id="e1401-111">Azure Automation DSC can be used to manage a variety of machines:</span></span>

* <span data-ttu-id="e1401-112">Azure virtual machines (classic)</span><span class="sxs-lookup"><span data-stu-id="e1401-112">Azure virtual machines (classic)</span></span>
* <span data-ttu-id="e1401-113">Azure virtual machines</span><span class="sxs-lookup"><span data-stu-id="e1401-113">Azure virtual machines</span></span>
* <span data-ttu-id="e1401-114">Amazon Web Services (AWS) virtual machines</span><span class="sxs-lookup"><span data-stu-id="e1401-114">Amazon Web Services (AWS) virtual machines</span></span>
* <span data-ttu-id="e1401-115">Physical/virtual Windows machines on-premises, or in a cloud other than Azure/AWS</span><span class="sxs-lookup"><span data-stu-id="e1401-115">Physical/virtual Windows machines on-premises, or in a cloud other than Azure/AWS</span></span>
* <span data-ttu-id="e1401-116">Physical/virtual Linux machines on-premises, in Azure, or in a cloud other than Azure</span><span class="sxs-lookup"><span data-stu-id="e1401-116">Physical/virtual Linux machines on-premises, in Azure, or in a cloud other than Azure</span></span>

<span data-ttu-id="e1401-117">In addition, if you are not ready to manage machine configuration from the cloud, Azure Automation DSC can also be used as a report-only endpoint.</span><span class="sxs-lookup"><span data-stu-id="e1401-117">In addition, if you are not ready to manage machine configuration from the cloud, Azure Automation DSC can also be used as a report-only endpoint.</span></span> <span data-ttu-id="e1401-118">This allows you to set (push) desired configuration through DSC on-premises and view rich reporting details on node compliance with the desired state in Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="e1401-118">This allows you to set (push) desired configuration through DSC on-premises and view rich reporting details on node compliance with the desired state in Azure Automation.</span></span>

<span data-ttu-id="e1401-119">The following sections outline how you can onboard each type of machine to Azure Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="e1401-119">The following sections outline how you can onboard each type of machine to Azure Automation DSC.</span></span>

## <a name="azure-virtual-machines-classic"></a><span data-ttu-id="e1401-120">Azure virtual machines (classic)</span><span class="sxs-lookup"><span data-stu-id="e1401-120">Azure virtual machines (classic)</span></span>

<span data-ttu-id="e1401-121">With Azure Automation DSC, you can easily onboard Azure virtual machines (classic) for configuration management using either the Azure portal, or PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e1401-121">With Azure Automation DSC, you can easily onboard Azure virtual machines (classic) for configuration management using either the Azure portal, or PowerShell.</span></span> <span data-ttu-id="e1401-122">Under the hood, and without an administrator having to remote into the VM, the Azure VM Desired State Configuration extension registers the VM with Azure Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="e1401-122">Under the hood, and without an administrator having to remote into the VM, the Azure VM Desired State Configuration extension registers the VM with Azure Automation DSC.</span></span> <span data-ttu-id="e1401-123">Since the Azure VM Desired State Configuration extension runs asynchronously, steps to track its progress or troubleshoot it are provided in the [**Troubleshooting Azure virtual machine onboarding**](#troubleshooting-azure-virtual-machine-onboarding) section below.</span><span class="sxs-lookup"><span data-stu-id="e1401-123">Since the Azure VM Desired State Configuration extension runs asynchronously, steps to track its progress or troubleshoot it are provided in the [**Troubleshooting Azure virtual machine onboarding**](#troubleshooting-azure-virtual-machine-onboarding) section below.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="e1401-124">Azure portal</span><span class="sxs-lookup"><span data-stu-id="e1401-124">Azure portal</span></span>

<span data-ttu-id="e1401-125">In the [Azure portal](http://portal.azure.com/), click **Browse** -> **Virtual machines (classic)**.</span><span class="sxs-lookup"><span data-stu-id="e1401-125">In the [Azure portal](http://portal.azure.com/), click **Browse** -> **Virtual machines (classic)**.</span></span> <span data-ttu-id="e1401-126">Select the Windows VM you want to onboard.</span><span class="sxs-lookup"><span data-stu-id="e1401-126">Select the Windows VM you want to onboard.</span></span> <span data-ttu-id="e1401-127">On the virtual machine's dashboard blade, click **All settings** -> **Extensions** -> **Add** -> **Azure Automation DSC** -> **Create**.</span><span class="sxs-lookup"><span data-stu-id="e1401-127">On the virtual machine's dashboard blade, click **All settings** -> **Extensions** -> **Add** -> **Azure Automation DSC** -> **Create**.</span></span> <span data-ttu-id="e1401-128">Enter the [PowerShell DSC Local Configuration Manager values](https://msdn.microsoft.com/powershell/dsc/metaconfig4) required for your use case, your Automation account's registration key and registration URL, and optionally a node configuration to assign to the VM.</span><span class="sxs-lookup"><span data-stu-id="e1401-128">Enter the [PowerShell DSC Local Configuration Manager values](https://msdn.microsoft.com/powershell/dsc/metaconfig4) required for your use case, your Automation account's registration key and registration URL, and optionally a node configuration to assign to the VM.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-dsc-onboarding/DSC_Onboarding_1.png)

<span data-ttu-id="e1401-129">To find the registration URL and key for the Automation account to onboard the machine to, see the [**Secure registration**](#secure-registration) section below.</span><span class="sxs-lookup"><span data-stu-id="e1401-129">To find the registration URL and key for the Automation account to onboard the machine to, see the [**Secure registration**](#secure-registration) section below.</span></span>

### <a name="powershell"></a><span data-ttu-id="e1401-130">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e1401-130">PowerShell</span></span>

```powershell
# log in to both Azure Service Management and Azure Resource Manager
Add-AzureAccount
Add-AzureRmAccount

# fill in correct values for your VM/Automation account here
$VMName = ""
$ServiceName = ""
$AutomationAccountName = ""
$AutomationAccountResourceGroup = ""

# fill in the name of a Node Configuration in Azure Automation DSC, for this VM to conform to
$NodeConfigName = ""

# get Azure Automation DSC registration info
$Account = Get-AzureRmAutomationAccount -ResourceGroupName $AutomationAccountResourceGroup -Name $AutomationAccountName
$RegistrationInfo = $Account | Get-AzureRmAutomationRegistrationInfo

# use the DSC extension to onboard the VM for management with Azure Automation DSC
$VM = Get-AzureVM -Name $VMName -ServiceName $ServiceName

$PublicConfiguration = ConvertTo-Json -Depth 8 @{
    SasToken = ""
    ModulesUrl = "https://eus2oaasibizamarketprod1.blob.core.windows.net/automationdscpreview/RegistrationMetaConfigV2.zip"
    ConfigurationFunction = "RegistrationMetaConfigV2.ps1\RegistrationMetaConfigV2"

# update these PowerShell DSC Local Configuration Manager defaults if they do not match your use case.
# See https://technet.microsoft.com/library/dn249922.aspx?f=255&MSPPError=-2147217396 for more details
    Properties = @{
    RegistrationKey = @{
        UserName = 'notused'
        Password = 'PrivateSettingsRef:RegistrationKey'
    }
    RegistrationUrl = $RegistrationInfo.Endpoint
    NodeConfigurationName = $NodeConfigName
    ConfigurationMode = "ApplyAndMonitor"
    ConfigurationModeFrequencyMins = 15
    RefreshFrequencyMins = 30
    RebootNodeIfNeeded = $False
    ActionAfterReboot = "ContinueConfiguration"
    AllowModuleOverwrite = $False
    }
}

$PrivateConfiguration = ConvertTo-Json -Depth 8 @{
    Items = @{
        RegistrationKey = $RegistrationInfo.PrimaryKey
    }
}

$VM = Set-AzureVMExtension `
    -VM $vm `
    -Publisher Microsoft.Powershell `
    -ExtensionName DSC `
    -Version 2.19 `
    -PublicConfiguration $PublicConfiguration `
    -PrivateConfiguration $PrivateConfiguration `
    -ForceUpdate

$VM | Update-AzureVM
```

## <a name="azure-virtual-machines"></a><span data-ttu-id="e1401-131">Azure virtual machines</span><span class="sxs-lookup"><span data-stu-id="e1401-131">Azure virtual machines</span></span>

<span data-ttu-id="e1401-132">Azure Automation DSC lets you easily onboard Azure virtual machines for configuration management, using either the Azure portal, Azure Resource Manager templates, or PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e1401-132">Azure Automation DSC lets you easily onboard Azure virtual machines for configuration management, using either the Azure portal, Azure Resource Manager templates, or PowerShell.</span></span> <span data-ttu-id="e1401-133">Under the hood, and without an administrator having to remote into the VM, the Azure VM Desired State Configuration extension registers the VM with Azure Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="e1401-133">Under the hood, and without an administrator having to remote into the VM, the Azure VM Desired State Configuration extension registers the VM with Azure Automation DSC.</span></span> <span data-ttu-id="e1401-134">Since the Azure VM Desired State Configuration extension runs asynchronously, steps to track its progress or troubleshoot it are provided in the [**Troubleshooting Azure virtual machine onboarding**](#troubleshooting-azure-virtual-machine-onboarding) section below.</span><span class="sxs-lookup"><span data-stu-id="e1401-134">Since the Azure VM Desired State Configuration extension runs asynchronously, steps to track its progress or troubleshoot it are provided in the [**Troubleshooting Azure virtual machine onboarding**](#troubleshooting-azure-virtual-machine-onboarding) section below.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="e1401-135">Azure portal</span><span class="sxs-lookup"><span data-stu-id="e1401-135">Azure portal</span></span>

<span data-ttu-id="e1401-136">In the [Azure portal](https://portal.azure.com/), navigate to the Azure Automation account where you want to onboard virtual machines.</span><span class="sxs-lookup"><span data-stu-id="e1401-136">In the [Azure portal](https://portal.azure.com/), navigate to the Azure Automation account where you want to onboard virtual machines.</span></span> <span data-ttu-id="e1401-137">On the Automation account dashboard, click **DSC Nodes** -> **Add Azure VM**.</span><span class="sxs-lookup"><span data-stu-id="e1401-137">On the Automation account dashboard, click **DSC Nodes** -> **Add Azure VM**.</span></span>

<span data-ttu-id="e1401-138">Under **Select virtual machines to onboard**, select one or more Azure virtual machines to onboard.</span><span class="sxs-lookup"><span data-stu-id="e1401-138">Under **Select virtual machines to onboard**, select one or more Azure virtual machines to onboard.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-dsc-onboarding/DSC_Onboarding_2.png)

<span data-ttu-id="e1401-139">Under **Configure registration data**, enter the [PowerShell DSC Local Configuration Manager values](https://msdn.microsoft.com/powershell/dsc/metaconfig4) required for your use case, and optionally a node configuration to assign to the VM.</span><span class="sxs-lookup"><span data-stu-id="e1401-139">Under **Configure registration data**, enter the [PowerShell DSC Local Configuration Manager values](https://msdn.microsoft.com/powershell/dsc/metaconfig4) required for your use case, and optionally a node configuration to assign to the VM.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-dsc-onboarding/DSC_Onboarding_3.png)

### <a name="azure-resource-manager-templates"></a><span data-ttu-id="e1401-140">Azure Resource Manager templates</span><span class="sxs-lookup"><span data-stu-id="e1401-140">Azure Resource Manager templates</span></span>

<span data-ttu-id="e1401-141">Azure virtual machines can be deployed and onboarded to Azure Automation DSC via Azure Resource Manager templates.</span><span class="sxs-lookup"><span data-stu-id="e1401-141">Azure virtual machines can be deployed and onboarded to Azure Automation DSC via Azure Resource Manager templates.</span></span> <span data-ttu-id="e1401-142">See [Configure a VM via DSC extension and Azure Automation DSC](https://azure.microsoft.com/documentation/templates/dsc-extension-azure-automation-pullserver/) for an example template that onboards an existing VM to Azure Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="e1401-142">See [Configure a VM via DSC extension and Azure Automation DSC](https://azure.microsoft.com/documentation/templates/dsc-extension-azure-automation-pullserver/) for an example template that onboards an existing VM to Azure Automation DSC.</span></span> <span data-ttu-id="e1401-143">To find the registration key and registration URL taken as input in this template, see the [**Secure registration**](#secure-registration) section below.</span><span class="sxs-lookup"><span data-stu-id="e1401-143">To find the registration key and registration URL taken as input in this template, see the [**Secure registration**](#secure-registration) section below.</span></span>

### <a name="powershell"></a><span data-ttu-id="e1401-144">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e1401-144">PowerShell</span></span>

<span data-ttu-id="e1401-145">The [Register-AzureRmAutomationDscNode](https://msdn.microsoft.com/library/mt603833.aspx) cmdlet can be used to onboard virtual machines in the Azure portal via PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e1401-145">The [Register-AzureRmAutomationDscNode](https://msdn.microsoft.com/library/mt603833.aspx) cmdlet can be used to onboard virtual machines in the Azure portal via PowerShell.</span></span>

## <a name="amazon-web-services-aws-virtual-machines"></a><span data-ttu-id="e1401-146">Amazon Web Services (AWS) virtual machines</span><span class="sxs-lookup"><span data-stu-id="e1401-146">Amazon Web Services (AWS) virtual machines</span></span>

<span data-ttu-id="e1401-147">You can easily onboard Amazon Web Services virtual machines for configuration management by Azure Automation DSC using the AWS DSC Toolkit.</span><span class="sxs-lookup"><span data-stu-id="e1401-147">You can easily onboard Amazon Web Services virtual machines for configuration management by Azure Automation DSC using the AWS DSC Toolkit.</span></span> <span data-ttu-id="e1401-148">You can learn more about the toolkit [here](https://blogs.msdn.microsoft.com/powershell/2016/04/20/aws-dsc-toolkit/).</span><span class="sxs-lookup"><span data-stu-id="e1401-148">You can learn more about the toolkit [here](https://blogs.msdn.microsoft.com/powershell/2016/04/20/aws-dsc-toolkit/).</span></span>

## <a name="physicalvirtual-windows-machines-on-premises-or-in-a-cloud-other-than-azureaws"></a><span data-ttu-id="e1401-149">Physical/virtual Windows machines on-premises, or in a cloud other than Azure/AWS</span><span class="sxs-lookup"><span data-stu-id="e1401-149">Physical/virtual Windows machines on-premises, or in a cloud other than Azure/AWS</span></span>

<span data-ttu-id="e1401-150">On-premises Windows machines and Windows machines in non-Azure clouds (such as Amazon Web Services) can also be onboarded to Azure Automation DSC, as long as they have outbound access to the internet, via a few simple steps:</span><span class="sxs-lookup"><span data-stu-id="e1401-150">On-premises Windows machines and Windows machines in non-Azure clouds (such as Amazon Web Services) can also be onboarded to Azure Automation DSC, as long as they have outbound access to the internet, via a few simple steps:</span></span>

1. <span data-ttu-id="e1401-151">Make sure the latest version of [WMF 5](http://aka.ms/wmf5latest) is installed on the machines you want to onboard to Azure Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="e1401-151">Make sure the latest version of [WMF 5](http://aka.ms/wmf5latest) is installed on the machines you want to onboard to Azure Automation DSC.</span></span>
2. <span data-ttu-id="e1401-152">Follow the directions in section [**Generating DSC metaconfigurations**](#generating-dsc-metaconfigurations) below to generate a folder containing the needed DSC metaconfigurations.</span><span class="sxs-lookup"><span data-stu-id="e1401-152">Follow the directions in section [**Generating DSC metaconfigurations**](#generating-dsc-metaconfigurations) below to generate a folder containing the needed DSC metaconfigurations.</span></span>
3. <span data-ttu-id="e1401-153">Remotely apply the PowerShell DSC metaconfiguration to the machines you want to onboard.</span><span class="sxs-lookup"><span data-stu-id="e1401-153">Remotely apply the PowerShell DSC metaconfiguration to the machines you want to onboard.</span></span> <span data-ttu-id="e1401-154">**The machine this command is run from must have the latest version of [WMF 5](http://aka.ms/wmf5latest) installed**:</span><span class="sxs-lookup"><span data-stu-id="e1401-154">**The machine this command is run from must have the latest version of [WMF 5](http://aka.ms/wmf5latest) installed**:</span></span>

    ```powershell
    Set-DscLocalConfigurationManager -Path C:\Users\joe\Desktop\DscMetaConfigs -ComputerName MyServer1, MyServer2
    ```

4. <span data-ttu-id="e1401-155">If you cannot apply the PowerShell DSC metaconfigurations remotely, copy the metaconfigurations folder from step 2 onto each machine to onboard.</span><span class="sxs-lookup"><span data-stu-id="e1401-155">If you cannot apply the PowerShell DSC metaconfigurations remotely, copy the metaconfigurations folder from step 2 onto each machine to onboard.</span></span> <span data-ttu-id="e1401-156">Then call **Set-DscLocalConfigurationManager** locally on each machine to onboard.</span><span class="sxs-lookup"><span data-stu-id="e1401-156">Then call **Set-DscLocalConfigurationManager** locally on each machine to onboard.</span></span>
5. <span data-ttu-id="e1401-157">Using the Azure portal or cmdlets, check that the machines to onboard now show up as DSC nodes registered in your Azure Automation account.</span><span class="sxs-lookup"><span data-stu-id="e1401-157">Using the Azure portal or cmdlets, check that the machines to onboard now show up as DSC nodes registered in your Azure Automation account.</span></span>

## <a name="physicalvirtual-linux-machines-on-premises-in-azure-or-in-a-cloud-other-than-azure"></a><span data-ttu-id="e1401-158">Physical/virtual Linux machines on-premises, in Azure, or in a cloud other than Azure</span><span class="sxs-lookup"><span data-stu-id="e1401-158">Physical/virtual Linux machines on-premises, in Azure, or in a cloud other than Azure</span></span>

<span data-ttu-id="e1401-159">On-premises Linux machines, Linux machines in Azure, and Linux machines in non-Azure clouds can also be onboarded to Azure Automation DSC, as long as they have outbound access to the internet, via a few simple steps:</span><span class="sxs-lookup"><span data-stu-id="e1401-159">On-premises Linux machines, Linux machines in Azure, and Linux machines in non-Azure clouds can also be onboarded to Azure Automation DSC, as long as they have outbound access to the internet, via a few simple steps:</span></span>

1. <span data-ttu-id="e1401-160">Make sure the latest version of the [DSC Linux agent](http://www.microsoft.com/download/details.aspx?id=49150) is installed on the machines you want to onboard to Azure Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="e1401-160">Make sure the latest version of the [DSC Linux agent](http://www.microsoft.com/download/details.aspx?id=49150) is installed on the machines you want to onboard to Azure Automation DSC.</span></span>
2. <span data-ttu-id="e1401-161">If the [PowerShell DSC Local Configuration Manager defaults](https://msdn.microsoft.com/powershell/dsc/metaconfig4) match your use case, and you want to onboard machines such that they **both** pull from and report to Azure Automation DSC:</span><span class="sxs-lookup"><span data-stu-id="e1401-161">If the [PowerShell DSC Local Configuration Manager defaults](https://msdn.microsoft.com/powershell/dsc/metaconfig4) match your use case, and you want to onboard machines such that they **both** pull from and report to Azure Automation DSC:</span></span>

   + <span data-ttu-id="e1401-162">On each Linux machine to onboard to Azure Automation DSC, use Register.py to onboard using the PowerShell DSC Local Configuration Manager defaults:</span><span class="sxs-lookup"><span data-stu-id="e1401-162">On each Linux machine to onboard to Azure Automation DSC, use Register.py to onboard using the PowerShell DSC Local Configuration Manager defaults:</span></span>

     `/opt/microsoft/dsc/Scripts/Register.py <Automation account registration key> <Automation account registration URL>`

   + <span data-ttu-id="e1401-163">To find the registration key and registration URL for your Automation account, see the [**Secure registration**](#secure-registration) section below.</span><span class="sxs-lookup"><span data-stu-id="e1401-163">To find the registration key and registration URL for your Automation account, see the [**Secure registration**](#secure-registration) section below.</span></span>

     <span data-ttu-id="e1401-164">If the PowerShell DSC Local Configuration Manager defaults **do** **not** match your use case, or you want to onboard machines such that they only report to Azure Automation DSC, but do not pull configuration or PowerShell modules from it,  follow steps 3 - 6.</span><span class="sxs-lookup"><span data-stu-id="e1401-164">If the PowerShell DSC Local Configuration Manager defaults **do** **not** match your use case, or you want to onboard machines such that they only report to Azure Automation DSC, but do not pull configuration or PowerShell modules from it,  follow steps 3 - 6.</span></span> <span data-ttu-id="e1401-165">Otherwise, proceed directly to step 6.</span><span class="sxs-lookup"><span data-stu-id="e1401-165">Otherwise, proceed directly to step 6.</span></span>

3. <span data-ttu-id="e1401-166">Follow the directions in the [**Generating DSC metaconfigurations**](#generating-dsc-metaconfigurations) section below to generate a folder containing the needed DSC metaconfigurations.</span><span class="sxs-lookup"><span data-stu-id="e1401-166">Follow the directions in the [**Generating DSC metaconfigurations**](#generating-dsc-metaconfigurations) section below to generate a folder containing the needed DSC metaconfigurations.</span></span>
4. <span data-ttu-id="e1401-167">Remotely apply the PowerShell DSC metaconfiguration to the machines you want to onboard:</span><span class="sxs-lookup"><span data-stu-id="e1401-167">Remotely apply the PowerShell DSC metaconfiguration to the machines you want to onboard:</span></span>

    ```powershell
    $SecurePass = ConvertTo-SecureString -String "<root password>" -AsPlainText -Force
    $Cred = New-Object System.Management.Automation.PSCredential "root", $SecurePass
    $Opt = New-CimSessionOption -UseSsl -SkipCACheck -SkipCNCheck -SkipRevocationCheck

    # need a CimSession for each Linux machine to onboard

    $Session = New-CimSession -Credential $Cred -ComputerName <your Linux machine> -Port 5986 -Authentication basic -SessionOption $Opt

    Set-DscLocalConfigurationManager -CimSession $Session -Path C:\Users\joe\Desktop\DscMetaConfigs
    ```

<span data-ttu-id="e1401-168">The machine this command is run from must have the latest version of [WMF 5](http://aka.ms/wmf5latest) installed.</span><span class="sxs-lookup"><span data-stu-id="e1401-168">The machine this command is run from must have the latest version of [WMF 5](http://aka.ms/wmf5latest) installed.</span></span>

1. <span data-ttu-id="e1401-169">If you cannot apply the PowerShell DSC metaconfigurations remotely, for each Linux machine to onboard, copy the metaconfiguration corresponding to that machine from the folder in step 5 onto the Linux machine.</span><span class="sxs-lookup"><span data-stu-id="e1401-169">If you cannot apply the PowerShell DSC metaconfigurations remotely, for each Linux machine to onboard, copy the metaconfiguration corresponding to that machine from the folder in step 5 onto the Linux machine.</span></span> <span data-ttu-id="e1401-170">Then call `SetDscLocalConfigurationManager.py` locally on each Linux machine you want to onboard to Azure Automation DSC:</span><span class="sxs-lookup"><span data-stu-id="e1401-170">Then call `SetDscLocalConfigurationManager.py` locally on each Linux machine you want to onboard to Azure Automation DSC:</span></span>

   `/opt/microsoft/dsc/Scripts/SetDscLocalConfigurationManager.py -configurationmof <path to metaconfiguration file>`

2. <span data-ttu-id="e1401-171">Using the Azure portal or cmdlets, check that the machines to onboard now show up as DSC nodes registered in your Azure Automation account.</span><span class="sxs-lookup"><span data-stu-id="e1401-171">Using the Azure portal or cmdlets, check that the machines to onboard now show up as DSC nodes registered in your Azure Automation account.</span></span>

## <a name="generating-dsc-metaconfigurations"></a><span data-ttu-id="e1401-172">Generating DSC metaconfigurations</span><span class="sxs-lookup"><span data-stu-id="e1401-172">Generating DSC metaconfigurations</span></span>

<span data-ttu-id="e1401-173">To generically onboard any machine to Azure Automation DSC, a [DSC metaconfiguration](https://msdn.microsoft.com/en-us/powershell/dsc/metaconfig) can be generated that, when applied, tells the DSC agent on the machine to pull from and/or report to Azure Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="e1401-173">To generically onboard any machine to Azure Automation DSC, a [DSC metaconfiguration](https://msdn.microsoft.com/en-us/powershell/dsc/metaconfig) can be generated that, when applied, tells the DSC agent on the machine to pull from and/or report to Azure Automation DSC.</span></span> <span data-ttu-id="e1401-174">DSC metaconfigurations for Azure Automation DSC can be generated using either a PowerShell DSC configuration, or the Azure Automation PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="e1401-174">DSC metaconfigurations for Azure Automation DSC can be generated using either a PowerShell DSC configuration, or the Azure Automation PowerShell cmdlets.</span></span>

> [!NOTE]
> <span data-ttu-id="e1401-175">DSC metaconfigurations contain the secrets needed to onboard a machine to an Automation account for management.</span><span class="sxs-lookup"><span data-stu-id="e1401-175">DSC metaconfigurations contain the secrets needed to onboard a machine to an Automation account for management.</span></span> <span data-ttu-id="e1401-176">Make sure to properly protect any DSC metaconfigurations you create, or delete them after use.</span><span class="sxs-lookup"><span data-stu-id="e1401-176">Make sure to properly protect any DSC metaconfigurations you create, or delete them after use.</span></span>

### <a name="using-a-dsc-configuration"></a><span data-ttu-id="e1401-177">Using a DSC Configuration</span><span class="sxs-lookup"><span data-stu-id="e1401-177">Using a DSC Configuration</span></span>

1. <span data-ttu-id="e1401-178">Open the PowerShell ISE as an administrator in a machine in your local environment.</span><span class="sxs-lookup"><span data-stu-id="e1401-178">Open the PowerShell ISE as an administrator in a machine in your local environment.</span></span> <span data-ttu-id="e1401-179">The machine must have the latest version of [WMF 5](http://aka.ms/wmf5latest) installed.</span><span class="sxs-lookup"><span data-stu-id="e1401-179">The machine must have the latest version of [WMF 5](http://aka.ms/wmf5latest) installed.</span></span>
2. <span data-ttu-id="e1401-180">Copy the following script locally.</span><span class="sxs-lookup"><span data-stu-id="e1401-180">Copy the following script locally.</span></span> <span data-ttu-id="e1401-181">This script contains a PowerShell DSC configuration for creating metaconfigurations, and a command to kick off the metaconfiguration creation.</span><span class="sxs-lookup"><span data-stu-id="e1401-181">This script contains a PowerShell DSC configuration for creating metaconfigurations, and a command to kick off the metaconfiguration creation.</span></span>

    ```powershell
    # The DSC configuration that will generate metaconfigurations
    [DscLocalConfigurationManager()]
    Configuration DscMetaConfigs
    {

        param
        (
            [Parameter(Mandatory=$True)]
            [String]$RegistrationUrl,

            [Parameter(Mandatory=$True)]
            [String]$RegistrationKey,

            [Parameter(Mandatory=$True)]
            [String[]]$ComputerName,

            [Int]$RefreshFrequencyMins = 30,

            [Int]$ConfigurationModeFrequencyMins = 15,

            [String]$ConfigurationMode = "ApplyAndMonitor",

            [String]$NodeConfigurationName,

            [Boolean]$RebootNodeIfNeeded= $False,

            [String]$ActionAfterReboot = "ContinueConfiguration",

            [Boolean]$AllowModuleOverwrite = $False,

            [Boolean]$ReportOnly
        )

        if(!$NodeConfigurationName -or $NodeConfigurationName -eq "")
        {
            $ConfigurationNames = $null
        }
        else
        {
            $ConfigurationNames = @($NodeConfigurationName)
        }

        if($ReportOnly)
        {
        $RefreshMode = "PUSH"
        }
        else
        {
        $RefreshMode = "PULL"
        }

        Node $ComputerName
        {

            Settings
            {
                RefreshFrequencyMins = $RefreshFrequencyMins
                RefreshMode = $RefreshMode
                ConfigurationMode = $ConfigurationMode
                AllowModuleOverwrite = $AllowModuleOverwrite
                RebootNodeIfNeeded = $RebootNodeIfNeeded
                ActionAfterReboot = $ActionAfterReboot
                ConfigurationModeFrequencyMins = $ConfigurationModeFrequencyMins
            }

            if(!$ReportOnly)
            {
            ConfigurationRepositoryWeb AzureAutomationDSC
                {
                    ServerUrl = $RegistrationUrl
                    RegistrationKey = $RegistrationKey
                    ConfigurationNames = $ConfigurationNames
                }

                ResourceRepositoryWeb AzureAutomationDSC
                {
                ServerUrl = $RegistrationUrl
                RegistrationKey = $RegistrationKey
                }
            }

            ReportServerWeb AzureAutomationDSC
            {
                ServerUrl = $RegistrationUrl
                RegistrationKey = $RegistrationKey
            }
        }
    }

    # Create the metaconfigurations
    # TODO: edit the below as needed for your use case
    $Params = @{
        RegistrationUrl = '<fill me in>';
        RegistrationKey = '<fill me in>';
        ComputerName = @('<some VM to onboard>', '<some other VM to onboard>');
        NodeConfigurationName = 'SimpleConfig.webserver';
        RefreshFrequencyMins = 30;
        ConfigurationModeFrequencyMins = 15;
        RebootNodeIfNeeded = $False;
        AllowModuleOverwrite = $False;
        ConfigurationMode = 'ApplyAndMonitor';
        ActionAfterReboot = 'ContinueConfiguration';
        ReportOnly = $False;  # Set to $True to have machines only report to AA DSC but not pull from it
    }

    # Use PowerShell splatting to pass parameters to the DSC configuration being invoked
    # For more info about splatting, run: Get-Help -Name about_Splatting
    DscMetaConfigs @Params
    ```

3. <span data-ttu-id="e1401-182">Fill in the registration key and URL for your Automation account, as well as the names of the machines to onboard.</span><span class="sxs-lookup"><span data-stu-id="e1401-182">Fill in the registration key and URL for your Automation account, as well as the names of the machines to onboard.</span></span> <span data-ttu-id="e1401-183">All other parameters are optional.</span><span class="sxs-lookup"><span data-stu-id="e1401-183">All other parameters are optional.</span></span> <span data-ttu-id="e1401-184">To find the registration key and registration URL for your Automation account, see the [**Secure registration**](#secure-registration) section below.</span><span class="sxs-lookup"><span data-stu-id="e1401-184">To find the registration key and registration URL for your Automation account, see the [**Secure registration**](#secure-registration) section below.</span></span>
4. <span data-ttu-id="e1401-185">If you want the machines to report DSC status information to Azure Automation DSC, but not pull configuration or PowerShell modules, set the **ReportOnly** parameter to true.</span><span class="sxs-lookup"><span data-stu-id="e1401-185">If you want the machines to report DSC status information to Azure Automation DSC, but not pull configuration or PowerShell modules, set the **ReportOnly** parameter to true.</span></span>
5. <span data-ttu-id="e1401-186">Run the script.</span><span class="sxs-lookup"><span data-stu-id="e1401-186">Run the script.</span></span> <span data-ttu-id="e1401-187">You should now have a folder called **DscMetaConfigs** in your working directory, containing the PowerShell DSC metaconfigurations for the machines to onboard (as an administrator):</span><span class="sxs-lookup"><span data-stu-id="e1401-187">You should now have a folder called **DscMetaConfigs** in your working directory, containing the PowerShell DSC metaconfigurations for the machines to onboard (as an administrator):</span></span>

    ```powershell
    Set-DscLocalConfigurationManager -Path ./DscMetaConfigs
    ```

### <a name="using-the-azure-automation-cmdlets"></a><span data-ttu-id="e1401-188">Using the Azure Automation cmdlets</span><span class="sxs-lookup"><span data-stu-id="e1401-188">Using the Azure Automation cmdlets</span></span>

<span data-ttu-id="e1401-189">If the PowerShell DSC Local Configuration Manager defaults match your use case, and you want to onboard machines such that they both pull from and report to Azure Automation DSC, the Azure Automation cmdlets provide a simplified method of generating the DSC metaconfigurations needed:</span><span class="sxs-lookup"><span data-stu-id="e1401-189">If the PowerShell DSC Local Configuration Manager defaults match your use case, and you want to onboard machines such that they both pull from and report to Azure Automation DSC, the Azure Automation cmdlets provide a simplified method of generating the DSC metaconfigurations needed:</span></span>

1. <span data-ttu-id="e1401-190">Open the PowerShell console or PowerShell ISE as an administrator in a machine in your local environment.</span><span class="sxs-lookup"><span data-stu-id="e1401-190">Open the PowerShell console or PowerShell ISE as an administrator in a machine in your local environment.</span></span>
2. <span data-ttu-id="e1401-191">Connect to Azure Resource Manager using **Add-AzureRmAccount**</span><span class="sxs-lookup"><span data-stu-id="e1401-191">Connect to Azure Resource Manager using **Add-AzureRmAccount**</span></span>
3. <span data-ttu-id="e1401-192">Download the PowerShell DSC metaconfigurations for the machines you want to onboard from the Automation account to which you want to onboard nodes:</span><span class="sxs-lookup"><span data-stu-id="e1401-192">Download the PowerShell DSC metaconfigurations for the machines you want to onboard from the Automation account to which you want to onboard nodes:</span></span>

    ```powershell
    # Define the parameters for Get-AzureRmAutomationDscOnboardingMetaconfig using PowerShell Splatting
    $Params = @{

        ResourceGroupName = 'ContosoResources'; # The name of the ARM Resource Group that contains your Azure Automation Account
        AutomationAccountName = 'ContosoAutomation'; # The name of the Azure Automation Account where you want a node on-boarded to
        ComputerName = @('web01', 'web02', 'sql01'); # The names of the computers that the meta configuration will be generated for
        OutputFolder = "$env:UserProfile\Desktop\";
    }
    # Use PowerShell splatting to pass parameters to the Azure Automation cmdlet being invoked
    # For more info about splatting, run: Get-Help -Name about_Splatting
    Get-AzureRmAutomationDscOnboardingMetaconfig @Params
    ```
    
4. <span data-ttu-id="e1401-193">You should now have a folder called ***DscMetaConfigs***, containing the PowerShell DSC metaconfigurations for the machines to onboard (as an administrator):</span><span class="sxs-lookup"><span data-stu-id="e1401-193">You should now have a folder called ***DscMetaConfigs***, containing the PowerShell DSC metaconfigurations for the machines to onboard (as an administrator):</span></span>
    
    ```powershell
    Set-DscLocalConfigurationManager -Path $env:UserProfile\Desktop\DscMetaConfigs
    ```

## <a name="secure-registration"></a><span data-ttu-id="e1401-194">Secure registration</span><span class="sxs-lookup"><span data-stu-id="e1401-194">Secure registration</span></span>

<span data-ttu-id="e1401-195">Machines can securely onboard to an Azure Automation account through the WMF 5 DSC registration protocol, which allows a DSC node to authenticate to a PowerShell DSC V2 Pull or Reporting server (including Azure Automation DSC).</span><span class="sxs-lookup"><span data-stu-id="e1401-195">Machines can securely onboard to an Azure Automation account through the WMF 5 DSC registration protocol, which allows a DSC node to authenticate to a PowerShell DSC V2 Pull or Reporting server (including Azure Automation DSC).</span></span> <span data-ttu-id="e1401-196">The node registers to the server at a **Registration URL**, authenticating using a **Registration key**.</span><span class="sxs-lookup"><span data-stu-id="e1401-196">The node registers to the server at a **Registration URL**, authenticating using a **Registration key**.</span></span> <span data-ttu-id="e1401-197">During registration, the DSC node and DSC Pull/Reporting server negotiate a unique certificate for this node to use for authentication to the server post-registration.</span><span class="sxs-lookup"><span data-stu-id="e1401-197">During registration, the DSC node and DSC Pull/Reporting server negotiate a unique certificate for this node to use for authentication to the server post-registration.</span></span> <span data-ttu-id="e1401-198">This process prevents onboarded nodes from impersonating one another, such as if a node is compromised and behaving maliciously.</span><span class="sxs-lookup"><span data-stu-id="e1401-198">This process prevents onboarded nodes from impersonating one another, such as if a node is compromised and behaving maliciously.</span></span> <span data-ttu-id="e1401-199">After registration, the Registration key is not used for authentication again, and is deleted from the node.</span><span class="sxs-lookup"><span data-stu-id="e1401-199">After registration, the Registration key is not used for authentication again, and is deleted from the node.</span></span>

<span data-ttu-id="e1401-200">You can get the information required for the DSC registration protocol from the **Manage Keys** blade in the Azure preview portal.</span><span class="sxs-lookup"><span data-stu-id="e1401-200">You can get the information required for the DSC registration protocol from the **Manage Keys** blade in the Azure preview portal.</span></span> <span data-ttu-id="e1401-201">Open this blade by clicking the key icon on the **Essentials** panel for the Automation account.</span><span class="sxs-lookup"><span data-stu-id="e1401-201">Open this blade by clicking the key icon on the **Essentials** panel for the Automation account.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-dsc-onboarding/DSC_Onboarding_4.png)

* <span data-ttu-id="e1401-202">Registration URL is the URL field in the Manage Keys blade.</span><span class="sxs-lookup"><span data-stu-id="e1401-202">Registration URL is the URL field in the Manage Keys blade.</span></span>
* <span data-ttu-id="e1401-203">Registration key is the Primary Access Key or Secondary Access Key in the Manage Keys blade.</span><span class="sxs-lookup"><span data-stu-id="e1401-203">Registration key is the Primary Access Key or Secondary Access Key in the Manage Keys blade.</span></span> <span data-ttu-id="e1401-204">Either key can be used.</span><span class="sxs-lookup"><span data-stu-id="e1401-204">Either key can be used.</span></span>

<span data-ttu-id="e1401-205">For added security, the primary and secondary access keys of an Automation account can be regenerated at any time (on the **Manage Keys** blade) to prevent future node registrations using previous keys.</span><span class="sxs-lookup"><span data-stu-id="e1401-205">For added security, the primary and secondary access keys of an Automation account can be regenerated at any time (on the **Manage Keys** blade) to prevent future node registrations using previous keys.</span></span>

## <a name="troubleshooting-azure-virtual-machine-onboarding"></a><span data-ttu-id="e1401-206">Troubleshooting Azure virtual machine onboarding</span><span class="sxs-lookup"><span data-stu-id="e1401-206">Troubleshooting Azure virtual machine onboarding</span></span>

<span data-ttu-id="e1401-207">Azure Automation DSC lets you easily onboard Azure Windows VMs for configuration management.</span><span class="sxs-lookup"><span data-stu-id="e1401-207">Azure Automation DSC lets you easily onboard Azure Windows VMs for configuration management.</span></span> <span data-ttu-id="e1401-208">Under the hood, the Azure VM Desired State Configuration extension is used to register the VM with Azure Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="e1401-208">Under the hood, the Azure VM Desired State Configuration extension is used to register the VM with Azure Automation DSC.</span></span> <span data-ttu-id="e1401-209">Since the Azure VM Desired State Configuration extension runs asynchronously, tracking its progress and troubleshooting its execution may be important.</span><span class="sxs-lookup"><span data-stu-id="e1401-209">Since the Azure VM Desired State Configuration extension runs asynchronously, tracking its progress and troubleshooting its execution may be important.</span></span>

> [!NOTE]
> <span data-ttu-id="e1401-210">Any method of onboarding an Azure Windows VM to Azure Automation DSC that uses the Azure VM Desired State Configuration extension could take up to an hour for the node to show up as registered in Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="e1401-210">Any method of onboarding an Azure Windows VM to Azure Automation DSC that uses the Azure VM Desired State Configuration extension could take up to an hour for the node to show up as registered in Azure Automation.</span></span> <span data-ttu-id="e1401-211">This is due to the installation of Windows Management Framework 5.0 on the VM by the Azure VM DSC extension, which is required to onboard the VM to Azure Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="e1401-211">This is due to the installation of Windows Management Framework 5.0 on the VM by the Azure VM DSC extension, which is required to onboard the VM to Azure Automation DSC.</span></span>

<span data-ttu-id="e1401-212">To troubleshoot or view the status of the Azure VM Desired State Configuration extension, in the Azure portal navigate to the VM being onboarded, then click -> **All settings** -> **Extensions** -> **DSC**.</span><span class="sxs-lookup"><span data-stu-id="e1401-212">To troubleshoot or view the status of the Azure VM Desired State Configuration extension, in the Azure portal navigate to the VM being onboarded, then click -> **All settings** -> **Extensions** -> **DSC**.</span></span> <span data-ttu-id="e1401-213">For more details, you can click **View detailed status**.</span><span class="sxs-lookup"><span data-stu-id="e1401-213">For more details, you can click **View detailed status**.</span></span>

[![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-dsc-onboarding/DSC_Onboarding_5.png)](https://technet.microsoft.com/library/dn249912.aspx)

## <a name="certificate-expiration-and-reregistration"></a><span data-ttu-id="e1401-214">Certificate expiration and reregistration</span><span class="sxs-lookup"><span data-stu-id="e1401-214">Certificate expiration and reregistration</span></span>

<span data-ttu-id="e1401-215">After registering a machine as a DSC node in Azure Automation DSC, there are a number of reasons why you may need to reregister that node in the future:</span><span class="sxs-lookup"><span data-stu-id="e1401-215">After registering a machine as a DSC node in Azure Automation DSC, there are a number of reasons why you may need to reregister that node in the future:</span></span>

* <span data-ttu-id="e1401-216">After registering, each node automatically negotiates a unique certificate for authentication that expires after one year.</span><span class="sxs-lookup"><span data-stu-id="e1401-216">After registering, each node automatically negotiates a unique certificate for authentication that expires after one year.</span></span> <span data-ttu-id="e1401-217">Currently, the PowerShell DSC registration protocol cannot automatically renew certificates when they are nearing expiration, so you need to reregister the nodes after a year's time.</span><span class="sxs-lookup"><span data-stu-id="e1401-217">Currently, the PowerShell DSC registration protocol cannot automatically renew certificates when they are nearing expiration, so you need to reregister the nodes after a year's time.</span></span> <span data-ttu-id="e1401-218">Before reregistering, ensure that each node is running Windows Management Framework 5.0 RTM.</span><span class="sxs-lookup"><span data-stu-id="e1401-218">Before reregistering, ensure that each node is running Windows Management Framework 5.0 RTM.</span></span> <span data-ttu-id="e1401-219">If a node's authentication certificate expires, and the node is not reregistered, the node will be unable to communicate with Azure Automation and will be marked 'Unresponsive.'</span><span class="sxs-lookup"><span data-stu-id="e1401-219">If a node's authentication certificate expires, and the node is not reregistered, the node will be unable to communicate with Azure Automation and will be marked 'Unresponsive.'</span></span> <span data-ttu-id="e1401-220">Reregistration performed 90 days or less from the certificate expiration time, or at any point after the certificate expiration time, will result in a new certificate being generated and used.</span><span class="sxs-lookup"><span data-stu-id="e1401-220">Reregistration performed 90 days or less from the certificate expiration time, or at any point after the certificate expiration time, will result in a new certificate being generated and used.</span></span>
* <span data-ttu-id="e1401-221">To change any [PowerShell DSC Local Configuration Manager values](https://msdn.microsoft.com/powershell/dsc/metaconfig4) that were set during initial registration of the node, such as ConfigurationMode.</span><span class="sxs-lookup"><span data-stu-id="e1401-221">To change any [PowerShell DSC Local Configuration Manager values](https://msdn.microsoft.com/powershell/dsc/metaconfig4) that were set during initial registration of the node, such as ConfigurationMode.</span></span> <span data-ttu-id="e1401-222">Currently, these DSC agent values can only be changed through reregistration.</span><span class="sxs-lookup"><span data-stu-id="e1401-222">Currently, these DSC agent values can only be changed through reregistration.</span></span> <span data-ttu-id="e1401-223">The one exception is the Node Configuration assigned to the node -- this can be changed in Azure Automation DSC directly.</span><span class="sxs-lookup"><span data-stu-id="e1401-223">The one exception is the Node Configuration assigned to the node -- this can be changed in Azure Automation DSC directly.</span></span>

<span data-ttu-id="e1401-224">Reregistration can be performed in the same way you registered the node initially, using any of the onboarding methods described in this document.</span><span class="sxs-lookup"><span data-stu-id="e1401-224">Reregistration can be performed in the same way you registered the node initially, using any of the onboarding methods described in this document.</span></span> <span data-ttu-id="e1401-225">You do not need to unregister a node from Azure Automation DSC before reregistering it.</span><span class="sxs-lookup"><span data-stu-id="e1401-225">You do not need to unregister a node from Azure Automation DSC before reregistering it.</span></span>

## <a name="related-articles"></a><span data-ttu-id="e1401-226">Related Articles</span><span class="sxs-lookup"><span data-stu-id="e1401-226">Related Articles</span></span>

* [<span data-ttu-id="e1401-227">Azure Automation DSC overview</span><span class="sxs-lookup"><span data-stu-id="e1401-227">Azure Automation DSC overview</span></span>](automation-dsc-overview.md)
* [<span data-ttu-id="e1401-228">Azure Automation DSC cmdlets</span><span class="sxs-lookup"><span data-stu-id="e1401-228">Azure Automation DSC cmdlets</span></span>](https://msdn.microsoft.com/library/mt244122.aspx)
* [<span data-ttu-id="e1401-229">Azure Automation DSC pricing</span><span class="sxs-lookup"><span data-stu-id="e1401-229">Azure Automation DSC pricing</span></span>](https://azure.microsoft.com/pricing/details/automation/)





