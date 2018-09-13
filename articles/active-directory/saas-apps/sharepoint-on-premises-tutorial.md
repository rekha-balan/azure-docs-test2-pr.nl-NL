---
title: 'Tutorial: Azure Active Directory integration with SharePoint on-premises | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and SharePoint on-premises.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 85b8d4d0-3f6a-4913-b9d3-8cc327d8280d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2018
ms.author: jeedes
ms.openlocfilehash: 25e78633e7f1bead1eaa575edc6983a59e9ffa2d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871007"
---
# <a name="tutorial-azure-active-directory-integration-with-sharepoint-on-premises"></a><span data-ttu-id="918da-103">Tutorial: Azure Active Directory integration with SharePoint on-premises</span><span class="sxs-lookup"><span data-stu-id="918da-103">Tutorial: Azure Active Directory integration with SharePoint on-premises</span></span>

<span data-ttu-id="918da-104">In this tutorial, you learn how to integrate SharePoint on-premises with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="918da-104">In this tutorial, you learn how to integrate SharePoint on-premises with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="918da-105">Integrating SharePoint on-premises with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="918da-105">Integrating SharePoint on-premises with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="918da-106">You can control in Azure AD who has access to SharePoint on-premises.</span><span class="sxs-lookup"><span data-stu-id="918da-106">You can control in Azure AD who has access to SharePoint on-premises.</span></span>
- <span data-ttu-id="918da-107">You can enable your users to automatically get signed-on to SharePoint on-premises (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="918da-107">You can enable your users to automatically get signed-on to SharePoint on-premises (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="918da-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="918da-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="918da-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="918da-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="918da-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="918da-110">Prerequisites</span></span>

<span data-ttu-id="918da-111">To configure Azure AD integration with SharePoint on-premises, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="918da-111">To configure Azure AD integration with SharePoint on-premises, you need the following items:</span></span>

- <span data-ttu-id="918da-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="918da-112">An Azure AD subscription</span></span>
- <span data-ttu-id="918da-113">A SharePoint on-premises single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="918da-113">A SharePoint on-premises single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="918da-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="918da-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="918da-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="918da-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="918da-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="918da-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="918da-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="918da-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="918da-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="918da-118">Scenario description</span></span>

<span data-ttu-id="918da-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="918da-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>
<span data-ttu-id="918da-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="918da-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="918da-121">Adding SharePoint on-premises from the gallery</span><span class="sxs-lookup"><span data-stu-id="918da-121">Adding SharePoint on-premises from the gallery</span></span>
2. <span data-ttu-id="918da-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="918da-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sharepoint-on-premises-from-the-gallery"></a><span data-ttu-id="918da-123">Adding SharePoint on-premises from the gallery</span><span class="sxs-lookup"><span data-stu-id="918da-123">Adding SharePoint on-premises from the gallery</span></span>

<span data-ttu-id="918da-124">To configure the integration of SharePoint on-premises into Azure AD, you need to add SharePoint on-premises from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="918da-124">To configure the integration of SharePoint on-premises into Azure AD, you need to add SharePoint on-premises from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="918da-125">**To add SharePoint on-premises from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="918da-125">**To add SharePoint on-premises from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="918da-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="918da-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span>

    ![The Azure Active Directory button][1]

2. <span data-ttu-id="918da-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="918da-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="918da-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="918da-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]

3. <span data-ttu-id="918da-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="918da-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

4. <span data-ttu-id="918da-133">In the search box, type **SharePoint on-premises**, select **SharePoint on-premises** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="918da-133">In the search box, type **SharePoint on-premises**, select **SharePoint on-premises** from result panel then click **Add** button to add the application.</span></span>

    ![SharePoint on-premises in the results list](./media\sharepoint-on-premises-tutorial/tutorial_sharepointonpremises_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="918da-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="918da-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="918da-136">In this section, you configure and test Azure AD single sign-on with SharePoint on-premises based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="918da-136">In this section, you configure and test Azure AD single sign-on with SharePoint on-premises based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="918da-137">For single sign-on to work, Azure AD needs to know what the counterpart user in SharePoint on-premises is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="918da-137">For single sign-on to work, Azure AD needs to know what the counterpart user in SharePoint on-premises is to a user in Azure AD.</span></span> <span data-ttu-id="918da-138">In other words, a link relationship between an Azure AD user and the related user in SharePoint on-premises needs to be established.</span><span class="sxs-lookup"><span data-stu-id="918da-138">In other words, a link relationship between an Azure AD user and the related user in SharePoint on-premises needs to be established.</span></span>

<span data-ttu-id="918da-139">To configure and test Azure AD single sign-on with SharePoint on-premises, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="918da-139">To configure and test Azure AD single sign-on with SharePoint on-premises, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="918da-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="918da-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="918da-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="918da-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="918da-142">**[Grant access to SharePoint on-premises test user](#grant-access-to-sharePoint-on-premises-test-user)** - to have a counterpart of Britta Simon in SharePoint on-premises that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="918da-142">**[Grant access to SharePoint on-premises test user](#grant-access-to-sharePoint-on-premises-test-user)** - to have a counterpart of Britta Simon in SharePoint on-premises that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="918da-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="918da-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="918da-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="918da-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="918da-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="918da-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="918da-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SharePoint on-premises application.</span><span class="sxs-lookup"><span data-stu-id="918da-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SharePoint on-premises application.</span></span>

<span data-ttu-id="918da-147">**To configure Azure AD single sign-on with SharePoint on-premises, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="918da-147">**To configure Azure AD single sign-on with SharePoint on-premises, perform the following steps:**</span></span>

1. <span data-ttu-id="918da-148">In the Azure portal, on the **SharePoint on-premises** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="918da-148">In the Azure portal, on the **SharePoint on-premises** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

2. <span data-ttu-id="918da-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="918da-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Single sign-on dialog box](./media\sharepoint-on-premises-tutorial/tutorial_sharepointonpremises_samlbase.png)

3. <span data-ttu-id="918da-152">On the **SharePoint on-premises Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="918da-152">On the **SharePoint on-premises Domain and URLs** section, perform the following steps:</span></span>

    ![SharePoint on-premises Domain and URLs single sign-on information](./media\sharepoint-on-premises-tutorial/tutorial_sharepointonpremises_url1.png)

    <span data-ttu-id="918da-154">a.</span><span class="sxs-lookup"><span data-stu-id="918da-154">a.</span></span> <span data-ttu-id="918da-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<YourSharePointServerURL>/_trust/default.aspx`</span><span class="sxs-lookup"><span data-stu-id="918da-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<YourSharePointServerURL>/_trust/default.aspx`</span></span>

    <span data-ttu-id="918da-156">b.</span><span class="sxs-lookup"><span data-stu-id="918da-156">b.</span></span> <span data-ttu-id="918da-157">In the **Identifier** textbox, type the URL: `urn:sharepoint:federation`</span><span class="sxs-lookup"><span data-stu-id="918da-157">In the **Identifier** textbox, type the URL: `urn:sharepoint:federation`</span></span>

    <span data-ttu-id="918da-158">c.</span><span class="sxs-lookup"><span data-stu-id="918da-158">c.</span></span> <span data-ttu-id="918da-159">In the **Reply URL** textbox, type a URL using the following pattern: `https://<YourSharePointServerURL>/_trust/default.aspx`</span><span class="sxs-lookup"><span data-stu-id="918da-159">In the **Reply URL** textbox, type a URL using the following pattern: `https://<YourSharePointServerURL>/_trust/default.aspx`</span></span>

4. <span data-ttu-id="918da-160">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="918da-160">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media\sharepoint-on-premises-tutorial/tutorial_sharepointonpremises_certificate.png)

    > [!Note]
    > <span data-ttu-id="918da-162">Please note down the file path to which you have downloaded the certificate file, as you need to use it later in the PowerShell script for configuration.</span><span class="sxs-lookup"><span data-stu-id="918da-162">Please note down the file path to which you have downloaded the certificate file, as you need to use it later in the PowerShell script for configuration.</span></span>

5. <span data-ttu-id="918da-163">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="918da-163">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media\sharepoint-on-premises-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="918da-165">On the **SharePoint on-premises Configuration** section, click **Configure SharePoint on-premises** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="918da-165">On the **SharePoint on-premises Configuration** section, click **Configure SharePoint on-premises** to open **Configure sign-on** window.</span></span> <span data-ttu-id="918da-166">Copy the **SAML Entity ID** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="918da-166">Copy the **SAML Entity ID** from the **Quick Reference section.**</span></span> <span data-ttu-id="918da-167">For **Single Sign-On Service URL**, use a value of the following pattern: `https://login.microsoftonline.com/_my_directory_id_/wsfed`</span><span class="sxs-lookup"><span data-stu-id="918da-167">For **Single Sign-On Service URL**, use a value of the following pattern: `https://login.microsoftonline.com/_my_directory_id_/wsfed`</span></span> 

    > [!Note]
    > <span data-ttu-id="918da-168">_my_directory_id_ is the tenant id of Azure Ad subcription.</span><span class="sxs-lookup"><span data-stu-id="918da-168">_my_directory_id_ is the tenant id of Azure Ad subcription.</span></span>

    ![SharePoint on-premises Configuration](./media\sharepoint-on-premises-tutorial/tutorial_sharepointonpremises_configure.png)

    > [!NOTE]
    > <span data-ttu-id="918da-170">Sharepoint On-Premises application uses SAML 1.1 token, so Azure AD expects WS Fed request from SharePoint server and after authentication, it issues the SAML 1.1.</span><span class="sxs-lookup"><span data-stu-id="918da-170">Sharepoint On-Premises application uses SAML 1.1 token, so Azure AD expects WS Fed request from SharePoint server and after authentication, it issues the SAML 1.1.</span></span> <span data-ttu-id="918da-171">token.</span><span class="sxs-lookup"><span data-stu-id="918da-171">token.</span></span>

7. <span data-ttu-id="918da-172">In a different web browser window, log in to your SharePoint on-premises company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="918da-172">In a different web browser window, log in to your SharePoint on-premises company site as an administrator.</span></span>

8. <span data-ttu-id="918da-173">**Configure a new trusted identity provider in SharePoint Server 2016**</span><span class="sxs-lookup"><span data-stu-id="918da-173">**Configure a new trusted identity provider in SharePoint Server 2016**</span></span>

    <span data-ttu-id="918da-174">Sign into the SharePoint Server 2016 server and open the SharePoint 2016 Management Shell.</span><span class="sxs-lookup"><span data-stu-id="918da-174">Sign into the SharePoint Server 2016 server and open the SharePoint 2016 Management Shell.</span></span> <span data-ttu-id="918da-175">Fill in the values of $realm (Identifier value from the SharePoint on-premises Domain and URLs section in the Azure portal), $wsfedurl (Single Sign-On Service URL), and $filepath (file path to which you have downloaded the certificate file) from Azure portal and run the following commands to configure a new trusted identity provider.</span><span class="sxs-lookup"><span data-stu-id="918da-175">Fill in the values of $realm (Identifier value from the SharePoint on-premises Domain and URLs section in the Azure portal), $wsfedurl (Single Sign-On Service URL), and $filepath (file path to which you have downloaded the certificate file) from Azure portal and run the following commands to configure a new trusted identity provider.</span></span>

    > [!TIP]
    > <span data-ttu-id="918da-176">If you're new to using PowerShell or want to learn more about how PowerShell works, see [SharePoint PowerShell](https://docs.microsoft.com/en-us/powershell/sharepoint/overview?view=sharepoint-ps).</span><span class="sxs-lookup"><span data-stu-id="918da-176">If you're new to using PowerShell or want to learn more about how PowerShell works, see [SharePoint PowerShell](https://docs.microsoft.com/en-us/powershell/sharepoint/overview?view=sharepoint-ps).</span></span> 

    ```
    $realm = "<Identifier value from the SharePoint on-premises Domain and URLs section in the Azure portal>"
    $wsfedurl="<SAML single sign-on service URL value which you have copied from the Azure portal>"
    $filepath="<Full path to SAML signing certificate file which you have downloaded from the Azure portal>"
    $cert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2($filepath)
    New-SPTrustedRootAuthority -Name "AzureAD" -Certificate $cert
    $map = New-SPClaimTypeMapping -IncomingClaimType "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name" -IncomingClaimTypeDisplayName "name" -LocalClaimType "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn"
    $map2 = New-SPClaimTypeMapping -IncomingClaimType "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname" -IncomingClaimTypeDisplayName "GivenName" -SameAsIncoming
    $map3 = New-SPClaimTypeMapping -IncomingClaimType "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname" -IncomingClaimTypeDisplayName "SurName" -SameAsIncoming
    $map4 = New-SPClaimTypeMapping -IncomingClaimType "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress" -IncomingClaimTypeDisplayName "Email" -SameAsIncoming
    $ap = New-SPTrustedIdentityTokenIssuer -Name "AzureAD" -Description "SharePoint secured by Azure AD" -realm $realm -ImportTrustCertificate $cert -ClaimsMappings $map,$map2,$map3 -SignInUrl $wsfedurl -IdentifierClaim "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name"
    ```

    <span data-ttu-id="918da-177">Next, follow these steps to enable the trusted identity provider for your application:</span><span class="sxs-lookup"><span data-stu-id="918da-177">Next, follow these steps to enable the trusted identity provider for your application:</span></span>

    <span data-ttu-id="918da-178">a.</span><span class="sxs-lookup"><span data-stu-id="918da-178">a.</span></span> <span data-ttu-id="918da-179">In Central Administration, navigate to **Manage Web Application** and select the web application that you wish to secure with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="918da-179">In Central Administration, navigate to **Manage Web Application** and select the web application that you wish to secure with Azure AD.</span></span>

    <span data-ttu-id="918da-180">b.</span><span class="sxs-lookup"><span data-stu-id="918da-180">b.</span></span> <span data-ttu-id="918da-181">In the ribbon, click **Authentication Providers** and choose the zone that you wish to use.</span><span class="sxs-lookup"><span data-stu-id="918da-181">In the ribbon, click **Authentication Providers** and choose the zone that you wish to use.</span></span>

    <span data-ttu-id="918da-182">c.</span><span class="sxs-lookup"><span data-stu-id="918da-182">c.</span></span> <span data-ttu-id="918da-183">Select **Trusted Identity provider** and select the identify provider you just registered named *AzureAD*.</span><span class="sxs-lookup"><span data-stu-id="918da-183">Select **Trusted Identity provider** and select the identify provider you just registered named *AzureAD*.</span></span>

    <span data-ttu-id="918da-184">d.</span><span class="sxs-lookup"><span data-stu-id="918da-184">d.</span></span> <span data-ttu-id="918da-185">On the sign-in page URL setting, select **Custom sign in page** and provide the value “/_trust/”.</span><span class="sxs-lookup"><span data-stu-id="918da-185">On the sign-in page URL setting, select **Custom sign in page** and provide the value “/_trust/”.</span></span>

    <span data-ttu-id="918da-186">e.</span><span class="sxs-lookup"><span data-stu-id="918da-186">e.</span></span> <span data-ttu-id="918da-187">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="918da-187">Click **OK**.</span></span>

    ![Configuring your authentication provider](./media\sharepoint-on-premises-tutorial/fig10-configauthprovider.png)

    > [!NOTE]
    > <span data-ttu-id="918da-189">Some of the external users will not able to use this single sign-on integration as their UPN will have mangled value something like `MYEMAIL_outlook.com#ext#@TENANT.onmicrosoft.com`.</span><span class="sxs-lookup"><span data-stu-id="918da-189">Some of the external users will not able to use this single sign-on integration as their UPN will have mangled value something like `MYEMAIL_outlook.com#ext#@TENANT.onmicrosoft.com`.</span></span> <span data-ttu-id="918da-190">Soon we will allow customers app config on how to handle the UPN depending on the user type.</span><span class="sxs-lookup"><span data-stu-id="918da-190">Soon we will allow customers app config on how to handle the UPN depending on the user type.</span></span> <span data-ttu-id="918da-191">After that all your guest users should be able to use SSO seamlessly as the organization employees.</span><span class="sxs-lookup"><span data-stu-id="918da-191">After that all your guest users should be able to use SSO seamlessly as the organization employees.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="918da-192">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="918da-192">Create an Azure AD test user</span></span>

<span data-ttu-id="918da-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="918da-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="918da-195">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="918da-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="918da-196">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="918da-196">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media\sharepoint-on-premises-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="918da-198">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="918da-198">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media\sharepoint-on-premises-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="918da-200">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="918da-200">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media\sharepoint-on-premises-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="918da-202">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="918da-202">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media\sharepoint-on-premises-tutorial/create_aaduser_04.png)

    <span data-ttu-id="918da-204">a.</span><span class="sxs-lookup"><span data-stu-id="918da-204">a.</span></span> <span data-ttu-id="918da-205">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="918da-205">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="918da-206">b.</span><span class="sxs-lookup"><span data-stu-id="918da-206">b.</span></span> <span data-ttu-id="918da-207">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="918da-207">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="918da-208">c.</span><span class="sxs-lookup"><span data-stu-id="918da-208">c.</span></span> <span data-ttu-id="918da-209">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="918da-209">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="918da-210">d.</span><span class="sxs-lookup"><span data-stu-id="918da-210">d.</span></span> <span data-ttu-id="918da-211">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="918da-211">Click **Create**.</span></span>

### <a name="grant-access-to-sharepoint-on-premises-test-user"></a><span data-ttu-id="918da-212">Grant access to SharePoint on-premises test user</span><span class="sxs-lookup"><span data-stu-id="918da-212">Grant access to SharePoint on-premises test user</span></span>

<span data-ttu-id="918da-213">The users who will log into Azure AD and access SharePoint must be granted access to the application  Use the following steps to set the permissions to access the web application.</span><span class="sxs-lookup"><span data-stu-id="918da-213">The users who will log into Azure AD and access SharePoint must be granted access to the application  Use the following steps to set the permissions to access the web application.</span></span>

1. <span data-ttu-id="918da-214">In Central Administration, click **Application Management**.</span><span class="sxs-lookup"><span data-stu-id="918da-214">In Central Administration, click **Application Management**.</span></span>

2. <span data-ttu-id="918da-215">On the **Application Management** page, in the **Web Applications** section, click **Manage web applications**.</span><span class="sxs-lookup"><span data-stu-id="918da-215">On the **Application Management** page, in the **Web Applications** section, click **Manage web applications**.</span></span>

3. <span data-ttu-id="918da-216">Click the appropriate web application, and then click **User Policy**.</span><span class="sxs-lookup"><span data-stu-id="918da-216">Click the appropriate web application, and then click **User Policy**.</span></span>

4. <span data-ttu-id="918da-217">In Policy for Web Application, click **Add Users**.</span><span class="sxs-lookup"><span data-stu-id="918da-217">In Policy for Web Application, click **Add Users**.</span></span>

    ![Searching for a user by their name claim](./media\sharepoint-on-premises-tutorial/fig11-searchbynameclaim.png)

5. <span data-ttu-id="918da-219">In the **Add Users** dialog box, click the appropriate zone in **Zones**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="918da-219">In the **Add Users** dialog box, click the appropriate zone in **Zones**, and then click **Next**.</span></span>

6. <span data-ttu-id="918da-220">In the **Policy for Web Application** dialog box, in the **Choose Users** section, click the **Browse** icon.</span><span class="sxs-lookup"><span data-stu-id="918da-220">In the **Policy for Web Application** dialog box, in the **Choose Users** section, click the **Browse** icon.</span></span>

7. <span data-ttu-id="918da-221">In the **Find** textbox, type the **user principal name(UPN)** value for which you have configured the SharePoint on-premises application in the Azure AD and click **Search**.</span><span class="sxs-lookup"><span data-stu-id="918da-221">In the **Find** textbox, type the **user principal name(UPN)** value for which you have configured the SharePoint on-premises application in the Azure AD and click **Search**.</span></span> </br><span data-ttu-id="918da-222">Example: *brittasimon@contoso.com*.</span><span class="sxs-lookup"><span data-stu-id="918da-222">Example: *brittasimon@contoso.com*.</span></span>

8. <span data-ttu-id="918da-223">Under the AzureAD heading in the list view, select the name property and click **Add** then click **OK** to close the dialog.</span><span class="sxs-lookup"><span data-stu-id="918da-223">Under the AzureAD heading in the list view, select the name property and click **Add** then click **OK** to close the dialog.</span></span>

9. <span data-ttu-id="918da-224">In Permissions, click **Full Control**.</span><span class="sxs-lookup"><span data-stu-id="918da-224">In Permissions, click **Full Control**.</span></span>

    ![Granting full control to a claims user](./media\sharepoint-on-premises-tutorial/fig12-grantfullcontrol.png)

10. <span data-ttu-id="918da-226">Click **Finish**, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="918da-226">Click **Finish**, and then click **OK**.</span></span>

### <a name="configuring-one-trusted-identity-provider-for-multiple-web-applications"></a><span data-ttu-id="918da-227">Configuring one trusted identity provider for multiple web applications</span><span class="sxs-lookup"><span data-stu-id="918da-227">Configuring one trusted identity provider for multiple web applications</span></span>

<span data-ttu-id="918da-228">The configuration works for a single web application, but needs additional configuration if you intend to use the same trusted identity provider for multiple web applications.</span><span class="sxs-lookup"><span data-stu-id="918da-228">The configuration works for a single web application, but needs additional configuration if you intend to use the same trusted identity provider for multiple web applications.</span></span> <span data-ttu-id="918da-229">For example, assume we had extended a web application to use the URL `https://portal.contoso.local` and now want to authenticate the users to `https://sales.contoso.local` as well.</span><span class="sxs-lookup"><span data-stu-id="918da-229">For example, assume we had extended a web application to use the URL `https://portal.contoso.local` and now want to authenticate the users to `https://sales.contoso.local` as well.</span></span> <span data-ttu-id="918da-230">To do this, we need to update the identity provider to honor the WReply parameter and update the application registration in Azure AD to add a reply URL.</span><span class="sxs-lookup"><span data-stu-id="918da-230">To do this, we need to update the identity provider to honor the WReply parameter and update the application registration in Azure AD to add a reply URL.</span></span>

1. <span data-ttu-id="918da-231">In the Azure Portal, open the Azure AD directory.</span><span class="sxs-lookup"><span data-stu-id="918da-231">In the Azure Portal, open the Azure AD directory.</span></span> <span data-ttu-id="918da-232">Click **App registrations**, then click **View all applications**.</span><span class="sxs-lookup"><span data-stu-id="918da-232">Click **App registrations**, then click **View all applications**.</span></span> <span data-ttu-id="918da-233">Click the application that you created previously (SharePoint SAML Integration).</span><span class="sxs-lookup"><span data-stu-id="918da-233">Click the application that you created previously (SharePoint SAML Integration).</span></span>

2. <span data-ttu-id="918da-234">Click **Settings**.</span><span class="sxs-lookup"><span data-stu-id="918da-234">Click **Settings**.</span></span>

3. <span data-ttu-id="918da-235">In the settings blade, click **Reply URLs**.</span><span class="sxs-lookup"><span data-stu-id="918da-235">In the settings blade, click **Reply URLs**.</span></span> 

4. <span data-ttu-id="918da-236">Add the URL for the additional web application with `/_trust/default.aspx` appended to the URL (such as `https://sales.contoso.local/_trust/default.aspx`) and click **Save**.</span><span class="sxs-lookup"><span data-stu-id="918da-236">Add the URL for the additional web application with `/_trust/default.aspx` appended to the URL (such as `https://sales.contoso.local/_trust/default.aspx`) and click **Save**.</span></span>

5. <span data-ttu-id="918da-237">On the SharePoint server, open the **SharePoint 2016 Management Shell** and execute the following commands, using the name of the trusted identity token issuer that you used previously.</span><span class="sxs-lookup"><span data-stu-id="918da-237">On the SharePoint server, open the **SharePoint 2016 Management Shell** and execute the following commands, using the name of the trusted identity token issuer that you used previously.</span></span>

    ```
    $t = Get-SPTrustedIdentityTokenIssuer "AzureAD"
    $t.UseWReplyParameter=$true
    $t.Update()
    ```
6. <span data-ttu-id="918da-238">In Central Administration, go to the web application and enable the existing trusted identity provider.</span><span class="sxs-lookup"><span data-stu-id="918da-238">In Central Administration, go to the web application and enable the existing trusted identity provider.</span></span> <span data-ttu-id="918da-239">Remember to also configure the sign-in page URL as a custom sign in page `/_trust/`.</span><span class="sxs-lookup"><span data-stu-id="918da-239">Remember to also configure the sign-in page URL as a custom sign in page `/_trust/`.</span></span>

7. <span data-ttu-id="918da-240">In Central Administration, click the web application and choose **User Policy**.</span><span class="sxs-lookup"><span data-stu-id="918da-240">In Central Administration, click the web application and choose **User Policy**.</span></span> <span data-ttu-id="918da-241">Add a user with the appropriate permissions as demonstrated previously in this article.</span><span class="sxs-lookup"><span data-stu-id="918da-241">Add a user with the appropriate permissions as demonstrated previously in this article.</span></span>

### <a name="fixing-people-picker"></a><span data-ttu-id="918da-242">Fixing People Picker</span><span class="sxs-lookup"><span data-stu-id="918da-242">Fixing People Picker</span></span>

<span data-ttu-id="918da-243">Users can now log into SharePoint 2016 using identities from Azure AD, but there are still opportunities for improvement to the user experience.</span><span class="sxs-lookup"><span data-stu-id="918da-243">Users can now log into SharePoint 2016 using identities from Azure AD, but there are still opportunities for improvement to the user experience.</span></span> <span data-ttu-id="918da-244">For instance, searching for a user presents multiple search results in the people picker.</span><span class="sxs-lookup"><span data-stu-id="918da-244">For instance, searching for a user presents multiple search results in the people picker.</span></span> <span data-ttu-id="918da-245">There is a search result for each of the 3 claim types that were created in the claim mapping.</span><span class="sxs-lookup"><span data-stu-id="918da-245">There is a search result for each of the 3 claim types that were created in the claim mapping.</span></span> <span data-ttu-id="918da-246">To choose a user using the people picker, you must type their user name exactly and choose the **name** claim result.</span><span class="sxs-lookup"><span data-stu-id="918da-246">To choose a user using the people picker, you must type their user name exactly and choose the **name** claim result.</span></span>

![Claims search results](./media\sharepoint-on-premises-tutorial/fig16-claimssearchresults.png)

<span data-ttu-id="918da-248">There is no validation on the values you search for, which can lead to misspellings or users accidentally choosing the wrong claim type to assign such as the **SurName** claim.</span><span class="sxs-lookup"><span data-stu-id="918da-248">There is no validation on the values you search for, which can lead to misspellings or users accidentally choosing the wrong claim type to assign such as the **SurName** claim.</span></span> <span data-ttu-id="918da-249">This can prevent users from successfully accessing resources.</span><span class="sxs-lookup"><span data-stu-id="918da-249">This can prevent users from successfully accessing resources.</span></span>

<span data-ttu-id="918da-250">To assist with this scenario, there is an open-source solution called [AzureCP](https://yvand.github.io/AzureCP/) that provides a custom claims provider for SharePoint 2016.</span><span class="sxs-lookup"><span data-stu-id="918da-250">To assist with this scenario, there is an open-source solution called [AzureCP](https://yvand.github.io/AzureCP/) that provides a custom claims provider for SharePoint 2016.</span></span> <span data-ttu-id="918da-251">It will use the Azure AD Graph to resolve what users enter and perform validation.</span><span class="sxs-lookup"><span data-stu-id="918da-251">It will use the Azure AD Graph to resolve what users enter and perform validation.</span></span> <span data-ttu-id="918da-252">Learn more at [AzureCP](https://yvand.github.io/AzureCP/).</span><span class="sxs-lookup"><span data-stu-id="918da-252">Learn more at [AzureCP](https://yvand.github.io/AzureCP/).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="918da-253">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="918da-253">Assign the Azure AD test user</span></span>

<span data-ttu-id="918da-254">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SharePoint on-premises.</span><span class="sxs-lookup"><span data-stu-id="918da-254">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SharePoint on-premises.</span></span>

![Assign the user role][200]

<span data-ttu-id="918da-256">**To assign Britta Simon to SharePoint on-premises, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="918da-256">**To assign Britta Simon to SharePoint on-premises, perform the following steps:**</span></span>

1. <span data-ttu-id="918da-257">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="918da-257">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201]

2. <span data-ttu-id="918da-259">In the applications list, select **SharePoint on-premises**.</span><span class="sxs-lookup"><span data-stu-id="918da-259">In the applications list, select **SharePoint on-premises**.</span></span>

    ![The SharePoint link in the Applications list](./media\sharepoint-on-premises-tutorial/tutorial_sharepointonpremises_app.png)

3. <span data-ttu-id="918da-261">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="918da-261">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

4. <span data-ttu-id="918da-263">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="918da-263">Click **Add** button.</span></span> <span data-ttu-id="918da-264">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="918da-264">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

5. <span data-ttu-id="918da-266">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="918da-266">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="918da-267">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="918da-267">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="918da-268">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="918da-268">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="test-single-sign-on"></a><span data-ttu-id="918da-269">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="918da-269">Test single sign-on</span></span>

<span data-ttu-id="918da-270">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="918da-270">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="918da-271">When you click the SharePoint on-premises tile in the Access Panel, you should get automatically signed-on to your SharePoint on-premises application.</span><span class="sxs-lookup"><span data-stu-id="918da-271">When you click the SharePoint on-premises tile in the Access Panel, you should get automatically signed-on to your SharePoint on-premises application.</span></span>
<span data-ttu-id="918da-272">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="918da-272">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="918da-273">Additional resources</span><span class="sxs-lookup"><span data-stu-id="918da-273">Additional resources</span></span>

* [<span data-ttu-id="918da-274">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="918da-274">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="918da-275">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="918da-275">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)
* [<span data-ttu-id="918da-276">Using Azure AD for SharePoint Server Authentication</span><span class="sxs-lookup"><span data-stu-id="918da-276">Using Azure AD for SharePoint Server Authentication</span></span>](https://docs.microsoft.com/en-us/office365/enterprise/using-azure-ad-for-sharepoint-server-authentication)

<!--Image references-->

[1]: ./media\sharepoint-on-premises-tutorial/tutorial_general_01.png
[2]: ./media\sharepoint-on-premises-tutorial/tutorial_general_02.png
[3]: ./media\sharepoint-on-premises-tutorial/tutorial_general_03.png
[4]: ./media\sharepoint-on-premises-tutorial/tutorial_general_04.png

[100]: ./media\sharepoint-on-premises-tutorial/tutorial_general_100.png

[200]: ./media\sharepoint-on-premises-tutorial/tutorial_general_200.png
[201]: ./media\sharepoint-on-premises-tutorial/tutorial_general_201.png
[202]: ./media\sharepoint-on-premises-tutorial/tutorial_general_202.png
[203]: ./media\sharepoint-on-premises-tutorial/tutorial_general_203.png