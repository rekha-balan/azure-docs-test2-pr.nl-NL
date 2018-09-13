<!--author=SharS last changed: 9/17/15-->

#### <a name="to-mount-initialize-and-format-a-volume"></a><span data-ttu-id="8cb98-101">To mount, initialize, and format a volume</span><span class="sxs-lookup"><span data-stu-id="8cb98-101">To mount, initialize, and format a volume</span></span>
1. <span data-ttu-id="8cb98-102">Start the Microsoft iSCSI initiator.</span><span class="sxs-lookup"><span data-stu-id="8cb98-102">Start the Microsoft iSCSI initiator.</span></span>
2. <span data-ttu-id="8cb98-103">In the **iSCSI Initiator Properties** window, on the **Discovery** tab, click **Discover Portal**.</span><span class="sxs-lookup"><span data-stu-id="8cb98-103">In the **iSCSI Initiator Properties** window, on the **Discovery** tab, click **Discover Portal**.</span></span>
3. <span data-ttu-id="8cb98-104">In the **Discover Target Portal** dialog box, supply the IP address of your iSCSI-enabled network interface, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="8cb98-104">In the **Discover Target Portal** dialog box, supply the IP address of your iSCSI-enabled network interface, and then click **OK**.</span></span> 
4. <span data-ttu-id="8cb98-105">In the **iSCSI Initiator Properties** window, on the **Targets** tab, locate the **Discovered targets**.</span><span class="sxs-lookup"><span data-stu-id="8cb98-105">In the **iSCSI Initiator Properties** window, on the **Targets** tab, locate the **Discovered targets**.</span></span> <span data-ttu-id="8cb98-106">The device status should appear as **Inactive**.</span><span class="sxs-lookup"><span data-stu-id="8cb98-106">The device status should appear as **Inactive**.</span></span>
5. <span data-ttu-id="8cb98-107">Select the target device and then click **Connect**.</span><span class="sxs-lookup"><span data-stu-id="8cb98-107">Select the target device and then click **Connect**.</span></span> <span data-ttu-id="8cb98-108">After the device is connected, the status should change to **Connected**.</span><span class="sxs-lookup"><span data-stu-id="8cb98-108">After the device is connected, the status should change to **Connected**.</span></span> <span data-ttu-id="8cb98-109">(For more information about using the Microsoft iSCSI initiator, see [Installing and Configuring Microsoft iSCSI Initiator][1]).</span><span class="sxs-lookup"><span data-stu-id="8cb98-109">(For more information about using the Microsoft iSCSI initiator, see [Installing and Configuring Microsoft iSCSI Initiator][1]).</span></span>
6. <span data-ttu-id="8cb98-110">On your Windows host, press the Windows Logo key + X, and then click **Run**.</span><span class="sxs-lookup"><span data-stu-id="8cb98-110">On your Windows host, press the Windows Logo key + X, and then click **Run**.</span></span> 
7. <span data-ttu-id="8cb98-111">In the **Run** dialog box, type **Diskmgmt.msc**.</span><span class="sxs-lookup"><span data-stu-id="8cb98-111">In the **Run** dialog box, type **Diskmgmt.msc**.</span></span> <span data-ttu-id="8cb98-112">Click **OK**, and the **Disk Management** dialog box will appear.</span><span class="sxs-lookup"><span data-stu-id="8cb98-112">Click **OK**, and the **Disk Management** dialog box will appear.</span></span> <span data-ttu-id="8cb98-113">The right pane will show the volumes on your host.</span><span class="sxs-lookup"><span data-stu-id="8cb98-113">The right pane will show the volumes on your host.</span></span>
8. <span data-ttu-id="8cb98-114">In the **Disk Management** window, the mounted volumes will appear as shown in the following illustration.</span><span class="sxs-lookup"><span data-stu-id="8cb98-114">In the **Disk Management** window, the mounted volumes will appear as shown in the following illustration.</span></span> <span data-ttu-id="8cb98-115">Right-click the discovered volume (click the disk name), and then click **Online**.</span><span class="sxs-lookup"><span data-stu-id="8cb98-115">Right-click the discovered volume (click the disk name), and then click **Online**.</span></span>
   
     ![Initialize format volume](./media/storsimple-8000-mount-initialize-format-volume/step7initializeformatvolume.png) 
9. <span data-ttu-id="8cb98-117">Right-click the volume (click the disk name) again, and then click **Initialize**.</span><span class="sxs-lookup"><span data-stu-id="8cb98-117">Right-click the volume (click the disk name) again, and then click **Initialize**.</span></span>
10. <span data-ttu-id="8cb98-118">To format a simple volume, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8cb98-118">To format a simple volume, perform the following steps:</span></span>
    
    1. <span data-ttu-id="8cb98-119">Select the volume, right-click it (click the right area), and click **New Simple Volume**.</span><span class="sxs-lookup"><span data-stu-id="8cb98-119">Select the volume, right-click it (click the right area), and click **New Simple Volume**.</span></span>
    2. <span data-ttu-id="8cb98-120">In the New Simple Volume wizard, specify the volume size and drive letter and configure the volume as an NTFS file system.</span><span class="sxs-lookup"><span data-stu-id="8cb98-120">In the New Simple Volume wizard, specify the volume size and drive letter and configure the volume as an NTFS file system.</span></span>
    3. <span data-ttu-id="8cb98-121">Specify a 64 KB allocation unit size.</span><span class="sxs-lookup"><span data-stu-id="8cb98-121">Specify a 64 KB allocation unit size.</span></span> <span data-ttu-id="8cb98-122">This allocation unit size works well with the deduplication algorithms used in the StorSimple solution.</span><span class="sxs-lookup"><span data-stu-id="8cb98-122">This allocation unit size works well with the deduplication algorithms used in the StorSimple solution.</span></span>
    4. <span data-ttu-id="8cb98-123">Perform a quick format.</span><span class="sxs-lookup"><span data-stu-id="8cb98-123">Perform a quick format.</span></span>

<!--Link references-->
[1]: https://technet.microsoft.com/library/ee338480(WS.10).aspx