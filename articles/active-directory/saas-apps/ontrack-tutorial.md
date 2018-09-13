---
title: 'Tutorial: Azure Active Directory integration with OnTrack | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and OnTrack.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: d2cafba2-3b4a-4471-ba34-80f6a96ff2b9
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2017
ms.author: jeedes
ms.openlocfilehash: 82e0788ad2f1e49cb593e504adc1e826516d4616
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868407"
---
# <a name="tutorial-azure-active-directory-integration-with-ontrack"></a><span data-ttu-id="50c39-103">Tutorial: Azure Active Directory integration with OnTrack</span><span class="sxs-lookup"><span data-stu-id="50c39-103">Tutorial: Azure Active Directory integration with OnTrack</span></span>

<span data-ttu-id="50c39-104">In this tutorial, you learn how to integrate OnTrack with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="50c39-104">In this tutorial, you learn how to integrate OnTrack with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="50c39-105">Integrating OnTrack with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="50c39-105">Integrating OnTrack with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="50c39-106">You can control in Azure AD who has access to OnTrack.</span><span class="sxs-lookup"><span data-stu-id="50c39-106">You can control in Azure AD who has access to OnTrack.</span></span>
- <span data-ttu-id="50c39-107">You can enable your users to automatically get signed-on to OnTrack (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="50c39-107">You can enable your users to automatically get signed-on to OnTrack (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="50c39-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="50c39-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="50c39-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="50c39-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="50c39-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="50c39-110">Prerequisites</span></span>

<span data-ttu-id="50c39-111">To configure Azure AD integration with OnTrack, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="50c39-111">To configure Azure AD integration with OnTrack, you need the following items:</span></span>

- <span data-ttu-id="50c39-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="50c39-112">An Azure AD subscription</span></span>
- <span data-ttu-id="50c39-113">An OnTrack single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="50c39-113">An OnTrack single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="50c39-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="50c39-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="50c39-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="50c39-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="50c39-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="50c39-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="50c39-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="50c39-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="50c39-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="50c39-118">Scenario description</span></span>
<span data-ttu-id="50c39-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="50c39-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="50c39-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="50c39-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="50c39-121">Adding OnTrack from the gallery</span><span class="sxs-lookup"><span data-stu-id="50c39-121">Adding OnTrack from the gallery</span></span>
1. <span data-ttu-id="50c39-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="50c39-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ontrack-from-the-gallery"></a><span data-ttu-id="50c39-123">Adding OnTrack from the gallery</span><span class="sxs-lookup"><span data-stu-id="50c39-123">Adding OnTrack from the gallery</span></span>
<span data-ttu-id="50c39-124">To configure the integration of OnTrack into Azure AD, you need to add OnTrack from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="50c39-124">To configure the integration of OnTrack into Azure AD, you need to add OnTrack from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="50c39-125">**To add OnTrack from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="50c39-125">**To add OnTrack from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="50c39-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="50c39-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="50c39-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="50c39-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="50c39-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="50c39-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="50c39-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="50c39-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="50c39-133">In the search box, type **OnTrack**, select **OnTrack** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="50c39-133">In the search box, type **OnTrack**, select **OnTrack** from result panel then click **Add** button to add the application.</span></span>

    ![OnTrack in the results list](./media/ontrack-tutorial/tutorial_ontrack_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="50c39-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="50c39-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="50c39-136">In this section, you configure and test Azure AD single sign-on with OnTrack based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="50c39-136">In this section, you configure and test Azure AD single sign-on with OnTrack based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="50c39-137">For single sign-on to work, Azure AD needs to know what the counterpart user in OnTrack is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="50c39-137">For single sign-on to work, Azure AD needs to know what the counterpart user in OnTrack is to a user in Azure AD.</span></span> <span data-ttu-id="50c39-138">In other words, a link relationship between an Azure AD user and the related user in OnTrack needs to be established.</span><span class="sxs-lookup"><span data-stu-id="50c39-138">In other words, a link relationship between an Azure AD user and the related user in OnTrack needs to be established.</span></span>

<span data-ttu-id="50c39-139">In OnTrack, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="50c39-139">In OnTrack, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="50c39-140">To configure and test Azure AD single sign-on with OnTrack, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="50c39-140">To configure and test Azure AD single sign-on with OnTrack, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="50c39-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="50c39-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="50c39-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="50c39-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="50c39-143">**[Create an OnTrack test user](#create-an-ontrack-test-user)** - to have a counterpart of Britta Simon in OnTrack that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="50c39-143">**[Create an OnTrack test user](#create-an-ontrack-test-user)** - to have a counterpart of Britta Simon in OnTrack that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="50c39-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="50c39-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="50c39-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="50c39-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="50c39-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="50c39-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="50c39-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your OnTrack application.</span><span class="sxs-lookup"><span data-stu-id="50c39-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your OnTrack application.</span></span>

<span data-ttu-id="50c39-148">**To configure Azure AD single sign-on with OnTrack, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="50c39-148">**To configure Azure AD single sign-on with OnTrack, perform the following steps:**</span></span>

1. <span data-ttu-id="50c39-149">In the Azure portal, on the **OnTrack** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="50c39-149">In the Azure portal, on the **OnTrack** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="50c39-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="50c39-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/ontrack-tutorial/tutorial_ontrack_samlbase.png)

1. <span data-ttu-id="50c39-153">On the **OnTrack Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="50c39-153">On the **OnTrack Domain and URLs** section, perform the following steps:</span></span>

    ![OnTrack Domain and URLs single sign-on information](./media/ontrack-tutorial/tutorial_ontrack_url.png)

    <span data-ttu-id="50c39-155">a.</span><span class="sxs-lookup"><span data-stu-id="50c39-155">a.</span></span> <span data-ttu-id="50c39-156">In the **Identifier** textbox,</span><span class="sxs-lookup"><span data-stu-id="50c39-156">In the **Identifier** textbox,</span></span>
    
    <span data-ttu-id="50c39-157">For the testing environment, type the URL: `https://staging.insigniagroup.com/sso`</span><span class="sxs-lookup"><span data-stu-id="50c39-157">For the testing environment, type the URL: `https://staging.insigniagroup.com/sso`</span></span>

    <span data-ttu-id="50c39-158">For the production environment, type the URL: `https://oeaccessories.com/sso`</span><span class="sxs-lookup"><span data-stu-id="50c39-158">For the production environment, type the URL: `https://oeaccessories.com/sso`</span></span>

    <span data-ttu-id="50c39-159">b.</span><span class="sxs-lookup"><span data-stu-id="50c39-159">b.</span></span> <span data-ttu-id="50c39-160">In the **Reply URL** textbox,</span><span class="sxs-lookup"><span data-stu-id="50c39-160">In the **Reply URL** textbox,</span></span>
    
    <span data-ttu-id="50c39-161">For the testing environment, type the URL: `https://indie.staging.insigniagroup.com/sso/autonation.aspx`</span><span class="sxs-lookup"><span data-stu-id="50c39-161">For the testing environment, type the URL: `https://indie.staging.insigniagroup.com/sso/autonation.aspx`</span></span>

    <span data-ttu-id="50c39-162">For the production environment, type the URL: `https://igaccessories.com/sso/autonation.aspx`</span><span class="sxs-lookup"><span data-stu-id="50c39-162">For the production environment, type the URL: `https://igaccessories.com/sso/autonation.aspx`</span></span>

1. <span data-ttu-id="50c39-163">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="50c39-163">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/ontrack-tutorial/tutorial_ontrack_certificate.png)

1. <span data-ttu-id="50c39-165">The OnTrack application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span><span class="sxs-lookup"><span data-stu-id="50c39-165">The OnTrack application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="50c39-166">Configure the following claims for this application.</span><span class="sxs-lookup"><span data-stu-id="50c39-166">Configure the following claims for this application.</span></span> <span data-ttu-id="50c39-167">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span><span class="sxs-lookup"><span data-stu-id="50c39-167">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> 

    ![Configure Single Sign-On](./media/ontrack-tutorial/tutorial_attribute.png)

1. <span data-ttu-id="50c39-169">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the preceding image and perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="50c39-169">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the preceding image and perform the following steps:</span></span>
    
    | <span data-ttu-id="50c39-170">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="50c39-170">Attribute Name</span></span> | <span data-ttu-id="50c39-171">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="50c39-171">Attribute Value</span></span> |
    | -------------- | ----------------|    
    | <span data-ttu-id="50c39-172">User-Role</span><span class="sxs-lookup"><span data-stu-id="50c39-172">User-Role</span></span>      | <span data-ttu-id="50c39-173">"42F432"</span><span class="sxs-lookup"><span data-stu-id="50c39-173">"42F432"</span></span> |
    | <span data-ttu-id="50c39-174">Hyperion-Code</span><span class="sxs-lookup"><span data-stu-id="50c39-174">Hyperion-Code</span></span>  | <span data-ttu-id="50c39-175">"12345"</span><span class="sxs-lookup"><span data-stu-id="50c39-175">"12345"</span></span> |

    > [!NOTE]
    > <span data-ttu-id="50c39-176">**User-Role** and **Hyperion-Code** attributes are mapped with Autonation User Role and Dealer Code respectively.</span><span class="sxs-lookup"><span data-stu-id="50c39-176">**User-Role** and **Hyperion-Code** attributes are mapped with Autonation User Role and Dealer Code respectively.</span></span> <span data-ttu-id="50c39-177">These values are example only, please use the correct code for your integration.</span><span class="sxs-lookup"><span data-stu-id="50c39-177">These values are example only, please use the correct code for your integration.</span></span> <span data-ttu-id="50c39-178">You can contact [Autonation support](mailto:CustomerService@insigniagroup.com) for these values.</span><span class="sxs-lookup"><span data-stu-id="50c39-178">You can contact [Autonation support](mailto:CustomerService@insigniagroup.com) for these values.</span></span>
    
    <span data-ttu-id="50c39-179">a.</span><span class="sxs-lookup"><span data-stu-id="50c39-179">a.</span></span> <span data-ttu-id="50c39-180">Click **Add attribute** to open the **Add Attribute** dialog.</span><span class="sxs-lookup"><span data-stu-id="50c39-180">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configure Single Sign-On](./media/ontrack-tutorial/tutorial_attribute_04.png) 

    ![Configure Single Sign-On](./media/ontrack-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="50c39-183">b.</span><span class="sxs-lookup"><span data-stu-id="50c39-183">b.</span></span> <span data-ttu-id="50c39-184">In the **Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="50c39-184">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="50c39-185">c.</span><span class="sxs-lookup"><span data-stu-id="50c39-185">c.</span></span> <span data-ttu-id="50c39-186">From the **Value** list, type the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="50c39-186">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="50c39-187">d.</span><span class="sxs-lookup"><span data-stu-id="50c39-187">d.</span></span> <span data-ttu-id="50c39-188">Click **Ok**.</span><span class="sxs-lookup"><span data-stu-id="50c39-188">Click **Ok**.</span></span>

1. <span data-ttu-id="50c39-189">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="50c39-189">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/ontrack-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="50c39-191">To configure single sign-on on **OnTrack** side, you need to send the downloaded **Metadata XML** to [OnTrack support team](mailto:CustomerService@insigniagroup.com).</span><span class="sxs-lookup"><span data-stu-id="50c39-191">To configure single sign-on on **OnTrack** side, you need to send the downloaded **Metadata XML** to [OnTrack support team](mailto:CustomerService@insigniagroup.com).</span></span> <span data-ttu-id="50c39-192">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="50c39-192">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="50c39-193">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="50c39-193">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="50c39-194">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="50c39-194">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="50c39-195">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="50c39-195">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="50c39-196">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="50c39-196">Create an Azure AD test user</span></span>

<span data-ttu-id="50c39-197">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="50c39-197">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="50c39-199">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="50c39-199">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="50c39-200">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="50c39-200">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/ontrack-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="50c39-202">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="50c39-202">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/ontrack-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="50c39-204">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="50c39-204">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/ontrack-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="50c39-206">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="50c39-206">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/ontrack-tutorial/create_aaduser_04.png)

    <span data-ttu-id="50c39-208">a.</span><span class="sxs-lookup"><span data-stu-id="50c39-208">a.</span></span> <span data-ttu-id="50c39-209">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="50c39-209">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="50c39-210">b.</span><span class="sxs-lookup"><span data-stu-id="50c39-210">b.</span></span> <span data-ttu-id="50c39-211">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="50c39-211">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="50c39-212">c.</span><span class="sxs-lookup"><span data-stu-id="50c39-212">c.</span></span> <span data-ttu-id="50c39-213">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="50c39-213">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="50c39-214">d.</span><span class="sxs-lookup"><span data-stu-id="50c39-214">d.</span></span> <span data-ttu-id="50c39-215">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="50c39-215">Click **Create**.</span></span>
 
### <a name="create-an-ontrack-test-user"></a><span data-ttu-id="50c39-216">Create an OnTrack test user</span><span class="sxs-lookup"><span data-stu-id="50c39-216">Create an OnTrack test user</span></span>

<span data-ttu-id="50c39-217">In this section, you create a user called Britta Simon in OnTrack.</span><span class="sxs-lookup"><span data-stu-id="50c39-217">In this section, you create a user called Britta Simon in OnTrack.</span></span> <span data-ttu-id="50c39-218">Work with [OnTrack support team](mailto:CustomerService@insigniagroup.com) to add the users in the OnTrack platform.</span><span class="sxs-lookup"><span data-stu-id="50c39-218">Work with [OnTrack support team](mailto:CustomerService@insigniagroup.com) to add the users in the OnTrack platform.</span></span> <span data-ttu-id="50c39-219">Users must be created and activated before you use single sign-on.</span><span class="sxs-lookup"><span data-stu-id="50c39-219">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="50c39-220">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="50c39-220">Assign the Azure AD test user</span></span>

<span data-ttu-id="50c39-221">In this section, you enable Britta Simon to use Azure single sign-on by granting access to OnTrack.</span><span class="sxs-lookup"><span data-stu-id="50c39-221">In this section, you enable Britta Simon to use Azure single sign-on by granting access to OnTrack.</span></span>

![Assign the user role][200] 

<span data-ttu-id="50c39-223">**To assign Britta Simon to OnTrack, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="50c39-223">**To assign Britta Simon to OnTrack, perform the following steps:**</span></span>

1. <span data-ttu-id="50c39-224">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="50c39-224">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="50c39-226">In the applications list, select **OnTrack**.</span><span class="sxs-lookup"><span data-stu-id="50c39-226">In the applications list, select **OnTrack**.</span></span>

    ![The OnTrack link in the Applications list](./media/ontrack-tutorial/tutorial_ontrack_app.png)  

1. <span data-ttu-id="50c39-228">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="50c39-228">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="50c39-230">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="50c39-230">Click **Add** button.</span></span> <span data-ttu-id="50c39-231">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="50c39-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="50c39-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="50c39-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="50c39-234">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="50c39-234">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="50c39-235">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="50c39-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="50c39-236">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="50c39-236">Test single sign-on</span></span>

<span data-ttu-id="50c39-237">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="50c39-237">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="50c39-238">When you click the OnTrack tile in the Access Panel, you should get automatically signed-on to your OnTrack application.</span><span class="sxs-lookup"><span data-stu-id="50c39-238">When you click the OnTrack tile in the Access Panel, you should get automatically signed-on to your OnTrack application.</span></span>
<span data-ttu-id="50c39-239">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="50c39-239">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="50c39-240">Additional resources</span><span class="sxs-lookup"><span data-stu-id="50c39-240">Additional resources</span></span>

* [<span data-ttu-id="50c39-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="50c39-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="50c39-242">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="50c39-242">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/ontrack-tutorial/tutorial_general_01.png
[2]: ./media/ontrack-tutorial/tutorial_general_02.png
[3]: ./media/ontrack-tutorial/tutorial_general_03.png
[4]: ./media/ontrack-tutorial/tutorial_general_04.png

[100]: ./media/ontrack-tutorial/tutorial_general_100.png

[200]: ./media/ontrack-tutorial/tutorial_general_200.png
[201]: ./media/ontrack-tutorial/tutorial_general_201.png
[202]: ./media/ontrack-tutorial/tutorial_general_202.png
[203]: ./media/ontrack-tutorial/tutorial_general_203.png

