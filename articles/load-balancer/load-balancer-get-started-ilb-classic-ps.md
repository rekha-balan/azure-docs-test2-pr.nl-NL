---
title: Create an Azure Internal load balancer - PowerShell classic | Microsoft Docs
description: Learn how to create an internal load balancer using PowerShell in the classic deployment model
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: ''
tags: azure-service-management
ms.assetid: 3be93168-3787-45a5-a194-9124fe386493
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: da46d13b89a728971be9386d1e8614b3309853b3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44671798"
---
# <a name="get-started-creating-an-internal-load-balancer-classic-using-powershell"></a><span data-ttu-id="654f4-103">Get started creating an internal load balancer (classic) using PowerShell</span><span class="sxs-lookup"><span data-stu-id="654f4-103">Get started creating an internal load balancer (classic) using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [PowerShell](../load-balancer/load-balancer-get-started-ilb-classic-ps.md)
> * [Azure CLI](../load-balancer/load-balancer-get-started-ilb-classic-cli.md)
> * [Cloud services](../load-balancer/load-balancer-get-started-ilb-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!IMPORTANT]
> Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).  This article covers using the classic deployment model. Microsoft recommends that most new deployments use the Resource Manager model. Learn how to [perform these steps using the Resource Manager model](load-balancer-get-started-ilb-arm-ps.md).

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-an-internal-load-balancer-set-for-virtual-machines"></a><span data-ttu-id="654f4-111">Create an internal load balancer set for virtual machines</span><span class="sxs-lookup"><span data-stu-id="654f4-111">Create an internal load balancer set for virtual machines</span></span>

<span data-ttu-id="654f4-112">To create an internal load balancer set and the servers that will send their traffic to it, you have to do the following:</span><span class="sxs-lookup"><span data-stu-id="654f4-112">To create an internal load balancer set and the servers that will send their traffic to it, you have to do the following:</span></span>

1. <span data-ttu-id="654f4-113">Create an instance of Internal Load Balancing that will be the endpoint of incoming traffic to be load balanced across the servers of a load-balanced set.</span><span class="sxs-lookup"><span data-stu-id="654f4-113">Create an instance of Internal Load Balancing that will be the endpoint of incoming traffic to be load balanced across the servers of a load-balanced set.</span></span>
2. <span data-ttu-id="654f4-114">Add endpoints corresponding to the virtual machines that will be receiving the incoming traffic.</span><span class="sxs-lookup"><span data-stu-id="654f4-114">Add endpoints corresponding to the virtual machines that will be receiving the incoming traffic.</span></span>
3. <span data-ttu-id="654f4-115">Configure the servers that will be sending the traffic to be load balanced to send their traffic to the virtual IP (VIP) address of the Internal Load Balancing instance.</span><span class="sxs-lookup"><span data-stu-id="654f4-115">Configure the servers that will be sending the traffic to be load balanced to send their traffic to the virtual IP (VIP) address of the Internal Load Balancing instance.</span></span>

### <a name="step-1-create-an-internal-load-balancing-instance"></a><span data-ttu-id="654f4-116">Step 1: Create an Internal Load Balancing instance</span><span class="sxs-lookup"><span data-stu-id="654f4-116">Step 1: Create an Internal Load Balancing instance</span></span>

<span data-ttu-id="654f4-117">For an existing cloud service or a cloud service deployed under a regional virtual network, you can create an Internal Load Balancing instance with the following Windows PowerShell commands:</span><span class="sxs-lookup"><span data-stu-id="654f4-117">For an existing cloud service or a cloud service deployed under a regional virtual network, you can create an Internal Load Balancing instance with the following Windows PowerShell commands:</span></span>

```powershell
$svc="<Cloud Service Name>"
$ilb="<Name of your ILB instance>"
$subnet="<Name of the subnet within your virtual network>"
$IP="<The IPv4 address to use on the subnet-optional>"

Add-AzureInternalLoadBalancer -ServiceName $svc -InternalLoadBalancerName $ilb –SubnetName $subnet –StaticVNetIPAddress $IP
```

<span data-ttu-id="654f4-118">Note that this use of the [Add-AzureEndpoint](https://msdn.microsoft.com/library/dn495300.aspx) Windows PowerShell cmdlet uses the DefaultProbe parameter set.</span><span class="sxs-lookup"><span data-stu-id="654f4-118">Note that this use of the [Add-AzureEndpoint](https://msdn.microsoft.com/library/dn495300.aspx) Windows PowerShell cmdlet uses the DefaultProbe parameter set.</span></span> <span data-ttu-id="654f4-119">For more information on additional parameter sets, see [Add-AzureEndpoint](https://msdn.microsoft.com/library/dn495300.aspx).</span><span class="sxs-lookup"><span data-stu-id="654f4-119">For more information on additional parameter sets, see [Add-AzureEndpoint](https://msdn.microsoft.com/library/dn495300.aspx).</span></span>

### <a name="step-2-add-endpoints-to-the-internal-load-balancing-instance"></a><span data-ttu-id="654f4-120">Step 2: Add endpoints to the Internal Load Balancing instance</span><span class="sxs-lookup"><span data-stu-id="654f4-120">Step 2: Add endpoints to the Internal Load Balancing instance</span></span>

<span data-ttu-id="654f4-121">Here is an example:</span><span class="sxs-lookup"><span data-stu-id="654f4-121">Here is an example:</span></span>

```powershell
$svc="mytestcloud"
$vmname="DB1"
$epname="TCP-1433-1433"
$lbsetname="lbset"
$prot="tcp"
$locport=1433
$pubport=1433
$ilb="ilbset"
Get-AzureVM –ServiceName $svc –Name $vmname | Add-AzureEndpoint -Name $epname -Lbset $lbsetname -Protocol $prot -LocalPort $locport -PublicPort $pubport –DefaultProbe -InternalLoadBalancerName $ilb | Update-AzureVM
```

### <a name="step-3-configure-your-servers-to-send-their-traffic-to-the-new-internal-load-balancing-endpoint"></a><span data-ttu-id="654f4-122">Step 3: Configure your servers to send their traffic to the new Internal Load Balancing endpoint</span><span class="sxs-lookup"><span data-stu-id="654f4-122">Step 3: Configure your servers to send their traffic to the new Internal Load Balancing endpoint</span></span>

<span data-ttu-id="654f4-123">You have to  configure the servers whose traffic is going to be load balanced to use the new IP address (the VIP) of the Internal Load Balancing instance.</span><span class="sxs-lookup"><span data-stu-id="654f4-123">You have to  configure the servers whose traffic is going to be load balanced to use the new IP address (the VIP) of the Internal Load Balancing instance.</span></span> <span data-ttu-id="654f4-124">This is the address on which the Internal Load Balancing instance is listening.</span><span class="sxs-lookup"><span data-stu-id="654f4-124">This is the address on which the Internal Load Balancing instance is listening.</span></span> <span data-ttu-id="654f4-125">In most cases, you need to just add or modify a DNS record for the VIP of the Internal Load Balancing instance.</span><span class="sxs-lookup"><span data-stu-id="654f4-125">In most cases, you need to just add or modify a DNS record for the VIP of the Internal Load Balancing instance.</span></span>

<span data-ttu-id="654f4-126">If you specified the IP address during the creation of the Internal Load Balancing instance, you already have the VIP.</span><span class="sxs-lookup"><span data-stu-id="654f4-126">If you specified the IP address during the creation of the Internal Load Balancing instance, you already have the VIP.</span></span> <span data-ttu-id="654f4-127">Otherwise, you can see the VIP from the following commands:</span><span class="sxs-lookup"><span data-stu-id="654f4-127">Otherwise, you can see the VIP from the following commands:</span></span>

```powershell
$svc="<Cloud Service Name>"
Get-AzureService -ServiceName $svc | Get-AzureInternalLoadBalancer
```

<span data-ttu-id="654f4-128">To use these commands, fill in the values and remove the < and >.</span><span class="sxs-lookup"><span data-stu-id="654f4-128">To use these commands, fill in the values and remove the < and >.</span></span> <span data-ttu-id="654f4-129">Here is an example:</span><span class="sxs-lookup"><span data-stu-id="654f4-129">Here is an example:</span></span>

```powershell
$svc="mytestcloud"
Get-AzureService -ServiceName $svc | Get-AzureInternalLoadBalancer
```

<span data-ttu-id="654f4-130">From the display of the Get-AzureInternalLoadBalancer command, note the IP address and make the necessary changes to your servers or DNS records to ensure that traffic gets sent to the VIP.</span><span class="sxs-lookup"><span data-stu-id="654f4-130">From the display of the Get-AzureInternalLoadBalancer command, note the IP address and make the necessary changes to your servers or DNS records to ensure that traffic gets sent to the VIP.</span></span>

> [!NOTE]
> The Microsoft Azure platform uses a static, publicly routable IPv4 address for a variety of administrative scenarios. The IP address is 168.63.129.16. This IP address should not be blocked by any firewalls, because it can cause unexpected behavior.
> With respect to Azure Internal Load Balancing, this IP address is used by monitoring probes from the load balancer to determine the health state for virtual machines in a load balanced set. If a Network Security Group is used to restrict traffic to Azure virtual machines in an internally load-balanced set or is applied to a Virtual Network Subnet, ensure that a Network Security Rule is added to allow traffic from 168.63.129.16.

## <a name="example-of-internal-load-balancing"></a><span data-ttu-id="654f4-136">Example of internal load balancing</span><span class="sxs-lookup"><span data-stu-id="654f4-136">Example of internal load balancing</span></span>

<span data-ttu-id="654f4-137">To step you through the end-to end process of creating a load-balanced set for two example configurations, see the following sections.</span><span class="sxs-lookup"><span data-stu-id="654f4-137">To step you through the end-to end process of creating a load-balanced set for two example configurations, see the following sections.</span></span>

### <a name="an-internet-facing-multi-tier-application"></a><span data-ttu-id="654f4-138">An Internet facing, multi-tier application</span><span class="sxs-lookup"><span data-stu-id="654f4-138">An Internet facing, multi-tier application</span></span>

<span data-ttu-id="654f4-139">You want to provide a load balanced database service for  a set of Internet-facing web servers.</span><span class="sxs-lookup"><span data-stu-id="654f4-139">You want to provide a load balanced database service for  a set of Internet-facing web servers.</span></span> <span data-ttu-id="654f4-140">Both sets of servers are hosted in a single Azure cloud service.</span><span class="sxs-lookup"><span data-stu-id="654f4-140">Both sets of servers are hosted in a single Azure cloud service.</span></span> <span data-ttu-id="654f4-141">Web server traffic to TCP port 1433 must be distributed among two virtual machines in the database tier.</span><span class="sxs-lookup"><span data-stu-id="654f4-141">Web server traffic to TCP port 1433 must be distributed among two virtual machines in the database tier.</span></span> <span data-ttu-id="654f4-142">Figure 1 shows the configuration.</span><span class="sxs-lookup"><span data-stu-id="654f4-142">Figure 1 shows the configuration.</span></span>

![Internal load-balanced set for the database tier](https://docstestmedia1.blob.core.windows.net/azure-media/articles/load-balancer/media/load-balancer-internal-getstarted/IC736321.png)

<span data-ttu-id="654f4-144">The configuration consists of the following:</span><span class="sxs-lookup"><span data-stu-id="654f4-144">The configuration consists of the following:</span></span>

* <span data-ttu-id="654f4-145">The existing cloud service hosting the virtual machines is named mytestcloud.</span><span class="sxs-lookup"><span data-stu-id="654f4-145">The existing cloud service hosting the virtual machines is named mytestcloud.</span></span>
* <span data-ttu-id="654f4-146">The two existing database servers are named DB1, DB2.</span><span class="sxs-lookup"><span data-stu-id="654f4-146">The two existing database servers are named DB1, DB2.</span></span>
* <span data-ttu-id="654f4-147">Web servers in the web tier connect to the database servers in the database tier by using the private IP address.</span><span class="sxs-lookup"><span data-stu-id="654f4-147">Web servers in the web tier connect to the database servers in the database tier by using the private IP address.</span></span> <span data-ttu-id="654f4-148">Another option is to use your own DNS for the virtual network and manually register an A record for the internal load balancer set.</span><span class="sxs-lookup"><span data-stu-id="654f4-148">Another option is to use your own DNS for the virtual network and manually register an A record for the internal load balancer set.</span></span>

<span data-ttu-id="654f4-149">The following commands configure a new Internal Load Balancing instance named **ILBset** and add endpoints to the virtual machines corresponding to the two database servers:</span><span class="sxs-lookup"><span data-stu-id="654f4-149">The following commands configure a new Internal Load Balancing instance named **ILBset** and add endpoints to the virtual machines corresponding to the two database servers:</span></span>

```powershell
$svc="mytestcloud"
$ilb="ilbset"
Add-AzureInternalLoadBalancer -ServiceName $svc -InternalLoadBalancerName $ilb
$prot="tcp"
$locport=1433
$pubport=1433
$epname="TCP-1433-1433"
$lbsetname="lbset"
$vmname="DB1"
Get-AzureVM –ServiceName $svc –Name $vmname | Add-AzureEndpoint -Name $epname -LbSetName $lbsetname -Protocol $prot -LocalPort $locport -PublicPort $pubport –DefaultProbe -InternalLoadBalancerName $ilb | Update-AzureVM

$epname="TCP-1433-1433-2"
$vmname="DB2"
Get-AzureVM –ServiceName $svc –Name $vmname | Add-AzureEndpoint -Name $epname -LbSetName $lbsetname -Protocol $prot -LocalPort $locport -PublicPort $pubport –DefaultProbe -InternalLoadBalancerName $ilb | Update-AzureVM
```

## <a name="remove-an-internal-load-balancing-configuration"></a><span data-ttu-id="654f4-150">Remove an Internal Load Balancing configuration</span><span class="sxs-lookup"><span data-stu-id="654f4-150">Remove an Internal Load Balancing configuration</span></span>

<span data-ttu-id="654f4-151">To remove a virtual machine as an endpoint from an internal load balancer instance, use the following commands:</span><span class="sxs-lookup"><span data-stu-id="654f4-151">To remove a virtual machine as an endpoint from an internal load balancer instance, use the following commands:</span></span>

```powershell
$svc="<Cloud service name>"
$vmname="<Name of the VM>"
$epname="<Name of the endpoint>"
Get-AzureVM -ServiceName $svc -Name $vmname | Remove-AzureEndpoint -Name $epname | Update-AzureVM
```

<span data-ttu-id="654f4-152">To use these commands, fill in the values, removing the < and >.</span><span class="sxs-lookup"><span data-stu-id="654f4-152">To use these commands, fill in the values, removing the < and >.</span></span>

<span data-ttu-id="654f4-153">Here is an example:</span><span class="sxs-lookup"><span data-stu-id="654f4-153">Here is an example:</span></span>

```powershell
$svc="mytestcloud"
$vmname="DB1"
$epname="TCP-1433-1433"
Get-AzureVM -ServiceName $svc -Name $vmname | Remove-AzureEndpoint -Name $epname | Update-AzureVM
```

<span data-ttu-id="654f4-154">To remove an internal load balancer instance from a cloud service, use the following commands:</span><span class="sxs-lookup"><span data-stu-id="654f4-154">To remove an internal load balancer instance from a cloud service, use the following commands:</span></span>

```powershell
$svc="<Cloud service name>"
Remove-AzureInternalLoadBalancer -ServiceName $svc
```

<span data-ttu-id="654f4-155">To use these commands, fill in the value and remove the < and >.</span><span class="sxs-lookup"><span data-stu-id="654f4-155">To use these commands, fill in the value and remove the < and >.</span></span>

<span data-ttu-id="654f4-156">Here is an example:</span><span class="sxs-lookup"><span data-stu-id="654f4-156">Here is an example:</span></span>

```powershell
$svc="mytestcloud"
Remove-AzureInternalLoadBalancer -ServiceName $svc
```

## <a name="additional-information-about-internal-load-balancer-cmdlets"></a><span data-ttu-id="654f4-157">Additional information about internal load balancer cmdlets</span><span class="sxs-lookup"><span data-stu-id="654f4-157">Additional information about internal load balancer cmdlets</span></span>

<span data-ttu-id="654f4-158">To obtain additional information about Internal Load Balancing cmdlets, run the following commands at a Windows PowerShell prompt:</span><span class="sxs-lookup"><span data-stu-id="654f4-158">To obtain additional information about Internal Load Balancing cmdlets, run the following commands at a Windows PowerShell prompt:</span></span>

```powershell
Get-Help New-AzureInternalLoadBalancerConfig -full
Get-Help Add-AzureInternalLoadBalancer -full
Get-Help Get-AzureInternalLoadbalancer -full
Get-Help Remove-AzureInternalLoadBalancer -full
```

## <a name="next-steps"></a><span data-ttu-id="654f4-159">Next steps</span><span class="sxs-lookup"><span data-stu-id="654f4-159">Next steps</span></span>

[<span data-ttu-id="654f4-160">Configure a load balancer distribution mode using source IP affinity</span><span class="sxs-lookup"><span data-stu-id="654f4-160">Configure a load balancer distribution mode using source IP affinity</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="654f4-161">Configure idle TCP timeout settings for your load balancer</span><span class="sxs-lookup"><span data-stu-id="654f4-161">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)


