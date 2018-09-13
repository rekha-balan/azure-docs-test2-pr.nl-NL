## <a name="deploy-the-arm-template-by-using-the-azure-cli"></a><span data-ttu-id="f60e1-101">Deploy the ARM template by using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="f60e1-101">Deploy the ARM template by using the Azure CLI</span></span>
<span data-ttu-id="f60e1-102">To deploy the ARM template you downloaded by using Azure CLI, follow the steps below.</span><span class="sxs-lookup"><span data-stu-id="f60e1-102">To deploy the ARM template you downloaded by using Azure CLI, follow the steps below.</span></span>

1. <span data-ttu-id="f60e1-103">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../articles/cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span><span class="sxs-lookup"><span data-stu-id="f60e1-103">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../articles/cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="f60e1-104">Run the **`azure config mode`** command to switch to Resource Manager mode, as shown below.</span><span class="sxs-lookup"><span data-stu-id="f60e1-104">Run the **`azure config mode`** command to switch to Resource Manager mode, as shown below.</span></span>
   
        azure config mode arm
   
    <span data-ttu-id="f60e1-105">Here is the expected output for the command above:</span><span class="sxs-lookup"><span data-stu-id="f60e1-105">Here is the expected output for the command above:</span></span>
   
        info:    New mode is arm
3. <span data-ttu-id="f60e1-106">If necessary, run the **`azure group create`** to create a new resource group, as shown below.</span><span class="sxs-lookup"><span data-stu-id="f60e1-106">If necessary, run the **`azure group create`** to create a new resource group, as shown below.</span></span> <span data-ttu-id="f60e1-107">Notice the output of the command.</span><span class="sxs-lookup"><span data-stu-id="f60e1-107">Notice the output of the command.</span></span> <span data-ttu-id="f60e1-108">The list shown after the output explains the parameters used.</span><span class="sxs-lookup"><span data-stu-id="f60e1-108">The list shown after the output explains the parameters used.</span></span> <span data-ttu-id="f60e1-109">For more information about resource groups, visit [Azure Resource Manager Overview](../articles/azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f60e1-109">For more information about resource groups, visit [Azure Resource Manager Overview](../articles/azure-resource-manager/resource-group-overview.md).</span></span>
   
        azure group create -n TestRG -l centralus
   
    <span data-ttu-id="f60e1-110">Here is the expected output for the command above:</span><span class="sxs-lookup"><span data-stu-id="f60e1-110">Here is the expected output for the command above:</span></span>
   
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
   
   * <span data-ttu-id="f60e1-111">**-n (or --name)**.</span><span class="sxs-lookup"><span data-stu-id="f60e1-111">**-n (or --name)**.</span></span> <span data-ttu-id="f60e1-112">Name for the new resource group.</span><span class="sxs-lookup"><span data-stu-id="f60e1-112">Name for the new resource group.</span></span> <span data-ttu-id="f60e1-113">For our scenario, *TestRG*.</span><span class="sxs-lookup"><span data-stu-id="f60e1-113">For our scenario, *TestRG*.</span></span>
   * <span data-ttu-id="f60e1-114">**-l (or --location)**.</span><span class="sxs-lookup"><span data-stu-id="f60e1-114">**-l (or --location)**.</span></span> <span data-ttu-id="f60e1-115">Azure region where the new resource group will be created.</span><span class="sxs-lookup"><span data-stu-id="f60e1-115">Azure region where the new resource group will be created.</span></span> <span data-ttu-id="f60e1-116">For our scenario, *centralus*.</span><span class="sxs-lookup"><span data-stu-id="f60e1-116">For our scenario, *centralus*.</span></span>
4. <span data-ttu-id="f60e1-117">Run the **`azure group deployment create`** cmdlet to deploy the new VNet by using the template and parameter files you downloaded and modified above.</span><span class="sxs-lookup"><span data-stu-id="f60e1-117">Run the **`azure group deployment create`** cmdlet to deploy the new VNet by using the template and parameter files you downloaded and modified above.</span></span> <span data-ttu-id="f60e1-118">The list shown after the output explains the parameters used.</span><span class="sxs-lookup"><span data-stu-id="f60e1-118">The list shown after the output explains the parameters used.</span></span>
   
        azure group deployment create -g TestRG -n TestVNetDeployment -f C:\ARM\azuredeploy.json -e C:\ARM\azuredeploy-parameters.json
   
    <span data-ttu-id="f60e1-119">Here is the expected output for the command above:</span><span class="sxs-lookup"><span data-stu-id="f60e1-119">Here is the expected output for the command above:</span></span>
   
        info:    Executing command group deployment create
        + Initializing template configurations and parameters
        + Creating a deployment
        info:    Created template deployment "TestVNetDeployment"
        + Registering providers
        info:    Registering provider microsoft.network
        + Waiting for deployment to complete
        data:    DeploymentName     : TestVNetDeployment
        data:    ResourceGroupName  : TestRG
        data:    ProvisioningState  : Succeeded
        data:    Timestamp          : 2015-08-14T21:56:11.152759Z
        data:    Mode               : Incremental
        data:    Name           Type    Value
        data:    -------------  ------  --------------
        data:    location       String  Central US
        data:    vnetName       String  TestVNet
        data:    addressPrefix  String  192.168.0.0/16
        data:    subnet1Prefix  String  192.168.1.0/24
        data:    subnet1Name    String  FrontEnd
        data:    subnet2Prefix  String  192.168.2.0/24
        data:    subnet2Name    String  BackEnd
        info:    group deployment create command OK
   
   * <span data-ttu-id="f60e1-120">**-g (or --resource-group)**.</span><span class="sxs-lookup"><span data-stu-id="f60e1-120">**-g (or --resource-group)**.</span></span> <span data-ttu-id="f60e1-121">Name of the resource group the new VNet will be created in.</span><span class="sxs-lookup"><span data-stu-id="f60e1-121">Name of the resource group the new VNet will be created in.</span></span>
   * <span data-ttu-id="f60e1-122">**-f (or --template-file)**.</span><span class="sxs-lookup"><span data-stu-id="f60e1-122">**-f (or --template-file)**.</span></span> <span data-ttu-id="f60e1-123">Path to your ARM template file.</span><span class="sxs-lookup"><span data-stu-id="f60e1-123">Path to your ARM template file.</span></span>
   * <span data-ttu-id="f60e1-124">**-e (or --parameters-file)**.</span><span class="sxs-lookup"><span data-stu-id="f60e1-124">**-e (or --parameters-file)**.</span></span> <span data-ttu-id="f60e1-125">Path to your ARM parameters file.</span><span class="sxs-lookup"><span data-stu-id="f60e1-125">Path to your ARM parameters file.</span></span>
5. <span data-ttu-id="f60e1-126">Run the **`azure network vnet show`** command to view the properties of the new vnet, as shown below.</span><span class="sxs-lookup"><span data-stu-id="f60e1-126">Run the **`azure network vnet show`** command to view the properties of the new vnet, as shown below.</span></span>
   
        azure network vnet show -g TestRG -n TestVNet
   
    <span data-ttu-id="f60e1-127">Here is the expected output for the command above:</span><span class="sxs-lookup"><span data-stu-id="f60e1-127">Here is the expected output for the command above:</span></span>
   
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

