## <a name="how-to-create-a-vnet-using-the-azure-cli"></a><span data-ttu-id="ce7c6-101">How to create a VNet using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="ce7c6-101">How to create a VNet using the Azure CLI</span></span>
<span data-ttu-id="ce7c6-102">You can use the Azure CLI to manage your Azure resources from the command prompt from any computer running Windows, Linux, or OSX.</span><span class="sxs-lookup"><span data-stu-id="ce7c6-102">You can use the Azure CLI to manage your Azure resources from the command prompt from any computer running Windows, Linux, or OSX.</span></span> <span data-ttu-id="ce7c6-103">To create a VNet by using the Azure CLI, follow the steps below.</span><span class="sxs-lookup"><span data-stu-id="ce7c6-103">To create a VNet by using the Azure CLI, follow the steps below.</span></span>

1. <span data-ttu-id="ce7c6-104">If you have never used the Azure CLI, see [Install and Configure the Azure CLI](../articles/cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span><span class="sxs-lookup"><span data-stu-id="ce7c6-104">If you have never used the Azure CLI, see [Install and Configure the Azure CLI](../articles/cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="ce7c6-105">Run the **azure config mode** command to switch to Resource Manager mode, as shown below.</span><span class="sxs-lookup"><span data-stu-id="ce7c6-105">Run the **azure config mode** command to switch to Resource Manager mode, as shown below.</span></span>
   
        azure config mode arm
   
    <span data-ttu-id="ce7c6-106">Here is the expected output for the command above:</span><span class="sxs-lookup"><span data-stu-id="ce7c6-106">Here is the expected output for the command above:</span></span>
   
        info:    New mode is arm
3. <span data-ttu-id="ce7c6-107">If necessary, run the **azure group create** to create a new resource group, as shown below.</span><span class="sxs-lookup"><span data-stu-id="ce7c6-107">If necessary, run the **azure group create** to create a new resource group, as shown below.</span></span> <span data-ttu-id="ce7c6-108">Notice the output of the command.</span><span class="sxs-lookup"><span data-stu-id="ce7c6-108">Notice the output of the command.</span></span> <span data-ttu-id="ce7c6-109">The list shown after the output explains the parameters used.</span><span class="sxs-lookup"><span data-stu-id="ce7c6-109">The list shown after the output explains the parameters used.</span></span> <span data-ttu-id="ce7c6-110">For more information about resource groups, visit [Azure Resource Manager Overview](../articles/azure-resource-manager/resource-group-overview.md#resource-groups).</span><span class="sxs-lookup"><span data-stu-id="ce7c6-110">For more information about resource groups, visit [Azure Resource Manager Overview](../articles/azure-resource-manager/resource-group-overview.md#resource-groups).</span></span>
   
        azure group create -n TestRG -l centralus
   
    <span data-ttu-id="ce7c6-111">Here is the expected output for the command above:</span><span class="sxs-lookup"><span data-stu-id="ce7c6-111">Here is the expected output for the command above:</span></span>
   
        info:    Executing command group create
        + Getting resource group TestRG
        + Creating resource group TestRG
        info:    Created resource group TestRG
        data:    Id:                  /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG
        data:    Name:                TestRG
        data:    Location:            centralus
        data:    Provisioning State:  Succeeded
        data:    Tags: null
        data:
        info:    group create command OK
   
   * <span data-ttu-id="ce7c6-112">**-n (or --name)**.</span><span class="sxs-lookup"><span data-stu-id="ce7c6-112">**-n (or --name)**.</span></span> <span data-ttu-id="ce7c6-113">Name for the new resource group.</span><span class="sxs-lookup"><span data-stu-id="ce7c6-113">Name for the new resource group.</span></span> <span data-ttu-id="ce7c6-114">For our scenario, *TestRG*.</span><span class="sxs-lookup"><span data-stu-id="ce7c6-114">For our scenario, *TestRG*.</span></span>
   * <span data-ttu-id="ce7c6-115">**-l (or --location)**.</span><span class="sxs-lookup"><span data-stu-id="ce7c6-115">**-l (or --location)**.</span></span> <span data-ttu-id="ce7c6-116">Azure region where the new resource group will be created.</span><span class="sxs-lookup"><span data-stu-id="ce7c6-116">Azure region where the new resource group will be created.</span></span> <span data-ttu-id="ce7c6-117">For our scenario, *centralus*.</span><span class="sxs-lookup"><span data-stu-id="ce7c6-117">For our scenario, *centralus*.</span></span>
4. <span data-ttu-id="ce7c6-118">Run the **azure network vnet create** command to create a VNet and a subnet, as shown below.</span><span class="sxs-lookup"><span data-stu-id="ce7c6-118">Run the **azure network vnet create** command to create a VNet and a subnet, as shown below.</span></span> 
   
        azure network vnet create -g TestRG -n TestVNet -a 192.168.0.0/16 -l centralus
   
    <span data-ttu-id="ce7c6-119">Here is the expected output for the command above:</span><span class="sxs-lookup"><span data-stu-id="ce7c6-119">Here is the expected output for the command above:</span></span>
   
        info:    Executing command network vnet create
        + Looking up virtual network "TestVNet"
        + Creating virtual network "TestVNet"
        + Loading virtual network state
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet2
        data:    Name                            : TestVNet
        data:    Type                            : Microsoft.Network/virtualNetworks
        data:    Location                        : centralus
        data:    ProvisioningState               : Succeeded
        data:    Address prefixes:
        data:      192.168.0.0/16
        info:    network vnet create command OK
   
   * <span data-ttu-id="ce7c6-120">**-g (or --resource-group)**.</span><span class="sxs-lookup"><span data-stu-id="ce7c6-120">**-g (or --resource-group)**.</span></span> <span data-ttu-id="ce7c6-121">Name of the resource group where the VNet will be created.</span><span class="sxs-lookup"><span data-stu-id="ce7c6-121">Name of the resource group where the VNet will be created.</span></span> <span data-ttu-id="ce7c6-122">For our scenario, *TestRG*.</span><span class="sxs-lookup"><span data-stu-id="ce7c6-122">For our scenario, *TestRG*.</span></span>
   * <span data-ttu-id="ce7c6-123">**-n (or --name)**.</span><span class="sxs-lookup"><span data-stu-id="ce7c6-123">**-n (or --name)**.</span></span> <span data-ttu-id="ce7c6-124">Name of the VNet to be created.</span><span class="sxs-lookup"><span data-stu-id="ce7c6-124">Name of the VNet to be created.</span></span> <span data-ttu-id="ce7c6-125">For our scenario, *TestVNet*</span><span class="sxs-lookup"><span data-stu-id="ce7c6-125">For our scenario, *TestVNet*</span></span>
   * <span data-ttu-id="ce7c6-126">**-a (or --address-prefixes)**.</span><span class="sxs-lookup"><span data-stu-id="ce7c6-126">**-a (or --address-prefixes)**.</span></span> <span data-ttu-id="ce7c6-127">List of CIDR blocks used for the VNet address space.</span><span class="sxs-lookup"><span data-stu-id="ce7c6-127">List of CIDR blocks used for the VNet address space.</span></span> <span data-ttu-id="ce7c6-128">For our scenario, *192.168.0.0/16*</span><span class="sxs-lookup"><span data-stu-id="ce7c6-128">For our scenario, *192.168.0.0/16*</span></span>
   * <span data-ttu-id="ce7c6-129">**-l (or --location)**.</span><span class="sxs-lookup"><span data-stu-id="ce7c6-129">**-l (or --location)**.</span></span> <span data-ttu-id="ce7c6-130">Azure region where the VNet will be created.</span><span class="sxs-lookup"><span data-stu-id="ce7c6-130">Azure region where the VNet will be created.</span></span> <span data-ttu-id="ce7c6-131">For our scenario, *centralus*.</span><span class="sxs-lookup"><span data-stu-id="ce7c6-131">For our scenario, *centralus*.</span></span>
5. <span data-ttu-id="ce7c6-132">Run the **azure network vnet subnet create** command to create a subnet as shown below.</span><span class="sxs-lookup"><span data-stu-id="ce7c6-132">Run the **azure network vnet subnet create** command to create a subnet as shown below.</span></span> <span data-ttu-id="ce7c6-133">Notice the output of the command.</span><span class="sxs-lookup"><span data-stu-id="ce7c6-133">Notice the output of the command.</span></span> <span data-ttu-id="ce7c6-134">The list shown after the output explains the parameters used.</span><span class="sxs-lookup"><span data-stu-id="ce7c6-134">The list shown after the output explains the parameters used.</span></span>
   
        azure network vnet subnet create -g TestRG -e TestVNet -n FrontEnd -a 192.168.1.0/24
   
    <span data-ttu-id="ce7c6-135">Here is the expected output for the command above:</span><span class="sxs-lookup"><span data-stu-id="ce7c6-135">Here is the expected output for the command above:</span></span>
   
        info:    Executing command network vnet subnet create
        + Looking up the subnet "FrontEnd"
        + Creating subnet "FrontEnd"
        + Looking up the subnet "FrontEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
        data:    Type                            : Microsoft.Network/virtualNetworks/subnets
        data:    ProvisioningState               : Succeeded
        data:    Name                            : FrontEnd
        data:    Address prefix                  : 192.168.1.0/24
        data:
        info:    network vnet subnet create command OK
   
   * <span data-ttu-id="ce7c6-136">**-e (or --vnet-name**.</span><span class="sxs-lookup"><span data-stu-id="ce7c6-136">**-e (or --vnet-name**.</span></span> <span data-ttu-id="ce7c6-137">Name of the VNet where the subnet will be created.</span><span class="sxs-lookup"><span data-stu-id="ce7c6-137">Name of the VNet where the subnet will be created.</span></span> <span data-ttu-id="ce7c6-138">For our scenario, *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="ce7c6-138">For our scenario, *TestVNet*.</span></span>
   * <span data-ttu-id="ce7c6-139">**-n (or --name)**.</span><span class="sxs-lookup"><span data-stu-id="ce7c6-139">**-n (or --name)**.</span></span> <span data-ttu-id="ce7c6-140">Name of the new subnet.</span><span class="sxs-lookup"><span data-stu-id="ce7c6-140">Name of the new subnet.</span></span> <span data-ttu-id="ce7c6-141">For our scenario, *FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="ce7c6-141">For our scenario, *FrontEnd*.</span></span>
   * <span data-ttu-id="ce7c6-142">**-a (or --address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="ce7c6-142">**-a (or --address-prefix)**.</span></span> <span data-ttu-id="ce7c6-143">Subnet CIDR block.</span><span class="sxs-lookup"><span data-stu-id="ce7c6-143">Subnet CIDR block.</span></span> <span data-ttu-id="ce7c6-144">Four our scenario, *192.168.1.0/24*.</span><span class="sxs-lookup"><span data-stu-id="ce7c6-144">Four our scenario, *192.168.1.0/24*.</span></span>
6. <span data-ttu-id="ce7c6-145">Repeat step 5 above to create other subnets, if necessary.</span><span class="sxs-lookup"><span data-stu-id="ce7c6-145">Repeat step 5 above to create other subnets, if necessary.</span></span> <span data-ttu-id="ce7c6-146">For our scenario, run the command below to create the *BackEnd* subnet.</span><span class="sxs-lookup"><span data-stu-id="ce7c6-146">For our scenario, run the command below to create the *BackEnd* subnet.</span></span>
   
        azure network vnet subnet create -g TestRG -e TestVNet -n BackEnd -a 192.168.2.0/24
7. <span data-ttu-id="ce7c6-147">Run the **azure network vnet show** command to view the properties of the new vnet, as shown below.</span><span class="sxs-lookup"><span data-stu-id="ce7c6-147">Run the **azure network vnet show** command to view the properties of the new vnet, as shown below.</span></span>
   
        azure network vnet show -g TestRG -n TestVNet
   
    <span data-ttu-id="ce7c6-148">Here is the expected output for the command above:</span><span class="sxs-lookup"><span data-stu-id="ce7c6-148">Here is the expected output for the command above:</span></span>
   
        info:    Executing command network vnet show
        + Looking up virtual network "TestVNet"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        data:    Name                            : TestVNet
        data:    Type                            : Microsoft.Network/virtualNetworks
        data:    Location                        : centralus
        data:    ProvisioningState               : Succeeded
        data:    Address prefixes:
        data:      192.168.0.0/16
        data:    Subnets:
        data:      Name                          : FrontEnd
        data:      Address prefix                : 192.168.1.0/24
        data:
        data:      Name                          : BackEnd
        data:      Address prefix                : 192.168.2.0/24
        data:
        info:    network vnet show command OK

