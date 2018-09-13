---
title: 'Tutorial: Azure Active Directory integration with SuccessFactors | Microsoft Docs'
description: Learn how to use SuccessFactors with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 32bd8898-c2d2-4aa7-8c46-f1f5c2aa05f1
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 542e6e0fa045bcc3dda9f7b7d5549a19613b3cfe
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563873"
---
# <a name="tutorial-azure-active-directory-integration-with-successfactors"></a><span data-ttu-id="e753c-103">Tutorial: Azure Active Directory integration with SuccessFactors</span><span class="sxs-lookup"><span data-stu-id="e753c-103">Tutorial: Azure Active Directory integration with SuccessFactors</span></span>
<span data-ttu-id="e753c-104">The objective of this tutorial is to show you how to integrate SuccessFactors with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e753c-104">The objective of this tutorial is to show you how to integrate SuccessFactors with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e753c-105">Integrating SuccessFactors with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="e753c-105">Integrating SuccessFactors with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="e753c-106">You can control in Azure AD who has access to SuccessFactors</span><span class="sxs-lookup"><span data-stu-id="e753c-106">You can control in Azure AD who has access to SuccessFactors</span></span>
* <span data-ttu-id="e753c-107">You can enable your users to automatically get signed-on to SuccessFactors (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="e753c-107">You can enable your users to automatically get signed-on to SuccessFactors (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="e753c-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="e753c-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="e753c-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e753c-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e753c-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e753c-110">Prerequisites</span></span>
<span data-ttu-id="e753c-111">To configure Azure AD integration with SuccessFactors, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="e753c-111">To configure Azure AD integration with SuccessFactors, you need the following items:</span></span>

* <span data-ttu-id="e753c-112">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="e753c-112">A valid Azure subscription</span></span>
* <span data-ttu-id="e753c-113">A tenant in SuccessFactors</span><span class="sxs-lookup"><span data-stu-id="e753c-113">A tenant in SuccessFactors</span></span>

> [!NOTE]
> <span data-ttu-id="e753c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="e753c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="e753c-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="e753c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="e753c-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="e753c-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="e753c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e753c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e753c-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="e753c-118">Scenario description</span></span>
<span data-ttu-id="e753c-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="e753c-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="e753c-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="e753c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e753c-121">Adding SuccessFactors from the gallery</span><span class="sxs-lookup"><span data-stu-id="e753c-121">Adding SuccessFactors from the gallery</span></span>
2. <span data-ttu-id="e753c-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="e753c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-successfactors-from-the-gallery"></a><span data-ttu-id="e753c-123">Adding SuccessFactors from the gallery</span><span class="sxs-lookup"><span data-stu-id="e753c-123">Adding SuccessFactors from the gallery</span></span>
<span data-ttu-id="e753c-124">To configure the integration of SuccessFactors into Azure AD, you need to add SuccessFactors from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="e753c-124">To configure the integration of SuccessFactors into Azure AD, you need to add SuccessFactors from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e753c-125">**To add SuccessFactors from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e753c-125">**To add SuccessFactors from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e753c-126">In the Azure classic portal, on the left navigation panel, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e753c-126">In the Azure classic portal, on the left navigation panel, click **Active Directory**.</span></span>
   
    ![Configuring single sign-on][1]
2. <span data-ttu-id="e753c-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="e753c-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="e753c-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="e753c-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Configuring single sign-on][2]
4. <span data-ttu-id="e753c-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="e753c-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="e753c-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="e753c-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Configuring single sign-on][4]
6. <span data-ttu-id="e753c-135">In the **search box**, type **SuccessFactors**.</span><span class="sxs-lookup"><span data-stu-id="e753c-135">In the **search box**, type **SuccessFactors**.</span></span>
   
    ![Configuring single sign-on][5]
7. <span data-ttu-id="e753c-137">In the results panel, select **SuccessFactors**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="e753c-137">In the results panel, select **SuccessFactors**, and then click **Complete** to add the application.</span></span>
   
    ![Configuring single sign-on][6]

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e753c-139">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="e753c-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e753c-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with SuccessFactors based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="e753c-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with SuccessFactors based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e753c-141">For single sign-on to work, Azure AD needs to know what the counterpart user in SuccessFactors to an user in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="e753c-141">For single sign-on to work, Azure AD needs to know what the counterpart user in SuccessFactors to an user in Azure AD is.</span></span> <span data-ttu-id="e753c-142">In other words, a link relationship between an Azure AD user and the related user in SuccessFactors needs to be established.</span><span class="sxs-lookup"><span data-stu-id="e753c-142">In other words, a link relationship between an Azure AD user and the related user in SuccessFactors needs to be established.</span></span>

<span data-ttu-id="e753c-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in SuccessFactors.</span><span class="sxs-lookup"><span data-stu-id="e753c-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in SuccessFactors.</span></span>

<span data-ttu-id="e753c-144">To configure and test Azure AD single sign-on with SuccessFactors, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="e753c-144">To configure and test Azure AD single sign-on with SuccessFactors, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e753c-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="e753c-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e753c-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e753c-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e753c-147">**[Creating a SuccessFactors test user](#creating-a-successfactors-test-user)** - to have a counterpart of Britta Simon in SuccessFactors that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="e753c-147">**[Creating a SuccessFactors test user](#creating-a-successfactors-test-user)** - to have a counterpart of Britta Simon in SuccessFactors that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="e753c-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="e753c-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e753c-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="e753c-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e753c-150">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="e753c-150">Configuring Azure AD single sign-on</span></span>
<span data-ttu-id="e753c-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your SuccessFactors application.</span><span class="sxs-lookup"><span data-stu-id="e753c-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your SuccessFactors application.</span></span>

<span data-ttu-id="e753c-152">**To configure Azure AD single sign-on with SuccessFactors, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e753c-152">**To configure Azure AD single sign-on with SuccessFactors, perform the following steps:**</span></span>

1. <span data-ttu-id="e753c-153">In the Azure classic portal, on the **SuccessFactors** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="e753c-153">In the Azure classic portal, on the **SuccessFactors** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
    ![Configuring single sign-on][7]
2. <span data-ttu-id="e753c-155">On the **How would you like users to sign on to SuccessFactors** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="e753c-155">On the **How would you like users to sign on to SuccessFactors** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configuring single sign-on][8]
3. <span data-ttu-id="e753c-157">On the **Configure App URL** page, perform the following steps, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="e753c-157">On the **Configure App URL** page, perform the following steps, and then click **Next**.</span></span>
   
    ![Configuring single sign-on][9]
   
    <span data-ttu-id="e753c-159">a.</span><span class="sxs-lookup"><span data-stu-id="e753c-159">a.</span></span> <span data-ttu-id="e753c-160">In the **Sign On URL** textbox, type a URL using one of the following patterns:</span><span class="sxs-lookup"><span data-stu-id="e753c-160">In the **Sign On URL** textbox, type a URL using one of the following patterns:</span></span> 
   
    |  |
    | --- |
    | `https://<company name>.successfactors.com/<company name>` |
    | `https://<company name>.sapsf.com/<company name>` |
    | `https://<company name>.successfactors.eu/<company name>` |
    | `https://<company name>.sapsf.eu` |
   
    <span data-ttu-id="e753c-161">b.</span><span class="sxs-lookup"><span data-stu-id="e753c-161">b.</span></span> <span data-ttu-id="e753c-162">In the **Reply URL** textbox, type a URL using one of the following patterns:</span><span class="sxs-lookup"><span data-stu-id="e753c-162">In the **Reply URL** textbox, type a URL using one of the following patterns:</span></span> 
   
    |  |
    | --- |
    | `https://<company name>.successfactors.com/<company name>` |
    | `https://<company name>.sapsf.com/<company name>` |
    | `https://<company name>.successfactors.eu/<company name>` |
    | `https://<company name>.sapsf.eu` |
    | `https://<company name>.sapsf.eu/<company name>` |
   
    <span data-ttu-id="e753c-163">c.</span><span class="sxs-lookup"><span data-stu-id="e753c-163">c.</span></span> <span data-ttu-id="e753c-164">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="e753c-164">Click **Next**.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="e753c-165">Please note that these are not the real values.</span><span class="sxs-lookup"><span data-stu-id="e753c-165">Please note that these are not the real values.</span></span> <span data-ttu-id="e753c-166">You have to update these values with the actual Sign On URL and Reply URL.</span><span class="sxs-lookup"><span data-stu-id="e753c-166">You have to update these values with the actual Sign On URL and Reply URL.</span></span> <span data-ttu-id="e753c-167">To get these values, contact [SuccessFactors support team](https://www.successfactors.com/en_us/support.html).</span><span class="sxs-lookup"><span data-stu-id="e753c-167">To get these values, contact [SuccessFactors support team](https://www.successfactors.com/en_us/support.html).</span></span>

1. <span data-ttu-id="e753c-168">On the **Configure single sign-on at SuccessFactors** page, click **Download certificate**, and then save the certificate file locally on your computer.</span><span class="sxs-lookup"><span data-stu-id="e753c-168">On the **Configure single sign-on at SuccessFactors** page, click **Download certificate**, and then save the certificate file locally on your computer.</span></span>
   
    ![Configuring single sign-on][10]

2. <span data-ttu-id="e753c-170">In a different web browser window, log into your **SuccessFactors admin portal** as an administrator.</span><span class="sxs-lookup"><span data-stu-id="e753c-170">In a different web browser window, log into your **SuccessFactors admin portal** as an administrator.</span></span>

3. <span data-ttu-id="e753c-171">Visit **Application Security** and native to **Single Sign On Feature**.</span><span class="sxs-lookup"><span data-stu-id="e753c-171">Visit **Application Security** and native to **Single Sign On Feature**.</span></span> 

4. <span data-ttu-id="e753c-172">Place any value in the **Reset Token** and click **Save Token** to enable SAML SSO.</span><span class="sxs-lookup"><span data-stu-id="e753c-172">Place any value in the **Reset Token** and click **Save Token** to enable SAML SSO.</span></span>
   
    ![Configuring single sign-on on app side][11]

    > [!NOTE] 
    > <span data-ttu-id="e753c-174">This value is just used as the on/off switch.</span><span class="sxs-lookup"><span data-stu-id="e753c-174">This value is just used as the on/off switch.</span></span> <span data-ttu-id="e753c-175">If any value is saved, the SAML SSO is ON.</span><span class="sxs-lookup"><span data-stu-id="e753c-175">If any value is saved, the SAML SSO is ON.</span></span> <span data-ttu-id="e753c-176">If a blank value is saved the SAML SSO is OFF.</span><span class="sxs-lookup"><span data-stu-id="e753c-176">If a blank value is saved the SAML SSO is OFF.</span></span>

1. <span data-ttu-id="e753c-177">Native to below screenshot and perform the following actions.</span><span class="sxs-lookup"><span data-stu-id="e753c-177">Native to below screenshot and perform the following actions.</span></span>
   
    ![Configuring single sign-on on app side][12]
   
    <span data-ttu-id="e753c-179">a.</span><span class="sxs-lookup"><span data-stu-id="e753c-179">a.</span></span> <span data-ttu-id="e753c-180">Select the **SAML v2 SSO** Radio Button</span><span class="sxs-lookup"><span data-stu-id="e753c-180">Select the **SAML v2 SSO** Radio Button</span></span>
   
    <span data-ttu-id="e753c-181">b.</span><span class="sxs-lookup"><span data-stu-id="e753c-181">b.</span></span> <span data-ttu-id="e753c-182">Set the SAML Asserting Party Name(e.g. SAml issuer + company name).</span><span class="sxs-lookup"><span data-stu-id="e753c-182">Set the SAML Asserting Party Name(e.g. SAml issuer + company name).</span></span>
   
    <span data-ttu-id="e753c-183">c.</span><span class="sxs-lookup"><span data-stu-id="e753c-183">c.</span></span> <span data-ttu-id="e753c-184">In the **SAML Issuer** textbox put the value of **Issuer URL** from Azure AD application configuration wizard.</span><span class="sxs-lookup"><span data-stu-id="e753c-184">In the **SAML Issuer** textbox put the value of **Issuer URL** from Azure AD application configuration wizard.</span></span>
   
    <span data-ttu-id="e753c-185">d.</span><span class="sxs-lookup"><span data-stu-id="e753c-185">d.</span></span> <span data-ttu-id="e753c-186">Select **Response(Customer Generated/IdP/AP)** as **Require Mandatory Signature**.</span><span class="sxs-lookup"><span data-stu-id="e753c-186">Select **Response(Customer Generated/IdP/AP)** as **Require Mandatory Signature**.</span></span>
   
    <span data-ttu-id="e753c-187">e.</span><span class="sxs-lookup"><span data-stu-id="e753c-187">e.</span></span> <span data-ttu-id="e753c-188">Select **Enabled** as **Enable SAML Flag**.</span><span class="sxs-lookup"><span data-stu-id="e753c-188">Select **Enabled** as **Enable SAML Flag**.</span></span>
   
    <span data-ttu-id="e753c-189">f.</span><span class="sxs-lookup"><span data-stu-id="e753c-189">f.</span></span> <span data-ttu-id="e753c-190">Select **No** as **Login Request Signature(SF Generated/SP/RP)**.</span><span class="sxs-lookup"><span data-stu-id="e753c-190">Select **No** as **Login Request Signature(SF Generated/SP/RP)**.</span></span>
   
    <span data-ttu-id="e753c-191">g.</span><span class="sxs-lookup"><span data-stu-id="e753c-191">g.</span></span> <span data-ttu-id="e753c-192">Select **Browser/Post Profile** as **SAML Profile**.</span><span class="sxs-lookup"><span data-stu-id="e753c-192">Select **Browser/Post Profile** as **SAML Profile**.</span></span>
   
    <span data-ttu-id="e753c-193">h.</span><span class="sxs-lookup"><span data-stu-id="e753c-193">h.</span></span> <span data-ttu-id="e753c-194">Select **No** as **Enforce Certificate Valid Period**.</span><span class="sxs-lookup"><span data-stu-id="e753c-194">Select **No** as **Enforce Certificate Valid Period**.</span></span>
   
    <span data-ttu-id="e753c-195">i.</span><span class="sxs-lookup"><span data-stu-id="e753c-195">i.</span></span> <span data-ttu-id="e753c-196">Copy the content of the downloaded certificate file, and then paste it into the **SAML Verifying Certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="e753c-196">Copy the content of the downloaded certificate file, and then paste it into the **SAML Verifying Certificate** textbox.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e753c-197">The certificate content must have begin certificate and end certificate tags.</span><span class="sxs-lookup"><span data-stu-id="e753c-197">The certificate content must have begin certificate and end certificate tags.</span></span>

1. <span data-ttu-id="e753c-198">Navigate to SAML V2, and then perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="e753c-198">Navigate to SAML V2, and then perform the following steps:</span></span>
   
    ![Configuring single sign-on on app side][13]
   
    <span data-ttu-id="e753c-200">a.</span><span class="sxs-lookup"><span data-stu-id="e753c-200">a.</span></span> <span data-ttu-id="e753c-201">Select **Yes** as **Support SP-initiated Global Logout**.</span><span class="sxs-lookup"><span data-stu-id="e753c-201">Select **Yes** as **Support SP-initiated Global Logout**.</span></span>
   
    <span data-ttu-id="e753c-202">b.</span><span class="sxs-lookup"><span data-stu-id="e753c-202">b.</span></span> <span data-ttu-id="e753c-203">In the **Global Logout Service URL (LogoutRequest destination)** textbox put the value of **Remote Logout URL** from Azure AD application configuration wizard.</span><span class="sxs-lookup"><span data-stu-id="e753c-203">In the **Global Logout Service URL (LogoutRequest destination)** textbox put the value of **Remote Logout URL** from Azure AD application configuration wizard.</span></span>
   
    <span data-ttu-id="e753c-204">c.</span><span class="sxs-lookup"><span data-stu-id="e753c-204">c.</span></span> <span data-ttu-id="e753c-205">Select **No** as **Require sp must encrypt all NameID element**.</span><span class="sxs-lookup"><span data-stu-id="e753c-205">Select **No** as **Require sp must encrypt all NameID element**.</span></span>
   
    <span data-ttu-id="e753c-206">d.</span><span class="sxs-lookup"><span data-stu-id="e753c-206">d.</span></span> <span data-ttu-id="e753c-207">Select **unspecified** as **NameID Format**.</span><span class="sxs-lookup"><span data-stu-id="e753c-207">Select **unspecified** as **NameID Format**.</span></span>
   
    <span data-ttu-id="e753c-208">e.</span><span class="sxs-lookup"><span data-stu-id="e753c-208">e.</span></span> <span data-ttu-id="e753c-209">Select **Yes** as **Enable sp initiated login (AuthnRequest)**.</span><span class="sxs-lookup"><span data-stu-id="e753c-209">Select **Yes** as **Enable sp initiated login (AuthnRequest)**.</span></span>
   
    <span data-ttu-id="e753c-210">f.</span><span class="sxs-lookup"><span data-stu-id="e753c-210">f.</span></span> <span data-ttu-id="e753c-211">In the **Send request as Company-Wide issuer** textbox put the value of **Remote Login URL** from Azure AD application configuration wizard.</span><span class="sxs-lookup"><span data-stu-id="e753c-211">In the **Send request as Company-Wide issuer** textbox put the value of **Remote Login URL** from Azure AD application configuration wizard.</span></span>
2. <span data-ttu-id="e753c-212">Perform these steps if you want to make the login usernames Case Insensitive, .</span><span class="sxs-lookup"><span data-stu-id="e753c-212">Perform these steps if you want to make the login usernames Case Insensitive, .</span></span>
   
    <span data-ttu-id="e753c-213">a.</span><span class="sxs-lookup"><span data-stu-id="e753c-213">a.</span></span> <span data-ttu-id="e753c-214">Visit **Company Settings**(near the bottom).</span><span class="sxs-lookup"><span data-stu-id="e753c-214">Visit **Company Settings**(near the bottom).</span></span>
   
    <span data-ttu-id="e753c-215">b.</span><span class="sxs-lookup"><span data-stu-id="e753c-215">b.</span></span> <span data-ttu-id="e753c-216">select checkbox near **Enable Non-Case-Sensitive Username**.</span><span class="sxs-lookup"><span data-stu-id="e753c-216">select checkbox near **Enable Non-Case-Sensitive Username**.</span></span>
   
    <span data-ttu-id="e753c-217">c.Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="e753c-217">c.Click **Save**.</span></span>
   
    ![Configure Single Sign-On][29]

    > [!NOTE] 
    > <span data-ttu-id="e753c-219">If you try to enable this, the system checks if it will create a duplicate SAML login name.</span><span class="sxs-lookup"><span data-stu-id="e753c-219">If you try to enable this, the system checks if it will create a duplicate SAML login name.</span></span> <span data-ttu-id="e753c-220">For example if the customer has usernames User1 and user1.</span><span class="sxs-lookup"><span data-stu-id="e753c-220">For example if the customer has usernames User1 and user1.</span></span> <span data-ttu-id="e753c-221">Taking away case sensitivity makes these duplicates.</span><span class="sxs-lookup"><span data-stu-id="e753c-221">Taking away case sensitivity makes these duplicates.</span></span> <span data-ttu-id="e753c-222">The system will give you an error message and will not enable the feature.</span><span class="sxs-lookup"><span data-stu-id="e753c-222">The system will give you an error message and will not enable the feature.</span></span> <span data-ttu-id="e753c-223">The customer will need to change one of the usernames so it’s actually spelled different.</span><span class="sxs-lookup"><span data-stu-id="e753c-223">The customer will need to change one of the usernames so it’s actually spelled different.</span></span> 

1. <span data-ttu-id="e753c-224">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="e753c-224">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
    ![Applications][14]
2. <span data-ttu-id="e753c-226">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="e753c-226">On the **Single sign-on confirmation** page, click **Complete**.</span></span>
   
    ![Applications][15]

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e753c-228">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="e753c-228">Creating an Azure AD test user</span></span>
<span data-ttu-id="e753c-229">The objective of this section is to create a test user in the classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e753c-229">The objective of this section is to create a test user in the classic portal called Britta Simon.</span></span>

![Create Azure AD User][16]

<span data-ttu-id="e753c-231">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e753c-231">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e753c-232">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e753c-232">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user][17]
2. <span data-ttu-id="e753c-234">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="e753c-234">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="e753c-235">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="e753c-235">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user][18]
4. <span data-ttu-id="e753c-237">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="e753c-237">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user][19]
5. <span data-ttu-id="e753c-239">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="e753c-239">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user][20]
   
    <span data-ttu-id="e753c-241">a.</span><span class="sxs-lookup"><span data-stu-id="e753c-241">a.</span></span> <span data-ttu-id="e753c-242">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="e753c-242">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="e753c-243">b.</span><span class="sxs-lookup"><span data-stu-id="e753c-243">b.</span></span> <span data-ttu-id="e753c-244">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e753c-244">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="e753c-245">c.</span><span class="sxs-lookup"><span data-stu-id="e753c-245">c.</span></span> <span data-ttu-id="e753c-246">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="e753c-246">Click **Next**.</span></span>
6. <span data-ttu-id="e753c-247">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="e753c-247">On the **User Profile** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user][21]
   
    <span data-ttu-id="e753c-249">a.</span><span class="sxs-lookup"><span data-stu-id="e753c-249">a.</span></span> <span data-ttu-id="e753c-250">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="e753c-250">In the **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="e753c-251">b.</span><span class="sxs-lookup"><span data-stu-id="e753c-251">b.</span></span> <span data-ttu-id="e753c-252">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="e753c-252">In the **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="e753c-253">c.</span><span class="sxs-lookup"><span data-stu-id="e753c-253">c.</span></span> <span data-ttu-id="e753c-254">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="e753c-254">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="e753c-255">d.</span><span class="sxs-lookup"><span data-stu-id="e753c-255">d.</span></span> <span data-ttu-id="e753c-256">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="e753c-256">In the **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="e753c-257">e.</span><span class="sxs-lookup"><span data-stu-id="e753c-257">e.</span></span> <span data-ttu-id="e753c-258">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="e753c-258">Click **Next**.</span></span>
7. <span data-ttu-id="e753c-259">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="e753c-259">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user][22]
8. <span data-ttu-id="e753c-261">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="e753c-261">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user][23]
   
    <span data-ttu-id="e753c-263">a.</span><span class="sxs-lookup"><span data-stu-id="e753c-263">a.</span></span> <span data-ttu-id="e753c-264">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="e753c-264">Write down the value of the **New Password**.</span></span>
   
    <span data-ttu-id="e753c-265">b.</span><span class="sxs-lookup"><span data-stu-id="e753c-265">b.</span></span> <span data-ttu-id="e753c-266">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="e753c-266">Click **Complete**.</span></span>  

### <a name="creating-a-successfactors-test-user"></a><span data-ttu-id="e753c-267">Creating a SuccessFactors test user</span><span class="sxs-lookup"><span data-stu-id="e753c-267">Creating a SuccessFactors test user</span></span>
<span data-ttu-id="e753c-268">In order to enable Azure AD users to log into SuccessFactors, they must be provisioned into SuccessFactors.</span><span class="sxs-lookup"><span data-stu-id="e753c-268">In order to enable Azure AD users to log into SuccessFactors, they must be provisioned into SuccessFactors.</span></span>  
<span data-ttu-id="e753c-269">In the case of SuccessFactors, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="e753c-269">In the case of SuccessFactors, provisioning is a manual task.</span></span>

<span data-ttu-id="e753c-270">To get users created in SuccessFactors, you need to contact the [SuccessFactors support team](https://www.successfactors.com/en_us/support.html).</span><span class="sxs-lookup"><span data-stu-id="e753c-270">To get users created in SuccessFactors, you need to contact the [SuccessFactors support team](https://www.successfactors.com/en_us/support.html).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e753c-271">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="e753c-271">Assigning the Azure AD test user</span></span>
<span data-ttu-id="e753c-272">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to SuccessFactors.</span><span class="sxs-lookup"><span data-stu-id="e753c-272">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to SuccessFactors.</span></span>

![Assign User][24]

<span data-ttu-id="e753c-274">**To assign Britta Simon to SuccessFactors, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e753c-274">**To assign Britta Simon to SuccessFactors, perform the following steps:**</span></span>

1. <span data-ttu-id="e753c-275">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="e753c-275">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][25]
2. <span data-ttu-id="e753c-277">In the applications list, select **SuccessFactors**.</span><span class="sxs-lookup"><span data-stu-id="e753c-277">In the applications list, select **SuccessFactors**.</span></span>
   
    ![Configure Single Sign-On][26]
3. <span data-ttu-id="e753c-279">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="e753c-279">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][27]
4. <span data-ttu-id="e753c-281">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="e753c-281">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="e753c-282">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="e753c-282">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][28]

### <a name="testing-single-sign-on"></a><span data-ttu-id="e753c-284">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="e753c-284">Testing single sign-on</span></span>
<span data-ttu-id="e753c-285">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="e753c-285">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e753c-286">When you click the SuccessFactors tile in the Access Panel, you should get automatically signed-on to your SuccessFactors application.</span><span class="sxs-lookup"><span data-stu-id="e753c-286">When you click the SuccessFactors tile in the Access Panel, you should get automatically signed-on to your SuccessFactors application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e753c-287">Additional resources</span><span class="sxs-lookup"><span data-stu-id="e753c-287">Additional resources</span></span>
* [<span data-ttu-id="e753c-288">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e753c-288">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e753c-289">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e753c-289">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[0]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_00.png
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-successfactors-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-successfactors-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-successfactors-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-successfactors-tutorial/tutorial_general_04.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_01.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_02.png
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_03.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_04.png
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_06.png

[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_07.png
[12]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_08.png
[13]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_09.png
[14]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-successfactors-tutorial/tutorial_general_05.png
[15]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-successfactors-tutorial/tutorial_general_06.png

[16]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-successfactors-tutorial/create_aaduser_00.png
[17]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-successfactors-tutorial/create_aaduser_01.png
[18]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-successfactors-tutorial/create_aaduser_02.png
[19]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-successfactors-tutorial/create_aaduser_03.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-successfactors-tutorial/create_aaduser_04.png
[21]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-successfactors-tutorial/create_aaduser_05.png
[22]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-successfactors-tutorial/create_aaduser_06.png
[23]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-successfactors-tutorial/create_aaduser_07.png

[24]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-successfactors-tutorial/tutorial_general_07.png
[25]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-successfactors-tutorial/tutorial_general_08.png
[26]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_11.png
[27]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-successfactors-tutorial/tutorial_general_09.png
[28]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-successfactors-tutorial/tutorial_general_10.png
[29]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_10.png






























