#### <a name="to-create-a-new-service"></a><span data-ttu-id="d8ce4-101">To create a new service</span><span class="sxs-lookup"><span data-stu-id="d8ce4-101">To create a new service</span></span>
1. <span data-ttu-id="d8ce4-102">Using your Microsoft account credentials, log on to the Azure classic portal at this URL: [https://manage.windowsazure.com/](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="d8ce4-102">Using your Microsoft account credentials, log on to the Azure classic portal at this URL: [https://manage.windowsazure.com/](https://manage.windowsazure.com/).</span></span> <span data-ttu-id="d8ce4-103">If deploying the device in Government portal, log in at:  [https://manage.windowsazure.us/](https://manage.windowsazure.us/)</span><span class="sxs-lookup"><span data-stu-id="d8ce4-103">If deploying the device in Government portal, log in at:  [https://manage.windowsazure.us/](https://manage.windowsazure.us/)</span></span>
2. <span data-ttu-id="d8ce4-104">In the portal, click **New > Data Services > StorSimple Manager > Quick Create**.</span><span class="sxs-lookup"><span data-stu-id="d8ce4-104">In the portal, click **New > Data Services > StorSimple Manager > Quick Create**.</span></span>
3. <span data-ttu-id="d8ce4-105">In the form that is displayed, do the following:</span><span class="sxs-lookup"><span data-stu-id="d8ce4-105">In the form that is displayed, do the following:</span></span>
   
   1. <span data-ttu-id="d8ce4-106">Supply a unique **Name** for your service.</span><span class="sxs-lookup"><span data-stu-id="d8ce4-106">Supply a unique **Name** for your service.</span></span> <span data-ttu-id="d8ce4-107">This is a friendly name that can be used to identify the service.</span><span class="sxs-lookup"><span data-stu-id="d8ce4-107">This is a friendly name that can be used to identify the service.</span></span> <span data-ttu-id="d8ce4-108">The name can have between 2 and 50 characters that can be letters, numbers, and hyphens.</span><span class="sxs-lookup"><span data-stu-id="d8ce4-108">The name can have between 2 and 50 characters that can be letters, numbers, and hyphens.</span></span> <span data-ttu-id="d8ce4-109">The name must start and end with a letter or a number.</span><span class="sxs-lookup"><span data-stu-id="d8ce4-109">The name must start and end with a letter or a number.</span></span>
   2. <span data-ttu-id="d8ce4-110">For a service to manage a StorSimple virtual device, from the drop down list for **Managed devices type**, choose **Virtual device series**.</span><span class="sxs-lookup"><span data-stu-id="d8ce4-110">For a service to manage a StorSimple virtual device, from the drop down list for **Managed devices type**, choose **Virtual device series**.</span></span>
   3. <span data-ttu-id="d8ce4-111">Supply a **Location** for your service.</span><span class="sxs-lookup"><span data-stu-id="d8ce4-111">Supply a **Location** for your service.</span></span> <span data-ttu-id="d8ce4-112">Location refers to the geographical region where you want to deploy your device.</span><span class="sxs-lookup"><span data-stu-id="d8ce4-112">Location refers to the geographical region where you want to deploy your device.</span></span>
      
      * <span data-ttu-id="d8ce4-113">If you have other workloads in Azure that you intend to deploy with your StorSimple device, we recommend that you use that datacenter.</span><span class="sxs-lookup"><span data-stu-id="d8ce4-113">If you have other workloads in Azure that you intend to deploy with your StorSimple device, we recommend that you use that datacenter.</span></span>
      * <span data-ttu-id="d8ce4-114">The StorSimple Manager and Azure storage can be in two separate locations.</span><span class="sxs-lookup"><span data-stu-id="d8ce4-114">The StorSimple Manager and Azure storage can be in two separate locations.</span></span> <span data-ttu-id="d8ce4-115">In such a case, you are required to create the StorSimple Manager and Azure storage account separately.</span><span class="sxs-lookup"><span data-stu-id="d8ce4-115">In such a case, you are required to create the StorSimple Manager and Azure storage account separately.</span></span> <span data-ttu-id="d8ce4-116">To create an Azure storage account, go to the Azure Storage service in portal and follow the steps in [Create an Azure Storage account](../articles/storage/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="d8ce4-116">To create an Azure storage account, go to the Azure Storage service in portal and follow the steps in [Create an Azure Storage account](../articles/storage/storage-create-storage-account.md#create-a-storage-account).</span></span> <span data-ttu-id="d8ce4-117">After this account is created, add this account to the StorSimple Manager service by following the steps in [Configure a new storage account for the service](#optional-step-configure-a-new-storage-account-for-the-service).</span><span class="sxs-lookup"><span data-stu-id="d8ce4-117">After this account is created, add this account to the StorSimple Manager service by following the steps in [Configure a new storage account for the service](#optional-step-configure-a-new-storage-account-for-the-service).</span></span>
      * <span data-ttu-id="d8ce4-118">If deploying the virtual device in the Government Portal, the StorSimple Manager service is available in US Iowa and US Virginia locations.</span><span class="sxs-lookup"><span data-stu-id="d8ce4-118">If deploying the virtual device in the Government Portal, the StorSimple Manager service is available in US Iowa and US Virginia locations.</span></span>
   4. <span data-ttu-id="d8ce4-119">Choose a **Subscription** from the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="d8ce4-119">Choose a **Subscription** from the drop-down list.</span></span> <span data-ttu-id="d8ce4-120">The subscription is linked to your billing account.</span><span class="sxs-lookup"><span data-stu-id="d8ce4-120">The subscription is linked to your billing account.</span></span> <span data-ttu-id="d8ce4-121">This field is not present when you have only one subscription.</span><span class="sxs-lookup"><span data-stu-id="d8ce4-121">This field is not present when you have only one subscription.</span></span>
   5. <span data-ttu-id="d8ce4-122">Select **Create a new Azure storage account** to automatically create a storage account with the service.</span><span class="sxs-lookup"><span data-stu-id="d8ce4-122">Select **Create a new Azure storage account** to automatically create a storage account with the service.</span></span> <span data-ttu-id="d8ce4-123">This storage account will have a special name such as "storsimplebwv8c6dcnf".</span><span class="sxs-lookup"><span data-stu-id="d8ce4-123">This storage account will have a special name such as "storsimplebwv8c6dcnf".</span></span> <span data-ttu-id="d8ce4-124">If you need your data in a different location, clear this check box.</span><span class="sxs-lookup"><span data-stu-id="d8ce4-124">If you need your data in a different location, clear this check box.</span></span>
   6. <span data-ttu-id="d8ce4-125">Click **Create StorSimple Manager** to create the service.</span><span class="sxs-lookup"><span data-stu-id="d8ce4-125">Click **Create StorSimple Manager** to create the service.</span></span>
      
      ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/storsimple-ova-create-new-service/image1m-include.png)
   
   <span data-ttu-id="d8ce4-126">You will be directed to the **Service** landing page.</span><span class="sxs-lookup"><span data-stu-id="d8ce4-126">You will be directed to the **Service** landing page.</span></span> <span data-ttu-id="d8ce4-127">The service creation will take a few minutes.</span><span class="sxs-lookup"><span data-stu-id="d8ce4-127">The service creation will take a few minutes.</span></span> <span data-ttu-id="d8ce4-128">After the service is successfully created, you will be notified appropriately.</span><span class="sxs-lookup"><span data-stu-id="d8ce4-128">After the service is successfully created, you will be notified appropriately.</span></span>
   
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/storsimple-ova-create-new-service/image2-include.png)
   
   <span data-ttu-id="d8ce4-129">The status of the service will change to **Active**.</span><span class="sxs-lookup"><span data-stu-id="d8ce4-129">The status of the service will change to **Active**.</span></span>


