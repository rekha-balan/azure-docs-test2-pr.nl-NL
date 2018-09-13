---
title: include file
description: include file
services: vpn-gateway
author: cherylmc
ms.service: vpn-gateway
ms.topic: include
ms.date: 03/21/2018
ms.author: cherylmc
ms.custom: include file
ms.openlocfilehash: 5acdd54bcf7e253bc21dc3f99207fc1b2bd1ff59
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "45306801"
---
<span data-ttu-id="5d363-103">You can connect to a VM that is deployed to your VNet by creating a Remote Desktop Connection to your VM.</span><span class="sxs-lookup"><span data-stu-id="5d363-103">You can connect to a VM that is deployed to your VNet by creating a Remote Desktop Connection to your VM.</span></span> <span data-ttu-id="5d363-104">The best way to initially verify that you can connect to your VM is to connect by using its private IP address, rather than computer name.</span><span class="sxs-lookup"><span data-stu-id="5d363-104">The best way to initially verify that you can connect to your VM is to connect by using its private IP address, rather than computer name.</span></span> <span data-ttu-id="5d363-105">That way, you are testing to see if you can connect, not whether name resolution is configured properly.</span><span class="sxs-lookup"><span data-stu-id="5d363-105">That way, you are testing to see if you can connect, not whether name resolution is configured properly.</span></span>

1. <span data-ttu-id="5d363-106">Locate the private IP address.</span><span class="sxs-lookup"><span data-stu-id="5d363-106">Locate the private IP address.</span></span> <span data-ttu-id="5d363-107">You can find the private IP address of a VM in multiple ways.</span><span class="sxs-lookup"><span data-stu-id="5d363-107">You can find the private IP address of a VM in multiple ways.</span></span> <span data-ttu-id="5d363-108">Below, we show the steps for the Azure portal and for PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5d363-108">Below, we show the steps for the Azure portal and for PowerShell.</span></span>

  - <span data-ttu-id="5d363-109">Azure portal - Locate your virtual machine in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="5d363-109">Azure portal - Locate your virtual machine in the Azure portal.</span></span> <span data-ttu-id="5d363-110">View the properties for the VM.</span><span class="sxs-lookup"><span data-stu-id="5d363-110">View the properties for the VM.</span></span> <span data-ttu-id="5d363-111">The private IP address is listed.</span><span class="sxs-lookup"><span data-stu-id="5d363-111">The private IP address is listed.</span></span>

  - <span data-ttu-id="5d363-112">PowerShell - Use the example to view a list of VMs and private IP addresses from your resource groups.</span><span class="sxs-lookup"><span data-stu-id="5d363-112">PowerShell - Use the example to view a list of VMs and private IP addresses from your resource groups.</span></span> <span data-ttu-id="5d363-113">You don't need to modify this example before using it.</span><span class="sxs-lookup"><span data-stu-id="5d363-113">You don't need to modify this example before using it.</span></span>

    ```azurepowershell-interactive
    $VMs = Get-AzureRmVM
    $Nics = Get-AzureRmNetworkInterface | Where VirtualMachine -ne $null

    foreach($Nic in $Nics)
    {
      $VM = $VMs | Where-Object -Property Id -eq $Nic.VirtualMachine.Id
      $Prv = $Nic.IpConfigurations | Select-Object -ExpandProperty PrivateIpAddress
      $Alloc = $Nic.IpConfigurations | Select-Object -ExpandProperty PrivateIpAllocationMethod
      Write-Output "$($VM.Name): $Prv,$Alloc"
    }
    ```

2. <span data-ttu-id="5d363-114">Verify that you are connected to your VNet using the VPN connection.</span><span class="sxs-lookup"><span data-stu-id="5d363-114">Verify that you are connected to your VNet using the VPN connection.</span></span>
3. <span data-ttu-id="5d363-115">Open **Remote Desktop Connection** by typing "RDP" or "Remote Desktop Connection" in the search box on the taskbar, then select Remote Desktop Connection.</span><span class="sxs-lookup"><span data-stu-id="5d363-115">Open **Remote Desktop Connection** by typing "RDP" or "Remote Desktop Connection" in the search box on the taskbar, then select Remote Desktop Connection.</span></span> <span data-ttu-id="5d363-116">You can also open Remote Desktop Connection using the 'mstsc' command in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5d363-116">You can also open Remote Desktop Connection using the 'mstsc' command in PowerShell.</span></span> 
4. <span data-ttu-id="5d363-117">In Remote Desktop Connection, enter the private IP address of the VM.</span><span class="sxs-lookup"><span data-stu-id="5d363-117">In Remote Desktop Connection, enter the private IP address of the VM.</span></span> <span data-ttu-id="5d363-118">You can click "Show Options" to adjust additional settings, then connect.</span><span class="sxs-lookup"><span data-stu-id="5d363-118">You can click "Show Options" to adjust additional settings, then connect.</span></span>

### <a name="to-troubleshoot-an-rdp-connection-to-a-vm"></a><span data-ttu-id="5d363-119">To troubleshoot an RDP connection to a VM</span><span class="sxs-lookup"><span data-stu-id="5d363-119">To troubleshoot an RDP connection to a VM</span></span>

<span data-ttu-id="5d363-120">If you are having trouble connecting to a virtual machine over your VPN connection, check the following:</span><span class="sxs-lookup"><span data-stu-id="5d363-120">If you are having trouble connecting to a virtual machine over your VPN connection, check the following:</span></span>

- <span data-ttu-id="5d363-121">Verify that your VPN connection is successful.</span><span class="sxs-lookup"><span data-stu-id="5d363-121">Verify that your VPN connection is successful.</span></span>
- <span data-ttu-id="5d363-122">Verify that you are connecting to the private IP address for the VM.</span><span class="sxs-lookup"><span data-stu-id="5d363-122">Verify that you are connecting to the private IP address for the VM.</span></span>
- <span data-ttu-id="5d363-123">If you can connect to the VM using the private IP address, but not the computer name, verify that you have configured DNS properly.</span><span class="sxs-lookup"><span data-stu-id="5d363-123">If you can connect to the VM using the private IP address, but not the computer name, verify that you have configured DNS properly.</span></span> <span data-ttu-id="5d363-124">For more information about how name resolution works for VMs, see [Name Resolution for VMs](../articles/virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span><span class="sxs-lookup"><span data-stu-id="5d363-124">For more information about how name resolution works for VMs, see [Name Resolution for VMs](../articles/virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>
- <span data-ttu-id="5d363-125">For more information about RDP connections, see [Troubleshoot Remote Desktop connections to a VM](../articles/virtual-machines/windows/troubleshoot-rdp-connection.md).</span><span class="sxs-lookup"><span data-stu-id="5d363-125">For more information about RDP connections, see [Troubleshoot Remote Desktop connections to a VM](../articles/virtual-machines/windows/troubleshoot-rdp-connection.md).</span></span>