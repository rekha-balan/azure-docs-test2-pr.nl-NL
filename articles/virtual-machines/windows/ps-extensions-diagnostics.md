---
title: Use Azure PowerShell to enable diagnostics on a Windows VM | Microsoft Docs
services: virtual-machines-windows
documentationcenter: ''
description: Learn how to use PowerShell to enable Azure Diagnostics in a virtual machine running Windows
author: sbtron
manager: timlt
editor: ''
ms.assetid: 2e6d88f2-1980-4a24-827e-a81616a0d247
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 12/15/2015
ms.author: saurabh
ms.openlocfilehash: 17b6760c16730097539a0c58e150f9d8eb0d88db
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661163"
---
# <a name="use-powershell-to-enable-azure-diagnostics-in-a-virtual-machine-running-windows"></a><span data-ttu-id="308fe-103">Use PowerShell to enable Azure Diagnostics in a virtual machine running Windows</span><span class="sxs-lookup"><span data-stu-id="308fe-103">Use PowerShell to enable Azure Diagnostics in a virtual machine running Windows</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="308fe-104">Azure Diagnostics is the capability within Azure that enables the collection of diagnostic data on a deployed application.</span><span class="sxs-lookup"><span data-stu-id="308fe-104">Azure Diagnostics is the capability within Azure that enables the collection of diagnostic data on a deployed application.</span></span> <span data-ttu-id="308fe-105">You can use the diagnostics extension to collect diagnostic data like application logs or performance counters from an Azure virtual machine (VM) that is running Windows.</span><span class="sxs-lookup"><span data-stu-id="308fe-105">You can use the diagnostics extension to collect diagnostic data like application logs or performance counters from an Azure virtual machine (VM) that is running Windows.</span></span> <span data-ttu-id="308fe-106">This article describes how to use Windows PowerShell to enable the diagnostics extension for a VM.</span><span class="sxs-lookup"><span data-stu-id="308fe-106">This article describes how to use Windows PowerShell to enable the diagnostics extension for a VM.</span></span> <span data-ttu-id="308fe-107">See [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for the prerequisites needed for this article.</span><span class="sxs-lookup"><span data-stu-id="308fe-107">See [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for the prerequisites needed for this article.</span></span>

## <a name="enable-the-diagnostics-extension-if-you-use-the-resource-manager-deployment-model"></a><span data-ttu-id="308fe-108">Enable the diagnostics extension if you use the Resource Manager deployment model</span><span class="sxs-lookup"><span data-stu-id="308fe-108">Enable the diagnostics extension if you use the Resource Manager deployment model</span></span>
<span data-ttu-id="308fe-109">You can enable the diagnostics extension while you create a Windows VM through the Azure Resource Manager deployment model by adding the extension configuration to the Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="308fe-109">You can enable the diagnostics extension while you create a Windows VM through the Azure Resource Manager deployment model by adding the extension configuration to the Resource Manager template.</span></span> <span data-ttu-id="308fe-110">See [Create a Windows virtual machine with monitoring and diagnostics by using the Azure Resource Manager template](extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="308fe-110">See [Create a Windows virtual machine with monitoring and diagnostics by using the Azure Resource Manager template](extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="308fe-111">To enable the diagnostics extension on an existing VM that was created through the Resource Manager deployment model, you can use the [Set-AzureRMVMDiagnosticsExtension](https://msdn.microsoft.com/library/mt603499.aspx) PowerShell cmdlet as shown below.</span><span class="sxs-lookup"><span data-stu-id="308fe-111">To enable the diagnostics extension on an existing VM that was created through the Resource Manager deployment model, you can use the [Set-AzureRMVMDiagnosticsExtension](https://msdn.microsoft.com/library/mt603499.aspx) PowerShell cmdlet as shown below.</span></span>

    $vm_resourcegroup = "myvmresourcegroup"
    $vm_name = "myvm"
    $diagnosticsconfig_path = "DiagnosticsPubConfig.xml"

    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name -DiagnosticsConfigurationPath $diagnosticsconfig_path


<span data-ttu-id="308fe-112">*$diagnosticsconfig_path* is the path to the file that contains the diagnostics configuration in XML, as described in the [sample](#sample-diagnostics-configuration) below.</span><span class="sxs-lookup"><span data-stu-id="308fe-112">*$diagnosticsconfig_path* is the path to the file that contains the diagnostics configuration in XML, as described in the [sample](#sample-diagnostics-configuration) below.</span></span>  

<span data-ttu-id="308fe-113">If the diagnostics configuration file specifies a **StorageAccount** element with a storage account name, then the *Set-AzureRMVMDiagnosticsExtension* script will automatically set the diagnostics extension to send diagnostic data to that storage account.</span><span class="sxs-lookup"><span data-stu-id="308fe-113">If the diagnostics configuration file specifies a **StorageAccount** element with a storage account name, then the *Set-AzureRMVMDiagnosticsExtension* script will automatically set the diagnostics extension to send diagnostic data to that storage account.</span></span> <span data-ttu-id="308fe-114">For this to work, the storage account needs to be in the same subscription as the VM.</span><span class="sxs-lookup"><span data-stu-id="308fe-114">For this to work, the storage account needs to be in the same subscription as the VM.</span></span>

<span data-ttu-id="308fe-115">If no **StorageAccount** was specified in the diagnostics configuration, then you need to pass in the *StorageAccountName* parameter to the cmdlet.</span><span class="sxs-lookup"><span data-stu-id="308fe-115">If no **StorageAccount** was specified in the diagnostics configuration, then you need to pass in the *StorageAccountName* parameter to the cmdlet.</span></span> <span data-ttu-id="308fe-116">If the *StorageAccountName* parameter is specified, then the cmdlet will always use the storage account that is specified in the parameter and not the one that is specified in the diagnostics configuration file.</span><span class="sxs-lookup"><span data-stu-id="308fe-116">If the *StorageAccountName* parameter is specified, then the cmdlet will always use the storage account that is specified in the parameter and not the one that is specified in the diagnostics configuration file.</span></span>

<span data-ttu-id="308fe-117">If the diagnostics storage account is in a different subscription from the VM, then you need to explicitly pass in the *StorageAccountName* and *StorageAccountKey* parameters to the cmdlet.</span><span class="sxs-lookup"><span data-stu-id="308fe-117">If the diagnostics storage account is in a different subscription from the VM, then you need to explicitly pass in the *StorageAccountName* and *StorageAccountKey* parameters to the cmdlet.</span></span> <span data-ttu-id="308fe-118">The *StorageAccountKey* parameter is not needed when the diagnostics storage account is in the same subscription, as the cmdlet can automatically query and set the key value when enabling the diagnostics extension.</span><span class="sxs-lookup"><span data-stu-id="308fe-118">The *StorageAccountKey* parameter is not needed when the diagnostics storage account is in the same subscription, as the cmdlet can automatically query and set the key value when enabling the diagnostics extension.</span></span> <span data-ttu-id="308fe-119">However, if the diagnostics storage account is in a different subscription, then the cmdlet might not be able to get the key automatically and you need to explicitly specify the key through the *StorageAccountKey* parameter.</span><span class="sxs-lookup"><span data-stu-id="308fe-119">However, if the diagnostics storage account is in a different subscription, then the cmdlet might not be able to get the key automatically and you need to explicitly specify the key through the *StorageAccountKey* parameter.</span></span>  

    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name -DiagnosticsConfigurationPath $diagnosticsconfig_path -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key

<span data-ttu-id="308fe-120">Once the diagnostics extension is enabled on a VM, you can get the current settings by using the [Get-AzureRMVmDiagnosticsExtension](https://msdn.microsoft.com/library/mt603678.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="308fe-120">Once the diagnostics extension is enabled on a VM, you can get the current settings by using the [Get-AzureRMVmDiagnosticsExtension](https://msdn.microsoft.com/library/mt603678.aspx) cmdlet.</span></span>

    Get-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name

<span data-ttu-id="308fe-121">The cmdlet returns *PublicSettings*, which contains the XML configuration in a Base64-encoded format.</span><span class="sxs-lookup"><span data-stu-id="308fe-121">The cmdlet returns *PublicSettings*, which contains the XML configuration in a Base64-encoded format.</span></span> <span data-ttu-id="308fe-122">To read the XML, you need to decode it.</span><span class="sxs-lookup"><span data-stu-id="308fe-122">To read the XML, you need to decode it.</span></span>

    $publicsettings = (Get-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name).PublicSettings
    $encodedconfig = (ConvertFrom-Json -InputObject $publicsettings).xmlCfg
    $xmlconfig = [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($encodedconfig))
    Write-Host $xmlconfig

<span data-ttu-id="308fe-123">The [Remove-AzureRMVmDiagnosticsExtension](https://msdn.microsoft.com/library/mt603782.aspx) cmdlet can be used to remove the diagnostics extension from the VM.</span><span class="sxs-lookup"><span data-stu-id="308fe-123">The [Remove-AzureRMVmDiagnosticsExtension](https://msdn.microsoft.com/library/mt603782.aspx) cmdlet can be used to remove the diagnostics extension from the VM.</span></span>  

## <a name="enable-the-diagnostics-extension-if-you-use-the-classic-deployment-model"></a><span data-ttu-id="308fe-124">Enable the diagnostics extension if you use the classic deployment model</span><span class="sxs-lookup"><span data-stu-id="308fe-124">Enable the diagnostics extension if you use the classic deployment model</span></span>
<span data-ttu-id="308fe-125">You can use the [Set-AzureVMDiagnosticsExtension](https://msdn.microsoft.com/library/mt589189.aspx) cmdlet to enable a diagnostics extension on a VM that you create through the classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="308fe-125">You can use the [Set-AzureVMDiagnosticsExtension](https://msdn.microsoft.com/library/mt589189.aspx) cmdlet to enable a diagnostics extension on a VM that you create through the classic deployment model.</span></span> <span data-ttu-id="308fe-126">The following example shows how to create a new VM through the classic deployment model with the diagnostics extension enabled.</span><span class="sxs-lookup"><span data-stu-id="308fe-126">The following example shows how to create a new VM through the classic deployment model with the diagnostics extension enabled.</span></span>

    $VM = New-AzureVMConfig -Name $VM -InstanceSize Small -ImageName $VMImage
    $VM = Add-AzureProvisioningConfig -VM $VM -AdminUsername $Username -Password $Password -Windows
    $VM = Set-AzureVMDiagnosticsExtension -DiagnosticsConfigurationPath $Config_Path -VM $VM -StorageContext $Storage_Context
    New-AzureVM -Location $Location -ServiceName $Service_Name -VM $VM

<span data-ttu-id="308fe-127">To enable the diagnostics extension on an existing VM that was created through the classic deployment model, first use the [Get-AzureVM](https://msdn.microsoft.com/library/mt589152.aspx) cmdlet to get the VM configuration.</span><span class="sxs-lookup"><span data-stu-id="308fe-127">To enable the diagnostics extension on an existing VM that was created through the classic deployment model, first use the [Get-AzureVM](https://msdn.microsoft.com/library/mt589152.aspx) cmdlet to get the VM configuration.</span></span> <span data-ttu-id="308fe-128">Then update the VM configuration to include the diagnostics extension by using the [Set-AzureVMDiagnosticsExtension](https://msdn.microsoft.com/library/mt589189.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="308fe-128">Then update the VM configuration to include the diagnostics extension by using the [Set-AzureVMDiagnosticsExtension](https://msdn.microsoft.com/library/mt589189.aspx) cmdlet.</span></span> <span data-ttu-id="308fe-129">Finally, apply the updated configuration to the VM by using [Update-AzureVM](https://msdn.microsoft.com/library/mt589121.aspx).</span><span class="sxs-lookup"><span data-stu-id="308fe-129">Finally, apply the updated configuration to the VM by using [Update-AzureVM](https://msdn.microsoft.com/library/mt589121.aspx).</span></span>

    $VM = Get-AzureVM -ServiceName $Service_Name -Name $VM_Name
    $VM_Update = Set-AzureVMDiagnosticsExtension -DiagnosticsConfigurationPath $Config_Path -VM $VM -StorageContext $Storage_Context
    Update-AzureVM -ServiceName $Service_Name -Name $VM_Name -VM $VM_Update.VM

## <a name="sample-diagnostics-configuration"></a><span data-ttu-id="308fe-130">Sample diagnostics configuration</span><span class="sxs-lookup"><span data-stu-id="308fe-130">Sample diagnostics configuration</span></span>
<span data-ttu-id="308fe-131">The following XML can be used for the diagnostics public configuration with the above scripts.</span><span class="sxs-lookup"><span data-stu-id="308fe-131">The following XML can be used for the diagnostics public configuration with the above scripts.</span></span> <span data-ttu-id="308fe-132">This sample configuration will transfer various performance counters to the diagnostics storage account, along with errors from the application, security, and system channels in the Windows event logs and any errors from the diagnostics infrastructure logs.</span><span class="sxs-lookup"><span data-stu-id="308fe-132">This sample configuration will transfer various performance counters to the diagnostics storage account, along with errors from the application, security, and system channels in the Windows event logs and any errors from the diagnostics infrastructure logs.</span></span>

<span data-ttu-id="308fe-133">The configuration needs to be updated to include the following:</span><span class="sxs-lookup"><span data-stu-id="308fe-133">The configuration needs to be updated to include the following:</span></span>

* <span data-ttu-id="308fe-134">The *resourceID* attribute of the **Metrics** element needs to be updated with the resource ID for the VM.</span><span class="sxs-lookup"><span data-stu-id="308fe-134">The *resourceID* attribute of the **Metrics** element needs to be updated with the resource ID for the VM.</span></span>
  
  * <span data-ttu-id="308fe-135">The resource ID can be constructed by using the following pattern: "/subscriptions/{*subscription ID for the subscription with the VM*}/resourceGroups/{*The resourcegroup name for the VM*}/providers/Microsoft.Compute/virtualMachines/{*The VM Name*}".</span><span class="sxs-lookup"><span data-stu-id="308fe-135">The resource ID can be constructed by using the following pattern: "/subscriptions/{*subscription ID for the subscription with the VM*}/resourceGroups/{*The resourcegroup name for the VM*}/providers/Microsoft.Compute/virtualMachines/{*The VM Name*}".</span></span>
  * <span data-ttu-id="308fe-136">For example, if the subscription ID for the subscription where the VM is running is **11111111-1111-1111-1111-111111111111**, the resource group name for the resource group is **MyResourceGroup**, and the VM Name is **MyWindowsVM**, then the value for *resourceID* would be:</span><span class="sxs-lookup"><span data-stu-id="308fe-136">For example, if the subscription ID for the subscription where the VM is running is **11111111-1111-1111-1111-111111111111**, the resource group name for the resource group is **MyResourceGroup**, and the VM Name is **MyWindowsVM**, then the value for *resourceID* would be:</span></span>
    
      ```
      <Metrics resourceId="/subscriptions/11111111-1111-1111-1111-111111111111/resourceGroups/MyResourceGroup/providers/Microsoft.Compute/virtualMachines/MyWindowsVM" >
      ```
  * <span data-ttu-id="308fe-137">For more information on how metrics are generated based on the performance counters and metrics configuration, see [Azure Diagnostics metrics table in storage](extensions-diagnostics-template.md#wadmetrics-tables-in-storage).</span><span class="sxs-lookup"><span data-stu-id="308fe-137">For more information on how metrics are generated based on the performance counters and metrics configuration, see [Azure Diagnostics metrics table in storage](extensions-diagnostics-template.md#wadmetrics-tables-in-storage).</span></span>
* <span data-ttu-id="308fe-138">The **StorageAccount** element needs to be updated with the name of the diagnostics storage account.</span><span class="sxs-lookup"><span data-stu-id="308fe-138">The **StorageAccount** element needs to be updated with the name of the diagnostics storage account.</span></span>
  
    ```
    <?xml version="1.0" encoding="utf-8"?>
    <PublicConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
        <WadCfg>
          <DiagnosticMonitorConfiguration overallQuotaInMB="4096">
            <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter="Error"/>
            <PerformanceCounters scheduledTransferPeriod="PT1M">
          <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT15S" unit="Percent">
            <annotation displayName="CPU utilization" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Privileged Time" sampleRate="PT15S" unit="Percent">
            <annotation displayName="CPU privileged time" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% User Time" sampleRate="PT15S" unit="Percent">
            <annotation displayName="CPU user time" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Processor Information(_Total)\Processor Frequency" sampleRate="PT15S" unit="Count">
            <annotation displayName="CPU frequency" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\System\Processes" sampleRate="PT15S" unit="Count">
            <annotation displayName="Processes" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Process(_Total)\Thread Count" sampleRate="PT15S" unit="Count">
            <annotation displayName="Threads" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Process(_Total)\Handle Count" sampleRate="PT15S" unit="Count">
            <annotation displayName="Handles" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Memory\% Committed Bytes In Use" sampleRate="PT15S" unit="Percent">
            <annotation displayName="Memory usage" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Available Bytes" sampleRate="PT15S" unit="Bytes">
            <annotation displayName="Memory available" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Committed Bytes" sampleRate="PT15S" unit="Bytes">
            <annotation displayName="Memory committed" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Commit Limit" sampleRate="PT15S" unit="Bytes">
            <annotation displayName="Memory commit limit" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Pool Paged Bytes" sampleRate="PT15S" unit="Bytes">
            <annotation displayName="Memory paged pool" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Pool Nonpaged Bytes" sampleRate="PT15S" unit="Bytes">
            <annotation displayName="Memory non-paged pool" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\% Disk Time" sampleRate="PT15S" unit="Percent">
            <annotation displayName="Disk active time" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\% Disk Read Time" sampleRate="PT15S" unit="Percent">
            <annotation displayName="Disk active read time" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\% Disk Write Time" sampleRate="PT15S" unit="Percent">
            <annotation displayName="Disk active write time" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Disk Transfers/sec" sampleRate="PT15S" unit="CountPerSecond">
            <annotation displayName="Disk operations" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Disk Reads/sec" sampleRate="PT15S" unit="CountPerSecond">
            <annotation displayName="Disk read operations" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Disk Writes/sec" sampleRate="PT15S" unit="CountPerSecond">
            <annotation displayName="Disk write operations" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Disk Bytes/sec" sampleRate="PT15S" unit="BytesPerSecond">
            <annotation displayName="Disk speed" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Disk Read Bytes/sec" sampleRate="PT15S" unit="BytesPerSecond">
            <annotation displayName="Disk read speed" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Disk Write Bytes/sec" sampleRate="PT15S" unit="BytesPerSecond">
            <annotation displayName="Disk write speed" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Avg. Disk Queue Length" sampleRate="PT15S" unit="Count">
            <annotation displayName="Disk average queue length" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Avg. Disk Read Queue Length" sampleRate="PT15S" unit="Count">
            <annotation displayName="Disk average read queue length" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Avg. Disk Write Queue Length" sampleRate="PT15S" unit="Count">
            <annotation displayName="Disk average write queue length" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\LogicalDisk(_Total)\% Free Space" sampleRate="PT15S" unit="Percent">
            <annotation displayName="Disk free space (percentage)" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\LogicalDisk(_Total)\Free Megabytes" sampleRate="PT15S" unit="Count">
            <annotation displayName="Disk free space (MB)" locale="en-us"/>
          </PerformanceCounterConfiguration>
        </PerformanceCounters>
        <Metrics resourceId="(Update with resource ID for the VM)" >
            <MetricAggregation scheduledTransferPeriod="PT1H"/>
            <MetricAggregation scheduledTransferPeriod="PT1M"/>
        </Metrics>
        <WindowsEventLog scheduledTransferPeriod="PT1M">
          <DataSource name="Application!*[System[(Level = 1 or Level = 2)]]"/>
          <DataSource name="Security!*[System[(Level = 1 or Level = 2)]"/>
          <DataSource name="System!*[System[(Level = 1 or Level = 2)]]"/>
        </WindowsEventLog>
          </DiagnosticMonitorConfiguration>
        </WadCfg>
        <StorageAccount>(Update with diagnostics storage account name)</StorageAccount>
    </PublicConfig>
    ```

## <a name="next-steps"></a><span data-ttu-id="308fe-139">Next steps</span><span class="sxs-lookup"><span data-stu-id="308fe-139">Next steps</span></span>
* <span data-ttu-id="308fe-140">For additional guidance on using the Azure Diagnostics capability and other techniques to troubleshoot problems, see [Enabling Diagnostics in Azure Cloud Services and Virtual Machines](../../cloud-services/cloud-services-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="308fe-140">For additional guidance on using the Azure Diagnostics capability and other techniques to troubleshoot problems, see [Enabling Diagnostics in Azure Cloud Services and Virtual Machines](../../cloud-services/cloud-services-dotnet-diagnostics.md).</span></span>
* <span data-ttu-id="308fe-141">[Diagnostics configurations schema](https://msdn.microsoft.com/library/azure/mt634524.aspx) explains the various XML configurations options for the diagnostics extension.</span><span class="sxs-lookup"><span data-stu-id="308fe-141">[Diagnostics configurations schema](https://msdn.microsoft.com/library/azure/mt634524.aspx) explains the various XML configurations options for the diagnostics extension.</span></span>

