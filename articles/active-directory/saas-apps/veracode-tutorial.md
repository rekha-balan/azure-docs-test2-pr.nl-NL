---
title: 'Tutorial: Azure Active Directory integration with Veracode | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Veracode.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: 4fe78050-cb6d-4db9-96ec-58cc0779167f
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: a295885d67e674e1cef7cbeb0480b8031d405a92
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871708"
---
# <a name="tutorial-azure-active-directory-integration-with-veracode"></a><span data-ttu-id="8a488-103">Tutorial: Azure Active Directory integration with Veracode</span><span class="sxs-lookup"><span data-stu-id="8a488-103">Tutorial: Azure Active Directory integration with Veracode</span></span>

<span data-ttu-id="8a488-104">In this tutorial, you learn how to integrate Veracode with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8a488-104">In this tutorial, you learn how to integrate Veracode with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8a488-105">Integrating Veracode with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="8a488-105">Integrating Veracode with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8a488-106">You can control in Azure AD who has access to Veracode.</span><span class="sxs-lookup"><span data-stu-id="8a488-106">You can control in Azure AD who has access to Veracode.</span></span>
- <span data-ttu-id="8a488-107">You can enable your users to automatically get signed-on to Veracode (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="8a488-107">You can enable your users to automatically get signed-on to Veracode (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="8a488-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="8a488-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="8a488-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="8a488-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8a488-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="8a488-110">Prerequisites</span></span>

<span data-ttu-id="8a488-111">To configure Azure AD integration with Veracode, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="8a488-111">To configure Azure AD integration with Veracode, you need the following items:</span></span>

- <span data-ttu-id="8a488-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="8a488-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8a488-113">A Veracode single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="8a488-113">A Veracode single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8a488-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="8a488-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8a488-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="8a488-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8a488-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="8a488-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8a488-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8a488-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8a488-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="8a488-118">Scenario description</span></span>
<span data-ttu-id="8a488-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="8a488-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8a488-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="8a488-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8a488-121">Add Veracode from the gallery</span><span class="sxs-lookup"><span data-stu-id="8a488-121">Add Veracode from the gallery</span></span>
1. <span data-ttu-id="8a488-122">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="8a488-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-veracode-from-the-gallery"></a><span data-ttu-id="8a488-123">Add Veracode from the gallery</span><span class="sxs-lookup"><span data-stu-id="8a488-123">Add Veracode from the gallery</span></span>
<span data-ttu-id="8a488-124">To configure the integration of Veracode into Azure AD, you need to add Veracode from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="8a488-124">To configure the integration of Veracode into Azure AD, you need to add Veracode from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8a488-125">**To add Veracode from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8a488-125">**To add Veracode from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8a488-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="8a488-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="8a488-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="8a488-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="8a488-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="8a488-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="8a488-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="8a488-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="8a488-133">In the search box, type **Veracode**, select  **Veracode** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="8a488-133">In the search box, type **Veracode**, select  **Veracode** from result panel then click **Add** button to add the application.</span></span>

    ![Veracode in the results list](./media/veracode-tutorial/tutorial_veracode_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="8a488-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="8a488-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="8a488-136">In this section, you configure and test Azure AD single sign-on with Veracode based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="8a488-136">In this section, you configure and test Azure AD single sign-on with Veracode based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8a488-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Veracode is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8a488-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Veracode is to a user in Azure AD.</span></span> <span data-ttu-id="8a488-138">In other words, a link relationship between an Azure AD user and the related user in Veracode needs to be established.</span><span class="sxs-lookup"><span data-stu-id="8a488-138">In other words, a link relationship between an Azure AD user and the related user in Veracode needs to be established.</span></span>

<span data-ttu-id="8a488-139">In Veracode, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="8a488-139">In Veracode, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="8a488-140">To configure and test Azure AD single sign-on with Veracode, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="8a488-140">To configure and test Azure AD single sign-on with Veracode, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8a488-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="8a488-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="8a488-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8a488-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="8a488-143">**[Create a Veracode test user](#create-a-veracode-test-user)** - to have a counterpart of Britta Simon in Veracode that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="8a488-143">**[Create a Veracode test user](#create-a-veracode-test-user)** - to have a counterpart of Britta Simon in Veracode that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="8a488-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="8a488-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="8a488-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="8a488-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="8a488-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="8a488-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="8a488-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Veracode application.</span><span class="sxs-lookup"><span data-stu-id="8a488-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Veracode application.</span></span>

<span data-ttu-id="8a488-148">**To configure Azure AD single sign-on with Veracode, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8a488-148">**To configure Azure AD single sign-on with Veracode, perform the following steps:**</span></span>

1. <span data-ttu-id="8a488-149">In the Azure portal, on the **Veracode** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="8a488-149">In the Azure portal, on the **Veracode** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="8a488-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="8a488-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/veracode-tutorial/tutorial_veracode_samlbase.png)

1. <span data-ttu-id="8a488-153">On the **Veracode Domain and URLs** section, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span><span class="sxs-lookup"><span data-stu-id="8a488-153">On the **Veracode Domain and URLs** section, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span></span> 

    ![Configure Single Sign-On](./media/veracode-tutorial/tutorial_veracode_url.png)

1. <span data-ttu-id="8a488-155">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="8a488-155">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/veracode-tutorial/tutorial_veracode_certificate.png) 

1. <span data-ttu-id="8a488-157">The objective of this section is to outline how to enable users to authenticate to Veracode with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="8a488-157">The objective of this section is to outline how to enable users to authenticate to Veracode with their account in Azure AD using federation based on the SAML protocol.</span></span>

    <span data-ttu-id="8a488-158">Your Veracode application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **saml token attributes** configuration.</span><span class="sxs-lookup"><span data-stu-id="8a488-158">Your Veracode application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **saml token attributes** configuration.</span></span> <span data-ttu-id="8a488-159">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="8a488-159">The following screenshot shows an example for this.</span></span>
    
    <span data-ttu-id="8a488-160">![Attributes](./media/veracode-tutorial/tutorial_veracode_attr.png "Attributes")</span><span class="sxs-lookup"><span data-stu-id="8a488-160">![Attributes](./media/veracode-tutorial/tutorial_veracode_attr.png "Attributes")</span></span>

1. <span data-ttu-id="8a488-161">To add the required attribute mappings, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8a488-161">To add the required attribute mappings, perform the following steps:</span></span>

    | <span data-ttu-id="8a488-162">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="8a488-162">Attribute Name</span></span> | <span data-ttu-id="8a488-163">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="8a488-163">Attribute Value</span></span> |
    |--- |--- |
    | <span data-ttu-id="8a488-164">firstname</span><span class="sxs-lookup"><span data-stu-id="8a488-164">firstname</span></span> |<span data-ttu-id="8a488-165">User.givenname</span><span class="sxs-lookup"><span data-stu-id="8a488-165">User.givenname</span></span> |
    | <span data-ttu-id="8a488-166">lastname</span><span class="sxs-lookup"><span data-stu-id="8a488-166">lastname</span></span> |<span data-ttu-id="8a488-167">User.surname</span><span class="sxs-lookup"><span data-stu-id="8a488-167">User.surname</span></span> |
    | <span data-ttu-id="8a488-168">email</span><span class="sxs-lookup"><span data-stu-id="8a488-168">email</span></span> |<span data-ttu-id="8a488-169">User.mail</span><span class="sxs-lookup"><span data-stu-id="8a488-169">User.mail</span></span> |
    
    <span data-ttu-id="8a488-170">a.</span><span class="sxs-lookup"><span data-stu-id="8a488-170">a.</span></span> <span data-ttu-id="8a488-171">For each data row in the table above, click **add user attribute**.</span><span class="sxs-lookup"><span data-stu-id="8a488-171">For each data row in the table above, click **add user attribute**.</span></span>
    
    <span data-ttu-id="8a488-172">![Attributes](./media/veracode-tutorial/tutorial_veracode_addattr.png "Attributes")</span><span class="sxs-lookup"><span data-stu-id="8a488-172">![Attributes](./media/veracode-tutorial/tutorial_veracode_addattr.png "Attributes")</span></span>
    
    <span data-ttu-id="8a488-173">![Attributes](./media/veracode-tutorial/tutorial_veracode_addattr1.png "Attributes")</span><span class="sxs-lookup"><span data-stu-id="8a488-173">![Attributes](./media/veracode-tutorial/tutorial_veracode_addattr1.png "Attributes")</span></span>
    
    <span data-ttu-id="8a488-174">b.</span><span class="sxs-lookup"><span data-stu-id="8a488-174">b.</span></span> <span data-ttu-id="8a488-175">In the **Attribute Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="8a488-175">In the **Attribute Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="8a488-176">c.</span><span class="sxs-lookup"><span data-stu-id="8a488-176">c.</span></span> <span data-ttu-id="8a488-177">In the **Attribute Value** textbox, select the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="8a488-177">In the **Attribute Value** textbox, select the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="8a488-178">d.</span><span class="sxs-lookup"><span data-stu-id="8a488-178">d.</span></span> <span data-ttu-id="8a488-179">Click **Ok**.</span><span class="sxs-lookup"><span data-stu-id="8a488-179">Click **Ok**.</span></span>

1. <span data-ttu-id="8a488-180">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="8a488-180">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/veracode-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="8a488-182">On the **Veracode Configuration** section, click **Configure Veracode** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="8a488-182">On the **Veracode Configuration** section, click **Configure Veracode** to open **Configure sign-on** window.</span></span> <span data-ttu-id="8a488-183">Copy the **SAML Entity ID** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="8a488-183">Copy the **SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![Veracode Configuration](./media/veracode-tutorial/tutorial_veracode_configure.png) 

1. <span data-ttu-id="8a488-185">In a different web browser window, log into your Veracode company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="8a488-185">In a different web browser window, log into your Veracode company site as an administrator.</span></span>

1. <span data-ttu-id="8a488-186">In the menu on the top, click **Settings**, and then click **Admin**.</span><span class="sxs-lookup"><span data-stu-id="8a488-186">In the menu on the top, click **Settings**, and then click **Admin**.</span></span>
   
    <span data-ttu-id="8a488-187">![Administration](./media/veracode-tutorial/ic802911.png "Administration")</span><span class="sxs-lookup"><span data-stu-id="8a488-187">![Administration](./media/veracode-tutorial/ic802911.png "Administration")</span></span>

1. <span data-ttu-id="8a488-188">Click the **SAML** tab.</span><span class="sxs-lookup"><span data-stu-id="8a488-188">Click the **SAML** tab.</span></span>

1. <span data-ttu-id="8a488-189">In the **Organization SAML Settings** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8a488-189">In the **Organization SAML Settings** section, perform the following steps:</span></span>
   
    <span data-ttu-id="8a488-190">![Administration](./media/veracode-tutorial/ic802912.png "Administration")</span><span class="sxs-lookup"><span data-stu-id="8a488-190">![Administration](./media/veracode-tutorial/ic802912.png "Administration")</span></span>
   
    <span data-ttu-id="8a488-191">a.</span><span class="sxs-lookup"><span data-stu-id="8a488-191">a.</span></span>  <span data-ttu-id="8a488-192">In  **Issuer** textbox, paste the value of  **SAML Entity ID** which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="8a488-192">In  **Issuer** textbox, paste the value of  **SAML Entity ID** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="8a488-193">b.</span><span class="sxs-lookup"><span data-stu-id="8a488-193">b.</span></span> <span data-ttu-id="8a488-194">To upload your downloaded certificate from Azure portal, click **Choose File**.</span><span class="sxs-lookup"><span data-stu-id="8a488-194">To upload your downloaded certificate from Azure portal, click **Choose File**.</span></span>
   
    <span data-ttu-id="8a488-195">c.</span><span class="sxs-lookup"><span data-stu-id="8a488-195">c.</span></span> <span data-ttu-id="8a488-196">Select **Enable Self Registration**.</span><span class="sxs-lookup"><span data-stu-id="8a488-196">Select **Enable Self Registration**.</span></span>

1. <span data-ttu-id="8a488-197">In the **Self Registration Settings** section, perform the following steps, and then click **Save**:</span><span class="sxs-lookup"><span data-stu-id="8a488-197">In the **Self Registration Settings** section, perform the following steps, and then click **Save**:</span></span>
   
    <span data-ttu-id="8a488-198">![Administration](./media/veracode-tutorial/ic802913.png "Administration")</span><span class="sxs-lookup"><span data-stu-id="8a488-198">![Administration](./media/veracode-tutorial/ic802913.png "Administration")</span></span>
   
    <span data-ttu-id="8a488-199">a.</span><span class="sxs-lookup"><span data-stu-id="8a488-199">a.</span></span> <span data-ttu-id="8a488-200">As **New User Activation**, select **No Activation Required**.</span><span class="sxs-lookup"><span data-stu-id="8a488-200">As **New User Activation**, select **No Activation Required**.</span></span>
   
    <span data-ttu-id="8a488-201">b.</span><span class="sxs-lookup"><span data-stu-id="8a488-201">b.</span></span> <span data-ttu-id="8a488-202">As **User Data Updates**, select **Preference Veracode User Data**.</span><span class="sxs-lookup"><span data-stu-id="8a488-202">As **User Data Updates**, select **Preference Veracode User Data**.</span></span>
   
    <span data-ttu-id="8a488-203">c.</span><span class="sxs-lookup"><span data-stu-id="8a488-203">c.</span></span> <span data-ttu-id="8a488-204">For **SAML Attribute Details**, select the following:</span><span class="sxs-lookup"><span data-stu-id="8a488-204">For **SAML Attribute Details**, select the following:</span></span>
      * <span data-ttu-id="8a488-205">**User Roles**</span><span class="sxs-lookup"><span data-stu-id="8a488-205">**User Roles**</span></span>
      * <span data-ttu-id="8a488-206">**Policy Administrator**</span><span class="sxs-lookup"><span data-stu-id="8a488-206">**Policy Administrator**</span></span>
      * <span data-ttu-id="8a488-207">**Reviewer**</span><span class="sxs-lookup"><span data-stu-id="8a488-207">**Reviewer**</span></span>
      * <span data-ttu-id="8a488-208">**Security Lead**</span><span class="sxs-lookup"><span data-stu-id="8a488-208">**Security Lead**</span></span>
      * <span data-ttu-id="8a488-209">**Executive**</span><span class="sxs-lookup"><span data-stu-id="8a488-209">**Executive**</span></span>
      * <span data-ttu-id="8a488-210">**Submitter**</span><span class="sxs-lookup"><span data-stu-id="8a488-210">**Submitter**</span></span>
      * <span data-ttu-id="8a488-211">**Creator**</span><span class="sxs-lookup"><span data-stu-id="8a488-211">**Creator**</span></span>
      * <span data-ttu-id="8a488-212">**All Scan Types**</span><span class="sxs-lookup"><span data-stu-id="8a488-212">**All Scan Types**</span></span>
      * <span data-ttu-id="8a488-213">**Team Memberships**</span><span class="sxs-lookup"><span data-stu-id="8a488-213">**Team Memberships**</span></span>
      * <span data-ttu-id="8a488-214">**Default Team**</span><span class="sxs-lookup"><span data-stu-id="8a488-214">**Default Team**</span></span>

> [!TIP]
> <span data-ttu-id="8a488-215">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="8a488-215">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="8a488-216">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="8a488-216">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="8a488-217">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8a488-217">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="8a488-218">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="8a488-218">Create an Azure AD test user</span></span>

<span data-ttu-id="8a488-219">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8a488-219">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="8a488-221">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8a488-221">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8a488-222">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="8a488-222">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/veracode-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="8a488-224">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="8a488-224">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/veracode-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="8a488-226">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="8a488-226">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/veracode-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="8a488-228">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8a488-228">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/veracode-tutorial/create_aaduser_04.png)

    <span data-ttu-id="8a488-230">a.</span><span class="sxs-lookup"><span data-stu-id="8a488-230">a.</span></span> <span data-ttu-id="8a488-231">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8a488-231">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8a488-232">b.</span><span class="sxs-lookup"><span data-stu-id="8a488-232">b.</span></span> <span data-ttu-id="8a488-233">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8a488-233">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="8a488-234">c.</span><span class="sxs-lookup"><span data-stu-id="8a488-234">c.</span></span> <span data-ttu-id="8a488-235">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="8a488-235">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="8a488-236">d.</span><span class="sxs-lookup"><span data-stu-id="8a488-236">d.</span></span> <span data-ttu-id="8a488-237">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="8a488-237">Click **Create**.</span></span>
 
### <a name="create-a-veracode-test-user"></a><span data-ttu-id="8a488-238">Create a Veracode test user</span><span class="sxs-lookup"><span data-stu-id="8a488-238">Create a Veracode test user</span></span>
<span data-ttu-id="8a488-239">In order to enable Azure AD users to log into Veracode, they must be provisioned into Veracode.</span><span class="sxs-lookup"><span data-stu-id="8a488-239">In order to enable Azure AD users to log into Veracode, they must be provisioned into Veracode.</span></span> <span data-ttu-id="8a488-240">In the case of Veracode, provisioning is an automated task.</span><span class="sxs-lookup"><span data-stu-id="8a488-240">In the case of Veracode, provisioning is an automated task.</span></span> <span data-ttu-id="8a488-241">There is no action item for you.</span><span class="sxs-lookup"><span data-stu-id="8a488-241">There is no action item for you.</span></span> <span data-ttu-id="8a488-242">Users are automatically created if necessary during the first single sign-on attempt.</span><span class="sxs-lookup"><span data-stu-id="8a488-242">Users are automatically created if necessary during the first single sign-on attempt.</span></span>

> [!NOTE]
> <span data-ttu-id="8a488-243">You can use any other Veracode user account creation tools or APIs provided by Veracode to provision Azure AD user accounts.</span><span class="sxs-lookup"><span data-stu-id="8a488-243">You can use any other Veracode user account creation tools or APIs provided by Veracode to provision Azure AD user accounts.</span></span>
> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="8a488-244">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="8a488-244">Assign the Azure AD test user</span></span>

<span data-ttu-id="8a488-245">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Veracode.</span><span class="sxs-lookup"><span data-stu-id="8a488-245">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Veracode.</span></span>

![Assign the user role][200] 

<span data-ttu-id="8a488-247">**To assign Britta Simon to Veracode, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8a488-247">**To assign Britta Simon to Veracode, perform the following steps:**</span></span>

1. <span data-ttu-id="8a488-248">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="8a488-248">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="8a488-250">In the applications list, select **Veracode**.</span><span class="sxs-lookup"><span data-stu-id="8a488-250">In the applications list, select **Veracode**.</span></span>

    ![The Veracode link in the Applications list](./media/veracode-tutorial/tutorial_veracode_app.png)  

1. <span data-ttu-id="8a488-252">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="8a488-252">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="8a488-254">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="8a488-254">Click **Add** button.</span></span> <span data-ttu-id="8a488-255">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="8a488-255">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="8a488-257">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="8a488-257">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="8a488-258">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="8a488-258">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="8a488-259">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="8a488-259">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="8a488-260">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="8a488-260">Test single sign-on</span></span>

<span data-ttu-id="8a488-261">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="8a488-261">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="8a488-262">When you click the Veracode tile in the Access Panel, you should get automatically signed-on to your Veracode application.</span><span class="sxs-lookup"><span data-stu-id="8a488-262">When you click the Veracode tile in the Access Panel, you should get automatically signed-on to your Veracode application.</span></span>
<span data-ttu-id="8a488-263">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8a488-263">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="8a488-264">Additional resources</span><span class="sxs-lookup"><span data-stu-id="8a488-264">Additional resources</span></span>

* [<span data-ttu-id="8a488-265">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8a488-265">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="8a488-266">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8a488-266">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/veracode-tutorial/tutorial_general_01.png
[2]: ./media/veracode-tutorial/tutorial_general_02.png
[3]: ./media/veracode-tutorial/tutorial_general_03.png
[4]: ./media/veracode-tutorial/tutorial_general_04.png

[100]: ./media/veracode-tutorial/tutorial_general_100.png

[200]: ./media/veracode-tutorial/tutorial_general_200.png
[201]: ./media/veracode-tutorial/tutorial_general_201.png
[202]: ./media/veracode-tutorial/tutorial_general_202.png
[203]: ./media/veracode-tutorial/tutorial_general_203.png

