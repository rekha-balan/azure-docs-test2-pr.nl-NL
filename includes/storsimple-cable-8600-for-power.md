<!--author=alkohli last changed: 9/16/15-->


#### <a name="to-cable-your-device-for-power"></a><span data-ttu-id="5e97c-101">To cable your device for power</span><span class="sxs-lookup"><span data-stu-id="5e97c-101">To cable your device for power</span></span>
> [!NOTE]
> <span data-ttu-id="5e97c-102">Both enclosures on your StorSimple device include redundant PCMs.</span><span class="sxs-lookup"><span data-stu-id="5e97c-102">Both enclosures on your StorSimple device include redundant PCMs.</span></span> <span data-ttu-id="5e97c-103">For each enclosure, the PCMs must be installed and connected to different power sources to ensure high availability.</span><span class="sxs-lookup"><span data-stu-id="5e97c-103">For each enclosure, the PCMs must be installed and connected to different power sources to ensure high availability.</span></span>
> 
> 

1. <span data-ttu-id="5e97c-104">Make sure that the power switches on all the PCMs are in the OFF position.</span><span class="sxs-lookup"><span data-stu-id="5e97c-104">Make sure that the power switches on all the PCMs are in the OFF position.</span></span>
2. <span data-ttu-id="5e97c-105">On the primary enclosure, connect the power cords to both PCMs.</span><span class="sxs-lookup"><span data-stu-id="5e97c-105">On the primary enclosure, connect the power cords to both PCMs.</span></span> <span data-ttu-id="5e97c-106">The power cords are identified in red in the power cabling diagram, below.</span><span class="sxs-lookup"><span data-stu-id="5e97c-106">The power cords are identified in red in the power cabling diagram, below.</span></span>
3. <span data-ttu-id="5e97c-107">Make sure that the two PCMs on the primary enclosure use separate power sources.</span><span class="sxs-lookup"><span data-stu-id="5e97c-107">Make sure that the two PCMs on the primary enclosure use separate power sources.</span></span>
4. <span data-ttu-id="5e97c-108">Attach the power cords to the power on the rack distribution units as shown in the power cabling diagram.</span><span class="sxs-lookup"><span data-stu-id="5e97c-108">Attach the power cords to the power on the rack distribution units as shown in the power cabling diagram.</span></span>
5. <span data-ttu-id="5e97c-109">Repeat steps 2 through 4 for the EBOD enclosure.</span><span class="sxs-lookup"><span data-stu-id="5e97c-109">Repeat steps 2 through 4 for the EBOD enclosure.</span></span>
6. <span data-ttu-id="5e97c-110">Turn on the EBOD enclosure by flipping the power switch on each PCM to the ON position.</span><span class="sxs-lookup"><span data-stu-id="5e97c-110">Turn on the EBOD enclosure by flipping the power switch on each PCM to the ON position.</span></span>
7. <span data-ttu-id="5e97c-111">Verify that the EBOD enclosure is turned on by checking that the green LEDs on the back of the EBOD controller are turned ON.</span><span class="sxs-lookup"><span data-stu-id="5e97c-111">Verify that the EBOD enclosure is turned on by checking that the green LEDs on the back of the EBOD controller are turned ON.</span></span>
8. <span data-ttu-id="5e97c-112">Turn on the primary enclosure by flipping each PCM switch to the ON position.</span><span class="sxs-lookup"><span data-stu-id="5e97c-112">Turn on the primary enclosure by flipping each PCM switch to the ON position.</span></span>
9. <span data-ttu-id="5e97c-113">Verify that the system is on by ensuring the device controller LEDs have turned ON.</span><span class="sxs-lookup"><span data-stu-id="5e97c-113">Verify that the system is on by ensuring the device controller LEDs have turned ON.</span></span>
10. <span data-ttu-id="5e97c-114">Make sure that the connection between the EBOD controller and the device controller is active by verifying that the four LEDs next to the SAS port on the EBOD controller are green.</span><span class="sxs-lookup"><span data-stu-id="5e97c-114">Make sure that the connection between the EBOD controller and the device controller is active by verifying that the four LEDs next to the SAS port on the EBOD controller are green.</span></span>
    
    > [!IMPORTANT]
    > <span data-ttu-id="5e97c-115">To ensure high availability for your system, we recommend that you strictly adhere to the power cabling scheme shown in the following diagram.</span><span class="sxs-lookup"><span data-stu-id="5e97c-115">To ensure high availability for your system, we recommend that you strictly adhere to the power cabling scheme shown in the following diagram.</span></span>
    > 
    > 
    
    ![Cable your 4U device for power](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/storsimple-cable-8600-for-power/HCSCableYour4UDeviceforPower.png)
    
    <span data-ttu-id="5e97c-117">**Power cabling**</span><span class="sxs-lookup"><span data-stu-id="5e97c-117">**Power cabling**</span></span>
    
    | <span data-ttu-id="5e97c-118">Label</span><span class="sxs-lookup"><span data-stu-id="5e97c-118">Label</span></span> | <span data-ttu-id="5e97c-119">Description</span><span class="sxs-lookup"><span data-stu-id="5e97c-119">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="5e97c-120">1</span><span class="sxs-lookup"><span data-stu-id="5e97c-120">1</span></span> |<span data-ttu-id="5e97c-121">Primary enclosure</span><span class="sxs-lookup"><span data-stu-id="5e97c-121">Primary enclosure</span></span> |
    | <span data-ttu-id="5e97c-122">2</span><span class="sxs-lookup"><span data-stu-id="5e97c-122">2</span></span> |<span data-ttu-id="5e97c-123">PCM 0</span><span class="sxs-lookup"><span data-stu-id="5e97c-123">PCM 0</span></span> |
    | <span data-ttu-id="5e97c-124">3</span><span class="sxs-lookup"><span data-stu-id="5e97c-124">3</span></span> |<span data-ttu-id="5e97c-125">PCM 1</span><span class="sxs-lookup"><span data-stu-id="5e97c-125">PCM 1</span></span> |
    | <span data-ttu-id="5e97c-126">4</span><span class="sxs-lookup"><span data-stu-id="5e97c-126">4</span></span> |<span data-ttu-id="5e97c-127">Controller 0</span><span class="sxs-lookup"><span data-stu-id="5e97c-127">Controller 0</span></span> |
    | <span data-ttu-id="5e97c-128">5</span><span class="sxs-lookup"><span data-stu-id="5e97c-128">5</span></span> |<span data-ttu-id="5e97c-129">Controller 1</span><span class="sxs-lookup"><span data-stu-id="5e97c-129">Controller 1</span></span> |
    | <span data-ttu-id="5e97c-130">6</span><span class="sxs-lookup"><span data-stu-id="5e97c-130">6</span></span> |<span data-ttu-id="5e97c-131">EBOD controller 0</span><span class="sxs-lookup"><span data-stu-id="5e97c-131">EBOD controller 0</span></span> |
    | <span data-ttu-id="5e97c-132">7</span><span class="sxs-lookup"><span data-stu-id="5e97c-132">7</span></span> |<span data-ttu-id="5e97c-133">EBOD controller 1</span><span class="sxs-lookup"><span data-stu-id="5e97c-133">EBOD controller 1</span></span> |
    | <span data-ttu-id="5e97c-134">8</span><span class="sxs-lookup"><span data-stu-id="5e97c-134">8</span></span> |<span data-ttu-id="5e97c-135">EBOD enclosure</span><span class="sxs-lookup"><span data-stu-id="5e97c-135">EBOD enclosure</span></span> |
    | <span data-ttu-id="5e97c-136">9</span><span class="sxs-lookup"><span data-stu-id="5e97c-136">9</span></span> |<span data-ttu-id="5e97c-137">PDUs</span><span class="sxs-lookup"><span data-stu-id="5e97c-137">PDUs</span></span> |


