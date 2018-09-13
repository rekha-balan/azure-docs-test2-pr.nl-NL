---
title: 'Azure AD Connect: Seamless Single Sign-On - quick start | Microsoft Docs'
description: This article describes how to get started with Azure Active Directory Seamless Single Sign-On
services: active-directory
keywords: what is Azure AD Connect, install Active Directory, required components for Azure AD, SSO, Single Sign-on
documentationcenter: ''
author: billmath
manager: mtillman
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/05/2018
ms.component: hybrid
ms.author: billmath
ms.openlocfilehash: 8cab491a874094ee195f12ba6fe7f19a87f09ef2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967852"
---
# <a name="azure-active-directory-seamless-single-sign-on-quick-start"></a><span data-ttu-id="6039e-104">Azure Active Directory Seamless Single Sign-On: Quick start</span><span class="sxs-lookup"><span data-stu-id="6039e-104">Azure Active Directory Seamless Single Sign-On: Quick start</span></span>

## <a name="deploy-seamless-single-sign-on"></a><span data-ttu-id="6039e-105">Deploy Seamless Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="6039e-105">Deploy Seamless Single Sign-On</span></span>

<span data-ttu-id="6039e-106">Azure Active Directory (Azure AD) Seamless Single Sign-On (Seamless SSO) automatically signs in users when they are on their corporate desktops that are connected to your corporate network.</span><span class="sxs-lookup"><span data-stu-id="6039e-106">Azure Active Directory (Azure AD) Seamless Single Sign-On (Seamless SSO) automatically signs in users when they are on their corporate desktops that are connected to your corporate network.</span></span> <span data-ttu-id="6039e-107">Seamless SSO provides your users with easy access to your cloud-based applications without needing any additional on-premises components.</span><span class="sxs-lookup"><span data-stu-id="6039e-107">Seamless SSO provides your users with easy access to your cloud-based applications without needing any additional on-premises components.</span></span>

<span data-ttu-id="6039e-108">To deploy Seamless SSO, follow these steps.</span><span class="sxs-lookup"><span data-stu-id="6039e-108">To deploy Seamless SSO, follow these steps.</span></span>

## <a name="step-1-check-the-prerequisites"></a><span data-ttu-id="6039e-109">Step 1: Check the prerequisites</span><span class="sxs-lookup"><span data-stu-id="6039e-109">Step 1: Check the prerequisites</span></span>

<span data-ttu-id="6039e-110">Ensure that the following prerequisites are in place:</span><span class="sxs-lookup"><span data-stu-id="6039e-110">Ensure that the following prerequisites are in place:</span></span>

* <span data-ttu-id="6039e-111">**Set up your Azure AD Connect server**: If you use [Pass-through Authentication](active-directory-aadconnect-pass-through-authentication.md) as your sign-in method, no additional prerequisite check is required.</span><span class="sxs-lookup"><span data-stu-id="6039e-111">**Set up your Azure AD Connect server**: If you use [Pass-through Authentication](active-directory-aadconnect-pass-through-authentication.md) as your sign-in method, no additional prerequisite check is required.</span></span> <span data-ttu-id="6039e-112">If you use [password hash synchronization](active-directory-aadconnectsync-implement-password-hash-synchronization.md) as your sign-in method, and if there is a firewall between Azure AD Connect and Azure AD, ensure that:</span><span class="sxs-lookup"><span data-stu-id="6039e-112">If you use [password hash synchronization](active-directory-aadconnectsync-implement-password-hash-synchronization.md) as your sign-in method, and if there is a firewall between Azure AD Connect and Azure AD, ensure that:</span></span>
   - <span data-ttu-id="6039e-113">You use version 1.1.644.0 or later of Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="6039e-113">You use version 1.1.644.0 or later of Azure AD Connect.</span></span> 
   - <span data-ttu-id="6039e-114">If your firewall or proxy allows DNS whitelisting, whitelist the connections to the **\*.msappproxy.net** URLs over port 443.</span><span class="sxs-lookup"><span data-stu-id="6039e-114">If your firewall or proxy allows DNS whitelisting, whitelist the connections to the **\*.msappproxy.net** URLs over port 443.</span></span> <span data-ttu-id="6039e-115">If not, allow access to the [Azure datacenter IP ranges](https://www.microsoft.com/download/details.aspx?id=41653), which are updated weekly.</span><span class="sxs-lookup"><span data-stu-id="6039e-115">If not, allow access to the [Azure datacenter IP ranges](https://www.microsoft.com/download/details.aspx?id=41653), which are updated weekly.</span></span> <span data-ttu-id="6039e-116">This prerequisite is applicable only when you enable the feature.</span><span class="sxs-lookup"><span data-stu-id="6039e-116">This prerequisite is applicable only when you enable the feature.</span></span> <span data-ttu-id="6039e-117">It is not required for actual user sign-ins.</span><span class="sxs-lookup"><span data-stu-id="6039e-117">It is not required for actual user sign-ins.</span></span>

    >[!NOTE]
    ><span data-ttu-id="6039e-118">Azure AD Connect versions 1.1.557.0, 1.1.558.0, 1.1.561.0, and 1.1.614.0 have a problem related to password hash synchronization.</span><span class="sxs-lookup"><span data-stu-id="6039e-118">Azure AD Connect versions 1.1.557.0, 1.1.558.0, 1.1.561.0, and 1.1.614.0 have a problem related to password hash synchronization.</span></span> <span data-ttu-id="6039e-119">If you _don't_ intend to use password hash synchronization in conjunction with Pass-through Authentication, read the [Azure AD Connect release notes](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-version-history#116470) to learn more.</span><span class="sxs-lookup"><span data-stu-id="6039e-119">If you _don't_ intend to use password hash synchronization in conjunction with Pass-through Authentication, read the [Azure AD Connect release notes](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-version-history#116470) to learn more.</span></span>

* <span data-ttu-id="6039e-120">**Use a supported Azure AD Connect topology**: Ensure that you are using one of Azure AD Connect's supported topologies described [here](active-directory-aadconnect-topologies.md).</span><span class="sxs-lookup"><span data-stu-id="6039e-120">**Use a supported Azure AD Connect topology**: Ensure that you are using one of Azure AD Connect's supported topologies described [here](active-directory-aadconnect-topologies.md).</span></span>

    >[!NOTE]
    ><span data-ttu-id="6039e-121">Seamless SSO supports multiple AD forests, whether there are AD trusts between them or not.</span><span class="sxs-lookup"><span data-stu-id="6039e-121">Seamless SSO supports multiple AD forests, whether there are AD trusts between them or not.</span></span>

* <span data-ttu-id="6039e-122">**Set up domain administrator credentials**: You need to have domain administrator credentials for each Active Directory forest that:</span><span class="sxs-lookup"><span data-stu-id="6039e-122">**Set up domain administrator credentials**: You need to have domain administrator credentials for each Active Directory forest that:</span></span>
    * <span data-ttu-id="6039e-123">You synchronize to Azure AD through Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="6039e-123">You synchronize to Azure AD through Azure AD Connect.</span></span>
    * <span data-ttu-id="6039e-124">Contains users you want to enable for Seamless SSO.</span><span class="sxs-lookup"><span data-stu-id="6039e-124">Contains users you want to enable for Seamless SSO.</span></span>
    
* <span data-ttu-id="6039e-125">**Enable modern authentication**: You need to enable [modern authentication](https://aka.ms/modernauthga) on your tenant for this feature to work.</span><span class="sxs-lookup"><span data-stu-id="6039e-125">**Enable modern authentication**: You need to enable [modern authentication](https://aka.ms/modernauthga) on your tenant for this feature to work.</span></span>

* <span data-ttu-id="6039e-126">**Use the latest versions of Office 365 clients**: To get a silent sign-on experience with Office 365 clients (Outlook, Word, Excel, and others), your users need to use versions 16.0.8730.xxxx or above.</span><span class="sxs-lookup"><span data-stu-id="6039e-126">**Use the latest versions of Office 365 clients**: To get a silent sign-on experience with Office 365 clients (Outlook, Word, Excel, and others), your users need to use versions 16.0.8730.xxxx or above.</span></span>

## <a name="step-2-enable-the-feature"></a><span data-ttu-id="6039e-127">Step 2: Enable the feature</span><span class="sxs-lookup"><span data-stu-id="6039e-127">Step 2: Enable the feature</span></span>

<span data-ttu-id="6039e-128">Enable Seamless SSO through [Azure AD Connect](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="6039e-128">Enable Seamless SSO through [Azure AD Connect](active-directory-aadconnect.md).</span></span>

<span data-ttu-id="6039e-129">If you're doing a fresh installation of Azure AD Connect, choose the [custom installation path](active-directory-aadconnect-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="6039e-129">If you're doing a fresh installation of Azure AD Connect, choose the [custom installation path](active-directory-aadconnect-get-started-custom.md).</span></span> <span data-ttu-id="6039e-130">At the **User sign-in** page, select the **Enable single sign on** option.</span><span class="sxs-lookup"><span data-stu-id="6039e-130">At the **User sign-in** page, select the **Enable single sign on** option.</span></span>

>[!NOTE]
> <span data-ttu-id="6039e-131">The option will be available for selection only if the Sign On method is **Password Hash Synchronization** or **Pass-through Authentication**.</span><span class="sxs-lookup"><span data-stu-id="6039e-131">The option will be available for selection only if the Sign On method is **Password Hash Synchronization** or **Pass-through Authentication**.</span></span>

![Azure AD Connect: User sign-in](./media/active-directory-aadconnect-sso/sso8.png)

<span data-ttu-id="6039e-133">If you already have an installation of Azure AD Connect, select the **Change user sign-in** page in Azure AD Connect, and then select **Next**.</span><span class="sxs-lookup"><span data-stu-id="6039e-133">If you already have an installation of Azure AD Connect, select the **Change user sign-in** page in Azure AD Connect, and then select **Next**.</span></span> <span data-ttu-id="6039e-134">If you are using Azure AD Connect versions 1.1.880.0 or above, the **Enable single sign on** option will be selected by default.</span><span class="sxs-lookup"><span data-stu-id="6039e-134">If you are using Azure AD Connect versions 1.1.880.0 or above, the **Enable single sign on** option will be selected by default.</span></span> <span data-ttu-id="6039e-135">If you are using older versions of Azure AD Connect, select the **Enable single sign on** option.</span><span class="sxs-lookup"><span data-stu-id="6039e-135">If you are using older versions of Azure AD Connect, select the **Enable single sign on** option.</span></span>

![Azure AD Connect: Change the user sign-in](./media/active-directory-aadconnect-user-signin/changeusersignin.png)

<span data-ttu-id="6039e-137">Continue through the wizard until you get to the **Enable single sign on** page.</span><span class="sxs-lookup"><span data-stu-id="6039e-137">Continue through the wizard until you get to the **Enable single sign on** page.</span></span> <span data-ttu-id="6039e-138">Provide domain administrator credentials for each Active Directory forest that:</span><span class="sxs-lookup"><span data-stu-id="6039e-138">Provide domain administrator credentials for each Active Directory forest that:</span></span>
    * <span data-ttu-id="6039e-139">You synchronize to Azure AD through Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="6039e-139">You synchronize to Azure AD through Azure AD Connect.</span></span>
    * <span data-ttu-id="6039e-140">Contains users you want to enable for Seamless SSO.</span><span class="sxs-lookup"><span data-stu-id="6039e-140">Contains users you want to enable for Seamless SSO.</span></span>

<span data-ttu-id="6039e-141">After completion of the wizard, Seamless SSO is enabled on your tenant.</span><span class="sxs-lookup"><span data-stu-id="6039e-141">After completion of the wizard, Seamless SSO is enabled on your tenant.</span></span>

>[!NOTE]
> <span data-ttu-id="6039e-142">The domain administrator credentials are not stored in Azure AD Connect or in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6039e-142">The domain administrator credentials are not stored in Azure AD Connect or in Azure AD.</span></span> <span data-ttu-id="6039e-143">They're used only to enable the feature.</span><span class="sxs-lookup"><span data-stu-id="6039e-143">They're used only to enable the feature.</span></span>

<span data-ttu-id="6039e-144">Follow these instructions to verify that you have enabled Seamless SSO correctly:</span><span class="sxs-lookup"><span data-stu-id="6039e-144">Follow these instructions to verify that you have enabled Seamless SSO correctly:</span></span>

1. <span data-ttu-id="6039e-145">Sign in to the [Azure Active Directory administrative center](https://aad.portal.azure.com) with the global administrator credentials for your tenant.</span><span class="sxs-lookup"><span data-stu-id="6039e-145">Sign in to the [Azure Active Directory administrative center](https://aad.portal.azure.com) with the global administrator credentials for your tenant.</span></span>
2. <span data-ttu-id="6039e-146">Select **Azure Active Directory** in the left pane.</span><span class="sxs-lookup"><span data-stu-id="6039e-146">Select **Azure Active Directory** in the left pane.</span></span>
3. <span data-ttu-id="6039e-147">Select **Azure AD Connect**.</span><span class="sxs-lookup"><span data-stu-id="6039e-147">Select **Azure AD Connect**.</span></span>
4. <span data-ttu-id="6039e-148">Verify that the **Seamless single sign-on** feature appears as **Enabled**.</span><span class="sxs-lookup"><span data-stu-id="6039e-148">Verify that the **Seamless single sign-on** feature appears as **Enabled**.</span></span>

![Azure portal: Azure AD Connect pane](./media/active-directory-aadconnect-sso/sso10.png)

>[!IMPORTANT]
> <span data-ttu-id="6039e-150">Seamless SSO creates a computer account named `AZUREADSSOACC` (which represents Azure AD) in your on-premises Active Directory (AD) in each AD forest.</span><span class="sxs-lookup"><span data-stu-id="6039e-150">Seamless SSO creates a computer account named `AZUREADSSOACC` (which represents Azure AD) in your on-premises Active Directory (AD) in each AD forest.</span></span> <span data-ttu-id="6039e-151">This computer account is needed for the feature to work.</span><span class="sxs-lookup"><span data-stu-id="6039e-151">This computer account is needed for the feature to work.</span></span> <span data-ttu-id="6039e-152">Move the `AZUREADSSOACC` computer account to an Organization Unit (OU) where other computer accounts are stored to ensure that it is managed in the same way and is not deleted.</span><span class="sxs-lookup"><span data-stu-id="6039e-152">Move the `AZUREADSSOACC` computer account to an Organization Unit (OU) where other computer accounts are stored to ensure that it is managed in the same way and is not deleted.</span></span>

## <a name="step-3-roll-out-the-feature"></a><span data-ttu-id="6039e-153">Step 3: Roll out the feature</span><span class="sxs-lookup"><span data-stu-id="6039e-153">Step 3: Roll out the feature</span></span>

<span data-ttu-id="6039e-154">You can gradually roll out Seamless SSO to your users using the instructions provided below.</span><span class="sxs-lookup"><span data-stu-id="6039e-154">You can gradually roll out Seamless SSO to your users using the instructions provided below.</span></span> <span data-ttu-id="6039e-155">You start by adding the following Azure AD URL to all or selected users' Intranet zone settings by using Group Policy in Active Directory:</span><span class="sxs-lookup"><span data-stu-id="6039e-155">You start by adding the following Azure AD URL to all or selected users' Intranet zone settings by using Group Policy in Active Directory:</span></span>

- https://autologon.microsoftazuread-sso.com

<span data-ttu-id="6039e-156">In addition, you need to enable an Intranet zone policy setting called **Allow updates to status bar via script** through Group Policy.</span><span class="sxs-lookup"><span data-stu-id="6039e-156">In addition, you need to enable an Intranet zone policy setting called **Allow updates to status bar via script** through Group Policy.</span></span> 

>[!NOTE]
> <span data-ttu-id="6039e-157">The following instructions work only for Internet Explorer and Google Chrome on Windows (if it shares a set of trusted site URLs with Internet Explorer).</span><span class="sxs-lookup"><span data-stu-id="6039e-157">The following instructions work only for Internet Explorer and Google Chrome on Windows (if it shares a set of trusted site URLs with Internet Explorer).</span></span> <span data-ttu-id="6039e-158">Read the next section for instructions on how to set up Mozilla Firefox and Google Chrome on macOS.</span><span class="sxs-lookup"><span data-stu-id="6039e-158">Read the next section for instructions on how to set up Mozilla Firefox and Google Chrome on macOS.</span></span>

### <a name="why-do-you-need-to-modify-users-intranet-zone-settings"></a><span data-ttu-id="6039e-159">Why do you need to modify users' Intranet zone settings?</span><span class="sxs-lookup"><span data-stu-id="6039e-159">Why do you need to modify users' Intranet zone settings?</span></span>

<span data-ttu-id="6039e-160">By default, the browser automatically calculates the correct zone, either Internet or Intranet, from a specific URL.</span><span class="sxs-lookup"><span data-stu-id="6039e-160">By default, the browser automatically calculates the correct zone, either Internet or Intranet, from a specific URL.</span></span> <span data-ttu-id="6039e-161">For example, "http://contoso/" maps to the Intranet zone, whereas "http://intranet.contoso.com/" maps to the Internet zone (because the URL contains a period).</span><span class="sxs-lookup"><span data-stu-id="6039e-161">For example, "http://contoso/" maps to the Intranet zone, whereas "http://intranet.contoso.com/" maps to the Internet zone (because the URL contains a period).</span></span> <span data-ttu-id="6039e-162">Browsers will not send Kerberos tickets to a cloud endpoint, like the Azure AD URL, unless you explicitly add the URL to the browser's Intranet zone.</span><span class="sxs-lookup"><span data-stu-id="6039e-162">Browsers will not send Kerberos tickets to a cloud endpoint, like the Azure AD URL, unless you explicitly add the URL to the browser's Intranet zone.</span></span>

<span data-ttu-id="6039e-163">There are two ways to modify users' Intranet zone settings:</span><span class="sxs-lookup"><span data-stu-id="6039e-163">There are two ways to modify users' Intranet zone settings:</span></span>

| <span data-ttu-id="6039e-164">Option</span><span class="sxs-lookup"><span data-stu-id="6039e-164">Option</span></span> | <span data-ttu-id="6039e-165">Admin consideration</span><span class="sxs-lookup"><span data-stu-id="6039e-165">Admin consideration</span></span> | <span data-ttu-id="6039e-166">User experience</span><span class="sxs-lookup"><span data-stu-id="6039e-166">User experience</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6039e-167">Group policy</span><span class="sxs-lookup"><span data-stu-id="6039e-167">Group policy</span></span> | <span data-ttu-id="6039e-168">Admin locks down editing of Intranet zone settings</span><span class="sxs-lookup"><span data-stu-id="6039e-168">Admin locks down editing of Intranet zone settings</span></span> | <span data-ttu-id="6039e-169">Users cannot modify their own settings</span><span class="sxs-lookup"><span data-stu-id="6039e-169">Users cannot modify their own settings</span></span> |
| <span data-ttu-id="6039e-170">Group policy preference</span><span class="sxs-lookup"><span data-stu-id="6039e-170">Group policy preference</span></span> |  <span data-ttu-id="6039e-171">Admin allows editing on Intranet zone settings</span><span class="sxs-lookup"><span data-stu-id="6039e-171">Admin allows editing on Intranet zone settings</span></span> | <span data-ttu-id="6039e-172">Users can modify their own settings</span><span class="sxs-lookup"><span data-stu-id="6039e-172">Users can modify their own settings</span></span> |

### <a name="group-policy-option---detailed-steps"></a><span data-ttu-id="6039e-173">"Group policy" option - Detailed steps</span><span class="sxs-lookup"><span data-stu-id="6039e-173">"Group policy" option - Detailed steps</span></span>

1. <span data-ttu-id="6039e-174">Open the Group Policy Management Editor tool.</span><span class="sxs-lookup"><span data-stu-id="6039e-174">Open the Group Policy Management Editor tool.</span></span>
2. <span data-ttu-id="6039e-175">Edit the group policy that's applied to some or all your users.</span><span class="sxs-lookup"><span data-stu-id="6039e-175">Edit the group policy that's applied to some or all your users.</span></span> <span data-ttu-id="6039e-176">This example uses **Default Domain Policy**.</span><span class="sxs-lookup"><span data-stu-id="6039e-176">This example uses **Default Domain Policy**.</span></span>
3. <span data-ttu-id="6039e-177">Browse to **User Configuration** > **Administrative Templates** > **Windows Components** > **Internet Explorer** > **Internet Control Panel** > **Security Page**.</span><span class="sxs-lookup"><span data-stu-id="6039e-177">Browse to **User Configuration** > **Administrative Templates** > **Windows Components** > **Internet Explorer** > **Internet Control Panel** > **Security Page**.</span></span> <span data-ttu-id="6039e-178">Then select **Site to Zone Assignment List**.</span><span class="sxs-lookup"><span data-stu-id="6039e-178">Then select **Site to Zone Assignment List**.</span></span>
    <span data-ttu-id="6039e-179">![Single sign-on](./media/active-directory-aadconnect-sso/sso6.png)</span><span class="sxs-lookup"><span data-stu-id="6039e-179">![Single sign-on](./media/active-directory-aadconnect-sso/sso6.png)</span></span>
4. <span data-ttu-id="6039e-180">Enable the policy, and then enter the following values in the dialog box:</span><span class="sxs-lookup"><span data-stu-id="6039e-180">Enable the policy, and then enter the following values in the dialog box:</span></span>
   - <span data-ttu-id="6039e-181">**Value name**: The Azure AD URL where the Kerberos tickets are forwarded.</span><span class="sxs-lookup"><span data-stu-id="6039e-181">**Value name**: The Azure AD URL where the Kerberos tickets are forwarded.</span></span>
   - <span data-ttu-id="6039e-182">**Value** (Data): **1** indicates the Intranet zone.</span><span class="sxs-lookup"><span data-stu-id="6039e-182">**Value** (Data): **1** indicates the Intranet zone.</span></span>

    <span data-ttu-id="6039e-183">The result looks like this:</span><span class="sxs-lookup"><span data-stu-id="6039e-183">The result looks like this:</span></span>

    <span data-ttu-id="6039e-184">Value: https://autologon.microsoftazuread-sso.com</span><span class="sxs-lookup"><span data-stu-id="6039e-184">Value: https://autologon.microsoftazuread-sso.com</span></span>
  
    <span data-ttu-id="6039e-185">Data: 1</span><span class="sxs-lookup"><span data-stu-id="6039e-185">Data: 1</span></span>

   >[!NOTE]
   > <span data-ttu-id="6039e-186">If you want to disallow some users from using Seamless SSO (for instance, if these users sign in on shared kiosks), set the preceding values to **4**.</span><span class="sxs-lookup"><span data-stu-id="6039e-186">If you want to disallow some users from using Seamless SSO (for instance, if these users sign in on shared kiosks), set the preceding values to **4**.</span></span> <span data-ttu-id="6039e-187">This action adds the Azure AD URL to the Restricted zone, and fails Seamless SSO all the time.</span><span class="sxs-lookup"><span data-stu-id="6039e-187">This action adds the Azure AD URL to the Restricted zone, and fails Seamless SSO all the time.</span></span>
   >

5. <span data-ttu-id="6039e-188">Select **OK**, and then select **OK** again.</span><span class="sxs-lookup"><span data-stu-id="6039e-188">Select **OK**, and then select **OK** again.</span></span>

    ![Single sign-on](./media/active-directory-aadconnect-sso/sso7.png)

6. <span data-ttu-id="6039e-190">Browse to **User Configuration** > **Administrative Templates** > **Windows Components** > **Internet Explorer** > **Internet Control Panel** > **Security Page** > **Intranet Zone**.</span><span class="sxs-lookup"><span data-stu-id="6039e-190">Browse to **User Configuration** > **Administrative Templates** > **Windows Components** > **Internet Explorer** > **Internet Control Panel** > **Security Page** > **Intranet Zone**.</span></span> <span data-ttu-id="6039e-191">Then select **Allow updates to status bar via script**.</span><span class="sxs-lookup"><span data-stu-id="6039e-191">Then select **Allow updates to status bar via script**.</span></span>

    ![Single sign-on](./media/active-directory-aadconnect-sso/sso11.png)

7. <span data-ttu-id="6039e-193">Enable the policy setting, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="6039e-193">Enable the policy setting, and then select **OK**.</span></span>

    ![Single sign-on](./media/active-directory-aadconnect-sso/sso12.png)

### <a name="group-policy-preference-option---detailed-steps"></a><span data-ttu-id="6039e-195">"Group policy preference" option - Detailed steps</span><span class="sxs-lookup"><span data-stu-id="6039e-195">"Group policy preference" option - Detailed steps</span></span>

1. <span data-ttu-id="6039e-196">Open the Group Policy Management Editor tool.</span><span class="sxs-lookup"><span data-stu-id="6039e-196">Open the Group Policy Management Editor tool.</span></span>
2. <span data-ttu-id="6039e-197">Edit the group policy that's applied to some or all your users.</span><span class="sxs-lookup"><span data-stu-id="6039e-197">Edit the group policy that's applied to some or all your users.</span></span> <span data-ttu-id="6039e-198">This example uses **Default Domain Policy**.</span><span class="sxs-lookup"><span data-stu-id="6039e-198">This example uses **Default Domain Policy**.</span></span>
3. <span data-ttu-id="6039e-199">Browse to **User Configuration** > **Preferences** > **Windows Settings** > **Registry** > **New** > **Registry item**.</span><span class="sxs-lookup"><span data-stu-id="6039e-199">Browse to **User Configuration** > **Preferences** > **Windows Settings** > **Registry** > **New** > **Registry item**.</span></span>

    ![Single sign-on](./media/active-directory-aadconnect-sso/sso15.png)

4. <span data-ttu-id="6039e-201">Enter the following values in appropriate fields and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="6039e-201">Enter the following values in appropriate fields and click **OK**.</span></span>
   - <span data-ttu-id="6039e-202">**Key Path**: ***Software\Microsoft\Windows\CurrentVersion\Internet Settings\ZoneMap\Domains\microsoftazuread-sso.com\autologon***</span><span class="sxs-lookup"><span data-stu-id="6039e-202">**Key Path**: ***Software\Microsoft\Windows\CurrentVersion\Internet Settings\ZoneMap\Domains\microsoftazuread-sso.com\autologon***</span></span>
   - <span data-ttu-id="6039e-203">**Value name**: ***https***.</span><span class="sxs-lookup"><span data-stu-id="6039e-203">**Value name**: ***https***.</span></span>
   - <span data-ttu-id="6039e-204">**Value type**: ***REG_DWORD***.</span><span class="sxs-lookup"><span data-stu-id="6039e-204">**Value type**: ***REG_DWORD***.</span></span>
   - <span data-ttu-id="6039e-205">**Value data**: ***00000001***.</span><span class="sxs-lookup"><span data-stu-id="6039e-205">**Value data**: ***00000001***.</span></span>
 
    ![Single sign-on](./media/active-directory-aadconnect-sso/sso16.png)
 
    ![Single sign-on](./media/active-directory-aadconnect-sso/sso17.png)

6. <span data-ttu-id="6039e-208">Browse to **User Configuration** > **Administrative Templates** > **Windows Components** > **Internet Explorer** > **Internet Control Panel** > **Security Page** > **Intranet Zone**.</span><span class="sxs-lookup"><span data-stu-id="6039e-208">Browse to **User Configuration** > **Administrative Templates** > **Windows Components** > **Internet Explorer** > **Internet Control Panel** > **Security Page** > **Intranet Zone**.</span></span> <span data-ttu-id="6039e-209">Then select **Allow updates to status bar via script**.</span><span class="sxs-lookup"><span data-stu-id="6039e-209">Then select **Allow updates to status bar via script**.</span></span>

    ![Single sign-on](./media/active-directory-aadconnect-sso/sso11.png)

7. <span data-ttu-id="6039e-211">Enable the policy setting, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="6039e-211">Enable the policy setting, and then select **OK**.</span></span>

    ![Single sign-on](./media/active-directory-aadconnect-sso/sso12.png)

### <a name="browser-considerations"></a><span data-ttu-id="6039e-213">Browser considerations</span><span class="sxs-lookup"><span data-stu-id="6039e-213">Browser considerations</span></span>

#### <a name="mozilla-firefox-all-platforms"></a><span data-ttu-id="6039e-214">Mozilla Firefox (all platforms)</span><span class="sxs-lookup"><span data-stu-id="6039e-214">Mozilla Firefox (all platforms)</span></span>

<span data-ttu-id="6039e-215">Mozilla Firefox doesn't automatically use Kerberos authentication.</span><span class="sxs-lookup"><span data-stu-id="6039e-215">Mozilla Firefox doesn't automatically use Kerberos authentication.</span></span> <span data-ttu-id="6039e-216">Each user must manually add the Azure AD URL to their Firefox settings by using the following steps:</span><span class="sxs-lookup"><span data-stu-id="6039e-216">Each user must manually add the Azure AD URL to their Firefox settings by using the following steps:</span></span>
1. <span data-ttu-id="6039e-217">Run Firefox and enter `about:config` in the address bar.</span><span class="sxs-lookup"><span data-stu-id="6039e-217">Run Firefox and enter `about:config` in the address bar.</span></span> <span data-ttu-id="6039e-218">Dismiss any notifications that you see.</span><span class="sxs-lookup"><span data-stu-id="6039e-218">Dismiss any notifications that you see.</span></span>
2. <span data-ttu-id="6039e-219">Search for the **network.negotiate-auth.trusted-uris** preference.</span><span class="sxs-lookup"><span data-stu-id="6039e-219">Search for the **network.negotiate-auth.trusted-uris** preference.</span></span> <span data-ttu-id="6039e-220">This preference lists Firefox's trusted sites for Kerberos authentication.</span><span class="sxs-lookup"><span data-stu-id="6039e-220">This preference lists Firefox's trusted sites for Kerberos authentication.</span></span>
3. <span data-ttu-id="6039e-221">Right-click and select **Modify**.</span><span class="sxs-lookup"><span data-stu-id="6039e-221">Right-click and select **Modify**.</span></span>
4. <span data-ttu-id="6039e-222">Enter https://autologon.microsoftazuread-sso.com in the field.</span><span class="sxs-lookup"><span data-stu-id="6039e-222">Enter https://autologon.microsoftazuread-sso.com in the field.</span></span>
5. <span data-ttu-id="6039e-223">Select **OK** and then reopen the browser.</span><span class="sxs-lookup"><span data-stu-id="6039e-223">Select **OK** and then reopen the browser.</span></span>

#### <a name="safari-macos"></a><span data-ttu-id="6039e-224">Safari (macOS)</span><span class="sxs-lookup"><span data-stu-id="6039e-224">Safari (macOS)</span></span>

<span data-ttu-id="6039e-225">Ensure that the machine running the macOS is joined to AD.</span><span class="sxs-lookup"><span data-stu-id="6039e-225">Ensure that the machine running the macOS is joined to AD.</span></span> <span data-ttu-id="6039e-226">Instructions for AD-joining your macOS device is outside the scope of this article.</span><span class="sxs-lookup"><span data-stu-id="6039e-226">Instructions for AD-joining your macOS device is outside the scope of this article.</span></span>

#### <a name="google-chrome-all-platforms"></a><span data-ttu-id="6039e-227">Google Chrome (all platforms)</span><span class="sxs-lookup"><span data-stu-id="6039e-227">Google Chrome (all platforms)</span></span>

<span data-ttu-id="6039e-228">If you have overridden the [AuthNegotiateDelegateWhitelist](https://www.chromium.org/administrators/policy-list-3#AuthNegotiateDelegateWhitelist) or the [AuthServerWhitelist](https://www.chromium.org/administrators/policy-list-3#AuthServerWhitelist) policy settings in your environment, ensure that you add Azure AD's URL (https://autologon.microsoftazuread-sso.com) to them as well.</span><span class="sxs-lookup"><span data-stu-id="6039e-228">If you have overridden the [AuthNegotiateDelegateWhitelist](https://www.chromium.org/administrators/policy-list-3#AuthNegotiateDelegateWhitelist) or the [AuthServerWhitelist](https://www.chromium.org/administrators/policy-list-3#AuthServerWhitelist) policy settings in your environment, ensure that you add Azure AD's URL (https://autologon.microsoftazuread-sso.com) to them as well.</span></span>

#### <a name="google-chrome-macos-only"></a><span data-ttu-id="6039e-229">Google Chrome (macOS only)</span><span class="sxs-lookup"><span data-stu-id="6039e-229">Google Chrome (macOS only)</span></span>

<span data-ttu-id="6039e-230">For Google Chrome on Mac OS and other non-Windows platforms, refer to [The Chromium Project Policy List](https://dev.chromium.org/administrators/policy-list-3#AuthServerWhitelist) for information on how to whitelist the Azure AD URL for integrated authentication.</span><span class="sxs-lookup"><span data-stu-id="6039e-230">For Google Chrome on Mac OS and other non-Windows platforms, refer to [The Chromium Project Policy List](https://dev.chromium.org/administrators/policy-list-3#AuthServerWhitelist) for information on how to whitelist the Azure AD URL for integrated authentication.</span></span>

<span data-ttu-id="6039e-231">The use of third-party Active Directory Group Policy extensions to roll out the Azure AD URL to Firefox and Google Chrome on Mac users is outside the scope of this article.</span><span class="sxs-lookup"><span data-stu-id="6039e-231">The use of third-party Active Directory Group Policy extensions to roll out the Azure AD URL to Firefox and Google Chrome on Mac users is outside the scope of this article.</span></span>

#### <a name="known-browser-limitations"></a><span data-ttu-id="6039e-232">Known browser limitations</span><span class="sxs-lookup"><span data-stu-id="6039e-232">Known browser limitations</span></span>

<span data-ttu-id="6039e-233">Seamless SSO doesn't work in private browsing mode on Firefox and Edge browsers.</span><span class="sxs-lookup"><span data-stu-id="6039e-233">Seamless SSO doesn't work in private browsing mode on Firefox and Edge browsers.</span></span> <span data-ttu-id="6039e-234">It also doesn't work on Internet Explorer if the browser is running in Enhanced Protected mode.</span><span class="sxs-lookup"><span data-stu-id="6039e-234">It also doesn't work on Internet Explorer if the browser is running in Enhanced Protected mode.</span></span>

## <a name="step-4-test-the-feature"></a><span data-ttu-id="6039e-235">Step 4: Test the feature</span><span class="sxs-lookup"><span data-stu-id="6039e-235">Step 4: Test the feature</span></span>

<span data-ttu-id="6039e-236">To test the feature for a specific user, ensure that all the following conditions are in place:</span><span class="sxs-lookup"><span data-stu-id="6039e-236">To test the feature for a specific user, ensure that all the following conditions are in place:</span></span>
  - <span data-ttu-id="6039e-237">The user signs in on a corporate device.</span><span class="sxs-lookup"><span data-stu-id="6039e-237">The user signs in on a corporate device.</span></span>
  - <span data-ttu-id="6039e-238">The device is joined to your Active Directory domain.</span><span class="sxs-lookup"><span data-stu-id="6039e-238">The device is joined to your Active Directory domain.</span></span> <span data-ttu-id="6039e-239">The device _doesn't_ need to be [Azure AD Joined](../active-directory-azureadjoin-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6039e-239">The device _doesn't_ need to be [Azure AD Joined](../active-directory-azureadjoin-overview.md).</span></span>
  - <span data-ttu-id="6039e-240">The device has a direct connection to your domain controller (DC), either on the corporate wired or wireless network or via a remote access connection, such as a VPN connection.</span><span class="sxs-lookup"><span data-stu-id="6039e-240">The device has a direct connection to your domain controller (DC), either on the corporate wired or wireless network or via a remote access connection, such as a VPN connection.</span></span>
  - <span data-ttu-id="6039e-241">You have [rolled out the feature](##step-3-roll-out-the-feature) to this user through Group Policy.</span><span class="sxs-lookup"><span data-stu-id="6039e-241">You have [rolled out the feature](##step-3-roll-out-the-feature) to this user through Group Policy.</span></span>

<span data-ttu-id="6039e-242">To test the scenario where the user enters only the username, but not the password:</span><span class="sxs-lookup"><span data-stu-id="6039e-242">To test the scenario where the user enters only the username, but not the password:</span></span>
   - <span data-ttu-id="6039e-243">Sign in to https://myapps.microsoft.com/ in a new private browser session.</span><span class="sxs-lookup"><span data-stu-id="6039e-243">Sign in to https://myapps.microsoft.com/ in a new private browser session.</span></span>

<span data-ttu-id="6039e-244">To test the scenario where the user doesn't have to enter the username or the password, use one of these steps:</span><span class="sxs-lookup"><span data-stu-id="6039e-244">To test the scenario where the user doesn't have to enter the username or the password, use one of these steps:</span></span> 
   - <span data-ttu-id="6039e-245">Sign in to https://myapps.microsoft.com/contoso.onmicrosoft.com in a new private browser session.</span><span class="sxs-lookup"><span data-stu-id="6039e-245">Sign in to https://myapps.microsoft.com/contoso.onmicrosoft.com in a new private browser session.</span></span> <span data-ttu-id="6039e-246">Replace *contoso* with your tenant's name.</span><span class="sxs-lookup"><span data-stu-id="6039e-246">Replace *contoso* with your tenant's name.</span></span>
   - <span data-ttu-id="6039e-247">Sign in to https://myapps.microsoft.com/contoso.com in a new private browser session.</span><span class="sxs-lookup"><span data-stu-id="6039e-247">Sign in to https://myapps.microsoft.com/contoso.com in a new private browser session.</span></span> <span data-ttu-id="6039e-248">Replace *contoso.com* with a verified domain (not a federated domain) on your tenant.</span><span class="sxs-lookup"><span data-stu-id="6039e-248">Replace *contoso.com* with a verified domain (not a federated domain) on your tenant.</span></span>

## <a name="step-5-roll-over-keys"></a><span data-ttu-id="6039e-249">Step 5: Roll over keys</span><span class="sxs-lookup"><span data-stu-id="6039e-249">Step 5: Roll over keys</span></span>

<span data-ttu-id="6039e-250">In Step 2, Azure AD Connect creates computer accounts (representing Azure AD) in all the Active Directory forests on which you have enabled Seamless SSO.</span><span class="sxs-lookup"><span data-stu-id="6039e-250">In Step 2, Azure AD Connect creates computer accounts (representing Azure AD) in all the Active Directory forests on which you have enabled Seamless SSO.</span></span> <span data-ttu-id="6039e-251">To learn more, see [Azure Active Directory Seamless Single Sign-On: Technical deep dive](active-directory-aadconnect-sso-how-it-works.md).</span><span class="sxs-lookup"><span data-stu-id="6039e-251">To learn more, see [Azure Active Directory Seamless Single Sign-On: Technical deep dive](active-directory-aadconnect-sso-how-it-works.md).</span></span>

>[!IMPORTANT]
><span data-ttu-id="6039e-252">The Kerberos decryption key on a computer account, if leaked, can be used to generate Kerberos tickets for any user in its AD forest.</span><span class="sxs-lookup"><span data-stu-id="6039e-252">The Kerberos decryption key on a computer account, if leaked, can be used to generate Kerberos tickets for any user in its AD forest.</span></span> <span data-ttu-id="6039e-253">Malicious actors can then impersonate Azure AD sign-ins for compromised users.</span><span class="sxs-lookup"><span data-stu-id="6039e-253">Malicious actors can then impersonate Azure AD sign-ins for compromised users.</span></span> <span data-ttu-id="6039e-254">We highly recommend that you periodically roll over these Kerberos decryption keys - at least once every 30 days.</span><span class="sxs-lookup"><span data-stu-id="6039e-254">We highly recommend that you periodically roll over these Kerberos decryption keys - at least once every 30 days.</span></span>

<span data-ttu-id="6039e-255">For instructions on how to roll over keys, see [Azure Active Directory Seamless Single Sign-On: Frequently asked questions](active-directory-aadconnect-sso-faq.md#how-can-i-roll-over-the-kerberos-decryption-key-of-the-azureadssoacc-computer-account).</span><span class="sxs-lookup"><span data-stu-id="6039e-255">For instructions on how to roll over keys, see [Azure Active Directory Seamless Single Sign-On: Frequently asked questions](active-directory-aadconnect-sso-faq.md#how-can-i-roll-over-the-kerberos-decryption-key-of-the-azureadssoacc-computer-account).</span></span> <span data-ttu-id="6039e-256">We are working on a capability to introduce automated roll over of keys.</span><span class="sxs-lookup"><span data-stu-id="6039e-256">We are working on a capability to introduce automated roll over of keys.</span></span>

>[!IMPORTANT]
><span data-ttu-id="6039e-257">You don't need to do this step _immediately_ after you have enabled the feature.</span><span class="sxs-lookup"><span data-stu-id="6039e-257">You don't need to do this step _immediately_ after you have enabled the feature.</span></span> <span data-ttu-id="6039e-258">Roll over the Kerberos decryption keys at least once every 30 days.</span><span class="sxs-lookup"><span data-stu-id="6039e-258">Roll over the Kerberos decryption keys at least once every 30 days.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6039e-259">Next steps</span><span class="sxs-lookup"><span data-stu-id="6039e-259">Next steps</span></span>

- <span data-ttu-id="6039e-260">[Technical deep dive](active-directory-aadconnect-sso-how-it-works.md): Understand how the Seamless Single Sign-On feature works.</span><span class="sxs-lookup"><span data-stu-id="6039e-260">[Technical deep dive](active-directory-aadconnect-sso-how-it-works.md): Understand how the Seamless Single Sign-On feature works.</span></span>
- <span data-ttu-id="6039e-261">[Frequently asked questions](active-directory-aadconnect-sso-faq.md): Get answers to frequently asked questions about Seamless Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="6039e-261">[Frequently asked questions](active-directory-aadconnect-sso-faq.md): Get answers to frequently asked questions about Seamless Single Sign-On.</span></span>
- <span data-ttu-id="6039e-262">[Troubleshoot](active-directory-aadconnect-troubleshoot-sso.md): Learn how to resolve common problems with the Seamless Single Sign-On feature.</span><span class="sxs-lookup"><span data-stu-id="6039e-262">[Troubleshoot](active-directory-aadconnect-troubleshoot-sso.md): Learn how to resolve common problems with the Seamless Single Sign-On feature.</span></span>
- <span data-ttu-id="6039e-263">[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect): Use the Azure Active Directory Forum to file new feature requests.</span><span class="sxs-lookup"><span data-stu-id="6039e-263">[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect): Use the Azure Active Directory Forum to file new feature requests.</span></span>
