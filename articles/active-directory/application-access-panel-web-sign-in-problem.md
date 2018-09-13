---
title: Problem signing in to the access panel website | Microsoft Docs
description: Guidance to troubleshoot issues you may encounter while trying to sign in to use the Access Panel
services: active-directory
documentationcenter: ''
author: ajamess
manager: femila
ms.assetid: ''
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: asteen
ms.openlocfilehash: bbd57547a0cc486a9cf7c8030dccaaf6f46c9860
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563725"
---
# <a name="problem-signing-in-to-the-access-panel-website"></a><span data-ttu-id="5b07b-103">Problem signing in to the access panel website</span><span class="sxs-lookup"><span data-stu-id="5b07b-103">Problem signing in to the access panel website</span></span>

<span data-ttu-id="5b07b-104">The Access Panel is a web-based portal which enables a user who has a work or school account in Azure Active Directory (Azure AD) to view and launch cloud-based applications that the Azure AD administrator has granted them access to.</span><span class="sxs-lookup"><span data-stu-id="5b07b-104">The Access Panel is a web-based portal which enables a user who has a work or school account in Azure Active Directory (Azure AD) to view and launch cloud-based applications that the Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="5b07b-105">A user who has Azure AD editions can also use self-service group and app management capabilities through the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="5b07b-105">A user who has Azure AD editions can also use self-service group and app management capabilities through the Access Panel.</span></span> <span data-ttu-id="5b07b-106">The Access Panel is separate from the Azure portal and does not require users to have an Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="5b07b-106">The Access Panel is separate from the Azure portal and does not require users to have an Azure subscription.</span></span>

<span data-ttu-id="5b07b-107">Users can sign in to the Access Panel if they have a work or school account in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5b07b-107">Users can sign in to the Access Panel if they have a work or school account in Azure AD.</span></span>

-   <span data-ttu-id="5b07b-108">Users can be authenticated by Azure AD directly.</span><span class="sxs-lookup"><span data-stu-id="5b07b-108">Users can be authenticated by Azure AD directly.</span></span>

-   <span data-ttu-id="5b07b-109">Users can be authenticated by using Active Directory Federation Services (AD FS).</span><span class="sxs-lookup"><span data-stu-id="5b07b-109">Users can be authenticated by using Active Directory Federation Services (AD FS).</span></span>

-   <span data-ttu-id="5b07b-110">Users can be authenticated by Windows Server Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5b07b-110">Users can be authenticated by Windows Server Active Directory.</span></span>

<span data-ttu-id="5b07b-111">If a user has a subscription for Azure or Office 365 and has been using the Azure portal or an Office 365 application, they'll be able to use the Access Panel seamlessly without needing to sign in again.</span><span class="sxs-lookup"><span data-stu-id="5b07b-111">If a user has a subscription for Azure or Office 365 and has been using the Azure portal or an Office 365 application, they'll be able to use the Access Panel seamlessly without needing to sign in again.</span></span> <span data-ttu-id="5b07b-112">Users who are not authenticated be prompted to sign in by using the username and password for their account in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5b07b-112">Users who are not authenticated be prompted to sign in by using the username and password for their account in Azure AD.</span></span> <span data-ttu-id="5b07b-113">If the organization has configured federation, typing the username is sufficient.</span><span class="sxs-lookup"><span data-stu-id="5b07b-113">If the organization has configured federation, typing the username is sufficient.</span></span>

## <a name="general-issues-to-check-first"></a><span data-ttu-id="5b07b-114">General issues to check first</span><span class="sxs-lookup"><span data-stu-id="5b07b-114">General issues to check first</span></span> 

-   <span data-ttu-id="5b07b-115">Make sure the user is signing in to the **correct URL**: <https://myapps.microsoft.com></span><span class="sxs-lookup"><span data-stu-id="5b07b-115">Make sure the user is signing in to the **correct URL**: <https://myapps.microsoft.com></span></span>

-   <span data-ttu-id="5b07b-116">Make sure the user’s browser has added the URL to its **trusted sites**</span><span class="sxs-lookup"><span data-stu-id="5b07b-116">Make sure the user’s browser has added the URL to its **trusted sites**</span></span>

-   <span data-ttu-id="5b07b-117">Make sure the user’s account is **enabled** for sign ins.</span><span class="sxs-lookup"><span data-stu-id="5b07b-117">Make sure the user’s account is **enabled** for sign ins.</span></span>

-   <span data-ttu-id="5b07b-118">Make sure the user’s account is **not locked out.**</span><span class="sxs-lookup"><span data-stu-id="5b07b-118">Make sure the user’s account is **not locked out.**</span></span>

-   <span data-ttu-id="5b07b-119">Make sure the user’s **password is not expired or forgotten.**</span><span class="sxs-lookup"><span data-stu-id="5b07b-119">Make sure the user’s **password is not expired or forgotten.**</span></span>

-   <span data-ttu-id="5b07b-120">Make sure **Multi-Factor Authentication** is not blocking user access.</span><span class="sxs-lookup"><span data-stu-id="5b07b-120">Make sure **Multi-Factor Authentication** is not blocking user access.</span></span>

-   <span data-ttu-id="5b07b-121">Make sure a **Conditional Access policy** or **Identity Protection** policy is not blocking user access.</span><span class="sxs-lookup"><span data-stu-id="5b07b-121">Make sure a **Conditional Access policy** or **Identity Protection** policy is not blocking user access.</span></span>

-   <span data-ttu-id="5b07b-122">Make sure that a user’s **authentication contact info** is up to date to allow Multi-Factor Authentication or Conditional Access policies to be enforced.</span><span class="sxs-lookup"><span data-stu-id="5b07b-122">Make sure that a user’s **authentication contact info** is up to date to allow Multi-Factor Authentication or Conditional Access policies to be enforced.</span></span>

-   <span data-ttu-id="5b07b-123">Make sure to also try clearing your browser’s cookies and trying to sign in again.</span><span class="sxs-lookup"><span data-stu-id="5b07b-123">Make sure to also try clearing your browser’s cookies and trying to sign in again.</span></span>

## <a name="meeting-browser-requirements-for-the-access-panel"></a><span data-ttu-id="5b07b-124">Meeting browser requirements for the Access Panel</span><span class="sxs-lookup"><span data-stu-id="5b07b-124">Meeting browser requirements for the Access Panel</span></span>

<span data-ttu-id="5b07b-125">The Access Panel requires a browser that supports JavaScript and has CSS enabled.</span><span class="sxs-lookup"><span data-stu-id="5b07b-125">The Access Panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="5b07b-126">To use password-based single sign-on (SSO) in the Access Panel, the Access Panel extension must be installed in the user’s browser.</span><span class="sxs-lookup"><span data-stu-id="5b07b-126">To use password-based single sign-on (SSO) in the Access Panel, the Access Panel extension must be installed in the user’s browser.</span></span> <span data-ttu-id="5b07b-127">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span><span class="sxs-lookup"><span data-stu-id="5b07b-127">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="5b07b-128">For password-based SSO, the end user’s browsers can be:</span><span class="sxs-lookup"><span data-stu-id="5b07b-128">For password-based SSO, the end user’s browsers can be:</span></span>

-   <span data-ttu-id="5b07b-129">Internet Explorer 8, 9, 10, 11 -- on Windows 7 or later</span><span class="sxs-lookup"><span data-stu-id="5b07b-129">Internet Explorer 8, 9, 10, 11 -- on Windows 7 or later</span></span>

-   <span data-ttu-id="5b07b-130">Chrome -- on Windows 7 or later, and on MacOS X or later</span><span class="sxs-lookup"><span data-stu-id="5b07b-130">Chrome -- on Windows 7 or later, and on MacOS X or later</span></span>

-   <span data-ttu-id="5b07b-131">Firefox 26.0 or later -- on Windows XP SP2 or later, and on Mac OS X 10.6 or later</span><span class="sxs-lookup"><span data-stu-id="5b07b-131">Firefox 26.0 or later -- on Windows XP SP2 or later, and on Mac OS X 10.6 or later</span></span>

>[!NOTE] 
><span data-ttu-id="5b07b-132">The password-based SSO extension become available for Edge in Windows 10 when browser extensions become supported for Edge.</span><span class="sxs-lookup"><span data-stu-id="5b07b-132">The password-based SSO extension become available for Edge in Windows 10 when browser extensions become supported for Edge.</span></span>
>
>

## <a name="problems-with-the-users-account"></a><span data-ttu-id="5b07b-133">Problems with the user’s account</span><span class="sxs-lookup"><span data-stu-id="5b07b-133">Problems with the user’s account</span></span>

<span data-ttu-id="5b07b-134">Access to the Access Panel can be blocked due to a problem with the user’s account.</span><span class="sxs-lookup"><span data-stu-id="5b07b-134">Access to the Access Panel can be blocked due to a problem with the user’s account.</span></span> <span data-ttu-id="5b07b-135">Below are some ways you can troubleshoot and solve problems with users and their account settings:</span><span class="sxs-lookup"><span data-stu-id="5b07b-135">Below are some ways you can troubleshoot and solve problems with users and their account settings:</span></span>

-   [<span data-ttu-id="5b07b-136">Check if a user account exists in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5b07b-136">Check if a user account exists in Azure Active Directory</span></span>](#check-if-a-user-account-exists-in-azure-active-directory)

-   [<span data-ttu-id="5b07b-137">Check a user’s account status</span><span class="sxs-lookup"><span data-stu-id="5b07b-137">Check a user’s account status</span></span>](#check-a-users-account-status)

-   [<span data-ttu-id="5b07b-138">Reset a user’s password</span><span class="sxs-lookup"><span data-stu-id="5b07b-138">Reset a user’s password</span></span>](#reset-a-users-password)

-   [<span data-ttu-id="5b07b-139">Enable self-service password reset</span><span class="sxs-lookup"><span data-stu-id="5b07b-139">Enable self-service password reset</span></span>](#enable-self-service-password-reset)

-   [<span data-ttu-id="5b07b-140">Check a user’s multi-factor authentication status</span><span class="sxs-lookup"><span data-stu-id="5b07b-140">Check a user’s multi-factor authentication status</span></span>](#check-a-users-multi-factor-authentication-status)

-   [<span data-ttu-id="5b07b-141">Check a user’s authentication contact info</span><span class="sxs-lookup"><span data-stu-id="5b07b-141">Check a user’s authentication contact info</span></span>](#check-a-users-authentication-contact-info)

-   [<span data-ttu-id="5b07b-142">Check a user’s group memberships</span><span class="sxs-lookup"><span data-stu-id="5b07b-142">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

-   [<span data-ttu-id="5b07b-143">Check a user’s assigned licenses</span><span class="sxs-lookup"><span data-stu-id="5b07b-143">Check a user’s assigned licenses</span></span>](#check-a-users-assigned-licenses)

-   [<span data-ttu-id="5b07b-144">Assign a user a license</span><span class="sxs-lookup"><span data-stu-id="5b07b-144">Assign a user a license</span></span>](#assign-a-user-a-license)

### <a name="check-if-a-user-account-exists-in-azure-active-directory"></a><span data-ttu-id="5b07b-145">Check if a user account exists in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5b07b-145">Check if a user account exists in Azure Active Directory</span></span>

<span data-ttu-id="5b07b-146">To check if a user’s account is present, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="5b07b-146">To check if a user’s account is present, follow the steps below:</span></span>

1.  <span data-ttu-id="5b07b-147">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span><span class="sxs-lookup"><span data-stu-id="5b07b-147">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="5b07b-148">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="5b07b-148">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5b07b-149">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="5b07b-149">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5b07b-150">click **Users and groups** in the navigation menu.</span><span class="sxs-lookup"><span data-stu-id="5b07b-150">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="5b07b-151">click **All users**.</span><span class="sxs-lookup"><span data-stu-id="5b07b-151">click **All users**.</span></span>

6.  <span data-ttu-id="5b07b-152">**Search** for the user you are interested in and **click the row** to select.</span><span class="sxs-lookup"><span data-stu-id="5b07b-152">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="5b07b-153">Check the properties of the user object to be sure that they look as you expect and no data is missing.</span><span class="sxs-lookup"><span data-stu-id="5b07b-153">Check the properties of the user object to be sure that they look as you expect and no data is missing.</span></span>

### <a name="check-a-users-account-status"></a><span data-ttu-id="5b07b-154">Check a user’s account status</span><span class="sxs-lookup"><span data-stu-id="5b07b-154">Check a user’s account status</span></span>

<span data-ttu-id="5b07b-155">To check a user’s account status, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="5b07b-155">To check a user’s account status, follow the steps below:</span></span>

1.  <span data-ttu-id="5b07b-156">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span><span class="sxs-lookup"><span data-stu-id="5b07b-156">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="5b07b-157">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="5b07b-157">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5b07b-158">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="5b07b-158">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5b07b-159">click **Users and groups** in the navigation menu.</span><span class="sxs-lookup"><span data-stu-id="5b07b-159">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="5b07b-160">click **All users**.</span><span class="sxs-lookup"><span data-stu-id="5b07b-160">click **All users**.</span></span>

6.  <span data-ttu-id="5b07b-161">**Search** for the user you are interested in and **click the row** to select.</span><span class="sxs-lookup"><span data-stu-id="5b07b-161">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="5b07b-162">click **Profile**.</span><span class="sxs-lookup"><span data-stu-id="5b07b-162">click **Profile**.</span></span>

8.  <span data-ttu-id="5b07b-163">Under **Settings** ensure that **Block sign in** is set to **No**.</span><span class="sxs-lookup"><span data-stu-id="5b07b-163">Under **Settings** ensure that **Block sign in** is set to **No**.</span></span>

### <a name="reset-a-users-password"></a><span data-ttu-id="5b07b-164">Reset a user’s password</span><span class="sxs-lookup"><span data-stu-id="5b07b-164">Reset a user’s password</span></span>

<span data-ttu-id="5b07b-165">To reset a user’s password, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="5b07b-165">To reset a user’s password, follow the steps below:</span></span>

1.  <span data-ttu-id="5b07b-166">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span><span class="sxs-lookup"><span data-stu-id="5b07b-166">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="5b07b-167">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="5b07b-167">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5b07b-168">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="5b07b-168">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5b07b-169">click **Users and groups** in the navigation menu.</span><span class="sxs-lookup"><span data-stu-id="5b07b-169">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="5b07b-170">click **All users**.</span><span class="sxs-lookup"><span data-stu-id="5b07b-170">click **All users**.</span></span>

6.  <span data-ttu-id="5b07b-171">**Search** for the user you are interested in and **click the row** to select.</span><span class="sxs-lookup"><span data-stu-id="5b07b-171">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="5b07b-172">click the **Reset password** button at the top of the user blade.</span><span class="sxs-lookup"><span data-stu-id="5b07b-172">click the **Reset password** button at the top of the user blade.</span></span>

8.  <span data-ttu-id="5b07b-173">click the **Reset password** button on the **Reset password** blade that appears.</span><span class="sxs-lookup"><span data-stu-id="5b07b-173">click the **Reset password** button on the **Reset password** blade that appears.</span></span>

9.  <span data-ttu-id="5b07b-174">Copy the **temporary password** or **enter a new password** for the user.</span><span class="sxs-lookup"><span data-stu-id="5b07b-174">Copy the **temporary password** or **enter a new password** for the user.</span></span>

10. <span data-ttu-id="5b07b-175">Communicate this new password to the user, they be required to change this password during their next sign in to Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5b07b-175">Communicate this new password to the user, they be required to change this password during their next sign in to Azure Active Directory.</span></span>

### <a name="enable-self-service-password-reset"></a><span data-ttu-id="5b07b-176">Enable self-service password reset</span><span class="sxs-lookup"><span data-stu-id="5b07b-176">Enable self-service password reset</span></span>

<span data-ttu-id="5b07b-177">To enable self-service password reset, follow the deployment steps below:</span><span class="sxs-lookup"><span data-stu-id="5b07b-177">To enable self-service password reset, follow the deployment steps below:</span></span>

-   [<span data-ttu-id="5b07b-178">Enable users to reset their Azure Active Directory passwords</span><span class="sxs-lookup"><span data-stu-id="5b07b-178">Enable users to reset their Azure Active Directory passwords</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-their-azure-ad-passwords)

-   [<span data-ttu-id="5b07b-179">Enable users to reset or change their Active Directory on-premises passwords</span><span class="sxs-lookup"><span data-stu-id="5b07b-179">Enable users to reset or change their Active Directory on-premises passwords</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-or-change-their-ad-passwords)

### <a name="check-a-users-multi-factor-authentication-status"></a><span data-ttu-id="5b07b-180">Check a user’s multi-factor authentication status</span><span class="sxs-lookup"><span data-stu-id="5b07b-180">Check a user’s multi-factor authentication status</span></span>

<span data-ttu-id="5b07b-181">To check a user’s multi-factor authentication status, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="5b07b-181">To check a user’s multi-factor authentication status, follow the steps below:</span></span>

1.  <span data-ttu-id="5b07b-182">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span><span class="sxs-lookup"><span data-stu-id="5b07b-182">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="5b07b-183">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="5b07b-183">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5b07b-184">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="5b07b-184">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5b07b-185">click **Users and groups** in the navigation menu.</span><span class="sxs-lookup"><span data-stu-id="5b07b-185">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="5b07b-186">click **All users**.</span><span class="sxs-lookup"><span data-stu-id="5b07b-186">click **All users**.</span></span>

6.  <span data-ttu-id="5b07b-187">click the **Multi-Factor Authentication** button at the top of the blade.</span><span class="sxs-lookup"><span data-stu-id="5b07b-187">click the **Multi-Factor Authentication** button at the top of the blade.</span></span>

7.  <span data-ttu-id="5b07b-188">Once the **Multi-Factor Authentication Administration Portal** loads, ensure you are on the **Users** tab.</span><span class="sxs-lookup"><span data-stu-id="5b07b-188">Once the **Multi-Factor Authentication Administration Portal** loads, ensure you are on the **Users** tab.</span></span>

8.  <span data-ttu-id="5b07b-189">Find the user in the list of users by searching, filtering, or sorting.</span><span class="sxs-lookup"><span data-stu-id="5b07b-189">Find the user in the list of users by searching, filtering, or sorting.</span></span>

9.  <span data-ttu-id="5b07b-190">Select the user from the list of users and **Enable**, **Disable**, or **Enforce** multi-factor authentication as desired.</span><span class="sxs-lookup"><span data-stu-id="5b07b-190">Select the user from the list of users and **Enable**, **Disable**, or **Enforce** multi-factor authentication as desired.</span></span>

   >[!NOTE]
   ><span data-ttu-id="5b07b-191">If a user is in an **Enforced** state, you may set them to **Disabled** temporarily to let them back into their account.</span><span class="sxs-lookup"><span data-stu-id="5b07b-191">If a user is in an **Enforced** state, you may set them to **Disabled** temporarily to let them back into their account.</span></span> <span data-ttu-id="5b07b-192">Once they are back in, you can then change their state to **Enabled** again to require them to re-register their contact information during their next sign in.</span><span class="sxs-lookup"><span data-stu-id="5b07b-192">Once they are back in, you can then change their state to **Enabled** again to require them to re-register their contact information during their next sign in.</span></span> <span data-ttu-id="5b07b-193">Alternatively, you can follow the steps in the [Check a user’s authentication contact info](#check-a-users-authentication-contact-info) to verify or set this data for them.</span><span class="sxs-lookup"><span data-stu-id="5b07b-193">Alternatively, you can follow the steps in the [Check a user’s authentication contact info](#check-a-users-authentication-contact-info) to verify or set this data for them.</span></span>
   >
   >

### <a name="check-a-users-authentication-contact-info"></a><span data-ttu-id="5b07b-194">Check a user’s authentication contact info</span><span class="sxs-lookup"><span data-stu-id="5b07b-194">Check a user’s authentication contact info</span></span>

<span data-ttu-id="5b07b-195">To check a user’s authentication contact info used for Multi-factor authentication, Conditional Access, Identity Protection, and Password Reset, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="5b07b-195">To check a user’s authentication contact info used for Multi-factor authentication, Conditional Access, Identity Protection, and Password Reset, follow the steps below:</span></span>

1.  <span data-ttu-id="5b07b-196">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span><span class="sxs-lookup"><span data-stu-id="5b07b-196">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="5b07b-197">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="5b07b-197">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5b07b-198">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="5b07b-198">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5b07b-199">click **Users and groups** in the navigation menu.</span><span class="sxs-lookup"><span data-stu-id="5b07b-199">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="5b07b-200">click **All users**.</span><span class="sxs-lookup"><span data-stu-id="5b07b-200">click **All users**.</span></span>

6.  <span data-ttu-id="5b07b-201">**Search** for the user you are interested in and **click the row** to select.</span><span class="sxs-lookup"><span data-stu-id="5b07b-201">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="5b07b-202">click **Profile**.</span><span class="sxs-lookup"><span data-stu-id="5b07b-202">click **Profile**.</span></span>

8.  <span data-ttu-id="5b07b-203">Scroll down to **Authentication contact info**.</span><span class="sxs-lookup"><span data-stu-id="5b07b-203">Scroll down to **Authentication contact info**.</span></span>

9.  <span data-ttu-id="5b07b-204">**Review** the data registered for the user and update as needed.</span><span class="sxs-lookup"><span data-stu-id="5b07b-204">**Review** the data registered for the user and update as needed.</span></span>

### <a name="check-a-users-group-memberships"></a><span data-ttu-id="5b07b-205">Check a user’s group memberships</span><span class="sxs-lookup"><span data-stu-id="5b07b-205">Check a user’s group memberships</span></span>

<span data-ttu-id="5b07b-206">To check a user’s group memberships, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="5b07b-206">To check a user’s group memberships, follow the steps below:</span></span>

1.  <span data-ttu-id="5b07b-207">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span><span class="sxs-lookup"><span data-stu-id="5b07b-207">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="5b07b-208">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="5b07b-208">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5b07b-209">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="5b07b-209">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5b07b-210">click **Users and groups** in the navigation menu.</span><span class="sxs-lookup"><span data-stu-id="5b07b-210">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="5b07b-211">click **All users**.</span><span class="sxs-lookup"><span data-stu-id="5b07b-211">click **All users**.</span></span>

6.  <span data-ttu-id="5b07b-212">**Search** for the user you are interested in and **click the row** to select.</span><span class="sxs-lookup"><span data-stu-id="5b07b-212">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="5b07b-213">click **Groups** to see which groups the user is a member of.</span><span class="sxs-lookup"><span data-stu-id="5b07b-213">click **Groups** to see which groups the user is a member of.</span></span>

### <a name="check-a-users-assigned-licenses"></a><span data-ttu-id="5b07b-214">Check a user’s assigned licenses</span><span class="sxs-lookup"><span data-stu-id="5b07b-214">Check a user’s assigned licenses</span></span>

<span data-ttu-id="5b07b-215">To check a user’s assigned licenses, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="5b07b-215">To check a user’s assigned licenses, follow the steps below:</span></span>

1.  <span data-ttu-id="5b07b-216">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span><span class="sxs-lookup"><span data-stu-id="5b07b-216">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="5b07b-217">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="5b07b-217">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5b07b-218">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="5b07b-218">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5b07b-219">click **Users and groups** in the navigation menu.</span><span class="sxs-lookup"><span data-stu-id="5b07b-219">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="5b07b-220">click **All users**.</span><span class="sxs-lookup"><span data-stu-id="5b07b-220">click **All users**.</span></span>

6.  <span data-ttu-id="5b07b-221">**Search** for the user you are interested in and **click the row** to select.</span><span class="sxs-lookup"><span data-stu-id="5b07b-221">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="5b07b-222">click **Licenses** to see which licenses the user currently has assigned.</span><span class="sxs-lookup"><span data-stu-id="5b07b-222">click **Licenses** to see which licenses the user currently has assigned.</span></span>

### <a name="assign-a-user-a-license"></a><span data-ttu-id="5b07b-223">Assign a user a license</span><span class="sxs-lookup"><span data-stu-id="5b07b-223">Assign a user a license</span></span> 

<span data-ttu-id="5b07b-224">To assign a license to a user, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="5b07b-224">To assign a license to a user, follow the steps below:</span></span>

1.  <span data-ttu-id="5b07b-225">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span><span class="sxs-lookup"><span data-stu-id="5b07b-225">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="5b07b-226">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="5b07b-226">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5b07b-227">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="5b07b-227">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5b07b-228">click **Users and groups** in the navigation menu.</span><span class="sxs-lookup"><span data-stu-id="5b07b-228">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="5b07b-229">click **All users**.</span><span class="sxs-lookup"><span data-stu-id="5b07b-229">click **All users**.</span></span>

6.  <span data-ttu-id="5b07b-230">**Search** for the user you are interested in and **click the row** to select.</span><span class="sxs-lookup"><span data-stu-id="5b07b-230">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="5b07b-231">click **Licenses** to see which licenses the user currently has assigned.</span><span class="sxs-lookup"><span data-stu-id="5b07b-231">click **Licenses** to see which licenses the user currently has assigned.</span></span>

8.  <span data-ttu-id="5b07b-232">click the **Assign** button.</span><span class="sxs-lookup"><span data-stu-id="5b07b-232">click the **Assign** button.</span></span>

9.  <span data-ttu-id="5b07b-233">Select **one or more products** from the list of available products.</span><span class="sxs-lookup"><span data-stu-id="5b07b-233">Select **one or more products** from the list of available products.</span></span>

10. <span data-ttu-id="5b07b-234">**Optional** click the **assignment options** item to granularly assign products.</span><span class="sxs-lookup"><span data-stu-id="5b07b-234">**Optional** click the **assignment options** item to granularly assign products.</span></span> <span data-ttu-id="5b07b-235">Click **Ok** when this is completed.</span><span class="sxs-lookup"><span data-stu-id="5b07b-235">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="5b07b-236">Click the **Assign** button to assign these licenses to this user.</span><span class="sxs-lookup"><span data-stu-id="5b07b-236">Click the **Assign** button to assign these licenses to this user.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-resolve-the-issue"></a><span data-ttu-id="5b07b-237">If these troubleshooting steps do not resolve the issue</span><span class="sxs-lookup"><span data-stu-id="5b07b-237">If these troubleshooting steps do not resolve the issue</span></span>

<span data-ttu-id="5b07b-238">open a support ticket with the following information if available:</span><span class="sxs-lookup"><span data-stu-id="5b07b-238">open a support ticket with the following information if available:</span></span>

-   <span data-ttu-id="5b07b-239">Correlation error ID</span><span class="sxs-lookup"><span data-stu-id="5b07b-239">Correlation error ID</span></span>

-   <span data-ttu-id="5b07b-240">UPN (user email address)</span><span class="sxs-lookup"><span data-stu-id="5b07b-240">UPN (user email address)</span></span>

-   <span data-ttu-id="5b07b-241">Tenant ID</span><span class="sxs-lookup"><span data-stu-id="5b07b-241">Tenant ID</span></span>

-   <span data-ttu-id="5b07b-242">Browser type</span><span class="sxs-lookup"><span data-stu-id="5b07b-242">Browser type</span></span>

-   <span data-ttu-id="5b07b-243">Time zone and time/timeframe during error occurs</span><span class="sxs-lookup"><span data-stu-id="5b07b-243">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="5b07b-244">Fiddler traces</span><span class="sxs-lookup"><span data-stu-id="5b07b-244">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="5b07b-245">Next steps</span><span class="sxs-lookup"><span data-stu-id="5b07b-245">Next steps</span></span>
[<span data-ttu-id="5b07b-246">Provide single sign-on to your apps with Application Proxy</span><span class="sxs-lookup"><span data-stu-id="5b07b-246">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
