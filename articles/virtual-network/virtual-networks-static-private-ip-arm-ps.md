---
title: Configure private IP addresses for VMs - Azure PowerShell | Microsoft Docs
description: Learn how to configure private IP addresses for virtual machines using PowerShell.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: d5f18929-15e3-40a2-9ee3-8188bc248ed8
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/23/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2810190897c44c944912ef3325b1f40479aa3078
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552989"
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-powershell"></a><span data-ttu-id="4e895-103">Configure private IP addresses for a virtual machine using PowerShell</span><span class="sxs-lookup"><span data-stu-id="4e895-103">Configure private IP addresses for a virtual machine using PowerShell</span></span>

[!INCLUDE [virtual-networks-static-private-ip-selectors-arm-include](../../includes/virtual-networks-static-private-ip-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

<span data-ttu-id="4e895-104">Azure has two deployment models: Azure Resource Manager and classic.</span><span class="sxs-lookup"><span data-stu-id="4e895-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="4e895-105">Microsoft recommends creating resources through the Resource Manager deployment model.</span><span class="sxs-lookup"><span data-stu-id="4e895-105">Microsoft recommends creating resources through the Resource Manager deployment model.</span></span> <span data-ttu-id="4e895-106">To learn more about the differences between the two models, read the [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span><span class="sxs-lookup"><span data-stu-id="4e895-106">To learn more about the differences between the two models, read the [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span> <span data-ttu-id="4e895-107">This article covers the Resource Manager deployment model.</span><span class="sxs-lookup"><span data-stu-id="4e895-107">This article covers the Resource Manager deployment model.</span></span> <span data-ttu-id="4e895-108">You can also [manage static private IP address in the classic deployment model](virtual-networks-static-private-ip-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="4e895-108">You can also [manage static private IP address in the classic deployment model](virtual-networks-static-private-ip-classic-ps.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

<span data-ttu-id="4e895-109">The sample PowerShell commands below expect a simple environment already created based on the scenario above.</span><span class="sxs-lookup"><span data-stu-id="4e895-109">The sample PowerShell commands below expect a simple environment already created based on the scenario above.</span></span> <span data-ttu-id="4e895-110">If you want to run the commands as they are displayed in this document, first build the test environment described in [create a vnet](virtual-networks-create-vnet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="4e895-110">If you want to run the commands as they are displayed in this document, first build the test environment described in [create a vnet](virtual-networks-create-vnet-arm-ps.md).</span></span>

## <a name="create-a-vm-with-a-static-private-ip-address"></a><span data-ttu-id="4e895-111">Create a VM with a static private IP address</span><span class="sxs-lookup"><span data-stu-id="4e895-111">Create a VM with a static private IP address</span></span>
<span data-ttu-id="4e895-112">To create a VM named *DNS01* in the *FrontEnd* subnet of a VNet named *TestVNet* with a static private IP of *192.168.1.101*, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="4e895-112">To create a VM named *DNS01* in the *FrontEnd* subnet of a VNet named *TestVNet* with a static private IP of *192.168.1.101*, follow the steps below:</span></span>

1. <span data-ttu-id="4e895-113">Set variables for the storage account, location, resource group, and credentials to be used.</span><span class="sxs-lookup"><span data-stu-id="4e895-113">Set variables for the storage account, location, resource group, and credentials to be used.</span></span> <span data-ttu-id="4e895-114">You will need to enter a user name and password for the VM.</span><span class="sxs-lookup"><span data-stu-id="4e895-114">You will need to enter a user name and password for the VM.</span></span> <span data-ttu-id="4e895-115">The storage account and resource group must already exist.</span><span class="sxs-lookup"><span data-stu-id="4e895-115">The storage account and resource group must already exist.</span></span>

    ```powershell
    $stName  = "vnetstorage"
    $locName = "Central US"
    $rgName  = "TestRG"
    $cred    = Get-Credential -Message "Type the name and password of the local administrator account."
    ```

2. <span data-ttu-id="4e895-116">Retrieve the virtual network and subnet you want to create the VM in.</span><span class="sxs-lookup"><span data-stu-id="4e895-116">Retrieve the virtual network and subnet you want to create the VM in.</span></span>

    ```powershell
    $vnet   = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    $subnet = $vnet.Subnets[0].Id
    ```

3. <span data-ttu-id="4e895-117">If necessary, create a public IP address to access the VM from the Internet.</span><span class="sxs-lookup"><span data-stu-id="4e895-117">If necessary, create a public IP address to access the VM from the Internet.</span></span>

    ```powershell
    $pip = New-AzureRmPublicIpAddress -Name TestPIP -ResourceGroupName $rgName `
    -Location $locName -AllocationMethod Dynamic
    ```

4. <span data-ttu-id="4e895-118">Create a NIC using the static private IP address you want to assign to the VM.</span><span class="sxs-lookup"><span data-stu-id="4e895-118">Create a NIC using the static private IP address you want to assign to the VM.</span></span> <span data-ttu-id="4e895-119">Make sure the IP is from the subnet range you are adding the VM to.</span><span class="sxs-lookup"><span data-stu-id="4e895-119">Make sure the IP is from the subnet range you are adding the VM to.</span></span> <span data-ttu-id="4e895-120">This is the main step for this article, where you set the private IP to be static.</span><span class="sxs-lookup"><span data-stu-id="4e895-120">This is the main step for this article, where you set the private IP to be static.</span></span>

    ```powershell
    $nic = New-AzureRmNetworkInterface -Name TestNIC -ResourceGroupName $rgName `
    -Location $locName -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id `
    -PrivateIpAddress 192.168.1.101
    ```

5. <span data-ttu-id="4e895-121">Create the VM using the NIC created above.</span><span class="sxs-lookup"><span data-stu-id="4e895-121">Create the VM using the NIC created above.</span></span>

    ```powershell
    $vm = New-AzureRmVMConfig -VMName DNS01 -VMSize "Standard_A1"
    $vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName DNS01 `
    -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm = Set-AzureRmVMSourceImage -VM $vm -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
    $osDiskUri = $storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/WindowsVMosDisk.vhd"
    $vm = Set-AzureRmVMOSDisk -VM $vm -Name "windowsvmosdisk" -VhdUri $osDiskUri `
    -CreateOption fromImage
    New-AzureRmVM -ResourceGroupName $rgName -Location $locName -VM $vm 
    ```

    <span data-ttu-id="4e895-122">Expected output:</span><span class="sxs-lookup"><span data-stu-id="4e895-122">Expected output:</span></span>
    
        EndTime             : [Date and time]
        Error               : 
        Output              : 
        StartTime           : [Date and time]
        Status              : Succeeded
        TrackingOperationId : [Id]
        RequestId           : [Id]
        StatusCode          : OK 

## <a name="retrieve-static-private-ip-address-information-for-a-network-interface"></a><span data-ttu-id="4e895-123">Retrieve static private IP address information for a network interface</span><span class="sxs-lookup"><span data-stu-id="4e895-123">Retrieve static private IP address information for a network interface</span></span>
<span data-ttu-id="4e895-124">To view the static private IP address information for the VM created with the script above, run the following PowerShell command and observe the values for *PrivateIpAddress* and *PrivateIpAllocationMethod*:</span><span class="sxs-lookup"><span data-stu-id="4e895-124">To view the static private IP address information for the VM created with the script above, run the following PowerShell command and observe the values for *PrivateIpAddress* and *PrivateIpAllocationMethod*:</span></span>

```powershell
Get-AzureRmNetworkInterface -Name TestNIC -ResourceGroupName TestRG
```

<span data-ttu-id="4e895-125">Expected output:</span><span class="sxs-lookup"><span data-stu-id="4e895-125">Expected output:</span></span>

    Name                 : TestNIC
    ResourceGroupName    : TestRG
    Location             : centralus
    Id                   : /subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC
    Etag                 : W/"[Id]"
    ProvisioningState    : Succeeded
    Tags                 : 
    VirtualMachine       : {
                             "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/DNS01"
                           }
    IpConfigurations     : [
                             {
                               "Name": "ipconfig1",
                               "Etag": "W/\"[Id]\"",
                               "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC/ipConfigurations/ipconfig1",
                               "PrivateIpAddress": "192.168.1.101",
                               "PrivateIpAllocationMethod": "Static",
                               "Subnet": {
                                 "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd"
                               },
                               "PublicIpAddress": {
                                 "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/TestPIP"
                               },
                               "LoadBalancerBackendAddressPools": [],
                               "LoadBalancerInboundNatRules": [],
                               "ProvisioningState": "Succeeded"
                             }
                           ]
    DnsSettings          : {
                             "DnsServers": [],
                             "AppliedDnsServers": [],
                             "InternalDnsNameLabel": null,
                             "InternalFqdn": null
                           }
    EnableIPForwarding   : False
    NetworkSecurityGroup : null
    Primary              : True

## <a name="remove-a-static-private-ip-address-from-a-network-interface"></a><span data-ttu-id="4e895-126">Remove a static private IP address from a network interface</span><span class="sxs-lookup"><span data-stu-id="4e895-126">Remove a static private IP address from a network interface</span></span>
<span data-ttu-id="4e895-127">To remove the static private IP address added to the VM in the script above, run the following PowerShell commands:</span><span class="sxs-lookup"><span data-stu-id="4e895-127">To remove the static private IP address added to the VM in the script above, run the following PowerShell commands:</span></span>

```powershell
$nic=Get-AzureRmNetworkInterface -Name TestNIC -ResourceGroupName TestRG
$nic.IpConfigurations[0].PrivateIpAllocationMethod = "Dynamic"
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

<span data-ttu-id="4e895-128">Expected output:</span><span class="sxs-lookup"><span data-stu-id="4e895-128">Expected output:</span></span>

    Name                 : TestNIC
    ResourceGroupName    : TestRG
    Location             : centralus
    Id                   : /subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC
    Etag                 : W/"[Id]"
    ProvisioningState    : Succeeded
    Tags                 : 
    VirtualMachine       : {
                             "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/WindowsVM"
                           }
    IpConfigurations     : [
                             {
                               "Name": "ipconfig1",
                               "Etag": "W/\"[Id]\"",
                               "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC/ipConfigurations/ipconfig1",
                               "PrivateIpAddress": "192.168.1.101",
                               "PrivateIpAllocationMethod": "Dynamic",
                               "Subnet": {
                                 "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd"
                               },
                               "PublicIpAddress": {
                                 "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/TestPIP"
                               },
                               "LoadBalancerBackendAddressPools": [],
                               "LoadBalancerInboundNatRules": [],
                               "ProvisioningState": "Succeeded"
                             }
                           ]
    DnsSettings          : {
                             "DnsServers": [],
                             "AppliedDnsServers": [],
                             "InternalDnsNameLabel": null,
                             "InternalFqdn": null
                           }
    EnableIPForwarding   : False
    NetworkSecurityGroup : null
    Primary              : True

## <a name="add-a-static-private-ip-address-to-a-network-interface"></a><span data-ttu-id="4e895-129">Add a static private IP address to a network interface</span><span class="sxs-lookup"><span data-stu-id="4e895-129">Add a static private IP address to a network interface</span></span>
<span data-ttu-id="4e895-130">To add a static private IP address to the VM created using the script above, run the following commands:</span><span class="sxs-lookup"><span data-stu-id="4e895-130">To add a static private IP address to the VM created using the script above, run the following commands:</span></span>

```powershell
$nic=Get-AzureRmNetworkInterface -Name TestNIC -ResourceGroupName TestRG
$nic.IpConfigurations[0].PrivateIpAllocationMethod = "Static"
$nic.IpConfigurations[0].PrivateIpAddress = "192.168.1.101"
Set-AzureRmNetworkInterface -NetworkInterface $nic
```
## <a name="change-the-allocation-method-for-a-private-ip-address-assigned-to-a-network-interface"></a><span data-ttu-id="4e895-131">Change the allocation method for a private IP address assigned to a network interface</span><span class="sxs-lookup"><span data-stu-id="4e895-131">Change the allocation method for a private IP address assigned to a network interface</span></span>

<span data-ttu-id="4e895-132">A private IP address is assigned to a NIC with the static or dynamic allocation method.</span><span class="sxs-lookup"><span data-stu-id="4e895-132">A private IP address is assigned to a NIC with the static or dynamic allocation method.</span></span> <span data-ttu-id="4e895-133">Dynamic IP addresses can change after starting a VM that was previously in the stopped (deallocated) state.</span><span class="sxs-lookup"><span data-stu-id="4e895-133">Dynamic IP addresses can change after starting a VM that was previously in the stopped (deallocated) state.</span></span> <span data-ttu-id="4e895-134">This can potentially cause issues if the VM is hosting a service that requires the same IP address, even after restarts from a stopped (deallocated) state.</span><span class="sxs-lookup"><span data-stu-id="4e895-134">This can potentially cause issues if the VM is hosting a service that requires the same IP address, even after restarts from a stopped (deallocated) state.</span></span> <span data-ttu-id="4e895-135">Static IP addresses are retained until the VM is deleted.</span><span class="sxs-lookup"><span data-stu-id="4e895-135">Static IP addresses are retained until the VM is deleted.</span></span> <span data-ttu-id="4e895-136">To change the allocation method of an IP address, run the following script, which changes the allocation method from dynamic to static.</span><span class="sxs-lookup"><span data-stu-id="4e895-136">To change the allocation method of an IP address, run the following script, which changes the allocation method from dynamic to static.</span></span> <span data-ttu-id="4e895-137">If the allocation method for the current private IP address is static, change *Static* to *Dynamic* before executing the script.</span><span class="sxs-lookup"><span data-stu-id="4e895-137">If the allocation method for the current private IP address is static, change *Static* to *Dynamic* before executing the script.</span></span>

```powershell
$RG = "TestRG"
$NIC_name = "testnic1"

$nic = Get-AzureRmNetworkInterface -ResourceGroupName $RG -Name $NIC_name
$nic.IpConfigurations[0].PrivateIpAllocationMethod = 'Static'
Set-AzureRmNetworkInterface -NetworkInterface $nic 
$IP = $nic.IpConfigurations[0].PrivateIpAddress

Write-Host "The allocation method is now set to"$nic.IpConfigurations[0].PrivateIpAllocationMethod"for the IP address" $IP"." -NoNewline
```

<span data-ttu-id="4e895-138">If you don't know the name of the NIC, you can view a list of NICs within a resource group by entering the following command:</span><span class="sxs-lookup"><span data-stu-id="4e895-138">If you don't know the name of the NIC, you can view a list of NICs within a resource group by entering the following command:</span></span>

```powershell
Get-AzureRmNetworkInterface -ResourceGroupName $RG | Where-Object {$_.ProvisioningState -eq 'Succeeded'} 
```

## <a name="next-steps"></a><span data-ttu-id="4e895-139">Next steps</span><span class="sxs-lookup"><span data-stu-id="4e895-139">Next steps</span></span>
* <span data-ttu-id="4e895-140">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span><span class="sxs-lookup"><span data-stu-id="4e895-140">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="4e895-141">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span><span class="sxs-lookup"><span data-stu-id="4e895-141">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="4e895-142">Consult the [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span><span class="sxs-lookup"><span data-stu-id="4e895-142">Consult the [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

