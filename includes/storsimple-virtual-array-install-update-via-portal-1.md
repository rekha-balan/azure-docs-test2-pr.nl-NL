<!--author=alkohli last changed: 11/02/17 -->

#### <a name="to-install-updates-via-the-azure-portal"></a><span data-ttu-id="d1397-101">To install updates via the Azure portal</span><span class="sxs-lookup"><span data-stu-id="d1397-101">To install updates via the Azure portal</span></span>

1. <span data-ttu-id="d1397-102">Go to your StorSimple Device Manager and select **Devices**.</span><span class="sxs-lookup"><span data-stu-id="d1397-102">Go to your StorSimple Device Manager and select **Devices**.</span></span> <span data-ttu-id="d1397-103">From the list of devices connected to your service, select and click the device you want to update.</span><span class="sxs-lookup"><span data-stu-id="d1397-103">From the list of devices connected to your service, select and click the device you want to update.</span></span>

    ![update device](../includes/media/storsimple-virtual-array-install-update-via-portal-04/azupdate1m.png) 

2. <span data-ttu-id="d1397-105">In the **Settings** blade, click **Device updates**.</span><span class="sxs-lookup"><span data-stu-id="d1397-105">In the **Settings** blade, click **Device updates**.</span></span>

    ![update device](../includes/media/storsimple-virtual-array-install-update-via-portal-04/azupdate2m.png)  

3. <span data-ttu-id="d1397-107">You see a message if the software updates are available.</span><span class="sxs-lookup"><span data-stu-id="d1397-107">You see a message if the software updates are available.</span></span> <span data-ttu-id="d1397-108">To check for updates, you can also click **Scan**.</span><span class="sxs-lookup"><span data-stu-id="d1397-108">To check for updates, you can also click **Scan**.</span></span> <span data-ttu-id="d1397-109">Make a note of the software version you are running.</span><span class="sxs-lookup"><span data-stu-id="d1397-109">Make a note of the software version you are running.</span></span> 

    ![update device](../includes/media/storsimple-virtual-array-install-update-via-portal-1/azupdate3m1.png)

    <span data-ttu-id="d1397-111">You are notified when the scan starts and completes successfully.</span><span class="sxs-lookup"><span data-stu-id="d1397-111">You are notified when the scan starts and completes successfully.</span></span>

    ![update device](../includes/media/storsimple-virtual-array-install-update-via-portal-1/azupdate5m.png)

4. <span data-ttu-id="d1397-113">Once the updates are scanned, click **Download updates**.</span><span class="sxs-lookup"><span data-stu-id="d1397-113">Once the updates are scanned, click **Download updates**.</span></span>

    ![update device](../includes/media/storsimple-virtual-array-install-update-via-portal-1/azupdate6m.png)

5. <span data-ttu-id="d1397-115">In the **New updates** blade, review the release notes.</span><span class="sxs-lookup"><span data-stu-id="d1397-115">In the **New updates** blade, review the release notes.</span></span> <span data-ttu-id="d1397-116">Also note that after the updates are downloaded, you need to confirm the installation.</span><span class="sxs-lookup"><span data-stu-id="d1397-116">Also note that after the updates are downloaded, you need to confirm the installation.</span></span> <span data-ttu-id="d1397-117">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="d1397-117">Click **OK**.</span></span>

    ![update device](../includes/media/storsimple-virtual-array-install-update-via-portal-1/azupdate7m.png)

6. <span data-ttu-id="d1397-119">You are notified when the upload starts and completes successfully.</span><span class="sxs-lookup"><span data-stu-id="d1397-119">You are notified when the upload starts and completes successfully.</span></span>

     ![update device](../includes/media/storsimple-virtual-array-install-update-via-portal-1/azupdate8m.png)

5. <span data-ttu-id="d1397-121">In the **Device updates** blade, click **Install**.</span><span class="sxs-lookup"><span data-stu-id="d1397-121">In the **Device updates** blade, click **Install**.</span></span>

     ![update device](../includes/media/storsimple-virtual-array-install-update-via-portal-1/azupdate11m1.png)

6. <span data-ttu-id="d1397-123">In the **New updates** blade, you are warned that the update is disruptive.</span><span class="sxs-lookup"><span data-stu-id="d1397-123">In the **New updates** blade, you are warned that the update is disruptive.</span></span> <span data-ttu-id="d1397-124">As virtual array is a single node device, the device restarts after it is updated.</span><span class="sxs-lookup"><span data-stu-id="d1397-124">As virtual array is a single node device, the device restarts after it is updated.</span></span> <span data-ttu-id="d1397-125">This disrupts any IO in progress.</span><span class="sxs-lookup"><span data-stu-id="d1397-125">This disrupts any IO in progress.</span></span> <span data-ttu-id="d1397-126">Click **OK** to install the updates.</span><span class="sxs-lookup"><span data-stu-id="d1397-126">Click **OK** to install the updates.</span></span>

    ![update device](../includes/media/storsimple-virtual-array-install-update-via-portal-1/azupdate12m.png)

7. <span data-ttu-id="d1397-128">You are notified when the install job starts.</span><span class="sxs-lookup"><span data-stu-id="d1397-128">You are notified when the install job starts.</span></span>

    ![update device](../includes/media/storsimple-virtual-array-install-update-via-portal-1/azupdate13m.png)

8.  <span data-ttu-id="d1397-130">After the install job completes successfully, click **View Job** link in the **Device updates** blade to monitor the installation.</span><span class="sxs-lookup"><span data-stu-id="d1397-130">After the install job completes successfully, click **View Job** link in the **Device updates** blade to monitor the installation.</span></span> 

    ![update device](../includes/media/storsimple-virtual-array-install-update-via-portal-1/azupdate15m1.png)

    <span data-ttu-id="d1397-132">This action takes you to the **Install Updates** blade.</span><span class="sxs-lookup"><span data-stu-id="d1397-132">This action takes you to the **Install Updates** blade.</span></span> <span data-ttu-id="d1397-133">You can view detailed information about the job here.</span><span class="sxs-lookup"><span data-stu-id="d1397-133">You can view detailed information about the job here.</span></span>

    ![update device](../includes/media/storsimple-virtual-array-install-update-via-portal-1/azupdate16m1.png)

9. <span data-ttu-id="d1397-135">If you started with a virtual array running software version Update 0.6 (10.0.10293.0), you are now running Update 1 and are done.</span><span class="sxs-lookup"><span data-stu-id="d1397-135">If you started with a virtual array running software version Update 0.6 (10.0.10293.0), you are now running Update 1 and are done.</span></span> <span data-ttu-id="d1397-136">You can skip the remaining steps.</span><span class="sxs-lookup"><span data-stu-id="d1397-136">You can skip the remaining steps.</span></span> <span data-ttu-id="d1397-137">If you started with a virtual array running a software version prior to Update 0.6 (10.0.10293.0), you are now updated to Update 0.6.</span><span class="sxs-lookup"><span data-stu-id="d1397-137">If you started with a virtual array running a software version prior to Update 0.6 (10.0.10293.0), you are now updated to Update 0.6.</span></span> <span data-ttu-id="d1397-138">You see another message indicating that updates are available.</span><span class="sxs-lookup"><span data-stu-id="d1397-138">You see another message indicating that updates are available.</span></span> <span data-ttu-id="d1397-139">Repeat steps 4-8 to install Update 1.</span><span class="sxs-lookup"><span data-stu-id="d1397-139">Repeat steps 4-8 to install Update 1.</span></span>

    ![update device](../includes/media/storsimple-virtual-array-install-update-via-portal-1/azupdate17.png)

