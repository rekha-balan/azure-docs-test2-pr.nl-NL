## <a name="how-to-create-a-classic-vnet-using-azure-cli"></a><span data-ttu-id="a5c81-101">How to create a classic VNet using Azure CLI</span><span class="sxs-lookup"><span data-stu-id="a5c81-101">How to create a classic VNet using Azure CLI</span></span>
<span data-ttu-id="a5c81-102">You can use the Azure CLI to manage your Azure resources from the command prompt from any computer running Windows, Linux, or OSX.</span><span class="sxs-lookup"><span data-stu-id="a5c81-102">You can use the Azure CLI to manage your Azure resources from the command prompt from any computer running Windows, Linux, or OSX.</span></span> <span data-ttu-id="a5c81-103">To create a VNet by using the Azure CLI, follow the steps below.</span><span class="sxs-lookup"><span data-stu-id="a5c81-103">To create a VNet by using the Azure CLI, follow the steps below.</span></span>

1. <span data-ttu-id="a5c81-104">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../articles/cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span><span class="sxs-lookup"><span data-stu-id="a5c81-104">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../articles/cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="a5c81-105">Run the **azure network vnet create** command to create a VNet and a subnet, as shown below.</span><span class="sxs-lookup"><span data-stu-id="a5c81-105">Run the **azure network vnet create** command to create a VNet and a subnet, as shown below.</span></span> <span data-ttu-id="a5c81-106">The list shown after the output explains the parameters used.</span><span class="sxs-lookup"><span data-stu-id="a5c81-106">The list shown after the output explains the parameters used.</span></span>
   
            azure network vnet create --vnet TestVNet -e 192.168.0.0 -i 16 -n FrontEnd -p 192.168.1.0 -r 24 -l "Central US"
   
    <span data-ttu-id="a5c81-107">Expected output:</span><span class="sxs-lookup"><span data-stu-id="a5c81-107">Expected output:</span></span>
   
            info:    Executing command network vnet create
            + Looking up network configuration
            + Looking up locations
            + Setting network configuration
            info:    network vnet create command OK
   
   * <span data-ttu-id="a5c81-108">**--vnet**.</span><span class="sxs-lookup"><span data-stu-id="a5c81-108">**--vnet**.</span></span> <span data-ttu-id="a5c81-109">Name of the VNet to be created.</span><span class="sxs-lookup"><span data-stu-id="a5c81-109">Name of the VNet to be created.</span></span> <span data-ttu-id="a5c81-110">For our scenario, *TestVNet*</span><span class="sxs-lookup"><span data-stu-id="a5c81-110">For our scenario, *TestVNet*</span></span>
   * <span data-ttu-id="a5c81-111">**-e (or --address-space)**.</span><span class="sxs-lookup"><span data-stu-id="a5c81-111">**-e (or --address-space)**.</span></span> <span data-ttu-id="a5c81-112">VNet address space.</span><span class="sxs-lookup"><span data-stu-id="a5c81-112">VNet address space.</span></span> <span data-ttu-id="a5c81-113">For our scenario, *192.168.0.0*</span><span class="sxs-lookup"><span data-stu-id="a5c81-113">For our scenario, *192.168.0.0*</span></span>
   * <span data-ttu-id="a5c81-114">**-i (or -cidr)**.</span><span class="sxs-lookup"><span data-stu-id="a5c81-114">**-i (or -cidr)**.</span></span> <span data-ttu-id="a5c81-115">Network mask in CIDR format.</span><span class="sxs-lookup"><span data-stu-id="a5c81-115">Network mask in CIDR format.</span></span> <span data-ttu-id="a5c81-116">For our scenario, *16*.</span><span class="sxs-lookup"><span data-stu-id="a5c81-116">For our scenario, *16*.</span></span>
   * <span data-ttu-id="a5c81-117">**-n (or --subnet-name**).</span><span class="sxs-lookup"><span data-stu-id="a5c81-117">**-n (or --subnet-name**).</span></span> <span data-ttu-id="a5c81-118">Name of the first subnet.</span><span class="sxs-lookup"><span data-stu-id="a5c81-118">Name of the first subnet.</span></span> <span data-ttu-id="a5c81-119">For our scenario, *FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="a5c81-119">For our scenario, *FrontEnd*.</span></span>
   * <span data-ttu-id="a5c81-120">**-p (or --subnet-start-ip)**.</span><span class="sxs-lookup"><span data-stu-id="a5c81-120">**-p (or --subnet-start-ip)**.</span></span> <span data-ttu-id="a5c81-121">Starting IP address for subnet, or subnet address space.</span><span class="sxs-lookup"><span data-stu-id="a5c81-121">Starting IP address for subnet, or subnet address space.</span></span> <span data-ttu-id="a5c81-122">For our scenario, *192.168.1.0*.</span><span class="sxs-lookup"><span data-stu-id="a5c81-122">For our scenario, *192.168.1.0*.</span></span>
   * <span data-ttu-id="a5c81-123">**-r (or --subnet-cidr)**.</span><span class="sxs-lookup"><span data-stu-id="a5c81-123">**-r (or --subnet-cidr)**.</span></span> <span data-ttu-id="a5c81-124">Network mask in CIDR format for subnet.</span><span class="sxs-lookup"><span data-stu-id="a5c81-124">Network mask in CIDR format for subnet.</span></span> <span data-ttu-id="a5c81-125">For our scenario, *24*.</span><span class="sxs-lookup"><span data-stu-id="a5c81-125">For our scenario, *24*.</span></span>
   * <span data-ttu-id="a5c81-126">**-l (or --location)**.</span><span class="sxs-lookup"><span data-stu-id="a5c81-126">**-l (or --location)**.</span></span> <span data-ttu-id="a5c81-127">Azure region where the VNet will be created.</span><span class="sxs-lookup"><span data-stu-id="a5c81-127">Azure region where the VNet will be created.</span></span> <span data-ttu-id="a5c81-128">For our scenario, *Central US*.</span><span class="sxs-lookup"><span data-stu-id="a5c81-128">For our scenario, *Central US*.</span></span>
3. <span data-ttu-id="a5c81-129">Run the **azure network vnet subnet create** command to create a subnet as shown below.</span><span class="sxs-lookup"><span data-stu-id="a5c81-129">Run the **azure network vnet subnet create** command to create a subnet as shown below.</span></span> <span data-ttu-id="a5c81-130">The list shown after the output explains the parameters used.</span><span class="sxs-lookup"><span data-stu-id="a5c81-130">The list shown after the output explains the parameters used.</span></span>
   
            azure network vnet subnet create -t TestVNet -n BackEnd -a 192.168.2.0/24
   
    <span data-ttu-id="a5c81-131">Here is the expected output for the command above:</span><span class="sxs-lookup"><span data-stu-id="a5c81-131">Here is the expected output for the command above:</span></span>
   
            info:    Executing command network vnet subnet create
            + Looking up network configuration
            + Creating subnet "BackEnd"
            + Setting network configuration
            + Looking up the subnet "BackEnd"
            + Looking up network configuration
            data:    Name                            : BackEnd
            data:    Address prefix                  : 192.168.2.0/24
            info:    network vnet subnet create command OK
   
   * <span data-ttu-id="a5c81-132">**-t (or --vnet-name**.</span><span class="sxs-lookup"><span data-stu-id="a5c81-132">**-t (or --vnet-name**.</span></span> <span data-ttu-id="a5c81-133">Name of the VNet where the subnet will be created.</span><span class="sxs-lookup"><span data-stu-id="a5c81-133">Name of the VNet where the subnet will be created.</span></span> <span data-ttu-id="a5c81-134">For our scenario, *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="a5c81-134">For our scenario, *TestVNet*.</span></span>
   * <span data-ttu-id="a5c81-135">**-n (or --name)**.</span><span class="sxs-lookup"><span data-stu-id="a5c81-135">**-n (or --name)**.</span></span> <span data-ttu-id="a5c81-136">Name of the new subnet.</span><span class="sxs-lookup"><span data-stu-id="a5c81-136">Name of the new subnet.</span></span> <span data-ttu-id="a5c81-137">For our scenario, *BackEnd*.</span><span class="sxs-lookup"><span data-stu-id="a5c81-137">For our scenario, *BackEnd*.</span></span>
   * <span data-ttu-id="a5c81-138">**-a (or --address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="a5c81-138">**-a (or --address-prefix)**.</span></span> <span data-ttu-id="a5c81-139">Subnet CIDR block.</span><span class="sxs-lookup"><span data-stu-id="a5c81-139">Subnet CIDR block.</span></span> <span data-ttu-id="a5c81-140">Four our scenario, *192.168.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="a5c81-140">Four our scenario, *192.168.2.0/24*.</span></span>
4. <span data-ttu-id="a5c81-141">Run the **azure network vnet show** command to view the properties of the new vnet, as shown below.</span><span class="sxs-lookup"><span data-stu-id="a5c81-141">Run the **azure network vnet show** command to view the properties of the new vnet, as shown below.</span></span>
   
            azure network vnet show
   
    <span data-ttu-id="a5c81-142">Here is the expected output for the command above:</span><span class="sxs-lookup"><span data-stu-id="a5c81-142">Here is the expected output for the command above:</span></span>
   
            info:    Executing command network vnet show
            Virtual network name: TestVNet
            + Looking up the virtual network sites
            data:    Name                            : TestVNet
            data:    Location                        : Central US
            data:    State                           : Created
            data:    Address space                   : 192.168.0.0/16
            data:    Subnets:
            data:      Name                          : FrontEnd
            data:      Address prefix                : 192.168.1.0/24
            data:
            data:      Name                          : BackEnd
            data:      Address prefix                : 192.168.2.0/24
            data:
            info:    network vnet show command OK

