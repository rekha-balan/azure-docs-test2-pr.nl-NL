---
title: Change the StorSimple virtual device admin password | Microsoft Docs
description: Describes how to use either the Azure classic portal or the StorSimple Virtual Array web UI to change the device administrator password.
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: ''
ms.assetid: 52acde45-ae29-4edb-9377-46918ab7eef8
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/17/2016
ms.author: alkohli
ms.openlocfilehash: 6a6233332786f9dc03bf8482f459a96fb1b1f0e4
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44670479"
---
# <a name="change-the-storsimple-virtual-array-device-administrator-password"></a><span data-ttu-id="1276a-103">Change the StorSimple Virtual Array device administrator password</span><span class="sxs-lookup"><span data-stu-id="1276a-103">Change the StorSimple Virtual Array device administrator password</span></span>
## <a name="overview"></a><span data-ttu-id="1276a-104">Overview</span><span class="sxs-lookup"><span data-stu-id="1276a-104">Overview</span></span>
<span data-ttu-id="1276a-105">When you use the Windows PowerShell interface to access the StorSimple virtual device, you are required to enter a device administrator password.</span><span class="sxs-lookup"><span data-stu-id="1276a-105">When you use the Windows PowerShell interface to access the StorSimple virtual device, you are required to enter a device administrator password.</span></span> <span data-ttu-id="1276a-106">When the StorSimple device is first provisioned and started, the default password is *Password1*.</span><span class="sxs-lookup"><span data-stu-id="1276a-106">When the StorSimple device is first provisioned and started, the default password is *Password1*.</span></span> <span data-ttu-id="1276a-107">For the security of your data, the default password expires the first time that you sign in and you are required to change this password.</span><span class="sxs-lookup"><span data-stu-id="1276a-107">For the security of your data, the default password expires the first time that you sign in and you are required to change this password.</span></span>

<span data-ttu-id="1276a-108">You can also use either the local web UI or the Azure classic portal to change the device administrator password at any time after the device is deployed in  your production environment.</span><span class="sxs-lookup"><span data-stu-id="1276a-108">You can also use either the local web UI or the Azure classic portal to change the device administrator password at any time after the device is deployed in  your production environment.</span></span> <span data-ttu-id="1276a-109">Each of these procedures is described in this article.</span><span class="sxs-lookup"><span data-stu-id="1276a-109">Each of these procedures is described in this article.</span></span>

## <a name="use-the-azure-classic-portal-to-change-the-password"></a><span data-ttu-id="1276a-110">Use the Azure classic portal to change the password</span><span class="sxs-lookup"><span data-stu-id="1276a-110">Use the Azure classic portal to change the password</span></span>
<span data-ttu-id="1276a-111">Perform the following steps to change the device administrator password through the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="1276a-111">Perform the following steps to change the device administrator password through the Azure classic portal.</span></span>

#### <a name="to-change-the-device-administrator-password-via-the-azure-classic-portal"></a><span data-ttu-id="1276a-112">To change the device administrator password via the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="1276a-112">To change the device administrator password via the Azure classic portal</span></span>
1. <span data-ttu-id="1276a-113">In the portal, click **Devices** > **Configuration** for your device.</span><span class="sxs-lookup"><span data-stu-id="1276a-113">In the portal, click **Devices** > **Configuration** for your device.</span></span>
2. <span data-ttu-id="1276a-114">Scroll down to the **Device Administrator Password** section.</span><span class="sxs-lookup"><span data-stu-id="1276a-114">Scroll down to the **Device Administrator Password** section.</span></span> <span data-ttu-id="1276a-115">Provide an administrator password that contains from 8 to 15 characters.</span><span class="sxs-lookup"><span data-stu-id="1276a-115">Provide an administrator password that contains from 8 to 15 characters.</span></span> <span data-ttu-id="1276a-116">The password must be a combination of uppercase, lowercase, numeric, and special characters.</span><span class="sxs-lookup"><span data-stu-id="1276a-116">The password must be a combination of uppercase, lowercase, numeric, and special characters.</span></span>
3. <span data-ttu-id="1276a-117">Confirm the password.</span><span class="sxs-lookup"><span data-stu-id="1276a-117">Confirm the password.</span></span>
4. <span data-ttu-id="1276a-118">Click **Save** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="1276a-118">Click **Save** at the bottom of the page.</span></span>

<span data-ttu-id="1276a-119">The device administrator password should now be updated.</span><span class="sxs-lookup"><span data-stu-id="1276a-119">The device administrator password should now be updated.</span></span> <span data-ttu-id="1276a-120">You can use this modified password to access the device locally.</span><span class="sxs-lookup"><span data-stu-id="1276a-120">You can use this modified password to access the device locally.</span></span>

## <a name="use-the-storsimple-virtual-array-web-ui-to-change-the-password"></a><span data-ttu-id="1276a-121">Use the StorSimple Virtual Array web UI to change the password</span><span class="sxs-lookup"><span data-stu-id="1276a-121">Use the StorSimple Virtual Array web UI to change the password</span></span>
<span data-ttu-id="1276a-122">Perform the following steps to change the device administrator password through the local web UI.</span><span class="sxs-lookup"><span data-stu-id="1276a-122">Perform the following steps to change the device administrator password through the local web UI.</span></span>

#### <a name="to-change-the-device-administrator-password-via-the-local-web-ui"></a><span data-ttu-id="1276a-123">To change the device administrator password via the local web UI</span><span class="sxs-lookup"><span data-stu-id="1276a-123">To change the device administrator password via the local web UI</span></span>
1. <span data-ttu-id="1276a-124">In the local web UI, click **Maintenance** > **Password change** for your device.</span><span class="sxs-lookup"><span data-stu-id="1276a-124">In the local web UI, click **Maintenance** > **Password change** for your device.</span></span>
   
    ![change password1](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-change-device-admin-password/image40.png)
2. <span data-ttu-id="1276a-126">Enter the **Current password**.</span><span class="sxs-lookup"><span data-stu-id="1276a-126">Enter the **Current password**.</span></span>
3. <span data-ttu-id="1276a-127">Provide a **New Password**.</span><span class="sxs-lookup"><span data-stu-id="1276a-127">Provide a **New Password**.</span></span> <span data-ttu-id="1276a-128">The password must be at least 8 characters long.</span><span class="sxs-lookup"><span data-stu-id="1276a-128">The password must be at least 8 characters long.</span></span> <span data-ttu-id="1276a-129">It must contain 3 of 4 of the following: uppercase, lowercase, numeric, and special characters.</span><span class="sxs-lookup"><span data-stu-id="1276a-129">It must contain 3 of 4 of the following: uppercase, lowercase, numeric, and special characters.</span></span>
   
    <span data-ttu-id="1276a-130">Note that your password cannot be the same as the last 24 passwords.</span><span class="sxs-lookup"><span data-stu-id="1276a-130">Note that your password cannot be the same as the last 24 passwords.</span></span>
4. <span data-ttu-id="1276a-131">Reenter the password to confirm it.</span><span class="sxs-lookup"><span data-stu-id="1276a-131">Reenter the password to confirm it.</span></span>
   
    ![change password2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-change-device-admin-password/image41.png)
5. <span data-ttu-id="1276a-133">At the bottom of the page, click **Apply**.</span><span class="sxs-lookup"><span data-stu-id="1276a-133">At the bottom of the page, click **Apply**.</span></span> <span data-ttu-id="1276a-134">The new password will then be applied.</span><span class="sxs-lookup"><span data-stu-id="1276a-134">The new password will then be applied.</span></span> <span data-ttu-id="1276a-135">If the password change is not successful, you will see the following error.</span><span class="sxs-lookup"><span data-stu-id="1276a-135">If the password change is not successful, you will see the following error.</span></span>
   
    ![password error](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-change-device-admin-password/image42.png)
   
    <span data-ttu-id="1276a-137">After the password is successfully updated, you will be notified.</span><span class="sxs-lookup"><span data-stu-id="1276a-137">After the password is successfully updated, you will be notified.</span></span> <span data-ttu-id="1276a-138">You can then use this modified password to access the device locally.</span><span class="sxs-lookup"><span data-stu-id="1276a-138">You can then use this modified password to access the device locally.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1276a-139">Next steps</span><span class="sxs-lookup"><span data-stu-id="1276a-139">Next steps</span></span>
<span data-ttu-id="1276a-140">Learn more about [administering your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="1276a-140">Learn more about [administering your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>




