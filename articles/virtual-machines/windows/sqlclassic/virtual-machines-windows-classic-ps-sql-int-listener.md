---
title: Configure an ILB Listener for Always On Availability Groups | Microsoft Docs
description: This tutorial uses resources created with  the classic deployment model, and creates an Always On Availability Group Listener in Azure using an Internal Load Balancer (ILB).
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: ''
tags: azure-service-management
ms.assetid: 291288a0-740b-4cfa-af62-053218beba77
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 03/01/2017
ms.author: mikeray
ms.openlocfilehash: d09d2b869606995d227aa485a85acd67c18ee4e5
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550997"
---
# <a name="configure-an-ilb-listener-for-always-on-availability-groups-in-azure"></a><span data-ttu-id="da70a-103">Configure an ILB listener for Always On Availability Groups in Azure</span><span class="sxs-lookup"><span data-stu-id="da70a-103">Configure an ILB listener for Always On Availability Groups in Azure</span></span>
> [!div class="op_single_selector"]
> * [Internal Listener](../classic/ps-sql-int-listener.md)
> * [External Listener](../classic/ps-sql-ext-listener.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="da70a-106">Overview</span><span class="sxs-lookup"><span data-stu-id="da70a-106">Overview</span></span>
<span data-ttu-id="da70a-107">This topic shows you how to configure a listener for an Always On Availability Group by using an **Internal Load Balancer (ILB)**.</span><span class="sxs-lookup"><span data-stu-id="da70a-107">This topic shows you how to configure a listener for an Always On Availability Group by using an **Internal Load Balancer (ILB)**.</span></span>

> [!IMPORTANT] 
> Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md). This article covers using the Classic deployment model. Microsoft recommends that most new deployments use the Resource Manager model.

<span data-ttu-id="da70a-111">To configure an ILB listener for an Always On availability group in Resource Manager model, see [Configure an internal load balancer for an Always On availability group in Azure](../sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).</span><span class="sxs-lookup"><span data-stu-id="da70a-111">To configure an ILB listener for an Always On availability group in Resource Manager model, see [Configure an internal load balancer for an Always On availability group in Azure](../sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).</span></span>

<span data-ttu-id="da70a-112">Your Availability Group can contain replicas that are on-premises only, Azure only, or span both on-premises and Azure for hybrid configurations.</span><span class="sxs-lookup"><span data-stu-id="da70a-112">Your Availability Group can contain replicas that are on-premises only, Azure only, or span both on-premises and Azure for hybrid configurations.</span></span> <span data-ttu-id="da70a-113">Azure replicas can reside within the same region or across multiple regions using multiple virtual networks (VNets).</span><span class="sxs-lookup"><span data-stu-id="da70a-113">Azure replicas can reside within the same region or across multiple regions using multiple virtual networks (VNets).</span></span> <span data-ttu-id="da70a-114">The steps below assume you have already [configured an availability group](../classic/portal-sql-alwayson-availability-groups.md) but have not configured a listener.</span><span class="sxs-lookup"><span data-stu-id="da70a-114">The steps below assume you have already [configured an availability group](../classic/portal-sql-alwayson-availability-groups.md) but have not configured a listener.</span></span>

## <a name="guidelines-and-limitations-for-internal-listeners"></a><span data-ttu-id="da70a-115">Guidelines and limitations for internal listeners</span><span class="sxs-lookup"><span data-stu-id="da70a-115">Guidelines and limitations for internal listeners</span></span>
<span data-ttu-id="da70a-116">Note the following guidelines on the availability group listener in Azure using ILB:</span><span class="sxs-lookup"><span data-stu-id="da70a-116">Note the following guidelines on the availability group listener in Azure using ILB:</span></span>

* <span data-ttu-id="da70a-117">The availability group listener is supported on Windows Server 2008 R2, Windows Server 2012, and Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="da70a-117">The availability group listener is supported on Windows Server 2008 R2, Windows Server 2012, and Windows Server 2012 R2.</span></span>
* <span data-ttu-id="da70a-118">Only one internal availability group listener is supported per cloud service, because the listener is configured to the ILB, and there is only one ILB per cloud service.</span><span class="sxs-lookup"><span data-stu-id="da70a-118">Only one internal availability group listener is supported per cloud service, because the listener is configured to the ILB, and there is only one ILB per cloud service.</span></span> <span data-ttu-id="da70a-119">However, it is possible to create multiple external listeners.</span><span class="sxs-lookup"><span data-stu-id="da70a-119">However, it is possible to create multiple external listeners.</span></span> <span data-ttu-id="da70a-120">For more information, see [Configure an external listener for Always On Availability Groups in Azure](../classic/ps-sql-ext-listener.md).</span><span class="sxs-lookup"><span data-stu-id="da70a-120">For more information, see [Configure an external listener for Always On Availability Groups in Azure](../classic/ps-sql-ext-listener.md).</span></span>

## <a name="determine-the-accessibility-of-the-listener"></a><span data-ttu-id="da70a-121">Determine the accessibility of the listener</span><span class="sxs-lookup"><span data-stu-id="da70a-121">Determine the accessibility of the listener</span></span>
[!INCLUDE [ag-listener-accessibility](../../../../includes/virtual-machines-ag-listener-determine-accessibility.md)]

<span data-ttu-id="da70a-122">This article focuses on creating a listener that uses an **Internal Load Balancer (ILB)**.</span><span class="sxs-lookup"><span data-stu-id="da70a-122">This article focuses on creating a listener that uses an **Internal Load Balancer (ILB)**.</span></span> <span data-ttu-id="da70a-123">If you need an public/external listener, see the version of this article that provides steps for setting up an [external listener](../classic/ps-sql-ext-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="da70a-123">If you need an public/external listener, see the version of this article that provides steps for setting up an [external listener](../classic/ps-sql-ext-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

## <a name="create-load-balanced-vm-endpoints-with-direct-server-return"></a><span data-ttu-id="da70a-124">Create load-balanced VM endpoints with direct server return</span><span class="sxs-lookup"><span data-stu-id="da70a-124">Create load-balanced VM endpoints with direct server return</span></span>
<span data-ttu-id="da70a-125">For ILB, you must first create the internal load balancer.</span><span class="sxs-lookup"><span data-stu-id="da70a-125">For ILB, you must first create the internal load balancer.</span></span> <span data-ttu-id="da70a-126">This is done in the script below.</span><span class="sxs-lookup"><span data-stu-id="da70a-126">This is done in the script below.</span></span>

<span data-ttu-id="da70a-127">You must create a load-balanced endpoint for each VM hosting an Azure replica.</span><span class="sxs-lookup"><span data-stu-id="da70a-127">You must create a load-balanced endpoint for each VM hosting an Azure replica.</span></span> <span data-ttu-id="da70a-128">If you have replicas in multiple regions, each replica for that region must be in the same cloud service in the same VNet.</span><span class="sxs-lookup"><span data-stu-id="da70a-128">If you have replicas in multiple regions, each replica for that region must be in the same cloud service in the same VNet.</span></span> <span data-ttu-id="da70a-129">Creating Availability Group replicas that span multiple Azure regions requires configuring multiple VNets.</span><span class="sxs-lookup"><span data-stu-id="da70a-129">Creating Availability Group replicas that span multiple Azure regions requires configuring multiple VNets.</span></span> <span data-ttu-id="da70a-130">For more information on configuring cross VNet connectivity, see  [Configure VNet to VNet Connectivity](../../../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).</span><span class="sxs-lookup"><span data-stu-id="da70a-130">For more information on configuring cross VNet connectivity, see  [Configure VNet to VNet Connectivity](../../../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).</span></span>

1. <span data-ttu-id="da70a-131">In the Azure portal, navigate to each VM hosting a replica and view the details.</span><span class="sxs-lookup"><span data-stu-id="da70a-131">In the Azure portal, navigate to each VM hosting a replica and view the details.</span></span>
2. <span data-ttu-id="da70a-132">Click the **Endpoints** tab for each of the VMs.</span><span class="sxs-lookup"><span data-stu-id="da70a-132">Click the **Endpoints** tab for each of the VMs.</span></span>
3. <span data-ttu-id="da70a-133">Verify that the **Name** and **Public Port** of the listener endpoint you want to use is not already in use.</span><span class="sxs-lookup"><span data-stu-id="da70a-133">Verify that the **Name** and **Public Port** of the listener endpoint you want to use is not already in use.</span></span> <span data-ttu-id="da70a-134">In the example below, the name is “MyEndpoint” and the port is “1433”.</span><span class="sxs-lookup"><span data-stu-id="da70a-134">In the example below, the name is “MyEndpoint” and the port is “1433”.</span></span>
4. <span data-ttu-id="da70a-135">On your local client, download and install [the latest PowerShell module](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="da70a-135">On your local client, download and install [the latest PowerShell module](https://azure.microsoft.com/downloads/).</span></span>
5. <span data-ttu-id="da70a-136">Launch **Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="da70a-136">Launch **Azure PowerShell**.</span></span> <span data-ttu-id="da70a-137">A new PowerShell session is opened with the Azure administrative modules loaded.</span><span class="sxs-lookup"><span data-stu-id="da70a-137">A new PowerShell session is opened with the Azure administrative modules loaded.</span></span>
6. <span data-ttu-id="da70a-138">Run **Get-AzurePublishSettingsFile**.</span><span class="sxs-lookup"><span data-stu-id="da70a-138">Run **Get-AzurePublishSettingsFile**.</span></span> <span data-ttu-id="da70a-139">This cmdlet directs you to a browser to download a publish settings file to a local directory.</span><span class="sxs-lookup"><span data-stu-id="da70a-139">This cmdlet directs you to a browser to download a publish settings file to a local directory.</span></span> <span data-ttu-id="da70a-140">You may be prompted for your log-in credentials for your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="da70a-140">You may be prompted for your log-in credentials for your Azure subscription.</span></span>
7. <span data-ttu-id="da70a-141">Run the **Import-AzurePublishSettingsFile** command with the path of the publish settings file that you downloaded:</span><span class="sxs-lookup"><span data-stu-id="da70a-141">Run the **Import-AzurePublishSettingsFile** command with the path of the publish settings file that you downloaded:</span></span>
   
        Import-AzurePublishSettingsFile -PublishSettingsFile <PublishSettingsFilePath>
   
    <span data-ttu-id="da70a-142">Once the publish settings file is imported, you can manage your Azure subscription in the PowerShell session.</span><span class="sxs-lookup"><span data-stu-id="da70a-142">Once the publish settings file is imported, you can manage your Azure subscription in the PowerShell session.</span></span>
    
1. <span data-ttu-id="da70a-143">For **ILB**, you should assign a static IP address.</span><span class="sxs-lookup"><span data-stu-id="da70a-143">For **ILB**, you should assign a static IP address.</span></span> <span data-ttu-id="da70a-144">First, examine the current VNet configuration by running the following command:</span><span class="sxs-lookup"><span data-stu-id="da70a-144">First, examine the current VNet configuration by running the following command:</span></span>
   
        (Get-AzureVNetConfig).XMLConfiguration
2. <span data-ttu-id="da70a-145">Note the **Subnet** name for the subnet that contains the VMs that host the replicas.</span><span class="sxs-lookup"><span data-stu-id="da70a-145">Note the **Subnet** name for the subnet that contains the VMs that host the replicas.</span></span> <span data-ttu-id="da70a-146">This will be used in the **$SubnetName** parameter in the script.</span><span class="sxs-lookup"><span data-stu-id="da70a-146">This will be used in the **$SubnetName** parameter in the script.</span></span>
3. <span data-ttu-id="da70a-147">Then note the **VirtualNetworkSite** name and the starting **AddressPrefix** for the subnet that contains the VMs that host the replicas.</span><span class="sxs-lookup"><span data-stu-id="da70a-147">Then note the **VirtualNetworkSite** name and the starting **AddressPrefix** for the subnet that contains the VMs that host the replicas.</span></span> <span data-ttu-id="da70a-148">Look for an available IP Address by passing both values to the **Test-AzureStaticVNetIP** command and examining the **AvailableAddresses**.</span><span class="sxs-lookup"><span data-stu-id="da70a-148">Look for an available IP Address by passing both values to the **Test-AzureStaticVNetIP** command and examining the **AvailableAddresses**.</span></span> <span data-ttu-id="da70a-149">For example, if the VNet was named *MyVNet* and had a subnet address range that started at *172.16.0.128*, the following command would list available addresses:</span><span class="sxs-lookup"><span data-stu-id="da70a-149">For example, if the VNet was named *MyVNet* and had a subnet address range that started at *172.16.0.128*, the following command would list available addresses:</span></span>
   
        (Test-AzureStaticVNetIP -VNetName "MyVNet"-IPAddress 172.16.0.128).AvailableAddresses
4. <span data-ttu-id="da70a-150">Choose one of the available addresses and use it in the **$ILBStaticIP** parameter of the following script.</span><span class="sxs-lookup"><span data-stu-id="da70a-150">Choose one of the available addresses and use it in the **$ILBStaticIP** parameter of the following script.</span></span>
5. <span data-ttu-id="da70a-151">Copy the PowerShell script below into a text editor and set the variable values to suit your environment (note that defaults have been provided for some parameters).</span><span class="sxs-lookup"><span data-stu-id="da70a-151">Copy the PowerShell script below into a text editor and set the variable values to suit your environment (note that defaults have been provided for some parameters).</span></span> <span data-ttu-id="da70a-152">Note that existing deployments that use affinity groups cannot add ILB.</span><span class="sxs-lookup"><span data-stu-id="da70a-152">Note that existing deployments that use affinity groups cannot add ILB.</span></span> <span data-ttu-id="da70a-153">For more information on ILB requirements, see [Internal Load Balancer](../../../load-balancer/load-balancer-internal-overview.md).</span><span class="sxs-lookup"><span data-stu-id="da70a-153">For more information on ILB requirements, see [Internal Load Balancer](../../../load-balancer/load-balancer-internal-overview.md).</span></span> <span data-ttu-id="da70a-154">Also, if your availability group spans Azure regions, you must run the script once in each datacenter for the cloud service and nodes that reside in that datacenter.</span><span class="sxs-lookup"><span data-stu-id="da70a-154">Also, if your availability group spans Azure regions, you must run the script once in each datacenter for the cloud service and nodes that reside in that datacenter.</span></span>
   
        # Define variables
        $ServiceName = "<MyCloudService>" # the name of the cloud service that contains the availability group nodes
        $AGNodes = "<VM1>","<VM2>","<VM3>" # all availability group nodes containing replicas in the same cloud service, separated by commas
        $SubnetName = "<MySubnetName>" # subnet name that the replicas use in the VNet
        $ILBStaticIP = "<MyILBStaticIPAddress>" # static IP address for the ILB in the subnet
        $ILBName = "AGListenerLB" # customize the ILB name or use this default value
   
        # Create the ILB
        Add-AzureInternalLoadBalancer -InternalLoadBalancerName $ILBName -SubnetName $SubnetName -ServiceName $ServiceName -StaticVNetIPAddress $ILBStaticIP
   
        # Configure a load balanced endpoint for each node in $AGNodes using ILB
        ForEach ($node in $AGNodes)
        {
            Get-AzureVM -ServiceName $ServiceName -Name $node | Add-AzureEndpoint -Name "ListenerEndpoint" -LBSetName "ListenerEndpointLB" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -InternalLoadBalancerName $ILBName -DirectServerReturn $true | Update-AzureVM
        }
6. <span data-ttu-id="da70a-155">Once you have set the variables, copy the script from the text editor into your Azure PowerShell session to run it.</span><span class="sxs-lookup"><span data-stu-id="da70a-155">Once you have set the variables, copy the script from the text editor into your Azure PowerShell session to run it.</span></span> <span data-ttu-id="da70a-156">If the prompt still shows >>, type ENTER again to make sure the script starts running.Note</span><span class="sxs-lookup"><span data-stu-id="da70a-156">If the prompt still shows >>, type ENTER again to make sure the script starts running.Note</span></span>

> [!NOTE]
> The Azure classic portal does not support the Internal Load Balancer at this time, so you will not see either the ILB or the endpoints in the Azure classic portal. However, **Get-AzureEndpoint** returns an internal IP address if the Load Balancer is running on it. Otherwise, it returns null.
> 
> 

## <a name="verify-that-kb2854082-is-installed-if-necessary"></a><span data-ttu-id="da70a-160">Verify that KB2854082 is installed if necessary</span><span class="sxs-lookup"><span data-stu-id="da70a-160">Verify that KB2854082 is installed if necessary</span></span>
[!INCLUDE [kb2854082](../../../../includes/virtual-machines-ag-listener-kb2854082.md)]

## <a name="open-the-firewall-ports-in-availability-group-nodes"></a><span data-ttu-id="da70a-161">Open the firewall ports in availability group nodes</span><span class="sxs-lookup"><span data-stu-id="da70a-161">Open the firewall ports in availability group nodes</span></span>
[!INCLUDE [firewall](../../../../includes/virtual-machines-ag-listener-open-firewall.md)]

## <a name="create-the-availability-group-listener"></a><span data-ttu-id="da70a-162">Create the availability group listener</span><span class="sxs-lookup"><span data-stu-id="da70a-162">Create the availability group listener</span></span>

<span data-ttu-id="da70a-163">Create the availability group listener in two steps.</span><span class="sxs-lookup"><span data-stu-id="da70a-163">Create the availability group listener in two steps.</span></span> <span data-ttu-id="da70a-164">First, create the client access point cluster resource and configure  dependencies.</span><span class="sxs-lookup"><span data-stu-id="da70a-164">First, create the client access point cluster resource and configure  dependencies.</span></span> <span data-ttu-id="da70a-165">Second, configure the cluster resources with PowerShell.</span><span class="sxs-lookup"><span data-stu-id="da70a-165">Second, configure the cluster resources with PowerShell.</span></span>

### <a name="create-the-client-access-point-and-configure-the-cluster-dependencies"></a><span data-ttu-id="da70a-166">Create the client access point and configure the cluster dependencies</span><span class="sxs-lookup"><span data-stu-id="da70a-166">Create the client access point and configure the cluster dependencies</span></span>
[!INCLUDE [firewall](../../../../includes/virtual-machines-ag-listener-create-listener.md)]

### <a name="configure-the-cluster-resources-in-powershell"></a><span data-ttu-id="da70a-167">Configure the cluster resources in PowerShell</span><span class="sxs-lookup"><span data-stu-id="da70a-167">Configure the cluster resources in PowerShell</span></span>
1. <span data-ttu-id="da70a-168">For ILB, you must use the IP address of the Internal Load Balancer (ILB) created earlier.</span><span class="sxs-lookup"><span data-stu-id="da70a-168">For ILB, you must use the IP address of the Internal Load Balancer (ILB) created earlier.</span></span> <span data-ttu-id="da70a-169">Use the following script to obtain this IP Address in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="da70a-169">Use the following script to obtain this IP Address in PowerShell.</span></span>
   
        # Define variables
        $ServiceName="<MyServiceName>" # the name of the cloud service that contains the AG nodes
        (Get-AzureInternalLoadBalancer -ServiceName $ServiceName).IPAddress
2. <span data-ttu-id="da70a-170">On one of the VMs, copy the PowerShell script for your operating system into a text editor and set the variables to the values you noted earlier.</span><span class="sxs-lookup"><span data-stu-id="da70a-170">On one of the VMs, copy the PowerShell script for your operating system into a text editor and set the variables to the values you noted earlier.</span></span>
   
    <span data-ttu-id="da70a-171">For Windows Server 2012 or higher use the following script:</span><span class="sxs-lookup"><span data-stu-id="da70a-171">For Windows Server 2012 or higher use the following script:</span></span>
   
        # Define variables
        $ClusterNetworkName = "<MyClusterNetworkName>" # the cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher to find the name)
        $IPResourceName = "<IPResourceName>" # the IP Address resource name
        $ILBIP = “<X.X.X.X>” # the IP Address of the Internal Load Balancer (ILB)
   
        Import-Module FailoverClusters
   
        Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"="59999";"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
   
    <span data-ttu-id="da70a-172">For Windows Server 2008 R2 use the following script:</span><span class="sxs-lookup"><span data-stu-id="da70a-172">For Windows Server 2008 R2 use the following script:</span></span>
   
        # Define variables
        $ClusterNetworkName = "<MyClusterNetworkName>" # the cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher to find the name)
        $IPResourceName = "<IPResourceName>" # the IP Address resource name
        $ILBIP = “<X.X.X.X>” # the IP Address of the Internal Load Balancer (ILB)
   
        Import-Module FailoverClusters
   
        cluster res $IPResourceName /priv enabledhcp=0 address=$ILBIP probeport=59999  subnetmask=255.255.255.255
3. <span data-ttu-id="da70a-173">Once you have set the variables, open an elevated Windows PowerShell window, then copy the script from the text editor and paste into your Azure PowerShell session to run it.</span><span class="sxs-lookup"><span data-stu-id="da70a-173">Once you have set the variables, open an elevated Windows PowerShell window, then copy the script from the text editor and paste into your Azure PowerShell session to run it.</span></span> <span data-ttu-id="da70a-174">If the prompt still shows >>, type ENTER again to make sure the script starts running.</span><span class="sxs-lookup"><span data-stu-id="da70a-174">If the prompt still shows >>, type ENTER again to make sure the script starts running.</span></span>
4. <span data-ttu-id="da70a-175">Repeat this on each VM.</span><span class="sxs-lookup"><span data-stu-id="da70a-175">Repeat this on each VM.</span></span> <span data-ttu-id="da70a-176">This script configures the IP Address resource with the IP address of the cloud service and sets other parameters like the probe port.</span><span class="sxs-lookup"><span data-stu-id="da70a-176">This script configures the IP Address resource with the IP address of the cloud service and sets other parameters like the probe port.</span></span> <span data-ttu-id="da70a-177">When the IP Address resource is brought online, it can then respond to the polling on the probe port from the load-balanced endpoint created earlier in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="da70a-177">When the IP Address resource is brought online, it can then respond to the polling on the probe port from the load-balanced endpoint created earlier in this tutorial.</span></span>

## <a name="bring-the-listener-online"></a><span data-ttu-id="da70a-178">Bring the listener online</span><span class="sxs-lookup"><span data-stu-id="da70a-178">Bring the listener online</span></span>
[!INCLUDE [Bring-Listener-Online](../../../../includes/virtual-machines-ag-listener-bring-online.md)]

## <a name="follow-up-items"></a><span data-ttu-id="da70a-179">Follow-up items</span><span class="sxs-lookup"><span data-stu-id="da70a-179">Follow-up items</span></span>
[!INCLUDE [Follow-up](../../../../includes/virtual-machines-ag-listener-follow-up.md)]

## <a name="test-the-availability-group-listener-within-the-same-vnet"></a><span data-ttu-id="da70a-180">Test the availability group listener (within the same VNet)</span><span class="sxs-lookup"><span data-stu-id="da70a-180">Test the availability group listener (within the same VNet)</span></span>
[!INCLUDE [Test-Listener-Within-VNET](../../../../includes/virtual-machines-ag-listener-test.md)]

## <a name="next-steps"></a><span data-ttu-id="da70a-181">Next steps</span><span class="sxs-lookup"><span data-stu-id="da70a-181">Next steps</span></span>
[!INCLUDE [Listener-Next-Steps](../../../../includes/virtual-machines-ag-listener-next-steps.md)]

