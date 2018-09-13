<!--author=alkohli last changed: 9/17/15-->

#### <a name="to-add-a-storage-account-in-storsimple-8000-series-update-10"></a><span data-ttu-id="7ecd4-101">To add a storage account in StorSimple 8000 Series Update 1.0</span><span class="sxs-lookup"><span data-stu-id="7ecd4-101">To add a storage account in StorSimple 8000 Series Update 1.0</span></span>
1. <span data-ttu-id="7ecd4-102">On the StorSimple Manager service landing page, select your service and double-click it.</span><span class="sxs-lookup"><span data-stu-id="7ecd4-102">On the StorSimple Manager service landing page, select your service and double-click it.</span></span> <span data-ttu-id="7ecd4-103">This will take you to the **Quick Start** page.</span><span class="sxs-lookup"><span data-stu-id="7ecd4-103">This will take you to the **Quick Start** page.</span></span> <span data-ttu-id="7ecd4-104">Select the **Configure** page.</span><span class="sxs-lookup"><span data-stu-id="7ecd4-104">Select the **Configure** page.</span></span>
2. <span data-ttu-id="7ecd4-105">Click **Add/edit storage account**.</span><span class="sxs-lookup"><span data-stu-id="7ecd4-105">Click **Add/edit storage account**.</span></span>
3. <span data-ttu-id="7ecd4-106">In the **Add/Edit Storage Account** dialog box, click **Add new**.</span><span class="sxs-lookup"><span data-stu-id="7ecd4-106">In the **Add/Edit Storage Account** dialog box, click **Add new**.</span></span>
4. <span data-ttu-id="7ecd4-107">In the **Provider** field, select the appropriate cloud service provider.</span><span class="sxs-lookup"><span data-stu-id="7ecd4-107">In the **Provider** field, select the appropriate cloud service provider.</span></span> <span data-ttu-id="7ecd4-108">The supported providers are Azure, Amazon S3, Amazon S3 with RRS, HP and OpenStack.</span><span class="sxs-lookup"><span data-stu-id="7ecd4-108">The supported providers are Azure, Amazon S3, Amazon S3 with RRS, HP and OpenStack.</span></span> <span data-ttu-id="7ecd4-109">Specify the credentials and the location associated with the storage account of your cloud service providers.</span><span class="sxs-lookup"><span data-stu-id="7ecd4-109">Specify the credentials and the location associated with the storage account of your cloud service providers.</span></span> <span data-ttu-id="7ecd4-110">The fields presented for credentials will be different depending upon the cloud service provider you have specified.</span><span class="sxs-lookup"><span data-stu-id="7ecd4-110">The fields presented for credentials will be different depending upon the cloud service provider you have specified.</span></span> 
   
   * <span data-ttu-id="7ecd4-111">If you have selected Azure as your cloud service provider, supply the **Name** and the primary **Access Key** for your Microsoft Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="7ecd4-111">If you have selected Azure as your cloud service provider, supply the **Name** and the primary **Access Key** for your Microsoft Azure storage account.</span></span> <span data-ttu-id="7ecd4-112">For an Azure account, the location will be automatically populated.</span><span class="sxs-lookup"><span data-stu-id="7ecd4-112">For an Azure account, the location will be automatically populated.</span></span>
     
        ![Add Azure storage account](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/storsimple-configure-new-storage-account-u1/AddAzureStorageaccount-include.png)
   * <span data-ttu-id="7ecd4-114">If you have selected Amazon S3 or Amazon S3 with RRS, provide a friendly **Storage Account name**, **Access Key**, and **Secret Key**.</span><span class="sxs-lookup"><span data-stu-id="7ecd4-114">If you have selected Amazon S3 or Amazon S3 with RRS, provide a friendly **Storage Account name**, **Access Key**, and **Secret Key**.</span></span> <span data-ttu-id="7ecd4-115">For Amazon S3 and Amazon S3 with RRS, the following locations are supported:</span><span class="sxs-lookup"><span data-stu-id="7ecd4-115">For Amazon S3 and Amazon S3 with RRS, the following locations are supported:</span></span>
     
     * <span data-ttu-id="7ecd4-116">US Standard</span><span class="sxs-lookup"><span data-stu-id="7ecd4-116">US Standard</span></span>
     * <span data-ttu-id="7ecd4-117">US West (Oregon)</span><span class="sxs-lookup"><span data-stu-id="7ecd4-117">US West (Oregon)</span></span>
     * <span data-ttu-id="7ecd4-118">US West (Northern California)</span><span class="sxs-lookup"><span data-stu-id="7ecd4-118">US West (Northern California)</span></span>
     * <span data-ttu-id="7ecd4-119">EU (Ireland)</span><span class="sxs-lookup"><span data-stu-id="7ecd4-119">EU (Ireland)</span></span>
     * <span data-ttu-id="7ecd4-120">Asia Pacific (Singapore)</span><span class="sxs-lookup"><span data-stu-id="7ecd4-120">Asia Pacific (Singapore)</span></span>
     * <span data-ttu-id="7ecd4-121">Asia Pacific (Sydney)</span><span class="sxs-lookup"><span data-stu-id="7ecd4-121">Asia Pacific (Sydney)</span></span>
     * <span data-ttu-id="7ecd4-122">Asia Pacific (Tokyo)</span><span class="sxs-lookup"><span data-stu-id="7ecd4-122">Asia Pacific (Tokyo)</span></span>
     * <span data-ttu-id="7ecd4-123">South America (Sao Paulo)</span><span class="sxs-lookup"><span data-stu-id="7ecd4-123">South America (Sao Paulo)</span></span>
       
       ![Add Amazon storage account](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/storsimple-configure-new-storage-account-u1/AddAmazonStorageaccount-include.png)
   * <span data-ttu-id="7ecd4-125">If you have selected HP as your cloud service provider, supply a friendly **Storage Account Name**, **Tenant ID**, **Username**, and **Password**.</span><span class="sxs-lookup"><span data-stu-id="7ecd4-125">If you have selected HP as your cloud service provider, supply a friendly **Storage Account Name**, **Tenant ID**, **Username**, and **Password**.</span></span> <span data-ttu-id="7ecd4-126">For HP, the following locations are supported:</span><span class="sxs-lookup"><span data-stu-id="7ecd4-126">For HP, the following locations are supported:</span></span>
     
     * <span data-ttu-id="7ecd4-127">US East</span><span class="sxs-lookup"><span data-stu-id="7ecd4-127">US East</span></span>
     * <span data-ttu-id="7ecd4-128">US West</span><span class="sxs-lookup"><span data-stu-id="7ecd4-128">US West</span></span>
       
       ![Add HP storage account](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/storsimple-configure-new-storage-account-u1/AddHPStorageaccount-include.png)
   * <span data-ttu-id="7ecd4-130">If you have selected **Openstack** as your cloud service provider, provide a **Hostname**, **Access Key**, and **Secret Key**.</span><span class="sxs-lookup"><span data-stu-id="7ecd4-130">If you have selected **Openstack** as your cloud service provider, provide a **Hostname**, **Access Key**, and **Secret Key**.</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="7ecd4-131">For all the cloud service providers, excluding Azure, a friendly name is allowed.</span><span class="sxs-lookup"><span data-stu-id="7ecd4-131">For all the cloud service providers, excluding Azure, a friendly name is allowed.</span></span> <span data-ttu-id="7ecd4-132">You can use different friendly names and create more than one storage account with the same set of credentials.</span><span class="sxs-lookup"><span data-stu-id="7ecd4-132">You can use different friendly names and create more than one storage account with the same set of credentials.</span></span>
     > 
     > 
     
        ![Add Openstack storage account](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/storsimple-configure-new-storage-account-u1/AddOpenstackStorageaccount-include.png)
5. <span data-ttu-id="7ecd4-134">Select **Enable SSL Mode** to create a secure channel for network communication between your device and the cloud.</span><span class="sxs-lookup"><span data-stu-id="7ecd4-134">Select **Enable SSL Mode** to create a secure channel for network communication between your device and the cloud.</span></span> <span data-ttu-id="7ecd4-135">Clear the **Enable SSL Mode** check box only if you are operating within a private cloud.</span><span class="sxs-lookup"><span data-stu-id="7ecd4-135">Clear the **Enable SSL Mode** check box only if you are operating within a private cloud.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="7ecd4-136">If you are using HP as your provider, SSL will always be enabled.</span><span class="sxs-lookup"><span data-stu-id="7ecd4-136">If you are using HP as your provider, SSL will always be enabled.</span></span>
   > 
   > 
6. <span data-ttu-id="7ecd4-137">Click the check icon</span><span class="sxs-lookup"><span data-stu-id="7ecd4-137">Click the check icon</span></span> ![check icon](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/storsimple-configure-new-storage-account/HCS_CheckIcon-include.png)<span data-ttu-id="7ecd4-139">.</span><span class="sxs-lookup"><span data-stu-id="7ecd4-139">.</span></span> <span data-ttu-id="7ecd4-140">You will be notified after the storage account is successfully created.</span><span class="sxs-lookup"><span data-stu-id="7ecd4-140">You will be notified after the storage account is successfully created.</span></span>
7. <span data-ttu-id="7ecd4-141">The newly created storage account will be displayed on the **Configure** page under **Storage accounts**.</span><span class="sxs-lookup"><span data-stu-id="7ecd4-141">The newly created storage account will be displayed on the **Configure** page under **Storage accounts**.</span></span> <span data-ttu-id="7ecd4-142">Click **Save** to save the new storage account.</span><span class="sxs-lookup"><span data-stu-id="7ecd4-142">Click **Save** to save the new storage account.</span></span> <span data-ttu-id="7ecd4-143">Click **OK** when prompted for confirmation.</span><span class="sxs-lookup"><span data-stu-id="7ecd4-143">Click **OK** when prompted for confirmation.</span></span>






