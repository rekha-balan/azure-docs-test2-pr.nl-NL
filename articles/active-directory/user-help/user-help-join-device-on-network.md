---
title: Join your work device to your organization's network - Azure Active Directory | Microsoft Docs
description: Learn how to join your work device to your organization's network.
services: active-directory
author: eross-msft
manager: mtillman
ms.assetid: 54e1b01b-03ee-4c46-bcf0-e01affc0419d
ms.service: active-directory
ms.component: user-help
ms.workload: identity
ms.topic: conceptual
ms.date: 08/03/2018
ms.author: lizross
ms.reviewer: jairoc
ms.openlocfilehash: 34d3c12c83aeac7e92aa019abc38d9c4109883bd
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967213"
---
# <a name="join-your-work-device-to-your-organizations-network"></a><span data-ttu-id="53178-103">Join your work device to your organization's network</span><span class="sxs-lookup"><span data-stu-id="53178-103">Join your work device to your organization's network</span></span>
<span data-ttu-id="53178-104">Join your work-owned Windows 10 device to your organization's network so you can access potentially restricted resources.</span><span class="sxs-lookup"><span data-stu-id="53178-104">Join your work-owned Windows 10 device to your organization's network so you can access potentially restricted resources.</span></span>

## <a name="what-happens-when-you-join-your-device"></a><span data-ttu-id="53178-105">What happens when you join your device</span><span class="sxs-lookup"><span data-stu-id="53178-105">What happens when you join your device</span></span>
<span data-ttu-id="53178-106">While you're joining your Windows 10 device to your organization's network, the following actions will happen:</span><span class="sxs-lookup"><span data-stu-id="53178-106">While you're joining your Windows 10 device to your organization's network, the following actions will happen:</span></span>

- <span data-ttu-id="53178-107">Windows registers your device to your organization's network, letting you can access your resources using your personal account.</span><span class="sxs-lookup"><span data-stu-id="53178-107">Windows registers your device to your organization's network, letting you can access your resources using your personal account.</span></span> <span data-ttu-id="53178-108">After your device is registered, Windows then joins your device to the network, so you can use your organization's username and password to sign in and access restricted resources.</span><span class="sxs-lookup"><span data-stu-id="53178-108">After your device is registered, Windows then joins your device to the network, so you can use your organization's username and password to sign in and access restricted resources.</span></span>

- <span data-ttu-id="53178-109">Optionally, based on your organization's choices, you might be asked to set up two-step verification through either [Multi-Factor Authentication](multi-factor-authentication-end-user-first-time.md) or [security info](user-help-security-info-overview.md).</span><span class="sxs-lookup"><span data-stu-id="53178-109">Optionally, based on your organization's choices, you might be asked to set up two-step verification through either [Multi-Factor Authentication](multi-factor-authentication-end-user-first-time.md) or [security info](user-help-security-info-overview.md).</span></span>

- <span data-ttu-id="53178-110">Optionally, based on your organization's choices, you might be automatically enrolled in mobile device management, such as Microsoft Intune.</span><span class="sxs-lookup"><span data-stu-id="53178-110">Optionally, based on your organization's choices, you might be automatically enrolled in mobile device management, such as Microsoft Intune.</span></span> <span data-ttu-id="53178-111">For more info about enrolling in Microsoft Intune, see [Enroll your device in Intune](https://docs.microsoft.com/intune-user-help/enroll-your-device-in-intune-all).</span><span class="sxs-lookup"><span data-stu-id="53178-111">For more info about enrolling in Microsoft Intune, see [Enroll your device in Intune](https://docs.microsoft.com/intune-user-help/enroll-your-device-in-intune-all).</span></span>

- <span data-ttu-id="53178-112">You'll go through the sign-in process, using automatic sign-in with your organizational account.</span><span class="sxs-lookup"><span data-stu-id="53178-112">You'll go through the sign-in process, using automatic sign-in with your organizational account.</span></span>

## <a name="to-join-a-brand-new-windows-10-device"></a><span data-ttu-id="53178-113">To join a brand-new Windows 10 device</span><span class="sxs-lookup"><span data-stu-id="53178-113">To join a brand-new Windows 10 device</span></span>
<span data-ttu-id="53178-114">If your device is brand-new and hasn't been set up yet, you can go through the Windows Out of Box Experience (OOBE) process to join your device to the network.</span><span class="sxs-lookup"><span data-stu-id="53178-114">If your device is brand-new and hasn't been set up yet, you can go through the Windows Out of Box Experience (OOBE) process to join your device to the network.</span></span>

1. <span data-ttu-id="53178-115">Start up your new device and begin the OOBE process.</span><span class="sxs-lookup"><span data-stu-id="53178-115">Start up your new device and begin the OOBE process.</span></span>

2. <span data-ttu-id="53178-116">On the **Sign in with Microsoft** screen, type your work or school email address.</span><span class="sxs-lookup"><span data-stu-id="53178-116">On the **Sign in with Microsoft** screen, type your work or school email address.</span></span>

    ![Sign in screen with email address](./media/user-help-join-device-on-network/join-device-oobe-signin.png)

3. <span data-ttu-id="53178-118">On the **Enter your password** screen, type your password.</span><span class="sxs-lookup"><span data-stu-id="53178-118">On the **Enter your password** screen, type your password.</span></span>

    ![Enter your password screen](./media/user-help-join-device-on-network/join-device-oobe-password.png)

4. <span data-ttu-id="53178-120">On your mobile device, approve your device so it can access your account.</span><span class="sxs-lookup"><span data-stu-id="53178-120">On your mobile device, approve your device so it can access your account.</span></span> 

    ![Mobile notification screen](./media/user-help-join-device-on-network/join-device-oobe-mobile.png)

5. <span data-ttu-id="53178-122">Complete the OOBE process, including setting your privacy settings and setting up Windows Hello (if necessary).</span><span class="sxs-lookup"><span data-stu-id="53178-122">Complete the OOBE process, including setting your privacy settings and setting up Windows Hello (if necessary).</span></span>

    <span data-ttu-id="53178-123">Your device is now joined to your organization's network.</span><span class="sxs-lookup"><span data-stu-id="53178-123">Your device is now joined to your organization's network.</span></span>

## <a name="to-make-sure-youre-joined"></a><span data-ttu-id="53178-124">To make sure you're joined</span><span class="sxs-lookup"><span data-stu-id="53178-124">To make sure you're joined</span></span>
<span data-ttu-id="53178-125">You can make sure that you're joined by looking at your settings.</span><span class="sxs-lookup"><span data-stu-id="53178-125">You can make sure that you're joined by looking at your settings.</span></span>

1. <span data-ttu-id="53178-126">Open **Settings**, and then select **Accounts**.</span><span class="sxs-lookup"><span data-stu-id="53178-126">Open **Settings**, and then select **Accounts**.</span></span>

    ![Accounts on the Settings screen](./media/user-help-join-device-on-network/join-device-settings-accounts.png)

2. <span data-ttu-id="53178-128">Select **Access work or school**, and make sure you see text that says something like, **Connected to *<your_organization>* Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="53178-128">Select **Access work or school**, and make sure you see text that says something like, **Connected to *<your_organization>* Azure AD**.</span></span>

    ![Access work or school screen with connected contoso account](./media/user-help-join-device-on-network/join-device-oobe-verify.png)


## <a name="to-join-an-already-configured-windows-10-device"></a><span data-ttu-id="53178-130">To join an already configured Windows 10 device</span><span class="sxs-lookup"><span data-stu-id="53178-130">To join an already configured Windows 10 device</span></span>
<span data-ttu-id="53178-131">If you've had your device for a while and it's already been set up, you can follow these steps to join your device to the network.</span><span class="sxs-lookup"><span data-stu-id="53178-131">If you've had your device for a while and it's already been set up, you can follow these steps to join your device to the network.</span></span>

1. <span data-ttu-id="53178-132">Open **Settings**, and then select **Accounts**.</span><span class="sxs-lookup"><span data-stu-id="53178-132">Open **Settings**, and then select **Accounts**.</span></span>

2. <span data-ttu-id="53178-133">Select **Access work or school**, and then select **Connect**.</span><span class="sxs-lookup"><span data-stu-id="53178-133">Select **Access work or school**, and then select **Connect**.</span></span>

    ![Access work or school and Connect links](./media/user-help-join-device-on-network/join-device-access-work-school-connect.png)

3. <span data-ttu-id="53178-135">On the **Set up a work or school account** screen, select **Join this device to Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="53178-135">On the **Set up a work or school account** screen, select **Join this device to Azure Active Directory**.</span></span>

    ![Set up a work or school account screen](./media/user-help-join-device-on-network/join-device-setup-join-aad.png)

4. <span data-ttu-id="53178-137">On the **Let's get you signed in** screen, type your email address (for example, alain@contoso.com), and then select **Next**.</span><span class="sxs-lookup"><span data-stu-id="53178-137">On the **Let's get you signed in** screen, type your email address (for example, alain@contoso.com), and then select **Next**.</span></span>

    ![Let's get you signed in screen](./media/user-help-join-device-on-network/join-device-setup-get-signed-in.png)

5. <span data-ttu-id="53178-139">On the **Enter password** screen, type your password, and then select **Sign in**.</span><span class="sxs-lookup"><span data-stu-id="53178-139">On the **Enter password** screen, type your password, and then select **Sign in**.</span></span>

    ![Enter password](./media/user-help-join-device-on-network/join-device-setup-password.png)

6. <span data-ttu-id="53178-141">On your mobile device, approve your device so it can access your account.</span><span class="sxs-lookup"><span data-stu-id="53178-141">On your mobile device, approve your device so it can access your account.</span></span> 

    ![Mobile notification screen](./media/user-help-join-device-on-network/join-device-setup-mobile.png)

7. <span data-ttu-id="53178-143">On the  **Make sure this is your organization** screen, review the information to make sure it's right, and then select **Join**.</span><span class="sxs-lookup"><span data-stu-id="53178-143">On the  **Make sure this is your organization** screen, review the information to make sure it's right, and then select **Join**.</span></span>

    ![Make sure this is your organization verification screen](./media/user-help-join-device-on-network/join-device-setup-confirm.png)

8. <span data-ttu-id="53178-145">On the **You're all set** screen, click **Done**.</span><span class="sxs-lookup"><span data-stu-id="53178-145">On the **You're all set** screen, click **Done**.</span></span>

    ![You're all set screen](./media/user-help-join-device-on-network/join-device-setup-finish.png)

## <a name="to-make-sure-youre-joined"></a><span data-ttu-id="53178-147">To make sure you're joined</span><span class="sxs-lookup"><span data-stu-id="53178-147">To make sure you're joined</span></span>
<span data-ttu-id="53178-148">You can make sure that you're joined by looking at your settings.</span><span class="sxs-lookup"><span data-stu-id="53178-148">You can make sure that you're joined by looking at your settings.</span></span>

1. <span data-ttu-id="53178-149">Open **Settings**, and then select **Accounts**.</span><span class="sxs-lookup"><span data-stu-id="53178-149">Open **Settings**, and then select **Accounts**.</span></span>

    ![Accounts on the Settings screen](./media/user-help-join-device-on-network/join-device-settings-accounts.png)

2. <span data-ttu-id="53178-151">Select **Access work or school**, and make sure you see text that says something like, **Connected to *<your_organization>* Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="53178-151">Select **Access work or school**, and make sure you see text that says something like, **Connected to *<your_organization>* Azure AD**.</span></span>

    ![Access work or school screen with connected contoso account](./media/user-help-join-device-on-network/join-device-setup-verify.png)

## <a name="next-steps"></a><span data-ttu-id="53178-153">Next steps</span><span class="sxs-lookup"><span data-stu-id="53178-153">Next steps</span></span>
<span data-ttu-id="53178-154">After you join your device to your organization's network, you should be able to access all of your resources using your work or school account information.</span><span class="sxs-lookup"><span data-stu-id="53178-154">After you join your device to your organization's network, you should be able to access all of your resources using your work or school account information.</span></span>

- <span data-ttu-id="53178-155">If your organization wants you to register your personal device, such as your phone, see [Register your personal device on your organization's network](user-help-register-device-on-network.md).</span><span class="sxs-lookup"><span data-stu-id="53178-155">If your organization wants you to register your personal device, such as your phone, see [Register your personal device on your organization's network](user-help-register-device-on-network.md).</span></span>

