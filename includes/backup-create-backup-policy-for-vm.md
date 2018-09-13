## <a name="defining-a-backup-policy"></a><span data-ttu-id="682c6-101">Defining a backup policy</span><span class="sxs-lookup"><span data-stu-id="682c6-101">Defining a backup policy</span></span>
<span data-ttu-id="682c6-102">A backup policy defines a matrix of when the data snapshots are taken, and how long those snapshots are retained.</span><span class="sxs-lookup"><span data-stu-id="682c6-102">A backup policy defines a matrix of when the data snapshots are taken, and how long those snapshots are retained.</span></span> <span data-ttu-id="682c6-103">When defining a policy for backing up a VM, you can trigger a backup job *once a day*.</span><span class="sxs-lookup"><span data-stu-id="682c6-103">When defining a policy for backing up a VM, you can trigger a backup job *once a day*.</span></span> <span data-ttu-id="682c6-104">When you create a new policy, it is applied to the vault.</span><span class="sxs-lookup"><span data-stu-id="682c6-104">When you create a new policy, it is applied to the vault.</span></span> <span data-ttu-id="682c6-105">The backup policy interface looks like this:</span><span class="sxs-lookup"><span data-stu-id="682c6-105">The backup policy interface looks like this:</span></span>

![Backup policy](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/backup-create-policy-for-vms/backup-policy.png)

<span data-ttu-id="682c6-107">To create a policy:</span><span class="sxs-lookup"><span data-stu-id="682c6-107">To create a policy:</span></span>

1. <span data-ttu-id="682c6-108">Enter a name for the **Policy name**.</span><span class="sxs-lookup"><span data-stu-id="682c6-108">Enter a name for the **Policy name**.</span></span>
2. <span data-ttu-id="682c6-109">Snapshots of your data can be taken at Daily or Weekly intervals.</span><span class="sxs-lookup"><span data-stu-id="682c6-109">Snapshots of your data can be taken at Daily or Weekly intervals.</span></span> <span data-ttu-id="682c6-110">Use the **Backup Frequency** drop-down menu to choose whether data snapshots are taken Daily or Weekly.</span><span class="sxs-lookup"><span data-stu-id="682c6-110">Use the **Backup Frequency** drop-down menu to choose whether data snapshots are taken Daily or Weekly.</span></span>
   
   * <span data-ttu-id="682c6-111">If you choose a Daily interval, use the highlighted control to select the time of the day for the snapshot.</span><span class="sxs-lookup"><span data-stu-id="682c6-111">If you choose a Daily interval, use the highlighted control to select the time of the day for the snapshot.</span></span> <span data-ttu-id="682c6-112">To change the hour, de-select the hour, and select the new hour.</span><span class="sxs-lookup"><span data-stu-id="682c6-112">To change the hour, de-select the hour, and select the new hour.</span></span>
     
     ![Daily backup policy](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/backup-create-policy-for-vms/backup-policy-daily.png) <br/>
   * <span data-ttu-id="682c6-114">If you choose a Weekly interval, use the highlighted controls to select the day(s) of the week, and the time of day to take the snapshot.</span><span class="sxs-lookup"><span data-stu-id="682c6-114">If you choose a Weekly interval, use the highlighted controls to select the day(s) of the week, and the time of day to take the snapshot.</span></span> <span data-ttu-id="682c6-115">In the day menu, select one or multiple days.</span><span class="sxs-lookup"><span data-stu-id="682c6-115">In the day menu, select one or multiple days.</span></span> <span data-ttu-id="682c6-116">In the hour menu, select one hour.</span><span class="sxs-lookup"><span data-stu-id="682c6-116">In the hour menu, select one hour.</span></span> <span data-ttu-id="682c6-117">To change the hour, de-select the selected hour, and select the new hour.</span><span class="sxs-lookup"><span data-stu-id="682c6-117">To change the hour, de-select the selected hour, and select the new hour.</span></span>
     
     ![Weekly backup policy](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/backup-create-policy-for-vms/backup-policy-weekly.png)
3. <span data-ttu-id="682c6-119">By default, all **Retention Range** options are selected.</span><span class="sxs-lookup"><span data-stu-id="682c6-119">By default, all **Retention Range** options are selected.</span></span> <span data-ttu-id="682c6-120">Uncheck any retention range limit you do not want to use.</span><span class="sxs-lookup"><span data-stu-id="682c6-120">Uncheck any retention range limit you do not want to use.</span></span> <span data-ttu-id="682c6-121">Then, specify the interval(s) to use.</span><span class="sxs-lookup"><span data-stu-id="682c6-121">Then, specify the interval(s) to use.</span></span>
   
    <span data-ttu-id="682c6-122">Monthly and Yearly retention ranges allow you to specify the snapshots based on a weekly or daily increment.</span><span class="sxs-lookup"><span data-stu-id="682c6-122">Monthly and Yearly retention ranges allow you to specify the snapshots based on a weekly or daily increment.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="682c6-123">When protecting a VM, a backup job runs once a day.</span><span class="sxs-lookup"><span data-stu-id="682c6-123">When protecting a VM, a backup job runs once a day.</span></span> <span data-ttu-id="682c6-124">The time when the backup runs is the same for each retention range.</span><span class="sxs-lookup"><span data-stu-id="682c6-124">The time when the backup runs is the same for each retention range.</span></span>
   > 
   > 
4. <span data-ttu-id="682c6-125">After setting all options for the policy, at the top of the blade click **Save**.</span><span class="sxs-lookup"><span data-stu-id="682c6-125">After setting all options for the policy, at the top of the blade click **Save**.</span></span>
   
    <span data-ttu-id="682c6-126">The new policy is immediately applied to the vault.</span><span class="sxs-lookup"><span data-stu-id="682c6-126">The new policy is immediately applied to the vault.</span></span>




