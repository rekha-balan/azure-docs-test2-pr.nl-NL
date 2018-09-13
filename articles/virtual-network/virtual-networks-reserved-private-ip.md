---
title: Static internal private IP - Azure VM - Classic
description: Understanding static internal IPs (DIPs) and how to manage them
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
ms.assetid: 93444c6f-af1b-41f8-a035-77f5c0302bf0
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/22/2016
ms.author: jdial
ms.openlocfilehash: d2e2effa9c215107cf0893a74df0b909fbf5d4c0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44548861"
---
# <a name="how-to-set-a-static-internal-private-ip-address-using-powershell-classic"></a>How to set a static internal private IP address using PowerShell (Classic)
In most cases, you won’t need to specify a static internal IP address for your virtual machine. VMs in a virtual network will automatically receive an internal IP address from a range that you specify. But in certain cases, specifying a static IP address for a particular VM makes sense. For example, if your VM is going to run DNS or will be a domain controller. A static internal IP address stays with the VM even through a stop/deprovision state. 

> [!IMPORTANT]
> Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md). This article covers using the classic deployment model. Microsoft recommends that most new deployments use the [Resource Manager deployment model](virtual-networks-static-private-ip-arm-ps.md).
> 
> 

## <a name="how-to-verify-if-a-specific-ip-address-is-available"></a>How to verify if a specific IP address is available
To verify if the IP address *10.0.0.7* is available in a vnet named *TestVnet*, run the following PowerShell command and verify the value for *IsAvailable*:

    Test-AzureStaticVNetIP –VNetName TestVNet –IPAddress 10.0.0.7 

    IsAvailable          : True
    AvailableAddresses   : {}
    OperationDescription : Test-AzureStaticVNetIP
    OperationId          : fd3097e1-5f4b-9cac-8afa-bba1e3492609
    OperationStatus      : Succeeded

> [!NOTE]
> If you want to test the command above in a safe environment follow the guidelines in [Create a Virtual Network](virtual-networks-create-vnet-classic-portal.md) to create a vnet named *TestVnet* and ensure it uses the *10.0.0.0/8* address space.
> 
> 

## <a name="how-to-specify-a-static-internal-ip-when-creating-a-vm"></a>How to specify a static internal IP when creating a VM
The PowerShell script below creates a new cloud service named *TestService*, then retrieves an image from Azure, then creates a VM named *TestVM* in the new cloud service using the retrieved image, sets the VM to be in a subnet named *Subnet-1*, and sets *10.0.0.7* as a static internal IP for the VM:

    New-AzureService -ServiceName TestService -Location "Central US"
    $image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}
    New-AzureVMConfig -Name TestVM -InstanceSize Small -ImageName $image.ImageName `
    | Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
    | Set-AzureSubnet –SubnetNames Subnet-1 `
    | Set-AzureStaticVNetIP -IPAddress 10.0.0.7 `
    | New-AzureVM -ServiceName "TestService" –VNetName TestVnet

## <a name="how-to-retrieve-static-internal-ip-information-for-a-vm"></a>How to retrieve static internal IP information for a VM
To view the static internal IP information for the VM created with the script above, run the following PowerShell command and observe the values for *IpAddress*:

    Get-AzureVM -Name TestVM -ServiceName TestService

    DeploymentName              : TestService
    Name                        : TestVM
    Label                       : 
    VM                          : Microsoft.WindowsAzure.Commands.ServiceManagement.Model.PersistentVM
    InstanceStatus              : Provisioning
    IpAddress                   : 10.0.0.7
    InstanceStateDetails        : Windows is preparing your computer for first use...
    PowerState                  : Started
    InstanceErrorCode           : 
    InstanceFaultDomain         : 0
    InstanceName                : TestVM
    InstanceUpgradeDomain       : 0
    InstanceSize                : Small
    HostName                    : rsR2-797
    AvailabilitySetName         : 
    DNSName                     : http://testservice000.cloudapp.net/
    Status                      : Provisioning
    GuestAgentStatus            : Microsoft.WindowsAzure.Commands.ServiceManagement.Model.GuestAgentStatus
    ResourceExtensionStatusList : {Microsoft.Compute.BGInfo}
    PublicIPAddress             : 
    PublicIPName                : 
    NetworkInterfaces           : {}
    ServiceName                 : TestService
    OperationDescription        : Get-AzureVM
    OperationId                 : 34c1560a62f0901ab75cde4fed8e8bd1
    OperationStatus             : OK

## <a name="how-to-remove-a-static-internal-ip-from-a-vm"></a>How to remove a static internal IP from a VM
To remove the static internal IP added to the VM in the script above, run the following PowerShell command:

    Get-AzureVM -ServiceName TestService -Name TestVM `
    | Remove-AzureStaticVNetIP `
    | Update-AzureVM

## <a name="how-to-add-a-static-internal-ip-to-an-existing-vm"></a>How to add a static internal IP to an existing VM
To add a static internal IP to the VM created using the script above, runt he following command:

    Get-AzureVM -ServiceName TestService000 -Name TestVM `
    | Set-AzureStaticVNetIP -IPAddress 10.10.0.7 `
    | Update-AzureVM

## <a name="next-steps"></a>Next steps
[Reserved IP](virtual-networks-reserved-public-ip.md)

[Instance-Level Public IP (ILPIP)](virtual-networks-instance-level-public-ip.md)

[Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx)

