---
title: 'Tutorial: Azure Active Directory integration with Adobe Sign | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Adobe Sign.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: f9385723-8fe7-4340-8afb-1508dac3e92b
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2018
ms.author: jeedes
ms.openlocfilehash: d5cdc2ec0c6cfcf52f84629485d0dd879fbf6fa2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857055"
---
# <a name="tutorial-azure-active-directory-integration-with-adobe-sign"></a><span data-ttu-id="6cb33-103">Tutorial: Azure Active Directory integration with Adobe Sign</span><span class="sxs-lookup"><span data-stu-id="6cb33-103">Tutorial: Azure Active Directory integration with Adobe Sign</span></span>

<span data-ttu-id="6cb33-104">In this tutorial, you learn how to integrate Adobe Sign with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6cb33-104">In this tutorial, you learn how to integrate Adobe Sign with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6cb33-105">Integrating Adobe Sign with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="6cb33-105">Integrating Adobe Sign with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="6cb33-106">You can control in Azure AD who has access to Adobe Sign.</span><span class="sxs-lookup"><span data-stu-id="6cb33-106">You can control in Azure AD who has access to Adobe Sign.</span></span>
- <span data-ttu-id="6cb33-107">You can enable your users to automatically get signed-on to Adobe Sign (single sign-on) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="6cb33-107">You can enable your users to automatically get signed-on to Adobe Sign (single sign-on) with their Azure AD accounts.</span></span>
- <span data-ttu-id="6cb33-108">You can manage your accounts in one central location--the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="6cb33-108">You can manage your accounts in one central location--the Azure portal.</span></span>

<span data-ttu-id="6cb33-109">For more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="6cb33-109">For more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6cb33-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="6cb33-110">Prerequisites</span></span>

<span data-ttu-id="6cb33-111">To configure Azure AD integration with Adobe Sign, you need:</span><span class="sxs-lookup"><span data-stu-id="6cb33-111">To configure Azure AD integration with Adobe Sign, you need:</span></span>

- <span data-ttu-id="6cb33-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="6cb33-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6cb33-113">An Adobe Sign single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="6cb33-113">An Adobe Sign single sign-on enabled subscription</span></span>

<span data-ttu-id="6cb33-114">To test the steps in this tutorial, follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="6cb33-114">To test the steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="6cb33-115">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="6cb33-115">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6cb33-116">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6cb33-116">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6cb33-117">Scenario description</span><span class="sxs-lookup"><span data-stu-id="6cb33-117">Scenario description</span></span>
<span data-ttu-id="6cb33-118">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="6cb33-118">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6cb33-119">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="6cb33-119">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6cb33-120">Adding Adobe Sign from the gallery.</span><span class="sxs-lookup"><span data-stu-id="6cb33-120">Adding Adobe Sign from the gallery.</span></span>
2. <span data-ttu-id="6cb33-121">Configuring and testing Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="6cb33-121">Configuring and testing Azure AD single sign-on.</span></span>

## <a name="add-adobe-sign-from-the-gallery"></a><span data-ttu-id="6cb33-122">Add Adobe Sign from the gallery</span><span class="sxs-lookup"><span data-stu-id="6cb33-122">Add Adobe Sign from the gallery</span></span>
<span data-ttu-id="6cb33-123">To configure the integration of Adobe Sign into Azure AD, you need to add Adobe Sign from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="6cb33-123">To configure the integration of Adobe Sign into Azure AD, you need to add Adobe Sign from the gallery to your list of managed SaaS apps.</span></span>

1. <span data-ttu-id="6cb33-124">In the [Azure portal](https://portal.azure.com), in the left pane, select the **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="6cb33-124">In the [Azure portal](https://portal.azure.com), in the left pane, select the **Azure Active Directory** icon.</span></span> 

    ![Screenshot of the Azure Active Directory icon][1]

2. <span data-ttu-id="6cb33-126">Browse to **Enterprise applications** > **All applications**.</span><span class="sxs-lookup"><span data-stu-id="6cb33-126">Browse to **Enterprise applications** > **All applications**.</span></span>

    ![Screenshot of Azure Active Directory menus, with Enterprise applications and All applications highlighted][2]
    
3. <span data-ttu-id="6cb33-128">To add a new application, select **New application** at the top of the dialog box.</span><span class="sxs-lookup"><span data-stu-id="6cb33-128">To add a new application, select **New application** at the top of the dialog box.</span></span>

    ![Screenshot of New application option at the top of the dialog box][3]

4. <span data-ttu-id="6cb33-130">In the search box, type **Adobe Sign**.</span><span class="sxs-lookup"><span data-stu-id="6cb33-130">In the search box, type **Adobe Sign**.</span></span>

    ![Screenshot of search box](./media/adobe-echosign-tutorial/tutorial_adobesign_search.png)

5. <span data-ttu-id="6cb33-132">In the results panel, select **Adobe Sign**, and then select **Add**.</span><span class="sxs-lookup"><span data-stu-id="6cb33-132">In the results panel, select **Adobe Sign**, and then select **Add**.</span></span>

    ![Screenshot of results panel](./media/adobe-echosign-tutorial/tutorial_adobesign_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="6cb33-134">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="6cb33-134">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="6cb33-135">In this section, you configure and test Azure AD single sign-on with Adobe Sign, based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="6cb33-135">In this section, you configure and test Azure AD single sign-on with Adobe Sign, based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="6cb33-136">For single sign-on to work, Azure AD needs to recognize a linked relationship between an Azure AD user and the related user in Adobe Sign.</span><span class="sxs-lookup"><span data-stu-id="6cb33-136">For single sign-on to work, Azure AD needs to recognize a linked relationship between an Azure AD user and the related user in Adobe Sign.</span></span>

<span data-ttu-id="6cb33-137">To establish the linked relationship, in Adobe Sign, assign the value of the **user name** in Azure AD as the value of the **Username**.</span><span class="sxs-lookup"><span data-stu-id="6cb33-137">To establish the linked relationship, in Adobe Sign, assign the value of the **user name** in Azure AD as the value of the **Username**.</span></span>

<span data-ttu-id="6cb33-138">To configure and test Azure AD single sign-on with Adobe Sign, complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="6cb33-138">To configure and test Azure AD single sign-on with Adobe Sign, complete the following building blocks:</span></span>

1. <span data-ttu-id="6cb33-139">[Configure Azure AD single sign-on](#configuring-azure-ad-single-sign-on) to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="6cb33-139">[Configure Azure AD single sign-on](#configuring-azure-ad-single-sign-on) to enable your users to use this feature.</span></span>
2. <span data-ttu-id="6cb33-140">[Create an Azure AD test user](#creating-an-azure-ad-test-user) to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6cb33-140">[Create an Azure AD test user](#creating-an-azure-ad-test-user) to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6cb33-141">[Create an Adobe Sign test user](#creating-an-adobe-sign-test-user) to have a counterpart of Britta Simon in Adobe Sign who is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="6cb33-141">[Create an Adobe Sign test user](#creating-an-adobe-sign-test-user) to have a counterpart of Britta Simon in Adobe Sign who is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="6cb33-142">[Assign the Azure AD test user](#assigning-the-azure-ad-test-user) to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="6cb33-142">[Assign the Azure AD test user](#assigning-the-azure-ad-test-user) to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6cb33-143">[Test single sign-On](#testing-single-sign-on) to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="6cb33-143">[Test single sign-On](#testing-single-sign-on) to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="6cb33-144">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="6cb33-144">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="6cb33-145">In this section, you enable Azure AD single sign-on in the Azure portal, and configure single sign-on in your Adobe Sign application.</span><span class="sxs-lookup"><span data-stu-id="6cb33-145">In this section, you enable Azure AD single sign-on in the Azure portal, and configure single sign-on in your Adobe Sign application.</span></span>

1. <span data-ttu-id="6cb33-146">In the Azure portal, on the **Adobe Sign** application integration page, select **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="6cb33-146">In the Azure portal, on the **Adobe Sign** application integration page, select **Single sign-on**.</span></span>

    ![Screenshot of Adobe Sign application integration page, with Single sign-on highlighted][4]

2. <span data-ttu-id="6cb33-148">On the **Single sign-on** dialog box, for **Mode**, select **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="6cb33-148">On the **Single sign-on** dialog box, for **Mode**, select **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Screenshot of Single sign-on dialog box, with Mode box highlighted](./media/adobe-echosign-tutorial/tutorial_adobesign_samlbase.png)

3. <span data-ttu-id="6cb33-150">In the **Adobe Sign Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="6cb33-150">In the **Adobe Sign Domain and URLs** section, perform the following steps:</span></span>

    ![Screenshot of Adobe Sign Domain and URLs section](./media/adobe-echosign-tutorial/tutorial_adobesign_url.png)

    <span data-ttu-id="6cb33-152">a.</span><span class="sxs-lookup"><span data-stu-id="6cb33-152">a.</span></span> <span data-ttu-id="6cb33-153">In the **Sign-on URL** text box, type a URL that uses the following pattern: `https://<companyname>.echosign.com/`</span><span class="sxs-lookup"><span data-stu-id="6cb33-153">In the **Sign-on URL** text box, type a URL that uses the following pattern: `https://<companyname>.echosign.com/`</span></span>

    <span data-ttu-id="6cb33-154">b.</span><span class="sxs-lookup"><span data-stu-id="6cb33-154">b.</span></span> <span data-ttu-id="6cb33-155">In the **Identifier** text box, type a URL that uses the following pattern: `https://<companyname>.echosign.com`</span><span class="sxs-lookup"><span data-stu-id="6cb33-155">In the **Identifier** text box, type a URL that uses the following pattern: `https://<companyname>.echosign.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6cb33-156">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="6cb33-156">These values are not real.</span></span> <span data-ttu-id="6cb33-157">Update these values with the actual sign-on URL and identifier.</span><span class="sxs-lookup"><span data-stu-id="6cb33-157">Update these values with the actual sign-on URL and identifier.</span></span> <span data-ttu-id="6cb33-158">Contact [Adobe Sign Client support team](https://helpx.adobe.com/in/contact/support.html) to get these values.</span><span class="sxs-lookup"><span data-stu-id="6cb33-158">Contact [Adobe Sign Client support team](https://helpx.adobe.com/in/contact/support.html) to get these values.</span></span>

4. <span data-ttu-id="6cb33-159">In the **SAML Signing Certificate** section, select **Certificate(Base64)**, and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="6cb33-159">In the **SAML Signing Certificate** section, select **Certificate(Base64)**, and then save the certificate file on your computer.</span></span>

    ![Screenshot of SAML Signing Certificate section](./media/adobe-echosign-tutorial/tutorial_adobesign_certificate.png) 

5. <span data-ttu-id="6cb33-161">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="6cb33-161">Select **Save**.</span></span>

    ![Screenshot of Save button](./media/adobe-echosign-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6cb33-163">In the **Adobe Sign Configuration** section, select **Configure Adobe Sign** to open the **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="6cb33-163">In the **Adobe Sign Configuration** section, select **Configure Adobe Sign** to open the **Configure sign-on** window.</span></span> <span data-ttu-id="6cb33-164">Copy the **Sign-Out URL**, **SAML Entity ID**, and **SAML Single Sign-On Service URL** from the **Quick Reference** section.</span><span class="sxs-lookup"><span data-stu-id="6cb33-164">Copy the **Sign-Out URL**, **SAML Entity ID**, and **SAML Single Sign-On Service URL** from the **Quick Reference** section.</span></span>

    ![Screenshot of Adobe Sign Configuration section, with Configure Adobe Sign highlighted](./media/adobe-echosign-tutorial/tutorial_adobesign_configure.png)

7. <span data-ttu-id="6cb33-166">Before configuration, contact the [Adobe Sign Client support team](https://helpx.adobe.com/in/contact/support.html) to whitelist your domain in the Adobe Sign.</span><span class="sxs-lookup"><span data-stu-id="6cb33-166">Before configuration, contact the [Adobe Sign Client support team](https://helpx.adobe.com/in/contact/support.html) to whitelist your domain in the Adobe Sign.</span></span> <span data-ttu-id="6cb33-167">Here's how to add the domain:</span><span class="sxs-lookup"><span data-stu-id="6cb33-167">Here's how to add the domain:</span></span>

    <span data-ttu-id="6cb33-168">a.</span><span class="sxs-lookup"><span data-stu-id="6cb33-168">a.</span></span> <span data-ttu-id="6cb33-169">The [Adobe Sign Client support team](https://helpx.adobe.com/in/contact/support.html) sends you a randomly generated token.</span><span class="sxs-lookup"><span data-stu-id="6cb33-169">The [Adobe Sign Client support team](https://helpx.adobe.com/in/contact/support.html) sends you a randomly generated token.</span></span> <span data-ttu-id="6cb33-170">For your domain, the token will be like the following: **adobe-sign-verification= xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx**</span><span class="sxs-lookup"><span data-stu-id="6cb33-170">For your domain, the token will be like the following: **adobe-sign-verification= xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx**</span></span>

    <span data-ttu-id="6cb33-171">b.</span><span class="sxs-lookup"><span data-stu-id="6cb33-171">b.</span></span> <span data-ttu-id="6cb33-172">Publish the verification token in a DNS text record, and notify the [Adobe Sign Client support team](https://helpx.adobe.com/in/contact/support.html).</span><span class="sxs-lookup"><span data-stu-id="6cb33-172">Publish the verification token in a DNS text record, and notify the [Adobe Sign Client support team](https://helpx.adobe.com/in/contact/support.html).</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="6cb33-173">This can take a few days, or longer.</span><span class="sxs-lookup"><span data-stu-id="6cb33-173">This can take a few days, or longer.</span></span> <span data-ttu-id="6cb33-174">Note that DNS propagation delays mean that a value published in DNS might not be visible for an hour or more.</span><span class="sxs-lookup"><span data-stu-id="6cb33-174">Note that DNS propagation delays mean that a value published in DNS might not be visible for an hour or more.</span></span> <span data-ttu-id="6cb33-175">Your IT administrator should be knowledgeable about how to publish this token in a DNS text record.</span><span class="sxs-lookup"><span data-stu-id="6cb33-175">Your IT administrator should be knowledgeable about how to publish this token in a DNS text record.</span></span>
    
    <span data-ttu-id="6cb33-176">c.</span><span class="sxs-lookup"><span data-stu-id="6cb33-176">c.</span></span> <span data-ttu-id="6cb33-177">When you notify the [Adobe Sign Client support team](https://helpx.adobe.com/in/contact/support.html) through the support ticket, after the token is published, they validate the domain and add it to your account.</span><span class="sxs-lookup"><span data-stu-id="6cb33-177">When you notify the [Adobe Sign Client support team](https://helpx.adobe.com/in/contact/support.html) through the support ticket, after the token is published, they validate the domain and add it to your account.</span></span>
    
    <span data-ttu-id="6cb33-178">d.</span><span class="sxs-lookup"><span data-stu-id="6cb33-178">d.</span></span> <span data-ttu-id="6cb33-179">Generally, here's how to publish the token on a DNS record:</span><span class="sxs-lookup"><span data-stu-id="6cb33-179">Generally, here's how to publish the token on a DNS record:</span></span>

    * <span data-ttu-id="6cb33-180">Sign in to your domain account</span><span class="sxs-lookup"><span data-stu-id="6cb33-180">Sign in to your domain account</span></span>
    * <span data-ttu-id="6cb33-181">Find the page for updating the DNS record.</span><span class="sxs-lookup"><span data-stu-id="6cb33-181">Find the page for updating the DNS record.</span></span> <span data-ttu-id="6cb33-182">This page might be called DNS Management, Name Server Management, or Advanced Settings.</span><span class="sxs-lookup"><span data-stu-id="6cb33-182">This page might be called DNS Management, Name Server Management, or Advanced Settings.</span></span>
    * <span data-ttu-id="6cb33-183">Find the TXT records for your domain.</span><span class="sxs-lookup"><span data-stu-id="6cb33-183">Find the TXT records for your domain.</span></span>
    * <span data-ttu-id="6cb33-184">Add a TXT record with the full token value supplied by Adobe.</span><span class="sxs-lookup"><span data-stu-id="6cb33-184">Add a TXT record with the full token value supplied by Adobe.</span></span>
    * <span data-ttu-id="6cb33-185">Save your changes.</span><span class="sxs-lookup"><span data-stu-id="6cb33-185">Save your changes.</span></span>

8. <span data-ttu-id="6cb33-186">In a different web browser window, sign in to your Adobe Sign company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="6cb33-186">In a different web browser window, sign in to your Adobe Sign company site as an administrator.</span></span>

9. <span data-ttu-id="6cb33-187">In the SAML menu, select **Account Settings** > **SAML Settings**.</span><span class="sxs-lookup"><span data-stu-id="6cb33-187">In the SAML menu, select **Account Settings** > **SAML Settings**.</span></span>
   
    <span data-ttu-id="6cb33-188">![Screenshot of Adobe Sign SAML Settings page](./media/adobe-echosign-tutorial/ic789520.png "Account")</span><span class="sxs-lookup"><span data-stu-id="6cb33-188">![Screenshot of Adobe Sign SAML Settings page](./media/adobe-echosign-tutorial/ic789520.png "Account")</span></span>

10. <span data-ttu-id="6cb33-189">In the **SAML Settings** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="6cb33-189">In the **SAML Settings** section, perform the following steps:</span></span>
  
    <span data-ttu-id="6cb33-190">![Screenshot of SAML Settings](./media/adobe-echosign-tutorial/ic789521.png "SAML Settings")</span><span class="sxs-lookup"><span data-stu-id="6cb33-190">![Screenshot of SAML Settings](./media/adobe-echosign-tutorial/ic789521.png "SAML Settings")</span></span>
   
    <span data-ttu-id="6cb33-191">a.</span><span class="sxs-lookup"><span data-stu-id="6cb33-191">a.</span></span> <span data-ttu-id="6cb33-192">Under **SAML Mode**, select **SAML Mandatory**.</span><span class="sxs-lookup"><span data-stu-id="6cb33-192">Under **SAML Mode**, select **SAML Mandatory**.</span></span>
   
    <span data-ttu-id="6cb33-193">b.</span><span class="sxs-lookup"><span data-stu-id="6cb33-193">b.</span></span> <span data-ttu-id="6cb33-194">Select **Allow Echosign Account Administrators to log in using their Echosign Credentials**.</span><span class="sxs-lookup"><span data-stu-id="6cb33-194">Select **Allow Echosign Account Administrators to log in using their Echosign Credentials**.</span></span>
   
    <span data-ttu-id="6cb33-195">c.</span><span class="sxs-lookup"><span data-stu-id="6cb33-195">c.</span></span> <span data-ttu-id="6cb33-196">Under **User Creation**, select **Automatically add users authenticated through SAML**.</span><span class="sxs-lookup"><span data-stu-id="6cb33-196">Under **User Creation**, select **Automatically add users authenticated through SAML**.</span></span>

    <span data-ttu-id="6cb33-197">d.</span><span class="sxs-lookup"><span data-stu-id="6cb33-197">d.</span></span> <span data-ttu-id="6cb33-198">Paste **SAML Entity ID**, which you have copied from the Azure portal into the **Entity ID/Issuer URL** text box.</span><span class="sxs-lookup"><span data-stu-id="6cb33-198">Paste **SAML Entity ID**, which you have copied from the Azure portal into the **Entity ID/Issuer URL** text box.</span></span>
    
    <span data-ttu-id="6cb33-199">e.</span><span class="sxs-lookup"><span data-stu-id="6cb33-199">e.</span></span> <span data-ttu-id="6cb33-200">Paste **SAML Single Sign-On Service URL**, which you have copied from Azure portal into the **Login URL/SSO Endpoint** text box.</span><span class="sxs-lookup"><span data-stu-id="6cb33-200">Paste **SAML Single Sign-On Service URL**, which you have copied from Azure portal into the **Login URL/SSO Endpoint** text box.</span></span>
   
    <span data-ttu-id="6cb33-201">f.</span><span class="sxs-lookup"><span data-stu-id="6cb33-201">f.</span></span> <span data-ttu-id="6cb33-202">Paste **Sign-Out URL**, which you have copied from the Azure portal into the **Logout URL/SLO Endpoint** text box.</span><span class="sxs-lookup"><span data-stu-id="6cb33-202">Paste **Sign-Out URL**, which you have copied from the Azure portal into the **Logout URL/SLO Endpoint** text box.</span></span>

    <span data-ttu-id="6cb33-203">g.</span><span class="sxs-lookup"><span data-stu-id="6cb33-203">g.</span></span> <span data-ttu-id="6cb33-204">Open your downloaded **Certificate(Base64)** file in Notepad.</span><span class="sxs-lookup"><span data-stu-id="6cb33-204">Open your downloaded **Certificate(Base64)** file in Notepad.</span></span> <span data-ttu-id="6cb33-205">Copy the content of it into your clipboard, and then paste it to the **IdP Certificate** text box.</span><span class="sxs-lookup"><span data-stu-id="6cb33-205">Copy the content of it into your clipboard, and then paste it to the **IdP Certificate** text box.</span></span>

    <span data-ttu-id="6cb33-206">h.</span><span class="sxs-lookup"><span data-stu-id="6cb33-206">h.</span></span> <span data-ttu-id="6cb33-207">Select **Save Changes**.</span><span class="sxs-lookup"><span data-stu-id="6cb33-207">Select **Save Changes**.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="6cb33-208">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="6cb33-208">Create an Azure AD test user</span></span>
<span data-ttu-id="6cb33-209">The objective of this section is to create a test user, named Britta Simon, in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="6cb33-209">The objective of this section is to create a test user, named Britta Simon, in the Azure portal.</span></span>

![Screenshot of test user name in the Azure portal][100]

1. <span data-ttu-id="6cb33-211">In the **Azure portal**, in the left pane, select the **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="6cb33-211">In the **Azure portal**, in the left pane, select the **Azure Active Directory** icon.</span></span>

    ![Screenshot of the Azure AD icon](./media/adobe-echosign-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6cb33-213">To display the list of users, go to **Users and groups**, and select **All users**.</span><span class="sxs-lookup"><span data-stu-id="6cb33-213">To display the list of users, go to **Users and groups**, and select **All users**.</span></span>
    
    ![Screenshot of Azure AD menus, with Users and groups and All users highlighted](./media/adobe-echosign-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6cb33-215">To open the **User** dialog box, select **Add**.</span><span class="sxs-lookup"><span data-stu-id="6cb33-215">To open the **User** dialog box, select **Add**.</span></span>
 
    ![Screenshot of top of All users dialog box, with Add option highlighted](./media/adobe-echosign-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6cb33-217">On the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="6cb33-217">On the **User** dialog box, perform the following steps:</span></span>
 
    ![Screenshot of User dialog box](./media/adobe-echosign-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6cb33-219">a.</span><span class="sxs-lookup"><span data-stu-id="6cb33-219">a.</span></span> <span data-ttu-id="6cb33-220">In the **Name** text box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6cb33-220">In the **Name** text box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6cb33-221">b.</span><span class="sxs-lookup"><span data-stu-id="6cb33-221">b.</span></span> <span data-ttu-id="6cb33-222">In the **User name** text box, type the email address of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="6cb33-222">In the **User name** text box, type the email address of BrittaSimon.</span></span>

    <span data-ttu-id="6cb33-223">c.</span><span class="sxs-lookup"><span data-stu-id="6cb33-223">c.</span></span> <span data-ttu-id="6cb33-224">Select **Show Password**, and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="6cb33-224">Select **Show Password**, and write down the value of the **Password**.</span></span>

    <span data-ttu-id="6cb33-225">d.</span><span class="sxs-lookup"><span data-stu-id="6cb33-225">d.</span></span> <span data-ttu-id="6cb33-226">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="6cb33-226">Select **Create**.</span></span>
 
### <a name="create-an-adobe-sign-test-user"></a><span data-ttu-id="6cb33-227">Create an Adobe Sign test user</span><span class="sxs-lookup"><span data-stu-id="6cb33-227">Create an Adobe Sign test user</span></span>

<span data-ttu-id="6cb33-228">To enable Azure AD users to sign in to Adobe Sign, they must be provisioned into Adobe Sign.</span><span class="sxs-lookup"><span data-stu-id="6cb33-228">To enable Azure AD users to sign in to Adobe Sign, they must be provisioned into Adobe Sign.</span></span> <span data-ttu-id="6cb33-229">This is a manual task.</span><span class="sxs-lookup"><span data-stu-id="6cb33-229">This is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="6cb33-230">You can use any other Adobe Sign user account creation tools or APIs provided by Adobe Sign to provision Azure AD user accounts.</span><span class="sxs-lookup"><span data-stu-id="6cb33-230">You can use any other Adobe Sign user account creation tools or APIs provided by Adobe Sign to provision Azure AD user accounts.</span></span> 

1. <span data-ttu-id="6cb33-231">Sign in to your **Adobe Sign** company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="6cb33-231">Sign in to your **Adobe Sign** company site as an administrator.</span></span>

2. <span data-ttu-id="6cb33-232">In the menu on the top, select **Account**.</span><span class="sxs-lookup"><span data-stu-id="6cb33-232">In the menu on the top, select **Account**.</span></span> <span data-ttu-id="6cb33-233">Then, in the left pane, select **Users & Groups** > **Create a new user**.</span><span class="sxs-lookup"><span data-stu-id="6cb33-233">Then, in the left pane, select **Users & Groups** > **Create a new user**.</span></span>
   
    <span data-ttu-id="6cb33-234">![Screenshot of Adobe Sign company site, with Account, Users &Groups, and Create a new user highlighted](./media/adobe-echosign-tutorial/ic789524.png "Account")</span><span class="sxs-lookup"><span data-stu-id="6cb33-234">![Screenshot of Adobe Sign company site, with Account, Users &Groups, and Create a new user highlighted](./media/adobe-echosign-tutorial/ic789524.png "Account")</span></span>
   
3. <span data-ttu-id="6cb33-235">In the **Create New User** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="6cb33-235">In the **Create New User** section, perform the following steps:</span></span>
   
    <span data-ttu-id="6cb33-236">![Screenshot of Create New User section](./media/adobe-echosign-tutorial/ic789525.png "Create User")</span><span class="sxs-lookup"><span data-stu-id="6cb33-236">![Screenshot of Create New User section](./media/adobe-echosign-tutorial/ic789525.png "Create User")</span></span>
   
    <span data-ttu-id="6cb33-237">a.</span><span class="sxs-lookup"><span data-stu-id="6cb33-237">a.</span></span> <span data-ttu-id="6cb33-238">Type the **Email Address**, **First Name**, and **Last Name** of a valid Azure AD account you want to provision into the related text boxes.</span><span class="sxs-lookup"><span data-stu-id="6cb33-238">Type the **Email Address**, **First Name**, and **Last Name** of a valid Azure AD account you want to provision into the related text boxes.</span></span>
   
    <span data-ttu-id="6cb33-239">b.</span><span class="sxs-lookup"><span data-stu-id="6cb33-239">b.</span></span> <span data-ttu-id="6cb33-240">Select **Create User**.</span><span class="sxs-lookup"><span data-stu-id="6cb33-240">Select **Create User**.</span></span>

>[!NOTE]
><span data-ttu-id="6cb33-241">The Azure Active Directory account holder receives an email that includes a link to confirm the account, before it becomes active.</span><span class="sxs-lookup"><span data-stu-id="6cb33-241">The Azure Active Directory account holder receives an email that includes a link to confirm the account, before it becomes active.</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="6cb33-242">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="6cb33-242">Assign the Azure AD test user</span></span>

<span data-ttu-id="6cb33-243">In this section, you enable Britta Simon to use Azure single sign-on, by granting access to Adobe Sign.</span><span class="sxs-lookup"><span data-stu-id="6cb33-243">In this section, you enable Britta Simon to use Azure single sign-on, by granting access to Adobe Sign.</span></span>

![Screenshot of Azure portal single sign-on][200] 

1. <span data-ttu-id="6cb33-245">In the Azure portal, open the applications view.</span><span class="sxs-lookup"><span data-stu-id="6cb33-245">In the Azure portal, open the applications view.</span></span> <span data-ttu-id="6cb33-246">Then browse to the directory view, go to **Enterprise applications**, and select **All applications**.</span><span class="sxs-lookup"><span data-stu-id="6cb33-246">Then browse to the directory view, go to **Enterprise applications**, and select **All applications**.</span></span>

    ![Screenshot of Azure portal applications view, with Enterprise applications and All applications highlighted][201] 

2. <span data-ttu-id="6cb33-248">In the applications list, select **Adobe Sign**.</span><span class="sxs-lookup"><span data-stu-id="6cb33-248">In the applications list, select **Adobe Sign**.</span></span>

    ![Screenshot of applications list, with Adobe Sign highlighted](./media/adobe-echosign-tutorial/tutorial_adobesign_app.png) 

3. <span data-ttu-id="6cb33-250">In the menu on the left, select **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="6cb33-250">In the menu on the left, select **Users and groups**.</span></span>

    ![Screenshot of menu, with Users and groups highlighted][202] 

4. <span data-ttu-id="6cb33-252">Select **Add**.</span><span class="sxs-lookup"><span data-stu-id="6cb33-252">Select **Add**.</span></span> <span data-ttu-id="6cb33-253">Then, in the **Add Assignment** section, select **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="6cb33-253">Then, in the **Add Assignment** section, select **Users and groups**.</span></span>

    ![Screenshot of Users and groups page and Add Assignment section][203]

5. <span data-ttu-id="6cb33-255">In **Users and groups** dialog box, in the users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="6cb33-255">In **Users and groups** dialog box, in the users list, select **Britta Simon**.</span></span>

6. <span data-ttu-id="6cb33-256">In the **Users and groups** dialog box, click **Select**.</span><span class="sxs-lookup"><span data-stu-id="6cb33-256">In the **Users and groups** dialog box, click **Select**.</span></span>

7. <span data-ttu-id="6cb33-257">In the **Add Assignment** dialog box, select **Assign**.</span><span class="sxs-lookup"><span data-stu-id="6cb33-257">In the **Add Assignment** dialog box, select **Assign**.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="6cb33-258">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="6cb33-258">Test single sign-on</span></span>

<span data-ttu-id="6cb33-259">When you select the Adobe Sign tile in the Access Panel, you should get automatically signed on to your Adobe Sign application.</span><span class="sxs-lookup"><span data-stu-id="6cb33-259">When you select the Adobe Sign tile in the Access Panel, you should get automatically signed on to your Adobe Sign application.</span></span> <span data-ttu-id="6cb33-260">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6cb33-260">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6cb33-261">Additional resources</span><span class="sxs-lookup"><span data-stu-id="6cb33-261">Additional resources</span></span>

* [<span data-ttu-id="6cb33-262">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6cb33-262">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="6cb33-263">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6cb33-263">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/adobe-echosign-tutorial/tutorial_general_01.png
[2]: ./media/adobe-echosign-tutorial/tutorial_general_02.png
[3]: ./media/adobe-echosign-tutorial/tutorial_general_03.png
[4]: ./media/adobe-echosign-tutorial/tutorial_general_04.png

[100]: ./media/adobe-echosign-tutorial/tutorial_general_100.png

[200]: ./media/adobe-echosign-tutorial/tutorial_general_200.png
[201]: ./media/adobe-echosign-tutorial/tutorial_general_201.png
[202]: ./media/adobe-echosign-tutorial/tutorial_general_202.png
[203]: ./media/adobe-echosign-tutorial/tutorial_general_203.png
