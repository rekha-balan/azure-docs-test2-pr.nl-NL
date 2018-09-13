<!--author=SharS last changed: 02/04/2016-->

#### <a name="to-create-a-volume"></a><span data-ttu-id="11c70-101">To create a volume</span><span class="sxs-lookup"><span data-stu-id="11c70-101">To create a volume</span></span>
1. <span data-ttu-id="11c70-102">On the device **Quick Start** page, click **Add a volume**.</span><span class="sxs-lookup"><span data-stu-id="11c70-102">On the device **Quick Start** page, click **Add a volume**.</span></span> <span data-ttu-id="11c70-103">This starts the Add a volume wizard.</span><span class="sxs-lookup"><span data-stu-id="11c70-103">This starts the Add a volume wizard.</span></span>
2. <span data-ttu-id="11c70-104">In the Add a volume wizard, under **Basic Settings**, do the following:</span><span class="sxs-lookup"><span data-stu-id="11c70-104">In the Add a volume wizard, under **Basic Settings**, do the following:</span></span>
   
   1. <span data-ttu-id="11c70-105">Supply a **Name** for your volume.</span><span class="sxs-lookup"><span data-stu-id="11c70-105">Supply a **Name** for your volume.</span></span>
   2. <span data-ttu-id="11c70-106">Specify the **Provisioned Capacity** for your volume in GB or TB.</span><span class="sxs-lookup"><span data-stu-id="11c70-106">Specify the **Provisioned Capacity** for your volume in GB or TB.</span></span> <span data-ttu-id="11c70-107">The volume capacity must be between 1 GB and 64 TB for a physical device.</span><span class="sxs-lookup"><span data-stu-id="11c70-107">The volume capacity must be between 1 GB and 64 TB for a physical device.</span></span>
   3. <span data-ttu-id="11c70-108">On the drop-down list, select the **Usage Type** for your volume.</span><span class="sxs-lookup"><span data-stu-id="11c70-108">On the drop-down list, select the **Usage Type** for your volume.</span></span> 
   4. <span data-ttu-id="11c70-109">If you are using this volume for archival data, select the **Use this volume for less frequently accessed archival data** check box.</span><span class="sxs-lookup"><span data-stu-id="11c70-109">If you are using this volume for archival data, select the **Use this volume for less frequently accessed archival data** check box.</span></span> <span data-ttu-id="11c70-110">For all other use cases, simply select **Tiered Volume**.</span><span class="sxs-lookup"><span data-stu-id="11c70-110">For all other use cases, simply select **Tiered Volume**.</span></span> <span data-ttu-id="11c70-111">(Tiered volumes were formerly called primary volumes).</span><span class="sxs-lookup"><span data-stu-id="11c70-111">(Tiered volumes were formerly called primary volumes).</span></span>
      
        ![Add volume](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/storsimple-create-volume/ScreenshotUpdate1VolumeFlow.png)
      
      1. <span data-ttu-id="11c70-113">Click the arrow icon</span><span class="sxs-lookup"><span data-stu-id="11c70-113">Click the arrow icon</span></span> ![arrow-icon](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/storsimple-create-volume/HCS_ArrowIcon-include.png) <span data-ttu-id="11c70-115">to go to the next page.</span><span class="sxs-lookup"><span data-stu-id="11c70-115">to go to the next page.</span></span>
3. <span data-ttu-id="11c70-116">In the **Additional Settings** dialog box, add a new access control record (ACR):</span><span class="sxs-lookup"><span data-stu-id="11c70-116">In the **Additional Settings** dialog box, add a new access control record (ACR):</span></span>
   
   1. <span data-ttu-id="11c70-117">Supply a **Name** for your ACR.</span><span class="sxs-lookup"><span data-stu-id="11c70-117">Supply a **Name** for your ACR.</span></span>
   2. <span data-ttu-id="11c70-118">Under **iSCSI Initiator Name**, provide the iSCSI Qualified Name (IQN) of your Windows host.</span><span class="sxs-lookup"><span data-stu-id="11c70-118">Under **iSCSI Initiator Name**, provide the iSCSI Qualified Name (IQN) of your Windows host.</span></span> <span data-ttu-id="11c70-119">If you don't have the IQN, go to [Get the IQN of a Windows Server host](#get-the-iqn-of-a-windows-server-host).</span><span class="sxs-lookup"><span data-stu-id="11c70-119">If you don't have the IQN, go to [Get the IQN of a Windows Server host](#get-the-iqn-of-a-windows-server-host).</span></span>
   3. <span data-ttu-id="11c70-120">We recommend that you enable a default backup by selecting the **Enable a default backup for this volume** check box.</span><span class="sxs-lookup"><span data-stu-id="11c70-120">We recommend that you enable a default backup by selecting the **Enable a default backup for this volume** check box.</span></span> <span data-ttu-id="11c70-121">The default backup will create a policy that executes at 22:30 each day (device time) and creates a cloud snapshot of this volume.</span><span class="sxs-lookup"><span data-stu-id="11c70-121">The default backup will create a policy that executes at 22:30 each day (device time) and creates a cloud snapshot of this volume.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="11c70-122">After the backup is enabled here, it cannot be reverted.</span><span class="sxs-lookup"><span data-stu-id="11c70-122">After the backup is enabled here, it cannot be reverted.</span></span> <span data-ttu-id="11c70-123">You will need to edit the volume to modify this setting.</span><span class="sxs-lookup"><span data-stu-id="11c70-123">You will need to edit the volume to modify this setting.</span></span>
      > 
      > 
      
        ![Add volume](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/storsimple-create-volume/AddVolume2-include.png)
4. <span data-ttu-id="11c70-125">Click the check icon</span><span class="sxs-lookup"><span data-stu-id="11c70-125">Click the check icon</span></span> ![check icon](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/storsimple-create-volume/HCS_CheckIcon-include.png)<span data-ttu-id="11c70-127">.</span><span class="sxs-lookup"><span data-stu-id="11c70-127">.</span></span> <span data-ttu-id="11c70-128">A volume will be created with the specified settings.</span><span class="sxs-lookup"><span data-stu-id="11c70-128">A volume will be created with the specified settings.</span></span>

<span data-ttu-id="11c70-129">![Video available](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/storsimple-create-volume/Video_icon.png) **Video available**</span><span class="sxs-lookup"><span data-stu-id="11c70-129">![Video available](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/storsimple-create-volume/Video_icon.png) **Video available**</span></span>

<span data-ttu-id="11c70-130">To watch a video that demonstrates how to create a StorSimple volume, click [here](https://azure.microsoft.com/documentation/videos/create-a-storsimple-volume/).</span><span class="sxs-lookup"><span data-stu-id="11c70-130">To watch a video that demonstrates how to create a StorSimple volume, click [here](https://azure.microsoft.com/documentation/videos/create-a-storsimple-volume/).</span></span>






