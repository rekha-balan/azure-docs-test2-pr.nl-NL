<!--author=alkohli last changed: 9/17/15-->

### <a name="to-take-a-backup"></a><span data-ttu-id="4697b-101">To take a backup</span><span class="sxs-lookup"><span data-stu-id="4697b-101">To take a backup</span></span>
1. <span data-ttu-id="4697b-102">On the device **Quick Start** page, click **Add a backup policy**.</span><span class="sxs-lookup"><span data-stu-id="4697b-102">On the device **Quick Start** page, click **Add a backup policy**.</span></span> <span data-ttu-id="4697b-103">This will start the Add Backup Policy wizard.</span><span class="sxs-lookup"><span data-stu-id="4697b-103">This will start the Add Backup Policy wizard.</span></span> 
2. <span data-ttu-id="4697b-104">On the **Define your backup policy** page:</span><span class="sxs-lookup"><span data-stu-id="4697b-104">On the **Define your backup policy** page:</span></span>
   
   1. <span data-ttu-id="4697b-105">Supply a name that contains between 3 and 150 characters for your backup policy.</span><span class="sxs-lookup"><span data-stu-id="4697b-105">Supply a name that contains between 3 and 150 characters for your backup policy.</span></span>
   2. <span data-ttu-id="4697b-106">Select the volumes to be backed up.</span><span class="sxs-lookup"><span data-stu-id="4697b-106">Select the volumes to be backed up.</span></span> <span data-ttu-id="4697b-107">If you select more than one volume, these volumes will be grouped together to create a crash-consistent backup.</span><span class="sxs-lookup"><span data-stu-id="4697b-107">If you select more than one volume, these volumes will be grouped together to create a crash-consistent backup.</span></span>
   3. <span data-ttu-id="4697b-108">Click the arrow icon</span><span class="sxs-lookup"><span data-stu-id="4697b-108">Click the arrow icon</span></span> ![arrow-icon](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/storsimple-take-backup/HCS_ArrowIcon-include.png)<span data-ttu-id="4697b-110">.</span><span class="sxs-lookup"><span data-stu-id="4697b-110">.</span></span> 
      
      ![Add-backup-policy](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/storsimple-take-backup/HCS_AddBackupPolicyWizard1M-include.png)
3. <span data-ttu-id="4697b-112">On the **Define a schedule** page:</span><span class="sxs-lookup"><span data-stu-id="4697b-112">On the **Define a schedule** page:</span></span>
   
   1. <span data-ttu-id="4697b-113">Select the type of backup from the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="4697b-113">Select the type of backup from the drop-down list.</span></span> <span data-ttu-id="4697b-114">For faster restores, select **Local Snapshot**.</span><span class="sxs-lookup"><span data-stu-id="4697b-114">For faster restores, select **Local Snapshot**.</span></span> <span data-ttu-id="4697b-115">For data resiliency, select **Cloud Snapshot**.</span><span class="sxs-lookup"><span data-stu-id="4697b-115">For data resiliency, select **Cloud Snapshot**.</span></span>
   2. <span data-ttu-id="4697b-116">Specify the backup frequency in minutes, hours, days, or weeks.</span><span class="sxs-lookup"><span data-stu-id="4697b-116">Specify the backup frequency in minutes, hours, days, or weeks.</span></span>
   3. <span data-ttu-id="4697b-117">Select a retention time.</span><span class="sxs-lookup"><span data-stu-id="4697b-117">Select a retention time.</span></span> <span data-ttu-id="4697b-118">The retention choices depend on the backup frequency.</span><span class="sxs-lookup"><span data-stu-id="4697b-118">The retention choices depend on the backup frequency.</span></span> <span data-ttu-id="4697b-119">For example, for a daily policy, the retention can be specified in weeks, whereas retention for a monthly policy is in months.</span><span class="sxs-lookup"><span data-stu-id="4697b-119">For example, for a daily policy, the retention can be specified in weeks, whereas retention for a monthly policy is in months.</span></span>
   4. <span data-ttu-id="4697b-120">Select the starting time and date for the backup policy.</span><span class="sxs-lookup"><span data-stu-id="4697b-120">Select the starting time and date for the backup policy.</span></span>
   5. <span data-ttu-id="4697b-121">Select the **Enable** check box to enable the backup policy.</span><span class="sxs-lookup"><span data-stu-id="4697b-121">Select the **Enable** check box to enable the backup policy.</span></span> 
   6. <span data-ttu-id="4697b-122">Click the check icon</span><span class="sxs-lookup"><span data-stu-id="4697b-122">Click the check icon</span></span> ![check-icon](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/storsimple-take-backup/HCS_CheckIcon-include.png) <span data-ttu-id="4697b-124">to save the policy.</span><span class="sxs-lookup"><span data-stu-id="4697b-124">to save the policy.</span></span>
      
      ![Add-backup-policy](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/storsimple-take-backup/HCS_AddBackupPolicyWizard2M-include.png)
      
      <span data-ttu-id="4697b-126">You now have a backup policy that will create scheduled backups of your volume data.</span><span class="sxs-lookup"><span data-stu-id="4697b-126">You now have a backup policy that will create scheduled backups of your volume data.</span></span>

<span data-ttu-id="4697b-127">You have completed the device configuration.</span><span class="sxs-lookup"><span data-stu-id="4697b-127">You have completed the device configuration.</span></span> 

<span data-ttu-id="4697b-128">![Video available](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/storsimple-take-backup/Video_icon.png) **Video available**</span><span class="sxs-lookup"><span data-stu-id="4697b-128">![Video available](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/storsimple-take-backup/Video_icon.png) **Video available**</span></span>

<span data-ttu-id="4697b-129">To watch a video that demonstrates how to take a StorSimple backup, click [here](https://azure.microsoft.com/documentation/videos/take-a-storsimple-backup/).</span><span class="sxs-lookup"><span data-stu-id="4697b-129">To watch a video that demonstrates how to take a StorSimple backup, click [here](https://azure.microsoft.com/documentation/videos/take-a-storsimple-backup/).</span></span>






