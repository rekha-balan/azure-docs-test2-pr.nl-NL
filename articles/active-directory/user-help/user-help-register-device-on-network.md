---
title: Register your personal device on your organization's network - Azure Active Directory | Microsoft Docs
description: Learn how to register your personal device on your organization's network so you can access your organization's protected resources.
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
ms.openlocfilehash: 7126a47bd90168c7d86fe9fcc05fab0a60955063
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870071"
---
# <a name="register-your-personal-device-on-your-organizations-network"></a><span data-ttu-id="f9563-103">Register your personal device on your organization's network</span><span class="sxs-lookup"><span data-stu-id="f9563-103">Register your personal device on your organization's network</span></span>
<span data-ttu-id="f9563-104">Register your personal device, typically a phone or tablet, on your organization's network.</span><span class="sxs-lookup"><span data-stu-id="f9563-104">Register your personal device, typically a phone or tablet, on your organization's network.</span></span> <span data-ttu-id="f9563-105">After your device is registered, it will be able to access your organization's restricted resources.</span><span class="sxs-lookup"><span data-stu-id="f9563-105">After your device is registered, it will be able to access your organization's restricted resources.</span></span>

>[!Note]
><span data-ttu-id="f9563-106">This article uses a Windows device for demonstration purposes, but you can also register devices running iOS, Android, or macOS.</span><span class="sxs-lookup"><span data-stu-id="f9563-106">This article uses a Windows device for demonstration purposes, but you can also register devices running iOS, Android, or macOS.</span></span>

## <a name="what-happens-when-you-register-your-device"></a><span data-ttu-id="f9563-107">What happens when you register your device</span><span class="sxs-lookup"><span data-stu-id="f9563-107">What happens when you register your device</span></span>
<span data-ttu-id="f9563-108">While you're registering your device on your organization's network, the following actions will happen:</span><span class="sxs-lookup"><span data-stu-id="f9563-108">While you're registering your device on your organization's network, the following actions will happen:</span></span>

- <span data-ttu-id="f9563-109">Windows registers your device on your organization's network.</span><span class="sxs-lookup"><span data-stu-id="f9563-109">Windows registers your device on your organization's network.</span></span>

- <span data-ttu-id="f9563-110">Optionally, based on your organization's choices, you might be asked to set up two-step verification through either [Multi-Factor Authentication](multi-factor-authentication-end-user-first-time.md) or [security info](user-help-security-info-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f9563-110">Optionally, based on your organization's choices, you might be asked to set up two-step verification through either [Multi-Factor Authentication](multi-factor-authentication-end-user-first-time.md) or [security info](user-help-security-info-overview.md).</span></span>

- <span data-ttu-id="f9563-111">Optionally, based on your organization's choices, you might be automatically enrolled in mobile device management, such as Microsoft Intune.</span><span class="sxs-lookup"><span data-stu-id="f9563-111">Optionally, based on your organization's choices, you might be automatically enrolled in mobile device management, such as Microsoft Intune.</span></span> <span data-ttu-id="f9563-112">For more info about enrolling in Microsoft Intune, see [Enroll your device in Intune](https://docs.microsoft.com/intune-user-help/enroll-your-device-in-intune-all).</span><span class="sxs-lookup"><span data-stu-id="f9563-112">For more info about enrolling in Microsoft Intune, see [Enroll your device in Intune](https://docs.microsoft.com/intune-user-help/enroll-your-device-in-intune-all).</span></span>

- <span data-ttu-id="f9563-113">You'll go through the sign-in process, using the username and password for your personal Microsoft account.</span><span class="sxs-lookup"><span data-stu-id="f9563-113">You'll go through the sign-in process, using the username and password for your personal Microsoft account.</span></span>

## <a name="to-register-your-windows-device"></a><span data-ttu-id="f9563-114">To register your Windows device</span><span class="sxs-lookup"><span data-stu-id="f9563-114">To register your Windows device</span></span>

<span data-ttu-id="f9563-115">Follow these steps to register your personal device on your network.</span><span class="sxs-lookup"><span data-stu-id="f9563-115">Follow these steps to register your personal device on your network.</span></span>

1. <span data-ttu-id="f9563-116">Open **Settings**, and then select **Accounts**.</span><span class="sxs-lookup"><span data-stu-id="f9563-116">Open **Settings**, and then select **Accounts**.</span></span>

    ![Accounts on the Settings screen](./media/user-help-register-device-on-network/register-device-settings-accounts.png)

2. <span data-ttu-id="f9563-118">Select **Email & accounts**, and then select **Join a Microsoft account**.</span><span class="sxs-lookup"><span data-stu-id="f9563-118">Select **Email & accounts**, and then select **Join a Microsoft account**.</span></span>

    ![Email & accounts and Add a Microsoft account links](./media/user-help-register-device-on-network/register-device-email-and-accounts.png)

3. <span data-ttu-id="f9563-120">On the **Add your Microsoft account** screen, type in your email address for your personal Microsoft account.</span><span class="sxs-lookup"><span data-stu-id="f9563-120">On the **Add your Microsoft account** screen, type in your email address for your personal Microsoft account.</span></span>

    ![Add your Microsoft account screen, with email](./media/user-help-register-device-on-network/register-device-add-accounts.png)

4. <span data-ttu-id="f9563-122">On the **Enter password** screen, type the password for your personal Microsoft account, and then select **Sign in**.</span><span class="sxs-lookup"><span data-stu-id="f9563-122">On the **Enter password** screen, type the password for your personal Microsoft account, and then select **Sign in**.</span></span>

    ![Enter password screen](./media/user-help-register-device-on-network/register-device-enter-password.png)

5. <span data-ttu-id="f9563-124">Complete the rest of the registration process, including approving your identity verification request (if you use two-step verification) and setting up Windows Hello (if necessary).</span><span class="sxs-lookup"><span data-stu-id="f9563-124">Complete the rest of the registration process, including approving your identity verification request (if you use two-step verification) and setting up Windows Hello (if necessary).</span></span>

## <a name="to-make-sure-youre-registered"></a><span data-ttu-id="f9563-125">To make sure you're registered</span><span class="sxs-lookup"><span data-stu-id="f9563-125">To make sure you're registered</span></span>
<span data-ttu-id="f9563-126">You can make sure that you're registered by looking at your settings.</span><span class="sxs-lookup"><span data-stu-id="f9563-126">You can make sure that you're registered by looking at your settings.</span></span>

1. <span data-ttu-id="f9563-127">Open **Settings**, and then select **Accounts**.</span><span class="sxs-lookup"><span data-stu-id="f9563-127">Open **Settings**, and then select **Accounts**.</span></span>

    ![Accounts on the Settings screen](./media/user-help-register-device-on-network/register-device-settings-accounts.png)

2. <span data-ttu-id="f9563-129">Select **Email & accounts**, and make sure you see your personal Microsoft account.</span><span class="sxs-lookup"><span data-stu-id="f9563-129">Select **Email & accounts**, and make sure you see your personal Microsoft account.</span></span>

    ![Access work or school screen with connected contoso account](./media/user-help-register-device-on-network/register-device-verify-account.png)

## <a name="next-steps"></a><span data-ttu-id="f9563-131">Next steps</span><span class="sxs-lookup"><span data-stu-id="f9563-131">Next steps</span></span>
<span data-ttu-id="f9563-132">After you register your personal device to your organization's network, you should be able to access most of your resources.</span><span class="sxs-lookup"><span data-stu-id="f9563-132">After you register your personal device to your organization's network, you should be able to access most of your resources.</span></span>

- <span data-ttu-id="f9563-133">If your organization wants you to join your work device, see [Join your work device to your organization's network](user-help-join-device-on-network.md).</span><span class="sxs-lookup"><span data-stu-id="f9563-133">If your organization wants you to join your work device, see [Join your work device to your organization's network](user-help-join-device-on-network.md).</span></span>



