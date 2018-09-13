---
title: Simulated hybrid cloud test environment | Microsoft Docs
description: Create a simulated hybrid cloud environment for IT pro or development testing, using two Azure virtual networks and a VNet-to-VNet connection.
services: virtual-machines-windows
documentationcenter: ''
author: JoeDavies-MSFT
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: ca5bf294-8172-44a9-8fed-d6f38d345364
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/30/2016
ms.author: josephd
ms.openlocfilehash: 521bea864d1b6ee301b9edd0526e979203f38571
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551468"
---
# <a name="set-up-a-simulated-hybrid-cloud-environment-for-testing"></a><span data-ttu-id="abb63-103">Set up a simulated hybrid cloud environment for testing</span><span class="sxs-lookup"><span data-stu-id="abb63-103">Set up a simulated hybrid cloud environment for testing</span></span>
<span data-ttu-id="abb63-104">This article steps you through creating a simulated hybrid cloud environment with Microsoft Azure using two Azure virtual networks.</span><span class="sxs-lookup"><span data-stu-id="abb63-104">This article steps you through creating a simulated hybrid cloud environment with Microsoft Azure using two Azure virtual networks.</span></span> <span data-ttu-id="abb63-105">Here is the resulting configuration.</span><span class="sxs-lookup"><span data-stu-id="abb63-105">Here is the resulting configuration.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph4.png)

<span data-ttu-id="abb63-106">This simulates a hybrid cloud production environment and consists of:</span><span class="sxs-lookup"><span data-stu-id="abb63-106">This simulates a hybrid cloud production environment and consists of:</span></span>

* <span data-ttu-id="abb63-107">A simulated and simplified on-premises network hosted in an Azure virtual network (the TestLab virtual network).</span><span class="sxs-lookup"><span data-stu-id="abb63-107">A simulated and simplified on-premises network hosted in an Azure virtual network (the TestLab virtual network).</span></span>
* <span data-ttu-id="abb63-108">A simulated cross-premises virtual network hosted in Azure (TestVNET).</span><span class="sxs-lookup"><span data-stu-id="abb63-108">A simulated cross-premises virtual network hosted in Azure (TestVNET).</span></span>
* <span data-ttu-id="abb63-109">A VNet-to-VNet connection between the two virtual networks.</span><span class="sxs-lookup"><span data-stu-id="abb63-109">A VNet-to-VNet connection between the two virtual networks.</span></span>
* <span data-ttu-id="abb63-110">A secondary domain controller in the TestVNET virtual network.</span><span class="sxs-lookup"><span data-stu-id="abb63-110">A secondary domain controller in the TestVNET virtual network.</span></span>

<span data-ttu-id="abb63-111">This provides a basis and common starting point from which you can:</span><span class="sxs-lookup"><span data-stu-id="abb63-111">This provides a basis and common starting point from which you can:</span></span>

* <span data-ttu-id="abb63-112">Develop and test applications in a simulated hybrid cloud environment.</span><span class="sxs-lookup"><span data-stu-id="abb63-112">Develop and test applications in a simulated hybrid cloud environment.</span></span>
* <span data-ttu-id="abb63-113">Create test configurations of computers, some within the TestLab virtual network and some within the TestVNET virtual network, to simulate hybrid cloud-based IT workloads.</span><span class="sxs-lookup"><span data-stu-id="abb63-113">Create test configurations of computers, some within the TestLab virtual network and some within the TestVNET virtual network, to simulate hybrid cloud-based IT workloads.</span></span>

<span data-ttu-id="abb63-114">There are four major phases to setting up this hybrid cloud test environment:</span><span class="sxs-lookup"><span data-stu-id="abb63-114">There are four major phases to setting up this hybrid cloud test environment:</span></span>

1. <span data-ttu-id="abb63-115">Configure the TestLab virtual network.</span><span class="sxs-lookup"><span data-stu-id="abb63-115">Configure the TestLab virtual network.</span></span>
2. <span data-ttu-id="abb63-116">Create the cross-premises virtual network.</span><span class="sxs-lookup"><span data-stu-id="abb63-116">Create the cross-premises virtual network.</span></span>
3. <span data-ttu-id="abb63-117">Create the VNet-to-VNet VPN connection.</span><span class="sxs-lookup"><span data-stu-id="abb63-117">Create the VNet-to-VNet VPN connection.</span></span>
4. <span data-ttu-id="abb63-118">Configure DC2.</span><span class="sxs-lookup"><span data-stu-id="abb63-118">Configure DC2.</span></span> 

<span data-ttu-id="abb63-119">This configuration requires an Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="abb63-119">This configuration requires an Azure subscription.</span></span> <span data-ttu-id="abb63-120">If you have an MSDN or Visual Studio subscription, see [Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span><span class="sxs-lookup"><span data-stu-id="abb63-120">If you have an MSDN or Visual Studio subscription, see [Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span>

> [!NOTE]
> <span data-ttu-id="abb63-121">Virtual machines and virtual network gateways in Azure incur an ongoing monetary cost when they are running.</span><span class="sxs-lookup"><span data-stu-id="abb63-121">Virtual machines and virtual network gateways in Azure incur an ongoing monetary cost when they are running.</span></span> <span data-ttu-id="abb63-122">This cost is billed against your MSDN or paid subscription.</span><span class="sxs-lookup"><span data-stu-id="abb63-122">This cost is billed against your MSDN or paid subscription.</span></span> <span data-ttu-id="abb63-123">An Azure VPN gateway is implemented as a set of two Azure virtual machines.</span><span class="sxs-lookup"><span data-stu-id="abb63-123">An Azure VPN gateway is implemented as a set of two Azure virtual machines.</span></span> <span data-ttu-id="abb63-124">To minimize the costs, create the test environment and perform your needed testing and demonstration as quickly as possible.</span><span class="sxs-lookup"><span data-stu-id="abb63-124">To minimize the costs, create the test environment and perform your needed testing and demonstration as quickly as possible.</span></span>
> 
> 

## <a name="phase-1-configure-the-testlab-virtual-network"></a><span data-ttu-id="abb63-125">Phase 1: Configure the TestLab virtual network</span><span class="sxs-lookup"><span data-stu-id="abb63-125">Phase 1: Configure the TestLab virtual network</span></span>
<span data-ttu-id="abb63-126">Use the instructions in the [Base Configuration test environment](https://technet.microsoft.com/library/mt771177.aspx) topic to configure the DC1, APP1, and CLIENT1 computers in the Azure virtual network named TestLab.</span><span class="sxs-lookup"><span data-stu-id="abb63-126">Use the instructions in the [Base Configuration test environment](https://technet.microsoft.com/library/mt771177.aspx) topic to configure the DC1, APP1, and CLIENT1 computers in the Azure virtual network named TestLab.</span></span> 

<span data-ttu-id="abb63-127">Next, start an Azure PowerShell prompt.</span><span class="sxs-lookup"><span data-stu-id="abb63-127">Next, start an Azure PowerShell prompt.</span></span>

> [!NOTE]
> <span data-ttu-id="abb63-128">The following command sets use Azure PowerShell 1.0 and later.</span><span class="sxs-lookup"><span data-stu-id="abb63-128">The following command sets use Azure PowerShell 1.0 and later.</span></span>
> 
> 

<span data-ttu-id="abb63-129">Sign in to your account.</span><span class="sxs-lookup"><span data-stu-id="abb63-129">Sign in to your account.</span></span>

    Login-AzureRMAccount

<span data-ttu-id="abb63-130">Get your subscription name using the following command.</span><span class="sxs-lookup"><span data-stu-id="abb63-130">Get your subscription name using the following command.</span></span>

    Get-AzureRMSubscription | Sort SubscriptionName | Select SubscriptionName

<span data-ttu-id="abb63-131">Set your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="abb63-131">Set your Azure subscription.</span></span> <span data-ttu-id="abb63-132">Use the same subscription that you used to build your base configuration in Phase 1.</span><span class="sxs-lookup"><span data-stu-id="abb63-132">Use the same subscription that you used to build your base configuration in Phase 1.</span></span> <span data-ttu-id="abb63-133">Replace everything within the quotes, including the < and > characters, with the correct name.</span><span class="sxs-lookup"><span data-stu-id="abb63-133">Replace everything within the quotes, including the < and > characters, with the correct name.</span></span>

    $subscr="<subscription name>"
    Get-AzureRmSubscription –SubscriptionName $subscr | Select-AzureRmSubscription

<span data-ttu-id="abb63-134">Next, add a gateway subnet to the TestLab virtual network of your base configuration, which will be used to host the Azure gateway.</span><span class="sxs-lookup"><span data-stu-id="abb63-134">Next, add a gateway subnet to the TestLab virtual network of your base configuration, which will be used to host the Azure gateway.</span></span>

    $rgName="<name of your resource group that you used for your TestLab virtual network>"
    $locName="<Azure location name where you placed the TestLab virtual network, such as West US>"
    $vnet=Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name TestLab
    Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix 10.255.255.248/29 -VirtualNetwork $vnet
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet

<span data-ttu-id="abb63-135">Next, request a public IP address to assign to the gateway for the TestLab virtual network.</span><span class="sxs-lookup"><span data-stu-id="abb63-135">Next, request a public IP address to assign to the gateway for the TestLab virtual network.</span></span>

    $gwpip=New-AzureRmPublicIpAddress -Name TestLab_pip -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic

<span data-ttu-id="abb63-136">Next, create your gateway.</span><span class="sxs-lookup"><span data-stu-id="abb63-136">Next, create your gateway.</span></span>

    $vnet=Get-AzureRmVirtualNetwork -Name TestLab -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
    $gwipconfig=New-AzureRmVirtualNetworkGatewayIpConfig -Name TestLab_GWConfig -SubnetId $subnet.Id -PublicIpAddressId $gwpip.Id 
    New-AzureRmVirtualNetworkGateway -Name TestLab_GW -ResourceGroupName $rgName -Location $locName -IpConfigurations $gwipconfig -GatewayType Vpn -VpnType RouteBased

<span data-ttu-id="abb63-137">Keep in mind that new gateways can take 20 minutes or more to create.</span><span class="sxs-lookup"><span data-stu-id="abb63-137">Keep in mind that new gateways can take 20 minutes or more to create.</span></span>

<span data-ttu-id="abb63-138">From the Azure portal on your local computer, connect to DC1 with the CORP\User1 credentials.</span><span class="sxs-lookup"><span data-stu-id="abb63-138">From the Azure portal on your local computer, connect to DC1 with the CORP\User1 credentials.</span></span> <span data-ttu-id="abb63-139">To configure the CORP domain so that computers and users use their local domain controller for authentication, run these commands from an administrator-level Windows PowerShell command prompt on DC1.</span><span class="sxs-lookup"><span data-stu-id="abb63-139">To configure the CORP domain so that computers and users use their local domain controller for authentication, run these commands from an administrator-level Windows PowerShell command prompt on DC1.</span></span>

    New-ADReplicationSite -Name "TestLab" 
    New-ADReplicationSite -Name "TestVNET"
    New-ADReplicationSubnet -Name "10.0.0.0/8" -Site "TestLab"
    New-ADReplicationSubnet -Name "192.168.0.0/16" -Site "TestVNET"

<span data-ttu-id="abb63-140">This is your current configuration.</span><span class="sxs-lookup"><span data-stu-id="abb63-140">This is your current configuration.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph1.png)

## <a name="phase-2-create-the-testvnet-virtual-network"></a><span data-ttu-id="abb63-141">Phase 2: Create the TestVNET virtual network</span><span class="sxs-lookup"><span data-stu-id="abb63-141">Phase 2: Create the TestVNET virtual network</span></span>
<span data-ttu-id="abb63-142">First, create the TestVNET virtual network and protect it with a network security group.</span><span class="sxs-lookup"><span data-stu-id="abb63-142">First, create the TestVNET virtual network and protect it with a network security group.</span></span>

    $rgName="<name of the resource group that you used for your TestLab virtual network>"
    $locName="<Azure location name where you placed the TestLab virtual network, such as West US>"
    $locShortName="<Azure location name from $locName in all lowercase letters with spaces removed. Example:  westus>"
    $testSubnet=New-AzureRMVirtualNetworkSubnetConfig -Name "TestSubnet" -AddressPrefix 192.168.0.0/24
    $gatewaySubnet=New-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix 192.168.255.248/29
    New-AzureRMVirtualNetwork -Name "TestVNET" -ResourceGroupName $rgName -Location $locName -AddressPrefix 192.168.0.0/16 -Subnet $testSubnet,$gatewaySubnet –DNSServer 10.0.0.4
    $rule1=New-AzureRMNetworkSecurityRuleConfig -Name "RDPTraffic" -Description "Allow RDP to all VMs on the subnet" -Access Allow -Protocol Tcp -Direction Inbound -Priority 100 -SourceAddressPrefix Internet -SourcePortRange * -DestinationAddressPrefix * -DestinationPortRange 3389
    New-AzureRMNetworkSecurityGroup -Name "TestSubnet" -ResourceGroupName $rgName -Location $locShortName -SecurityRules $rule1
    $vnet=Get-AzureRMVirtualNetwork -ResourceGroupName $rgName -Name TestVNET
    $nsg=Get-AzureRMNetworkSecurityGroup -Name "TestSubnet" -ResourceGroupName $rgName
    Set-AzureRMVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name "TestSubnet" -AddressPrefix 192.168.0.0/24 -NetworkSecurityGroup $nsg

<span data-ttu-id="abb63-143">Next, request a public IP address to be allocated to the gateway for the TestVNET virtual network and create your gateway.</span><span class="sxs-lookup"><span data-stu-id="abb63-143">Next, request a public IP address to be allocated to the gateway for the TestVNET virtual network and create your gateway.</span></span>

    $gwpip=New-AzureRmPublicIpAddress -Name TestVNET_pip -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $vnet=Get-AzureRmVirtualNetwork -Name TestVNET -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
    $gwipconfig=New-AzureRmVirtualNetworkGatewayIpConfig -Name "TestVNET_GWConfig" -SubnetId $subnet.Id -PublicIpAddressId $gwpip.Id
    New-AzureRmVirtualNetworkGateway -Name "TestVNET_GW" -ResourceGroupName $rgName -Location $locName -IpConfigurations $gwipconfig -GatewayType Vpn -VpnType RouteBased

<span data-ttu-id="abb63-144">This is your current configuration.</span><span class="sxs-lookup"><span data-stu-id="abb63-144">This is your current configuration.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph2.png)

## <a name="phase-3-create-the-vnet-to-vnet-connection"></a><span data-ttu-id="abb63-145">Phase 3: Create the VNet-to-VNet connection</span><span class="sxs-lookup"><span data-stu-id="abb63-145">Phase 3: Create the VNet-to-VNet connection</span></span>
<span data-ttu-id="abb63-146">First, obtain a random, cryptographically strong, 32-character pre-shared key from your network or security administrator.</span><span class="sxs-lookup"><span data-stu-id="abb63-146">First, obtain a random, cryptographically strong, 32-character pre-shared key from your network or security administrator.</span></span> <span data-ttu-id="abb63-147">Alternately, use the information at [Create a random string for an IPsec preshared key](http://social.technet.microsoft.com/wiki/contents/articles/32330.create-a-random-string-for-an-ipsec-preshared-key.aspx) to obtain a pre-shared key.</span><span class="sxs-lookup"><span data-stu-id="abb63-147">Alternately, use the information at [Create a random string for an IPsec preshared key](http://social.technet.microsoft.com/wiki/contents/articles/32330.create-a-random-string-for-an-ipsec-preshared-key.aspx) to obtain a pre-shared key.</span></span>

<span data-ttu-id="abb63-148">Next, use these commands to create the VNet-to-VNet VPN connection, which can take some time to complete.</span><span class="sxs-lookup"><span data-stu-id="abb63-148">Next, use these commands to create the VNet-to-VNet VPN connection, which can take some time to complete.</span></span>

    $sharedKey="<pre-shared key value>"
    $gwTestLab=Get-AzureRmVirtualNetworkGateway -Name TestLab_GW -ResourceGroupName $rgName
    $gwTestVNET=Get-AzureRmVirtualNetworkGateway -Name TestVNET_GW -ResourceGroupName $rgName
    New-AzureRmVirtualNetworkGatewayConnection -Name TestLab_to_TestVNET -ResourceGroupName $rgName -VirtualNetworkGateway1 $gwTestLab -VirtualNetworkGateway2 $gwTestVNET -Location $locName -ConnectionType Vnet2Vnet -SharedKey $sharedKey
    New-AzureRmVirtualNetworkGatewayConnection -Name TestVNET_to_TestLab -ResourceGroupName $rgName -VirtualNetworkGateway1 $gwTestVNET -VirtualNetworkGateway2 $gwTestLab -Location $locName -ConnectionType Vnet2Vnet -SharedKey $sharedKey

<span data-ttu-id="abb63-149">After a few minutes, the connection should be established.</span><span class="sxs-lookup"><span data-stu-id="abb63-149">After a few minutes, the connection should be established.</span></span>

<span data-ttu-id="abb63-150">This is your current configuration.</span><span class="sxs-lookup"><span data-stu-id="abb63-150">This is your current configuration.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph3.png)

## <a name="phase-4-configure-dc2"></a><span data-ttu-id="abb63-151">Phase 4: Configure DC2</span><span class="sxs-lookup"><span data-stu-id="abb63-151">Phase 4: Configure DC2</span></span>
<span data-ttu-id="abb63-152">First, create a virtual machine for DC2.</span><span class="sxs-lookup"><span data-stu-id="abb63-152">First, create a virtual machine for DC2.</span></span> <span data-ttu-id="abb63-153">Run these commands at the Azure PowerShell command prompt on your local computer.</span><span class="sxs-lookup"><span data-stu-id="abb63-153">Run these commands at the Azure PowerShell command prompt on your local computer.</span></span>

    $rgName="<your resource group name>"
    $locName="<your Azure location, such as West US>"
    $saName="<the storage account name for the base configuration>"
    $vnet=Get-AzureRMVirtualNetwork -Name TestVNET -ResourceGroupName $rgName
    $pip=New-AzureRMPublicIpAddress -Name DC2-NIC -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $nic=New-AzureRMNetworkInterface -Name DC2-NIC -ResourceGroupName $rgName -Location $locName -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -PrivateIpAddress 192.168.0.4
    $vm=New-AzureRMVMConfig -VMName DC2 -VMSize Standard_A1
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $vhdURI=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/DC2-TestVNET-ADDSDisk.vhd"
    Add-AzureRMVMDataDisk -VM $vm -Name ADDS-Data -DiskSizeInGB 20 -VhdUri $vhdURI  -CreateOption empty
    $cred=Get-Credential -Message "Type the name and password of the local administrator account for DC2."
    $vm=Set-AzureRMVMOperatingSystem -VM $vm -Windows -ComputerName DC2 -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm=Set-AzureRMVMSourceImage -VM $vm -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm=Add-AzureRMVMNetworkInterface -VM $vm -Id $nic.Id
    $osDiskUri=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/DC2-TestLab-OSDisk.vhd"
    $vm=Set-AzureRMVMOSDisk -VM $vm -Name DC2-TestVNET-OSDisk -VhdUri $osDiskUri -CreateOption fromImage
    New-AzureRMVM -ResourceGroupName $rgName -Location $locName -VM $vm

<span data-ttu-id="abb63-154">Next, connect to the new DC2 virtual machine from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="abb63-154">Next, connect to the new DC2 virtual machine from the Azure portal.</span></span>

<span data-ttu-id="abb63-155">Next, configure a Windows Firewall rule to allow traffic for basic connectivity testing.</span><span class="sxs-lookup"><span data-stu-id="abb63-155">Next, configure a Windows Firewall rule to allow traffic for basic connectivity testing.</span></span> <span data-ttu-id="abb63-156">From an administrator-level Windows PowerShell command prompt on DC2, run these commands.</span><span class="sxs-lookup"><span data-stu-id="abb63-156">From an administrator-level Windows PowerShell command prompt on DC2, run these commands.</span></span>

    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc1.corp.contoso.com

<span data-ttu-id="abb63-157">The ping command should result in four successful replies from IP address 10.0.0.4.</span><span class="sxs-lookup"><span data-stu-id="abb63-157">The ping command should result in four successful replies from IP address 10.0.0.4.</span></span> <span data-ttu-id="abb63-158">This is a test of traffic across the VNet-to-VNet connection.</span><span class="sxs-lookup"><span data-stu-id="abb63-158">This is a test of traffic across the VNet-to-VNet connection.</span></span>

<span data-ttu-id="abb63-159">Next, add the extra data disk on DC2 as a new volume with the drive letter F:.</span><span class="sxs-lookup"><span data-stu-id="abb63-159">Next, add the extra data disk on DC2 as a new volume with the drive letter F:.</span></span>

1. <span data-ttu-id="abb63-160">In the left pane of Server Manager, click **File and Storage Services**, and then click **Disks**.</span><span class="sxs-lookup"><span data-stu-id="abb63-160">In the left pane of Server Manager, click **File and Storage Services**, and then click **Disks**.</span></span>
2. <span data-ttu-id="abb63-161">In the contents pane, in the **Disks** group, click **disk 2** (with the **Partition** set to **Unknown**).</span><span class="sxs-lookup"><span data-stu-id="abb63-161">In the contents pane, in the **Disks** group, click **disk 2** (with the **Partition** set to **Unknown**).</span></span>
3. <span data-ttu-id="abb63-162">Click **Tasks**, and then click **New Volume**.</span><span class="sxs-lookup"><span data-stu-id="abb63-162">Click **Tasks**, and then click **New Volume**.</span></span>
4. <span data-ttu-id="abb63-163">On the Before you begin page of the New Volume Wizard, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="abb63-163">On the Before you begin page of the New Volume Wizard, click **Next**.</span></span>
5. <span data-ttu-id="abb63-164">On the Select the server and disk page, click **Disk 2**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="abb63-164">On the Select the server and disk page, click **Disk 2**, and then click **Next**.</span></span> <span data-ttu-id="abb63-165">When prompted, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="abb63-165">When prompted, click **OK**.</span></span>
6. <span data-ttu-id="abb63-166">On the Specify the size of the volume page, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="abb63-166">On the Specify the size of the volume page, click **Next**.</span></span>
7. <span data-ttu-id="abb63-167">On the Assign to a drive letter or folder page, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="abb63-167">On the Assign to a drive letter or folder page, click **Next**.</span></span>
8. <span data-ttu-id="abb63-168">On the Select file system settings page, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="abb63-168">On the Select file system settings page, click **Next**.</span></span>
9. <span data-ttu-id="abb63-169">On the Confirm selections page, click **Create**.</span><span class="sxs-lookup"><span data-stu-id="abb63-169">On the Confirm selections page, click **Create**.</span></span>
10. <span data-ttu-id="abb63-170">When complete, click **Close**.</span><span class="sxs-lookup"><span data-stu-id="abb63-170">When complete, click **Close**.</span></span>

<span data-ttu-id="abb63-171">Next, configure DC2 as a replica domain controller for the corp.contoso.com domain.</span><span class="sxs-lookup"><span data-stu-id="abb63-171">Next, configure DC2 as a replica domain controller for the corp.contoso.com domain.</span></span> <span data-ttu-id="abb63-172">Run these commands from the Windows PowerShell command prompt on DC2.</span><span class="sxs-lookup"><span data-stu-id="abb63-172">Run these commands from the Windows PowerShell command prompt on DC2.</span></span>

    Install-WindowsFeature AD-Domain-Services -IncludeManagementTools
    Install-ADDSDomainController -Credential (Get-Credential CORP\User1) -DomainName "corp.contoso.com" -InstallDns:$true -DatabasePath "F:\NTDS" -LogPath "F:\Logs" -SysvolPath "F:\SYSVOL"

<span data-ttu-id="abb63-173">Note that you are prompted to supply both the CORP\User1 password and a Directory Services Restore Mode (DSRM) password, and to restart DC2.</span><span class="sxs-lookup"><span data-stu-id="abb63-173">Note that you are prompted to supply both the CORP\User1 password and a Directory Services Restore Mode (DSRM) password, and to restart DC2.</span></span>

<span data-ttu-id="abb63-174">Now that the TestVNET virtual network has its own DNS server (DC2), you must configure the TestVNET virtual network to use this DNS server.</span><span class="sxs-lookup"><span data-stu-id="abb63-174">Now that the TestVNET virtual network has its own DNS server (DC2), you must configure the TestVNET virtual network to use this DNS server.</span></span>

1. <span data-ttu-id="abb63-175">In the left pane of the Azure portal, click the virtual networks icon, and then click **TestVNET**.</span><span class="sxs-lookup"><span data-stu-id="abb63-175">In the left pane of the Azure portal, click the virtual networks icon, and then click **TestVNET**.</span></span>
2. <span data-ttu-id="abb63-176">On the **Settings** tab, click **DNS servers**.</span><span class="sxs-lookup"><span data-stu-id="abb63-176">On the **Settings** tab, click **DNS servers**.</span></span>
3. <span data-ttu-id="abb63-177">In **Primary DNS server**, type **192.168.0.4** to replace 10.0.0.4.</span><span class="sxs-lookup"><span data-stu-id="abb63-177">In **Primary DNS server**, type **192.168.0.4** to replace 10.0.0.4.</span></span>
4. <span data-ttu-id="abb63-178">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="abb63-178">Click **Save**.</span></span>

<span data-ttu-id="abb63-179">This is your current configuration.</span><span class="sxs-lookup"><span data-stu-id="abb63-179">This is your current configuration.</span></span> 

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph4.png)

<span data-ttu-id="abb63-180">Your simulated hybrid cloud environment is now ready for testing.</span><span class="sxs-lookup"><span data-stu-id="abb63-180">Your simulated hybrid cloud environment is now ready for testing.</span></span>

## <a name="next-step"></a><span data-ttu-id="abb63-181">Next step</span><span class="sxs-lookup"><span data-stu-id="abb63-181">Next step</span></span>
* <span data-ttu-id="abb63-182">Set up a [web-based, line of business application](ps-hybrid-cloud-test-env-lob.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) in this environment.</span><span class="sxs-lookup"><span data-stu-id="abb63-182">Set up a [web-based, line of business application](ps-hybrid-cloud-test-env-lob.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) in this environment.</span></span>






