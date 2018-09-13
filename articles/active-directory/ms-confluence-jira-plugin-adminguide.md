---
title: Admin guide for the Azure Active Directory SSO plug-in | Microsoft Docs
description: Learn how to configure single sign-on between Azure Active Directory and Jira/Confluence.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 4b663047-7f88-443b-97bd-54224b232815
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/30/2018
ms.author: jeedes
ms.openlocfilehash: 7cbe0d0ea3bbbd60b7cd2dc88ef249c4380083a7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967428"
---
# <a name="admin-guide-for-the-azure-active-directory-sso-plug-in"></a><span data-ttu-id="503a5-103">Admin guide for the Azure Active Directory SSO plug-in</span><span class="sxs-lookup"><span data-stu-id="503a5-103">Admin guide for the Azure Active Directory SSO plug-in</span></span>

## <a name="overview"></a><span data-ttu-id="503a5-104">Overview</span><span class="sxs-lookup"><span data-stu-id="503a5-104">Overview</span></span>

<span data-ttu-id="503a5-105">The Azure Active Directory (Azure AD) single sign-on (SSO) plug-in enables Microsoft Azure AD customers to use their work or school account for signing in to Atlassian Jira and Confluence Server-based products.</span><span class="sxs-lookup"><span data-stu-id="503a5-105">The Azure Active Directory (Azure AD) single sign-on (SSO) plug-in enables Microsoft Azure AD customers to use their work or school account for signing in to Atlassian Jira and Confluence Server-based products.</span></span> <span data-ttu-id="503a5-106">It implements SAML 2.0-based SSO.</span><span class="sxs-lookup"><span data-stu-id="503a5-106">It implements SAML 2.0-based SSO.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="503a5-107">How it works</span><span class="sxs-lookup"><span data-stu-id="503a5-107">How it works</span></span>

<span data-ttu-id="503a5-108">When users want to sign in to the Atlassian Jira or Confluence application, they see the **Login with Azure AD** button on the sign-in page.</span><span class="sxs-lookup"><span data-stu-id="503a5-108">When users want to sign in to the Atlassian Jira or Confluence application, they see the **Login with Azure AD** button on the sign-in page.</span></span> <span data-ttu-id="503a5-109">When they select it, they're required to sign in by using the Azure AD organization sign-in page (that is, their work or school account).</span><span class="sxs-lookup"><span data-stu-id="503a5-109">When they select it, they're required to sign in by using the Azure AD organization sign-in page (that is, their work or school account).</span></span>

<span data-ttu-id="503a5-110">After the users are authenticated, they should be able to sign in to the application.</span><span class="sxs-lookup"><span data-stu-id="503a5-110">After the users are authenticated, they should be able to sign in to the application.</span></span> <span data-ttu-id="503a5-111">If they are already authenticated with the ID and password for their work or school account, then they directly sign in to the application.</span><span class="sxs-lookup"><span data-stu-id="503a5-111">If they are already authenticated with the ID and password for their work or school account, then they directly sign in to the application.</span></span> 

<span data-ttu-id="503a5-112">Sign-in works across Jira and Confluence.</span><span class="sxs-lookup"><span data-stu-id="503a5-112">Sign-in works across Jira and Confluence.</span></span> <span data-ttu-id="503a5-113">If users are signed in to the Jira application and Confluence is opened in the same browser window, they don't have to provide the credentials for the other app.</span><span class="sxs-lookup"><span data-stu-id="503a5-113">If users are signed in to the Jira application and Confluence is opened in the same browser window, they don't have to provide the credentials for the other app.</span></span> 

<span data-ttu-id="503a5-114">Users can also get to the Atlassian product through My Apps under the work or school account.</span><span class="sxs-lookup"><span data-stu-id="503a5-114">Users can also get to the Atlassian product through My Apps under the work or school account.</span></span> <span data-ttu-id="503a5-115">They should be signed in without being asked for credentials.</span><span class="sxs-lookup"><span data-stu-id="503a5-115">They should be signed in without being asked for credentials.</span></span>

> [!NOTE]
> <span data-ttu-id="503a5-116">User provisioning is not done through the plug-in.</span><span class="sxs-lookup"><span data-stu-id="503a5-116">User provisioning is not done through the plug-in.</span></span>

## <a name="audience"></a><span data-ttu-id="503a5-117">Audience</span><span class="sxs-lookup"><span data-stu-id="503a5-117">Audience</span></span>

<span data-ttu-id="503a5-118">Jira and Confluence admins can use the plug-in to enable SSO by using Azure AD.</span><span class="sxs-lookup"><span data-stu-id="503a5-118">Jira and Confluence admins can use the plug-in to enable SSO by using Azure AD.</span></span>

## <a name="assumptions"></a><span data-ttu-id="503a5-119">Assumptions</span><span class="sxs-lookup"><span data-stu-id="503a5-119">Assumptions</span></span>

* <span data-ttu-id="503a5-120">Jira and Confluence instances are HTTPS enabled.</span><span class="sxs-lookup"><span data-stu-id="503a5-120">Jira and Confluence instances are HTTPS enabled.</span></span>
* <span data-ttu-id="503a5-121">Users are already created in Jira or Confluence.</span><span class="sxs-lookup"><span data-stu-id="503a5-121">Users are already created in Jira or Confluence.</span></span>
* <span data-ttu-id="503a5-122">Users have roles assigned in Jira or Confluence.</span><span class="sxs-lookup"><span data-stu-id="503a5-122">Users have roles assigned in Jira or Confluence.</span></span>
* <span data-ttu-id="503a5-123">Admins have access to information required to configure the plug-in.</span><span class="sxs-lookup"><span data-stu-id="503a5-123">Admins have access to information required to configure the plug-in.</span></span>
* <span data-ttu-id="503a5-124">Jira or Confluence is available outside the company network as well.</span><span class="sxs-lookup"><span data-stu-id="503a5-124">Jira or Confluence is available outside the company network as well.</span></span>
* <span data-ttu-id="503a5-125">The plug-in works with only the on-premises version of Jira and Confluence.</span><span class="sxs-lookup"><span data-stu-id="503a5-125">The plug-in works with only the on-premises version of Jira and Confluence.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="503a5-126">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="503a5-126">Prerequisites</span></span>

<span data-ttu-id="503a5-127">Note the following information before you install the plug-in:</span><span class="sxs-lookup"><span data-stu-id="503a5-127">Note the following information before you install the plug-in:</span></span>

* <span data-ttu-id="503a5-128">Jira and Confluence are installed on a Windows 64-bit version.</span><span class="sxs-lookup"><span data-stu-id="503a5-128">Jira and Confluence are installed on a Windows 64-bit version.</span></span>
* <span data-ttu-id="503a5-129">Jira and Confluence versions are HTTPS enabled.</span><span class="sxs-lookup"><span data-stu-id="503a5-129">Jira and Confluence versions are HTTPS enabled.</span></span>
* <span data-ttu-id="503a5-130">Jira and Confluence are available on the internet.</span><span class="sxs-lookup"><span data-stu-id="503a5-130">Jira and Confluence are available on the internet.</span></span>
* <span data-ttu-id="503a5-131">Admin credentials are in place for Jira and Confluence.</span><span class="sxs-lookup"><span data-stu-id="503a5-131">Admin credentials are in place for Jira and Confluence.</span></span>
* <span data-ttu-id="503a5-132">Admin credentials are in place for Azure AD.</span><span class="sxs-lookup"><span data-stu-id="503a5-132">Admin credentials are in place for Azure AD.</span></span>
* <span data-ttu-id="503a5-133">WebSudo is disabled in Jira and Confluence.</span><span class="sxs-lookup"><span data-stu-id="503a5-133">WebSudo is disabled in Jira and Confluence.</span></span>

## <a name="supported-versions-of-jira-and-confluence"></a><span data-ttu-id="503a5-134">Supported versions of Jira and Confluence</span><span class="sxs-lookup"><span data-stu-id="503a5-134">Supported versions of Jira and Confluence</span></span>

<span data-ttu-id="503a5-135">The plug-in supports the following versions of Jira and Confluence:</span><span class="sxs-lookup"><span data-stu-id="503a5-135">The plug-in supports the following versions of Jira and Confluence:</span></span>

* <span data-ttu-id="503a5-136">Jira Core and Software: 6.0 to 7.8</span><span class="sxs-lookup"><span data-stu-id="503a5-136">Jira Core and Software: 6.0 to 7.8</span></span>
* <span data-ttu-id="503a5-137">Jira Service Desk: 3.0 to 3.2</span><span class="sxs-lookup"><span data-stu-id="503a5-137">Jira Service Desk: 3.0 to 3.2</span></span>
* <span data-ttu-id="503a5-138">Confluence: 5.0 to 5.10</span><span class="sxs-lookup"><span data-stu-id="503a5-138">Confluence: 5.0 to 5.10</span></span>

## <a name="installation"></a><span data-ttu-id="503a5-139">Installation</span><span class="sxs-lookup"><span data-stu-id="503a5-139">Installation</span></span>

<span data-ttu-id="503a5-140">To install the plug-in, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="503a5-140">To install the plug-in, follow these steps:</span></span>

1. <span data-ttu-id="503a5-141">Sign in to your Jira or Confluence instance as an admin.</span><span class="sxs-lookup"><span data-stu-id="503a5-141">Sign in to your Jira or Confluence instance as an admin.</span></span>

2. <span data-ttu-id="503a5-142">Go to the Jira/Confluence administration console and select **Add-ons**.</span><span class="sxs-lookup"><span data-stu-id="503a5-142">Go to the Jira/Confluence administration console and select **Add-ons**.</span></span>

3. <span data-ttu-id="503a5-143">From the Atlassian Marketplace, search for **Microsoft SAML SSO Plugin**.</span><span class="sxs-lookup"><span data-stu-id="503a5-143">From the Atlassian Marketplace, search for **Microsoft SAML SSO Plugin**.</span></span>

   <span data-ttu-id="503a5-144">The appropriate version of the plug-in appears in the search results.</span><span class="sxs-lookup"><span data-stu-id="503a5-144">The appropriate version of the plug-in appears in the search results.</span></span>

4. <span data-ttu-id="503a5-145">Select the plug-in, and the Universal Plug-in Manager (UPM) installs it.</span><span class="sxs-lookup"><span data-stu-id="503a5-145">Select the plug-in, and the Universal Plug-in Manager (UPM) installs it.</span></span>

<span data-ttu-id="503a5-146">After the plug-in is installed, it appears in the **User Installed Add-ons** section of **Manage Add-ons**.</span><span class="sxs-lookup"><span data-stu-id="503a5-146">After the plug-in is installed, it appears in the **User Installed Add-ons** section of **Manage Add-ons**.</span></span>

## <a name="plug-in-configuration"></a><span data-ttu-id="503a5-147">Plug-in configuration</span><span class="sxs-lookup"><span data-stu-id="503a5-147">Plug-in configuration</span></span>

<span data-ttu-id="503a5-148">Before you start using the plug-in, you must configure it.</span><span class="sxs-lookup"><span data-stu-id="503a5-148">Before you start using the plug-in, you must configure it.</span></span> <span data-ttu-id="503a5-149">Select the plug-in, select the **Configure** button, and provide the configuration details.</span><span class="sxs-lookup"><span data-stu-id="503a5-149">Select the plug-in, select the **Configure** button, and provide the configuration details.</span></span>

<span data-ttu-id="503a5-150">The following image shows the configuration screen in both Jira and Confluence:</span><span class="sxs-lookup"><span data-stu-id="503a5-150">The following image shows the configuration screen in both Jira and Confluence:</span></span>

![Plug-in configuration screen](./media/ms-confluence-jira-plugin-adminguide/jira.png)

*   <span data-ttu-id="503a5-152">**Metadata URL**: The URL to get federation metadata from Azure AD.</span><span class="sxs-lookup"><span data-stu-id="503a5-152">**Metadata URL**: The URL to get federation metadata from Azure AD.</span></span>

*   <span data-ttu-id="503a5-153">**Identifiers**: The URL that Azure AD uses to validate the source of the request.</span><span class="sxs-lookup"><span data-stu-id="503a5-153">**Identifiers**: The URL that Azure AD uses to validate the source of the request.</span></span> <span data-ttu-id="503a5-154">It maps to the **Identifier** element in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="503a5-154">It maps to the **Identifier** element in Azure AD.</span></span> <span data-ttu-id="503a5-155">The plug-in automatically derives this URL as https://*<domain:port>*/.</span><span class="sxs-lookup"><span data-stu-id="503a5-155">The plug-in automatically derives this URL as https://*<domain:port>*/.</span></span>

*   <span data-ttu-id="503a5-156">**Reply URL**: The reply URL in your identity provider (IdP) that initiates the SAML sign-in.</span><span class="sxs-lookup"><span data-stu-id="503a5-156">**Reply URL**: The reply URL in your identity provider (IdP) that initiates the SAML sign-in.</span></span> <span data-ttu-id="503a5-157">It maps to the **Reply URL** element in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="503a5-157">It maps to the **Reply URL** element in Azure AD.</span></span> <span data-ttu-id="503a5-158">The plug-in automatically derives this URL as https://*<domain:port>*/plugins/servlet/saml/auth.</span><span class="sxs-lookup"><span data-stu-id="503a5-158">The plug-in automatically derives this URL as https://*<domain:port>*/plugins/servlet/saml/auth.</span></span>

*   <span data-ttu-id="503a5-159">**Sign On URL**: The sign-on URL in your IdP that initiates the SAML sign-in.</span><span class="sxs-lookup"><span data-stu-id="503a5-159">**Sign On URL**: The sign-on URL in your IdP that initiates the SAML sign-in.</span></span> <span data-ttu-id="503a5-160">It maps to the **Sign On** element in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="503a5-160">It maps to the **Sign On** element in Azure AD.</span></span> <span data-ttu-id="503a5-161">The plug-in automatically derives this URL as https://*<domain:port>*/plugins/servlet/saml/auth.</span><span class="sxs-lookup"><span data-stu-id="503a5-161">The plug-in automatically derives this URL as https://*<domain:port>*/plugins/servlet/saml/auth.</span></span>

*   <span data-ttu-id="503a5-162">**IdP Entity ID**: The entity ID that your IdP uses.</span><span class="sxs-lookup"><span data-stu-id="503a5-162">**IdP Entity ID**: The entity ID that your IdP uses.</span></span> <span data-ttu-id="503a5-163">This box is populated when the metadata URL is resolved.</span><span class="sxs-lookup"><span data-stu-id="503a5-163">This box is populated when the metadata URL is resolved.</span></span>

*   <span data-ttu-id="503a5-164">**Login URL**: The sign-in URL from your IdP.</span><span class="sxs-lookup"><span data-stu-id="503a5-164">**Login URL**: The sign-in URL from your IdP.</span></span> <span data-ttu-id="503a5-165">This box is populated from Azure AD when the metadata URL is resolved.</span><span class="sxs-lookup"><span data-stu-id="503a5-165">This box is populated from Azure AD when the metadata URL is resolved.</span></span>

*   <span data-ttu-id="503a5-166">**Logout URL**: The logout URL from your IdP.</span><span class="sxs-lookup"><span data-stu-id="503a5-166">**Logout URL**: The logout URL from your IdP.</span></span> <span data-ttu-id="503a5-167">This box is populated from Azure AD when the metadata URL is resolved.</span><span class="sxs-lookup"><span data-stu-id="503a5-167">This box is populated from Azure AD when the metadata URL is resolved.</span></span>

*   <span data-ttu-id="503a5-168">**X.509 Certificate**: Your IdP’s X.509 certificate.</span><span class="sxs-lookup"><span data-stu-id="503a5-168">**X.509 Certificate**: Your IdP’s X.509 certificate.</span></span> <span data-ttu-id="503a5-169">This box is populated from Azure AD when the metadata URL is resolved.</span><span class="sxs-lookup"><span data-stu-id="503a5-169">This box is populated from Azure AD when the metadata URL is resolved.</span></span>

*   <span data-ttu-id="503a5-170">**Login Button Name**: The name of the sign-in button that your organization wants users to see on the sign-in page.</span><span class="sxs-lookup"><span data-stu-id="503a5-170">**Login Button Name**: The name of the sign-in button that your organization wants users to see on the sign-in page.</span></span>

*   <span data-ttu-id="503a5-171">**SAML User ID Locations**: The location where the Jira or Confluence user ID is expected in the SAML response.</span><span class="sxs-lookup"><span data-stu-id="503a5-171">**SAML User ID Locations**: The location where the Jira or Confluence user ID is expected in the SAML response.</span></span> <span data-ttu-id="503a5-172">It can be in **NameID** or in a custom attribute name.</span><span class="sxs-lookup"><span data-stu-id="503a5-172">It can be in **NameID** or in a custom attribute name.</span></span>

*   <span data-ttu-id="503a5-173">**Attribute Name**: The name of the attribute where the user ID is expected.</span><span class="sxs-lookup"><span data-stu-id="503a5-173">**Attribute Name**: The name of the attribute where the user ID is expected.</span></span>

*   <span data-ttu-id="503a5-174">**Enable Home Realm Discovery**: The selection to make if the company is using Active Directory Federation Services (AD FS)-based sign-in.</span><span class="sxs-lookup"><span data-stu-id="503a5-174">**Enable Home Realm Discovery**: The selection to make if the company is using Active Directory Federation Services (AD FS)-based sign-in.</span></span>

*   <span data-ttu-id="503a5-175">**Domain Name**: The domain name if sign-in is AD FS based.</span><span class="sxs-lookup"><span data-stu-id="503a5-175">**Domain Name**: The domain name if sign-in is AD FS based.</span></span>

*   <span data-ttu-id="503a5-176">**Enable Single Signout**: The selection to make if you want to sign out from Azure AD when a user signs out from Jira or Confluence.</span><span class="sxs-lookup"><span data-stu-id="503a5-176">**Enable Single Signout**: The selection to make if you want to sign out from Azure AD when a user signs out from Jira or Confluence.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="503a5-177">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="503a5-177">Troubleshooting</span></span>

* <span data-ttu-id="503a5-178">**You're getting multiple certificate errors**: Sign in to Azure AD and remove the multiple certificates that are available against the app.</span><span class="sxs-lookup"><span data-stu-id="503a5-178">**You're getting multiple certificate errors**: Sign in to Azure AD and remove the multiple certificates that are available against the app.</span></span> <span data-ttu-id="503a5-179">Ensure that only one certificate is present.</span><span class="sxs-lookup"><span data-stu-id="503a5-179">Ensure that only one certificate is present.</span></span>

* <span data-ttu-id="503a5-180">**A certificate is about to expire in Azure AD**: Add-ons take care of automatic rollover of the certificate.</span><span class="sxs-lookup"><span data-stu-id="503a5-180">**A certificate is about to expire in Azure AD**: Add-ons take care of automatic rollover of the certificate.</span></span> <span data-ttu-id="503a5-181">When a certificate is about to expire, a new certificate should be marked active and unused certificates should be deleted.</span><span class="sxs-lookup"><span data-stu-id="503a5-181">When a certificate is about to expire, a new certificate should be marked active and unused certificates should be deleted.</span></span> <span data-ttu-id="503a5-182">When a user tries to sign in to Jira in this scenario, the plug-in fetches and saves the new certificate.</span><span class="sxs-lookup"><span data-stu-id="503a5-182">When a user tries to sign in to Jira in this scenario, the plug-in fetches and saves the new certificate.</span></span>

* <span data-ttu-id="503a5-183">**You want to disable WebSudo (disable the secure administrator session)**:</span><span class="sxs-lookup"><span data-stu-id="503a5-183">**You want to disable WebSudo (disable the secure administrator session)**:</span></span>

  * <span data-ttu-id="503a5-184">For Jira, secure administrator sessions (that is, password confirmation before accessing administration functions) are enabled by default.</span><span class="sxs-lookup"><span data-stu-id="503a5-184">For Jira, secure administrator sessions (that is, password confirmation before accessing administration functions) are enabled by default.</span></span> <span data-ttu-id="503a5-185">If you want to remove this ability in your Jira instance, specify the following line in your jira-config.properties file: `ira.websudo.is.disabled = true`</span><span class="sxs-lookup"><span data-stu-id="503a5-185">If you want to remove this ability in your Jira instance, specify the following line in your jira-config.properties file: `ira.websudo.is.disabled = true`</span></span>

  * <span data-ttu-id="503a5-186">For Confluence, follow the steps on the [Confluence support site](https://confluence.atlassian.com/doc/configuring-secure-administrator-sessions-218269595.html).</span><span class="sxs-lookup"><span data-stu-id="503a5-186">For Confluence, follow the steps on the [Confluence support site](https://confluence.atlassian.com/doc/configuring-secure-administrator-sessions-218269595.html).</span></span>

* <span data-ttu-id="503a5-187">**Fields that are supposed to be populated by the metadata URL are not getting populated**:</span><span class="sxs-lookup"><span data-stu-id="503a5-187">**Fields that are supposed to be populated by the metadata URL are not getting populated**:</span></span>

  * <span data-ttu-id="503a5-188">Check if the URL is correct.</span><span class="sxs-lookup"><span data-stu-id="503a5-188">Check if the URL is correct.</span></span> <span data-ttu-id="503a5-189">Check if you have mapped the correct tenant and app ID.</span><span class="sxs-lookup"><span data-stu-id="503a5-189">Check if you have mapped the correct tenant and app ID.</span></span>

  * <span data-ttu-id="503a5-190">Enter the URL in a browser and see if you receive the federation metadata XML.</span><span class="sxs-lookup"><span data-stu-id="503a5-190">Enter the URL in a browser and see if you receive the federation metadata XML.</span></span>

* <span data-ttu-id="503a5-191">**There's an internal server error**: Review the logs in the log directory of the installation.</span><span class="sxs-lookup"><span data-stu-id="503a5-191">**There's an internal server error**: Review the logs in the log directory of the installation.</span></span> <span data-ttu-id="503a5-192">If you're getting the error when the user is trying to sign in by using Azure AD SSO, you can share the logs with the support team.</span><span class="sxs-lookup"><span data-stu-id="503a5-192">If you're getting the error when the user is trying to sign in by using Azure AD SSO, you can share the logs with the support team.</span></span>

* <span data-ttu-id="503a5-193">**There's a "User ID not found" error when the user tries to sign in**: Create the user ID in Jira or Confluence.</span><span class="sxs-lookup"><span data-stu-id="503a5-193">**There's a "User ID not found" error when the user tries to sign in**: Create the user ID in Jira or Confluence.</span></span>

* <span data-ttu-id="503a5-194">**There's an "App not found" error in Azure AD**: See if the appropriate URL is mapped to the app in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="503a5-194">**There's an "App not found" error in Azure AD**: See if the appropriate URL is mapped to the app in Azure AD.</span></span>

* <span data-ttu-id="503a5-195">**You need support**: Reach out to the [Azure AD SSO Integration Team](<mailto:SaaSApplicationIntegrations@service.microsoft.com>).</span><span class="sxs-lookup"><span data-stu-id="503a5-195">**You need support**: Reach out to the [Azure AD SSO Integration Team](<mailto:SaaSApplicationIntegrations@service.microsoft.com>).</span></span> <span data-ttu-id="503a5-196">The team responds in 24-48 business hours.</span><span class="sxs-lookup"><span data-stu-id="503a5-196">The team responds in 24-48 business hours.</span></span>

  <span data-ttu-id="503a5-197">You can also raise a support ticket with Microsoft through the Azure portal channel.</span><span class="sxs-lookup"><span data-stu-id="503a5-197">You can also raise a support ticket with Microsoft through the Azure portal channel.</span></span>