---
title: 'Tutorial: Azure Active Directory integration with Boomi | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Boomi.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 40d034ff-7394-4713-923d-1f8f2ed8bf36
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/03/2018
ms.author: jeedes
ms.openlocfilehash: cf925e0e0e7b6b4c10b6b21d17214f91473a9026
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856329"
---
# <a name="tutorial-azure-active-directory-integration-with-boomi"></a><span data-ttu-id="68267-103">Tutorial: Azure Active Directory integration with Boomi</span><span class="sxs-lookup"><span data-stu-id="68267-103">Tutorial: Azure Active Directory integration with Boomi</span></span>

<span data-ttu-id="68267-104">In this tutorial, you learn how to integrate Boomi with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="68267-104">In this tutorial, you learn how to integrate Boomi with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="68267-105">Integrating Boomi with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="68267-105">Integrating Boomi with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="68267-106">You can control in Azure AD who has access to Boomi.</span><span class="sxs-lookup"><span data-stu-id="68267-106">You can control in Azure AD who has access to Boomi.</span></span>
- <span data-ttu-id="68267-107">You can enable your users to automatically get signed-on to Boomi (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="68267-107">You can enable your users to automatically get signed-on to Boomi (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="68267-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="68267-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="68267-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="68267-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="68267-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="68267-110">Prerequisites</span></span>

<span data-ttu-id="68267-111">To configure Azure AD integration with Boomi, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="68267-111">To configure Azure AD integration with Boomi, you need the following items:</span></span>

- <span data-ttu-id="68267-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="68267-112">An Azure AD subscription</span></span>
- <span data-ttu-id="68267-113">A Boomi single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="68267-113">A Boomi single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="68267-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="68267-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="68267-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="68267-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="68267-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="68267-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="68267-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="68267-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="68267-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="68267-118">Scenario description</span></span>
<span data-ttu-id="68267-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="68267-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="68267-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="68267-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="68267-121">Adding Boomi from the gallery</span><span class="sxs-lookup"><span data-stu-id="68267-121">Adding Boomi from the gallery</span></span>
1. <span data-ttu-id="68267-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="68267-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-boomi-from-the-gallery"></a><span data-ttu-id="68267-123">Adding Boomi from the gallery</span><span class="sxs-lookup"><span data-stu-id="68267-123">Adding Boomi from the gallery</span></span>
<span data-ttu-id="68267-124">To configure the integration of Boomi into Azure AD, you need to add Boomi from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="68267-124">To configure the integration of Boomi into Azure AD, you need to add Boomi from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="68267-125">**To add Boomi from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="68267-125">**To add Boomi from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="68267-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="68267-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="68267-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="68267-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="68267-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="68267-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="68267-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="68267-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="68267-133">In the search box, type **Boomi**, select **Boomi** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="68267-133">In the search box, type **Boomi**, select **Boomi** from result panel then click **Add** button to add the application.</span></span>

    ![Boomi in the results list](./media/boomi-tutorial/tutorial_boomi_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="68267-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="68267-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="68267-136">In this section, you configure and test Azure AD single sign-on with Boomi based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="68267-136">In this section, you configure and test Azure AD single sign-on with Boomi based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="68267-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Boomi is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="68267-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Boomi is to a user in Azure AD.</span></span> <span data-ttu-id="68267-138">In other words, a link relationship between an Azure AD user and the related user in Boomi needs to be established.</span><span class="sxs-lookup"><span data-stu-id="68267-138">In other words, a link relationship between an Azure AD user and the related user in Boomi needs to be established.</span></span>

<span data-ttu-id="68267-139">In Boomi, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="68267-139">In Boomi, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="68267-140">To configure and test Azure AD single sign-on with Boomi, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="68267-140">To configure and test Azure AD single sign-on with Boomi, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="68267-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="68267-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="68267-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="68267-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="68267-143">**[Create a Boomi test user](#create-a-boomi-test-user)** - to have a counterpart of Britta Simon in Boomi that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="68267-143">**[Create a Boomi test user](#create-a-boomi-test-user)** - to have a counterpart of Britta Simon in Boomi that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="68267-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="68267-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="68267-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="68267-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="68267-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="68267-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="68267-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Boomi application.</span><span class="sxs-lookup"><span data-stu-id="68267-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Boomi application.</span></span>

<span data-ttu-id="68267-148">**To configure Azure AD single sign-on with Boomi, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="68267-148">**To configure Azure AD single sign-on with Boomi, perform the following steps:**</span></span>

1. <span data-ttu-id="68267-149">In the Azure portal, on the **Boomi** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="68267-149">In the Azure portal, on the **Boomi** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="68267-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="68267-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/boomi-tutorial/tutorial_boomi_samlbase.png)

1. <span data-ttu-id="68267-153">On the **Boomi Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="68267-153">On the **Boomi Domain and URLs** section, perform the following steps:</span></span>

    ![Boomi Domain and URLs single sign-on information](./media/boomi-tutorial/tutorial_boomi_url.png)

    <span data-ttu-id="68267-155">a.</span><span class="sxs-lookup"><span data-stu-id="68267-155">a.</span></span> <span data-ttu-id="68267-156">In the **Identifier** textbox, type a URL: `https://platform.boomi.com/`</span><span class="sxs-lookup"><span data-stu-id="68267-156">In the **Identifier** textbox, type a URL: `https://platform.boomi.com/`</span></span>

    <span data-ttu-id="68267-157">b.</span><span class="sxs-lookup"><span data-stu-id="68267-157">b.</span></span> <span data-ttu-id="68267-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://platform.boomi.com/sso/<boomi-tenant>/saml`</span><span class="sxs-lookup"><span data-stu-id="68267-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://platform.boomi.com/sso/<boomi-tenant>/saml`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="68267-159">The Reply URL value is not real.</span><span class="sxs-lookup"><span data-stu-id="68267-159">The Reply URL value is not real.</span></span> <span data-ttu-id="68267-160">Update the value with the actual Reply URL.</span><span class="sxs-lookup"><span data-stu-id="68267-160">Update the value with the actual Reply URL.</span></span> <span data-ttu-id="68267-161">Contact [Boomi support team](https://boomi.com/company/contact/) to get the value.</span><span class="sxs-lookup"><span data-stu-id="68267-161">Contact [Boomi support team](https://boomi.com/company/contact/) to get the value.</span></span>
 
1. <span data-ttu-id="68267-162">Boomi application expects the SAML assertions in a specific format.</span><span class="sxs-lookup"><span data-stu-id="68267-162">Boomi application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="68267-163">Please configure the following claims for this application.</span><span class="sxs-lookup"><span data-stu-id="68267-163">Please configure the following claims for this application.</span></span> <span data-ttu-id="68267-164">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span><span class="sxs-lookup"><span data-stu-id="68267-164">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="68267-165">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="68267-165">The following screenshot shows an example for this.</span></span>
    
    ![Configure Single Sign-On](./media/boomi-tutorial/tutorial_attribute.png)

1. <span data-ttu-id="68267-167">In the **User Attributes** section on the **Single sign-on** dialog, for each row shown in the table below, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="68267-167">In the **User Attributes** section on the **Single sign-on** dialog, for each row shown in the table below, perform the following steps:</span></span>

    | <span data-ttu-id="68267-168">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="68267-168">Attribute Name</span></span> | <span data-ttu-id="68267-169">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="68267-169">Attribute Value</span></span> |
    | -------------- | --------------- |
    | <span data-ttu-id="68267-170">FEDERATION_ID</span><span class="sxs-lookup"><span data-stu-id="68267-170">FEDERATION_ID</span></span> | <span data-ttu-id="68267-171">user.mail</span><span class="sxs-lookup"><span data-stu-id="68267-171">user.mail</span></span> |
    
    <span data-ttu-id="68267-172">a.</span><span class="sxs-lookup"><span data-stu-id="68267-172">a.</span></span> <span data-ttu-id="68267-173">Click **Add attribute** to open the **Add Attribute** dialog.</span><span class="sxs-lookup"><span data-stu-id="68267-173">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>
    
    ![Configure Single Sign-On](./media/boomi-tutorial/tutorial_officespace_04.png)
    
    ![Configure Single Sign-On](./media/boomi-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="68267-176">b.</span><span class="sxs-lookup"><span data-stu-id="68267-176">b.</span></span> <span data-ttu-id="68267-177">In the **Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="68267-177">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="68267-178">c.</span><span class="sxs-lookup"><span data-stu-id="68267-178">c.</span></span> <span data-ttu-id="68267-179">From the **Value** list, type the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="68267-179">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="68267-180">d.</span><span class="sxs-lookup"><span data-stu-id="68267-180">d.</span></span> <span data-ttu-id="68267-181">Click **Ok**.</span><span class="sxs-lookup"><span data-stu-id="68267-181">Click **Ok**.</span></span>

1. <span data-ttu-id="68267-182">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="68267-182">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/boomi-tutorial/tutorial_boomi_certificate.png) 

1. <span data-ttu-id="68267-184">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="68267-184">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/boomi-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="68267-186">On the **Boomi Configuration** section, click **Configure Boomi** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="68267-186">On the **Boomi Configuration** section, click **Configure Boomi** to open **Configure sign-on** window.</span></span> <span data-ttu-id="68267-187">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="68267-187">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Boomi Configuration](./media/boomi-tutorial/tutorial_boomi_configure.png) 

1. <span data-ttu-id="68267-189">In a different web browser window, log into your Boomi company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="68267-189">In a different web browser window, log into your Boomi company site as an administrator.</span></span> 

1. <span data-ttu-id="68267-190">Navigate to **Company Name** and go to **Set up**.</span><span class="sxs-lookup"><span data-stu-id="68267-190">Navigate to **Company Name** and go to **Set up**.</span></span>

1. <span data-ttu-id="68267-191">Click the **SSO Options** tab and perform below steps.</span><span class="sxs-lookup"><span data-stu-id="68267-191">Click the **SSO Options** tab and perform below steps.</span></span>

    ![Configure Single Sign-On On App Side](./media/boomi-tutorial/tutorial_boomi_11.png)

    <span data-ttu-id="68267-193">a.</span><span class="sxs-lookup"><span data-stu-id="68267-193">a.</span></span> <span data-ttu-id="68267-194">Check **Enable SAML Single Sign-On** checkbox.</span><span class="sxs-lookup"><span data-stu-id="68267-194">Check **Enable SAML Single Sign-On** checkbox.</span></span>

    <span data-ttu-id="68267-195">b.</span><span class="sxs-lookup"><span data-stu-id="68267-195">b.</span></span> <span data-ttu-id="68267-196">Click **Import** to upload the downloaded certificate from Azure AD to **Identity Provider Certificate**.</span><span class="sxs-lookup"><span data-stu-id="68267-196">Click **Import** to upload the downloaded certificate from Azure AD to **Identity Provider Certificate**.</span></span>
    
    <span data-ttu-id="68267-197">c.</span><span class="sxs-lookup"><span data-stu-id="68267-197">c.</span></span> <span data-ttu-id="68267-198">In the **Identity Provider Login URL** textbox, put the value of **SAML Single Sign-On Service URL** from Azure AD application configuration window.</span><span class="sxs-lookup"><span data-stu-id="68267-198">In the **Identity Provider Login URL** textbox, put the value of **SAML Single Sign-On Service URL** from Azure AD application configuration window.</span></span>

    <span data-ttu-id="68267-199">d.</span><span class="sxs-lookup"><span data-stu-id="68267-199">d.</span></span> <span data-ttu-id="68267-200">As **Federation Id Location**, select **Federation Id is in FEDERATION_ID Attribute element** radio button.</span><span class="sxs-lookup"><span data-stu-id="68267-200">As **Federation Id Location**, select **Federation Id is in FEDERATION_ID Attribute element** radio button.</span></span> 

    <span data-ttu-id="68267-201">e.</span><span class="sxs-lookup"><span data-stu-id="68267-201">e.</span></span> <span data-ttu-id="68267-202">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="68267-202">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="68267-203">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="68267-203">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="68267-204">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="68267-204">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="68267-205">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="68267-205">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="68267-206">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="68267-206">Create an Azure AD test user</span></span>

<span data-ttu-id="68267-207">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="68267-207">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="68267-209">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="68267-209">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="68267-210">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="68267-210">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/boomi-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="68267-212">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="68267-212">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/boomi-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="68267-214">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="68267-214">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/boomi-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="68267-216">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="68267-216">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/boomi-tutorial/create_aaduser_04.png)

    <span data-ttu-id="68267-218">a.</span><span class="sxs-lookup"><span data-stu-id="68267-218">a.</span></span> <span data-ttu-id="68267-219">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="68267-219">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="68267-220">b.</span><span class="sxs-lookup"><span data-stu-id="68267-220">b.</span></span> <span data-ttu-id="68267-221">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="68267-221">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="68267-222">c.</span><span class="sxs-lookup"><span data-stu-id="68267-222">c.</span></span> <span data-ttu-id="68267-223">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="68267-223">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="68267-224">d.</span><span class="sxs-lookup"><span data-stu-id="68267-224">d.</span></span> <span data-ttu-id="68267-225">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="68267-225">Click **Create**.</span></span>
  
### <a name="create-a-boomi-test-user"></a><span data-ttu-id="68267-226">Create a Boomi test user</span><span class="sxs-lookup"><span data-stu-id="68267-226">Create a Boomi test user</span></span>

<span data-ttu-id="68267-227">In order to enable Azure AD users to log in to Boomi, they must be provisioned into Boomi.</span><span class="sxs-lookup"><span data-stu-id="68267-227">In order to enable Azure AD users to log in to Boomi, they must be provisioned into Boomi.</span></span> <span data-ttu-id="68267-228">In the case of Boomi, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="68267-228">In the case of Boomi, provisioning is a manual task.</span></span>

### <a name="to-provision-a-user-account-perform-the-following-steps"></a><span data-ttu-id="68267-229">To provision a user account, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="68267-229">To provision a user account, perform the following steps:</span></span>

1. <span data-ttu-id="68267-230">Log in to your Boomi company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="68267-230">Log in to your Boomi company site as an administrator.</span></span>

1. <span data-ttu-id="68267-231">After logging in, navigate to **User Management** and go to **Users**.</span><span class="sxs-lookup"><span data-stu-id="68267-231">After logging in, navigate to **User Management** and go to **Users**.</span></span>

    <span data-ttu-id="68267-232">![Users](./media/boomi-tutorial/tutorial_boomi_001.png "Users")</span><span class="sxs-lookup"><span data-stu-id="68267-232">![Users](./media/boomi-tutorial/tutorial_boomi_001.png "Users")</span></span>

1. <span data-ttu-id="68267-233">Click **+**  icon and the **Add/Maintain User Roles** dialog opens.</span><span class="sxs-lookup"><span data-stu-id="68267-233">Click **+**  icon and the **Add/Maintain User Roles** dialog opens.</span></span>

    <span data-ttu-id="68267-234">![Users](./media/boomi-tutorial/tutorial_boomi_002.png "Users")</span><span class="sxs-lookup"><span data-stu-id="68267-234">![Users](./media/boomi-tutorial/tutorial_boomi_002.png "Users")</span></span>

    <span data-ttu-id="68267-235">![Users](./media/boomi-tutorial/tutorial_boomi_003.png "Users")</span><span class="sxs-lookup"><span data-stu-id="68267-235">![Users](./media/boomi-tutorial/tutorial_boomi_003.png "Users")</span></span>

    <span data-ttu-id="68267-236">a.</span><span class="sxs-lookup"><span data-stu-id="68267-236">a.</span></span> <span data-ttu-id="68267-237">In the **User e-mail address** textbox, type the email of user like BrittaSimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="68267-237">In the **User e-mail address** textbox, type the email of user like BrittaSimon@contoso.com.</span></span>
    
    <span data-ttu-id="68267-238">b.</span><span class="sxs-lookup"><span data-stu-id="68267-238">b.</span></span> <span data-ttu-id="68267-239">In the **First name** textbox, type the First name of user like Britta.</span><span class="sxs-lookup"><span data-stu-id="68267-239">In the **First name** textbox, type the First name of user like Britta.</span></span>

    <span data-ttu-id="68267-240">c.</span><span class="sxs-lookup"><span data-stu-id="68267-240">c.</span></span> <span data-ttu-id="68267-241">In the **Last name** textbox, type the Last name of user like Simon.</span><span class="sxs-lookup"><span data-stu-id="68267-241">In the **Last name** textbox, type the Last name of user like Simon.</span></span>
    
    <span data-ttu-id="68267-242">d.</span><span class="sxs-lookup"><span data-stu-id="68267-242">d.</span></span> <span data-ttu-id="68267-243">Enter the user's **Federation ID**.</span><span class="sxs-lookup"><span data-stu-id="68267-243">Enter the user's **Federation ID**.</span></span> <span data-ttu-id="68267-244">Each user must have a Federation ID that uniquely identifies the user within the account.</span><span class="sxs-lookup"><span data-stu-id="68267-244">Each user must have a Federation ID that uniquely identifies the user within the account.</span></span>
    
    <span data-ttu-id="68267-245">e.</span><span class="sxs-lookup"><span data-stu-id="68267-245">e.</span></span> <span data-ttu-id="68267-246">Assign the **Standard User** role to the user.</span><span class="sxs-lookup"><span data-stu-id="68267-246">Assign the **Standard User** role to the user.</span></span> <span data-ttu-id="68267-247">Do not assign the Administrator role because that would give him normal Atmosphere access as well as single sign-on access.</span><span class="sxs-lookup"><span data-stu-id="68267-247">Do not assign the Administrator role because that would give him normal Atmosphere access as well as single sign-on access.</span></span>
    
    <span data-ttu-id="68267-248">f.</span><span class="sxs-lookup"><span data-stu-id="68267-248">f.</span></span> <span data-ttu-id="68267-249">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="68267-249">Click **OK**.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="68267-250">The user will not receive a welcome notification email containing a password that can be used to log in to the AtomSphere account because his password is managed through the identity provider.</span><span class="sxs-lookup"><span data-stu-id="68267-250">The user will not receive a welcome notification email containing a password that can be used to log in to the AtomSphere account because his password is managed through the identity provider.</span></span> <span data-ttu-id="68267-251">You may use any other Boomi user account creation tools or APIs provided by Boomi to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="68267-251">You may use any other Boomi user account creation tools or APIs provided by Boomi to provision AAD user accounts.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="68267-252">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="68267-252">Assign the Azure AD test user</span></span>

<span data-ttu-id="68267-253">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Boomi.</span><span class="sxs-lookup"><span data-stu-id="68267-253">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Boomi.</span></span>

![Assign the user role][200] 

<span data-ttu-id="68267-255">**To assign Britta Simon to Boomi, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="68267-255">**To assign Britta Simon to Boomi, perform the following steps:**</span></span>

1. <span data-ttu-id="68267-256">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="68267-256">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="68267-258">In the applications list, select **Boomi**.</span><span class="sxs-lookup"><span data-stu-id="68267-258">In the applications list, select **Boomi**.</span></span>

    ![The Boomi link in the Applications list](./media/boomi-tutorial/tutorial_boomi_app.png)  

1. <span data-ttu-id="68267-260">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="68267-260">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="68267-262">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="68267-262">Click **Add** button.</span></span> <span data-ttu-id="68267-263">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="68267-263">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="68267-265">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="68267-265">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="68267-266">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="68267-266">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="68267-267">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="68267-267">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="68267-268">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="68267-268">Test single sign-on</span></span>

<span data-ttu-id="68267-269">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="68267-269">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="68267-270">When you click the Boomi tile in the Access Panel, you should get automatically signed-on to your Boomi application.</span><span class="sxs-lookup"><span data-stu-id="68267-270">When you click the Boomi tile in the Access Panel, you should get automatically signed-on to your Boomi application.</span></span>
<span data-ttu-id="68267-271">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="68267-271">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="68267-272">Additional resources</span><span class="sxs-lookup"><span data-stu-id="68267-272">Additional resources</span></span>

* [<span data-ttu-id="68267-273">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="68267-273">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="68267-274">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="68267-274">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/boomi-tutorial/tutorial_general_01.png
[2]: ./media/boomi-tutorial/tutorial_general_02.png
[3]: ./media/boomi-tutorial/tutorial_general_03.png
[4]: ./media/boomi-tutorial/tutorial_general_04.png

[100]: ./media/boomi-tutorial/tutorial_general_100.png

[200]: ./media/boomi-tutorial/tutorial_general_200.png
[201]: ./media/boomi-tutorial/tutorial_general_201.png
[202]: ./media/boomi-tutorial/tutorial_general_202.png
[203]: ./media/boomi-tutorial/tutorial_general_203.png

