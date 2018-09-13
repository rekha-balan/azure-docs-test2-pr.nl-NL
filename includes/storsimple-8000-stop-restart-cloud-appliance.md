#### <a name="to-stop-and-start-a-cloud-appliance"></a><span data-ttu-id="dbac5-101">To stop and start a cloud appliance</span><span class="sxs-lookup"><span data-stu-id="dbac5-101">To stop and start a cloud appliance</span></span>

1. <span data-ttu-id="dbac5-102">To stop a cloud appliance, go to the VM for your cloud appliance.</span><span class="sxs-lookup"><span data-stu-id="dbac5-102">To stop a cloud appliance, go to the VM for your cloud appliance.</span></span>
    <span data-ttu-id="dbac5-103">![StorSimple Cloud Appliance Virtual Machine](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart1.png)</span><span class="sxs-lookup"><span data-stu-id="dbac5-103">![StorSimple Cloud Appliance Virtual Machine](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart1.png)</span></span>

2. <span data-ttu-id="dbac5-104">From the command bar, click **Stop**.</span><span class="sxs-lookup"><span data-stu-id="dbac5-104">From the command bar, click **Stop**.</span></span>

    ![StorSimple Cloud Appliance Virtual Machine](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart2.png)

3. <span data-ttu-id="dbac5-106">When prompted for confirmation, click **Yes**.</span><span class="sxs-lookup"><span data-stu-id="dbac5-106">When prompted for confirmation, click **Yes**.</span></span>

    ![StorSimple Cloud Appliance Virtual Machine](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart3.png)

4. <span data-ttu-id="dbac5-108">When you stop a VM, it gets deallocated.</span><span class="sxs-lookup"><span data-stu-id="dbac5-108">When you stop a VM, it gets deallocated.</span></span> <span data-ttu-id="dbac5-109">While the cloud appliance is stopping, its status is **Deallocating**.</span><span class="sxs-lookup"><span data-stu-id="dbac5-109">While the cloud appliance is stopping, its status is **Deallocating**.</span></span> <span data-ttu-id="dbac5-110">After the cloud appliance is stopped, its status is **Stopped (deallocated)**.</span><span class="sxs-lookup"><span data-stu-id="dbac5-110">After the cloud appliance is stopped, its status is **Stopped (deallocated)**.</span></span>

    ![StorSimple Cloud Appliance Virtual Machine](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart4.png)

5. <span data-ttu-id="dbac5-112">Once a VM is stopped, click **Start** (button becomes available) to start the VM.</span><span class="sxs-lookup"><span data-stu-id="dbac5-112">Once a VM is stopped, click **Start** (button becomes available) to start the VM.</span></span> <span data-ttu-id="dbac5-113">After the cloud appliance has started up, its status is **Started**.</span><span class="sxs-lookup"><span data-stu-id="dbac5-113">After the cloud appliance has started up, its status is **Started**.</span></span>

    ![StorSimple Cloud Appliance Virtual Machine](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart5.png)

<span data-ttu-id="dbac5-115">Use the following cmdlets to stop and start a cloud appliance.</span><span class="sxs-lookup"><span data-stu-id="dbac5-115">Use the following cmdlets to stop and start a cloud appliance.</span></span>

`Stop-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

`Start-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

#### <a name="to-restart-a-cloud-appliance"></a><span data-ttu-id="dbac5-116">To restart a cloud appliance</span><span class="sxs-lookup"><span data-stu-id="dbac5-116">To restart a cloud appliance</span></span>

<span data-ttu-id="dbac5-117">To restart a cloud appliance, go to the VM for your cloud appliance.</span><span class="sxs-lookup"><span data-stu-id="dbac5-117">To restart a cloud appliance, go to the VM for your cloud appliance.</span></span> <span data-ttu-id="dbac5-118">From the command bar, click **Restart**.</span><span class="sxs-lookup"><span data-stu-id="dbac5-118">From the command bar, click **Restart**.</span></span> <span data-ttu-id="dbac5-119">When prompted, confirm the restart.</span><span class="sxs-lookup"><span data-stu-id="dbac5-119">When prompted, confirm the restart.</span></span> <span data-ttu-id="dbac5-120">When the cloud appliance is ready for you to use, its status is **Running**.</span><span class="sxs-lookup"><span data-stu-id="dbac5-120">When the cloud appliance is ready for you to use, its status is **Running**.</span></span>

![StorSimple Cloud Appliance Virtual Machine](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart6.png)

<span data-ttu-id="dbac5-122">Use the following cmdlet to restart a cloud appliance.</span><span class="sxs-lookup"><span data-stu-id="dbac5-122">Use the following cmdlet to restart a cloud appliance.</span></span>

`Restart-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

