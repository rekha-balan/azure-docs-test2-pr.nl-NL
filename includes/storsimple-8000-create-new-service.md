<!--author=alkohli last changed:02/10/2017-->

---
title: include file
description: include file
services: storage
author: alkohli
ms.service: storage
ms.topic: include
ms.date: 08/20/2018
ms.author: alkohli
ms.custom: include file
---

#### <a name="to-create-a-new-service"></a><span data-ttu-id="2ff3b-103">To create a new service</span><span class="sxs-lookup"><span data-stu-id="2ff3b-103">To create a new service</span></span>

1. <span data-ttu-id="2ff3b-104">Use your Microsoft account credentials to sign in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="2ff3b-104">Use your Microsoft account credentials to sign in to the [Azure portal](https://portal.azure.com/).</span></span>

2. <span data-ttu-id="2ff3b-105">In the Azure portal, click **Create a resource** and then in the marketplace, click **See all**.</span><span class="sxs-lookup"><span data-stu-id="2ff3b-105">In the Azure portal, click **Create a resource** and then in the marketplace, click **See all**.</span></span>

    ![Create StorSimple Device Manager](./media/storsimple-8000-create-new-service/createssdevman1.png)

    <span data-ttu-id="2ff3b-107">Search for _StorSimple Physical_.</span><span class="sxs-lookup"><span data-stu-id="2ff3b-107">Search for _StorSimple Physical_.</span></span> <span data-ttu-id="2ff3b-108">Select and click **StorSimple Physical Device Series** and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="2ff3b-108">Select and click **StorSimple Physical Device Series** and then click **Create**.</span></span> <span data-ttu-id="2ff3b-109">Alternatively, in the Azure portal click **+** and then under **Storage**, click **StorSimple Physical Device Series**.</span><span class="sxs-lookup"><span data-stu-id="2ff3b-109">Alternatively, in the Azure portal click **+** and then under **Storage**, click **StorSimple Physical Device Series**.</span></span>

    ![Create StorSimple Device Manager](./media/storsimple-8000-create-new-service/createssdevman11.png)

3. <span data-ttu-id="2ff3b-111">In the **StorSimple Device Manager** blade, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="2ff3b-111">In the **StorSimple Device Manager** blade, do the following steps:</span></span>
   
   1. <span data-ttu-id="2ff3b-112">Supply a unique **Resource name** for your service.</span><span class="sxs-lookup"><span data-stu-id="2ff3b-112">Supply a unique **Resource name** for your service.</span></span> <span data-ttu-id="2ff3b-113">This name is a friendly name that can be used to identify the service.</span><span class="sxs-lookup"><span data-stu-id="2ff3b-113">This name is a friendly name that can be used to identify the service.</span></span> <span data-ttu-id="2ff3b-114">The name can have between 2 and 50 characters that can be letters, numbers, and hyphens.</span><span class="sxs-lookup"><span data-stu-id="2ff3b-114">The name can have between 2 and 50 characters that can be letters, numbers, and hyphens.</span></span> <span data-ttu-id="2ff3b-115">The name must start and end with a letter or a number.</span><span class="sxs-lookup"><span data-stu-id="2ff3b-115">The name must start and end with a letter or a number.</span></span>

   2. <span data-ttu-id="2ff3b-116">Choose a **Subscription** from the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="2ff3b-116">Choose a **Subscription** from the drop-down list.</span></span> <span data-ttu-id="2ff3b-117">The subscription is linked to your billing account.</span><span class="sxs-lookup"><span data-stu-id="2ff3b-117">The subscription is linked to your billing account.</span></span> <span data-ttu-id="2ff3b-118">This field is not present if you have only one subscription.</span><span class="sxs-lookup"><span data-stu-id="2ff3b-118">This field is not present if you have only one subscription.</span></span>

   3. <span data-ttu-id="2ff3b-119">For **Resource group**, **Use existing** or **Create new** group.</span><span class="sxs-lookup"><span data-stu-id="2ff3b-119">For **Resource group**, **Use existing** or **Create new** group.</span></span> <span data-ttu-id="2ff3b-120">For more information, see [Azure resource groups](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-infrastructure-resource-groups-guidelines/).</span><span class="sxs-lookup"><span data-stu-id="2ff3b-120">For more information, see [Azure resource groups](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-infrastructure-resource-groups-guidelines/).</span></span>
   
   4. <span data-ttu-id="2ff3b-121">Supply a **Location** for your service.</span><span class="sxs-lookup"><span data-stu-id="2ff3b-121">Supply a **Location** for your service.</span></span> <span data-ttu-id="2ff3b-122">In general, choose a location closest to the geographical region where you want to deploy your device.</span><span class="sxs-lookup"><span data-stu-id="2ff3b-122">In general, choose a location closest to the geographical region where you want to deploy your device.</span></span> <span data-ttu-id="2ff3b-123">You may also want to factor in the following considerations:</span><span class="sxs-lookup"><span data-stu-id="2ff3b-123">You may also want to factor in the following considerations:</span></span> 
      
      * <span data-ttu-id="2ff3b-124">If you have existing workloads in Azure that you also intend to deploy with your StorSimple device, you should use that datacenter.</span><span class="sxs-lookup"><span data-stu-id="2ff3b-124">If you have existing workloads in Azure that you also intend to deploy with your StorSimple device, you should use that datacenter.</span></span>
      * <span data-ttu-id="2ff3b-125">Your StorSimple Device Manager service and Azure storage can be in two separate locations.</span><span class="sxs-lookup"><span data-stu-id="2ff3b-125">Your StorSimple Device Manager service and Azure storage can be in two separate locations.</span></span> <span data-ttu-id="2ff3b-126">In such a case, you are required to create the StorSimple Device Manager and Azure storage account separately.</span><span class="sxs-lookup"><span data-stu-id="2ff3b-126">In such a case, you are required to create the StorSimple Device Manager and Azure storage account separately.</span></span> <span data-ttu-id="2ff3b-127">To create an Azure storage account, go to the Azure Storage service in the Azure portal and follow the steps in [Create an Azure Storage account](../articles/storage/common/storage-quickstart-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="2ff3b-127">To create an Azure storage account, go to the Azure Storage service in the Azure portal and follow the steps in [Create an Azure Storage account](../articles/storage/common/storage-quickstart-create-account.md).</span></span> <span data-ttu-id="2ff3b-128">After you create this account, add it to the StorSimple Device Manager service by following the steps in [Configure a new storage account for the service](../articles/storsimple/storsimple-8000-deployment-walkthrough-u2.md#configure-a-new-storage-account-for-the-service).</span><span class="sxs-lookup"><span data-stu-id="2ff3b-128">After you create this account, add it to the StorSimple Device Manager service by following the steps in [Configure a new storage account for the service](../articles/storsimple/storsimple-8000-deployment-walkthrough-u2.md#configure-a-new-storage-account-for-the-service).</span></span>

   5. <span data-ttu-id="2ff3b-129">Select **Create a new storage account** to automatically create a storage account with the service.</span><span class="sxs-lookup"><span data-stu-id="2ff3b-129">Select **Create a new storage account** to automatically create a storage account with the service.</span></span> <span data-ttu-id="2ff3b-130">Specify a name for this storage account.</span><span class="sxs-lookup"><span data-stu-id="2ff3b-130">Specify a name for this storage account.</span></span> <span data-ttu-id="2ff3b-131">If you need your data in a different location, uncheck this box.</span><span class="sxs-lookup"><span data-stu-id="2ff3b-131">If you need your data in a different location, uncheck this box.</span></span>

   6. <span data-ttu-id="2ff3b-132">Check **Pin to dashboard** if you want a quick link to this service on your dashboard.</span><span class="sxs-lookup"><span data-stu-id="2ff3b-132">Check **Pin to dashboard** if you want a quick link to this service on your dashboard.</span></span>
      
   7. <span data-ttu-id="2ff3b-133">Click **Create** to create the StorSimple Device Manager.</span><span class="sxs-lookup"><span data-stu-id="2ff3b-133">Click **Create** to create the StorSimple Device Manager.</span></span>

       ![Create StorSimple Device Manager](./media/storsimple-8000-create-new-service/createssdevman2.png)
   
<span data-ttu-id="2ff3b-135">The service creation takes a few minutes.</span><span class="sxs-lookup"><span data-stu-id="2ff3b-135">The service creation takes a few minutes.</span></span> <span data-ttu-id="2ff3b-136">After the service is successfully created, you will see a notification and the new service blade opens up.</span><span class="sxs-lookup"><span data-stu-id="2ff3b-136">After the service is successfully created, you will see a notification and the new service blade opens up.</span></span>
   
![Create StorSimple Device Manager](./media/storsimple-8000-create-new-service/createssdevman5.png)


