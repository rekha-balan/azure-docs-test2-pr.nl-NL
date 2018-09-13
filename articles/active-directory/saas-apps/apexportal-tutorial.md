---
title: 'Tutorial: Azure Active Directory integration with Apex Portal | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Apex Portal.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: db204a46-6460-4ace-bdbb-4353846723ad
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2017
ms.author: jeedes
ms.openlocfilehash: 4c267313e4851e621b57aa1d2bddc73118405776
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870332"
---
# <a name="tutorial-azure-active-directory-integration-with-apex-portal"></a><span data-ttu-id="b0509-103">Tutorial: Azure Active Directory integration with Apex Portal</span><span class="sxs-lookup"><span data-stu-id="b0509-103">Tutorial: Azure Active Directory integration with Apex Portal</span></span>

<span data-ttu-id="b0509-104">In this tutorial, you learn how to integrate Apex Portal with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b0509-104">In this tutorial, you learn how to integrate Apex Portal with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b0509-105">Integrating Apex Portal with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="b0509-105">Integrating Apex Portal with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b0509-106">You can control in Azure AD who has access to Apex Portal.</span><span class="sxs-lookup"><span data-stu-id="b0509-106">You can control in Azure AD who has access to Apex Portal.</span></span>
- <span data-ttu-id="b0509-107">You can enable your users to automatically get signed-on to Apex Portal (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="b0509-107">You can enable your users to automatically get signed-on to Apex Portal (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="b0509-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="b0509-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="b0509-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="b0509-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b0509-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b0509-110">Prerequisites</span></span>

<span data-ttu-id="b0509-111">To configure Azure AD integration with Apex Portal, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="b0509-111">To configure Azure AD integration with Apex Portal, you need the following items:</span></span>

- <span data-ttu-id="b0509-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="b0509-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b0509-113">A Apex Portal single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="b0509-113">A Apex Portal single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b0509-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="b0509-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b0509-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="b0509-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b0509-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="b0509-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b0509-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b0509-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b0509-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="b0509-118">Scenario description</span></span>
<span data-ttu-id="b0509-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="b0509-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b0509-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="b0509-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b0509-121">Adding Apex Portal from the gallery</span><span class="sxs-lookup"><span data-stu-id="b0509-121">Adding Apex Portal from the gallery</span></span>
2. <span data-ttu-id="b0509-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="b0509-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-apex-portal-from-the-gallery"></a><span data-ttu-id="b0509-123">Adding Apex Portal from the gallery</span><span class="sxs-lookup"><span data-stu-id="b0509-123">Adding Apex Portal from the gallery</span></span>
<span data-ttu-id="b0509-124">To configure the integration of Apex Portal into Azure AD, you need to add Apex Portal from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="b0509-124">To configure the integration of Apex Portal into Azure AD, you need to add Apex Portal from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b0509-125">**To add Apex Portal from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b0509-125">**To add Apex Portal from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b0509-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="b0509-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

2. <span data-ttu-id="b0509-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="b0509-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b0509-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="b0509-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
3. <span data-ttu-id="b0509-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="b0509-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

4. <span data-ttu-id="b0509-133">In the search box, type **Apex Portal**, select **Apex Portal** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="b0509-133">In the search box, type **Apex Portal**, select **Apex Portal** from result panel then click **Add** button to add the application.</span></span>

    ![Apex Portal in the results list](./media/apexportal-tutorial/tutorial_apexonline_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="b0509-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="b0509-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="b0509-136">In this section, you configure and test Azure AD single sign-on with Apex Portal based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="b0509-136">In this section, you configure and test Azure AD single sign-on with Apex Portal based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b0509-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Apex Portal is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b0509-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Apex Portal is to a user in Azure AD.</span></span> <span data-ttu-id="b0509-138">In other words, a link relationship between an Azure AD user and the related user in Apex Portal needs to be established.</span><span class="sxs-lookup"><span data-stu-id="b0509-138">In other words, a link relationship between an Azure AD user and the related user in Apex Portal needs to be established.</span></span>

<span data-ttu-id="b0509-139">In Apex Portal, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="b0509-139">In Apex Portal, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="b0509-140">To configure and test Azure AD single sign-on with Apex Portal, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="b0509-140">To configure and test Azure AD single sign-on with Apex Portal, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b0509-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="b0509-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b0509-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b0509-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b0509-143">**[Create an Apex Portal test user](#create-an-apex-online-test-user)** - to have a counterpart of Britta Simon in Apex Portal that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="b0509-143">**[Create an Apex Portal test user](#create-an-apex-online-test-user)** - to have a counterpart of Britta Simon in Apex Portal that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b0509-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="b0509-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b0509-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="b0509-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="b0509-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="b0509-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="b0509-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Apex Portal application.</span><span class="sxs-lookup"><span data-stu-id="b0509-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Apex Portal application.</span></span>

<span data-ttu-id="b0509-148">**To configure Azure AD single sign-on with Apex Portal, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b0509-148">**To configure Azure AD single sign-on with Apex Portal, perform the following steps:**</span></span>

1. <span data-ttu-id="b0509-149">In the Azure portal, on the **Apex Portal** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="b0509-149">In the Azure portal, on the **Apex Portal** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

2. <span data-ttu-id="b0509-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="b0509-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/apexportal-tutorial/tutorial_apexonline_samlbase.png)

3. <span data-ttu-id="b0509-153">On the **Apex Portal Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b0509-153">On the **Apex Portal Domain and URLs** section, perform the following steps:</span></span>

    ![Apex Portal Domain and URLs single sign-on information](./media/apexportal-tutorial/tutorial_apexonline_url.png)

    <span data-ttu-id="b0509-155">a.</span><span class="sxs-lookup"><span data-stu-id="b0509-155">a.</span></span> <span data-ttu-id="b0509-156">In the **Identifier** textbox, type a URL using the following pattern: `https://<customer name>.apexanalytix.com/saml/sso.aspx`</span><span class="sxs-lookup"><span data-stu-id="b0509-156">In the **Identifier** textbox, type a URL using the following pattern: `https://<customer name>.apexanalytix.com/saml/sso.aspx`</span></span>

    <span data-ttu-id="b0509-157">b.</span><span class="sxs-lookup"><span data-stu-id="b0509-157">b.</span></span> <span data-ttu-id="b0509-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<customer name>.apexanalytix.com/saml/sso.aspx`</span><span class="sxs-lookup"><span data-stu-id="b0509-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<customer name>.apexanalytix.com/saml/sso.aspx`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b0509-159">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="b0509-159">These values are not real.</span></span> <span data-ttu-id="b0509-160">Update these values with the actual Identifier and Reply URL.</span><span class="sxs-lookup"><span data-stu-id="b0509-160">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="b0509-161">Contact [Apex Portal support team](mailto:support@apexanalytix.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="b0509-161">Contact [Apex Portal support team](mailto:support@apexanalytix.com) to get these values.</span></span>
 
4. <span data-ttu-id="b0509-162">The Apex Portal application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span><span class="sxs-lookup"><span data-stu-id="b0509-162">The Apex Portal application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="b0509-163">Configure the following claims for this application.</span><span class="sxs-lookup"><span data-stu-id="b0509-163">Configure the following claims for this application.</span></span> <span data-ttu-id="b0509-164">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span><span class="sxs-lookup"><span data-stu-id="b0509-164">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> 

    ![Configure Single Sign-On](./media/apexportal-tutorial/attribute.png)

5. <span data-ttu-id="b0509-166">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the preceding image and perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b0509-166">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the preceding image and perform the following steps:</span></span>
    
    | <span data-ttu-id="b0509-167">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="b0509-167">Attribute Name</span></span> | <span data-ttu-id="b0509-168">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="b0509-168">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="b0509-169">FIRSTNAME</span><span class="sxs-lookup"><span data-stu-id="b0509-169">FIRSTNAME</span></span> | <span data-ttu-id="b0509-170">user.givenname</span><span class="sxs-lookup"><span data-stu-id="b0509-170">user.givenname</span></span> |
    | <span data-ttu-id="b0509-171">LASTNAME</span><span class="sxs-lookup"><span data-stu-id="b0509-171">LASTNAME</span></span> | <span data-ttu-id="b0509-172">user.surname</span><span class="sxs-lookup"><span data-stu-id="b0509-172">user.surname</span></span> |
    | <span data-ttu-id="b0509-173">MAIL</span><span class="sxs-lookup"><span data-stu-id="b0509-173">MAIL</span></span> | <span data-ttu-id="b0509-174">user.mail</span><span class="sxs-lookup"><span data-stu-id="b0509-174">user.mail</span></span> |    

    <span data-ttu-id="b0509-175">a.</span><span class="sxs-lookup"><span data-stu-id="b0509-175">a.</span></span> <span data-ttu-id="b0509-176">Click **Add attribute** to open the **Add Attribute** dialog.</span><span class="sxs-lookup"><span data-stu-id="b0509-176">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configure Single Sign-On](./media/apexportal-tutorial/tutorial_attribute_04.png)

    ![Configure Single Sign-On](./media/apexportal-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="b0509-179">b.</span><span class="sxs-lookup"><span data-stu-id="b0509-179">b.</span></span> <span data-ttu-id="b0509-180">In the **Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="b0509-180">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="b0509-181">c.</span><span class="sxs-lookup"><span data-stu-id="b0509-181">c.</span></span> <span data-ttu-id="b0509-182">From the **Value** list, type the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="b0509-182">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="b0509-183">d.</span><span class="sxs-lookup"><span data-stu-id="b0509-183">d.</span></span> <span data-ttu-id="b0509-184">Click **Ok**.</span><span class="sxs-lookup"><span data-stu-id="b0509-184">Click **Ok**.</span></span>

6. <span data-ttu-id="b0509-185">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="b0509-185">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/apexportal-tutorial/tutorial_apexonline_certificate.png) 

7. <span data-ttu-id="b0509-187">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="b0509-187">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/apexportal-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="b0509-189">To configure single sign-on on **Apex Portal** side, you need to send the downloaded **Metadata XML** to [Apex Portal support team](mailto:support@apexanalytix.com).</span><span class="sxs-lookup"><span data-stu-id="b0509-189">To configure single sign-on on **Apex Portal** side, you need to send the downloaded **Metadata XML** to [Apex Portal support team](mailto:support@apexanalytix.com).</span></span> <span data-ttu-id="b0509-190">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="b0509-190">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="b0509-191">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="b0509-191">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b0509-192">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="b0509-192">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b0509-193">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b0509-193">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="b0509-194">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="b0509-194">Create an Azure AD test user</span></span>

<span data-ttu-id="b0509-195">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b0509-195">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="b0509-197">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b0509-197">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b0509-198">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="b0509-198">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/apexportal-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="b0509-200">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="b0509-200">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/apexportal-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="b0509-202">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="b0509-202">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/apexportal-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="b0509-204">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b0509-204">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/apexportal-tutorial/create_aaduser_04.png)

    <span data-ttu-id="b0509-206">a.</span><span class="sxs-lookup"><span data-stu-id="b0509-206">a.</span></span> <span data-ttu-id="b0509-207">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b0509-207">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b0509-208">b.</span><span class="sxs-lookup"><span data-stu-id="b0509-208">b.</span></span> <span data-ttu-id="b0509-209">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b0509-209">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="b0509-210">c.</span><span class="sxs-lookup"><span data-stu-id="b0509-210">c.</span></span> <span data-ttu-id="b0509-211">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="b0509-211">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="b0509-212">d.</span><span class="sxs-lookup"><span data-stu-id="b0509-212">d.</span></span> <span data-ttu-id="b0509-213">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="b0509-213">Click **Create**.</span></span>
  
### <a name="create-an-apex-portal-test-user"></a><span data-ttu-id="b0509-214">Create an Apex Portal test user</span><span class="sxs-lookup"><span data-stu-id="b0509-214">Create an Apex Portal test user</span></span>

<span data-ttu-id="b0509-215">The objective of this section is to create a user called Britta Simon in Apex Portal.</span><span class="sxs-lookup"><span data-stu-id="b0509-215">The objective of this section is to create a user called Britta Simon in Apex Portal.</span></span> <span data-ttu-id="b0509-216">Apex Portal supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="b0509-216">Apex Portal supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="b0509-217">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="b0509-217">There is no action item for you in this section.</span></span> <span data-ttu-id="b0509-218">A new user is created during an attempt to access Apex Portal if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="b0509-218">A new user is created during an attempt to access Apex Portal if it doesn't exist yet.</span></span>
 
> [!NOTE]
> <span data-ttu-id="b0509-219">If you need to create a user manually, you need to contact the [Apex Portal support team](mailto:support@apexanalytix.com).</span><span class="sxs-lookup"><span data-stu-id="b0509-219">If you need to create a user manually, you need to contact the [Apex Portal support team](mailto:support@apexanalytix.com).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="b0509-220">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="b0509-220">Assign the Azure AD test user</span></span>

<span data-ttu-id="b0509-221">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Apex Portal.</span><span class="sxs-lookup"><span data-stu-id="b0509-221">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Apex Portal.</span></span>

![Assign the user role][200] 

<span data-ttu-id="b0509-223">**To assign Britta Simon to Apex Portal, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b0509-223">**To assign Britta Simon to Apex Portal, perform the following steps:**</span></span>

1. <span data-ttu-id="b0509-224">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="b0509-224">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="b0509-226">In the applications list, select **Apex Portal**.</span><span class="sxs-lookup"><span data-stu-id="b0509-226">In the applications list, select **Apex Portal**.</span></span>

    ![The Apex Portal link in the Applications list](./media/apexportal-tutorial/tutorial_apexonline_app.png)  

3. <span data-ttu-id="b0509-228">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="b0509-228">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

4. <span data-ttu-id="b0509-230">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="b0509-230">Click **Add** button.</span></span> <span data-ttu-id="b0509-231">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="b0509-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

5. <span data-ttu-id="b0509-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="b0509-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b0509-234">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="b0509-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b0509-235">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="b0509-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="b0509-236">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="b0509-236">Test single sign-on</span></span>

<span data-ttu-id="b0509-237">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="b0509-237">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b0509-238">When you click the Apex Portal tile in the Access Panel, you should get automatically signed-on to your Apex Portal application.</span><span class="sxs-lookup"><span data-stu-id="b0509-238">When you click the Apex Portal tile in the Access Panel, you should get automatically signed-on to your Apex Portal application.</span></span>
<span data-ttu-id="b0509-239">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b0509-239">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="b0509-240">Additional resources</span><span class="sxs-lookup"><span data-stu-id="b0509-240">Additional resources</span></span>

* [<span data-ttu-id="b0509-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b0509-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="b0509-242">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b0509-242">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/apexportal-tutorial/tutorial_general_01.png
[2]: ./media/apexportal-tutorial/tutorial_general_02.png
[3]: ./media/apexportal-tutorial/tutorial_general_03.png
[4]: ./media/apexportal-tutorial/tutorial_general_04.png

[100]: ./media/apexportal-tutorial/tutorial_general_100.png

[200]: ./media/apexportal-tutorial/tutorial_general_200.png
[201]: ./media/apexportal-tutorial/tutorial_general_201.png
[202]: ./media/apexportal-tutorial/tutorial_general_202.png
[203]: ./media/apexportal-tutorial/tutorial_general_203.png

