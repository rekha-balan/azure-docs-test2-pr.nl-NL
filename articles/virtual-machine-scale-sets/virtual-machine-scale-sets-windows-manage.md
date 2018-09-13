---
title: Manage VMs in a Virtual Machine Scale Set | Microsoft Docs
description: Manage virtual machines in a virtual machine scale set using Azure PowerShell.
services: virtual-machine-scale-sets
documentationcenter: ''
author: Thraka
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: d35fa77a-de96-4ccd-a332-eb181d1f4273
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/27/2016
ms.author: adegeo
ms.openlocfilehash: ea6e9b0feb9891b0839fcfcd5fdd7dc8c7c488aa
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556645"
---
# <a name="manage-virtual-machines-in-a-virtual-machine-scale-set"></a><span data-ttu-id="56f32-103">Manage virtual machines in a virtual machine scale set</span><span class="sxs-lookup"><span data-stu-id="56f32-103">Manage virtual machines in a virtual machine scale set</span></span>
<span data-ttu-id="56f32-104">Use the tasks in this article to manage virtual machines in your virtual machine scale set.</span><span class="sxs-lookup"><span data-stu-id="56f32-104">Use the tasks in this article to manage virtual machines in your virtual machine scale set.</span></span>

<span data-ttu-id="56f32-105">Most of the tasks that involve managing a virtual machine in a scale set require that you know the instance ID of the machine that you want to manage.</span><span class="sxs-lookup"><span data-stu-id="56f32-105">Most of the tasks that involve managing a virtual machine in a scale set require that you know the instance ID of the machine that you want to manage.</span></span> <span data-ttu-id="56f32-106">You can use [Azure Resource Explorer](https://resources.azure.com) to find the instance ID of a virtual machine in a scale set.</span><span class="sxs-lookup"><span data-stu-id="56f32-106">You can use [Azure Resource Explorer](https://resources.azure.com) to find the instance ID of a virtual machine in a scale set.</span></span> <span data-ttu-id="56f32-107">You also use Resource Explorer to verify the status of the tasks that you finish.</span><span class="sxs-lookup"><span data-stu-id="56f32-107">You also use Resource Explorer to verify the status of the tasks that you finish.</span></span>

<span data-ttu-id="56f32-108">See [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for information about installing the latest version of Azure PowerShell, selecting your subscription, and signing in to your account.</span><span class="sxs-lookup"><span data-stu-id="56f32-108">See [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for information about installing the latest version of Azure PowerShell, selecting your subscription, and signing in to your account.</span></span>

## <a name="display-information-about-a-scale-set"></a><span data-ttu-id="56f32-109">Display information about a scale set</span><span class="sxs-lookup"><span data-stu-id="56f32-109">Display information about a scale set</span></span>
<span data-ttu-id="56f32-110">You can get general information about a scale set, which is also referred to as the instance view.</span><span class="sxs-lookup"><span data-stu-id="56f32-110">You can get general information about a scale set, which is also referred to as the instance view.</span></span> <span data-ttu-id="56f32-111">Or, you can get more specific information, such as information about the resources in the scale set.</span><span class="sxs-lookup"><span data-stu-id="56f32-111">Or, you can get more specific information, such as information about the resources in the scale set.</span></span>

<span data-ttu-id="56f32-112">Replace the quoted values with the name or your resource group and scale set and then run the command:</span><span class="sxs-lookup"><span data-stu-id="56f32-112">Replace the quoted values with the name or your resource group and scale set and then run the command:</span></span>

    Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name"

<span data-ttu-id="56f32-113">It returns something like this:</span><span class="sxs-lookup"><span data-stu-id="56f32-113">It returns something like this:</span></span>

    Id                                          : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Compute/virtualMachineScaleSets/myvmss1
    Name                                        : myvmss1
    Type                                        : Microsoft.Compute/virtualMachineScaleSets
    Location                                    : centralus
    Sku                                         :
      Name                                      : Standard_A0
      Tier                                      : Standard
      Capacity                                  : 3
    UpgradePolicy                               :
      Mode                                      : Manual
    VirtualMachineProfile                       :
      OsProfile                                 :
        ComputerNamePrefix                      : vmss1
        AdminUsername                           : admin1
        WindowsConfiguration                    :
          ProvisionVMAgent                      : True
          EnableAutomaticUpdates                : True
    StorageProfile                              :
      ImageReference                            :
        Publisher                               : MicrosoftWindowsServer
        Offer                                   : WindowsServer
        Sku                                     : 2012-R2-Datacenter
        Version                                 : latest
      OsDisk                                    :
        Name                                    : vmssosdisk
        Caching                                 : ReadOnly
        CreateOption                            : FromImage
        VhdContainers[0]                        : https://astore.blob.core.windows.net/vmss
        VhdContainers[1]                        : https://gstore.blob.core.windows.net/vmss
        VhdContainers[2]                        : https://mstore.blob.core.windows.net/vmss
        VhdContainers[3]                        : https://sstore.blob.core.windows.net/vmss
        VhdContainers[4]                        : https://ystore.blob.core.windows.net/vmss
    NetworkProfile                              :
      NetworkInterfaceConfigurations[0]         :
        Name                                    : mync1
        Primary                                 : True
        IpConfigurations[0]                     :
          Name                                  : ip1
          Subnet                                :
            Id                                  : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Network/virtualNetworks/myvn1/subnets/mysn1
          LoadBalancerBackendAddressPools[0]    :
            Id                                  : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Network/loadBalancers/mylb1/backendAddressPools/bepool1
        LoadBalancerInboundNatPools[0]          :
            Id                                  : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Network/loadBalancers/mylb1/inboundNatPools/natpool1
    ExtensionProfile                            :
      Extensions[0]                             :
        Name                                    : Microsoft.Insights.VMDiagnosticsSettings
        Publisher                               : Microsoft.Azure.Diagnostics
        Type                                    : IaaSDiagnostics
        TypeHandlerVersion                      : 1.5
        AutoUpgradeMinorVersion                 : True
        Settings                                : {"xmlCfg":"...","storageAccount":"astore"}
    ProvisioningState                           : Succeeded

<span data-ttu-id="56f32-114">Replace the quoted values with the name of your resource group and scale set.</span><span class="sxs-lookup"><span data-stu-id="56f32-114">Replace the quoted values with the name of your resource group and scale set.</span></span> <span data-ttu-id="56f32-115">Replace *#* with the instance identifier of the virtual machine that you want to get information about and then run it:</span><span class="sxs-lookup"><span data-stu-id="56f32-115">Replace *#* with the instance identifier of the virtual machine that you want to get information about and then run it:</span></span>

    Get-AzureRmVmssVM -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

<span data-ttu-id="56f32-116">It returns something like this example:</span><span class="sxs-lookup"><span data-stu-id="56f32-116">It returns something like this example:</span></span>

    Id                            : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Compute/
                                    virtualMachineScaleSets/myvmss1/virtualMachines/0
    Name                          : myvmss1_0
    Type                          : Microsoft.Compute/virtualMachineScaleSets/virtualMachines
    Location                      : centralus
    InstanceId                    : 0
    Sku                           :
      Name                        : Standard_A0
      Tier                        : Standard
    LatestModelApplied            : True
    StorageProfile                :
      ImageReference              :
        Publisher                 : MicrosoftWindowsServer
        Offer                     : WindowsServer
        Sku                       : 2012-R2-Datacenter
        Version                   : 4.0.20160617
      OsDisk                      :
        OsType                    : Windows
        Name                      : vmssosdisk-os-0-e11cad52959b4b76a8d9f26c5190c4f8
        Vhd                       :
          Uri                     : https://astore.blob.core.windows.net/vmss/vmssosdisk-os-0-e11cad52959b4b76a8d9f26c5190c4f8.vhd
        Caching                   : ReadOnly
        CreateOption              : FromImage
    OsProfile                     :
      ComputerName                : myvmss1-0
      AdminUsername               : admin1
      WindowsConfiguration        :
        ProvisionVMAgent          : True
        EnableAutomaticUpdates    : True
    NetworkProfile                :
      NetworkInterfaces[0]        :
        Id                        : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Compute/virtualMachineScaleSets/
                                    myvmss1/virtualMachines/0/networkInterfaces/mync1
    ProvisioningState             : Succeeded
    Resources[0]                  :
      Id                          : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Compute/virtualMachines/
                                    myvmss1_0/extensions/Microsoft.Insights.VMDiagnosticsSettings
      Name                        : Microsoft.Insights.VMDiagnosticsSettings
      Type                        : Microsoft.Compute/virtualMachines/extensions
      Location                    : centralus
      Publisher                   : Microsoft.Azure.Diagnostics
      VirtualMachineExtensionType : IaaSDiagnostics
      TypeHandlerVersion          : 1.5
      AutoUpgradeMinorVersion     : True
      Settings                    : {"xmlCfg":"...","storageAccount":"astore"}
      ProvisioningState           : Succeeded

## <a name="start-a-virtual-machine-in-a-scale-set"></a><span data-ttu-id="56f32-117">Start a virtual machine in a scale set</span><span class="sxs-lookup"><span data-stu-id="56f32-117">Start a virtual machine in a scale set</span></span>
<span data-ttu-id="56f32-118">Replace the quoted values with the name of your resource group and scale set.</span><span class="sxs-lookup"><span data-stu-id="56f32-118">Replace the quoted values with the name of your resource group and scale set.</span></span> <span data-ttu-id="56f32-119">Replace *#* with the identifier of the virtual machine that you want to start and then run it:</span><span class="sxs-lookup"><span data-stu-id="56f32-119">Replace *#* with the identifier of the virtual machine that you want to start and then run it:</span></span>

    Start-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

<span data-ttu-id="56f32-120">In Resource Explorer, we can see that the status of the instance is **running**:</span><span class="sxs-lookup"><span data-stu-id="56f32-120">In Resource Explorer, we can see that the status of the instance is **running**:</span></span>

    "statuses": [
      {
        "code": "ProvisioningState/succeeded",
        "level": "Info",
        "displayStatus": "Provisioning succeeded",
        "time": "2016-03-15T02:10:08.0730839+00:00"
      },
      {
        "code": "PowerState/running",
        "level": "Info",
        "displayStatus": "VM running"
      }
    ]

<span data-ttu-id="56f32-121">You can start all the virtual machines in the scale set by not using the -InstanceId parameter.</span><span class="sxs-lookup"><span data-stu-id="56f32-121">You can start all the virtual machines in the scale set by not using the -InstanceId parameter.</span></span>

## <a name="stop-a-virtual-machine-in-a-scale-set"></a><span data-ttu-id="56f32-122">Stop a virtual machine in a scale set</span><span class="sxs-lookup"><span data-stu-id="56f32-122">Stop a virtual machine in a scale set</span></span>
<span data-ttu-id="56f32-123">Replace the quoted values with the name of your resource group and scale set.</span><span class="sxs-lookup"><span data-stu-id="56f32-123">Replace the quoted values with the name of your resource group and scale set.</span></span> <span data-ttu-id="56f32-124">Replace *#* with the identifier of the virtual machine that you want to stop and then run it:</span><span class="sxs-lookup"><span data-stu-id="56f32-124">Replace *#* with the identifier of the virtual machine that you want to stop and then run it:</span></span>

    Stop-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

<span data-ttu-id="56f32-125">In Resource Explorer, we can see that the status of the instance is **deallocated**:</span><span class="sxs-lookup"><span data-stu-id="56f32-125">In Resource Explorer, we can see that the status of the instance is **deallocated**:</span></span>

    "statuses": [
      {
        "code": "ProvisioningState/succeeded",
        "level": "Info",
        "displayStatus": "Provisioning succeeded",
        "time": "2016-03-15T01:25:17.8792929+00:00"
      },
      {
        "code": "PowerState/deallocated",
        "level": "Info",
        "displayStatus": "VM deallocated"
      }
    ]

<span data-ttu-id="56f32-126">To stop a virtual machine and not deallocate it, use the -StayProvisioned parameter.</span><span class="sxs-lookup"><span data-stu-id="56f32-126">To stop a virtual machine and not deallocate it, use the -StayProvisioned parameter.</span></span> <span data-ttu-id="56f32-127">You can stop all the virtual machines in the set by not using the -InstanceId parameter.</span><span class="sxs-lookup"><span data-stu-id="56f32-127">You can stop all the virtual machines in the set by not using the -InstanceId parameter.</span></span>

## <a name="restart-a-virtual-machine-in-a-scale-set"></a><span data-ttu-id="56f32-128">Restart a virtual machine in a scale set</span><span class="sxs-lookup"><span data-stu-id="56f32-128">Restart a virtual machine in a scale set</span></span>
<span data-ttu-id="56f32-129">Replace the quoted values with the name of your resource group and the scale set.</span><span class="sxs-lookup"><span data-stu-id="56f32-129">Replace the quoted values with the name of your resource group and the scale set.</span></span> <span data-ttu-id="56f32-130">Replace *#* with the identifier of the virtual machine that you want to restart and then run it:</span><span class="sxs-lookup"><span data-stu-id="56f32-130">Replace *#* with the identifier of the virtual machine that you want to restart and then run it:</span></span>

    Restart-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

<span data-ttu-id="56f32-131">You can restart all the virtual machines in the set by not using the -InstanceId parameter.</span><span class="sxs-lookup"><span data-stu-id="56f32-131">You can restart all the virtual machines in the set by not using the -InstanceId parameter.</span></span>

## <a name="remove-a-virtual-machine-from-a-scale-set"></a><span data-ttu-id="56f32-132">Remove a virtual machine from a scale set</span><span class="sxs-lookup"><span data-stu-id="56f32-132">Remove a virtual machine from a scale set</span></span>
<span data-ttu-id="56f32-133">Replace the quoted values with the name of your resource group and the scale set.</span><span class="sxs-lookup"><span data-stu-id="56f32-133">Replace the quoted values with the name of your resource group and the scale set.</span></span> <span data-ttu-id="56f32-134">Replace *#* with the identifier of the virtual machine that you want to remove and then run it:</span><span class="sxs-lookup"><span data-stu-id="56f32-134">Replace *#* with the identifier of the virtual machine that you want to remove and then run it:</span></span>  

    Remove-AzureRmVmss -ResourceGroupName "resource group name" –VMScaleSetName "scale set name" -InstanceId #

<span data-ttu-id="56f32-135">You can remove the virtual machine scale set all at once by not using the -InstanceId parameter.</span><span class="sxs-lookup"><span data-stu-id="56f32-135">You can remove the virtual machine scale set all at once by not using the -InstanceId parameter.</span></span>

## <a name="change-the-capacity-of-a-scale-set"></a><span data-ttu-id="56f32-136">Change the capacity of a scale set</span><span class="sxs-lookup"><span data-stu-id="56f32-136">Change the capacity of a scale set</span></span>
<span data-ttu-id="56f32-137">You can add or remove virtual machines by changing the capacity of the set.</span><span class="sxs-lookup"><span data-stu-id="56f32-137">You can add or remove virtual machines by changing the capacity of the set.</span></span> <span data-ttu-id="56f32-138">Get the scale set that you want to change, set the capacity to what you want it to be, and then update the scale set with the new capacity.</span><span class="sxs-lookup"><span data-stu-id="56f32-138">Get the scale set that you want to change, set the capacity to what you want it to be, and then update the scale set with the new capacity.</span></span> <span data-ttu-id="56f32-139">In these commands, replace the quoted values with the name of your resource group and the scale set.</span><span class="sxs-lookup"><span data-stu-id="56f32-139">In these commands, replace the quoted values with the name of your resource group and the scale set.</span></span>

    $vmss = Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name"
    $vmss.sku.capacity = 5
    Update-AzureRmVmss -ResourceGroupName "resource group name" -Name "scale set name" -VirtualMachineScaleSet $vmss 

<span data-ttu-id="56f32-140">If you are removing virtual machines from the scale set, the virtual machines with the highest ids are removed first.</span><span class="sxs-lookup"><span data-stu-id="56f32-140">If you are removing virtual machines from the scale set, the virtual machines with the highest ids are removed first.</span></span>

