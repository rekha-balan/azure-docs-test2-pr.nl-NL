---
title: Deploy StorSimple Device Manager service | Microsoft Docs
description: Explains how to create and delete the StorSimple Device Manager service in the Azure portal, and describes how to manage the service registration key.
services: storsimple
documentationcenter: ''
author: alkohli
manager: carmonm
editor: ''
ms.assetid: 28499494-8c4d-4a7f-9d44-94b2b8a93c93
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/29/2016
ms.author: alkohli
ms.openlocfilehash: aaef3aeb9e9a3982c722c69f4a50c4c8d15b3486
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554073"
---
# <a name="deploy-the-storsimple-device-manager-service-for-storsimple-virtual-array"></a><span data-ttu-id="76596-103">Deploy the StorSimple Device Manager service for StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="76596-103">Deploy the StorSimple Device Manager service for StorSimple Virtual Array</span></span>
## <a name="overview"></a><span data-ttu-id="76596-104">Overview</span><span class="sxs-lookup"><span data-stu-id="76596-104">Overview</span></span>

<span data-ttu-id="76596-105">The StorSimple Device Manager service runs in Microsoft Azure and connects to multiple StorSimple devices.</span><span class="sxs-lookup"><span data-stu-id="76596-105">The StorSimple Device Manager service runs in Microsoft Azure and connects to multiple StorSimple devices.</span></span> <span data-ttu-id="76596-106">After you create the service, you can use it to manage the devices from the Microsoft Azure portal running in a browser.</span><span class="sxs-lookup"><span data-stu-id="76596-106">After you create the service, you can use it to manage the devices from the Microsoft Azure portal running in a browser.</span></span> <span data-ttu-id="76596-107">This allows you to monitor all the devices that are connected to the StorSimple Device Manager service from a single, central location, thereby minimizing administrative burden.</span><span class="sxs-lookup"><span data-stu-id="76596-107">This allows you to monitor all the devices that are connected to the StorSimple Device Manager service from a single, central location, thereby minimizing administrative burden.</span></span>

<span data-ttu-id="76596-108">The common tasks related to a StorSimple Device Manager service are:</span><span class="sxs-lookup"><span data-stu-id="76596-108">The common tasks related to a StorSimple Device Manager service are:</span></span>

* <span data-ttu-id="76596-109">Create a service</span><span class="sxs-lookup"><span data-stu-id="76596-109">Create a service</span></span>
* <span data-ttu-id="76596-110">Delete a service</span><span class="sxs-lookup"><span data-stu-id="76596-110">Delete a service</span></span>
* <span data-ttu-id="76596-111">Get the service registration key</span><span class="sxs-lookup"><span data-stu-id="76596-111">Get the service registration key</span></span>
* <span data-ttu-id="76596-112">Regenerate the service registration key</span><span class="sxs-lookup"><span data-stu-id="76596-112">Regenerate the service registration key</span></span>

<span data-ttu-id="76596-113">This tutorial describes how to perform each of the preceding tasks.</span><span class="sxs-lookup"><span data-stu-id="76596-113">This tutorial describes how to perform each of the preceding tasks.</span></span> <span data-ttu-id="76596-114">The information contained in this article is applicable only to StorSimple Virtual Arrays.</span><span class="sxs-lookup"><span data-stu-id="76596-114">The information contained in this article is applicable only to StorSimple Virtual Arrays.</span></span> <span data-ttu-id="76596-115">For more information on StorSimple 8000 series, go to [deploy a StorSimple Manager service](storsimple-manage-service.md).</span><span class="sxs-lookup"><span data-stu-id="76596-115">For more information on StorSimple 8000 series, go to [deploy a StorSimple Manager service](storsimple-manage-service.md).</span></span>

## <a name="create-a-service"></a><span data-ttu-id="76596-116">Create a service</span><span class="sxs-lookup"><span data-stu-id="76596-116">Create a service</span></span>

<span data-ttu-id="76596-117">To create a service, you need to have:</span><span class="sxs-lookup"><span data-stu-id="76596-117">To create a service, you need to have:</span></span>

* <span data-ttu-id="76596-118">A subscription with an Enterprise Agreement</span><span class="sxs-lookup"><span data-stu-id="76596-118">A subscription with an Enterprise Agreement</span></span>
* <span data-ttu-id="76596-119">An active Microsoft Azure storage account</span><span class="sxs-lookup"><span data-stu-id="76596-119">An active Microsoft Azure storage account</span></span>
* <span data-ttu-id="76596-120">The billing information that is used for access management</span><span class="sxs-lookup"><span data-stu-id="76596-120">The billing information that is used for access management</span></span>

<span data-ttu-id="76596-121">You can also choose to generate a storage account when you create the service.</span><span class="sxs-lookup"><span data-stu-id="76596-121">You can also choose to generate a storage account when you create the service.</span></span>

<span data-ttu-id="76596-122">A single service can manage multiple devices.</span><span class="sxs-lookup"><span data-stu-id="76596-122">A single service can manage multiple devices.</span></span> <span data-ttu-id="76596-123">However, a device cannot span multiple services.</span><span class="sxs-lookup"><span data-stu-id="76596-123">However, a device cannot span multiple services.</span></span> <span data-ttu-id="76596-124">A large enterprise can have multiple service instances to work with different subscriptions, organizations, or even deployment locations.</span><span class="sxs-lookup"><span data-stu-id="76596-124">A large enterprise can have multiple service instances to work with different subscriptions, organizations, or even deployment locations.</span></span>

> [!NOTE]
> <span data-ttu-id="76596-125">You need separate instances of StorSimple Device Manager service to manage StorSimple 8000 series devices and StorSimple Virtual Arrays.</span><span class="sxs-lookup"><span data-stu-id="76596-125">You need separate instances of StorSimple Device Manager service to manage StorSimple 8000 series devices and StorSimple Virtual Arrays.</span></span>


<span data-ttu-id="76596-126">Perform the following steps to create a service.</span><span class="sxs-lookup"><span data-stu-id="76596-126">Perform the following steps to create a service.</span></span>

[!INCLUDE [storsimple-virtual-array-create-new-service](../../includes/storsimple-virtual-array-create-new-service.md)]

## <a name="delete-a-service"></a><span data-ttu-id="76596-127">Delete a service</span><span class="sxs-lookup"><span data-stu-id="76596-127">Delete a service</span></span>

<span data-ttu-id="76596-128">Before you delete a service, make sure that no connected devices are using it.</span><span class="sxs-lookup"><span data-stu-id="76596-128">Before you delete a service, make sure that no connected devices are using it.</span></span> <span data-ttu-id="76596-129">If the service is in use, deactivate the connected devices.</span><span class="sxs-lookup"><span data-stu-id="76596-129">If the service is in use, deactivate the connected devices.</span></span> <span data-ttu-id="76596-130">The deactivate operation will sever the connection between the device and the service, but preserve the device data in the cloud.</span><span class="sxs-lookup"><span data-stu-id="76596-130">The deactivate operation will sever the connection between the device and the service, but preserve the device data in the cloud.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="76596-131">After a service is deleted, the operation cannot be reversed.</span><span class="sxs-lookup"><span data-stu-id="76596-131">After a service is deleted, the operation cannot be reversed.</span></span> <span data-ttu-id="76596-132">Any device that was using the service will need to be factory reset before it can be used with another service.</span><span class="sxs-lookup"><span data-stu-id="76596-132">Any device that was using the service will need to be factory reset before it can be used with another service.</span></span> <span data-ttu-id="76596-133">In this scenario, the local data on the device, as well as the configuration, will be lost.</span><span class="sxs-lookup"><span data-stu-id="76596-133">In this scenario, the local data on the device, as well as the configuration, will be lost.</span></span>
 

<span data-ttu-id="76596-134">Perform the following steps to delete a service.</span><span class="sxs-lookup"><span data-stu-id="76596-134">Perform the following steps to delete a service.</span></span>

#### <a name="to-delete-a-service"></a><span data-ttu-id="76596-135">To delete a service</span><span class="sxs-lookup"><span data-stu-id="76596-135">To delete a service</span></span>

1. <span data-ttu-id="76596-136">Go to **All resources**.</span><span class="sxs-lookup"><span data-stu-id="76596-136">Go to **All resources**.</span></span> <span data-ttu-id="76596-137">Search for your StorSimple Device Manager service.</span><span class="sxs-lookup"><span data-stu-id="76596-137">Search for your StorSimple Device Manager service.</span></span> <span data-ttu-id="76596-138">Select the service that you wish to delete.</span><span class="sxs-lookup"><span data-stu-id="76596-138">Select the service that you wish to delete.</span></span>
   
    ![Select service to delete](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-manage-service/deleteservice2.png)
2. <span data-ttu-id="76596-140">Go to your service dashboard to ensure there are no devices connected to the service.</span><span class="sxs-lookup"><span data-stu-id="76596-140">Go to your service dashboard to ensure there are no devices connected to the service.</span></span> <span data-ttu-id="76596-141">If there are no devices registered with this service, you will also see a banner message to the effect.</span><span class="sxs-lookup"><span data-stu-id="76596-141">If there are no devices registered with this service, you will also see a banner message to the effect.</span></span> <span data-ttu-id="76596-142">Click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="76596-142">Click **Delete**.</span></span>
   
    ![Delete service](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-manage-service/deleteservice3.png)

3. <span data-ttu-id="76596-144">When prompted for confirmation, click **Yes** in the confirmation notification.</span><span class="sxs-lookup"><span data-stu-id="76596-144">When prompted for confirmation, click **Yes** in the confirmation notification.</span></span> 
   
    ![Confirm service deletion](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-manage-service/deleteservice4.png)
4. <span data-ttu-id="76596-146">It may take a few minutes for the service to be deleted.</span><span class="sxs-lookup"><span data-stu-id="76596-146">It may take a few minutes for the service to be deleted.</span></span> <span data-ttu-id="76596-147">After the service is successfully deleted, you will be notified.</span><span class="sxs-lookup"><span data-stu-id="76596-147">After the service is successfully deleted, you will be notified.</span></span>
   
    ![Successful service deletion](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-manage-service/deleteservice6.png)

<span data-ttu-id="76596-149">The list of services will be refreshed.</span><span class="sxs-lookup"><span data-stu-id="76596-149">The list of services will be refreshed.</span></span>

 ![Updated list of services](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-manage-service/deleteservice7.png)

## <a name="get-the-service-registration-key"></a><span data-ttu-id="76596-151">Get the service registration key</span><span class="sxs-lookup"><span data-stu-id="76596-151">Get the service registration key</span></span>
<span data-ttu-id="76596-152">After you have successfully created a service, you will need to register your StorSimple device with the service.</span><span class="sxs-lookup"><span data-stu-id="76596-152">After you have successfully created a service, you will need to register your StorSimple device with the service.</span></span> <span data-ttu-id="76596-153">To register your first StorSimple device, you will need the service registration key.</span><span class="sxs-lookup"><span data-stu-id="76596-153">To register your first StorSimple device, you will need the service registration key.</span></span> <span data-ttu-id="76596-154">To register additional devices with an existing StorSimple service, you will need both the registration key and the service data encryption key (which is generated on the first device during registration).</span><span class="sxs-lookup"><span data-stu-id="76596-154">To register additional devices with an existing StorSimple service, you will need both the registration key and the service data encryption key (which is generated on the first device during registration).</span></span> <span data-ttu-id="76596-155">For more information about the service data encryption key, see [StorSimple security](storsimple-security.md).</span><span class="sxs-lookup"><span data-stu-id="76596-155">For more information about the service data encryption key, see [StorSimple security](storsimple-security.md).</span></span> <span data-ttu-id="76596-156">You can get the registration key by accessing the **Keys** blade for your service.</span><span class="sxs-lookup"><span data-stu-id="76596-156">You can get the registration key by accessing the **Keys** blade for your service.</span></span>

<span data-ttu-id="76596-157">Perform the following steps to get the service registration key.</span><span class="sxs-lookup"><span data-stu-id="76596-157">Perform the following steps to get the service registration key.</span></span>

#### <a name="to-get-the-service-registration-key"></a><span data-ttu-id="76596-158">To get the service registration key</span><span class="sxs-lookup"><span data-stu-id="76596-158">To get the service registration key</span></span>
1. <span data-ttu-id="76596-159">In the **StorSimple Device Manager** blade, go to **Management &gt;** **Keys**.</span><span class="sxs-lookup"><span data-stu-id="76596-159">In the **StorSimple Device Manager** blade, go to **Management &gt;** **Keys**.</span></span>
   
   ![Keys blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-manage-service/getregkey2.png)
2. <span data-ttu-id="76596-161">In the **Keys** blade, a service registration key appears.</span><span class="sxs-lookup"><span data-stu-id="76596-161">In the **Keys** blade, a service registration key appears.</span></span> <span data-ttu-id="76596-162">Copy the registration key using the copy icon.</span><span class="sxs-lookup"><span data-stu-id="76596-162">Copy the registration key using the copy icon.</span></span> 

<span data-ttu-id="76596-163">Keep the service registration key in a safe location.</span><span class="sxs-lookup"><span data-stu-id="76596-163">Keep the service registration key in a safe location.</span></span> <span data-ttu-id="76596-164">You will need this key, as well as the service data encryption key, to register additional devices with this service.</span><span class="sxs-lookup"><span data-stu-id="76596-164">You will need this key, as well as the service data encryption key, to register additional devices with this service.</span></span> <span data-ttu-id="76596-165">After obtaining the service registration key, you will need to configure your device through the Windows PowerShell for StorSimple interface.</span><span class="sxs-lookup"><span data-stu-id="76596-165">After obtaining the service registration key, you will need to configure your device through the Windows PowerShell for StorSimple interface.</span></span>

## <a name="regenerate-the-service-registration-key"></a><span data-ttu-id="76596-166">Regenerate the service registration key</span><span class="sxs-lookup"><span data-stu-id="76596-166">Regenerate the service registration key</span></span>
<span data-ttu-id="76596-167">You will need to regenerate a service registration key if you are required to perform key rotation or if the list of service administrators has changed.</span><span class="sxs-lookup"><span data-stu-id="76596-167">You will need to regenerate a service registration key if you are required to perform key rotation or if the list of service administrators has changed.</span></span> <span data-ttu-id="76596-168">When you regenerate the key, the new key is used only for registering subsequent devices.</span><span class="sxs-lookup"><span data-stu-id="76596-168">When you regenerate the key, the new key is used only for registering subsequent devices.</span></span> <span data-ttu-id="76596-169">The devices that were already registered are unaffected by this process.</span><span class="sxs-lookup"><span data-stu-id="76596-169">The devices that were already registered are unaffected by this process.</span></span>

<span data-ttu-id="76596-170">Perform the following steps to regenerate a service registration key.</span><span class="sxs-lookup"><span data-stu-id="76596-170">Perform the following steps to regenerate a service registration key.</span></span>

#### <a name="to-regenerate-the-service-registration-key"></a><span data-ttu-id="76596-171">To regenerate the service registration key</span><span class="sxs-lookup"><span data-stu-id="76596-171">To regenerate the service registration key</span></span>
1. <span data-ttu-id="76596-172">In the **StorSimple Device Manager** blade, go to **Management &gt;** **Keys**.</span><span class="sxs-lookup"><span data-stu-id="76596-172">In the **StorSimple Device Manager** blade, go to **Management &gt;** **Keys**.</span></span>
   
   ![Keys blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-manage-service/getregkey2.png)
2. <span data-ttu-id="76596-174">In the **Keys** blade, click **Regenerate**.</span><span class="sxs-lookup"><span data-stu-id="76596-174">In the **Keys** blade, click **Regenerate**.</span></span>
   
   ![Click regenerate](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-manage-service/getregkey5.png)
3. <span data-ttu-id="76596-176">In the **Regenerate service registration key** blade, review the action required when the keys are regenerated.</span><span class="sxs-lookup"><span data-stu-id="76596-176">In the **Regenerate service registration key** blade, review the action required when the keys are regenerated.</span></span> <span data-ttu-id="76596-177">All the subsequent devices that are registered with this service will use the new registration key.</span><span class="sxs-lookup"><span data-stu-id="76596-177">All the subsequent devices that are registered with this service will use the new registration key.</span></span> <span data-ttu-id="76596-178">Click **Regenerate** to confirm.</span><span class="sxs-lookup"><span data-stu-id="76596-178">Click **Regenerate** to confirm.</span></span> <span data-ttu-id="76596-179">You will be notified after the registration is complete.</span><span class="sxs-lookup"><span data-stu-id="76596-179">You will be notified after the registration is complete.</span></span>
   
   ![Confirm regenerate key](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-manage-service/getregkey3.png)
4. <span data-ttu-id="76596-181">A new service registration key will appear.</span><span class="sxs-lookup"><span data-stu-id="76596-181">A new service registration key will appear.</span></span>
   
    ![Confirm regenerate key](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-manage-service/getregkey4.png)
   
   <span data-ttu-id="76596-183">Copy this key and save it for registering any new devices with this service.</span><span class="sxs-lookup"><span data-stu-id="76596-183">Copy this key and save it for registering any new devices with this service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="76596-184">Next steps</span><span class="sxs-lookup"><span data-stu-id="76596-184">Next steps</span></span>
* <span data-ttu-id="76596-185">Learn how to [get started](storsimple-virtual-array-deploy1-portal-prep.md) with a StorSimple Virtual Array.</span><span class="sxs-lookup"><span data-stu-id="76596-185">Learn how to [get started](storsimple-virtual-array-deploy1-portal-prep.md) with a StorSimple Virtual Array.</span></span>
* <span data-ttu-id="76596-186">Learn how to [administer your StorSimple device](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="76596-186">Learn how to [administer your StorSimple device](storsimple-ova-web-ui-admin.md).</span></span>











