<!--author=v-sharos last changed: 11/06/15-->

#### <a name="to-add-a-storsimple-backup-policy"></a><span data-ttu-id="0d91e-101">To add a StorSimple backup policy</span><span class="sxs-lookup"><span data-stu-id="0d91e-101">To add a StorSimple backup policy</span></span>
1. <span data-ttu-id="0d91e-102">On the device **Quick Start** page, click the **Backup Policies** tab. This will take you to the **Backup Policies** page.</span><span class="sxs-lookup"><span data-stu-id="0d91e-102">On the device **Quick Start** page, click the **Backup Policies** tab. This will take you to the **Backup Policies** page.</span></span>
2. <span data-ttu-id="0d91e-103">At the bottom of the page, click **Add** to start the Add Backup Policy wizard.</span><span class="sxs-lookup"><span data-stu-id="0d91e-103">At the bottom of the page, click **Add** to start the Add Backup Policy wizard.</span></span>
   
    ![Add a backup policy 1](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/storsimple-add-backup-policy-u2/AddBackupPolicy1.png)
3. <span data-ttu-id="0d91e-105">In the **Add Backup Policy** dialog box, under **Define your backup policy**, do the following:</span><span class="sxs-lookup"><span data-stu-id="0d91e-105">In the **Add Backup Policy** dialog box, under **Define your backup policy**, do the following:</span></span>
   
   1. <span data-ttu-id="0d91e-106">Specify a backup policy name that contains between 3 and 150 characters.</span><span class="sxs-lookup"><span data-stu-id="0d91e-106">Specify a backup policy name that contains between 3 and 150 characters.</span></span>
   2. <span data-ttu-id="0d91e-107">Click the check box(es) to assign one or more volumes to this backup policy.</span><span class="sxs-lookup"><span data-stu-id="0d91e-107">Click the check box(es) to assign one or more volumes to this backup policy.</span></span> <span data-ttu-id="0d91e-108">Note that you cannot select volumes that use different cloud service providers.</span><span class="sxs-lookup"><span data-stu-id="0d91e-108">Note that you cannot select volumes that use different cloud service providers.</span></span> <span data-ttu-id="0d91e-109">If you are using multiple cloud service providers, based on your first selection, the list will show volumes belonging to only that cloud service provider.</span><span class="sxs-lookup"><span data-stu-id="0d91e-109">If you are using multiple cloud service providers, based on your first selection, the list will show volumes belonging to only that cloud service provider.</span></span> <span data-ttu-id="0d91e-110">This will allow you to group volumes belonging to a single cloud service provider in a snapshot.</span><span class="sxs-lookup"><span data-stu-id="0d91e-110">This will allow you to group volumes belonging to a single cloud service provider in a snapshot.</span></span>
   3. <span data-ttu-id="0d91e-111">Click the arrow icon</span><span class="sxs-lookup"><span data-stu-id="0d91e-111">Click the arrow icon</span></span> ![arrow icon](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/storsimple-add-backup-policy-u2/HCS_ArrowIcon-include.png) <span data-ttu-id="0d91e-113">to go to the next page.</span><span class="sxs-lookup"><span data-stu-id="0d91e-113">to go to the next page.</span></span>
      
      ![Add a backup policy 2](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/storsimple-add-backup-policy-u2/AddBackupPolicy2.png)
4. <span data-ttu-id="0d91e-115">Under **Define a schedule**, do the following:</span><span class="sxs-lookup"><span data-stu-id="0d91e-115">Under **Define a schedule**, do the following:</span></span>
   
   1. <span data-ttu-id="0d91e-116">In the **Type of Backup** box, select **Cloud Snapshot** or **Local Snapshot** from the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="0d91e-116">In the **Type of Backup** box, select **Cloud Snapshot** or **Local Snapshot** from the drop-down list.</span></span>
   2. <span data-ttu-id="0d91e-117">Indicate the frequency of backups (specify a number and then choose **Days** or **Weeks** from the drop-down list).</span><span class="sxs-lookup"><span data-stu-id="0d91e-117">Indicate the frequency of backups (specify a number and then choose **Days** or **Weeks** from the drop-down list).</span></span>
   3. <span data-ttu-id="0d91e-118">Enter a retention schedule.</span><span class="sxs-lookup"><span data-stu-id="0d91e-118">Enter a retention schedule.</span></span>
   4. <span data-ttu-id="0d91e-119">Enter a time and date for the backup policy to begin.</span><span class="sxs-lookup"><span data-stu-id="0d91e-119">Enter a time and date for the backup policy to begin.</span></span>  
   5. <span data-ttu-id="0d91e-120">Click the check icon</span><span class="sxs-lookup"><span data-stu-id="0d91e-120">Click the check icon</span></span> ![check icon](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/storsimple-add-backup-policy-u2/HCS_CheckIcon-include.png) <span data-ttu-id="0d91e-122">to save the policy.</span><span class="sxs-lookup"><span data-stu-id="0d91e-122">to save the policy.</span></span>

<span data-ttu-id="0d91e-123">The newly added policy will be displayed in the tabular view on the **Backup Policies** page.</span><span class="sxs-lookup"><span data-stu-id="0d91e-123">The newly added policy will be displayed in the tabular view on the **Backup Policies** page.</span></span>





