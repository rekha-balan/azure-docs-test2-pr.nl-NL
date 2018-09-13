---
title: How to manage app passwords in Azure Active Directory | Microsoft Docs
description: This page will help users understand what app passwords are and what they are used for with regard to two-step verification.
services: active-directory
author: eross-msft
manager: mtillman
ms.reviewer: richagi
ms.assetid: 345b757b-5a2b-48eb-953f-d363313be9e5
ms.workload: identity
ms.service: active-directory
ms.component: user-help
ms.topic: conceptual
ms.date: 07/30/2018
ms.author: lizross
ms.openlocfilehash: 836f426be950e33031ff74276218d1ba59f1f2f7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856160"
---
# <a name="manage-app-passwords-for-two-step-verification"></a><span data-ttu-id="0c725-103">Manage app passwords for two-step verification</span><span class="sxs-lookup"><span data-stu-id="0c725-103">Manage app passwords for two-step verification</span></span>

<span data-ttu-id="0c725-104">Certain non-browser apps, such as Outlook 2010, doesn't support two-step verification.</span><span class="sxs-lookup"><span data-stu-id="0c725-104">Certain non-browser apps, such as Outlook 2010, doesn't support two-step verification.</span></span> <span data-ttu-id="0c725-105">This lack of support means that if you're using two-step verification, the app won't work.</span><span class="sxs-lookup"><span data-stu-id="0c725-105">This lack of support means that if you're using two-step verification, the app won't work.</span></span> <span data-ttu-id="0c725-106">To get around this problem, you can create an auto-generated password to use with each non-browser app, separate from your normal password.</span><span class="sxs-lookup"><span data-stu-id="0c725-106">To get around this problem, you can create an auto-generated password to use with each non-browser app, separate from your normal password.</span></span>

<span data-ttu-id="0c725-107">When using app passwords, it's important to remember:</span><span class="sxs-lookup"><span data-stu-id="0c725-107">When using app passwords, it's important to remember:</span></span>

- <span data-ttu-id="0c725-108">App passwords are auto-generated and only entered once per app.</span><span class="sxs-lookup"><span data-stu-id="0c725-108">App passwords are auto-generated and only entered once per app.</span></span>

- <span data-ttu-id="0c725-109">There's a limit of 40 passwords per user.</span><span class="sxs-lookup"><span data-stu-id="0c725-109">There's a limit of 40 passwords per user.</span></span> <span data-ttu-id="0c725-110">If you try to create one after that limit, you'll be prompted to delete an existing password before being allowed to create the new one.</span><span class="sxs-lookup"><span data-stu-id="0c725-110">If you try to create one after that limit, you'll be prompted to delete an existing password before being allowed to create the new one.</span></span>

- <span data-ttu-id="0c725-111">Use one app password per device, not per app.</span><span class="sxs-lookup"><span data-stu-id="0c725-111">Use one app password per device, not per app.</span></span> <span data-ttu-id="0c725-112">For example, create a single password for all the apps on your laptop, and then another single password for all the apps on your desktop.</span><span class="sxs-lookup"><span data-stu-id="0c725-112">For example, create a single password for all the apps on your laptop, and then another single password for all the apps on your desktop.</span></span>

    >[!Note]
    ><span data-ttu-id="0c725-113">Office 2013 clients (including Outlook) support new authentication protocols and can be used with two-step verification.</span><span class="sxs-lookup"><span data-stu-id="0c725-113">Office 2013 clients (including Outlook) support new authentication protocols and can be used with two-step verification.</span></span> <span data-ttu-id="0c725-114">This support means that after two-step verification is turned on, you'll no longer need app passwords for Office 2013 clients.</span><span class="sxs-lookup"><span data-stu-id="0c725-114">This support means that after two-step verification is turned on, you'll no longer need app passwords for Office 2013 clients.</span></span> <span data-ttu-id="0c725-115">For more info, see the [How modern authentication works for Office 2013 and Office 2016 client apps](https://support.office.com/article/how-modern-authentication-works-for-office-2013-and-office-2016-client-apps-e4c45989-4b1a-462e-a81b-2a13191cf517) article.</span><span class="sxs-lookup"><span data-stu-id="0c725-115">For more info, see the [How modern authentication works for Office 2013 and Office 2016 client apps](https://support.office.com/article/how-modern-authentication-works-for-office-2013-and-office-2016-client-apps-e4c45989-4b1a-462e-a81b-2a13191cf517) article.</span></span>

## <a name="where-to-create-and-delete-your-app-passwords"></a><span data-ttu-id="0c725-116">Where to create and delete your app passwords</span><span class="sxs-lookup"><span data-stu-id="0c725-116">Where to create and delete your app passwords</span></span>

<span data-ttu-id="0c725-117">You're given an app password during your initial two-step verification registration.</span><span class="sxs-lookup"><span data-stu-id="0c725-117">You're given an app password during your initial two-step verification registration.</span></span> <span data-ttu-id="0c725-118">If you need more than that one password, you can create additional passwords, based on how you use two-step verification:</span><span class="sxs-lookup"><span data-stu-id="0c725-118">If you need more than that one password, you can create additional passwords, based on how you use two-step verification:</span></span>

- <span data-ttu-id="0c725-119">**You use two-step verification with your work or school account and the MyApps portal.**</span><span class="sxs-lookup"><span data-stu-id="0c725-119">**You use two-step verification with your work or school account and the MyApps portal.**</span></span> <span data-ttu-id="0c725-120">Create and delete your app passwords using the instructions in the [Create and delete app passwords using the MyApps portal](#create-and-delete-app-passwords-using-the-myapps-portal) section of this article.</span><span class="sxs-lookup"><span data-stu-id="0c725-120">Create and delete your app passwords using the instructions in the [Create and delete app passwords using the MyApps portal](#create-and-delete-app-passwords-using-the-myapps-portal) section of this article.</span></span> <span data-ttu-id="0c725-121">For more info about the MyApps portal and how to use it, see [What is the MyApps portal in Azure Active Directory?](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0c725-121">For more info about the MyApps portal and how to use it, see [What is the MyApps portal in Azure Active Directory?](active-directory-saas-access-panel-introduction.md).</span></span>

- <span data-ttu-id="0c725-122">**You use two-step verification with your work or school account and the Office 365 portal.**</span><span class="sxs-lookup"><span data-stu-id="0c725-122">**You use two-step verification with your work or school account and the Office 365 portal.**</span></span> <span data-ttu-id="0c725-123">Create and delete your app passwords using the instructions in the [Create and delete app passwords using the Office 365 portal](#create-and-delete-app-passwords-using-the-office-365-portal) section of this article.</span><span class="sxs-lookup"><span data-stu-id="0c725-123">Create and delete your app passwords using the instructions in the [Create and delete app passwords using the Office 365 portal](#create-and-delete-app-passwords-using-the-office-365-portal) section of this article.</span></span>

- <span data-ttu-id="0c725-124">**You use two-step verification with your personal Microsoft account.**</span><span class="sxs-lookup"><span data-stu-id="0c725-124">**You use two-step verification with your personal Microsoft account.**</span></span> <span data-ttu-id="0c725-125">Create and delete your app passwords using the [Security basics](https://account.microsoft.com/account/) page with your personal Microsoft account.</span><span class="sxs-lookup"><span data-stu-id="0c725-125">Create and delete your app passwords using the [Security basics](https://account.microsoft.com/account/) page with your personal Microsoft account.</span></span> <span data-ttu-id="0c725-126">For more info, see the [App passwords and two-step verification](https://support.microsoft.com/help/12409/microsoft-account-app-passwords-two-step-verification) article.</span><span class="sxs-lookup"><span data-stu-id="0c725-126">For more info, see the [App passwords and two-step verification](https://support.microsoft.com/help/12409/microsoft-account-app-passwords-two-step-verification) article.</span></span>

## <a name="create-and-delete-app-passwords-using-the-myapps-portal"></a><span data-ttu-id="0c725-127">Create and delete app passwords using the MyApps portal</span><span class="sxs-lookup"><span data-stu-id="0c725-127">Create and delete app passwords using the MyApps portal</span></span>
<span data-ttu-id="0c725-128">You can create and delete app passwords through the MyApps portal.</span><span class="sxs-lookup"><span data-stu-id="0c725-128">You can create and delete app passwords through the MyApps portal.</span></span>

### <a name="to-create-an-app-password-using-the-myapps-portal"></a><span data-ttu-id="0c725-129">To create an app password using the MyApps portal</span><span class="sxs-lookup"><span data-stu-id="0c725-129">To create an app password using the MyApps portal</span></span>

1. <span data-ttu-id="0c725-130">Sign in to [https://myapps.microsoft.com](https://myapps.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="0c725-130">Sign in to [https://myapps.microsoft.com](https://myapps.microsoft.com).</span></span>

2. <span data-ttu-id="0c725-131">Select your name at the top right, and choose **Profile**.</span><span class="sxs-lookup"><span data-stu-id="0c725-131">Select your name at the top right, and choose **Profile**.</span></span>

3. <span data-ttu-id="0c725-132">Select **Additional Security Verification**.</span><span class="sxs-lookup"><span data-stu-id="0c725-132">Select **Additional Security Verification**.</span></span>

   ![Select additional security verification - screenshot](./media/multi-factor-authentication-end-user-app-passwords/myapps1.png)

4. <span data-ttu-id="0c725-134">Select **App passwords**.</span><span class="sxs-lookup"><span data-stu-id="0c725-134">Select **App passwords**.</span></span>

   ![Select app passwords - screenshot](./media/multi-factor-authentication-end-user-app-passwords/apppass2.png)

5. <span data-ttu-id="0c725-136">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="0c725-136">Click **Create**.</span></span>

6. <span data-ttu-id="0c725-137">Type a name for the app password, and then select **Next**.</span><span class="sxs-lookup"><span data-stu-id="0c725-137">Type a name for the app password, and then select **Next**.</span></span>

7. <span data-ttu-id="0c725-138">Copy the app password to the clipboard and paste it into your app.</span><span class="sxs-lookup"><span data-stu-id="0c725-138">Copy the app password to the clipboard and paste it into your app.</span></span>
   
    ![Create an app password](./media/multi-factor-authentication-end-user-app-passwords/create2.png)

### <a name="to-delete-an-app-password-using-the-myapps-portal"></a><span data-ttu-id="0c725-140">To delete an app password using the MyApps portal</span><span class="sxs-lookup"><span data-stu-id="0c725-140">To delete an app password using the MyApps portal</span></span>

1. <span data-ttu-id="0c725-141">Go to your profile, and then select **Additional Security Verification**.</span><span class="sxs-lookup"><span data-stu-id="0c725-141">Go to your profile, and then select **Additional Security Verification**.</span></span>

2. <span data-ttu-id="0c725-142">Select **App passwords**, and then select **Delete** next to the app password you want to delete.</span><span class="sxs-lookup"><span data-stu-id="0c725-142">Select **App passwords**, and then select **Delete** next to the app password you want to delete.</span></span>

   ![Delete an app password](./media/multi-factor-authentication-end-user-app-passwords/delete1.png)

3. <span data-ttu-id="0c725-144">Select **Yes** to confirm you want to delete the password, and then select **Close**.</span><span class="sxs-lookup"><span data-stu-id="0c725-144">Select **Yes** to confirm you want to delete the password, and then select **Close**.</span></span>

## <a name="create-and-delete-app-passwords-using-the-office-365-portal"></a><span data-ttu-id="0c725-145">Create and delete app passwords using the Office 365 portal</span><span class="sxs-lookup"><span data-stu-id="0c725-145">Create and delete app passwords using the Office 365 portal</span></span>

<span data-ttu-id="0c725-146">If you use two-step verification with your work or school account and your Office 365 apps, you can create and delete your app passwords using the Office 365 portal.</span><span class="sxs-lookup"><span data-stu-id="0c725-146">If you use two-step verification with your work or school account and your Office 365 apps, you can create and delete your app passwords using the Office 365 portal.</span></span> <span data-ttu-id="0c725-147">You can have a maximum of 40 app passwords at any one time.</span><span class="sxs-lookup"><span data-stu-id="0c725-147">You can have a maximum of 40 app passwords at any one time.</span></span> <span data-ttu-id="0c725-148">If you need another app password after that limit, you'll have to delete one of your existing app passwords.</span><span class="sxs-lookup"><span data-stu-id="0c725-148">If you need another app password after that limit, you'll have to delete one of your existing app passwords.</span></span>

### <a name="to-create-app-passwords-using-the-office-365-portal"></a><span data-ttu-id="0c725-149">To create app passwords using the Office 365 portal</span><span class="sxs-lookup"><span data-stu-id="0c725-149">To create app passwords using the Office 365 portal</span></span>

1. <span data-ttu-id="0c725-150">Sign in to your work or school account.</span><span class="sxs-lookup"><span data-stu-id="0c725-150">Sign in to your work or school account.</span></span>

2. <span data-ttu-id="0c725-151">Go to https://portal.office.com, select the **Settings** icon from the upper right of the **Office 365 portal** page, and then expand **Additional security verification**.</span><span class="sxs-lookup"><span data-stu-id="0c725-151">Go to https://portal.office.com, select the **Settings** icon from the upper right of the **Office 365 portal** page, and then expand **Additional security verification**.</span></span>

    ![Office portal showing expanded additional security verification area](media/security-info/security-info-o365password.png)

3. <span data-ttu-id="0c725-153">Select the text that says, **Create and manage app passwords** to open the **app passwords** page.</span><span class="sxs-lookup"><span data-stu-id="0c725-153">Select the text that says, **Create and manage app passwords** to open the **app passwords** page.</span></span>

4. <span data-ttu-id="0c725-154">Select **Create**, type a friendly name for the app that needs the app password, and then select **Next**.</span><span class="sxs-lookup"><span data-stu-id="0c725-154">Select **Create**, type a friendly name for the app that needs the app password, and then select **Next**.</span></span>

5. <span data-ttu-id="0c725-155">Select **Copy password to clipboard**, and then select **Close**.</span><span class="sxs-lookup"><span data-stu-id="0c725-155">Select **Copy password to clipboard**, and then select **Close**.</span></span>

6. <span data-ttu-id="0c725-156">Use the copied app password to sign in to your non-browser app.</span><span class="sxs-lookup"><span data-stu-id="0c725-156">Use the copied app password to sign in to your non-browser app.</span></span> <span data-ttu-id="0c725-157">You only need to enter this password once and it's remembered for the future.</span><span class="sxs-lookup"><span data-stu-id="0c725-157">You only need to enter this password once and it's remembered for the future.</span></span>

### <a name="to-delete-app-passwords-using-the-office-365-portal"></a><span data-ttu-id="0c725-158">To delete app passwords using the Office 365 portal</span><span class="sxs-lookup"><span data-stu-id="0c725-158">To delete app passwords using the Office 365 portal</span></span>

1. <span data-ttu-id="0c725-159">Sign in to your work or school account.</span><span class="sxs-lookup"><span data-stu-id="0c725-159">Sign in to your work or school account.</span></span>

2. <span data-ttu-id="0c725-160">Go to https://portal.office.com, select the **Settings** icon from the upper right of the **Office 365 portal** page, and then select **Additional security verification**.</span><span class="sxs-lookup"><span data-stu-id="0c725-160">Go to https://portal.office.com, select the **Settings** icon from the upper right of the **Office 365 portal** page, and then select **Additional security verification**.</span></span>

3. <span data-ttu-id="0c725-161">Select the text that says, **Create and manage app passwords** to open the **app passwords** page.</span><span class="sxs-lookup"><span data-stu-id="0c725-161">Select the text that says, **Create and manage app passwords** to open the **app passwords** page.</span></span>

4. <span data-ttu-id="0c725-162">Select **Delete** for the app password to delete, select **Yes** in the confirmation box, and then select **Close**.</span><span class="sxs-lookup"><span data-stu-id="0c725-162">Select **Delete** for the app password to delete, select **Yes** in the confirmation box, and then select **Close**.</span></span>

    <span data-ttu-id="0c725-163">The app password is successfully deleted.</span><span class="sxs-lookup"><span data-stu-id="0c725-163">The app password is successfully deleted.</span></span>

5. <span data-ttu-id="0c725-164">Follow the steps for creating an app password to create your new app password.</span><span class="sxs-lookup"><span data-stu-id="0c725-164">Follow the steps for creating an app password to create your new app password.</span></span>

## <a name="if-your-app-passwords-arent-working-properly"></a><span data-ttu-id="0c725-165">If your app passwords aren't working properly</span><span class="sxs-lookup"><span data-stu-id="0c725-165">If your app passwords aren't working properly</span></span>

<span data-ttu-id="0c725-166">Make sure you typed your password correctly.</span><span class="sxs-lookup"><span data-stu-id="0c725-166">Make sure you typed your password correctly.</span></span> <span data-ttu-id="0c725-167">If you're sure you entered your password correctly, you can try to sign in again and create a new app password.</span><span class="sxs-lookup"><span data-stu-id="0c725-167">If you're sure you entered your password correctly, you can try to sign in again and create a new app password.</span></span> <span data-ttu-id="0c725-168">If neither of those options fix your problem, contact your company support so they can delete your existing app passwords, letting you create brand-new ones.</span><span class="sxs-lookup"><span data-stu-id="0c725-168">If neither of those options fix your problem, contact your company support so they can delete your existing app passwords, letting you create brand-new ones.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="0c725-169">Next steps</span><span class="sxs-lookup"><span data-stu-id="0c725-169">Next steps</span></span>

- [<span data-ttu-id="0c725-170">Manage your two-step verification settings</span><span class="sxs-lookup"><span data-stu-id="0c725-170">Manage your two-step verification settings</span></span>](multi-factor-authentication-end-user-manage-settings.md)

- <span data-ttu-id="0c725-171">Try out the [Microsoft Authenticator app](microsoft-authenticator-app-how-to.md) to verify your sign-ins with app notifications, instead of receiving texts or calls.</span><span class="sxs-lookup"><span data-stu-id="0c725-171">Try out the [Microsoft Authenticator app](microsoft-authenticator-app-how-to.md) to verify your sign-ins with app notifications, instead of receiving texts or calls.</span></span>
