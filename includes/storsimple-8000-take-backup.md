<!--author=alkohli last changed: 01/12/17-->

### <a name="to-take-a-backup"></a><span data-ttu-id="bf8b1-101">To take a backup</span><span class="sxs-lookup"><span data-stu-id="bf8b1-101">To take a backup</span></span>

1. <span data-ttu-id="bf8b1-102">Go to your StorSimple Device Manager service.</span><span class="sxs-lookup"><span data-stu-id="bf8b1-102">Go to your StorSimple Device Manager service.</span></span> <span data-ttu-id="bf8b1-103">From the tabular listing of devices, select and click your device and then click **All settings**.</span><span class="sxs-lookup"><span data-stu-id="bf8b1-103">From the tabular listing of devices, select and click your device and then click **All settings**.</span></span> <span data-ttu-id="bf8b1-104">In the **Settings** blade, go to **Settings > Manage > Backup policy**.</span><span class="sxs-lookup"><span data-stu-id="bf8b1-104">In the **Settings** blade, go to **Settings > Manage > Backup policy**.</span></span>

    ![Add-backup-policy](./media/storsimple-8000-take-backup/step8takebu1.png)

2. <span data-ttu-id="bf8b1-106">In the **Backup policy** blade, click **+ Add policy**.</span><span class="sxs-lookup"><span data-stu-id="bf8b1-106">In the **Backup policy** blade, click **+ Add policy**.</span></span>

    ![Add-backup-policy](./media/storsimple-8000-take-backup/step8takebu2.png)

3. <span data-ttu-id="bf8b1-108">In the **Create backup policy** blade, supply a name that contains between 3 and 150 characters for your backup policy.</span><span class="sxs-lookup"><span data-stu-id="bf8b1-108">In the **Create backup policy** blade, supply a name that contains between 3 and 150 characters for your backup policy.</span></span>

4. <span data-ttu-id="bf8b1-109">Select the volumes to be backed up.</span><span class="sxs-lookup"><span data-stu-id="bf8b1-109">Select the volumes to be backed up.</span></span> <span data-ttu-id="bf8b1-110">If you select more than one volume, these volumes are grouped together to create a crash-consistent backup.</span><span class="sxs-lookup"><span data-stu-id="bf8b1-110">If you select more than one volume, these volumes are grouped together to create a crash-consistent backup.</span></span>

    ![Add-backup-policy](./media/storsimple-8000-take-backup/step8takebu4.png)

5. <span data-ttu-id="bf8b1-112">On **Add first schedule** blade:</span><span class="sxs-lookup"><span data-stu-id="bf8b1-112">On **Add first schedule** blade:</span></span>

    1. <span data-ttu-id="bf8b1-113">Select the type of backup.</span><span class="sxs-lookup"><span data-stu-id="bf8b1-113">Select the type of backup.</span></span> <span data-ttu-id="bf8b1-114">For faster restores, select **Local** snapshot.</span><span class="sxs-lookup"><span data-stu-id="bf8b1-114">For faster restores, select **Local** snapshot.</span></span> <span data-ttu-id="bf8b1-115">For data resiliency, select **Cloud** snapshot.</span><span class="sxs-lookup"><span data-stu-id="bf8b1-115">For data resiliency, select **Cloud** snapshot.</span></span>
    2. <span data-ttu-id="bf8b1-116">Specify the backup frequency in minutes, hours, days, or weeks.</span><span class="sxs-lookup"><span data-stu-id="bf8b1-116">Specify the backup frequency in minutes, hours, days, or weeks.</span></span>
    3. <span data-ttu-id="bf8b1-117">Select a retention time.</span><span class="sxs-lookup"><span data-stu-id="bf8b1-117">Select a retention time.</span></span> <span data-ttu-id="bf8b1-118">The retention choices depend on the backup frequency.</span><span class="sxs-lookup"><span data-stu-id="bf8b1-118">The retention choices depend on the backup frequency.</span></span> <span data-ttu-id="bf8b1-119">For example, for a daily policy, the retention can be specified in weeks, whereas retention for a monthly policy is in months.</span><span class="sxs-lookup"><span data-stu-id="bf8b1-119">For example, for a daily policy, the retention can be specified in weeks, whereas retention for a monthly policy is in months.</span></span>
    4. <span data-ttu-id="bf8b1-120">Select the starting time and date for the backup policy.</span><span class="sxs-lookup"><span data-stu-id="bf8b1-120">Select the starting time and date for the backup policy.</span></span>
    5. <span data-ttu-id="bf8b1-121">Click **OK** to create the backup policy.</span><span class="sxs-lookup"><span data-stu-id="bf8b1-121">Click **OK** to create the backup policy.</span></span>

        ![Add-backup-policy](./media/storsimple-8000-take-backup/step8takebu5.png) 

6. <span data-ttu-id="bf8b1-123">Click **Create** to start the backup policy creation.</span><span class="sxs-lookup"><span data-stu-id="bf8b1-123">Click **Create** to start the backup policy creation.</span></span> <span data-ttu-id="bf8b1-124">You are notified when the backup policy is successfully created.</span><span class="sxs-lookup"><span data-stu-id="bf8b1-124">You are notified when the backup policy is successfully created.</span></span> <span data-ttu-id="bf8b1-125">The list of backup policies is also updated.</span><span class="sxs-lookup"><span data-stu-id="bf8b1-125">The list of backup policies is also updated.</span></span>
      
      ![Add-backup-policy](./media/storsimple-8000-take-backup/step8takebu9.png)
      
      <span data-ttu-id="bf8b1-127">You now have a backup policy that creates scheduled backups of your volume data.</span><span class="sxs-lookup"><span data-stu-id="bf8b1-127">You now have a backup policy that creates scheduled backups of your volume data.</span></span>




