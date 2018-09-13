## <a name="scenario"></a><span data-ttu-id="9c601-101">Scenario</span><span class="sxs-lookup"><span data-stu-id="9c601-101">Scenario</span></span>
<span data-ttu-id="9c601-102">To better illustrate how to create a VNet and subnets, this document will use the scenario below.</span><span class="sxs-lookup"><span data-stu-id="9c601-102">To better illustrate how to create a VNet and subnets, this document will use the scenario below.</span></span>

![VNet scenario](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-networks-create-vnet-scenario-include/vnet-scenario.png)

<span data-ttu-id="9c601-104">In this scenario you will create a VNet named **TestVNet** with a reserved CIDR block of **192.168.0.0./16**.</span><span class="sxs-lookup"><span data-stu-id="9c601-104">In this scenario you will create a VNet named **TestVNet** with a reserved CIDR block of **192.168.0.0./16**.</span></span> <span data-ttu-id="9c601-105">Your VNet will contain the following subnets:</span><span class="sxs-lookup"><span data-stu-id="9c601-105">Your VNet will contain the following subnets:</span></span> 

* <span data-ttu-id="9c601-106">**FrontEnd**, using **192.168.1.0/24** as its CIDR block.</span><span class="sxs-lookup"><span data-stu-id="9c601-106">**FrontEnd**, using **192.168.1.0/24** as its CIDR block.</span></span>
* <span data-ttu-id="9c601-107">**BackEnd**, using **192.168.2.0/24** as its CIDR block.</span><span class="sxs-lookup"><span data-stu-id="9c601-107">**BackEnd**, using **192.168.2.0/24** as its CIDR block.</span></span>


