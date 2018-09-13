---
title: Manage Azure reserved IP addresses (Classic) - PowerShell | Microsoft Docs
description: Understand reserved IP addresses (Classic) and how to manage them using PowerShell.
services: virtual-network
documentationcenter: na
author: genlin
manager: cshepard
editor: tysonn
ms.assetid: 34652a55-3ab8-4c2d-8fb2-43684033b191
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/10/2016
ms.author: genli
ms.openlocfilehash: 25fe3c5361ff58f8d62d5d083b7a69f517d2a267
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44809080"
---
# <a name="reserved-ip-addresses-classic"></a><span data-ttu-id="21a19-103">Reserved IP addresses (Classic)</span><span class="sxs-lookup"><span data-stu-id="21a19-103">Reserved IP addresses (Classic)</span></span>

> [!div class="op_single_selector"]
> * [Azure portal](virtual-network-deploy-static-pip-arm-portal.md)
> * [PowerShell](virtual-network-deploy-static-pip-arm-ps.md)
> * [Azure CLI](virtual-network-deploy-static-pip-arm-cli.md)
> * [PowerShell (Classic)](virtual-networks-reserved-public-ip.md)

<span data-ttu-id="21a19-108">IP addresses in Azure fall into two categories: dynamic and reserved.</span><span class="sxs-lookup"><span data-stu-id="21a19-108">IP addresses in Azure fall into two categories: dynamic and reserved.</span></span> <span data-ttu-id="21a19-109">Public IP addresses managed by Azure are dynamic by default.</span><span class="sxs-lookup"><span data-stu-id="21a19-109">Public IP addresses managed by Azure are dynamic by default.</span></span> <span data-ttu-id="21a19-110">That means that the IP address used for a given cloud service (VIP) or to access a VM or role instance directly (ILPIP) can change from time to time, when resources are shut down or stopped (deallocated).</span><span class="sxs-lookup"><span data-stu-id="21a19-110">That means that the IP address used for a given cloud service (VIP) or to access a VM or role instance directly (ILPIP) can change from time to time, when resources are shut down or stopped (deallocated).</span></span>

<span data-ttu-id="21a19-111">To prevent IP addresses from changing, you can reserve an IP address.</span><span class="sxs-lookup"><span data-stu-id="21a19-111">To prevent IP addresses from changing, you can reserve an IP address.</span></span> <span data-ttu-id="21a19-112">Reserved IPs can be used only as a VIP, ensuring that the IP address for the cloud service remains the same, even as resources are shut down or stopped (deallocated).</span><span class="sxs-lookup"><span data-stu-id="21a19-112">Reserved IPs can be used only as a VIP, ensuring that the IP address for the cloud service remains the same, even as resources are shut down or stopped (deallocated).</span></span> <span data-ttu-id="21a19-113">Furthermore, you can convert existing dynamic IPs used as a VIP to a reserved IP address.</span><span class="sxs-lookup"><span data-stu-id="21a19-113">Furthermore, you can convert existing dynamic IPs used as a VIP to a reserved IP address.</span></span>

> [!IMPORTANT]
> Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md). This article covers using the classic deployment model. Microsoft recommends that most new deployments use the Resource Manager model. Learn how to reserve a static public IP address using the [Resource Manager deployment model](virtual-network-ip-addresses-overview-arm.md).

<span data-ttu-id="21a19-118">To learn more about IP addresses in Azure, read the [IP addresses](virtual-network-ip-addresses-overview-classic.md) article.</span><span class="sxs-lookup"><span data-stu-id="21a19-118">To learn more about IP addresses in Azure, read the [IP addresses](virtual-network-ip-addresses-overview-classic.md) article.</span></span>

## <a name="when-do-i-need-a-reserved-ip"></a><span data-ttu-id="21a19-119">When do I need a reserved IP?</span><span class="sxs-lookup"><span data-stu-id="21a19-119">When do I need a reserved IP?</span></span>
* <span data-ttu-id="21a19-120">**You want to ensure that the IP is reserved in your subscription**.</span><span class="sxs-lookup"><span data-stu-id="21a19-120">**You want to ensure that the IP is reserved in your subscription**.</span></span> <span data-ttu-id="21a19-121">If you want to reserve an IP address that is not released from your subscription under any circumstance, you should use a reserved public IP.</span><span class="sxs-lookup"><span data-stu-id="21a19-121">If you want to reserve an IP address that is not released from your subscription under any circumstance, you should use a reserved public IP.</span></span>  
* <span data-ttu-id="21a19-122">**You want your IP to stay with your cloud service even across stopped or deallocated state (VMs)**.</span><span class="sxs-lookup"><span data-stu-id="21a19-122">**You want your IP to stay with your cloud service even across stopped or deallocated state (VMs)**.</span></span> <span data-ttu-id="21a19-123">If you want your service to be accessed by using an IP address that doesn't change, even when VMs in the cloud service are shut down or stop (deallocated).</span><span class="sxs-lookup"><span data-stu-id="21a19-123">If you want your service to be accessed by using an IP address that doesn't change, even when VMs in the cloud service are shut down or stop (deallocated).</span></span>
* <span data-ttu-id="21a19-124">**You want to ensure that outbound traffic from Azure uses a predictable IP address**.</span><span class="sxs-lookup"><span data-stu-id="21a19-124">**You want to ensure that outbound traffic from Azure uses a predictable IP address**.</span></span> <span data-ttu-id="21a19-125">You may have your on-premises firewall configured to allow only traffic from specific IP addresses.</span><span class="sxs-lookup"><span data-stu-id="21a19-125">You may have your on-premises firewall configured to allow only traffic from specific IP addresses.</span></span> <span data-ttu-id="21a19-126">By reserving an IP, you know the source IP address, and don't need to update your firewall rules due to an IP change.</span><span class="sxs-lookup"><span data-stu-id="21a19-126">By reserving an IP, you know the source IP address, and don't need to update your firewall rules due to an IP change.</span></span>

## <a name="faq"></a><span data-ttu-id="21a19-127">FAQ</span><span class="sxs-lookup"><span data-stu-id="21a19-127">FAQ</span></span>
1. <span data-ttu-id="21a19-128">Can I use a reserved IP for all Azure services?</span><span class="sxs-lookup"><span data-stu-id="21a19-128">Can I use a reserved IP for all Azure services?</span></span> <br>
    <span data-ttu-id="21a19-129">No.</span><span class="sxs-lookup"><span data-stu-id="21a19-129">No.</span></span> <span data-ttu-id="21a19-130">Reserved IPs can only be used for VMs and cloud service instance roles exposed through a VIP.</span><span class="sxs-lookup"><span data-stu-id="21a19-130">Reserved IPs can only be used for VMs and cloud service instance roles exposed through a VIP.</span></span>
2. <span data-ttu-id="21a19-131">How many reserved IPs can I have?</span><span class="sxs-lookup"><span data-stu-id="21a19-131">How many reserved IPs can I have?</span></span> <br>
    <span data-ttu-id="21a19-132">For details, see the [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span><span class="sxs-lookup"><span data-stu-id="21a19-132">For details, see the [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>
3. <span data-ttu-id="21a19-133">Is there a charge for reserved IPs?</span><span class="sxs-lookup"><span data-stu-id="21a19-133">Is there a charge for reserved IPs?</span></span> <br>
    <span data-ttu-id="21a19-134">Sometimes.</span><span class="sxs-lookup"><span data-stu-id="21a19-134">Sometimes.</span></span> <span data-ttu-id="21a19-135">For pricing details, see the [Reserved IP Address Pricing Details](http://go.microsoft.com/fwlink/?LinkID=398482) page.</span><span class="sxs-lookup"><span data-stu-id="21a19-135">For pricing details, see the [Reserved IP Address Pricing Details](http://go.microsoft.com/fwlink/?LinkID=398482) page.</span></span>
4. <span data-ttu-id="21a19-136">How do I reserve an IP address?</span><span class="sxs-lookup"><span data-stu-id="21a19-136">How do I reserve an IP address?</span></span> <br>
    <span data-ttu-id="21a19-137">You can use PowerShell, the [Azure Management REST API](https://msdn.microsoft.com/library/azure/dn722420.aspx), or the [Azure portal](https://portal.azure.com) to reserve an IP address in an Azure region.</span><span class="sxs-lookup"><span data-stu-id="21a19-137">You can use PowerShell, the [Azure Management REST API](https://msdn.microsoft.com/library/azure/dn722420.aspx), or the [Azure portal](https://portal.azure.com) to reserve an IP address in an Azure region.</span></span> <span data-ttu-id="21a19-138">A reserved IP address is associated to your subscription.</span><span class="sxs-lookup"><span data-stu-id="21a19-138">A reserved IP address is associated to your subscription.</span></span>
5. <span data-ttu-id="21a19-139">Can I use a reserved IP with affinity group-based VNets?</span><span class="sxs-lookup"><span data-stu-id="21a19-139">Can I use a reserved IP with affinity group-based VNets?</span></span> <br>
    <span data-ttu-id="21a19-140">No.</span><span class="sxs-lookup"><span data-stu-id="21a19-140">No.</span></span> <span data-ttu-id="21a19-141">Reserved IPs are only supported in regional VNets.</span><span class="sxs-lookup"><span data-stu-id="21a19-141">Reserved IPs are only supported in regional VNets.</span></span> <span data-ttu-id="21a19-142">Reserved IPs are not supported for VNets that are associated with affinity groups.</span><span class="sxs-lookup"><span data-stu-id="21a19-142">Reserved IPs are not supported for VNets that are associated with affinity groups.</span></span> <span data-ttu-id="21a19-143">For more information about associating a VNet with a region or affinity group, see the [About Regional VNets and Affinity Groups](virtual-networks-migrate-to-regional-vnet.md) article.</span><span class="sxs-lookup"><span data-stu-id="21a19-143">For more information about associating a VNet with a region or affinity group, see the [About Regional VNets and Affinity Groups](virtual-networks-migrate-to-regional-vnet.md) article.</span></span>

## <a name="manage-reserved-vips"></a><span data-ttu-id="21a19-144">Manage reserved VIPs</span><span class="sxs-lookup"><span data-stu-id="21a19-144">Manage reserved VIPs</span></span>

<span data-ttu-id="21a19-145">Ensure you have installed and configured PowerShell by completing the steps in the [Install and configure PowerShell](/powershell/azure/overview) article.</span><span class="sxs-lookup"><span data-stu-id="21a19-145">Ensure you have installed and configured PowerShell by completing the steps in the [Install and configure PowerShell](/powershell/azure/overview) article.</span></span> 

<span data-ttu-id="21a19-146">Before you can use reserved IPs, you must add it to your subscription.</span><span class="sxs-lookup"><span data-stu-id="21a19-146">Before you can use reserved IPs, you must add it to your subscription.</span></span> <span data-ttu-id="21a19-147">To create a reserved IP from the pool of public IP addresses available in the *Central US* location, run the following command:</span><span class="sxs-lookup"><span data-stu-id="21a19-147">To create a reserved IP from the pool of public IP addresses available in the *Central US* location, run the following command:</span></span>

```powershell
New-AzureReservedIP –ReservedIPName MyReservedIP –Location "Central US"
```

<span data-ttu-id="21a19-148">Notice, however, that you cannot specify what IP is being reserved.</span><span class="sxs-lookup"><span data-stu-id="21a19-148">Notice, however, that you cannot specify what IP is being reserved.</span></span> <span data-ttu-id="21a19-149">To view what IP addresses are reserved in your subscription, run the following PowerShell command, and notice the values for *ReservedIPName* and *Address*:</span><span class="sxs-lookup"><span data-stu-id="21a19-149">To view what IP addresses are reserved in your subscription, run the following PowerShell command, and notice the values for *ReservedIPName* and *Address*:</span></span>

```powershell
Get-AzureReservedIP
```

<span data-ttu-id="21a19-150">Expected output:</span><span class="sxs-lookup"><span data-stu-id="21a19-150">Expected output:</span></span>

    ReservedIPName       : MyReservedIP
    Address              : 23.101.114.211
    Id                   : d73be9dd-db12-4b5e-98c8-bc62e7c42041
    Label                :
    Location             : Central US
    State                : Created
    InUse                : False
    ServiceName          :
    DeploymentName       :
    OperationDescription : Get-AzureReservedIP
    OperationId          : 55e4f245-82e4-9c66-9bd8-273e815ce30a
    OperationStatus      : Succeeded

>[!NOTE]
>When you create a reserved IP address with PowerShell, you cannot specify a resource group to create the reserved IP in. Azure places it into a resource group named *Default-Networking* automatically. If you create the reserved IP using the [Azure portal](http://portal.azure.com), you can specify any resource group you choose. If you create the reserved IP in a resource group other than *Default-Networking* however, whenever you reference the reserved IP with commands such as `Get-AzureReservedIP` and `Remove-AzureReservedIP`, you must reference the name *Group resource-group-name reserved-ip-name*.  For example, if you create a reserved IP named *myReservedIP* in a resource group named *myResourceGroup*, you must reference the name of the reserved IP as *Group myResourceGroup myReservedIP*.   

<span data-ttu-id="21a19-156">Once an IP is reserved, it remains associated to your subscription until you delete it.</span><span class="sxs-lookup"><span data-stu-id="21a19-156">Once an IP is reserved, it remains associated to your subscription until you delete it.</span></span> <span data-ttu-id="21a19-157">To delete a reserved IP, run the following PowerShell command:</span><span class="sxs-lookup"><span data-stu-id="21a19-157">To delete a reserved IP, run the following PowerShell command:</span></span>

```powershell
Remove-AzureReservedIP -ReservedIPName "MyReservedIP"
```

## <a name="reserve-the-ip-address-of-an-existing-cloud-service"></a><span data-ttu-id="21a19-158">Reserve the IP address of an existing cloud service</span><span class="sxs-lookup"><span data-stu-id="21a19-158">Reserve the IP address of an existing cloud service</span></span>
<span data-ttu-id="21a19-159">You can reserve the IP address of an existing cloud service by adding the `-ServiceName` parameter.</span><span class="sxs-lookup"><span data-stu-id="21a19-159">You can reserve the IP address of an existing cloud service by adding the `-ServiceName` parameter.</span></span> <span data-ttu-id="21a19-160">To reserve the IP address of a cloud service *TestService* in the *Central US* location, run the following PowerShell command:</span><span class="sxs-lookup"><span data-stu-id="21a19-160">To reserve the IP address of a cloud service *TestService* in the *Central US* location, run the following PowerShell command:</span></span>

```powershell
New-AzureReservedIP –ReservedIPName MyReservedIP –Location "Central US" -ServiceName TestService
```

## <a name="associate-a-reserved-ip-to-a-new-cloud-service"></a><span data-ttu-id="21a19-161">Associate a reserved IP to a new cloud service</span><span class="sxs-lookup"><span data-stu-id="21a19-161">Associate a reserved IP to a new cloud service</span></span>
<span data-ttu-id="21a19-162">The following script creates a new reserved IP, then associates it to a new cloud service named *TestService*.</span><span class="sxs-lookup"><span data-stu-id="21a19-162">The following script creates a new reserved IP, then associates it to a new cloud service named *TestService*.</span></span>

```powershell
New-AzureReservedIP –ReservedIPName MyReservedIP –Location "Central US"

$image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}

New-AzureVMConfig -Name TestVM -InstanceSize Small -ImageName $image.ImageName `
| Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
| New-AzureVM -ServiceName TestService -ReservedIPName MyReservedIP -Location "Central US"
```

> [!NOTE]
> When you create a reserved IP to use with a cloud service, you still refer to the VM by using *VIP:&lt;port number>* for inbound communication. Reserving an IP does not mean you can connect to the VM directly. The reserved IP is assigned to the cloud service that the VM has been deployed to. If you want to connect to a VM by IP directly, you have to configure an instance-level public IP. An instance-level public IP is a type of public IP (called an ILPIP) that is assigned directly to your VM. It cannot be reserved. For more information, read the [Instance-level Public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) article.
> 

## <a name="remove-a-reserved-ip-from-a-running-deployment"></a><span data-ttu-id="21a19-170">Remove a reserved IP from a running deployment</span><span class="sxs-lookup"><span data-stu-id="21a19-170">Remove a reserved IP from a running deployment</span></span>
<span data-ttu-id="21a19-171">To remove a reserved IP added to a new cloud service, run the following PowerShell command:</span><span class="sxs-lookup"><span data-stu-id="21a19-171">To remove a reserved IP added to a new cloud service, run the following PowerShell command:</span></span>

```powershell
Remove-AzureReservedIPAssociation -ReservedIPName MyReservedIP -ServiceName TestService
```

> [!NOTE]
> Removing a reserved IP from a running deployment does not remove the reservation from your subscription. It simply frees the IP to be used by another resource in your subscription.
> 

## <a name="associate-a-reserved-ip-to-a-running-deployment"></a><span data-ttu-id="21a19-174">Associate a reserved IP to a running deployment</span><span class="sxs-lookup"><span data-stu-id="21a19-174">Associate a reserved IP to a running deployment</span></span>
<span data-ttu-id="21a19-175">The following commands create a cloud service named *TestService2* with a new VM named *TestVM2*.</span><span class="sxs-lookup"><span data-stu-id="21a19-175">The following commands create a cloud service named *TestService2* with a new VM named *TestVM2*.</span></span> <span data-ttu-id="21a19-176">The existing reserved IP named *MyReservedIP* is then associated to the cloud service.</span><span class="sxs-lookup"><span data-stu-id="21a19-176">The existing reserved IP named *MyReservedIP* is then associated to the cloud service.</span></span>

```powershell
$image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}

New-AzureVMConfig -Name TestVM2 -InstanceSize Small -ImageName $image.ImageName `
| Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
| New-AzureVM -ServiceName TestService2 -Location "Central US"

Set-AzureReservedIPAssociation -ReservedIPName MyReservedIP -ServiceName TestService2
```

## <a name="associate-a-reserved-ip-to-a-cloud-service-by-using-a-service-configuration-file"></a><span data-ttu-id="21a19-177">Associate a reserved IP to a cloud service by using a service configuration file</span><span class="sxs-lookup"><span data-stu-id="21a19-177">Associate a reserved IP to a cloud service by using a service configuration file</span></span>
<span data-ttu-id="21a19-178">You can also associate a reserved IP to a cloud service by using a service configuration (CSCFG) file.</span><span class="sxs-lookup"><span data-stu-id="21a19-178">You can also associate a reserved IP to a cloud service by using a service configuration (CSCFG) file.</span></span> <span data-ttu-id="21a19-179">The following sample xml shows how to configure a cloud service to use a reserved VIP named *MyReservedIP*:</span><span class="sxs-lookup"><span data-stu-id="21a19-179">The following sample xml shows how to configure a cloud service to use a reserved VIP named *MyReservedIP*:</span></span>

    <?xml version="1.0" encoding="utf-8"?>
    <ServiceConfiguration serviceName="ReservedIPSample" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="4" osVersion="*" schemaVersion="2014-01.2.3">
      <Role name="WebRole1">
        <Instances count="1" />
        <ConfigurationSettings>
          <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true" />
        </ConfigurationSettings>
      </Role>
      <NetworkConfiguration>
        <AddressAssignments>
          <ReservedIPs>
           <ReservedIP name="MyReservedIP"/>
          </ReservedIPs>
        </AddressAssignments>
      </NetworkConfiguration>
    </ServiceConfiguration>

## <a name="next-steps"></a><span data-ttu-id="21a19-180">Next steps</span><span class="sxs-lookup"><span data-stu-id="21a19-180">Next steps</span></span>
* <span data-ttu-id="21a19-181">Understand how [IP addressing](virtual-network-ip-addresses-overview-classic.md) works in the classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="21a19-181">Understand how [IP addressing](virtual-network-ip-addresses-overview-classic.md) works in the classic deployment model.</span></span>
* <span data-ttu-id="21a19-182">Learn about [reserved private IP addresses](virtual-networks-reserved-private-ip.md).</span><span class="sxs-lookup"><span data-stu-id="21a19-182">Learn about [reserved private IP addresses](virtual-networks-reserved-private-ip.md).</span></span>
* <span data-ttu-id="21a19-183">Learn about [Instance Level Public IP (ILPIP) addresses](virtual-networks-instance-level-public-ip.md).</span><span class="sxs-lookup"><span data-stu-id="21a19-183">Learn about [Instance Level Public IP (ILPIP) addresses](virtual-networks-instance-level-public-ip.md).</span></span>

