---
title: Configure private IP addresses for VMs (Classic) - Azure PowerShell | Microsoft Docs
description: Learn how to configure private IP addresses for virtual machines (Classic) using PowerShell.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 60c7b489-46ae-48af-a453-2b429a474afd
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5da2992fad89a703086b7645c88f6d8e1a39e4b3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562742"
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-classic-using-powershell"></a><span data-ttu-id="a9803-103">Configure private IP addresses for a virtual machine (Classic) using PowerShell</span><span class="sxs-lookup"><span data-stu-id="a9803-103">Configure private IP addresses for a virtual machine (Classic) using PowerShell</span></span>

[!INCLUDE [virtual-networks-static-private-ip-selectors-classic-include](../../includes/virtual-networks-static-private-ip-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="a9803-104">This article covers the classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="a9803-104">This article covers the classic deployment model.</span></span> <span data-ttu-id="a9803-105">You can also [manage a static private IP address in the Resource Manager deployment model](virtual-networks-static-private-ip-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="a9803-105">You can also [manage a static private IP address in the Resource Manager deployment model](virtual-networks-static-private-ip-arm-ps.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

<span data-ttu-id="a9803-106">The sample PowerShell commands below expect a simple environment already created.</span><span class="sxs-lookup"><span data-stu-id="a9803-106">The sample PowerShell commands below expect a simple environment already created.</span></span> <span data-ttu-id="a9803-107">If you want to run the commands as they are displayed in this document, first build the test environment described in [Create a VNet](virtual-networks-create-vnet-classic-netcfg-ps.md).</span><span class="sxs-lookup"><span data-stu-id="a9803-107">If you want to run the commands as they are displayed in this document, first build the test environment described in [Create a VNet](virtual-networks-create-vnet-classic-netcfg-ps.md).</span></span>

## <a name="how-to-verify-if-a-specific-ip-address-is-available"></a><span data-ttu-id="a9803-108">How to verify if a specific IP address is available</span><span class="sxs-lookup"><span data-stu-id="a9803-108">How to verify if a specific IP address is available</span></span>
<span data-ttu-id="a9803-109">To verify if the IP address *192.168.1.101* is available in a VNet named *TestVNet*, run the following PowerShell command and verify the value for *IsAvailable*:</span><span class="sxs-lookup"><span data-stu-id="a9803-109">To verify if the IP address *192.168.1.101* is available in a VNet named *TestVNet*, run the following PowerShell command and verify the value for *IsAvailable*:</span></span>

    Test-AzureStaticVNetIP –VNetName TestVNet –IPAddress 192.168.1.101 

<span data-ttu-id="a9803-110">Expected output:</span><span class="sxs-lookup"><span data-stu-id="a9803-110">Expected output:</span></span>

    IsAvailable          : True
    AvailableAddresses   : {}
    OperationDescription : Test-AzureStaticVNetIP
    OperationId          : fd3097e1-5f4b-9cac-8afa-bba1e3492609
    OperationStatus      : Succeeded

## <a name="how-to-specify-a-static-private-ip-address-when-creating-a-vm"></a><span data-ttu-id="a9803-111">How to specify a static private IP address when creating a VM</span><span class="sxs-lookup"><span data-stu-id="a9803-111">How to specify a static private IP address when creating a VM</span></span>
<span data-ttu-id="a9803-112">The PowerShell script below creates a new cloud service named *TestService*, then retrieves an image from Azure, creates a VM named *DNS01* in the new cloud service using the retrieved image, sets the VM to be in a subnet named *FrontEnd*, and sets *192.168.1.7* as a static private IP address for the VM:</span><span class="sxs-lookup"><span data-stu-id="a9803-112">The PowerShell script below creates a new cloud service named *TestService*, then retrieves an image from Azure, creates a VM named *DNS01* in the new cloud service using the retrieved image, sets the VM to be in a subnet named *FrontEnd*, and sets *192.168.1.7* as a static private IP address for the VM:</span></span>

    New-AzureService -ServiceName TestService -Location "Central US"
    $image = Get-AzureVMImage | where {$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}
    New-AzureVMConfig -Name DNS01 -InstanceSize Small -ImageName $image.ImageName |
      Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! |
      Set-AzureSubnet –SubnetNames FrontEnd |
      Set-AzureStaticVNetIP -IPAddress 192.168.1.7 |
      New-AzureVM -ServiceName TestService –VNetName TestVNet

<span data-ttu-id="a9803-113">Expected output:</span><span class="sxs-lookup"><span data-stu-id="a9803-113">Expected output:</span></span>

    WARNING: No deployment found in service: 'TestService'.
    OperationDescription OperationId                          OperationStatus
    -------------------- -----------                          ---------------
    New-AzureService     fcf705f1-d902-011c-95c7-b690735e7412 Succeeded      
    New-AzureVM          3b99a86d-84f8-04e5-888e-b6fc3c73c4b9 Succeeded  

## <a name="how-to-retrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="a9803-114">How to retrieve static private IP address information for a VM</span><span class="sxs-lookup"><span data-stu-id="a9803-114">How to retrieve static private IP address information for a VM</span></span>
<span data-ttu-id="a9803-115">To view the static private IP address information for the VM created with the script above, run the following PowerShell command and observe the values for *IpAddress*:</span><span class="sxs-lookup"><span data-stu-id="a9803-115">To view the static private IP address information for the VM created with the script above, run the following PowerShell command and observe the values for *IpAddress*:</span></span>

    Get-AzureVM -Name DNS01 -ServiceName TestService

<span data-ttu-id="a9803-116">Expected output:</span><span class="sxs-lookup"><span data-stu-id="a9803-116">Expected output:</span></span>

    DeploymentName              : TestService
    Name                        : DNS01
    Label                       : 
    VM                          : Microsoft.WindowsAzure.Commands.ServiceManagement.Model.PersistentVM
    InstanceStatus              : Provisioning
    IpAddress                   : 192.168.1.7
    InstanceStateDetails        : Windows is preparing your computer for first use...
    PowerState                  : Started
    InstanceErrorCode           : 
    InstanceFaultDomain         : 0
    InstanceName                : DNS01
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

## <a name="how-to-remove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="a9803-117">How to remove a static private IP address from a VM</span><span class="sxs-lookup"><span data-stu-id="a9803-117">How to remove a static private IP address from a VM</span></span>
<span data-ttu-id="a9803-118">To remove the static private IP address added to the VM in the script above, run the following PowerShell command:</span><span class="sxs-lookup"><span data-stu-id="a9803-118">To remove the static private IP address added to the VM in the script above, run the following PowerShell command:</span></span>

    Get-AzureVM -ServiceName TestService -Name DNS01 |
      Remove-AzureStaticVNetIP |
      Update-AzureVM

<span data-ttu-id="a9803-119">Expected output:</span><span class="sxs-lookup"><span data-stu-id="a9803-119">Expected output:</span></span>

    OperationDescription OperationId                          OperationStatus
    -------------------- -----------                          ---------------
    Update-AzureVM       052fa6f6-1483-0ede-a7bf-14f91f805483 Succeeded

## <a name="how-to-add-a-static-private-ip-address-to-an-existing-vm"></a><span data-ttu-id="a9803-120">How to add a static private IP address to an existing VM</span><span class="sxs-lookup"><span data-stu-id="a9803-120">How to add a static private IP address to an existing VM</span></span>
<span data-ttu-id="a9803-121">To add a static private IP address to the VM created using the script above, runt he following command:</span><span class="sxs-lookup"><span data-stu-id="a9803-121">To add a static private IP address to the VM created using the script above, runt he following command:</span></span>

    Get-AzureVM -ServiceName TestService -Name DNS01 |
      Set-AzureStaticVNetIP -IPAddress 192.168.1.7 |
      Update-AzureVM

<span data-ttu-id="a9803-122">Expected output:</span><span class="sxs-lookup"><span data-stu-id="a9803-122">Expected output:</span></span>

    OperationDescription OperationId                          OperationStatus
    -------------------- -----------                          ---------------
    Update-AzureVM       77d8cae2-87e6-0ead-9738-7c7dae9810cb Succeeded 

## <a name="next-steps"></a><span data-ttu-id="a9803-123">Next steps</span><span class="sxs-lookup"><span data-stu-id="a9803-123">Next steps</span></span>
* <span data-ttu-id="a9803-124">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span><span class="sxs-lookup"><span data-stu-id="a9803-124">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="a9803-125">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span><span class="sxs-lookup"><span data-stu-id="a9803-125">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="a9803-126">Consult the [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span><span class="sxs-lookup"><span data-stu-id="a9803-126">Consult the [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

