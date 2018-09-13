## <a name="scenario"></a><span data-ttu-id="425be-101">Scenario</span><span class="sxs-lookup"><span data-stu-id="425be-101">Scenario</span></span>
<span data-ttu-id="425be-102">This document will walk through a deployment that uses a static public IP address allocated to a virtual machine (VM).</span><span class="sxs-lookup"><span data-stu-id="425be-102">This document will walk through a deployment that uses a static public IP address allocated to a virtual machine (VM).</span></span> <span data-ttu-id="425be-103">In this scenario, you have a single VM with its own static public IP address.</span><span class="sxs-lookup"><span data-stu-id="425be-103">In this scenario, you have a single VM with its own static public IP address.</span></span> <span data-ttu-id="425be-104">The VM is part of a subnet named **FrontEnd** and also has a static private IP address (**192.168.1.101**) in that subnet.</span><span class="sxs-lookup"><span data-stu-id="425be-104">The VM is part of a subnet named **FrontEnd** and also has a static private IP address (**192.168.1.101**) in that subnet.</span></span>

<span data-ttu-id="425be-105">You may need a static IP address for web servers that require SSL connections in which the SSL certificate is linked to an IP address.</span><span class="sxs-lookup"><span data-stu-id="425be-105">You may need a static IP address for web servers that require SSL connections in which the SSL certificate is linked to an IP address.</span></span> 

![IMAGE DESCRIPTION](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-network-deploy-static-pip-scenario-include/figure1.png)

<span data-ttu-id="425be-107">You can follow the steps below to deploy the environment shown in the figure above.</span><span class="sxs-lookup"><span data-stu-id="425be-107">You can follow the steps below to deploy the environment shown in the figure above.</span></span>


