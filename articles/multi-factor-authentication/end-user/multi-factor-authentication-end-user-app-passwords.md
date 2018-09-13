---
title: How to use App Passwords in Azure MFA? | Microsoft Docs
description: This page will help users understand what app passwords are and what they are used for with regard to Azure MFA.
services: multi-factor-authentication
documentationcenter: ''
author: kgremban
manager: femila
editor: yossib
ms.assetid: 345b757b-5a2b-48eb-953f-d363313be9e5
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/15/2017
ms.author: kgremban
ms.custom: end-user
ms.openlocfilehash: 5ab21f53d3ab6be9a4bd6e6f11b42fe166cc70ed
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662419"
---
# <a name="what-are-app-passwords-in-azure-multi-factor-authentication"></a><span data-ttu-id="0d97e-104">What are App Passwords in Azure Multi-Factor Authentication?</span><span class="sxs-lookup"><span data-stu-id="0d97e-104">What are App Passwords in Azure Multi-Factor Authentication?</span></span>
<span data-ttu-id="0d97e-105">Certain non-browser apps, such as the Apple native email client that uses Exchange Active Sync, currently do not support multi-factor authentication.</span><span class="sxs-lookup"><span data-stu-id="0d97e-105">Certain non-browser apps, such as the Apple native email client that uses Exchange Active Sync, currently do not support multi-factor authentication.</span></span> <span data-ttu-id="0d97e-106">Multi-factor authentication is enabled per user.</span><span class="sxs-lookup"><span data-stu-id="0d97e-106">Multi-factor authentication is enabled per user.</span></span> <span data-ttu-id="0d97e-107">This means that if a user has been enabled for multi-factor authentication and they are attempting to use non-browser apps, they will be unable to do so.</span><span class="sxs-lookup"><span data-stu-id="0d97e-107">This means that if a user has been enabled for multi-factor authentication and they are attempting to use non-browser apps, they will be unable to do so.</span></span> <span data-ttu-id="0d97e-108">An app password allows this to occur.</span><span class="sxs-lookup"><span data-stu-id="0d97e-108">An app password allows this to occur.</span></span>

<span data-ttu-id="0d97e-109">Once you have an app password, you use this in place of your original password with these non-browser apps.</span><span class="sxs-lookup"><span data-stu-id="0d97e-109">Once you have an app password, you use this in place of your original password with these non-browser apps.</span></span> <span data-ttu-id="0d97e-110">This is because when you register for two-step verification, you're telling Microsoft not to let anyone sign in with your password if they can't also perform the second verification.</span><span class="sxs-lookup"><span data-stu-id="0d97e-110">This is because when you register for two-step verification, you're telling Microsoft not to let anyone sign in with your password if they can't also perform the second verification.</span></span> <span data-ttu-id="0d97e-111">The Apple native email client on your phone can't sign in as you because it can't ask for two-step verification.</span><span class="sxs-lookup"><span data-stu-id="0d97e-111">The Apple native email client on your phone can't sign in as you because it can't ask for two-step verification.</span></span> <span data-ttu-id="0d97e-112">The solution for this is to create a more secure app password that you don't use day-to-day, but only for those apps that can't support two-step verification.</span><span class="sxs-lookup"><span data-stu-id="0d97e-112">The solution for this is to create a more secure app password that you don't use day-to-day, but only for those apps that can't support two-step verification.</span></span> <span data-ttu-id="0d97e-113">Use the app password so that apps can bypass multi-factor authentication and continue to work.</span><span class="sxs-lookup"><span data-stu-id="0d97e-113">Use the app password so that apps can bypass multi-factor authentication and continue to work.</span></span>

> [!NOTE]
> <span data-ttu-id="0d97e-114">Office 2013 clients (including Outlook) support new authentication protocols and can be used with two-step verification.</span><span class="sxs-lookup"><span data-stu-id="0d97e-114">Office 2013 clients (including Outlook) support new authentication protocols and can be used with two-step verification.</span></span>  <span data-ttu-id="0d97e-115">This means that once enabled, app passwords are not required for use with Office 2013 clients.</span><span class="sxs-lookup"><span data-stu-id="0d97e-115">This means that once enabled, app passwords are not required for use with Office 2013 clients.</span></span>  <span data-ttu-id="0d97e-116">For more information, see [Office 2013 modern authentication public preview announced](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/).</span><span class="sxs-lookup"><span data-stu-id="0d97e-116">For more information, see [Office 2013 modern authentication public preview announced](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/).</span></span>


## <a name="how-to-use-app-passwords"></a><span data-ttu-id="0d97e-117">How to use app passwords</span><span class="sxs-lookup"><span data-stu-id="0d97e-117">How to use app passwords</span></span>
<span data-ttu-id="0d97e-118">The following are some things to remember on how to use app passwords.</span><span class="sxs-lookup"><span data-stu-id="0d97e-118">The following are some things to remember on how to use app passwords.</span></span>

* <span data-ttu-id="0d97e-119">You don't create your own app passwords.</span><span class="sxs-lookup"><span data-stu-id="0d97e-119">You don't create your own app passwords.</span></span> <span data-ttu-id="0d97e-120">Instead, they are automatically generated.</span><span class="sxs-lookup"><span data-stu-id="0d97e-120">Instead, they are automatically generated.</span></span> <span data-ttu-id="0d97e-121">Since you only have to enter the app password once per app, it's safer to use a more complex, automatically generated password rather than making one that you can remember.</span><span class="sxs-lookup"><span data-stu-id="0d97e-121">Since you only have to enter the app password once per app, it's safer to use a more complex, automatically generated password rather than making one that you can remember.</span></span>
* <span data-ttu-id="0d97e-122">Currently there is a limit of 40 passwords per user.</span><span class="sxs-lookup"><span data-stu-id="0d97e-122">Currently there is a limit of 40 passwords per user.</span></span> <span data-ttu-id="0d97e-123">If you attempt to create one after you have reached the limit, you will be prompted to delete one of your existing app passwords before you create a new one.</span><span class="sxs-lookup"><span data-stu-id="0d97e-123">If you attempt to create one after you have reached the limit, you will be prompted to delete one of your existing app passwords before you create a new one.</span></span>
* <span data-ttu-id="0d97e-124">You should use one app password per device, not per application.</span><span class="sxs-lookup"><span data-stu-id="0d97e-124">You should use one app password per device, not per application.</span></span> <span data-ttu-id="0d97e-125">For example, you can create one app password for your laptop and use that app password for all of your applications on that laptop.</span><span class="sxs-lookup"><span data-stu-id="0d97e-125">For example, you can create one app password for your laptop and use that app password for all of your applications on that laptop.</span></span> <span data-ttu-id="0d97e-126">Then, create a second app password to use for all your apps on your desktop.</span><span class="sxs-lookup"><span data-stu-id="0d97e-126">Then, create a second app password to use for all your apps on your desktop.</span></span> 
* <span data-ttu-id="0d97e-127">You are given one app password the first time you register for two-step verification.</span><span class="sxs-lookup"><span data-stu-id="0d97e-127">You are given one app password the first time you register for two-step verification.</span></span>  <span data-ttu-id="0d97e-128">If you need additional ones, you can create them.</span><span class="sxs-lookup"><span data-stu-id="0d97e-128">If you need additional ones, you can create them.</span></span>



## <a name="creating-and-deleting-app-passwords"></a><span data-ttu-id="0d97e-129">Creating and deleting app passwords</span><span class="sxs-lookup"><span data-stu-id="0d97e-129">Creating and deleting app passwords</span></span>
<span data-ttu-id="0d97e-130">During your initial sign-in you are given an app password that you can use.</span><span class="sxs-lookup"><span data-stu-id="0d97e-130">During your initial sign-in you are given an app password that you can use.</span></span>  <span data-ttu-id="0d97e-131">Additionally you can also create and delete app passwords later on.</span><span class="sxs-lookup"><span data-stu-id="0d97e-131">Additionally you can also create and delete app passwords later on.</span></span>  <span data-ttu-id="0d97e-132">How you do this depends on how you use multi-factor authentication.</span><span class="sxs-lookup"><span data-stu-id="0d97e-132">How you do this depends on how you use multi-factor authentication.</span></span> <span data-ttu-id="0d97e-133">Answer the following questions to determine where you should go to manage app passwords:</span><span class="sxs-lookup"><span data-stu-id="0d97e-133">Answer the following questions to determine where you should go to manage app passwords:</span></span> 

1. <span data-ttu-id="0d97e-134">Do you use two-step verification for your personal Microsoft account?</span><span class="sxs-lookup"><span data-stu-id="0d97e-134">Do you use two-step verification for your personal Microsoft account?</span></span> <span data-ttu-id="0d97e-135">If yes, you should refer to the [App passwords and two-step verification](https://support.microsoft.com/help/12409/microsoft-account-app-passwords-two-step-verification) article for help.</span><span class="sxs-lookup"><span data-stu-id="0d97e-135">If yes, you should refer to the [App passwords and two-step verification](https://support.microsoft.com/help/12409/microsoft-account-app-passwords-two-step-verification) article for help.</span></span> <span data-ttu-id="0d97e-136">If no, continue to question two.</span><span class="sxs-lookup"><span data-stu-id="0d97e-136">If no, continue to question two.</span></span>

2. <span data-ttu-id="0d97e-137">Ok, so you use two-step verification for your work or school account.</span><span class="sxs-lookup"><span data-stu-id="0d97e-137">Ok, so you use two-step verification for your work or school account.</span></span> <span data-ttu-id="0d97e-138">Do you use it to sign in to Office 365 apps?</span><span class="sxs-lookup"><span data-stu-id="0d97e-138">Do you use it to sign in to Office 365 apps?</span></span> <span data-ttu-id="0d97e-139">If yes, you should refer to [Create an app password for Office 365](https://support.office.com/article/Create-an-app-password-for-Office-365-3e7c860f-bda4-4441-a618-b53953ee1183) for help.</span><span class="sxs-lookup"><span data-stu-id="0d97e-139">If yes, you should refer to [Create an app password for Office 365](https://support.office.com/article/Create-an-app-password-for-Office-365-3e7c860f-bda4-4441-a618-b53953ee1183) for help.</span></span> <span data-ttu-id="0d97e-140">If no, continue to question three.</span><span class="sxs-lookup"><span data-stu-id="0d97e-140">If no, continue to question three.</span></span> 

3. <span data-ttu-id="0d97e-141">Do you use two-step verification with Microsoft Azure?</span><span class="sxs-lookup"><span data-stu-id="0d97e-141">Do you use two-step verification with Microsoft Azure?</span></span> <span data-ttu-id="0d97e-142">If yes, continue to the [Manage app passwords in the Azure portal](#manage-app-passwords-in-the-Azure-portal) section of this article.</span><span class="sxs-lookup"><span data-stu-id="0d97e-142">If yes, continue to the [Manage app passwords in the Azure portal](#manage-app-passwords-in-the-Azure-portal) section of this article.</span></span> <span data-ttu-id="0d97e-143">If no, continue to question four.</span><span class="sxs-lookup"><span data-stu-id="0d97e-143">If no, continue to question four.</span></span>

4. <span data-ttu-id="0d97e-144">Not sure where you use two-step verification?</span><span class="sxs-lookup"><span data-stu-id="0d97e-144">Not sure where you use two-step verification?</span></span> <span data-ttu-id="0d97e-145">Continue to the [Manage app passwords with the MyApps portal](#manage-app-passwords-with-the-myapps-portal) section of this article.</span><span class="sxs-lookup"><span data-stu-id="0d97e-145">Continue to the [Manage app passwords with the MyApps portal](#manage-app-passwords-with-the-myapps-portal) section of this article.</span></span> 


## <a name="manage-app-passwords-in-the-azure-portal"></a><span data-ttu-id="0d97e-146">Manage app passwords in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="0d97e-146">Manage app passwords in the Azure portal</span></span>
<span data-ttu-id="0d97e-147">If you use two-step verification with Azure, you want to create app passwords through the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="0d97e-147">If you use two-step verification with Azure, you want to create app passwords through the Azure portal.</span></span>

### <a name="to-create-app-passwords-in-the-azure-portal"></a><span data-ttu-id="0d97e-148">To create app passwords in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="0d97e-148">To create app passwords in the Azure portal</span></span>
1. <span data-ttu-id="0d97e-149">Sign in to the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="0d97e-149">Sign in to the Azure classic portal.</span></span>
2. <span data-ttu-id="0d97e-150">At the top, right-click your user name and select Additional Security Verification.</span><span class="sxs-lookup"><span data-stu-id="0d97e-150">At the top, right-click your user name and select Additional Security Verification.</span></span>
3. <span data-ttu-id="0d97e-151">On the proofup page, at the top, select app passwords</span><span class="sxs-lookup"><span data-stu-id="0d97e-151">On the proofup page, at the top, select app passwords</span></span>
4. <span data-ttu-id="0d97e-152">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="0d97e-152">Click **Create**.</span></span>
5. <span data-ttu-id="0d97e-153">Enter a name for the app password and click **Next**</span><span class="sxs-lookup"><span data-stu-id="0d97e-153">Enter a name for the app password and click **Next**</span></span>
6. <span data-ttu-id="0d97e-154">Copy the app password to the clipboard and paste it into your app.</span><span class="sxs-lookup"><span data-stu-id="0d97e-154">Copy the app password to the clipboard and paste it into your app.</span></span>

   ![Cloud](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/end-user/media/multi-factor-authentication-end-user-app-passwords/app2.png)

### <a name="to-delete-app-passwords-in-the-azure-portal"></a><span data-ttu-id="0d97e-156">To delete app passwords in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="0d97e-156">To delete app passwords in the Azure portal</span></span>
1. <span data-ttu-id="0d97e-157">Sign in to the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="0d97e-157">Sign in to the Azure classic portal.</span></span>
2. <span data-ttu-id="0d97e-158">At the top, right-click your user name and select Additional Security Verification.</span><span class="sxs-lookup"><span data-stu-id="0d97e-158">At the top, right-click your user name and select Additional Security Verification.</span></span>
3. <span data-ttu-id="0d97e-159">At the top, next to additional security verification, select **app passwords.**</span><span class="sxs-lookup"><span data-stu-id="0d97e-159">At the top, next to additional security verification, select **app passwords.**</span></span>
4. <span data-ttu-id="0d97e-160">Next to the app password you want to delete, select **Delete**.</span><span class="sxs-lookup"><span data-stu-id="0d97e-160">Next to the app password you want to delete, select **Delete**.</span></span>
5. <span data-ttu-id="0d97e-161">Confirm the deletion by clicking **yes**.</span><span class="sxs-lookup"><span data-stu-id="0d97e-161">Confirm the deletion by clicking **yes**.</span></span>
6. <span data-ttu-id="0d97e-162">Once the app password is deleted, you can click **close**.</span><span class="sxs-lookup"><span data-stu-id="0d97e-162">Once the app password is deleted, you can click **close**.</span></span>


## <a name="manage-app-passwords-with-the-myapps-portal"></a><span data-ttu-id="0d97e-163">Manage app passwords with the MyApps portal.</span><span class="sxs-lookup"><span data-stu-id="0d97e-163">Manage app passwords with the MyApps portal.</span></span>
<span data-ttu-id="0d97e-164">If you are not sure how you use multi-factor authentication, then you can always create and delete app passwords through the myapps portal.</span><span class="sxs-lookup"><span data-stu-id="0d97e-164">If you are not sure how you use multi-factor authentication, then you can always create and delete app passwords through the myapps portal.</span></span>

### <a name="to-create-an-app-password-using-the-myapps-portal"></a><span data-ttu-id="0d97e-165">To create an app password using the Myapps portal</span><span class="sxs-lookup"><span data-stu-id="0d97e-165">To create an app password using the Myapps portal</span></span>
1. <span data-ttu-id="0d97e-166">Sign in to [https://myapps.microsoft.com](https://myapps.microsoft.com)</span><span class="sxs-lookup"><span data-stu-id="0d97e-166">Sign in to [https://myapps.microsoft.com](https://myapps.microsoft.com)</span></span>
2. <span data-ttu-id="0d97e-167">Click your name at the top right, and choose **Profile**.</span><span class="sxs-lookup"><span data-stu-id="0d97e-167">Click your name at the top right, and choose **Profile**.</span></span>
3. <span data-ttu-id="0d97e-168">Select **Additional Security Verification**.</span><span class="sxs-lookup"><span data-stu-id="0d97e-168">Select **Additional Security Verification**.</span></span>

   ![Select additional security verification - screenshot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/end-user/media/multi-factor-authentication-end-user-manage/myapps1.png)

4. <span data-ttu-id="0d97e-170">Select **app passwords**.</span><span class="sxs-lookup"><span data-stu-id="0d97e-170">Select **app passwords**.</span></span>

   ![Select app passwords - screenshot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/end-user/media/multi-factor-authentication-end-user-app-passwords/apppass2.png)

5. <span data-ttu-id="0d97e-172">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="0d97e-172">Click **Create**.</span></span>
6. <span data-ttu-id="0d97e-173">Enter a name for the app password and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="0d97e-173">Enter a name for the app password and click **Next**.</span></span>
7. <span data-ttu-id="0d97e-174">Copy the app password to the clipboard and paste it into your app.</span><span class="sxs-lookup"><span data-stu-id="0d97e-174">Copy the app password to the clipboard and paste it into your app.</span></span>

   ![Create an app password](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/end-user/media/multi-factor-authentication-end-user-app-passwords/create2.png)

### <a name="to-delete-an-app-password-using-the-myapps-portal"></a><span data-ttu-id="0d97e-176">To delete an app password using the Myapps portal</span><span class="sxs-lookup"><span data-stu-id="0d97e-176">To delete an app password using the Myapps portal</span></span>
1. <span data-ttu-id="0d97e-177">Sign in to [https://myapps.microsoft.com](https://myapps.microsoft.com)</span><span class="sxs-lookup"><span data-stu-id="0d97e-177">Sign in to [https://myapps.microsoft.com](https://myapps.microsoft.com)</span></span>
2. <span data-ttu-id="0d97e-178">At the top, select profile.</span><span class="sxs-lookup"><span data-stu-id="0d97e-178">At the top, select profile.</span></span>
3. <span data-ttu-id="0d97e-179">Select **Additional Security Verification**.</span><span class="sxs-lookup"><span data-stu-id="0d97e-179">Select **Additional Security Verification**.</span></span>

   ![Select additional security verification - screenshot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/end-user/media/multi-factor-authentication-end-user-manage/myapps1.png)

4. <span data-ttu-id="0d97e-181">Select **app passwords**.</span><span class="sxs-lookup"><span data-stu-id="0d97e-181">Select **app passwords**.</span></span>

   ![Select app passwords - screenshot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/end-user/media/multi-factor-authentication-end-user-app-passwords/apppass2.png)

5. <span data-ttu-id="0d97e-183">Next to the app password you want to delete, click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="0d97e-183">Next to the app password you want to delete, click **Delete**.</span></span>

   ![Delete an app password](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/end-user/media/multi-factor-authentication-end-user-app-passwords/delete1.png)

6. <span data-ttu-id="0d97e-185">Confirm that you want to delete that password by clicking **yes**.</span><span class="sxs-lookup"><span data-stu-id="0d97e-185">Confirm that you want to delete that password by clicking **yes**.</span></span>
7. <span data-ttu-id="0d97e-186">Once the app password is deleted, you can click **close**.</span><span class="sxs-lookup"><span data-stu-id="0d97e-186">Once the app password is deleted, you can click **close**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0d97e-187">Next steps</span><span class="sxs-lookup"><span data-stu-id="0d97e-187">Next steps</span></span>

- [<span data-ttu-id="0d97e-188">Manage your two-step verification settings</span><span class="sxs-lookup"><span data-stu-id="0d97e-188">Manage your two-step verification settings</span></span>](multi-factor-authentication-end-user-manage-settings.md)

- <span data-ttu-id="0d97e-189">Try out the [Microsoft Authenticator app](microsoft-authenticator-app-how-to.md) to verify your sign-ins with app notifications, instead of receiving texts or calls.</span><span class="sxs-lookup"><span data-stu-id="0d97e-189">Try out the [Microsoft Authenticator app](microsoft-authenticator-app-how-to.md) to verify your sign-ins with app notifications, instead of receiving texts or calls.</span></span> 







