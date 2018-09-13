---
title: What is the MyApps portal in Azure Active Directory? | Microsoft Docs
description: Learn how to use variations of the MyApps portal (web browser, Android app, iPhone and iPad app) to access SaaS apps.
services: active-directory
author: eross-msft
manager: mtillman
ms.assetid: c0252d01-7e6e-4f79-a70e-600479577dfd
ms.service: active-directory
ms.component: user-help
ms.workload: identity
ms.topic: conceptual
ms.date: 05/11/18
ms.author: lizross
ms.reviewer: asteen
ms.openlocfilehash: 2e74e45761a2f21c522f80d453da48948e17de58
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868207"
---
# <a name="what-is-the-myapps-portal"></a><span data-ttu-id="2b864-104">What is the MyApps portal?</span><span class="sxs-lookup"><span data-stu-id="2b864-104">What is the MyApps portal?</span></span>

<span data-ttu-id="2b864-105">If you have a work or school account in Azure Active Directory (Azure AD), you can use the My Apps web-based portal to view and start cloud-based applications that an Azure AD administrator has granted you access to.</span><span class="sxs-lookup"><span data-stu-id="2b864-105">If you have a work or school account in Azure Active Directory (Azure AD), you can use the My Apps web-based portal to view and start cloud-based applications that an Azure AD administrator has granted you access to.</span></span> <span data-ttu-id="2b864-106">You can also use self-service group and app management capabilities through the MyApps portal.</span><span class="sxs-lookup"><span data-stu-id="2b864-106">You can also use self-service group and app management capabilities through the MyApps portal.</span></span>

<span data-ttu-id="2b864-107">The MyApps portal is separate from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="2b864-107">The MyApps portal is separate from the Azure portal.</span></span> <span data-ttu-id="2b864-108">It does not require you to have an Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="2b864-108">It does not require you to have an Azure subscription.</span></span>

<span data-ttu-id="2b864-109">![MyApps portal][1] By using the MyApps portal, you can edit some of your profile settings and do the following:</span><span class="sxs-lookup"><span data-stu-id="2b864-109">![MyApps portal][1] By using the MyApps portal, you can edit some of your profile settings and do the following:</span></span>

- <span data-ttu-id="2b864-110">Change the password associated with a work or school account.</span><span class="sxs-lookup"><span data-stu-id="2b864-110">Change the password associated with a work or school account.</span></span>

- <span data-ttu-id="2b864-111">Edit password reset settings.</span><span class="sxs-lookup"><span data-stu-id="2b864-111">Edit password reset settings.</span></span>

- <span data-ttu-id="2b864-112">Edit contact and preference settings related to multi-factor authentication (for accounts that have been required to use it by an administrator).</span><span class="sxs-lookup"><span data-stu-id="2b864-112">Edit contact and preference settings related to multi-factor authentication (for accounts that have been required to use it by an administrator).</span></span>

- <span data-ttu-id="2b864-113">View account details, such as user ID, alternate email, mobile and office phone numbers, and devices.</span><span class="sxs-lookup"><span data-stu-id="2b864-113">View account details, such as user ID, alternate email, mobile and office phone numbers, and devices.</span></span>

- <span data-ttu-id="2b864-114">View and start cloud-based applications that the Azure AD administrator has granted you access to.</span><span class="sxs-lookup"><span data-stu-id="2b864-114">View and start cloud-based applications that the Azure AD administrator has granted you access to.</span></span> 

- <span data-ttu-id="2b864-115">Self-manage groups.</span><span class="sxs-lookup"><span data-stu-id="2b864-115">Self-manage groups.</span></span> <span data-ttu-id="2b864-116">Administrators can create and manage security groups and request security group memberships in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2b864-116">Administrators can create and manage security groups and request security group memberships in Azure AD.</span></span> <span data-ttu-id="2b864-117">For more information, see [Self-service group management for users in Azure AD](../users-groups-roles/groups-self-service-management.md) and [Manage your groups](../fundamentals/active-directory-manage-groups.md).</span><span class="sxs-lookup"><span data-stu-id="2b864-117">For more information, see [Self-service group management for users in Azure AD](../users-groups-roles/groups-self-service-management.md) and [Manage your groups](../fundamentals/active-directory-manage-groups.md).</span></span>

## <a name="access-the-myapps-portal"></a><span data-ttu-id="2b864-118">Access the MyApps portal</span><span class="sxs-lookup"><span data-stu-id="2b864-118">Access the MyApps portal</span></span>

<span data-ttu-id="2b864-119">You can access the MyApps portal by going to `http://myapps.microsoft.com`.</span><span class="sxs-lookup"><span data-stu-id="2b864-119">You can access the MyApps portal by going to `http://myapps.microsoft.com`.</span></span>

<span data-ttu-id="2b864-120">If you have custom branding configured for your sign-in page, you can load the branding by appending your organization’s domain to the URL (for example, `http://myapps.microsoft.com/<your domain>.com`).</span><span class="sxs-lookup"><span data-stu-id="2b864-120">If you have custom branding configured for your sign-in page, you can load the branding by appending your organization’s domain to the URL (for example, `http://myapps.microsoft.com/<your domain>.com`).</span></span>

<span data-ttu-id="2b864-121">You can use any active or verified domain name that has been configured in your Azure portal, as shown here: ![Wingtip Toys domain name][2]</span><span class="sxs-lookup"><span data-stu-id="2b864-121">You can use any active or verified domain name that has been configured in your Azure portal, as shown here: ![Wingtip Toys domain name][2]</span></span>  

<span data-ttu-id="2b864-122">Distribute the URL to all users who sign in to applications that are integrated with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2b864-122">Distribute the URL to all users who sign in to applications that are integrated with Azure AD.</span></span>

## <a name="authentication"></a><span data-ttu-id="2b864-123">Authentication</span><span class="sxs-lookup"><span data-stu-id="2b864-123">Authentication</span></span>

<span data-ttu-id="2b864-124">To reach the MyApps portal, you must be authenticated through a work or school account in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2b864-124">To reach the MyApps portal, you must be authenticated through a work or school account in Azure AD.</span></span> <span data-ttu-id="2b864-125">You can be authenticated to Azure AD directly.</span><span class="sxs-lookup"><span data-stu-id="2b864-125">You can be authenticated to Azure AD directly.</span></span> <span data-ttu-id="2b864-126">Alternatively, if an organization has configured federation by using Active Directory Federation Services (AD FS) or other technologies, you can be authenticated by Windows Server Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2b864-126">Alternatively, if an organization has configured federation by using Active Directory Federation Services (AD FS) or other technologies, you can be authenticated by Windows Server Active Directory.</span></span>

<span data-ttu-id="2b864-127">If you have a subscription for Azure or Office 365 and you have been using the Azure portal or an Office 365 application, you can view the list of applications without signing in again.</span><span class="sxs-lookup"><span data-stu-id="2b864-127">If you have a subscription for Azure or Office 365 and you have been using the Azure portal or an Office 365 application, you can view the list of applications without signing in again.</span></span> <span data-ttu-id="2b864-128">If you are not authenticated, you are prompted to sign in by using the username and password for your account in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2b864-128">If you are not authenticated, you are prompted to sign in by using the username and password for your account in Azure AD.</span></span> <span data-ttu-id="2b864-129">If your organization has configured federation, typing the username is sufficient.</span><span class="sxs-lookup"><span data-stu-id="2b864-129">If your organization has configured federation, typing the username is sufficient.</span></span>

<span data-ttu-id="2b864-130">When you are authenticated, you can interact with the applications that your administrator has integrated with the directory.</span><span class="sxs-lookup"><span data-stu-id="2b864-130">When you are authenticated, you can interact with the applications that your administrator has integrated with the directory.</span></span> <span data-ttu-id="2b864-131">To learn how to integrate applications with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="2b864-131">To learn how to integrate applications with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="web-browser-requirements"></a><span data-ttu-id="2b864-132">Web browser requirements</span><span class="sxs-lookup"><span data-stu-id="2b864-132">Web browser requirements</span></span>

<span data-ttu-id="2b864-133">At a minimum, the MyApps portal requires a browser that supports JavaScript and has CSS enabled.</span><span class="sxs-lookup"><span data-stu-id="2b864-133">At a minimum, the MyApps portal requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="2b864-134">To be signed in to applications through password-based single sign-on (SSO), you must have the MyApps portal extension installed in your browser.</span><span class="sxs-lookup"><span data-stu-id="2b864-134">To be signed in to applications through password-based single sign-on (SSO), you must have the MyApps portal extension installed in your browser.</span></span> <span data-ttu-id="2b864-135">The extension is downloaded automatically when you select an application that is configured for password-based SSO.</span><span class="sxs-lookup"><span data-stu-id="2b864-135">The extension is downloaded automatically when you select an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="2b864-136">The installer is architecture-specific.</span><span class="sxs-lookup"><span data-stu-id="2b864-136">The installer is architecture-specific.</span></span> <span data-ttu-id="2b864-137">If you click the download link, you only get the installer for the OS architecture that you are currently running on.</span><span class="sxs-lookup"><span data-stu-id="2b864-137">If you click the download link, you only get the installer for the OS architecture that you are currently running on.</span></span> <span data-ttu-id="2b864-138">If you are an application deployment administrator, make sure that you visit the download link from a 64 bit and 32 bit device to get both installers.</span><span class="sxs-lookup"><span data-stu-id="2b864-138">If you are an application deployment administrator, make sure that you visit the download link from a 64 bit and 32 bit device to get both installers.</span></span>


<span data-ttu-id="2b864-139">The MyApps portal extension is currently available for:</span><span class="sxs-lookup"><span data-stu-id="2b864-139">The MyApps portal extension is currently available for:</span></span>
- <span data-ttu-id="2b864-140">**Edge**: on Windows 10 Anniversary Edition or later.</span><span class="sxs-lookup"><span data-stu-id="2b864-140">**Edge**: on Windows 10 Anniversary Edition or later.</span></span> 
- <span data-ttu-id="2b864-141">**Chrome**: on Windows 7 or later, and on MacOS X or later.</span><span class="sxs-lookup"><span data-stu-id="2b864-141">**Chrome**: on Windows 7 or later, and on MacOS X or later.</span></span>
- <span data-ttu-id="2b864-142">**Firefox 26.0 or later**: on Windows XP SP2 or later, and on Mac OS X 10.6 or later.</span><span class="sxs-lookup"><span data-stu-id="2b864-142">**Firefox 26.0 or later**: on Windows XP SP2 or later, and on Mac OS X 10.6 or later.</span></span>
- <span data-ttu-id="2b864-143">**Internet Explorer 11**: on Windows 7 or later (limited support).</span><span class="sxs-lookup"><span data-stu-id="2b864-143">**Internet Explorer 11**: on Windows 7 or later (limited support).</span></span>

## <a name="my-apps-secure-sign-in-extension"></a><span data-ttu-id="2b864-144">My Apps Secure Sign-in Extension</span><span class="sxs-lookup"><span data-stu-id="2b864-144">My Apps Secure Sign-in Extension</span></span>
<span data-ttu-id="2b864-145">To sign in to password-based single sign-on, you must use the extension.</span><span class="sxs-lookup"><span data-stu-id="2b864-145">To sign in to password-based single sign-on, you must use the extension.</span></span> <span data-ttu-id="2b864-146">After the extension is installed, you can sign in to it to enable additional features by selecting **Sign in to get started**.</span><span class="sxs-lookup"><span data-stu-id="2b864-146">After the extension is installed, you can sign in to it to enable additional features by selecting **Sign in to get started**.</span></span> 

- <span data-ttu-id="2b864-147">You can sign in to an app directly by using the app's **Sign-on URL**.</span><span class="sxs-lookup"><span data-stu-id="2b864-147">You can sign in to an app directly by using the app's **Sign-on URL**.</span></span> <span data-ttu-id="2b864-148">When you use the app's URL, the extension detects the action and gives you the option of signing in from the extension.</span><span class="sxs-lookup"><span data-stu-id="2b864-148">When you use the app's URL, the extension detects the action and gives you the option of signing in from the extension.</span></span>
- <span data-ttu-id="2b864-149">You can launch any of your apps from the MyApps portal by using the *quick search* feature of the extension.</span><span class="sxs-lookup"><span data-stu-id="2b864-149">You can launch any of your apps from the MyApps portal by using the *quick search* feature of the extension.</span></span> 
- <span data-ttu-id="2b864-150">The extension shows you the last three applications that you launched in **Recently Used** section.</span><span class="sxs-lookup"><span data-stu-id="2b864-150">The extension shows you the last three applications that you launched in **Recently Used** section.</span></span>
- <span data-ttu-id="2b864-151">You can use internal company URLs while remote through [Application Proxy](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-get-started)</span><span class="sxs-lookup"><span data-stu-id="2b864-151">You can use internal company URLs while remote through [Application Proxy](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-get-started)</span></span>

> [!NOTE]
> <span data-ttu-id="2b864-152">Additional features are available only for Edge, Chrome, and Firefox.</span><span class="sxs-lookup"><span data-stu-id="2b864-152">Additional features are available only for Edge, Chrome, and Firefox.</span></span>
>
<span data-ttu-id="2b864-153">You can download the extension directly from the following sites:</span><span class="sxs-lookup"><span data-stu-id="2b864-153">You can download the extension directly from the following sites:</span></span>
- [<span data-ttu-id="2b864-154">Chrome</span><span class="sxs-lookup"><span data-stu-id="2b864-154">Chrome</span></span>](https://go.microsoft.com/fwlink/?linkid=866367)
- [<span data-ttu-id="2b864-155">Edge</span><span class="sxs-lookup"><span data-stu-id="2b864-155">Edge</span></span>](https://go.microsoft.com/fwlink/?linkid=845176)
- [<span data-ttu-id="2b864-156">Firefox</span><span class="sxs-lookup"><span data-stu-id="2b864-156">Firefox</span></span>](https://go.microsoft.com/fwlink/?linkid=866366)

<span data-ttu-id="2b864-157">If you are using a My Apps URL other than `https://myapps.microsoft.com`, configure your default URL by doing the following:</span><span class="sxs-lookup"><span data-stu-id="2b864-157">If you are using a My Apps URL other than `https://myapps.microsoft.com`, configure your default URL by doing the following:</span></span>
1. <span data-ttu-id="2b864-158">While you are *not* signed in to the extension, right-click the extension icon.</span><span class="sxs-lookup"><span data-stu-id="2b864-158">While you are *not* signed in to the extension, right-click the extension icon.</span></span>
2. <span data-ttu-id="2b864-159">On the menu, select **My Apps URL**.</span><span class="sxs-lookup"><span data-stu-id="2b864-159">On the menu, select **My Apps URL**.</span></span>
3. <span data-ttu-id="2b864-160">Select your default URL.</span><span class="sxs-lookup"><span data-stu-id="2b864-160">Select your default URL.</span></span>
4. <span data-ttu-id="2b864-161">Select the extension icon.</span><span class="sxs-lookup"><span data-stu-id="2b864-161">Select the extension icon.</span></span>
5. <span data-ttu-id="2b864-162">Select **Sign in to get started**.</span><span class="sxs-lookup"><span data-stu-id="2b864-162">Select **Sign in to get started**.</span></span>

<span data-ttu-id="2b864-163">To use internal company URLs while remote using the extension, do the following:</span><span class="sxs-lookup"><span data-stu-id="2b864-163">To use internal company URLs while remote using the extension, do the following:</span></span>
1. <span data-ttu-id="2b864-164">[Configure Application Proxy](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-enable) on your tenant.</span><span class="sxs-lookup"><span data-stu-id="2b864-164">[Configure Application Proxy](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-enable) on your tenant.</span></span>
2. <span data-ttu-id="2b864-165">[Publish the application](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal) and URL through Application Proxy.</span><span class="sxs-lookup"><span data-stu-id="2b864-165">[Publish the application](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal) and URL through Application Proxy.</span></span>
3. <span data-ttu-id="2b864-166">Install the extension, and sign in to it by selecting Sign in to get started.</span><span class="sxs-lookup"><span data-stu-id="2b864-166">Install the extension, and sign in to it by selecting Sign in to get started.</span></span>
4. <span data-ttu-id="2b864-167">You can now browse to the internal company URL even while remote.</span><span class="sxs-lookup"><span data-stu-id="2b864-167">You can now browse to the internal company URL even while remote.</span></span>

> [!NOTE]
> <span data-ttu-id="2b864-168">You may also turn off automatic redirection to company URLs by selecting the settings gear on the main menu and selecting **off** for the Company internal URL redirection option.</span><span class="sxs-lookup"><span data-stu-id="2b864-168">You may also turn off automatic redirection to company URLs by selecting the settings gear on the main menu and selecting **off** for the Company internal URL redirection option.</span></span>


## <a name="mobile-app-support"></a><span data-ttu-id="2b864-169">Mobile app support</span><span class="sxs-lookup"><span data-stu-id="2b864-169">Mobile app support</span></span>

<span data-ttu-id="2b864-170">The Azure Active Directory team publishes the My Apps mobile app.</span><span class="sxs-lookup"><span data-stu-id="2b864-170">The Azure Active Directory team publishes the My Apps mobile app.</span></span> <span data-ttu-id="2b864-171">When you install the app, you can sign in to password-based SSO applications on iOS and Android devices.</span><span class="sxs-lookup"><span data-stu-id="2b864-171">When you install the app, you can sign in to password-based SSO applications on iOS and Android devices.</span></span>

> [!NOTE]
> <span data-ttu-id="2b864-172">You can sign in to applications that support federation with Azure AD (including Salesforce, Google Apps, Dropbox, Box, Concur, Workday, Office 365, and more than 70 others) on virtually any web browser, on any device, without needing a plug-in or mobile app.</span><span class="sxs-lookup"><span data-stu-id="2b864-172">You can sign in to applications that support federation with Azure AD (including Salesforce, Google Apps, Dropbox, Box, Concur, Workday, Office 365, and more than 70 others) on virtually any web browser, on any device, without needing a plug-in or mobile app.</span></span> <span data-ttu-id="2b864-173">To be used on a mobile device, the other [MyApps portal experiences](https://myapps.microsoft.com/) also do not require the My Apps mobile app.</span><span class="sxs-lookup"><span data-stu-id="2b864-173">To be used on a mobile device, the other [MyApps portal experiences](https://myapps.microsoft.com/) also do not require the My Apps mobile app.</span></span>

### <a name="my-apps-for-iphone-and-ipad"></a><span data-ttu-id="2b864-174">My Apps for iPhone and iPad</span><span class="sxs-lookup"><span data-stu-id="2b864-174">My Apps for iPhone and iPad</span></span>

<span data-ttu-id="2b864-175">My Apps for iOS is supported on any iPhone or iPad that is running iOS version 7 or later.</span><span class="sxs-lookup"><span data-stu-id="2b864-175">My Apps for iOS is supported on any iPhone or iPad that is running iOS version 7 or later.</span></span>  

<span data-ttu-id="2b864-176">It is available at the [Apple App Store](https://itunes.apple.com/us/app/my-apps-azure-active-directory/id824048653?mt=8).</span><span class="sxs-lookup"><span data-stu-id="2b864-176">It is available at the [Apple App Store](https://itunes.apple.com/us/app/my-apps-azure-active-directory/id824048653?mt=8).</span></span>

![My Apps for iOS][4]    


## <a name="intune-managed-browser-for-my-apps"></a><span data-ttu-id="2b864-178">Intune Managed Browser for My Apps</span><span class="sxs-lookup"><span data-stu-id="2b864-178">Intune Managed Browser for My Apps</span></span>

<span data-ttu-id="2b864-179">My Apps is also integrated with the Intune Managed Browser.</span><span class="sxs-lookup"><span data-stu-id="2b864-179">My Apps is also integrated with the Intune Managed Browser.</span></span> <span data-ttu-id="2b864-180">The Intune Managed Browser for iOS and Android devices helps you to more safely view and navigate webpages that might contain company information, helping to provide a more secure web-browsing experience.</span><span class="sxs-lookup"><span data-stu-id="2b864-180">The Intune Managed Browser for iOS and Android devices helps you to more safely view and navigate webpages that might contain company information, helping to provide a more secure web-browsing experience.</span></span>  

<span data-ttu-id="2b864-181">You can get to My Apps from both the Managed Browser home page and from your bookmarks, which means there are fewer clicks needed to reach your apps.</span><span class="sxs-lookup"><span data-stu-id="2b864-181">You can get to My Apps from both the Managed Browser home page and from your bookmarks, which means there are fewer clicks needed to reach your apps.</span></span>

<span data-ttu-id="2b864-182">Intune Managed Browser is available at the [Apple App Store](https://itunes.apple.com/us/app/microsoft-intune-managed-browser/id943264951?mt=8) and [Google Play Store](https://play.google.com/store/apps/details?id=com.microsoft.intune.mam.managedbrowser).</span><span class="sxs-lookup"><span data-stu-id="2b864-182">Intune Managed Browser is available at the [Apple App Store](https://itunes.apple.com/us/app/microsoft-intune-managed-browser/id943264951?mt=8) and [Google Play Store](https://play.google.com/store/apps/details?id=com.microsoft.intune.mam.managedbrowser).</span></span>

![Managed browser for My Apps][5]    


## <a name="tips-for-testing-the-user-experience"></a><span data-ttu-id="2b864-184">Tips for testing the user experience</span><span class="sxs-lookup"><span data-stu-id="2b864-184">Tips for testing the user experience</span></span>

<span data-ttu-id="2b864-185">If you are an Azure administrator and you are signed in to the Azure portal by using an account in the directory, you are automatically signed in to the MyApps portal as your current account.</span><span class="sxs-lookup"><span data-stu-id="2b864-185">If you are an Azure administrator and you are signed in to the Azure portal by using an account in the directory, you are automatically signed in to the MyApps portal as your current account.</span></span> <span data-ttu-id="2b864-186">This view displays all applications that are assigned to you.</span><span class="sxs-lookup"><span data-stu-id="2b864-186">This view displays all applications that are assigned to you.</span></span>

<span data-ttu-id="2b864-187">To test in a *different* user account, do the following:</span><span class="sxs-lookup"><span data-stu-id="2b864-187">To test in a *different* user account, do the following:</span></span>

1. <span data-ttu-id="2b864-188">At the upper right of the Azure portal or the MyApps portal, select **Sign Out**.</span><span class="sxs-lookup"><span data-stu-id="2b864-188">At the upper right of the Azure portal or the MyApps portal, select **Sign Out**.</span></span> 
2. <span data-ttu-id="2b864-189">Go to the [MyApps portal](http://myapps.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="2b864-189">Go to the [MyApps portal](http://myapps.microsoft.com).</span></span>
3. <span data-ttu-id="2b864-190">On the sign-in page, type the username and password for the account in your directory that you want to test.</span><span class="sxs-lookup"><span data-stu-id="2b864-190">On the sign-in page, type the username and password for the account in your directory that you want to test.</span></span>


## <a name="starting-applications"></a><span data-ttu-id="2b864-191">Starting applications</span><span class="sxs-lookup"><span data-stu-id="2b864-191">Starting applications</span></span>

<span data-ttu-id="2b864-192">This section discusses several types of applications that can appear on the MyApps portal.</span><span class="sxs-lookup"><span data-stu-id="2b864-192">This section discusses several types of applications that can appear on the MyApps portal.</span></span>

### <a name="office-365-applications"></a><span data-ttu-id="2b864-193">Office 365 applications</span><span class="sxs-lookup"><span data-stu-id="2b864-193">Office 365 applications</span></span>

<span data-ttu-id="2b864-194">If your organization is using Office 365 applications and you are licensed for them, the Office 365 applications appear on your MyApps portal.</span><span class="sxs-lookup"><span data-stu-id="2b864-194">If your organization is using Office 365 applications and you are licensed for them, the Office 365 applications appear on your MyApps portal.</span></span>

<span data-ttu-id="2b864-195">When you select an application tile for an Office 365 application, you are redirected to the application and automatically signed in.</span><span class="sxs-lookup"><span data-stu-id="2b864-195">When you select an application tile for an Office 365 application, you are redirected to the application and automatically signed in.</span></span>

### <a name="microsoft-and-third-party-applications-configured-with-federation-based-sso"></a><span data-ttu-id="2b864-196">Microsoft and third-party applications configured with federation-based SSO</span><span class="sxs-lookup"><span data-stu-id="2b864-196">Microsoft and third-party applications configured with federation-based SSO</span></span>

<span data-ttu-id="2b864-197">Your administrator can add applications in the Active Directory section of the Azure portal with the SSO mode set to **Azure AD Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="2b864-197">Your administrator can add applications in the Active Directory section of the Azure portal with the SSO mode set to **Azure AD Single Sign-On**.</span></span> <span data-ttu-id="2b864-198">You can see these applications only if your administrator has explicitly granted you access to them.</span><span class="sxs-lookup"><span data-stu-id="2b864-198">You can see these applications only if your administrator has explicitly granted you access to them.</span></span>

<span data-ttu-id="2b864-199">When you select a tile for an application, you are redirected and automatically signed in to it.</span><span class="sxs-lookup"><span data-stu-id="2b864-199">When you select a tile for an application, you are redirected and automatically signed in to it.</span></span>

### <a name="password-based-sso-without-identity-provisioning"></a><span data-ttu-id="2b864-200">Password-based SSO without identity provisioning</span><span class="sxs-lookup"><span data-stu-id="2b864-200">Password-based SSO without identity provisioning</span></span>

<span data-ttu-id="2b864-201">Your administrator can add applications in the Active Directory section of the Azure portal with the SSO mode set to **Password-based Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="2b864-201">Your administrator can add applications in the Active Directory section of the Azure portal with the SSO mode set to **Password-based Single Sign-On**.</span></span> <span data-ttu-id="2b864-202">All users in the directory can see all applications that have been configured in this mode.</span><span class="sxs-lookup"><span data-stu-id="2b864-202">All users in the directory can see all applications that have been configured in this mode.</span></span>

<span data-ttu-id="2b864-203">The first time you select an application tile, you are prompted to install the Password SSO plug-in for Internet Explorer or Chrome.</span><span class="sxs-lookup"><span data-stu-id="2b864-203">The first time you select an application tile, you are prompted to install the Password SSO plug-in for Internet Explorer or Chrome.</span></span> <span data-ttu-id="2b864-204">The installation might require you to restart your web browser.</span><span class="sxs-lookup"><span data-stu-id="2b864-204">The installation might require you to restart your web browser.</span></span> <span data-ttu-id="2b864-205">When you return to the MyApps portal and select the application tile again, you are prompted for a username and password for the application.</span><span class="sxs-lookup"><span data-stu-id="2b864-205">When you return to the MyApps portal and select the application tile again, you are prompted for a username and password for the application.</span></span> <span data-ttu-id="2b864-206">When you have entered your username and password, the credentials are securely stored and linked to your account in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2b864-206">When you have entered your username and password, the credentials are securely stored and linked to your account in Azure AD.</span></span>

<span data-ttu-id="2b864-207">The next time you select the application tile, you are automatically signed in to the application.</span><span class="sxs-lookup"><span data-stu-id="2b864-207">The next time you select the application tile, you are automatically signed in to the application.</span></span>  

<span data-ttu-id="2b864-208">You don't have to enter your credentials again and or install the Password SSO plug-in.</span><span class="sxs-lookup"><span data-stu-id="2b864-208">You don't have to enter your credentials again and or install the Password SSO plug-in.</span></span>

<span data-ttu-id="2b864-209">If your credentials have changed in the target third-party application, you must also update your credentials that are stored in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2b864-209">If your credentials have changed in the target third-party application, you must also update your credentials that are stored in Azure AD.</span></span> 

<span data-ttu-id="2b864-210">To update your credentials, do the following:</span><span class="sxs-lookup"><span data-stu-id="2b864-210">To update your credentials, do the following:</span></span>

1. <span data-ttu-id="2b864-211">Select the icon on the application tile.</span><span class="sxs-lookup"><span data-stu-id="2b864-211">Select the icon on the application tile.</span></span>
2. <span data-ttu-id="2b864-212">Select **update credentials** to reenter the username and password for the application.</span><span class="sxs-lookup"><span data-stu-id="2b864-212">Select **update credentials** to reenter the username and password for the application.</span></span>


### <a name="password-based-sso-with-identity-provisioning"></a><span data-ttu-id="2b864-213">Password-based SSO with identity provisioning</span><span class="sxs-lookup"><span data-stu-id="2b864-213">Password-based SSO with identity provisioning</span></span>

<span data-ttu-id="2b864-214">Your administrator can add applications in the Active Directory section of the Azure portal with the SSO mode set to **Password-based Single Sign-On**, along with identity provisioning.</span><span class="sxs-lookup"><span data-stu-id="2b864-214">Your administrator can add applications in the Active Directory section of the Azure portal with the SSO mode set to **Password-based Single Sign-On**, along with identity provisioning.</span></span>

<span data-ttu-id="2b864-215">The first time you select an application tile, you are prompted to install the Password SSO plug-in for Internet Explorer or Chrome.</span><span class="sxs-lookup"><span data-stu-id="2b864-215">The first time you select an application tile, you are prompted to install the Password SSO plug-in for Internet Explorer or Chrome.</span></span> <span data-ttu-id="2b864-216">The installation might require you to restart your web browser.</span><span class="sxs-lookup"><span data-stu-id="2b864-216">The installation might require you to restart your web browser.</span></span>  

<span data-ttu-id="2b864-217">When you return to the MyApps portal and select the application tile again, you are automatically signed in to the application.</span><span class="sxs-lookup"><span data-stu-id="2b864-217">When you return to the MyApps portal and select the application tile again, you are automatically signed in to the application.</span></span>

<span data-ttu-id="2b864-218">Some applications might require you to change your password at the first sign-in.</span><span class="sxs-lookup"><span data-stu-id="2b864-218">Some applications might require you to change your password at the first sign-in.</span></span> <span data-ttu-id="2b864-219">If your credentials have changed in the target third-party application, you must also update the credentials that are stored in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2b864-219">If your credentials have changed in the target third-party application, you must also update the credentials that are stored in Azure AD.</span></span> 

<span data-ttu-id="2b864-220">To update your credentials, do the following:</span><span class="sxs-lookup"><span data-stu-id="2b864-220">To update your credentials, do the following:</span></span>

1. <span data-ttu-id="2b864-221">Select the icon on the application tile.</span><span class="sxs-lookup"><span data-stu-id="2b864-221">Select the icon on the application tile.</span></span>
2. <span data-ttu-id="2b864-222">Select **update credentials** to reenter the username and password for the application.</span><span class="sxs-lookup"><span data-stu-id="2b864-222">Select **update credentials** to reenter the username and password for the application.</span></span>


### <a name="application-with-existing-sso-solutions"></a><span data-ttu-id="2b864-223">Application with existing SSO solutions</span><span class="sxs-lookup"><span data-stu-id="2b864-223">Application with existing SSO solutions</span></span>

<span data-ttu-id="2b864-224">To configure SSO for an application, the Azure portal provides a third option called Existing Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="2b864-224">To configure SSO for an application, the Azure portal provides a third option called Existing Single Sign-On.</span></span> <span data-ttu-id="2b864-225">This option enables your administrator to create a link to an application and place it on the MyApps portal for selected users.</span><span class="sxs-lookup"><span data-stu-id="2b864-225">This option enables your administrator to create a link to an application and place it on the MyApps portal for selected users.</span></span>

<span data-ttu-id="2b864-226">For example, if an application is configured to authenticate users by using AD FS 2.0, your administrator can use the Existing Single Sign-On option to create a link to it on the MyApps portal.</span><span class="sxs-lookup"><span data-stu-id="2b864-226">For example, if an application is configured to authenticate users by using AD FS 2.0, your administrator can use the Existing Single Sign-On option to create a link to it on the MyApps portal.</span></span> <span data-ttu-id="2b864-227">When you access the link, you are authenticated through AD FS 2.0 or whatever existing SSO solution the application provides.</span><span class="sxs-lookup"><span data-stu-id="2b864-227">When you access the link, you are authenticated through AD FS 2.0 or whatever existing SSO solution the application provides.</span></span>


## <a name="next-steps"></a><span data-ttu-id="2b864-228">Next steps</span><span class="sxs-lookup"><span data-stu-id="2b864-228">Next steps</span></span>

- <span data-ttu-id="2b864-229">To view a list of all topics that are related to application management, see the [article index for application management in Azure Active Directory](../active-directory-apps-index.md).</span><span class="sxs-lookup"><span data-stu-id="2b864-229">To view a list of all topics that are related to application management, see the [article index for application management in Azure Active Directory](../active-directory-apps-index.md).</span></span>
 
- <span data-ttu-id="2b864-230">To learn how to integrate a SaaS app with Azure AD, see the [list of tutorials on how to integrate SaaS apps](../saas-apps/tutorial-list.md).</span><span class="sxs-lookup"><span data-stu-id="2b864-230">To learn how to integrate a SaaS app with Azure AD, see the [list of tutorials on how to integrate SaaS apps](../saas-apps/tutorial-list.md).</span></span>
 
- <span data-ttu-id="2b864-231">To learn more about managing apps with Azure AD, see the [introduction to single sign-on and managing app access with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="2b864-231">To learn more about managing apps with Azure AD, see the [introduction to single sign-on and managing app access with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>
 
- <span data-ttu-id="2b864-232">To learn more about user provisioning, see [automate user provisioning and deprovisioning to SaaS applications](../manage-apps/user-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="2b864-232">To learn more about user provisioning, see [automate user provisioning and deprovisioning to SaaS applications](../manage-apps/user-provisioning.md).</span></span>

<!--Image references-->
[1]: ./media/active-directory-saas-access-panel-introduction/01.png
[2]: ./media/active-directory-saas-access-panel-introduction/02.png
[4]: ./media/active-directory-saas-access-panel-introduction/04.png
[5]: ./media/active-directory-saas-access-panel-introduction/05.png
