---
title: 'Tutorial: Azure Active Directory integration with 4me | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and 4me.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 983eecc6-41f8-49b7-b7f6-dcf833dde121
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2018
ms.author: jeedes
ms.openlocfilehash: c9134ceebca696ed2b3376a69e26c2ea06f4f0f6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870886"
---
# <a name="tutorial-azure-active-directory-integration-with-4me"></a><span data-ttu-id="1b274-103">Tutorial: Azure Active Directory integration with 4me</span><span class="sxs-lookup"><span data-stu-id="1b274-103">Tutorial: Azure Active Directory integration with 4me</span></span>

<span data-ttu-id="1b274-104">In this tutorial, you learn how to integrate 4me with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1b274-104">In this tutorial, you learn how to integrate 4me with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1b274-105">Integrating 4me with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="1b274-105">Integrating 4me with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1b274-106">You can control in Azure AD who has access to 4me.</span><span class="sxs-lookup"><span data-stu-id="1b274-106">You can control in Azure AD who has access to 4me.</span></span>
- <span data-ttu-id="1b274-107">You can enable your users to automatically get signed-on to 4me (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="1b274-107">You can enable your users to automatically get signed-on to 4me (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="1b274-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="1b274-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="1b274-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="1b274-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1b274-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="1b274-110">Prerequisites</span></span>

<span data-ttu-id="1b274-111">To configure Azure AD integration with 4me, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="1b274-111">To configure Azure AD integration with 4me, you need the following items:</span></span>

- <span data-ttu-id="1b274-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="1b274-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1b274-113">A 4me single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="1b274-113">A 4me single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1b274-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="1b274-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1b274-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="1b274-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1b274-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="1b274-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1b274-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1b274-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1b274-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="1b274-118">Scenario description</span></span>
<span data-ttu-id="1b274-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="1b274-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1b274-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="1b274-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1b274-121">Adding 4me from the gallery</span><span class="sxs-lookup"><span data-stu-id="1b274-121">Adding 4me from the gallery</span></span>
2. <span data-ttu-id="1b274-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="1b274-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-4me-from-the-gallery"></a><span data-ttu-id="1b274-123">Adding 4me from the gallery</span><span class="sxs-lookup"><span data-stu-id="1b274-123">Adding 4me from the gallery</span></span>
<span data-ttu-id="1b274-124">To configure the integration of 4me into Azure AD, you need to add 4me from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="1b274-124">To configure the integration of 4me into Azure AD, you need to add 4me from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1b274-125">**To add 4me from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1b274-125">**To add 4me from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1b274-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="1b274-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

2. <span data-ttu-id="1b274-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="1b274-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1b274-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="1b274-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
3. <span data-ttu-id="1b274-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="1b274-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

4. <span data-ttu-id="1b274-133">In the search box, type **4me**, select **4me** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="1b274-133">In the search box, type **4me**, select **4me** from result panel then click **Add** button to add the application.</span></span>

    ![4me in the results list](./media/4me-tutorial/tutorial_4me_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="1b274-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="1b274-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="1b274-136">In this section, you configure and test Azure AD single sign-on with 4me based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="1b274-136">In this section, you configure and test Azure AD single sign-on with 4me based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1b274-137">For single sign-on to work, Azure AD needs to know what the counterpart user in 4me is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1b274-137">For single sign-on to work, Azure AD needs to know what the counterpart user in 4me is to a user in Azure AD.</span></span> <span data-ttu-id="1b274-138">In other words, a link relationship between an Azure AD user and the related user in 4me needs to be established.</span><span class="sxs-lookup"><span data-stu-id="1b274-138">In other words, a link relationship between an Azure AD user and the related user in 4me needs to be established.</span></span>

<span data-ttu-id="1b274-139">To configure and test Azure AD single sign-on with 4me, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="1b274-139">To configure and test Azure AD single sign-on with 4me, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1b274-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="1b274-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1b274-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1b274-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1b274-142">**[Create a 4me test user](#create-a-4me-test-user)** - to have a counterpart of Britta Simon in 4me that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="1b274-142">**[Create a 4me test user](#create-a-4me-test-user)** - to have a counterpart of Britta Simon in 4me that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="1b274-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="1b274-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1b274-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="1b274-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="1b274-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="1b274-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="1b274-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your 4me application.</span><span class="sxs-lookup"><span data-stu-id="1b274-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your 4me application.</span></span>

<span data-ttu-id="1b274-147">**To configure Azure AD single sign-on with 4me, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1b274-147">**To configure Azure AD single sign-on with 4me, perform the following steps:**</span></span>

1. <span data-ttu-id="1b274-148">In the Azure portal, on the **4me** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="1b274-148">In the Azure portal, on the **4me** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

2. <span data-ttu-id="1b274-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="1b274-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/4me-tutorial/tutorial_4me_samlbase.png)

3. <span data-ttu-id="1b274-152">On the **4me Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1b274-152">On the **4me Domain and URLs** section, perform the following steps:</span></span>

    ![4me Domain and URLs single sign-on information](./media/4me-tutorial/tutorial_4me_url.png)

    <span data-ttu-id="1b274-154">a.</span><span class="sxs-lookup"><span data-stu-id="1b274-154">a.</span></span> <span data-ttu-id="1b274-155">In the **Sign-on URL** textbox, type a URL using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="1b274-155">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span>

    | <span data-ttu-id="1b274-156">Environment</span><span class="sxs-lookup"><span data-stu-id="1b274-156">Environment</span></span>| <span data-ttu-id="1b274-157">URL</span><span class="sxs-lookup"><span data-stu-id="1b274-157">URL</span></span>|
    |---|---|
    | <span data-ttu-id="1b274-158">PRODUCTION</span><span class="sxs-lookup"><span data-stu-id="1b274-158">PRODUCTION</span></span> | `https://<SUBDOMAIN>.4me.com`|
    | <span data-ttu-id="1b274-159">QA</span><span class="sxs-lookup"><span data-stu-id="1b274-159">QA</span></span>| `https://<SUBDOMAIN>.4me.qa`|
  
    <span data-ttu-id="1b274-160">b.</span><span class="sxs-lookup"><span data-stu-id="1b274-160">b.</span></span> <span data-ttu-id="1b274-161">In the **Identifier** textbox, type a URL using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="1b274-161">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    
    | <span data-ttu-id="1b274-162">Environment</span><span class="sxs-lookup"><span data-stu-id="1b274-162">Environment</span></span>| <span data-ttu-id="1b274-163">URL</span><span class="sxs-lookup"><span data-stu-id="1b274-163">URL</span></span>|
    |---|---|
    | <span data-ttu-id="1b274-164">PRODUCTION</span><span class="sxs-lookup"><span data-stu-id="1b274-164">PRODUCTION</span></span> | `https://<SUBDOMAIN>.4me.com`|
    | <span data-ttu-id="1b274-165">QA</span><span class="sxs-lookup"><span data-stu-id="1b274-165">QA</span></span>| `https://<SUBDOMAIN>.4me.qa`|

    > [!NOTE] 
    > <span data-ttu-id="1b274-166">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="1b274-166">These values are not real.</span></span> <span data-ttu-id="1b274-167">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="1b274-167">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="1b274-168">Contact [4me Client support team](mailto:support@4me.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="1b274-168">Contact [4me Client support team](mailto:support@4me.com) to get these values.</span></span> 
 
4. <span data-ttu-id="1b274-169">4me application expects the SAML assertions in a specific format.</span><span class="sxs-lookup"><span data-stu-id="1b274-169">4me application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="1b274-170">Configure the following claims for this application.</span><span class="sxs-lookup"><span data-stu-id="1b274-170">Configure the following claims for this application.</span></span> <span data-ttu-id="1b274-171">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span><span class="sxs-lookup"><span data-stu-id="1b274-171">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span></span> <span data-ttu-id="1b274-172">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="1b274-172">The following screenshot shows an example for this.</span></span>
    
    ![Configure Single Sign-On](./media/4me-tutorial/tutorial_4me_attribute.png)

5. <span data-ttu-id="1b274-174">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1b274-174">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="1b274-175">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="1b274-175">Attribute Name</span></span> | <span data-ttu-id="1b274-176">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="1b274-176">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="1b274-177">first_name</span><span class="sxs-lookup"><span data-stu-id="1b274-177">first_name</span></span> | <span data-ttu-id="1b274-178">user.givenname</span><span class="sxs-lookup"><span data-stu-id="1b274-178">user.givenname</span></span> |
    | <span data-ttu-id="1b274-179">last_name</span><span class="sxs-lookup"><span data-stu-id="1b274-179">last_name</span></span> | <span data-ttu-id="1b274-180">user.surname</span><span class="sxs-lookup"><span data-stu-id="1b274-180">user.surname</span></span> |

    <span data-ttu-id="1b274-181">a.</span><span class="sxs-lookup"><span data-stu-id="1b274-181">a.</span></span> <span data-ttu-id="1b274-182">Click **Add attribute** to open the **Add Attribute** dialog.</span><span class="sxs-lookup"><span data-stu-id="1b274-182">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configure Single Sign-On](./media/4me-tutorial/tutorial_attribute_04.png)

    ![Configure Single Sign-On](./media/4me-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="1b274-185">b.</span><span class="sxs-lookup"><span data-stu-id="1b274-185">b.</span></span> <span data-ttu-id="1b274-186">In the **Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="1b274-186">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="1b274-187">c.</span><span class="sxs-lookup"><span data-stu-id="1b274-187">c.</span></span> <span data-ttu-id="1b274-188">From the **Value** list, type the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="1b274-188">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="1b274-189">d.</span><span class="sxs-lookup"><span data-stu-id="1b274-189">d.</span></span> <span data-ttu-id="1b274-190">Leave the **Namespace** blank.</span><span class="sxs-lookup"><span data-stu-id="1b274-190">Leave the **Namespace** blank.</span></span>
    
    <span data-ttu-id="1b274-191">d.</span><span class="sxs-lookup"><span data-stu-id="1b274-191">d.</span></span> <span data-ttu-id="1b274-192">Click **Ok**</span><span class="sxs-lookup"><span data-stu-id="1b274-192">Click **Ok**</span></span>

6. <span data-ttu-id="1b274-193">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value on your computer.</span><span class="sxs-lookup"><span data-stu-id="1b274-193">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value on your computer.</span></span>

    ![The Certificate download link](./media/4me-tutorial/tutorial_4me_certificate.png) 

7. <span data-ttu-id="1b274-195">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="1b274-195">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/4me-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="1b274-197">On the **4me Configuration** section, click **Configure 4me** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="1b274-197">On the **4me Configuration** section, click **Configure 4me** to open **Configure sign-on** window.</span></span> <span data-ttu-id="1b274-198">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="1b274-198">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![4me Configuration](./media/4me-tutorial/tutorial_4me_configure.png) 

9. <span data-ttu-id="1b274-200">In a different web browser window, login to 4me as an Administrator.</span><span class="sxs-lookup"><span data-stu-id="1b274-200">In a different web browser window, login to 4me as an Administrator.</span></span>

10. <span data-ttu-id="1b274-201">On the top left, click on **Settings** logo and on the left side bar click **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="1b274-201">On the top left, click on **Settings** logo and on the left side bar click **Single Sign-On**.</span></span>

    ![4me settings](./media/4me-tutorial/tutorial_4me_settings.png)

11. <span data-ttu-id="1b274-203">On the **Single Sign-On** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1b274-203">On the **Single Sign-On** page, perform the following steps:</span></span>

    ![4me singleasignon](./media/4me-tutorial/tutorial_4me_singlesignon.png)

    <span data-ttu-id="1b274-205">a.</span><span class="sxs-lookup"><span data-stu-id="1b274-205">a.</span></span> <span data-ttu-id="1b274-206">Select the **Enabled** option.</span><span class="sxs-lookup"><span data-stu-id="1b274-206">Select the **Enabled** option.</span></span>

    <span data-ttu-id="1b274-207">b.</span><span class="sxs-lookup"><span data-stu-id="1b274-207">b.</span></span> <span data-ttu-id="1b274-208">In the **Remote logout URL** textbox, paste the value of **Sign-Out URL**, which you have copied from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="1b274-208">In the **Remote logout URL** textbox, paste the value of **Sign-Out URL**, which you have copied from the Azure portal.</span></span>

    <span data-ttu-id="1b274-209">c.</span><span class="sxs-lookup"><span data-stu-id="1b274-209">c.</span></span> <span data-ttu-id="1b274-210">Under **SAML** section, in the **SAML SSO URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="1b274-210">Under **SAML** section, in the **SAML SSO URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from the Azure portal.</span></span>

    <span data-ttu-id="1b274-211">d.</span><span class="sxs-lookup"><span data-stu-id="1b274-211">d.</span></span> <span data-ttu-id="1b274-212">In the **Certificate fingerprint** textbox, paste the **THUMBPRINT** value seperated by a colon in duplets order (AA:BB:CC:DD:EE:FF:GG:HH:II), which you have copied from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="1b274-212">In the **Certificate fingerprint** textbox, paste the **THUMBPRINT** value seperated by a colon in duplets order (AA:BB:CC:DD:EE:FF:GG:HH:II), which you have copied from the Azure portal.</span></span>

    <span data-ttu-id="1b274-213">e.</span><span class="sxs-lookup"><span data-stu-id="1b274-213">e.</span></span> <span data-ttu-id="1b274-214">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="1b274-214">Click **Save**.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="1b274-215">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="1b274-215">Create an Azure AD test user</span></span>

<span data-ttu-id="1b274-216">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1b274-216">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="1b274-218">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1b274-218">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1b274-219">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="1b274-219">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/4me-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="1b274-221">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="1b274-221">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/4me-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="1b274-223">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="1b274-223">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/4me-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="1b274-225">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1b274-225">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/4me-tutorial/create_aaduser_04.png)

    <span data-ttu-id="1b274-227">a.</span><span class="sxs-lookup"><span data-stu-id="1b274-227">a.</span></span> <span data-ttu-id="1b274-228">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1b274-228">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1b274-229">b.</span><span class="sxs-lookup"><span data-stu-id="1b274-229">b.</span></span> <span data-ttu-id="1b274-230">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1b274-230">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="1b274-231">c.</span><span class="sxs-lookup"><span data-stu-id="1b274-231">c.</span></span> <span data-ttu-id="1b274-232">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="1b274-232">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="1b274-233">d.</span><span class="sxs-lookup"><span data-stu-id="1b274-233">d.</span></span> <span data-ttu-id="1b274-234">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="1b274-234">Click **Create**.</span></span>
 
### <a name="create-a-4me-test-user"></a><span data-ttu-id="1b274-235">Create a 4me test user</span><span class="sxs-lookup"><span data-stu-id="1b274-235">Create a 4me test user</span></span>

<span data-ttu-id="1b274-236">The objective of this section is to create a user called Britta Simon in 4me.</span><span class="sxs-lookup"><span data-stu-id="1b274-236">The objective of this section is to create a user called Britta Simon in 4me.</span></span> <span data-ttu-id="1b274-237">4me supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="1b274-237">4me supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="1b274-238">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="1b274-238">There is no action item for you in this section.</span></span> <span data-ttu-id="1b274-239">A new user is created during an attempt to access 4me if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="1b274-239">A new user is created during an attempt to access 4me if it doesn't exist yet.</span></span>

>[!Note]
><span data-ttu-id="1b274-240">If you need to create a user manually, contact [4me support team](mailto:support@4me.com).</span><span class="sxs-lookup"><span data-stu-id="1b274-240">If you need to create a user manually, contact [4me support team](mailto:support@4me.com).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="1b274-241">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="1b274-241">Assign the Azure AD test user</span></span>

<span data-ttu-id="1b274-242">In this section, you enable Britta Simon to use Azure single sign-on by granting access to 4me.</span><span class="sxs-lookup"><span data-stu-id="1b274-242">In this section, you enable Britta Simon to use Azure single sign-on by granting access to 4me.</span></span>

![Assign the user role][200] 

<span data-ttu-id="1b274-244">**To assign Britta Simon to 4me, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1b274-244">**To assign Britta Simon to 4me, perform the following steps:**</span></span>

1. <span data-ttu-id="1b274-245">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="1b274-245">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="1b274-247">In the applications list, select **4me**.</span><span class="sxs-lookup"><span data-stu-id="1b274-247">In the applications list, select **4me**.</span></span>

    ![The 4me link in the Applications list](./media/4me-tutorial/tutorial_4me_app.png)  

3. <span data-ttu-id="1b274-249">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="1b274-249">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

4. <span data-ttu-id="1b274-251">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="1b274-251">Click **Add** button.</span></span> <span data-ttu-id="1b274-252">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="1b274-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

5. <span data-ttu-id="1b274-254">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="1b274-254">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1b274-255">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="1b274-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1b274-256">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="1b274-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="1b274-257">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="1b274-257">Test single sign-on</span></span>

<span data-ttu-id="1b274-258">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="1b274-258">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="1b274-259">When you click the 4me tile in the Access Panel, you should get automatically signed-on to your 4me application.</span><span class="sxs-lookup"><span data-stu-id="1b274-259">When you click the 4me tile in the Access Panel, you should get automatically signed-on to your 4me application.</span></span>
<span data-ttu-id="1b274-260">For more information about the Access Panel, see [Introduction to the Access Panel](../active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1b274-260">For more information about the Access Panel, see [Introduction to the Access Panel](../active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="1b274-261">Additional resources</span><span class="sxs-lookup"><span data-stu-id="1b274-261">Additional resources</span></span>

* [<span data-ttu-id="1b274-262">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1b274-262">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="1b274-263">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1b274-263">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/4me-tutorial/tutorial_general_01.png
[2]: ./media/4me-tutorial/tutorial_general_02.png
[3]: ./media/4me-tutorial/tutorial_general_03.png
[4]: ./media/4me-tutorial/tutorial_general_04.png

[100]: ./media/4me-tutorial/tutorial_general_100.png

[200]: ./media/4me-tutorial/tutorial_general_200.png
[201]: ./media/4me-tutorial/tutorial_general_201.png
[202]: ./media/4me-tutorial/tutorial_general_202.png
[203]: ./media/4me-tutorial/tutorial_general_203.png

