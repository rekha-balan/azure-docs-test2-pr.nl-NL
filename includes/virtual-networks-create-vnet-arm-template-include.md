## <a name="download-and-understand-the-arm-template"></a><span data-ttu-id="01dc6-101">Download and understand the ARM template</span><span class="sxs-lookup"><span data-stu-id="01dc6-101">Download and understand the ARM template</span></span>
<span data-ttu-id="01dc6-102">You can download the existing ARM template for creating a VNet and two subnets from github, make any changes you might want, and reuse it.</span><span class="sxs-lookup"><span data-stu-id="01dc6-102">You can download the existing ARM template for creating a VNet and two subnets from github, make any changes you might want, and reuse it.</span></span> <span data-ttu-id="01dc6-103">To do so, follow the steps below.</span><span class="sxs-lookup"><span data-stu-id="01dc6-103">To do so, follow the steps below.</span></span>

1. <span data-ttu-id="01dc6-104">Navigate to [the sample template page](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).</span><span class="sxs-lookup"><span data-stu-id="01dc6-104">Navigate to [the sample template page](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).</span></span>
2. <span data-ttu-id="01dc6-105">Click **azuredeploy.json**, and then click **RAW**.</span><span class="sxs-lookup"><span data-stu-id="01dc6-105">Click **azuredeploy.json**, and then click **RAW**.</span></span>
3. <span data-ttu-id="01dc6-106">Save the file to a a local folder on your computer.</span><span class="sxs-lookup"><span data-stu-id="01dc6-106">Save the file to a a local folder on your computer.</span></span>
4. <span data-ttu-id="01dc6-107">If you are familiar with ARM templates, skip to step 7.</span><span class="sxs-lookup"><span data-stu-id="01dc6-107">If you are familiar with ARM templates, skip to step 7.</span></span>
5. <span data-ttu-id="01dc6-108">Open the file you just saved and look at the contents under **parameters** in line 5.</span><span class="sxs-lookup"><span data-stu-id="01dc6-108">Open the file you just saved and look at the contents under **parameters** in line 5.</span></span> <span data-ttu-id="01dc6-109">ARM template parameters provide a placeholder for values that can be filled out during deployment.</span><span class="sxs-lookup"><span data-stu-id="01dc6-109">ARM template parameters provide a placeholder for values that can be filled out during deployment.</span></span>
   
   | <span data-ttu-id="01dc6-110">Parameter</span><span class="sxs-lookup"><span data-stu-id="01dc6-110">Parameter</span></span> | <span data-ttu-id="01dc6-111">Description</span><span class="sxs-lookup"><span data-stu-id="01dc6-111">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="01dc6-112">**location**</span><span class="sxs-lookup"><span data-stu-id="01dc6-112">**location**</span></span> |<span data-ttu-id="01dc6-113">Azure region where the VNet will be created</span><span class="sxs-lookup"><span data-stu-id="01dc6-113">Azure region where the VNet will be created</span></span> |
   | <span data-ttu-id="01dc6-114">**vnetName**</span><span class="sxs-lookup"><span data-stu-id="01dc6-114">**vnetName**</span></span> |<span data-ttu-id="01dc6-115">Name for the new VNet</span><span class="sxs-lookup"><span data-stu-id="01dc6-115">Name for the new VNet</span></span> |
   | <span data-ttu-id="01dc6-116">**addressPrefix**</span><span class="sxs-lookup"><span data-stu-id="01dc6-116">**addressPrefix**</span></span> |<span data-ttu-id="01dc6-117">Address space for the VNet, in CIDR format</span><span class="sxs-lookup"><span data-stu-id="01dc6-117">Address space for the VNet, in CIDR format</span></span> |
   | <span data-ttu-id="01dc6-118">**subnet1Name**</span><span class="sxs-lookup"><span data-stu-id="01dc6-118">**subnet1Name**</span></span> |<span data-ttu-id="01dc6-119">Name for the first VNet</span><span class="sxs-lookup"><span data-stu-id="01dc6-119">Name for the first VNet</span></span> |
   | <span data-ttu-id="01dc6-120">**subnet1Prefix**</span><span class="sxs-lookup"><span data-stu-id="01dc6-120">**subnet1Prefix**</span></span> |<span data-ttu-id="01dc6-121">CIDR block for the first subnet</span><span class="sxs-lookup"><span data-stu-id="01dc6-121">CIDR block for the first subnet</span></span> |
   | <span data-ttu-id="01dc6-122">**subnet2Name**</span><span class="sxs-lookup"><span data-stu-id="01dc6-122">**subnet2Name**</span></span> |<span data-ttu-id="01dc6-123">Name for the second VNet</span><span class="sxs-lookup"><span data-stu-id="01dc6-123">Name for the second VNet</span></span> |
   | <span data-ttu-id="01dc6-124">**subnet2Prefix**</span><span class="sxs-lookup"><span data-stu-id="01dc6-124">**subnet2Prefix**</span></span> |<span data-ttu-id="01dc6-125">CIDR block for the second subnet</span><span class="sxs-lookup"><span data-stu-id="01dc6-125">CIDR block for the second subnet</span></span> |
   
   > [!IMPORTANT]
   > <span data-ttu-id="01dc6-126">ARM templates maintained in github can change over time.</span><span class="sxs-lookup"><span data-stu-id="01dc6-126">ARM templates maintained in github can change over time.</span></span> <span data-ttu-id="01dc6-127">Make sure you check the template before using it.</span><span class="sxs-lookup"><span data-stu-id="01dc6-127">Make sure you check the template before using it.</span></span>
   > 
   > 
6. <span data-ttu-id="01dc6-128">Check the content under **resources** and notice the following:</span><span class="sxs-lookup"><span data-stu-id="01dc6-128">Check the content under **resources** and notice the following:</span></span>
   
   * <span data-ttu-id="01dc6-129">**type**.</span><span class="sxs-lookup"><span data-stu-id="01dc6-129">**type**.</span></span> <span data-ttu-id="01dc6-130">Type of resource being created by the template.</span><span class="sxs-lookup"><span data-stu-id="01dc6-130">Type of resource being created by the template.</span></span> <span data-ttu-id="01dc6-131">In this case, **Microsoft.Network/virtualNetworks**, which represent a VNet.</span><span class="sxs-lookup"><span data-stu-id="01dc6-131">In this case, **Microsoft.Network/virtualNetworks**, which represent a VNet.</span></span>
   * <span data-ttu-id="01dc6-132">**name**.</span><span class="sxs-lookup"><span data-stu-id="01dc6-132">**name**.</span></span> <span data-ttu-id="01dc6-133">Name for the resource.</span><span class="sxs-lookup"><span data-stu-id="01dc6-133">Name for the resource.</span></span> <span data-ttu-id="01dc6-134">Notice the use of **[parameters('vnetName')]**, which means the name will provided as input by the user or a parameter file during deployment.</span><span class="sxs-lookup"><span data-stu-id="01dc6-134">Notice the use of **[parameters('vnetName')]**, which means the name will provided as input by the user or a parameter file during deployment.</span></span>
   * <span data-ttu-id="01dc6-135">**properties**.</span><span class="sxs-lookup"><span data-stu-id="01dc6-135">**properties**.</span></span> <span data-ttu-id="01dc6-136">List of properties for the resource.</span><span class="sxs-lookup"><span data-stu-id="01dc6-136">List of properties for the resource.</span></span> <span data-ttu-id="01dc6-137">This template uses the address space and subnet properties during VNet creation.</span><span class="sxs-lookup"><span data-stu-id="01dc6-137">This template uses the address space and subnet properties during VNet creation.</span></span>
7. <span data-ttu-id="01dc6-138">Navigate back to [the sample template page](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).</span><span class="sxs-lookup"><span data-stu-id="01dc6-138">Navigate back to [the sample template page](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).</span></span>
8. <span data-ttu-id="01dc6-139">Click **azuredeploy-paremeters.json**, and then click **RAW**.</span><span class="sxs-lookup"><span data-stu-id="01dc6-139">Click **azuredeploy-paremeters.json**, and then click **RAW**.</span></span>
9. <span data-ttu-id="01dc6-140">Save the file to a a local folder on your computer.</span><span class="sxs-lookup"><span data-stu-id="01dc6-140">Save the file to a a local folder on your computer.</span></span>
10. <span data-ttu-id="01dc6-141">Open the file you just saved and edit the values for the parameters.</span><span class="sxs-lookup"><span data-stu-id="01dc6-141">Open the file you just saved and edit the values for the parameters.</span></span> <span data-ttu-id="01dc6-142">Use the values below to deploy the VNet described in our scenario.</span><span class="sxs-lookup"><span data-stu-id="01dc6-142">Use the values below to deploy the VNet described in our scenario.</span></span>
    
        {
          "location": {
            "value": "Central US"
          },
          "vnetName": {
              "value": "TestVNet"
          },
          "addressPrefix": {
              "value": "192.168.0.0/16"
          },
          "subnet1Name": {
              "value": "FrontEnd"
          },
          "subnet1Prefix": {
            "value": "192.168.1.0/24"
          },
          "subnet2Name": {
              "value": "BackEnd"
          },
          "subnet2Prefix": {
              "value": "192.168.2.0/24"
          }
        }
11. <span data-ttu-id="01dc6-143">Save the file.</span><span class="sxs-lookup"><span data-stu-id="01dc6-143">Save the file.</span></span>

