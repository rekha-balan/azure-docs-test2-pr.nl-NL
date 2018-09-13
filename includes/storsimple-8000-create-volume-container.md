<!--author=alkohli last changed: 06/22/17-->

#### <a name="to-create-a-volume-container"></a><span data-ttu-id="ddcbb-101">To create a volume container</span><span class="sxs-lookup"><span data-stu-id="ddcbb-101">To create a volume container</span></span>
1. <span data-ttu-id="ddcbb-102">Go to your StorSimple Device Manager service and click **Devices**.</span><span class="sxs-lookup"><span data-stu-id="ddcbb-102">Go to your StorSimple Device Manager service and click **Devices**.</span></span> <span data-ttu-id="ddcbb-103">From the tabular listing of the devices, select and click a device.</span><span class="sxs-lookup"><span data-stu-id="ddcbb-103">From the tabular listing of the devices, select and click a device.</span></span> 

    ![Volume container blade](./media/storsimple-8000-create-volume-container/createvolumecontainer1.png)

2. <span data-ttu-id="ddcbb-105">In the device dashboard, click **+ Add volume container**</span><span class="sxs-lookup"><span data-stu-id="ddcbb-105">In the device dashboard, click **+ Add volume container**</span></span>

    ![Volume container blade](./media/storsimple-8000-create-volume-container/createvolumecontainer2.png)

3. <span data-ttu-id="ddcbb-107">In the **Add volume container** blade:</span><span class="sxs-lookup"><span data-stu-id="ddcbb-107">In the **Add volume container** blade:</span></span>
   
   1. <span data-ttu-id="ddcbb-108">The device is automatically selected.</span><span class="sxs-lookup"><span data-stu-id="ddcbb-108">The device is automatically selected.</span></span>
   2. <span data-ttu-id="ddcbb-109">Supply a **Name** for your volume container.</span><span class="sxs-lookup"><span data-stu-id="ddcbb-109">Supply a **Name** for your volume container.</span></span> <span data-ttu-id="ddcbb-110">The name must be 3 to 32 characters long.</span><span class="sxs-lookup"><span data-stu-id="ddcbb-110">The name must be 3 to 32 characters long.</span></span> <span data-ttu-id="ddcbb-111">You cannot rename a volume container once it is created.</span><span class="sxs-lookup"><span data-stu-id="ddcbb-111">You cannot rename a volume container once it is created.</span></span>
   3. <span data-ttu-id="ddcbb-112">Select **Enable Cloud Storage Encryption** to enable encryption of the data sent from the device to the cloud.</span><span class="sxs-lookup"><span data-stu-id="ddcbb-112">Select **Enable Cloud Storage Encryption** to enable encryption of the data sent from the device to the cloud.</span></span>
   4. <span data-ttu-id="ddcbb-113">Provide and confirm a **Cloud Storage Encryption Key** that is 8 to 32 characters long.</span><span class="sxs-lookup"><span data-stu-id="ddcbb-113">Provide and confirm a **Cloud Storage Encryption Key** that is 8 to 32 characters long.</span></span> <span data-ttu-id="ddcbb-114">This key is used by the device to access encrypted data.</span><span class="sxs-lookup"><span data-stu-id="ddcbb-114">This key is used by the device to access encrypted data.</span></span>
   5. <span data-ttu-id="ddcbb-115">Select a **Storage Account** to associate with this volume container.</span><span class="sxs-lookup"><span data-stu-id="ddcbb-115">Select a **Storage Account** to associate with this volume container.</span></span> <span data-ttu-id="ddcbb-116">You can choose an existing storage account or the default account that is generated at the time of service creation.</span><span class="sxs-lookup"><span data-stu-id="ddcbb-116">You can choose an existing storage account or the default account that is generated at the time of service creation.</span></span> <span data-ttu-id="ddcbb-117">You can also use the **Add new** option to specify a storage account that is not linked to this service subscription.</span><span class="sxs-lookup"><span data-stu-id="ddcbb-117">You can also use the **Add new** option to specify a storage account that is not linked to this service subscription.</span></span>
   6. <span data-ttu-id="ddcbb-118">Select **Unlimited** in the **Specify bandwidth** drop-down list if you wish to consume all the available bandwidth.</span><span class="sxs-lookup"><span data-stu-id="ddcbb-118">Select **Unlimited** in the **Specify bandwidth** drop-down list if you wish to consume all the available bandwidth.</span></span> <span data-ttu-id="ddcbb-119">You can also set this option to **Custom** to employ bandwidth controls, and specify a value between 1 Mbps and 1,000 Mbps.</span><span class="sxs-lookup"><span data-stu-id="ddcbb-119">You can also set this option to **Custom** to employ bandwidth controls, and specify a value between 1 Mbps and 1,000 Mbps.</span></span>
      <span data-ttu-id="ddcbb-120">If you have your bandwidth usage information available, you may be able to allocate bandwidth based on a schedule by specifying **Select a bandwidth template**.</span><span class="sxs-lookup"><span data-stu-id="ddcbb-120">If you have your bandwidth usage information available, you may be able to allocate bandwidth based on a schedule by specifying **Select a bandwidth template**.</span></span> <span data-ttu-id="ddcbb-121">For a step-by-step procedure, go to [Add a bandwidth template](../articles/storsimple/storsimple-8000-manage-bandwidth-templates.md#add-a-bandwidth-template).</span><span class="sxs-lookup"><span data-stu-id="ddcbb-121">For a step-by-step procedure, go to [Add a bandwidth template](../articles/storsimple/storsimple-8000-manage-bandwidth-templates.md#add-a-bandwidth-template).</span></span>

      ![Volume container blade](./media/storsimple-8000-create-volume-container/createvolumecontainer6b.png)
   7. <span data-ttu-id="ddcbb-123">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="ddcbb-123">Click **Create**.</span></span>

        ![Volume container blade](./media/storsimple-8000-create-volume-container/createvolumecontainer6.png)
   
       <span data-ttu-id="ddcbb-125">You are notified when the volume container is successfully created.</span><span class="sxs-lookup"><span data-stu-id="ddcbb-125">You are notified when the volume container is successfully created.</span></span>

       ![Volume container creation notification](./media/storsimple-8000-create-volume-container/createvolumecontainer8.png)

   <span data-ttu-id="ddcbb-127">The newly created volume container is listed in the list of volume containers for your device.</span><span class="sxs-lookup"><span data-stu-id="ddcbb-127">The newly created volume container is listed in the list of volume containers for your device.</span></span>

   ![Add volume container blade](./media/storsimple-8000-create-volume-container/createvolumecontainer9.png)


