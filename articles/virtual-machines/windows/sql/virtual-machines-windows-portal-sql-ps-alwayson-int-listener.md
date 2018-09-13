---
title: Configure Always On Availability Group Listeners – Microsoft Azure | Microsoft Docs
description: Configure Availability Group Listeners on the Azure Resource Manager model, using an internal load balancer with one or more IP addresses.
services: virtual-machines
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: monicar
ms.assetid: 14b39cde-311c-4ddf-98f3-8694e01a7d3b
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 12/28/2016
ms.author: mikeray
ms.openlocfilehash: 1430807db46326779866f57bca3982e5f9448951
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563848"
---
# <a name="configure-one-or-more-always-on-availability-group-listeners---resource-manager"></a><span data-ttu-id="b759d-103">Configure one or more Always On Availability Group Listeners - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b759d-103">Configure one or more Always On Availability Group Listeners - Resource Manager</span></span>
<span data-ttu-id="b759d-104">This topic shows how to:</span><span class="sxs-lookup"><span data-stu-id="b759d-104">This topic shows how to:</span></span>

* <span data-ttu-id="b759d-105">Create an internal load balancer for SQL Server availability groups using PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="b759d-105">Create an internal load balancer for SQL Server availability groups using PowerShell cmdlets.</span></span>
* <span data-ttu-id="b759d-106">Add additional IP addresses to a load balancer for more than one availability group.</span><span class="sxs-lookup"><span data-stu-id="b759d-106">Add additional IP addresses to a load balancer for more than one availability group.</span></span> 

<span data-ttu-id="b759d-107">An availability group listener is a virtual network name that clients connect to for database access.</span><span class="sxs-lookup"><span data-stu-id="b759d-107">An availability group listener is a virtual network name that clients connect to for database access.</span></span> <span data-ttu-id="b759d-108">On Azure virtual machines, a load balancer holds the IP address for the listener.</span><span class="sxs-lookup"><span data-stu-id="b759d-108">On Azure virtual machines, a load balancer holds the IP address for the listener.</span></span> <span data-ttu-id="b759d-109">The load balancer routes traffic to the instance of SQL Server that is listening on the probe port.</span><span class="sxs-lookup"><span data-stu-id="b759d-109">The load balancer routes traffic to the instance of SQL Server that is listening on the probe port.</span></span> <span data-ttu-id="b759d-110">Usually, an availability group uses an internal load balancer.</span><span class="sxs-lookup"><span data-stu-id="b759d-110">Usually, an availability group uses an internal load balancer.</span></span> <span data-ttu-id="b759d-111">An Azure internal load balancer can host one or many IP addresses.</span><span class="sxs-lookup"><span data-stu-id="b759d-111">An Azure internal load balancer can host one or many IP addresses.</span></span> <span data-ttu-id="b759d-112">Each IP address uses a specific probe port.</span><span class="sxs-lookup"><span data-stu-id="b759d-112">Each IP address uses a specific probe port.</span></span> <span data-ttu-id="b759d-113">This document shows how to use PowerShell to create a load balancer, or add IP addresses to an existing load balancer for SQL Server availability groups.</span><span class="sxs-lookup"><span data-stu-id="b759d-113">This document shows how to use PowerShell to create a load balancer, or add IP addresses to an existing load balancer for SQL Server availability groups.</span></span> 

<span data-ttu-id="b759d-114">The ability to assign multiple IP addresses to an internal load balancer is new to Azure and is only available in Resource Manager model.</span><span class="sxs-lookup"><span data-stu-id="b759d-114">The ability to assign multiple IP addresses to an internal load balancer is new to Azure and is only available in Resource Manager model.</span></span> <span data-ttu-id="b759d-115">To complete this task, you need to have a SQL Server availability group deployed on Azure virtual machines in Resource Manager model.</span><span class="sxs-lookup"><span data-stu-id="b759d-115">To complete this task, you need to have a SQL Server availability group deployed on Azure virtual machines in Resource Manager model.</span></span> <span data-ttu-id="b759d-116">Both SQL Server virtual machines must belong to the same availability set.</span><span class="sxs-lookup"><span data-stu-id="b759d-116">Both SQL Server virtual machines must belong to the same availability set.</span></span> <span data-ttu-id="b759d-117">You can use the [Microsoft template](virtual-machines-windows-portal-sql-alwayson-availability-groups.md) to automatically create the availability group in Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b759d-117">You can use the [Microsoft template](virtual-machines-windows-portal-sql-alwayson-availability-groups.md) to automatically create the availability group in Azure Resource Manager.</span></span> <span data-ttu-id="b759d-118">This template automatically creates the availability group, including the internal load balancer for you.</span><span class="sxs-lookup"><span data-stu-id="b759d-118">This template automatically creates the availability group, including the internal load balancer for you.</span></span> <span data-ttu-id="b759d-119">If you prefer, you can [manually configure an AlwaysOn availability group](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).</span><span class="sxs-lookup"><span data-stu-id="b759d-119">If you prefer, you can [manually configure an AlwaysOn availability group](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).</span></span>

<span data-ttu-id="b759d-120">This topic requires that your availability groups are already configured.</span><span class="sxs-lookup"><span data-stu-id="b759d-120">This topic requires that your availability groups are already configured.</span></span>  

<span data-ttu-id="b759d-121">Related topics include:</span><span class="sxs-lookup"><span data-stu-id="b759d-121">Related topics include:</span></span>

* [<span data-ttu-id="b759d-122">Configure AlwaysOn Availability Groups in Azure VM (GUI)</span><span class="sxs-lookup"><span data-stu-id="b759d-122">Configure AlwaysOn Availability Groups in Azure VM (GUI)</span></span>](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md)   
* [<span data-ttu-id="b759d-123">Configure a VNet-to-VNet connection by using Azure Resource Manager and PowerShell</span><span class="sxs-lookup"><span data-stu-id="b759d-123">Configure a VNet-to-VNet connection by using Azure Resource Manager and PowerShell</span></span>](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md)

[!INCLUDE [Start your PowerShell session](../../../../includes/sql-vm-powershell.md)]

## <a name="configure-the-windows-firewall"></a><span data-ttu-id="b759d-124">Configure the Windows Firewall</span><span class="sxs-lookup"><span data-stu-id="b759d-124">Configure the Windows Firewall</span></span>
<span data-ttu-id="b759d-125">Configure the Windows Firewall to allow SQL Server access.</span><span class="sxs-lookup"><span data-stu-id="b759d-125">Configure the Windows Firewall to allow SQL Server access.</span></span> <span data-ttu-id="b759d-126">The firewall rules allow TCP connections to the ports use by the SQL Server instance, and the listener probe.</span><span class="sxs-lookup"><span data-stu-id="b759d-126">The firewall rules allow TCP connections to the ports use by the SQL Server instance, and the listener probe.</span></span> <span data-ttu-id="b759d-127">For detailed instructions, see [Configure a Windows Firewall for Database Engine Access](http://msdn.microsoft.com/library/ms175043.aspx#Anchor_1).</span><span class="sxs-lookup"><span data-stu-id="b759d-127">For detailed instructions, see [Configure a Windows Firewall for Database Engine Access](http://msdn.microsoft.com/library/ms175043.aspx#Anchor_1).</span></span> <span data-ttu-id="b759d-128">Create an inbound rule for the SQL Server port and for the probe port.</span><span class="sxs-lookup"><span data-stu-id="b759d-128">Create an inbound rule for the SQL Server port and for the probe port.</span></span>

## <a name="example-script-create-an-internal-load-balancer-with-powershell"></a><span data-ttu-id="b759d-129">Example Script: Create an internal load balancer with PowerShell</span><span class="sxs-lookup"><span data-stu-id="b759d-129">Example Script: Create an internal load balancer with PowerShell</span></span>
> [!NOTE]
> <span data-ttu-id="b759d-130">If you created your availability group with the [Microsoft template](virtual-machines-windows-portal-sql-alwayson-availability-groups.md), the internal load balancer was already created.</span><span class="sxs-lookup"><span data-stu-id="b759d-130">If you created your availability group with the [Microsoft template](virtual-machines-windows-portal-sql-alwayson-availability-groups.md), the internal load balancer was already created.</span></span> 
> 
> 

<span data-ttu-id="b759d-131">The following PowerShell script creates an internal load balancer, configures the load balancing rules, and sets an IP address for the load balancer.</span><span class="sxs-lookup"><span data-stu-id="b759d-131">The following PowerShell script creates an internal load balancer, configures the load balancing rules, and sets an IP address for the load balancer.</span></span> <span data-ttu-id="b759d-132">To run the script, open Windows PowerShell ISE, and paste the script in the Script pane.</span><span class="sxs-lookup"><span data-stu-id="b759d-132">To run the script, open Windows PowerShell ISE, and paste the script in the Script pane.</span></span> <span data-ttu-id="b759d-133">Use `Login-AzureRMAccount` to log in to PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b759d-133">Use `Login-AzureRMAccount` to log in to PowerShell.</span></span> <span data-ttu-id="b759d-134">If you have multiple Azure subscriptions, use `Select-AzureRmSubscription ` to set the subscription.</span><span class="sxs-lookup"><span data-stu-id="b759d-134">If you have multiple Azure subscriptions, use `Select-AzureRmSubscription ` to set the subscription.</span></span> 

```powershell
# Login-AzureRmAccount
# Select-AzureRmSubscription -SubscriptionId <xxxxxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx>

$ResourceGroupName = "<Resource Group Name>" # Resource group name
$VNetName = "<Virtual Network Name>"         # Virtual network name
$SubnetName = "<Subnet Name>"                # Subnet name
$ILBName = "<Load Balancer Name>"            # ILB name
$Location = "<Azure Region>"                 # Azure location
$VMNames = "<VM1>","<VM2>"                   # Virtual machine names

$ILBIP = "<n.n.n.n>"                         # IP address
[int]$ListenerPort = "<nnnn>"                # AG listener port
[int]$ProbePort = "<nnnn>"                   # Probe port

$LBProbeName ="ILBPROBE_$ListenerPort"       # The Load balancer Probe Object Name              
$LBConfigRuleName = "ILBCR_$ListenerPort"    # The Load Balancer Rule Object Name

$FrontEndConfigurationName = "FE_SQLAGILB_1" # Object name for the front-end configuration 
$BackEndConfigurationName ="BE_SQLAGILB_1"   # Object name for the back-end configuration

$VNet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName 

$Subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $VNet -Name $SubnetName 

$FEConfig = New-AzureRMLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -PrivateIpAddress $ILBIP -SubnetId $Subnet.id

$BEConfig = New-AzureRMLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName 

$SQLHealthProbe = New-AzureRmLoadBalancerProbeConfig -Name $LBProbeName -Protocol tcp -Port $ProbePort -IntervalInSeconds 15 -ProbeCount 2

$ILBRule = New-AzureRmLoadBalancerRuleConfig -Name $LBConfigRuleName -FrontendIpConfiguration $FEConfig -BackendAddressPool $BEConfig -Probe $SQLHealthProbe -Protocol tcp -FrontendPort $ListenerPort -BackendPort $ListenerPort -LoadDistribution Default -EnableFloatingIP 

$ILB= New-AzureRmLoadBalancer -Location $Location -Name $ILBName -ResourceGroupName $ResourceGroupName -FrontendIpConfiguration $FEConfig -BackendAddressPool $BEConfig -LoadBalancingRule $ILBRule -Probe $SQLHealthProbe 

$bepool = Get-AzureRmLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName -LoadBalancer $ILB 

foreach($VMName in $VMNames)
    {
        $VM = Get-AzureRmVM -ResourceGroupName $ResourceGroupName -Name $VMName 
        $NICName = ($VM.NetworkInterfaceIDs[0].Split('/') | select -last 1)
        $NIC = Get-AzureRmNetworkInterface -name $NICName -ResourceGroupName $ResourceGroupName
        $NIC.IpConfigurations[0].LoadBalancerBackendAddressPools = $BEPool
        Set-AzureRmNetworkInterface -NetworkInterface $NIC
        start-AzureRmVM -ResourceGroupName $ResourceGroupName -Name $VM.Name 
    }
```

## <a name="Add-IP"></a> <span data-ttu-id="b759d-135">Example script: Add an IP address to an existing load balancer with PowerShell</span><span class="sxs-lookup"><span data-stu-id="b759d-135">Example script: Add an IP address to an existing load balancer with PowerShell</span></span>
<span data-ttu-id="b759d-136">To use more than one availability group, add an additional IP address to the load balancer.</span><span class="sxs-lookup"><span data-stu-id="b759d-136">To use more than one availability group, add an additional IP address to the load balancer.</span></span> <span data-ttu-id="b759d-137">Each IP address requires its own load balancing rule, probe port, and front port.</span><span class="sxs-lookup"><span data-stu-id="b759d-137">Each IP address requires its own load balancing rule, probe port, and front port.</span></span>

<span data-ttu-id="b759d-138">The front-end port is the port that applications use to connect to the SQL Server instance.</span><span class="sxs-lookup"><span data-stu-id="b759d-138">The front-end port is the port that applications use to connect to the SQL Server instance.</span></span> <span data-ttu-id="b759d-139">IP addresses for different availability groups can use the same front-end port.</span><span class="sxs-lookup"><span data-stu-id="b759d-139">IP addresses for different availability groups can use the same front-end port.</span></span>

> [!NOTE]
> <span data-ttu-id="b759d-140">For SQL Server availability groups, each IP address requires a specific probe port.</span><span class="sxs-lookup"><span data-stu-id="b759d-140">For SQL Server availability groups, each IP address requires a specific probe port.</span></span> <span data-ttu-id="b759d-141">For example, if one IP address on a load balancer uses probe port 59999, no other IP addresses on that load balancer can use probe port 59999.</span><span class="sxs-lookup"><span data-stu-id="b759d-141">For example, if one IP address on a load balancer uses probe port 59999, no other IP addresses on that load balancer can use probe port 59999.</span></span>

* <span data-ttu-id="b759d-142">For information about load balancer limits, see **Private front end IP per load balancer** under [Networking Limits - Azure Resource Manager](../../../azure-subscription-service-limits.md#azure-resource-manager-virtual-networking-limits).</span><span class="sxs-lookup"><span data-stu-id="b759d-142">For information about load balancer limits, see **Private front end IP per load balancer** under [Networking Limits - Azure Resource Manager](../../../azure-subscription-service-limits.md#azure-resource-manager-virtual-networking-limits).</span></span>
* <span data-ttu-id="b759d-143">For information about availability group limits, see [Restrictions (Availability Groups)](http://msdn.microsoft.com/library/ff878487.aspx#RestrictionsAG).</span><span class="sxs-lookup"><span data-stu-id="b759d-143">For information about availability group limits, see [Restrictions (Availability Groups)](http://msdn.microsoft.com/library/ff878487.aspx#RestrictionsAG).</span></span>

<span data-ttu-id="b759d-144">The following script adds a new IP address to an existing load balancer.</span><span class="sxs-lookup"><span data-stu-id="b759d-144">The following script adds a new IP address to an existing load balancer.</span></span> <span data-ttu-id="b759d-145">The ILB uses the listener port for the load balancing front-end port.</span><span class="sxs-lookup"><span data-stu-id="b759d-145">The ILB uses the listener port for the load balancing front-end port.</span></span> <span data-ttu-id="b759d-146">This port can be the port that SQL Server is listening on.</span><span class="sxs-lookup"><span data-stu-id="b759d-146">This port can be the port that SQL Server is listening on.</span></span> <span data-ttu-id="b759d-147">For default instances of SQL Server, the port is 1433.</span><span class="sxs-lookup"><span data-stu-id="b759d-147">For default instances of SQL Server, the port is 1433.</span></span> <span data-ttu-id="b759d-148">The load balancing rule for an availability group requires a floating IP (direct server return) so the back-end port is the same as the front-end port.</span><span class="sxs-lookup"><span data-stu-id="b759d-148">The load balancing rule for an availability group requires a floating IP (direct server return) so the back-end port is the same as the front-end port.</span></span> <span data-ttu-id="b759d-149">Update the variables for your environment.</span><span class="sxs-lookup"><span data-stu-id="b759d-149">Update the variables for your environment.</span></span> 

```powershell
# Login-AzureRmAccount
# Select-AzureRmSubscription -SubscriptionId <xxxxxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx>

$ResourceGroupName = "<ResourceGroup>"          # Resource group name
$VNetName = "<VirtualNetwork>"                  # Virtual network name
$SubnetName = "<Subnet>"                        # Subnet name
$ILBName = "<ILBName>"                          # ILB name                      

$ILBIP = "<n.n.n.n>"                            # IP address
[int]$ListenerPort = "<nnnn>"                   # AG listener port
[int]$ProbePort = "<nnnnn>"                     # Probe port 

$ILB = Get-AzureRmLoadBalancer -Name $ILBName -ResourceGroupName $ResourceGroupName 

$count = $ILB.FrontendIpConfigurations.Count+1
$FrontEndConfigurationName ="FE_SQLAGILB_$count"  

$LBProbeName = "ILBPROBE_$count"
$LBConfigrulename = "ILBCR_$count"

$VNet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName 
$Subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $VNet -Name $SubnetName

$ILB | Add-AzureRmLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -PrivateIpAddress $ILBIP -SubnetId $Subnet.Id 

$ILB | Add-AzureRmLoadBalancerProbeConfig -Name $LBProbeName  -Protocol Tcp -Port $Probeport -ProbeCount 2 -IntervalInSeconds 15  | Set-AzureRmLoadBalancer 

$ILB = Get-AzureRmLoadBalancer -Name $ILBname -ResourceGroupName $ResourceGroupName

$FEConfig = get-AzureRMLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -LoadBalancer $ILB

$SQLHealthProbe  = Get-AzureRmLoadBalancerProbeConfig -Name $LBProbeName -LoadBalancer $ILB

$BEConfig = Get-AzureRmLoadBalancerBackendAddressPoolConfig -Name $ILB.BackendAddressPools[0].Name -LoadBalancer $ILB 

$ILB | Add-AzureRmLoadBalancerRuleConfig -Name $LBConfigRuleName -FrontendIpConfiguration $FEConfig  -BackendAddressPool $BEConfig -Probe $SQLHealthProbe -Protocol tcp -FrontendPort  $ListenerPort -BackendPort $ListenerPort -LoadDistribution Default -EnableFloatingIP | Set-AzureRmLoadBalancer   
```

## <a name="configure-the-listener"></a><span data-ttu-id="b759d-150">Configure the listener</span><span class="sxs-lookup"><span data-stu-id="b759d-150">Configure the listener</span></span>

[!INCLUDE [ag-listener-configure](../../../../includes/virtual-machines-ag-listener-configure.md)]


<!------------------------------- The content below is duplicated. Pointing to the link. Thinking about an include. 

## Configure the cluster to use the load balancer IP address
The next step is to configure the listener on the cluster, and bring the listener online. To accomplish this, do the following: 

1. Create the availability group listener on the failover cluster  
2. Bring the listener online

## Create the availability group listener on the failover cluster

The availability group listener is an IP address and network name that the SQL Server availability group listens on. To create the availability group listener, do the following steps:

1. [Get the name of the cluster network resource](#getnet).

1. [Add the client access point](#addcap).

1. [Configure the IP resource for the availability group](#congroup).

1. [Make the availability group resource dependent on the listener resource name](#listname).

1. [Set the cluster parameters in PowerShell](#setparam).

The following sections provide detailed instructions for each of these steps. 

### <a name="getnet">Get the name of the cluster network resource</a> 

1. Use RDP to connect to the Azure virtual machine that hosts the primary replica. 

1. Open Failover Cluster Manager.

1. Select the **Networks** node, and note the cluster network name. Use this name in the `$ClusterNetworkName` variable in the PowerShell script.

### <a name="addcap">Add the client access point</a>

1. Expand the cluster name, and then click **Roles**.

1. In the **Roles** pane, right-click the availability group name and then select **Add Resource** > **Client Access Point**.

1. In the **Name** box, create a name for this new listener. 

   The name for the new listener is the network name that applications will use to connect to databases in the SQL Server availability group.
   
   To finish creating the listener, click **Next** twice, and then click **Finish**. Do not bring the listener or resource online at this point.
   
### <a name="congroup">Configure the IP resource for the availability group</a>

1. Click the **Resources** tab, then expand the Client Access Point you just created. Right-click the IP resource and click properties. Note the name of the IP address. You will use this name in the `$IPResourceName` variable in the PowerShell script.

1. Under **IP Address** click **Static IP Address** and set the static IP address to the same address that you used when you set the load balancer IP address on the Azure portal. 

1. Disable NetBIOS for this address and click **OK**. Repeat this step for each IP resource if your solution spans multiple Azure VNets. 

### <a name="listname">Make the availability group resource dependent on the listener resource</a>

1. In Failover Cluster Manager click **Roles** and click your Availability Group. 

1. On the **Resources** tab, right-click the availability resource group and click **Properties**. 

1. Click the **Dependencies** tab. Set a dependency on the listener resource name. If there are multiple resources listed, verify that the IP addresses have OR, not AND, dependencies. Click **OK**. 

1. Right-click the listener name and click **Bring Online**. 

### <a name="setparam">Set the cluster parameters in PowerShell</a>

Set the cluster parameters. To do this, update the following PowerShell script. Set the variables with the values for your environment. Run the PowerShell script on one of the cluster nodes.  
    
   ```PowerShell
   $ClusterNetworkName = "<MyClusterNetworkName>" # the cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher to find the name)
   $IPResourceName = "<IPResourceName>" # the IP Address resource name
   $ILBIP = “<n.n.n.n>” # the IP Address of the Internal Load Balancer (ILB). This is the static IP address for the load balancer you configured in the Azure portal.
   [int]$ProbePort = <nnnnn>

   Import-Module FailoverClusters

   Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
   ```
> [!NOTE]
> If your SQL Servers are in separate regions, you need to run the PowerShell script twice. The first time use the `$ILBIP` and `$ProbePort` from the first region. The second time, use the `$ILBIP` and `$ProbePort` from the second region. The cluster network name, and the cluster IP resource name are the same. 

## Set the listener port in SQL Server Management Studio

1. Launch SQL Server Management Studio and connect to the primary replica.

1. Navigate to **AlwaysOn High Availability** | **Availability Groups** | **Availability Group Listeners**. 

1. You should now see the listener name that you created in Failover Cluster Manager. Right-click the listener name and click **Properties**.

1. In the **Port** box, specify the port number for the availability group listener by using the $EndpointPort you used earlier (1433 was the default), then click **OK**.

You now have a SQL Server availability group in Azure virtual machines running in Resource Manager mode. 
-------------------------------->

## <a name="set-the-listener-port-in-sql-server-management-studio"></a><span data-ttu-id="b759d-151">Set the listener port in SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="b759d-151">Set the listener port in SQL Server Management Studio</span></span>

1. <span data-ttu-id="b759d-152">Launch SQL Server Management Studio and connect to the primary replica.</span><span class="sxs-lookup"><span data-stu-id="b759d-152">Launch SQL Server Management Studio and connect to the primary replica.</span></span>

1. <span data-ttu-id="b759d-153">Navigate to **AlwaysOn High Availability** | **Availability Groups** | **Availability Group Listeners**.</span><span class="sxs-lookup"><span data-stu-id="b759d-153">Navigate to **AlwaysOn High Availability** | **Availability Groups** | **Availability Group Listeners**.</span></span> 

1. <span data-ttu-id="b759d-154">You should now see the listener name that you created in Failover Cluster Manager.</span><span class="sxs-lookup"><span data-stu-id="b759d-154">You should now see the listener name that you created in Failover Cluster Manager.</span></span> <span data-ttu-id="b759d-155">Right-click the listener name and click **Properties**.</span><span class="sxs-lookup"><span data-stu-id="b759d-155">Right-click the listener name and click **Properties**.</span></span>

1. <span data-ttu-id="b759d-156">In the **Port** box, specify the port number for the availability group listener by using the $EndpointPort you used earlier (1433 was the default), then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="b759d-156">In the **Port** box, specify the port number for the availability group listener by using the $EndpointPort you used earlier (1433 was the default), then click **OK**.</span></span>

## <a name="test-the-connection-to-the-listener"></a><span data-ttu-id="b759d-157">Test the connection to the listener</span><span class="sxs-lookup"><span data-stu-id="b759d-157">Test the connection to the listener</span></span>

<span data-ttu-id="b759d-158">To test the connection:</span><span class="sxs-lookup"><span data-stu-id="b759d-158">To test the connection:</span></span>

1. <span data-ttu-id="b759d-159">RDP to a SQL Server that is in the same virtual network, but does not own the replica.</span><span class="sxs-lookup"><span data-stu-id="b759d-159">RDP to a SQL Server that is in the same virtual network, but does not own the replica.</span></span> <span data-ttu-id="b759d-160">This can be the other SQL Server in the cluster.</span><span class="sxs-lookup"><span data-stu-id="b759d-160">This can be the other SQL Server in the cluster.</span></span>

1. <span data-ttu-id="b759d-161">Use **sqlcmd** utility to test the connection.</span><span class="sxs-lookup"><span data-stu-id="b759d-161">Use **sqlcmd** utility to test the connection.</span></span> <span data-ttu-id="b759d-162">For example, the following script establishes a **sqlcmd** connection to the primary replica through the listener with Windows authentication:</span><span class="sxs-lookup"><span data-stu-id="b759d-162">For example, the following script establishes a **sqlcmd** connection to the primary replica through the listener with Windows authentication:</span></span>
   
    ```
    sqlmd -S <listenerName> -E
    ```
   
    <span data-ttu-id="b759d-163">If the listener is using a port other than the default port (1433), specify the port in the connection string.</span><span class="sxs-lookup"><span data-stu-id="b759d-163">If the listener is using a port other than the default port (1433), specify the port in the connection string.</span></span> <span data-ttu-id="b759d-164">For example, the following sqlcmd command connects to a listener at port 1435:</span><span class="sxs-lookup"><span data-stu-id="b759d-164">For example, the following sqlcmd command connects to a listener at port 1435:</span></span> 
   
    ```
    sqlcmd -S <listenerName>,1435 -E
    ```

<span data-ttu-id="b759d-165">The SQLCMD connection automatically connects to whichever instance of SQL Server hosts the primary replica.</span><span class="sxs-lookup"><span data-stu-id="b759d-165">The SQLCMD connection automatically connects to whichever instance of SQL Server hosts the primary replica.</span></span> 

> [!NOTE]
> <span data-ttu-id="b759d-166">Make sure that the port you specify is open on the firewall of both SQL Servers.</span><span class="sxs-lookup"><span data-stu-id="b759d-166">Make sure that the port you specify is open on the firewall of both SQL Servers.</span></span> <span data-ttu-id="b759d-167">Both servers require an inbound rule for the TCP port that you use.</span><span class="sxs-lookup"><span data-stu-id="b759d-167">Both servers require an inbound rule for the TCP port that you use.</span></span> <span data-ttu-id="b759d-168">See [Add or Edit Firewall Rule](http://technet.microsoft.com/library/cc753558.aspx) for more information.</span><span class="sxs-lookup"><span data-stu-id="b759d-168">See [Add or Edit Firewall Rule](http://technet.microsoft.com/library/cc753558.aspx) for more information.</span></span> 
> 
> 

## <a name="guidelines-and-limitations"></a><span data-ttu-id="b759d-169">Guidelines and limitations</span><span class="sxs-lookup"><span data-stu-id="b759d-169">Guidelines and limitations</span></span>
<span data-ttu-id="b759d-170">Note the following guidelines on availability group listener in Azure using internal load balancer:</span><span class="sxs-lookup"><span data-stu-id="b759d-170">Note the following guidelines on availability group listener in Azure using internal load balancer:</span></span>

* <span data-ttu-id="b759d-171">With an internal load balancer, you only access the listener from within the same virtual network.</span><span class="sxs-lookup"><span data-stu-id="b759d-171">With an internal load balancer, you only access the listener from within the same virtual network.</span></span>


## <a name="for-more-information"></a><span data-ttu-id="b759d-172">For more information</span><span class="sxs-lookup"><span data-stu-id="b759d-172">For more information</span></span>
<span data-ttu-id="b759d-173">For more information, see [Configure Always On availability group in Azure VM manually](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).</span><span class="sxs-lookup"><span data-stu-id="b759d-173">For more information, see [Configure Always On availability group in Azure VM manually](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).</span></span>

## <a name="powershell-cmdlets"></a><span data-ttu-id="b759d-174">PowerShell cmdlets</span><span class="sxs-lookup"><span data-stu-id="b759d-174">PowerShell cmdlets</span></span>
<span data-ttu-id="b759d-175">Use the following PowerShell cmdlets to create an internal load balancer for Azure virtual machines.</span><span class="sxs-lookup"><span data-stu-id="b759d-175">Use the following PowerShell cmdlets to create an internal load balancer for Azure virtual machines.</span></span>

* <span data-ttu-id="b759d-176">[New-AzureRmLoadBalancer](http://msdn.microsoft.com/library/mt619450.aspx) creates a load balancer.</span><span class="sxs-lookup"><span data-stu-id="b759d-176">[New-AzureRmLoadBalancer](http://msdn.microsoft.com/library/mt619450.aspx) creates a load balancer.</span></span> 
* <span data-ttu-id="b759d-177">[New-AzureRMLoadBalancerFrontendIpConfig](http://msdn.microsoft.com/library/mt603510.aspx) creates a front-end IP configuration for a load balancer.</span><span class="sxs-lookup"><span data-stu-id="b759d-177">[New-AzureRMLoadBalancerFrontendIpConfig](http://msdn.microsoft.com/library/mt603510.aspx) creates a front-end IP configuration for a load balancer.</span></span> 
* <span data-ttu-id="b759d-178">[New-AzureRmLoadBalancerRuleConfig](http://msdn.microsoft.com/library/mt619391.aspx) creates a rule configuration for a load balancer.</span><span class="sxs-lookup"><span data-stu-id="b759d-178">[New-AzureRmLoadBalancerRuleConfig](http://msdn.microsoft.com/library/mt619391.aspx) creates a rule configuration for a load balancer.</span></span> 
* <span data-ttu-id="b759d-179">[New-AzureRmLoadBalancerBackendAddressPoolConfig](http://msdn.microsoft.com/library/mt603791.aspx) creates a backend address pool configuration for a load balancer.</span><span class="sxs-lookup"><span data-stu-id="b759d-179">[New-AzureRmLoadBalancerBackendAddressPoolConfig](http://msdn.microsoft.com/library/mt603791.aspx) creates a backend address pool configuration for a load balancer.</span></span> 
* <span data-ttu-id="b759d-180">[New-AzureRmLoadBalancerProbeConfig](http://msdn.microsoft.com/library/mt603847.aspx) creates a probe configuration for a load balancer.</span><span class="sxs-lookup"><span data-stu-id="b759d-180">[New-AzureRmLoadBalancerProbeConfig](http://msdn.microsoft.com/library/mt603847.aspx) creates a probe configuration for a load balancer.</span></span>
* <span data-ttu-id="b759d-181">[Remove-AzureRmLoadBalancer](http://msdn.microsoft.com/library/mt603862.aspx) removes a load balancer from an Azure resource group.</span><span class="sxs-lookup"><span data-stu-id="b759d-181">[Remove-AzureRmLoadBalancer](http://msdn.microsoft.com/library/mt603862.aspx) removes a load balancer from an Azure resource group.</span></span>
