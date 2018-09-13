<!--author=alkohli last changed: 08/04/17-->

#### <a name="to-install-an-update-from-the-azure-portal"></a><span data-ttu-id="1db8e-101">To install an update from the Azure portal</span><span class="sxs-lookup"><span data-stu-id="1db8e-101">To install an update from the Azure portal</span></span>

1. <span data-ttu-id="1db8e-102">On the StorSimple service page, select your device.</span><span class="sxs-lookup"><span data-stu-id="1db8e-102">On the StorSimple service page, select your device.</span></span>

    ![Select device](./media/storsimple-8000-install-update5-via-portal/update1.png)

2. <span data-ttu-id="1db8e-104">Navigate to **Device settings** > **Device updates**.</span><span class="sxs-lookup"><span data-stu-id="1db8e-104">Navigate to **Device settings** > **Device updates**.</span></span>

    ![Click Device updates](./media/storsimple-8000-install-update5-via-portal/update2.png)

2. <span data-ttu-id="1db8e-106">A notification appears if new updates are available.</span><span class="sxs-lookup"><span data-stu-id="1db8e-106">A notification appears if new updates are available.</span></span> <span data-ttu-id="1db8e-107">Alternatively, in the **Device updates** blade, click **Scan Updates**.</span><span class="sxs-lookup"><span data-stu-id="1db8e-107">Alternatively, in the **Device updates** blade, click **Scan Updates**.</span></span> <span data-ttu-id="1db8e-108">A job is created to scan for available updates.</span><span class="sxs-lookup"><span data-stu-id="1db8e-108">A job is created to scan for available updates.</span></span> <span data-ttu-id="1db8e-109">You are notified when the job completes successfully.</span><span class="sxs-lookup"><span data-stu-id="1db8e-109">You are notified when the job completes successfully.</span></span>

    ![Click Device updates](./media/storsimple-8000-install-update5-via-portal/update3.png)

3. <span data-ttu-id="1db8e-111">We recommend that you review the release notes before you apply an update on your device.</span><span class="sxs-lookup"><span data-stu-id="1db8e-111">We recommend that you review the release notes before you apply an update on your device.</span></span> <span data-ttu-id="1db8e-112">To apply updates, click **Install updates**.</span><span class="sxs-lookup"><span data-stu-id="1db8e-112">To apply updates, click **Install updates**.</span></span> <span data-ttu-id="1db8e-113">In the **Confirm regular updates** blade, review the prerequisites to complete before you apply updates.</span><span class="sxs-lookup"><span data-stu-id="1db8e-113">In the **Confirm regular updates** blade, review the prerequisites to complete before you apply updates.</span></span> <span data-ttu-id="1db8e-114">Select the checkbox to indicate that you are ready to update the device and then click **Install**.</span><span class="sxs-lookup"><span data-stu-id="1db8e-114">Select the checkbox to indicate that you are ready to update the device and then click **Install**.</span></span>

    ![Click Device updates](./media/storsimple-8000-install-update5-via-portal/update4.png)

6. <span data-ttu-id="1db8e-116">A set of prerequisite checks starts.</span><span class="sxs-lookup"><span data-stu-id="1db8e-116">A set of prerequisite checks starts.</span></span> <span data-ttu-id="1db8e-117">These checks include:</span><span class="sxs-lookup"><span data-stu-id="1db8e-117">These checks include:</span></span>
   
   * <span data-ttu-id="1db8e-118">**Controller health checks** to verify that both the device controllers are healthy and online.</span><span class="sxs-lookup"><span data-stu-id="1db8e-118">**Controller health checks** to verify that both the device controllers are healthy and online.</span></span>
   * <span data-ttu-id="1db8e-119">**Hardware component health checks** to verify that all the hardware components on your StorSimple device are healthy.</span><span class="sxs-lookup"><span data-stu-id="1db8e-119">**Hardware component health checks** to verify that all the hardware components on your StorSimple device are healthy.</span></span>
   * <span data-ttu-id="1db8e-120">**DATA 0 checks** to verify that DATA 0 is enabled on your device.</span><span class="sxs-lookup"><span data-stu-id="1db8e-120">**DATA 0 checks** to verify that DATA 0 is enabled on your device.</span></span> <span data-ttu-id="1db8e-121">If this interface is not enabled, you must enable it and then retry.</span><span class="sxs-lookup"><span data-stu-id="1db8e-121">If this interface is not enabled, you must enable it and then retry.</span></span>

    <span data-ttu-id="1db8e-122">The update is downloaded and installed only if all the checks are successfully completed.</span><span class="sxs-lookup"><span data-stu-id="1db8e-122">The update is downloaded and installed only if all the checks are successfully completed.</span></span> <span data-ttu-id="1db8e-123">You are notified when the checks are in progress.</span><span class="sxs-lookup"><span data-stu-id="1db8e-123">You are notified when the checks are in progress.</span></span> <span data-ttu-id="1db8e-124">If the prechecks fail, then you will be provided with the reasons for failure.</span><span class="sxs-lookup"><span data-stu-id="1db8e-124">If the prechecks fail, then you will be provided with the reasons for failure.</span></span> <span data-ttu-id="1db8e-125">Address those issues and then retry the operation.</span><span class="sxs-lookup"><span data-stu-id="1db8e-125">Address those issues and then retry the operation.</span></span> <span data-ttu-id="1db8e-126">You may need to contact Microsoft Support if you cannot address these issues by yourself.</span><span class="sxs-lookup"><span data-stu-id="1db8e-126">You may need to contact Microsoft Support if you cannot address these issues by yourself.</span></span>

7. <span data-ttu-id="1db8e-127">After the prechecks are successfully completed, an update job is created.</span><span class="sxs-lookup"><span data-stu-id="1db8e-127">After the prechecks are successfully completed, an update job is created.</span></span> <span data-ttu-id="1db8e-128">You are notified when the update job is successfully created.</span><span class="sxs-lookup"><span data-stu-id="1db8e-128">You are notified when the update job is successfully created.</span></span>
   
    ![Update job creation](./media/storsimple-8000-install-update5-via-portal/update6.png)
   
    <span data-ttu-id="1db8e-130">The update is then applied on your device.</span><span class="sxs-lookup"><span data-stu-id="1db8e-130">The update is then applied on your device.</span></span>

9. <span data-ttu-id="1db8e-131">The update takes a few hours to complete.</span><span class="sxs-lookup"><span data-stu-id="1db8e-131">The update takes a few hours to complete.</span></span> <span data-ttu-id="1db8e-132">Select the update job and click **Details** to view the details of the job at any time.</span><span class="sxs-lookup"><span data-stu-id="1db8e-132">Select the update job and click **Details** to view the details of the job at any time.</span></span>

    ![Update job creation](./media/storsimple-8000-install-update5-via-portal/update8.png)

     <span data-ttu-id="1db8e-134">You can also monitor the progress of the update job from **Device settings > Jobs**.</span><span class="sxs-lookup"><span data-stu-id="1db8e-134">You can also monitor the progress of the update job from **Device settings > Jobs**.</span></span> <span data-ttu-id="1db8e-135">On the **Jobs** blade, you can see the update progress.</span><span class="sxs-lookup"><span data-stu-id="1db8e-135">On the **Jobs** blade, you can see the update progress.</span></span>

     ![Update job creation](./media/storsimple-8000-install-update5-via-portal/update7.png)

10. <span data-ttu-id="1db8e-137">After the job is complete, navigate to the **Device settings > Device updates**.</span><span class="sxs-lookup"><span data-stu-id="1db8e-137">After the job is complete, navigate to the **Device settings > Device updates**.</span></span> <span data-ttu-id="1db8e-138">The software version should now be updated.</span><span class="sxs-lookup"><span data-stu-id="1db8e-138">The software version should now be updated.</span></span>

