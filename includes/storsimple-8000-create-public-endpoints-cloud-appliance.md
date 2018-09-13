#### <a name="to-create-public-endpoints-on-the-cloud-appliance"></a><span data-ttu-id="1e7a5-101">To create public endpoints on the cloud appliance</span><span class="sxs-lookup"><span data-stu-id="1e7a5-101">To create public endpoints on the cloud appliance</span></span>

1. <span data-ttu-id="1e7a5-102">Sign in to the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-102">Sign in to the Azure portal.</span></span>
2. <span data-ttu-id="1e7a5-103">Go to **Virtual Machines**, and then select and click the virtual machine that is being used as your cloud appliance.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-103">Go to **Virtual Machines**, and then select and click the virtual machine that is being used as your cloud appliance.</span></span>
    
3. <span data-ttu-id="1e7a5-104">You need to create a network security group (NSG) rule to control the flow of traffic in and out of your virtual machine.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-104">You need to create a network security group (NSG) rule to control the flow of traffic in and out of your virtual machine.</span></span> <span data-ttu-id="1e7a5-105">Perform the following steps to create an NSG rule.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-105">Perform the following steps to create an NSG rule.</span></span>
    1. <span data-ttu-id="1e7a5-106">Select **Network security group**.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-106">Select **Network security group**.</span></span>
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt1.png)

    2. <span data-ttu-id="1e7a5-107">Click the default network security group that is presented.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-107">Click the default network security group that is presented.</span></span>
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt2.png)

    3. <span data-ttu-id="1e7a5-108">Select **Inbound security rules**.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-108">Select **Inbound security rules**.</span></span>
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt3.png)

    4. <span data-ttu-id="1e7a5-109">Click **+ Add** to create an inbound security rule.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-109">Click **+ Add** to create an inbound security rule.</span></span>
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt4.png)

        <span data-ttu-id="1e7a5-110">In the Add inbound security rule blade:</span><span class="sxs-lookup"><span data-stu-id="1e7a5-110">In the Add inbound security rule blade:</span></span>

        1. <span data-ttu-id="1e7a5-111">For the **Name**, type the following name for the endpoint: WinRMHttps.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-111">For the **Name**, type the following name for the endpoint: WinRMHttps.</span></span>
        
        2. <span data-ttu-id="1e7a5-112">For the **Priority**, select a number lesser than 1000 (which is the priority for the default rule).</span><span class="sxs-lookup"><span data-stu-id="1e7a5-112">For the **Priority**, select a number lesser than 1000 (which is the priority for the default rule).</span></span> <span data-ttu-id="1e7a5-113">Higher the value, lower the priority.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-113">Higher the value, lower the priority.</span></span>

        3. <span data-ttu-id="1e7a5-114">Set the **Source** to **Any**.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-114">Set the **Source** to **Any**.</span></span>

        4. <span data-ttu-id="1e7a5-115">For the **Service**, select **WinRM**.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-115">For the **Service**, select **WinRM**.</span></span> <span data-ttu-id="1e7a5-116">The **Protocol** is automatically set to **TCP** and the **Port range** is set to **5986**.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-116">The **Protocol** is automatically set to **TCP** and the **Port range** is set to **5986**.</span></span>

        5. <span data-ttu-id="1e7a5-117">Click **OK** to create the rule.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-117">Click **OK** to create the rule.</span></span>

            ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt5.png)

4. <span data-ttu-id="1e7a5-118">Your final step is to associate your network security group with a subnet or a specific network interface.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-118">Your final step is to associate your network security group with a subnet or a specific network interface.</span></span> <span data-ttu-id="1e7a5-119">Perform the following steps to associate your network security group with a subnet.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-119">Perform the following steps to associate your network security group with a subnet.</span></span>
    1. <span data-ttu-id="1e7a5-120">Go to **Subnets**.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-120">Go to **Subnets**.</span></span>
    2. <span data-ttu-id="1e7a5-121">Click **+ Associate**.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-121">Click **+ Associate**.</span></span>
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt7.png)

    3. <span data-ttu-id="1e7a5-122">Select your virtual network, and then select the appropriate subnet.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-122">Select your virtual network, and then select the appropriate subnet.</span></span>
    4. <span data-ttu-id="1e7a5-123">Click **OK** to create the rule.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-123">Click **OK** to create the rule.</span></span>

        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt11.png)

<span data-ttu-id="1e7a5-124">After the rule is created, you can view its details to determine the Public Virtual IP (VIP) address.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-124">After the rule is created, you can view its details to determine the Public Virtual IP (VIP) address.</span></span> <span data-ttu-id="1e7a5-125">Record this address.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-125">Record this address.</span></span>


