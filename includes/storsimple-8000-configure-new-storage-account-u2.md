<!--author=alkohli last changed: 01/20/17-->


#### <a name="to-add-a-storage-account-credential-in-the-same-azure-subscription-as-the-storsimple-device-manager-service"></a><span data-ttu-id="19e2e-101">To add a storage account credential in the same Azure subscription as the StorSimple Device Manager service</span><span class="sxs-lookup"><span data-stu-id="19e2e-101">To add a storage account credential in the same Azure subscription as the StorSimple Device Manager service</span></span>

1. <span data-ttu-id="19e2e-102">Go to your StorSimple Device Manager service.</span><span class="sxs-lookup"><span data-stu-id="19e2e-102">Go to your StorSimple Device Manager service.</span></span> <span data-ttu-id="19e2e-103">In the **Configuration** section, click **Storage account credentials**.</span><span class="sxs-lookup"><span data-stu-id="19e2e-103">In the **Configuration** section, click **Storage account credentials**.</span></span>

    ![Storage account credentials](./media/storsimple-8000-configure-new-storage-account-u2/createnewstorageacct1.png)

2. <span data-ttu-id="19e2e-105">On the **Storage account credentials** blade, click **+ Add**.</span><span class="sxs-lookup"><span data-stu-id="19e2e-105">On the **Storage account credentials** blade, click **+ Add**.</span></span>

    ![Add a storage account credential](./media/storsimple-8000-configure-new-storage-account-u2/createnewstorageacct2.png)

3. <span data-ttu-id="19e2e-107">In the **Add a storage account credential** blade, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="19e2e-107">In the **Add a storage account credential** blade, do the following steps:</span></span>

    1. <span data-ttu-id="19e2e-108">As you are adding a storage account credential in the same Azure subscription as your service, ensure that **Current** is selected.</span><span class="sxs-lookup"><span data-stu-id="19e2e-108">As you are adding a storage account credential in the same Azure subscription as your service, ensure that **Current** is selected.</span></span>

    2. <span data-ttu-id="19e2e-109">From the **storage account** dropdown list, select an existing storage account.</span><span class="sxs-lookup"><span data-stu-id="19e2e-109">From the **storage account** dropdown list, select an existing storage account.</span></span>

    3. <span data-ttu-id="19e2e-110">Based on the storage account selected, the **location** will be displayed (grayed out and cannot be changed here).</span><span class="sxs-lookup"><span data-stu-id="19e2e-110">Based on the storage account selected, the **location** will be displayed (grayed out and cannot be changed here).</span></span>

    4. <span data-ttu-id="19e2e-111">Select **Enable SSL Mode** to create a secure channel for network communication between your device and the cloud.</span><span class="sxs-lookup"><span data-stu-id="19e2e-111">Select **Enable SSL Mode** to create a secure channel for network communication between your device and the cloud.</span></span> <span data-ttu-id="19e2e-112">Disable **Enable SSL** only if you are operating within a private cloud.</span><span class="sxs-lookup"><span data-stu-id="19e2e-112">Disable **Enable SSL** only if you are operating within a private cloud.</span></span>

        ![Add storage account credentials blade](./media/storsimple-8000-configure-new-storage-account-u2/createnewstorageacct3.png)

    5. <span data-ttu-id="19e2e-114">Click **Add** to start the job creation for the storage account credential.</span><span class="sxs-lookup"><span data-stu-id="19e2e-114">Click **Add** to start the job creation for the storage account credential.</span></span> <span data-ttu-id="19e2e-115">You will be notified after the storage account credential is successfully created.</span><span class="sxs-lookup"><span data-stu-id="19e2e-115">You will be notified after the storage account credential is successfully created.</span></span>

        ![Success notification for storage account credentials](./media/storsimple-8000-configure-new-storage-account-u2/createnewstorageacct5.png)

<span data-ttu-id="19e2e-117">The newly created storage account credential will be displayed under the list of **Storage account credentials**.</span><span class="sxs-lookup"><span data-stu-id="19e2e-117">The newly created storage account credential will be displayed under the list of **Storage account credentials**.</span></span>

![List of storage account credentials](./media/storsimple-8000-configure-new-storage-account-u2/createnewstorageacct6.png)

