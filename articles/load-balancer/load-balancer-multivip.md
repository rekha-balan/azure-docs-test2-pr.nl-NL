---
title: Mutiple VIPs for a cloud service
description: Overview of multiVIP and how to set multiple VIPs on a cloud service
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: 85f6d26a-3df5-4b8e-96a1-92b2793b5284
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: cf0ee68ddc647331093dab612b91d55cdf4ca445
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552410"
---
# <a name="configure-multiple-vips-for-a-cloud-service"></a><span data-ttu-id="bb961-103">Configure multiple VIPs for a cloud service</span><span class="sxs-lookup"><span data-stu-id="bb961-103">Configure multiple VIPs for a cloud service</span></span>

<span data-ttu-id="bb961-104">You can access Azure cloud services over the public Internet by using an IP address provided by Azure.</span><span class="sxs-lookup"><span data-stu-id="bb961-104">You can access Azure cloud services over the public Internet by using an IP address provided by Azure.</span></span> <span data-ttu-id="bb961-105">This public IP address is referred to as a VIP (virtual IP) since it is linked to the Azure load balancer, and not the Virtual Machine (VM) instances within the cloud service.</span><span class="sxs-lookup"><span data-stu-id="bb961-105">This public IP address is referred to as a VIP (virtual IP) since it is linked to the Azure load balancer, and not the Virtual Machine (VM) instances within the cloud service.</span></span> <span data-ttu-id="bb961-106">You can access any VM instance within a cloud service by using a single VIP.</span><span class="sxs-lookup"><span data-stu-id="bb961-106">You can access any VM instance within a cloud service by using a single VIP.</span></span>

<span data-ttu-id="bb961-107">However, there are scenarios in which you may need more than one VIP as an entry point to the same cloud service.</span><span class="sxs-lookup"><span data-stu-id="bb961-107">However, there are scenarios in which you may need more than one VIP as an entry point to the same cloud service.</span></span> <span data-ttu-id="bb961-108">For instance, your cloud service may host multiple websites that require SSL connectivity using the default port of 443, as each site is hosted for a different customer, or tenant.</span><span class="sxs-lookup"><span data-stu-id="bb961-108">For instance, your cloud service may host multiple websites that require SSL connectivity using the default port of 443, as each site is hosted for a different customer, or tenant.</span></span> <span data-ttu-id="bb961-109">In this scenario, you need to have a different public facing IP address for each website.</span><span class="sxs-lookup"><span data-stu-id="bb961-109">In this scenario, you need to have a different public facing IP address for each website.</span></span> <span data-ttu-id="bb961-110">The diagram below illustrates a typical multi-tenant web hosting with a need for multiple SSL certificates on the same public port.</span><span class="sxs-lookup"><span data-stu-id="bb961-110">The diagram below illustrates a typical multi-tenant web hosting with a need for multiple SSL certificates on the same public port.</span></span>

![Multi VIP SSL scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/load-balancer/media/load-balancer-multivip/Figure1.png)

<span data-ttu-id="bb961-112">In the example above, all VIPs use the same public port (443) and traffic is redirected to one or more load balanced VMs on a unique private port for the internal IP address of the cloud service hosting all the websites.</span><span class="sxs-lookup"><span data-stu-id="bb961-112">In the example above, all VIPs use the same public port (443) and traffic is redirected to one or more load balanced VMs on a unique private port for the internal IP address of the cloud service hosting all the websites.</span></span>

> [!NOTE]
> <span data-ttu-id="bb961-113">Another situation requiring the use the multiple VIPs is hosting multiple SQL AlwaysOn availability group listeners on the same set of Virtual Machines.</span><span class="sxs-lookup"><span data-stu-id="bb961-113">Another situation requiring the use the multiple VIPs is hosting multiple SQL AlwaysOn availability group listeners on the same set of Virtual Machines.</span></span>

<span data-ttu-id="bb961-114">VIPs are dynamic by default, which means that the actual IP address assigned to the cloud service may change over time.</span><span class="sxs-lookup"><span data-stu-id="bb961-114">VIPs are dynamic by default, which means that the actual IP address assigned to the cloud service may change over time.</span></span> <span data-ttu-id="bb961-115">To prevent that from happening, you can reserve a VIP for your service.</span><span class="sxs-lookup"><span data-stu-id="bb961-115">To prevent that from happening, you can reserve a VIP for your service.</span></span> <span data-ttu-id="bb961-116">To learn more about reserved VIPs, see [Reserved Public IP](../virtual-network/virtual-networks-reserved-public-ip.md).</span><span class="sxs-lookup"><span data-stu-id="bb961-116">To learn more about reserved VIPs, see [Reserved Public IP](../virtual-network/virtual-networks-reserved-public-ip.md).</span></span>

> [!NOTE]
> <span data-ttu-id="bb961-117">Please see [IP Address pricing](https://azure.microsoft.com/pricing/details/ip-addresses/) for information on pricing on VIPs and reserved IPs.</span><span class="sxs-lookup"><span data-stu-id="bb961-117">Please see [IP Address pricing](https://azure.microsoft.com/pricing/details/ip-addresses/) for information on pricing on VIPs and reserved IPs.</span></span>

<span data-ttu-id="bb961-118">You can use PowerShell to verify the VIPs used by your cloud services, as well as add and remove VIPs, associate a VIP to an endpoint, and configure load balancing on a specific VIP.</span><span class="sxs-lookup"><span data-stu-id="bb961-118">You can use PowerShell to verify the VIPs used by your cloud services, as well as add and remove VIPs, associate a VIP to an endpoint, and configure load balancing on a specific VIP.</span></span>

## <a name="limitations"></a><span data-ttu-id="bb961-119">Limitations</span><span class="sxs-lookup"><span data-stu-id="bb961-119">Limitations</span></span>

<span data-ttu-id="bb961-120">At this time, Multi VIP functionality is limited to the following scenarios:</span><span class="sxs-lookup"><span data-stu-id="bb961-120">At this time, Multi VIP functionality is limited to the following scenarios:</span></span>

* <span data-ttu-id="bb961-121">**IaaS only**.</span><span class="sxs-lookup"><span data-stu-id="bb961-121">**IaaS only**.</span></span> <span data-ttu-id="bb961-122">You can only enable Multi VIP for cloud services that contain VMs.</span><span class="sxs-lookup"><span data-stu-id="bb961-122">You can only enable Multi VIP for cloud services that contain VMs.</span></span> <span data-ttu-id="bb961-123">You cannot use Multi VIP in PaaS scenarios with role instances.</span><span class="sxs-lookup"><span data-stu-id="bb961-123">You cannot use Multi VIP in PaaS scenarios with role instances.</span></span>
* <span data-ttu-id="bb961-124">**PowerShell only**.</span><span class="sxs-lookup"><span data-stu-id="bb961-124">**PowerShell only**.</span></span> <span data-ttu-id="bb961-125">You can only manage Multi VIP by using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bb961-125">You can only manage Multi VIP by using PowerShell.</span></span>

<span data-ttu-id="bb961-126">These limitations are temporary, and may change at any time.</span><span class="sxs-lookup"><span data-stu-id="bb961-126">These limitations are temporary, and may change at any time.</span></span> <span data-ttu-id="bb961-127">Make sure to revisit this page to verify future changes.</span><span class="sxs-lookup"><span data-stu-id="bb961-127">Make sure to revisit this page to verify future changes.</span></span>

## <a name="how-to-add-a-vip-to-a-cloud-service"></a><span data-ttu-id="bb961-128">How to add a VIP to a cloud service</span><span class="sxs-lookup"><span data-stu-id="bb961-128">How to add a VIP to a cloud service</span></span>
<span data-ttu-id="bb961-129">To add a VIP to your service, run the following PowerShell command:</span><span class="sxs-lookup"><span data-stu-id="bb961-129">To add a VIP to your service, run the following PowerShell command:</span></span>

```powershell
Add-AzureVirtualIP -VirtualIPName Vip3 -ServiceName myService
```

<span data-ttu-id="bb961-130">This command displays a result similar to the following sample:</span><span class="sxs-lookup"><span data-stu-id="bb961-130">This command displays a result similar to the following sample:</span></span>

    OperationDescription OperationId                          OperationStatus
    -------------------- -----------                          ---------------
    Add-AzureVirtualIP   4bd7b638-d2e7-216f-ba38-5221233d70ce Succeeded

## <a name="how-to-remove-a-vip-from-a-cloud-service"></a><span data-ttu-id="bb961-131">How to remove a VIP from a cloud service</span><span class="sxs-lookup"><span data-stu-id="bb961-131">How to remove a VIP from a cloud service</span></span>
<span data-ttu-id="bb961-132">To remove the VIP added to your service in the example above, run the following PowerShell command:</span><span class="sxs-lookup"><span data-stu-id="bb961-132">To remove the VIP added to your service in the example above, run the following PowerShell command:</span></span>

```powershell
Remove-AzureVirtualIP -VirtualIPName Vip3 -ServiceName myService
```

> [!IMPORTANT]
> <span data-ttu-id="bb961-133">You can only remove a VIP if it has no endpoints associated to it.</span><span class="sxs-lookup"><span data-stu-id="bb961-133">You can only remove a VIP if it has no endpoints associated to it.</span></span>


## <a name="how-to-retrieve-vip-information-from-a-cloud-service"></a><span data-ttu-id="bb961-134">How to retrieve VIP information from a Cloud Service</span><span class="sxs-lookup"><span data-stu-id="bb961-134">How to retrieve VIP information from a Cloud Service</span></span>
<span data-ttu-id="bb961-135">To retrieve the VIPs associated with a cloud service, run the following PowerShell script:</span><span class="sxs-lookup"><span data-stu-id="bb961-135">To retrieve the VIPs associated with a cloud service, run the following PowerShell script:</span></span>

```powershell
$deployment = Get-AzureDeployment -ServiceName myService
$deployment.VirtualIPs
```

<span data-ttu-id="bb961-136">The script displays a result similar to the following sample:</span><span class="sxs-lookup"><span data-stu-id="bb961-136">The script displays a result similar to the following sample:</span></span>

    Address         : 191.238.74.148
    IsDnsProgrammed : True
    Name            : Vip1
    ReservedIPName  :
    ExtensionData   :

    Address         :
    IsDnsProgrammed :
    Name            : Vip2
    ReservedIPName  :
    ExtensionData   :

    Address         :
    IsDnsProgrammed :
    Name            : Vip3
    ReservedIPName  :
    ExtensionData   :

<span data-ttu-id="bb961-137">In this example, the cloud service has 3 VIPs:</span><span class="sxs-lookup"><span data-stu-id="bb961-137">In this example, the cloud service has 3 VIPs:</span></span>

* <span data-ttu-id="bb961-138">**Vip1** is the default VIP, you know that because the value for IsDnsProgrammedName is set to true.</span><span class="sxs-lookup"><span data-stu-id="bb961-138">**Vip1** is the default VIP, you know that because the value for IsDnsProgrammedName is set to true.</span></span>
* <span data-ttu-id="bb961-139">**Vip2** and **Vip3** are not used as they do not have any IP addresses.</span><span class="sxs-lookup"><span data-stu-id="bb961-139">**Vip2** and **Vip3** are not used as they do not have any IP addresses.</span></span> <span data-ttu-id="bb961-140">They will only be used if you associate an endpoint to the VIP.</span><span class="sxs-lookup"><span data-stu-id="bb961-140">They will only be used if you associate an endpoint to the VIP.</span></span>

> [!NOTE]
> <span data-ttu-id="bb961-141">Your subscription will only be charged for extra VIPs once they are associated with an endpoint.</span><span class="sxs-lookup"><span data-stu-id="bb961-141">Your subscription will only be charged for extra VIPs once they are associated with an endpoint.</span></span> <span data-ttu-id="bb961-142">For more information on pricing, see [IP Address pricing](https://azure.microsoft.com/pricing/details/ip-addresses/).</span><span class="sxs-lookup"><span data-stu-id="bb961-142">For more information on pricing, see [IP Address pricing](https://azure.microsoft.com/pricing/details/ip-addresses/).</span></span>

## <a name="how-to-associate-a-vip-to-an-endpoint"></a><span data-ttu-id="bb961-143">How to associate a VIP to an endpoint</span><span class="sxs-lookup"><span data-stu-id="bb961-143">How to associate a VIP to an endpoint</span></span>

<span data-ttu-id="bb961-144">To associate a VIP on a cloud service to an endpoint, run the following PowerShell command:</span><span class="sxs-lookup"><span data-stu-id="bb961-144">To associate a VIP on a cloud service to an endpoint, run the following PowerShell command:</span></span>

```powershell
Get-AzureVM -ServiceName myService -Name myVM1 |
    Add-AzureEndpoint -Name myEndpoint -Protocol tcp -LocalPort 8080 -PublicPort 80 -VirtualIPName Vip2 |
    Update-AzureVM
```

<span data-ttu-id="bb961-145">The command creates an endpoint linked to the VIP called *Vip2* on port *80*, and links it to the VM named *myVM1* in a cloud service named *myService* using *TCP* on port *8080*.</span><span class="sxs-lookup"><span data-stu-id="bb961-145">The command creates an endpoint linked to the VIP called *Vip2* on port *80*, and links it to the VM named *myVM1* in a cloud service named *myService* using *TCP* on port *8080*.</span></span>

<span data-ttu-id="bb961-146">To verify the configuration, run the following PowerShell command:</span><span class="sxs-lookup"><span data-stu-id="bb961-146">To verify the configuration, run the following PowerShell command:</span></span>

```powershell
$deployment = Get-AzureDeployment -ServiceName myService
$deployment.VirtualIPs
```

<span data-ttu-id="bb961-147">The output looks similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="bb961-147">The output looks similar to the following example:</span></span>

    Address         : 191.238.74.148
    IsDnsProgrammed : True
    Name            : Vip1
    ReservedIPName  :
    ExtensionData   :

    Address         : 191.238.74.13
    IsDnsProgrammed :
    Name            : Vip2
    ReservedIPName  :
    ExtensionData   :

    Address         :
    IsDnsProgrammed :
    Name            : Vip3
    ReservedIPName  :
    ExtensionData   :

## <a name="how-to-enable-load-balancing-on-a-specific-vip"></a><span data-ttu-id="bb961-148">How to enable load balancing on a specific VIP</span><span class="sxs-lookup"><span data-stu-id="bb961-148">How to enable load balancing on a specific VIP</span></span>

<span data-ttu-id="bb961-149">You can associate a single VIP with multiple virtual machines for load balancing purposes.</span><span class="sxs-lookup"><span data-stu-id="bb961-149">You can associate a single VIP with multiple virtual machines for load balancing purposes.</span></span> <span data-ttu-id="bb961-150">For example, you have a cloud service named *myService*, and two virtual machines named *myVM1* and *myVM2*.</span><span class="sxs-lookup"><span data-stu-id="bb961-150">For example, you have a cloud service named *myService*, and two virtual machines named *myVM1* and *myVM2*.</span></span> <span data-ttu-id="bb961-151">And your cloud service has multiple VIPs, one of them named *Vip2*.</span><span class="sxs-lookup"><span data-stu-id="bb961-151">And your cloud service has multiple VIPs, one of them named *Vip2*.</span></span> <span data-ttu-id="bb961-152">If you want to ensure that all traffic to port *81* on *Vip2* is balanced between *myVM1* and *myVM2* on port *8181*, run the following PowerShell script:</span><span class="sxs-lookup"><span data-stu-id="bb961-152">If you want to ensure that all traffic to port *81* on *Vip2* is balanced between *myVM1* and *myVM2* on port *8181*, run the following PowerShell script:</span></span>

```powershell
Get-AzureVM -ServiceName myService -Name myVM1 |
    Add-AzureEndpoint -Name myEndpoint -LoadBalancedEndpointSetName myLBSet -Protocol tcp -LocalPort 8181 -PublicPort 81 -VirtualIPName Vip2 -DefaultProbe |
    Update-AzureVM

Get-AzureVM -ServiceName myService -Name myVM2 |
    Add-AzureEndpoint -Name myEndpoint -LoadBalancedEndpointSetName myLBSet -Protocol tcp -LocalPort 8181 -PublicPort 81 -VirtualIPName Vip2  -DefaultProbe |
    Update-AzureVM
```

<span data-ttu-id="bb961-153">You can also update your load balancer to use a different VIP.</span><span class="sxs-lookup"><span data-stu-id="bb961-153">You can also update your load balancer to use a different VIP.</span></span> <span data-ttu-id="bb961-154">For example, if you run the PowerShell command below, you will change the load balancing set to use a VIP named Vip1:</span><span class="sxs-lookup"><span data-stu-id="bb961-154">For example, if you run the PowerShell command below, you will change the load balancing set to use a VIP named Vip1:</span></span>

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName myService -LBSetName myLBSet -VirtualIPName Vip1
```

## <a name="next-steps"></a><span data-ttu-id="bb961-155">Next Steps</span><span class="sxs-lookup"><span data-stu-id="bb961-155">Next Steps</span></span>

[<span data-ttu-id="bb961-156">Log analytics for Azure Load Balance</span><span class="sxs-lookup"><span data-stu-id="bb961-156">Log analytics for Azure Load Balance</span></span>](load-balancer-monitor-log.md)

[<span data-ttu-id="bb961-157">Internet facing load balancer overview</span><span class="sxs-lookup"><span data-stu-id="bb961-157">Internet facing load balancer overview</span></span>](load-balancer-internet-overview.md)

[<span data-ttu-id="bb961-158">Get started on Internet facing load balancer</span><span class="sxs-lookup"><span data-stu-id="bb961-158">Get started on Internet facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="bb961-159">Virtual Network Overview</span><span class="sxs-lookup"><span data-stu-id="bb961-159">Virtual Network Overview</span></span>](../virtual-network/virtual-networks-overview.md)

[<span data-ttu-id="bb961-160">Reserved IP REST APIs</span><span class="sxs-lookup"><span data-stu-id="bb961-160">Reserved IP REST APIs</span></span>](https://msdn.microsoft.com/library/azure/dn722420.aspx)

