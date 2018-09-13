---
title: Change StorSimple Virtual Array device admin password | Microsoft Docs
description: Describes how to use either the Azure portal or StorSimple Virtual Array web UI to change the device administrator password.
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: ''
ms.assetid: 11490814-d9fd-4dc7-9c3b-55dd2c23eaf1
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 172e56f4e103f2c7929ac5cb219bdee10474fee9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555987"
---
# <a name="change-the-storsimple-virtual-array-device-administrator-password-via-storsimple-device-manager"></a><span data-ttu-id="dd43e-103">Change the StorSimple Virtual Array device administrator password via StorSimple Device Manager</span><span class="sxs-lookup"><span data-stu-id="dd43e-103">Change the StorSimple Virtual Array device administrator password via StorSimple Device Manager</span></span>

## <a name="overview"></a><span data-ttu-id="dd43e-104">Overview</span><span class="sxs-lookup"><span data-stu-id="dd43e-104">Overview</span></span>

<span data-ttu-id="dd43e-105">When you use the Windows PowerShell interface to access the StorSimple Virtual Array, you are required to enter a device administrator password.</span><span class="sxs-lookup"><span data-stu-id="dd43e-105">When you use the Windows PowerShell interface to access the StorSimple Virtual Array, you are required to enter a device administrator password.</span></span> <span data-ttu-id="dd43e-106">When the StorSimple device is first provisioned and started, the default password is *Password1*.</span><span class="sxs-lookup"><span data-stu-id="dd43e-106">When the StorSimple device is first provisioned and started, the default password is *Password1*.</span></span> <span data-ttu-id="dd43e-107">For the security of your data, the default password expires the first time that you sign in and you are required to change this password.</span><span class="sxs-lookup"><span data-stu-id="dd43e-107">For the security of your data, the default password expires the first time that you sign in and you are required to change this password.</span></span>

<span data-ttu-id="dd43e-108">You can also use either the local web UI or the Azure portal to change the device administrator password at any time after the device is deployed in your production environment.</span><span class="sxs-lookup"><span data-stu-id="dd43e-108">You can also use either the local web UI or the Azure portal to change the device administrator password at any time after the device is deployed in your production environment.</span></span> <span data-ttu-id="dd43e-109">Each of these procedures is described in this article.</span><span class="sxs-lookup"><span data-stu-id="dd43e-109">Each of these procedures is described in this article.</span></span>

 ![devices blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-change-device-admin-password/ova-devices-blade.png)

## <a name="use-the-azure-portal-to-change-the-password"></a><span data-ttu-id="dd43e-111">Use the Azure portal to change the password</span><span class="sxs-lookup"><span data-stu-id="dd43e-111">Use the Azure portal to change the password</span></span>

<span data-ttu-id="dd43e-112">Perform the following steps to change the device administrator password through the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="dd43e-112">Perform the following steps to change the device administrator password through the Azure portal.</span></span>

#### <a name="to-change-the-device-administrator-password-via-the-azure-portal"></a><span data-ttu-id="dd43e-113">To change the device administrator password via the Azure portal</span><span class="sxs-lookup"><span data-stu-id="dd43e-113">To change the device administrator password via the Azure portal</span></span>

1. <span data-ttu-id="dd43e-114">On the service landing page, select your service, double-click the service name, and then within the **Management** section, click **Devices**.</span><span class="sxs-lookup"><span data-stu-id="dd43e-114">On the service landing page, select your service, double-click the service name, and then within the **Management** section, click **Devices**.</span></span> <span data-ttu-id="dd43e-115">This opens the **Devices** blade that lists all your StorSimple Virtual Array devices.</span><span class="sxs-lookup"><span data-stu-id="dd43e-115">This opens the **Devices** blade that lists all your StorSimple Virtual Array devices.</span></span>

2. <span data-ttu-id="dd43e-116">In the **Devices** blade, double-click the device that requires a change of password.</span><span class="sxs-lookup"><span data-stu-id="dd43e-116">In the **Devices** blade, double-click the device that requires a change of password.</span></span>

3. <span data-ttu-id="dd43e-117">In the **Settings** blade for your device, click **Security**.</span><span class="sxs-lookup"><span data-stu-id="dd43e-117">In the **Settings** blade for your device, click **Security**.</span></span>

4. <span data-ttu-id="dd43e-118">In the **Security Settings** blade, do the following:</span><span class="sxs-lookup"><span data-stu-id="dd43e-118">In the **Security Settings** blade, do the following:</span></span>
   
   1. <span data-ttu-id="dd43e-119">Scroll down to the **Device Administrator Password** section.</span><span class="sxs-lookup"><span data-stu-id="dd43e-119">Scroll down to the **Device Administrator Password** section.</span></span> <span data-ttu-id="dd43e-120">Provide an administrator password that contains from 8 to 15 characters.</span><span class="sxs-lookup"><span data-stu-id="dd43e-120">Provide an administrator password that contains from 8 to 15 characters.</span></span>
   2. <span data-ttu-id="dd43e-121">Confirm the password.</span><span class="sxs-lookup"><span data-stu-id="dd43e-121">Confirm the password.</span></span>
   3. <span data-ttu-id="dd43e-122">Click **Save** at the top of the blade.</span><span class="sxs-lookup"><span data-stu-id="dd43e-122">Click **Save** at the top of the blade.</span></span>

<span data-ttu-id="dd43e-123">The device administrator password is now updated.</span><span class="sxs-lookup"><span data-stu-id="dd43e-123">The device administrator password is now updated.</span></span> <span data-ttu-id="dd43e-124">You can use this modified password to access the device locally.</span><span class="sxs-lookup"><span data-stu-id="dd43e-124">You can use this modified password to access the device locally.</span></span>

![Security settings blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-change-device-admin-password/ova-change-device-pwd.png)

## <a name="use-the-local-web-ui-to-change-the-password"></a><span data-ttu-id="dd43e-126">Use the local web UI to change the password</span><span class="sxs-lookup"><span data-stu-id="dd43e-126">Use the local web UI to change the password</span></span>

<span data-ttu-id="dd43e-127">Perform the following steps to change the device administrator password through the local web UI.</span><span class="sxs-lookup"><span data-stu-id="dd43e-127">Perform the following steps to change the device administrator password through the local web UI.</span></span>

#### <a name="to-change-the-device-administrator-password-via-the-local-web-ui"></a><span data-ttu-id="dd43e-128">To change the device administrator password via the local web UI</span><span class="sxs-lookup"><span data-stu-id="dd43e-128">To change the device administrator password via the local web UI</span></span>

1. <span data-ttu-id="dd43e-129">In the local web UI, click **Maintenance** > **Password change** for your device.</span><span class="sxs-lookup"><span data-stu-id="dd43e-129">In the local web UI, click **Maintenance** > **Password change** for your device.</span></span>
   
    ![change password1](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-change-device-admin-password/image40.png)
2. <span data-ttu-id="dd43e-131">Enter the **Current password**.</span><span class="sxs-lookup"><span data-stu-id="dd43e-131">Enter the **Current password**.</span></span>
3. <span data-ttu-id="dd43e-132">Provide a **New Password**.</span><span class="sxs-lookup"><span data-stu-id="dd43e-132">Provide a **New Password**.</span></span> <span data-ttu-id="dd43e-133">The password must be at least 8 characters long.</span><span class="sxs-lookup"><span data-stu-id="dd43e-133">The password must be at least 8 characters long.</span></span> <span data-ttu-id="dd43e-134">It must contain 3 of 4 of the following: uppercase, lowercase, numeric, and special characters.</span><span class="sxs-lookup"><span data-stu-id="dd43e-134">It must contain 3 of 4 of the following: uppercase, lowercase, numeric, and special characters.</span></span>
   
    <span data-ttu-id="dd43e-135">Note that your password cannot be the same as the last 24 passwords.</span><span class="sxs-lookup"><span data-stu-id="dd43e-135">Note that your password cannot be the same as the last 24 passwords.</span></span>
4. <span data-ttu-id="dd43e-136">Reenter the password to confirm it.</span><span class="sxs-lookup"><span data-stu-id="dd43e-136">Reenter the password to confirm it.</span></span>
   
    ![change password2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-change-device-admin-password/image41.png)
5. <span data-ttu-id="dd43e-138">At the bottom of the page, click **Apply**.</span><span class="sxs-lookup"><span data-stu-id="dd43e-138">At the bottom of the page, click **Apply**.</span></span> <span data-ttu-id="dd43e-139">The new password is now applied.</span><span class="sxs-lookup"><span data-stu-id="dd43e-139">The new password is now applied.</span></span> <span data-ttu-id="dd43e-140">If the password change is not successful, you see the following error:</span><span class="sxs-lookup"><span data-stu-id="dd43e-140">If the password change is not successful, you see the following error:</span></span>
   
    ![password error](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-change-device-admin-password/image42.png)
   
    <span data-ttu-id="dd43e-142">After the password is successfully updated, you are notified.</span><span class="sxs-lookup"><span data-stu-id="dd43e-142">After the password is successfully updated, you are notified.</span></span> <span data-ttu-id="dd43e-143">You can then use this modified password to access the device locally.</span><span class="sxs-lookup"><span data-stu-id="dd43e-143">You can then use this modified password to access the device locally.</span></span>


## <a name="next-steps"></a><span data-ttu-id="dd43e-144">Next steps</span><span class="sxs-lookup"><span data-stu-id="dd43e-144">Next steps</span></span>
<span data-ttu-id="dd43e-145">Learn how to [administer your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="dd43e-145">Learn how to [administer your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>






