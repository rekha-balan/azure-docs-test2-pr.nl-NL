<!--author=SharS last changed: 1/7/2016-->

#### <a name="to-add-a-volume-container"></a><span data-ttu-id="9d1e4-101">To add a volume container</span><span class="sxs-lookup"><span data-stu-id="9d1e4-101">To add a volume container</span></span>
1. <span data-ttu-id="9d1e4-102">On the **Devices** page, select the device, double-click it, and then click the **Volume containers** tab.</span><span class="sxs-lookup"><span data-stu-id="9d1e4-102">On the **Devices** page, select the device, double-click it, and then click the **Volume containers** tab.</span></span>
2. <span data-ttu-id="9d1e4-103">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="9d1e4-103">Click **Add** at the bottom of the page.</span></span> <span data-ttu-id="9d1e4-104">In the **Create volume container** dialog box, do the following:</span><span class="sxs-lookup"><span data-stu-id="9d1e4-104">In the **Create volume container** dialog box, do the following:</span></span>
   
   1. <span data-ttu-id="9d1e4-105">Supply a unique **Name** for your volume container.</span><span class="sxs-lookup"><span data-stu-id="9d1e4-105">Supply a unique **Name** for your volume container.</span></span> <span data-ttu-id="9d1e4-106">This name can contain a maximum of 32 characters.</span><span class="sxs-lookup"><span data-stu-id="9d1e4-106">This name can contain a maximum of 32 characters.</span></span>
   2. <span data-ttu-id="9d1e4-107">Select a **Storage Account** to be associated with this volume container.</span><span class="sxs-lookup"><span data-stu-id="9d1e4-107">Select a **Storage Account** to be associated with this volume container.</span></span> <span data-ttu-id="9d1e4-108">You can choose from an existing storage account within the same subscription or select **Add more** to select a storage account from another subscription.</span><span class="sxs-lookup"><span data-stu-id="9d1e4-108">You can choose from an existing storage account within the same subscription or select **Add more** to select a storage account from another subscription.</span></span> <span data-ttu-id="9d1e4-109">You can also choose the storage account that was first generated when the service was created.</span><span class="sxs-lookup"><span data-stu-id="9d1e4-109">You can also choose the storage account that was first generated when the service was created.</span></span>
   3. <span data-ttu-id="9d1e4-110">Specify bandwidth as **Unlimited** if you want to consume all available bandwidth, or **Custom** to employ bandwidth controls.</span><span class="sxs-lookup"><span data-stu-id="9d1e4-110">Specify bandwidth as **Unlimited** if you want to consume all available bandwidth, or **Custom** to employ bandwidth controls.</span></span> <span data-ttu-id="9d1e4-111">For a custom bandwidth, supply a value between 1 and 1000 Mbps.</span><span class="sxs-lookup"><span data-stu-id="9d1e4-111">For a custom bandwidth, supply a value between 1 and 1000 Mbps.</span></span> <span data-ttu-id="9d1e4-112">To allocate bandwidth based on a schedule, you can **Select a bandwidth template**.</span><span class="sxs-lookup"><span data-stu-id="9d1e4-112">To allocate bandwidth based on a schedule, you can **Select a bandwidth template**.</span></span>
   4. <span data-ttu-id="9d1e4-113">We recommend that you keep **Enable Cloud Storage Encryption** selected to encrypt the data that is going to the cloud.</span><span class="sxs-lookup"><span data-stu-id="9d1e4-113">We recommend that you keep **Enable Cloud Storage Encryption** selected to encrypt the data that is going to the cloud.</span></span> <span data-ttu-id="9d1e4-114">Disable encryption only if you are employing other means to encrypt your data.</span><span class="sxs-lookup"><span data-stu-id="9d1e4-114">Disable encryption only if you are employing other means to encrypt your data.</span></span> <span data-ttu-id="9d1e4-115">You cannot modify the encryption setting once the volume container has been created.</span><span class="sxs-lookup"><span data-stu-id="9d1e4-115">You cannot modify the encryption setting once the volume container has been created.</span></span>
   5. <span data-ttu-id="9d1e4-116">Provide a **Cloud Storage Encryption Key** that contains between 8 and 32 characters.</span><span class="sxs-lookup"><span data-stu-id="9d1e4-116">Provide a **Cloud Storage Encryption Key** that contains between 8 and 32 characters.</span></span> <span data-ttu-id="9d1e4-117">The device uses this key to access the encrypted data.</span><span class="sxs-lookup"><span data-stu-id="9d1e4-117">The device uses this key to access the encrypted data.</span></span> <span data-ttu-id="9d1e4-118">In the **Confirm Cloud Storage Encryption Key** field, enter the cloud storage encryption key again to confirm it.</span><span class="sxs-lookup"><span data-stu-id="9d1e4-118">In the **Confirm Cloud Storage Encryption Key** field, enter the cloud storage encryption key again to confirm it.</span></span> 
   6. <span data-ttu-id="9d1e4-119">Click the arrow to proceed to the next page.</span><span class="sxs-lookup"><span data-stu-id="9d1e4-119">Click the arrow to proceed to the next page.</span></span>
      
      ![Create volume container with bandwidth template 1](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/storsimple-add-volume-container/HCS_CreateVCBT1-include.png) 
3. <span data-ttu-id="9d1e4-121">If you specified **Select a bandwidth template**, choose from the dropdown list of existing bandwidth templates.</span><span class="sxs-lookup"><span data-stu-id="9d1e4-121">If you specified **Select a bandwidth template**, choose from the dropdown list of existing bandwidth templates.</span></span> <span data-ttu-id="9d1e4-122">Review the schedule settings and click the check icon ![check icon](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/storsimple-configure-new-storage-account/HCS_CheckIcon-include.png).</span><span class="sxs-lookup"><span data-stu-id="9d1e4-122">Review the schedule settings and click the check icon ![check icon](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/storsimple-configure-new-storage-account/HCS_CheckIcon-include.png).</span></span>
   
    ![Create volume container with bandwidth template 2](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/storsimple-add-volume-container/HCS_CreateVCBT2-include.png) 

<span data-ttu-id="9d1e4-124">The volume container will be saved and the newly created volume container will be listed on the **Volume container** page.</span><span class="sxs-lookup"><span data-stu-id="9d1e4-124">The volume container will be saved and the newly created volume container will be listed on the **Volume container** page.</span></span>



