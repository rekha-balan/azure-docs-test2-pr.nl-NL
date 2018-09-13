---
title: Tutorial - Create an Azure DNS private zone using Azure PowerShell
description: In this tutorial, you create and test a private DNS zone and record in Azure DNS. This is a step-by-step guide to create and manage your first private DNS zone and record using Azure PowerShell.
services: dns
author: vhorne
ms.service: dns
ms.topic: tutorial
ms.date: 7/24/2018
ms.author: victorh
ms.openlocfilehash: 872227e0521bd54e6bf7fdbe3626dfca34170863
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855594"
---
# <a name="tutorial-create-an-azure-dns-private-zone-using-azure-powershell"></a><span data-ttu-id="f70e7-104">Tutorial: Create an Azure DNS private zone using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="f70e7-104">Tutorial: Create an Azure DNS private zone using Azure PowerShell</span></span>

<span data-ttu-id="f70e7-105">This tutorial walks you through the steps to create your first private DNS zone and record using Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f70e7-105">This tutorial walks you through the steps to create your first private DNS zone and record using Azure PowerShell.</span></span>

[!INCLUDE [private-dns-public-preview-notice](../../includes/private-dns-public-preview-notice.md)]

<span data-ttu-id="f70e7-106">A DNS zone is used to host the DNS records for a particular domain.</span><span class="sxs-lookup"><span data-stu-id="f70e7-106">A DNS zone is used to host the DNS records for a particular domain.</span></span> <span data-ttu-id="f70e7-107">To start hosting your domain in Azure DNS, you need to create a DNS zone for that domain name.</span><span class="sxs-lookup"><span data-stu-id="f70e7-107">To start hosting your domain in Azure DNS, you need to create a DNS zone for that domain name.</span></span> <span data-ttu-id="f70e7-108">Each DNS record for your domain is then created inside this DNS zone.</span><span class="sxs-lookup"><span data-stu-id="f70e7-108">Each DNS record for your domain is then created inside this DNS zone.</span></span> <span data-ttu-id="f70e7-109">To publish a private DNS zone to your virtual network, you specify the list of virtual networks that are allowed to resolve records within the zone.</span><span class="sxs-lookup"><span data-stu-id="f70e7-109">To publish a private DNS zone to your virtual network, you specify the list of virtual networks that are allowed to resolve records within the zone.</span></span>  <span data-ttu-id="f70e7-110">These are called *resolution virtual networks*.</span><span class="sxs-lookup"><span data-stu-id="f70e7-110">These are called *resolution virtual networks*.</span></span> <span data-ttu-id="f70e7-111">You may also specify a virtual network for which Azure DNS maintains hostname records whenever a VM is created, changes IP, or is deleted.</span><span class="sxs-lookup"><span data-stu-id="f70e7-111">You may also specify a virtual network for which Azure DNS maintains hostname records whenever a VM is created, changes IP, or is deleted.</span></span>  <span data-ttu-id="f70e7-112">This is called a *registration virtual network*.</span><span class="sxs-lookup"><span data-stu-id="f70e7-112">This is called a *registration virtual network*.</span></span>

<span data-ttu-id="f70e7-113">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="f70e7-113">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f70e7-114">Create a DNS private zone</span><span class="sxs-lookup"><span data-stu-id="f70e7-114">Create a DNS private zone</span></span>
> * <span data-ttu-id="f70e7-115">Create test virtual machines</span><span class="sxs-lookup"><span data-stu-id="f70e7-115">Create test virtual machines</span></span>
> * <span data-ttu-id="f70e7-116">Create an additional DNS record</span><span class="sxs-lookup"><span data-stu-id="f70e7-116">Create an additional DNS record</span></span>
> * <span data-ttu-id="f70e7-117">Test the private zone</span><span class="sxs-lookup"><span data-stu-id="f70e7-117">Test the private zone</span></span>

<span data-ttu-id="f70e7-118">If you don’t have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="f70e7-118">If you don’t have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="f70e7-119">If you prefer, you can complete this tutorial using [Azure CLI](private-dns-getstarted-cli.md).</span><span class="sxs-lookup"><span data-stu-id="f70e7-119">If you prefer, you can complete this tutorial using [Azure CLI](private-dns-getstarted-cli.md).</span></span>

<!--- ## Get the Preview PowerShell modules
These instructions assume you have already installed and signed in to Azure PowerShell, including ensuring you have the required modules for the Private Zone feature. -->

<!---[!INCLUDE [dns-powershell-setup](../../includes/dns-powershell-setup-include.md)] -->

[!INCLUDE [cloud-shell-powershell.md](../../includes/cloud-shell-powershell.md)]

## <a name="create-the-resource-group"></a><span data-ttu-id="f70e7-120">Create the resource group</span><span class="sxs-lookup"><span data-stu-id="f70e7-120">Create the resource group</span></span>

<span data-ttu-id="f70e7-121">First, create a resource group to contain the DNS zone:</span><span class="sxs-lookup"><span data-stu-id="f70e7-121">First, create a resource group to contain the DNS zone:</span></span> 

```azurepowershell
New-AzureRMResourceGroup -name MyAzureResourceGroup -location "eastus"
```

## <a name="create-a-dns-private-zone"></a><span data-ttu-id="f70e7-122">Create a DNS private zone</span><span class="sxs-lookup"><span data-stu-id="f70e7-122">Create a DNS private zone</span></span>

<span data-ttu-id="f70e7-123">A DNS zone is created by using the `New-AzureRmDnsZone` cmdlet with a value of *Private* for the **ZoneType** parameter.</span><span class="sxs-lookup"><span data-stu-id="f70e7-123">A DNS zone is created by using the `New-AzureRmDnsZone` cmdlet with a value of *Private* for the **ZoneType** parameter.</span></span> <span data-ttu-id="f70e7-124">The following example creates a DNS zone called **contoso.local** in the resource group called **MyAzureResourceGroup** and makes the DNS zone available to the virtual network called **MyAzureVnet**.</span><span class="sxs-lookup"><span data-stu-id="f70e7-124">The following example creates a DNS zone called **contoso.local** in the resource group called **MyAzureResourceGroup** and makes the DNS zone available to the virtual network called **MyAzureVnet**.</span></span>

<span data-ttu-id="f70e7-125">If the **ZoneType** parameter is omitted, the zone is created as a public zone, so it is required to create a private zone.</span><span class="sxs-lookup"><span data-stu-id="f70e7-125">If the **ZoneType** parameter is omitted, the zone is created as a public zone, so it is required to create a private zone.</span></span> 

```azurepowershell
$backendSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name backendSubnet -AddressPrefix "10.2.0.0/24"
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName MyAzureResourceGroup `
  -Location eastus `
  -Name myAzureVNet `
  -AddressPrefix 10.2.0.0/16 `
  -Subnet $backendSubnet

New-AzureRmDnsZone -Name contoso.local -ResourceGroupName MyAzureResourceGroup `
   -ZoneType Private `
   -RegistrationVirtualNetworkId @($vnet.Id)
```

<span data-ttu-id="f70e7-126">If you wanted to create a zone just for name resolution (no automatic hostname creation), you could use the *ResolutionVirtualNetworkId* parameter instead of the *RegistrationVirtualNetworkId* parameter.</span><span class="sxs-lookup"><span data-stu-id="f70e7-126">If you wanted to create a zone just for name resolution (no automatic hostname creation), you could use the *ResolutionVirtualNetworkId* parameter instead of the *RegistrationVirtualNetworkId* parameter.</span></span>

> [!NOTE]
> <span data-ttu-id="f70e7-127">You won't be able to see the automatically created hostname records.</span><span class="sxs-lookup"><span data-stu-id="f70e7-127">You won't be able to see the automatically created hostname records.</span></span> <span data-ttu-id="f70e7-128">But later, you will test to ensure they exist.</span><span class="sxs-lookup"><span data-stu-id="f70e7-128">But later, you will test to ensure they exist.</span></span>

### <a name="list-dns-private-zones"></a><span data-ttu-id="f70e7-129">List DNS private zones</span><span class="sxs-lookup"><span data-stu-id="f70e7-129">List DNS private zones</span></span>

<span data-ttu-id="f70e7-130">By omitting the zone name from `Get-AzureRmDnsZone`, you can enumerate all zones in a resource group.</span><span class="sxs-lookup"><span data-stu-id="f70e7-130">By omitting the zone name from `Get-AzureRmDnsZone`, you can enumerate all zones in a resource group.</span></span> <span data-ttu-id="f70e7-131">This operation returns an array of zone objects.</span><span class="sxs-lookup"><span data-stu-id="f70e7-131">This operation returns an array of zone objects.</span></span>

```azurepowershell
Get-AzureRmDnsZone -ResourceGroupName MyAzureResourceGroup
```

<span data-ttu-id="f70e7-132">By omitting both the zone name and the resource group name from `Get-AzureRmDnsZone`, you can enumerate all zones in the Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="f70e7-132">By omitting both the zone name and the resource group name from `Get-AzureRmDnsZone`, you can enumerate all zones in the Azure subscription.</span></span>

```azurepowershell
Get-AzureRmDnsZone
```

## <a name="create-the-test-virtual-machines"></a><span data-ttu-id="f70e7-133">Create the test virtual machines</span><span class="sxs-lookup"><span data-stu-id="f70e7-133">Create the test virtual machines</span></span>

<span data-ttu-id="f70e7-134">Now, create two virtual machines so you can test your private DNS zone:</span><span class="sxs-lookup"><span data-stu-id="f70e7-134">Now, create two virtual machines so you can test your private DNS zone:</span></span>

```azurepowershell
New-AzureRmVm `
    -ResourceGroupName "myAzureResourceGroup" `
    -Name "myVM01" `
    -Location "East US" `
    -subnetname backendSubnet `
    -VirtualNetworkName "myAzureVnet" `
    -addressprefix 10.2.0.0/24 `
    -OpenPorts 3389

New-AzureRmVm `
    -ResourceGroupName "myAzureResourceGroup" `
    -Name "myVM02" `
    -Location "East US" `
    -subnetname backendSubnet `
    -VirtualNetworkName "myAzureVnet" `
    -addressprefix 10.2.0.0/24 `
    -OpenPorts 3389
```

<span data-ttu-id="f70e7-135">This will take a few minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="f70e7-135">This will take a few minutes to complete.</span></span>

## <a name="create-an-additional-dns-record"></a><span data-ttu-id="f70e7-136">Create an additional DNS record</span><span class="sxs-lookup"><span data-stu-id="f70e7-136">Create an additional DNS record</span></span>

<span data-ttu-id="f70e7-137">You create record sets by using the `New-AzureRmDnsRecordSet` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f70e7-137">You create record sets by using the `New-AzureRmDnsRecordSet` cmdlet.</span></span> <span data-ttu-id="f70e7-138">The following example creates a record with the relative name **db** in the DNS Zone **contoso.local**, in resource group **MyAzureResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="f70e7-138">The following example creates a record with the relative name **db** in the DNS Zone **contoso.local**, in resource group **MyAzureResourceGroup**.</span></span> <span data-ttu-id="f70e7-139">The fully-qualified name of the record set is **db.contoso.local**.</span><span class="sxs-lookup"><span data-stu-id="f70e7-139">The fully-qualified name of the record set is **db.contoso.local**.</span></span> <span data-ttu-id="f70e7-140">The record type is "A", with IP address "10.2.0.4", and the TTL is 3600 seconds.</span><span class="sxs-lookup"><span data-stu-id="f70e7-140">The record type is "A", with IP address "10.2.0.4", and the TTL is 3600 seconds.</span></span>

```azurepowershell
New-AzureRmDnsRecordSet -Name db -RecordType A -ZoneName contoso.local `
   -ResourceGroupName MyAzureResourceGroup -Ttl 3600 `
   -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "10.2.0.4")
```

### <a name="view-dns-records"></a><span data-ttu-id="f70e7-141">View DNS records</span><span class="sxs-lookup"><span data-stu-id="f70e7-141">View DNS records</span></span>

<span data-ttu-id="f70e7-142">To list the DNS records in your zone, run:</span><span class="sxs-lookup"><span data-stu-id="f70e7-142">To list the DNS records in your zone, run:</span></span>

```azurepowershell
Get-AzureRmDnsRecordSet -ZoneName contoso.local -ResourceGroupName MyAzureResourceGroup
```
<span data-ttu-id="f70e7-143">Remember, you won't see the automatically created A records for your two test virtual machines.</span><span class="sxs-lookup"><span data-stu-id="f70e7-143">Remember, you won't see the automatically created A records for your two test virtual machines.</span></span>

## <a name="test-the-private-zone"></a><span data-ttu-id="f70e7-144">Test the private zone</span><span class="sxs-lookup"><span data-stu-id="f70e7-144">Test the private zone</span></span>

<span data-ttu-id="f70e7-145">Now you can test the name resolution for your **contoso.local** private zone.</span><span class="sxs-lookup"><span data-stu-id="f70e7-145">Now you can test the name resolution for your **contoso.local** private zone.</span></span>

### <a name="configure-vms-to-allow-inbound-icmp"></a><span data-ttu-id="f70e7-146">Configure VMs to allow inbound ICMP</span><span class="sxs-lookup"><span data-stu-id="f70e7-146">Configure VMs to allow inbound ICMP</span></span>

<span data-ttu-id="f70e7-147">You can use the ping command to test name resolution.</span><span class="sxs-lookup"><span data-stu-id="f70e7-147">You can use the ping command to test name resolution.</span></span> <span data-ttu-id="f70e7-148">So, configure the firewall on both virtual machines to allow inbound ICMP packets.</span><span class="sxs-lookup"><span data-stu-id="f70e7-148">So, configure the firewall on both virtual machines to allow inbound ICMP packets.</span></span>

1. <span data-ttu-id="f70e7-149">Connect to myVM01, and open a Windows PowerShell window with administrator privileges.</span><span class="sxs-lookup"><span data-stu-id="f70e7-149">Connect to myVM01, and open a Windows PowerShell window with administrator privileges.</span></span>
2. <span data-ttu-id="f70e7-150">Run the following command:</span><span class="sxs-lookup"><span data-stu-id="f70e7-150">Run the following command:</span></span>

   ```powershell
   New-NetFirewallRule –DisplayName “Allow ICMPv4-In” –Protocol ICMPv4
   ```

<span data-ttu-id="f70e7-151">Repeat for myVM02.</span><span class="sxs-lookup"><span data-stu-id="f70e7-151">Repeat for myVM02.</span></span>

### <a name="ping-the-vms-by-name"></a><span data-ttu-id="f70e7-152">Ping the VMs by name</span><span class="sxs-lookup"><span data-stu-id="f70e7-152">Ping the VMs by name</span></span>

1. <span data-ttu-id="f70e7-153">From the myVM02 Windows PowerShell command prompt, ping myVM01 using the automatically registered host name:</span><span class="sxs-lookup"><span data-stu-id="f70e7-153">From the myVM02 Windows PowerShell command prompt, ping myVM01 using the automatically registered host name:</span></span>
   ```
   ping myVM01.contoso.local
   ```
   <span data-ttu-id="f70e7-154">You should see output that looks similar to this:</span><span class="sxs-lookup"><span data-stu-id="f70e7-154">You should see output that looks similar to this:</span></span>
   ```
   PS C:\> ping myvm01.contoso.local

   Pinging myvm01.contoso.local [10.2.0.4] with 32 bytes of data:
   Reply from 10.2.0.4: bytes=32 time<1ms TTL=128
   Reply from 10.2.0.4: bytes=32 time=1ms TTL=128
   Reply from 10.2.0.4: bytes=32 time<1ms TTL=128
   Reply from 10.2.0.4: bytes=32 time<1ms TTL=128

   Ping statistics for 10.2.0.4:
       Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
   Approximate round trip times in milli-seconds:
       Minimum = 0ms, Maximum = 1ms, Average = 0ms
   PS C:\>
   ```
2. <span data-ttu-id="f70e7-155">Now ping the **db** name you created previously:</span><span class="sxs-lookup"><span data-stu-id="f70e7-155">Now ping the **db** name you created previously:</span></span>
   ```
   ping db.contoso.local
   ```
   <span data-ttu-id="f70e7-156">You should see output that looks similar to this:</span><span class="sxs-lookup"><span data-stu-id="f70e7-156">You should see output that looks similar to this:</span></span>
   ```
   PS C:\> ping db.contoso.local

   Pinging db.contoso.local [10.2.0.4] with 32 bytes of data:
   Reply from 10.2.0.4: bytes=32 time<1ms TTL=128
   Reply from 10.2.0.4: bytes=32 time<1ms TTL=128
   Reply from 10.2.0.4: bytes=32 time<1ms TTL=128
   Reply from 10.2.0.4: bytes=32 time<1ms TTL=128

   Ping statistics for 10.2.0.4:
       Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
   Approximate round trip times in milli-seconds:
       Minimum = 0ms, Maximum = 0ms, Average = 0ms
   PS C:\>
   ```

## <a name="delete-all-resources"></a><span data-ttu-id="f70e7-157">Delete all resources</span><span class="sxs-lookup"><span data-stu-id="f70e7-157">Delete all resources</span></span>

<span data-ttu-id="f70e7-158">When no longer needed, delete the **MyAzureResourceGroup** resource group to delete the resources created in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="f70e7-158">When no longer needed, delete the **MyAzureResourceGroup** resource group to delete the resources created in this tutorial.</span></span>

```azurepowershell
Remove-AzureRMResourceGroup -Name MyAzureResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="f70e7-159">Next steps</span><span class="sxs-lookup"><span data-stu-id="f70e7-159">Next steps</span></span>

<span data-ttu-id="f70e7-160">In this tutorial, you deployed a private DNS zone, created a DNS record, and tested the zone.</span><span class="sxs-lookup"><span data-stu-id="f70e7-160">In this tutorial, you deployed a private DNS zone, created a DNS record, and tested the zone.</span></span>
<span data-ttu-id="f70e7-161">Next, you can learn more about private DNS zones.</span><span class="sxs-lookup"><span data-stu-id="f70e7-161">Next, you can learn more about private DNS zones.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f70e7-162">Using Azure DNS for private domains</span><span class="sxs-lookup"><span data-stu-id="f70e7-162">Using Azure DNS for private domains</span></span>](private-dns-overview.md)




