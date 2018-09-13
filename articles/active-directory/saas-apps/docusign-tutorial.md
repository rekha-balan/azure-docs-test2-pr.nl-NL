---
title: 'Tutorial: Azure Active Directory integration with DocuSign | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and DocuSign.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: a691288b-84c1-40fb-84bd-5b06878865f0
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: 5d8aef1edf4d7a02686db48d3e788e4f9493c398
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857240"
---
# <a name="tutorial-azure-active-directory-integration-with-docusign"></a><span data-ttu-id="92929-103">Tutorial: Azure Active Directory integration with DocuSign</span><span class="sxs-lookup"><span data-stu-id="92929-103">Tutorial: Azure Active Directory integration with DocuSign</span></span>

<span data-ttu-id="92929-104">In this tutorial, you learn how to integrate DocuSign with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="92929-104">In this tutorial, you learn how to integrate DocuSign with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="92929-105">Integrating DocuSign with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="92929-105">Integrating DocuSign with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="92929-106">You can control in Azure AD who has access to DocuSign</span><span class="sxs-lookup"><span data-stu-id="92929-106">You can control in Azure AD who has access to DocuSign</span></span>
- <span data-ttu-id="92929-107">You can enable your users to automatically get signed-on to DocuSign (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="92929-107">You can enable your users to automatically get signed-on to DocuSign (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="92929-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="92929-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="92929-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="92929-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="92929-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="92929-110">Prerequisites</span></span>

<span data-ttu-id="92929-111">To configure Azure AD integration with DocuSign, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="92929-111">To configure Azure AD integration with DocuSign, you need the following items:</span></span>

- <span data-ttu-id="92929-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="92929-112">An Azure AD subscription</span></span>
- <span data-ttu-id="92929-113">A DocuSign single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="92929-113">A DocuSign single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="92929-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="92929-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="92929-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="92929-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="92929-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="92929-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="92929-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="92929-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="92929-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="92929-118">Scenario description</span></span>
<span data-ttu-id="92929-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="92929-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="92929-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="92929-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="92929-121">Adding DocuSign from the gallery</span><span class="sxs-lookup"><span data-stu-id="92929-121">Adding DocuSign from the gallery</span></span>
1. <span data-ttu-id="92929-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="92929-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-docusign-from-the-gallery"></a><span data-ttu-id="92929-123">Adding DocuSign from the gallery</span><span class="sxs-lookup"><span data-stu-id="92929-123">Adding DocuSign from the gallery</span></span>
<span data-ttu-id="92929-124">To configure the integration of DocuSign into Azure AD, you need to add DocuSign from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="92929-124">To configure the integration of DocuSign into Azure AD, you need to add DocuSign from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="92929-125">**To add DocuSign from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="92929-125">**To add DocuSign from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="92929-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="92929-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="92929-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="92929-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="92929-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="92929-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="92929-131">Click **New application** button on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="92929-131">Click **New application** button on the top of the dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="92929-133">In the search box, type **DocuSign**.</span><span class="sxs-lookup"><span data-stu-id="92929-133">In the search box, type **DocuSign**.</span></span>

    ![Creating an Azure AD test user](./media/docusign-tutorial/tutorial_docusign_search.png)

1. <span data-ttu-id="92929-135">In the results panel, select **DocuSign**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="92929-135">In the results panel, select **DocuSign**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/docusign-tutorial/tutorial_docusign_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="92929-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="92929-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="92929-138">In this section, you configure and test Azure AD single sign-on with DocuSign based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="92929-138">In this section, you configure and test Azure AD single sign-on with DocuSign based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="92929-139">For single sign-on to work, Azure AD needs to know what the counterpart user in DocuSign is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="92929-139">For single sign-on to work, Azure AD needs to know what the counterpart user in DocuSign is to a user in Azure AD.</span></span> <span data-ttu-id="92929-140">In other words, a link relationship between an Azure AD user and the related user in DocuSign needs to be established.</span><span class="sxs-lookup"><span data-stu-id="92929-140">In other words, a link relationship between an Azure AD user and the related user in DocuSign needs to be established.</span></span>

<span data-ttu-id="92929-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in DocuSign.</span><span class="sxs-lookup"><span data-stu-id="92929-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in DocuSign.</span></span>

<span data-ttu-id="92929-142">To configure and test Azure AD single sign-on with DocuSign, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="92929-142">To configure and test Azure AD single sign-on with DocuSign, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="92929-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="92929-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="92929-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="92929-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="92929-145">**[Creating a DocuSign test user](#creating-a-docusign-test-user)** - to have a counterpart of Britta Simon in DocuSign that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="92929-145">**[Creating a DocuSign test user](#creating-a-docusign-test-user)** - to have a counterpart of Britta Simon in DocuSign that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="92929-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="92929-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="92929-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="92929-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="92929-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="92929-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="92929-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your DocuSign application.</span><span class="sxs-lookup"><span data-stu-id="92929-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your DocuSign application.</span></span>

<span data-ttu-id="92929-150">**To configure Azure AD single sign-on with DocuSign, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="92929-150">**To configure Azure AD single sign-on with DocuSign, perform the following steps:**</span></span>

1. <span data-ttu-id="92929-151">In the Azure portal, on the **DocuSign** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="92929-151">In the Azure portal, on the **DocuSign** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="92929-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="92929-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/docusign-tutorial/tutorial_docusign_samlbase.png)

1. <span data-ttu-id="92929-155">On the **SAML Signing Certificate** section, click **Certificate(Base 64)** and then save certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="92929-155">On the **SAML Signing Certificate** section, click **Certificate(Base 64)** and then save certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/docusign-tutorial/tutorial_docusign_certificate.png) 

1. <span data-ttu-id="92929-157">On the **DocuSign Configuration** section of Azure portal, Click **Configure DocuSign** to open Configure sign-on window.</span><span class="sxs-lookup"><span data-stu-id="92929-157">On the **DocuSign Configuration** section of Azure portal, Click **Configure DocuSign** to open Configure sign-on window.</span></span> <span data-ttu-id="92929-158">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="92929-158">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>
    
    ![Configure Single Sign-On](./media/docusign-tutorial/tutorial_docusign_configure.png)

1. <span data-ttu-id="92929-160">In a different web browser window, login to your **DocuSign admin portal** as an administrator.</span><span class="sxs-lookup"><span data-stu-id="92929-160">In a different web browser window, login to your **DocuSign admin portal** as an administrator.</span></span>

1. <span data-ttu-id="92929-161">In the navigation menu on the left, click **Domains**.</span><span class="sxs-lookup"><span data-stu-id="92929-161">In the navigation menu on the left, click **Domains**.</span></span>
   
    ![Configuring single sign-on][51]

1. <span data-ttu-id="92929-163">On the right pane, click **Claim Domain**.</span><span class="sxs-lookup"><span data-stu-id="92929-163">On the right pane, click **Claim Domain**.</span></span>
   
    ![Configuring single sign-on][52]

1. <span data-ttu-id="92929-165">On the **Claim a domain** dialog, in the **Domain Name** textbox, type your company domain, and then click **Claim**.</span><span class="sxs-lookup"><span data-stu-id="92929-165">On the **Claim a domain** dialog, in the **Domain Name** textbox, type your company domain, and then click **Claim**.</span></span> <span data-ttu-id="92929-166">Make sure that you verify the domain and the status is active.</span><span class="sxs-lookup"><span data-stu-id="92929-166">Make sure that you verify the domain and the status is active.</span></span>
   
    ![Configuring single sign-on][53]

1. <span data-ttu-id="92929-168">In menu on the left side, click **Identity Providers**</span><span class="sxs-lookup"><span data-stu-id="92929-168">In menu on the left side, click **Identity Providers**</span></span>  
   
    ![Configuring single sign-on][54]
1. <span data-ttu-id="92929-170">In the right pane, click **Add Identity Provider**.</span><span class="sxs-lookup"><span data-stu-id="92929-170">In the right pane, click **Add Identity Provider**.</span></span> 
   
    ![Configuring single sign-on][55]

1. <span data-ttu-id="92929-172">On the **Identity Provider Settings** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="92929-172">On the **Identity Provider Settings** page, perform the following steps:</span></span>
   
    ![Configuring single sign-on][56]

    <span data-ttu-id="92929-174">a.</span><span class="sxs-lookup"><span data-stu-id="92929-174">a.</span></span> <span data-ttu-id="92929-175">In the **Name** textbox, type a unique name for your configuration.</span><span class="sxs-lookup"><span data-stu-id="92929-175">In the **Name** textbox, type a unique name for your configuration.</span></span> <span data-ttu-id="92929-176">Do not use spaces.</span><span class="sxs-lookup"><span data-stu-id="92929-176">Do not use spaces.</span></span>

    <span data-ttu-id="92929-177">b.</span><span class="sxs-lookup"><span data-stu-id="92929-177">b.</span></span> <span data-ttu-id="92929-178">Paste **SAML Entity ID** into the **Identity Provider Issuer** textbox.</span><span class="sxs-lookup"><span data-stu-id="92929-178">Paste **SAML Entity ID** into the **Identity Provider Issuer** textbox.</span></span>

    <span data-ttu-id="92929-179">c.</span><span class="sxs-lookup"><span data-stu-id="92929-179">c.</span></span> <span data-ttu-id="92929-180">Paste **SAML Single Sign-On Service URL** into the **Identity Provider Login URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="92929-180">Paste **SAML Single Sign-On Service URL** into the **Identity Provider Login URL** textbox.</span></span>

    <span data-ttu-id="92929-181">d.</span><span class="sxs-lookup"><span data-stu-id="92929-181">d.</span></span> <span data-ttu-id="92929-182">Paste **Sign-Out URL** into the **Identity Provider Logout URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="92929-182">Paste **Sign-Out URL** into the **Identity Provider Logout URL** textbox.</span></span>

    <span data-ttu-id="92929-183">e.</span><span class="sxs-lookup"><span data-stu-id="92929-183">e.</span></span> <span data-ttu-id="92929-184">Select **Sign AuthN Request**.</span><span class="sxs-lookup"><span data-stu-id="92929-184">Select **Sign AuthN Request**.</span></span>

    <span data-ttu-id="92929-185">f.</span><span class="sxs-lookup"><span data-stu-id="92929-185">f.</span></span> <span data-ttu-id="92929-186">As **Send AuthN request by**, select **POST**.</span><span class="sxs-lookup"><span data-stu-id="92929-186">As **Send AuthN request by**, select **POST**.</span></span>

    <span data-ttu-id="92929-187">g.</span><span class="sxs-lookup"><span data-stu-id="92929-187">g.</span></span> <span data-ttu-id="92929-188">As **Send logout request by**, select **GET**.</span><span class="sxs-lookup"><span data-stu-id="92929-188">As **Send logout request by**, select **GET**.</span></span>

1. <span data-ttu-id="92929-189">In the **Custom Attribute Mapping** section, choose the field you want to map with Azure AD Claim.</span><span class="sxs-lookup"><span data-stu-id="92929-189">In the **Custom Attribute Mapping** section, choose the field you want to map with Azure AD Claim.</span></span> <span data-ttu-id="92929-190">In this example, the **emailaddress** claim is mapped with the value of **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="92929-190">In this example, the **emailaddress** claim is mapped with the value of **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span> <span data-ttu-id="92929-191">It is the default claim name from Azure AD for email claim.</span><span class="sxs-lookup"><span data-stu-id="92929-191">It is the default claim name from Azure AD for email claim.</span></span> 
   
    > [!NOTE]
    > <span data-ttu-id="92929-192">Use the appropriate **User identifier** to map the user from Azure AD to DocuSign user mapping.</span><span class="sxs-lookup"><span data-stu-id="92929-192">Use the appropriate **User identifier** to map the user from Azure AD to DocuSign user mapping.</span></span> <span data-ttu-id="92929-193">Select the proper Field and enter the appropriate value based on your organization settings.</span><span class="sxs-lookup"><span data-stu-id="92929-193">Select the proper Field and enter the appropriate value based on your organization settings.</span></span>
          
    ![Configuring single sign-on][57]

1. <span data-ttu-id="92929-195">In the **Identity Provider Certificate** section, click **Add Certificate**, and then upload the certificate you have downloaded from Azure AD portal.</span><span class="sxs-lookup"><span data-stu-id="92929-195">In the **Identity Provider Certificate** section, click **Add Certificate**, and then upload the certificate you have downloaded from Azure AD portal.</span></span>   
   
    ![Configuring single sign-on][58]

1. <span data-ttu-id="92929-197">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="92929-197">Click **Save**.</span></span>

1. <span data-ttu-id="92929-198">In the **Identity Providers** section, click **Actions**, and then click **Endpoints**.</span><span class="sxs-lookup"><span data-stu-id="92929-198">In the **Identity Providers** section, click **Actions**, and then click **Endpoints**.</span></span>   
   
    ![Configuring single sign-on][59]
 
1. <span data-ttu-id="92929-200">In the **View SAML 2.0 Endpoints** section on **DocuSign admin portal**, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="92929-200">In the **View SAML 2.0 Endpoints** section on **DocuSign admin portal**, perform the following steps:</span></span>
   
    ![Configuring single sign-on][60]
   
    <span data-ttu-id="92929-202">a.</span><span class="sxs-lookup"><span data-stu-id="92929-202">a.</span></span> <span data-ttu-id="92929-203">Copy the **Service Provider Issuer URL**, and then paste into the **Identifier** textbox on **DocuSign Domain and URLs** section of the Azure portal following the pattern: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/login/sp/<uniqueID>`.</span><span class="sxs-lookup"><span data-stu-id="92929-203">Copy the **Service Provider Issuer URL**, and then paste into the **Identifier** textbox on **DocuSign Domain and URLs** section of the Azure portal following the pattern: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/login/sp/<uniqueID>`.</span></span>
   
    <span data-ttu-id="92929-204">b.</span><span class="sxs-lookup"><span data-stu-id="92929-204">b.</span></span> <span data-ttu-id="92929-205">Copy the **Service Provider Login URL**, and then paste into the **Sign On URL** textbox on **DocuSign Domain and URLs** section of the Azure portal following the pattern: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/`.</span><span class="sxs-lookup"><span data-stu-id="92929-205">Copy the **Service Provider Login URL**, and then paste into the **Sign On URL** textbox on **DocuSign Domain and URLs** section of the Azure portal following the pattern: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/`.</span></span>

    ![Configure Single Sign-On](./media/docusign-tutorial/tutorial_docusign_url.png)
      
    <span data-ttu-id="92929-207">c.</span><span class="sxs-lookup"><span data-stu-id="92929-207">c.</span></span>  <span data-ttu-id="92929-208">Click **Close**</span><span class="sxs-lookup"><span data-stu-id="92929-208">Click **Close**</span></span>
    
1. <span data-ttu-id="92929-209">On the Azure portal, click **Save**.</span><span class="sxs-lookup"><span data-stu-id="92929-209">On the Azure portal, click **Save**.</span></span>
    
    ![Configure Single Sign-On](./media/docusign-tutorial/tutorial_general_400.png)

> [!TIP]
> <span data-ttu-id="92929-211">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="92929-211">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="92929-212">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="92929-212">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="92929-213">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="92929-213">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="92929-214">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="92929-214">Creating an Azure AD test user</span></span>
<span data-ttu-id="92929-215">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="92929-215">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="92929-217">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="92929-217">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="92929-218">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="92929-218">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/docusign-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="92929-220">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="92929-220">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/docusign-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="92929-222">At the top of the dialog, click **Add** to open the **User** dialog.</span><span class="sxs-lookup"><span data-stu-id="92929-222">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/docusign-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="92929-224">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="92929-224">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/docusign-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="92929-226">a.</span><span class="sxs-lookup"><span data-stu-id="92929-226">a.</span></span> <span data-ttu-id="92929-227">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="92929-227">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="92929-228">b.</span><span class="sxs-lookup"><span data-stu-id="92929-228">b.</span></span> <span data-ttu-id="92929-229">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="92929-229">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="92929-230">c.</span><span class="sxs-lookup"><span data-stu-id="92929-230">c.</span></span> <span data-ttu-id="92929-231">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="92929-231">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="92929-232">d.</span><span class="sxs-lookup"><span data-stu-id="92929-232">d.</span></span> <span data-ttu-id="92929-233">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="92929-233">Click **Create**.</span></span>
 
### <a name="creating-a-docusign-test-user"></a><span data-ttu-id="92929-234">Creating a DocuSign test user</span><span class="sxs-lookup"><span data-stu-id="92929-234">Creating a DocuSign test user</span></span>

<span data-ttu-id="92929-235">Application supports **Just in time user provisioning** and after authentication users are created in the application automatically.</span><span class="sxs-lookup"><span data-stu-id="92929-235">Application supports **Just in time user provisioning** and after authentication users are created in the application automatically.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="92929-236">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="92929-236">Assigning the Azure AD test user</span></span>

<span data-ttu-id="92929-237">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to DocuSign.</span><span class="sxs-lookup"><span data-stu-id="92929-237">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to DocuSign.</span></span>

![Assign User][200] 

<span data-ttu-id="92929-239">**To assign Britta Simon to DocuSign, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="92929-239">**To assign Britta Simon to DocuSign, perform the following steps:**</span></span>

1. <span data-ttu-id="92929-240">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="92929-240">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="92929-242">In the applications list, select **DocuSign**.</span><span class="sxs-lookup"><span data-stu-id="92929-242">In the applications list, select **DocuSign**.</span></span>

    ![Configure Single Sign-On](./media/docusign-tutorial/tutorial_docusign_app.png) 

1. <span data-ttu-id="92929-244">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="92929-244">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="92929-246">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="92929-246">Click **Add** button.</span></span> <span data-ttu-id="92929-247">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="92929-247">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="92929-249">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="92929-249">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="92929-250">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="92929-250">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="92929-251">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="92929-251">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="92929-252">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="92929-252">Testing single sign-on</span></span>

<span data-ttu-id="92929-253">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="92929-253">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="92929-254">When you click the DocuSign tile in the Access Panel, you should get automatically signed-on to your DocuSign application.</span><span class="sxs-lookup"><span data-stu-id="92929-254">When you click the DocuSign tile in the Access Panel, you should get automatically signed-on to your DocuSign application.</span></span>
<span data-ttu-id="92929-255">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="92929-255">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="92929-256">Additional resources</span><span class="sxs-lookup"><span data-stu-id="92929-256">Additional resources</span></span>

* [<span data-ttu-id="92929-257">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="92929-257">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="92929-258">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="92929-258">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)
* [<span data-ttu-id="92929-259">Configure User Provisioning</span><span class="sxs-lookup"><span data-stu-id="92929-259">Configure User Provisioning</span></span>](docusign-provisioning-tutorial.md)


<!--Image references-->

[1]: ./media/docusign-tutorial/tutorial_general_01.png
[2]: ./media/docusign-tutorial/tutorial_general_02.png
[3]: ./media/docusign-tutorial/tutorial_general_03.png
[4]: ./media/docusign-tutorial/tutorial_general_04.png
[51]: ./media/docusign-tutorial/tutorial_docusign_21.png
[52]: ./media/docusign-tutorial/tutorial_docusign_22.png
[53]: ./media/docusign-tutorial/tutorial_docusign_23.png
[54]: ./media/docusign-tutorial/tutorial_docusign_19.png
[55]: ./media/docusign-tutorial/tutorial_docusign_20.png
[56]: ./media/docusign-tutorial/tutorial_docusign_24.png
[57]: ./media/docusign-tutorial/tutorial_docusign_25.png
[58]: ./media/docusign-tutorial/tutorial_docusign_26.png
[59]: ./media/docusign-tutorial/tutorial_docusign_27.png
[60]: ./media/docusign-tutorial/tutorial_docusign_28.png
[61]: ./media/docusign-tutorial/tutorial_docusign_29.png
[100]: ./media/docusign-tutorial/tutorial_general_100.png

[200]: ./media/docusign-tutorial/tutorial_general_200.png
[201]: ./media/docusign-tutorial/tutorial_general_201.png
[202]: ./media/docusign-tutorial/tutorial_general_202.png
[203]: ./media/docusign-tutorial/tutorial_general_203.png

