---
title: Deploy the StorSimple Manager service for StorSimple virtual array| Microsoft Docs
description: Explains how to create and delete the StorSimple Manager service in the Azure classic portal, and describes how to manage the service registration key.
services: storsimple
documentationcenter: ''
author: alkohli
manager: carmonm
editor: ''
ms.assetid: 40084881-ad8d-440f-a365-68259beee616
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/19/2016
ms.author: alkohli
ms.openlocfilehash: daf168845df982bc615c470a29f35cc9dbc9ab3a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553028"
---
# <a name="deploy-the-storsimple-manager-service-for-storsimple-virtual-array"></a><span data-ttu-id="bf3f0-103">Deploy the StorSimple Manager service for StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="bf3f0-103">Deploy the StorSimple Manager service for StorSimple Virtual Array</span></span>
## <a name="overview"></a><span data-ttu-id="bf3f0-104">Overview</span><span class="sxs-lookup"><span data-stu-id="bf3f0-104">Overview</span></span>
<span data-ttu-id="bf3f0-105">The StorSimple Manager service runs in Microsoft Azure and connects to multiple StorSimple devices.</span><span class="sxs-lookup"><span data-stu-id="bf3f0-105">The StorSimple Manager service runs in Microsoft Azure and connects to multiple StorSimple devices.</span></span> <span data-ttu-id="bf3f0-106">After you create the service, you can use it to manage the devices from the Microsoft Azure classic portal running in a browser.</span><span class="sxs-lookup"><span data-stu-id="bf3f0-106">After you create the service, you can use it to manage the devices from the Microsoft Azure classic portal running in a browser.</span></span> <span data-ttu-id="bf3f0-107">This allows you to monitor all the devices that are connected to the StorSimple Manager service from a single, central location, thereby minimizing administrative burden.</span><span class="sxs-lookup"><span data-stu-id="bf3f0-107">This allows you to monitor all the devices that are connected to the StorSimple Manager service from a single, central location, thereby minimizing administrative burden.</span></span>

<span data-ttu-id="bf3f0-108">The StorSimple Manager landing page lists all the StorSimple Manager services that you can use to manage your StorSimple storage devices.</span><span class="sxs-lookup"><span data-stu-id="bf3f0-108">The StorSimple Manager landing page lists all the StorSimple Manager services that you can use to manage your StorSimple storage devices.</span></span> <span data-ttu-id="bf3f0-109">For each StorSimple Manager service, the following information is presented on the StorSimple Manager page:</span><span class="sxs-lookup"><span data-stu-id="bf3f0-109">For each StorSimple Manager service, the following information is presented on the StorSimple Manager page:</span></span>

* <span data-ttu-id="bf3f0-110">**Name** – The name that was assigned to your StorSimple Manager service when it was created.</span><span class="sxs-lookup"><span data-stu-id="bf3f0-110">**Name** – The name that was assigned to your StorSimple Manager service when it was created.</span></span> <span data-ttu-id="bf3f0-111">The service name cannot be changed after the service is created.</span><span class="sxs-lookup"><span data-stu-id="bf3f0-111">The service name cannot be changed after the service is created.</span></span>
* <span data-ttu-id="bf3f0-112">**Status** – The status of the service, which can be **Active**, **Creating**, or **Online**.</span><span class="sxs-lookup"><span data-stu-id="bf3f0-112">**Status** – The status of the service, which can be **Active**, **Creating**, or **Online**.</span></span>
* <span data-ttu-id="bf3f0-113">**Location** – The geographical location in which the StorSimple device will be deployed.</span><span class="sxs-lookup"><span data-stu-id="bf3f0-113">**Location** – The geographical location in which the StorSimple device will be deployed.</span></span>
* <span data-ttu-id="bf3f0-114">**Subscription** – The billing subscription that is associated with your service.</span><span class="sxs-lookup"><span data-stu-id="bf3f0-114">**Subscription** – The billing subscription that is associated with your service.</span></span>

<span data-ttu-id="bf3f0-115">The common tasks that can be performed through the StorSimple Manager page are:</span><span class="sxs-lookup"><span data-stu-id="bf3f0-115">The common tasks that can be performed through the StorSimple Manager page are:</span></span>

* <span data-ttu-id="bf3f0-116">Create a service</span><span class="sxs-lookup"><span data-stu-id="bf3f0-116">Create a service</span></span>
* <span data-ttu-id="bf3f0-117">Delete a service</span><span class="sxs-lookup"><span data-stu-id="bf3f0-117">Delete a service</span></span>
* <span data-ttu-id="bf3f0-118">Get the service registration key</span><span class="sxs-lookup"><span data-stu-id="bf3f0-118">Get the service registration key</span></span>
* <span data-ttu-id="bf3f0-119">Regenerate the service registration key</span><span class="sxs-lookup"><span data-stu-id="bf3f0-119">Regenerate the service registration key</span></span>

<span data-ttu-id="bf3f0-120">This tutorial describes how to perform each of these tasks.</span><span class="sxs-lookup"><span data-stu-id="bf3f0-120">This tutorial describes how to perform each of these tasks.</span></span> <span data-ttu-id="bf3f0-121">The information contained in this article is applicable only to StorSimple Virtual Arrays.</span><span class="sxs-lookup"><span data-stu-id="bf3f0-121">The information contained in this article is applicable only to StorSimple Virtual Arrays.</span></span> <span data-ttu-id="bf3f0-122">For more information on StorSimple 8000 series, go to [deploy a StorSimple Manager service](storsimple-manage-service.md).</span><span class="sxs-lookup"><span data-stu-id="bf3f0-122">For more information on StorSimple 8000 series, go to [deploy a StorSimple Manager service](storsimple-manage-service.md).</span></span>

## <a name="create-a-service"></a><span data-ttu-id="bf3f0-123">Create a service</span><span class="sxs-lookup"><span data-stu-id="bf3f0-123">Create a service</span></span>
<span data-ttu-id="bf3f0-124">Use the **Quick Create** option to create a StorSimple Manager service if you want to deploy your StorSimple device.</span><span class="sxs-lookup"><span data-stu-id="bf3f0-124">Use the **Quick Create** option to create a StorSimple Manager service if you want to deploy your StorSimple device.</span></span> <span data-ttu-id="bf3f0-125">To create a service, you need to have:</span><span class="sxs-lookup"><span data-stu-id="bf3f0-125">To create a service, you need to have:</span></span>

* <span data-ttu-id="bf3f0-126">A subscription with an Enterprise Agreement</span><span class="sxs-lookup"><span data-stu-id="bf3f0-126">A subscription with an Enterprise Agreement</span></span>
* <span data-ttu-id="bf3f0-127">An active Microsoft Azure storage account</span><span class="sxs-lookup"><span data-stu-id="bf3f0-127">An active Microsoft Azure storage account</span></span>
* <span data-ttu-id="bf3f0-128">The billing information that is used for access management</span><span class="sxs-lookup"><span data-stu-id="bf3f0-128">The billing information that is used for access management</span></span>

<span data-ttu-id="bf3f0-129">You can also choose to generate a default storage account when you create the service.</span><span class="sxs-lookup"><span data-stu-id="bf3f0-129">You can also choose to generate a default storage account when you create the service.</span></span>

<span data-ttu-id="bf3f0-130">A single service can manage multiple devices.</span><span class="sxs-lookup"><span data-stu-id="bf3f0-130">A single service can manage multiple devices.</span></span> <span data-ttu-id="bf3f0-131">However, a device cannot span multiple services.</span><span class="sxs-lookup"><span data-stu-id="bf3f0-131">However, a device cannot span multiple services.</span></span> <span data-ttu-id="bf3f0-132">A large enterprise can have multiple service instances to work with different subscriptions, organizations, or even deployment locations.</span><span class="sxs-lookup"><span data-stu-id="bf3f0-132">A large enterprise can have multiple service instances to work with different subscriptions, organizations, or even deployment locations.</span></span>  

> [!NOTE]
> <span data-ttu-id="bf3f0-133">You need separate instances of StorSimple Manager service to manage StorSimple 8000 series devices and StorSimple Virtual Arrays.</span><span class="sxs-lookup"><span data-stu-id="bf3f0-133">You need separate instances of StorSimple Manager service to manage StorSimple 8000 series devices and StorSimple Virtual Arrays.</span></span>
> 
> 

<span data-ttu-id="bf3f0-134">Perform the following steps to create a service.</span><span class="sxs-lookup"><span data-stu-id="bf3f0-134">Perform the following steps to create a service.</span></span>

[!INCLUDE [storsimple-ova-create-new-service](../../includes/storsimple-ova-create-new-service.md)]

## <a name="delete-a-service"></a><span data-ttu-id="bf3f0-135">Delete a service</span><span class="sxs-lookup"><span data-stu-id="bf3f0-135">Delete a service</span></span>
<span data-ttu-id="bf3f0-136">Before you delete a service, make sure that no connected devices are using it.</span><span class="sxs-lookup"><span data-stu-id="bf3f0-136">Before you delete a service, make sure that no connected devices are using it.</span></span> <span data-ttu-id="bf3f0-137">If the service is in use, deactivate the connected devices.</span><span class="sxs-lookup"><span data-stu-id="bf3f0-137">If the service is in use, deactivate the connected devices.</span></span> <span data-ttu-id="bf3f0-138">The deactivate operation will sever the connection between the device and the service, but preserve the device data in the cloud.</span><span class="sxs-lookup"><span data-stu-id="bf3f0-138">The deactivate operation will sever the connection between the device and the service, but preserve the device data in the cloud.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="bf3f0-139">After a service is deleted, the operation cannot be reversed.</span><span class="sxs-lookup"><span data-stu-id="bf3f0-139">After a service is deleted, the operation cannot be reversed.</span></span> 
> 
> 

<span data-ttu-id="bf3f0-140">Perform the following steps to delete a service.</span><span class="sxs-lookup"><span data-stu-id="bf3f0-140">Perform the following steps to delete a service.</span></span>

### <a name="to-delete-a-service"></a><span data-ttu-id="bf3f0-141">To delete a service</span><span class="sxs-lookup"><span data-stu-id="bf3f0-141">To delete a service</span></span>
1. <span data-ttu-id="bf3f0-142">On the **StorSimple Manager service** page, select the service that you wish to delete.</span><span class="sxs-lookup"><span data-stu-id="bf3f0-142">On the **StorSimple Manager service** page, select the service that you wish to delete.</span></span>
2. <span data-ttu-id="bf3f0-143">Click **Delete** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="bf3f0-143">Click **Delete** at the bottom of the page.</span></span>
3. <span data-ttu-id="bf3f0-144">Click **Yes** in the confirmation notification.</span><span class="sxs-lookup"><span data-stu-id="bf3f0-144">Click **Yes** in the confirmation notification.</span></span> <span data-ttu-id="bf3f0-145">It may take a few minutes for the service to be deleted.</span><span class="sxs-lookup"><span data-stu-id="bf3f0-145">It may take a few minutes for the service to be deleted.</span></span>

## <a name="get-the-service-registration-key"></a><span data-ttu-id="bf3f0-146">Get the service registration key</span><span class="sxs-lookup"><span data-stu-id="bf3f0-146">Get the service registration key</span></span>
<span data-ttu-id="bf3f0-147">After you have successfully created a service, you will need to register your StorSimple device with the service.</span><span class="sxs-lookup"><span data-stu-id="bf3f0-147">After you have successfully created a service, you will need to register your StorSimple device with the service.</span></span> <span data-ttu-id="bf3f0-148">To register your first StorSimple device, you will need the service registration key.</span><span class="sxs-lookup"><span data-stu-id="bf3f0-148">To register your first StorSimple device, you will need the service registration key.</span></span> <span data-ttu-id="bf3f0-149">To register additional devices with an existing StorSimple service, you will need both the registration key and the service data encryption key (which is generated on the first device during registration).</span><span class="sxs-lookup"><span data-stu-id="bf3f0-149">To register additional devices with an existing StorSimple service, you will need both the registration key and the service data encryption key (which is generated on the first device during registration).</span></span> <span data-ttu-id="bf3f0-150">For more information about the service data encryption key, see [Get the service data encryption key from the local web UI](storsimple-ova-web-ui-admin.md#get-the-service-data-encryption-key).</span><span class="sxs-lookup"><span data-stu-id="bf3f0-150">For more information about the service data encryption key, see [Get the service data encryption key from the local web UI](storsimple-ova-web-ui-admin.md#get-the-service-data-encryption-key).</span></span> 

<span data-ttu-id="bf3f0-151">Perform the following steps to get the service registration key.</span><span class="sxs-lookup"><span data-stu-id="bf3f0-151">Perform the following steps to get the service registration key.</span></span>

[!INCLUDE [storsimple-ova-get-service-registration-key](../../includes/storsimple-ova-get-service-registration-key.md)]

<span data-ttu-id="bf3f0-152">Keep the service registration key in a safe location.</span><span class="sxs-lookup"><span data-stu-id="bf3f0-152">Keep the service registration key in a safe location.</span></span> <span data-ttu-id="bf3f0-153">You will need this key, as well as the service data encryption key, to register additional devices with this service.</span><span class="sxs-lookup"><span data-stu-id="bf3f0-153">You will need this key, as well as the service data encryption key, to register additional devices with this service.</span></span> <span data-ttu-id="bf3f0-154">After obtaining the service registration key, you will need to configure your device through the Windows PowerShell for StorSimple interface.</span><span class="sxs-lookup"><span data-stu-id="bf3f0-154">After obtaining the service registration key, you will need to configure your device through the Windows PowerShell for StorSimple interface.</span></span>

## <a name="regenerate-the-service-registration-key"></a><span data-ttu-id="bf3f0-155">Regenerate the service registration key</span><span class="sxs-lookup"><span data-stu-id="bf3f0-155">Regenerate the service registration key</span></span>
<span data-ttu-id="bf3f0-156">You will need to regenerate a service registration key if you are required to perform key rotation or if the list of service administrators has changed.</span><span class="sxs-lookup"><span data-stu-id="bf3f0-156">You will need to regenerate a service registration key if you are required to perform key rotation or if the list of service administrators has changed.</span></span> <span data-ttu-id="bf3f0-157">When you regenerate the key, the new key is used only for registering subsequent devices.</span><span class="sxs-lookup"><span data-stu-id="bf3f0-157">When you regenerate the key, the new key is used only for registering subsequent devices.</span></span> <span data-ttu-id="bf3f0-158">The devices that were already registered are unaffected by this process.</span><span class="sxs-lookup"><span data-stu-id="bf3f0-158">The devices that were already registered are unaffected by this process.</span></span>

<span data-ttu-id="bf3f0-159">Perform the following steps to regenerate a service registration key.</span><span class="sxs-lookup"><span data-stu-id="bf3f0-159">Perform the following steps to regenerate a service registration key.</span></span>

### <a name="to-regenerate-the-service-registration-key"></a><span data-ttu-id="bf3f0-160">To regenerate the service registration key</span><span class="sxs-lookup"><span data-stu-id="bf3f0-160">To regenerate the service registration key</span></span>
1. <span data-ttu-id="bf3f0-161">On the **StorSimple Manager service** page, click **Registration Key**.</span><span class="sxs-lookup"><span data-stu-id="bf3f0-161">On the **StorSimple Manager service** page, click **Registration Key**.</span></span>
2. <span data-ttu-id="bf3f0-162">In the **Service Registration Key** dialog box, click **Regenerate**.</span><span class="sxs-lookup"><span data-stu-id="bf3f0-162">In the **Service Registration Key** dialog box, click **Regenerate**.</span></span>
3. <span data-ttu-id="bf3f0-163">You will see a confirmation message.</span><span class="sxs-lookup"><span data-stu-id="bf3f0-163">You will see a confirmation message.</span></span> <span data-ttu-id="bf3f0-164">Click **OK** to continue with the regeneration.</span><span class="sxs-lookup"><span data-stu-id="bf3f0-164">Click **OK** to continue with the regeneration.</span></span>
4. <span data-ttu-id="bf3f0-165">A new service registration key will appear.</span><span class="sxs-lookup"><span data-stu-id="bf3f0-165">A new service registration key will appear.</span></span>
5. <span data-ttu-id="bf3f0-166">Copy this key and save it for registering any new devices with this service.</span><span class="sxs-lookup"><span data-stu-id="bf3f0-166">Copy this key and save it for registering any new devices with this service.</span></span>
6. <span data-ttu-id="bf3f0-167">Click the check icon</span><span class="sxs-lookup"><span data-stu-id="bf3f0-167">Click the check icon</span></span> ![Check icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-manage-service/image7.png) <span data-ttu-id="bf3f0-169">to close this dialog box.</span><span class="sxs-lookup"><span data-stu-id="bf3f0-169">to close this dialog box.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bf3f0-170">Next steps</span><span class="sxs-lookup"><span data-stu-id="bf3f0-170">Next steps</span></span>
* <span data-ttu-id="bf3f0-171">Learn how to [get started](storsimple-ova-deploy1-portal-prep.md) with a StorSimple virtual array.</span><span class="sxs-lookup"><span data-stu-id="bf3f0-171">Learn how to [get started](storsimple-ova-deploy1-portal-prep.md) with a StorSimple virtual array.</span></span>
* <span data-ttu-id="bf3f0-172">Learn how to [administer your StorSimple device](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="bf3f0-172">Learn how to [administer your StorSimple device](storsimple-ova-web-ui-admin.md).</span></span>


