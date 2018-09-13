<span data-ttu-id="0a16b-101">The Availability Group listener is an IP address and network name that the SQL Server Availability Group listens on.</span><span class="sxs-lookup"><span data-stu-id="0a16b-101">The Availability Group listener is an IP address and network name that the SQL Server Availability Group listens on.</span></span> <span data-ttu-id="0a16b-102">To create the Availability Group listener, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="0a16b-102">To create the Availability Group listener, do the following steps:</span></span>

1. <span data-ttu-id="0a16b-103">[Get the name of the cluster network resource](#getnet).</span><span class="sxs-lookup"><span data-stu-id="0a16b-103">[Get the name of the cluster network resource](#getnet).</span></span>

1. <span data-ttu-id="0a16b-104">[Add the client access point](#addcap).</span><span class="sxs-lookup"><span data-stu-id="0a16b-104">[Add the client access point](#addcap).</span></span>

1. <span data-ttu-id="0a16b-105">[Configure the IP resource for the Availability Group](#congroup).</span><span class="sxs-lookup"><span data-stu-id="0a16b-105">[Configure the IP resource for the Availability Group](#congroup).</span></span>

1. [<span data-ttu-id="0a16b-106">Make the SQL Server availability group resource dependent on the client access point</span><span class="sxs-lookup"><span data-stu-id="0a16b-106">Make the SQL Server availability group resource dependent on the client access point</span></span>](#dependencyGroup)

1. <span data-ttu-id="0a16b-107">[Make the client access point resource dependent on the IP address](#listname).</span><span class="sxs-lookup"><span data-stu-id="0a16b-107">[Make the client access point resource dependent on the IP address](#listname).</span></span>

1. <span data-ttu-id="0a16b-108">[Set the cluster parameters in PowerShell](#setparam).</span><span class="sxs-lookup"><span data-stu-id="0a16b-108">[Set the cluster parameters in PowerShell](#setparam).</span></span>

<span data-ttu-id="0a16b-109">The following sections provide detailed instructions for each of these steps.</span><span class="sxs-lookup"><span data-stu-id="0a16b-109">The following sections provide detailed instructions for each of these steps.</span></span> 

#### <a name="getnet"></a><span data-ttu-id="0a16b-110">Get the name of the cluster network resource</span><span class="sxs-lookup"><span data-stu-id="0a16b-110">Get the name of the cluster network resource</span></span>

1. <span data-ttu-id="0a16b-111">Use RDP to connect to the Azure virtual machine that hosts the primary replica.</span><span class="sxs-lookup"><span data-stu-id="0a16b-111">Use RDP to connect to the Azure virtual machine that hosts the primary replica.</span></span> 

1. <span data-ttu-id="0a16b-112">Open Failover Cluster Manager.</span><span class="sxs-lookup"><span data-stu-id="0a16b-112">Open Failover Cluster Manager.</span></span>

1. <span data-ttu-id="0a16b-113">Select the **Networks** node, and note the cluster network name.</span><span class="sxs-lookup"><span data-stu-id="0a16b-113">Select the **Networks** node, and note the cluster network name.</span></span> <span data-ttu-id="0a16b-114">Use this name in the `$ClusterNetworkName` variable in the PowerShell script.</span><span class="sxs-lookup"><span data-stu-id="0a16b-114">Use this name in the `$ClusterNetworkName` variable in the PowerShell script.</span></span>

   <span data-ttu-id="0a16b-115">In the following picture the cluster network name is **Cluster Network 1**:</span><span class="sxs-lookup"><span data-stu-id="0a16b-115">In the following picture the cluster network name is **Cluster Network 1**:</span></span>

   ![Cluster Network Name](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-ag-listener-configure/90-clusternetworkname.png)

#### <a name="addcap"></a><span data-ttu-id="0a16b-117">Add the client access point</span><span class="sxs-lookup"><span data-stu-id="0a16b-117">Add the client access point</span></span>

<span data-ttu-id="0a16b-118">The client access point is the network name that applications use to connect to the databases in an availability group.</span><span class="sxs-lookup"><span data-stu-id="0a16b-118">The client access point is the network name that applications use to connect to the databases in an availability group.</span></span> <span data-ttu-id="0a16b-119">Create the client access point in Failover Cluster Manager.</span><span class="sxs-lookup"><span data-stu-id="0a16b-119">Create the client access point in Failover Cluster Manager.</span></span> 

1. <span data-ttu-id="0a16b-120">Expand the cluster name, and then click **Roles**.</span><span class="sxs-lookup"><span data-stu-id="0a16b-120">Expand the cluster name, and then click **Roles**.</span></span>

1. <span data-ttu-id="0a16b-121">In the **Roles** pane, right-click the Availability Group name and then select **Add Resource** > **Client Access Point**.</span><span class="sxs-lookup"><span data-stu-id="0a16b-121">In the **Roles** pane, right-click the Availability Group name and then select **Add Resource** > **Client Access Point**.</span></span>

   ![Client Access Point](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-ag-listener-configure/92-addclientaccesspoint.png)

1. <span data-ttu-id="0a16b-123">In the **Name** box, create a name for this new listener.</span><span class="sxs-lookup"><span data-stu-id="0a16b-123">In the **Name** box, create a name for this new listener.</span></span> 

   <span data-ttu-id="0a16b-124">The name for the new listener is the network name that applications use to connect to databases in the SQL Server Availability Group.</span><span class="sxs-lookup"><span data-stu-id="0a16b-124">The name for the new listener is the network name that applications use to connect to databases in the SQL Server Availability Group.</span></span>
   
   <span data-ttu-id="0a16b-125">To finish creating the listener, click **Next** twice, and then click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="0a16b-125">To finish creating the listener, click **Next** twice, and then click **Finish**.</span></span> <span data-ttu-id="0a16b-126">Do not bring the listener or resource online at this point.</span><span class="sxs-lookup"><span data-stu-id="0a16b-126">Do not bring the listener or resource online at this point.</span></span>
   
#### <a name="congroup"></a><span data-ttu-id="0a16b-127">Configure the IP resource for the Availability Group</span><span class="sxs-lookup"><span data-stu-id="0a16b-127">Configure the IP resource for the Availability Group</span></span>

1. <span data-ttu-id="0a16b-128">Click the **Resources** tab, then expand the client access point you created.</span><span class="sxs-lookup"><span data-stu-id="0a16b-128">Click the **Resources** tab, then expand the client access point you created.</span></span> <span data-ttu-id="0a16b-129">The client access point is offline.</span><span class="sxs-lookup"><span data-stu-id="0a16b-129">The client access point is offline.</span></span>

   ![Client Access Point](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-ag-listener-configure/94-newclientaccesspoint.png) 

1. <span data-ttu-id="0a16b-131">Right-click the IP resource and click properties.</span><span class="sxs-lookup"><span data-stu-id="0a16b-131">Right-click the IP resource and click properties.</span></span> <span data-ttu-id="0a16b-132">Note the name of the IP address.</span><span class="sxs-lookup"><span data-stu-id="0a16b-132">Note the name of the IP address.</span></span> <span data-ttu-id="0a16b-133">Use this name in the `$IPResourceName` variable in the PowerShell script.</span><span class="sxs-lookup"><span data-stu-id="0a16b-133">Use this name in the `$IPResourceName` variable in the PowerShell script.</span></span>

1. <span data-ttu-id="0a16b-134">Under **IP Address**, click **Static IP Address**.</span><span class="sxs-lookup"><span data-stu-id="0a16b-134">Under **IP Address**, click **Static IP Address**.</span></span> <span data-ttu-id="0a16b-135">Set the IP address to the same address that you used when you set the load balancer address on the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="0a16b-135">Set the IP address to the same address that you used when you set the load balancer address on the Azure portal.</span></span>

   ![IP Resource](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-ag-listener-configure/96-ipresource.png) 

<!-----------------------I don't see this option on server 2016
1. Disable NetBIOS for this address and click **OK**. Repeat this step for each IP resource if your solution spans multiple Azure VNets. 
------------------------->

#### <a name = "dependencyGroup"></a><span data-ttu-id="0a16b-137">Make the SQL Server availability group resource dependent on the client access point</span><span class="sxs-lookup"><span data-stu-id="0a16b-137">Make the SQL Server availability group resource dependent on the client access point</span></span>

1. <span data-ttu-id="0a16b-138">In Failover Cluster Manager, click **Roles** and click your Availability Group.</span><span class="sxs-lookup"><span data-stu-id="0a16b-138">In Failover Cluster Manager, click **Roles** and click your Availability Group.</span></span>

1. <span data-ttu-id="0a16b-139">On the **Resources** tab, right-click the availability resource group under **Server Name** and click **Properties**.</span><span class="sxs-lookup"><span data-stu-id="0a16b-139">On the **Resources** tab, right-click the availability resource group under **Server Name** and click **Properties**.</span></span> 

1. <span data-ttu-id="0a16b-140">On the dependencies tab, add the name resource.</span><span class="sxs-lookup"><span data-stu-id="0a16b-140">On the dependencies tab, add the name resource.</span></span> <span data-ttu-id="0a16b-141">This resource is the client access point.</span><span class="sxs-lookup"><span data-stu-id="0a16b-141">This resource is the client access point.</span></span> 

   ![IP Resource](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-ag-listener-configure/97-propertiesdependencies.png) 

1. <span data-ttu-id="0a16b-143">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="0a16b-143">Click **OK**.</span></span>

#### <a name="listname"></a><span data-ttu-id="0a16b-144">Make the client access point resource dependent on the IP address</span><span class="sxs-lookup"><span data-stu-id="0a16b-144">Make the client access point resource dependent on the IP address</span></span>

1. <span data-ttu-id="0a16b-145">In Failover Cluster Manager, click **Roles** and click your Availability Group.</span><span class="sxs-lookup"><span data-stu-id="0a16b-145">In Failover Cluster Manager, click **Roles** and click your Availability Group.</span></span> 

1. <span data-ttu-id="0a16b-146">On the **Resources** tab, right-click the client access point resource under **Server Name** and click **Properties**.</span><span class="sxs-lookup"><span data-stu-id="0a16b-146">On the **Resources** tab, right-click the client access point resource under **Server Name** and click **Properties**.</span></span> 

   ![IP Resource](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-ag-listener-configure/98-dependencies.png) 

1. <span data-ttu-id="0a16b-148">Click the **Dependencies** tab. Set a dependency on the listener resource name.</span><span class="sxs-lookup"><span data-stu-id="0a16b-148">Click the **Dependencies** tab. Set a dependency on the listener resource name.</span></span> <span data-ttu-id="0a16b-149">If there are multiple resources listed, verify that the IP addresses have OR, not AND, dependencies.</span><span class="sxs-lookup"><span data-stu-id="0a16b-149">If there are multiple resources listed, verify that the IP addresses have OR, not AND, dependencies.</span></span> <span data-ttu-id="0a16b-150">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="0a16b-150">Click **OK**.</span></span> 

   ![IP Resource](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-ag-listener-configure/98-propertiesdependencies.png) 

1. <span data-ttu-id="0a16b-152">Right-click the listener name and click **Bring Online**.</span><span class="sxs-lookup"><span data-stu-id="0a16b-152">Right-click the listener name and click **Bring Online**.</span></span> 

#### <a name="setparam"></a><span data-ttu-id="0a16b-153">Set the cluster parameters in PowerShell</span><span class="sxs-lookup"><span data-stu-id="0a16b-153">Set the cluster parameters in PowerShell</span></span>

1. <span data-ttu-id="0a16b-154">Copy the following PowerShell script to one of your SQL Servers.</span><span class="sxs-lookup"><span data-stu-id="0a16b-154">Copy the following PowerShell script to one of your SQL Servers.</span></span> <span data-ttu-id="0a16b-155">Update the variables for your environment.</span><span class="sxs-lookup"><span data-stu-id="0a16b-155">Update the variables for your environment.</span></span>     
   ```PowerShell
   $ClusterNetworkName = "<MyClusterNetworkName>" # the cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher to find the name)
   $IPResourceName = "<IPResourceName>" # the IP Address resource name
   $ILBIP = “<n.n.n.n>” # the IP Address of the Internal Load Balancer (ILB). This is the static IP address for the load balancer you configured in the Azure portal.
   [int]$ProbePort = <nnnnn>

   Import-Module FailoverClusters

   Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
   ```

2. <span data-ttu-id="0a16b-156">Set the cluster parameters by running the PowerShell script on one of the cluster nodes.</span><span class="sxs-lookup"><span data-stu-id="0a16b-156">Set the cluster parameters by running the PowerShell script on one of the cluster nodes.</span></span>  

> [!NOTE]
> <span data-ttu-id="0a16b-157">If your SQL Servers are in separate regions, you need to run the PowerShell script twice.</span><span class="sxs-lookup"><span data-stu-id="0a16b-157">If your SQL Servers are in separate regions, you need to run the PowerShell script twice.</span></span> <span data-ttu-id="0a16b-158">The first time, use the `$ILBIP` and `$ProbePort` from the first region.</span><span class="sxs-lookup"><span data-stu-id="0a16b-158">The first time, use the `$ILBIP` and `$ProbePort` from the first region.</span></span> <span data-ttu-id="0a16b-159">The second time, use the `$ILBIP` and `$ProbePort` from the second region.</span><span class="sxs-lookup"><span data-stu-id="0a16b-159">The second time, use the `$ILBIP` and `$ProbePort` from the second region.</span></span> <span data-ttu-id="0a16b-160">The cluster network name, and the cluster IP resource name are the same.</span><span class="sxs-lookup"><span data-stu-id="0a16b-160">The cluster network name, and the cluster IP resource name are the same.</span></span> 









