
<!--author=alkohli last changed: 01/20/2017-->

#### <a name="to-create-a-manual-backup"></a><span data-ttu-id="10467-101">To create a manual backup</span><span class="sxs-lookup"><span data-stu-id="10467-101">To create a manual backup</span></span>

1. <span data-ttu-id="10467-102">Go to your StorSimple Device Manager service and then click **Devices**.</span><span class="sxs-lookup"><span data-stu-id="10467-102">Go to your StorSimple Device Manager service and then click **Devices**.</span></span> <span data-ttu-id="10467-103">From the tabular listing of devices, select your device.</span><span class="sxs-lookup"><span data-stu-id="10467-103">From the tabular listing of devices, select your device.</span></span> <span data-ttu-id="10467-104">Go to **Settings > Manage > Backup policies**.</span><span class="sxs-lookup"><span data-stu-id="10467-104">Go to **Settings > Manage > Backup policies**.</span></span>

2. <span data-ttu-id="10467-105">The **Backup policies** blade lists all the backup policies in a tabular format, including the policy for the volume that you want to back up.</span><span class="sxs-lookup"><span data-stu-id="10467-105">The **Backup policies** blade lists all the backup policies in a tabular format, including the policy for the volume that you want to back up.</span></span> <span data-ttu-id="10467-106">Select the policy associated with the volume you want to back up and right-click to invoke the context menu.</span><span class="sxs-lookup"><span data-stu-id="10467-106">Select the policy associated with the volume you want to back up and right-click to invoke the context menu.</span></span> <span data-ttu-id="10467-107">From the dropdown list, select **Back up now**.</span><span class="sxs-lookup"><span data-stu-id="10467-107">From the dropdown list, select **Back up now**.</span></span>

    ![Create manual backup](./media/storsimple-8000-create-manual-backup/createmanualbu1.png)

3. <span data-ttu-id="10467-109">In the **Back up now** blade, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="10467-109">In the **Back up now** blade, do the following steps:</span></span>

    1. <span data-ttu-id="10467-110">Choose the appropriate **Snapshot type** from the dropdown list: **Local** snapshot or **Cloud** snapshot.</span><span class="sxs-lookup"><span data-stu-id="10467-110">Choose the appropriate **Snapshot type** from the dropdown list: **Local** snapshot or **Cloud** snapshot.</span></span> <span data-ttu-id="10467-111">Select local snapshot for fast backups or restores, and cloud snapshot for data resiliency.</span><span class="sxs-lookup"><span data-stu-id="10467-111">Select local snapshot for fast backups or restores, and cloud snapshot for data resiliency.</span></span>

        ![Create manual backup](./media/storsimple-8000-create-manual-backup/createmanualbu2.png)

    2. <span data-ttu-id="10467-113">Click **OK** to start a job to create a snapshot.</span><span class="sxs-lookup"><span data-stu-id="10467-113">Click **OK** to start a job to create a snapshot.</span></span> <span data-ttu-id="10467-114">You will see a notification at the top of the page after the job is successfully created.</span><span class="sxs-lookup"><span data-stu-id="10467-114">You will see a notification at the top of the page after the job is successfully created.</span></span>

        ![Create manual backup](./media/storsimple-8000-create-manual-backup/createmanualbu4.png)

    3. <span data-ttu-id="10467-116">To monitor the job, click the notification.</span><span class="sxs-lookup"><span data-stu-id="10467-116">To monitor the job, click the notification.</span></span> <span data-ttu-id="10467-117">This takes you to the **Jobs** blade where you can view the job progress.</span><span class="sxs-lookup"><span data-stu-id="10467-117">This takes you to the **Jobs** blade where you can view the job progress.</span></span>


5. <span data-ttu-id="10467-118">After the backup job is finished, go to the **Backup catalog** tab.</span><span class="sxs-lookup"><span data-stu-id="10467-118">After the backup job is finished, go to the **Backup catalog** tab.</span></span>

6. <span data-ttu-id="10467-119">Set the filter selections to the appropriate device, backup policy, and time range.</span><span class="sxs-lookup"><span data-stu-id="10467-119">Set the filter selections to the appropriate device, backup policy, and time range.</span></span> <span data-ttu-id="10467-120">The backup should appear in the list of backup sets that is displayed in the catalog.</span><span class="sxs-lookup"><span data-stu-id="10467-120">The backup should appear in the list of backup sets that is displayed in the catalog.</span></span>

