---
title: 'Azure AD Connect: Seamless Single Sign-On - How it works | Microsoft Docs'
description: This article describes how the Azure Active Directory Seamless Single Sign-On feature works.
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
ms.date: 07/19/2018
ms.component: hybrid
ms.author: billmath
ms.openlocfilehash: 6507158a63de508164fc74bcafe39785046a2c79
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871067"
---
# <a name="azure-active-directory-seamless-single-sign-on-technical-deep-dive"></a><span data-ttu-id="204dd-104">Azure Active Directory Seamless Single Sign-On: Technical deep dive</span><span class="sxs-lookup"><span data-stu-id="204dd-104">Azure Active Directory Seamless Single Sign-On: Technical deep dive</span></span>

<span data-ttu-id="204dd-105">This article gives you technical details into how the Azure Active Directory Seamless Single Sign-On (Seamless SSO) feature works.</span><span class="sxs-lookup"><span data-stu-id="204dd-105">This article gives you technical details into how the Azure Active Directory Seamless Single Sign-On (Seamless SSO) feature works.</span></span>

## <a name="how-does-seamless-sso-work"></a><span data-ttu-id="204dd-106">How does Seamless SSO work?</span><span class="sxs-lookup"><span data-stu-id="204dd-106">How does Seamless SSO work?</span></span>

<span data-ttu-id="204dd-107">This section has three parts to it:</span><span class="sxs-lookup"><span data-stu-id="204dd-107">This section has three parts to it:</span></span>
1. <span data-ttu-id="204dd-108">The setup of the Seamless SSO feature.</span><span class="sxs-lookup"><span data-stu-id="204dd-108">The setup of the Seamless SSO feature.</span></span>
2. <span data-ttu-id="204dd-109">How a single user sign-in transaction on a web browser works with Seamless SSO.</span><span class="sxs-lookup"><span data-stu-id="204dd-109">How a single user sign-in transaction on a web browser works with Seamless SSO.</span></span>
3. <span data-ttu-id="204dd-110">How a single user sign-in transaction on a native client works with Seamless SSO.</span><span class="sxs-lookup"><span data-stu-id="204dd-110">How a single user sign-in transaction on a native client works with Seamless SSO.</span></span>

### <a name="how-does-set-up-work"></a><span data-ttu-id="204dd-111">How does set up work?</span><span class="sxs-lookup"><span data-stu-id="204dd-111">How does set up work?</span></span>

<span data-ttu-id="204dd-112">Seamless SSO is enabled using Azure AD Connect as shown [here](active-directory-aadconnect-sso-quick-start.md).</span><span class="sxs-lookup"><span data-stu-id="204dd-112">Seamless SSO is enabled using Azure AD Connect as shown [here](active-directory-aadconnect-sso-quick-start.md).</span></span> <span data-ttu-id="204dd-113">While enabling the feature, the following steps occur:</span><span class="sxs-lookup"><span data-stu-id="204dd-113">While enabling the feature, the following steps occur:</span></span>
- <span data-ttu-id="204dd-114">A computer account named `AZUREADSSOACC` (which represents Azure AD) is created in your on-premises Active Directory (AD) in each AD forest.</span><span class="sxs-lookup"><span data-stu-id="204dd-114">A computer account named `AZUREADSSOACC` (which represents Azure AD) is created in your on-premises Active Directory (AD) in each AD forest.</span></span>
- <span data-ttu-id="204dd-115">The computer account's Kerberos decryption key is shared securely with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="204dd-115">The computer account's Kerberos decryption key is shared securely with Azure AD.</span></span> <span data-ttu-id="204dd-116">If there are multiple AD forests, each one will have its own Kerberos decryption key.</span><span class="sxs-lookup"><span data-stu-id="204dd-116">If there are multiple AD forests, each one will have its own Kerberos decryption key.</span></span>
- <span data-ttu-id="204dd-117">In addition, two Kerberos service principal names (SPNs) are created to represent two URLs that are used during Azure AD sign-in.</span><span class="sxs-lookup"><span data-stu-id="204dd-117">In addition, two Kerberos service principal names (SPNs) are created to represent two URLs that are used during Azure AD sign-in.</span></span>

>[!NOTE]
> <span data-ttu-id="204dd-118">The computer account and the Kerberos SPNs are created in each AD forest you synchronize to Azure AD (using Azure AD Connect) and for whose users you want Seamless SSO.</span><span class="sxs-lookup"><span data-stu-id="204dd-118">The computer account and the Kerberos SPNs are created in each AD forest you synchronize to Azure AD (using Azure AD Connect) and for whose users you want Seamless SSO.</span></span> <span data-ttu-id="204dd-119">Move the `AZUREADSSOACC` computer account to an Organization Unit (OU) where other computer accounts are stored to ensure that it is managed in the same way and is not deleted.</span><span class="sxs-lookup"><span data-stu-id="204dd-119">Move the `AZUREADSSOACC` computer account to an Organization Unit (OU) where other computer accounts are stored to ensure that it is managed in the same way and is not deleted.</span></span>

>[!IMPORTANT]
><span data-ttu-id="204dd-120">We highly recommend that you [roll over the Kerberos decryption key](active-directory-aadconnect-sso-faq.md#how-can-i-roll-over-the-kerberos-decryption-key-of-the-azureadssoacc-computer-account) of the `AZUREADSSOACC` computer account at least every 30 days.</span><span class="sxs-lookup"><span data-stu-id="204dd-120">We highly recommend that you [roll over the Kerberos decryption key](active-directory-aadconnect-sso-faq.md#how-can-i-roll-over-the-kerberos-decryption-key-of-the-azureadssoacc-computer-account) of the `AZUREADSSOACC` computer account at least every 30 days.</span></span>

<span data-ttu-id="204dd-121">Once the set-up is complete, Seamless SSO works the same way as any other sign-in that uses Integrated Windows Authentication (IWA).</span><span class="sxs-lookup"><span data-stu-id="204dd-121">Once the set-up is complete, Seamless SSO works the same way as any other sign-in that uses Integrated Windows Authentication (IWA).</span></span>

### <a name="how-does-sign-in-on-a-web-browser-with-seamless-sso-work"></a><span data-ttu-id="204dd-122">How does sign-in on a web browser with Seamless SSO work?</span><span class="sxs-lookup"><span data-stu-id="204dd-122">How does sign-in on a web browser with Seamless SSO work?</span></span>

<span data-ttu-id="204dd-123">The sign-in flow on a web browser is as follows:</span><span class="sxs-lookup"><span data-stu-id="204dd-123">The sign-in flow on a web browser is as follows:</span></span>

1. <span data-ttu-id="204dd-124">The user tries to access a web application (for example, the Outlook Web App - https://outlook.office365.com/owa/) from a domain-joined corporate device inside your corporate network.</span><span class="sxs-lookup"><span data-stu-id="204dd-124">The user tries to access a web application (for example, the Outlook Web App - https://outlook.office365.com/owa/) from a domain-joined corporate device inside your corporate network.</span></span>
2. <span data-ttu-id="204dd-125">If the user is not already signed in, the user is redirected to the Azure AD sign-in page.</span><span class="sxs-lookup"><span data-stu-id="204dd-125">If the user is not already signed in, the user is redirected to the Azure AD sign-in page.</span></span>
3. <span data-ttu-id="204dd-126">The user types in their user name into the Azure AD sign-in page.</span><span class="sxs-lookup"><span data-stu-id="204dd-126">The user types in their user name into the Azure AD sign-in page.</span></span>

  >[!NOTE]
  ><span data-ttu-id="204dd-127">For [certain applications](./active-directory-aadconnect-sso-faq.md#what-applications-take-advantage-of-domainhint-or-loginhint-parameter-capability-of-seamless-sso), steps 2 & 3 are skipped.</span><span class="sxs-lookup"><span data-stu-id="204dd-127">For [certain applications](./active-directory-aadconnect-sso-faq.md#what-applications-take-advantage-of-domainhint-or-loginhint-parameter-capability-of-seamless-sso), steps 2 & 3 are skipped.</span></span>

4. <span data-ttu-id="204dd-128">Using JavaScript in the background, Azure AD challenges the browser, via a 401 Unauthorized response, to provide a Kerberos ticket.</span><span class="sxs-lookup"><span data-stu-id="204dd-128">Using JavaScript in the background, Azure AD challenges the browser, via a 401 Unauthorized response, to provide a Kerberos ticket.</span></span>
5. <span data-ttu-id="204dd-129">The browser, in turn, requests a ticket from Active Directory for the `AZUREADSSOACC` computer account (which represents Azure AD).</span><span class="sxs-lookup"><span data-stu-id="204dd-129">The browser, in turn, requests a ticket from Active Directory for the `AZUREADSSOACC` computer account (which represents Azure AD).</span></span>
6. <span data-ttu-id="204dd-130">Active Directory locates the computer account and returns a Kerberos ticket to the browser encrypted with the computer account's secret.</span><span class="sxs-lookup"><span data-stu-id="204dd-130">Active Directory locates the computer account and returns a Kerberos ticket to the browser encrypted with the computer account's secret.</span></span>
7. <span data-ttu-id="204dd-131">The browser forwards the Kerberos ticket it acquired from Active Directory to Azure AD.</span><span class="sxs-lookup"><span data-stu-id="204dd-131">The browser forwards the Kerberos ticket it acquired from Active Directory to Azure AD.</span></span>
8. <span data-ttu-id="204dd-132">Azure AD decrypts the Kerberos ticket, which includes the identity of the user signed into the corporate device, using the previously shared key.</span><span class="sxs-lookup"><span data-stu-id="204dd-132">Azure AD decrypts the Kerberos ticket, which includes the identity of the user signed into the corporate device, using the previously shared key.</span></span>
9. <span data-ttu-id="204dd-133">After evaluation, Azure AD either returns a token back to the application or asks the user to perform additional proofs, such as Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="204dd-133">After evaluation, Azure AD either returns a token back to the application or asks the user to perform additional proofs, such as Multi-Factor Authentication.</span></span>
10. <span data-ttu-id="204dd-134">If the user sign-in is successful, the user is able to access the application.</span><span class="sxs-lookup"><span data-stu-id="204dd-134">If the user sign-in is successful, the user is able to access the application.</span></span>

<span data-ttu-id="204dd-135">The following diagram illustrates all the components and the steps involved.</span><span class="sxs-lookup"><span data-stu-id="204dd-135">The following diagram illustrates all the components and the steps involved.</span></span>

![Seamless Single Sign On - Web app flow](./media/active-directory-aadconnect-sso/sso2.png)

<span data-ttu-id="204dd-137">Seamless SSO is opportunistic, which means if it fails, the sign-in experience falls back to its regular behavior - i.e, the user needs to enter their password to sign in.</span><span class="sxs-lookup"><span data-stu-id="204dd-137">Seamless SSO is opportunistic, which means if it fails, the sign-in experience falls back to its regular behavior - i.e, the user needs to enter their password to sign in.</span></span>

### <a name="how-does-sign-in-on-a-native-client-with-seamless-sso-work"></a><span data-ttu-id="204dd-138">How does sign-in on a native client with Seamless SSO work?</span><span class="sxs-lookup"><span data-stu-id="204dd-138">How does sign-in on a native client with Seamless SSO work?</span></span>

<span data-ttu-id="204dd-139">The sign-in flow on a native client is as follows:</span><span class="sxs-lookup"><span data-stu-id="204dd-139">The sign-in flow on a native client is as follows:</span></span>

1. <span data-ttu-id="204dd-140">The user tries to access a native application (for example, the Outlook client) from a domain-joined corporate device inside your corporate network.</span><span class="sxs-lookup"><span data-stu-id="204dd-140">The user tries to access a native application (for example, the Outlook client) from a domain-joined corporate device inside your corporate network.</span></span>
2. <span data-ttu-id="204dd-141">If the user is not already signed in, the native application retrieves the username of the user from the device's Windows session.</span><span class="sxs-lookup"><span data-stu-id="204dd-141">If the user is not already signed in, the native application retrieves the username of the user from the device's Windows session.</span></span>
3. <span data-ttu-id="204dd-142">The app sends the username to Azure AD, and retrieves your tenant's WS-Trust MEX endpoint.</span><span class="sxs-lookup"><span data-stu-id="204dd-142">The app sends the username to Azure AD, and retrieves your tenant's WS-Trust MEX endpoint.</span></span>
4. <span data-ttu-id="204dd-143">The app then queries the WS-Trust MEX endpoint to see if integrated authentication endpoint is available.</span><span class="sxs-lookup"><span data-stu-id="204dd-143">The app then queries the WS-Trust MEX endpoint to see if integrated authentication endpoint is available.</span></span>
5. <span data-ttu-id="204dd-144">If step 4 succeeds, a Kerberos challenge is issued.</span><span class="sxs-lookup"><span data-stu-id="204dd-144">If step 4 succeeds, a Kerberos challenge is issued.</span></span>
6. <span data-ttu-id="204dd-145">If the app is able to retrieve the Kerberos ticket, it forwards it up to Azure AD's integrated authentication endpoint.</span><span class="sxs-lookup"><span data-stu-id="204dd-145">If the app is able to retrieve the Kerberos ticket, it forwards it up to Azure AD's integrated authentication endpoint.</span></span>
7. <span data-ttu-id="204dd-146">Azure AD decrypts the Kerberos ticket and validates it.</span><span class="sxs-lookup"><span data-stu-id="204dd-146">Azure AD decrypts the Kerberos ticket and validates it.</span></span>
8. <span data-ttu-id="204dd-147">Azure AD signs the user in, and issues a SAML token to the app.</span><span class="sxs-lookup"><span data-stu-id="204dd-147">Azure AD signs the user in, and issues a SAML token to the app.</span></span>
9. <span data-ttu-id="204dd-148">The app then submits the SAML token to Azure AD's OAuth2 token endpoint.</span><span class="sxs-lookup"><span data-stu-id="204dd-148">The app then submits the SAML token to Azure AD's OAuth2 token endpoint.</span></span>
10. <span data-ttu-id="204dd-149">Azure AD validates the SAML token, and issues to the app an access token and a refresh token for the specified resource, and an id token.</span><span class="sxs-lookup"><span data-stu-id="204dd-149">Azure AD validates the SAML token, and issues to the app an access token and a refresh token for the specified resource, and an id token.</span></span>
11. <span data-ttu-id="204dd-150">The user gets access to the app's resource.</span><span class="sxs-lookup"><span data-stu-id="204dd-150">The user gets access to the app's resource.</span></span>

<span data-ttu-id="204dd-151">The following diagram illustrates all the components and the steps involved.</span><span class="sxs-lookup"><span data-stu-id="204dd-151">The following diagram illustrates all the components and the steps involved.</span></span>

![Seamless Single Sign On - Native app flow](./media/active-directory-aadconnect-sso/sso14.png)

## <a name="next-steps"></a><span data-ttu-id="204dd-153">Next steps</span><span class="sxs-lookup"><span data-stu-id="204dd-153">Next steps</span></span>

- <span data-ttu-id="204dd-154">[**Quick Start**](active-directory-aadconnect-sso-quick-start.md) - Get up and running Azure AD Seamless SSO.</span><span class="sxs-lookup"><span data-stu-id="204dd-154">[**Quick Start**](active-directory-aadconnect-sso-quick-start.md) - Get up and running Azure AD Seamless SSO.</span></span>
- <span data-ttu-id="204dd-155">[**Frequently Asked Questions**](active-directory-aadconnect-sso-faq.md) - Answers to frequently asked questions.</span><span class="sxs-lookup"><span data-stu-id="204dd-155">[**Frequently Asked Questions**](active-directory-aadconnect-sso-faq.md) - Answers to frequently asked questions.</span></span>
- <span data-ttu-id="204dd-156">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-sso.md) - Learn how to resolve common issues with the feature.</span><span class="sxs-lookup"><span data-stu-id="204dd-156">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-sso.md) - Learn how to resolve common issues with the feature.</span></span>
- <span data-ttu-id="204dd-157">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span><span class="sxs-lookup"><span data-stu-id="204dd-157">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
